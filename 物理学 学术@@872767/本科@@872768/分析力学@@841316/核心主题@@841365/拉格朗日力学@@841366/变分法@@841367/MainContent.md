## 引言
变分法是[数学分析](@entry_id:139664)中的一个强大分支，其核心思想是寻找一个函数，使得某个依赖于该函数的积分值（称为泛函）达到极大或极小。从寻找两点间的最短路径，到推导自然界的基本物理定律，[变分原理](@entry_id:198028)提供了一个深刻而统一的视角来理解和解决各种[优化问题](@entry_id:266749)。然而，对于初学者而言，从抽象的泛函概念到具体的求解方程，往往存在一道难以跨越的鸿沟。本文旨在系统地填补这一知识空白，引领读者深入[变分法](@entry_id:163656)的世界。

在接下来的内容中，我们将分三步展开：首先，在 **“原理与机制”** 一章中，我们将详细推导[变分法](@entry_id:163656)的基石——欧拉-拉格朗-日方程，并探讨其在不同条件下的简化形式和物理意义。接着，在 **“应用与跨学科联系”** 一章中，我们将展示[变分法](@entry_id:163656)如何作为一种普适工具，在经典力学、几何学、[场论](@entry_id:155241)、工程设计乃至量子力学和经济学中大放异彩。最后，通过 **“动手实践”** 部分，你将有机会亲手应用所学知识，解决具体的[变分问题](@entry_id:756445)，从而巩固理解。让我们一同开始这段探索最优路径与基本定律的奇妙旅程。

## 原理与机制

在上一章中，我们介绍了变分法作为一个旨在寻找使某个积分量（称为 **泛函**）取[极值](@entry_id:145933)的函数的数学分支。现在，我们将深入探讨其核心原理和工作机制。[变分法](@entry_id:163656)的威力在于它提供了一个统一的框架来解决物理学、工程学和几何学中大量的[优化问题](@entry_id:266749)，从寻找两点间的最短路径到推导基本物理定律。本章的目标是系统地建立并阐释[变分法](@entry_id:163656)的中心方程—— **[欧拉-拉格朗日方程](@entry_id:137827) (Euler-Lagrange equation)**，并探索其各种形式、简化和推广。

### 泛函与[欧拉-拉格朗日方程](@entry_id:137827)

让我们从最基本的问题形式开始。考虑一个依赖于未知函数 $y(x)$ 及其一阶导数 $y'(x) = \frac{dy}{dx}$ 的泛函，其形式如下：

$$J[y] = \int_{x_1}^{x_2} L(x, y(x), y'(x)) \, dx$$

在这里，函数 $L(x, y, y')$ 被称为 **[拉格朗日量](@entry_id:174593) (Lagrangian)**。我们的任务是找到一个函数 $y(x)$，它在两个固定的端点 $y(x_1) = y_1$ 和 $y(x_2) = y_2$ 之间连接，并使得泛函 $J[y]$ 的值是 **平稳的 (stationary)**，即取极大值、极小值或[鞍点](@entry_id:142576)值。

这个任务类似于普通微积分中寻找函数 $f(x)$ 的[极值](@entry_id:145933)点，我们需要找到使导数 $f'(x)$ 为零的点。在[变分法](@entry_id:163656)中，我们需要找到一种“函数求导”的方法。其基本思想是考虑对[目标函数](@entry_id:267263) $y(x)$ 进行微小的 **变分 (variation)**。假设 $y(x)$ 是使泛函 $J$ 平稳的真实路径。我们可以构造一个包含真实路径的函数族：

$$y(\epsilon, x) = y(0, x) + \epsilon \eta(x)$$

其中 $y(0, x) = y(x)$ 就是我们寻找的[极值](@entry_id:145933)函数，$\eta(x)$ 是一个在端点处为零（即 $\eta(x_1) = \eta(x_2) = 0$）的任意、可微的函数，而 $\epsilon$ 是一个很小的实数参数。当 $\epsilon=0$ 时，我们回到真实路径。

现在，泛函 $J$ 成为一个关于参数 $\epsilon$ 的普通函数 $J(\epsilon)$。如果 $y(x)$ 是一个极值函数，那么 $J(\epsilon)$ 在 $\epsilon=0$ 处必然有极值，这意味着其导数必须为零：

$$\left. \frac{dJ}{d\epsilon} \right|_{\epsilon=0} = 0$$

通过在积分号下对 $\epsilon$ 求导，我们得到：

$$\frac{dJ}{d\epsilon} = \int_{x_1}^{x_2} \left( \frac{\partial L}{\partial y} \frac{\partial y}{\partial \epsilon} + \frac{\partial L}{\partial y'} \frac{\partial y'}{\partial \epsilon} \right) dx = \int_{x_1}^{x_2} \left( \frac{\partial L}{\partial y} \eta(x) + \frac{\partial L}{\partial y'} \eta'(x) \right) dx$$

为了使方程中只出现 $\eta(x)$ 而不是其导数，我们对第二项使用 **[分部积分法](@entry_id:136350)**：

$$\int_{x_1}^{x_2} \frac{\partial L}{\partial y'} \eta'(x) dx = \left[ \frac{\partial L}{\partial y'} \eta(x) \right]_{x_1}^{x_2} - \int_{x_1}^{x_2} \frac{d}{dx}\left(\frac{\partial L}{\partial y'}\right) \eta(x) dx$$

由于边界条件要求变分在端点为零，即 $\eta(x_1) = \eta(x_2) = 0$，边界项 $\left[ \frac{\partial L}{\partial y'} \eta(x) \right]_{x_1}^{x_2}$ 自然消失。将此结果代回原方程，我们得到：

$$\left. \frac{dJ}{d\epsilon} \right|_{\epsilon=0} = \int_{x_1}^{x_2} \left( \frac{\partial L}{\partial y} - \frac{d}{dx}\left(\frac{\partial L}{\partial y'}\right) \right) \eta(x) dx = 0$$

根据 **变分法基本引理 (fundamental lemma of calculus of variations)**，如果这个积分对于任何满足条件的函数 $\eta(x)$ 都等于零，那么括号内的表达式本身必须处处为零。由此，我们得到了[变分法](@entry_id:163656)的核心方程—— **[欧拉-拉格朗日方程](@entry_id:137827)**：

$$\frac{\partial L}{\partial y} - \frac{d}{dx}\left(\frac{\partial L}{\partial y'}\right) = 0$$

任何使得泛函 $J[y]$ 平稳的函数 $y(x)$ 都必须满足这个[二阶常微分方程](@entry_id:204212)。

作为一个直接的应用，考虑寻找使泛函 $J[y] = \int_{x_1}^{x_2} (y'^2 + 2xy) dx$ 取极值的函数 $y(x)$ [@problem_id:1281]。这里的[拉格朗日量](@entry_id:174593)是 $L(x, y, y') = y'^2 + 2xy$。我们计算所需的偏导数：
$\frac{\partial L}{\partial y} = 2x$ 和 $\frac{\partial L}{\partial y'} = 2y'$。
代入欧拉-拉格朗日方程，得到：
$$2x - \frac{d}{dx}(2y') = 0 \quad \Longrightarrow \quad 2x - 2y'' = 0 \quad \Longrightarrow \quad y'' = x$$
这是一个简单的[二阶常微分方程](@entry_id:204212)。通过两次积分，我们得到通解 $y(x) = \frac{x^3}{6} + C_1 x + C_2$。积分常数 $C_1$ 和 $C_2$ 的值由具体的边界条件 $y(x_1)=y_1$ 和 $y(x_2)=y_2$ 确定。

另一个重要的例子来自物理学，考虑泛函 $J[y] = \int (y'^2 - k^2 y^2) dx$ [@problem_id:1260]。这个泛函描述了简谐振子的行为。其拉格朗日量为 $L = y'^2 - k^2 y^2$。应用[欧拉-拉格朗日方程](@entry_id:137827)：
$\frac{\partial L}{\partial y} = -2k^2 y$ 和 $\frac{\partial L}{\partial y'} = 2y'$。
方程变为 $-2k^2 y - \frac{d}{dx}(2y') = 0$，即：
$$y'' + k^2 y = 0$$
这个方程正是描述简谐运动的方程，其通解为 $y(x) = A\cos(kx) + B\sin(kx)$。

### 拉格朗日量的特殊情况与守恒律

当[拉格朗日量](@entry_id:174593) $L$ 具有某些对称性时，欧拉-拉格朗日方程可以被简化，从而揭示出深刻的物理守恒律。

#### 拉格朗日量不显含 $y$

如果 $L$ 不显式地依赖于 $y$，即 $\frac{\partial L}{\partial y} = 0$，那么欧拉-拉格朗日方程简化为：

$$\frac{d}{dx}\left(\frac{\partial L}{\partial y'}\right) = 0$$

这意味着量 $p_y = \frac{\partial L}{\partial y'}$ 是一个常数。在[分析力学](@entry_id:166738)中，这个量被称为[广义动量](@entry_id:165699)。

一个经典的例子是寻找圆柱体表面上的最短路径，即 **[测地线](@entry_id:269969) (geodesic)** [@problem_id:1268]。对于一个半径为 $R$ 的圆柱，其上的[弧长](@entry_id:191173)微元在[柱坐标系](@entry_id:266798) $(\rho, \phi, z)$ 中为 $ds^2 = \rho^2 d\phi^2 + dz^2$（因为 $\rho=R$ 是常数，所以 $d\rho=0$）。如果我们用角坐标 $\phi$ 来[参数化](@entry_id:272587)路径，即 $z=z(\phi)$，则[弧长泛函](@entry_id:265800)为：

$$S[z] = \int_{\phi_1}^{\phi_2} \sqrt{R^2 + \left(\frac{dz}{d\phi}\right)^2} \, d\phi$$

这里的[拉格朗日量](@entry_id:174593)是 $L(z, z') = \sqrt{R^2 + (z')^2}$，其中 $z' = \frac{dz}{d\phi}$。由于 $L$ 不显式依赖于 $z$（路径的高度），我们有 $\frac{\partial L}{\partial z} = 0$。因此，其[共轭动量](@entry_id:172203)是一个常数：

$$\frac{\partial L}{\partial z'} = \frac{z'}{\sqrt{R^2 + (z')^2}} = C$$

通过代数运算可以解出 $z'$，结果表明 $z'$ 必须是一个常数。这意味着 $z' = \frac{dz}{d\phi}$ 是一个常数，积分后得到 $z(\phi) = C\phi + D$。这说明圆柱体上的最短路径是一条螺旋线。如果我们展开圆柱表面，螺旋线就变成了一条直线，这与我们的直觉相符。

#### [拉格朗日量](@entry_id:174593)不显含 $x$ (贝尔特拉米等式)

当拉格朗日量 $L$ 不显式依赖于[自变量](@entry_id:267118) $x$（即 $\frac{\partial L}{\partial x} = 0$）时，存在一个非常有用的[首次积分](@entry_id:261013)，称为 **贝尔特拉米等式 (Beltrami identity)**。这个守恒律源于系统在 $x$ 方向上的[平移不变性](@entry_id:195885)。其形式为：

$$L - y' \frac{\partial L}{\partial y'} = \text{constant}$$

这个等式可以将一个二阶的[欧拉-拉格朗日方程](@entry_id:137827)降为一阶，从而大大简化求解过程。

考虑一个泛函，其[拉格朗日量](@entry_id:174593)为 $L(y, y') = y^2 (y')^2$ [@problem_id:1274]。由于 $L$ 不依赖于 $x$，我们可以使用贝尔特拉米等式。计算 $\frac{\partial L}{\partial y'} = 2y^2 y'$，代入等式：

$$y^2 (y')^2 - y'(2y^2 y') = -y^2 (y')^2 = C$$

其中 $C$ 是一个常数。这个[一阶微分方程](@entry_id:173139)比直接应用[欧拉-拉格朗日方程](@entry_id:137827)要容易得多。

一个深刻的物理应用是 **[费马原理](@entry_id:175608) (Fermat's principle)**，它指出光在两点之间传播的路径是耗时最短的路径。在[折射率](@entry_id:168910)为 $n(x, y)$ 的介质中，光的传播时间为 $T = \int \frac{n \, ds}{c}$，其中 $c$ 是真空光速，$ds$ 是[弧长](@entry_id:191173)微元。为了最小化时间，我们只需最小化[光程](@entry_id:178906) $S = \int n \, ds$。对于二维平面上的路径 $y(x)$，这变为：

$$S[y] = \int n(x, y) \sqrt{1 + (y')^2} \, dx$$

现在，考虑一个[折射率](@entry_id:168910)只随深度 $y$ 变化的介质，即 $n = n(y)$ [@problem_id:1260696]。这种情况下，[拉格朗日量](@entry_id:174593) $L = n(y) \sqrt{1 + (y')^2}$ 不显式依赖于 $x$。应用贝尔特拉米等式得到：

$$n(y) \sqrt{1 + (y')^2} - y' \frac{n(y) y'}{\sqrt{1 + (y')^2}} = \text{constant}$$

化简后得到：

$$\frac{n(y)}{\sqrt{1 + (y')^2}} = \text{constant}$$

如果我们用路径与 $x$ 轴的夹角 $\alpha$ 来表示斜率，即 $y' = \tan \alpha$，那么 $\sqrt{1+(y')^2} = \sec \alpha = 1/\cos \alpha$。因此，上式变为 $n(y) \cos \alpha = \text{constant}$。这正是 **斯涅尔定律 (Snell's Law)** 在连续变化介质中的推广形式。它表明，尽管光的路径是弯曲的，但在每一点，[折射率](@entry_id:168910)与路径和水平线夹角的余弦之积是一个[守恒量](@entry_id:150267)。

### [变分原理](@entry_id:198028)的推广

基本的[变分问题](@entry_id:756445)可以向多个方向推广，以适应更复杂的物理和几何情境。

#### [等周问题](@entry_id:190109)与[拉格朗日乘子](@entry_id:142696)

**[等周问题](@entry_id:190109) (isoperimetric problem)** 是指在满足某个积分约束的条件下，寻求另一个积分泛函的极值。例如，在所有[周长](@entry_id:263239)固定的封闭曲线中，哪一条能围成最大的面积？

解决这类问题的标准方法是使用 **拉格朗日乘子法 (method of Lagrange multipliers)**。假设我们要极化泛函 $J[y] = \int L(y,y',x) dx$，同时满足约束条件 $K[y] = \int G(y,y',x) dx = \text{constant}$。我们可以构造一个新的、无约束的泛函 $J^*[y]$，其[拉格朗日量](@entry_id:174593)为 $L^* = L + \lambda G$，其中 $\lambda$ 是一个待定的常数，称为拉格朗日乘子。然后对 $J^*$ 应用标准的欧拉-拉格朗日方程：

$$\frac{\partial (L + \lambda G)}{\partial y} - \frac{d}{dx}\left(\frac{\partial (L + \lambda G)}{\partial y'}\right) = 0$$

求解这个方程会得到一个依赖于 $\lambda$ 的解族。最后，我们将解代入约束条件 $K[y]$ 来确定 $\lambda$ 的具体值。

例如，考虑在满足 $y(0)=0$、$y(1)=0$ 和约束 $\int_0^1 (y')^2 dx = 1$ 的条件下，最大化泛函 $J[y] = \int_0^1 xy \, dx$ [@problem_id:1275]。这里 $L = xy$，$G = (y')^2$。我们构造[增广拉格朗日量](@entry_id:177042) $L^* = xy + \lambda (y')^2$。对其应用欧拉-拉格朗日方程：

$$\frac{\partial L^*}{\partial y} = x, \quad \frac{\partial L^*}{\partial y'} = 2\lambda y'$$
$$x - \frac{d}{dx}(2\lambda y') = 0 \quad \Longrightarrow \quad 2\lambda y'' = x$$

这个方程的解为 $y(x) = \frac{x^3}{12\lambda} + C_1 x + C_2$。利用边界条件 $y(0)=0$ 和 $y(1)=0$ 可以确定 $C_1$ 和 $C_2$（关于 $\lambda$）。最后，将得到的 $y(x)$ 代入约束 $\int_0^1 (y')^2 dx = 1$，即可解出 $\lambda$ 的值。

#### 依赖[高阶导数](@entry_id:140882)的泛函

在某些物理问题中，[拉格朗日量](@entry_id:174593)可能依赖于函数的高阶导数，例如 $y''$。一个典型的例子是弹性梁的弯曲。对于小挠度，梁的弯曲势能正比于其曲率平方的积分。如果用 $y''(x)$ 来近似曲率，[能量泛函](@entry_id:170311)为：

$$J[y] = \int_{x_1}^{x_2} L(x, y, y', y'') dx$$

通过对变分过程进行两次[分部积分](@entry_id:136350)，可以推导出适用于这种情况的 **[欧拉-泊松方程](@entry_id:749105) (Euler-Poisson equation)**：

$$\frac{\partial L}{\partial y} - \frac{d}{dx}\left(\frac{\partial L}{\partial y'}\right) + \frac{d^2}{dx^2}\left(\frac{\partial L}{\partial y''}\right) = 0$$

考虑一个两端被固定的弹性梁，其[弯曲能](@entry_id:174691)量为 $J[y] = \int_0^L (y'')^2 dx$ [@problem_id:1260540]。这里的[拉格朗日量](@entry_id:174593)是 $L=(y'')^2$。它不依赖于 $y$ 和 $y'$，所以[欧拉-泊松方程](@entry_id:749105)的前两项为零，方程简化为：

$$\frac{d^2}{dx^2}\left(\frac{\partial L}{\partial y''}\right) = 0 \quad \Longrightarrow \quad \frac{d^2}{dx^2}(2y'') = 0 \quad \Longrightarrow \quad y^{(4)}(x) = 0$$

这个四阶[微分方程](@entry_id:264184)的通解是一个三次多项式 $y(x) = ax^3 + bx^2 + cx + d$。四个积分常数由四个边界条件确定，例如两端的位置和斜率，从而唯一确定了梁的平衡形状。

#### 自然边界条件

在推导欧拉-拉格朗日方程时，我们假设了变分 $\eta(x)$ 在端点为零。但如果某个端点是自由的，或者受到某种力的约束，该怎么办？

让我们回到分部积分的边界项：$\left[ \frac{\partial L}{\partial y'} \eta(x) \right]_{x_1}^{x_2}$。如果端点 $x_2$ 上的变分 $\eta(x_2)$ 不为零（即端点是自由的），那么为了使总变分为零，我们必须要求在该端点处：

$$\left. \frac{\partial L}{\partial y'} \right|_{x=x_2} = 0$$

这被称为 **自然边界条件 (natural boundary condition)**。它不是预先规定的，而是从变分原理本身推导出来的。

更一般地，如果作用量本身包含边界项，例如一个弹簧连接在端点上，其[势能](@entry_id:748988)为 $\frac{1}{2}k(y(L,t))^2$ [@problem_id:1260641]。[作用量泛函](@entry_id:169216)为：

$$S[y] = \int_{t_1}^{t_2} \left[ \int_0^L L(y_t, y_x) dx - \frac{1}{2}k (y(L,t))^2 \right] dt$$

其中 $y_t = \frac{\partial y}{\partial t}$，$y_x = \frac{\partial y}{\partial x}$，$L = \frac{1}{2}\rho y_t^2 - \frac{1}{2}T y_x^2$ 是弦的动能和[势能](@entry_id:748988)密度。变分 $\delta S$ 不仅包含[体积分](@entry_id:171119)项（它给出了[波动方程](@entry_id:139839) $\rho y_{tt} - T y_{xx} = 0$），还包含一个边界项：

$$\delta S_{\text{boundary}} = \int_{t_1}^{t_2} \left[ -T y_x(L,t) - k y(L,t) \right] \delta y(L,t) dt$$

由于在 $x=L$ 处的变分 $\delta y(L,t)$ 是任意的，为了使 $\delta S$ 始终为零，括号内的表达式必须为零。这给出了自然边界条件：

$$T \frac{\partial y}{\partial x}(L,t) + k y(L,t) = 0$$

这个条件在物理上表示在弦的末端，弦的张力在竖直方向的分量 $(-T y_x)$ 与弹簧的恢复力 $(-k y)$ 相平衡。

#### 多维推广：[场论](@entry_id:155241)

[变分原理](@entry_id:198028)可以从描述粒子路径的单变量函数 $y(x)$ 推广到描述物理场的[多元函数](@entry_id:145643)，如 $u(x,y,z)$。在这种情况下，泛函是在一个体积 $\Omega$ 上的积分，拉格朗日量依赖于场 $u$ 及其梯度 $\nabla u$：

$$J[u] = \int_{\Omega} L(x, u, \nabla u) dV$$

通过与一维情况类似的推导，但使用 **[散度定理](@entry_id:143110) (divergence theorem)** 来代替[分部积分](@entry_id:136350)，我们可以得到适用于[场的欧拉-拉格朗日方程](@entry_id:173994)，这是一个[偏微分方程(PDE)](@entry_id:166689) [@problem_id:2691373]：

$$\frac{\partial L}{\partial u} - \nabla \cdot \left(\frac{\partial L}{\partial (\nabla u)}\right) = 0$$

这里 $\frac{\partial L}{\partial (\nabla u)}$ 是一个向量，其分量是 $L$ 对 $\nabla u$ 各个分量的偏导数。

例如，考虑一个由[拉格朗日量密度](@entry_id:156695) $L = \frac{1}{2}a |\nabla u|^2 - fu$ 描述的[标量场](@entry_id:151443) $u$，其中 $a$ 和 $f$ 是常数。计算[偏导数](@entry_id:146280)：
$\frac{\partial L}{\partial u} = -f$ 和 $\frac{\partial L}{\partial (\nabla u)} = a \nabla u$。
代入[场的欧拉-拉格朗日方程](@entry_id:173994)，我们得到：
$$-f - \nabla \cdot (a \nabla u) = 0 \quad \Longrightarrow \quad -a \Delta u = f$$
其中 $\Delta = \nabla \cdot \nabla$ 是拉普拉斯算子。这正是 **泊松方程 (Poisson's equation)**，它是静电学、[引力](@entry_id:175476)理论和许多其他物理领域的基础方程。这个例子有力地证明了变分原理作为描述自然界基本规律的深刻而普适的工具的地位。

通过本章的学习，我们已经看到，一个简单的变分原理——寻找使某个积分平稳的路径——能够生成描述从几何路径到复杂物理场的各种现象的[微分方程](@entry_id:264184)。欧拉-拉格朗日方程及其推广是连接这一原理与具体数学模型的关键桥梁。