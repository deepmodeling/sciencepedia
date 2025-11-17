## 引言
布朗运动，作为描述自然界和金融市场中随机现象的基石模型，其路径行为蕴含着丰富的信息。然而，仅仅了解其在某个特定时刻的位置（即边缘[分布](@entry_id:182848)）是不够的。在许多实际问题中，我们更关心的是其历史极值——例如，在一段时间内，股价曾达到的最高点，或[污染物扩散](@entry_id:195534)达到的最大范围。这些路径依赖的量无法直接从布朗运动的简单性质中得出，从而构成了一个核心的知识挑战：如何精确地刻画一个连续[随机过程](@entry_id:159502)的运行最大值的[概率分布](@entry_id:146404)？

本文旨在系统性地解决这一问题。我们将深入探讨[标准布朗运动](@entry_id:197332)最大值的[分布理论](@entry_id:186499)，揭示其背后优美的数学结构和强大的应用价值。读者将通过本文学习到：

在“原理与机制”一章中，我们将介绍强大的**[反射原理](@entry_id:148504)**，并利用它从布朗运动的[基本对称性](@entry_id:161256)出发，一步步推导出其最大值的[累积分布函数](@entry_id:143135)（CDF）、概率密度函数（PDF）和[期望值](@entry_id:153208)。我们还将揭示一个令人惊讶的[分布](@entry_id:182848)等价关系，并讨论[反射原理](@entry_id:148504)成立的关键前提。

在“应用与跨学科联系”一章中，我们将展示该理论如何跨越学科界限，应用于[金融工程](@entry_id:136943)中的[障碍期权](@entry_id:264959)定价、[材料科学](@entry_id:152226)中的可靠性评估，以及如何通过[不变性原理](@entry_id:199405)连接离散的[随机游走](@entry_id:142620)和连续的布朗运动。

最后，在“动手实践”部分，我们提供了一系列精心设计的问题，旨在引导读者将理论知识付诸实践，加深对核心概念的理解。

现在，让我们从布朗运动的基本特性出发，正式进入“原理与机制”的探索。

## 原理与机制

本章旨在深入探讨[标准布朗运动](@entry_id:197332)的运行最大值的[分布](@entry_id:182848)及其相关性质。我们将从布朗运动的基本特性出发，系统地建立描述其最大值行为的数学框架。核心工具是**[反射原理](@entry_id:148504)**（reflection principle），这是一个强大而直观的工具，它巧妙地将最大值的概率问题与布朗运动自身在某个时间点的边缘[分布](@entry_id:182848)联系起来。我们将推导最大值的累积分布函数（CDF）、[概率密度函数](@entry_id:140610)（PDF）和期望，并揭示一个令人惊讶的[分布](@entry_id:182848)[等价关系](@entry_id:138275)。最后，我们将讨论一些更深入的性质，例如马尔可夫性，并阐明[反射原理](@entry_id:148504)成立的关键前提。

### 布朗运动的基本特性与最大值的非负性

让我们从[标准布朗运动](@entry_id:197332) $(B_t)_{t \ge 0}$ 的两个基本定义属性开始：

1.  初始状态：$B_0 = 0$，几乎必然成立。
2.  路径连续性：样本路径 $t \mapsto B_t$ 是时间的[连续函数](@entry_id:137361)，[几乎必然](@entry_id:262518)成立。

这两个看似简单的属性直接导出了关于其**运行最大值**（running maximum）$M_t = \sup_{0 \le s \le t} B_s$ 的一个根本结论。根据上确界的定义，$M_t$ 必须大于或等于其定义域内任意一点的函数值。由于时间点 $s=0$ 包含在区间 $[0, t]$ 中，我们必然有 $M_t \ge B_0$。因为 $B_0=0$ [几乎必然](@entry_id:262518)成立，所以 $M_t \ge 0$ 也[几乎必然](@entry_id:262518)成立。这意味着，布朗运动的运行最大值是一个非负[随机变量](@entry_id:195330)。因此，对于任何负数 $a  0$，事件 $\{M_t \le a\}$ 是不可能发生的，其概率为零，即 $\mathbb{P}(M_t \le a) = 0$ [@problem_id:3049932]。这个结论的依据是路径的连续性和起始点，它构成了我们后续分析的基石。

另一个关键属性是布朗运动的**对称性**。对于任意固定的 $t>0$，$B_t$ 是一个均值为 $0$、[方差](@entry_id:200758)为 $t$ 的正态[随机变量](@entry_id:195330)，记为 $B_t \sim \mathcal{N}(0, t)$。一个均值为零的[正态分布](@entry_id:154414)是关于[原点对称](@entry_id:172995)的。这意味着[随机变量](@entry_id:195330) $B_t$ 和 $-B_t$ 具有完全相同的[分布](@entry_id:182848)，我们记为 $B_t \stackrel{d}{=} -B_t$。这是因为若 $B_t \sim \mathcal{N}(0, t)$，则 $-B_t \sim \mathcal{N}(-1 \cdot 0, (-1)^2 t) = \mathcal{N}(0, t)$。这个对称性对于任意 $t>0$ 都成立，而不仅仅是当[方差](@entry_id:200758)为1时 [@problem_id:3049908]。该对称性的一个直接推论是，对于任意 $a \ge 0$，事件 $\{B_t \ge a\}$ 和 $\{B_t \le -a\}$ 的概率是相等的：
$$ \mathbb{P}(B_t \ge a) = \mathbb{P}(-B_t \ge a) = \mathbb{P}(B_t \le -a) $$
这个性质在后续推导中将扮演重要角色。

### [反射原理](@entry_id:148504)

[反射原理](@entry_id:148504)是连接布朗运动最大值[分布](@entry_id:182848)和其自身边缘[分布](@entry_id:182848)的桥梁。这个原理的深层根基是布朗运动的**强马尔可夫性**（Strong Markov property）以及其增量的对称性。

#### [反射原理](@entry_id:148504)的一般形式

让我们首先考虑一个更具一般性的问题。对于给定的水平 $a \ge 0$ 和 $t>0$，我们关心的是布朗运动在时间 $t$ 之前曾达到或超过水平 $a$，并且在时间 $t$ 最终处于某个值 $x \le a$ 以下的联合概率。这个事件可以写作 $E_x = \{\sup_{0 \le s \le t} B_s \ge a, B_t \le x\}$。

[反射原理](@entry_id:148504)指出，这个事件的概率等于布朗运动在时间 $t$ 处于一个“反射”水平之上的概率。具体来说，对于任意 $x \le a$，有如下恒等式 [@problem_id:3049931]：
$$ \mathbb{P}\left(\sup_{0\le s\le t} B_s\ge a, B_t\le x\right) = \mathbb{P}\left(B_t\ge 2a-x\right) $$
这个结果可以通过以下直观方式理解：考虑一条满足 $M_t \ge a$ 和 $B_t \le x$ 的路径。设 $\tau_a = \inf\{s \ge 0: B_s = a\}$ 为首次到达水平 $a$ 的时间。由于 $M_t \ge a$，这样的时间 $\tau_a \le t$ 存在。现在，我们将路径在 $\tau_a$ 之后的部分关于水平线 $y=a$ 进行“反射”。新的路径在 $s > \tau_a$ 时的值为 $B'_s = a - (B_s - a) = 2a - B_s$。由于布朗运动在 $\tau_a$ 之后的增量 $(B_s - B_{\tau_a})_{s \ge \tau_a}$ 是对称的，原始路径和反射后的路径具有相同的概率测度。原始路径的终点是 $B_t \le x$，而反射路径的终点是 $B'_t = 2a - B_t \ge 2a-x$。由于 $x \le a$，我们有 $2a-x \ge a$。一条终点在 $2a-x$ 或其上方的路径，必然也曾达到过水平 $a$。因此，这个反射过程建立了一个从事件 $\{\tau_a \le t, B_t \le x\}$ 到事件 $\{B_t \ge 2a-x\}$ 的[概率测度](@entry_id:190821)保持的映射。

#### [反射原理](@entry_id:148504)的简化形式

在许多应用中，我们更关心的是最大值超过某个水平的总概率，即 $\mathbb{P}(M_t \ge a)$。这个概率可以通过对上述一般形式进行积分得到，但也可以通过一个更直接的论证来推导 [@problem_id:3049928]。

事件 $\{M_t \ge a\}$ 可以分解为两个[互斥事件](@entry_id:265118)的并集（忽略概率为零的边界情况）：路径在时间 $t$ 结束时高于 $a$，或低于 $a$。
$$ \mathbb{P}(M_t \ge a) = \mathbb{P}(M_t \ge a, B_t > a) + \mathbb{P}(M_t \ge a, B_t  a) $$
首先，如果 $B_t > a$，那么 $M_t$ 必然大于 $a$。所以事件 $\{M_t \ge a, B_t > a\}$ 就等同于 $\{B_t > a\}$。
其次，根据[反射原理](@entry_id:148504)的逻辑，路径达到 $a$ 后最终低于 $a$ 的概率，等于路径达到 $a$ 后最终高于 $a$ 的概率。因此，$\mathbb{P}(M_t \ge a, B_t  a) = \mathbb{P}(M_t \ge a, B_t > a)$。
结合起来，我们得到：
$$ \mathbb{P}(M_t \ge a) = \mathbb{P}(B_t > a) + \mathbb{P}(B_t > a) = 2 \mathbb{P}(B_t > a) $$
由于 $B_t$ 是一个[连续随机变量](@entry_id:166541)，$\mathbb{P}(B_t > a) = \mathbb{P}(B_t \ge a)$。因此，我们得到了[反射原理](@entry_id:148504)最常用的形式 [@problem_id:3049908]：
$$ \mathbb{P}(M_t \ge a) = 2 \mathbb{P}(B_t \ge a) \quad (\text{for } a \ge 0) $$
这个简洁的公式表明，[布朗运动的最大值](@entry_id:263793)超过 $a$ 的概率，恰好是其终点值超过 $a$ 的概率的两倍。这个令人惊讶的“因子2”是布朗运动理论中的一个标志性结果。

### 最大值的[分布](@entry_id:182848)

利用[反射原理](@entry_id:148504)，我们现在可以精确地刻画 $M_t$ 的[概率分布](@entry_id:146404)。

#### [累积分布函数 (CDF)](@entry_id:264700)

我们想要计算 $M_t$ 的CDF，$F_{M_t}(a) = \mathbb{P}(M_t \le a)$。
对于 $a  0$，我们已经知道 $\mathbb{P}(M_t \le a)=0$。
对于 $a \ge 0$，我们可以利用[互补事件](@entry_id:271719)：
$$ \mathbb{P}(M_t \le a) = 1 - \mathbb{P}(M_t > a) = 1 - \mathbb{P}(M_t \ge a) $$
将[反射原理](@entry_id:148504)的结果 $\mathbb{P}(M_t \ge a) = 2 \mathbb{P}(B_t \ge a)$ 代入，得到：
$$ \mathbb{P}(M_t \le a) = 1 - 2 \mathbb{P}(B_t \ge a) $$
为了得到一个具体的表达式，我们使用 $B_t \sim \mathcal{N}(0, t)$ 的事实。将其[标准化](@entry_id:637219)，我们得到 $\frac{B_t}{\sqrt{t}} \sim \mathcal{N}(0, 1)$。令 $\Phi(z)$ 表示[标准正态分布](@entry_id:184509)的CDF，即 $\Phi(z) = \mathbb{P}(\mathcal{N}(0,1) \le z)$。
$$ \mathbb{P}(B_t \ge a) = \mathbb{P}\left(\frac{B_t}{\sqrt{t}} \ge \frac{a}{\sqrt{t}}\right) = 1 - \Phi\left(\frac{a}{\sqrt{t}}\right) $$
将此式代回，我们得到 $M_t$ 的CDF [@problem_id:3049911] [@problem_id:3049954]：
$$ \mathbb{P}(M_t \le a) = 1 - 2\left(1 - \Phi\left(\frac{a}{\sqrt{t}}\right)\right) = 2\Phi\left(\frac{a}{\sqrt{t}}\right) - 1, \quad \text{for } a \ge 0 $$
相应的，我们也可以直接得到[尾概率](@entry_id:266795)的表达式 [@problem_id:3049930]：
$$ \mathbb{P}(M_t \ge a) = 2\left(1 - \Phi\left(\frac{a}{\sqrt{t}}\right)\right) $$
我们可以检验这个公式的极限行为。当 $a \to 0^+$ 时，$\frac{a}{\sqrt{t}} \to 0$，而 $\Phi(0) = 0.5$。所以 $\mathbb{P}(M_t \ge a) \to 2(1 - 0.5) = 1$，这与 $M_t \ge 0$ [几乎必然](@entry_id:262518)成立的事实相符。当 $a \to \infty$ 时，$\frac{a}{\sqrt{t}} \to \infty$，而 $\Phi(z) \to 1$。所以 $\mathbb{P}(M_t \ge a) \to 2(1 - 1) = 0$，这说明布朗运动达到任意大的水平都是小概率事件 [@problem_id:3049930]。

#### [概率密度函数](@entry_id:140610) (PDF)

通过对CDF求导，我们可以得到 $M_t$ 的PDF $f_{M_t}(a)$。对于 $a>0$：
$$ f_{M_t}(a) = \frac{d}{da} \left( 2\Phi\left(\frac{a}{\sqrt{t}}\right) - 1 \right) = 2 \frac{d}{da}\Phi\left(\frac{a}{\sqrt{t}}\right) $$
利用链式法则以及 $\frac{d}{dz}\Phi(z) = \varphi(z)$（其中 $\varphi(z) = \frac{1}{\sqrt{2\pi}} \exp(-z^2/2)$ 是标准正态PDF），我们得到 [@problem_id:3049911]：
$$ f_{M_t}(a) = 2 \varphi\left(\frac{a}{\sqrt{t}}\right) \cdot \frac{1}{\sqrt{t}} = \frac{2}{\sqrt{2\pi t}} \exp\left(-\frac{a^2}{2t}\right), \quad \text{for } a \ge 0 $$
这个[分布](@entry_id:182848)被称为**折叠[正态分布](@entry_id:154414)**（folded normal distribution）。它是一个均值为0、[标准差](@entry_id:153618)为 $\sqrt{t}$ 的[正态分布](@entry_id:154414)，将其负半轴部分翻折到正半轴上得到的[分布](@entry_id:182848)。

### 关键性质与[分布](@entry_id:182848)等价

#### 期望

利用 $M_t$ 的PDF，我们可以计算其[期望值](@entry_id:153208) $\mathbb{E}[M_t]$：
$$ \mathbb{E}[M_t] = \int_0^\infty a \cdot f_{M_t}(a) da = \int_0^\infty a \cdot \frac{2}{\sqrt{2\pi t}} \exp\left(-\frac{a^2}{2t}\right) da $$
通过变量代换 $u = a^2/(2t)$，可以算出这个积分 [@problem_id:3049911] [@problem_id:3049954]：
$$ \mathbb{E}[M_t] = \sqrt{\frac{2t}{\pi}} $$
[期望值](@entry_id:153208)与 $\sqrt{t}$ 成正比，这与布朗运动的[扩散](@entry_id:141445)特性是一致的。

#### [标度不变性](@entry_id:180291)

布朗运动具有一个重要的**标度不变性**（scaling property）：对于任何常数 $c>0$，过程 $X_t = \frac{1}{\sqrt{c}} B_{ct}$ 在[分布](@entry_id:182848)上与 $B_t$ 完全相同。运行最大值过程也继承了这一性质。我们可以证明 [@problem_id:3049911]：
$$ \frac{M_{ct}}{\sqrt{c}} = \frac{1}{\sqrt{c}} \sup_{0 \le s \le ct} B_s = \sup_{0 \le s \le ct} \left(\frac{B_s}{\sqrt{c}}\right) $$
令 $u = s/c$，则上式变为：
$$ \sup_{0 \le u \le t} \left(\frac{B_{cu}}{\sqrt{c}}\right) = \sup_{0 \le u \le t} X_u $$
由于 $X_u$ 是一个标准布朗运动，其在 $[0, t]$ 上的最大值与 $B_u$ 在 $[0, t]$ 上的最大值 $M_t$ 具有相同的[分布](@entry_id:182848)。因此，我们得到 $M_{ct}/\sqrt{c} \stackrel{d}{=} M_t$。

#### 与[绝对值](@entry_id:147688)的[分布](@entry_id:182848)等价关系

现在我们来揭示一个令人瞩目的结果：运行最大值 $M_t$ 与布朗运动在时间 $t$ 的**[绝对值](@entry_id:147688)** $|B_t|$ 具有完全相同的[分布](@entry_id:182848)，即 $M_t \stackrel{d}{=} |B_t|$。

要证明这一点，我们只需比较它们的CDF。我们已经推导了 $M_t$ 的CDF。现在我们来推导 $|B_t|$ 的CDF，$F_{|B_t|}(a) = \mathbb{P}(|B_t| \le a)$。
对于 $a  0$，显然 $F_{|B_t|}(a) = 0$。
对于 $a \ge 0$，我们有：
$$ \mathbb{P}(|B_t| \le a) = \mathbb{P}(-a \le B_t \le a) = \mathbb{P}(B_t \le a) - \mathbb{P}(B_t \le -a) $$
利用 $B_t$ 的对称性 $\mathbb{P}(B_t \le -a) = \mathbb{P}(B_t \ge a) = 1 - \mathbb{P}(B_t \le a)$，我们得到：
$$ \mathbb{P}(|B_t| \le a) = \mathbb{P}(B_t \le a) - (1 - \mathbb{P}(B_t \le a)) = 2\mathbb{P}(B_t \le a) - 1 $$
将 $\mathbb{P}(B_t \le a) = \Phi(a/\sqrt{t})$ 代入，得到：
$$ F_{|B_t|}(a) = 2\Phi\left(\frac{a}{\sqrt{t}}\right) - 1, \quad \text{for } a \ge 0 $$
这与我们之前为 $M_t$ 推导出的CDF完全相同 [@problem_id:3049956] [@problem_id:3049954]。因此，尽管 $M_t$ 和 $|B_t|$ 是两个截然不同的[随机变量](@entry_id:195330)（在同一条样本路径上，它们的值通常不同），但它们的[概率分布](@entry_id:146404)是完全一样的。这个结论也为计算 $\mathbb{E}[M_t]$ 提供了另一条途径，即计算 $\mathbb{E}[|B_t|]$。

### 深入探讨：马尔可夫性与[反射原理](@entry_id:148504)的[适用范围](@entry_id:636189)

#### 运行最大值的马尔可夫性

一个[随机过程](@entry_id:159502)被称为**[马尔可夫过程](@entry_id:160396)**（Markov process），如果其未来状态的[条件概率分布](@entry_id:163069)只依赖于当前状态，而与过去的历史无关。一个自然的问题是：运行最大值过程 $(M_t)_{t \ge 0}$ 是否是[马尔可夫过程](@entry_id:160396)？

答案是否定的。为了预测 $M_{t+h}$ ($h>0$) 的行为，仅仅知道 $M_t = m$ 是不够的。我们还需要知道当前布朗运动的值 $B_t=b$。直观地说，如果 $B_t$ 非常接近其历史最大值 $m$（即 $m-b$ 很小），那么在接下来的短暂时间内，布朗运动很有可能创造一个新的最大值。相反，如果 $B_t$ 远低于 $m$（即 $m-b$ 很大），那么它需要更多的时间和更有利的波动才能超过 $m$。

我们可以精确地量化这一点。未来最大值超过当前最大值 $m$ 的概率，以 $M_t=m$ 和 $B_t=b$ 为条件，为：
$$ \mathbb{P}(M_{t+h} > m | M_t=m, B_t=b) = \mathbb{P}(\sup_{0 \le s \le h} B_{t+s} > m | B_t=b) $$
利用布朗运动的[独立增量](@entry_id:262163)性质，这等价于一个从 $b$ 开始的布朗运动在 $h$ 时间内最大值超过 $m$ 的问题，也即一个从0开始的布朗运动最大值超过 $m-b$ 的问题。应用[反射原理](@entry_id:148504)，我们得到 [@problem_id:3049952]：
$$ \mathbb{P}(M_{t+h} > m | M_t=m, B_t=b) = 2 \left(1 - \Phi\left(\frac{m-b}{\sqrt{h}}\right)\right) $$
这个概率明显依赖于“缺口” $m-b$，而不仅仅是 $m$。因此，$(M_t)_{t \ge 0}$ 不是一个[马尔可夫过程](@entry_id:160396)。然而，由 $B_t$ 和 $M_t$ 构成的二维过程 $((B_t, M_t))_{t \ge 0}$ 是一个[马尔可夫过程](@entry_id:160396)，因为给定 $(B_t, M_t)$，其未来的演化就完全确定了（在概率意义上）[@problem_id:3049952]。

#### [反射原理](@entry_id:148504)的独特性

最后，值得思考的是，为什么[反射原理](@entry_id:148504)对布朗运动有效？它是否适用于更一般的[随机过程](@entry_id:159502)，比如其他连续的**[鞅](@entry_id:267779)**（martingale）？

答案是否定的。[反射原理](@entry_id:148504)本质上依赖于布朗运动的两个独特属性的结合：**[独立增量](@entry_id:262163)**和**对称的增量[分布](@entry_id:182848)**。当我们在首次到达时间 $\tau_a$ 应用强马尔可夫性时，我们得到的“新”过程 $(B_{\tau_a+s} - B_{\tau_a})_{s \ge 0}$ 不仅是一个布朗运动，而且它与 $\tau_a$ 之前的历史**独立**。此外，这个新过程的[分布](@entry_id:182848)是**对称**的，这使得向上和向下运动的概率相等，从而允许“反射”。

对于一个一般形式的[连续鞅](@entry_id:185466)，例如 $X_t = \int_0^t \sigma_s dB_s$，其中波动率 $\sigma_s$ 自身可能依赖于路径历史，这两个条件通常都不满足。在击中某个水平 $a$ 之后，未来的过程 $X_{\tau_a+s}-X_{\tau_a}$ 的动态（即其波动率）可能仍然取决于它到达 $a$ 的方式。它的增量[分布](@entry_id:182848)也不再保证是对称的。例如，我们可以构造一个[鞅](@entry_id:267779)，当其值变大时波动率也随之变大。这样的过程在达到一个高水平后，其向上和向下波动的可能性就不再对称，反射论证也就失效了 [@problem_id:3049916]。因此，[反射原理](@entry_id:148504)及其推论，包括 $M_t \stackrel{d}{=} |B_t|$，是布朗运动（以及更广泛的具有对称[独立增量](@entry_id:262163)的 Lévy 过程）的标志性特征，而非普遍性质。