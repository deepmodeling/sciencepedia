## 引言
在现代[控制工程](@entry_id:149859)中，让一个系统的输出精确跟踪预设的参考轨迹是一项核心任务。标准的[线性二次调节器](@entry_id:267871)（LQR）在稳定系统方面表现出色，但当面对恒定的参考信号或外部扰动时，它往往会留下持续的[稳态误差](@entry_id:271143)。这一根本性问题限制了其在需要高精度定位或调节的应用中的效果。如何设计一个既具备LQR最优性又能自动消除稳态误差的鲁棒控制器，是控制理论中一个长期存在的挑战。

本文系统地介绍了带积分作用的[线性二次调节器](@entry_id:267871)（LQI），这是一种优雅而强大的解决方案。通过在控制器中巧妙地引入[跟踪误差](@entry_id:273267)的积分，LQI从结构上保证了[零稳态误差](@entry_id:269428)，而无需精确的系统模型知识。本文将引导您全面掌握LQI的设计与应用。

在接下来的内容中，我们将首先在“原理与机制”一章中深入剖析LQI的数学基础，从积分作用的引入到增广系统的构建，再到保证稳定性的核心条件。随后，在“应用与交叉学科联系”一章，我们将探讨LQI在现实世界中的应用，涵盖参数整定、抗饱和设计、与[状态观测器](@entry_id:268642)的结合，以及如何将其扩展至更复杂的跟踪任务。最后，“动手实践”部分将提供一系列精心设计的编程练习，帮助您将理论知识转化为实际的工程技能。

## 原理与机制

在上一章引言的基础上，本章深入探讨带有积分作用的线性二次[跟踪控制](@entry_id:170442)（LQI）的核心原理与底层机制。我们将从稳态误差问题出发，系统地阐述积分作用的引入、增广系统的构建、[控制器设计](@entry_id:274982)的基本框架，并深入分析其理论基础，包括内部模型原理、[可镇定性](@entry_id:178956)条件，以及在LQR框架下进行最优设计的具体考量。

### [跟踪控制](@entry_id:170442)中的稳态误差问题

在控制理论中，一个核心任务是设计[反馈控制](@entry_id:272052)器，使系统的输出 $y(t)$ 能够精确跟踪一个给定的参考信号 $r(t)$。对于线性时不变（LTI）系统 $\dot{x}=Ax+Bu, y=Cx$，一种基础的控制策略是状态调节器（State Regulator）。其目标是在没有外部参考（即 $r(t) \equiv 0$）的情况下，将系统状态 $x(t)$ 从任意初始条件调节至原点。标准LQR设计通过最小化[代价函数](@entry_id:138681) $J = \int_{0}^{\infty} (x^TQx + u^TRu)dt$ 得到[状态反馈](@entry_id:151441)律 $u(t) = -Kx(t)$，该反馈律通过配置闭环矩阵 $A-BK$ 的[特征值](@entry_id:154894)于左半复平面来实现系统的[渐近稳定](@entry_id:168077)，从而确保 $x(t) \to 0$。在这种调节问题中，[跟踪误差](@entry_id:273267) $e(t)=r(t)-y(t) = -y(t)$ 并不直接出现在[控制器综合](@entry_id:261816)过程中 [@problem_id:2755126]。

然而，当目标是使输出 $y(t)$ 跟踪一个非零的恒定参考 $r$ 时，单纯的[状态反馈](@entry_id:151441)调节器 $u=-Kx$ 会导致问题。由于[闭环系统](@entry_id:270770)是稳定的，其状态将收敛到原点 $x_{ss}=0$，进而导致输出也收敛到 $y_{ss}=Cx_{ss}=0$。此时，[稳态](@entry_id:182458)[跟踪误差](@entry_id:273267)为 $e_{ss} = r - y_{ss} = r$，这显然无法满足跟踪要求。

一种看似直接的改进方法是在反馈律中引入一个基于参考信号的前馈项，构成 $u(t) = -Kx(t) + N_r r(t)$ 的形式。通过精心选择前馈增益 $N_r$，理论上可以实现[零稳态误差](@entry_id:269428)。具体来说，在[稳态](@entry_id:182458)下，我们期望 $0=(A-BK)x_{ss} + BN_r r$ 且 $y_{ss}=Cx_{ss}=r$。由此可解得 $N_r$ 必须满足 $-C(A-BK)^{-1}B N_r = I$。然而，这种方法的成功严重依赖于对系统模型 $(A, B, C)$ 的精确知识。任何模型参数的不确定性或未建模的恒定外部扰动（例如，作用在输入通道的扰动 $\dot{x} = A x + B(u+d)$）都会破坏这种精密的平衡，导致稳态误差重新出现 [@problem_id:2755126]。因此，需要一种更具鲁棒性的结构性方法来确保[零稳态误差](@entry_id:269428)。

### 积分作用：一种消除稳态误差的结构性方法

积分作用提供了一种优雅且鲁棒的解决方案。其核心思想是引入一个新的[状态变量](@entry_id:138790)，该变量是[跟踪误差](@entry_id:273267)的积分。我们定义**积分状态** $z(t)$ 如下：
$$
\dot{z}(t) = e(t) = r(t) - y(t)
$$
这个简单的[微分方程](@entry_id:264184)蕴含着深刻的控制原理。为了使闭环系统最终达到一个稳定的平衡状态（即[稳态](@entry_id:182458)），系统中所有[状态变量](@entry_id:138790)的时间导数都必须收敛到零。具体到积分状态 $z(t)$，其[稳态](@entry_id:182458)条件 $\dot{z}_{ss}=0$ 直接等价于[稳态](@entry_id:182458)[跟踪误差](@entry_id:273267) $e_{ss} = r - y_{ss} = 0$。这意味着，只要我们能设计一个控制器使包含积分状态的整个系统稳定下来，那么系统输出在[稳态](@entry_id:182458)时就必然会精确地等于参考输入。

这种机制的美妙之处在于其**[结构鲁棒性](@entry_id:195302)**。无论系统参数 $(A, B, C)$ 发生何种微小变化，也无论是否存在未知的恒定扰动，只要闭环系统保持稳定，[积分器](@entry_id:261578)就会持续累积误差，直到控制输入 $u(t)$ 产生一个“对抗”分量，足以精确抵消这些不确定性和扰动的影响，最终迫使 $e(t)$ 趋于零。这种能力是单纯的[前馈控制](@entry_id:153676)所不具备的。因此，积分作用是从控制器结构层面保证了[零稳态误差](@entry_id:269428)，而非依赖于参数的精确对消 [@problem_id:2755073]。

### 增广系统：LQI控制的数学框架

为了将[积分控制](@entry_id:270104)纳入到现代[状态空间控制](@entry_id:268565)（特别是LQR）的框架中，我们需要将原系统与[积分器](@entry_id:261578)结合，构建一个**增广系统（Augmented System）**。设原系统状态为 $x \in \mathbb{R}^n$，积分状态为 $z \in \mathbb{R}^p$（其中 $p$ 是输出和参考信号的维度）。我们定义增广状态向量为：
$$
x_a(t) = \begin{pmatrix} x(t) \\ z(t) \end{pmatrix} \in \mathbb{R}^{n+p}
$$
接下来，我们推导这个增广状态的动态方程。其导数为 $\dot{x}_a(t) = \begin{pmatrix} \dot{x}(t) \\ \dot{z}(t) \end{pmatrix}$。根据原系统动力学和积分器的定义，我们有：
$$
\dot{x}(t) = Ax(t) + Bu(t)
$$
$$
\dot{z}(t) = r(t) - y(t) = r(t) - Cx(t)
$$
将这两部分组合起来，我们可以得到：
$$
\dot{x}_a(t) = \begin{pmatrix} Ax(t) + Bu(t) \\ r(t) - Cx(t) \end{pmatrix}
$$
为了将其写成标准的[状态空间](@entry_id:177074)形式 $\dot{x}_a = A_a x_a + B_a u + E_a r$，我们将与 $x_a$ 和 $u$ 相关的项分离出来：
$$
\dot{x}_a(t) = \begin{pmatrix} A  0 \\ -C  0 \end{pmatrix} \begin{pmatrix} x(t) \\ z(t) \end{pmatrix} + \begin{pmatrix} B \\ 0 \end{pmatrix} u(t) + \begin{pmatrix} 0 \\ I \end{pmatrix} r(t)
$$
由此，我们定义了增广系统的[系统矩阵](@entry_id:172230) $A_a$ 和输入矩阵 $B_a$ [@problem_id:2719957] [@problem_id:2755118]：
$$
A_a = \begin{pmatrix} A  0_{n \times p} \\ -C  0_{p \times p} \end{pmatrix}, \quad B_a = \begin{pmatrix} B \\ 0_{p \times m} \end{pmatrix}
$$
这个增广系统是一个更高维度的[LTI系统](@entry_id:271946)。现在，我们的控制问题转化为：为增广系统 $(A_a, B_a)$ 设计一个[状态反馈控制器](@entry_id:203349)。一个自然且强大的选择是应用LQR理论，这种方法被称为**线性二次积分（Linear Quadratic Integral, LQI）控制**。我们为增广系统定义一个二次型代价函数：
$$
J = \int_{0}^{\infty} \left( x_a(t)^T Q_a x_a(t) + u(t)^T R u(t) \right) dt
$$
其中增广状态的权重矩阵 $Q_a$ 通常被构造成分块[对角形式](@entry_id:264850) $Q_a = \mathrm{diag}(Q, Q_i)$，分别对原系统状态 $x$ 的偏差和积分状态 $z$ 的累积进行惩罚。$Q \succeq 0$, $Q_i \succeq 0$ 和 $R \succ 0$ 是标准要求。

求解这个[LQR问题](@entry_id:267315)将得到一个针对增广状态的最优反馈律：
$$
u(t) = -K_a x_a(t) = -\begin{pmatrix} K_x  K_i \end{pmatrix} \begin{pmatrix} x(t) \\ z(t) \end{pmatrix} = -K_x x(t) - K_i z(t)
$$
其中 $K_a = \begin{pmatrix} K_x  K_i \end{pmatrix}$ 是LQR增益矩阵。将此反馈律代入增广系统动力学，我们得到闭环系统的齐次部分的矩阵 $A_{cl}$ [@problem_id:2755118]：
$$
A_{cl} = A_a - B_a K_a = \begin{pmatrix} A  0 \\ -C  0 \end{pmatrix} - \begin{pmatrix} B \\ 0 \end{pmatrix} \begin{pmatrix} K_x  K_i \end{pmatrix} = \begin{pmatrix} A - BK_x  -BK_i \\ -C  0 \end{pmatrix}
$$
$K_x$ 部分起到了传统[状态反馈](@entry_id:151441)的作用，主要用于塑造瞬态响应，而 $K_i$ 部分则将累积误差的[积分反馈](@entry_id:268328)到系统中，是实现[零稳态误差](@entry_id:269428)的核心。

### 内部模型原理：鲁棒跟踪的理论基石

[积分控制](@entry_id:270104)的成功并非偶然，它是一个更深层次理论——**内部模型原理（Internal Model Principle, IMP）**的体现。该原理指出：要使一个控制系统能够鲁棒地（即在模型参数不确定和外部扰动存在的情况下）跟踪一类特定的参考信号并抑制一类特定的扰动，控制器必须在[反馈回路](@entry_id:273536)中包含一个能够生成这些信号的动态模型（称为“外部系统”）。

对于恒定的参考信号 $r$ 和恒定的扰动 $d$，其共同的数学模型是最简单的动力系统：$\dot{w}=0$。在拉普拉斯域中，这个系统的[传递函数](@entry_id:273897)是 $1/s$，即一个纯积分器。因此，IMP要求控制器必须包含一个积分器。我们引入的积分状态 $\dot{z} = r - y$ 正是在[反馈回路](@entry_id:273536)中嵌入了这个 $1/s$ 模型 [@problem_id:2755129]。

当[闭环系统](@entry_id:270770)稳定时，[稳态](@entry_id:182458)的存在性要求系统能够达到一个代数平衡。具体来说，必须存在一个[稳态解](@entry_id:200351) $(x_{ss}, u_{ss})$ 满足以下[方程组](@entry_id:193238) [@problem_id:2755074]：
$$
\begin{cases}
Ax_{ss} + Bu_{ss} + Ed = 0  \text{(系统动态平衡)} \\
Cx_{ss} = r  \text{(零稳态误差)}
\end{cases}
$$
这里我们考虑了可能存在的恒定输入扰动 $d$。这个[方程组](@entry_id:193238)可以写成矩阵形式：
$$
\begin{pmatrix} A  B \\ C  0 \end{pmatrix} \begin{pmatrix} x_{ss} \\ u_{ss} \end{pmatrix} = \begin{pmatrix} -Ed \\ r \end{pmatrix}
$$
为了让这个方程对任意的 $r$ 和 $d$ 都有解，左侧的系数矩阵（即系统的**[Rosenbrock系统矩阵](@entry_id:164744)**在 $s=0$ 处的值）必须具有满行秩。这就是IMP在代数层面的体现。

### LQI [控制器设计](@entry_id:274982)的必要与充分条件

现在我们面临一个核心问题：对于给定的系统 $(A, B, C)$，何时才能设计出一个稳定的[LQI控制器](@entry_id:167548)？答案在于增广系统 $(A_a, B_a)$ 的**[可镇定性](@entry_id:178956)（stabilizability）**。只有当 $(A_a, B_a)$ 可镇定时，我们才能找到一个[反馈增益](@entry_id:271155) $K_a$ 使得闭环矩阵 $A_{cl} = A_a - B_a K_a$ 是Hurwitz的（即所有[特征值](@entry_id:154894)都有负实部）。

通过对增广系统应用PBH（Popov-Belevitch-Hautus）[可镇定性](@entry_id:178956)测试，可以推导出两个基本条件 [@problem_id:2755050]：

1.  **原系统 $(A, B)$ 必须是可镇定的。** 这是显而易见的，如果原系统本身有无法镇定的[不稳定模式](@entry_id:263056)，增加[积分器](@entry_id:261578)也无济于事。

2.  **原系统 $(A, B, C)$ 在 $s=0$ 处不能有[传输零点](@entry_id:175186)（transmission zero）。**  从数学上讲，这意味着[Rosenbrock系统矩阵](@entry_id:164744) $\mathcal{R}(s) = \begin{pmatrix} sI-A  -B \\ C  D \end{pmatrix}$（对于 $D=0$ 的情况）在 $s=0$ 时必须是列满秩的。对于更一般的情况，如[MIMO系统](@entry_id:268566)，条件是 $\mathcal{R}(0)$ 必须是行满秩的，即 $\mathrm{rank}(\mathcal{R}(0)) = n+p$ [@problem_id:2755074]。

如果系统在 $s=0$ 处有一个[传输零点](@entry_id:175186)，这意味着存在一个非零的直流（DC）输入，它产生的输出恰好为零。当控制器试图通过积分作用产生一个直流分量来消除误差时，这个零点会“吞噬”掉[控制信号](@entry_id:747841)，使得控制器无法有效地影响输出，从而导致一个位于 $s=0$ 的不可控模式。这个不可控模式对应于积分器本身，它将无法被稳定。

**一个说明性的反例** [@problem_id:2755092]
考虑一个系统：
$$
A=\begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix}, \quad B=\begin{pmatrix} 0 \\ 1 \end{pmatrix}, \quad C=\begin{pmatrix} 0  1 \end{pmatrix}
$$
该系统 $(A,B)$ 是完全可控的，因此也是可镇定的。然而，其[传递函数](@entry_id:273897)为 $G(s) = C(sI-A)^{-1}B$。
$ (sI-A)^{-1} = \begin{pmatrix} s  -1 \\ 0  s \end{pmatrix}^{-1} = \frac{1}{s^2} \begin{pmatrix} s  1 \\ 0  s \end{pmatrix} = \begin{pmatrix} 1/s  1/s^2 \\ 0  1/s \end{pmatrix} $
$ G(s) = \begin{pmatrix} 0  1 \end{pmatrix} \begin{pmatrix} 1/s  1/s^2 \\ 0  1/s \end{pmatrix} \begin{pmatrix} 0 \\ 1 \end{pmatrix} = \begin{pmatrix} 0  1/s \end{pmatrix} \begin{pmatrix} 0 \\ 1 \end{pmatrix} = 1/s $。
要检查[传输零点](@entry_id:175186)，我们检查Rosenbrock矩阵：
$\det P(s) = \det \begin{pmatrix} s  -1  0 \\ 0  s  -1 \\ 0  1  0 \end{pmatrix} = s \det \begin{pmatrix} s  -1 \\ 1  0 \end{pmatrix} = s(1) = s$。
所以它在 $s=0$ 处有一个[传输零点](@entry_id:175186)。
当构建增广系统时，
$$
A_a = \begin{pmatrix} 0  1  0 \\ 0  0  0 \\ 0  -1  0 \end{pmatrix}, \quad B_a = \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix}
$$
$A_a$ 的[特征值](@entry_id:154894)为 $\{0, 0, 0\}$。PBH测试矩阵在 $\lambda=0$ 处为 $\begin{pmatrix} A_a  B_a \end{pmatrix} = \begin{pmatrix} 0  1  0  0 \\ 0  0  0  1 \\ 0  -1  0  0 \end{pmatrix}$。该[矩阵的秩](@entry_id:155507)为2，小于增广状态维数3。这证实了在 $\lambda=0$ 处存在一个不可控模式。因此，尽管原系统 $(A,B)$ 可控，增广系统 $(A_a, B_a)$ 却由于 $s=0$ 处的[传输零点](@entry_id:175186)而变得不可镇定。

### 权重矩阵的选择：LQI 设计中的关键考量

在确定[LQI控制器](@entry_id:167548)可以被设计之后，接下来的实际问题是如何选择代价函数中的权重矩阵 $Q_a=\mathrm{diag}(Q, Q_i)$ 和 $R$。这些选择不仅影响系统的性能，还与LQR解的存在性和唯一性密切相关 [@problem_id:2755121]。

1.  **输入权重 $R$**: 必须是**对称正定矩阵** ($R \succ 0$)。$R \succeq 0$ 保证了代价函数的凸性，而严格的正定性 $R \succ 0$ 保证了控制能量总是有代价的，这使得标准代数[Riccati方程](@entry_id:184132)（ARE）中的 $R^{-1}$ 项有意义，并确保了[最优控制](@entry_id:138479)[解的唯一性](@entry_id:143619)。

2.  **状态权重 $Q$**: 通常选择为**[对称半正定矩阵](@entry_id:163376)** ($Q \succeq 0$)，用于惩罚原系统状态的偏移。

3.  **积分状态权重 $Q_i$**: 这是LQI设计中最关键的选择。$Q_i$ 必须是**对称正定矩阵** ($Q_i \succ 0$)。虽然 $Q_i \succeq 0$足以保证[代价函数](@entry_id:138681)的[凸性](@entry_id:138568)，但严格的正定性是确保增广系统稳定性的必要条件。原因在于[增广矩阵](@entry_id:150523) $A_a$ 由于[积分器](@entry_id:261578)的引入，必然包含 $p$ 个位于原点的[特征值](@entry_id:154894)。这些模式本身不是渐近稳定的。为了使[LQR控制器](@entry_id:267871)能够稳定它们，这些模式必须通过[代价函数](@entry_id:138681)是**可检测（detectable）**的。如果 $Q_i$ 不是正定的（例如 $Q_i = 0$），那么积分状态 $z$ 的任何变化都不会产生代价，这意味着积分器模式对于[代价函数](@entry_id:138681)是“不可见”的。因此，[LQR控制器](@entry_id:267871)将无法稳定这些模式，可能导致积分状态 $z$ 漂移至无穷。选择 $Q_i \succ 0$ 确保了任何非零的积分状态都会产生代价，从而使得[LQR控制器](@entry_id:267871)必须作用于并稳定这些积分模式。

综上所述，保证一个良好定义的、能产生稳定[闭环系统](@entry_id:270770)的LQI问题的标准权重选择是：$R \succ 0$，$Q \succeq 0$ 以及 $Q_i \succ 0$。

### 一个完整的[LQI控制器](@entry_id:167548)设计实例

让我们通过一个具体的例子来整合上述所有概念 [@problem_id:2719957]。考虑一个单输入单输出（SISO）系统：
$$
\dot{x} = u, \quad y = x \quad (\text{即 } A=0, B=1, C=1)
$$
我们希望设计一个[LQI控制器](@entry_id:167548)。首先检查条件：
- $(A,B)=(0,1)$ 是可控的，因此可镇定。
- 系统[传递函数](@entry_id:273897)为 $G(s) = 1/s$。Rosenbrock矩阵在 $s=0$ 时为 $\begin{pmatrix} -A  -B \\ C  0 \end{pmatrix} = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}$，其[行列式](@entry_id:142978)为1，是满秩的。因此系统在 $s=0$ 没有[传输零点](@entry_id:175186)。
所有条件均满足，可以进行LQI设计。

1.  **构建增广系统**：
    我们遵循 $\dot{z}=r-y$ 的定义，在调节器设计中设 $r=0$ 得到 $\dot{z}=-y=-Cx$。
    $$
    A_a = \begin{pmatrix} A  0 \\ -C  0 \end{pmatrix} = \begin{pmatrix} 0  0 \\ -1  0 \end{pmatrix}, \quad B_a = \begin{pmatrix} B \\ 0 \end{pmatrix} = \begin{pmatrix} 1 \\ 0 \end{pmatrix}
    $$

2.  **定义[LQR问题](@entry_id:267315)**：
    选择[代价函数](@entry_id:138681) $J = \int_{0}^{\infty} (x^2 + q_i z^2 + u^2) dt$。对应的权重矩阵为：
    $$
    Q_a = \begin{pmatrix} 1  0 \\ 0  q_i \end{pmatrix}, \quad R = 1
    $$
    其中 $q_i > 0$。

3.  **求解代数[Riccati方程](@entry_id:184132)（ARE）**：
    ARE为 $A_a^T P + P A_a - P B_a R^{-1} B_a^T P + Q_a = 0$。设对称正定矩阵 $P = \begin{pmatrix} p_{11}  p_{12} \\ p_{12}  p_{22} \end{pmatrix}$。代入各项并化简，得到以下代数方程组：
    $$
    \begin{cases}
    -2p_{12} - p_{11}^2 + 1 = 0 \\
    -p_{22} - p_{11}p_{12} = 0 \\
    -p_{12}^2 + q_i = 0
    \end{cases}
    $$
    为保证[闭环稳定性](@entry_id:265949)，需要 $P$ 是正定解。从第三个方程解得 $p_{12} = \sqrt{q_i}$（选择[正根](@entry_id:199264)以确保稳定性）。代入第一个方程，得到 $p_{11}^2 = 1 - 2\sqrt{q_i}$。为了得到实数解 $p_{11}$，必须有 $1 - 2\sqrt{q_i} \ge 0$，即 $\sqrt{q_i} \le 1/2$。这表明对于这个特定的系统，权重 $q_i$ 不能任意大。*（编者注：此处推导与原文不同，因原文引用案例的定义为 $\dot{z}=y$。采用 $\dot{z}=r-y$ 定义后，ARE方程发生变化，导致解的形式和约束不同。例如，若采用 $\dot{z}=y$，则ARE中第一项为 $2p_{12}$，最终解为 $p_{11}=\sqrt{1+2\sqrt{q_i}}$，对所有 $q_i>0$ 都有解。）*

4.  **计算最优增益**：
    最优增益 $K_a = R^{-1} B_a^T P = \begin{pmatrix} 1  0 \end{pmatrix} P = \begin{pmatrix} p_{11}  p_{12} \end{pmatrix}$。
    代入已解出的值，得到最终的[LQI控制器](@entry_id:167548)增益：
    $$
    K_a = \begin{pmatrix} K_x  K_i \end{pmatrix} = \begin{pmatrix} \sqrt{1 - 2\sqrt{q_i}}  \sqrt{q_i} \end{pmatrix} \quad (\text{在 } 0  q_i \le 1/4 \text{ 时有效})
    $$
    这个显式解清晰地展示了[状态反馈](@entry_id:151441)增益 $K_x$ 和[积分反馈](@entry_id:268328)增益 $K_i$ 是如何由积分项的权重 $q_i$ 决定的。这个例子完整地体现了从理论分析到控制器参数计算的全过程。