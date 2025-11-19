## 引言
在现代工程与科学计算中，有限元方法（FEM）已成为分析复杂物理系统行为不可或缺的工具。然而，传统的确定性分析假设所有模型参数、几何形状和边界条件都是精确已知的，这与充满不确定性的现实世界相去甚远。材料属性的固有变异、制造[公差](@entry_id:275018)、环境载荷的波动等随机因素，都可能对系统的性能和安全性产生显著影响。因此，如何量化这些不确定性并预测其对[系统响应](@entry_id:264152)的影响，已成为一个核心的科学与工程挑战。

[随机有限元](@entry_id:755461)方法（SFEM）正是为应对这一挑战而生的一套强大的计算框架。它将概率论与[有限元法](@entry_id:749389)相结合，使得我们能够在模型中直接处理不确定性，从而得到响应量的完整概率信息，而不仅仅是一个确定性的预测值。这为进行可靠性设计、[风险评估](@entry_id:170894)和稳健性优化提供了坚实的理论基础。

本文旨在为读者提供一个关于[随机有限元](@entry_id:755461)方法的全面而深入的指南，涵盖从基本原理到前沿应用的完整知识体系。本指南将分三章引领读者系统地掌握SFEM：第一章“原理与机制”将奠定理论基础，详细阐述如何使用随机场表示不确定性，并通过[Karhunen-Loève展开](@entry_id:751050)和[多项式混沌展开](@entry_id:162793)等技术进行离散化，最后对比侵入式和非侵入式两种主流求解策略。第二章“应用与跨学科交叉”将展示SFEM在解决[非线性力学](@entry_id:178303)、[结构动力学](@entry_id:172684)、[多物理场耦合](@entry_id:171389)及[可靠性分析](@entry_id:192790)等复杂问题时的强大能力，并探讨其与数据科学等领域的交叉融合。最后一章“动手实践”则提供了一系列计算练习，旨在帮助读者将理论知识转化为解决实际问题的能力。

## 原理与机制

本章旨在深入探讨[随机有限元](@entry_id:755461)方法（SFEM）的核心原理与底层机制。我们将从如何在[连续介质力学](@entry_id:155125)中数学地表示不确定性出发，介绍用于描述空间变化属性的随机场概念。随后，我们将详细阐述两种关键的随机性离散化技术——[Karhunen-Loève展开](@entry_id:751050)和[多项式混沌展开](@entry_id:162793)，它们能将无限维的随机场转化为有限数量的[随机变量](@entry_id:195330)。最后，我们将对比研究求解最终随机[方程组](@entry_id:193238)的两种主流策略：[侵入式随机伽辽金法](@entry_id:750793)和非侵入式[配置法](@entry_id:142690)，分析它们在实现、并行性、[误差控制](@entry_id:169753)和[计算效率](@entry_id:270255)方面的权衡。

### 连续系统中的[不确定性建模](@entry_id:268420)：[随机场](@entry_id:177952)

在确定性[有限元分析](@entry_id:138109)中，材料属性（如[弹性模量](@entry_id:198862) $E$）和载荷通常被假定为在空间上均匀或以确定性函数形式变化的。然而，在现实世界的工程问题中，这些量往往由于制造过程中的变异、环境波动或知识的局限性而表现出不确定性。为了在力学模型中捕捉这种空间相关的不确定性，我们需要引入**随机场**（random field）的概念。

从形式上看，一个随机场 $a(x, \theta)$ 是一个由两个变量索引的函数：一个物理空间坐标 $x \in D$（其中 $D$ 是物理域），以及一个来自[样本空间](@entry_id:275301) $\Omega$ 的随机结果 $\theta$。对于固定的物理点 $x_0$，函数 $\theta \mapsto a(x_0, \theta)$ 是一个**[随机变量](@entry_id:195330)**（random variable），它描述了该点上物理量的不确定性。而对于一个固定的随机结果 $\theta_0$，函数 $x \mapsto a(x, \theta_0)$ 是一个确定性函数，被称为随机场的一个**样本路径**（sample path）或实现。将随机场视为由空间坐标 $x$ 索引的一族[随机变量](@entry_id:195330) $\lbrace a(x, \cdot) : x \in D \rbrace$ 是很有帮助的。从这个角度看，随机场是**[随机过程](@entry_id:159502)**（stochastic process）概念在多维索引集（即空间域 $D \subset \mathbb{R}^d, d \ge 1$）上的推广 [@problem_id:2687009]。

在建立一个严谨的[随机有限元](@entry_id:755461)框架时，对随机场进行严格的数学定义至关重要。例如，在求解[随机偏微分方程](@entry_id:188292)的[弱形式](@entry_id:142897)时，我们经常需要[交换空间](@entry_id:755701)积分和期望（即在概率空间上的积分）的顺序。根据[Fubini定理](@entry_id:136363)，这种操作的合法性要求被积函数在乘[积空间](@entry_id:151693) $D \times \Omega$上是可测的，并且其[绝对值](@entry_id:147688)是可积的。这引出了**二阶[随机场](@entry_id:177952)**的现代理论定义。一个[随机场](@entry_id:177952) $a(x, \theta)$ 被称为二阶随机场，如果它在乘积[测度空间](@entry_id:191702) $(D \times \Omega, \mathcal{B}(D) \otimes \mathcal{F}, \text{Lebesgue} \otimes \mathbb{P})$ 上是平方可积的，即 $a \in L^2(D \times \Omega)$。这里，$(\Omega, \mathcal{F}, \mathbb{P})$ 是一个完备的[概率空间](@entry_id:201477)。这个紧凑的定义蕴含了以下关键属性 [@problem_id:2686919]：
1.  **联合可测性**：函数 $a(x, \theta)$ 必须对于乘积$\sigma$-代数 $\mathcal{B}(D) \otimes \mathcal{F}$ 是可测的。
2.  **积分可积性**：积分 $\int_{\Omega} \int_{D} |a(x, \theta)|^2 \, \mathrm{d}x \, \mathrm{d}\mathbb{P}(\theta)  \infty$。

这个积分条件等价于要求[随机场](@entry_id:177952)的样本路径对于$\mathbb{P}$-几乎所有的 $\theta$ 都是空间平方可积的（即 $a(\cdot, \theta) \in L^2(D)$），并且从[概率空间](@entry_id:201477)到[希尔伯特空间](@entry_id:261193) $L^2(D)$ 的映射 $\theta \mapsto a(\cdot, \theta)$ 是Bochner平方可积的。这个函数分析框架是现代SFE[M理论](@entry_id:161892)的基石。

[随机场](@entry_id:177952)的另一个重要性质是其样本路径的**正则性**（regularity），例如连续性。样本路径的光滑程度直接影响[随机偏微分方程](@entry_id:188292)解的正则性。虽然一个随机场的均方连续性（即 $\lim_{y \to x} \mathbb{E}[|a(y, \theta) - a(x, \theta)|^2] = 0$）并不足以保证其样本路径的连续性，但更强的条件可以。例如，**[Kolmogorov-Chentsov连续性定理](@entry_id:180697)**提供了一个充分条件：如果存在常数 $p0$, $\eta0$, 和 $C\infty$，使得对于所有 $x, y \in D$，增量的 $p$-阶矩满足 $\mathbb{E}[|a(x, \theta) - a(y, \theta)|^p] \le C \|x-y\|^{d+\eta}$，那么该[随机场](@entry_id:177952)（或其一个版本）的样本路径[几乎必然](@entry_id:262518)是Hölder连续的，因此也是连续的 [@problem_id:2687009]。

最后，值得区分不确定性的两种基本类型：**偶然不确定性**（aleatory uncertainty）和**[认知不确定性](@entry_id:149866)**（epistemic uncertainty）。偶然不确定性源于系统固有的、不可约的随机性，如风载荷的波动。它最适合用经典的、基于频率的概率论来建模，即为一个[随机变量](@entry_id:195330)指定一个明确的[概率分布](@entry_id:146404)。认知不确定性则源于知识的缺乏，原则上可以通过收集更多数据或改进模型来减少。例如，由于[材料测试](@entry_id:196870)数据稀疏而导致的[弹性模量](@entry_id:198862)不确定性。将这种不确定性赋予一个精确的[概率分布](@entry_id:146404)可能具有误导性。更严谨的处理方法包括非概率的区间模型（如 $E \in [E_{\min}, E_{\max}]$）或贝叶斯方法，其中概率被解释为一种[置信度](@entry_id:267904)，并可以通过新数据进行更新 [@problem_id:2686928]。在SFEM中，虽然通常将所有不确定性都形式化为概率模型，但理解其来源对于模型的建立和结果的解释至关重要。

### 随机性的离散化

为了在计算机上处理随机场，我们必须将其用有限数量的参数来表示。这个过程被称为随机性的离散化。两种最主流的方法是[Karhunen-Loève展开](@entry_id:751050)和[多项式混沌展开](@entry_id:162793)。

#### [Karhunen-Loève展开](@entry_id:751050)

**Karhunen-Loève (K-L) 展开**为二阶[随机场](@entry_id:177952)提供了一种最优的[级数表示](@entry_id:175860)。其核心思想是对[随机场](@entry_id:177952)的[协方差函数](@entry_id:265031)进行谱分解。对于一个零均值的二阶随机场 $a(x, \theta)$，其[协方差函数](@entry_id:265031)定义为 $C(x, x') := \mathbb{E}[a(x, \theta) a(x', \theta)]$。这个函数是空间坐标的对称非负定核。我们可以定义一个相关的[积分算子](@entry_id:262332)，称为协[方差](@entry_id:200758)算子 $\mathcal{K}$：
$$
(\mathcal{K}\varphi)(x) := \int_D C(x, x') \, \varphi(x') \, \mathrm{d}x'
$$
根据[Mercer定理](@entry_id:264894)，这个紧的、自伴的、非负定的算子 $\mathcal{K}$ 存在一个[谱分解](@entry_id:173707)。它有一系列非负[特征值](@entry_id:154894) $\lambda_n \ge 0$ 和相应的特征函数 $\phi_n(x)$，这些特征函数在 $L^2(D)$ 空间中是正交的。它们满足以下积分特征值问题 [@problem_id:2600438]：
$$
\int_D C(x, x') \, \phi_n(x') \, \mathrm{d}x' = \lambda_n \, \phi_n(x)
$$
K-L展开将随机场 $a(x, \theta)$ 表示为由这些确定性特征函数 $\phi_n(x)$ 作为基，与一组不相关的[随机变量](@entry_id:195330) $\xi_n(\theta)$ 作为系数的无穷级数：
$$
a(x, \theta) = \sum_{n=1}^\infty \sqrt{\lambda_n} \, \xi_n(\theta) \, \phi_n(x)
$$
这里的[随机变量](@entry_id:195330) $\xi_n(\theta)$ 满足 $\mathbb{E}[\xi_n] = 0$ 和 $\mathbb{E}[\xi_m \xi_n] = \delta_{mn}$（即它们是标准化的、不相关的）。$\{\phi_n(x)\}$ 是一个 $L^2(D)$ 正交归一基。这个级数在 $L^2(\Omega; L^2(D))$ 意义下收敛。K-L展开的一个关键优势是其**最优性**：在所有具有相同数量项的线性展开中，截断的K-L展开能够最小化均方[截断误差](@entry_id:140949)。

另一种等价的表示形式使用非[标准化](@entry_id:637219)的系数 $\eta_n(\theta) = \sqrt{\lambda_n} \xi_n(\theta)$，其协[方差](@entry_id:200758)为 $\mathbb{E}[\eta_m \eta_n] = \lambda_n \delta_{mn}$ [@problem_id:2600438]：
$$
a(x, \theta) = \sum_{n=1}^\infty \eta_n(\theta) \, \phi_n(x)
$$
在实践中，我们截取级数的前 $M$ 项来近似[随机场](@entry_id:177952)，从而将无限维的随机场表示简化为 $M$ 个不相关的[随机变量](@entry_id:195330) $\lbrace \xi_1, \dots, \xi_M \rbrace$。如果原[随机场](@entry_id:177952)是高斯场，那么这些系数 $\xi_n$ 也是独立的高斯[随机变量](@entry_id:195330)。

#### [多项式混沌展开](@entry_id:162793)

**[多项式混沌展开](@entry_id:162793) (PCE)** 是另一种强大的随机性离散化技术。与K-L展开专注于表示输入随机场不同，PCE可以用来表示任何二阶随机量，包括模型的输出（如位移场或应[力场](@entry_id:147325)）。其核心思想是将一个随机量 $u(x, \theta)$ 表示为一个由[随机变量](@entry_id:195330) $\boldsymbol{\xi}(\theta) = (\xi_1, \dots, \xi_M)$ 的正交多项式构成的级数。

假设模型的不确定性可以由一个 $M$ 维随机向量 $\boldsymbol{\xi}$ 描述，其[联合概率密度函数](@entry_id:267139)为 $\rho(\boldsymbol{\xi})$。PCE将模型输出 $u(x, \theta)$（对于固定的 $x$）展开为：
$$
u(x, \theta) = \sum_{\alpha \in \mathbb{N}_0^M} u_{\alpha}(x) \, \Psi_{\alpha}(\boldsymbol{\xi}(\theta))
$$
其中 $\alpha$ 是多重指标， $u_{\alpha}(x)$ 是确定性的系数场，而 $\lbrace \Psi_{\alpha}(\boldsymbol{\xi}) \rbrace$ 是一个多项式基，它关于 $\boldsymbol{\xi}$ 的[概率测度](@entry_id:190821)是正交的 [@problem_id:2686986]：
$$
\mathbb{E}[\Psi_{\alpha}(\boldsymbol{\xi}) \Psi_{\beta}(\boldsymbol{\xi})] = \int \Psi_{\alpha}(\boldsymbol{\xi}) \Psi_{\beta}(\boldsymbol{\xi}) \, \rho(\boldsymbol{\xi}) \, \mathrm{d}\boldsymbol{\xi} = \delta_{\alpha\beta}
$$
（这里假设基是正交归一的）。由于正交性，系数可以通过投影得到：
$$
u_{\alpha}(x) = \mathbb{E}[u(x, \theta) \Psi_{\alpha}(\boldsymbol{\xi}(\theta))]
$$
PCE的[收敛速度](@entry_id:636873)很大程度上取决于所选多项式基与输入[随机变量](@entry_id:195330) $\boldsymbol{\xi}$ 的[概率分布](@entry_id:146404)的匹配程度。**Wiener-[Askey方案](@entry_id:187960)**系统地建立了这种对应关系 [@problem_id:2600479]。该方案指出，为了获得最佳收敛性，多项式的权重函数应与[随机变量](@entry_id:195330)的[概率密度函数](@entry_id:140610)（经过适当的[仿射变换](@entry_id:144885)后）相匹配。一些关键的对应关系包括 [@problem_id:2686986, @problem_id:2600479]：
-   **高斯**[分布](@entry_id:182848) $\rightarrow$ **Hermite** 多项式 (经典[Wiener混沌](@entry_id:181915))
-   **均匀**[分布](@entry_id:182848) $\rightarrow$ **Legendre** 多项式
-   **Gamma** [分布](@entry_id:182848) $\rightarrow$ **Laguerre** 多项式
-   **Beta** [分布](@entry_id:182848) $\rightarrow$ **Jacobi** 多项式

如果输入[随机变量](@entry_id:195330) $\xi_1, \dots, \xi_M$ 是相互独立的，那么多元[正交多项式](@entry_id:146918)基 $\Psi_{\alpha}(\boldsymbol{\xi})$ 可以简单地通过一维[正交多项式](@entry_id:146918)基的[张量积](@entry_id:140694)来构造：$\Psi_{\alpha}(\boldsymbol{\xi}) = \prod_{i=1}^M \psi_{i, \alpha_i}(\xi_i)$。如果变量是相关的，则必须针对其[联合概率分布](@entry_id:171550)构造多元正交基，例如通过[Gram-Schmidt正交化](@entry_id:143035)过程 [@problem_id:2686986]。

### 求解随机问题：侵入式与非侵入式方法

在将不确定性用有限个[随机变量](@entry_id:195330) $\boldsymbol{\xi}$ [参数化](@entry_id:272587)，并将所有随机量用PCE表示后，下一步是求解[随机控制](@entry_id:170804)方程。主要有两种策略：侵入式和非侵入式方法。

#### [侵入式随机伽辽金法](@entry_id:750793) (SGM)

侵入式方法，或称**[随机伽辽金法](@entry_id:178148) (SGM)**，其思想是将[伽辽金投影](@entry_id:145611)原理同时应用于物理空间和随机空间。我们从控制方程的[弱形式](@entry_id:142897)开始，它对几乎所有的 $\boldsymbol{\xi}$ 都成立。然后，我们将所有随机项（如材料属性 $E(x, \boldsymbol{\xi})$）和未知解（如位移 $u(x, \boldsymbol{\xi})$）代入它们的PCE形式。

以一维弹性杆为例，其随机弱形式为：求 $u(x, \boldsymbol{\xi})$ 使得对所有合适的检验函数 $v(x, \boldsymbol{\xi})$，
$$
\mathbb{E}\left[ \int_D E(x, \boldsymbol{\xi}) \frac{\partial u}{\partial x} \frac{\partial v}{\partial x} \, \mathrm{d}x \right] = \mathbb{E}\left[ \int_D f(x) v \, \mathrm{d}x \right]
$$
我们将解和检验函数都用[张量积](@entry_id:140694)形式表示，即空间[有限元基函数](@entry_id:749279) $N_j(x)$ 和随机[多项式混沌](@entry_id:196964)[基函数](@entry_id:170178) $\Psi_{\alpha}(\boldsymbol{\xi})$ 的乘积。例如，解的近似为 $u(x, \boldsymbol{\xi}) \approx \sum_{j, \alpha} \hat{u}_{j,\alpha} N_j(x) \Psi_{\alpha}(\boldsymbol{\xi})$。将这个近似代入[弱形式](@entry_id:142897)，并[选择检验](@entry_id:182706)函数为 $v(x, \boldsymbol{\xi}) = N_i(x) \Psi_{\beta}(\boldsymbol{\xi})$，对每个 $(i, \beta)$ 进行[伽辽金投影](@entry_id:145611)，最终会得到一个关于未知PCE系数 $\hat{u}_{j,\alpha}$ 的庞大的、耦合的确定性[线性方程组](@entry_id:148943)。

这个全局系统的矩阵具有特殊的块结构。如果材料属性对[随机变量](@entry_id:195330)是仿射依赖的，即 $E(x, \boldsymbol{\xi}) = \sum_{r=0}^R E_r(x) \Psi_r(\boldsymbol{\xi})$，则[全局刚度矩阵](@entry_id:138630) $\mathcal{K}$ 可以简洁地表示为克罗内克积的形式 [@problem_id:2686880]：
$$
\mathcal{K} = \sum_{r=0}^R G_r \otimes K_r
$$
其中，$K_r$ 是由材料系数场 $E_r(x)$ 产生的确定性空间刚度矩阵，而 $G_r$ 是随机空间中的“[三重积](@entry_id:162942)”矩阵，其元素为 $\mathbb{E}[\Psi_r \Psi_{\alpha} \Psi_{\beta}]$。这个耦合系统的大小为 $(N \times S) \times (N \times S)$，其中 $N$ 是空间自由度数，$S$ 是PCE[基函数](@entry_id:170178)个数。

SGM的一个主要挑战是其**计算复杂度**。组装和求解这个大型耦合系统的成本对随机维度 $m$ 和多项式阶数 $p$ 非常敏感。对于一个具有 $m$ 个[随机变量](@entry_id:195330)和总阶数为 $p$ 的PCE，[基函数](@entry_id:170178)数量 $S = \binom{p+m}{m}$。在理想情况下（例如，使用最优的预条件子），求解的总计算量与 $N \cdot m \cdot S$ 成正比，即 [@problem_id:2687016]：
$$
\text{Cost} \propto N m \binom{p+m}{m}
$$
当 $m$ 和 $p$ 增大时，$S$ 会发生组合爆炸，这种现象被称为**“维度灾难”**（curse of dimensionality），它限制了SGM在高维随机问题中的应用。

#### 非侵入式谱方法 ([随机配置法](@entry_id:174778))

与SGM深度修改求解器的方式不同，**非侵入式[谱方法](@entry_id:141737)**（通常称为**[随机配置法](@entry_id:174778)**）将确定性求解器视为一个“黑箱”。其基本思想是在随机[参数空间](@entry_id:178581) $\boldsymbol{\xi}$ 中选择一组巧妙的节点（[配置点](@entry_id:169000)），在每个节点上运行一次确定性求解器，然后利用这些解来重构整个随机解。

具体来说，为了计算解 $u(x, \boldsymbol{\xi})$ 的PCE系数 $a_{\alpha}(x)$，我们可以使用两种主要技术 [@problem_id:2686979]：
1.  **[谱投影](@entry_id:265201)法**：利用数值积分（求积）来近似计算投影积分 $a_{\alpha}(x) = \mathbb{E}[u(x, \theta) \Psi_{\alpha}(\boldsymbol{\xi})]$。为此，我们在随机空间中构建一个求积法则，由一组求积节点 $\lbrace \boldsymbol{\xi}^{(n)} \rbrace$ 和相应的权重 $\lbrace w^{(n)} \rbrace$ 组成。系数的计算公式为：
    $$
    a_{\alpha}(x) \approx \frac{1}{\mathbb{E}[\Psi_{\alpha}^2]} \sum_{n=1}^{N_{\text{quad}}} u(x, \boldsymbol{\xi}^{(n)}) \Psi_{\alpha}(\boldsymbol{\xi}^{(n)}) w^{(n)}
    $$
    为了使这个[数值积分](@entry_id:136578)对于PCE（截断到总阶数 $p$）是精确的，[求积法则](@entry_id:753909)必须能精确地积分最高达到 $2p$ 阶的多项式。对于基于[高斯求积](@entry_id:146011)的[张量积法则](@entry_id:177156)，如果每个维度使用 $q$ 个点，则需要满足 $2q-1 \ge 2p$，即 $q \ge p+1$。

2.  **插值法**：在[配置点](@entry_id:169000)集 $\lbrace \boldsymbol{\xi}^{(n)} \rbrace_{n=1}^N$ 上，我们强制PCE近似等于确定性求解器的输出：
    $$
    \sum_{\alpha \in \mathcal{A}_p} a_{\alpha}(x) \Psi_{\alpha}(\boldsymbol{\xi}^{(n)}) = u(x, \boldsymbol{\xi}^{(n)}), \quad \text{for } n=1, \dots, N
    $$
    这构成了一个关于未知系数 $a_{\alpha}(x)$ 的[线性方程组](@entry_id:148943) $V \boldsymbol{a} = \boldsymbol{u}$，其中 $V$ 是由在[配置点](@entry_id:169000)处求值的[基函数](@entry_id:170178)构成的范德蒙德式矩阵。如果[配置点](@entry_id:169000)的数量 $N$ 等于未知系数的数量 $S$，并且矩阵 $V$ 可逆，则可以得到唯一解。如果 $N  S$，则通常通过最小二乘法求解。

非侵入式方法的最大优点是它们不需要修改现有的、经过充分验证的确定性有限元代码。此外，由于在每个[配置点](@entry_id:169000)上的求解都是完全独立的，因此该方法具有**高度并行性**（embarrassingly parallel），非常适合在现代多核或[分布式计算](@entry_id:264044)环境上实现。

#### 方法比较：侵入式 vs. 非侵入式

选择侵入式SGM还是非侵入式[配置法](@entry_id:142690)取决于问题的具体特性和可用的计算资源。下表总结了它们的关键区别 [@problem_id:2686895]：

| 特性 | [侵入式随机伽辽金法](@entry_id:750793) (SGM) | 非侵入式[配置法](@entry_id:142690) |
| :--- | :--- | :--- |
| **实现复杂度** | **高** (侵入式)。需要深度修改FE代码以组装和求解大型耦合系统。 | **低** (非侵入式)。将确定性求解器作为黑箱，只需编写外部驱动脚本。 |
| **并行性** | **有限**。主要瓶颈是求解一个大型耦合线性系统，需要复杂的并行代数求解器和[预条件子](@entry_id:753679)。 | **极高** (易于并行)。每个[配置点](@entry_id:169000)的求解完全独立，可以轻松分配给不同处理器。 |
| **[误差控制](@entry_id:169753)** | **数学上严谨**。作为[伽辽金法](@entry_id:749698)，它在能量范数下提供最优解，有坚实的先验和[后验误差估计](@entry_id:167288)理论。 | **基于插值/求积理论**。误差依赖于解在[参数空间](@entry_id:178581)中的光滑程度。 |
| **效率** | 对于**低维** ($m$ 较小)、随机依赖性为**仿射**的线性问题非常高效。 | 对于**高维**问题（特别是结合[稀疏网格](@entry_id:139655)技术时）、必须使用**遗留代码**或**黑箱**求解器时，以及问题具有**非仿射**或**[非线性](@entry_id:637147)**依赖时，通常更具优势。 |

总之，SGM以其数学上的优雅和最优性著称，但在实现和计算上要求苛刻，特别是在高维情况下。非侵入式[配置法](@entry_id:142690)则以其灵活性、易于实现和卓越的并行性而受到青睐，使其成为许多实际工程应用中更具吸[引力](@entry_id:175476)的选择。