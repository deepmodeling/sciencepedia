## 引言
在固体力学中，应力的传播并非瞬时完成，而是以波的形式进行。其中，[膨胀波](@entry_id:749166)（[P波](@entry_id:178440)）与[畸变波](@entry_id:197437)（S波）是弹性固体中两种最基本的[能量传播](@entry_id:202589)模式。理解这两种波的物理机制和传播特性，对于从[地球物理学](@entry_id:147342)的[地震分析](@entry_id:175587)到[材料科学](@entry_id:152226)的[无损检测](@entry_id:273209)等众多领域都至关重要。然而，描述波传播的矢量[波动方程](@entry_id:139839)的复杂性，往往会掩盖这两种波各自独特的物理本质及其深刻的内在联系。本文旨在系统地揭开这一面纱，为读者构建一个从第一性原理到前沿应用的完整知识体系。

为实现这一目标，本文分为三个核心章节。在“**原理与机制**”中，我们将从[弹性动力学](@entry_id:175818)的基础定律出发，推导[纳维-柯西方程](@entry_id:189211)，并通过[亥姆霍兹分解](@entry_id:181767)等数学工具，清晰地展示如何将复杂的矢量波场[解耦](@entry_id:637294)为独立的[膨胀波](@entry_id:749166)和[畸变波](@entry_id:197437)，并深入探讨它们的物理特性与[传播速度](@entry_id:189384)。接下来，在“**应用与跨学科联系**”中，我们将走出纯理论的范畴，展示这些基本原理如何在地球物理、[材料科学](@entry_id:152226)和[计算力学](@entry_id:174464)等不同学科中发挥关键作用，解决从行星尺度到微观尺度的实际问题。最后，“**动手实践**”部分将通过一系列精选的计算练习，帮助读者将理论知识转化为解决实际问题的能力，加深对波能、衰减等关键概念的理解。

## 原理与机制

本章旨在从[弹性动力学](@entry_id:175818)的第一性原理出发，系统阐述[膨胀波](@entry_id:749166)（P波）与[畸变波](@entry_id:197437)（S波）的物理机制和数学描述。我们将从建立控制方程入手，进而探讨如何将复杂的矢量波动分解为两种[基本模式](@entry_id:165201)，并推导它们的传播速度。随后，我们将深入分析这两种波的物理特性及其与[材料弹性](@entry_id:751729)常数的关系。最后，我们将介绍一些更为高级的主题，包括波在界面上的相互作用、广义弹性理论中的[色散](@entry_id:263750)现象以及[各向异性介质](@entry_id:187796)中的波传播特性。

### [弹性动力学](@entry_id:175818)的控制方程

在[连续介质力学](@entry_id:155125)的框架下，描述弹性体[内波](@entry_id:261048)传播现象的理论建立在三个基本支柱之上：[动量守恒](@entry_id:149964)、[运动学](@entry_id:173318)关系和[本构关系](@entry_id:186508)。对于一个无限、均匀、各向同性的线性弹性体，在小变形假设下，这些基本定律共同构成了[弹性波](@entry_id:196203)理论的出发点。[@problem_id:2907170]

首先，**动量守恒**由柯西第一运动定律（Cauchy's first law of motion）给出，其局部微分形式为：
$$
\nabla \cdot \boldsymbol{\sigma} + \mathbf{f} = \rho \ddot{\mathbf{u}}
$$
其中，$\boldsymbol{\sigma}$ 是柯西应力张量，它描述了材料内部的力的[分布](@entry_id:182848)状态；$\mathbf{f}$ 是单位体积所受的体力（如重力），在许多波传播问题中可以忽略；$\rho$ 是材料的质量密度；$\mathbf{u}(\mathbf{x}, t)$ 是[位移场](@entry_id:141476)，代表材料点从其平衡位置的移动；$\ddot{\mathbf{u}}$ 是位移对时间的[二阶导数](@entry_id:144508)，即加速度。对于经典的非极性连续体，在没有体力偶和面力偶的情况下，角动量守恒定律要求柯西[应力张量](@entry_id:148973)必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$。

其次，**运动学关系**描述了变形与位移场之间的几何联系。在“小变形”或“小应变”的假设下，[位移梯度](@entry_id:165352) $\nabla \mathbf{u}$ 的范数远小于1。这不仅意味着应变很小，也意味着转动很小。在此条件下，[非线性](@entry_id:637147)的[格林-拉格朗日应变张量](@entry_id:187745)可以被线性化，得到[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon}$：
$$
\boldsymbol{\varepsilon} = \frac{1}{2}\left(\nabla \mathbf{u} + (\nabla \mathbf{u})^{\mathsf{T}}\right)
$$
该张量定义为[位移梯度](@entry_id:165352)的对称部分，它精确地度量了材料微元的拉伸和[剪切变形](@entry_id:170920)。

最后，**本构关系**描述了材料的力学响应，即[应力与应变](@entry_id:137374)之间的关系。对于一个线性、各向同性的弹性材料，该关系由[广义胡克定律](@entry_id:203555)（Hooke's Law）给出：
$$
\boldsymbol{\sigma} = \lambda \operatorname{tr}(\boldsymbol{\varepsilon}) \mathbf{I} + 2 \mu \boldsymbol{\varepsilon}
$$
其中，$\lambda$ 和 $\mu$ 是材料的拉梅（Lamé）常数，$\mathbf{I}$ 是二阶单位张量。$\operatorname{tr}(\boldsymbol{\varepsilon})$ 是[应变张量](@entry_id:193332)的迹，等于 $\nabla \cdot \mathbf{u}$，代表了材料的体积变化，称为**[体应变](@entry_id:267252)**或**膨胀**。常数 $\mu$ 被称为**剪切模量**，它量化了材料对形状改变（剪切）的抵抗能力。拉梅常数、剪切模量、杨氏模量 $E$ 和泊松比 $\nu$ 都是描述[各向同性材料](@entry_id:170678)弹性的等价参数集。

将上述运动学和[本构关系](@entry_id:186508)代入动量守恒方程，就可以得到一个完全用位移场 $\mathbf{u}$ 表达的控制方程。这个过程如下：
$$
\rho \ddot{\mathbf{u}} = \nabla \cdot \left[ \lambda (\nabla \cdot \mathbf{u}) \mathbf{I} + \mu \left( \nabla \mathbf{u} + (\nabla \mathbf{u})^{\mathsf{T}} \right) \right] + \mathbf{f}
$$
利用矢量恒等式 $\nabla \cdot (\phi \mathbf{I}) = \nabla \phi$ 和 $\nabla \cdot (\nabla \mathbf{u}^{\mathsf{T}}) = \nabla(\nabla \cdot \mathbf{u})$，以及矢量[拉普拉斯算子](@entry_id:146319)的定义 $\nabla^2 \mathbf{u} = \nabla \cdot (\nabla \mathbf{u})$，可以推导出应力散度项：
$$
\nabla \cdot \boldsymbol{\sigma} = (\lambda + \mu) \nabla(\nabla \cdot \mathbf{u}) + \mu \nabla^2 \mathbf{u}
$$
最终，我们得到了描述均匀各向同性线性弹性体中[位移场](@entry_id:141476)演化的**[纳维-柯西方程](@entry_id:189211)**（Navier-Cauchy equation）：
$$
\rho \ddot{\mathbf{u}} = (\lambda + \mu) \nabla(\nabla \cdot \mathbf{u}) + \mu \nabla^2 \mathbf{u} + \mathbf{f}
$$
这个矢量[偏微分方程](@entry_id:141332)是[弹性波](@entry_id:196203)理论的核心，它内含了两种基本波动的耦合行为。[@problem_id:2630830]

### 波场的解耦：[势函数](@entry_id:176105)与极化

[纳维-柯西方程](@entry_id:189211)是一个矢量方程，直接求解相当复杂。然而，通过巧妙的数学变换，我们可以将其解耦为两个更简单的[标量和矢量](@entry_id:170784)波方程，分别描述两种截然不同的物理运动：膨胀和畸变。

一种直观的[解耦](@entry_id:637294)方法是利用矢量恒等式 $\nabla^2 \mathbf{u} = \nabla(\nabla \cdot \mathbf{u}) - \nabla \times (\nabla \times \mathbf{u})$。将此恒等式代入不含[体力](@entry_id:174230)项的[纳维-柯西方程](@entry_id:189211)中，我们得到：
$$
\rho \ddot{\mathbf{u}} = (\lambda + \mu) \nabla(\nabla \cdot \mathbf{u}) + \mu [\nabla(\nabla \cdot \mathbf{u}) - \nabla \times (\nabla \times \mathbf{u})]
$$
整理后得到：
$$
\rho \ddot{\mathbf{u}} = (\lambda + 2\mu) \nabla(\nabla \cdot \mathbf{u}) - \mu \nabla \times (\nabla \times \mathbf{u})
$$
这个形式清晰地揭示了两种驱动力：第一项 $\nabla(\nabla \cdot \mathbf{u})$ 与位移场的散度（即体积变化）有关，是**膨胀运动**的策源；第二项 $\nabla \times (\nabla \times \mathbf{u})$ 与[位移场](@entry_id:141476)的旋度（即转动或形状改变）有关，是**畸变运动**的策源。[@problem_id:2630830]

为了实现更彻底的数学解耦，我们引入**[亥姆霍兹分解](@entry_id:181767)**（Helmholtz decomposition），将任何足够光滑的矢量场 $\mathbf{u}$ 分解为一个[无旋场](@entry_id:183486)（irrotational field）和一个[无散场](@entry_id:260932)（solenoidal field）的和。这可以通过一个[标量势](@entry_id:276177) $\phi$ 和一个矢量势 $\boldsymbol{\Psi}$ 来实现：
$$
\mathbf{u} = \nabla \phi + \nabla \times \boldsymbol{\Psi}
$$
其中，$\nabla \phi$ 是无旋部分，因为 $\nabla \times (\nabla \phi) = \mathbf{0}$；$\nabla \times \boldsymbol{\Psi}$ 是无散部分，因为 $\nabla \cdot (\nabla \times \boldsymbol{\Psi}) = 0$。为了保证分[解的唯一性](@entry_id:143619)（在适当的边界条件下），通常施加一个[规范条件](@entry_id:749730)，如[库仑规范](@entry_id:273044)（Coulomb gauge）$\nabla \cdot \boldsymbol{\Psi} = 0$。[@problem_id:2907190]

将这个分解代入[纳维-柯西方程](@entry_id:189211)的解耦形式，并利用 $\nabla \cdot \mathbf{u} = \nabla^2 \phi$ 和 $\nabla \times \mathbf{u} = \nabla \times (\nabla \times \boldsymbol{\Psi})$，方程可以被分离为两个独立的部分：
$$
\nabla \left[ (\lambda + 2\mu) \nabla^2 \phi - \rho \ddot{\phi} \right] + \nabla \times \left[ \mu \nabla^2 \boldsymbol{\Psi} - \rho \ddot{\boldsymbol{\Psi}} \right] = \mathbf{0}
$$
由于一个场的梯度[部分和](@entry_id:162077)旋度部分是相互独立的，上式成立的唯一可能是两个方括号内的表达式同时为零。这样，我们就得到了两个解耦的波方程：
$$
\frac{\partial^2 \phi}{\partial t^2} = \left(\frac{\lambda + 2\mu}{\rho}\right) \nabla^2 \phi
$$
$$
\frac{\partial^2 \boldsymbol{\Psi}}{\partial t^2} = \left(\frac{\mu}{\rho}\right) \nabla^2 \boldsymbol{\Psi}
$$
第一个是描述[标量势](@entry_id:276177) $\phi$ 传播的标量波方程。由于 $\phi$ 完全决定了[位移场](@entry_id:141476)的散度 $\nabla \cdot \mathbf{u} = \nabla^2 \phi$，它描述的是**[膨胀波](@entry_id:749166)**（Dilatational Wave）的传播，也称为**[P波](@entry_id:178440)**（Primary Wave）。其传播速度 $c_p$ 为：
$$
c_p = \sqrt{\frac{\lambda + 2\mu}{\rho}}
$$
第二个是描述矢量势 $\boldsymbol{\Psi}$ 传播的矢量波方程。由于 $\boldsymbol{\Psi}$ 完全决定了[位移场](@entry_id:141476)的旋度（在[规范条件](@entry_id:749730)下 $\nabla \times \mathbf{u} = -\nabla^2 \boldsymbol{\Psi}$），它描述的是**[畸变波](@entry_id:197437)**（Distortional Wave）的传播，也称为**[S波](@entry_id:174890)**（Secondary Wave）。其[传播速度](@entry_id:189384) $c_s$ 为：
$$
c_s = \sqrt{\frac{\mu}{\rho}}
$$
这个[解耦](@entry_id:637294)过程清晰地表明，在一个均匀[各向同性弹性](@entry_id:203237)体中，任何复杂的弹性扰动都可以被看作是这两种基本波的线性叠加。[@problem_id:2112540]

### [平面波](@entry_id:189798)分析与[克里斯托费尔方程](@entry_id:180126)

除了势[函数分解](@entry_id:197881)法，另一种强大且更具普适性的分析方法是**平面波分析**。该方法假设存在形如
$$
\mathbf{u}(\mathbf{x}, t) = \mathbf{A} \exp\left[i(k \mathbf{n} \cdot \mathbf{x} - \omega t)\right]
$$
的[平面波解](@entry_id:195230)。其中 $\mathbf{A}$ 是恒定的极化（振幅）矢量，$\mathbf{n}$ 是波的传播方向单位矢量，$k$ 是波数，$\omega$ 是角频率。波的相速度为 $c = \omega/k$。[@problem_id:2574478]

将此[平面波解](@entry_id:195230)代入[纳维-柯西方程](@entry_id:189211)，[微分](@entry_id:158718)运算转变为代数运算：$\nabla \to ik\mathbf{n}$，$\partial/\partial t \to -i\omega$。经过化简，我们得到一个关于[极化矢量](@entry_id:269389) $\mathbf{A}$ 的[特征值问题](@entry_id:142153)，即**[克里斯托费尔方程](@entry_id:180126)**（Christoffel equation）：
$$
\left[(\lambda+\mu)(\mathbf{n}\otimes\mathbf{n}) + \mu\mathbf{I}\right]\mathbf{A} = \rho c^2 \mathbf{A}
$$
其中，$\mathbf{n}\otimes\mathbf{n}$ 表示 $\mathbf{n}$ 的并矢。左侧的张量 $\mathbf{\Gamma}(\mathbf{n}) = (\lambda+\mu)(\mathbf{n}\otimes\mathbf{n}) + \mu\mathbf{I}$ 被称为[克里斯托费尔声学张量](@entry_id:186595)。该方程的[特征值](@entry_id:154894) $\rho c^2$ 决定了允许传播的波的相速度，而对应的特征矢量 $\mathbf{A}$ 则给出了波的极化方向。

现在我们分析两种可能的极化情况：
1.  **[纵向极化](@entry_id:202391)（[P波](@entry_id:178440)）**：[极化矢量](@entry_id:269389) $\mathbf{A}$ 与传播方向 $\mathbf{n}$ 平行，即 $\mathbf{A} \parallel \mathbf{n}$。在这种情况下，[质点](@entry_id:186768)的[振动](@entry_id:267781)方向与[波的传播](@entry_id:144063)方向一致。代入[克里斯托费尔方程](@entry_id:180126)，我们发现一个[特征值](@entry_id:154894)解：
    $$
    \rho c_p^2 = \lambda + 2\mu \quad \implies \quad c_p = \sqrt{\frac{\lambda + 2\mu}{\rho}}
    $$
    这与我们之前得到的结果完全一致。这种波涉及体积变化，因为 $\nabla \cdot \mathbf{u} = ik(\mathbf{n} \cdot \mathbf{A}) \neq 0$。

2.  **横向极化（[S波](@entry_id:174890)）**：[极化矢量](@entry_id:269389) $\mathbf{A}$ 与传播方向 $\mathbf{n}$ 垂直，即 $\mathbf{A} \perp \mathbf{n}$。[质点](@entry_id:186768)在垂直于传播方向的平面内[振动](@entry_id:267781)。代入[克里斯托费尔方程](@entry_id:180126)，我们发现另一个[特征值](@entry_id:154894)解：
    $$
    \rho c_s^2 = \mu \quad \implies \quad c_s = \sqrt{\frac{\mu}{\rho}}
    $$
    这同样与之前的结果吻合。这种波是等容的，即不引起体积变化，因为 $\nabla \cdot \mathbf{u} = ik(\mathbf{n} \cdot \mathbf{A}) = 0$。

[克里斯托费尔方程](@entry_id:180126)方法的美妙之处在于其普适性，它不仅适用于各向同性介质，更是分析更复杂的[各向异性介质](@entry_id:187796)中波传播特性的关键工具。

### [膨胀波](@entry_id:749166)与[畸变波](@entry_id:197437)的物理特性

P波和[S波](@entry_id:174890)的本质区别在于它们的变形模式和[传播速度](@entry_id:189384)。

**P波**是**纵波**，其[质点](@entry_id:186768)[振动](@entry_id:267781)方向与[能量传播](@entry_id:202589)方向平行。它的传播伴随着介质的交替压缩和稀疏，因此被称为**[膨胀波](@entry_id:749166)**。控制其速度的弹性模量是**[P波](@entry_id:178440)模量** $M = \lambda + 2\mu$，它代表了材料在无法横向收缩的条件下抵抗单轴压缩的能力。由于对于稳定材料 $\lambda > 0$ 和 $\mu > 0$（通常情况），我们总是有 $\lambda+2\mu > \mu$，因此**P波的[传播速度](@entry_id:189384)总是快于[S波](@entry_id:174890)**，这也是它被称为“Primary Wave”（首达波）的原因。

**[S波](@entry_id:174890)**是**[横波](@entry_id:269527)**，其[质点](@entry_id:186768)[振动](@entry_id:267781)方向垂直于[能量传播](@entry_id:202589)方向。它的传播使得介质单元发生形状改变（剪切），而[体积保持](@entry_id:141001)不变，因此被称为**[畸变波](@entry_id:197437)**或**剪切波**。控制其速度的[弹性模量](@entry_id:198862)就是**[剪切模量](@entry_id:167228)** $\mu$。考虑一个在 $+z$ 方向传播、沿 $x$ 方向极化的S波，其位移场可以表示为 $\mathbf{u} = U_0 \mathbf{e}_x \cos(kz - \omega t)$。通过直接计算可以验证，其散度 $\nabla \cdot \mathbf{u} = 0$，表明其纯畸变性质。其唯一的非零应变分量是[剪应变](@entry_id:175241) $\varepsilon_{xz}$，相应的应力也只有剪应力分量 $\sigma_{xz} = 2\mu \varepsilon_{xz}$，这清晰地展示了S波的物理内涵。[@problem_id:2630832]

为了更好地理解[波速](@entry_id:186208)与常用[工程弹性常数](@entry_id:182223)的关系，我们可以将 $\lambda$ 和 $\mu$ 替换为[杨氏模量](@entry_id:140430) $E$ 和泊松比 $\nu$：
$$
\mu = \frac{E}{2(1+\nu)} \quad \text{and} \quad \lambda = \frac{E\nu}{(1+\nu)(1-2\nu)}
$$
代入后，我们得到：
$$
c_p = \sqrt{\frac{E(1-\nu)}{\rho(1+\nu)(1-2\nu)}}, \quad c_s = \sqrt{\frac{E}{2\rho(1+\nu)}}
$$
这组表达式揭示了[波速](@entry_id:186208)与材料宏观力学行为的深刻联系。我们可以进一步考察[P波与S波](@entry_id:177682)速度之比 $c_p/c_s$：[@problem_id:2630831]
$$
\frac{c_p}{c_s} = \sqrt{\frac{2(1-\nu)}{1-2\nu}}
$$
这个比值仅依赖于[泊松比](@entry_id:158876) $\nu$。对于物理上可能的泊松比范围 $\nu \in (-1, 0.5)$，该比值是单调递增的。当 $\nu \to 0.5$ 时，材料趋于不可压缩，此时 $c_p/c_s \to \infty$，意味着在[不可压缩材料](@entry_id:159741)中，任何体积扰动（P波）会瞬间传遍整个介质。对于典型的工程材料，$\nu \approx 0.3$，此时 $c_p/c_s \approx 1.87$。这个比值在[地震学](@entry_id:203510)和[无损检测](@entry_id:273209)中是确定震源位置和评估材料特性的重要参数。

### 波传播中的高等课题

#### 波在[材料界面](@entry_id:751731)上的相互作用

当[弹性波](@entry_id:196203)遇到两种不同材料的界面时，会发生反射和透射现象。如果两种介质是**完美焊接**（perfectly bonded）的，那么在界面处必须满足两个基本条件：**运动学连续性条件**和**动力学连续性条件**。[@problem_id:2630844]

1.  **位移连续性**：界面两侧的[位移矢量](@entry_id:262782)必须相等，以确保材料不会在界面处撕裂或相互穿透。
    $$
    \mathbf{u}^{(1)} = \mathbf{u}^{(2)} \quad \text{at the interface}
    $$

2.  **[牵引力连续性](@entry_id:756091)**：根据牛顿第三定律，界面两侧的牵[引力](@entry_id:175476)矢量（单位面积上的作用力）必须大小相等、方向相反。这意味着牵[引力](@entry_id:175476)矢量在界面上是连续的。
    $$
    \mathbf{t}^{(1)} = \boldsymbol{\sigma}^{(1)}\mathbf{n} = \mathbf{t}^{(2)} = \boldsymbol{\sigma}^{(2)}\mathbf{n} \quad \text{at the interface}
    $$
    其中 $\mathbf{n}$ 是界面的法向量。

当一束P波或S波以[斜入射](@entry_id:267188)角到达界面时，这两个矢量边界条件（共6个标量分量，在平面问题中简化为4个）通常无法仅由反射和透射的同类型波来满足。为了满足所有条件，必须在反射和透射场中同时激发P波和S波。这种现象称为**[模式转换](@entry_id:197482)**（mode conversion），是[弹性波](@entry_id:196203)界面行为的一个核心特征。例如，一束入射[P波](@entry_id:178440)通常会产生反射P波、反射S波、透射P波和透射S波。这四种波的振幅由一个[线性方程组](@entry_id:148943)（即[Zoeppritz方程](@entry_id:756827)）唯一确定。

#### 广义弹性连续体中的[色散](@entry_id:263750)

在经典的柯西[弹性理论](@entry_id:184142)中，P波和S波的速度 $c_p$ 和 $c_s$ 是材料常数，与波的频率或波数无关。这种现象称为**非[色散](@entry_id:263750)**（non-dispersive），意味着任何形状的[波包](@entry_id:154698)在传播时都将保持其形状。然而，当波长小到与材料的微观结构（如[晶粒尺寸](@entry_id:161460)、分子链长度）相当时，经典理论不再适用。[@problem_id:2630842]

为了描述这种尺寸效应，需要引入**[广义连续介质力学](@entry_id:186593)理论**，如**[应变梯度弹性理论](@entry_id:197079)**或**偶应力理论**。这些理论在[本构关系](@entry_id:186508)中引入了[应变梯度](@entry_id:204192)或转动梯度等高阶项，并伴随着一个或多个具有长度量纲的**[内禀长度尺度](@entry_id:750789)**参数（例如 $\ell$）。

例如，在一种[应变梯度模型](@entry_id:196189)中，[本构关系](@entry_id:186508)可能变为 $(\mathbf{I}-\ell^{2}\nabla^{2})\boldsymbol{\sigma} = \lambda \operatorname{tr}(\boldsymbol{\varepsilon})\mathbf{I}+2\mu\boldsymbol{\varepsilon}$。对于平面波，这会导致[波速](@entry_id:186208)依赖于波数 $k$：
$$
c_p(k) = \frac{c_{p, \text{classic}}}{\sqrt{1+\ell^2 k^2}}, \quad c_s(k) = \frac{c_{s, \text{classic}}}{\sqrt{1+\ell^2 k^2}}
$$
而在另一种偶应力模型中，S[波的[色](@entry_id:275520)散关系](@entry_id:140395)可能变为 $\omega^2 = c_s^2 k^2 + \alpha k^4$，其中 $\alpha > 0$。在这两种情况下，相速度 $c = \omega/k$ 都变成了[波数](@entry_id:172452) $k$ 的函数，这种现象称为**[色散](@entry_id:263750)**（dispersion）。[色散](@entry_id:263750)意味着不同频率（或波长）的波以不同的速度传播，导致波包在传播过程中会弥散开来，改变其形状。

#### 各向异性与[剪切波分裂](@entry_id:187112)

我们之前的讨论都局限于各向同性介质。然而，大多数真实材料，如晶体、[复合材料](@entry_id:139856)和具有织构的多晶金属，都表现出**各向异性**，即它们的弹性性质依赖于方向。对于各向异性材料，[弹性张量](@entry_id:170728) $C_{ijkl}$ 不再能用两个常数 ($\lambda, \mu$) 来描述。[@problem_id:2630827]

在这种情况下，[克里斯托费尔方程](@entry_id:180126) $\mathbf{\Gamma}(\mathbf{n})\mathbf{A} = \rho c^2 \mathbf{A}$ 仍然是分析[平面波传播](@entry_id:753479)的核心工具，但[声学张量](@entry_id:200089) $\mathbf{\Gamma}_{ik} = C_{ijkl}n_j n_l$ 的结构变得复杂。对于一个任意的传播方向 $\mathbf{n}$，$\mathbf{\Gamma}(\mathbf{n})$ 通常有三个互不相同的[特征值](@entry_id:154894)，对应三个相互正交的[极化矢量](@entry_id:269389)。

这导致了两个重要后果：
1.  **波模式的混合**：这三种波通常不再是纯粹的[纵波](@entry_id:172335)或横波。其中一种是**准[纵波](@entry_id:172335)**（quasi-longitudinal, qP），其极化方向大致平行于 $\mathbf{n}$；另外两种是**准横波**（quasi-transverse, qS），其极化方向大致垂直于 $\mathbf{n}$。
2.  **[剪切波分裂](@entry_id:187112)**（Shear Wave Splitting）：在各向同性介质中，两个S波模式是**简并**的，意味着任何垂直于 $\mathbf{n}$ 的方向都可以是S波的极化方向，且速度相同。这是因为各向同性[声学张量](@entry_id:200089)关于 $\mathbf{n}$ 轴具有[旋转对称](@entry_id:137077)性。而在[各向异性介质](@entry_id:187796)中，这种对称性通常被破坏。对于给定的传播方向 $\mathbf{n}$，通常只有两个特定的、相互正交的极化方向是允许的，并且它们对应两个**不同**的准[剪切波速度](@entry_id:754765)。这种由各向异性引起的剪切波简并性的解除，就称为[剪切波分裂](@entry_id:187112)。

以横观[各向同性材料](@entry_id:170678)（如具有层状或纤维状结构的材料）为例，当波在包含对称轴的平面内传播时，一个剪切波（SH波）的极化方向会严格垂直于该平面，而另一个剪切波（qSV波）的极化方向则位于该平面内。除非沿着特殊的对称轴传播，这两种剪切波的速度是不同的。[剪切波分裂](@entry_id:187112)是探测地球地幔和地壳各向异性、以及表征[材料微观结构](@entry_id:198422)的重要工具。