## 引言
连续介质力学是一门基础性的理论学科，它提供了一套普适的数学物理框架，用于描述和预测固体、流体等可变形物质在外力、温度变化或其他物理作用下的力学行为。从板块构造的宏伟尺度到生物细胞的微观世界，其原理无处不在，是众多现代科学与工程领域（如地球物理学、材料科学、生物力学和计算力学）的理论基石。然而，其深刻的数学内涵与抽象的概念体系，如张量分析和多构型描述，往往给初学者带来挑战，造成了理论与应用之间的知识鸿沟。

本文旨在系统性地梳理连续介质力学的核心概念与基本定律，为读者构建一个坚实且连贯的知识体系。我们首先将在“原理与机制”一章中，详细阐述描述变形的运动学语言、量化内力的动力学概念，以及支配物质行为的质量、动量和能量守恒定律，并讨论构建材料本构关系所必须遵循的普适原则。接着，在“应用与交叉学科联系”一章中，我们将展示这些看似抽象的理论如何具体地应用于解决地球物理、材料工程及生物力学等前沿领域的实际问题。最后，“动手实践”部分将提供一系列精心设计的练习，帮助读者将理论知识转化为解决问题的能力。通过这一结构化的学习路径，读者将能够深刻理解连续介质力学的精髓，并有能力将其作为强大工具应用于自己的研究领域。

## 原理与机制

本章旨在系统性地阐述连续介质力学的核心原理与机制。我们将从运动学（即对变形和运动的数学描述）出发，接着探讨动力学（即力与应力的概念），然后介绍支配这些过程的基本守恒定律，最后讨论建立材料本构模型所必须遵循的普适性原则。

### 运动学：变形与运动的描述

运动学是描述物体如何运动和变形的几何语言，而不涉及引起这些运动的力。

#### 参考构型、当前构型与物质点描述

为了描述一个可变形物体（或称**连续体**）的运动，我们首先需要一个参照系。我们选择一个特定的时刻（通常是初始时刻 $t=0$）下物体所占据的空间区域，称之为**参考构型**，记作 $\mathcal{B}_0$。在此构型中，连续体内的每一个物质点都可以通过其位置向量 $\boldsymbol{X}$ 进行唯一的标记。因此，$\boldsymbol{X}$ 可被视为该物质点的“标签”。

随着时间的推移，物体会运动和变形。在任意时刻 $t$，物体所占据的空间区域被称为**当前构型**，记作 $\mathcal{B}_t$。物质点 $\boldsymbol{X}$ 在时刻 $t$ 的空间位置由向量 $\boldsymbol{x}$ 给出。连接这两种描述的是**运动映射** $\boldsymbol{\varphi}$：
$$
\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t)
$$
这个映射描述了每个物质点 $\boldsymbol{X}$ 在所有时刻 $t$ 的运动轨迹。为了保证物理上的合理性，我们要求映射 $\boldsymbol{\varphi}$ 具备良好的数学性质：它必须是连续可微的，并且是双射（一一对应），以确保物质不会凭空消失或相互穿透。此外，它的逆映射 $\boldsymbol{\varphi}^{-1}$ 也必须是光滑的。这些性质共同要求运动映射是一个**微分同胚** [@problem_id:3440092]。

在连续介质力学中，任何物理量（如温度或密度）都可以通过两种方式来描述。**物质描述**（或拉格朗日描述）将物理量视为物质点 $\boldsymbol{X}$ 和时间 $t$ 的函数，例如温度场 $T(\boldsymbol{X}, t)$。而**空间描述**（或欧拉描述）则将该物理量视为空间点 $\boldsymbol{x}$ 和时间 $t$ 的函数，例如 $\hat{T}(\boldsymbol{x}, t)$。这两种描述通过运动映射联系在一起：$\hat{T}(\boldsymbol{\varphi}(\boldsymbol{X}, t), t) = T(\boldsymbol{X}, t)$。

当我们想知道某个特定物质点所经历的物理量变化率时，我们需要计算该物理量跟随物质点运动时的全时间导数，这被称为**物质导数** (material derivative)，记为 $D/Dt$ 或 $\dot{(\cdot)}$。对一个以空间形式表示的标量场 $\phi(\boldsymbol{x}, t)$，利用链式法则，其物质导数可以表达为：
$$
\frac{D\phi}{Dt} = \frac{\partial \phi}{\partial t} + (\nabla \phi) \cdot \boldsymbol{v}
$$
其中 $\boldsymbol{v}(\boldsymbol{x}, t)$ 是物质点在空间位置 $\boldsymbol{x}$ 处的速度场，$\nabla$ 是对空间坐标 $\boldsymbol{x}$ 的梯度算子。上式等号右边的第一项 $\partial \phi / \partial t$ 是**局部变化率**，表示在一个固定的空间点上物理量的变化快慢。第二项 $(\nabla \phi) \cdot \boldsymbol{v}$ 是**迁移项**（或对流项），表示由于物质点运动到具有不同物理量值的新位置而引起的变化 [@problem_id:3581547]。物质导数是连接拉格朗日和欧拉描述的关键桥梁。

#### 变形梯度

**变形梯度** (deformation gradient) 张量 $\mathbf{F}$ 是连续介质力学的核心运动学量，它量化了物质点的局部变形。它被定义为运动映射 $\boldsymbol{\varphi}$ 对参考坐标 $\boldsymbol{X}$ 的梯度：
$$
\mathbf{F}(\boldsymbol{X}, t) = \nabla_{\boldsymbol{X}} \boldsymbol{\varphi}(\boldsymbol{X}, t) \quad \text{or} \quad F_{ij} = \frac{\partial x_i}{\partial X_j}
$$
$\mathbf{F}$ 的基本物理意义在于，它将参考构型中的一个无穷小矢量元 $d\boldsymbol{X}$ 线性映射到当前构型中的对应矢量元 $d\boldsymbol{x}$ [@problem_id:3440088]：
$$
d\boldsymbol{x} = \mathbf{F} d\boldsymbol{X}
$$
$\mathbf{F}$ 的行列式，记为 $J = \det \mathbf{F}$，被称为雅可比行列式。它表示了局部的体积变化率，即当前构型中的一个无穷小体积元 $dv$ 与参考构型中的对应体积元 $dV$ 之间的关系 [@problem_id:3440092]：
$$
dv = J dV
$$
为了保证物质不会被压缩到零体积或发生“内外翻转”的非物理变形，我们必须要求 $J > 0$。这个条件保证了运动映射的局部**可逆性**。此外，要使变形梯度场 $\mathbf{F}$ 能够对应于一个连续、单值的位移场，它必须满足**协调性**条件，数学上表示为其旋度为零：$\text{Curl}\,\mathbf{F} = \mathbf{0}$ [@problem_id:3440088]。

在不同构型之间转换场量时，我们会用到**推前** (push-forward) 和**拉回** (pull-back) 操作。例如，一个附着在物质上的矢量场 $\boldsymbol{V}(\boldsymbol{X})$ 会被变形梯度推前为空间矢量场 $\boldsymbol{v}(\boldsymbol{x}) = \mathbf{F}\boldsymbol{V}$。反之，一个空间协矢量场（例如某个标量场的梯度）$\boldsymbol{a}(\boldsymbol{x})$ 会被拉回到参考构型，成为物质协矢量场 $\boldsymbol{A}(\boldsymbol{X}) = \mathbf{F}^{\mathsf{T}}\boldsymbol{a}$ [@problem_id:3440092]。这些变换规则是张量分析在连续介质力学中的具体体现。

#### 变形的分解：拉伸与旋转

变形梯度 $\mathbf{F}$ 同时包含了物体的局部拉伸和旋转信息。通过**极分解定理** (polar decomposition theorem)，我们可以将 $\mathbf{F}$唯一地分解为一个纯旋转和一个纯拉伸的组合 [@problem_id:3440100]：
$$
\mathbf{F} = \mathbf{R}\mathbf{U} = \mathbf{V}\mathbf{R}
$$
这里，$\mathbf{R}$ 是一个旋转张量（$\mathbf{R}^{\mathsf{T}}\mathbf{R}=\mathbf{I}, \det\mathbf{R}=1$）。$\mathbf{U}$ 和 $\mathbf{V}$ 都是对称正定的拉伸张量，分别称为**右拉伸张量**和**左拉伸张量**。$\mathbf{U}$ 描述了在参考构型坐标系下的拉伸，而 $\mathbf{V}$ 则描述了在当前构型坐标系下的拉伸。

为了得到一个只反映拉伸而不包含旋转的应变度量，我们定义了两个重要的张量：
- **右柯西-格林张量** (Right Cauchy-Green tensor): $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = \mathbf{U}^2$
- **左柯西-格林张量** (Left Cauchy-Green tensor): $\mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}} = \mathbf{V}^2$

$\mathbf{C}$ 是一个完全定义在参考构型上的张量，它度量了物质线段长度的平方变化。由于 $\mathbf{C}$ 的定义中不显含旋转张量 $\mathbf{R}$，它是一个“纯粹”的应变度量。$\mathbf{C}$ 和 $\mathbf{B}$ 的特征值相同，等于主拉伸比的平方，但它们的特征向量（主拉伸方向）通常不同，分别定义在参考构型和当前构型中，并通过旋转张量 $\mathbf{R}$ 联系 [@problem_id:3440100]。

#### 运动速率：速度梯度、变形率与自旋

将注意力转向变形的速率，我们考察空间速度场 $\boldsymbol{v}(\boldsymbol{x}, t)$。**速度梯度张量** $\mathbf{l}$ 定义为速度场对空间坐标的梯度：
$$
\mathbf{l} = \nabla_{\boldsymbol{x}}\boldsymbol{v} \quad \text{or} \quad l_{ij} = \frac{\partial v_i}{\partial x_j}
$$
它描述了邻近物质点之间的相对速度。$\mathbf{l}$ 可以唯一地分解为其对称部分和反对称部分 [@problem_id:3581544]：
$$
\mathbf{l} = \mathbf{D} + \mathbf{W}
$$
其中，
- **变形率张量** (rate-of-deformation tensor) $\mathbf{D} = \frac{1}{2}(\mathbf{l} + \mathbf{l}^{\mathsf{T}})$ 是对称的。它描述了物质线元长度的瞬时变化率。一个物质线元 $d\boldsymbol{x}$ 的长度平方的变化率为 $\frac{d}{dt} \|d\boldsymbol{x}\|^2 = 2 d\boldsymbol{x} \cdot \mathbf{D} d\boldsymbol{x}$。
- **自旋张量** (spin tensor) $\mathbf{W} = \frac{1}{2}(\mathbf{l} - \mathbf{l}^{\mathsf{T}})$ 是反对称的。它描述了物质的瞬时刚体转动速率，并与速度场的旋度（涡度）密切相关：$\mathbf{W}$ 的轴矢量为 $\frac{1}{2}(\nabla \times \boldsymbol{v})$。

这种分解至关重要，因为它将变形的速率（由 $\mathbf{D}$ 度量）与纯刚体转动速率（由 $\mathbf{W}$ 度量）分离开来。

### 动力学：力与应力的概念

动力学研究引起物体运动的力。连续体中的力分为两类：作用于整个体积的**体力**（如重力）和作用于物体表面的**面力**（或称**traction**）。

#### 牵引力与柯西应力

考虑连续体内部一个假想的切割面，其单位法向量为 $\mathbf{n}$。面的一侧对另一侧的作用力，除以该面的面积，取极限即得到**牵引力矢量** (traction vector) $\mathbf{t}(\mathbf{n})$。

**柯西应力定理** (Cauchy's stress theorem) 是动力学的一个基石。它指出，对于一个给定的物质点，牵引力矢量 $\mathbf{t}$ 与该点处的表面法向量 $\mathbf{n}$ 之间存在线性关系。这种线性关系可以通过一个二阶张量来表示，即**柯西应力张量** (Cauchy stress tensor) $\boldsymbol{\sigma}$ [@problem_id:3440162]：
$$
\mathbf{t}(\mathbf{x}, t, \mathbf{n}) = \boldsymbol{\sigma}(\mathbf{x}, t) \mathbf{n}
$$
柯西应力张量 $\boldsymbol{\sigma}$ 完全描述了物质点处的应力状态。它是一个定义在**当前构型**中的空间张量。动量矩守恒定律进一步要求（在没有体力矩的情况下）柯西应力张量必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$。

#### 有限变形中的其他应力度量

在处理大变形问题时，直接在随时间变化的当前构型上进行计算可能很复杂。因此，通常将问题转化到固定的参考构型上进行求解。这催生了其他应力度量的定义。

我们定义**名义牵引力** (nominal traction) $\mathbf{T}$ 为作用在变形后物体上的力除以**参考构型**中的初始面积。名义牵引力与柯西牵引力的关系是 $d\mathbf{f} = \mathbf{t} \, da = \mathbf{T} \, dA$，其中 $d\mathbf{f}$ 是作用在面元上的力。

**第一皮奥拉-基尔霍夫应力张量** (First Piola-Kirchhoff stress tensor, PK1) $\mathbf{P}$ 被定义为将参考构型中的法向量 $\mathbf{N}$ 映射到名义牵引力 $\mathbf{T}$ 的张量 [@problem_id:3440101]：
$$
\mathbf{T} = \mathbf{P}\mathbf{N}
$$
$\mathbf{P}$ 是一个“两点”张量，它将参考构型中的一个方向（$\mathbf{N}$）与当前构型中的一个力（包含在 $\mathbf{T}$ 中）联系起来。它通常是非对称的。$\mathbf{P}$ 和 $\boldsymbol{\sigma}$ 之间的关系可以通过**Nanson 公式** ($\mathbf{n}da = J\mathbf{F}^{-\mathsf{T}}\mathbf{N}dA$) 推导得出：
$$
\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-\mathsf{T}}
$$
**第二皮奥拉-基尔霍夫应力张量** (Second Piola-Kirchhoff stress tensor, PK2) $\mathbf{S}$ 是一个完全定义在参考构型上的对称张量，它通过以下关系与 $\mathbf{P}$ 联系：
$$
\mathbf{P} = \mathbf{F}\mathbf{S} \quad \text{or} \quad \mathbf{S} = \mathbf{F}^{-1}\mathbf{P}
$$
$\mathbf{S}$ 的一个重要特性是它与格林-拉格朗日应变张量 $\mathbf{E} = \frac{1}{2}(\mathbf{C}-\mathbf{I})$ 在能量上是共轭的。它与柯西应力的关系为：
$$
\boldsymbol{\sigma} = \frac{1}{J} \mathbf{F} \mathbf{S} \mathbf{F}^{\mathsf{T}}
$$
这个关系被称为**推前** (push-forward) 操作，它将物质应力张量 $\mathbf{S}$ 映射为空间应力张量 $\boldsymbol{\sigma}$。此外，**基尔霍夫应力张量** $\boldsymbol{\tau} = J\boldsymbol{\sigma}$ 也常被用作一个中间量，因为它与 PK2 应力有更简洁的推前关系 $\boldsymbol{\tau} = \mathbf{F}\mathbf{S}\mathbf{F}^{\mathsf{T}}$ [@problem_id:3440101]。

### 基本原理与守恒定律

物理定律以守恒律的形式出现，它们构成了控制连续介质行为的控制方程。

#### 质量守恒

质量守恒原理指出，一个物质体的总质量不随时间改变。对于任意物质体积 $\mathcal{V}_0$，其质量为 $\int_{\mathcal{V}_0} \rho_0 dV$。在时刻 $t$，这个物质体积占据了空间体积 $\mathcal{V}_t = \boldsymbol{\varphi}(\mathcal{V}_0)$，其质量为 $\int_{\mathcal{V}_t} \rho dv$。二者必须相等。利用体积变换关系 $dv = J dV$，我们可以得到点wise的**物质形式**的质量守恒方程 [@problem_id:3440092]：
$$
\rho_0(\boldsymbol{X}) = J(\boldsymbol{X}, t) \rho(\boldsymbol{\varphi}(\boldsymbol{X}, t), t)
$$
对其应用物质导数，并结合雷诺输运定理，可得到等价的**空间形式**（连续性方程）：
$$
\frac{D\rho}{Dt} + \rho (\nabla \cdot \boldsymbol{v}) = 0 \quad \text{or} \quad \dot{\rho} + \rho\,\text{tr}(\mathbf{D}) = 0
$$

#### 动量守恒与虚功原理

牛顿第二定律应用于连续体，形成了动量守恒定律。其**局部（强）形式**，也称为柯西运动方程，在参考构型中表示为：
$$
\text{Div}(\mathbf{P}) + \rho_0 \mathbf{b} = \rho_0 \ddot{\mathbf{u}}
$$
其中 $\ddot{\mathbf{u}}$ 是物质加速度，$\text{Div}$ 是对参考坐标的散度。在忽略惯性项的**准静态**情况下（$\ddot{\mathbf{u}} \approx \mathbf{0}$），此方程简化为平衡方程：$\text{Div}(\mathbf{P}) + \rho_0 \mathbf{b} = \mathbf{0}$。

直接求解这个偏微分方程组（强形式）可能很困难。一种更强大且适用于数值方法（如有限元法）的替代方案是**虚功原理** (principle of virtual work)，即方程的**弱形式**。通过将平衡方程乘以一个满足位移边界条件的任意**虚位移**场 $\delta\mathbf{u}$，并在整个体积上积分，再利用分部积分法，我们得到 [@problem_id:3440158]：
$$
\underbrace{\int_{\mathcal{B}_0} \mathbf{P} : \delta \mathbf{F} \, dV}_{\text{Internal Virtual Work}} = \underbrace{\int_{\mathcal{B}_0} \rho_0 \mathbf{b} \cdot \delta \mathbf{u} \, dV + \int_{\partial_t \mathcal{B}_0} \bar{\mathbf{T}} \cdot \delta \mathbf{u} \, dA}_{\text{External Virtual Work}}
$$
其中 $\delta\mathbf{F} = \nabla_0 \delta\mathbf{u}$ 是虚变形梯度，$\bar{\mathbf{T}}$ 是在力的边界 $\partial_t\mathcal{B}_0$ 上施加的名义牵引力。这个方程的物理意义是：对于任何满足约束的虚位移，内力所做的虚功必须等于外力所做的虚功。

#### 热力学定律

对于热力耦合问题，热力学定律是不可或缺的。
**第一定律（能量守恒）**的局部形式为 [@problem_id:3440099]：
$$
\rho \dot{e} = \boldsymbol{\sigma}:\mathbf{D} - \nabla \cdot \mathbf{q} + \rho r
$$
该方程表明，单位质量内能 $e$ 的变化率（$\rho\dot{e}$）等于应力所做的功率（**应力功率** $\boldsymbol{\sigma}:\mathbf{D}$），减去热量流失（**热通量** $\mathbf{q}$ 的散度），加上内部热源 $r$ 的供给。注意，由于柯西应力是对称的，应力功率只与变形率张量 $\mathbf{D}$ 有关，而与自旋张量 $\mathbf{W}$ 无关。

**第二定律（熵增原理）**以 Clausius-Duhem 不等式的形式，对材料的本构关系施加了基本约束。其局部形式为 [@problem_id:3440099]：
$$
\rho \dot{\eta} + \nabla \cdot \left(\frac{\mathbf{q}}{\theta}\right) - \frac{\rho r}{\theta} \ge 0
$$
其中 $\eta$ 是单位质量的熵，$\theta$ 是绝对温度。该不等式表明，总的熵产生率（左侧项）必须是非负的。这一原理是推导耗散材料（如塑性或粘性材料）本构关系的基础。

### 本构模型构建原则

本构方程描述特定材料的力学行为（例如，应力与应变的关系）。为了确保物理上的合理性，任何本构模型都必须遵循一些普适原则。

#### 客观性原理

**客观性原理** (Principle of Objectivity) 或称**标架无关性** (frame-indifference) 要求物理定律（特别是本构关系）的形式不应依赖于观察者。一个观察者的变换可以被看作是一个叠加的刚体运动：$\mathbf{x}^* = \mathbf{c}(t) + \mathbf{Q}(t)\mathbf{x}$，其中 $\mathbf{c}(t)$ 是平移，$\mathbf{Q}(t)$ 是一个时间依赖的旋转。

在此变换下，运动学和动力学量会相应地变换，例如：
$$
\mathbf{F}^* = \mathbf{Q}\mathbf{F} \quad \text{and} \quad \boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^{\mathsf{T}}
$$
客观性要求一个本构关系（例如 $\boldsymbol{\sigma} = \mathbf{f}(\mathbf{F})$）必须满足以下条件 [@problem_id:3440114]：
$$
\mathbf{f}(\mathbf{Q}\mathbf{F}) = \mathbf{Q}\mathbf{f}(\mathbf{F})\mathbf{Q}^{\mathsf{T}}
$$
这意味着本构定律必须与刚体运动解耦。使用纯粹的物质张量（如 $\mathbf{C}$ 或 $\mathbf{S}$）来构建本构关系是确保客观性的一种有效途径，因为这些量本身在叠加刚体运动下是不变的。

#### 材料对称性

**材料对称性** (material symmetry) 是材料本身的内在属性，与观察者无关。它描述了材料在参考构型中旋转后，其力学响应是否保持不变。

例如，对于一个弹性材料，其响应由应变能函数 $W(\mathbf{F})$ 决定。如果对于任意旋转 $\mathbf{Q}_0$，都有 $W(\mathbf{F}) = W(\mathbf{F}\mathbf{Q}_0)$ 成立，那么该材料是**各向同性**的 (isotropic)。这意味着材料内部没有“优先”方向。客观性涉及对变形梯度 $\mathbf{F}$ 的**左乘**旋转（$\mathbf{Q}\mathbf{F}$），代表观察者的变换；而材料对称性则涉及**右乘**旋转（$\mathbf{F}\mathbf{Q}_0$），代表材料自身的旋转 [@problem_id:3440114]。这两个概念必须严格区分。

#### 材料约束：不可压缩性

许多材料（如橡胶、水）在很大程度上是**不可压缩**的 (incompressible)。这意味着它们的体积在变形过程中保持不变。这个**运动学约束**可以用数学语言表达为：
$$
J = \det \mathbf{F} = 1
$$
对于受此约束的材料，其应力响应不能完全由变形决定。为了处理这种约束，我们采用**拉格朗日乘子法**。通过引入一个称为**拉格朗日乘子**的标量场 $p$，我们将约束项加入到能量泛函中，例如，总势能写为 $\Pi = \int (W_{\text{iso}}({\mathbf{F}}) - p(J-1)) dV_0$。

通过对这个增广泛函进行变分，我们发现拉格朗日乘子 $p$ 以静水压力的形式出现在柯西应力张量中 [@problem_id:3440094]：
$$
\boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\sigma}^{\text{dev}}
$$
其中 $\boldsymbol{\sigma}^{\text{dev}}$ 是由应变能函数 $W_{\text{iso}}$ 决定的**偏应力**（traceless part），而 $-p\mathbf{I}$ 是纯静水应力。这里的压力 $p$ 并不是由变形直接确定的，而是一个独立的场变量，它会调整自身的值以维持 $J=1$ 的约束。除非在边界上给定压力值，否则压力场 $p$ 通常只能确定到一个任意的常数，即它是**不确定的** (indeterminate) [@problem_id:3440094]。