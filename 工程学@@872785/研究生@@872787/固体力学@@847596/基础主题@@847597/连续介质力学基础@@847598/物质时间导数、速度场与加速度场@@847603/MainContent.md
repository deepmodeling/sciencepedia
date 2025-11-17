## 引言
在连续介质力学中，精确描述物体的运动是理解其力学行为（如变形、应力和流动）的基石。物理量（如速度和加速度）不仅随时间变化，还随空间位置的不同而变化。如何追踪一个移动物质点的属性，同时又能在固定的空间[坐标系](@entry_id:156346)下进行分析，是运动学中的一个核心挑战。[物质时间导数](@entry_id:190892)正是为了解决这一问题而引入的强大数学工具，它构成了从“追随粒子”的[拉格朗日视角](@entry_id:265471)到“固定观察点”的[欧拉视角](@entry_id:265288)之间的桥梁。

本文将系统地引导读者深入理解这一关键概念及其广泛应用。在“原理和机制”章节中，我们将首先建立拉格朗日和[欧拉描述](@entry_id:264722)的运动学框架，并在此基础上推导出[物质时间导数](@entry_id:190892)的表达式，揭示[局部加速度](@entry_id:272847)与[对流加速度](@entry_id:263153)的物理本质。接着，在“应用与跨学科联系”章节中，我们将展示物质导数如何成为连接运动学与动力学（如牛顿定律）、[流体动力学](@entry_id:136788)（如涡量演化）和固体力学（如[动态断裂](@entry_id:190194)）的纽带，阐明其在不同科学领域中的统一作用。最后，“动手实践”章节将提供具体的计算练习，帮助读者将理论知识转化为解决实际问题的能力。通过这一结构化的学习路径，读者将全面掌握描述和分析连续介质运动的核心方法。

## 原理和机制

在[连续介质力学](@entry_id:155125)中，对物体运动的描述是理解其变形和受力的基础。本章旨在深入阐释描述运动的基本原理，重点关注速度场和[加速度场](@entry_id:266595)，并引入材料时间导数这一核心概念。我们将从拉格朗日和欧拉这两种基本描述方法出发，系统地建立起描述连续介质运动的运动学框架。

### 描述运动：[拉格朗日与欧拉](@entry_id:270774)视角

为了精确描述连续体的运动，我们需要一种方法来追踪其内部的每一个物[质点](@entry_id:186768)。有两种标准的方法：[拉格朗日描述](@entry_id:264498)和[欧拉描述](@entry_id:264722)。

**[拉格朗日描述](@entry_id:264498)（Lagrangian Description）**，或称**物质描述（Material Description）**，采取的是一种“追随粒子”的观点。我们首先在某个参考时刻（通常是 $t=0$）为连续体中的每一个物[质点](@entry_id:186768)分配一个唯一的标签。这个标签通常就是该点在**参考构型（reference configuration）** $\mathcal{B}_0$ 中的位置向量 $\mathbf{X}$。然后，我们通过一个**运动映射（motion map）** $\boldsymbol{\chi}$ 来追踪这个被标记的物质点在所有时刻 $t$ 的空间位置 $\mathbf{x}$。

$$
\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)
$$

这个映射将物质坐标 $\mathbf{X}$ 和时间 $t$ 映射到该物质点在**当前构型（current configuration）** $\mathcal{B}_t$ 中的空间位置 $\mathbf{x}$。对于一个固定的物质点 $\mathbf{X}$，函数 $\mathbf{x}_{\mathbf{X}}(t) = \boldsymbol{\chi}(\mathbf{X}, t)$ 描绘了该物质点随时间变化的轨迹，这条轨迹被称为**质点路径（pathline）**[@problem_id:2659098]。[拉格朗日描述](@entry_id:264498)的本质是观察固定物[质点](@entry_id:186768)的物理量如何随时间演化。

**[欧拉描述](@entry_id:264722)（Eulerian Description）**，或称**空间描述（Spatial Description）**，则采取一种“固定观测点”的观点。我们关注空间中一个固定的点 $\mathbf{x}$，并观察在不同时刻 $t$ 流经该点的不同物质点的物理性质。例如，一个欧拉速度场 $\mathbf{v}(\mathbf{x}, t)$ 给出的是在时刻 $t$ 位于空间点 $\mathbf{x}$ 的那个物[质点](@entry_id:186768)的速度。

这两种描述通过运动映射 $\boldsymbol{\chi}$ 紧密联系在一起。一个在[欧拉框架](@entry_id:749109)下定义的场 $f(\mathbf{x}, t)$ 可以通过[复合函数](@entry_id:147347) $f(\boldsymbol{\chi}(\mathbf{X}, t), t)$ 转换为[拉格朗日描述](@entry_id:264498)。反之，一个拉格朗日场 $F(\mathbf{X}, t)$ 则可以通过反向映射 $\mathbf{X} = \boldsymbol{\chi}^{-1}(\mathbf{x}, t)$ 转换为欧拉场 $F(\boldsymbol{\chi}^{-1}(\mathbf{x}, t), t)$。这个反向映射的存在性，要求运动映射对于任意固定的时刻 $t$ 都是[一一对应](@entry_id:143935)的，这保证了物质不会发生非物理的自我穿透。

### [速度场](@entry_id:271461)和[加速度场](@entry_id:266595)

基于上述两种描述，我们可以定义速度和加速度。

在[拉格朗日描述](@entry_id:264498)中，物质点 $\mathbf{X}$ 的**材料速度（material velocity）** $\mathbf{V}$ 和**材料加速度（material acceleration）** $\mathbf{A}$ 的定义非常直观，它们分别是物[质点](@entry_id:186768)位置对时间的[偏导数](@entry_id:146280)，因为我们是固定 $\mathbf{X}$ 进行求导的：

$$
\mathbf{V}(\mathbf{X}, t) = \frac{\partial \boldsymbol{\chi}(\mathbf{X}, t)}{\partial t}
$$

$$
\mathbf{A}(\mathbf{X}, t) = \frac{\partial^2 \boldsymbol{\chi}(\mathbf{X}, t)}{\partial t^2} = \frac{\partial \mathbf{V}(\mathbf{X}, t)}{\partial t}
$$

在[欧拉描述](@entry_id:264722)中，**[空间速度](@entry_id:190294)场（spatial velocity field）** $\mathbf{v}(\mathbf{x}, t)$ 描述的是在时刻 $t$ 位于空间点 $\mathbf{x}$ 的那个物[质点](@entry_id:186768)的速度。为了得到这个速度，我们首先需要知道是哪个物[质点](@entry_id:186768) $\mathbf{X}$ 在该时刻位于 $\mathbf{x}$，即 $\mathbf{X} = \boldsymbol{\chi}^{-1}(\mathbf{x}, t)$。然后，我们取这个物[质点](@entry_id:186768)的材料速度 $\mathbf{V}(\mathbf{X}, t)$。因此，[空间速度](@entry_id:190294)场与材料速度场的关系是 [@problem_id:2659098]：

$$
\mathbf{v}(\mathbf{x}, t) = \mathbf{V}(\boldsymbol{\chi}^{-1}(\mathbf{x}, t), t) = \frac{\partial \boldsymbol{\chi}}{\partial t} \bigg|_{\mathbf{X}=\boldsymbol{\chi}^{-1}(\mathbf{x}, t)}
$$

一个关键的问题是，如何从[空间速度](@entry_id:190294)场 $\mathbf{v}(\mathbf{x}, t)$ 出发计算加速度？我们不能简单地对 $\mathbf{v}(\mathbf{x}, t)$ 求时间[偏导数](@entry_id:146280) $\frac{\partial \mathbf{v}}{\partial t}$。这个量表示在空间[固定点](@entry_id:156394) $\mathbf{x}$ 处[速度场](@entry_id:271461)自身随时间的变化率，它被称为**[局部加速度](@entry_id:272847)（local acceleration）**。然而，一个物质点在运动时，其自身的位置也在变化，它会从一个速度较低的区域移动到一个速度较高的区域，即使[速度场](@entry_id:271461)本身不随时间变化（[定常流](@entry_id:191654)动），该物[质点](@entry_id:186768)依然在加速。这种由于物[质点](@entry_id:186768)在空间中位置变化而引起的速度变化所导致的加速度，称为**[对流加速度](@entry_id:263153)（convective acceleration）**。

一个物[质点](@entry_id:186768)的真实加速度，即**材料加速度（material acceleration）**，必须同时包含[局部加速度](@entry_id:272847)和[对流加速度](@entry_id:263153)。为了计算这个加速度，我们需要计算跟随物[质点](@entry_id:186768)运动的[速度场](@entry_id:271461)的时间变化率。这个变化率被称为**材料时间导数（material time derivative）**，通常记为 $\frac{D}{Dt}$。

对于一个任意的空间[标量场](@entry_id:151443) $f(\mathbf{x}, t)$，其材料时间导数是函数 $f(\boldsymbol{\chi}(\mathbf{X}, t), t)$ 对时间的[全导数](@entry_id:137587)。根据[多元函数](@entry_id:145643)[链式法则](@entry_id:190743)：

$$
\frac{D f}{D t} = \frac{d}{dt} f(\boldsymbol{\chi}(\mathbf{X}, t), t) = \frac{\partial f}{\partial t} + \nabla f \cdot \frac{\partial \boldsymbol{\chi}(\mathbf{X}, t)}{\partial t}
$$

注意到 $\frac{\partial \boldsymbol{\chi}}{\partial t}$ 正是物质点的速度 $\mathbf{v}$，因此我们得到了材料时间导数在[欧拉描述](@entry_id:264722)下的标准形式 [@problem_id:2659098]：

$$
\frac{D f}{D t} = \underbrace{\frac{\partial f}{\partial t}}_{\text{局部变化}} + \underbrace{\mathbf{v} \cdot \nabla f}_{\text{对流变化}}
$$

现在，我们可以将这个算子应用于[空间速度](@entry_id:190294)场 $\mathbf{v}(\mathbf{x}, t)$ 本身，以获得空间[加速度场](@entry_id:266595) $\mathbf{a}(\mathbf{x}, t)$ [@problem_id:2659113]。$\mathbf{a}(\mathbf{x}, t)$ 是在时刻 $t$ 位于空间点 $\mathbf{x}$ 的物[质点](@entry_id:186768)的真实加速度。

$$
\mathbf{a}(\mathbf{x}, t) = \frac{D \mathbf{v}}{D t} = \frac{\partial \mathbf{v}}{\partial t} + (\mathbf{v} \cdot \nabla)\mathbf{v}
$$

值得强调的是，$\mathbf{a}(\boldsymbol{\chi}(\mathbf{X}, t), t) = \mathbf{A}(\mathbf{X}, t) = \frac{\partial^2 \boldsymbol{\chi}}{\partial t^2}$，这表明在物[质点](@entry_id:186768)轨迹上求值的空间[加速度场](@entry_id:266595)与该点的材料加速度是完全等价的 [@problem_id:2659098]。

一个经典的例子可以阐明[对流加速度](@entry_id:263153)的重要性。考虑一个绕 $z$ 轴以恒定角速度 $\omega_0$ 作[刚体转动](@entry_id:191086)的物体。其[空间速度](@entry_id:190294)场为 $\mathbf{v}(\mathbf{x}) = \omega_0 \mathbf{e}_z \times \mathbf{x} = (-\omega_0 y, \omega_0 x, 0)$。这是一个**定常（steady）**流动，因为速度场不随时间变化，即 $\frac{\partial \mathbf{v}}{\partial t} = \mathbf{0}$。然而，物体中的[质点](@entry_id:186768)（除轴上点外）显然在做[匀速圆周运动](@entry_id:178264)，存在向心加速度。让我们用公式计算：

$$
\mathbf{a} = (\mathbf{v} \cdot \nabla)\mathbf{v} = \left(-\omega_0 y \frac{\partial}{\partial x} + \omega_0 x \frac{\partial}{\partial y}\right) (-\omega_0 y, \omega_0 x, 0)
$$

计算各分量可得：
$a_x = -\omega_0^2 x$
$a_y = -\omega_0^2 y$
$a_z = 0$

因此，[加速度场](@entry_id:266595)为 $\mathbf{a}(\mathbf{x}) = -\omega_0^2(x, y, 0) = -\omega_0^2 \mathbf{x}_{\perp}$，这正是指向旋转中心的[向心加速度](@entry_id:190458)。例如，在点 $\mathbf{x}^* = (R, 0, 0)$，加速度为 $\mathbf{a} = -\omega_0^2 R \mathbf{e}_x$。如果 $\omega_0 = 3.0 \, \text{s}^{-1}$ 且 $R = 2.0 \, \text{m}$，则加速度大小为 $(3.0)^2 \times 2.0 = 18.0 \, \text{m/s}^2$ [@problem_id:2659113]。这个例子清晰地表明，即使在[定常流](@entry_id:191654)中，只要[速度场](@entry_id:271461)在空间上不均匀（$\nabla \mathbf{v} \neq \mathbf{0}$），物[质点](@entry_id:186768)依然可以有非零的加速度。

### 运动学诠释与路径几何

为了更直观地理解流场，我们引入三个几何概念：质点路径、[流线和迹线](@entry_id:182288)。

*   **[质点](@entry_id:186768)路径（Pathline）**：如前所述，是一个特定物质点随时间移动的轨迹。它是[常微分方程](@entry_id:147024) $\frac{d\mathbf{x}_p}{dt} = \mathbf{v}(\mathbf{x}_p, t)$ 的解 [@problem_id:2659106]。

*   **[流线](@entry_id:266815)（Streamline）**：是在某一固定时刻 $t^*$，流场中一系列与速度矢量相切的曲线。它们给出了该时刻流速方向的“快照”。流线由方程 $\frac{d\mathbf{x}}{ds} \parallel \mathbf{v}(\mathbf{x}, t^*)$ 定义，其中 $s$是曲线的[弧长](@entry_id:191173)参数 [@problem_id:2659106]。

*   **[迹线](@entry_id:261720)（Streakline）**：是在某一固定时刻 $t^*$，所有曾经流经空间中某一同个[固定点](@entry_id:156394) $\mathbf{x}_a$ 的物[质点](@entry_id:186768)的集合。可以想象成在 $\mathbf{x}_a$ 处不断注入染料所形成的线条 [@problem_id:2659106]。

在**[定常流](@entry_id:191654)（steady flow）**中，即 $\frac{\partial \mathbf{v}}{\partial t} = \mathbf{0}$，[速度场](@entry_id:271461)不随时间变化，这三个概念定义的曲线是重合的。然而，在**[非定常流](@entry_id:269993)（unsteady flow）**中，它们通常是不同的。一个更普适的重合条件是，[速度场](@entry_id:271461)的方向不随时间改变，即[速度场](@entry_id:271461)可以写成 $\mathbf{v}(\mathbf{x}, t) = \alpha(t) \mathbf{u}(\mathbf{x})$ 的形式，其中 $\alpha(t)$ 是一个标量时间函数，$\mathbf{u}(\mathbf{x})$ 是一个矢量空间函数。在这种情况下，尽管速度大小可能变化，但流线图案的几何形状是固定的，[质点](@entry_id:186768)路径和[迹线](@entry_id:261720)都将被限制在这些固定的[流线](@entry_id:266815)上 [@problem_id:2659106]。例如，对于速度场 $\mathbf{v}_1 = (\alpha(t)x, -\alpha(t)y)$，其流线总是满足 $xy = \text{const.}$ 的[双曲线](@entry_id:174213)，因此质点路径和[迹线](@entry_id:261720)也位于这些双曲线上。

加速度的概念也可以通过[质点](@entry_id:186768)路径的几何形状来深入理解。一个物[质点](@entry_id:186768)的速度矢量 $\mathbf{v}$ 总是与该点的质点路径相切 [@problem_id:2659114]。我们可以将速度写成 $\mathbf{v} = v \mathbf{T}$，其中 $v = \|\mathbf{v}\|$ 是速率，$\mathbf{T}$ 是路径的[单位切向量](@entry_id:262985)。物质点的加速度是其速度的材料时间导数：

$$
\mathbf{a} = \frac{D\mathbf{v}}{Dt} = \frac{d(v\mathbf{T})}{dt} = \frac{dv}{dt}\mathbf{T} + v\frac{d\mathbf{T}}{dt}
$$

利用链式法则和[弧长](@entry_id:191173)参数 $s$，我们有 $\frac{d\mathbf{T}}{dt} = \frac{d\mathbf{T}}{ds}\frac{ds}{dt}$。根据[微分几何](@entry_id:145818)中的[Frenet-Serret公式](@entry_id:267751)，$d\mathbf{T}/ds = \kappa \mathbf{n}$，其中 $\kappa$ 是路径的**曲率（curvature）**，$\mathbf{n}$ 是指向曲线凹侧的**[主法向量](@entry_id:263263)（principal normal vector）**。同时，$\frac{ds}{dt} = v$ 是速率。将这些代入，我们得到加速度的内蕴分解 [@problem_id:2659114]：

$$
\mathbf{a} = \underbrace{\frac{dv}{dt}\mathbf{T}}_{\text{切向加速度}} + \underbrace{v^2\kappa\mathbf{n}}_{\text{法向加速度}}
$$

这个简洁的公式表明，加速度有两个分量：
1.  **[切向加速度](@entry_id:173884)**：与路径相切，大小为 $\frac{dv}{dt}$，负责改变速度的大小（速率）。
2.  **[法向加速度](@entry_id:170071)**（或向心加速度）：与路径垂直，指向[曲率中心](@entry_id:270032)，大小为 $v^2\kappa$，负责改变速度的方向。

如果一个质点沿其路径以恒定速率运动（$\frac{dv}{dt}=0$），它的加速度将完全是法向的，即 $\mathbf{a} = v^2\kappa\mathbf{n}$ [@problem_id:2659114]。在前面讨论的刚体旋转例子中，质点做[匀速圆周运动](@entry_id:178264)，速率 $v=\omega_0 r$ 恒定，曲率 $\kappa=1/r$，法向量 $\mathbf{n}=-\mathbf{e}_r$。代入公式得到 $\mathbf{a} = (\omega_0 r)^2 (1/r) (-\mathbf{e}_r) = -\omega_0^2 r \mathbf{e}_r$，与我们之前的计算完全吻合 [@problem_id:2659082]。这表明[对流加速度](@entry_id:263153)项 $(\mathbf{v} \cdot \nabla)\mathbf{v}$ 包含了关于路径曲率的关键信息。

### 材料导数与输运现象

材料时间导数的概念不仅适用于速度，也适用于任何与物[质点](@entry_id:186768)相关的物理量，它是描述物质属性如何在流体中被输运的基本工具。

考虑一个[标量场](@entry_id:151443) $c(\mathbf{x}, t)$，例如温度或浓度。如果这个量是**被动[平流](@entry_id:270026)输运（passively advected）**的，意味着它仅仅是随物质点一起运动，而没有自身的产生、消散或[扩散](@entry_id:141445)。这在物理上等价于说，对于任何一个物质点，其 $c$ 值不随时间改变。用材料导数表达，就是 [@problem_id:2659108]：

$$
\frac{Dc}{Dt} = \frac{\partial c}{\partial t} + \mathbf{v} \cdot \nabla c = 0
$$

这个方程是连续介质力学中描述守恒律的基础。例如，如果 $c$ 代表一个相场变量，其值为 $c^*$ 的[等值面](@entry_id:196027) $c(\mathbf{x}, t)=c^*$ 定义了一个移动的界面。从上式可以推导出，该界面的法向速度 $v_n$ 等于材料速度在该方向上的投影，即 $v_n = \mathbf{v} \cdot \mathbf{n}$。这个演化规律是纯运动学的，不包含曲率等几何效应。只有当物理模型包含[扩散](@entry_id:141445)（如$\nabla^2 c$项）或其它依赖于界面几何的物理（如表面张力）时，曲率才会出现在界面的[演化方程](@entry_id:268137)中 [@problem_id:2659108]。

材料导数也可以应用于矢量和张量场。一个特别重要的例子是**物质线元（material line element）** $d\boldsymbol{\ell}$ 的演化。一个在参考构型中连接两个邻近物质点 $\mathbf{X}$ 和 $\mathbf{X}+d\mathbf{X}$ 的线元 $d\mathbf{X}$，在当前构型中被映射为 $d\boldsymbol{\ell} = \mathbf{F} d\mathbf{X}$，其中 $\mathbf{F} = \frac{\partial \boldsymbol{\chi}}{\partial \mathbf{X}}$ 是**变形梯度（deformation gradient）**。$d\boldsymbol{\ell}$ 的材料时间导数描述了这个物质线元如何被流动拉伸和旋转。可以证明 [@problem_id:2659110]：

$$
\frac{D(d\boldsymbol{\ell})}{Dt} = \dot{\mathbf{F}} d\mathbf{X} = (\nabla\mathbf{v})\mathbf{F} d\mathbf{X} = \mathbf{L} d\boldsymbol{\ell}
$$

其中 $\mathbf{L} = \nabla \mathbf{v}$ 是**[空间速度梯度](@entry_id:187198)（spatial velocity gradient）**。这个基本关系表明，物质[线元](@entry_id:196833)的拉伸和旋转率由[速度梯度张量](@entry_id:270928) $\mathbf{L}$ 控制。

### 高级主题：张量的[客观时间导数](@entry_id:189677)

在构建本构关系（如应力-[应变率](@entry_id:154778)关系）时，一个核心要求是物理定律必须独立于观察者，即满足**物质客观性（material frame-indifference）原理**。这意味着[本构方程](@entry_id:138559)的形式在不同的（旋转或平移的）[坐标系](@entry_id:156346)下应该保持不变。

一个直接的后果是，本构关系中使用的张量时间导数必须是**客观的（objective）**。一个张量率 $\mathcal{R}(\mathbf{S})$ 被认为是客观的，如果在一个叠加的刚体运动下，它的变换规律与张量本身相同，即 $\mathcal{R}^*(\mathbf{S}^*) = \mathbf{Q} \mathcal{R}(\mathbf{S}) \mathbf{Q}^T$，其中 $\mathbf{Q}(t)$ 是描述[坐标系](@entry_id:156346)变换的正交张量。

一个令人惊讶但至关重要的事实是，**材料时间导数 $\frac{D\mathbf{S}}{Dt}$ 本身并不是一个[客观率](@entry_id:198692)**。在[坐标系](@entry_id:156346)变换下，它的变换规律会多出与观察者自旋相关的附加项 [@problem_id:2659119]：

$$
\frac{D \mathbf{S}^{\ast}}{D t} = \mathbf{Q}\frac{D \mathbf{S}}{D t}\mathbf{Q}^{T} + \mathbf{W}_{Q} \mathbf{S}^{\ast} - \mathbf{S}^{\ast} \mathbf{W}_{Q}
$$

其中 $\mathbf{W}_Q = \dot{\mathbf{Q}}\mathbf{Q}^T$ 是观察者[坐标系](@entry_id:156346)的[自旋张量](@entry_id:187346)。附加项 $\mathbf{W}_{Q} \mathbf{S}^{\ast} - \mathbf{S}^{\ast} \mathbf{W}_{Q}$ 的存在表明 $\frac{D\mathbf{S}}{Dt}$ 依赖于观察者的选择。

为了解决这个问题，我们需要构建客观的时间导数。这些导数通过从材料导数中减去由材料自身旋转引起的部分来“修正”非客观性。最常用的两个[客观率](@entry_id:198692)是：

1.  **[上随体导数](@entry_id:756365)（Upper-Convected Derivative）** $\overset{\triangledown}{\mathbf{S}}$:
    $$
    \overset{\triangledown}{\mathbf{S}} = \frac{D\mathbf{S}}{Dt} - \mathbf{L}\mathbf{S} - \mathbf{S}\mathbf{L}^T
    $$
    这个导数测量了张量 $\mathbf{S}$ 在随体[坐标系](@entry_id:156346)下的变化率，该[坐标系](@entry_id:156346)随材料一起变形。可以证明，当一个矢量场 $\mathbf{w}$ 像物质线元一样被输运时（即 $\mathbf{w} = \mathbf{F} \mathbf{W}_0$），其[上随体导数](@entry_id:756365)为零，即 $\frac{D\mathbf{w}}{Dt} - \mathbf{L}\mathbf{w} = \mathbf{0}$ [@problem_id:2659110]。对于速度场本身 $\mathbf{v}$，在[定常流](@entry_id:191654)条件下 ($\partial\mathbf{v}/\partial t = \mathbf{0}$)，也满足这个关系 [@problem_id:2659110]。

2.  **[同转导数](@entry_id:203813)（Corotational or Jaumann Derivative）** $\overset{\circ}{\mathbf{T}}$:
    $$
    \overset{\circ}{\mathbf{T}} = \frac{D\mathbf{T}}{Dt} - \mathbf{W}\mathbf{T} + \mathbf{T}\mathbf{W}
    $$
    其中 $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^T)$ 是流动的**[自旋张量](@entry_id:187346)（spin tensor）**。这个导数测量了张量相对于一个仅随材料旋转但不变形的[坐标系](@entry_id:156346)的变化率。可以严格证明，$\overset{\triangledown}{\mathbf{S}}$ 和 $\overset{\circ}{\mathbf{T}}$ 都是客观的 [@problem_id:2659119] [@problem_id:2659097]。特别地，如果物体本身只进行[刚体运动](@entry_id:193355)（无变形），那么一个随体固定的张量（例如，$\mathbf{T} = \mathbf{Q}(t)\mathbf{T}_0\mathbf{Q}^T(t)$）的[同转导数](@entry_id:203813)恒为零，这直观地体现了其物理意义 [@problem_id:2659097]。

### 与动力学的联系：关于边界条件的注记

最后，澄清一个运动学和动力学之间的常见混淆点。考虑一个具有**自由表面（free surface）**的物体，即边界上没有施加外力（traction-free）。根据柯西应力定理，这个**动力学边界条件**写作 $\boldsymbol{\sigma}\mathbf{n} = \mathbf{0}$，其中 $\boldsymbol{\sigma}$ 是柯西[应力张量](@entry_id:148973) [@problem_id:2659096]。

重要的是要认识到，这个条件直接约束的是应力状态，而不是[运动学](@entry_id:173318)量。它并不直接规定边界上的速度 $\mathbf{v}$ 或加速度 $\mathbf{a}$ 必须是多少。边界上点的速度和加速度是整个动力学问题（包括[运动方程](@entry_id:170720) $\rho\mathbf{a} = \nabla \cdot \boldsymbol{\sigma} + \mathbf{b}$、本构关系和所有边界/[初始条件](@entry_id:152863)）求解的结果，而不是预先设定的。

那么，自由表面的运动学如何保证呢？关键在于自由表面是一个**物质表面（material surface）**。这意味着构成表面的物[质点](@entry_id:186768)永远停留在表面上。因此，表面的运动必须与表面上物[质点](@entry_id:186768)的运动兼容。这意味着边界点 $\mathbf{x}_b$ 的速度就是该点处的材料速度，即 $\frac{d\mathbf{x}_b}{dt} = \mathbf{v}(\mathbf{x}_b, t)$。边界的形状和位置因此与内部的运动场耦合在一起，共同作为问题的解被确定下来。认为自由表面上法向速度或加速度必须为零是错误的；例如，一个正在膨胀或[振动](@entry_id:267781)的气泡，其表面上的点显然具有非零的法向速度和加速度 [@problem_id:2659096]。