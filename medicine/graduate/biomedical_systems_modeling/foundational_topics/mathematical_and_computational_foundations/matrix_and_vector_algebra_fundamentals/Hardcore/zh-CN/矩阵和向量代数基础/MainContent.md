## 引言
在现代生物医学研究中，从[基因组学](@entry_id:138123)到[系统生理学](@entry_id:156175)，我们面临着前所未有的数据复杂性与系统规模。为了从这些海量数据中提取有意义的知识并构建可预测的模型，我们需要一种能够精确描述多变量关系和动态过程的语言。矩阵与[向量代数](@entry_id:152340)正是这样一种基础而强大的数学语言，它为理解、分析和操控复杂的生物医学系统提供了不可或缺的框架。

然而，许多研究者常常在抽象的数学定义与具体的生物学问题之间感到脱节。本文旨在弥合这一差距，不仅仅是罗列公式和定理，而是系统性地阐明矩阵与[向量代数](@entry_id:152340)的核心思想如何直接转化为对生物系统的深刻洞察。我们将展示，这些数学工具并非仅仅是计算的辅助，它们本身就编码了关于系统结构、动态行为和内在约束的根本信息。

在接下来的内容中，读者将踏上一段从理论到实践的旅程。在“**原理与机制**”一章中，我们将从第一性原理出发，建立对向量空间、[矩阵算子](@entry_id:269557)、特征值和[基变换](@entry_id:189626)等核心概念的直观理解。随后，在“**应用与交叉学科联系**”一章，我们将这些抽象原理应用于解决真实世界的生物医学问题，涵盖从[代谢网络分析](@entry_id:270574)到[高维数据](@entry_id:138874)处理的广泛领域。最后，通过“**上手实践**”部分提供的精选练习，您将有机会亲手应用所学知识，巩固并深化对这些强大工具的掌握。

## 原理与机制

在本章中，我们将深入探讨构成[生物医学系统建模](@entry_id:1121641)核心的矩阵与[向量代数](@entry_id:152340)的基本原理和机制。我们将从[向量空间的基](@entry_id:191509)本概念出发，逐步建立描述和分析复杂生物系统的数学框架。我们的方法将侧重于从第一性原理出发进行推导，并将抽象的数学概念与具体的生物医学问题背景紧密联系起来。

### [向量空间](@entry_id:151108)：生物状态的舞台

在[生物医学建模](@entry_id:1121638)中，我们常常需要量化和表示复杂系统的状态。无论是[基因组学](@entry_id:138123)中成千上万个基因的表达水平，还是生理监测中多个[生物传感器](@entry_id:182252)的读数，我们都可以将这些[多维数据](@entry_id:189051)表示为一个向量。这种表示不仅仅是一种数据存储方式，它更将我们带入了一个强大的数学结构——**[向量空间](@entry_id:151108) (vector space)** 的世界。

一个向量，如 $\boldsymbol{v} \in \mathbb{R}^n$，是一个有序的数字列表，可以被看作是 $n$ 维空间中的一个点或一个箭头。这个空间中的向量遵循特定的代数规则，即[向量加法](@entry_id:155045)和[标量乘法](@entry_id:155971)。这两个基本运算的组合构成了**[线性组合](@entry_id:154743) (linear combination)**。给定一组向量 $\{\boldsymbol{v}_1, \boldsymbol{v}_2, \dots, \boldsymbol{v}_k\}$，它们的线性组合具有以下形式：

$$
\boldsymbol{w} = \alpha_1 \boldsymbol{v}_1 + \alpha_2 \boldsymbol{v}_2 + \dots + \alpha_k \boldsymbol{v}_k
$$

其中 $\alpha_1, \alpha_2, \dots, \alpha_k$ 是标量（实数）。这组向量所有可能的线性组合构成的集合称为它们的**张成空间 (span)**，记作 $\operatorname{span}\{\boldsymbol{v}_1, \dots, \boldsymbol{v}_k\}$。这个张成空间本身也是一个[向量空间](@entry_id:151108)（称为原空间的**子空间 (subspace)**），它捕捉了这组向量所能描述的所有可能性。

在生物学研究中，张成空间的概念非常有用。例如，在基因调控网络的研究中，我们可能假设某种特定组织状况下的所有基因表达谱都位于由少数几个潜在的“元基因”向量 $\boldsymbol{v}_1, \boldsymbol{v}_2$ 所张成的[线性子空间](@entry_id:151815)中 。为了验证这一假设，我们需要检验从该组织测得的样本表达向量 $\boldsymbol{s}$ 是否属于 $\operatorname{span}\{\boldsymbol{v}_1, \boldsymbol{v}_2\}$。这等价于求解是否存在标量 $\alpha_1, \alpha_2$ 使得 $\boldsymbol{s} = \alpha_1 \boldsymbol{v}_1 + \alpha_2 \boldsymbol{v}_2$。这个向量方程本质上是一个[线性方程组](@entry_id:148943)。如果该方程组有解，则样本 $\boldsymbol{s}$ 与假设一致；如果无解，则该样本不位于假设的子空间中，可能意味着模型假设有误或该样本是异常值。

例如，假设元基因向量为 $\boldsymbol{v}_1=\begin{pmatrix}1  2  0  1\end{pmatrix}^\top$ 和 $\boldsymbol{v}_2=\begin{pmatrix}0  1  1  1\end{pmatrix}^\top$。一个样本向量 $\boldsymbol{s}_A=\begin{pmatrix}2  5  1  3\end{pmatrix}^\top$ 位于此子空间中，因为我们可以找到系数 $\alpha_1=2, \alpha_2=1$ 使得 $\boldsymbol{s}_A = 2\boldsymbol{v}_1 + 1\boldsymbol{v}_2$。然而，另一个样本 $\boldsymbol{s}_B=\begin{pmatrix}1  3  0  1\end{pmatrix}^\top$ 则不在此子空间中，因为方程组 $\begin{pmatrix}1  3  0  1\end{pmatrix}^\top = \alpha_1\boldsymbol{v}_1 + \alpha_2\boldsymbol{v}_2$ 会导出矛盾的约束（例如，从第一和第三个分量我们得到 $\alpha_1=1, \alpha_2=0$，但这与第二个分量 $3=2\alpha_1+\alpha_2$ 矛盾）。

一个张成空间可以由不同的向量组生成。这就引出了一个核心问题：描述一个子空间最有效的方式是什么？答案在于**基 (basis)** 的概念。一个[向量空间的基](@entry_id:191509)是一组**[线性无关](@entry_id:148207) (linearly independent)** 的向量，并且这些[向量张成](@entry_id:152883)了整个空间。[线性无关](@entry_id:148207)意味着这组向量中没有任何一个是多余的，即没有任何一个向量可以表示为其他向量的[线性组合](@entry_id:154743)。换言之，方程 $\alpha_1 \boldsymbol{v}_1 + \dots + \alpha_k \boldsymbol{v}_k = \boldsymbol{0}$ 仅在所有标量 $\alpha_i$ 都为零时成立。

一个给定子空间的任何一组基都含有相同数量的向量，这个数量被称为该子空间的**维度 (dimension)**。维度是子空间的一个内在属性，它量化了在不离开该子空间的情况下，我们可以在多少个独立方向上移动。在生物医学应用中，维度通常对应于驱动系统变化的独立潜在机制的数量。

为了从一组给定的向量（例如，来自多个实验条件的[生物传感器](@entry_id:182252)读数）中找到它们所张成[子空间的基](@entry_id:160685)和维度，我们可以使用一种系统性的算法——[高斯消元法](@entry_id:153590)。我们将这些向量作为列构成一个矩阵 $\mathbf{A}$，然后通过一系列行变换将其化为**[行阶梯形矩阵](@entry_id:199986) (row echelon form)**。矩阵中主元（每行第一个非零元素）所在的列是[线性无关](@entry_id:148207)的，这些列对应的原始向量就构成了[列空间](@entry_id:156444)的一个基。主元的总数，即[阶梯形](@entry_id:153067)矩阵中非零行的数目，就是该子空间的维度 。

### 矩阵：算子与数据容器

矩阵在线性代数中扮演着双重角色。一方面，它可以作为一个数据容器，将一组向量（如基因表达谱或传感器读数）组织在一起。另一方面，一个矩阵可以被看作是一个**[线性算子](@entry_id:149003) (linear operator)**，它通过矩阵乘法将一个向量从一个[向量空间](@entry_id:151108)映射到另一个（或相同的）[向量空间](@entry_id:151108)。

与任何矩阵 $\mathbf{A} \in \mathbb{R}^{m \times n}$ 相关联的有两个基本的子空间：**[列空间](@entry_id:156444) (column space)** 和 **[零空间](@entry_id:171336) (null space)**。

#### [列空间](@entry_id:156444)与秩

矩阵 $\mathbf{A}$ 的[列空间](@entry_id:156444)，记作 $\operatorname{col}(\mathbf{A})$，是其所有列向量的张成空间。它是在 $\mathbb{R}^m$ 中的一个子空间，代表了通过对 $\mathbf{A}$ 的列进行[线性组合](@entry_id:154743)可以到达的所有向量的集合。换句话说，它是方程 $\mathbf{A}\boldsymbol{x}=\boldsymbol{b}$ 有解的所有可能的 $\boldsymbol{b}$ 的集合。

[列空间](@entry_id:156444)的维度被称为矩阵的**秩 (rank)**，记作 $\operatorname{rank}(\mathbf{A})$。秩是一个极其重要的概念，它量化了矩阵列向量中的[线性无关](@entry_id:148207)向量的最大数目。在生物医学背景下，秩通常揭示了数据背后的“内在维度”或“复杂性”。例如，在一个[信号转导网络](@entry_id:265756)模型中，如果我们用一个矩阵 $C$ 来表示不同通路对网络中边的使用情况，那么 $\operatorname{rank}(C)$ 就代表了[线性无关](@entry_id:148207)的通路使用模式的数量 。如果秩小于通路的总数，则说明某些通路的使用模式是冗余的，可以由其他通路[线性表示](@entry_id:139970)。

同样，如果一个数据矩阵 $X$ 的列代表不同[生物传感器](@entry_id:182252)的测量值，行代表不同实验条件，那么 $\operatorname{rank}(X)$ 则表示驱动这些传感器读数变化的独立生理机制的数量。如果 $p$ 个传感器测量值的[矩阵秩](@entry_id:153017)远小于 $p$，例如 $\operatorname{rank}(X)=2$，这强烈暗示了这 $p$ 个传感器并非在测量 $p$ 个独立的生物过程，而是测量由两个主导的潜在生理机制线性混合而成的信号 。

#### 零空间与[秩-零度定理](@entry_id:154441)

矩阵 $\mathbf{A}$ 的**零空间 (null space)**，也称为**核 (kernel)**，记作 $\ker(\mathbf{A})$，是所有被 $\mathbf{A}$ 映射到[零向量](@entry_id:156189)的向量 $\boldsymbol{x} \in \mathbb{R}^n$ 的集合。也就是说，$\ker(\mathbf{A}) = \{\boldsymbol{x} \in \mathbb{R}^n \mid \mathbf{A}\boldsymbol{x} = \boldsymbol{0}\}$。[零空间](@entry_id:171336)是 $\mathbb{R}^n$ 的一个子空间。

[零空间](@entry_id:171336)在建模中有着深刻的物理意义。例如，在[代谢网络](@entry_id:166711)[稳态分析](@entry_id:271474)（如[通量平衡分析](@entry_id:155597)，FBA）中，核心约束是质量守恒，即 $\mathbf{S}\boldsymbol{v}=\boldsymbol{0}$。这里，$\mathbf{S}$ 是[化学计量矩阵](@entry_id:275342)，$\boldsymbol{v}$ 是反应通量向量。这个方程表明，对于网络中的每种代谢物，其总产生速率等于总消耗速率。因此，所有满足[稳态](@entry_id:139253)条件的通量向量 $\boldsymbol{v}$ 的集合恰好就是[化学计量矩阵](@entry_id:275342) $\mathbf{S}$ 的零空间 。

零空间的维度，称为矩阵的**零度 (nullity)**，代表了解空间的自由度。我们可以通过求解[齐次线性方程组](@entry_id:153432) $\mathbf{A}\boldsymbol{x}=\boldsymbol{0}$ 来找到[零空间](@entry_id:171336)的一组基。这通常通过将 $\mathbf{A}$ 化为**行最简[阶梯形](@entry_id:153067)矩阵 (reduced row echelon form, RREF)** 来完成。与非[主元列](@entry_id:148772)对应的变量成为[自由变量](@entry_id:151663)，我们可以通过这些[自由变量](@entry_id:151663)表示出[主元变量](@entry_id:154928)，从而构造出零空间的一组[基向量](@entry_id:199546)。

秩和[零度](@entry_id:156285)之间存在一个优美的关系，即**[秩-零度定理](@entry_id:154441) (Rank-Nullity Theorem)**：
$$
\operatorname{rank}(\mathbf{A}) + \operatorname{dim}(\ker(\mathbf{A})) = n
$$
其中 $n$ 是矩阵 $\mathbf{A}$ 的列数。这个定理可以理解为一个“维度守恒定律”：矩阵的 $n$ 个输入维度，一部分被映射到非零输出（构成了[列空间](@entry_id:156444)），另一部分则被“压扁”到零（构成了[零空间](@entry_id:171336)）。在代谢网络的例子中，如果 $\mathbf{S}$ 有 $n$ 个反应（列）且秩为 $r$，那么该网络在[稳态](@entry_id:139253)下的自由度就是 $n-r$ 。

### [向量空间](@entry_id:151108)的几何学

到目前为止，我们主要关注了向量空间的[代数结构](@entry_id:137052)。现在，我们引入几何概念，如长度、距离和角度，这将使我们能够更深入地分析数据。

#### [内积](@entry_id:750660)与正交性

几何概念的核心是**[内积](@entry_id:750660) (inner product)**。对于 $\mathbb{R}^n$ 中的两个向量 $\boldsymbol{x}$ 和 $\boldsymbol{y}$，最常见的[内积](@entry_id:750660)是**标准点积 (standard dot product)**：$\boldsymbol{x} \cdot \boldsymbol{y} = \boldsymbol{x}^\top \boldsymbol{y} = \sum_{i=1}^n x_i y_i$。

然而，在许多生物医学应用中，标准点积可能无法完全捕捉问题的本质。例如，当不同[生物标志物](@entry_id:914280)的测量可靠性不同时，我们可能希望赋予更可靠的测量值更大的权重。这可以通过定义一个**[加权内积](@entry_id:163877) (weighted inner product)** 来实现：$\langle \boldsymbol{x}, \boldsymbol{y} \rangle_W = \boldsymbol{x}^\top \mathbf{W} \boldsymbol{y}$，其中 $\mathbf{W}$ 是一个[对称正定矩阵](@entry_id:136714)（我们将在后面详细讨论）。例如，一个对角矩阵 $\mathbf{W}$ 可以为每个分量分配不同的权重 。

[内积](@entry_id:750660)允许我们定义两个关键的几何量：
1.  **范数 (Norm)**：一个[向量的范数](@entry_id:154882)（或长度）由 $\Vert \boldsymbol{x} \Vert = \sqrt{\langle \boldsymbol{x}, \boldsymbol{x} \rangle}$ 定义。它度量了向量的大小。
2.  **正交性 (Orthogonality)**：如果两个非[零向量](@entry_id:156189)的[内积](@entry_id:750660)为零，即 $\langle \boldsymbol{x}, \boldsymbol{y} \rangle = 0$，则称它们是**正交 (orthogonal)** 的。在几何上，这意味着它们相互垂直。

一个由两两正交且范数为1的向量组成的基称为**规范[正交基](@entry_id:264024) (orthonormal basis)**。规范[正交基](@entry_id:264024)在计算上非常方便，因为将一个[向量投影](@entry_id:147046)到基向量上变得异常简单。

如何从任意一组基构造一个规范[正交基](@entry_id:264024)呢？**[格拉姆-施密特过程](@entry_id:141060) (Gram-Schmidt process)** 提供了一种系统性的算法。从一组[线性无关](@entry_id:148207)的向量 $\{\boldsymbol{b}_1, \dots, \boldsymbol{b}_k\}$ 出发，我们逐步构造一个[正交基](@entry_id:264024) $\{\boldsymbol{v}_1, \dots, \boldsymbol{v}_k\}$：
-   $\boldsymbol{v}_1 = \boldsymbol{b}_1$
-   $\boldsymbol{v}_2 = \boldsymbol{b}_2 - \operatorname{proj}_{\boldsymbol{v}_1}(\boldsymbol{b}_2)$
-   $\boldsymbol{v}_3 = \boldsymbol{b}_3 - \operatorname{proj}_{\boldsymbol{v}_1}(\boldsymbol{b}_3) - \operatorname{proj}_{\boldsymbol{v}_2}(\boldsymbol{b}_3)$
-   ...

其中，$\operatorname{proj}_{\boldsymbol{v}}(\boldsymbol{b}) = \frac{\langle \boldsymbol{b}, \boldsymbol{v} \rangle}{\langle \boldsymbol{v}, \boldsymbol{v} \rangle}\boldsymbol{v}$ 是向量 $\boldsymbol{b}$ 在向量 $\boldsymbol{v}$ 上的投影。这个过程的本质是，在构造第 $i$ 个[正交基](@entry_id:264024)向量 $\boldsymbol{v}_i$ 时，我们取原始向量 $\boldsymbol{b}_i$，并减去它在所有已经构造好的[正交向量](@entry_id:142226) $\{\boldsymbol{v}_1, \dots, \boldsymbol{v}_{i-1}\}$ 上的分量，剩下的就是与之前所有向量都正交的部分。最后，我们将每个[正交向量](@entry_id:142226) $\boldsymbol{v}_i$ 进行归一化，即除以其范数 $\Vert\boldsymbol{v}_i\Vert$，便得到规范[正交基](@entry_id:264024)向量 $\boldsymbol{u}_i = \boldsymbol{v}_i / \Vert\boldsymbol{v}_i\Vert$ 。

#### [行列式与体积](@entry_id:192291)

线性变换（由[矩阵表示](@entry_id:146025)）不仅会旋转和拉伸向量，还会改变区域的体积。**行列式 (determinant)** 是一个与方阵关联的标量，它精确地量化了这种体积变化的比例因子。

对于一个 $n \times n$ 矩阵 $\mathbf{A}$，其行列式 $\det(\mathbf{A})$ 定义为由[标准基向量](@entry_id:152417) $\{\boldsymbol{e}_1, \dots, \boldsymbol{e}_n\}$ 张成的单位[超立方体](@entry_id:273913)，在经过 $\mathbf{A}$ 变换后所形成的平行[多面体](@entry_id:637910)（由 $\mathbf{A}$ 的列向量 $\{\mathbf{A}\boldsymbol{e}_1, \dots, \mathbf{A}\boldsymbol{e}_n\}$ 张成）的有向体积。
-   $|\det(\mathbf{A})|$ 的大小表示[体积缩放](@entry_id:197908)的比例。如果 $|\det(\mathbf{A})| > 1$，体积被放大；如果 $|\det(\mathbf{A})|  1$，体积被压缩；如果 $|\det(\mathbf{A})| = 1$，[体积保持](@entry_id:141001)不变。
-   $\det(\mathbf{A})$ 的符号表示方向的变化。如果 $\det(\mathbf{A}) > 0$，变换保持了空间的定向（例如，在三维空间中，保持了“右手法则”）；如果 $\det(\mathbf{A})  0$，变换反转了空间的定向（如同照镜子）。如果 $\det(\mathbf{A})=0$，则变换将空间压缩到一个更低的维度（例如，将一个三维物体压成一个平面或一条线），其体积为零。

在生物医学应用中，行列式可以提供关键的物理洞察。例如，在模拟[心肌](@entry_id:924326)组织的局部变形时，变形梯度矩阵 $\mathbf{A}$ 的行列式描述了组织微元的局部体积变化。如果 $\det(\mathbf{A}) > 1$，表示组织局部扩张或拉伸；如果 $0  \det(\mathbf{A})  1$，表示局部压缩。$\det(\mathbf{A}) > 0$ 保证了变形是物理上可能的，没有发生“内翻外”的现象 。对于上三角或下[三角矩阵](@entry_id:636278)，行列式的计算非常简单，它就是对角线上所有元素的乘积。

### [对称矩阵](@entry_id:143130)、二次型与[特征分解](@entry_id:181333)

[对称矩阵](@entry_id:143130)在[生物医学建模](@entry_id:1121638)中无处不在，它们出现在描述系统能量、协方差结构和[扩散过程](@entry_id:268015)的模型中。它们的特殊属性使得分析变得更加深入和直观。

#### 二次型与[正定矩阵](@entry_id:155546)

一个**二次型 (quadratic form)** 是一个关于向量 $\boldsymbol{x}$ 分量的二次[齐次多项式](@entry_id:178156)，可以紧凑地写为 $q(\boldsymbol{x}) = \boldsymbol{x}^\top \mathbf{Q} \boldsymbol{x}$，其中 $\mathbf{Q}$ 是一个方阵。值得注意的是，二次型的值仅取决于 $\mathbf{Q}$ 的**对称部分** $\mathbf{S} = \frac{1}{2}(\mathbf{Q} + \mathbf{Q}^\top)$，因为对于任何向量 $\boldsymbol{x}$，其与反对称部分的乘积 $\boldsymbol{x}^\top \mathbf{A} \boldsymbol{x}$ 恒为零 。因此，在讨论二次型时，我们通常可以不失[一般性](@entry_id:161765)地假设矩阵是还称的。

二次型的符号（正、负或零）至关重要。这引出了**[正定矩阵](@entry_id:155546) (positive definite matrices)** 的概念：
-   一个[对称矩阵](@entry_id:143130) $\mathbf{S}$ 如果对于所有非[零向量](@entry_id:156189) $\boldsymbol{x}$ 都满足 $\boldsymbol{x}^\top \mathbf{S} \boldsymbol{x} > 0$，则称其为**正定的 (positive definite)**。
-   如果对于所有 $\boldsymbol{x}$ 都满足 $\boldsymbol{x}^\top \mathbf{S} \boldsymbol{x} \ge 0$，则称其为**半正定的 (positive semidefinite)**。

这些概念在物理和[统计模型](@entry_id:165873)中具有核心意义。在生物力学中，一个系统的弹性势能通常由二次型 $E(\boldsymbol{x}) = \frac{1}{2}\boldsymbol{x}^\top \mathbf{Q} \boldsymbol{x}$ 给出。系统的静态稳定性要求在平衡点附近的任何微小变形 $\boldsymbol{x}$ 都会增加势能，即 $E(\boldsymbol{x}) > 0$，这等价于要求 $\mathbf{Q}$ 的对称部分是正定的 。在统计学中，一个随机向量 $\boldsymbol{Z}$ 的[协方差矩阵](@entry_id:139155) $\boldsymbol{\Sigma} = \mathbb{E}[\boldsymbol{Z}\boldsymbol{Z}^\top]$ 必须是半正定的，因为任何线性组合 $a^\top \boldsymbol{Z}$ 的方差 $\operatorname{Var}(a^\top \boldsymbol{Z}) = a^\top \boldsymbol{\Sigma} a$ 必须是非负的。

#### 特征值、[特征向量](@entry_id:151813)与[谱定理](@entry_id:136620)

对于一个线性变换 $\mathbf{A}$，是否存在一些特殊的非[零向量](@entry_id:156189)，使得它们在变换后方向保持不变，仅仅被拉伸或压缩？这些特殊的向量被称为**[特征向量](@entry_id:151813) (eigenvectors)**，而对应的缩放因子被称为**特征值 (eigenvalues)**。它们满足方程：
$$
\mathbf{A}\boldsymbol{v} = \lambda\boldsymbol{v}
$$
其中 $\boldsymbol{v}$ 是[特征向量](@entry_id:151813)，$\lambda$ 是特征值。[特征向量](@entry_id:151813)和特征值揭示了变换的内在几何结构，即变换作用的主要方向和强度。

对于[对称矩阵](@entry_id:143130)，其特征值和[特征向量](@entry_id:151813)具有一些非常优美的性质，这些性质由**[谱定理](@entry_id:136620) (Spectral Theorem)** 概括：一个 $n \times n$ 的[实对称矩阵](@entry_id:192806) $\mathbf{S}$ 具有 $n$ 个实数特征值（不一定不同），并且存在一个由其[特征向量](@entry_id:151813)构成的规范[正交基](@entry_id:264024)。这意味着 $\mathbf{S}$ 可以被**[正交对角化](@entry_id:149411)**，即可以写成 $\mathbf{S} = \mathbf{P}\mathbf{D}\mathbf{P}^\top$ 的形式，其中 $\mathbf{P}$ 是一个[正交矩阵](@entry_id:169220)（其列是规范正交的[特征向量](@entry_id:151813)），$\mathbf{D}$ 是一个对角矩阵（其对角线元素是对应的特征值）。

[谱定理](@entry_id:136620)为我们提供了一个强大的视角来理解二次型。在一个由[对称矩阵](@entry_id:143130) $\mathbf{S}$ 的[特征向量](@entry_id:151813)构成的坐标系中（称为主轴坐标系），二次型 $\boldsymbol{x}^\top \mathbf{S} \boldsymbol{x}$ 的形式变得极为简单。如果 $\boldsymbol{y}$ 是 $\boldsymbol{x}$ 在这个新坐标系下的坐标，那么二次型就分解为：
$$
\boldsymbol{x}^\top \mathbf{S} \boldsymbol{x} = \boldsymbol{y}^\top \mathbf{D} \boldsymbol{y} = \sum_{i=1}^n \lambda_i y_i^2
$$
这个表达式清晰地表明，二次型的值是由特征值 $\lambda_i$ 加权的坐标分量平方和。从这个形式可以立刻看出，一个[对称矩阵](@entry_id:143130)是正定的，当且仅当它的所有特征值都为正；是半正定的，当且仅当它的所有特征值都为非负 。

### 表示与变换

同一个物理或生物实体可以用不同的坐标系统来描述。例如，大脑活动可以用解剖区域（解剖基）来描述，也可以用从功能性磁共振成像（fMRI）中提取的独立功能模式（[功能基](@entry_id:139479)）来描述 。线性代数提供了一套优雅的工具来处理不同表示之间的转换。

#### [基变换](@entry_id:189626)

假设我们有两个基 $B = \{\boldsymbol{b}_1, \dots, \boldsymbol{b}_n\}$ 和 $C = \{\boldsymbol{c}_1, \dots, \boldsymbol{c}_n\}$。任何一个向量 $\boldsymbol{v}$ 在这两个基下都有对应的[坐标向量](@entry_id:153319) $[\boldsymbol{v}]_B$ 和 $[\boldsymbol{v}]_C$。这两个[坐标向量](@entry_id:153319)通过一个可逆的**[基变换矩阵](@entry_id:184480) (change-of-basis matrix)** $\mathbf{P}$ 联系在一起：$[\boldsymbol{v}]_B = \mathbf{P}[\boldsymbol{v}]_C$。矩阵 $\mathbf{P}$ 的列是基 $C$ 中的向量在基 $B$ 下的坐标。

现在，考虑一个[线性算子](@entry_id:149003) $T: V \to V$。它在不同的基下也有不同的[矩阵表示](@entry_id:146025)，$[T]_B$ 和 $[T]_C$。这两个[矩阵表示](@entry_id:146025)的是同一个内在的线性变换，只是从不同的“视角”来看。它们之间的关系可以通过**[相似变换](@entry_id:152935) (similarity transformation)** 来描述：
$$
[T]_C = \mathbf{P}^{-1} [T]_B \mathbf{P}
$$
这个公式允许我们将在一个坐标系下建立的模型（例如，基于解剖连接的神经网络动力学模型 $[T]_B$）转换到另一个更有意义或更方便的坐标系下（例如，功能模式的动力学模型 $[T]_C$），从而揭示系统在不同层面上的行为规律 。

#### [函数的线性无关性](@entry_id:269975)

向量空间的概念可以从有限维的 $\mathbb{R}^n$ 推广到函数构成的无限维空间。例如，在[药代动力学](@entry_id:136480)或示踪剂动力学模型中，每个房室的浓度随时间的变化曲线 $c_r(t)$ 可以被看作是函数空间中的一个“向量”。

我们可以问，一组函数 $\{c_1(t), c_2(t), \dots, c_k(t)\}$ 是否[线性无关](@entry_id:148207)？这个问题的定义与[有限维向量空间](@entry_id:265491)中的定义完全平行：如果方程 $\sum_{r=1}^k \alpha_r c_r(t) = 0$ 对于所有 $t \ge 0$ 都成立的唯一解是所有 $\alpha_r=0$，那么这组函数是[线性无关](@entry_id:148207)的。

在一个[线性时不变系统](@entry_id:178866)中，如果系统矩阵可[对角化](@entry_id:147016)且具有 $k$ 个不同的特征值 $-\lambda_i$，那么每个房室的浓度可以表示为指数衰减函数的[线性组合](@entry_id:154743)：$c_r(t) = \sum_{i=1}^k a_{ri} e^{-\lambda_i t}$。这里，函数集 $\{e^{-\lambda_i t}\}$ 构成了函数空间的一个基。由于 $\lambda_i$ 是互不相同的，这个[指数函数](@entry_id:161417)基是[线性无关](@entry_id:148207)的。然而，观测到的浓度曲线 $\{c_r(t)\}$ 的[线性无关](@entry_id:148207)性，还取决于将指数基混合成浓度曲线的[系数矩阵](@entry_id:151473) $\mathbf{A}=[a_{ri}]$。可以证明，函数集 $\{c_r(t)\}$ [线性无关](@entry_id:148207)的充分必要条件是[系数矩阵](@entry_id:151473) $\mathbf{A}$ 是非奇异的（即可逆的）。这个结论将系统辨识（即从输出确定模型参数）中的一个核心问题与矩阵的代数性质直接联系了起来。