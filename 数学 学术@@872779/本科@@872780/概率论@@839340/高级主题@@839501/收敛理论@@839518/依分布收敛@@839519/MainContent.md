## 引言
在概率论和统计学的广阔领域中，一个核心问题是理解当样本量趋于无穷时，[随机变量](@entry_id:195330)序列的极限行为。这一问题不仅具有深刻的理论意义，更是连接理论与实践的桥梁，为现实世界中的数据分析和建模提供了基础。在多种[随机变量的收敛](@entry_id:187766)模式中，**[分布](@entry_id:182848)收敛**（Convergence in Distribution）因其广泛的适用性和深刻的内涵而占据了中心地位。它不关注[随机变量](@entry_id:195330)的单个实[现值](@entry_id:141163)，而是聚焦于其整体[概率分布](@entry_id:146404)的演化形态，这使得我们能够分析和预测许多复杂系统的长期行为。

然而，对于初学者而言，[分布](@entry_id:182848)收敛的定义可能显得抽象，其背后的强大工具和定理（如中心极限定理）如何应用于实际问题也常常令人困惑。本文旨在弥合这一知识鸿沟，系统地引导读者深入[分布](@entry_id:182848)收敛的世界。

本文将通过三个核心章节，层层递进地展开论述：
- **第一章：原理与机制**，我们将从[分布](@entry_id:182848)收敛的严格定义和直观例子入手，建立对其本质的理解。随后，我们将介绍证明收敛性的两大支柱——[矩生成函数](@entry_id:154347)法和中心极限定理，并进一步探讨[连续映射定理](@entry_id:269346)、[Delta方法](@entry_id:276272)和[斯卢茨基定理](@entry_id:181685)等高级工具。
- **第二章：应用与跨学科联系**，我们将展示[分布](@entry_id:182848)收敛如何作为理论基石，支撑起统计推断、[随机过程](@entry_id:159502)分析、极端值理论等多个领域，并联系金融、工程、生物学等学科中的具体实例。
- **第三章：动手实践**，读者将通过解决一系列精心设计的问题，将理论知识转化为解决实际问题的能力。

通过本次学习，你将不仅掌握[分布](@entry_id:182848)收敛的数学原理，更能领会其在现代科学研究中作为一种强大分析[范式](@entry_id:161181)的力量。让我们从[分布](@entry_id:182848)收敛最基本的原理与机制开始探索。

## 原理与机制

在概率论和统计学的研究中，我们常常关心当样本量趋于无穷时，一个[随机变量](@entry_id:195330)序列的行为。[随机变量](@entry_id:195330)[序列的收敛](@entry_id:140648)有多种模式，其中**[分布](@entry_id:182848)收敛** (convergence in distribution) 是最基本且应用最广泛的一种。它描述的是[随机变量](@entry_id:195330)的[累积分布函数 (CDF)](@entry_id:264700) [序列的收敛](@entry_id:140648)行为。本章将深入探讨[分布](@entry_id:182848)收敛的核心原理、证明其收敛性的关键工具，以及在这些基础上建立的若干高级定理。

### [分布](@entry_id:182848)收敛的定义与直观理解

一个[随机变量](@entry_id:195330)序列 $\{X_n\}_{n=1}^{\infty}$ 被称为**[分布](@entry_id:182848)收敛**于[随机变量](@entry_id:195330) $X$，记作 $X_n \xrightarrow{d} X$，如果对于 $X$ 的累积分布函数 $F(x)$ 的所有连续点 $x$，序列 $\{X_n\}$ 的累积分布函数 $F_n(x)$ 都[逐点收敛](@entry_id:145914)于 $F(x)$。即：
$$ \lim_{n\to\infty} F_n(x) = F(x) $$
其中 $F_n(x) = P(X_n \le x)$ 且 $F(x) = P(X \le x)$。

这个定义有几个值得注意的要点。首先，收敛性是在[极限分布](@entry_id:174797) $F(x)$ 的**连续点**上定义的，这允许在离散点上存在不一致。其次，[分布](@entry_id:182848)收敛只关心[随机变量](@entry_id:195330)的分布函数，而不关心[随机变量](@entry_id:195330)本身。这意味着 $X_n$ 和 $X$ 可以定义在完全不同的概率空间上。

为了建立直观理解，我们来看两个典型的例子，它们展示了[分布](@entry_id:182848)收敛如何连接离散和连续世界。

#### 从连续到离散的收敛

考虑一个思想实验：我们从区间 $[0, 1]$ 上的[连续均匀分布](@entry_id:275979)中独立抽取 $n$ 个随机数 $U_1, U_2, \dots, U_n$。然后，我们定义一个新的[随机变量](@entry_id:195330) $X_n$ 为这 $n$ 个数中的最大值，即 $X_n = \max(U_1, \dots, U_n)$。我们想知道当 $n$ 变得非常大时，$X_n$ 的[分布](@entry_id:182848)会趋向于什么 [@problem_id:1353124]。

为了找到 $X_n$ 的累积分布函数 $F_n(x)$，我们注意到事件 $\{X_n \le x\}$ 等价于所有 $U_i$ 都小于或等于 $x$。由于 $U_i$ 是[相互独立](@entry_id:273670)的，并且对于 $x \in [0, 1]$，单个 $U_i$ 满足 $P(U_i \le x) = x$，我们得到：
$$ F_n(x) = P(X_n \le x) = P(U_1 \le x, \dots, U_n \le x) = \prod_{i=1}^{n} P(U_i \le x) = x^n $$
对于 $x \in [0, 1]$。完整的 CDF 为：
$$ F_n(x) = \begin{cases} 0,  x  0 \\ x^n,  0 \le x  1 \\ 1,  x \ge 1 \end{cases} $$
现在我们考察当 $n \to \infty$ 时 $F_n(x)$ 的极限。
- 若 $0 \le x  1$，则 $\lim_{n\to\infty} x^n = 0$。
- 若 $x \ge 1$，则 $\lim_{n\to\infty} F_n(x) = 1$。

因此，[极限分布](@entry_id:174797)函数 $F(x)$ 是一个阶梯函数：
$$ F(x) = \lim_{n\to\infty} F_n(x) = \begin{cases} 0,  x  1 \\ 1,  x \ge 1 \end{cases} $$
这个 CDF 对应于一个**退化[随机变量](@entry_id:195330)** (degenerate random variable) $X$，它以概率 1 取值为 1，即 $P(X=1) = 1$。这是一个深刻的结果：一个[连续随机变量](@entry_id:166541)序列 $X_n$ 在[分布](@entry_id:182848)上收敛到了一个[离散随机变量](@entry_id:163471)。直观上，随着样本量 $n$ 的增加，样本中的最大值越来越可能接近 1。

#### 从离散到连续的收敛

现在我们来看一个相反方向的例子。考虑一个[离散随机变量](@entry_id:163471) $U_n$，它在集合 $\{ \frac{1}{n}, \frac{2}{n}, \dots, \frac{n}{n}=1 \}$ 上均匀取值 [@problem_id:1910208]。这意味着 $P(U_n = k/n) = 1/n$ 对于 $k = 1, \dots, n$。

对于任意 $x \in [0, 1]$，其[累积分布函数](@entry_id:143135) $F_n(x)$ 是所有小于或等于 $x$ 的可能取值的概率之和。小于或等于 $x$ 的点的形式为 $k/n$，即 $k/n \le x$，或 $k \le nx$。满足这个条件的整数 $k$ 的数量是 $\lfloor nx \rfloor$。因此，
$$ F_n(x) = P(U_n \le x) = \sum_{k=1}^{\lfloor nx \rfloor} P(U_n = k/n) = \frac{\lfloor nx \rfloor}{n} $$
我们知道不等式 $nx - 1  \lfloor nx \rfloor \le nx$ 成立。两边同除以 $n$ 得到：
$$ x - \frac{1}{n}  \frac{\lfloor nx \rfloor}{n} \le x $$
根据[夹逼定理](@entry_id:147218)，当 $n \to \infty$ 时，$\frac{\lfloor nx \rfloor}{n}$ 收敛于 $x$。因此，[极限分布](@entry_id:174797)函数为：
$$ F(x) = \lim_{n\to\infty} F_n(x) = \begin{cases} 0,  x  0 \\ x,  0 \le x \le 1 \\ 1,  x > 1 \end{cases} $$
这正是区间 $[0, 1]$ 上[连续均匀分布](@entry_id:275979)的 CDF。这个例子说明，一个[离散随机变量](@entry_id:163471)序列可以“填充”整个区间，其[分布](@entry_id:182848)最终收敛到一个连续分布。

#### 关于收敛本质的注记

[分布](@entry_id:182848)收敛关注的是分布[函数序列的极限](@entry_id:142182)行为，而非[随机变量](@entry_id:195330)实现值[序列的极限](@entry_id:159239)。一个有趣的例子可以阐明这一点 [@problem_id:1910231]。设 $X$ 是一个服从 $(-1, 1)$ 上[均匀分布](@entry_id:194597)的[随机变量](@entry_id:195330)，其[概率密度函数](@entry_id:140610) $f_X(x) = 1/2$ for $x \in (-1, 1)$。定义一个序列 $X_n = (-1)^n X$。
- 当 $n$ 是偶数时，$X_n = X$。
- 当 $n$ 是奇数时，$X_n = -X$。由于 $X$ 的[分布](@entry_id:182848)是关于[原点对称](@entry_id:172995)的，$-X$ 的[分布](@entry_id:182848)与 $X$ 完全相同。

因此，对于所有的 $n$，[随机变量](@entry_id:195330) $X_n$ 都具有与 $X$ 相同的[分布](@entry_id:182848)。其 CDF 序列 $F_n(x)$ 是一个常数序列，即 $F_n(x) = F_X(x)$ 对所有 $n$ 成立。这个序列当然收敛于 $F_X(x)$。所以，$X_n \xrightarrow{d} X$。然而，序列 $X_1, X_2, X_3, \dots$ 的实[现值](@entry_id:141163)是 $-x, x, -x, \dots$，它并不会收敛到一个固定的值。这突显了[分布](@entry_id:182848)收敛与更强的[收敛模式](@entry_id:189917)（如[依概率收敛](@entry_id:145927)或[几乎必然收敛](@entry_id:265812)）之间的区别。

### 证明收敛的基本工具

虽然直接使用 CDF 的定义来证明收敛是可行的，但在许多情况下，这样做会非常繁琐。幸运的是，我们有两个强大的工具可以极大地简化这一过程：[矩生成函数](@entry_id:154347)和[中心极限定理](@entry_id:143108)。

#### [矩生成函数](@entry_id:154347)法

**[矩生成函数](@entry_id:154347)** (Moment Generating Function, MGF) 是一个强大的分析工具。**Lévy-Cramér [连续性定理](@entry_id:262016)**建立了 MGF 收敛与[分布](@entry_id:182848)收敛之间的桥梁：如果[随机变量](@entry_id:195330)序列 $\{X_n\}$ 的 MGF $M_{X_n}(t)$ 在包含原点的一个开区间内对所有 $t$ 都逐点收敛于某个函数 $M_X(t)$，并且 $M_X(t)$ 是某个[随机变量](@entry_id:195330) $X$ 的 MGF，那么 $X_n$ 在[分布](@entry_id:182848)上收敛于 $X$。

一个经典的例子是泊松分布作为二项分布的极限 [@problem_id:1353076]。考虑一个[二项分布](@entry_id:141181)序列 $X_n \sim B(n, p_n)$，其中试验次数 $n \to \infty$，而成功概率 $p_n = \lambda/n$ 趋于 0，使得期望 $np_n = \lambda$ 保持不变。[二项分布](@entry_id:141181)的 MGF 是 $M_{B(n,p)}(t) = (1 - p + pe^t)^n$。代入 $p_n = \lambda/n$，我们得到 $X_n$ 的 MGF：
$$ M_{X_n}(t) = \left(1 - \frac{\lambda}{n} + \frac{\lambda}{n}e^t\right)^n = \left(1 + \frac{\lambda(e^t - 1)}{n}\right)^n $$
利用极限 $\lim_{n\to\infty} (1 + a/n)^n = \exp(a)$，我们得到极限 MGF：
$$ \lim_{n\to\infty} M_{X_n}(t) = \exp(\lambda(e^t - 1)) $$
我们识别出这个[极限函数](@entry_id:157601)正是参数为 $\lambda$ 的[泊松分布](@entry_id:147769)的 MGF。因此，根据[连续性定理](@entry_id:262016)，$X_n \xrightarrow{d} \text{Pois}(\lambda)$。

另一个例子展示了如何通过 MGF 和[泰勒展开](@entry_id:145057)来识别[正态分布](@entry_id:154414)极限 [@problem_id:1353089]。假设一个序列 $X_n$ 的 MGF 为 $M_{X_n}(t) = (\cosh(t/\sqrt{n}))^n$。为了求其极限，我们先取对数：
$$ \ln M_{X_n}(t) = n \ln\left(\cosh\left(\frac{t}{\sqrt{n}}\right)\right) $$
使用 $\cosh(u) = 1 + u^2/2 + O(u^4)$ 和 $\ln(1+v) = v - v^2/2 + O(v^3)$ 的[泰勒级数展开](@entry_id:138468)，令 $u=t/\sqrt{n}$，我们得到：
$$ \ln\left(\cosh\left(\frac{t}{\sqrt{n}}\right)\right) = \ln\left(1 + \frac{t^2}{2n} + O\left(\frac{1}{n^2}\right)\right) = \frac{t^2}{2n} + O\left(\frac{1}{n^2}\right) $$
因此，
$$ \ln M_{X_n}(t) = n \left(\frac{t^2}{2n} + O\left(\frac{1}{n^2}\right)\right) = \frac{t^2}{2} + O\left(\frac{1}{n}\right) $$
当 $n \to \infty$ 时，$\ln M_{X_n}(t) \to t^2/2$，所以 $M_{X_n}(t) \to \exp(t^2/2)$。这是[标准正态分布](@entry_id:184509) $\mathcal{N}(0, 1)$ 的 MGF。因此，$X_n \xrightarrow{d} \mathcal{N}(0, 1)$。

#### [中心极限定理](@entry_id:143108)

**中心极限定理** (Central Limit Theorem, CLT) 是概率论的基石。其 **Lindeberg-Lévy** 形式指出，如果 $X_1, X_2, \dots$ 是独立同分布 (i.i.d.) 的[随机变量](@entry_id:195330)，具有有限的均值 $\mu$ 和有限的非零[方差](@entry_id:200758) $\sigma^2$，那么它们的标准化和将[分布](@entry_id:182848)收敛于标准正态分布。令 $S_n = \sum_{i=1}^n X_i$，则：
$$ Z_n = \frac{S_n - n\mu}{\sqrt{n\sigma^2}} \xrightarrow{d} \mathcal{N}(0, 1) \quad \text{as } n \to \infty $$
CLT 的惊人之处在于其普适性：无论原始[随机变量](@entry_id:195330) $X_i$ 的[分布](@entry_id:182848)是什么（只要其[方差](@entry_id:200758)有限），其标准化和的[极限分布](@entry_id:174797)总是标准正态分布。

一个基本的应用是 **De Moivre-Laplace 定理**，它是伯努利试验的 CLT [@problem_id:1353083]。设 $X_i \sim \text{Bernoulli}(p)$，则 $\mu = p$ 且 $\sigma^2 = p(1-p)$。样本比例 $\hat{p}_n = (\sum X_i)/n$。其标准化形式为：
$$ Z_n = \frac{\hat{p}_n - p}{\sqrt{\frac{p(1-p)}{n}}} = \frac{S_n/n - p}{\sqrt{p(1-p)/n}} = \frac{S_n - np}{\sqrt{np(1-p)}} $$
根据 CLT，当 $n \to \infty$ 时，$Z_n \xrightarrow{d} \mathcal{N}(0, 1)$。

CLT 同样适用于连续分布。例如，假设一个系统的组件寿命 $T_i$ 是 i.i.d. 的[指数分布](@entry_id:273894)[随机变量](@entry_id:195330)，参数为 $\lambda$ [@problem_id:1353115]。指数分布的均值为 $\mu = 1/\lambda$，[方差](@entry_id:200758)为 $\sigma^2 = 1/\lambda^2$。$n$ 个组件的总寿命 $S_n = \sum_{i=1}^n T_i$ 的期望为 $E[S_n] = n/\lambda$，[方差](@entry_id:200758)为 $\mathrm{Var}(S_n) = n/\lambda^2$。其标准化和为：
$$ Z_n = \frac{S_n - E[S_n]}{\sqrt{\mathrm{Var}(S_n)}} = \frac{S_n - n/\lambda}{\sqrt{n/\lambda^2}} $$
根据 CLT，无论 $\lambda$ 的值是多少，$Z_n$ 都[分布](@entry_id:182848)收敛于[标准正态分布](@entry_id:184509) $\mathcal{N}(0, 1)$。

### 高级定理及其应用

基于[分布](@entry_id:182848)收敛和中心极限定理，我们可以推导出一系列功能强大的定理，它们极大地扩展了我们分析复杂统计量[渐近行为](@entry_id:160836)的能力。

#### [连续映射定理](@entry_id:269346)

**[连续映射定理](@entry_id:269346)** (Continuous Mapping Theorem, CMT) 指出，如果 $X_n \xrightarrow{d} X$，并且 $g$ 是一个[连续函数](@entry_id:137361)，那么 $g(X_n) \xrightarrow{d} g(X)$。这意味着我们可以将收敛性“传递”给一个[连续函数](@entry_id:137361)作用后的新序列。

例如，假设我们已知根据 CLT，$\sqrt{n}(\bar{X}_n - \mu) \xrightarrow{d} Y$，其中 $Y \sim \mathcal{N}(0, \sigma^2)$ [@problem_id:1910230]。我们想知道统计量 $T_n = n(\bar{X}_n - \mu)^2$ 的[极限分布](@entry_id:174797)。我们可以将 $T_n$ 写成 $(\sqrt{n}(\bar{X}_n - \mu))^2$。令 $Y_n = \sqrt{n}(\bar{X}_n - \mu)$ 和函数 $g(y) = y^2$。由于 $g$ 是一个[连续函数](@entry_id:137361)，根据 CMT，
$$ T_n = g(Y_n) \xrightarrow{d} g(Y) = Y^2 $$
其中 $Y \sim \mathcal{N}(0, \sigma^2)$。我们可以将 $Y$ 写成 $Y = \sigma Z$，其中 $Z \sim \mathcal{N}(0, 1)$ 是标准正态[随机变量](@entry_id:195330)。因此，[极限分布](@entry_id:174797)是 $(\sigma Z)^2 = \sigma^2 Z^2$。$Z^2$ 是一个标准正态[随机变量](@entry_id:195330)的平方，它服从自由度为 1 的**[卡方分布](@entry_id:165213)** ($\chi_1^2$)。所以 $T_n$ 收敛到一个按 $\sigma^2$ 缩放的卡方分布。

#### Delta 方法

**Delta 方法**是 CLT 和 CMT 的一种巧妙结合，它利用[泰勒展开](@entry_id:145057)来近似一个函数作用于[随机变量](@entry_id:195330)序列后的[分布](@entry_id:182848)。其核心思想是，如果一个序列经过适当中心化和缩放后收敛于[正态分布](@entry_id:154414)，那么该序列经过平滑[函数变换](@entry_id:141095)后，其[极限分布](@entry_id:174797)仍然是[正态分布](@entry_id:154414)，只是[方差](@entry_id:200758)会根据函数的导数进行调整。

具体来说，如果 $\sqrt{n}(T_n - \theta) \xrightarrow{d} \mathcal{N}(0, \sigma^2)$，并且函数 $g(x)$ 在 $\theta$ 点可微，那么：
$$ \sqrt{n}(g(T_n) - g(\theta)) \xrightarrow{d} \mathcal{N}(0, [g'(\theta)]^2 \sigma^2) $$
直观上，这是基于一阶泰勒展开 $g(T_n) \approx g(\theta) + g'(\theta)(T_n - \theta)$。

考虑一个应用场景：我们测量了 $n$ 个[独立样本](@entry_id:177139)的电阻值 $R_1, \dots, R_n$，[总体均值](@entry_id:175446)为 $\mu > 0$，[方差](@entry_id:200758)为 $\sigma^2$。样本均值为 $\bar{R}_n$。根据 CLT，$\sqrt{n}(\bar{R}_n - \mu) \xrightarrow{d} \mathcal{N}(0, \sigma^2)$。现在我们关心电阻平方根的统计量 $\sqrt{\bar{R}_n}$ 的行为 [@problem_id:1353120]。

我们应用 Delta 方法，其中 $T_n = \bar{R}_n$, $\theta = \mu$。我们感兴趣的变换是 $g(x) = \sqrt{x}$。这个函数在 $\mu > 0$ 处是可微的，其导数为 $g'(x) = \frac{1}{2\sqrt{x}}$。在 $\mu$ 点的导数值为 $g'(\mu) = \frac{1}{2\sqrt{\mu}}$。根据 Delta 方法的公式，我们得到：
$$ \sqrt{n}(\sqrt{\bar{R}_n} - \sqrt{\mu}) \xrightarrow{d} \mathcal{N}\left(0, [g'(\mu)]^2 \sigma^2\right) = \mathcal{N}\left(0, \left(\frac{1}{2\sqrt{\mu}}\right)^2 \sigma^2\right) = \mathcal{N}\left(0, \frac{\sigma^2}{4\mu}\right) $$
因此，极限正态分布的[方差](@entry_id:200758)是 $\frac{\sigma^2}{4\mu}$。

#### [斯卢茨基定理](@entry_id:181685)

**[斯卢茨基定理](@entry_id:181685)** (Slutsky's Theorem) 提供了一套关于[随机变量](@entry_id:195330)极限的“代数法则”，它允许我们将[分布](@entry_id:182848)收敛与**[依概率收敛](@entry_id:145927)** (convergence in probability) 结合起来。如果 $X_n \xrightarrow{d} X$ 且 $Y_n \xrightarrow{p} c$（其中 $c$ 是一个常数），那么：
1. $X_n + Y_n \xrightarrow{d} X + c$
2. $X_n Y_n \xrightarrow{d} cX$
3. 如果 $c \ne 0$，则 $X_n / Y_n \xrightarrow{d} X/c$

这个定理在统计推断中极其有用，特别是当我们处理的统计量是多个部分的组合时。一个经典的应用是推导学生 t-统计量在大样本下的[极限分布](@entry_id:174797) [@problem_id:1910194]。考虑统计量：
$$ T_n = \frac{\sqrt{n}(\bar{X}_n - \mu)}{S_n} $$
其中 $\bar{X}_n$ 是样本均值，$S_n$ 是样本标准差。我们分两部分来分析：
1.  **分子**: 根据[中心极限定理](@entry_id:143108)，分子 $\sqrt{n}(\bar{X}_n - \mu)$ [分布](@entry_id:182848)收敛于一个正态分布 $Y \sim \mathcal{N}(0, \sigma^2)$。
2.  **分母**: 样本[方差](@entry_id:200758) $S_n^2 = \frac{1}{n-1}\sum (X_i - \bar{X}_n)^2$ 是总体[方差](@entry_id:200758) $\sigma^2$ 的[一致估计量](@entry_id:266642)。这意味着 $S_n^2$ [依概率收敛](@entry_id:145927)于 $\sigma^2$ (即 $S_n^2 \xrightarrow{p} \sigma^2$)。由于[平方根函数](@entry_id:184630) $g(x)=\sqrt{x}$ 在 $\sigma^2 > 0$ 处连续，根据[连续映射定理](@entry_id:269346)的一个推论，样本标准差 $S_n = \sqrt{S_n^2}$ [依概率收敛](@entry_id:145927)于 $\sigma$ (即 $S_n \xrightarrow{p} \sigma$)。

现在我们有了 $A_n = \sqrt{n}(\bar{X}_n - \mu) \xrightarrow{d} Y \sim \mathcal{N}(0, \sigma^2)$ 和 $B_n = S_n \xrightarrow{p} \sigma$。根据[斯卢茨基定理](@entry_id:181685)的第三条，它们的比值收敛于：
$$ T_n = \frac{A_n}{B_n} \xrightarrow{d} \frac{Y}{\sigma} $$
其中 $Y \sim \mathcal{N}(0, \sigma^2)$。[随机变量](@entry_id:195330) $Y/\sigma$ 的[分布](@entry_id:182848)是什么？它的期望是 $E[Y/\sigma] = 0/\sigma = 0$，[方差](@entry_id:200758)是 $\mathrm{Var}(Y/\sigma) = \mathrm{Var}(Y)/\sigma^2 = \sigma^2/\sigma^2 = 1$。因此，[极限分布](@entry_id:174797)是标准正态分布 $\mathcal{N}(0, 1)$。

这个结果意义重大：它意味着即使总体[方差](@entry_id:200758) $\sigma^2$ 未知，我们也可以用样本[标准差](@entry_id:153618) $S_n$ 来代替它，在大样本情况下，得到的 t-统计量仍然近似服从标准正态分布。这为构建关于均值 $\mu$ 的大样本[置信区间](@entry_id:142297)和假设检验提供了理论基础。