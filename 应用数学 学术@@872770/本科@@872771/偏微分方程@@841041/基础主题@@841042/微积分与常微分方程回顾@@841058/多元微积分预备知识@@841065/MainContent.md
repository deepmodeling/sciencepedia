## 引言
多元微积分是理解和描述自然现象的通用语言，而[偏微分方程](@entry_id:141332)（PDEs）则是运用这门语言写成的壮丽诗篇，捕捉从热量[扩散](@entry_id:141445)到[波的传播](@entry_id:144063)等万千变化。然而，许多学习者在掌握微积分的计算技巧后，仍难以体会其在构建物理模型和解决实际问题中的深刻意义。本文旨在填补这一鸿沟，系统性地展示多元微积分如何成为研究[偏微分方程](@entry_id:141332)不可或缺的基石。

在接下来的内容中，读者将踏上一段从基础到应用的旅程。我们将首先在“原理与机制”一章中，深入剖析[梯度、散度、旋度](@entry_id:269893)等核心微分算子和[积分定理](@entry_id:183680)，揭示它们如何精确描述物理量的时空变化。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章，我们将跨越物理、工程乃至生命科学的界限，展示这些数学原理在解决真实世界问题中的强大威力。最后，通过“动手实践”部分，你将有机会巩固所学，将理论知识转化为解决问题的实际能力。

让我们从构建这门科学语言的基础——多元微积分的核心原理与机制开始。

## 原理与机制

[偏微分方程](@entry_id:141332)（PDEs）是描述自然界和工程领域中各种物理现象的基本数学语言，从热量传导、[流体运动](@entry_id:182721)到电磁波的传播。为了流利地使用这门语言，我们必须首先掌握其语法和词汇——这正是多元微积分提供给我们的工具。本章将系统地介绍研究[偏微分方程](@entry_id:141332)所需的核心微积分原理和机制，重点关注[微分算子](@entry_id:140145)（如梯度、[散度和旋度](@entry_id:270881)）以及它们在积分理论中的应用。我们将通过一系列物理情境，揭示这些数学概念如何精确地捕捉和描述时空变化的系统。

### [标量场](@entry_id:151443)的描述：[偏导数](@entry_id:146280)、梯度与方向导数

在物理学中，许多量（如温度、压力或浓度）在空间和时间上是变化的，可以用一个**[标量场](@entry_id:151443)**来表示，即一个将时空中的每一点映射到一个标量值的函数，例如 $u(x, y, z, t)$。理解这些场如何变化是分析物理系统的第一步。

最基本的工具是**[偏导数](@entry_id:146280)**。偏导数测量的是当所有其他变量保持不变时，函数沿某一特定坐标轴的变化率。例如，对于一个温度场 $u(x, t)$，偏导数 $\frac{\partial u}{\partial t}$ 表示在空间中一个[固定点](@entry_id:156394) $x$ 处温度随时间的变化速率。

考虑一个长度为 $L$ 的细杆，其温度[分布](@entry_id:182848)由函数 $u(x,t) = T_{amb} + T_{max} \sin(\frac{\pi x}{L}) \exp(-\alpha t)$ 描述，其中 $T_{amb}$ 是环境温度，$T_{max}$ 是初始温度振幅，$\alpha$ 是热衰减常数 [@problem_id:2120127]。要计算在杆上任意位置 $x$ 和任意时刻 $t$ 的瞬时冷却速率，我们需求解 $u$ 对 $t$ 的[偏导数](@entry_id:146280)：
$$ \frac{\partial u}{\partial t} = \frac{\partial}{\partial t} \left[ T_{amb} + T_{max} \sin\left(\frac{\pi x}{L}\right) \exp(-\alpha t) \right] $$
由于 $T_{amb}$、$T_{max}$、$\sin(\frac{\pi x}{L})$ 在对 $t$ 求导时均被视为常数，我们得到：
$$ \frac{\partial u}{\partial t} = T_{max} \sin\left(\frac{\pi x}{L}\right) \cdot (-\alpha \exp(-\alpha t)) = -\alpha T_{max} \sin\left(\frac{\pi x}{L}\right) \exp(-\alpha t) $$
这个结果告诉我们，在杆的正弦温度[分布区](@entry_id:204061)域（$\sin(\frac{\pi x}{L}) > 0$），温度总是在下降（因为导数为负），其下降的速率不仅取决于时间（通过 $\exp(-\alpha t)$ 项），还取决于空间位置（通过 $\sin(\frac{\pi x}{L})$ 项）。

然而，[物理变化](@entry_id:136242)并非总是沿着坐标轴发生。为了描述空间中任意方向的变化率，我们引入**梯度（gradient）**。对于一个三维[标量场](@entry_id:151443) $f(x, y, z)$，其梯度是一个矢量场，定义为：
$$ \nabla f = \frac{\partial f}{\partial x} \mathbf{i} + \frac{\partial f}{\partial y} \mathbf{j} + \frac{\partial f}{\partial z} \mathbf{k} $$
其中 $\nabla = \mathbf{i} \frac{\partial}{\partial x} + \mathbf{j} \frac{\partial}{\partial y} + \mathbf{k} \frac{\partial}{\partial z}$ 是一个向量微分算子，称为**del算子**。[梯度向量](@entry_id:141180) $\nabla f$ 指向函数 $f$ 在该点增长最快的方向，其大小 $| \nabla f |$ 等于这个最大变化率。

一旦我们有了梯度，就可以计算任何方向上的变化率。**方向导数** $D_{\mathbf{u}}f$ 描述了函数 $f$ 在一个特定[单位向量](@entry_id:165907) $\mathbf{u}$ 方向上的变化率，它通过梯度和方向向量的[点积](@entry_id:149019)计算：
$$ D_{\mathbf{u}}f = \nabla f \cdot \mathbf{u} $$
这个公式直观地表示：任意方向的变化率是“最快变化率”在该方向上的投影。

设想一个环境监测无人机正在测量由地面源释放的污染物浓度 [@problem_id:2120115]。浓度场由高斯函数 $C(x, y, z) = 500 \exp\left(-\frac{x^2 + y^2}{(100)^2} - \frac{z^2}{(50)^2}\right)$ 给出。如果无人机在点 $P(100, 0, 50)$，并希望测量方向 $\mathbf{v} = \langle 1, 1, -1 \rangle$ 上的浓度瞬时空间变化率，我们首先需要计算浓度场在该点的梯度 $\nabla C(P)$。
各分量偏导数为：
$$ \frac{\partial C}{\partial x} = C(x,y,z) \left(-\frac{2x}{100^2}\right), \quad \frac{\partial C}{\partial y} = C(x,y,z) \left(-\frac{2y}{100^2}\right), \quad \frac{\partial C}{\partial z} = C(x,y,z) \left(-\frac{2z}{50^2}\right) $$
在点 $P(100, 0, 50)$，我们得到[梯度向量](@entry_id:141180) $\nabla C(P) = \langle -10 e^{-2}, 0, -20 e^{-2} \rangle$。接着，我们将方向向量 $\mathbf{v}$ 单位化得到 $\mathbf{u} = \frac{\mathbf{v}}{|\mathbf{v}|} = \frac{1}{\sqrt{3}}\langle 1, 1, -1 \rangle$。最后，方向导数为：
$$ D_{\mathbf{u}}C(P) = \nabla C(P) \cdot \mathbf{u} = \langle -10 e^{-2}, 0, -20 e^{-2} \rangle \cdot \frac{1}{\sqrt{3}}\langle 1, 1, -1 \rangle = \frac{10 e^{-2}}{\sqrt{3}} $$
这个正值表示，如果无人机朝向 $\mathbf{v}$ 方向移动，它将立即测量到浓度在增加。

当一个物体在场中运动时，它所经历的场值的**[全导数](@entry_id:137587)（total derivative）** $\frac{df}{dt}$ 可以通过**[多元链式法则](@entry_id:635606)**计算。如果物体轨迹由 $x(t), y(t), z(t)$ 给出，那么：
$$ \frac{df}{dt} = \frac{\partial f}{\partial x}\frac{dx}{dt} + \frac{\partial f}{\partial y}\frac{dy}{dt} + \frac{\partial f}{\partial z}\frac{dz}{dt} = \nabla f \cdot \mathbf{v} $$
其中 $\mathbf{v} = \langle \frac{dx}{dt}, \frac{dy}{dt}, \frac{dz}{dt} \rangle$ 是物体的速度。这个重要的关系表明，物体经历的变化率是场梯度与物体速度的[点积](@entry_id:149019)。

考虑一架无人机在压[力场](@entry_id:147325) $P(x, y) = P_c - \alpha x^2 - \beta y^2$ 中沿轨迹 $x(t) = A \cos(\omega t)$，$y(t) = B \sin(2\omega t)$ 飞行 [@problem_id:2120132]。无人机感受到的压力变化率 $\frac{dP}{dt}$ 由[链式法则](@entry_id:190743)给出：
$$ \frac{dP}{dt} = \frac{\partial P}{\partial x} \frac{dx}{dt} + \frac{\partial P}{\partial y} \frac{dy}{dt} $$
计算各个导数：$\frac{\partial P}{\partial x} = -2\alpha x$, $\frac{\partial P}{\partial y} = -2\beta y$, $\frac{dx}{dt} = -A\omega \sin(\omega t)$, $\frac{dy}{dt} = 2B\omega \cos(2\omega t)$。代入并用 $x(t)$ 和 $y(t)$ 替换 $x$ 和 $y$，我们得到：
$$ \frac{dP}{dt} = (-2\alpha (A \cos(\omega t)))(-A\omega \sin(\omega t)) + (-2\beta (B \sin(2\omega t)))(2B\omega \cos(2\omega t)) $$
利用[三角恒等式](@entry_id:165065) $\sin(2\theta) = 2\sin(\theta)\cos(\theta)$，上式可以简化为：
$$ \frac{dP}{dt} = \alpha A^2 \omega \sin(2\omega t) - 2\beta B^2 \omega \sin(4\omega t) $$
这个表达式完全描述了无人机在其复杂路径上所经历的压力随时间的变化。

### 矢量场的特征：散度与旋度

物理世界中同样充满了**矢量场**，例如流体的[速度场](@entry_id:271461)或[电磁场](@entry_id:265881)，它们在每一点都赋予一个矢量（大小和方向）。为了描述矢量场的局部行为，我们需要另外两个关键的[微分算子](@entry_id:140145)：[散度和旋度](@entry_id:270881)。

**散度（divergence）** 测量的是一个矢量场在某一点的“源”或“汇”的强度。对于一个矢量场 $\mathbf{F} = \langle P, Q, R \rangle$，其散度是一个标量，定义为：
$$ \nabla \cdot \mathbf{F} = \frac{\partial P}{\partial x} + \frac{\partial Q}{\partial y} + \frac{\partial R}{\partial z} $$
在[流体动力学](@entry_id:136788)中，[速度场](@entry_id:271461) $\mathbf{v}$ 的散度表示单位体积流体膨胀或收缩的速率。如果 $\nabla \cdot \mathbf{v} > 0$，该点就像一个源头，流体从这里流出；如果 $\nabla \cdot \mathbf{v} < 0$，该点就像一个汇点，流体向这里汇集。如果对于整个流场 $\nabla \cdot \mathbf{v} = 0$，则称该流体是**不可压缩的**，这意味着任何流体微元的体积在运动时保持不变。

为了判断一个给定的流速场是否代表不可压缩流体，我们只需计算其散度 [@problem_id:2120155]。例如，考虑速度场 $\mathbf{v} = \langle x^2y, y^2z, -2xyz - yz^2 \rangle$。其散度为：
$$ \nabla \cdot \mathbf{v} = \frac{\partial}{\partial x}(x^2y) + \frac{\partial}{\partial y}(y^2z) + \frac{\partial}{\partial z}(-2xyz - yz^2) $$
$$ \nabla \cdot \mathbf{v} = (2xy) + (2yz) + (-2xy - 2yz) = 0 $$
由于散度处处为零，该[速度场](@entry_id:271461)描述的是一个不可压缩的[流体流动](@entry_id:201019)。

**旋度（curl）** 测量的是一个矢量场在某一点的局部旋转趋势。矢量场 $\mathbf{F}$ 的旋度是一个新的矢量场，定义为：
$$ \nabla \times \mathbf{F} = \begin{vmatrix} \mathbf{i}  \mathbf{j}  \mathbf{k} \\ \frac{\partial}{\partial x}  \frac{\partial}{\partial y}  \frac{\partial}{\partial z} \\ P  Q  R \end{vmatrix} = \left(\frac{\partial R}{\partial y} - \frac{\partial Q}{\partial z}\right)\mathbf{i} - \left(\frac{\partial R}{\partial x} - \frac{\partial P}{\partial z}\right)\mathbf{j} + \left(\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y}\right)\mathbf{k} $$
在[流体动力学](@entry_id:136788)中，速度场 $\mathbf{v}$ 的旋度被称为**涡度（vorticity）**，记为 $\mathbf{\Omega} = \nabla \times \mathbf{v}$。涡度向量的方向是流体微元[旋转轴](@entry_id:187094)的方向（遵循[右手定则](@entry_id:156766)），其大小是旋转角速度的两倍。如果一个场的旋度处处为零，则称该场为**[无旋场](@entry_id:183486)（irrotational field）**。

考虑一个简化的[海洋环流](@entry_id:180204)模型，其[速度场](@entry_id:271461)由 $\mathbf{V}(x, y, z) = -\omega y \mathbf{i} + \omega x \mathbf{j} + U_0 \mathbf{k}$ 给出，其中 $\omega$ 代表旋[转角频率](@entry_id:264901) [@problem_id:2120125]。该流场的涡度为：
$$ \mathbf{\Omega} = \nabla \times \mathbf{V} = \left( \frac{\partial (U_0)}{\partial y} - \frac{\partial (\omega x)}{\partial z} \right) \mathbf{i} - \left( \frac{\partial (U_0)}{\partial x} - \frac{\partial (-\omega y)}{\partial z} \right) \mathbf{j} + \left( \frac{\partial (\omega x)}{\partial x} - \frac{\partial (-\omega y)}{\partial y} \right) \mathbf{k} $$
计算各个偏导数：
$$ \mathbf{\Omega} = (0 - 0)\mathbf{i} - (0 - 0)\mathbf{j} + (\omega - (-\omega))\mathbf{k} = 2\omega \mathbf{k} $$
这个结果表明，流体在每一点都具有一个恒定的、沿 $z$ 轴正方向的涡度。这意味着整个流体像一个刚体一样绕着垂直轴旋转，其旋转速率是 $\omega$。

### [微分算子](@entry_id:140145)与[偏微分方程](@entry_id:141332)

[偏微分方程](@entry_id:141332)本质上就是用[微分算子](@entry_id:140145)写成的关于未知函数的方程。梯度、[散度和旋度](@entry_id:270881)，以及由它们组合而成的[高阶算子](@entry_id:750304)，构成了描述物理定律的基石。

一个至关重要的二阶算子是**[拉普拉斯算子](@entry_id:146319)（Laplacian）**，记为 $\nabla^2$ 或 $\Delta$。它定义为[梯度的散度](@entry_id:270716)：
$$ \nabla^2 f = \nabla \cdot (\nabla f) = \frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2} + \frac{\partial^2 f}{\partial z^2} $$
[拉普拉斯算子](@entry_id:146319)在物理学中无处不在。例如，在[热传导](@entry_id:147831)中，$\nabla^2 u$ 与某点温度和其周围平均温度之差成正比，驱动热量从高温区流向低温区。许多基本的PDE，如拉普拉斯方程 $(\nabla^2 u = 0)$、[泊松方程](@entry_id:143763) $(\nabla^2 u = f)$、[热传导方程](@entry_id:194763) $(\frac{\partial u}{\partial t} = \alpha \nabla^2 u)$ 和波动方程 $(\frac{\partial^2 u}{\partial t^2} = c^2 \nabla^2 u)$，都以拉普拉斯算子为核心。

分析PDE的一个核心任务是验证一个给定的函数是否是其解。这需要我们计算函数的所有相关[偏导数](@entry_id:146280)，并将它们代入方程中。例如，考虑一个有阻尼的弦的[振动](@entry_id:267781)，由一维[阻尼波动方程](@entry_id:171138)描述 [@problem_id:2120154]：
$$ \frac{\partial^2 u}{\partial t^2} + 2\beta \frac{\partial u}{\partial t} = v^2 \frac{\partial^2 u}{\partial x^2} $$
假设一个可能的解的形式为[驻波](@entry_id:148648) $u(x, t) = \exp(-\alpha t) \cos(k x)$。为了验证它，我们计算所需的导数：
$$ \frac{\partial u}{\partial t} = -\alpha \exp(-\alpha t) \cos(k x) $$
$$ \frac{\partial^2 u}{\partial t^2} = \alpha^2 \exp(-\alpha t) \cos(k x) $$
$$ \frac{\partial^2 u}{\partial x^2} = -k^2 \exp(-\alpha t) \cos(k x) $$
将这些代入[阻尼波动方程](@entry_id:171138)：
$$ \alpha^2 e^{-\alpha t} \cos(kx) + 2\beta (-\alpha e^{-\alpha t} \cos(kx)) = v^2 (-k^2 e^{-\alpha t} \cos(kx)) $$
消去公因子 $e^{-\alpha t} \cos(kx)$ 后，我们得到一个关于参数的代数方程：
$$ \alpha^2 - 2\beta \alpha = -v^2 k^2 \quad \implies \quad \alpha^2 - 2\beta \alpha + v^2 k^2 = 0 $$
这是一个关于 $\alpha$ 的二次方程，其解为 $\alpha = \beta \pm \sqrt{\beta^2 - v^2 k^2}$。这表明，所提出的函数形式确实可以是方程的解，但前提是其衰减率 $\alpha$ 必须满足这个特定的关系。

更复杂的物理定律通常会组合多个算子。一个典型的例子是物质[守恒定律](@entry_id:269268)。考虑一个密度为 $\rho(x,y,z,t)$、速度为 $\mathbf{v}(x,y,z,t)$ 的流体，并且存在一个源项 $\sigma(x,y,z,t)$ 描述单位体积内质量的生成速率 [@problem_id:2120121]。[质量守恒](@entry_id:204015)原理指出：
$$ \text{（局部密度变化率）} = \text{（源生成率）} - \text{（净流出率）} $$
用数学语言表达，即为**[连续性方程](@entry_id:195013)**：
$$ \frac{\partial \rho}{\partial t} = \sigma - \nabla \cdot (\rho \mathbf{v}) $$
这里的 $\rho \mathbf{v}$ 是质量通量密度（单位时间穿过单位面积的质量），而 $\nabla \cdot (\rho \mathbf{v})$ 是单位体积的净[质量流](@entry_id:143424)出率。这个方程本身就是一个重要的PDE。如果给出 $\rho$ 和 $\mathbf{v}$，我们可以反过来计算所需的源项 $\sigma$。
$$ \sigma = \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) $$
利用矢量恒等式 $\nabla \cdot (f\mathbf{A}) = (\nabla f) \cdot \mathbf{A} + f(\nabla \cdot \mathbf{A})$，我们可以展开第二项：
$$ \sigma = \frac{\partial \rho}{\partial t} + (\nabla \rho) \cdot \mathbf{v} + \rho (\nabla \cdot \mathbf{v}) $$
这个方程完美地展示了时间导数、梯度和散度如何共同描述一个包含源的动态物理过程。

### 积分关系与函数空间

除了[微分](@entry_id:158718)（局部）描述，我们还需要积分（全局）工具。这些工具不仅用于求解PDE，还用于理解解的性质和导出方程本身。

在求解许多PDE时，我们会将解表示为一系列“[基函数](@entry_id:170178)”的叠加，这类似于将一个几何向量分解到坐标轴上。这个思想的基础是**[函数空间](@entry_id:143478)**的概念，其中函数被视为向量。为了衡量函数之间的“对齐”程度，我们定义了**[内积](@entry_id:158127)（inner product）**。对于在区间 $[a, b]$ 上的两个实值函数 $f(x)$ 和 $g(x)$，其标准[内积](@entry_id:158127)定义为：
$$ \langle f, g \rangle = \int_{a}^{b} f(x)g(x)dx $$
如果 $\langle f, g \rangle = 0$，我们称函数 $f$ 和 $g$ 在该区间上是**正交的（orthogonal）**。正交性是傅里叶级数和其它[本征函数展开](@entry_id:177104)法的基石，这些方法是求解PDE的有力武器。

三角函数系 $\{\sin(nx), \cos(mx)\}$ 在区间 $[-\pi, \pi]$ 上构成了一个重要的[正交集](@entry_id:268255)。例如，我们有如下[正交关系](@entry_id:145540)（对于整数 $m, n \ge 1$）：
$$ \int_{-\pi}^{\pi} \sin(nx)\cos(mx)dx = 0 \quad (\text{对所有 } m, n) $$
$$ \int_{-\pi}^{\pi} \cos(nx)\cos(mx)dx = 0 \quad (\text{若 } n \neq m) $$
$$ \int_{-\pi}^{\pi} \sin(nx)\sin(mx)dx = 0 \quad (\text{若 } n \neq m) $$
这些性质极大地简化了[内积](@entry_id:158127)的计算。例如，计算 $f(x) = 3\sin(4x) + 5\cos(6x)$ 和 $g(x) = 2\sin(4x) + 7\cos(8x)$ 在 $[-\pi, \pi]$ 上的[内积](@entry_id:158127) [@problem_id:2120158]：
$$ \langle f, g \rangle = \int_{-\pi}^{\pi} (3\sin(4x) + 5\cos(6x))(2\sin(4x) + 7\cos(8x)) dx $$
展开后，由于正交性，所有[交叉](@entry_id:147634)项的积分（如 $\int \sin(4x)\cos(8x)dx$ 和 $\int \cos(6x)\sin(4x)dx$ 等）都为零。唯一非零的项是：
$$ \langle f, g \rangle = \int_{-\pi}^{\pi} (3\sin(4x))(2\sin(4x)) dx = 6 \int_{-\pi}^{\pi} \sin^2(4x) dx $$
利用积分 $\int_{-\pi}^{\pi} \sin^2(nx)dx = \pi$，我们得到 $\langle f, g \rangle = 6\pi$。

正交性的概念也适用于其他函数族，如勒让德多项式、[贝塞尔函数](@entry_id:265752)等，它们都是特定PDE的解。例如，在区间 $[-1, 1]$ 上，函数 $f(x)=x$ 和 $g(x)=\frac{3}{2}x^2 - \frac{1}{2}$（它们分别是第一和第二阶勒让德多项式）是正交的 [@problem_id:2120119]。它们的[内积](@entry_id:158127)是：
$$ \int_{-1}^{1} x \left(\frac{3}{2}x^2 - \frac{1}{2}\right) dx = \int_{-1}^{1} \left(\frac{3}{2}x^3 - \frac{1}{2}x\right) dx $$
由于被积函数是[奇函数](@entry_id:173259)，在一个对称于原点的区间 $[-1, 1]$ 上的积分为零。

连接[微分](@entry_id:158718)和积分的桥梁是[积分定理](@entry_id:183680)，其中最重要的是**散度定理（Divergence Theorem）**，也称为[高斯定理](@entry_id:143110)。它指出，一个矢量场 $\mathbf{F}$ 穿过一个闭合[曲面](@entry_id:267450) $\partial\Omega$ 的总通量，等于该场在[曲面](@entry_id:267450)所包围的体积 $\Omega$ 内的散度的[体积分](@entry_id:171119)：
$$ \oint_{\partial \Omega} \mathbf{F} \cdot \mathbf{n} \, dS = \int_{\Omega} (\nabla \cdot \mathbf{F}) \, dV $$
其中 $\mathbf{n}$ 是指向外部的[单位法向量](@entry_id:178851)。这个定理的物理意义是：体积内部所有源和汇的总和，等于流出或流入该体积边界的总流量。

散度定理是推导PDE和分析其解的极其强大的工具。例如，它可以用来推导**[格林第一恒等式](@entry_id:170345)（Green's first identity）**。考虑一个积分 $\mathcal{I} = \int_{\Omega} \left( u (\nabla^2 v) + (\nabla u) \cdot (\nabla v) \right) \, dV$ [@problem_id:2120122]。直接计算这个[体积分](@entry_id:171119)可能非常复杂。然而，我们可以注意到被积函数恰好是矢量场 $\mathbf{F} = u \nabla v$ 的散度：
$$ \nabla \cdot (u \nabla v) = (\nabla u) \cdot (\nabla v) + u (\nabla \cdot (\nabla v)) = (\nabla u) \cdot (\nabla v) + u (\nabla^2 v) $$
因此，我们可以应用散度定理将[体积分](@entry_id:171119)转化为[面积分](@entry_id:275394)：
$$ \mathcal{I} = \int_{\Omega} \nabla \cdot (u \nabla v) \, dV = \oint_{\partial \Omega} (u \nabla v) \cdot \mathbf{n} \, dS $$
这个转换通常会使问题大大简化。例如，在一个以原点为中心、半径为 $R$ 的球体内，对于场 $u = \beta \exp(-\frac{r^2}{\sigma^2})$ 和 $v = \alpha r^2$（其中 $r^2=x^2+y^2+z^2$），在球面上 $u$ 是常数 $\beta \exp(-R^2/\sigma^2)$，$\nabla v = 2\alpha \mathbf{r}$，法向量 $\mathbf{n} = \mathbf{r}/R$。于是[面积分](@entry_id:275394)中的被积函数变为：
$$ (u \nabla v) \cdot \mathbf{n} = \left(\beta e^{-R^2/\sigma^2}\right) (2\alpha \mathbf{r}) \cdot \left(\frac{\mathbf{r}}{R}\right) = 2\alpha\beta R e^{-R^2/\sigma^2} $$
这是一个常数，因此积分结果就是这个常数乘以球的表面积 $4\pi R^2$，即 $8\pi \alpha \beta R^3 \exp(-R^2/\sigma^2)$。这个例子展示了散度定理如何将一个复杂的[体积分](@entry_id:171119)问题优雅地转化为一个简单的表[面积分](@entry_id:275394)问题，这在PDE的理论和数值求解中都扮演着核心角色。