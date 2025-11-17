## 引言
在科学与工程领域，从气候模型到金融市场，再到结构力学，我们面临的系统日益复杂，并且普遍受到不确定性的影响。量化这些不确定性对模型预测的影响——即不确定性量化（UQ）——对于做出可靠的决策和稳健的设计至关重要。然而，传统方法如蒙特卡洛模拟，尽管普适，但往往需要成千上万次昂贵的模型评估，造成了巨大的计算瓶颈。这一挑战催生了对高效代理模型（surrogate models）的需求，而[多项式混沌](@entry_id:196964)展开 (PCE) 正是其中一种功能最强大、理论最优雅的代表。

PCE 不仅仅是一种减少计算量的技巧，它提供了一个严谨的数学框架，将被建模系统中的随机性转化为一组确定性的系数，从而揭示了系统深层的统计结构。本文旨在系统性地介绍[多项式混沌](@entry_id:196964)展开的理论与实践，填补从基础理论到高级应用之间的知识鸿沟。

为了实现这一目标，本文将分为三个核心部分。在“原理与机制”一章中，我们将深入探讨 PCE 的数学基础，包括其在希尔伯特空间中的表述、[正交基](@entry_id:264024)的构建以及系数的计算方法。接下来，在“应用与跨学科联系”一章中，我们将展示 PCE 如何作为通用元建模技术，在前向[不确定性传播](@entry_id:146574)、[全局敏感性分析](@entry_id:171355)以及加速贝叶斯推断等多样化场景中发挥关键作用。最后，“动手实践”部分将通过具体的编程练习，指导您将理论知识转化为实际的计算能力。通过这一结构化的学习路径，您将全面掌握 PCE 这一前沿方法，并有能力将其应用于您自己的研究与工程问题中。

## 原理与机制

在上一章对[多项式混沌](@entry_id:196964)展开 (PCE) 的概念性介绍之后，本章将深入探讨其数学原理和核心机制。我们将建立一个严谨的框架来理解 PCE 如何表示随机量，如何构建其基础，以及如何在实际应用中计算其系数。本章旨在为读者提供将 PCE 应用于复杂系统（尤其是在逆问题和[数据同化](@entry_id:153547)领域）所需的理论基础和实践见解。

### [希尔伯特空间](@entry_id:261193)框架下的[多项式混沌](@entry_id:196964)展开

[多项式混沌](@entry_id:196964)展开的核心思想是将一个依赖于一组随机输入 $\boldsymbol{\xi}$ 的随机输出量 $Y(\boldsymbol{\xi})$ 表示为一个关于 $\boldsymbol{\xi}$ 的[正交多项式](@entry_id:146918)函数的[无穷级数](@entry_id:143366)。为了严谨地描述这一思想，我们必须借助希尔伯特空间 (Hilbert space) 的语言。

#### [随机变量](@entry_id:195330)的 $L^2$ 空间

考虑一个随机输出 $Y$，其不确定性完全由一个随机向量 $\boldsymbol{\xi} \in \mathbb{R}^d$ 决定。该向量遵循一个已知的概率定律，由概率测度 $\mu$ 描述。所有具有有限二阶矩（即[有限方差](@entry_id:269687)）的此类[随机变量](@entry_id:195330)构成了一个希尔伯特空间，记为 $L^2(\mu)$。这个空间中的元素是关于测度 $\mu$ 平方可积的函数，即满足 $\mathbb{E}[|Y|^2] = \int |Y(\boldsymbol{\xi})|^2 d\mu(\boldsymbol{\xi})  \infty$ 的函数。

在这个空间中，我们可以定义一个**[内积](@entry_id:158127) (inner product)**，它为我们提供了衡量两个[随机变量](@entry_id:195330)之间关系的几何工具。对于任意两个函数 $f, g \in L^2(\mu)$，它们的[内积](@entry_id:158127)定义为其[乘积的期望值](@entry_id:201037)：

$$
\langle f, g \rangle = \mathbb{E}[f(\boldsymbol{\xi}) g(\boldsymbol{\xi})] = \int_{\mathbb{R}^d} f(\boldsymbol{\xi}) g(\boldsymbol{\xi}) d\mu(\boldsymbol{\xi})
$$

这个[内积](@entry_id:158127)诱导出一个范数 $\|f\|_{L^2} = \sqrt{\langle f, f \rangle} = \sqrt{\mathbb{E}[f^2]}$，它衡量了[随机变量](@entry_id:195330)的大小或离散程度。

#### [正交多项式](@entry_id:146918)基与[广义傅里叶级数](@entry_id:170054)

PCE 的本质是将 $Y$ 在 $L^2(\mu)$ 空间中投影到一个由特殊多项式构成的**正交基 (orthogonal basis)** 上。假设我们有一族多变量多项式 $\{\Psi_{\boldsymbol{\alpha}}\}_{\boldsymbol{\alpha} \in \mathcal{A}}$（其中 $\mathcal{A}$ 是一个可数的多元索引集，例如 $\mathbb{N}_0^d$），它们相对于上述[内积](@entry_id:158127)是**标准正交 (orthonormal)** 的。这意味着：

$$
\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}
$$

其中 $\delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$ 是克罗内克 delta 函数，当且仅当 $\boldsymbol{\alpha} = \boldsymbol{\beta}$ 时为 1，否则为 0。

如果这个[标准正交基](@entry_id:147779)是**完备的 (complete)**，即它可以张成整个 $L^2(\mu)$ 空间，那么任何函数 $Y \in L^2(\mu)$ 都可以唯一地表示为这个基上的[广义傅里叶级数](@entry_id:170054)：

$$
Y(\boldsymbol{\xi}) = \sum_{\boldsymbol{\alpha} \in \mathcal{A}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})
$$

这个级数在**均方意义 (mean-square sense)** 下收敛，即截断和的范数误差趋于零：$\mathbb{E}[|Y - \sum_{|\boldsymbol{\alpha}|\le p} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}|^2] \to 0$ 当 $p \to \infty$ 时。[@problem_id:3523156]

PCE 的系数 $c_{\boldsymbol{\alpha}}$ 可以通过将 $Y$ 投影到相应的[基函数](@entry_id:170178)上得到。利用基的[标准正交性](@entry_id:267887)，我们对上式两边取与 $\Psi_{\boldsymbol{\beta}}$ 的[内积](@entry_id:158127)：

$$
\langle Y, \Psi_{\boldsymbol{\beta}} \rangle = \left\langle \sum_{\boldsymbol{\alpha} \in \mathcal{A}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \right\rangle = \sum_{\boldsymbol{\alpha} \in \mathcal{A}} c_{\boldsymbol{\alpha}} \langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \sum_{\boldsymbol{\alpha} \in \mathcal{A}} c_{\boldsymbol{\alpha}} \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}} = c_{\boldsymbol{\beta}}
$$

因此，PCE 系数由以下**[投影公式](@entry_id:152164) (projection formula)** 唯一确定：

$$
c_{\boldsymbol{\alpha}} = \langle Y, \Psi_{\boldsymbol{\alpha}} \rangle = \mathbb{E}[Y(\boldsymbol{\xi}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]
$$

[@problem_id:3411038]

按照惯例，零阶多项式 $\Psi_{\boldsymbol{0}}$ 是一个常数。为了满足[归一化条件](@entry_id:156486) $\langle \Psi_{\boldsymbol{0}}, \Psi_{\boldsymbol{0}} \rangle = \mathbb{E}[\Psi_{\boldsymbol{0}}^2] = 1$，我们选择 $\Psi_{\boldsymbol{0}}(\boldsymbol{\xi}) \equiv 1$。因此，零阶系数 $c_{\boldsymbol{0}} = \mathbb{E}[Y \cdot 1] = \mathbb{E}[Y]$，恰好是随机输出的均值。对于所有非零索引 $\boldsymbol{\alpha} \neq \boldsymbol{0}$，正交性要求 $\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{0}} \rangle = \mathbb{E}[\Psi_{\boldsymbol{\alpha}}] = 0$，这意味着所有高阶基多项式都必须是零均值的。

值得注意的是，PCE 的存在和[均方收敛](@entry_id:137545)性依赖于三个基本条件：
1.  **[可测性](@entry_id:199191) (Measurability)**：随机量 $Y$ 必须完全由随机输入 $\boldsymbol{\xi}$ 决定，即 $Y$ 是 $\sigma(\boldsymbol{\xi})$-可测的。这保证了 $Y$ 可以写成 $Y = f(\boldsymbol{\xi})$ 的形式。
2.  **平方[可积性](@entry_id:142415) (Square Integrability)**：$Y$ 必须具有[有限方差](@entry_id:269687)，即 $\mathbb{E}[|Y|^2]  \infty$，以确保它是 $L^2(\mu)$ 空间的一个元素。
3.  **[基的完备性](@entry_id:196285) (Completeness of the Basis)**：多项式基 $\{\Psi_{\boldsymbol{\alpha}}\}$ 必须在 $L^2(\mu)$ 中是完备的。

[均方收敛](@entry_id:137545)是一个很强的[收敛模式](@entry_id:189917)，但它并不一定意味着**[几乎必然收敛](@entry_id:265812) (almost-sure convergence)**（即对几乎所有的 $\boldsymbol{\xi}$ 样本，级数都点态收敛到 $Y(\boldsymbol{\xi})$）。后者是一个更强的条件，通常需要对函数 $Y$ 的[光滑性](@entry_id:634843)或系数的求和性施加额外的要求。[@problem_id:3523156]

### 构建[基函数](@entry_id:170178)：Wiener-Askey 框架

PCE 的“广义”特性在于其[基函数](@entry_id:170178)的选择可以根据输入[随机变量](@entry_id:195330)的[概率分布](@entry_id:146404)进行定制。这种“门当户对”的选择是至关重要的，因为它极大地简化了计算，并构成了所谓的 **Wiener-Askey [多项式混沌](@entry_id:196964) (Wiener-Askey polynomial chaos)** 框架。

核心原则是：选择一个与输入测度 $\mu$ 的权重函数相正交的多项式族。当输入变量 $\xi_1, \dots, \xi_d$ [相互独立](@entry_id:273670)时，联合测度 $\mu$ 是边际测度的乘积，多变量[基函数](@entry_id:170178)可以通过单变量[正交多项式](@entry_id:146918)的张量积来构建。以下是一些经典对应关系：

-   **高斯分布 (Gaussian Distribution)**：如果输入 $\xi$ 服从标准正态分布 $\mathcal{N}(0,1)$，其[概率密度函数](@entry_id:140610)为 $\rho(x) = \frac{1}{\sqrt{2\pi}}\exp(-x^2/2)$。与之对应的正交多项式是**概率论者[埃尔米特多项式](@entry_id:153594) (Probabilists' Hermite polynomials)** $\{\text{He}_n(x)\}_{n \ge 0}$。它们满足[正交关系](@entry_id:145540)：
    $$
    \mathbb{E}[\text{He}_m(\xi)\text{He}_n(\xi)] = \int_{-\infty}^{\infty} \text{He}_m(x)\text{He}_n(x) \frac{1}{\sqrt{2\pi}}e^{-x^2/2} dx = n! \delta_{mn}
    $$
    对于一般的[正态分布](@entry_id:154414) $\xi \sim \mathcal{N}(\mu, \sigma^2)$，可以通过[仿射变换](@entry_id:144885) $z = (x-\mu)/\sigma$ 来使用标准[埃尔米特多项式](@entry_id:153594)，即[基函数](@entry_id:170178)为 $\{\text{He}_n((\xi-\mu)/\sigma)\}_{n \ge 0}$。[@problem_id:3341875] [@problem_id:3411021]

-   **[均匀分布](@entry_id:194597) (Uniform Distribution)**：如果输入 $\xi$ 服从 $[-1,1]$ 上的[均匀分布](@entry_id:194597)，其[概率密度函数](@entry_id:140610)为 $\rho(x) = 1/2$。与之对应的正交多项式是**勒让德多项式 (Legendre polynomials)** $\{P_n(x)\}_{n \ge 0}$。它们满足：
    $$
    \mathbb{E}[P_m(\xi)P_n(\xi)] = \int_{-1}^{1} P_m(x)P_n(x) \frac{1}{2} dx = \frac{1}{2n+1} \delta_{mn}
    $$
    [@problem_id:3341875]

Askey 框架还包括其他经典[分布](@entry_id:182848)，如伽马[分布](@entry_id:182848)（对应[拉盖尔多项式](@entry_id:200702)）和贝塔分布（对应[雅可比多项式](@entry_id:197425)）。

正确选择[基函数](@entry_id:170178)的巨大优势在于，它使得所谓的**随机 Galerkin [质量矩阵](@entry_id:177093)** $M_{ij} = \mathbb{E}[\psi_i(\xi)\psi_j(\xi)]$ 成为[对角矩阵](@entry_id:637782)。例如，在处理一个由高斯不确定性驱动的问题时，若选择[埃尔米特多项式](@entry_id:153594)作为基，该矩阵就是对角阵。但如果错误地选择了勒让德多项式，$\mathbb{E}[P_i(\xi)P_j(\xi)]$ 对于 $i \neq j$ 通常不为零，导致质量矩阵是稠密的。这在**侵入式 (intrusive)** PCE 方法中尤其关键，因为[对角质量矩阵](@entry_id:173002)意味着求解系数的[方程组](@entry_id:193238)是[解耦](@entry_id:637294)的，计算成本大大降低。[@problem_id:3341875]

### 从[随机场](@entry_id:177952)到有限维输入：Karhunen-Loève 展开

在许多科学和工程问题中，不确定性并非来自有限个参数，而是来自一个**随机场 (random field)**，例如材料属性（如[介电常数](@entry_id:146714)）在空间上随机变化。[随机场](@entry_id:177952)是一个无限维的对象，无法直接用标准 PCE 处理。**Karhunen-Loève (KL) 展开**提供了一种系统性的[降维](@entry_id:142982)方法，将随机场表示为一组不相关的[随机变量](@entry_id:195330)。

KL 展开是[随机过程](@entry_id:159502)最优的[线性表示](@entry_id:139970)，它将一个二阶随机场（即具有有限二阶矩）分解为其均值和一个无穷级数。假设有一个零均值随机场 $u(x, \omega)$，其[协方差核](@entry_id:266561)为 $C(x, x') = \mathbb{E}[u(x, \omega) u(x', \omega)]$。KL 展开基于该[协方差核](@entry_id:266561)对应的[积分算子](@entry_id:262332)的谱分解。具体来说，我们求解以下 Fredholm 第二类积分[特征值问题](@entry_id:142153)：

$$
\int_D C(x, x') \phi_n(x') dx' = \lambda_n \phi_n(x)
$$

其中 $D$ 是场的定义域。解出的[特征值](@entry_id:154894) $\lambda_n$ 是非负的，它们表示了每个模态对总[方差](@entry_id:200758)的贡献；[特征函数](@entry_id:186820) $\phi_n(x)$ 是确定性的空间模态，并在 $L^2(D)$ 空间中标准正交。[@problem_id:3341904]

随机场 $u(x)$ 于是可以表示为：

$$
u(x, \omega) = \mathbb{E}[u(x)] + \sum_{n=1}^{\infty} \sqrt{\lambda_n} \phi_n(x) \xi_n(\omega)
$$

其中 $\xi_n(\omega)$ 是一组[标准化](@entry_id:637219)的、**不相关 (uncorrelated)** 的[随机变量](@entry_id:195330)，其定义为 $u(x)$ 在[基函数](@entry_id:170178) $\phi_n(x)$ 上的投影：
$$
\xi_n(\omega) = \frac{1}{\sqrt{\lambda_n}} \int_D (u(x, \omega) - \mathbb{E}[u(x)]) \phi_n(x) dx
$$
它们满足 $\mathbb{E}[\xi_n] = 0$ 和 $\mathbb{E}[\xi_n \xi_m] = \delta_{nm}$。如果原[随机场](@entry_id:177952)是高斯场，那么 $\xi_n$ 也是[相互独立](@entry_id:273670)的标准正态[随机变量](@entry_id:195330)。

**一个具体的例子**：考虑定义在 $[0,1]$ 上的一个零均值[高斯随机场](@entry_id:749757)，其[协方差核](@entry_id:266561)为 $C(x,x') = \sigma^2 \min(x,x')$（这对应于标准布朗运动的终点）。通过将上述积分方程转化为一个带有边界条件的[二阶常微分方程](@entry_id:204212)，可以求解得到其 KL 展开的特征对 [@problem_id:3411021]：
-   [特征值](@entry_id:154894)： $\lambda_n = \frac{\sigma^2}{\pi^2 (n - 1/2)^2}$
-   [特征函数](@entry_id:186820)： $\phi_n(x) = \sqrt{2} \sin((n - 1/2)\pi x)$

KL 展开在[不确定性量化](@entry_id:138597)中的关键作用在于**[降维](@entry_id:142982)**。由于[特征值](@entry_id:154894) $\lambda_n$ 通常会快速衰减，我们可以通过截断 KL 级数来获得一个精确的低维近似：

$$
u_m(x) = \mathbb{E}[u(x)] + \sum_{n=1}^{m} \sqrt{\lambda_n} \phi_n(x) \xi_n
$$

这个截断后的近似场 $u_m(x)$ 完全由一个**有限维**的随机向量 $\boldsymbol{\xi} = (\xi_1, \dots, \xi_m)^T$ [参数化](@entry_id:272587)。这个向量随后就可以作为 PCE 的输入，从而将无限维不确定性问题转化为有限维问题。截断引入的误差是可控的。例如，对于上述布朗运动场，在 $x=1$ 处的线性泛函 $y=u(1)$，其 KL 截断引入的均方误差可以精确计算为 $\mathbb{E}[(y-y_m)^2] = \sum_{n=m+1}^{\infty} \lambda_n (\phi_n(1))^2$，这是一个关于 $m$ 的解析表达式。[@problem_id:3411021]

### 多变量展开与实际计算

将 PCE 应用于由 $d$ 个[独立随机变量](@entry_id:273896) $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$ 驱动的实际问题时，我们面临着构建多维基和有效计算系数的挑战。

#### 多维基与截断策略

如果输入变量 $\xi_i$ 是相互独立的，那么多变量正交多项式基可以通过单变量基的**张量积 (tensor product)** 构建。设 $\{\psi_{\alpha_i}^{(i)}\}_{\alpha_i=0}^\infty$ 是与 $\xi_i$ 的[分布](@entry_id:182848)相对应的单变量标准[正交多项式](@entry_id:146918)族。那么多变量[基函数](@entry_id:170178) $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$ 就由下式给出：

$$
\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = \prod_{i=1}^d \psi_{\alpha_i}^{(i)}(\xi_i)
$$

其中 $\boldsymbol{\alpha} = (\alpha_1, \dots, \alpha_d) \in \mathbb{N}_0^d$ 是一个**多元索引 (multi-index)**。由于输入变量的独立性，可以证明这个[张量积](@entry_id:140694)基在联合测度下是标准正交的。[@problem_id:3411063]

在实践中，[无穷级数](@entry_id:143366)必须被截断为一个有限和。选择哪些项保留在一个有限的索引集 $\mathcal{A}$ 中，是一个关键的建模决策，它直接影响到 PCE 的精度和计算成本。常见的截断策略包括：

-   **全[张量积](@entry_id:140694) (Full Tensor-product, FT)**：保留所有单变量阶数不超过 $p$ 的项。索引集为 $\mathcal{A}_p^{\text{FT}} = \{\boldsymbol{\alpha} \in \mathbb{N}_0^d : \max_i \alpha_i \le p\}$。其项数为 $(p+1)^d$，随维度 $d$ 呈[指数增长](@entry_id:141869)，很快变得不可行。[@problem_id:3411063]

-   **总阶数 (Total-Degree, TD)**：保留所有总阶数 $|{\boldsymbol{\alpha}}| = \sum_{i=1}^d \alpha_i$ 不超过 $p$ 的项。索引集为 $\mathcal{A}_p^{\text{TD}} = \{\boldsymbol{\alpha} \in \mathbb{N}_0^d : |\boldsymbol{\alpha}| \le p\}$。其项数为 $\binom{d+p}{p}$。虽然这个数字也随 $d$ 快速增长（对固定的 $p$，呈 $d^p$ 的[多项式增长](@entry_id:177086)），但通常远小于全张量积的项数。[@problem_id:3411063] [@problem_id:3341902]

-   **双曲交叉 (Hyperbolic Cross, HC)**：这种策略基于一个假设，即高阶交互项（即多个变量同时具有高阶数）对模型输出的影响较小。它优先保留那些总阶数较高但只涉及少数变量的项。一个常见的 HC 索引集定义为 $\mathcal{A}_p^{\text{HC}} = \{\boldsymbol{\alpha} \in \mathbb{N}_0^d : \prod_{j=1}^d (\alpha_j+1) \le p+1\}$。其项数增长速度远慢于 TD 截断，大约为 $O(p(\log p)^{d-1})$，有助于缓解**[维数灾难](@entry_id:143920) (curse of dimensionality)**。[@problem_id:3411063] [@problem_id:3341902]

#### 非侵入式[系数估计](@entry_id:175952)

对于许多复杂的“黑箱”模型，我们只能在给定的输入点 $\boldsymbol{\xi}^{(j)}$ 上运行模型并获得输出 $Q(\boldsymbol{\xi}^{(j)})$。**非侵入式 (non-intrusive)** 方法正是利用这些模型运行结果来估计 PCE 系数，而无需修改模型代码。

-   **[投影法](@entry_id:144836) (Projection Method)**：此方法直接逼近系数的积分公式 $c_{\boldsymbol{\alpha}} = \mathbb{E}[Q(\boldsymbol{\xi}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]$。这个[期望值](@entry_id:153208)（一个[高维积分](@entry_id:143557)）通过**[数值求积](@entry_id:136578) (numerical quadrature)** 来计算，例如[高斯求积](@entry_id:146011)。
    $$
    c_{\boldsymbol{\alpha}} \approx \sum_{j=1}^N w_j Q(\boldsymbol{\xi}^{(j)}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}^{(j)})
    $$
    其中 $(\boldsymbol{\xi}^{(j)}, w_j)$ 是求积点和相应的权重。为了精确计算一个总阶数最高为 $2p$ 的多项式（当 $Q$ 本身是 $p$ 阶多项式时），基于张量积的高斯求积在每个维度上需要 $p+1$ 个点，总共需要 $(p+1)^d$ 次模型评估。这种指数级的增长使得该方法在高维下不切实际。**[稀疏网格](@entry_id:139655) (sparse grids)** 求积是对此的一种改进，可以显著减少所需的点数。[@problem_id:3341911]

-   **回归法 (Regression Method)**：此方法将[系数估计](@entry_id:175952)问题转化为一个**最小二乘 (least-squares)** 回归问题。我们生成 $N$ 个输入样本 $\{\boldsymbol{\xi}^{(j)}\}_{j=1}^N$（通常通过蒙特卡洛或拉丁超立方采样），运行模型得到相应的输出 $\{y_j = Q(\boldsymbol{\xi}^{(j)})\}_{j=1}^N$。然后，我们寻找一组系数 $\mathbf{c} = \{c_{\boldsymbol{\alpha}}\}$，使得 PCE 在这些样本点上的预测值与真实输出的平方误差最小：
    $$
    \min_{\mathbf{c}} \sum_{j=1}^N \left( y_j - \sum_{\boldsymbol{\alpha} \in \mathcal{A}_p} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}^{(j)}) \right)^2
    $$
    这是一个标准的线性回归问题 $\min_{\mathbf{c}} \|\mathbf{y} - \boldsymbol{\Psi}\mathbf{c}\|_2^2$，其中 $\boldsymbol{\Psi}$ 是[设计矩阵](@entry_id:165826)，其元素为 $\Psi_{j,\boldsymbol{\alpha}} = \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}^{(j)})$。为了得到一个稳定且唯一的解，所需的样本数 $N$ 必须至少等于未知系数的个数 $M = |\mathcal{A}_p| = \binom{d+p}{p}$。实践中，通常采用[过采样](@entry_id:270705)，即 $N \approx 2M$ 或 $3M$。与[张量积求积](@entry_id:145940)的指数级增长相比，回归法所需的样本数仅随维数呈[多项式增长](@entry_id:177086)，因此在高维问题中更具优势，是缓解维数灾难的有效手段。[@problem_id:3341911]

### 高级主题

#### [收敛率](@entry_id:146534)：谱收敛

PCE 的一个显著优点是其**谱收敛 (spectral convergence)** 特性。这意味着，如果被展开的函数 $Q(\boldsymbol{\xi})$ 关于其输入 $\boldsymbol{\xi}$ 足够光滑，那么 PCE 的均方误差会以指数速率衰减，即误差 $\propto \rho^{-p}$，其中 $\rho  1$。这远快于标准蒙特卡洛方法的代数[收敛率](@entry_id:146534)（$O(N^{-1/2})$）。

收敛速度的理论基础是函数的光滑性。具体来说，谱收敛成立的充分必要条件是函数 $Q(\boldsymbol{\xi})$ 能够**[解析延拓](@entry_id:147225) (analytically continued)** 到复数空间 $\mathbb{C}^d$ 中一个包含 $\boldsymbol{\xi}$ 实数支撑集的区域。

以麦克斯韦方程组为例，其解对[介电常数](@entry_id:146714) $\epsilon(\boldsymbol{\xi})$ 的依赖性决定了 PCE 的[收敛率](@entry_id:146534)。如果 $\epsilon$ 对 $\boldsymbol{\xi}$ 是解析的，并且在某个复数邻域内，问题始终是良定的（例如，通过保持一定的物理损耗 $\text{Im}(\epsilon)  0$，或是在无损情况下，确保工作频率 $\omega$ 一致地避开所有可能的谐振频率），那么解映射 $\boldsymbol{\xi} \mapsto \boldsymbol{E}(\cdot, \boldsymbol{\xi})$ 就是全纯的。因此，任何关于解的[连续线性泛函](@entry_id:262913) $Q(\boldsymbol{\xi})$ 也将是解析的，其 PCE 就会呈现谱收敛。反之，如果 $Q(\boldsymbol{\xi})$ 的依赖关系不光滑，例如是一个阶跃函数，那么 PCE 将失去谱收敛性，退化为缓慢的代数收敛，并可能出现吉布斯现象。[@problem_id:3341842]

#### 处理相关输入变量

标准 PCE 的张量积结构依赖于输入变量的[相互独立](@entry_id:273670)性。当输入变量**相关 (dependent)** 时，必须采用更高级的方法。

根据 Sklar 定理，任何一个联合分布都可以由其[边际分布](@entry_id:264862)和一个 **copula 函数**来描述。Copula 捕捉了变量之间的全部相关结构。处理相关输入主要有两种策略：

1.  **直接法 (Direct Approach)**：构建一个直接与相关的[联合概率](@entry_id:266356)密度 $f_{\mathbf{X}}(\mathbf{x})$ 正交的多变量多项式基。联合密度可以表示为 $f_{\mathbf{X}}(\mathbf{x}) = c(F_1(x_1), \dots, F_d(x_d))\prod_i f_i(x_i)$，其中 $c$ 是 copula 密度。这种方法的挑战在于，当相关性存在时（即 $c \neq 1$），联合密度是不可分的。这使得[正交多项式](@entry_id:146918)的构建和计算投影系数所需的[高维积分](@entry_id:143557)（求积）都变得异常困难。[@problem_id:3411039]

2.  **变换法 (Transformation Approach)**：通过一个保持[概率测度](@entry_id:190821)的变换 $T$，将相关的输入变量 $\mathbf{X}$ 表示为一组独立的标准变量 $\mathbf{U}$ 的函数，即 $\mathbf{X} = T(\mathbf{U})$。常见的变换有 **Nataf 变换**（适用于高斯 copula）或更通用的**Rosenblatt 变换**。然后，我们不直接为原始模型 $\mathcal{M}(\mathbf{X})$ 构建 PCE，而是为复合模型 $g(\mathbf{U}) = \mathcal{M}(T(\mathbf{U}))$ 构建一个关于[独立变量](@entry_id:267118) $\mathbf{U}$ 的标准 PCE。这种方法将相关性的复杂性从测度（和[基函数](@entry_id:170178)）转移到了被展开的函数本身。虽然复合模型 $g(\mathbf{U})$ 可能比 $\mathcal{M}(\mathbf{X})$ 更复杂、更具[非线性](@entry_id:637147)，但它允许我们使用所有为独立变量开发的成熟工具，如[张量积](@entry_id:140694)基和标准求积/回归方法。[@problem_id:3411039]

无论采用哪种方法，如果 PCE 代理模型能够精确地（在几乎必然意义上）表示原模型，那么基于该代理进行的后续推断（例如，在贝叶斯框架下计算[后验分布](@entry_id:145605)）将与使用原模型得到的结果完全一致。选择哪种表示法只是一个计算上的便利问题，而非根本性的区别。[@problem_id:3411039]