## 引言
不变[子空间](@entry_id:150286)是线性代数和[算子理论](@entry_id:139990)中的一个核心概念，它为分析复杂的线性变换提供了一个强大的简化工具。通过将算子的作用限制在特定的[子空间](@entry_id:150286)上，我们可以将其结构分解并独立研究，从而揭示其内在的谱特性。然而，在实际的数值计算中，不变[子空间](@entry_id:150286)的识别、计算及其在存在舍入误差和数据扰动时的稳定性，构成了一个核心挑战，特别是对于[非正规矩阵](@entry_id:752668)。本文旨在系统性地阐述不变[子空间](@entry_id:150286)的理论、计算及其应用，填补纯粹理论与数值实践之间的鸿沟。

本文将分三个章节展开。第一章“原理与机制”将深入探讨不变[子空间的基](@entry_id:160685)本定义、结构定理（如主分解定理）、摄动理论（如Davis-Kahan定理）以及[非正规性](@entry_id:752585)带来的数值挑战。第二章“应用与跨学科联系”将展示不变[子空间](@entry_id:150286)如何在[QR算法](@entry_id:145597)、[克雷洛夫子空间方法](@entry_id:144111)等核心[数值算法](@entry_id:752770)中发挥作用，并探讨其在控制理论、[结构力学](@entry_id:276699)和[量子信息](@entry_id:137721)等领域的深刻联系。最后，在“动手实践”部分，您将通过具体的编程和分析练习，将理论知识转化为解决实际问题的能力。让我们从不变[子空间的基](@entry_id:160685)本原理开始，逐步揭开其神秘的面纱。

## 原理与机制

在理解和分析线性变换时，一个核心策略是将其分解为更简单的部分。不变[子空间](@entry_id:150286)为实现这一目标提供了基本的框架。一个线性算子在不变[子空间](@entry_id:150286)上的作用可以被隔离和独立研究，这极大地简化了其整体结构的分析。本章将深入探讨不变[子空间](@entry_id:150286)的定义、其结构定理、在摄动下的行为，以及与[非正规性](@entry_id:752585)相关的数值挑战。

### [不变性](@entry_id:140168)的基本概念

一个线性算子在[向量空间](@entry_id:151108)中的作用，可以通过其如何变换特定[子空间](@entry_id:150286)来理解。其中最重要的一类[子空间](@entry_id:150286)就是那些在算子作用下“封闭”的[子空间](@entry_id:150286)。

#### 定义与直接推论

设 $A \in \mathbb{C}^{n \times n}$ 是一个作用于 $\mathbb{C}^n$ 的线性算子。一个[子空间](@entry_id:150286) $\mathcal{S} \subseteq \mathbb{C}^n$ 被称为 **$A$-不变[子空间](@entry_id:150286)**（$A$-invariant subspace），如果对于 $\mathcal{S}$ 中的任意向量 $x$，其像 $Ax$ 仍然在 $\mathcal{S}$ 中。用集合论的语言来说，就是 $A(\mathcal{S}) \subseteq \mathcal{S}$ 。

这个定义虽然简单，但其蕴含的意义却十分深远。不变[子空间](@entry_id:150286)的存在允许我们将算子 $A$ 的作用进行分解。假设 $\mathcal{S}$ 是一个 $k$ 维的 $A$-不变[子空间](@entry_id:150286)，其中 $1 \le k \lt n$。我们可以构建一个特殊的基来揭示这种分解结构。令 $\{u_1, \dots, u_k\}$ 是 $\mathcal{S}$ 的一组基，并将其扩展为 $\mathbb{C}^n$ 的一组基 $\{u_1, \dots, u_k, v_1, \dots, v_{n-k}\}$。令矩阵 $T$ 的列由这些[基向量](@entry_id:199546)构成，即 $T = \begin{pmatrix} U  V \end{pmatrix}$，其中 $U \in \mathbb{C}^{n \times k}$ 的列是 $\mathcal{S}$ 的基，而 $V \in \mathbb{C}^{n \times (n-k)}$ 的列是补充的[基向量](@entry_id:199546)。

由于 $\mathcal{S}$ 是 $A$-不变的，所以 $A$ 作用于 $U$ 的任何一列（即 $\mathcal{S}$ 的一个[基向量](@entry_id:199546)）的结果仍然在 $\mathcal{S}$ 中。这意味着 $AU$ 的每一列都可以表示为 $U$ 的[列的线性组合](@entry_id:150240)。因此，存在一个 $k \times k$ 的矩阵 $A_{11}$，使得 $AU = UA_{11}$。现在，我们来考察相似变换 $T^{-1}AT$：
$$
AT = A \begin{pmatrix} U  V \end{pmatrix} = \begin{pmatrix} AU  AV \end{pmatrix} = \begin{pmatrix} UA_{11}  AV \end{pmatrix}
$$
于是，
$$
T^{-1}AT = T^{-1} \begin{pmatrix} UA_{11}  AV \end{pmatrix} = \begin{pmatrix} T^{-1}UA_{11}  T^{-1}AV \end{pmatrix}
$$
由于 $T^{-1}T = I$，我们可以推断出 $T^{-1}U = \begin{pmatrix} I_k \\ 0 \end{pmatrix}$。因此，变换后的矩阵具有如下的**块上三角形式** ：
$$
T^{-1}AT = \begin{pmatrix} A_{11}  A_{12} \\ 0  A_{22} \end{pmatrix}
$$
其中 $A_{11} \in \mathbb{C}^{k \times k}$，$A_{22} \in \mathbb{C}^{(n-k) \times (n-k)}$，而 $A_{12}$ 是某个矩阵。矩阵 $A_{11}$ 表示的是算子 $A$ 在[子空间](@entry_id:150286) $\mathcal{S}$ 上的限制 $A|_{\mathcal{S}}$ 在基 $\{u_i\}$ 下的表示。这个块上三角结构清晰地表明，算子 $A$ 的谱（[特征值](@entry_id:154894)集合）是其在不变[子空间](@entry_id:150286) $\mathcal{S}$ 上的谱与在[商空间](@entry_id:274314) $\mathbb{C}^n / \mathcal{S}$ 上的谱的并集，即 $\Lambda(A) = \Lambda(A_{11}) \cup \Lambda(A_{22})$。

最简单也是最基本的不变[子空间](@entry_id:150286)是一维的。如果 $\mathcal{S} = \mathrm{span}\{v\}$ 是一个一维 $A$-不变[子空间](@entry_id:150286)（其中 $v \neq 0$），那么根据定义，$Av \in \mathcal{S}$。这意味着 $Av$ 必须是 $v$ 的一个标量倍，即 $Av = \lambda v$ 对于某个标量 $\lambda \in \mathbb{C}$ 成立。这正是**[特征向量](@entry_id:151813)**（eigenvector）的定义。因此，任何非零[特征向量](@entry_id:151813)都张成一个一维的 $A$-不变[子空间](@entry_id:150286) 。

#### 约化[子空间](@entry_id:150286)

一个比[不变性](@entry_id:140168)更强的概念是**约化**（reducing）。一个[子空间](@entry_id:150286) $\mathcal{S}$ 被称为**约化 $A$ 的[子空间](@entry_id:150286)**（subspace that reduces $A$），如果 $\mathcal{S}$ 和其[正交补](@entry_id:149922) $\mathcal{S}^\perp$ 都是 $A$-不变的。

这个条件等价于说，$\mathcal{S}$ 同时被 $A$ 和其伴随算子 $A^*$ 保持不变。这又等价于正交投影算子 $P_\mathcal{S}$ 与 $A$ 可交换，即 $AP_\mathcal{S} = P_\mathcal{S}A$ 。如果 $\mathcal{S}$ 约化 $A$，那么在适应于分解 $\mathbb{C}^n = \mathcal{S} \oplus \mathcal{S}^\perp$ 的一组[标准正交基](@entry_id:147779)下，$A$ 的矩阵表示是块对角的：
$$
A = \begin{pmatrix} A_{11}  0 \\ 0  A_{22} \end{pmatrix}
$$
这表示算子 $A$ 完全分解为两个在正交[子空间](@entry_id:150286)上独立作用的部分。对于[正规矩阵](@entry_id:185943)（即满足 $A^*A = AA^*$ 的矩阵），任何不变[子空间](@entry_id:150286)都是约化[子空间](@entry_id:150286)。这是[正规矩阵](@entry_id:185943)具有良好谱性质的根本原因之一。

### 不变[子空间](@entry_id:150286)的结构

一个给定的线性算子 $A$ 有哪些不变[子空间](@entry_id:150286)？它们的全体构成一个怎样的结构？这个问题通常很复杂，但通过研究一些典型例子和一般性定理，我们可以获得深刻的洞察。

#### 若尔当块的例子

若尔当块是理解[非正规矩阵](@entry_id:752668)行为的基石。考虑一个 $k \times k$ 的若尔当块 $J_k(\lambda) = \lambda I + N$，其中 $N$ 是主超对角线上为1、其余位置为0的[幂零矩阵](@entry_id:152732)。一个[子空间](@entry_id:150286) $\mathcal{S}$ 是 $J_k(\lambda)$-不变的，当且仅当它是 $N$-不变的。

设 $\{e_1, \dots, e_k\}$ 是标准基，其中 $Ne_1=0$ 且 $Ne_i=e_{i-1}$ 对于 $i \ge 2$。可以证明，$J_k(\lambda)$ 的所有不变[子空间](@entry_id:150286)恰好是如下 $k+1$ 个[子空间](@entry_id:150286) ：
$$
\mathcal{S}_r = \mathrm{span}\{e_1, e_2, \dots, e_r\} \quad \text{for } r = 0, 1, \dots, k
$$
其中 $\mathcal{S}_0 = \{0\}$。这些[子空间](@entry_id:150286)构成一个由包含关系决定的全序集（一条链）：
$$
\{0\} = \mathcal{S}_0 \subset \mathcal{S}_1 \subset \mathcal{S}_2 \subset \dots \subset \mathcal{S}_k = \mathbb{C}^k
$$
对于每个维度 $r \in \{0, \dots, k\}$，都恰好存在一个 $r$ 维的不变[子空间](@entry_id:150286)。这个例子清晰地表明，[非正规矩阵](@entry_id:752668)（当 $k1$ 时）的不变[子空间](@entry_id:150286)结构可能非常“稀疏”和刚性。

#### 主分解定理

对于一般的矩阵 $A$，其不变[子空间](@entry_id:150286)的结构可以通过其最小多项式来完全刻画。这就是**主分解定理**（Primary Decomposition Theorem）的内容。

设 $A \in \mathbb{C}^{n \times n}$ 的[最小多项式](@entry_id:153598)为 $m_A(t)$。在复数域上，它可以分解为互异线性因子的幂的乘积：
$$
m_A(t) = \prod_{j=1}^{r} (t - \lambda_j)^{\alpha_j}
$$
其中 $\lambda_j$ 是 $A$ 的互异[特征值](@entry_id:154894)。对于每个 $j$，我们定义**广义[特征空间](@entry_id:638014)**（generalized eigenspace）或**主分量**（primary component）为：
$$
\mathcal{K}_j = \ker\bigl((A - \lambda_j I)^{\alpha_j}\bigr)
$$
主分解定理断言，整个空间 $\mathbb{C}^n$ 可以被分解为这些广义[特征空间](@entry_id:638014)的[直和](@entry_id:156782)：
$$
\mathbb{C}^n = \bigoplus_{j=1}^{r} \mathcal{K}_j
$$
并且，每个 $\mathcal{K}_j$ 都是一个 $A$-不变[子空间](@entry_id:150286)。

这个分解的机制源于多项式环 $\mathbb{C}[t]$ 的代数性质 。令 $p_j(t) = (t - \lambda_j)^{\alpha_j}$。由于这些多项式 $p_j(t)$ [两两互素](@entry_id:154147)，根据扩展的[欧几里得算法](@entry_id:138330)（或贝祖等式），存在多项式 $a_j(t)$ 使得 $\sum_{j=1}^r a_j(t) \frac{m_A(t)}{p_j(t)} = 1$。将矩阵 $A$ 代入此恒等式，可以构造出一族投影算子 $P_j$。这些[投影算子](@entry_id:154142)满足 $P_j^2 = P_j$，$P_j P_k = 0$（当 $j \neq k$），以及 $\sum_{j=1}^r P_j = I$。更重要的是，每个[投影算子](@entry_id:154142) $P_j$ 的值域恰好是广义[特征空间](@entry_id:638014) $\mathcal{K}_j$。这一族[投影算子](@entry_id:154142)因此提供了将[空间分解](@entry_id:755142)为不变[子空间](@entry_id:150286)[直和](@entry_id:156782)的精确机制。

这个定理是深刻的，因为它将一个算子的复杂结构分解为在各个（可能较小的）不变[子空间](@entry_id:150286)上的更简单的结构。在每个 $\mathcal{K}_j$ 上，算子 $A$ 的作用可以表示为 $\lambda_j I + N_j$，其中 $N_j$ 是一个[幂零算子](@entry_id:148875)。

### 奇异[子空间](@entry_id:150286)与[奇异值分解](@entry_id:138057)

不变[子空间](@entry_id:150286)的概念与[特征值分解](@entry_id:272091)紧密相关。类似地，我们可以为[奇异值分解](@entry_id:138057)（SVD）定义一个平行的概念：奇异[子空间](@entry_id:150286)。

对于任意矩阵 $A \in \mathbb{C}^{m \times n}$，矩阵 $A^*A$（$n \times n$）和 $AA^*$（$m \times m$）都是埃尔米特且半正定的。它们的非零[特征值](@entry_id:154894)是相同的。$A$ 的[奇异值](@entry_id:152907) $\sigma$ 定义为这些共同的非零[特征值](@entry_id:154894)的正平方根，再加上适量的零。

与 $A$ 的[奇异值](@entry_id:152907)的一个[子集](@entry_id:261956) $\Gamma \subset [0, \infty)$ 相关联，我们可以定义**右奇异[子空间](@entry_id:150286)** $V_\Gamma$ 和**左奇异[子空间](@entry_id:150286)** $U_\Gamma$ 。
- **右奇异[子空间](@entry_id:150286) $V_\Gamma$** 是 $A^*A$ 的不变[子空间](@entry_id:150286)，对应于[特征值](@entry_id:154894)集合 $\{\sigma^2 \mid \sigma \in \Gamma\}$。
- **左奇异[子空间](@entry_id:150286) $U_\Gamma$** 是 $AA^*$ 的不变[子空间](@entry_id:150286)，也对应于[特征值](@entry_id:154894)集合 $\{\sigma^2 \mid \sigma \in \Gamma\}$。

这些[子空间](@entry_id:150286)之间存在着优美的几何关系，这正是 SVD 的核心：
1.  $A$ 将右奇异[子空间](@entry_id:150286) $V_\Gamma$ 映射到左奇异[子空间](@entry_id:150286) $U_\Gamma$ 内（$A(V_\Gamma) \subseteq U_\Gamma$）。
2.  $A^*$ 将左奇异[子空间](@entry_id:150286) $U_\Gamma$ 映射到右奇异[子空间](@entry_id:150286) $V_\Gamma$ 内（$A^*(U_\Gamma) \subseteq V_\Gamma$）。

这是因为如果 $v$ 是 $A^*A$ 的[特征向量](@entry_id:151813)，对应[特征值](@entry_id:154894)为 $\lambda \neq 0$（即 $A^*Av = \lambda v$），那么 $Av$ 就是 $AA^*$ 的[特征向量](@entry_id:151813)，对应相同的[特征值](@entry_id:154894) $\lambda$：
$$
(AA^*)(Av) = A(A^*Av) = A(\lambda v) = \lambda (Av)
$$
因此，$Av$ 位于由 $\lambda$ 所属的 $AA^*$ 的谱[子空间](@entry_id:150286)中。

如果 $\Gamma$ 不包含 $0$，那么映射 $A: V_\Gamma \to U_\Gamma$ 是一个同构，这意味着这两个[子空间](@entry_id:150286)的维数相等 。这个性质是 SVD 存在性的基础，并为低秩逼近等应用提供了几何解释。

### 摄动理论与数值稳定性

在数值计算中，我们处理的矩阵几乎总是带有误差或摄动。一个核心问题是：当矩阵 $A$ 发生微小变化（$A \to \tilde{A} = A+E$）时，它的不变[子空间](@entry_id:150286)会如何变化？不变[子空间](@entry_id:150286)的摄动理论是[数值线性代数](@entry_id:144418)的基石之一。

#### [子空间](@entry_id:150286)之间的距离

要量化不变[子空间](@entry_id:150286)的变化，我们首先需要一种方法来度量两个[子空间](@entry_id:150286)之间的“距离”。设 $\mathcal{U}$ 和 $\mathcal{V}$ 是 $\mathbb{C}^n$ 中两个相同维度 $r$ 的[子空间](@entry_id:150286)。它们之间的相对方向可以通过一组**主角度**（principal angles）$\theta_1, \dots, \theta_r \in [0, \pi/2]$ 来刻画。

这些角度可以通过一个变分过程来定义，但一个等价且在计算上更直接的方法是利用标准正交基。设 $U$ 和 $V$ 是列向量构成 $\mathcal{U}$ 和 $\mathcal{V}$ [标准正交基](@entry_id:147779)的矩阵。那么，主角度的余弦值 $\cos\theta_i$ 就是矩阵 $U^*V$ 的奇异值 。

对于摄动分析，更有用的是主角度的正弦值。矩阵 $\sin\Theta(\mathcal{U}, \mathcal{V})$ 是一个对角矩阵，其对角元为 $\sin\theta_i$。它的范数，特别是[谱范数](@entry_id:143091) $\|\sin\Theta(\mathcal{U}, \mathcal{V})\|_2 = \max_i \sin\theta_i$，在[子空间](@entry_id:150286)构成的格拉斯曼[流形](@entry_id:153038)上定义了一个度量（距离）。这个距离等于一个[子空间的基](@entry_id:160685)在另一个[子空间](@entry_id:150286)的[正交补](@entry_id:149922)上的投影范数，也等于两个[正交投影](@entry_id:144168)算子之差的[谱范数](@entry_id:143091)：
$$
d(\mathcal{U}, \mathcal{V}) = \|\sin\Theta(\mathcal{U}, \mathcal{V})\|_2 = \|(I - P_{\mathcal{U}})V\|_2 = \|P_{\mathcal{U}} - P_{\mathcal{V}}\|_2
$$
这个等式为抽象的[子空间距离](@entry_id:198307)提供了一个具体的、可计算的表示。

#### Davis-Kahan 定理

有了度量[子空间距离](@entry_id:198307)的工具，我们就可以陈述摄动理论中的一个里程碑式的成果——**Davis-Kahan $\sin\Theta$ 定理**。该定理为[埃尔米特矩阵](@entry_id:155147)的不变[子空间](@entry_id:150286)摄动提供了简洁而深刻的[上界](@entry_id:274738)。

设 $A$ 是一个埃尔米特矩阵，其谱被分为两个不相交的部分，两者之间的最小距离（谱间隙）为 $\delta  0$。设 $\mathcal{U}$ 是与其中一部分谱相关联的 $A$-不变[子空间](@entry_id:150286)。考虑一个摄动矩阵 $\tilde{A} = A+E$（其中 $E$ 也是埃尔米特矩阵），并设 $\tilde{\mathcal{U}}$ 是 $\tilde{A}$ 的对应不变[子空间](@entry_id:150286)。Davis-Kahan 定理给出了这两个[子空间](@entry_id:150286)之间距离的一个[上界](@entry_id:274738) ：
$$
\|\sin\Theta(\mathcal{U}, \tilde{\mathcal{U}})\|_{2} \le \frac{\|E\|_{2}}{\delta}
$$
这个不等式表明，不变[子空间](@entry_id:150286)的稳定性由两个因素决定：摄动的大小 $\|E\|$ 和谱的**分离程度** $\delta$。如果谱间隙 $\delta$ 很大，那么即使有中等大小的摄动，不变[子空间](@entry_id:150286)也相对稳定。相反，如果谱间隙很小（即[特征值](@entry_id:154894)聚集），那么即使是微小的摄动也可能导致不变[子空间](@entry_id:150286)的剧烈变化。

对于非埃尔米特矩阵，情况更为复杂。类似的上界仍然存在，但谱间隙 $\delta$ 需要被一个更复杂的量——**谱块分离度**（separation of spectral blocks），记为 $\mathrm{sep}(T_{11}, T_{22})$——所取代。这个量衡量了求解[西尔维斯特方程](@entry_id:155720) $T_{11}X - XT_{22} = Y$ 的算子的最小[奇异值](@entry_id:152907) 。一个典型的界形如：
$$
\|\tan\Theta(\mathcal{U}, \tilde{\mathcal{U}})\|_{\mathrm{F}} \le \frac{\|E_{21}\|_{\mathrm{F}}}{\mathrm{sep}(T_{11}, T_{22})}
$$
其中 $\| \cdot \|_{\mathrm{F}}$ 是[弗罗贝尼乌斯范数](@entry_id:143384)，$E_{21}$ 是摄动矩阵在相应分块下的非对角块。这个界同样强调了谱分离的重要性，但其形式和所依赖的量都比埃尔米特情况复杂。

### [非正规性](@entry_id:752585)的挑战

为什么非[埃尔米特矩阵](@entry_id:155147)的摄动理论更复杂？根本原因在于**[非正规性](@entry_id:752585)**（non-normality）。

#### 左右不变[子空间](@entry_id:150286)与[条件数](@entry_id:145150)

对于[非正规矩阵](@entry_id:752668)，与单个[特征值](@entry_id:154894) $\lambda$ 相关联的右不变[子空间](@entry_id:150286)（由右[特征向量](@entry_id:151813)张成，满足 $Ax = \lambda x$）和左不变[子空间](@entry_id:150286)（由左[特征向量](@entry_id:151813)张成，满足 $y^*A = \lambda y^*$）通常是不同的。它们之间的夹角是衡量[非正规性](@entry_id:752585)的一个指标。

对于一个单[特征值](@entry_id:154894) $\lambda_1$，其对应的（一维）不变[子空间](@entry_id:150286)的**[条件数](@entry_id:145150)** $\kappa_{\mathrm{vec}}$ 定义为左右[特征向量](@entry_id:151813) $x$ 和 $y$ 之间夹角 $\varphi$ 的余弦的倒数 ：
$$
\kappa_{\mathrm{vec}} = \frac{1}{\cos\varphi} = \frac{\|x\|_2 \|y\|_2}{|y^*x|}
$$
对于[正规矩阵](@entry_id:185943)，左右[特征向量](@entry_id:151813)是相同的，所以 $\varphi=0$ 且 $\kappa_{\mathrm{vec}}=1$。然而，对于[非正规矩阵](@entry_id:752668)，这个角度可以非常接近 $\pi/2$，导致[条件数](@entry_id:145150)变得极大。例如，对于矩阵 $A_\alpha = \begin{pmatrix} 1  \alpha \\ 0  -1 \end{pmatrix}$，[特征值](@entry_id:154894) $\lambda=1$ 的[条件数](@entry_id:145150)是 $\kappa_{\mathrm{vec}}(\alpha) = \sqrt{4+\alpha^2}/2$。当非正规项 $|\alpha|$ 增大时，[条件数](@entry_id:145150)可以无界增长 。

这个条件数直接影响摄动界。一个更精细的摄动界表明，不变[子空间](@entry_id:150286)的敏感性正比于这个[条件数](@entry_id:145150)，反比于谱间隙。巨大的条件数意味着即使谱间隙很大，[子空间](@entry_id:150286)也可能对微小摄动极其敏感。

#### 伪谱

理解[非正规性](@entry_id:752585)影响的一个强大现代工具是**$\varepsilon$-伪谱**（$\varepsilon$-pseudospectrum）。矩阵 $A$ 的 $\varepsilon$-[伪谱](@entry_id:138878) $\Lambda_\varepsilon(A)$ 定义为所有复数 $z$ 的集合，这些 $z$ 使得矩阵 $A-zI$ 的最小[奇异值](@entry_id:152907) $\sigma_{\min}(A-zI)$ 小于或等于 $\varepsilon$。等价地，它是使求逆算子（或称 resolvent）范数 $\|(A-zI)^{-1}\|_2$ 大于或等于 $1/\varepsilon$ 的点集 。

- 对于[正规矩阵](@entry_id:185943)，$\Lambda_\varepsilon(A)$ 就是以其[特征值](@entry_id:154894)为中心、半径为 $\varepsilon$ 的圆盘的并集。
- 对于[非正规矩阵](@entry_id:752668)，[伪谱](@entry_id:138878)区域可能会非常大，远远超出这些小圆盘的范围，并可能将谱中相距遥远的[特征值](@entry_id:154894)连接起来。

[伪谱](@entry_id:138878)的这种“膨胀”和“融合”现象直观地揭示了[非正规矩阵](@entry_id:752668)的敏感性。如果两个[特征值](@entry_id:154894) $\lambda_1$ 和 $\lambda_2$ 的伪谱区域在某个较小的 $\varepsilon$ 水平下就融合在一起，这表明将这两个[特征值](@entry_id:154894)对应的[谱投影](@entry_id:265201)和不变[子空间](@entry_id:150286)分离开来是数值上不稳定的 。计算不变[子空间](@entry_id:150286)的算法，如 Arnoldi 方法，可能会产生所谓的**[伪特征值](@entry_id:749897)**（spurious eigenvalues），它们实际上是位于[伪谱](@entry_id:138878)中具有大求逆[算子范数](@entry_id:752960)的点，而非真实的[特征值](@entry_id:154894)。

为了在实践中区分真实的谱信息和由[非正规性](@entry_id:752585)引起的虚假信息，可以设计更精细的测试。例如，可以计算一个 Ritz 对 $(\theta, x)$ 的归一化残差 $q(\theta,x) = \frac{\|Ax-\theta x\|_2}{\sigma_{\min}(\theta I - A)}$，并将其与一个依赖于矩阵非正规度（如亨里奇非正规度 $\delta(A)$）的自适应阈值进行比较 。这种方法将本章讨论的多个概念——残差、求逆[算子范数](@entry_id:752960)（通过 $\sigma_{\min}$ 体现）和[非正规性](@entry_id:752585)度量——结合起来，为评估数值计算结果的可靠性提供了一个强大的机制。

总之，不变[子空间](@entry_id:150286)为理解和计算[线性变换](@entry_id:149133)提供了基础的理论框架。然而，从数值的角度看，其稳定性和可计算性严重依赖于[算子的谱](@entry_id:272027)分离度和正规性。对这些原理的深刻理解对于设计和分析可靠的[数值算法](@entry_id:752770)至关重要。