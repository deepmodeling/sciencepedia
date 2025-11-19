## 引言
在[经典物理学](@entry_id:150394)的世界里，空间是舞台，时间是普适的节拍器，两者各自独立且绝对。然而，20世纪初，[狭义相对论](@entry_id:275552)的[光速不变](@entry_id:265351)和[相对性原理](@entry_id:271855)两大支柱，彻底动摇了这一牛顿式的宇宙观。一个核心的矛盾浮出水面：如果光速对所有观察者都一样，那么空间和时间的测量必然是相对的。这就需要一个全新的数学框架来描述这个统一但又相对的物理实在。这个问题，即如何调和相对的同时性与不变的物理定律，正是本文所要解决的知识缺口。

本文旨在深入剖析解决这一问题的关键——[闵可夫斯基度规](@entry_id:154660)。它不仅是一个数学公式，更是理解时空作为一个统一实体的语言。通过学习本文，你将掌握时空几何的精髓。我们将首先在“原则与机制”一章中，揭示[闵可夫斯基度规](@entry_id:154660)如何定义不变的时空间隔，并由此确立宇宙的因果律。接着，在“应用与跨学科联系”中，我们将探索这一强大工具如何在[相对论电动力学](@entry_id:160964)、粒子物理和[场论](@entry_id:155241)中大放异彩，甚至成为通向广义相对论的桥梁。最后，通过“动手实践”环节，你将有机会亲自运用这些概念来解决具体的物理问题，从而巩固你的理解。

## 原则与机制

在前一章中，我们介绍了[狭义相对论](@entry_id:275552)的基本假设，即[光速不变原理](@entry_id:201268)和[相对性原理](@entry_id:271855)。这些假设彻底改变了我们对空间和时间的理解，将它们从各自独立的实体融合成一个统一的四维结构——时空。本章将深入探讨描述这一时空几何的数学框架的核心：[闵可夫斯基度规](@entry_id:154660)。我们将阐明它是如何定义[不变量](@entry_id:148850)、决定因果结构，并为[相对论动力学](@entry_id:264218)和电磁学奠定基础的。

### [时空间隔](@entry_id:154935)与[闵可夫斯基度规](@entry_id:154660)

在[经典物理学](@entry_id:150394)中，空间距离和时间间隔是绝对的。对于任何两位惯性观察者，他们测量的两个事件之间的空间距离和时间间隔可能不同，但如果他们对欧几里得空间和通用时间的观念是正确的，那么经过简单的伽利略变换，他们总能就物理定律达成一致。然而，[光速不变原理](@entry_id:201268)打破了这一经典图景。为了保持所有惯性系中光速恒定，我们必须放弃绝对的时间和空间。

取而代之的是一个在洛伦兹变换下保持不变的量，称为 **[时空间隔](@entry_id:154935) (spacetime interval)**。对于两个事件，如果它们在某一[惯性系](@entry_id:266190)中的时空坐标差为 $(\Delta t, \Delta x, \Delta y, \Delta z)$，那么它们之间的[时空间隔](@entry_id:154935)平方 $\Delta s^2$ 定义为：

$$
\Delta s^2 = (c\Delta t)^2 - ((\Delta x)^2 + (\Delta y)^2 + (\Delta z)^2)
$$

其中 $c$ 是[真空中的光速](@entry_id:272753)。这个表达式酷似欧几里得距离公式的推广，但关键的区别在于时间分量和空间分量之间存在一个负号。这个负号是时空几何与我们熟悉的三维[欧几里得几何](@entry_id:634933)的根本区别。

为了以更系统和强大的方式处理时空几何，我们引入 **[闵可夫斯基度规](@entry_id:154660) (Minkowski metric)** 张量，记为 $\eta_{\mu\nu}$。它是一个 $4 \times 4$ 的矩阵，用于定义如何计算时空中的“距离”。我们将遵循物理学中常见的 **[度规符号差](@entry_id:265893) (metric signature)** $(+,-,-,-)$ 约定，这意味着时间分量为正，而空间分量为负。在此约定下，[闵可夫斯基度规张量](@entry_id:180802)的矩阵形式为 [@problem_id:1511976]：

$$
\eta_{\mu\nu} = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & -1 & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 0 & 0 & -1 \end{pmatrix}
$$

使用这个度规，我们可以将时空间隔的计算写成一种更紧凑的张量形式。首先，我们将两个事件之间的时空坐标差定义为一个 **四维[位移矢量](@entry_id:262782) (displacement 4-vector)**，$\Delta x^\mu = (c\Delta t, \Delta x, \Delta y, \Delta z)$。那么，[时空间隔](@entry_id:154935)的平方可以通过以下方式计算，这里我们使用了爱因斯坦求和约定（即对重复出现的上下指标求和）：

$$
\Delta s^2 = \eta_{\mu\nu} \Delta x^\mu \Delta x^\nu
$$

展开这个表达式，我们得到 $\Delta s^2 = \eta_{00} (\Delta x^0)^2 + \eta_{11} (\Delta x^1)^2 + \eta_{22} (\Delta x^2)^2 + \eta_{33} (\Delta x^3)^2 = (c\Delta t)^2 - (\Delta x)^2 - (\Delta y)^2 - (\Delta z)^2$，这与我们最初的定义完全一致。

作为一个具体的计算示例，考虑两个爆炸事件 [@problem_id:1868492]。事件1发生在 $t_1 = 5.000 \text{ s}$，位置为 $(1.200 \times 10^8 \text{ m}, 0.500 \times 10^8 \text{ m}, 0)$。事件2发生在 $t_2 = 5.400 \text{ s}$，位置为 $(2.150 \times 10^8 \text{ m}, 1.700 \times 10^8 \text{ m}, 0)$。首先计算坐标差：

$\Delta t = 0.400 \text{ s}$
$\Delta x = 0.950 \times 10^8 \text{ m}$
$\Delta y = 1.200 \times 10^8 \text{ m}$
$\Delta z = 0 \text{ m}$

使用光速 $c = 2.998 \times 10^8 \text{ m/s}$，时间分量 $c\Delta t = 1.1992 \times 10^8 \text{ m}$。时空间隔平方为：

$$
\Delta s^2 = (1.1992 \times 10^8)^2 - (0.950 \times 10^8)^2 - (1.200 \times 10^8)^2 - 0^2 \approx -9.04 \times 10^{15} \text{ m}^2
$$

这个结果的负号具有深刻的物理意义，我们将在下一节中探讨。值得注意的是，虽然我们在这里使用了 $(+,-,-,-)$ 符号差，但一些文献（尤其是在广义相对论中）会使用 $(-,+,+,+)$ 约定。在这种情况下，$\Delta s^2$ 的定义会整体反号，但所有基于其符号的物理结论（如因果关系）都保持不变。

### [时空的因果结构](@entry_id:199989)

[闵可夫斯基度规](@entry_id:154660)最深刻的含义之一是它定义了时空的 **[因果结构](@entry_id:159914) (causal structure)**。两个事件之间的关系不是绝对的，而是取决于它们之间的时空间隔的符号。

**[类时间隔](@entry_id:276041) (Timelike Interval, $\Delta s^2 > 0$)**
如果 $\Delta s^2 > 0$，则 $(c\Delta t)^2 > (\Delta x)^2 + (\Delta y)^2 + (\Delta z)^2$。这意味着时间间隔足够长，以至于一个速度小于光速的物理信号可以从一个事件的位置传播到另一个事件的位置。因此，这两个事件是 **有因果联系的 (causally connected)**。一个事件可以影响另一个事件。
至关重要的是，对于[类时间隔](@entry_id:276041)，所有惯性观察者都会就事件的时间顺序达成一致。也就是说，如果在一个[参考系](@entry_id:169232) $S$ 中，$\Delta t = t_B - t_A > 0$，那么在任何其他以速度 $v < c$ 相对 $S$ 运动的[参考系](@entry_id:169232) $S'$ 中，测得的时间间隔 $\Delta t'$ 也必定为正。我们可以证明这一点 [@problem_id:1834204]。根据[洛伦兹变换](@entry_id:176827)，$\Delta t' = \gamma (\Delta t - \frac{v \Delta x}{c^2})$。因为间隔是类时的，我们有 $c|\Delta t| > |\Delta x|$。因此，$\frac{v |\Delta x|}{c^2} < \frac{c |\Delta x|}{c^2} = \frac{|\Delta x|}{c} < |\Delta t|$。这意味着 $\Delta t - \frac{v \Delta x}{c^2}$ 的符号与 $\Delta t$ 相同，而[洛伦兹因子](@entry_id:159588) $\gamma$ 总是正的。因此，$\Delta t'$ 的符号与 $\Delta t$ 相同。时间的箭头对于类时事件是绝对的，这保障了因果律的[逻辑一致性](@entry_id:637867)。

**[类空间隔](@entry_id:183831) (Spacelike Interval, $\Delta s^2 < 0$)**
如果 $\Delta s^2 < 0$，则 $(c\Delta t)^2 < (\Delta x)^2 + (\Delta y)^2 + (\Delta z)^2$。这意味着即使以光速传播的信号，也没有足够的时间从一个事件的位置到达另一个事件的位置。这两个事件是 **因果无关的 (causally disconnected)**。它们不可能相互影响。
对于[类空间隔](@entry_id:183831)，事件的时间顺序是相对的。一个观察者可能会看到事件A先于事件B发生，而另一个观察者可能会看到B先于A发生。更引人注目的是，总能找到一个特定的[惯性参考系](@entry_id:276742)，在其中这两个事件是 **同时发生的 (simultaneous)** [@problem_id:1834161]。如果事件A在原点 $(0, \vec{0})$，事件B在 $(T, \vec{R})$，且满足 $| \vec{R} |^2 > (cT)^2$，那么一个以速度 $\vec{v}$ 运动的观察者测量到的时间差为 $\Delta t' = \gamma (T - \frac{\vec{v} \cdot \vec{R}}{c^2})$。为了使 $\Delta t' = 0$，我们只需要找到一个速度 $\vec{v}$ 使得 $\vec{v} \cdot \vec{R} = c^2 T$。一个简单的解是让 $\vec{v}$ 平行于 $\vec{R}$，即 $\vec{v} = \frac{c^2 T}{|\vec{R}|^2} \vec{R}$。由于间隔是类空的，我们保证了 $|v| = \frac{c^2 |T|}{|\vec{R}|} < c$，所以这样的[参考系](@entry_id:169232)总是物理上可实现的。

**[类光间隔](@entry_id:197063) (Lightlike Interval, $\Delta s^2 = 0$)**
如果 $\Delta s^2 = 0$，则 $(c\Delta t)^2 = (\Delta x)^2 + (\Delta y)^2 + (\Delta z)^2$。这精确地描述了光在真空中传播的轨迹。只有以光速传播的信号才能连接这两个事件。

让我们通过一个例子来巩固这些概念 [@problem_id:1868512]。假设一个星际信标A在 $t_A=2.0$ 年，位置 $(1.0, 3.0, 0.0)$ 光年处发出脉冲。一个深空探测器B在 $t_B=8.0$ 年，位置 $(5.0, 6.0, 0.0)$ 光年处发生故障。脉冲A能引起故障B吗？
坐标差为 $\Delta t = 6.0$ 年，$\Delta x = 4.0$ 光年，$\Delta y = 3.0$ 光年，$\Delta z = 0$。空间距离为 $\Delta d = \sqrt{4.0^2 + 3.0^2} = 5.0$ 光年。
[时空间隔](@entry_id:154935)平方为（注意 $c=1$ 光年/年）：
$$
\Delta s^2 = (c\Delta t)^2 - (\Delta d)^2 = (1 \times 6.0)^2 - (5.0)^2 = 36.0 - 25.0 = 11.0 \text{ ly}^2
$$
由于 $\Delta s^2 > 0$，这是一个[类时间隔](@entry_id:276041)。这意味着因果联系是可能的。信号从A传播到B所需的最小时间（即光速传播）是 $t_{light} = \Delta d / c = 5.0$ 年。实际的时间间隔是 $\Delta t = 6.0$ 年。因为 $\Delta t > t_{light}$，所以一个速度为 $v = \Delta d / \Delta t = 5.0/6.0 c \approx 0.83c$（小于光速）的信号可以从A传到B。因此，信标脉冲完全有可能是导致探测器故障的原因。

### 度规作为几何工具

[闵可夫斯基度规](@entry_id:154660)不仅用于计算两个遥远事件之间的间隔，它还是进行[时空几何](@entry_id:139497)运算的基础工具，尤其是用于 **[升降指标](@entry_id:161292) (raising and lowering indices)**。

在四维时空中，我们区分两种类型的矢量分量：**[逆变分量](@entry_id:185440) (contravariant components)**，通常用上指标表示（如 $V^\mu$），和 **[协变](@entry_id:634097)分量 (covariant components)**，用下指标表示（如 $V_\mu$）。四维位移 $x^\mu = (ct, x, y, z)$ 是一个典型的[逆变](@entry_id:192290)矢量。

度规张量 $\eta_{\mu\nu}$ 的作用就是在这两种分量之间建立联系。给定一个逆变矢量 $A^\mu$，其对应的[协变矢量](@entry_id:263917) $A_\mu$ 通过以下方式获得：

$$
A_\mu = \eta_{\mu\nu} A^\nu
$$

例如，考虑由[标量势](@entry_id:276177) $\phi = -E_0 x$ 和矢量势 $\vec{A} = x B_0 \hat{y}$ 描述的[电磁场](@entry_id:265881) [@problem_id:1834206]。它们可以组合成一个[逆变](@entry_id:192290)[四维势](@entry_id:188407) $A^\mu = (\phi/c, A_x, A_y, A_z)$。代入给定的势，我们得到 $A^\mu = (-E_0 x/c, 0, x B_0, 0)$。
现在我们使用度规 $\eta_{\mu\nu} = \text{diag}(1, -1, -1, -1)$ 来“降低”指标：

$A_0 = \eta_{0\nu} A^\nu = \eta_{00} A^0 = (1)(-\frac{E_0 x}{c}) = -\frac{E_0 x}{c}$
$A_1 = \eta_{1\nu} A^\nu = \eta_{11} A^1 = (-1)(0) = 0$
$A_2 = \eta_{2\nu} A^\nu = \eta_{22} A^2 = (-1)(x B_0) = -x B_0$
$A_3 = \eta_{3\nu} A^\nu = \eta_{33} A^3 = (-1)(0) = 0$

所以，协变[四维势](@entry_id:188407)为 $A_\mu = (-\frac{E_0 x}{c}, 0, -x B_0, 0)$。可以看到，[协变](@entry_id:634097)分量的空间部分的符号与[逆变分量](@entry_id:185440)相反。

这个操作最重要的应用是构造 **[洛伦兹不变量](@entry_id:161821) (Lorentz invariant)**。通过一个逆变矢量和一个[协变矢量](@entry_id:263917)的缩并，我们可以得到一个标量，其值在所有[惯性系](@entry_id:266190)中都相同。例如，两个[四维矢量](@entry_id:275085) $A^\mu$ 和 $B^\mu$ 的[标量积](@entry_id:138996)定义为：

$$
A \cdot B = A_\mu B^\mu = \eta_{\mu\nu} A^\mu B^\nu = A^0 B^0 - \vec{A} \cdot \vec{B}
$$

这个[标量积](@entry_id:138996)的值对于所有惯性观察者都是相同的。

### [相对论动力学](@entry_id:264218)中的[不变量](@entry_id:148850)

利用度规构造[不变量](@entry_id:148850)的能力是建立相对论性物理定律的关键。物理定律必须在所有[惯性系](@entry_id:266190)中形式相同，而基于标量构造的方程自然满足这一要求。

**[固有时](@entry_id:192124) (Proper Time)**
考虑一个沿着其 **[世界线](@entry_id:199036) (worldline)** 运动的粒子。在微小的时间 $dt$ 内，它移动了[无穷小位移](@entry_id:202209) $dx^\mu = (c dt, d\vec{x})$。这个位移对应的时空间隔平方是 $ds^2 = (c dt)^2 - |d\vec{x}|^2$。由于[粒子速度](@entry_id:196946) $v = |d\vec{x}/dt|$ 必须小于 $c$，所以 $ds^2$ 总是正的，即粒子的[世界线](@entry_id:199036)总是类时的。
这个[不变量](@entry_id:148850) $ds^2$ 定义了 **[固有时](@entry_id:192124) (proper time)** $\tau$，即粒子自身携带的时钟所测量的时间。它们的关系是 $ds^2 = (c d\tau)^2$。
将 $ds^2 = (c dt)^2 - (v dt)^2 = (c dt)^2(1 - v^2/c^2)$ 代入，我们得到 $(c d\tau)^2 = (c dt)^2(1 - v^2/c^2)$。由此可直接导出著名的[时间膨胀公式](@entry_id:266668) [@problem_id:1868488]：

$$
\frac{d\tau}{dt} = \sqrt{1 - \frac{v^2}{c^2}} = \frac{1}{\gamma}
$$

这表明，运动时钟（测量 $d\tau$）比静止的[坐标时](@entry_id:263720)钟（测量 $dt$）走得慢。

**[四维速度](@entry_id:269673) (Four-Velocity)**
四维速度 $u^\mu$ 定义为粒子世界线坐标对其固有时 $\tau$ 的导数：$u^\mu = \frac{dx^\mu}{d\tau}$。利用[链式法则](@entry_id:190743)， $u^\mu = \frac{dx^\mu}{dt} \frac{dt}{d\tau} = \gamma \frac{dx^\mu}{dt} = \gamma(c, \vec{v})$。
四维速度的“长度”平方是一个[普适常数](@entry_id:165600)。我们可以通过计算[标量积](@entry_id:138996) $u^\mu u_\mu$ 来验证这一点 [@problem_id:1834214]：

$$
u^\mu u_\mu = \eta_{\mu\nu} u^\mu u^\nu = \gamma^2(c^2 - v^2) = \frac{1}{1 - v^2/c^2} c^2 (1 - v^2/c^2) = c^2
$$

这个结果 $u^\mu u_\mu = c^2$ 是一个[不变量](@entry_id:148850)，它不依赖于粒子的速度，对所有有质量的粒子都成立。

**[四维动量](@entry_id:272346) (Four-Momentum)**
将四维速度乘以粒子的 **[静止质量](@entry_id:264101) (rest mass)** $m_0$（一个[不变量](@entry_id:148850)），我们得到[四维动量](@entry_id:272346) $p^\mu = m_0 u^\mu$。其分量为 $p^\mu = m_0 \gamma (c, \vec{v}) = (E/c, \vec{p})$，其中 $E = \gamma m_0 c^2$ 是总能量，$\vec{p} = \gamma m_0 \vec{v}$ 是相对论三维动量。
四维动量的“长度”平方同样是一个重要的[不变量](@entry_id:148850)，它直接与粒子的[静止质量](@entry_id:264101)相关 [@problem_id:1834203]。

$$
p^\mu p_\mu = \eta_{\mu\nu} p^\mu p^\nu = (E/c)^2 - |\vec{p}|^2
$$

利用能量-动量关系 $E^2 = (|\vec{p}|c)^2 + (m_0 c^2)^2$，我们代入上式：

$$
p^\mu p_\mu = \frac{(|\vec{p}|c)^2 + (m_0 c^2)^2}{c^2} - |\vec{p}|^2 = |\vec{p}|^2 + m_0^2 c^2 - |\vec{p}|^2 = m_0^2 c^2
$$

因此，$p^\mu p_\mu = m_0^2 c^2$。这个[不变量](@entry_id:148850)关系是[相对论动力学](@entry_id:264218)的基石，它将能量、动量和[静止质量](@entry_id:264101)统一在一个几何框架内。[静止质量](@entry_id:264101) $m_0$ 本身被揭示为一个洛伦兹不变量，是粒子[四维动量矢量](@entry_id:172785)“长度”的度量。

### 度规自身的不变性

我们已经看到，[闵可夫斯基度规](@entry_id:154660)是构建所有其他[不变量](@entry_id:148850)的基石。但我们为何能断言时空间隔 $\Delta s^2 = \eta_{\mu\nu} \Delta x^\mu \Delta x^\nu$ 本身就是[不变量](@entry_id:148850)呢？答案在于，[闵可夫斯基度规张量](@entry_id:180802) $\eta_{\mu\nu}$ 的分量在所有[惯性参考系](@entry_id:276742)中都是相同的。
连接不同[惯性系](@entry_id:266190)坐标的变换是 **洛伦兹变换 (Lorentz transformation)**，$x'^\alpha = \Lambda^\alpha_\mu x^\mu$，其中 $\Lambda$ 是变换矩阵。如果间隔在变换前后保持不变，即 $\Delta s'^2 = \Delta s^2$，这意味着：

$$
\eta_{\alpha\beta} \Delta x'^\alpha \Delta x'^\beta = \eta_{\mu\nu} \Delta x^\mu \Delta x^\nu
$$

代入[洛伦兹变换](@entry_id:176827) $ \Delta x'^\alpha = \Lambda^\alpha_\mu \Delta x^\mu$ 和 $ \Delta x'^\beta = \Lambda^\beta_\nu \Delta x^\nu$，我们得到：

$$
\eta_{\alpha\beta} \Lambda^\alpha_\mu \Lambda^\beta_\nu \Delta x^\mu \Delta x^\nu = \eta_{\mu\nu} \Delta x^\mu \Delta x^\nu
$$

由于这对任意 $\Delta x^\mu$ 都成立，我们必须有：

$$
\Lambda^\alpha_\mu \eta_{\alpha\beta} \Lambda^\beta_\nu = \eta_{\mu\nu}
$$

用矩阵语言来说，这等价于 $\Lambda^T \eta \Lambda = \eta$。这正是[洛伦兹变换](@entry_id:176827)的定义：一个保持[闵可夫斯基度规](@entry_id:154660)不变的线性变换。

我们可以通过一个具体的例子来验证这一点。考虑一个沿x轴方向的速度为 $v$ 的标准洛伦兹 boost [@problem_id:1834184]。其变换矩阵 $\Lambda$ 和度规矩阵 $\eta$ 分别是：

$$
\Lambda = \begin{pmatrix} \gamma & -\gamma\beta & 0 & 0 \\ -\gamma\beta & \gamma & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}, \quad \eta = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & -1 & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 0 & 0 & -1 \end{pmatrix}
$$

其中 $\beta = v/c$ 且 $\gamma = (1-\beta^2)^{-1/2}$。进行[矩阵乘法](@entry_id:156035) $\Lambda^T \eta \Lambda$：
首先计算 $\eta \Lambda$:

$$
\eta \Lambda = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & -1 & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 0 & 0 & -1 \end{pmatrix} \begin{pmatrix} \gamma & -\gamma\beta & 0 & 0 \\ -\gamma\beta & \gamma & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix} = \begin{pmatrix} \gamma & -\gamma\beta & 0 & 0 \\ \gamma\beta & -\gamma & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 0 & 0 & -1 \end{pmatrix}
$$

然后左乘 $\Lambda^T$（在此例中 $\Lambda$ 是对称的，所以 $\Lambda^T = \Lambda$）：

$$
\Lambda^T (\eta \Lambda) = \begin{pmatrix} \gamma & -\gamma\beta & 0 & 0 \\ -\gamma\beta & \gamma & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} \gamma & -\gamma\beta & 0 & 0 \\ \gamma\beta & -\gamma & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 0 & 0 & -1 \end{pmatrix}
$$

计算左上角 $2 \times 2$ 子矩阵的元素：
$M_{11} = \gamma(\gamma) + (-\gamma\beta)(\gamma\beta) = \gamma^2(1-\beta^2) = 1$
$M_{12} = \gamma(-\gamma\beta) + (-\gamma\beta)(-\gamma) = -\gamma^2\beta + \gamma^2\beta = 0$
$M_{21} = (-\gamma\beta)(\gamma) + \gamma(\gamma\beta) = -\gamma^2\beta + \gamma^2\beta = 0$
$M_{22} = (-\gamma\beta)(-\gamma\beta) + \gamma(-\gamma) = \gamma^2\beta^2 - \gamma^2 = -\gamma^2(1-\beta^2) = -1$

右下角的 $2 \times 2$ 子矩阵显然是 $\text{diag}(-1, -1)$。因此，我们得到：

$$
\Lambda^T \eta \Lambda = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & -1 & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 0 & 0 & -1 \end{pmatrix} = \eta
$$

这个计算明确地证明了[闵可夫斯基度规](@entry_id:154660)在洛伦兹变换下的[不变性](@entry_id:140168)。正是这一根本属性，使得[时空间隔](@entry_id:154935)成为一个普适的、所有观察者都同意的量，并构成了我们理解相对论世界中物理定律的坚实基础。