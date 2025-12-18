## 引言
在物理学和工程学的广阔天地中，质量、动量和[能量守恒](@entry_id:140514)定律是颠扑不破的基石。对于致力于多物理场耦合仿真的研究生和学者而言，这些定律不仅是理论知识，更是构建和理解复杂系统数值模型的通用语言。然而，从抽象的物理法则到精确的数学方程，再到可靠的计算机代码，这一过程充满了挑战。它要求我们不仅理解每个定律的独立意义，更要洞悉它们如何相互关联、如何在多相、多组分、移动边界等复杂场景下扩展，以及如何转化为稳健的[数值算法](@entry_id:752770)。本文旨在弥合这一知识鸿沟，为读者提供一个关于[守恒定律](@entry_id:269268)的系统性、深层次的视角。

在接下来的内容中，我们将踏上一段从理论到实践的旅程。在“原理与机制”一章，我们将建立[守恒定律](@entry_id:269268)的通用数学框架，并由此严谨推导单相、多相及多组分系统下的核心控制方程，同时探讨保证模型物理有效性的基本准则。随后，在“应用与交叉学科联系”一章，我们将通过[计算流体动力学](@entry_id:147500)、天体物理学、电化学等领域的生动实例，展示这些定律如何解决真实世界的工程与科学问题。最后，通过一系列“动手实践”练习，您将有机会亲手应用这些原理，巩固对理论的理解并提升解决问题的能力。

## 原理与机制

在多物理场耦合仿真的宏伟蓝图之中，质量、动量和[能量守恒](@entry_id:140514)定律是构建一切模型的基石。这些定律不仅是物理世界的普适法则，也是连接不同物理现象的桥梁。本章旨在深入剖析这些[守恒定律](@entry_id:269268)在[连续介质力学](@entry_id:155125)框架下的数学表述、物理内涵及其在高级应用和数值建模中的关键作用。我们假定读者已具备基础的矢量分析和[连续介质力学](@entry_id:155125)知识，本章将在此基础上构建一个系统而严谨的理论体系。

### [守恒定律](@entry_id:269268)的通用框架

在深入探讨具体的物理定律之前，我们首先建立一个适用于任何守恒广延量（extensive quantity）的通用数学框架。一个广延量是指其大小与系统尺寸成正比的物理量，如质量、动量或总能量。

考虑一个固定的、边界光滑的控制体（Control Volume）$V$，其边界为 $\partial V$，向外的[单位法向量](@entry_id:178851)为 $\mathbf{n}$。对于某个广延量，我们可以定义其密度场 $\psi(\mathbf{x}, t)$，使得在体积 $V$ 内该量的总量为 $\int_V \psi \, dV$。该量在[控制体](@entry_id:143882)内的变化遵循以下基本原则：

**总量的时间变化率 = 净流入速率 + 体内源的生成速率**

这可以精确地表述为一个积分形式的平衡律。我们将其中的各项进行分解：

1.  **储存项 (Storage Term)**：控制体内总量的累积或消耗速率，由对时间的[全导数](@entry_id:137587)表示：
    $$
    \text{储存项} = \frac{d}{dt} \int_V \psi \, dV
    $$

2.  **通量项 (Flux Term)**：物质穿过[控制体](@entry_id:143882)边界 $\partial V$ 的净速率。通量通常包含两种机制：
    *   **[对流通量](@entry_id:158187) (Advective Flux)**：物质随连续介质的宏观运动（[速度场](@entry_id:271461)为 $\mathbf{v}$）而被携带。其[通量矢量](@entry_id:273577)为 $\psi \mathbf{v}$。
    *   **非[对流通量](@entry_id:158187) (Non-convective Flux)**：通过其他物理机制（如[扩散](@entry_id:141445)、热传导或应力）传递。我们用一个通用的非[对流通量](@entry_id:158187)矢量 $\mathbf{j}_\psi$ 来表示。
    因此，总[通量矢量](@entry_id:273577)为 $\mathbf{F}_\psi = \psi \mathbf{v} + \mathbf{j}_\psi$。根据[高斯散度定理](@entry_id:188065)的习惯，流出控制体的净通量为 $\int_{\partial V} \mathbf{F}_\psi \cdot \mathbf{n} \, dS$。因此，净流入速率是其相反数。

3.  **[源项](@entry_id:269111) (Source Term)**：控制体内部由于与其他物理过程的耦合而产生或消耗该物质的速率。我们用体积源密度 $s_\psi$ 来描述，其在整个体积内的总生成速率为：
    $$
    \text{源项} = \int_V s_\psi \, dV
    $$

综合以上各项，我们得到了[守恒定律](@entry_id:269268)的通用积分形式 ()：

$$
\frac{d}{dt} \int_V \psi \, dV = - \int_{\partial V} \left( \psi \mathbf{v} + \mathbf{j}_\psi \right) \cdot \mathbf{n} \, dS + \int_V s_\psi \, dV
$$

这个方程是后续所有讨论的出发点。通过为 $\psi$, $\mathbf{j}_\psi$ 和 $s_\psi$ 指定具体的物理意义，我们便能得到质量、动量和能量的守恒方程。

### 单相连续介质的基本[守恒定律](@entry_id:269268)

现在，我们将上述通用框架应用于牛顿力学中的三大基本[守恒定律](@entry_id:269268)。

#### 质量守恒（连续性方程）

质量是物质最基本的属性。对于一个单组分连续介质，质量是严格守恒的。

*   [守恒量](@entry_id:150267)密度为质量密度：$\psi = \rho(\mathbf{x}, t)$。
*   质量不能通过非[对流](@entry_id:141806)方式（如[扩散](@entry_id:141445)）产生或消失，因此非[对流通量](@entry_id:158187)为零：$\mathbf{j}_\psi = \mathbf{0}$。
*   质量不能被创造或毁灭，因此体积源项为零：$s_\psi = 0$。

将这些代入通用平衡律 ()，我们得到[质量守恒的积分形式](@entry_id:750704)：

$$
\frac{d}{dt} \int_V \rho \, dV = - \int_{\partial V} \rho \mathbf{v} \cdot \mathbf{n} \, dS
$$

该式表明，控制体内质量的变化率等于通过其边界的净[质量流](@entry_id:143424)入率。若被积函数足够光滑，我们可以应用[高斯散度定理](@entry_id:188065)将面积分转化为[体积分](@entry_id:171119)，并考虑到[控制体](@entry_id:143882) $V$ 是固定的，从而得到其[微分形式](@entry_id:146747)，即**[连续性方程](@entry_id:195013) (Continuity Equation)**：

$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) = 0
$$

#### [线性动量守恒](@entry_id:165717)

根据[牛顿第二定律](@entry_id:274217)，一个物体的动量变化率等于作用在其上的合外力。我们将此定律应用于控制体中的连续介质。

*   守恒量是动量，这是一个矢量。其密度为[动量密度](@entry_id:271360)：$\boldsymbol{\psi} = \rho \mathbf{v}$。
*   动量的来源是作用在连续介质上的力。力分为两类：
    *   **体力 (Body Forces)**：作用于整个体积，如重力。单位质量的[体力](@entry_id:174230)为 $\mathbf{b}$，因此动量的体积源项为 $s_\psi = \rho \mathbf{b}$。
    *   **面力 (Surface Forces)**：作用于[控制体](@entry_id:143882)的边界，由周围介质施加。这种力通过内部应力来传递。

为了描述面力，我们引入一个核心概念：**柯西[应力张量](@entry_id:148973) (Cauchy Stress Tensor)** $\boldsymbol{\sigma}$ ()。根据柯西应力定理，作用在具有[单位法向量](@entry_id:178851) $\mathbf{n}$ 的微小表面上的[面力矢量](@entry_id:189429)（或称**牵[引力](@entry_id:175476) (traction)**）$\mathbf{t}(\mathbf{n})$ 与 $\mathbf{n}$ 之间存在[线性关系](@entry_id:267880)，这个关系由[应力张量](@entry_id:148973)定义：

$$
\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma} \mathbf{n}
$$

在此定义下，$\boldsymbol{\sigma}$ 是一个二阶张量，它完全描述了介质内某一点的应力状态。因此，作用在整个边界 $\partial V$ 上的总面力为 $\int_{\partial V} \boldsymbol{\sigma} \mathbf{n} \, dS$。这个面力构成了动量的另一种“源”。

然而，为了与通用输运方程的形式保持一致，更深刻的理解是将应力视为动量的非[对流通量](@entry_id:158187)。作用于[控制体](@entry_id:143882)的面力 $\boldsymbol{\sigma}\mathbf{n}$ 是外部介质传递给控制体的动量。根据[牛顿第三定律](@entry_id:166652)，这也是[控制体](@entry_id:143882)通过该界面“流失”给外部介质的动量流的反向。因此，我们可以将非[对流](@entry_id:141806)的[动量通量](@entry_id:199796)定义为 $\mathbf{J}_\psi = -\boldsymbol{\sigma}$。

将以上各部分组合起来，动量守恒的积分形式为 ()：

$$
\frac{d}{dt}\int_{V} \rho\mathbf{v} \, dV = - \int_{\partial V} (\rho\mathbf{v} \otimes \mathbf{v})\mathbf{n} \, dS + \int_{\partial V} \boldsymbol{\sigma}\mathbf{n} \, dS + \int_{V} \rho\mathbf{b} \, dV
$$

这里，$\rho\mathbf{v} \otimes \mathbf{v}$ 是一个[二阶张量](@entry_id:199780)，代表动量的[对流通量](@entry_id:158187)。应用[高斯散度定理](@entry_id:188065)，我们得到动量守恒的微分形式，即**[柯西运动方程](@entry_id:204126) (Cauchy's Equation of Motion)** ()：

$$
\frac{\partial (\rho\mathbf{v})}{\partial t} + \nabla \cdot (\rho \mathbf{v} \otimes \mathbf{v}) = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b}
$$

利用[连续性方程](@entry_id:195013)，上式可以写成更熟悉的使用物质导数 $\frac{D(\cdot)}{Dt} = \frac{\partial(\cdot)}{\partial t} + \mathbf{v} \cdot \nabla(\cdot)$ 的形式：

$$
\rho \frac{D\mathbf{v}}{Dt} = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b}
$$

值得注意的是，[热力学](@entry_id:141121)压力 $p$ 与柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 不同。$\boldsymbol{\sigma}$ 可以分解为各向同性[部分和](@entry_id:162077)偏（剪切）部分。[机械压力](@entry_id:263227)定义为平均[正应力](@entry_id:260622)的相反数，$p_m = -\frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})$。在平衡状态下的[理想流体](@entry_id:161909)中，$\boldsymbol{\sigma} = -p\mathbf{I}$，此时 $p_m = p$。但在非平衡的粘性流中，由于体积粘性的存在，这两者通常不相等 ()。

#### [能量守恒](@entry_id:140514)

[能量守恒](@entry_id:140514)是[热力学第一定律](@entry_id:146485)在连续介质中的体现：[控制体](@entry_id:143882)中总能量的变化率等于对[控制体](@entry_id:143882)做的功和向其传递的热量之和。

*   [守恒量](@entry_id:150267)密度为单位体积的总能量，即 $\psi = \rho E$，其中 $E = e + \frac{1}{2}|\mathbf{v}|^2$ 是比总能（单位质量的总能量），由比内能 $e$ 和比动能 $\frac{1}{2}|\mathbf{v}|^2$ 构成 ()。
*   能量的非[对流通量](@entry_id:158187) $\mathbf{j}_\psi$ 包括两个部分：
    1.  **热传导 (Heat Conduction)**：由热流矢量 $\mathbf{q}$ 描述。按照惯例，$\mathbf{q}$ 指向热量流出的方向。
    2.  **应力做功 (Work by Stresses)**：边界上的面力 $\boldsymbol{\sigma}\mathbf{n}$ 对[速度场](@entry_id:271461) $\mathbf{v}$ 做功，其功率为 $(\boldsymbol{\sigma}\mathbf{n})\cdot\mathbf{v}$。这代表能量的流入，因此在流出通量中记为 $-\boldsymbol{\sigma}\mathbf{v}$。
    综合起来，总的非[对流](@entry_id:141806)[能量通量](@entry_id:266056)为 $\mathbf{j}_E = \mathbf{q} - \boldsymbol{\sigma}\mathbf{v}$ ()。
*   能量的体积源项 $s_\psi$ 也包括两个部分：
    1.  **[体力](@entry_id:174230)做功 (Work by Body Forces)**：[体力](@entry_id:174230) $\rho\mathbf{b}$ 做功的[功率密度](@entry_id:194407)为 $\rho\mathbf{b}\cdot\mathbf{v}$。
    2.  **体积生热 (Volumetric Heating)**：如辐射吸收或焦耳热，由 $r$ 表示。
    总的体积源为 $s_E = \rho\mathbf{b}\cdot\mathbf{v} + r$ ()。

将这些项代入通用平衡律，得到总[能量守恒的积分形式](@entry_id:202417)：

$$
\frac{d}{dt}\int_{V} \rho E \, dV = - \int_{\partial V} \left( \rho E \mathbf{v} + \mathbf{q} - \boldsymbol{\sigma}\mathbf{v} \right) \cdot \mathbf{n} \, dS + \int_{V} (\rho\mathbf{b}\cdot\mathbf{v} + r) \, dV
$$

其对应的微分形式为 ()：

$$
\rho \frac{DE}{Dt} = \nabla\cdot(\boldsymbol{\sigma}\mathbf{v}) - \nabla\cdot\mathbf{q} + \rho\mathbf{b}\cdot\mathbf{v} + r
$$

这个方程优雅地统一了机械能和热能，是[热力学](@entry_id:141121)与[流体力学](@entry_id:136788)耦合的核心。

### 框架的延伸：高级应用

基于上述基本定律，我们可以将其推广到更复杂的[多物理场](@entry_id:164478)场景中。

#### 多组分系统：[组分守恒](@entry_id:197272)

在许多应用中，例如[化学反应](@entry_id:146973)流或[合金凝固](@entry_id:148532)，我们需要追踪混合物中各个组分的演化。

考虑一个包含 $N$ 个组分的混合物。我们引入**[质量分数](@entry_id:161575) (mass fraction)** $Y_k = \rho_k / \rho$，其中 $\rho_k$ 是组分 $k$ 的分密度，$\rho = \sum_k \rho_k$ 是混合物总密度。[质量分数](@entry_id:161575)满足约束 $\sum_{k=1}^{N} Y_k = 1$ ()。

每个组分自身的运动速度 $\mathbf{u}_k$ 可能与混合物的**[质量平均速度](@entry_id:149575) (mass-averaged velocity)** $\mathbf{u} = (\sum_k \rho_k \mathbf{u}_k) / \rho$ 不同。这种相对运动导致了**[扩散](@entry_id:141445) (diffusion)**。我们定义组分 $k$ 的**[扩散](@entry_id:141445)速度 (diffusion velocity)** 为 $\mathbf{V}_k = \mathbf{u}_k - \mathbf{u}$。

组分 $k$ 的质量通量可以分解为[对流](@entry_id:141806)部分和[扩散](@entry_id:141445)部分：$\rho_k \mathbf{u}_k = \rho_k \mathbf{u} + \rho_k \mathbf{V}_k$。第二项 $\mathbf{J}_k = \rho_k \mathbf{V}_k$ 被称为**[扩散](@entry_id:141445)质量通量 (diffusive mass flux)**。根据[质量平均速度](@entry_id:149575)的定义，所有组分的[扩散](@entry_id:141445)质量通量之和恒为零 ()：

$$
\sum_{k=1}^{N} \mathbf{J}_k = \sum_{k=1}^{N} \rho_k(\mathbf{u}_k - \mathbf{u}) = \sum_{k=1}^{N} \rho_k \mathbf{u}_k - \mathbf{u}\sum_{k=1}^{N} \rho_k = \rho\mathbf{u} - \mathbf{u}\rho = \mathbf{0}
$$

这个零和约束是多组分系统建模中的一个基本[自洽性](@entry_id:160889)要求。

如果组分 $k$ 还参与[化学反应](@entry_id:146973)，其[质量生成](@entry_id:161427)速率为 $\dot{\omega}_k$，则组分 $k$ 的[质量守恒](@entry_id:204015)方程（即**组分[连续性方程](@entry_id:195013)**）为 ()：

$$
\frac{\partial (\rho Y_k)}{\partial t} + \nabla \cdot (\rho Y_k \mathbf{u}) = - \nabla \cdot \mathbf{J}_k + \dot{\omega}_k
$$

或使用物质导数形式：

$$
\rho \frac{DY_k}{Dt} + \nabla \cdot \mathbf{J}_k = \dot{\omega}_k
$$

要封闭这个[方程组](@entry_id:193238)，需要为[扩散通量](@entry_id:748422) $\mathbf{J}_k$ 提供一个本构关系，例如[Fick定律](@entry_id:155177)。一种简化的**混合平均[Fick定律](@entry_id:155177)**模型将通量表示为与质量分数梯度成正比：$\mathbf{J}_k \approx - \rho D_k \nabla Y_k$。然而，这种简单的形式通常不满足零和约束。在数值实践中，一种常见的做法是只求解 $N-1$ 个组分的方程，第 $N$ 个组分的通量则由约束 $\mathbf{J}_N = - \sum_{k=1}^{N-1} \mathbf{J}_k$ 来确定，从而强制保证总[质量守恒](@entry_id:204015) ()。

#### 多相系统：平均化与相间传递

当系统中存在多个不互溶的相（如气-液[两相流](@entry_id:153752)）时，直接求解每个相内部的瞬时场通常是不现实的。取而代之的方法是进行**体积平均 (volume averaging)**，从而得到宏观的、可在较大尺度上求解的方程。

我们引入一个关键变量：**相体积分数 (phase volume fraction)** $\alpha_i$，它表示在任一微元体积内，第 $i$ 相所占的比例。所有相的[体积分数](@entry_id:756566)之和为1：$\sum_i \alpha_i = 1$。通过对微观[守恒定律](@entry_id:269268)进行平均，我们得到每个相的宏观守恒方程，即**相平衡方程 (phasic balance equations)** ()。

以质量守恒为例，第 $i$ 相的平均方程形式为：

$$
\frac{\partial (\alpha_i \rho_i)}{\partial t} + \nabla \cdot (\alpha_i \rho_i \mathbf{v}_i) = \Gamma_i
$$

这里，$\rho_i$ 和 $\mathbf{v}_i$ 是第 $i$ 相的本征密度和[平均速度](@entry_id:267649)。右侧的 $\Gamma_i$ 是**相间[质量传递](@entry_id:151080)项 (interfacial mass transfer term)**，表示由于[相变](@entry_id:147324)（如蒸发或冷凝）而从其他相转移到第 $i$ 相的质量速率。由于质量在[相界面](@entry_id:172947)上是守恒的，即一个相失去的质量必须被另一个相获得，因此所有相的[质量传递](@entry_id:151080)项之和必为零：$\sum_i \Gamma_i = 0$。

同样，动量和能量的相平衡方程也会包含相间传递项，分别代表相间作用力（如拖曳力、升力）和相间热量传递。根据[牛顿第三定律](@entry_id:166652)和[能量守恒](@entry_id:140514)，这些相间动量和能量的传递项在所有相之间求和后也必为零 ()。

这个性质的直接结果是，如果我们将所有相的[平衡方程](@entry_id:172166)相加，所有的相间传递项都会抵消，从而得到一个描述整个**混合物 (mixture)** 的守恒方程。例如，将所有相的质量守恒方程相加，即可得到混合物的质量守恒方程：

$$
\frac{\partial \rho_m}{\partial t} + \nabla \cdot (\rho_m \mathbf{u}_m) = 0
$$

其中 $\rho_m = \sum_i \alpha_i \rho_i$ 是混合物密度，$\mathbf{u}_m = (\sum_i \alpha_i \rho_i \mathbf{v}_i) / \rho_m$ 是混合物的[质量平均速度](@entry_id:149575)。这表明，无论内部的相间传递多么复杂，混合物作为一个整体仍然严格遵守[守恒定律](@entry_id:269268)。

#### 间断与界面：[跳跃条件](@entry_id:750965)

在一些情况下，相与相之间的界面可以被视为一个厚度为零的数学[曲面](@entry_id:267450) $\Sigma(t)$，物理量在该界面两侧可能发生跳跃。[守恒定律](@entry_id:269268)在这种[间断面](@entry_id:180188)上表现为**[跳跃条件](@entry_id:750965) (jump conditions)**。

考虑一个以法向速度 $s$ 运动的界面，其[单位法向量](@entry_id:178851) $\mathbf{n}$ 从“-”侧指向“+”侧。对于任意物理量 $a$，其在界面上的跳跃定义为 $[a] \equiv a^{+} - a^{-}$。通过在一个跨越界面的、厚度趋于零的“药丸盒”(pillbox) [控制体](@entry_id:143882)上应用积分形式的[守恒定律](@entry_id:269268)，我们可以推导出相应的[跳跃条件](@entry_id:750965) ()。

对于质量守恒，这个过程得到**[Rankine-Hugoniot跳跃条件](@entry_id:139267)**：

$$
[\rho(\mathbf{u}\cdot\mathbf{n} - s)] = 0
$$

这个表达式的物理意义是，穿过运动界面的相对质量通量是连续的。如果界面上没有[相变](@entry_id:147324)（即界面是**物质界面 (material interface)**），那么流体不会穿过界面，即 $\mathbf{u}^\pm \cdot \mathbf{n} = s$，该条件自动满足。但如果存在[相变](@entry_id:147324)（如蒸发），那么 $s$ 是界面本身的运动速度，而 $\mathbf{u}^\pm \cdot \mathbf{n}$ 是流体的法向速度，它们之间存在差异，其差异由[相变](@entry_id:147324)速率决定。该方程可以代数重排为 ()：

$$
s[\rho] = [\rho \mathbf{u}\cdot\mathbf{n}]
$$

类似的[跳跃条件](@entry_id:750965)也可以为动量和能量推导出来，它们构成了在仿真中处理[移动界面](@entry_id:141467)的夏普界面方法（sharp-interface methods）的基础。

### 物理与数值建[模的基](@entry_id:156416)本准则

在将[守恒定律](@entry_id:269268)应用于实际建模和仿真时，我们必须遵守一系列更深层次的物理和数学准则，以确保模型的有效性和一致性。

#### [热力学一致性](@entry_id:138886)：第二定律

[热力学第一定律](@entry_id:146485)（[能量守恒](@entry_id:140514)）允许任何能量形式之间的转换，但并未指明这些过程的方向。热力学第二定律通过**熵 (entropy)** 的概念引入了过程不可逆性的约束。

对于连续介质，第二定律的局部形式通常写作**克劳修斯-杜亥姆不等式 (Clausius-Duhem inequality, CDI)**。通过将第一定律和第二定律的局部形式相结合，并引入**[亥姆霍兹自由能](@entry_id:136442) (Helmholtz free energy)** $\psi = e - \theta s$（其中 $\theta$ 是绝对温度，s 是比熵），我们可以推导出一个不含外部供给项的、只涉及材料内部过程的更基本的不等式，称为**[耗散不等式](@entry_id:188634) (dissipation inequality)** ()：

$$
\boldsymbol{\sigma}:\mathbf{d} - \rho\dot{\psi} - \rho s\dot{\theta} - \frac{1}{\theta}\mathbf{q}\cdot\nabla\theta \ge 0
$$

这里 $\mathbf{d}$ 是[形变率张量](@entry_id:184787)（[速度梯度](@entry_id:261686)的对称部分），$\dot{\psi}$ 和 $\dot{\theta}$ 是[物质时间导数](@entry_id:190892)。这个不等式的左边代表了单位体积内由于内部摩擦（粘性）、塑性变形和跨越有限温差的[热传导](@entry_id:147831)等不[可逆过程](@entry_id:276625)所产生的熵，其值必须非负。这个不等式是发展[热力学](@entry_id:141121)上自洽的[本构关系](@entry_id:186508)（例如，[应力-应变关系](@entry_id:274093)或热流-[温度梯度](@entry_id:136845)关系）的根本约束。任何本构模型，如果可能导致这个不等式在某些过程中小于零，那么它就是物理上不可接受的。

#### 观察者不变性：客观性与伽利略不变性

物理定律的数学形式不应依赖于观察者。这一原则在[连续介质力学](@entry_id:155125)中具体化为两个相关的概念：伽利略[不变性](@entry_id:140168)和客观性 ()。

*   **伽利略不变性 (Galilean Invariance)** 要求物理定律在所有**惯性参考系**（即以恒定速度相对运动的[参考系](@entry_id:169232)）中形式相同。可以证明，我们之前导出的质量、动量和总[能量守恒方程](@entry_id:748978)都满足伽利略[不变性](@entry_id:140168)。这是牛顿力学基本原理的直接体现。

*   **客观性 (Objectivity)** 或称**标架无关性 (frame indifference)** 是一个更强的要求，它要求物理定律的形式在任意[参考系](@entry_id:169232)（包括旋转或加速的**[非惯性参考系](@entry_id:169712)**）之间进行适当变换后保持不变。然而，并非所有方程都具有这种性质。例如，[动量方程](@entry_id:197225)在[非惯性系](@entry_id:168746)中会出现额外的“[惯性力](@entry_id:169104)”（如[科里奥利力](@entry_id:160096)、离心力），因此其形式发生了改变，它不是客观的。

[客观性原理](@entry_id:185412)的核心应用在于**[本构关系](@entry_id:186508)**。材料的响应（如应力如何依赖于变形）是材料的内在属性，不应取决于我们如何观察它。因此，所有[本构关系](@entry_id:186508)都必须是客观的，即它们必须只涉及在刚体运动变换下表现良好的**客观张量 (objective tensors)**。例如，柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 和[形变率张量](@entry_id:184787) $\mathbf{d}$ 都是客观的，而速度 $\mathbf{v}$ 和速度梯度 $\nabla\mathbf{v}$ 则不是。同样，内能[平衡方程](@entry_id:172166)被证明是客观的，而包含依赖于观察者的动能项的总[能量平衡方程](@entry_id:191484)则不是。这个原则对[多物理场建模](@entry_id:752308)至关重要，因为它指导我们如何构建在复杂运动（如大旋转）下依然有效的材料模型。

#### 从[微分](@entry_id:158718)到数值：弱形式与离散守恒

为了进行计算机模拟，我们必须将连续的[偏微分方程](@entry_id:141332)（PDEs）转化为离散的代数方程组。这个过程中的一个关键步骤是推导PDE的**弱形式 (weak form)** ()。

对于一个通用守恒律 $\partial_t u + \nabla \cdot \mathbf{f} = s$，其弱形式是通过将其与一个**测试函数 (test function)** $\varphi$ 相乘，然后在整个计算域 $\Omega$ 上积分得到的。通过应用**[分部积分](@entry_id:136350) (integration by parts)**，我们可以将散度项上的导数转移到测试函数上：

$$
\int_\Omega \varphi (\partial_t u) \, dV - \int_\Omega \nabla \varphi \cdot \mathbf{f} \, dV + \oint_{\partial \Omega} \varphi (\mathbf{f} \cdot \mathbf{n}) \, dA = \int_\Omega \varphi s \, dV
$$

这种形式有两个主要优点：1) 它降低了对解 $u$ 和通量 $\mathbf{f}$ 光滑性的要求；2) 它自然地引出了边界积分项，使得施加[通量边界条件](@entry_id:749481)变得直接。在多物理场问题中，通过在子区域间的共享界面上强制法向通量的连续性，弱形式可以系统地保证全局守恒。

数值方法的**守恒性 (conservativeness)** 是指离散格式在多大程度上再现了积分[守恒定律](@entry_id:269268)。
*   **[有限体积法](@entry_id:749372) (Finite Volume Method, FVM)** 将计算[域划分](@entry_id:748628)为一系列不重叠的控制体（网格单元），并直接对每个单元的积分[守恒定律](@entry_id:269268)进行离散。如果一个单元流出的[数值通量](@entry_id:752791)被精确地计为相邻单元的流入通量，那么该方法就是“天生守恒”的 ()。
*   标准的**连续伽利略有限元法 (Continuous Galerkin Finite Element Method, CG-FEM)** 虽然在整个区域上满足[弱形式](@entry_id:142897)，但通常不能保证在每个单元的边界上通量是守恒的，即它不具备**局部守恒性 (local conservativeness)** ()。这在处理带有激波或陡峭梯度的流动时可能成为一个严重问题。

此外，守恒性也与所离散的方程形式有关。例如，对于可压缩流，动量方程的**[守恒形式](@entry_id:747710)**（以[动量密度](@entry_id:271360) $\rho\mathbf{v}$ 为变量）和**[非守恒形式](@entry_id:752551)**（以速度 $\mathbf{v}$ 为变量）在解析上是等价的。然而，在离散层面上，直接离散[非守恒形式](@entry_id:752551)通常会因为离散的质量和[动量方程](@entry_id:197225)之间不完全匹配而破坏动量的精确守恒。因此，为了保证物理守恒性，采用[守恒形式](@entry_id:747710)的方程进行离散至关重要 ()。

#### 处理运动域：任意拉格朗日-欧拉（ALE）方法

许多[多物理场](@entry_id:164478)问题涉及移动或变形的边界，例如流固耦合或[自由表面流](@entry_id:265322)。在这种情况下，固定的欧拉网格或随物质运动的拉格朗日网格都有其局限性。**任意拉格朗日-欧拉 (Arbitrary Lagrangian-Eulerian, ALE)** 方法提供了一个灵活的框架，其中计算网格的运动可以独立于物质的运动进行指定 ()。

在ALE框架中，我们区分三种速度：物质速度 $\mathbf{u}$，网格速度 $\mathbf{w}$，以及物质相对于网格的[对流](@entry_id:141806)速度 $(\mathbf{u}-\mathbf{w})$。[守恒定律](@entry_id:269268)需要在移动的[控制体](@entry_id:143882)上重新表述。这导致了时间导数概念的扩展：
*   **欧拉时间导数** $\left.\frac{\partial \phi}{\partial t}\right|_{\mathbf{x}}$：在空间[固定点](@entry_id:156394)观察到的变化率。
*   **拉格朗日（物质）时间导数** $\frac{D\phi}{Dt}$：跟随物[质粒](@entry_id:263777)子观察到的变化率。
*   **ALE时间导数** $\left.\frac{\partial \phi}{\partial t}\right|_{\mathbf{X}}$：跟随网格节点观察到的变化率。

它们之间的关系为 ()：

$$
\frac{D\phi}{Dt} = \left.\frac{\partial \phi}{\partial t}\right|_{\mathbf{X}} + (\mathbf{u} - \mathbf{w})\cdot \nabla \phi
$$

在ALE框架下，通用守恒律的[微分形式](@entry_id:146747)变为：

$$
\left.\frac{\partial u}{\partial t}\right|_{\mathbf{X}} + \nabla \cdot (u(\mathbf{u}-\mathbf{w})) + \nabla \cdot \mathbf{f}_{\text{non-adv}} = s
$$

这里，$\mathbf{f}_{\text{non-adv}}$ 是非[对流通量](@entry_id:158187)。对于有限体积法，这意味着穿过[移动网格](@entry_id:752196)面的数值通量必须考虑[网格运动](@entry_id:163293)，其形式为 $(\mathbf{f} - u\mathbf{w})\cdot\mathbf{n}$ ()。正确实施ALE公式对于在移动和变形域中精确地保持守恒性是必不可少的。