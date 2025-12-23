## 引言
对[聚合物溶液](@entry_id:145399)和熔体等粘弹性流体的精确模拟，在材料加工、[生物工程](@entry_id:270890)和能源等领域至关重要。然而，当流动的弹性效应远超粘性效应时——即在高韦森伯格数（Wi）下——标准的计算方法往往会遭遇被称为“高韦森伯格数难题”（HWNP）的数值崩溃。这一难题长期以来限制了我们对强弹性流动的预测和理解能力，构成了一个亟待解决的知识缺口。

本文旨在系统性地阐释两种为克服HWNP而发展的强大技术：**[应力分裂](@entry_id:1132510)（stress-splitting）**和**[对数构象重构](@entry_id:1127423)（log-conformation reformulation, LCR）**。通过阅读本文，您将深入理解这些先进方法背后的核心思想，并掌握它们如何从根本上保证[数值模拟](@entry_id:146043)的稳定性和物理真实性。

为实现这一目标，本文将分为三个核心章节。在接下来的**“原理与机制”**一章中，我们将从基本控制方程出发，揭示传统方法失效的根源，并详细推导[应力分裂](@entry_id:1132510)和[对数构象重构](@entry_id:1127423)的数学与物理基础。随后，在**“应用与跨学科连接”**一章中，我们将展示这些技术如何在基准问题、实验对比和复杂流动模拟中发挥作用，并揭示其与材料科学及[数值分析](@entry_id:142637)等领域的深刻联系。最后，**“动手实践”**部分将通过一系列计算练习，帮助您将理论知识转化为实践技能。

## 原理与机制

在上一章引言的基础上，本章将深入探讨在粘弹性流体模拟中，为克服高韦森伯格数难题 (High Weissenberg Number Problem, HWNP) 而发展的两种核心技术：**[应力分裂](@entry_id:1132510) (stress-splitting)** 和 **[对数构象重构](@entry_id:1127423) (log-conformation reformulation)**。我们将从基本控制方程出发，揭示标准数值方法失效的根本原因，并系统地阐述这些先进技术背后的物理原理和数学机制。

### 柯西[应力张量](@entry_id:148973)与[应力分裂](@entry_id:1132510)

粘弹性流体的运动由连续介质力学的基本守恒定律描述。对于一个密度为常数 $\rho$ 的[不可压缩流体](@entry_id:181066)，其[动量守恒](@entry_id:149964)方程（或称[柯西动量方程](@entry_id:187010)）和[不可压缩性约束](@entry_id:750592)分别为：
$$
\rho(\partial_t \boldsymbol{u} + \boldsymbol{u}\cdot\nabla \boldsymbol{u}) = \nabla \cdot \boldsymbol{\sigma}
$$
$$
\nabla \cdot \boldsymbol{u} = 0
$$
其中 $\boldsymbol{u}(\boldsymbol{x},t)$ 是速度场，$\boldsymbol{\sigma}(\boldsymbol{x},t)$ 是柯西应力张量。

与[牛顿流体](@entry_id:263796)不同，粘弹性流体的[应力张量](@entry_id:148973)包含了更为复杂的贡献。一个普遍的模型是将总应力 $\boldsymbol{\sigma}$ 分解为三个部分：各向同性的压力项、牛顿溶剂的粘性贡献以及由[聚合物微观结构](@entry_id:185362)产生的弹性贡献  。这种分解本身就是一种物理意义上的 **[应力分裂](@entry_id:1132510)**：
$$
\boldsymbol{\sigma} = -p\boldsymbol{I} + \boldsymbol{\tau}_s + \boldsymbol{\tau}_p
$$
在这里，$p$ 是压力，在不可压缩流中，它主要扮演着[拉格朗日乘子](@entry_id:142696)的角色，其值在流场中不断调整以确保速度场满足 $\nabla \cdot \boldsymbol{u} = 0$ 的约束。$\boldsymbol{I}$ 是单位张量。$\boldsymbol{\tau}_s$ 是溶剂产生的粘性应力，对于粘度为 $\eta_s$ 的牛顿溶剂，它与对称变形率张量 $\boldsymbol{D} = \frac{1}{2}(\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^\top)$ 呈线性关系：
$$
\boldsymbol{\tau}_s = 2\eta_s \boldsymbol{D}
$$
$\boldsymbol{\tau}_p$ 是聚合物附加[应力张量](@entry_id:148973)，它源于聚合物分子链在流动中的拉伸和取向，是流体弹性的主要来源。

将此[应力分解](@entry_id:272862)代入动量方程，并利用不可压缩条件（即 $\nabla \cdot ((\nabla \boldsymbol{u})^\top) = \nabla(\nabla \cdot \boldsymbol{u}) = \boldsymbol{0}$），溶剂项的散度可以简化为 $\nabla \cdot (2\eta_s \boldsymbol{D}) = \eta_s \nabla^2 \boldsymbol{u}$。于是，动量方程呈现出一种明确分裂的形式：
$$
\rho(\partial_t \boldsymbol{u} + \boldsymbol{u}\cdot\nabla \boldsymbol{u}) = -\nabla p + \eta_s \nabla^2 \boldsymbol{u} + \nabla \cdot \boldsymbol{\tau}_p
$$
这个方程清晰地展示了作用在流体微元上的各种力：压力[梯度力](@entry_id:166847)、溶剂[粘性力](@entry_id:263294)（一个扩散项）和聚合物弹性力。在数值计算中，这种形式为发展高效的算法提供了基础。例如，我们可以对线性、稳定的溶剂粘性项采用隐式处理以获得更好的稳定性，而对高度[非线性](@entry_id:637147)的聚合物应力项则采用显式处理，这构成了数值 **算子分裂 (operator-splitting)** 策略的核心思想 。

为了更好地分析流动特性，我们常将方程无量纲化。选取特征长度 $L$、[特征速度](@entry_id:165394) $U$ 和总零剪切粘度 $\eta_0$，我们可以定义雷诺数 $\mathrm{Re} = \frac{\rho U L}{\eta_0}$ 和[溶剂粘度](@entry_id:264247)比 $\beta = \frac{\eta_s}{\eta_0}$ 。总零[剪切粘度](@entry_id:141046) $\eta_0$ 是[溶剂粘度](@entry_id:264247) $\eta_s$ 与聚合物在零剪切速率下贡献的粘度 $\eta_p$ 之和，即 $\eta_0 = \eta_s + \eta_p$。例如，若某流体的 $\eta_s = 0.8\,\mathrm{Pa\cdot s}$ 且 $\eta_p = 1.2\,\mathrm{Pa\cdot s}$，则 $\eta_0 = 2.0\,\mathrm{Pa\cdot s}$，[溶剂粘度](@entry_id:264247)比 $\beta = 0.8 / 2.0 = 0.4$。[无量纲化](@entry_id:136704)的动量方程为：
$$
\mathrm{Re}(\partial_t \boldsymbol{u} + \boldsymbol{u}\cdot\nabla \boldsymbol{u}) = -\nabla p + \beta \nabla^2 \boldsymbol{u} + \nabla \cdot \boldsymbol{\tau}_p
$$
此形式突出了不同物理效应的相对重要性。

### [聚合物构象](@entry_id:180389)张量及其物理约束

聚合物附加应力 $\boldsymbol{\tau}_p$ 不是一个独立的变量，它本身由更底层的微观状态决定。在哑铃模型等动理学理论中，聚合物分子的平均拉伸和取向状态由一个[二阶张量](@entry_id:199780)——**构象张量 (conformation tensor)** $\boldsymbol{A}$ 来描述。它被定义为聚合物端到端矢量 $\boldsymbol{Q}$ 的系综平均二次矩 ：
$$
\boldsymbol{A} = \langle \boldsymbol{Q} \otimes \boldsymbol{Q} \rangle = \int_{\mathbb{R}^{d}} (\boldsymbol{Q} \otimes \boldsymbol{Q}) \psi(\boldsymbol{Q}, t) \,d\boldsymbol{Q}
$$
其中 $\psi(\boldsymbol{Q}, t)$ 是在时刻 $t$ 找到一个端到端矢量为 $\boldsymbol{Q}$ 的聚合物的[概率密度函数](@entry_id:140610)。聚合物应力 $\boldsymbol{\tau}_p$ 则是构象张量 $\boldsymbol{A}$ 的函数，例如在[Oldroyd-B模型](@entry_id:752895)中，$\boldsymbol{\tau}_p = G(\boldsymbol{A}-\boldsymbol{I})$，其中 $G$ 是弹性模量。

[构象张量](@entry_id:1122882) $\boldsymbol{A}$ 具有一个至关重要的物理属性：它必须是 **[对称正定](@entry_id:145886) (Symmetric Positive-Definite, SPD)** 的。
- **对称性** 直接源于其定义。由于标量乘法是可交换的 ($Q_i Q_j = Q_j Q_i$)，我们有 $A_{ij} = \langle Q_i Q_j \rangle = \langle Q_j Q_i \rangle = A_{ji}$，因此 $\boldsymbol{A} = \boldsymbol{A}^\top$。
- **[正定性](@entry_id:149643)** 则源于概率的非负性。对于任意非[零向量](@entry_id:156189) $\boldsymbol{x}$，我们可以构造二次型 $\boldsymbol{x}^\top \boldsymbol{A} \boldsymbol{x}$：
$$
\boldsymbol{x}^\top \boldsymbol{A} \boldsymbol{x} = \boldsymbol{x}^\top \langle \boldsymbol{Q} \otimes \boldsymbol{Q} \rangle \boldsymbol{x} = \langle \boldsymbol{x}^\top (\boldsymbol{Q} \otimes \boldsymbol{Q}) \boldsymbol{x} \rangle = \langle (\boldsymbol{x}^\top \boldsymbol{Q})(\boldsymbol{Q}^\top \boldsymbol{x}) \rangle = \langle (\boldsymbol{x} \cdot \boldsymbol{Q})^2 \rangle
$$
因为 $(\boldsymbol{x} \cdot \boldsymbol{Q})^2 \ge 0$ 且[概率密度](@entry_id:175496) $\psi(\boldsymbol{Q}, t) \ge 0$，所以积分 $\int (\boldsymbol{x} \cdot \boldsymbol{Q})^2 \psi \,d\boldsymbol{Q}$ 必然是非负的，即 $\boldsymbol{A}$ 是半正定的。在包含热噪声的物理现实系统中，聚合物构型不会被限制在一个与 $\boldsymbol{x}$ 正交的[超平面](@entry_id:268044)上，因此总能在 $\boldsymbol{x} \cdot \boldsymbol{Q} \neq 0$ 的区域找到非零的概率密度。这确保了该积分严格为正，即 $\boldsymbol{x}^\top \boldsymbol{A} \boldsymbol{x} > 0$。因此，[构象张量](@entry_id:1122882) $\boldsymbol{A}$ 必须是严格的[对称正定矩阵](@entry_id:136714) 。

这个SPD约束不仅是一个物理要求，也是后续引入[对数构象重构](@entry_id:1127423)的数学前提。

### 高韦森伯格数难题

构象张量 $\boldsymbol{A}$ 的演化由一个本构方程决定。以[Oldroyd-B模型](@entry_id:752895)为例，其演化方程是一个张量[输运方程](@entry_id:174281)：
$$
\frac{D \boldsymbol{A}}{D t} = (\nabla \boldsymbol{u})\boldsymbol{A} + \boldsymbol{A}(\nabla \boldsymbol{u})^\top - \frac{1}{\lambda}(\boldsymbol{A}-\boldsymbol{I})
$$
其中 $\frac{D}{Dt}$ 是物质导数，$\lambda$ 是聚合物的松弛时间。左侧是物质导数，右侧第一、二项描述了[速度梯度](@entry_id:261686)场 $\nabla\boldsymbol{u}$ 对[聚合物构象](@entry_id:180389)的拉伸和旋转作用（运动学拉伸），第三项则描述了构象向各向同性[平衡态](@entry_id:270364) $\boldsymbol{I}$ 的松弛。

我们可以将该方程改写为使用[上随体导数](@entry_id:756365) $\overset{\nabla}{\boldsymbol{A}}$ 的形式：
$$
\overset{\nabla}{\boldsymbol{A}} \equiv \frac{D \boldsymbol{A}}{D t} - (\nabla \boldsymbol{u})\boldsymbol{A} - \boldsymbol{A}(\nabla \boldsymbol{u})^\top = -\frac{1}{\lambda}(\boldsymbol{A}-\boldsymbol{I})
$$
**韦森伯格数 (Weissenberg number, Wi)** 定义为松弛时间 $\lambda$ 与流动特征时间 $\tau_f$（例如 $\tau_f = L/U$）的比值，即 $\mathrm{Wi} = \lambda/\tau_f$。当 $\mathrm{Wi} \gg 1$ 时，意味着聚合物的松弛非常缓慢，流动变形效应占据主导地位。此时，本构方程近似变为一个[双曲型方程](@entry_id:145657)：
$$
\overset{\nabla}{\boldsymbol{A}} \approx \boldsymbol{0} \quad \text{或} \quad \frac{D \boldsymbol{A}}{D t} \approx (\nabla \boldsymbol{u})\boldsymbol{A} + \boldsymbol{A}(\nabla \boldsymbol{u})^\top
$$
在强拉伸流区域，运动学拉伸项会导致 $\boldsymbol{A}$ 的特征值沿[流线](@entry_id:266815)呈指数增长。这在物理上对应于聚合物分子链被极度拉伸和取向，形成[应力集中](@entry_id:160987)区域。

**高韦森伯格数难题 (HWNP)** 正是源于此。它是一个 **数值不稳定性** 问题，而非物理不稳定性。当标准数值方法（如有限元或[有限差分](@entry_id:167874)）被直接应用于求解 $\boldsymbol{A}$ 的演化方程时，[离散化误差](@entry_id:147889)（如[截断误差](@entry_id:140949)或[插值误差](@entry_id:139425)）不可避免。在 $\boldsymbol{A}$ 的特征值经历指数增长和剧烈变化时，这些小误差可能导致计算出的构象张量 $\boldsymbol{A}_h$ 失去其SPD属性，例如出现一个微小的负特征值。一旦这种情况发生，运动学拉伸项会作用于这个非物理的负特征值，导致其幅值也呈[指数增长](@entry_id:141869)，产生巨大的、非物理的负应力。在高Wi下，方程的双曲特性会迅速将这种局部数值崩溃传播到整个计算域，最终导致整个模拟发散 。

我们可以通过一个简单的思想实验来具体说明这种失效 。考虑一个均匀平面拉伸流，其速度梯度为 $\boldsymbol{L} = \mathrm{diag}(\varepsilon, -\varepsilon)$。如果我们使用简单的一阶显式欧拉格式来离散构象方程的时间演化，从初始状态 $\boldsymbol{A}^0 = \boldsymbol{I}$ 出发，一步之后得到的构象张量为：
$$
\boldsymbol{A}^{1} = \boldsymbol{I} + \Delta t(2\boldsymbol{L}) = \begin{pmatrix} 1 + 2\varepsilon\Delta t  0 \\ 0  1 - 2\varepsilon\Delta t \end{pmatrix}
$$
$\boldsymbol{A}^1$ 的第二个特征值是 $1 - 2\varepsilon\Delta t$。为了保持正定性，该值必须为正，即 $1 - 2\varepsilon\Delta t  0$，这要求时间步长 $\Delta t  \frac{1}{2\varepsilon}$。如果时间步长超过这个由流场拉伸率 $\varepsilon$ 决定的临界值，计算出的 $\boldsymbol{A}^1$ 将失去正定性，从而引发数值不稳定。这清楚地表明，即使在精确的不可压缩流场中，标准离散格式也存在固有的缺陷，无法无条件地保证SPD约束。

### [对数构象重构](@entry_id:1127423)：一种稳健的解决方案

为了从根本上解决HWNP，研究者们提出了一种优雅而强大的方法：**[对数构象重构](@entry_id:1127423) (Log-Conformation Reformulation, LCR)**。其核心思想不是在[数值算法](@entry_id:752770)层面进行修补，而是通过[变量替换](@entry_id:141386)，将[演化方程](@entry_id:268137)重构于一个能够自然满足SPD约束的数学空间中 。

LCR引入了一个新的[张量场](@entry_id:190170) $\boldsymbol{\Psi}$，定义为构象张量 $\boldsymbol{A}$ 的[矩阵对数](@entry_id:169041)：
$$
\boldsymbol{\Psi} = \log \boldsymbol{A}
$$
相应的，构象张量由 $\boldsymbol{\Psi}$ 通过矩阵指数重构：
$$
\boldsymbol{A} = \exp \boldsymbol{\Psi}
$$
这种变换的巧妙之处在于，它将SPD约束的强制执行变成了代数上的必然。

#### 对数变换的数学基础

[矩阵对数](@entry_id:169041)和指数的定义依赖于[谱分解](@entry_id:173707)（即特征分解）。根据[谱定理](@entry_id:136620)，任何一个[实对称矩阵](@entry_id:192806) $\boldsymbol{A}$ 都可以被[正交对角化](@entry_id:149411)为 $\boldsymbol{A} = \boldsymbol{R}\boldsymbol{\Lambda}\boldsymbol{R}^\top$，其中 $\boldsymbol{R}$ 是由其标准[正交特征向量](@entry_id:155522)构成的[正交矩阵](@entry_id:169220)，$\boldsymbol{\Lambda}$ 是由其对应的实特征值 $\lambda_i$ 构成的[对角矩阵](@entry_id:637782)。

由于 $\boldsymbol{A}$ 是SPD的，其所有特征值 $\lambda_i$ 都是严格正数。这使得我们可以明确地定义其[矩阵对数](@entry_id:169041)  ：
$$
\boldsymbol{\Psi} = \log \boldsymbol{A} := \boldsymbol{R} (\log \boldsymbol{\Lambda}) \boldsymbol{R}^\top = \boldsymbol{R} \,\mathrm{diag}(\ln \lambda_1, \dots, \ln \lambda_d) \,\boldsymbol{R}^\top
$$
由于 $\ln \lambda_i$ 都是实数，$\boldsymbol{\Psi}$ 是一个良定义的[实对称矩阵](@entry_id:192806)。

反过来，对于任意一个[实对称矩阵](@entry_id:192806) $\boldsymbol{\Psi}$，其[矩阵指数](@entry_id:139347) $\boldsymbol{A} = \exp \boldsymbol{\Psi}$ 必然是SPD的。这是因为 $\exp \boldsymbol{\Psi}$ 也是对称的，并且其特征值为 $e^{\psi_i}$（其中 $\psi_i$ 是 $\boldsymbol{\Psi}$ 的实特征值），这些特征值永远是正数。因此，通过求解 $\boldsymbol{\Psi}$ 的演化，然后通过[指数映射](@entry_id:137184)重构 $\boldsymbol{A}$，我们从代数上保证了构象张量的SPD属性，无论离散化误差如何，计算出的 $\boldsymbol{A}$ 都将保持物理上的[可实现性](@entry_id:193701)。

#### [对数构象重构](@entry_id:1127423)的稳定化机理

LCR之所以能够有效缓解HWNP，其背后有两大关键机理 ：

1.  **线性化[指数增长](@entry_id:141869)**：在强拉伸流中，$\boldsymbol{A}$ 的特征值 $\lambda_i$ 随时间 $t$ 呈[指数增长](@entry_id:141869)，形如 $\lambda_i(t) \sim \exp(\alpha t)$。通过[对数变换](@entry_id:267035)，对应的 $\boldsymbol{\Psi}$ 的特征值 $\psi_i = \ln \lambda_i$ 则变为[线性增长](@entry_id:157553)，即 $\psi_i(t) \sim \alpha t$。这种从乘性增长到加性增长的转变，极大地缓和了方程的刚性，使得数值求解变得更加稳定和容易。

2.  **压缩[特征值谱](@entry_id:1124216)**：HWNP的另一个特征是 $\boldsymbol{A}$ 的[特征值谱](@entry_id:1124216)变得极其宽广，即最大特征值 $\lambda_{\max}$ 与[最小特征值](@entry_id:177333) $\lambda_{\min}$ 的比值（即[条件数](@entry_id:145150) $\kappa = \lambda_{\max}/\lambda_{\min}$）可能跨越许多数量级。这会严重恶化数值问题的条件。[对数变换](@entry_id:267035)将这个巨大的乘性尺度差距转变为一个温和的加性尺度差距。$\boldsymbol{\Psi}$ 的特征值范围为：
    $$
    \psi_{\max} - \psi_{\min} = \ln \lambda_{\max} - \ln \lambda_{\min} = \ln(\lambda_{\max}/\lambda_{\min}) = \ln(\kappa)
    $$
    例如，一个高达 $10^{10}$ 的[条件数](@entry_id:145150)在[对数空间](@entry_id:270258)中仅对应约 $23$ 的特征值范围。这种谱压缩效应显著改善了数值求解的条件，提高了精度和鲁棒性。

#### 对数[构象张量](@entry_id:1122882)的演化方程

将[变量替换](@entry_id:141386) $\boldsymbol{A} = \exp \boldsymbol{\Psi}$ 代入原始的本构方程，并通过复杂的[矩阵微积分](@entry_id:181100)运算，可以推导出 $\boldsymbol{\Psi}$ 自身的[演化方程](@entry_id:268137)。对于[Oldroyd-B模型](@entry_id:752895)，该方程由Fattal和Kupferman首次导出，其形式相当复杂 。一个关键特征是，流动中的旋转部分（由速度梯度的反对称部分，即[涡量张量](@entry_id:189621) $\boldsymbol{W}$ 描述）在 $\boldsymbol{\Psi}$ 的方程中以[交换子](@entry_id:158878) $[\boldsymbol{W}, \boldsymbol{\Psi}] = \boldsymbol{W}\boldsymbol{\Psi} - \boldsymbol{\Psi}\boldsymbol{W}$ 的形式出现。完整的方程（这里仅作展示，不作推导）为：
$$
\frac{\mathrm{D} \boldsymbol{\Psi}}{\mathrm{D} t} - [\boldsymbol{W},\boldsymbol{\Psi}] \;=\; 2\boldsymbol{B} \;-\; \frac{1}{\lambda}\left(\boldsymbol{I}-e^{-\boldsymbol{\Psi}}\right)
$$
其中 $\boldsymbol{B}$ 是一个与对称变形率张量 $\boldsymbol{D}$ 和 $\boldsymbol{\Psi}$ 自身相关的复杂[对称张量](@entry_id:148092)。虽然此方程看起来比原始的 $\boldsymbol{A}$ 方程更复杂，但其优越的数值特性使其成为现代[粘弹性](@entry_id:148045)流模拟中的首选方法。

### [非线性](@entry_id:637147)[本构模型](@entry_id:174726)与数值分裂格式

以上讨论主要基于线性的[Oldroyd-B模型](@entry_id:752895)。对于更真实的聚合物模型，如 **FENE-P (Finitely Extensible Nonlinear Elastic with Peterlin approximation)** 模型，[本构方程](@entry_id:138559)的[非线性](@entry_id:637147)会进一步加剧。在[FENE-P模型](@entry_id:1124902)中，松弛项被修改为包含一个依赖于[构象张量](@entry_id:1122882)迹 $\mathrm{tr}(\boldsymbol{A})$ 的[非线性](@entry_id:637147)函数 $f(\boldsymbol{A})$ ：
$$
\overset{\nabla}{\boldsymbol{A}} = -\frac{1}{\lambda}[f(\boldsymbol{A})\boldsymbol{A}-\boldsymbol{I}], \quad \text{其中} \quad f(\boldsymbol{A}) = \frac{L^2-d}{L^2 - \operatorname{tr}(\boldsymbol{A})}
$$
$L$ 是聚合物的最大可拉伸长度，$d$ 是空间维度。当 $\mathrm{tr}(\boldsymbol{A})$ 接近 $L^2$ 时，$f(\boldsymbol{A})$ 趋于无穷，代表了弹簧的“硬化”，这使得方程的刚性问题比[Oldroyd-B模型](@entry_id:752895)严重得多，从而对数值方法的鲁棒性提出了更高的要求。

至此，我们将物理上的[应力分裂](@entry_id:1132510)和数值上的LCR与 **算子分裂 (operator splitting)** 算法联系起来，形成一个完整的计算框架 。一个典型的现代算法（如[Strang分裂](@entry_id:755497)）在一个时间步 $\Delta t$ 内按以下顺序执行：

1.  **第一步（动量/压力求解，半步）**: 求解一个类Navier-Stokes系统，时长为 $\Delta t/2$。此步骤通常将聚合物应力项作为显式[源项处理](@entry_id:755077)，并使用[投影法](@entry_id:147401)求解压力以保证速度场的无散性。
    $$
    \rho(\partial_t \boldsymbol{u}) = -\nabla p + \eta_s \nabla^2 \boldsymbol{u} + \nabla\cdot\boldsymbol{\tau}_p^{n}
    $$

2.  **第二步（[本构方程](@entry_id:138559)求解，全步）**: 使用第一步更新得到的速度场，求解对数[构象张量](@entry_id:1122882) $\boldsymbol{\Psi}$ 的[演化方程](@entry_id:268137)，时长为 $\Delta t$。这一步的核心是LCR，它保证了更新后的构象张量 $\boldsymbol{A}^{n+1} = \exp(\boldsymbol{\Psi}^{n+1})$ 保持SPD。

3.  **第三步（动量/压力求解，半步）**: 使用第二步更新后的聚合物应力 $\boldsymbol{\tau}_p^{n+1}$，再次执行与第一步类似的操作，时长为 $\Delta t/2$。

这种对称的分裂格式可以达到二阶时间精度，并且通过将不同物理过程（粘性扩散、压力投影、弹性[应力演化](@entry_id:1132517)）[解耦](@entry_id:160890)，允许为每个子问题选择最合适的数值方法。它既利用了[应力分裂](@entry_id:1132510)带来的灵活性，也依赖于LCR提供的鲁棒性，共同构成了解决高韦森伯格数难题的强大工具。