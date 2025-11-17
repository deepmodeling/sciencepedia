## 引言
在现代工程与科学研究中，准确预测材料和结构在极端载荷下的行为至关重要。当物体经历大位移、大转动和[大应变](@entry_id:751152)时，其响应通常表现出显著的几何与[材料非线性](@entry_id:162855)，传统的线性分析方法将不再适用。更新拉格朗日（Updated Lagrangian, UL）[有限元列式](@entry_id:164720)正是为应对这一挑战而设计的强大计算框架。它通过在每个分析步中更新参考构型，提供了一种物理直观且数学严谨的方式来处理大变形问题，从而成为[计算固体力学](@entry_id:169583)领域不可或缺的工具。

然而，正确实施UL列式需要深入理解其背后的力学原理和数值细节。从如何追踪累积变形，到如何在本构关系中满足物质客观性这一基本物理要求，再到如何构建保证数值高效收敛的[切线刚度矩阵](@entry_id:170852)，每一步都充满了理论挑战。本文旨在系统地梳理这些关键概念，填补理论与实践之间的知识鸿沟。

读者将通过本文学习到：第一章“原理和机制”将深入剖析UL列式的[运动学](@entry_id:173318)、控制方程、[客观应力率](@entry_id:199282)以及[有限元离散化](@entry_id:193156)的核心机制。第二章“应用与[交叉](@entry_id:147634)学科联系”将展示UL列式在解决结构稳定性、先进[材料建模](@entry_id:751724)、多物理场耦合等前沿问题中的强大能力。最后，在“动手实践”部分，通过具体计算练习，读者将能够巩固所学知识，将理论应用于实际问题的解决。

## 原理和机制

在对经历大变形的固体进行数值分析时，必须采用能够系统地处理几何形状显著变化和[材料非线性](@entry_id:162855)行为的计算框架。更新拉格朗日（Updated Lagrangian, UL）列式正是为此类问题设计的核心方法之一。与总是参考初始未变形构型的总拉格朗日（Total Lagrangian, TL）列式不同，UL 列式采用一种更为动态的视角：它将系统在每个增量步开始时的构型（即最新计算出的构型）作为当前计算的参考基准。本章将深入探讨 UL 列式的基本原理和关键机制，从其[运动学](@entry_id:173318)和动力学基础，到[本构关系](@entry_id:186508)的核心要求，再到其在有限元法中的具体实施。

### 更新[拉格朗日视角](@entry_id:265471)：一个移动的参考框架

更新拉格朗日（UL）列式的核心思想在于其“移动参考”的哲学。在求解过程中，时间或载荷被划分为一系列离散的增量步。在每一个增量步中，UL 列式将系统在增量步开始时的已知构型作为计算该步内发生的进一步变形、应变和应力的参考。计算完成后，该增量步结束时的新构型又将成为下一个增量步的参考。这种方法与总拉格朗日（TL）列式形成了鲜明对比，后者在整个分析过程中始终以物体初始的、未变形的构型作为唯一的参考框架。[@problem_id:3608858]

这两种方法的选择并非任意，而是取决于具体问题的物理特性。UL 列式本质上是一种率形式的增量理论，它天然适用于那些[本构关系](@entry_id:186508)以率形式定义的材料，例如[金属塑性](@entry_id:176585)和[粘塑性](@entry_id:165397)。在这些模型中，材料的响应取决于应变率和应力历史，而非仅仅是当前的总应变。此外，对于那些几何边界不断演化的问题，如接触力学或流固耦合，UL 列式也显示出巨大优势，因为在当前构型中处理接触判断和边界条件更新要比将其映射回遥远的初始构型更为直观和高效。[@problem_id:3608858]

另一方面，TL 列式对于[超弹性材料](@entry_id:190241)（如橡胶）的建模则更为直接。这类材料的应力状态可以通过一个定义在初始构型上的[应变能密度函数](@entry_id:755490)（例如，关于[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$ 的函数 $\Psi(\mathbf{E})$）来完全确定。由于所有计算都在一个固定的、不变的初始域上进行，积分和求导操作相对简化。

### 当前构型中的控制方程

UL 列式的数学基础是在当前构型 $\Omega_t$ 中表述的[虚功原理](@entry_id:138749)（或[虚功](@entry_id:176403)率原理）。对于一个处于平衡状态的物体，在任何满足[运动学](@entry_id:173318)约束的虚速度场 $\delta\mathbf{u}$ 下，内力所做的[虚功](@entry_id:176403)率必须等于外力所做的[虚功](@entry_id:176403)率。在忽略惯性效应的准静态情况下，该原理的表达式为：
$$
\int_{\Omega_t} \boldsymbol{\sigma} : \delta\mathbf{d} \, dv = \int_{\Omega_t} \rho \mathbf{b} \cdot \delta\mathbf{u} \, dv + \int_{\partial\Omega_t^t} \overline{\mathbf{t}} \cdot \delta\mathbf{u} \, da
$$
这个方程是 UL 列式的出发点，其中每个量都定义在当前（或更新后的）构型上：[@problem_id:2609717]

*   $\boldsymbol{\sigma}$ 是 **柯西应力张量（Cauchy stress tensor）**，它是一个定义在当前构型中的真实物理应力。
*   $\delta\mathbf{d}$ 是 **虚[应变率张量](@entry_id:266108)（virtual rate of deformation tensor）**，它是虚速度场 $\delta\mathbf{u}$ 在当前空间坐标 $\mathbf{x}$ 下梯度（$\nabla_{\mathbf{x}} \delta \mathbf{u}$）的对称部分。柯西应力 $\boldsymbol{\sigma}$ 和应变率 $\mathbf{d}$ 在当前构型体积积分的意义下是 **[功共轭](@entry_id:194957)（work-conjugate）** 的。
*   $\rho$ 是物体在当前构型下的质量密度。
*   $\mathbf{b}$ 是单位质量所受的体力。
*   $dv$ 和 $da$ 分别是当前构型中的体积和面积微元。
*   $\overline{\mathbf{t}}$ 是在当前构型的自然边界 $\partial\Omega_t^t$ 上施加的、单位当前面积上的面力。

虽然柯西应力是 UL 列式中最自然的应力度量，但为了理论上的完备性或特定本构模型的需要，有时会引入其他应力度量。例如，**[基尔霍夫应力](@entry_id:751039)张量（Kirchhoff stress tensor）** $\boldsymbol{\tau}$ 定义为 $\boldsymbol{\tau} = J \boldsymbol{\sigma}$，其中 $J$ 是变形梯度 $\mathbf{F}$ 的[行列式](@entry_id:142978)。[基尔霍夫应力](@entry_id:751039)与应变率张量 $\mathbf{d}$ 的[功共轭](@entry_id:194957)关系是通过在 *初始* 构型体积上积分来体现的：$\int_{\Omega_0} \boldsymbol{\tau} : \mathbf{d} \, dV$。[@problem_id:3608888] 同样，**第一皮奥拉-基尔霍夫（1st Piola-Kirchhoff, PK1）应力张量** $\mathbf{P}$ 也是一个重要的理论工具，它将初始构型中的名义面力与当前构型中的柯西应力联系起来。值得注意的是，尽管柯西应力是对称的，但 PK1 [应力张量](@entry_id:148973) $\mathbf{P}$ 通常是 *非对称* 的。[@problem_id:3608888]

### 增量[运动学](@entry_id:173318)：追踪变形过程

UL 列式的增量特性要求我们能够精确地追踪从初始构型到当前构型的累积变形。这是通过对变形梯度 $\mathbf{F} = \partial\mathbf{x}/\partial\mathbf{X}$ 的乘法更新来实现的。

考虑从时刻 $t_n$ 的构型 $\Omega_n$ 到时刻 $t_{n+1}$ 的构型 $\Omega_{n+1}$ 的一个增量步。我们可以定义一个 **相对变形梯度（relative deformation gradient）** $\mathbf{f}^n$，它将 $\Omega_n$ 中的向量映射到 $\Omega_{n+1}$ 中：$\mathbf{f}^n = \partial\mathbf{x}^{n+1} / \partial\mathbf{x}^n$。于是，总变形梯度可以通过一个简单的[乘法法则](@entry_id:144424)进行更新：
$$
\mathbf{F}^{n+1} = \mathbf{f}^n \mathbf{F}^n
$$
这个关系式构成了 UL 列式中运动学更新的核心。它表明，从初始构型到最终构型的总变形，可以看作是一系列连续增量步变形的累积结果。[@problem_id:3608926]

那么，如何计算相对变形梯度 $\mathbf{f}^n$ 呢？它与当前构型中的[空间速度梯度](@entry_id:187198) $\mathbf{L} = \nabla_{\mathbf{x}}\mathbf{v} = \dot{\mathbf{F}}\mathbf{F}^{-1}$ 密切相关。通过对关系式 $\dot{\mathbf{F}} = \mathbf{L}\mathbf{F}$ 在时间增量 $\Delta t = t_{n+1} - t_n$ 上进行积分，可以得到 $\mathbf{f}^n$。一个常用且具有[二阶精度](@entry_id:137876)的[数值积分方法](@entry_id:141406)是基于[矩阵指数](@entry_id:139347)映射的[中点法则](@entry_id:177487)：
$$
\mathbf{f}^n \approx \exp\left(\mathbf{L}(t_{n+1/2}) \Delta t\right)
$$
其中 $t_{n+1/2}$ 是增量步的中点时刻。这个公式将连续的率度量（[速度梯度](@entry_id:261686) $\mathbf{L}$）与离散的有限元增量步（相对变形梯度 $\mathbf{f}^n$）联系起来，是实现精确[运动学](@entry_id:173318)更新的关键。[@problem_id:3608926]

### 客观性的挑战：率形式本构关系

在 UL 列式中，[本构关系](@entry_id:186508)通常以率形式给出，即应力率与[应变率](@entry_id:154778)之间的关系。这就引出了连续介质力学中一个深刻而关键的概念：**物质客观性（material objectivity）**，也称为物质[坐标系](@entry_id:156346)无关性。该原理要求[本构方程](@entry_id:138559)必须独立于观察者，即方程的形式不应因观察者自身的刚体运动而改变。

一个直接的推论是，[本构方程](@entry_id:138559)必须仅由客观的张量构成。[应变率张量](@entry_id:266108) $\mathbf{d}$ 是客观的，但柯西应力的简单[物质时间导数](@entry_id:190892) $\dot{\boldsymbol{\sigma}}$ 却 *不是* 客观的。[@problem_id:3608851] 如果我们天真地使用一个形如 $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\mathbf{d}$ 的本构模型（其中 $\mathbb{C}$ 是[弹性张量](@entry_id:170728)），将会导致严重的物理谬误。

为了阐明这一点，考虑一个仅承受[单轴拉伸](@entry_id:188287) $\sigma_0$ 的物体，然后使其绕轴进行刚体旋转。在刚体旋转过程中，物体内部没有发生变形，因此[应变率](@entry_id:154778) $\mathbf{d} = \mathbf{0}$。天真的本构模型会预测 $\dot{\boldsymbol{\sigma}} = \mathbf{0}$，这意味着柯西[应力张量](@entry_id:148973)的分量在固定的空间[坐标系](@entry_id:156346)中保持不变。然而，这显然是错误的。物理上，应力状态应该随着物体一起旋转。这种不正确的应力更新，当在一个随体旋转的[坐标系](@entry_id:156346)（即材料自身的[坐标系](@entry_id:156346)）中观察时，会产生虚假的、非物理的剪切应力。[@problem_id:3608842] 我们可以精确地量化这个虚假剪切应力的大小。对于初始单轴应力 $\sigma_0$ 和旋转角度 $\theta$，在随体[坐标系](@entry_id:156346)中产生的虚假[剪切应力](@entry_id:137139)大小为：
$$
|\tau_{\text{artificial}}| = \frac{1}{2} \sigma_0 |\sin(2\theta)|
$$
这个结果清晰地表明，未使用[客观应力率](@entry_id:199282)会导致在纯旋转下产生人为的应力。[@problem_id:3608842]

解决这一问题的唯一途径是使用 **[客观应力率](@entry_id:199282)（objective stress rate）**。[客观应力率](@entry_id:199282)是一种对柯西应力时间导数的修正，它通过引入 **[自旋张量](@entry_id:187346)（spin tensor）** $\mathbf{W} = \text{skw}(\mathbf{L})$ 来剔除刚体旋转对应力率的贡献。一个广泛使用的[客观应力率](@entry_id:199282)是 **[Jaumann 率](@entry_id:185572)**（或随转率），其定义为：
$$
\overset{\triangle}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\mathbf{W} - \mathbf{W}\boldsymbol{\sigma}
$$
一个客观的率形式本构关系应写为 $\overset{\triangle}{\boldsymbol{\sigma}} = \mathbb{C}:\mathbf{d}$。在刚体旋转（$\mathbf{d}=\mathbf{0}$）的情况下，该模型正确地预测了 $\overset{\triangle}{\boldsymbol{\sigma}} = \mathbf{0}$。这反过来给出了柯西应力在空间中正确的演化方程 $\dot{\boldsymbol{\sigma}} = \mathbf{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\mathbf{W}$，该方程描述了应力张量随物体刚性旋转。[@problem_id:3608851] [@problem_id:3608842]

### 有限元离散与求解流程

将 UL 列式的连续理论应用于[有限元分析](@entry_id:138109)，需要将其离散化并通过迭代[求解非线性方程](@entry_id:177343)组。这一过程中的几个关键机制值得关注。

#### 空间梯度的计算
在[等参单元](@entry_id:173863)中，形函数 $N_a$ 是母单元坐标 $\boldsymbol{\xi}$ 的函数。然而，虚功原理中的[运动学](@entry_id:173318)量（如[应变率](@entry_id:154778) $\mathbf{d}$）需要计算形函数相对于当前空间坐标 $\mathbf{x}$ 的梯度 $\nabla_{\mathbf{x}} N_a$。这通过[链式法则](@entry_id:190743)和当前构型的[雅可比矩阵](@entry_id:264467) $\mathbf{J} = \partial\mathbf{x}/\partial\boldsymbol{\xi}$ 来实现：
$$
\nabla_{\mathbf{x}} N_a = \mathbf{J}^{-1} \nabla_{\boldsymbol{\xi}} N_a
$$
至关重要的是，雅可比矩阵 $\mathbf{J}$ 本身是通过当前构型的节点坐标 $\mathbf{x}_a^{n+1}$ 构建的：$\mathbf{x}(\boldsymbol{\xi}) = \sum_a N_a(\boldsymbol{\xi})\mathbf{x}_a^{n+1}$。因此，$\nabla_{\mathbf{x}} N_a$ 的值在每个迭代步中都会随着节点坐标的更新而改变。这是[几何非线性](@entry_id:169896)的核心体现之一。[@problem_id:3608868]

#### 迭代求解流程
UL 列式产生的非线性方程组通常使用牛顿-拉夫逊（[Newton-Raphson](@entry_id:177436)）法求解。在一个典型的单元子程序中，对于每个牛顿迭代步，其数据流如下：[@problem_id:3608876]
1.  **更新几何**：根据上一步迭代得到的位移修正量，更新单元节点坐标至当前试探构型 $\Omega_{n+1}$。
2.  **高斯积分点循环**：在每个高斯积分点上执行以下操作：
    a. 计算雅可比矩阵 $\mathbf{J}$ 和空间梯度 $\nabla_{\mathbf{x}}N$，并构建离散的运动学矩阵，如[应变-位移矩阵](@entry_id:163451) $\mathbf{B}$ 和[梯度算子](@entry_id:275922)矩阵 $\mathbf{G}$。
    b. 根据增量[运动学](@entry_id:173318)法则，更新总变形梯度 $\mathbf{F}_{n+1}$。
    c. 调用材料本构子程序。输入是变形历史（如 $\mathbf{F}_{n+1}$），输出是当前构型的柯西应力 $\boldsymbol{\sigma}_{n+1}$ 和与所选[客观应力率](@entry_id:199282)相一致的 **空间[切线](@entry_id:268870)模量（spatial tangent modulus）** $\mathbb{c}_{n+1}$。
    d. 计算单元[内力向量](@entry_id:750751) $\mathbf{r}_{\text{int}}$ 和[切线刚度矩阵](@entry_id:170852) $\mathbf{K}$ 的积分项。
3.  **积分与组装**：完成对所有[高斯点](@entry_id:170251)的积分，得到单元的[内力向量](@entry_id:750751)和[切线刚度矩阵](@entry_id:170852)，然后将它们组装到总体系统。
4.  **更新外载荷**：如果外载荷（如压力）是“跟随”变形的，则需要在当前构型上重新计算外[载荷向量](@entry_id:635284) $\mathbf{r}_{\text{ext}}$。

#### 一致性[切线刚度矩阵](@entry_id:170852)
为了使牛顿-拉夫逊法达到其标志性的 **二次收敛（quadratic convergence）** 速度，所使用的[切线刚度矩阵](@entry_id:170852) $\mathbf{K}$ 必须是[残差向量](@entry_id:165091) $\mathbf{r}$ 对节点位移的精确导数，即 **一致性[切线刚度矩阵](@entry_id:170852)（consistent tangent stiffness matrix）**。[@problem_id:2609710] 在[大变形](@entry_id:167243) UL 分析中，该矩阵包含两个部分：
$$
\mathbf{K} = \mathbf{K}_{\text{mat}} + \mathbf{K}_{\text{geo}}
$$

*   **材料刚度矩阵** $\mathbf{K}_{\text{mat}} = \int_{\Omega_{n+1}} \mathbf{B}^T \mathbb{c}_{n+1} \mathbf{B} \, dv$：它源于应力对应变的敏感性，直接依赖于[本构模型](@entry_id:174726)返回的空间[切线](@entry_id:268870)模量 $\mathbb{c}_{n+1}$。

*   **[几何刚度矩阵](@entry_id:162967)（geometric stiffness matrix）** $\mathbf{K}_{\text{geo}}$，也称[初始应力](@entry_id:750652)矩阵：它源于当前应[力场](@entry_id:147325)对几何扰动响应的影响。其形式为：
    $$
    \mathbf{K}_{\text{geo}} = \int_{\Omega_{n+1}} \mathbf{G}^T \boldsymbol{\sigma}_{n+1} \mathbf{G} \, dv
    $$
    其中 $\boldsymbol{\sigma}_{n+1}$ 是当前应力。[@problem_id:3608864]

[几何刚度](@entry_id:172820)的物理意义在[结构稳定性](@entry_id:147935)分析（如[屈曲](@entry_id:162815)）中表现得尤为突出。线性化[屈曲分析](@entry_id:168558)的控制方程正是 $(\mathbf{K}_{\text{mat}} + \alpha \mathbf{K}_{\text{geo}})\boldsymbol{\phi} = \mathbf{0}$，其中 $\alpha$ 是[屈曲](@entry_id:162815)载荷因子。这表明，一个受压的结构（$\boldsymbol{\sigma}$ 为负）会因 $\mathbf{K}_{\text{geo}}$ 的存在而“软化”，最终在某个临界载荷下失去刚度。[@problem_id:3608864]

在迭代求解中，忽略[几何刚度](@entry_id:172820)或使用不精确的（非一致的）[切线](@entry_id:268870)模量，都会导致[切线](@entry_id:268870)矩阵与残差的真实梯度不符，从而将算法从[牛顿法](@entry_id:140116)降级为[修正牛顿法](@entry_id:636309)或[割线法](@entry_id:147486)。这通常会使[收敛速度](@entry_id:636873)从二次降为线性，导致需要更多的迭代次数才能达到[收敛容差](@entry_id:635614)，并且可能需要更小的载荷增量步来保证收敛。对于[超弹性材料](@entry_id:190241)，精确推导的一致性[切线刚度矩阵](@entry_id:170852)是对称的，这一特性可被高效的[线性求解器](@entry_id:751329)利用。[@problem_id:2609710] 因此，在 UL 列式中，从[客观应力率](@entry_id:199282)到一致性[切线刚度矩阵](@entry_id:170852)的每一个环节都至关重要，它们共同确保了求解过程的准确性、鲁棒性和高效性。