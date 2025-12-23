## 引言
在计算岩[土力学](@entry_id:180264)领域，如何精确模拟材料中不连续性（如裂纹、断层和剪切带）的产生与演化，是理解岩土体复杂力学行为并确保工程结构安全的核心挑战。传统的连续介质有限元方法在处理这些几何和物理场均呈非连续特征的问题时，常常面临网格重构的巨大困难和计算精度的瓶颈。本文旨在系统性地介绍一套强大的数值工具——增强有限元技术与[水平集方法](@entry_id:165633)，它们能够在不依赖网格的情况下，优雅地处理不连续性的建模问题。

本文将引导读者逐步深入该领域的核心。在“原理与机制”一章中，我们将奠定理论基础，详细解析[单位分解法](@entry_id:170899)、[水平集](@entry_id:751248)几何描述以及针对不同不连续性的增强策略。接着，在“应用与跨学科联系”一章中，我们将通过[断裂力学](@entry_id:141480)、土体塑性以及水力-力学等多物理场耦合的实例，展示这些方法在解决实际工程与科学问题中的强大能力。最后，“动手实践”部分提供了精心设计的练习，旨在将理论知识转化为解决具体问题的实践技能。通过这三章的学习，读者将全面掌握利用增强与水平集技术进行[不连续性分析](@entry_id:170740)的原理、应用与实现要点。

## 原理与机制

本章旨在深入探讨使用增强技术和[水平集方法](@entry_id:165633)对岩[土力学](@entry_id:180264)中的[不连续性](@entry_id:144108)进行建模的核心原理与关键机制。在上一章介绍性讨论的基础上，我们将系统性地阐述这些方法的理论基础，从[不连续性](@entry_id:144108)的[运动学](@entry_id:173318)分类，到其几何表示，再到具体的数值增强策略和实现细节。

### [不连续性建模](@entry_id:165486)的基础概念

在深入研究数值方法之前，我们必须首先建立一个精确描述不连续性的物理和数学框架。

#### [不连续性](@entry_id:144108)的[运动学](@entry_id:173318)分类

在[连续介质力学](@entry_id:155125)中，不连续性通常根据[位移场](@entry_id:141476)及其梯度的连续性进行分类。考虑一个被内蕴界面 $\Gamma$ 分割的区域 $\Omega$，[位移场](@entry_id:141476) $\boldsymbol{u}$ 在 $\Omega \setminus \Gamma$ 上是分段光滑的。我们可以定义一个跳跃算子 $[\![ f ]\!] = f^+ - f^-$，它表示一个场 $f$ 穿过界面 $\Gamma$ 时，从正侧（由法向 $\boldsymbol{n}$ 指向的一侧）到负侧的变化。

**强不连续性 (Strong Discontinuity)** 代表了物理上的分离或滑移，例如裂纹的张开或断层的错动。其运动学特征是[位移场](@entry_id:141476)本身在界面上存在跳跃，即：
$$ [\![\boldsymbol{u}]\!] \neq \boldsymbol{0} $$
在这种情况下，即使位移场的经典梯度 $\nabla \boldsymbol{u}^{\pm}$ 在界面的两侧是有界的，位移场的[分布](@entry_id:182848)梯度（distributional gradient）也会包含一个集中在界面 $\Gamma$ 上的奇异部分。这个奇异部分与狄拉克面[分布](@entry_id:182848) $\delta_\Gamma$ 成正比，可以表示为 $[\![\boldsymbol{u}]\!] \otimes \boldsymbol{n} \, \delta_\Gamma$。这个奇异项代表了在零厚度的界面上存在无限大的应变。

**弱[不连续性](@entry_id:144108) (Weak Discontinuity)** 则代表了位移场中的“扭折”或“[尖点](@entry_id:636792)”，例如在[应变局部化](@entry_id:176973)带中。在这种情况下，材料在界面上保持连接，但应变场是不连续的。其运动学特征是位移场连续，但其梯度不连续：
$$ [\![\boldsymbol{u}]\!] = \boldsymbol{0}, \quad \text{但} \quad [\![\nabla \boldsymbol{u}]\!] \neq \boldsymbol{0} $$
由于[位移场](@entry_id:141476) $\boldsymbol{u}$ 是连续的，其一阶[分布](@entry_id:182848)梯度不包含狄拉克型的奇异项。[分布](@entry_id:182848)梯度 $\nabla \boldsymbol{u}$ 就是经典梯度，它本身是一个跨越 $\Gamma$ 的[不连续函数](@entry_id:143848)。因此，$\nabla \boldsymbol{u}$ 中没有支撑在 $\Gamma$ 上的[奇异测度](@entry_id:191565)。

正确区分这两种[不连续性](@entry_id:144108)至关重要，因为它们需要截然不同的数值处理和增强函数。

#### [单位分解法](@entry_id:170899)(PUM)：一种广义的增强框架

广义/扩展有限元方法 (GFEM/XFEM) 的核心思想是**[单位分解法](@entry_id:170899) (Partition of Unity Method, PUM)**。标准有限元方法的形函数 $\{N_i(\boldsymbol{x})\}$ 天然具有**[单位分解](@entry_id:150115) (Partition of Unity, PoU)** 性质，即在单元内的任意点 $\boldsymbol{x}$，形函数之和恒为1：
$$ \sum_{i=1}^{n_{\text{nodes}}} N_i(\boldsymbol{x}) = 1 $$
这个性质保证了标准有限元空间能够精确地再现常数场，这是保证收敛性的一个基本要求（完备性）。

PUM利用这一性质，通过将标准形函数与局部**增强函数 (enrichment functions)** $\psi(\boldsymbol{x})$ 相乘，来将关于解的先验知识（例如，不连续性或奇异性）“[植入](@entry_id:177559)”到近似空间中。一个增强的近似场 $u_h(\boldsymbol{x})$ 通常具有如下形式：
$$ u_h(\boldsymbol{x}) = \sum_{i \in \mathcal{I}} N_i(\boldsymbol{x}) u_i + \sum_{j \in \mathcal{J}} N_j(\boldsymbol{x}) \psi(\boldsymbol{x}) a_j $$
其中，第一项是标准的[有限元近似](@entry_id:166278)，第二项是增强部分。$\mathcal{I}$ 是所有节点的集合，而 $\mathcal{J}$ 是被选定要增强的节点[子集](@entry_id:261956)。

[单位分解](@entry_id:150115)性质的美妙之处在于它允许我们引入任意（通常是非多项式）的增强函数 $\psi(\boldsymbol{x})$，而不会破坏近似空间原有的多项式再现能力。这是因为标准有限元空间 $V_{\text{std}}$ 仍然是增强空间 $V_{\text{enr}}$ 的一个[子空间](@entry_id:150286)（只需令所有增强自由度 $a_j=0$ 即可获得）。因此，如果 $V_{\text{std}}$ 能够再现 $m$ 次多项式，那么 $V_{\text{enr}}$ 至少也能再现 $m$ 次多项式，从而保证了完备性不会降低。

更进一步，PoU性质使得增强空间有能力精确再现增强函数本身。对于任意函数 $\psi(\boldsymbol{x})$，我们可以写出：
$$ \psi(\boldsymbol{x}) = 1 \cdot \psi(\boldsymbol{x}) = \left(\sum_{i=1}^{n_{\text{nodes}}} N_i(\boldsymbol{x})\right) \psi(\boldsymbol{x}) = \sum_{i=1}^{n_{\text{nodes}}} N_i(\boldsymbol{x}) \psi(\boldsymbol{x}) $$
这意味着，如果我们对所有节点都进行增强，并取增强自由度为 $\psi(\boldsymbol{x})$ 在节点处的值，我们就能精确地表示 $\psi(\boldsymbol{x})$。虽然在实际操作中通常只对部分节点进行增强，但这揭示了PUM的内在能力。

### 不连续性的隐式几何表示：[水平集方法](@entry_id:165633)

为了在不依赖于网格的情况下描述复杂和演化中的不连续性，我们需要一种灵活的几何表示工具。**[水平集方法](@entry_id:165633) (Level Set Method, LSM)** 正是为此而生。

#### 用水平集函数定义界面

[水平集方法](@entry_id:165633)使用一个定义在整个计算域 $\Omega$ 上的高一维标量函数 $\phi(\boldsymbol{x})$ 来隐式地表示一个界面 $\Gamma$。界面被定义为 $\phi$ 的零[等值面](@entry_id:196027)：
$$ \Gamma = \{\boldsymbol{x} \in \Omega \mid \phi(\boldsymbol{x})=0\} $$
通常，$\phi(\boldsymbol{x})$ 被构造为一个**[符号距离函数](@entry_id:754834)**，即 $|\phi(\boldsymbol{x})|$ 表示点 $\boldsymbol{x}$ 到界面 $\Gamma$ 的最短距离。$\phi$ 的符号则用来区分界面的两侧：
$$ \phi(\boldsymbol{x}) \begin{cases} > 0  \text{在 } \Gamma \text{ 的一侧 (例如，外部)} \\  0  \text{在 } \Gamma \text{ 的另一侧 (例如，内部)} \end{cases} $$
这种[隐式表示](@entry_id:195378)方法极为强大，因为它将一个复杂的、可能随[时间演化](@entry_id:153943)的几何问题（追踪界面）转化为了一个在固定网格上求解标量函数 $\phi$ 的问题。[拓扑变化](@entry_id:136654)，如裂纹的合并或[分叉](@entry_id:270606)，可以被自然地处理，而无需复杂的网格重构。

#### 提取几何信息

一旦有了[水平集](@entry_id:751248)函数 $\phi(\boldsymbol{x})$，所有相关的几何信息都可以从中导出。其中最重要的是界面的**[单位法向量](@entry_id:178851) $\boldsymbol{n}$**，它由 $\phi$ 的梯度方向决定：
$$ \boldsymbol{n}(\boldsymbol{x}) = \frac{\nabla \phi(\boldsymbol{x})}{\|\nabla \phi(\boldsymbol{x})\|}, \quad \text{对于 } \boldsymbol{x} \in \Gamma $$
在有限元实现中，水平集函数 $\phi$ 像位移或其他场一样，通过节点值 $\phi_i$ 和形函数 $N_i$ 进行离散化：$\phi_h(\boldsymbol{x}) = \sum_i N_i(\boldsymbol{x}) \phi_i$。因此，在单元内的任意点（如积分点），我们可以计算出 $\phi_h$ 的梯度，进而得到法向量。

这个计算过程涉及到从父单元坐标 $(\xi, \eta)$ 到物理坐标 $(x, y)$ 的转换。根据[链式法则](@entry_id:190743)，物理梯度 $\nabla_{(x,y)}\phi_h$ 与父单元梯度 $\nabla_{(\xi,\eta)}\phi_h$ 之间的关系为：
$$ \nabla_{(x,y)}\phi_h = (\mathbf{J}^{-1})^T \nabla_{(\xi,\eta)}\phi_h $$
其中 $\mathbf{J}$ 是[坐标变换](@entry_id:172727)的[雅可比矩阵](@entry_id:264467)。

作为一个具体的例子，考虑一个四节点[四边形单元](@entry_id:176937)，其节点坐标和[水平集](@entry_id:751248)值为已知。我们可以首先计算雅可比矩阵 $\mathbf{J}$ 及其逆 $\mathbf{J}^{-1}$。然后，在父单元中心 $(\xi, \eta) = (0,0)$ 处计算 $\nabla_{(\xi,\eta)}\phi_h = (\frac{\partial \phi_h}{\partial \xi}, \frac{\partial \phi_h}{\partial \eta})^T$。最后，通过上述变换得到物理梯度 $\nabla_{(x,y)}\phi_h$。将其归一化，就得到了该点的[单位法向量](@entry_id:178851) $\boldsymbol{n}$。这个[法向量](@entry_id:264185)在定义位移跳跃的方向、建立界面本构关系（如内聚力模型）等方面起着至关重要的作用。

### 针对不同[不连续性](@entry_id:144108)的增强策略

根据[不连续性](@entry_id:144108)的[运动学](@entry_id:173318)分类，我们需要选择合适的增强函数。

#### 强不连续性（裂纹、断层）的建模

强[不连续性](@entry_id:144108)，即[位移场](@entry_id:141476)本身的不连续，是裂纹和断层问题的核心特征。

**Heaviside 增强**

为了在近似中引入一个跳跃，最自然的增强函数是**[Heaviside函数](@entry_id:176879)**（或其变体，如[符号函数](@entry_id:167507)），它基于水平集函数 $\phi$ 构建：
$$ H_{\Gamma}(\boldsymbol{x}) = \begin{cases} +1  \text{if } \phi(\boldsymbol{x}) \ge 0 \\ -1  \text{if } \phi(\boldsymbol{x})  0 \end{cases} $$
一个典型的增强位移近似可以写为：
$$ \boldsymbol{u}_h(\boldsymbol{x}) = \sum_{i \in \mathcal{I}} N_i(\boldsymbol{x}) \boldsymbol{u}_i + \sum_{j \in \mathcal{J}} N_j(\boldsymbol{x}) \left[ H_{\Gamma}(\boldsymbol{x}) - H_{\Gamma}(\boldsymbol{x}_j) \right] \boldsymbol{a}_j $$
这里，$\mathcal{J}$ 是其支撑域被界面 $\Gamma$ 切割的节点集合。增强部分采用了**平移的[Heaviside函数](@entry_id:176879)**。这种平移确保了在节点 $\boldsymbol{x}_j$ 处，增强项为零，从而使得节点自由度 $\boldsymbol{u}_j$ 仍然直接对应于该点的物理位移，极大地简化了[本质边界条件](@entry_id:173524)的施加。

通过这个增强形式，位移场在穿过界面 $\Gamma$ 时会产生一个跳跃。跳跃量 $[\![\boldsymbol{u}_h]\!]$ 可以计算为：
$$ [\![\boldsymbol{u}_h]\!](\boldsymbol{x}_{\Gamma}) = 2 \sum_{j \in \mathcal{J}} N_j(\boldsymbol{x}_{\Gamma}) \boldsymbol{a}_j $$
其中 $\boldsymbol{x}_{\Gamma}$ 是界面上的点。这表明，增强自由度 $\boldsymbol{a}_j$ 控制着位移跳跃的幅度。

将这种增强位移代入虚功原理的弱形式中，由于 $H_{\Gamma}$ 的梯度包含一个支撑在界面 $\Gamma$ 上的狄拉克[分布](@entry_id:182848)，内部[虚功](@entry_id:176403)项会自动产生一个界面积分项。这个界面积分项的形式为 $\int_{\Gamma} \boldsymbol{t}_{\Gamma} \cdot [\![\delta \boldsymbol{u}]\!] \, d\Gamma$，其中 $\boldsymbol{t}_{\Gamma}$ 是界面上的力，$[\![\delta \boldsymbol{u}]\!]$ 是[虚位移](@entry_id:168781)跳跃。正是通过这个项，我们可以施加界面的物理条件，例如无张力裂纹（$\boldsymbol{t}_{\Gamma} = \boldsymbol{0}$）或遵循特定[牵引-分离法则](@entry_id:170931)的[内聚力](@entry_id:274824)裂纹。

**裂尖增强 (LEFM)**

对于服从线弹性断裂力学 (LEFM) 的裂纹问题，仅使用Heaviside增强是不够的。LEFM预测，在裂纹尖端附近，应[力场](@entry_id:147325)和应变场会呈现一个 $r^{-1/2}$ 的奇异性，其中 $r$ 是到裂尖的距离。标准的Heaviside增强无法捕捉这种奇异行为。

为了解决这个问题，我们需要引入额外的**裂尖增强函数**，它们直接来自于裂尖渐近场的[Williams展开](@entry_id:183698)。对于二维平面问题，这些函数是[位移场](@entry_id:141476)的最低阶项，形式为 $\sqrt{r} f(\theta)$。一个标准的裂尖增强函数集包括四个函数：
$$ \mathcal{B}(\boldsymbol{x}) = \left\{ \sqrt{r} \sin\left(\frac{\theta}{2}\right), \sqrt{r} \cos\left(\frac{\theta}{2}\right), \sqrt{r} \sin\left(\frac{\theta}{2}\right)\sin(\theta), \sqrt{r} \cos\left(\frac{\theta}{2}\right)\sin(\theta) \right\} $$
注意：有时使用 $\sqrt{r}\sin(3\theta/2)$ 和 $\sqrt{r}\cos(3\theta/2)$ 作为后两个[基函数](@entry_id:170178)，它们与这里的形式是[线性等价](@entry_id:182886)的。

要使用这些函数，我们需要在每个点建立一个局部的极[坐标系](@entry_id:156346) $(r, \theta)$。这通常通过两个[水平集](@entry_id:751248)函数来实现：一个 $\phi(\boldsymbol{x})$ 描述到裂纹面的法向距离，另一个 $\psi(\boldsymbol{x})$ 描述沿裂纹切向到裂尖的距离。这样，[局部坐标](@entry_id:181200)可以方便地计算为 $r = \sqrt{\phi^2 + \psi^2}$ 和 $\theta = \operatorname{atan2}(\phi, \psi)$。

因此，一个完整的裂纹建模近似场包含三个部分：标准部分、应用于整个裂纹体的Heaviside增强部分，以及仅应用于包含裂尖的单元节点的裂尖增强部分。

#### 弱不连续性（剪切带）的建模

弱不连续性，即位移连续但梯度不连续，是模拟剪切带等[应变局部化](@entry_id:176973)现象的关键。

**[运动学](@entry_id:173318)与力学条件**

从虚功原理出发，可以推导出，在一个Cauchy连续体中，如果位移场（及其虚变分）跨界面 $\Gamma$ 是连续的，那么为了满足[动量平衡](@entry_id:193575)，界面上的柯西牵[引力](@entry_id:175476) $\boldsymbol{t} = \boldsymbol{\sigma n}$ 也必须是连续的：
$$ [\![\boldsymbol{t}]\!] = [\![\boldsymbol{\sigma n}]\!] = \boldsymbol{0} $$
然而，在标准的Cauchy模型中，[应变局部化](@entry_id:176973)会导致带厚度趋于零，从而引发数值上的[网格依赖性](@entry_id:198563)病态。[广义连续介质理论](@entry_id:193621)，如Cosserat（微极）介质或[应变梯度理论](@entry_id:180517)，通过引入一个**[内禀长度尺度](@entry_id:750789)**来正则化这个问题。这些理论包含了[高阶应力](@entry_id:186008)和高阶运动学量，其平衡方程要求相应的高阶广义牵[引力](@entry_id:175476)（如偶应力矩）在界面上也是连续的。[内禀长度尺度](@entry_id:750789)的存在为梯度提供了能量惩罚，从而使局部化带保持一个与该长度尺度相关的有限厚度。

**“扭折”增强**

为了在数值上模拟弱不连续性，我们需要一个能够使位移连续但梯度跳跃的增强函数。[Heaviside函数](@entry_id:176879)会引入位移跳跃，因此不适用。正确的选择是一个在界面上[连续但不可导](@entry_id:261860)的“扭折”函数。最典型的例子是基于水平集函数 $\phi$ 的[绝对值函数](@entry_id:160606)：
$$ \Psi(\boldsymbol{x}) = |\phi(\boldsymbol{x})| $$
这个函数是一个“斜坡”函数，它在 $\phi=0$ 处是连续的，但其梯度 $\nabla \Psi = \text{sign}(\phi) \nabla\phi$ 在 $\phi=0$ 处从 $-\nabla\phi$ 跳跃到 $+\nabla\phi$。将这个函数用于增强，可以自然地在近似位移场中引入一个梯度的跳跃，同时保持位移的连续性。

### [不连续性](@entry_id:144108)演化的机制

对于许多[地球科学](@entry_id:749876)问题，如[水力压裂](@entry_id:750442)或断层扩展，[不连续性](@entry_id:144108)是动态演化的。[水平集方法](@entry_id:165633)提供了一个优雅的框架来处理这种演化。

#### 水平集[对流](@entry_id:141806)方程

假设[不连续性](@entry_id:144108)界面 $\Gamma(t)$ 上的每一点都随着一个给定的速度场 $\boldsymbol{v}(\boldsymbol{x},t)$ 运动。由于界面上的点始终满足 $\phi(\boldsymbol{x}(t), t) = 0$，其随时间的[全导数](@entry_id:137587)（物质导数）也必须为零：
$$ \frac{D\phi}{Dt} = \frac{\partial \phi}{\partial t} + \nabla \phi \cdot \frac{d\boldsymbol{x}}{dt} = 0 $$
将点的速度 $\frac{d\boldsymbol{x}}{dt} = \boldsymbol{v}$ 代入，我们得到描述[水平集](@entry_id:751248)函数 $\phi$ 演化的欧拉[偏微分方程](@entry_id:141332)，即**[对流](@entry_id:141806)方程**：
$$ \frac{\partial \phi}{\partial t} + \boldsymbol{v} \cdot \nabla \phi = 0 $$
这是一个一阶[双曲型方程](@entry_id:145657)，它表明 $\phi$ 的值沿着[速度场](@entry_id:271461) $\boldsymbol{v}$ 的[流线](@entry_id:266815)保持不变。通过在固定的欧拉网格上求解这个方程，我们就可以追踪界面的运动。

#### 断裂扩展准则与水平集更新

在断裂问题中，界面的速度场 $\boldsymbol{v}$ 并非预先给定的，而是由材料的断裂行为决定的。[断裂力学](@entry_id:141480)提供了确定裂纹何时以及向何处扩展的准则。

一个经典的准则是**最大周向应力 (Maximum Circumferential Stress, MCS) 准则**。该准则假设裂纹会沿着裂尖前方周向（环向）应力 $\sigma_{\theta\theta}$ 达到最大值的方向 $\theta_c$ 扩展。在二维混合模式（I型和II型）加载下，这个方向 $\theta_c$ 可以通过[应力强度因子](@entry_id:183032) $K_I$ 和 $K_{II}$ 来确定。求解 $\partial \sigma_{\theta\theta} / \partial \theta = 0$（或等价地，$\sigma_{r\theta}=0$）可以得到扩展角：
$$ \theta_c = 2 \arctan\left[ \frac{1}{4} \left( \frac{K_I}{K_{II}} - \sqrt{\left(\frac{K_I}{K_{II}}\right)^2 + 8} \right) \right] \quad (\text{对于 } K_{II} \neq 0) $$
对于纯I型加载（$K_{II}=0$），$\theta_c=0$，即裂纹沿直线扩展。

一旦确定了扩展方向，裂纹扩展的速度大小 $v$ 可以由一个动力学法则（如Paris法则）给出，它通常也依赖于 $K_I$ 和 $K_{II}$。界面的运动只依赖于其法向速度 $v_n = \boldsymbol{v} \cdot \boldsymbol{n}$。因此，[对流](@entry_id:141806)方程可以写成更通用的**Hamilton-Jacobi形式**：
$$ \frac{\partial \phi}{\partial t} + v_n |\nabla \phi| = 0 $$
其中 $v_n$ 是裂尖的法向速度，由物理准则确定。通过求解这个方程，就可以更新水平集函数，从而模拟裂纹的扩展。

### 数值实现：关键机制与挑战

将上述原理转化为一个稳健的数值代码需要克服几个关键的实现挑战。

#### 不连续场上的积分：子单元求积

在计算[单元刚度矩阵](@entry_id:139369)或[内力向量](@entry_id:750751)时，需要计算形如 $\int_K f(\boldsymbol{x}) \, d\boldsymbol{x}$ 的积分。对于被[不连续性](@entry_id:144108)切割的单元，被积函数通常是[分段多项式](@entry_id:634113)，例如，它可能包含[Heaviside函数](@entry_id:176879) $H_{\Gamma}(\boldsymbol{x})$。标准的**高斯求积 (Gaussian Quadrature)** 法则是为光滑的（多项式）被积函数设计的，其求积点和权重的选择是为了精确积分多项式。当被积函数在积分域内部存在跳跃不连续时，[高斯求积](@entry_id:146011)的理论基础被破坏，导致积分结果不准确。

例如，对于一维积分 $\int_{-1}^{1} H(x) x \, dx$，其精确值为 $1/2$。但一个2点高斯求积会给出 $1/\sqrt{3}$，这是一个显著的误差。

正确的处理方法是**子单元求积 (Subcell Quadrature)**。其核心思想是：
1.  **几何剖分**：利用[水平集](@entry_id:751248)函数 $\phi$ 将被切割的单元 $K$ 剖分为两个或多个子单元，例如 $K^+ = \{\boldsymbol{x} \in K \mid \phi(\boldsymbol{x})>0\}$ 和 $K^- = \{\boldsymbol{x} \in K \mid \phi(\boldsymbol{x})0\}$。
2.  **分片积分**：在每个子单元上，被积函数（如 $q(\boldsymbol{x}) H_{\Gamma}(\boldsymbol{x})$）都变成了光滑的多项式（在 $K^+$ 上为 $q(\boldsymbol{x})$，在 $K^-$ 上为 $0$）。
3.  **精确求积**：在每个子单元上应用标准的[高斯求积法](@entry_id:146011)则。由于被积函数在子单元上是多项式，只要选取足够高阶的求积法则，就可以保证积分的精确性。

通过这种方式，我们将一个在复杂域上的[不连续函数](@entry_id:143848)积分问题，转化为了若干个在简单域（如三角形或四面体）上的多项式积分问题，从而保证了计算的精度。

#### 混合单元问题与[单位分解](@entry_id:150115)修正

当一个单元的某些节点被增强，而另一些节点没有被增强时，就会出现问题。这种情况发生在一个未被[不连续性](@entry_id:144108)切割，但与被切割单元相邻的单元中。这种单元被称为**混合单元 (blending element)**。

在混合单元中，用于增强的形函数集合（即仅与增强节点相关的那些形函数）之和不再等于1。也就是说，增强空间的单位分解特性被破坏了。其后果是，增强的近似空间甚至无法精确再现增强函数本身，这会导致收敛性变差和精度损失。

举一个简单的一维例子：考虑一个单元 $[1,2]$，其节点1被增强，而节点2未被增强。该单元内的增强[基函数](@entry_id:170178)只有 $N_1(x)\psi(x)$。我们无法找到一个常数增强自由度 $a_1$ 使得 $N_1(x)\psi(x)a_1 = \psi(x)$ 在整个单元上成立（除非 $N_1(x)=1$，但这显然不成立）。

为了解决这个问题，需要对增强函数进行修正，以在混合单元区域内恢复[单位分解](@entry_id:150115)特性。常用的方法包括使用“[斜坡函数](@entry_id:273156)”或其他过渡函数来平滑地将增强从增强区域过渡到非增强区域。

#### 通过[正交化](@entry_id:149208)缓解[病态问题](@entry_id:137067)

当在同一个单元中使用多个增强函数时（例如，同时使用[Heaviside函数](@entry_id:176879)和裂尖函数，或[Heaviside函数](@entry_id:176879)和扭折函数），这些函数之间可能存在近似的线性相关性。这会导致有限元系统矩阵（如[质量矩阵](@entry_id:177093)或[刚度矩阵](@entry_id:178659)）变得**病态 (ill-conditioned)**。

一个矩阵的条件数（如谱[条件数](@entry_id:145150) $\kappa_2(M) = \lambda_{\max}/\lambda_{\min}$）衡量了其对输入的扰动的敏感性。一个大的[条件数](@entry_id:145150)意味着微小的输入误差（如[舍入误差](@entry_id:162651)）可能被放大，导致解的精度严重下降。

基[函数的线性相关性](@entry_id:186071)体现在其**格拉姆矩阵 (Gram matrix)** $G$ 上，其元素为 $G_{ij} = \langle b_i, b_j \rangle$，其中 $\langle \cdot, \cdot \rangle$ 是适当的[内积](@entry_id:158127)。如果[基函数](@entry_id:170178)非正交，格拉姆矩阵就不是单位阵，其条件数可能很大。

为了缓解这个问题，可以在单元层面对增强[基函数](@entry_id:170178)进行**[正交化](@entry_id:149208)**处理。例如，可以使用**格拉姆-施密特 (Gram-Schmidt)** 过程，将原始的线性相关的[基函数](@entry_id:170178)集合 $\{b_i\}$ 转化为一个标准正交基集合 $\{u_i\}$。对于一个标准正交基，其[格拉姆矩阵](@entry_id:203297)就是单位矩阵 $I$，其条件数为 $\kappa_2(I)=1$，这是最优的。通过在正交化后的基上构建有限元方程，可以显著改善系统[矩阵的[条件](@entry_id:150947)数](@entry_id:145150)，从而提高数值解的稳定性和精度。