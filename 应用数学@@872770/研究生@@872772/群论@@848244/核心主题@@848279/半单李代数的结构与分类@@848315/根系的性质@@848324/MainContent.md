## 引言
根系是现代数学中的一个核心概念，尤其在群论和李代数领域中扮演着基石的角色。它不仅为[半单李代数](@entry_id:190073)提供了一个完整而优雅的分类方案，其本身所蕴含的丰富对称性和精巧结构，也使其成为连接代数、几何与组合学的强大桥梁。然而，初学者往往只接触其作为分类工具的一面，而忽略了其作为一个[独立数](@entry_id:260943)学对象的深刻内涵及其在更广阔领域中的应用。本文旨在填补这一认知空白，系统性地揭示[根系](@entry_id:198970)的内在性质。

本文将引导读者踏上一场探索根系世界的旅程。在第一章“原理与机制”中，我们将深入剖析[根系](@entry_id:198970)的几何与代数构造，包括其如何由卡丹矩阵完全确定，外尔群如何刻画其对称性，以及对偶根系和相关格的重要概念。接下来的“应用与交叉学科联系”一章将展示这些抽象原理的强大威力，探讨根系理论如何在[表示论](@entry_id:137998)、现代[组合学](@entry_id:144343)乃至无限维[李代数](@entry_id:137954)的理论中找到具体应用。最后，“动手实践”部分将提供一系列精心设计的问题，帮助读者巩固所学知识。通过这一结构化的学习路径，读者将全面掌握[根系](@entry_id:198970)理论的核心，并领略其在[数学物理](@entry_id:265403)前沿中的重要作用。

## 原理与机制

在介绍根系统的基本定义之后，本章将深入探讨其内在的原理与核心机制。根系统不仅是向量的特定集合，更是一个蕴含着深刻几何与代数对称性的丰富结构。我们将从根之间的几何关系出发，探索其对偶性、外尔群的作用，并揭示一些深刻的组合与结构性质。

### 根的基本几何性质

根系统的所有结构信息，包括根之间的相对长度和角度，都被精炼地编码在一个称为 **卡丹矩阵 (Cartan matrix)** 的对象中。假设一个秩为 $r$ 的根系统 $\Phi$ 存在于[欧几里得空间](@entry_id:138052) $E$ 中，其[内积](@entry_id:158127)记为 $(\cdot, \cdot)$。我们选取一组 **单根 (simple roots)** $\Delta = \{\alpha_1, \alpha_2, \dots, \alpha_r\}$ 作为 $E$ 的一组基。卡丹矩阵 $A$ 的元素 $A_{ij}$ 定义为：

$$A_{ij} = \frac{2(\alpha_i, \alpha_j)}{(\alpha_j, \alpha_j)}$$

这个定义看起来不对称，但它恰好是理解根之间相互作用的关键。$A_{ij}$ 是一个整数，被称为卡丹整数。对角元素 $A_{ii}$ 恒等于 $2$，因为 $A_{ii} = \frac{2(\alpha_i, \alpha_i)}{(\alpha_i, \alpha_i)} = 2$。非对角元素 $A_{ij}$ ($i \ne j$) 则描述了根 $\alpha_i$ 在沿着根 $\alpha_j$ 方向的[反射变换](@entry_id:175518)中的行为，我们稍后会详细讨论这一点。

卡丹矩阵的一个直接而重要的应用是确定单根之间的相对长度。利用[内积](@entry_id:158127)的对称性 $(\alpha_i, \alpha_j) = (\alpha_j, \alpha_i)$，我们可以建立 $A_{ij}$ 和 $A_{ji}$ 之间的关系。从定义出发：
$$(\alpha_i, \alpha_j) = \frac{A_{ij}}{2} (\alpha_j, \alpha_j)$$
$$(\alpha_j, \alpha_i) = \frac{A_{ji}}{2} (\alpha_i, \alpha_i)$$
由于两者相等，我们得到：
$$\frac{A_{ij}}{2} (\alpha_j, \alpha_j) = \frac{A_{ji}}{2} (\alpha_i, \alpha_i)$$
整理后可得两个单根的长度平方之比：
$$\frac{(\alpha_j, \alpha_j)}{(\alpha_i, \alpha_i)} = \frac{A_{ji}}{A_{ij}}$$

这个简单的公式威力巨大。例如，对于秩为2的[例外李代数](@entry_id:202996) $G_2$，其卡丹矩阵为：
$$A = \begin{pmatrix} 2  -1 \\ -3  2 \end{pmatrix}$$
我们令 $\alpha_1, \alpha_2$ 为其单根。利用上述公式，取 $i=1, j=2$，我们立刻可以得到两个单根长度的平方比：
$$\frac{(\alpha_2, \alpha_2)}{(\alpha_1, \alpha_1)} = \frac{A_{21}}{A_{12}} = \frac{-3}{-1} = 3$$
这表明 $G_2$ [根系](@entry_id:198970)统中的两个单根长度不同。我们称长度较长的根为 **长根 (long root)**，较短的为 **短根 (short root)**。此例中，$(\alpha_2, \alpha_2) = 3(\alpha_1, \alpha_1)$，因此 $\alpha_2$ 是长根，$\alpha_1$ 是短根，它们的长度平方比为 $3$ [@problem_id:747293]。对于一个不可约根系统，最多只存在两种根长度（所有根要么是长根，要么是短根）。如果所有根的长度都相同，则称该根系统为 **单边 (simply-laced)** 的。

### 对偶根系统与[余根](@entry_id:193338)

与每个根 $\alpha$ 紧密相关的是它的 **[余根](@entry_id:193338) (coroot)**，记作 $\alpha^\vee$，定义为：
$$\alpha^\vee = \frac{2\alpha}{(\alpha, \alpha)}$$
[余根](@entry_id:193338)本质上是一个重新标定长度的根向量。这个定义的重要性在于它将[内积](@entry_id:158127)运算转化为一个更具代数性的“配对” $\langle \beta, \alpha^\vee \rangle = \frac{2(\beta, \alpha)}{(\alpha, \alpha)}$，这恰好是卡丹矩阵的元素 $A_{\beta\alpha}$（如果 $\alpha, \beta$ 都是单根）。

给定一个[根系](@entry_id:198970)统 $\Phi$，所有[余根](@entry_id:193338)的集合 $\Phi^\vee = \{\alpha^\vee \mid \alpha \in \Phi\}$ 本身也构成一个[根系](@entry_id:198970)统，称为 **对偶[根系](@entry_id:198970)统 (dual root system)**。$\Phi$ 与 $\Phi^\vee$ 共享同一个外尔群，并且如果 $\Delta = \{\alpha_1, \dots, \alpha_r\}$ 是 $\Phi$ 的一组单根，那么 $\Delta^\vee = \{\alpha_1^\vee, \dots, \alpha_r^\vee\}$ 就是 $\Phi^\vee$ 的一组单根。

对偶操作有一个有趣的性质：它会“翻转”长根和短根的角色。如果 $\alpha$ 是 $\Phi$ 中的一个长根，那么它的平方范数 $(\alpha, \alpha)$ 较大，导致 $\alpha^\vee$ 的平方范数 $(\alpha^\vee, \alpha^\vee) = \frac{4(\alpha, \alpha)}{(\alpha, \alpha)^2} = \frac{4}{(\alpha, \alpha)}$ 较小。反之，短根对应的[余根](@entry_id:193338)则会变长。

让我们通过 $C_3$ 型[根系](@entry_id:198970)统来具体考察这个现象。在以[标准正交基](@entry_id:147779) $\{e_1, e_2, e_3\}$ 张成的 $\mathbb{R}^3$ 空间中，$C_3$ 的根集为：
$$\Phi(C_3) = \{ \pm 2e_i \mid i=1,2,3 \} \cup \{ \pm e_i \pm e_j \mid 1 \le i  j \le 3 \}$$
我们计算根的长度平方：
*   对于 $\alpha = \pm 2e_i$，$(\alpha, \alpha) = 4$。
*   对于 $\beta = \pm e_i \pm e_j$，$(\beta, \beta) = 2$。
因此，$\pm 2e_i$ 形式的根是长根，而 $\pm e_i \pm e_j$ 形式的根是短根。$C_3$ 的短根数量 $N_S(C_3)$ 为 $\binom{3}{2} \times 2^2 = 12$ 个。

现在我们来构建其对偶根系统 $\Phi(C_3)^\vee$。
*   对于长根 $\alpha = 2e_i$，其对应的[余根](@entry_id:193338)为 $\alpha^\vee = \frac{2(2e_i)}{(2e_i, 2e_i)} = \frac{4e_i}{4} = e_i$。这些[余根](@entry_id:193338)的长度平方为 $(e_i, e_i)=1$。
*   对于短根 $\beta = e_i \pm e_j$，其对应的[余根](@entry_id:193338)为 $\beta^\vee = \frac{2(e_i \pm e_j)}{(e_i \pm e_j, e_i \pm e_j)} = \frac{2(e_i \pm e_j)}{2} = e_i \pm e_j$。这些[余根](@entry_id:193338)的长度平方为 $(e_i \pm e_j, e_i \pm e_j)=2$。
因此，$\Phi(C_3)^\vee = \{ \pm e_i \} \cup \{ \pm e_i \pm e_j \}$。这恰好是 $B_3$ 型[根系](@entry_id:198970)统的标准实现。在 $B_3$ 系统中，长度平方为 $1$ 的根是短根，长度平方为 $2$ 的根是长根。所以，$C_3$ 的对偶系统 $C_3^\vee$（即 $B_3$）的短根是 $\{\pm e_i\}$，数量为 $2 \times 3 = 6$ 个。
这个例子清晰地表明，从 $C_3$ 到其对偶 $B_3$，长根变成了短根，短根变成了长根。两者短根数量之比为 $\frac{N_S(C_3)}{N_S(C_3^\vee)} = \frac{12}{6} = 2$ [@problem_id:747381]。

### 外尔群及其作用

**外尔群 (Weyl group)** $W$ 是根系统的基本[对称群](@entry_id:146083)，它是由一系列根超平面（即与根向量正交的超平面）上的反射生成的有限群。对于每个根 $\alpha \in \Phi$，它定义了一个反射 $s_\alpha$：
$$s_\alpha(v) = v - \frac{2(v, \alpha)}{(\alpha, \alpha)} \alpha = v - \langle v, \alpha^\vee \rangle \alpha$$
其中 $v$ 是空间 $E$ 中的任意向量。外尔群 $W$ 由所有这些反射 $s_\alpha$ 生成。一个更经济的方式是，整个外尔群可以仅由对应于单根 $\alpha_i \in \Delta$ 的 **单反射 (simple reflections)** $s_i \equiv s_{\alpha_i}$ 生成。

单反射 $s_i$ 作用在另一个单根 $\alpha_j$ 上的结果有一个简洁的公式，直接与卡丹矩阵相关：
$$s_i(\alpha_j) = \alpha_j - \frac{2(\alpha_j, \alpha_i)}{(\alpha_i, \alpha_i)}\alpha_i = \alpha_j - A_{ij}\alpha_i$$
注意公式中卡丹[矩阵元](@entry_id:186505)素的索引是 $A_{ij}$。这个公式是进行[根系](@entry_id:198970)和外尔群相关计算的基石。由于反射是线性算子，我们可以通过线性组合来计算任意一个外尔群元素（即一串单反射的乘积）作用于任意一个由单根[线性表示](@entry_id:139970)的向量上的结果。

让我们以 $B_3$ 型根系统为例，其卡丹矩阵为：
$$A = \begin{pmatrix} 2  -1  0 \\ -1  2  -2 \\ 0  -1  2 \end{pmatrix}$$
考虑外尔群元素 $w = s_1 s_2 s_1$（这是一个常见的元素，表示先作用 $s_1$，再作用 $s_2$，最后再作用 $s_1$）。我们想知道它作用在单根 $\alpha_2$ 上会得到哪个根。
1.  首先，计算 $s_1(\alpha_2)$:
    $$s_1(\alpha_2) = \alpha_2 - A_{21}\alpha_1 = \alpha_2 - (-1)\alpha_1 = \alpha_1 + \alpha_2$$
2.  接着，将 $s_2$ 作用于上一步的结果 $s_1(\alpha_2)$:
    $$s_2(\alpha_1 + \alpha_2) = s_2(\alpha_1) + s_2(\alpha_2) = (\alpha_1 - A_{12}\alpha_2) + (\alpha_2 - A_{22}\alpha_2) = (\alpha_1 - (-1)\alpha_2) + (\alpha_2 - 2\alpha_2) = \alpha_1 + \alpha_2 - \alpha_2 = \alpha_1$$
3.  最后，将 $s_1$ 作用于上一步的结果 $s_2(s_1(\alpha_2))$:
    $$s_1(\alpha_1) = \alpha_1 - A_{11}\alpha_1 = \alpha_1 - 2\alpha_1 = -\alpha_1$$
所以，$s_1 s_2 s_1 (\alpha_2) = -\alpha_1$。这表明通过外尔群的作用，一个根可以变换为另一个根。事实上，整个[根系](@entry_id:198970)统 $\Phi$ 都可以通过将外尔群 $W$ 作用于单根集 $\Delta$ 来生成，即 $\Phi = \bigcup_{\alpha \in \Delta} W(\alpha)$。
另一个例子是计算 $w = s_1 s_3 s_2$ 作用在 $\alpha_3$ 上的结果[@problem_id:747428]。按照从右到左的顺序：
1. $s_2(\alpha_3) = \alpha_3 - A_{32}\alpha_2 = \alpha_3 - (-1)\alpha_2 = \alpha_2 + \alpha_3$。
2. $s_3(\alpha_2 + \alpha_3) = s_3(\alpha_2) + s_3(\alpha_3) = (\alpha_2 - A_{23}\alpha_3) + (-\alpha_3) = (\alpha_2 - (-2)\alpha_3) - \alpha_3 = \alpha_2 + \alpha_3$。
3. $s_1(\alpha_2 + \alpha_3) = s_1(\alpha_2) + s_1(\alpha_3) = (\alpha_2 - A_{21}\alpha_1) + (\alpha_3 - A_{31}\alpha_1) = (\alpha_2 - (-1)\alpha_1) + \alpha_3 = \alpha_1+\alpha_2+\alpha_3$。
最终得到根 $\beta = \alpha_1+\alpha_2+\alpha_3$。

外尔群本身作为一种有限群，其群论结构也值得研究。例如，$D_n$ 型[根系](@entry_id:198970)统的外尔群 $W(D_n)$ 可以被描述为作用在 $\mathbb{R}^n$ 上的[置换](@entry_id:136432)和偶数次变号的组合。其中心 $Z(W(D_n))$ 的结构依赖于 $n$ 的奇偶性。当 $n$ 为奇数时，中心是平凡的，仅包含单位元，即 $|Z(W(D_n))|=1$。例如，对于 $D_5$，$|Z(W(D_5))|=1$ [@problem_id:747407]。当 $n \ge 4$ 且为偶数时，中心由单位元和全局变号 $-I$ 构成，阶为2。

### 组合与结构性质

除了几何和[代数结构](@entry_id:137052)，根系统还展现出丰富的[组合性](@entry_id:637804)质。

**[正根](@entry_id:199264)、高度和[根串](@entry_id:180284)**

选定一组单根 $\Delta$ 后，根系统 $\Phi$ 可以唯一地划分为 **[正根](@entry_id:199264) (positive roots)** $\Phi^+$ 和 **负根 (negative roots)** $\Phi^-$。[正根](@entry_id:199264)是指那些可以表示为单根的非负整系数线性组合的根。对于一个[正根](@entry_id:199264) $\beta = \sum k_i \alpha_i$（其中 $k_i \in \mathbb{Z}_{\ge 0}$），它的 **高度 (height)** 定义为系数之和 $\text{ht}(\beta) = \sum k_i$。例如，在 $B_3$ 根系统中，单根为 $\alpha_1=e_1-e_2, \alpha_2=e_2-e_3, \alpha_3=e_3$。短[正根](@entry_id:199264)有 $e_3, e_2, e_1$，它们可以表示为：
$$e_3 = \alpha_3 \quad (\text{高度为 } 1)$$
$$e_2 = \alpha_2 + \alpha_3 \quad (\text{高度为 } 2)$$
$$e_1 = \alpha_1 + \alpha_2 + \alpha_3 \quad (\text{高度为 } 3)$$
因此，$e_1$ 是 $B_3$ 中的 **最高短根 (highest short root)** [@problem_id:747361]。

对于任意两个根 $\alpha, \beta \in \Phi$，所有形如 $\alpha + k\beta$（$k$ 为整数）且本身也属于 $\Phi$ 的向量集合，被称为通过 $\alpha$ 的 $\beta$-**[根串](@entry_id:180284) (root string)**。根系统的一个基本公理保证了这些 $k$ 值构成一个连续的整数序列，即 $k \in \{p, p+1, \dots, q\}$，其中 $p \le 0 \le q$。这个[根串](@entry_id:180284)的长度（即根的数量）为 $q-p+1$。这两个端点 $p, q$ 可以通过一个优美的公式确定：
$$p-q = \langle \alpha, \beta^\vee \rangle = \frac{2(\alpha, \beta)}{(\beta, \beta)}$$
以 $G_2$ [根系](@entry_id:198970)统为例，我们来确定通过长单根 $\alpha_2$ 的 $\alpha_1$-[根串](@entry_id:180284)的长度。已知 $(\alpha_2, \alpha_2) = 3(\alpha_1, \alpha_1)$，且两单根夹角为 $5\pi/6$。我们需要计算 $\langle \alpha_2, \alpha_1^\vee \rangle$。
$$ \langle \alpha_2, \alpha_1^\vee \rangle = \frac{2(\alpha_2, \alpha_1)}{(\alpha_1, \alpha_1)} = \frac{2\sqrt{(\alpha_1, \alpha_1)(\alpha_2, \alpha_2)}\cos(5\pi/6)}{(\alpha_1, \alpha_1)} = \frac{2\sqrt{3(\alpha_1, \alpha_1)^2}(-\sqrt{3}/2)}{(\alpha_1, \alpha_1)} = -3 $$
根据公式 $p-q = -3$，且 $p \le 0 \le q$，唯一解是 $p=0, q=3$。因此，[根串](@entry_id:180284)为 $\{\alpha_2, \alpha_2+\alpha_1, \alpha_2+2\alpha_1, \alpha_2+3\alpha_1\}$。[根串](@entry_id:180284)中共有 $q-p+1 = 3-0+1=4$ 个根 [@problem_id:747341]。

**根的数量与[不变量](@entry_id:148850)**

一个根系统的总根数 $|\Phi|$ 是一个重要的[不变量](@entry_id:148850)。它与根系统的秩 $r$ 和另一个称为 **[考克斯特数](@entry_id:185785) (Coxeter number)** $h$ 的整数有着惊人的简单关系：
$$|\Phi| = r \cdot h$$
[考克斯特数](@entry_id:185785) $h$ 本身与外尔群的 **指数 (exponents)** $\{m_1, \dots, m_r\}$ 相关。指数是描述外尔群[代数结构](@entry_id:137052)的一组整数，按惯例排序为 $1 = m_1 \le m_2 \le \dots \le m_r$。[考克斯特数](@entry_id:185785)由最大指数确定：$h = m_r + 1$。
例如，对于秩 $r=4$ 的 $F_4$ 型根系统，其外尔[群的指数](@entry_id:145655)已知为 $\{1, 5, 7, 11\}$。最大指数是 $m_4=11$，因此[考克斯特数](@entry_id:185785) $h = 11+1 = 12$。从而，$F_4$ 的总根数就是 $|\Phi(F_4)| = r \cdot h = 4 \times 12 = 48$ [@problem_id:747448]。

根的数量还可以通过外尔群[不变量](@entry_id:148850)多项式的次数来计算。根据 Chevalley-Shephard-Todd 定理，对于一个秩为 $l$ 的外尔群 $W$，其在[多项式环](@entry_id:152854)上的[不变量](@entry_id:148850)子代数是由 $l$ 个[代数无关](@entry_id:156712)的[齐次多项式](@entry_id:178156)生成的，这些生成元的次数 $d_1, \dots, d_l$ 被称为 **基本次数 (fundamental degrees)**。[正根](@entry_id:199264)的数量 $N=|\Phi^+|$ 与这些次数有如下关系：
$$N = \sum_{i=1}^{l} (d_i - 1)$$
由于外尔群中的反射与正负根对 $\{\alpha, -\alpha\}$ [一一对应](@entry_id:143935)，所以 $N$ 也等于外尔群中反射的个数。
以 $E_6$ 型根系统为例，其秩为 $l=6$，其外尔群的基本次数为 $\{2, 5, 6, 8, 9, 12\}$。因此，其[正根](@entry_id:199264)数量为：
$$N = (2-1) + (5-1) + (6-1) + (8-1) + (9-1) + (12-1) = 1+4+5+7+8+11 = 36$$
这意味着 $E_6$ [根系](@entry_id:198970)统共有 $2N = 72$ 个根，其外尔群 $W(E_6)$ 中有 $36$ 个反射 [@problem_id:747279]。这些深刻的联系展示了[根系](@entry_id:198970)统理论中代数、几何与组合的惊人统一。

### 与根系统相关的格

[根系](@entry_id:198970)统中的向量生活在一个连续的欧几里得空间中，但它们的线性组合形成了离散的结构，称为 **格 (lattice)**。与[根系](@entry_id:198970)统直接相关的两个主要格是根格和[余根](@entry_id:193338)格。

**根格 (root lattice)** $Q$ 是由所有单根的整系数线性组合构成的集合：
$$ Q = \bigoplus_{i=1}^{n} \mathbb{Z}\alpha_i $$
**[余根](@entry_id:193338)格 (coroot lattice)** $Q^\vee$ 则是由所有单[余根](@entry_id:193338)的整系数线性组合构成的集合：
$$ Q^\vee = \bigoplus_{i=1}^{n} \mathbb{Z}\alpha_i^\vee $$
对于单边根系统（如 A、D、E 型），所有根长度相同，$(\alpha_i, \alpha_i)$ 是一个常数 $c$。此时 $\alpha_i^\vee = (2/c)\alpha_i$，[余根](@entry_id:193338)格 $Q^\vee$ 只是根格 $Q$ 的一个缩放版本，两者作为格是同构的。但对于存在不同根长的根系统（如 B、C、F、G 型），情况就变得更加复杂。

让我们考察 $B_4$ 型根系统。其一组单根为 $\alpha_1 = e_1 - e_2, \alpha_2 = e_2 - e_3, \alpha_3 = e_3 - e_4, \alpha_4 = e_4$。它们的长度平方为：
$$(\alpha_1, \alpha_1) = 2, \quad (\alpha_2, \alpha_2) = 2, \quad (\alpha_3, \alpha_3) = 2, \quad (\alpha_4, \alpha_4) = 1$$
对应的单[余根](@entry_id:193338)为：
$$\alpha_1^\vee = \alpha_1, \quad \alpha_2^\vee = \alpha_2, \quad \alpha_3^\vee = \alpha_3, \quad \alpha_4^\vee = 2\alpha_4$$
可以看到，[余根](@entry_id:193338)格 $Q^\vee$ 是由 $\{\alpha_1, \alpha_2, \alpha_3, 2\alpha_4\}$ 张成的。由于 $2\alpha_4$ 是根格 $Q$ 的一个元素，所以 $Q^\vee$ 的所有[基向量](@entry_id:199546)都属于 $Q$，这意味着 $Q^\vee$ 是 $Q$ 的一个子格。

我们可以计算子格 $Q^\vee$ 在格 $Q$ 中的 **指数 (index)** $[Q:Q^\vee]$，它等于[商群](@entry_id:145113) $Q/Q^\vee$ 的阶。在几何上，这个指数等于两个格的基本区域的体积之比。对于由[基向量](@entry_id:199546) $\{v_1, \dots, v_n\}$ 张成的格，其基本区域的体积是 $|\det(M)|$，其中 $M$ 是将这些[基向量](@entry_id:199546)按列[排列](@entry_id:136432)构成的矩阵。
对于 $B_4$，以标准基 $\{e_i\}$ 表示，根格 $Q$ 的基矩阵 $M_Q$ 和[余根](@entry_id:193338)格 $Q^\vee$ 的基矩阵 $M_{Q^\vee}$ 分别是：
$$ M_Q = \begin{pmatrix} 1  0  0  0 \\ -1  1  0  0 \\ 0  -1  1  0 \\ 0  0  -1  1 \end{pmatrix}, \quad M_{Q^\vee} = \begin{pmatrix} 1  0  0  0 \\ -1  1  0  0 \\ 0  -1  1  0 \\ 0  0  -1  2 \end{pmatrix} $$
它们的[行列式](@entry_id:142978)分别为 $\det(M_Q) = 1$ 和 $\det(M_{Q^\vee}) = 2$。因此，指数为：
$$[Q:Q^\vee] = \frac{|\det(M_{Q^\vee})|}{|\det(M_Q)|} = \frac{2}{1} = 2$$
这表明对于 $B_4$ 根系统，根格的基本区域体积是[余根](@entry_id:193338)格基本区域体积的一半 [@problem_id:747439]。这个指数也等于卡丹矩阵的行列式 $|\det(A)|$，对于 $B_4$，$|\det(A)| = 2$。这个非平凡的指数反映了根系统非单边的特性。这些格及其相互关系在李代数的[表示论](@entry_id:137998)中扮演着至关重要的角色。