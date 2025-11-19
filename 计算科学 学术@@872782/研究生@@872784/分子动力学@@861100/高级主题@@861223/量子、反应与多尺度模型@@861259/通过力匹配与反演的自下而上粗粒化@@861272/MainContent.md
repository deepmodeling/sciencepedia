## 引言
分子动力学（MD）模拟是探索原子尺度世界的强大窗口，但其巨大的计算成本往往限制了我们研究复杂生物分子或材料在长时间、大尺度下行为的能力。粗粒化（Coarse-Graining, CG）建模通过将多个原子合并为一个“超原子”或CG珠，显著降低了系统的自由度，从而成为连接微观细节与宏观现象的关键桥梁。然而，一个根本性的问题随之而来：我们如何系统性地构建一个既能保持[计算效率](@entry_id:270255)，又能忠实反映底层全原子物理特性的CG模型？

本文旨在深入解答这一问题，系统介绍自下而上（bottom-up）粗粒化的两大支柱方法：力匹配（Force Matching）和结构反演（Structural Inversion）。我们将引导读者穿越这一前沿领域的核心地带，从理论基石到实践前沿。

在**第一章：原理与机制**中，我们将深入剖析这些方法背后的[统计力](@entry_id:194984)学原理，阐明它们与[平均力势](@entry_id:137947)（PMF）的深刻联系，并探讨其数值实现的核心算法。在**第二章：应用与[交叉](@entry_id:147634)学科联系**中，我们将超越基础理论，探讨如何通过融合物理知识与数据科学思想来提升模型的真实性和可移植性，应对实际模拟中的挑战，并建立与[统计推断](@entry_id:172747)、信息论等领域的联系。最后，在**第三章：动手实践**中，你将通过一系列精心设计的编程练习，将理论知识转化为实际的建模技能。通过这趟旅程，你将掌握构建高质量CG模型的关键原理与实用技术。

## 原理与机制

在上一章中，我们介绍了自下而上粗粒化建[模的基](@entry_id:156416)本思想，即旨在构建一个简化的粗粒度（Coarse-Grained, CG）模型，使其能够重现由高精度、全原子（All-Atom, AA）模拟所描述的系统的关键物理特性。本章将深入探讨实现这一目标的核心原理与机制，重点关注两种主流方法：力匹配（Force Matching）和结构反演（Structural Inversion）。我们将从这些方法的理论基础出发，探讨它们的实际应用、数值挑战，并最终深入剖析其内在的局限性与高级概念。

### 粗粒化目标：匹配结构还是力？

构建CG势能函数 $U_{\text{CG}}(\mathbf{R})$ 的首要任务是明确我们的优化目标。我们究竟希望CG模型重现全原子系统的哪种特性？通常，目标可以分为两大类：平衡结构特性和作用在CG坐标上的[平均力](@entry_id:170826)。

#### 结构匹配与[平均力势](@entry_id:137947)

从[统计力](@entry_id:194984)学的角度来看，一个系统的所有平衡结构性质都蕴含在其[平衡概率](@entry_id:187870)[分布](@entry_id:182848) $P(\mathbf{R})$ 中，其中 $\mathbf{R}$ 是CG坐标。该[分布](@entry_id:182848)可以通过对与特定CG构型 $\mathbf{R}$ 相对应的所有微观状态进行积分（或求和）来获得：

$$
P(\mathbf{R}) \propto \int \delta(\mathbf{R} - \mathcal{M}(\mathbf{x})) \exp(-\beta U_{\text{AA}}(\mathbf{x})) \, d\mathbf{x}
$$

其中 $\mathcal{M}$ 是从全原子坐标 $\mathbf{x}$到CG坐标 $\mathbf{R}$ 的映射函数，$U_{\text{AA}}$ 是全原子势能，$\beta = 1/(k_B T)$ 是[逆温](@entry_id:140086)度。

这个CG坐标的[平衡分布](@entry_id:263943)定义了一个核心的理论量，即**[平均力势](@entry_id:137947)**（Potential of Mean Force, PMF），记为 $U_{\text{PMF}}(\mathbf{R})$：

$$
U_{\text{PMF}}(\mathbf{R}) = - \frac{1}{\beta} \ln P(\mathbf{R}) + C
$$

其中 $C$ 是一个任意常数。$U_{\text{PMF}}$ 是一个自由能[曲面](@entry_id:267450)，它精确地描述了CG坐标在平衡态下的统计行为。因此，一个理想的CG[势能函数](@entry_id:200753) $U_{\text{CG}}(\mathbf{R})$ 应该尽可能地逼近 $U_{\text{PMF}}(\mathbf{R})$。

评估两个[概率分布](@entry_id:146404) $p^\star(\mathbf{R})$（由PMF导出的[目标分布](@entry_id:634522)）和 $p_\theta(\mathbf{R})$（由CG模型 $U_\theta(\mathbf{R})$ 导出的[分布](@entry_id:182848)）之间相似性的一个严格方法是计算它们之间的**[相对熵](@entry_id:263920)**（Relative Entropy），也称为**库尔贝克-莱布勒散度**（Kullback-Leibler Divergence, KLD）：

$$
S_{\text{rel}}(p^\star || p_\theta) = \int p^\star(\mathbf{R}) \ln \frac{p^\star(\mathbf{R})}{p_\theta(\mathbf{R})} \, d\mathbf{R}
$$

$S_{\text{rel}}$ 总是非负的，当且仅当 $p_\theta = p^\star$ 时等于零。因此，通过最小化[相对熵](@entry_id:263920)来优化CG[势能](@entry_id:748988)参数 $\boldsymbol{\theta}$，是一种以结构为目标的、原则性的粗粒化方法。

#### 力匹配

与关注最终的平衡结构不同，**力匹配**（Force Matching）方法旨在直接匹配作用在CG粒子上的**[平均力](@entry_id:170826)**。对于给定的CG构型 $\mathbf{R}$，其上的[平均力](@entry_id:170826)是所有映射到该CG构型的微观状态下，作用在CG粒子上的瞬时原子力的[条件期望](@entry_id:159140)：

$$
\mathbf{F}^\star(\mathbf{R}) = \mathbb{E}[\mathbf{F}_{\text{AA}} | \mathcal{M}(\mathbf{x}) = \mathbf{R}]
$$

值得注意的是，如果CG映射 $\mathcal{M}$ 是线性的，这个[平均力](@entry_id:170826)与PMF的梯度精确相关：$\mathbf{F}^\star(\mathbf{R}) = -\nabla U_{\text{PMF}}(\mathbf{R})$。

力匹配的目标是最小化CG模型力 $\mathbf{F}_\theta(\mathbf{R}) = -\nabla U_\theta(\mathbf{R})$ 与目标[平均力](@entry_id:170826) $\mathbf{F}^\star(\mathbf{R})$ 之间的[均方差](@entry_id:153618)。[目标函数](@entry_id:267263)通常定义为：

$$
J(\boldsymbol{\theta}) = \int p^\star(\mathbf{R}) \left| \mathbf{F}_\theta(\mathbf{R}) - \mathbf{F}^\star(\mathbf{R}) \right|^2 \, d\mathbf{R}
$$

其中积分是按目标分布 $p^\star(\mathbf{R})$ 进行加权的。

#### 理想条件下的等价性

结构匹配与力匹配这两种看似不同的方法，在理想条件下是等价的。这里的“理想条件”主要是指CG[势能函数](@entry_id:200753) $U_\theta(\mathbf{R})$ 的函数形式足够灵活，能够精确地表示真实的PMF。

我们可以通过一个简单的思想实验来理解这一点 [@problem_id:3399922]。考虑一个一维系统，其PMF是二次的，$U^{\star}(R) = \frac{1}{2}\alpha R^2$，对应的[目标分布](@entry_id:634522)是一个[高斯分布](@entry_id:154414) $p^{\star}(R) \propto \exp(-\frac{1}{2}\beta \alpha R^2)$。我们使用一个同样是二次形式的CG模型势 $U_{\theta}(R) = \frac{1}{2}\theta R^2$。

*   通过**最小化[相对熵](@entry_id:263920)** $S_{\text{rel}}(p^{\star}\|p_{\theta})$，我们可以推导出最优参数为 $\theta = \alpha$。
*   另一方面，我们计算目标力 $F^{\star}(R) = -\frac{d}{dR}U^{\star}(R) = -\alpha R$ 和模型力 $F_{\theta}(R) = -\theta R$。通过**最小化力匹配[目标函数](@entry_id:267263)** $J(\theta) = \int p^{\star}(R) (F_{\theta}(R) - F^{\star}(R))^2 dR$，我们同样可以得到最优参数为 $\theta = \alpha$。

这个例子清晰地表明，当CG模型能够完美描述PMF时（即模型“设定正确”），最小化结构差异（[相对熵](@entry_id:263920)）与最小化力的差异（力匹配）将得到相同的结果。这为力匹[配方法](@entry_id:265480)的合理性提供了坚实的理论基础。在实践中，由于力是PMF的[一阶导数](@entry_id:749425)，[对力](@entry_id:159909)的拟合通常比直接拟合PMF本身（一个高维自由能[曲面](@entry_id:267450)）在数值上更为稳健和高效。

### 力匹[配方法](@entry_id:265480)

力匹[配方法](@entry_id:265480)的核心优势在于其可以将[参数优化](@entry_id:151785)问题转化为一个标准的线性最小二乘问题，这使得求解过程非常高效。

#### 线性最小二乘公式

假设我们的CG势能函数对参数 $\boldsymbol{\theta}$ 是线性的，例如，表示为一组[基函数](@entry_id:170178) $\phi_i(\mathbf{R})$ 的线性组合：

$$
U_{\text{CG}}(\mathbf{R}; \boldsymbol{\theta}) = \sum_{i=1}^{M} \theta_i \phi_i(\mathbf{R})
$$

那么，CG力同样是参数的线性函数：

$$
\mathbf{F}_{\text{CG}}(\mathbf{R}; \boldsymbol{\theta}) = -\nabla U_{\text{CG}}(\mathbf{R}; \boldsymbol{\theta}) = -\sum_{i=1}^{M} \theta_i \nabla \phi_i(\mathbf{R})
$$

力匹配的目标函数是在一个从[全原子模拟](@entry_id:202465)中得到的包含 $N$ 个快照的轨迹上，最小化力的[残差平方和](@entry_id:174395)：

$$
J(\boldsymbol{\theta}) = \frac{1}{2} \sum_{j=1}^{N} \left| \mathbf{F}_{j}^{\text{AA}} - \mathbf{F}_{\text{CG}}(\mathbf{R}_j; \boldsymbol{\theta}) \right|^2
$$

其中 $\mathbf{F}_{j}^{\text{AA}}$ 是第 $j$ 个快照的目标（平均）力。

为了找到最优参数 $\boldsymbol{\theta}^\star$，我们令目标函数对每个参数 $\theta_i$ 的[偏导数](@entry_id:146280)为零，即 $\frac{\partial J}{\partial \theta_i} = 0$。这个[一阶最优性条件](@entry_id:634945)可以推导为一个优美的[正交性条件](@entry_id:168905) [@problem_id:3399890]：

$$
\left\langle \left( \mathbf{F}^{\text{AA}} + \nabla U_{\text{CG}}(\mathbf{R}; \boldsymbol{\theta}) \right) \cdot \left( \nabla \frac{\partial U_{\text{CG}}}{\partial \theta_i} \right) \right\rangle = 0
$$

这里的 $\langle \cdot \rangle$ 表示在全原子轨迹上的样本平均。这个公式的几何解释是，在最优解处，力的[残差向量](@entry_id:165091) $(\mathbf{F}^{\text{AA}} - \mathbf{F}_{\text{CG}})$ 必须与由模型力对各参数的“敏感度”向量 $\nabla \frac{\partial U_{\text{CG}}}{\partial \theta_i}$ 所张成的[子空间](@entry_id:150286)正交。

将[线性势](@entry_id:160860)能的表达式代入，上述条件最终可以化为一组线性方程组，即**正规方程**（Normal Equations）：

$$
\mathbf{A} \boldsymbol{\theta} = \mathbf{b}
$$

其中矩阵 $\mathbf{A}$ 和向量 $\mathbf{b}$ 的元素由轨迹数据中的相关项平均值构成。具体来说，对于一个一维算例，若 $U(R; \boldsymbol{\theta}) = \frac{\theta_{1}}{2} R^{2} + \frac{\theta_{2}}{4} R^{4}$，则[正规方程](@entry_id:142238)的矩阵形式为 [@problem_id:3399890]：

$$
\begin{pmatrix} \langle R^2 \rangle & \langle R^4 \rangle \\ \langle R^4 \rangle & \langle R^6 \rangle \end{pmatrix} \begin{pmatrix} \theta_1 \\ \theta_2 \end{pmatrix} = \begin{pmatrix} -\langle f(R) R \rangle \\ -\langle f(R) R^3 \rangle \end{pmatrix}
$$

其中 $f(R)$ 是目标力。只要矩阵 $\mathbf{A}$（通常称为[正规矩阵](@entry_id:185943)）是可逆的，我们就可以通过求解这个线性系统直接得到最优参数 $\boldsymbol{\theta}^\star = \mathbf{A}^{-1}\mathbf{b}$。矩阵 $\mathbf{A}$ 是[对称正定](@entry_id:145886)的，这保证了[解的唯一性](@entry_id:143619)，并允许使用如共轭梯度法（Conjugate Gradient）等高效的数值算法进行求解。对于一个 $M$ 维的参数空间，[共轭梯度法](@entry_id:143436)在精确算术下至多需要 $M$ 次迭代即可收敛 [@problem_id:3399890]。

#### [统计偏差](@entry_id:275818)与有限样本效应

上述推导假设我们能获得精确的系综平均值。然而在实践中，我们只能通过有限长度的模拟轨迹来估计这些平均值。这会引入[统计误差](@entry_id:755391)，并可能导致估计参数 $\hat{\boldsymbol{\theta}}$ 的**偏差**（bias），即 $\mathbb{E}[\hat{\boldsymbol{\theta}}] \neq \boldsymbol{\theta}^\star$，其中 $\boldsymbol{\theta}^\star$ 是理想的、在无限数据下得到的参数。

这种偏差的根源在于模型的不完美性或[表示能力](@entry_id:636759)不足。我们可以将真实的目标力 $y$ 写成模型预测部分与残差部分之和：$y = X \boldsymbol{\theta}^\star + \boldsymbol{\epsilon}$，其中 $X$ 是[设计矩阵](@entry_id:165826)（由[基函数](@entry_id:170178)的梯度构成），$\boldsymbol{\epsilon}$ 是包含了热噪声和模型[表示能力](@entry_id:636759)不足所产生的系统性误差的残差向量。

通过对[最小二乘解](@entry_id:152054)进行一阶[微扰分析](@entry_id:178808)，我们可以推导出估计偏差的主要来源 [@problem_id:3399932]：

$$
\mathbb{E}[\hat{\boldsymbol{\theta}} - \boldsymbol{\theta}^{\star}] \approx (\mathbf{X}^{T}\mathbf{X})^{-1}\mathbb{E}[\mathbf{X}^{T}\boldsymbol{\epsilon}]
$$

这个公式揭示了一个深刻的见解：偏差主要来自于模型特征（[设计矩阵](@entry_id:165826) $\mathbf{X}$ 的列）与系统性误差 $\boldsymbol{\epsilon}$ 之间的相关性 $\mathbb{E}[\mathbf{X}^{T}\boldsymbol{\epsilon}]$。如果模型是完全正确的（$\boldsymbol{\epsilon}$ 仅为与特征无关的白噪声），则此相关项为零，估计是无偏的。但在粗粒化中，由于将高维自由度投影到低维空间，$\boldsymbol{\epsilon}$ 往往包含结构化的、与CG构型相关的系统性分量，导致该相关项非零，从而产生偏差。在实践中，可以使用**自助法**（Bootstrap）等重采样技术来估计这种偏差的大小 [@problem_id:3399932]。

### 迭代式结构反演方法

与力匹配直接求解参数不同，结构反演方法采用迭代的方式来优化CG[势能](@entry_id:748988)，直到CG模拟产生的结构性质（如径向分布函数, Radial Distribution Function, RDF, 记为 $g(r)$）与目标结构性质相匹配。

#### 玻尔兹曼反演法

**[逆玻尔兹曼反演](@entry_id:750797)**（Inverse Boltzmann Inversion, IBI）是一种流行且直观的[启发式方法](@entry_id:637904)。其核心思想来源于PMF与$g(r)$之间的关系：在稀疏极限下，$U_{\text{PMF}}(r) \approx -k_B T \ln g(r)$。IBI将此关系转化为一个迭代更新规则：

$$
U_{n+1}(r) = U_n(r) + \alpha k_{B}T \ln \frac{g_n(r)}{g_{\text{target}}(r)}
$$

其中 $U_n(r)$ 和 $g_n(r)$ 分别是第 $n$ 次迭代的[势能](@entry_id:748988)和产生的RDF，$g_{\text{target}}(r)$ 是目标RDF，$\alpha$ 是一个可调的步长参数（通常小于1）。这个更新规则非常直观：如果在某距离 $r$ 处，$g_n(r) > g_{\text{target}}(r)$，说明粒子在该距离出现的概率过高，即当前势能 $U_n(r)$ 在该处过于吸引（或不够排斥），因此需要增加 $U_n(r)$ 的值使其更具排斥性。

#### 逆[蒙特卡洛](@entry_id:144354)法与线性响应

IBI虽然直观，但其理论基础并不严格。**逆蒙特卡洛**（Inverse Monte Carlo, IMC）方法提供了一个基于[统计力](@entry_id:194984)学**[线性响应理论](@entry_id:145737)**的更严谨的框架 [@problem_id:3399898]。

其基本思想是，[对势能](@entry_id:203104)的一个微小扰动 $\delta u(r')$ 会引起RDF的[线性响应](@entry_id:146180) $\delta g(r)$：

$$
\delta g(r) = \int \chi(r, r') \delta u(r') \, dr'
$$

其中，响应核（或称[响应矩阵](@entry_id:754302)）$\chi(r, r')$ 与不同距离上粒子对数目的涨落协[方差](@entry_id:200758)相关：

$$
\chi(r, r') = \frac{\partial \langle \hat{g}(r) \rangle}{\partial u(r')} = -\beta \left( \langle \hat{g}(r) \hat{N}_{\text{pairs}}(r') \rangle - \langle \hat{g}(r) \rangle \langle \hat{N}_{\text{pairs}}(r') \rangle \right)
$$

在数值实现中，我们将径向距离 $r$ 离散化为若干个区间（bins）。[势能](@entry_id:748988)的更新量 $\delta \mathbf{u}$ 和RDF的偏差 $\delta \mathbf{g} = \mathbf{g}_{\text{target}} - \mathbf{g}_{\text{current}}$ 都表示为向量。上述[积分方程](@entry_id:138643)相应地转化为一个矩阵方程 [@problem_id:3399898]：

$$
\delta \mathbf{g} = \mathbf{M} \delta \mathbf{u}
$$

其中矩阵 $\mathbf{M}$ 的元素 $M_{ij}$ 表示在第 $j$ 个区间上施加单位[势能](@entry_id:748988)变化对第 $i$ 个区间的RD[F值](@entry_id:178445)造成的影响。迭代的目标就是求解这个[线性系统](@entry_id:147850)以获得势能更新量 $\delta \mathbf{u} = \mathbf{M}^{-1} \delta \mathbf{g}$。

然而，[响应矩阵](@entry_id:754302) $\mathbf{M}$ 往往是**病态的**（ill-conditioned）甚至是奇异的。这是因为不同距离处的[势能](@entry_id:748988)变化可能对RDF产生非常相似的影响，导致 $\mathbf{M}$ 的列向量近似[线性相关](@entry_id:185830)。直接求逆会极大地放大测量噪声，导致[势能](@entry_id:748988)更新不稳定。因此，必须采用**正则化**技术，例如使用**摩尔-彭若斯[伪逆](@entry_id:140762)**（Moore-Penrose Pseudoinverse）$\mathbf{M}^+$ 来求解最小范数[最小二乘解](@entry_id:152054)，或者使用**[吉洪诺夫正则化](@entry_id:140094)**（Tikhonov Regularization）来求解一个带罚项的[优化问题](@entry_id:266749) [@problem_id:3399898]。

#### [收敛性分析](@entry_id:151547)

IBI和IMC都是迭代格式，因此分析它们的收敛性和稳定性至关重要。我们可以通过在目标解（即[不动点](@entry_id:156394) $u^\star$）附近对更新映射进行线性化来研究误差的传播 [@problem_id:3399894]。

对于一个通用的更新格式 $u_{n+1} = u_n + \Delta(u_n)$，其误差 $\epsilon_n$（例如 $\ln g_n - \ln g^\star$ 或 $g_n - g^\star$）在[不动点](@entry_id:156394)附近的演化近似为：

$$
\epsilon_{n+1}(r) \approx \lambda(r) \epsilon_n(r)
$$

其中[放大因子](@entry_id:144315) $\lambda(r) = 1 + \left.\frac{\partial \Delta}{\partial u}\right|_{u^{\star}(r)}$。要保证误差单调收敛（即误差大小持续减小且不改变符号），需要满足 $0 < \lambda(r) < 1$，这等价于 $-1 < \left.\frac{\partial \Delta}{\partial u}\right|_{u^{\star}(r)} < 0$。

将此条件分别应用于IBI和IMC，可以得到它们保证单调收敛的最大步长 [@problem_id:3399894]：

*   对于IBI，$\left.\frac{\partial \Delta_{\text{IBI}}}{\partial u}\right|_{u^{\star}} = \alpha k_B T s(r)$，其中 $s(r) = \left.\frac{\partial \ln g}{\partial u}\right|_{u^\star}$ 是对数RDF的响应。由于 $s(r)$ 通常为负（增加[排斥势](@entry_id:185622)会降低粒子出现概率），[收敛条件](@entry_id:166121)要求 $\alpha < \frac{-1}{k_B T s(r)}$。最大步长 $\alpha_{\text{IBI,max}}(r)$ 依赖于局部的响应 $s(r)$。

*   对于IMC（的简化形式），可以证明 $\left.\frac{\partial \Delta_{\text{IMC}}}{\partial u}\right|_{u^{\star}} = -\alpha$。[收敛条件](@entry_id:166121)直接给出 $0 < \alpha < 1$。因此，其最大步长 $\alpha_{\text{IMC,max}} = 1$，且不依赖于系统细节。

这个分析揭示了IMC相对于IBI的理论优势：其收敛性不依赖于未知的[系统响应](@entry_id:264152)函数，使其在实践中通常更为鲁棒。

### 基础局限性与高级议题

尽管上述方法功能强大，但在应用中会遇到一系列深刻的理论挑战和局限性。理解这些问题对于正确构建和评估CG模型至关重要。

#### [可表示性](@entry_id:635277)问题与[保守力场](@entry_id:164320)

所有基于势能的方法都隐含了一个核心假设：CG[平均力](@entry_id:170826)场是**保守的**（conservative）。一个[力场](@entry_id:147325) $\mathbf{F}(\mathbf{R})$ 是保守的，当且仅当它可以表示为某个[标量势](@entry_id:276177) $U(\mathbf{R})$ 的负梯度，即 $\mathbf{F} = -\nabla U$。根据矢量分析理论，这等价于[力场](@entry_id:147325)的**旋度**（curl）处处为零：$\nabla \times \mathbf{F} = \mathbf{0}$。

然而，通过Mori-[Zwanzig投影](@entry_id:158200)算符理论可以证明，从微观动力学精确投影得到的CG[平均力](@entry_id:170826)，除了保守部分 $(-\nabla U_{\text{PMF}})$ 外，通常还包含与速度相关的[摩擦力](@entry_id:171772)和随机力。在某些情况下，即使是[平均力](@entry_id:170826)本身也可能包含非保守（有旋）分量。如果真实的CG[平均力](@entry_id:170826)场 $\mathbf{F}^\star(\mathbf{R})$ 具有非零旋度，那么就不存在任何一个[标量势](@entry_id:276177) $U_{\text{CG}}(\mathbf{R})$ 能够完美地重现它。这种不匹配被称为**[可表示性](@entry_id:635277)问题**（representability problem）。

我们可以通过数值方法来诊断[力场](@entry_id:147325)的非保守性 [@problem_id:3399961]。一个直接的方法是计算[力场](@entry_id:147325)沿两个不同[路径连接](@entry_id:149343)相同起点和终点的线积分。对于保守场，积分结果应与路径无关。另一个方法是直接在空间网格上计算[力场的旋度](@entry_id:174409) $\omega_z = \frac{\partial F_y}{\partial x} - \frac{\partial F_x}{\partial y}$。如果计算得到的旋度显著不为零，则表明该[力场](@entry_id:147325)无法被一个[标量势](@entry_id:276177)精确表示，任何基于势能的力匹配都将存在系统性误差。

#### [规范自由度](@entry_id:160491)与[解的唯一性](@entry_id:143619)

即使[力场](@entry_id:147325)是保守的，我们得到的CG势能函数是否唯一？这涉及到**[规范自由度](@entry_id:160491)**（gauge freedom）的概念 [@problem_id:3399962]。

最明显的[规范自由度](@entry_id:160491)是，给[势能](@entry_id:748988)加上一个任意常数 $C$ 并不会改变其导出的力：$-\nabla(U(\mathbf{R}) + C) = -\nabla U(\mathbf{R})$。因此，势能的绝对零点是无法由力匹配确定的。

在实际的数值计算中，可能会出现更复杂的“表观”[规范自由度](@entry_id:160491)。当使用一组[基函数](@entry_id:170178) $\phi_i(\mathbf{R})$ 来表示势能时，如果存在某个非零的[线性组合](@entry_id:154743) $\sum_i \theta_i \phi_i(\mathbf{R})$，其梯度在所有采样点上都恰好为零，那么对应的参数组合 $\boldsymbol{\theta}$ 就无法被力匹配过程所确定。这会导致正规方程的矩阵 $\mathbf{A}$ 奇[异或](@entry_id:172120)接近奇异，使得解不唯一。这种情况下的不确定性，虽然源于离散化和有限采样，但其表现形式类似于一种规范自由度 [@problem_id:3399962]。

需要强调的是，向一个[保守力场](@entry_id:164320)中添加一个通用的无散（divergence-free）矢量场并不会产生一个合法的[规范变换](@entry_id:176521)，因为这样的操作通常会引入非零的旋度，从而破坏[力场](@entry_id:147325)的保守性 [@problem_id:3399962]。

#### 系综不匹配与自洽性

标准力匹[配方法](@entry_id:265480)使用从全原子（AA）模拟中获得的轨迹来计算[平均力](@entry_id:170826)。这意味着，我们得到的CG参数 $\boldsymbol{\theta}_{\text{AA}}$ 是在最小化**AA系综**上的力误差。然而，一旦我们使用这个[参数化](@entry_id:272587)的CG[势能](@entry_id:748988) $U_{\boldsymbol{\theta}_{\text{AA}}}$ 进行模拟，它将生成其自身的、不同于AA系综的CG系综。这种**系综不匹配**（ensemble mismatch）是CG建模中一个微妙但重要的问题，它可能导致CG模型产生的结构性质（如RDF）与目标不符。

为了解决这个问题，可以采用一种**自洽**（self-consistent）的迭代方案 [@problem_id:3399911]。该方案从一个初始的CG[势能](@entry_id:748988)出发，进行一次CG模拟，然后利用这次CG模拟的轨迹来计算新的[平均力](@entry_id:170826)（相对于目标AA力），并求解新的CG势能。这个过程不断迭代，直到输入的CG[势能](@entry_id:748988)与输出的CG势能收敛到同一个[不动点](@entry_id:156394) $\boldsymbol{\theta}_{\text{CG}}^{(\star)}$。这个[不动点](@entry_id:156394)满足的条件是，该势能是在其**自身产生的系综**上对AA力的最优近似。

如果CG模型具有足够强的[表示能力](@entry_id:636759)（即真实的PMF就在其函数空间内），那么 $\boldsymbol{\theta}_{\text{AA}}$ 和 $\boldsymbol{\theta}_{\text{CG}}^{(\star)}$ 将会是相同的。然而，当模型存在[表示能力](@entry_id:636759)不足时，这两种方法会得到不同的结果。它们之间的差异 $\Delta_{\theta} = \|\boldsymbol{\theta}_{\text{AA}} - \boldsymbol{\theta}_{\text{CG}}^{(\star)}\|_2$ 可以作为模型不匹配程度的一个度量 [@problem_id:3399911]。

#### 可移植性与状态点依赖

PMF本质上是一个自由能，因此它依赖于系统的[热力学状态](@entry_id:755916)点（如温度、压强）。这意味着，在一个状态点（例如，特定温度 $T_1$）下[参数化](@entry_id:272587)的CG势能，在另一个状态点（$T_2$）下可能不再准确。这限制了CG模型的**可移植性**（transferability）。

我们可以利用[线性响应理论](@entry_id:145737)来量化这种依赖性 [@problem_id:3399909]。假设温度发生了一个微小的变化 $\delta\beta$，我们希望找到势能参数需要做出的相应调整 $\delta\boldsymbol{\theta}$，以保持系统的结构（例如，由特征期望 $\langle f_a \rangle$ 描述的RDF）不变。通过[线性响应](@entry_id:146180)分析可以推导出：

$$
\delta \boldsymbol{\theta} = - \frac{\delta \beta}{\beta} (\boldsymbol{C}_{ff})^{-1} \boldsymbol{c}_{fU}
$$

其中 $\boldsymbol{C}_{ff}$ 是[特征函数](@entry_id:186820)之间的协方差矩阵，而 $\boldsymbol{c}_{fU}$ 是[特征函数](@entry_id:186820)与总能量 $U_{\boldsymbol{\theta}}$ 之间的协[方差](@entry_id:200758)向量。这个优雅的公式表明，参数对温度的响应由系统在单一状态点下的能量和特征的涨落性质决定。这些协[方差](@entry_id:200758)都可以从一次模拟中测量得到，为改进[势能](@entry_id:748988)的可移植性提供了理论指导。

#### 从结构到动力学

最后，一个至关重要的问题是：一个能够精确重现平衡结构的CG模型，能否重现正确的动力学？答案通常是否定的。

一个静态的CG势能 $U_{\text{CG}} \approx U_{\text{PMF}}$ 之所以能重现结构，是因为平衡结构只依赖于[玻尔兹曼分布](@entry_id:142765) $P(\mathbf{R}) \propto \exp(-\beta U_{\text{PMF}})$。然而，系统的动力学演化远比这复杂。如前所述，精确的CG动力学方程（[广义朗之万方程](@entry_id:158854)）不仅包含来自PMF的[保守力](@entry_id:170586)，还包含了描述[能量耗散](@entry_id:147406)的**[摩擦力](@entry_id:171772)**（通常带有[记忆效应](@entry_id:266709)）和驱动系统涨落的**随机力** [@problem_id:3399947]。

当我们在CG模拟中使用牛顿或简单的[朗之万动力学](@entry_id:142305)时，我们实际上是用一个简化的模型取代了这些复杂的动力学项。例如，一个标准的朗之万方程用一个瞬时的摩擦项 $-M\gamma\mathbf{v}$ 和一个白噪声项 $\boldsymbol{\eta}(t)$ 来近似真实的记忆核摩擦和[有色噪声](@entry_id:265434)。这种简化意味着，即使CG势能是完美的，其动力学性质（如[扩散](@entry_id:141445)系数、[弛豫时间](@entry_id:191572)）通常也与真实的全原子系统不符。

因此，CG模型的动力学性质往往需要**独立校准**。一个常见的做法是调整[朗之万动力学](@entry_id:142305)中的[摩擦系数](@entry_id:150354) $\gamma$ 来匹配一个目标动力学性质。例如，对于自由[扩散](@entry_id:141445)的粒子，[扩散](@entry_id:141445)系数 $D$ 与摩擦系数 $\gamma$ 之间存在爱因斯坦-斯摩洛霍夫斯基关系：$D = k_B T / (M\gamma)$。通过测量[全原子模拟](@entry_id:202465)中的目标[扩散](@entry_id:141445)系数 $D_{\text{target}}$，我们可以反解出应在CG模拟中使用的[摩擦系数](@entry_id:150354) $\gamma = \frac{k_B T}{M D_{\text{target}}}$，从而保证CG模型至少能重现正确的长时[扩散](@entry_id:141445)行为 [@problem_id:3399947]。这凸显了在粗粒化建模中，结构和动力学是两个既相关又独立的目标。