## 引言
在连续介质力学和计算地球物理的交汇处，变分原理扮演着一个至关重要的角色。它不仅为描述物质变形与运动提供了优雅而深刻的理论框架，更是现代计算方法——如[有限元法](@entry_id:749389)——的基石。然而，从抽象的数学原理到解决实际[地球科学](@entry_id:749876)问题的强大数值工具，这之间存在一条需要系统性学习和理解的路径。本文旨在填补这一鸿沟，为读者提供一个关于[变分原理](@entry_id:198028)及其在地球物理中应用的全面指南。通过本文的学习，你将深入理解如何运用变分思想来构建、分析和求解复杂的力学问题。我们将分为三个核心部分展开：第一章“原理与机制”，将从有限变形的运动学出发，系统阐述应变、应力、[虚功](@entry_id:176403)以及能量泛函等核心概念，揭示[最小势能原理](@entry_id:173340)如何导出平衡方程与边界条件，并探讨处理不可压缩性、动力学及[耗散系统](@entry_id:151564)的关键技术。第二章“应用与跨学科联系”，会将理论与实践相结合，展示[变分原理](@entry_id:198028)在[地震学](@entry_id:203510)、[地球动力学](@entry_id:749832)、[断裂力学](@entry_id:141480)和多物理场耦合等前沿领域的具体应用，特别是其在[全波形反演](@entry_id:749622)中的核心作用。最后，在“动手实践”部分，通过一系列精心设计的计算问题，你将亲手实现变分公式的推导与数值离散，将理论知识转化为解决实际问题的能力。现在，让我们从变分原理的基本构建模块开始，进入其优雅而强大的世界。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，[变分原理](@entry_id:198028)不仅为理论的建立提供了优雅而深刻的框架，也为解决复杂的[计算地球物理学](@entry_id:747618)问题提供了强大的数值工具。本章旨在系统地阐述变分原理的核心思想及其在固体力学问题中的具体应用机制。我们将从有限变形的[运动学](@entry_id:173318)描述出发，逐步引入应力、[虚功](@entry_id:176403)、[能量泛函](@entry_id:170311)等基本概念，进而探讨如何利用[变分原理](@entry_id:198028)推导[平衡方程](@entry_id:172166)、处理材料本构关系与边界条件。特别地，本章将重点关注在计算实践中至关重要的若干主题，包括如何处理[不可压缩性约束](@entry_id:750592)、如何将变分思想推广至动力学与[耗散系统](@entry_id:151564)，以及其在[全波形反演](@entry_id:749622)等前沿地球物理问题中的应用。

### 变形与应变的[拉格朗日描述](@entry_id:264498)

为了精确描述一个[可变形体](@entry_id:201887)（如地壳或地幔的一部分）的运动，我们首先需要建立一个清晰的数学框架。在连续介质力学中，这通常通过区分物体的两种构型来完成：**参考构型 (reference configuration)** 和 **当前构型 (current configuration)**。参考构型，记作 $\mathcal{B}_0$，是物体在某一初始时刻（通常是 $t=0$）所占据的空间区域，我们可以将其视为未变形的“标签”空间。在此构型中的点用物质坐标 $\mathbf{X}$ 表示。随着时间的推移，物体变形并占据新的空间区域，即当前构型 $\mathcal{B}_t$，其中的点用空间坐标 $\mathbf{x}$ 表示。

描述这种运动的核心工具是 **变形映射 (deformation map)** $\boldsymbol{\varphi}$，它将每个物[质点](@entry_id:186768) $\mathbf{X}$ 映射到其在当前构型中的空间位置 $\mathbf{x}$：
$$
\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)
$$
物质点 $\mathbf{X}$ 的 **位移 (displacement)** 矢量 $\mathbf{u}$ 定义为其当前位置与初始位置之差：
$$
\mathbf{u}(\mathbf{X}, t) = \boldsymbol{\varphi}(\mathbf{X}, t) - \mathbf{X}
$$
在拉格朗日（或物质）描述中，所有的物理量都被表达为物质坐标 $\mathbf{X}$ 和时间 $t$ 的函数。

变形的核心度量是 **变形梯度 (deformation gradient)** $\mathbf{F}$，它量化了物质点邻域的局部变形。$\mathbf{F}$ 定义为变形映射 $\boldsymbol{\varphi}$ 对物质坐标 $\mathbf{X}$ 的梯度：
$$
\mathbf{F}(\mathbf{X}, t) = \nabla_{\mathbf{X}} \boldsymbol{\varphi}(\mathbf{X}, t) = \frac{\partial \boldsymbol{\varphi}}{\partial \mathbf{X}}
$$
从位移的定义出发，我们还可以得到 $\mathbf{F}$ 与[位移梯度](@entry_id:165352)之间的重要关系：
$$
\mathbf{F} = \nabla_{\mathbf{X}} (\mathbf{X} + \mathbf{u}) = \mathbf{I} + \nabla_{\mathbf{X}} \mathbf{u}
$$
其中 $\mathbf{I}$ 是二阶单位张量。变形梯度 $\mathbf{F}$ 包含了关于局部拉伸、剪切和旋转的全部信息。

然而，变形梯度本身并不能直接作为应变的度量，因为它包含了[刚体转动](@entry_id:191086)。一个真正的[应变度量](@entry_id:755495)应该在刚体运动下保持不变。为了构建这样一个客观的度量，我们比较物质点邻域内一个微元线段 $d\mathbf{X}$ 在变形前后的长度平方。变形前，其长度平方为 $ds_0^2 = d\mathbf{X} \cdot d\mathbf{X}$。变形后，该线段变为 $d\mathbf{x} = \mathbf{F} d\mathbf{X}$，其长度平方为 $ds^2 = d\mathbf{x} \cdot d\mathbf{x} = (\mathbf{F} d\mathbf{X}) \cdot (\mathbf{F} d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{F}^T \mathbf{F} d\mathbf{X})$。

这引出了 **右柯西-格林变形张量 (Right Cauchy-Green deformation tensor)** $\mathbf{C}$ 的定义：
$$
\mathbf{C} = \mathbf{F}^T \mathbf{F}
$$
$\mathbf{C}$ 描述了变形后度量在参考构型上的“[拉回](@entry_id:160816)”(pull-back)。长度平方的改变完全由 $\mathbf{C}$ 决定：$ds^2 - ds_0^2 = d\mathbf{X} \cdot (\mathbf{C} - \mathbf{I}) d\mathbf{X}$。

基于此，我们定义 **[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)** $\mathbf{E}$，它精确地量化了长度的改变：
$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^T \mathbf{F} - \mathbf{I})
$$
当且仅当变形为[刚体运动](@entry_id:193355)时，$\mathbf{E}$ 为零张量，这使其成为一个理想的[有限应变度量](@entry_id:185716)。这些在参考构型中定义的运动学量，构成了建立基于变分原理的[非线性固体力学](@entry_id:171757)模型的基石 。

### 应力与虚功原理

有了应变的度量，我们还需要一个描述物体内部相互作用力的量，即 **应力 (stress)**。最直观的应力定义是在当前构型中进行的。**柯西[应力张量](@entry_id:148973) (Cauchy stress tensor)** $\boldsymbol{\sigma}$ 是一个[二阶张量](@entry_id:199780)，它通过柯西公式 $ \mathbf{t} = \boldsymbol{\sigma} \mathbf{n} $ 将当前构型中一个面的[单位法向量](@entry_id:178851) $\mathbf{n}$ 映射到作用在该面上的力矢量（面力）$\mathbf{t}$。对于经典（非极性）连续介质，[角动量守恒](@entry_id:156798)定律要求柯西[应力张量](@entry_id:148973)是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$。

**虚功原理 (Principle of Virtual Work)** 或[虚功](@entry_id:176403)率原理，是连接应力、应变和外力的基本法则，也是变分法的核心。它断言，对于任意一个满足[运动学](@entry_id:173318)约束的虚速度场 $\mathbf{w}$，[内力](@entry_id:167605)所做的[虚功](@entry_id:176403)率（即[内虚功](@entry_id:172278)率）等于外力所做的[虚功](@entry_id:176403)率。在当前构型中，内虚[功率密度](@entry_id:194407)是应力张量与[速度梯度张量](@entry_id:270928)的[双点积](@entry_id:748648)。由于 $\boldsymbol{\sigma}$ 的对称性，它只在速度梯度的对称部分上做功。因此，[内虚功](@entry_id:172278)率 $\delta W_{\text{int}}$ 可以写作：
$$
\delta W_{\text{int}} = \int_{\mathcal{B}_t} \boldsymbol{\sigma} : \nabla_{\mathbf{x}}^s \mathbf{w} \, dv
$$
其中 $\nabla_{\mathbf{x}}^s \mathbf{w} = \frac{1}{2}(\nabla_{\mathbf{x}} \mathbf{w} + (\nabla_{\mathbf{x}} \mathbf{w})^T)$ 是虚[速度场](@entry_id:271461)的对称梯度，在实际运动中对应于 **变形率张量 (rate-of-deformation tensor)** $\mathbf{d}$。这表明柯西应力 $\boldsymbol{\sigma}$ 与变形率 $\mathbf{d}$ 是 **[功共轭](@entry_id:194957) (work-conjugate)** 的。

在[拉格朗日描述](@entry_id:264498)中，我们希望将所有积分都在固定的参考构型 $\mathcal{B}_0$ 上进行。通过应用功率[不变性原理](@entry_id:199405)和[坐标变换](@entry_id:172727)（$dv = J dV$，其中 $J = \det \mathbf{F}$ 是变形梯度的[雅可比行列式](@entry_id:137120)），我们可以定义与参考构型相关的应力张量。

将柯西应力从当前[构型转换](@entry_id:180774)回参考构型，我们得到 **[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量 (First Piola-Kirchhoff stress tensor, PK1)** $\mathbf{P}$。它的定义使其与变形梯度的[物质时间导数](@entry_id:190892) $\dot{\mathbf{F}}$（或虚速度的物质梯度 $\nabla_{\mathbf{X}}\mathbf{w}$）[功共轭](@entry_id:194957)。其变换关系和[虚功](@entry_id:176403)率表达式为：
$$
\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-T}
$$
$$
\delta W_{\text{int}} = \int_{\mathcal{B}_0} \mathbf{P} : \nabla_{\mathbf{X}} \mathbf{w} \, dV
$$
由于 $\mathbf{F}$ 通常不是正交的，即使 $\boldsymbol{\sigma}$ 是对称的，$\mathbf{P}$ 也通常是 **非对称** 的。$\mathbf{P}$ 将参考构型中的法向量映射到当前构型中的力。

为了得到一个对称的物质应力张量，我们进一步定义 **[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量 (Second Piola-Kirchhoff stress tensor, PK2)** $\mathbf{S}$，它通过关系 $\mathbf{P} = \mathbf{F} \mathbf{S}$ 与 $\mathbf{P}$ 联系。$\mathbf{S}$ 是对称的，并且与[格林-拉格朗日应变张量](@entry_id:187745)的时间导数 $\dot{\mathbf{E}}$ [功共轭](@entry_id:194957)：
$$
\mathbf{S} = \mathbf{F}^{-1} \mathbf{P} = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T}
$$
$$
\delta W_{\text{int}} = \int_{\mathcal{B}_0} \mathbf{S} : \delta \mathbf{E} \, dV
$$
其中 $\delta \mathbf{E}$ 是[格林-拉格朗日应变张量](@entry_id:187745)的变分。这三个[应力张量](@entry_id:148973)——$\boldsymbol{\sigma}$、$\mathbf{P}$ 和 $\mathbf{S}$——以及它们对应的[功共轭](@entry_id:194957)应变率度量，为在不同构型下建立力学模型提供了完备的工具集 。

### [变分原理](@entry_id:198028)与平衡方程

对于准静态（忽略[惯性力](@entry_id:169104)）的弹性问题，系统的平衡状态对应于其 **总势能 (total potential energy)** 达到极小值的状态。这一 **[最小势能原理](@entry_id:173340)** 是[变分法](@entry_id:163656)的基石。总[势能](@entry_id:748988)泛函 $\Pi[\mathbf{u}]$ 通常由两部分组成：储存在物体内的 **应变能 (strain energy)** $U_{int}$ 和外力所做的功的负值，即 **外力势能** $W_{ext}$。
$$
\Pi[\mathbf{u}] = U_{int}[\mathbf{u}] - W_{ext}[\mathbf{u}]
$$
对于一个[超弹性](@entry_id:159356)体，其[应变能](@entry_id:162699)是[应变能密度函数](@entry_id:755490) $\Psi$ 在整个物体上的积分。外力通常包括[体力](@entry_id:174230) $\mathbf{f}$ (如重力) 和面力 $\bar{\mathbf{t}}$ (如边界上的压力)。因此，势能泛函的具体形式为：
$$
\Pi[\mathbf{u}] = \int_{\Omega} \Psi(\mathbf{E}(\mathbf{u})) \, d\Omega - \int_{\Omega} \mathbf{f} \cdot \mathbf{u} \, d\Omega - \int_{\Gamma_N} \bar{\mathbf{t}} \cdot \mathbf{u} \, d\Gamma
$$
平衡状态的位移场 $\mathbf{u}$ 使得 $\Pi[\mathbf{u}]$ 对任意满足[运动学](@entry_id:173318)约束的[虚位移](@entry_id:168781) $\delta \mathbf{u}$ 的一阶变分 $\delta \Pi$ 为零：
$$
\delta \Pi[\mathbf{u}; \delta \mathbf{u}] = 0
$$
计算这个变分，我们得到[平衡方程](@entry_id:172166)的 **[弱形式](@entry_id:142897) (weak form)**：
$$
\int_{\Omega} \frac{\partial \Psi}{\partial \mathbf{E}} : \delta \mathbf{E} \, d\Omega = \int_{\Omega} \mathbf{f} \cdot \delta \mathbf{u} \, d\Omega + \int_{\Gamma_N} \bar{\mathbf{t}} \cdot \delta \mathbf{u} \, d\Gamma
$$
左端代表[内虚功](@entry_id:172278)，右端代表外[虚功](@entry_id:176403)。这个方程必须对所有 **容许的 (admissible)** [虚位移](@entry_id:168781) $\delta \mathbf{u}$ 成立。

这个推导过程清晰地揭示了两种边界条件的本质区别 。
*   **[本质边界条件](@entry_id:173524) (Essential Boundary Conditions)**，也称为狄利克雷 (Dirichlet) 条件，是对位移场 $\mathbf{u}$ 本身施加的约束，例如在边界 $\Gamma_D$ 上规定 $\mathbf{u} = \bar{\mathbf{u}}$。这些条件必须在求解之前就得到满足。在变分框架中，这通过限制求解所在的 **[试探函数](@entry_id:756165)空间 (trial function space)** 和[虚位移](@entry_id:168781)所在的 **[检验函数](@entry_id:166589)空间 (test function space)** 来实现。例如，试探解 $\mathbf{u}$ 必须属于函数空间 $\{ \mathbf{v} \in [H^1(\Omega)]^3 \mid \mathbf{v} = \bar{\mathbf{u}} \text{ on } \Gamma_D \}$，而[检验函数](@entry_id:166589)（[虚位移](@entry_id:168781)）$\delta \mathbf{u}$ 必须属于 $\{ \mathbf{w} \in [H^1(\Omega)]^3 \mid \mathbf{w} = \mathbf{0} \text{ on } \Gamma_D \}$。

*   **自然边界条件 (Natural Boundary Conditions)**，也称为诺伊曼 (Neumann) 条件，是对力（即应力）施加的约束，例如在边界 $\Gamma_N$ 上规定面力 $\boldsymbol{\sigma}\mathbf{n} = \bar{\mathbf{t}}$。这些条件是[变分原理](@entry_id:198028)的 **结果**，而非前提。它们之所以“自然”，是因为它们是通过对弱形式中的项进行分部积分（[格林公式](@entry_id:173118)）而自动出现的。在势能泛函中包含面力功的项 $-\int_{\Gamma_N} \bar{\mathbf{t}} \cdot \mathbf{u} \, d\Gamma$，其变分恰好平衡了应力在边界上产生的[虚功](@entry_id:176403)项，从而在没有对检验函数 $\delta \mathbf{u}$ 在 $\Gamma_N$ 上施加任何约束的情况下，自然地满足了力边界条件。

### 本构关系与材料性质

变分框架的普适性在于，不同的材料行为可以通过选择不同的 **[应变能密度函数](@entry_id:755490) (strain energy density function)** $\Psi$ 来描述。这种将应力通过能量势函数与应变联系起来的材料模型称为 **超弹性 (hyperelastic)** 材料。

对于小应变线性弹性问题，$\Psi$ 是应变张量 $\mathbf{E}$ 的二次函数。对于各向异性材料，其最一般的形式由四阶 **[刚度张量](@entry_id:176588) (stiffness tensor)** $C_{ijkl}$ 决定：
$$
\Psi(\mathbf{E}) = \frac{1}{2} E_{ij} C_{ijkl} E_{kl}
$$
[刚度张量](@entry_id:176588) $C_{ijkl}$ 编码了材料在不同方向上抵[抗变](@entry_id:192290)形的能力。为了确保物理上的合理性和数学上的[适定性](@entry_id:148590)，$\mathbf{C}$ 必须满足特定的对称性和[正定性](@entry_id:149643)条件 。

*   **对称性 (Symmetries)**:
    *   **次对称性 (Minor symmetries)**: 由于应力张量 ($\sigma_{ij} = \sigma_{ji}$) 和应变张量 ($E_{kl} = E_{lk}$) 的对称性，[刚度张量](@entry_id:176588)必然满足 $C_{ijkl} = C_{jikl}$ 和 $C_{ijkl} = C_{ijlk}$。
    *   **主对称性 (Major symmetry)**: [超弹性](@entry_id:159356)假设（即 $\Psi$ 的存在）要求应力可以从 $\Psi$ 求导得到，即 $\sigma_{ij} = \partial \Psi / \partial E_{ij}$。这一条件蕴含了更强的对称性 $C_{ijkl} = C_{klij}$。

*   **正定性 (Positive-Definiteness)**:
    为了保证材料在变形时储存的能量为正，且[平衡解](@entry_id:174651)是唯一的，[应变能函数](@entry_id:178435) $\Psi$ 必须是严格凸的。这要求[刚度张量](@entry_id:176588) $\mathbf{C}$ 是正定的。更准确地说，为了保证[变分问题](@entry_id:756445)的 **[适定性](@entry_id:148590) (well-posedness)**（解的存在性和唯一性），需要一个更强的条件，即 **一致[正定性](@entry_id:149643) (uniform positive-definiteness)** 或椭圆性：存在一个常数 $\alpha > 0$，使得对于任意非零对称二阶张量 $\mathbf{E}$，都有
    $$
    E_{ij} C_{ijkl} E_{kl} \ge \alpha E_{ij} E_{ij}
    $$
    这个条件保证了[能量泛函](@entry_id:170311)的 **[矫顽性](@entry_id:159399) (coercivity)**。在泛函分析中，对于具有狄利克雷边界条件的问题，**[科恩不等式](@entry_id:174794) (Korn's inequality)** 保证了应变能范数可以控制位移的 $H^1$ 范数。因此，[刚度张量](@entry_id:176588)的一致[正定性](@entry_id:149643)与[科恩不等式](@entry_id:174794)相结合，通过[Lax-Milgram定理](@entry_id:137966)保证了[弹性静力学](@entry_id:198298)问题有唯一解。一个更弱的条件是[Legendre-Hadamard条件](@entry_id:190308)，它对于[材料稳定性](@entry_id:183933)是必要的，但本身不足以保证[解的唯一性](@entry_id:143619)。

### [不可压缩性约束](@entry_id:750592)的处理

在许多地球物理场景中，如[地幔对流](@entry_id:203493)或饱水岩土的变形，材料可以被近似为 **不可压缩的 (incompressible)**。在有限变形理论中，这意味着体积不变，即变形梯度的[雅可比行列式](@entry_id:137120) $J = \det \mathbf{F} = 1$。在[线性弹性](@entry_id:166983)理论中，这对应于体积应变为零，即 $\text{div} \mathbf{u} = 0$。

在标准的位移有限元方法中，直接在离散[函数空间](@entry_id:143478)中强制施加这个[运动学](@entry_id:173318)约束，会导致一个被称为 **[体积锁定](@entry_id:172606) (volumetric locking)** 的数值问题 。当材料接[近不可压缩](@entry_id:752387)时（即体积模量 $\kappa$ 远大于剪切模量 $\mu$），离散系统会变得过度刚硬，导致计算出的位移小得不切实际。这是因为低阶的有限元单元（如线性三角形或四面体）无法精确地表示一个散度为零的向量场，离散的不可压缩条件施加了过多的约束。

为了解决[体积锁定](@entry_id:172606)问题，我们需要采用不直接在位移空间施加约束的 **[混合变分原理](@entry_id:165106) (mixed variational principles)**。

#### [拉格朗日乘子法](@entry_id:176596)

处理约束的最经典方法是引入一个 **拉格朗日乘子 (Lagrange multiplier)** $p$ 来弱化[不可压缩性约束](@entry_id:750592)。这个乘子场通常可以解释为 **[静水压力](@entry_id:275365) (hydrostatic pressure)**。我们构造一个增广的、依赖于位移 $\mathbf{u}$ 和压力 $p$ 的 **[鞍点](@entry_id:142576)泛函 (saddle-point functional)**，例如，对于有限变形问题，可以构造如下的 **增广拉格朗日泛函 (augmented Lagrangian)** ：
$$
\mathcal{L}(\mathbf{u}, p) = \int_{\Omega} \left[ \Psi_{\text{iso}}(\mathbf{F}) - p(J-1) \right] d\mathbf{X} - W_{ext}(\mathbf{u})
$$
其中 $\Psi_{\text{iso}}$ 是材料的等容（仅与形状改变相关）应变能部分。对 $\mathcal{L}$ 关于 $\mathbf{u}$ 和 $p$ 分别求变分并令其为零，我们得到一个混合弱形式 ：
1.  [动量平衡](@entry_id:193575)方程（关于 $\delta \mathbf{u}$ 的变分）：
    $$
    \int_{\Omega} \left( \frac{\partial \Psi_{\text{iso}}}{\partial \mathbf{F}} - p J \mathbf{F}^{-T} \right) : \nabla \delta \mathbf{u} \, dV = \delta W_{ext}
    $$
    这给出了包含压力项的[第一皮奥拉-基尔霍夫应力](@entry_id:163971) $\mathbf{P} = \partial \Psi_{\text{iso}}/\partial \mathbf{F} - p J \mathbf{F}^{-T}$。
2.  弱形式的不可压缩约束（关于 $\delta p$ 的变分）：
    $$
    \int_{\Omega} \delta p (J-1) \, dV = 0
    $$
离散化后，这种[混合格式](@entry_id:167436)会产生一个块状的[鞍点线性系统](@entry_id:754478) ：
$$
\begin{pmatrix} \mathbf{K} & \mathbf{G}^{T} \\ \mathbf{G} & -\frac{1}{\kappa}\mathbf{M} \end{pmatrix} \begin{pmatrix} \mathbf{U} \\ \mathbf{P} \end{pmatrix} = \begin{pmatrix} \mathbf{F} \\ \mathbf{0} \end{pmatrix}
$$
其中 $\mathbf{K}$ 是[刚度矩阵](@entry_id:178659)，$\mathbf{G}$ 是离散的[梯度算子](@entry_id:275922)，$\mathbf{M}$ 是质量矩阵。为了保证该系统的稳定性和唯一可解性，位移和压力的有限元空间必须满足 **Ladyzhenskaya-Babuška-Brezzi (LBB)** 或 **inf-sup** 稳定条件。

#### [罚函数法](@entry_id:636090)

另一种方法是 **[罚函数法](@entry_id:636090) (penalty method)**，它通过在能量泛函中增加一个惩罚项来近似地施加约束 。修改后的势能泛函为：
$$
\Pi_{\kappa}(\mathbf{u}) = \int_{\Omega} \left( \Psi_{\text{iso}}(\mathbf{F}) + \frac{\kappa}{2}(J-1)^2 \right) d\mathbf{X} - W_{ext}(\mathbf{u})
$$
其中 $\kappa$ 是一个大的正数，称为罚参数。当 $\kappa \to \infty$ 时，任何导致 $J \neq 1$ 的变形都会受到巨大的能量惩罚，从而迫使解趋向于不可压缩。

[罚函数法](@entry_id:636090)的好处是它避免了[LBB条件](@entry_id:746626)和[鞍点问题](@entry_id:174221)，回到了一个只关于位移的、正定的系统。然而，它的代价是当 $\kappa$ 非常大时，离散系统的[刚度矩阵](@entry_id:178659)会变得 **病态 (ill-conditioned)**，条件数随 $\kappa$ 增长，这同样会带来数值计算上的困难。在[罚函数法](@entry_id:636090)中，压力可以被后验地重构出来，其表达式为 $p_{\kappa} = -\kappa(J-1)$。可以证明，当 $\kappa \to \infty$ 时，[罚函数法](@entry_id:636090)的解会收敛到不可压缩问题的解，并且重构的压力 $p_{\kappa}$ 会弱收敛到真实的[拉格朗日乘子](@entry_id:142696) $p$。

### 动力学与[耗散系统](@entry_id:151564)

变分原理的应用不限于静态问题。**[哈密顿原理](@entry_id:175601) (Hamilton's principle)** 将变分思想推广到了动力学领域。该原理指出，一个保守系统在两个时间点之间的真实运动路径，是使其 **[作用量泛函](@entry_id:169216) (action functional)** $S[\mathbf{u}]$ 取驻值的路径。作用量定义为拉格朗日量 $L$ (动能减去势能) 的时间积分：
$$
S[\mathbf{u}] = \int_{t_0}^{t_1} L(\mathbf{u}, \dot{\mathbf{u}}) \, dt = \int_{t_0}^{t_1} (T - \Pi) \, dt = \int_{t_0}^{t_1} \int_{\Omega} \left( \frac{1}{2}\rho_0 |\dot{\mathbf{u}}|^2 - \Psi(\mathbf{F}) \right) \, d\mathbf{X} dt
$$
对作用量 $S[\mathbf{u}]$ 求变分并令 $\delta S = 0$，经过分部积分后，我们可以同时得到系统的运动方程（强形式）和自然边界条件。例如，对于[弹性动力学](@entry_id:175818)，变分会导出[拉格朗日形式](@entry_id:145697)的动量守恒方程 ：
$$
\rho_0 \ddot{\mathbf{u}} - \text{Div}_{\mathbf{X}} \mathbf{P} = \mathbf{0}
$$
其中 $\rho_0$ 是参考构型中的密度，$\ddot{\mathbf{u}}$ 是[物质加速度](@entry_id:270992)，$\mathbf{P}$ 是第一PK应力。

对于包含 **耗散 (dissipation)** 的系统，如[粘弹性材料](@entry_id:194223)，标准的[哈密顿原理](@entry_id:175601)不再适用。然而，变分思想仍然可以通过扩展的[虚功原理](@entry_id:138749)来应用。对于一个 **开尔文-沃伊特 (Kelvin-Voigt)** [粘弹性模型](@entry_id:175352)，其应力可以分解为弹性部分和粘性部分，分别由[应变能密度](@entry_id:200085) $\Psi(\mathbf{\varepsilon})$ 和 **耗散势 (dissipation potential)** $\mathcal{D}(\dot{\mathbf{\varepsilon}})$ 导出：
$$
\boldsymbol{\sigma} = \frac{\partial \Psi}{\partial \boldsymbol{\varepsilon}} + \frac{\partial \mathcal{D}}{\partial \dot{\boldsymbol{\varepsilon}}}
$$
此时，内虚功原理变为 $\delta W_{int} = \delta W_{el} + \delta W_{visc}$。这一框架对于设计保持[能量耗散](@entry_id:147406)平衡的数值积分算法至关重要。通过构造一个离散的增量变分原理，可以设计出所谓的 **[变分积分子](@entry_id:174311) (variational integrators)**，这些算法在离散层面上精确地满足一个能量耗散恒等式，从而具有优异的[长期稳定性](@entry_id:146123)和物理保真度 。

### 高等应用：[全波形反演](@entry_id:749622)中的伴随方法

变分原理在现代[计算地球物理学](@entry_id:747618)中的一个尖端应用是为 **[全波形反演](@entry_id:749622) (Full Waveform Inversion, FWI)** 提供高效的梯度计算方法。FWI 是一个大规模的[非线性](@entry_id:637147)反演问题，旨在通过匹配观测到的[地震波](@entry_id:164985)形和数值模拟的波形来重构地下介质参数（如[波速](@entry_id:186208)）。其目标是最小化一个由观测数据与模拟数据之差定义的 **[失配泛函](@entry_id:752011) (misfit functional)** $J$。

计算这个庞大[参数空间](@entry_id:178581)上的梯度是FWI的核心挑战。**伴随状态法 (adjoint-state method)**，它本质上是约束优化问题的[拉格朗日乘子法](@entry_id:176596)在泛函空间的应用，为此提供了极其高效的解决方案。

考虑一个由[波动方程](@entry_id:139839)描述的系统，我们构造如下的拉格朗日泛函 ：
$$
\mathcal{L}(p, \lambda) = J(p) + \int_0^T \int_{\Omega} \lambda \left( \mathcal{A}p - s \right) \, d\mathbf{x} dt
$$
其中 $p$ 是状态变量（如压[力场](@entry_id:147325)），$\mathcal{A}$ 是波动方程算子， $s$ 是震源项，而 $\lambda$ 是引入的[拉格朗日乘子](@entry_id:142696)，称为 **伴随场 (adjoint field)**。

通过对 $\mathcal{L}$ 求关于[状态变量](@entry_id:138790) $p$ 的变分并令其为零，经过分部积分，我们可以推导出伴随场 $\lambda$ 所满足的 **伴随方程 (adjoint equation)**。伴随方程的形式与原波动方程类似，但其“震[源项](@entry_id:269111)”由[失配泛函](@entry_id:752011)的变分决定。值得注意的是，不同的数据测量方式（即不同的[失配泛函](@entry_id:752011) $J$）会导致不同形式的伴随源：

*   **内部测量**: 如果[失配泛函](@entry_id:752011)是基于区域内部的观测数据（例如，井中检波器），如 $J_I = \frac{1}{2} \int \int_{\Omega_m} (p-d)^2 \,d\mathbf{x}dt$，那么伴随源将是一个作用在相应区域的 **体积源 (volumetric source)**。

*   **表面测量**: 如果[失配泛函](@entry_id:752011)基于边界上的观测数据，情况则更为微妙。
    *   若测量的是边界上的压力（狄利克雷型数据），如 $J_D = \frac{1}{2} \int \int_{\Gamma_m} (p-d)^2 \,ds dt$，则伴随源通常表现为伴随场的 **诺伊曼型边界条件**。
    *   若测量的是边界上压力的[法向导数](@entry_id:169511)（诺伊曼型数据），如 $J_N = \frac{1}{2} \int \int_{\Gamma_m} (\partial_n p - d)^2 \,ds dt$，则伴随源通常表现为伴随场的 **狄利克雷型边界条件**。

一旦求解了伴随场，[失配泛函](@entry_id:752011)对模型参数的梯度就可以通过一个简单的积分（通常是正向波场和伴随波场的[互相关](@entry_id:143353)）高效地计算出来，其计算成本与一次正演模拟相当。这种源于变分演算的深刻对偶性，使得处理具有数百万甚至数十亿参数的[地球物理反演](@entry_id:749866)问题成为可能。