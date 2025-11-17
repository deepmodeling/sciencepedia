## 引言
在基础微积分中，[函数的微分](@entry_id:274991)通常被理解为对函数变化的线性近似。然而，这种直观理解在推广到高维弯曲空间（即[流形](@entry_id:153038)）时遇到了挑战。为了建立一个不依赖于特定[坐标系](@entry_id:156346)的、普适的框架，微分几何将[函数的微分](@entry_id:274991)重新定义为一个被称为“[1-形式](@entry_id:270392)”的几何对象。本文旨在填补从直观概念到严谨数学定义之间的鸿沟，阐明为何这一抽象是深刻且极其有用的。

通过本文，您将踏上一段从基础到应用的探索之旅。在“原理与机制”一章中，我们将建立函数[微分](@entry_id:158718)作为1-形式的严格定义，探索其代数性质与几何内涵。接着，在“应用与交叉学科联系”一章中，我们将见证这一概念如何成为连接物理学、高等力学与拓扑学的强大桥梁。最后，通过“动手实践”部分，您将有机会通过具体计算来巩固所学知识。让我们首先从第一章开始，深入了解其背后的核心原理。

## 原理与机制

在本章中，我们将深入探讨光滑函数[微分](@entry_id:158718)的形式化定义，即作为一种“1-形式”。我们将从其作为函数变化[最佳线性近似](@entry_id:164642)的直观概念出发，建立其严谨的数学框架。随后，我们将探索其核心的代数性质和深刻的几何解释，特别是它与函数的等位集以及沿路径的变化率之间的关系。最后，我们将把[函数的微分](@entry_id:274991)置于更广阔的[微分形式](@entry_id:146747)理论中，讨论一个给定的[1-形式](@entry_id:270392)在何种条件下可以成为某个[函数的微分](@entry_id:274991)，从而引出[闭形式与恰当形式](@entry_id:635477)的重要概念。

### 函数[微分](@entry_id:158718)的定义：[最佳线性近似](@entry_id:164642)

在单变量微积分中，函数 $f(x)$ 在点 $p$ 的[微分](@entry_id:158718) $df_p$ 被理解为一个线性映射，它将微小的位移 $\Delta x$ 映射为函数值变化的线性[主部](@entry_id:168896)，即 $df_p(\Delta x) = f'(p) \Delta x$。这个值是对实际变化量 $\Delta f = f(p+\Delta x) - f(p)$ 的[最佳线性近似](@entry_id:164642)。现在，我们将此概念推广到定义在多维空间（如 $\mathbb{R}^n$ 或更一般的[微分](@entry_id:158718)[流形](@entry_id:153038)）上的光滑标量函数 $f$。

给定一个定义在[流形](@entry_id:153038) $M$ 上的光滑函数 $f: M \to \mathbb{R}$ 和 $M$ 上的一个点 $p$。我们考虑从 $p$ 点出发的一个[切向量](@entry_id:265494) $v \in T_p M$。这个[切向量](@entry_id:265494)代表了从 $p$ 点出发的一个[无穷小位移](@entry_id:202209)的方向和速率。函数 $f$ 沿着这个向量 $v$ 的变化可以用其[微分](@entry_id:158718)来描述。

**[函数的微分](@entry_id:274991)** (differential of a function)，记作 $df$，在点 $p$ 是一个作用于该点切空间 $T_p M$ 的线性函数，即 $df_p: T_p M \to \mathbb{R}$。对于任意切向量 $v \in T_p M$， $df_p(v)$ 的值给出了函数 $f$ 在点 $p$ 沿方向 $v$ 的变化的[最佳线性近似](@entry_id:164642)。

从计算的角度来看，如果我们在点 $p$ 附近使用局部坐标系 $(x^1, x^2, \dots, x^n)$，那么函数 $f$ 可以表示为坐标的函数 $f(x^1, \dots, x^n)$。切向量 $v$ 可以写成[基向量](@entry_id:199546)的[线性组合](@entry_id:154743) $v = \sum_{i=1}^n v^i \frac{\partial}{\partial x^i}$。此时，[微分](@entry_id:158718) $df_p$ 作用于 $v$ 的结果由下式给出：

$df_p(v) = \sum_{i=1}^n \frac{\partial f}{\partial x^i}\bigg|_p v^i$

这个表达式正是[多变量微积分](@entry_id:147547)中方向导数的定义。因此，**$df_p(v)$ 就是函数 $f$ 在点 $p$ 沿向量 $v$ 的[方向导数](@entry_id:189133)**。

[微分](@entry_id:158718) $df_p$ 本身是一个[线性映射](@entry_id:185132)，它在点 $p$ 的[余切空间](@entry_id:270516) $T_p^*M$ 中。在[局部坐标](@entry_id:181200)下，它可以表示为基[1-形式](@entry_id:270392) $dx^i$ 的线性组合：

$df = \sum_{i=1}^n \frac{\partial f}{\partial x^i} dx^i$

这里，$dx^i$ 是对偶基的元素，其定义为 $dx^i(\frac{\partial}{\partial x^j}) = \delta^i_j$（其中 $\delta^i_j$ 是克罗内克符号）。因此，$df$ 是一个1-形式场，它在[流形](@entry_id:153038)的每个点上都指定了一个余[切向量](@entry_id:265494)。

让我们通过一个具体的例子来理解“[最佳线性近似](@entry_id:164642)”的含义 [@problem_id:1670940]。考虑一个定义在 $\mathbb{R}^2$ 上的函数 $f(x, y) = x^3 y^2$。我们想分析从点 $p = (1, 2)$ 沿一个小的位移向量 $v = (0.1, 0.2)$ 移动时函数值的变化。

首先，计算在点 $p$ 的[微分](@entry_id:158718) $df_p$ 作用于向量 $v$ 的值。$f$ 的[偏导数](@entry_id:146280)是 $\frac{\partial f}{\partial x} = 3x^2 y^2$ 和 $\frac{\partial f}{\partial y} = 2x^3 y$。在点 $p=(1,2)$，我们有：

$\frac{\partial f}{\partial x}\bigg|_p = 3(1)^2(2)^2 = 12$
$\frac{\partial f}{\partial y}\bigg|_p = 2(1)^3(2) = 4$

因此，线性近似的变化量为：
$df_p(v) = 12 \cdot v_x + 4 \cdot v_y = 12(0.1) + 4(0.2) = 1.2 + 0.8 = 2$

现在，我们计算实际的函数值变化 $\Delta f = f(p+v) - f(p)$。新的点是 $p+v = (1.1, 2.2)$。
$f(p) = f(1,2) = 1^3 \cdot 2^2 = 4$
$f(p+v) = f(1.1, 2.2) = (1.1)^3 (2.2)^2 = 1.331 \cdot 4.84 = 6.44204$

实际变化量为 $\Delta f = 6.44204 - 4 = 2.44204$。
近似值 $df_p(v)=2$ 与实际值 $\Delta f=2.44204$ 之间的绝对误差是 $|2.44204 - 2| = 0.44204$。当位移向量 $v$ 的模长变得更小时，这个误差会以比 $|v|$ 更快的速度趋向于零，这正是“[最佳线性近似](@entry_id:164642)”的数学含义。

### 几何解释与物理应用

$df$ 的核心作用是衡量函数的变化。正如我们所见，$df$ 可以作用于一个切向量（方向），也可以作用于一个[切向量](@entry_id:265494)场。

#### 作用于向量场

如果 $V$ 是一个向量场，那么 $df(V)$ 是一个新的标量函数，其在点 $p$ 的值等于 $df_p(V_p)$。这代表了函数 $f$ 沿向量场 $V$ 定义的流动方向的变化率。

例如，考虑一个三维空间中的标量场 $f(x, y, z) = x^2 \exp(y) \cos(z)$ 和一个向量场 $V = (z^2 - x) \frac{\partial}{\partial x} + xy \frac{\partial}{\partial y} - y \exp(z) \frac{\partial}{\partial z}$ [@problem_id:1528014]。我们来计算 $df(V)$ 在点 $P = (1, \ln(2), 0)$ 的值。

首先，计算 $df$：
$\frac{\partial f}{\partial x} = 2x \exp(y) \cos(z)$
$\frac{\partial f}{\partial y} = x^2 \exp(y) \cos(z)$
$\frac{\partial f}{\partial z} = -x^2 \exp(y) \sin(z)$
所以，$df = (2x \exp(y) \cos(z)) dx + (x^2 \exp(y) \cos(z)) dy - (x^2 \exp(y) \sin(z)) dz$。

$df(V)$ 的计算公式为：
$df(V) = \frac{\partial f}{\partial x} V^x + \frac{\partial f}{\partial y} V^y + \frac{\partial f}{\partial z} V^z$

在点 $P=(1, \ln(2), 0)$，我们有 $x=1, y=\ln(2), z=0$，因此 $\exp(y)=2, \cos(z)=1, \sin(z)=0$。
各分量在点 $P$ 的值为：
$\frac{\partial f}{\partial x}\bigg|_P = 2(1)(2)(1) = 4$
$\frac{\partial f}{\partial y}\bigg|_P = 1^2(2)(1) = 2$
$\frac{\partial f}{\partial z}\bigg|_P = -1^2(2)(0) = 0$

向量场 $V$ 在点 $P$ 的分量为：
$V^x|_P = 0^2 - 1 = -1$
$V^y|_P = 1 \cdot \ln(2) = \ln(2)$
$V^z|_P = -\ln(2) \exp(0) = -\ln(2)$

所以，$df_P(V_P) = 4(-1) + 2(\ln(2)) + 0(-\ln(2)) = 2\ln(2) - 4$。这个[数值表示](@entry_id:138287)在点 $P$，函数 $f$ 沿着向量 $V_P$ 方向的变化率。

#### 沿曲线的变化率

一个极其重要的应用是计算函数沿着某条路径的变化情况。假设一个粒子沿着曲线 $\gamma(t)$ 在[流形](@entry_id:153038)中运动，其速度向量为 $\gamma'(t)$。那么，该粒子所经历的[标量场](@entry_id:151443) $f$ 的瞬时变化率是多少？

这个变化率就是复合函数 $f(\gamma(t))$ 对时间 $t$ 的导数，即 $\frac{d}{dt}(f \circ \gamma)(t)$。根据链式法则，这个导数恰好等于 $f$ 的[微分](@entry_id:158718)作用在其速度向量上：

$\frac{d}{dt} (f \circ \gamma)(t) = df_{\gamma(t)}(\gamma'(t))$

这个恒等式是连接抽象[微分](@entry_id:158718)和具体物理过程的关键桥梁。

让我们通过一个例子来验证这一点 [@problem_id:1670915]。设[标量场](@entry_id:151443)为 $f(x, y, z) = x^2 y z$，[粒子轨迹](@entry_id:204827)为 $\gamma(t) = (t, t^2, t^3)$。我们想求在 $t=2$ 时 $f$ 的[瞬时变化率](@entry_id:141382)。

一方面，我们可以直接计算[复合函数](@entry_id:147347)：
$F(t) = f(\gamma(t)) = (t)^2(t^2)(t^3) = t^7$
其对时间的导数为 $F'(t) = 7t^6$。在 $t=2$ 时，变化率为 $7(2^6) = 7 \cdot 64 = 448$。

另一方面，我们使用[微分](@entry_id:158718)的方法。首先计算 $df$ 和 $\gamma'(t)$：
$df = (2xyz) dx + (x^2z) dy + (x^2y) dz$
$\gamma'(t) = (1, 2t, 3t^2)$

在任意时刻 $t$，粒子位于 $\gamma(t)=(t, t^2, t^3)$。将这些坐标代入 $df$ 的系数中：
$df_{\gamma(t)} = (2(t)(t^2)(t^3)) dx + ((t)^2(t^3)) dy + ((t)^2(t^2)) dz = 2t^6 dx + t^5 dy + t^4 dz$

现在，将 $df_{\gamma(t)}$ 作用于速度向量 $\gamma'(t) = 1 \cdot \frac{\partial}{\partial x} + 2t \cdot \frac{\partial}{\partial y} + 3t^2 \cdot \frac{\partial}{\partial z}$：
$df_{\gamma(t)}(\gamma'(t)) = (2t^6)(1) + (t^5)(2t) + (t^4)(3t^2) = 2t^6 + 2t^6 + 3t^6 = 7t^6$

这个结果与直接求导完全一致。在 $t=2$ 时，结果为 $7(2^6) = 448$。这个方法在函数形式复杂或轨迹不由简单解析式给出时，显示出其强大的普适性 [@problem_id:1670917]。

### 微分算子 $d$ 的代数性质

作用于函数（0-形式）以产生1-形式的算子 $d$ 具有一些基本的代数性质，这些性质使其成为微积分中一个非常强大的工具。

1.  **线性性 (Linearity)**：对于任意常数 $a, b \in \mathbb{R}$ 和光滑函数 $f, g$，有：
    $d(af + bg) = a \, df + b \, dg$

    这个性质可以直接从[偏导数](@entry_id:146280)的线性性得到。例如，考虑函数 $h(x,y) = a f(x,y) + b g(x,y)$ [@problem_id:1670947]。其[微分](@entry_id:158718)为：
    $dh = \frac{\partial(af+bg)}{\partial x} dx + \frac{\partial(af+bg)}{\partial y} dy$
    $= (a \frac{\partial f}{\partial x} + b \frac{\partial g}{\partial x}) dx + (a \frac{\partial f}{\partial y} + b \frac{\partial g}{\partial y}) dy$
    $= a(\frac{\partial f}{\partial x} dx + \frac{\partial f}{\partial y} dy) + b(\frac{\partial g}{\partial x} dx + \frac{\partial g}{\partial y} dy) = a \, df + b \, dg$
    例如，若 $f(x,y)=x^2$, $g(x,y)=y^3$, 则 $df=2x\,dx$, $dg=3y^2\,dy$。对于 $h=af+bg$, $dh = a(2x\,dx) + b(3y^2\,dy) = 2ax\,dx + 3by^2\,dy$。

2.  **[莱布尼茨法则](@entry_id:157949) (Leibniz Rule / Product Rule)**：对于两个[光滑函数](@entry_id:267124) $f, g$，其乘积的[微分](@entry_id:158718)为：
    $d(fg) = f \, dg + g \, df$

    证明同样依赖于偏导数的乘法法则：
    $d(fg) = \frac{\partial(fg)}{\partial x^i} dx^i = (f \frac{\partial g}{\partial x^i} + g \frac{\partial f}{\partial x^i}) dx^i = f (\frac{\partial g}{\partial x^i} dx^i) + g (\frac{\partial f}{\partial x^i} dx^i) = f \, dg + g \, df$

3.  **链式法则 (Chain Rule)**：如果 $f: M \to \mathbb{R}$ 是一个[光滑函数](@entry_id:267124)，而 $g: \mathbb{R} \to \mathbb{R}$ 是另一个[光滑函数](@entry_id:267124)，那么复合函数 $h = g \circ f$ 的[微分](@entry_id:158718)满足：
    $dh = (g' \circ f) \, df$

    这里 $g'$ 是 $g$ 对其单变量自变量的导数。这个法则表明，复合函数 $h$ 的变化率（由 $dh$ 描述）与 $f$ 的变化率（由 $df$ 描述）成正比，比例因子是在 $f(p)$ 点的 $g$ 的变化率 $g'(f(p))$。

    例如，考虑 $f(x, y) = x^2 \cos(y)$ 和 $g(t) = t^3$ [@problem_id:1670912]。则 $h(x, y) = (x^2 \cos(y))^3$。
    我们有 $g'(t) = 3t^2$，所以 $g'(f(x,y)) = 3(x^2 \cos(y))^2 = 3x^4 \cos^2(y)$。
    $f$ 的[微分](@entry_id:158718)是 $df = 2x \cos(y) dx - x^2 \sin(y) dy$。
    根据[链式法则](@entry_id:190743)，$dh = (3x^4 \cos^2(y)) (2x \cos(y) dx - x^2 \sin(y) dy) = 6x^5 \cos^3(y) dx - 3x^6 \sin(y) \cos^2(y) dy$。

### $df$ 的核与等位集

1-形式 $df_p$ 是一个从[切空间](@entry_id:199137) $T_p M$ 到实数 $\mathbb{R}$ 的[线性映射](@entry_id:185132)。因此，我们可以讨论它的**核** (kernel)，记为 $\ker(df_p)$。

$\ker(df_p) = \{ v \in T_p M \mid df_p(v) = 0 \}$

核是由所有使得函数 $f$ 在 $p$ 点沿该方向变化率为零的切向量组成的集合。这揭示了一个深刻的几何事实：$\ker(df_p)$ 正是函数 $f$ 通过 $p$ 点的**等位集** $S = \{ q \in M \mid f(q) = f(p) \}$ 在点 $p$ 的[切空间](@entry_id:199137)。

换句话说，任何位于等位集[切空间](@entry_id:199137)内的向量都与函数梯度的方向正交。在[欧几里得空间](@entry_id:138052)中，我们可以通过度规将1-形式 $df$ 与梯度向量场 $\nabla f$ 等同起来，它们的关系是 $df(v) = \langle \nabla f, v \rangle$。于是，$df_p(v) = 0$ 等价于 $\langle \nabla f_p, v \rangle = 0$，即向量 $v$ 与[梯度向量](@entry_id:141180) $\nabla f_p$ 正交。我们知道梯度向量指向[函数增长](@entry_id:267648)最快的方向，且垂直于[等位面](@entry_id:158674)。因此，与梯度垂直的向量构成的空间，正是[等位面](@entry_id:158674)的[切空间](@entry_id:199137)。

让我们考虑一个例子 [@problem_id:1635267]。设 $f(x, y, z) = x^2 + 4y^2 - z$。我们想描述在点 $p=(1, 1, 5)$ 处1-形式 $\omega = df$ 的核。
首先计算 $df$：
$df = 2x \, dx + 8y \, dy - 1 \, dz$
在点 $p=(1,1,5)$，我们有 $df_p = 2 \, dx + 8 \, dy - dz$。
一个[切向量](@entry_id:265494) $v = (v^x, v^y, v^z)$ 位于核中，当且仅当 $df_p(v) = 0$，即：
$2v^x + 8v^y - v^z = 0$
这个方程描述了 $\mathbb{R}^3$ 中所有与向量 $(2, 8, -1)$ 正交的向量 $(v^x, v^y, v^z)$ 构成的集合。这个集合是一个二维平面，其法向量为 $(2, 8, -1)$。这个平面就是函数 $f$ 的[等位面](@entry_id:158674) $x^2 + 4y^2 - z = f(1,1,5) = 1+4-5=0$ 在点 $p$ 的切平面。

这个性质在物理学中有重要应用。如果一个物理系统的运动被约束在某个[守恒量](@entry_id:150267) $F$ 的[等位面](@entry_id:158674)上，那么它的速度向量 $\mathbf{v}$ 必须始终位于该等位面的[切空间](@entry_id:199137)中 [@problem_id:1670930]。这意味着速度向量必须始终在 $dF$ 的核中，即 $dF(\mathbf{v}) = 0$ 必须恒成立。

例如，一个系统的特征由 $F(x, y, z) = x^3 y^{-2} z^5$ 描述，其运动由速度场 $\mathbf{v} = (2x, \alpha y, -4z)$ 决定。要使[运动约束](@entry_id:168736)在 $F$ 的[等位面](@entry_id:158674)上，必须满足 $dF(\mathbf{v}) = 0$。
$dF = (3x^2 y^{-2} z^5) dx + (-2x^3 y^{-3} z^5) dy + (5x^3 y^{-2} z^4) dz$
$dF(\mathbf{v}) = (3x^2 y^{-2} z^5)(2x) + (-2x^3 y^{-3} z^5)(\alpha y) + (5x^3 y^{-2} z^4)(-4z)$
$= 6x^3 y^{-2} z^5 - 2\alpha x^3 y^{-2} z^5 - 20x^3 y^{-2} z^5$
$= (6 - 2\alpha - 20) x^3 y^{-2} z^5 = (-14 - 2\alpha) F$
要使 $dF(\mathbf{v})=0$ 对于任意 $F \neq 0$ 的点都成立，我们必须有 $-14 - 2\alpha = 0$，解得 $\alpha = -7$。

最后，一个直接的推论是，如果在一个连通的[流形](@entry_id:153038)上 $df=0$ 处处成立，这意味着所有[偏导数](@entry_id:146280)都为零。因此，函数 $f$ 必须是常数 [@problem_id:1670917]。

### 恰当形式与闭形式

到目前为止，我们都是从一个函数 $f$ 出发，然后构造其[微分](@entry_id:158718) $df$。现在我们提出一个[逆问题](@entry_id:143129)：给定一个[1-形式](@entry_id:270392) $\omega$，是否存在一个函数 $f$ 使得 $\omega = df$？

如果存在这样的函数 $f$，我们称[1-形式](@entry_id:270392) $\omega$ 是**恰当的** (exact)，并称 $f$ 是 $\omega$ 的一个**[势函数](@entry_id:176105)** (potential function)。

一个1-形式 $\omega$ 是恰当的，其必要条件是它是**闭的** (closed)。在 $\mathbb{R}^2$ 上，一个1-形式 $\omega = P(x,y) dx + Q(x,y) dy$ 是闭的，如果它满足条件 $\frac{\partial P}{\partial y} = \frac{\partial Q}{\partial x}$。在 $\mathbb{R}^3$ 上，$\omega = P dx + Q dy + R dz$ 是闭的，如果其对应的向量场 $\mathbf{F}=(P,Q,R)$ 的旋度为零，即 $\nabla \times \mathbf{F} = 0$。这个条件来自于二阶偏导的对称性 (Clairaut-[Schwarz定理](@entry_id:139597))：如果 $\omega=df$，那么 $P = \frac{\partial f}{\partial x}$ 和 $Q = \frac{\partial f}{\partial y}$，因此 $\frac{\partial P}{\partial y} = \frac{\partial^2 f}{\partial y \partial x} = \frac{\partial^2 f}{\partial x \partial y} = \frac{\partial Q}{\partial x}$。

这个闭性条件是检验一个[1-形式](@entry_id:270392)是否可能为恰当形式的有力工具 [@problem_id:1670936]。例如，考虑1-形式 $\omega = (C y^3 \cos(x) + 2xy) dx + (9 y^2 \sin(x) + x^2) dy$。要使其成为某个 $f$ 的[微分](@entry_id:158718)，我们必须有：
$\frac{\partial}{\partial y}(C y^3 \cos(x) + 2xy) = \frac{\partial}{\partial x}(9 y^2 \sin(x) + x^2)$
$3C y^2 \cos(x) + 2x = 9 y^2 \cos(x) + 2x$
为了使该等式对所有 $(x,y)$ 成立，我们必须有 $3C = 9$，即 $C=3$。

然而，闭性条件只是必要条件，而非充分条件。一个闭的[1-形式](@entry_id:270392)是否一定是恰当的，取决于其定义域的[拓扑性质](@entry_id:141605)。**[庞加莱引理](@entry_id:160150) (Poincaré Lemma)** 指出：在一个**单连通** (simply connected) 的区域（即区域中任何闭合回路都可以连续地收缩到一个点，不包含“洞”）上，任何闭的1-形式都是恰当的。$\mathbb{R}^2$ 和 $\mathbb{R}^3$ 都是单连通的，所以在这些空间上，“闭”和“恰当”是等价的。

当定义域不是单连通时，情况就变得微妙了。一个经典的例子是定义在“[穿孔平面](@entry_id:150262)” $\mathcal{D} = \mathbb{R}^2 \setminus \{(0,0)\}$ 上的[1-形式](@entry_id:270392) [@problem_id:1670913]：
$\omega = \frac{-y}{x^2+y^2} dx + \frac{x}{x^2+y^2} dy$

我们来检验其闭性。令 $P(x,y) = \frac{-y}{x^2+y^2}$ 和 $Q(x,y) = \frac{x}{x^2+y^2}$。
$\frac{\partial P}{\partial y} = \frac{(-1)(x^2+y^2) - (-y)(2y)}{(x^2+y^2)^2} = \frac{y^2-x^2}{(x^2+y^2)^2}$
$\frac{\partial Q}{\partial x} = \frac{(1)(x^2+y^2) - (x)(2x)}{(x^2+y^2)^2} = \frac{y^2-x^2}{(x^2+y^2)^2}$
由于 $\frac{\partial P}{\partial y} = \frac{\partial Q}{\partial x}$，这个1-形式在 $\mathcal{D}$ 上是闭的。

然而，它在 $\mathcal{D}$ 上不是恰当的。我们可以通过计算它沿一个环绕原点（即“洞”）的闭合路径的[线积分](@entry_id:141417)来证明这一点。取逆时针方向的单位圆 $C$，$x = \cos t, y = \sin t$，$t \in [0, 2\pi]$。
$\oint_C \omega = \int_0^{2\pi} \left( \frac{-\sin t}{1} (-\sin t dt) + \frac{\cos t}{1} (\cos t dt) \right) = \int_0^{2\pi} (\sin^2 t + \cos^2 t) dt = \int_0^{2\pi} dt = 2\pi$
根据[斯托克斯定理](@entry_id:264534)（或其在平面上的特例[格林公式](@entry_id:173118)），如果一个1-形式 $\omega$ 是恰当的（$\omega=df$），那么它在任何闭合路径上的积分都必须为零（$\oint_C df = f(\text{终点}) - f(\text{起点}) = 0$）。由于我们找到了一个积分为 $2\pi \neq 0$ 的闭合路径，所以 $\omega$ 在 $\mathcal{D}$ 上不可能是恰当的。

这个例子深刻地揭示了[流形的拓扑](@entry_id:267834)结构（是否存在“洞”）如何影响其上的微积分性质。局域上看，$\omega$ 确实是函数 $f(x,y) = \arctan(y/x)$ 的[微分](@entry_id:158718)，但这个函数无法在整个[穿孔平面](@entry_id:150262)上被连续地、单值地定义，从而导致了全局上的非恰当性。