## 引言
[流体运动学](@entry_id:202835)是研究流体运动几何性质的学科，它为整个流[体力](@entry_id:174230)学提供了描述语言，而不涉及引起运动的力。理解如何精确描述流体质点的运动以及附着于其上的物理量（如温度或密度）如何随之变化，是进行任何深入动力学分析或[计算模拟](@entry_id:146373)的先决条件。然而，在描述这种连续介质的运动时，我们面临着一个根本性的选择：是观察空间中的固定点（欧拉视角），还是追踪单个流体质点（[拉格朗日视角](@entry_id:265471)）？如何在这两种看似不同的描述之间建立联系，并从中提炼出关于局部变形、旋转和膨胀的普适性信息，构成了[流体运动学](@entry_id:202835)的核心挑战。

本文旨在系统地梳理[流体运动学](@entry_id:202835)的关键概念，为研究生层次的学习者构建一个清晰的知识框架。我们将通过三个章节的递进式学习，带领读者从基本原理走向前沿应用：
*   在“**原理和机制**”中，我们将建立欧拉与拉格朗日描述，引入核心概念“[物质导数](@entry_id:262900)”作为连接两者的桥梁，并深入探讨[速度梯度张量](@entry_id:270928)如何揭示流动的局部结构。
*   在“**应用与跨学科连接**”中，我们将展示这些运动学原理如何在[计算流体动力学](@entry_id:142614)（CFD）、[复杂流体流变学](@entry_id:747570)、地球物理学乃至几何力学等领域中发挥关键作用。
*   最后，通过“**实践环节**”，读者将通过解决具体问题来巩固对物质导数及其物理意义的理解。

通过这一结构，本文将帮助你不仅掌握[流体运动学](@entry_id:202835)的数学形式，更能深刻理解其物理内涵及其在现代科学与工程中的广泛应用。

## 原理和机制

在对流体运动进行数学描述时，运动学是研究其几何性质的基础，而不涉及引起运动的力。本章旨在系统地阐述[流体运动学](@entry_id:202835)的核心原理与机制，为后续的动力学分析和计算建模奠定基础。我们将从描述流体运动的两种基本视角出发，引入[物质导数](@entry_id:262900)的概念以刻画随流体运动的物理量变化，进而深入探讨流场的局部变形、旋转和膨胀，并最终讨论这些运动学量如何与基本物理守恒定律以及观察者无关性原理相联系。

### 欧拉与拉格朗日描述

描述流体运动存在两种经典视角：欧拉（Eulerian）视角和拉格朗日（Lagrangian）视角。

**[欧拉描述](@entry_id:264722)**将注意力集中在空间中的固定点上。我们定义一个**欧拉速度场** $\mathbf{v}(\mathbf{x}, t)$，它给出了在时刻 $t$ 占据空间位置 $\mathbf{x}$ 的流体[质点](@entry_id:186768)的[瞬时速度](@entry_id:167797)。这就像站在河岸上观察特定位置的水流速度。速度的量纲是长度除以时间，即 $[\mathbf{v}] = \mathrm{L}\mathrm{T}^{-1}$。为了能够进行标准的[运动学分析](@entry_id:1126917)，例如定义加速度、散度和变形率，速度场 $\mathbf{v}$ 必须具备一定的[光滑性](@entry_id:634843)。具体而言，$\mathbf{v}$ 需要在空间上至少是连续可微的（$\mathcal{C}^1$），以确保其空间梯度 $\nabla \mathbf{v}$ 是良定义的和连续的；同时，它也需要在时间上是连续可微的，以确保[局部时](@entry_id:194383)间导数 $\partial \mathbf{v}/\partial t$ 存在。这些正则性假设是[运动学分析](@entry_id:1126917)的数学前提，独立于任何特定的本构关系 。

与[欧拉描述](@entry_id:264722)不同，**拉格朗日描述**则追踪每一个单独的流体质点。我们将流体中的每个[质点](@entry_id:186768)用其在初始时刻 $t=0$ 的位置 $\mathbf{X}$（称为物质坐标或标签）来唯一标识。该[质点](@entry_id:186768)在任意时刻 $t$ 的空间位置 $\mathbf{x}$ 便是其物质坐标 $\mathbf{X}$ 和时间 $t$ 的函数。这个映射关系被称为**流映射**（flow map），记作 $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$。流映射的定义域是参考构型中的所有物[质点](@entry_id:186768)与时间的[笛卡尔积](@entry_id:154642)，而其值域则是当前的物理空间。根据定义，在初始时刻，质点位于其标签所示的位置，因此流映射满足初始条件 $\boldsymbol{\chi}(\mathbf{X}, 0) = \mathbf{X}$。

这两种描述通过一个基本关系联系在一起：一个被标记为 $\mathbf{X}$ 的物质质点在时刻 $t$ 的速度，正是其位置函数 $\boldsymbol{\chi}(\mathbf{X}, t)$ 对时间的导数（保持 $\mathbf{X}$ 不变）。同时，根据欧拉速度场的定义，该速度也等于质点当前所在位置 $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$ 处的欧拉速度值。这便得到了连接两种描述的核心[微分](@entry_id:158422)方程 ：
$$
\frac{\partial \boldsymbol{\chi}(\mathbf{X}, t)}{\partial t} = \mathbf{v}(\boldsymbol{\chi}(\mathbf{X}, t), t)
$$
给定一个欧拉速度场 $\mathbf{v}(\mathbf{x}, t)$，通过求解上述以 $\boldsymbol{\chi}(\mathbf{X}, 0) = \mathbf{X}$ 为初始条件的[常微分方程组](@entry_id:907499)，我们就可以确定每个流体质点的运动轨迹，即**[迹线](@entry_id:261720)**（pathline）。

除了[迹线](@entry_id:261720)，流场的可视化还常常用到**[流线](@entry_id:266815)**（streamline）。流线是在某一固定时刻 $t^{\star}$，与该时刻速度场 $\mathbf{v}(\mathbf{x}, t^{\star})$ 处处相切的曲线族。它们给出了流体在该瞬间的“快照”方向。只有当流场是**定常**的（steady），即 $\partial \mathbf{v}/\partial t = \mathbf{0}$ 时，[迹线和流线](@entry_id:184041)才会重合。对于**非定常**（unsteady）流，一个[质点](@entry_id:186768)的轨迹通常会穿越多条不同时刻的[流线](@entry_id:266815)。例如，在一个振荡流场 $\mathbf{v}(\mathbf{x}, t) = \left(U_0, \beta x \cos(\omega t)\right)$ 中，任意时刻 $t^{\star}$ 的[流线](@entry_id:266815)是一族抛物线 $y(x; t^{\star}) = \frac{\beta}{2 U_0} x^2 \cos(\omega t^{\star}) + C$，而一个[质点](@entry_id:186768)的[迹线](@entry_id:261720)则是通[过积分](@entry_id:753033) $\dot{\mathbf{x}}(t) = \mathbf{v}(\mathbf{x}(t), t)$ 得到的更为复杂的曲线 。

### [物质导数](@entry_id:262900)：跟随流体的变化率

在流[体力](@entry_id:174230)学中，我们不仅关心流体的位置如何变化，更关心与流体一同运动的各种物理量（如温度、浓度、微结构参数等）的变化率。这里，欧拉和[拉格朗日视角](@entry_id:265471)再次体现出差异。

一个[标量场](@entry_id:151443) $\phi(\mathbf{x}, t)$ 在固定空间点 $\mathbf{x}$ 的变化率由其对时间的偏导数 $\partial \phi / \partial t$ 给出，这被称为**局部导数**或欧拉导数。然而，一个随波逐流的流体质点所经历的变化率，不仅取决于该点物理量的局域时间变化，还取决于[质点](@entry_id:186768)运动到物理量[空间分布](@entry_id:188271)不同的新位置所带来的变化。

跟随一个流体质点（其轨迹为 $\mathbf{x}(t)$）测量的物理量 $\phi$ 的[全时间导数](@entry_id:172646)，被称为**物质导数**（material derivative）或随流导数（substantive derivative），记作 $D\phi/Dt$。根据多元微积分的链式法则，我们可以推导出其表达式 ：
$$
\frac{D\phi}{Dt} = \frac{d}{dt}\phi(\mathbf{x}(t), t) = \frac{\partial \phi}{\partial t} + (\nabla \phi) \cdot \frac{d\mathbf{x}(t)}{dt}
$$
由于质点的速度就是该处的流体速度，即 $d\mathbf{x}(t)/dt = \mathbf{v}(\mathbf{x}(t), t)$，我们得到[物质导数](@entry_id:262900)的标准[欧拉形式](@entry_id:637896)：
$$
\frac{D\phi}{Dt} = \frac{\partial \phi}{\partial t} + (\mathbf{v} \cdot \nabla)\phi
$$
这个表达式清晰地展示了[物质导数](@entry_id:262900)由两部分构成：
1.  **局部项** $\partial \phi / \partial t$：在固定位置上观察到的场的时间变化。
2.  **对流项**（或称移流项） $(\mathbf{v} \cdot \nabla)\phi$：由于[质点](@entry_id:186768)运动到场 $\phi$ 具有空间梯度的新位置而引起的变化。

为了具体理解这两者的区别，考虑一个二维[剪切流](@entry_id:266817) $\mathbf{u}(x,y,t) = (\gamma(t)y, 0)$ 和一个[标量场](@entry_id:151443) $\phi(x,y,t) = at + bxy$。在空间固定点 $(x^{\star}, y^{\star})$ 处，我们测量的变化率就是局部导数 $\partial_t \phi = a$。然而，一个在 $t^{\star}$ 时刻恰好经过该点的流体质点，它所经历的变化率是物质导数 $D\phi/Dt = \partial_t \phi + u_x \partial_x \phi + u_y \partial_y \phi = a + (\gamma(t^{\star})y^{\star})(by^{\star}) + 0 = a + b\gamma(t^{\star})(y^{\star})^2$。显然，只要对流项不为零，这两个变化率就不同 。例如，对于一个具体的例子，若速度场 $\mathbf{v}=(-2tx, y^2, 0)$ 且标量场 $\phi=e^{-4t}xy+z$，则在点 $(1, -2, 3)$ 和时刻 $t=0$，局部项 $\partial_t\phi$ 为 $8$，对流项 $\mathbf{v}\cdot\nabla\phi$ 为 $4$，使得总的物质导数为 $12$ 。

物质导数这一概念可以推广到矢量场 $\mathbf{w}$ 和[张量场](@entry_id:190170) $\mathbf{A}$：
$$
\frac{D\mathbf{w}}{Dt} = \frac{\partial \mathbf{w}}{\partial t} + (\mathbf{v} \cdot \nabla)\mathbf{w}
$$
$$
\frac{D\mathbf{A}}{Dt} = \frac{\partial \mathbf{A}}{\partial t} + (\mathbf{v} \cdot \nabla)\mathbf{A}
$$
其中 $(\mathbf{v} \cdot \nabla)$ 算子作用于矢量或张量的每一个分量。

### 局部运动学：[速度梯度张量](@entry_id:270928)

为了理解流体微团（一个无限小的物质体积）的局部运动，我们需要考察速度场的空间变化，这由**[速度梯度张量](@entry_id:270928)** $\mathbf{L} = \nabla \mathbf{v}$ 来描述。在[笛卡尔坐标系](@entry_id:169789)下，其分量为 $L_{ij} = \partial v_i / \partial x_j$。这个张量包含了流体微团平动之外的所有运动信息，并且可以唯一地分解为一个对称[部分和](@entry_id:162077)一个反对称部分：$\mathbf{L} = \mathbf{D} + \mathbf{W}$ 。

1.  **[应变率张量](@entry_id:266108)**（rate-of-strain tensor） $\mathbf{D}$ 是 $\mathbf{L}$ 的对称部分：
    $$
    \mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\top}) = \frac{1}{2}(\nabla\mathbf{v} + (\nabla\mathbf{v})^{\top})
    $$
    $\mathbf{D}$ 描述了流体微团的变形速率。考虑两个无限靠近的物质点，其[分离矢量](@entry_id:268468)为 $\boldsymbol{\xi}$。可以证明，其长度平方的变化率仅由 $\mathbf{D}$ 决定 ：
    $$
    \frac{D}{Dt}(|\boldsymbol{\xi}|^2) = \frac{D}{Dt}(\boldsymbol{\xi}^{\top}\boldsymbol{\xi}) = 2\boldsymbol{\xi}^{\top}\mathbf{D}\boldsymbol{\xi}
    $$
    $\mathbf{D}$ 的对角分量 $D_{ii}$ 代表了沿坐标轴方向的拉伸或压缩率，非对角分量 $D_{ij}$ ($i \neq j$) 代表了[剪切变形](@entry_id:170920)率。

2.  **[自旋张量](@entry_id:187346)**（spin tensor） $\mathbf{W}$ 是 $\mathbf{L}$ 的反对称部分：
    $$
    \mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^{\top}) = \frac{1}{2}(\nabla\mathbf{v} - (\nabla\mathbf{v})^{\top})
    $$
    $\mathbf{W}$ 描述了流体微团的刚性旋转速率。它与流体的**涡度矢量** $\boldsymbol{\omega} = \nabla \times \mathbf{v}$ 密切相关。对于任意矢量 $\mathbf{a}$，它们的关系是 $\mathbf{W}\mathbf{a} = \frac{1}{2}\boldsymbol{\omega} \times \mathbf{a}$。这表明流体微团的角速度是涡度的一半，即 $\boldsymbol{\Omega}_{\text{fluid}} = \frac{1}{2}\boldsymbol{\omega}$ 。由于[反对称张量](@entry_id:199349)的二次型 $\boldsymbol{\xi}^{\top}\mathbf{W}\boldsymbol{\xi}$ 恒为零，自旋运动本身不会改变物质[线元](@entry_id:196833)的长度。

[速度梯度张量](@entry_id:270928)的迹，即速度场的**散度** $\nabla \cdot \mathbf{v}$，具有特殊的物理意义。由于任何[反对称张量](@entry_id:199349)的迹都为零 ($\mathrm{tr}(\mathbf{W})=0$)，我们有 ：
$$
\nabla \cdot \mathbf{v} = \mathrm{tr}(\mathbf{L}) = \mathrm{tr}(\mathbf{D} + \mathbf{W}) = \mathrm{tr}(\mathbf{D})
$$
这表明，[速度散度](@entry_id:264117)完全由[应变率张量](@entry_id:266108)决定，它代表了单位体积的流体微团[体积膨胀](@entry_id:144241)率。

### 运动学约束与守恒定律

流体的运动学并非完全任意，它必须服从基本的物理守恒定律。[质量守恒](@entry_id:204015)是其中最基本的一条。在没有源或汇的情况下，[质量守恒](@entry_id:204015)的局部形式——**连续性方程**——为：
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho\mathbf{v}) = 0
$$
利用[物质导数](@entry_id:262900)的定义，该方程可以改写为一种极其重要的形式：
$$
\frac{D\rho}{Dt} + \rho(\nabla \cdot \mathbf{v}) = 0
$$
这个方程纯粹是运动学和质量守恒的结果，不依赖于任何关于流体材料属性（如粘性）的假设。它揭示了[物质密度](@entry_id:263043)变化与流场体积膨胀之间的深刻联系 。

一个重要的运动学约束是**[不可压缩性](@entry_id:274914)**。如果一个流体是不可压缩的，意味着跟随流体运动的任何微团的密度都保持不变，即 $D\rho/Dt = 0$。将此条件代入上述[连续性方程](@entry_id:195013)，只要密度 $\rho > 0$，我们立即得到一个至关重要的结论 ：
$$
\nabla \cdot \mathbf{v} = 0
$$
因此，[不可压缩流](@entry_id:140301)动的速度场必须是**无散的**（divergence-free）。值得强调的是，不可压缩性 ($D\rho/Dt = 0$) 并不要求密度在空间上是均匀的。例如，在稳定的密度[分层流体](@entry_id:181098)中，密度可以随深度变化，但流场仍然可以是无散的。

[速度散度](@entry_id:264117)的物理意义可以通过考察一个物质体积 $\Omega(t)$ 的变化来进一步阐明。根据雷诺输运定理和高斯散度定理，该体积的变化率等于速度场在其边界面上的通量，也等于[速度散度](@entry_id:264117)在整个体积上的积分 ：
$$
\frac{d}{dt}|\Omega(t)| = \int_{\partial\Omega(t)} \mathbf{v} \cdot \mathbf{n} \,dA = \int_{\Omega(t)} \nabla \cdot \mathbf{v} \,dV
$$
这表明 $\nabla \cdot \mathbf{v}$ 确实是局部体积膨胀率。

在[拉格朗日框架](@entry_id:751113)下，体积变化由**变形梯度张量** $\mathbf{F} = \partial\boldsymbol{\chi}/\partial\mathbf{X}$ 的行列式——**[雅可比行列式](@entry_id:137120)** $J = \det(\mathbf{F})$ 来描述，$J$ 表示局部体积微元 $dV$ 相对于其初始体积 $dV_0$ 的比率。可以证明，$J$ 的物质导数满足著名的**欧拉展开公式** ：
$$
\frac{DJ}{Dt} = J (\nabla \cdot \mathbf{v})
$$
这个公式优雅地连接了[拉格朗日描述](@entry_id:1127015)中的体积变化 ($J$) 和[欧拉描述](@entry_id:264722)中的膨胀率 ($\nabla \cdot \mathbf{v}$)。对于不可压缩流，$\nabla \cdot \mathbf{v} = 0$，因此 $DJ/Dt = 0$，这意味着 $J$ 保持为其初始值（通常为 $1$），即物质体积守恒。此外，[质量守恒定律](@entry_id:147377)在[拉格朗日框架](@entry_id:751113)下可以简洁地表示为 $\rho(\boldsymbol{\chi}(\mathbf{X},t), t) J(\mathbf{X},t) = \rho_0(\mathbf{X})$，即“当前密度乘以体积比等于初始密度” 。

### 标架无关性与[客观时间导数](@entry_id:1129024)

物理定律的形式不应依赖于观察者。这一基本原则被称为**物质标架无关性**（principle of material frame-indifference）或**客观性**（objectivity）。在力学中，这意味着物理方程在叠加一个任意的刚体运动（平动和转动）作为观察者变换后，其形式应保持不变。

一个关键的问题是，我们之前定义的物质导数 $D/Dt$ 是否是一个**客观的**时间导数算子？也就是说，对于一个客观的矢量场 $\mathbf{w}$（在不同观察者看来，它通过旋转矩阵 $\mathbf{Q}(t)$ 联系），其[物质导数](@entry_id:262900) $(D\mathbf{w}/Dt)$ 是否也像一个客观矢量那样变换？答案是否定的。可以证明，在旋转观察系中计算的[物质导数](@entry_id:262900)会多出一个与观察者角速度相关的项 ：
$$
\left(\frac{D\mathbf{w}}{Dt}\right)' = \mathbf{Q}\frac{D\mathbf{w}}{Dt} + \dot{\mathbf{Q}}\mathbf{w}
$$
这个多出来的项 $\dot{\mathbf{Q}}\mathbf{w}$ 破坏了客观性。这意味着，任何直接使用[物质导数](@entry_id:262900)来描述张量物理量（如应力、微结构张量）演化的[本构方程](@entry_id:138559)，其预测结果都会随观察者的旋转而改变，这是非物理的。

为了构建客观的本构方程，必须使用**[客观时间导数](@entry_id:1129024)**。这些导数通过在物质导数的基础上减去额外的项来修正非客观性。在[复杂流体](@entry_id:198415)计算中，常用的客观导数包括：

- **共旋（Jaumann）导数**：它通过减去与流体局部刚性旋转相关的项来修正。对于矢量 $\mathbf{w}$，其形式为：
  $$
  \overset{\circ}{\mathbf{w}} = \frac{D\mathbf{w}}{Dt} - \mathbf{W}\mathbf{w}
  $$
  可以证明，这个导数是客观的，因为它恰好消除了由观察者旋转引入的非客观项。这种修正的需求纯粹源于运动学，与应力如何建模无关  。

- **上随体（Oldroyd-B）导数**：对于描述材料[线元](@entry_id:196833)仿射变形的构象张量 $\mathbf{C}$（一种[逆变张量](@entry_id:636697)），其客观的[演化速率](@entry_id:202008)由[上随体导数](@entry_id:756365)给出：
  $$
  \overset{\triangledown}{\mathbf{C}} = \frac{D\mathbf{C}}{Dt} - \mathbf{L}\mathbf{C} - \mathbf{C}\mathbf{L}^{\top}
  $$
  这个导数同样被证明是客观的，其形式源于对物质线元向量在流动中如何被拉伸和旋转的运动学描述。因此，使用这类客观导数是保证微[结构演化](@entry_id:186256)模型物理真实性的运动学前提  。

最后，值得一提的是，物质导数对于[标量场](@entry_id:151443)是**伽利略不变的**，即在恒速平动的参考系下保持不变。这是客观性的一个特例（无旋转）。在这种变换下，局部项 $\partial\phi/\partial t$ 和对流项 $(\mathbf{v}\cdot\nabla)\phi$ 各自都不是不变的，但它们的变换部分相互抵消，使得它们的和——[物质导数](@entry_id:262900)——保持不变  。这进一步凸显了物质导数作为描述“跟随物质”变化的物理重要性。