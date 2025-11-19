## 引言
率无关塑性理论是固体力学，特别是计算岩[土力学](@entry_id:180264)领域的基石，它为描述材料在经受荷载后产生的不可恢复变形提供了核心的数学框架。当岩石、土壤或金属等材料的受力超过其[弹性极限](@entry_id:186242)时，它们会进入塑性状态，其行为不再仅仅是简单的应力-应变成正比。理解并量化这一过程对于确保从地基、边坡到机械部件等各类工程结构的安全性与稳定性至关重要。本文旨在系统性地解决如何构建一个既符合物理规律（如[热力学](@entry_id:141121)）又在数学上严谨且便于数值实现的理论，用以预测这类与加载速率无关的永久变形。

为实现这一目标，本文将引导读者完成一次从理论基础到前沿应用的深度探索。在“原理与机制”一章中，我们将剖析构成该理论骨架的核心假设，包括屈服准则、[流动法则](@entry_id:177163)与[硬化](@entry_id:177483)规律，并探讨其背后的[热力学](@entry_id:141121)与稳定性约束，最终将其推广至大变形框架。随后的“应用与[交叉](@entry_id:147634)学科联系”章节将理论与实践相结合，展示如何利用这些原理构建针对岩土材料的经典模型（如Mohr-Coulomb和[修正剑桥模型](@entry_id:752089)），并探讨其在孔隙介质力学、接触摩擦和[断裂力学](@entry_id:141480)等[交叉](@entry_id:147634)领域的延伸。最后，“动手实践”部分将通过具体的计算练习，巩固您对理论的理解，并初步接触将理论转化为可执行代码的核心算法。通过这一结构化的学习路径，您将建立起对率无关塑性理论全面而深刻的认识。

## 原理与机制

本章旨在系统阐述率无关塑性理论的核心原理与基本机制。在前一章介绍其背景和重要性的基础上，我们将深入探讨该理论的力学、[热力学](@entry_id:141121)和数学基础。我们将从塑性流动的基本假设出发，构建一个自洽的理论框架，并逐步引入适用于岩土材料的特定[本构关系](@entry_id:186508)，最终将理论推广至大变形领域。

### 塑性理论的核心假设

率无关塑性理论建立在三个核心假设之上：[屈服准则](@entry_id:193897)、[流动法则](@entry_id:177163)和硬化/软化法则。这三个支柱共同定义了材料从弹性到塑性行为的转变及其后续演化。

#### [屈服准则](@entry_id:193897)与弹性域

材料的力学响应可以被划分为弹性区和塑性区。**弹性域** (elastic domain) 是一个在[应力空间](@entry_id:199156)中的区域，当应力状态位于该区域内部时，材料的变形是完全可逆的。这个区域的边界被称为**屈服面** (yield surface)。

为了在数学上描述这一概念，我们引入一个**[屈服函数](@entry_id:167970)** (yield function)，记为 $f(\boldsymbol{\sigma}, \boldsymbol{\alpha})$，其中 $\boldsymbol{\sigma}$ 是柯西[应力张量](@entry_id:148973)，$\boldsymbol{\alpha}$ 代表一组描述材料内部状态的**内变量** (internal variables)，例如[硬化](@entry_id:177483)程度。根据定义，[屈服函数](@entry_id:167970)满足以下条件 [@problem_id:3554856]：

*   当 $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) < 0$ 时，应力状态位于弹性域内部，材料响应为纯弹性。
*   当 $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = 0$ 时，应力状态位于[屈服面](@entry_id:175331)上，塑性变形可能即将发生。
*   $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) > 0$ 的状态是**塑性不可容许** (plastically inadmissible) 的，即在率无关塑性理论框架内，材料的应力状态不能超越屈服面。

因此，在任意给定的内部状态 $\boldsymbol{\alpha}$ 下，弹性域 $\mathcal{K}$ 可以被严格定义为应力张量的集合 $\mathcal{K}(\boldsymbol{\alpha}) = \{ \boldsymbol{\sigma} \mid f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) \le 0 \}$。

#### [流动法则](@entry_id:177163)

当应力状态达到[屈服面](@entry_id:175331)并持续加载时，材料将产生不可逆的塑性变形。**[流动法则](@entry_id:177163)** (flow rule) 描述了塑性应变率 $\dot{\boldsymbol{\varepsilon}}^p$ 的方向。在标准的塑性理论中，这一方向由一个称为**塑性势函数** (plastic potential function) 的标量函数 $g(\boldsymbol{\sigma})$ 决定。该法则假设塑性[应变率](@entry_id:154778)向量垂直于塑性势函数的[等值面](@entry_id:196027)，这被称为**法向法则** (normality rule)。数学上，流动法则表示为 [@problem_id:3554916]：

$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$

其中，$\dot{\lambda} \ge 0$ 是一个非负的标量，称为**塑性乘子率** (plastic multiplier rate)。它的大小决定了塑性变形的速率，只有在塑性加载时才为正值。

根据塑性[势函数](@entry_id:176105) $g$ 与[屈服函数](@entry_id:167970) $f$ 之间的关系，流动法则可分为两种：
1.  **关联流动法则 (Associated Flow Rule):** 当塑性势函数与[屈服函数](@entry_id:167970)相同时，即 $g = f$。此时，塑性应变率的方向垂直于屈服面。
2.  **[非关联流动法则](@entry_id:752544) (Non-associated Flow Rule):** 当塑性势函数与[屈服函数](@entry_id:167970)不同时，即 $g \neq f$。此时，塑性[应变率](@entry_id:154778)的方向垂直于塑性势面，而非屈服面。

对于岩土材料，[非关联流动法则](@entry_id:752544)是至关重要的，我们将在后续章节详细探讨其物理动机。

#### 硬化/软化法则

**[硬化](@entry_id:177483)/软化法则** (hardening/softening law) 描述了屈服面如何随着塑性变形的累积而演化。这种演化是通过内变量 $\boldsymbol{\alpha}$ 的变化来体现的。如果屈服面在应力空间中扩大，材料抵抗进一步塑性变形的能力增强，这种现象称为**硬化** (hardening)。反之，如果屈服面收缩，则称为**软化** (softening)。

[硬化](@entry_id:177483)法则定义了内变量率 $\dot{\boldsymbol{\alpha}}$ 与[塑性流动](@entry_id:201346)之间的关系，通常形式为 $\dot{\boldsymbol{\alpha}} = \text{func}(\dot{\lambda}, \boldsymbol{\sigma}, \boldsymbol{\alpha})$。两种最基本的[硬化](@entry_id:177483)机制是 [@problem_id:3554912]：
*   **[各向同性硬化](@entry_id:164486) (Isotropic Hardening):** 屈服面在保持其形状和中心位置不变的情况下，均匀地扩大或缩小。这通常通过一个标量内变量（如累积塑性应变）来控制屈服面尺寸的变化。
*   **[运动硬化](@entry_id:172077) (Kinematic Hardening):** 屈服面在应力空间中发生平移，而其尺寸和形状保持不变。这种平移由一个称为**[背应力](@entry_id:198105)** (backstress) 的张量内变量 $\boldsymbol{X}$ 来描述，它对于模拟材料在[循环加载](@entry_id:181502)下的[包辛格效应](@entry_id:173790) (Bauschinger effect) 至关重要。

在更复杂的模型中，这两种机制可以结合使用，以更准确地描述材料的力学行为。

### [热力学](@entry_id:141121)与稳定性基础

塑性本构关系并非任意构造，它必须遵循[热力学](@entry_id:141121)基本定律，并保证材料响应的稳定性。

#### [热力学一致性](@entry_id:138886)与耗散

根据热力学第二定律，任何不[可逆过程](@entry_id:276625)都必须产生非负的[能量耗散](@entry_id:147406)。对于在恒温条件下的[弹塑性](@entry_id:193198)体，这可以通过**克劳修斯-杜亨不等式** (Clausius-Duhem inequality) 导出。在小应变框架下，假设[亥姆霍兹自由能](@entry_id:136442) $\psi$ 是弹性应变 $\boldsymbol{\varepsilon}^e$ 和内变量 $\boldsymbol{\alpha}$ 的函数，即 $\psi = \psi(\boldsymbol{\varepsilon}^e, \boldsymbol{\alpha})$，则单位体积的力学[耗散率](@entry_id:748577) $\mathcal{D}$ 必须满足 [@problem_id:3554865]：

$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p - \mathbf{A} \cdot \dot{\boldsymbol{\alpha}} \ge 0
$$

其中，$\mathbf{A} = \frac{\partial \psi}{\partial \boldsymbol{\alpha}}$ 是与内变量 $\boldsymbol{\alpha}$ 共轭的[热力学力](@entry_id:161907)。此不等式表明，塑性功（$\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p$）的一部分被耗散为热，另一部分作为“冻结”能量储存在材料的微观结构中（由硬化项 $\mathbf{A} \cdot \dot{\boldsymbol{\alpha}}$ 体现）。

率无关塑性的一个深刻数学特征是，其耗散势 $\mathcal{R}$ 是关于广义塑性率（$\dot{\boldsymbol{\gamma}} := (\dot{\boldsymbol{\varepsilon}}^p, \dot{\boldsymbol{\alpha}})$）的正一次齐次函数，即对于任意 $\lambda > 0$，有 $\mathcal{R}(\lambda\dot{\boldsymbol{\gamma}}) = \lambda\mathcal{R}(\dot{\boldsymbol{\gamma}})$。这一性质意味着，对应的[热力学力](@entry_id:161907)（应力等）仅取决于[塑性流动](@entry_id:201346)的“方向”，而与其“速率”大小无关，这正是“率无关”的本质 [@problem_id:3554865]。

#### Drucker 稳定性公设

除了[热力学约束](@entry_id:755911)，材料的稳定性也是一个基本要求。**[Drucker稳定性公设](@entry_id:200080)** (Drucker's stability postulate) 提供了一个更偏向力学视角的[稳定性判据](@entry_id:755304)。其原始形式要求，在一个塑性加载-卸载的[应力循环](@entry_id:200486)中，外力所做的净功必须是非负的。其增量形式（或称“在小范围内稳定”）可以表达为 [@problem_id:2899927]：

$$
\delta \boldsymbol{\sigma} : \delta \boldsymbol{\varepsilon}^p \ge 0
$$

其中 $\delta \boldsymbol{\sigma}$ 是一个从当前塑性状态出发的应力增量，$\delta \boldsymbol{\varepsilon}^p$ 是其引起的塑性应变增量。这个不等式的物理意义是，由应力增量在塑性应变增量上做的二阶功必须为非负。这意味着材料在[塑性流动](@entry_id:201346)过程中不会自发释放能量，从而保证了其稳定性。

[Drucker公设](@entry_id:180546)具有深远的意义。可以证明，对于服从该公设的材料，其屈服面必须是**凸** (convex) 的，并且流动法则是**关联**的 ($g=f$)。在现代塑性理论中，这一稳定性要求通常通过[凸分析](@entry_id:273238)的工具来形式化表达。将流动法则写为 $\dot{\boldsymbol{\varepsilon}}^p \in \partial I_{\mathcal{K}}(\boldsymbol{\sigma})$，其中 $I_{\mathcal{K}}$ 是弹性域 $\mathcal{K}$ 的[指示函数](@entry_id:186820)，$\partial I_{\mathcal{K}}$ 是其**[次微分](@entry_id:175641)** (subdifferential)。[Drucker公设](@entry_id:180546)等价于要求这个从应力到塑性[应变率](@entry_id:154778)的映射是一个**[单调算子](@entry_id:637459)** (monotone operator) [@problem_id:2899927]。

### 数学形式与本构法则

上述原理通过一组数学关系式被整合为一套完整的本构理论，其中最核心的是加载/卸载的判断条件。

#### 加载-卸载条件（KKT 条件）

率无关塑性的一个标志性特征是其“开关”行为：材料要么处于弹性状态，要么处于塑性状态。这一行为由一组被称为**[Karush-Kuhn-Tucker (KKT) 条件](@entry_id:176491)**的互补关系精确描述 [@problem_id:3554886]：

1.  **可容许性 (Admissibility):** $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) \le 0$
2.  **非负性 (Non-negativity):** $\dot{\lambda} \ge 0$
3.  **互补性 (Complementarity):** $\dot{\lambda} f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = 0$

[互补条件](@entry_id:747558)是核心。它表明：如果应力在弹性域内部 ($f < 0$)，则必须有 $\dot{\lambda} = 0$，即没有塑性流动；反之，如果发生塑性流动 ($\dot{\lambda} > 0$)，则应力必须位于[屈服面](@entry_id:175331)上 ($f=0$)。

#### 一致性条件

当塑性加载持续进行时（即 $\dot{\lambda} > 0$），应力状态必须始终保持在演化中的屈服面上。这意味着[屈服函数](@entry_id:167970)的时间变化率必须为零，即 $\dot{f} = 0$。这被称为**一致性条件** (consistency condition) [@problem_id:3554856, @problem_id:3554886]。将 $\dot{f}$ 用链式法则展开：

$$
\dot{f} = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \dot{\boldsymbol{\sigma}} + \frac{\partial f}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}} = 0
$$

这个方程是求解塑性乘子 $\dot{\lambda}$ 的关键。它将应力率 $\dot{\boldsymbol{\sigma}}$ 与内变量的演化联系起来，确保了在[塑性流动](@entry_id:201346)过程中，应力点不会“穿出”[屈服面](@entry_id:175331)。

综合来看，[KKT条件](@entry_id:185881)和[一致性条件](@entry_id:637057)共同构成了加载/卸载的判断逻辑：
*   若 $f < 0$，或 $f=0$ 且弹性试探表明 $\dot{f} < 0$（应力趋向弹性域内部），则为弹性加载或卸载，$\dot{\lambda}=0$。
*   若 $f=0$ 且弹性试探表明 $\dot{f} > 0$（应力试图穿出屈服面），则为塑性加载，此时必须有 $\dot{\lambda} > 0$，其大小通过满足[一致性条件](@entry_id:637057) $\dot{f}=0$ 来确定 [@problem_id:3554886]。

### 岩土材料的[本构模型](@entry_id:174726)

将上述通用框架应用于岩土材料，需要选择能够反映其特有力学行为的函数形式。

#### [应力不变量](@entry_id:170526)与各向同性

由于岩土材料（如土壤）通常在宏观上被视为各向同性，其力学响应应与[坐标系](@entry_id:156346)的选择无关。根据**客观性** (objectivity) 和**各向同性** (isotropy) 原理，任何描述材料行为的标量函数（如[屈服函数](@entry_id:167970)）都必须能表示为其张量参数（如[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$）的[主不变量](@entry_id:193522)的函数。

对于受压力影响显著的岩土材料，使用以下三个[应力不变量](@entry_id:170526)尤为方便 [@problem_id:3554910]：
1.  **平均应力 (Mean Stress) $p$:** $p = \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})$。它度量了[静水压力](@entry_id:275365)，与材料的体积变化密切相关。岩土的强度和刚度强烈依赖于 $p$，这种现象称为**压力敏感性** (pressure sensitivity)。
2.  **偏[应力[不变](@entry_id:170526)量](@entry_id:148850) (Deviatoric Stress Invariant) $q$:** $q = \sqrt{\frac{3}{2}\boldsymbol{s}:\boldsymbol{s}}$，其中 $\boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I}$ 是[偏应力张量](@entry_id:267642)。$q$ 度量了剪切应力的大小，是驱动材料形状改变的主要因素。
3.  **[Lode角](@entry_id:191590) (Lode Angle) $\theta$:** $\theta = \frac{1}{3}\arccos\left(\frac{3\sqrt{3}}{2}\frac{J_3}{J_2^{3/2}}\right)$，其中 $J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s}$ 和 $J_3 = \det(\boldsymbol{s})$ 是偏应力的第二和第三[不变量](@entry_id:148850)。[Lode角](@entry_id:191590)描述了在给定 $p$ 和 $q$ 的情况下，中间[主应力](@entry_id:176761) $\sigma_2$ 的相对大小，反映了应力状态在**$\pi$平面**（[偏应力](@entry_id:163323)平面）上的形状。

一个完备的岩土材料模型，其[屈服函数](@entry_id:167970)和塑性[势函数](@entry_id:176105)通常应表示为这三个[不变量](@entry_id:148850)的函数，即 $f(p,q,\theta)$ 和 $g(p,q,\theta)$。

#### 岩土材料的屈服面

*   **光滑[屈服面](@entry_id:175331):** 以**Drucker-Prager (DP) 模型**为代表，其[屈服函数](@entry_id:167970)通常写为 $f(p,q) = q - m p - k \le 0$。在[主应力空间](@entry_id:184388)中，它是一个圆锥面，在 $p-q$ 平面内是一条直线。DP模型结构简单，能够反映压力敏感性，但由于其屈服面对 $\theta$ 不敏感（在$\pi$平面上为圆形），无法区分三轴压缩和三轴拉伸下的不同强度 [@problem_id:3554856]。

*   **非光滑[屈服面](@entry_id:175331):** 以**Mohr-Coulomb (MC) 模型**为代表，是岩土工程中最经典的强度准则。其[屈服面](@entry_id:175331)在[主应力空间](@entry_id:184388)中是一个不规则的六棱锥，在$\pi$平面上是一个不等边六边形。这种非[光滑性](@entry_id:634843)源于其表达式，它通常是多个线性函数的最大值形式 [@problem_id:3554856]。在屈服面的棱和角点处，法向是不唯一的。这时，流动方向由[次微分](@entry_id:175641) $\partial f(\boldsymbol{\sigma})$ 给出的法向向量集合决定。根据[凸分析](@entry_id:273238)理论，$\partial f(\boldsymbol{\sigma})$ 是在光滑点梯度的极限的[凸包](@entry_id:262864)。因此，在非光滑点，[塑性流动法则](@entry_id:189597)推广为 $\dot{\boldsymbol{\varepsilon}}^p \in \dot{\lambda} \partial f(\boldsymbol{\sigma})$，允许流动方向在由所有激活屈服面法向构成的**法向锥** (normal cone) 内取值 [@problem_id:3554867]。

#### 流动法则与[剪胀性](@entry_id:201001)

实验表明，许多岩土材料（如密砂、超固结黏土）在剪切过程中会发生[体积膨胀](@entry_id:144241)，这种现象称为**剪胀** (dilatancy)。相反，松散的材料在剪切时则会体积压缩，称为**剪缩** (compaction)。为了描述这种塑性体积应变，[非关联流动法则](@entry_id:752544)变得必不可少 [@problem_id:3554916]。

在 $p-q$ 空间中，塑性[体积应变率](@entry_id:272471) $\dot{\varepsilon}_v^p$ 和塑性[剪应变率](@entry_id:189459) $\dot{\varepsilon}_s^p$ 的比值由塑性势函数 $g$ 的梯度决定。对于一个Drucker-Prager形式的塑性势 $g(p,q) = q - p\tan\psi$，其中 $\psi$ 被称为**[剪胀角](@entry_id:748435)** (dilatancy angle)，我们有：

$$
\frac{\dot{\varepsilon}_v^p}{\dot{\varepsilon}_s^p} \propto \frac{\partial g / \partial p}{\partial g / \partial q} = -\tan\psi
$$

*   $\psi > 0$ 意味着剪切伴随着[体积膨胀](@entry_id:144241)（剪胀）。
*   $\psi = 0$ 意味着塑性流动是等容的（剪切不改变体积）。
*   $\psi < 0$ 意味着剪切伴随着体积压缩（剪缩）。

大量实验数据表明，对于土壤，其[剪胀角](@entry_id:748435) $\psi$ 通常远小于其[内摩擦角](@entry_id:197521) $\phi$。如果采用关联[流动法则](@entry_id:177163)（即 $g=f$，$\psi=\phi$），模型将严重高估材料的[剪胀性](@entry_id:201001)。因此，采用[非关联流动法则](@entry_id:752544)（$g \neq f$，$\psi < \phi$）是真实模拟岩土行为的关键 [@problem_id:3554916]。

### 向[大变形理论](@entry_id:188422)的推广

以上讨论均基于小应变假设。然而，在许多岩土工程问题中，如滑坡、贯入和剪切带的形成，变形和转动都可能非常大，小应变理论不再适用。

#### [运动学分解](@entry_id:751020)

在小应变理论中，总应变被简单地**加法分解** (additive decomposition) 为弹性和塑性两部分：$\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p$。这个近似仅在应变和转动都极小的情况下才具有客观性 [@problem_id:3554877]。

在[大变形理论](@entry_id:188422)中，更严谨的运动学框架是基于变形梯度 $\boldsymbol{F}$ 的**[乘法分解](@entry_id:199514)** (multiplicative decomposition)：

$$
\boldsymbol{F} = \boldsymbol{F}^e \boldsymbol{F}^p
$$

这里，$\boldsymbol{F}$ 将初始构型映射到当前构型。该分解引入了一个概念性的、无应力的**[中间构型](@entry_id:193000)** (intermediate configuration)。$\boldsymbol{F}^p$ 代表从初始构型到[中间构型](@entry_id:193000)的不可逆塑性变形，而 $\boldsymbol{F}^e$ 代表从[中间构型](@entry_id:193000)到当前构型的可逆弹性变形。这种乘法结构能够正确地处理大转动，确保本构关系满足[材料客观性原理](@entry_id:177427) [@problem_id:3554877, @problem_id:3554878]。对于岩土材料，其塑性变形往往伴随着体积变化，因此必须允许 $\det(\boldsymbol{F}^p) \neq 1$ [@problem_id:3554877]。

#### 客观性与应力率

在大变形框架下，本构法则的构建必须确保其在任意叠加的刚体运动下保持形式不变（即客观性）。直接使用柯西应力 $\boldsymbol{\sigma}$ 的时间导数 $\dot{\boldsymbol{\sigma}}$ 会破坏客观性，因为它在[刚体转动](@entry_id:191086)下会产生虚假的应力。为解决此问题，有两种主要途径 [@problem_id:3554878]：

1.  **空间构型方法：** 在当前构型下建立[本构关系](@entry_id:186508)。此时，必须使用**[客观应力率](@entry_id:199282)** (objective stress rate)，如Jaumann率或[Green-Naghdi率](@entry_id:190839)。这些应力率通过从材料导数中减去由[刚体转动](@entry_id:191086)引起的部分，来保证其客观性。
2.  **[中间构型](@entry_id:193000)方法：** 在[中间构型](@entry_id:193000)上建立本构关系。这被认为是一种更物理的方法。通过定义一个在[中间构型](@entry_id:193000)上的应力量，如**[Mandel应力](@entry_id:191786)** $\boldsymbol{M} = \boldsymbol{C}^e \boldsymbol{S}$ (其中 $\boldsymbol{C}^e = (\boldsymbol{F}^e)^\mathrm{T} \boldsymbol{F}^e$, $\boldsymbol{S}$ 是[第二Piola-Kirchhoff应力](@entry_id:173163)），可以构建一个天然满足客观性的理论，因为 $\boldsymbol{M}$ 本身在叠加[刚体运动](@entry_id:193355)下是不变的。此时，[屈服函数](@entry_id:167970)和流动法则都用 $\boldsymbol{M}$ 来表达。

#### 塑性自旋的角色

在[乘法分解](@entry_id:199514)中，塑性[速度梯度](@entry_id:261686) $\boldsymbol{L}_p = \dot{\boldsymbol{F}}_p \boldsymbol{F}_p^{-1}$ 可以分解为对称的塑性[应变率](@entry_id:154778) $\boldsymbol{D}_p$ 和反对称的**塑性自旋** $\boldsymbol{W}_p$。$\boldsymbol{D}_p$ 由[流动法则](@entry_id:177163)确定且产生耗散，而 $\boldsymbol{W}_p$ 不产生耗散，其取值是一个本构假设，不受[热力学](@entry_id:141121)或流动法则的直接约束。塑性自旋描述了[中间构型](@entry_id:193000)的转动速率，它的选择会影响[材料各向异性](@entry_id:204117)（如[运动硬化](@entry_id:172077)中背应力张量）的演化。例如，一个常见的假设是 $\boldsymbol{W}_p=0$（等斜假设），但这并非唯一选择。不同的 $\boldsymbol{W}_p$ 本构假定不会破坏理论的客观性，但会影响对复杂加载路径下材料行为的预测 [@problem_id:3554878]。

总之，从基本假设到[热力学](@entry_id:141121)和稳定性约束，再到针对岩土材料的具体模型，并最终推广到[大变形](@entry_id:167243)框架，率无关塑性理论为模拟复杂岩土力学行为提供了强大而严谨的工具。