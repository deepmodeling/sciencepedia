## 引言
在概率论和[随机过程](@entry_id:159502)的研究中，理解[随机变量](@entry_id:195330)序列的[长期行为](@entry_id:192358)是一个根本性的问题。与确定性分析中单一的收敛概念不同，随机性引入了多种描述“极限”行为的方式，每一种都捕捉了序列渐近特性的一个独特侧面。从几乎每个样本路径的逐点收敛，到整个[分布](@entry_id:182848)形态的趋同，这些不同的[收敛模式](@entry_id:189917)构成了严谨分析随机现象的语言。然而，这些模式之间的微妙区别和层级关系常常导致混淆，而这种混淆可能在应用中引发错误的结论。本文旨在系统地厘清这些概念，填补理论与实践之间的认知鸿沟。

本文将通过以下部分展开探讨：首先，“**原理与机制**”部分将精确定义[几乎必然收敛](@entry_id:265812)、[依概率收敛](@entry_id:145927)、$L^p$收敛和[依分布收敛](@entry_id:275544)，并通过关键定理和反例深入剖析它们之间的逻辑关系。接着，“**应用与交叉学科联系**”部分将展示这些抽象概念如何在[统计推断](@entry_id:172747)、[随机微分方程](@entry_id:146618)[数值模拟](@entry_id:137087)和控制理论等领域发挥关键作用。最后，通过“**动手实践**”中的一系列问题，读者将有机会在具体情境中应用和巩固所学知识。

现在，让我们深入探讨[随机变量](@entry_id:195330)收敛的基本原理与机制。

## 原理与机制

在研究[随机变量](@entry_id:195330)序列时，一个核心问题是如何描述它们的极限行为。与确定性[序列的收敛](@entry_id:140648)不同，随机[序列的收敛](@entry_id:140648)性可以在多种截然不同的意义下被定义。这些不同的[收敛模式](@entry_id:189917)捕捉了序列行为的不同方面，从逐点实现的收敛到分布函数的渐近形态。理解这些[收敛模式](@entry_id:189917)及其相互关系，对于严格分析[随机微分方程](@entry_id:146618)的解及其数值近似至关重要。本章将系统地阐述[随机变量](@entry_id:195330)和[随机过程](@entry_id:159502)收敛的主要模式，并通过关键示例和定理揭示它们之间的深刻联系。

### [随机变量](@entry_id:195330)的基本[收敛模式](@entry_id:189917)

设 $(\Omega, \mathcal{F}, \mathbb{P})$ 为一个[概率空间](@entry_id:201477)，$\{X_n\}_{n \ge 1}$ 和 $X$ 是定义在该空间上的实值[随机变量](@entry_id:195330)。以下四种[收敛模式](@entry_id:189917)构成了概率论的基石。

#### [几乎必然收敛](@entry_id:265812) (Almost Sure Convergence)

**[几乎必然收敛](@entry_id:265812)**，或称**[以概率1收敛](@entry_id:265812)**，是[随机变量](@entry_id:195330)最强的[收敛模式](@entry_id:189917)。它要求对于概率空间中除了一个零测集之外的所有结果 $\omega$，序列 $X_n(\omega)$ 都像普通的[实数序列](@entry_id:141090)一样收敛到 $X(\omega)$。

**定义 2.1 ([几乎必然收敛](@entry_id:265812))**：序列 $\{X_n\}$ **[几乎必然收敛](@entry_id:265812)**到 $X$，记作 $X_n \xrightarrow{a.s.} X$，如果
$$
\mathbb{P}\left( \left\{ \omega \in \Omega : \lim_{n\to\infty} X_n(\omega) = X(\omega) \right\} \right) = 1
$$
这等价于 $\mathbb{P}(\lim_{n\to\infty} |X_n - X| = 0) = 1$ [@problem_id:2994139] [@problem_id:2987745]。强[大数定律](@entry_id:140915) (Strong Law of Large Numbers, SLLN) 是[几乎必然收敛](@entry_id:265812)的一个典型例子，它断言在适当条件下，[独立同分布随机变量](@entry_id:270381)序列的样本均值几乎必然收斂到其[期望值](@entry_id:153208) [@problem_id:2984547]。

#### [依概率收敛](@entry_id:145927) (Convergence in Probability)

**[依概率收敛](@entry_id:145927)**是一个比[几乎必然收敛](@entry_id:265812)更弱的概念。它不要求每个样本实现都收敛，而是要求 $X_n$ 和 $X$ 之间出现显著偏差的概率随着 $n$ 的增大而趋于零。

**定义 2.2 ([依概率收敛](@entry_id:145927))**：序列 $\{X_n\}$ **[依概率收敛](@entry_id:145927)**到 $X$，记作 $X_n \xrightarrow{p} X$，如果对于任意 $\varepsilon > 0$，
$$
\lim_{n\to\infty} \mathbb{P}(|X_n - X| > \varepsilon) = 0
$$
[@problem_id:2994139] [@problem_id:2987766]。[弱大数定律](@entry_id:159016) (Weak Law of Large Numbers, WLLN) 就是一个关于[依概率收敛](@entry_id:145927)的经典结果 [@problem_id:2984547]。[依概率收敛](@entry_id:145927)有时也称为[依测度收敛](@entry_id:141115)，在[概率测度](@entry_id:190821)下这两个概念是等价的 [@problem_id:2987758]。

#### $L^p$ 收敛 (Convergence in Mean)

**$L^p$收敛**（或称**$p$阶[均值收敛](@entry_id:269534)**）通过期望来度量收敛性，要求 $X_n$ 与 $X$ 之间差的 $p$ 次幂的期望趋于零。

**定义 2.3 ($L^p$ 收敛)**：对于 $p \ge 1$，序列 $\{X_n\}$ **在 $L^p$ 中收敛**到 $X$，记作 $X_n \xrightarrow{L^p} X$，如果 $\mathbb{E}[|X|^p]  \infty$，$\mathbb{E}[|X_n|^p]  \infty$ 对所有 $n$ 成立，并且
$$
\lim_{n\to\infty} \mathbb{E}\left[|X_n - X|^p\right] = 0
$$
[@problem_id:2994139]。$L^1$ 收敛确保了期望的[可交换性](@entry_id:263314)，即 $\lim_{n\to\infty} \mathbb{E}[X_n] = \mathbb{E}[X]$。

#### [依分布收敛](@entry_id:275544) (Convergence in Distribution)

**[依分布收敛](@entry_id:275544)**，也称**弱收敛**，是最弱的[收敛模式](@entry_id:189917)。它只关心[随机变量](@entry_id:195330)的[概率分布](@entry_id:146404)的渐近形态，而不关心[随机变量](@entry_id:195330)本身的值。

**定义 2.4 ([依分布收敛](@entry_id:275544))**：序列 $\{X_n\}$ **[依分布收敛](@entry_id:275544)**到 $X$，记作 $X_n \Rightarrow X$，如果它们的[累积分布函数 (CDF)](@entry_id:264700) 在 $F_X$ 的所有连续点 $x$ 处逐点收敛，即 $\lim_{n\to\infty} F_{X_n}(x) = F_X(x)$。一个等价且更强大的定义是，对于任意有界[连续函数](@entry_id:137361) $f: \mathbb{R} \to \mathbb{R}$，都有
$$
\lim_{n\to\infty} \mathbb{E}[f(X_n)] = \mathbb{E}[f(X)]
$$
[@problem_id:2994139]。中心极限定理 (Central Limit Theorem) 是[依分布收敛](@entry_id:275544)的最著名例子。

### [收敛模式](@entry_id:189917)的层级与关系

这些[收敛模式](@entry_id:189917)之间存在一个明确的层级关系。理解它们之间的推论和非推论关系对于正确[应用概率论](@entry_id:264675)至关重要。

#### 主要的推论链

两个最强的[收敛模式](@entry_id:189917)——[几乎必然收敛](@entry_id:265812)和$L^p$收敛——都蕴含着[依概率收敛](@entry_id:145927)。而[依概率收敛](@entry_id:145927)又蕴含着最弱的[依分布收敛](@entry_id:275544)。

1.  **[几乎必然收敛](@entry_id:265812) $\implies$ [依概率收敛](@entry_id:145927)**：如果 $X_n(\omega)$ 对几乎所有的 $\omega$ 都收敛到 $X(\omega)$，那么 $|X_n - X|$ 大于某个正数 $\varepsilon$ 的事件最终只会发生在概率为零的集合上。

2.  **$L^p$ 收敛 $\implies$ [依概率收敛](@entry_id:145927)**：这个推论可以通过[Markov不等式](@entry_id:266353)优雅地证明。对于任意 $\varepsilon  0$，
    $$
    \mathbb{P}(|X_n - X|  \varepsilon) = \mathbb{P}(|X_n - X|^p  \varepsilon^p) \le \frac{\mathbb{E}[|X_n - X|^p]}{\varepsilon^p}
    $$
    由于 $X_n \xrightarrow{L^p} X$，期望项趋于零，因此概率也趋于零 [@problem_id:2984547]。

3.  **[依概率收敛](@entry_id:145927) $\implies$ [依分布收敛](@entry_id:275544)**：这是因为当 $X_n$ 在概率上接近 $X$ 时，它们的分布函数也必然会趋于一致。

综上，我们有如下的推论关系图 [@problem_id:2994139] [@problem_id:2984547]：
$$
\begin{matrix}
    \text{几乎必然收敛 (a.s.)} \\
   \downarrow \\
L^p \text{收敛}  \to  \text{依概率收敛 (p)}  \to  \text{依分布收敛 (d)} \\
   \nwarrow  \uparrow \\
    L^q \text{收敛 (q>p)} \\
\end{matrix}
$$
此外，通过Lyapunov不等式可以证明，如果 $q>p\ge 1$，那么$L^q$收敛蕴含$L^p$收敛。

#### 反向推论的失效：关键反例

上述推论链的箭头通常是不可逆的。理解其原因的最佳方式是通过一系列精心构造的反例。

*   **[依分布收敛](@entry_id:275544) $\nRightarrow$ [依概率收敛](@entry_id:145927)**

    [依分布收敛](@entry_id:275544)只关心[分布](@entry_id:182848)的形状，而[依概率收敛](@entry_id:145927)关心[随机变量](@entry_id:195330)的“值”是否接近。一个简单的例子可以清晰地说明这一点。设 $X \sim \text{Bernoulli}(1/2)$，并定义序列 $X_n = 1-X$ 对所有 $n$ 成立。由于 $X$ 取值为0和1的概率均为$1/2$，那么 $1-X$ 也服从 $\text{Bernoulli}(1/2)$ [分布](@entry_id:182848)。因此，$X_n$ 和 $X$ 对所有 $n$ 都是同[分布](@entry_id:182848)的，这自然意味着 $X_n \Rightarrow X$。然而，我们来考察[依概率收敛](@entry_id:145927)。$|X_n - X| = |(1-X) - X| = |1-2X|$。当 $X=0$ 时，差为1；当 $X=1$ 时，差也为1。所以 $|X_n-X|=1$ 几乎必然成立。对于任意 $\varepsilon \in (0,1)$，$\mathbb{P}(|X_n - X|  \varepsilon) = \mathbb{P}(1  \varepsilon) = 1$，它并不趋于0。因此，$X_n$ 不[依概率收敛](@entry_id:145927)到 $X$ [@problem_id:1319229]。

*   **[依概率收敛](@entry_id:145927) $\nRightarrow$ [几乎必然收敛](@entry_id:265812)**

    这个区别比较微妙。[依概率收敛](@entry_id:145927)允许 $X_n(\omega)$ 和 $X(\omega)$ 在特定 $\omega$ 处频繁地出现偏差，只要这些偏差事件的概率总和趋于零。而[几乎必然收敛](@entry_id:265812)要求对于几乎每个 $\omega$，$X_n(\omega)$ 最终必须永久地停留在 $X(\omega)$ 的任意小邻域内。

    一个经典的例子是**“[打字机序列](@entry_id:139010)”** (typewriter sequence)。考虑概率空间 $((0,1), \mathcal{B}((0,1)), \lambda)$，其中 $\lambda$ 是[勒贝格测度](@entry_id:139781)。我们构造一列移动的指示函数。将正整数 $n$ 唯一地表示为 $n = \frac{k(k-1)}{2} + j$，其中 $k \ge 1, 1 \le j \le k$。定义区间 $I_n = [\frac{j-1}{k}, \frac{j}{k})$，并令 $X_n = \mathbf{1}_{I_n}$。
    -   **[依概率收敛](@entry_id:145927)到0**：对于任意 $\varepsilon \in (0,1)$，$\mathbb{P}(|X_n - 0|  \varepsilon) = \mathbb{P}(X_n=1) = \lambda(I_n) = \frac{1}{k}$。当 $n \to \infty$ 时，$k \to \infty$，所以该概率趋于0。因此 $X_n \xrightarrow{p} 0$。
    -   **不[几乎必然收敛](@entry_id:265812)**：对于任意一个 $\omega \in (0,1)$，在每一个“块”$k$ 中，由于区间族 $\{[\frac{j-1}{k}, \frac{j}{k})\}_{j=1}^k$ 覆盖了 $(0,1)$，总存在一个 $j$ 使得 $\omega \in I_n$ (其中 $n$ 对应于 $(k,j)$)。这意味着对于任意 $\omega$，序列 $X_n(\omega)$ 中会无限次出现1。因此，$\lim_{n\to\infty} X_n(\omega)$ 不存在，更不会是0。[几乎必然收敛](@entry_id:265812)失败了，而且是在整个[样本空间](@entry_id:275301)上失败 [@problem_id:2987766]。另一个基于[独立事件](@entry_id:275822)和[Borel-Cantelli引理](@entry_id:158432)的例子也同样说明了这一点 [@problem_id:2987758]。

*   **[几乎必然收敛](@entry_id:265812) $\nRightarrow L^p$ 收敛**

    即使序列几乎处处都收敛，它仍然可能在期望意义上不收敛。这通常发生在概率很小的集合上，$X_n$ 的值变得非常大，足以破坏期望的收敛性。考虑概率空间 $((0,1), \mathcal{B}((0,1)), \lambda)$，并定义序列 $X_n = n \mathbf{1}_{(0, 1/n)}$。
    -   **[几乎必然收敛](@entry_id:265812)到0**：对于任意固定的 $\omega \in (0,1)$，当 $n$ 足够大以至于 $1/n  \omega$ 时，$X_n(\omega) = 0$。因此，对于所有 $\omega \in (0,1)$，$\lim_{n\to\infty} X_n(\omega) = 0$。所以 $X_n \xrightarrow{a.s.} 0$。
    -   **不 $L^1$ 收敛**：我们计算其[期望值](@entry_id:153208)：$\mathbb{E}[|X_n - 0|] = \mathbb{E}[X_n] = \int_0^1 n \mathbf{1}_{(0, 1/n)}(\omega) d\lambda(\omega) = n \cdot \lambda((0, 1/n)) = n \cdot \frac{1}{n} = 1$。由于 $\mathbb{E}[|X_n|]$ 恒等于1，它不收敛到0。因此，$X_n$ 不在 $L^1$ 中收敛 [@problem_id:2987745]。

#### 弥合差距：一些重要定理

尽管反向推论通常不成立，但在某些附加条件下，我们可以从较弱的[收敛模式](@entry_id:189917)升级到较强的模式。

- **从依[分布](@entry_id:182848)到依概率**：如果 $X_n \Rightarrow c$，其中 $c$ 是一个常数（确定性）[随机变量](@entry_id:195330)，那么 $X_n \xrightarrow{p} c$。这是因为[极限分布](@entry_id:174797)的所有概率质量都集中在一个点上，排除了 $X_n$ 值在别处出现的可能性 [@problem_id:2994139]。

- **从依概率到[几乎必然](@entry_id:262518)**：虽然[依概率收敛](@entry_id:145927)本身不保证[几乎必然收敛](@entry_id:265812)，但一个深刻的结果（Riesz[子序列](@entry_id:147702)定理）表明，我们总能从中提取一个**[几乎必然收敛](@entry_id:265812)的[子序列](@entry_id:147702)**。即如果 $X_n \xrightarrow{p} X$，则存在一个子序列 $\{X_{n_k}\}$ 使得 $X_{n_k} \xrightarrow{a.s.} X$ [@problem_id:2987758] [@problem_id:2994139]。

- **从依概率到 $L^p$**：从[依概率收敛](@entry_id:145927)到 $L^p$ 收敛的鸿沟由**[一致可积性](@entry_id:199715) (Uniform Integrability, UI)** 来弥合。一个[随机变量](@entry_id:195330)族 $\{X_n\}$ 是[一致可积](@entry_id:202893)的，如果当 $M \to \infty$ 时，$\sup_n \mathbb{E}[|X_n| \mathbf{1}_{\{|X_n| > M\}}] \to 0$。这本质上是说，序列的“尾部”期望是一致小的，没有概率质量“逃逸到无穷远处”。**[Vitali收敛定理](@entry_id:276533)**断言：$X_n \xrightarrow{L^1} X$ 的充要条件是 $X_n \xrightarrow{p} X$ 且 $\{X_n\}$ 是[一致可积](@entry_id:202893)的。前述 $X_n=n \mathbf{1}_{(0,1/n)}$ 的例子就不是[一致可积](@entry_id:202893)的，因此即使它[依概率收敛](@entry_id:145927)（甚至a.s.收敛），也无法在$L^1$中收敛 [@problem_id:2987763]。

- **Skorokhod [表示定理](@entry_id:637872)**：这个强大的定理建立了[依分布收敛](@entry_id:275544)和[几乎必然收敛](@entry_id:265812)之间的另一座桥梁。它表明，如果 $X_n \Rightarrow X$ 并且它们都取值于一个Polish空间（如 $\mathbb{R}$），那么我们可以在另一个[概率空间](@entry_id:201477)上构造新的[随机变量](@entry_id:195330)序列 $\{Y_n\}$ 和 $Y$，使得 $Y_n$ 与 $X_n$同[分布](@entry_id:182848)，$Y$ 与 $X$同[分布](@entry_id:182848)，并且 $Y_n \xrightarrow{a.s.} Y$。这意味着任何关于[依分布收敛](@entry_id:275544)的问题都可以转化为一个（可能在不同空间上的）[几乎必然收敛](@entry_id:265812)的问题 [@problem_id:2987749]。这种“耦合”构造非常有用。例如，利用[分位数函数](@entry_id:271351)（CDF的[广义逆](@entry_id:140762)）和单个[均匀分布](@entry_id:194597)[随机变量](@entry_id:195330) $U \sim \mathcal{U}(0,1)$，可以构造 $Y_n = F_{X_n}^{-1}(U)$ 和 $Y = F_X^{-1}(U)$，从而将[依分布收敛](@entry_id:275544)转化为[几乎必然收敛](@entry_id:265812)，进而可以使用[Lebesgue控制收敛定理](@entry_id:158548)等工具来计算期望的极限 [@problem_id:2987749]。

### [随机过程](@entry_id:159502)的收敛

对于[随机过程](@entry_id:159502)，我们关注的是作为函数（或路径）的随机元素的收敛性。这需要将收敛的概念推广到[函数空间](@entry_id:143478)。对于随机微分方程而言，最相关的空间是**càdlàg[函数空间](@entry_id:143478)** $D([0,T];\mathbb{R}^d)$，即在 $[0,T]$ 上右连续且有[左极限](@entry_id:139055)的函数空间。

#### Skorokhod $J_1$ 拓扑

直接在 $D([0,T])$ 上使用[上确界范数](@entry_id:145717)（uniform norm）作为度量是有问题的。考虑一个[跳跃过程](@entry_id:180953)，如果其跳跃时间有微小的[抖动](@entry_id:200248)，那么两条路径在[上确界范数](@entry_id:145717)下的距离可能会很大，即使它们在视觉上非常接近。

**Skorokhod $J_1$ 拓扑**通过允许对时间轴进行微小的[非线性](@entry_id:637147)“扭曲”来解决这个问题。两条路径 $x, y \in D([0,T])$ 之间的 $J_1$ 距离 $d_{J_1}(x,y)$ 定义为：
$$
d_{J_1}(x,y) = \inf_{\lambda \in \Lambda} \max\left\{ \sup_{t \in [0,T]} |\lambda(t) - t|, \sup_{t \in [0,T]} |x(t) - y(\lambda(t))| \right\}
$$
其中 $\Lambda$ 是从 $[0,T]$到自身的严格递增[连续双射](@entry_id:198258)（即时间扭曲函数）的集合 [@problem_id:2994139] [@problem_id:2987739]。这个度量寻找一个最佳的时间扭曲 $\lambda$，使得扭曲后的函数 $y \circ \lambda$ 与 $x$ 在[上确界范数](@entry_id:145717)下的距离和扭曲本身的幅度都尽可能小。

例如，考虑函数 $x(t) = \mathbf{1}_{\{t \ge t_0\}}$ 和 $x_n(t) = \mathbf{1}_{\{t \ge t_0+1/n\}}$。它们的[上确界](@entry_id:140512)距离为1。但在Skorokhod度量下，我们可以构造一个时间扭曲函数 $\lambda_n$ 将 $t_0$ 映射到 $t_0+1/n$，从而使 $x_n(\lambda_n(t))$ 与 $x(t)$ 完全重合。这个 $\lambda_n$ 与[恒等函数](@entry_id:152136) $t \mapsto t$ 的偏差可以做到与 $1/n$同阶。因此，$d_{J_1}(x_n, x) \to 0$ [@problem_id:2987739]。

然而，需要注意的是，样本路径的[逐点收敛](@entry_id:145914)并不足以保证Skorokhod收敛。例如，序列 $f_n(t) = \mathbf{1}_{[1-1/n, 1)}(t)$ 在 $[0,1]$ 上逐点收敛于零函数，但在 $J_1$ 拓扑下，它与零函数的距离恒为1，不收敛 [@problem_id:2994139]。

#### 函数空间中的弱收敛

有了Skorokhod度量，我们可以定义[随机过程](@entry_id:159502)的各种[收敛模式](@entry_id:189917)。对过程 $\{X^n\}$ 和 $X$，[几乎必然收敛](@entry_id:265812)和[依概率收敛](@entry_id:145927)分别意味着 $d_{J_1}(X^n, X)$ 几乎必然或依概率趋于零。

最重要的概念是**[弱收敛](@entry_id:146650)**，$X^n \Rightarrow X$。根据Prohorov定理，在Polish空间（如赋予了 $d_{J_1}$ 度量的 $D([0,T])$ 空间）上，弱收敛等价于两个条件 [@problem_id:2994139]：
1.  **[有限维分布](@entry_id:197042)收敛 (FDD Convergence)**：对于任意有限的时间点集合 $\{t_1, \dots, t_k\} \subset [0,T]$，随机向量 $(X^n_{t_1}, \dots, X^n_{t_k})$ [依分布收敛](@entry_id:275544)到 $(X_{t_1}, \dots, X_{t_k})$。
2.  **紧性 (Tightness)**：序列 $\{X^n\}$ 的[分布](@entry_id:182848)是紧的。直观上，这意味着过程的样本路径不会“太野”或“逃逸到无穷”。紧性保证了没有概率质量在函数空间中“丢失”。

仅有[有限维分布](@entry_id:197042)收敛是**不足以**保证[弱收敛](@entry_id:146650)的，紧性条件不可或缺 [@problem_id:2994139] [@problem_id:2987739]。

### 深入探讨：[稳定收敛](@entry_id:199422)

在许多随机[微分方程的应用](@entry_id:176360)中，一个序列的极限本身可能是一个[随机变量](@entry_id:195330)，并且其[分布](@entry_id:182848)可能依赖于我们已知的某些信息。**[稳定收敛](@entry_id:199422) (Stable Convergence)** 正是为此而设计的概念，它比[依分布收敛](@entry_id:275544)更精细。

**定义 2.5 ([稳定收敛](@entry_id:199422))**：设 $\mathcal{G} \subseteq \mathcal{F}$ 是一个子$\sigma$-代数，代表已知信息。序列 $\{X_n\}$ **关于 $\mathcal{G}$ 稳定收斂**到 $X$，记作 $X_n \xrightarrow{st(\mathcal{G})} X$，如果对于任意有界的$\mathcal{G}$-可测[随机变量](@entry_id:195330) $Z$ 和任意有界[连续函数](@entry_id:137361) $f$，都有：
$$
\mathbb{E}[Z f(X_n)] \to \mathbb{E}[Z f(X)]
$$
取 $Z=1$ 可知，[稳定收敛](@entry_id:199422)蕴含[依分布收敛](@entry_id:275544)。但它的要求更高：它要求 $X_n$ 和任意的 $\mathcal{G}$-可测变量的[联合分布](@entry_id:263960)都收敛。一个等价的表述是，对于任意有界的 $\mathcal{G}$-可测变量 $Z$，二元组 $(X_n, Z)$ [依分布收敛](@entry_id:275544)到 $(X, Z)$ [@problem_id:2987754]。

[稳定收敛](@entry_id:199422)的典型应用是混合正态[极限定理](@entry_id:188579)。例如，如果 $X_n = \frac{1}{\sqrt{n}} \sum_{k=1}^n \sigma(Y) \eta_k$，其中 $Y$ 是 $\mathcal{G}$-可测的，$\eta_k$ 是独立于 $\mathcal{G}$ 的i.i.d. 标准[随机变量](@entry_id:195330)，那么 $X_n$ [稳定收敛](@entry_id:199422)到 $\sigma(Y)Z$，其中 $Z \sim \mathcal{N}(0,1)$ 且独立于 $\mathcal{G}$。这里的极限是一个“混合”[正态分布](@entry_id:154414)，其[方差](@entry_id:200758)是随机的。这在[随机波动率模型](@entry_id:142734)中非常常见 [@problem_id:2987754]。

需要强调的是，[稳定收敛](@entry_id:199422)并不比[依概率收敛](@entry_id:145927)更强。一个序列可以[稳定收敛](@entry_id:199422)但完全不[依概率收敛](@entry_id:145927) [@problem_id:2987754]。[稳定收敛](@entry_id:199422)的真正威力在于它在[依分布收敛](@entry_id:275544)的框架内保留了与背景信息 $\mathcal{G}$ 的渐近相关性结构。