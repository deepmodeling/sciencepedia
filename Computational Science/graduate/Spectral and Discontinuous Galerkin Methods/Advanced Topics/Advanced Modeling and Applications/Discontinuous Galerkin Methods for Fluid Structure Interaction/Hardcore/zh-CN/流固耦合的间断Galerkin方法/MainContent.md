## 引言
流固耦合（FSI）现象在自然界和工程领域中无处不在，从桥梁在风中的[振动](@entry_id:267781)到人体内的[血液流动](@entry_id:148677)，都涉及流体与固体结构的复杂相互作用。精确预测这些相互作用对于优化设计、确保安全和推动科学发现至关重要。然而，FSI问题的[数值模拟](@entry_id:137087)面临着巨大挑战，包括处理移动和变形的计算域、在不匹配的网格间传递信息、以及确保[多物理场耦合](@entry_id:171389)的稳定性和准确性。不连续伽辽金（DG）方法作为一种先进的有限元技术，以其局部守恒性、对复杂几何的高适应性和[高阶精度](@entry_id:750325)潜力，为解决这些难题提供了强大的框架。

本文旨在系统性地介绍如何应用DG方法解决流固耦合问题。我们将从第一性原理出发，逐步构建一个完整、鲁棒的数值求解体系。在“原理与机制”一章中，我们将建立FSI的控制方程，引入处理移动域的任意拉格朗日-欧拉（ALE）框架，并详细阐述[DG方法](@entry_id:748369)[对流](@entry_id:141806)体、固体及[界面耦合](@entry_id:750728)的[空间离散化](@entry_id:172158)策略，最后深入分析[附加质量效应](@entry_id:746267)等关键稳定性问题。随后，在“应用与跨学科连接”一章中，我们将展示该方法在声学、空气动力学、接触力学等多个领域的实际应用，揭示其解决前沿工程问题的能力。最后，通过“动手实践”部分的具体练习，读者将有机会将理论知识应用于解决实际的数值问题，从而加深对核心概念的理解。让我们首先从构建FSI问题的基本原理与机制开始。

## 原理与机制

本章旨在深入探讨用于[流固耦合](@entry_id:171183)（FSI）问题的不连续伽辽金（DG）方法的数学原理与核心机制。在引言章节的基础上，我们将首先建立描述FSI问题的连续介质力学控制方程，然后引入处理移动和变形域的必要数学框架。随后，我们将详细阐述DG方法在[空间离散化](@entry_id:172158)中的具体应用，包括[对流](@entry_id:141806)项、[扩散](@entry_id:141445)项及[界面耦合](@entry_id:750728)的处理。最后，我们将分析时间推进策略中的关键挑战，特别是[附加质量效应](@entry_id:746267)，并以[能量稳定性](@entry_id:748991)分析为结尾，为构建鲁棒且精确的数值格式提供理论依据。

### [流固耦合](@entry_id:171183)的控制方程

任何FSI问题的[数值模拟](@entry_id:137087)都始于其物理模型的数学描述。一个典型的FSI系统由一个流体子域和一个固体[子域](@entry_id:155812)组成，它们通过一个共享的、可移动的界面相互作用。为了建立一个完整的模型，我们必须定义每个[子域](@entry_id:155812)内的控制方程以及在界面上强制执行的耦合条件 。

#### 流体域

在流体域 $\Omega_f(t)$ 中，对于不可压缩的[粘性流](@entry_id:136330)体，其运动由 **纳维-斯托克斯（[Navier-Stokes](@entry_id:276387)）方程** 描述，这组方程代表了[质量守恒](@entry_id:204015)和[动量守恒](@entry_id:149964)。

- **质量守恒（连续性方程）**：对于[不可压缩流体](@entry_id:181066)，其密度 $\rho_f$ 为常数，这导致流体速度场 $\boldsymbol{u}_f$ 的散度为零。这是一个[运动学](@entry_id:173318)约束，表示流体体积在运动过程中保持不变：
$$
\nabla \cdot \boldsymbol{u}_f = 0
$$

- **动量守恒**：根据[牛顿第二定律](@entry_id:274217)，流体微元的动量变化率等于作用在其上的面力（由应力产生）和体力之和。在欧拉[坐标系](@entry_id:156346)下，其强形式（strong form）为：
$$
\rho_f \left( \frac{\partial \boldsymbol{u}_f}{\partial t} + (\boldsymbol{u}_f \cdot \nabla) \boldsymbol{u}_f \right) = \nabla \cdot \boldsymbol{\sigma}_f + \boldsymbol{f}_f
$$
其中，$\frac{\partial \boldsymbol{u}_f}{\partial t}$ 是[局部时](@entry_id:194383)间导数，[非线性](@entry_id:637147)的 $(\boldsymbol{u}_f \cdot \nabla) \boldsymbol{u}_f$ 项是 **[对流](@entry_id:141806)项**，它描述了动量随流体质点空间位置变化而产生的变化。$\boldsymbol{\sigma}_f$ 是流体的 **柯西应力张量（Cauchy stress tensor）**，$\boldsymbol{f}_f$ 是单位体积的体力（如重力）。

- **[本构关系](@entry_id:186508)**：对于牛顿流体，应力张量与流场的变形率[线性相关](@entry_id:185830)。对于[不可压缩流体](@entry_id:181066)，[本构关系](@entry_id:186508)为：
$$
\boldsymbol{\sigma}_f = -p_f \boldsymbol{I} + 2\mu_f \boldsymbol{\varepsilon}(\boldsymbol{u}_f)
$$
这里，$p_f$ 是流体压力，一个由不可压缩约束产生的拉格朗日乘子。$\boldsymbol{I}$ 是单位张量，$\mu_f$ 是流体的[动力粘度](@entry_id:268228)。$\boldsymbol{\varepsilon}(\boldsymbol{u}_f)$ 是 **[应变率张量](@entry_id:266108)**，定义为[速度梯度](@entry_id:261686)的对称部分：
$$
\boldsymbol{\varepsilon}(\boldsymbol{u}_f) = \frac{1}{2} \left( \nabla \boldsymbol{u}_f + (\nabla \boldsymbol{u}_f)^\top \right)
$$

#### 固体域

在固体域 $\Omega_s$ 中，我们考虑一个[线性弹性](@entry_id:166983)体。在小应变假设下，其运动由 **线性[弹性动力学](@entry_id:175818)方程** 描述。

- **动量守恒**：固体的[动量方程](@entry_id:197225)为：
$$
\rho_s \frac{\partial^2 \boldsymbol{d}_s}{\partial t^2} = \nabla \cdot \boldsymbol{\sigma}_s + \boldsymbol{f}_s
$$
其中，$\rho_s$ 是固体密度，$\boldsymbol{d}_s$ 是位移场，因此 $\frac{\partial^2 \boldsymbol{d}_s}{\partial t^2}$ 是[局部加速度](@entry_id:272847)。$\boldsymbol{\sigma}_s$ 是固体的柯西[应力张量](@entry_id:148973)，$\boldsymbol{f}_s$ 是[体力](@entry_id:174230)。

- **[本构关系](@entry_id:186508)**：对于线性的[各向同性弹性](@entry_id:203237)材料，应力与应变通过[胡克定律](@entry_id:149682)（Hooke's law）联系：
$$
\boldsymbol{\sigma}_s = \lambda_s \mathrm{tr}(\boldsymbol{\varepsilon}(\boldsymbol{d}_s)) \boldsymbol{I} + 2\mu_s \boldsymbol{\varepsilon}(\boldsymbol{d}_s)
$$
其中，$\lambda_s$ 和 $\mu_s$ 是材料的 **拉梅参数（Lamé parameters）**。$\boldsymbol{\varepsilon}(\boldsymbol{d}_s)$ 是无穷小 **[应变张量](@entry_id:193332)**，定义为[位移梯度](@entry_id:165352)的对称部分：
$$
\boldsymbol{\varepsilon}(\boldsymbol{d}_s) = \frac{1}{2} \left( \nabla \boldsymbol{d}_s + (\nabla \boldsymbol{d}_s)^\top \right)
$$

#### [界面条件](@entry_id:750725)

在[流固界面](@entry_id:148992) $\Gamma_{fs}(t)$ 上，必须满足两个基本的物理条件，以确保两个子系统之间的耦合是相容的 。

- **运动学条件（速度连续性）**：假设在界面上没有滑移和质量交换（如[相变](@entry_id:147324)），流体[质点](@entry_id:186768)和固体质点的速度必须相同。固体的速度是其位移的时间变化率，即 $\dot{\boldsymbol{d}}_s$。因此，我们有：
$$
\boldsymbol{u}_f = \dot{\boldsymbol{d}}_s \quad \text{on } \Gamma_{fs}(t)
$$
这个矢量条件同时保证了法向速度（无穿透）和切向速度（无滑移）的连续性。

- **动力学条件（牵引[力平衡](@entry_id:267186)）**：根据[牛顿第三定律](@entry_id:166652)（作用力与[反作用](@entry_id:203910)力），流体作用在固体界面上的力必须与固体作用在[流体界面](@entry_id:197635)上的力大小相等、方向相反。单位面积上的力即为 **牵[引力](@entry_id:175476)（traction）** $\boldsymbol{t} = \boldsymbol{\sigma} \boldsymbol{n}$，其中 $\boldsymbol{n}$ 是界面的[单位法向量](@entry_id:178851)。如果我们定义 $\boldsymbol{n}$ 指向固体域，那么流体对固体的牵[引力](@entry_id:175476)为 $\boldsymbol{t}_f = \boldsymbol{\sigma}_f \boldsymbol{n}$，而固体[对流](@entry_id:141806)体的牵[引力](@entry_id:175476)为 $\boldsymbol{t}_s = \boldsymbol{\sigma}_s (-\boldsymbol{n})$。作用力-反作用[力平衡](@entry_id:267186)要求 $\boldsymbol{t}_f = -\boldsymbol{t}_s$，代入后得到：
$$
\boldsymbol{\sigma}_f \boldsymbol{n} = \boldsymbol{\sigma}_s \boldsymbol{n} \quad \text{on } \Gamma_{fs}(t)
$$
这个条件表明，在界面上牵[引力](@entry_id:175476)矢量是连续的，这意味着[法向应力](@entry_id:260622)和切向应力都必须连续。

### 移动域的挑战：任意拉格朗日-欧拉（ALE）框架

FSI 问题的核心挑战之一是流体域 $\Omega_f(t)$ 的边界随时间移动。标准的[欧拉描述](@entry_id:264722)（固定网格）或[拉格朗日描述](@entry_id:264498)（网格随物质运动）都难以有效处理此类问题。**任意拉格朗日-欧拉（Arbitrary Lagrangian-Eulerian, ALE）** 框架通过引入一个独立的计算网格来解决这一问题，该网格的运动既不完全固定，也不必跟随流体[质点](@entry_id:186768) 。

在[ALE方法](@entry_id:746347)中，我们定义一个从固定的 **参考域** $\hat{\Omega}$ 到随时间变化的 **物理域** $\Omega(t)$ 的光滑可逆映射 $\boldsymbol{\chi}$：
$$
\boldsymbol{x} = \boldsymbol{\chi}(\hat{\boldsymbol{x}}, t), \quad \text{其中 } \hat{\boldsymbol{x}} \in \hat{\Omega}, \boldsymbol{x} \in \Omega(t)
$$
**网格速度** $\boldsymbol{w}$ 被定义为参考点 $\hat{\boldsymbol{x}}$ 在物理空间中的运动速度：
$$
\boldsymbol{w}(\boldsymbol{x}, t) = \frac{\partial \boldsymbol{\chi}}{\partial t}\left(\boldsymbol{\chi}^{-1}(\boldsymbol{x}, t), t\right)
$$
为了在移动的控制体积上保持守恒律，我们需要修改标准的[欧拉形式](@entry_id:637896)。对于一个守恒律 $\partial_t U + \nabla \cdot F(U) = 0$，其ALE形式通过引入一个由[网格运动](@entry_id:163293)引起的附加通量来得到。根据 **[雷诺输运定理](@entry_id:191217)（Reynolds Transport Theorem）**，一个在[移动控制体积](@entry_id:265261) $V(t)$ 内的量的总变化率，等于体积内的[局部变化率](@entry_id:264961)加上通过边界的通量。这最终导出了守恒律的ALE[微分形式](@entry_id:146747)：
$$
\frac{\partial U}{\partial t} + \nabla \cdot \left(F(U) - U \boldsymbol{w}\right) = 0
$$
这里的 $U \boldsymbol{w}$ 是一个张量积，代表由于[网格运动](@entry_id:163293)而产生的[对流输运](@entry_id:149512)。$(F(U) - U \boldsymbol{w})$ 被称为 **相对通量**，因为它代表了物理通量相对于[移动网格](@entry_id:752196)的通量。这个形式是完全守恒的。

#### [几何守恒律](@entry_id:170384)（GCL）

为了保证ALE数值格式的正确性，它不仅要满足物理守恒律，还必须精确地描述网格本身的几何变化。这一点由 **[几何守恒律](@entry_id:170384)（Geometric Conservation Law, GCL）** 来保证。GCL 描述了映射的雅可比行列式 $J = \det(\nabla_{\hat{\boldsymbol{x}}} \boldsymbol{\chi})$ 的[时间演化](@entry_id:153943)与网格[速度散度](@entry_id:264117)之间的关系：
$$
\frac{\partial J}{\partial t} = J (\nabla_{\boldsymbol{x}} \cdot \boldsymbol{w})
$$
在数值离散中，必须满足GCL的离散形式。否则，即使在均匀流场（如 $U = \text{常数}$）中，仅由[网格运动](@entry_id:163293)本身也可能产生虚假的源或汇，从而破坏守恒性。满足离散GCL是确保数值格式能够保持常数解（即所谓的 **[自由流](@entry_id:159506)保持** 性质）的关键 。

对于高阶DG方法，尤其是在处理弯曲边界时，这一要求变得更加严格 。通常采用 **[等参映射](@entry_id:173239)（isoparametric mapping）**，即用与求解变量相同的多项式[基函数](@entry_id:170178)来表示几何形状。在这种情况下，为了精确地保持[自由流](@entry_id:159506)，离散格式必须满足一系列 **度量恒等式（metric identities）**，包括对静止网格的 **皮奥拉恒等式（Piola identity）** 和对[移动网格](@entry_id:752196)的ALE GCL。这些恒等式保证了即使在弯曲变形的单元上，离散的[微分算子](@entry_id:140145)也能精确地处理常数状态。

### 不[连续伽辽金方法](@entry_id:747805)的离散化

[DG方法](@entry_id:748369)通过在不重叠的单元网格上定义分片多项式解和[检验函数](@entry_id:166589)空间，为FSI问题提供了一个灵活且高精度的离散框架。其核心思想是在单元内部求解方程的弱形式，并通过 **数值通量** 在单元边界上传递信息。

#### 粘性项/弹性项的离散化

对于包含[二阶导数](@entry_id:144508)的粘性项（如 $-\nabla \cdot (2\mu \boldsymbol{\varepsilon}(\boldsymbol{u}))$），[DG方法](@entry_id:748369)需要特殊处理。有几种主流格式，它们在稳定性、对称性和计算成本之间做出了不同的权衡 。

- **[对称内部罚](@entry_id:755719)函数[伽辽金法](@entry_id:749698)（Symmetric Interior Penalty Galerkin, SIPG）**：这是最直接的方法之一。它通过在单元边界上对解的跳跃项施加一个 **[罚函数](@entry_id:638029)** 来保证稳定性。其数值通量既包含[应力张量](@entry_id:148973)的平均值，也包含一个与解的跳跃成正比的惩罚项。为了保证方法的[矫顽性](@entry_id:159399)（coercivity），罚函数参数 $\eta$ 必须足够大，其尺度通常为 $\eta \sim \mu k^2 / h$，其中 $k$ 是多项式次数，$h$ 是单元尺寸。

- **局部[不连续伽辽金法](@entry_id:748485)（Local Discontinuous Galerkin, [LDG](@entry_id:751395)）**：[LDG](@entry_id:751395)通过引入一个辅助变量来表示梯度的近似值，从而将二阶问题转化为[一阶系统](@entry_id:147467)。例如，引入 $\boldsymbol{q} \approx \nabla \boldsymbol{u}$。然后对这个[一阶系统](@entry_id:147467)进行离散。稳定性通过在单元边界上交替选择“上游”和“下游”的数值通量来实现，而不需要显式的罚函数参数。其代价是引入了额外的未知量，增加了计算成本。

- **Bassi-Rebay 2 (BR2) 方法**：BR2方法  是一种巧妙的折衷方案。它既不引入辅助变量，也不依赖于大的罚函数参数。其核心思想是通过一个 **[提升算子](@entry_id:751273)（lifting operator）** 从单元边界上解的跳跃中重构一个更精确的梯度。这个重构的梯度被用来计算粘性通量。稳定性是通过[提升算子](@entry_id:751273)本身的设计隐式地获得的，它将边界上跳跃的范数与单元内部的范数联系起来，从而提供了必要的控制。

这些方法各有优劣，SIPG因其简单和对称性而受欢迎；[LDG](@entry_id:751395)在某些情况下更具鲁棒性；而BR2则在[计算效率](@entry_id:270255)上具有优势。

#### 边界条件和[界面条件](@entry_id:750725)的弱施加

[DG方法](@entry_id:748369)的另一个强大之处在于其以自然的方式 **弱施加** 边界和[界面条件](@entry_id:750725)。

- **[Nitsche方法](@entry_id:175793)**：对于狄利克雷（Dirichlet）类型的条件，如在FSI界面上的速度连续性条件 $\boldsymbol{u}_f = \dot{\boldsymbol{d}}_s$，**[Nitsche方法](@entry_id:175793)** 是一种非常有效的弱施加技术 。该方法通过在[弱形式](@entry_id:142897)中添加三项来修改边界积分：一项是标准的通量项，一项是保证对称性（或伴随一致性）的项，以及一项惩罚速度差的罚函数项。对于粘性算子，对称[Nitsche方法](@entry_id:175793)的边界项形式为：
$$
-\int_{\Gamma_{fs}} \boldsymbol{v} \cdot \boldsymbol{\sigma}_f \boldsymbol{n} \, ds - \int_{\Gamma_{fs}} (\boldsymbol{u}_f - \dot{\boldsymbol{d}}_s) \cdot \boldsymbol{\sigma}_f(\boldsymbol{v}) \boldsymbol{n} \, ds + \int_{\Gamma_{fs}} \tau (\boldsymbol{u}_f - \dot{\boldsymbol{d}}_s) \cdot \boldsymbol{v} \, ds
$$
其中 $\boldsymbol{v}$ 是[检验函数](@entry_id:166589)。与SIPG类似，[罚函数](@entry_id:638029)参数 $\tau$ 必须足够大以保证稳定性，其尺度也为 $\tau \sim \mu k^2/h$。

- **ALE[对流](@entry_id:141806)项的边界通量**：对于远场的[对流边界条件](@entry_id:165911)，必须使用ALE框架下的数值通量。信息传播的方向由 **相对速度** $(\boldsymbol{u}_f - \boldsymbol{w}) \cdot \boldsymbol{n}$ 的符号决定。
    - 如果 $(\boldsymbol{u}_f - \boldsymbol{w}) \cdot \boldsymbol{n} \ge 0$，则信息从域内向外传播（流出），[数值通量](@entry_id:752791)应使用域内的解。
    - 如果 $(\boldsymbol{u}_f - \boldsymbol{w}) \cdot \boldsymbol{n}  0$，则信息从域外向内传播（流入），[数值通量](@entry_id:752791)应使用指定的[远场](@entry_id:269288)或外部数据。
这种基于信息传播方向选择状态的方法被称为 **上游通量（upwind flux）**，它对于保证[对流](@entry_id:141806)主导问题的稳定性至关重要 。

### [时间离散化](@entry_id:169380)与耦合策略

将[空间离散化](@entry_id:172158)后，FSI问题变成一个大型的[常微分方程组](@entry_id:266774)。下一步是在时间上对其进行求解。针对流固耦合这一多物理场问题，主要有两种时间推进策略 。

#### 整体式（Monolithic）方法

在整体式方法中，所有未知量——包括流体速度、流体压力和固体位移——在每个时间步内被组合成一个单一的、巨大的代数系统进行求解。[流固界面](@entry_id:148992)的耦合条件被直接内置到这个[大系统](@entry_id:166848)的矩阵和右端向量中。

- **优点**：这种紧[耦合方法](@entry_id:195982)能够精确地满足每个时间步结束时的[界面条件](@entry_id:750725)。因此，它具有卓越的 **稳定性和鲁棒性**，特别是对于那些分区式方法难以处理的问题（如下文将讨论的附加质量问题）。
- **缺点**：实现复杂度高，需要构建和求解一个通常是非对称且病态的庞大线性系统。为了高效求解，必须设计和实现复杂的 **块预条件子（block preconditioners）**，例如基于[舒尔补](@entry_id:142780)（Schur complement）近似的预条件子。

#### 分区式（Partitioned）方法

在分区式方法中，流体和固体子问题在每个时间步内被顺序求解。例如，一个典型的 **狄利克雷-诺伊曼（Dirichlet-Neumann）** 格式会：
1. 预测界面运动（例如，将结构速度作为流体的狄利克雷边界条件）。
2. 求解流体子问题。
3. 计算流体作用在界面上的牵[引力](@entry_id:175476)。
4. 将此牵[引力](@entry_id:175476)作为[诺伊曼边界条件](@entry_id:142124)，求解固体子问题。
5. 比较求解得到的结构运动与第一步的预测是否一致。如果不一致，则更新预测并重复上述过程，直到界面残差收敛。

- **优点**：分区式方法的核心优势在于其 **模块化**。它允许重用现有的、高度优化的单物理场求解器，大大降低了开发难度。
- **缺点**：收敛性是其主要挑战。这种在界面上的[不动点迭代](@entry_id:749443)可能收敛缓慢，甚至发散。为了达到与整体式方法相当的精度和一致性，每个时间步内通常需要多次界面迭代，这会增加计算成本。更严重的是，在某些物理条件下，这种耦合方式存在固有的[数值不稳定性](@entry_id:137058)。

### 一个关键挑战：[附加质量不稳定性](@entry_id:174360)

分区式方法面临的最著名挑战是 **[附加质量不稳定性](@entry_id:174360)（added-mass instability）**  。

[附加质量效应](@entry_id:746267)是一种物理现象：当一个结构在流体中加速时，它必须同时加速周围的流体。这部分被加速的流体表现得就像是附着在结构上的一个额外质量，即 **[附加质量](@entry_id:267870)（added mass）**。对于一个在长度为$L$、[截面](@entry_id:154995)积为$A$的通道中运动的活塞，其[附加质量](@entry_id:267870)可以简单地估算为 $m_a = \rho_f A L$ 。

当使用显式或松耦合的分区式方案时，这种物理效应会引发[数值不稳定性](@entry_id:137058)。问题根源在于[界面力](@entry_id:184024)的计算存在 **时间滞后**。结构在第 $n$ 步的加速度是由第 $n-1$ 步的[流体压力](@entry_id:142203)决定的。这种滞后在流体惯性（[附加质量](@entry_id:267870)）相对于结构惯性非常显著时，会形成一个不稳定的正反馈循环。

我们可以通过一个简单的模型来分析这种不稳定性。考虑一个分区式迭代，其速度的迭代映射可以近似表示为 $v^{(k+1)} = G v^{(k)} + C$。其收敛性由放大因子 $G$ 的大小决定。分析表明，这个[放大因子](@entry_id:144315)主要由 **[附加质量](@entry_id:267870)比** $r = m_a / m_s$ 控制，其中 $m_s$ 是结构质量 。当忽略其他阻尼效应时，[放大因子](@entry_id:144315)的[绝对值](@entry_id:147688)近似为 $|G| \approx r$。

因此，当[附加质量](@entry_id:267870)超过结构质量时，即 $r  1$ 时，迭代[放大因子](@entry_id:144315)的模将大于1，导致[不动点迭代](@entry_id:749443)发散。这种不稳定性与时间步长 $\Delta t$ 的大小无关，仅仅减小时间步长无法解决问题。这就是为什么当结构非常轻（$m_s$ 小）而流体密度大（$\rho_f$ 大）时，FSI问题尤其具有挑战性。虽然通过在界面附近加密网格可以减小与单个单元相关的局部附加质量，但这并不能从根本上解决当 $m_s$ 极小时的问题 。

解决[附加质量不稳定性](@entry_id:174360)的根本方法是采用 **强耦合** 策略，即消除或减小[界面力](@entry_id:184024)的时间滞后。**整体式方法** 通过同时求解将[附加质量](@entry_id:267870)项隐式地移到了矩阵的左侧，从而天然地避免了这种不稳定性。一些先进的分区式方法，如采用界面预测、松弛或隐式交换边界条件（如Robin-Neumann耦合），也旨在通过在每个时间步内迭代至收敛来模拟隐式耦合，从而恢复稳定性 。

### 耦合系统的[能量稳定性](@entry_id:748991)

最后，一个设计良好的数值格式应该在物理上是稳定的。对于一个没有外部能量输入的封闭FSI系统，其总能量应该是耗散的（即非增的）。这为我们分析和设计[DG格式](@entry_id:178043)提供了坚实的理论基础 。

系统的 **半离散总能量** $E_h(t)$ 由流体动能、固体动能和固体弹性势能组成：
$$
E_h(t) = \sum_{K \subset \Omega_f} \int_K \frac{1}{2} \rho_f |\boldsymbol{u}_h|^2 \, d\boldsymbol{x} + \sum_{K \subset \Omega_s} \int_K \left( \frac{1}{2} \rho_s |\boldsymbol{v}_h^s|^2 + \mu_s \boldsymbol{\varepsilon}(\boldsymbol{d}_h) : \boldsymbol{\varepsilon}(\boldsymbol{d}_h) \right) d\boldsymbol{x}
$$
为了保证 $\frac{d}{dt} E_h(t) \le 0$，[数值格式](@entry_id:752822)的每个组成部分都必须满足特定的条件，以确保它们不会人为地产生能量：

- **[对流](@entry_id:141806)项**：必须采用一种在离散层面上不产生能量的格式，例如 **偏对称（skew-symmetric）** 形式的离散。
- **[压力-速度耦合](@entry_id:155962)**：离散的梯度和[散度算子](@entry_id:265975)必须是 **偏伴随（skew-adjoint）** 的，以保证压力项所做的总功为零。
- **粘性/弹性项**：必须采用稳定的离散格式，如 **SIPG**。这要求罚函数参数足够大，以确保离散算子是矫顽的，从而其贡献是耗散的。
- **[界面耦合](@entry_id:750728)**：必须采用能量稳定的耦合格式，如 **对称的、伴随一致的[Nitsche方法](@entry_id:175793)**。这种方法通过精心设计的项和足够大的罚函数参数，确保了在界面上的功率交换是守恒或耗散的，从而惩罚速度失配而不产生虚假能量。

通过满足所有这些条件，我们可以构建一个在理论上保证能量稳定的DG-FSI格式，这是实现长期、大规模[数值模拟](@entry_id:137087)的基石。