## 引言
从熟悉的笛卡尔坐标系迈向更具普适性的曲线坐标系时，我们面临着一个根本性的挑战：基矢不再是固定不变的。在笛卡尔网格中，基矢在空间中处处相同；但在极坐标、球坐标或任何广义坐标系中，基矢的方向和长度都会随位置而变化。正确理解和处理这些变化的基矢，是掌握张量分析、描述弯曲空间和表达普适物理定律的关键。本文旨在系统性地解决“如何在变化的基底上进行一致的物理和几何描述”这一核心问题，为读者搭建从基础向量代数到高级张量演算的桥梁。

在接下来的内容中，读者将循序渐进地掌握这一主题。我们将在“原理与机制”一章中，从第一性原理出发，定义协变与逆变基矢，揭示它们的几何对偶性，并引入度规张量作为衡量局部空间几何的工具。随后，在“应用与跨学科联系”一章，我们将把这些理论工具应用于解决从经典力学、连续介质力学到广义相对论等不同领域的实际问题，展示其强大的跨学科能力。最后，“动手实践”部分将提供一系列练习，帮助读者将抽象概念转化为具体的计算技能。通过这一结构，本文将带领读者全面理解曲线坐标系中基矢的理论与实践。

## 原理与机制

在从熟悉的笛卡尔坐标系过渡到更普适的曲线坐标系时，我们遇到的第一个根本性转变在于基矢（basis vectors）的概念本身。在笛卡尔坐标系中，基矢（如 $\mathbf{\hat{i}}, \mathbf{\hat{j}}, \mathbf{\hat{k}}$）是恒定不变的：无论我们在空间中的哪个位置，它们都指向相同的方向且长度为1。然而，在曲线坐标系（如极坐标、球坐标或任何自定义的坐标系）中，基矢是局域的（local）且随位置变化的。理解这些变化的基矢的性质和它们之间的关系，是张量分析的核心。本章将系统地阐述协变基矢和逆变基矢的定义、几何意义以及它们在构建物理和几何不变量中的作用。

### 协变基矢：坐标曲线的切线

想象在空间中绘制一个曲线坐标网格。例如，在二维平面上，极坐标系 $(r, \theta)$ 由一系列同心圆（$r = \text{常数}$）和从原点发出的射线（$\theta = \text{常数}$）构成。在任何一点，我们都可以自然地定义一组与这些坐标线相关的方向。

最直观的基矢定义方式，是将其与坐标曲线的切线方向联系起来。如果我们固定除一个坐标 $u^i$ 之外的所有坐标，然后让 $u^i$ 变化，那么空间中的点就会描绘出一条**坐标曲线**。这条曲线上任意一点的切向量，就自然地成为了描述该方向的基矢。

形式上，如果一个点的位置矢量 $\mathbf{r}$ 是曲线坐标 $(u^1, u^2, \dots, u^n)$ 的函数，即 $\mathbf{r} = \mathbf{r}(u^1, u^2, \dots, u^n)$，那么第 $i$ 个**协变基矢**（covariant basis vector）$\mathbf{e}_i$ 定义为位置矢量 $\mathbf{r}$ 对坐标 $u^i$ 的偏导数：

$$
\mathbf{e}_i = \frac{\partial \mathbf{r}}{\partial u^i}
$$

这个定义的美妙之处在于其几何直观性。导数 $\frac{\partial \mathbf{r}}{\partial u^i}$ 精确地描述了当 $u^i$ 发生微小变化 $du^i$ 时，位置矢量 $\mathbf{r}$ 的变化率，这正是沿 $u^i$ 坐标曲线的切向量方向。

由于坐标曲线在空间中通常是弯曲的，它们的切线方向会随位置而变。因此，协变基矢 $\mathbf{e}_i$ 通常是位置的函数，即 $\mathbf{e}_i = \mathbf{e}_i(u^1, u^2, \dots, u^n)$。这一点与笛卡尔基矢的恒定性形成鲜明对比。例如，在二维极坐标系中，归一化的径向基矢 $\hat{\mathbf{e}}_r$ 和角向基矢 $\hat{\mathbf{e}}_\theta$ 的方向都依赖于角坐标 $\theta$。对 $\hat{\mathbf{e}}_r$ 求关于 $\theta$ 的导数可以清晰地看到这一点，我们发现 $\frac{\partial \hat{\mathbf{e}}_r}{\partial \theta} = \hat{\mathbf{e}}_\theta$，这表明 $\hat{\mathbf{e}}_r$ 的方向确实随着 $\theta$ 的变化而旋转 [@problem_id:1491045]。

**示例：抛物柱坐标中的协变基矢**
考虑一个由抛物柱坐标 $(\sigma, \tau, z)$ 描述的三维空间，其与笛卡尔坐标 $(x, y, z)$ 的转换关系为 $x = \sigma\tau$, $y = \frac{1}{2}(\tau^2 - \sigma^2)$, $z = z$。位置矢量可以写为 $\mathbf{r} = (\sigma\tau)\mathbf{\hat{i}} + \frac{1}{2}(\tau^2 - \sigma^2)\mathbf{\hat{j}} + z\mathbf{\hat{k}}$。我们可以根据定义计算与坐标 $\sigma$ 相关联的协变基矢 $\mathbf{e}_\sigma$ [@problem_id:1491018]：

$$
\mathbf{e}_\sigma = \frac{\partial \mathbf{r}}{\partial \sigma} = \frac{\partial x}{\partial \sigma}\mathbf{\hat{i}} + \frac{\partial y}{\partial \sigma}\mathbf{\hat{j}} + \frac{\partial z}{\partial \sigma}\mathbf{\hat{k}} = \tau\mathbf{\hat{i}} - \sigma\mathbf{\hat{j}}
$$

可以看到，$\mathbf{e}_\sigma$ 的分量依赖于坐标 $\sigma$ 和 $\tau$。在点 $(\sigma, \tau, z) = (2, -1, 3)$，这个基矢的具体值为 $\mathbf{e}_\sigma = -1\mathbf{\hat{i}} - 2\mathbf{\hat{j}}$。类似地，我们可以计算出 $\mathbf{e}_\tau = \sigma\mathbf{\hat{i}} + \tau\mathbf{\hat{j}}$ 和 $\mathbf{e}_z = \mathbf{\hat{k}}$。

### 度规张量与局域几何

协变基矢虽然直观，但它们不一定是单位向量，也不一定相互正交。为了量化这些几何特性——即基矢的长度和它们之间的夹角——我们引入了**度规张量**（metric tensor），其分量用 $g_{ij}$ 表示。

协变度规张量的分量定义为协变基矢之间的点积：

$$
g_{ij} = \mathbf{e}_i \cdot \mathbf{e}_j
$$

这个定义蕴含了坐标系在某一点的全部局域几何信息：
- **对角分量** $g_{ii} = \mathbf{e}_i \cdot \mathbf{e}_i = |\mathbf{e}_i|^2$，表示第 $i$ 个协变基矢长度的平方。
- **非对角分量** $g_{ij} = \mathbf{e}_i \cdot \mathbf{e}_j = |\mathbf{e}_i| |\mathbf{e}_j| \cos\theta_{ij}$ (其中 $i \neq j$)，它与基矢 $\mathbf{e}_i$ 和 $\mathbf{e}_j$ 之间夹角的余弦有关。

如果一个坐标系在某点是**正交的**（orthogonal），那么在该点的所有基矢都相互垂直。这意味着当 $i \neq j$ 时，$\mathbf{e}_i \cdot \mathbf{e}_j = 0$，因此所有非对角度规分量 $g_{ij}$ 都为零。此时度规张量矩阵是一个对角矩阵。常见的极坐标、圆柱坐标和球坐标都是正交坐标系。

然而，在一般情况下，坐标系可以是非正交的。例如，考虑坐标变换 $x = q_1^2 - q_2^2, y = q_1 q_2$ [@problem_id:1491050]。协变基矢为 $\mathbf{e}_1 = 2q_1 \mathbf{\hat{i}} + q_2 \mathbf{\hat{j}}$ 和 $\mathbf{e}_2 = -2q_2 \mathbf{\hat{i}} + q_1 \mathbf{\hat{j}}$。非对角度规分量为：

$$
g_{12} = \mathbf{e}_1 \cdot \mathbf{e}_2 = (2q_1)(-2q_2) + (q_2)(q_1) = -3q_1 q_2
$$

由于 $g_{12}$ 通常不为零，这个坐标系是**非正交的**。这意味着坐标线 $q_1=\text{常数}$ 和 $q_2=\text{常数}$ 在大多数点上不是以直角相交。

一个更极端的情况是，在某些点上，协变基矢可能变得线性相关。这意味着坐标变换在这些点上是**奇异的**或**退化的**。两个基矢 $\mathbf{e}_1, \mathbf{e}_2$ 线性相关意味着一个可以表示为另一个的倍数，它们指向相同或相反的方向。从几何上看，这意味着在这一点，两个坐标网格线相切，无法唯一地区分两个独立的方向。这种情况在数学上等价于坐标变换的雅可比行列式（Jacobian determinant）为零 [@problem_id:1490995]。

### 逆变基矢：坐标曲面的法线

除了协变基矢，我们还需要引入另一组同样重要的基矢，称为**逆变基矢**（contravariant basis vectors）或**对偶基矢**（dual basis vectors），记作 $\mathbf{e}^i$。它们的定义可能不那么直观，但其几何意义和代数便利性是不可或缺的。

逆变基矢 $\mathbf{e}^i$ 是通过它们与协变基矢 $\mathbf{e}_j$ 的关系来定义的，这个关系被称为**对偶关系**：

$$
\mathbf{e}^i \cdot \mathbf{e}_j = \delta^i_j
$$

这里 $\delta^i_j$ 是**克罗内克 δ**（Kronecker delta），当 $i=j$ 时其值为1，当 $i \neq j$ 时其值为0。

这个定义揭示了一个深刻的几何对偶性：
- $\mathbf{e}^i \cdot \mathbf{e}_j = 0$ (当 $i \neq j$) 意味着逆变基矢 $\mathbf{e}^i$ 必须垂直于所有与它索引不同的协变基矢 $\mathbf{e}_j$。
- $\mathbf{e}^i \cdot \mathbf{e}_i = 1$ 则是一种归一化条件，但它是一种“投影”意义上的归一化，而非长度为1。

在三维空间中，垂直于两个不同向量（例如 $\mathbf{e}_2$ 和 $\mathbf{e}_3$）的向量必定平行于它们的叉积 $\mathbf{e}_2 \times \mathbf{e}_3$。而向量 $\mathbf{e}_2$ 和 $\mathbf{e}_3$ 张成了一个坐标曲面 $u^1=\text{常数}$ 的局部切平面。因此，$\mathbf{e}^1$ 必须垂直于 $u^1=\text{常数}$ 这个坐标曲面。

这一结论可以推广：**逆变基矢 $\mathbf{e}^i$ 的方向总是垂直于对应的坐标超曲面 $u^i=\text{常数}$**。

这与协变基矢形成了鲜明的对比：$\mathbf{e}_i$ 沿 $u^i$ 坐标**线**相切，而 $\mathbf{e}^i$ 则垂直于 $u^i$ 坐标**面**。在正交坐标系中，坐标线与坐标面本就垂直，因此协变基矢和逆变基矢指向相同的方向，仅在长度上有所不同。但在非正交系中，它们的方向会不同。

**示例：球坐标中的逆变基矢几何**
在球坐标 $(r, \theta, \phi)$ 中，坐标曲面 $\theta=\theta_0$ 是一个以原点为顶点的圆锥面。这个曲面上的切向量由 $\mathbf{e}_r$ 和 $\mathbf{e}_\phi$ 张成。因此，这个圆锥面的法向量 $\mathbf{N}$ 平行于 $\mathbf{e}_r \times \mathbf{e}_\phi$。根据我们刚建立的几何图像，逆变基矢 $\mathbf{e}^\theta$ 也必须垂直于 $\theta=\theta_0$ 曲面。因此，$\mathbf{e}^\theta$ 和 $\mathbf{N}$ 必须是平行的。通过详细计算可以确定它们之间的比例常数 [@problem_id:1491019]。

计算逆变基矢有两种主要方法：
1.  **使用度规张量**：这是最普适的方法。逆变基矢可以通过协变基矢和**逆变度规张量** $g^{ij}$ 来构建。逆变度规张量是协变度规张量矩阵 $(g_{ij})$ 的逆矩阵，即 $g^{ik}g_{kj} = \delta^i_j$。它们的关系是：
    $$
    \mathbf{e}^i = \sum_j g^{ij} \mathbf{e}_j
    $$
    这个公式在任何维度都有效，并且是进行张量计算的标准工具 [@problem_id:1491053]。

2.  **使用叉积（仅限三维）**：在三维空间中，可以使用更具几何色彩的公式：
    $$
    \mathbf{e}^1 = \frac{\mathbf{e}_2 \times \mathbf{e}_3}{\mathbf{e}_1 \cdot (\mathbf{e}_2 \times \mathbf{e}_3)}, \quad \mathbf{e}^2 = \frac{\mathbf{e}_3 \times \mathbf{e}_1}{\mathbf{e}_1 \cdot (\mathbf{e}_2 \times \mathbf{e}_3)}, \quad \mathbf{e}^3 = \frac{\mathbf{e}_1 \times \mathbf{e}_2}{\mathbf{e}_1 \cdot (\mathbf{e}_2 \times \mathbf{e}_3)}
    $$
    分母中的 $J = \mathbf{e}_1 \cdot (\mathbf{e}_2 \times \mathbf{e}_3)$ 是由三个协变基矢构成的平行六面体的体积，也等于坐标变换的雅可比行列式的平方根 $\sqrt{\det(g_{ij})}$。

### 矢量分量与不变量运算

有了协变和逆变这两组基矢，我们可以用两种不同的方式来分解任意一个矢量 $\mathbf{A}$：

1.  **逆变分量**（Contravariant Components）：将 $\mathbf{A}$ 分解为协变基矢的线性组合：
    $$
    \mathbf{A} = A^1 \mathbf{e}_1 + A^2 \mathbf{e}_2 + \dots = \sum_i A^i \mathbf{e}_i
    $$
    分量 $A^i$ 被称为逆变分量。这种分解遵循向量加法的“平行四边形法则”。

2.  **协变分量**（Covariant Components）：将 $\mathbf{A}$ 分解为逆变基矢的线性组合：
    $$
    \mathbf{A} = A_1 \mathbf{e}^1 + A_2 \mathbf{e}^2 + \dots = \sum_i A_i \mathbf{e}^i
    $$
    分量 $A_i$ 被称为协变分量。

如何得到这些分量？利用基矢的对偶关系，我们可以通过点积（即投影）来提取它们：
- 两边点乘 $\mathbf{e}^j$ 到第一个展开式：$\mathbf{A} \cdot \mathbf{e}^j = (\sum_i A^i \mathbf{e}_i) \cdot \mathbf{e}^j = \sum_i A^i (\mathbf{e}_i \cdot \mathbf{e}^j) = \sum_i A^i \delta_i^j = A^j$。所以：
  $$A^j = \mathbf{A} \cdot \mathbf{e}^j$$
  逆变分量是矢量在逆变基矢上的投影 [@problem_id:1491060]。

- 两边点乘 $\mathbf{e}_j$ 到第二个展开式：$\mathbf{A} \cdot \mathbf{e}_j = (\sum_i A_i \mathbf{e}^i) \cdot \mathbf{e}_j = \sum_i A_i (\mathbf{e}^i \cdot \mathbf{e}_j) = \sum_i A_i \delta^i_j = A_j$。所以：
  $$A_j = \mathbf{A} \cdot \mathbf{e}_j$$
  协变分量是矢量在协变基矢上的投影。

物理定律必须独立于我们选择的坐标系。这意味着像矢量的长度、两个矢量之间的夹角或一个力所做的功等物理量，其数值不应随坐标系的改变而改变。这些量被称为**不变量**（invariants）。标量积（点积）是构建不变量的核心运算。

考虑两个矢量 $\mathbf{A}$ 和 $\mathbf{B}$ 的标量积 $\mathbf{A} \cdot \mathbf{B}$。使用分量表示，我们有多种计算方法，但结果都是一样的：
$$
\mathbf{A} \cdot \mathbf{B} = (A^i \mathbf{e}_i) \cdot (B^j \mathbf{e}_j) = A^i B^j (\mathbf{e}_i \cdot \mathbf{e}_j) = g_{ij} A^i B^j
$$
$$
\mathbf{A} \cdot \mathbf{B} = (A_i \mathbf{e}^i) \cdot (B_j \mathbf{e}^j) = A_i B_j (\mathbf{e}^i \cdot \mathbf{e}^j) = g^{ij} A_i B_j
$$
$$
\mathbf{A} \cdot \mathbf{B} = (A^i \mathbf{e}_i) \cdot (B_j \mathbf{e}^j) = A^i B_j (\mathbf{e}_i \cdot \mathbf{e}^j) = A^i B_j \delta^j_i = A^i B_i
$$
最后一种形式 $\mathbf{A} \cdot \mathbf{B} = \sum_i A^i B_i$ 是最简洁的，它体现了张量代数中“一个上标索引与一个下标索引求和”的核心思想。这种操作称为**张量缩并**（tensor contraction）。

**应用示例：坐标变换下的功的计算**
一个力 $\mathbf{F}$ 对一个微小位移 $\mathbf{d}$ 做的功 $W = \mathbf{F} \cdot \mathbf{d}$ 是一个标量不变量。我们可以在任何坐标系中计算它。假设在笛卡尔坐标系下，我们知道 $\mathbf{F}$ 和 $\mathbf{d}$ 的分量。为了在极坐标系 $(r, \theta)$ 中计算功，我们可以将 $\mathbf{F}$ 的分量转换为逆变分量 $(F^r, F^\theta)$，将 $\mathbf{d}$ 的分量转换为协变分量 $(d_r, d_\theta)$，然后进行缩并 [@problem_id:1491011]：

$$
W = F^r d_r + F^\theta d_\theta
$$

无论计算多么复杂，最终得到的功 $W$ 的数值将与在笛卡尔坐标系中直接计算 $\mathbf{F} \cdot \mathbf{d}$ 的结果完全相同。这完美地展示了张量方法的威力：尽管基矢和分量在不同坐标系下会发生复杂的变换，但它们以一种精确的方式相互补偿，以保持物理实在（如功）的独立性。

### 完整基与非完整基

到目前为止，我们讨论的基矢都源于一个潜在的坐标系，即它们可以表示为 $\mathbf{e}_i = \partial \mathbf{r} / \partial u^i$。这种可以由一组坐标函数 $u^i$ 积分得到的基矢场被称为**完整基**（holonomic basis）或**坐标基**（coordinate basis）。

然而，在物理学和工程学中，有时会遇到无法从任何坐标系导出的基矢场。例如，在处理带约束的力学系统时，可能方便地定义一组局部基矢，但这组基矢在数学上并不对应任何全局或局部的坐标网格。这样的基矢被称为**非完整基**（non-holonomic basis）。

如何判断一个给定的基矢场 $\{\mathbf{b}_1, \mathbf{b}_2, \dots, \mathbf{b}_n\}$ 是否是完整基？根据**弗罗贝尼乌斯定理**（Frobenius' theorem），一个充要条件是这组基矢的**李括号**（Lie bracket）或**对易子**（commutator）全部为零。两个矢量场 $\mathbf{U}$ 和 $\mathbf{V}$ 的李括号定义为：

$$
[\mathbf{U}, \mathbf{V}] = (\mathbf{U} \cdot \nabla) \mathbf{V} - (\mathbf{V} \cdot \nabla) \mathbf{U}
$$

李括号 $[\mathbf{U}, \mathbf{V}]$ 衡量了沿 $\mathbf{U}$ 方向移动再沿 $\mathbf{V}$ 方向移动，与先沿 $\mathbf{V}$ 方向移动再沿 $\mathbf{U}$ 方向移动，这两条路径终点之间的差异。如果一个基矢场是完整基，那么沿着坐标线的微小移动是可以交换顺序的，因此李括号为零：

$$
[\mathbf{e}_i, \mathbf{e}_j] = 0 \quad \text{for all } i, j
$$

如果对于某个基矢场 $\{\mathbf{b}_i\}$，存在 $[\mathbf{b}_i, \mathbf{b}_j] \neq 0$，那么这个基矢场就是非完整的 [@problem_id:1491005]。这为我们区分两种性质截然不同的基矢提供了严格的数学工具，并为研究更广义的几何结构（如带约束的流形）奠定了基础。