## 引言
在随机微分方程（SDE）的数值分析领域，理解数值解如何逼近真实解是核心议题。通常，我们关注路径级别的误差，即强收敛性。然而，在金融工程、统计物理和贝叶斯计算等众多应用中，我们更关心的是解的统计特性，例如某个量的[期望值](@entry_id:153208)。在这种情境下，一种不同但同样关键的收敛性概念——**弱收敛性**——便凸显其重要性。它衡量的是数值解的[概率分布](@entry_id:146404)与真实解[分布](@entry_id:182848)的接近程度，直接关系到[蒙特卡洛模拟](@entry_id:193493)等方法的[计算效率](@entry_id:270255)和精度。

本文旨在全面而深入地探讨SDE[数值格式](@entry_id:752822)的[弱收敛](@entry_id:146650)性理论及其应用。许多从业者可能熟悉强收敛，但对弱收敛的原理、其阶数为何常常高于强[收敛阶](@entry_id:146394)，以及如何利用这一特性来优化计算，可能存在知识上的空白。

为了填补这一空白，本文将引导读者开启一段系统的学习之旅。在第一章**“原理与机制”**中，我们将从弱收敛性的严格定义出发，通过直接泰勒展开和基于倒向[Kolmogorov方程](@entry_id:270139)的对偶方法，揭示其阶数背后的数学机理。接着，在第二章**“应用与跨学科联系”**中，我们将展示这些理论如何在[蒙特卡洛](@entry_id:144354)[误差控制](@entry_id:169753)、[多层蒙特卡洛方法](@entry_id:752291)（MLMC）以及金融和物理学的专用格式设计中发挥关键作用。最后，第三章**“动手实践”**将提供一系列精心设计的练习，帮助您将理论知识转化为解决实际问题的能力。

通过本文的学习，您将建立起对弱收敛性完整而扎实的理解，并掌握在[随机建模](@entry_id:261612)与计算中有效运用它的方法。

## 原理与机制

在[随机微分方程](@entry_id:146618)（SDE）的数值分析中，我们关注[数值格式](@entry_id:752822)如何逼近真实解。这种逼近的质量可以通过不同的误差准则来衡量。虽然强收敛性关注单个样本路径的路径误差，但另一类同样重要的收敛性，即 **[弱收敛](@entry_id:146650)性**（weak convergence），关注的是数值解的统计分布对真实解[分布](@entry_id:182848)的逼近程度。在许多应用中，尤其是在金融工程和物理学中，我们通常关心的是解的某个函数的[期望值](@entry_id:153208)，例如期权价格或某个物理量的[统计矩](@entry_id:268545)。在这些场景下，[弱收敛](@entry_id:146650)性是更自然、更核心的概念。

本章将深入探讨[弱收敛](@entry_id:146650)性的原理和机制。我们将首先严格定义[弱收敛](@entry_id:146650)性及其阶数，并阐明其在蒙特卡洛模拟等实际应用中的重要性。接着，我们将以经典的欧拉-丸山（Euler-Maruyama）格式为例，通过两种核心分析方法——直接[泰勒展开](@entry_id:145057)和基于倒向[Kolmogorov方程](@entry_id:270139)的对偶方法——来揭示[弱收敛](@entry_id:146650)阶数的来源。最后，我们将讨论如何利用[伊藤-泰勒展开](@entry_id:139712)来设计高阶弱格式，并探讨[检验函数](@entry_id:166589)的[光滑性](@entry_id:634843)对收敛阶数的影响，从而为读者构建一个完整而严谨的理论框架。

### 弱收敛性的定义与意义

#### 强收敛性与[弱收敛](@entry_id:146650)性的对比

在深入弱收敛性之前，我们首先需要将其与强收敛性进行区分。考虑如下 $d$ 维[伊藤随机微分方程](@entry_id:637785)：
$$
\mathrm{d}X_t = a(X_t)\,\mathrm{d}t + b(X_t)\,\mathrm{d}W_t, \quad X_0 = x_0
$$
其中 $W_t$ 是一个 $m$ 维[标准布朗运动](@entry_id:197332)。设 $X_T^h$ 是该SDE在终端时刻 $T$ 的一个时间步长为 $h$ 的数值近似。

**强收敛性**（strong convergence）衡量的是数值[解路径](@entry_id:755046)与真实[解路径](@entry_id:755046)在路径意义下的接近程度。一个[数值格式](@entry_id:752822)被称为具有 $\gamma$ 阶强收敛性，如果存在一个常数 $C$（不依赖于 $h$），使得在某个 $L^r(\Omega)$ 范数下，终端时刻的路径误差满足：
$$
\left(\mathbb{E}\left[|X_T - X_T^h|^r\right]\right)^{1/r} \le C h^\gamma
$$
这里，我们关注的是可观测值 $X_T$ 本身，误差在路径差异的矩范数下进行评估。强收敛性对于需要模拟单条精确轨迹的应用至关重要。[@problem_id:3083314]

**弱收敛性**（weak convergence）则衡量数值解的[概率分布](@entry_id:146404)逼近真实解[概率分布](@entry_id:146404)的程度。由于一个[随机变量](@entry_id:195330)的[分布](@entry_id:182848)完全由其所有（足够好的）函数的[期望值](@entry_id:153208)所刻画，[弱收敛](@entry_id:146650)性是通过检验函数（test functions）来定义的。一个[数值格式](@entry_id:752822)被称为具有 $p$ 阶弱收敛性，如果对于某个足够广泛的光滑检验函数类 $\varphi$ 中的任意函数，都存在一个常数 $C_\varphi$（不依赖于 $h$），使得：
$$
\left|\mathbb{E}[\varphi(X_T)] - \mathbb{E}[\varphi(X_T^h)]\right| \le C_\varphi h^p
$$
这里，我们关注的可观测量是 $\varphi(X_T)$ 的期望，误差体现在[期望值](@entry_id:153208)的差异上。[@problem_id:3083314]

#### [弱收敛](@entry_id:146650)阶数的严格定义

弱收敛阶数的严格定义不仅依赖于误差界的形式，还对检验函数的光滑性提出了要求。理论上，要证明一个格式具有 $p$ 阶弱收敛性，通常需要[检验函数](@entry_id:166589) $\varphi$ 足够光滑。一个标准的函数类别是 $C_P^k(\mathbb{R}^d)$，它包含所有 $k$ 阶连续可微且其直到 $k$ 阶的导数都具有至多是[多项式增长](@entry_id:177086)的函数。严格来说，一个[数值格式](@entry_id:752822)具有 $p$ 阶[弱收敛](@entry_id:146650)性，是指对于所有属于 $C_P^{2(p+1)}(\mathbb{R}^d)$ 的检验函数 $\varphi$，都存在一个不依赖于 $h$ 的常数 $C_{\varphi,T}$，使得对于足够小的 $h$，下式成立：
$$
\left|\mathbb{E}[\varphi(X_T)] - \mathbb{E}[\varphi(X_T^h)]\right| \le C_{\varphi,T} h^p
$$
对[光滑性](@entry_id:634843)的要求（如此处的 $2(p+1)$ 阶导数）源于[弱误差分析](@entry_id:184494)中使用的泰勒展开。为了将局部[误差控制](@entry_id:169753)在 $O(h^{p+1})$，展开式中的余项需要被更高阶的导数所控制。[@problem_id:3083346]

#### 弱收敛性的实际应用：[蒙特卡洛模拟](@entry_id:193493)

弱收敛性的核心价值在[金融工程](@entry_id:136943)、计算物理和贝叶斯统计等领域的[蒙特卡洛](@entry_id:144354)（Monte Carlo）模拟中体现得淋漓尽致。在这些领域，我们通常需要计算形如 $\theta = \mathbb{E}[\varphi(X_T)]$ 的量，例如，欧式期权的价格就是其到期收益函数关于[风险中性测度](@entry_id:147013)下的期望。

我们无法直接计算 $\theta$，因此采用数值方法。一个典型的方法是：
1.  使用步长为 $h$ 的[数值格式](@entry_id:752822)（如[欧拉-丸山法](@entry_id:142440)）模拟出 $X_T$ 的近似值 $X_T^h$。
2.  通过模拟 $M$ 条独立的路径，得到 $M$ 个独立的 $X_T^h$ 的实现，记为 $X_T^{h,(i)}$。
3.  构造[蒙特卡洛估计](@entry_id:637986)量：
    $$
    \widehat{\theta}_{M,h} = \frac{1}{M}\sum_{i=1}^{M} \varphi(X_T^{h,(i)})
    $$

这个估计量的总均方误差（Mean Squared Error, MSE）可以分解为两部分：
$$
\mathbb{E}[(\widehat{\theta}_{M,h} - \theta)^2] = \underbrace{\left(\mathbb{E}[\widehat{\theta}_{M,h}] - \theta\right)^2}_{\text{平方离散化偏差}} + \underbrace{\mathrm{Var}(\widehat{\theta}_{M,h})}_{\text{统计方差}}
$$
其中，$\mathbb{E}[\widehat{\theta}_{M,h}] = \mathbb{E}[\varphi(X_T^h)]$。因此，平方离散化偏差正是弱收敛误差的平方：$(\mathbb{E}[\varphi(X_T^h)] - \mathbb{E}[\varphi(X_T)])^2$。如果格式的弱收敛阶为 $p$，则该偏差为 $O(h^{2p})$。而统计[方差](@entry_id:200758)则由中心极限定理控制，为 $\mathrm{Var}(\widehat{\theta}_{M,h}) = \frac{1}{M}\mathrm{Var}(\varphi(X_T^h)) = O(M^{-1})$。

因此，总误差由两部分组成：由时间步长 $h$ 控制的离散化偏差和由模拟路径数 $M$ 控制的[统计误差](@entry_id:755391)。为了有效地分配计算资源（总计算量大致与 $M \times (T/h)$ 成正比），我们需要平衡这两个误差源。[@problem_id:3083363]

一个经典的例子是 **欧拉-丸山（Euler-Maruyama, EM）格式**。对于给定的SDE，其更新法则为：
$$
X_{n+1}^h = X_n^h + a(X_n^h)h + b(X_n^h)\Delta W_n
$$
其中 $\Delta W_n = W_{t_{n+1}} - W_{t_n}$ 是独立的高斯增量，$\Delta W_n \sim \mathcal{N}(0, hI_m)$。在适当的[光滑性](@entry_id:634843)和增长条件下，EM格式的强收敛阶为 $\gamma = 1/2$，而弱收敛阶为 $p = 1$。[@problem_id:3083385] [@problem_id:3083363] 这意味着，在估计[期望值](@entry_id:153208)时，离散化偏差以 $O(h)$ 的速率减小，远快于路径误差 $O(h^{1/2})$ 的[收敛速度](@entry_id:636873)。这一事实凸显了弱收敛分析的独特价值：对于正确的任务，我们可以使用在强意义下收敛较慢的简单格式，并仍然获得很高的精度。

### 弱收敛性的分析方法

要证明一个[数值格式](@entry_id:752822)的[弱收敛](@entry_id:146650)阶，核心是分析其 **局部弱误差**（local weak error），即单步误差的期望。如果单步误差为 $O(h^{p+1})$，那么在 $[0, T]$ 区间上累积 $N=T/h$ 步，全局误差就将是 $N \times O(h^{p+1}) = O(h^p)$。本节介绍两种分析局部弱误差的主流方法。

#### 方法一：[矩匹配](@entry_id:144382)与直接泰勒展开

这种方法的核心思想是直接比较真实解 $\varphi(X_{t+h})$ 和数值解 $\varphi(Y_{t+h})$ 在一个时间步长内的条件期望，并通过泰勒展开来量化它们的差异。

我们以一个具体的例子来阐述这个过程。考虑一维几何布朗运动（在金融中用于建模股票价格）：
$$
dX_t = \alpha X_t dt + \sigma X_t dW_t
$$
为了简化计算，我们考虑一个更简单的模型——奥恩斯坦-乌伦贝克（Ornstein-Uhlenbeck）过程，其系数为线性或常数：
$$
dX_t = \alpha X_t dt + \sigma dW_t
$$
设检验函数为 $\varphi(x) = x^4$。我们的目标是计算局部弱误差的 $h^2$ 阶主项。[@problem_id:3083395]

**1. 精确解的期望展开**

对于光滑函数 $\varphi$，其条件期望 $\mathbb{E}[\varphi(X_{t+h}) | X_t = x]$ 可以通过SDE的 **无穷小生成元** (infinitesimal generator) $L$ 进行展开。该SDE的生成元为：
$$
L\psi(x) = a(x)\psi'(x) + \frac{1}{2}b(x)^2\psi''(x) = \alpha x \psi'(x) + \frac{1}{2}\sigma^2 \psi''(x)
$$
弱[泰勒展开](@entry_id:145057)（weak Taylor expansion）给出：
$$
\mathbb{E}[\varphi(X_{t+h}) | X_t = x] = \varphi(x) + h(L\varphi)(x) + \frac{h^2}{2}(L^2\varphi)(x) + O(h^3)
$$
其中 $L^2\varphi = L(L\varphi)$。对于 $\varphi(x)=x^4$，我们计算：
- $\varphi'(x) = 4x^3$, $\varphi''(x) = 12x^2$
- $L\varphi(x) = (\alpha x)(4x^3) + \frac{1}{2}\sigma^2(12x^2) = 4\alpha x^4 + 6\sigma^2 x^2$
- 经过进一步计算可得 $L^2\varphi(x) = 16\alpha^2 x^4 + 36\alpha\sigma^2 x^2 + 6\sigma^4$。

代入展开式，我们得到精确期望：
$$
\mathbb{E}[\varphi(X_{t+h}) | X_t = x] = x^4 + (4\alpha x^4 + 6\sigma^2 x^2)h + (8\alpha^2 x^4 + 18\alpha\sigma^2 x^2 + 3\sigma^4)h^2 + O(h^3)
$$

**2. 数值解的期望展开**

EM格式的单步迭代为 $\bar{X}_{t+h} = x + \alpha x h + \sigma \Delta W$，其中 $\Delta W \sim \mathcal{N}(0,h)$。我们需要计算 $\mathbb{E}[\varphi(\bar{X}_{t+h})] = \mathbb{E}[(x + \alpha x h + \sigma \Delta W)^4]$。利用高斯[随机变量的矩](@entry_id:174539)（$\mathbb{E}[\Delta W]=0, \mathbb{E}[(\Delta W)^2]=h, \mathbb{E}[(\Delta W)^3]=0, \mathbb{E}[(\Delta W)^4]=3h^2$），通过[二项式展开](@entry_id:269603)并保留至 $h^2$ 阶，可以得到：
$$
\mathbb{E}[\varphi(\bar{X}_{t+h})] = x^4 + (4\alpha x^4 + 6\sigma^2 x^2)h + (6\alpha^2 x^4 + 12\alpha\sigma^2 x^2 + 3\sigma^4)h^2 + O(h^3)
$$

**3. 局部弱误差**

将两者相减，可以看到 $h^0$ 和 $h^1$ 阶项完全抵消。这正是EM格式具有至少1阶[弱收敛](@entry_id:146650)性的原因。局部弱误差的主项由 $h^2$ 阶的系数差异决定：
$$
\text{Error} = \mathbb{E}[\varphi(X_{t+h})] - \mathbb{E}[\varphi(\bar{X}_{t+h})] = \left[ (8\alpha^2 x^4 + 18\alpha\sigma^2 x^2) - (6\alpha^2 x^4 + 12\alpha\sigma^2 x^2) \right]h^2 + O(h^3)
$$
$$
\text{Error} = (2\alpha^2 x^4 + 6\alpha\sigma^2 x^2)h^2 + O(h^3)
$$
这个 $O(h^2)$ 的局部[误差累积](@entry_id:137710)起来，就得到了 $O(h)$ 的全局弱误差。[@problem_id:3083395]

这个例子清晰地展示了，[弱误差分析](@entry_id:184494)本质上是 **[矩匹配](@entry_id:144382)**（moment matching）的过程。EM格式的增量矩与真实解的增量矩在低阶上是一致的，而[高阶矩](@entry_id:266936)的差异导致了[离散化误差](@entry_id:748522)。同时，这个计算也揭示了检验函数 $\varphi$ 的[光滑性](@entry_id:634843)是如何进入分析的：$\varphi$ 的各阶导数 $\varphi', \varphi'', \varphi'''$ 等作为系数出现在[泰勒展开](@entry_id:145057)中，因此需要它们存在且有界来保证余项的[可控性](@entry_id:148402)。[@problem_id:3083372]

#### 方法二：基于倒向[Kolmogorov方程](@entry_id:270139)的对偶方法

这是一种更抽象但通常更强大的分析技术。其出发点是著名的 **[费曼-卡茨公式](@entry_id:272429)**（Feynman-Kac formula），它在SDE的期望与一个[偏微分方程](@entry_id:141332)（PDE）的解之间建立了桥梁。

令 $u(t,x) = \mathbb{E}[\varphi(X_T) | X_t = x]$。[费曼-卡茨公式](@entry_id:272429)表明，在适当的[正则性条件](@entry_id:166962)下，$u(t,x)$ 是以下 **倒向[Kolmogorov方程](@entry_id:270139)**（backward Kolmogorov equation）的解：
$$
\frac{\partial u}{\partial t}(t,x) + L u(t,x) = 0, \quad \text{对于 } t \in [0,T)
$$
其终端条件为 $u(T,x) = \varphi(x)$。[@problem_id:3083351]

利用这个性质，我们可以将全局弱误差 $E_N = \mathbb{E}[\varphi(X_T)] - \mathbb{E}[\varphi(X_N^h)]$ 表示为一个伸缩求和（telescoping sum）：
$$
\begin{aligned}
E_N = u(0, x_0) - \mathbb{E}[u(T, X_N^h)] \\
= \mathbb{E}[u(t_0, X_0^h)] - \mathbb{E}[u(t_N, X_N^h)] \\
= \sum_{n=0}^{N-1} \left( \mathbb{E}[u(t_n, X_n^h)] - \mathbb{E}[u(t_{n+1}, X_{n+1}^h)] \right)
\end{aligned}
$$
现在，我们聚焦于求和中的单项，即局部误差余项。利用塔式期望法则，我们可以分析其[条件期望](@entry_id:159140)。令 $x=X_n^h$，我们对 $u(t_{n+1}, X_{n+1}^h)$ 在点 $(t_n, x)$ 进行[泰勒展开](@entry_id:145057)：
$$
\mathbb{E}[u(t_{n+1}, X_{n+1}^h) | X_n^h=x] = u(t_n,x) + h\frac{\partial u}{\partial t} + \mathbb{E}[\Delta X_h]\cdot \nabla u + \frac{1}{2}\mathbb{E}[\text{tr}(\Delta X_h (\Delta X_h)^\top \nabla^2 u)] + \dots
$$
其中 $\Delta X_h = X_{n+1}^h - x$ 是[数值格式](@entry_id:752822)的增量。对于EM格式，我们有 $\mathbb{E}[\Delta X_h] = a(x)h$ 和 $\mathbb{E}[\Delta X_h (\Delta X_h)^\top] = b(x)b(x)^\top h + O(h^2)$。将这些代入展开式，我们发现 $h$ 阶项恰好组合成：
$$
h\frac{\partial u}{\partial t}(t_n,x) + h \left(a(x)\cdot \nabla u(t_n,x) + \frac{1}{2}\text{tr}(b(x)b(x)^\top \nabla^2 u(t_n,x))\right) = h\left(\frac{\partial u}{\partial t} + L u\right)(t_n,x)
$$
由于 $u$ 求解倒向PDE，该项为零！这意味着 $O(h)$ 的项神奇地消失了，留下的局部误差余项为 $O(h^2)$。这个优雅的抵消是弱收敛分析的核心。[全局误差](@entry_id:147874)因此是 $N \times O(h^2) = O(h)$。[@problem_id:3083351]

这种方法的威力在于它将复杂的[随机分析](@entry_id:188809)问题转化为了[PDE解](@entry_id:166250)的正则性问题。要使上述[泰勒展开](@entry_id:145057)和误差界成立，我们需要PDE的解 $u(t,x)$ 具有足够的[光滑性](@entry_id:634843)（例如，对于EM格式的1阶弱收敛性证明，通常需要 $u$ 的时间导数有界，空间导数直到四阶有界）。而 $u$ 的光滑性又取决于SDE系数 $a, b$ 和终端函数 $\varphi$ 的光滑性。例如，在系数足够光滑且[扩散](@entry_id:141445)项一致椭圆的条件下，如果 $\varphi \in C_b^k$，那么 $u$ 也将具有相应的高阶[光滑性](@entry_id:634843)。[@problem_id:3083342]

### 高阶弱格式的设计原理与收敛性的细微之处

#### 基于[伊藤-泰勒展开](@entry_id:139712)设计[高阶格式](@entry_id:150564)

我们已经看到，EM格式之所以是1阶[弱收敛](@entry_id:146650)，是因为其单步期望与真实解的期望在 $O(h)$ 阶上一致。为了构造更高阶的弱收敛格式，我们需要在更高阶上匹配这些期望。这引导我们使用 **[伊藤-泰勒展开](@entry_id:139712)**（Itô-Taylor expansion）。

[伊藤-泰勒展开](@entry_id:139712)是SDE解在时间步长 $h$ 上的随机版本泰勒级数，它通过迭代[伊藤积分](@entry_id:272774)来表示。对于标量SDE，其展开式的前几项为：
$$
X_{t+h} = X_t + a I_{(0)} + b I_{(1)} + b b' I_{(1,1)} + (ab' + \frac{1}{2}b^2b'') I_{(0,1)} + b a' I_{(1,0)} + \dots
$$
其中 $a, b$ 及其导数在 $X_t$ 处取值，$I_{(\dots)}$ 是迭代[伊藤积分](@entry_id:272774)，例如 $I_{(0)}=\int_t^{t+h} ds = h$, $I_{(1)}=\int_t^{t+h}dW_s = \Delta W$, $I_{(1,1)} = \int_t^{t+h}\int_t^{s_1} dW_{s_2}dW_{s_1} = \frac{1}{2}((\Delta W)^2-h)$。[@problem_id:3083380]

一个数值格式 $Y_{n+1} = \Psi(Y_n, h, \xi_n)$（其中 $\xi_n$ 是一组易于模拟的[随机变量](@entry_id:195330)）若要达到 $p$ 阶[弱收敛](@entry_id:146650)，其设计原则是：选择 $\Psi$ 和 $\xi_n$ 的[分布](@entry_id:182848)，使得 $\varphi(Y_{n+1})$ 的条件期望与 $\varphi(X_{t+h})$ 的[条件期望](@entry_id:159140)在展开后匹配到 $h^p$ 阶。这等价于匹配 $Y_{n+1}-Y_n$ 和 $X_{t+h}-X_t$ 的某些组合矩。[@problem_id:3083380]

例如，要实现2阶[弱收敛](@entry_id:146650)，[数值格式](@entry_id:752822)的增量需要模拟真实增量直到 $h^2$ 阶的矩，这通常需要引入额外的修正项和更复杂的[随机变量](@entry_id:195330)，而不仅仅是高斯增量 $\Delta W_n$。标准[Milstein格式](@entry_id:140856)虽然通过引入 $I_{(1,1)}$ 项将强[收敛阶](@entry_id:146394)提高到1，但其[弱收敛](@entry_id:146650)阶通常仍为1，因为它没有包含获得2阶[弱收敛](@entry_id:146650)所需的额外漂移修正。[@problem_id:3083342] [@problem_id:3083325]

#### 检验[函数[光滑](@entry_id:161935)性](@entry_id:634843)的影响

我们反复强调[弱收敛](@entry_id:146650)阶依赖于检验函数 $\varphi$ 的光滑性。现在我们来系统地审视这一问题。一个数值格式的“[弱收敛](@entry_id:146650)阶”并不是一个单一的数字，而是依赖于我们用何种函数“探查”其[分布](@entry_id:182848)。[@problem_id:3083378]

1.  **光滑[有界函数](@entry_id:176803) ($C_b^k$)**: 对于这[类函数](@entry_id:146970)（例如 $k \ge 4$），我们之前介绍的分析方法完全适用。EM格式具有1阶[弱收敛](@entry_id:146650)性。这是最经典的结果。

2.  **利普希茨函数 (Lipschitz functions)**: 如果 $\varphi$ 仅仅是利普希茨连续而不可微，那么基于泰勒展开的分析方法就会失效。此时，误差界通常通过强收敛误差来获得：
    $$
    |\mathbb{E}[\varphi(X_T)] - \mathbb{E}[\varphi(X_T^h)]| \le \mathbb{E}[|\varphi(X_T) - \varphi(X_T^h)|] \le L_\varphi \mathbb{E}[|X_T - X_T^h|]
    $$
    其中 $L_\varphi$ 是 $\varphi$ 的[利普希茨常数](@entry_id:146583)。由于EM格式的强[收敛阶](@entry_id:146394)为 $1/2$，我们只能得到一个 $O(h^{1/2})$ 的弱收敛界。因此，对于非光滑的利普希茨[可观测量](@entry_id:267133)，弱[收敛速度](@entry_id:636873)会退化到与强收敛速度相同。

3.  **[不连续函数](@entry_id:143848) (Discontinuous functions)**: 一个重要的例子是[示性函数](@entry_id:261577) $\varphi(x) = \mathbf{1}_A(x)$，其期望 $\mathbb{E}[\mathbf{1}_A(X_T)] = \mathbb{P}(X_T \in A)$ 是解落入某个区域 $A$ 的概率。由于 $\varphi$ 的[不连续性](@entry_id:144108)，微小的路径扰动可能导致函数值从0跳到1。误差主要集中在区域 $A$ 的边界 $\partial A$ 附近。在[扩散](@entry_id:141445)项非退化（即一致椭圆）的假设下，$X_T$ 的概率密度函数是光滑的。误差可以被看作是数值解的路径“错误地”穿过边界 $\partial A$ 所致。由于EM格式的路径误差尺度为 $h^{1/2}$，可以想象误差主要来自一个宽度为 $O(h^{1/2})$ 的“[边界层](@entry_id:139416)”。该层的测度也大致是 $O(h^{1/2})$，因此弱误差通常也是 $O(h^{1/2})$。

综上所述，EM格式的[弱收敛](@entry_id:146650)阶依赖于观测量的正则性：对于高度光滑的量，收敛阶为1；而对于仅仅是利普希茨连续或不连续的量（如期权价格的某些数字期权或概率），收敛阶通常会降低到1/2。理解这种依赖关系对于在实际应用中选择合适的数值格式和步长至关重要。[@problem_id:3083378]