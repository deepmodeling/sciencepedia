## 引言
在工程与科学的众多领域中，从汽车碰撞到人体关节运动，物体间的相互作用无处不在。有限元模拟（FEM）为预测这些复杂系统的力学行为提供了强大的工具，而其核心挑战之一便是准确地建模[接触与摩擦](@entry_id:747779)。这些现象本质上是高度[非线性](@entry_id:637147)的，由不可穿透的单边约束和非光滑的摩擦定律所支配，这给数值求解带来了巨大的困难和独特的挑战。本文旨在系统性地剖析[有限元分析](@entry_id:138109)中[接触与摩擦](@entry_id:747779)建模的理论基础、[数值算法](@entry_id:752770)和前沿应用。

为了引导读者逐步深入这一复杂领域，本文组织为三个核心章节。
- 在“**原理与机制**”一章中，我们将奠定理论基石，从[接触运动学](@entry_id:165205)的基本定义（间隙与滑移）出发，详细阐述描述法向接触的赫兹-西尼奥里尼-莫罗条件，并系统比较实现这些约束的几种关键数值方法：[罚函数法](@entry_id:636090)、[拉格朗日乘子法](@entry_id:176596)和[Nitsche方法](@entry_id:175793)。此外，我们还将探讨经典的[库仑摩擦模型](@entry_id:747944)及其高效的数值实现算法——[返回映射](@entry_id:754324)法。
- 随后的“**应用与跨学科交叉**”一章将理论付诸实践，通过一系列生物力学领域的实例，展示这些模型如何被用于分析人工关节的设计、天然软骨的复杂双[相行为](@entry_id:199883)，以及软组织与医疗器械间的交互作用。本章将强调[接触力学](@entry_id:177379)如何与材料科学、摩擦学乃至[流体动力](@entry_id:750449)学等学科交叉，共同解决真实世界中的[多物理场](@entry_id:164478)问题。
- 最后，通过“**动手实践**”部分，读者将有机会通过具体的编程练习，将理论知识转化为实际的计算技能，从而加深对核心概念的理解。

通过这一结构化的学习路径，本文将为您提供一个关于有限元[接触与摩擦](@entry_id:747779)建模的全面而深入的视角，使您能够充满信心地应对学术研究和工程实践中的相关挑战。

## 原理与机制

本章深入探讨有限元模拟中[接触与摩擦](@entry_id:747779)建模的核心原理和数值机制。我们将从描述接触界面的基本运动学入手，系统地介绍处理法向不可穿透约束和切向摩擦行为的各[类数](@entry_id:156164)学及计算方法，并讨论在生物力学等特定应用领域中出现的挑战，如几何精度、[非匹配网格](@entry_id:168552)和材料的[近不可压缩性](@entry_id:752381)。

### [接触运动学](@entry_id:165205)：间隙与滑移的定义

在模拟两个或多个[可变形体](@entry_id:1123496)之间的相互作用时，首要任务是精确地描述它们在空间中的相对位置。这构成了[接触运动学](@entry_id:165205)的基础。在有限元方法中，通常采用**主-从面 (master-slave)**的概念来定义接触对。其中一个表面被指定为**从面 (slave surface)**，其上的点（通常是节点）将被检测是否与另一个表面，即**主面 (master surface)**，发生接触。

最常用和最稳健的[接触运动学](@entry_id:165205)描述是在**当前构型 (spatial configuration)**下进行的。考虑从面上的任意一点 $\boldsymbol{x}_s$ 和由参数 $\boldsymbol{\xi} = (\xi_1, \xi_2)$ [参数化](@entry_id:265163)的主面 $\boldsymbol{x}_m(\boldsymbol{\xi})$。为了量化它们之间的关系，我们采用**[最近点投影](@entry_id:168047) (closest-point projection)**的方法。该方法旨在寻找主面上距离从点 $\boldsymbol{x}_s$ 最近的一点 $\boldsymbol{x}_m(\boldsymbol{\xi}^\ast)$。从数学上讲，这是通过最小化距离的平方 $d^2(\boldsymbol{\xi}) = \|\boldsymbol{x}_s - \boldsymbol{x}_m(\boldsymbol{\xi})\|^2$ 来实现的。

该最小化问题的必要条件是，连接点 $\boldsymbol{x}_s$ 与其投影点 $\boldsymbol{x}_m(\boldsymbol{\xi}^\ast)$ 的向量必须与主面在投影点的[切平面](@entry_id:136914)正交。若主面的协变切向量为 $\boldsymbol{a}_\alpha(\boldsymbol{\xi}) = \partial \boldsymbol{x}_m / \partial \xi_\alpha$，则该**正交条件**可表示为 ：
$$
(\boldsymbol{x}_s - \boldsymbol{x}_m(\boldsymbol{\xi}^\ast)) \cdot \boldsymbol{a}_\alpha(\boldsymbol{\xi}^\ast) = 0 \quad \text{for } \alpha \in \{1,2\}
$$
这意味着，**间隙向量 (gap vector)** $\boldsymbol{g} = \boldsymbol{x}_s - \boldsymbol{x}_m(\boldsymbol{\xi}^\ast)$ 平行于主面在投影点的[法向量](@entry_id:264185) $\boldsymbol{n}_m(\boldsymbol{\xi}^\ast)$。

一旦找到投影点 $\boldsymbol{\xi}^\ast$，我们便可以定义两个关键的运动学变量：

1.  **法向间隙 (Normal Gap, $g_n$)**: 这是从点 $\boldsymbol{x}_s$ 到主面的有符号距离，沿着主面[法线](@entry_id:167651)方向测量。通常约定，当体分离时 $g_n > 0$，当它们恰好接触时 $g_n = 0$，而当它们相互穿透时 $g_n < 0$。其计算公式为间隙向量在主[面法向量](@entry_id:749211)上的投影：
    $$
    g_n = \boldsymbol{g} \cdot \boldsymbol{n}_m(\boldsymbol{\xi}^\ast) = (\boldsymbol{x}_s - \boldsymbol{x}_m(\boldsymbol{\xi}^\ast)) \cdot \boldsymbol{n}_m(\boldsymbol{\xi}^\ast)
    $$
    $g_n$ 的符号对于区分分离与穿透至关重要，这是所有[接触算法](@entry_id:177014)的基础。

2.  **切向滑移向量 (Tangential Slip Vector, $\boldsymbol{g}_t$)**: 该向量代表了从点 $\boldsymbol{x}_s$ 在主面[切平面](@entry_id:136914)内的相对位置。它是总间隙向量 $\boldsymbol{g}$ 减去其法向分量后得到的向量。利用单位张量 $\boldsymbol{I}$ 和[并矢积](@entry_id:748716) $\otimes$，它可以表示为 ：
    $$
    \boldsymbol{g}_t = \boldsymbol{g} - (\boldsymbol{g} \cdot \boldsymbol{n}_m(\boldsymbol{\xi}^\ast)) \boldsymbol{n}_m(\boldsymbol{\xi}^\ast) = (\boldsymbol{I} - \boldsymbol{n}_m(\boldsymbol{\xi}^\ast) \otimes \boldsymbol{n}_m(\boldsymbol{\xi}^\ast)) \boldsymbol{g}
    $$
    在理想的[最近点投影](@entry_id:168047)下，$\boldsymbol{g}_t$ 应为零。然而，在迭代求解过程中以及在描述摩擦现象时，$\boldsymbol{g}_t$ 的变化率（即切向滑移速率）是定义摩擦力和能量耗散的核心。

尽管在空间构型中定义[接触运动学](@entry_id:165205)更为直观和常用，但在某些[大变形理论](@entry_id:188422)框架下，也可以在**参考构型 (material configuration)** 中建立类似的几何关系。这种方法通过在未变形的物体几何上进行[最近点投影](@entry_id:168047)来定义物质间隙和物质滑移，其原理与空间描述完全类似 。

### 单边约束：法向接触的公式化

接触问题的核心物理特性是其**单边性 (unilateral)**：物体表面可以相互推挤（产生压力），但不能相互拉拽（除非存在粘附）。此外，两个物体不能占据同一空间，即不可相互穿透。这些物理原理可以通过一组被称为**赫兹-西尼奥里尼-莫罗 (Hertz-Signorini-Moreau)** 条件的数学关系来精确表述。

假设法向间隙 $g_n \ge 0$ 表示无穿透，法向接触压力（或其在[弱形式](@entry_id:142897)中的对应物，[拉格朗日乘子](@entry_id:142696)）$\lambda_n \ge 0$ 表示压缩。则在接触界面上的每一点，必须同时满足以下三个条件 ：

1.  **运动学许可条件 (Kinematic Admissibility)**: $g_n \ge 0$ (不可穿透)。
2.  **静力学许可条件 (Static Admissibility)**: $\lambda_n \ge 0$ ([接触力](@entry_id:165079)只能是压力)。
3.  **互补松弛条件 (Complementarity Slackness)**: $g_n \lambda_n = 0$。

[互补条件](@entry_id:747558)是这组关系的核心，它优美地概括了接触的开关特性：如果两点之间存在间隙 ($g_n > 0$)，则它们之间的[接触力](@entry_id:165079)必须为零 ($\lambda_n = 0$)；反之，如果存在非零的接触压力 ($\lambda_n > 0$)，则两点必须紧密接触，间隙为零 ($g_n = 0$)。

在有限元框架中，有多种方法可以施加这些单边约束。这些方法在精度、计算成本和鲁棒性之间各有取舍。

#### [罚函数法](@entry_id:636090)

**[罚函数法](@entry_id:636090) (Penalty Method)** 是最直观和易于实现的方法之一。它将接触界面理想化为一张极硬的“弹簧床”。当从面穿透主面时 ($g_n < 0$)，一个与穿透深度成正比的排斥力（接触压力）便会产生。其关系式为：
$$
p_n = k_n \langle -g_n \rangle
$$
其中，$k_n$ 是**[罚刚度](@entry_id:753321) (penalty stiffness)**，一个需要用户指定的大数值；$\langle x \rangle = \max(x, 0)$ 是澳门括号，确保只有在穿透时才产生压力。

在[虚功原理](@entry_id:1133834)的框架下，这个[接触力](@entry_id:165079)对虚位移 $\boldsymbol{w}$ 做的虚功贡献，可以表示为一个边界积分项。在主动接触 ($g_n < 0$) 的情况下，修改后的虚功方程（[弱形式](@entry_id:142897)）为 ：
$$
\int_{\Omega} \boldsymbol{\sigma}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\boldsymbol{w}) \, dV - \int_{\Gamma_c} k_n g_n(\boldsymbol{u}) (\boldsymbol{w} \cdot \boldsymbol{n}) \, dA = \int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \boldsymbol{w} \, dA
$$
[罚函数法](@entry_id:636090)的优点是它不引入新的未知数，从而保持了[系统矩阵](@entry_id:172230)的规模和[正定性](@entry_id:149643)。然而，它的解是近似的。[罚刚度](@entry_id:753321) $k_n$ 的选择是一个微妙的平衡：太小会导致不可接受的穿透，太大则会使[系统矩阵](@entry_id:172230)变得**病态 (ill-conditioned)**，导致数值求解困难。例如，在一个简化的准一维压缩问题中，若[总压](@entry_id:265293)力为 $P$，接触面积为 $A$，则罚模型预测的穿透深度为 $\delta = P / (A k_n)$ 。这表明穿透量与[罚刚度](@entry_id:753321)成反比，只有当 $k_n \to \infty$ 时，穿透才趋于零。

#### [拉格朗日乘子法](@entry_id:176596)

与[罚函数法](@entry_id:636090)不同，**[拉格朗日乘子法](@entry_id:176596) (Lagrange Multiplier Method)** 旨在精确地施加不可穿透约束 $g_n \ge 0$。此方法引入一个新的未知场，即**[拉格朗日乘子](@entry_id:142696)场** $\lambda_n$，它在物理上就代表了接触压力。

通过构造一个包含总势能和约束项的**拉格朗日泛函 (Lagrangian functional)**，接触问题被转化为一个[鞍点问题](@entry_id:174221) 。这种混合公式 (mixed formulation) 同时求解位移场和乘子场。

然而，这种方法的精确性是有代价的。离散后的代数系统不再是正定的，而是具有鞍点结构的。其数值稳定性和[解的唯一性](@entry_id:143619)取决于位移插值空间和乘子插值空间之间的一个关键[相容性条件](@entry_id:637057)，即**Ladyzhenskaya–Babuška–Brezzi (LBB) 条件**，或称**[inf-sup 条件](@entry_id:174538)** 。

直观地说，LBB 条件要求乘子空间（压力）不能相对于位移[迹空间](@entry_id:756085)“过于丰富”。如果违反了此条件（例如，对位移和压力使用相同的连续线性插值），就会导致数值不稳定性，表现为计算出的接触压[力场](@entry_id:147325)出现剧烈的、非物理性的振荡。更糟糕的是，它可能导致**锁定 (locking)** 现象，即离散系统表现得过度刚硬，无法收敛到正确的解。为了满足[LBB条件](@entry_id:746626)，一个常见且稳健的选择是为拉格朗日乘子（压力）采用比位移低一阶的、不连续的插值，例如，对线性位移单元采用分片常数压力单元。

#### Nitsche 方法

**Nitsche 方法**是近年来流行的一种替代方案，它巧妙地结合了[罚函数法](@entry_id:636090)和[拉格朗日乘子法](@entry_id:176596)的特点。它像[罚函数法](@entry_id:636090)一样，不引入额外的[拉格朗日乘子](@entry_id:142696)变量，从而避免了[LBB条件](@entry_id:746626)的限制和[鞍点问题](@entry_id:174221)。但与[罚函数法](@entry_id:636090)不同，它通过在[弱形式](@entry_id:142897)中添加精心设计的**一致性项 (consistency terms)** 和**稳定性项 (stabilization term)** 来近似地满足约束，从而减小了对罚参数的敏感性。

一个典型的 Nitsche 弱形式包括标准弹性项、一个模拟[拉格朗日乘子](@entry_id:142696)作用的一致性项，以及一个类似于罚项的稳定性项 。根据一致性项符号的不同，可分为**对称**和**斜对称**两种变体。例如，其对称形式的接触贡献部分可写作：
$$
-\int_{\Gamma_c} p_n(\boldsymbol{v}) g_n(\boldsymbol{u}) d\Gamma - \int_{\Gamma_c} p_n(\boldsymbol{u}) g_n(\boldsymbol{v}) d\Gamma + \int_{\Gamma_c} \gamma g_n(\boldsymbol{u}) g_n(\boldsymbol{v}) d\Gamma
$$
其中的稳定化参数 $\gamma$ 并非任意选取，而是需要足够大以保证离散系统的[矫顽性](@entry_id:159399) (coercivity)。其临界值可以通过局部化的谱分析推导出来，通常与[单元刚度矩阵](@entry_id:139369)和单元边界上的力-位移算子有关 。Nitsche 方法因其良好的稳定性和精度，已成为处理接触问题的一个强大工具。

### [摩擦接触](@entry_id:1125326)

当接触面之间不仅有[法向力](@entry_id:174233)，还存在切向力时，问题就进入了摩擦的范畴。

#### [库仑摩擦模型](@entry_id:747944)

最经典的摩擦模型是**[库仑摩擦定律](@entry_id:747943) (Coulomb's Law of Friction)**。它是一个经验模型，其核心思想是：

1.  切向摩擦力的大小存在一个上限，该上限与法向压力 $\lambda_n$ 成正比，比例系数为**摩擦系数 (coefficient of friction)** $\mu$。所有许可的切向摩擦力 $\boldsymbol{\lambda}_t$ 必须位于一个**[摩擦锥](@entry_id:171476) (friction cone)** 内，即 $\|\boldsymbol{\lambda}_t\| \le \mu \lambda_n$。
2.  当切向力小于该上限时，接触点处于**[粘滞](@entry_id:201265)状态 (stick state)**，没有相对滑动，即切向滑移速率 $\dot{\boldsymbol{g}}_t = \boldsymbol{0}$。
3.  当切向力达到上限时，接触点进入**滑移状态 (slip state)**，发生相对滑动。此时，摩擦力的方向与相对滑动的方向相反，其大小恰好等于摩擦力上限，即 $\boldsymbol{\lambda}_t = -\mu \lambda_n \frac{\dot{\boldsymbol{g}}_t}{\|\dot{\boldsymbol{g}}_t\|}$。

这个模型可以通过**最大耗散原理 (principle of maximum dissipation)** 得到更严格的理论支撑 。该原理指出，在所有满足[摩擦锥](@entry_id:171476)约束的许可摩擦力中，实际发生的摩擦力 $\boldsymbol{\lambda}_t$ 将使得[能量耗散](@entry_id:147406)率 $\mathcal{D} = -\boldsymbol{\lambda}_t \cdot \dot{\boldsymbol{g}}_t$ 最大化。通过求解这个约束最大化问题，可以唯一地确定在给定滑移速率 $\dot{\boldsymbol{g}}_t$ 下的摩擦力，其结果与上述的粘滞-[滑移条件](@entry_id:1131753)完全吻合。

#### 数值实现：[返回映射算法](@entry_id:168456)

[库仑定律](@entry_id:139360)的[非线性](@entry_id:637147)、非光滑以及历史依赖性（粘滞状态下的摩擦力取决于加载历史）给数值实现带来了挑战。直接求解变得非常困难。为此，发展了一套高效的**[返回映射算法](@entry_id:168456) (return-mapping algorithm)**，广泛应用于[计算塑性力学](@entry_id:171377)和[接触力学](@entry_id:177379)。

该算法是一个两步的**预测-修正 (predictor-corrector)** 过程 ：

1.  **预测步 (Trial Step)**: 在一个时间步内，首先假定切向响应是纯弹性的。基于上一时刻的切向应力 $\boldsymbol{t}^n$ 和当前时间步的切向相对位移增量 $\Delta\boldsymbol{u}_t$，计算出一个**试探切向应力 (trial tangential traction)**：
    $$
    \boldsymbol{t}^{\text{trial}} = \boldsymbol{t}^n + k_t \Delta\boldsymbol{u}_t
    $$
    其中 $k_t$ 是切向[罚刚度](@entry_id:753321)。

2.  **修正步 (Return/Correction Step)**: 检查试探应力是否在许可的[摩擦锥](@entry_id:171476)内。
    *   **如果 $\|\boldsymbol{t}^{\text{trial}}\| \le \mu p_n$**，说明试探应力是许可的，接触点处于[粘滞](@entry_id:201265)状态。最终的切向应力就是试探应力：$\boldsymbol{t}^{n+1} = \boldsymbol{t}^{\text{trial}}$。
    *   **如果 $\|\boldsymbol{t}^{\text{trial}}\| > \mu p_n$**，说明试探应力超出了[摩擦锥](@entry_id:171476)，是非物理的。此时接触点处于滑移状态。必须将试探应力“返回”到[摩擦锥](@entry_id:171476)的边界上。这个返回操作是一个[最近点投影](@entry_id:168047)，即将试探应力向量径向地缩放回[摩擦锥](@entry_id:171476)的边界：
        $$
        \boldsymbol{t}^{n+1} = \mu p_n \frac{\boldsymbol{t}^{\text{trial}}}{\|\boldsymbol{t}^{\text{trial}}\|}
        $$
    这个过程确保了在每个时间步结束时，摩擦定律都得到满足。

#### 正则化摩擦模型

库仑模型在[粘滞](@entry_id:201265)与滑移转换点上的非[光滑性](@entry_id:634843)（数学上的“[尖点](@entry_id:636792)”）给基于梯度的[非线性求解器](@entry_id:177708)（如牛顿-拉夫逊法）带来了困难，因为它导致[雅可比矩阵](@entry_id:178326)（[切线刚度](@entry_id:166213)）的定义不唯一。为了克服这一问题，研究者们提出了各种**正则化摩擦模型 (regularized friction models)**。

一个常见的正则化模型是引入粘性项，使得摩擦力平滑地依赖于滑移速率 。例如，使用[双曲正切函数](@entry_id:634307)：
$$
\boldsymbol{\lambda}_t = \mu \lambda_n \tanh\left(\frac{\|\dot{\boldsymbol{g}}_t\|}{v_0}\right) \frac{\dot{\boldsymbol{g}}_t}{\|\dot{\boldsymbol{g}}_t\|}
$$
其中 $v_0$ 是一个小的参考速度，用于控制过渡区域的光滑程度。

该正则化模型具有许多优良的数值特性  ：
*   **[光滑性](@entry_id:634843)**: 摩擦力对于滑移速率是连续且可微的，这使得标准的牛顿-拉夫逊法可以有效应用，并有望实现二次收敛。
*   **存在耗散势**: 该模型可以从一个凸的[标量耗散](@entry_id:1131248)势 $\psi(\dot{\boldsymbol{g}}_t)$ 的梯度导出，即 $\boldsymbol{\lambda}_t = \partial \psi / \partial \dot{\boldsymbol{g}}_t$。这保证了算法[切线[刚度矩](@entry_id:170852)阵](@entry_id:178659)的对称性，有利于线性方程组的求解。
*   **物理近似**: 当滑移速率远大于 $v_0$ 时，$\tanh(\cdot) \to 1$，模型近似于库仑[滑移条件](@entry_id:1131753)。当滑移速率远小于 $v_0$ 时，$\tanh(x) \approx x$，模型退化为一个线性[粘性阻尼](@entry_id:168972)关系 $\boldsymbol{\lambda}_t \approx (\mu \lambda_n / v_0) \dot{\boldsymbol{g}}_t$。

然而，正则化也引入了新的问题。参数 $v_0$ 的选择会影响结果，并且当 $v_0$ 或时间步长 $\Delta t$ 过小时，算法的[切线刚度](@entry_id:166213)会变得非常大，导致[系统矩阵](@entry_id:172230)病态，从而恶化求解器的收敛性能 。

### 高级离散化与材料考虑因素

在生物力学等复杂应用中，除了基本的接触和摩擦定律，还必须考虑离散化精度和特殊材料行为带来的挑战。

#### 几何保真度与[非匹配网格](@entry_id:168552)

[有限元网格](@entry_id:174862)的离散化方式对接触分析的精度有显著影响。

*   **节点-面 (Node-to-Surface, N2S) 算法的几何偏差**: 在经典的N2S算法中，约束仅在从面节点上施加。当接触面为曲面时，这会导致一种称为**几何偏差 (geometric bias)** 的系统性误差。即使从面节点被精确地约束在主面上，节点之间的平直单元边也会穿透到凸的主面内部，或者与凹的主面形成间隙 。这种非物理的穿透或间隙会产生虚假的[接触力](@entry_id:165079)，导致系统表现出过度的刚度，并且使得算法无法通过弯曲界面上的**接触补片测试 (contact patch test)**。该偏差的大小与单元尺寸 $h$ 和主面曲率 $\kappa$ 的乘积 $\kappa h$ 成正比。

*   **面-面 (Surface-to-Surface, S2S) 与[砂浆法](@entry_id:752184) (Mortar Methods) 的改进**: 为了克服N2S的缺陷，发展了S2S和更严格的[砂浆法](@entry_id:752184)。这些方法的核心思想是在弱形式（积分形式）下施加约束，而不是在离散点上。例如，[砂浆法](@entry_id:752184)通过构造一个独立的[拉格朗日乘子](@entry_id:142696)空间和一套对偶形函数，在整个接触界面上以积分的方式来传递约束。这种变分一致的公式能够平均掉N2S中的局部穿透误差，使得误差阶次从 $O(\kappa h)$ 降低到 $O((\kappa h)^2)$ 。

*   **处理[非匹配网格](@entry_id:168552)**: 在模拟复杂几何（如人体关节）时，接触体双方的表面网格往往尺寸和节点位置都无法匹配，即**[非匹配网格](@entry_id:168552) (non-matching meshes)**。N2S算法在此情况下会严重破坏[牛顿第三定律](@entry_id:166652)的离散形式，即作用力与[反作用](@entry_id:203910)力在离散节点力向量的层面上不再相等和相反，从而导致**全局平衡 (global equilibrium)** 的丧失 。而[砂浆法](@entry_id:752184)的主要优势之一就是能出色地处理[非匹配网格](@entry_id:168552)。其变分一致的积分形式确保了离散[接触力](@entry_id:165079)算子的伴随性，从而在离散层面上精确地保持了作用力与反作用力定律，即使在网格完全不匹配的情况下也能保证全局动量守恒  。

#### 材料不可压缩性与[体积锁定](@entry_id:172606)

生物软组织（如软骨、肌腱）通常表现出近乎**不可压缩 (nearly incompressible)** 的特性，其[泊松比](@entry_id:158876) $\nu$ 接近 $0.5$。这给标准的、纯位移的有限元公式带来了巨大挑战。

当 $\nu \to 0.5$ 时，材料的[体积模量](@entry_id:160069) $K \to \infty$。在纯位移单元中，位移[插值函数](@entry_id:262791)隐式地约束了单元的体积变形能力。当材料本身几乎不可压缩时，这种离散带来的约束与材料的物理约束相冲突，导致单元表现得极其刚硬，无法正确变形。这种现象被称为**[体积锁定](@entry_id:172606) (volumetric locking)**。在接触问题中，[体积锁定](@entry_id:172606)会导致计算出的接触压力产生剧烈的非物理振荡，并且其数值会被人为地、极大地夸大。

我们可以通过一个简化的[平面应变](@entry_id:167046)压缩问题来量化这个问题。对于一个标准位移单元，其预测的接触压力 $P_1$ 与泊松比的关系为 $P_1 \propto \frac{1-\nu}{1-2\nu}$。显然，当 $\nu \to 0.5$ 时，$P_1 \to \infty$ 。

为了解决[体积锁定](@entry_id:172606)问题，必须采用**混合公式 ($u-p$ formulation)**。在这种方法中，[静水压力](@entry_id:275365) $p$ (或等效的[体积应变](@entry_id:267252))被当作一个独立的未知场，与位移场 $\boldsymbol{u}$ 一同求解。通过将[应力张量](@entry_id:148973)分解为偏量[部分和](@entry_id:162077)静水压力部分，并将压力与[体积应变](@entry_id:267252)的关系通过一个独立的[约束方程](@entry_id:138140)（而不是直接通过[位移梯度](@entry_id:165352)）来施加，混合单元极大地缓解了[体积锁定](@entry_id:172606)的问题。在上述同样的问题中，一个稳定的混合公式预测的接触压力 $P_2$ 将不再依赖于 $(1-2\nu)^{-1}$ 这一项，从而在[近不可压缩](@entry_id:752387)极限下保持有界和准确 。因此，在进行[软组织生物力学](@entry_id:1121634)接触分析时，选择能够避免[体积锁定](@entry_id:172606)的单元技术（如混合单元）是至关重要的。