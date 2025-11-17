## 引言
在数据驱动的时代，信息常常以多维数组的形式出现，例如用户-产品-时间的交互数据，或是神经科学中的时空脑[活动记录](@entry_id:636889)。这些被称为“张量”的复杂数据结构蕴含着丰富的模式，但直接从中提取洞见却是一项重大挑战。我们如何才能揭开这些[高维数据](@entry_id:138874)背后的简洁结构，理解其内在的驱动因素？典范多元分解（Canonical Polyadic Decomposition, CPD），作为[张量分析](@entry_id:161423)的基石之一，为解决这一问题提供了强有力的框架。本文旨在系统性地介绍CPD，带领读者从理论基础走向实际应用。在接下来的内容中，您将首先通过“原理与机制”章节深入学习CPD的数学定义、关键性质（如唯一性）及其与[张量秩](@entry_id:266558)的深刻联系；随后，“应用与跨学科联系”章节将通过来自[推荐系统](@entry_id:172804)、神经科学和机器学习等领域的生动案例，展示CPD在揭示潜在结构、压缩数据和构建预测模型方面的巨大威力；最后，“动手实践”部分将提供具体的练习，帮助您巩固对核心概念的理解。通过这三个层次的递进学习，您将掌握使用CPD分析[多维数据](@entry_id:189051)的核心思想与方法。

## 原理与机制

在上一章引言中，我们介绍了张量作为多维数组在现代科学与工程领域中的普遍性。为了从这些复杂的[数据结构](@entry_id:262134)中提取有意义的潜在模式，我们需要强大的分析工具。其中最核心的工具之一是**典范多元分解（Canonical Polyadic Decomposition, CPD）**，也称为 CANDECOMP/[PARAFAC](@entry_id:753095)。本章将深入探讨 CPD 的基本原理、关键性质以及其背后的数学机制。

### 构建基石：秩-1张量

理解任何复杂的分解方法，首先要从其最基本的构成单元开始。对于 CPD 而言，这个基本单元就是**秩-1张量（rank-1 tensor）**。一个秩-1张量是由两个或多个向量的**[外积](@entry_id:147029)（outer product）**构成的。

对于一个 $N$ 阶张量 $\mathcal{T}$，如果它可以表示为 $N$ 个向量 $\mathbf{v}^{(1)}, \mathbf{v}^{(2)}, \dots, \mathbf{v}^{(N)}$ 的外积，那么它就是一个秩-1张量。我们记作：
$$ \mathcal{T} = \mathbf{v}^{(1)} \circ \mathbf{v}^{(2)} \circ \dots \circ \mathbf{v}^{(N)} $$
其中 $\circ$ 符号代表外积。这个表达式的含义在分量层面最为清晰。张量 $\mathcal{T}$ 的每一个元素 $(i_1, i_2, \dots, i_N)$ 都由各个向量的对应分量相乘得到：
$$ T_{i_1 i_2 \dots i_N} = v^{(1)}_{i_1} v^{(2)}_{i_2} \dots v^{(N)}_{i_N} $$
这里的 $v^{(n)}_{i_n}$ 是第 $n$ 个向量 $\mathbf{v}^{(n)}$ 的第 $i_n$ 个分量。

为了使这个定义更加具体，让我们考虑一个四阶秩-1张量 $\mathcal{T}$，它由四个三维向量 $\mathbf{a}, \mathbf{b}, \mathbf{c}, \mathbf{d}$ 构建而成。根据定义，其分量形式为 $T_{ijkl} = a_i b_j c_k d_l$。假设我们有以下四个向量 [@problem_id:1491555]：
$$ \mathbf{a} = (1.5, -2.1, 0.5) $$
$$ \mathbf{b} = (3.2, 1.8, -4.5) $$
$$ \mathbf{c} = (-1.0, 2.5, 6.1) $$
$$ \mathbf{d} = (0.9, -3.3, -5.2) $$
如果我们想计算张量分量 $T_{3123}$，我们只需根据索引选取相应向量的分量并相乘即可。这里 $i=3, j=1, k=2, l=3$。因此：
$$ T_{3123} = a_3 b_1 c_2 d_3 = (0.5) \times (3.2) \times (2.5) \times (-5.2) = -20.8 $$
这个简单的计算揭示了秩-1张量的核心特征：其所有信息都被编码在少数几个生成向量之中。一个 $I_1 \times I_2 \times \dots \times I_N$ 的张量通常需要 $\prod I_n$ 个数值来存储，而一个秩-1张量只需要 $\sum I_n$ 个数值（即所有生成向量的分量总数）。这种数据压缩的思想是[张量分解](@entry_id:173366)的基石。

### 典范多元分解（CPD）模型

现实世界中的数据张量很少是纯粹的秩-1张量。然而，一个更强大的假设是，一个复杂的张量可以被近似或精确地表示为有限个秩-1张量的和。这正是典范多元分解的核心思想。

一个 $N$ 阶张量 $\mathcal{T}$ 的秩-$R$ CPD 将其表示为 $R$ 个秩-1张量的和：
$$ \mathcal{T} = \sum_{r=1}^{R} \mathcal{T}_r = \sum_{r=1}^{R} \mathbf{a}^{(1)}_r \circ \mathbf{a}^{(2)}_r \circ \dots \circ \mathbf{a}^{(N)}_r $$
其中，每一个 $\mathbf{a}^{(n)}_r$ 都是一个向量。这些向量通常被组织成所谓的**因子矩阵（factor matrices）**。对于一个三阶张量 $\mathcal{T} \in \mathbb{R}^{I \times J \times K}$，其 CPD 由三个因子矩阵给出：
- $A \in \mathbb{R}^{I \times R}$，其列向量为 $\mathbf{a}_r$
- $B \in \mathbb{R}^{J \times R}$，其列向量为 $\mathbf{b}_r$
- $C \in \mathbb{R}^{K \times R}$，其列向量为 $\mathbf{c}_r$

因此，张量可以写作：
$$ \mathcal{T} = \sum_{r=1}^{R} \mathbf{a}_r \circ \mathbf{b}_r \circ \mathbf{c}_r $$
在分量层面，这个模型有一个非常直观的表达形式 [@problem_id:1542379]。张量 $\mathcal{T}$ 的任意一个元素 $T_{ijk}$ 可以通过对所有 $R$ 个秩-1分量在 $(i,j,k)$ 位置上的贡献求和得到：
$$ T_{ijk} = \sum_{r=1}^{R} (\mathbf{a}_r)_i (\mathbf{b}_r)_j (\mathbf{c}_r)_k = \sum_{r=1}^{R} A_{ir} B_{jr} C_{kr} $$
这个公式是 CPD 的核心计算式。它将高维张量中的一个元素与三个（或更多）低维因子矩阵中的元素联系起来。在[数据科学应用](@entry_id:276818)中（例如，用户-商品-情境数据），$A$ 的列可以被解释为“用户”的潜在特征，$B$ 的列是“商品”的潜在特征，$C$ 的列是“情境”的潜在特征，而 $R$ 是潜在特征的数量。

让我们通过一个具体的例子来理解这个求和过程 [@problem_id:1491553]。考虑一个 $2 \times 2 \times 2$ 的张量 $\mathcal{T}$，它由一个秩-2的CPD构成：
$$ \mathcal{T} = \mathbf{a}_1 \circ \mathbf{b}_1 \circ \mathbf{c}_1 + \mathbf{a}_2 \circ \mathbf{b}_2 \circ \mathbf{c}_2 $$
其中向量为：
$$ \mathbf{a}_1 = \begin{pmatrix} 1 \\ 3 \end{pmatrix}, \quad \mathbf{b}_1 = \begin{pmatrix} 2 \\ -1 \end{pmatrix}, \quad \mathbf{c}_1 = \begin{pmatrix} 1 \\ -2 \end{pmatrix} $$
$$ \mathbf{a}_2 = \begin{pmatrix} -1 \\ 2 \end{pmatrix}, \quad \mathbf{b}_2 = \begin{pmatrix} 4 \\ 1 \end{pmatrix}, \quad \mathbf{c}_2 = \begin{pmatrix} 0 \\ 3 \end{pmatrix} $$
要计算张量分量 $T_{212}$，我们应用分量公式，令 $i=2, j=1, k=2$：
$$ T_{212} = a_{1,2}b_{1,1}c_{1,2} + a_{2,2}b_{2,1}c_{2,2} $$
其中 $a_{r,i}$ 是向量 $\mathbf{a}_r$ 的第 $i$ 个分量。代入数值：
$$ T_{212} = (3)(2)(-2) + (2)(4)(3) = -12 + 24 = 12 $$
这个例子清楚地展示了最终张量的每个元素是如何由所有秩-1分量共同贡献形成的。

### CPD 的基本性质

CPD 不仅仅是一个数学表示，它还揭示了张量固有的结构。这些结构信息体现在因子矩阵与原始张量之间的深刻联系上。

#### 模态与因子的对应关系

CPD 的一个关键特性是每个因子矩阵都唯一地与张量的一个**模态（mode）**相关联。在三阶张量 $\mathcal{T} \in \mathbb{R}^{I \times J \times K}$ 的分解中，因子矩阵 $A \in \mathbb{R}^{I \times R}$ 对应第一模态（索引为 $i$），$B \in \mathbb{R}^{J \times R}$ 对应第二模态（索引为 $j$），$C \in \mathbb{R}^{K \times R}$ 对应第三模态（索引为 $k$）。

这种对应关系意味着，如果张量的模态发生[置换](@entry_id:136432)，其因子矩阵也会相应地进行同样的[置换](@entry_id:136432)。考虑一个张量 $\mathcal{T}$，其CPD因子为 $(A, B, C)$。现在，我们定义一个新张量 $\mathcal{P}$，通过交换 $\mathcal{T}$ 的第一和第二模态得到，即 $\mathcal{P}_{jik} = \mathcal{T}_{ijk}$ [@problem_id:1491586]。

原始张量的分量是：
$$ \mathcal{T}_{ijk} = \sum_{r=1}^{R} A_{ir} B_{jr} C_{kr} $$
由于 $\mathcal{P}_{jik} = \mathcal{T}_{ijk}$，我们可以写出：
$$ \mathcal{P}_{jik} = \sum_{r=1}^{R} A_{ir} B_{jr} C_{kr} $$
因为[标量乘法](@entry_id:155971)是可交换的，我们可以重新[排列](@entry_id:136432)求和项内的因子，使其与 $\mathcal{P}$ 的索引顺序 $(j, i, k)$ 相匹配：
$$ \mathcal{P}_{jik} = \sum_{r=1}^{R} B_{jr} A_{ir} C_{kr} $$
将这个表达式与 $\mathcal{P}$ 的标准CPD形式 $\mathcal{P}_{jik} = \sum_{r=1}^R A'_{jr} B'_{ir} C'_{kr}$ 进行比较，我们立即可以识别出新张量 $\mathcal{P}$ 的因子矩阵为 $(B, A, C)$。这个简单的练习强调了一个深刻的观点：CPD 的因子矩阵忠实地反映了它们所对应的张量模态的属性。

#### 对称性

当张量具有某些对称性时，这些对称性会直接反映在其CPD因子矩阵上，前提是分解是唯一的。这是一个非常有用的性质，因为它允许我们从数据中学习到结构约束。

考虑一个三阶张量 $\mathcal{T} \in \mathbb{R}^{I \times J \times I}$，其第一和第三模态的维度相同。如果这个张量在这两个模态上是对称的，即 $\mathcal{T}_{ijk} = \mathcal{T}_{kji}$ 对所有 $i, j, k$ 成立 [@problem_id:1491542]。

给定 $\mathcal{T}$ 的CPD为 $(A, B, C)$，我们有：
$$ \mathcal{T}_{ijk} = \sum_{r=1}^{R} A_{ir} B_{jr} C_{kr} $$
利用对称性，我们也可以写出：
$$ \mathcal{T}_{kji} = \sum_{r=1}^{R} A_{kr} B_{jr} C_{ir} $$
由于对称性，$\mathcal{T}_{ijk} = \mathcal{T}_{kji}$，因此 $\mathcal{T}_{ijk} = \sum_{r=1}^{R} A_{kr} B_{jr} C_{ir}$。由于[标量乘法](@entry_id:155971)是可交换的，我们可以重新[排列](@entry_id:136432)求和项内的因子，得到 $\mathcal{T}_{ijk} = \sum_{r=1}^{R} C_{ir} B_{jr} A_{kr}$。这表明张量 $\mathcal{T}$ 同时拥有两个CPD表示：一个由因子 $(A, B, C)$ 给出，另一个由 $(C, B, A)$ 给出。在CPD具有**本质唯一性**（稍后讨论）的条件下，这两个分解必须是等价的。在消除了平凡的尺度和[置换](@entry_id:136432)模糊性后，我们可以得出结论，对应的因子矩阵必须相等。因此，对于一个在第一和第三模态上对称的张量，其CPD因子矩阵必须满足：
$$ A = C $$
这个结果在许多领域都有应用，例如在信号处理和[化学计量学](@entry_id:140916)中，[对称张量](@entry_id:148092)模型很常见。它意味着我们只需要寻找两个而不是三个因子矩阵，从而简化了计算问题并增强了模型的可解释性。

### [张量秩](@entry_id:266558)的概念

与矩阵一样，**[张量秩](@entry_id:266558)（tensor rank）**（或称**[CP秩](@entry_id:748030)**）是一个核心概念，但其性质要复杂得多。一个张量 $\mathcal{T}$ 的秩，记为 $\operatorname{rank}(\mathcal{T})$，被定义为能够精确表示该张量所需的最少秩-1张量的数量 $R$。

对于矩阵（[二阶张量](@entry_id:199780)），秩具有许多良好性质，例如秩可以通过奇异值分解轻松计算。然而，对于三阶及更高阶的张量，情况就大为不同了：
1.  计算[张量秩](@entry_id:266558)是一个NP-hard问题。
2.  [张量秩](@entry_id:266558)依赖于其所在的[数域](@entry_id:155558)（例如，实数域或[复数域](@entry_id:153768)）。
3.  [张量秩](@entry_id:266558)的性质远不如[矩阵秩](@entry_id:153017)直观。

一个基本的性质是秩的[次可加性](@entry_id:137224)。对于两个同样大小的张量 $\mathcal{A}$ 和 $\mathcal{B}$，其和的秩上限为：
$$ \operatorname{rank}(\mathcal{A} + \mathcal{B}) \le \operatorname{rank}(\mathcal{A}) + \operatorname{rank}(\mathcal{B}) $$
这个不等式很容易理解：如果 $\mathcal{A}$ 是 $R_A$ 个秩-1项的和，$\mathcal{B}$ 是 $R_B$ 个秩-1项的和，那么 $\mathcal{A} + \mathcal{B}$ 显然可以表示为 $R_A + R_B$ 个秩-1项的和。然而，有趣的是，当 $\mathcal{A}$ 和 $\mathcal{B}$ 的秩-1分量之间存在线性相关时，和的秩可能会显著减小 [@problem_id:1491595]。例如，如果 $\mathcal{A}$ 的一个秩-1分量恰好是 $\mathcal{B}$ 的一个秩-1分量的负数，它们在求和时会相互抵消，从而降低最终的秩。

确定[张量秩](@entry_id:266558)的下界是一个有用的实践技巧。一种方法是检查张量的**切片（slices）**。一个三阶张量 $\mathcal{T}$ 的第 $k$ 个**正面切片（frontal slice）**是一个矩阵 $\mathcal{T}_{::k}$，其元素为 $(\mathcal{T}_{::k})_{ij} = \mathcal{T}_{ijk}$。从CPD的定义式 $T_{ijk} = \sum_{r=1}^{R} A_{ir} B_{jr} C_{kr}$ 可以看出，每个切片都可以写成：
$$ \mathcal{T}_{::k} = \sum_{r=1}^{R} C_{kr} (\mathbf{a}_r \mathbf{b}_r^T) $$
这是一个秩-1矩阵的线性组合，因此其[矩阵秩](@entry_id:153017)最多为 $R$。这意味着张量的[CP秩](@entry_id:748030)必然不小于其任何切片的[矩阵秩](@entry_id:153017)：
$$ \operatorname{rank}(\mathcal{T}) \ge \max_{k} \operatorname{rank}(\mathcal{T}_{::k}) $$
这个**切片秩下界**为我们提供了一个估计[张量秩](@entry_id:266558)的实用工具。

#### 边界秩

[张量秩](@entry_id:266558)最令人困惑和着迷的特性之一是**边界秩（border rank）**的概念。与矩阵不同，低秩张量的集合在拓扑上不是闭合的。这意味着一个秩较高的张量可以是一系列秩较低的张量的极限。

一个张量 $\mathcal{T}$ 的边界秩，记为 $\underline{\operatorname{rank}}(\mathcal{T})$，是 $R$ 的最小值，使得 $\mathcal{T}$ 可以被一系列秩为 $R$ 的张量 $\mathcal{T}_n$ 任意逼近，即 $\lim_{n \to \infty} \mathcal{T}_n = \mathcal{T}$。显然，总有 $\underline{\operatorname{rank}}(\mathcal{T}) \le \operatorname{rank}(\mathcal{T})$。

一个经典的例子是所谓的**W-张量**，它源于[量子信息](@entry_id:137721)理论，是一个 $2 \times 2 \times 2$ 的张量 [@problem_id:1491556]。该[张量的秩](@entry_id:204291)为3，但其边界秩为2。这意味着 $\mathcal{W}$ 本身不能表示为2个秩-1张量的和，但我们可以构造一个序列，其中每个张量都是秩-2的，而这个序列的极限是 $\mathcal{W}$。

考虑一个张量序列 $\mathcal{T}_n$，其秩为2，定义为：
$$ \mathcal{T}_n = (n\mathbf{e}_1 + \mathbf{e}_2) \circ (\mathbf{e}_1 + \frac{1}{n}\mathbf{e}_2) \circ (\mathbf{c}_1^{(n)}) + (-n\mathbf{e}_1) \circ (\mathbf{e}_1) \circ (\mathbf{e}_1) $$
通过适当选择向量 $\mathbf{c}_1^{(n)}$ 并展开这些项，可以发现随着 $n \to \infty$，一些项会消失，而另一些项会汇聚，最终得到秩-3的W-张量。这个现象表明，在数值计算中，一个真实的秩-3张量可能被一个秩-2的模型以极高的精度近似，这给秩的确定带来了巨大的挑战。

### CPD的唯一性

对于数据分析而言，分解的**唯一性（uniqueness）**至关重要。如果一个张量只有一个（或本质上一个）CPD，那么我们就可以赋予其因子以明确的物理解释。幸运的是，与大多数矩阵分解不同，CPD在非常温和的条件下通常是唯一的。

#### 内在的模糊性

首先，我们需要明确CPD中无法避免的两种模糊性：
1.  **尺度模糊性（Scaling Ambiguity）**：对于任何一个秩-1分量 $\mathbf{a}_r \circ \mathbf{b}_r \circ \mathbf{c}_r$，我们可以用非零标量 $\alpha, \beta, \gamma$ 来重新缩放因子向量，只要它们的乘积为1 [@problem_id:1491578]。
    $$ (\alpha \mathbf{a}_r) \circ (\beta \mathbf{b}_r) \circ (\gamma \mathbf{c}_r) = (\alpha\beta\gamma)(\mathbf{a}_r \circ \mathbf{b}_r \circ \mathbf{c}_r) $$
    如果 $\alpha\beta\gamma=1$，则秩-1张量保持不变。这意味着因子[向量的范数](@entry_id:154882)本身没有绝对的意义，通常需要通过施加约束（如将其中一个或多个[向量归一化](@entry_id:149602)）来固定尺度。

2.  **[置换](@entry_id:136432)模糊性（Permutation Ambiguity）**：CPD是秩-1项的求和，求和的顺序无关紧要。因此，我们可以任意[置换](@entry_id:136432)秩-1分量的顺序。这对应于同时对因子矩阵 $A, B, C$ 的列进行相同的[置换](@entry_id:136432)。

当一个CPD在排除了这两种平凡的模糊性后是唯一的，我们就称其为**本质唯一（essentially unique）**。

#### Kruskal 唯一性定理

对于[二阶张量](@entry_id:199780)（矩阵），即使是秩-R分解通常也不是唯一的。例如，一个简单的 $2 \times 2$ 单位矩阵（乘以2）可以有无穷多组不同的秩-2分解 [@problem_id:1491570]。然而，对于三阶及更高阶的张量，情况截然不同。

关于CPD唯一性的最著名结果是 **Kruskal 定理**。该定理为三阶张量的CPD提供了充分的唯一性条件。它依赖于一个叫做**Kruskal秩（k-rank）**或**k-秩**的概念。一个矩阵的k-秩是最大的整数 $k$，使得该矩阵的任意 $k$ 个列向量都是[线性无关](@entry_id:148207)的。

**Kruskal 定理**：
考虑一个三阶张量 $\mathcal{T}$ 的秩-$R$ CPD，其因子矩阵为 $A, B, C$。设这些矩阵的k-秩分别为 $k_A, k_B, k_C$。如果满足以下条件：
$$ k_A + k_B + k_C \ge 2R + 2 $$
那么张量 $\mathcal{T}$ 的秩就是 $R$，并且其CPD是本质唯一的。

这个定理非常强大。它告诉我们，只要因子矩阵的列向量具有足够高的“[一般性](@entry_id:161765)”（即不包含太多线性相关的列），分解就是唯一的。在实际应用中，例如，当一个团队分析一个客户-产品-地区数据集时，他们需要确保他们提取的 $R$ 个潜在因子是可解释和稳定的。Kruskal定理提供了一个可检验的条件来保证这一点 [@problem_id:1491598]。如果已知因子矩阵 $A$ 和 $B$ 的k-秩分别为 $k_A$ 和 $k_B$，那么为了保证唯一性，第三个因子矩阵 $C$ 的k-秩 $k_C$ 必须至少满足：
$$ k_C \ge 2R + 2 - k_A - k_B $$
这个条件是CPD成为[多维数据分析](@entry_id:201803)中一个如此有价值的工具的核心原因之一：它能够从数据中提取出稳定且可解释的潜在结构，而这在传统的矩阵方法中是很难实现的。

本章我们从CPD的基本构成单元——秩-1张量开始，逐步构建了CPD模型。我们探讨了该模型的关键性质，如模态-因子对应和对称性，并深入研究了[张量秩](@entry_id:266558)和边界秩的复杂概念。最后，我们阐明了CPD的唯一性条件，这是其在实践中获得成功的理论基石。在接下来的章节中，我们将讨论如何计算CPD以及它在不同领域的具体应用。