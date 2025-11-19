## 引言
在几何学与物理学中，精确描述旋转和[刚体运动](@entry_id:193355)是一个基础而核心的问题。[正交群](@entry_id:152531) $O(n)$ 与[特殊正交群](@entry_id:146418) $SO(n)$ 为此提供了统一而强大的数学语言。它们不仅是抽象的[代数结构](@entry_id:137052)，更是理解对称性、坐标变换和动力学定律不变性的关键。然而，初学者往往难以将这些群的抽象定义（如矩阵条件 $A^T A = I$）与其丰富的几何意义、深刻的拓扑内涵以及在物理世界中的具体应用联系起来。本文旨在弥合这一差距，系统地引导读者穿越 $SO(n)$ 的理论与实践。

本文将分为三个核心章节。在“原理与机制”中，我们将从第一性原理出发，深入剖析 $O(n)$ 和 $SO(n)$ 的代数、几何与拓扑性质，并揭示它们与其[李代数](@entry_id:137954) $\mathfrak{so}(n)$ 之间的内在联系。接着，在“应用与跨学科联系”中，我们将展示这些理论如何在[刚体动力学](@entry_id:142040)、微分几何和连续介质力学等领域中发挥作用，将抽象概念与具体问题相结合。最后，通过“动手实践”部分，读者将有机会通过解决具体问题来巩固所学知识，将理论转化为可操作的技能。

## 原理与机制

在对[几何变换](@entry_id:150649)（尤其是[刚体运动](@entry_id:193355)）的研究中，[正交群](@entry_id:152531)和[特殊正交群](@entry_id:146418)扮演着核心角色。本章将深入探讨这些矩阵群的代数、几何与[拓扑性质](@entry_id:141605)，并阐述它们与其关联的[李代数](@entry_id:137954)之间的深刻联系。我们将从基本定义出发，逐步揭示这些数学对象的内在结构与运作机制。

### [正交群](@entry_id:152531) $O(n)$：定义与几何意义

#### 代数定义

**[正交群](@entry_id:152531) (Orthogonal Group)**，记作 $O(n)$，是所有 $n \times n$ 实数矩阵 $A$ 构成的集合，其满足以下代数条件：
$$
A^T A = I
$$
其中 $A^T$ 是矩阵 $A$ 的[转置](@entry_id:142115)，$I$ 是 $n \times n$ 单位矩阵。这个条件蕴含了几个重要的推论。首先，由于 $A$ 是方阵，该条件也等价于 $A A^T = I$。其次，它表明 $A$ 的[逆矩阵](@entry_id:140380)恰好是其[转置](@entry_id:142115)矩阵，即 $A^{-1} = A^T$。拥有[逆矩阵](@entry_id:140380)保证了 $A$ 是可逆的。可以验证，满足此条件的矩阵集合在矩阵乘法下构成一个群：乘法封闭性、存在单位元（单位矩阵 $I$ 自身满足 $I^T I = I$）、每个元素都存在逆元。

#### 几何解释：保持原点的等距变换

[正交群](@entry_id:152531)的代数定义背后，隐藏着深刻的几何意义。一个[线性变换](@entry_id:149133) $A$ 属于 $O(n)$ 的充要条件是它保持向量的**标准[内积](@entry_id:158127) (Euclidean inner product)**。考虑 $\mathbb{R}^n$ 中的任意两个向量 $\mathbf{u}$ 和 $\mathbf{v}$，它们经过变换 $A$ 后变为 $A\mathbf{u}$ 和 $A\mathbf{v}$。这两个新向量的[内积](@entry_id:158127)（[点积](@entry_id:149019)）为：
$$
(A\mathbf{u}) \cdot (A\mathbf{v}) = (A\mathbf{u})^T (A\mathbf{v}) = \mathbf{u}^T A^T A \mathbf{v}
$$
由于 $A \in O(n)$，我们有 $A^T A = I$，因此上式简化为：
$$
\mathbf{u}^T I \mathbf{v} = \mathbf{u}^T \mathbf{v} = \mathbf{u} \cdot \mathbf{v}
$$
这个结果表明，正交变换保持了任意两个向量之间的[内积](@entry_id:158127)。这一性质是正交变换的核心。[@problem_id:1656356]

从[内积](@entry_id:158127)保持性可以直接导出两个关键的几何推论：

1.  **长度保持**：一个向量 $\mathbf{u}$ 的欧几里得范数（长度）的平方由 $\|\mathbf{u}\|^2 = \mathbf{u} \cdot \mathbf{u}$ 定义。由于[内积](@entry_id:158127)被保持，我们有 $\|A\mathbf{u}\|^2 = (A\mathbf{u}) \cdot (A\mathbf{u}) = \mathbf{u} \cdot \mathbf{u} = \|\mathbf{u}\|^2$。因此，$\|A\mathbf{u}\| = \|\mathbf{u}\|$。这意味着[正交变换](@entry_id:155650)不改变任何向量的长度。这种保持长度的变换称为**等距变换 (isometry)**。

2.  **角度保持**：两个非[零向量](@entry_id:156189) $\mathbf{u}$ 和 $\mathbf{v}$ 之间的夹角 $\theta$ 由公式 $\cos(\theta) = \frac{\mathbf{u} \cdot \mathbf{v}}{\|\mathbf{u}\| \|\mathbf{v}\|}$ 确定。经过正交变换 $A$ 后，新向量之间的夹角 $\phi$ 满足：
    $$
    \cos(\phi) = \frac{(A\mathbf{u}) \cdot (A\mathbf{v})}{\|A\mathbf{u}\| \|A\mathbf{v}\|} = \frac{\mathbf{u} \cdot \mathbf{v}}{\|\mathbf{u}\| \|\mathbf{v}\|} = \cos(\theta)
    $$
    由于 $\theta, \phi \in [0, \pi]$，这表明 $\phi=\theta$。也就是说，[正交变换](@entry_id:155650)也保持向量之间的夹角。[@problem_id:1656356]

综上所述，$O(n)$ 中的元素代表了 $\mathbb{R}^n$ 空间中所有保持原点固定的**[刚性变换](@entry_id:140326)**，即不产生任何形变的变换，它们由**旋转 (rotation)** 和**反射 (reflection)** 组成。

#### [标准正交基](@entry_id:147779)解释

$A^T A = I$ 这个矩阵方程还可以从另一个角度理解。若我们将矩阵 $A$ 的列向量记为 $\mathbf{c}_1, \mathbf{c}_2, \dots, \mathbf{c}_n$，即 $A = [\mathbf{c}_1 | \mathbf{c}_2 | \dots | \mathbf{c}_n]$，那么矩阵 $A^T$ 的行向量就是这些列向量的转置。此时，$A^T A$ 的 $(i, j)$ 元等于第 $i$ 个行向量（即 $\mathbf{c}_i^T$）与第 $j$ 个列向量（即 $\mathbf{c}_j$）的乘积，这正是它们的[点积](@entry_id:149019)：
$$
(A^T A)_{ij} = \mathbf{c}_i \cdot \mathbf{c}_j
$$
由于 $A^T A = I$，我们有 $(A^T A)_{ij} = \delta_{ij}$（Kronecker delta，当 $i=j$ 时为1，否则为0）。因此，
$$
\mathbf{c}_i \cdot \mathbf{c}_j = \delta_{ij}
$$
这个条件表明，矩阵 $A$ 的所有列向量构成 $\mathbb{R}^n$ 的一组**标准正交基 (orthonormal basis)**。反之，若一个矩阵的列向量构成[标准正交基](@entry_id:147779)，它必定是[正交矩阵](@entry_id:169220)。同理，从 $A A^T = I$ 可以推断出其行向量也构成一组标准正交基。[@problem_id:1656342]

### [特殊正交群](@entry_id:146418) $SO(n)$：旋转与定向

#### [行列式](@entry_id:142978)性质

[正交矩阵](@entry_id:169220)的一个关键代数性质涉及其[行列式](@entry_id:142978)。对 $A^T A = I$ 两边取[行列式](@entry_id:142978)，并利用 $\det(A^T) = \det(A)$ 和 $\det(AB) = \det(A)\det(B)$ 的性质，我们得到：
$$
\det(A^T A) = \det(A^T) \det(A) = (\det(A))^2 = \det(I) = 1
$$
这个简单的方程揭示了一个重要的事实：任何正交矩阵 $A \in O(n)$ 的[行列式](@entry_id:142978)必须是 $1$ 或 $-1$。[@problem_id:1656361]

这个二元选择将[正交群](@entry_id:152531) $O(n)$ 分为两个不相交的[子集](@entry_id:261956)。

#### $SO(n)$ 的定义

[行列式](@entry_id:142978)为 $1$ 的[正交矩阵](@entry_id:169220)构成了 $O(n)$ 的一个重要[子群](@entry_id:146164)，称为**[特殊正交群](@entry_id:146418) (Special Orthogonal Group)**，记作 $SO(n)$：
$$
SO(n) = \{ A \in O(n) \mid \det(A) = 1 \}
$$
可以验证 $SO(n)$ 确实是一个群：[单位矩阵](@entry_id:156724) $I$ 的[行列式](@entry_id:142978)为1；若 $\det(A)=1$ 且 $\det(B)=1$，则 $\det(AB) = \det(A)\det(B)=1$；若 $\det(A)=1$，则 $\det(A^{-1}) = \det(A^T) = \det(A) = 1$。

[行列式](@entry_id:142978)为 $+1$ 的变换通常被称为**旋转**或**[真旋转](@entry_id:141831) (proper rotations)**。而[行列式](@entry_id:142978)为 $-1$ 的变换（它们不构成一个群，因为不包含单位元）则代表了包含反射的[刚性变换](@entry_id:140326)，例如单一的反射或旋转与[反射的复合](@entry_id:173247)，被称为**非[真旋转](@entry_id:141831) (improper rotations)**。

#### 定向保持

[行列式](@entry_id:142978)的值与变换对空间**定向 (orientation)** 的影响密切相关。一个基的定向可以通俗地理解为其“手性”（例如三维空间中的[右手系](@entry_id:166669)或左手系）。

在三维空间 $\mathbb{R}^3$ 中，由三个列向量 $\mathbf{c}_1, \mathbf{c}_2, \mathbf{c}_3$ 构成的矩阵 $A$ 的[行列式](@entry_id:142978)等于这三个向量的**[标量三重积](@entry_id:177480) (scalar triple product)**：
$$
\det(A) = (\mathbf{c}_1 \times \mathbf{c}_2) \cdot \mathbf{c}_3
$$
如果一组基是**[右手系](@entry_id:166669)**，其标量三重积为正；如果是**左手系**，则为负。因此：
-   如果 $A \in SO(3)$，则 $\det(A) = 1$，意味着变换将一个标准正交右手基（如[单位矩阵](@entry_id:156724)的列向量）映射到另一个[右手系](@entry_id:166669)标准正交基。这种变换保持了空间的定向。
-   如果 $A \in O(3)$ 但 $A \notin SO(3)$，则 $\det(A) = -1$，意味着变换将右手基映射到了左手基，从而反转了空间的定向。[@problem_id:1656361]

对于 $SO(3)$ 中的矩阵，其列向量 $\{\mathbf{c}_1, \mathbf{c}_2, \mathbf{c}_3\}$ 构成一个[右手系](@entry_id:166669)标准正交基。这不仅意味着 $\mathbf{c}_i \cdot \mathbf{c}_j = \delta_{ij}$，还蕴含着它们之间的叉积关系。由于 $\mathbf{c}_1 \times \mathbf{c}_2$ 是一个同时垂直于 $\mathbf{c}_1$ 和 $\mathbf{c}_2$ 的[单位向量](@entry_id:165907)，它必然等于 $\pm \mathbf{c}_3$。通过[标量三重积](@entry_id:177480)可以确定其符号：
$$
(\mathbf{c}_1 \times \mathbf{c}_2) \cdot \mathbf{c}_3 = \det(A) = 1
$$
由于 $(\pm \mathbf{c}_3) \cdot \mathbf{c}_3 = \pm \|\mathbf{c}_3\|^2 = \pm 1$，我们必须选择正号。因此，对于 $SO(3)$，我们有循环关系：
$$
\mathbf{c}_1 \times \mathbf{c}_2 = \mathbf{c}_3, \quad \mathbf{c}_2 \times \mathbf{c}_3 = \mathbf{c}_1, \quad \mathbf{c}_3 \times \mathbf{c}_1 = \mathbf{c}_2
$$
这精确地刻画了[右手系](@entry_id:166669)标准正交基的几何结构。[@problem_id:1656342]

### $O(n)$ 与 $SO(n)$ 的[拓扑性质](@entry_id:141605)

作为所有 $n \times n$ [矩阵空间](@entry_id:261335) $M_n(\mathbb{R}) \cong \mathbb{R}^{n^2}$ 的[子集](@entry_id:261956)，我们可以研究 $O(n)$ 和 $SO(n)$ 的拓扑性质，如紧致性和连通性。

#### 紧致性

在[欧几里得空间](@entry_id:138052)中，一个集合是**紧致的 (compact)** 当且仅当它是**[闭集](@entry_id:136446) (closed)** 且**有界的 (bounded)**（Heine-Borel 定理）。

1.  **有界性**：对于任意矩阵 $A \in O(n)$，其列向量 $\mathbf{c}_j$ 都是单位向量，即 $\sum_{i=1}^n A_{ij}^2 = 1$。矩阵的[弗罗贝尼乌斯范数](@entry_id:143384) (Frobenius norm) 平方为所有元素平方和，因此：
    $$
    \|A\|_F^2 = \sum_{i,j=1}^n A_{ij}^2 = \sum_{j=1}^n \left( \sum_{i=1}^n A_{ij}^2 \right) = \sum_{j=1}^n 1 = n
    $$
    这意味着 $O(n)$ 中的所有矩阵都位于 $\mathbb{R}^{n^2}$ 空间中半径为 $\sqrt{n}$ 的球面上。因此，$O(n)$ 是有界的。[@problem_id:1656360]

2.  **闭性**：考虑一个[连续函数](@entry_id:137361) $f: M_n(\mathbb{R}) \to M_n(\mathbb{R})$ 定义为 $f(A) = A^T A$。由于矩阵乘法和[转置](@entry_id:142115)都是连续操作，所以 $f$ 是连续的。$O(n)$ 是单点集 $\{I\}$ 在 $f$ 下的[原像](@entry_id:150899)，即 $O(n) = f^{-1}(\{I\})$。由于单点集是[闭集](@entry_id:136446)，其在[连续函数](@entry_id:137361)下的原像也是[闭集](@entry_id:136446)。因此 $O(n)$ 是[闭集](@entry_id:136446)。$SO(n)$ 可以表示为 $O(n) \cap \det^{-1}(\{1\})$，是两个[闭集](@entry_id:136446)的交集，因此也是[闭集](@entry_id:136446)。[@problem_id:1656360]

由于 $O(n)$ 和 $SO(n)$ 既是[闭集](@entry_id:136446)也是[有界集](@entry_id:157754)，它们都是 $M_n(\mathbb{R})$ 中的紧致集。

#### 连通性

一个[拓扑空间](@entry_id:155056)是**连通的 (connected)**，如果它不能被分成两个不相交的非空开集。

考虑[行列式](@entry_id:142978)函数 $\det: O(n) \to \mathbb{R}$。这是一个[连续函数](@entry_id:137361)，其像集（值的范围）我们已经知道是[离散集](@entry_id:146023)合 $\{-1, 1\}$。如果 $O(n)$ 是连通的，那么根据拓扑学基本定理，其在连续映射下的像也必须是连通的。但 $\{-1, 1\}$ 显然是不连通的。因此，唯一的结论是 $O(n)$ 本身是**不连通的 (disconnected)**。[@problem_id:1656376]

$O(n)$ 被[行列式](@entry_id:142978)的值分成了两个部分：$SO(n) = \det^{-1}(1)$ 和 $\det^{-1}(-1)$。这两部分都是开集也是[闭集](@entry_id:136446)（在 $O(n)$ 的[子空间拓扑](@entry_id:147159)中），它们构成了 $O(n)$ 的两个**连通分支 (connected components)**。可以证明，$SO(n)$ 本身是**路径连通的 (path-connected)**（任何两个[旋转矩阵](@entry_id:140302)都可以通过一条连续的旋转路径相连），包含反射的那个分支也是[路径连通](@entry_id:148704)的。

### [李代数](@entry_id:137954) $\mathfrak{so}(n)$：[无穷小旋转](@entry_id:166635)

#### [斜对称矩阵](@entry_id:155998)

李群理论提供了一个强大的工具，通过研究群在单位元附近的“无穷小”行为来理解整个群的结构。考虑一条通过单位元的平滑路径 $A(t) \in SO(n)$，且 $A(0)=I$。这条路径代表了一个连续的旋转过程。在 $t=0$ 时刻的“速度”或“[无穷小生成元](@entry_id:270424)”由该路径的导数给出：
$$
X = \dot{A}(0) = \frac{d}{dt}A(t)\bigg|_{t=0}
$$
由于对于所有 $t$，路径上的矩阵都满足 $A(t)^T A(t) = I$，我们可以对这个方程求导：
$$
\frac{d}{dt}(A(t)^T A(t)) = \dot{A}(t)^T A(t) + A(t)^T \dot{A}(t) = 0
$$
在 $t=0$ 处计算，并利用 $A(0)=I$ 和 $\dot{A}(0)=X$：
$$
X^T I + I^T X = 0 \implies X^T + X = 0 \quad \text{或} \quad X^T = -X
$$
这个条件 $X^T = -X$ 定义了**[斜对称矩阵](@entry_id:155998) (skew-symmetric matrix)**。所有 $n \times n$ 实斜对称矩阵的集合构成了 $SO(n)$（以及 $O(n)$）的**[李代数](@entry_id:137954) (Lie algebra)**，记作 $\mathfrak{so}(n)$。

#### [向量空间](@entry_id:151108)结构与李括号

$\mathfrak{so}(n)$ 具有重要的[代数结构](@entry_id:137052)。首先，它是一个[向量空间](@entry_id:151108)：任意两个斜对称矩阵的[线性组合](@entry_id:154743)仍然是斜对称的。例如，在二维情况下，任何斜对称矩阵都可以写成 $A(\omega) = \begin{pmatrix} 0  -\omega \\ \omega  0 \end{pmatrix}$ 的形式。两个这样的矩阵的线性组合 $c_1 A(\omega_1) + c_2 A(\omega_2)$ 显然也是一个具有相同形式的[斜对称矩阵](@entry_id:155998)。[@problem_id:1656354]

除了[向量空间](@entry_id:151108)结构，李代数还有一个额外的[二元运算](@entry_id:152272)，称为**李括号 (Lie bracket)**，对于[矩阵李代数](@entry_id:204591)，它被定义为**[交换子](@entry_id:158878) (commutator)**：
$$
[X, Y] = XY - YX
$$
对于 $\mathfrak{so}(n)$，如果 $X, Y \in \mathfrak{so}(n)$，那么它们的[李括号](@entry_id:636461) $[X, Y]$ 也属于 $\mathfrak{so}(n)$。我们可以验证这一点：
$$
[X, Y]^T = (XY - YX)^T = (XY)^T - (YX)^T = Y^T X^T - X^T Y^T
$$
因为 $X, Y$ 是斜对称的 ($X^T=-X, Y^T=-Y$)，所以：
$$
(-Y)(-X) - (-X)(-Y) = YX - XY = -(XY - YX) = -[X, Y]
$$
这证明了 $[X,Y]$ 也是斜对称的。[李代数](@entry_id:137954)在其李括号运算下是封闭的。[@problem_id:1656374]

#### $\mathfrak{so}(3)$ 与帽映射

对于 $n=3$ 的情况，$\mathfrak{so}(3)$ 中的矩阵具有以下形式：
$$
X = \begin{pmatrix} 0  -c  b \\ c  0  -a \\ -b  a  0 \end{pmatrix}
$$
这个矩阵完全由三个实数 $a, b, c$ 确定。这表明 $\mathfrak{so}(3)$ 是一个三维[向量空间](@entry_id:151108)，与我们熟悉的三维[欧几里得空间](@entry_id:138052) $\mathbb{R}^3$ 同构。

这个同构关系可以通过**帽映射 (hat map)** 显式地建立。它将一个向量 $\mathbf{v} = (v_1, v_2, v_3)^T \in \mathbb{R}^3$ 映射到一个矩阵 $\hat{\mathbf{v}} \in \mathfrak{so}(3)$：
$$
\hat{\mathbf{v}} = \begin{pmatrix} 0  -v_3  v_2 \\ v_3  0  -v_1 \\ -v_2  v_1  0 \end{pmatrix}
$$
这个映射的精妙之处在于，矩阵 $\hat{\mathbf{v}}$ 对另一个向量 $\mathbf{x}$ 的作用等同于向量 $\mathbf{v}$ 与 $\mathbf{x}$ 的**叉积 (cross product)**：
$$
\hat{\mathbf{v}}\mathbf{x} = \mathbf{v} \times \mathbf{x}
$$
因此，$\mathfrak{so}(3)$ 中的元素（[无穷小旋转](@entry_id:166635)）与 $\mathbb{R}^3$ 中的向量（旋转轴和[角速度](@entry_id:192539)）[一一对应](@entry_id:143935)。[@problem_id:1656380]

更进一步，$\mathfrak{so}(3)$ 中的李括号运算与 $\mathbb{R}^3$ 中的[叉积](@entry_id:156672)运算通过帽映射联系起来，满足著名的**[雅可比恒等式](@entry_id:140480) (Jacobi identity)** 的一个变体：
$$
[\hat{\mathbf{u}}, \hat{\mathbf{v}}] = \widehat{\mathbf{u} \times \mathbf{v}}
$$
这意味着两个[无穷小旋转](@entry_id:166635)的交换子对应于它们的生成向量的叉积所生成的[无穷小旋转](@entry_id:166635)。这揭示了[旋转的非交换性](@entry_id:167347)在无穷小层面上的根源。[@problem_id:1656374]

### [指数映射](@entry_id:137184)：从代数到群

[李代数](@entry_id:137954) $\mathfrak{so}(n)$ 描述了无穷小的旋转，而李群 $SO(n)$ 描述了有限的旋转。连接这两者的桥梁是**[矩阵指数](@entry_id:139347)映射 (matrix exponential map)**：
$$
\exp(X) = \sum_{k=0}^{\infty} \frac{1}{k!}X^{k} = I + X + \frac{1}{2!}X^2 + \dots
$$
一个基本而深刻的结果是：如果 $X$ 是一个李代数元素（即一个斜对称矩阵），那么 $\exp(X)$ 是一个对应的[李群](@entry_id:137659)元素（即一个特殊[正交矩阵](@entry_id:169220)）。
$$
X \in \mathfrak{so}(n) \implies \exp(X) \in SO(n)
$$
这可以被看作是将一个具有恒定“[角速度](@entry_id:192539)” $X$ 的[无穷小旋转](@entry_id:166635)，通过“积分”一段时间（单位时间），得到一个有限的旋转。

#### 示例：从 $\mathfrak{so}(2)$ 到 $SO(2)$

这个过程在 $n=2$ 时最为清晰。考虑 $\mathfrak{so}(2)$ 中的一个通用元素 $X = \begin{pmatrix} 0  -a \\ a  0 \end{pmatrix}$。我们来计算它的指数。首先计算 $X$ 的幂：
$$
X^2 = \begin{pmatrix} 0  -a \\ a  0 \end{pmatrix} \begin{pmatrix} 0  -a \\ a  0 \end{pmatrix} = \begin{pmatrix} -a^2  0 \\ 0  -a^2 \end{pmatrix} = -a^2 I
$$
$$
X^3 = -a^2 X, \quad X^4 = (-a^2)^2 I = a^4 I, \quad \dots
$$
将这些代入指数级数，并按 $I$ 和 $X$ 的系数分组：
\begin{align*}
\exp(X)  = I + X + \frac{1}{2!}X^2 + \frac{1}{3!}X^3 + \frac{1}{4!}X^4 + \dots \\
 = \left(1 - \frac{a^2}{2!} + \frac{a^4}{4!} - \dots \right)I + \left(a - \frac{a^3}{3!} + \frac{a^5}{5!} - \dots \right) \frac{1}{a}X \\
 = (\cos a)I + (\sin a)\frac{1}{a}X
\end{align*}
代入 $I$ 和 $X$ 的矩阵形式：
$$
\exp(X) = \cos a \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} + \sin a \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix} = \begin{pmatrix} \cos a  -\sin a \\ \sin a  \cos a \end{pmatrix}
$$
结果正是 $SO(2)$ 中表示逆时针旋转角度 $a$ 的标准[旋转矩阵](@entry_id:140302)。这个例子完美地展示了[李代数](@entry_id:137954)中的元素（由参数 $a$ 定义）如何通过指数映射生成李群中的一个有限旋转（角度为 $a$）。[@problem_id:1656385]