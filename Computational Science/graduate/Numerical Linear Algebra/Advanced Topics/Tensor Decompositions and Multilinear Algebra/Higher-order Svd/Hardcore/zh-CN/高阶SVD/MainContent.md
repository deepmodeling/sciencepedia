## 引言
随着数据科学的进步，处理多维数组（即张量）的能力变得至关重要。[高阶奇异值分解](@entry_id:197696)（Higher-Order Singular Value Decomposition, [HOSVD](@entry_id:197696)），也称[Tucker分解](@entry_id:182831)，正是为此而生的一种强大数学工具。它将经典的矩阵奇异值分解（SVD）推广到了更高维度，为分析复杂的[多维数据](@entry_id:189051)结构提供了核心框架。

然而，从矩阵到张量的跃升并非一帆风顺。许多对矩阵SVD的直观理解在[HOSVD](@entry_id:197696)中不再适用，例如其在低秩逼近上的最优性保证。理解[HOSVD](@entry_id:197696)独特的数学性质、应用优势及其与矩阵SVD的关键区别，是有效利用这一工具的关键。

本文旨在系统性地构建读者对[HOSVD](@entry_id:197696)的全面理解。我们将分为三个部分：首先，在“原理与机制”一章中，我们将深入其多线性代数的数学核心，建立算法并剖析其关键性质。接着，在“应用与跨学科联系”一章中，我们将通过来自计算科学、神经科学乃至量子物理的实例，展示[HOSVD](@entry_id:197696)在真实世界问题中的强大威力。最后，“动手实践”部分将提供一系列精心设计的练习，帮助您将理论知识转化为实践技能。

通过这趟从理论到实践的旅程，读者将不仅掌握[HOSVD](@entry_id:197696)的计算方法，更能深刻领会其在现代数据分析工具箱中的核心地位。

## 原理与机制

本章在前一章介绍张量基本概念的基础上，深入探讨[高阶奇异值分解](@entry_id:197696)（Higher-Order Singular Value Decomposition, [HOSVD](@entry_id:197696)）的数学原理与核心机制。[HOSVD](@entry_id:197696) 是将矩阵[奇异值分解](@entry_id:138057)（SVD）推广到多维数组（即张量）的一种重要方法，它在数据压缩、[特征提取](@entry_id:164394)和[模式识别](@entry_id:140015)等领域扮演着关键角色。我们将从其代数基础出发，系统地建立 [HOSVD](@entry_id:197696) 的定义、算法和性质，并辨析其与矩阵 SVD 的关键差异。

### 多线性代数的基础：模-n积与展开

要理解 [HOSVD](@entry_id:197696)，必须首先掌握两种基本张量运算：**模-n 积（mode-n product）**和**模-n 展开（mode-n unfolding）**，后者也常被称为**[矩阵化](@entry_id:751739)（matricization）**。

**模-n 积** 是一个张量与一个矩阵之间的乘法。对于一个 $N$ 阶张量 $\mathcal{X} \in \mathbb{R}^{I_1 \times I_2 \times \cdots \times I_N}$ 和一个矩阵 $U \in \mathbb{R}^{J \times I_n}$，它们沿第 $n$ 模的乘积结果为一个新的张量 $\mathcal{Y} = \mathcal{X} \times_n U$，其维度为 $\mathbb{R}^{I_1 \times \cdots \times I_{n-1} \times J \times I_{n+1} \times \cdots \times I_N}$。从概念上讲，这个运算将张量 $\mathcal{X}$ 的每一个**模-n 纤维（mode-n fiber）**（即固定除第 $n$ 个以外所有索引得到的一维向量）视为一个列向量，并用矩阵 $U$ 左乘它。

我们可以推导出其坐标表达式 。张量 $\mathcal{Y}$ 的每一个元素 $(i_1, \dots, i_{n-1}, j, i_{n+1}, \dots, i_N)$ 是通过将 $\mathcal{X}$ 沿其第 $n$ 模与矩阵 $U$ 的第 $j$ 行进行[线性组合](@entry_id:154743)得到的：
$$
\mathcal{Y}(i_1, \dots, i_{n-1}, j, i_{n+1}, \dots, i_N) = \sum_{i_n=1}^{I_n} U_{j,i_n} \mathcal{X}(i_1, \dots, i_{n-1}, i_n, i_{n+1}, \dots, i_N)
$$
这个公式揭示了模-n 积的本质：它在张量的特定模式上进行线性变换，而保持其他模式的结构不变。

**模-n 展开** 则是将[高阶张量](@entry_id:200122)“压平”成一个矩阵的过程。张量 $\mathcal{X}$ 的模-n 展开，记作 $X_{(n)}$，是一个 $I_n \times (I_1 \cdots I_{n-1} I_{n+1} \cdots I_N)$ 的矩阵。该矩阵的每一列是 $\mathcal{X}$ 的一个模-n 纤维。为了保证展开的唯一性，通常采用一种固定的顺序（如[字典序](@entry_id:143032)）来[排列](@entry_id:136432)这些纤维。

例如，考虑一个三阶张量 $\mathcal{T} \in \mathbb{R}^{2 \times 2 \times 2}$ ，其元素由两个 $2 \times 2$ 的正面切片（frontal slices）定义：
$$
T_{:,:,1} = \begin{pmatrix} 4.0 & 5.5 \\ 2.0 & 6.5 \end{pmatrix}, \quad T_{:,:,2} = \begin{pmatrix} -2.0 & 3.5 \\ 4.0 & 0.5 \end{pmatrix}
$$
其**模-1 展开** $T_{(1)}$ 是一个 $2 \times 4$ 的矩阵。它的列由模-1 纤维（即张量的“列”）构成。按字典序[排列](@entry_id:136432)索引对 $(i_2, i_3)$：$(1,1), (2,1), (1,2), (2,2)$，我们得到 $T_{(1)}$ 的四个列向量：
- 第1列 ($i_2=1, i_3=1$): $(t_{111}, t_{211})^\top = (4.0, 2.0)^\top$
- 第2列 ($i_2=2, i_3=1$): $(t_{121}, t_{221})^\top = (5.5, 6.5)^\top$
- 第3列 ($i_2=1, i_3=2$): $(t_{112}, t_{212})^\top = (-2.0, 4.0)^\top$
- 第4列 ($i_2=2, i_3=2$): $(t_{122}, t_{222})^\top = (3.5, 0.5)^\top$

于是，模-1 展开矩阵为：
$$
T_{(1)} = \begin{pmatrix} 4.0 & 5.5 & -2.0 & 3.5 \\ 2.0 & 6.5 & 4.0 & 0.5 \end{pmatrix}
$$
模-n 积和模-n 展开之间存在一个关键的代数关系，它构成了 [HOSVD](@entry_id:197696) 理论的基石：
$$
(\mathcal{X} \times_n U)_{(n)} = U X_{(n)}
$$
这个等式表明，对一个张量进行模-n 积运算，等价于对其模-n 展开矩阵进行标准的矩阵左乘。

### [高阶奇异值分解 (HOSVD)](@entry_id:750334) 的定义与算法

[HOSVD](@entry_id:197696)，也称为 **Tucker 分解**，将一个张量 $\mathcal{X}$ 表示为一个**[核心张量](@entry_id:747891)（core tensor）** $\mathcal{S}$ 与一系列**因子矩阵（factor matrices）** $U^{(n)}$ 的模-n 积：
$$
\mathcal{X} = \mathcal{S} \times_1 U^{(1)} \times_2 U^{(2)} \cdots \times_N U^{(N)}
$$
其中，$\mathcal{X} \in \mathbb{R}^{I_1 \times \cdots \times I_N}$，[核心张量](@entry_id:747891) $\mathcal{S} \in \mathbb{R}^{I_1 \times \cdots \times I_N}$，因子矩阵 $U^{(n)} \in \mathbb{R}^{I_n \times I_n}$ 是一组[正交矩阵](@entry_id:169220)。

标准 [HOSVD](@entry_id:197696) 算法的计算过程如下 ：
1.  **计算因子矩阵**：对于每一个模式 $n \in \{1, \dots, N\}$：
    a.  构建张量 $\mathcal{X}$ 的模-n 展开矩阵 $X_{(n)}$。
    b.  对 $X_{(n)}$ 进行矩阵[奇异值分解](@entry_id:138057)：$X_{(n)} = U^{(n)} \Sigma^{(n)} (V^{(n)})^\top$。
    c.  因子矩阵 $U^{(n)}$ 即为 SVD 得到的[左奇异向量](@entry_id:751233)矩阵。

2.  **计算[核心张量](@entry_id:747891)**：由于所有因子矩阵 $U^{(n)}$ 都是正交的（$(U^{(n)})^\top U^{(n)} = I$），我们可以通过对原始张量 $\mathcal{X}$ 进行逆向变换来求得[核心张量](@entry_id:747891) $\mathcal{S}$：
    $$
    \mathcal{S} = \mathcal{X} \times_1 (U^{(1)})^\top \times_2 (U^{(2)})^\top \cdots \times_N (U^{(N)})^\top
    $$
这个过程提供了一种系统地分解任何[高阶张量](@entry_id:200122)的方法。[HOSVD](@entry_id:197696) 将原始数据中的多维交互结构分离到[核心张量](@entry_id:747891) $\mathcal{S}$ 中，而将每个模式内的主要方向（或基）提炼到因子矩阵 $U^{(n)}$ 中。

### [HOSVD](@entry_id:197696) 的核心性质

[HOSVD](@entry_id:197696) 具有一系列重要的数学性质，这些性质揭示了其结构和内涵。

#### 能量保持性：范数不变

张量的**[弗罗贝尼乌斯范数](@entry_id:143384)（Frobenius norm）**，定义为所有元素平方和的平方根，$\|\mathcal{X}\|_F = \sqrt{\sum_{i_1, \dots, i_N} x_{i_1 \dots i_N}^2}$，通常被视为张量的总“能量”。[HOSVD](@entry_id:197696) 分解是一个保范数的变换，即原始张量和[核心张量](@entry_id:747891)的[弗罗贝尼乌斯范数](@entry_id:143384)相等  ：
$$
\|\mathcal{X}\|_F = \|\mathcal{S}\|_F
$$
这个性质源于模-n 积的等距性。当因子矩阵 $U^{(n)}$ 是正交（或列正交）时，模-n 积不会改变张量的[弗罗贝尼乌斯范数](@entry_id:143384)。由于 [HOSVD](@entry_id:197696) 的所有因子矩阵都是正交的，从 $\mathcal{X}$ 到 $\mathcal{S}$ 的变换以及其逆变换都是保范数的。

#### [核心张量](@entry_id:747891)的全正交性

对于矩阵 SVD，$A = U\Sigma V^\top$，其“核心”（即奇异值矩阵 $\Sigma$）是对角的。[HOSVD](@entry_id:197696) 的[核心张量](@entry_id:747891) $\mathcal{S}$ 通常不是对角的，但它满足一个较弱的性质，称为**全正交性（all-orthogonality）**。

全正交性意味着，对于任何一个模式 $n$，将[核心张量](@entry_id:747891) $\mathcal{S}$ 按第 $n$ 个索引切分成的一组子张量是相互正交的。这在代数上等价于，[核心张量](@entry_id:747891)的模-n 展开 $S_{(n)}$ 满足 $S_{(n)} S_{(n)}^\top$ 是一个对角矩阵 [@problem_id:3549397, Part A]。更具体地，这个[对角矩阵](@entry_id:637782)的对角元是张量 $\mathcal{X}$ 的**模-n 奇异值**的平方：
$$
S_{(n)} S_{(n)}^\top = \Sigma^{(n)} (\Sigma^{(n)})^\top = \mathrm{diag}((\sigma_1^{(n)})^2, (\sigma_2^{(n)})^2, \dots, (\sigma_{I_n}^{(n)})^2)
$$
其中 $\sigma_i^{(n)}$ 是 $X_{(n)}$ 的奇异值。这一性质可以通过 [HOSVD](@entry_id:197696) 的定义推导得出。我们有 $X_{(n)} = U^{(n)} S_{(n)} (U^{(N)} \otimes \cdots \otimes U^{(n+1)} \otimes U^{(n-1)} \otimes \cdots \otimes U^{(1)})^\top$。由于 $U^{(n)}$ 和由克罗内克积构成的矩阵都是正交的，可得 $S_{(n)} = (U^{(n)})^\top X_{(n)} U_{(-n)}$，其中 $U_{(-n)}$ 是正交的。因此，$S_{(n)} S_{(n)}^\top = (U^{(n)})^\top X_{(n)} X_{(n)}^\top U^{(n)}$。代入 $X_{(n)} X_{(n)}^\top = U^{(n)} \Sigma^{(n)} (\Sigma^{(n)})^\top (U^{(n)})^\top$ 即可证明此性质。

这个性质是 [HOSVD](@entry_id:197696) 的一个标志。[核心张量](@entry_id:747891) $\mathcal{S}$ 的非对角元素描述了不同模式[基向量](@entry_id:199546)之间的交互强度。如果[核心张量](@entry_id:747891)是对角的，则意味着张量可以分解为一组不相关的“主成分”；如果非对角元素很大，则表明模式之间存在复杂的多线性耦合。

#### 多线性秩

与矩阵的秩相对应，张量有**多线性秩（multilinear rank）**的概念。一个张量 $\mathcal{X}$ 的多线性秩被定义为其各个模式展开[矩阵的秩](@entry_id:155507)所组成的元组：
$$
\mathrm{rank}_{ML}(\mathcal{X}) = (\mathrm{rank}(X_{(1)}), \mathrm{rank}(X_{(2)}), \dots, \mathrm{rank}(X_{(N)}))
$$
我们可以通过一个[核心张量](@entry_id:747891) $\mathcal{G} \in \mathbb{R}^{r_1 \times \cdots \times r_N}$ 和一组列正交的因子矩阵 $A^{(n)} \in \mathbb{R}^{I_n \times r_n}$ 来构造一个具有特定多线性秩 $(r_1, \dots, r_N)$ 的张量 $\mathcal{X}$ 。只要[核心张量](@entry_id:747891) $\mathcal{G}$ 本身是“满”的（即其自身的多线性秩为 $(r_1, \dots, r_N)$），那么构造出的张量 $\mathcal{X} = \mathcal{G} \times_1 A^{(1)} \cdots \times_N A^{(N)}$ 的多线性秩就是 $(r_1, \dots, r_N)$。这是因为 $\mathcal{X}$ 的第 $n$ 模的列空间恰好是 $A^{(n)}$ 的列空间，其维度为 $r_n$。

#### 唯一性与旋转自由度

[HOSVD](@entry_id:197696) 的唯一性比矩阵 SVD 更为复杂。对于矩阵 SVD，如果所有[奇异值](@entry_id:152907)都是唯一的，则[奇异向量](@entry_id:143538)唯一确定（不计符号变化）。对于 [HOSVD](@entry_id:197696)，如果张量的所有模-n [奇异值](@entry_id:152907)都是唯一的，则相应的因子矩阵 $U^{(n)}$ 的列向量也唯一确定（不计符号变化）。这种符号上的不确定性会传递给[核心张量](@entry_id:747891)，导致其相应模式的切片也发生符号翻转 [@problem_id:3549397, Part D]。

然而，一个更深刻的非唯一性来源是当模-n [奇异值](@entry_id:152907)出现重合时。考虑一个特殊构造的张量 $\mathcal{X} \in \mathbb{R}^{2 \times 2 \times 2}$ ，其模-1 和模-2 展开矩阵 $X_{(1)}$ 和 $X_{(2)}$ 的奇异值谱均由两个相等的[奇异值](@entry_id:152907)构成。这意味着 $X_{(1)}X_{(1)}^\top$ 和 $X_{(2)}X_{(2)}^\top$ 都是[单位矩阵](@entry_id:156724)的倍数。在这种情况下，任何一组标准正交基都可以作为[左奇异向量](@entry_id:751233)。因此，对应的因子矩阵 $U^{(1)}$ 和 $U^{(2)}$ 可以是任意的 $2 \times 2$ 正交矩阵，例如任意的旋转矩阵 $R(\theta)$ 和 $R(\phi)$。这种选择的自由度意味着 [HOSVD](@entry_id:197696) 分解不是唯一的，而是存在一个由参数 $(\theta, \phi)$ 描述的分解族。[核心张量](@entry_id:747891) $\mathcal{S}$ 也依赖于这些参数，$\mathcal{S} = \mathcal{S}(\theta, \phi)$。这揭示了 [HOSVD](@entry_id:197696) 的一个重要特征：当某个模式的[奇异谱](@entry_id:183789)出现简并时，相应的因子矩阵存在旋转自由度，[核心张量](@entry_id:747891)的结构也会随之连续变化。

### [HOSVD](@entry_id:197696) 与矩阵 SVD 的关键区别：截断的次优性

矩阵 SVD 最重要的应用之一是低秩逼近。根据 **Eckart-Young 定理**，对一个矩阵进行截断 SVD（即保留前 $k$ 大的奇异值及其对应的奇异向量）可以得到在[弗罗贝尼乌斯范数](@entry_id:143384)和[谱范数](@entry_id:143091)意义下的最佳 $k$ 秩逼近。

一个普遍的误解是 [HOSVD](@entry_id:197696) 也具有类似的性质。**然而，截断 [HOSVD](@entry_id:197696) 通常不能得到最佳低秩张量逼近**。截断 [HOSVD](@entry_id:197696) 是指通过选取每个因子矩阵 $U^{(n)}$ 的前 $r_n$ 列来构造一个低秩逼近。这种方法虽然简单直观，但其最小化的是 $\sum_{n=1}^N \| X_{(n)} - U^{(n)}_{:,1:r_n} (U^{(n)}_{:,1:r_n})^\top X_{(n)} \|_F^2$ 的和，这并不等价于最小化原始张量的逼近误差 $\| \mathcal{X} - \tilde{\mathcal{X}} \|_F^2$。

我们可以构造一个反例来清晰地说明这一点 。考虑一个 $2 \times 2 \times 2$ 的张量，其大部分能量[分布](@entry_id:182848)在“非对角”位置，例如 $\mathcal{X} = \mathbf{e}_1 \otimes \mathbf{e}_2 \otimes \mathbf{e}_2 + \mathbf{e}_2 \otimes \mathbf{e}_1 \otimes \mathbf{e}_2 + \mathbf{e}_2 \otimes \mathbf{e}_2 \otimes \mathbf{e}_1$ (加上一个微小的扰动项)。对该张量进行 [HOSVD](@entry_id:197696)，会发现每个模式的主导[奇异向量](@entry_id:143538)都是 $\mathbf{e}_2$。因此，截断 [HOSVD](@entry_id:197696) 得到的秩-$(1,1,1)$ 逼近所张成的空间是 $\mathbf{e}_2 \otimes \mathbf{e}_2 \otimes \mathbf{e}_2$。然而，原始张量在这个方向上的投影为零。[HOSVD](@entry_id:197696) [核心张量](@entry_id:747891) $\mathcal{S}$ 的能量几乎完全[分布](@entry_id:182848)在非首项元素上。

为了找到最佳的低秩 Tucker 逼近，需要采用迭代[优化算法](@entry_id:147840)，其中最著名的是**高阶正交迭代（Higher-Order Orthogonal Iteration, HOOI）**，也称为 Tucker-ALS。HOOI 算法从 [HOSVD](@entry_id:197696) 的结果出发，交替地更新每一个因子矩阵，使其在固定其他因子矩阵时，能够最大化捕获张量的能量。这个过程最终会收敛到一个（通常是局部的）最优解，其逼近误差小于或等于截断 [HOSVD](@entry_id:197696)。上述反例中，HOOI 能够将因子从 $(\mathbf{e}_2, \mathbf{e}_2, \mathbf{e}_2)$ 旋转到像 $(\mathbf{e}_1, \mathbf{e}_2, \mathbf{e}_2)$ 这样的更优组合，从而捕获更多的能量 。

### [HOSVD](@entry_id:197696) 的高级性质与关系

#### 对称性与[置换](@entry_id:136432)

[HOSVD](@entry_id:197696) 的结构与张量模式的顺序有优雅的协变关系。如果我们对一个张量 $\mathcal{X}$ 的模式进行[置换](@entry_id:136432)，得到一个新的张量 $\mathcal{Y}$，其定义为 $\mathcal{Y}_{i_1, \dots, i_d} = \mathcal{X}_{i_{\pi(1)}, \dots, i_{\pi(d)}}$，其中 $\pi$ 是 $\{1, \dots, d\}$ 的一个[置换](@entry_id:136432)。那么，新张量 $\mathcal{Y}$ 的 [HOSVD](@entry_id:197696) 与原张量 $\mathcal{X}$ 的 [HOSVD](@entry_id:197696) 之间存在一个简单的关系 ：
- $\mathcal{Y}$ 的第 $m$ 个因子矩阵等于 $\mathcal{X}$ 的第 $\pi(m)$ 个因子矩阵：$U_{\mathcal{Y}}^{(m)} = U_{\mathcal{X}}^{(\pi(m))}$。
- $\mathcal{Y}$ 的[核心张量](@entry_id:747891)是 $\mathcal{X}$ 的[核心张量](@entry_id:747891)经过同样模式[置换](@entry_id:136432)的结果：$\mathcal{S}_{\mathcal{Y}} = \mathrm{permute}_{\pi}(\mathcal{S})$。

这一性质表明 [HOSVD](@entry_id:197696) 在结构上是与模式[置换](@entry_id:136432)相容的，进一步体现了其作为一种“自然”的[张量分解](@entry_id:173366)的地位。

#### 与[典范分解](@entry_id:634116)/[多相分解](@entry_id:269253) (CP) 的关系

[HOSVD](@entry_id:197696) (Tucker 分解) 和 CP 分解是两种最主要的[张量分解](@entry_id:173366)方法。它们之间存在深刻的联系 。一个秩为 $R$ 的 CP 分解可以写成 $\mathcal{X} = \sum_{r=1}^R \lambda_r a_r \circ b_r \circ c_r$。
- **多线性秩**：如果 CP 分解的因子矩阵 $A=[a_1, \dots, a_R]$, $B=[b_1, \dots, b_R]$, $C=[c_1, \dots, c_R]$ 都是列满秩的，那么张量 $\mathcal{X}$ 的多线性秩恰好为 $(R,R,R)$ [@problem_id:3549368, Part C]。这意味着 [HOSVD](@entry_id:197696) 截断到秩 $(R,R,R)$ 能够捕获到与 CP 分解相同的[信号子空间](@entry_id:185227)。
- **正交特殊情况**：在一个理想化的场景中，如果 CP 分解的因子矩阵 $A,B,C$ 恰好是列正交的，那么 $\mathcal{X}$ 的 [HOSVD](@entry_id:197696) 因子矩阵 $U^{(1)}, U^{(2)}, U^{(3)}$ 分别就是 $A,B,C$ 的列所张成的空间。其[核心张量](@entry_id:747891) $\mathcal{G} \in \mathbb{R}^{R \times R \times R}$ 将会是一个**超对角（superdiagonal）**张量，其对角线元素为 $\lambda_r$（可能伴有符号和顺序变化）[@problem_id:3549368, Part A]。
- **一般情况与 CP-ALS 初始化**：在一般情况下，CP 因子矩阵并非正交。但如果它们的列向量之间的相关性（即**相干性**）较小，[HOSVD](@entry_id:197696) 得到的[核心张量](@entry_id:747891)依然会是**对角占优**的。这一性质使得 [HOSVD](@entry_id:197696) 成为初始化 CP 分解[迭代算法](@entry_id:160288)（如[交替最小二乘法](@entry_id:746387)，ALS）的有力工具。通过 [HOSVD](@entry_id:197696) 找到[信号子空间](@entry_id:185227)，然后在这个缩小的[子空间](@entry_id:150286)上对[核心张量](@entry_id:747891)进行 CP 分解，可以为 CP-ALS 提供一个良好的初始点，从而加速收敛并有助于避免陷入不良的局部最小值 [@problem_id:3549368, Part D]。然而，这种初始化的稳定性严重依赖于张量模-n [奇异值](@entry_id:152907)的[谱隙](@entry_id:144877)。如果第 $R$ 个奇异值与第 $R+1$ 个奇异值非常接近，那么即使微小的噪声也可能导致计算出的[子空间](@entry_id:150286)发生巨大偏离，从而降低初始化质量 [@problem_id:3549368, Part F]。

### [HOSVD](@entry_id:197696) 的计算考量

尽管 [HOSVD](@entry_id:197696) 在理论上十分优雅，但其直接计算的成本可能非常高昂 。标准 [HOSVD](@entry_id:197696) 算法的计算量主要来自两个部分：
1.  **$N$ 次 SVD**：对每个模-n 展开矩阵 $X_{(n)} \in \mathbb{R}^{I_n \times J_n}$（其中 $J_n = \prod_{m \neq n} I_m$）进行 SVD 的计算成本约为 $\mathcal{O}(\min\{I_n, J_n\} \cdot \max\{I_n, J_n\}^2)$。如果张量的阶数较高或维度较大，展开矩阵的尺寸会急剧增长，导致计算成本非常高。
2.  **$N$ 次模-n 积**：计算[核心张量](@entry_id:747891)需要进行 $N$ 次模-n 积，第 $n$ 次的成本约为 $\mathcal{O}(I_n^2 \prod_{m \neq n} I_m) = \mathcal{O}(I_n \prod_{m=1}^N I_m)$。

将这两部分加总，总的计算成本可以表示为：
$$
C_{\text{total}} = \left(\prod_{m=1}^{N} I_{m}\right) \sum_{n=1}^{N} \left( \max\left\{I_{n}, \prod_{m \neq n} I_{m}\right\} + I_{n} \right)
$$
这个表达式凸显了 [HOSVD](@entry_id:197696) 计算成本对张量维度和阶数的高度敏感性。对于大规模张量，直接计算 [HOSVD](@entry_id:197696) 变得不可行，必须依赖于各种[迭代算法](@entry_id:160288)（如[随机化](@entry_id:198186)方法或上面提到的 HOOI）来近似计算其分解。