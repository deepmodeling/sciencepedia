## 引言
在[计算复杂流体](@entry_id:1122778)领域，准确描述[聚合物熔体](@entry_id:192068)、浓溶液等非牛顿流体的力学行为是一项核心挑战。这些材料的应力不仅取决于当前的变形速率，更依赖于其经历的完整变形历史，且常常表现出强烈的[非线性](@entry_id:637147)特征。经典的[线性粘弹性](@entry_id:181219)模型虽然在小变形下行之有效，却无法胜任工业过程中常见的[大变形](@entry_id:167243)和高应变率场景。因此，发展能够捕捉这些复杂现象的[非线性](@entry_id:637147)[本构模型](@entry_id:174726)至关重要。

Kaye-Bernstein-Kearsley-Zapas (K-BKZ) 模型正是为了填补这一知识空白而提出的里程碑式理论。作为一个积分型本构框架，它成功地将[线性粘弹性](@entry_id:181219)的记忆效应与有限变形的非线性响应相结合，为预测和理解复杂流体的宏观流变行为提供了强大而灵活的工具。

本文将系统性地剖析[K-BKZ模型](@entry_id:1126852)。在“原理与机制”一章中，我们将从运动学基础出发，详细构建K-BKZ本构方程，并深入探讨其核心——阻尼函数的物理内涵与作用。接下来的“应用与跨学科联系”一章将通过一系列实际流场案例，展示该模型如何预测[应变软化](@entry_id:755491)、应变硬化及[法向应力差](@entry_id:199507)等关键流变现象，并讨论其适用范围与局限性。最后，“动手实践”部分将提供具体的计算练习，帮助读者将理论知识转化为解决实际问题的能力。通过这一结构，读者将对[K-BKZ模型](@entry_id:1126852)建立起从理论基础到实际应用的全方位理解。

## 原理与机制

本章旨在深入阐述Kaye-Bernstein-Kearsley-Zapas (K-BKZ)积分本构模型的理论基础与核心机制。我们将从描述[大变形](@entry_id:167243)历史所需的运动学量开始，逐步构建完整的本构方程，并探讨其各个组成部分的物理意义、模型假设及其局限性。

### 运动学基础：描述有限变形历史

在粘弹性流体力学中，材料当前的应力状态取决于其完整的变形历史。对于能够经历[大变形](@entry_id:167243)的流体，我们需要一个不依赖于观察者（即客观的）并能量化任意两个时间点之间变形程度的数学工具。

我们首先定义**相对[形变梯度](@entry_id:163749)**（relative deformation gradient） $\boldsymbol{F}(t, t')$。它将流体在过去某一时刻 $t'$ 的构型映射到当前时刻 $t$ 的构型。一个在 $t'$ 时刻的无限小材料线元 $\mathrm{d}\boldsymbol{x}'$ 会被映射为当前时刻的线元 $\mathrm{d}\boldsymbol{x}(t) = \boldsymbol{F}(t, t') \mathrm{d}\boldsymbol{x}'$。对于一个给定的[速度梯度](@entry_id:261686)场 $\boldsymbol{L}(t)$，相对[形变梯度张量](@entry_id:150370)的时间演化遵循以下方程：
$$
\frac{\mathrm{d}}{\mathrm{d}t}\boldsymbol{F}(t, t') = \boldsymbol{L}(t) \boldsymbol{F}(t, t')
$$
其初始条件为 $\boldsymbol{F}(t', t') = \boldsymbol{I}$，其中 $\boldsymbol{I}$ 是单位张量。这个方程的解形式上可以写成一个时间有序指数，以处理在不同时刻[速度梯度](@entry_id:261686) $\boldsymbol{L}(s)$ 不可交换的情况。

然而，相对[形变梯度](@entry_id:163749) $\boldsymbol{F}(t, t')$ 本身并非一个客观的张量。根据**[物质坐标系无关性原理](@entry_id:188784)**（principle of material frame indifference, MFI），[本构方程](@entry_id:138559)必须在任意叠加的刚体运动（[旋转和平移](@entry_id:175994)）下保持形式不变。在一个随时间变化的旋转 $\boldsymbol{Q}(t)$ 下，相对[形变梯度](@entry_id:163749)会按 $\boldsymbol{F}^*(t, t') = \boldsymbol{Q}(t) \boldsymbol{F}(t, t') \boldsymbol{Q}(t')^{\top}$ 进行变换。由于变换涉及两个不同时刻的[旋转张量](@entry_id:191990)（$\boldsymbol{Q}(t)$ 和 $\boldsymbol{Q}(t')$），$\boldsymbol{F}(t, t')$ 不能直接用于构建在当前时刻 $t$ 客观的应力。

为了构建一个客观的[应变度量](@entry_id:755495)，我们采用[形变梯度](@entry_id:163749)的二次型。有两个关键的张量：
1.  **左柯西-格林[应变张量](@entry_id:1132487)**（Left Cauchy-Green strain tensor），在流变学中也常称为**[芬格张量](@entry_id:1124965)**（Finger tensor）：
    $$
    \boldsymbol{B}(t, t') = \boldsymbol{F}(t, t') \boldsymbol{F}(t, t')^{\top}
    $$
2.  **[右柯西-格林应变张量](@entry_id:1131030)**（Right Cauchy-Green strain tensor）：
    $$
    \boldsymbol{C}(t, t') = \boldsymbol{F}(t, t')^{\top} \boldsymbol{F}(t, t')
    $$

根据MFI原理，当前时刻 $t$ 的柯西应力张量 $\boldsymbol{\sigma}(t)$ 必须按 $\boldsymbol{\sigma}^*(t) = \boldsymbol{Q}(t) \boldsymbol{\sigma}(t) \boldsymbol{Q}(t)^{\top}$ 变换。因此，任何用于计算应力的积分核中的张量也必须遵循此变换法则。我们可以验证，[芬格张量](@entry_id:1124965) $\boldsymbol{B}(t, t')$ 的变换规律为 $\boldsymbol{B}^*(t, t') = \boldsymbol{Q}(t) \boldsymbol{B}(t, t') \boldsymbol{Q}(t)^{\top}$，这使其成为一个在当前构型 $t$ 中的客观张量。相反，[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}(t, t')$ 的变换依赖于过去时刻的旋转 $\boldsymbol{Q}(t')$，因此不适合直接用于构建当前时刻的应力。因此，[K-BKZ模型](@entry_id:1126852)及其他相关积分模型均采用[芬格张量](@entry_id:1124965) $\boldsymbol{B}(t, t')$ 作为核心的[应变度量](@entry_id:755495)。

对于[不可压缩材料](@entry_id:159741)（体积守恒，即 $\det\boldsymbol{F}=1$），[芬格张量](@entry_id:1124965)的第三不变量 $\det\boldsymbol{B}=1$。因此，描述其大小的只有两个独立的**[主不变量](@entry_id:193522)**（principal invariants）：
$$
I_1 = \mathrm{tr}(\boldsymbol{B}) \quad \text{和} \quad I_2 = \mathrm{tr}(\boldsymbol{B}^{-1})
$$
这两个[标量不变量](@entry_id:193787)自身也是客观的，它们将在[本构模型](@entry_id:174726)中扮演关键角色。

### 从线性粘弹到[非线性](@entry_id:637147)积分框架

在进入复杂的[非线性](@entry_id:637147)领域之前，回顾[线性粘弹性](@entry_id:181219)的基础是很有裨益的。对于微小变形，**[玻尔兹曼叠加原理](@entry_id:185170)**（Boltzmann superposition principle）是描述[粘弹性](@entry_id:148045)行为的基石。它指出，当前时刻的应力是过去所有应变率历史的线性叠加，通过一个只依赖于时间间隔的**松弛模量** $G(s)$ 加权：
$$
\boldsymbol{\tau}(t) = \int_{-\infty}^{t} G(t-t') \dot{\boldsymbol{\gamma}}(t') \mathrm{d}t'
$$
其中 $\boldsymbol{\tau}$ 是[偏应力张量](@entry_id:267642)，$\dot{\boldsymbol{\gamma}}$ 是[无穷小应变](@entry_id:197162)率张量。实际材料的松弛行为通常可以用**[广义麦克斯韦模型](@entry_id:169862)**（generalized Maxwell model）来描述，即松弛模量由一系列离散的指数衰减模式构成：
$$
G(s) = \sum_{i} G_i \exp(-s/\lambda_i)
$$
其中 $G_i$ 是第 $i$ 个模式的模量，$\lambda_i = \eta_i/G_i$ 是其松弛时间，$\eta_i$ 是相应粘性元件的粘度。

[线性粘弹性](@entry_id:181219)理论的局限性在于它仅适用于[无穷小应变](@entry_id:197162)，且其[应变度量](@entry_id:755495)不是客观的。为了将这一框架推广到能够描述聚合物熔体和浓溶液等[复杂流体](@entry_id:198415)所经历的有限变形，必须进行两个根本性的改造：
1.  **[几何非线性](@entry_id:169896)**：用一个客观的有限[应变张量](@entry_id:1132487)（如[芬格张量](@entry_id:1124965) $\boldsymbol{B}$）取代[无穷小应变张量](@entry_id:167211) $\boldsymbol{\gamma}$。
2.  **[材料非线性](@entry_id:162855)**：允许材料的记忆响应不仅依赖于变形发生的时间，还依赖于变形的“幅度”。

[K-BKZ模型](@entry_id:1126852)正是实现这一推广的经典框架之一。

### K-BKZ[本构方程](@entry_id:138559)

[K-BKZ模型](@entry_id:1126852)是一个积分形式的[本构方程](@entry_id:138559)，它将当前时刻的应力表示为过去所有变形历史的积分。对于不可压缩流体，柯西应力张量 $\boldsymbol{\sigma}(t)$ 分为压力项和[偏应力](@entry_id:163323)项 $\boldsymbol{\tau}(t)$：
$$
\boldsymbol{\sigma}(t) = -p(t)\boldsymbol{I} + \boldsymbol{\tau}(t)
$$
其中 $p(t)$ 是用于满足不可压缩约束的[静水压力](@entry_id:275365)。[K-BKZ模型](@entry_id:1126852)的核心在于[偏应力](@entry_id:163323) $\boldsymbol{\tau}(t)$ 的表达式。一个常见的、被称为**可[因子分解](@entry_id:150389)的[K-BKZ模型](@entry_id:1126852)**（factorable K-BKZ model）的形式如下：
$$
\boldsymbol{\tau}(t) = \int_{-\infty}^{t} M(t-t') h(I_1, I_2) \left[ \boldsymbol{B}(t, t') - \boldsymbol{I} \right] \mathrm{d}t'
$$
让我们逐一解析这个方程的组成部分：

-   $M(t-t')$ 是**记忆函数**（memory function），它是一个只依赖于时间间隔 $s=t-t'$ 的标量函数。它描述了材料的“遗忘”速率，确保了遥远过去的变形对当前应力的影响会随时间衰减，这体现了**衰减记忆原理**（principle of fading memory）。对于广义麦克斯韦谱，记忆函数与松弛模量相关，通常取 $M(s) = -\frac{\mathrm{d}G}{\mathrm{d}s} = \sum_{i} \frac{G_i}{\lambda_i} \exp(-s/\lambda_i)$。

-   $\boldsymbol{B}(t, t') - \boldsymbol{I}$ 是[应变度量](@entry_id:755495)。使用 $\boldsymbol{B}(t, t')$ 保证了客观性。减去单位张量 $\boldsymbol{I}$ 确保了在静止状态下（此时 $\boldsymbol{B} = \boldsymbol{I}$），[偏应力](@entry_id:163323)为零，这对于流体是必须满足的物理要求。

-   $h(I_1, I_2)$ 是**[阻尼函数](@entry_id:1123370)**（damping function），它是[应变不变量](@entry_id:190518) $I_1$ 和 $I_2$ 的一个标量函数。这是[K-BKZ模型](@entry_id:1126852)中引入[材料非线性](@entry_id:162855)的关键。它调节了不同大小的变形对总应力的贡献权重。

### [阻尼函数](@entry_id:1123370)的作用与诠释

[阻尼函数](@entry_id:1123370) $h(I_1, I_2)$ 是区分不同[材料非线性](@entry_id:162855)响应的核心。如果 $h \equiv 1$，[K-BKZ模型](@entry_id:1126852)就退化为**Lodge橡胶状液体模型**（Lodge rubberlike liquid model），该模型在[应变度量](@entry_id:755495)上是线性的。

从微观角度看，阻尼函数的引入具有深刻的物理背景。基于[聚合物网络](@entry_id:191902)理论，如果将流体看作一个由瞬态聚合物链段构成的网络，并假设链段的形变是仿射的且其统计行为服从**[高斯链](@entry_id:154876)**（Gaussian chain）模型，那么推导出的[本构方程](@entry_id:138559)正是[Lodge模型](@entry_id:189750)，即应力与[芬格张量](@entry_id:1124965) $\boldsymbol{B}$ 成正比。

然而，真实的聚合物链具有**有限伸展性**（finite extensibility）。当链段被大幅拉伸时，其行为会偏离高斯统计，产生比线性模型预测的更强的恢复力。这种非高斯效应以及其他观察到的[非线性](@entry_id:637147)现象，如[应变软化](@entry_id:755491)，都可以通过引入[阻尼函数](@entry_id:1123370) $h$ 来进行唯象描述。作为一个依赖于客观[标量不变量](@entry_id:193787)的函数， $h(I_1, I_2)$ 的引入既满足了材料各向同性的要求，也保证了模型的客观性。

[阻尼函数](@entry_id:1123370)的具体形式决定了材料在[非线性](@entry_id:637147)区的宏观力学行为：
-   **应变致稀**或**[应变软化](@entry_id:755491)**（strain thinning/softening）：当材料在[大应变](@entry_id:751152)下表现出的模量或粘度低于线性理论预测时，对应的阻尼函数 $h$ 是[应变不变量](@entry_id:190518)的减函数。即随着应变增大，$h$ 的值小于1并减小。
-   **应变致稠**或**应变硬化**（strain hardening）：当材料在[大应变](@entry_id:751152)下表现出急剧的应力增长时，对应的阻尼函数 $h$ 是[应变不变量](@entry_id:190518)的增函数，其值大于1。

以一个恒定拉伸速率 $\dot{\epsilon}$ 的[单轴拉伸](@entry_id:188287)流场为例，经过时间 $s$ 后，[芬格张量](@entry_id:1124965)的[主值](@entry_id:189577)分量为 $e^{2\dot{\epsilon}s}$ 和 $e^{-\dot{\epsilon}s}$。其第一不变量 $I_1 = e^{2\dot{\epsilon}s} + 2e^{-\dot{\epsilon}s}$ 会随应变（或时间 $s$）的增加而单调增大。此时，如果选用一个随 $I_1$ 减小的[阻尼函数](@entry_id:1123370) $h(I_1)$，那么来自较[大应变](@entry_id:751152)（即较久远的过去）的贡献将被“阻尼”或“衰减”，导致总应力的增长慢于[线性预测](@entry_id:180569)，从而表现出应变致稀的行为。

### 实际应用与扩展

为了更精确地拟合真实聚合物材料的实验数据，通常采用多模式的[K-BKZ模型](@entry_id:1126852)。该模型将总应力视为多个松弛模式贡献的总和，每种模式对应一种特征松弛时间：
$$
\boldsymbol{\tau}(t) = \sum_{i} \int_{-\infty}^{t} M_i(t-t') h_i(I_1, I_2) \left[ \boldsymbol{B}(t, t') - \boldsymbol{I} \right] \mathrm{d}t'
$$
其中 $M_i(s) = (G_i/\lambda_i) \exp(-s/\lambda_i)$ 是第 $i$ 个模式的记忆函数。

这种多模式框架的一个重要扩展是允许每个模式拥有其自身的**模式特定阻尼函数**（mode-specific damping function） $h_i$。其物理意义在于，与不同松弛时间 $\lambda_i$ 相关联的不同[分子尺](@entry_id:166706)度上的运动机制（如短链的运动和长链的纠缠松弛）可能对[大变形](@entry_id:167243)有不同的[非线性响应](@entry_id:188175)。通过为每个[模式指定](@entry_id:920302)不同的 $h_i$，模型可以更灵活地捕捉和[解耦](@entry_id:160890)这些复杂的[非线性](@entry_id:637147)行为。

### 关键假设与局限性：时间-应变可分离性

可[因子分解](@entry_id:150389)的[K-BKZ模型](@entry_id:1126852)的一个核心假设是**时间-应变可分离性**（time-strain separability）。这意味着积分核可以分解为一个只依赖于时间的函数 $M(s)$ 和一个只依赖于应变的函数 $h(I_1, I_2)$ 的乘积。

这个假设的直接推论是，在某一过去时刻 $t'$ 的变形对当前应力 $t$ 的贡献，仅取决于时间差 $s=t-t'$ 和该时刻的相对变形状态 $\boldsymbol{B}(t,t')$，而与材料从构型 $t'$ 演化到构型 $t$ 所经历的**中间路径**无关。换言之，如果两个不同的变形历史在所有过去时刻 $t'$ 都产生了相同的相对[芬格张量](@entry_id:1124965) $\boldsymbol{B}(t,t')$，那么根据可分离的[K-BKZ模型](@entry_id:1126852)，它们在当前时刻 $t$ 的应力将完全相同。

然而，许多[复杂流体](@entry_id:198415)的行为违背了这一假设。一个典型的例子是**触变性**（thixotropy），即材料的粘度或结构会因剪切历史而发生可逆变化。例如，在静置一段时间后，触[变性](@entry_id:165583)流体的内部结构会逐渐“搭建”起来。此时若启动剪切流，会观察到比短时静置后启动时更大的应力超调，因为破坏一个更“坚固”的结构需要更大的力。这种依赖于静置时间的行为无法被时间-应变可分离的模型所描述，因为该模型中的记忆函数 $M(s)$ 是固定不变的，不随流体结构状态的演化而改变。

为了描述这类现象，必须放弃时间-应变可分离性假设。一种改进思路是引入一个或多个**内部结构变量**（internal structural variable），该变量自身遵循一个独立的动力学演化方程。然后，让记忆函数或阻尼函数依赖于这个结构变量在过去时刻 $t'$ 的状态。这样，积分核就变成了一个不可分离的、依赖于两个时间的函数，从而能够捕捉到由于流动诱导的[结构演化](@entry_id:186256)所带来的复杂记忆效应。