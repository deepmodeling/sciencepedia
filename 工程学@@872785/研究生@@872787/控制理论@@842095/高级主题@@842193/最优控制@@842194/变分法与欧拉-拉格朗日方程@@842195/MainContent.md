## 引言
[变分法](@entry_id:163656)是数学分析的一个强大分支，它致力于解决一类深刻的[优化问题](@entry_id:266749)：在所有可能的函数中，哪一个能使某个特定量（如时间、能量或成本）达到最小值或最大值？与标准微积分寻找函数极值点不同，变分法寻找的是“极值函数”。这一根本性的转变开启了通往理解自然法则与最优设计原理的大门。从[最速降线](@entry_id:178084)上滚动的物体，到行星围绕太阳的轨迹，再到现代工程中的最优控制策略，其背后都隐藏着一个寻求最优路径的[变分问题](@entry_id:756445)。然而，我们如何从无限的函数海洋中精确地捕获这一个最优解呢？

本文旨在系统地回答这一问题，为读者构建一个关于变分法及其核心工具——[欧拉-拉格朗日方程](@entry_id:137827)的完整知识体系。我们将分三个章节逐步深入：
- 在“原理与机制”一章中，我们将从第一性原理出发，通过引入泛函和变分的概念，严谨地推导出[欧拉-拉格朗日方程](@entry_id:137827)。我们还将探讨其与守恒律的内在联系，并将其推广至更高维度和更复杂的情形。
- 接着，在“应用与跨学科联系”一章，我们将跨越从经典力学、最优控制到广义相对论和计算机视觉等多个领域，展示变分原理作为一种普适的建模语言，如何统一描述和解决看似迥异的科学与工程问题。
- 最后，通过一系列精心设计的“动手实践”，您将有机会亲自应用所学理论，解决具体的[变分问题](@entry_id:756445)，从而巩固和深化理解。

通过本次学习，您将不仅掌握一个强大的数学方法，更将获得一种看待物理世界和[优化问题](@entry_id:266749)的全新视角。让我们从最基本的原理开始，探索变分法的奥秘。

## 原理与机制

在引言章节中，我们初步探讨了[变分法](@entry_id:163656)作为一种工具，用于解决寻求最优函数的[优化问题](@entry_id:266749)。本章将深入探讨其核心的数学原理与机制，从最基本的第一性原理出发，系统地推导和阐释[欧拉-拉格朗日方程](@entry_id:137827)及其各种推广形式。我们将看到，这一强大的数学工具不仅是理论物理的基石，也在现代控制理论、工程学和计算机科学中扮演着至关重要的角色。

### 泛函与变分：核心思想

在标准的微积分中，我们处理的是将一个或多个数映射到另一个数的函数，例如 $f(x) = x^2$。[变分法](@entry_id:163656)处理的对象则更为抽象，它研究的是**泛函 (functionals)**。一个泛函可以被看作是“函数的函数”，它接收一个函数作为输入，并返回一个标量值。一个典型的例子是连接平面上两点 $(a, y_a)$ 和 $(b, y_b)$ 的所有可能曲线 $y(x)$ 的[弧长泛函](@entry_id:265800)：

$$
S[y] = \int_{a}^{b} \sqrt{1 + [y'(x)]^2} \, dx
$$

这里的方括号 $S[y]$ 强调其输入是一个函数 $y(x)$。[变分法](@entry_id:163656)的核心问题就是：在哪一个函数 $y(x)$ 的作用下，泛函 $S[y]$ 取得其极值（极大值或极小值）？

为了找到普通函数 $f(x)$ 的极值点，我们考察其一阶导数 $f'(x)$ 为零的点。类似地，为了找到使泛函 $J[y]$ 取极值的函数 $y_0(x)$，我们需要一种方法来“[微分](@entry_id:158718)”泛函。这个过程是通过**变分 (variation)** 实现的。我们考虑一个在“最优”函数 $y_0(x)$ 基础上的微小扰动或变分。这个变分后的函数可以写作：

$$
y(x, \epsilon) = y_0(x) + \epsilon \eta(x)
$$

其中，$\epsilon$ 是一个很小的实数参数，而 $\eta(x)$ 是一个满足特定边界条件的任意函数，称为**变分函数 (variation function)**。例如，在固定端点的问题中，我们要求 $y(a) = y_a$ 和 $y(b) = y_b$，这意味着变分函数必须满足 $\eta(a) = 0$ 和 $\eta(b) = 0$。

通过这种方式，泛函 $J[y(x, \epsilon)]$ 可以被看作是单变量 $\epsilon$ 的函数。如果 $y_0(x)$ 是一个[极值](@entry_id:145933)函数，那么当 $\epsilon=0$ 时，这个关于 $\epsilon$ 的函数必然达到极值。因此，其一阶导数必须为零：

$$
\frac{d}{d\epsilon} J[y_0 + \epsilon \eta] \bigg|_{\epsilon=0} = 0
$$

这个导数被称为泛函 $J$ 的**一阶变分 (first variation)**，记作 $\delta J$。从更严谨的泛函分析角度看，这一定义对应于**盖托导数 (Gâteaux derivative)** [@problem_id:2691389]。盖托导数是在特定方向 $\eta$ 上的[方向导数](@entry_id:189133)。一个更强的概念是**弗雷歇导数 (Fréchet derivative)**，它要求导数在所有方向上一致收敛。在无限维[函数空间](@entry_id:143478)中，盖托可微不一定意味着弗雷歇可微。然而，对于[变分法](@entry_id:163656)中大多数行为良好的泛函，通过盖托导数足以推导出核心的必要条件。

### [欧拉-拉格朗日方程](@entry_id:137827)：[一阶必要条件](@entry_id:170730)

“一阶变分为零”是所有[变分问题](@entry_id:756445)的出发点。通过对这一条件进行分析，我们可以推导出描述极值函数所必须满足的[微分方程](@entry_id:264184)，即[欧拉-拉格朗日方程](@entry_id:137827)。

#### 标量单变量情形的推导

考虑最常见的一类泛函：
$$
J[y] = \int_{a}^{b} L(x, y(x), y'(x)) \, dx
$$
其中 $L$ 被称为**[拉格朗日量](@entry_id:174593) (Lagrangian)**。我们寻找一个函数 $y(x)$，它满足固定的边界条件 $y(a)=y_a$ 和 $y(b)=y_b$，并使 $J[y]$ 取得[极值](@entry_id:145933)。

根据一阶变分为零的原则：
$$
\delta J = \frac{d}{d\epsilon} \int_{a}^{b} L(x, y + \epsilon \eta, y' + \epsilon \eta') \, dx \bigg|_{\epsilon=0} = 0
$$
在积分号下使用[微分](@entry_id:158718)，并利用[链式法则](@entry_id:190743)，我们得到：
$$
\int_{a}^{b} \left( \frac{\partial L}{\partial y} \frac{\partial (y+\epsilon\eta)}{\partial \epsilon} + \frac{\partial L}{\partial y'} \frac{\partial (y'+\epsilon\eta')}{\partial \epsilon} \right) \bigg|_{\epsilon=0} \, dx = \int_{a}^{b} \left( \frac{\partial L}{\partial y} \eta(x) + \frac{\partial L}{\partial y'} \eta'(x) \right) \, dx = 0
$$
为了消除 $\eta'(x)$，我们对第二项使用**分部积分法 (integration by parts)**：
$$
\int_{a}^{b} \frac{\partial L}{\partial y'} \eta'(x) \, dx = \left[ \frac{\partial L}{\partial y'} \eta(x) \right]_{a}^{b} - \int_{a}^{b} \frac{d}{dx} \left( \frac{\partial L}{\partial y'} \right) \eta(x) \, dx
$$
由于端点是固定的，变分函数必须满足 $\eta(a) = \eta(b) = 0$，因此边界项 $\left[ \frac{\partial L}{\partial y'} \eta(x) \right]_{a}^{b}$ 为零。将[分部积分](@entry_id:136350)的结果代回原式，[并合](@entry_id:147963)并积分项，我们得到：
$$
\int_{a}^{b} \left( \frac{\partial L}{\partial y} - \frac{d}{dx} \left( \frac{\partial L}{\partial y'} \right) \right) \eta(x) \, dx = 0
$$
此等式必须对**所有**满足边界条件的任意函数 $\eta(x)$ 都成立。根据**变分法基本引理 (Fundamental Lemma of Calculus of Variations)**，如果一个[连续函数](@entry_id:137361)与任意一个在边界为零的光滑函数的乘积的积分始终为零，那么这个[连续函数](@entry_id:137361)自身必然恒等于零。因此，括号内的表达式必须为零：

$$
\frac{\partial L}{\partial y} - \frac{d}{dx} \left( \frac{\partial L}{\partial y'} \right) = 0
$$

这就是著名的**欧拉-拉格朗日方程 (Euler-Lagrange equation)**。它是一个[二阶常微分方程](@entry_id:204212)（通常是[非线性](@entry_id:637147)的），其解（称为**极值曲线 (extremal)**）是使泛函取得平稳值（可能是极大值、极小值或[鞍点](@entry_id:142576)）的候选函数。

#### 应用：[最短路径问题](@entry_id:273176)

欧拉-拉格朗日方程的应用极为广泛。让我们考虑一个寻找柱面上的最短路径（即**[测地线](@entry_id:269969) (geodesic)**）的问题 [@problem_id:1268]。假设一个半径为 $R$ 的无限长圆柱面，在[柱坐标系](@entry_id:266798) $(\rho, \phi, z)$ 下，其[弧长](@entry_id:191173)微元为 $ds^2 = d\rho^2 + \rho^2 d\phi^2 + dz^2$。在柱面上，$\rho=R$ 且 $d\rho=0$，因此 $ds = \sqrt{R^2 d\phi^2 + dz^2}$。

如果我们用角度 $\phi$ 来[参数化](@entry_id:272587)路径，即 $z=z(\phi)$，那么 $dz = \frac{dz}{d\phi} d\phi = z' d\phi$。总[弧长泛函](@entry_id:265800)为：
$$
S[z] = \int_{\phi_1}^{\phi_2} \sqrt{R^2 + (z')^2} \, d\phi
$$
这里的拉格朗日量是 $L(z, z') = \sqrt{R^2 + (z')^2}$。注意到 $L$ 并不显式地依赖于 $z$，即 $\frac{\partial L}{\partial z} = 0$。欧拉-拉格朗日方程简化为：
$$
-\frac{d}{d\phi} \left( \frac{\partial L}{\partial z'} \right) = 0 \quad \implies \quad \frac{\partial L}{\partial z'} = \text{constant}
$$
这个结论非常重要：如果拉格朗日量不显式依赖于某个变量（如 $z$），那么它对该变量导数（$z'$）的[偏导数](@entry_id:146280)是一个守恒量。计算这个偏导数：
$$
\frac{\partial L}{\partial z'} = \frac{z'}{\sqrt{R^2 + (z')^2}} = C \quad (\text{常数})
$$
解出 $z'$，我们发现 $z' = \frac{dz}{d\phi}$ 必须是一个常数。这意味着柱面上的[最短路径](@entry_id:157568)是一条螺旋线，其轴向位置 $z$ 随角度 $\phi$ 线性变化。将边界条件 $z(\phi_1)=z_1$ 和 $z(\phi_2)=z_2$ 代入，即可确定这个常数：$\frac{dz}{d\phi} = \frac{z_2 - z_1}{\phi_2 - \phi_1}$。

#### 边界条件

在推导[欧拉-拉格朗日方程](@entry_id:137827)时，我们利用了固定端点使得 $\eta(a)=\eta(b)=0$ 这一事实。如果某个端点是自由的，情况会如何？例如，在控制理论中，我们可能只固定初始状态，而终端状态是自由的 [@problem_id:2691388]。

让我们重新审视分部积分产生的边界项：$\left[ \frac{\partial L}{\partial y'} \eta(x) \right]_{a}^{b}$。如果初始点 $y(a)$ 固定，而终点 $y(b)$ 自由，则变分函数需满足 $\eta(a)=0$，但 $\eta(b)$ 是任意的。此时，一阶变分的完整表达式为：
$$
\delta J = \int_{a}^{b} \left( \frac{\partial L}{\partial y} - \frac{d}{dx} \left( \frac{\partial L}{\partial y'} \right) \right) \eta(x) \, dx + \frac{\partial L}{\partial y'}\bigg|_{x=b} \eta(b) = 0
$$
首先，我们可以选取所有在 $b$ 点也为零的变分函数（即 $\eta(b)=0$）。对于这部分变分，方程退化为我们之前见过的形式，从而我们依然可以得出[欧拉-拉格朗日方程](@entry_id:137827)必须在区间 $(a,b)$ 内成立。

既然欧拉-拉格朗日方程成立，那么积分项对于任何 $\eta(x)$（包括那些在 $b$ 点不为零的）都恒为零。因此，上述方程简化为：
$$
\frac{\partial L}{\partial y'}\bigg|_{x=b} \eta(b) = 0
$$
由于 $\eta(b)$ 是任意的，为了使此式成立，其系数必须为零。这就给出了在自由端点处必须满足的**自然边界条件 (natural boundary condition)**：

$$
\frac{\partial L}{\partial y'}\bigg|_{x=b} = 0
$$

这个条件不是人为施加的，而是从变分原理中自然产生的。例如，对于问题 [@problem_id:2691388] 中给出的二次型[拉格朗日量](@entry_id:174593) $L = \frac{1}{2}y'^T R y' + y'^T S y + \dots$，其关于 $y'$ 的梯度为 $\nabla_{y'} L = R(t) y'(t) + S(t) y(t) + r(t)$。如果终点 $y(b)$ 自由，那么最优轨迹必须在终点满足 $R(b) y'(b) + S(b) y(b) + r(b) = 0$。

### 守恒律与对称性

在物理学和工程学中，守恒律（如[能量守恒](@entry_id:140514)、[动量守恒](@entry_id:149964)）是基本原则。变分法通过[诺特定理](@entry_id:145690)为这些守恒律提供了深刻的数学基础，揭示了它们与系统对称性之间的内在联系。

#### [自治系统](@entry_id:173841)与贝尔特拉米等式

一类重要的系统是**[自治系统](@entry_id:173841) (autonomous systems)**，其[拉格朗日量](@entry_id:174593) $L(y, y')$ 不显式地依赖于自变量 $x$（在力学中通常是时间 $t$），即 $\frac{\partial L}{\partial x} = 0$。在这种情况下，存在一个守恒量。为了找到它，我们计算 $L$ 沿着一条轨迹对 $x$ 的[全导数](@entry_id:137587)：

$$
\frac{dL}{dx} = \frac{\partial L}{\partial x} + \frac{\partial L}{\partial y} y' + \frac{\partial L}{\partial y'} y''
$$
由于系统是自治的，$\frac{\partial L}{\partial x} = 0$。如果这条轨迹是一条极值曲线，它必须满足[欧拉-拉格朗日方程](@entry_id:137827) $\frac{\partial L}{\partial y} = \frac{d}{dx}(\frac{\partial L}{\partial y'})$。代入上式：
$$
\frac{dL}{dx} = \left( \frac{d}{dx} \frac{\partial L}{\partial y'} \right) y' + \frac{\partial L}{\partial y'} y''
$$
根据乘法法则，右边恰好是 $\frac{d}{dx} \left( y' \frac{\partial L}{\partial y'} \right)$。因此，我们有 $\frac{dL}{dx} = \frac{d}{dx} \left( y' \frac{\partial L}{\partial y'} \right)$，移项可得：
$$
\frac{d}{dx} \left( y' \frac{\partial L}{\partial y'} - L \right) = 0
$$
这意味着括号内的量是一个与 $x$ 无关的常数。这个守恒量被称为**[贝尔特拉米恒等式](@entry_id:178954) (Beltrami Identity)** 或[能量积分](@entry_id:166228)。

$$
H = y' \frac{\partial L}{\partial y'} - L = \text{constant}
$$

考虑一个经典的力学系统，其拉格朗日量为动能减[势能](@entry_id:748988)的形式。但在[变分问题](@entry_id:756445)中，我们常常遇到如 [@problem_id:2691392] 的形式 $L = \frac{1}{2}(y')^2 + V(y)$。应用贝尔特拉米等式，其中 $\frac{\partial L}{\partial y'} = y'$，我们得到守恒量为：
$$
y'(y') - \left(\frac{1}{2}(y')^2 + V(y)\right) = \frac{1}{2}(y')^2 - V(y) = \text{constant}
$$
这在物理上对应于系统的总能量（在这个特定的 $L$ 定义下）。

#### [诺特定理](@entry_id:145690)

贝尔特拉米等式是更普适的**诺特定理 (Noether's Theorem)** 的一个特例。[诺特定理](@entry_id:145690)指出：如果一个系统的[拉格朗日量](@entry_id:174593)在某个**连续[对称变换](@entry_id:144406)**下保持不变（或者变化量是一个[全导数](@entry_id:137587)），那么该系统必然存在一个与之对应的守恒量。

[自治系统](@entry_id:173841)的[时间平移不变性](@entry_id:270209)（$x \to x + \epsilon$）就是一种[连续对称性](@entry_id:137257)，它对应着[能量守恒](@entry_id:140514)（由[贝尔特拉米恒等式](@entry_id:178954)给出）。空间[平移不变性](@entry_id:195885)则对应动量守恒，[旋转不变性](@entry_id:137644)对应[角动量守恒](@entry_id:156798)。

考虑一个更微妙的例子：在均匀[磁场中的带电粒子](@entry_id:262149) [@problem_id:404002]。其[拉格朗日量](@entry_id:174593)为 $L = \frac{1}{2} m (\dot{x}^2 + \dot{y}^2) + q B x \dot{y}$（这对应于磁矢量势 $A_y=Bx, A_x=A_z=0$ 的选择）。我们考虑在 $x$ 方向上的空间平移变换：$x \to x' = x + \epsilon$。这是一个连续对称变换，其生成元为 $X_x=1, X_y=0$。在此变换下，[拉格朗日量](@entry_id:174593)的变化为：
$$
\Delta L = L(x+\epsilon, y, \dot{x}, \dot{y}) - L(x, y, \dot{x}, \dot{y}) = q B (x+\epsilon) \dot{y} - q B x \dot{y} = q B \dot{y} \epsilon
$$
这个变化量是一个关于时间的[全导数](@entry_id:137587)：$\Delta L = \epsilon \frac{d}{dt}(q B y)$。根据诺特定理，如果对于变换 $q_i \to q_i + \epsilon X_i$，[拉格朗日量](@entry_id:174593)的变化为 $\Delta L = \epsilon \frac{dF}{dt}$，那么[守恒量](@entry_id:150267)为 $I = \sum_i p_i X_i - F$，其中 $p_i = \frac{\partial L}{\partial \dot{q}_i}$ 是[正则动量](@entry_id:155151)。

在本例中，$X_x=1, X_y=0$，并且 $F=qBy$。$x$ 方向的[正则动量](@entry_id:155151)为 $p_x = \frac{\partial L}{\partial \dot{x}} = m\dot{x}$。因此，守恒量为：
$$
I = p_x X_x - F = (m\dot{x}) \cdot 1 - qBy = m\dot{x} - qBy
$$
这个守恒量是沿 $x$ 方向的[正则动量](@entry_id:155151)，它在物理上不同于[机械动量](@entry_id:156068) $m\dot{x}$。这个例子清晰地展示了诺特定理如何揭示更深层次的守恒律。

### [欧拉-拉格朗日方程](@entry_id:137827)的推广

基本的[欧拉-拉格朗日方程](@entry_id:137827)可以向多个维度和更高阶的导数推广，使其能够处理更广泛和复杂的问题。

#### 多个[自变量](@entry_id:267118)：[偏微分方程](@entry_id:141332)

当研究对象是一个场（如温度场、[电磁场](@entry_id:265881)）时，它依赖于多个自变量，例如空间坐标 $(x, y, z)$。此时，泛函的形式为 $J[u] = \int_{\Omega} L(x, u, \nabla u) \, d^nx$，其中 $x \in \mathbb{R}^n$，$u(x)$ 是一个标量场，$\nabla u$ 是其梯度。

通过与单变量情况完全平行的推导（使用高维的[分部积分](@entry_id:136350)，即[散度定理](@entry_id:143110)），可以得到多变量的[欧拉-拉格朗日方程](@entry_id:137827)，这是一个**[偏微分方程](@entry_id:141332) (PDE)** [@problem_id:2691373]：

$$
\frac{\partial L}{\partial u} - \nabla \cdot \left( \frac{\partial L}{\partial \nabla u} \right) = 0
$$

其中 $\frac{\partial L}{\partial \nabla u}$ 是一个向量，其分量为 $\frac{\partial L}{\partial u_{x_i}}$，而 $\nabla \cdot$ 是[散度算子](@entry_id:265975)。例如，对于拉格朗日量 $L = \frac{1}{2}a |\nabla u|^2 - f u$，其[欧拉-拉格朗日方程](@entry_id:137827)为 $-a \Delta u - f = 0$，即**[泊松方程](@entry_id:143763) (Poisson's equation)**，这是静电学和热传导中的基本方程。

#### 多个因变量：向量情形

当系统由多个[状态变量](@entry_id:138790)描述时，例如一个多自由度的机器人手臂，其状态可以由一个向量 $y(x) = (y_1(x), \dots, y_n(x))^{\top}$ 描述。[拉格朗日量](@entry_id:174593) $L(x, y, y')$ 依赖于这个向量及其导数。

此时，对每个分量 $y_i$ 进行独立的变分，可以得到一个[欧拉-拉格朗日方程组](@entry_id:159532) [@problem_id:2691388]：
$$
\frac{\partial L}{\partial y_i} - \frac{d}{dx} \left( \frac{\partial L}{\partial y'_i} \right) = 0, \quad \text{for } i = 1, \dots, n
$$
这可以更紧凑地写成向量形式：
$$
\frac{\partial L}{\partial y} - \frac{d}{dx} \left( \frac{\partial L}{\partial y'} \right) = \mathbf{0}
$$
其中 $\frac{\partial L}{\partial y}$ 和 $\frac{\partial L}{\partial y'}$ 是梯度向量。

#### [高阶导数](@entry_id:140882)：[欧拉-泊松方程](@entry_id:749105)

在某些问题中，如弹性梁的弯曲，泛函可能依赖于更高阶的导数，例如 $J[y] = \int_a^b L(x, y, y', y'') \, dx$。推导其必要条件需要进行多次分部积分 [@problem_id:2691356]。对于一个依赖于直到 $k$ 阶导数的泛函 $J[y] = \int_a^b L(x, y, y', \dots, y^{(k)}) \, dx$，其[极值](@entry_id:145933)曲线必须满足**[欧拉-泊松方程](@entry_id:749105) (Euler-Poisson equation)**：

$$
\frac{\partial L}{\partial y^{(0)}} - \frac{d}{dx}\left(\frac{\partial L}{\partial y^{(1)}}\right) + \frac{d^2}{dx^2}\left(\frac{\partial L}{\partial y^{(2)}}\right) - \dots + (-1)^k \frac{d^k}{dx^k}\left(\frac{\partial L}{\partial y^{(k)}}\right) = 0
$$
或者写为求和形式：
$$
\sum_{j=0}^{k} (-1)^j \frac{d^j}{dx^j} \left( \frac{\partial L}{\partial y^{(j)}} \right) = 0
$$
其中 $y^{(j)}$ 是 $y$ 的 $j$ 阶导数。

#### [等周问题](@entry_id:190109)与[拉格朗日乘子](@entry_id:142696)

另一类重要的推广是带有积分约束的[变分问题](@entry_id:756445)，称为**[等周问题](@entry_id:190109) (isoperimetric problems)**。例如，在所有周长为定值的封闭曲线中，哪一条围成的面积最大？

这类问题的一般形式是：求泛函 $J[y] = \int L \, dx$ 的极值，同时满足约束条件 $K[y] = \int G \, dx = c$（常数）。解决方法是引入一个**[拉格朗日乘子](@entry_id:142696) (Lagrange multiplier)** $\lambda$，构造一个新的[增广拉格朗日量](@entry_id:177042) $\bar{L} = L + \lambda G$。然后，寻找使增广泛函 $\bar{J}[y] = \int \bar{L} \, dx$ 取[极值](@entry_id:145933)的函数 $y(x)$。该函数必须满足对应于 $\bar{L}$ 的[欧拉-拉格朗日方程](@entry_id:137827) [@problem_id:2691358]：

$$
\frac{\partial (L+\lambda G)}{\partial y} - \frac{d}{dx} \left( \frac{\partial (L+\lambda G)}{\partial y'} \right) = 0
$$
解这个方程会得到一个依赖于 $\lambda$ 的解族，而常数 $\lambda$ 的值最终由积分约束 $K[y]=c$ 来确定。

### 现代观点与[二阶条件](@entry_id:635610)

欧拉-拉格朗日方程提供了寻找极值点的“[一阶必要条件](@entry_id:170730)”。现代变分理论在更广阔的函数空间中重新审视了这些概念，并发展了用于判断极值类型的[二阶条件](@entry_id:635610)。

#### 弱形式与索博列夫空间

经典的[变分法](@entry_id:163656)通常假设解函数具有足够的平滑性（例如二阶连续可微）。然而，许多实际问题的解可能不那么光滑，例如可能存在[尖点](@entry_id:636792)。现代方法将[变分问题](@entry_id:756445)置于**[索博列夫空间](@entry_id:141995) (Sobolev spaces)**（如 $H^1$）中来处理，这些空间允许函数及其“弱”导数是平方可积的。

在这种框架下，欧拉-拉格朗日方程被理解为其**弱形式 (weak form)**。例如，在问题 [@problem_id:2691357] 中，一个函数的弗雷歇导数 $DJ(u)[v]$ 是一个作用于变分函数 $v$ 的线性泛函。根据[里斯表示定理](@entry_id:140012)，在希尔伯特空间（如 $H^1$）中，这个线性泛函可以由与某个特定元素 $g = \nabla_{H^1}J(u)$ 的[内积](@entry_id:158127)来表示：
$$
DJ(u)[v] = \langle g, v \rangle_{H^1}
$$
这个元素 $g$ 被称为泛函 $J$ 在 $u$ 点的**梯度**。极值条件 $DJ(u)[v]=0$ 就等价于梯度 $g$ 为零。将 $g=0$ 转化为其对应的强形式（即[微分方程](@entry_id:264184)），我们就能重新得到[欧拉-拉格朗日方程](@entry_id:137827)。这种观点为数值方法（如[有限元法](@entry_id:749389)）和非光滑解的研究提供了坚实的理论基础。

#### 二阶变分与勒让德条件

[欧拉-拉格朗日方程](@entry_id:137827)只是一个必要条件，它找到的是平稳点，而无法区分是极大值、极小值还是[鞍点](@entry_id:142576)。为此，我们需要考察**二阶变分 (second variation)** $\delta^2 J$。对于一个（弱）[局部极小值](@entry_id:143537)点，必须有 $\delta^2 J \ge 0$。

二阶变分的表达式为：
$$
\delta^2 J[\eta] = \int_{a}^{b} \left[ L_{yy}\eta^2 + 2L_{yy'}\eta\eta' + L_{y'y'}(\eta')^2 \right] dx
$$
其中所有[二阶偏导数](@entry_id:635213)均在极值曲线上取值。为了确保 $\delta^2 J \ge 0$ 对所有 $\eta$ 成立，我们可以通过构造一类在小区间内剧烈[振荡](@entry_id:267781)的变分函数 $\eta$ 来进行分析。对于这类函数，$(\eta')^2$ 项将占主导地位。为了使积分非负，其系数必须非负。这导出了**勒让德必要条件 (Legendre necessary condition)** [@problem_id:2691410]：

$$
L_{y'y'}(x, y(x), y'(x)) \ge 0
$$
对于一个极小值，该条件必须在整个区间 $[a,b]$ 上成立。对于向量值问题 $y \in \mathbb{R}^n$，该条件推广为 $L$ 关于 $y'$ 的海森矩阵 $L_{y'y'}$ 必须是半正定的。

值得注意的是，勒让德条件本身并不足以保证一个极小值。即使是其严格形式 $L_{y'y'} > c > 0$，也需要结合另一个条件——**[雅可比](@entry_id:264467)条件 (Jacobi condition)**（要求区间内不存在[共轭点](@entry_id:160335)），才能共同构成（弱）局部极小值的充分条件。勒让德条件在[最优控制理论](@entry_id:139992)中也以**勒让德-克莱布施条件 (Legendre-Clebsch condition)** 的形式出现，它与[庞特里亚金极大值原理](@entry_id:269943)中的[哈密顿量](@entry_id:172864)[二阶导数](@entry_id:144508)条件直接相关。

本章系统地建立了变分法的基本框架。从简单的[弧长](@entry_id:191173)问题出发，我们推导了核心的[欧拉-拉格朗日方程](@entry_id:137827)，探讨了其与守恒律的深刻联系，并将其推广到处理多变量、[高阶导数](@entry_id:140882)和积分约束的复杂情况。最后，我们简要介绍了现代泛函分析观点和用于判断[极值](@entry_id:145933)类型的[二阶条件](@entry_id:635610)。这些原理与机制共同构成了解决各类[优化问题](@entry_id:266749)的强大理论基础。