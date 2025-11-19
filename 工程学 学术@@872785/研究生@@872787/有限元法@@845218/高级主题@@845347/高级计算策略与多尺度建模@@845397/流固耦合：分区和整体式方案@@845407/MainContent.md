## 引言
[流固耦合](@entry_id:171183)（Fluid-Structure Interaction, FSI）是描述可变形固体与内部或外部流场相互作用的物理现象，广泛存在于航空航天、[生物医学工程](@entry_id:268134)、土木工程等多个前沿领域。从飞机的机翼振颤、心脏瓣膜的开合，到桥梁在风中的摆动，精确预测和模拟这些复杂的耦合行为对于工程设计的安全性和优化至关重要。然而，由于其固有的高度[非线性](@entry_id:637147)、移动的物理边界以及[多物理场](@entry_id:164478)之间的紧密耦合，FSI问题的数值求解构成了计算力学领域的一大挑战。其中，如何高效且稳定地耦合流体和固体求解器，是决定仿真成败的核心问题。

本文旨在系统性地梳理和剖析FSI数值求解的两种主流策略：整体式（monolithic）与分离式（partitioned）方法。我们将从第一章“原理与机制”出发，首先建立FSI问题的控制方程和[界面条件](@entry_id:750725)，然后深入剖析整体式与分离式方法的数学构造、优缺点，并着重探讨[附加质量效应](@entry_id:746267)和[几何守恒律](@entry_id:170384)等关键概念。接下来，在第二章“应用与交叉学科联系”中，我们将理论联系实际，通过Turek-Hron基准问题、异步时间步进、[非匹配网格](@entry_id:168552)等高级应用，展示这些方法在解决真实世界问题时的权衡与选择。最后，第三章“动手实践”将提供一系列编程练习，帮助读者将理论知识转化为实践能力。通过本文的学习，您将建立起对FSI数值方法全面而深入的理解，为解决复杂的耦合问题打下坚实的基础。

## 原理与机制

本章将深入探讨流固耦合（FSI）问题的核心原理及其数值求解机制。我们将从描述控制物理现象的耦合[方程组](@entry_id:193238)出发，进而介绍两种主流的求解策略——整体式（monolithic）方法和分离式（partitioned）方法。我们将详细分析这些方法的数学构造、优缺点，并着重阐述分离式方法中出现的关键挑战，如[数值稳定性](@entry_id:146550)和[附加质量效应](@entry_id:746267)（added-mass effect）。最后，我们将讨论在处理移动和变形域时至关重要的任意拉格朗日-欧拉（Arbitrary Lagrangian-Eulerian, ALE）方法及其[几何守恒律](@entry_id:170384)（Geometric Conservation Law, GCL）的基本要求。

### [流固耦合](@entry_id:171183)的控制方程

一个完整的流固耦合问题由至少两个相互作用的物理域组成：流体域和固体域。对这些域的精确数学描述是进行任何数值分析的起点。考虑一个由不可压缩[牛顿流体](@entry_id:263796)占据的时变域 $\Omega_f(t)$ 和一个[非线性弹性](@entry_id:185743)体占据的时变域 $\Omega_s(t)$ 组成的系统。这两个域共享一个移动的界面 $\Gamma_{fs}(t)$。

**流体子系统**在欧拉[坐标系](@entry_id:156346)下由不可压缩的[纳维-斯托克斯](@entry_id:276387)（[Navier-Stokes](@entry_id:276387)）方程描述，该方程表达了质量守恒和[动量守恒](@entry_id:149964)：
$$
\begin{aligned}
\rho_f \left( \frac{\partial \boldsymbol{u}_f}{\partial t} + (\boldsymbol{u}_f \cdot \nabla) \boldsymbol{u}_f \right) - \nabla \cdot \boldsymbol{\sigma}_f = \boldsymbol{f}_f \quad \text{in } \Omega_f(t) \\
\nabla \cdot \boldsymbol{u}_f = 0 \quad \text{in } \Omega_f(t)
\end{aligned}
$$
其中，$\rho_f$ 是流体密度，$\boldsymbol{u}_f$ 是[流体速度](@entry_id:267320)，$\boldsymbol{f}_f$ 是单位体积的体力。流体的柯西（Cauchy）应力张量 $\boldsymbol{\sigma}_f$ 对于牛顿流体来说，由下式给出：
$$
\boldsymbol{\sigma}_f = -p_f \boldsymbol{I} + 2 \mu_f \boldsymbol{\varepsilon}(\boldsymbol{u}_f)
$$
这里 $p_f$ 是流体压力，$\mu_f$ 是[动力粘度](@entry_id:268228)，$\boldsymbol{\varepsilon}(\boldsymbol{u}_f) = \frac{1}{2}(\nabla \boldsymbol{u}_f + (\nabla \boldsymbol{u}_f)^\top)$ 是应变率张量。

**固体子系统**的运动通常在拉格朗日[坐标系](@entry_id:156346)下描述最为自然，但为了与流体部分的[欧拉描述](@entry_id:264722)相耦合，其控制方程也可以在当前构型 $\Omega_s(t)$ 下以[欧拉形式](@entry_id:637896)写出。对于一个[非线性](@entry_id:637147)超弹性固体，其动量守恒方程为 [@problem_id:2560154]：
$$
\rho_s \left( \frac{\partial \boldsymbol{u}_s}{\partial t} + (\boldsymbol{u}_s \cdot \nabla) \boldsymbol{u}_s \right) - \nabla \cdot \boldsymbol{\sigma}_s = \boldsymbol{f}_s \quad \text{in } \Omega_s(t)
$$
其中 $\rho_s$ 是固体在当前构型下的密度，$\boldsymbol{u}_s$ 是固体速度，$\boldsymbol{f}_s$ 是[体力](@entry_id:174230)。固体的柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}_s$ 通过一个[储能函数](@entry_id:197811) $W(\boldsymbol{F})$ 导出，该函数依赖于变形梯度 $\boldsymbol{F}$。第一皮奥拉-基尔霍夫（Piola-Kirchhoff）应力 $P$ 由 $P = \partial W(\boldsymbol{F}) / \partial \boldsymbol{F}$ 给出，而柯西应力则通过[Piola变换](@entry_id:163790)得到：$\boldsymbol{\sigma}_s = J^{-1} \boldsymbol{P} \boldsymbol{F}^\top$，其中 $J = \det \boldsymbol{F}$。

**[界面耦合](@entry_id:750728)条件**是流固耦合问题的核心，它将两个子系统联系在一起。在界面 $\Gamma_{fs}(t)$ 上，必须同时满足两个条件：
1.  **运动学连续性条件 (Kinematic Condition)**：此条件要求在界面上无滑移、无穿透，即流体和固体的速度必须相等。
    $$
    \boldsymbol{u}_f = \boldsymbol{u}_s \quad \text{on } \Gamma_{fs}(t)
    $$
2.  **[动力学平衡](@entry_id:187220)条件 (Dynamic Condition)**：根据[牛顿第三定律](@entry_id:166652)（作用力与反作用力定律），流体作用在界面上的力必须与固体作用在界面上的力大小相等、方向相反。这表现为界面上的牵[引力](@entry_id:175476)（traction）平衡。
    $$
    \boldsymbol{\sigma}_f \boldsymbol{n}_f + \boldsymbol{\sigma}_s \boldsymbol{n}_s = \boldsymbol{0} \quad \text{on } \Gamma_{fs}(t)
    $$
    这里，$\boldsymbol{n}_f$ 和 $\boldsymbol{n}_s$ 分别是流体域和固体域在界面处指向域外的[单位法向量](@entry_id:178851)，因此在界面上总有 $\boldsymbol{n}_f = -\boldsymbol{n}_s$。

这些方程，再加上适当的外部边界条件和[初始条件](@entry_id:152863)，共同构成了一个完整且复杂的流固耦合初边值问题 [@problem_id:2560154]。由于其高度的[非线性](@entry_id:637147)和几何复杂性，直接求解该问题几乎是不可能的，必须依赖数值方法。

### 数值求解策略：整体式与分离式方法

在有限元等数值方法的框架下，求解上述耦合[方程组](@entry_id:193238)主要有两种策略：整体式（monolithic）方法和分离式（partitioned）方法。

#### 整体式方法

整体式方法将整个流固耦合系统视为一个单一的、巨大的[非线性方程组](@entry_id:178110)。它将流体变量（如速度 $\boldsymbol{u}_f$ 和压力 $p_f$）和固体变量（如位移 $\boldsymbol{d}_s$ 或速度 $\boldsymbol{u}_s$）放在一个大的未知向量中，然后对整个系统同时进行离散和求解。

这种方法的数学基础源于将耦合系统的弱形式（variational form）整合在一起。首先，我们为流体和固体子问题分别构建其[虚功](@entry_id:176403)（或[虚功](@entry_id:176403)率）方程。例如，通过将动量方程乘以一个任意的虚速度（检验函数），然后在各自的域上积分，并应用[散度定理](@entry_id:143110)（[分部积分](@entry_id:136350)），我们可以得到每个子系统的[弱形式](@entry_id:142897) [@problem_id:2560184]。

关键在于如何处理界面项。在推导[弱形式](@entry_id:142897)的过程中，每个子系统都会产生一个边界积分项，其中包括在界面 $\Gamma_{fs}$ 上的积分。例如，流体和固体的[虚功](@entry_id:176403)率方程中会分别包含以下界面项：
$$
I_f = \int_{\Gamma_{fs}} \delta\boldsymbol{v}_f \cdot (\boldsymbol{\sigma}_f \boldsymbol{n}_f) \, \mathrm{d}\Gamma \quad \text{and} \quad I_s = \int_{\Gamma_{fs}} \delta\boldsymbol{v}_s \cdot (\boldsymbol{\sigma}_s \boldsymbol{n}_s) \, \mathrm{d}\Gamma
$$
在整体式方法中，由于运动学条件 $\boldsymbol{u}_f = \boldsymbol{u}_s$ 被强加，检验函数也必须满足相同的连续性，即 $\delta\boldsymbol{v}_f = \delta\boldsymbol{v}_s \equiv \delta\boldsymbol{v}_\Gamma$。当我们把两个子系统的[虚功](@entry_id:176403)率方程相加来构建整个系统的方程时，这两个界面项可以合并：
$$
I_f + I_s = \int_{\Gamma_{fs}} \delta\boldsymbol{v}_\Gamma \cdot (\boldsymbol{\sigma}_f \boldsymbol{n}_f + \boldsymbol{\sigma}_s \boldsymbol{n}_s) \, \mathrm{d}\Gamma
$$
由于[动力学平衡](@entry_id:187220)条件 $\boldsymbol{\sigma}_f \boldsymbol{n}_f + \boldsymbol{\sigma}_s \boldsymbol{n}_s = \boldsymbol{0}$ 是我们要求解的强形式的一部分，这个合并后的积分项恒等于零，因此在最终的整体[弱形式](@entry_id:142897)中自然消失 [@problem_id:2560184]。

这意味着，在最终形成的[代数方程](@entry_id:272665)组 $R(U)=0$ 中，界面本身成为了一个“内部”边界，其上的力自然平衡，无需特殊处理。最终得到的系统是一个巨大的、全耦合的非线性方程组，需要使用专门的求解器（如耦合[牛顿法](@entry_id:140116)）来求解 [@problem_id:2560161]。

**优点**：
-   **强耦合**：通过同时求解所有变量，该方法能够隐式地、精确地满足[界面条件](@entry_id:750725)，因此具有优异的稳定性和精度。
-   **鲁棒性**：对于具有强耦合效应的问题（如下文将讨论的[附加质量效应](@entry_id:746267)），整体式方法通常是唯一可靠的选择。

**缺点**：
-   **实现复杂**：需要开发或使用能够处理[多物理场耦合](@entry_id:171389)的高度专用的软件。
-   **计算成本高**：求解一个巨大的、结构复杂的[非线性系统](@entry_id:168347)通常比求解几个较小的系统要昂贵得多。

#### 分离式方法

与整体式方法相反，分离式方法遵循“[分而治之](@entry_id:273215)”的哲学。它将[流固耦合](@entry_id:171183)[问题分解](@entry_id:272624)为流体和固体两个（或更多）子问题，然后通过在界面上迭代交换数据来求解。这种方法允许研究人员复用现有的、高度优化的单物理场求解器（例如，一个用于计算流体动力学（CFD）的求解器和一个用于计算结构力学（CSM）的求解器）。

一个典型的分离式算法，例如**狄利克雷-诺伊曼（Dirichlet-Neumann）**分区方案，其在一个时间步 $t^n \to t^{n+1}$ 内的执行流程如下 [@problem_id:2560132]：

1.  **预测 (Prediction)**：预测在 $t^{n+1}$ 时刻的界面位移和速度。这通常基于前几个时间步的历史数据进行外插。
2.  **流体求解 (Fluid Solve)**：将预测的界面速度作为狄利克雷（Dirichlet）边界条件，求解流体子问题，得到 $t^{n+1}$ 时刻的流场和压[力场](@entry_id:147325)。
3.  **[载荷传递](@entry_id:201778) (Load Transfer)**：根据求解出的流场，计算流体作用在界面上的牵[引力](@entry_id:175476)（即载荷）。
4.  **固体求解 (Structure Solve)**：将此流体载荷作为诺伊曼（Neumann）边界条件，求解固体子问题，得到一个新的 $t^{n+1}$ 时刻的界面位移和速度。
5.  **收敛性检查与迭代 (Convergence Check  Iteration)**：比较第4步计算出的界面位移/速度与第1步预测的值。如果差异大于预设的容差，则用新计算出的值（或通过松弛技术混合后的值）进行新的预测，并返回第2步，开始一次新的**子迭代（sub-iteration）**。如果差异小于容差，则认为该时间步收敛，进入下一个时间步。

这种迭代过程在数学上可以被抽象为一个[不动点迭代](@entry_id:749443)问题 [@problem_id:2560182]。我们可以定义一个界面算子 $\mathcal{T}$，它将一个给定的界面位移猜测值 $g^k$（$k$ 是子迭代次数），通过一次流体求解和一次固体求解，映射到一个新的界面位移值 $\tilde{g}$。即 $\tilde{g} = \mathcal{T}(g^k)$。我们的目标是找到一个[不动点](@entry_id:156394) $g^\star$，使得 $g^\star = \mathcal{T}(g^\star)$。
子迭代过程就是简单的[不动点迭代](@entry_id:749443)：
$$
g^{k+1} = \mathcal{T}(g^k)
$$
而收敛性则通过监测残差 $r^k = g^k - \mathcal{T}(g^k)$ 的范数是否足够小来判断。

**优点**：
-   **模块化和灵活性**：可以利用现成的、成熟的单物理场软件。
-   **实现相对简单**：耦合逻辑主要体现在数据交换和迭代控制上。

**缺点**：
-   **收敛性和稳定性问题**：分离式方法的收敛性并非总是得到保证，尤其是在某些物理条件下，可能会出现严重的稳定性问题。

### 分离式方法的关键挑战

分离式方法虽然在工程实践中应用广泛，但其成功与否取决于如何处理两个核心挑战：一致性（[分裂误差](@entry_id:755244)）和稳定性（[附加质量效应](@entry_id:746267)）。

#### 一致性与[分裂误差](@entry_id:755244)

根据子迭代的执行情况，分离式方法可以分为两类：

-   **松耦合（Loosely-coupled）或交错（Staggered）方法**：在每个时间步内只执行一次流体-固体求解交换，不进行子迭代。这种方法本质上是用来自前一时刻或前一次迭代的信息来求解当前子问题，例如，用 $t^n$ 时刻的固体运动来计算 $t^{n+1}$ 时刻的流体载荷。这导致[界面条件](@entry_id:750725)在 $t^{n+1}$ 时刻没有被精确满足，从而引入了一个与时间步长 $\Delta t$ 同阶的**[分裂误差](@entry_id:755244)（splitting error）**，即 $\mathcal{O}(\Delta t)$ [@problem_id:2560140]。这个误差是算法内在的，即使子问题的求解精度再高也无法消除。

-   **强耦合（Strongly-coupled）方法**：在每个时间步内执行多次子迭代，直到界面上的残差（例如，位移和力的不匹配度）收敛到容差范围内。通过这种方式，强[耦合方法](@entry_id:195982)能够确保在每个时间步结束时，[界面条件](@entry_id:750725)都得到（近似）精确满足。一个收敛的强耦合分离式方法，其在一个时间步内得到的解，在代数上等价于整体式方法在该时间步的解，从而消除了[分裂误差](@entry_id:755244) [@problem_id:2560140]。

#### 稳定性与[附加质量效应](@entry_id:746267)

对于某些类型的FSI问题，松[耦合方法](@entry_id:195982)不仅精度有限，还可能存在严重的数值不稳定性。最著名的例子就是**[附加质量效应](@entry_id:746267)（added-mass effect）**。

当一个结构在流体中加速时，它必须同时推动周围的流体一起加速。从结构的角度看，就好像它的[惯性质量](@entry_id:267233)增加了。这部分由流体惯性引起的“额外”质量，就被称为**[附加质量](@entry_id:267870)**。对于[不可压缩流体](@entry_id:181066)，压[力场](@entry_id:147325)会瞬时响应边界的加速度，因此[附加质量效应](@entry_id:746267)是一种纯惯性效应，与流体粘性无关。

我们可以通过一个简化的1D活塞模型来深刻理解[附加质量](@entry_id:267870)及其对稳定性的影响 [@problem_id:2560186] [@problem_id:2560142]。考虑一个质量为 $m$ 的活塞，通过刚度为 $k$ 的弹簧连接，浸没在密度为 $\rho$ 的不可压缩流体中。流体被限制在长度为 $L$、[横截面](@entry_id:154995)积为 $A$ 的管道内。通过[对流](@entry_id:141806)体和固体分别应用[动量守恒](@entry_id:149964)，可以推导出流体施加在活塞上的力与活塞加速度 $\ddot{x}$ 成正比：$F_{\text{fluid}} = -(\rho A L) \ddot{x}$。这里的 $M_a = \rho A L$ 就是附加质量。

在一个**整体式**或**强耦合**的框架下，这个力被隐式处理，耦合系统的[运动方程](@entry_id:170720)变为：
$$
m \ddot{x} + k x = -M_a \ddot{x} \quad \implies \quad (m + M_a) \ddot{x} + k x = 0
$$
这是一个稳定的[谐振子](@entry_id:155622)系统，其固有频率被[附加质量](@entry_id:267870)修正为 $\tilde{\omega}_n = \sqrt{k / (m + M_a)}$ [@problem_id:2560186]。

然而，在一个**松耦合**方案中，流体载荷的计算是基于前一时间步（或迭代步）的结构运动。因此，在 $t^n$ 时刻，结构感受到的流[体力](@entry_id:174230)是基于 $t^{n-1}$ 时刻的加速度计算的：$F_{\text{fluid}}^n = -M_a \ddot{x}^{n-1}$。结构的[运动方程](@entry_id:170720)变为：
$$
m \ddot{x}^n + k x^n = -M_a \ddot{x}^{n-1}
$$
在高频[振荡](@entry_id:267781)中，惯性项占主导地位，上式近似为 $m \ddot{x}^n \approx -M_a \ddot{x}^{n-1}$，即：
$$
\ddot{x}^n \approx -\left(\frac{M_a}{m}\right) \ddot{x}^{n-1}
$$
这是一个关于加速度的迭代关系。如果附加质量与结构质量的比值 $M_a/m > 1$（例如，轻质结构在重流体中，如水中的薄板或生物组织），那么每一次迭代，加速度的幅值都会被放大，导致[振荡](@entry_id:267781)发散。这就是所谓的**[附加质量不稳定性](@entry_id:174360)**。至关重要的是，这个不[稳定性判据](@entry_id:755304)与时间步长 $\Delta t$ 无关，因此单纯减小时间步长无法抑制这种不稳定性 [@problem_id:2560142]。

因此，对于[附加质量效应](@entry_id:746267)显著的问题，强耦合分离式方法或整体式方法是必须的。

### 处理移动域：[ALE方法](@entry_id:746347)与[几何守恒律](@entry_id:170384)

FSI问题的一个固有特征是流体域的边界会随着结构的运动而变形。为了在数值计算中处理这种移动和变形的网格，**任意拉格朗日-欧拉（Arbitrary Lagrangian-Eulerian, ALE）**方法被广泛采用。

在ALE框架下，[计算网格](@entry_id:168560)可以独立于物质点（[拉格朗日视角](@entry_id:265471)）和空间[固定点](@entry_id:156394)（[欧拉视角](@entry_id:265288)）运动。流体控制方程中的时间导数项被修改，以包含网格速度 $\boldsymbol{w}$ 的影响。例如，动量方程中的[对流](@entry_id:141806)项变为相对于网格的[对流](@entry_id:141806)速度 $(\boldsymbol{u}_f - \boldsymbol{w})$。

然而，[ALE方法](@entry_id:746347)引入了一个新的数值一致性要求，即**[几何守恒律](@entry_id:170384)（Geometric Conservation Law, GCL）**。GCL要求，即使在[网格运动](@entry_id:163293)的情况下，[数值格式](@entry_id:752822)也必须能够精确地保持一个[均匀流](@entry_id:272775)场（例如 $\boldsymbol{u} = \text{const}$）。换句话说，仅仅因为网格自身的运动，不应在计算中产生虚假的源项，从而污染物理守恒律的计算。在数学上，GCL要求对雅可比行列式 $J$ 的时间变化率（代表体积变化）的离散化，必须与对网格[速度散度](@entry_id:264117) $\nabla \cdot \boldsymbol{w}$ 的离散化相容 [@problem_id:2560158]。一个满足GCL的格式可以确保在一个移动的域上，均匀流场的动能变化完全由域体积的真实变化引起，而不会产生虚假的能量增益或耗散 [@problem_id:2560158] [@problem_id:2560149]。

GCL对于分离式方法尤为重要。在一个简单的交错式方案中，可能会出现这样的情况：在计算 $t^{n+1}$ 时刻的流场时，我们已经将网格移动到了由结构在 $t^{n+1}$ 时刻位移决定的新位置上，但用于ALE修正项中的网格速度 $\boldsymbol{w}$ 却是基于旧的时刻（例如 $\boldsymbol{w}^n$）计算的。这种几何信息和运动学信息的时间不匹配，直接违反了GCL，并同时在界面上引入了对[运动学](@entry_id:173318)条件 $\mathcal{O}(\Delta t)$ 的误差。这种不一致性是导致数值不稳定性的另一个重要来源 [@problem_id:2560149]。

为了恢复一致性，一种有效的策略是采用**预测-校正（predictor-corrector）**方法。在进行流体求解之前，首先利用已知的结构历史信息（如速度和加速度）预测一个在 $t^{n+1}$ 时刻的界面位移，并更新整个流体网格。然后，基于这个预测的网格位移和 $t^n$ 时刻的网格位移，计算一个时间上一致的网格速度 $\boldsymbol{w}$（例如，$\boldsymbol{w}^{n+1/2}$ 或 $\boldsymbol{w}^{n+1}$）。将这个一致的网格速度用于ALE项和[界面边界条件](@entry_id:203905)，可以恢复算法的一阶时间精度，并显著改善其稳定性 [@problem_id:2560149]。