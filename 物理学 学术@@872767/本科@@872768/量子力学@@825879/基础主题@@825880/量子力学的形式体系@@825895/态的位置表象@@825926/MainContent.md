## 引言
在量子力学的宏伟画卷中，如何描述一个微观粒子的状态是所有理论的出发点。态的位置表象提供了一种最直观且功能强大的方法：通过一个名为[波函数](@entry_id:147440)（wavefunction）的数学函数$\psi(x, t)$，我们可以描绘出粒子在空间中无所不在的概率性存在。这种表述不仅是[薛定谔波动方程](@entry_id:141604)的核心，也是连接抽象量子世界与可观测物理现象的桥梁。然而，一个关键的问题随之而来：我们如何从这个复数函数中提取出关于粒子位置、动量或能量等具体、可测量的物理信息？一个任意的数学函数都能成为有效的[波函数](@entry_id:147440)吗？

本文旨在系统地回答这些问题，为你构建一个关于位置表象的坚实理解。在第一部分“原理与机制”中，我们将深入探讨[波函数](@entry_id:147440)的概率诠释、物理上可接受的[波函数](@entry_id:147440)必须满足的严格条件，以及如何使用位置和[动量算符](@entry_id:151743)来计算物理量的[期望值](@entry_id:153208)。接下来，在“应用与跨学科联系”部分，我们将展示这一理论框架的强大威力，看它如何被用于分析从[原子结构](@entry_id:137190)到晶体电子行为等多样化的物理系统，并揭示其与统计物理、电磁学等领域的深刻联系。最后，通过“动手实践”环节，你将有机会亲手应用所学知识，解决具体的量子力学问题，从而巩固和深化你的理解。

## 原理与机制

在量子力学中，描述一个粒子在空间中状态的最基本工具是**[波函数](@entry_id:147440) (wavefunction)**。在位置表象中，对于一个沿一维轴运动的无自旋粒子，其状态由一个[复值函数](@entry_id:196054) $\psi(x, t)$ 完全描述，其中 $x$ 是位置坐标，$t$ 是时间。本章将深入探讨位置表象的核心原理与机制，阐明[波函数](@entry_id:147440)的物理意义、它必须满足的数学条件，以及如何利用它来计算可观测量的[期望值](@entry_id:153208)。

### [波函数](@entry_id:147440)及其概率诠释

量子力学的一个核心公设是，[波函数](@entry_id:147440)的模平方代表了粒子在某点被发现的**[概率密度](@entry_id:175496) (probability density)**。具体而言，在时刻 $t$，在位置 $x$ 附近的一个无穷小区间 $dx$ 内发现该粒子的概率 $dP$ 为：

$dP = |\psi(x, t)|^2 dx$

因此，函数 $\rho(x, t) = |\psi(x, t)|^2 = \psi^*(x, t)\psi(x, t)$ 被定义为[概率密度函数](@entry_id:140610)，其中 $\psi^*(x, t)$ 是 $\psi(x, t)$ 的复共轭。

一个重要的推论是，[波函数](@entry_id:147440)中的复相位因子在计算[概率密度](@entry_id:175496)时会消失。例如，考虑一个由[波函数](@entry_id:147440) $\psi(x) = N \exp(ikx) \exp(-|x|/a)$ 描述的粒子，其中 $N$ 是[归一化常数](@entry_id:752675)，$k$ 和 $a$ 是实常数。尽管[波函数](@entry_id:147440)本身是复数，其[概率密度](@entry_id:175496)却是实数。根据定义：

$\rho(x) = |\psi(x)|^2 = |N \exp(ikx) \exp(-|x|/a)|^2 = |N|^2 |\exp(ikx)|^2 |\exp(-|x|/a)|^2$

由于 $k$ 和 $x$ 都是实数，根据[欧拉公式](@entry_id:176440) $\exp(ikx) = \cos(kx) + i\sin(kx)$，我们有 $|\exp(ikx)|^2 = \cos^2(kx) + \sin^2(kx) = 1$。因此，相位因子 $\exp(ikx)$ 对[概率密度](@entry_id:175496)没有贡献，我们得到：

$\rho(x) = |N|^2 \exp(-2|x|/a)$

这表明，具有不同动量信息（由 $k$ 体现）的[波函数](@entry_id:147440)可以拥有相同的空间[概率分布](@entry_id:146404)。[@problem_id:2107974]

由于粒子必然存在于某个地方，将[概率密度](@entry_id:175496)在整个可及空间[内积](@entry_id:158127)分，总概率必须为 1。这个条件被称为**[归一化条件](@entry_id:156486) (normalization condition)**：

$\int_{-\infty}^{\infty} |\psi(x, t)|^2 dx = 1$

一个满足此条件的[波函数](@entry_id:147440)被称为**归一化[波函数](@entry_id:147440) (normalized wavefunction)**。对于任何一个物理上可能的状态，其[波函数](@entry_id:147440)必须是可归一化的。我们可以利用这个条件来确定[波函数](@entry_id:147440)中的待定常数。以上述[波函数](@entry_id:147440)为例，我们要求：

$\int_{-\infty}^{\infty} |N|^2 \exp(-2|x|/a) dx = 1$

由于被积函数是一个[偶函数](@entry_id:163605)，积分可以简化为 $|N|^2 \cdot 2 \int_{0}^{\infty} \exp(-2x/a) dx = 1$。计算这个标准积分得到 $|N|^2 \cdot 2 \cdot (a/2) = 1$，因此 $|N|^2 = 1/a$。最终，归一化后的[概率密度](@entry_id:175496)为 $\rho(x) = \frac{1}{a} \exp(-2|x|/a)$。[@problem_id:2107974]

归一化的积分区间取决于粒子被限制的区域。如果一个粒子被限制在正半轴（$x \ge 0$），那么其[波函数](@entry_id:147440)在 $x  0$ 的区域为零。例如，对于一个在 $x \ge 0$ 区域由 $\psi(x) = N \exp(-\alpha x)$（其中 $\alpha > 0$）描述的粒子，[归一化条件](@entry_id:156486)变为：

$\int_{0}^{\infty} |N \exp(-\alpha x)|^2 dx = 1$

求解该积分，$|N|^2 \int_{0}^{\infty} \exp(-2\alpha x) dx = |N|^2 (\frac{1}{2\alpha}) = 1$，得出归一化常数 $N = \sqrt{2\alpha}$（通常取正实数解）。[@problem_id:2108004]

### 物理上可接受[波函数](@entry_id:147440)的条件

并非任何数学函数都可以代表一个物理状态。一个物理上可接受的[波函数](@entry_id:147440) $\psi(x)$ 必须满足一系列“良好行为”的条件。这些条件源于[波函数](@entry_id:147440)的概率诠释以及量子力学理论的[自洽性](@entry_id:160889)要求。

最基本、最根本的条件是[波函数](@entry_id:147440)必须是**平方可积 (square-integrable)** 的。这意味着积分 $\int |\psi(x)|^2 dx$ 的结果必须是一个有限值。只有这样，[波函数](@entry_id:147440)才可以通过乘以一个常数来进行归一化，从而使总概率为 1。如果一个函数的模平方在整个空间中的积分发散到无穷大，那么它就不能代表一个局域粒子，因为它无法被归一化，其概率诠释也因此失效。

一个极具启发性的反例是考虑一个被限制在 $(0, L)$ 区间内的粒子，其[波函数](@entry_id:147440)被假设为 $\psi(x) = C \tan(kx)$，其中 $k = \pi/L$。这个函数巧妙地满足了边界条件 $\psi(0)=0$ 和 $\psi(L)=0$。然而，它并非一个物理上可接受的[波函数](@entry_id:147440)。为了检验其有效性，我们考察其平方可积性：

$\int_0^L |\psi(x)|^2 dx = |C|^2 \int_0^L \tan^2(kx) dx$

当 $x$ 从 $0$ 遍历到 $L$ 时，参数 $kx$ 从 $0$ 遍历到 $\pi$。在 $x=L/2$ 处，$kx = \pi/2$，此时 $\tan(kx)$ 函数存在一个垂直渐近线，趋向于无穷大。这意味着[波函数](@entry_id:147440)本身在区间内的一个点上是发散的。对该点附近的积分 $\int_{L/2-\epsilon}^{L/2+\epsilon} \tan^2(kx) dx$ 进行计算，会发现其结果发散。因此，整个积分 $\int_0^L |\psi(x)|^2 dx$ 也是发散的。由于该[波函数](@entry_id:147440)不是平方可积的，它无法被归一化，不能代表一个物理态。[@problem_id:2108005]

除了平方[可积性](@entry_id:142415)，其他通常被要求的条件包括：
1.  **[单值性](@entry_id:174849) (Single-valued)**：在空间的每一点，$|\psi(x)|^2$ 必须有一个唯一确定的值，因为粒子在某点的[概率密度](@entry_id:175496)不能是模棱两可的。
2.  **有限性 (Finite)**：[波函数](@entry_id:147440)在任何地方都必须是有限的。如 $\tan(kx)$ 的例子所示，一个发散的[波函数](@entry_id:147440)直接导致了其不可归一化。
3.  **连续性 (Continuous)**：通常要求[波函数](@entry_id:147440) $\psi(x)$ 本身是连续的。一个不连续的[波函数](@entry_id:147440)可能意味着无限大的动能，这在物理上是不现实的，除非在[势能](@entry_id:748988)无限大的点上。
4.  **[一阶导数](@entry_id:749425)的连续性 (Continuous first derivative)**：$\frac{d\psi}{dx}$ 的连续性与动能的有限性有关。在[势能](@entry_id:748988) $V(x)$ 是有限的区域，要求 $\frac{d\psi}{dx}$ 必须连续。在势能为无穷大的[边界点](@entry_id:176493)，这个条件可以放宽。

在这些条件中，**平方可积性**是最为根本的物理要求，因为它直接关系到[量子力学概率](@entry_id:272484)诠释的根基。

### 位置表象中的[算符与可观测量](@entry_id:262342)

在量子力学中，每一个经典力学中的物理量（如位置、动量、能量）都对应一个线性**[厄米算符](@entry_id:153410) (Hermitian operator)**。在位置表象中，这些算符作用在[波函数](@entry_id:147440) $\psi(x)$ 上。

最基本的两个算符是**位置算符 ($\hat{x}$)** 和**动量算符 ($\hat{p}$)**：
-   位置算符的作用是简单地乘以位置坐标 $x$：$\hat{x}\psi(x) = x\psi(x)$
-   [动量算符](@entry_id:151743)则是一个[微分](@entry_id:158718)算符：$\hat{p}\psi(x) = -i\hbar \frac{d}{dx}\psi(x)$，其中 $\hbar$ 是约化普朗克常数，$i$ 是虚数单位。

一个特殊的状态被称为算符 $\hat{A}$ 的**[本征态](@entry_id:149904) (eigenstate)**，如果算符作用于该态上，结果等于一个常数（称为**[本征值](@entry_id:154894) (eigenvalue)** $a$）乘以原来的状态：

$\hat{A}\psi(x) = a\psi(x)$

本征态的物理意义是：如果一个系统处于算符 $\hat{A}$ 的[本征态](@entry_id:149904) $\psi(x)$，那么对该系统测量物理量 $A$，其结果将确定地是[本征值](@entry_id:154894) $a$。

然而，一个任意的[量子态](@entry_id:146142)通常不是某个算符的[本征态](@entry_id:149904)。例如，考虑一个由波包 $\psi(x) = A \cos(kx) \exp\left(-\frac{x^2}{2\sigma^2}\right)$ 描述的粒子。我们可以通过将动量算符作用于它来检验它是否为动量[本征态](@entry_id:149904)：

$\hat{p}\psi(x) = -i\hbar \frac{d}{dx} \left[A \cos(kx) \exp\left(-\frac{x^2}{2\sigma^2}\right)\right]$
$= -i\hbar A \left[ -k\sin(kx)\exp\left(-\frac{x^2}{2\sigma^2}\right) - \frac{x}{\sigma^2}\cos(kx)\exp\left(-\frac{x^2}{2\sigma^2}\right) \right]$
$= i\hbar A \exp\left(-\frac{x^2}{2\sigma^2}\right) \left[ k\sin(kx) + \frac{x}{\sigma^2}\cos(kx) \right]$

得到的结果函数在形式上与原始的 $\psi(x)$ 完全不同，它无法被写成一个常数乘以 $\psi(x)$ 的形式。因此，该状态不是动量[本征态](@entry_id:149904)。这意味着，对此状态进行动量测量，结果不是一个确定的值，而是会得到一个[概率分布](@entry_id:146404)。实际上，这个[波函数](@entry_id:147440)可以被看作是许多不同动量的平面[波的叠加](@entry_id:166456)。[@problem_id:2107991]

算符之间的**对易子 (commutator)** 揭示了相应物理量之间深刻的关系。两个算符 $\hat{A}$ 和 $\hat{B}$ 的对易子定义为 $[\hat{A}, \hat{B}] = \hat{A}\hat{B} - \hat{B}\hat{A}$。如果对易子不为零，则称这两个算符不对易，其对应的物理量不能同时被精确测量，这正是海森堡不确定性原理的数学体现。

位置和动量算符的对易关系是量子力学的基石：$[\hat{x}, \hat{p}] = i\hbar$。我们可以通过将对易子作用于一个任意测试函数 $\psi(x)$ 来验证更复杂的对易关系。例如，计算 $[\hat{x}^2, \hat{p}^2]\psi(x)$：

$[\hat{x}^2, \hat{p}^2]\psi(x) = \hat{x}^2\hat{p}^2\psi(x) - \hat{p}^2\hat{x}^2\psi(x)$

其中 $\hat{p}^2\psi(x) = (-i\hbar \frac{d}{dx})^2 \psi(x) = -\hbar^2 \frac{d^2\psi(x)}{dx^2}$。
第一项为 $\hat{x}^2\hat{p}^2\psi(x) = -\hbar^2 x^2 \frac{d^2\psi}{dx^2}$。
第二项需要使用链式法则：
$\hat{p}^2(\hat{x}^2\psi) = -\hbar^2 \frac{d^2}{dx^2}(x^2\psi) = -\hbar^2 \frac{d}{dx}(2x\psi + x^2\frac{d\psi}{dx}) = -\hbar^2 (2\psi + 4x\frac{d\psi}{dx} + x^2\frac{d^2\psi}{dx^2})$。
将两者相减，含有 $x^2\frac{d^2\psi}{dx^2}$ 的项相互抵消，得到：

$[\hat{x}^2, \hat{p}^2]\psi(x) = \hbar^2 (2\psi + 4x\frac{d\psi}{dx}) = (4i\hbar \hat{x}\hat{p} + 2\hbar^2)\psi(x)$

这个结果表明，算符 $\hat{x}^2$ 和 $\hat{p}^2$ 也是不对易的。[@problem_id:2107978]

### [期望值](@entry_id:153208)与对称性

对于一个不处于算符 $\hat{A}$ 本征态的系统，测量物理量 $A$ 的结果是不确定的。然而，我们可以计算多次测量结果的统计平均值，即**[期望值](@entry_id:153208) (expectation value)**，记为 $\langle \hat{A} \rangle$。其计算公式为：

$\langle \hat{A} \rangle = \int_{-\infty}^{\infty} \psi^*(x) \hat{A} \psi(x) dx$

对称性在量子力学计算中扮演着至关重要的角色，它常常能够极大地简化[期望值](@entry_id:153208)的计算。一个常见的对称性是宇称（奇偶性）。如果一个[波函数](@entry_id:147440)是偶函数，即 $\psi(x) = \psi(-x)$，那么其[概率密度](@entry_id:175496) $|\psi(x)|^2$ 也必然是偶函数。在这种情况下，位置的[期望值](@entry_id:153208) $\langle x \rangle$ 必定为零。

$\langle x \rangle = \int_{-\infty}^{\infty} x |\psi(x)|^2 dx$

被积函数 $f(x) = x |\psi(x)|^2$ 是一个[奇函数](@entry_id:173259)（奇函数 $x$ 与偶函数 $|\psi(x)|^2$ 的乘积）。一个奇函数在对称区间 $(-\infty, \infty)$ 上的积分恒为零。因此，对于任何一个宇称为偶的态，粒子位置的平均值就在原点。例如，一个由两个对称[高斯波包](@entry_id:151158)叠加而成的态 $\psi(x) = N [ \exp(-\frac{(x-x_0)^2}{4\alpha^2}) + \exp(-\frac{(x+x_0)^2}{4\alpha^2}) ]$ 是一个偶函数，因此无需进行复杂的积分计算，我们就可以断定其[位置期望值](@entry_id:171721)为 $\langle x \rangle = 0$。[@problem_id:2107996]

类似地，动量[期望值](@entry_id:153208) $\langle p \rangle$ 也与[波函数](@entry_id:147440)的性质密切相关。对于任何一个**纯实数**的归一化[波函数](@entry_id:147440) $\psi(x)$，其动量[期望值](@entry_id:153208)也为零。这可以通过[分部积分](@entry_id:136350)证明：

$\langle p \rangle = \int_{-\infty}^{\infty} \psi(x) (-i\hbar \frac{d}{dx}) \psi(x) dx = -i\hbar \int_{-\infty}^{\infty} \psi \frac{d\psi}{dx} dx = -\frac{i\hbar}{2} \int_{-\infty}^{\infty} \frac{d(\psi^2)}{dx} dx = -\frac{i\hbar}{2} [\psi^2]_{-\infty}^{\infty}$

对于一个局域化的粒子，[波函数](@entry_id:147440)在无穷远处必须趋于零，所以上式结果为 0。

当[波函数](@entry_id:147440)是复数时，动量[期望值](@entry_id:153208)通常不为零。一个非零的动量[期望值](@entry_id:153208)来源于[波函数](@entry_id:147440)不同部分之间的[量子干涉](@entry_id:139127)。考虑一个由偶函数 $\psi_1(x) = N_1 \exp(-ax^2)$ 和[奇函数](@entry_id:173259)（乘以 $i$）$\psi_2(x) = i N_2 x \exp(-bx^2)$ 叠加而成的态 $\Psi(x) = \frac{1}{\sqrt{2}}(\psi_1(x) + \psi_2(x))$。其动量[期望值](@entry_id:153208)为：

$\langle p \rangle = \frac{1}{2} ( \langle \psi_1|p|\psi_1 \rangle + \langle \psi_2|p|\psi_2 \rangle + \langle \psi_1|p|\psi_2 \rangle + \langle \psi_2|p|\psi_1 \rangle )$

如前所述，对角项 $\langle \psi_1|p|\psi_1 \rangle$ 和 $\langle \psi_2|p|\psi_2 \rangle$ 均为零。动量[期望值](@entry_id:153208)完全由**[交叉](@entry_id:147634)项** $\langle \psi_1|p|\psi_2 \rangle + \langle \psi_2|p|\psi_1 \rangle$ 贡献。这些[交叉](@entry_id:147634)项代表了态的实部和虚部之间的干涉，正是这种干涉导致了净的动量流。通过直接计算，可以得到一个依赖于参数 $a$ 和 $b$ 的非零结果，这清晰地展示了[量子干涉](@entry_id:139127)在决定物理可观测量中的核心作用。[@problem_id:2107990]

### [概率流密度](@entry_id:152013)

[概率密度](@entry_id:175496)的概念是静态的，它描述了在某一时刻粒子在各处的概率。为了描述概率随时间的动态演化，我们引入**[概率流密度](@entry_id:152013) (probability current density)**，记为 $j(x, t)$。它描述了单位时间内通过某一点 $x$ 的概率“流量”。[概率密度](@entry_id:175496)和[概率流密度](@entry_id:152013)由**连续性方程 (continuity equation)** 联系在一起：

$\frac{\partial \rho}{\partial t} + \frac{\partial j}{\partial x} = 0$

这个方程表达了概率的[局域守恒](@entry_id:751393)：一个区域内概率的减少必然伴随着流出该区域的概率流。从薛定谔方程可以推导出[概率流密度](@entry_id:152013)的表达式：

$j(x) = \frac{\hbar}{2mi} \left( \psi^* \frac{d\psi}{dx} - \psi \frac{d\psi^*}{dx} \right) = \frac{\hbar}{m} \operatorname{Im}\left[ \psi^* \frac{d\psi}{dx} \right]$

其中 $\operatorname{Im}[\cdot]$ 表示取复数的虚部。

让我们将此公式应用于一个由向右传播的平面波和向左传播的[平面波](@entry_id:189798)叠加而成的态：$\psi(x) = A \exp(ikx) + B \exp(-ikx)$，其中 $A$ 和 $B$ 是实常数。
首先计算 $\psi^*$ 和 $\frac{d\psi}{dx}$：
$\psi^*(x) = A \exp(-ikx) + B \exp(ikx)$
$\frac{d\psi}{dx} = ikA \exp(ikx) - ikB \exp(-ikx)$

然后计算它们的乘积：
$\psi^* \frac{d\psi}{dx} = (A \exp(-ikx) + B \exp(ikx))(ikA \exp(ikx) - ikB \exp(-ikx))$
$= ik(A^2 - B^2) + ikAB(\exp(2ikx) - \exp(-2ikx)) = ik(A^2 - B^2) - 2kAB\sin(2kx)$

该表达式的虚部为 $k(A^2 - B^2)$。因此，[概率流密度](@entry_id:152013)为：

$j(x) = \frac{\hbar k}{m} (A^2 - B^2)$

这个结果具有清晰的物理解释：$\frac{\hbar k}{m}$ 是动量为 $p=\hbar k$ 的粒子的速度。$A^2$ 正比于向右运动的粒子流，而 $B^2$ 正比于向左运动的粒子流。总的净概率流是两者之差，并且它不依赖于位置 $x$，这对于一个定态是合理的。[@problem_id:2108007]

### 不同表象之间的联系

位置表象只是描述[量子态](@entry_id:146142)的多种方式之一。同一个[量子态](@entry_id:146142)也可以在其他表象中描述，例如[动量表象](@entry_id:156131)或能量表象。这些表象通过数学变换相互关联。

**位置表象与[动量表象](@entry_id:156131)**
一个态在位置空间的[波函数](@entry_id:147440) $\psi(x)$ 和在动量空间的[波函数](@entry_id:147440) $\phi(p)$ 通过**[傅里叶变换](@entry_id:142120) (Fourier transform)** 对相互联系：

$\psi(x) = \frac{1}{\sqrt{2\pi\hbar}} \int_{-\infty}^{\infty} \phi(p) \exp\left(\frac{ipx}{\hbar}\right) dp$
$\phi(p) = \frac{1}{\sqrt{2\pi\hbar}} \int_{-\infty}^{\infty} \psi(x) \exp\left(-\frac{ipx}{\hbar}\right) dx$

这种关系体现了位置和动量的[不确定性原理](@entry_id:141278)。例如，一个在[动量空间](@entry_id:148936)中被精确确定的态，在位置空间中会完全[离域](@entry_id:183327)。
考虑一个动量[波函数](@entry_id:147440)为两个狄拉克 $\delta$ 函数之和的态：$\phi(p) = N[\delta(p - p_0) + \delta(p + p_0)]$。这意味着该粒子只可能被测得动量为 $+p_0$ 或 $-p_0$。其对应的位置[波函数](@entry_id:147440)为：

$\psi(x) = \frac{N}{\sqrt{2\pi\hbar}} \int_{-\infty}^{\infty} [\delta(p - p_0) + \delta(p + p_0)] \exp\left(\frac{ipx}{\hbar}\right) dp$
$= \frac{N}{\sqrt{2\pi\hbar}} \left[ \exp\left(\frac{ip_0x}{\hbar}\right) + \exp\left(-\frac{ip_0x}{\hbar}\right) \right] = \frac{2N}{\sqrt{2\pi\hbar}} \cos\left(\frac{p_0x}{\hbar}\right)$

这是一个余弦函数，即一个[驻波](@entry_id:148648)。其[概率密度](@entry_id:175496) $|\psi(x)|^2 \propto \cos^2(p_0x/\hbar)$。$\cos^2(\theta)$ 函数的周期是 $\pi$，因此我们要求 $\frac{p_0 L}{\hbar} = \pi$，其中 $L$ 是概率密度的空间周期。解得 $L = \frac{\pi\hbar}{p_0}$。这个结果清晰地表明，动量空间中的一个特定属性（动量大小 $p_0$）直接决定了位置空间中的一个周期性结构。[@problem_id:2107969]

**位置表象与能量表象**
对于一个给定的势场，薛定谔方程的[定态](@entry_id:137260)解（[能量本征态](@entry_id:152154)）$\psi_n(x)$ 构成一个完备的[正交基](@entry_id:264024)。这意味着任何一个物理上可接受的态 $\Phi(x)$ 都可以表示为这些[能量本征态](@entry_id:152154)的线性叠加：

$\Phi(x) = \sum_n c_n \psi_n(x)$

其中 $c_n$ 是复数系数。这个系数的物理意义是，当对处于 $\Phi(x)$ 态的系统进行能量测量时，测得[能量本征值](@entry_id:144381) $E_n$ 的**[概率幅](@entry_id:150609) (probability amplitude)**。测得能量 $E_n$ 的概率 $P_n$ 就是该系数的模平方：

$P_n = |c_n|^2$

由于[能量本征态](@entry_id:152154)是正交的（$\int \psi_m^*(x)\psi_n(x)dx = \delta_{mn}$），我们可以通过将态函数 $\Phi(x)$ 投影到[本征态](@entry_id:149904) $\psi_n(x)$ 上来计算系数 $c_n$：

$c_n = \langle \psi_n | \Phi \rangle = \int_{-\infty}^{\infty} \psi_n^*(x) \Phi(x) dx$

作为一个综合性应用，考虑一个宽度为 $L$ 的[一维无限深势阱](@entry_id:271157)，其能量本征态为 $\psi_n(x)$。假设粒子初始处于一个非[定态](@entry_id:137260) $\Phi(x)$，该态与[基态](@entry_id:150928) $\psi_1(x)$ 和位置 $x$ 的乘积成正比，即 $\Phi(x) \propto x\psi_1(x)$。要计算测量到第一[激发态](@entry_id:261453)能量 $E_2$ 的概率，我们需要计算 $P_2 = |c_2|^2$。

首先，对初始态进行归一化：$\Phi_{\text{norm}}(x) = \frac{x\psi_1(x)}{\sqrt{\int |x\psi_1(x)|^2 dx}} = \frac{x\psi_1(x)}{\sqrt{\langle x^2 \rangle_1}}$，其中 $\langle x^2 \rangle_1$ 是[基态](@entry_id:150928)的位置平方[期望值](@entry_id:153208)。
然后，计算投影系数 $c_2$：
$c_2 = \langle \psi_2 | \Phi_{\text{norm}} \rangle = \frac{\langle \psi_2 | x | \psi_1 \rangle}{\sqrt{\langle x^2 \rangle_1}}$

这个计算涉及到两个关键积分：跃迁矩阵元 $\langle \psi_2 | x | \psi_1 \rangle = \int \psi_2^*(x) x \psi_1(x) dx$ 和[期望值](@entry_id:153208) $\langle x^2 \rangle_1 = \int \psi_1^*(x) x^2 \psi_1(x) dx$。对于[无限深势阱](@entry_id:140940)，这些积分可以通过标准的积分技术求得。最终得到的概率 $P_2 = \frac{|\langle \psi_2 | x | \psi_1 \rangle|^2}{\langle x^2 \rangle_1}$ 是一个仅依赖于 $\pi$ 的纯数字。这个过程完美地整合了本章的多个核心概念：归一化、算符、[期望值](@entry_id:153208)、以及在不同基（位置基和能量基）之间的转换，展示了位置表象作为进行量子力学计算的强大框架。[@problem_id:2107959]