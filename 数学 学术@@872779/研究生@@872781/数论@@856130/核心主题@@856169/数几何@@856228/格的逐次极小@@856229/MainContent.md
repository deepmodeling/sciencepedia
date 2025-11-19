## 引言
在几何数论领域，格的**逐次最小值（Successive Minima）**是一个核心概念，它为量化一个格在欧氏空间中的几何结构提供了比其[行列式](@entry_id:142978)更为精细的度量。虽然格的[行列式](@entry_id:142978)描述了格点的平均“稀疏度”，但它无法捕捉格点在不同方向上的[分布](@entry_id:182848)情况。逐次最小值正是为了填补这一认知空白而生，它精确地描述了一个格相对于一个给定的几何形状（[凸体](@entry_id:183909)）在各个维度上的“密度”。

本文旨在系统地介绍逐次最小值的理论框架及其深远影响。我们将从最基本的定义出发，逐步构建这一强大工具的理论体系，并展示其如何将抽象的几何洞察转化为解决具体数学问题的有力武器。在接下来的章节中，你将学到：

- 在 **“原理与机制”** 一章中，我们将建立逐次最小值的形式化定义，探讨其基本性质，并深入剖析几何数论的两大基石——Minkowski第一和第二定理。此外，我们还将揭示逐次最小值与堆积、覆盖等基本几何概念以及深刻的对偶性原理之间的联系。

- 在 **“应用与交叉学科联系”** 一章中，我们将探索这些理论原理的实际威力，展示逐次最小值如何在[代数数论](@entry_id:148067)中揭示理想和[单位群](@entry_id:184012)的结构，如何为[丢番图逼近](@entry_id:199334)问题提供几何化的解决方案，以及如何驱动格基约化等现代计算算法。

- 最后，在 **“动手实践”** 部分，你将通过解决一系列精心设计的具体问题，亲手计算和应用逐次最小值，从而将抽象的理论知识内化为坚实的分析技能。

通过这一系列的学习，读者将能够全面掌握逐次最小值的概念，并理解其作为连接纯粹几何、[代数结构](@entry_id:137052)与算法实践的关键桥梁所扮演的重要角色。

## 原理与机制

继前一章介绍几何数论的基本背景之后，本章将深入探讨格的逐次最小值的核心原理与机制。我们将从格与[凸体](@entry_id:183909)的基本定义出发，系统地建立逐次最小值的概念，阐明其基本性质，并介绍其在现代数论中两个最核心的定理——Minkowski第一和第二定理。最后，我们将通过几个关键应用，揭示逐次最小值如何与其他重要的[几何不变量](@entry_id:178611)（如堆积半径、覆盖半径和[Hermite常数](@entry_id:203913)）联系起来，并探讨其与对偶性的深刻关系。

### 基本概念：格与[凸体](@entry_id:183909)

#### 格及其[行列式](@entry_id:142978)

在几何数论中，**格 (lattice)** 是 $\mathbb{R}^n$ 中一个离散的加法[子群](@entry_id:146164)。一个**满秩格 (full-rank lattice)** $\Lambda \subset \mathbb{R}^n$ 可以由 $\mathbb{R}^n$ 的一组基 $b_1, \dots, b_n$ 生成，其形式为这些[基向量](@entry_id:199546)的所有整系数[线性组合](@entry_id:154743)的集合：
$$
\Lambda = \left\{ \sum_{i=1}^n z_i b_i : z_i \in \mathbb{Z} \right\}
$$
这组[线性无关](@entry_id:148207)的向量 $\{b_1, \dots, b_n\}$ 称为格 $\Lambda$ 的一组**基 (basis)**。若我们将这些[基向量](@entry_id:199546)作为列向量构成一个 $n \times n$ 矩阵 $B = (b_1 | \dots | b_n)$，则格可以简洁地表示为 $\Lambda = \{Bz : z \in \mathbb{Z}^n\}$。

与格的基 $B$ 相关联的一个重要几何对象是**基本平行[多面体](@entry_id:637910) (fundamental parallelepiped)**，它是一个半开集：
$$
P = \left\{ \sum_{i=1}^n t_i b_i : t_i \in [0, 1) \right\} = \{Bt : t \in [0, 1)^n\}
$$
这个集合构成了 $\mathbb{R}^n$ 的一个**[基本域](@entry_id:201756) (fundamental domain)**。这意味着，$\mathbb{R}^n$ 中的任意向量 $v$ 都可以唯一地表示为一个格点 $x \in \Lambda$ 与[基本域](@entry_id:201756)中一个点 $p \in P$ 的和，即 $v = x + p$。因此，[基本域](@entry_id:201756)的格平移 $\{x+P\}_{x \in \Lambda}$ 构成了对整个空间 $\mathbb{R}^n$ 的一个无重叠内部的完美覆盖或**铺砌 (tiling)**。

**格的[行列式](@entry_id:142978) (determinant)**，记作 $\det(\Lambda)$，定义为任何一个[基本域](@entry_id:201756)的 $n$ 维勒贝格测度（即体积）。根据多元微积分中的[换元积分法](@entry_id:144683)则，基本平行多面体 $P$ 的体积 $\mu(P)$ 可以通过其到单位立方体 $[0,1)^n$ 的[线性映射](@entry_id:185132) $B$ 计算得出：
$$
\det(\Lambda) = \mu(P) = |\det(B)|
$$
这个值也被称为格的**[协体积](@entry_id:186549) (covolume)**，它衡量了格点的“稀疏”程度：[行列式](@entry_id:142978)越大，格点[分布](@entry_id:182848)越稀疏。值得注意的是，格的[行列式](@entry_id:142978)不应与基的**格拉姆矩阵 (Gram matrix)** $G = B^\top B$ 的[行列式](@entry_id:142978)混淆。两者之间的关系是 $\det(G) = (\det B)^2 = (\det \Lambda)^2$。

格的基不是唯一的。任何两组基 $B$ 和 $B'$ 之间通过一个**[幺模矩阵](@entry_id:148345) (unimodular matrix)** $U \in \mathrm{GL}_n(\mathbb{Z})$ 相联系，即 $B' = BU$。这里 $\mathrm{GL}_n(\mathbb{Z})$ 是所有 $n \times n$ 整系数且具有整系数逆的矩阵构成的群。由于幺模[矩阵的[行列](@entry_id:148198)式](@entry_id:142978)为 $\pm 1$，因此 $|\det(U)| = 1$。这意味着改变格的基不会改变格本身，也不会改变格的[行列式](@entry_id:142978)的值：
$$
\det(\Lambda') = |\det(B')| = |\det(BU)| = |\det(B)||\det(U)| = |\det(B)| = \det(\Lambda)
$$
这种不变性至关重要，它保证了格的[行列式](@entry_id:142978)是格的内在属性，不依赖于基的选择。然而，如果用一个普通的非奇异实矩阵 $A \in \mathrm{GL}_n(\mathbb{R})$ 作用于基，通常会得到一个不同的格，其[行列式](@entry_id:142978)也会相应地改变。

#### [凸体](@entry_id:183909)与[Minkowski泛函](@entry_id:274530)

我们的研究对象不仅包括离散的格，还包括连续的几何体。一个**中心对称[凸体](@entry_id:183909) (centrally symmetric convex body)** $K \subset \mathbb{R}^n$ 是一个满足以下条件的集合：
1.  **凸性 (Convexity)**：对任意 $x, y \in K$ 和任意 $t \in [0, 1]$，都有 $tx + (1-t)y \in K$。
2.  **[中心对称](@entry_id:144242)性 (Central Symmetry)**：$K = -K$，即如果 $x \in K$，那么 $-x \in K$。
3.  **紧性 (Compactness)**：$K$ 是 $\mathbb{R}^n$ 中的[闭集](@entry_id:136446)和[有界集](@entry_id:157754)。
4.  **非[空内部](@entry_id:147624) (Non-empty Interior)**：$K$ 包含一个以原点为中心的[开球](@entry_id:143668)。

与这类[凸体](@entry_id:183909)相关联的是**[Minkowski泛函](@entry_id:274530) (Minkowski functional)** 或**[规范函数](@entry_id:749731) (gauge)**，定义为：
$$
\lVert x \rVert_K = \inf\{ \lambda > 0 : x \in \lambda K \}
$$
对于一个中心对称[凸体](@entry_id:183909) $K$，其[Minkowski泛函](@entry_id:274530) $\lVert \cdot \rVert_K$ 在 $\mathbb{R}^n$ 上定义了一个**范数 (norm)**，其[单位球](@entry_id:142558) $\{x \in \mathbb{R}^n : \lVert x \rVert_K \le 1\}$ 正是[凸体](@entry_id:183909) $K$ 本身。这为我们提供了一种强大的工具，可以用代数的方式来描述几何体的伸缩。两个最重要的例子是[欧几里得范数](@entry_id:172687)和[上确界范数](@entry_id:145717)对应的单位球：
-   **欧几里得球 (Euclidean ball)**：$B_2^n = \{x \in \mathbb{R}^n : \lVert x \rVert_2 \le 1\}$，其中 $\lVert x \rVert_2 = \sqrt{\sum_{i=1}^n x_i^2}$。
-   **[超立方体](@entry_id:273913) (Hypercube)**：$B_\infty^n = \{x \in \mathbb{R}^n : \lVert x \rVert_\infty \le 1\}$，其中 $\lVert x \rVert_\infty = \max_{i} |x_i|$。

### 逐次最小值的定义

现在我们结合格与[凸体](@entry_id:183909)这两个概念，来定义本章的核心研究对象——逐次最小值。

#### 形式化定义

逐次最小值的直观思想是：将一个[中心对称](@entry_id:144242)[凸体](@entry_id:183909) $K$ 从原点开始均匀地“吹大”，并观察它在什么尺度下能“捕获”到足够多的[线性无关](@entry_id:148207)的格点。

对于一个满秩格 $\Lambda \subset \mathbb{R}^n$ 和一个中心对称[凸体](@entry_id:183909) $K \subset \mathbb{R}^n$，第 $i$ 个**逐次最小值 (successive minimum)** $\lambda_i(K, \Lambda)$ ($i=1, \dots, n$) 被定义为：
$$
\lambda_i(K, \Lambda) = \inf\{ \lambda > 0 : \dim \operatorname{span}_{\mathbb{R}}((\lambda K) \cap \Lambda) \ge i \}
$$
其中 $\operatorname{span}_{\mathbb{R}}(\cdot)$ 表示集合中所有向量在实数域 $\mathbb{R}$ 上张成的[线性子空间](@entry_id:151815)的维度。

这个定义等价于一个更具描述性的说法：$\lambda_i(K, \Lambda)$ 是使得伸缩体 $\lambda K$ 包含 $\Lambda$ 中至少 $i$ 个线性无关向量的最小伸缩因子 $\lambda$。**[线性无关](@entry_id:148207)**的要求是这个定义的核心，它确保了我们是在探索格在不同维度方向上的“密度”，而不仅仅是计算落入体内的格点数量。如果去掉这个要求，只计算不同格点的数量，我们将无法得到深刻的几何定理，比如Minkowski第二定理就会失效。

特别地，第一个逐次最小值 $\lambda_1(K, \Lambda)$ 就是使得 $\lambda K$ 包含第一个非零格点的最小伸缩因子。用[Minkowski泛函](@entry_id:274530)来表达，它就是格中最“短”的非零向量的长度：
$$
\lambda_1(K, \Lambda) = \min_{x \in \Lambda \setminus \{0\}} \lVert x \rVert_K
$$

#### 基本性质

逐次最小值的定义直接导出了一系列重要的性质：

1.  **单调性 (Monotonicity)**：逐次最小值构成一个[非递减序列](@entry_id:139501)：
    $$
    \lambda_1(K, \Lambda) \le \lambda_2(K, \Lambda) \le \dots \le \lambda_n(K, \Lambda)
    $$
    这是因为，如果一个伸缩体 $\lambda K$ 包含了 $i+1$ 个[线性无关](@entry_id:148207)的格点，它必然也包含了 $i$ 个[线性无关](@entry_id:148207)的格点。

2.  **伸缩性 (Scaling)**：如果[凸体](@entry_id:183909) $K$ 被缩放了 $t$ 倍（$t>0$），则逐次最小值会相应地被缩放 $1/t$ 倍：
    $$
    \lambda_i(tK, \Lambda) = \frac{\lambda_i(K, \Lambda)}{t}
    $$
    这是因为 $(\lambda/t)(tK) = \lambda K$，所以捕获相同格点所需的伸缩因子成反比。

3.  **包含性 (Inclusion)**：如果一个[凸体](@entry_id:183909) $K$ 包含在另一个[凸体](@entry_id:183909) $L$ 中（$K \subset L$），那么用 $K$ 来测量会更“困难”，因此其逐次最小值会更大：
    $$
    \lambda_i(K, \Lambda) \ge \lambda_i(L, \Lambda)
    $$
    这是因为在相同的伸缩因子 $\lambda$下，$\lambda K \cap \Lambda \subset \lambda L \cap \Lambda$，所以 $\lambda L$ 能捕获的线性无关向量至少和 $\lambda K$ 一样多。

4.  **[线性变换](@entry_id:149133)下的不变性 (Invariance under Linear Maps)**：逐次最小值在同时对格和[凸体](@entry_id:183909)施加同一个[可逆线性变换](@entry_id:149915) $A \in \mathrm{GL}_n(\mathbb{R})$ 时保持不变：
    $$
    \lambda_i(AK, A\Lambda) = \lambda_i(K, \Lambda)
    $$
    这是因为线性变换保持了[线性无关](@entry_id:148207)性，并且 $v \in \lambda K \iff Av \in A(\lambda K) = \lambda(AK)$。这个性质表明逐次最小值是格与[凸体](@entry_id:183909)之间相对几何关系的度量。然而，如果只对其中一个对象进行变换，例如考虑 $\lambda_i(AK, \Lambda)$，其值通常会改变。

#### 一个直观的例子：标准整格 $\mathbb{Z}^n$

为了建立对逐次最小值的直观理解，我们来计算标准整格 $\Lambda = \mathbb{Z}^n$ 关于两个标准[凸体](@entry_id:183909)——欧几里得球 $B_2^n$ 和[超立方体](@entry_id:273913) $B_\infty^n$ 的逐次最小值。

-   **对于欧几里得球 $K=B_2^n$**：$\lambda_1(B_2^n, \mathbb{Z}^n)$ 是 $\mathbb{Z}^n$ 中最短非[零向量](@entry_id:156189)的欧几里得长度。显然，[标准基向量](@entry_id:152417) $e_k$（第 $k$ 个分量为1，其余为0）的长度为 $\lVert e_k \rVert_2 = 1$，并且没有更短的非零整数向量。因此，$\lambda_1(B_2^n, \mathbb{Z}^n) = 1$。
    现在考虑 $\lambda_n(B_2^n, \mathbb{Z}^n)$。我们需要找到包含 $n$ 个线性无关的整格向量的最小伸缩球。[标准基向量](@entry_id:152417) $\{e_1, \dots, e_n\}$ 本身就是 $n$ 个[线性无关](@entry_id:148207)的整格向量，且它们的长度都为1。这意味着当伸缩因子 $\lambda=1$ 时，伸缩球 $1 \cdot B_2^n$ 已经包含了这 $n$ 个向量。因此，$\lambda_n(B_2^n, \mathbb{Z}^n) \le 1$。
    结合[单调性](@entry_id:143760) $1 = \lambda_1 \le \dots \le \lambda_n \le 1$，我们得出结论：
    $$
    \lambda_i(B_2^n, \mathbb{Z}^n) = 1 \quad \text{for all } i=1, \dots, n
    $$

-   **对于超立方体 $K=B_\infty^n$**：同样地，$\lambda_1(B_\infty^n, \mathbb{Z}^n)$ 是 $\mathbb{Z}^n$ 中非[零向量](@entry_id:156189)的最小[上确界范数](@entry_id:145717)。[标准基向量](@entry_id:152417) $e_k$ 的[上确界范数](@entry_id:145717)为 $\lVert e_k \rVert_\infty = 1$，且没有更小的值。因此，$\lambda_1(B_\infty^n, \mathbb{Z}^n) = 1$。
    与上面类似，[标准基向量](@entry_id:152417) $\{e_1, \dots, e_n\}$ 都位于单位[超立方体](@entry_id:273913) $1 \cdot B_\infty^n$ 内，所以 $\lambda_n(B_\infty^n, \mathbb{Z}^n) \le 1$。
    因此，我们也得到：
    $$
    \lambda_i(B_\infty^n, \mathbb{Z}^n) = 1 \quad \text{for all } i=1, \dots, n
    $$

这个例子表明，对于高度对称的格和[凸体](@entry_id:183909)，所有逐次最小值可能相等。在更一般的情况下，它们的值会分散开，揭示出格与[凸体](@entry_id:183909)在不同方向上的相互作用。

### [Minkowski定理](@entry_id:204587)及其意义

Hermann Minkowski 的工作奠定了现代几何数论的基础，他的两个核心定理揭示了格、[凸体](@entry_id:183909)体积和逐次最小值之间的深刻联系。

#### Minkowski第一定理

Minkowski第一定理给出了一个保证[凸体](@entry_id:183909)内部存在非零格点的充分条件。

**Minkowski第一定理**：设 $\Lambda \subset \mathbb{R}^n$ 是一个满秩格， $K \subset \mathbb{R}^n$ 是一个中心对称[凸体](@entry_id:183909)。如果 $K$ 的体积满足 $\operatorname{vol}(K) > 2^n \det(\Lambda)$，则 $K$ 至少包含一个 $\Lambda$ 中的非零格点。

这个定理可以用逐次最小值来重新表述。$\lambda_1(K, \Lambda)$ 的定义意味着对于任何 $\lambda  \lambda_1(K, \Lambda)$，伸缩体 $\lambda K$ 不包含非零格点。根据Minkowski第一定理的[逆否命题](@entry_id:265332)，这要求其体积 $\operatorname{vol}(\lambda K) \le 2^n \det(\Lambda)$。由于 $\operatorname{vol}(\lambda K) = \lambda^n \operatorname{vol}(K)$，我们得到 $\lambda^n \operatorname{vol}(K) \le 2^n \det(\Lambda)$。通过取 $\lambda \to \lambda_1(K, \Lambda)$ 的极限，我们得到Minkowski第一定理的一个等价形式：
$$
\lambda_1(K, \Lambda)^n \operatorname{vol}(K) \le 2^n \det(\Lambda)
$$
这个不等式为第一个逐次最小值提供了一个[上界](@entry_id:274738)。例如，如果一个格的[行列式](@entry_id:142978)为1，且[凸体](@entry_id:183909) $K$ 的体积大于 $2^n$，则必然有 $\lambda_1(K, \Lambda)  1$。

然而，该定理的逆命题不成立。即，即使 $\operatorname{vol}(K) \le 2^n \det(\Lambda)$，也可能存在 $\lambda_1(K, \Lambda)  1$ 的情况。例如，考虑一个在 $x$ 轴方向上很长但在 $y$ 轴方向上很扁的矩形 $K$，其面积可以很小，但它仍然可以轻易地包含 $(\pm 1, 0)$ 这两个格点。

#### Minkowski第二定理

Minkowski第二定理是第一定理的深刻推广，它将所有 $n$ 个逐次最小值与格的[行列式](@entry_id:142978)和[凸体](@entry_id:183909)的体积联系在一起。

**Minkowski第二定理**：设 $\Lambda \subset \mathbb{R}^n$ 是一个满秩格， $K \subset \mathbb{R}^n$ 是一个[中心对称](@entry_id:144242)[凸体](@entry_id:183909)。则 $n$ 个逐次最小值 $\lambda_i = \lambda_i(K, \Lambda)$ 的乘积满足以下双边不等式：
$$
\frac{2^n}{n!} \le \frac{\operatorname{vol}(K)}{\det(\Lambda)} \prod_{i=1}^n \lambda_i(K, \Lambda) \le 2^n
$$
这个定理的成立严格依赖于 $K$ 的**[中心对称](@entry_id:144242)性**和**[凸性](@entry_id:138568)**。

这个定理的意义是巨大的：
-   **上界**：$\left(\prod \lambda_i\right) \operatorname{vol}(K) \le 2^n \det(\Lambda)$。这可以看作是第一定理的加强版。由于 $\lambda_1 \le \lambda_i$ 对所有 $i$ 成立，我们有 $\lambda_1^n \le \prod \lambda_i$，所以 $ \lambda_1^n \operatorname{vol}(K) \le \left(\prod \lambda_i\right) \operatorname{vol}(K) \le 2^n \det(\Lambda) $，这恢复了第一定理。
-   **下界**：$\left(\prod \lambda_i\right) \operatorname{vol}(K) \ge \frac{2^n}{n!} \det(\Lambda)$。这个下界更为精妙，它表明逐次最小值的乘积不能太小。这意味着如果格在某些方向上非常“密集”（即某些 $\lambda_i$ 很小），那么为了补偿，它在其他方向上必须非常“稀疏”（即某些 $\lambda_j$ 很大），以维持乘积的下限。

值得注意的是，由逐次最小值定义所确定的 $n$ 个[线性无关](@entry_id:148207)的格点 $v_1, \dots, v_n$（满足 $\lVert v_i \rVert_K \approx \lambda_i$）不一定能构成格 $\Lambda$ 的一组基。它们可能只生成 $\Lambda$ 的一个子格。

### 应用与相关概念

逐次最小值不仅是理论上的抽象概念，它们还与许多具体的几何量和数论问题密切相关。

#### 几何解释：堆积与覆盖

逐次最小值与格的两个基本几何操作——**堆积 (packing)** 和 **覆盖 (covering)** ——直接相关。

-   **堆积半径 (Packing Radius)** $r_{\mathrm{pack}}(K, \Lambda)$ 定义为能使以格点为中心的、内部互不相交的 $rK$ 平移体族的最大半径 $r$。两个平移体 $x+rK$ 和 $y+rK$（$x, y \in \Lambda, x \neq y$）不相交的条件是 $x-y \notin 2rK$。为了对所有非零格向量 $x-y$ 都成立，我们必须有 $(2r)K$ 不包含任何非零格点。这等价于 $2r  \lambda_1(K, \Lambda)$。因此，堆积半径与第一个逐次最小值有精确的关系：
    $$
    r_{\mathrm{pack}}(K, \Lambda) = \frac{1}{2} \lambda_1(K, \Lambda)
    $$
    这为 $\lambda_1$ 提供了一个非常直观的几何意义：它决定了可以用给定的“形状”$K$ 进行的最密集的格堆积的尺寸。

-   **覆盖半径 (Covering Radius)** $\rho(K, \Lambda)$ 定义为使得以格点为中心的 $rK$ 平移体族能够覆盖整个空间 $\mathbb{R}^n$ 的最小半径 $r$。覆盖半径与所有逐次最小值都有关。可以证明它满足以下不等式：
    $$
    \frac{1}{2} \lambda_1(K, \Lambda) \le \rho(K, \Lambda) \le \frac{1}{2} \sum_{i=1}^n \lambda_i(K, \Lambda)
    $$
    右侧的不等式进一步可以放宽为 $\rho(K, \Lambda) \le \frac{n}{2} \lambda_n(K, \Lambda)$。这表明，虽然 $\lambda_1$ 控制了堆积，但覆盖整个空间则需要考虑所有方向上的格点[分布](@entry_id:182848)，这由整个逐次最小值谱 $\lambda_1, \dots, \lambda_n$ 共同决定。

#### 应用于[球堆积](@entry_id:268295)：[Hermite常数](@entry_id:203913)

逐次最小值理论的一个经典应用是研究**[球堆积问题](@entry_id:200186) (sphere packing problem)**，即在 $n$ 维空间中如何最密集地堆积相同大小的球体。对于格堆积，这个问题转化为寻找使得[堆积密度](@entry_id:138204)最大的格。

[堆积密度](@entry_id:138204) $\Delta(\Lambda)$ 是球体体积与格的[基本域](@entry_id:201756)体积之比。对于以欧几里得球 $B_2^n$ 为形状的堆积，其最大半径为 $r_{\mathrm{pack}} = \frac{1}{2} \lambda_1(B_2^n, \Lambda)$。[堆积密度](@entry_id:138204)因此为：
$$
\Delta(\Lambda) = \frac{\operatorname{vol}(r_{\mathrm{pack}} B_2^n)}{\det(\Lambda)} = \frac{(\frac{1}{2}\lambda_1)^n \operatorname{vol}(B_2^n)}{\det(\Lambda)} = \frac{\operatorname{vol}(B_2^n)}{2^n} \frac{\lambda_1(B_2^n, \Lambda)^n}{\det(\Lambda)}
$$
为了比较不同尺度的格的[堆积效率](@entry_id:138204)，我们定义一个尺度无关的量。**[Hermite常数](@entry_id:203913) (Hermite constant)** $\gamma_n$ 正是为此而生：
$$
\gamma_n = \sup_{\Lambda \subset \mathbb{R}^n} \frac{\lambda_1(B_2^n, \Lambda)^2}{(\det \Lambda)^{2/n}}
$$
其中上确界取遍 $\mathbb{R}^n$ 中所有的满秩格。这个量是[尺度不变的](@entry_id:178566)，因此我们可以把[上确界](@entry_id:140512)限制在所有[行列式](@entry_id:142978)为1的格上。Minkowski第一定理保证了 $\gamma_n$ 对任意 $n$ 都是有限的。

通过[Hermite常数](@entry_id:203913)的定义，我们可以将最大格[堆积密度](@entry_id:138204) $\Delta_n = \sup_{\Lambda} \Delta(\Lambda)$ 与 $\gamma_n$ 直接联系起来：
$$
\Delta_n = \frac{\operatorname{vol}(B_2^n)}{2^n} \gamma_n^{n/2}
$$
这表明，寻找最密集的格堆积等价于寻找使 $\lambda_1^2 / (\det \Lambda)^{2/n}$ 达到最大值的格，即寻找[Hermite常数](@entry_id:203913)的极值格。

#### 格点在原点附近的结构

逐次最小值还精确地描述了原点附近格点的[分布](@entry_id:182848)结构。由定义可知，当伸缩因子 $t  \lambda_1(K, \Lambda)$ 时，伸缩体 $tK$ 中唯一的格点是原点。当 $t$ 增长到 $\lambda_1(K, \Lambda) \le t  \lambda_2(K, \Lambda)$ 时，情况变得有趣。

在这个区间内，$tK$ 包含了非零格点，但它所包含的所有非零格点都必须是**[线性相关](@entry_id:185830)**的。由于格是离散的，这意味着所有这些点都必须位于同一条穿过原点的直线上，即它们都是某个**本原格向量 (primitive lattice vector)** $v_0$ 的整数倍。$v_0$ 是实现第一个最小值的最短向量之一。

我们可以精确地计算出在这个区间内 $tK$ 中包含的格点数量 $N(t) = |\Lambda \cap tK|$。这些点形如 $kv_0$，其中 $k \in \mathbb{Z}$。一个点 $kv_0$ 位于 $tK$ 中的条件是 $\lVert kv_0 \rVert_K \le t$，即 $|k| \lVert v_0 \rVert_K \le t$。由于 $\lVert v_0 \rVert_K = \lambda_1(K, \Lambda)$，我们得到 $|k| \le t / \lambda_1(K, \Lambda)$。

满足这个条件的非零整数 $k$ 的数量是 $2 \lfloor t / \lambda_1(K, \Lambda) \rfloor$。加上原点本身，我们得到：
$$
N(t) = 1 + 2 \left\lfloor \frac{t}{\lambda_1(K, \Lambda)} \right\rfloor \quad \text{for } 0  t  \lambda_2(K, \Lambda)
$$
这个公式清晰地展示了格点是如何以“量子化”的方式，沿着最短向量的方向，随着 $t$ 的增加逐对（正负）进入[凸体](@entry_id:183909)的。$\lambda_2$ 的值标志着第二个独立方向上的格点开始进入的临界尺度。

### 对偶性原理

在几何数论中，对偶性是一个极其强大的工具，它在格和[凸体](@entry_id:183909)之间建立了深刻的联系。

#### [对偶格](@entry_id:150046)与极体

对于[欧几里得空间](@entry_id:138052) $\mathbb{R}^n$ 中的一个满秩格 $\Lambda$，其**[对偶格](@entry_id:150046) (dual lattice)** $\Lambda^*$ 定义为：
$$
\Lambda^* = \{ y \in \mathbb{R}^n : \langle y, x \rangle \in \mathbb{Z} \text{ for all } x \in \Lambda \}
$$
[对偶格](@entry_id:150046)本身也是一个满秩格。如果 $\Lambda$ 的一个基矩阵是 $B$，那么 $\Lambda^*$ 的一个基矩阵是 $(B^{-1})^\top$。[对偶格](@entry_id:150046)的[行列式](@entry_id:142978)与原格的[行列式](@entry_id:142978)之间有一个简单的倒数关系：
$$
\det(\Lambda) \cdot \det(\Lambda^*) = 1
$$
对于一个中心对称[凸体](@entry_id:183909) $K$，其**极体 (polar body)** $K^\circ$ 定义为：
$$
K^\circ = \{ y \in \mathbb{R}^n : \langle y, x \rangle \le 1 \text{ for all } x \in K \}
$$
极体本身也是一个中心对称[凸体](@entry_id:183909)。如果 $K$ 是一个闭[凸体](@entry_id:183909)且包含原点，那么我们有**[对偶定理](@entry_id:137804) (Bipolar Theorem)**：$(K^\circ)^\circ = K$。

[对偶格](@entry_id:150046)和极体在[可逆线性变换](@entry_id:149915) $A \in \mathrm{GL}_n(\mathbb{R})$ 下表现出一种“逆变”的行为：
$$
(A\Lambda)^* = (A^{-1})^\top \Lambda^* \quad \text{and} \quad (AK)^\circ = (A^{-1})^\top K^\circ
$$
这种对称的变换性质暗示了它们之间存在深刻的联系。

#### 对偶性与逐次最小值

对偶性的力量在逐次最小值理论中体现得淋漓尽致。一个基本问题是：格 $\Lambda$ 关于 $K$ 的逐次最小值与[对偶格](@entry_id:150046) $\Lambda^*$ 关于极体 $K^\circ$ 的逐次最小值之间有什么关系？

答案由一系列被称为**传递定理 (transference theorems)** 的结果给出。其中最著名的是由 Kurt Mahler 证明的一个结果，它为这两个序列的逐次最小值乘积提供了双边界定：
$$
1 \le \lambda_i(K, \Lambda) \lambda_{n-i+1}(K^\circ, \Lambda^*) \le C_n
$$
其中 $i=1, \dots, n$，而 $C_n$ 是一个只依赖于维度 $n$ 的常数（例如，一个已知的界是 $C_n = (n!)^2$）。

这个定理揭示了一种惊人的对偶关系：如果格 $\Lambda$ 在 $K$ 的某个“方向”上很密集（即 $\lambda_i(K, \Lambda)$ 很小），那么[对偶格](@entry_id:150046) $\Lambda^*$ 在极体 $K^\circ$ 相应的对偶“方向”上就必须很稀疏（即 $\lambda_{n-i+1}(K^\circ, \Lambda^*)$ 很大），反之亦然。这种深刻的[对偶原理](@entry_id:276615)是几何数论中许多高级应用的基础，它将我们对格的几何理解提升到了一个新的层次。