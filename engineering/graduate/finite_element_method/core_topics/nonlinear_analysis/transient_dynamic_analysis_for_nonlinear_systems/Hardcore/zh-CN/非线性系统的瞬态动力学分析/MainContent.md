## 引言
在工程与科学的广阔天地中，从航天器再入大气层到生物细胞的力学响应，许多关键现象的本质都是非线性的和瞬态的。非线性系统瞬态动力学分析正是为理解和预测这些复杂过程而生的强大工具，它使我们能够超越静态和线性假设的局限，捕捉现实世界中丰富的动态行为。然而，有效驾驭这一领域要求从业者不仅要掌握其深厚的理论根基，还要洞悉其精密的数值算法和广泛的应用场景。

本文旨在系统地构建从基础原理到前沿应用的知识桥梁。我们将解决从连续介质力学到可计算的离散模型之间的认知鸿沟，并展示这些看似抽象的理论如何在不同学科中转化为解决实际问题的洞见。

为此，文章将分为三个核心部分展开：
- **第一章：原理与机制**，将奠定理论基石。我们将从动量守恒出发，推导动力学控制方程，深入探讨大变形运动学、非线性本构关系、有限元离散化以及隐式与显式时间积分算法的内在机制。
- **第二章：应用与交叉学科联系**，将展示理论的广度与力量。通过一系列精心挑选的案例，我们将探索这些方法在先进结构、材料科学、流固耦合、化学反应乃至生态系统建模中的具体应用，揭示贯穿其中的共通挑战与解决策略。
- **第三章：动手实践**，旨在巩固和深化理解。通过一系列引导性问题，读者将有机会亲手推导关键公式，分析数值方法的特性，从而将理论知识内化为解决问题的实践能力。

通过这一结构化的学习路径，读者将能够全面掌握非线性瞬态动力学分析的核心思想，并有能力将其应用于各自的研究与工程实践之中。

## 原理与机制

本章旨在深入探讨非线性系统瞬态动力学分析的核心原理与关键机制。继前一章对该领域的宏观介绍之后，我们将从连续介质力学的基本定律出发，系统地建立控制方程的弱形式和强形式。随后，我们将详细阐述处理几何非线性（大变形）和材料非线性的关键概念，包括各种运动学描述、应力应变度量以及确保本构关系客观性的应力率。在此基础上，我们将讨论从连续体到离散系统的转化过程，即有限元空间离散化和时间积分算法。我们将重点分析隐式和显式时间积分格式的稳定性、精度和数值特性。最后，本章将探讨两个高级议题：如何在动力学分析中施加约束，以及如何处理因材料软化等现象导致的数学模型不适定性问题。

### 动力学问题的控制方程

任何动力学分析的出发点都是动量守恒定律。对于一个连续体，该定律可以有多种等价的数学表述，其中以虚功原理（弱形式）和局部动量平衡方程（强形式）最为核心。

#### 虚功原理与局部动量平衡

在瞬态动力学分析中，最通用和强大的基础是**达朗贝尔原理 (d'Alembert's principle)**，它本质上是动力学问题的**虚功原理 (principle of virtual work)**。该原理断言，在任意时刻 $t$，对于任意满足运动学约束的虚位移 $\boldsymbol{w}$，惯性力、内力和外力所做的虚功之和为零。这一原理直接导出了控制方程的积分形式（或称弱形式），是有限元方法进行空间离散化的理论基石。

为了更深入地理解各力项的物理来源，我们可以考察动量守恒的局部形式，即强形式。考虑一个在当前时刻 $t$ 占据空间域 $\Omega(t)$ 的连续体。根据牛顿第二定律和柯西应力公设，可以推导出在当前构型（欧拉描述）下的局部线性[动量平衡](@entry_id:193575)方程 [@problem_id:2607406]：

$$
\rho \ddot{\boldsymbol{u}} = \nabla \cdot \boldsymbol{\sigma} + \rho \boldsymbol{b}
$$

此方程中各项的物理意义极为明确：
- $\rho(\boldsymbol{x}, t)$ 是在当前构型下，位置 $\boldsymbol{x}$ 处材料的**质量密度**，单位为单位当前体积的质量。由于体积会随变形而改变，它通常是变形的函数。
- $\ddot{\boldsymbol{u}}$ 是**物质加速度**，即跟随一个物质点（质点）运动所测量到的加速度。它等于物质速度 $\boldsymbol{v}$ 对时间的物质导数 $D\boldsymbol{v}/Dt$。
- $\rho \ddot{\boldsymbol{u}}$ 代表单位当前体积的**惯性力**，是牛顿第二定律 ($F=ma$) 在连续介质中的体现。
- $\boldsymbol{\sigma}$ 是对称的**柯西应力张量 (Cauchy stress tensor)**。它描述了物体内部单位当前面积上的接触力分布，其与作用面法向 $\boldsymbol{n}$ 的关系通过柯西公式 $\boldsymbol{t} = \boldsymbol{\sigma n}$ 给出，其中 $\boldsymbol{t}$ 为面力矢量。
- $\nabla \cdot \boldsymbol{\sigma}$ 是柯西应力张量的**散度**，代表由应力场空间不均匀性引起的单位当前体积的**净内力**。
- $\boldsymbol{b}$ 是单位质量所受的**体力 (body force)**，例如重力加速度 $\boldsymbol{g}$。因此，$\rho \boldsymbol{b}$ 代表单位当前体积的体力。

通过对上述强形式方程乘以一个虚位移（或称为权函数）$\boldsymbol{w}$ 并在当前域 $\Omega(t)$ 上积分，再利用高斯散度定理对内力项进行分部积分，即可重新得到虚功原理的数学表达式，并将不同类型的边界条件清晰地呈现出来。

#### 本质边界条件与自然边界条件

在弱形式的推导过程中，分部积分会产生一个边界积分项 $\int_{\partial \Omega(t)} \boldsymbol{w} \cdot (\boldsymbol{\sigma n}) \, \mathrm{d}a$。这自然地引出了两类边界条件的区分 [@problem_id:2607406]：

1.  **本质边界条件 (Essential Boundary Conditions)**，也称为狄利克雷 (Dirichlet) 型条件。这类条件直接施加在求解的基本变量（在位移法中即为位移 $\boldsymbol{u}$）或其时间导数（速度 $\dot{\boldsymbol{u}}$、加速度 $\ddot{\boldsymbol{u}}$）上。例如，在边界的某一部分 $\partial \Omega_u(t)$ 上规定 $\boldsymbol{u} = \bar{\boldsymbol{u}}(t)$。在有限元方法中，这些条件必须在构建求解空间时就预先满足。与之对应，权函数 $\boldsymbol{w}$ 必须在这些边界上为零。

2.  **自然边界条件 (Natural Boundary Conditions)**，也称为诺伊曼 (Neumann) 型条件。这类条件是通过弱形式的边界积分项来施加的。最常见的例子是在边界的另一部分 $\partial \Omega_t(t)$ 上规定面力 $\bar{\boldsymbol{t}}(t)$。通过柯西公式 $\boldsymbol{t} = \boldsymbol{\sigma n}$，这个已知的面力 $\bar{\boldsymbol{t}}$ 可以直接替换边界积分中的项 $\boldsymbol{\sigma n}$。这类条件是“自然”出现的，并在积分意义上得到满足，而不是在离散化的初始阶段就强行施加。

#### 变分原理的比较

除了达朗贝尔原理，另一个著名的变分原理是**哈密顿原理 (Hamilton's principle)**。该原理指出，对于一个保守系统，在两个时间点 $t_0$ 和 $t_1$ 之间，其真实运动路径使得作用量泛函 $S = \int_{t_0}^{t_1} L \, dt$ 取驻值。其中 $L = T - V$ 是拉格朗日量，即动能 $T$ 与势能 $V$之差。

在理想条件下（如双弹性材料、无耗散、无非保守外力），哈密顿原理与达朗贝尔原理是等价的。然而，达朗贝尔原理具有更广泛的适用性 [@problem_id:2607435]。当系统存在非保守力（如黏性阻尼、流体-结构相互作用产生的追随力）或耗散过程（如塑性）时，经典的哈密顿原理不再适用，因为它无法从一个标量势能函数中导出这些力。相比之下，达朗贝尔原理（虚功原理）可以轻易地将这些非保守力的虚功项包含在内，例如，通过在虚功方程中加入 $\delta W_{nc} = \int_{\Omega} \boldsymbol{w} \cdot \boldsymbol{f}_{nc} \, dV$。因此，在处理复杂的、包含各类非线性效应的工程实际问题时，基于虚功原理的表述是更为通用和直接的出发点。

### 大变形运动学与本构模型

非线性动力学问题的非线性来源主要有两个：**几何非线性**（因大位移、大转动、大应变引起的运动学关系非线性化）和**材料非线性**（应力-应变关系的非线性）。

#### 拉格朗日描述与欧拉描述

为了精确描述大变形，我们需要区分两种坐标系：
- **材料坐标系（拉格朗日描述, Lagrangian description）**: 质点的位置用其在初始参考构型 $\Omega_0$ 中的坐标 $\boldsymbol{X}$ 来标记。所有物理量都表示为 $\boldsymbol{X}$ 和时间 $t$ 的函数。
- **空间坐标系（欧拉描述, Eulerian description）**: 物理量在当前时刻 $t$ 的空间位置 $\boldsymbol{x}$ 处进行描述。

连接这两个描述的核心是**变形梯度 (deformation gradient)** $\boldsymbol{F}$ [@problem_id:2607416]：
$$
\boldsymbol{F} = \frac{\partial \boldsymbol{x}}{\partial \boldsymbol{X}}
$$
$\boldsymbol{F}$ 衡量了材料微元的局部变形（拉伸和旋转）。基于 $\boldsymbol{F}$，可以定义一系列应变度量。在拉格朗日描述中，最常用的是**格林-拉格朗日应变张量 (Green-Lagrange strain tensor)** $\boldsymbol{E}$：
$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{F}^{\top}\boldsymbol{F} - \boldsymbol{I})
$$
$\boldsymbol{E}$ 的一个重要特性是它对刚体转动不敏感，即纯刚体转动下 $\boldsymbol{E}=\boldsymbol{0}$。

在欧拉描述中，我们关注的是变形的“率”。**速度梯度张量 (velocity gradient tensor)** $\boldsymbol{l} = \nabla_{\boldsymbol{x}}\boldsymbol{v}$ 描述了速度场的空间变化。它的对称部分是**变形率张量 (rate-of-deformation tensor)** $\boldsymbol{d}$，反对称部分是**自旋张量 (spin tensor)** $\boldsymbol{W}$：
$$
\boldsymbol{d} = \frac{1}{2}(\boldsymbol{l} + \boldsymbol{l}^{\top}), \quad \boldsymbol{W} = \frac{1}{2}(\boldsymbol{l} - \boldsymbol{l}^{\top})
$$
$\boldsymbol{d}$ 描述了材料微元在当前构型下的变形速率。这些应变率度量之间存在精确的转换关系，例如，格林-拉格朗日应变率 $\dot{\boldsymbol{E}}$ 与 $\boldsymbol{d}$ 的关系为 $\dot{\boldsymbol{E}} = \boldsymbol{F}^{\top}\boldsymbol{d}\boldsymbol{F}$ [@problem_id:2607416]。

#### 应力度量与功共轭关系

与不同的应变度量相对应，也需要引入不同的应力度量，以确保内力功（或功率）的表达形式在不同描述下保持一致。这种关系称为**功共轭 (work conjugacy)**。
- 在欧拉描述下，单位当前体积的内力功率密度由柯西应力 $\boldsymbol{\sigma}$ 和变形率张量 $\boldsymbol{d}$ 的收缩给出：$\boldsymbol{\sigma} : \boldsymbol{d}$。
- 在拉格朗日描述下，单位参考体积的内力功率密度由**第二皮奥拉-基尔霍夫应力张量 (2nd Piola-Kirchhoff stress tensor)** $\boldsymbol{S}$ 和格林-拉格朗日应变率 $\dot{\boldsymbol{E}}$ 的收缩给出：$\boldsymbol{S} : \dot{\boldsymbol{E}}$。

通过功率恒等原则，可以建立不同应力度量之间的转换关系。例如，柯西应力 $\boldsymbol{\sigma}$ 和第二PK应力 $\boldsymbol{S}$ 之间的关系为 [@problem_id:2607416]：
$$
\boldsymbol{\sigma} = \frac{1}{J} \boldsymbol{F} \boldsymbol{S} \boldsymbol{F}^{\top}
$$
其中 $J = \det(\boldsymbol{F})$ 是变形的雅可比行列式，代表了局部体积变化率。

#### 客观应力率

当处理材料非线性，特别是对于采用率形式本构关系的模型（如许多塑性、黏塑性模型），一个关键问题是确保本构律满足**物质客观性原理 (principle of material objectivity)**。该原理要求本构关系在任意叠加的刚体运动（观察者变换）下形式不变。

柯西应力 $\boldsymbol{\sigma}$ 的物质时间导数 $\dot{\boldsymbol{\sigma}}$ 并不是客观的，因为它包含了刚体转动的影响。直接使用如 $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{d}$ 这样的本构关系是错误的，因为它会在纯刚体转动（此时 $\boldsymbol{d}=\boldsymbol{0}$）时错误地预测应力不变，而实际上应力张量应该随物体一起转动 [@problem_id:2607442]。

为了解决这个问题，必须使用**客观应力率 (objective stress rate)**，记作 $\stackrel{\circ}{\boldsymbol{\sigma}}$。客观应力率从物质导数中移除了刚体转动的影响。一种常见的客观率是共转率，其通用形式为 $\stackrel{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}_{\text{spin}}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}_{\text{spin}}$，其中 $\boldsymbol{W}_{\text{spin}}$ 是一个合适的自旋张量。两种常见的选择是：
1.  **Jaumann 率**: 使用速度梯度的反对称部分，即自旋张量 $\boldsymbol{W}$。
2.  **Green-Naghdi 率**: 使用由极分解 $\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$ 中得到的材料转动张量 $\boldsymbol{R}$ 所定义的自旋 $\boldsymbol{\Omega}=\dot{\boldsymbol{R}}\boldsymbol{R}^{\top}$。

对于纯刚体转动，$\boldsymbol{W}$ 和 $\boldsymbol{\Omega}$ 是相等的，两种率都能正确地预测应力为零增长，保证了在无变形情况下的客观性。但在包含剪切变形的复杂流动中，$\boldsymbol{W}$ 和 $\boldsymbol{\Omega}$ 存在差异。例如，在简单剪切流动中，使用Jaumann率的亚弹性模型会预测出非物理的应力振荡，而Green-Naghdi率则不会，因为它更准确地追踪了材料主拉伸方向的转动 [@problem_id:2607442]。因此，在具有大转动和持续变形的非线性动力学分析中，选择合适的客观率至关重要。

### 离散化与求解方法

将连续介质动力学问题转化为可计算的代数方程组，需要经过空间和时间两个层面的离散化。

#### 有限元半离散化与内力向量

有限元法的核心思想是，在每个单元内，用一组基于节点值的形函数来近似位移场：$\boldsymbol{u}(\boldsymbol{X}, t) \approx \sum_a N_a(\boldsymbol{X}) \boldsymbol{d}_a(t)$。将此近似代入系统的虚功原理表达式中，并考虑到虚位移的任意性，最终可以得到一个常微分方程组（ODE），称为**半离散系统**：
$$
\boldsymbol{M}\ddot{\boldsymbol{d}}(t) + \boldsymbol{f}_{\mathrm{int}}(\boldsymbol{d}, \dot{\boldsymbol{d}}) = \boldsymbol{f}_{\mathrm{ext}}(t)
$$
- $\boldsymbol{d}(t)$ 是所有节点自由度的列向量。
- $\boldsymbol{M}$ 是**质量矩阵**，通常通过对密度和形函数积分得到。
- $\boldsymbol{f}_{\mathrm{ext}}$ 是**外力向量**，由体力及自然边界条件贡献。
- $\boldsymbol{f}_{\mathrm{int}}$ 是**内力向量**，它源于内力虚功项，并且是位移 $\boldsymbol{d}$ 的非线性函数，体现了系统的几何与材料非线性。

对于一个由应变能密度函数 $W(\boldsymbol{F})$ 定义的超弹性材料，其节点 $a$ 处的内力向量 $\boldsymbol{f}_{\mathrm{int}, a}$ 可以从内力虚功 $\delta W_{\mathrm{int}} = \int_{\Omega_0} \boldsymbol{P}:\delta\boldsymbol{F} \, d\Omega_0$ 推导得出 [@problem_id:2607434]：
$$
\boldsymbol{f}_{\mathrm{int}, a}(\boldsymbol{d}) = \int_{\Omega_0} \boldsymbol{P}(\boldsymbol{F}(\boldsymbol{d})) \nabla_0 N_a(\boldsymbol{X}) \, d\Omega_0 = \int_{\Omega_0} \frac{\partial W(\boldsymbol{F})}{\partial \boldsymbol{F}} \nabla_0 N_a(\boldsymbol{X}) \, d\Omega_0
$$
其中 $\boldsymbol{P} = \partial W / \partial \boldsymbol{F}$ 是**第一皮奥拉-基尔霍夫应力 (1st Piola-Kirchhoff stress)**。这个积分通常通过在每个单元上进行高斯数值积分来计算。

#### 数值时间积分

半离散方程是一个二阶常微分方程组。为了求解它，需要采用时间积分算法，将其在时间域上离散化。时间积分算法大致分为两类：

- **隐式 (Implicit) 算法**: 求解 $t_{n+1}$ 时刻的状态需要用到 $t_{n+1}$ 时刻的未知量（如加速度 $a_{n+1}$），因此每个时间步都需要求解一个（通常是非线性的）代数方程组。
- **显式 (Explicit) 算法**: $t_{n+1}$ 时刻的状态完全由 $t_n$ 时刻及之前的已知量确定，无需迭代求解方程组。

**Newmark 方法族** 是一类广泛应用的隐式/显式积分格式，其通过两个参数 $(\beta, \gamma)$ 来控制精度和稳定性。对一个无阻尼线性振子 $\ddot{u} + \omega^2 u = 0$ 进行稳定性分析表明，为了使算法对任意大小的时间步长 $\Delta t$ 都保持稳定（即**无条件稳定**），Newmark参数必须满足 [@problem_id:2607402]：
$$
\gamma \ge \frac{1}{2} \quad \text{and} \quad \beta \ge \frac{\gamma}{2}
$$
例如，平均加速度法（$\gamma=1/2, \beta=1/4$）是无条件稳定且不引入数值耗散的二阶精度方法，非常适合模拟保守系统的动力学。

然而，在许多非线性问题中，由于接触、材料非线性或网格畸变，会激发虚假的、物理上不存在的高频振荡。这些振荡会污染求解结果，甚至导致数值不稳定。为了抑制这些高频噪声，人们希望算法能具有**可控的数值耗散 (controllable numerical dissipation)**。**广义-$\alpha$ (Generalized-$\alpha$) 方法** 就是为此设计的先进算法 [@problem_id:2607415]。它通过引入参数 $\rho_{\infty} \in [0, 1]$ 来精确控制算法在高频极限下的能量衰减率。可以证明，在每个时间步，高频部分的能量会被衰减一个因子 $\rho_{\infty}^2$。当 $\rho_{\infty}=1$ 时，算法无耗散；当 $\rho_{\infty}1$ 时，算法能有效滤除高频噪声，同时保持对低频物理响应的二阶精度。这一特性使其在求解复杂的非线性动力学问题时非常鲁棒。

与隐式方法不同，显式方法（如中心差分法，即Newmark族中 $\gamma=1/2, \beta=0$ 的特例）是**有条件稳定**的。其稳定性要求时间步长 $\Delta t$ 必须小于一个临界值 $\Delta t_{\text{crit}}$。这个限制来源于**Courant-Friedrichs-Lewy (CFL) 条件**，它要求数值信息的传播速度不能超过物理波的传播速度。对于一个有限元网格，这意味着 $\Delta t$ 必须小于波穿越网格中最“苛刻”单元所需的时间 [@problem_id:2607428]：
$$
\Delta t_{\text{crit}} \approx \min_{e} \left( \frac{L_e}{c} \right)
$$
其中 $L_e$ 是单元的特征长度，$c$ 是材料中的最大波速。在非线性分析中，波速 $c$ 取决于材料的瞬时**切线模量**，因此是随状态变化的。
- **材料硬化**：切线模量增加，波速 $c$ 变大，导致 $\Delta t_{\text{crit}}$ 减小。
- **弹塑性**：进入塑性区后，切线模量通常小于弹性模量，波速降低，这可能允许更大的稳定时间步。
- **近不可压材料**：体积模量 $K$ 远大于剪切模量 $G$，导致压力波速 $c_p = \sqrt{(K+4/3G)/\rho}$ 极大，从而使 $\Delta t_{\text{crit}}$ 变得非常小。这是显式方法处理近不可压问题时遇到的一个严重困难。

### 高级议题：约束与材料不稳定性

在实际工程应用中，我们常常需要处理额外的复杂性，如部件间的接触约束和材料本身的失效行为。

#### 约束的施加方法

许多动力学系统包含**完整约束 (holonomic constraints)**，即形如 $\boldsymbol{g}(\boldsymbol{d}, t) = \boldsymbol{0}$ 的代数方程。例如，刚性接触要求两物体间的距离不能为负。施加这些约束有几种主流方法 [@problem_id:2607430]：

1.  **罚函数法 (Penalty Method)**: 这是一种近似方法，它在系统的势能中增加一个罚项 $\frac{1}{2}\gamma \boldsymbol{g}^T\boldsymbol{g}$，其中 $\gamma$ 是一个很大的罚参数。这等效于在违反约束时施加一个与违反程度成正比的“弹力”。优点是简单，不改变原方程组的结构。缺点是：(1) 约束只能近似满足，精度与 $\gamma$ 的大小成反比；(2) 当 $\gamma$ 趋于无穷大时，系统刚度矩阵的[条件数](@entry_id:145150)会急剧恶化，导致求解困难；(3) 在显式动力学中，巨大的罚刚度会引入极高的频率，导致稳定时间步长 $\Delta t_{crit}$ 急剧减小 [@problem_id:2607430]。

2.  **拉格朗日乘子法 (Lagrange Multiplier Method)**: 这种方法引入一个新的未知量向量——拉格朗日乘子 $\boldsymbol{\lambda}$，它物理解释为维持约束所需的力。通过求解一个增广的方程组，可以精确满足约束条件 $\boldsymbol{g}=\boldsymbol{0}$。优点是精度高。缺点是：(1) 增加了未知量；(2) 得到的线性化系统刚度矩阵是对称不定的（鞍点问题），需要特殊的求解器。但它不会向原始系统引入虚假的刚度，因此对显式时间步长的影响较小 [@problem_id:2607430]。

3.  **增广拉格朗日法 (Augmented Lagrangian Method)**: 该方法结合了前两者的优点。它既引入了拉格朗日乘子，又保留了一个有限大小的罚参数。通过一个迭代过程（在每个时间步内进行），交替求解位移和更新乘子，最终可以精确满足约束，同时避免了纯罚函数法因罚参数过大导致的病态问题。这是一种在精度和鲁棒性之间取得良好平衡的先进方法。

#### 材料软化与正则化

在模拟材料损伤和断裂时，本构模型常常会表现出**应变软化 (strain softening)**，即在达到峰值应力后，应力随应变的增加而减小。这对应于一个负的切线模量 $E_t  0$。对于标准的局部连续介质模型，应变软化会导致灾难性的数学和物理后果 [@problem_id:2607421]。

在线性化分析中，当 $E_t  0$ 时，控制运动的偏微分方程 $\rho \ddot{u} = E_t u_{,xx}$ 的性质从双曲型（描述波动）变为椭圆型。这意味着波速变为虚数，扰动将以指数形式增长，而不是传播。更严重的是，扰动的增长率与波数成正比，意味着波长越短的扰动增长越快。这导致了数学上的**不适定性 (ill-posedness)**：解不再连续依赖于初始条件。

在有限元模拟中，这种不适定性表现为**病态的网格依赖性 (pathological mesh dependency)**。应变会无限地集中在网格所能分辨的最小区域内（通常是一个单元的宽度），形成一个宽度为零的应变局部化带。随着网格的细化，计算出的总耗散能会趋于零，这与物理实验结果严重不符。单纯地细化网格并不能解决问题，反而会使这种病态行为更加显著 [@problem_id:2607421]。

要解决这个问题，必须对原始的局部模型进行**正则化 (regularization)**，即引入一个**内禀长度尺度 (internal length scale)**，从而使得极短波长的模式被抑制。常用的正则化方法包括：
- **率相关模型**: 引入黏性或率相关性，例如在应力中加入黏性项 $\eta \dot{\varepsilon}$。这会使得高频（短波长）模式的增长率受到抑制，趋于一个有限值，从而恢复问题的适定性 [@problem_id:2607421]。
- **非局部或梯度模型**: 在本构关系中引入应变梯度项，例如，能量密度不仅依赖于应变 $\varepsilon$，还依赖于其梯度 $\nabla\varepsilon$。这同样引入了一个长度尺度，可以有效地限制局部化带的宽度，使其成为一个有物理意义的有限值，从而得到网格无关的客观结果。

总之，在进行涉及材料失效的非线性动力学模拟时，必须认识到标准局部软化模型的内在缺陷，并采用经过正则化的、物理上更完备的本构理论，以确保计算结果的有效性和可靠性。