## 引言
[功率谱密度](@entry_id:141002)（Power Spectral Density, PSD）是信号处理和系统建模领域中的一个基石概念，它为我们提供了一个强有力的数学工具，用以描述随机信号的功率如何在频率域上[分布](@entry_id:182848)。从通信系统中的噪声到金融市场中的价格波动，再到天体物理学中的[引力波背景](@entry_id:635196)，理解这些[随机过程](@entry_id:159502)的频率特性对于分析、建模和预测至关重要。然而，随机信号的不可预测性使得直接对其进行[频域分析](@entry_id:265642)变得复杂。我们如何才能量化一个看似无序的信号中，哪些频率分量更强，哪些更弱？本文旨在填补这一知识鸿沟，系统性地回答这个问题。

通过本文，读者将踏上一段从理论到实践的完整学习之旅。在“原理与机制”一章中，我们将深入探讨[功率谱密度](@entry_id:141002)的数学定义、核心性质以及与[维纳-辛钦定理](@entry_id:188017)的深刻联系。接下来的“应用与跨学科联系”一章将展示功率谱密度如何在信号处理、控制理论、物理学乃至神经科学等多个领域中发挥其强大的分析能力。最后，“动手实践”部分将通过具体的编程练习，帮助读者将理论知识转化为解决实际问题的技能。

## 原理与机制

本章在前一章介绍的基础上，深入探讨[功率谱密度](@entry_id:141002) (Power Spectral Density, PSD) 的核心原理与基本机制。我们将从其数学定义出发，揭示其内在属性，并将其扩展到更广泛的理论框架和实际应用场景中。我们的目标是构建一个关于功率谱密度的系统性知识体系，从基本概念到高级应用，为信号处理和[系统建模](@entry_id:197208)领域的深入研究奠定坚实基础。

### 功率谱密度的基本定义：[维纳-辛钦定理](@entry_id:188017)

功率谱密度的核心思想是描述一个[随机过程](@entry_id:159502)的功率如何在不同频率上[分布](@entry_id:182848)。对于一类重要的[随机过程](@entry_id:159502)——**宽义平稳 (Wide-Sense Stationary, WSS)** 过程，这一概念可以通过**[维纳-辛钦定理](@entry_id:188017) (Wiener-Khinchin Theorem)** 得到精确的数学表述。该定理指出，一个宽义[平稳过程](@entry_id:196130)的功率谱密度是其[自相关函数](@entry_id:138327)的[傅里叶变换](@entry_id:142120)。

#### 离散时间功率谱密度

对于一个零均值的复数离散时间宽义[平稳序列](@entry_id:144560) $x[n]$，其[自相关](@entry_id:138991)序列定义为 $r_x[k] = \mathbb{E}\{x[n]\overline{x[n-k]}\}$，其中 $\overline{(\cdot)}$ 表示复共轭，$\mathbb{E}\{\cdot\}$ 表示期望。由于过程是宽义平稳的，该函数仅依赖于时间延迟 $k$。离散时间功率谱密度 $S_x(e^{j\omega})$ 被定义为自相关序列 $r_x[k]$ 的**[离散时间傅里叶变换](@entry_id:196741) (Discrete-Time Fourier Transform, DTFT)** [@problem_id:2892504]：

$S_x(e^{j\omega}) = \sum_{k=-\infty}^{\infty} r_x[k] e^{-j\omega k}$

这个定义揭示了[功率谱密度](@entry_id:141002)的一个基本性质：**周期性**。由于 DTFT 的[核函数](@entry_id:145324) $e^{-j\omega k}$ 对于整数 $k$ 而言，在角频率 $\omega$ 上是以 $2\pi$ 为周期的，即 $e^{-j(\omega+2\pi)k} = e^{-j\omega k}e^{-j2\pi k} = e^{-j\omega k}$，因此 $S_x(e^{j\omega})$ 也必然是以 $2\pi$ 为周期的函数。这意味着[离散时间信号](@entry_id:272771)的所有[频谱](@entry_id:265125)信息都完全包含在任何长度为 $2\pi$ 的频率区间内，例如 $[-\pi, \pi)$。

为了更具体地理解这个定义，我们可以通过一个实例来推导其[闭合形式](@entry_id:271343)解。考虑一个自相关序列为 $R_x[k] = \sigma^2 \rho^{|k|} \cos(\Omega_0 k)$ 的宽义[平稳过程](@entry_id:196130)，其中 $0  \rho  1$ [@problem_id:2892507]。根据定义，其功率谱密度为：

$S_x(e^{j\omega}) = \sum_{k=-\infty}^{\infty} \sigma^2 \rho^{|k|} \cos(\Omega_0 k) e^{-j\omega k}$

利用欧拉公式 $\cos(\Omega_0 k) = \frac{1}{2}(e^{j\Omega_0 k} + e^{-j\Omega_0 k})$，并利用求和的线性性质，上式可以分解为：

$S_x(e^{j\omega}) = \frac{\sigma^2}{2} \left( \sum_{k=-\infty}^{\infty} \rho^{|k|} e^{-j(\omega - \Omega_0)k} + \sum_{k=-\infty}^{\infty} \rho^{|k|} e^{-j(\omega + \Omega_0)k} \right)$

每一项都是对序列 $\rho^{|k|}$ 进行的 DTFT。我们可以通过求解[几何级数](@entry_id:158490)来计算这个变换。序列 $\rho^{|k|}$ 的 DTFT 为：

$\sum_{k=-\infty}^{\infty} \rho^{|k|} e^{-j\alpha k} = \sum_{k=0}^{\infty} (\rho e^{-j\alpha})^k + \sum_{k=1}^{\infty} (\rho e^{j\alpha})^k = \frac{1}{1 - \rho e^{-j\alpha}} + \frac{\rho e^{j\alpha}}{1 - \rho e^{j\alpha}} = \frac{1 - \rho^2}{1 - 2\rho\cos(\alpha) + \rho^2}$

将此结果代入原式，令 $\alpha = \omega - \Omega_0$ 和 $\alpha = \omega + \Omega_0$，即可得到最终的[功率谱密度](@entry_id:141002)表达式：

$S_x(e^{j\omega}) = \frac{\sigma^2(1 - \rho^2)}{2} \left[ \frac{1}{1 - 2\rho\cos(\omega - \Omega_0) + \rho^2} + \frac{1}{1 - 2\rho\cos(\omega + \Omega_0) + \rho^2} \right]$

这个例子展示了如何从自相关函数出发，通过第一性原理推导出[功率谱密度](@entry_id:141002)的具体形态。

#### 连续时间功率谱密度

与离散时间情况相类似，对于一个零均值的连续时间宽义[平稳过程](@entry_id:196130) $x(t)$，其[自相关函数](@entry_id:138327)定义为 $R_x(\tau) = \mathbb{E}\{x(t+\tau)x^*(t)\}$。其功率谱密度 $S_x(\omega)$ 定义为 $R_x(\tau)$ 的**[傅里叶变换](@entry_id:142120) (Fourier Transform, FT)**：

$S_x(\omega) = \int_{-\infty}^{\infty} R_x(\tau) e^{-j\omega\tau} d\tau$

相应的，[自相关函数](@entry_id:138327)可以通过[傅里叶逆变换](@entry_id:178300)从[功率谱密度](@entry_id:141002)得到：

$R_x(\tau) = \frac{1}{2\pi} \int_{-\infty}^{\infty} S_x(\omega) e^{j\omega\tau} d\omega$

这里，我们采用了信号处理领域常用的角频率 $\omega$ (单位为 rad/s) [傅里叶变换](@entry_id:142120)对约定。需要注意的是，不同的文献和领域可能采用不同的约定（例如使用普通频率 $f$ 或不同的 $2\pi$ 因子位置），在进行计算时必须保持一致。

### [功率谱密度](@entry_id:141002)的核心性质

[功率谱密度](@entry_id:141002)作为描述[随机过程](@entry_id:159502)二阶统计特性的核心工具，具有一系列重要的性质。

*   **实值性与对称性**：对于一个实值宽义[平稳过程](@entry_id:196130) $x(t)$，其[自相关函数](@entry_id:138327) $R_x(\tau)$ 是一个实偶函数，即 $R_x(\tau) = R_x(-\tau)$。根据[傅里叶变换的性质](@entry_id:265641)，其实部变换也是一个实偶函数，因此[功率谱密度](@entry_id:141002) $S_x(\omega)$ 是一个实值的[偶函数](@entry_id:163605)，即 $S_x(\omega) = S_x(-\omega)$。

*   **非负性**：任何宽义[平稳过程](@entry_id:196130)的[功率谱密度](@entry_id:141002)在所有频率上都是非负的，即 $S_x(\omega) \ge 0$。这个性质的直观理解是，功率在任何频率上的[分布](@entry_id:182848)都不可能为负。

*   **与[平均功率](@entry_id:271791)的关系**：过程的[平均功率](@entry_id:271791)（或均方值）等于其自相关函数在延迟为零时的取值，即 $P_x = \mathbb{E}\{|x(t)|^2\} = R_x(0)$。根据傅里叶逆变换公式，当 $\tau=0$ 时，我们得到：

    $P_x = R_x(0) = \frac{1}{2\pi} \int_{-\infty}^{\infty} S_x(\omega) d\omega$

    这个关系式被称为**帕萨瓦尔定理 (Parseval's Theorem)** 在[随机过程](@entry_id:159502)中的推广，它表明过程的总平均功率等于其功率谱密度在整个频率轴上的积分（除以 $2\pi$）。这进一步强化了 PSD 作为功率在[频域](@entry_id:160070)“密度”函数的诠释。

*   **功率谱密度的单位**：理解 PSD 的单位对于正确解释物理测量至关重要。假设一个[连续时间过程](@entry_id:274437) $x(t)$ 的物理单位为 $\mathsf{U_x}$（例如，电压 V）。其自相关函数 $R_x(\tau)$ 的单位是 $\mathsf{U_x}^2$。根据 $S_x(\omega)$ 的[傅里叶变换](@entry_id:142120)定义，其单位是 $R_x(\tau)$ 的单位乘以时间的单位 [@problem_id:2892489]。因此，

    $\mathrm{units}\{S_x(\omega)\} = \mathsf{U_x}^2 \cdot \mathrm{s}$

    这个单位初看起来可能不直观，但它与[平均功率](@entry_id:271791)的关系是一致的。考虑量纲 $S_x(\omega) d\omega$，其单位为 $(\mathsf{U_x}^2 \cdot \mathrm{s}) \cdot (\mathrm{rad/s}) = \mathsf{U_x}^2$，这正是功率的单位（因为弧度是无量纲的）。因此，积分 $\int S_x(\omega) d\omega$ 确实代表了功率的累加。如果 PSD 中包含一个狄拉克 $\delta$ 函数项，例如[谱线](@entry_id:193408) $c \cdot \delta(\omega - \omega_0)$，那么为了使整个项的单位与 $S_x(\omega)$ 一致，即 $\mathsf{U_x}^2 \cdot \mathrm{s}$，考虑到 $\delta(\omega)$ 的单位是 $\mathrm{s}$，系数 $c$ 的单位必须是 $\mathsf{U_x}^2$ [@problem_id:2892489]。

### 严格的数学观点：[谱测度](@entry_id:201693)与[周期图](@entry_id:194101)法

虽然[维纳-辛钦定理](@entry_id:188017)为[功率谱密度](@entry_id:141002)提供了一个简洁的定义，但在更复杂的场景下，我们需要一个更严格的数学框架来处理。例如，当一个信号包含确定性的[正弦波](@entry_id:274998)分量时，其功率谱密度会包含**狄拉克 $\delta$ 函数**，这在传统函数意义下是不可积的。

#### Herglotz-Bochner 定理与[谱测度](@entry_id:201693)

为了处理这种[广义函数](@entry_id:182848)，现代[随机过程](@entry_id:159502)理论引入了**[谱测度](@entry_id:201693) (Spectral Measure)** 的概念。**Herglotz-Bochner 定理** 指出，对于任何宽义[平稳过程](@entry_id:196130)，其[自相关函数](@entry_id:138327) $R_x(\tau)$ 都可以表示为一个有界非负测度 $\mu_x$ 的傅里叶-斯蒂尔切斯变换 [@problem_id:2892476]：

$R_x(\tau) = \int_{-\infty}^{\infty} e^{j\omega\tau} d\mu_x(\omega)$

这个[谱测度](@entry_id:201693) $\mu_x$ 才是对过程频率内容最根本的描述。根据[测度论](@entry_id:139744)中的**[勒贝格分解定理](@entry_id:197665) (Lebesgue Decomposition Theorem)**，任何测度 $\mu_x$ 都可以唯一地分解为三个相互奇异的部分：

$\mu_x = \mu_{\mathrm{ac}} + \mu_{\mathrm{pp}} + \mu_{\mathrm{sc}}$

1.  **绝对连续部分 (Absolutely Continuous, $\mu_{\mathrm{ac}}$)**：这部分可以表示为一个函数（即我们通常所说的功率谱密度函数）对勒贝格测度的积分，即 $d\mu_{\mathrm{ac}}(\omega) = f_x(\omega)d\omega$。$f_x(\omega)$ 是 $\mu_{\mathrm{ac}}$ 关于[勒贝格测度](@entry_id:139781)的**[拉东-尼科迪姆导数](@entry_id:158399) (Radon-Nikodym derivative)**。这部分对应于过程中的随机噪声成分，如白噪声或色噪声。功率谱密度 $S_x(\omega)$ 与这个密度函数的关系为 $S_x(\omega) = 2\pi f_x(\omega)$，这个 $2\pi$ 因子源于[傅里叶变换](@entry_id:142120)的约定 [@problem_id:2892476]。

2.  **纯点部分 (Pure Point, $\mu_{\mathrm{pp}}$)**：也称为原子部分，它由在特定频率点上的离散质量组成，可以写成一系列[狄拉克测度](@entry_id:197577)之和 $\mu_{\mathrm{pp}} = \sum_k a_k \delta_{\omega_k}$。这部分对应于过程中的确定性周期分量，例如[正弦波](@entry_id:274998)或非零均值。例如，一个均值为 $m_x$ 的过程，其[谱测度](@entry_id:201693)在 $\omega=0$ 处会有一个质量为 $m_x^2$ 的原子，对应于[功率谱密度](@entry_id:141002)中的 $2\pi m_x^2 \delta(\omega)$ 项 [@problem_id:2892476]。

3.  **奇异连续部分 (Singular Continuous, $\mu_{\mathrm{sc}}$)**：这是一种较为奇特的组成部分，其[测度集中](@entry_id:265372)在一个勒贝格测度为零的集合上，但又不包含任何原子。它在物理信号中较为罕见，但在分形几何和混沌理论中会出现。其对应的[功率谱](@entry_id:159996)既不是一个[可积函数](@entry_id:191199)，也不是[离散谱](@entry_id:150970)线的和 [@problem_id:2892476]。

#### 从[周期图](@entry_id:194101)到[功率谱密度](@entry_id:141002)

在实践中，我们通常只有过程的一段有限长度的观测样本。一个自然的想法是通过计算这段样本的[傅里叶变换](@entry_id:142120)的模平方来估计[功率谱](@entry_id:159996)，这被称为**[周期图](@entry_id:194101) (Periodogram)**。然而，可以证明，当观测长度 $N \to \infty$ 时，[周期图](@entry_id:194101)本身并不是一个**[一致估计量](@entry_id:266642)**，即其[方差](@entry_id:200758)不趋于零。它的值会在真实的 PSD 周围剧烈波动。

一个更严谨的定义方式是将功率谱密度视为**期望[周期图](@entry_id:194101)的极限** [@problem_id:2892470]。对于长度为 $N$ 的观测，期望[周期图](@entry_id:194101)可以表示为对真实[谱测度](@entry_id:201693) $dF_x$ 与一个称为**费歇尔核 (Fejér Kernel)** 的函数进行卷积。随着 $N \to \infty$，费歇尔核趋近于一个 $\delta$ 函数，这个卷积操作也就趋近于恢复原始的[谱测度](@entry_id:201693)。

这种收敛的最一般形式是**[测度的弱收敛](@entry_id:199755) (Weak Convergence of Measures)**。这意味着，对于任何连续[有界函数](@entry_id:176803) $g(\omega)$，$\int g(\omega) \mathbb{E}\{I_N(\omega)\} d\omega$ 会收敛到 $\int g(\omega) dF_x(\omega)$。这种[收敛方式](@entry_id:189917)的优越性在于它能统一处理包含连续谱和[离散谱](@entry_id:150970)线在内的所有情况。只有当[谱测度](@entry_id:201693)是纯粹绝对连续时（即PSD是一个普通函数），我们才能在几乎处处的意义上谈论期望[周期图](@entry_id:194101)的点态收敛 [@problem_id:2892470]。

### 实际应用与扩展

#### 单边与双边谱密度

在数学定义中，频率 $\omega$ 或 $f$ 的取值范围是 $(-\infty, \infty)$，由此得到的功率谱密度被称为**双边谱密度 (Two-Sided PSD)**。然而，对于实值信号，由于 $S_x(\omega)$ 是[偶函数](@entry_id:163605)，[负频率](@entry_id:264021)部分的信息是冗余的。在工程应用中，人们更关心物理上可测量的正频率，因此常常定义**单边谱密度 (One-Sided PSD)**，记为 $S_x^{(1)}(f)$，仅在 $f \ge 0$ 上有定义。

单边谱和双边谱的转换关系由功率[守恒定律](@entry_id:269268)决定。对于一个实值过程，其总功率可以表示为：

$P_x = \int_{-\infty}^{\infty} S_x(f) df = \int_{-\infty}^{0} S_x(f) df + \int_{0}^{\infty} S_x(f) df = 2 \int_{0}^{\infty} S_x(f) df$

（这里我们暂时使用普通频率 $f$ 且假设在 $f=0$ 处没有[奇异点](@entry_id:199525)）。而根据单边谱的定义，$P_x = \int_0^{\infty} S_x^{(1)}(f) df$。比较两者可得，对于 $f > 0$：

$S_x^{(1)}(f) = 2 S_x(f)$

对于 $f=0$ 处的[直流分量](@entry_id:272384)，其功率不应被加倍，所以 $S_x^{(1)}(0) = S_x(0)$。

如果使用[角频率](@entry_id:261565) $\omega$ 和普通频率 $f$ 混合的表示，并考虑[傅里叶变换](@entry_id:142120)的约定，关系会稍有变化。以 [@problem_id:2892511] 中的约定为例，总功率 $r_x(0) = \frac{1}{2\pi} \int_{-\infty}^{\infty} S_x(\omega) d\omega = \int_0^{\infty} S_x^{(1)}(f) df$。通过变量替换 $\omega=2\pi f$，可推导出对于 $f>0$：

$S_x^{(1)}(f) = 2 S_x(2\pi f)$

例如，考虑一个[确定性信号](@entry_id:272873) $x(t) = A\cos(2\pi f_0 t)$，其[平均功率](@entry_id:271791)为 $A^2/2$。其双边角频率谱为 $S_x(\omega) = \frac{\pi A^2}{2} [\delta(\omega - \omega_0) + \delta(\omega + \omega_0)]$，其中 $\omega_0=2\pi f_0$。对应的单边谱必须在 $f=f_0$ 处包含所有功率，因此 $S_x^{(1)}(f) = \frac{A^2}{2} \delta(f-f_0)$ [@problem_id:2892511]。

#### 混合谱

许多实际信号由确定性分量（如[正弦波](@entry_id:274998)）和随机分量（如噪声）叠加而成，这类信号具有**混合谱**，即其[谱测度](@entry_id:201693)同时包含纯点[部分和](@entry_id:162077)绝对连续部分。如果这些分量是统计独立的，那么总信号的功率谱密度就是各分量[功率谱密度](@entry_id:141002)的和。

例如，一个信号 $x(t) = s(t) + n(t)$，其中 $s(t) = A_1\cos(2\pi f_1 t + \phi_1)$ 是一个[正弦波](@entry_id:274998)，而 $n(t)$ 是一个具有连续谱 $S_n(f)$ 的零均值噪声，且两者独立。那么 $x(t)$ 的总功率就是 $s(t)$ 的功率与 $n(t)$ 的功率之和 [@problem_id:2892484]。
- 噪声的功率贡献（[连续谱](@entry_id:155477)部分）为 $P_{\text{cont}} = \int_{-\infty}^{\infty} S_n(f) df$。
- [正弦波](@entry_id:274998)的功率贡献（[离散谱](@entry_id:150970)部分）为 $P_{f_1} = A_1^2/2$。

这种功率的叠加原理是分析复杂[信号频谱](@entry_id:198418)的基础。

#### [互功率谱密度](@entry_id:268814)

[功率谱密度](@entry_id:141002)的概念可以推广到两个联合宽义[平稳过程](@entry_id:196130) $x(t)$ 和 $y(t)$ 之间的关系，由此引出**[互功率谱密度](@entry_id:268814) (Cross-Spectral Density)**。首先定义**[互相关函数](@entry_id:147301) (Cross-Correlation Function)**：

$R_{xy}(\tau) = \mathbb{E}\{x(t+\tau)y^*(t)\}$

[互功率谱密度](@entry_id:268814) $S_{xy}(\omega)$ 被定义为[互相关函数](@entry_id:147301) $R_{xy}(\tau)$ 的[傅里叶变换](@entry_id:142120) [@problem_id:2892459]：

$S_{xy}(\omega) = \int_{-\infty}^{\infty} R_{xy}(\tau) e^{-j\omega\tau} d\tau$

[互功率谱密度](@entry_id:268814)是一个复数函数，其幅度和相位分别描述了两个过程在不同频率上的相关强度和相位关系。它具有以下重要性质：

*   **[埃尔米特对称性](@entry_id:266311) (Hermitian Symmetry)**：$S_{yx}(\omega) = S_{xy}^*(\omega)$。这个性质表明，交换两个过程的顺序等价于取[复共轭](@entry_id:174690) [@problem_id:2892459]。
*   **[共轭对称性](@entry_id:144131)（对于实过程）**：如果 $x(t)$ 和 $y(t)$ 都是实值过程，那么 $R_{xy}(\tau)$ 是一个实函数，其[傅里叶变换](@entry_id:142120)满足[共轭对称性](@entry_id:144131) $S_{xy}(-\omega) = S_{xy}^*(\omega)$ [@problem_id:2892459]。然而，与自[功率谱密度](@entry_id:141002)不同，[互功率谱密度](@entry_id:268814)通常不是一个实函数，因为 $R_{xy}(\tau)$ 一般不是偶函数。

### [线性系统](@entry_id:147850)中的功率谱密度

功率谱密度在分析随机信号通过**线性时不变 (Linear Time-Invariant, LTI)** 系统时尤为重要。假设一个宽义[平稳过程](@entry_id:196130) $x(t)$ 作为输入，通过一个具有冲激响应 $h(t)$ 和频率响应 $H(\omega)$ 的 LTI 系统，产生输出 $y(t)$。

通过从卷积定义出发，可以严格推导出输出过程 $y(t)$ 的功率谱密度 $S_y(\omega)$ 与输入过程的功率谱密度 $S_x(\omega)$ 以及系统的频率响应之间的简单关系 [@problem_id:2892475]：

$S_y(\omega) = |H(\omega)|^2 S_x(\omega)$

这个公式是随机信号处理中的基石之一。它表明，输出信号在某个频率上的[功率密度](@entry_id:194407)等于输入信号在该频率上的[功率密度](@entry_id:194407)乘以系统在该频率上[频率响应](@entry_id:183149)的模平方。换句话说，LTI 系统对随机输入的[功率谱](@entry_id:159996)起到了一个“滤波器”的作用，其滤波形状由 $|H(\omega)|^2$ 决定。

利用此关系，我们可以计算输出过程的总[平均功率](@entry_id:271791) $P_y$：

$P_y = R_y(0) = \frac{1}{2\pi} \int_{-\infty}^{\infty} S_y(\omega) d\omega = \frac{1}{2\pi} \int_{-\infty}^{\infty} |H(\omega)|^2 S_x(\omega) d\omega$

这个积分计算了经过系统频率响应 $|H(\omega)|^2$ 加权后的输入功率谱的总和。例如，如果一个具有指数[自相关函数](@entry_id:138327) $R_x(\tau) = \sigma^2 \exp(-|\tau|/\tau_c)$ 的过程通过一个一阶低通滤波器 $h(t) = a \exp(-at)u(t)$，我们可以通过计算上述积分得到输出功率为 $P_y = \frac{\sigma^2 a\tau_c}{1+a\tau_c}$ [@problem_id:2892475]。这表明输出功率不仅取决于输入总功率 $\sigma^2$，还取决于输入信号的带宽（由 $\tau_c$ 决定）和滤波器的带宽（由 $a$ 决定）之间的相互作用。

### 超越[平稳性](@entry_id:143776)：展望

经典功率谱密度的定义严格依赖于过程的宽义平稳性，即其二阶统计特性不随时间改变。然而，许多现实世界中的信号，如语音信号、地震波和经济数据，都是**非平稳的**，它们的频率内容会随时间演化。对于这类过程，单一的、不随时间变化的功率谱密度是不足以描述其特性的 [@problem_id:2892461]。

为了分析[非平稳信号](@entry_id:262838)，研究者们发展了多种[时频分析](@entry_id:186268)方法。其中一个有影响力的理论框架是 **Priestley 的演化谱 (Evolutionary Spectrum)**。其核心思想是将一个[非平稳过程](@entry_id:269756) $x(t)$ 模型化为一个[振荡](@entry_id:267781)过程，其振幅在不同频率上随时间缓慢变化：

$x(t) = \int_{-\infty}^{\infty} A(\omega, t) e^{j\omega t} dZ(\omega)$

其中 $dZ(\omega)$ 是一个具有正交增量的过程，而 $A(\omega, t)$ 是一个时变振幅函数。**演化谱密度**被定义为 $S_x(\omega, t) = |A(\omega, t)|^2$ (相对于某个基础[谱测度](@entry_id:201693))，它描述了过程在时间 $t$ 和频率 $\omega$ 点的[瞬时功率](@entry_id:174754)[分布](@entry_id:182848)。

这个概念的一个重要优点是它的**一致性**：如果一个过程本身是宽义平稳的，那么其演化谱将退化为一个与时间无关的函数，即 $S_x(\omega, t) = S_x(\omega)$，这个函数恰好就是经典的[功率谱密度](@entry_id:141002) [@problem_id:2892461]。这确保了演化谱是经典[谱理论](@entry_id:275351)的一个自然推广。演化谱为我们理解和分析那些统计特性随时间变化的复杂动态过程提供了强有力的理论工具，是通向更高级信号处理课题的桥梁。