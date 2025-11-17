## 引言
在科学与工程的众多领域，理解物质如何在空间中运动和[分布](@entry_id:182848)是一个核心问题。[平流-扩散](@entry_id:151021)-漂移方程正是描述这一过程的基石，它统一了由宏观流动（平流）和微观随机运动（[扩散](@entry_id:141445)）共同主导的输运现象。从河流中污染物的[扩散](@entry_id:141445)，到细胞内信号分子的传递，再到[半导体](@entry_id:141536)中杂质的[分布](@entry_id:182848)，这些看似无关的现象背后都遵循着相同的物理和数学规律。本文旨在揭示这一普适模型的核心原理，填补理论与实际应用之间的知识鸿沟。

本文将带领读者踏上一段系统性的学习之旅。在“原理与机制”一章中，我们将从第一性原理出发，推导[平流-扩散方程](@entry_id:746317)，并掌握关键的求解技术。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将探索该模型如何在环境科学、生物学、[材料科学](@entry_id:152226)等多个前沿领域中大放异彩。最后，通过“动手实践”部分，你将有机会亲自应用所学知识解决具体问题。让我们一同开始，深入探索这个描述运动与变化的强大数学工具。

## 原理与机制

在物理、化学、生物学和工程学的众多领域中，物质的输运是一个核心过程。当一种物质（如热量、化学溶质或悬浮颗粒）的浓度[分布](@entry_id:182848)因两种基本机制——**[平流](@entry_id:270026)（advection）**和**[扩散](@entry_id:141445)（diffusion）**——而随时间和空间演变时，其动力学行为可以用[平流-扩散方程](@entry_id:746317)来描述。平流是指物质随流体整体（或宏观）运动而被携带的过程，而[扩散](@entry_id:141445)则是由于分子的随机热运动（或微观）引起的物质从高浓度区域向低浓度区域的净迁移。本章旨在从基本原理出发，系统地阐述描述这些过程的数学模型，并探讨其背后的物理机制和关键的求解方法。

### [平流-扩散方程](@entry_id:746317)：一种唯象描述

描述一维空间中浓度为 $u(x, t)$ 的物质输运的最基本方程是[平流-扩散方程](@entry_id:746317)：
$$
\frac{\partial u}{\partial t} + c \frac{\partial u}{\partial x} = D \frac{\partial^2 u}{\partial x^2}
$$
其中，$u(x, t)$ 是在位置 $x$ 和时间 $t$ 的浓度，$c$ 是恒定的平流速度，$D$ 是恒定的[扩散](@entry_id:141445)系数。这个方程优雅地捕捉了两种输运机制的竞争与协作。

方程左侧的 $\frac{\partial u}{\partial t}$ 代表浓度的局部时间变化率。$c \frac{\partial u}{\partial x}$ 是**平流项**，它描述了浓度场以速度 $c$ 进行的整体平移。如果[浓度梯度](@entry_id:136633) $\frac{\partial u}{\partial x}$ 为正（即浓度随 $x$ 增加），且 $c > 0$，则该项为正，意味着由于上游（$x$ 较小处）更高浓度的物质流向下游，导致该点的浓度有增加的趋势。

方程右侧的 $D \frac{\partial^2 u}{\partial x^2}$ 是**[扩散](@entry_id:141445)项**，它源于**[菲克第二定律](@entry_id:149792)（Fick's second law）**。这一项的作用是平滑浓度[分布](@entry_id:182848)。$\frac{\partial^2 u}{\partial x^2}$ 的正负反映了浓度曲线的凹[凸性](@entry_id:138568)。如果某点浓度高于其邻近点的平均值（$\frac{\partial^2 u}{\partial x^2}  0$），[扩散](@entry_id:141445)将使该点浓度降低；反之，如果浓度低于邻近点（$\frac{\partial^2 u}{\partial x^2} > 0$），[扩散](@entry_id:141445)将使其浓度升高。因此，[扩散](@entry_id:141445)总试图消除浓度极值，使[分布](@entry_id:182848)变得更均匀。

为了更深入地理解该方程的物理意义，我们可以引入**通量（flux）**的概念。通量 $J(x, t)$ 代表在位置 $x$ 处单位时间通过单位面积的物质量。总通量由[平流](@entry_id:270026)通量 $J_{\text{adv}} = c u$ 和[扩散通量](@entry_id:748422) $J_{\text{diff}} = -D \frac{\partial u}{\partial x}$（[菲克第一定律](@entry_id:141732)）组成：
$$
J(x, t) = c u - D \frac{\partial u}{\partial x}
$$
利用通量的概念，[平流-扩散方程](@entry_id:746317)可以写成**[守恒形式](@entry_id:747710)**：
$$
\frac{\partial u}{\partial t} + \frac{\partial J}{\partial x} = 0
$$
这种形式明确地表达了**[质量守恒](@entry_id:204015)原理**：一个微小区域内浓度的变化率等于流入和流出该区域的通量之差。如果一个系统是封闭的，或者在边界处通量为零，那么系统中的总物质量将保持不变。例如，在一个无限长的通道中，如果污染物最初是局部化的，那么在无穷远处浓度 $u$ 和其梯度 $\frac{\partial u}{\partial x}$ 都会趋于零。即使在流速不均匀（即 $v$ 是 $x$ 的函数）的情况下，总通量变为 $J(x, t) = v(x)u - D \frac{\partial u}{\partial x}$，总质量 $M(t) = \int_{-\infty}^{\infty} u(x, t) \, dx$ 的变化率依然为零 [@problem_id:2096193]：
$$
\frac{dM}{dt} = \int_{-\infty}^{\infty} \frac{\partial u}{\partial t} \, dx = - \int_{-\infty}^{\infty} \frac{\partial J}{\partial x} \, dx = - [J(x, t)]_{x=-\infty}^{x=\infty} = 0
$$
这表明，只要通量在无穷远处消失，总质量就是守恒的，这为分析[污染物扩散](@entry_id:195534)等问题提供了一个重要的基本约束。

### 微观起源：从[随机游走](@entry_id:142620)到连续介质方程

[平流-扩散方程](@entry_id:746317)作为宏观的连续介质模型，其根源在于大量微观粒子的集体随机运动。通过分析一个简化的**有偏[随机游走](@entry_id:142620)（biased random walk）**模型，我们可以深刻地理解平流项和[扩散](@entry_id:141445)项的物理起源 [@problem_id:866960]。

想象一个粒子在一维格点上运动，格点间距为 $\Delta x$。在每个时间步长 $\Delta t$ 内，粒子有向右移动一步的概率 $p_R$ 和向左移动一步的概率 $p_L$，且 $p_R + p_L = 1$。如果 $p_R \neq p_L$，则游走是“有偏的”，这意味着存在一个优选的运动方向。

设 $P_j^n$ 是粒子在时间步 $n$ 位于格点 $j$ 的概率。粒子到达格点 $j$ 的唯一方式是在前一步位于 $j-1$ 并向右移动，或者位于 $j+1$ 并向左移动。因此，概率演化遵循以下**主方程（master equation）**：
$$
P_j^{n+1} = p_R P_{j-1}^n + p_L P_{j+1}^n
$$
现在，我们将这个离散模型与连续的概率密度函数 $p(x, t)$ 联系起来，其中 $P_j^n \approx p(j\Delta x, n\Delta t) \Delta x$。[主方程](@entry_id:142959)可以近似写为：
$$
p(x, t+\Delta t) = p_R p(x-\Delta x, t) + p_L p(x+\Delta x, t)
$$
为了过渡到[连续极限](@entry_id:162780)，我们对上式两边进行泰勒展开，假设 $\Delta x$ 和 $\Delta t$ 都很小。对左边展开到 $\Delta t$ 的一阶，对右边展开到 $\Delta x$ 的二阶：
$$
p + \frac{\partial p}{\partial t}\Delta t + \dots \approx p_R \left(p - \frac{\partial p}{\partial x}\Delta x + \frac{1}{2}\frac{\partial^2 p}{\partial x^2}(\Delta x)^2\right) + p_L \left(p + \frac{\partial p}{\partial x}\Delta x + \frac{1}{2}\frac{\partial^2 p}{\partial x^2}(\Delta x)^2\right)
$$
利用 $p_R + p_L = 1$ 并整理各项，我们得到：
$$
\frac{\partial p}{\partial t}\Delta t \approx -(p_R - p_L)\frac{\partial p}{\partial x}\Delta x + \frac{1}{2}(p_R+p_L)\frac{\partial^2 p}{\partial x^2}(\Delta x)^2
$$
两边同除以 $\Delta t$：
$$
\frac{\partial p}{\partial t} \approx -\frac{(p_R - p_L)\Delta x}{\Delta t} \frac{\partial p}{\partial x} + \frac{(\Delta x)^2}{2\Delta t} \frac{\partial^2 p}{\partial x^2}
$$
在[连续极限](@entry_id:162780)中（$\Delta x \to 0$, $\Delta t \to 0$），为了得到一个有意义的非平凡结果，我们必须要求[漂移速度](@entry_id:262489) $v$ 和[扩散](@entry_id:141445)系数 $D$ 保持有限：
$$
v = \frac{(p_R - p_L)\Delta x}{\Delta t}, \quad D = \frac{(\Delta x)^2}{2\Delta t}
$$
这样，我们就从微观的[随机游走模型](@entry_id:180803)推导出了宏观的[平流-扩散方程](@entry_id:746317) $\frac{\partial p}{\partial t} = -v \frac{\partial p}{\partial x} + D \frac{\partial^2 p}{\partial x^2}$。这个推导揭示了：
1.  **[漂移速度](@entry_id:262489) $v$** 直接源于单步运动的**不对称性**或**偏向**（由 $p_R - p_L$ 度量）。如果没有偏向（$p_R = p_L = 0.5$），则 $v=0$，只有纯[扩散](@entry_id:141445)。
2.  **[扩散](@entry_id:141445)系数 $D$** 与**步长的平方**成正比，与**时间步长**成反比。它反映了粒子运动的**随机性**或**波动性**的强度，即使在没有宏观漂移的情况下也存在。

### 动力学分析：关键求解技术

[平流-扩散方程](@entry_id:746317)虽然形式简洁，但其求解往往需要巧妙的数学技巧。下面我们介绍两种核心的变换方法，它们能将[平流-扩散方程](@entry_id:746317)简化为我们更为熟悉的[热传导方程](@entry_id:194763)。

#### 移动[坐标系](@entry_id:156346)

平流项的物理意义是整个浓度[分布](@entry_id:182848)随背景流体平移。这启发我们采用一个随流体一起移动的[坐标系](@entry_id:156346)，即**伽利略变换（Galilean transformation）**。定义移动坐标 $\xi = x - ct$，并设新函数 $v(\xi, t) = u(x, t) = u(\xi + ct, t)$。我们利用[链式法则](@entry_id:190743)计算 $u$ 对 $x$ 和 $t$ 的[偏导数](@entry_id:146280)：
$$
\frac{\partial u}{\partial x} = \frac{\partial v}{\partial \xi} \frac{\partial \xi}{\partial x} = \frac{\partial v}{\partial \xi}
$$
$$
\frac{\partial u}{\partial t} = \frac{\partial v}{\partial t} + \frac{\partial v}{\partial \xi} \frac{\partial \xi}{\partial t} = \frac{\partial v}{\partial t} - c \frac{\partial v}{\partial \xi}
$$
将这些导数代入原方程 $u_t + c u_x = D u_{xx}$（注意到 $u_{xx} = v_{\xi\xi}$）：
$$
\left(\frac{\partial v}{\partial t} - c \frac{\partial v}{\partial \xi}\right) + c \left(\frac{\partial v}{\partial \xi}\right) = D \frac{\partial^2 v}{\partial \xi^2}
$$
[平流](@entry_id:270026)项恰好被抵消，我们得到了在移动[坐标系](@entry_id:156346)下的标准**[热传导方程](@entry_id:194763)（heat equation）**：
$$
\frac{\partial v}{\partial t} = D \frac{\partial^2 v}{\partial \xi^2}
$$
这个变换的威力在于，我们可以先在移动[坐标系](@entry_id:156346)中求解简单的热传导方程，然后再通过 $x = \xi + ct$ 变换回原始的[实验室坐标系](@entry_id:166991)。

考虑一个经典例子：在无限长直杆上，初始温度[分布](@entry_id:182848)为一个高斯函数 $u(x, 0) = U_0 \exp(-x^2/a^2)$ [@problem_id:2144060]。在移动[坐标系](@entry_id:156346)中，初始条件变为 $v(\xi, 0) = U_0 \exp(-\xi^2/a^2)$。[热传导方程](@entry_id:194763)对于高斯初始条件的解是已知的，它本身也是一个随时间展宽的[高斯函数](@entry_id:261394)：
$$
v(\xi, t) = U_0 \frac{a}{\sqrt{a^2 + 4Dt}} \exp\left(-\frac{\xi^2}{a^2 + 4Dt}\right)
$$
最后，我们转换回 $x$ 坐标，得到[平流-扩散方程](@entry_id:746317)的解：
$$
u(x, t) = U_0 \frac{a}{\sqrt{a^2 + 4Dt}} \exp\left(-\frac{(x - ct)^2}{a^2 + 4Dt}\right)
$$
这个解清晰地展示了平流和[扩散](@entry_id:141445)的共同作用：整个[高斯分布](@entry_id:154414)的中心以速度 $c$ 沿着 $x$ 轴移动（体现在 $(x-ct)^2$ 项中），同时[分布](@entry_id:182848)的宽度随时间增加（[方差](@entry_id:200758)为 $\frac{a^2+4Dt}{2}$），峰值高度随时间衰减（幅度为 $U_0 \frac{a}{\sqrt{a^2+4Dt}}$）。重要的是，峰值衰减的速度仅由[扩散](@entry_id:141445)系数 $D$ 和初始宽度 $a$ 决定，而与[平流](@entry_id:270026)速度 $c$ 无关。这直观地证实了[平流](@entry_id:270026)只是“搬运”浓度[分布](@entry_id:182848)，而[扩散](@entry_id:141445)才是使其“弥散”和“衰减”的根本原因。

#### 指数变换

除了移动[坐标系](@entry_id:156346)，还有另一种强大的数学技巧可以将[平流-扩散方程](@entry_id:746317)化为标准热传导方程。我们寻找一个形式为 $u(x,t) = w(x, t) \exp(\alpha x + \beta t)$ 的变换，其中 $\alpha$ 和 $\beta$ 是待定常数 [@problem_id:2096146]。我们的目标是选择合适的 $\alpha$ 和 $\beta$，使得新函数 $w(x,t)$ 满足[热传导方程](@entry_id:194763) $w_t = D w_{xx}$。

为此，我们将 $u$ 的各阶导数用 $w$ 的导数表示，并代入原方程 $u_t + c u_x = D u_{xx}$。经过一系列代数运算后，我们会得到一个关于 $w$ 的方程，其中包含了 $w_x$ 和 $w$ 本身的项。为了使该方程简化为 $w_t = D w_{xx}$，我们必须让 $w_x$ 和 $w$ 的系数为零。这给出了确定 $\alpha$ 和 $\beta$ 的两个条件：
1.  $w_x$ 的系数为零：$c - 2D\alpha = 0 \implies \alpha = \frac{c}{2D}$
2.  $w$ 的系数为零：$\beta + c\alpha - D\alpha^2 = 0 \implies \beta = D\alpha^2 - c\alpha = -\frac{c^2}{4D}$

因此，通过变换 $u(x,t) = w(x, t) \exp\left(\frac{c}{2D}x - \frac{c^2}{4D}t\right)$，[平流-扩散方程](@entry_id:746317)可以严格地转化为热传导方程。这个变换在求解具有特定边界条件的初值问题时尤其有用，因为它保持了空间坐标不变，有时比移动[坐标系](@entry_id:156346)更便于处理边界。

### [稳态](@entry_id:182458)现象

在许多工程和自然系统中，当外部条件（如源、边界浓度）长时间保持不变时，系统会演化到一个**[稳态](@entry_id:182458)（steady state）**，此时浓度[分布](@entry_id:182848) $u(x)$不再随时间变化，即 $\frac{\partial u}{\partial t} = 0$。在这种情况下，原来的[偏微分方程](@entry_id:141332)简化为一个[常微分方程](@entry_id:147024)（ODE），问题的核心变为求解一个边界值问题。

#### 平流与[扩散](@entry_id:141445)的平衡

考虑最简单的情况，即没有反应或[源项](@entry_id:269111)的[稳态](@entry_id:182458)[平流-扩散](@entry_id:151021)过程。此时方程变为：
$$
c \frac{du}{dx} = D \frac{d^2u}{dx^2}
$$
这是一个[二阶线性常微分方程](@entry_id:189146)，其通解为 $u(x) = K_1 + K_2 \exp(\frac{c}{D}x)$。常数 $K_1$ 和 $K_2$ 由边界条件确定。

一个极具启发性的例子是长度为 $L$ 的管道内的[溶质输运](@entry_id:755044) [@problem_id:2096180]。设管道入口 $x=0$ 处浓度维持为 $C_0$，出口 $x=L$ 处浓度为 $0$（例如，溶质被完全吸收）。利用这两个边界条件，可以确定 $K_1$ 和 $K_2$，得到浓度[分布](@entry_id:182848)解。

在这个问题中，一个至关重要的[无量纲参数](@entry_id:169335)自然而然地出现了，那就是**贝克莱数（Péclet number）**：
$$
Pe = \frac{cL}{D}
$$
贝克莱数代表了**平流输运速率**（与 $c$ 相关）与**[扩散输运](@entry_id:150792)速率**（与 $D/L$ 相关）之比。它定量地描述了两种机制的相对重要性：
*   **$Pe \ll 1$ ([扩散](@entry_id:141445)主导)**：当流速很慢或[扩散](@entry_id:141445)很快时，[平流](@entry_id:270026)作用可以忽略。浓度[分布](@entry_id:182848)近似为一条直线 $C(x) \approx C_0(1 - x/L)$，这与纯[扩散](@entry_id:141445)情况下的[稳态解](@entry_id:200351)一致。物质通过[扩散](@entry_id:141445)缓慢地穿过管道。
*   **$Pe \gg 1$ (平流主导)**：当流速很快或[扩散](@entry_id:141445)很慢时，物质主要被水流“冲刷”到下游。在大部分管道区域（远离出口），浓度都接近入口浓度 $C_0$。只有在靠近出口 $x=L$ 的一个薄**[边界层](@entry_id:139416)（boundary layer）**内，浓度才急剧下降至零。这个[边界层](@entry_id:139416)的厚度尺度约为 $D/c$。

系统的总物质量 $M$ 的表达式同样依赖于 $Pe$ [@problem_id:2096180]。在[扩散](@entry_id:141445)主导时，$M \approx \frac{1}{2} A C_0 L$（对应线性[分布](@entry_id:182848)的积分），而在[平流](@entry_id:270026)主导时，$M \approx A C_0 L$（对应近乎常数 $C_0$ 的[分布](@entry_id:182848)）。类似地，通过管道的[稳态通量](@entry_id:183999) $J$ 也可以根据 $Pe$ 进行分析 [@problem_id:2096166]，在平流主导时，$J \approx vC_0$，表明几乎所有物质都是被平流带走的。

#### 与反应和空间变化漂移的平衡

[稳态分析](@entry_id:271474)可以推广到更复杂的情况。例如，当物质在[输运过程](@entry_id:177992)中还会发生一级衰变反应时，方程变为 $D u'' - c u' - k u = 0$，其中 $k > 0$ 是[反应速率常数](@entry_id:187887) [@problem_id:2096174]。其解的形式为指数衰减函数。对于一个从 $x=0$ 处开始的半无限长通道，浓度[分布](@entry_id:182848)将呈指数形式从入口值 $u_0$ 衰减到无穷远处的零。衰减的[特征长度](@entry_id:265857)由[平流](@entry_id:270026)、[扩散](@entry_id:141445)和反应三者的复杂相互作用共同决定，其特征根为 $\lambda = \frac{c \pm \sqrt{c^2+4Dk}}{2D}$。由于浓度必须在 $x \to \infty$ 时衰减至零，我们必须选择负的特征根，从而得到一个随距离指数衰减的[稳态](@entry_id:182458)剖面。

更有趣的是当漂移速度本身依赖于空间位置时的情况。考虑一个将粒子拉向原点的线性恢复[力场](@entry_id:147325)，其导致的[漂移速度](@entry_id:262489)为 $v(x) = -\alpha x$（$\alpha > 0$）[@problem_id:2096160]。[稳态](@entry_id:182458)意味着净通量处处为零：
$$
J = v(x)u - D \frac{du}{dx} = -\alpha x u - D \frac{du}{dx} = 0
$$
这是一个可分离变量的[一阶常微分方程](@entry_id:264241)，其解为一个高斯分布：
$$
u_{ss}(x) = A \exp\left(-\frac{\alpha}{2D} x^2\right)
$$
其中 $A$ 是由总质量决定的归一化常数。这个结果意义深远：系统达到平衡时，由恢复[力场](@entry_id:147325)引起的向中心的确定性漂移与由随机运动引起的向外的[扩散](@entry_id:141445)趋势精确平衡。

这个[高斯分布](@entry_id:154414)的[方差](@entry_id:200758)为 $\sigma^2 = \frac{D}{\alpha}$。这个关系式是**爱因斯坦关系（Einstein relation）**的一个例子，也是**涨落-耗散定理（fluctuation-dissipation theorem）**的一种体现。它深刻地揭示了微观世界的随机涨落（由[扩散](@entry_id:141445)系数 $D$ 表征）与系统对宏观扰动（此处为恢复力，由 $\alpha$ 表征）的响应之间的内在联系。

### 高级主题：[行波](@entry_id:185008)与[非线性](@entry_id:637147)

#### [行波解](@entry_id:272909)

在某些情况下，[平流-扩散系统](@entry_id:746318)可以支持一种特殊类型的解，其形状保持不变，仅以恒定速度在空间中传播。这种解被称为**[行波解](@entry_id:272909)（traveling wave solution）**，通常形式为 $u(x, t) = f(x - v_w t)$，其中 $v_w$ 是波速。

考虑一个同时包含[平流](@entry_id:270026)、[扩散](@entry_id:141445)和反应的例子，化学物质在速度为 $v_0$ 的水流中输运，并以速率 $k$ 衰减 [@problem_id:2096188]。其方程为 $C_t + v_0 C_x = D C_{xx} - kC$。如果我们假设存在一个随水流一起移动的稳定浓度剖面，即寻找波速 $v_w=v_0$ 的[行波解](@entry_id:272909)，我们可以设 $C(x, t) = u(\xi)$，其中 $\xi = x - v_0 t$。代入原方程后，平流项 $v_0 C_x$ 和时间导数项 $C_t = -v_0 u'$ 恰好抵消，方程简化为关于 $u(\xi)$ 的[常微分方程](@entry_id:147024)：
$$
D u'' - k u = 0
$$
对于一个在前端 $\xi=0$ 处浓度为 $C_0$ 并向后方（$\xi \to \infty$）衰减的物理情景，解为 $u(\xi) = C_0 \exp(-\sqrt{k/D} \xi)$。这描述了一个稳定的浓度锋面，它以流体速度 $v_0$ 传播，其锋面形状（指数衰减长度）由[扩散](@entry_id:141445)和反应之间的平衡决定。

#### 质心与[非线性](@entry_id:637147)[扩散](@entry_id:141445)

平流的一个核心特性是它作为一种整体输运机制。这个特性即使在扩散过程变得复杂（例如[非线性](@entry_id:637147)）时也依然保持。考虑一个**[非线性](@entry_id:637147)[扩散](@entry_id:141445)**过程，其[扩散](@entry_id:141445)系数依赖于浓度本身，例如 $D(u) \propto u^m$ ($m>0$)。相应的方程为 [@problem_id:2096175]：
$$
\frac{\partial u}{\partial t} + c \frac{\partial u}{\partial x} = \frac{\partial}{\partial x}\left(u^m \frac{\partial u}{\partial x}\right)
$$
尽管这个方程是高度[非线性](@entry_id:637147)的，我们仍然可以分析其**质心（center of mass）** $x_{cm}(t) = \frac{\int x u \,dx}{\int u \,dx}$ 的运动。

通过对总质量 $M = \int u \,dx$ 和一阶矩 $M_1 = \int x u \,dx$ 的时间演化进行分析，可以证明：
1.  总质量 $M$ 是守恒的，即 $\frac{dM}{dt} = 0$。
2.  一阶矩的变化率是 $\frac{dM_1}{dt} = cM$。

推导过程表明，复杂的[非线性](@entry_id:637147)[扩散](@entry_id:141445)项在对 $\frac{dM_1}{dt}$ 的贡献中，经过分部积分后恰好为零。因此，[质心](@entry_id:265015)的速度为：
$$
v_{cm} = \frac{d x_{cm}}{dt} = \frac{d}{dt}\left(\frac{M_1}{M}\right) = \frac{1}{M} \frac{dM_1}{dt} = c
$$
这个优雅的结果表明，无论内部的[扩散过程](@entry_id:170696)多么复杂（线性或[非线性](@entry_id:637147)），物质[分布](@entry_id:182848)的质心总是以恒定的[平流](@entry_id:270026)速度 $c$ 移动。这强有力地说明了平流输运的宏观本质：它将整个物质[分布](@entry_id:182848)作为一个整体进行平移，而[扩散](@entry_id:141445)（无论其形式如何）则负责改变[分布](@entry_id:182848)相对于其[质心](@entry_id:265015)的形状。