## 引言
在现实世界的科学与工程问题中，从通信系统中的功放失真到生物系统中的神经元响应，[非线性](@entry_id:637147)现象无处不在。传统的[线性时不变](@entry_id:276287)（LTI）系统理论虽然强大，但其核心的叠加原理在面对这些复杂行为时常常失效，这使得对[非线性](@entry_id:637147)动态的精确建模成为一项关键挑战。本文旨在填补这一知识鸿沟，为读者提供一个关于非线性系统建模的系统性框架，重点介绍应用广泛的Volterra、Wiener和[Hammerstein模型](@entry_id:193919)。

为了构建一个全面的理解，本文将分三个层次展开。首先，在“原理与机制”一章中，我们将深入探讨[非线性](@entry_id:637147)行为的数学基础，从[Volterra级数](@entry_id:167552)的泛函理论到Wiener和[Hammerstein模型](@entry_id:193919)的结构化表示。接着，在“应用与交叉学科联系”一章中，我们将展示这些理论如何应用于实际的[系统辨识](@entry_id:201290)问题，讨论从实验设计到[模型验证](@entry_id:141140)的各种策略，并探索其在不同学科领域的应用。最后，“动手实践”部分将通过具体的计算和推导练习，帮助读者将理论知识转化为解决实际问题的能力。现在，让我们从[非线性系统](@entry_id:168347)建模最核心的数学原理出发，开启我们的探索之旅。

## 原理与机制

在上一章对[非线性系统](@entry_id:168347)建模的重要性有了宏观认识之后，本章将深入探讨描述这类系统的核心数学原理与基本机制。我们将从最根本的[线性系统理论](@entry_id:172825)的局限性出发，逐步建立起描述[非线性](@entry_id:637147)行为的通用框架——[Volterra级数](@entry_id:167552)。随后，我们将探讨这一框架的理论基础、[频域](@entry_id:160070)特性，并介绍几种在工程实践中广泛应用的结构化模型，如[Hammerstein模型](@entry_id:193919)和[Wiener模型](@entry_id:188978)。最后，我们将讨论在[模型辨识](@entry_id:139651)过程中遇到的一个关键理论问题：[可辨识性](@entry_id:194150)。

### [线性叠加原理](@entry_id:196987)的失效与[非线性](@entry_id:637147)现象

[线性时不变](@entry_id:276287)（LTI）系统的理论基石是**[叠加原理](@entry_id:144649)**（superposition principle），它包含两个基本性质：**可加性**（additivity）与**齐次性**（homogeneity）。可加性要求系统对两个输入信号之和的响应，等于系统对每个信号单独响应之和，即 $S[u_1 + u_2] = S[u_1] + S[u_2]$。齐次性则要求将输入信号放大 $a$ 倍，其输出信号也被同样放大 $a$ 倍，即 $S[a \cdot u] = a \cdot S[u]$。然而，在现实世界中，绝大多数物理系统在输入信号较大时都会表现出[非线性](@entry_id:637147)特征，此时[叠加原理](@entry_id:144649)不再成立。

为了直观理解[叠加原理](@entry_id:144649)的失效，我们可以考察一个极简的非线性系统：平方器。假设一个静态系统的输出 $y(t)$ 是其输入 $u(t)$ 的平方，即 $y(t) = S[u](t) = (u(t))^2$。

首先，我们检验可加性。对于两个输入信号 $u_1(t)$ 和 $u_2(t)$，系统对它们和的响应是：
$S[u_1 + u_2](t) = (u_1(t) + u_2(t))^2 = (u_1(t))^2 + (u_2(t))^2 + 2u_1(t)u_2(t)$
而系统对每个信号单独响应之和为：
$S[u_1](t) + S[u_2](t) = (u_1(t))^2 + (u_2(t))^2$
显然，只要[交叉](@entry_id:147634)项 $2u_1(t)u_2(t)$ 不恒为零，可加性就不成立。这个[交叉](@entry_id:147634)项是非线性系统区别于线性系统的关键特征之一，它导致了**[互调失真](@entry_id:267789)**（intermodulation distortion）。例如，若输入为两个不同频率的余弦信号之和，即 $u(t) = A_1\cos(\omega_1 t) + A_2\cos(\omega_2 t)$，平方器的输出将包含频率为 $\omega_1 \pm \omega_2$ 的新频率分量，这些分量在原始输入中是不存在的。

其次，我们检验齐次性。对于输入 $a \cdot u(t)$，系统响应为：
$S[a \cdot u](t) = (a \cdot u(t))^2 = a^2 (u(t))^2$
而对原始输出的 $a$ 倍缩放为：
$a \cdot S[u](t) = a \cdot (u(t))^2$
只有当 $a^2 = a$（即 $a=0$ 或 $a=1$）时两者才相等。由于齐次性要求对任意标量 $a$ 都成立，故该系统不满足齐次性。一个 $n$ 次多项式[非线性](@entry_id:637147)环节，在输入被缩放 $a$ 倍时，其输出会被缩放 $a^n$ 倍。这种非线性关系导致了**[谐波失真](@entry_id:264840)**（harmonic distortion），例如，当输入为 $\cos(\omega_1 t)$ 时，平方器的输出将包含频率为 $2\omega_1$ 的二次谐波分量。

叠加原理的失效给[系统辨识](@entry_id:201290)带来了根本性的挑战。对于线性系统，我们可以通过分析系统对单一[正弦信号](@entry_id:196767)或[高斯白噪声](@entry_id:749762)的响应来完全刻画其特性。但在[非线性系统](@entry_id:168347)中，如上例所示，不同频率分量会相互作用产生新的频率成分。当使用零均值高斯过程作为输入时，由于[高斯过程](@entry_id:182192)的奇数阶矩（如三阶矩）为零，输入与输出的互相关（二阶统计量）仅能揭示系统的线性部分（一阶响应），而无法捕捉到偶数阶[非线性](@entry_id:637147)（如二次项）的信息。因此，辨识非线性系统必须借助[高阶统计量](@entry_id:193349)或特殊设计的激励信号，这构成了[非线性系统辨识](@entry_id:191103)理论的核心内容 [@problem_id:2887116]。

### [Volterra级数](@entry_id:167552)：非线性系统的通用表示

面对非线性系统的复杂性，我们需要一个通用的数学框架来描述其输入输出关系。**[Volterra级数](@entry_id:167552)**正是为此而生，它可以被视为[线性卷积](@entry_id:190500)积分向[非线性系统](@entry_id:168347)的推广，为具有“衰减记忆”特性的[时不变系统](@entry_id:264083)提供了一种强大的表示方法。

对于一个连续时间、因果、时不变的[非线性系统](@entry_id:168347)，其输出 $y(t)$ 可以表示为输入 $x(t)$ 的一系列[多重积分](@entry_id:146170)之和。截断至 $P$ 阶的[Volterra级数](@entry_id:167552)表达式为：
$y(t) = h_0 + \sum_{p=1}^{P} \int_{0}^{\infty}\! \cdots \! \int_{0}^{\infty} h_p(\tau_1,\ldots,\tau_p)\,\prod_{k=1}^{p} x(t-\tau_k)\, \mathrm{d}\tau_1\cdots \mathrm{d}\tau_p$

- $h_0$ 是零阶核，代表系统在零输入下的直流偏置或静态输出。
- $h_p(\tau_1,\ldots,\tau_p)$ 被称为 **$p$ 阶Volterra核**。它是一个 $p$ 维函数，刻画了 $p$ 个不同时刻的输入样本如何共同作用以影响当前时刻的输出。
- 积分的下限为 $0$ 体现了系统的**因果性**（causality），即输出只依赖于当前和过去的输入（$t-\tau_k \le t$ 要求 $\tau_k \ge 0$）。
- 表达式的形式 $x(t-\tau_k)$ 保证了系统的**[时不变性](@entry_id:198838)**（time-invariance），即系统的行为不随时间起点变化。
- 一阶核 $h_1(\tau)$ 正是[LTI系统](@entry_id:271946)的脉冲响应。因此，[Volterra级数](@entry_id:167552)的第一项就是[线性卷积](@entry_id:190500)，后续各项则是对[非线性](@entry_id:637147)行为的逐级修正 [@problem_id:2887075]。

类似地，对于[离散时间系统](@entry_id:263935)，[Volterra级数](@entry_id:167552)由多[重求和](@entry_id:275405)定义。对于一个具有[有限记忆](@entry_id:136984)长度 $M$ 阶和 $P$ 阶[非线性](@entry_id:637147)的因果离散系统，其输出 $y[n]$ 可表示为：
$y[n] = h_0 + \sum_{p=1}^{P} \sum_{k_1=0}^{M}\cdots\sum_{k_p=0}^{M} h_p[k_1,\ldots,k_p] \prod_{i=1}^{p} x[n-k_i]$
这里的离散Volterra核 $h_p[k_1,\ldots,k_p]$ 定义在延迟索引构成的立方体 $\{0, 1, \ldots, M\}^p$ 上，描述了最近 $M+1$ 个输入样本之间的 $p$ 阶[交互作用](@entry_id:176776) [@problem_id:2887038]。

Volterra核的一个核心性质是**对称性**（symmetry）。我们可以不失一般性地假设Volterra核对其所有参数都是对称的，即交换任意两个延迟变量 $\tau_i$ 和 $\tau_j$ 的位置，核函数的值不变。例如，对于二阶核，$h_2(\tau_1, \tau_2) = h_2(\tau_2, \tau_1)$。这个性质并非是物理系统的内在约束，而是一个数学上的便利。其根源在于Volterra积分（或求和）的结构。在积分项 $\prod_{k=1}^{p} x(t-\tau_k)$ 中，由于实数乘法满足交换律，其值不随延迟变量 $(\tau_1, \ldots, \tau_p)$ 的[排列](@entry_id:136432)顺序而改变。同时，积分测度 $\mathrm{d}\tau_1\cdots \mathrm{d}\tau_p$ 也是[排列](@entry_id:136432)不变的。这意味着，任何一个Volterra核 $h_p$ 的非对称部分在与对称的输入乘积项进行积分后，其贡献会相互抵消。我们可以将任意一个核 $h_p$ 替换为其“对称化”版本 $h_p^{\text{sym}}$，而系统的输入输出关系完全不变。对称化核定义为对原始核的所有 $p!$ 种参数[排列](@entry_id:136432)进行平均：
$h_p^{\text{sym}}(\tau_1,\ldots,\tau_p) = \frac{1}{p!}\sum_{\pi \in \mathcal{S}_p} h_p(\tau_{\pi(1)},\ldots,\tau_{\pi(p)})$
其中 $\mathcal{S}_p$ 是 $p$ 个符号的[置换群](@entry_id:142907)。由于任何核产生的系统行为都等价于其对称化版本产生的行为，我们通常直接定义和使用对称的Volterra核，这大大简化了核的辨识与分析 [@problem_id:2887113]。

### [Volterra级数](@entry_id:167552)的理论基础：泛函泰勒展开

[Volterra级数](@entry_id:167552)不仅仅是一个启发式的多项式推广，它具有坚实的数学基础，可以被视为在[函数空间](@entry_id:143478)中对系统算子进行的**泛函[泰勒展开](@entry_id:145057)**（functional Taylor expansion）。

我们可以将一个系统视为一个算子 $F$，它将输入信号（一个函数）$x(t)$ 映射到输出信号（另一个函数）$y(t)$，即 $y = F[x]$。假设这些信号属于某个合适的[巴拿赫空间](@entry_id:143833)（例如，具有加权范数的有界[连续函数空间](@entry_id:150395)），我们可以像研究普通函数一样研究算子 $F$ 的“[光滑性](@entry_id:634843)”。

如果算子 $F$ 在零输入点（$x \equiv 0$）附近是**Fréchet解析**的（Fréchet-analytic），这意味着它可以在该点附近展开为一个收敛的[幂级数](@entry_id:146836)，这个级数就是泛函[泰勒级数](@entry_id:147154)。对于满足 $F[0]=0$ 的系统，其展开形式为：
$F[x] = \sum_{n=1}^{\infty} \frac{1}{n!} D^nF[0](x, \dots, x)$
其中 $D^nF[0]$ 是 $F$ 在零输入处的 $n$ 阶Fréchet导数。它是一个 $n$-重[线性算子](@entry_id:149003)，描述了系统对 $n$ 个微小输入扰动的 $n$ 阶响应。

这个泛函展开与[Volterra级数](@entry_id:167552)之间的联系在于：如果系统 $F$ 同时是时不变和因果的，那么它的各阶Fréchet导数 $D^nF[0]$ 也将继承这些性质。根据泛函分析中的一个基本定理（[Riesz表示定理](@entry_id:140012)的推广），任何一个连续、时不变、因果的 $n$-重线性算子都可以唯一地表示为一个 $n$ 维[卷积积分](@entry_id:155865)，其积分核正是一个对称的 $n$ 维函数。这个函数，正是我们之前定义的 $n$ 阶Volterra核 $h_n$。

因此，[Volterra级数](@entry_id:167552)正是Fréchet解析的非[线性[时不变系](@entry_id:276591)统](@entry_id:264083)的泛函泰勒级数。Fréchet[解析性](@entry_id:140716)是保证[Volterra级数](@entry_id:167552)在零输入邻域内存在且收敛的严格数学条件。这种观点不仅为[Volterra级数](@entry_id:167552)提供了理论合法性，也揭示了Volterra核的本质——它们是系统算子在[函数空间](@entry_id:143478)中逐阶导数的积分核表示 [@problem_id:2887092]。

### 频率域分析：[广义频率响应函数](@entry_id:187726)

对于[线性时不变系统](@entry_id:276591)，频率响应函数（[傅里叶变换](@entry_id:142120)后的脉冲响应）是分析其动态特性的核心工具。这一概念可以推广到[Volterra级数](@entry_id:167552)，引出**[广义频率响应函数](@entry_id:187726)**（Generalized Frequency Response Function, GFRF）的概念。

$p$ 阶GFRF，记作 $H_p(\omega_1, \ldots, \omega_p)$，被定义为 $p$ 阶Volterra核 $h_p(\tau_1, \ldots, \tau_p)$ 的 $p$ 维[傅里叶变换](@entry_id:142120)：
$H_p(\omega_1,\ldots,\omega_p)=\int_{-\infty}^{\infty}\cdots\int_{-\infty}^{\infty} h_p(\tau_1,\ldots,\tau_p)\,e^{-j(\omega_1\tau_1+\cdots+\omega_p\tau_p)}\,\mathrm{d}\tau_1\cdots \mathrm{d}\tau_p$

GFRF揭示了系统如何在频率域中进行[非线性](@entry_id:637147)转换。当输入包含频率为 $\omega_1, \ldots, \omega_p$ 的分量时，系统通过 $H_p(\omega_1, \ldots, \omega_p)$ 的加权，在输出端产生一个频率为 $\omega_1 + \cdots + \omega_p$ 的新分量。

与Volterra核的性质相对应，GFRF也具有重要的对称性：
1.  **[排列](@entry_id:136432)对称性 (Permutation Symmetry)**: 由于Volterra核 $h_p$ 可以被假定为对称的，其[傅里叶变换](@entry_id:142120) $H_p$ 也对其频率变量具有[排列](@entry_id:136432)对称性。即，交换任意两个频率变量的位置，GFRF的值不变：$H_p(\ldots, \omega_i, \ldots, \omega_j, \ldots) = H_p(\ldots, \omega_j, \ldots, \omega_i, \ldots)$。
2.  **[共轭对称性](@entry_id:144131) (Conjugate Symmetry)**: 如果系统是实值系统（即实输入产生实输出），则其Volterra核 $h_p$ 是实函数。这导致GFRF具有[共轭对称性](@entry_id:144131)：$H_p(\omega_1, \ldots, \omega_p) = H_p^*(-\omega_1, \ldots, -\omega_p)$。这个性质保证了当输入为实信号时，输出信号的[频谱](@entry_id:265125)也具有[共轭对称性](@entry_id:144131)，从而确保输出也是实信号。

这些对称性质极大地减少了辨识和存储GFRF所需的[独立数](@entry_id:260943)据量，是[高阶谱](@entry_id:191458)分析和[非线性系统](@entry_id:168347)[频域](@entry_id:160070)辨识中的关键考量 [@problem_id:2887033]。

### 结构化[非线性模型](@entry_id:276864)：Hammerstein、Wiener与Wiener-[Hammerstein模型](@entry_id:193919)

尽管[Volterra级数](@entry_id:167552)提供了完备的理论框架，但在实际应用中，直接辨识高维的Volterra核非常困难，因为它需要估计的参数数量会随着阶数和记忆长度的增加而急剧膨胀（所谓的“[维数灾难](@entry_id:143920)”）。因此，工程上更常用的是一些结构受限的**块状模型**（block-oriented models），它们可以看作是[Volterra级数](@entry_id:167552)的特例，但参数更少，物理意义更明确。

#### [Hammerstein模型](@entry_id:193919)（NL-LTI）

[Hammerstein模型](@entry_id:193919)由一个**静态[非线性](@entry_id:637147)模块 (NL)** [串联](@entry_id:141009)一个**[线性时不变](@entry_id:276287)模块 (LTI)** 构成。输入信号 $u(t)$ 首先经过一个无记忆的[非线性](@entry_id:637147)函数 $g(\cdot)$ 变换，得到中间信号 $v(t) = g(u(t))$，然后 $v(t)$ 再通过一个脉冲响应为 $h(t)$ 的线性滤波器。

其输入输出关系可以通过[卷积积分](@entry_id:155865)直接导出。若[非线性](@entry_id:637147)函数 $g(x)$ 是一个 $P$ 次多项式 $g(x)=\sum_{p=1}^{P} a_{p} x^{p}$，则系统总输出 $y(t)$ 为：
$y(t) = \int_{-\infty}^{\infty} h(\tau) v(t-\tau) \mathrm{d}\tau = \int_{-\infty}^{\infty} h(\tau) \left( \sum_{p=1}^{P} a_p (u(t-\tau))^p \right) \mathrm{d}\tau$
交换求和与积分的顺序，我们得到：
$y(t)=\sum_{p=1}^{P} a_{p} \int_{-\infty}^{\infty} h(\tau)\,(u(t-\tau))^{p}\, \mathrm{d}\tau$
通过与通用[Volterra级数](@entry_id:167552)比较，可以看出[Hammerstein模型](@entry_id:193919)的Volterra核具有一种特殊的“对角”结构。例如，其二阶核为 $h_2(\tau_1, \tau_2) = a_2 h(\tau_1) \delta(\tau_1 - \tau_2)$（在离散情况下），这表示[非线性](@entry_id:637147)交互仅发生在同一时刻的输入样本上 [@problem_id:2887082]。

#### [Wiener模型](@entry_id:188978)（LTI-NL）

[Wiener模型](@entry_id:188978)与[Hammerstein模型](@entry_id:193919)的结构恰好相反，它由一个**LTI模块**[串联](@entry_id:141009)一个**静态NL模块**构成。输入信号 $x(t)$ 首先通过脉冲响应为 $h(t)$ 的线性滤波器，得到中间信号 $v(t) = (x * h)(t)$，然后 $v(t)$ 再经过[非线性](@entry_id:637147)函数 $g(\cdot)$ 变换得到最终输出 $y(t) = g(v(t))$。

假设[非线性](@entry_id:637147)函数是一个三次多项式 $g(v) = c_{0} + c_{1} v + c_{2} v^{2} + c_{3} v^{3}$，我们可以将 $v(t)$ 的卷积表达式代入，得到系统的[Volterra级数](@entry_id:167552)表示。例如，对于二次项 $c_2 [v(t)]^2$：
$c_2 [v(t)]^2 = c_2 \left( \int_{-\infty}^{\infty} h(\tau_1) x(t-\tau_1) \mathrm{d}\tau_1 \right) \left( \int_{-\infty}^{\infty} h(\tau_2) x(t-\tau_2) \mathrm{d}\tau_2 \right)$
这可以写成一个[二重积分](@entry_id:198869)：
$c_2 \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} c_2 h(\tau_1) h(\tau_2) x(t-\tau_1) x(t-\tau_2) \mathrm{d}\tau_1 \mathrm{d}\tau_2$
从中我们可以识别出[Wiener模型](@entry_id:188978)的二阶Volterra核为 $h_2(\tau_1, \tau_2) = c_2 h(\tau_1) h(\tau_2)$。推广到任意阶，[Wiener模型](@entry_id:188978)的 $p$ 阶Volterra核具有**可分离**（separable）的结构：$h_p(\tau_1, \ldots, \tau_p) = c_p h(\tau_1) \cdots h(\tau_p)$。这意味着高维的 $p$ 阶核可以完全由一个一维函数 $h(\tau)$ 和一个标量系数 $c_p$ 确定。这种结构极大地简化了[模型辨识](@entry_id:139651)问题 [@problem_id:2887035]。

#### Wiener-[Hammerstein模型](@entry_id:193919)（LTI-NL-LTI）

Wiener-[Hammerstein模型](@entry_id:193919)是上述两种模型的级联，其结构为 LTI-NL-LTI。信号依次通过第一个[LTI系统](@entry_id:271946)（脉冲响应 $h_1[n]$）、静态[非线性](@entry_id:637147)环节 $f(\cdot)$ 和第二个[LTI系统](@entry_id:271946)（脉冲响应 $h_2[n]$）。这种结构在许多应用中都很有用。

通过逐步推导，可以得到其完整的输入输出关系，并进一步推导出其等效的Volterra核。对于一个 $p$ 次多项式[非线性](@entry_id:637147) $f(u) = \sum a_p u^p$，其 $p$ 阶Volterra核 $g_p[\tau_1, \ldots, \tau_p]$ 可以表示为：
$g_p[\tau_1, \ldots, \tau_p] = a_p \sum_{m \in \mathbb{Z}} h_2[m] \prod_{i=1}^{p} h_1[\tau_i - m]$
这个表达式优雅地展示了三个模块的特性是如何共同塑造最终的Volterra核的：$h_1$ 的乘积形式源于第一个LTI模块和[非线性](@entry_id:637147)的幂次，而与 $h_2$ 的卷积（体现为求和）则源于最后一个LTI模块 [@problem_id:2887042]。

### [模型辨识](@entry_id:139651)中的关键问题：[可辨识性](@entry_id:194150)与尺度模糊

即使是对于结构相对简单的块状模型，其辨识过程也并非一帆风顺。一个核心的理论问题是**[可辨识性](@entry_id:194150)**（identifiability），即我们能否从输入输出数据中唯一地确定模型的参数。

以[Wiener模型](@entry_id:188978)为例，它存在固有的**尺度模糊**（scale ambiguity）问题。考虑一个[Wiener模型](@entry_id:188978)对 $(g, f)$，其中 $g$ 是线性滤波器的脉冲响应，$f$ 是[非线性](@entry_id:637147)函数。现在，我们构造一个新的模型对 $(\tilde{g}, \tilde{f})$，其中 $\tilde{g}(\tau) = a \cdot g(\tau)$ 且 $\tilde{f}(x) = f(x/a)$，其中 $a$ 是任意非零常数。让我们来考察新模型的输出。其线性部分的输出为 $\tilde{v}(t) = (\tilde{g} * u)(t) = a \cdot (g * u)(t) = a \cdot v(t)$。再经过[非线性](@entry_id:637147)环节，最终输出为 $\tilde{f}(\tilde{v}(t)) = f(\tilde{v}(t)/a) = f((a \cdot v(t))/a) = f(v(t))$。这与原始模型的输出完全相同。

这意味着，我们无法从输入输出数据中区分 $(g,f)$ 和 $(a \cdot g, f(\cdot/a))$。本质上，我们可以任意地将系统的总增益在LTI模块和NL模块之间进行分配。为了解决这种不确定性，必须引入**归一化**（normalization）约束。一个常见的做法是固定[非线性](@entry_id:637147)函数在原点的斜率，例如，要求 $f'(0) = 1$。这个约束打破了上述的尺度变换关系，从而使得模型参数（在一定条件下）可以被唯一确定。

然而，这种归一化也带来了新的后果。例如，一个经过归一化（$f'(0)=1$）的[Wiener模型](@entry_id:188978)类，在保持LTI模块不变的情况下，对于外部的输出缩放操作 $y_c(t) = c \cdot y(t)$ ($c \neq 1$) 是不封闭的。这是因为新的等效[非线性](@entry_id:637147)函数 $\tilde{f}(x) = c \cdot f(x)$ 的导数将变为 $\tilde{f}'(0) = c \cdot f'(0) = c$，不再满足[归一化条件](@entry_id:156486)。这揭示了在[系统辨识](@entry_id:201290)中，为了确保参数的唯一性而施加的约束，可能会改变模型类的代数性质，这是一个在设计辨识算法时必须考虑的深刻权衡 [@problem_id:2887047] [@problem_id:2887116]。