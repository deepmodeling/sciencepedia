## 引言
在从工程学到物理学的各个领域，我们不断遇到一些[随机信号](@keyword=random_signals|lang=zh-CN|style=Feynman)，但它们随时间表现出某种形式的统计规律性。稳定的背景嘶嘶声、电机的随机[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)或金融市场的波动可能每时每刻都看起来不可预测，但它们的整体特征——平均水平和内部节律——通常保持一致。宽平稳（WSS）过程的概念为理解和处理此类信号提供了必要的数学框架。它通过定义一种“统计同一性”的实用形式来应对分析随机性的挑战，这种形式不过于严格，却足够强大以适用于广泛的应用。本文将 WSS 过程分解为其核心组成部分。首先，我们将探讨“原理与机制”，定义支配 WSS 过程的两条简单规则，并检验[自相关函数](@keyword=autocorrelation_function|lang=zh-CN|style=Feynman)中编码的丰富信息。随后，“应用与跨学科联系”一节将展示这些理论思想如何应用于现实世界，探讨当我们对 WSS 信号进行滤波、采样和测量时会发生什么，并引入连接抽象理论与实际数据的关键概念——遍历性。

## 原理与机制

想象一下，你正在收听一个调谐在电台之间的收音机发出的稳定嘶嘶声，或者正在观察广阔无垠的大海上的波浪。如果你今天录制一段十秒钟的嘶嘶声，明天再录制一段十秒钟的嘶嘶声，这两段录音在细节上会完全不同。然而，在统计意义上，它们给人的感觉是相同的。平均响度、存在的频率范围、声音的“质感”——这些特征都没有改变。这种统计上“同一性”的直观概念，就是我们所说的**[平稳性](@keyword=stationarity|lang=zh-CN|style=Feynman)**的核心。这是一个非常有用的概念，因为它允许我们分析过程的一小部分，并对其在任何其他时间的行为做出有力的预测。

在物理学和工程学中，我们通常不需要最严格形式的平稳性。我们可以稍微放宽条件，仍然能得到一个非常强大的工具。这就引出了**宽[平稳性](@keyword=stationarity|lang=zh-CN|style=Feynman) (WSS)** 的概念，它建立在两条简单且符合常识的规则之上。如果一个[随机过程](@keyword=random_process|lang=zh-CN|style=Feynman)的均值和[自相关](@keyword=autocorrelation|lang=zh-CN|style=Feynman)满足这些条件，那么它就是 WSS 过程。让我们逐一来看。

### 同一性的本质：定义[平稳性](@keyword=stationarity|lang=zh-CN|style=Feynman)

**规则 1：均值必须是常数。**

这是最直接的要求。信号的平均水平不能随时间上升或下降，它必须是稳定的。假设你有一个传感器，其读数由于发热等原因正在缓慢向上漂移。我们可以将其建模为信号 $X(t) = at + N(t)$，其中 $N(t)$ 代表随机噪声，$at$是确定性漂移。该信号在时间 $t$ 的平均值，或[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman)，是 $E[X(t)] = at$。你可以立即看到，这个平均值随时间变化。该过程不是平稳的。只有当漂移率 $a$ 恰好为零时，该过程才有可能是平稳的 [@problem_id:1755471]。统计特性随[绝对时间](@keyword=absolute_time|lang=zh-CN|style=Feynman)而改变的过程称为**非平稳**过程。

**规则 2：自相关必须仅依赖于[时间延迟](@keyword=time_lag|lang=zh-CN|style=Feynman)。**

这条规则更为微妙，也更为强大。让我们首先思考**[自相关](@keyword=autocorrelation|lang=zh-CN|style=Feynman)**的含义。[自相关函数](@keyword=autocorrelation_function|lang=zh-CN|style=Feynman) $R_{XX}(t_1, t_2) = E[X(t_1) X(t_2)]$，衡量的是信号在两个不同时间点 $t_1$ 和 $t_2$ 上的值的统计关系。它回答的是：“如果信号在时间 $t_1$ 很高，那么它在时间 $t_2$ 也可能很高吗？”

对于一个 WSS 过程，这种关系不能取决于你观察的*时间点*，而只能取决于你观察的*时间间隔*。也就是说，下午 1:00 和 1:01 之间信号的相关性，应该与下午 5:00 和 5:01 之间信号的相关性相同。时间差 $\tau = t_2 - t_1$ 是唯一重要的因素。因此，对于一个 WSS 过程，我们可以将自相关简单地写成一个变量，即时间延迟 $\tau$ 的函数：$R_{XX}(\tau)$。

一个很好的例子是简单地延迟一个信号会发生什么。如果 $X(t)$ 是一个 WSS 过程，我们创建一个新的延迟过程 $Y(t) = X(t - t_0)$，那么 $Y(t)$ 的[自相关](@keyword=autocorrelation|lang=zh-CN|style=Feynman)是什么？一个快速的计算表明 $R_{YY}(\tau) = E[Y(t)Y(t+\tau)] = E[X(t-t_0)X(t+\tau-t_0)]$。如果我们仅仅改变时间参考，令 $u = t - t_0$，这便成为 $E[X(u)X(u+\tau)]$，也就是 $R_{XX}(\tau)$。[自相关函数](@keyword=autocorrelation_function|lang=zh-CN|style=Feynman)完全不受时间平移的影响 [@problem_id:1283257]。过程的内部“节律”与它何时开始无关。

### [平稳过程](@keyword=stationary_processes|lang=zh-CN|style=Feynman)一览

有了这两条规则，我们就可以开始建立一个囊括各种过程的“画廊”，其中一些是 WSS 的，一些则不是。其多样性可能会让你感到惊讶。

- **随机常数：** 你能想到的最简单的“随机”过程是什么？一个完全不改变的过程如何？设 $X(t) = C$，其中 $C$ 是在最开始时选择一次的[随机变量](@keyword=random_variable|lang=zh-CN|style=Feynman)。也许它是一次[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)的最终温度，这个温度有一定的随机性，但之后就永远固定了。这个过程是 WSS 吗？其均值为 $E[X(t)] = E[C]$，是一个常数。其自相关为 $R_{XX}(t_1, t_2) = E[X(t_1)X(t_2)] = E[C^2]$，也是一个常数。由于这些值不依赖于时间，只要二阶矩 $E[C^2]$ 是有限的，这个过程就是 WSS 的 [@problem_id:1350242]。这可能看起来微不足道，但它是一个很好的健全性检查：一个过程不需要“摆动”才能成为 WSS 过程。

- **欺骗性的[振荡器](@keyword=oscillators|lang=zh-CN|style=Feynman)：** 现在来看一个更令人兴奋的案例。考虑一个看起来像纯[正弦波](@keyword=sinusoid|lang=zh-CN|style=Feynman)的过程：$X_n = A \cos(\omega n) + B \sin(\omega n)$。这里，[时间演化](@keyword=time_evolution|lang=zh-CN|style=Feynman)是离散的 ($n=0, 1, 2, ...$)，随机性来自振幅 $A$ 和 $B$。假设 $A$ 和 $B$ 是不相关的[随机变量](@keyword=random_variable|lang=zh-CN|style=Feynman)，均值为零，方差同为 $\sigma^2$。这个过程的任何一次实现都是一个具有特定振幅和相位的完美[正弦波](@keyword=sinusoid|lang=zh-CN|style=Feynman)。这看起来一点也不平稳！但请记住，平稳性是*系综*——所有可能结果的集合——的属性。
均值为 $E[X_n] = E[A]\cos(\omega n) + E[B]\sin(\omega n) = 0$，是常数。[自相关](@keyword=autocorrelation|lang=zh-CN|style=Feynman)呢？经过一些涉及[三角恒等式](@keyword=trigonometric_identities|lang=zh-CN|style=Feynman)的代数运算后，我们得到了一个了不起的结果：$E[X_n X_m] = \sigma^2 \cos(\omega(n-m))$。它只取决于时间延迟 $n-m$！所以，这个过程是完美的 WSS 过程 [@problem_id:1289222]。这是一个深刻的教训：一个过程在任何单个实例中可能看起来高度结构化且随时间变化，但其底层的统计“规则”可以是完全平稳的。

- **物理学家的噪声模型：** 在许多现实世界的实验中，涨落在短时间尺度上是相关的，但在长时间尺度上是不相关的。高斯过程是对此的一个绝佳模型，其中电压涨落 $V(t)$ 有一个恒定均值 $\mu_0$（一个直流偏置）和一个像 $K(s, t) = \sigma^2 \exp\left(-\frac{(s-t)^2}{\ell^2}\right)$ 这样的[协方差函数](@keyword=covariance_function|lang=zh-CN|style=Feynman)。因为均值是常数，且协方差只依赖于时间差 $s-t$，所以这个过程是 WSS 的 [@problem_id:1304142]。这个函数形状告诉我们，两点之间的相关性随着它们之间时间间隔的增加而平滑且迅速地减小，这是一种非常普遍的物理行为。

### 自相关函数：一种统计指纹

[自相关函数](@keyword=autocorrelation_function|lang=zh-CN|style=Feynman) $R_X(\tau)$ 远不止是平稳性的一个数学检验项，它还是过程的一种丰富指纹，揭示了其最深层的物理和统计特性。

- **零点处的峰值：[平均功率](@keyword=average_power|lang=zh-CN|style=Feynman)：** 在延迟为零时，$R_X(\tau)$ 的含义是什么？根据定义，$R_X(0) = E[X(t)X(t+0)] = E[X(t)^2]$。如果 $X(t)$ 代表一个 1 欧姆电阻两端的电压，那么 $X(t)^2$ 就是[瞬时功率](@keyword=instantaneous_power|lang=zh-CN|style=Feynman)。因此，[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman) $E[X(t)^2]$ 就是信号的**平均功率**。所以，[自相关函数](@keyword=autocorrelation_function|lang=zh-CN|style=Feynman)在 $\tau=0$ 处的值不仅仅是一个数字，它还是该过程所携带的总平均功率 [@problem_id:1699343]。

- **遥远的未来：直流功率与[交流功率](@keyword=ac_power|lang=zh-CN|style=Feynman)：** 当时间延迟 $\tau$ 变得非常大时会发生什么？对于大多数没有完美周期性分量的物理过程，时间 $t$ 处的信号将完全忘记其在时间 $t+\tau$ 时的状态。它们在统计上变得独立。在这种情况下，乘积的[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)变成[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)的乘积：$\lim_{\tau \to \infty} R_X(\tau) = E[X(t)X(t+\tau)] \to E[X(t)] E[X(t+\tau)] = \mu_X \cdot \mu_X = \mu_X^2$。[自相关函数](@keyword=autocorrelation_function|lang=zh-CN|style=Feynman)趋近的值是均值的平方！
这为我们提供了一种分解信号功率的绝佳方式。例如，如果一个传感器信号的[自相关](@keyword=autocorrelation|lang=zh-CN|style=Feynman)为 $R_V(\tau) = 13 \exp(-\frac{\tau^2}{2\sigma_0^2}) + 36$，我们可以立即读出其功率分量。总功率为 $R_V(0) = 13 + 36 = 49$ W。在无穷远处的值为 $36$ W，这必定是**直流功率**（$\mu_V^2$）。剩下的部分，即衰减到零的部分，代表了围绕均值的涨落。其功率贡献是**[交流功率](@keyword=ac_power|lang=zh-CN|style=Feynman)**，即 $R_V(0) - \mu_V^2 = 49 - 36 = 13$ W [@problem_id:1767418], [@problem_id:1730060]。功率预算的全部信息都写在了自相关函数的形状里！

- **频率和[白噪声](@keyword=white_noise|lang=zh-CN|style=Feynman)：** 当我们在[频域](@keyword=frequency_domain|lang=zh-CN|style=Feynman)中观察一个过程时，故事变得更加有趣。**维纳-[辛钦定理](@keyword=khintchine_s_theorem|lang=zh-CN|style=Feynman)**告诉我们，[自相关函数](@keyword=autocorrelation_function|lang=zh-CN|style=Feynman) $R_X(\tau)$ 和**[功率谱密度 (PSD)](@keyword=power_spectral_density_(psd)|lang=zh-CN|style=Feynman)** $S_X(f)$——后者描述了[信号功率](@keyword=signal_power|lang=zh-CN|style=Feynman)在不同频率上的分布情况——构成一个[傅里叶变换对](@keyword=ctft_pairs|lang=zh-CN|style=Feynman)。这种联系非常强大。
考虑最终极的[随机过程](@keyword=random_process|lang=zh-CN|style=Feynman)：**白噪声**。这是一种如此不可预测的信号，以至于它在任何瞬间的值都与它在任何其他瞬间的值完全不相关，无论两者有多近。它的自相关函数会是什么样的？对于任何 $\tau \neq 0$，它必须为零，并在 $\tau=0$ 处有一个无限尖锐的峰，以解释信号的功率。具有此性质的数学对象是**[狄拉克δ函数](@keyword=dirac_delta_function|lang=zh-CN|style=Feynman)** $\delta(\tau)$。如果白噪声的功率谱密度是一个常数 $S_{VV}(f) = N_0/2$，那么它的[自相关](@keyword=autocorrelation|lang=zh-CN|style=Feynman)恰好是 $R_{VV}(\tau) = \frac{N_0}{2}\delta(\tau)$ [@problem_id:1345912]。一个平坦的[频谱](@keyword=frequency_spectrum|lang=zh-CN|style=Feynman)（所有频率都同样存在）对应一个在任意不同时刻都完全不相关的信号。

### 更深层次的探讨：宽平稳与严平稳

我们必须小心。我们对宽平稳性的定义只关注过程的前两个矩：均值和[自相关](@keyword=autocorrelation|lang=zh-CN|style=Feynman)。如果更高阶的统计特性，比如信号[概率分布](@keyword=probability_distribution|lang=zh-CN|style=Feynman)的偏度（不对称性）或[峰度](@keyword=kurtosis|lang=zh-CN|style=Feynman)（“峰态”），随时间变化怎么办？

这就引出了一个更强的条件：**[严平稳性](@keyword=strict_sense_stationarity|lang=zh-CN|style=Feynman) (SSS)**。如果一个过程的*全部*[联合概率分布](@keyword=joint_probability_distributions|lang=zh-CN|style=Feynman)对于时间平移是不变的，那么这个过程是严平稳的。这意味着*所有*统计特性——均值、方差、偏度、每一阶矩、每一种可能的统计度量——在时间上都是恒定的。

显然，SSS 是一个强得多的条件。如果一个过程是 SSS 且具有有限的二阶矩，那么它也必须是 WSS。但反过来成立吗？WSS 是否意味着 SSS？

总的来说，答案是**否**。我们可以构造一个 WSS 但非 SSS 的过程。想象一个[离散时间过程](@keyword=discrete_time_process_2|lang=zh-CN|style=Feynman)，在每一步，我们抽取一个独立的随机数。但我们根据时间步改变规则：在偶数时间步，我们从[拉普拉斯分布](@keyword=double_exponential_distribution|lang=zh-CN|style=Feynman)（尖峰，重尾）中抽取；在奇数时间步，我们从高斯分布（经典的[钟形曲线](@keyword=bell_curve|lang=zh-CN|style=Feynman)）中抽取。我们可以巧妙地设置参数，使得两种分布的均值都为零，且方差完全相同。这个过程是 WSS 的，因为它的均值（0）和[自协方差](@keyword=autocovariance|lang=zh-CN|style=Feynman)（在零延迟处的一个δ函数）是时不变的。然而，[概率分布](@keyword=probability_distribution|lang=zh-CN|style=Feynman)的基本形状在每个时间步都来回翻转。这个过程不是严平稳的 [@problem_id:2869731]。

有一个非常重要的特例，这种区别消失了。对于一个**[高斯过程](@keyword=gaussian_processes|lang=zh-CN|style=Feynman)**——即任何样本集合都具有[联合高斯分布](@keyword=jointly_gaussian|lang=zh-CN|style=Feynman)的过程——WSS *确实*意味着 SSS。这是因为一个高斯分布完全由其均值和[协方差](@keyword=covariance|lang=zh-CN|style=Feynman)唯一确定。如果这两者是时不变的，那么该过程的整个统计结构也必须是时不变的 [@problem_id:2869731]。这也是高斯过程在信号处理和机器学习中如此核心的原因之一：它们的[平稳性](@keyword=stationarity|lang=zh-CN|style=Feynman)特性是独一无二的简单和优雅。

因此，从一个简单、直观的“同一性”概念出发，我们穿行于[随机过程](@keyword=random_process|lang=zh-CN|style=Feynman)的景观之中，揭示了时间、频率、功率和概率之间的深刻联系。平稳性的概念，以其宽平稳的形式，提供了恰到好处的结构，使随机世界变得可预测，而又不牺牲其行为的丰富性。