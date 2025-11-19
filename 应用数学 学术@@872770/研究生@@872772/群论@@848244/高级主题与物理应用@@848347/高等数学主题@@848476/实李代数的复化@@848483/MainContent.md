## 引言
实李代数的[复化](@entry_id:260775)是[李理论](@entry_id:148240)中的一个核心概念，它通过将[实数域](@entry_id:151347)上的[代数结构](@entry_id:137052)延拓至[复数域](@entry_id:153768)，构建了一座连接实[李代数](@entry_id:137954)与[复李代数](@entry_id:204650)世界的关键桥梁。许多在物理学和几何学中自然出现的对称性由实[李代数](@entry_id:137954)描述，但它们的结构和表示理论往往比[复数域](@entry_id:153768)上的对应物更为复杂和多样。本文旨在系统性地解决这一问题，展示如何通过[复化](@entry_id:260775)这一工具，利用复[半单李代数](@entry_id:190073)完整而优美的理论来分析和理解实[李代数](@entry_id:137954)。在接下来的内容中，我们将分三部分展开：第一章“原理与机制”将深入探讨[复化](@entry_id:260775)的定义、[实形式](@entry_id:193866)的概念以及它如何影响代数的基本结构；第二章“应用与跨学科联系”将展示[复化](@entry_id:260775)在解决物理学、几何学问题中的强大威力；最后，“动手实践”部分将通过具体计算问题，帮助读者巩固所学知识。

## 原理与机制

继引言部分对[李代数](@entry_id:137954)[复化](@entry_id:260775)这一主题的概述之后，本章将深入探讨其背后的基本原理和核心机制。我们将从最基础的[向量空间](@entry_id:151108)结构开始，逐步引入[李代数](@entry_id:137954)的[代数结构](@entry_id:137052)，并最终揭示[复化](@entry_id:260775)作为一种强大工具，如何在李代数的分类、结构分解和[表示论](@entry_id:137998)中发挥关键作用。

### 始于[向量空间](@entry_id:151108)：[复化](@entry_id:260775)的定义与[复结构](@entry_id:269128)

从根本上说，一个实李代数首先是一个实[向量空间](@entry_id:151108)。因此，理解其[复化](@entry_id:260775)的第一步是理解如何将一个实[向量空间](@entry_id:151108)“扩展”为一个[复向量空间](@entry_id:264355)。

给定一个实[向量空间](@entry_id:151108) $V$，其**[复化](@entry_id:260775) (complexification)**，记作 $V_\mathbb{C}$，可以通过张量积来形式化地定义为 $V_\mathbb{C} = V \otimes_\mathbb{R} \mathbb{C}$。尽管这个定义在形式上是严谨的，但一个更直观且在实践中非常有用的观点是，将 $V_\mathbb{C}$ 视为由形如 $v_1 + i v_2$ 的形式和构成的集合，其中 $v_1, v_2 \in V$。这里的 $i$ 是虚数单位，满足 $i^2 = -1$。

在这个集合上，向量加法和复标量乘法被自然地定义：
对于 $v_1, v_2, w_1, w_2 \in V$ 和 $\alpha + i\beta \in \mathbb{C}$ (其中 $\alpha, \beta \in \mathbb{R}$)，我们有：
- **加法**: $(v_1 + i v_2) + (w_1 + i w_2) = (v_1 + w_1) + i(v_2 + w_2)$
- **复[标量乘法](@entry_id:155971)**: $(\alpha + i\beta) (v_1 + i v_2) = (\alpha v_1 - \beta v_2) + i(\alpha v_2 + \beta v_1)$

通过这种构造，如果 $V$ 是一个 $n$ 维的实[向量空间](@entry_id:151108)，那么 $V_\mathbb{C}$ 就成为了一个 $n$ 维的[复向量空间](@entry_id:264355)。一个重要的观察是，任何[复向量空间](@entry_id:264355)也可以被视为一个实[向量空间](@entry_id:151108)。如果 $V_\mathbb{C}$ 的复维度为 $n$，那么它作为实[向量空间](@entry_id:151108)的维度就是 $2n$。

这种视角引出了**[复结构](@entry_id:269128) (complex structure)** 的概念。在一个[复向量空间](@entry_id:264355) $W$ 上，乘以虚数单位 $i$ 的运算可以被看作是一个作用于其下层实[向量空间](@entry_id:151108)的实[线性算子](@entry_id:149003)。我们定义这个算子为 $J: W \to W$，其作用为 $J(w) = iw$。显然，$J$ 是实线性的（即 $J(aw+bv) = aJ(w)+bJ(v)$ 对所有 $a, b \in \mathbb{R}$ 成立），并且满足 $J^2 = -I$，其中 $I$ 是[恒等算子](@entry_id:204623)。

让我们考虑一个具体的例子。设 $\mathfrak{g} = \mathfrak{u}(n)$，即所有 $n \times n$ 阶复[斜埃尔米特矩阵](@entry_id:153530)构成的实[李代数](@entry_id:137954)。其[复化](@entry_id:260775)是 $\mathfrak{g}_\mathbb{C} = \mathfrak{gl}(n, \mathbb{C})$，即所有 $n \times n$ 阶[复矩阵](@entry_id:190650)构成的空间。$\mathfrak{gl}(n, \mathbb{C})$ 的复维度是 $n^2$，因此其作为实[向量空间](@entry_id:151108)的维度是 $2n^2$。我们可以考察复结构算子 $J$ 在这个 $2n^2$ 维实空间上的迹。要计算这个迹，我们可以选择一个方便的基。对于 $\mathfrak{gl}(n, \mathbb{C})$ 中的任何一个[基向量](@entry_id:199546) $E_k$，我们可以将它和一个新的向量 $J(E_k) = iE_k$ 配对，构成一个二维的实[子空间](@entry_id:150286)。在这个[子空间](@entry_id:150286)中，基为 $\{E_k, iE_k\}$，算子 $J$ 的作用是 $J(E_k) = iE_k$ 和 $J(iE_k) = i(iE_k) = -E_k$。因此，在这个基下，$J$ 的[矩阵表示](@entry_id:146025)是 $\begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}$，其迹为 0。由于整个空间可以分解为 $n^2$ 个这样的二维[子空间](@entry_id:150286)的[直和](@entry_id:156782)，算子 $J$ 在整个空间上的矩阵表示是块[对角形式](@entry_id:264850)，每个块都是上述的 $2 \times 2$ 矩阵。因此，$J$ 的总迹是 $n^2 \times 0 = 0$ [@problem_id:646673]。

### 实[李代数](@entry_id:137954)的[复化](@entry_id:260775)

现在我们将[代数结构](@entry_id:137052)——李括号——引入讨论。给定一个实李代数 $\mathfrak{g}$，其[李括号](@entry_id:636461)为 $[\cdot, \cdot]_\mathfrak{g}$。我们可以在其[复化](@entry_id:260775)[向量空间](@entry_id:151108) $\mathfrak{g}_\mathbb{C}$ 上定义一个李括号，使其成为一个[复李代数](@entry_id:204650)。这个新的李括号通过 $\mathbb{C}$-线性性从 $\mathfrak{g}$ 的括号自然延伸而来。对于 $\mathfrak{g}_\mathbb{C}$ 中的任意两个元素 $X = X_1 + iY_1$ 和 $Y = X_2 + iY_2$（其中 $X_1, Y_1, X_2, Y_2 \in \mathfrak{g}$），它们的李括号定义为：
$$
[X, Y]_{\mathfrak{g}_\mathbb{C}} = [X_1 + iY_1, X_2 + iY_2] = ([X_1, X_2]_\mathfrak{g} - [Y_1, Y_2]_\mathfrak{g}) + i([X_1, Y_2]_\mathfrak{g} + [Y_1, X_2]_\mathfrak{g})
$$
可以验证，这个新定义的括号满足双线性（在[复数域](@entry_id:153768)上）、反交换性和雅可比恒等式，因此 $\mathfrak{g}_\mathbb{C}$ 确实是一个[复李代数](@entry_id:204650)。

[复化](@entry_id:260775)过程如何影响[李代数](@entry_id:137954)的代数性质？一个基本问题是代数的中心会发生什么变化。李代数 $\mathfrak{h}$ 的中心 $Z(\mathfrak{h})$ 定义为与所有元素交换的元素集合，即 $Z(\mathfrak{h}) = \{Z \in \mathfrak{h} \mid [Z, X] = 0 \text{ for all } X \in \mathfrak{h}\}$。通常情况下，$Z(\mathfrak{g}_\mathbb{C})$ 就是 $Z(\mathfrak{g})$ 的[复化](@entry_id:260775)，即 $Z(\mathfrak{g}_\mathbb{C}) \cong (Z(\mathfrak{g}))_\mathbb{C}$。

考虑实[李代数](@entry_id:137954) $\mathfrak{g} = \mathfrak{t}(2, \mathbb{R})$，即所有 $2 \times 2$ 实[上三角矩阵](@entry_id:150931)构成的李代数。其[复化](@entry_id:260775)是 $\mathfrak{g}_\mathbb{C} = \mathfrak{t}(2, \mathbb{C})$，即所有 $2 \times 2$ 复[上三角矩阵](@entry_id:150931)。为了找到 $\mathfrak{t}(2, \mathbb{C})$ 的中心，我们取一个一般元素 $Z = \begin{pmatrix} x  y \\ 0  z \end{pmatrix}$，并要求它与任意元素 $X = \begin{pmatrix} a  b \\ 0  c \end{pmatrix}$ 的交换子为零。通过直接计算：
$$
[Z, X] = ZX - XZ = \begin{pmatrix} 0  b(x-z) + y(c-a) \\ 0  0 \end{pmatrix}
$$
为了使这个矩阵对所有 $a, b, c \in \mathbb{C}$ 都为零矩阵，我们必须有 $x-z = 0$ 和 $y=0$。这意味着 $Z$ 必须是标量矩阵的形式，即 $Z = \begin{pmatrix} x  0 \\ 0  x \end{pmatrix} = xI$。因此，中心 $Z(\mathfrak{t}(2, \mathbb{C}))$是由所有[复标量](@entry_id:272141)矩阵构成的集合，它是一个一维的[复向量空间](@entry_id:264355) [@problem_id:646728]。

### [实形式](@entry_id:193866)及其分类

[复化](@entry_id:260775)的逆向过程引出了“[实形式](@entry_id:193866)”这一至关重要的概念。一个[复李代数](@entry_id:204650) $\mathfrak{g}_\mathbb{C}$ 的一个**[实形式](@entry_id:193866) (real form)** 是指一个实李子代数 $\mathfrak{g}$，使得 $\mathfrak{g}_\mathbb{C}$ 是 $\mathfrak{g}$ 的[复化](@entry_id:260775)。这等价于说 $\mathfrak{g}_\mathbb{C}$ 可以分解为 $\mathfrak{g}_\mathbb{C} = \mathfrak{g} \oplus i\mathfrak{g}$。这个分解意味着 $\mathfrak{g}_\mathbb{C}$ 中的任何元素 $Z$ 都可以被唯一地写成 $Z = X + iY$ 的形式，其中 $X, Y \in \mathfrak{g}$。

这个唯一的分解是理解和使用[实形式](@entry_id:193866)的关键。让我们以最重要的例子之一——[复李代数](@entry_id:204650) $\mathfrak{sl}(2, \mathbb{C})$（所有迹为零的 $2 \times 2$ [复矩阵](@entry_id:190650)）——来说明。这个[复李代数](@entry_id:204650)有（至少）两个重要的[实形式](@entry_id:193866)。

一个[实形式](@entry_id:193866)是 $\mathfrak{su}(2)$，即迹为零的[斜埃尔米特矩阵](@entry_id:153530)构成的实[李代数](@entry_id:137954)。$\mathfrak{sl}(2, \mathbb{C})$ 是 $\mathfrak{su}(2)$ 的[复化](@entry_id:260775)。这意味着任何 $M \in \mathfrak{sl}(2, \mathbb{C})$ 都可以唯一地写成 $M=A+iB$ 的形式，其中 $A, B \in \mathfrak{su}(2)$。给定一个 $M$，其分量 $A$ 和 $B$ 可以通过利用[埃尔米特共轭](@entry_id:191215)（记为 $\dagger$）的性质来找到。因为 $A, B$ 是斜埃尔米特的，所以 $A^\dagger = -A$ 且 $B^\dagger = -B$。于是，
$$
M^\dagger = (A+iB)^\dagger = A^\dagger + (iB)^\dagger = -A -i(B^\dagger) = -A + iB
$$
通过这个关系式和 $M=A+iB$，我们可以解出 $A$ 和 $B$：
$$
A = \frac{1}{2}(M - M^\dagger), \quad B = \frac{1}{2i}(M - M^\dagger)
$$
这与将一个复数 $z=x+iy$ 分解为实部和虚部 $x = \frac{1}{2}(z+\bar{z})$ 和 $y = \frac{1}{2i}(z-\bar{z})$ 非常相似。例如，对于矩阵 $M = \begin{pmatrix} i  k+i \\ 1-ik  -i \end{pmatrix} \in \mathfrak{sl}(2, \mathbb{C})$，其中 $k \in \mathbb{R}$，我们可以计算出其 $\mathfrak{su}(2)$ 分量 $A$ 为 $A = \frac{1}{2}(M - M^\dagger) = \begin{pmatrix} i  \frac{(k-1)(1-i)}{2} \\ \frac{(1-k)(1+i)}{2}  -i \end{pmatrix}$ [@problem_id:646710]。

另一个重要的[实形式](@entry_id:193866)是 $\mathfrak{sl}(2, \mathbb{R})$，即迹为零的实矩阵构成的[李代数](@entry_id:137954)。同样，$\mathfrak{sl}(2, \mathbb{C})$ 也是 $\mathfrak{sl}(2, \mathbb{R})$ 的[复化](@entry_id:260775)。这意味着任何 $Z \in \mathfrak{sl}(2, \mathbb{C})$ 也可以唯一地写成 $Z=X+iY$ 的形式，但这次 $X, Y \in \mathfrak{sl}(2, \mathbb{R})$。找到 $X$ 和 $Y$ 更加直接：$X$ 就是 $Z$ 的逐元素实部，而 $Y$ 是 $Z$ 的逐元素虚部。例如，对于[埃尔米特矩阵](@entry_id:155147) $H = \begin{pmatrix} \alpha  \beta + i\gamma \\ \beta - i\gamma  -\alpha \end{pmatrix}$（其中 $\alpha, \beta, \gamma \in \mathbb{R}$），它的分解是 $H = X+iY$，其中 $X = \begin{pmatrix} \alpha  \beta \\ \beta  -\alpha \end{pmatrix}$ 和 $Y = \begin{pmatrix} 0  \gamma \\ -\gamma  0 \end{pmatrix}$ 都是 $\mathfrak{sl}(2, \mathbb{R})$ 的元素 [@problem_id:646703]。

一个给定的[复李代数](@entry_id:204650)可能有多个非同构的[实形式](@entry_id:193866)。对这些[实形式](@entry_id:193866)进行分类是[李理论](@entry_id:148240)中的一个深刻问题。从理论上讲，一个[复李代数](@entry_id:204650) $\mathfrak{g}_\mathbb{C}$ 的[实形式](@entry_id:193866)与它的**共轭 (conjugation)** 算子——即满足 $\sigma^2 = I$ 的[反线性](@entry_id:268590)自同构——一一对应。[实形式](@entry_id:193866)就是相应共轭算子的[不动点子代数](@entry_id:186495) $\mathfrak{g} = \{X \in \mathfrak{g}_\mathbb{C} \mid \sigma(X) = X\}$。对于 $\mathfrak{sl}(2, \mathbb{C})$，可以证明（在同构意义下）存在且仅存在两个[实形式](@entry_id:193866)，它们分别对应两个不等价的共轭。一个是标准的逐元素复共轭 $\sigma_0(X)=\overline{X}$，其[不动点](@entry_id:156394)集正是 $\mathfrak{sl}(2, \mathbb{R})$。另一个共轭可以取为 $\sigma_1(X) = -X^\dagger$，其[不动点](@entry_id:156394)集是 $\mathfrak{su}(2)$。

区分不同[实形式](@entry_id:193866)的一个强大[不变量](@entry_id:148850)是**Killing 型 (Killing form)** 的符号差。Killing 型是[李代数](@entry_id:137954)上一个内在的[对称双线性形式](@entry_id:148281)，定义为 $K(X,Y) = \mathrm{tr}(\mathrm{ad}_X \circ \mathrm{ad}_Y)$。在实李代数上，Killing 型是一个实二次型，我们可以计算其正[特征值](@entry_id:154894)的数量 $p$ 和负[特征值](@entry_id:154894)的数量 $q$。其符号差 $(p,q)$ 是一个同构[不变量](@entry_id:148850)。
- 如果 Killing 型是负定的（即 $p=0$），则称该[实形式](@entry_id:193866)为**紧致[实形式](@entry_id:193866) (compact real form)**。
- 如果 Killing 型是混合符号的，则该[实形式](@entry_id:193866)为非紧的。其中一类重要的非紧形式是**可裂[实形式](@entry_id:193866) (split real form)**。

对于 $\mathfrak{sl}(2, \mathbb{C})$ 的两个[实形式](@entry_id:193866)：
- $\mathfrak{su}(2)$：在一个合适的基下，其 Killing 型矩阵是对角的，且对角元全为负。其符号差为 $(0,3)$。因此 $\mathfrak{su}(2)$ 是 $\mathfrak{sl}(2, \mathbb{C})$ 的紧致[实形式](@entry_id:193866)。
- $\mathfrak{sl}(2, \mathbb{R})$：在其标准基 $\{H, E, F\}$ 下，Killing 型矩阵的[特征值](@entry_id:154894)为 $\{8, 4, -4\}$。其符号差为 $(2,1)$。这是一个不定的形式，$\mathfrak{sl}(2, \mathbb{R})$ 是 $\mathfrak{sl}(2, \mathbb{C})$ 的可裂[实形式](@entry_id:193866)。

这两个[实形式](@entry_id:193866)的 Killing 型符号差之和的差值 $s=p-q$ 分别为 $s_{\mathfrak{su}(2)}=-3$ 和 $s_{\mathfrak{sl}(2, \mathbb{R})}=1$，这清晰地表明了它们是不同的[实形式](@entry_id:193866) [@problem_id:3031889]。

### [复化](@entry_id:260775)带来的[结构洞](@entry_id:138651)察

[复化](@entry_id:260775)的主要威力之一在于它能够揭示不同实[李代数](@entry_id:137954)之间隐藏的联系，并简化它们的结构理论。

#### 结构的统一
不同的实[李代数](@entry_id:137954)在[复化](@entry_id:260775)后可能变得同构。最著名的例子是旋转代数 $\mathfrak{so}(3)$（三维实反对称矩阵）和 $\mathfrak{su}(2)$。它们本身是不同构的实李代数（例如，$\mathfrak{su}(2)$ 是三维的，而 $\mathfrak{so}(3)$ 也是三维的，但它们的[李群](@entry_id:137659)性质不同），但它们的[复化](@entry_id:260775)是同构的：$\mathfrak{so}(3)_\mathbb{C} \cong \mathfrak{su}(2)_\mathbb{C}$。更进一步，它们都同构于 $\mathfrak{sl}(2, \mathbb{C})$。

这个同构 $\Phi: \mathfrak{so}(3)_\mathbb{C} \to \mathfrak{sl}(2, \mathbb{C})$ 可以通过将 $\mathfrak{so}(3)$ 的标准生成元 $L_k$（$k=1,2,3$，表示绕 $x,y,z$ 轴的[无穷小旋转](@entry_id:166635)）映射到 $\mathfrak{sl}(2, \mathbb{C})$ 中的元素来建立。一个标准的选择是 $\Phi(L_k) = -\frac{i}{2}\sigma_k$，其中 $\sigma_k$ 是[泡利矩阵](@entry_id:139493)。这个映射保持了[李括号](@entry_id:636461)结构，并可以通过线性性扩展到整个[复化](@entry_id:260775)代数 $\mathfrak{so}(3)_\mathbb{C}$。这一同构极其强大，因为它意味着 $\mathfrak{so}(3)$ 的（复）[表示论](@entry_id:137998)可以完全在 $\mathfrak{sl}(2, \mathbb{C})$ 的框架内进行研究，而后者具有更为简单和优雅的结构。例如，我们可以利用这个同构和 $\mathfrak{sl}(2, \mathbb{C})$ 上的 Killing 型公式 $K(X,Y) = 4\mathrm{tr}(XY)$ 来计算 $\mathfrak{so}(3)_\mathbb{C}$ 中元素的 Killing 型范数 [@problem_id:646627]。

#### 结构理论的简化
[复化](@entry_id:260775)同样可以简化李代数的内部结构分解。以 $\mathfrak{sl}(2, \mathbb{R})$ 的 **Cartan 分解 (Cartan decomposition)** 为例。这是一个将非紧[半单李代数](@entry_id:190073)分解为其紧致子代数[部分和](@entry_id:162077)非紧致[向量空间](@entry_id:151108)部分的构造。对于 $\mathfrak{g}_0 = \mathfrak{sl}(2, \mathbb{R})$，Cartan 分解为 $\mathfrak{g}_0 = \mathfrak{k}_0 \oplus \mathfrak{p}_0$，其中 $\mathfrak{k}_0 = \mathfrak{so}(2)$ 是反对称部分（紧致子代数），$\mathfrak{p}_0$ 是对称部分（非紧致[向量空间](@entry_id:151108)）。
- $\mathfrak{k}_0$ 由 $K = \begin{pmatrix} 0  1 \\ -1  0 \end{pmatrix}$ 张成。
- $\mathfrak{p}_0$ 由 $P_1 = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}$ 和 $P_2 = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}$ 张成。

这些[子空间](@entry_id:150286)满足交换关系：$[\mathfrak{k}_0, \mathfrak{k}_0] \subseteq \mathfrak{k}_0$，$[\mathfrak{k}_0, \mathfrak{p}_0] \subseteq \mathfrak{p}_0$，以及 $[\mathfrak{p}_0, \mathfrak{p}_0] \subseteq \mathfrak{k}_0$。
当我们对这些[子空间](@entry_id:150286)进行[复化](@entry_id:260775)时，结构变得更加清晰。特别是在[复化](@entry_id:260775)的非紧致部分 $(\mathfrak{p}_0)_\mathbb{C}$ 中，我们可以选取一组特别的[基矢](@entry_id:199546)：
$$
E_+ = \frac{1}{2}(P_1 + iP_2), \quad E_- = \frac{1}{2}(P_1 - iP_2)
$$
计算它们的[李括号](@entry_id:636461)会发现，结果落在了[复化](@entry_id:260775)的紧致部分 $(\mathfrak{k}_0)_\mathbb{C}$ 中。具体计算给出：
$$
[E_+, E_-] = -\frac{i}{2}[P_1, P_2] = -\frac{i}{2}(2K) = -iK
$$
这个结果表明 $[E_+, E_-]$ 是 $K$ 的一个纯虚数倍，验证了 $[\mathfrak{p}_0, \mathfrak{p}_0] \subseteq \mathfrak{k}_0$ 的[复化](@entry_id:260775)版本。这种在[复化](@entry_id:260775)空间中选取“升降算子” $E_\pm$ 的技巧是研究[李代数表示论](@entry_id:190569)的标准方法，它将复杂的矩阵运算转化为更易于处理的代数关系 [@problem_id:646668]。

### [实化](@entry_id:266794)及 $(\mathfrak{g}_\mathbb{R})_\mathbb{C}$ 的结构

最后，我们探讨一个与[复化](@entry_id:260775)密切相关的概念：**[实化](@entry_id:266794) (realification)**。任何一个 $n$ 维[复李代数](@entry_id:204650) $\mathfrak{g}_0$ 都可以被看作一个 $2n$ 维的实[李代数](@entry_id:137954)，记为 $(\mathfrak{g}_0)_\mathbb{R}$。我们仅仅是忘记了可以乘以非实数标量的能力，而保留了原有的[向量加法](@entry_id:155045)和[李括号](@entry_id:636461)结构。

一个自然的问题是：如果我们将这个[实化](@entry_id:266794)后的李代数 $(\mathfrak{g}_0)_\mathbb{R}$ 再次进行[复化](@entry_id:260775)，会得到什么？结果是一个维度为 $\mathfrak{g}_0$ 两倍的[复李代数](@entry_id:204650)。一个深刻的结构性结论是，这个新的代数同构于两个原始代数的[直和](@entry_id:156782)：
$$
((\mathfrak{g}_0)_\mathbb{R})_\mathbb{C} \cong \mathfrak{g}_0 \oplus \mathfrak{g}_0
$$
要理解这个同构，让我们用 $i$ 表示 $\mathfrak{g}_0$ 中原有的[复结构](@entry_id:269128)（例如[矩阵元](@entry_id:186505)中的 $i$），用 $j$ 表示[复化](@entry_id:260775)过程中引入的形式虚数单位。$((\mathfrak{g}_0)_\mathbb{R})_\mathbb{C}$ 中的元素形如 $X+jY$，其中 $X, Y \in \mathfrak{g}_0$。同构映射 $\phi$ 可以被定义为：
$$
\phi(X+jY) = (X+iY, X-iY) \in \mathfrak{g}_0 \oplus \mathfrak{g}_0
$$
这个映射是一个[李代数](@entry_id:137954)同构。这个结构在计算 Killing 型时非常有用。[直和](@entry_id:156782)代数 $\mathfrak{g}_0 \oplus \mathfrak{g}_0$ 上的 Killing 型是两个分量上 Killing 型的和。例如，在 $((\mathfrak{sl}(2, \mathbb{C}))_\mathbb{R})_\mathbb{C}$ 中，如果一个元素 $Z$ 对应于[直和](@entry_id:156782)中的 $(H, -H)$，那么其 Killing 型范数为 $K(Z, Z) = K_{\mathfrak{sl}(2, \mathbb{C})}(H,H) + K_{\mathfrak{sl}(2, \mathbb{C})}(-H,-H) = 2K_{\mathfrak{sl}(2, \mathbb{C})}(H,H)$。由于在 $\mathfrak{sl}(2, \mathbb{C})$ 中 $K(H,H)=8$，我们得到 $K(Z,Z) = 16$ [@problem_id:646699]。

这个[实化](@entry_id:266794)与[复化](@entry_id:260775)的过程也揭示了实[李代数](@entry_id:137954)和[复李代数](@entry_id:204650)上 Killing 型之间的直接关系。对于一个[复李代数](@entry_id:204650) $\mathfrak{g}$，其 Killing 型 $K_\mathbb{C}$ 是复[双线性](@entry_id:146819)的。对于其作为实李代数的[实化](@entry_id:266794) $\mathfrak{g}_\mathbb{R}$，其 Killing 型 $K_\mathbb{R}$ 是实[双线性](@entry_id:146819)的。两者之间的关系为：
$$
K_\mathbb{R}(X, Y) = 2 \cdot \mathrm{Re}(K_\mathbb{C}(X, Y))
$$
其中 $\mathrm{Re}$ 表示取复数的实部。这个关系源于一个更普遍的事实，即任何复线性算子 $T$ 在一个 $n$ 维[复向量空间](@entry_id:264355)上的迹，与其作为实[线性算子](@entry_id:149003)在对应的 $2n$ 维实[向量空间](@entry_id:151108)上的迹相关，关系为 $\mathrm{tr}_\mathbb{R}(T) = 2 \mathrm{Re}(\mathrm{tr}_\mathbb{C}(T))$ [@problem_id:646744]。

这种双重结构也反映在表示论中。如果我们从一个[复李代数](@entry_id:204650) $\mathfrak{g}_0$ 的一个不可约表示 $(\pi, V)$ 开始，将其视为[实化](@entry_id:266794)代数 $(\mathfrak{g}_0)_\mathbb{R}$ 的一个[实表示](@entry_id:146117)，然后再将这个[实表示](@entry_id:146117)[复化](@entry_id:260775)，那么得到的[复表示](@entry_id:144331)不再是不可约的。它会分解为两个不可约分量的[直和](@entry_id:156782)：
$$
W_\mathbb{C} = (V_\mathbb{R})_\mathbb{C} \cong V \oplus \bar{V}
$$
其中 $V$ 是原始表示空间，而 $\bar{V}$ 是其[共轭表示](@entry_id:139136)空间。这两个分量分别对应于同构 $\mathfrak{g}_0 \oplus \mathfrak{g}_0$ 中的两个副本 [@problem_id:646573]。这一现象是理解复[半单李代数](@entry_id:190073)的[实表示](@entry_id:146117)的关键。

综上所述，[复化](@entry_id:260775)和[实化](@entry_id:266794)是研究李[代数结构](@entry_id:137052)的两个互补且强大的工具。它们不仅提供了在实与复领域之间转换的途径，更重要的是，它们揭示了不同代数之间的深刻联系，简化了[结构分析](@entry_id:153861)，并为表示论提供了清晰的框架。