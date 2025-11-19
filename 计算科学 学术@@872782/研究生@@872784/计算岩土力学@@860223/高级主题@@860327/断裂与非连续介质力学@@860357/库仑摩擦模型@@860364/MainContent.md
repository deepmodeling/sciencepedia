## 引言
[库仑摩擦模型](@entry_id:747944)是描述两个接触表面之间剪切阻力的基石，在计算岩[土力学](@entry_id:180264)、工程和物理科学中无处不在。从模拟地震断层的滑动到设计机器ンの稳定抓取，准确地对摩擦行为进行建模至关重要。然而，摩擦现象固有的非光滑和[非线性](@entry_id:637147)特性——即黏滞（stick）与滑移（slip）状态之间的突然切换——给理论分析和数值模拟带来了巨大的挑战。本文旨在系统性地攻克这一难题，为读者构建一个从基本原理到高级应用的完整知识体系。

本文将分为三个核心部分。在“原理与机制”一章中，我们将从最基本的接触定律出发，深入剖析[库仑摩擦](@entry_id:169196)的数学表述、[变分形式](@entry_id:166033)以及在数值计算中实现它的关键算法。接着，在“应用与跨学科联系”一章中，我们将视野扩展到现实世界，探讨该模型如何应用于分析地震滑坡、先进材料行为，并揭示其与[机器人学](@entry_id:150623)、控制理论等领域的深刻联系。最后，通过“动手实践”部分，你将有机会运用所学知识解决具体的计算问题，从而巩固理论并提升实践能力。让我们首先进入第一章，奠定理解摩擦行为的理论基础。

## 原理与机制

本章旨在系统性地阐述[库仑摩擦模型](@entry_id:747944)的基本原理与核心机制。在前一章介绍背景知识的基础上，本章将深入探讨控制摩擦行为的数学定律、其在计算力学中的实现算法，以及在岩土力学领域中至关重要的若干高等概念。我们将从最基本的接触定律出发，逐步构建一个完整而严谨的理论框架。

### [接触与摩擦](@entry_id:747779)的基本定律

在模拟两个物体间的相互作用时，我们需要分别描述法向和切向的行为。法向行为由接触定律控制，确保物体不会相互穿透；切向行为则由摩擦定律控制，描述界面上的剪切阻力。

#### 单边法向接触

考虑两个可能接触的物体，其接触界面上任意一点的几何关系可以用**法向间隙** $g_n$ 来描述。我们约定，当 $g_n > 0$ 时，两物体表面存在物理间隙，处于分离状态；当 $g_n = 0$ 时，两物体表面恰好接触。物理上的**不可入性（impenetrability）**约束要求法向间隙必须为非负值：

$$
g_n \ge 0
$$

与法向间隙 $g_n$ 共轭的力学量是**法向接触压力** $p$。按照岩土力学中的惯例，我们定义压应力为正，即当物体相互挤压时 $p > 0$。对于典型的无粘结性接触（如岩石节理或土体颗粒间的接触），界面无法承受拉力。这一**无粘结性（non-adhesion）**的物理特性意味着法向接触压力也必须为非负值：

$$
p \ge 0
$$

这两个条件并非[相互独立](@entry_id:273670)。当物体间存在间隙（$g_n > 0$）时，它们之间不可能有接触力，因此压力必须为零（$p = 0$）。反之，当存在接触压力（$p > 0$）时，物体必须紧密接触，因此间隙必须为零（$g_n = 0$）。这种“或此或彼”的逻辑关系可以用一个**[互补条件](@entry_id:747558)（complementarity condition）**来精确描述：

$$
p \cdot g_n = 0
$$

综合以上三条，我们得到了描述无粘结、单边法向接触的完整数学表达，这组条件在文献中常被称为**[Signorini条件](@entry_id:169339)**或Hertz-Signorini-Moreau条件 [@problem_id:3512322]：

$$
g_n \ge 0, \quad p \ge 0, \quad p \cdot g_n = 0
$$

这组简单的方程构成了所有接触力学问题的基础，它以一种优雅的方式同时编码了运动学约束（$g_n \ge 0$）、动力学约束（$p \ge 0$）以及两者之间的开关逻辑（$p \cdot g_n = 0$）。

#### 经典[库仑摩擦定律](@entry_id:747943)

当两个表面在正压力 $p$ 的作用下接触时，它们之间便产生了抵抗相对切向运动的能力，即[摩擦力](@entry_id:171772)。最经典且应用最广泛的模型是**[库仑摩擦定律](@entry_id:747943)**。该定律的核心思想是，界面能够承受的极限切向力（[摩擦力](@entry_id:171772)）与作用在其上的法向压力成正比。

令 $\boldsymbol{\tau}$ 为界面上的切向牵[引力](@entry_id:175476)矢量，$\mu$ 为**[摩擦系数](@entry_id:150354)**，它是一个无量纲的材料参数，取决于接触面的粗糙度、材料属性等。[库仑定律](@entry_id:139360)将界面的摩擦状态分为两种截然不同的情形：

1.  **黏滞状态（Stick/No-Slip）**: 如果切向牵[引力](@entry_id:175476)的模量小于或等于最大[静摩擦力](@entry_id:163518)，即 $\|\boldsymbol{\tau}\| \le \mu p$，则界面保持“锁定”，没有相对切向运动。此时，相对切向速度 $\boldsymbol{v}_t = \boldsymbol{0}$。切向牵[引力](@entry_id:175476) $\boldsymbol{\tau}$ 的大小和方向由系统的弹性变形或外部驱动力决定，只要其不超过摩擦极限即可。这个不等式 $\|\boldsymbol{\tau}\| \le \mu p$ 定义了应力空间中的一个允许区域，称为**[摩擦锥](@entry_id:171476)（friction cone）**。

2.  **滑移状态（Slip/Sliding）**: 如果驱动力足够大，使得切向牵[引力](@entry_id:175476)达到了摩擦极限，即 $\|\boldsymbol{\tau}\| = \mu p$，界面就会开始相对滑动。此时，相对切向速度 $\boldsymbol{v}_t \neq \boldsymbol{0}$。[摩擦力](@entry_id:171772)作为一种[耗散力](@entry_id:166970)，其方向总是与相对运动的方向相反。若定义相对滑移方向的单位矢量为 $\boldsymbol{m} = \boldsymbol{v}_t / \|\boldsymbol{v}_t\|$，则滑移状态下的切向牵[引力](@entry_id:175476)可以精确表示为：

    $$
    \boldsymbol{\tau} = - (\mu p) \boldsymbol{m} = - (\mu p) \frac{\boldsymbol{v}_t}{\|\boldsymbol{v}_t\|}
    $$

这个定律的一个关键前提是法向压力的存在（$p > 0$）。从公式 $\|\boldsymbol{\tau}\| \le \mu p$ 可以看出，如果法向压力为零或为拉力（$p \le 0$），[摩擦力](@entry_id:171772)的上限将为零或负值。由于力的模量 $\|\boldsymbol{\tau}\|$ 必然为非负，因此在 $p \le 0$ 的情况下，唯一可能的解是 $\boldsymbol{\tau} = \boldsymbol{0}$。这意味着没有法向压力，就没有[摩擦力](@entry_id:171772)。

从[热力学](@entry_id:141121)角度看，摩擦是一个能量耗散过程。单位面积的[耗散功率](@entry_id:177328) $\mathcal{D}$ 等于[摩擦力](@entry_id:171772)所做功的速率的[相反数](@entry_id:151709)，即 $\mathcal{D} = -\boldsymbol{\tau} \cdot \boldsymbol{v}_t$。根据[热力学第二定律](@entry_id:142732)，耗散必须为非负，即 $\mathcal{D} \ge 0$。在滑移状态下，将 $\boldsymbol{\tau} = - \mu p (\boldsymbol{v}_t / \|\boldsymbol{v}_t\|)$ 代入，得到 $\mathcal{D} = - \left(-\mu p \frac{\boldsymbol{v}_t}{\|\boldsymbol{v}_t\|}\right) \cdot \boldsymbol{v}_t = \mu p \|\boldsymbol{v}_t\|$。由于 $\mu \ge 0$ 且 $\|\boldsymbol{v}_t\| \ge 0$，要保证 $\mathcal{D} \ge 0$，就必须有 $p \ge 0$。这为“[库仑摩擦](@entry_id:169196)与法向拉力不相容”提供了更基本的物理依据 [@problem_id:3512322]。

### [库仑摩擦](@entry_id:169196)的数学表述

为了在数学和计算模型中精确地使用库仑定律，我们需要一个严谨的表述。除了上述的分段定义，现代接触力学更倾向于使用基于[变分原理](@entry_id:198028)的等价形式。

#### [分段函数](@entry_id:160275)形式与[变分形式](@entry_id:166033)

[库仑摩擦定律](@entry_id:747943)的分段性质给数值求解带来了挑战，因为它在黏滞与滑移的转换点上是**非光滑（non-smooth）**的。一个更紧凑且在数学上更强大的表述可以借助[凸分析](@entry_id:273238)中的**次梯度（subdifferential）**概念来构建 [@problem_id:3512296]。

考虑一个**耗散势函数** $\Psi(\boldsymbol{v}_t) = \mu p \|\boldsymbol{v}_t\|$，它表示在给定法向压力 $p$ 和相对速度 $\boldsymbol{v}_t$ 下的最大可能[耗散率](@entry_id:748577)。[库仑摩擦定律](@entry_id:747943)可以被优雅地表达为切向牵[引力](@entry_id:175476) $\boldsymbol{\tau}$ 属于该势函数关于速度 $\boldsymbol{v}_t$ 的次梯度：

$$
\boldsymbol{\tau} \in \partial \Psi(\boldsymbol{v}_t) = \mu p \, \partial \|\boldsymbol{v}_t\|
$$

这里的 $\partial\|\boldsymbol{v}_t\|$ 是欧几里得范数函数 $\|\cdot\|$ 的次梯度。这个单一的包含关系式完美地统一了黏滞和滑移两种状态：

*   当 $\boldsymbol{v}_t \neq \boldsymbol{0}$ 时，范数函数是可微的，其梯度为 $\nabla \|\boldsymbol{v}_t\| = \boldsymbol{v}_t / \|\boldsymbol{v}_t\|$。此时[次梯度](@entry_id:142710)集合中只有一个元素，即该梯度。于是上式变为 $\boldsymbol{\tau} = \mu p (\boldsymbol{v}_t / \|\boldsymbol{v}_t\|)$。（注意：在此变分推导中，$\boldsymbol{\tau}$ 与 $\boldsymbol{v}_t$ 方向相同，这对应于最大耗散原理；在实际物理模型中，[摩擦力](@entry_id:171772)与速度相反，这取决于具体的公式约定。核心思想是共线性。）
*   当 $\boldsymbol{v}_t = \boldsymbol{0}$ 时，范数函数在原点不可微。其在该点的次梯度是所有模长不大于1的向量组成的集合，即一个闭合的单位球（在二维中为[单位圆盘](@entry_id:172324)）：$\partial\|\boldsymbol{0}\| = \{\boldsymbol{z} \mid \|\boldsymbol{z}\| \le 1\}$。因此，摩擦定律变为 $\boldsymbol{\tau} \in \{\mu p \boldsymbol{z} \mid \|\boldsymbol{z}\| \le 1\}$，这等价于黏滞条件 $\|\boldsymbol{\tau}\| \le \mu p$。

这种[变分形式](@entry_id:166033)不仅在理论上更为优雅，也为设计稳健的数值算法（如[变分不等式](@entry_id:172788)求解器）奠定了基础。而经典的分段定义，即：

$$
\begin{cases}
\|\boldsymbol{\tau}\| \le \mu p  \text{if } \boldsymbol{v}_t = \boldsymbol{0} \\
\boldsymbol{\tau} = - \mu p \frac{\boldsymbol{v}_t}{\|\boldsymbol{v}_t\|}  \text{if } \boldsymbol{v}_t \neq \boldsymbol{0}
\end{cases}
$$

可以被视为上述变分原理的KKT（[Karush-Kuhn-Tucker](@entry_id:634966)）条件，两者在本质上是等价的 [@problem_id:3512296]。

### 计算实现与算法

将非光滑、[非线性](@entry_id:637147)的[库仑摩擦定律](@entry_id:747943)应用于[数值模拟](@entry_id:137087)（如有限元法FEM或[离散元法](@entry_id:748501)DEM）需要专门的算法。核心思想通常是采用一种**增量式（incremental）**的预测-校正方案。

#### [返回映射算法](@entry_id:168456)

在基于位移的隐式[有限元分析](@entry_id:138109)中，**[返回映射算法](@entry_id:168456)（return-mapping algorithm）**是处理[弹塑性](@entry_id:193198)或摩擦问题的标准方法。在一个时间（或荷载）增量步内，该算法分为两步 [@problem_id:3512346]：

1.  **弹性预测步（Elastic Predictor）**: 首先，假设在整个增量步内接触点的行为是纯弹性的（即处于黏滞状态）。基于这一假设，计算出一个**试验切向牵[引力](@entry_id:175476)（trial tangential traction）**，记为 $\boldsymbol{\tau}^{\text{tr}}$。

2.  **塑性校正步（Plastic Corrector）**: 接下来，检查试验牵[引力](@entry_id:175476)是否满足摩擦约束，即判断它是否位于[摩擦锥](@entry_id:171476)内部：$\|\boldsymbol{\tau}^{\text{tr}}\| \stackrel{?}{\le} \mu p$。
    *   如果满足约束（$\|\boldsymbol{\tau}^{\text{tr}}\| \le \mu p$），则弹性假设成立。界面处于黏滞状态，真实的切向牵[引力](@entry_id:175476)就是试验值，即 $\boldsymbol{\tau} = \boldsymbol{\tau}^{\text{tr}}$。
    *   如果违反约束（$\|\boldsymbol{\tau}^{\text{tr}}\| > \mu p$），则弹性假设错误，界面发生了滑移。真实的切向牵[引力](@entry_id:175476)必须位于[摩擦锥](@entry_id:171476)的边界上。此时，需要将试验牵[引力](@entry_id:175476)“返回”或“投影”到[摩擦锥](@entry_id:171476)的表面。校正后的牵[引力](@entry_id:175476) $\boldsymbol{\tau}$ 与试验牵[引力](@entry_id:175476) $\boldsymbol{\tau}^{\text{tr}}$ 方向相同，但其模量被缩放到极限值 $\mu p$：
        $$
        \boldsymbol{\tau} = \mu p \frac{\boldsymbol{\tau}^{\text{tr}}}{\|\boldsymbol{\tau}^{\text{tr}}\|}
        $$

这个过程确保了最终的应力状态始终满足物理约束。例如，考虑一个接触点，其法向压力 $p=1.5\,\text{MPa}$，[摩擦系数](@entry_id:150354) $\mu=0.5$。摩擦极限为 $\mu p = 0.75\,\text{MPa}$。若弹性预测得到的试验牵[引力](@entry_id:175476)为 $\boldsymbol{\tau}^{\text{tr}} = -0.8\,\text{MPa}\,\boldsymbol{e}_{1}+0.6\,\text{MPa}\,\boldsymbol{e}_{2}$，其模量 $\|\boldsymbol{\tau}^{\text{tr}}\| = \sqrt{(-0.8)^2 + 0.6^2} = 1.0\,\text{MPa}$。由于 $1.0\,\text{MPa} > 0.75\,\text{MPa}$，滑移发生。最终的牵[引力](@entry_id:175476)将被“[拉回](@entry_id:160816)”到[摩擦锥](@entry_id:171476)边界，其方向与 $\boldsymbol{\tau}^{\text{tr}}$ 相同，模量为 $0.75\,\text{MPa}$。最终的牵[引力](@entry_id:175476)为 $\boldsymbol{\tau} = 0.75 \frac{\boldsymbol{\tau}^{\text{tr}}}{1.0} = -0.6\,\text{MPa}\,\boldsymbol{e}_{1}+0.45\,\text{MPa}\,\boldsymbol{e}_{2}$。值得注意的是，在这种情况下，最终的牵[引力](@entry_id:175476)方向应该与实际的滑移速度方向相反。如果已知滑移速度 $\boldsymbol{v}_t$ 的方向，则最终牵[引力](@entry_id:175476)由 $\boldsymbol{\tau} = -\mu p (\boldsymbol{v}_t / \|\boldsymbol{v}_t\|)$ 给出 [@problem_id:3512346]。

#### 离散元方法中的Cundall-Strack模型

[返回映射](@entry_id:754324)的思想在[离散元法](@entry_id:748501)（DEM）中也有直接体现，其中最著名的就是**Cundall-Strack模型** [@problem_id:3512323]。该模型将颗粒间的接触理想化为一个法向弹簧和切向弹簧-滑块系统。

*   [法向力](@entry_id:174233)由法向弹簧的压缩量（颗粒重叠量 $\delta_n$）决定：$F_n = k_n \delta_n$。
*   切向力则更为复杂。一个切向弹簧记录了[接触过程](@entry_id:152214)中的弹性切向位移 $\boldsymbol{\xi}_t$。切向力由 $\boldsymbol{F}_t = -k_t \boldsymbol{\xi}_t$ 给出。在一个增量步中，当有相对切向位移增量 $\Delta \boldsymbol{u}_t$ 发生时：
    1.  **弹性预测**: 计算一个试验的弹性位移 $\boldsymbol{\xi}_{t, \text{trial}} = \boldsymbol{\xi}_t^{\text{old}} + \Delta \boldsymbol{u}_t$，并由此得到试验切向力 $\boldsymbol{F}_{t, \text{trial}} = -k_t \boldsymbol{\xi}_{t, \text{trial}}$。
    2.  **屈服检查**: 比较试验力的模量与摩擦极限 $\|\boldsymbol{F}_{t, \text{trial}}\| \stackrel{?}{\le} \mu F_n$。
    3.  **状态更新**:
        *   若**黏滞**，则接受试验状态：$\boldsymbol{F}_t^{\text{new}} = \boldsymbol{F}_{t, \text{trial}}$，$\boldsymbol{\xi}_t^{\text{new}} = \boldsymbol{\xi}_{t, \text{trial}}$。
        *   若**滑移**，则将力投影回摩擦极限：$\boldsymbol{F}_t^{\text{new}} = \mu F_n \frac{\boldsymbol{F}_{t, \text{trial}}}{\|\boldsymbol{F}_{t, \text{trial}}\|}$。关键在于，内部状态变量（弹性弹簧位移）也必须被更新以与这个新的力保持一致：$\boldsymbol{\xi}_t^{\text{new}} = -\boldsymbol{F}_t^{\text{new}} / k_t$。这个对内部变量的校正至关重要，它代表了因塑性滑移而释放的弹性变形，确保了模型的历史依赖性。

#### 有限元方法中的[一致化](@entry_id:756317)[切线刚度](@entry_id:166213)

在隐式有限元求解中，为了获得牛顿-拉夫逊（[Newton-Raphson](@entry_id:177436)）迭代法的二次收敛速度，需要提供系统的**[切线刚度矩阵](@entry_id:170852)（tangent stiffness matrix）**。对于[摩擦接触](@entry_id:749595)问题，这对应于**[一致化](@entry_id:756317)[算法切线](@entry_id:165770)（consistent algorithmic tangent）**，即在离散增量步的框架下，接触点牵[引力](@entry_id:175476)对位移跳跃的导数 $\boldsymbol{J} = \partial\boldsymbol{t}/\partial\boldsymbol{\delta}$。

由于[库仑摩擦](@entry_id:169196)的非光滑性，这个[切线刚度](@entry_id:166213)在黏滞和滑移状态下是不同的 [@problem_id:3512281]：

*   **黏滞状态**: 行为是弹性的，法向和切向是解耦的。[切线](@entry_id:268870)矩阵是对角的：
    $$
    \boldsymbol{J}_{\text{stick}} = \begin{pmatrix} \partial t_n / \partial \delta_n & \partial t_n / \partial \delta_t \\ \partial t_t / \partial \delta_n & \partial t_t / \partial \delta_t \end{pmatrix} = \begin{pmatrix} k_n & 0 \\ 0 & k_t \end{pmatrix}
    $$
    其中 $k_n$ 和 $k_t$ 是法向和切向的[罚刚度](@entry_id:753321)。

*   **滑移状态**: 行为是[弹塑性](@entry_id:193198)的。此时，切向牵[引力](@entry_id:175476)的大小直接依赖于法向压力 $t_n$ (即 $t_t = \mu \, t_n \cdot \mathrm{sign}(\delta_t)$)，而与切向位移 $\delta_t$ 无关。这导致[切线](@entry_id:268870)矩阵变得非对角且非对称：
    $$
    \boldsymbol{J}_{\text{slip}} = \begin{pmatrix} k_n & 0 \\ \mu k_n \cdot \mathrm{sign}(\delta_t) & 0 \end{pmatrix}
    $$
    这里的非对角项 $J_{tn} = \partial t_t / \partial \delta_n = \mu k_n \cdot \mathrm{sign}(\delta_t)$ 反映了法向-切向的耦合：法向位移的变化会改变[法向力](@entry_id:174233)，从而改变切向[摩擦力](@entry_id:171772)的极限。而 $J_{tt} = \partial t_t / \partial \delta_t = 0$ 则是[一致化](@entry_id:756317)塑性[切线](@entry_id:268870)的典型特征，表明在完美塑性流动中，应力不再随塑性应变增量而增加。这个非对称的[切线](@entry_id:268870)矩阵是**[非关联塑性](@entry_id:186531)流动（non-associative plasticity）**的一个标志，[库仑摩擦](@entry_id:169196)是其典型例子。

### 岩[土力学](@entry_id:180264)中的高等摩擦概念

经典的库仑模型虽然强大，但在描述岩土材料复杂的摩擦行为时仍有局限。以下几个方面是对基础模型的关键扩展。

#### [路径依赖性](@entry_id:186326)与非光滑能量函数

摩擦是一个不可逆的耗散过程，这意味着系统的响应具有**[路径依赖性](@entry_id:186326)（path dependence）**。对于同一个最终荷载状态，通过不同加载路径（例如，单调加载 vs. 加载-卸载-再加载）到达，系统的最终构型（位移、应力）可能会完全不同 [@problem_id:3512313]。

从变分角度看，这个问题源于包含摩擦耗散的增量[能量泛函](@entry_id:170311)的非光滑性。在一个增量步中，系统寻求最小化的泛函 $\Pi$ 是[弹性势能](@entry_id:168893) $E_{el}$ 和摩擦[耗散功](@entry_id:748576) $W_{diss}$ 的和。[耗散功](@entry_id:748576)正比于滑移距离的[绝对值](@entry_id:147688)，例如 $\mu N |\Delta u|$。这个[绝对值](@entry_id:147688)项使得总泛函 $\Pi$ 在零滑移点（黏滞-滑移转换点）是不可微的。

因此，不能用传统的基于梯度的[欧拉-拉格朗日方程](@entry_id:137827)来寻找最优解，而必须使用[次梯度](@entry_id:142710)理论。更重要的是，由于每一步的耗散都不可恢复，系统的“[能量景观](@entry_id:147726)”是**非保守的**。每一步的最优解都取决于上一步的终点，而上一步的终点又取决于之前的路径。这种对加载历史的“记忆”是摩擦系统最根本的特性之一。

#### 剪胀与[非关联流动法则](@entry_id:752544)

当剪切作用于粗糙的岩石节理或密实的[颗粒材料](@entry_id:750005)时，我们常常观察到一种称为**剪胀（dilatancy）**的现象：切向滑移会伴随着法向的膨胀或抬升。这是因为滑移必须克服界面上相互啮合的凸起（asperities），导致界面“爬升” [@problem_id:3512339]。

在塑性力学框架中，这种剪切-体积耦合是通过**[非关联流动法则](@entry_id:752544)（non-associated flow rule）**来描述的。这意味着用于定义塑性应变增量方向的**塑性[势函数](@entry_id:176105) $Q$** 与定义屈服条件的**[屈服函数](@entry_id:167970) $F$** 是不同的。对于[库仑摩擦](@entry_id:169196)，[屈服函数](@entry_id:167970)为 $F = |\tau| + \sigma_n' \tan\phi$，其中 $\phi$ 是摩擦角。而塑性[势函数](@entry_id:176105)可以写为 $Q = |\tau| + \sigma_n' \tan\psi$，其中 $\psi$ 是**[剪胀角](@entry_id:748435)**。

根据[流动法则](@entry_id:177163)，塑性应变增量（即滑移增量 $d\delta_t^p$ 和法向张开增量 $dg_n^p$）的方向垂直于[势函数](@entry_id:176105) $Q$ 的[等值面](@entry_id:196027)。这导致：

$$
\frac{dg_n^p}{d\delta_t^p} = \tan\psi
$$

这个关系表明，每发生单位的切向塑性滑移，就会产生 $\tan\psi$ 单位的法向张开。[剪胀角](@entry_id:748435) $\psi$ 是一个独立的材料参数，它控制着剪胀的程度。当 $\psi = \phi$ 时，[流动法则](@entry_id:177163)是关联的；当 $\psi = 0$ 时，没有剪胀；当 $\psi  \phi$（岩土材料的常见情况），流动法则是非关联的。

#### 体材料模型与界面模型的区别

在岩土工程模拟中，区分**体材料（bulk）**的[本构模型](@entry_id:174726)和**界面（interface）**的本构模型至关重要 [@problem_id:3512302]。

*   **体材料模型**，如**Mohr-Coulomb塑性模型**，描述的是三维连续介质内部的[应力-应变关系](@entry_id:274093)。其[屈服准则](@entry_id:193897)通常用[应力不变量](@entry_id:170526)来表示，例如 $q = M p' + c$，其中 $p'$ 是[平均有效应力](@entry_id:751815)，q是偏[应力[不变](@entry_id:170526)量](@entry_id:148850)。这些[不变量](@entry_id:148850)是对整个三维应力状态的综合度量。参数 $M$ 与材料的[内摩擦角](@entry_id:197521) $\phi$ 相关，但其关系依赖于应力状态（例如，通过[Lode角](@entry_id:191590)体现），并非简单的 $M=\tan\phi$。

*   **界面模型**，如我们一直讨论的[库仑摩擦模型](@entry_id:747944)，描述的是两个表面之间的二维接触行为。其准则 $\boldsymbol{\tau} \le \mu p'$ 直接关联作用在特定平面上的局部法向和切向牵[引力](@entry_id:175476)。这里的 $p'$ 是该平面上的法向[有效应力](@entry_id:198048)，$\boldsymbol{\tau}$ 是切向牵[引力](@entry_id:175476)矢量。对于界面，[摩擦系数](@entry_id:150354) $\mu$ 和摩擦角 $\phi$ 的关系是直接的几何定义：$\mu = \tan\phi$。

尽管两者都可能使用“[有效应力](@entry_id:198048)”和“摩擦角”等术语，但它们的物理含义和数学形式是不同的。体模型中的 $p'$ 是三维[平均应力](@entry_id:751819)，而界面模型中的 $p'$ 是特定平面上的法向应力分量。混淆这两种模型是一个常见的概念错误。

#### 历史依赖与率相关摩擦

经典库仑定律中的[摩擦系数](@entry_id:150354) $\mu$ 是一个常数。然而，实验表明，岩土材料的摩擦系数可以随滑移历史和滑移速率而演化。

**历史依赖性（History Dependence）**的一个常见模型是**滑移弱化（slip-weakening）** [@problem_id:3512345]。在这种模型中，摩擦系数 $\mu$ 是一个内部[状态变量](@entry_id:138790)——**累积滑移量 $\gamma$** 的函数。累积滑移量定义为滑移速率的模量对时间的积分：

$$
\gamma(t) = \int_0^t \|\boldsymbol{v}_t(\tau)\| \, d\tau
$$

它记录了接触点经历的总滑移路径长度，无论滑移方向如何。一个典型的滑移弱化规律是，[摩擦系数](@entry_id:150354)从一个较高的[静摩擦系数](@entry_id:163255) $\mu_s$ 开始，随着累积滑移量的增加而指数衰减，最终趋于一个较低的[动摩擦系数](@entry_id:162794) $\mu_d$：

$$
\mu(\gamma) = \mu_d + (\mu_s - \mu_d) \exp(-\gamma/D_c)
$$

其中 $D_c$ 是一个特征滑移距离，控制着弱化的速率。这类模型对于模拟地震断层破裂、滑坡启动等现象至关重要，因为它们能够捕捉从静态到动态的强度下降过程。

**率相关性（Rate Dependence）**是指[摩擦力](@entry_id:171772)对滑移速率 $\boldsymbol{v}_t$ 的依赖。虽然我们主要讨论的是率无关（rate-independent）模型，但真实的[地质材料](@entry_id:749838)摩擦往往表现出轻微的率相关性，尤其是在[地震学](@entry_id:203510)研究中，这通常通过**率-状态摩擦定律（rate-and-state friction laws）**来描述 [@problem_id:3512289]。

在这种模型中，摩擦系数 $\mu$ 不仅是瞬时滑移速率 $\|\boldsymbol{v}_t\|$ 的函数，还依赖于一个或多个描述界面接触状态的“状态变量”。一个简化的形式是 $\mu = \mu(\|\boldsymbol{v}_t\|)$。率无关的常数 $\mu_0$ 模型可以被视为率相关模型在特定条件下的有效近似。这种近似的适用条件是：在所研究问题涉及的滑移速率范围内，$\mu(\|\boldsymbol{v}_t\|)$ 的变化非常小，即 $|\mu(\|\boldsymbol{v}_t\|) - \mu_0| \ll \mu_0$。这通常发生在准静态、低速滑移的过程中，其中与速率相关的效应（如[摩擦生热](@entry_id:201286)、孔隙压力变化）可以忽略不计。