## 引言
在[张量分析](@entry_id:161423)的广阔领域中，对称性扮演着核心角色，它揭示了物理和几何对象深层的内在结构。其中一类特殊的张量——交错张量（或称[反对称张量](@entry_id:199349)），因其独特的反对称性质，成为描述旋转、[有向面积](@entry_id:169588)与体积以及物理场（如[电磁场](@entry_id:265881)）等概念不可或缺的数学工具。然而，初学者往往难以把握其抽象定义背后的具体意义，以及如何将其与我们熟悉的矢量运算和几何直观联系起来。本文旨在系统性地弥合这一知识鸿沟。

在接下来的内容中，我们将分三步深入探索交错张量的世界。
- 首先，在“原理与机制”一章中，我们将从基本定义和性质出发，建立起交错张量的坚实理论基础，并引入强大的代数工具——外积与[外代数](@entry_id:201164)。
- 接着，在“应用与跨学科联系”部分，我们将展示这些理论如何在[连续介质力学](@entry_id:155125)、电磁学、广义相对论乃至抽象代数等多个学科中大放异彩，揭示其作为统一描述语言的强大功能。
- 最后，通过“动手实践”环节，你将有机会通过解决具体问题来巩固所学知识，将理论真正内化为自己的技能。

## 原理与机制

在对张量进行更深入的研究时，我们会遇到一类具有特殊对称性的张量，它们在物理学和几何学中扮演着至关重要的角色。本章将系统地探讨**交错张量（alternating tensors）**，也称为**[反对称张量](@entry_id:199349)（anti-symmetric tensors）**或**[斜对称张量](@entry_id:199349)（skew-symmetric tensors）**。我们将从其基本定义出发，揭示其核心性质，并引入一个强大的代数工具——**外积（wedge product）**，它为处理这类张量提供了优雅而深刻的框架。

### 交错张量的定义与基本性质

一个秩为 $(0, k)$ 的[协变张量](@entry_id:634493) $T$ 被称为**交错张量**，如果当其任意两个矢量参数互换位置时，张量的值会变号。形式上，对于任意矢量 $\mathbf{v}_1, \dots, \mathbf{v}_k$，以及任意索引 $i \neq j$，我们有：
$$
T(\dots, \mathbf{v}_i, \dots, \mathbf{v}_j, \dots) = -T(\dots, \mathbf{v}_j, \dots, \mathbf{v}_i, \dots)
$$
这个定义不依赖于任何特定的[坐标系](@entry_id:156346)，是张量内在的几何属性。然而，在给定的基底下，这个定义可以更具体地通过张量的分量来表达。若张量 $T$ 的分量为 $T_{i_1 \dots i_k}$，则交错性质等价于：交换任意两个索引的位置，分量的值会变号。例如，对于一个秩为 $(0, 2)$ 的张量，其交错性质表现为：
$$
T_{ij} = -T_{ji} \quad \text{for all } i, j
$$

这个看似简单的条件蕴含了几个重要的推论。

首先，考虑一个交错张量的对角分量，即索引重复出现的情况。对于一个秩为 $(0, 2)$ 的交错张量 $T$，如果我们令 $i=j$，则反对称条件变为 $T_{ii} = -T_{ii}$。这立即导出 $2T_{ii} = 0$，因此 $T_{ii} = 0$。这意味着**任何秩为2的交错张量，其对角分量必须全部为零**。这个性质是判断一个张量是否为交错张量的快速检验方法。

例如，假设在 $\mathbb{R}^3$ 的[标准正交基](@entry_id:147779)下，一个 $(0, 2)$ 型张量 $T$ 的分量由以下矩阵给出 [@problem_id:1489337]：
$$
T_{ij} = \begin{pmatrix}
0  & 4  & -1 \\
-4 & 0  & 6 \\
1  & -6 & 2
\end{pmatrix}
$$
我们来检验它是否为交错张量。首先检查非对角分量：$T_{12} = 4$ 且 $T_{21} = -4$，满足 $T_{12} = -T_{21}$。同样，$T_{13} = -1, T_{31} = 1$ 和 $T_{23} = 6, T_{32} = -6$ 也都满足[反对称关系](@entry_id:261979)。然而，当我们检查对角分量时，发现 $T_{11}=0, T_{22}=0$，但 $T_{33}=2 \neq 0$。由于存在一个非零的对角分量，该张量不满足交错张量的定义。

这个性质可以推广到任意秩的交错张量。如果一个秩为 $k$ 的交错张量 $A$ 的任意两个索引相同，那么该分量必为零。例如，对于一个秩为3的交错张量 $A_{ijk}$，如果 $i=k$，那么根据定义，交换这两个索引会改变符号：$A_{ijk} = -A_{kji}$。但由于 $i=k$，我们实际上是在说 $A_{iji} = -A_{iji}$，这意味着 $A_{iji} = 0$。这个结论适用于任何一对重复的索引。因此，诸如 $A_{212}$ 这样的分量，由于索引 2 重复出现，其值必然为零 [@problem_id:1489387]。

其次，交错张量的一个深刻几何意义在于它如何作用于一组矢量。**一个 $k$-阶交错张量作用于一组 $k$ 个[线性相关](@entry_id:185830)的矢量时，其结果必定为零**。我们可以通过张量的[多重线性](@entry_id:151506)性质来理解这一点。假设有一组矢量 $\{\mathbf{v}_1, \dots, \mathbf{v}_k\}$ 是线性相关的，这意味着其中至少有一个矢量可以表示为其他矢量的[线性组合](@entry_id:154743)。不失[一般性](@entry_id:161765)，我们假设 $\mathbf{v}_k = \sum_{i=1}^{k-1} c_i \mathbf{v}_i$。那么，
$$
T(\mathbf{v}_1, \dots, \mathbf{v}_{k-1}, \mathbf{v}_k) = T(\mathbf{v}_1, \dots, \mathbf{v}_{k-1}, \sum_{i=1}^{k-1} c_i \mathbf{v}_i)
$$
利用张量的线性性质，我们得到：
$$
\sum_{i=1}^{k-1} c_i T(\mathbf{v}_1, \dots, \mathbf{v}_{k-1}, \mathbf{v}_i)
$$
在求和的每一项 $T(\mathbf{v}_1, \dots, \mathbf{v}_{k-1}, \mathbf{v}_i)$ 中，矢量 $\mathbf{v}_i$ 都出现了两次。由于 $T$ 是交错的，交换这两个相同的矢量会得到 $T(\dots) = -T(\dots)$，因此每一项都为零。于是，总和也为零。

这个性质在实际计算中非常有用。例如，考虑 $\mathbb{R}^4$ 上的一个3-形式（即秩为3的交错张量）$\omega$ 和三个矢量 $\mathbf{v}_1 = (1, 2, 0, 1)$，$\mathbf{v}_2 = (-1, 0, 1, 3)$，以及 $\mathbf{v}_3 = (1, 6, 2, 9)$。如果我们观察到 $2\mathbf{v}_1 + 3\mathbf{v}_2 = (2-3, 4+0, 0+3, 2+9) = (-1, 4, 3, 11)$... 啊，让我们重新审视一下矢量。实际上，通过检验可以发现 $\mathbf{v}_3 = 2\mathbf{v}_1 + 3\mathbf{v}_2$ 这个关系并不成立，但通过高斯消元法或其他方法可以验证这组矢量是[线性相关](@entry_id:185830)的，例如 $3\mathbf{v}_1+2\mathbf{v}_2-\mathbf{v}_3=0$。由于这三个矢量线性相关，我们无需进行任何复杂的计算，就可以立即断定 $\omega(\mathbf{v}_1, \mathbf{v}_2, \mathbf{v}_3) = 0$ [@problem_id:1489374]。这揭示了交错张量与（广义的）体积概念的内在联系：一组[线性相关](@entry_id:185830)的矢量无法张成一个具有非零体积的平行[多面体](@entry_id:637910)。

### 反对称化与[张量分解](@entry_id:173366)

并非所有张量都是交错的，但我们可以从任意一个张量中提取其交错部分。这个过程称为**反对称化（antisymmetrization）** 或 **交错化（alternation）**。对于一个秩为 $(0, k)$ 的张量 $T$，其交错部分 $Alt(T)$ 是通过对所有可能的索引[排列](@entry_id:136432)求和（并根据[排列](@entry_id:136432)的奇偶性赋予正负号）然后归一化得到的。具体来说，其分量为：
$$
(Alt(T))_{i_1 \dots i_k} = \frac{1}{k!} \sum_{\sigma \in S_k} \text{sgn}(\sigma) T_{i_{\sigma(1)} \dots i_{\sigma(k)}}
$$
其中 $S_k$ 是集合 $\{1, \dots, k\}$ 的所有[置换](@entry_id:136432)构成的对称群，$\text{sgn}(\sigma)$ 是[置换](@entry_id:136432) $\sigma$ 的符号（对于[偶置换](@entry_id:146469)为 $+1$，奇[置换](@entry_id:136432)为 $-1$）。经过这个操作得到的张量 $Alt(T)$ 自动满足交错性质。

对于秩为 $(0, 2)$ 的张量，这个过程尤为简单和重要。任何一个秩为 $(0, 2)$ 的张量 $T$ 都可以唯一地分解为一个**[对称张量](@entry_id:148092)（symmetric tensor）** $S$ 和一个**交错张量（alternating tensor）** $A$ 的和，即 $T = S + A$。对称张量满足 $S_{ij} = S_{ji}$，而交错张量满足 $A_{ij} = -A_{ji}$。

这个分解的公式可以直接构造出来。给定 $T_{ij}$，我们可以定义：
$$
S_{ij} = \frac{1}{2}(T_{ij} + T_{ji})
$$
$$
A_{ij} = \frac{1}{2}(T_{ij} - T_{ji})
$$
很容易验证 $S_{ij}$ 确实是对称的，$A_{ij}$ 确实是交错的，并且它们的和 $S_{ij} + A_{ij} = T_{ij}$。这个分解在理论和应用中都非常有用，例如在[连续介质力学](@entry_id:155125)中，形变张量可以分解为代表纯拉伸的对称[部分和](@entry_id:162077)代表刚性转动的交错部分。

让我们看一个具体的例子。假设在 $\mathbb{R}^2$ 中，一个张量 $T$ 的分量矩阵为 [@problem_id:1489320]：
$$
T = \begin{pmatrix} 5 & 9 \\ 1 & 7 \end{pmatrix}
$$
我们可以计算其交错部分 $A$ 的分量。例如，分量 $A_{12}$ 是：
$$
A_{12} = \frac{1}{2}(T_{12} - T_{21}) = \frac{1}{2}(9 - 1) = 4
$$
相应地，$A_{21} = \frac{1}{2}(T_{21} - T_{12}) = \frac{1}{2}(1 - 9) = -4$，满足 $A_{21} = -A_{12}$。对角分量则为 $A_{11} = \frac{1}{2}(T_{11} - T_{11}) = 0$ 和 $A_{22} = \frac{1}{2}(T_{22} - T_{22}) = 0$。因此，该张量的交错部分由矩阵 $\begin{pmatrix} 0 & 4 \\ -4 & 0 \end{pmatrix}$ 表示。

### 外积与[外代数](@entry_id:201164)

虽然我们可以通过反对称化操作从任意张量构造交错张量，但还有一种更根本、更具构造性的方法来产生它们，那就是**[外积](@entry_id:147029)（wedge product）**，记作 $\wedge$。通过[外积](@entry_id:147029)运算得到的交错张量通常被称为**[外形](@entry_id:146590)式（exterior forms）**或简称**[k-形式](@entry_id:191021)（k-forms）**。

外积的基础是从1-形式（即 $(0, 1)$ 型[协变张量](@entry_id:634493)）开始的。给定两个1-形式 $\alpha$ 和 $\beta$，它们的**[张量积](@entry_id:140694)（tensor product）** $\alpha \otimes \beta$ 是一个 $(0, 2)$ 型张量，但通常不是交错的。外积 $\alpha \wedge \beta$ 被定义为 $\alpha$ 和 $\beta$ 的[张量积](@entry_id:140694)的反对称化部分：
$$
\alpha \wedge \beta = \alpha \otimes \beta - \beta \otimes \alpha
$$
注意，有些定义中会包含一个 $\frac{1}{2}$ 的因子，但这里的定义在很多应用中更为方便。从这个定义可以清楚地看到 $\alpha \wedge \beta$ 是一个交错的 $(0, 2)$ 型张量，因为它作用于两个矢量 $\mathbf{u}, \mathbf{v}$ 的结果是：
$$
(\alpha \wedge \beta)(\mathbf{u}, \mathbf{v}) = (\alpha \otimes \beta)(\mathbf{u}, \mathbf{v}) - (\beta \otimes \alpha)(\mathbf{u}, \mathbf{v}) = \alpha(\mathbf{u})\beta(\mathbf{v}) - \beta(\mathbf{u})\alpha(\mathbf{v})
$$
交换 $\mathbf{u}$ 和 $\mathbf{v}$，我们得到：
$$
(\alpha \wedge \beta)(\mathbf{v}, \mathbf{u}) = \alpha(\mathbf{v})\beta(\mathbf{u}) - \beta(\mathbf{v})\alpha(\mathbf{u}) = -(\alpha \wedge \beta)(\mathbf{u}, \mathbf{v})
$$
这证实了其交错性质。

让我们通过一个例子来比较张量积和外积。在 $\mathbb{R}^2$ 中，设 $\{dx^1, dx^2\}$ 是对偶基。我们来构造两个张量 $A = dx^1 \otimes dx^2$ 和 $B = dx^1 \wedge dx^2$，并计算它们在基底 $\{e_1, e_2\}$ 下的分量矩阵 [@problem_id:1489366]。
对于[张量积](@entry_id:140694) $A=dx^1 \otimes dx^2$，其分量为 $A_{ij} = A(e_i, e_j) = (dx^1 \otimes dx^2)(e_i, e_j) = dx^1(e_i)dx^2(e_j) = \delta^1_i \delta^2_j$。唯一非零的分量是当 $i=1, j=2$ 时，$A_{12}=1$。所以其分量矩阵为：
$$
M_A = \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}
$$
对于外积 $B=dx^1 \wedge dx^2$，其分量为 $B_{ij} = B(e_i, e_j) = dx^1(e_i)dx^2(e_j) - dx^1(e_j)dx^2(e_i) = \delta^1_i \delta^2_j - \delta^1_j \delta^2_i$。计算各分量得到：$B_{11}=0, B_{22}=0, B_{12}=1, B_{21}=-1$。所以其分量矩阵为：
$$
M_B = \begin{pmatrix} 0 & 1 \\ -1 & 0 \end{pmatrix}
$$
这个例子清晰地展示了[外积](@entry_id:147029)如何通过反对称化过程，从一个非对称的张量积中构建出一个交错张量。

[外积](@entry_id:147029)具有以下几个关键代数性质：
1.  **[反对易](@entry_id:186708)性（Anti-commutativity）**：对于任意两个[1-形式](@entry_id:270392) $\alpha, \beta$，有 $\alpha \wedge \beta = -\beta \wedge \alpha$。这是定义的直接结果。因此，$\alpha \wedge \beta - \beta \wedge \alpha = 2(\alpha \wedge \beta)$ [@problem_id:1489342]。
2.  **零幂性（Nilpotency）**：对于任意一个[1-形式](@entry_id:270392) $\alpha$，有 $\alpha \wedge \alpha = 0$。这是因为 $\alpha \wedge \alpha = -\alpha \wedge \alpha$，所以 $2(\alpha \wedge \alpha)=0$。这意味着，无论一个[1-形式](@entry_id:270392)多么复杂，它与自身的[外积](@entry_id:147029)总是零 [@problem_id:1489365]。例如，对于 $\alpha = (2x+y^3)dx + (\sin(z))dy + (x e^{y})dz$，计算 $\alpha \wedge \alpha$ 会得到一大串项，但利用 $dx \wedge dx = 0$ 和 $dx \wedge dy = -dy \wedge dx$ 等规则，所有项最终都会抵消，结果为零。
3.  **结合律（Associativity）**：$(\alpha \wedge \beta) \wedge \gamma = \alpha \wedge (\beta \wedge \gamma)$。
4.  **分配律（Distributivity）**：$\alpha \wedge (\beta + \gamma) = \alpha \wedge \beta + \alpha \wedge \gamma$。

这些性质使得在一个[向量空间](@entry_id:151108) $V$ 上所有[k-形式](@entry_id:191021)构成的空间 $\Lambda(V^*) = \bigoplus_{k=0}^n \Lambda^k(V^*)$，与外积运算一起，构成了一个[代数结构](@entry_id:137052)，称为**[外代数](@entry_id:201164)（Exterior Algebra）**。

### [k-形式](@entry_id:191021)空间的维度

[外代数](@entry_id:201164)的一个核心结果是关于[k-形式](@entry_id:191021)空间的维度。在一个 $n$ 维[向量空间](@entry_id:151108) $V$ 上，如果其对偶空间 $V^*$ 有一组基底 $\{dx^1, \dots, dx^n\}$，那么 $k$-形式的空间 $\Lambda^k(V^*)$ 的一组基底可以由以下形式的所有[外积](@entry_id:147029)构成：
$$
dx^{i_1} \wedge dx^{i_2} \wedge \dots \wedge dx^{i_k}, \quad \text{其中 } 1 \le i_1 \lt i_2 \lt \dots \lt i_k \le n
$$
选择索引时要求严格递增，这是因为反对易性意味着任何其他顺序的索引组合都可以被重新[排列](@entry_id:136432)成这个[标准形式](@entry_id:153058)（可能带有负号），而任何重复的索引都会使整个[外积](@entry_id:147029)为零。

从这个基底的构造可以看出，$\Lambda^k(V^*)$ 的维度等于从 $n$ 个基底1-形式中选取 $k$ 个不同形式来构造基底[k-形式](@entry_id:191021)的方法数。这个数目正是二项式系数：
$$
\dim(\Lambda^k(V^*)) = \binom{n}{k} = \frac{n!}{k!(n-k)!}
$$

这个维度公式有两个极其重要的推论：

第一，如果 $k > n$，那么 $\binom{n}{k} = 0$。这意味着**在一个 $n$ 维空间中，任何阶数大于 $n$ 的交错张量（[k-形式](@entry_id:191021)）都必然是零张量**。例如，在二维空间 $\mathbb{R}^2$ 中（$n=2$），任何3-形式（$k=3$）都必定为零。这是因为在二维空间中，任何三个[1-形式](@entry_id:270392)都必然是[线性相关](@entry_id:185830)的。因此，由它们的[外积](@entry_id:147029)构成的3-形式 $\Omega = \alpha_1 \wedge \alpha_2 \wedge \alpha_3$ 作用于任意三个矢量 $u,v,w$ 时，其结果可以表示为一个[行列式](@entry_id:142978)，而这个[行列式](@entry_id:142978)的行（或列）是线性相关的，故[行列式](@entry_id:142978)值为零。所以，$\Omega(u,v,w)=0$ 对任意 $u,v,w$ 成立，即 $\Omega$ 是零张量 [@problem_id:1489339]。

第二，当 $k=n$ 时，$\dim(\Lambda^n(V^*)) = \binom{n}{n} = 1$。这意味着在 $n$ 维空间中，所有 $n$-形式构成一个一维空间。该空间中的任何非零元素都可以作为基底，并被称为该空间的**体积形式（volume form）**。例如，在 $\mathbb{R}^3$ 中， $dx \wedge dy \wedge dz$ 就是一个标准的体积形式。

### 高阶主题与几何解释

交错张量和外积的概念引向了线性代数和微分几何中一些更深刻的结果。

#### [行列式](@entry_id:142978)作为[体积形式](@entry_id:203000)

$n$-形式与[行列式](@entry_id:142978)的概念有着本质的联系。考虑一个 $n$ 维[向量空间](@entry_id:151108) $V$ 和一个[线性算子](@entry_id:149003) $T: V \to V$。这个算子不仅作用于矢量，还能**诱导（induce）**出一个作用于[k-形式](@entry_id:191021)的映射 $\Lambda^k T: \Lambda^k(V) \to \Lambda^k(V)$。当 $k=n$ 时，由于 $\Lambda^n(V)$ 是一维的，任何作用于其上的线性映射 $\Lambda^n T$ 都必然等同于乘以一个标量。这个标量，正是算子 $T$ 的**[行列式](@entry_id:142978)（determinant）**。

具体来说，设 $\Omega$ 是 $\Lambda^n(V)$ 的一个基底（一个体积形式）。那么存在一个标量 $\lambda$，使得：
$$
(\Lambda^n T)(\Omega) = \lambda \Omega
$$
这个标量 $\lambda$ 就是 $\det(T)$。如果我们选择[基矢](@entry_id:199546) $e_1, \dots, e_n$ 使得 $\Omega = e_1 \wedge \dots \wedge e_n$，那么诱导映射的作用由下式给出：
$$
(\Lambda^n T)(e_1 \wedge \dots \wedge e_n) = T(e_1) \wedge \dots \wedge T(e_n)
$$
将 $T(e_j)$ 表示为[基矢](@entry_id:199546)的[线性组合](@entry_id:154743) $T(e_j) = \sum_i [T]^i_j e_i$，其中 $[T]$ 是算子 $T$ 的矩阵表示。利用外积的[多重线性](@entry_id:151506)和交错性质，可以证明：
$$
T(e_1) \wedge \dots \wedge T(e_n) = \det([T]) (e_1 \wedge \dots \wedge e_n)
$$
因此，我们得到 $\lambda = \det([T])$。这为[行列式](@entry_id:142978)提供了一个不依赖于具体基底选择的几何定义：[行列式](@entry_id:142978)是线性算子改变空间中（有向）体积的[比例因子](@entry_id:266678)。例如，对于 $\mathbb{R}^3$ 上的一个算子 $T$，其矩阵为 $[T] = \begin{pmatrix} 2 & 1 & 0 \\ 0 & 3 & 1 \\ 1 & 0 & 1 \end{pmatrix}$，其[行列式](@entry_id:142978) $\det([T]) = 7$。这意味着该算子会将基底体积形式 $e_1 \wedge e_2 \wedge e_3$ 映射为 $7 (e_1 \wedge e_2 \wedge e_3)$ [@problem_id:1489386]。

#### 单纯形式与几何

一个[k-形式](@entry_id:191021) $\omega$ 如果可以表示为 $k$ 个[1-形式](@entry_id:270392)的[外积](@entry_id:147029)，即 $\omega = \alpha_1 \wedge \dots \wedge \alpha_k$，则称其为**单纯的（simple）**或**可分解的（decomposable）**。

单纯的[k-形式](@entry_id:191021)具有清晰的几何意义。一个单纯的[2-形式](@entry_id:188008)（也称**双矢量 bivector**）$\alpha \wedge \beta$ 可以被看作是由矢量 $\alpha^\sharp$ 和 $\beta^\sharp$（通过度量张量与[1-形式](@entry_id:270392)对偶的矢量）张成的带方向和面积的平面元素。

一个重要的判别法则是：一个[2-形式](@entry_id:188008) $\omega$ 是单纯的，当且仅当 $\omega \wedge \omega = 0$。这是因为如果 $\omega = \alpha \wedge \beta$，那么 $\omega \wedge \omega = (\alpha \wedge \beta) \wedge (\alpha \wedge \beta) = 0$，因为1-形式的重排和零幂性会导致表达式为零。

在低维空间中，情况比较简单。例如，在三维空间 $\mathbb{R}^3$ 中，任何[2-形式](@entry_id:188008)都是单纯的。这意味着任何反对称的 $3 \times 3$ 矩阵所代表的几何对象都可以被看作一个单一的平面。

然而，在更高维度（$n \ge 4$）中，这个结论不再成立。存在非单纯的[2-形式](@entry_id:188008)。一个典型的例子是在 $\mathbb{R}^4$ 中考虑2-形式 [@problem_id:1489350]：
$$
\omega = A \, dx_1 \wedge dx_2 + B \, dx_3 \wedge dx_4
$$
其中 $A, B$ 是非零常数。我们来计算 $\omega \wedge \omega$：
$$
\omega \wedge \omega = (A \, dx_1 \wedge dx_2 + B \, dx_3 \wedge dx_4) \wedge (A \, dx_1 \wedge dx_2 + B \, dx_3 \wedge dx_4)
$$
展开后，利用 $(dx_1 \wedge dx_2) \wedge (dx_1 \wedge dx_2) = 0$ 和 $(dx_3 \wedge dx_4) \wedge (dx_3 \wedge dx_4) = 0$，我们只剩下交叉项：
$$
\omega \wedge \omega = A B \, (dx_1 \wedge dx_2) \wedge (dx_3 \wedge dx_4) + B A \, (dx_3 \wedge dx_4) \wedge (dx_1 \wedge dx_2)
$$
由于2-形式与[2-形式](@entry_id:188008)的外积是可交换的（因为 $(-1)^{2 \times 2} = 1$），上式变为：
$$
\omega \wedge \omega = 2AB \, dx_1 \wedge dx_2 \wedge dx_3 \wedge dx_4
$$
只要 $A$ 和 $B$ 都不为零，$\omega \wedge \omega$ 就不为零。因此，这个 $\omega$ 不是一个单纯的[2-形式](@entry_id:188008)。它的几何意义不能用一个简单的平面来描述，而是代表了两个不相交的、独立的平面（$x_1-x_2$ 平面和 $x_3-x_4$ 平面）的某种叠加。这个概念在研究电磁场张量和更广义的几何结构时至关重要。