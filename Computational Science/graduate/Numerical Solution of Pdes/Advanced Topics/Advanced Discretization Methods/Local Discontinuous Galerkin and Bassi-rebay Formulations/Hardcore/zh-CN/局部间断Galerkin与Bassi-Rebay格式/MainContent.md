## 引言
在[偏微分方程](@entry_id:141332)（PDEs）的数值求解领域，间断Galerkin (DG) 方法因其处理复杂几何、[非协调网格](@entry_id:752550)以及实现任意[高阶精度](@entry_id:750325)的灵活性而备受瞩目。其中，局部间断Galerkin ([LDG](@entry_id:751395)) 方法与 Bassi-Rebay (BR) 格式作为两种先进的DG变体，为求解[扩散](@entry_id:141445)主导及更复杂的[多物理场](@entry_id:164478)问题提供了强有力的工具。然而，理解其背后的数学机理、掌握其高阶实现的细微差别，并认识其在不同科学工程领域中的应用潜力，是充分发挥其优势的关键。本文旨在弥合理论与应用之间的鸿沟，为读者提供一份关于[LDG](@entry_id:751395)与BR格式的全面指南。

在接下来的章节中，我们将踏上一段从核心原理到前沿应用的探索之旅。在“原理与机制”一章中，我们将深入剖析这些方法是如何从基本的单元[弱形式](@entry_id:142897)演化而来，重点阐述数值通量和[提升算子](@entry_id:751273)等关键构件如何确保方法的稳定性与守恒性。随后，在“应用与跨学科连接”一章中，我们将展示这些理论工具如何在[计算流体动力学](@entry_id:147500)、[材料科学](@entry_id:152226)乃至新兴的数据科学领域中解决实际挑战，彰显其强大的适用性。最后，通过“动手实践”部分，我们将引导读者将理论知识转化为具体的计算技能。让我们首先从这两种方法的基本构造和数学原理开始。

## 原理与机制

本章旨在深入阐述局部间断Galerkin ([LDG](@entry_id:751395)) 方法与Bassi-Rebay (BR) 方法的核心原理和内在机制。我们将从[偏微分方程](@entry_id:141332)的单元弱形式出发，揭示[数值通量](@entry_id:752791)的必要性，并逐步构建起这些先进的间断Galerkin (DG) 格式。我们将重点讨论这些方法设计的关键构件，如数值通量、[提升算子](@entry_id:751273)，以及它们如何确保方法的稳定性、一致性与局部守恒性。此外，我们还将探讨与高阶实现相关的实际问题，包括[基函数](@entry_id:170178)的选择、刚度[矩阵的[条件](@entry_id:150947)数](@entry_id:145150)，以及高效代数求解器的设计，最后对这些方法进行综合比较，以揭示它们在不同应用场景下的优势与局限。

### 从混合方法到局部间断Galerkin ([LDG](@entry_id:751395))

为了求解[二阶椭圆问题](@entry_id:754613)，例如标量扩散方程 $-\nabla \cdot (\kappa \nabla u) = f$，一个有效且系统的方式是将其重写为[一阶系统](@entry_id:147467)。通过引入一个辅助变量来表示通量，即 $\mathbf{q} = -\kappa \nabla u$，原方程可分解为：
$$
\begin{cases}
\mathbf{q} + \kappa \nabla u = \mathbf{0} \\
\nabla \cdot \mathbf{q} = f
\end{cases}
$$
这种形式被称为**混合形式** (mixed form)，因为它同时求解[原始变量](@entry_id:753733) $u$ 和通量变量 $\mathbf{q}$。

局部间断Galerkin ([LDG](@entry_id:751395)) 方法正是基于这[一阶系统](@entry_id:147467)。在一个由互不重叠的单元 $K$ 组成的网格 $\mathcal{T}_h$ 上，我们定义了分片[多项式空间](@entry_id:144410) $V_h$ 和 $\mathbf{W}_h$ 来分别逼近 $u$ 和 $\mathbf{q}$。在每个单元 $K$ 内，我们将上述两个方程分别乘以测试函数 $v \in V_h$ 和 $\boldsymbol{\tau} \in \mathbf{W}_h$，然后进行[分部积分](@entry_id:136350)，得到单元弱形式：
$$
\int_K \mathbf{q}_h \cdot \boldsymbol{\tau} \, d\mathbf{x} - \int_K \kappa u_h (\nabla \cdot \boldsymbol{\tau}) \, d\mathbf{x} + \int_{\partial K} \kappa u_h (\boldsymbol{\tau} \cdot \mathbf{n}_K) \, dS = 0 \quad \forall \boldsymbol{\tau} \in \mathbf{W}_h
$$
$$
-\int_K \mathbf{q}_h \cdot \nabla v \, d\mathbf{x} + \int_{\partial K} v (\mathbf{q}_h \cdot \mathbf{n}_K) \, dS = \int_K f v \, d\mathbf{x} \quad \forall v \in V_h
$$
由于逼近解 $u_h$ 和 $\mathbf{q}_h$ 在单元边界 $\partial K$ 上是间断的，其迹（trace）是双值的。因此，我们必须用精心设计的**数值通量** (numerical fluxes)，记作 $\widehat{u}_h$ 和 $\widehat{\mathbf{q}}_h$，来替换单元边界上的 $u_h$ 和 $\mathbf{q}_h \cdot \mathbf{n}_K$。这使得[弱形式](@entry_id:142897)变为：
$$
\int_K \mathbf{q}_h \cdot \boldsymbol{\tau} \, d\mathbf{x} - \int_K \kappa u_h (\nabla \cdot \boldsymbol{\tau}) \, d\mathbf{x} + \int_{\partial K} \kappa \widehat{u}_h (\boldsymbol{\tau} \cdot \mathbf{n}_K) \, dS = 0
$$
$$
-\int_K \mathbf{q}_h \cdot \nabla v \, d\mathbf{x} + \int_{\partial K} v (\widehat{\mathbf{q}}_h \cdot \mathbf{n}_K) \, dS = \int_K f v \, d\mathbf{x}
$$
[LDG方法](@entry_id:751397)的关键在于数值通量的选择。为了保证稳定性，通量的选择必须是协调的。一种常见且有效的选择是**交替通量** (alternating fluxes)。在一个内部界面 $F$ 上，该界面是单元 $K^+$ 和 $K^-$ 的公共边界，我们可以选择：
$$
\widehat{u}_h = u_h^- \quad \text{和} \quad \widehat{\mathbf{q}}_h = \mathbf{q}_h^+
$$
或者
$$
\widehat{u}_h = u_h^+ \quad \text{和} \quad \widehat{\mathbf{q}}_h = \mathbf{q}_h^-
$$
这种“向上取值”的选择取决于信息流动的方向，但对于[扩散](@entry_id:141445)问题，方向是任意的，只要在整个计算中保持一致即可。更一般地，[数值通量](@entry_id:752791)可以取为平均值和罚项的组合，例如：
$$
\widehat{u}_h = \{u_h\} - C_{11} \llbracket u_h \rrbracket - C_{12} \llbracket \mathbf{q}_h \rrbracket
$$
$$
\widehat{\mathbf{q}}_h = \{\mathbf{q}_h\} - C_{21} \llbracket u_h \rrbracket - C_{22} \llbracket \mathbf{q}_h \rrbracket
$$
其中 $\{\cdot\}$ 表示平均，$\llbracket \cdot \rrbracket$ 表示跨界面的跳跃。通过恰当选择系数 $C_{ij}$，可以确保方法的稳定性和收敛性。

从一个更抽象的视角看，[LDG方法](@entry_id:751397)可以被理解为一种离散的**[亥姆霍兹分解](@entry_id:181767)** (Helmholtz decomposition)。[亥姆霍兹分解](@entry_id:181767)定理指出，任何足够光滑的向量场（如此处的通量 $\mathbf{q}$）可以被唯一地分解为一个[无旋场](@entry_id:183486)（梯度部分）和一个[无散场](@entry_id:260932)（散度自由部分）的和。[LDG方法](@entry_id:751397)的目标正是找到通量场 $\mathbf{q}$ 在梯度空间 $\nabla V_h$ 上的最佳逼近。具体来说，它求解 $u_h \in V_h$，使得 $\nabla u_h$ 是 $\mathbf{q}$ 在 $\nabla V_h$ 上的 $L^2$ [正交投影](@entry_id:144168)，即满足 $(\mathbf{q} - \nabla u_h, \nabla v_h)_K = 0$ 对所有 $v_h \in V_h$ 成立。这个[正交性条件](@entry_id:168905)正是L[DG[弱形](@entry_id:748377)式](@entry_id:142897)的核心。

### 局部守恒性：DG方法的一个基本性质

DG方法的一个标志性优点是其内在的**局部守恒性** (local conservation)。这个性质直接源于其单元层面的弱形式构造，并且对于模拟物理[守恒定律](@entry_id:269268)至关重要。我们可以通过一个简单的步骤来揭示这一性质。

考虑[扩散](@entry_id:141445)问题的第二个方程 $\nabla \cdot \mathbf{q} = f$ 的[DG弱形式](@entry_id:748377)：
$$
-\int_K \mathbf{q}_h \cdot \nabla v \, d\mathbf{x} + \int_{\partial K} v (\widehat{\mathbf{q}}_h \cdot \mathbf{n}_K) \, dS = \int_K f v \, d\mathbf{x}
$$
这个方程对所有测试函数 $v \in V_h$ 都成立。由于我们的多项式空间 $V_h$ 包含了[常数函数](@entry_id:152060)（即 $p \ge 0$），我们可以选择一个特殊的测试函数 $v \equiv 1$。对于这个选择，其梯度 $\nabla v = \mathbf{0}$。因此，体积积分项 $-\int_K \mathbf{q}_h \cdot \nabla v \, d\mathbf{x}$ 精确地为零。弱形式立即简化为：
$$
\int_{\partial K} \widehat{\mathbf{q}}_h \cdot \mathbf{n}_K \, dS = \int_K f \, d\mathbf{x}
$$
这个方程有一个清晰的物理解释：离开单元 $K$ 的总[数值通量](@entry_id:752791)精确地等于单元 $K$ 内部[源项](@entry_id:269111)的总和。这正是物理量在单元 $K$ 上的[守恒定律](@entry_id:269268)的离散体现。对于瞬态守恒律问题，如 $\partial_t u + \nabla \cdot \mathbf{F}(u) = 0$，采用相同的步骤，取 $v \equiv 1$，可以得到：
$$
\frac{d}{dt} \int_K u_h \, d\mathbf{x} + \int_{\partial K} \widehat{\mathbf{F}} \cdot \mathbf{n}_K \, dS = 0
$$
这表明单元内 $u_h$ 的总量变化率精确地由通过边界的[数值通量](@entry_id:752791)平衡。

这个性质的成立依赖于两个关键条件：第一，测试[函数空间](@entry_id:143478)必须包含常数函数；第二，所使用的[数值积分](@entry_id:136578)（求积）规则必须足够精确，以至于当 $v$ 是常数时，梯度项的积分为零。只要满足这些条件，任何基于这种弱形式构造的DG方法（包括[LDG](@entry_id:751395)和Bassi-Rebay方法）都是天然局部守恒的。

### Bassi-Rebay 方法：一种基于[提升算子](@entry_id:751273)的[原始变量](@entry_id:753733)方法

尽管[LDG方法](@entry_id:751397)在理论上很优雅，但它引入了额外的通量变量 $\mathbf{q}_h$，导致全局自由度数量增加。Bassi-Rebay方法家族则提供了一种仅求解原始变量 $u_h$ 的替代方案，同时巧妙地利用了混合方法的思想。其核心工具是**[提升算子](@entry_id:751273)** (lifting operator)。

#### [提升算子](@entry_id:751273)：定义与性质

[提升算子](@entry_id:751273)是一种将定义在单元界面上的函数（通常是解的跳跃）“提升”为定义在单元体内的向量场的技术。这种转换使得原本的界面积分可以被等价地表示为[体积分](@entry_id:171119)，从而在代数上统一处理。

我们区分两种[提升算子](@entry_id:751273)：
1.  **局部[提升算子](@entry_id:751273) (Local Lifting Operator)** $\mathcal{R}_e^K$：对于单元 $K$ 的一个面 $e$，它将面上的标量函数 $g$ 映射到一个仅在单元 $K$ 内部非零的向量场 $\mathcal{R}_e^K(g)$。其定义为：对于所有向量测试函数 $\boldsymbol{\tau}_h \in [\mathbb{P}_p(K)]^d$，满足
    $$
    \int_K \mathcal{R}_e^K(g) \cdot \boldsymbol{\tau}_h \, d\mathbf{x} = \int_e g \, (\boldsymbol{\tau}_h|_K \cdot \mathbf{n}_K) \, dS
    $$

2.  **全局[提升算子](@entry_id:751273) (Global Lifting Operator)** $\mathcal{R}$：它将定义在所有界面上的函数 $g$ 映射到一个在整个计算域上（分片地）定义的向量场 $\mathcal{R}(g)$。其定义为：对于所有向量测试函数 $\boldsymbol{\tau}_h \in \mathbf{W}_h$，满足
    $$
    \sum_{K \in \mathcal{T}_h} \int_K \mathcal{R}(g) \cdot \boldsymbol{\tau}_h \, d\mathbf{x} = \sum_{e \in \partial \mathcal{T}_h} \int_e g \, \{\boldsymbol{\tau}_h \cdot \mathbf{n}\} \, dS
    $$
    其中 $\{\boldsymbol{\tau}_h \cdot \mathbf{n}\}$ 是法向通量的平均值。

[提升算子](@entry_id:751273)本质上是[Riesz表示定理](@entry_id:140012)的应用，它将一个线性泛函（右侧的界面积分）表示为与某个函数（左侧的提升结果）的[内积](@entry_id:158127)。

#### 从BR1到BR2的演进

Bassi和Rebay的开创性工作利用[提升算子](@entry_id:751273)来构造一个改进的梯度，并在此基础上定义[数值通量](@entry_id:752791)。

**原始Bassi-Rebay方法 (BR1)** 使用全局[提升算子](@entry_id:751273)来修正分片梯度。它首先计算解的跳跃 $\llbracket u_h \rrbracket$ 的全局提升 $\mathcal{R}(\llbracket u_h \rrbracket)$，然后构造一个重构梯度 $\boldsymbol{G}_h(u_h) = \nabla_h u_h + \mathcal{R}(\llbracket u_h \rrbracket)$。界面上的[数值通量](@entry_id:752791)则取为这个重构梯度的平均值，即 $\widehat{\mathbf{q}}_h = -\{\kappa \boldsymbol{G}_h(u_h)\}$。

然而，BR1方法有一个显著的缺点：它导致了一个**非紧致的计算模板** (non-compact stencil)。考虑单元 $K_1$ 的计算，它需要其邻居 $K_2$ 的重构梯度 $\boldsymbol{G}_h(u_h)|_{K_2}$。由于 $\boldsymbol{G}_h(u_h)|_{K_2}$ 的计算涉及 $K_2$ 所有界面上的跳跃，其中一个界面可能是与 $K_3$ 共享的，因此 $K_1$ 的计算依赖于 $K_2$ 的邻居 $K_3$ 的信息。这意味着一个单元的更新依赖于其“邻居的邻居”，形成了一个两环（two-ring）的计算模板。这增加了矩阵的带宽和计算的复杂性。

**Bassi-Rebay 2 (BR2) 方法** 通过使用局部[提升算子](@entry_id:751273)解决了这个问题。在BR2中，稳定项不再通过平均重构梯度来引入，而是直接定义为一个惩罚项，该惩罚项是解的跳跃经过局部提升后在单元体上的 $L^2$ [内积](@entry_id:158127)。其[双线性形式](@entry_id:746794)通常包含三部分：标准的[体积分](@entry_id:171119)项、与原始弱形式一致的界面项，以及一个基于[提升算子](@entry_id:751273)的稳定项：
$$
a_{\mathrm{BR2}}(u,v) = \sum_{K \in \mathcal{T}_h} \int_K \kappa \nabla u \cdot \nabla v \, d\mathbf{x} - (\text{consistency terms}) + \sum_{F \in \mathcal{F}_h^{\mathrm{int}}} \eta \int_{\omega_F} \kappa \, \mathbf{r}_F(\llbracket u \rrbracket) \cdot \mathbf{r}_F(\llbracket v \rrbracket) \, d\mathbf{x}
$$
其中 $\mathbf{r}_F$ 是与界面 $F$ 相关的局部[提升算子](@entry_id:751273)，$\omega_F$ 是共享界面 $F$ 的两个单元的并集，$\eta$ 是一个稳定参数。因为每个[提升算子](@entry_id:751273) $\mathbf{r}_F$ 只依赖于其对应界面 $F$ 上的跳跃，并只作用于相邻的两个单元，所以单元 $K$ 只与其直接通过面相邻的单元耦合。这确保了BR2方法具有**紧致的计算模板** (compact stencil)，这是其相对于BR1的主要优势。

有趣的是，BR2的稳定项在谱意义上等价于一个经典的**[对称内部罚](@entry_id:755719)方法** (Symmetric Interior Penalty Galerkin, SIPG) 的罚项。SIPG的稳定项形式为 $\sum_F \int_F \tau \llbracket u \rrbracket \cdot \llbracket v \rrbracket dS$。在BR2中，通过[提升算子](@entry_id:751273)，界面上的跳跃惩罚被转化为了相邻单元体上的[体积分](@entry_id:171119)惩罚。这种等价性意味着，尽管形式不同，BR2和SIPG在本质上是通过相似的机制来[稳定数值格式](@entry_id:755322)的。

### 高阶方法的理论与实践

为了充分发挥DG方法的潜力，尤其是在追求高精度解时，采用高阶[多项式逼近](@entry_id:137391)（大 $p$）是至关重要的。然而，这给理论分析和实际实现都带来了新的挑战。

#### [基函数](@entry_id:170178)的选择：[模态基](@entry_id:752055)与[节点基](@entry_id:752522)

在高阶DG方法中，单元内[基函数](@entry_id:170178)的选择对计算效率和数值稳定性有深远影响。主要有两种选择：

1.  **[模态基](@entry_id:752055) (Modal Basis)**：通常选择一组在参考单元上 $L^2$-正交的多项式，如[勒让德多项式](@entry_id:141510)。其主要优点是，在经过[仿射变换](@entry_id:144885)到物理单元后，对应的**质量矩阵** ($M_{ij} = \int_K \phi_i \phi_j d\mathbf{x}$) 是对角阵（通常是单位阵的倍数）。在实现BR2等方法时，计算[提升算子](@entry_id:751273)需要求解形如 $\mathbf{M}_K \mathbf{r}_F = \mathbf{b}_F$ 的[线性系统](@entry_id:147850)。如果质量矩阵 $\mathbf{M}_K$ 是对角的，其逆矩阵的计算是平凡的，极大地简化了[提升算子](@entry_id:751273)的组装过程。

2.  **[节点基](@entry_id:752522) (Nodal Basis)**：通常选择一组[拉格朗日多项式](@entry_id:142463)，其在一个预定义的节点集上满足插值性质。这种[基函数](@entry_id:170178)使得自由度具有明确的物理解释（即在节点上的函数值），便于施加边界条件和进行后处理。然而，其缺点是[质量矩阵](@entry_id:177093)通常是**稠密的**，且其条件数对节点的[分布](@entry_id:182848)非常敏感。对于[等距节点](@entry_id:168260)，质量[矩阵的[条件](@entry_id:150947)数](@entry_id:145150)会随着多项式次数 $p$ 的增加而急剧恶化。即使是对于更优的[Gauss-Lobatto-Legendre节点](@entry_id:165096)，[条件数](@entry_id:145150)仍然会随 $p$ [多项式增长](@entry_id:177086)。这意味着求解[提升算子](@entry_id:751273)所需的[线性系统](@entry_id:147850)在数值上更敏感，并且每次求解都需要 $O(n_K^3)$ 的计算量（其中 $n_K \sim p^d$ 是单元自由度数目）来预计算[矩阵的逆](@entry_id:140380)或进行[LU分解](@entry_id:144767)。

总的来说，对于涉及大量局部[矩阵求逆](@entry_id:636005)的[DG格式](@entry_id:178043)（如BR2），使用模态正交基通常在计算上更具优势，因为它避免了稠密质量矩阵带来的高昂计算成本和潜在的[数值不稳定性](@entry_id:137058)。

#### 稳定性、罚项与条件数

[DG方法](@entry_id:748369)的稳定性是通过在双线性形式中加入惩罚项来保证的，如SIPG的界面罚项或BR2的[提升算子](@entry_id:751273)罚项。这个罚项必须足够大才能控制解在界面上的跳跃，从而保证**[矫顽性](@entry_id:159399)** (coercivity)。理论分析表明，为了平衡来自[迹不等式](@entry_id:756082)和[逆不等式](@entry_id:750800)的项，罚参数 $\tau$ 必须满足一定的缩放规律。

对于次数为 $p$ 的多项式和特征尺寸为 $h$ 的网格，罚参数 $\tau$ 的最优缩放规律为：
$$
\tau \sim \frac{p^2}{h}
$$
这个缩放保证了方法在 $h \to 0$ 或 $p \to \infty$ 时的稳定性。然而，过大的罚参数会损害线性系统的条件数。对DG[刚度矩阵](@entry_id:178659) $K$ 的谱分析可以揭示其条件数 $\kappa(K) = \lambda_{\max}/\lambda_{\min}$ 的行为。

-   最大[特征值](@entry_id:154894) $\lambda_{\max}$ 的尺度由[逆不等式](@entry_id:750800)决定，主要受两个部分的控制：梯度项和罚项。它们的贡献分别缩放为 $\lambda_{\max} \sim \frac{p^4}{h^2} + \tau \frac{p^2}{h}$。
-   [最小特征值](@entry_id:177333) $\lambda_{\min}$ 的尺度由离散[庞加莱不等式](@entry_id:142086)决定。在满足 $\tau \sim p^2/h$ 的条件下，$\lambda_{\min}$ 通常是有界的，即 $\lambda_{\min} \sim 1$。

将最优的罚参数缩放 $\tau \sim p^2/h$ 代入 $\lambda_{\max}$ 的表达式中，我们发现两项具有相同的尺度。因此，最终条件数的渐进行为是：
$$
\kappa(K) \sim \frac{p^4}{h^2}
$$
这个结果揭示了[DG方法](@entry_id:748369)的一个内在挑战：随着多项式次数 $p$ 的增加或网格 $h$ 的加密，线性系统的病态性会迅速恶化，这对代数求解器的性能提出了严峻的考验。

#### 高效求解器设计：[DG方法](@entry_id:748369)的多重网格策略

由于DG方法产生的线性系统规模庞大且条件数高，设计高效的求解器至关重要。**[多重网格](@entry_id:172017)** (Multigrid) 方法是求解此类问题的理想选择，因为它具有计算量与自由度数成线性的潜力。多重网格的核心是**光滑子** (smoother)，其作用是衰减高频误差。

[DG方法](@entry_id:748369)中误差的高频分量通常表现为在单元间剧烈[振荡](@entry_id:267781)的跳跃模式。一个有效的光滑子必须能有效地抑制这些模式。不同[DG格式](@entry_id:178043)的耦合结构决定了哪种光滑子更有效。

-   对于**SIPG**，单元间的耦合主要通过界面罚项实现，这是一种相对“软”的耦合。因此，像**单元块雅可比** (element-block Jacobi) 这样的简单光滑子，即在每个单元上求解局部问题，往往就能提供足够的阻尼效果。

-   对于**BR2**，情况则完全不同。如前所述，其[提升算子](@entry_id:751273)稳定项在相邻单元之间引入了非常强的、稠密的耦合。这种耦合不仅涉及界面自由度，还贯穿到单元内部。单元块[雅可比](@entry_id:264467)光滑子无法有效处理这种强耦合，因为它将这部分耦合视为显式项处理。因此，对于BR2方法，必须采用更强的光滑子，如**界面块（或面片）松弛** (face-based patch relaxation)。这种光滑子将共享一个界面的两个相邻单元视为一个“面片”，并同时求解该面片上的所有自由度。通过隐式地处理由[提升算子](@entry_id:751273)引入的强耦合，这种光滑子能有效地抑制跳跃误差模式，从而为BR2格式实现鲁棒的多重网格收敛。

### 方法比较：[LDG](@entry_id:751395), BR2, 与HDG

最后，我们将[LDG](@entry_id:751395)和BR2方法置于更广阔的DG方法家族中进行比较，特别是与另一种流行的**可杂交间断Galerkin** (Hybridizable Discontinuous Galerkin, HDG) 方法进行对比。

-   **自由度 (Degrees of Freedom, DoFs)**：
    -   **[LDG](@entry_id:751395)/BR2**：在最直接的实现中，自由度位于单元内部。对于次数为 $k$ 的二维三角元，每个单元有 $O(k^2)$ 个自由度。
    -   **HDG**：其巧妙之处在于，通过引入一个仅定义在网格骨架（所有单元的边界）上的杂化变量，可以将单元内部的自由度通过[静态凝聚](@entry_id:176722)（static condensation）在单元层面消除。最终的全局[线性系统](@entry_id:147850)只涉及这些界面上的自由度。对于二维问题，界面自由度数目为 $O(k)$。因此，当多项式次数 $k$ 较高时（$k \ge 2$），HDG的全局系统规模远小于[LDG](@entry_id:751395)或BR2。

-   **计算成本 (Computational Cost)**：
    -   HDG的优势来自于其较小的全局系统，但这需要付出[静态凝聚](@entry_id:176722)的代价，这是一个在每个单元上求解局部问题的过程，其计算成本随 $k$ 高阶增长（例如 $O(k^6)$）。
    -   对于[非线性](@entry_id:637147)问题，其中系数（如 $\kappa$）依赖于解，每次牛顿迭代都可能需要重新计算和分解[静态凝聚](@entry_id:176722)的局部矩阵，这使得HDG的每次迭代成本非常高。相比之下，BR2或[LDG](@entry_id:751395)的组装过程可能更直接。

-   **[收敛阶](@entry_id:146394) (Convergence Rate)**：
    -   **[LDG](@entry_id:751395)/BR2**：对于光滑解，使用次数为 $k$ 的多项式，通常可以获得 $O(h^{k+1})$ 的 $L^2$ [范数收敛](@entry_id:261322)阶。
    -   **HDG**：其一个显著的优势是，尽管求解的是次数为 $k$ 的逼近，但可以通过一个简单的、单元层面的**后处理** (post-processing) 步骤，构造出一个次数为 $k+1$ 的、具有更高[收敛阶](@entry_id:146394)的解 $u_h^\star$，其 $L^2$ 误差达到 $O(h^{k+2})$。这种“超收敛”性质意味着，为了达到相同的精度 $\varepsilon$，[HDG方法](@entry_id:170956)可以使用更粗的网格或更低的多项式次数，这在许多情况下弥补了其较高的单位成本。

综上所述，没有一种方法是绝对最优的。[LDG](@entry_id:751395)和BR2因其实现相对直接和内在的局部守恒性而受到青睐。HDG则以其小规模的全局系统和超收敛性质在[高精度计算](@entry_id:200567)中脱颖而出。方法的选择应基于具体问题的特性、所需的精度、以及可用的计算资源。