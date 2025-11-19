## 引言
在求解[偏微分方程的数值方法](@entry_id:143514)中，间断伽辽金（DG）方法因其灵活性和局部守恒性而备受青睐，但其代价是产生了包含大量自由度的全局耦合系统，带来了巨大的计算挑战。为了解决这一核心问题，可杂交间断伽辽金（HDG）方法应运而生，它通过一种创新的代数技巧——[静态凝聚](@entry_id:176722)，在保持DG方法优点的同时，显著提升了[计算效率](@entry_id:270255)。本文旨在系统性地剖析[HDG方法](@entry_id:170956)的理论框架及其应用。

我们将分步展开探讨。在第一章“原理与机制”中，我们将从第一性原理出发，详细推导HDG的原始与混合形式，并揭示[静态凝聚](@entry_id:176722)如何将庞大的全局问题转化为一个仅涉及网格边界自由度的小型系统。随后的“应用与跨学科连接”一章将展示[HDG方法](@entry_id:170956)在[流体力学](@entry_id:136788)、波传播等领域的强大应用，并阐明其与[对称内部罚](@entry_id:755719)分法（SIPG）、[区域分解](@entry_id:165934)等其他重要数值[范式](@entry_id:161181)的深刻联系。最后，一系列实践练习将帮助读者巩固所学知识。

通过本文的学习，读者将不仅掌握一种先进的数值方法，更将深入理解其背后的数学结构和计算思想。让我们首先进入[HDG方法](@entry_id:170956)的核心，探究其精妙的原理与机制。

## 原理与机制

本章旨在深入阐述可杂交间断伽辽金（Hybridizable Discontinuous Galerkin, HDG）方法的核心原理与运作机制。与前一章的介绍性概述不同，本章将从第一性原理出发，系统地剖析[HDG方法](@entry_id:170956)的原始（primal）与混合（mixed）形式，并详细解释其关键优势——[静态凝聚](@entry_id:176722)（static condensation）的实现方式及其带来的[计算效率](@entry_id:270255)提升。我们将通过一系列推导和实例，揭示该方法在[代数结构](@entry_id:137052)、计算实现和理论性质等方面的精妙之处。

### 杂交原理：分解全局问题

传统有限元方法的核心挑战之一在于，求解过程中产生的全局线性系统规模庞大，其中所有自由度（degrees of freedom, DOFs）相互耦合。间断伽辽金（Discontinuous Galerkin, DG）方法通过允许单元间的解不连续，获得了更高的灵活性和局部性，但其代价是自由度数量的增加，因为每个单元的自由度都需要参与全局耦合。

**可杂交（Hybridizable）**思想为此提供了一种创新的解决方案。其核心在于引入一个新的未知量，即定义在网格骨架（所有单元面（face）的集合）上的**迹（trace）**，我们称之为**杂交迹（hybrid trace）**，记作 $\widehat{u}_h$。这个迹变量的作用是充当相邻单元间的“粘合剂”。单元内部的未知量（如解 $u_h$ 或其通量 $\boldsymbol{q}_h$）不再直接与相邻单元的内部未知量耦合，而是仅与自身所在单元边界上的迹变量 $\widehat{u}_h$ 耦合。

通过这种方式，原始的全局耦合问题被分解为两个层次：
1.  一系列完全独立的**局部问题**：在每个单元 $K$ 上，给定边界上的迹 $\widehat{u}_h|_{\partial K}$ 作为边界条件，求解单元内部的未知量。
2.  一个耦合自由度大幅减少的**全局问题**：通过在单元交界面上强制施加某种形式的连续性条件（通常是数值通量的连续性），建立一个只涉及全局迹变量 $\widehat{u}_h$ 的[方程组](@entry_id:193238)。

这种结构与标准的DG方法形成鲜明对比。在标准DG方法中，单元自由度通过单元面上的积分直接与相邻单元的自由度耦合，导致所有单元自由度都进入最终的全局[线性系统](@entry_id:147850)。而HDG通过引入独立的迹变量 $\widehat{u}_h$ 作为唯一的全局耦合媒介，为后续的[静态凝聚](@entry_id:176722)技术铺平了道路，这是[HDG方法](@entry_id:170956)计算效率优势的根源 [@problem_id:3410450]。

### HDG公式：原始形式与混合形式

对于一个典型的[二阶椭圆问题](@entry_id:754613)，例如泊松方程 $-\nabla \cdot (\kappa \nabla u) = f$，[HDG方法](@entry_id:170956)可以基于其二阶（原始）形式或一阶（混合）形式来构建。

#### 混合HDG公式

混合方法首先引入一个辅助变量，即通量 $\boldsymbol{q} = -\kappa \nabla u$，将原问题转化为一个[一阶系统](@entry_id:147467)：
$$
\kappa^{-1} \boldsymbol{q} + \nabla u = \boldsymbol{0}
$$
$$
\nabla \cdot \boldsymbol{q} = f
$$
在混合HDG框架下，我们在每个单元 $K$ 内部逼近解 $u_h$ 和通量 $\boldsymbol{q}_h$，同时在网格骨架上逼近杂交迹 $\widehat{u}_h$。

局部[弱形式](@entry_id:142897)在每个单元 $K$ 上建立。对于所有适当的检验函数 $\boldsymbol{r}$ 和 $v$，我们要求：
$$
\int_K \kappa^{-1} \boldsymbol{q}_h \cdot \boldsymbol{r} \, \mathrm{d}\boldsymbol{x} - \int_K u_h (\nabla \cdot \boldsymbol{r}) \, \mathrm{d}\boldsymbol{x} + \int_{\partial K} \widehat{u}_h (\boldsymbol{r} \cdot \boldsymbol{n}) \, \mathrm{d}s = 0
$$
$$
- \int_K \boldsymbol{q}_h \cdot \nabla v \, \mathrm{d}\boldsymbol{x} + \int_{\partial K} (\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n}) v \, \mathrm{d}s = \int_K f v \, \mathrm{d}\boldsymbol{x}
$$
其中 $\boldsymbol{n}$ 是单元边界 $\partial K$ 上的单位外法向向量。请注意，所有边界积分项都由杂交迹 $\widehat{u}_h$ 或**数值通量（numerical flux）** $\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n}$ 代替。[数值通量](@entry_id:752791)是[HDG方法](@entry_id:170956)的核心构件，它将单元内部的解 $(u_h, \boldsymbol{q}_h)$ 与迹 $\widehat{u}_h$ 联系起来，并引入稳定性。一个典型的定义是：
$$
\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n} := \boldsymbol{q}_h \cdot \boldsymbol{n} + \tau (u_h - \widehat{u}_h)
$$
这里的 $\tau > 0$ 是一个**稳定化参数**，它惩罚了单元内部解的迹 $u_h|_{\partial K}$ 与杂交迹 $\widehat{u}_h$ 之间的偏差，从而保证了方法的稳定性和收敛性 [@problem_id:3410450]。

全局耦合方程通过在每个内部单元面 $F$ 上强制执行数值通量的连续性来得到：
$$
\int_F ((\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n})|_{K_1} + (\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n})|_{K_2}) \, \mu \, \mathrm{d}s = 0
$$
对于所有定义在 $F$ 上的迹[检验函数](@entry_id:166589) $\mu$ 成立，其中 $K_1$ 和 $K_2$ 是共享面 $F$ 的两个相邻单元。

#### 原始HDG公式

原始[HDG方法](@entry_id:170956)直接从二阶方程 $-\nabla \cdot (\kappa \nabla u) = f$ 出发。在每个单元 $K$ 上，我们只逼近解 $u_h$，同时在网格骨架上定义杂交迹 $\widehat{u}_h$。

通过在单元 $K$ 上对二阶方程进行分部积分，我们得到局部[弱形式](@entry_id:142897)：
$$
\int_K \kappa \nabla u_h \cdot \nabla v \, \mathrm{d}\boldsymbol{x} - \int_{\partial K} (\kappa \nabla u_h \cdot \boldsymbol{n}) v \, \mathrm{d}s = \int_K f v \, \mathrm{d}\boldsymbol{x}
$$
同样，边界上的物理通量项 $\kappa \nabla u_h \cdot \boldsymbol{n}$ 被一个数值通量所取代。在原始形式中，这个[数值通量](@entry_id:752791)通常定义为：
$$
\widehat{\boldsymbol{\sigma}}_h \cdot \boldsymbol{n} := -\kappa \nabla u_h \cdot \boldsymbol{n} + \tau (u_h - \widehat{u}_h)
$$
代入[弱形式](@entry_id:142897)后，得到依赖于 $\widehat{u}_h$ 的局部方程。全局耦合方程与混合形式类似，同样通过强制数值通量的跨单元连续性来建立 [@problem_id:3410450]。

### [静态凝聚](@entry_id:176722)：效率的引擎

[静态凝聚](@entry_id:176722)是[HDG方法](@entry_id:170956)区别于其他[DG方法](@entry_id:748369)的最显著特征，它极大地提升了计算效率。其本质是利用[HDG方法](@entry_id:170956)的两层结构，在形成全局系统之前，通过代数操作将所有单元内部的自由度局部地消除。

#### 代数机制

让我们以混合HDG为例，来考察[静态凝聚](@entry_id:176722)的代数过程。在给定迹变量 $\widehat{\boldsymbol{u}}$ （表示 $\widehat{u}_h$ 的系数向量）的情况下，每个单元 $K$ 上的局部[弱形式](@entry_id:142897)可以写成一个关于内部未知量系数向量 $\boldsymbol{x} = \begin{pmatrix} \boldsymbol{q} \\ \boldsymbol{u} \end{pmatrix}$ 的线性系统。这个系统可以清晰地表示为如下的块结构形式 [@problem_id:3410462]：
$$
K \boldsymbol{x} + R \widehat{\boldsymbol{u}} = \boldsymbol{b}
$$
这里，$K$ 是一个[块矩阵](@entry_id:148435)，包含了单元内部未知量之间的相互作用（例如质量矩阵和梯度-散度[耦合矩阵](@entry_id:191757)）；$R$ 是[耦合矩阵](@entry_id:191757)，描述了迹变量 $\widehat{\boldsymbol{u}}$ 对内部问题的影响；$\boldsymbol{b}$ 是由[源项](@entry_id:269111) $f$ 产生的[载荷向量](@entry_id:635284)。

同时，单元边界上的[数值通量](@entry_id:752791)（其系数向量记为 $\boldsymbol{h}$）也可以表示为内部未知量和迹未知量的线性组合：
$$
\boldsymbol{h} = W \boldsymbol{x} + S \widehat{\boldsymbol{u}}
$$
由于局部问题是良定的（要求 $K$ 可逆），我们可以从第一个方程中形式上解出 $\boldsymbol{x}$：
$$
\boldsymbol{x} = K^{-1}(\boldsymbol{b} - R \widehat{\boldsymbol{u}})
$$
将这个表达式代入第二个方程，我们就消除了内部未知量 $\boldsymbol{x}$，得到了一个只涉及迹变量 $\widehat{\boldsymbol{u}}$ 和其对应通量 $\boldsymbol{h}$ 的关系：
$$
\boldsymbol{h} = W K^{-1}(\boldsymbol{b} - R \widehat{\boldsymbol{u}}) + S \widehat{\boldsymbol{u}} = (S - W K^{-1} R) \widehat{\boldsymbol{u}} + W K^{-1} \boldsymbol{b}
$$
矩阵 $\boldsymbol{S}_{sc} = S - W K^{-1} R$ 被称为**舒尔补（Schur complement）**。它构成了单元 $K$ 对全局系统的贡献。全局系统就是通过将所有单元的[舒尔补](@entry_id:142780)矩阵 $\boldsymbol{S}_{sc}$ 组装起来，并施加通量连续性条件（$\sum \boldsymbol{h} = 0$）而形成的。

#### 一个具体的例子：一维[舒尔补](@entry_id:142780)的物理解释

为了更直观地理解[舒尔补](@entry_id:142780)的含义，我们考虑一个一维[泊松方程](@entry_id:143763)的原始H[DG离散化](@entry_id:748366)。在一个长度为 $h$ 的单元 $K=(0,h)$上，使用线性[基函数](@entry_id:170178)。通过直接计算，可以推导出连接该单元两个端点迹值 $(\widehat{u}_0, \widehat{u}_h)$ 与其对应[数值通量](@entry_id:752791) $(r_0, r_h)$ 的舒尔补矩阵 [@problem_id:3410473]。在某种特定的HDG公式下，这个 $2 \times 2$ 的[舒尔补](@entry_id:142780)矩阵 $S$ 具有一个非常简洁和富有启发性的形式：
$$
S = \frac{1}{h} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}
$$
这个矩阵正是描述连接两个节点、电阻为 $h$ 的电路（或刚度为 $1/h$ 的弹簧）的刚度矩阵。它是一个[图拉普拉斯算子](@entry_id:275190)。这揭示了[舒尔补](@entry_id:142780)的物理本质：它是一个离散的**狄利克雷-诺伊曼（Dirichlet-to-Neumann, DtN）映射**，即给定单元边界上的“位移”（迹值 $\widehat{u}$），它能计算出维持该位移所需的“力”（通量 $r$）。[静态凝聚](@entry_id:176722)的过程，本质上就是计算出每个单元的等效刚度，然后像组装电路或桁架一样将它们组装成一个全局系统。

#### 计算优势与实现考量

[静态凝聚](@entry_id:176722)带来的计算优势是多方面的：
1.  **减小系统规模**：最终求解的全局[线性系统](@entry_id:147850)只包含网格骨架上的迹自由度，其数量远少于所有单元内部的自由度总和。这极大地节省了内存和求解时间。
2.  **并行性**：[舒尔补](@entry_id:142780)的计算（包括 $K^{-1}$ 的计算和[矩阵乘法](@entry_id:156035)）是完全局限在每个单元内部的，因此可以在所有单元上完美地并行执行。
3.  **结构一致性**：[静态凝聚](@entry_id:176722)过程只依赖于单元内部的代数消元，而最终全局系统的稀疏模式仅由网格的拓扑结构决定（即哪些单元共享一个面）。因此，对于相同的网格和迹函数空间，无论是采用原始形式还是混合形式，其最终的全局稀疏矩阵具有完全相同的结构和带宽 [@problem_id:3410516]。不同之处仅在于矩阵块内数值的差异。

为了高效地实现[静态凝聚](@entry_id:176722)，特别是 $K^{-1}$ 的计算，单元内部[基函数](@entry_id:170178)的选择至关重要。如果选用**模态正交基**（如[勒让德多项式](@entry_id:141510)），在仿射单元上，[质量矩阵](@entry_id:177093)将是对角阵（甚至是单位矩阵的倍数）。这使得包含质量矩阵的局部[块矩阵](@entry_id:148435) $K$ 的求逆过程变得非常简单和数值稳定。相反，如果使用标准的**[节点基](@entry_id:752522)**（如[拉格朗日基](@entry_id:751105)函数），[质量矩阵](@entry_id:177093)将是稠密的且随着多项式次数的增加而变得病态，这会增加局部求逆的计算成本和[数值误差](@entry_id:635587) [@problem_id:3410506]。

### 高级性质与特征

[HDG方法](@entry_id:170956)不仅在计算上高效，还在理论上具备许多优良性质。

#### 凝聚系统的性质

对于自伴随的[椭圆问题](@entry_id:146817)（例如 $\kappa$ 是对称正定张量），[HDG方法](@entry_id:170956)经过精心设计可以继承其优良的数学结构。无论是原始HDG还是混合HDG，其最终形成的全局凝聚系统都是**[对称正定](@entry_id:145886)（Symmetric Positive Definite, SPD）**的 [@problem_id:3410492]。这是一个非常理想的性质，因为它保证了全局系统[解的存在唯一性](@entry_id:177406)，并且可以使用最高效的[线性求解器](@entry_id:751329)（如[共轭梯度法](@entry_id:143436)）。

有趣的是，在混合HDG中，尽管局部系统 $K$ 是一个不定（[鞍点](@entry_id:142576)）的[块矩阵](@entry_id:148435)，但其舒尔补 $\boldsymbol{S}_{sc}$ 最终却能恢复正定性。这是HDG理论中一个深刻且重要的结果。

然而，当[HDG方法](@entry_id:170956)用于求解[特征值问题](@entry_id:142153)时，[静态凝聚](@entry_id:176722)过程可能会引入**伪特征模态（spurious eigenmodes）**。这些伪模态是纯粹的数值产物，不对应于真实的物理[特征模](@entry_id:174677)态。其根源在于，对于某些特定的[特征值](@entry_id:154894) $\lambda_h$，局部算子 $\mathcal{A}_K(\lambda_h)$ 可能会变得奇异，导致[静态凝聚](@entry_id:176722)的前提（局部可解性）被破坏。因此，在求解完凝聚系统的[特征值](@entry_id:154894)后，必须进行后处理检验：对于每个计算出的特征对 $(\lambda_h, \widehat{u}_h)$，必须检查其在每个单元上的局部重构问题是否都是良定的。如果存在任何一个单元上的重构问题是奇异的，则该[特征模](@entry_id:174677)态就是伪模态，必须被剔除 [@problem_id:3410469]。

#### 超收敛与局部后处理

[HDG方法](@entry_id:170956)最引人注目的理论优势之一是其**超收敛（superconvergence）**性质。对于许多[椭圆问题](@entry_id:146817)，可以证明[HDG方法](@entry_id:170956)计算出的数值通量 $\boldsymbol{q}_h$ 的[收敛阶](@entry_id:146394)比从 $u_h$ 中直接计算梯度所预期的要高一阶。例如，当使用 $k$ 次多项式时，通量 $\boldsymbol{q}_h$ 在 $L^2$ 范数下可以达到 $h^{k+1}$ 的[收敛阶](@entry_id:146394)。

这一性质可以通过**局部后处理（local post-processing）**技术来充分利用，从而获得一个更高精度的解。具体步骤如下 [@problem_id:3410486] [@problem_id:3410513]：
1.  首先，通过标准的[HDG方法](@entry_id:170956)求解得到 $(u_h, \boldsymbol{q}_h, \widehat{u}_h)$。
2.  然后，在每个单元 $K$ 上，定义一个新的、更高一阶（$k+1$ 次）的解 $u_h^\star \in \mathcal{P}_{k+1}(K)$。
3.  这个后处理的解 $u_h^\star$ 通过求解一个局部的[变分问题](@entry_id:756445)来确定，其核心条件是要求 $\nabla u_h^\star$ 在 $L^2$ 意义下最佳地逼近超收敛的通量 $-\kappa^{-1}\boldsymbol{q}_h$。同时，通常会施加一个均值守恒的约束条件，如 $\int_K u_h^\star = \int_K u_h$。

由于后处理的误差主要由 $\boldsymbol{q}_h$ 的超收敛误差（$O(h^{k+1})$）所控制，通过应用一个对偶参数（Aubin-Nitsche duality argument），可以证明后处理解 $u_h^\star$ 在 $L^2$ 范数下的[收敛阶](@entry_id:146394)能够再提升一阶，达到惊人的 $h^{k+2}$。

值得注意的是，这种 $O(h^{k+2})$ 的超收敛性质并非对所有HDG公式都成立。它依赖于所选[离散空间](@entry_id:155685)之间精妙的[代数结构](@entry_id:137052)，这种结构通常被称为**$\mathcal{M}$-分解**。某些[混合HDG方法](@entry_id:752023)的特定多项式空间组合（例如，通量、解和迹均使用 $k$ 次多项式）恰好具备这种结构，从而可以实现后处理的完全超收敛。然而，许多其他公式，包括一些原始[HDG方法](@entry_id:170956)，可能不具备此结构，导致其通量收敛阶较低，后处理也只能达到 $O(h^{k+1})$ 的[收敛阶](@entry_id:146394) [@problem_id:3410513]。这凸显了在设计[HDG方法](@entry_id:170956)时，对离散空间选择的深刻理论考量。