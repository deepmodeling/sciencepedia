## 引言
带漂移和波动性的布朗运动，或称[算术布朗运动](@entry_id:198508)，是[随机过程](@entry_id:159502)理论的基石之一。它通过在标准布朗运动的基础上增加一个确定性趋势（漂移）和一个波动尺度，为模拟现实世界中广泛存在的、兼具确定性增长和随机波动的现象提供了一个既简洁又强大的数学框架。从股票价格的波动到微观粒子的运动，再到[生物种群](@entry_id:200266)的演化，这一模型无处不在，使其成为理论研究和实际应用之间的重要桥梁。然而，要真正驾驭这一工具，仅理解其定义是远远不够的。学习者常常面临一个挑战：如何将抽象的数学原理与具体的应用场景联系起来，并掌握解决实际问题的分析技术。本文旨在填补这一鸿沟，系统性地引导读者从基础理论深入到跨学科应用，并最终通过实践来巩固所学知识。

为实现这一目标，本文分为三个循序渐进的章节。第一章“原理与机制”将深入剖析该过程的数学构造，包括其统计特性、路径行为以及伊藤公式和[吉尔萨诺夫定理](@entry_id:147068)等核心分析工具。第二章“应用与跨学科联系”将展示这些理论如何在金融、生态学和统计推断等不同领域中发挥作用，揭示其作为通用建模语言的强大能力。最后，第三章“动手实践”提供了一系列精心设计的问题，旨在通过解决具体问题来加深理解和提升分析技能。通过本次学习，读者将能够建立起一个关于带漂移和波动性的布朗运动的完整知识体系，并有能力将其应用于解决复杂的现实问题。

## 原理与机制

在理解了带有漂移和波动性的布朗运动的基本概念之后，本章将深入探讨其数学构造、核心性质以及分析该过程所必需的关键工具。我们将从其精确的数学定义出发，系统地推导其统计特性，探索其路径行为，并介绍一些在现代[随机分析](@entry_id:188809)中至关重要的高等技术，如[无穷小生成元](@entry_id:270424)和[测度变换](@entry_id:157887)。

### 定义与基本性质

我们考虑的[随机过程](@entry_id:159502)，即带有**漂移**（drift）和**波动性**（volatility）的布朗运动，通常也称为**[算术布朗运动](@entry_id:198508)**（Arithmetic Brownian Motion），是[标准布朗运动](@entry_id:197332)最直接和最重要的推广之一。

在一个满足通常条件的带滤[概率空间](@entry_id:201477) $(\Omega, \mathcal{F}, (\mathcal{F}_t)_{t \ge 0}, \mathbb{P})$ 上，给定一个标准布朗运动 $(W_t)_{t \ge 0}$，一个带有常数漂移 $\mu \in \mathbb{R}$ 和常数波动率 $\sigma > 0$、从 $x_0 \in \mathbb{R}$ 出发的布朗运动 $(X_t)_{t \ge 0}$ 定义为：
$$
X_t = x_0 + \mu t + \sigma W_t
$$
这个过程也可以等价地视为以下随机微分方程（SDE）的唯一[强解](@entry_id:198344)：
$$
dX_t = \mu \, dt + \sigma \, dW_t, \quad X_0 = x_0
$$
其中，$dt$ 项捕捉了过程的确定性趋势（漂移），而 $dW_t$ 项则代表了其随机波动。

#### 矩与[分布](@entry_id:182848)

过程的基本统计特性直接源于其定义以及[标准布朗运动](@entry_id:197332)的性质。

首先，我们计算其在任意时刻 $t \ge 0$ 的**期望**和**[方差](@entry_id:200758)**。利用期望算子的线性性质以及[标准布朗运动](@entry_id:197332) $\mathbb{E}[W_t] = 0$ 的事实，我们得到：
$$
\mathbb{E}[X_t] = \mathbb{E}[x_0 + \mu t + \sigma W_t] = x_0 + \mu t + \sigma \mathbb{E}[W_t] = x_0 + \mu t
$$
这个结果 [@problem_id:2970479] 直观地表明，过程的[期望值](@entry_id:153208)沿着一条由初始点 $x_0$ 和漂移率 $\mu$ 决定的直线演化。漂移项 $\mu t$ 是唯一影响过程均值的项。

接下来，我们计算其[方差](@entry_id:200758)。由于 $x_0 + \mu t$ 是一个确定性项，它不影响[方差](@entry_id:200758)。利用[方差的性质](@entry_id:185416) $\mathrm{Var}(aY+b) = a^2 \mathrm{Var}(Y)$以及 $\mathrm{Var}(W_t) = t$，我们有：
$$
\mathrm{Var}(X_t) = \mathrm{Var}(x_0 + \mu t + \sigma W_t) = \mathrm{Var}(\sigma W_t) = \sigma^2 \mathrm{Var}(W_t) = \sigma^2 t
$$
这表明过程的[方差](@entry_id:200758)随时间线性增长，其增长速率由波动率的平方 $\sigma^2$ 决定 [@problem_id:2970479]。波动率 $\sigma$ 控制着过程随机性的大小。

过程的二阶性质还包括协[方差](@entry_id:200758)。对于 $0 \le s \le t$，其**协[方差](@entry_id:200758)**函数为：
$$
\mathrm{Cov}(X_s, X_t) = \mathbb{E}[(X_s - \mathbb{E}[X_s])(X_t - \mathbb{E}[X_t])] = \mathbb{E}[(\sigma W_s)(\sigma W_t)] = \sigma^2 \mathbb{E}[W_s W_t]
$$
由于标准布朗运动的协[方差](@entry_id:200758)为 $\mathbb{E}[W_s W_t] = \min(s,t)$，我们得到：
$$
\mathrm{Cov}(X_s, X_t) = \sigma^2 \min(s,t)
$$
值得注意的是，漂移项 $\mu$ 对协[方差](@entry_id:200758)没有贡献。这意味着过程的协[方差](@entry_id:200758)结构与一个经 $\sigma$ 缩放的标准布朗运动完全相同 [@problem_id:2970483]。

#### 增量性质

对于任意 $0 \le s  t$，过程 $X_t$ 的增量为：
$$
X_t - X_s = (\mu t + \sigma W_t) - (\mu s + \sigma W_s) = \mu(t-s) + \sigma(W_t - W_s)
$$
由于标准布朗运动的增量 $W_t - W_s$ 服从正态分布 $\mathcal{N}(0, t-s)$，并且独立于 $\mathcal{F}_s$，因此 $X_t$ 的增量 $X_t - X_s$ 也服从正态分布。其均值为 $\mu(t-s)$，[方差](@entry_id:200758)为 $\sigma^2(t-s)$。即：
$$
X_t - X_s \sim \mathcal{N}(\mu(t-s), \sigma^2(t-s))
$$
由于该[分布](@entry_id:182848)仅依赖于时间差 $t-s$，所以 $X_t$ 的增量是**平稳的**（stationary）。此外，由于[标准布朗运动](@entry_id:197332)具有[独立增量](@entry_id:262163)，对于任意不重叠的时间区间，$X_t$ 的增量也是**独立的**（independent）[@problem_id:2970483]。

#### [分布](@entry_id:182848)的完整刻画：矩生成函数

由于 $X_t$ 是对高斯过程 $W_t$ 的仿射变换，它本身也是一个[高斯过程](@entry_id:182192)。在任意固定时刻 $t$，$X_t$ 是一个高斯[随机变量](@entry_id:195330)。我们可以通过计算其**矩生成函数**（Moment Generating Function, MGF）来完整地刻画其[分布](@entry_id:182848)。
$$
M_{X_t}(u) = \mathbb{E}[\exp(u X_t)] = \mathbb{E}[\exp(u(x_0 + \mu t + \sigma W_t))]
$$
利用指数函数的性质和[期望的线性](@entry_id:273513)，我们可以分离出确定性部分：
$$
M_{X_t}(u) = \exp(u(x_0 + \mu t)) \mathbb{E}[\exp(u \sigma W_t)]
$$
其中 $\mathbb{E}[\exp(u \sigma W_t)]$ 是[标准布朗运动](@entry_id:197332) $W_t$ 的矩生成函数在点 $u\sigma$ 处的值。由于 $W_t \sim \mathcal{N}(0, t)$，其矩生成函数为 $M_{W_t}(k) = \mathbb{E}[\exp(k W_t)] = \exp\left(\frac{1}{2}k^2 t\right)$。因此，
$$
\mathbb{E}[\exp(u \sigma W_t)] = M_{W_t}(u\sigma) = \exp\left(\frac{1}{2}(u \sigma)^2 t\right) = \exp\left(\frac{1}{2} u^2 \sigma^2 t\right)
$$
将此结果代回，我们得到 $X_t$ 的 MGF [@problem_id:2970458]：
$$
M_{X_t}(u) = \exp\left(u(x_0 + \mu t) + \frac{1}{2} u^2 \sigma^2 t\right)
$$
这正是均值为 $x_0 + \mu t$、[方差](@entry_id:200758)为 $\sigma^2 t$ 的[正态分布](@entry_id:154414)[随机变量](@entry_id:195330)的 MGF。

#### [鞅性质](@entry_id:261270)

一个过程是否为鞅，取决于其[条件期望](@entry_id:159140)。对于 $s  t$，我们计算 $\mathbb{E}[X_t | \mathcal{F}_s]$：
$$
\mathbb{E}[X_t | \mathcal{F}_s] = \mathbb{E}[x_0 + \mu t + \sigma W_t | \mathcal{F}_s] = \mathbb{E}[X_s + \mu(t-s) + \sigma(W_t - W_s) | \mathcal{F}_s]
$$
由于 $X_s$ 是 $\mathcal{F}_s$-可测的，而增量 $W_t - W_s$ 独立于 $\mathcal{F}_s$ 且均值为0，我们得到：
$$
\mathbb{E}[X_t | \mathcal{F}_s] = X_s + \mu(t-s)
$$
根据[鞅](@entry_id:267779)的定义，一个过程是[鞅](@entry_id:267779)当且仅当 $\mathbb{E}[X_t | \mathcal{F}_s] = X_s$。这要求 $\mu(t-s) = 0$，由于 $t>s$，此条件成立的充要条件是 $\mu = 0$。因此，带有漂移和波动性的布朗运动 $X_t$ 是一个**鞅当且仅当其漂移项为零** [@problem_id:2970483]。当 $\mu \neq 0$ 时，$X_t$ 是一个**[半鞅](@entry_id:184490)**（semimartingale）。特别地，过程 $M_t = X_t - \mu t = x_0 + \sigma W_t$ 是一个鞅，它被称为 $X_t$ 的**补偿过程**（compensated process）。

### 路径性质与[伊藤积分](@entry_id:272774)

除了统计特性，过程的路径行为也至关重要，这在[随机分析](@entry_id:188809)中通过二次变差和伊藤公式来描述。

#### 二次变差

**二次变差**（Quadratic Variation）是随机微积分区别于经典微积分的核心概念。对于一个[连续半鞅](@entry_id:636909) $Y_t$，其在 $[0, t]$ 上的二次变差 $[Y]_t$ 定义为沿时间分割的增量平方和的极限。对于我们的过程 $X_t = x_0 + \mu t + \sigma W_t$，我们可以将其分解为一个有限变差部分 $A_t = x_0 + \mu t$ 和一个[鞅](@entry_id:267779)部分 $M_t = \sigma W_t$。
二次变差的一个关键性质是，任何连续的[有限变差过程](@entry_id:635841)（如 $A_t$）的二次变差为零。这意味着确定性的漂移项对二次变差没有贡献。因此，$X_t$ 的二次变差完全由其[鞅](@entry_id:267779)部分决定：
$$
[X]_t = [x_0 + \mu t + \sigma W_t]_t = [\sigma W_t]_t = \sigma^2 [W]_t
$$
由于[标准布朗运动](@entry_id:197332)的二次变差是 $[W]_t = t$，我们最终得到 [@problem_id:2970460]：
$$
[X]_t = \sigma^2 t
$$
这个结果表明，尽管过程的期望路径是平滑的直线，但其样本路径的“能量”或“变异性”以速率 $\sigma^2$ 随时间累积。

#### [协变差](@entry_id:634097)

类似地，我们可以计算 $X_t$ 与其底层的标准布朗运动 $W_t$ 之间的**协变差**（Covariation）。[协变差](@entry_id:634097) $[Y, Z]_t$ 衡量了两个过程的随机部分如何协同变化。
$$
[X, W]_t = [x_0 + \mu t + \sigma W_t, W_t]_t
$$
利用协变差的[双线性](@entry_id:146819)和[有限变差过程](@entry_id:635841)与任何[连续半鞅](@entry_id:636909)的协变差为零的性质，我们有：
$$
[X, W]_t = [x_0 + \mu t, W]_t + [\sigma W_t, W_t]_t = 0 + \sigma [W, W]_t = \sigma [W]_t = \sigma t
$$
这个结果 [@problem_id:2970460] 量化了 $X_t$ 的随机波动与 $W_t$ 的随机波动之间的关联程度。

#### [伊藤公式](@entry_id:159684)

**伊藤公式**（Itô's Formula）是[随机微积分](@entry_id:143864)的基石，它描述了应用于[随机过程](@entry_id:159502)的函数的动态演化。对于一个二次连续可微的函数 $f \in C^2(\mathbb{R})$ 和过程 $X_t$，伊藤公式给出 $f(X_t)$ 的[微分形式](@entry_id:146747)：
$$
df(X_t) = f'(X_t) dX_t + \frac{1}{2} f''(X_t) d[X]_t
$$
将 $dX_t = \mu dt + \sigma dW_t$ 和 $d[X]_t = \sigma^2 dt$ 代入，我们得到 $f(X_t)$ 的 SDE [@problem_id:2970457]：
$$
df(X_t) = f'(X_t)(\mu dt + \sigma dW_t) + \frac{1}{2} f''(X_t) (\sigma^2 dt)
$$
整理 $dt$ 和 $dW_t$ 项，可得：
$$
df(X_t) = \left(\mu f'(X_t) + \frac{1}{2} \sigma^2 f''(X_t)\right) dt + \sigma f'(X_t) dW_t
$$
这个公式揭示了一个深刻的事实：函数 $f(X_t)$ 的漂移项不仅包含由 $X_t$ 的漂移传递而来的 $\mu f'(X_t)$，还包含一个额外的项 $\frac{1}{2} \sigma^2 f''(X_t)$。这一项是由于 $X_t$ 的非零二次变差产生的，是[随机微积分](@entry_id:143864)独有的特征，它源于 $(dW_t)^2 \sim dt$ 的[启发式](@entry_id:261307)规则。

### 高等分析工具

为了更深入地分析过程 $X_t$ 的行为，我们需要引入一些更强大的数学工具，包括无穷小生成元和[吉尔萨诺夫定理](@entry_id:147068)。

#### 无穷小生成元

对于一个[马尔可夫过程](@entry_id:160396)，其**无穷小生成元**（Infinitesimal Generator）是一个描述过程在“无穷小”时间步长内期望变化的算子。对于过程 $X_t$，其生成元 $\mathcal{L}$ 作用于一个足够光滑的函数 $f$ 上，定义为：
$$
\mathcal{L}f(x) = \lim_{t \downarrow 0} \frac{\mathbb{E}_x[f(X_t)] - f(x)}{t}
$$
其中 $\mathbb{E}_x[\cdot]$ 表示从 $X_0 = x$ 出发的期望。我们可以利用伊藤公式来推导 $\mathcal{L}$ 的具体形式。对伊藤公式 $f(X_t) - f(X_0) = \int_0^t (\dots) ds + \int_0^t (\dots) dW_s$ 两边取条件期望 $\mathbb{E}_x$，注意到[伊藤积分](@entry_id:272774)项的期望为零，得到：
$$
\mathbb{E}_x[f(X_t)] - f(x) = \mathbb{E}_x\left[\int_0^t \left(\mu f'(X_s) + \frac{1}{2} \sigma^2 f''(X_s)\right) ds\right]
$$
两边除以 $t$ 并取 $t \downarrow 0$ 的极限，根据[积分中值定理](@entry_id:159120)和被积[函数的连续性](@entry_id:193744)，我们得到 [@problem_id:2970510]：
$$
\mathcal{L}f(x) = \mu f'(x) + \frac{1}{2} \sigma^2 f''(x)
$$
这个二阶[微分算子](@entry_id:140145) $\mathcal{L}$ 完整地编码了过程的局部动态。生成元在连接[随机过程](@entry_id:159502)理论与[偏微分方程](@entry_id:141332)（如 Kolmogorov 方程和 Feynman-Kac 公式）中扮演着核心角色。其定义域 $D(\mathcal{L})$ 通常是 $C_0(\mathbb{R})$（在无穷远处消失的[连续函数空间](@entry_id:150395)）中使得 $\mathcal{L}f$ 也属于 $C_0(\mathbb{R})$ 的 $C^2$ 函数的[闭包](@entry_id:148169)，而 $C_c^\infty(\mathbb{R})$（[紧支集](@entry_id:276214)上的[无穷可微函数](@entry_id:267124)）是其一个核心（core）[@problem_id:2970510]。

#### [测度变换](@entry_id:157887)：[吉尔萨诺夫定理](@entry_id:147068)

**[吉尔萨诺夫定理](@entry_id:147068)**（Girsanov's Theorem）是[随机分析](@entry_id:188809)中最强大的工具之一，它允许我们通过改变底层的概率测度来改变[随机过程](@entry_id:159502)的漂移项，而不改变其波动结构。

考虑一个在[概率测度](@entry_id:190821) $\mathbb{P}$ 下的[标准布朗运动](@entry_id:197332) $W_t$。我们可以定义一个新的[概率测度](@entry_id:190821) $\mathbb{Q}$，它与 $\mathbb{P}$ 等价（即它们具有相同的[零测集](@entry_id:157694)），使得在 $\mathbb{Q}$ 下，另一个过程 $\tilde{W}_t$ 成为[标准布朗运动](@entry_id:197332)。这一变换通过一个称为**雷顿-尼科迪姆导数**（Radon-Nikodym derivative）的[随机过程](@entry_id:159502) $Z_t$ 来实现，该过程本身是一个 $\mathbb{P}$-[鞅](@entry_id:267779)。

对于常数漂移变换，这个过程 $Z_t$ 具有一个特别简洁的形式，即**[随机指数](@entry_id:197698)**（stochastic exponential）或 Doléans-Dade 指数。例如，要将一个 $\mathbb{P}$-布朗运动 $W_t$ 变换为一个带有漂移 $-\theta$ 的过程，即我们希望过程 $\tilde{W}_t = W_t + \theta t$ 在新测度 $\mathbb{Q}$ 下成为[标准布朗运动](@entry_id:197332)，我们应选择 Girsanov 核（kernel）为 $\gamma_s = -\theta$。对应的密度过程为 [@problem_id:2970474]：
$$
Z_t = \exp\left( \int_0^t (-\theta) dW_s - \frac{1}{2} \int_0^t (-\theta)^2 ds \right) = \exp\left(-\theta W_t - \frac{1}{2}\theta^2 t\right)
$$
只要 **Novikov 条件** $\mathbb{E}_\mathbb{P}[\exp(\frac{1}{2}\int_0^T \gamma_s^2 ds)]  \infty$ 满足（对于常数核，此条件总是成立），$Z_t$ 就是一个真鞅，且 $\mathbb{E}[Z_T]=1$。我们便可定义 $d\mathbb{Q} = Z_T d\mathbb{P}$。

这个定理的一个关键应用是“消除”漂移。对于我们的过程 $X_t = x_0 + \mu t + \sigma W_t$，我们希望找到一个测度 $\mathbb{Q}$，使得在该测度下 $X_t$ 没有漂移。这意味着我们需要找到一个 $\mathbb{Q}$-布朗运动 $\tilde{W}_t$ 使得 $X_t = x_0 + \sigma \tilde{W}_t$。
通过代数替换，我们发现 $x_0 + \mu t + \sigma W_t = x_0 + \sigma \tilde{W}_t$，这意味着 $\tilde{W}_t = W_t + \frac{\mu}{\sigma} t$。根据[吉尔萨诺夫定理](@entry_id:147068)，要使这个过程成为 $\mathbb{Q}$-布朗运动，我们需要的 Girsanov 核是 $\gamma_t = -\frac{\mu}{\sigma}$。因此，相应的雷顿-尼科迪姆导数为 [@problem_id:2970502]：
$$
\frac{d\mathbb{Q}}{d\mathbb{P}}\bigg|_{\mathcal{F}_T} = Z_T = \exp\left(-\frac{\mu}{\sigma} W_T - \frac{1}{2}\left(\frac{\mu}{\sigma}\right)^2 T\right)
$$
在这个新的测度 $\mathbb{Q}$ 下，原过程 $X_t$ 的 SDE 变为 $dX_t = \sigma d\tilde{W}_t$，其漂移项被成功消除。这个技术在[金融数学](@entry_id:143286)中用于从“真实世界”测度转换到“风险中性”测度，是[衍生品定价](@entry_id:144008)理论的基石。

### 多维推广

上述概念可以自然地推广到 $d$ 维空间。一个 $d$ 维带漂移和波动性的布朗运动 $X_t \in \mathbb{R}^d$ 定义为：
$$
X_t = x_0 + \mu t + \Sigma W_t
$$
其中 $x_0, \mu \in \mathbb{R}^d$ 是初始向量和漂移向量，$\Sigma \in \mathbb{R}^{d \times d}$ 是一个常数**波动率矩阵**，$W_t$ 是一个 $d$ 维标准布朗运动（其分量是相互独立的[标准布朗运动](@entry_id:197332)）。

该过程的关键性质如下 [@problem_id:2970466]：
- **[分布](@entry_id:182848)**：在时刻 $t$，$X_t$ 是一个多维[高斯随机向量](@entry_id:635820)，其均值为 $x_0 + \mu t$，[协方差矩阵](@entry_id:139155)为 $t \Sigma \Sigma^{\top}$。注意矩阵乘法的顺序至关重要，通常 $\Sigma \Sigma^{\top} \neq \Sigma^{\top} \Sigma$。
- **[无穷小生成元](@entry_id:270424)**：对于 $f \in C^2(\mathbb{R}^d)$，生成元 $\mathcal{L}$ 作用为：
  $$
  \mathcal{L}f(x) = \mu \cdot \nabla f(x) + \frac{1}{2} \sum_{i,j=1}^d (\Sigma \Sigma^{\top})_{ij} \frac{\partial^2 f}{\partial x_i \partial x_j}(x)
  $$
- **非退化性**：过程被认为是**非退化的**（non-degenerate），如果它在所有方向上都表现出随机性。这在数学上等价于要求[扩散矩阵](@entry_id:182965) $a = \Sigma \Sigma^{\top}$ 是正定的。这又等价于要求波动率矩阵 $\Sigma$ 是可逆的。
- **分量相关性**：$X_t$ 的各个分量 $X_t^{(i)}$ 是否不相关，取决于协方差矩阵 $\text{Cov}(X_t) = t \Sigma \Sigma^{\top}$ 是否为[对角矩阵](@entry_id:637782)。一个常见的误解是，这要求 $\Sigma$ 本身是对角矩阵。然而，这是不正确的。例如，如果 $\Sigma$ 是一个非对角的正交矩阵，那么 $\Sigma \Sigma^{\top} = I$ 是[对角矩阵](@entry_id:637782)，但 $\Sigma$ 不是。因此，分量不相关仅要求 $\Sigma \Sigma^{\top}$ 是对角的。

### 过程的边界行为

当我们将[扩散过程](@entry_id:170696)的定义域限制在一个区间上时，例如 $(a, b)$，过程在到达边界点 $a$ 或 $b$ 时的行为需要特别关注。Feller 的边界[分类理论](@entry_id:153976)为此提供了系统的框架。

对于[一维扩散](@entry_id:181320)过程，其[边界点](@entry_id:176493)可以分为四类：**正则**（regular）、**出口**（exit）、**入口**（entrance）或**自然**（natural）。分类依赖于两个关键量：**标度函数**（scale function）$s(x)$ 和**速度测度**（speed measure）$m(dx)$。对于过程 $X_t = x_0 + \mu t + \sigma W_t$，其标度函[数密度](@entry_id:268986)为 $s'(x) = \exp(-\frac{2\mu}{\sigma^2}x)$，速度测度密度为 $m(x) = \frac{2}{\sigma^2} \exp(\frac{2\mu}{\sigma^2}x)$。

分类是通过检查这两个密度函数在[边界点](@entry_id:176493)附近的积分是否收敛来进行的。对于一个有限区间 $(a,b)$，我们需要考察积分 $\int_a^c s'(x) dx$ 和 $\int_a^c m(x) dx$ 对左边界 $a$ 的敛散性，以及 $\int_c^b s'(x) dx$ 和 $\int_c^b m(x) dx$ 对右边界 $b$ 的敛散性（其中 $c$ 是 $(a,b)$ 内的任意一点）。

- **正则边界**：两个积分都收敛。
- **[出口边界](@entry_id:186494)**：标度函数[积分收敛](@entry_id:139742)，速度测度积分发散。
- **[入口边界](@entry_id:187498)**：标度函数积分发散，速度测度[积分收敛](@entry_id:139742)。
- **自然边界**：两个积分都发散。

对于我们的过程，由于漂移 $\mu$ 和波动率 $\sigma$ 都是常数，标度函数和速度测度的密度都是[指数函数](@entry_id:161417)。指数函数在任何有限[闭区间](@entry_id:136474)上都是连续且有界的。因此，对于任意有限的 $a$ 和 $b$，上述所有积分都是对一个[连续函数](@entry_id:137361)在有限区间上的定积分，其结果必然是有限的。

这意味着，对于在任意**有限区间** $(a, b)$ 上定义的带常数漂移和波动率的布朗运动，其两个边界点 $a$ 和 $b$ **总是正则边界** [@problem_id:2970506]。这与过程在半无限或无限区间上的行为形成鲜明对比，后者的边界分类通常会依赖于漂移项 $\mu$ 的符号。正则边界的直观含义是，过程可以从区间内部以正概率到达该边界，并且一旦到达，也可以立即返回区间内部。