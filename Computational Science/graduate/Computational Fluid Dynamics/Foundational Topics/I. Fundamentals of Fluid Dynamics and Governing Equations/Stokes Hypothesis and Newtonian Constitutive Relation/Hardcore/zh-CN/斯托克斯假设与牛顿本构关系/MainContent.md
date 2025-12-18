## 引言
在[流体动力学](@entry_id:136788)研究中，建立描述流体内部应力与运动变形之间关系的[本构方程](@entry_id:138559)是核心任务之一。对于[牛顿流体](@entry_id:263796)，这一关系是线性的，构成了广泛应用的纳维-斯托克斯方程的理论基石。然而，在处理[可压缩流体](@entry_id:164617)时，一个名为“[斯托克斯假设](@entry_id:195909)”的简化被频繁采用，但其物理内涵、适用范围和理论推论却常常引起混淆。本文旨在填补这一认知空白，系统性地剖析[牛顿本构关系](@entry_id:752479)及其背后深刻的物理原理。

本文将引导读者踏上一段从理论到实践的探索之旅。在“原理与机制”一章中，我们将从线性、客观性和各向同性等基本公理出发，严谨推导[牛顿流体](@entry_id:263796)本构关系的一般形式，并阐明[斯托克斯假设](@entry_id:195909)的多种等价表述及其与体积黏度的直接关联。随后的“应用与跨学科联系”一章将展示这些理论如何在[计算流体动力学](@entry_id:147500)（CFD）、[声学](@entry_id:265335)和气体动力学等前沿领域中发挥关键作用，揭示其在声波衰减和激波结构分析中的重要性。最后，通过“动手实践”环节，读者将有机会将理论知识应用于解决具体的计算问题，从而加深对模型假设在[数值模拟](@entry_id:137087)中实际影响的理解。

## 原理与机制

在对流体运动进行数学描述时，一个核心挑战在于建立[应力张量](@entry_id:148973)与[流体变形](@entry_id:271538)之间的关系。这个关系被称为[本构关系](@entry_id:186508)，它体现了特定流体的材料属性。对于一类被称为牛顿流体的常见流体，这种关系是线性的。本章将从基本物理原理出发，系统地推导[牛顿流体](@entry_id:263796)的本构关系，并深入探讨一个在[流体动力学](@entry_id:136788)中被广泛应用但又常被误解的假设——[斯托克斯假设](@entry_id:195909)。我们将阐明其物理意义、理论基础、适用范围及其在现代[计算流体力学](@entry_id:747620)（CFD）模型中的具体体现。

### 牛顿流体的[本构关系](@entry_id:186508)

我们旨在建立流体内部的黏性[应力张量](@entry_id:148973) $\boldsymbol{\tau}$ 与[流体运动学](@entry_id:202835)特性之间的定量关系。对于[牛顿流体](@entry_id:263796)，这一关系遵循三个基本原理：线性、物质[坐标系](@entry_id:156346)无关性（客观性）和材料各向同性。

#### 基本原理

1.  **线性 (Linearity)**：[牛顿流体](@entry_id:263796)的定义性特征是，黏性应力是应变率的线性函数。流体的局部运动可以通过[速度梯度张量](@entry_id:270928) $\nabla \boldsymbol{u}$ 来完全描述。因此，我们可以假设存在一个线性映射 $\boldsymbol{f}$，使得 $\boldsymbol{\tau} = \boldsymbol{f}(\nabla \boldsymbol{u})$。

2.  **物质[坐标系](@entry_id:156346)无关性 (Material Frame-Indifference)**：该原理，也称为**客观性 (objectivity)**，要求[本构定律](@entry_id:178936)独立于观察者的[刚体运动](@entry_id:193355)。换言之，本构关系在叠加一个任意的刚体平移和旋转后应保持形式不变。速度梯度 $\nabla \boldsymbol{u}$ 本身不是客观的，因为在叠加一个刚体旋转时它会发生变化。然而，通过严谨的数学推导可以证明，为了满足[客观性原理](@entry_id:185412)，黏性应力 $\boldsymbol{\tau}$ 只能依赖于[速度梯度](@entry_id:261686)的对称部分，即**[形变率张量](@entry_id:184787) (rate-of-deformation tensor)** $\boldsymbol{D}$，而不能依赖于其反对称部分，即**[自旋张量](@entry_id:187346) (spin tensor)** $\boldsymbol{W}$ 。

    [速度梯度](@entry_id:261686)可以分解为：
    $$
    \nabla \boldsymbol{u} = \boldsymbol{D} + \boldsymbol{W}
    $$
    其中，
    $$
    \boldsymbol{D} = \frac{1}{2}(\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^{\top})
    $$
    $$
    \boldsymbol{W} = \frac{1}{2}(\nabla \boldsymbol{u} - (\nabla \boldsymbol{u})^{\top})
    $$
    $\boldsymbol{D}$ 描述了流体微元的拉伸和剪切变形速率，而 $\boldsymbol{W}$ 描述了其刚性旋转速率。[客观性原理](@entry_id:185412)的核心结论是，流体的黏性响应仅源于其形状的改变，而与其纯粹的刚性旋转无关。因此，本构关系简化为 $\boldsymbol{\tau} = \boldsymbol{f}(\boldsymbol{D})$。我们可以通过一个思想实验来验证这一点：在一个基础流场 $\boldsymbol{U}(\boldsymbol{x},t)$ 上叠加一个刚体旋转 $\boldsymbol{\Omega}(t) \times \boldsymbol{x}$，总[速度场](@entry_id:271461)为 $\boldsymbol{u} = \boldsymbol{U} + \boldsymbol{\Omega} \times \boldsymbol{x}$。计算表明，无论旋转角速度 $\boldsymbol{\Omega}$ 多大，所产生的[形变率张量](@entry_id:184787) $\boldsymbol{D}(\boldsymbol{u})$ 始终等于基础流场的[形变率张量](@entry_id:184787) $\boldsymbol{D}(\boldsymbol{U})$。由于黏性应力仅依赖于 $\boldsymbol{D}$，因此叠加的刚体旋转不会产生任何额外的黏性应力 。

3.  **材料各向同性 (Material Isotropy)**：该原理指出，流体的材料属性在所有方向上都是相同的。这意味着本构关系的形式不应因[坐标系](@entry_id:156346)的旋转而改变。数学上，对于任意的正交张量 $\boldsymbol{Q}$，本构函数 $\boldsymbol{f}$ 必须满足 $\boldsymbol{Q}\boldsymbol{f}(\boldsymbol{D})\boldsymbol{Q}^{\top} = \boldsymbol{f}(\boldsymbol{Q}\boldsymbol{D}\boldsymbol{Q}^{\top})$。满足此性质的函数被称为**[各向同性张量](@entry_id:195105)函数**。

#### 本构关系的一般形式

综合上述三个原理，我们可以推导出各向同性牛顿流体黏性应力的一般形式。根据[张量表示](@entry_id:180492)定理，一个将对称二阶张量 $\boldsymbol{D}$ [线性映射](@entry_id:185132)到另一个对称[二阶张量](@entry_id:199780) $\boldsymbol{\tau}$ 的[各向同性函数](@entry_id:750877)，其最普遍的形式必须是 $\boldsymbol{D}$ 和单位张量 $\boldsymbol{I}$ 的[线性组合](@entry_id:154743)。具体而言，$\boldsymbol{\tau}$ 可以表示为：
$$
\boldsymbol{\tau} = \lambda_v (\operatorname{tr}(\boldsymbol{D})) \boldsymbol{I} + 2\mu \boldsymbol{D}
$$
其中，$\operatorname{tr}(\boldsymbol{D}) = \nabla \cdot \boldsymbol{u}$ 是[形变率张量](@entry_id:184787)的迹，等于速度场的散度，表示流体微元的体积膨胀率。

方程中的两个标量系数 $\mu$ 和 $\lambda_v$ 是材料常数，分别称为**动力黏度 (dynamic viscosity)** 或**剪切黏度 (shear viscosity)**，以及**第二黏度系数 (second coefficient of viscosity)**。这个方程是描述可压缩[牛顿流体](@entry_id:263796)黏性应力的最通用形式 。

### 体积黏度与本构关系的不同表述

为了更清晰地[分离流](@entry_id:754694)体对[剪切变形](@entry_id:170920)和体积变形的响应，我们引入**体积黏度 (bulk viscosity)** 的概念。为此，可将[形变率张量](@entry_id:184787) $\boldsymbol{D}$ 分解为其**[偏张量](@entry_id:185837) (deviatoric part)** $\boldsymbol{D}'$ 和**各向同性部分 (isotropic part)**：
$$
\boldsymbol{D} = \boldsymbol{D}' + \frac{1}{3}(\operatorname{tr}(\boldsymbol{D}))\boldsymbol{I} = \boldsymbol{D}' + \frac{1}{3}(\nabla \cdot \boldsymbol{u})\boldsymbol{I}
$$
其中 $\boldsymbol{D}'$ 是无迹的，$\operatorname{tr}(\boldsymbol{D}') = 0$，它代表了纯剪切变形（即不改变体积的变形）。

将此分解代入通用[本构关系](@entry_id:186508)，经过整理可得 ：
$$
\boldsymbol{\tau} = 2\mu \boldsymbol{D}' + \left(\lambda_v + \frac{2}{3}\mu\right)(\nabla \cdot \boldsymbol{u})\boldsymbol{I}
$$
在这个形式中，第一项 $2\mu \boldsymbol{D}'$ 完全由剪切变形驱动，是黏性应力张量的无迹部分。第二项则与体积膨胀率 $\nabla \cdot \boldsymbol{u}$ 成正比，代表了由体积变化引起的各向同性应力。我们将括号中的系数定义为**体积黏度** $\zeta$（有时也用 $\kappa$ 表示）：
$$
\zeta \equiv \lambda_v + \frac{2}{3}\mu
$$
于是，本构关系可以等价地写为：
$$
\boldsymbol{\tau} = 2\mu \boldsymbol{D}' + \zeta (\nabla \cdot \boldsymbol{u})\boldsymbol{I}
$$
这种形式在物理上更为直观：剪切黏度 $\mu$ 衡量了流体对剪切变形的阻力，而体积黏度 $\zeta$ 衡量了流体对体积胀缩的黏性阻力。两种表述（使用 $(\mu, \lambda_v)$ 或 $(\mu, \zeta)$）是完[全等](@entry_id:273198)价的，它们之间的关系为 $\lambda_v = \zeta - \frac{2}{3}\mu$ 。

### [斯托克斯假设](@entry_id:195909)：物理诠释与推论

在许多[流体力学](@entry_id:136788)应用中，一个被称为**[斯托克斯假设](@entry_id:195909) (Stokes hypothesis)** 的简化被广泛采用。这个假设有几种等价的表述，但它们都指向同一个物理后果。

#### [热力学](@entry_id:141121)压力与力学压力

流体中的压力有两个不同的定义。**[热力学](@entry_id:141121)压力** $p$ 是一个状态量，通过[状态方程](@entry_id:274378)（如[理想气体定律](@entry_id:146757) $p=\rho R T$）与密度 $\rho$ 和温度 $T$ 等[状态变量](@entry_id:138790)相联系。而**力学压力** $p_m$ 则根据柯西应力张量 $\boldsymbol{\sigma}$ 定义，即正向应力的平均值的相反数：
$$
p_m \equiv -\frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})
$$
柯西[应力张量](@entry_id:148973)由[热力学](@entry_id:141121)压力和黏性应力组成：$\boldsymbol{\sigma} = -p\boldsymbol{I} + \boldsymbol{\tau}$。将此代入力学压力的定义，我们得到 $p_m$ 和 $p$ 之间的普适关系  ：
$$
p_m = -\frac{1}{3}\operatorname{tr}(-p\boldsymbol{I} + \boldsymbol{\tau}) = p - \frac{1}{3}\operatorname{tr}(\boldsymbol{\tau})
$$
利用 $\operatorname{tr}(\boldsymbol{\tau}) = 3\zeta(\nabla \cdot \boldsymbol{u})$，该关系可以进一步写为：
$$
p_m = p - \zeta (\nabla \cdot \boldsymbol{u})
$$
这个重要的方程表明，力学压力与[热力学](@entry_id:141121)压力之间的差异正比于体积黏度 $\zeta$ 和[体积膨胀](@entry_id:144241)率 $\nabla \cdot \boldsymbol{u}$ 的乘积。

[斯托克斯假设](@entry_id:195909)的一种物理表述是：**对于任何流动，力学压力等于[热力学](@entry_id:141121)压力**，即 $p_m = p$。根据上述方程，要使此等式对任意[可压缩流](@entry_id:747589)动（即任意 $\nabla \cdot \boldsymbol{u}$）都成立，唯一的可能是体积黏度为零 ：
$$
\zeta = 0
$$

#### 黏性应力张量的迹

[斯托克斯假设](@entry_id:195909)的另一种更直接的数学表述是：**黏性[应力张量](@entry_id:148973)是无迹的**，即 $\operatorname{tr}(\boldsymbol{\tau}) = 0$。从[本构关系](@entry_id:186508) $\boldsymbol{\tau} = \lambda_v (\nabla \cdot \boldsymbol{u}) \boldsymbol{I} + 2\mu \boldsymbol{D}$ 出发，取其迹可得：
$$
\operatorname{tr}(\boldsymbol{\tau}) = \operatorname{tr}(\lambda_v (\nabla \cdot \boldsymbol{u}) \boldsymbol{I}) + \operatorname{tr}(2\mu \boldsymbol{D}) = 3\lambda_v (\nabla \cdot \boldsymbol{u}) + 2\mu (\nabla \cdot \boldsymbol{u}) = (3\lambda_v + 2\mu)(\nabla \cdot \boldsymbol{u})
$$
要使 $\operatorname{tr}(\boldsymbol{\tau})=0$ 对任意 $\nabla \cdot \boldsymbol{u}$ 成立，其系数必须为零：
$$
3\lambda_v + 2\mu = 0 \quad \implies \quad \lambda_v = -\frac{2}{3}\mu
$$
这给出了第二黏度系数 $\lambda_v$ 与剪切黏度 $\mu$ 之间的特定关系 。

这两种表述是完全一致的。如果 $\lambda_v = -\frac{2}{3}\mu$，那么根据体积黏度的定义 $\zeta = \lambda_v + \frac{2}{3}\mu$，我们立即得到 $\zeta=0$。因此，[斯托克斯假设](@entry_id:195909)等价于假定流体的体积黏度为零。

### 物理机制与表现形式

剪切黏度 $\mu$ 和体积黏度 $\zeta$ 在[流体动力学](@entry_id:136788)中扮演着截然不同的角色，它们分别与不同类型的运动[能量耗散](@entry_id:147406)相关联。

一个极具启发性的例子是黏性松弛过程 。考虑一个[速度场](@entry_id:271461)，通过[亥姆霍兹分解](@entry_id:181767)将其分为无散的**[螺线管](@entry_id:261182)部分** $\boldsymbol{u}_s$（$\nabla \cdot \boldsymbol{u}_s = 0$）和无旋的**[势流](@entry_id:159985)部分** $\boldsymbol{u}_l$（$\nabla \times \boldsymbol{u}_l = \boldsymbol{0}$）。在只考虑黏性作用的简化动量方程 $\rho \frac{\partial \boldsymbol{u}}{\partial t} = \nabla \cdot \boldsymbol{\tau}$ 中，可以推导出这两个分量各自遵循的演化方程：
*   [螺线管](@entry_id:261182)（剪切/涡旋）部分： $\frac{\partial \boldsymbol{u}_s}{\partial t} = \frac{\mu}{\rho} \nabla^2 \boldsymbol{u}_s$
*   [势流](@entry_id:159985)（胀缩）部分： $\frac{\partial \boldsymbol{u}_l}{\partial t} = \frac{\zeta + \frac{4}{3}\mu}{\rho} \nabla^2 \boldsymbol{u}_l$

这清晰地表明：
*   **剪切黏度 $\mu$** 充当了剪切运动和[涡旋运动](@entry_id:198769)的[扩散](@entry_id:141445)系数，负责耗散由速度剪切产生的能量。
*   **体积黏度 $\zeta$** 与 $\frac{4}{3}\mu$ 一起，构成了胀缩运动的有效黏度，负责耗散由流体压缩和膨胀产生的能量。这一组合 $(\zeta + \frac{4}{3}\mu)$ 被称为**纵向黏度 (longitudinal viscosity)**。

这个例子揭示了[斯托克斯假设](@entry_id:195909)的一个重要推论：
*   对于**不可压缩流**，其定义为 $\nabla \cdot \boldsymbol{u} = 0$。在这种情况下，所有与 $\nabla \cdot \boldsymbol{u}$ 相关的项（包括含有 $\lambda_v$ 和 $\zeta$ 的项）在黏性应力本构关系中都自动消失。黏性应力简化为 $\boldsymbol{\tau} = 2\mu \boldsymbol{D}$（此时 $\boldsymbol{D}$ 与标准应变率张量 $\boldsymbol{S}$ 相同）。因此，[斯托克斯假设](@entry_id:195909)是否成立对不可压缩流的动力学行为**毫无影响**，该假设在此背景下是**冗余**的 。
*   对于**[可压缩流](@entry_id:747589)**，$\nabla \cdot \boldsymbol{u} \neq 0$，体积黏度 $\zeta$ 的作用就凸显出来。它直接影响声[波的衰减](@entry_id:271778)、激波的结构以及其他涉及体积变化的快速过程。要想通过实验测量一个流体的体积黏度，就必须设计一个产生非零[速度散度](@entry_id:264117)的流动，例如均匀的体积膨胀实验 。

### 动力学理论起源与有效性极限

[斯托克斯假设](@entry_id:195909)并非一个普适的物理定律，而是一个在特定条件下成立的近似。其根源和[适用范围](@entry_id:636189)必须从微观的分子动力学理论中寻找。

#### 微观理论基础

对于**稀薄[单原子气体](@entry_id:140562)**，气体分子间的碰撞可被视为弹性的、瞬时的二体碰撞。在这种理想情况下，通过求解玻尔兹曼方程的查普曼-恩斯科格（Chapman-Enskog）展开，可以在理论上证明，其体积黏度 $\zeta$ 在努森数 $Kn \to 0$ 的一阶近似下精确为零 。这是因为在纯粹的[平动能](@entry_id:170705)之间不存在[能量弛豫](@entry_id:136820)机制。因此，[斯托克斯假设](@entry_id:195909)对于稀薄[单原子气体](@entry_id:140562)（如氩气、氦气）是一个非常好的近似。

#### 假设的失效情形

然而，在许多其他情况下，[斯托克斯假设](@entry_id:195909)会失效：
1.  **多原子气体**：[多原子分子](@entry_id:268323)（如氮气 $N_2$、二氧化碳 $CO_2$）除了[平动能](@entry_id:170705)外，还拥有转动和[振动](@entry_id:267781)等**内能模式**。当气体被快速压缩时，其[平动](@entry_id:187700)温度会瞬时升高，但能量需要一定时间（弛豫时间 $\tau_{int}$）才能传递并重新分配到内能模式中。如果压缩过程的时间尺度与[弛豫时间](@entry_id:191572)相当（即频率 $\omega \sim 1/\tau_{int}$），就会出现平动温度与内能温度之间的瞬时不平衡。这种[能量弛豫](@entry_id:136820)的滞后效应在宏观上表现为非零的体积黏度  。因此，对于大多数多原子气体，$\zeta$ 不为零。

2.  **稠密流体**：在液体或高压气体中，分子间距很小，多体碰撞和持续的[分子间作用力](@entry_id:203760)变得非常重要。在体积变化过程中，分子间的[势能](@entry_id:748988)和动能需要重新分配。这种重新分配同样存在[弛豫时间](@entry_id:191572)，从而产生非零的体积黏度。因此，即使是单原子构成的稠密流体（如液氩），也具有不可忽略的体积黏度 。

3.  **高度非平衡流动**：[牛顿本构关系](@entry_id:752479)本身是基于流体偏离[局部热力学平衡](@entry_id:139579)不远的假设（即努森数 $Kn \ll 1$）。在**激波**内部或极度稀薄的气体流动中，梯度变化剧烈，$Kn$ 不再是一个小量。此时，流体分布函数严重偏离麦克斯韦[分布](@entry_id:182848)，线性的、局域的应力-[应变率](@entry_id:154778)关系失效，整个牛顿模型（包括[斯托克斯假设](@entry_id:195909)）都不再适用 。

### 在CFD简化模型中的应用

[斯托克斯假设](@entry_id:195909)的地位在不同的CFD简化模型中有所不同，这取决于这些模型对[速度散度](@entry_id:264117)的处理方式 。

*   **[Boussinesq近似](@entry_id:147239)**：该近似用于处理密度变化很小但[浮力](@entry_id:144145)效应重要的流动。其核心[运动学](@entry_id:173318)约束是 $\nabla \cdot \boldsymbol{u} = 0$，即视流体为不可压缩。如前所述，既然 $\nabla \cdot \boldsymbol{u}$ 为零，那么体积黏度项 $\zeta (\nabla \cdot \boldsymbol{u})\boldsymbol{I}$ 自动为零。因此，在Boussinesq模型中，[斯托克斯假设](@entry_id:195909)是**冗余**的。无论流体本身的 $\zeta$ 是否为零，模型预测的黏性力都与之无关。

*   **滞弹性近似 (Anelastic Approximation)**：该近似用于处理密度有显著空间变化（如在大气或天体物理中）但[马赫数](@entry_id:274014)很低的流动。它通过约束 $\nabla \cdot (\rho_0 \boldsymbol{u}) = 0$ 来过滤声波，其中 $\rho_0(\boldsymbol{x})$ 是背景密度剖面。这个约束通常意味着 $\nabla \cdot \boldsymbol{u} = -(\boldsymbol{u} \cdot \nabla \rho_0)/\rho_0 \neq 0$。由于[速度散度](@entry_id:264117)不为零，体积黏度项原则上是存在的。如果在模型中省略了这一项（这在许多实际的滞弹性求解器中是标准做法），就等同于**隐式地采纳了[斯托克斯假设](@entry_id:195909)**。在这种情况下，$\zeta=0$ 是一个**必要**的额外假设，而非冗余的。

综上所述，[牛顿本构关系](@entry_id:752479)和[斯托克斯假设](@entry_id:195909)是[流体力学](@entry_id:136788)理论体系中的基石。理解它们的推导过程、物理内涵、理论依据以及适用边界，对于准确地建立物理模型、正确地解读模拟结果、深刻地洞察[流体运动](@entry_id:182721)的内在机制都至关重要。