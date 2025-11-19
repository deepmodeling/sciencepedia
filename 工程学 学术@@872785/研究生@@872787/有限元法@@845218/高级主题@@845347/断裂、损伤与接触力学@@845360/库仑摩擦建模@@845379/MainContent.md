## 引言
摩擦，作为自然界中最普遍而又最复杂的物理现象之一，支配着从宏观[结构稳定性](@entry_id:147935)到微观原子运动的无数过程。在工程与[科学计算](@entry_id:143987)领域，准确地模拟摩擦行为是预测结构响应、优化设计和理解物理系统动态的关键。在众多摩擦模型中，[库仑摩擦模型](@entry_id:747944)以其简洁的形式和广泛的适用性，成为了[计算接触力学](@entry_id:168113)的基石。然而，其数学上的非光滑和非关联特性给数值实现带来了独特的挑战，这构成了理论与实践之间的一道鸿沟。本文旨在系统地跨越这道鸿沟，为读者提供关于[库仑摩擦模型](@entry_id:747944)的全面理解。

为实现这一目标，本文将分为三个核心章节。首先，在**“原理与机制”**一章中，我们将深入剖析[库仑摩擦](@entry_id:169196)的力学基础，从经典的[摩擦锥](@entry_id:171476)概念到其与塑性理论的深刻类比，并详细阐述在有限元框架下实现它的核心数值算法，如[返回映射](@entry_id:754324)法，以及这些算法对计算效率和收敛性的影响。接下来，**“应用与跨学科连接”**一章将展示该模型如何在岩土工程、[材料科学](@entry_id:152226)、机器人学和生物力学等不同领域中发挥作用，揭示了这一经典理论在解决前沿问题时的强大生命力与必要的适应性。最后，**“动手实践”**部分将理论付诸行动，通过一系列精心设计的编程练习，引导读者亲自实现和验证模型的核心特性，从而将抽象的理论知识转化为扎实的计算技能。

## 原理与机制

本章旨在深入阐述[库仑摩擦模型](@entry_id:747944)的力学原理与数值实现机制。我们将从接触点处的局部本构关系出发，构建摩擦定律的数学框架，进而探讨其在有限元方法中的运动学描述、数值算法实现，以及这些实现所带来的深刻[计算力学](@entry_id:174464)影响。

### [库仑摩擦](@entry_id:169196)的基本表述

在接触界面上任意一点，其力学行为可由法向和切向两个分量[解耦](@entry_id:637294)描述。法向描述物体间不可穿透的约束，而切向则描述[摩擦阻力](@entry_id:270342)。

#### 法向接触定律

设想两个物体可能发生接触。在一个潜在接触点，我们定义**法向间隙** $g_N$ 为两表面间沿公法线方向的距离，通常规定 $g_N \ge 0$ 表示分离或恰好接触。相应的，**法向接触应力** $p$ （或称接触压力）为沿[法线](@entry_id:167651)方向的压应力，规定 $p \ge 0$ 表示压缩。

无粘附的[单边接触](@entry_id:756326)行为遵循三个基本条件，合称为 **Signorini-Fichera 条件**：
1.  **不可穿透条件**: $g_N \ge 0$。这表明物体不能相互嵌入。
2.  **非拉伸条件**: $p \ge 0$。这表明接触力只能是压力，不能是拉力。
3.  **[互补条件](@entry_id:747558)**: $p \cdot g_N = 0$。该条件是核心，它表明：如果存在接触压力（$p > 0$），则两表面必须紧密接触（$g_N = 0$）；反之，如果两表面分离（$g_N > 0$），则它们之间不能有接触力（$p = 0$）。

这组条件精确地描述了理想刚性接触的法向行为。

#### 切向摩擦定律与[摩擦锥](@entry_id:171476)

切向行为由经典的[库仑摩擦定律](@entry_id:747943)描述。该定律指出，切向摩擦应力 $\boldsymbol{t}_\mathrm{T}$ 的大小受法向压力 $p$ 的制约。对于一个给定的[静摩擦系数](@entry_id:163255) $\mu$，所有物理上允许的接触应力状态 $(\boldsymbol{t}_\mathrm{T}, p)$ 必须满足：

$$
\|\boldsymbol{t}_\mathrm{T}\| \le \mu p
$$

这里，$\|\cdot\|$ 表示欧几里得范数。结合法向压力的非负性 $p \ge 0$，这个不等式在应力空间 $(\boldsymbol{t}_\mathrm{T}, p)$ 中定义了一个几何区域。若我们将切向[应力分解](@entry_id:272862)为 $\boldsymbol{t}_\mathrm{T} = (t_x, t_y)$，这个区域在三维空间 $(t_x, t_y, p)$ 中的表述为 $\sqrt{t_x^2 + t_y^2} \le \mu p$ 且 $p \ge 0$。这正是一个以原点为顶点、以 $p$ 轴为中心轴的圆锥的上半部分。这个几何体被称为 **[摩擦锥](@entry_id:171476) (friction cone)**。

[摩擦锥](@entry_id:171476)的几何形状直观地展示了所有可能的应力状态。锥的半角 $\alpha$，即锥的[母线](@entry_id:172692)与中心轴（$p$ 轴）的夹角，完全由[摩擦系数](@entry_id:150354) $\mu$ 决定。通过简单的三角关系可以推得：

$$
\tan(\alpha) = \frac{\|\boldsymbol{t}_\mathrm{T}\|}{p} = \mu \implies \alpha = \arctan(\mu)
$$

因此，更大的摩擦系数对应于更宽的[摩擦锥](@entry_id:171476)，意味着在相同的法向压力下，界面可以承受更大的切向力。

为了更方便地描述摩擦状态，我们引入一个 **[屈服函数](@entry_id:167970) (yield function)** $\phi(\boldsymbol{t}_\mathrm{T}, p)$：

$$
\phi(\boldsymbol{t}_\mathrm{T}, p) = \|\boldsymbol{t}_\mathrm{T}\| - \mu p
$$

[屈服函数](@entry_id:167970)的值将接触点的切向状态划分为两种截然不同的类型：

1.  **粘着状态 (Stick State)**: 当 $\phi  0$ 时，切向应力严格处于[摩擦锥](@entry_id:171476)内部。在这种状态下，界面没有相对滑动。任何施加的切向力只要不足以使应力状态达到锥的边界，都会被[静摩擦力](@entry_id:163518)完全平衡，相对切向速度 $\boldsymbol{v}_\mathrm{T}$ 为零。

2.  **滑移状态 (Slip State)**: 当 $\phi = 0$ 时，切向应力的大小达到了极限值，即 $\|\boldsymbol{t}_\mathrm{T}\| = \mu p$，应力状态位于[摩擦锥](@entry_id:171476)的表面。此时，界面发生相对滑动（$\boldsymbol{v}_\mathrm{T} \neq \boldsymbol{0}$）。[库仑定律](@entry_id:139360)进一步规定，[滑动摩擦](@entry_id:167677)力的方向总是与相对运动方向相反，以最大程度地耗散能量。数学上，这表示为：

    $$
    \boldsymbol{t}_\mathrm{T} = -\mu p \frac{\boldsymbol{v}_\mathrm{T}}{\|\boldsymbol{v}_\mathrm{T}\|}
    $$

#### 基于最大耗散原理的表述

上述区分粘着和滑移的规则可以从一个更基本的物理原理——**最大耗散原理 (principle of maximum dissipation)**——中导出。该原理指出，对于给定的相对滑移速率 $\boldsymbol{v}_\mathrm{T}$，界面上实际产生的摩擦应力 $\boldsymbol{t}_\mathrm{T}$ 将是[摩擦锥](@entry_id:171476)内所有可能应力中，使[能量耗散](@entry_id:147406)率 $\mathcal{D} = -\boldsymbol{t}_\mathrm{T} \cdot \boldsymbol{v}_\mathrm{T}$ 达到最大的那一个。

这个原理可以通过[变分不等式](@entry_id:172788)或更为现代的[凸分析](@entry_id:273238)工具——**[次微分](@entry_id:175641) (subdifferential)**——来精确表述。利用[次微分](@entry_id:175641)，整个[库仑摩擦定律](@entry_id:747943)（包括粘着和滑移）可以被紧凑地写作一个包含关系：

$$
\boldsymbol{t}_\mathrm{T} \in -\mu p \, \partial \|\boldsymbol{v}_\mathrm{T}\|
$$

这里, $\partial \|\boldsymbol{v}_\mathrm{T}\|$ 是范数函数 $\|\cdot\|$ 在点 $\boldsymbol{v}_\mathrm{T}$ 处的[次微分](@entry_id:175641)。其含义是：
-   如果 $\boldsymbol{v}_\mathrm{T} = \boldsymbol{0}$ （粘着），[次微分](@entry_id:175641)是单位球，即 $\{\boldsymbol{q} \mid \|\boldsymbol{q}\| \le 1\}$。因此，$\|\boldsymbol{t}_\mathrm{T}\| \le \mu p$。
-   如果 $\boldsymbol{v}_\mathrm{T} \neq \boldsymbol{0}$ （滑移），[次微分](@entry_id:175641)是唯一的单位向量 $\frac{\boldsymbol{v}_\mathrm{T}}{\|\boldsymbol{v}_\mathrm{T}\|}$。因此，$\boldsymbol{t}_\mathrm{T} = -\mu p \frac{\boldsymbol{v}_\mathrm{T}}{\|\boldsymbol{v}_\mathrm{T}\|}$。

这种表述不仅在数学上更为严谨和优雅，而且为高级数值算法的设计提供了坚实的理论基础。[@problem_id:2550803]

### 接触与滑移的运动学

在有限元分析中，精确定义[接触运动学](@entry_id:165205)变量是至关重要的，尤其是在[大变形](@entry_id:167243)问题中。这些定义必须满足**客观性 (objectivity)** 原理，即在[刚体运动](@entry_id:193355)变换下保持形式不变。

通常，我们将接触对中的一个表面定义为**主表面 (master surface)**，另一个为**从表面 (slave surface)**。[接触运动学](@entry_id:165205)通常以从表面上的点（例如积分点或节点）为出发点进行描述。

对于从表面上的任意一点 $\boldsymbol{x}_\mathrm{s}$，我们首先在当前构型的主表面上找到其**[最近点投影](@entry_id:168047) (closest-point projection)** $\boldsymbol{x}_\mathrm{m}^\star$。这个投影点定义了该从属点对应的接触点对。[@problem_id:2550847]

基于这个投影，**法向间隙** $g_N$ 被定义为从属点 $\boldsymbol{x}_\mathrm{s}$ 与其投影点 $\boldsymbol{x}_\mathrm{m}^\star$ 之间的有向距离，方向沿主表面在投影点的[法线](@entry_id:167651) $\boldsymbol{n}$ 方向：

$$
g_N = (\boldsymbol{x}_\mathrm{s} - \boldsymbol{x}_\mathrm{m}^\star) \cdot \boldsymbol{n}
$$

重要的是，[法向量](@entry_id:264185) $\boldsymbol{n}$ 和相应的切平面必须根据主表面在**当前时刻的几何构型**计算，以确保整个[运动学](@entry_id:173318)描述的客观性。

与间隙不同，摩擦滑移是一个累积的、依赖于历史路径的过程。因此，我们不能定义一个绝对的“切向间隙”，而必须定义一个**切向滑移增量 (tangential slip increment)** $\Delta \boldsymbol{g}_\mathrm{T}$。在一个时间步 $[t_n, t_{n+1}]$ 内，滑移增量代表了从属点相对于其“接触伙伴”的切向[相对运动](@entry_id:169798)。其“接触伙伴”是在 $t_{n+1}$ 时刻确定的主面物质点，该点在 $t_n$ 时刻的位置为 $\boldsymbol{x}_\mathrm{m}^{n\star}$。滑移增量是总相对位移在当前时刻 $t_{n+1}$ [切平面](@entry_id:136914)上的投影：

$$
\Delta \boldsymbol{g}_\mathrm{T} = \boldsymbol{P}_\mathrm{T}^{n+1} \left[ (\boldsymbol{x}_\mathrm{s}^{n+1} - \boldsymbol{x}_\mathrm{m}^{n+1\star}) - (\boldsymbol{x}_\mathrm{s}^{n} - \boldsymbol{x}_\mathrm{m}^{n\star}) \right]
$$

其中 $\boldsymbol{P}_\mathrm{T}^{n+1} = \boldsymbol{I} - \boldsymbol{n}^{n+1} \otimes \boldsymbol{n}^{n+1}$ 是在 $t_{n+1}$ 时刻[切平面](@entry_id:136914)上的[投影算子](@entry_id:154142)。这种增量式的定义正确地捕捉了摩擦的[路径依赖性](@entry_id:186326)，并且在任意大转动和[大变形](@entry_id:167243)下都保持客观。[@problem_id:2550847]

### 塑性类比：屈服面与流动法则

[库仑摩擦模型](@entry_id:747944)与[材料塑性](@entry_id:186852)理论之间存在深刻的类比关系。这种类比不仅有助于理论理解，也使得能够将成熟的计算塑性方法应用于摩擦问题。

在这个类比中：
-   摩擦应力 $(\boldsymbol{t}_\mathrm{T}, p)$ 对应于塑性理论中的应力张量。
-   摩擦[屈服函数](@entry_id:167970) $\phi = \|\boldsymbol{t}_\mathrm{T}\| - \mu p$ 对应于材料的屈服面，它定义了弹性区域的边界。
-   相对滑移速率 $(\dot{\boldsymbol{u}}_\mathrm{T}, \dot{u}_n)$ 对应于塑性[应变率](@entry_id:154778)。

在塑性理论中，塑性[应变率](@entry_id:154778)的方向由**流动法则 (flow rule)** 决定，该法则通常与一个**塑性[势函数](@entry_id:176105) (plastic potential function)** $g$ 相关联。塑性流动方向被假设为垂直于塑性[势函数](@entry_id:176105)的[等值面](@entry_id:196027)，即 $\dot{\boldsymbol{\epsilon}}^p \propto \nabla g$。

如果塑性势函数 $g$ 与[屈服函数](@entry_id:167970) $\phi$ 相同（或成正比），则该[流动法则](@entry_id:177163)是**关联的 (associated)**。否则，它是**非关联的 (non-associated)**。

现在，让我们考察[库仑摩擦](@entry_id:169196)的[流动法则](@entry_id:177163)。如果我们假设一个关联[流动法则](@entry_id:177163)，即 $g = \phi = \|\boldsymbol{t}_\mathrm{T}\| - \mu p_n$（这里使用 $p_n$ 表示法向压力），则滑移速率的分量将正比于 $g$ 对相应应力的梯度：

$$
\dot{\boldsymbol{u}}_\mathrm{T}^p \propto \frac{\partial g}{\partial \boldsymbol{t}_\mathrm{T}} = \frac{\boldsymbol{t}_\mathrm{T}}{\|\boldsymbol{t}_\mathrm{T}\|}
$$

$$
\dot{u}_n^p \propto \frac{\partial g}{\partial p_n} = -\mu
$$

切向分量表明滑移方向与切向应力方向一致，这与物理直觉相符（因为[摩擦力](@entry_id:171772)方向与滑移方向相反）。然而，法向分量 $\dot{u}_n^p \propto -\mu$ 预测，只要发生切向滑移，就必然会伴随一个法向的[相对运动](@entry_id:169798)（$\dot{u}_n^p \neq 0$）。这种现象被称为**法向剪胀 (normal dilatancy)**。对于许多工程界面，如金属间的接触，这种剪切引起的法向分离或嵌入是不符合物理实际的。[@problem_id:2550787]

为了模拟无剪胀的物理行为（即 $\dot{u}_n^p = 0$），我们必须选择一个不依赖于法向压力 $p_n$ 的塑性势函数，以使其对 $p_n$ 的偏导数为零。一个标准的选择是：

$$
g(\boldsymbol{t}_\mathrm{T}) = \|\boldsymbol{t}_\mathrm{T}\|
$$

使用这个塑性势，我们得到 $\frac{\partial g}{\partial p_n} = 0$，从而确保了 $\dot{u}_n^p = 0$。由于此时 $g \neq \phi$，这意味着**经典的[库仑摩擦模型](@entry_id:747944)是一个非关联的塑性模型**。这一特性是理解摩擦问题计算复杂性的关键，因为它破坏了模型的变分结构。[@problem_id:2550787, @problem_id:2544060]

### 数值实现：[预测-校正算法](@entry_id:753695)

在有限元增量分析中，摩擦本构关系通常通过一种称为**弹性预测-塑性校正 (elastic predictor-plastic corrector)** 的算法来积分，该算法在计算塑性领域中也被称为**[返回映射](@entry_id:754324) (return mapping)** 算法。

我们将以广泛使用的**[罚函数法](@entry_id:636090) (penalty method)** 为例来说明这一过程。[罚函数法](@entry_id:636090)通过引入较大的刚度系数（罚金）来近似地强制执行约束。
-   对于法向接触，法向应力 $t_n$（压缩为负）与穿透深度 $-g_n$（当 $g_n  0$ 时）成正比：$t_n = -\epsilon_n [-g_n]_+$，其中 $\epsilon_n$ 是法向罚金，$[x]_+ = \max(x,0)$。
-   对于切向摩擦，我们采用增量式的[预测-校正方法](@entry_id:147382)。

在一个时间（或荷载）增量步内，算法包含以下核心步骤：

1.  **弹性预测 (Elastic Predictor)**: 假设该增量步完全处于粘着状态（即纯弹性响应）。基于上一时刻收敛的切向应力 $\boldsymbol{t}_\mathrm{T}^k$ 和当前增量步的切向相对位移增量 $\Delta \boldsymbol{g}_\mathrm{T}$，计算出一个**试探切向应力 (trial tangential traction)** $\boldsymbol{t}_\mathrm{T}^{\text{tr}}$：
    $$
    \boldsymbol{t}_\mathrm{T}^{\text{tr}} = \boldsymbol{t}_\mathrm{T}^{k} + \epsilon_t \Delta \boldsymbol{g}_\mathrm{T}
    $$
    其中 $\epsilon_t$ 是切向罚金刚度。

2.  **滑移判断 (Slip Check)**: 用试探应力来评估[屈服函数](@entry_id:167970)，判断是否发生滑移：
    $$
    \phi^{\text{tr}} = \|\boldsymbol{t}_\mathrm{T}^{\text{tr}}\| - \mu p
    $$
    其中 $p = -t_n$ 是由当前法向状态决定的接触压力。

3.  **状态更新与塑性校正 (State Update and Plastic Corrector)**:
    -   如果 $\phi^{\text{tr}} \le 0$，试探应力在容许域内或边界上。粘着假设成立，无需校正。更新后的切向应力即为试探应力：$\boldsymbol{t}_\mathrm{T}^{k+1} = \boldsymbol{t}_\mathrm{T}^{\text{tr}}$。塑性滑移增量为零。
    -   如果 $\phi^{\text{tr}}  0$，试探应力超出了[摩擦锥](@entry_id:171476)，粘着假设不成立，必须发生滑移。此时需要执行“[返回映射](@entry_id:754324)”，将试探应力“[拉回](@entry_id:160816)”到屈服面上。对于标准的[库仑摩擦](@entry_id:169196)，这是一个[径向返回](@entry_id:754007)过程：
        $$
        \boldsymbol{t}_\mathrm{T}^{k+1} = \mu p \frac{\boldsymbol{t}_\mathrm{T}^{\text{tr}}}{\|\boldsymbol{t}_\mathrm{T}^{\text{tr}}\|}
        $$
        这保证了更新后的应力大小恰好为摩擦极限，方向与试探应力一致。相应的，不可恢复的**塑性滑移增量**大小 $\Delta \gamma$ 可以计算为：
        $$
        \Delta \gamma = \frac{\phi^{\text{tr}}}{\epsilon_t} = \frac{\|\boldsymbol{t}_\mathrm{T}^{\text{tr}}\| - \mu p}{\epsilon_t}
        $$

为了具体说明该算法，考虑一个接触积分点的情形。假设我们通过形函数插值得到了该点的位移增量 $\Delta \boldsymbol{u}_{GP}$，已知[法向量](@entry_id:264185) $\boldsymbol{n}$、摩擦系数 $\mu$、法向压力 $p_n$ 和切向罚金 $\epsilon_t$。首先将 $\Delta \boldsymbol{u}_{GP}$ 分解为[法向和切向分量](@entry_id:166204) $\Delta u_n$ 和 $\Delta \boldsymbol{g}_\mathrm{T}$。然后，假定[初始应力](@entry_id:750652)为零，计算试探应力 $\boldsymbol{t}_\mathrm{T}^{\text{tr}} = \epsilon_t \Delta \boldsymbol{g}_\mathrm{T}$。接着，计算摩擦极限 $\tau_{\text{crit}} = \mu p_n$。若 $\|\boldsymbol{t}_\mathrm{T}^{\text{tr}}\|  \tau_{\text{crit}}$，则判定发生滑移。塑性滑移的大小即为 $\Delta \gamma = (\|\boldsymbol{t}_\mathrm{T}^{\text{tr}}\| - \tau_{\text{crit}}) / \epsilon_t$。例如，在一个具体的算例中，若计算得出 $\|\boldsymbol{t}_\mathrm{T}^{\text{tr}}\| \approx 0.8876 \text{ MPa}$，而摩擦极限 $\tau_{\text{crit}} = 0.6 \text{ MPa}$，且切向罚金 $\epsilon_t = 50 \text{ MPa/mm}$，则塑性滑移增量的大小为 $\Delta \gamma = (0.8876 - 0.6) / 50 \approx 0.005751 \text{ mm}$。[@problem_id:2547953, @problem_id:2586606]

### 计算影响与高级论题

将摩擦模型集成到有限元框架中会带来一系列复杂的计算问题，这些问题主要源于模型的非[光滑性](@entry_id:634843)和非关联性。

#### 算法切向刚度

在采用[隐式求解器](@entry_id:140315)（如 [Newton-Raphson](@entry_id:177436) 方法）求解[非线性有限元](@entry_id:173184)方程时，系统的切向[刚度矩阵](@entry_id:178659)至关重要。摩擦[本构关系](@entry_id:186508)的贡献体现在**算法切向刚度 (algorithmic tangent stiffness)** $\boldsymbol{C}_{tt} = \partial \boldsymbol{t}_\mathrm{T} / \partial \Delta \boldsymbol{g}_\mathrm{T}$ 上。对[返回映射算法](@entry_id:168456)进行精确线性化，可以得到不同状态下的切向刚度。

-   **粘着状态**: $\boldsymbol{t}_\mathrm{T} = \epsilon_t \Delta \boldsymbol{g}_\mathrm{T}$ (假设[初始应力](@entry_id:750652)为零)。其切向刚度为：
    $$
    \boldsymbol{C}_{tt}^{\text{stick}} = \epsilon_t \boldsymbol{I}
    $$
    其中 $\boldsymbol{I}$ 是二维单位张量。这是一个满秩（秩为2）、对角、正定的矩阵，表示在任意切向方向上都存在弹性抗力。

-   **滑移状态**: $\boldsymbol{t}_\mathrm{T} = \mu p \frac{\boldsymbol{s}^{\text{tr}}}{\|\boldsymbol{s}^{\text{tr}}\|}$，其中 $\boldsymbol{s}^{\text{tr}}$ 是试探应力。其一致性切向刚度可以推导为：
    $$
    \boldsymbol{C}_{tt}^{\text{slip}} = \frac{\mu p \epsilon_t}{\|\boldsymbol{s}^{\text{tr}}\|} (\boldsymbol{I} - \hat{\boldsymbol{s}} \otimes \hat{\boldsymbol{s}})
    $$
    其中 $\hat{\boldsymbol{s}}$ 是滑移方向的[单位向量](@entry_id:165907)。算子 $\boldsymbol{I} - \hat{\boldsymbol{s}} \otimes \hat{\boldsymbol{s}}$ 是一个向 $\hat{\boldsymbol{s}}$ 正交方向的[投影算子](@entry_id:154142)。这个矩阵是奇异的，其秩为1。它在滑移方向 $\hat{\boldsymbol{s}}$ 上的刚度为零，反映了在达到摩擦极限后，沿滑移方向不再有额外的承载能力。

从粘着到滑移的转变伴随着切向[刚度矩阵](@entry_id:178659)的**秩下降**（从2降到1），这是塑性力学中的一个普遍现象，对[非线性](@entry_id:637147)求解的收敛性有重要影响。[@problem_id:2550822]

#### 对称性、变分原理与收敛性

如前所述，标准[库仑摩擦模型](@entry_id:747944)是非关联的。这一特性破坏了问题潜在的变分结构。

-   对于**关联**塑性模型，其本构关系可以从一个增量势能函数中导出。这保证了全局有限元系统的**切向[刚度矩阵](@entry_id:178659)是对称的**。对称性使得可以采用高效的对称矩阵求解器。

-   对于**非关联**的[库仑摩擦模型](@entry_id:747944)，不存在这样的增量[势能](@entry_id:748988)。其算法切向[刚度矩阵](@entry_id:178659)在严格推导下通常是**非对称的**。这就要求使用更为昂贵且鲁棒性较差的[非对称矩阵](@entry_id:153254)求解器。[@problem_id:2544060]

此外，[库仑摩擦模型](@entry_id:747944)在[摩擦锥](@entry_id:171476)顶点（$\boldsymbol{t}_\mathrm{T} = \boldsymbol{0}$）处存在不可导点（非光滑性），这对应于粘着与滑移的转换点。标准的 [Newton-Raphson](@entry_id:177436) 方法依赖于梯度的存在和连续性，因此在这种非光滑点附近可能失去其二次收敛特性，甚至导致迭代失败。解决这一问题的策略包括对模型进行光滑化处理，或采用更为先进的**[半光滑牛顿法](@entry_id:754689) (semi-smooth Newton methods)**。[@problem_id:2544060]

#### 高级正则化与求解方法

为了克服罚函数法的一些缺点（如需要选择合适的罚金、可能导致[病态问题](@entry_id:137067)）以及标准库仑模型的理论难题，研究者发展了多种高级方法。

**[增广拉格朗日法](@entry_id:170637) (Augmented Lagrangian Method)** 是一种结合了[拉格朗日乘子法](@entry_id:176596)和[罚函数法](@entry_id:636090)优点的强大技术。它通过迭代更新[拉格朗日乘子](@entry_id:142696)（即接触应力）来精确满足约束，同时罚金项提高了算法的稳定性和收敛性。该方法在能量上是一致的，能够正确地计算出摩擦所做的功（即耗散的能量），例如，在一个滑移增量中，摩擦功近似为 $W_{\text{fric}} = -(\mu \lambda_n^m) \|\Delta \boldsymbol{g}_t\|$，其中 $\lambda_n^m$ 是增量步中平均的法向[接触力](@entry_id:165079)。[@problem_id:2586606, @problem_id:2550824]

为了改善标准库仑模型的数学性质，可以引入**正则化 (regularization)**。例如，考虑一个依赖于滑移量的正则化摩擦定律：
$$
\|\boldsymbol{t}_\mathrm{T}\| \le \mu p + \kappa \|\boldsymbol{g}_\mathrm{T}\|
$$
其中 $\kappa  0$ 是一个正则化参数。这种形式的正则化，当 $\kappa  0$ 时，可以证明其[本构关系](@entry_id:186508)是**强单调的 (strongly monotone)**。在数学上，强单调性可以保证离散静力学问题解的**唯一性**，这是一个在标准库仑模型中无法保证的良好性质。[@problem_id:2550789]

然而，这种正则化也必须谨慎使用，以避免引入新的非物理效应，如**[网格依赖性](@entry_id:198563) (mesh dependency)**。若罚金刚度 $\epsilon_t$ 按常规随网格尺寸 $h$ 变化（如 $\epsilon_t \propto 1/h$），而 $\kappa$ 保持不变，则发生滑移的临界位移 $g_* = \mu p / (\epsilon_t - \kappa)$ 将会随着[网格加密](@entry_id:168565)而趋于零。这显然不符合物理现实。为了恢复**网格客观性 (mesh objectivity)**，正则化参数 $\kappa$ 必须与网格尺寸耦合，例如，取 $\kappa(h) = \epsilon_t(h) - C$，其中 $C$ 是一个与网格无关的常数。通过这种方式，可以确保滑移的起始点对应于一个物理上确定的、不随网格变化的临界滑移值。[@problem_id:2550789]