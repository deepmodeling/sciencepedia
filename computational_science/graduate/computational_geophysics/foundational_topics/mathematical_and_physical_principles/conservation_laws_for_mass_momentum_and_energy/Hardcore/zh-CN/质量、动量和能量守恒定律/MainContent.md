## 引言
质量、动量和[能量守恒](@entry_id:140514)定律是物理世界的基本支柱，在[计算地球物理学](@entry_id:747618)领域，它们构成了我们理解和模拟地球系统复杂行为的数学基石。从地幔的缓慢[对流](@entry_id:141806)到海洋的湍急环流，从火山的剧烈喷发到冰盖的消长，这些看似迥异的现象本质上都受到同一组核心物理法则的支配。然而，将这些抽象的物理原理转化为能够进行精确预测的实用计算模型，并非一个简单的过程。这其中存在一个关键的知识鸿沟：我们如何从一个有限体积内的宏观平衡关系，推导出适用于空间每一点的[偏微分方程](@entry_id:141332)？又如何根据具体问题的物理尺度，对这些复杂的方程进行合理的简化，从而在保证精度的前提下，使计算变得可行？

本文旨在系统地填补这一鸿沟，为读者构建一个从第一性原理到前沿应用的完整知识框架。我们将带领读者深入探索这些[守恒定律](@entry_id:269268)的内在逻辑和数学之美。

在接下来的“原理与机制”章节中，我们将追本溯源，详细展示如何从积分形式的平衡定律出发，通过严谨的数学推导得到点态的[偏微分方程组](@entry_id:172573)。我们还将重点剖析一系列在[地球物理学](@entry_id:147342)中至关重要的近似方法，如布辛涅斯克近似和[静力平衡](@entry_id:163498)，并量化其适用条件。随后，在“应用与跨学科联系”章节中，我们将通过一系列生动的实例，展示这些[守恒定律](@entry_id:269268)如何被灵活运用于解决从[水文地质学](@entry_id:750462)、[地球动力学](@entry_id:749832)到[高能天体物理学](@entry_id:159925)等不同领域的实际问题。最后，“动手实践”部分将提供具体的计算练习，让读者有机会亲手实现并验证本文所学的核心概念，将理论知识转化为真正的计算能力。

## 原理与机制

在[计算地球物理学](@entry_id:747618)中，模拟从[地幔对流](@entry_id:203493)到[海洋环流](@entry_id:180204)等各种现象，其核心是求解一组描述质量、动量和[能量守恒](@entry_id:140514)的[偏微分方程](@entry_id:141332)（PDEs）。这些[守恒定律](@entry_id:269268)源于物理学的基本原理，为我们提供了理解和预测地球系统行为的数学框架。本章旨在深入阐释这些基本[守恒定律](@entry_id:269268)的原理，展示它们如何从普适的积分形式转化为在计算中使用的[微分形式](@entry_id:146747)，并探讨在特定地球物理情境下为简化模型而引入的关键近似。

### 从积分平衡到[偏微分方程](@entry_id:141332)

物理[守恒定律](@entry_id:269268)最直观的表达形式是积分形式，它描述了一个有限控制体积（control volume）内的物理量如何随时间变化。考虑一个占据空间区域 $\Omega \subset \mathbb{R}^{3}$ 的连续介质。对于其中任何固定的[控制体积](@entry_id:143882) $\mathcal{V} \subset \Omega$，其边界为 $\partial\mathcal{V}$，一个广义的[守恒定律](@entry_id:269268)可以写作：

$$
\frac{\mathrm{d}}{\mathrm{d}t}\int_{\mathcal{V}} q \, \mathrm{d}V = \int_{\mathcal{V}} s \, \mathrm{d}V - \int_{\partial\mathcal{V}} \boldsymbol{J}\cdot\boldsymbol{n} \, \mathrm{d}A
$$

这里，$q$ 是某个物理量（如质量、动量或能量）的体密度，$\boldsymbol{J}$ 是该物理量穿过边界的**通量**（flux），$s$ 是体积内部的**源**（source）或**汇**（sink），$\boldsymbol{n}$ 是指向[控制体积](@entry_id:143882)外部的[单位法向量](@entry_id:178851)。这个方程的物理意义是：[控制体积](@entry_id:143882)内物理总量的变化率，等于体积内[源项](@entry_id:269111)的总和，减去通过边[界面流](@entry_id:264650)出的总量。

虽然积分形式具有普适性，但为了进行数值计算，我们通常需要将其转化为适用于空间中每一点的**局部**（local）或**点态**（pointwise）的[偏微分方程](@entry_id:141332)。这个转化过程包含几个关键的数学步骤，并且需要对所涉及的物理场和区域的**正则性**（regularity）或[光滑性](@entry_id:634843)做出一定假设 。

第一步，处理时间导数。由于控制体积 $\mathcal{V}$ 是固定的（这种描述被称为**[欧拉描述](@entry_id:264722)**），我们可以将时间导数移到积分号内部。这要求被积函数在时间上足够光滑。在弱形式理论中，我们要求映射 $t \mapsto \int_{\mathcal{V}} q \, \mathrm{d}V$ 是绝对连续的，这保证了时间导数 $\partial_t q$ 是一个[可积函数](@entry_id:191199)。于是，我们得到：

$$
\int_{\mathcal{V}} \frac{\partial q}{\partial t} \, \mathrm{d}V = \int_{\mathcal{V}} s \, \mathrm{d}V - \int_{\partial\mathcal{V}} \boldsymbol{J}\cdot\boldsymbol{n} \, \mathrm{d}A
$$

第二步，处理面积分。为了将所有项都表示为[体积分](@entry_id:171119)，我们使用**[散度定理](@entry_id:143110)**（Divergence Theorem），也称为[高斯定理](@entry_id:143110)。该定理将穿过闭合[曲面](@entry_id:267450)的通量与场在[曲面](@entry_id:267450)所围体积内的散度联系起来：

$$
\int_{\partial\mathcal{V}} \boldsymbol{J}\cdot\boldsymbol{n} \, \mathrm{d}A = \int_{\mathcal{V}} \nabla\cdot \boldsymbol{J} \, \mathrm{d}V
$$

[散度定理](@entry_id:143110)的成立同样需要满足一定的[正则性条件](@entry_id:166962)。在经典理论中，要求向量场 $\boldsymbol{J}$ 连续可微，且边界 $\partial\mathcal{V}$ 是分片光滑的。然而，在现代[偏微分方程理论](@entry_id:189232)中，这些条件可以大大减弱。例如，只要 $\mathcal{V}$ 是一个**[利普希茨域](@entry_id:751354)**（Lipschitz domain，即边界局部可用利普希茨[连续函数](@entry_id:137361)[图表示](@entry_id:273102)），并且 $\boldsymbol{J}$ 属于适当的[函数空间](@entry_id:143478)（如 $H(\mathrm{div};\Omega)$，其散度为[平方可积函数](@entry_id:200316)），[散度定理](@entry_id:143110)的广义形式依然成立 。

将散度定理应用于通量项后，[守恒定律](@entry_id:269268)变为：

$$
\int_{\mathcal{V}} \frac{\partial q}{\partial t} \, \mathrm{d}V = \int_{\mathcal{V}} s \, \mathrm{d}V - \int_{\mathcal{V}} \nabla\cdot \boldsymbol{J} \, \mathrm{d}V
$$

将所有项移到等式左边，我们得到一个对体积 $\mathcal{V}$ 的积分等于零：

$$
\int_{\mathcal{V}} \left( \frac{\partial q}{\partial t} + \nabla\cdot \boldsymbol{J} - s \right) \mathrm{d}V = 0
$$

第三步，局部化。由于上述方程对于**任意**控制体积 $\mathcal{V}$ 都成立，根据**变分法基本引理**（fundamental lemma of the calculus of variations），如果被积函数是连续的（或更一般地，是 $L^1$ 可积的），那么它必须在[几乎处处](@entry_id:146631)为零。这就给出了最终的点态[守恒定律](@entry_id:269268)：

$$
\frac{\partial q}{\partial t} + \nabla\cdot \boldsymbol{J} = s
$$

这个方程是所有后续讨论的基础。它将一个抽象的全局平衡关系，转化为了一个可以在空间和时间上求解的具体数学方程。

### 质量与[动量守恒](@entry_id:149964)

#### [质量守恒](@entry_id:204015)与不可压缩近似

将上述通用框架应用于[质量守恒](@entry_id:204015)，我们取 $q = \rho$（质量密度），通量 $\boldsymbol{J} = \rho \boldsymbol{u}$（质量通量，其中 $\boldsymbol{u}$ 是流体速度），并且通常没有质量源（$s=0$）。于是，我们得到**连续性方程**（continuity equation）：

$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \boldsymbol{u}) = 0
$$

这个方程也可以用**物质导数**（material derivative）$D/Dt \equiv \partial/\partial t + \boldsymbol{u} \cdot \nabla$ 来写，它描述了跟随流体[质点](@entry_id:186768)移动时物理量的变化率：

$$
\frac{D\rho}{Dt} + \rho \nabla \cdot \boldsymbol{u} = 0
$$

在许多地球物理应用中，尤其是在涉及液体（如海洋）或缓慢流动的固体（如地幔）时，流体的压缩性很小。一个极其实用的简化是**不可压缩近似**（incompressibility approximation），即假设流体密度不随压力变化，或者密度变化对动力学的影响可以忽略。在这种情况下，$D\rho/Dt = 0$，[连续性方程](@entry_id:195013)简化为：

$$
\nabla \cdot \boldsymbol{u} = 0
$$

这个条件表示流体体积在运动中是守恒的。然而，在地球内部的高压环境下，即使是岩石也会被压缩。假设完全不可压缩可能会引入误差。我们可以量化这种误差。对于一个具有恒定等温体积模量 $K$ 的材料，其定义为 $K = \rho (\partial p / \partial \rho)_T$。由此，密度的[物质导数](@entry_id:172646)与压力的物质导数相关联：$\frac{D\rho}{Dt} = \frac{\rho}{K} \frac{Dp}{Dt}$。代入完整的连续性方程，我们发现真实的[体积应变率](@entry_id:272471)应该是 ：

$$
\nabla \cdot \boldsymbol{u} = -\frac{1}{\rho} \frac{D\rho}{Dt} = -\frac{1}{K} \frac{Dp}{Dt}
$$

因此，采用不可压缩假设 $\nabla \cdot \boldsymbol{u} = 0$ 所引入的[质量守恒](@entry_id:204015)误差，其大小为 $\frac{1}{K} |\frac{Dp}{Dt}|$。在地质动力学模型中，如果一个岩石质点以速度 $\boldsymbol{u}$ 穿过一个具有很大[压力梯度](@entry_id:274112) $\nabla p$ 的区域，那么即使流速很慢，$\frac{Dp}{Dt} = \boldsymbol{u} \cdot \nabla p$ 也可能变得显著，导致不可压缩假设失效。

#### [动量守恒](@entry_id:149964)：从流体运动到[静力平衡](@entry_id:163498)

动量守恒是[牛顿第二定律](@entry_id:274217)在连续介质中的体现。对于[动量密度](@entry_id:271360) $q_i = \rho u_i$（动量的第 $i$ 个分量），其通量 $\boldsymbol{J}_i$ 不仅包括随流体一起运动的**平流**（advection）项 $\rho u_i \boldsymbol{u}$，还包括由于分子间相互作用或内部应力而产生的力通量。这些内部力由**柯西应力张量**（Cauchy stress tensor）$\boldsymbol{\sigma}$ 描述。因此，[动量方程](@entry_id:197225)写作：

$$
\frac{\partial (\rho \boldsymbol{u})}{\partial t} + \nabla \cdot (\rho \boldsymbol{u} \otimes \boldsymbol{u}) = \nabla \cdot \boldsymbol{\sigma} + \rho \boldsymbol{b}
$$

其中 $\boldsymbol{b}$ 是单位质量的[体力](@entry_id:174230)（如重力），$\nabla \cdot \boldsymbol{\sigma}$ 代表由应力不均匀性产生的[合力](@entry_id:163825)。使用[物质导数](@entry_id:172646)，这个方程可以更简洁地写成我们熟悉的**[柯西动量方程](@entry_id:187010)**：

$$
\rho \frac{D\boldsymbol{u}}{Dt} = \nabla \cdot \boldsymbol{\sigma} + \rho \boldsymbol{b}
$$

**应力与曳力**

应力张量 $\boldsymbol{\sigma}$ 是理解连续介质内部力如何传递的关键。在一个假想的切割面上，流体一侧对另一侧施加的作用力（单位面积）被称为**曳力**（traction）向量 $\boldsymbol{t}$。曳力的大小和方向取决于切割面的方位，即其法向量 $\boldsymbol{n}$。通过对一个无限小的四面体进行[动量平衡](@entry_id:193575)分析（柯西四面体论证），可以证明曳力向量与[应力张量](@entry_id:148973)之间存在一个基本的线性关系 ：

$$
\boldsymbol{t} = \boldsymbol{\sigma} \cdot \boldsymbol{n}
$$

这个关系，即**柯西应力定理**，是[连续介质力学](@entry_id:155125)的基石。它意味着，只要我们知道了某一点的[应力张量](@entry_id:148973)（一个二阶张量，在三维空间中有9个分量），我们就能计算出作用在通过该点的任意方向平面上的力。对于理想的[静止流体](@entry_id:187621)，应力是各向同性的，$\boldsymbol{\sigma} = -p\boldsymbol{I}$，其中 $p$ 是[静水压力](@entry_id:275365)，$\boldsymbol{I}$ 是单位张量。此时，曳力为 $\boldsymbol{t} = -p\boldsymbol{n}$，即压力总是垂直于作用面并指向内部。

**[角动量守恒](@entry_id:156798)与应力[张量的对称性](@entry_id:202126)**

除了[线动量](@entry_id:174467)，角动量也是守恒的。对于一个连续介质，在没有体力矩或体力偶（body couple）的经典情况下，角动量守恒定律要求柯西应力张量必须是**对称**的，即 $\sigma_{ij} = \sigma_{ji}$。这个性质将应力张量的独立分量从9个减少到6个。然而，在一些更复杂的材料模型中（例如，包含颗粒旋转效应的微极流体理论），可能会出现非对称的[应力张量](@entry_id:148973)。在这种情况下，为了维持角动量守恒，必须引入**[力偶应力](@entry_id:747952)**（couple stress）的概念，它描述了力偶矩的传递。在计算模型中，若本构关系导致[非对称应力](@entry_id:191550)，则必须通过引入[力偶应力](@entry_id:747952)通量或强制[离散梯度](@entry_id:171970)的对称性来确保[角动量守恒](@entry_id:156798) 。

**[静力平衡](@entry_id:163498)：动量方程的特例**

在许多地球物理问题中，如描述大气或海洋的[大尺度结构](@entry_id:158990)，或者地壳的长期应力状态，流体处于静止或近乎静止的状态。当 $\boldsymbol{u} = \boldsymbol{0}$ 时，[动量方程](@entry_id:197225)显著简化。此时，$\rho \frac{D\boldsymbol{u}}{Dt} = \boldsymbol{0}$，方程变为力的平衡：

$$
\nabla \cdot \boldsymbol{\sigma} + \rho \boldsymbol{b} = \boldsymbol{0}
$$

对于一个只受重力作用（$\boldsymbol{b} = \boldsymbol{g}$）的理想流体（$\boldsymbol{\sigma} = -p\boldsymbol{I}$），这个平衡方程变为著名的**静水压力方程**（hydrostatic equation）：

$$
\nabla p = \rho \boldsymbol{g}
$$

该方程表明，在[静止流体](@entry_id:187621)中，[压力梯度](@entry_id:274112)完全由重力体[力平衡](@entry_id:267186)。若重力指向 $-z$ 方向，即 $\boldsymbol{g} = (0, 0, -g)$，则压力只随深度变化，其关系为 $\frac{dp}{dz} = -\rho(z)g$。给定密度随深度的[分布](@entry_id:182848) $\rho(z)$ 和一个边界条件（如海平面压力），我们就可以通过积分计算出任意深度的压力 。这个简单的关系是理解地球内部压力分布的基础。

### [能量守恒](@entry_id:140514)与耗散

[能量守恒](@entry_id:140514)是第一类永动机不存在的体现，即能量不能无中生有，只能从一种形式转化为另一种。在[连续介质力学](@entry_id:155125)中，能量方程描述了动能、内能和[势能](@entry_id:748988)之间的转化和传递。

#### 机械能方程与[粘性耗散](@entry_id:143708)

我们可以通过将[动量方程](@entry_id:197225)与速度向量 $\boldsymbol{u}$ 做[点积](@entry_id:149019)来推导**[机械能](@entry_id:162989)方程**。经过一系列向量[恒等变换](@entry_id:264671)，我们得到 ：

$$
\rho \frac{D}{Dt}\left(\frac{1}{2} |\boldsymbol{u}|^2\right) = \nabla \cdot (\boldsymbol{\sigma} \cdot \boldsymbol{u}) - \boldsymbol{\sigma} : \nabla \boldsymbol{u} + \rho \boldsymbol{b} \cdot \boldsymbol{u}
$$

这个方程的各项有明确的物理意义：
- 左边项：跟随质点移动的单位体积动能的变化率。
- $\nabla \cdot (\boldsymbol{\sigma} \cdot \boldsymbol{u})$：应力所做功的通量。
- $\rho \boldsymbol{b} \cdot \boldsymbol{u}$：单位体积体力所做的功率。
- $-\boldsymbol{\sigma} : \nabla \boldsymbol{u}$：单位体积[应力功率](@entry_id:182907)，即应力做功使[材料变形](@entry_id:169356)的速率。

[应力功率](@entry_id:182907)项 $\boldsymbol{\sigma} : \nabla \boldsymbol{u}$ 是理解能量转化的关键。由于[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 是对称的，它与[速度梯度张量](@entry_id:270928) $\nabla \boldsymbol{u}$ 的[双点积](@entry_id:748648)等价于它与[速度梯度](@entry_id:261686)对称部分，即**[形变率张量](@entry_id:184787)** $\boldsymbol{D} = \frac{1}{2}(\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^\top)$ 的[双点积](@entry_id:748648)。即 $\boldsymbol{\sigma} : \nabla \boldsymbol{u} = \boldsymbol{\sigma} : \boldsymbol{D}$。

为了进一步区分可逆和不可逆的过程，我们将应力张量分解为压力部分和**偏应力**或**[粘性应力](@entry_id:261328)**（viscous stress）部分 $\boldsymbol{\tau}$：

$$
\boldsymbol{\sigma} = -p\boldsymbol{I} + \boldsymbol{\tau}
$$

于是，[应力功率](@entry_id:182907)可以分解为：

$$
\boldsymbol{\sigma} : \boldsymbol{D} = (-p\boldsymbol{I} + \boldsymbol{\tau}) : \boldsymbol{D} = -p (\boldsymbol{I}:\boldsymbol{D}) + \boldsymbol{\tau}:\boldsymbol{D} = -p(\nabla \cdot \boldsymbol{u}) + \boldsymbol{\tau}:\boldsymbol{D}
$$

这里，$-p(\nabla \cdot \boldsymbol{u})$ 代[表压力](@entry_id:147760)在体积变化（压缩或膨胀）时所做的可逆功。而第二项 $\Phi \equiv \boldsymbol{\tau}:\boldsymbol{D}$，被称为**粘性耗散函数**（viscous dissipation function）。它代表了[粘性力](@entry_id:263294)在[流体变形](@entry_id:271538)过程中所做的功，这部分机械能将不可逆地转化为内能（热量）。根据[热力学第二定律](@entry_id:142732)，这个过程总是耗散能量的，因此对于所有物理上可能的流动，必须有 $\Phi \ge 0$。

例如，对于一个作刚体旋转的流体，其[速度场](@entry_id:271461)为 $\boldsymbol{v}(\boldsymbol{x}) = \boldsymbol{\Omega} \times \boldsymbol{x}$。在这种情况下，[形变率张量](@entry_id:184787) $\boldsymbol{D}$ 为零，因此粘性耗散 $\Phi=0$。这符合我们的直觉：刚体旋转不涉及内部变形，因此没有粘性[摩擦生热](@entry_id:201286)。相反，在简单的[剪切流](@entry_id:266817) $\boldsymbol{v}(x,y,z) = (\gamma y, 0, 0)$ 中，[形变率张量](@entry_id:184787)非零，导致[粘性耗散](@entry_id:143708) $\Phi = \eta \gamma^2 > 0$（其中 $\eta$ 是[剪切粘度](@entry_id:141046)），[机械能](@entry_id:162989)被持续转化为热能 。

#### 完整能量方程

完整的[能量守恒](@entry_id:140514)（热力学第一定律）必须同时考虑机械能和**内能**（internal energy）。一个常见的形式是关于温度 $T$ 的方程：

$$
\rho c_p \frac{DT}{Dt} = \nabla \cdot (k \nabla T) + \Phi + \rho H + \alpha T \frac{Dp}{Dt}
$$

其中 $c_p$ 是定[压比](@entry_id:137698)热容，$k$ 是[热导率](@entry_id:147276)，$\Phi$ 是前面定义的粘性耗散， $H$ 是单位质量的内部热源（如[放射性衰变](@entry_id:142155)[生热](@entry_id:167810)），$\alpha$ 是热膨胀系数。方程右边的各项代表了改变一个流体质点温度的几种方式：
1.  $\nabla \cdot (k \nabla T)$：**[热传导](@entry_id:147831)**（heat conduction），由温度梯度驱动的热量[扩散](@entry_id:141445)。
2.  $\Phi$：**粘性耗散**，由粘性摩擦产生的热量。
3.  $\rho H$：**内部热源**。
4.  $\alpha T \frac{Dp}{Dt}$：**[绝热压缩](@entry_id:142708)/膨胀**生热或致冷。当一个流体质点被压缩（$Dp/Dt > 0$），它会升温；反之，膨胀时会降温。

### 地球物理模型中的近似与简化

求解包含上述所有物理过程的全套方程在计算上是极其昂贵的，而且对于特定问题可能是不必要的。因此，在[计算地球物理学](@entry_id:747618)中，一个核心技能是基于[尺度分析](@entry_id:153681)（scaling analysis）来判断哪些项是主导的，哪些可以被安全地忽略，从而构建出更简单但依然能抓住核心物理的近似模型。

#### 布辛涅斯克近似 (Boussinesq Approximation)

在模拟[地幔对流](@entry_id:203493)或大尺度[海洋环流](@entry_id:180204)时，流体速度非常缓慢。**布辛涅斯克近似**是一个强有力的工具，它基于以下观察：密度的变化非常小，以至于它们在除了**[浮力](@entry_id:144145)项**（buoyancy term）$\rho\boldsymbol{g}$ 之外的所有项中都可以被忽略。具体来说，这意味着：
- 在连续性方程中，我们假设流体是不可压缩的，即 $\nabla \cdot \boldsymbol{u} = 0$。
- 在惯性项 $\rho D\boldsymbol{u}/Dt$ 中，我们使用一个参考密度 $\rho_0$。
- 在动量方程的[浮力](@entry_id:144145)项中，我们保留密度的变化，因为它驱动了整个[对流](@entry_id:141806)系统，通常写作 $\rho = \rho_0 (1 - \alpha (T-T_0))$。

在能量方程中，布辛涅斯克近似通常也涉及对生热项的简化。例如，我们可以评估[绝热压缩](@entry_id:142708)加热项 $\alpha T \frac{Dp}{Dt}$ 相对于热[平流](@entry_id:270026)项 $\rho c_p \frac{DT}{Dt}$ 的重要性 。通过尺度分析，可以定义一个无量纲比率 $R$：

$$
R \equiv \frac{|\alpha T \frac{Dp}{Dt}|}{|\rho c_p \frac{DT}{Dt}|} \sim \frac{\alpha T (\rho g U)}{\rho c_p (U \Delta T / L)} = \frac{\alpha g L}{c_p} \frac{T}{\Delta T} = Di \frac{T}{\Delta T}
$$

其中 $Di = \frac{\alpha g L}{c_p}$ 是**耗散数**（dissipation number），它衡量了在一个[对流](@entry_id:141806)元从底部上升到顶部过程中，因膨胀而损失的内能与总热能的比值。对于[地幔对流](@entry_id:203493)的典型参数，这个比率 $R$ 大约是 $0.4$ 。这个数值小于1，表明压缩加热是一个次要项，忽略它是合理的，但不是完全可以忽略的。这为在特定精度要求下简化能量方程提供了定量依据。

#### 非弹性与刚盖近似

另两种在地球物理[流体力学](@entry_id:136788)中常见的近似是**非弹性近似**（anelastic approximation）和**刚盖近似**（rigid-lid approximation）。

**非弹性近似**的目标是过滤掉[传播速度](@entry_id:189384)极快的声波，以便在[数值模拟](@entry_id:137087)中使用更大的时间步长来研究较慢的现象，如重力[内波](@entry_id:261048)或[对流](@entry_id:141806)。其有效性取决于声波的时间尺度与我们感兴趣的现象的时间尺度是否充分分离。通过对能量收支的尺度分析，可以发现该近似的有效性由两个条件控制 ：
1.  [声学模](@entry_id:263916)式所携带的能量必须很小。这要求马赫数 $\mathrm{Ma} = U/c_s$（其中 $c_s$ 是声速）很小，具体为 $\mathrm{Ma}^2 \le \varepsilon$，$\varepsilon$ 是允许的能量误差。
2.  [声学](@entry_id:265335)和浮力（由布伦特-瓦萨拉频率 $N$ 表征）时间尺度的耦合必须很弱。这要求 $(\mathrm{Ma}/\mathrm{Fr})^2 \le \varepsilon$，其中[弗劳德数](@entry_id:271895) $\mathrm{Fr} = U/(NL)$。

综合这两个条件，我们得到最大允许马赫数的限制：$\mathrm{Ma}_{\max} = \sqrt{\varepsilon} \min(1, \mathrm{Fr})$。这个结果为何时可以安全地使用非弹性近似提供了明确的、基于[能量守恒](@entry_id:140514)的准则。

**刚盖近似**常用于海洋模型中，它通过假设海面是刚性的、不可变形的，从而消除了传播速度很快的[表面重力](@entry_id:160565)波。在积分[质量守恒](@entry_id:204015)方程 $\frac{\partial \eta}{\partial t} + \nabla \cdot (H\boldsymbol{u}) = 0$ 中（其中 $\eta$ 是海面高度），这个近似直接将 $\partial \eta / \partial t$ 设为零。这种近似的[相对误差](@entry_id:147538)可以通过比较被忽略项的振幅 $|\partial \eta / \partial t| = \omega \hat{\eta}$ 与一个具有相同空间尺度 $k$ 的[表面重力](@entry_id:160565)波的参考通量散度振幅 $\omega_{gw} \hat{\eta}$ 来量化 。这个误差就是频率之比：

$$
\varepsilon = \frac{\omega}{\omega_{gw}} = \frac{\omega}{k\sqrt{gH}}
$$

因此，刚盖近似对于频率远低于同尺度[表面重力](@entry_id:160565)波的低频运动（如大尺度[海洋环流](@entry_id:180204)）是有效的。

### 涌现的守恒律：[位涡](@entry_id:276663)

除了质量、动量和能量这些基本守恒量之外，流体系统在特定条件下还可以表现出更复杂的**涌现守恒律**（emergent conservation laws）。其中最著名和最强大的之一就是**[位涡守恒](@entry_id:270380)**（potential vorticity conservation）。

对于一个旋转、分层、无粘、绝热的流体，可以证明一个被称为**厄特尔[位涡](@entry_id:276663)**（Ertel Potential Vorticity, PV）的标量 $q$ 是物质守恒的，即跟随流体[质点](@entry_id:186768)其值保持不变（$Dq/Dt = 0$）。其定义为：

$$
q \equiv \frac{\boldsymbol{\omega}_a \cdot \nabla \theta}{\rho}
$$

其中 $\boldsymbol{\omega}_a = \nabla \times \boldsymbol{u} + 2\boldsymbol{\Omega}$ 是[绝对涡度](@entry_id:262794)（相对涡度与[行星涡度](@entry_id:265327)之和），$\theta$ 是一个物质守恒的标量，如位温或势密度。[位涡守恒](@entry_id:270380)的推导过程巧妙地结合了动量方程的涡度形式、质量守恒方程和[热力学](@entry_id:141121)方程（$D\theta/Dt=0$）。

[位涡守恒](@entry_id:270380)是一个极其强大的动力学约束。它将流体的运动（涡度）、旋转（[行星涡度](@entry_id:265327) $2\boldsymbol{\Omega}$）和分层（由 $\nabla\theta$ 体现）联系在一起。例如，如果一个流体柱被垂直拉伸，其厚度减小，为了保持[位涡守恒](@entry_id:270380)，它的相对涡度就必须改变。这解释了许多大气和海洋中的现象，如高空急流的形成和海洋涡旋的行为。

值得强调的是，[位涡守恒](@entry_id:270380)并不意味着能量转换的停止。在一个无粘、绝热的系统中，总能量是守恒的，但动能和势能之间仍然可以通过压力做功进行可逆的转换。[位涡守恒](@entry_id:270380)限制了流体质点可以经历的运动路径，从而制约了能量转换的途径，但它本身不是一个[能量守恒](@entry_id:140514)定律 。

总之，从基本的积分平衡出发，我们推导出了描述连续介质运动和演化的[偏微分方程组](@entry_id:172573)。通过对这些方程的分析和简化，我们不仅能模拟复杂的地球物理现象，还能深入理解其背后的物理机制，如[静力平衡](@entry_id:163498)、能量耗散，以及如[位涡守恒](@entry_id:270380)这类深刻的动力学原理。