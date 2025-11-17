## 引言
在[代数拓扑学](@entry_id:138192)中，同调论是一种强大的工具，它通过将拓扑空间与一系列阿贝尔群（即同调群）相关联，来研究空间的几何形状。然而，标准的同调论存在一个理论上的“不雅之处”：即便是最简单的[可缩空间](@entry_id:153541)，比如一个点，其同调群也并非完全平凡，它的零维同调群是 $\mathbb{Z}$。这与我们期望“拓扑上平凡”的空间在代数上也应“完全平凡”的直觉相悖。

为了解决这一问题，数学家们引入了**既约同调群（Reduced Homology Groups）**。这是一种对标准同调论的精巧修正，旨在使[可缩空间](@entry_id:153541)的同调性质更加自然。本文将系统地介绍既约同调的理论与应用，旨在帮助读者理解其构造动机、核心性质以及在解决拓扑问题中的威力。

在“原理与机制”一章中，我们将从[增广链复形](@entry_id:274443)出发，严格定义既约同调群，并阐明它与标准同调群之间精确的代数关系。接着，在“应用与跨学科联系”一章中，我们将展示既约同调如何作为探测空间连通性与“孔洞”的探针，并作为[Mayer-Vietoris序列](@entry_id:161286)和悬置同构等强大计算工具的核心组成部分。最后，通过“动手实践”中的具体问题，你将有机会亲自运用这些理论来计算和分析[拓扑空间](@entry_id:155056)的性质，从而巩固所学知识。

## 原理与机制

在标准同调论中，我们发现一个空间的第零同调群 $H_0(X)$ 具有特殊的地位，它描述了空间的[路径连通分支](@entry_id:275432)。具体来说，如果 $X$ 有 $k$ 个[路径连通分支](@entry_id:275432)，则 $H_0(X) \cong \mathbb{Z}^k$。这导致了一个略显“不雅”的后果：即使是最简单的空间，如一个点 $\{p\}$，其同调群也并非完全平凡。我们有 $H_0(\{p\}) \cong \mathbb{Z}$，而对所有 $n > 0$，$H_n(\{p\}) = 0$。一个在拓扑上可缩（即可以[连续收缩](@entry_id:154115)到一个点）的空间，我们直观地认为它应该是“平凡的”。如果有一种同调论能将这种拓扑平凡性转化为代数上的完全平凡性（即所有同调群均为零群），那将是十分便利的。这正是**既约同调 (reduced homology)** 的主要动机。

### [增广链复形](@entry_id:274443)与既约同调的定义

为了实现这一目标，我们对标准的奇异[链复形](@entry_id:150246)进行一个小小的修改。回忆一下，标准的奇异[链复形](@entry_id:150246)是一个阿贝尔群和同态的序列：
$$ \dots \xrightarrow{\partial_{n+1}} C_n(X) \xrightarrow{\partial_n} C_{n-1}(X) \xrightarrow{\partial_{n-1}} \dots \xrightarrow{\partial_1} C_0(X) \to 0 $$
其中 $C_n(X)$ 是 $X$ 上的 $n$-链构成的自由阿贝尔群，$\partial_n$ 是[边界算子](@entry_id:160216)。

为了定义既约同调，我们在这个[链复形](@entry_id:150246)的末端增加一步。我们引入一个称为**[增广映射](@entry_id:272732) (augmentation map)** 的同态 $\epsilon: C_0(X) \to \mathbb{Z}$。$C_0(X)$ 是由 $X$ 中的点（即 0-单纯形）作为基底生成的自由阿贝尔群。对于任意一个 0-链 $c = \sum_i k_i \sigma_i$，其中 $\sigma_i$ 是从 0-单纯形到 $X$ 中某个点的映射，$\epsilon$ 的定义为系数之和：
$$ \epsilon(c) = \epsilon\left(\sum_i k_i \sigma_i\right) = \sum_i k_i $$
直观上，[增广映射](@entry_id:272732)“忘掉”了 0-链中每个点的位置，只计算了它们的“[代数数](@entry_id:150888)量”。

我们可以验证 $\epsilon \circ \partial_1 = 0$。对于任意 1-单纯形 $\sigma: \Delta^1 \to X$，其边界 $\partial_1(\sigma)$ 是 $\sigma(v_1) - \sigma(v_0)$，其中 $v_0, v_1$ 是 $\Delta^1$ 的顶点。应用 $\epsilon$ 得到 $\epsilon(\partial_1(\sigma)) = \epsilon(\sigma(v_1) - \sigma(v_0)) = 1 - 1 = 0$。由于 $\partial_1$ 的任何一个生成元都被 $\epsilon$ 映为 0，所以对于任意 1-链 $c \in C_1(X)$，都有 $\epsilon(\partial_1(c)) = 0$。

这一性质意味着 $\text{im}(\partial_1) \subseteq \ker(\epsilon)$，这使得我们可以构造一个**[增广链复形](@entry_id:274443) (augmented chain complex)**：
$$ \dots \xrightarrow{\partial_2} C_1(X) \xrightarrow{\partial_1} C_0(X) \xrightarrow{\epsilon} \mathbb{Z} \to 0 $$
**既约同调群 (reduced homology groups)** $\tilde{H}_n(X)$ 就被定义为这个[增广链复形](@entry_id:274443)的同调群。具体来说：
$$ \tilde{H}_n(X) = \frac{\ker(\partial_n)}{\text{im}(\partial_{n+1})} \quad \text{for } n \ge 1 $$
$$ \tilde{H}_0(X) = \frac{\ker(\epsilon)}{\text{im}(\partial_1)} $$

### 与标准同调的关系

从定义中我们可以立即看出既约同调与标准同调之间的密切联系。

对于 $n \ge 1$，既约同调群 $\tilde{H}_n(X)$ 的定义 $\ker(\partial_n) / \text{im}(\partial_{n+1})$ 与标准同调群 $H_n(X)$ 的定义完全相同。因此，我们可以得出第一个重要结论：

**对于任何[拓扑空间](@entry_id:155056) $X$ 和所有 $n \ge 1$，我们有 $H_n(X) \cong \tilde{H}_n(X)$**。[@problem_id:1668774]

这意味着既约同调的所有“新”特性都集中在第零个同调群 $\tilde{H}_0(X)$ 上。让我们来深入探讨这一点。

标准第零同调群是 $H_0(X) = C_0(X) / \text{im}(\partial_1)$，而既约版本是 $\tilde{H}_0(X) = \ker(\epsilon) / \text{im}(\partial_1)$。两者之间的唯一区别在于分子：一个是整个 $C_0(X)$，另一个是 $\ker(\epsilon)$。

为了理解 $\ker(\epsilon)$，我们可以考虑一个由三个离散点 $\{p_1, p_2, p_3\}$ 构成的空间 $X$ [@problem_id:1668777]。$C_0(X)$ 是由 $[p_1], [p_2], [p_3]$ 生成的秩为 3 的自由阿贝尔群。一个任意的 0-链是 $c = a_1[p_1] + a_2[p_2] + a_3[p_3]$。[增广映射](@entry_id:272732)为 $\epsilon(c) = a_1 + a_2 + a_3$。因此，$\ker(\epsilon)$ 由所有系数和为零的 0-链组成。容易验证，$\ker(\epsilon)$ 是一个秩为 2 的自由[阿贝尔群](@entry_id:150284)，它可以由 $\{[p_1] - [p_2], [p_1] - [p_3]\}$ 这样的元素生成。

对于一个非空空间 $X$，[增广映射](@entry_id:272732) $\epsilon: C_0(X) \to \mathbb{Z}$ 是一个满射（取任意一点 $p \in X$，则 $\epsilon([p]) = 1$）。我们有短[正合序列](@entry_id:151503)：
$$ 0 \to \ker(\epsilon) \to C_0(X) \xrightarrow{\epsilon} \mathbb{Z} \to 0 $$
由于 $\mathbb{Z}$ 是自由群，这个序列是可分裂的。这意味着 $C_0(X) \cong \ker(\epsilon) \oplus \mathbb{Z}$。将这个关系除以 $\text{im}(\partial_1)$，我们得到：
$$ H_0(X) = \frac{C_0(X)}{\text{im}(\partial_1)} \cong \frac{\ker(\epsilon) \oplus \mathbb{Z}}{\text{im}(\partial_1)} \cong \frac{\ker(\epsilon)}{\text{im}(\partial_1)} \oplus \mathbb{Z} = \tilde{H}_0(X) \oplus \mathbb{Z} $$
这个关系 $H_0(X) \cong \tilde{H}_0(X) \oplus \mathbb{Z}$ 对所有非空空间 $X$ 都成立。[@problem_id:1668774]

现在我们可以赋予 $\tilde{H}_0(X)$ 一个清晰的几何解释。我们知道 $H_0(X)$ 是一个自由[阿贝尔群](@entry_id:150284)，其秩等于 $X$ 的[路径连通分支](@entry_id:275432)的数量，记为 $k$。因此，$\text{rank}(H_0(X)) = k$。根据上述同构关系，我们立即得到 $\text{rank}(\tilde{H}_0(X)) = k-1$ [@problem_id:1668756]。特别地，对于一个非空[路径连通空间](@entry_id:152443)（$k=1$），我们有 $\tilde{H}_0(X) \cong \{0\}$。

对于[空集](@entry_id:261946) $\emptyset$，其所有链群 $C_n(\emptyset)$ 都是[平凡群](@entry_id:151996) $\{0\}$。[增广映射](@entry_id:272732) $\epsilon: C_0(\emptyset) \to \mathbb{Z}$ 是从 $\{0\}$ 到 $\mathbb{Z}$ 的唯一同态，即零映射。因此，[增广链复形](@entry_id:274443)是 $\dots \to \{0\} \to \{0\} \xrightarrow{0} \mathbb{Z} \to 0$。计算其同调，我们发现 $\tilde{H}_n(\emptyset) = 0$ 对所有 $n \ge 0$ 成立 [@problem_id:1633160]。注意，对于空集，$H_0(\emptyset) = 0$，因此 $H_0(\emptyset) \cong \tilde{H}_0(\emptyset) \oplus \mathbb{Z}$ 不再成立，这强调了该同构关系中空间非空的假设是必要的。

### [可缩空间](@entry_id:153541)的同调特征

现在我们来到了既约同调的核心优势：它能完美地刻画[可缩空间](@entry_id:153541)的同调性质。

让我们从最简单的[可缩空间](@entry_id:153541)——单点空间 $X=\{p\}$ 开始。对于任意 $n \ge 0$，只存在一个奇异 $n$-单纯形 $\sigma_n: \Delta^n \to \{p\}$，即常映射。因此，$C_n(X) \cong \mathbb{Z}$，由 $\sigma_n$ 生成。[边界算子](@entry_id:160216) $\partial_n(\sigma_n) = \sum_{i=0}^n (-1)^i \sigma_{n-1}$。当 $n$ 为偶数时，系数和为 1；当 $n$ 为奇数时，系数和为 0。因此，$\partial_n$ 在 $n$ 为偶数时是同构，在 $n$ 为奇数时是零映射。[增广映射](@entry_id:272732) $\epsilon: C_0(X) \to \mathbb{Z}$ 将生成元 $\sigma_0$ 映为 1，因此也是同构。
[增广链复形](@entry_id:274443)具体表现为：
$$ \dots \xrightarrow{0} \mathbb{Z} \xrightarrow{\cong} \mathbb{Z} \xrightarrow{0} \mathbb{Z} \xrightarrow{\cong} \mathbb{Z} \to 0 $$
这是一个[正合序列](@entry_id:151503)。[正合序列](@entry_id:151503)的定义就是每一步的核等于前一步的像，这意味着它的所有同调群都是平凡的。因此，我们得出结论：**$\tilde{H}_n(\{p\}) = 0$ 对所有 $n \ge 0$ 成立** [@problem_id:1654895]。

这个结果可以推广到所有[可缩空间](@entry_id:153541)。一个非空空间 $X$ 是可缩的，意味着它的[恒等映射](@entry_id:634191) $\text{id}_X: X \to X$ 与一个常映射 $c_p: X \to X$（其中 $c_p(x) = p$ 对所有 $x \in X$）是同伦的。同调论的[同伦公理](@entry_id:260899)表明，同伦的映射在同调群上诱导相同的同态。因此，$(\text{id}_X)_* = (c_p)_* : \tilde{H}_n(X) \to \tilde{H}_n(X)$。

$(\text{id}_X)_*$ 是 $\tilde{H}_n(X)$ 上的恒等同态。另一方面，常映射 $c_p$ 可以分解为 $X \to \{p\} \to X$。因此，其诱导的同态 $(c_p)_*$ 可以分解为：
$$ \tilde{H}_n(X) \xrightarrow{} \tilde{H}_n(\{p\}) \xrightarrow{} \tilde{H}_n(X) $$
由于我们已经证明了中间的群 $\tilde{H}_n(\{p\})$ 是零群，任何经过零群的同态必然是零同态 [@problem_id:1668750]。这意味着 $(c_p)_*$ 是零同态。

综上所述，我们证明了在 $\tilde{H}_n(X)$ 上，恒等同态等于零同态。一个群上的恒等映射是零映射，当且仅当这个群本身是只包含零元的平凡群。因此，我们得到了既约同调的标志性定理：

**如果 $X$ 是一个非空[可缩空间](@entry_id:153541)，则 $\tilde{H}_n(X) = 0$ 对所有 $n \ge 0$ 成立。** [@problem_id:1655132]

一个重要的[可缩空间](@entry_id:153541)族是**锥 (cone)**。对于任何非空空间 $X$，其上的锥 $CX$ 总是可缩的。因此，无论 $X$ 本身多么复杂（例如，一个由两个球面不交并构成的空间），其锥的既约同调群总是平凡的：$\tilde{H}_n(CX) = 0$ 对所有 $n \ge 0$ 成立 [@problem_id:1668753]。

### 关键同构与计算工具

既约同调不仅在理论上优雅，也简化了许多代数拓扑中的关键定理和计算。

一个核心应用是它与**[相对同调](@entry_id:159348) (relative homology)** 的联系。考虑一个拓扑对 $(X, A)$，其中 $A$ 是 $X$ 的一个非空[子空间](@entry_id:150286)。既约同调的[长正合序列](@entry_id:153438)为：
$$ \dots \to \tilde{H}_n(A) \to \tilde{H}_n(X) \to H_n(X, A) \to \tilde{H}_{n-1}(A) \to \dots $$
注意：当 $A$ 非空时，既约[相对同调群](@entry_id:159711) $\tilde{H}_n(X, A)$ 与普通[相对同调群](@entry_id:159711) $H_n(X, A)$ 是同构的。

现在，让我们考虑一个非常特殊但重要的情形，即[子空间](@entry_id:150286) $A$ 是 $X$ 中的一个单点 $\{x_0\}$。我们将 $(X, \{x_0\})$ 代入上述长正合序列：
$$ \dots \to \tilde{H}_n(\{x_0\}) \to \tilde{H}_n(X) \to H_n(X, x_0) \to \tilde{H}_{n-1}(\{x_0\}) \to \dots $$
由于我们已经知道单点的所有既约同调群均为零，即 $\tilde{H}_k(\{x_0\}) = 0$ 对所有 $k$ 成立，上述序列变成了许多短[正合序列](@entry_id:151503)的拼接：
$$ \dots \to 0 \to \tilde{H}_n(X) \to H_n(X, x_0) \to 0 \to \dots $$
从这个短[正合序列](@entry_id:151503) $0 \to \tilde{H}_n(X) \to H_n(X, x_0) \to 0$ 可以立即得出，中间的映射是一个同构。这为我们提供了一个极为有用的工具：

**对于任何非空空间 $X$ 和其中的任意一点 $x_0 \in X$，[相对同调群](@entry_id:159711) $H_n(X, x_0)$ 与既约同调群 $\tilde{H}_n(X)$ 同构：**
$$ H_n(X, x_0) \cong \tilde{H}_n(X) \quad \text{for all } n \ge 0 $$
[@problem_id:1680222]
这个同构告诉我们，“相对于一个点的同调”恰好就是既约同调。

此外，既约同调在处理[商空间](@entry_id:274314)时也很有用。对于一个“良序对”(good pair) $(X, A)$，[相对同调](@entry_id:159348)与[商空间](@entry_id:274314)的既约同调之间存在同构 $H_n(X, A) \cong \tilde{H}_n(X/A)$。例如，考虑空间 $X = S^2 \vee S^1$（球面和圆在一点处的[楔和](@entry_id:270607)），以及其[子空间](@entry_id:150286) $A=S^2$。将[子空间](@entry_id:150286) $A$ 压缩到一个点得到的[商空间](@entry_id:274314) $X/A$ 同胚于 $S^1$。因此，我们可以计算：
$$ \tilde{H}_n(S^1) \cong \tilde{H}_n(X/A) \cong H_n(X, A) $$
我们知道 $\tilde{H}_1(S^1) \cong \mathbb{Z}$ 且其他度数的既约同调群为零。因此，$\tilde{H}_1(X/A) \cong \mathbb{Z}$ [@problem_id:1668739]。

最后，另一个使用既约同调表述得更简洁的基本定理是**悬置同构 (Suspension Isomorphism)** 定理，它指出 $\tilde{H}_n(X) \cong \tilde{H}_{n+1}(SX)$，其中 $SX$ 是 $X$ 的悬置。这个定理是代数拓扑中许多计算和理论发展的基石。

总之，既约同调通过对标准同调进行微小的修改，为我们提供了一个强大的理论框架。它不仅使[可缩空间](@entry_id:153541)（如点）的同调性质更加自然，还简化了许多核心定理的表述，并提供了与[相对同调](@entry_id:159348)和[商空间同调](@entry_id:269206)的直接联系，成为代数拓扑中不可或缺的工具。