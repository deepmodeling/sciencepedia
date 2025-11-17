## 引言
在科学与工程计算中，传统的确定性模型往往假设所有物理参数、载荷和几何形状都是精确已知的。然而，在现实世界中，从材料属性的微观变异到外部环境的随机波动，不确定性无处不在。忽略这些不确定性可能导致对系统行为的预测产生严重偏差，甚至引发灾难性设计失效。[随机有限元](@entry_id:755461)方法 (Stochastic Finite Element Methods, SFEM) 应运而生，它将[有限元分析](@entry_id:138109)的强大功能与概率论和统计学相结合，为系统地量化和传播模型中的不确定性提供了严谨的计算框架，是现代[不确定性量化](@entry_id:138597) (UQ) 领域的核心支柱。

本文旨在全面介绍[随机有限元](@entry_id:755461)方法。我们将从不确定性的数学表示出发，解决如何将物理世界中的随机性转化为计算机可以处理的数学对象这一根本问题。通过本文的学习，读者将系统地掌握SFEM的完整知识体系。在“原理与机制”一章中，我们将深入探讨[随机场](@entry_id:177952)的数学表示、Karhunen-Loève[降维技术](@entry_id:169164)以及[广义多项式混沌](@entry_id:749788)展开，并对比分析侵入式与非侵入式两大类求解策略。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示SFEM如何解决复杂的多物理场耦合、非线性系统、[结构动力学](@entry_id:172684)以及几何不确定性等前沿问题，并揭示其与[全局敏感性分析](@entry_id:171355)、可靠性评估和[模型校准](@entry_id:146456)等领域的深刻联系。最后，“动手实践”部分将提供具体的编程练习，帮助读者将理论知识转化为实践能力。

让我们首先进入第一章，系统地建立描述、离散化和求解包含随机参数的物理问题的数学框架。

## 原理与机制

本章旨在深入探讨[随机有限元](@entry_id:755461)方法 (Stochastic Finite Element Methods, SFEM) 的核心原理与机制。在之前的章节中，我们已经了解了在工程与科学问题中考虑不确定性的重要性。现在，我们将系统地建立一个数学框架，用以描述、离散化和求解包含随机参数的[偏微分方程](@entry_id:141332) (PDEs)。我们将从不确定性的基本数学表示出发，逐步过渡到随机场的[降维技术](@entry_id:169164)、解的随机性表达方式，并最终阐述求解[随机偏微分方程](@entry_id:188292)的两种主要方法学：侵入式与非侵入式方法。

### 不确定性的数学表示：[随机场](@entry_id:177952)

在物理系统中，许多材料属性或外部载荷并非确定不变的，而是在空间上呈现出不确定性的变化。例如，[复合材料](@entry_id:139856)的[弹性模量](@entry_id:198862)或[地下水](@entry_id:201480)流中的渗透率都可能因微观结构或地质构造的异质性而成为一个随空间位置变化的随机量。为了对这类不确定性进行严谨的[数学建模](@entry_id:262517)，我们引入**随机场 (random field)** 的概念。

从数学上讲，给定一个[概率空间](@entry_id:201477) $(\Omega, \mathcal{F}, \mathbb{P})$ 和一个物理域 $D \subset \mathbb{R}^d$，一个[随机场](@entry_id:177952) $E(x, \theta)$ 是一个由空间坐标 $x \in D$ 索引的[随机变量](@entry_id:195330)族。这里，$\theta \in \Omega$ 代表随机事件。我们可以从以下几个层面来理解这个定义 [@problem_id:2687009]：

1.  **[随机变量](@entry_id:195330) (Random Variable)**：对于物理域 $D$ 中任意一个固定的点 $x_0$，函数 $\theta \mapsto E(x_0, \theta)$ 是一个从[样本空间](@entry_id:275301) $\Omega$ 到实数域 $\mathbb{R}$ 的可测映射。这便是一个**[随机变量](@entry_id:195330)**，它描述了在特定位置 $x_0$ 处物理量（如[弹性模量](@entry_id:198862)）的不确定性。

2.  **[随机过程](@entry_id:159502) (Stochastic Process)**：[随机过程](@entry_id:159502)是一族由某个参数集索引的[随机变量](@entry_id:195330)。[随机场](@entry_id:177952)是[随机过程](@entry_id:159502)的一个特例，其特殊之处在于索引集是多维的，通常是 $\mathbb{R}^d$ 的一个[子集](@entry_id:261956)，代表空间位置。因此，认为[随机过程](@entry_id:159502)仅限于一维参数（如时间）的看法是不正确的。

3.  **样本路径 (Sample Path)**：对于[概率空间](@entry_id:201477)中的一个特定实现（即一个固定的 $\theta_0 \in \Omega$），映射 $x \mapsto E(x, \theta_0)$ 定义了一个在物理域 $D$ 上的确定性函数。这个函数被称为随机场的一个**样本路径**或**实现**。在实际应用中，我们通过数值方法求解的，正是这些样本路径。

一个关键的理论问题是样本路径的正则性，例如连续性。我们自然希望物理量的实现是连续的，而不是在空间中任意[振荡](@entry_id:267781)或跳跃。然而，[随机场](@entry_id:177952)的**均方连续性** (mean-square continuity)，即 $\lim_{y \to x} \mathbb{E}[(E(y, \theta) - E(x, \theta))^2] = 0$，并不足以保证样本路径的连续性。为了获得几乎必然（almost surely）连续的样本路径，需要更强的条件。**Kolmogorov-Chentsov [连续性定理](@entry_id:262016)**为此提供了重要的理论依据。该定理指出，如果存在正常数 $p > 0$, $\eta > 0$ 和 $C  \infty$，使得对于域中所有的 $x, y \in D$，随机场的增量矩满足
$$
\mathbb{E}\big[\,|E(x,\theta)-E(y,\theta)|^{p}\,\big] \le C \,\|x-y\|^{d+\eta}
$$
那么该[随机场](@entry_id:177952)存在一个修正版本，其样本路径几乎必然是 Hölder 连续的，从而也是连续的 [@problem_id:2687009]。这一条件将[随机场](@entry_id:177952)增量的统计特性与其样本路径的光滑性直接联系起来。

### 随机场的降维：Karhunen-Loève 展开

[随机场](@entry_id:177952)是无限维的随机对象，因为它在域 $D$ 的每个点上都定义了一个[随机变量](@entry_id:195330)。为了在计算机上进行数值处理，必须将其表示为有限数量的[随机变量](@entry_id:195330)。**Karhunen-Loève (KL) 展开** (或称主成分分析) 为此提供了一种最优的[降维](@entry_id:142982)方法。

KL 展开将一个零均值、二阶[随机场](@entry_id:177952) $a(x, \omega)$（即 $\mathbb{E}[a(x,\omega)]=0$ 且 $\mathbb{E}[a(x,\omega)^2]  \infty$）表示为一系列确定性空间函数与不相关[随机变量的乘积](@entry_id:266496)之和。其核心在于对随机场的**协[方差](@entry_id:200758)算子 (covariance operator)** 进行谱分解 [@problem_id:2600438]。

给定随机场 $a(x, \omega)$，其[协方差函数](@entry_id:265031)定义为 $C(x, x') := \mathbb{E}[a(x, \omega) a(x', \omega)]$。这是一个对称、非负定的函数。与之相关的[积分算子](@entry_id:262332) $\mathcal{K}: L^2(D) \to L^2(D)$ 定义为：
$$
(\mathcal{K}\phi)(x) := \int_D C(x, x') \phi(x') \,\mathrm{d}x'
$$
根据[紧自伴算子](@entry_id:147701)的谱理论，该算子存在一列非负[特征值](@entry_id:154894) $\{\lambda_n\}_{n \ge 1}$ 和一族对应的在 $L^2(D)$ 中标准正交的特征函数 $\{\phi_n(x)\}_{n \ge 1}$，它们满足以下[特征值问题](@entry_id:142153)：
$$
\int_D C(x, x') \phi_n(x') \,\mathrm{d}x' = \lambda_n \phi_n(x)
$$
基于这组[特征基](@entry_id:151409)，[随机场](@entry_id:177952) $a(x, \omega)$ 可以展开为如下级数形式：
$$
a(x, \omega) = \sum_{n=1}^\infty \sqrt{\lambda_n} \xi_n(\omega) \phi_n(x)
$$
其中，$\{\xi_n(\omega)\}_{n \ge 1}$ 是一组满足 $\mathbb{E}[\xi_n] = 0$ 和 $\mathbb{E}[\xi_m \xi_n] = \delta_{mn}$ 的标准正交[随机变量](@entry_id:195330)。$\delta_{mn}$ 是克罗内克符号。这意味着 KL 展开将复杂的空间相关[随机场](@entry_id:177952)分解为一组不相关的“基本”[随机变量](@entry_id:195330) $\xi_n$ 和与之对应的确定性空间“模式” $\phi_n(x)$。[特征值](@entry_id:154894) $\lambda_n$ 的大小度量了相应模式对随机场总[方差](@entry_id:200758)的贡献。

另一种等价的表示形式是 [@problem_id:2600438]：
$$
a(x, \omega) = \sum_{n=1}^\infty \eta_n(\omega) \phi_n(x)
$$
其中随机系数 $\eta_n(\omega) = \int_D a(x, \omega) \phi_n(x) \mathrm{d}x$ 是不相关的，但不是[标准化](@entry_id:637219)的，它们满足 $\mathbb{E}[\eta_n] = 0$ 和 $\mathbb{E}[\eta_m \eta_n] = \lambda_n \delta_{mn}$。

KL 展开的“最优性”体现在，对于任意给定的截断项数 $N$，它在所有线性展开中能够最小化均方截断误差。在实践中，我们通常选取最大的 $N$ 个[特征值](@entry_id:154894)对应的项来近似原始[随机场](@entry_id:177952)，从而实现从无限维到有限维的有效[降维](@entry_id:142982)。

### 解的随机性表示：[多项式混沌展开](@entry_id:162793)

通过 KL 展开等方法，我们将输入的不确定性（如材料属性）[参数化](@entry_id:272587)为一组[随机变量](@entry_id:195330) $\boldsymbol{\xi}(\theta) = (\xi_1(\theta), \dots, \xi_m(\theta))$。随机 PDE 的解 $u(x, \theta)$ 也将依赖于这些[随机变量](@entry_id:195330)。**[广义多项式混沌](@entry_id:749788)展开 (Generalized Polynomial Chaos, gPC)** 提供了一种强大而高效的方式来表示解对这些[随机变量](@entry_id:195330)的依赖关系。

假设解 $u(x, \theta)$ 对于固定的 $x$ 是一个平方可积的[随机变量](@entry_id:195330)，即 $u(x, \cdot) \in L^2(\Omega)$。gPC 的核心思想是将其在 $L^2(\Omega)$ 空间中展开为一组与输入[随机变量](@entry_id:195330) $\boldsymbol{\xi}$ 的[概率分布](@entry_id:146404)相匹配的标准[正交多项式](@entry_id:146918)基 $\{\Psi_{\alpha}(\boldsymbol{\xi})\}_{\alpha \in \mathbb{N}_0^m}$ [@problem_id:2686986]：
$$
u(x, \theta) = \sum_{\alpha \in \mathbb{N}_0^m} u_{\alpha}(x) \Psi_{\alpha}(\boldsymbol{\xi}(\theta))
$$
这里的 $\alpha$ 是一个多重指标，$\{\Psi_{\alpha}\}$ 是满足以下[正交关系](@entry_id:145540)的多项式基：
$$
\mathbb{E}[\Psi_{\alpha}(\boldsymbol{\xi}) \Psi_{\beta}(\boldsymbol{\xi})] = \int_{\Gamma} \Psi_{\alpha}(\boldsymbol{y}) \Psi_{\beta}(\boldsymbol{y}) \rho(\boldsymbol{y}) \mathrm{d}\boldsymbol{y} = \delta_{\alpha\beta}
$$
其中 $\rho(\boldsymbol{y})$ 是随机向量 $\boldsymbol{\xi}$ 的[联合概率密度函数](@entry_id:267139) (PDF)。由于基是标准正交的，展开系数 $u_{\alpha}(x)$ 可以通过投影得到，它们是确定性的空间函数：
$$
u_{\alpha}(x) = \mathbb{E}[u(x, \theta) \Psi_{\alpha}(\boldsymbol{\xi}(\theta))]
$$
gPC 的一个精髓在于 **Wiener-Askey 框架**，它为不同类型的[概率分布](@entry_id:146404)指定了最优的多项式基族，使得多项式的权重函数与[随机变量](@entry_id:195330)的 PDF 相匹配。这种匹配保证了展开级数的快速收敛。常见的对应关系包括 [@problem_id:2686986] [@problem_id:2600479]：
-   **高斯 (Gaussian)** [分布](@entry_id:182848) $\rightarrow$ **Hermite** 多项式
-   **均匀 (Uniform)** [分布](@entry_id:182848) $\rightarrow$ **Legendre** 多项式
-   **伽马 (Gamma)** [分布](@entry_id:182848) $\rightarrow$ **广义 Laguerre** 多项式
-   **贝塔 (Beta)** [分布](@entry_id:182848) $\rightarrow$ **Jacobi** 多项式

当输入[随机变量](@entry_id:195330) $\xi_1, \dots, \xi_m$ 相互独立时，多维正交基可以通过一维正交基的[张量积](@entry_id:140694)构造，即 $\Psi_{\alpha}(\boldsymbol{\xi}) = \prod_{i=1}^m \psi_{i, \alpha_i}(\xi_i)$ [@problem_id:2686986]。如果变量是相关的，则必须构造关于其联合概率测度的[正交多项式](@entry_id:146918)，例如通过 Gram-Schmidt [正交化](@entry_id:149208)。

在实际计算中，我们必须截断这个无限级数。一种常见的策略是采用**总阶数截断**，即保留所有总阶数 $|\alpha| = \sum_i \alpha_i$ 不超过某个预设值 $p$ 的多项式。对于 $s$ 个[随机变量](@entry_id:195330)和总阶数 $p$，[基函数](@entry_id:170178)的总数 $P(p, s)$ 为：
$$
P(p,s) = \binom{p+s}{s} = \frac{(p+s)!}{p!s!}
$$
这个数量会随着变量数 $s$ 和阶数 $p$ 的增加而急剧增长，这种现象被称为**维数灾难 (curse of dimensionality)** [@problem_id:2600483]。例如，对于 $s=10$ 和 $p=4$，就需要 $1001$ 个[基函数](@entry_id:170178)，这使得基于总阶数截断的 gPC 方法在处理高维随机问题时面临巨大挑战。

### 求解随机问题：方法论框架

在建立了表示不确定性输入和解的数学工具后，我们现在转向求解随机 PDE。首先，我们需要确定解所在的恰当函数空间。

#### [泛函分析](@entry_id:146220)基础：Bochner 空间

随机 PDE 的解 $u(\omega)$ 对每个随机事件 $\omega \in \Omega$ 都是一个函数，比如属于 Sobolev 空间 $V = H_0^1(D)$。因此，解本身是一个以函数为值的[随机变量](@entry_id:195330)。描述这类对象的正确数学框架是 **Bochner 空间** $L^2(\Omega; V)$ [@problem_id:2600514]。该空间包含所有从 $\Omega$ 到 $V$ 的**强可测 (strongly measurable)** 函数 $u$，且其范数的平方是可积的，即 $\mathbb{E}[\|u(\omega)\|_V^2]  \infty$。

强可测性是一个拓扑概念，它要求函数可以被一列[简单函数](@entry_id:137521)（在 $V$ 的范数下）[几乎处处](@entry_id:146631)逼近。对于[可分希尔伯特空间](@entry_id:271477)（如 $H_0^1(D)$），根据 **Pettis 定理**，强[可测性](@entry_id:199191)等价于**弱[可测性](@entry_id:199191)**，即对于 $V$ 中任意固定的 $\varphi$，标量函数 $\omega \mapsto (u(\omega), \varphi)_V$ 是可测的。这个等价性在理论分析中极为有用。

Bochner 空间 $L^2(\Omega; V)$ 本身也是一个[希尔伯特空间](@entry_id:261193)，其[内积](@entry_id:158127)定义为 $\mathbb{E}[(u(\omega), v(\omega))_V]$。这个完备的[内积空间](@entry_id:271570)结构是伽辽金方法等变分方法的基石，它允许我们定义随机[能量范数](@entry_id:274966)、建立正交性，并通过 Fubini-Tonelli 定理严谨地交换期望和空间积分的次序 [@problem_id:2600514]。在适当的条件下（例如，随机系数可测且随机载荷项属于 $L^2(\Omega; V^*)$），可以证明随机[椭圆问题](@entry_id:146817)的解确实属于 $L^2(\Omega; V)$ [@problem_id:2600514]。

#### 侵入式方法：[随机伽辽金法](@entry_id:178148)

**侵入式 (intrusive)** 方法的特点是需要推导并求解一组新的、与原始确定性 PDE 不同的耦合[方程组](@entry_id:193238)。**随机伽辽金 (Stochastic Galerkin, SG)** 方法是其典型代表。

考虑一个随机[椭圆问题](@entry_id:146817)：
$$
-\nabla \cdot (a(x, \boldsymbol{\xi}(\omega)) \nabla u(x, \omega)) = f(x)
$$
其路径形式的[弱形式](@entry_id:142897)为：对几乎所有 $\omega$，求 $u(\cdot, \omega) \in V$ 使得对所有 $v \in V$ 成立
$$
\int_D a(x, \boldsymbol{\xi}) \nabla u(x, \boldsymbol{\xi}) \cdot \nabla v(x) \, \mathrm{d}x = \int_D f(x) v(x) \, \mathrm{d}x
$$
SG 方法直接在 Bochner 空间 $H_0^1(D) \otimes L^2_\rho(\Gamma)$ 中寻求近似解。我们将解 $u$ 和测试函数 $v$ 都用 gPC 级数展开，并选择一个有限维的[张量积](@entry_id:140694)试验空间 $W_{h,p} = V_h \otimes S_p$，其中 $V_h$ 是一个标准的有限元空间，而 $S_p$ 是一个截断的[多项式混沌](@entry_id:196964)空间 [@problem_id:2600499]。

[伽辽金法](@entry_id:749698)的要求是，残差与试验空间中的所有函数正交。这等价于对路径[弱形式](@entry_id:142897)在整个[概率空间](@entry_id:201477)上取期望。因此，SG 的[变分问题](@entry_id:756445)是：求 $u_{h,p} \in W_{h,p}$ 使得对所有 $v \in W_{h,p}$ 成立：
$$
\mathbb{E}\left[\int_D a(x, \boldsymbol{\xi}) \nabla u_{h,p}(x, \boldsymbol{\xi}) \cdot \nabla v(x, \boldsymbol{\xi}) \, \mathrm{d}x\right] = \mathbb{E}\left[\int_D f(x) v(x, \boldsymbol{\xi}) \, \mathrm{d}x\right]
$$
这等价于用概率密度函数 $\rho(\boldsymbol{y})$ 作为权重在[参数空间](@entry_id:178581) $\Gamma$ 上积分 [@problem_id:2600499]：
$$
\int_{\Gamma}\int_{D} a(x,\boldsymbol{y})\,\nabla u_{h,p}(x,\boldsymbol{y})\cdot \nabla v(x,\boldsymbol{y}) \, \mathrm{d}x \; \rho(\boldsymbol{y})\,\mathrm{d}\boldsymbol{y} = \int_{\Gamma}\int_{D} f(x)\, v(x,\boldsymbol{y}) \, \mathrm{d}x \; \rho(\boldsymbol{y})\,\mathrm{d}\boldsymbol{y}
$$
将 $u_{h,p}$ 和 $v$ 的 gPC 展开式代入，并选择测试函数为每个[基函数](@entry_id:170178)，最终会得到一个针对所有确定性系数 $u_\alpha(x)$ 的大型耦合[线性系统](@entry_id:147850)。这个系统的规模大约是 $(N_s \times P(p,s)) \times (N_s \times P(p,s))$，其中 $N_s$ 是空间自由度数量。尽管该系统通常是稀疏、[对称正定](@entry_id:145886)的，但其耦合结构和巨大规模使得实现复杂且计算成本高昂 [@problem_id:2600518]。

#### 非侵入式方法：采样与配置

与侵入式方法相反，**非侵入式 (non-intrusive)** 方法将现有的确定性求解器视为一个“黑箱”，通过多次调用它来收集信息并重构统计量或随机解。

最简单的非侵入式方法是**[蒙特卡洛](@entry_id:144354) ([Monte Carlo](@entry_id:144354), MC) 方法**。为了估计某个目标量（如解的某个[线性泛函](@entry_id:276136)）的期望 $\mu = \mathbb{E}[Q(u)]$，MC 方法生成 $N$ 个独立的随机参数样本 $\{\boldsymbol{\xi}_i\}_{i=1}^N$，对每个样本求解确定性 PDE 得到解 $u(\boldsymbol{\xi}_i)$，然后计算样本均值：
$$
\widehat{Q}_{N,h} := \frac{1}{N} \sum_{i=1}^N Q(u_h(\boldsymbol{\xi}_i))
$$
其中 $u_h$ 是[有限元近似](@entry_id:166278)解。根据中心极限定理，该估计量的[均方根误差](@entry_id:170440)（即统计[采样误差](@entry_id:182646)）的[收敛速度](@entry_id:636873)为 $O(N^{-1/2})$ [@problem_id:2600445]。这个收敛速度与随机问题的维度 $s$ 无关，这是 MC 方法在高维问题中的一个巨大优势。然而，其[收敛速度](@entry_id:636873)较慢，为了获得高精度需要大量的样本。

总误差由两部分组成：有限元离散带来的**偏倚 (bias)**，其大小为 $O(h^p)$；以及 MC 采样带来的**[方差](@entry_id:200758)**，其大小为 $O(N^{-1})$。为了有效控制总误差，必须平衡这两个误差源。通常，需要选择样本量 $N$ 使得[采样误差](@entry_id:182646)与离散误差同阶，即 $N \approx C h^{-2p}$ [@problem_id:2600445]。

**随机配置 (Stochastic Collocation, SC)** 是另一种更先进的非侵入式方法。它并非[随机采样](@entry_id:175193)，而是在[参数空间](@entry_id:178581)中选择一组精心设计的“[配置点](@entry_id:169000)”（通常是[稀疏网格](@entry_id:139655)上的求积节点）。在每个[配置点](@entry_id:169000)上求解确定性 PDE，然后使用这些解来构造一个全局的（例如，[多项式插值](@entry_id:145762)）代理模型。对于解对参数依赖性光滑的问题，SC 方法可以实现比 MC 快得多的收敛速度 [@problem_id:2600518]。SC 方法的主要优点是实现简单、易于[并行化](@entry_id:753104)，且无需修改现有代码。

### 收敛性与效率分析

不同 SFEM 方法的效率取决于其收敛特性。

对于 gPC 类方法（如 SG 和 SC），其收敛速度与解对随机参数的**正则性 (regularity)** 密切相关。一个重要的理论结果是，如果随机 PDE 的系数对参数是仿射依赖的（例如 $a(x, \boldsymbol{\xi}) = a_0(x) + \sum \xi_j a_j(x)$），并且在参数域的一个复数邻域内保持[一致椭圆性](@entry_id:194714)，那么解映射 $\boldsymbol{\xi} \mapsto u(\cdot, \boldsymbol{\xi})$ 在该邻域内是**解析 (analytic)** 的 [@problem_id:2600470]。这种[解析性](@entry_id:140716)保证了 gPC 系数 $u_\alpha$ 会指数衰减。因此，gPC 展开的截断误差会以**谱收敛 (spectral convergence)** 的速度下降，即误差随多项式阶数 $p$ 的增加呈指数衰减，快于任何代数[收敛速度](@entry_id:636873) $O(p^{-k})$。这种快速收敛是 gPC 方法在低维问题中极为高效的根本原因 [@problem_id:2600470] [@problem_id:2600518]。值得注意的是，谱收敛的根本原因是解的解析性，而非算子依赖关系的仿射性本身；任何保证了[解析性](@entry_id:140716)的非仿射依赖关系同样能带来谱收敛 [@problem_id:2600470]。

总结一下各种方法的优劣：
-   **[随机伽辽金法](@entry_id:178148) (SG)**：侵入式。通过[伽辽金投影](@entry_id:145611)在[能量范数](@entry_id:274966)下获得准最优解，对于给定自由度通常精度最高。但实现复杂，计算和内存成本高，受[维数灾难](@entry_id:143920)影响严重 [@problem_id:2600518]。
-   **[蒙特卡洛](@entry_id:144354)法 (MC)**：非侵入式。实现简单，完全并行，且[收敛速度](@entry_id:636873)与维度无关，适用于高维或不光滑问题。但[收敛速度](@entry_id:636873)慢 ($O(N^{-1/2})$)，通常不适合追求高精度。
-   **[随机配置法](@entry_id:174778) (SC)**：非侵入式。实现简单，易于并行。对于解光滑的低维问题，通过[稀疏网格](@entry_id:139655)等技术可以实现接近谱收敛的速度，效率远高于 MC。其精度通常略低于同等自由度的 SG 方法，但实现成本和灵活性优势明显 [@problem_id:2600518]。

选择哪种方法取决于问题的具体特性，包括随机维度、解的正则性、所需精度以及可用的计算资源和开发时间。