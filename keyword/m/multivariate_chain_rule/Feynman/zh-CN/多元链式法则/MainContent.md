## 引言
如果一个量依赖于其他本身也在变化的变量，我们该如何计算这个量的变化率？想象一下，你在艘正在航行的船的甲板上行走；你相对于海岸的速度，既取决于你在船上的速度，也取决于船在水中的速度。这个简单的依赖链就是[链式法则](@keyword=chain_rule|lang=zh-CN|style=Feynman)的精髓。但在一个单一结果可能受到一张错综复杂的关联因素网络影响的世界里，我们需要一个更强大的工具。[多元链式法则](@keyword=multivariable_chain_rule|lang=zh-CN|style=Feynman)正是这样的工具——它是为这个万物互联的世界量身打造的微积分。它为理解变化如何通过复杂系统传播提供了万能钥匙，从[力场](@keyword=force_field|lang=zh-CN|style=Feynman)中粒子的运动到人工智能心智的学习过程。

本文将深入探讨这一基本原理。首先，在“原理与机制”部分，我们将为该法则建立直观认识，探索它如何被用来追踪沿路径的变化，以及如何通过改变[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)来转换我们的数学视角。我们将看到它如何优雅地求解物理方程，并揭示关于波的本质的深刻真理。然后，在“应用与跨学科联系”部分，我们将见证[链式法则](@keyword=chain_rule|lang=zh-CN|style=Feynman)在广阔领域中的实际应用，从物理学和工程学，到其在名为[反向传播](@keyword=backpropagation|lang=zh-CN|style=Feynman)的深度学习[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)核心中所扮演的革命性角色，揭示出它是一条真正普适的互联变化定律。

## 原理与机制

想象你正站在一艘大船的甲板上。你决定从船尾走到船头。你相对于船的速度是，比如说，每小时5公里。但船本身正在以每小时20公里的速度在水中航行。那么，你相对于岸上一个静止的灯塔移动得有多快？如果你朝船头走，你相对于灯塔的速度就是简单的相加：$5 + 20 = 25$ 公里/小时。如果你朝船尾走，那就是 $20 - 5 = 15$ 公里/小时。这个简单的加法就是一维链式法则的核心。你的最终速度是一条*依赖链*的结果：你的位置取决于你在船上的运动，而船的位置又取决于它在水中的运动。

但我们的世界很少像一条直线那么简单。如果一个量，比如房间里的温度，取决于你的位置 $(x, y, z)$ 呢？又如果你的位置因为你在四处走动而随时间变化呢？你*感觉*到的温度变化有多快？这就不再是一个简单的加法了。温度的变化取决于你是朝向一个热炉子还是一个冷窗户移动。它取决于你移动的*方向*。[多元链式法则](@keyword=multivariable_chain_rule|lang=zh-CN|style=Feynman)正是我们理解和计算变化如何通过这些错综复杂的关联变量网络传播的万能钥匙。它是为这个万物互联的世界量身打造的微积分。

### 沿景观路径行进

让我们把直觉变得更精确些。想象你是一个粒子，或许是一架微型无人机，正在一个存在某种[标量场](@keyword=scalar_field|lang=zh-CN|style=Feynman)的空间区域中飞行。这个标量可以是温度、压力或电势。我们可以用一个函数来描述这个量，比如 $z(x, y)$。这个函数定义了一个“景观”——一个表面，其在任意点 $(x, y)$ 的高度由 $z$ 给出。当你的无人机沿着一条路径飞行时，它的坐标 $(x(t), y(t))$ 会随时间 $t$ 变化。我们想回答的问题是：无人机所经历的量 $z$ 随时间的变化率 $\frac{dz}{dt}$ 是多少？

[链式法则](@keyword=chain_rule|lang=zh-CN|style=Feynman)告诉我们，这个总变化率是每个独立运动所贡献变化的总和。这个变化一部分是由于在 $x$ 方向上移动，一部分是由于在 $y$ 方向上移动。来自 $x$ 方向移动的贡献是 $z$ 关于 $x$ 的变化率（即景观在该方向的陡峭程度，$\frac{\partial z}{\partial x}$）乘以你在这个方向上移动的速度（$\frac{dx}{dt}$）。我们为 $y$ 方向加上一个类似的项。于是，这个法则以其优雅的形式呈现出来：

$$
\frac{dz}{dt} = \frac{\partial z}{\partial x} \frac{dx}{dt} + \frac{\partial z}{\partial y} \frac{dy}{dt}
$$

右边的每一项都讲述了一个故事：($z$ 随 $x$ 变化的程度) $\times$ ($x$ 随 $t$ 变化的程度)。我们只需将 $t$ 能够影响 $z$ 的所有路径的贡献加起来。

例如，如果一个粒子沿着由 $x(t) = at^2$ 和 $y(t) = bt^3$ 给出的轨迹，穿过一个标量场 $z(x, y) = \sin(x)\cos(y)$，链式法则使我们能够精确计算出粒子所经历的 $z$ 值在任何瞬间的变化情况 [@problem_id:34728]。这不仅仅是一个抽象的练习；我们就是这样计算一个气象气球在上升并被风吹动时所经历的温度变化，或者一个处于复杂轨道上的卫星其[引力势能](@keyword=gravitational_potential_energy|lang=zh-CN|style=Feynman)的变化。

依赖链甚至可以更长。一个量 $w$ 可能依赖于 $x$ 和 $y$，而 $y$ 又依赖于 $x$，$x$ 本身又依赖于时间 $t$ [@problem_id:34729]。我们可以将此看作一个依赖关系网络。为了找到[全导数](@keyword=total_derivative|lang=zh-CN|style=Feynman) $\frac{dw}{dt}$，我们只需追踪网络中从 $t$到 $w$ 的每一条可能路径，将路径上每一段的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)相乘，然后将所有完整路径的贡献相加。这个系统化的过程正是链式法则如此强大和普适的原因。

### 改变你的视角：变换坐标

链式法则不仅仅用于追踪沿路径的变化。它最深刻的用途之一是改变我们的[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)——即我们描述世界的方式。我们通常用[笛卡尔坐标](@keyword=cartesian_coordinates|lang=zh-CN|style=Feynman) $(x, y)$ 来描述平面上的一个点。但有时，使用[极坐标](@keyword=polar_coordinates|lang=zh-CN|style=Feynman) $(r, \theta)$ 或其他一些自定义[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman) $(s, t)$ 会更方便。如果我们有一个函数 $f(x, y)$，它的变化率（即它的[偏导数](@keyword=partial_derivatives|lang=zh-CN|style=Feynman)）在新的[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)中看起来是怎样的？

假设我们有一个由 $x = x(s, t)$ 和 $y = y(s, t)$ 定义的变换。如果我们稍微扰动新的坐标 $s$，同时保持 $t$ 不变，$f$ 会如何变化？这就是[偏导数](@keyword=partial_derivatives|lang=zh-CN|style=Feynman) $\frac{\partial f}{\partial s}$。扰动 $s$ 会导致 $x$ 和 $y$ 都发生扰动，这反过来又导致 $f$ 发生变化。链式法则再次告诉我们要将这些贡献相加：

$$
\frac{\partial f}{\partial s} = \frac{\partial f}{\partial x} \frac{\partial x}{\partial s} + \frac{\partial f}{\partial y} \frac{\partial y}{\partial s}
$$

对于关于 $t$ 的[偏导数](@keyword=partial_derivatives|lang=zh-CN|style=Feynman)也是如此。这个公式是将[导数](@keyword=derivative|lang=zh-CN|style=Feynman)的语言从一个[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)翻译到另一个[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)的秘诀。它告诉我们一个函数的“斜率”从不同的视角看是怎样的。例如，对于任何线性[坐标变换](@keyword=coordinate_transformations|lang=zh-CN|style=Feynman)，这个变换都异常简单，它将新的偏导数表示为旧偏导数的[线性组合](@keyword=linear_combinations|lang=zh-CN|style=Feynman) [@problem_id:34735]。这是[张量分析](@keyword=tensor_analysis|lang=zh-CN|style=Feynman)和广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)大部分内容的数学基础，在这些理论中，物理定律必须在任何我们选择用来描述它们的[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)中看起来都一样。

无论变换是简单的旋转、缩放，还是像 $x = r e^{\alpha \theta}$，$y = r e^{-\alpha \theta}$ 这样更复杂的映射，原理都保持不变 [@problem_id:18438]。我们可以有任意数量的中间变量和最终变量，而法则都能优雅地扩展。关键在于画出依赖关系图，并确保你对从求导变量到最终函数的所有可能路径进行求和 [@problem_id:34742] [@problem_id:577473]。

### 揭示简单性：行[波的物理学](@keyword=physics_of_waves|lang=zh-CN|style=Feynman)

现在来看真正的魔力。让我们看看这个看似机械的法则如何能揭示深刻的物理真理。考虑物理学中最基本的方程之一，一维**[平流方程](@keyword=advection_equation|lang=zh-CN|style=Feynman)**（或[输运方程](@keyword=transport_equation|lang=zh-CN|style=Feynman)）：

$$
\frac{\partial u}{\partial t} + c \frac{\partial u}{\partial x} = 0
$$

这里，$u(x,t)$ 可以代表河流中污染物的浓度，或者在空气中传播的压力波的轮廓。该方程表明，$u$ 在一个固定点的时间变化率 $\frac{\partial u}{\partial t}$ 与其空间梯度 $\frac{\partial u}{\partial x}$ 直接相关。这个方程描述了任何以[恒定速度](@keyword=constant_velocity|lang=zh-CN|style=Feynman) $c$ 传播且形状不变的量。

我们如何能确定这一点？让我们提出一个解。任何行波都可以被描述为单个变量的函数 $f(s)$，代表其形状，其中[自变量](@keyword=independent_variables|lang=zh-CN|style=Feynman)在空间和时间上发生了平移。让我们尝试一个形式为 $u(x, t) = f(x - ct)$ 的函数。我们定义中间变量 $s = x - ct$。我们能否证明这个函数总是满足[波动方程](@keyword=wave_equation|lang=zh-CN|style=Feynman)，而与形状 $f$ 无关？链式法则是完成此任务的完美工具。

我们计算 $u$ 关于 $t$ 和 $x$ 的偏导数：
$$
\frac{\partial u}{\partial t} = \frac{df}{ds} \frac{\partial s}{\partial t} = f'(s) \cdot (-c)
$$
$$
\frac{\partial u}{\partial x} = \frac{df}{ds} \frac{\partial s}{\partial x} = f'(s) \cdot (1)
$$

现在，将它们代入[平流方程](@keyword=advection_equation|lang=zh-CN|style=Feynman)：
$$
\frac{\partial u}{\partial t} + c \frac{\partial u}{\partial x} = (-c \cdot f'(s)) + c \cdot (f'(s)) = 0
$$

完美吻合！[@problem_id:34747] [链式法则](@keyword=chain_rule|lang=zh-CN|style=Feynman)刚刚向我们展示了*任何*形式为 $f(x-ct)$ 的[可微函数](@keyword=differentiable_function|lang=zh-CN|style=Feynman)都是一个解。波的形状无关紧要。[链式法则](@keyword=chain_rule|lang=zh-CN|style=Feynman)揭示了一个深刻的真理：结构 $x-ct$ 是以速度 $c$ 进行无畸变传播的数学本质。

我们可以从另一个方向来探讨这个问题，这甚至更有启发性。如果我们不知道解会是什么样子呢？让我们使用[链式法则](@keyword=chain_rule|lang=zh-CN|style=Feynman)来简化方程本身。$x-ct$ 这个形式似乎很重要，所以让我们定义一个随波移动的新[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)。我们定义新坐标为：
$$
\xi = x - ct \quad (\text{在移动坐标系中的位置})
$$
$$
\tau = t \quad (\text{时间的度量})
$$

现在我们将我们的函数 $u$ 视为在这些新坐标下的函数 $v(\xi, \tau)$。我们必须用 $\frac{\partial v}{\partial \xi}$ 和 $\frac{\partial v}{\partial \tau}$ 来重新表示[导数](@keyword=derivative|lang=zh-CN|style=Feynman) $\frac{\partial u}{\partial x}$ 和 $\frac{\partial u}{\partial t}$。使用链式法则：
$$
\frac{\partial u}{\partial x} = \frac{\partial v}{\partial \xi}\frac{\partial \xi}{\partial x} + \frac{\partial v}{\partial \tau}\frac{\partial \tau}{\partial x} = \frac{\partial v}{\partial \xi} \cdot (1) + \frac{\partial v}{\partial \tau} \cdot (0) = \frac{\partial v}{\partial \xi}
$$
$$
\frac{\partial u}{\partial t} = \frac{\partial v}{\partial \xi}\frac{\partial \xi}{\partial t} + \frac{\partial v}{\partial \tau}\frac{\partial \tau}{\partial t} = \frac{\partial v}{\partial \xi} \cdot (-c) + \frac{\partial v}{\partial \tau} \cdot (1) = -c\frac{\partial v}{\partial \xi} + \frac{\partial v}{\partial \tau}
$$

将这些变换后的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)代回我们原来的[平流方程](@keyword=advection_equation|lang=zh-CN|style=Feynman)，得到：
$$
\left( -c\frac{\partial v}{\partial \xi} + \frac{\partial v}{\partial \tau} \right) + c \left( \frac{\partial v}{\partial \xi} \right) = 0
$$

包含 $\frac{\partial v}{\partial \xi}$ 的项相互抵消，这个复杂的[偏微分方程](@keyword=partial_differential_equation|lang=zh-CN|style=Feynman)坍缩成一个惊人简单的形式 [@problem_id:577584]：
$$
\frac{\partial v}{\partial \tau} = 0
$$

这是什么意思？它意味着在移动[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)中，函数 $v$ 不随时间 $\tau$ 变化。因此，$v$ 只能是 $\xi$ 的函数。因为 $v$ 只是 $u$ 的伪装，而 $\xi = x-ct$，我们刚刚证明了*所有*解都必须是 $u(x,t) = f(x-ct)$ 的形式。通过巧妙地选择我们的坐标——一个由链式法则实现的变换——我们将一个动力学问题转化为了一个静态问题，从而完全解出了这个方程。这种寻找能简化问题的坐标的思想，在物理学中是一个反复出现的主题，它支撑着从波现象研究 [@problem_id:34773] 到广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)等强大概念。

### 深入探索更广阔的世界

[链式法则](@keyword=chain_rule|lang=zh-CN|style=Feynman)的力量远不止于这些例子。它像一座桥梁，以令人惊讶的方式连接着数学和科学的不同领域。

在**复分析**中，我们研究函数 $f(z)$，其中变量 $z = x+iy$ 是一个复数。这些函数可以写成 $f(z) = u(x,y) + i v(x,y)$。其中一个被称为“解析”或“全纯”的特殊函数类别，是该理论的真正构建基石。它们满足一对称为**柯西-黎曼方程**的条件。事实证明，有一种极其优雅的方式来思考这个问题。通过形式上定义坐标 $z = x+iy$ 及其[共轭](@keyword=conjugacy|lang=zh-CN|style=Feynman) $\bar{z} = x-iy$，我们可以将 $f$ 视为两个[独立变量](@keyword=independent_variables|lang=zh-CN|style=Feynman) $z$ 和 $\bar{z}$ 的函数。使用[链式法则](@keyword=chain_rule|lang=zh-CN|style=Feynman)，可以计算出[形式导数](@keyword=formal_derivative|lang=zh-CN|style=Feynman) $\frac{\partial f}{\partial \bar{z}}$。结果是惊人的：一个函数是[解析函数](@keyword=analytic_functions|lang=zh-CN|style=Feynman)的条件，恰好是它不依赖于 $\bar{z}$。也就是说，$\frac{\partial f}{\partial \bar{z}} = 0$。整个[解析函数](@keyword=analytic_functions|lang=zh-CN|style=Feynman)理论可以概括为这一句简单的陈述，而链式法则正是让我们能将其与 $(x,y)$ 世界中的柯西-黎曼方程来回转换的工具 [@problem_id:2326910]。

而在我们当今的世界，[链式法则](@keyword=chain_rule|lang=zh-CN|style=Feynman)正在全球各地的服务器上静默运行，为人工智能革命提供动力。用于训练**[深度神经网络](@keyword=deep_neural_networks|lang=zh-CN|style=Feynman)**的核心[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，即**[反向传播](@keyword=backpropagation|lang=zh-CN|style=Feynman)**，不过是[多元链式法则](@keyword=multivariable_chain_rule|lang=zh-CN|style=Feynman)的一个巨大而巧妙的组织化应用。要教会一个网络，你必须理解一个深藏在数百万个连接权重中的单个权重的微小变化，是如何影响最终的输出误差的。[链式法则](@keyword=chain_rule|lang=zh-CN|style=Feynman)为计算这种影响提供了精确的秘诀，使得网络能够调整其权重并进行“学习”。

从在船上行走的简单动作，到纯粹数学和人工智能的前沿，[多元链式法则](@keyword=multivariable_chain_rule|lang=zh-CN|style=Feynman)都是统一的原则。它是变化如何在一个相互连接的系统中流动的逻辑，一个简单的思想，一旦被理解，便能开启对世界复杂机制的更深层次的领悟。

