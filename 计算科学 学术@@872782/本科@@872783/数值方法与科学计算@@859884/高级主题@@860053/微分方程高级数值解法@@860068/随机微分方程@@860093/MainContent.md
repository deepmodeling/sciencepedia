## 引言
从行星的[轨道](@entry_id:137151)到[化学反应](@entry_id:146973)的速率，许多自然和工程系统传统上都通过常微分方程 (ODE) 进行描述，这些模型假定未来是完全由当前状态决定的。然而，现实世界充满了不确定性：金融市场的价格波动、神经元的随机放电、微观粒子在液体中的无规则运动。这些现象的共同点是它们都受到内在随机性的深刻影响，这使得确定性模型无法完全捕捉其动态本质。[随机微分](@entry_id:194556)方程 (SDE) 正是为了填补这一知识空白而生，它提供了一套强大的数学语言来描述和分析这些随机演化的系统。

本文将带领您进入[随机动力学](@entry_id:187867)的世界，系统地介绍[随机微分](@entry_id:194556)方程的理论基础与实践应用。我们首先将在“原则与机理”一章中，建立一套全新的微积分规则——[伊藤微积分](@entry_id:266022)，以处理随机噪声的特殊性质，并深入剖析几何布朗运动和[奥恩斯坦-乌伦贝克过程](@entry_id:140047)等核心模型。接下来，在“应用与跨学科联系”一章中，我们将展示SDE如何在物理学、金融、生物学和工程学等不同领域中，为理解复杂随机现象提供深刻的见解。最后，通过“动手实践”部分，您将有机会将理论应用于具体问题，从而巩固所学知识。现在，让我们从构建随机微积分的基础开始，探索这些描述不确定世界的强大工具。

## 原则与机理

在本章中，我们将深入探讨[随机微分](@entry_id:194556)方程 (SDE) 的核心数学原理和内在机制。与依赖于平滑、可预测变化的常微分方程 (ODE) 不同，SDE 旨在描述那些本质上包含不确定性和随机波动的系统。为了掌握这些工具，我们必须建立一套新的微积分规则，理解其关键模型，并探索其解的统计特性。

### 从确定性到随机动态

许多科学模型始于对变化率的描述。一个经典的例子是生态学中的[种群增长模型](@entry_id:274310)。在最简单的情况下，马尔萨斯定律假设种群 $N(t)$ 的增长率与其当前规模成正比，可用[常微分方程](@entry_id:147024)表示：
$$
\frac{dN}{dt} = rN
$$
其中 $r$ 是恒定的净增长率。该模型的解是指数增长或衰减：$N(t) = N_0 \exp(rt)$。这是一个完全确定性的模型：给定初始种群 $N_0$，任何未来时刻的种群规模都是唯一确定的。

然而，真实世界的系统很少如此规律。环境因素，如资源可用性、温度波动或捕食者行为，都具有随机性。这些因素会影响增长率 $r$，使其不再是一个常数，而是在一个平均值附近随机波动。为了在模型中捕捉这种不确定性，我们可以将增长率分解为一个平均部分和一个随机波动部分。这引导我们进入[随机微分](@entry_id:194556)方程的领域。

一个通用的**[伊藤随机微分方程](@entry_id:637785) (Itô SDE)** 形式如下：
$$
dX_t = \mu(X_t, t)dt + \sigma(X_t, t)dW_t
$$
这个方程描述了[随机过程](@entry_id:159502) $X_t$ 的无穷小变化 $dX_t$。它由两部分构成：
1.  **漂移项 (Drift Term)**：$\mu(X_t, t)dt$。其中 $\mu(X_t, t)$ 称为**[漂移系数](@entry_id:199354)**，它代表了过程在时间 $dt$ 内的确定性、可预测的平均变化趋势。这类似于经典物理学中的速度或力。
2.  **[扩散](@entry_id:141445)项 (Diffusion Term)**：$\sigma(X_t, t)dW_t$。其中 $\sigma(X_t, t)$ 称为**[扩散](@entry_id:141445)系数**，它衡量随机波动的大小或强度。$dW_t$ 是**[维纳过程](@entry_id:137696)**（或布朗运动）的无穷小增量，是随机性的来源。维纳过程增量 $dW_t$ 可以被认为是服从均值为0、[方差](@entry_id:200758)为 $dt$ 的[正态分布](@entry_id:154414)的[随机变量](@entry_id:195330)，即 $dW_t \sim \mathcal{N}(0, dt)$。

以我们的种群模型为例，我们可以将随机性引入增长率，得到一个称为**[几何布朗运动](@entry_id:137398) (Geometric Brownian Motion, GBM)** 的模型 [@problem_id:1311581]。该模型在金融学中也常用于描述资产价格：
$$
dN_t = r N_t dt + \sigma N_t dW_t
$$
在这里，[漂移系数](@entry_id:199354)是 $\mu(N_t) = rN_t$，代表平均指数增长趋势。[扩散](@entry_id:141445)系数是 $\sigma(N_t) = \sigma N_t$，表明随机波动的幅度与当前种群规模成正比——种群越大，波动的绝对量也越大。参数 $r$ 是平均增长率，而 $\sigma$ 则代表环境的**波动性 (volatility)**。

### 噪声的特殊微积分：伊藤积分

处理 SDE 的一个核心挑战是，由[维纳过程](@entry_id:137696)驱动的路径 $W_t$ 极不规则。它在任何地方都是连续的，但又在任何地方都不可微。这种奇异的性质使得经典微积分的法则（如[链式法则](@entry_id:190743)）不再适用。为了理解为什么，我们需要引入**二次变差 (Quadratic Variation)** 的概念。

对于一个在 $[0, T]$ 区间内正常可微的函数 $f(t)$，如果我们将其分割成 $N$ 个小段，其二次变差定义为 $\sum_{i=1}^{N} (f(t_i) - f(t_{i-1}))^2$。根据[中值定理](@entry_id:141085)，$\Delta f_i = f(t_i) - f(t_{i-1}) = f'(c_i) \Delta t$。因此，二次变差约为 $\sum (f'(c_i))^2 (\Delta t)^2$。当 $\Delta t \to 0$ 时，这个和将趋向于零。

然而，[维纳过程](@entry_id:137696)则完全不同。考虑一个离散时间[随机游走](@entry_id:142620)，它在每个时间步长 $\Delta t$ 内的变化为 $\Delta P_i = \mu \Delta t + \sigma \sqrt{\Delta t} Z_i$，其中 $Z_i$ 是一个独立的[随机变量](@entry_id:195330)，取值为 $+1$ 或 $-1$ [@problem_id:1710328]。这个模型是 SDE 的离散近似。其一步变化的平方是：
$$
(\Delta P_i)^2 = (\mu \Delta t)^2 + 2\mu\sigma (\Delta t)^{3/2} Z_i + (\sigma \sqrt{\Delta t} Z_i)^2 = \mu^2 (\Delta t)^2 + 2\mu\sigma (\Delta t)^{3/2} Z_i + \sigma^2 \Delta t
$$
注意到 $Z_i^2 = 1$。在整个时间区间 $[0, T]$ 上的总二次变差是 $Q_N = \sum_{i=1}^{N} (\Delta P_i)^2$。当时间步数 $N \to \infty$（即 $\Delta t = T/N \to 0$）时：
-   第一项 $\sum \mu^2 (\Delta t)^2 = N \mu^2 (T/N)^2 = \mu^2 T^2/N \to 0$。
-   第二项由于 $Z_i$ 的随机性，其和的增长速度慢于 $N$，导致整个项也趋向于零。
-   第三项 $\sum \sigma^2 \Delta t = N \sigma^2 (T/N) = \sigma^2 T$。

因此，在[连续极限](@entry_id:162780)下，二次变差收敛到一个非零的确定性值 $\sigma^2 T$。这揭示了[伊藤积分](@entry_id:272774)的一个基本规则：维纳过程增量的平方在平均意义上不为零。我们可以[启发式](@entry_id:261307)地将其写为：
$$
(dW_t)^2 = dt
$$
此外，由于 $dt$ 是一个更高阶的无穷小量，我们有 $(dt)^2 = 0$ 和 $dt \cdot dW_t = 0$。这些“伊藤法则”是随机微积分的基石。

### 随机链式法则：[伊藤引理](@entry_id:138912)

在经典微积分中，[链式法则](@entry_id:190743)是求[复合函数](@entry_id:147347)导数的基本工具。在随机世界中，它的对应物是**[伊藤引理](@entry_id:138912) (Itô's Lemma)**。[伊藤引理](@entry_id:138912)告诉我们，如果一个[随机过程](@entry_id:159502) $X_t$ 遵循 SDE $dX_t = \mu dt + \sigma dW_t$，那么关于 $X_t$ 的任意二次[可微函数](@entry_id:144590) $f(X_t)$ 的动态是什么。

为了推导它，我们对 $f(X_t)$ 进行泰勒展开，并保留到二阶项（因为 $(dX_t)^2$ 不可忽略）：
$$
df(X_t) = f'(X_t) dX_t + \frac{1}{2} f''(X_t) (dX_t)^2 + \dots
$$
现在，我们使用伊藤法则来计算 $(dX_t)^2$：
$$
(dX_t)^2 = (\mu dt + \sigma dW_t)^2 = \mu^2 (dt)^2 + 2\mu\sigma dt dW_t + \sigma^2 (dW_t)^2 = \sigma^2 dt
$$
将 $dX_t$ 和 $(dX_t)^2$ 的表达式代入泰勒展开，我们得到[伊藤引理](@entry_id:138912)的完整形式：
$$
df(X_t) = \left( \mu f'(X_t) + \frac{1}{2}\sigma^2 f''(X_t) \right)dt + \sigma f'(X_t) dW_t
$$
这个公式的核心在于**[伊藤修正项](@entry_id:136428) (Itô correction term)** $\frac{1}{2}\sigma^2 f''(X_t)dt$。这个多出来的漂移项是由于过程的非零二次变差造成的，在普通微积分中没有对应物。

[伊藤引理](@entry_id:138912)是解决和分析 SDE 的最强大工具之一。让我们看两个经典应用：

**应用1：从[算术布朗运动](@entry_id:198508)推导[几何布朗运动](@entry_id:137398)**
假设一个过程 $X_t$ 遵循最简单的 SDE，即**[算术布朗运动](@entry_id:198508)** $dX_t = \mu dt + \sigma dW_t$，其中 $\mu$ 和 $\sigma$ 是常数。我们想知道过程 $Y_t = \exp(X_t)$ 遵循什么样的 SDE [@problem_id:1311610]。这里 $f(x) = \exp(x)$，所以 $f'(x) = \exp(x)$ 且 $f''(x) = \exp(x)$。应用[伊藤引理](@entry_id:138912)：
$$
dY_t = \left( \mu \exp(X_t) + \frac{1}{2}\sigma^2 \exp(X_t) \right)dt + \sigma \exp(X_t) dW_t
$$
代入 $Y_t = \exp(X_t)$，我们得到：
$$
dY_t = \left(\mu + \frac{1}{2}\sigma^2\right) Y_t dt + \sigma Y_t dW_t
$$
这是一个几何布朗运动。有趣的是，对数过程 $X_t$ 的漂移为 $\mu$，而其指数形式 $Y_t$ 的增长率漂移却是 $\mu + \frac{1}{2}\sigma^2$。这个额外的 $\frac{1}{2}\sigma^2$ 项就是[伊藤修正项](@entry_id:136428)的体现。

**应用2：求解[几何布朗运动](@entry_id:137398)**
反过来，我们可以利用[伊藤引理](@entry_id:138912)求解 GBM 方程 $dN_t = r N_t dt + \sigma N_t dW_t$ [@problem_id:1710365]。这里的技巧是寻找一个变换，将这个复杂的[乘性噪声](@entry_id:261463) SDE 变成一个简单的[加性噪声](@entry_id:194447) SDE。我们考虑 $X_t = \ln(N_t)$。这里 $f(n) = \ln(n)$，所以 $f'(n) = 1/n$，$f''(n) = -1/n^2$。漂移和扩散系数分别为 $\mu(N_t) = rN_t$ 和 $\sigma(N_t) = \sigma N_t$。应用[伊藤引理](@entry_id:138912)：
$$
dX_t = d(\ln N_t) = \left( (rN_t) \frac{1}{N_t} + \frac{1}{2}(\sigma N_t)^2 \left(-\frac{1}{N_t^2}\right) \right)dt + (\sigma N_t) \frac{1}{N_t} dW_t
$$
$$
dX_t = \left(r - \frac{1}{2}\sigma^2\right) dt + \sigma dW_t
$$
这个关于 $X_t$ 的 SDE 非常简单，其系数都是常数。我们可以直接从 $t=0$ 到 $t=T$ 进行积分：
$$
X_T - X_0 = \int_0^T \left(r - \frac{1}{2}\sigma^2\right) dt + \int_0^T \sigma dW_t
$$
$$
\ln(N_T) - \ln(N_0) = \left(r - \frac{1}{2}\sigma^2\right)T + \sigma W_T
$$
因此，我们得到了 GBM 的显式解：
$$
N_T = N_0 \exp\left( \left(r - \frac{1}{2}\sigma^2\right)T + \sigma W_T \right)
$$
这个解清晰地揭示了[随机过程](@entry_id:159502)的结构：它由一个确定性的指数趋势项和一个由维纳过程 $W_T$ 驱动的随机波动项组成。

### 重要的 SDE 模型及其解释

#### [几何布朗运动 (GBM)](@entry_id:270219)

如上所述，GBM 的 SDE 为 $dX_t = r X_t dt + \sigma X_t dW_t$。由于其解总是正的（如果 $X_0 > 0$），并且其波动与当前值成比例，它成为金融学中为股票价格建模和生态学中为[种群建模](@entry_id:267037)的标准模型。

利用其显式解，我们可以计算其[统计矩](@entry_id:268545)。例如，其[期望值](@entry_id:153208) $E[X_T]$ 为 [@problem_id:1311581]：
$$
E[X_T] = E\left[X_0 \exp\left( \left(r - \frac{1}{2}\sigma^2\right)T + \sigma W_T \right)\right] = X_0 \exp\left( \left(r - \frac{1}{2}\sigma^2\right)T \right) E[\exp(\sigma W_T)]
$$
由于 $W_T \sim \mathcal{N}(0, T)$，我们使用[正态分布的矩生成函数](@entry_id:262318)性质 $E[\exp(aZ)] = \exp(\frac{1}{2}a^2\text{Var}(Z))$，得到 $E[\exp(\sigma W_T)] = \exp(\frac{1}{2}\sigma^2 T)$。代入上式，我们发现：
$$
E[X_T] = X_0 \exp\left( \left(r - \frac{1}{2}\sigma^2\right)T \right) \exp\left(\frac{1}{2}\sigma^2 T\right) = X_0 \exp(rT)
$$
这表明，过程的[期望值](@entry_id:153208)与没有噪声的确定性模型 $dX/dt = rX$ 的解完全相同。然而，过程的典型路径行为可能与平均行为大相径庭。

考察[长期行为](@entry_id:192358) ($t \to \infty$)，我们看对数过程 $\frac{1}{t}\ln X_t = \frac{1}{t}\ln X_0 + (r - \frac{1}{2}\sigma^2) + \frac{W_t}{t}$。根据布朗运动的强大数定律，$\lim_{t\to\infty} W_t/t = 0$ 几乎必然成立。因此：
$$
\lim_{t\to\infty} \frac{1}{t}\ln X_t = r - \frac{1}{2}\sigma^2 \quad (\text{几乎必然})
$$
这个量的符号决定了 $X_t$ 的长期命运 [@problem_id:1710345]。
-   如果 $r - \frac{1}{2}\sigma^2  0$，那么 $\ln X_t \to -\infty$，这意味着 $X_t \to 0$。种群几乎必然灭绝。
-   如果 $r - \frac{1}{2}\sigma^2 > 0$，那么 $\ln X_t \to \infty$，这意味着 $X_t \to \infty$。

一个惊人的结论是：即使平均增长率 $r$ 为正（例如 $r=0.01, \sigma=0.2$），如果波动性 $\sigma$ 足够大以至于 $r - \frac{1}{2}\sigma^2  0$（例如 $0.01 - 0.5 \times 0.04 = -0.01  0$），那么虽然期望种群 $E[X_t]$ 会指数增长到无穷，但几乎每一条样本路径最终都会衰减到零！这是因为随机性产生的巨大向下波动（在对数尺度上）比向上波动更有可能导致灭绝。

#### 奥恩斯坦-乌伦贝克 (OU) 过程

另一个关键模型是**奥恩斯坦-乌伦贝克 (Ornstein-Uhlenbeck, OU) 过程**，它描述了**均值回归 (mean-reversion)** 现象。其 SDE 形式为 [@problem_id:1311586]：
$$
dX_t = \kappa(\theta - X_t)dt + \sigma dW_t
$$
这个模型广泛用于模拟利率、温度或粒子速度等趋向于某个平衡水平的物理量。各参数的解释如下：
-   $\theta$：**长期均值**或**平衡水平**。当 $X_t = \theta$ 时，漂移项为零，过程没有向任何特定方向漂移的趋势。
-   $\kappa$：**回归速率**。$\kappa > 0$。当 $X_t > \theta$ 时，漂移项为负，将过程[拉回](@entry_id:160816) $\theta$。当 $X_t  \theta$ 时，漂移项为正，将过程推向 $\theta$。$\kappa$ 的值越大，这种回归力就越强，过程回到均值附近的速度就越快。
-   $\sigma$：**波动率**。它衡量了随机噪声的强度，与 GBM 中的解释相同。

### 统计描述：福克-普朗克方程

SDE 描述了单个粒子或样本路径的演化。但如果我们想知道在时刻 $t$ 时，过程 $X_t$ 处于位置 $x$ 的概率密度 $p(x,t)$ 是如何随时间演化的，该怎么办？答案由一个称为**[福克-普朗克方程](@entry_id:140155) ([Fokker-Planck](@entry_id:635508) Equation)** 的[偏微分方程](@entry_id:141332)给出。

对于一维 SDE $dX_t = \mu(X_t)dt + \sigma(X_t)dW_t$，其对应的[福克-普朗克方程](@entry_id:140155)为：
$$
\frac{\partial p(x,t)}{\partial t} = -\frac{\partial}{\partial x}[\mu(x)p(x,t)] + \frac{1}{2}\frac{\partial^2}{\partial x^2}[\sigma^2(x)p(x,t)]
$$
这个方程是一个确定性的 PDE，它描述了[概率密度](@entry_id:175496)的守恒和流动。右边的第一项是由于漂移引起的[概率流](@entry_id:150949)动，第二项是由于[扩散](@entry_id:141445)引起的概率展宽。

在许多系统中，随着时间的推移，系统会达到一个[统计平衡](@entry_id:186577)状态，此时[概率分布](@entry_id:146404)不再随时间变化，即 $\frac{\partial p}{\partial t} = 0$。这个不随时间变化的[分布](@entry_id:182848) $p_{ss}(x)$ 称为**平稳分布 (stationary distribution)**。

**应用1：寻找[平稳分布](@entry_id:194199)**
对于平稳分布，福克-普朗克方程变为一个[常微分方程](@entry_id:147024)。我们可以通过引入**[概率流](@entry_id:150949) (probability current)** $J(x) = \mu(x)p_{ss}(x) - \frac{1}{2}\frac{\partial}{\partial x}[\sigma^2(x)p_{ss}(x)]$ 来求解它。对于在无穷远处有界或衰减的系统，平稳状态对应于零概率流条件 $J(x)=0$。

以 OU 过程为例 [@problem_id:1710383]，$\mu(x) = -\kappa x$ (为简化，设 $\theta=0$)，$\sigma(x) = \sigma$。零流条件给出：
$$
-\kappa x p_{ss}(x) - \frac{\sigma^2}{2} \frac{dp_{ss}(x)}{dx} = 0
$$
这是一个可分离变量的一阶 ODE，其解为：
$$
p_{ss}(x) = A \exp\left(-\frac{\kappa x^2}{\sigma^2}\right)
$$
通过归一化（$\int_{-\infty}^{\infty} p_{ss}(x) dx = 1$），可以确定常数 $A$，最终得到一个[高斯分布](@entry_id:154414)：
$$
p_{ss}(x) = \sqrt{\frac{\kappa}{\pi\sigma^2}} \exp\left(-\frac{\kappa x^2}{\sigma^2}\right)
$$
这表明，在[均值回归](@entry_id:164380)和随机噪声的共同作用下，系统最终的温度或位置将服从一个以[平衡点](@entry_id:272705)为中心的正态分布，其[方差](@entry_id:200758)为 $\sigma^2/(2\kappa)$。

**应用2：计算平稳矩**
有时我们不需要知道完整的平稳分布，而只想计算其某些矩（如均值、[方差](@entry_id:200758)）。一个强大的技巧是利用[平稳性](@entry_id:143776)的定义：在平稳状态下，任何关于 $X_t$ 的函数 $f(X_t)$ 的[期望值](@entry_id:153208)都是恒定的，即 $\frac{d}{dt}\langle f(X_t) \rangle_{ss} = 0$。

考虑一个被困在[势阱](@entry_id:151413)中的粒子，其 SDE 为 $dX_t = \frac{F(X_t)}{\gamma} dt + \sigma dW_t$，其中力 $F(x) = -kx - \lambda x^3$ [@problem_id:1311602]。我们想计算 $k \langle X^2 \rangle_{ss} + \lambda \langle X^4 \rangle_{ss}$。我们可以取 $f(X_t) = X_t^2$，应用[伊藤引理](@entry_id:138912)得到 $d(X_t^2)$，然后取期望：
$$
\frac{d}{dt}\langle X_t^2 \rangle_{ss} = \left\langle 2X_t \frac{F(X_t)}{\gamma} + \sigma^2 \right\rangle_{ss} = 0
$$
代入 $F(X_t)$ 的表达式：
$$
-\frac{2}{\gamma} \langle X_t(kX_t + \lambda X_t^3) \rangle_{ss} + \sigma^2 = 0
$$
$$
\frac{2}{\gamma} (k\langle X^2 \rangle_{ss} + \lambda\langle X^4 \rangle_{ss}) = \sigma^2
$$
整理得到 $k\langle X^2 \rangle_{ss} + \lambda\langle X^4 \rangle_{ss} = \frac{\gamma\sigma^2}{2}$。利用爱因斯坦关系 $\sigma^2 = 2k_B T / \gamma$，我们最终得到一个深刻的物理结果：$k\langle X^2 \rangle_{ss} + \lambda\langle X^4 \rangle_{ss} = k_B T$。这个结果直接将宏观可测量的[统计矩](@entry_id:268545)与系统的温度联系起来，而无需解出复杂的非高斯平稳分布。

### 高级主题与诠释

#### 伊藤积分 vs. [斯特拉托诺维奇积分](@entry_id:266086)

到目前为止，我们一直使用[伊藤积分](@entry_id:272774)的框架。然而，还有另一种定义随机积分的方式，称为**斯特拉托诺维奇 (Stratonovich) 积分**。两者的主要区别在于对积分中[扩散](@entry_id:141445)项 $\sigma(X_t)$ 的取值点不同。[伊藤积分](@entry_id:272774)使用区间的左端点，使其成为**非预期的 (non-anticipating)**，这在金融等应用中非常自然。[斯特拉托诺维奇积分](@entry_id:266086)使用区间的中点，这使得它遵循经典微积分的[链式法则](@entry_id:190743)。

一个斯特拉托诺维奇 SDE $dY_t = a(Y_t)dt + b(Y_t) \circ dW_t$（$\circ$ 表示[斯特拉托诺维奇积分](@entry_id:266086)）可以被转换为一个等价的伊藤 SDE。转换公式为：
$$
dY_t = \left(a(Y_t) + \frac{1}{2}b(Y_t) \frac{\partial b(Y_t)}{\partial y}\right) dt + b(Y_t) dW_t
$$
这个转换引入了一个额外的漂移项，有时被称为**虚假漂移 (spurious drift)**。例如，对于斯特拉托诺维奇方程 $dY_t = \sin(Y_t) \circ dW_t$ [@problem_id:1710370]，其等价的伊藤形式为：
$$
dY_t = \frac{1}{2}\sin(Y_t)\cos(Y_t) dt + \sin(Y_t) dW_t
$$
选择哪种积分取决于所建模型的物理背景。通常，如果 SDE 是一个物理过程在噪声关联时间趋于零时的极限，斯特拉托诺维奇形式更自然。而在金融和需要严格[鞅性质](@entry_id:261270)的领域，伊藤形式是标准选择。

#### [数值模拟](@entry_id:137087)与收敛性

解析解只适用于少数 SDE。在实践中，我们通常需要数值方法来模拟 SDE 的样本路径。最简单的[数值格式](@entry_id:752822)是**欧拉-丸山 (Euler-Maruyama) 法**，它是[常微分方程](@entry_id:147024)欧拉法的一个直接推广：
$$
X_{n+1} = X_n + \mu(X_n, t_n)\Delta t + \sigma(X_n, t_n) \Delta W_n
$$
其中 $\Delta W_n = W_{t_{n+1}} - W_{t_n}$ 是一个独立的随机增量，可以从正态分布 $\mathcal{N}(0, \Delta t)$ 中抽取，即 $\Delta W_n = \sqrt{\Delta t} Z_n$，其中 $Z_n \sim \mathcal{N}(0,1)$。

在评估数值方法的准确性时，需要区分两种收敛性：
1.  **强收敛 (Strong Convergence)**：衡量的是模拟路径与真实路径在逐点意义上的接近程度。其误差通常定义为 $E[|X_T - \hat{X}_T|]$，其中 $\hat{X}_T$ 是数值解。
2.  **弱收敛 (Weak Convergence)**：衡量的是模拟解的[统计矩](@entry_id:268545)（如期望、[方差](@entry_id:200758)）与真实解的[统计矩](@entry_id:268545)的接近程度。其误差通常定义为 $|E[f(X_T)] - E[f(\hat{X}_T)]|$。

对于[欧拉-丸山法](@entry_id:142440)，其强[收敛阶](@entry_id:146394)通常为 $O(\sqrt{\Delta t})$，而[弱收敛](@entry_id:146650)阶为 $O(\Delta t)$ [@problem_id:1710330]。这意味着，要获得一条精确的样本路径（强收敛），需要的计算量远大于获得精确的统计特性（弱收敛）。当我们的目标是计算期权价格（即一个[期望值](@entry_id:153208)）时，弱收敛就足够了；而当我们想模拟特定风险场景下的路径时，强收敛则更为重要。