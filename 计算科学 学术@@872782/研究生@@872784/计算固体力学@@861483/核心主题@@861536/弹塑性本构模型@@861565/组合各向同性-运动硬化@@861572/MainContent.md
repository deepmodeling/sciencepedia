## 引言
在[计算固体力学](@entry_id:169583)领域，精确预测材料在复杂加载下的力学响应是结构安全性和耐久性分析的基石。然而，许多工程金属材料在承受[循环载荷](@entry_id:181502)时，会表现出传统硬化模型难以描述的复杂行为，如包申格效应、循环硬化/软化和棘轮效应。单纯的等向[硬化](@entry_id:177483)或[随动硬化](@entry_id:172077)模型在模拟这些现象时存在固有局限性，从而形成了一个关键的知识缺口。

为了解决这一挑战，联合等向-[随动硬化](@entry_id:172077)（Combined Isotropic-Kinematic Hardening）模型应运而生。它作为一种高级本构理论，通过同时考虑屈服面的扩张和平移，为精确捕捉材料的[循环塑性](@entry_id:176411)行为提供了强大的数学框架。本文旨在系统性地剖析这一重要模型。在接下来的内容中，我们将首先在“原理与机制”一章中深入探讨其核心力学原理、数学表述和计算方法。随后，我们将在“应用与交叉学科联系”一章中展示该模型如何应用于解决实际工程问题，并揭示其与[材料科学](@entry_id:152226)、岩[土力学](@entry_id:180264)等领域的深刻联系。最后，通过“动手实践”部分提供的具体问题，您将有机会巩固所学知识，并将其付诸实践。

## 原理与机制

在理解了塑性理论的基本框架之后，本章将深入探讨一种更为复杂和贴近工程实际的材料本构模型：联合等向-[随动硬化](@entry_id:172077)（combined isotropic-kinematic hardening）模型。与仅考虑等向硬化或[随动硬化](@entry_id:172077)的模型相比，联合硬化模型能够更精确地描述金属材料在[循环加载](@entry_id:181502)下的复杂行为，例如包申格效应（Bauschinger effect）、循环硬化/软化（cyclic hardening/softening）以及棘轮效应（ratcheting）。本章将系统地阐述其核心原理、物理动机、演化规律、计算方法和[热力学](@entry_id:141121)基础。

### 联合[硬化](@entry_id:177483)[屈服函数](@entry_id:167970)

描述[材料塑性](@entry_id:186852)行为的起点是定义其[弹性极限](@entry_id:186242)，这通过一个标量函数——[屈服函数](@entry_id:167970)——来实现。对于联合硬化模型，其[屈服面](@entry_id:175331)在[应力空间](@entry_id:199156)中既可以平移，也可以扩张。

#### 几何与物理诠释

在[主应力空间](@entry_id:184388)中，对于与[静水压力](@entry_id:275365)无关的金属材料，其初始屈服面通常被描述为一个以原点为中心的圆柱体，即 von Mises 屈服面。其在[偏应力](@entry_id:163323)平面（$\pi$ 平面）上的投影是一个以原点为中心的圆。

*   **[随动硬化](@entry_id:172077) (Kinematic Hardening)** 在几何上表现为[屈服面](@entry_id:175331)的**平移**。[屈服面](@entry_id:175331)的中心不再固定于原点，而是移动到一个由**背应力张量** $\boldsymbol{\alpha}$ 定义的位置。背应力 $\boldsymbol{\alpha}$ 是一个与塑性变形历史相关的内变量，它记录了屈服中心在偏应力空间中的偏移。这种平移机制是模拟包申格效应的关键，即材料在某个方向发生塑性变形后，其在反向加载时的屈服强度会降低。

*   **等向[硬化](@entry_id:177483) (Isotropic Hardening)** 在几何上表现为[屈服面](@entry_id:175331)的**均匀扩张或收缩**。屈服面的尺寸（在 $\pi$ 平面上的半径）会随着塑性变形的累积而改变。这个尺寸的变化由一个标量内变量 $R$ 控制。当 $R$ 增大时，[屈服面](@entry_id:175331)扩张，材料发生[硬化](@entry_id:177483)；反之则发生软化。

联合[硬化](@entry_id:177483)模型将这两种效应结合起来，允许屈服面在平移的同时改变尺寸，从而能够更全面地模拟材料的[循环塑性](@entry_id:176411)行为。

#### 数学表达式

基于上述几何概念，我们可以构建联合[硬化](@entry_id:177483)模型的 von Mises 型[屈服函数](@entry_id:167970)。首先，定义[偏应力张量](@entry_id:267642)为 $\boldsymbol{s} = \boldsymbol{\sigma} - \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})\mathbf{I}$，其中 $\boldsymbol{\sigma}$ 是柯西[应力张量](@entry_id:148973)，$\mathbf{I}$ 是二阶单位张量。由于屈服对[静水压力](@entry_id:275365)不敏感，[屈服函数](@entry_id:167970)仅依赖于偏应力。

为了引入[随动硬化](@entry_id:172077)，我们将[偏应力](@entry_id:163323) $\boldsymbol{s}$ 替换为“有效”或“相对”[偏应力](@entry_id:163323) $\boldsymbol{s} - \boldsymbol{\alpha}$，其中 $\boldsymbol{\alpha}$ 是一个偏量（即 $\mathrm{tr}(\boldsymbol{\alpha}) = 0$）[@problem_id:2652013]。[屈服函数](@entry_id:167970)的具体形式为 [@problem_id:2621864]：

$f(\boldsymbol{\sigma}, \boldsymbol{\alpha}, R) = \sqrt{\frac{3}{2}} \|\boldsymbol{s} - \boldsymbol{\alpha}\| - (\sigma_{y0} + R)$

其中：
*   $\|\cdot\|$ 表示 Frobenius 范数，即 $\|\mathbf{A}\| = \sqrt{\mathbf{A}:\mathbf{A}}$。
*   $\boldsymbol{s} - \boldsymbol{\alpha}$ 是有效[偏应力](@entry_id:163323)，其范数度量了当前应力状态点到[屈服面](@entry_id:175331)中心的距离。
*   $\sigma_{y0}$ 是材料的初始单轴[屈服应力](@entry_id:274513)。
*   $R$ 是等向[硬化](@entry_id:177483)变量，代表[屈服面](@entry_id:175331)半径相对于初始尺寸的增量。
*   $\sqrt{3/2}$ 是一个归一化因子，确保在[单轴拉伸](@entry_id:188287)情况下，当 $\boldsymbol{\alpha}=\mathbf{0}$ 且 $R=0$ 时，屈服条件简化为 $|\sigma_{11}| = \sigma_{y0}$。

屈服条件定义为 $f \le 0$。当 $f  0$ 时，材料处于弹性状态；当 $f = 0$ 时，材料处于塑性临界状态，可能发生塑性流动。

### [循环塑性](@entry_id:176411)现象的模拟

联合硬化模型的核心价值在于其能够捕捉纯粹等向或[随动硬化](@entry_id:172077)模型无法描述的关键[循环塑性](@entry_id:176411)现象。

#### 包申格效应

包申格效应是指金属材料在经历一定量的拉伸塑性变形后，其在后续压缩加载中的屈服强度会显著低于其初始屈服强度。纯等向硬化模型无法预测这一现象，因为它只会使[屈服面](@entry_id:175331)均匀扩张，导致拉伸和压缩[屈服强度](@entry_id:162154)同步增加。

联合硬化模型通过背应力 $\boldsymbol{\alpha}$ 的演化来自然地捕捉包申格效应。在[单轴拉伸](@entry_id:188287)过程中，$\varepsilon_p  0$，背应力 $\alpha$ 通常也随之增长为正值（假设采用线性 Prager 模型 $\alpha = C \varepsilon_p$，其中 $C  0$）。此时，[屈服面](@entry_id:175331)中心向[正应力](@entry_id:260622)方向移动。当卸载并反向加载至压缩状态时（$\sigma  0$），屈服条件 $| \sigma - \alpha | = \sigma_y$ 变为 $-(\sigma - \alpha) = \sigma_y$。反向屈服应力 $\sigma_{y, \mathrm{rev}}$ 因而变为：

$\sigma_{y, \mathrm{rev}} = \alpha - \sigma_y$

由于 $\alpha  0$ 且 $\sigma_y$ 是当前（可能因等向[硬化](@entry_id:177483)而增大了的）屈服半径，反向[屈服应力](@entry_id:274513)的[绝对值](@entry_id:147688) $|\sigma_{y, \mathrm{rev}}| = \sigma_y - \alpha$ 会小于 $\sigma_y$。这正是包申格效应的数学体现。

我们可以通过一个**包申格折减因子** $B$ 来量化此效应 [@problem_id:2930115]。在一个拉伸-压缩循环中，该因子定义为：

$B \equiv \frac{\sigma_{y0} - |\sigma_{y,\mathrm{rev}}|}{\sigma_{y0}}$

其中 $\sigma_{y, \mathrm{rev}}$ 是反向压缩[屈服应力](@entry_id:274513)。在一个具体的算例中，对于一个初始[屈服强度](@entry_id:162154)为 $\sigma_{y0} = 300 \, \mathrm{MPa}$ 的材料，在经历 $1.5\%$ 的[拉伸应变](@entry_id:183817)后，其反向压缩[屈服应力](@entry_id:274513)的大小可能降至约 $273.4 \, \mathrm{MPa}$，计算得到的 $B$ 值约为 $0.08879$。这个非零的 $B$ 值明确地量化了由[随动硬化](@entry_id:172077)引起的[屈服强度](@entry_id:162154)降低。

#### 棘轮效应

棘轮效应是指在[非对称应力](@entry_id:191550)控制循环（即平均应力不为零）下，材料会逐周期地累积塑性应变。这种现象在承受[振动](@entry_id:267781)和持续载荷的工程结构中尤为重要，可能导致构件因过度变形而失效。

要精确模拟棘轮效应，通常需要采用[非线性](@entry_id:637147)[随动硬化](@entry_id:172077)模型，例如 **Armstrong-Frederick 模型**。与线性模型不同，该模型引入了一个“动态回复”项，使得背应力的增长随着塑性变形的增加而逐渐饱和。当平均应力 $\sigma_m$ 导致[应力循环](@entry_id:200486)的中心偏离原点时，背应力的饱和行为使得屈服面无法“跟随”[应力循环](@entry_id:200486)的中心完全移动到位，从而在每个加载峰值附近都会产生微小的塑性应变增量，导致棘轮效应的发生。当背应力 $\boldsymbol{\alpha}$ 和等向[硬化](@entry_id:177483) $R$ 演化到一个稳定状态，使得整个[应力循环](@entry_id:200486)都落在弹性域内时，棘轮变形才会停止，材料达到“弹性安定 (elastic shakedown)”状态 [@problem_id:2930081]。

### 内变量演化定律

联合硬化模型的核心在于描述内变量 $\boldsymbol{\varepsilon}^p$、$\boldsymbol{\alpha}$ 和 $R$ 如何随加载历史演化。这些演化定律必须基于[塑性流动](@entry_id:201346)理论。

#### 关联流动法则

对于关联塑性，塑性[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}^p$ 的方向被假定为垂直于屈服面。这被称为**法向流动法则 (normality rule)**，源于[最大塑性耗散](@entry_id:184825)原理。数学上，它表示为：

$\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}$

其中 $\dot{\lambda} \ge 0$ 是塑性乘子，它是一个标量率，度量了塑性流动的量。只有当 $f=0$ 且 $\dot{f}=0$（[一致性条件](@entry_id:637057)）时，$\dot{\lambda}$ 才可能大于零。

对于前述的 von Mises 型[屈服函数](@entry_id:167970)，可以证明其对应力 $\boldsymbol{\sigma}$ 的梯度恰好是屈服面的[单位法向量](@entry_id:178851)（经过适当缩放）[@problem_id:2621894]。具体而言，可以推导出：

$\frac{\partial f}{\partial \boldsymbol{\sigma}} = \sqrt{\frac{3}{2}} \frac{\boldsymbol{s} - \boldsymbol{\alpha}}{\|\boldsymbol{s} - \boldsymbol{\alpha}\|}$

这个[方向向量](@entry_id:169562)通常被记为 $\mathbf{n}$。因此，[流动法则](@entry_id:177163)可以简洁地写为 $\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \mathbf{n}$。这个结果表明，塑性应变增量的方向由有效[偏应力](@entry_id:163323) $\boldsymbol{s} - \boldsymbol{\alpha}$ 决定。

#### 等向[硬化](@entry_id:177483)演化律

等向[硬化](@entry_id:177483)变量 $R$ 的演化通常与累积塑性应变量的大小相关。累积等效塑性[应变率](@entry_id:154778)定义为 $\dot{\bar{\varepsilon}}^p = \sqrt{\frac{2}{3}} \|\dot{\boldsymbol{\varepsilon}}^p\|$。对于关联 $J_2$ 塑性，可以证明 $\dot{\bar{\varepsilon}}^p = \dot{\lambda}$。因此，等向[硬化](@entry_id:177483)演化律的一般形式为 $\dot{R} = h(\dots) \dot{\bar{\varepsilon}}^p$。常见的模型有 [@problem_id:3549566]：

1.  **线性硬化 (Linear Hardening)**: 这是最简单的模型，
    $\dot{R} = H \dot{\bar{\varepsilon}}^p$
    其中 $H$ 是一个常数硬化模量。这意味着屈服面半径随塑性变形线性增长。

2.  **饱和硬化 (Saturating Hardening)**: 为了更真实地模拟[材料硬化](@entry_id:175896)能力逐渐减弱的现象，可以采用[非线性模型](@entry_id:276864)，如 Voce 硬化律：
    $\dot{R} = b (Q - R) \dot{\bar{\varepsilon}}^p$
    其中 $Q$ 是饱和硬化值，$b$是控制饱和速率的参数。当塑性应变累积时，$R$ 会渐近地趋向于 $Q$。

需要注意的是，基于静水压力不敏感的 $J_2$ 塑性理论，[塑性流动](@entry_id:201346)是保体积的，即 $\mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p) = 0$。因此，任何依赖于塑性体积变化的[硬化](@entry_id:177483)模型（例如 $\dot{R} = K \, \mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p)$）对于致密金属的 $J_2$ 塑性模型是不适用的 [@problem_id:3549566]。

#### [随动硬化](@entry_id:172077)演化律

背应力 $\boldsymbol{\alpha}$ 的演化决定了屈服面的平移。

1.  **线性 Prager 模型**:
    $\dot{\boldsymbol{\alpha}} = c \dot{\boldsymbol{\varepsilon}}^p$
    其中 $c$ 是[随动硬化](@entry_id:172077)模量。这个[线性关系](@entry_id:267880)意味着[屈服面](@entry_id:175331)中心的移动量与塑性应变成正比。虽然简单，但它无法描述背应力饱和，因此在模拟棘轮效应等方面存在局限性。

2.  **Armstrong-Frederick 模型**:
    $\dot{\boldsymbol{\alpha}} = c \dot{\boldsymbol{\varepsilon}}^p - \gamma \boldsymbol{\alpha} \dot{\bar{\varepsilon}}^p$
    这是[非线性](@entry_id:637147)[随动硬化](@entry_id:172077)模型的典范。等式右边第一项是线性 Prager 项，驱动[背应力](@entry_id:198105)随塑性应变演化。第二项是“动态回复”项，它使[背应力](@entry_id:198105)的增长率随着背应力自身的增大而减小，从而导致 $\boldsymbol{\alpha}$ 的饱和。对于单向拉伸，该方程的积分形式为 [@problem_id:3549552]：
    $\alpha(p) = \frac{c}{\gamma}(1 - \exp(-\gamma p))$
    其中 $p$ 是累积塑性应变。这表明背应力 $\alpha$ 将饱和于值 $c/\gamma$。

### 计算实现：[返回映射算法](@entry_id:168456)

在有限元等[数值模拟](@entry_id:137087)中，需要在每个时间（或载荷）增量步[内积](@entry_id:158127)分上述[本构方程](@entry_id:138559)。**[返回映射算法](@entry_id:168456) (Return Mapping Algorithm)** 是此任务的标准方法，它包含一个“弹性预测”和一个“塑性修正”步骤。

#### 1. 弹性预测

首先，假设在时间步 $t_n$到 $t_{n+1}$ 之间，整个应变增量 $\Delta\boldsymbol{\varepsilon}$ 完全是弹性的。由此计算出一个“试探”应力状态：

$\boldsymbol{\sigma}^{\mathrm{tr}} = \mathbb{C} : (\boldsymbol{\varepsilon}^e_n + \Delta\boldsymbol{\varepsilon}) = \boldsymbol{\sigma}_n + \mathbb{C} : \Delta\boldsymbol{\varepsilon}$

或者在偏[应力空间](@entry_id:199156)中：

$\boldsymbol{s}^{\mathrm{tr}} = \boldsymbol{s}_n + 2\mu \, \mathrm{dev}(\Delta\boldsymbol{\varepsilon})$

在这一步，所有塑性内变量都保持在 $t_n$ 时刻的值：$\boldsymbol{\varepsilon}^p_{n+1} = \boldsymbol{\varepsilon}^p_n$, $\boldsymbol{\alpha}_{n+1} = \boldsymbol{\alpha}_n$, $R_{n+1} = R_n$。

#### 2. 屈服检查

接下来，用试探状态的变量来评估[屈服函数](@entry_id:167970)：

$f^{\mathrm{tr}} = \|\boldsymbol{s}^{\mathrm{tr}} - \boldsymbol{\alpha}_n\| - \sqrt{\frac{2}{3}}(\sigma_{y0} + R_n)$

如果 $f^{\mathrm{tr}} \le 0$，说明弹性假设成立，该增量步确实是弹性的。试探状态就是最终状态。如果 $f^{\mathrm{tr}}  0$，说明材料发生了塑性变形，弹性假设错误，必须进行塑性修正。

#### 3. 塑性修正

当 $f^{\mathrm{tr}}  0$ 时，真实的应力点 $\boldsymbol{s}_{n+1}$ 必须被“[拉回](@entry_id:160816)”到演化后的[屈服面](@entry_id:175331)上。这个过程基于[后向欧拉法](@entry_id:139674)对[演化方程](@entry_id:268137)进行离散化。对于线性的 Prager 和线性等向硬化模型，可以推导出塑性乘子增量 $\Delta\lambda$ 的一个闭式解 [@problem_id:3549551]。

更新后的[状态变量](@entry_id:138790)为：
*   $\boldsymbol{s}_{n+1} = \boldsymbol{s}^{\mathrm{tr}} - 2\mu \Delta\boldsymbol{\varepsilon}^p = \boldsymbol{s}^{\mathrm{tr}} - 2\mu \Delta\lambda \mathbf{n}_{n+1}$
*   $\boldsymbol{\alpha}_{n+1} = \boldsymbol{\alpha}_n + c \Delta\boldsymbol{\varepsilon}^p = \boldsymbol{\alpha}_n + c \Delta\lambda \mathbf{n}_{n+1}$
*   $R_{n+1} = R_n + H \Delta\lambda$ （注意：这里的 $R$ 是基于 $\dot{R} = H \dot{\lambda}$，在某些定义下需要[转换因子](@entry_id:142644)）

关键在于，流动方向 $\mathbf{n}_{n+1}$ 被证明与试探方向相同，即 $\mathbf{n}_{n+1} = (\boldsymbol{s}^{\mathrm{tr}} - \boldsymbol{\alpha}_n) / \|\boldsymbol{s}^{\mathrm{tr}} - \boldsymbol{\alpha}_n\|$。利用最终状态必须满足屈服条件 $f_{n+1}=0$ 这一事实，可以求解 $\Delta\lambda$。

对于问题 [@problem_id:3549551] 中定义的模型，可推导出：

$\Delta\lambda = \frac{\|\boldsymbol{s}^{\mathrm{tr}} - \boldsymbol{\alpha}_n\| - \sqrt{\frac{2}{3}}(\sigma_{y0} + R_n)}{2\mu + c + \sqrt{\frac{2}{3}}H}$

这个公式直观地展示了[塑性流动](@entry_id:201346)的量（由 $\Delta\lambda$ 度量）：
*   分子 $f^{\mathrm{tr}}$ 代表了塑性流动的“驱动力”，即试探应力超出屈服面的程度。
*   分母代表了抵抗[塑性流动](@entry_id:201346)的“总模量”，由弹性抗力（$2\mu$）、[随动硬化](@entry_id:172077)抗力（$c$）和等向[硬化](@entry_id:177483)抗力（$\sqrt{2/3}H$）三部分组成。

在一个一维算例中 [@problem_id:3549582]，对于初始状态为零的材料施加 $0.003$ 的[拉伸应变](@entry_id:183817)，其试探应力远超初始屈服强度。利用上述原理的一维形式 $\Delta\lambda = f^{\mathrm{trial}} / (E+C+H)$，可以精确计算出塑性应变增量 $\Delta\varepsilon^p \approx 0.00166$，并最终确定终点应力为 $\sigma_{n+1} \approx 268.2 \, \mathrm{MPa}$，背应力为 $\alpha_{n+1} \approx 16.6 \, \mathrm{MPa}$。

对于非[线性硬化模型](@entry_id:180941)（如 Armstrong-Frederick），由于演化方程与状态变量耦合，通常无法得到 $\Delta\lambda$ 的[闭式](@entry_id:271343)解，需要采用[牛顿-拉弗森](@entry_id:177436)等迭代方法求解一个[非线性](@entry_id:637147)标量方程 [@problem_id:3549552]。

### [热力学](@entry_id:141121)基础

塑性[本构模型](@entry_id:174726)并非任意构建，它们必须遵循[热力学](@entry_id:141121)基本定律，以确保物理上的合理性。对于等温小应变过程，这主要通过亥姆霍兹自由能 (Helmholtz free energy) 和克劳修斯-杜亨不等式 (Clausius-Duhem inequality) 来保证。

[亥姆霍兹自由能](@entry_id:136442) $\psi$ 代表储存在材料中的能量。对于[弹塑性](@entry_id:193198)材料，它不仅是弹性应变 $\boldsymbol{\varepsilon}^e$ 的函数，也是内部[状态变量](@entry_id:138790)（如 $\boldsymbol{\alpha}$ 和 $r$）的函数。一个典型的形式为 [@problem_id:2711768]：

$\psi(\boldsymbol{\varepsilon}^{e}, \boldsymbol{\alpha}, r) = \frac{1}{2} \boldsymbol{\varepsilon}^{e} : \mathbb{C} : \boldsymbol{\varepsilon}^{e} + \frac{1}{2C_k} \boldsymbol{\alpha}:\boldsymbol{\alpha} + \frac{1}{2}H r^2$

这里，后两项分别代表了与[位错](@entry_id:157482)结构（对应背应力）和微观均匀硬化（对应等向硬化）相关的储存能。

克劳修斯-杜亨不等式要求在任何过程中，力学耗散 $\mathcal{D}$ 必须是非负的。耗散是在塑性变形中转化为热量的能量，其表达式为：

$\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p - \mathbf{A} : \dot{\boldsymbol{\alpha}} - Q \dot{r} \ge 0$

其中 $\mathbf{A} = \partial\psi/\partial\boldsymbol{\alpha}$ 和 $Q = \partial\psi/\partial r$ 是与内变量共轭的[热力学力](@entry_id:161907)。

为了保证该不等式对于任何可能的塑性过程都成立，必须对本构模型中的参数施加严格的限制 [@problem_id:2711768]：
1.  **[热力学稳定性](@entry_id:142877)**: [自由能函数](@entry_id:749582) $\psi$ 必须是[凸函数](@entry_id:143075)且有下界。这意味着储存能的二次项系数必须为正，即[硬化](@entry_id:177483)模量 $C_k  0$ 且 $H \ge 0$。负的硬化模量将导致材料在能量上不稳定。
2.  **耗散一致性**: 为了确保耗散非负，唯象的动力学演化法则（如 $\dot{\boldsymbol{\alpha}} = c \dot{\boldsymbol{\varepsilon}}^p$）必须与基于能量的定义（$\mathbf{A} = \boldsymbol{\alpha}/C_k$）相匹配。对于线性 Prager 模型，这要求 $c = C_k$。同样，[屈服函数](@entry_id:167970)中的[硬化](@entry_id:177483)项 $R(r)$ 必须与[热力学力](@entry_id:161907) $Q=Hr$ 一致，即 $R(r) = Hr$。

在满足这些条件后，可以证明力学耗散简化为 $\mathcal{D} = \dot{\lambda} \sqrt{2/3} \sigma_{y0}$，由于 $\dot{\lambda} \ge 0$ 且 $\sigma_{y0}  0$，耗散非负性得到保证。这套[热力学](@entry_id:141121)框架为构建物理上自洽的塑性模型提供了严谨的理论指导。