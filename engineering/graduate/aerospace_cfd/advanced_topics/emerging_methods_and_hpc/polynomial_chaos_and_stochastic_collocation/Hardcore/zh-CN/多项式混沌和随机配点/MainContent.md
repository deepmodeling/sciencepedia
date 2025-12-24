## 引言
在现代计算科学与工程中，仅仅得出一个确定性的仿真结果已远远不够。模型的输入参数，如材料属性、边界条件或几何尺寸，往往存在固有的不确定性。忽略这些不确定性可能导致对系统性能的预测过于乐观，甚至引发灾难性的设计缺陷。因此，不确定性量化 (Uncertainty Quantification, UQ) 已成为确保仿真预测可靠性和鲁棒性的关键环节。多项式混沌 (Polynomial Chaos, PC) 和随机配置 (Stochastic Collocation, SC) 方法正是 UQ 领域中最强大、最受推崇的两大支柱。

本文旨在系统性地解决如何将输入端的不确定性有效地传播通过复杂的[计算模型](@entry_id:637456)，并量化其对最终输出结果影响的问题。我们将深入探讨 PC 和 SC 方法，从其数学原理到实际应用，为读者构建一个完整的知识体系。

本文将分为三个核心章节。在“原理与机制”中，我们将奠定理论基础，阐明如何用[随机变量](@entry_id:195330)表示不确定性，如何构建[正交多项式](@entry_id:146918)基，以及如何计算展开系数。随后，在“应用与跨学科联系”中，我们将通过流体力学、材料科学、贝叶斯推断等领域的丰富案例，展示这些方法的强大威力与广泛适用性。最后，“动手实践”部分将提供具体的编程练习，帮助您将理论知识转化为解决实际问题的能力。读完本文，您将能够掌握使用 PC 和 SC 方法进行严谨 UQ 分析的核心技能。

## 原理与机制

在[计算流体力学](@entry_id:747620) (CFD) 和其他计算科学与工程领域中，对不确定性进行量化已成为确保仿真结果可靠性和鲁棒性的关键步骤。多项式混沌 (Polynomial Chaos, PC) 和随机配置 (Stochastic Collocation, SC) 方法是现代[不确定性量化 (UQ)](@entry_id:756296) 的两大支柱，它们提供了一种系统性的框架，用于表征和传播模型输入中的不确定性，以评估其对输出量的影响。本章旨在阐述这些方法背后的核心原理和关键机制，为后续章节的应用和高级主题奠定理论基础。

### 不确定性的[参数化](@entry_id:265163)表示：从随机场到[随机变量](@entry_id:195330)

许多由[偏微分](@entry_id:194612)方程 (PDE) 描述的物理系统，其参数本身就存在不确定性，例如材料属性、边界条件或几何形状。在 UQ 的框架下，我们的首要任务是用一组有限的[随机变量](@entry_id:195330)来表示这些不确定性输入，这构成了我们随机模型的基础。

#### 从[随机场](@entry_id:177952)到有限维度：Karhunen-Loève 展开

一个常见的不确定性来源是空间变化的物理属性，例如在椭圆型 PDE 中的扩散系数 $a(x, \omega)$，其中 $x$ 是空间坐标，$\omega$ 代表一个随机结果。这样的函数被称为**[随机场](@entry_id:177952)** (random field)。为了使计算变得可行，我们需要用有限数量的[随机变量](@entry_id:195330)来近似这个无限维度的不确定性。**Karhunen-Loève 展开 (KLE)** 提供了一种系统且最优的方法来实现这种降维。

KLE 将一个二阶[随机场](@entry_id:177952) $a(x, \omega)$（即具有[有限方差](@entry_id:269687)的场）分解为其均值 $\mu(x) = \mathbb{E}[a(x, \omega)]$ 以及一系列由不相关的[随机变量](@entry_id:195330) $\xi_n(\omega)$ 调制的确定性空间模态 $\phi_n(x)$：

$$ a(x, \omega) = \mu(x) + \sum_{n=1}^{\infty} \sqrt{\lambda_n} \xi_n(\omega) \phi_n(x) $$

在这里，对 $(\lambda_n, \phi_n(x))$ 是该场协方差算子的特征值和[特征函数](@entry_id:186820)，通过求解以下积分特征问题得到：

$$ \int_D C(x, y) \phi_n(y) \, \mathrm{d}y = \lambda_n \phi_n(x) $$

其中 $C(x, y) = \operatorname{Cov}(a(x, \omega), a(y, \omega))$ 是场的协方差函数。[随机变量](@entry_id:195330) $\xi_n$ 被构造为不相关的，具有零均值和单位方差（即 $\mathbb{E}[\xi_n] = 0$, $\mathbb{E}[\xi_n \xi_m] = \delta_{nm}$）。一个至关重要的性质是，如果原始场 $a(x, \omega)$ 是[高斯随机场](@entry_id:749757)，那么变量 $\xi_n$ 不仅是不相关的，而且是[相互独立](@entry_id:273670)且服从[标准正态分布](@entry_id:184509)的。

KLE 在以下意义上是最优的：对于任意有限数量的项 $M$，截断展开

$$ a_M(x, \omega) = \mu(x) + \sum_{n=1}^{M} \sqrt{\lambda_n} \xi_n(\omega) \phi_n(x) $$

在所有使用 $M$ 个基函数的表示中，能够最小化均方误差 $\mathbb{E}[\|a - a_M\|_{L^2(D)}^2]$。场的总方差由特征值之和 $\sum_{n=1}^{\infty} \lambda_n$ 给出，而截断的均方误差就是被忽略的特征值之和 $\sum_{n=M+1}^{\infty} \lambda_n$。这提供了一个有原则的截断准则：我们选择足够大的 $M$ 以捕获总方差的期望比例，例如，选择 $M$ 使得对于某个小容差 $\varepsilon$，满足 $\sum_{n=1}^{M} \lambda_n \ge (1-\varepsilon) \sum_{n=1}^{\infty} \lambda_n$。

这个过程有效地将一个依赖于无限维随机场的问题，转化为一个依赖于有限维不[相关随机变量](@entry_id:200386)向量 $\boldsymbol{\xi} = (\xi_1, \dots, \xi_M)$ 的问题，为[多项式混沌](@entry_id:196964)等方法铺平了道路。

#### 处理相关的[随机变量](@entry_id:195330)

一旦我们有了一个有限维的随机输入向量 $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$，下一个挑战就是处理它们之间的依赖结构。[多项式混沌](@entry_id:196964)方法最容易为**独立**的[随机变量](@entry_id:195330)构建。如果输入变量是相关的，我们有两种主要策略。

第一种也是最常见的策略，是寻找一个**等概率变换 (isoprobabilistic transform)** $T$，将原始的相关向量 $\boldsymbol{\xi}$ 映射到一个由独立变量组成的新向量 $\boldsymbol{\eta}$，使得 $\boldsymbol{\xi} = T(\boldsymbol{\eta})$ 在分布上成立。然后我们就可以在更简单的[独立变量](@entry_id:267118) $\boldsymbol{\eta}$ 的空间中进行分析。 

这类变换的两个重要例子是：

1.  **Rosenblatt 变换**：对于任何具有已知[联合分布](@entry_id:263960)的[连续随机变量](@entry_id:166541)集，此变换是精确且普遍适用的。它使用一串条件[累积分布函数 (CDF)](@entry_id:264700) [递归定义](@entry_id:266613)。尽管功能强大且通用，但其实际实现可能很复杂，因为它需要了解完整的[联合分布](@entry_id:263960)，并且其最终的映射依赖于所选变量的排序。

2.  **Nataf 变换**：当只有变量 $X_i$ 的边缘分布及其[相关矩阵](@entry_id:262631)已知时，此变换被广泛使用。它在一个简化的假设下运作，即依赖结构（即 copula）是高斯的。该变换首先将每个边缘变量映射到一个标准正态变量，从而创建一个相关的多维高斯向量，然后通过线性变换（例如，对[相关矩阵](@entry_id:262631)进行 Cholesky 分解）来[解耦](@entry_id:160890)。Nataf 变换仅在真实依赖性确实为高斯时才是精确的；否则，它提供了一个保留了边缘分布和相关结构的近似。

处理相关输入的第二种策略是完全绕过变换，直接构建一个相对于相关变量 $\boldsymbol{\xi}$ 的[联合概率](@entry_id:266356)测度正交的多元多项式基。例如，这可以通过 Gram-Schmidt [正交化](@entry_id:149208)过程实现。虽然理论上是合理的，但这种“数据驱动”的方法在计算上可能要求很高。

### [广义多项式混沌 (gPC)](@entry_id:749789) 展开

一旦我们将[不确定性表示](@entry_id:1133583)为由 $d$ 个[独立随机变量](@entry_id:273896) $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$ 组成的向量，我们就可以表示一个依赖于这些不确定性的物理量 $u(\boldsymbol{\xi})$。[广义多项式混沌 (gPC)](@entry_id:749789) 的核心思想是将 $u(\boldsymbol{\xi})$ 展开为一系列关于 $\boldsymbol{\xi}$ 的正交多项式。

#### 正交性：gPC 的基石

假设 $u(\boldsymbol{\xi})$ 是一个具有[有限方差](@entry_id:269687)的量（即，在加权 $L^2$ 空间中）。gPC 展开的形式为：

$$ u(\boldsymbol{\xi}) = \sum_{\boldsymbol{\alpha} \in \mathbb{N}_0^d} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) $$

其中 $\boldsymbol{\alpha} = (\alpha_1, \dots, \alpha_d)$ 是一个多重指标，$c_{\boldsymbol{\alpha}}$ 是展开系数，$\{\Psi_{\boldsymbol{\alpha}}\}$ 是一组多元[正交多项式](@entry_id:146918)基。这里的**正交性**是关键，它定义为相对于 $\boldsymbol{\xi}$ 的联合概率测度。如果 $\boldsymbol{\xi}$ 的[联合概率密度函数](@entry_id:267139) (PDF) 为 $\rho(\boldsymbol{\xi})$，则两个基函数 $\Psi_{\boldsymbol{\alpha}}$ 和 $\Psi_{\boldsymbol{\beta}}$ 的[内积](@entry_id:750660)定义为它们乘[积的期望](@entry_id:190023)：

$$ \langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \mathbb{E}[\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})] = \int_{\Gamma} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi}) \rho(\boldsymbol{\xi}) \, d\boldsymbol{\xi} = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}} $$

其中 $\delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$ 是 Kronecker delta，$\Gamma$ 是 $\boldsymbol{\xi}$ 的支撑域。这种正交性（或更准确地说是**正交归一性**）极大地简化了 gPC 框架。它确保了 gPC 展开是 $L^2$ 空间中的一种最优均方近似，类似于确定性函数在傅里叶级数中的展开。

得益于正交性，gPC 系数 $c_{\boldsymbol{\alpha}}$ 可以通过将 $u(\boldsymbol{\xi})$ 投影到相应的基函数上来直接计算：

$$ c_{\boldsymbol{\alpha}} = \langle u, \Psi_{\boldsymbol{\alpha}} \rangle = \mathbb{E}[u(\boldsymbol{\xi}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})] $$

这是一个基础性的结果，表明 gPC 展开的系数就是广义的[傅里叶系数](@entry_id:144886)。此外，截断展开的均方误差由被截断的系数的平方和给出，这是希尔伯特空间中[毕达哥拉斯定理](@entry_id:264352)的一个推论，类似于[帕塞瓦尔恒等式](@entry_id:147134)。

#### Wiener-Askey 框架：为概率分布选择合适的多项式

选择哪个多项式族 $\{\Psi_{\boldsymbol{\alpha}}\}$ 取决于输入[随机变量](@entry_id:195330) $\boldsymbol{\xi}$ 的概率分布。**Wiener-Askey 框架**为常见的连续和[离散概率分布](@entry_id:166565)与经典的[超几何正交多项式](@entry_id:182622)族之间建立了对应关系。这种匹配确保了所选的多项式基对于相应分布的[概率测度](@entry_id:190821)是正交的，从而保证了 gPC 展开的快速收敛（对于[解析函数](@entry_id:139584)，即所谓的**[谱收敛](@entry_id:142546)**）。

一些关键的对应关系包括：
-   **高斯分布** ($\mathcal{N}(\mu, \sigma^2)$) $\longleftrightarrow$ **Hermite 多项式**。
-   **均匀分布** ($\mathcal{U}(a, b)$) $\longleftrightarrow$ **Legendre 多项式**。
-   **Beta 分布** ($\mathrm{Beta}(\alpha, \beta)$) $\longleftrightarrow$ **Jacobi 多项式**。
-   **Gamma 分布** ($\mathrm{Gamma}(k, \theta)$) $\longleftrightarrow$ **Laguerre 多项式**。

例如，如果一个输入 $\eta$ 服从高斯分布 $\mathcal{N}(M_\infty, \sigma^2)$，我们首先将其标准化为 $Z = (\eta - M_\infty)/\sigma$，使其服从[标准正态分布](@entry_id:184509) $\mathcal{N}(0,1)$。然后，我们使用 Hermite 多项式作为 $Z$ 的基。如果某个输出量 $Q$ 是 $\eta$ 的一个 $p$ 次多项式，那么它也可以表示为 $Z$ 的一个 $p$ 次多项式。由于任何 $p$ 次多项式都可以精确地表示为最高 $p$ 次的 Hermite 多项式的有限和，因此其 gPC 展开中所有高于 $p$ 次的系数都将为零。

对于独立的[随机变量](@entry_id:195330) $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$，多元[正交基](@entry_id:264024) $\{\Psi_{\boldsymbol{\alpha}}\}$ 可以通过对每个变量对应的单变量[正交多项式](@entry_id:146918)族进行[张量积](@entry_id:140694)来构建。

#### 截断策略与多重[指标集](@entry_id:268489)

在实践中，无限的 gPC 级数必须被截断为一个有限和。这通过选择一个有限的多重[指标集](@entry_id:268489) $\mathcal{A}$ 来实现：

$$ u(\boldsymbol{\xi}) \approx u_{\mathcal{A}}(\boldsymbol{\xi}) = \sum_{\boldsymbol{\alpha} \in \mathcal{A}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) $$

选择 $\mathcal{A}$ 的方式对方法的效率和准确性有显著影响，尤其是在高维问题中（即 $d$ 很大时），这被称为**维数灾难**。两种常见的各向同性[指标集](@entry_id:268489)是：

1.  **总阶数 (Total Degree, TD) 集**: $\mathcal{A}_p^{\mathrm{TD}} = \{\boldsymbol{\alpha} \in \mathbb{N}_0^d : \sum_{k=1}^d \alpha_k \le p\}$。这个集合包含所有总阶数不超过 $p$ 的多项式。其[基数](@entry_id:754020)（即展开中的项数）为 $|\mathcal{A}_p^{\mathrm{TD}}| = \binom{p+d}{d}$，随着维度 $d$ 的增加，这个数量会以 $d^p$ 的速度增长，增长非常迅速。

2.  **双曲交叉 (Hyperbolic Cross, HC) 集**: $\mathcal{A}_p^{\mathrm{HC}} = \{\boldsymbol{\alpha} \in \mathbb{N}_0^d : \prod_{k=1}^{d}(\alpha_k+1) \le p+1\}$。这种截断策略倾向于包含混合阶数的项（即多个 $\alpha_k$ 非零），而惩罚单一变量的高阶项。对于许多物理问题，高阶[交互作用](@entry_id:164533)的重要性会迅速下降，因此这种策略可以更有效地构建近似。对于固定的 $p$，HC 集的[基数](@entry_id:754020)随维度 $d$ 的增长速度远慢于 TD 集，其增长速度是 $d$ 的多项式，阶数约为 $\log_2(p)$。这使得 HC 集在高维问题中成为一个更有吸[引力](@entry_id:189550)的选择。

### 计算 gPC 系数：侵入式与非侵入式方法

确定了 gPC 展开的形式后，核心任务就是计算系数 $c_{\boldsymbol{\alpha}}$。主要有两种方法：侵入式和非侵入式。

#### 侵入式方法：随机 Galerkin (SG)

**随机 Galerkin (SG) 方法**直接在控制方程的弱形式上进行操作。它将 gPC 展开式代入到不确定参数和待求解的解中，然后将得到的随机残差投影到 gPC 基的每个多项式上，使其在期望意义下为零。

考虑一个随机[椭圆问题](@entry_id:146817) $-\nabla \cdot (k(x, \boldsymbol{\xi}) \nabla u(x, \boldsymbol{\xi})) = f(x)$。我们用 gPC 展开来近似 $k(x, \boldsymbol{\xi}) = \sum_r k_r(x) \Psi_r(\boldsymbol{\xi})$ 和 $u(x, \boldsymbol{\xi}) = \sum_j u_j(x) \Psi_j(\boldsymbol{\xi})$。将这些代入 PDE 的弱形式，并对每个基函数 $\Psi_i(\boldsymbol{\xi})$ 进行 Galerkin 投影（即乘以 $\Psi_i$ 并取期望），会产生一个关于未知系数场 $u_j(x)$ 的耦合确定性 PDE 系统。

经过[空间离散化](@entry_id:172158)（例如，使用有限元方法 FEM），这个耦合的 PDE 系统变成了一个大型的、耦合的代数系统。其一般形式为：

$$ \sum_{j=0}^{P} \left( \sum_{r=0}^{R} T_{ijr} \, K^{(r)} \right) U_{j} = \delta_{i0} \, f^{h} $$

其中 $U_j$ 是系数 $u_j(x)$ 的有限元[节点向量](@entry_id:176218)，$K^{(r)}$ 是与 $k_r(x)$ 相关的[刚度矩阵](@entry_id:178659)，$f^h$ 是确定性[载荷向量](@entry_id:635284)。耦合是由**三阶张量** $T_{ijr} = \langle \Psi_i \Psi_j \Psi_r \rangle$ 引入的，它代表了 gPC 基函数的三重[积的期望](@entry_id:190023)。这个过程被称为**侵入式 (intrusive)**，因为它需要对确定性求解器的源代码进行重大修改，以组装和求解这个新的、更大的耦合系统。 

#### 非侵入式方法：随机配置 (SC)

与侵入式方法形成对比，**非侵入式 (non-intrusive)** 方法将确定性 PDE 求解器视为一个“黑箱”。它通过在随机空间中精心选择的点上重复运行求解器来收集信息，然后用这些信息来构建 gPC 展开。

**随机配置 (SC)** 是非侵入式方法中的一种，其核心思想是插值或回归。该过程如下：
1.  在随机[参数空间](@entry_id:178581) $\Gamma$ 中选择一组**[配置点](@entry_id:169000)** $\{\boldsymbol{\xi}^{(m)}\}_{m=1}^M$。这些点通常是基于为底层[概率测度](@entry_id:190821)设计的[数值积分](@entry_id:136578)（求积）规则（如 Gauss 求积或 Clenshaw-Curtis 求积）的[稀疏网格](@entry_id:139655)或[张量积网格](@entry_id:755861)节点。
2.  对于每个[配置点](@entry_id:169000) $\boldsymbol{\xi}^{(m)}$，运行确定性求解器，得到一个确定性解 $u(\boldsymbol{\xi}^{(m)})$。这相当于将求解器作为[黑箱函数](@entry_id:163083)进行 $M$ 次调用。
3.  利用这 $M$ 个解的“快照”来构建 $u(\boldsymbol{\xi})$ 的全局多项式近似。这可以通过构造一个在[配置点](@entry_id:169000)上与快照值相匹配的[多项式插值](@entry_id:145762)来实现。

另一种密切相关的非侵入式方法是**伪[谱投影](@entry_id:265201) (pseudospectral projection)**。它直接利用 gPC 系数的积分定义 $c_{\boldsymbol{\alpha}} = \mathbb{E}[u(\boldsymbol{\xi}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]$。这个期望（即积分）通过数值求积来近似：

$$ \hat{c}_{\boldsymbol{\alpha}} = \sum_{m=1}^M u(\boldsymbol{\xi}^{(m)}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}^{(m)}) w_m $$

其中 $\{\boldsymbol{\xi}^{(m)}\}$ 和 $\{w_m\}$ 分别是求积点和相应的权重。如果 $u(\boldsymbol{\xi})$ 本身是一个多项式，并且使用了足够高精度的[求积规则](@entry_id:753909)，那么计算出的系数 $\hat{c}_{\boldsymbol{\alpha}}$ 将是精确的。例如，如果 $u(\boldsymbol{\xi})\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$ 的总阶数最高为 $D_{max}$，那么一个对所有阶数不超过 $D_{max}$ 的多项式都精确的[求积规则](@entry_id:753909)将能精确地计算出系数。 

因为这些方法只需要对现有求解器进行重复调用，而无需修改其内部代码，所以它们被称为**非侵入式**的，这使得它们在与复杂的、专有的或遗留的 CFD 代码集成时特别有吸[引力](@entry_id:189550)。

### gPC 展开的应用：后处理与分析

一旦计算出 gPC 系数 $\{c_{\boldsymbol{\alpha}}\}$，我们就获得了一个关于不确定性输入的输出量的紧凑、解析的代理模型。这个代理模型可以被高效地用于各种后处理分析。

#### [统计矩](@entry_id:268545)的计算

由于 gPC 基的正交性，输出量 $u$ 的统计矩可以直接从其 gPC 系数中解析地、几乎无成本地计算出来。

-   **均值 (Mean)**：均值就是零阶 gPC 系数，因为所有[高阶基函数](@entry_id:165641)的期望均为零。
    $$ \mathbb{E}[u] = c_{\boldsymbol{0}} $$

-   **方差 (Variance)**：方差是所有非零阶 gPC 系数的[平方和](@entry_id:161049)。这源于[希尔伯特空间](@entry_id:261193)中的[毕达哥拉斯定理](@entry_id:264352)（或[帕塞瓦尔恒等式](@entry_id:147134)）。
    $$ \mathrm{Var}[u] = \mathbb{E}[(u - \mathbb{E}[u])^2] = \mathbb{E}\left[\left(\sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}\right)^2\right] = \sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}}^2 $$

例如，对于一个依赖于单个标准正态变量 $\xi$ 的量，其二阶 gPC 展开为 $u(\xi) = u_0 \psi_0(\xi) + u_1 \psi_1(\xi) + u_2 \psi_2(\xi)$，其中 $\{\psi_i\}$ 是正交归一的 Hermite 多项式。其均值为 $\mathbb{E}[u] = u_0$，方差为 $\mathrm{Var}[u] = u_1^2 + u_2^2$。

#### [全局敏感性分析 (GSA)](@entry_id:749930)

**[全局敏感性分析 (GSA)](@entry_id:749930)** 旨在量化各个输入不确定性对输出方差的贡献。gPC 展开为计算基于方差的**Sobol' 指数**提供了一个极其高效的途径，因为 gPC 展开本身就是一种**[方差分析 (ANOVA)](@entry_id:262372)** 分解的函数形式。

gPC 展开中的每一项 $c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$ 都只依赖于多重指标 $\boldsymbol{\alpha}$ 的支撑集（即非零元素对应的变量子集）中的变量。我们可以根据其依赖的变量子集对 gPC 系数进行分组。

总方差 $V = \sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}}^2$ 可以分解为与不同变量子集相关的偏方差之和。对于一个变量子集 $A \subseteq \{1, \dots, d\}$：

-   **一阶 Sobol' 指数 (First-order Sobol' index)** $S_A$：衡量变量子集 $A$ 的主要影响（不包括与其他变量的[交互作用](@entry_id:164533)）对总方差的贡献。它可以通过对所有其支撑集为 $A$ 的非空子集的 gPC 系数的平方求和来计算：
    $$ S_A = \frac{1}{V} \sum_{\emptyset \neq U \subseteq A} \left( \sum_{\boldsymbol{\alpha} : \mathrm{supp}(\boldsymbol{\alpha}) = U} c_{\boldsymbol{\alpha}}^2 \right) = \frac{1}{V} \sum_{\boldsymbol{\alpha} : \emptyset \neq \mathrm{supp}(\boldsymbol{\alpha}) \subseteq A} c_{\boldsymbol{\alpha}}^2 $$

-   **总效应 Sobol' 指数 (Total-effect Sobol' index)** $S_{T,A}$：衡量变量子集 $A$ 的所有影响（包括其自身的主要影响以及与所有其他变量的全部[交互作用](@entry_id:164533)）对总方差的贡献。它可以通过对所有其支撑集与 $A$ 有非空交集的 gPC 系数的平方求和来计算：
    $$ S_{T,A} = \frac{1}{V} \sum_{\boldsymbol{\alpha} : \mathrm{supp}(\boldsymbol{\alpha}) \cap A \neq \emptyset} c_{\boldsymbol{\alpha}}^2 $$

利用这些公式，一旦 gPC 系数可用，计算所有 Sobol' 指数就仅仅是简单的代数运算，无需额外的模型运行。这使得 gPC 成为进行详细[敏感性分析](@entry_id:147555)的强大工具。