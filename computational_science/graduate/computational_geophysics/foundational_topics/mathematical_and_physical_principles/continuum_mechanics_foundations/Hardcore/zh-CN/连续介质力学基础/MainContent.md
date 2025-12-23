## 引言
连续介质力学是一门基础性的理论学科，它提供了一套普适的[数学物理](@entry_id:265403)框架，用于描述和预测固体、流体等可变形物质在外力、温度变化或其他物理作用下的力学行为。从板块构造的宏伟尺度到生物细胞的微观世界，其原理无处不在，是众多现代科学与工程领域（如[地球物理学](@entry_id:147342)、[材料科学](@entry_id:152226)、[生物力学](@entry_id:153973)和[计算力学](@entry_id:174464)）的理论基石。然而，其深刻的数学内涵与抽象的概念体系，如[张量分析](@entry_id:161423)和多构型描述，往往给初学者带来挑战，造成了理论与应用之间的知识鸿沟。

本文旨在系统性地梳理连续介质力学的核心概念与基本定律，为读者构建一个坚实且连贯的知识体系。我们首先将在“原理与机制”一章中，详细阐述描述变形的运动学语言、量化[内力](@entry_id:167605)的动力学概念，以及支配物质行为的质量、动量和[能量守恒](@entry_id:140514)定律，并讨论构建材料[本构关系](@entry_id:186508)所必须遵循的普适原则。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些看似抽象的理论如何具体地应用于解决地球物理、材料工程及[生物力学](@entry_id:153973)等前沿领域的实际问题。最后，“动手实践”部分将提供一系列精心设计的练习，帮助读者将理论知识转化为解决问题的能力。通过这一结构化的学习路径，读者将能够深刻理解连续介质力学的精髓，并有能力将其作为强大工具应用于自己的研究领域。

## 原理与机制

本章旨在系统性地阐述连续介质力学的核心原理与机制。我们将从[运动学](@entry_id:173318)（即对变形和运动的数学描述）出发，接着探讨动力学（即力与应力的概念），然后介绍支配这些过程的基本[守恒定律](@entry_id:269268)，最后讨论建立材料[本构模型](@entry_id:174726)所必须遵循的普适性原则。

### [运动学](@entry_id:173318)：变形与运动的描述

[运动学](@entry_id:173318)是描述物体如何运动和变形的几何语言，而不涉及引起这些运动的力。

#### 参考构型、当前构型与物质点描述

为了描述一个可变形物体（或称**连续体**）的运动，我们首先需要一个参照系。我们选择一个特定的时刻（通常是初始时刻 $t=0$）下物体所占据的空间区域，称之为**参考构型**，记作 $\mathcal{B}_0$。在此构型中，连续体内的每一个物[质点](@entry_id:186768)都可以通过其位置向量 $\boldsymbol{X}$ 进行唯一的标记。因此，$\boldsymbol{X}$ 可被视为该物[质点](@entry_id:186768)的“标签”。

随着时间的推移，物体会运动和变形。在任意时刻 $t$，物体所占据的空间区域被称为**当前构型**，记作 $\mathcal{B}_t$。物质点 $\boldsymbol{X}$ 在时刻 $t$ 的空间位置由向量 $\boldsymbol{x}$ 给出。连接这两种描述的是**运动映射** $\boldsymbol{\varphi}$：
$$
\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t)
$$
这个映射描述了每个物[质点](@entry_id:186768) $\boldsymbol{X}$ 在所有时刻 $t$ 的运动轨迹。为了保证物理上的合理性，我们要求映射 $\boldsymbol{\varphi}$ 具备良好的数学性质：它必须是连续可微的，并且是[双射](@entry_id:138092)（一一对应），以确保物质不会凭空消失或相互穿透。此外，它的逆映射 $\boldsymbol{\varphi}^{-1}$ 也必须是光滑的。这些性质共同要求运动映射是一个**微分同胚** 。

在连续介质力学中，任何物理量（如温度或密度）都可以通过两种方式来描述。**物质描述**（或[拉格朗日描述](@entry_id:264498)）将物理量视为物[质点](@entry_id:186768) $\boldsymbol{X}$ 和时间 $t$ 的函数，例如温度场 $T(\boldsymbol{X}, t)$。而**空间描述**（或[欧拉描述](@entry_id:264722)）则将该物理量视为空间点 $\boldsymbol{x}$ 和时间 $t$ 的函数，例如 $\hat{T}(\boldsymbol{x}, t)$。这两种描述通过运动映射联系在一起：$\hat{T}(\boldsymbol{\varphi}(\boldsymbol{X}, t), t) = T(\boldsymbol{X}, t)$。

当我们想知道某个特定物质点所经历的物理量变化率时，我们需要计算该物理量跟随物质点运动时的[全时间导数](@entry_id:172646)，这被称为**物质导数** (material derivative)，记为 $D/Dt$ 或 $\dot{(\cdot)}$。对一个以[空间形式](@entry_id:186145)表示的标量场 $\phi(\boldsymbol{x}, t)$，利用[链式法则](@entry_id:190743)，其[物质导数](@entry_id:172646)可以表达为：
$$
\frac{D\phi}{Dt} = \frac{\partial \phi}{\partial t} + (\nabla \phi) \cdot \boldsymbol{v}
$$
其中 $\boldsymbol{v}(\boldsymbol{x}, t)$ 是物[质点](@entry_id:186768)在空间位置 $\boldsymbol{x}$ 处的速度场，$\nabla$ 是对空间坐标 $\boldsymbol{x}$ 的[梯度算子](@entry_id:275922)。上式等号右边的第一项 $\partial \phi / \partial t$ 是**[局部变化率](@entry_id:264961)**，表示在一个固定的空间点上物理量的变化快慢。第二项 $(\nabla \phi) \cdot \boldsymbol{v}$ 是**迁移项**（或[对流](@entry_id:141806)项），表示由于物[质点](@entry_id:186768)运动到具有不同物理量值的新位置而引起的变化 。[物质导数](@entry_id:172646)是连接拉格朗日和[欧拉描述](@entry_id:264722)的关键桥梁。

#### 变形梯度

**变形梯度** (deformation gradient) 张量 $\mathbf{F}$ 是连续介质力学的核心运动学量，它量化了物质点的局部变形。它被定义为运动映射 $\boldsymbol{\varphi}$ 对参考坐标 $\boldsymbol{X}$ 的梯度：
$$
\mathbf{F}(\boldsymbol{X}, t) = \nabla_{\boldsymbol{X}} \boldsymbol{\varphi}(\boldsymbol{X}, t) \quad \text{or} \quad F_{ij} = \frac{\partial x_i}{\partial X_j}
$$
$\mathbf{F}$ 的基本物理意义在于，它将参考构型中的一个无穷小矢量元 $d\boldsymbol{X}$ 线性映射到当前构型中的对应矢量元 $d\boldsymbol{x}$ ：
$$
d\boldsymbol{x} = \mathbf{F} d\boldsymbol{X}
$$
$\mathbf{F}$ 的[行列式](@entry_id:142978)，记为 $J = \det \mathbf{F}$，被称为雅可比行列式。它表示了局部的体积变化率，即当前构型中的一个无穷小体积元 $dv$ 与参考构型中的对应[体积元](@entry_id:267802) $dV$ 之间的关系 ：
$$
dv = J dV
$$
为了保证物质不会被压缩到零体积或发生“内外翻转”的非物理变形，我们必须要求 $J > 0$。这个条件保证了运动映射的局部**可逆性**。此外，要使变形梯度场 $\mathbf{F}$ 能够对应于一个连续、单值的位移场，它必须满足**协调性**条件，数学上表示为其旋度为零：$\text{Curl}\,\mathbf{F} = \mathbf{0}$ 。

在不同构型之间转换场量时，我们会用到**推前** (push-forward) 和**[拉回](@entry_id:160816)** (pull-back) 操作。例如，一个附着在物质上的矢量场 $\boldsymbol{V}(\boldsymbol{X})$ 会被变形梯度推前为空间矢量场 $\boldsymbol{v}(\boldsymbol{x}) = \mathbf{F}\boldsymbol{V}$。反之，一个空间协矢量场（例如某个[标量场的梯度](@entry_id:270765)）$\boldsymbol{a}(\boldsymbol{x})$ 会被[拉回](@entry_id:160816)到参考构型，成为物质协矢量场 $\boldsymbol{A}(\boldsymbol{X}) = \mathbf{F}^{\mathsf{T}}\boldsymbol{a}$ 。这些变换规则是[张量分析](@entry_id:161423)在[连续介质力学](@entry_id:155125)中的具体体现。

#### 变形的分解：[拉伸与旋转](@entry_id:150197)

变形梯度 $\mathbf{F}$ 同时包含了物体的局部拉伸和旋转信息。通过**极分解定理** (polar decomposition theorem)，我们可以将 $\mathbf{F}$唯一地分解为一个纯旋转和一个纯拉伸的组合 ：
$$
\mathbf{F} = \mathbf{R}\mathbf{U} = \mathbf{V}\mathbf{R}
$$
这里，$\mathbf{R}$ 是一个[旋转张量](@entry_id:191990)（$\mathbf{R}^{\mathsf{T}}\mathbf{R}=\mathbf{I}, \det\mathbf{R}=1$）。$\mathbf{U}$ 和 $\mathbf{V}$ 都是[对称正定](@entry_id:145886)的[拉伸张量](@entry_id:193200)，分别称为**右[拉伸张量](@entry_id:193200)**和**左[拉伸张量](@entry_id:193200)**。$\mathbf{U}$ 描述了在参考构型[坐标系](@entry_id:156346)下的拉伸，而 $\mathbf{V}$ 则描述了在当前构型[坐标系](@entry_id:156346)下的拉伸。

为了得到一个只反映拉伸而不包含旋转的[应变度量](@entry_id:755495)，我们定义了两个重要的张量：
- **[右柯西-格林张量](@entry_id:174156)** (Right Cauchy-Green tensor): $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = \mathbf{U}^2$
- **[左柯西-格林张量](@entry_id:186163)** (Left Cauchy-Green tensor): $\mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}} = \mathbf{V}^2$

$\mathbf{C}$ 是一个完全定义在参考构型上的张量，它度量了物质线段长度的平方变化。由于 $\mathbf{C}$ 的定义中不显含[旋转张量](@entry_id:191990) $\mathbf{R}$，它是一个“纯粹”的[应变度量](@entry_id:755495)。$\mathbf{C}$ 和 $\mathbf{B}$ 的[特征值](@entry_id:154894)相同，等于主拉伸比的平方，但它们的[特征向量](@entry_id:151813)（主拉伸方向）通常不同，分别定义在参考构型和当前构型中，并通过[旋转张量](@entry_id:191990) $\mathbf{R}$ 联系 。

#### 运动速率：[速度梯度](@entry_id:261686)、变形率与自旋

将注意力转向变形的速率，我们考察[空间速度](@entry_id:190294)场 $\boldsymbol{v}(\boldsymbol{x}, t)$。**[速度梯度张量](@entry_id:270928)** $\mathbf{l}$ 定义为[速度场](@entry_id:271461)对空间坐标的梯度：
$$
\mathbf{l} = \nabla_{\boldsymbol{x}}\boldsymbol{v} \quad \text{or} \quad l_{ij} = \frac{\partial v_i}{\partial x_j}
$$
它描述了邻近物质点之间的[相对速度](@entry_id:178060)。$\mathbf{l}$ 可以唯一地分解为其对称部分和反对称部分 ：
$$
\mathbf{l} = \mathbf{D} + \mathbf{W}
$$
其中，
- **变形率张量** (rate-of-deformation tensor) $\mathbf{D} = \frac{1}{2}(\mathbf{l} + \mathbf{l}^{\mathsf{T}})$ 是对称的。它描述了物质[线元](@entry_id:196833)长度的[瞬时变化率](@entry_id:141382)。一个物质线元 $d\boldsymbol{x}$ 的长度平方的变化率为 $\frac{d}{dt} \|d\boldsymbol{x}\|^2 = 2 d\boldsymbol{x} \cdot \mathbf{D} d\boldsymbol{x}$。
- **[自旋张量](@entry_id:187346)** (spin tensor) $\mathbf{W} = \frac{1}{2}(\mathbf{l} - \mathbf{l}^{\mathsf{T}})$ 是反对称的。它描述了物质的瞬时[刚体转动](@entry_id:191086)速率，并与[速度场的旋度](@entry_id:183606)（涡度）密切相关：$\mathbf{W}$ 的[轴矢量](@entry_id:196296)为 $\frac{1}{2}(\nabla \times \boldsymbol{v})$。

这种分解至关重要，因为它将变形的速率（由 $\mathbf{D}$ 度量）与纯[刚体转动](@entry_id:191086)速率（由 $\mathbf{W}$ 度量）分离开来。

### 动力学：力与应力的概念

动力学研究引起物体运动的力。连续体中的力分为两类：作用于整个体积的**[体力](@entry_id:174230)**（如重力）和作用于物体表面的**面力**（或称**traction**）。

#### 牵[引力](@entry_id:175476)与柯西应力

考虑连续体内部一个假想的切割面，其[单位法向量](@entry_id:178851)为 $\mathbf{n}$。面的一侧对另一侧的作用力，除以该面的面积，取极限即得到**牵[引力](@entry_id:175476)矢量** (traction vector) $\mathbf{t}(\mathbf{n})$。

**柯西应力定理** (Cauchy's stress theorem) 是动力学的一个基石。它指出，对于一个给定的物[质点](@entry_id:186768)，牵[引力](@entry_id:175476)矢量 $\mathbf{t}$ 与该点处的表[面法向量](@entry_id:749211) $\mathbf{n}$ 之间存在[线性关系](@entry_id:267880)。这种线性关系可以通过一个二阶张量来表示，即**柯西应力张量** (Cauchy stress tensor) $\boldsymbol{\sigma}$ ：
$$
\mathbf{t}(\mathbf{x}, t, \mathbf{n}) = \boldsymbol{\sigma}(\mathbf{x}, t) \mathbf{n}
$$
柯西应力张量 $\boldsymbol{\sigma}$ 完全描述了物[质点](@entry_id:186768)处的应力状态。它是一个定义在**当前构型**中的[空间张量](@entry_id:185799)。动量矩[守恒定律](@entry_id:269268)进一步要求（在没有体力矩的情况下）柯西应力张量必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$。

#### 有限变形中的其他应力度量

在处理[大变形](@entry_id:167243)问题时，直接在随时间变化的当前构型上进行计算可能很复杂。因此，通常将问题转化到固定的参考构型上进行求解。这催生了其他应力度量的定义。

我们定义**名义牵[引力](@entry_id:175476)** (nominal traction) $\mathbf{T}$ 为作用在变形后物体上的力除以**参考构型**中的初始面积。名义牵[引力](@entry_id:175476)与柯西牵[引力](@entry_id:175476)的关系是 $d\mathbf{f} = \mathbf{t} \, da = \mathbf{T} \, dA$，其中 $d\mathbf{f}$ 是作用在面元上的力。

**[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量** (First Piola-Kirchhoff stress tensor, PK1) $\mathbf{P}$ 被定义为将参考构型中的[法向量](@entry_id:264185) $\mathbf{N}$ 映射到名义牵[引力](@entry_id:175476) $\mathbf{T}$ 的张量 ：
$$
\mathbf{T} = \mathbf{P}\mathbf{N}
$$
$\mathbf{P}$ 是一个“两点”张量，它将参考构型中的一个方向（$\mathbf{N}$）与当前构型中的一个力（包含在 $\mathbf{T}$ 中）联系起来。它通常是非对称的。$\mathbf{P}$ 和 $\boldsymbol{\sigma}$ 之间的关系可以通过**Nanson 公式** ($\mathbf{n}da = J\mathbf{F}^{-\mathsf{T}}\mathbf{N}dA$) 推导得出：
$$
\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-\mathsf{T}}
$$
**[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量** (Second Piola-Kirchhoff stress tensor, PK2) $\mathbf{S}$ 是一个完全定义在参考构型上的对称张量，它通过以下关系与 $\mathbf{P}$ 联系：
$$
\mathbf{P} = \mathbf{F}\mathbf{S} \quad \text{or} \quad \mathbf{S} = \mathbf{F}^{-1}\mathbf{P}
$$
$\mathbf{S}$ 的一个重要特性是它与[格林-拉格朗日应变张量](@entry_id:187745) $\mathbf{E} = \frac{1}{2}(\mathbf{C}-\mathbf{I})$ 在能量上是共轭的。它与柯西应力的关系为：
$$
\boldsymbol{\sigma} = \frac{1}{J} \mathbf{F} \mathbf{S} \mathbf{F}^{\mathsf{T}}
$$
这个关系被称为**推前** (push-forward) 操作，它将物质[应力张量](@entry_id:148973) $\mathbf{S}$ 映射为空间[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$。此外，**[基尔霍夫应力](@entry_id:751039)张量** $\boldsymbol{\tau} = J\boldsymbol{\sigma}$ 也常被用作一个中间量，因为它与 PK2 应力有更简洁的推前关系 $\boldsymbol{\tau} = \mathbf{F}\mathbf{S}\mathbf{F}^{\mathsf{T}}$ 。

### 基本原理与[守恒定律](@entry_id:269268)

物理定律以守恒律的形式出现，它们构成了控制连续介质行为的控制方程。

#### [质量守恒](@entry_id:204015)

[质量守恒](@entry_id:204015)原理指出，一个物质体的总质量不随时间改变。对于任意物质体积 $\mathcal{V}_0$，其质量为 $\int_{\mathcal{V}_0} \rho_0 dV$。在时刻 $t$，这个物质体积占据了空间体积 $\mathcal{V}_t = \boldsymbol{\varphi}(\mathcal{V}_0)$，其质量为 $\int_{\mathcal{V}_t} \rho dv$。二者必须相等。利用体积变换关系 $dv = J dV$，我们可以得到点wise的**物质形式**的质量守恒方程 ：
$$
\rho_0(\boldsymbol{X}) = J(\boldsymbol{X}, t) \rho(\boldsymbol{\varphi}(\boldsymbol{X}, t), t)
$$
对其应用[物质导数](@entry_id:172646)，并结合[雷诺输运定理](@entry_id:191217)，可得到等价的**[空间形式](@entry_id:186145)**（[连续性方程](@entry_id:195013)）：
$$
\frac{D\rho}{Dt} + \rho (\nabla \cdot \boldsymbol{v}) = 0 \quad \text{or} \quad \dot{\rho} + \rho\,\text{tr}(\mathbf{D}) = 0
$$

#### 动量守恒与虚功原理

牛顿第二定律应用于连续体，形成了动量守恒定律。其**局部（强）形式**，也称为[柯西运动方程](@entry_id:204126)，在参考构型中表示为：
$$
\text{Div}(\mathbf{P}) + \rho_0 \mathbf{b} = \rho_0 \ddot{\mathbf{u}}
$$
其中 $\ddot{\mathbf{u}}$ 是[物质加速度](@entry_id:270992)，$\text{Div}$ 是对参考坐标的散度。在忽略惯性项的**准静态**情况下（$\ddot{\mathbf{u}} \approx \mathbf{0}$），此方程简化为[平衡方程](@entry_id:172166)：$\text{Div}(\mathbf{P}) + \rho_0 \mathbf{b} = \mathbf{0}$。

直接求解这个[偏微分方程组](@entry_id:172573)（强形式）可能很困难。一种更强大且适用于数值方法（如[有限元法](@entry_id:749389)）的替代方案是**[虚功原理](@entry_id:138749)** (principle of virtual work)，即方程的**[弱形式](@entry_id:142897)**。通过将平衡方程乘以一个满足[位移边界条件](@entry_id:203261)的任意**[虚位移](@entry_id:168781)**场 $\delta\mathbf{u}$，并在整个体积上积分，再利用分部积分法，我们得到 ：
$$
\underbrace{\int_{\mathcal{B}_0} \mathbf{P} : \delta \mathbf{F} \, dV}_{\text{Internal Virtual Work}} = \underbrace{\int_{\mathcal{B}_0} \rho_0 \mathbf{b} \cdot \delta \mathbf{u} \, dV + \int_{\partial_t \mathcal{B}_0} \bar{\mathbf{T}} \cdot \delta \mathbf{u} \, dA}_{\text{External Virtual Work}}
$$
其中 $\delta\mathbf{F} = \nabla_0 \delta\mathbf{u}$ 是虚变形梯度，$\bar{\mathbf{T}}$ 是在力的边界 $\partial_t\mathcal{B}_0$ 上施加的名义牵[引力](@entry_id:175476)。这个方程的物理意义是：对于任何满足约束的[虚位移](@entry_id:168781)，内力所做的[虚功](@entry_id:176403)必须等于外力所做的[虚功](@entry_id:176403)。

#### [热力学定律](@entry_id:202285)

对于[热力耦合问题](@entry_id:186655)，[热力学定律](@entry_id:202285)是不可或缺的。
**第一定律（[能量守恒](@entry_id:140514)）**的局部形式为 ：
$$
\rho \dot{e} = \boldsymbol{\sigma}:\mathbf{D} - \nabla \cdot \mathbf{q} + \rho r
$$
该方程表明，单位质量内能 $e$ 的变化率（$\rho\dot{e}$）等于应力所做的功率（**[应力功率](@entry_id:182907)** $\boldsymbol{\sigma}:\mathbf{D}$），减去热量流失（**[热通量](@entry_id:138471)** $\mathbf{q}$ 的散度），加上内部热源 $r$ 的供给。注意，由于柯西应力是对称的，[应力功率](@entry_id:182907)只与变形率张量 $\mathbf{D}$ 有关，而与[自旋张量](@entry_id:187346) $\mathbf{W}$ 无关。

**第二定律（[熵增原理](@entry_id:142282)）**以 Clausius-Duhem 不等式的形式，对材料的[本构关系](@entry_id:186508)施加了基本约束。其局部形式为 ：
$$
\rho \dot{\eta} + \nabla \cdot \left(\frac{\mathbf{q}}{\theta}\right) - \frac{\rho r}{\theta} \ge 0
$$
其中 $\eta$ 是单位质量的熵，$\theta$ 是绝对温度。该不等式表明，总的熵产生率（左侧项）必须是非负的。这一原理是推导耗散材料（如塑性或粘性材料）[本构关系](@entry_id:186508)的基础。

### 本构模型构建原则

[本构方程](@entry_id:138559)描述特定材料的力学行为（例如，应力与应变的关系）。为了确保物理上的合理性，任何本构模型都必须遵循一些普适原则。

#### [客观性原理](@entry_id:185412)

**[客观性原理](@entry_id:185412)** (Principle of Objectivity) 或称**标架无关性** (frame-indifference) 要求物理定律（特别是[本构关系](@entry_id:186508)）的形式不应依赖于观察者。一个观察者的变换可以被看作是一个叠加的[刚体运动](@entry_id:193355)：$\mathbf{x}^* = \mathbf{c}(t) + \mathbf{Q}(t)\mathbf{x}$，其中 $\mathbf{c}(t)$ 是平移，$\mathbf{Q}(t)$ 是一个时间依赖的旋转。

在此变换下，[运动学](@entry_id:173318)和动力学量会相应地变换，例如：
$$
\mathbf{F}^* = \mathbf{Q}\mathbf{F} \quad \text{and} \quad \boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^{\mathsf{T}}
$$
客观性要求一个本构关系（例如 $\boldsymbol{\sigma} = \mathbf{f}(\mathbf{F})$）必须满足以下条件 ：
$$
\mathbf{f}(\mathbf{Q}\mathbf{F}) = \mathbf{Q}\mathbf{f}(\mathbf{F})\mathbf{Q}^{\mathsf{T}}
$$
这意味着[本构定律](@entry_id:178936)必须与[刚体运动](@entry_id:193355)解耦。使用纯粹的物质张量（如 $\mathbf{C}$ 或 $\mathbf{S}$）来构建本构关系是确保客观性的一种有效途径，因为这些量本身在叠加[刚体运动](@entry_id:193355)下是不变的。

#### [材料对称性](@entry_id:190289)

**[材料对称性](@entry_id:190289)** (material symmetry) 是材料本身的内在属性，与观察者无关。它描述了材料在参考构型中旋转后，其力学响应是否保持不变。

例如，对于一个弹性材料，其响应由[应变能函数](@entry_id:178435) $W(\mathbf{F})$ 决定。如果对于任意旋转 $\mathbf{Q}_0$，都有 $W(\mathbf{F}) = W(\mathbf{F}\mathbf{Q}_0)$ 成立，那么该材料是**各向同性**的 (isotropic)。这意味着材料内部没有“优先”方向。客观性涉及对变形梯度 $\mathbf{F}$ 的**左乘**旋转（$\mathbf{Q}\mathbf{F}$），代表观察者的变换；而[材料对称性](@entry_id:190289)则涉及**右乘**旋转（$\mathbf{F}\mathbf{Q}_0$），代表材料自身的旋转 。这两个概念必须严格区分。

#### 材料约束：不可压缩性

许多材料（如橡胶、水）在很大程度上是**不可压缩**的 (incompressible)。这意味着它们的体积在变形过程中保持不变。这个**运动学约束**可以用数学语言表达为：
$$
J = \det \mathbf{F} = 1
$$
对于受此约束的材料，其应力响应不能完全由变形决定。为了处理这种约束，我们采用**[拉格朗日乘子法](@entry_id:176596)**。通过引入一个称为**[拉格朗日乘子](@entry_id:142696)**的标量场 $p$，我们将约束项加入到能量泛函中，例如，总[势能](@entry_id:748988)写为 $\Pi = \int (W_{\text{iso}}({\mathbf{F}}) - p(J-1)) dV_0$。

通过对这个增广泛函进行变分，我们发现拉格朗日乘子 $p$ 以[静水压力](@entry_id:275365)的形式出现在柯西[应力张量](@entry_id:148973)中 ：
$$
\boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\sigma}^{\text{dev}}
$$
其中 $\boldsymbol{\sigma}^{\text{dev}}$ 是由[应变能函数](@entry_id:178435) $W_{\text{iso}}$ 决定的**偏应力**（traceless part），而 $-p\mathbf{I}$ 是纯[静水应力](@entry_id:186327)。这里的压力 $p$ 并不是由变形直接确定的，而是一个独立的场变量，它会调整自身的值以维持 $J=1$ 的约束。除非在边界上给定压力值，否则压[力场](@entry_id:147325) $p$ 通常只能确定到一个任意的常数，即它是**不确定的** (indeterminate) 。