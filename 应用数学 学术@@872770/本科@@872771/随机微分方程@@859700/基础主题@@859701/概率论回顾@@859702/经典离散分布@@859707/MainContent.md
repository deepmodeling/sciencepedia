## 引言
经典[离散分布](@entry_id:193344)，如二项分布和[泊松分布](@entry_id:147769)，是概率论和统计学的基石。然而，它们真正的威力在于其作为理解和构建更复杂随机现象（尤其是在随机微分方程中至关重要的[跳跃过程](@entry_id:180953)）的出发点。许多初学者熟悉这些[分布](@entry_id:182848)的静态定义，但常常在将这些静态概念应用于动态、[连续时间过程](@entry_id:274437)时遇到困难。本文旨在填补这一知识鸿沟，系统性地展示这些基础[分布](@entry_id:182848)如何演化为强大的[随机过程模型](@entry_id:272197)。

在接下来的章节中，我们将踏上一段从基础到前沿的旅程。首先，在“原理与机制”一章中，我们将深入剖析[二项分布](@entry_id:141181)和泊松分布的数学构造，探讨它们之间的深刻联系，并引入[生成函数](@entry_id:146702)作为统一的分析工具，最终将这些概念无缝过渡到泊松过程及其推广。接着，在“应用与交叉学科联系”一章，我们将探索这些模型在[随机微分方程](@entry_id:146618)数值模拟、动态系统[稳态分析](@entry_id:271474)、统计推断和信息论等领域的实际应用，展示其广泛的实用价值。最后，“动手实践”部分将提供一系列精心设计的问题，引导您将理论知识转化为解决具体问题的实践能力。

## 原理与机制

本章旨在深入探讨在[随机过程](@entry_id:159502)理论中占据核心地位的若干经典[离散分布](@entry_id:193344)。这些[分布](@entry_id:182848)不仅是概率论的基石，更是构建和理解随机微分方程中[跳跃过程](@entry_id:180953)的出发点。我们将从最基本的[伯努利试验](@entry_id:268355)出发，系统地构建[二项分布](@entry_id:141181)和泊松分布，并阐明它们之间的深刻联系。随后，我们将引入生成函数这一强有力的分析工具，并将其应用于从静态[分布](@entry_id:182848)向动态过程的过渡——即泊松过程。最后，本章将探讨泊松过程的若干重要推广，包括[复合泊松过程](@entry_id:140283)和泊松随机测度，这些都是在金融、物理和工程领域中对跳跃-[扩散](@entry_id:141445)现象进行建模不可或缺的组成部分。

### [二项分布](@entry_id:141181)：基于计数的基石

许多随机现象的建模始于对一系列基本[二元结果](@entry_id:173636)的计数。最简单的此类模型是**伯努利试验**（Bernoulli trial），即一个只有两种可能结果（通常称为“成功”与“失败”）的单次随机实验。若以[随机变量](@entry_id:195330) $Y$ 表示其结果，并令成功为 $1$，失败为 $0$，其[概率分布](@entry_id:146404)为 $P(Y=1)=p$ 和 $P(Y=0)=1-p$，其中 $p \in (0,1)$ 称为成功概率。

当我们将 $n$ 次**[独立同分布](@entry_id:169067)**（independent and identically distributed, i.i.d.）的[伯努利试验](@entry_id:268355)[串联](@entry_id:141009)起来时，我们便进入了[二项分布](@entry_id:141181)的领域。设 $Y_1, \dots, Y_n$ 是代表这 $n$ 次试验结果的[独立同分布](@entry_id:169067)伯努利[随机变量](@entry_id:195330)。我们最常关心的问题是，在这次系列试验中，总共出现了多少次成功？这个总成功次数由[随机变量](@entry_id:195330) $X = \sum_{i=1}^n Y_i$ 描述，其[分布](@entry_id:182848)即为**二项分布**（Binomial Distribution），记作 $X \sim \mathrm{Bin}(n,p)$。[@problem_id:3044299]

要推导其**[概率质量函数](@entry_id:265484)**（Probability Mass Function, PMF），即计算事件 $\{X=k\}$（恰好发生 $k$ 次成功）的概率，我们可以采用组合学的方法。[@problem_id:3044344] 首先，考虑一个包含 $k$ 次成功和 $n-k$ 次失败的特定序列，例如前 $k$ 次成功而后 $n-k$ 次失败。由于各次试验相互独立，该特定序列发生的概率是各次试验概率的乘积：
$$ \underbrace{p \cdot p \cdots p}_{k \text{ 次}} \cdot \underbrace{(1-p) \cdot (1-p) \cdots (1-p)}_{n-k \text{ 次}} = p^k (1-p)^{n-k} $$
这个概率值对应于任意一个恰有 $k$ 次成功和 $n-k$ 次失败的序列，这正是因为试验是同[分布](@entry_id:182848)的。

接下来，我们需要计算总共有多少个这样的不同序列。这等价于在 $n$ 个位置中选择 $k$ 个位置用于安放“成功”，其数目由二项式系数给出：
$$ \binom{n}{k} = \frac{n!}{k!(n-k)!} $$
由于这些序列是[互斥事件](@entry_id:265118)，总概率是所有这些序列的概率之和。因此，[二项分布](@entry_id:141181)的[概率质量函数](@entry_id:265484)为：
$$ P(X=k) = \binom{n}{k} p^k (1-p)^{n-k}, \quad k \in \{0, 1, \dots, n\} $$
这一公式的结构清晰地反映了其[组合学](@entry_id:144343)来源：$\binom{n}{k}$ 是组合因子，计算路径数量；$p^k$ 是成功的概率因子；$(1-p)^{n-k}$ 是失败的概率因子。[@problem_id:3044344]

推导[二项分布的均值和方差](@entry_id:167195)，直接利用 $X$ 是[独立随机变量](@entry_id:273896)之和的结构，比使用其复杂的PMF进行求和要简洁得多。利用[期望的线性](@entry_id:273513)性质：
$$ \mathbb{E}[X] = \mathbb{E}\left[\sum_{i=1}^n Y_i\right] = \sum_{i=1}^n \mathbb{E}[Y_i] $$
对于单个[伯努利试验](@entry_id:268355) $Y_i$，其期望为 $\mathbb{E}[Y_i] = 1 \cdot p + 0 \cdot (1-p) = p$。因此，
$$ \mathbb{E}[X] = \sum_{i=1}^n p = np $$
对于[独立随机变量](@entry_id:273896)之和，[方差](@entry_id:200758)也具有可加性：
$$ \mathrm{Var}(X) = \mathrm{Var}\left(\sum_{i=1}^n Y_i\right) = \sum_{i=1}^n \mathrm{Var}(Y_i) $$
单个伯努利试验的[方差](@entry_id:200758)为 $\mathrm{Var}(Y_i) = \mathbb{E}[Y_i^2] - (\mathbb{E}[Y_i])^2$。由于 $Y_i$ 只取值 $0$ 和 $1$，有 $Y_i^2 = Y_i$，所以 $\mathbb{E}[Y_i^2] = \mathbb{E}[Y_i] = p$。于是，$\mathrm{Var}(Y_i) = p - p^2 = p(1-p)$。因此，
$$ \mathrm{Var}(X) = \sum_{i=1}^n p(1-p) = np(1-p) $$
这些结果——$P(X=k) = \binom{n}{k}p^k(1-p)^{n-k}$, $\mathbb{E}[X]=np$, $\mathrm{Var}(X)=np(1-p)$——构成了对二项分布的基本描述。[@problem_id:3044299] 值得注意的是，保证每个包含 $k$ 次成功的序列具有相同概率 $p^k(1-p)^{n-k}$ 的根本原因在于试验的[独立同分布](@entry_id:169067)特性。一个更普适的条件是**可交换性**（exchangeability），即[随机变量](@entry_id:195330)序列的[联合概率分布](@entry_id:171550)在任意[置换](@entry_id:136432)下标后保持不变。[@problem_id:3044344]

### 泊松分布：[稀有事件定律](@entry_id:152495)

现在我们转向另一种重要的[离散分布](@entry_id:193344)——**泊松分布**（Poisson Distribution）。一个[随机变量](@entry_id:195330) $X$ 若服从参数为 $\lambda>0$ 的泊松分布，记作 $X \sim \mathrm{Pois}(\lambda)$，其[概率质量函数](@entry_id:265484)定义为：
$$ P(X=k) = \frac{e^{-\lambda} \lambda^k}{k!}, \quad k \in \{0, 1, 2, \dots\} $$
[泊松分布](@entry_id:147769)通常用于模拟在固定的时间、空间或体积单位内，稀有事件发生的次数。例如，在随机微分方程的语境下，它可以描述单位时间内，一个系统的跳跃次数，其中 $\lambda$ 代表平均跳跃率或强度。[@problem_id:3044275]

[泊松分布的均值和方差](@entry_id:168457)可以从其定义出发，借助指数函数的[泰勒级数展开](@entry_id:138468) $\exp(z) = \sum_{k=0}^{\infty} z^k/k!$ 进行推导。
其期望为：
$$ \mathbb{E}[X] = \sum_{k=0}^{\infty} k \cdot P(X=k) = \sum_{k=1}^{\infty} k \frac{e^{-\lambda} \lambda^k}{k!} = e^{-\lambda} \sum_{k=1}^{\infty} \frac{\lambda^k}{(k-1)!} $$
令 $j=k-1$，则：
$$ \mathbb{E}[X] = e^{-\lambda} \sum_{j=0}^{\infty} \frac{\lambda^{j+1}}{j!} = \lambda e^{-\lambda} \sum_{j=0}^{\infty} \frac{\lambda^j}{j!} = \lambda e^{-\lambda} e^{\lambda} = \lambda $$
为了计算[方差](@entry_id:200758) $\mathrm{Var}(X) = \mathbb{E}[X^2] - (\mathbb{E}[X])^2$，我们先计算二阶[阶乘矩](@entry_id:201532) $\mathbb{E}[X(X-1)]$：
$$ \mathbb{E}[X(X-1)] = \sum_{k=0}^{\infty} k(k-1) \frac{e^{-\lambda} \lambda^k}{k!} = \sum_{k=2}^{\infty} \frac{e^{-\lambda} \lambda^k}{(k-2)!} $$
令 $j=k-2$，则：
$$ \mathbb{E}[X(X-1)] = e^{-\lambda} \sum_{j=0}^{\infty} \frac{\lambda^{j+2}}{j!} = \lambda^2 e^{-\lambda} \sum_{j=0}^{\infty} \frac{\lambda^j}{j!} = \lambda^2 e^{-\lambda} e^{\lambda} = \lambda^2 $$
由于 $\mathbb{E}[X^2] = \mathbb{E}[X(X-1)] + \mathbb{E}[X] = \lambda^2 + \lambda$，[方差](@entry_id:200758)为：
$$ \mathrm{Var}(X) = (\lambda^2 + \lambda) - \lambda^2 = \lambda $$
因此，泊松分布有一个非常独特的性质：其均值和[方差](@entry_id:200758)相等，均为参数 $\lambda$。[@problem_id:3044275]

### 从[二项分布](@entry_id:141181)到[泊松分布](@entry_id:147769)的桥梁

二项分布与泊松分布之间存在着深刻而实用的联系。当二项分布的试验次数 $n$ 非常大，而单次成功概率 $p$ 非常小时，如果它们的乘积 $\lambda = np$ 保持为一个有限的常数，那么该[二项分布](@entry_id:141181)可以由一个参数为 $\lambda$ 的[泊松分布](@entry_id:147769)很好地近似。这通常被称为**小数定律**（law of small numbers）。

我们可以通过分析零事件的概率来严格地考察这种收敛关系。对于 $X \sim \mathrm{Bin}(n,p)$，事件 $\{X=0\}$ 的概率为 $P(X=0) = (1-p)^n$。在极限条件下 $n \to \infty, p \to 0$ 且 $\lambda=np$ 固定，我们有 $p=\lambda/n$。于是：
$$ P(X=0) = \left(1-\frac{\lambda}{n}\right)^n $$
这是一个著名的极限形式，其结果为 $\lim_{n\to\infty}(1-\frac{\lambda}{n})^n = e^{-\lambda}$，这恰好是 $\mathrm{Pois}(\lambda)$ [分布](@entry_id:182848)中 $k=0$ 时的概率。

为了量化这种近似的误差，我们可以推导其领先阶的渐近项。定义误差 $E(n,p) = (1-p)^n - \exp(-np)$。利用对数和[指数函数](@entry_id:161417)的[泰勒展开](@entry_id:145057)，我们可以得到在 $n \to \infty$ 时误差的领先项。具体来说，对 $\ln(1-\lambda/n)$ 进行展开：
$$ \ln\left(1 - \frac{\lambda}{n}\right) = -\frac{\lambda}{n} - \frac{\lambda^2}{2n^2} - O\left(\frac{1}{n^3}\right) $$
从而
$$ n\ln\left(1 - \frac{\lambda}{n}\right) = -\lambda - \frac{\lambda^2}{2n} - O\left(\frac{1}{n^2}\right) $$
取指数后得到：
$$ \left(1 - \frac{\lambda}{n}\right)^n = \exp\left(-\lambda - \frac{\lambda^2}{2n} + O\left(\frac{1}{n^2}\right)\right) \approx \exp(-\lambda) \left(1 - \frac{\lambda^2}{2n}\right) $$
因此，误差 $E(n,p)$ 的领先阶项为：
$$ E(n,p) \approx \exp(-\lambda) - \frac{\lambda^2 \exp(-\lambda)}{2n} - \exp(-\lambda) = -\frac{\lambda^2 \exp(-\lambda)}{2n} $$
这个结果表明，近似误差是负的（即二项概率略小于泊松概率），且随着 $n$ 的增加以 $1/n$ 的速率趋向于零。[@problem_id:3044324]

除了[渐近分析](@entry_id:160416)，我们还可以使用**[全变差距离](@entry_id:143997)**（Total Variation Distance）来度量两个[概率分布](@entry_id:146404)之间的差异。对于定义在非负整数集上的两个概率律 $\mathbb{P}$ 和 $\mathbb{Q}$，其[全变差距离](@entry_id:143997)为：
$$ d_{\mathrm{TV}}(\mathbb{P},\mathbb{Q}) = \frac{1}{2}\sum_{k=0}^{\infty}|\mathbb{P}\{k\}-\mathbb{Q}\{k\}| $$
**[勒卡姆不等式](@entry_id:635781)**（Le Cam's inequality）为[泊松近似](@entry_id:265225)提供了一个强大且非渐近的误差[上界](@entry_id:274738)。对于一系列独立的[伯努利试验](@entry_id:268355)，其成功概率分别为 $p_1, \dots, p_n$，令 $S$ 为成功总数，$\lambda = \sum p_i$，则 $S$ 的[分布](@entry_id:182848)与 $\mathrm{Pois}(\lambda)$ [分布](@entry_id:182848)之间的[全变差距离](@entry_id:143997)满足：
$$ d_{\mathrm{TV}}(\mathcal{L}(S), \mathrm{Pois}(\lambda)) \le \sum_{i=1}^{n}p_i^2 $$
在二项分布的特殊情况中，$p_i=p$ 对所有 $i$ 成立，此时 $\lambda=np$，不等式简化为：
$$ d_{\mathrm{TV}}(\mathrm{Bin}(n,p), \mathrm{Pois}(np)) \le np^2 $$
这个不等式提供了一个简单易算的[误差界](@entry_id:139888)。例如，对于 $n=800$ 和 $p=0.006$，我们有 $\lambda=4.8$，误差[上界](@entry_id:274738)为 $800 \times (0.006)^2 = 0.0288$。这表明在此参数下，两个[分布](@entry_id:182848)非常接近。该不等式的证明通常依赖于精巧的**耦合**（coupling）论证，即在同一[概率空间](@entry_id:201477)中构造两个[随机变量](@entry_id:195330)，使其分别服从目标分布，然后估计它们取值不等的概率。[@problem_id:3044300]

### 生成函数：统一的代数框架

[生成函数](@entry_id:146702)为研究[离散随机变量](@entry_id:163471)提供了一种强大的代数工具，它将整个[概率分布](@entry_id:146404)压缩到一个函数中。

**[概率生成函数](@entry_id:190573)**（Probability Generating Function, PGF）定义为 $G_X(s) = \mathbb{E}[s^X]$。对于 $X \sim \mathrm{Pois}(\lambda)$：
$$ G_X(s) = \mathbb{E}[s^X] = \sum_{k=0}^{\infty} s^k \frac{e^{-\lambda} \lambda^k}{k!} = e^{-\lambda} \sum_{k=0}^{\infty} \frac{(\lambda s)^k}{k!} = e^{-\lambda} e^{\lambda s} = \exp(\lambda(s-1)) $$
PGF的导数在 $s=1$ 处的值可以用来计算[阶乘矩](@entry_id:201532)。例如，[一阶导数](@entry_id:749425)为 $G'_X(s) = \lambda \exp(\lambda(s-1))$，在 $s=1$ 处的值为 $G'_X(1) = \lambda = \mathbb{E}[X]$。[二阶导数](@entry_id:144508)为 $G''_X(s) = \lambda^2 \exp(\lambda(s-1))$，在 $s=1$ 处的值为 $G''_X(1) = \lambda^2 = \mathbb{E}[X(X-1)]$。这提供了一种计算[高阶矩](@entry_id:266936)的系统方法。[@problem_id:3044342]

**矩生成函数**（Moment Generating Function, MGF）定义为 $M_X(t) = \mathbb{E}[e^{tX}]$。通过在 PGF 中进行[变量替换](@entry_id:141386) $s=e^t$ 即可得到 MGF。对于泊松分布，$M_X(t) = G_X(e^t) = \exp(\lambda(e^t-1))$。

**[累积量生成函数](@entry_id:748109)**（Cumulant Generating Function, CGF）定义为 $K_X(t) = \ln M_X(t)$。它之所以重要，是因为其在 $t=0$ 处的[泰勒展开](@entry_id:145057)系数是[分布](@entry_id:182848)的**[累积量](@entry_id:152982)**（cumulants）。对于[泊松分布](@entry_id:147769)：
$$ K_X(t) = \ln(\exp(\lambda(e^t-1))) = \lambda(e^t-1) $$
第一[累积量](@entry_id:152982)是均值，第二累积量是[方差](@entry_id:200758)。对 $K_X(t)$ 求导可得 $K'_X(t) = \lambda e^t$ 和 $K''_X(t) = \lambda e^t$。在 $t=0$ 处求值，得到均值为 $K'_X(0) = \lambda$，[方差](@entry_id:200758)为 $K''_X(0) = \lambda$，再次验证了[泊松分布的均值和方差](@entry_id:168457)相等。[@problem_id:3044301]

### 从静态[分布](@entry_id:182848)到动态过程：泊松过程

泊松分布是理解**泊松过程**（Poisson Process）的关键。一个速率为 $\lambda$ 的标准（或齐次）泊松过程 $\{N(t)\}_{t \ge 0}$ 是一个[计数过程](@entry_id:260664)，它描述了事件随时间累积发生的情况，并满足以下核心性质：
1.  $N(0) = 0$：过程从零开始。
2.  **[独立增量](@entry_id:262163)**：在任意不重叠的时间区间内，事件发生的次数是相互独立的[随机变量](@entry_id:195330)。
3.  **[平稳增量](@entry_id:263290)**：在任何长度为 $\Delta t$ 的时间区间内，事件发生的次数的[分布](@entry_id:182848)是相同的，只依赖于区间长度 $\Delta t$，而与区间的位置无关。
4.  对于 $0 \le s  t$，增量 $N(t) - N(s)$ 服从参数为 $\lambda(t-s)$ 的[泊松分布](@entry_id:147769)，即 $N(t)-N(s) \sim \mathrm{Pois}(\lambda(t-s))$。

[累积量生成函数](@entry_id:748109)是展示这些性质的有力工具。利用[独立增量](@entry_id:262163)性质，我们可以将 $N(t)$ 写成 $N(t) = N(s) + (N(t)-N(s))$，其中 $N(s)$ 和 $N(t)-N(s)$ 独立。对于独立变量之和，CGF具有可加性：
$$ K_{N(t)}(u) = K_{N(s)}(u) + K_{N(t)-N(s)}(u) $$
由于 $N(\tau) \sim \mathrm{Pois}(\lambda \tau)$，其CGF为 $K_{N(\tau)}(u) = \lambda \tau (e^u-1)$。代入上式可得增量的CGF：
$$ K_{N(t)-N(s)}(u) = K_{N(t)}(u) - K_{N(s)}(u) = \lambda t (e^u-1) - \lambda s (e^u-1) = \lambda(t-s)(e^u-1) $$
这个结果的形式与 $N(t-s)$ 的CGF完全相同，完美地体现了[平稳增量](@entry_id:263290)性质，而其推导过程则直接依赖于[独立增量](@entry_id:262163)性质。[@problem_id:3044301]

泊松过程的协[方差](@entry_id:200758)结构也深刻地反映了其增量特性。对于 $0 \le s \le t$，协[方差](@entry_id:200758) $\mathrm{Cov}(N(s), N(t))$ 的计算如下：
$$ \mathrm{Cov}(N(s), N(t)) = \mathbb{E}[N(s)N(t)] - \mathbb{E}[N(s)]\mathbb{E}[N(t)] $$
利用分解 $N(t) = N(s) + (N(t)-N(s))$：
$$ \mathbb{E}[N(s)N(t)] = \mathbb{E}[N(s)(N(s) + N(t)-N(s))] = \mathbb{E}[N(s)^2] + \mathbb{E}[N(s)(N(t)-N(s))] $$
由于 $N(s)$ 和增量 $N(t)-N(s)$ 独立，$\mathbb{E}[N(s)(N(t)-N(s))] = \mathbb{E}[N(s)]\mathbb{E}[N(t)-N(s)] = (\lambda s)(\lambda(t-s))$。
又因为 $\mathbb{E}[N(s)^2] = \mathrm{Var}(N(s)) + (\mathbb{E}[N(s)])^2 = \lambda s + (\lambda s)^2$。
将这些代入，我们得到：
$$ \mathbb{E}[N(s)N(t)] = (\lambda s + \lambda^2 s^2) + (\lambda^2 st - \lambda^2 s^2) = \lambda s + \lambda^2 st $$
最后，协[方差](@entry_id:200758)为：
$$ \mathrm{Cov}(N(s), N(t)) = (\lambda s + \lambda^2 st) - (\lambda s)(\lambda t) = \lambda s $$
这个简洁的结果 $\mathrm{Cov}(N(s), N(t)) = \lambda s = \lambda \min(s,t)$ 表明，过程在 $t$ 时刻的值与在较早 $s$ 时刻的值之间的协[方差](@entry_id:200758)，完全由直到 $s$ 时刻的[方差](@entry_id:200758)决定。这体现了过程的[马尔可夫性质](@entry_id:139474)：过程的未来只通过其当前状态与过去发生关联。[@problem_id:3044305]

### [随机建模](@entry_id:261612)中的推广与应用

泊松过程是构建更复杂随机模型的基础。以下是几个关键的推广。

#### [补偿泊松过程](@entry_id:182161)与[鞅](@entry_id:267779)

在[随机分析](@entry_id:188809)中，将[随机过程分解](@entry_id:637354)为可预测部分和不可预测的**[鞅](@entry_id:267779)**（martingale）部分是一种标准做法。泊松过程 $N(t)$ 的期望是 $\mathbb{E}[N(t)]=\lambda t$，这是一个确定性的、可预测的增长趋势。通过减去这个趋势，我们得到**[补偿泊松过程](@entry_id:182161)**（compensated Poisson process）：
$$ M(t) = N(t) - \lambda t $$
可以证明 $M(t)$ 是一个[鞅](@entry_id:267779)，这意味着在任何时刻 $s$，过程在未来时刻 $t  s$ 的[期望值](@entry_id:153208)等于其当前值，即 $\mathbb{E}[M(t)|\mathcal{F}_s] = M(s)$。

对于像 $M(t)$ 这样的[跳跃过程](@entry_id:180953)，其**二次变分**（quadratic variation）$[M](t)$ 捕捉了过程路径的能量或波动性，定义为跳跃大小平方和：
$$ [M](t) = \sum_{0  s \le t} (\Delta M(s))^2 $$
其中 $\Delta M(s) = M(s) - M(s-)$ 是在时刻 $s$ 的跳跃。由于 $M(t)$ 的跳跃与 $N(t)$ 完全相同，且 $N(t)$ 的跳跃大小均为 $1$，我们得到：
$$ [M](t) = \sum_{0  s \le t} (\Delta N(s))^2 = \sum_{0  s \le t, \Delta N(s)=1} 1^2 = N(t) $$
有趣的是，[补偿泊松过程](@entry_id:182161)的二次变分本身是一个[随机过程](@entry_id:159502)。与之对应的是**可预见二次变分**（predictable quadratic variation）$\langle M \rangle(t)$，它是 $[M](t)$ 的可预测补偿子，使得 $[M](t) - \langle M \rangle(t)$ 是一个鞅。对于[补偿泊松过程](@entry_id:182161)，这个补偿子恰好是它的补偿项：
$$ \langle M \rangle(t) = \lambda t $$
因此，我们有 $([M](t), \langle M \rangle(t)) = (N(t), \lambda t)$。这两个过程是理解[跳跃过程](@entry_id:180953)随机积分理论的核心。[@problem_id:3044323]

#### [复合泊松过程](@entry_id:140283)

标准泊松过程只计数事件的发生，但未描述每个事件的“大小”或“影响”。**[复合泊松过程](@entry_id:140283)**（compound Poisson process）通过为每次跳跃附加一个随机的幅度来弥补这一点。其形式为：
$$ S(t) = \sum_{i=1}^{N(t)} Y_i $$
其中 $\{N(t)\}$ 是一个速率为 $\lambda$ 的泊松过程，而 $\{Y_i\}_{i \ge 1}$ 是一系列独立同分布的[随机变量](@entry_id:195330)（代表跳跃大小），且与 $\{N(t)\}$ 过程独立。设 $Y_i$ 的均值为 $\mu$，[方差](@entry_id:200758)为 $\sigma^2$。

$S(t)$ 在任意固定时刻 $t$ 的均值和[方差](@entry_id:200758)可以通过**[全期望定律](@entry_id:265946)**和**[全方差定律](@entry_id:184705)**（或称作[Wald恒等式](@entry_id:273715)）推导。
$$ \mathbb{E}[S(t)] = \mathbb{E}[\mathbb{E}[S(t)|N(t)]] = \mathbb{E}[N(t)\mu] = \mu \mathbb{E}[N(t)] = \lambda t \mu $$
$$ \mathrm{Var}(S(t)) = \mathbb{E}[\mathrm{Var}(S(t)|N(t))] + \mathrm{Var}(\mathbb{E}[S(t)|N(t)]) = \mathbb{E}[N(t)\sigma^2] + \mathrm{Var}(N(t)\mu) $$
$$ = \sigma^2 \mathbb{E}[N(t)] + \mu^2 \mathrm{Var}(N(t)) = \sigma^2 (\lambda t) + \mu^2 (\lambda t) = \lambda t (\sigma^2 + \mu^2) $$
注意到 $\sigma^2+\mu^2 = \mathbb{E}[Y^2]$，所以[方差](@entry_id:200758)也可写成 $\lambda t \mathbb{E}[Y^2]$。这些结果是构建带有随机跳跃幅度的随机微分方程模型的基础。[@problem_id:3044328]

#### 泊松随机测度

泊松过程的最终极推广是**泊松随机测度**（Poisson Random Measure, PRM），有时也称为泊松点过程（Poisson Point Process）。它将事件的概念从一维时间线推广到更一般的空间。设 $(E, \mathcal{E})$ 是一个[可测空间](@entry_id:189701)（例如，表示所有可能的跳跃大小），$\nu$ 是其上的一个 $\sigma$-[有限测度](@entry_id:183212)，称为强度测度。

泊松随机测度 $\mu$ 是定义在乘[积空间](@entry_id:151693) $\mathbb{R}_+ \times E$ 上的一个随机整数值测度，其均值测度为 $\Lambda(dt,dz) = dt \nu(dz)$。它由以下两个核心性质完全定义 [@problem_id:3044309]：
1.  **[分布](@entry_id:182848)性质**：对任意[可测集](@entry_id:159173) $A \subset \mathbb{R}_+ \times E$，其测度 $\Lambda(A) = \int_A dt \nu(dz)$ 如果是有限的，则[随机变量](@entry_id:195330) $\mu(A)$（表示落在集合 $A$ 中的点的个数）服从[泊松分布](@entry_id:147769)，其参数为 $\Lambda(A)$。即 $\mu(A) \sim \mathrm{Pois}(\Lambda(A))$。
2.  **独立性质**：对于任意有限个互不相交的可测集 $A_1, \dots, A_n$，[随机变量](@entry_id:195330) $\mu(A_1), \dots, \mu(A_n)$ 是[相互独立](@entry_id:273670)的。

泊松随机测度是构建最一般的具有跳跃性的[随机过程](@entry_id:159502)——**[列维过程](@entry_id:266171)**（Lévy process）——的基本工具，它为随机微分方程中的跳跃项提供了最普适和最严谨的数学框架。