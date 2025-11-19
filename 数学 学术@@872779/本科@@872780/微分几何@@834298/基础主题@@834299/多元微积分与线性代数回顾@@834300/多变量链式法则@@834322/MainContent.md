## 引言
链式法则是微积分的基石，它为计算[复合函数的导数](@entry_id:190743)提供了基本框架。当从单变量微积分过渡到[多变量微积分](@entry_id:147547)时，[链式法则](@entry_id:190743)不仅得到了自然的推广，其内涵也变得更为深刻和强大。它成为理解和量化相互关联的变量系统中变化的核心工具，无论是在物理学中追踪粒子在场中的运动，还是在几何学中变换不同的[坐标系](@entry_id:156346)，[多变量链式法则](@entry_id:146671)都扮演着不可或缺的角色。然而，许多学习者在面对其多种形式和抽象的雅可比矩阵时感到困惑，难以把握其统一的本质和广泛的应用价值。

本文旨在系统地揭示[多变量链式法则](@entry_id:146671)的强大功能与内在逻辑。通过三个章节的递进式讲解，你将建立起对这一核心概念的全面理解。

*   在**“原理与机制”**一章中，我们将从最直观的“标量场与路径”情形入手，逐步推导出[链式法则](@entry_id:190743)的向量形式和几何意义，并最终将其推广至使用雅可比矩阵的通用形式，同时介绍其在[隐函数求导](@entry_id:137929)等方面的直接应用。
*   接下来，在**“应用与跨学科联系”**一章中，我们将探索链式法则在物理学、工程学、[微分几何](@entry_id:145818)、经济学等多个学科中的具体应用，展示它如何成为解决实际问题的强大模型工具。
*   最后，在**“动手实践”**部分，你将通过解决具体问题来巩固所学知识，将理论应用于实际计算，从而真正掌握[多变量链式法则](@entry_id:146671)。

通过本文的学习，你将不仅学会如何计算，更能深刻理解[多变量链式法则](@entry_id:146671)为何是连接数学理论与现实世界动态系统的关键桥梁。

## 原理与机制

在单变量微积分中，[链式法则](@entry_id:190743)是计算[复合函数](@entry_id:147347)导数的基石。当我们进入[多变量微积分](@entry_id:147547)的领域时，这一法则不仅得到了自然的推广，其内涵和应用也变得更加丰富和深刻。[多变量链式法则](@entry_id:146671)构成了连接不同[坐标系](@entry_id:156346)、分析动态系统中物理量变化率以及理解高维空间几何性质的核心工具。本章将系统地阐述[多变量链式法则](@entry_id:146671)的各项原理，从最基础的情形出发，逐步深入到其在矩阵形式下的推广及其在几何与物理学中的高级应用。

### 基本原理：标量场与路径

我们从最简单但最富有物理直觉的情形开始：一个标量场在空间中的值如何随着观察者的运动而变化。想象一个三维空间，其中每个点 $(x, y, z)$ 都对应一个标量值，例如温度或压力，由函数 $w = f(x, y, z)$ 描述。现在，假设有一个物体或探测器沿着一条由时间 $t$ 参数化的路径 $\mathbf{r}(t) = \langle x(t), y(t), z(t) \rangle$ 运动。在任何时刻 $t$，探测器所处位置的标量值是[复合函数](@entry_id:147347) $w(t) = f(x(t), y(t), z(t))$。我们关心的是，探测器所经历的标量值 $w$ 随时间 $t$ 的变化率是多少，即 $\frac{dw}{dt}$。

根据[链式法则](@entry_id:190743)，总变化率 $\frac{dw}{dt}$ 是由每个自变量的变化所贡献的变化率之和。具体来说， $w$ 的变化率等于它对每个坐标的[偏导数](@entry_id:146280)与该坐标随时间变化率的乘[积之和](@entry_id:266697)：

$$
\frac{dw}{dt} = \frac{\partial f}{\partial x}\frac{dx}{dt} + \frac{\partial f}{\partial y}\frac{dy}{dt} + \frac{\partial f}{\partial z}\frac{dz}{dt}
$$

这个公式的直观意义是：$x$ 方向上的微小运动导致 $w$ 变化的速率是 $\frac{\partial f}{\partial x}\frac{dx}{dt}$，同样地，$y$ 和 $z$ 方向上的运动也各自贡献一部分变化率。总的变化率就是这三部分贡献的线性叠加。

我们可以使用[梯度算子](@entry_id:275922) $\nabla$ 和向量记法将此表达式写得更为紧凑。回忆一下，函数 $f$ 的**梯度 (gradient)** 是一个向量场，定义为 $\nabla f = \langle \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}, \frac{\partial f}{\partial z} \rangle$。路径的**速度向量 (velocity vector)** 是 $\mathbf{r}'(t) = \langle \frac{dx}{dt}, \frac{dy}{dt}, \frac{dz}{dt} \rangle$。因此，链式法则可以优雅地写成[梯度向量](@entry_id:141180)与速度向量的[点积](@entry_id:149019)：

$$
\frac{dw}{dt} = \nabla f(\mathbf{r}(t)) \cdot \mathbf{r}'(t)
$$

这种形式不仅简洁，而且揭示了深刻的几何意义，我们将在下一节探讨。

**示例：沿路径的温度变化** [@problem_id:1680071]

考虑一个在晶圆表面移动的传感器。晶圆的温度[分布](@entry_id:182848)由函数 $T(x,y) = T_a + C x^2 \exp(-y^2/L^2)$ 描述。传感器沿路径 $\mathbf{r}(t) = \langle x(t), y(t) \rangle$ 移动，其中 $x(t) = v_0 t$ 且 $y(t) = y_0 + \frac{1}{2} a_0 t^2$。要计算传感器在任意时刻 $t$ 经历的温度瞬时变化率 $\frac{dT}{dt}$，我们应用[链式法则](@entry_id:190743)：
$$
\frac{dT}{dt} = \frac{\partial T}{\partial x}\frac{dx}{dt} + \frac{\partial T}{\partial y}\frac{dy}{dt}
$$
计算各偏导数和速度分量后，将它们代入即可得到 $\frac{dT}{dt}$ 作为时间 $t$ 的函数，从而可以确定在任何特定时刻的温度变化率。

**示例：沿螺旋路径的压力变化** [@problem_id:2326921]

一个在流体中移动的探测器，其所处环境的压[力场](@entry_id:147325)为 $P(x, y, z) = P_0 + \alpha x^2 y - \beta z^3$。探测器沿螺旋路径 $\mathbf{r}(t) = \langle R\cos(\omega t), R\sin(\omega t), v_z t \rangle$ 运动。要计算探测器测量的压力[瞬时变化率](@entry_id:141382) $\frac{dP}{dt}$，我们同样使用[链式法则](@entry_id:190743)的向量形式：
$$
\frac{dP}{dt} = \nabla P(\mathbf{r}(t)) \cdot \mathbf{r}'(t)
$$
首先计算压[力场](@entry_id:147325)的梯度 $\nabla P = \langle 2\alpha xy, \alpha x^2, -3\beta z^2 \rangle$ 和探测器的速度向量 $\mathbf{r}'(t) = \langle -R\omega \sin(\omega t), R\omega \cos(\omega t), v_z \rangle$。然后将[路径函数](@entry_id:144689) $\mathbf{r}(t)$ 的分量代入梯度表达式中，再与速度向量求[点积](@entry_id:149019)，即可得到 $\frac{dP}{dt}$。这个例子清晰地展示了如何将一个抽象的数学法则应用于解决具体的物理或工程问题。

### 几何诠释：方向导数与[等值面](@entry_id:196027)

[链式法则](@entry_id:190743)的向量形式 $\frac{dw}{dt} = \nabla f \cdot \mathbf{r}'(t)$ 是探索函数几何特性的有力工具。它将一个动态的过程（沿路径的变化率）与函数在某一点的静态属性（梯度）联系起来。

首先，让我们考虑一个特殊情况：物体沿直线运动。设路径为 $\mathbf{r}(t) = \mathbf{p} + t\mathbf{u}$，其中 $\mathbf{p}$ 是初始位置，$\mathbf{u}$ 是一个单位向量，代表运动方向。此时，速度向量恒为 $\mathbf{r}'(t) = \mathbf{u}$。在 $t=0$ 时刻，物体位于 $\mathbf{p}$ 点，其经历的变化率是：
$$
\frac{dw}{dt}\bigg|_{t=0} = \nabla f(\mathbf{p}) \cdot \mathbf{u}
$$
这正是函数 $f$ 在点 $\mathbf{p}$ 沿方向 $\mathbf{u}$ 的**[方向导数](@entry_id:189133) (directional derivative)** $D_{\mathbf{u}}f(\mathbf{p})$ 的定义。因此，[链式法则](@entry_id:190743)揭示了方向导数的本质：它是在一个特定方向上，函数值因位置的瞬时变化而产生的变化率。[@problem_id:1680049] 中的例子，一个深空探测器以恒定速度穿过非均匀温度场，其在某一点测得的温度变化率正是温度场在该点的梯度与探测器速度向量的[点积](@entry_id:149019)。

链式法则还揭示了[梯度向量](@entry_id:141180)与**[等值面](@entry_id:196027) (level surfaces)** 之间的基本关系。[等值面](@entry_id:196027)是指所有使得函数 $f(x, y, z)$取值为某个常数 $k$ 的点的集合，其方程为 $f(x, y, z) = k$。

现在，假设有一条曲线 $\mathbf{c}(t)$ 完全位于这个[等值面](@entry_id:196027)上。这意味着对于所有 $t$，都有 $f(\mathbf{c}(t)) = k$。由于 $k$ 是常数，这个复合函数对 $t$ 的导数恒为零：
$$
\frac{d}{dt} f(\mathbf{c}(t)) = 0
$$
根据[链式法则](@entry_id:190743)，我们知道这个导数也等于 $\nabla f(\mathbf{c}(t)) \cdot \mathbf{c}'(t)$。因此，我们得出一个至关重要的几何结论：
$$
\nabla f(\mathbf{c}(t)) \cdot \mathbf{c}'(t) = 0
$$
这个等式表明，在[等值面](@entry_id:196027)上的任意一点，该点的梯度向量 $\nabla f$ 与任何位于该平面上并通过该点的曲线的切向量 $\mathbf{c}'(t)$ 都相互正交。换言之，**梯度向量总是垂直于其所在点的[等值面](@entry_id:196027)**。梯度指向函数值增长最快的方向，而沿着[等值面](@entry_id:196027)移动则函数值不发生变化。[@problem_id:1680067] 中，一个粒子沿着椭圆柱面上的路径运动，该[曲面](@entry_id:267450)恰好是某个[标量场](@entry_id:151443) $f$ 的一个[等值面](@entry_id:196027)。通过直接计算可以验证，在运动路径上的任意一点，场的梯度与粒子的速度向量的[点积](@entry_id:149019)始终为零，这正是上述原理的具体体现。

### 推广：[多变量函数](@entry_id:145643)的复合

到目前为止，我们只考虑了最终函数值依赖于一个参数（如时间 $t$）的情形。现在我们将[链式法则](@entry_id:190743)推广到更一般的情况，其中中间变量本身就是多个[独立变量](@entry_id:267118)的函数。

假设有一个函数 $w = f(u, v)$，而中间变量 $u$ 和 $v$ 又都是另外两个[独立变量](@entry_id:267118) $s$ 和 $t$ 的函数，即 $u = u(s, t)$ 和 $v = v(s, t)$。我们想要求 $w$ 相对于 $s$ 或 $t$ 的[偏导数](@entry_id:146280)，例如 $\frac{\partial w}{\partial s}$。

此时，当我们计算对 $s$ 的[偏导数](@entry_id:146280)时，我们将 $t$ 视为常数。变量之间的依赖关系可以用一个[树状图](@entry_id:266792)来表示：$s$ 和 $t$ 是根，它们影响 $u$ 和 $v$；而 $u$ 和 $v$ 又影响最终的 $w$。要找到 $s$ 的变化对 $w$ 的总影响，我们需要沿着所有从 $s$ 到 $w$ 的路径，将路径上各段的[偏导数](@entry_id:146280)相乘，然后将所有路径的贡献相加。

因此， $w$ 对 $s$ 的偏导数是：
$$
\frac{\partial w}{\partial s} = \frac{\partial w}{\partial u}\frac{\partial u}{\partial s} + \frac{\partial w}{\partial v}\frac{\partial v}{\partial s}
$$
同理， $w$ 对 $t$ 的[偏导数](@entry_id:146280)是：
$$
\frac{\partial w}{\partial t} = \frac{\partial w}{\partial u}\frac{\partial u}{\partial t} + \frac{\partial w}{\partial v}\frac{\partial v}{\partial t}
$$
这个法则可以自然地推广到任意数量的中间变量和[独立变量](@entry_id:267118)。

**示例：计算复合函数的[偏导数](@entry_id:146280)** [@problem_id:1680078]

设[标量场](@entry_id:151443) $w(u, v) = u \ln(v)$，其中 $u(s, t) = s^2 + t^2$，$v(s, t) = s t$。为了求 $\frac{\partial w}{\partial s}$，我们应用上述法则：
$$
\frac{\partial w}{\partial s} = \frac{\partial w}{\partial u}\frac{\partial u}{\partial s} + \frac{\partial w}{\partial v}\frac{\partial v}{\partial s} = (\ln v)(2s) + \left(\frac{u}{v}\right)(t)
$$
为了在特定点（例如 $(s, t) = (2, 1)$）求值，我们首先计算该点对应的中间变量值 $u(2,1)=5$ 和 $v(2,1)=2$，然后将所有值代入上式，即可得到最终结果。

一个非常重要的应用是在不同[坐标系](@entry_id:156346)之间转换偏导数。例如，将一个定义在笛卡尔坐标 $(x,y)$ 下的函数 $h(x,y)$ 的导数用极坐标 $(r, \theta)$ 来表示。它们之间的关系是 $x = r\cos(\theta)$ 和 $y = r\sin(\theta)$。要计算径向导数 $\frac{\partial h}{\partial r}$，我们将 $h$ 视为 $r$ 和 $\theta$ 的复合函数，并应用[链式法则](@entry_id:190743)（此时将 $\theta$ 视为常数）：
$$
\frac{\partial h}{\partial r} = \frac{\partial h}{\partial x}\frac{\partial x}{\partial r} + \frac{\partial h}{\partial y}\frac{\partial y}{\partial r} = \frac{\partial h}{\partial x}\cos(\theta) + \frac{\partial h}{\partial y}\sin(\theta)
$$
这个结果在物理和工程中非常有用，例如，分析在径向方向上移动的探测器所经历的场量变化 [@problem_id:2326954]。

### 矩阵形式：[雅可比矩阵](@entry_id:264467)

[链式法则](@entry_id:190743)的最通用和最强大的形式是用矩阵来表述的。这种形式适用于[向量值函数](@entry_id:261164)的复合，即从 $\mathbb{R}^n$ 到 $\mathbb{R}^m$ 的映射。

对于一个可微的向量函数（或称映射）$\mathbf{F}: \mathbb{R}^n \to \mathbb{R}^m$，其在某一点的导数不再是一个数或一个向量，而是一个线性变换，这个线性变换由一个 $m \times n$ 的[矩阵表示](@entry_id:146025)，称为**[雅可比矩阵](@entry_id:264467) (Jacobian matrix)**，记作 $D\mathbf{F}$。如果 $\mathbf{y} = \mathbf{F}(\mathbf{x})$，其中 $\mathbf{x} = (x_1, \dots, x_n)$ 和 $\mathbf{y} = (y_1, \dots, y_m)$，则雅可比矩阵的第 $i$ 行第 $j$ 列的元素是 $(D\mathbf{F})_{ij} = \frac{\partial y_i}{\partial x_j}$。

$$
D\mathbf{F} = \frac{\partial(y_1, \dots, y_m)}{\partial(x_1, \dots, x_n)} = \begin{pmatrix}
\frac{\partial y_1}{\partial x_1}  \cdots  \frac{\partial y_1}{\partial x_n} \\
\vdots  \ddots  \vdots \\
\frac{\partial y_m}{\partial x_1}  \cdots  \frac{\partial y_m}{\partial x_n}
\end{pmatrix}
$$
[雅可比矩阵](@entry_id:264467)的本质是函数在某一点附近的**[最佳线性逼近](@entry_id:164642)**。例如，从柱坐标 $(\rho, \phi, z)$ 到笛卡尔坐标 $(x, y, z)$ 的变换可以看作一个映射 $\mathbf{F}: (\rho, \phi, z) \mapsto (x, y, z)$，其中 $x = \rho \cos(\phi), y = \rho \sin(\phi), z = z$。它的[雅可比矩阵](@entry_id:264467)可以通过计算所有九个可能的偏导数得到 [@problem_id:1680046]。

现在，考虑两个映射的复合：$\mathbf{F}: \mathbb{R}^n \to \mathbb{R}^m$ 和 $\mathbf{G}: \mathbb{R}^m \to \mathbb{R}^p$。复合映射为 $\mathbf{H} = \mathbf{G} \circ \mathbf{F}$，它将 $\mathbb{R}^n$ 中的点映射到 $\mathbb{R}^p$ 中。[多变量链式法则](@entry_id:146671)的矩阵形式表明，复合映射 $\mathbf{H}$ 在点 $\mathbf{x}$ 的[雅可比矩阵](@entry_id:264467)，等于映射 $\mathbf{G}$ 在点 $\mathbf{F}(\mathbf{x})$ 的雅可比矩阵与映射 $\mathbf{F}$ 在点 $\mathbf{x}$ 的[雅可比矩阵](@entry_id:264467)的**矩阵乘积**：

$$
D\mathbf{H}(\mathbf{x}) = D\mathbf{G}(\mathbf{F}(\mathbf{x})) \cdot D\mathbf{F}(\mathbf{x})
$$

这个法则的直观意义是：复合映射的[线性逼近](@entry_id:142309)是各个映射[线性逼近](@entry_id:142309)的复合。

如果映射的输入和输出空间维数相同（$n=m=p$），雅可比矩阵就是方阵。在这种情况下，我们可以讨论它的[行列式](@entry_id:142978)，即**[雅可比行列式](@entry_id:137120) (Jacobian determinant)**，它衡量了映射在局部如何缩放体积。根据[矩阵行列式](@entry_id:194066)的乘法法则，我们有：
$$
\det(D\mathbf{H}) = \det(D\mathbf{G}) \cdot \det(D\mathbf{F})
$$
这在进行多重[积分的[变量替](@entry_id:178219)换](@entry_id:141386)时至关重要。例如，一个从笛卡尔坐标到对数-极坐标的变换可以分解为两步：先从笛卡尔到极坐标，再从极坐标到对数-极坐标 [@problem_id:1680066]。总变换的雅可比行列式可以通过计算每一步变换的雅可比行列式然后将它们相乘得到，这往往比直接计算总变换的[雅可比行列式](@entry_id:137120)要简单。

### [链式法则](@entry_id:190743)的高级应用

[链式法则](@entry_id:190743)是许多高等数学概念和技术的基础。以下是几个重要的例子。

#### [隐函数求导](@entry_id:137929)

在许多科学应用中，变量之间的关系是通过一个方程 $F(x, y, z) = 0$ 以隐式方式给出的，而不是形如 $z = f(x, y)$ 的显式函数。链式法则为我们提供了一种求隐函数[偏导数](@entry_id:146280)的系统方法。

假设方程 $F(x, y, z) = 0$ 在某点附近隐式地定义了 $z$ 是 $x$ 和 $y$ 的函数，即 $z = z(x, y)$。将此关系代入方程，我们得到一个恒等式：$F(x, y, z(x, y)) = 0$。现在，我们可以用[链式法则](@entry_id:190743)对这个恒等式两边关于 $x$ 求偏导（同时将 $y$ 视为常数）：
$$
\frac{\partial F}{\partial x}\frac{\partial x}{\partial x} + \frac{\partial F}{\partial y}\frac{\partial y}{\partial x} + \frac{\partial F}{\partial z}\frac{\partial z}{\partial x} = 0
$$
由于 $\frac{\partial x}{\partial x} = 1$ 和 $\frac{\partial y}{\partial x} = 0$（因为 $x$ 和 $y$ 是独立变量），上式简化为：
$$
\frac{\partial F}{\partial x} + \frac{\partial F}{\partial z}\frac{\partial z}{\partial x} = 0
$$
只要 $\frac{\partial F}{\partial z} \neq 0$，我们就可以解出所需的[偏导数](@entry_id:146280)：
$$
\frac{\partial z}{\partial x} = - \frac{\frac{\partial F}{\partial x}}{\frac{\partial F}{\partial z}}
$$
同理可得 $\frac{\partial z}{\partial y} = - \frac{\frac{\partial F}{\partial y}}{\frac{\partial F}{\partial z}}$。这个强大的技术使我们无需解出 $z$ 的显式表达式就能计算其[偏导数](@entry_id:146280)。例如，在[热力学](@entry_id:141121)中，范德华方程 $\left( P + \frac{a}{V_m^2} \right) (V_m - b) = RT$ 隐式地定义了压力 $P$、[摩尔体积](@entry_id:145604) $V_m$ 和温度 $T$ 之间的关系。我们可以利用[隐函数求导](@entry_id:137929)法则来计算诸如 $\left(\frac{\partial P}{\partial T}\right)_{V_m}$ 这样的重要[热力学](@entry_id:141121)系数 [@problem_id:2326946]。

#### [反函数](@entry_id:141256)的雅可比矩阵

[链式法则](@entry_id:190743)的矩阵形式也为我们提供了一种计算[反函数](@entry_id:141256)[雅可比矩阵](@entry_id:264467)的巧妙方法，而无需先求出[反函数](@entry_id:141256)的解析表达式。

假设有一个可逆的映射 $\mathbf{y} = \mathbf{F}(\mathbf{x})$，其[反函数](@entry_id:141256)为 $\mathbf{x} = \mathbf{F}^{-1}(\mathbf{y})$。根据反函数的定义，我们有恒等式 $\mathbf{F}^{-1}(\mathbf{F}(\mathbf{x})) = \mathbf{x}$。对这个恒等式两边关于 $\mathbf{x}$ 使用矩阵链式法则求导，我们得到：
$$
D(\mathbf{F}^{-1})(\mathbf{F}(\mathbf{x})) \cdot D\mathbf{F}(\mathbf{x}) = I
$$
其中 $I$ 是单位矩阵（作为恒等映射 $\mathbf{x} \mapsto \mathbf{x}$ 的雅可比矩阵）。

从这个方程中，只要 $D\mathbf{F}(\mathbf{x})$ 是[可逆矩阵](@entry_id:171829)，我们就可以解出反函数的[雅可比矩阵](@entry_id:264467)：
$$
D(\mathbf{F}^{-1})(\mathbf{F}(\mathbf{x})) = [D\mathbf{F}(\mathbf{x})]^{-1}
$$
令 $\mathbf{y} = \mathbf{F}(\mathbf{x})$，则 $\mathbf{x} = \mathbf{F}^{-1}(\mathbf{y})$。代入上式，我们得到最终的公式：
$$
D(\mathbf{F}^{-1})(\mathbf{y}) = [D\mathbf{F}(\mathbf{F}^{-1}(\mathbf{y}))]^{-1}
$$
这个公式的含义是：**[反函数](@entry_id:141256)在点 $\mathbf{y}$ 的[雅可比矩阵](@entry_id:264467)，是原函数在对应点 $\mathbf{x} = \mathbf{F}^{-1}(\mathbf{y})$ 的雅可比矩阵的逆矩阵。**
在实际问题中 [@problem_id:1680048]，如果我们想求一个复杂变换的反变换在某点的[雅可比矩阵](@entry_id:264467)，我们不需要费力去求反变换的表达式。我们只需要找到该点是由原空间的哪个点映射过来的，然后计算原变换在该点的雅可比矩阵，最后求该[矩阵的逆](@entry_id:140380)即可。这在计算上通常要简单得多。

#### [微分形式](@entry_id:146747)的变换

链式法则也是理解[微分几何](@entry_id:145818)中一个核心对象——**[微分形式](@entry_id:146747) (differential forms)** 如何在[坐标变换](@entry_id:172727)下表现的基础。考虑一个在 $(x,y)$ 平面上的 [1-形式](@entry_id:270392) $\omega = P(x,y) dx + Q(x,y) dy$。当我们引入新的[坐标系](@entry_id:156346) $(u,v)$ 时，其中 $x=x(u,v), y=y(u,v)$，我们想知道 $\omega$ 在新[坐标系](@entry_id:156346)下的表达式 $\omega = \tilde{P}(u,v) du + \tilde{Q}(u,v) dv$。

为了找到新旧分量之间的关系，我们应用链式法则于[微分](@entry_id:158718) $dx$ 和 $dy$：
$$
dx = \frac{\partial x}{\partial u} du + \frac{\partial x}{\partial v} dv
$$
$$
dy = \frac{\partial y}{\partial u} du + \frac{\partial y}{\partial v} dv
$$
将这两个表达式以及 $P$ 和 $Q$ 用 $u, v$ 表示的式子代入 $\omega$ 的原始定义中，然后重新整理关于 $du$ 和 $dv$ 的项，我们就能得到新分量 $\tilde{P}$ 和 $\tilde{Q}$ 的表达式。例如，$\tilde{Q}(u,v)$ 将是所有 $dv$ 项的系数之和：
$$
\tilde{Q}(u,v) = P(x(u,v), y(u,v)) \frac{\partial x}{\partial v} + Q(x(u,v), y(u,v)) \frac{\partial y}{\partial v}
$$
这个变换规则被称为[1-形式](@entry_id:270392)的**[拉回](@entry_id:160816) (pullback)**，它是[链式法则](@entry_id:190743)在[微分几何](@entry_id:145818)语言中的直接体现 [@problem_id:1680081]。

综上所述，[多变量链式法则](@entry_id:146671)是微积分中一个具有深远影响的统一性原理。它不仅是进行计算的实用工具，更是一种深刻的思维方式，揭示了变化率、几何结构和坐标变换之间的内在联系。