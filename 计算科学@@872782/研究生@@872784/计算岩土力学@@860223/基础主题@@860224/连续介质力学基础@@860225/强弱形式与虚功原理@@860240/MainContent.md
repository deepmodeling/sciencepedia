## 引言
在现代[计算力学](@entry_id:174464)，尤其是计算岩[土力学](@entry_id:180264)领域，将描述物理世界的连续介质模型转化为计算机可以求解的离散方程，是一项根本性的任务。这一转化的核心，是从描述点态物理定律的“强形式”（通常为[偏微分方程](@entry_id:141332)）过渡到其等价的积分“弱形式”。这一过程不仅是有限元法等强大数值工具的理论基石，也深刻地影响着我们如何处理边界条件、[材料非线性](@entry_id:162855)以及复杂的[多物理场耦合](@entry_id:171389)问题。

直接求解强形式方程对于真实世界的复杂几何形状、材料异质性和[非线性](@entry_id:637147)行为往往极其困难甚至不切实际。因此，理解如何系统地、严谨地“弱化”这些方程，是所有计算力学研究者和工程师必须掌握的关键技能。

本文旨在系统地阐明这一关键转化过程。在第一章“原理与机制”中，我们将以静态[平衡问题](@entry_id:636409)为例，详细介绍如何利用[虚功原理](@entry_id:138749)从强形式推导出弱形式，并阐明边界条件、[功共轭](@entry_id:194957)对等核心概念。接下来，在第二章“应用与跨学科联系”中，我们将展示这一理论框架如何被广泛应用于解决从经典岩土工程到复杂的多物理场耦合、结构相互作用乃至动力学等前沿问题。最后，在第三章“动手实践”中，你将通过一系列精心设计的练习，亲手实践弱形式的推导与应用，将理论知识转化为解决实际问题的能力。

通过这三个章节的学习，读者将建立起对强弱形式转换的深刻理解，为深入学习和应用高级计算方法打下坚实的基础。

## 原理与机制

在计算岩[土力学](@entry_id:180264)中，将物理定律转化为可计算的离散方程是核心任务。这一转化过程的核心在于将描述连续[体力](@entry_id:174230)学行为的强形式（通常是[偏微分方程](@entry_id:141332)）转换为等价的弱形式（积分形式）。本章将系统地阐述这一过程背后的基本原理与机制，重点关注虚功原理的应用。我们将从静态平衡的强形式出发，逐步推导出其[弱形式](@entry_id:142897)，并在此过程中阐明各种边界条件的处理方式、[运动学](@entry_id:173318)关系、[功共轭应力](@entry_id:182069)-应变对以及该数学框架的严谨性。

### 平衡的强形式

对于一个在静态或准静态条件下（即忽略惯性效应）的连续体，其内部任何一点都必须满足[线性动量守恒](@entry_id:165717)，这也被称为柯西（Cauchy）第一运动定律。该定律的局部表达式构成了力学问题的**强形式**（strong form）或点态平衡方程。考虑一个占据空间域 $\Omega$ 的土体，其[平衡方程](@entry_id:172166)可以写作：

$$
\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}
$$

在此方程中：
- $\boldsymbol{\sigma}$ 是**柯西[应力张量](@entry_id:148973)**，代表物体内部单位面积上的内力[分布](@entry_id:182848)。在[国际单位制](@entry_id:172547)（SI）中，其单位为帕斯卡（Pa）或牛顿每平方米（$\mathrm{N/m^2}$）。
- $\mathbf{b}$ 是**体力**（body force），代表作用在物体体积上的力，例如重力。在岩土工程中，体力通常指单位体积的自重，其单位为牛顿每立方米（$\mathrm{N/m^3}$）。有时，[体力](@entry_id:174230)也可能被定义为单位质量的力（例如重力加速度 $\mathbf{g}$，单位为 $\mathrm{m/s^2}$），此时平衡方程写作 $\nabla \cdot \boldsymbol{\sigma} + \rho\mathbf{b} = \mathbf{0}$，其中 $\rho$ 是材料的质量密度（单位 $\mathrm{kg/m^3}$）[@problem_id:3565492]。
- $\nabla \cdot$ 是[散度算子](@entry_id:265975)。

这个[偏微分方程](@entry_id:141332)必须在域 $\Omega$ 内的每一点都成立。然而，仅有此方程不足以确定一个唯一解。我们还需要在物体的边界 $\Gamma$ 上施加**边界条件**（boundary conditions），以完整地定义一个[边值问题](@entry_id:193901)。

### 边界条件：本质与自然

在连续[体力](@entry_id:174230)学中，边界条件主要分为两类：[本质边界条件和自然边界条件](@entry_id:168198)。正确区分和处理这两类边界条件对于建立正确的弱形式至关重要。

**[本质边界条件](@entry_id:173524)**（Essential Boundary Conditions），也称为狄利克雷（Dirichlet）条件，直接对问题的主要场变量（在固体力学中通常是位移 $\mathbf{u}$）进行约束。它们在边界的特定部分 $\Gamma_u$ 上规定了位移的值：

$$
\mathbf{u} = \bar{\mathbf{u}} \quad \text{在 } \Gamma_u \text{ 上}
$$

其中 $\bar{\mathbf{u}}$ 是已知的位移函数。一个典型的例子是模拟一个紧贴着**刚性挡土墙**的土体。如果墙体完全刚性且固定不动，那么在土与墙的接触面 $\Gamma_w$ 上，土体法向位移必须为零，即 $\mathbf{u} \cdot \mathbf{n}_w = 0$（其中 $\mathbf{n}_w$ 是墙面的法向量）[@problem_id:3565452]。这种直接施加在[位移场](@entry_id:141476)上的约束，必须在求解过程的初始阶段就得到“强行”满足。

**自然边界条件**（Natural Boundary Conditions），也称为诺伊曼（Neumann）条件，涉及主要场变量的导数。在[固体力学](@entry_id:164042)中，这通常表现为对**面力**（traction）的规定。根据柯西原理，边界上某点的[面力矢量](@entry_id:189429) $\mathbf{t}$ 与该点的[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 和边界外[法线](@entry_id:167651)矢量 $\mathbf{n}$ 之间存在关系 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$。因此，自然边界条件在边界的特定部分 $\Gamma_t$ 上规定了面力的值：

$$
\boldsymbol{\sigma}\mathbf{n} = \bar{\mathbf{t}} \quad \text{在 } \Gamma_t \text{ 上}
$$

其中 $\bar{\mathbf{t}}$ 是已知的面力[分布](@entry_id:182848)。例如，在地面上施加的均布荷载 $q$ 就是一种自然边界条件[@problem_id:3565452]。与本质条件不同，自然条件在推导弱形式的过程中会“自然地”出现，并通[过积分](@entry_id:753033)形式得到“弱”满足。

在某些更复杂的情况下，边界条件可能将位移和面力联系起来，形成**[混合边界条件](@entry_id:176456)**（Mixed Boundary Conditions）或罗宾（Robin）条件。例如，模拟一个放置在[弹性地基](@entry_id:186539)上的基础板时，地基的反力可能与基础的沉降成正比。若采用[Winkler地基模型](@entry_id:756736)，其边界条件可表示为 $\boldsymbol{\sigma}\mathbf{n} + k_s (\mathbf{u} \cdot \mathbf{n})\mathbf{n} = \mathbf{0}$，其中 $k_s$ 是地基刚度。这种条件也属于自然边界条件的范畴，因为它涉及应力（位移的导数）[@problem_id:3565527]。

值得注意的是，同一个物理边界上可能同时存在不同类型的条件。一个经典的例子是**对称边界**。在[对称面](@entry_id:198308)上，法向位移为零（$u_n = 0$），这是一个本质条件；同时，切向面力为零（$t_t = 0$），这是一个自然条件。因此，一个[对称面](@entry_id:198308)既是本质边界的一部分，又是自然边界的一部分[@problem_id:3565527]。

### 虚功原理：从强形式到[弱形式](@entry_id:142897)

直接求解强形式的[偏微分方程](@entry_id:141332)通常非常困难，尤其对于具有复杂几何形状和[材料非线性](@entry_id:162855)的岩土工程问题。因此，我们引入**虚功原理**（Principle of Virtual Work, PVW），将强形式转化为等价的**[弱形式](@entry_id:142897)**（weak form）或[变分形式](@entry_id:166033)。[弱形式](@entry_id:142897)是一个[积分方程](@entry_id:138643)，相比于要求在每一点都成立的强形式，它对解的连续性要求更低，更适合于数值近似，如有限单元法（FEM）。

推导过程的核心思想是：如果一个物体处于平衡状态，那么对于任何满足[运动学](@entry_id:173318)约束的、任意微小的**[虚位移](@entry_id:168781)**（virtual displacement）$\delta\mathbf{u}$，所有外力（[体力](@entry_id:174230)、面力）所做的总[虚功](@entry_id:176403)必定等于所有内力（应力）所做的总[虚功](@entry_id:176403)。

数学上，我们通过以下步骤实现这一转换：
1.  将强形式[平衡方程](@entry_id:172166) $\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}$ 的两边点乘一个**容许的**（admissible）[虚位移](@entry_id:168781)场 $\delta\mathbf{u}$。
2.  在整个求解域 $\Omega$ 上进行积分：
    $$
    \int_{\Omega} (\nabla \cdot \boldsymbol{\sigma} + \mathbf{b}) \cdot \delta\mathbf{u} \, \mathrm{d}\Omega = 0
    $$

    此处的**容许[虚位移](@entry_id:168781)** $\delta\mathbf{u}$ 必须是[运动学](@entry_id:173318)上可能的，并且满足所有[本质边界条件](@entry_id:173524)的齐次形式。也就是说，如果在边界 $\Gamma_u$ 上规定了位移 $\mathbf{u} = \bar{\mathbf{u}}$，那么[虚位移](@entry_id:168781)在该边界上必须为零，即 $\delta\mathbf{u} = \mathbf{0}$ 在 $\Gamma_u$ 上[@problem_id:3565452] [@problem_id:3565519]。

3.  将积分拆分并应用**[散度定理](@entry_id:143110)**（即高斯-奥斯特罗格拉德斯基定理或分部积分）于应力项：
    $$
    \int_{\Omega} (\nabla \cdot \boldsymbol{\sigma}) \cdot \delta\mathbf{u} \, \mathrm{d}\Omega = \int_{\Gamma} (\boldsymbol{\sigma}\mathbf{n}) \cdot \delta\mathbf{u} \, \mathrm{d}\Gamma - \int_{\Omega} \boldsymbol{\sigma} : \nabla(\delta\mathbf{u}) \, \mathrm{d}\Omega
    $$
    这一步是关键，它将对 $\boldsymbol{\sigma}$ 的[微分](@entry_id:158718)转移到了对 $\delta\mathbf{u}$ 的[微分](@entry_id:158718)上，从而降低了对应[力场](@entry_id:147325)连续性的要求。同时，它引入了边界积分项 $\int_{\Gamma} (\boldsymbol{\sigma}\mathbf{n}) \cdot \delta\mathbf{u} \, \mathrm{d}\Gamma$，其中包含了面力 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$。

4.  将此结果代回原积分方程，并重新整理，我们得到虚功原理的经典陈述：
    $$
    \underbrace{\int_{\Omega} \boldsymbol{\sigma} : \nabla(\delta\mathbf{u}) \, \mathrm{d}\Omega}_{\delta W_{\text{int}}} = \underbrace{\int_{\Omega} \mathbf{b} \cdot \delta\mathbf{u} \, \mathrm{d}\Omega + \int_{\Gamma} \mathbf{t} \cdot \delta\mathbf{u} \, \mathrm{d}\Gamma}_{\delta W_{\text{ext}}}
    $$
    等式左边是**内力[虚功](@entry_id:176403)**（internal virtual work），右边是**外力[虚功](@entry_id:176403)**（external virtual work）。

5.  最后，我们应用边界条件来处理边界积分项。边界 $\Gamma$ 分为本质边界 $\Gamma_u$ 和自然边界 $\Gamma_t$。
    -   在 $\Gamma_u$ 上，根据容许[虚位移](@entry_id:168781)的定义，$\delta\mathbf{u} = \mathbf{0}$。因此，该部分边界上的积分 $\int_{\Gamma_u} \mathbf{t} \cdot \delta\mathbf{u} \, \mathrm{d}\Gamma$ 为零。这巧妙地消除了未知的反力 $\mathbf{t}$ 在[弱形式](@entry_id:142897)中的显式出现[@problem_id:3565452]。
    -   在 $\Gamma_t$ 上，面力是已知的，$\mathbf{t} = \bar{\mathbf{t}}$。因此，该部分积分成为 $\int_{\Gamma_t} \bar{\mathbf{t}} \cdot \delta\mathbf{u} \, \mathrm{d}\Gamma$，这是一个已知的载荷项。

至此，我们得到了准静态问题的最终弱形式：求解位移场 $\mathbf{u}$（满足在 $\Gamma_u$ 上的[本质边界条件](@entry_id:173524)），使得对于所有容许的[虚位移](@entry_id:168781) $\delta\mathbf{u}$（满足在 $\Gamma_u$ 上 $\delta\mathbf{u}=\mathbf{0}$），以下方程成立：
$$
\int_{\Omega} \boldsymbol{\sigma}(\mathbf{u}) : \delta\boldsymbol{\varepsilon}(\delta\mathbf{u}) \, \mathrm{d}\Omega = \int_{\Omega} \rho\mathbf{b} \cdot \delta\mathbf{u} \, \mathrm{d}\Omega + \int_{\Gamma_t} \bar{\mathbf{t}} \cdot \delta\mathbf{u} \, \mathrm{d}\Gamma
$$
这里，我们将[内力](@entry_id:167605)[虚功](@entry_id:176403)中的虚[位移梯度](@entry_id:165352) $\nabla(\delta\mathbf{u})$ 替换为了虚应变 $\delta\boldsymbol{\varepsilon}(\delta\mathbf{u})$。这一替换将在下一节中详细阐述。这个方程明确展示了，自然边界条件是通过外力[虚功](@entry_id:176403)项以积分形式（即“弱”形式）被满足的[@problem_id:3565489]。

### [运动学](@entry_id:173318)与[功共轭](@entry_id:194957)对

[弱形式](@entry_id:142897)中的内力[虚功](@entry_id:176403)项 $\int_{\Omega} \boldsymbol{\sigma} : \nabla(\delta\mathbf{u}) \, \mathrm{d}\Omega$ 值得我们进一步探究。它揭示了应力与应变度量之间的深刻联系，即**[功共轭](@entry_id:194957)**（work-conjugacy）关系。

在**小应变**（small-strain）理论框架下，我们假设[位移梯度](@entry_id:165352) $\nabla\mathbf{u}$ 的所有分量都远小于1（$\|\nabla\mathbf{u}\| \ll 1$）。这意味着应变和转动都必须是微小的[@problem_id:3565472]。在此假设下，应变被定义为**[无穷小应变张量](@entry_id:167211)**（infinitesimal strain tensor）：
$$
\boldsymbol{\varepsilon}(\mathbf{u}) = \frac{1}{2}\left(\nabla\mathbf{u} + (\nabla\mathbf{u})^T\right)
$$
这是一个线性算子，它只保留了[位移梯度](@entry_id:165352)的对称部分。为什么只取对称部分呢？答案就在于[功共轭](@entry_id:194957)。根据角动量守恒，在没有体力偶的情况下，柯西应力张量 $\boldsymbol{\sigma}$ 必须是对称的。任何二阶张量（如虚[位移梯度](@entry_id:165352) $\nabla(\delta\mathbf{u})$）都可以分解为其对称部分和反对称部分。一个[对称张量](@entry_id:148092)与一个[反对称张量](@entry_id:199349)的[双点积](@entry_id:748648)恒为零。因此：
$$
\boldsymbol{\sigma} : \nabla(\delta\mathbf{u}) = \boldsymbol{\sigma} : \left( \text{sym}(\nabla(\delta\mathbf{u})) + \text{skew}(\nabla(\delta\mathbf{u})) \right) = \boldsymbol{\sigma} : \text{sym}(\nabla(\delta\mathbf{u})) = \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\delta\mathbf{u})
$$
这表明，做功的只有[位移梯度](@entry_id:165352)的对称部分，即虚应变。因此，柯西应力 $\boldsymbol{\sigma}$ 与[无穷小应变](@entry_id:197162) $\boldsymbol{\varepsilon}$ 构成了一对**[功共轭](@entry_id:194957)**的应力-[应变度量](@entry_id:755495)。这是将 $\boldsymbol{\varepsilon}$ 定义为[位移梯度](@entry_id:165352)对称部分的根本物理原因[@problem_id:3565472] [@problem_id:3565492]。

当变形不可忽略时，我们必须进入**[大应变](@entry_id:751152)**（large-strain）或有限应变（finite-strain）的领域。此时，[小应变张量](@entry_id:754968)不再适用，因为它不是**客观的**（objective），即它在[刚体转动](@entry_id:191086)下不会保持不变。取而代之，我们使用**[格林-拉格朗日应变张量](@entry_id:187745)**（Green-Lagrange strain tensor）：
$$
\mathbf{E} = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I})
$$
其中 $\mathbf{F} = \mathbf{I} + \nabla\mathbf{u}$ 是**变形梯度**（deformation gradient），$\mathbf{I}$ 是单位张量。$\mathbf{E}$ 与 $\boldsymbol{\varepsilon}$ 之间的精确关系是 $\mathbf{E} = \boldsymbol{\varepsilon} + \frac{1}{2}(\nabla\mathbf{u})^T(\nabla\mathbf{u})$。只有当[位移梯度](@entry_id:165352)的二次项可以忽略时，$\mathbf{E} \approx \boldsymbol{\varepsilon}$。与 $\boldsymbol{\varepsilon}$ 不同，$\mathbf{E}$ 对于任意[刚体转动](@entry_id:191086)其值均为零，因此是一个客观的[应变度量](@entry_id:755495)[@problem_id:3565508]。

在[大应变](@entry_id:751152)框架下，应力度量也需要相应调整。与[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$ [功共轭](@entry_id:194957)的应力度量是**[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量**（Second Piola-Kirchhoff stress, $\mathbf{S}$）。而在另一种描述中，与变形梯度 $\mathbf{F}$ [功共轭](@entry_id:194957)的是**[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量**（First Piola-Kirchhoff stress, $\mathbf{P}$）。这些应力度量都与柯西应力 $\boldsymbol{\sigma}$ 相关联，但定义在未变形的参考构型上。内力[虚功](@entry_id:176403)可以在不同构型下等价地表示[@problem_id:3565511]：
$$
\delta W_{\text{int}} = \int_{\Omega_t} \boldsymbol{\sigma} : \delta\mathbf{d} \, \mathrm{d}v = \int_{\Omega_0} \mathbf{P} : \delta\mathbf{F} \, \mathrm{d}V_0 = \int_{\Omega_0} \mathbf{S} : \delta\mathbf{E} \, \mathrm{d}V_0
$$
其中 $\Omega_0$ 和 $\Omega_t$ 分别是参考构型和当前构型，$\mathbf{d}$ 是变形率张量（[虚位移](@entry_id:168781)在当前构型下的对称梯度）。这表明 $(\boldsymbol{\sigma}, \mathbf{d})$、$(\mathbf{P}, \mathbf{F})$ 和 $(\mathbf{S}, \mathbf{E})$ 都是合法的[功共轭](@entry_id:194957)对[@problem_id:3565508]。

### 数学框架：函数空间

为了给弱形式提供一个严谨的数学基础，我们需要引入**函数空间**（function spaces）的概念。由于[弱形式](@entry_id:142897)涉及位移场的一阶导数（即应变），并且要求[能量积分](@entry_id:166228)（如 $\int \boldsymbol{\sigma}:\boldsymbol{\varepsilon} \, \mathrm{d}\Omega$）是有限的，因此位移场及其一阶导数都必须是平方可积的。

满足这一条件的函数所构成的空间被称为**[索博列夫空间](@entry_id:141995)**（Sobolev space），记为 $H^1(\Omega)$。对于矢量场（如位移），我们使用 $[H^1(\Omega)]^d$。其严格定义为：
$$
H^1(\Omega; \mathbb{R}^d) = \{\mathbf{u} \in [L^2(\Omega)]^d : \nabla\mathbf{u} \in [L^2(\Omega)]^{d \times d}\}
$$
其中 $L^2(\Omega)$ 是[平方可积函数](@entry_id:200316)的空间，导数是在**[弱导数](@entry_id:189356)**（weak derivative）意义下定义的[@problem_id:3565494]。

在这个框架下，弱形式的提法变得更加精确：
-   **[试探函数](@entry_id:756165)空间**（Trial space）：寻求的解 $\mathbf{u}$ 必须属于一个函数集合，该集合中的函数满足 $H^1$ 正则性，并满足非齐次的本质边界条件 $\mathbf{u} = \bar{\mathbf{u}}$ 在 $\Gamma_u$ 上。
-   **检验函数空间**（Test space）$V_0$：[虚位移](@entry_id:168781) $\delta\mathbf{u}$ 必须属于一个[向量空间](@entry_id:151108)，该空间中的函数也满足 $H^1$ 正则性，并满足齐次的[本质边界条件](@entry_id:173524) $\delta\mathbf{u} = \mathbf{0}$ 在 $\Gamma_u$ 上。因此，
    $$
    V_0 = \{\delta\mathbf{u} \in H^1(\Omega; \mathbb{R}^d) : \delta\mathbf{u} = \mathbf{0} \text{ on } \Gamma_u\}
    $$
    边界条件在[索博列夫空间](@entry_id:141995)的意义下由“迹”（trace）定理来保证[@problem_id:3565494]。

### 应用与推广：实际考量

将强形式转化为[弱形式](@entry_id:142897)不仅是理论上的优雅，更在数值计算中具有深刻的实际意义和影响。

首先，自然边界条件的“弱”施加方式意味着，如果对 prescribed traction $\bar{\mathbf{t}}$ 的应用出现错误（例如，大小、方向或位置错误），其影响将是全局性的。这是一个**[一致性误差](@entry_id:747725)**（consistency error），它不会随着网格的加密而消失。解将收敛到一个错误问题的精确解，导致整个域内的位移和应[力场](@entry_id:147325)产生系统性偏差[@problem_id:3565489]。

其次，弱形式的表述也与[刚体运动](@entry_id:193355)和全局平衡紧密相关。如果施加的体力 $\mathbf{b}$ 和面力 $\bar{\mathbf{t}}$ 不是自平衡的，并且[本质边界条件](@entry_id:173524)不足以约束所有的[刚体运动](@entry_id:193355)模态，那么静态[平衡解](@entry_id:174651)将不存在。弱形式能够敏锐地捕捉到这一点：对于一个纯刚体[虚位移](@entry_id:168781)（其虚应变为零，因此[内力](@entry_id:167605)[虚功](@entry_id:176403)为零），如果外力[虚功](@entry_id:176403)不为零，则表明外力不平衡，离散后的[刚度矩阵](@entry_id:178659)将是奇异的[@problem_id:3565489]。

最后，标准的位移法[弱形式](@entry_id:142897)在处理某些特殊材料时会遇到困难。一个典型的例子是**[体积锁定](@entry_id:172606)**（volumetric locking）现象，它发生在模拟[近不可压缩材料](@entry_id:752388)（如饱和土的不排水行为）时。对于这类材料，体积模量 $K$ 远大于剪切模量 $G$。在位移法弱形式中，体积能项 $\int K (\nabla \cdot \mathbf{u})^2 \mathrm{d}\Omega$ 起到了一个罚函数的作用，迫使[体积应变](@entry_id:267252) $\nabla \cdot \mathbf{u}$ 趋近于零。然而，对于低阶有限元（如线性单元），其离散的[位移场](@entry_id:141476)模式非常有限，难以在满足一般变形的同时精确满足 $\nabla \cdot \mathbf{u}^h = 0$ 的约束。这种[运动学](@entry_id:173318)上的不匹配导致系统被人为地“锁死”，表现出远超实际的刚度[@problem_id:3565512]。

为了解决[体积锁定](@entry_id:172606)，**[混合格式](@entry_id:167436)**（mixed formulation）应运而生。在 **u-p [混合格式](@entry_id:167436)**中，我们将[静水压力](@entry_id:275365) $p$ 作为一个独立的未知场引入。原来的[不可压缩性](@entry_id:274914)条件 $\nabla \cdot \mathbf{u} = 0$ 被作为一个[约束方程](@entry_id:138140)，通过拉格朗日乘子法（其中压力 $p$ 扮演拉格朗日乘子的角色）弱化地施加。这种方法通过为位移和压力选择满足特定数学条件（即 LBB 或 [inf-sup 条件](@entry_id:174538)）的离散函数空间，可以在不产生锁定的情况下获得稳定且精确的解[@problem_id:3565512]。

综上所述，从强形式到弱形式的转换是现代计算力学的基石。它不仅为求解复杂的边值问题提供了可行的途径，其背后的原理和机制也深刻地影响着数值方法的精度、稳定性和[适用范围](@entry_id:636189)。