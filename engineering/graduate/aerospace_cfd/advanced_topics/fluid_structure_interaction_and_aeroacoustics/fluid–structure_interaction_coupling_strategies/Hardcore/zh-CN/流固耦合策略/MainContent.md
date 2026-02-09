## 引言
流固耦合（Fluid-structure Interaction, FSI）是描述变形固体与内部或外部流场相互作用的物理现象，它在航空航天工程、生物力学、土木工程等众多前沿领域中扮演着核心角色。从飞机机翼在高速气流中的颤振，到心脏瓣膜在血流驱动下的开合，精确预测并理解这些复杂的相互作用对于工程设计的安全性、效率以及科学探索的深度至关重要。然而，在数值上模拟这种耦合行为极具挑战性，其核心困难在于如何高效、稳定且精确地求解由性质迥异的流体和固体子系统组成的统一问题。

本文旨在系统性地阐述和解析解决这一挑战的各种耦合策略。我们将深入探讨不同的数值方法，揭示其背后的物理原理和数学机制，并展示它们在实际问题中的应用与权衡。通过学习本文，读者将能够理解不同耦合策略的适用边界，并掌握评估其性能的关键准则。

为了实现这一目标，我们将分三章展开讨论。首先，在**“原理与机制”**一章中，我们将建立流固耦合问题的数学框架，详细剖析整体式与分离式两大耦合策略，并深入探讨如任意拉格朗日-欧拉（ALE）方法、附加质量不稳定性以及能量守恒等核心机制。接着，在**“应用与跨学科交叉”**一章中，我们将通过航空航天、生物医学等领域的具体案例，展示这些策略在解决实际工程问题中的强大能力，并探讨其与湍流建模、不确定性量化和机器学习等先进领域的交叉融合。最后，**“动手实践”**部分将通过一系列引导性问题，帮助读者巩固对附加质量、数值稳定性等关键概念的理解。

## 原理与机制

流固耦合（FSI）问题的数值求解核心在于精确且稳定地处理流体和固体两个子系统之间复杂的相互作用。上一章介绍了流固耦合的背景和重要性，本章将深入探讨其核心的物理原理和数值机制。我们将首先建立耦合系统的数学描述，然后探讨求解这些方程的两种主要策略：整体式（monolithic）和分离式（partitioned）方法。随后，我们将详细分析处理移动边界的关键技术——任意拉格朗日-欧拉（ALE）方法，并讨论其对几何守恒和网格质量的严格要求。最后，我们将剖析分离式方案中一个臭名昭著的数值不稳定性——附加质量不稳定性，并阐述保证数值能量守恒的基本原则。

### 耦合FSI问题：控制方程与界面条件

一个典型的流固耦合问题的数学模型由各自域内的控制方程和连接它们的界面条件组成。为了清晰地阐述这些原理，我们考虑一个规范的FSI系统：一个不可压缩的牛顿流体与一个线性弹性固体相互作用 [@problem_id:3959286]。

**流体域方程**

流体通常在随时间变化的欧拉域 $\Omega_{f}(t)$ 中进行描述。其运动由不可压缩的Navier-Stokes方程组控制，包括动量守恒和质量守恒（不可压缩性约束）：

$$
\rho_{f}\left(\frac{\partial \boldsymbol{u}_{f}}{\partial t}+(\boldsymbol{u}_{f}\cdot\nabla)\boldsymbol{u}_{f}\right)=\nabla\cdot\boldsymbol{\sigma}_{f}+\rho_{f}\boldsymbol{b}_{f}
$$

$$
\nabla\cdot\boldsymbol{u}_{f}=0
$$

其中，$\rho_{f}$ 是流体密度，$\boldsymbol{u}_{f}$ 是流体速度矢量，$\boldsymbol{b}_{f}$ 是单位质量的体积力。左侧的 $\frac{\partial \boldsymbol{u}_{f}}{\partial t}+(\boldsymbol{u}_{f}\cdot\nabla)\boldsymbol{u}_{f}$ 是流体速度的物质导数，描述了流体微团的加速度。$\boldsymbol{\sigma}_{f}$ 是流体的柯西应力张量。对于不可压缩牛顿流体，其本构关系为：

$$
\boldsymbol{\sigma}_{f}=-p\boldsymbol{I}+2\mu_{f}\boldsymbol{\varepsilon}(\boldsymbol{u}_{f})
$$

这里，$p$ 是流体压力，$\boldsymbol{I}$ 是单位张量，$\mu_{f}$ 是流体动力粘度。$\boldsymbol{\varepsilon}(\boldsymbol{u}_{f})$ 是应变率张量，定义为速度梯度的对称部分：$\boldsymbol{\varepsilon}(\boldsymbol{u}_{f}) = \frac{1}{2}(\nabla\boldsymbol{u}_{f}+(\nabla\boldsymbol{u}_{f})^{\mathsf{T}})$。压力项 $-p\boldsymbol{I}$ 代表各向同性的压力作用，而粘性项 $2\mu_{f}\boldsymbol{\varepsilon}(\boldsymbol{u}_{f})$ 则描述了由流体变形速率引起的偏应力。

**固体域方程**

固体力学的描述通常采用拉格朗日框架，在固定的参考域 $\Omega_{s}$ 上跟踪物质点的位移 $\boldsymbol{d}$。其动力学行为由动量守恒方程（牛顿第二定律）描述：

$$
\rho_{s}\frac{\partial^{2}\boldsymbol{d}}{\partial t^{2}}=\nabla\cdot\boldsymbol{\sigma}_{s}+\rho_{s}\boldsymbol{b}_{s}
$$

其中，$\rho_{s}$ 是固体密度，$\boldsymbol{b}_{s}$ 是单位质量的体积力，$\boldsymbol{\sigma}_{s}$ 是固体的柯西应力张量。对于线性各向同性弹性体，在小应变假设下，应力-应变关系遵循胡克定律，可以用拉梅参数 $\lambda_{s}$ 和 $\mu_{s}$ 表示：

$$
\boldsymbol{\sigma}_{s}=2\mu_{s}\boldsymbol{\varepsilon}(\boldsymbol{d})+\lambda_{s}\mathrm{tr}(\boldsymbol{\varepsilon}(\boldsymbol{d}))\boldsymbol{I}
$$

这里的 $\boldsymbol{\varepsilon}(\boldsymbol{d})$ 是无穷小应变张量，定义为位移梯度的对称部分：$\boldsymbol{\varepsilon}(\boldsymbol{d}) = \frac{1}{2}(\nabla\boldsymbol{d}+(\nabla\boldsymbol{d})^{\mathsf{T}})$。

**界面条件**

流体域和固体域通过共享的移动界面 $\Gamma(t)$ 耦合在一起。在这个界面上，必须强制执行两个基本的物理条件，它们是整个FSI问题的核心 [@problem_id:3959286]。

1.  **运动学条件 (Kinematic Condition)**：此条件要求界面上物质的连续性。对于粘性流，无滑移条件规定流体在界面上的速度必须与固体在该点的速度完全相同。由于固体点的速度是其位移的时间导数，该条件表示为：
    $$
    \boldsymbol{u}_{f}=\frac{\partial \boldsymbol{d}}{\partial t} \quad \text{on } \Gamma(t)
    $$
    对于无粘流，通常只要求法向速度连续，即无穿透条件。

2.  **动力学条件 (Dynamic Condition)**：此条件源于牛顿第三定律（作用力与反作用力原理），要求在界面上达到牵引力平衡。流体作用在固体上的力必须与固体作用在流体上的力大小相等、方向相反。牵引力矢量定义为应力张量与界面法向量的乘积，$\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$。若定义 $\boldsymbol{n}_{f}$ 为流体域的外法向量，$\boldsymbol{n}_{s}$ 为固体域的外法向量（在界面上 $\boldsymbol{n}_{f} = -\boldsymbol{n}_{s}$），则牵引力平衡可写作：
    $$
    \boldsymbol{\sigma}_{f}\boldsymbol{n}_{f}+\boldsymbol{\sigma}_{s}\boldsymbol{n}_{s}=\boldsymbol{0} \quad \text{on } \Gamma(t)
    $$
    这确保了跨越界面的动量通量是守恒的。

这套完整的方程组——两个域的控制方程加上两个界面条件——构成了FSI问题的连续介质力学描述。数值求解的目标就是找到满足这一整套方程组的离散解。

### 耦合策略：整体式与分离式方法

求解上述高度非线性的耦合方程组，主要有两种策略：整体式（Monolithic）方法和分离式（Partitioned）方法 [@problem_id:3959268]。

**整体式方法**

整体式方法将流体和固体的未知量（如流体速度、压力和固体位移）组合成一个单一的、巨大的未知向量 $\boldsymbol{U} = [\boldsymbol{x}_f, \boldsymbol{x}_s]^{\top}$。然后，将流体和固体的离散控制方程以及界面条件作为一个统一的非线性代数系统在每个时间步内同时求解：

$$
\boldsymbol{R}(\boldsymbol{U}^{n+1}) = \begin{pmatrix} \boldsymbol{R}_f(\boldsymbol{x}_f^{n+1}, \boldsymbol{x}_s^{n+1}) \\ \boldsymbol{R}_s(\boldsymbol{x}_f^{n+1}, \boldsymbol{x}_s^{n+1}) \\ \boldsymbol{R}_c(\boldsymbol{x}_f^{n+1}, \boldsymbol{x}_s^{n+1}) \end{pmatrix} = \boldsymbol{0}
$$

这里 $\boldsymbol{R}_f$ 和 $\boldsymbol{R}_s$ 分别代表流体和固体的离散残差，$\boldsymbol{R}_c$ 代表离散的界面耦合条件。这个大型非线性系统通常通过牛顿类方法求解，其线性化的雅可比矩阵具有鲜明的块结构：

$$
\begin{pmatrix} \frac{\partial \boldsymbol{R}_f}{\partial \boldsymbol{x}_f} & \frac{\partial \boldsymbol{R}_f}{\partial \boldsymbol{x}_s} \\ \frac{\partial \boldsymbol{R}_s}{\partial \boldsymbol{x}_f} & \frac{\partial \boldsymbol{R}_s}{\partial \boldsymbol{x}_s} \end{pmatrix} \begin{pmatrix} \Delta \boldsymbol{x}_f \\ \Delta \boldsymbol{x}_s \end{pmatrix} = - \begin{pmatrix} \boldsymbol{R}_f \\ \boldsymbol{R}_s \end{pmatrix}
$$

非对角块 $\frac{\partial \boldsymbol{R}_f}{\partial \boldsymbol{x}_s}$ 和 $\frac{\partial \boldsymbol{R}_s}{\partial \boldsymbol{x}_f}$ 体现了流体和固体之间的双向耦合。前者主要源于运动学条件（流体域的运动依赖于固体位移），后者源于动力学条件（固体载荷依赖于流体压力和粘性力）。

对于不匹配的界面网格，运动学条件通常通过拉格朗日乘子法强制执行，此时未知向量会增加拉格朗日乘子项 $\boldsymbol{\lambda}$，代表界面上的约束力 [@problem_id:3959268]。整体式方法的主要优点是其出色的**数值稳定性**。由于它在代数层面完全隐式地处理了耦合，因此对于强耦合问题，特别是那些由“附加质量效应”（后文详述）主导的问题，表现得非常鲁棒。其缺点在于需要开发和维护复杂的、高度集成的求解器，且内存消耗和计算成本较高。

**分离式方法**

分离式方法采用“分而治之”的策略。它利用现有的、独立的流体和固体求解器，通过在每个时间步内迭代交换界面数据来满足耦合条件。这种方法在软件工程上更具模块性和灵活性。

一个经典的分离式方案是**狄利克雷-诺依曼（Dirichlet-Neumann, DN）**划分 [@problem_id:3959302]。在一个耦合迭代步中：
1.  **结构求解器** 将预测或计算得到的界面位移（或速度）传递给流体求解器。
2.  **流体求解器** 将此位移/速度作为运动边界，即**狄利克雷（Dirichlet）**类型的边界条件，来求解流场。
3.  求解完成后，流体求解器计算出作用在界面上的压力和粘性力，即牵引力。
4.  这个牵引力被作为载荷，即**诺依曼（Neumann）**类型的边界条件，传递给结构求解器。
5.  **结构求解器** 在此载荷作用下计算新的位移，完成一次迭代。

这个过程在代数上等价于对整体式系统的雅可比矩阵进行块高斯-赛德尔（Block Gauss-Seidel）或块雅可比（Block Jacobi）迭代 [@problem_id:3959268]。根据在一个时间步内执行数据交换的次数，分离式方法可分为：

-   **弱耦合（Weak/Explicit Coupling）**：每个时间步只执行一次数据交换。这种方法实现简单，计算成本低，但对于强耦合问题（如轻质结构在密实流体中的运动）往往数值不稳定。
-   **强耦合（Strong/Implicit Coupling）**：在每个时间步内执行多次上述的子迭代，直到界面上的量（如位移和力）收敛到某个容差范围内。当子迭代收敛时，其解与整体式方法在相同离散化下的解是相同的，因此也能获得相似的稳定性和精度 [@problem_id:3959268]。

分离式方法的主要挑战在于确保子迭代的收敛性和稳定性，尤其是在存在显著附加质量效应的情况下。

### 核心机制 I：通过任意拉格朗日-欧拉（ALE）框架适应运动

在FSI中，流体域的边界是移动的，这给使用传统欧拉方法的流体求解器带来了困难。任意拉格朗日-欧拉（ALE）方法是解决这一问题的标准框架 [@problem_id:3959304]。

ALE引入了一个独立的参考构型（通常是初始的、未变形的网格），其坐标为 $\boldsymbol{X}$。物理空间中随时间变化的坐标为 $\boldsymbol{x}$。ALE方法定义了一个从参考域到物理域的映射 $\boldsymbol{x} = \boldsymbol{\chi}(\boldsymbol{X}, t)$。流体网格的节点可以独立于流体质点运动。网格本身的速度，即**网格速度** $\boldsymbol{a}$，定义为保持参考坐标 $\boldsymbol{X}$ 不变时物理坐标 $\boldsymbol{x}$ 的变化率：

$$
\boldsymbol{a}(\boldsymbol{X}, t) = \frac{\partial \boldsymbol{\chi}(\boldsymbol{X}, t)}{\partial t}\bigg|_{\boldsymbol{X}}
$$

ALE框架下的守恒方程需要考虑网格运动带来的额外通量。描述映射局部变形的量是**变形梯度张量** $\boldsymbol{F} = \frac{\partial \boldsymbol{\chi}}{\partial \boldsymbol{X}}$，其行列式 $J = \det(\boldsymbol{F})$ 衡量了局部体积的变化率。$J>0$ 是维持网格有效性的基本要求。

在ALE框架下，积分形式的质量守恒方程变为：

$$
\frac{\partial (J \rho)}{\partial t}\bigg|_{\boldsymbol{X}} + \nabla_{\boldsymbol{X}} \cdot \big(J \rho\,\boldsymbol{F}^{-1}(\boldsymbol{u} - \boldsymbol{a})\big) = 0
$$

这里的关键是引入了流体相对于网格的对流通量，由相对速度 $(\boldsymbol{u} - \boldsymbol{a})$ 驱动。在流固耦合界面上，为了保证网格与固体边界贴合，网格速度必须等于结构速度，即 $\boldsymbol{a} = \boldsymbol{v}_s$。同时，无穿透的物理条件要求流体法向速度等于结构法向速度，$\boldsymbol{u} \cdot \boldsymbol{n} = \boldsymbol{v}_s \cdot \boldsymbol{n}$。因此，在界面上，法向相对速度为零，$(\boldsymbol{u} - \boldsymbol{a}) \cdot \boldsymbol{n} = 0$，这意味着没有质量穿过移动的界面，这与物理现实相符，并且该结论与切向滑移无关 [@problem_id:3959304]。

**几何守恒律 (Geometric Conservation Law, GCL)**

在ALE数值模拟中，一个至关重要的一致性条件是**几何守恒律（GCL）** [@problem_id:3959266]。GCL本身不是一个物理定律，而是一个为了保证数值精度，特别是时间精度，必须满足的数学约束。其连续形式源于对一个恒为1的标量场应用雷诺输运定理，它指出控制体体积的变化率等于网格速度在其边界上的通量：

$$
\frac{\mathrm{d}}{\mathrm{d}t}\int_{\mathcal{V}(t)} \mathrm{d}\Omega = \oint_{\partial \mathcal{V}(t)} \boldsymbol{a}\cdot\boldsymbol{n}\,\mathrm{d}S
$$

在离散层面，这意味着一个网格单元体积 $V_c$ 的时间导数必须精确等于通过其所有面元 $f$ 的网格速度通量之和：

$$
\frac{\mathrm{d}V_c}{\mathrm{d}t} = \sum_{f} A_f\,\boldsymbol{a}_f\cdot\boldsymbol{n}_f
$$

为何这个纯粹的几何关系如此重要？考虑一个均匀流场（例如静止的流体，$\boldsymbol{u} = \boldsymbol{0}$）。在这种情况下，物理通量为零，任何物理量的变化都只应该由网格运动引起。如果离散的GCL不被满足，即 $\frac{\mathrm{d}V_c}{\mathrm{d}t} - \sum_f A_f\,\boldsymbol{a}_f\cdot\boldsymbol{n}_f \neq 0$，那么即使在没有物理驱动的情况下，离散的守恒方程也会产生一个虚假的源项，导致均匀流场被破坏。这对于要求高时间精度的气动弹性等FSI仿真来说是不可接受的。因此，用于更新网格几何的时间积分格式必须与用于求解流场方程的时间积分格式相兼容，以精确满足离散GCL [@problem_id:3959266]。

### 核心机制 II：管理大变形与网格质量

在模拟例如柔性机翼的大幅度振动等问题时，结构会经历大位移和转动，这给ALE网格带来了严峻的挑战。如果边界位移过大或过于局部化，靠近界面的流体网格单元可能会被过度压缩或扭曲，导致**网格缠结（tangling）**或**反转（inversion）** [@problem_id:3959276]。

从数学上看，网格反转意味着映射雅可比行列式 $J = \det(\boldsymbol{I} + \nabla_{\boldsymbol{X}} \boldsymbol{u})$ 在某处变为非正值 ($J \le 0$)。一个避免这种情况的充分条件是控制网格位移梯度 $\boldsymbol{H} = \nabla_{\boldsymbol{X}} \boldsymbol{u}$ 的大小。具体来说，如果能保证其谱范数 $\lVert \boldsymbol{H} \rVert_2 < 1$，那么就能确保 $J > 0$。

**径向基函数（RBF）**网格变形技术因其能产生平滑的位移场且不依赖于网格连通性而广受欢迎。然而，一个鲁棒的网格变形策略不能仅仅依赖于RBF插值的平滑性，而必须主动控制和保证网格质量。一个健壮的策略应包含以下要素 [@problem_id:3959276]：

1.  **增量式变形**：将总的边界位移分解为多个小步骤施加。这被称为**位移延拓法（displacement continuation）**。在每个增量步中，检查所有单元的雅可比行列式。
2.  **质量监控与回溯**：如果某个增量步导致任何单元的 $J$ 低于一个安全阈值（例如 $J_{\text{tol}} > 0$），则减小该步的步长（回溯），直到找到一个不会破坏网格质量的有效步长。
3.  **正则化**：在求解RBF系数时加入正则化项（如吉洪诺夫正则化），可以惩罚过大的位移梯度，从而使变形场更加平滑，有助于从一开始就避免网格质量问题。

相比之下，那种一次性施加全部位移而不监控雅可比行列式的方法，在面对大变形时是脆弱和不可靠的。一个预防性的、主动监控的策略是保证复杂FSI仿真成功的关键。

### 分离式方案的稳定性：附加质量效应

分离式方法最著名的挑战是**附加质量不稳定性（added-mass instability）**。这种不稳定性在模拟轻质结构（如薄壁航空结构）与高密度流体（如水，或高亚音速空气）相互作用时尤为突出 [@problem_id:3959291]。

其物理根源在于不可压缩流体的特性。当一个浸在不可压缩流体中的结构加速时，它必须推开周围的流体。由于流体要保持体积不变，结构局部的加速会瞬时地在整个流体域中引发一个压力场，从而驱动流体运动。这个压力场反过来又对结构产生一个与结构加速度成正比的附加作用力。仿佛结构“附加”了一部分流体的质量，这就是**附加质量（added mass）**。

这种效应的数学基础在于不可压缩流的压力泊松方程（Pressure Poisson Equation, PPE）。通过对动量方程取散度，并利用不可压缩条件 $\nabla \cdot \boldsymbol{u} = 0$，可以得到压力满足一个椭圆型的泊松方程：

$$
\nabla^{2}p = -\rho_{f}\nabla\cdot((\boldsymbol{u}\cdot\nabla)\boldsymbol{u}) + \dots
$$

更重要的是，在流固耦合界面上，压力梯度与结构加速度直接相关。通过将动量方程投影到界面法向，并忽略粘性和对流项的次要贡献，我们得到诺依曼边界条件：

$$
\frac{\partial p}{\partial n} \approx \rho_{f} (\boldsymbol{a}_s \cdot \boldsymbol{n})
$$

其中 $\boldsymbol{a}_s$ 是结构加速度。这个关系意味着结构在某一点的法向加速度会通过椭圆型的PPE瞬时地、全局地影响整个流场的压力分布，进而影响作用在结构所有点上的力。

在弱耦合的分离式方案中，这种全局耦合被滞后地处理了。在一个时间步内，流体求解器基于上一步的结构运动计算压力，然后将这个压力对应的力传递给结构求解器来计算新的运动。这构成了一个迭代映射。对于一个简化的单自由度模型，这个迭代过程可以表示为 $a^{(k+1)} \approx \frac{m_a}{m_s} a^{(k)}$，其中 $m_a$ 是附加质量，$m_s$ 是结构质量 [@problem_id:3959291]。当附加质量与结构质量之比 $m_a/m_s > 1$ 时，这个迭代会发散，导致数值解的剧烈振荡和崩溃。

有趣的是，这种不稳定性与耦合信息传递的方向密切相关。标准的狄利克雷-诺依曼（DN）方案，即结构传递运动给流体，流体传递力给结构，在附加质量主导（质量比 $r = m_s / m_a \ll 1$）的情况下是不稳定的，其子迭代的谱半径为 $\rho_{DN} \approx 1/r \gg 1$。然而，如果交换角色，采用**诺依曼-狄利克雷（ND）**方案，即结构传递力给流体，流体传递运动给结构，其谱半径会变为 $\rho_{ND} \approx r \ll 1$，从而变得稳定 [@problem_id:3959294]。

解决附加质量不稳定性的根本方法是更紧密地处理加速度-压力的耦合。**强耦合**分离式方案通过在每个时间步内进行子迭代，直到压力和加速度收敛，从而有效地逼近了隐式耦合。而**整体式**方法则从根本上在一个代数系统中同时求解压力和加速度，完全避免了这种由交错滞后引起的迭代不稳定性 [@problem_id:3959291] [@problem_id:3959268]。

### FSI耦合中的守恒原则

一个可靠的数值方案不仅要稳定，还必须离散地遵循基本的物理守恒定律，如动量守恒和能量守恒。

**能量守恒**

首先考虑连续系统的总机械能。总能量是流体动能、固体动能和固体弹性势能之和。通过对流体和固体的动量方程分别点乘其速度场并积分，可以推导出各自的能量平衡方程。将两者相加，可以证明，在界面上，流体对固体做的功与固体对流体做的功大小相等、方向相反 [@problem_id:3959313]。因此，界面功率项在总能量平衡中相互抵消。总机械能的变化率加上流体的粘性耗散，等于所有外力所做的功：

$$
\frac{\mathrm{d}}{\mathrm{d}t} (E_{kin,f} + E_{kin,s} + E_{pot,s}) + \mathcal{D}_f = P_{ext}
$$

这一结果表明，对于一个封闭的、无外力做功的FSI系统，总能量（计入耗散）应该是守恒的。然而，在离散层面，尤其是在流体和固体网格不匹配的情况下，保证能量守恒是一个严峻的挑战。

在不匹配网格间传递数据时，如果运动学量的传递（例如，将流体速度插值到结构节点上）和动力学量的传递（例如，将流体牵引力投影到结构节点力上）不是以一种**功共轭（work-conjugate）**或**伴随（adjoint）**的方式进行的，就会在数值上产生虚假的能量源或汇 [@problem_id:3959290]。

一个确保离散能量守恒的方案是：
1.  **动力学传递**：通过伽辽金（Galerkin）投影将流体牵引力场一致地转换为结构节点力。这确保了力的传递在弱形式意义下是精确的。
2.  **运动学传递**：通过与动力学传递算子互为伴随的算子来传递速度。这通常通过所谓的 $L^2$ 投影来实现，即在结构界面上寻找一个速度场，使其与流体速度场的 $L^2$ 范数误差最小。

当运动学和动力学传递算子满足这种伴随关系时，离散的界面功率交换才能精确为零，从而保证了全局离散能量守恒。任何非共轭的传递方法，如简单的最近邻插值，通常都会违反能量守恒，可能导致长期仿真的物理结果失真。

总之，本章阐述了构建和求解流固耦合问题的核心原理与机制。从基本的控制方程出发，我们探讨了整体式与分离式策略的选择，深入分析了处理边界运动的ALE方法及其对GCL的要求，剖析了分离式方案中关键的附加质量不稳定性，并最终强调了保证数值守恒性的重要性。这些原理构成了现代FSI仿真技术的基石。