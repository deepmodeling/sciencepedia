## 引言
间断伽辽金（Discontinuous Galerkin, DG）方法是计算流体动力学（CFD）领域中一类功能强大的[高阶数值方法](@entry_id:142601)，尤其在求解以[可压缩欧拉方程](@entry_id:747588)为代表的[双曲守恒律](@entry_id:147752)方面展现出巨大潜力。然而，准确且高效地模拟包含激波、[接触间断](@entry_id:194702)等[复杂流动](@entry_id:747569)现象的高速流，对传统数值方法构成了严峻挑战。低阶方法难以兼顾精度与计算效率，而连续的[高阶方法](@entry_id:165413)在处理间断解时又显得力不从心。DG方法通过在单元内部采用高阶[多项式逼近](@entry_id:137391)，同时允许单元边界处存在间断，为解决这一核心难题提供了优雅而稳健的框架。

本文旨在系统地介绍[可压缩欧拉方程](@entry_id:747588)的[DG格式](@entry_id:178043)。为了引导读者从理论基础逐步走向前沿应用，文章组织为三个递进的部分。在“原理与机制”一章中，我们将深入剖析[DG方法](@entry_id:748369)的数学构造，包括其[弱形式](@entry_id:142897)、数值通量设计以及保证稳定性的关键技术。接着，在“应用与跨学科连接”一章中，我们将展示如何将这些原理应用于处理激波、复杂边界以及如何通过算法优化和高性能计算来应对大规模模拟的挑战，并探讨其在地球物理学、交通工程学等领域的延伸。最后，“动手实践”部分将提供具体的编程练习，帮助读者巩固所学知识。通过这一结构化的学习路径，您将全面掌握DG方法的核心思想及其在现代科学与工程计算中的强大应用。

## 原理与机制

本章将深入探讨不连续伽辽金 (Discontinuous Galerkin, DG) 方法应用于[可压缩欧拉方程](@entry_id:747588)的核心数学原理和数值机制。我们将从控制方程的标准化入手，系统地构建DG方法的弱形式，并讨论其在参考[坐标系](@entry_id:156346)下的实现、[基函数](@entry_id:170178)的选择、以及保证数值解稳定性和精度的关键技术。

### [可压缩欧拉方程](@entry_id:747588)

理想气体的[可压缩欧拉方程](@entry_id:747588)是描述无粘、绝热流体运动的一组[非线性](@entry_id:637147)[双曲型偏微分方程](@entry_id:144631)。在二维笛卡尔坐标系 $(x, y)$ 中，其[守恒形式](@entry_id:747710)为：
$$
\partial_{t} \boldsymbol{U} + \partial_{x} \boldsymbol{F}(\boldsymbol{U}) + \partial_{y} \boldsymbol{G}(\boldsymbol{U}) = \boldsymbol{0}
$$
其中 $\boldsymbol{U}$ 是[守恒变量](@entry_id:747720)向量，$\boldsymbol{F}$ 和 $\boldsymbol{G}$ 分别是 $x$ 和 $y$ 方向的物理通量向量。对于比热比为 $\gamma$ 的量热完全理想气体，这些向量定义为：
$$
\boldsymbol{U} = \begin{pmatrix} \rho \\ \rho u_x \\ \rho u_y \\ \rho E \end{pmatrix}, \quad
\boldsymbol{F} = \begin{pmatrix} \rho u_x \\ \rho u_x^2 + p \\ \rho u_x u_y \\ u_x(\rho E + p) \end{pmatrix}, \quad
\boldsymbol{G} = \begin{pmatrix} \rho u_y \\ \rho u_x u_y \\ \rho u_y^2 + p \\ u_y(\rho E + p) \end{pmatrix}
$$
这里，$\rho$ 是密度，$\boldsymbol{u} = (u_x, u_y)$ 是[速度矢量](@entry_id:269648)，$p$ 是压力，$E$ 是单位质量的总能量。总能量由内能 $e$ 和动能组成，$E = e + \frac{1}{2}|\boldsymbol{u}|^2$。[理想气体状态方程](@entry_id:137803) $p = \rho R T$ 和内能关系 $e = c_v T$ 构成了[封闭系统](@entry_id:139565)，其中 $R$ 是气体常数，$T$ 是温度，$c_v = R/(\gamma - 1)$ 是定容比热。

#### [无量纲化](@entry_id:136704)

在进行数值模拟之前，通常会对控制方程进行**无量纲化 (non-dimensionalization)**。这一过程通过引入参考尺度（如参考长度 $L_{\mathrm{ref}}$、密度 $\rho_{\mathrm{ref}}$、速度 $U_{\mathrm{ref}}$ 和温度 $T_{\mathrm{ref}}$）来重新标度物理量。无量纲化不仅可以简化方程，减少参数数量，还能改善数值问题的尺度特性，避免因变量[数量级](@entry_id:264888)差异过大而导致的精度损失。

我们将[原始变量](@entry_id:753733)（带维度）替换为其无量纲形式（带星号 *）与参考尺度的乘积，例如 $\boldsymbol{x} = L_{\mathrm{ref}} \boldsymbol{x}^{*}$, $t = (L_{\mathrm{ref}}/U_{\mathrm{ref}}) t^{*}$, $\rho = \rho_{\mathrm{ref}} \rho^{*}$等。通过这一变换，[偏导数](@entry_id:146280)也相应地被缩放。经过一系列代数推导，我们可以得到无量纲形式的[欧拉方程](@entry_id:177914)。特别地，无量纲通量向量会显式地包含流动特征的无量纲参数。

例如，考虑二维[欧拉方程](@entry_id:177914)的 $x$ 方向无量纲通量 $\boldsymbol{F}_{x}^{*}$。通过仔细的变量代换，可以将它表示为无量纲原始变量 $(\rho^{*}, u_x^{*}, u_y^{*}, T^{*})$ 以及两个重要的[无量纲数](@entry_id:136814)：比热比 $\gamma$ 和 **[马赫数](@entry_id:274014) (Mach number)** $\mathrm{Ma} = U_{\mathrm{ref}}/a_{\mathrm{ref}}$，其中 $a_{\mathrm{ref}} = \sqrt{\gamma R T_{\mathrm{ref}}}$ 是参考声速。最终得到的无量纲 $x$ 通量为 [@problem_id:3376079]：
$$
\boldsymbol{F}_{x}^{*} = 
\begin{pmatrix}
\rho^{*} u_{x}^{*} \\
\rho^{*} (u_{x}^{*})^{2} + \frac{\rho^{*} T^{*}}{\gamma \mathrm{Ma}^{2}} \\
\rho^{*} u_{x}^{*} u_{y}^{*} \\
\rho^{*} u_{x}^{*} \left( \frac{1}{2}((u_{x}^{*})^{2} + (u_{y}^{*})^{2}) + \frac{T^{*}}{(\gamma - 1)\mathrm{Ma}^{2}} \right)
\end{pmatrix}
$$
这个表达式清晰地展示了压力项和能量项是如何依赖于[马赫数](@entry_id:274014)的平方的。在数值求解器中，我们直接处理这些无量纲方程，从而使代码和结果具有更广泛的适用性。

### 不连续伽辽金弱形式

DG方法的核心思想在于将求解域 $\Omega$ 剖分成一系列不重叠的单元（或元素）$K$。在每个单元内部，解 $U$ 被近似为一个局部多项式 $U_h \in \mathcal{P}_p(K)$，其中 $\mathcal{P}_p$ 是次数不超过 $p$ 的多项式空间。与[连续伽辽金方法](@entry_id:747805)不同，DG方法不要求解在单元边界上连续，这为处理[双曲守恒律](@entry_id:147752)中的间断（如激波）提供了天然的框架。

为了推导[DG方法](@entry_id:748369)的离散格式，我们将控制方程乘以一个测试函数 $v_h \in \mathcal{P}_p(K)$，并在单元 $K$ 上积分：
$$
\int_K (\partial_t U_h) v_h \, d\boldsymbol{x} + \int_K (\nabla \cdot \boldsymbol{F}(U_h)) v_h \, d\boldsymbol{x} = \boldsymbol{0}
$$
对第二项使用[分部积分](@entry_id:136350)（或高维[散度定理](@entry_id:143110)），我们得到[DG方法](@entry_id:748369)的**[弱形式](@entry_id:142897) (weak form)**：
$$
\int_K (\partial_t U_h) v_h \, d\boldsymbol{x} - \int_K \boldsymbol{F}(U_h) : \nabla v_h \, d\boldsymbol{x} + \oint_{\partial K} (\boldsymbol{F}(U_h) \cdot \boldsymbol{n}) v_h \, dS = \boldsymbol{0}
$$
其中 $\boldsymbol{n}$ 是单元边界 $\partial K$ 的单位外法向向量。由于解 $U_h$ 在单元边界上是多值的（从单元内部逼近得到 $U_h^{-}$，从相邻单元逼近得到 $U_h^{+}$），物理通量 $\boldsymbol{F}(U_h) \cdot \boldsymbol{n}$ 的定义是不明确的。[DG方法](@entry_id:748369)的关键创新在于用一个**[数值通量](@entry_id:752791) (numerical flux)** $\widehat{\boldsymbol{F}}(\boldsymbol{U}_h^-, \boldsymbol{U}_h^+, \boldsymbol{n})$ 来代替边界上的物理通量。这个数值通量是[黎曼问题](@entry_id:171440)的近似解，它不仅为单元间的耦合提供了机制，还引入了必要的[数值耗散](@entry_id:168584)以保证稳定性。最终的半离散[DG格式](@entry_id:178043)为：
$$
\int_K (\partial_t U_h) v_h \, d\boldsymbol{x} - \int_K \boldsymbol{F}(U_h) : \nabla v_h \, d\boldsymbol{x} + \oint_{\partial K} \widehat{\boldsymbol{F}}(\boldsymbol{U}_h^-, \boldsymbol{U}_h^+, \boldsymbol{n}) v_h \, dS = \boldsymbol{0}
$$

#### 离散守恒性

守恒性是求解守恒律方程的数值方法的一项至关重要的性质，它确保了在离散层面，物理量的总量在没有边界通量的情况下是守恒的。对于DG方法，要实现**离散守恒性 (discrete conservation)**，数值通量的设计必须满足特定条件。

我们可以通过选择测试函数 $v_h \equiv 1$ 来考察单元 $K$ 内守恒量的总变化率。此时，$\nabla v_h = \boldsymbol{0}$，弱形式简化为单元平衡方程：
$$
\frac{d}{dt} \int_K U_h \, d\boldsymbol{x} + \oint_{\partial K} \widehat{\boldsymbol{F}}(\boldsymbol{U}_h^-, \boldsymbol{U}_h^+, \boldsymbol{n}) \, dS = \boldsymbol{0}
$$
将这个方程在所有单元上求和，我们得到全局量的变化。为了使内部单元交界面上的通量贡献相互抵消，只留下物理边界上的通量，数值通量函数必须满足两个条件：
1.  **[单值性](@entry_id:174849) (Single-valued)**：对于任意一个共享界面，相邻两个单元计算出的[数值通量](@entry_id:752791)的值必须是唯一的（大小相等，方向相反）。
2.  **[反对称性](@entry_id:261893) (Anti-symmetry)**：考虑一个由单元 $K^-$ 和 $K^+$ 共享的界面，其[法向量](@entry_id:264185) $\boldsymbol{n}$ 从 $K^-$ 指向 $K^+$。数值通量必须满足关系 $\widehat{\boldsymbol{F}}(\boldsymbol{U}^-, \boldsymbol{U}^+, \boldsymbol{n}) = - \widehat{\boldsymbol{F}}(\boldsymbol{U}^+, \boldsymbol{U}^-, -\boldsymbol{n})$。

当这两个条件满足时，在全局求和过程中，每个内部界面上的通量贡献 ($\int_f \widehat{\boldsymbol{F}}(\boldsymbol{U}^-, \boldsymbol{U}^+, \boldsymbol{n}) dS$ from $K^-$ and $\int_f \widehat{\boldsymbol{F}}(\boldsymbol{U}^+, \boldsymbol{U}^-, -\boldsymbol{n}) dS$ from $K^+$) 会精确抵消，从而保证了离散守恒性 [@problem_id:3376132]。所有设计良好的数值通量，无论是中心格式还是[迎风格式](@entry_id:756374)，都遵循这一基本原则。

### 参考单元上的变换

为了简化计算和实现，[DG方法](@entry_id:748369)通常在统一的**[参考单元](@entry_id:168425) (reference element)** $\hat{K}$（例如，1D中的 $[-1,1]$，2D中的标准三角形或正方形）上进行。每个物理单元 $K$ 都通过一个光滑的可逆映射 $\boldsymbol{x}(\hat{\boldsymbol{x}})$ 从参考单元变换而来。

通过此变换，物理[坐标系](@entry_id:156346) $(x, y)$ 中的守恒律需要被改写为参考[坐标系](@entry_id:156346) $(\xi, \eta)$ 中的形式。利用[链式法则](@entry_id:190743)，物理空间中的散度可以变换为参考空间中的导数组合。为了保持[守恒形式](@entry_id:747710)，我们将变换后的方程乘以雅可比行列式 $J = \det(\partial \boldsymbol{x} / \partial \hat{\boldsymbol{x}})$。对于一个二维时不变映射，我们得到如下形式的守恒律 [@problem_id:3376127]：
$$
\frac{\partial}{\partial t}\left(J U\right) + \frac{\partial \hat{\boldsymbol{F}}^{\xi}}{\partial \xi} + \frac{\partial \hat{\boldsymbol{F}}^{\eta}}{\partial \eta} = 0
$$
这里的 $\hat{\boldsymbol{F}}^{\xi}$ 和 $\hat{\boldsymbol{F}}^{\eta}$ 是**逆变通量 (contravariant fluxes)**，它们是物理通量 $F$ 和 $G$ 与[映射度](@entry_id:268707)量 (Jacobian matrix entries) 的[线性组合](@entry_id:154743)。具体而言：
$$
\hat{\boldsymbol{F}}^{\xi} = J (\xi_x F + \xi_y G) = y_{\eta} F - x_{\eta} G
$$
$$
\hat{\boldsymbol{F}}^{\eta} = J (\eta_x F + \eta_y G) = -y_{\xi} F + x_{\xi} G
$$
其中 $x_\xi, y_\eta$ 等是[雅可比矩阵](@entry_id:264467) $\partial\boldsymbol{x}/\partial\hat{\boldsymbol{x}}$ 的元素。[DG方法](@entry_id:748369)的弱形式现在可以完全在[参考单元](@entry_id:168425)上构建，所有的积分和求导都在固定的 $(\xi, \eta)$ [坐标系](@entry_id:156346)中进行，这极大地简化了代码的实现，使其能够处理任意形状的网格。

### [基函数](@entry_id:170178)与[半离散系统](@entry_id:754680)

在参考单元上，近似解 $U_h$ 可以展开为一组[基函数](@entry_id:170178) $\{\phi_i(\hat{\boldsymbol{x}})\}_{i=0}^N$ 的[线性组合](@entry_id:154743)：
$$
U_h(\hat{\boldsymbol{x}}, t) = \sum_{j=0}^{N} U_j(t) \phi_j(\hat{\boldsymbol{x}})
$$
其中 $U_j(t)$ 是随时间变化的自由度。将此展开式代入[弱形式](@entry_id:142897)，并选择测试函数 $v_h$ 为[基函数](@entry_id:170178) $\phi_i$，我们得到一个关于自由度 $U_j$ 的[常微分方程组](@entry_id:266774)（即[半离散系统](@entry_id:754680)）：
$$
\boldsymbol{M} \frac{d\boldsymbol{U}}{dt} = \boldsymbol{R}(\boldsymbol{U})
$$
其中 $\boldsymbol{U} = (U_0, ..., U_N)^T$ 是自由度向量，$\boldsymbol{M}$ 是**[质量矩阵](@entry_id:177093) (mass matrix)**，其元素为 $M_{ij} = \int_{\hat{K}} \phi_i \phi_j J \, d\hat{\boldsymbol{x}}$，$\boldsymbol{R}(\boldsymbol{U})$ 是包含体积积分和面积分项的[残差向量](@entry_id:165091)。

#### [模态基](@entry_id:752055)与[节点基](@entry_id:752522)

[基函数](@entry_id:170178)的选择对[DG方法](@entry_id:748369)的性质和效率有重要影响，主要有两种选择 [@problem_id:3376110]：

1.  **[模态基](@entry_id:752055) (Modal Basis)**：通常选用一组在参考单元上$L^2$-正交的多项式，如勒让德多项式 (Legendre polynomials)。对于一维[参考单元](@entry_id:168425) $[-1,1]$，标准[勒让德多项式](@entry_id:141510) $P_n(x)$ 满足：
    $$
    \int_{-1}^{1} P_i(x) P_j(x) \, dx = \frac{2}{2i+1} \delta_{ij}
    $$
    其中 $\delta_{ij}$ 是克罗内克符号。使用[模态基](@entry_id:752055)的一个显著优点是，如果积分被精确计算，[质量矩阵](@entry_id:177093) $\boldsymbol{M}$ 是对角的。这使得求解时间导数项 $\frac{d\boldsymbol{U}}{dt}$ 变得非常简单，只需进行逐元素相除。

2.  **[节点基](@entry_id:752522) (Nodal Basis)**：通常选用一组[拉格朗日插值多项式](@entry_id:176861) $\{\ell_i(x)\}_{i=0}^p$，它们定义在一组预先选择的节点 $\{x_j\}_{j=0}^p$ 上，并满足 $\ell_i(x_j) = \delta_{ij}$。在这种情况下，自由度 $U_j(t)$ 就是解在节点 $x_j$ 上的值，这使得物理解释和施加边界条件更为直观。然而，如果使用精确积分，[拉格朗日基](@entry_id:751105)函数彼此不正交，会导致一个稠密的质量矩阵，求解时间导数项需要矩阵求逆，计算成本高昂。

#### 求积法则与DGSEM方法

在实际应用中，[弱形式](@entry_id:142897)中的积分通常通过**[数值求积](@entry_id:136578) (numerical quadrature)**来近似计算。求积法则的选择与[基函数](@entry_id:170178)的选择密切相关，并能带来巨大的计算优势。

一个特别强大且流行的组合是使用**[勒让德-高斯-洛巴托](@entry_id:751235) ([Legendre-Gauss-Lobatto](@entry_id:751235), LGL)** 节点来定义[节点基](@entry_id:752522)，并使用相应的LGL[求积法则](@entry_id:753909)来计算积分 [@problem_id:3376110]。LGL求积法则使用LGL节点作为求积点，其[求积权重](@entry_id:753910) $\{w_q\}$ 均为正。当我们用LGL求积来计算基于LGL节点的[拉格朗日基](@entry_id:751105)的质量矩阵时：
$$
M_{ij} = \int_{-1}^{1} \ell_i(x) \ell_j(x) \, dx \approx \sum_{q=0}^{p} w_q \ell_i(x_q) \ell_j(x_q)
$$
由于 $\ell_i(x_q) = \delta_{iq}$，上式简化为 $M_{ij} \approx w_i \delta_{ij}$。这意味着[质量矩阵](@entry_id:177093)变成了[对角矩阵](@entry_id:637782)，其对角元素就是LGL[求积权重](@entry_id:753910)。这种技术被称为**[质量集中](@entry_id:175432) (mass lumping)**，它结合了[节点基](@entry_id:752522)的直观性和[模态基](@entry_id:752055)的[计算效率](@entry_id:270255)，是现代[DG方法](@entry_id:748369)（特别是高阶方法）的基石。

当这种[节点基](@entry_id:752522)与求积点重合的策略被系统地应用到所有积分项时，[DG方法](@entry_id:748369)就演变成了所谓的**不连续伽辽金[谱元法](@entry_id:755171) (Discontinuous Galerkin Spectral Element Method, DGSEM)** [@problem_id:3376080]。在这种框架下，体积积分项 $\int_{-1}^{1} \ell_i'(x) \boldsymbol{F}(U_h) \, dx$ 也通过LGL求积近似。这使得整个空间离散算子可以表示为一个作用于节点值的矩阵向量乘积。特别是，导数算子可以表示为一个**[微分矩阵](@entry_id:149870) (differentiation matrix)** $D$，其元素为 $D_{ij} = \ell_j'(\xi_i)$。这个矩阵有明确的解析形式，可以预先计算和存储。DGSEM方法因其高效率和与谱方法的紧密联系而备受青睐。

### DG算子的关键组件

一个DG求解器的核心是构建并应用离散算子，它主要由[质量矩阵](@entry_id:177093)和包含体积与[面积分](@entry_id:275394)量的残差项组成。

#### 质量矩阵

如前所述，**质量矩阵** $\boldsymbol{M}$ 源于[弱形式](@entry_id:142897)中的时间导数项。其结构由[基函数](@entry_id:170178)和积分方式决定。
- 对于1D中的模态勒让德基，精确积分得到对角矩阵 $M_{ii}^{\text{modal}} = 2/(2i+1)$ [@problem_id:3376110]。
- 对于1D中的LGL[节点基](@entry_id:752522)，LGL求积得到[对角矩阵](@entry_id:637782) $M_{ii}^{\text{nodal}} = w_i$，其中 $w_i$ 是LGL权重 [@problem_id:3376110]。
- 对于2D或3D中的[节点基](@entry_id:752522)，通过在节点上进行求积同样可以得到[对角质量矩阵](@entry_id:173002)。但在某些情况下，例如为了理论分析或当几何形状复杂时，可能会使用精确积分，此时[质量矩阵](@entry_id:177093)是稠密的。例如，在2D标准三角形上使用线性($p=1$)[拉格朗日基](@entry_id:751105)函数，精确积分得到的[质量矩阵](@entry_id:177093)是稠密且对称的 [@problem_id:3376139]。

#### [提升算子](@entry_id:751273)

[DG方法](@entry_id:748369)的一个优雅的表述方式是通过**[提升算子](@entry_id:751273) (lift operator)** $\boldsymbol{L}^{(f)}$。这个算子将单元边界上的通量跃度（即数值通量与内部物理通量的差）“提升”为一个定义在单元内部的多项式。具体来说，[DG弱形式](@entry_id:748377)中的[面积分](@entry_id:275394)项可以等价地写成一个体积积分：
$$
\oint_{\partial K} \widehat{\boldsymbol{F}} v_h \, dS - \int_K \boldsymbol{F}(U_h) : \nabla v_h \, dS = \dots \implies \int_K \boldsymbol{S}_h \cdot \nabla v_h \, d\boldsymbol{x} + \int_K \boldsymbol{L}(\llbracket U_h \rrbracket) v_h \, d\boldsymbol{x}
$$
(注：此为split-form DG的视角，但[提升算子](@entry_id:751273)的概念更通用)。更直接地，[提升算子](@entry_id:751273)将边界上的通量不匹配 $ \widehat{\boldsymbol{F}} - \boldsymbol{F}(U_h^-)\cdot\boldsymbol{n}$ 映射到体积贡献。其定义为 $\boldsymbol{L}^{(f)} := \boldsymbol{M}^{-1} \boldsymbol{R}^{(f)}$，其中 $\boldsymbol{R}^{(f)}$ 是一个“面质量矩阵”，其元素为 $R_{i\alpha}^{(f)} = \int_{f} \phi_i \ell_{\alpha} \, ds$，它将面上的自由度（由面[基函数](@entry_id:170178) $\ell_\alpha$ 表示）耦合到体内的自由度（由体[基函数](@entry_id:170178) $\phi_i$ 表示）。[提升算子](@entry_id:751273)是实现DG方法的一种高效且[代数结构](@entry_id:137052)清晰的方式，尤其适用于非结构网格 [@problem_id:3376139]。

### 欧拉方程的数值通量

[数值通量](@entry_id:752791)的选择对DG方法的性能至关重要，它决定了格式的稳定性和精度。一个好的[数值通量](@entry_id:752791)应满足：
- **相容性 (Consistent)**：当左右状态相同时，$\widehat{\boldsymbol{F}}(W,W,\boldsymbol{n}) = \boldsymbol{F}(W)\cdot \boldsymbol{n}$，确保对于光滑解，格式能收敛到正确的PDE [@problem_id:3376101]。
- **守恒性 (Conservative)**：如前所述，满足[反对称性](@entry_id:261893)以确保全局守恒。
- **稳定性 (Stable)**：引入适量的[数值耗散](@entry_id:168584)来抑制非物理[振荡](@entry_id:267781)，尤其是在间断附近。

对于[欧拉方程](@entry_id:177914)，常用的[数值通量](@entry_id:752791)包括 [@problem_id:3376084]：
- **Lax-Friedrichs通量 (LLF)** 或 **[Rusanov通量](@entry_id:637224)**：这是最简单的数值通量之一。它在[中心通量](@entry_id:747204)的基础上增加了一个与左右状态差成正比的耗散项，耗散系数由局部最大特征[波速](@entry_id:186208)决定。LLF通量非常鲁棒，但其耗散是各向同性的，即它对所有特征波（包括移动缓慢的接触间断）都施加了同样强的耗散。这会导致对接触间断和[剪切层](@entry_id:274623)过度模糊，降低了[高阶方法](@entry_id:165413)的实际精度。
- **[Roe通量](@entry_id:754409)**：这是一种基于[特征分解](@entry_id:181333)的线性化[黎曼求解器](@entry_id:754362)。它为每个特征波引入与其[波速](@entry_id:186208)成比例的耗散，因此对移动缓慢的接触间断几乎不施加耗散，能够非常清晰地捕捉它们。然而，[Roe通量](@entry_id:754409)可能不满足[熵条件](@entry_id:166346)（需要“[熵修正](@entry_id:749021)”），并且在某些状态（如强[稀疏波](@entry_id:168428)或接近真空）下可能变得“脆弱”，产生非物理结果（如负压）。
- **[HLLC通量](@entry_id:750350) (Harten-Lax-van Leer-Contact)**：这是对[HLL通量](@entry_id:750354)的改进。[HLL通量](@entry_id:750354)假设黎曼扇中只有两个波（左[行波](@entry_id:185008)和右[行波](@entry_id:185008)），因此会模糊接触间断。HLLC在此基础上恢复了中间的接触波，构建了一个三波模型。它能够像[Roe通量](@entry_id:754409)一样精确地捕捉[接触间断](@entry_id:194702)，同时又如LLF通量一样鲁棒，且能保证正定性。由于其在精度和鲁棒性之间的出色平衡，[HLLC通量](@entry_id:750350)成为高阶DG方法求解[欧拉方程](@entry_id:177914)的优选方案。

### 稳定性与精度考量

除了数值通量的选择，DG方法的稳定性和精度还受到其他几个因素的影响。

#### [混叠](@entry_id:146322)失稳

在DG方法中，当处理像欧拉方程这样的[非线性](@entry_id:637147)通量时，一个微妙的挑战是**[混叠](@entry_id:146322)失稳 (aliasing instability)**。这个问题源于在求积过程中对[非线性](@entry_id:637147)项的近似计算。例如，考虑通量 $f(u) = \frac{1}{2}u^2$。如果解 $u_h$ 是一个 $p$ 次多项式，那么 $f(u_h)$ 就是一个 $2p$ 次多项式。在弱形式的体积积分 $\int_K \nabla v_h \cdot f(U_h) \, d\boldsymbol{x}$ 中，被积函数是一个更高次的多项式。如果使用的求积法则的精度不足以精确计算这个积分（即“欠积分”），就会产生混叠错误。

这种错误会破坏离散算子的某些对称性（如[反对称性](@entry_id:261893)），从而引入虚假的能量产生项。在一个简化的模型问题中可以证明，即使边界通量为零，欠积分也可能导致单元内的离散能量随时间增长，最终导致计算发散 [@problem_id:3376105]。为了克服这个问题，可以使用更高精度的求积法则（通常要求能精确积分 $3p$ 次多项式，这被称为de-aliasing），或者采用所谓的“分裂形式”(split-form) DG，它通过代数操作恢复了离散算子的[能量守恒](@entry_id:140514)性质。

#### 正定性保持

欧拉方程的物理[可行解](@entry_id:634783)必须满足密度 $\rho > 0$ 和压力 $p > 0$（即内能为正）。然而，标准的高阶[DG方法](@entry_id:748369)由于其[多项式逼近](@entry_id:137391)会产生[振荡](@entry_id:267781)（[吉布斯现象](@entry_id:138701)），尤其是在间断附近，这可能导致数值解在某些点上出现非物理的负密度或负压，从而使计算崩溃。

为了解决这个问题，**[正定性](@entry_id:149643)保持 (positivity-preserving)**技术被发展出来。一个广泛采用的策略是Zhang-Shu型限制器 [@problem_id:3376125]。其核心思想是，如果一个单元的平均状态是正定的，那么可以通过将该单元内求积点上的值向单元平均值进行缩放来保证这些点上的值也是正定的。这就将问题转化为如何保证单元平均值在时间演化中保持正定。

这可以通过结合使用鲁棒的[数值通量](@entry_id:752791)（如LLF）和满足特定[时间步长限制](@entry_id:756010)的**强稳定性保持 (Strong Stability Preserving, SSP)** [时间积分方法](@entry_id:136323)（如SSP-RK）来实现。[SSP方法](@entry_id:755294)保证了如果一个前向欧拉步满足某个[凸集](@entry_id:155617)[不变性](@entry_id:140168)（如正定性），那么高阶[SSP方法](@entry_id:755294)在更严格的时间步长下也能保持该性质。因此，一个充分的CFL条件可以被推导出来，它依赖于单元几何、[求积法则](@entry_id:753909)常数、局部最大[波速](@entry_id:186208)以及[SSP方法](@entry_id:755294)的系数，以确保单元平均值和节点值始终保持物理上的[正定性](@entry_id:149643)。

#### [先验误差估计](@entry_id:170366)

对于光滑解，[DG方法](@entry_id:748369)的精度可以通过**[先验误差估计](@entry_id:170366) (a priori error estimates)**来理论分析。对于一个使用 $p$ 次多项式的[DG方法](@entry_id:748369)，在光滑解区域，其 $L^2$ 范数下的[收敛阶](@entry_id:146394)通常被证明为 $O(h^{p+1})$，其中 $h$ 是网格尺寸。然而，对于[双曲守恒律](@entry_id:147752)，标准的DG分析得到一个略微次优的收敛阶 [@problem_id:3376101]：
$$
\|U(t) - U_h(t)\|_{L^2(\Omega)} \le C \, h^{p+1/2}
$$
这里的半阶损失 ($h^{1/2}$)源于控制单元边界上解的跳跃项。在[误差分析](@entry_id:142477)中，这些边界项通过[迹不等式](@entry_id:756082)进行估计，而[迹不等式](@entry_id:756082)会引入一个 $h^{-1/2}$ 的因子，导致最终误差界中出现 $h^{p+1/2}$。这个结果是[DG方法](@entry_id:748369)处理双曲问题时的一个经典理论特征。

实现这一收敛阶的前提是[数值通量](@entry_id:752791)的**相容性 (consistency)**。正如前面所讨论的，相容性保证了当数值解等于精确解时，格式的残差为零。如果通量不相容，会引入一个 $O(1)$ 的误差项，从而阻止格式收敛到正确的解 [@problem_id:3376101]。这一系列的理论分析构成了DG方法严格数学基础的一部分，并指导了数值格式的设计与改进。