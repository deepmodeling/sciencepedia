## 引言
[动量守恒](@entry_id:149964)是继质量守恒和[能量守恒](@entry_id:140514)之后，支配所有物理系统行为的普适性基本定律之一，在[流体动力学](@entry_id:136788)领域，它更是描述流体运动的核心支柱。无论是微风拂过脸颊，还是超音速飞机划破长空，其背后复杂的流场演化都遵循着动量守恒的制约。然而，从这一抽象的物理原理，到能够精确预测和模拟[复杂流动](@entry_id:747569)的具体数学方程，存在着一条充满严谨推导和深刻物理洞见的路径。本文旨在系统性地跨越这一鸿沟，为读者铺设一条从第一性原理到高级应用的清晰学习路线。

本文将分为三个核心章节，带领读者层层深入动量守恒的世界。在第一章“原理与机制”中，我们将从经典力学的粒子体系出发，通过连续介质假设，建立起适用于流体的动量守恒积分形式，并详细剖析其中每一个物理项的含义，特别是关键的柯西应力张量。随后，我们将展示如何从积分形式推导出微分形式的[柯西动量方程](@entry_id:187010)，并最终通过引入本构关系，得到[流体力学](@entry_id:136788)王冠上的明珠——纳维-斯托克斯方程。第二章“应用与跨学科联系”将视野从理论转向实践，展示这些基本方程如何在空气动力学、能源工程、磁流体动力学乃至计算流体动力学（CFD）的[算法设计](@entry_id:634229)中发挥着决定性作用。最后，在“动手实践”部分，我们提供了一系列精心设计的问题，旨在通过实践加深对理论的理解，例如如何构建[壁面模型](@entry_id:756612)或设计保持守恒律的数值格式。通过这一结构化的学习旅程，读者将不仅掌握动量守恒的数学表述，更能深刻理解其在解决前沿科学与工程问题中的强大威力。

## 原理与机制

在[流体动力学](@entry_id:136788)的研究中，[动量守恒](@entry_id:149964)是描述流体运动的核心定律。本章旨在深入阐释[动量守恒](@entry_id:149964)定律的积分形式与微分形式，并揭示其背后的物理机制与数学基础。我们将从离散粒子体系的经典力学出发，过渡到连续介质的[场论](@entry_id:155241)描述，并最终建立起在[计算流体动力学](@entry_id:147500)（CFD）中广泛应用的控制方程。

### 从离散粒子到连续介质

经典力学告诉我们，一个由$N$个粒子组成的系统，其总动量的变化率等于所有作用于该系统上的外力之和。然而，流体由数量极其庞大的分子组成，直接对每个分子应用[牛顿第二定律](@entry_id:274217)在计算上是不可行的。因此，[流体动力学](@entry_id:136788)的基础是**连续介质假设**，它允许我们将流体视为一个连续的、可无限分割的物质，其物理性质（如密度和速度）在空间中是光滑变化的场。

这一假设的合理性建立在尺度分离的原则之上。 我们引入**代表性微元体（Representative Elementary Volume, REV）**的概念。REV的尺度必须远大于分子的[平均自由程](@entry_id:139563)（$\ell_m$），这样微元体内部就包含了足够多的分子，使得统计平均有意义，分子运动的随机涨落可以被平滑掉。同时，REV的尺度又必须远小于宏观流场变化的特征长度（$L_{\text{field}}$），这样我们才能将微元体内的平均物理量（如密度$\rho(\boldsymbol{x},t)$和速度$\boldsymbol{u}(\boldsymbol{x},t)$）视为空间点$\boldsymbol{x}$处的属性。这种空间上的尺度分离关系（$\ell_m \ll \Delta\ell \ll L_{\text{field}}$，其中$\Delta\ell$是REV的特征尺度）是连续介质模型成立的基石，它通常由[克努森数](@entry_id:139772)（$\mathrm{Kn} = \ell_m / L_{\text{field}}$）远小于1来保证。

此外，为了建立描述[应力与应变率](@entry_id:263123)关系的**[本构方程](@entry_id:138559)**，还需要时间尺度上的分离。 分子碰撞和达到[局部热力学平衡](@entry_id:139579)所需的时间（$\tau_{\text{coll}}$）必须远小于宏观流动特征时间（$T_{\text{macro}}$），即$\tau_{\text{coll}} \ll T_{\text{macro}}$。这保证了流体在每个瞬间和每个点上都处于[局部平衡](@entry_id:156295)态，使得应力等物理量可以表示为速度场及其梯度的瞬时函数。

### 动量守恒的积分形式

在连续介质假设下，我们可以将动量守恒定律应用于空间中的一个固定区域，即**控制体（Control Volume）** $V$。动量守恒的积分形式是一个普适的、基础的陈述：在任何固定的[控制体](@entry_id:143882)内，[总动量](@entry_id:173071)的变化率等于作用在该[控制体](@entry_id:143882)上的所有外力之和，加上穿过其边界的净[动量通量](@entry_id:199796)。

为了精确表述，我们引入**[雷诺输运定理](@entry_id:191217)（Reynolds Transport Theorem, RTT）**。该定理为我们提供了将跟随一个物质系统的[拉格朗日描述](@entry_id:264498)（[物质导数](@entry_id:172646)）与固定空间区域的[欧拉描述](@entry_id:264722)（局部时间导数和通量）联系起来的数学工具。对于一个固定的控制体$V$，其边界为$\partial V$，动量守恒的积分形式表述为：

$$
\frac{d}{dt} \int_V \rho \boldsymbol{u} \, dV + \oint_{\partial V} \rho \boldsymbol{u} (\boldsymbol{u} \cdot \boldsymbol{n}) \, dS = \oint_{\partial V} \boldsymbol{\sigma} \cdot \boldsymbol{n} \, dS + \int_V \rho \boldsymbol{f} \, dV
$$

让我们逐项解析这个方程的物理意义：
-   **$\frac{d}{dt} \int_V \rho \boldsymbol{u} \, dV$**: 控制体$V$内[总动量](@entry_id:173071)随时间的变化率。$\rho\boldsymbol{u}$是动量密度（单位体积的动量）。

-   **$\oint_{\partial V} \rho \boldsymbol{u} (\boldsymbol{u} \cdot \boldsymbol{n}) \, dS$**: 通过[控制体](@entry_id:143882)边界$\partial V$的净动量流出率。其中$\boldsymbol{u} \cdot \boldsymbol{n}$是垂直于边界微元$dS$的速度分量，$\rho (\boldsymbol{u} \cdot \boldsymbol{n}) \, dS$代表每秒钟流出该微元的质量，乘以速度$\boldsymbol{u}$即为流出的动量。这一项被称为**[对流](@entry_id:141806)（或移流）动量通量**。

-   **$\oint_{\partial V} \boldsymbol{\sigma} \cdot \boldsymbol{n} \, dS$**: 作用在[控制体](@entry_id:143882)边界$\partial V$上的总[表面力](@entry_id:188034)。$\boldsymbol{\sigma}$是**柯西[应力张量](@entry_id:148973)**，$\boldsymbol{n}$是边界外[法线](@entry_id:167651)向量。

-   **$\int_V \rho \boldsymbol{f} \, dV$**: 作用在控制体$V$内部的总体积力。$\boldsymbol{f}$是单位质量的体积力（例如[重力加速度](@entry_id:173411)）。

[动量守恒](@entry_id:149964)的积分形式是[流体动力学](@entry_id:136788)中最基本的表述之一。它的一个重要特性是，即使在流场存在间断（如激波）的情况下，它依然成立。 这使得它成为有限体积法（FVM）等数值方法的理论基础，因为这些方法正是通过在网格单元（控制体）上保证积分守恒来构建离散方程的。

### [表面力](@entry_id:188034)与柯西[应力张量](@entry_id:148973)

[表面力](@entry_id:188034)项$\oint_{\partial V} \boldsymbol{\sigma} \cdot \boldsymbol{n} \, dS$在[动量平衡](@entry_id:193575)中起着至关重要的作用。为了理解它，我们必须引入**柯西[应力张量](@entry_id:148973)** $\boldsymbol{\sigma}$。在流体内部任意一点，我们可以想象一个微小的表面，其法向量为$\boldsymbol{n}$。作用在该表面上的力（单位面积）被称为**牵[引力](@entry_id:175476)矢量** $\boldsymbol{t}(\boldsymbol{n})$。柯西应力定理指出，这个牵[引力](@entry_id:175476)矢量是[法向量](@entry_id:264185)的线性函数，这个[线性变换](@entry_id:149133)就由[应力张量](@entry_id:148973)$\boldsymbol{\sigma}$来定义：

$$
\boldsymbol{t}(\boldsymbol{n}) = \boldsymbol{\sigma} \cdot \boldsymbol{n}
$$

柯西[应力张量](@entry_id:148973)$\boldsymbol{\sigma}$可以被分解为两部分：一部分是各向同性的压力项，另一部分是[偏应力](@entry_id:163323)项（或称黏性应力项）：

$$
\boldsymbol{\sigma} = -p \boldsymbol{I} + \boldsymbol{\tau}
$$

这里，$p$是[热力学](@entry_id:141121)压力，$\boldsymbol{I}$是单位张量，$\boldsymbol{\tau}$是**黏性应力张量**（或[偏应力张量](@entry_id:267642)）。这个分解具有深刻的物理意义：
-   **压力项 $-p \boldsymbol{I}$**: 压力是一种各向同性的[正应力](@entry_id:260622)。它产生的牵[引力](@entry_id:175476)为$\boldsymbol{t}_p = (-p \boldsymbol{I}) \cdot \boldsymbol{n} = -p \boldsymbol{n}$。这个力总是沿着与表面法线相反的方向，即指向表面内部，代表压缩作用。

-   **黏性应力项 $\boldsymbol{\tau}$**: 黏性应力源于流体内部的摩擦和变形。它产生的牵[引力](@entry_id:175476)为$\boldsymbol{t}_{\tau} = \boldsymbol{\tau} \cdot \boldsymbol{n}$。这个力既可以有法向分量（非各向同性[正应力](@entry_id:260622)），也可以有切向分量（**切应力**），后者是导致流体产生剪切流动的直接原因。

例如，考虑一个位于$z=0$的平板，流体在其上方流动。作用在平板上的力可以通过对牵[引力](@entry_id:175476)矢量在板面积分得到。指向流体内部的[法向量](@entry_id:264185)为$\boldsymbol{n}=\boldsymbol{e}_z$。作用在板上任意一点$(x,y)$的力（单位面积）为$\boldsymbol{t} = \boldsymbol{\sigma} \cdot \boldsymbol{e}_z$。其分量形式为 $t_x = \tau_{xz}$, $t_y = \tau_{yz}$, $t_z = -p + \tau_{zz}$。总作用力$\boldsymbol{F} = \int_A \boldsymbol{t} \, dA$就是由沿板面积分的切应力（产生拖曳力）和[法向应力](@entry_id:260622)（压力和黏性正应力，产生[升力](@entry_id:274767)或压力）共同决定的。

### 微分形式：[柯西动量方程](@entry_id:187010)

虽然积分形式具有普适性，但对于分析流场在某一点的局部行为，微分形式的方程更为方便。从积分形式到微分形式的转换，需要一个关键的数学工具——**[高斯散度定理](@entry_id:188065)**，以及[对流](@entry_id:141806)场变量足够**光滑**的假设。  具体来说，我们需要密度、速度和应[力场](@entry_id:147325)至少是连续可微的（$C^1$[类函数](@entry_id:146970)），这样才能将边界上的[面积分](@entry_id:275394)转换为[控制体](@entry_id:143882)内的[体积分](@entry_id:171119)。

将[高斯散度定理](@entry_id:188065)应用于动量守恒积分方程中的通量项和[表面力](@entry_id:188034)项：
$$
\oint_{\partial V} \rho \boldsymbol{u} (\boldsymbol{u} \cdot \boldsymbol{n}) \, dS = \int_V \nabla \cdot (\rho \boldsymbol{u} \otimes \boldsymbol{u}) \, dV
$$
$$
\oint_{\partial V} \boldsymbol{\sigma} \cdot \boldsymbol{n} \, dS = \int_V \nabla \cdot \boldsymbol{\sigma} \, dV
$$
这里 $\otimes$ 表示张量[外积](@entry_id:147029)，$\rho \boldsymbol{u} \otimes \boldsymbol{u}$ 是一个[二阶张量](@entry_id:199780)，其 $(i,j)$ 分量为 $\rho u_i u_j$。

将这些[体积分](@entry_id:171119)代回原积分方程，并把时间导数移入积分号内，我们得到：
$$
\int_V \left( \frac{\partial (\rho \boldsymbol{u})}{\partial t} + \nabla \cdot (\rho \boldsymbol{u} \otimes \boldsymbol{u}) - \nabla \cdot \boldsymbol{\sigma} - \rho \boldsymbol{f} \right) dV = \mathbf{0}
$$
由于这个等式必须对任意选择的[控制体](@entry_id:143882)$V$都成立，并且被积函数是连续的，因此被积函数本身必须处处为零。这就得到了动量守恒的[微分形式](@entry_id:146747)，即**[柯西动量方程](@entry_id:187010)**：
$$
\frac{\partial (\rho \boldsymbol{u})}{\partial t} + \nabla \cdot (\rho \boldsymbol{u} \otimes \boldsymbol{u}) = \nabla \cdot \boldsymbol{\sigma} + \rho \boldsymbol{f}
$$
将[应力张量](@entry_id:148973)分解式 $\boldsymbol{\sigma} = -p \boldsymbol{I} + \boldsymbol{\tau}$ 代入，得到更常用的形式：
$$
\frac{\partial (\rho \boldsymbol{u})}{\partial t} + \nabla \cdot (\rho \boldsymbol{u} \otimes \boldsymbol{u}) = -\nabla p + \nabla \cdot \boldsymbol{\tau} + \rho \boldsymbol{f}
$$
这个方程也可以写成一个更紧凑的**[守恒形式](@entry_id:747710)**：
$$
\frac{\partial (\rho \boldsymbol{u})}{\partial t} + \nabla \cdot (\rho \boldsymbol{u} \otimes \boldsymbol{u} + p \boldsymbol{I} - \boldsymbol{\tau}) = \rho \boldsymbol{f}
$$
在这个形式中，**总[动量通量](@entry_id:199796)张量**被定义为 $\boldsymbol{\Pi} = \rho \boldsymbol{u} \otimes \boldsymbol{u} + p \boldsymbol{I} - \boldsymbol{\tau}$。它清晰地展示了动量是如何通过三种机制在空间中输运的：
1.  **[对流通量](@entry_id:158187) $\rho \boldsymbol{u} \otimes \boldsymbol{u}$**: 流体[质点](@entry_id:186768)自身携带的动量随着流动发生的输运。
2.  **压力通量 $p \boldsymbol{I}$**: 由压力产生的[法向力](@entry_id:174233)在流体内部传递动量。
3.  **黏性通量 $-\boldsymbol{\tau}$**: 由黏性力（剪切力和非各向同性正应力）传递动量。

### 本构关系与纳维-斯托克斯方程

[柯西动量方程](@entry_id:187010)本身是不封闭的，因为它包含了未知的黏性应力张量$\boldsymbol{\tau}$。为了求解方程，我们必须引入**本构关系**，即建立$\boldsymbol{\tau}$与流场运动学（主要是速度梯度$\nabla\boldsymbol{u}$）之间的关系。

对于[牛顿流体](@entry_id:263796)，我们假设[应力与应变率](@entry_id:263123)之间存在线性关系。最一般的可压缩[牛顿流体](@entry_id:263796)本构关系是：
$$
\boldsymbol{\tau} = \mu \left( \nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^T - \frac{2}{3}(\nabla \cdot \boldsymbol{u})\boldsymbol{I} \right) + \lambda_v (\nabla \cdot \boldsymbol{u})\boldsymbol{I}
$$
其中，$\mu$是**动力黏度**（或剪切黏度），$\lambda_v$是**体积黏度**。动力黏度$\mu$描述了流体抵抗[剪切变形](@entry_id:170920)的能力。体积黏度$\lambda_v$则与流体在压缩或膨胀过程中的[能量耗散](@entry_id:147406)有关。**[斯托克斯假设](@entry_id:195909)**通常被用于简化该关系，该假设认为$3\lambda_v + 2\mu = 0$，这在许多常见流体中是很好的近似。 

将此本构关系代入[柯西动量方程](@entry_id:187010)，我们就得到了描述可压缩黏性流体运动的**纳维-斯托克斯（Navier-Stokes）方程**。

一个极其重要且常见的特例是**不可压缩流动**，其特征是流体密度为常数，且速度场的散度为零（$\nabla \cdot \boldsymbol{u} = 0$）。在这种情况下，本构关系得到极大简化：
$$
\boldsymbol{\tau} = \mu \left( \nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^T \right)
$$
黏性力项$\nabla \cdot \boldsymbol{\tau}$也随之简化。如果动力黏度$\mu$在空间上是均匀的，则：
$$
\nabla \cdot \boldsymbol{\tau} = \mu \nabla \cdot (\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^T) = \mu (\nabla^2 \boldsymbol{u} + \nabla(\nabla \cdot \boldsymbol{u})) = \mu \nabla^2 \boldsymbol{u}
$$
这里的$\nabla^2 \boldsymbol{u}$是矢量[拉普拉斯算子](@entry_id:146319)。于是，不可压缩流动的[纳维-斯托克斯方程](@entry_id:142275)为：
$$
\rho \left( \frac{\partial \boldsymbol{u}}{\partial t} + (\boldsymbol{u} \cdot \nabla)\boldsymbol{u} \right) = -\nabla p + \mu \nabla^2 \boldsymbol{u} + \rho \boldsymbol{f}
$$
将此方程两边同除以密度$\rho$，得到：
$$
\frac{\partial \boldsymbol{u}}{\partial t} + (\boldsymbol{u} \cdot \nabla)\boldsymbol{u} = -\frac{1}{\rho}\nabla p + \frac{\mu}{\rho} \nabla^2 \boldsymbol{u} + \boldsymbol{f}
$$
在这里，我们定义**运动黏度** $\nu = \mu / \rho$。这个方程的形式清楚地揭示了$\nu$的物理意义。它是一个动量-扩散方程，其中$\nu \nabla^2 \boldsymbol{u}$是[扩散](@entry_id:141445)项。因此，**运动黏度$\nu$是动量的[扩散](@entry_id:141445)系数**，其量纲为$\text{长度}^2/\text{时间}$。它直接决定了动量（以及涡量）由于黏性效应在流体中[扩散](@entry_id:141445)的速率，而动力黏度$\mu$则直接关联了[应力与应变率](@entry_id:263123)。

### 进阶议题与诠释

#### 压力梯度的角色

在[动量方程](@entry_id:197225)中，[压力梯度](@entry_id:274112)项$-\nabla p$扮演着一个特殊的角色。它代表一种内部力，本身不产生或消灭动量，而是在流体内部重新分配动量。我们可以通过散度定理来理解这一点。作用于整个[控制体](@entry_id:143882)$V$的净压力为$\int_V (-\nabla p) \, dV$。根据[散度定理](@entry_id:143110)，这个力等于$\oint_{\partial V} (-p \boldsymbol{n}) \, dS$。 如果一个流体系统具有[周期性边界条件](@entry_id:147809)，这意味着在相对边界上的压力值是相等的，那么净压力$\oint_{\partial V} (-p \boldsymbol{n}) \, dS$将精确为零。这说明对于一个孤立的或周期性的系统，压力无法改变系统的[总动量](@entry_id:173071)，它只能将动量从高压区推向低压区。

#### [非惯性参考系](@entry_id:169712)

[动量守恒](@entry_id:149964)定律的结构在[非惯性参考系](@entry_id:169712)中依然保持，只需将[参考系](@entry_id:169232)本身的加速和旋转效应视为一种**表观体积力（apparent body force）**。 如果一个[控制体](@entry_id:143882)固定在一个以加速度$\boldsymbol{a}_0$平动并以[角速度](@entry_id:192539)$\boldsymbol{\Omega}$转动的[参考系](@entry_id:169232)中，那么在相对于该[参考系](@entry_id:169232)的速度$\boldsymbol{u}$的动量方程中，必须引入一个有效的体积力$\boldsymbol{f}_{\text{eff}}$：
$$
\boldsymbol{f}_{\text{eff}} = \boldsymbol{f}_{\text{phys}} - \boldsymbol{a}_0 - 2\boldsymbol{\Omega} \times \boldsymbol{u} - \dot{\boldsymbol{\Omega}} \times \boldsymbol{r} - \boldsymbol{\Omega} \times (\boldsymbol{\Omega} \times \boldsymbol{r})
$$
其中，$\boldsymbol{f}_{\text{phys}}$是物理体积力（如重力），其余各项分别是[平动](@entry_id:187700)加速力、科里奥利力、[欧拉力](@entry_id:173795)（由角加速度引起）和[离心力](@entry_id:173726)。通过这种方式，我们可以在任何[参考系](@entry_id:169232)中统一地应用[动量守恒](@entry_id:149964)框架。

#### 积分形式的首要性

最后，我们必须再次强调，[动量守恒](@entry_id:149964)的**积分形式是比[微分形式](@entry_id:146747)更为根本的物理定律**。 [微分形式](@entry_id:146747)的推导依赖于场的连续性和[可微性](@entry_id:140863)。当流场中出现像激波这样的间断时，速度、密度和压力会发生跳变，[微分形式](@entry_id:146747)在[间断面](@entry_id:180188)上变得没有意义。然而，积分形式在跨越[间断面](@entry_id:180188)的控制体上仍然有效。实际上，正是通过对一个无限薄的、跨越[间断面](@entry_id:180188)的[控制体](@entry_id:143882)应用[积分守恒律](@entry_id:202878)，我们才能推导出著名的**兰金-雨果尼厄（Rankine-Hugoniot）跳跃关系**，这是分析激波和其它间断流动的理论基石。这一思想也深刻地影响了现代[计算流体动力学](@entry_id:147500)的发展，许多鲁棒的数值格式都是建立在积分守恒的基础之上的。