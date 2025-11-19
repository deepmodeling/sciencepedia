## 引言
[广义奇异值](@entry_id:749794)分解（Generalized Singular Value Decomposition, GSVD）是数值线性代数中一个极其强大的工具，它是标准奇异值分解（SVD）向处理矩阵对的自然推广。当一个系统或问题涉及两个[线性变换](@entry_id:149133)作用于同一个[向量空间](@entry_id:151108)时，SVD便独力难支，而GSVD则能提供深刻的洞察。其核心意义在于，它能够揭示两个矩阵之间相互关联的内在几何结构，这在解决许多科学与工程领域的复杂问题时至关重要。

本文旨在系统性地介绍[广义奇异值](@entry_id:749794)分解。我们面临的核心问题是：如何理解并利用两个矩阵的联合作用？GSVD通过提供一个统一的谱分解框架来回答这一问题，从而解决了从[不适定问题](@entry_id:182873)的正则化到[多模态数据](@entry_id:635386)的比较等一系列挑战。

在接下来的内容中，读者将踏上一段从理论到实践的旅程。第一章“原理与机制”将深入探讨GSVD的数学定义、[代数结构](@entry_id:137052)及其与[广义特征值问题](@entry_id:151614)的深刻联系，并分析其数值计算方法。第二章“应用与跨学科联系”将展示GSVD如何在正则化、[约束优化](@entry_id:635027)、数据集比较等实际问题中发挥作用，连接起理论与不同学科的应用。最后，在“动手实践”部分，通过精心设计的计算问题，您将有机会亲手应用所学知识，巩固对GSVD的理解。

## 原理与机制

继前一章介绍[广义奇异值分解 (GSVD)](@entry_id:749795) 的背景与动机之后，本章将深入探讨其核心的数学原理与内在机制。我们将从其形式化定义出发，揭示其[代数结构](@entry_id:137052)，阐明[广义奇异值](@entry_id:749794)的含义，并探讨其与[广义特征值问题](@entry_id:151614)之间深刻的联系。此外，本章还将详细分析计算 GSVD 的主要数值方法，讨论其稳定性、计算成本以及在[有限精度算术](@entry_id:142321)下面临的挑战。最后，我们将通过正则化这一经典应用，展示 GSVD 如何为解决[不适定问题](@entry_id:182873)提供一个强大而优雅的分析框架。

### GSVD 的形式化定义与[代数结构](@entry_id:137052)

[广义奇异值](@entry_id:749794)分解旨在同时处理一对具有相同列数的矩阵。对于给定的两个矩阵 $A \in \mathbb{C}^{m \times n}$ 和 $B \in \mathbb{C}^{p \times n}$，它们的 GSVD 提供了一种将这两个矩阵[同时对角化](@entry_id:196036)的方法，从而揭示出它们作用于同一个[向量空间](@entry_id:151108) $\mathbb{C}^n$ 时的内在几何关系。

一个被广泛采用的 GSVD 定义，特别是 Paige 和 Saunders 提出的形式，其表述如下：对于任意矩阵对 $(A, B)$，存在酉矩阵 $U \in \mathbb{C}^{m \times m}$ 和 $V \in \mathbb{C}^{p \times p}$，以及一个[可逆矩阵](@entry_id:171829) $X \in \mathbb{C}^{n \times n}$，使得：

$U^* A X = \Sigma_A$
$V^* B X = \Sigma_B$

这里的 $\Sigma_A$ 和 $\Sigma_B$ 是具有特定稀疏块结构的“广义对角”矩阵。为了精确描述这种结构，我们需要首先定义几个与[矩阵秩](@entry_id:153017)相关的整数 [@problem_id:3547764]。令 $\mathrm{rank}(A) = r_A$，$\mathrm{rank}(B) = r_B$，并定义复合矩阵 $G = \begin{bmatrix} A \\ B \end{bmatrix}$ 的秩为 $k = \mathrm{rank}(G)$。基于这些量，我们可以定义以下四个[子空间](@entry_id:150286)的维度：

- $q = n - k$：这是 $A$ 和 $B$ 的公共零空间 $\mathcal{N}(A) \cap \mathcal{N}(B)$ 的维度。
- $s = r_A + r_B - k$：这对应于被 $A$ 和 $B$ 同时非平凡地映射的“共享”[子空间](@entry_id:150286)的维度。
- $k_A = r_A - s$：这对应于仅被 $A$ 非平凡地映射的“A-独占”[子空间](@entry_id:150286)的维度。
- $k_B = r_B - s$：这对应于仅被 $B$ 非平凡地映射的“B-独占”[子空间](@entry_id:150286)的维度。

这些维度之和恰好为 $n$：$q + s + k_A + k_B = n$。矩阵 $X$ 的列向量构成了 $\mathbb{C}^n$ 的一组基，这组基根据其在 $A$ 和 $B$ 作用下的不同行为被划分为四个组，其大小分别对应于 $q, s, k_B, k_A$。

在 GSVD 分解中，矩阵 $\Sigma_A$ 和 $\Sigma_B$ 的具体形式为：

$\Sigma_A = U^*AX = \begin{bmatrix} 0_{m \times q}  C  0_{m \times k_B}  I_{k_A} \end{bmatrix}_{\text{padded}}$
$\Sigma_B = V^*BX = \begin{bmatrix} 0_{p \times q}  S  I_{k_B}  0_{p \times k_A} \end{bmatrix}_{\text{padded}}$

其中，下标 "padded" 表示这些[块矩阵](@entry_id:148435)被适当地嵌入到 $m \times n$ 和 $p \times n$ 的零矩阵中。核心部分是两个对角矩阵 $C = \mathrm{diag}(c_1, \dots, c_s)$ 和 $S = \mathrm{diag}(s_1, \dots, s_s)$，它们的对角元均为非负实数，并满足 **余弦-正弦关系** (cosine-sine relationship)：

$C^T C + S^T S = I_s \quad (\text{即 } c_i^2 + s_i^2 = 1 \text{ for } i=1, \dots, s)$

$I_{k_A}$ 和 $I_{k_B}$ 是单位矩阵。这个分解清晰地揭示了 $A$ 和 $B$ 的行为：$X$ 的前 $q$ 列构成了它们的公共[零空间](@entry_id:171336)；接下来的 $s$ 列被两者同时以一种“互补”的方式映射（由 $c_i, s_i$ 体现）；再接下来的 $k_B$ 列仅被 $B$ “单位化”地映射（而为 $A$ 的[零空间](@entry_id:171336)部分）；最后 $k_A$ 列则仅被 $A$ “单位化”地映射（而为 $B$ 的[零空间](@entry_id:171336)部分）。

### [广义奇异值](@entry_id:749794)及其解释

GSVD 的核心是 **[广义奇异值](@entry_id:749794) (Generalized Singular Values)**，定义为与 $C$ 和 $S$ 相关的比值。对于 $s_i \neq 0$ 的指标 $i$，[广义奇异值](@entry_id:749794) $\gamma_i$ 定义为：

$\gamma_i = \frac{c_i}{s_i}$

这些值捕捉了矩阵 $A$ 和 $B$ 在“共享”[子空间](@entry_id:150286)上的相对“尺度”。然而，当 $s_i$ 或 $c_i$ 为零时，会出现一些特殊但具有重要解释意义的情况 [@problem_id:3547797]。

- **无限[广义奇异值](@entry_id:749794) ($\gamma_i = \infty$)**: 当 $s_i = 0$ 且 $c_i  0$ 时（根据约定 $c_i^2+s_i^2=1$，此时 $c_i=1$），[广义奇异值](@entry_id:749794)被视为无限大。这种情况对应于 GSVD 结构中的 $I_{k_A}$ 区块，或者在 $C, S$ 块中出现 $s_i=0, c_i=1$ 的情况。设 $x_i$ 是 $X$ 中与此对应的列向量。分解关系 $A x_i = c_i u_i$ 和 $B x_i = s_i v_i$ 变为 $A x_i \neq 0$ 和 $B x_i = 0$。因此，**无限[广义奇异值](@entry_id:749794)对应于那些属于 $B$ 的[零空间](@entry_id:171336)但不属于 $A$ 的[零空间](@entry_id:171336)的向量**。例如，对于矩阵对 $A = \begin{bmatrix} 0  1 \\ 0  1 \\ 0  1 \end{bmatrix}$ 和 $B = \begin{bmatrix} 1  0 \\ 0  0 \\ 0  0 \end{bmatrix}$，向量 $x = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$ 满足 $Bx=0$ 但 $Ax \neq 0$，因此它对应一个无限[广义奇异值](@entry_id:749794)。

- **零[广义奇异值](@entry_id:749794) ($\gamma_i = 0$)**: 当 $c_i = 0$ 且 $s_i  0$ 时（此时 $s_i=1$），[广义奇异值](@entry_id:749794)为零。这对应于 $I_{k_B}$ 区块或 $C,S$ 块中的相应情况。此时，$A x_i = 0$ 且 $B x_i \neq 0$。因此，**零[广义奇异值](@entry_id:749794)对应于那些属于 $A$ 的[零空间](@entry_id:171336)但不属于 $B$ 的[零空间](@entry_id:171336)的向量**。在上述例子中，向量 $x = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$ 满足 $Ax=0$ 但 $Bx \neq 0$，因此它对应一个零[广义奇异值](@entry_id:749794)。

### 与[广义特征值问题](@entry_id:151614)的联系

GSVD 与一个特定的[广义特征值问题](@entry_id:151614) (GEP) 紧密相关。考虑由 $A$ 和 $B$ 导出的两个[对称半正定矩阵](@entry_id:163376) $A^T A$ 和 $B^T B$。与矩阵对 $(A^T A, B^T B)$ 相关的[广义特征值问题](@entry_id:151614)定义为寻找标量 $\lambda$ 和非[零向量](@entry_id:156189) $x$，使得：

$A^T A x = \lambda B^T B x$

这个 GEP 的[特征值](@entry_id:154894)与[广义奇异值](@entry_id:749794)之间存在直接关系。将 GSVD 关系 $A = U \Sigma_A X^{-1}$ 和 $B = V \Sigma_B X^{-1}$ 代入上式（注意此处为了简化，我们使用$\Sigma_A, \Sigma_B$代表其核心对角部分$C,S$等），可得：

$(X^{-T} \Sigma_A^T U^T) (U \Sigma_A X^{-1}) x = \lambda (X^{-T} \Sigma_B^T V^T) (V \Sigma_B X^{-1}) x$

化简后得到：

$X^{-T} \Sigma_A^T \Sigma_A X^{-1} x = \lambda X^{-T} \Sigma_B^T \Sigma_B X^{-1} x$

两边同时左乘 $X^T$ 并右乘 $X$，我们得到：

$(\Sigma_A^T \Sigma_A) y = \lambda (\Sigma_B^T \Sigma_B) y$，其中 $y = X^{-1} x$。

由于 $\Sigma_A^T \Sigma_A$ 和 $\Sigma_B^T \Sigma_B$ 的核心部分是 $C^T C = \mathrm{diag}(c_i^2)$ 和 $S^T S = \mathrm{diag}(s_i^2)$，上式对每个分量 $y_i$ 独立成立：$c_i^2 y_i = \lambda_i s_i^2 y_i$。因此，我们得到广义[特征值](@entry_id:154894) $\lambda_i$ 和[广义奇异值](@entry_id:749794) $\gamma_i$ 之间的核心关系：

$\lambda_i = \frac{c_i^2}{s_i^2} = \left(\frac{c_i}{s_i}\right)^2 = \gamma_i^2$

这个关系是 GSVD 理论的基石之一，它不仅提供了另一种理解 GSVD 的视角，也启发了一种计算 GSVD 的方法 [@problem_id:3547782]。

这个框架可以自然地推广到 **加权GSVD (Weighted GSVD)**。如果我们考虑带权重的二次型 $\|Ax\|_M^2 = x^T A^T M A x$ 和 $\|Bx\|_N^2 = x^T B^T N B x$，其中 $M$ 和 $N$ 是[对称正定](@entry_id:145886)权重矩阵，那么相应的[广义特征值问题](@entry_id:151614)就变为求解 $(A^T M A, B^T N B)$ 的[特征值](@entry_id:154894) [@problem_id:3547766]。其[特征值](@entry_id:154894) $\lambda_i$ 同样满足 $\lambda_i = \gamma_i^2$，其中 $\gamma_i$ 是相应加权 GSVD 的[广义奇异值](@entry_id:749794)。

### 计算方法与数值稳定性

尽管通过求解[广义特征值问题](@entry_id:151614) $(A^T A, B^T B)$ 来计算 GSVD 在理论上是可行的，但在数值实践中，这种方法存在严重缺陷。

#### 基于[正规方程](@entry_id:142238)的方法及其缺陷

直接计算并形成[格拉姆矩阵](@entry_id:203297) (Gram matrices) $A^T A$ 和 $B^T B$ 的方法被称为 **正规方程法**。其主要问题在于，这个过程会 **平方矩阵的条件数**。对于一个矩阵 $M$，其[条件数](@entry_id:145150) $\kappa(M)$ 衡量了其对扰动的敏感性。在数值计算中，有如下重要关系：

$\kappa(M^T M) = (\kappa(M))^2$

如果原始矩阵 $A$ 或 $B$ 是病态的（即[条件数](@entry_id:145150)很大），那么 $A^T A$ 或 $B^T B$ 的条件数将变得极大，导致在求解特征值问题时出现严重的精度损失。

更糟糕的是，当 $A$ 或 $B$ 接近[秩亏](@entry_id:754065)时，其最小[奇异值](@entry_id:152907) $\sigma_{\min}$ 接近于零。对应的格拉姆矩阵的[最小特征值](@entry_id:177333)为 $\sigma_{\min}^2$，这个值可能比计算过程中产生的[浮点舍入](@entry_id:749455)误差还要小。这会导致计算出的 $A^T A$ 或 $B^T B$ 在数值上失去[半正定性](@entry_id:147720)，甚至可能出现负的[特征值](@entry_id:154894)。依赖于矩阵[正定性](@entry_id:149643)（如基于 Cholesky 分解）的 GEP 求解器在这种情况下会彻底失败 [@problem_id:3547782]。

#### 基于[正交变换](@entry_id:155650)的稳定算法

为了避免上述数值陷阱，现代数值计算推崇使用直接作用于原始矩阵 $A$ 和 $B$ 的 **正交变换** 方法。这类算法，如 Paige 和 Saunders 的经典算法，通过一系列数值稳定的变换（如 QR 分解和 CS 分解）来逐步得到 GSVD。由于[正交变换](@entry_id:155650)是保范数的，它们不会放大舍入误差，因此整个算法是 **向后稳定 (backward stable)** 的。这意味着计算得到的 GSVD 是一个与原始矩阵对 $(A, B)$ 相差很小的矩阵对 $(A+\delta A, B+\delta B)$ 的精确分解。

这类算法的典型步骤是首先对[增广矩阵](@entry_id:150523) $G = \begin{bmatrix} A \\ B \end{bmatrix}$ 进行 QR 分解。为了在[数值秩](@entry_id:752818)亏的情况下获得可靠的结果，通常会采用 **列主元 QR 分解 (QR with column pivoting)**。主元策略通过在每一步选择范数最大的列作为主元，有助于将线性相关的列排到后面，从而可靠地识别出矩阵的[数值秩](@entry_id:752818)，并将问题分解为良态和病态两个部分 [@problem_id:3547789]。这大大提高了计算所得的有限[广义奇异值](@entry_id:749794)的相对精度。

这类基于 QR 的算法的计算成本主要由初始的 QR 分解和后续的 CS 分解主导，其领先项复杂度通常为 $O((m+p)n^2 + n^3)$ [@problem_id:3547789]。

#### 实践中的预处理与后处理

1.  **缩放与均衡 (Scaling and Equilibration)**: 当矩阵 $A$ 和 $B$ 的范数相差悬殊时（例如 $\|A\| \gg \|B\|$），直接对[增广矩阵](@entry_id:150523) $G$ 进行 QR 分解可能会导致 $B$ 的信息在[浮点运算](@entry_id:749454)中被“淹没”。因此，对 $A$ 和 $B$ 进行预处理的缩放是一个重要的步骤。一个有效的策略是应用一个共同的右[对角缩放](@entry_id:748382)矩阵 $D$，即考虑矩阵对 $(AD, BD)$。这种变换不改变[广义奇异值](@entry_id:749794)，但通过选择合适的 $D$（例如，使得[增广矩阵](@entry_id:150523)的各列范数大致相等），可以改善问题的整体[条件数](@entry_id:145150)，提高计算的鲁棒性 [@problem_id:3547771]。

2.  **后处理与约束强制**: 由于[浮点误差](@entry_id:173912)的累积，计算得到的对角元 $\hat{c}_i, \hat{s}_i$ 可能不严格满足 $\hat{c}_i^2 + \hat{s}_i^2 = 1$ 的约束，而是 $\hat{c}_i^2 + \hat{s}_i^2 = 1 + \delta_i$，其中 $\delta_i$ 是一个小的误差。为了恢复这一重要结构，可以进行一次后处理。一个稳定有效的方法是对每一对 $(\hat{c}_i, \hat{s}_i)$ 进行归一化：
    $r_i = \sqrt{\hat{c}_i^2 + \hat{s}_i^2}$
    $c_i' = \hat{c}_i / r_i, \quad s_i' = \hat{s}_i / r_i$
    为了保持 GSVD 的整体关系，这个缩放必须被吸收到可逆矩阵 $X$ 中，即令 $X' = X \cdot \mathrm{diag}(1/r_1, \dots, 1/r_n)$。这个过程可以精确地恢复余弦-正弦关系，且对原始分解的扰动极小 [@problem_id:3547769]。

### 在正则化问题中的应用

GSVD 最重要的应用之一是分析和求解一般形式的 **Tikhonov 正则化问题**。这类问题旨在处理不适定线性系统 $Ax=b$，其形式如下：

$\min_{x} \|Ax - b\|^2 + \lambda^2 \|Bx\|^2$

其中 $A$ 是系统矩阵， $B$ 是正则化算子（或惩罚项），$\lambda  0$ 是正则化参数。GSVD 提供了一个理想的[坐标系](@entry_id:156346)来分析和解决这个问题。

将 GSVD 分解 $A = U \Sigma_A X^{-1}$ 和 $B = V \Sigma_B X^{-1}$ 代入[目标函数](@entry_id:267263)，并令 $y = X^{-1}x$ 以及 $\tilde{b} = U^T b$，目标函数在 $y$ 坐标下变为：

$\min_{y} \|\Sigma_A y - \tilde{b}\|^2 + \lambda^2 \|\Sigma_B y\|^2$

由于 $\Sigma_A$ 和 $\Sigma_B$ 的核心是[对角矩阵](@entry_id:637782) $C$ 和 $S$，上式可以分解为多个独立的标量最小化问题：

$\min_{y_i} (c_i y_i - \tilde{b}_i)^2 + \lambda^2 (s_i y_i)^2$

对每个 $y_i$ 求导并令其为零，可得解：

$y_i = \left( \frac{c_i}{c_i^2 + \lambda^2 s_i^2} \right) \tilde{b}_i$

括号中的项被称为 **滤波因子 (filter factors)**。它们揭示了正则化解的本质：原始数据在 GSVD [坐标系](@entry_id:156346)下的分量 $\tilde{b}_i$ 被一个与[广义奇异值](@entry_id:749794) $\gamma_i=c_i/s_i$ 和正则化参数 $\lambda$ 相关的因子所“过滤”或“抑制”。

- 当[广义奇异值](@entry_id:749794) $\gamma_i = c_i/s_i$ 很大时，滤波因子近似为 $1/c_i$，解的分量 $y_i$ 主要由数据决定。
- 当[广义奇异值](@entry_id:749794) $\gamma_i$ 很小时（即 $c_i \ll s_i$），问题变得不适定。此时滤波因子近似为 $c_i/(\lambda^2 s_i^2)$。若不加正则化（$\lambda \to 0$），该因子会变得极大，导致噪声被剧烈放大。正则化参数 $\lambda$ 的作用正是为了抑制这些与小 $\gamma_i$ 相关的分量，从而稳定解。

GSVD 框架也使得选择正则化参数的策略变得透明。例如，**Morozov 差异原理 (Morozov's Discrepancy Principle)** 要求[残差范数](@entry_id:754273) $\|Ax_\lambda - b\|$ 等于噪声水平 $\delta$。在 GSVD [坐标系](@entry_id:156346)下，这个方程可以被精确表达并求解 $\lambda$ [@problem_id:3547791]。同样，我们也可以精确计算为将噪声放大控制在特定水平下所需的最小正则化参数 [@problem_id:3547802]。

### 高级结构属性：块分解

在处理大规模问题时，例如在区域分解方法中，我们常常关心 GSVD 是否具有块结构，从而允许并行或分块计算。GSVD 确实可以在特定条件下进行块分解。

考虑矩阵 $A$ 和 $B$ 被划分为列块 $A = [A_1, \dots, A_q]$ 和 $B = [B_1, \dots, B_q]$。如果这些块满足特定的[正交性条件](@entry_id:168905)：

$A_i^T A_j = 0 \quad \text{and} \quad B_i^T B_j = 0 \quad \text{for all } i \neq j$

那么，[格拉姆矩阵](@entry_id:203297) $A^T A$ 和 $B^T B$ 都是[块对角矩阵](@entry_id:145530)。这意味着与 GSVD 相关的[广义特征值问题](@entry_id:151614) $(A^T A, B^T B)$ 可以分解为 $q$ 个独立的、规模更小的子问题 $(A_i^T A_i, B_i^T B_i)$。

在这种情况下，GSVD 本身也具有块结构 [@problem_id:3547785]。可逆矩阵 $X$ 可以是[块对角矩阵](@entry_id:145530) $X = \mathrm{diag}(X_1, \dots, X_q)$，其中每个 $X_i$ 来自于对子问题 $(A_i, B_i)$ 的 GSVD。核心矩阵 $\Sigma_A$ 和 $\Sigma_B$ 也是块[对角形式](@entry_id:264850)。全局的[广义奇异值](@entry_id:749794)集合是所有子问题[广义奇异值](@entry_id:749794)集合的并集。

这种解耦性质在计算上极为有利。它意味着我们可以独立地（例如在不同的处理器上）计算每个块 $(A_i, B_i)$ 的 GSVD，然后将结果（主要是 $X_i$）组合起来。全局的耦合仅体现在通常是稠密的酉矩阵 $U$ 和 $V$ 中，它们负责行变换。这为设计高效的并行 GSVD 算法提供了理论基础。