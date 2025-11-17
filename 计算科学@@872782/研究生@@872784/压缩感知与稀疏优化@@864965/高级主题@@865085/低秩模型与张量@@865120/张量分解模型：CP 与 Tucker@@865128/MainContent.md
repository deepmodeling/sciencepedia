## 引言
[张量分解](@entry_id:173366)是分析多维（或多路）数据的核心工具，而 CANDECOMP/[PARAFAC](@entry_id:753095) (CP) 分解和 Tucker 分解是该领域最基础的两大基石。这些模型为从复杂的高维数据集中提取有意义的结构和潜在模式提供了强大的数学框架。然而，尽管它们被广泛应用，但对于其核心原理、不同的结构假设、以及在实践中的权衡取舍，往往缺乏一个系统性的比较和深入的理解。本文旨在填补这一知识空白，为读者提供一个关于这两种基础张量模型的全面视角。

为了实现这一目标，本文将引导读者逐步深入。在“原理与机制”一章中，我们将深入探讨 CP 和 Tucker 分解的数学基础，剖析它们的定义、代数性质、唯一性条件和计算方法，并对比它们在表示不同类型数据结构时的优劣。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些理论如何在信号处理、机器学习、医学成像和地球物理等多个学科领域中解决现实世界的问题。最后，“动手实践”部分将通过具体的练习，帮助读者巩固对自由度、唯一性条件等关键概念的理解。通过这种结构化的学习路径，本文旨在为读者在理论和实践层面全面掌握这两种关键的[张量分解](@entry_id:173366)模型。

## 原理与机制

本章旨在系统性地阐述两种基础的[张量分解](@entry_id:173366)模型：CANDECOMP/[PARAFAC](@entry_id:753095) (CP) 分解和 Tucker 分解。我们将从定义其核心数学构造入手，深入探讨它们各自的代数性质、内在不确定性、模型复杂性，并比较它们在表示[高维数据](@entry_id:138874)时所捕捉的不同结构。最后，我们将讨论与这些模型相关的关键计算方法及其所面临的挑战，为后续章节中基于[稀疏优化](@entry_id:166698)的[张量分析](@entry_id:161423)方法奠定理论基础。

### 张量操作的基础：[矩阵化](@entry_id:751739)与[向量化](@entry_id:193244)

为了处理和分析张量，我们经常需要将其重塑为矩阵或向量，这一过程分别称为**[矩阵化](@entry_id:751739) (matricization)** 或**展开 (unfolding)**，以及**[向量化](@entry_id:193244) (vectorization)**。这些操作是连接多线性代数与传统线性代数的桥梁，对于理解分解算法至关重要。

考虑一个 $N$ 阶张量 $\mathcal{X} \in \mathbb{R}^{I_1 \times I_2 \times \cdots \times I_N}$，其元素由一组索引 $(i_1, i_2, \ldots, i_N)$ 唯一确定。

**张量纤维 (Fibers)** 是通过固定除一个索引外的所有索引而得到的向量。例如，一个**模式-n 纤维 (mode-n fiber)** 是通过固定所有索引 $i_k$ ($k \neq n$) 并让 $i_n$ 变化而形成的向量。它是张量沿第 $n$ 个模式的一维切片。

**模式-n [矩阵化](@entry_id:751739)**，记作 $\mathbf{X}_{(n)}$，是将张量 $\mathcal{X}$ 重排为一个矩阵的过程。在此矩阵中，所有的模式-n 纤维被[排列](@entry_id:136432)成列。具体而言，索引 $i_n$ 映射到矩阵的行，而所有其他 $N-1$ 个索引 $(i_1, \ldots, i_{n-1}, i_{n+1}, \ldots, i_N)$ 被线性化后映射到矩阵的列。因此，$\mathbf{X}_{(n)}$ 的维度为 $I_n \times (I_1 \cdots I_{n-1} I_{n+1} \cdots I_N)$，即 $I_n \times \prod_{k \neq n} I_k$。

为了确保这种映射是明确的，我们必须指定一个索引排序约定。在本书中，我们遵循**[列主序](@entry_id:637645) (column-major order)** 或**字典序 (lexicographic order)**，其中第一个索引 $i_1$ 变化最快，最后一个索引 $i_N$ 变化最慢。根据此约定 [@problem_id:3485656]：
-   张量元素 $\mathcal{X}(i_1, \ldots, i_N)$ 在矩阵 $\mathbf{X}_{(n)}$ 中的位置为 $(r, c)$，其中行索引为 $r = i_n$。
-   列索引 $c$ 由剩余索引 $(i_1, \ldots, i_{n-1}, i_{n+1}, \ldots, i_N)$ 的字典序位置确定。若令 $p: \{1, \ldots, N-1\} \to \{1, \ldots, N\} \setminus \{n\}$ 是一个保持升序的索引映射，则列索引 $c$ (假设为 1-based 索引) 的计算公式为：
    $$
    c = 1 + \sum_{u=1}^{N-1} (i_{p(u)} - 1) \prod_{v=1}^{u-1} I_{p(v)}
    $$
    其中空积定义为 1。

**[向量化](@entry_id:193244)**，记作 $\mathrm{vec}(\mathcal{X})$，则是将张量的所有元素按预定顺序堆叠成一个长向量。遵循同样的[列主序](@entry_id:637645)，$\mathrm{vec}(\mathcal{X})$ 的维度为 $(\prod_{k=1}^N I_k) \times 1$。元素 $\mathcal{X}(i_1, \ldots, i_N)$ 在向量中的线性索引 $\ell$ 为：
$$
\ell = 1 + \sum_{k=1}^N (i_k - 1) \prod_{m=1}^{k-1} I_m
$$

概念上，[矩阵化](@entry_id:751739) $\mathbf{X}_{(n)}$ 的目的是将张量数据重新组织，以突出其沿特定模式 $n$ 的向量结构，这对于模式相关的矩阵运算（如在[交替最小二乘法](@entry_id:746387)中）至关重要。而[向量化](@entry_id:193244) $\mathrm{vec}(\mathcal{X})$ 则完全“压平”了张量的多维结构，在处理涉及[克罗内克积](@entry_id:182766)或[哈达玛积](@entry_id:182073)的代数关系时非常有用。值得注意的是，$\mathrm{vec}(\mathbf{X}_{(n)})$（即对展开矩阵进行向量化）通常与 $\mathrm{vec}(\mathcal{X})$ 不同，它们之间仅相差一个固定的[置换](@entry_id:136432)关系，除非 $n=1$（在我们的[列主序](@entry_id:637645)约定下）。

### CANDECOMP/[PARAFAC](@entry_id:753095) (CP) 分解

CP 分解，亦称为典范多线性分解 (Canonical Polyadic Decomposition)，将一个[张量表示](@entry_id:180492)为一系列**秩-1 (rank-1)** 张量的和。一个秩-1张量可以表示为若干向量的外积。

#### 定义与 CP 秩

对于一个三阶张量 $\mathcal{X} \in \mathbb{R}^{I \times J \times K}$，其秩为 $R$ 的 CP 分解形式为：
$$
\mathcal{X} = \sum_{r=1}^R a_r \circ b_r \circ c_r
$$
其中 $a_r \in \mathbb{R}^I, b_r \in \mathbb{R}^J, c_r \in \mathbb{R}^K$ 是因子向量，$\circ$ 表示向量[外积](@entry_id:147029)。这个模型可以用三个**因子矩阵 (factor matrices)** $A = [a_1, \ldots, a_R] \in \mathbb{R}^{I \times R}$, $B = [b_1, \ldots, b_R] \in \mathbb{R}^{J \times R}$, 和 $C = [c_1, \ldots, c_R] \in \mathbb{R}^{K \times R}$ 简洁地表示。

张量 $\mathcal{X}$ 的 **CP 秩 (CP rank)**，记作 $\mathrm{rank}_{\text{CP}}(\mathcal{X})$，是能够**精确**表示 $\mathcal{X}$ 所需的最少秩-1分量的数量 $R$ [@problem_id:3485653]。与[矩阵秩](@entry_id:153017)不同，[张量秩](@entry_id:266558)的计算是一个 NP-hard 问题，且在[实数域](@entry_id:151347)上的最佳低秩近似问题可能是不适定的 (ill-posed)。

#### 不确定性与唯一性

CP 分解具有内在的**不确定性 (indeterminacies)**，即使在唯一性条件满足时也是如此 [@problem_id:3485653]。

1.  **缩放不确定性 (Scaling Indeterminacy)**：对于任何一个秩-1分量 $a_r \circ b_r \circ c_r$，我们可以用非零标量 $\alpha_r, \beta_r, \gamma_r$ 重新缩放其因子向量，只要它们的乘积为 1，即 $\alpha_r \beta_r \gamma_r = 1$。
    $$
    a_r \circ b_r \circ c_r = (\alpha_r a_r) \circ (\beta_r b_r) \circ (\gamma_r c_r)
    $$
    这种变换可以独立地应用于每个分量。使用因子矩阵，这对应于 $(A, B, C) \to (A D_1, B D_2, C D_3)$，其中 $D_1, D_2, D_3$ 是对角矩阵，其对角元素满足元素级乘积 $\alpha \odot \beta \odot \gamma = \mathbf{1}_R$。

2.  **[置换](@entry_id:136432)不确定性 (Permutation Indeterminacy)**：求和的顺序是任意的。我们可以同时[置换](@entry_id:136432)三个因子矩阵的列，而总和保持不变。这对应于 $(A, B, C) \to (A\Pi, B\Pi, C\Pi)$，其中 $\Pi$ 是一个 $R \times R$ 的[置换矩阵](@entry_id:136841)。

尽管存在这些不确定性，但在满足某些条件下，CP 分解本质上是唯一的。一个著名的充分条件是 **Kruskal 定理**。该定理指出，如果因子矩阵 $A, B, C$ 的 **[Kruskal 秩](@entry_id:751064) (k-rank)**（即任意 $k$ 个列向量[线性无关](@entry_id:148207)的最大 $k$ 值）$k_A, k_B, k_C$ 满足：
$$
k_A + k_B + k_C \ge 2R + 2
$$
则 CP 分解在计入上述缩放和[置换](@entry_id:136432)不确定性后是唯一的。

当 Kruskal 条件不满足时，CP 分解可能不是唯一的。例如，考虑一个 $R=2$ 的分解，其中因子矩阵 $C$ 的两列相同，即 $c_1=c_2=c$。此时 $k_C=1$，即使 $k_A=2, k_B=2$，Kruskal 条件 $2+2+1 = 5$ 未能满足 $2R+2 = 2(2)+2 = 6$ 的要求，因此唯一性不被保证。事实上，可以构造出无穷多个不同的因[子集](@entry_id:261956)来表示同一个张量 [@problem_id:3485686]。例如，对于任何标量 $t$，新的因子 $(A', B', C')$ 定义为：
$$
a_1' = a_1 + t a_2, \quad b_1' = b_1, \quad c_1' = c
$$
$$
a_2' = a_2, \quad b_2' = b_2 - t b_1, \quad c_2' = c
$$
它们生成的张量与原始张量完全相同，因为附加项 $t(a_2 \circ b_1 \circ c)$ 和 $-t(a_2 \circ b_1 \circ c)$ 相互抵消了。

#### 自由度

一个模型的**自由度 (degrees of freedom, DoF)** 指的是其参数空间在剔除连续的重[参数化](@entry_id:272587)对称性后的维度。对于一个秩为 $R$ 的三阶 CP 模型，其自由度的计算如下 [@problem_id:3485670]：
1.  **初始参数计数**：三个因子矩阵 $A, B, C$ 的总参数数量为 $IR + JR + KR = R(I+J+K)$。
2.  **[连续对称性](@entry_id:137257)导致的冗余**：对于 $R$ 个分量中的每一个，缩放不确定性 $\alpha_r \beta_r \gamma_r = 1$ 引入了三个标量和一重约束。这意味着每个分量存在一个二维的连续变换族（例如，自由选择 $\alpha_r$ 和 $\beta_r$，$\gamma_r$ 则被确定），这些变换不改变模型。因此，总的冗[余维](@entry_id:273141)度为 $2R$。
3.  **[置换对称性](@entry_id:185825)的影响**：[置换](@entry_id:136432)是一种**离散**对称性。它在[参数空间](@entry_id:178581)中将有限个点等同起来，但不会形成连续的等价路径。因此，它不减少参数空间的局部维度，即自由度。

综上，CP 模型的自由度为：
$$
\text{DoF}_{\text{CP}} = R(I+J+K) - 2R = R(I+J+K-2)
$$

### Tucker 分解

Tucker 分解，也称为高阶主成分分析 (Higher-Order PCA)，将一个[张量表示](@entry_id:180492)为一个**[核心张量](@entry_id:747891) (core tensor)** 与每个模式下的一个因子矩阵的乘积。

#### 定义与多线性秩

一个 $N$ 阶张量 $\mathcal{X} \in \mathbb{R}^{I_1 \times \cdots \times I_N}$ 的 Tucker 分解形式为：
$$
\mathcal{X} = \mathcal{G} \times_1 U_1 \times_2 U_2 \cdots \times_N U_N
$$
其中 $\mathcal{G} \in \mathbb{R}^{r_1 \times \cdots \times r_N}$ 是[核心张量](@entry_id:747891)，而 $U_n \in \mathbb{R}^{I_n \times r_n}$ 是第 $n$ 个模式的因子矩阵。$\times_n$ 表示**模式-n 乘积 (mode-n product)**，即张量与矩阵的乘法。

Tucker 分解的“大小”或“秩”由一个元组 $(r_1, \ldots, r_N)$ 描述，这被称为张量的**多线性秩 (multilinear rank)**。$r_n$ 是第 $n$ 个模式的[子空间](@entry_id:150286)的维度，其等于模式-n 展开[矩阵的秩](@entry_id:155507)，即 $r_n = \mathrm{rank}(\mathbf{X}_{(n)})$。

#### 可识别性与正交约束

与 CP 分解类似，Tucker 分解也存在可识别性问题 [@problem_id:3485669]。
1.  **无约束情况**：如果对因子矩阵 $U_n$ 和[核心张量](@entry_id:747891) $\mathcal{G}$ 不加任何约束，那么对于任意一组可逆矩阵 $Q_n \in \mathbb{R}^{r_n \times r_n}$，变换
    $$
    \tilde{U}_n = U_n Q_n, \quad \tilde{\mathcal{G}} = \mathcal{G} \times_1 Q_1^{-1} \times_2 Q_2^{-1} \cdots \times_N Q_N^{-1}
    $$
    会生成完全相同的张量 $\mathcal{X}$。这种由任意[可逆矩阵](@entry_id:171829)（代表缩放、旋转、反射和剪切）引起的模糊性意味着因子和核心在没有额外约束的情况下是无法唯一确定的。

2.  **正交约束情况**：为了解决这种模糊性，通常会对因子矩阵施加**列正交约束 (column orthonormality)**，即 $U_n^\top U_n = I_{r_n}$。在这种情况下，[变换矩阵](@entry_id:151616) $Q_n$ 必须满足 $(U_n Q_n)^\top (U_n Q_n) = Q_n^\top U_n^\top U_n Q_n = Q_n^\top Q_n = I_{r_n}$。这意味着 $Q_n$ 必须是**正交矩阵**。因此，施加正交约束消除了任意缩放和剪切的模糊性，但保留了旋转和反射的自由度。

为了完全确定分解，还需要对[核心张量](@entry_id:747891) $\mathcal{G}$ 施加规范化条件，例如**[高阶奇异值分解 (HOSVD)](@entry_id:750334)** 所产生的[核心张量](@entry_id:747891)，它要求[核心张量](@entry_id:747891)是**全正交的** (all-orthogonal，即任何模式的切片都相互正交) 并且是**有序的** (ordered，例如切片的范数按降序[排列](@entry_id:136432))。施加这些条件后，剩余的模糊性通常会减少为离散的符号和[置换](@entry_id:136432)模糊性。

#### 自由度 (正交情况)

在一个具有正交因子矩阵的 Tucker 模型中，自由度的计算需要考虑[核心张量](@entry_id:747891)和每个因子矩阵的参数 [@problem_id:3485662]。
1.  **[核心张量](@entry_id:747891)**：[核心张量](@entry_id:747891) $\mathcal{G} \in \mathbb{R}^{r_1 \times \cdots \times r_N}$ 是无约束的，其自由度为 $r_1 r_2 \cdots r_N$。
2.  **因子矩阵**：每个因子矩阵 $U_n \in \mathbb{R}^{I_n \times r_n}$ 的列是正交的。这类矩阵构成的空间称为**斯蒂菲尔[流形](@entry_id:153038) (Stiefel manifold)** $\mathrm{St}(I_n, r_n)$。其维度（即自由度）可以通过从总参数 $I_n r_n$ 中减去正交性约束的数量来计算。约束 $U_n^\top U_n = I_{r_n}$ 是一个[对称矩阵](@entry_id:143130)等式，因此包含 $r_n(r_n+1)/2$ 个独立的标量约束。所以，每个因子矩阵的自由度为 $I_n r_n - \frac{r_n(r_n+1)}{2}$。

因此，正交 Tucker 模型的总自由度为：
$$
\text{DoF}_{\text{Tucker}} = r_1 r_2 \cdots r_N + \sum_{n=1}^N \left( I_n r_n - \frac{r_n(r_n+1)}{2} \right)
$$

### CP 与 Tucker 模型的比较

CP 和 Tucker 分解提供了两种看待张量结构的不同视角，它们之间的关系和差异是理解[张量分析](@entry_id:161423)的关键。

#### CP 秩 vs. 多线性秩

一个基本关系是，张量的 CP 秩总是大于或等于其多线性秩的任何一个分量：
$$
\mathrm{rank}_{\text{CP}}(\mathcal{X}) \ge \max(r_1, r_2, \ldots, r_N)
$$
然而，CP 秩可能远大于多线性秩。一个经典的例子可以说明这一点 [@problem_id:3485666]。考虑一个由三个秩-1分量构成的 $2 \times 2 \times 2$ 张量 $\mathcal{T}$，其切片为：
$$
\mathcal{T}(:,:,1) = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} \quad \text{和} \quad \mathcal{T}(:,:,2) = \begin{pmatrix} 0  1 \\ -1  0 \end{pmatrix}
$$
-   **多线性秩**：通过分析因子向量的张成空间，可以确定其多线性秩为 $(2, 2, 2)$，这是 $2 \times 2 \times 2$ 张量所能达到的最大值。
-   **CP 秩**：由于 $\mathcal{T}$ 是由 3 个秩-1项之和构造的，其 CP 秩至多为 3。为了确定它是否能由 2 个秩-1项表示，我们考察其切片构成的[矩阵束](@entry_id:751760) (matrix pencil)：
$$
\mathbf{S}_1 - t\mathbf{S}_2 = \begin{pmatrix} 1  -t \\ t  1 \end{pmatrix}
$$
其[行列式](@entry_id:142978)为 $1+t^2$。因为方程 $1+t^2=0$ 在实数域上无解，所以这个[矩阵束](@entry_id:751760)中不存在秩为 1 的矩阵。根据一个关键定理，一个 $2 \times 2 \times 2$ 张量的 CP 秩为 2 当且仅当其切片构成的[矩阵束](@entry_id:751760)的[行列式](@entry_id:142978)方程有实数根。因此，$\mathcal{T}$ 的 CP 秩不能为 2，必须为 3。

这个例子清楚地表明，一个张量可以具有很高的多线性秩，但其 CP 秩甚至更高，揭示了两种“秩”概念的根本区别。

#### 结构解释与凸代理

CP 和 Tucker 模型捕捉了不同类型的张量结构。
-   **CP 模型**寻找一种**多线性组合 (polyadic)** 结构，即张量是否可以被分解为少数几个简单的、可分离的交互项之和。
-   **Tucker 模型**则寻找一种**[子空间](@entry_id:150286) (subspace)** 结构，即张量的数据是否主要位于每个模式下的一个低维[子空间](@entry_id:150286)中。

一个张量可能在一个模型下是“简单”的，而在另一个模型下是“复杂”的。考虑“对角”张量 $\mathcal{X} = \mathbf{e}_1 \otimes \mathbf{e}_1 \otimes \mathbf{e}_1 + \mathbf{e}_2 \otimes \mathbf{e}_2 \otimes \mathbf{e}_2 \in \mathbb{R}^{2 \times 2 \times 2}$ [@problem_id:3485673]。
-   从 CP 的角度看，这个张量非常简单，其 CP 秩为 2。其对应的**CP [原子范数](@entry_id:746563) (CP atomic norm)**，作为 CP 秩的凸代理，值为 2。
-   从 Tucker 的角度看，这个张量的所有模式展开矩阵 $\mathbf{X}_{(n)}$ 都是 $2 \times 4$ 的满秩矩阵，即其多线性秩为 $(2,2,2)$，是可能的最大值。这导致其**重叠迹范数 (overlapped trace norm)** $\sum_n \|\mathbf{X}_{(n)}\|_\ast$（作为多线性秩之和的凸代理）很大，值为 $2+2+2=6$。

这个例子中，两个凸代理范数之比为 $6/2 = 3$，显著地说明了两种模型假设的差异。CP 模型适合表示具有稀疏秩-1分量结构的张量，而 Tucker 模型更适合数据可以由低维[子空间](@entry_id:150286)良好近似的情况。

### 计算方面与挑战

#### [交替最小二乘法](@entry_id:746387) (ALS)

[交替最小二乘法](@entry_id:746387) (ALS) 是计算 CP 和 Tucker 分解最常用的算法之一。其思想是循环地优化一个因子矩阵，同时固定其他所有因子矩阵。对于 CP 分解，更新因子矩阵 $A$ 的子问题是：
$$
\min_A \left\| \mathcal{X} - \sum_{r=1}^R a_r \circ b_r \circ c_r \right\|_F^2
$$
利用模式-1 [矩阵化](@entry_id:751739)，这个问题可以写成一个标准的线性[最小二乘问题](@entry_id:164198)：
$$
\min_A \left\| \mathbf{X}_{(1)} - A (C \odot B)^\top \right\|_F^2
$$
其中 $\odot$ 表示 **Khatri-Rao 积**（矩阵的逐列 [Kronecker 积](@entry_id:156298)）。该问题的[正规方程](@entry_id:142238)为：
$$
A \left((C \odot B)^\top (C \odot B)\right) = \mathbf{X}_{(1)} (C \odot B)
$$
一个关键的恒等式是 [@problem_id:3485665]：
$$
(C \odot B)^\top (C \odot B) = (C^\top C) * (B^\top B)
$$
其中 $*$ 表示 **Hadamard 积**（矩阵的元素级乘积）。这个恒等式可以通过逐元素验证 $(c_r \otimes b_r)^\top (c_s \otimes b_s) = (c_r^\top c_s)(b_r^\top b_s)$ 来证明。

因此，假设逆矩阵存在，ALS 对因子矩阵 $A$ 的更新法则为：
$$
A \leftarrow \mathbf{X}_{(1)} (C \odot B) \left( (C^\top C) * (B^\top B) \right)^{-1}
$$
因子矩阵 $B$ 和 $C$ 的更新可以类似地通过[循环置换](@entry_id:272913)模式得到。

#### CP 分解的[不适定性](@entry_id:635673)与退化

与矩阵分解不同，低秩张量集合在 Frobenius 范数拓扑下不是[闭集](@entry_id:136446)。这意味着一个秩大于 $R$ 的张量可以是一个秩为 $R$ 的张量[序列的极限](@entry_id:159239)。因此，寻找最佳低秩 CP 近似的问题可能是**不适定的 (ill-posed)**。

在实践中，这表现为一种称为**退化 (degeneracy)** 或 **沼泽 (swamping)** 的现象。在迭代逼近目标张量的过程中，算法可能陷入一个区域，其中目标函数的下降变得极其缓慢，而因子矩阵的范数却趋向于无穷大。这是因为模型试图用两个或多个范数巨大但几乎相互抵消的秩-1分量来拟合数据 [@problem_id:3485668]。

一个典型的例子是，一个秩为 2 的序列 $X(t) = \frac{1}{t}((u+tv)^{\otimes 3} - u^{\otimes 3})$。当 $t \to 0^+$ 时，
-   $X(t)$ 趋向于一个秩为 3 的张量 $T = u \otimes u \otimes v + u \otimes v \otimes u + v \otimes u \otimes u$。
-   近似误差 $\|T-X(t)\|_F^2$ 按 $\mathcal{O}(t^2)$ 的速率减小，例如，其极限 $\lim_{t \to 0^+} \|T-X(t)\|_F^2 / (2t^2) = 3/2$。
-   同时，两个秩-1分量的权重 $\pm 1/t$ 趋于无穷，而因子向量 $u+tv$ 和 $u$ 变得几乎共线。

这种近[共线性](@entry_id:270224)导致 ALS 子问题中的 Gram 矩阵（如 $(C^\top C) * (B^\top B)$）变得病态（其[条件数](@entry_id:145150)可能按 $\mathcal{O}(t^{-2})$ 发散），使得[正规方程](@entry_id:142238)的求解极其不稳定，从而导致算法收敛极其缓慢，在[目标函数](@entry_id:267263)值上形成“平台期”。相比之下，Tucker 模型由于其可行集是[闭集](@entry_id:136446)，不存在这类退化问题。