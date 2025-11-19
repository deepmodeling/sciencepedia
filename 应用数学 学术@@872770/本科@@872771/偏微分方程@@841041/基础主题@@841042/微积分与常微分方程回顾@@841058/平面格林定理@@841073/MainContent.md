## 引言
在向量微积分的宏伟殿堂中，[格林定理](@entry_id:140478)是一块连接不同概念的基石。它在二维平面上建立了一座优雅的桥梁，将沿着封闭边界的一维线积分与边界所围区域内的二维[二重积分](@entry_id:198869)紧密地联系起来。这一定理的意义远不止于提供一种计算技巧；它揭示了局部（点上的旋度或散度）与全局（边界上的环量或通量）之间深刻的内在关系，这一思想贯穿于现代科学的许多领域。

在实际操作中，直接计算沿复杂路径的线积分往往是一项繁琐甚至棘手的任务。[格林定理](@entry_id:140478)通过提供一种替代的计算路径，即计算一个可能更简单的[二重积分](@entry_id:198869)，从而有效地解决了这一难题。本文旨在系统地阐述[格林定理](@entry_id:140478)，并展示其在多个学科中的强大应用。在接下来的章节中，我们将首先深入“原理与机制”，剖析[格林定理](@entry_id:140478)的两种形式、其数学前提以及一些重要的直接推论。随后，我们将在“应用与跨学科联系”中，探索该定理如何在几何计算、物理场分析、[偏微分方程](@entry_id:141332)乃至[复分析](@entry_id:167282)中发挥关键作用。最后，通过“动手实践”部分，您将有机会运用所学知识解决具体问题，巩固对这一定理的理解。

## 原理与机制

[格林定理](@entry_id:140478)（Green's Theorem）是向量微积分中的一块基石，它在二维平面上建立了一个深刻的联系：一个封闭边界上的线积分（环量或通量）与其所围区域上的[二重积分](@entry_id:198869)之间的关系。这一关系不仅为计算线积分提供了强有力的替代方法，也为[流体力学](@entry_id:136788)、电磁学和[偏微分方程](@entry_id:141332)等领域中的物理定律提供了深刻的见解。本章将系统地阐述[格林定理](@entry_id:140478)的两种主要形式——环量-旋度形式和通量-[散度形式](@entry_id:748608)，并探讨其应用、前提条件以及在推导其他重要[数学物理](@entry_id:265403)恒等式中的作用。

### [格林定理](@entry_id:140478)的环量-旋度形式

[格林定理](@entry_id:140478)的核心在于将宏观边界行为与微观区域内禀性联系起来。其最常见的形式，即环量-旋度形式，正是这一思想的体现。

**定理陈述**

考虑一个在 $xy$ 平面上的向量场 $\vec{F}(x, y) = P(x, y)\hat{i} + Q(x, y)\hat{j}$，其中分量函数 $P$ 和 $Q$ 具有连续的一阶[偏导数](@entry_id:146280)。设 $C$ 为一条分段光滑、简单闭合的曲线，它以**逆时针方向**（正方向）包围着一个区域 $D$。[格林定理](@entry_id:140478)的环量形式表明：

$$ \oint_C (P\,dx + Q\,dy) = \iint_D \left(\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y}\right) dA $$

左侧的[线积分](@entry_id:141417) $\oint_C \vec{F} \cdot d\vec{r} = \oint_C (P\,dx + Q\,dy)$ 被称为向量场 $\vec{F}$ 沿路径 $C$ 的**环量**（circulation）。它衡量了向量场沿曲线切向分量的累积效应。在[流体力学](@entry_id:136788)中，它代表了流体沿闭合路径流动的总趋势。

右侧的[二重积分](@entry_id:198869)则是在区域 $D$ 内对一个标量函数进行积分。这个被积函数 $\left(\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y}\right)$ 是 $\vec{F}$ 的**标量旋度**（scalar curl）。它度量了向量场在每一点的“微观旋转”强度或[涡量](@entry_id:142747)（vorticity）。从直观上看，如果在流体中的某一点放置一个微小的桨叶轮，旋度描述了该桨叶轮的旋转速率和方向。

因此，[格林定理](@entry_id:140478)的物理意义可以理解为：区域 $D$ 内所有微观旋转效应（涡量）的总和，等于沿其边界 $C$ 的宏观环流。

**应用：简化线积分计算**

[格林定理](@entry_id:140478)最直接的应用是它提供了一种计算[线积分](@entry_id:141417)的强大工具。直接计算[线积分](@entry_id:141417)通常需要对边界曲线 $C$ 进行[参数化](@entry_id:272587)，这可能非常繁琐，特别是当边界由多段不同函数曲线构成时。[格林定理](@entry_id:140478)允许我们将这个问题转化为一个可能更简单的[二重积分](@entry_id:198869)。

例如，考虑一个[力场](@entry_id:147325) $\vec{F}(x,y) = \left(-\frac{1}{3}y^{3} + \ln(1+x^{4})\right)\hat{i} + \left(\frac{1}{3}x^{3} + \arctan(y^{2})\right)\hat{j}$ 对一个沿闭合路径 $C$ 运动的粒子所做的功 $W = \oint_C \vec{F} \cdot d\vec{r}$。假设路径 $C$ 围成的区域 $R$ 由直线 $y=x$ 和抛物线 $y=x^2$ 限定 [@problem_id:2109250]。直接对 $C$ 的两段曲线（直线和抛物线）分别进行参数化积分会相当复杂。然而，应用[格林定理](@entry_id:140478)则使问题迎刃而解。

这里，$P(x,y) = -\frac{1}{3}y^{3} + \ln(1+x^{4})$ 且 $Q(x,y) = \frac{1}{3}x^{3} + \arctan(y^{2})$。尽管 $P$ 和 $Q$ 本身包含复杂的项，但它们的[偏导数](@entry_id:146280)组合却异常简洁：
$$ \frac{\partial Q}{\partial x} = \frac{\partial}{\partial x}\left(\frac{1}{3}x^{3} + \arctan(y^{2})\right) = x^{2} $$
$$ \frac{\partial P}{\partial y} = \frac{\partial}{\partial y}\left(-\frac{1}{3}y^{3} + \ln(1+x^{4})\right) = -y^{2} $$
因此，标量旋度为 $\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} = x^2 - (-y^2) = x^2 + y^2$。

功的计算就转化为一个在区域 $R$ 上的[二重积分](@entry_id:198869)：
$$ W = \iint_R (x^2 + y^2) \,dA $$
这个积分比原来的线积分容易处理得多。通过将区域 $R$ 描述为 $0 \le x \le 1, x^2 \le y \le x$，我们可以计算出功为 $\frac{3}{35}$ [@problem_id:2109250]。

另一个例子是计算[力场](@entry_id:147325) $\vec{F}(x, y) = (e^{x^2} - y^3) \hat{i} + (x^3 + \arctan(y)) \hat{j}$ 沿半径为 $R$ 的圆周所做的功。其旋度为 $\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} = 3x^2 - (-3y^2) = 3(x^2+y^2)$。在极坐标下，这个[二重积分](@entry_id:198869)变得非常简单，最终功为 $\frac{3}{2}\pi R^{4}$ [@problem_id:2109273]。

### 特殊情况与直接推论

**常数旋度场**

一个特别重要且富有启发性的情况是当向量场的旋度在整个区域 $D$ 内为常数时，即 $\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} = k$。在这种情况下，[格林定理](@entry_id:140478)简化为：
$$ \oint_C (P\,dx + Q\,dy) = \iint_D k \,dA = k \iint_D dA = k \cdot \text{Area}(D) $$
这意味着环量的大小与路径的具体形状无关，而仅仅与路径所围区域的**面积**成正比，比例常数为场的旋度。

例如，考虑一个[力场](@entry_id:147325) $\vec{F}(x, y) = \langle -3y + \sin(x), 4x + \exp(y^{2}) \rangle$ [@problem_id:2109245]。该场的旋度为：
$$ \frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} = \frac{\partial}{\partial x}(4x + \exp(y^2)) - \frac{\partial}{\partial y}(-3y + \sin(x)) = 4 - (-3) = 7 $$
这是一个常数。因此，该[力场](@entry_id:147325)沿任何[简单闭合路径](@entry_id:178274)所做的功都等于 $7$ 乘以该路径所围的面积。如果路径是一个[半长轴](@entry_id:164167)为 $a$、半短轴为 $b$ 的椭圆，其面积为 $\pi ab$，那么所做的功就是 $W = 7\pi ab$。

反过来，如果一个物理系统已知其环量（或做的功）总是与所围面积成正比，即 $\oint_C \vec{F} \cdot d\vec{r} = \lambda \cdot \text{Area}(D)$，那么我们可以通过[格林定理](@entry_id:140478)推断该场的旋度必然是一个常数 $\lambda$ [@problem_id:2109233]。

**路径无关性与保守场**

[格林定理](@entry_id:140478)为[保守向量场](@entry_id:172767)的一个基本性质提供了优雅的证明。一个向量场 $\vec{F}$ 被称为**[保守场](@entry_id:137555)**，如果它是某个标量势函数 $\phi$ 的梯度，即 $\vec{F} = \nabla\phi$。这意味着 $P = \frac{\partial \phi}{\partial x}$ 且 $Q = \frac{\partial \phi}{\partial y}$。如果 $\phi$ 具有连续的[二阶偏导数](@entry_id:635213)（根据[克莱罗定理](@entry_id:139814)，Clairaut's theorem），那么[混合偏导数相等](@entry_id:138898)：
$$ \frac{\partial Q}{\partial x} = \frac{\partial}{\partial x}\left(\frac{\partial \phi}{\partial y}\right) = \frac{\partial^2 \phi}{\partial x \partial y} = \frac{\partial^2 \phi}{\partial y \partial x} = \frac{\partial}{\partial y}\left(\frac{\partial \phi}{\partial x}\right) = \frac{\partial P}{\partial y} $$
因此，保守场的旋度为零：$\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} = 0$。
将此结果代入[格林定理](@entry_id:140478)，我们立即得到：
$$ \oint_C \vec{F} \cdot d\vec{r} = \iint_D 0 \,dA = 0 $$
这表明，在满足[格林定理](@entry_id:140478)条件的简单连通区域内，任何[保守场](@entry_id:137555)沿任意[简单闭合路径](@entry_id:178274)的[线积分](@entry_id:141417)（环量）恒为零。这是[保守场](@entry_id:137555)[路径无关性](@entry_id:163750)的一个关键特征。

**路径方向的重要性**

[格林定理](@entry_id:140478)的[标准形式](@entry_id:153058)假定曲线 $C$ 是**正向**的，即逆时针方向。当我们沿曲线行走时，所围区域 $D$ 始终在我们的左侧。如果路径的方向被反转为顺时针方向（记为 $-C$），线积分中的位移微元 $d\vec{r}$ 会变为 $-d\vec{r}$，导致整个[线积分](@entry_id:141417)的值变号：
$$ \oint_{-C} \vec{F} \cdot d\vec{r} = - \oint_{C} \vec{F} \cdot d\vec{r} $$
因此，对于顺时针方向的路径，[格林定理](@entry_id:140478)的形式变为：
$$ \oint_{-C} (P\,dx + Q\,dy) = - \iint_D \left(\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y}\right) dA $$
在应用[格林定理](@entry_id:140478)时，正确判断和处理路径的方向至关重要 [@problem_id:2109253]。

### [格林定理](@entry_id:140478)的通量-[散度形式](@entry_id:748608)

除了环量，另一个与向量场相关的重要物理量是**通量**（flux）。它衡量的是向量场“穿过”一条曲线的净流量。[格林定理](@entry_id:140478)也存在一个[通量形式](@entry_id:273811)，它将穿过封闭边界的总通量与区域内部的“源”或“汇”的强度联系起来。

**定理陈述**

设 $\vec{F}(x, y) = P(x, y)\hat{i} + Q(x, y)\hat{j}$ 是一个向量场，$C$ 是一条正向（逆时针）的[简单闭合曲线](@entry_id:275541)，包围区域 $D$。$\vec{F}$ 穿过 $C$ 的**外向通量**定义为 $\oint_C \vec{F} \cdot \vec{n} \, ds$，其中 $\vec{n}$ 是 $C$ 的单位外法向量，$ds$ 是弧长微元。[格林定理](@entry_id:140478)的[通量形式](@entry_id:273811)（也称为二维散度定理）表明：

$$ \oint_C \vec{F} \cdot \vec{n} \, ds = \iint_D \left(\frac{\partial P}{\partial x} + \frac{\partial Q}{\partial y}\right) dA $$

这里的被积函数 $\frac{\partial P}{\partial x} + \frac{\partial Q}{\partial y}$ 是向量场 $\vec{F}$ 的**散度**（divergence），记作 $\nabla \cdot \vec{F}$。散度衡量了向量场在某一点的“源”强度（正散度，表示流体从此点流出）或“汇”强度（负散度，表示流体向此点汇集）。

因此，[通量形式](@entry_id:273811)的物理意义是：区域 $D$ 内所有源和汇的总强度，等于流出该区域边界的总净流量（通量）。

**从环量形式到[通量形式](@entry_id:273811)的推导**

这两种形式的[格林定理](@entry_id:140478)实际上是等价的，并且可以相互推导。我们可以从环量-旋度形式出发，推导出通量-[散度形式](@entry_id:748608) [@problem_id:2109278]。

1.  首先，我们需要将[通量积分](@entry_id:138365) $\oint_C \vec{F} \cdot \vec{n} \, ds$ 用 $dx$ 和 $dy$ 表示。对于一条逆时针参数化的曲线 $\vec{r}(t) = \langle x(t), y(t) \rangle$，切向向量是 $\langle x'(t), y'(t) \rangle$。外法向量可以通过将切向向量顺时针旋转 $90^\circ$ 得到，即 $\langle y'(t), -x'(t) \rangle$。因此，单位外[法向量](@entry_id:264185) $\vec{n}$ 与 $\langle dy, -dx \rangle$ 同向。我们可以写出向量关系 $\vec{n} \, ds = dy\,\hat{i} - dx\,\hat{j}$。

2.  将此代入[通量积分](@entry_id:138365)：
    $$ \oint_C \vec{F} \cdot \vec{n} \, ds = \oint_C (P\hat{i} + Q\hat{j}) \cdot (dy\,\hat{i} - dx\,\hat{j}) = \oint_C (P\,dy - Q\,dx) $$

3.  现在，考虑一个新的向量场 $\vec{G} = \langle -Q, P \rangle$。计算 $\vec{G}$ 沿 $C$ 的环量：
    $$ \oint_C \vec{G} \cdot d\vec{r} = \oint_C (-Q\,dx + P\,dy) $$
    我们发现 $\vec{F}$ 的通量恰好等于 $\vec{G}$ 的环量。

4.  对 $\vec{G}$ 的环量应用[格林定理](@entry_id:140478)的环量-旋度形式。$\vec{G}$ 的分量是 $P_G = -Q$ 和 $Q_G = P$。
    $$ \oint_C (-Q\,dx + P\,dy) = \iint_D \left(\frac{\partial (Q_G)}{\partial x} - \frac{\partial (P_G)}{\partial y}\right) dA = \iint_D \left(\frac{\partial P}{\partial x} - \frac{\partial (-Q)}{\partial y}\right) dA $$

5.  简化右侧的积分，我们得到：
    $$ \iint_D \left(\frac{\partial P}{\partial x} + \frac{\partial Q}{\partial y}\right) dA $$
    这就完成了通量-[散度形式](@entry_id:748608)的推导。

### 重要考量：[奇点](@entry_id:137764)与区域的连通性

[格林定理](@entry_id:140478)的强大功能是建立在严格的数学前提之上的。其中一个核心要求是：向量场 $\vec{F}$ 的分量 $P$ 和 $Q$ 及其一阶[偏导数](@entry_id:146280)必须在包含区域 $D$ 及其边界 $C$ 的某个开集上是**连续的**。如果这个条件不满足，直接应用[格林定理](@entry_id:140478)可能会导致错误结论。

最经典的例子是描述理想涡旋的向量场 $\vec{F}(x, y) = \left\langle \frac{-y}{x^2 + y^2}, \frac{x}{x^2 + y^2} \right\rangle$ [@problem_id:2109248]。该向量场在原点 $(0,0)$ 处没有定义，因此不连续。

让我们分析一下，如果一个区域 $D$ 包含原点，为什么标准的[格林定理](@entry_id:140478)会失效：

1.  **计算旋度**：在任何非原点处 $(x,y) \neq (0,0)$，我们可以计算该场的旋度：
    $$ \frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} = \frac{\partial}{\partial x}\left(\frac{x}{x^2+y^2}\right) - \frac{\partial}{\partial y}\left(\frac{-y}{x^2+y^2}\right) = \frac{y^2-x^2}{(x^2+y^2)^2} - \frac{y^2-x^2}{(x^2+y^2)^2} = 0 $$
    该场的旋度处处为零（除了[奇点](@entry_id:137764)）。

2.  **错误应用定理**：如果无视原点的[奇点](@entry_id:137764)，并天真地应用[格林定理](@entry_id:140478)，我们会得到 $\oint_C \vec{F} \cdot d\vec{r} = \iint_D 0 \, dA = 0$。

3.  **直接计算线积分**：然而，如果我们沿任何一条包围原点的逆时针[简单闭合路径](@entry_id:178274) $C$（例如[单位圆](@entry_id:267290)）直接计算线积分，会发现其值恒为 $2\pi$ [@problem_id:2109229]。

$2\pi = 0$ 的矛盾表明，由于原点[奇点](@entry_id:137764)的存在，[格林定理](@entry_id:140478)的连续性假设在区域 $D$ 上不成立，因此定理的[标准形式](@entry_id:153058)不适用。

**处理含[奇点](@entry_id:137764)的区域（多连通区域）**

为了处理这类问题，我们可以使用适用于**多连通区域**（即带有“洞”的区域）的[格林定理](@entry_id:140478)。假设我们想计算上述涡旋场沿一个包围原点的大正方形 $C_{out}$ 的环量。我们可以构造一个不包含[奇点](@entry_id:137764)的新区域 $D'$，方法是从大正方形所围区域中“挖掉”一个以原点为中心的小圆盘，该圆盘的边界为 $C_{in}$。

新区域 $D'$ 的边界由两条曲线组成：外边界 $C_{out}$（逆时针）和内边界 $C_{in}$（相对于 $D'$ 而言，其正方向是顺时针）。由于 $D'$ 不包含[奇点](@entry_id:137764)，我们可以在其上应用[格林定理](@entry_id:140478)：
$$ \oint_{C_{out}} \vec{F} \cdot d\vec{r} + \oint_{C_{in}} \vec{F} \cdot d\vec{r} = \iint_{D'} (\text{旋度}) \, dA = \iint_{D'} 0 \, dA = 0 $$
注意，内边界 $C_{in}$ 是顺时针的。如果我们将其方向反转为标准的逆时针方向 $-C_{in}$，则[线积分](@entry_id:141417)变号：
$$ \oint_{C_{out}} \vec{F} \cdot d\vec{r} - \oint_{-C_{in}} \vec{F} \cdot d\vec{r} = 0 \quad \implies \quad \oint_{C_{out}} \vec{F} \cdot d\vec{r} = \oint_{-C_{in}} \vec{F} \cdot d\vec{r} $$
$-C_{in}$ 是一条围绕原点的逆时针小圆。我们已经知道，该场沿任何围绕原点的逆时针路径的环量都是 $2\pi$。因此，我们得出结论：该场沿大正方形边界的环量也是 $2\pi$ [@problem_id:2109229]。这一强大的技术表明，对于旋度为零但含有[奇点](@entry_id:137764)的场，其环量仅取决于路径围绕[奇点](@entry_id:137764)的方式，而与路径的具体形状和大小无关。

### 在[偏微分方程](@entry_id:141332)中的应用：[格林恒等式](@entry_id:176369)

[格林定理](@entry_id:140478)不仅是计算工具，更是推导其他重要数学定理的母定理。通过巧妙地选择[格林定理](@entry_id:140478)中的向量场，我们可以得到一系列在[偏微分方程理论](@entry_id:189232)中至关重要的**[格林恒等式](@entry_id:176369)**（Green's Identities）。

**[格林第一恒等式](@entry_id:170345)**

让我们从[格林定理](@entry_id:140478)的通量-[散度形式](@entry_id:748608)出发，选择一个特殊的向量场 $\vec{F} = u \nabla v$，其中 $u(x,y)$ 和 $v(x,y)$ 是两个标量场。这里 $\nabla v = \left\langle \frac{\partial v}{\partial x}, \frac{\partial v}{\partial y} \right\rangle$ 是 $v$ 的[梯度场](@entry_id:264143)。
这个向量场的分量是 $P = u \frac{\partial v}{\partial x}$ 和 $Q = u \frac{\partial v}{\partial y}$。它的散度是：
$$ \nabla \cdot \vec{F} = \frac{\partial P}{\partial x} + \frac{\partial Q}{\partial y} = \frac{\partial}{\partial x}\left(u \frac{\partial v}{\partial x}\right) + \frac{\partial}{\partial y}\left(u \frac{\partial v}{\partial y}\right) $$
使用[乘法法则](@entry_id:144424)展开，得到：
$$ \nabla \cdot \vec{F} = \left(\frac{\partial u}{\partial x}\frac{\partial v}{\partial x} + u \frac{\partial^2 v}{\partial x^2}\right) + \left(\frac{\partial u}{\partial y}\frac{\partial v}{\partial y} + u \frac{\partial^2 v}{\partial y^2}\right) = (\nabla u \cdot \nabla v) + u (\nabla^2 v) $$
其中 $\nabla^2 v = \frac{\partial^2 v}{\partial x^2} + \frac{\partial^2 v}{\partial y^2}$ 是 $v$ 的拉普拉斯算子。

将此散度表达式代入[通量形式](@entry_id:273811)的[格林定理](@entry_id:140478) $\oint_{\partial D} (\vec{F} \cdot \vec{n}) ds = \iint_D (\nabla \cdot \vec{F}) dA$，我们得到**[格林第一恒等式](@entry_id:170345)**:
$$ \iint_D (u \nabla^2 v + \nabla u \cdot \nabla v) dA = \oint_{\partial D} u (\nabla v \cdot \vec{n}) ds $$
这个恒等式将一个区域积分（包含[拉普拉斯算子](@entry_id:146319)和梯度）与一个边界积分（包含方向导数 $\nabla v \cdot \vec{n}$）联系起来。例如，计算积分 $I = \iint_D (u \nabla^2 v + \nabla u \cdot \nabla v) dA$ 可以直接通过计算被积表达式后积分得到 [@problem_id:2109227]，但这个恒等式揭示了其与边界值的深刻联系。

**应用于[偏微分方程解的唯一性](@entry_id:184927)证明**

[格林恒等式](@entry_id:176369)是证明诸如拉普拉斯方程和泊松方程等[边值问题](@entry_id:193901)[解的唯一性](@entry_id:143619)的标准工具。让我们通过一个例子来展示其威力 [@problem_id:2109252]。

考虑一个区域 $D$ 上的修正[亥姆霍兹方程](@entry_id:149977) $\nabla^2 u - \alpha u = f$，其中 $\alpha > 0$ 是常数，边界条件为在 $\partial D$ 上 $u = g$（[狄利克雷边界条件](@entry_id:173524)）。我们要证明该问题的解是唯一的。

证明思路是假设存在两个不同的解 $u_1$ 和 $u_2$。令 $w = u_1 - u_2$。
1.  **推导 $w$ 满足的方程**：由于 $u_1$ 和 $u_2$ 都满足原方程，将两式相减得到：
    $(\nabla^2 u_1 - \nabla^2 u_2) - \alpha(u_1 - u_2) = f - f$，即 $\nabla^2 w - \alpha w = 0$。$w$ 满足[齐次方程](@entry_id:163650)。
2.  **推导 $w$ 的边界条件**：在边界 $\partial D$ 上，$u_1 = g$ 且 $u_2 = g$，因此 $w = g - g = 0$。$w$ 满足[齐次边界条件](@entry_id:750371)。
3.  **应用[格林第一恒等式](@entry_id:170345)**：在[格林第一恒等式](@entry_id:170345)中，令 $u=w$ 且 $v=w$：
    $$ \iint_D (w \nabla^2 w + |\nabla w|^2) dA = \oint_{\partial D} w (\nabla w \cdot \vec{n}) ds $$
4.  **利用边界条件**：由于在边界上 $w=0$，右侧的边界积分恒为零。
    $$ \iint_D (w \nabla^2 w + |\nabla w|^2) dA = 0 $$
5.  **利用 $w$ 满足的[偏微分方程](@entry_id:141332)**：从 $w$ 满足的方程可知 $\nabla^2 w = \alpha w$。将其代入积分：
    $$ \iint_D (w(\alpha w) + |\nabla w|^2) dA = 0 \quad \implies \quad \iint_D (\alpha w^2 + |\nabla w|^2) dA = 0 $$
    这直接回答了问题 [@problem_id:2109252] 中所求积分的值为 $0$。

为了完成唯一性证明，我们注意到被积函数 $(\alpha w^2 + |\nabla w|^2)$ 是两个非负项的和。由于 $\alpha > 0$，因此 $\alpha w^2 \ge 0$ 且 $|\nabla w|^2 \ge 0$。一个非负[连续函数](@entry_id:137361)在区域上的积分为零，当且仅当该函数在区域内处处为零。因此，在 $D$ 内必须有 $\alpha w^2 = 0$ 和 $|\nabla w|^2 = 0$。这意味着 $w$ 在整个区域 $D$ 内必须为零。所以 $w=0$ 在 $D$ 中处处成立，即 $u_1=u_2$。解是唯一的。

这个例子完美地展示了[格林定理](@entry_id:140478)如何作为一座桥梁，将分析学（微积分）与几何学（边界与区域）联系起来，为[偏微分方程](@entry_id:141332)的理论分析提供了不可或缺的工具。