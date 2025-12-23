## 引言
在描述材料如何响应变形时，[本构关系](@entry_id:186508)是[连续介质力学](@entry_id:155125)的核心。一个基本的物理要求是，这些定律必须独立于观察者，即满足物质标架无关性（或客观性）原理。然而，在[流体动力](@entry_id:750449)学中常用的物质导数本身并不满足此要求，这给在欧拉坐标系下建立普适的本构方程带来了根本性挑战。本文旨在系统性地解决这一问题，深入探讨[客观时间导数](@entry_id:1129024)的理论、应用与实践。

在接下来的内容中，我们将分三个章节展开讨论。首先，在“原理与机制”一章中，我们将阐明物质[标架无关性原理](@entry_id:200995)，解释为何需要客观导数，并详细推导和比较几种关键的客观导数，特别是上随体和[下随体导数](@entry_id:1127499)，揭示其深刻的几何意义。随后，在“应用与交叉学科联系”一章中，我们将展示这些导数如何应用于构建粘弹性流体的本构模型（如[Oldroyd-B模型](@entry_id:752895)），分析其在流变学预测和[计算模拟](@entry_id:146373)中的关键作用，并探讨其在地球物理等交叉领域的应用。最后，通过“动手实践”部分提供的练习，您将有机会亲手计算和验证这些概念，从而加深理解。

让我们首先从物质标架无关性这一基本原理出发，探究[客观时间导数](@entry_id:1129024)构建的必要性与机制。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，本构关系描述了材料的力学响应，例如应力如何依赖于变形或变形率。为了使这些物理定律具有普遍性，它们必须独立于观察者。这意味着，无论观察者是在[静止参考系](@entry_id:262703)中，还是在[平动](@entry_id:187700)或旋转的参考系中，本构方程的形式都必须保持不变。这一基本要求被称为**物质[标架无关性原理](@entry_id:200995)**（Principle of Material Frame Indifference, MFI），或称**[客观性原理](@entry_id:185412)**。本章旨在阐述如何构建满足此原理的时间导数，这对于在欧拉坐标系下描述复杂流体的本构行为至关重要。

### 物质标架无关性与客观性时间导数的需求

物质[标架无关性原理](@entry_id:200995)，由 Walter Noll 系统阐述，断言[本构关系](@entry_id:186508)在任意叠加[刚体运动](@entry_id:144691)下必须保持不变 。一个叠加[刚体运动](@entry_id:144691)可以通过一个时间相关的正交[旋转张量](@entry_id:191990) $\boldsymbol{Q}(t)$ 和一个时间相关的平动向量 $\boldsymbol{c}(t)$ 来描述。在此变换下，一个观察者（在带星号的标架中）所看到的空间点 $\boldsymbol{x}^*$ 与另一个观察者（在不带星号的标架中）所看到的点 $\boldsymbol{x}$ 之间的关系为：
$$
\boldsymbol{x}^*(t) = \boldsymbol{Q}(t) \boldsymbol{x}(t) + \boldsymbol{c}(t)
$$
其中 $\boldsymbol{Q}(t)$ 满足 $\boldsymbol{Q}(t)\boldsymbol{Q}^{\mathsf{T}}(t) = \boldsymbol{I}$，$\boldsymbol{I}$ 为单位张量。

根据该原理，一个物理量若要成为**客观的**（objective），其在不同标架下的表示必须遵循标准的[张量变换法则](@entry_id:185176)。例如，一个二阶[空间张量](@entry_id:185799)场 $\boldsymbol{A}(\boldsymbol{x}, t)$（如柯西[应力张量](@entry_id:148973)或[聚合物构象](@entry_id:180389)张量）若要客观，其在带星号标架中的表示 $\boldsymbol{A}^*$ 必须与在不带星号标架中的表示 $\boldsymbol{A}$ 满足以下关系：
$$
\boldsymbol{A}^*(\boldsymbol{x}^*, t) = \boldsymbol{Q}(t) \boldsymbol{A}(\boldsymbol{x}, t) \boldsymbol{Q}^{\mathsf{T}}(t)
$$
[本构关系](@entry_id:186508)通常涉及张量的时间变化率。因此，[本构方程](@entry_id:138559)中使用的任何时间导数算子 $\mathcal{D}$ 也必须是客观的。这意味着，由该算子作用于张量 $\boldsymbol{A}$ 所产生的时间导数张量 $\mathcal{D}[\boldsymbol{A}]$ 本身也必须是一个客观张量。其数学表达为，对于任意叠加刚体运动，该算子必须满足以下变换规则 ：
$$
\mathcal{D}^*[\boldsymbol{A}^*](\boldsymbol{x}^*, t) = \boldsymbol{Q}(t) (\mathcal{D}[\boldsymbol{A}](\boldsymbol{x}, t)) \boldsymbol{Q}^{\mathsf{T}}(t)
$$
其中 $\mathcal{D}^*$ 是在带星号标架中，使用该标架下的运动学量（如速度梯度 $\boldsymbol{L}^*$）构造的相同形式的算子。

在[流体动力](@entry_id:750449)学中，最自然的时间导数是**[物质导数](@entry_id:262900)**（material derivative），它描述了跟随一个物质点运动时物理量的变化率。对于一个[张量场](@entry_id:190170) $\boldsymbol{A}(\boldsymbol{x}, t)$，其物质导数 $\dot{\boldsymbol{A}}$ 定义为：
$$
\dot{\boldsymbol{A}} = \frac{D\boldsymbol{A}}{Dt} = \frac{\partial \boldsymbol{A}}{\partial t} + (\boldsymbol{v} \cdot \nabla) \boldsymbol{A}
$$
其中 $\boldsymbol{v}$ 是速度场。然而，物质导数并不是一个客观的时间导数。我们可以通过考察其在叠加刚体运动下的变换行为来证明这一点。对变换关系 $\boldsymbol{A}^* = \boldsymbol{Q}\boldsymbol{A}\boldsymbol{Q}^{\mathsf{T}}$ 两边求物质导数，并使用[乘法法则](@entry_id:144424)，可得：
$$
\dot{\boldsymbol{A}}^* = \dot{\boldsymbol{Q}}\boldsymbol{A}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{Q}\dot{\boldsymbol{A}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{Q}\boldsymbol{A}\dot{\boldsymbol{Q}}^{\mathsf{T}}
$$
引入观察者标架的[自旋张量](@entry_id:187346) $\boldsymbol{\Omega}(t) = \dot{\boldsymbol{Q}}(t)\boldsymbol{Q}^{\mathsf{T}}(t)$（这是一个[反对称张量](@entry_id:199349)），上式可以改写为：
$$
\dot{\boldsymbol{A}}^* = \boldsymbol{Q}\dot{\boldsymbol{A}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}\boldsymbol{A}^* - \boldsymbol{A}^*\boldsymbol{\Omega}
$$
显然，除非旋转是时间无关的（即 $\boldsymbol{\Omega} = \boldsymbol{0}$），否则 $\dot{\boldsymbol{A}}^* \neq \boldsymbol{Q}\dot{\boldsymbol{A}}\boldsymbol{Q}^{\mathsf{T}}$。多出来的项 $\boldsymbol{\Omega}\boldsymbol{A}^* - \boldsymbol{A}^*\boldsymbol{\Omega}$ 表明[物质导数](@entry_id:262900)包含了由于观察者自身旋转而产生的非客观贡献。一个简单的例子可以说明这个问题：假设在一个标架中，张量 $\boldsymbol{A}$ 是恒定的，因此其[物质导数](@entry_id:262900) $\dot{\boldsymbol{A}} = \boldsymbol{0}$。在另一个相对于该标架做纯旋转的标架中，我们期望客观导数也为零。然而，$\dot{\boldsymbol{A}}^*$ 却等于 $\boldsymbol{\Omega}\boldsymbol{A}^* - \boldsymbol{A}^*\boldsymbol{\Omega}$，通常不为零 。

因此，为了构建满足物质[标架无关性原理](@entry_id:200995)的[本构方程](@entry_id:138559)，我们必须发展并使用[客观时间导数](@entry_id:1129024)，这些导数能够从物质导数中移除或补偿这种非客观的旋转效应。

### [运动学分解](@entry_id:751020)与变换法则

在构造客观导数之前，我们首先需要定义流动的基本运动学量，并确定它们在叠加[刚体运动](@entry_id:144691)下的变换法则 。流动的局部运动由[速度梯度张量](@entry_id:270928) $\boldsymbol{L} = \nabla \boldsymbol{v}$ 描述。$\boldsymbol{L}$ 可以分解为其对称和反对称部分：
- **变形率张量**（rate-of-deformation tensor）：$\boldsymbol{D} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^{\mathsf{T}})$，描述了物质单元的拉伸和[剪切变形](@entry_id:170920)速率。
- **[涡量张量](@entry_id:189621)**（vorticity tensor）或**[自旋张量](@entry_id:187346)**（spin tensor）：$\boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^{\mathsf{T}})$，描述了物质单元的刚性转动速率。

在叠加[刚体运动](@entry_id:144691)下，这些运动学量的变换法则是推导客观导数的关键。可以证明它们遵循以下规则：
$$
\boldsymbol{L}^* = \boldsymbol{Q}\boldsymbol{L}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}
$$
$$
\boldsymbol{D}^* = \boldsymbol{Q}\boldsymbol{D}\boldsymbol{Q}^{\mathsf{T}}
$$
$$
\boldsymbol{W}^* = \boldsymbol{Q}\boldsymbol{W}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}
$$
其中 $\boldsymbol{\Omega} = \dot{\boldsymbol{Q}}\boldsymbol{Q}^{\mathsf{T}}$ 是观察者标架的[自旋张量](@entry_id:187346)。这些关系表明，变形率张量 $\boldsymbol{D}$ 是一个客观张量，而[速度梯度](@entry_id:261686) $\boldsymbol{L}$ 和[涡量张量](@entry_id:189621) $\boldsymbol{W}$ 则不是，它们在变换中都包含了额外的观察者自旋项 $\boldsymbol{\Omega}$。

### [客观时间导数](@entry_id:1129024)的构造

构造[客观时间导数](@entry_id:1129024)的思想是从物质导数 $\dot{\boldsymbol{A}}$ 中减去或加上一些项，这些项的构造方式是利用流动的运动学量（如 $\boldsymbol{L}$ 或 $\boldsymbol{W}$），使得在叠加刚体运动下，这些附加项的变换正好能够抵消 $\dot{\boldsymbol{A}}$ 变换时产生的非客观项 $\boldsymbol{\Omega}\boldsymbol{A}^* - \boldsymbol{A}^*\boldsymbol{\Omega}$。下面我们介绍三种最常用的[客观时间导数](@entry_id:1129024) 。

#### 协同转动（Jaumann）导数

**协同转动导数**（corotational derivative），或称**Jaumann导数**，通过从物质导数中减去由流体局部平均转速（由[涡量张量](@entry_id:189621) $\boldsymbol{W}$ 描述）引起的张量转动效应来构造。其定义为：
$$
\overset{\circ}{\boldsymbol{A}} = \dot{\boldsymbol{A}} - \boldsymbol{W}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{W}
$$
该导数衡量的是在一个随流体局部旋转的参考系中观察到的张量变化率。利用前面给出的 $\dot{\boldsymbol{A}}$ 和 $\boldsymbol{W}$ 的变换法则，可以严格证明 Jaumann 导数是客观的，即 $(\overset{\circ}{\boldsymbol{A}})^* = \boldsymbol{Q}(\overset{\circ}{\boldsymbol{A}})\boldsymbol{Q}^{\mathsf{T}}$。

#### 上随体（Oldroyd）导数

**[上随体导数](@entry_id:756365)**（upper-convected derivative），也称为 Oldroyd 导数，是另一种重要的客观导数，在[聚合物流变学](@entry_id:144905)中尤其常用。其定义为：
$$
\stackrel{\nabla}{\boldsymbol{A}} = \dot{\boldsymbol{A}} - \boldsymbol{L}\boldsymbol{A} - \boldsymbol{A}\boldsymbol{L}^{\mathsf{T}}
$$
这个定义看起来比 Jaumann 导数更复杂，因为它涉及整个[速度梯度张量](@entry_id:270928) $\boldsymbol{L}$ 而不仅仅是其反对称部分。然而，正是这种形式赋予了它深刻的几何意义，我们将在稍后探讨。同样，利用 $\dot{\boldsymbol{A}}$ 和 $\boldsymbol{L}$ 的变换法则，可以证明[上随体导数](@entry_id:756365)是客观的，即 $(\stackrel{\nabla}{\boldsymbol{A}})^* = \boldsymbol{Q}(\stackrel{\nabla}{\boldsymbol{A}})\boldsymbol{Q}^{\mathsf{T}}$ 。

#### [下随体导数](@entry_id:1127499)

与[上随体导数](@entry_id:756365)相对应的是**[下随体导数](@entry_id:1127499)**（lower-convected derivative），其定义为：
$$
\stackrel{\triangle}{\boldsymbol{A}} = \dot{\boldsymbol{A}} + \boldsymbol{L}^{\mathsf{T}}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{L}
$$
[下随体导数](@entry_id:1127499)与[上随体导数](@entry_id:756365)在 $\boldsymbol{L}$ 和 $\boldsymbol{L}^{\mathsf{T}}$ 的符号和位置上有所不同，但它同样是客观的，即 $(\stackrel{\triangle}{\boldsymbol{A}})^* = \boldsymbol{Q}(\stackrel{\triangle}{\boldsymbol{A}})\boldsymbol{Q}^{\mathsf{T}}$ 。

#### 三种导数的结构关系

为了更好地理解这三种导数之间的联系，我们可以将上随体和[下随体导数](@entry_id:1127499)用变形率张量 $\boldsymbol{D}$ 和[涡量张量](@entry_id:189621) $\boldsymbol{W}$ 来表示 。利用 $\boldsymbol{L} = \boldsymbol{D} + \boldsymbol{W}$ 和 $\boldsymbol{L}^{\mathsf{T}} = \boldsymbol{D} - \boldsymbol{W}$，我们得到：
$$
\stackrel{\nabla}{\boldsymbol{A}} = \dot{\boldsymbol{A}} - (\boldsymbol{D}+\boldsymbol{W})\boldsymbol{A} - \boldsymbol{A}(\boldsymbol{D}-\boldsymbol{W}) = (\dot{\boldsymbol{A}} - \boldsymbol{W}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{W}) - (\boldsymbol{D}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{D}) = \overset{\circ}{\boldsymbol{A}} - (\boldsymbol{D}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{D})
$$
$$
\stackrel{\triangle}{\boldsymbol{A}} = \dot{\boldsymbol{A}} + (\boldsymbol{D}-\boldsymbol{W})\boldsymbol{A} + \boldsymbol{A}(\boldsymbol{D}+\boldsymbol{W}) = (\dot{\boldsymbol{A}} - \boldsymbol{W}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{W}) + (\boldsymbol{D}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{D}) = \overset{\circ}{\boldsymbol{A}} + (\boldsymbol{D}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{D})
$$
这些关系揭示了一个清晰的结构：
1.  上随体和[下随体导数](@entry_id:1127499)都内含了 Jaumann 导数，即它们都以相同的方式对流体的局部旋转进行了修正。
2.  它们的区别在于如何处理由变形率 $\boldsymbol{D}$ 引起的效应。[上随体导数](@entry_id:756365)减去了一个与 $\boldsymbol{D}$ 相关的项，而[下随体导数](@entry_id:1127499)则加上了这一项。这表明它们对材料拉伸的描述方式不同，这与它们各自的几何意义密切相关。

### 几何与物理诠释

客观导数的选择并非任意，它深刻地依赖于所研究张量的物理本质。这种本质通过张量在变形过程中的[几何变换](@entry_id:150649)特性来体现，即它是**逆变**（contravariant）的还是**协变**（covariant）的。

#### [上随体导数](@entry_id:756365)与[逆变张量](@entry_id:636697)

[上随体导数](@entry_id:756365)与[逆变张量](@entry_id:636697)的演化紧密相连。[逆变张量](@entry_id:636697)与物质**线元**（line elements）的变换行为类似。在聚合物稀溶液模型中，聚合物链可以被抽象为连接两个珠子的哑铃，其端到端向量 $\boldsymbol{q}$ 就是一个物质线元。由这些向量构成的二阶[构象张量](@entry_id:1122882)，如 $\boldsymbol{C} = \langle \boldsymbol{q} \otimes \boldsymbol{q} \rangle$，其行为就像一个二阶[逆变张量](@entry_id:636697) 。

为了理解上随体[导数的几何意义](@entry_id:159499)，我们可以将一个欧拉空间中的[张量场](@entry_id:190170) $\boldsymbol{A}$ 通过变形梯度 $\boldsymbol{F} = \partial \boldsymbol{x} / \partial \boldsymbol{X}$ **拉回**（pull back）到参考构型，得到一个拉格朗日物质张量。对于[逆变张量](@entry_id:636697)，其拉回操作定义为：
$$
\boldsymbol{A}_R(\boldsymbol{X}, t) = \boldsymbol{F}^{-1} \boldsymbol{A}(\boldsymbol{x}, t) \boldsymbol{F}^{-\mathsf{T}}
$$
这个操作的意义是，在一个随物质变形的坐标系中来观察张量 $\boldsymbol{A}$。对 $\boldsymbol{A}_R$ 求物质导数（即对时间求偏导，保持物质坐标 $\boldsymbol{X}$ 不变），可以得到 ：
$$
\dot{\boldsymbol{A}}_R = \frac{D\boldsymbol{A}_R}{Dt} = \boldsymbol{F}^{-1} \left( \dot{\boldsymbol{A}} - \boldsymbol{L}\boldsymbol{A} - \boldsymbol{A}\boldsymbol{L}^{\mathsf{T}} \right) \boldsymbol{F}^{-\mathsf{T}} = \boldsymbol{F}^{-1} (\stackrel{\nabla}{\boldsymbol{A}}) \boldsymbol{F}^{-\mathsf{T}}
$$
这个优美的结果表明，[空间张量](@entry_id:185799) $\boldsymbol{A}$ 的[上随体导数](@entry_id:756365) $\stackrel{\nabla}{\boldsymbol{A}}$，经过拉回操作后，恰好等于其对应的物质张量 $\boldsymbol{A}_R$ 的[物质导数](@entry_id:262900)。换言之，**[上随体导数](@entry_id:756365)衡量的是在一个随物质线元一起平移、旋转和拉伸的参考系中观察到的张量变化率**。

一个重要的例子是**左柯西-格林变形张量** $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^{\mathsf{T}}$。它本身就描述了物质[线元](@entry_id:196833)在变形后的拉伸和取向。可以证明其物质导数为 $\dot{\boldsymbol{B}} = \boldsymbol{L}\boldsymbol{B} + \boldsymbol{B}\boldsymbol{L}^{\mathsf{T}}$。代入[上随体导数](@entry_id:756365)的定义，我们得到一个基本恒等式 ：
$$
\stackrel{\nabla}{\boldsymbol{B}} = \dot{\boldsymbol{B}} - \boldsymbol{L}\boldsymbol{B} - \boldsymbol{B}\boldsymbol{L}^{\mathsf{T}} = (\boldsymbol{L}\boldsymbol{B} + \boldsymbol{B}\boldsymbol{L}^{\mathsf{T}}) - (\boldsymbol{L}\boldsymbol{B} + \boldsymbol{B}\boldsymbol{L}^{\mathsf{T}}) = \boldsymbol{0}
$$
$\stackrel{\nabla}{\boldsymbol{B}} = \boldsymbol{0}$ 的物理意义非常直观：由于 $\boldsymbol{B}$ 张量本身就完整地描述了材料[线元](@entry_id:196833)的变形，在一个随[线元](@entry_id:196833)变形的坐标系中观察它，自然会发现它没有“变化”。这正是[上随体导数](@entry_id:756365)为零所表达的含义。因此，对于描述[聚合物拉伸](@entry_id:1129920)等基于线元概念的物理模型，[上随体导数](@entry_id:756365)是自然而然的选择，例如在上随体 Maxwell (UCM) 模型中 。

#### [下随体导数](@entry_id:1127499)与[协变张量](@entry_id:634493)

与[上随体导数](@entry_id:756365)相对应，[下随体导数](@entry_id:1127499)与[协变张量](@entry_id:634493)的演化相关。[协变张量](@entry_id:634493)与物质**面元**（surface elements）的变换行为相关。一个二阶协变[空间张量](@entry_id:185799) $\boldsymbol{S}$ 的拉回操作定义为：
$$
\boldsymbol{S}_R(\boldsymbol{X}, t) = \boldsymbol{F}^{\mathsf{T}} \boldsymbol{S}(\boldsymbol{x}, t) \boldsymbol{F}
$$
对其求[物质导数](@entry_id:262900)，可以得到与[上随体导数](@entry_id:756365)相对应的结果 ：
$$
\dot{\boldsymbol{S}}_R = \boldsymbol{F}^{\mathsf{T}} \left( \dot{\boldsymbol{S}} + \boldsymbol{L}^{\mathsf{T}}\boldsymbol{S} + \boldsymbol{S}\boldsymbol{L} \right) \boldsymbol{F} = \boldsymbol{F}^{\mathsf{T}} (\stackrel{\triangle}{\boldsymbol{S}}) \boldsymbol{F}
$$
这个关系表明，**[下随体导数](@entry_id:1127499)衡量的是在一个随物质面元一起平移、旋转和变形的参考系中观察到的张量变化率**。因此，当一个物理量（如某种应力张量）的物理本质与[表面力](@entry_id:188034)或[法向量](@entry_id:264185)相关时，[下随体导数](@entry_id:1127499)便成为构建其本构模型的恰当选择。

综上所述，[客观时间导数](@entry_id:1129024)的概念源于物质标架无关性这一基本物理原理。虽然存在多种形式的客观导数，但上随体和[下随体导数](@entry_id:1127499)因其深刻的几何意义而尤为重要。它们分别与[逆变张量](@entry_id:636697)（与线元相关）和[协变张量](@entry_id:634493)（与面元相关）的随体变化率相联系。因此，在为特定物理问题选择合适的本构模型时，理解张量所代表的物理量的几何属性，并选用与之匹配的[客观时间导数](@entry_id:1129024)，是至关重要的一步。