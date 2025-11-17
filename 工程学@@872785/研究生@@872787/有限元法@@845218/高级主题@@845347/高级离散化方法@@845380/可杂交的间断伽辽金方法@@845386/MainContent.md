## 引言
混合可断裂伽辽金（HDG）方法是近年来在计算科学与工程领域备受关注的一类高级有限元方法。它巧妙地结合了连续与[间断伽辽金方法](@entry_id:748369)的优点，以其独特的结构在保证[高阶精度](@entry_id:750325)的同时，显著提升了[计算效率](@entry_id:270255)，尤其是在求解大规模问题时展现出巨大潜力。传统有限元方法在处理复杂物理约束（如不可压缩性）或寻求更高计算效率时常面临挑战。[HDG方法](@entry_id:170956)通过其创新的杂交变量和[静态凝聚](@entry_id:176722)机制，为这些难题提供了一个优雅且强大的解决方案。本文旨在全面系统地介绍[HDG方法](@entry_id:170956)。我们将从其核心理论出发，逐步揭示其工作原理、计算优势及其在不同科学与工程领域的应用。在接下来的章节中，我们将首先深入剖析[HDG方法](@entry_id:170956)的**原理与机制**，详细阐述其公式化、[静态凝聚](@entry_id:176722)过程以及超收敛后处理技术。随后，在**应用与交叉学科联系**一章中，我们将展示该方法如何被应用于解决[流体力学](@entry_id:136788)、固体力学和电磁学等领域的复杂问题。最后，通过一系列精心设计的**动手实践**，读者将有机会将理论知识应用于具体问题，巩固对[HDG方法](@entry_id:170956)核心思想的理解。

## 原理与机制

在上一章中，我们介绍了混合可断裂伽辽金（Hybridizable Discontinuous Galerkin, HDG）方法的基本思想。本章将深入探讨其核心原理与内在机制。我们将从[HDG方法](@entry_id:170956)的基本构造块开始，逐步揭示其公式化、[代数结构](@entry_id:137052)，并最终阐明其独特的计算优势，如[静态凝聚](@entry_id:176722)和超收敛后处理。我们将以标量[扩散](@entry_id:141445)问题作为贯穿全章的模型，以清晰地阐述这些概念。

### 杂交的核心思想：HDG三元组

为了求解一个[偏微分方程](@entry_id:141332)，[HDG方法](@entry_id:170956)的基本策略是将其分解为一系列定义在网格单元上的局部问题，这些局部问题通过定义在单元边界上的全局未知量耦合在一起。我们考虑以下二阶椭圆模型问题的一阶形式，该问题通过引入通量 $\boldsymbol{q} := -\kappa \nabla u$ 得到：
$$
\boldsymbol{q} + \kappa \nabla u = \boldsymbol{0} \quad \text{在 } \Omega \text{ 内}
$$
$$
\nabla \cdot \boldsymbol{q} = f \quad \text{在 } \Omega \text{ 内}
$$

[HDG方法](@entry_id:170956)的核心在于引入了一组离散未知量，通常称为 **HDG三元组** $(u_h, \boldsymbol{q}_h, \widehat{u}_h)$ [@problem_id:2566486]。这三个变量的性质和定义空间是理解此方法的关键。

-   **单元内部未知量 $(u_h, \boldsymbol{q}_h)$**：变量 $u_h$ 和 $\boldsymbol{q}_h$ 分别是标量场 $u$ 和向量通量场 $\boldsymbol{q}$ 在每个网格单元 $K$ 内部的[多项式逼近](@entry_id:137391)。它们被定义在**断裂**的函数空间中，意味着这些函数在单元边界上不要求任何连续性。给定一个非负整数 $k$（多项式次数），这些空间可以精确地定义为 [@problem_id:2566525]：
    $$
    W_h := \{ v \in L^2(\Omega) : v|_K \in \mathcal{P}_k(K), \forall K \in \mathcal{T}_h \}
    $$
    $$
    \boldsymbol{V}_h := \{ \boldsymbol{v} \in [L^2(\Omega)]^d : \boldsymbol{v}|_K \in [\mathcal{P}_k(K)]^d, \forall K \in \mathcal{T}_h \}
    $$
    其中 $\mathcal{P}_k(K)$ 表示在单元 $K$ 上次数最高为 $k$ 的[多项式空间](@entry_id:144410)。因此，离散解 $(u_h, \boldsymbol{q}_h)$ 属于 $\boldsymbol{V}_h \times W_h$。

-   **杂交未知量 $\widehat{u}_h$**：这是[HDG方法](@entry_id:170956)的“杂交”或“混合”成分，也是其名称的由来。$\widehat{u}_h$ 是一个定义在**网格骨架** $\mathcal{F}_h$（即所有网格单元面（faces）的集合）上的新未知量。它在每个内部单元面 $F$ 上是**单值**的，这与标准间断伽辽金（DG）方法中来自相邻单元的双值迹（traces）形成鲜明对比 [@problem_id:2566506]。$\widehat{u}_h$ 的作用是作为精确解 $u$ 在单元边界上的迹的近似，其函数空间为：
    $$
    M_h := \{ \mu \in L^2(\mathcal{F}_h) : \mu|_F \in \mathcal{P}_k(F), \forall F \in \mathcal{F}_h \}
    $$
    从概念上讲，$\widehat{u}_h$ 扮演着一个定义在单元界面上的拉格朗日乘子的角色，它通过一个保守的[通量平衡](@entry_id:637776)条件，[弱形式](@entry_id:142897)地强制实现了单元间的连续性 [@problem_id:2566506]。它像一根“电线”，将原本完全独立的各个单元“焊接”在一起，构成了唯一的全局耦合变量。

值得注意的是，这种将[标量场](@entry_id:151443) $u$ 的迹作为全局耦合未知量的设定，是“原始（primal）HDG”或“混合（mixed）HDG”方法的特征。其他类型的杂交方法可能选择通量相关的量作为界面未知量，但这超出了我们当前的讨论范围 [@problem_id:2566483]。

### 局部问题与全局问题：构建方程体系

[HDG方法](@entry_id:170956)的方程体系分为两个层次：在每个单元上求解的局部问题，以及耦合所有单元的全局问题。

#### 局部问题与[数值通量](@entry_id:752791)

在每个单元 $K \in \mathcal{T}_h$ 上，我们通过对一阶[方程组](@entry_id:193238)进行[弱形式](@entry_id:142897)化来构建局部问题。关键思想是，在求解单元 $K$ 内部的 $(u_h, \boldsymbol{q}_h)$ 时，我们将界面上的杂交变量 $\widehat{u}_h$ 视为已知的边界数据。通过在每个单元 $K$ 上使用[格林公式](@entry_id:173118)，我们会遇到边界积分项，这些项需要对边界上的 $u$ 和 $\boldsymbol{q}\cdot\boldsymbol{n}$ 的值进行定义。在[HDG方法](@entry_id:170956)中，我们用 $\widehat{u}_h$ 替代 $u$ 的迹，并引入一个**[数值通量](@entry_id:752791)** $\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n}$ 来替代真实的法向通量 $\boldsymbol{q} \cdot \boldsymbol{n}$。一个标准的HDG[数值通量](@entry_id:752791)定义如下 [@problem_id:2566505]：
$$
\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n} = \boldsymbol{q}_h \cdot \boldsymbol{n} + \tau (u_h - \widehat{u}_h)
$$
其中，$\tau$ 是一个非负的 **稳定化参数**，它在每个单元面上定义。这个定义是[HDG方法](@entry_id:170956)的核心机制之一。

#### 稳定化参数 $\tau$ 的作用

稳定化参数 $\tau$ 在H[DG格式](@entry_id:178043)中扮演着双重但至关重要的角色：

1.  **相容性 (Consistency)**：一个数值格式必须是相容的，意味着当精确解代入离散方程时，方程应在某种意义下得到满足。对于HDG的数值通量，如果我们代入精确解 $(u, \boldsymbol{q})$，由于精确解是连续的，其在单元边界上的迹 $u|_{\partial K}$ 与杂交变量的精确对应值 $\widehat{u}=u|_{\partial K}$ 相等。因此，稳定化项 $\tau(u_h - \widehat{u}_h)$ 变为 $\tau(u - u) = 0$。这意味着数值通量退化为精确通量，$\widehat{\boldsymbol{q}} \cdot \boldsymbol{n} = \boldsymbol{q} \cdot \boldsymbol{n}$。这一性质对任意有界的 $\tau$ 都成立，保证了格式的相容性 [@problem_id:2566505]。

2.  **稳定性 (Stability)**：稳定性是保证数值方法适定和收敛的基石。在[HDG方法](@entry_id:170956)中，特别是在为 $u_h$ 和 $\boldsymbol{q}_h$ 选择相同阶次的[多项式空间](@entry_id:144410)（这是一种常见且方便的选择）时，若没有稳定化项（即 $\tau=0$），局部问题会变得不稳定或不满足LBB (Ladyzhenskaya-Babuška-Brezzi) 条件。引入 $\tau > 0$ 的稳定化项，在伽辽金方法产生的[双线性形式](@entry_id:746794)中增加了一个正定项 $\sum_K \int_{\partial K} \tau (u_h - \widehat{u}_h)^2 ds$，从而保证了整个系统的矫顽性（coercivity）和稳定性 [@problem_id:2566505]。

为了确保稳定性和最优收敛性，$\tau$ 的取值需要根据网格尺寸 $h$ 和材料系数 $\kappa$ 进行恰当的缩放。通过[量纲分析](@entry_id:140259)和[稳定性分析](@entry_id:144077)可以推断出其正确的缩放关系。物理上，$\tau (u - \widehat{u})$ 必须与通量 $\boldsymbol{q} \cdot \boldsymbol{n}$ 具有相同的量纲。由于 $[\boldsymbol{q}] = [\kappa][\nabla u] = [\kappa][U][L]^{-1}$ 且 $[u] = [U]$，我们得到 $[\tau] = [\kappa][L]^{-1}$。因此，$\tau$ 必须与 $\kappa/h$ 成正比。更严格的稳定性分析也证实了这一点，为了使稳定性常数不依赖于网格尺寸和材料属性，$\tau$ 应按以下方式取值 [@problem_id:2566545]：
$$
\tau_F \simeq C_{\tau} \frac{\kappa_F}{h_F}
$$
其中 $C_{\tau} > 0$ 是一个常数，$h_F$ 是单元面 $F$ 的特征尺寸，$\kappa_F$ 是该面附近的[代表性](@entry_id:204613)[扩散](@entry_id:141445)系数。为了使方法对于多项式次数 $p$ 也是鲁棒的，通常还需要包含一个与 $p$ 相关的因子，如 $\tau_F \simeq C_{\tau} \frac{\kappa_F p^2}{h_F}$。

#### 全局问题

有了局部问题的定义，全局问题就自然而然地产生了。它通过在所有内部单元面上弱形式地强制执行**法向[数值通量](@entry_id:752791)的连续性**来建立。对于共享一个内部面 $F$ 的两个相邻单元 $K^+$ 和 $K^-$，此条件要求：
$$
(\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n})|_{K^+} + (\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n})|_{K^-} = 0 \quad \text{在 } F \text{ 上}
$$
其中[法向量](@entry_id:264185) $\boldsymbol{n}$ 分别指向各自单元的外部。将这个条件对所有面上的检验函数积分并求和，就构成了一个只包含未知量 $\widehat{u}_h$ 的全局[线性方程组](@entry_id:148943)。这个[方程组](@entry_id:193238)的解将唯一确定所有界面上的迹函数，从而将所有独立的局部问题联系在一起。

### [静态凝聚](@entry_id:176722)机制

[HDG方法](@entry_id:170956)最显著的计算优势之一来自于一种称为**[静态凝聚](@entry_id:176722)**（static condensation）的代数过程。这个过程极大地减小了最终需要求解的全局线性系统的规模。

#### 核心思想：局部求解与消除

[静态凝聚](@entry_id:176722)的实现得益于[HDG方法](@entry_id:170956)独特的结构。由于在给定迹变量 $\widehat{u}_h$ 的情况下，每个单元 $K$ 上的局部问题都是完全独立的，不与其他任何单元的内部未知量 $(u_h, \boldsymbol{q}_h)$ 耦合 [@problem_id:2566486] [@problem_id:2566537]。这使得我们可以在代数上将每个单元的内部自由度（即 $u_h|_K$ 和 $\boldsymbol{q}_h|_K$ 对应的系数）表示为该单元边界上迹变量 $\widehat{u}_h|_{\partial K}$ 自由度的线性函数。

这个过程在概念上是：对于每个单元 $K$，我们定义一个局部求解器，该求解器输入边界数据 $\widehat{u}_h|_{\partial K}$，输出内部解 $(u_h|_K, \boldsymbol{q}_h|_K)$。在将这些表达式代入全局通量连续性方程后，所有的单元内部未知量都被**消除**了，最终得到的全局系统只包含界面未知量 $\widehat{u}_h$。

值得将HDG中的[静态凝聚](@entry_id:176722)与标准连续有限元（CFEM）中的[静态凝聚](@entry_id:176722)进行对比 [@problem_id:2566540]。在CFEM中，[静态凝聚](@entry_id:176722)通常用于消除与单元内部（或“气泡”）[基函数](@entry_id:170178)相关的自由度，而与单元边界（即网格骨架）上的节点相关的自由度则被保留下来，形成全局系统。相比之下，HDG的[静态凝聚](@entry_id:176722)更为彻底：它消除了**所有**与单元体积相关的未知量（$u_h$ 和 $\boldsymbol{q}_h$），仅保留了在网格骨架上新引入的杂交变量 $\widehat{u}_h$。

#### [代数结构](@entry_id:137052)与稀疏性

让我们更具体地审视这一过程的代数形式 [@problem_id:2566512]。对于一个单元 $K$，其局部离散方程可以写成如下的矩阵形式，其中 $\boldsymbol{y}_K$ 代表内部自由度（来自 $u_h, \boldsymbol{q}_h$），$\hat{\boldsymbol{u}}_{\partial K}$ 代表其边界上的迹自由度：
$$
\begin{pmatrix}
A_{K}  B_{K} \\
B_{K}^{\top}  D_{K}
\end{pmatrix}
\begin{pmatrix}
\boldsymbol{y}_{K} \\ \hat{\boldsymbol{u}}_{\partial K}
\end{pmatrix}
=
\begin{pmatrix}
\boldsymbol{f}_{K} \\ \boldsymbol{g}_{K}
\end{pmatrix}
$$
通过求解第一个块方程，我们可以得到 $\boldsymbol{y}_{K} = A_{K}^{-1} (\boldsymbol{f}_{K} - B_{K} \hat{\boldsymbol{u}}_{\partial K})$。将此表达式代入第二个块方程，我们得到了一个只涉及迹变量 $\hat{\boldsymbol{u}}_{\partial K}$ 的关系：
$$
(D_{K} - B_{K}^{\top} A_{K}^{-1} B_{K}) \hat{\boldsymbol{u}}_{\partial K} = \boldsymbol{g}_{K} - B_{K}^{\top} A_{K}^{-1} \boldsymbol{f}_{K}
$$
矩阵 $S_K := D_{K} - B_{K}^{\top} A_{K}^{-1} B_{K}$ 被称为单元 $K$ 的**舒尔补（Schur complement）**。全局系统 $S \hat{\boldsymbol{u}} = \boldsymbol{g}$ 正是通过将所有单元的[舒尔补](@entry_id:142780)矩阵 $S_K$ 进行组装（累加）而形成的。

这个最终的全局矩阵 $S$ 具有一个非常重要的稀疏模式。$S$ 中的一个非零块 $S_{F_a, F_b}$ 表示面 $F_a$ 上的自由度与面 $F_b$ 上的自由度之间存在耦合。这种耦合仅当且仅当存在一个单元 $K$ 同时包含 $F_a$ 和 $F_b$ 作为其边界的一部[分时](@entry_id:274419)才会发生。换言之，两个面上的自由度是耦合的，如果它们是“单元相邻”的。

例如，在一个二维三角剖分中，考虑一个与内部面 $F_0$ 相关的自由度。该面被两个三角形 $K_1$ 和 $K_2$ 共享。与 $F_0$ 耦合的所有自由度必须位于 $\partial K_1 \cup \partial K_2$ 上。这个集合总共包含5个不同的面（$F_0$ 本身，以及 $K_1$ 和 $K_2$ 的另外四个面）。如果每个面上有 $m=p+1$ 个自由度（其中 $p$ 是多项式次数），那么全局矩阵 $S$ 中对应于 $F_0$ 上任一自由度的行，其非零项的最大数量为 $5m = 5(p+1)$ [@problem_id:2566512]。这表明全局系统不仅规模小，而且非常稀疏。

### HDG 工作流程与超收敛性

综上所述，一个典型的HDG计算过程包含三个主要阶段：

1.  **组装 (Assembly)**：对每个单元，通过计算其舒尔补矩阵 $S_K$ 和有效右端项，然后将它们组装成全局系统 $S \hat{\boldsymbol{u}} = \boldsymbol{g}$。这个过程是完全并行的。
2.  **全局求解 (Global Solve)**：求解关于迹未知量 $\hat{\boldsymbol{u}}$ 的、规模相对较小的[稀疏线性系统](@entry_id:174902)。
3.  **重构 (Reconstruction)**：一旦获得[全局解](@entry_id:180992) $\widehat{u}_h$，我们回到每个单元，利用已知的 $\widehat{u}_h$ 作为边界条件，求解局部问题以恢复单元内部的解 $(u_h, \boldsymbol{q}_h)$。这个重构步骤也是完全并行的，因为它可以在每个单元上独立执行。

#### 局部重构及其复杂度

局部重构步骤本身涉及在每个单元上求解一个小的线性系统。具体来说，为了从已知的 $\widehat{u}_h$ 计算出 $(u_h, \boldsymbol{q}_h)$，我们需要求解一个形如 $\mathbf{A}_{\mathrm{loc}} \mathbf{X} = \mathbf{b}_{\mathrm{loc}}$ 的方程，其中 $\mathbf{A}_{\mathrm{loc}}$ 是局部系统矩阵，$\mathbf{b}_{\mathrm{loc}}$ 是依赖于 $\widehat{u}_h$ 和[源项](@entry_id:269111) $f$ 的右端向量。如果 $\mathbf{A}_{\mathrm{loc}}$ 的[LU分解](@entry_id:144767)在组装阶段就已经预先计算并存储，那么重构的成本就非常低。每个单元的计算量主要包括一次矩阵-向量乘法（将 $\widehat{u}_h$ 数据并入右端项）和两次三角求解（前代和[回代](@entry_id:146909)）。对于一个 $d$ 维空间中次数为 $k$ 的方法，每个单元的重构计算成本（[浮点运算次数](@entry_id:749457)）可以精确地表示为 $d$ 和 $k$ 的函数，其量级大约为 $O((k+d)^{2d})$ [@problem_id:2566468]。

#### 后处理与超收敛

[HDG方法](@entry_id:170956)最吸引人的特性之一是其解具有**超收敛**（superconvergence）性质。虽然直接计算出的解 $u_h$ 和 $\boldsymbol{q}_h$ 在 $L^2$ 范数下通常以 $\mathcal{O}(h^{k+1})$ 的速率收敛（其中 $h$ 是网格尺寸），但通量近似 $\boldsymbol{q}_h$ 往往表现出比 $u_h$ 更高的精度。[HDG方法](@entry_id:170956)允许我们利用这一高精度的通量信息，通过一个简单的、完全局部的**后处理**（post-processing）步骤，构造一个新的标量场近似 $u_h^\star$，使其在 $L^2$ 范数下达到 $\mathcal{O}(h^{k+2})$ 的收敛阶，即比原始解 $u_h$ 高一阶。

这个后处理过程在每个单元 $K$ 上独立进行，具体步骤如下 [@problem_id:2566489]：
寻找一个更高阶的多项式 $u_h^\star \in \mathcal{P}_{k+1}(K)$，使其满足一个局部的[变分问题](@entry_id:756445)：
$$
(\nabla u_h^\star, \nabla w)_K = (\boldsymbol{q}_h, \nabla w)_K \quad \forall w \in \mathcal{P}_{k+1}(K)
$$
$$
(u_h^\star, 1)_K = (u_h, 1)_K
$$
第一个方程本质上是要求 $u_h^\star$ 的梯度在弱形式下“最佳”地逼近已知的、高精度的数值通量 $\boldsymbol{q}_h$。第二个方程通过保持单元平均值不变来唯一确定 $u_h^\star$。这个过程相当于在每个单元上求解一个以 $\boldsymbol{q}_h$ 为数据源的纯[Neumann问题](@entry_id:176713)。

$u_h^\star$ 之所以能够实现超收敛，其根本原因在于[HDG方法](@entry_id:170956)得到的通量近似 $\boldsymbol{q}_h$ 本身就具有特殊的超收敛性质。通过精巧的数值通量设计，$\boldsymbol{q}_h$ 对精确通量 $\boldsymbol{q}$ 的 $L^2$ 误差可以达到最优的 $\mathcal{O}(h^{k+1})$ 阶。后处理步骤有效地将这一高精度信息“转移”到了新的标量近似 $u_h^\star$ 上。通过应用对偶性论证（Aubin-Nitsche技巧）的变体，可以严格证明，在适当的正则性假设下，最终得到的后处理解满足 $\|u - u_h^\star\|_{0,\Omega} = \mathcal{O}(h^{k+2})$ [@problem_id:2566489]。

这种通过廉价的局部计算来提升[全局解](@entry_id:180992)精度的能力，是[HDG方法](@entry_id:170956)在科学与工程计算中备受青睐的关键原因之一。