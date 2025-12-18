## 引言
[纳维-斯托克斯方程](@entry_id:142275)是描述流体运动的基石，其重要性贯穿于从工程设计到[行星科学](@entry_id:158926)的广阔领域。这组优雅的[偏微分](@entry_id:194612)方程统一地描述了流体[质点](@entry_id:186768)的加速度如何由压力梯度、粘性力以及外部体力共同决定。然而，其内在的[非线性](@entry_id:637147)特性使得解析求解异常困难，并催生了物理学中最后一个尚未完全解决的重大难题——[湍流](@entry_id:151300)。理解这组方程不仅是掌握流体力学的关键，也是开启对自然界和工程世界中无数复杂现象深刻洞察的钥匙。

本文旨在为读者提供一个关于[纳维-斯托克斯方程](@entry_id:142275)的全面而深入的视角，系统性地弥合基础理论与前沿应用之间的鸿沟。我们将带领您踏上一段从第一性原理到多样化应用的探索之旅：

- 在“**原理与机制**”一章中，我们将从最基本的[拉格朗日与欧拉描述](@entry_id:190556)出发，通过守恒定律和本构关系，一步步构建起完整的[纳维-斯托克斯方程](@entry_id:142275)。您将深入理解[非线性](@entry_id:637147)、压力约束和涡量动力学等核心机制的物理本质。
- 接着，在“**应用与交叉学科联系**”一章中，我们将展示这套方程的惊人普适性。您将看到它如何通过简化或扩展，被应用于从经典[管道流](@entry_id:189531)到磁流体动力学、地球大气科学乃至生物血液动力学等截然不同的领域。
- 最后，在“**动手实践**”部分，我们提供了一系列精心设计的思考题和练习，旨在巩固您对关键概念的理解，并初步接触解决这些方程的数值思想。

通过这三个章节的学习，您将不仅掌握[纳维-斯托克斯方程](@entry_id:142275)的数学形式，更能领会其背后的物理直觉和建模艺术，为您在[计算复杂流体](@entry_id:1122778)领域的研究奠定坚实的基础。

## 原理与机制

本章旨在深入剖析[纳维-斯托克斯方程](@entry_id:142275)的物理原理与数学机制。我们将从最基本的概念出发，逐步构建起描述流体运动的完整方程组，并探讨其各项的物理意义及其所带来的深刻影响，如[非线性](@entry_id:637147)、[湍流](@entry_id:151300)与涡量动力学。本章的推导与讨论将为后续章节中复杂的[计算模型](@entry_id:637456)与应用奠定坚实的理论基础。

### [拉格朗日与欧拉描述](@entry_id:190556)：物质导数

在描述流体运动时，存在两种基本视角：**拉格朗日（Lagrangian）**视角与**欧拉（Eulerian）**视角。拉格朗日方法如同给每个流体质点贴上标签，然后追踪其在空间中的运动轨迹。而欧拉方法则是在空间中设置固定的观测点，研究流体属性（如速度、压力）在这些点上随时间的变化。[纳维-斯托克斯方程](@entry_id:142275)通常采用[欧拉描述](@entry_id:264722)，因为它更适合处理复杂的流动边界与形态，但其核心的物理定律，如牛顿第二定律，本质上是应用于一个“物质”粒子或系统的，即拉格朗日性质的。

连接这两种视角的关键数学工具是**物质导数（material derivative）**，记作 $D/Dt$。它表示一个随流体一同运动的观测者所测得的物理量 $\phi$ 的变化率。对于一个[标量场](@entry_id:151443) $\phi(\mathbf{x}, t)$，其[物质导数](@entry_id:262900)的定义如下 ：
$$
\frac{D\phi}{Dt} = \frac{\partial \phi}{\partial t} + \mathbf{u} \cdot \nabla \phi
$$
其中 $\mathbf{u}(\mathbf{x}, t)$ 是[流体速度](@entry_id:267320)场。这个表达式由两部分组成：

1.  **[局部时](@entry_id:194383)间导数（Local time derivative）** $\frac{\partial \phi}{\partial t}$：表示在空间固定点 $\mathbf{x}$ 处，$\phi$ 随时间的变化。这是纯粹的非定常效应。
2.  **[对流导数](@entry_id:262900)（Convective derivative）** $\mathbf{u} \cdot \nabla \phi$：表示由于流体质点从一个位置移动到另一个具有不同 $\phi$ 值的位置而引起的变化。即使流场是定常的（即 $\frac{\partial \phi}{\partial t} = 0$），只要[质点](@entry_id:186768)在空间梯度 $\nabla \phi$ 不为零的区域中运动，这个量就不为零。

例如，想象一条河，上游水温低，下游水温高，即使每个位置的水温不随时间变化（[定常流](@entry_id:191654)），一艘随波逐流的小船上的温度计读数也会不断升高，这就是对流效应。物质导数捕捉了局部变化和随流运动带来的变化的“总和”。值得注意的是，对于标量场，物质导数的形式在[旋转坐标系](@entry_id:170324)和惯性坐标系下是相同的。然而，对于矢量场（如速度），在[旋转坐标系](@entry_id:170324)中对其求物质导数时，会额外出现科里奥利力和[离心力](@entry_id:173726)等惯性力项 。

### 普适[输运方程](@entry_id:174281)与守恒定律

流[体力](@entry_id:174230)学的核心是基于质量、动量和能量的守恒原理。这些原理可以通过一个普适的[输运方程](@entry_id:174281)来表述。考虑一个随流体运动的**物质控制体（material control volume）** $V_m(t)$，以及一个单位质量的物理量 $\phi$（例如，$\phi=1$ 代表质量本身，$\phi=\mathbf{u}$ 代表单位质量的动量）。该物理量在控制体内的总量变化率，等于其内部源/汇的生成/消耗率与通过边界的净通量之和。

这一守恒原理的积分形式可以写作 ：
$$
\frac{d}{dt} \int_{V_m(t)} \rho \phi \, dV = \int_{V_m(t)} \rho s \, dV - \oint_{\partial V_m(t)} \mathbf{J} \cdot \mathbf{n} \, dA
$$
这里，$\rho$ 是密度，$\rho \phi$ 是单位体积的该物理量， $s$ 是单位质量的源/汇率，$\mathbf{J}$ 是该物理量相对于主体流动的扩散通量，$\mathbf{n}$ 是控制体表面的外法向[单位向量](@entry_id:165907)。

为了将这个[拉格朗日形式](@entry_id:145697)的积分方程转化为[欧拉形式](@entry_id:637896)的[偏微分](@entry_id:194612)方程，我们需要两个关键的数学工具：**雷诺输运定理（Reynolds Transport Theorem, RTT）** 和 **高斯散度定理（Gauss's Divergence Theorem）**。RTT 将物质控制体上的积分的时间导数，转换到[固定控制体](@entry_id:272149)上的积分：
$$
\frac{d}{dt} \int_{V_m(t)} (\rho\phi) \, dV = \int_{V_m(t)} \left( \frac{\partial (\rho\phi)}{\partial t} + \nabla \cdot (\rho\phi\mathbf{u}) \right) dV
$$
同时，[散度定理](@entry_id:143110)将边界上的面积分通量转换为体积分：
$$
\oint_{\partial V_m(t)} \mathbf{J} \cdot \mathbf{n} \, dA = \int_{V_m(t)} \nabla \cdot \mathbf{J} \, dV
$$
将这两个定理代入积分守恒定律，并考虑到该定律对任意控制体均成立，我们可以得到普适守恒定律的局部（[微分](@entry_id:158422)）形式，也称为**[守恒形式](@entry_id:1122899)（conservative form）**：
$$
\frac{\partial (\rho\phi)}{\partial t} + \nabla \cdot (\rho\phi\mathbf{u}) = -\nabla \cdot \mathbf{J} + \rho s
$$
这个方程可以通过[链式法则](@entry_id:190743)和质量守恒定律，转化为更直观的**对流形式（advective form）**。

#### 质量守恒：连续性方程

将 $\phi=1$（单位质量的质量）且不存在源汇（$s=0$）和扩散（$\mathbf{J}=0$）代入[守恒形式方程](@entry_id:1122915)，我们得到**连续性方程（continuity equation）**：
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho\mathbf{u}) = 0
$$
这个方程表明，一个区域内密度的增加率等于[质量流](@entry_id:143424)入该区域的净速率。利用[链式法则](@entry_id:190743)展开 $\nabla \cdot (\rho\mathbf{u}) = \mathbf{u} \cdot \nabla\rho + \rho \nabla \cdot \mathbf{u}$，并结合[物质导数](@entry_id:262900)的定义，[连续性方程](@entry_id:195013)可以写成如下形式 ：
$$
\frac{D\rho}{Dt} + \rho \nabla \cdot \mathbf{u} = 0 \quad \text{或} \quad \frac{D\rho}{Dt} = -\rho \nabla \cdot \mathbf{u}
$$
这个形式生动地揭示了[速度场散度](@entry_id:178755) $\nabla \cdot \mathbf{u}$ 的物理意义：它代表了流体微团体积的膨胀率。对于**不可压缩流（incompressible flow）**，定义为跟随流体[质点](@entry_id:186768)运动时其密度保持不变，即 $\frac{D\rho}{Dt}=0$。由此可见，不可压缩流动的运动学约束条件是速度场无散：
$$
\nabla \cdot \mathbf{u} = 0
$$
对于密度为常数的流体，这一条件自然满足。

回到普适[输运方程](@entry_id:174281)，利用连续性方程，其[守恒形式](@entry_id:1122899)可以化简为对流形式：
$$
\rho \frac{D\phi}{Dt} = -\nabla \cdot \mathbf{J} + \rho s
$$
这个方程优雅地表述了随流运动的[质点](@entry_id:186768)其属性 $\phi$ 的变化，是由扩散和源汇项引起的。

### 动量守恒：从[柯西动量方程](@entry_id:187010)到[纳维-斯托克斯方程](@entry_id:142275)

将普适守恒原理应用于动量（即 $\phi = \mathbf{u}$），我们就可以推导出流体运动的核心方程。流体微团的动量变化来源于两类力：作用于整个体积的**体力（body forces）**（如重力，$\rho\mathbf{b}$），以及作用于其表面的**面力（surface forces）**（如压力和摩擦力）。面力通过**柯西[应力张量](@entry_id:148973)（Cauchy stress tensor）** $\boldsymbol{\sigma}$ 来描述。根据柯西应力原理，作用在法向为 $\mathbf{n}$ 的微小表面上的力（牵[引力](@entry_id:189550)）为 $\mathbf{t} = \boldsymbol{\sigma} \cdot \mathbf{n}$。

因此，[动量守恒](@entry_id:149964)的积分形式为：
$$
\frac{d}{dt} \int_{V_m(t)} \rho \mathbf{u} \, dV = \oint_{\partial V_m(t)} \boldsymbol{\sigma} \cdot \mathbf{n} \, dA + \int_{V_m(t)} \rho \mathbf{b} \, dV
$$
利用[雷诺输运定理](@entry_id:191217)和[散度定理](@entry_id:143110)（作用于张量 $\boldsymbol{\sigma}$），我们可以得到**[柯西动量方程](@entry_id:187010)（Cauchy's momentum equation）**：
$$
\rho \frac{D\mathbf{u}}{Dt} = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b}
$$
这个方程是牛顿第二定律在连续介质中的体现，它指出流体质点的加速度（左侧项）是由作用在其上的净[表面力](@entry_id:188034)（应力[张量的散度](@entry_id:191736)）和[体力](@entry_id:174230)共同引起的。然而，这个方程本身是不封闭的，因为我们尚未定义[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 与流场运动之间的关系。

#### 本构关系：定义流体特性

为了封闭方程，我们需要一个**本构关系（constitutive relation）**，它根据流体的物理特性将[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 与流体的变形关联起来。

首先，[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 自身具有一些基本性质。在经典连续介质理论中，若无[体力](@entry_id:174230)矩或[力偶应力](@entry_id:747952)，角动量守恒定律要求柯西[应力张量](@entry_id:148973)必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^\top$ 。此外，$\boldsymbol{\sigma}$ 可以唯一地分解为一个**各向同性（isotropic）**部分和一个**偏（deviatoric）**部分。在流体中，各向同性部分与压力有关，而偏部分则与导致[流体变形](@entry_id:271538)的剪切和拉伸应力有关。这种分解形式为 ：
$$
\boldsymbol{\sigma} = -p \mathbf{I} + \boldsymbol{\tau}
$$
其中 $p$ 是[热力学压力](@entry_id:1133073)，$\mathbf{I}$ 是单位张量，$\boldsymbol{\tau}$ 是**[偏应力张量](@entry_id:267642)（deviatoric stress tensor）** 或 **[粘性应力](@entry_id:261328)张量（viscous stress tensor）**。根据定义，[偏应力张量](@entry_id:267642)的迹为零，即 $\text{tr}(\boldsymbol{\tau})=0$。需要澄清一个常见的误解：[偏应力张量](@entry_id:267642)并非只产生剪切应力，它也可以产生法向应力（对角线分量），例如在某些非牛顿流体中出现的[法向应力差](@entry_id:199507)现象就是由 $\boldsymbol{\tau}$ 引起的 。

接下来，我们需要将应力与流动联系起来。流体的局部运动学可以通过[速度梯度张量](@entry_id:270928) $\nabla \mathbf{u}$ 来描述。$\nabla \mathbf{u}$ 可以分解为一个对称[部分和](@entry_id:162077)一个反对称部分 ：
$$
\nabla \mathbf{u} = \mathbf{D} + \mathbf{W}
$$
其中：
-   **[形变率张量](@entry_id:184787)（rate-of-deformation tensor）** $\mathbf{D} = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^\top)$ 是对称的，描述了流体微团的拉伸、压缩和[剪切变形](@entry_id:170920)速率。
-   **[涡量张量](@entry_id:189621)（vorticity tensor）** 或[自旋张量](@entry_id:187346) $\mathbf{W} = \frac{1}{2}(\nabla \mathbf{u} - (\nabla \mathbf{u})^\top)$ 是反对称的，描述了流体微团的刚性旋转速率，它与[涡量矢量](@entry_id:187667) $\boldsymbol{\omega} = \nabla \times \mathbf{u}$ 密切相关。

对于一类被称为**[牛顿流体](@entry_id:263796)（Newtonian fluids）**的常见流体（如水、空气），其本构关系假设粘性应力 $\boldsymbol{\tau}$ 与形变率 $\mathbf{D}$ 之间存在线性关系。对于不可压缩的[牛顿流体](@entry_id:263796)，这一关系极为简洁 ：
$$
\boldsymbol{\tau} = 2\mu \mathbf{D}
$$
其中 $\mu$ 是流体的**[动力粘度](@entry_id:268228)（dynamic viscosity）**，是一个衡量流体“粘稠度”的材料常数。将这个关系代入应力张量的分解式，我们得到不可压缩[牛顿流体](@entry_id:263796)的完整本构方程：
$$
\boldsymbol{\sigma} = -p\mathbf{I} + 2\mu \mathbf{D} = -p\mathbf{I} + \mu (\nabla \mathbf{u} + (\nabla \mathbf{u})^\top)
$$

#### 方程的综合与解读

最后，将不可压缩[牛顿流体的本构关系](@entry_id:1122933)代入[柯西动量方程](@entry_id:187010)，我们就得到了**[不可压缩纳维-斯托克斯](@entry_id:750595)方程（incompressible Navier-Stokes equations）**：
$$
\rho \frac{D\mathbf{u}}{Dt} = -\nabla p + \nabla \cdot (2\mu \mathbf{D}) + \rho\mathbf{b}
$$
若粘度 $\mu$ 为常数，并利用不可压缩条件 $\nabla \cdot \mathbf{u} = 0$，粘性项可以简化为 $\nabla \cdot (2\mu \mathbf{D}) = \mu \nabla^2 \mathbf{u}$。于是，我们得到最为人熟知的方程形式：
$$
\rho \left( \frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla)\mathbf{u} \right) = -\nabla p + \mu \nabla^2 \mathbf{u} + \rho\mathbf{b}
$$
该方程与连续性方程 $\nabla \cdot \mathbf{u} = 0$ 共同构成了描述不可压缩[牛顿流体](@entry_id:263796)运动的完整方程组。

方程中的每一项都有明确的物理意义 ：
-   $\rho \frac{\partial \mathbf{u}}{\partial t}$：**局部惯性项**，表示单位体积流体的[局部加速度](@entry_id:272847)。
-   $\rho (\mathbf{u} \cdot \nabla)\mathbf{u}$：**对流惯性项**，表示因流体[质点](@entry_id:186768)位置改变而产生的加速度。这是方程中的**[非线性](@entry_id:637147)项**，也是流[体力](@entry_id:174230)学丰富复杂现象（如[湍流](@entry_id:151300)）的根源。
-   $-\nabla p$：**压力[梯度力](@entry_id:166847)**，驱动流体从高压区流向低压区。
-   $\mu \nabla^2 \mathbf{u}$：**[粘性力](@entry_id:263294)**，源于流体内部的摩擦，作用是耗散动能并使速度分布趋于平滑。它可以被看作是动量的扩散。
-   $\rho\mathbf{b}$：**体力**，如重力。

这个方程深刻地揭示了流体运动的内在机制：流体质点的加速度是由压力、[粘性力](@entry_id:263294)和[体力](@entry_id:174230)共同作用的结果。

### 关键机制与推论

#### [非线性](@entry_id:637147)及其后果：从层流到[湍流](@entry_id:151300)

[纳维-斯托克斯方程](@entry_id:142275)的[非线性](@entry_id:637147)项 $\rho (\mathbf{u} \cdot \nabla)\mathbf{u}$ 是其最显著的数学特征。这种二次[非线性](@entry_id:637147)意味着解的[叠加原理](@entry_id:144649)不再适用。一个直接的例子是，如果 $(\mathbf{u}_1, p_1)$ 是一组解，那么将速度加倍得到的 $\mathbf{u}_2 = 2\mathbf{u}_1$ 通常不再是方程的解，因为它会导致对流项变为原来的四倍，而粘性项仅为原来的两倍。为了维持[动量平衡](@entry_id:1128118)，必须有一个新的压[力场](@entry_id:147325) $p_2$ 来抵消这种不平衡 。这种[非线性](@entry_id:637147)使得解析求解[纳维-斯托克斯方程](@entry_id:142275)极为困难，绝大多数实际问题都需要依赖数值方法。

更重要的是，[非线性](@entry_id:637147)项是**[湍流](@entry_id:151300)（turbulence）**产生的根本原因。当流速足够高，惯性力（由[非线性](@entry_id:637147)项主导）相对于[粘性力](@entry_id:263294)变得非常大时，平滑的层流状态会变得不稳定，演化为充满涡旋、时空尺度混乱的[湍流](@entry_id:151300)。

直接数值模拟（DNS）[湍流](@entry_id:151300)需要极高的计算资源，因为它必须解析所有尺度的涡旋。为了在工程上可行，人们发展了**[雷诺平均纳维-斯托克斯](@entry_id:173045)（Reynolds-Averaged Navier-Stokes, RANS）**方法。通过将[瞬时速度](@entry_id:167797)分解为平均[部分和](@entry_id:162077)脉动部分（$u_i = \bar{u}_i + u'_i$），并对[纳维-斯托克斯方程](@entry_id:142275)进行[时间平均](@entry_id:267915)，[非线性](@entry_id:637147)项会产生一个额外的项 ：
$$
\frac{\partial}{\partial x_j}(-\rho \overline{u'_i u'_j})
$$
这个张量 $\boldsymbol{\tau}^{(R)}_{ij} = -\rho \overline{u'_i u'_j}$ 被称为**[雷诺应力张量](@entry_id:270803)（Reynolds stress tensor）**。它代表了速度脉动对平均动量的输运效应，表现为一种额外的“[湍流](@entry_id:151300)应力”。然而，[雷诺应力](@entry_id:263788)本身是未知的，它依赖于脉动速度。如何用平均流场的量来模化[雷诺应力](@entry_id:263788)，这就是著名的**[湍流封闭问题](@entry_id:268973)（turbulence closure problem）**。

#### 压力的双重角色：驱动力与约束力

在[可压缩流](@entry_id:747589)中，压力是一个由状态方程决定的[热力学变量](@entry_id:160587)。但在[不可压缩流](@entry_id:140301)中，压力的角色更为微妙。一方面，它的梯度 $-\nabla p$ 是驱动流动的力。另一方面，压力本身扮演了一个**拉格朗日乘子**的角色，其值会自适应地调整，以确保速度场在任何时刻都满足不可压缩约束 $\nabla \cdot \mathbf{u} = 0$。

这种约束作用可以通过对动量方程两边取散度来揭示 。对于一个[不可压缩流](@entry_id:140301)，$\nabla \cdot (\partial \mathbf{u} / \partial t) = 0$ 和 $\nabla \cdot (\mu \nabla^2 \mathbf{u}) = \mu \nabla^2(\nabla \cdot \mathbf{u}) = 0$。因此，我们得到一个关于压力的**泊松方程（Poisson equation for pressure）**：
$$
\nabla^2 p = -\nabla \cdot (\rho (\mathbf{u} \cdot \nabla)\mathbf{u}) + \nabla \cdot (\rho\mathbf{b})
$$
这个方程表明，压[力场](@entry_id:147325)的拉普拉斯由惯性力和体力的散度决定。源项 $-\nabla \cdot (\rho (\mathbf{u} \cdot \nabla)\mathbf{u})$ 可以被理解为：在没有压力梯度干预的情况下，对流项试图产生或消除局部散度（即压缩或膨胀）的趋势。压[力场](@entry_id:147325)则会瞬时地建立起一个合适的梯度，精确地抵消这种趋势，从而强制维持 $\nabla \cdot \mathbf{u} = 0$ 的约束。

#### [涡量](@entry_id:142747)的产生与演化

[涡量](@entry_id:142747) $\boldsymbol{\omega} = \nabla \times \mathbf{u}$ 是流体力学中的一个核心概念，它描述了流体微团的局部旋转强度和方向。在[无粘流](@entry_id:273124)中，[涡量](@entry_id:142747)线会随着流体[质点](@entry_id:186768)一同运动（亥姆霍兹[涡量](@entry_id:142747)守恒定律）。然而，粘性的存在彻底改变了这一图景。

一个关键的机制是**在固体边界处产生涡量**。考虑一个原本静止的流体，其边界（如一块平板）突然开始运动。由于**[无滑移边界条件](@entry_id:186229)（no-slip boundary condition）**，与平板接触的流体层必须获得与平板相同的速度，而远离平板的流体仍然静止。这就在边界上形成了一个极大的[速度梯度](@entry_id:261686)，即一个强的[剪切层](@entry_id:274623)。由于[涡量](@entry_id:142747)本质上就是速度的卷曲（或剪切），这意味着在边界处产生了大量的[涡量](@entry_id:142747)。这些[新生的](@entry_id:918789)[涡量](@entry_id:142747)随后通过粘性扩散（diffusion）从边界向流体内部传播，并被流体通过对流（convection）带到更远的地方 。这个过程是许多流动现象（如机翼绕流中的尾涡）的根源。在著名的[斯托克斯第一问题](@entry_id:202672)（Stokes' first problem）中，平板运动产生的涡量在边界上的值可以精确求解为 $\omega_z(0, t) = U / \sqrt{\pi \nu t}$，其中 $\nu = \mu/\rho$ 是运动粘度。这表明[涡量](@entry_id:142747)在初始瞬间是无限大的，然后随时间扩散而减小。

### 数学基础：[适定性](@entry_id:148590)与函数空间

[纳维-斯托克斯方程](@entry_id:142275)的数学理论，特别是解的存在性与[光滑性](@entry_id:634843)问题，是现代数学中最具挑战性的难题之一，它被列为克莱数学研究所的七个千禧年大奖难题之一。然而，对于其[弱解](@entry_id:161732)（weak solutions）和数值解，我们已经有了坚实的理论框架。

在用有限元等方法求解[稳态](@entry_id:139253)[不可压缩纳维-斯托克斯](@entry_id:750595)方程时，我们需要在一个精确定义的**[函数空间](@entry_id:143478)**中寻找解。对于速度场 $\mathbf{u}$，它不仅需要能量有限（即其梯度平方可积），还必须满足边界条件。对于固壁上的[无滑移边界条件](@entry_id:186229) $\mathbf{u}=\mathbf{0}$，对应的[函数空间](@entry_id:143478)是**[索博列夫空间](@entry_id:141995)（Sobolev space）** $H^1_0(\Omega)^d$。对于压力 $p$，其要求较低，通常只需平方可积，即属于$L^2(\Omega)$空间 。

然而，这样的设置存在一个问题：压力的不唯一性。如前所述，由于压力仅以其梯度 $\nabla p$ 的形式出现在[动量方程](@entry_id:197225)中，如果 $p$ 是一个解，那么 $p+c$（其中 $c$ 是任意常数）也是一个解。这种“[规范自由度](@entry_id:160491)”导致了压力的无穷多解。

为了确保[解的唯一性](@entry_id:143619)，必须施加一个额外的约束来固定这个常数。一个标准且计算上方便的做法是要求压力在整个区域内的平均值为零：
$$
\int_{\Omega} p \, dV = 0
$$
这等价于将压力的求解空间限制在零平均的$L^2$函数空间，记作$L^2_0(\Omega)$。因此，一个适定的（well-posed）[稳态](@entry_id:139253)[不可压缩纳维-斯托克斯](@entry_id:750595)问题的弱形式，是在速度空间 $H^1_0(\Omega)^d$ 和压力空间 $L^2_0(\Omega)$ 中寻找唯一解。这一看似纯数学的处理，实际上是正确进行[数值模拟](@entry_id:146043)的根本保障 。