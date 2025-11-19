## 引言
代数拓扑学的核心目标之一，是利用代数[不变量](@entry_id:148850)来研究和区分拓扑空间。同调群作为一套强大的[不变量](@entry_id:148850)，为我们提供了洞察空间“孔洞”结构的代数视角。然而，对于大多数有趣的空间，直接从定义出发计算其同调群是一项艰巨甚至不可能完成的任务。这引出了一个根本性的问题：我们能否将一个复杂的[空间分解](@entry_id:755142)为更简单的、我们已经理解的部分，然后像拼拼图一样，从这些部分的代数信息中重构出整体的同调结构？

[Mayer-Vietoris序列](@entry_id:161286)正是对这个问题强有力的回答。它是同调论中的“[分而治之](@entry_id:273215)”策略，一个将拓扑分解与[代数结构](@entry_id:137052)完美结合的定理。它告诉我们，一个空间分裂成两块时，其同调群并非简单相加，而是通过一个称为“[长正合序列](@entry_id:153438)”的精巧代数机器相互关联。理解并掌握这个工具，是打开高效[计算同调](@entry_id:161051)群大门的关键。

本文将带领您系统地探索[Mayer-Vietoris序列](@entry_id:161286)。在“**原理与机制**”一章中，我们将深入其定理陈述、剖析其核心部件——[连接同态](@entry_id:160713)的几何意义，并掌握其基本计算策略。随后，在“**应用与跨学科联系**”一章中，我们将见证该序列在计算各种重要[拓扑空间](@entry_id:155056)（从球面到[纽结补空间](@entry_id:264989)）同调群时的威力，并探索其与微分几何等领域的联系。最后，在“**动手实践**”部分，您将有机会通过解决具体问题来巩固所学知识，将理论真正转化为计算能力。

## 原理与机制

在“引言”中，我们了解了[代数拓扑学](@entry_id:138192)的核心目标之一，即利用代数[不变量](@entry_id:148850)来研究和区分[拓扑空间](@entry_id:155056)。同调论为我们提供了这样一套强大的[不变量](@entry_id:148850)——同调群。然而，直接从定义出发计算一个复杂空间的同调群往往是极其困难的。我们需要一种系统性的方法，能够将一个复杂[空间分解](@entry_id:755142)为更简单的部分，并通过这些部分的同调信息来推断整体的同调信息。Mayer-Vietoris 序列正是实现这一目标的核心工具。本章将深入探讨其原理、内在机制，并通过一系列应用展示其强大的计算能力。

### Mayer-Vietoris 序列：定理陈述

Mayer-Vietoris 序列是一个代数学和拓扑学相结合的强大构造，它将一个[空间分解](@entry_id:755142)为两个[子集](@entry_id:261956)的并集，并建立起这几个空间（并集、两个[子集](@entry_id:261956)、它们的交集）的同调群之间的一个[长正合序列](@entry_id:153438)。

**定理 (Mayer-Vietoris 序列)**：设 $X$ 是一个拓扑空间，并且 $A$ 和 $B$ 是 $X$ 的两个**开**[子集](@entry_id:261956)，满足 $X = A \cup B$。那么，存在一个[连接同态](@entry_id:160713) $\partial_n: H_n(X) \to H_{n-1}(A \cap B)$，使得以下序列对于所有整数 $n$ 都是正合的：

$$
\cdots \to H_n(A \cap B) \xrightarrow{\Phi_n} H_n(A) \oplus H_n(B) \xrightarrow{\Psi_n} H_n(X) \xrightarrow{\partial_n} H_{n-1}(A \cap B) \to \cdots
$$

这个序列称为 $X$ 关于开覆盖 $\{A, B\}$ 的 **Mayer-Vietoris 序列**。

序列中的同态定义如下：
- $\Phi_n$ 是由包含映射 $i_A: A \cap B \hookrightarrow A$ 和 $i_B: A \cap B \hookrightarrow B$ 诱导的。对于任意同调类 $[z] \in H_n(A \cap B)$，$\Phi_n([z]) = ((i_A)_*([z]), -(i_B)_*([z]))$。注意这里的负号，它对于序列的正合性至关重要。
- $\Psi_n$ 是由包含映射 $j_A: A \hookrightarrow X$ 和 $j_B: B \hookrightarrow X$ 诱导的。对于任意一对同调类 $([u], [v]) \in H_n(A) \oplus H_n(B)$，$\Psi_n([u], [v]) = (j_A)_*([u]) + (j_B)_*([v])$。

除了上述的标准形式，还有一个非常实用的**简约同调 (reduced homology)** 版本。如果交集 $A \cap B$非空，该序列对于简约同调群 $\tilde{H}_n$ 同样成立：

$$
\cdots \to \tilde{H}_n(A \cap B) \xrightarrow{\Phi_n} \tilde{H}_n(A) \oplus \tilde{H}_n(B) \xrightarrow{\Psi_n} \tilde{H}_n(X) \xrightarrow{\partial_n} \tilde{H}_{n-1}(A \cap B) \to \cdots
$$

简约序列在处理道路[连通空间](@entry_id:156017)时特别有用，因为对于道路[连通空间](@entry_id:156017) $Y$，$\tilde{H}_0(Y) = 0$，这常常能简化序列的末端。

定理中强调 $A$ 和 $B$ 必须是**开集**，这一点至关重要。如果这个条件不满足，序列可能不再正合。让我们通过一个例子来理解这一点 [@problem_id:1687849]。考虑 $\mathbb{R}^2$ 中的两个不相交的[闭圆盘](@entry_id:148403)：$A = \{ (x,y) \mid (x+2)^2 + y^2 \le 1 \}$ 和 $B = \{ (x,y) \mid (x-2)^2 + y^2 \le 1 \}$。它们的并集 $X = A \cup B$ 是两个分离的圆盘。显然 $A$ 和 $B$ 是[闭集](@entry_id:136446)，并且它们的交集 $A \cap B = \varnothing$ 是空集。

现在我们考察序列在 $n=0$ 时的部分：
$$ \tilde{H}_0(A \cap B) \xrightarrow{\alpha} \tilde{H}_0(A) \oplus \tilde{H}_0(B) \xrightarrow{\beta} \tilde{H}_0(X) \xrightarrow{\gamma} 0 $$
首先，[空集](@entry_id:261946)的简约同调群为零，所以 $\tilde{H}_0(A \cap B) = 0$。其次，$A$ 和 $B$ 都是[闭圆盘](@entry_id:148403)，是可缩的，因此也是道路连通的，所以 $\tilde{H}_0(A) = 0$ 和 $\tilde{H}_0(B) = 0$。于是，同态 $\beta$ 的定义域是 $0 \oplus 0 = 0$，这意味着它的像 $\text{Im}(\beta)$ 必然是[平凡群](@entry_id:151996) $0$。

然而，空间 $X$ 由两个不相交的[道路连通分支](@entry_id:155468)构成。根据简约同调的定义，如果一个空间有 $k$ 个[道路连通分支](@entry_id:155468)，它的 0 阶简约同调群是 $\mathbb{Z}^{k-1}$。在这里，$k=2$，所以 $\tilde{H}_0(X) \cong \mathbb{Z}$。

如果 Mayer-Vietoris 序列是正合的，那么在 $\tilde{H}_0(X)$ 处的“同调”（即 $\text{Ker}(\gamma) / \text{Im}(\beta)$）必须为零。但在我们的例子中，$\text{Ker}(\gamma) = \tilde{H}_0(X) \cong \mathbb{Z}$，而 $\text{Im}(\beta) = 0$。因此，$\text{Ker}(\gamma) / \text{Im}(\beta) \cong \mathbb{Z} \neq 0$。这表明序列在 $\tilde{H}_0(X)$ 处不正合。这个例子深刻地揭示了 $A$ 和 $B$ 必须是开集的假设是序列成立的基石。

### 序列的内在机制：[连接同态](@entry_id:160713)

Mayer-Vietoris 序列中最神秘也最关键的部分是**[连接同态](@entry_id:160713) (connecting homomorphism)** $\partial_n: H_n(X) \to H_{n-1}(A \cap B)$。它的存在保证了序列的“正合性”，并揭示了空间的同调是如何通过局部粘合构造起来的。

让我们通过几何直观来理解 $\partial_n$ 的定义。
1.  从 $H_n(X)$ 中取一个代表元，它是一个 $n$-闭链 $z \in C_n(X)$（即 $\partial z = 0$）。
2.  由于 $\{A, B\}$ 是 $X$ 的一个开覆盖，我们可以通过一个称为“[重心](@entry_id:273519)重分”的过程，将构成 $z$ 的[奇异单纯形](@entry_id:265569)细分成足够小的部分，使得每个小单纯形要么完全包含在 $A$ 中，要么完全包含在 $B$ 中。这样，我们可以将链 $z$ 写成 $z = u + v$ 的形式，其中 $u$ 是一个 $A$ 中的 $n$-链（即它的所有单纯形都在 $A$ 中），$v$ 是一个 $B$ 中的 $n$-链。
3.  现在我们来考察 $u$ 的边界 $\partial u$。由于 $z$ 是一个闭链，$\partial z = \partial(u+v) = \partial u + \partial v = 0$，这意味着 $\partial u = -\partial v$。
4.  $u$ 是 $A$ 中的链，所以它的边界 $\partial u$ 必然位于 $A$ 中。同理，$\partial v$ 位于 $B$ 中。由于 $\partial u = -\partial v$，这条 $(n-1)$-链必须同时位于 $A$ 和 $B$ 中，也就是说，它是一条在交集 $A \cap B$ 中的链。
5.  不仅如此，$\partial u$ 还是一个闭链，因为 $\partial(\partial u) = 0$（[边界的边界为零](@entry_id:269907)）。因此，$\partial u$ 代表了 $H_{n-1}(A \cap B)$ 中的一个同调类。
6.  我们就定义[连接同态](@entry_id:160713)为 $\partial_n([z]) = [\partial u]$。可以证明这个定义不依赖于 $z$ 的代表元选取以及 $z$ 分解为 $u+v$ 的方式。

#### 基础示例：计算 $H_1(S^1)$

这个抽象的定义最好通过一个具体的例子来理解。让我们用 Mayer-Vietoris 序列来计算圆周 $S^1$ 的一阶同调群，并在此过程中追踪[连接同态](@entry_id:160713)的作用 [@problem_id:1687803]。

我们将 $S^1$ 视为复平面上的[单位圆](@entry_id:267290)。取两个开集 $A = S^1 \setminus \{i\}$ 和 $B = S^1 \setminus \{-i\}$。$A$ 和 $B$ 都是开弧，它们可以[形变收缩](@entry_id:148036)到一个点，因此是可缩的。它们的交集 $A \cap B = S^1 \setminus \{i, -i\}$ 由两段不相交的开弧构成。

由于 $A$ 和 $B$ 是可缩的，它们的所有简约同调群都是零：$\tilde{H}_n(A) = \tilde{H}_n(B) = 0$ for all $n$。
交集 $A \cap B$ 有两个[道路连通分支](@entry_id:155468)，所以 $\tilde{H}_0(A \cap B) \cong \mathbb{Z}$。它的所有更高阶的简约同调群为零。

现在考察简约 Mayer-Vietoris 序列的相关部分：
$$
\cdots \to \tilde{H}_1(A) \oplus \tilde{H}_1(B) \to \tilde{H}_1(S^1) \xrightarrow{\partial_1} \tilde{H}_0(A \cap B) \to \tilde{H}_0(A) \oplus \tilde{H}_0(B) \to \cdots
$$
将已知的同调群代入，得到：
$$
\cdots \to 0 \oplus 0 \to \tilde{H}_1(S^1) \xrightarrow{\partial_1} \mathbb{Z} \to 0 \oplus 0 \to \cdots
$$
根据[正合序列](@entry_id:151503)的性质，这意味着 $\partial_1$ 是一个同构。也就是说，$\tilde{H}_1(S^1) \cong \mathbb{Z}$。

现在，让我们追踪 $H_1(S^1)$ 的生成元在 $\partial_1$ 下的像是什么。取 $H_1(S^1)$ 的标准生成元，即逆时针绕圆心一周的回路，记为 $[z]$。我们可以将这个回路 $z$ 分解为两段：一段是下半圆周的路径 $u$，从点 $1$ 到 $-1$；另一段是上半圆周的路径 $v$，从 $-1$ 回到 $1$。路径 $u$ 完全在 $B$ 中（因为它避开了 $i$），路径 $v$ 完全在 $A$ 中（因为它避开了 $-i$）。这样我们得到了 $z = v+u$，其中 $v$ 是 $A$ 中的 1-链，$u$ 是 $B$ 中的 1-链。

根据[连接同态](@entry_id:160713)的定义，$\partial_1([z]) = [\partial v]$。链 $v$ 的边界是它的两个端点，$\partial v = (1) - (-1)$。这个 0-链是 $H_0(A \cap B)$ 中的一个元素。在简约同调群 $\tilde{H}_0(A \cap B)$ 中，它代表了将一个连通分支中的点（这里是1）与另一个连通分支中的点（这里是-1）相减得到的类。这正是 $\tilde{H}_0(A \cap B) \cong \mathbb{Z}$ 的一个生成元。

因此，我们不仅计算出 $H_1(S^1) \cong \mathbb{Z}$，还通过[连接同态](@entry_id:160713)将 $S^1$ 上的一维“洞”的几何概念（逆时针回路）与 $A \cap B$ 的零维“分离”状态（两个[连通分支](@entry_id:141881)）精确地联系了起来。

### 核心计算策略

Mayer-Vietoris 序列之所以强大，在于它提供了一系列解决问题的标准策略。

#### 悬挂同构 (Suspension Isomorphism)

$S^1$ 的计算是更一般原理的一个特例。当空间 $X$可以分解为两个**可缩**的开集 $A$ 和 $B$ 的并时，Mayer-Vietoris 序列会变得极其简单 [@problem_id:1687848]。因为 $A$ 和 $B$ 可缩，所以对于所有 $n \ge 1$，$H_n(A) = H_n(B) = 0$；并且对于 $n=0$，$\tilde{H}_0(A) = \tilde{H}_0(B) = 0$。

将这些零代入简约 Mayer-Vietoris 序列：
$$
\cdots \to \tilde{H}_n(A) \oplus \tilde{H}_n(B) \to \tilde{H}_n(X) \xrightarrow{\partial_n} \tilde{H}_{n-1}(A \cap B) \to \tilde{H}_{n-1}(A) \oplus \tilde{H}_{n-1}(B) \to \cdots
$$
对于任意 $n \ge 1$，序列的相关片段变为：
$$
\cdots \to 0 \to \tilde{H}_n(X) \xrightarrow{\partial_n} \tilde{H}_{n-1}(A \cap B) \to 0 \to \cdots
$$
根据正合性，这意味着 $\partial_n$ 是一个同构。我们得到了一个惊人的结果：
$$
\tilde{H}_n(X) \cong \tilde{H}_{n-1}(A \cap B) \quad \text{for all } n \ge 1
$$
这个同构通常被称为**悬挂同构**，因为它与拓扑学中的“悬挂”操作密切相关。它允许我们将计算 $X$ 的同调群的问题[降维](@entry_id:142982)成计算其交集 $A \cap B$ 的同调群。例如，如果 $X = A \cup B$，$A, B$ 是可缩开集，且它们的交集 $A \cap B$ [同伦](@entry_id:139266)于 3-球面 $S^3$，那么我们可以立即推断出 $X$ 的简约同调群。我们知道 $\tilde{H}_k(S^3)$ 在 $k=3$ 时为 $\mathbb{Z}$，否则为 0。因此，
$$
\tilde{H}_4(X) \cong \tilde{H}_3(A \cap B) \cong \tilde{H}_3(S^3) \cong \mathbb{Z}
$$
而对于所有 $n \neq 4$，$\tilde{H}_n(X) = 0$。通过这个简单的分解，一个看似复杂的空间 $X$ 的同调群被完全确定了。

#### [楔和](@entry_id:270607)的同调 (Homology of Wedge Sums)

另一个基本应用是计算[楔和](@entry_id:270607) $A \vee B$ 的同调群。[楔和](@entry_id:270607)是通过在 $A$ 和 $B$ 的基点处将它们粘合在一起得到的空间。只要基点是“良性的”（即它们有可缩的邻域），我们就可以证明一个非常简洁的公式 [@problem_id:1687807]：
$$
\tilde{H}_n(A \vee B) \cong \tilde{H}_n(A) \oplus \tilde{H}_n(B) \quad \text{for all } n \ge 0
$$
这个结果可以通过巧妙地应用 Mayer-Vietoris 序列来证明。设 $X = A \vee B$。我们可以构造两个开集 $U$ 和 $V$，其中 $U$ 是 $A$ 加上 $B$ 基点附近的一个小邻域，而 $V$ 是 $B$ 加上 $A$ 基点附近的一个小邻域。这样，$U$ 可以[形变收缩](@entry_id:148036)到 $A$，$V$ 可以[形变收缩](@entry_id:148036)到 $B$，因此它们的同调群分别与 $A$ 和 $B$ 的同调[群同构](@entry_id:147371)。它们的交集 $U \cap V$ 是两个可缩邻域的[楔和](@entry_id:270607)，它本身是可缩的。因此 $U \cap V$ 的所有简约同调群都为零。

将这些信息代入 Mayer-Vietoris 序列：
$$
\cdots \to \tilde{H}_n(U \cap V) \to \tilde{H}_n(U) \oplus \tilde{H}_n(V) \to \tilde{H}_n(X) \to \tilde{H}_{n-1}(U \cap V) \to \cdots
$$
由于 $\tilde{H}_k(U \cap V) = 0$ for all $k$，序列变成了：
$$
\cdots \to 0 \to \tilde{H}_n(A) \oplus \tilde{H}_n(B) \to \tilde{H}_n(A \vee B) \to 0 \to \cdots
$$
正合性再次表明中间的映射是一个同构，从而证明了[楔和](@entry_id:270607)的同调公式。这个公式是构建和理解更复杂空间同调群的基础。例如，由 $k$ 个圆周构成的[楔和](@entry_id:270607)（一个有 $k$ 个花瓣的“花束”），其一阶同调群就是 $\mathbb{Z}^k$。

### 对复杂空间的应用

掌握了基本策略后，我们可以挑战更复杂的空间。

#### 一个[经典计算](@entry_id:136968)：[克莱因瓶](@entry_id:149661)的同调

[克莱因瓶](@entry_id:149661) $K$ 是一个著名的非[可定向曲面](@entry_id:271413)。它可以通过粘合两个莫比乌斯带的边界来构造。这个构造天然地给出了一个开覆盖 $K = A \cup B$，其中 $A$ 和 $B$ 都同伦于莫比乌斯带，而它们的交集 $A \cap B$ 同伦于一个圆环，也就是 $S^1$ [@problem_id:1687820]。

我们知道以下同调群信息（使用整数系数的简约同调）：
- [莫比乌斯带](@entry_id:152389) $M$：$\tilde{H}_1(M) \cong \mathbb{Z}$，其他阶为 0。
- 圆 $S^1$：$\tilde{H}_1(S^1) \cong \mathbb{Z}$，其他阶为 0。

所以，$\tilde{H}_1(A) \cong \mathbb{Z}$，$\tilde{H}_1(B) \cong \mathbb{Z}$，$\tilde{H}_1(A \cap B) \cong \mathbb{Z}$。
让我们来看 Mayer-Vietoris 序列的关键部分：
$$
\tilde{H}_1(A \cap B) \xrightarrow{\Phi_1} \tilde{H}_1(A) \oplus \tilde{H}_1(B) \xrightarrow{\Psi_1} \tilde{H}_1(K) \to \tilde{H}_0(A \cap B) = 0
$$
从序列末端可知，$\Psi_1$ 是满射。根据[正合序列](@entry_id:151503)的基本定理，我们有：
$$
\tilde{H}_1(K) \cong (\tilde{H}_1(A) \oplus \tilde{H}_1(B)) / \text{Im}(\Phi_1)
$$
为了完成计算，我们必须理解映射 $\Phi_1=( (i_A)_*, -(i_B)_* )$。$A \cap B$ 的核心圆是莫比乌斯带 $A$ 的边界圆。当我们将这个边界圆视为 $A$ 中的一个回路时，它会环绕莫比乌斯带的核心线两次。因此，包含映射 $i_A: A \cap B \to A$ 诱导的同态 $(i_A)_*: \tilde{H}_1(A \cap B) \to \tilde{H}_1(A)$ 是一个“乘以 2”的映射。也就是说，如果 $x$ 是 $\tilde{H}_1(A \cap B) \cong \mathbb{Z}$ 的生成元，$a$ 是 $\tilde{H}_1(A) \cong \mathbb{Z}$ 的生成元，则 $(i_A)_*(x) = 2a$。同理，$(i_B)_*(x) = 2b$，其中 $b$ 是 $\tilde{H}_1(B)$ 的生成元。

因此，$\Phi_1(x) = (2a, -2b)$。在同构 $\tilde{H}_1(A) \oplus \tilde{H}_1(B) \cong \mathbb{Z} \oplus \mathbb{Z}$下，$\text{Im}(\Phi_1)$ 是由向量 $(2, -2)$ 生成的[子群](@entry_id:146164)。
我们得到：
$$
\tilde{H}_1(K) \cong (\mathbb{Z} \oplus \mathbb{Z}) / \langle(2, -2)\rangle
$$
通过基变换，令 $u = (1, -1)$，$v = (0, 1)$，则 $\mathbb{Z} \oplus \mathbb{Z}$ 由 $u$ 和 $v$ 生成。在新的基下，$\langle(2,-2)\rangle = \langle 2u \rangle = 2\mathbb{Z} \oplus 0$。因此，商群是：
$$
(\mathbb{Z}u \oplus \mathbb{Z}v) / (2\mathbb{Z}u) \cong (\mathbb{Z}/2\mathbb{Z}) \oplus \mathbb{Z}
$$
最终，我们计算出[克莱因瓶](@entry_id:149661)的一阶同调群 $H_1(K) \cong \mathbb{Z} \oplus \mathbb{Z}_2$。这揭示了[克莱因瓶同调](@entry_id:268370)中的一个“扭曲”部分（由 $\mathbb{Z}_2$ 表示），这是非[可定向性](@entry_id:149777)的代数体现。

#### 计算序列中的映射

在应用 Mayer-Vietoris 序列时，一个实际的挑战是确定序列中的映射，特别是 $\Phi_n$。这通常需要仔细的几何分析。例如，考虑一个8字形空间 $X = C_a \vee C_b$，它由两个圆 $C_a$ 和 $C_b$ 在一点 $v_0$ 处[楔和](@entry_id:270607)而成 [@problem_id:1687847]。
我们可以选择一个开覆盖 $X=A \cup B$，其中 $A$ 是 $C_a$ 的一个“加粗”的[开邻域](@entry_id:268496)（[同伦](@entry_id:139266)于 $C_a$），而 $B = X \setminus \{p_a\}$，其中 $p_a$ 是 $C_a$ 上不同于 $v_0$ 的一个点。$B$ 可以[形变收缩](@entry_id:148036)到 $C_b$。
在这种情况下，$H_1(A) \cong \mathbb{Z}\langle\alpha\rangle$，$H_1(B) \cong \mathbb{Z}\langle\beta\rangle$，其中 $\alpha, \beta$ 分别是 $C_a, C_b$ 的生成元。
交集 $A \cap B = A \setminus \{p_a\}$ 是一个带有一个穿孔的开[圆环](@entry_id:163678)。它的[第一同调群](@entry_id:145318) $H_1(A \cap B) \cong \mathbb{Z} \oplus \mathbb{Z}$。一个自然的基由两条回路给出：$g_1$ 是平行于 $A$ 核心的回路，$g_2$ 是环绕 puncture $p_a$ 的一个小回路。

现在我们来计算 $\Phi_1 = ((i_A)_*, -(i_B)_*)$。
- 映射 $(i_A)_*: H_1(A \cap B) \to H_1(A)$：回路 $g_1$ 在 $A$ 中是[同伦](@entry_id:139266)于核心圆的，所以 $(i_A)_*(g_1) = \alpha$。回路 $g_2$ 在 $A$ 中是可缩的（因为它环绕的点 $p_a$ 在 $A$ 中），所以 $(i_A)_*(g_2) = 0$。
- 映射 $(i_B)_*: H_1(A \cap B) \to H_1(B)$：回路 $g_1$ 和 $g_2$ 都位于 $X$ 中 $C_a$ 的邻域内，它们在 $B$ 中可以被收缩到基点 $v_0$（因为 $B$ [形变收缩](@entry_id:148036)到 $C_b$）。因此，$(i_B)_*(g_1) = 0$ 且 $(i_B)_*(g_2) = 0$。

综上所述，$\Phi_1(g_1) = (\alpha, 0)$，$\Phi_1(g_2) = (0, 0)$。相对于基 $\{g_1, g_2\}$ 和 $\{(\alpha,0), (0,\beta)\}$，$\Phi_1$ 的矩阵表示为：
$$
\begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix}
$$
确定了这张映射，我们就可以继续使用序列来计算 $X$ 的同调群或其他相关信息。

### 序列的代数威力

Mayer-Vietoris 序列不仅是一个计算工具，它的正合性本身就蕴含了深刻的代数约束。

#### 从正合性推断性质

[正合序列](@entry_id:151503)的[代数结构](@entry_id:137052)允许我们在只知道部分信息的情况下推断出其他信息。假设对于某个开覆盖 $X=A \cup B$ 和某个 $n \ge 1$，我们知道 $H_n(X) = 0$ [@problem_id:1687816]。考察序列的两个片段：
1.  $\cdots \to H_n(A \cap B) \xrightarrow{\Phi_n} H_n(A) \oplus H_n(B) \xrightarrow{\Psi_n} H_n(X) = 0$
    由于 $\text{Im}(\Phi_n) = \text{Ker}(\Psi_n)$，而 $\Psi_n$ 的值域是 $0$，所以 $\text{Ker}(\Psi_n)$ 是整个定义域 $H_n(A) \oplus H_n(B)$。因此，$\text{Im}(\Phi_n) = H_n(A) \oplus H_n(B)$，这意味着 $\Phi_n$ 是**满射**。

2.  $0 = H_n(X) \xrightarrow{\partial_n} H_{n-1}(A \cap B) \xrightarrow{\Phi_{n-1}} H_{n-1}(A) \oplus H_{n-1}(B) \to \cdots$
    由于 $\text{Im}(\partial_n) = \text{Ker}(\Phi_{n-1})$，而 $\partial_n$ 的定义域是 $0$，所以 $\text{Im}(\partial_n) = 0$。因此，$\text{Ker}(\Phi_{n-1}) = 0$，这意味着 $\Phi_{n-1}$ 是**[单射](@entry_id:183792)**。

仅仅利用 $H_n(X)=0$ 这个条件，我们就能推断出相邻映射的[单射性](@entry_id:147722)或满射性。这展示了长正合序列如何像多米诺骨牌一样传递代数信息。

#### 反向推理：从整体到局部

在某些情况下，我们可能知道整体空间和[子空间](@entry_id:150286)的同调，但对它们交集的[拓扑性质](@entry_id:141605)感兴趣。Mayer-Vietoris 序列同样能胜任这种反向推理。

设 $X$ 是一个道路连通的空间，由两个道路连通的开集 $A$ 和 $B$ 覆盖。假设我们知道 $\tilde{H}_1(A) \cong \mathbb{Z}$，$\tilde{H}_1(B) \cong \mathbb{Z}$，以及 $\tilde{H}_1(X) \cong \mathbb{Z}^4$。我们还知道包含映射 $j_A: A \to X$ 和 $j_B: B \to X$ 在一阶同调上诱导的映射。我们想确定交集 $A \cap B$ 有多少个[道路连通分支](@entry_id:155468) [@problem_id:1687855]。

[道路连通分支](@entry_id:155468)的数量 $c$ 与 0 阶简约同调群的关系是 $\tilde{H}_0(A \cap B) \cong \mathbb{Z}^{c-1}$。让我们考察简约 Mayer-Vietoris 序列的尾部：
$$
\tilde{H}_1(A) \oplus \tilde{H}_1(B) \xrightarrow{\Psi_1} \tilde{H}_1(X) \xrightarrow{\partial_1} \tilde{H}_0(A \cap B) \to \tilde{H}_0(A) \oplus \tilde{H}_0(B) = 0
$$
由于 $A, B$ 道路连通，$\tilde{H}_0(A) = \tilde{H}_0(B) = 0$。序列的末端告诉我们 $\partial_1$ 是满射。根据正合性，我们有同构：
$$
\tilde{H}_0(A \cap B) \cong \tilde{H}_1(X) / \text{Im}(\Psi_1)
$$
映射 $\Psi_1$ 将 $(u,v)$ 映为 $(j_A)_*(u) + (j_B)_*(v)$。假设 $a$ 是 $\tilde{H}_1(A)$ 的生成元，$b$ 是 $\tilde{H}_1(B)$ 的生成元。给定 $(j_A)_*(a) = (2, 1, 0, 0)$ 和 $(j_B)_*(b) = (1, 1, 0, 0)$（在 $\mathbb{Z}^4$ 的某个基下），那么 $\text{Im}(\Psi_1)$ 就是由这两个向量在 $\mathbb{Z}^4$ 中生成的子格 $L$。我们需要计算[商群](@entry_id:145113) $\mathbb{Z}^4 / L$。

$L$ 由矩阵 $M = \begin{pmatrix} 2  1 \\ 1  1 \\ 0  0 \\ 0  0 \end{pmatrix}$ 的列[向量生成](@entry_id:152883)。这是一个秩为 2 的格。通过整数行变换（或者计算 Smith 标准型），我们可以发现 $\mathbb{Z}^4 / L \cong \mathbb{Z}^2$。
因此，$\tilde{H}_0(A \cap B) \cong \mathbb{Z}^2$。这意味着 $c-1 = 2$，所以交集 $A \cap B$ 有 $c=3$ 个[道路连通分支](@entry_id:155468)。这个例子完美地展示了 Mayer-Vietoris 序列作为一个强大的代数工具，如何从同调信息中提取出深刻的[拓扑性质](@entry_id:141605)。

### 相对 Mayer-Vietoris 序列

Mayer-Vietoris 序列的思想可以推广到[相对同调](@entry_id:159348)中。对于开覆盖 $X = A \cup B$，存在一个连接[相对同调群](@entry_id:159711)的长正合序列 [@problem_id:1687786]：
$$
\cdots \to H_n(B, A \cap B) \to H_n(X, A) \to H_n(X, A \cup B) \to H_{n-1}(B, A \cap B) \to \cdots
$$
这个序列可以通过对三元组 $(X, A \cup B, A)$ 应用长正合序列，并结合[切除定理](@entry_id:159397) $H_n(A \cup B, A) \cong H_n(B, A \cap B)$ 来得到。注意到 $H_n(X, A \cup B) = H_n(X, X) = 0$，序列可以进一步简化。这个相对版本在处理某些几何问题时，比标准版本更为直接和有效。

总而言之，Mayer-Vietoris 序列是同调论中的瑞士军刀。它不仅是[计算同调](@entry_id:161051)群的核心工具，其深刻的[代数结构](@entry_id:137052)也使其成为理论推导和反向推断[拓扑性质](@entry_id:141605)的强大引擎。熟练掌握其原理和应用，是深入学习[代数拓扑学](@entry_id:138192)的关键一步。