## 引言
在物理世界与数学模型中，我们常常遇到这样一类量：它们在空间中的每一点都有一个确定的数值，却没有方向，例如温度、压强或[电势](@entry_id:267554)。这类量场被称为[标量场](@entry_id:151443)。然而，这些量的空间变化往往会驱动有方向的物理过程，如热量从高温区流向低温区，或[带电粒子](@entry_id:160311)在[电场](@entry_id:194326)中受力运动。[标量场的梯度](@entry_id:270765)（Gradient）正是描述这种从“量变”到“质变”的核心数学工具，它将一个标量场转化为一个矢量场，精确地揭示了空间变化率的大小和方向。

本文旨在系统性地阐述[标量场](@entry_id:151443)梯度的理论与应用。我们将解决一个根本问题：如何从一个标量[分布](@entry_id:182848)中提取出有向的、动态的信息？通过学习本文，您将能够深刻理解梯度不仅是数学上的一个微分算子，更是连接“势”与“力”、描述系统平衡与变化的物理桥梁。

文章将分为三个核心部分。在“原理与机制”一章中，我们将从梯度的基本定义出发，探讨其与[方向导数](@entry_id:189133)、[等值面](@entry_id:196027)以及保守场等关键概念的内在联系。接着，在“应用与跨学科联系”一章中，我们将展示梯度如何在物理学、工程学乃至微分几何和广义相对论等前沿学科中发挥作用，解决从计算[电场](@entry_id:194326)力到分析[时空结构](@entry_id:158931)的各类问题。最后，“动手实践”部分将提供一系列精心设计的问题，帮助您将理论知识应用于具体的计算与分析，从而巩固和深化理解。

## 原理与机制

在对标量场的研究中，梯度是一个核心概念，它将一个在空间中每点只取一个数值的标量场，转化为一个在每点都具有大小和方向的矢量场。这个转化不仅是数学上的一个优美构造，更深刻地揭示了物理世界中从“势”到“力”的内在联系。本章将系统地阐述梯度的基本原理、关键性质及其在不同科学领域中的核心机制。

### 定义梯度：[最速上升方向](@entry_id:140639)

想象一下身处一座山脉之中，你脚下的每一点都有一个特定的海拔高度。海拔就是一个标量场，它将你的二维位置坐标 $(x, y)$ 映射为一个标量值 $h(x, y)$。在任何一点，你都想找到一个方向，沿着这个方向攀登，海拔上升得最快。这个方向，就是梯度的方向。

在数学上，对于一个在三维笛卡尔坐标系中定义的可微[标量场](@entry_id:151443) $f(x, y, z)$，其**梯度（gradient）**被定义为一个矢量场，记作 $\nabla f$ 或 $\text{grad}(f)$。它由 $f$ 对各个坐标分量的偏导数构成：

$$
\nabla f(x, y, z) = \frac{\partial f}{\partial x}\hat{\mathbf{i}} + \frac{\partial f}{\partial y}\hat{\mathbf{j}} + \frac{\partial f}{\partial z}\hat{\mathbf{k}}
$$

其中 $\hat{\mathbf{i}}$, $\hat{\mathbf{j}}$, $\hat{\mathbf{k}}$ 是沿 $x, y, z$ 轴的单位矢量。这里的符号 $\nabla$（读作 nabla 或 del）是一个矢量[微分算子](@entry_id:140145)，定义为 $\nabla = \hat{\mathbf{i}}\frac{\partial}{\partial x} + \hat{\mathbf{j}}\frac{\partial}{\partial y} + \hat{\mathbf{k}}\frac{\partial}{\partial z}$。当它作用于一个标量场 $f$ 时，便生成了梯度矢量场 $\nabla f$。

梯度矢量 $\nabla f$ 在某一点的**方向**指向该点标量场 $f$ 增长最快的方向。其**大小** $|\nabla f|$ 则表示在这个最速增长方向上的变化率。

为了将这个抽象定义具体化，让我们考虑一个物理情景。假设在一个[复合材料](@entry_id:139856)内部，[稳态温度分布](@entry_id:176266)由[标量场](@entry_id:151443) $T(x,y,z) = x^2 \sin(y) + z \cos(y)$ 描述。一个热敏微型机器人被放置在点 $P_0(1, \frac{\pi}{4}, 2)$，它的任务是沿着温度上升最快的方向移动。这个方向正是由温度场在该点的梯度决定的 [@problem_id:1675897]。

首先，我们计算温度场 $T$ 的梯度：
$$
\nabla T = \langle \frac{\partial T}{\partial x}, \frac{\partial T}{\partial y}, \frac{\partial T}{\partial z} \rangle
= \langle 2x \sin(y), x^2 \cos(y) - z \sin(y), \cos(y) \rangle
$$

接下来，在点 $P_0(1, \frac{\pi}{4}, 2)$ 处计算该梯度矢量：
$$
\nabla T|_{P_0} = \langle 2(1)\sin(\frac{\pi}{4}), (1)^2\cos(\frac{\pi}{4}) - 2\sin(\frac{\pi}{4}), \cos(\frac{\pi}{4}) \rangle
= \langle 2(\frac{\sqrt{2}}{2}), \frac{\sqrt{2}}{2} - 2(\frac{\sqrt{2}}{2}), \frac{\sqrt{2}}{2} \rangle
= \langle \sqrt{2}, -\frac{\sqrt{2}}{2}, \frac{\sqrt{2}}{2} \rangle
$$
这个矢量 $\vec{v} = \langle \sqrt{2}, -\frac{\sqrt{2}}{2}, \frac{\sqrt{2}}{2} \rangle$ 就精确地指向了在 $P_0$ 点温度上升最快的方向。机器人移动的初始方向，即为该矢量的单位方向矢量 $\hat{u} = \frac{\vec{v}}{|\vec{v}|}$。通过计算可得，其方向为 $\langle \frac{\sqrt{6}}{3}, -\frac{\sqrt{6}}{6}, \frac{\sqrt{6}}{6} \rangle$。

### [方向导数](@entry_id:189133)：任意方向的变化率

梯度为我们指明了“最陡峭”的路径，但在很多情况下，我们关心的是沿任意指定方向的变化情况。例如，一个传感器沿预定[轨道运动](@entry_id:162856)，它所经历的温度变化率是多少？这个量由**[方向导数](@entry_id:189133)（directional derivative）**给出。

标量场 $f$ 在点 $P$ 沿单位矢量 $\mathbf{u}$ 方向的方向导数，记作 $D_{\mathbf{u}}f(P)$，定义了 $f$ 在该点沿 $\mathbf{u}$ 方向的[瞬时变化率](@entry_id:141382)。它与梯度之间有一个简洁而深刻的关系：

$$
D_{\mathbf{u}}f = \nabla f \cdot \mathbf{u}
$$

这个公式是梯度概念的核心。我们可以通过[点积](@entry_id:149019)的几何意义来理解它：$D_{\mathbf{u}}f = |\nabla f| |\mathbf{u}| \cos\theta = |\nabla f| \cos\theta$，其中 $\theta$ 是 $\nabla f$ 与 $\mathbf{u}$ 之间的夹角。

这个关系清晰地表明：
- 当 $\mathbf{u}$ 与 $\nabla f$ 方向相同时（$\theta = 0$），$\cos\theta = 1$，方向导数取得最大值 $|\nabla f|$。这再次确认了梯度方向是[函数增长](@entry_id:267648)最快的方向。
- 当 $\mathbf{u}$ 与 $\nabla f$ 方向垂直时（$\theta = \pi/2$），$\cos\theta = 0$，[方向导数](@entry_id:189133)为零。这意味着沿垂直于梯度的方向移动，函数值在瞬时没有变化。
- 当 $\mathbf{u}$ 与 $\nabla f$ 方向相反时（$\theta = \pi$），$\cos\theta = -1$，方向导数取得最小值 $-|\nabla f|$。这对应于函数下降最快的方向。

让我们考察一个实际应用。假设某各向异性材料中的温度场为 $T(x,y,z) = k_{1}xyz + k_{2}(x^2+z^2)$。一个传感器从点 $P_A = (1, 3, 2)$ 直线移动向点 $P_B = (3, 2, 0)$。我们想知道传感器在出发瞬间记录到的温度随距离的变化率 [@problem_id:1675878]。

这正是要求解在点 $P_A$ 处，沿 $P_A$ 指向 $P_B$ 方向的温度方向导数。
1.  **计算梯度**：首先计算 $\nabla T = \langle k_{1}yz+2k_{2}x, k_{1}xz, k_{1}xy+2k_{2}z \rangle$，并代入 $P_A$ 的坐标和常数值，得到 $\nabla T(P_A) = (27, 8, 18)$。
2.  **确定方向**：运动方向由矢量 $\mathbf{v} = P_B - P_A = \langle 2, -1, -2 \rangle$ 给出。重要的是，[方向导数](@entry_id:189133)公式中的 $\mathbf{u}$ 必须是单位矢量，因此我们需要将 $\mathbf{v}$ 标准化：$\mathbf{u} = \frac{\mathbf{v}}{|\mathbf{v}|} = \frac{\langle 2, -1, -2 \rangle}{\sqrt{2^2+(-1)^2+(-2)^2}} = \langle \frac{2}{3}, -\frac{1}{3}, -\frac{2}{3} \rangle$。
3.  **计算[方向导数](@entry_id:189133)**：利用[点积](@entry_id:149019)公式 $D_{\mathbf{u}}T = \nabla T(P_A) \cdot \mathbf{u}$：
    $$
    D_{\mathbf{u}}T = (27, 8, 18) \cdot \langle \frac{2}{3}, -\frac{1}{3}, -\frac{2}{3} \rangle = 27(\frac{2}{3}) + 8(-\frac{1}{3}) + 18(-\frac{2}{3}) = \frac{54 - 8 - 36}{3} = \frac{10}{3}
    $$
    因此，传感器记录到的初始温度变化率约为 $3.33 \text{ K/m}$。

### 物理体现：[势场](@entry_id:143025)与力

梯度在物理学中扮演着至关重要的角色，它构成了从**标量势（scalar potential）**到**矢量[力场](@entry_id:147325)（vector force field）**的桥梁。许多基本的物理[力场](@entry_id:147325)，如静电场和[引力场](@entry_id:169425)，都是**[保守场](@entry_id:137555)**，这意味着作用在物体上的力可以表示为某个标量[势能函数](@entry_id:200753) $U$ 的梯度。具体关系是：

$$
\mathbf{F} = -\nabla U
$$

类似地，静电场 $\mathbf{E}$ 与静电势 $V$ 的关系为：

$$
\mathbf{E} = -\nabla V
$$

这个负号具有深刻的物理意义：[保守力](@entry_id:170586)总是指向势能**减小**最快的方向。物体会自发地从高势能区域移动到低[势能](@entry_id:748988)区域，如同水往低处流。例如，一个带正电的粒子在[电场](@entry_id:194326)中会受到一个力，使其从高[电势](@entry_id:267554)处移向低[电势](@entry_id:267554)处 [@problem_id:1618053]。

设想一个由 $V(x,y,z) = A \left( \frac{x^2 z}{a^3} - \frac{y^3}{a^3} \right)$ 描述的[静电势](@entry_id:188370)。一个质子（带正[电荷](@entry_id:275494)）位于点 $P(2a, a, -a)$。它所受[电场](@entry_id:194326)力的方向是什么？由于质子[电荷](@entry_id:275494)为正，力 $\mathbf{F} = q\mathbf{E}$ 的方向与[电场](@entry_id:194326) $\mathbf{E}$ 的方向相同。我们只需计算 $-\nabla V$ 在该点的方向即可。

1.  **计算梯度 $\nabla V$**：
    $$
    \nabla V = \langle \frac{2Axz}{a^3}, -\frac{3Ay^2}{a^3}, \frac{Ax^2}{a^3} \rangle
    $$
2.  **计算[电场](@entry_id:194326) $\mathbf{E} = -\nabla V$**：
    $$
    \mathbf{E} = \langle -\frac{2Axz}{a^3}, \frac{3Ay^2}{a^3}, -\frac{Ax^2}{a^3} \rangle
    $$
3.  **在点 $P$ 处求值**：代入 $(x,y,z)=(2a, a, -a)$，得到：
    $$
    \mathbf{E}(P) = \langle -\frac{2A(2a)(-a)}{a^3}, \frac{3A(a)^2}{a^3}, -\frac{A(2a)^2}{a^3} \rangle = \langle \frac{4A}{a}, \frac{3A}{a}, -\frac{4A}{a} \rangle = \frac{A}{a}\langle 4, 3, -4 \rangle
    $$
    力的方向由矢量 $\langle 4, 3, -4 \rangle$ 决定。将其单位化，即可得到力的单位方向矢量 [@problem_id:1618053]。这个计算过程是求解静电学问题的基本步骤 [@problem_id:1830336]。

### [梯度算子](@entry_id:275922)的性质

如同普通导数一样，[梯度算子](@entry_id:275922) $\nabla$ 也遵循一系列代数运算法则，这些法则是进行矢量分析计算的基础。

**1. 线性性质（Linearity）**
如果 $f$ 和 $g$ 是两个[标量场](@entry_id:151443)，$a$ 和 $b$ 是常数，那么[梯度算子](@entry_id:275922)满足[线性叠加原理](@entry_id:196987)：
$$
\nabla(af + bg) = a\nabla f + b\nabla g
$$
这个性质的证明很简单，源于[偏导数](@entry_id:146280)自身的线性性。它的物理意义极为重要，对应于物理学中的**[叠加原理](@entry_id:144649)**。例如，如果一个粒子同时受到两个独立势场 $U_1$ 和 $U_2$ 的影响，总势能为 $U = c_1 U_1 + c_2 U_2$，那么作用在粒子上的总力就是各个[势场](@entry_id:143025)单独产生的力的矢量和：$\mathbf{F} = -\nabla U = -\nabla(c_1 U_1 + c_2 U_2) = -c_1 \nabla U_1 - c_2 \nabla U_2 = \mathbf{F}_1 + \mathbf{F}_2$ [@problem_id:1675908]。

**2. [乘积法则](@entry_id:158393)（Product Rule）**
对于两个标量场 $f$ 和 $g$ 的乘积，其梯度遵循一个类似于单变量微积分中[乘积法则](@entry_id:158393)的规则：
$$
\nabla(fg) = f(\nabla g) + g(\nabla f)
$$
这个法则可以通过在梯度定义的每个分量上应用普通[乘积法则](@entry_id:158393)来证明 [@problem_id:1675931]。例如，对于 $x$ 分量：
$$
\frac{\partial (fg)}{\partial x} = f \frac{\partial g}{\partial x} + g \frac{\partial f}{\partial x}
$$
将三个分量的结果组合起来，并重新组合成矢量形式，即可得到上述乘积法则。这个法则在处理由多个场相互作用构成的复杂系统时非常有用。

### 梯度、[等值面](@entry_id:196027)与[路径无关性](@entry_id:163750)

梯度的一个核心几何特性是它与**[等值面](@entry_id:196027)（level surfaces）**的关系。对于[标量场](@entry_id:151443) $f(x,y,z)$，所有满足 $f(x,y,z) = C$（其中 $C$ 是常数）的点构成的集合就是一个[等值面](@entry_id:196027)。例如，地形图上的等高线就是海拔这个[标量场](@entry_id:151443)的等值线。

**梯度与[等值面](@entry_id:196027)正交**
在[等值面](@entry_id:196027)上的任意一点，该点的梯度矢量 $\nabla f$ 总是与该[等值面](@entry_id:196027)正交（垂直）。
我们可以通过以下方式证明：考虑一条完全位于[等值面](@entry_id:196027) $f=C$ 上的可微曲线 $\mathbf{c}(t)$。因为曲线在[等值面](@entry_id:196027)上，所以对于所有的 $t$，都有 $f(\mathbf{c}(t)) = C$。根据多元[复合函数](@entry_id:147347)[求导法则](@entry_id:145443)，对 $t$ 求导：
$$
\frac{d}{dt} f(\mathbf{c}(t)) = \nabla f(\mathbf{c}(t)) \cdot \mathbf{c}'(t) = \frac{dC}{dt} = 0
$$
矢量 $\mathbf{c}'(t)$ 是曲线在该点的切矢量，因此它位于[等值面](@entry_id:196027)的[切平面](@entry_id:136914)内。由于它与梯度 $\nabla f$ 的[点积](@entry_id:149019)为零，这表明 $\nabla f$ 必定与任意切矢量正交，从而与[等值面](@entry_id:196027)本身正交。这解释了为什么沿着等高线行走（方向与梯度垂直），海拔不会发生变化。

**[梯度基本定理](@entry_id:263112)与[路径无关性](@entry_id:163750)**
梯度最重要的积分性质由**[梯度基本定理](@entry_id:263112)**（也称线积分基本定理）给出：
$$
\int_{\mathcal{C}} \nabla f \cdot d\mathbf{l} = f(B) - f(A)
$$
其中 $\mathcal{C}$ 是从点 $A$ 到点 $B$ 的任意一条路径。这个定理表明，一个梯度场（即[保守场](@entry_id:137555)）沿任意路径的线积分，其结果仅取决于路径的起点和终点，而与路径的具体形状完全无关。

这个定理在物理学中具有非凡的意义。例如，计算一个[电荷](@entry_id:275494) $q$ 在静电场 $\mathbf{E}=-\nabla V$ 中从 $A$ 点移动到 $B$ 点时[电场](@entry_id:194326)力所做的功 $W$ [@problem_id:1830334]：
$$
W = \int_A^B \mathbf{F} \cdot d\mathbf{l} = \int_A^B (q\mathbf{E}) \cdot d\mathbf{l} = -q \int_A^B \nabla V \cdot d\mathbf{l}
$$
应用[梯度基本定理](@entry_id:263112)，积分的结果变得异常简单：
$$
W = -q (V(B) - V(A)) = q(V(A) - V(B))
$$
这意味着，无论[电荷](@entry_id:275494)的移动轨迹多么复杂，[电场](@entry_id:194326)力所做的功只由起点和终点的电势差决定。这也正是“保守力”名称的由来——它对应着能量的守恒。当一个问题给出了复杂的运动轨迹，但涉及的场是[保守场](@entry_id:137555)时，通常暗示着可以直接利用这个定理来简化计算，而无需进行复杂的路径积分 [@problem_id:1830334]。

当我们计算一个标量场 $\phi$ 沿着一条参数化路径 $\mathbf{c}(t)$ 的变化率 $\frac{d\phi}{dt}$ 时，也可以利用梯度。通过[链式法则](@entry_id:190743)，我们有 $\frac{d\phi}{dt} = \nabla\phi(\mathbf{c}(t)) \cdot \mathbf{c}'(t)$。这提供了一种计算沿路径变化率的通用方法 [@problem_id:1515826]。

### 梯度与[保守场](@entry_id:137555)：旋度条件

我们已经知道，如果一个矢量场 $\mathbf{F}$ 是一个梯度场（即 $\mathbf{F} = \nabla f$），那么它就是一个[保守场](@entry_id:137555)。那么反过来，我们如何判断一个给定的矢量场 $\mathbf{F}$ 是否是保守场呢？**旋度（curl）**提供了一个强有力的判据。

一个重要的矢量恒等式是：**任意标量场 $f$ 的[梯度的旋度](@entry_id:274168)恒为零**。
$$
\nabla \times (\nabla f) = \mathbf{0}
$$
这个恒等式可以通过直接在[笛卡尔坐标系](@entry_id:169789)下展开计算来证明。旋度的定义是：
$$
\nabla \times \mathbf{F} = \left( \frac{\partial F_z}{\partial y} - \frac{\partial F_y}{\partial z} \right)\hat{\mathbf{i}} + \left( \frac{\partial F_x}{\partial z} - \frac{\partial F_z}{\partial x} \right)\hat{\mathbf{j}} + \left( \frac{\partial F_y}{\partial x} - \frac{\partial F_x}{\partial y} \right)\hat{\mathbf{k}}
$$
将 $\mathbf{F} = \nabla f = \langle \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}, \frac{\partial f}{\partial z} \rangle$ 代入，例如计算 $x$ 分量：
$$
\frac{\partial}{\partial y}\left(\frac{\partial f}{\partial z}\right) - \frac{\partial}{\partial z}\left(\frac{\partial f}{\partial y}\right) = \frac{\partial^2 f}{\partial y \partial z} - \frac{\partial^2 f}{\partial z \partial y}
$$
根据[Clairaut定理](@entry_id:139814)，只要[二阶偏导数](@entry_id:635213)连续，它们的[混合偏导数](@entry_id:139334)顺序无关，因此上式为零。对其他分量进行类似的计算，可以证明整个旋度矢量为零。

这个恒等式为我们提供了一个判断矢量场是否保守的必要条件：如果 $\mathbf{F}$ 是[保守场](@entry_id:137555)，则其旋度必须为零，即 $\nabla \times \mathbf{F} = \mathbf{0}$。在定义域为单连通区域（例如整个 $\mathbb{R}^3$）时，这个条件也是充分的。

我们可以利用这个条件来“修复”一个[非保守场](@entry_id:265048)，使其变为[保守场](@entry_id:137555)。例如，考虑一个[力场](@entry_id:147325) $\mathbf{H} = \mathbf{F} + \mathbf{G}$，其中 $\mathbf{F} = (8yz)\mathbf{j} - (3y^2)\mathbf{k}$ 是已知的非保守部分，而 $\mathbf{G} = f(y, z)\mathbf{k}$ 是一个待定的修正项。我们的目标是找到一个函数 $f(y,z)$ 使得总[力场](@entry_id:147325) $\mathbf{H}$ 是保守的 [@problem_id:1675934]。
为此，我们只需求解方程 $\nabla \times \mathbf{H} = \mathbf{0}$。
将 $\mathbf{H} = (0, 8yz, -3y^2 + f(y,z))$ 的分量代入旋度公式，我们得到一系列方程。其中非平凡的方程是：
$$
(\nabla \times \mathbf{H})_x = \frac{\partial}{\partial y}(-3y^2 + f(y,z)) - \frac{\partial}{\partial z}(8yz) = -6y + \frac{\partial f}{\partial y} - 8y = \frac{\partial f}{\partial y} - 14y = 0
$$
其他分量自然为零。因此，我们得到一个关于 $f$ 的[偏微分方程](@entry_id:141332) $\frac{\partial f}{\partial y} = 14y$。通过对 $y$ 积分，我们发现 $f(y,z) = 7y^2 + C(z)$，其中 $C(z)$ 是一个只与 $z$ 有关的任意函数。选择最简单的非恒定多项式形式，我们可以令 $C(z)=0$，从而得到 $f(y,z) = 7y^2$。这个过程展示了如何运用旋度为零的条件来构造一个保守场。

### 进阶主题：作为[协变矢量](@entry_id:263917)的梯度

到目前为止，我们主要在笛卡尔坐标系下讨论梯度。然而，物理定律本身不应依赖于我们选择的[坐标系](@entry_id:156346)。梯度在不同[坐标系](@entry_id:156346)下如何变换？这个问题将我们引向[张量分析](@entry_id:161423)的领域。

考虑一个从[笛卡尔坐标](@entry_id:167698) $(x,y)$ 到新坐标 $(u,v)$ 的变换，例如 $x=u+v, y=u-v$ [@problem_id:1515795]。一个标量场 $\phi(x,y)$ 的值在[坐标变换](@entry_id:172727)下是不变的，即 $\phi(x(u,v), y(u,v))$ 在空间同一点的值相同。但是，它的梯度分量会如何变化呢？

在 $(x,y)$ 系中，梯度分量是 $(\frac{\partial \phi}{\partial x}, \frac{\partial \phi}{\partial y})$。在 $(u,v)$ 系中，梯度分量是 $(\frac{\partial \phi}{\partial u}, \frac{\partial \phi}{\partial v})$。我们可以利用[多元链式法则](@entry_id:635606)来找到它们之间的关系：
$$
\frac{\partial \phi}{\partial u} = \frac{\partial \phi}{\partial x}\frac{\partial x}{\partial u} + \frac{\partial \phi}{\partial y}\frac{\partial y}{\partial u}
$$
$$
\frac{\partial \phi}{\partial v} = \frac{\partial \phi}{\partial x}\frac{\partial x}{\partial v} + \frac{\partial \phi}{\partial y}\frac{\partial y}{\partial v}
$$
对于 $x=u+v, y=u-v$ 的变换，我们有 $\frac{\partial x}{\partial u}=1, \frac{\partial y}{\partial u}=1, \frac{\partial x}{\partial v}=1, \frac{\partial y}{\partial v}=-1$。代入后得到：
$$
\frac{\partial \phi}{\partial u} = \frac{\partial \phi}{\partial x} + \frac{\partial \phi}{\partial y}
$$
$$
\frac{\partial \phi}{\partial v} = \frac{\partial \phi}{\partial x} - \frac{\partial \phi}{\partial y}
$$
这种特定的变换法则，即新[坐标系](@entry_id:156346)下的分量是旧[坐标系](@entry_id:156346)下分量的线性组合，其系数是[坐标变换](@entry_id:172727)函数（$x(u,v), y(u,v), \dots$）的偏导数，正是**[协变矢量](@entry_id:263917)（covariant vector）**（也称 1-形式，one-form）的定义。

梯度是一个[协变矢量](@entry_id:263917)，这与像[位移矢量](@entry_id:262782) $d\mathbf{r} = (dx, dy)$ 这样的**[逆变](@entry_id:192290)矢量（contravariant vector）**的变换法则是不同的。后者的分量变换法则涉及[偏导数](@entry_id:146280)矩阵的逆。理解梯度作为[协变矢量](@entry_id:263917)的本质，对于在[广义坐标](@entry_id:156576)（如球坐标、柱坐标）下正确地表达物理定律，以及在更高级的理论（如广义相对论）中处理弯曲时空，都是至关重要的一步。