## 引言
在[数值求解偏微分方程](@entry_id:634353)的领域，间断Galerkin (DG)方法因其[高阶精度](@entry_id:750325)、局部守恒性和处理复杂几何的灵活性而备受青睐。然而，[基函数](@entry_id:170178)的选择对[DG格式](@entry_id:178043)的性能、稳定性和实现复杂度有着深远影响。传统[正交基](@entry_id:264024)虽然简化了质量矩阵的求逆，却常常导致微分算子稠密，并且难以直接保证解的物理约束（如密度和压力的非负性），这在高[马赫数](@entry_id:274014)[流体模拟](@entry_id:138114)等领域是一个关键的知识空白和技术挑战。

本文旨在深入探讨一种替代方案——使用[Bernstein多项式基](@entry_id:746761)进行[DG离散化](@entry_id:748366)。这种[基函数](@entry_id:170178)源于计算机辅助几何设计，其独特的几何与代数性质为克服上述挑战提供了优雅而强大的工具。

通过本文，读者将系统地学习到：在“原则与机制”章节中，我们将剖析[Bernstein基](@entry_id:164098)的定义、优良性质，并构建其在[DG方法](@entry_id:748369)中的核心算子，揭示其与正交基的根本计算权衡。接着，在“应用与跨学科连接”章节，我们将展示这些理论如何转化为解决计算流体动力学、不确定性量化和图像处理等领域实际问题的稳健算法。最后，“动手实践”部分将提供具体的编程练习，帮助读者将理论知识付诸实践。

## 原则与机制

本章深入探讨了在间断Galerkin (DG)方法的离散化中使用[Bernstein多项式基](@entry_id:746761)的核心原理与关键机制。我们将从[Bernstein多项式](@entry_id:146090)的基本定义出发，逐步构建在单纯形单元上进行DG计算所需的算子，并最终分析其相对于标准正交基的计算特性与优势。

### [Bernstein多项式](@entry_id:146090)：定义与基本性质

理解[Bernstein基](@entry_id:164098)的第一步是掌握其在一维参考区间 $[0,1]$ 上的定义。对于一个给定的非负整数次数 $n$，次数为 $n$ 的**[Bernstein多项式](@entry_id:146090) (Bernstein polynomial)** 基由 $n+1$ 个函数构成，定义如下：
$$
B_i^n(x) = \binom{n}{i} x^i (1-x)^{n-i}, \quad \text{其中 } i = 0, 1, \dots, n
$$
这些[基函数](@entry_id:170178)构成了 $[0,1]$ 上次数不超过 $n$ 的[多项式空间](@entry_id:144410) $\mathbb{P}^n$ 的一组基。它们具有若干优良的性质，例如**非负性** ($B_i^n(x) \ge 0$ for $x \in [0,1]$)、**[单位分解](@entry_id:150115)性** ($\sum_{i=0}^n B_i^n(x) = 1$)，以及在区间端点处的**插值性质** ($B_i^n(0) = \delta_{i0}$ 和 $B_i^n(1) = \delta_{in}$)。这些性质使得[Bernstein多项式](@entry_id:146090)在几何造型和[计算机辅助设计](@entry_id:157566)领域中扮演着核心角色，同时也为它们在数值方法中的应用带来了独特的优势。

在[DG方法](@entry_id:748369)中，一个核心操作是在不同的多项式基之间进行转换。例如，我们可能需要将一个以[Bernstein基](@entry_id:164098)表示的多项式转换到更常见的**单项式基 (monomial basis)** $\{x^k\}_{k=0}^n$。任何一个多项式 $u(x) \in \mathbb{P}^n$ 都可以表示为这两种基的[线性组合](@entry_id:154743)：
$$
u(x) = \sum_{i=0}^n b_i B_i^n(x) = \sum_{k=0}^n a_k x^k
$$
其中 $b_i$ 是Bernstein系数，$a_k$ 是单项式系数。我们可以推导出这两个系数向量之间的[线性变换矩阵](@entry_id:186379)。通过对 $(1-x)^{n-i}$ 进行[二项式展开](@entry_id:269603)，我们可以将每个[Bernstein基](@entry_id:164098)函数表示为单项式的[线性组合](@entry_id:154743) ：
$$
B_i^n(x) = \sum_{k=i}^{n} (-1)^{k-i} \binom{n}{k} \binom{k}{i} x^k
$$
通过这个表达式，我们可以得到从Bernstein系数向量 $\boldsymbol{b}$ 到单项式系数向量 $\boldsymbol{a}$ 的[变换矩阵](@entry_id:151616) $T_{B\to P}^{(n)}$。同样，我们也可以找到其逆变换 $T_{P\to B}^{(n)}$。这两个[变换矩阵](@entry_id:151616)都是下[三角矩阵](@entry_id:636278)，其对角线元素均为非零，因此它们总是可逆的，保证了[基变换](@entry_id:189626)的唯一性和稳定性。

例如，对于 $n=2$ 的情况，从单项式基到[Bernstein基](@entry_id:164098)的变换矩阵为 ：
$$
T_{P\to B}^{(2)} = \begin{pmatrix} 1  0  0 \\ 1  \frac{1}{2}  0 \\ 1  1  1 \end{pmatrix}
$$
利用这个矩阵，我们可以将一个在单项式基中给出的多项式，如 $u(x) = 1+2x+3x^2$（其系数向量为 $\boldsymbol{a} = (1, 2, 3)^T$），转换为其在[Bernstein基](@entry_id:164098)下的表示。其Bernstein系数向量 $\boldsymbol{b}$ 计算如下：
$$
\boldsymbol{b} = T_{P\to B}^{(2)} \boldsymbol{a} = \begin{pmatrix} 1  0  0 \\ 1  \frac{1}{2}  0 \\ 1  1  1 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \\ 3 \end{pmatrix} = \begin{pmatrix} 1 \\ 2 \\ 6 \end{pmatrix}
$$
这意味着 $u(x) = 1 \cdot B_0^2(x) + 2 \cdot B_1^2(x) + 6 \cdot B_2^2(x)$。这种在不同基之间进行精确转换的能力是数值算法实现中的一项基本要求。

### 高维单纯形上的[Bernstein基](@entry_id:164098)

[DG方法](@entry_id:748369)通常在更复杂的几何形状（如三角形或四面体）上进行，这需要我们将[Bernstein基](@entry_id:164098)的定义推广到高维**单纯形 (simplex)** 上。在一个 $d$ 维单纯形 $K$ 上，任何一点的位置可以由其 $d+1$ 个**[重心坐标](@entry_id:155488) (barycentric coordinates)** $\lambda = (\lambda_1, \dots, \lambda_{d+1})$ 唯一确定，这些坐标满足 $\lambda_i \ge 0$ 且 $\sum_{i=1}^{d+1} \lambda_i = 1$。

次数为 $n$ 的[Bernstein基](@entry_id:164098)函数由一个多重指标 $\alpha = (\alpha_1, \dots, \alpha_{d+1})$ 来索引，其中 $\alpha_i$ 是非负整数且 $\sum \alpha_i = n$。其定义为：
$$
B_{\alpha}^{n}(\lambda) = \frac{n!}{\alpha_{1}!\,\alpha_{2}!\,\cdots\,\alpha_{d+1}!} \prod_{i=1}^{d+1} \lambda_{i}^{\alpha_{i}} = \binom{n}{\alpha} \lambda^\alpha
$$
在二维情况（三角形）下，多重指标为 $\alpha = (\alpha_1, \alpha_2, \alpha_3)$ 且 $\alpha_1+\alpha_2+\alpha_3=n$。与一维情况类似，这些[基函数](@entry_id:170178)构成了三角形上次数不超过 $n$ 的多项式空间 $\mathcal{P}_n(T)$ 的一组基。

在DG方法的某些高级构造中，我们可能需要将多项式从一个**分层[模态基](@entry_id:752055) (hierarchical modal basis)**（例如，由[重心坐标](@entry_id:155488)的单项式 $\lambda^\alpha$ 构成）转换到[Bernstein基](@entry_id:164098)。一个重要的观察是，如果我们将[多项式空间](@entry_id:144410)按[齐次多项式](@entry_id:178156)的次数进行分解，那么在每个固定的齐次次数 $m$ 的[子空间](@entry_id:150286)内，从[模态基](@entry_id:752055)到[Bernstein基](@entry_id:164098)的转换变得非常简单 。一个次数为 $m$ 的齐次[模态基](@entry_id:752055)函数 $\lambda^\alpha$ (其中 $|\alpha|=m$) 可以直接表示为相应[Bernstein基](@entry_id:164098)函数 $B_\alpha^m$ 的倍数：
$$
\lambda^\alpha = \frac{1}{\binom{m}{\alpha}} B_\alpha^m(\lambda)
$$
这意味着，对于一个固定的齐次次数 $m$，从[模态系数](@entry_id:752057)到Bernstein系数的变换矩阵是一个**对角矩阵**，其对角[线元](@entry_id:196833)素为 $1/\binom{m}{\alpha}$。

这个简单的对角关系引出了一个关于变换稳定性的重要问题。整个 $\mathcal{P}_p(T)$ 空间上的模态-Bernstein变换矩阵是一个[块对角矩阵](@entry_id:145530)，其对角线上的元素汇集了从 $m=0$ 到 $p$ 的所有 $1/\binom{m}{\alpha}$。该变换的**[条件数](@entry_id:145150) (condition number)**，即其最大[奇异值](@entry_id:152907)与最小奇异值之比，决定了变换在数值上的稳定性。由于变换矩阵是对角阵，其奇异值就是对角元素本身。因此，[条件数](@entry_id:145150)等于 $\binom{m}{\alpha}$ 的最大值与最小值之比 。
$$
\kappa(p) = \frac{\max_{0 \le m \le p, |\alpha|=m} \binom{m}{\alpha}}{\min_{0 \le m \le p, |\alpha|=m} \binom{m}{\alpha}}
$$
[多项式系数](@entry_id:262287) $\binom{m}{\alpha}$ 的最小值在索引单纯形的顶点处取得（例如 $\alpha = (m, 0, \dots, 0)$），其值为 $1$。其最大值在最高次数 $m=p$ 且当 $p$ 被尽可能均匀地分配给 $\alpha_i$ 时取得。对于三角形（$d=2$），这个最大值由中心[多项式系数](@entry_id:262287)给出。因此，[条件数](@entry_id:145150)可以精确计算为：
$$
\kappa(p) = \frac{p!}{(\lfloor \frac{p}{3} \rfloor)! (\lfloor \frac{p+1}{3} \rfloor)! (\lfloor \frac{p+2}{3} \rfloor)!}
$$
这个结果表明，随着多项式次数 $p$ 的增加，该变换的[条件数](@entry_id:145150)会迅速增长，这意味着在高阶离散中，数值稳定性成为一个需要关注的问题。

### [微分与积分](@entry_id:141565)算子

在DG方法中[求解偏微分方程](@entry_id:138485)，核心在于如何有效地计算[基函数](@entry_id:170178)及其导数的积分。[Bernstein基](@entry_id:164098)在这些运算中展现出独特的结构。

#### 微分算子

[Bernstein基](@entry_id:164098)最显著的优点之一是其简洁的[微分性质](@entry_id:275298)。一个次数为 $n$ 的[Bernstein基](@entry_id:164098)函数的梯度可以精确地表示为三个次数为 $n-1$ 的[Bernstein基](@entry_id:164098)函数的线性组合。在三角形上，该恒等式为  ：
$$
\nabla B_{\alpha}^{n} = n \sum_{j=1}^{3} B_{\alpha-\boldsymbol{e}_{j}}^{n-1} \nabla\lambda_{j}
$$
其中 $\boldsymbol{e}_{j}$ 是三维[标准基向量](@entry_id:152417)（例如 $\boldsymbol{e}_1=(1,0,0)$），$\nabla\lambda_{j}$ 是第 $j$ 个[重心坐标](@entry_id:155488)的梯度。由于[重心坐标](@entry_id:155488)是[仿射函数](@entry_id:635019)，它们的梯度 $\nabla\lambda_{j}$ 在整个单元上是常向量。

这个公式的意义深远：它将一个[微分](@entry_id:158718)运算转换为了一个代数运算（降低多重指标）和一个次数降低的操作。这使得涉及导数的计算变得异常高效和结构化，因为微分[算子的矩阵表示](@entry_id:153664)将是**稀疏的 (sparse)**，每行最多只有三个非零项。

#### 质量矩阵与积分

DG方法中的**质量矩阵 (mass matrix)** 定义为[基函数](@entry_id:170178)之间的 $L^2$ [内积](@entry_id:158127)：
$$
M_{\alpha\beta} = \int_K B^{(n)}_{\alpha}(x) B^{(n)}_{\beta}(x) \,\mathrm{d}x
$$
为了计算这个积分，我们需要计算两个[Bernstein基](@entry_id:164098)函[数乘](@entry_id:155971)积的积分。这个乘积 $B^{(n)}_{\alpha} B^{(n)}_{\beta}$ 是一个次数为 $2n$ 的多项式。因此，为了精确计算所有[质量矩阵](@entry_id:177093)的元素，我们需要一个**[数值积分法则](@entry_id:175061) (quadrature rule)**，其精度至少要能精确积分所有次数不超过 $2n$ 的多项式 。

与[基函数](@entry_id:170178)非负且相互重叠的性质相对应，[Bernstein基](@entry_id:164098)的[质量矩阵](@entry_id:177093)通常是**稠密的 (dense)**，即几乎所有非对角元素都不为零。这是与正交基（其质量矩阵是对角阵）的一个关键区别。此外，随着多项式次数 $n$ 的增加，[Bernstein基](@entry_id:164098)函数之间的线性相关性增强，导致质量[矩阵的条件数](@entry_id:150947)快速增长，即矩阵变得**病态 (ill-conditioned)**。数值实验证实了这种增长趋势，这对[求解线性系统](@entry_id:146035)提出了挑战 。

#### [刚度矩阵](@entry_id:178659)

对于包含[二阶导数](@entry_id:144508)（如[扩散](@entry_id:141445)项）的问题，我们需要计算**刚度矩阵 (stiffness matrix)**：
$$
A_{\alpha\beta} = \int_{K} \nabla B_{\alpha}^{n}(x) \cdot \nabla B_{\beta}^{n}(x)\,\mathrm{d}x
$$
利用前面提到的梯度恒等式，我们可以将刚度矩阵的计算与低一阶的质量型积分联系起来 ：
$$
A_{\alpha\beta} = n^{2} \sum_{i=1}^{3}\sum_{j=1}^{3} (\nabla\lambda_{i}\cdot\nabla\lambda_{j}) \int_{K} B_{\alpha-\boldsymbol{e}_{i}}^{n-1}(x) B_{\beta-\boldsymbol{e}_{j}}^{n-1}(x)\,\mathrm{d}x
$$
这个表达式揭示了[刚度矩阵](@entry_id:178659)的美妙结构：它由两部分组成——一部分是与单元几何形状相关的常数因子 $(\nabla\lambda_{i}\cdot\nabla\lambda_{j})$，另一部分是次数为 $n-1$ 的[基函数](@entry_id:170178)乘积的积分（即一个低阶质量矩阵的元素）。例如，对于 $n=1$ 的线性元，刚度矩阵的计算可以直接简化为几何量的组合 。这个结构使得[刚度矩阵](@entry_id:178659)的组装过程高度结构化，并且可以利用[微分算子](@entry_id:140145)的[稀疏性](@entry_id:136793)来设计高效算法 。

### 在[DG方法](@entry_id:748369)中的应用

现在我们将这些基[本构建模](@entry_id:183370)块应用于[DG方法](@entry_id:748369)的实际场景中。

#### 从[参考单元](@entry_id:168425)到物理单元

实际计算通常在规则的**[参考单元](@entry_id:168425) (reference element)** $\hat{K}$（如单位直角三角形）上进行，然后通过一个**[仿射映射](@entry_id:746332) (affine map)** $x = A \hat{x} + b$ 将结果转换到网格中的**物理单元 (physical element)** $K$。在这个过程中，梯度和积分都需要相应地变换。[梯度算子](@entry_id:275922)通过雅可比矩阵的逆[转置](@entry_id:142115)进行变换，即 $\nabla_x = A^{-T} \nabla_{\hat{x}}$。积分测度则乘以雅可比行列式的[绝对值](@entry_id:147688)，即 $\mathrm{d}x = |\det A| \,\mathrm{d}\hat{x}$。

利用这些变换规则，我们可以在[参考单元](@entry_id:168425)上计算梯度和积分，然后将它们组合起来得到物理单元上的[刚度矩阵](@entry_id:178659)。例如，要计算物理单元上的刚度矩阵项 $K_{ij} = \int_{K} \nabla_{x} B_{i} \cdot \nabla_{x} B_{j} \,\mathrm{d}x$，我们可以执行以下步骤 ：
1.  在[参考单元](@entry_id:168425)上计算[基函数](@entry_id:170178)梯度 $\nabla_{\hat{x}} B_i$ 和 $\nabla_{\hat{x}} B_j$。
2.  使用 $A^{-T}$ 将它们变换到物理梯度 $\nabla_{x} B_i$ 和 $\nabla_{x} B_j$。
3.  计算它们的[点积](@entry_id:149019)，这是一个常数（对于线性元）。
4.  将该常[数乘](@entry_id:155971)以物理单元的面积 $|K| = |\det A| \cdot \text{Area}(\hat{K})$。

这种系统性的方法是所有基于有限元的代码实现的基础。

#### 多项式次数变换

在自适应方法或[多重网格方法](@entry_id:146386)中，经常需要在不同多项式次数的空间之间传递信息。**次数提升 (degree elevation)** 是将一个次数为 $n$ 的[Bernstein多项式](@entry_id:146090)精确表示为次数为 $n+1$ 的多项式的过程，这是一个简单而精确的代数操作。

相比之下，**次数降低 (degree reduction)** 更为复杂，通常通过 $L^2$ **投影 (projection)** 来实现。给定一个次数为 $n$ 的多项式 $p_n(x)$，我们寻找其在次数为 $n-1$ 的[多项式空间](@entry_id:144410) $\mathbb{P}_{n-1}$ 中的最佳逼近 $q_{n-1}(x)$，使得误差 $p_n - q_{n-1}$ 与 $\mathbb{P}_{n-1}$ 中的所有函数正交。这导致了一个[线性方程组](@entry_id:148943)，即**法方程 (normal equations)** ：
$$
M \boldsymbol{b} = R \boldsymbol{a}
$$
其中 $\boldsymbol{a}$ 是 $p_n$ 的次数为 $n$ 的Bernstein系数向量，$\boldsymbol{b}$ 是 $q_{n-1}$ 的次数为 $n-1$ 的Bernstein系数向量。矩阵 $M$ 是次数为 $n-1$ 的基的[质量矩阵](@entry_id:177093)，而 $R$ 是一个耦合了次数 $n$ 和 $n-1$ 基的“矩形”[质量矩阵](@entry_id:177093)。通过求解这个（通常很小）的[线性系统](@entry_id:147850)，我们可以得到一个保持 $L^2$ 范数意义下最佳逼近的降阶算子。

#### [提升算子](@entry_id:751273)

在处理DG方法中的通量项时，**[提升算子](@entry_id:751273) (lifting operator)** $L$ 是一个至关重要的工具。它将定义在单元边界 $\partial T$ 上的函数（或多项式）$\phi$ “提升”为单元内部 $T$ 的一个多项式 $L\phi$，其定义满足以下变分关系：
$$
\int_{T} w\,(L\phi) \, \mathrm{d}A = \int_{\partial T} w\,\phi \, \mathrm{d}s, \quad \text{对所有检验函数 } w \in \mathcal{P}_n(T)
$$
为了计算 $L\phi$，我们将其在内部[Bernstein基](@entry_id:164098)中展开，$L\phi = \sum c_i B_i^n$，然后通过选择 $w$ 为每个[基函数](@entry_id:170178)来求解一个[线性系统](@entry_id:147850) ：
$$
M \boldsymbol{c} = \boldsymbol{r}
$$
这里，$M$ 正是内部基的[质量矩阵](@entry_id:177093)，而右端项 $\boldsymbol{r}$ 的分量为 $r_i = \int_{\partial T} B_i^n \phi \, \mathrm{d}s$。一个关键的观察是，由于 $\phi$ 通常只定义在一个面上，所以向量 $\boldsymbol{r}$ 是稀疏的。然而，由于质量矩阵 $M$ 是稠密的，其逆矩阵 $M^{-1}$ 也是稠密的。因此，最终的系数向量 $\boldsymbol{c} = M^{-1}\boldsymbol{r}$ 将是稠密的。这意味着，即使输入是一个局部化的面函数，[提升算子](@entry_id:751273)的输出也会影响到单元内部所有的[基函数](@entry_id:170178)。这揭示了[DG方法](@entry_id:748369)中局部通量如何影响整个单元解的内在机制。

### 与其他基的比较及计算考量

选择[Bernstein基](@entry_id:164098)并非没有代价，理解其与其它常用基（特别是**正交基 (orthogonal bases)**，如Dubiner基）的优劣对于设计高效的DG求解器至关重要。

#### 核心权衡：质量矩阵 vs. [微分算子](@entry_id:140145)

这两种基的选择体现了一个基本的计算权衡 ：
-   **[正交基](@entry_id:264024)**：根据定义，其**质量矩阵是对角的**。这使得[质量矩阵](@entry_id:177093)求[逆变](@entry_id:192290)得微不足道（只需对对角元素求倒数），这在[显式时间步进](@entry_id:168157)方法中是一个巨大的优势。然而，[正交多项式](@entry_id:146918)的导数通常是低阶多项式的稠密[线性组合](@entry_id:154743)，导致其**[微分算子](@entry_id:140145)是稠密的**。
-   **[Bernstein基](@entry_id:164098)**：其**质量矩阵是稠密且病态的**，求逆计算成本高昂。但是，它的**[微分算子](@entry_id:140145)是极其稀疏的**（如前所述，每行最多三个非零项），这使得与梯度相关的计算（如组装[刚度矩阵](@entry_id:178659)）非常高效。

我们可以通过构造一个显式的**[基变换矩阵](@entry_id:184480) (change-of-basis matrix)** $P$ 来量化这两种基之间的关系，该矩阵是稠密且可逆的 。

#### 时间步进与稳定性

在[显式时间步进](@entry_id:168157)方案中，稳定性通常受到Courant–Friedrichs–Lewy (CFL)条件的限制，该条件与半离散算子 $\mathbf{L} = \mathbf{M}^{-1}\mathbf{A}$ 的谱（[特征值](@entry_id:154894)）密切相关。

一个关键的理论事实是，算子 $\mathbf{L}$ 的**[特征值](@entry_id:154894)与基的选择无关** 。因为不同基下的矩阵表示是通过相似变换关联的，它们的谱是相同的。因此，任何纯粹基于[特征值](@entry_id:154894)[谱半径](@entry_id:138984)的CFL[稳定性估计](@entry_id:755306)对于[Bernstein基](@entry_id:164098)和正交基将是完全一样的。

然而，稳定性分析还有更深层次的考量。一个算子矩阵的**[非正规性](@entry_id:752585) (non-normality)** 会影响其短期行为和范数增长。由于[Bernstein基](@entry_id:164098)是非正交的，其对应的算子矩阵 $\mathbf{L}_{\text{Bernstein}}$ 通常比正交基下的矩阵 $\mathbf{L}_{\text{ortho}}$ 具有更强的[非正规性](@entry_id:752585)。这意味着，即使[特征值](@entry_id:154894)相同，$\|\exp(t\mathbf{L}_{\text{Bernstein}})\|$ 的范数可能在短期内经历显著增长。对于依赖范数有界性来保证稳定性的强稳定保持 (SSP)方法，这种[非正规性](@entry_id:752585)可能导致对[Bernstein基](@entry_id:164098)更严格（即更小）的[时间步长限制](@entry_id:756010) 。

#### 计算策略

综合以上考量，现代[DG方法](@entry_id:748369)的实现常常采用一种[混合策略](@entry_id:145261)，以兼得两类基的优点。一种常见的做法是 ：
1.  在计算代价主要由[微分算子](@entry_id:140145)决定的步骤中（例如，计算物理通量和体积积分），使用具有稀疏微分算子的基（如[Bernstein基](@entry_id:164098)或[节点基](@entry_id:752522)）。
2.  当需要应用[质量矩阵](@entry_id:177093)的逆时（这在[显式时间步进](@entry_id:168157)中每一步都需要），将系数向量**变换到[正交基](@entry_id:264024)**。
3.  在[正交基](@entry_id:264024)下，[质量矩阵](@entry_id:177093)的逆可以简单地通过[对角缩放](@entry_id:748382)来实现。
4.  将结果变换回原来的计算基。

虽然每次时间步都进行基变换会产生额外开销（两次[稠密矩阵](@entry_id:174457)-向量乘法），但这通常远低于求解一个稠密的线性系统（即对稠密[质量矩阵](@entry_id:177093)求逆）的成本。因此，在实践中，灵活地在不同基之间切换，是发挥[Bernstein基](@entry_id:164098)优势、同时克服其缺点的有效计算策略。