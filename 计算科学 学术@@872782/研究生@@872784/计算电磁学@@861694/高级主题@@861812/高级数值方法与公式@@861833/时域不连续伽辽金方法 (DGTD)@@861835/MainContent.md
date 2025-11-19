## 引言
在计算电磁学领域，间断伽辽金时域 (Discontinuous Galerkin Time-Domain, DGTD) 方法已成为一种强大而前沿的数值工具，以其[高阶精度](@entry_id:750325)、几何灵活性和卓越的并行计算可扩展性而备受瞩目。传统数值方法在处理复杂几何、非共形网格以及在现代[并行计算](@entry_id:139241)架构上实现高效扩展时常面临挑战。DGTD 方法的出现，正是为了填补这一空白，为解决下一代复杂[电磁仿真](@entry_id:748890)问题提供了一个稳健而灵活的框架。

本文旨在引领读者全面深入地探索 DGTD 方法。在“原理与机制”部分中，我们将奠定其理论基石，剖析从[麦克斯韦方程组](@entry_id:150940)出发的数学构建、数值通量的关键作用以及保证稳定性的核心策略。随后的“应用与跨学科交叉”部分将搭建理论与实践的桥梁，展示 DGTD 如何应对从复杂材料与边界建模到与[高性能计算](@entry_id:169980)结合等真实世界的挑战。最后，“动手实践”部分将通过具体的编程练习，巩固理论知识并培养实际的编程实现能力。通过学习这三个环环相扣的部分，读者将能从核心数学原理到前沿研究和工程应用，全面掌握 DGTD 方法的精髓。

## 原理与机制

本章旨在系统性阐述间断伽辽金时域 (Discontinuous Galerkin Time-Domain, DGTD) 方法的核心原理与关键机制。我们将从其数学构造的基础出发，逐步深入到保证数值稳定性的核心技术、[高阶方法](@entry_id:165413)的实现细节，以及在复杂电磁系统中必须处理的特定挑战。

### [麦克斯韦方程组](@entry_id:150940)的间断伽辽金离散

DGTD 方法的核心思想是在求解区域 $\Omega$ 的每个离散单元（或元素）$K$ 内部，使用一组局部多项式[基函数](@entry_id:170178)来逼近[电磁场](@entry_id:265881)，并允许场在单元边界上存在间断。这种设计带来了极大的灵活性，特别是在处理复杂几何和并行计算方面。

我们从[源项](@entry_id:269111)为零的麦克斯韦旋度方程出发：
$$
\epsilon \frac{\partial \mathbf{E}}{\partial t} = \nabla \times \mathbf{H}, \qquad \mu \frac{\partial \mathbf{H}}{\partial t} = - \nabla \times \mathbf{E}
$$
其中 $\mathbf{E}$ 和 $\mathbf{H}$ 分别是[电场和磁场](@entry_id:261347)强度，$\epsilon$ 和 $\mu$ 是[介电常数](@entry_id:146714)和[磁导率](@entry_id:154559)。为了构建伽辽金弱形式，我们在任意一个单元 $K$ 上，将上述方程与一个矢量测试函数 $\mathbf{v}$ 做[内积](@entry_id:158127)并积分。以[法拉第感应定律](@entry_id:146175)为例：
$$
\int_K \mu \frac{\partial \mathbf{H}}{\partial t} \cdot \mathbf{v} \, dV = - \int_K (\nabla \times \mathbf{E}) \cdot \mathbf{v} \, dV
$$
为了处理单元间的耦合以及允许场的不连续性，我们对右侧的旋度项使用[分部积分](@entry_id:136350)（矢量恒等式）：
$$
\int_K (\nabla \times \mathbf{E}) \cdot \mathbf{v} \, dV = \int_K \mathbf{E} \cdot (\nabla \times \mathbf{v}) \, dV + \oint_{\partial K} (\mathbf{n} \times \mathbf{E}) \cdot \mathbf{v} \, dS
$$
其中 $\partial K$ 是单元 $K$ 的边界，$\mathbf{n}$ 是指向外部的[单位法向量](@entry_id:178851)。将此式代入原弱形式，我们得到：
$$
\int_K \mu \frac{\partial \mathbf{H}}{\partial t} \cdot \mathbf{v} \, dV = - \int_K \mathbf{E} \cdot (\nabla \times \mathbf{v}) \, dV - \oint_{\partial K} (\mathbf{n} \times \mathbf{E}) \cdot \mathbf{v} \, dS
$$
表[面积分](@entry_id:275394)项中的 $\mathbf{n} \times \mathbf{E}$ 是[电场](@entry_id:194326)的切向分量。由于场的逼近在单元边界上是间断的，该项没有唯一定义。DGTD 方法的关键创新在于用一个**[数值通量](@entry_id:752791) (numerical flux)**，记作 $\widehat{\mathbf{n} \times \mathbf{E}}$，来代替它。数值通量是一个依赖于界面两侧场值的函数，它负责在单元间传递信息并保证方案的稳定性。

从弱形式的结构可以看出，为了使所有积分有意义，场的逼近函数和测试函数 $\mathbf{u}$ 必须满足其自身及其旋度 $\nabla \times \mathbf{u}$ 都是平方可积的，即 $\mathbf{u} \in \mathbf{L}^2(K)$ 且 $\nabla \times \mathbf{u} \in \mathbf{L}^2(K)$。满足此条件的[函数空间](@entry_id:143478)称为 $\mathbf{H}(\mathrm{curl}; K)$。因此，从严格的数学角度看，DGTD 方法的函数空间是在整个网格剖分 $\mathcal{T}_h$ 上的**破碎 Sobolev 空间 (broken Sobolev space)** $\mathbf{H}(\mathrm{curl}; \mathcal{T}_h)$ [@problem_id:3300640]。然而，在大多数实际应用中，为了简化[基函数](@entry_id:170178)的构造和提高计算效率，通常选择一个更简单的空间，即每个笛卡尔分量都由 $p$ 次多项式构成的向量值[多项式空间](@entry_id:144410) $[\mathbb{P}_p(K)]^3$ [@problem_id:3300603]。这种选择的合理性依赖于[数值通量](@entry_id:752791)的正确设计，我们将在下一节讨论。

### 单元间耦合与数值通量

数值通量是 DGTD 方法的灵魂。它不仅实现了单元间的耦合，还通过引入耗散来抑制因场间断而可能产生的非物理[振荡](@entry_id:267781)，从而确保数值稳定性。为了定义通量，我们首先引入在单元界面 $F$ 上的**平均 (average)** 和**跳变 (jump)** 算子。对于一个界面两侧的场 $\mathbf{v}^-$ 和 $\mathbf{v}^+$，我们定义：
$$
\{\!\{\mathbf{v}\}\!\} = \frac{\mathbf{v}^- + \mathbf{v}^+}{2}, \qquad [\![\mathbf{v}]\!] = \mathbf{v}^- - \mathbf{v}^+
$$

不同的[数值通量](@entry_id:752791)选择会赋予 DGTD 格式不同的性质。通过分析单一界面对总[电磁能](@entry_id:264720)量变化率的贡献，我们可以理解各种通量的稳定性特征 [@problem_id:3300582]。离散能量的时间变化率中，来自界面的贡献可以表达为：
$$
\left(\frac{d\mathcal{E}}{dt}\right)_f = \int_f \left( (\mathbf{n} \times [\![\mathbf{E}_t]\!]) \cdot (\widehat{\mathbf{H}_t} - \{\!\{\mathbf{H}_t\}\!\}) - (\mathbf{n} \times [\![\mathbf{H}_t]\!]) \cdot (\widehat{\mathbf{E}_t} - \{\!\{\mathbf{E}_t\}\!\}) \right) dS
$$
其中 $\mathbf{E}_t$ 和 $\mathbf{H}_t$ 代表切向场。一个稳定的格式要求此项小于等于零。

*   **[中心通量](@entry_id:747204) (Central Flux)**：
    $$
    \widehat{\mathbf{n} \times \mathbf{E}} = \mathbf{n} \times \{\!\{\mathbf{E}\}\!\}, \qquad \widehat{\mathbf{n} \times \mathbf{H}} = \mathbf{n} \times \{\!\{\mathbf{H}\}\}
    $$
    [中心通量](@entry_id:747204)简单地取界面两侧场的平均值。代入能量变化率表达式后，我们发现其贡献恒为零。这意味着[中心通量](@entry_id:747204)在半离散层面上是[能量守恒](@entry_id:140514)的。然而，它没有提供任何耗散机制来抑制[数值振荡](@entry_id:163720)，因此对于标准 DGTD 格式通常是不稳定的。

*   **[迎风通量](@entry_id:143931) (Upwind Flux)**：
    $$
    \widehat{\mathbf{n} \times \mathbf{E}} = \mathbf{n} \times \{\!\{\mathbf{E}\}\} + \frac{1}{2} Z \, \mathbf{n} \times ([\![\mathbf{H}]\!] \times \mathbf{n})
    $$
    $$
    \widehat{\mathbf{n} \times \mathbf{H}} = \mathbf{n} \times \{\!\{\mathbf{H}\}\} - \frac{1}{2} Y \, \mathbf{n} \times ([\![\mathbf{E}]\!] \times \mathbf{n})
    $$
    其中 $Z = \sqrt{\mu/\epsilon}$ 是[波阻抗](@entry_id:276571)，$Y = 1/Z$ 是[波导](@entry_id:198471)纳。[迎风通量](@entry_id:143931)在[中心通量](@entry_id:747204)的基础上增加了一个与场跳变成比例的惩罚项。这个惩罚项的设计源于[麦克斯韦方程组](@entry_id:150940)的特征波分解，它模拟了[波的传播](@entry_id:144063)方向。将[迎风通量](@entry_id:143931)代入能量变化率表达式，可以证明其贡献是负半定的 [@problem_id:3300582] [@problem_id:3300640]：
    $$
    \left(\frac{d\mathcal{E}}{dt}\right)_f = - \int_f \left( \frac{Y}{2} |[\![\mathbf{E}_t]\!]|^2 + \frac{Z}{2} |[\![\mathbf{H}_t]\!]|^2 \right) dS \le 0
    $$
    这种[耗散性](@entry_id:162959)确保了数值格式的[能量稳定性](@entry_id:748991)，是 DGTD 方法中应用最广泛的通量之一。

*   **Lax–Friedrichs (LF) 通量**：
    LF 通量是另一种耗散型通量，它引入一个可调参数 $\alpha$。对于[麦克斯韦方程组](@entry_id:150940)，其形式为：
    $$
    \widehat{\mathbf{n} \times \mathbf{E}} = \mathbf{n} \times \{\!\{\mathbf{E}\}\} + \frac{\alpha \mu}{2} \mathbf{n} \times [\![\mathbf{H}_t]\!]
    $$
    $$
    \widehat{\mathbf{n} \times \mathbf{H}} = \mathbf{n} \times \{\!\{\mathbf{H}\}\} - \frac{\alpha \epsilon}{2} \mathbf{n} \times [\![\mathbf{E}_t]\!]
    $$
    能量分析表明，只要参数 $\alpha \ge 0$，LF 通量就是耗散的，能够保证能量不增。当 $\alpha$ 被选为特征波速时，它与[迎风通量](@entry_id:143931)有密切联系。

### [基函数](@entry_id:170178)与算子结构

在每个单元内，我们可以选择不同类型的多项式[基函数](@entry_id:170178)来展开[电磁场](@entry_id:265881)。这个选择直接影响到离散系统代数方程的性质，尤其是**[质量矩阵](@entry_id:177093) (mass matrix)** 的结构，进而决定了[显式时间步进](@entry_id:168157)算法的效率。最终的[半离散系统](@entry_id:754680)可以写成矩阵形式 $\mathbf{M} \frac{d\mathbf{U}}{dt} = \mathbf{R}(\mathbf{U})$，其中 $\mathbf{U}$ 是所有自由度的向量，$\mathbf{M}$ 是质量矩阵。

*   **[模态基](@entry_id:752055)函数 (Modal Basis)**：这类[基函数](@entry_id:170178)通常是在一个参考单元上构造的一组正交多项式（如 Legendre 多项式）。如果单元是[仿射映射](@entry_id:746332)（即由[线性变换](@entry_id:149133)加平移得到），并且材料参数是常数，那么使用正交[模态基](@entry_id:752055)可以使得质量矩阵 $\mathbf{M}$ 成为一个对角阵 [@problem_id:3300603]。[对角质量矩阵](@entry_id:173002)的[逆矩阵计算](@entry_id:189198)非常简单（只需对角元素取倒数），这对于[显式时间积分](@entry_id:165797)方法至关重要。然而，当单元是弯曲的或材料参数在单元内变化时，质量矩阵将失去对角性。

*   **[节点基](@entry_id:752522)函数 (Nodal Basis)**：这类[基函数](@entry_id:170178)是与单元内一组特定节点（如 [Gauss-Lobatto-Legendre](@entry_id:749736), GLL 节点）相关联的 Lagrange [插值多项式](@entry_id:750764)。其关键特性是，在节点 $i$ 上的[基函数](@entry_id:170178) $\ell_j$ 满足 $\ell_j(\mathbf{x}_i) = \delta_{ij}$。如果我们在计算[质量矩阵](@entry_id:177093)的积分时，采用与[基函数](@entry_id:170178)节点重合的求积点进行[数值积分](@entry_id:136578)（即所谓的**配置 (collocation)**），那么由于 Lagrange [基函数](@entry_id:170178)的插值特性，得到的离散[质量矩阵](@entry_id:177093)将自然地成为对角阵。这个过程被称为**[质量集中](@entry_id:175432) (mass lumping)**。[节点基](@entry_id:752522)的一个巨大优势是，即使在弯曲单元和可变材料参数下，[质量集中](@entry_id:175432)仍然可以得到[对角质量矩阵](@entry_id:173002) [@problem_id:3300645]。这使得[节点基](@entry_id:752522) DGTD 方法在处理复杂问题时非常高效。

### [高阶方法](@entry_id:165413)的稳定性挑战与对策

虽然 DGTD 方法在[高阶精度](@entry_id:750325)方面表现出色，但也引入了一些独特的稳定性挑战，尤其是在处理弯曲网格和[非均匀介质](@entry_id:750241)时。

#### [混叠不稳定性](@entry_id:746361)

[麦克斯韦方程组](@entry_id:150940)本身是线性的。然而，当[介电常数](@entry_id:146714) $\epsilon(\mathbf{x})$ 和[磁导率](@entry_id:154559) $\mu(\mathbf{x})$ 空间可变，或者当网格包含弯曲单元（其[几何映射](@entry_id:749852)的 Jacobian 因子 $J(\boldsymbol{\xi})$ 可变）时，DGTD [弱形式](@entry_id:142897)中的体积积分会出现诸如 $\int_K \epsilon(\mathbf{x}) \mathbf{E}_h \cdot \mathbf{v}_h dV$ 这样的项。即使 $\mathbf{E}_h$ 和 $\mathbf{v}_h$ 是 $p$ 次多项式，乘积项的次数可能会更高。如果用于计算该积分的数值求积法则的精度不足以精确计算这个乘积，就会发生**[混叠](@entry_id:146322) (aliasing)** 错误。这种错误会破坏离散算子（如[旋度算子](@entry_id:184984)）本应具有的反对称性，从而在数值上产生虚假的能量源，导致计算结果发散 [@problem_id:3300583]。

要精确积分这些项，[求积法则](@entry_id:753909)需要对高达 $2p+m+r-1$ 次的多项式精确，其中 $p$ 是场的多项式次数，$m$ 是[几何映射](@entry_id:749852)次数，$r$ 是材料参数的多项式次数。采用如此高精度的[求积法则](@entry_id:753909)（即**[过积分](@entry_id:753033) over-integration**）计算成本非常高。

#### 求和分部积分与分裂格式

一种更高效且优雅的解决方案是构造一种即使在积分不精确的情况下也能保持能量稳定的格式。这可以通过**分裂格式 (split-form discretization)** 实现，它依赖于具有**求和[分部积分](@entry_id:136350) (Summation-By-Parts, SBP)** 性质的离散算子。

SBP 算子是一对离散微分算子 $D$ 和对角范数矩阵 $P$，它们在离散层面上模拟了分部积分的性质。对于节点 DGTD 方法，若采用 GLL 节点和相应的[求积权重](@entry_id:753910)，所构造的[微分矩阵](@entry_id:149870)和[质量矩阵](@entry_id:177093)恰好构成一个 SBP 对。通过将麦克斯韦方程中的旋度项重写为一个代数上反对称的“分裂形式”，并结合 SBP 算子，可以确保离散的体积项在能量分析中精确为零，从而从代数上消除了[混叠不稳定性](@entry_id:746361)，而无需昂贵的过积分 [@problem_id:3300583] [@problem_id:3300645] [@problem_id:3300639]。这种方法对于开发稳健的高阶 DGTD 代码至关重要。

### 散度约束的强制执行

[麦克斯韦方程组](@entry_id:150940)不仅包含两个旋度演化方程，还包含两个散度约束：
$$
\nabla \cdot \mathbf{D} = \rho, \qquad \nabla \cdot \mathbf{B} = 0
$$
在连续理论中，如果初始场满足这些约束，并且[电荷守恒](@entry_id:264158)定律 $\partial_t \rho + \nabla \cdot \mathbf{J} = 0$ 成立，那么旋度方程会自动保证散度约束在所有时间都得到满足 [@problem_id:3300569]。然而，在离散的 DGTD 格式中，由于截断误差和跨单元边界的场间断，这种自动保持的性质会丧失。[数值误差](@entry_id:635587)可能导致离散散度非零，产生虚假[电荷](@entry_id:275494)或磁单极子，污染物理结果。因此，需要特殊技术来控制或消除这些散度误差，即所谓的**[散度清理](@entry_id:748607) (divergence cleaning)**。

*   **[投影法](@entry_id:144836) (Projection Method)**：这种方法在每个时间步结束后进行一次修正。它通过求解一个全局的泊松方程来计算一个标量校正势 $\phi$，然后从场中减去该[势的梯度](@entry_id:268447)（例如，$\mathbf{B}_{\text{new}} = \mathbf{B}_{\text{old}} - \nabla \phi$）来消除其散度分量。这种方法的优点是它能精确地（在求解器容差内）强制散度为零，并且不改变场的旋度分量。其主要缺点是计算成本高昂，因为它需要求解一个大型的、全局耦合的椭圆型方程，这在[并行计算](@entry_id:139241)中难以高效扩展 [@problem_id:3300569] [@problem_id:3300586]。

*   **[双曲清理](@entry_id:750468) (Hyperbolic Cleaning / GLM)**：广义[拉格朗日乘子](@entry_id:142696) (Generalized Lagrange Multiplier, GLM) 方法是另一种主流技术。它通过引入辅助标量场（例如 $\psi$）并修改[麦克斯韦方程组](@entry_id:150940)来工作。例如，[法拉第定律](@entry_id:149836)被修改为 $\partial_t \mathbf{B} + \nabla \times \mathbf{E} + \nabla \psi = 0$，同时为 $\psi$ 增加一个演化方程，如 $\partial_t \psi + c_h^2 \nabla \cdot \mathbf{B} = -\kappa \psi$。这个扩增的系统仍然是双曲型的，它将散度误差转化为以速度 $c_h$ 传播并以速率 $\kappa$ 衰减的波。GLM 的巨大优势在于，整个扩增系统可以用与原 DGTD 格式完全相同的、局部的、显式的方法来求解，因此计算成本增加不多且易于[并行化](@entry_id:753104)。其缺点是它会略微扰动物理场的演化，并且需要仔细选择参数 $c_h$ 和 $\kappa$ [@problem_id:3300586] [@problem_id:3300593]。

*   **保[电荷](@entry_id:275494)通量 (Charge-Conserving Flux)**：对于 $\nabla \cdot \mathbf{D} = \rho$ 约束，还可以通过精心设计[数值通量](@entry_id:752791)来构造一个离散上严格满足[电荷守恒](@entry_id:264158)定律的格式。这需要统一处理麦克斯韦-安培定律和[电荷连续性](@entry_id:747292)方程的离散化，确保[位移电流](@entry_id:190231)的法向通量和[传导电流](@entry_id:265343)的法向通量在离散层面上协调一致 [@problem_id:3300569]。

### [各向异性介质](@entry_id:187796)的扩展

DGTD 方法可以自然地推广到更复杂的介质，如[各向异性材料](@entry_id:184874)。在这种情况下，[介电常数](@entry_id:146714) $\boldsymbol{\varepsilon}$ 和磁导率 $\boldsymbol{\mu}$ 是张量。[麦克斯韦方程组](@entry_id:150940)可以被重写为一个一阶[双曲系统](@entry_id:260647)：
$$
\frac{\partial \mathbf{U}}{\partial t} + \sum_{i=1}^3 A_i \frac{\partial \mathbf{U}}{\partial x_i} = 0
$$
其中 $\mathbf{U} = (\mathbf{E}^T, \mathbf{H}^T)^T$ 是六维场向量，系数矩阵 $A_i$ 依赖于 $\boldsymbol{\varepsilon}^{-1}$ 和 $\boldsymbol{\mu}^{-1}$ [@problem_id:3300627]。

为了证明该系统的[适定性](@entry_id:148590)和 DGTD 格式的稳定性，关键在于证明该系统是**对称双曲 (symmetric-hyperbolic)** 的。这意味着存在一个[对称正定](@entry_id:145886)的**对称化子 (symmetrizer)** 矩阵 $S$，使得所有矩阵乘积 $S A_i$ 都是对称的。对于麦克斯韦方程组，只要 $\boldsymbol{\varepsilon}$ 和 $\boldsymbol{\mu}$ 是[对称正定](@entry_id:145886)张量，我们就可以找到一个块对角的对称化子 $S = \text{diag}(\boldsymbol{\varepsilon}, \boldsymbol{\mu})$。这个对称双曲结构保证了系统的特征[波速](@entry_id:186208)是实数，并且存在一个守恒的[能量范数](@entry_id:274966)，从而为 DGTD 方法的稳定性分析提供了坚实的理论基础。在[各向异性介质](@entry_id:187796)中，[波的传播](@entry_id:144063)速度将依赖于方向，这与各向同性介质中的单一光速形成对比。