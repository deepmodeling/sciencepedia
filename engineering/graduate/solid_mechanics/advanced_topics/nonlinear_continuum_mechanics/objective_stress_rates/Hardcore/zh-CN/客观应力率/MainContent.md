## 引言
在固体力学中，精确描述材料在经历大变形和大转动时的力学行为是一个核心挑战。当一个物体发生显著的形状改变和旋转时，我们如何客观地衡量其内部应力状态的变化？这个问题引出了连续介质力学中一个至关重要的概念——**客观应力率**。简单地跟踪一个物质点的应力并对其求时间导数，会混入由观察者或坐标系自身旋转引起的“虚假”变化，这违反了物理定律必须独立于观察者的基本原则。因此，为了建立物理上真实且自洽的本构关系，我们必须构建一种能够滤除这种旋转效应的特殊应力率。

本文旨在系统地梳理客观应力率的理论与实践。我们将从根本问题出发，逐步深入其复杂的内涵和广泛的应用。
*   在**“原理与机制”**一章中，我们将首先揭示为何常规的物质时间导数不满足客观性要求，然后详细介绍共旋率（如Jaumann率和Green-Naghdi率）和对流率（如Truesdell率）的构建原理，并比较它们之间的关键差异。
*   接下来的**“应用与跨学科联系”**一章将展示这些理论工具如何在实际的本构模型（如次弹性和超弹塑性）中发挥作用，并探讨不同客观率的选择如何导致截然不同的物理预测，甚至影响数值计算的稳定性和效率。
*   最后，在**“动手实践”**部分，我们提供了一系列精心设计的计算练习，旨在通过具体例子加深您对客观率必要性、计算方法及其物理后果的理解。

通过学习本文，您将掌握在大变形力学建模中处理应力率的核心技能，并能批判性地评估不同本构框架的优缺点。

## 原理与机制

在描述材料于大变形和大转动下的本构行为时，一个核心挑战是如何客观地描述应力状态的变化率。本章将深入探讨客观应力率的必要性、其构建原理以及不同应力率之间的区别与联系。我们将从根本上阐明为何简单的物质时间导数在有限转动下是不客观的，并系统地介绍几种在连续介质力学中至关重要的客观率，包括共旋（corotational）率和对流（convected）率。最后，我们将讨论这些应力率在次弹性本构模型中的应用及其固有的理论局限性。

### 客观性问题：物质时间导数的局限性

在连续介质力学中，一个基本原则是**物质框架无差异性**（principle of material frame-indifference），或称**客观性**（objectivity）。该原则要求物理定律和本构关系在所有刚体运动的观察者（或参考标架）看来形式相同。一个“观察者”由一个随时间变化的刚体运动来定义，该运动由一个平移向量 $\boldsymbol{c}(t)$ 和一个正常正交旋转张量 $\boldsymbol{Q}(t)$ 描述。在任意时刻 $t$，一个观察者（有星号*）测量的空间点位置 $\boldsymbol{x}^*$ 与另一个观察者（无星号）测量的位置 $\boldsymbol{x}$ 之间的关系为：
$$
\boldsymbol{x}^*(t) = \boldsymbol{c}(t) + \boldsymbol{Q}(t)\boldsymbol{x}(t)
$$
其中 $\boldsymbol{Q}(t)$ 属于特殊正交群 $SO(3)$，满足 $\boldsymbol{Q}\boldsymbol{Q}^{\mathsf{T}} = \boldsymbol{I}$ 和 $\det(\boldsymbol{Q})=1$。

根据欧几里得空间的几何法则，任何空间二阶张量（例如柯西应力张量 $\boldsymbol{\sigma}$）在两个观察者标架之间的变换关系遵循标准的张量变换法则 [@problem_id:2666106]：
$$
\boldsymbol{\sigma}^*(t) = \boldsymbol{Q}(t)\boldsymbol{\sigma}(t)\boldsymbol{Q}(t)^{\mathsf{T}}
$$
这个关系确保了应力张量所描述的物理状态（例如作用在某个方向上的面力）在不同观察者看来是一致的。一个张量率，如果要成为一个物理上有效的量，其自身也必须是一个客观张量，即它必须遵循相同的变换法则。例如，一个客观应力率 $\mathring{\boldsymbol{\sigma}}$ 必须满足：
$$
\mathring{\boldsymbol{\sigma}}^* = \boldsymbol{Q}\mathring{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}}
$$
问题在于，最直观的应力变化率——**物质时间导数** $\dot{\boldsymbol{\sigma}}$（即跟随某一物质点测量的应力变化率）——并不满足这个客观性要求。为了证明这一点，我们可以对 $\boldsymbol{\sigma}^*$ 的变换法则直接求时间导数，并应用乘法法则 [@problem_id:2905931]：
$$
\dot{\boldsymbol{\sigma}}^* = \frac{d}{dt}(\boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}) = \dot{\boldsymbol{Q}}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{Q}\boldsymbol{\sigma}\dot{\boldsymbol{Q}}^{\mathsf{T}}
$$
我们定义观察者标架的自旋张量为 $\boldsymbol{\Omega} = \dot{\boldsymbol{Q}}\boldsymbol{Q}^{\mathsf{T}}$。由于 $\boldsymbol{Q}$ 是正交的，$\boldsymbol{\Omega}$ 是一个反对称张量（即 $\boldsymbol{\Omega}^{\mathsf{T}} = -\boldsymbol{\Omega}$）。利用这个定义以及关系式 $\boldsymbol{Q}\dot{\boldsymbol{Q}}^{\mathsf{T}} = -\boldsymbol{\Omega}^{\mathsf{T}} = \boldsymbol{\Omega}$，我们可以将 $\dot{\boldsymbol{\sigma}}^*$ 的表达式重写为：
$$
\dot{\boldsymbol{\sigma}}^* = (\dot{\boldsymbol{Q}}\boldsymbol{Q}^{\mathsf{T}})(\boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}) + \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}} + (\boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}})(\boldsymbol{Q}\dot{\boldsymbol{Q}}^{\mathsf{T}})
$$
$$
\dot{\boldsymbol{\sigma}}^* = \boldsymbol{\Omega}\boldsymbol{\sigma}^* + \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}} - \boldsymbol{\sigma}^*\boldsymbol{\Omega}
$$
整理后得到 $\dot{\boldsymbol{\sigma}}$ 的变换法则：
$$
\dot{\boldsymbol{\sigma}}^* = \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}\boldsymbol{\sigma}^* - \boldsymbol{\sigma}^*\boldsymbol{\Omega}
$$
显然，由于存在额外的交换子项 $[\boldsymbol{\Omega}, \boldsymbol{\sigma}^*] \equiv \boldsymbol{\Omega}\boldsymbol{\sigma}^* - \boldsymbol{\sigma}^*\boldsymbol{\Omega}$，$\dot{\boldsymbol{\sigma}}$ 的变换法则与客观张量的要求不符。这个非客观项的出现，其物理根源在于物质时间导数混合了材料内在的应力变化与由于观察者自身旋转所引起的应力分量的变化。因此，为了建立满足客观性原理的本构关系，我们必须构建一种能够消除这种观察者依赖性的应力率，这便是**客观应力率**。

### 共旋率（Corotational Rates）的构建原理

消除物质时间导数中非客观项的一种通用方法是引入**共旋率**。其核心思想是从物质导数中减去由材料局部旋转引起的应力变化部分。一个通用的共旋率可以定义为：
$$
\mathring{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}_{\text{spin}}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}_{\text{spin}}
$$
其中 $\boldsymbol{W}_{\text{spin}}$ 是一个用于描述材料局部旋转的反对称**自旋张量**。这个定义的巧妙之处在于，通过恰当地选择自旋张量，其在观察者变换下的非客观部分可以精确地抵消掉 $\dot{\boldsymbol{\sigma}}$ 中的非客观项。

为了使上述定义的 $\mathring{\boldsymbol{\sigma}}$ 成为客观率，自旋张量 $\boldsymbol{W}_{\text{spin}}$ 本身必须遵循一个特定的变换法则。可以证明，这个法则是 [@problem_id:2666126]：
$$
\boldsymbol{W}_{\text{spin}}^* = \boldsymbol{Q}\boldsymbol{W}_{\text{spin}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}
$$
满足此变换律的自旋张量有时被称为**客观自旋**。它表明，在新的观察者看来，测得的自旋是原自旋的刚体旋转叠加上观察者自身的自旋 $\boldsymbol{\Omega}$。任何满足此条件的自旋张量都可以用来构造一个客观的共旋率。

#### Zaremba-Jaumann率

最直观和常用的共旋率是 **Zaremba-Jaumann 率**（或简称 Jaumann 率），它选用连续体的**涡量张量**（或称空间自旋张量）$\boldsymbol{W}$ 作为自旋张量。涡量张量定义为速度梯度 $\boldsymbol{L}=\nabla\boldsymbol{v}$ 的反对称部分：
$$
\boldsymbol{W} = \text{skw}(\boldsymbol{L}) = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^{\mathsf{T}})
$$
Jaumann 率 $\boldsymbol{\sigma}^{\nabla J}$ 的表达式为：
$$
\boldsymbol{\sigma}^{\nabla J} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}
$$
可以证明，涡量张量 $\boldsymbol{W}$ 的变换规律恰好是 $\boldsymbol{W}^* = \boldsymbol{Q}\boldsymbol{W}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}$，因此 Jaumann 率是客观的 [@problem_id:2905949]。它通过减去由连续体局部平均旋转速率（由 $\boldsymbol{W}$ 描述）引起的应力变化，从而得到一个在物理上更为内在的应力率。

### 客观率家族：不同的自旋选择

Jaumann 率只是众多可能性中的一种。对“材料旋转”的不同物理诠释导致了不同的客观应力率定义。

#### Green-Naghdi率

另一种重要的共旋率是 **Green-Naghdi 率**。它的构建基于变形梯度 $\boldsymbol{F}$ 的极分解 $\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$。在这个分解中，$\boldsymbol{R}$ 是一个正常正交张量，代表了物质微元从参考构型到当前构型的纯刚体旋转，而 $\boldsymbol{U}$ 是对称正定的右伸长张量，描述了纯粹的拉伸。

Green-Naghdi 率使用的自旋张量是与材料旋转 $\boldsymbol{R}$ 直接关联的自旋，定义为 $\boldsymbol{\Omega}_{GN} = \dot{\boldsymbol{R}}\boldsymbol{R}^{\mathsf{T}}$。这个自旋同样满足客观自旋的变换法则，因此基于它定义的 Green-Naghdi 率也是客观的 [@problem_id:2905949]。其表达式为：
$$
\boldsymbol{\sigma}^{\nabla{GN}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\Omega}_{GN}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\Omega}_{GN}
$$
**Jaumann 率与 Green-Naghdi 率的比较**

这两种率的关键区别在于它们选用的自旋张量不同：Jaumann 率使用空间速度梯度的反对称部分 $\boldsymbol{W}$，而 Green-Naghdi 率使用极分解中旋转张量的变化率 $\boldsymbol{\Omega}_{GN}$。这两者在一般情况下并不相等。它们之间的差异具有深刻的物理意义。可以推导出如下关系 [@problem_id:2905963]：
$$
\boldsymbol{R}^{\mathsf{T}}(\boldsymbol{\Omega}_{GN} - \boldsymbol{W})\boldsymbol{R} = \text{skw}(\dot{\boldsymbol{U}}\boldsymbol{U}^{-1})
$$
这个公式表明，两种自旋的差异与右伸长张量 $\boldsymbol{U}$ 的主轴是否旋转直接相关。只有当 $\dot{\boldsymbol{U}}$ 和 $\boldsymbol{U}^{-1}$ 可交换时（即它们拥有相同的特征向量/主轴），$\text{skw}(\dot{\boldsymbol{U}}\boldsymbol{U}^{-1})$ 才为零，此时 $\boldsymbol{\Omega}_{GN} = \boldsymbol{W}$。物理上，这对应于材料的拉伸或收缩恰好沿着当前的应变主轴方向进行，而没有剪切效应导致主轴方向发生旋转。

这种差异对本构模型有何影响？Green-Naghdi 率与 Jaumann 率之差可以表示为 [@problem_id:2666116]：
$$
\Delta\mathring{\boldsymbol{\sigma}} = \boldsymbol{\sigma}^{\nabla{GN}} - \boldsymbol{\sigma}^{\nabla J} = [\boldsymbol{\sigma}, \boldsymbol{\Omega}_{GN} - \boldsymbol{W}]
$$
即应力张量与自旋差的交换子。一个重要的结论是：如果在应力的主轴坐标系下观察，这个差异张量 $\Delta\mathring{\boldsymbol{\sigma}}$ 的对角线分量恒为零。这意味着，选择 Jaumann 率还是 Green-Naghdi 率，会影响模型预测的**应力主轴的旋转速率**，但并**不影响应力主值本身的变化率** $\dot{s}_i$。

### 对流率（Convected Rates）：另一种客观化途径

除了共旋率，还存在另一类被称为**对流率**的客观率。它们不是通过与自旋张量的交换子来修正物质导数，而是通过包含整个速度梯度 $\boldsymbol{L}$ 的项来实现客观性。

#### Truesdell率与Oldroyd上随体导数

**Truesdell 率** $\boldsymbol{\sigma}^{\nabla T}$ 是对流率的一个典型代表，其定义为：
$$
\boldsymbol{\sigma}^{\nabla T} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{L}^{\mathsf{T}} + (\text{tr}\boldsymbol{D})\boldsymbol{\sigma}
$$
其中 $\boldsymbol{D}=\text{sym}(\boldsymbol{L})$ 是变形率张量。这个定义与**Oldroyd 上随体导数**密切相关。对于任意空间张量 $\boldsymbol{A}$，其 Oldroyd 上随体导数 $\overset{\triangledown}{\boldsymbol{A}}$ 定义为：
$$
\overset{\triangledown}{\boldsymbol{A}} = \dot{\boldsymbol{A}} - \boldsymbol{L}\boldsymbol{A} - \boldsymbol{A}\boldsymbol{L}^{\mathsf{T}}
$$
通过直接应用 $\dot{\boldsymbol{A}}$ 和 $\boldsymbol{L}$ 的变换法则，可以证明 Oldroyd 上随体导数是客观的 [@problem_id:2905932]。Truesdell 率就是柯西应力 $\boldsymbol{\sigma}$ 的 Oldroyd 上随体导数加上一个与体积变化率相关的项 $(\text{tr}\boldsymbol{D})\boldsymbol{\sigma}$，因此它也是客观的。

**Truesdell 率与 Jaumann 率的比较**

这两种重要的客观率之间的差异是什么？通过将 $\boldsymbol{L} = \boldsymbol{D} + \boldsymbol{W}$ 代入 Truesdell 率的定义，并与 Jaumann 率的定义进行比较，可以得到它们之间的精确关系 [@problem_id:2666095]：
$$
\boldsymbol{\sigma}^{\nabla T} - \boldsymbol{\sigma}^{\nabla J} = (\text{tr}\boldsymbol{D})\boldsymbol{\sigma} - (\boldsymbol{D}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{D})
$$
这个结果揭示了一个关键点：Truesdell 率和 Jaumann 率之间的差异取决于**变形率张量** $\boldsymbol{D}$ 和当前的应力状态 $\boldsymbol{\sigma}$，而与自旋张量 $\boldsymbol{W}$ 无关。这意味着，即便在无旋流动（$\boldsymbol{W}=\boldsymbol{0}$）中，只要存在变形（$\boldsymbol{D} \neq \boldsymbol{0}$），这两种率的计算结果也不同，因此选用哪种率仍然会对本构模型的预测产生影响。一个具体的数值算例可以表明，这种差异在数值上可能是显著的，并非可以忽略的小量 [@problem_id:2666095]。

### 应用与局限性：次弹性与可积性

客观应力率在**次弹性**（hypoelasticity）本构模型中扮演着核心角色。一个典型的次弹性模型将一个客观应力率与变形率张量通过一个四阶弹性张量 $\mathbb{C}$ 线性关联起来：
$$
\mathring{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}
$$
由于 $\boldsymbol{D}$ 和 $\mathbb{C}$ 都是客观张量，为了使整个本构关系满足框架无差异性原理，左侧的应力率 $\mathring{\boldsymbol{\sigma}}$ 必须是客观的 [@problem_id:2905949]。

然而，这种形式简洁的本构模型存在一个深刻的理论问题：它是否能代表一个真正的弹性材料（即**超弹性**，hyperelastic）？换言之，这种基于“率”的定义是否可以**积分**得到一个应力仅是当前变形状态的单值函数（即 $\boldsymbol{\sigma} = \boldsymbol{h}(\boldsymbol{F})$）的关系？

答案通常是否定的。以一个基于 Jaumann 率的各向同性次弹性模型为例，我们可以分析其在简单剪切变形下的响应 [@problem_id:2905938]。分析表明，随着剪切应变的持续增加，模型预测的剪切应力会呈现非物理的振荡行为，甚至在变形很大时应力会变回零。这意味着对于同一个变形状态，可能对应多个应力值，这与超弹性材料的定义相悖。这证明了基于 Jaumann 率的次弹性模型通常是**路径依赖**和**不可积**的。

只有在非常特殊的运动类别下，例如无旋的纯拉伸（$\boldsymbol{W}=\boldsymbol{0}$）或当 $\boldsymbol{D}$ 和 $\boldsymbol{W}$ 可交换的特定流动中，这类模型才能恢复路径无关性。这个理论上的缺陷是现代大变形力学更倾向于使用基于储能函数的超弹性本构框架的一个重要原因，尽管次弹性模型在计算上可能更简单。

### 基础检验：纯刚体转动

作为对所有客观率概念的最终检验，我们考虑一个最简单的情形：材料只进行纯刚体转动，没有任何变形。例如，一个速度场为 $\boldsymbol{v}(t) = \omega(t)\boldsymbol{e}_3 \times \boldsymbol{x}$ 的运动描述了绕 $\boldsymbol{e}_3$ 轴的刚体转动 [@problem_id:2666120]。对于这种运动，变形率张量 $\boldsymbol{D}=\boldsymbol{0}$。

如果一个应力场只是被动地随着材料一起旋转，那么在一个随体旋转的坐标系中，应力是恒定的。因此，任何一个有效的客观应力率在应用于这个应力场时，其值都应该为零，因为它应该能“滤除”纯刚体转动的影响。通过计算可以验证，对于这种情况，Jaumann 率、Truesdell 率和 Green-Naghdi 率的值确实都为零。这证实了它们都正确地将变形引起的应力变化与纯旋转引起的表观变化分离开来，这是客观率必须具备的基本属性。