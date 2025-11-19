## 引言
在现代[抽象代数](@entry_id:145216)的宏伟殿堂中，**[正合序列](@entry_id:151503) (Exact Sequence)** 堪称一种通用而优雅的语言。它不仅统一了模的子模、[商模](@entry_id:155903)、同态、[核与像](@entry_id:151957)等一系列基本概念，还为探索不同[代数结构](@entry_id:137052)之间的深层联系提供了强大的框架。初学者往往会被其抽象的定义所困惑，难以把握其背后蕴含的丰富结构信息以及在解决实际问题中的巨大威力。本文旨在填补这一认知鸿沟，系统地剖析[正合序列](@entry_id:151503)的理论精髓与实践应用。

为实现这一目标，本文将分为三个核心部分。首先，在“**原理与机制**”一章中，我们将从正合性的基本定义出发，逐步构建起整个理论体系。读者将学习到最重要的构件——短[正合序列](@entry_id:151503)，理解其与[模的直和](@entry_id:156308)分解之间的关系（即[分裂引理](@entry_id:150631)），并探索当函子（如Hom和[张量积](@entry_id:140694)）作用于[正合序列](@entry_id:151503)时会发生什么，以及如何通过蛇形引理和长正合序列来“修复”正合性的缺失。

接着，在“**应用与跨学科联系**”一章中，我们将展示这些抽象的理论如何转化为解决具体问题的利器。通过一系列来自[模论](@entry_id:139410)、同调代数、[表示论](@entry_id:137998)、群论和[交换代数](@entry_id:149047)等领域的实例，读者将看到[正合序列](@entry_id:151503)如何作为一种分析工具，用于计算[不变量](@entry_id:148850)、刻画模的性质（如投射性与内射性），并为不同数学分支的核心定理提供统一的视角。

最后，“**动手实践**”部分提供了一系列精心挑选的练习题，旨在帮助读者巩固所学知识，将理论应用于具体的计算与证明，从而真正内化[正合序列](@entry_id:151503)的思想。通过这三个层次的递进学习，读者将能够掌握[正合序列](@entry_id:151503)这一核心工具，为深入探索更高等的代数世界打下坚实的基础。

## 原理与机制

### 正合性的定义

在模理论中，**[正合序列](@entry_id:151503) (exact sequence)** 是一个核心概念，它以一种优雅的方式将模的同态、[核与像](@entry_id:151957)联系在一起。一个由模与[模同态](@entry_id:148144)组成的序列：
$$ \dots \to M_{i-1} \xrightarrow{f_{i-1}} M_i \xrightarrow{f_i} M_{i+1} \to \dots $$
被称为在模 $M_i$ 处**正合 (exact)**，如果前一个同态的**像 (image)** 恰好等于后一个同态的**核 (kernel)**，即 $\text{Im}(f_{i-1}) = \text{Ker}(f_i)$。如果一个序列在其每一个可能的中间位置都正合，那么这个序列就称为一个**[正合序列](@entry_id:151503)**。

理解正合性的一个关键在于，条件 $\text{Im}(f_{i-1}) = \text{Ker}(f_i)$ 蕴含了复合映射 $f_i \circ f_{i-1}$ 是零同态。这是因为对于任何 $x \in M_{i-1}$，它的像 $f_{i-1}(x)$ 位于 $\text{Im}(f_{i-1})$ 中。根据正合性定义，这也意味着 $f_{i-1}(x)$ 位于 $\text{Ker}(f_i)$ 中，因此 $f_i(f_{i-1}(x)) = 0$。所以，$f_i \circ f_{i-1} = 0$ 是序列在 $M_i$ 处正合的必要条件。

然而，这个条件并非充分。$\text{Im}(f_{i-1}) \subseteq \text{Ker}(f_i)$ 总是由 $f_i \circ f_{i-1} = 0$ 保证，但正合性要求的是二者之间严格的相等关系。为了阐明这一点，我们可以考察一个不满足此条件的例子。考虑如下的 $\mathbb{Z}$-模（即阿贝尔群）序列：
$$ \mathbb{Z} \xrightarrow{f} \mathbb{Z} \xrightarrow{g} \mathbb{Z} $$
其中 $f(n) = 2n$，$g$ 是零同态，即对所有 $n \in \mathbb{Z}$ 都有 $g(n) = 0$。复合映射 $g \circ f$ 显然是零映射，因为 $g(f(n)) = g(2n) = 0$。然而，这个序列在中间的 $\mathbb{Z}$ 处并不正合。$f$ 的像是所有偶数构成的集合，即 $\text{Im}(f) = 2\mathbb{Z}$。而 $g$ 的核是其整个定义域，即 $\text{Ker}(g) = \mathbb{Z}$。由于 $2\mathbb{Z}$ 是 $\mathbb{Z}$ 的一个[真子集](@entry_id:152276)，我们有 $\text{Im}(f) \neq \text{Ker}(g)$，因此该序列不正合 [@problem_id:1792265]。

### 基本构造块：短[正合序列](@entry_id:151503)

[正合序列](@entry_id:151503)中最基本也最重要的类型是**短[正合序列](@entry_id:151503) (short exact sequence)**。它由五个模组成，其中首尾两个是零模 $0$。在分析短[正合序列](@entry_id:151503)之前，我们先考察[正合序列](@entry_id:151503)在端点处的含义。

考虑形如 $0 \to M \xrightarrow{f} N$ 的序列。从零模 $0$ 到 $M$ 的唯一同态是零映射，其像为 $\{0\}$。因此，此序列在 $M$ 处正合的条件是 $\text{Ker}(f) = \{0\}$。这正是同态 $f$ 是**[单射](@entry_id:183792) (injective)** 的定义。例如，我们可以考察两个从 $M = \mathbb{Z}_4$ 到 $N = \mathbb{Z}_8$ 的映射。若定义 $f_1([x]_4) = [2x]_8$，要使其成为[正合序列](@entry_id:151503) $0 \to \mathbb{Z}_4 \xrightarrow{f_1} \mathbb{Z}_8$ 的一部分，我们需要 $f_1$ 是单射。$f_1$ 的核由满足 $2x \equiv 0 \pmod 8$ 的 $[x]_4$ 组成，这意味着 $x$ 必须是 $4$ 的倍数。在 $\mathbb{Z}_4$ 中，唯一的解是 $[0]_4$，所以 $\text{Ker}(f_1) = \{[0]_4\}$，$f_1$ 是单射，序列是正合的。相反，如果定义 $f_2([x]_4) = [4x]_8$，则其核由满足 $4x \equiv 0 \pmod 8$ 的 $[x]_4$ 组成，这意味着 $x$ 是 $2$ 的倍数。在 $\mathbb{Z}_4$ 中，解为 $[0]_4$ 和 $[2]_4$，核非平凡，故 $f_2$ 不是[单射](@entry_id:183792)，序列 $0 \to \mathbb{Z}_4 \xrightarrow{f_2} \mathbb{Z}_8$ 不正合 [@problem_id:1792294]。

现在考虑序列的另一端，形如 $M \xrightarrow{g} N \to 0$。从 $N$到零模 $0$ 的唯一[同态的核](@entry_id:145895)是整个 $N$。因此，此序列在 $N$ 处正合的条件是 $\text{Im}(g) = N$。这正是同态 $g$ 是**满射 (surjective)** 的定义 [@problem_id:1792314]。

结合这两种情况，我们便得到了**短[正合序列](@entry_id:151503)**的定义。一个形如
$$ 0 \to A \xrightarrow{f} B \xrightarrow{g} C \to 0 $$
的序列是一个短[正合序列](@entry_id:151503)，当且仅当它同时满足以下三个条件：
1.  序列在 $A$ 处正合，即 $f$ 是[单射](@entry_id:183792)。
2.  序列在 $C$ 处正合，即 $g$ 是满射。
3.  序列在 $B$ 处正合，即 $\text{Im}(f) = \text{Ker}(g)$。

短[正合序列](@entry_id:151503)提供了一种简洁而深刻的方式来表达模之间的关系。$f$是单射意味着 $A$ 同构于 $B$ 的一个[子模](@entry_id:148922) $\text{Im}(f)$。而 $\text{Im}(f) = \text{Ker}(g)$ 和 $g$是满射，根据同态基本定理，意味着 $C$ 同构于[商模](@entry_id:155903) $B / \text{Ker}(g)$，也就是 $B / \text{Im}(f)$。因此，一个短[正合序列](@entry_id:151503)本质上描述了 $B$ 是 $C$ 对 $A$ 的一个“扩张”。

一个典型的短[正合序列](@entry_id:151503)例子是对于任何整数 $n > 1$：
$$ 0 \to n\mathbb{Z} \xrightarrow{i} \mathbb{Z} \xrightarrow{\pi} \mathbb{Z}_n \to 0 $$
这里 $i$ 是自然包含映射（$i(nx) = nx$），$\pi$ 是典范[投影映射](@entry_id:153398)（$\pi(k) = k \pmod n$）。$i$ 显然是[单射](@entry_id:183792)。$\pi$ 根据定义是满射。序列在中间 $\mathbb{Z}$ 处是否正合呢？$i$ 的像是 $n\mathbb{Z}$，而 $\pi$ 的核是所有映射到 $\mathbb{Z}_n$ 中零元的整数集合，这恰好也是 $n\mathbb{Z}$。因此 $\text{Im}(i) = \text{Ker}(\pi)$，该序列确实是一个短[正合序列](@entry_id:151503)。如果我们稍微改变一下这个序列，例如，考虑 $0 \to 2\mathbb{Z} \xrightarrow{i} \mathbb{Z} \xrightarrow{\pi} \mathbb{Z}_3 \to 0$，那么 $\text{Im}(i) = 2\mathbb{Z}$ 但 $\text{Ker}(\pi) = 3\mathbb{Z}$，二者不相等，所以这个序列在中间不正合，不是一个短[正合序列](@entry_id:151503) [@problem_id:1792279]。

### 短[正合序列](@entry_id:151503)的结构：分裂

既然短[正合序列](@entry_id:151503) $0 \to A \to B \to C \to 0$ 意味着 $B$ 是 $C$ 对 $A$ 的扩张，一个自然的问题是：$B$ 的结构在多大程度上由 $A$ 和 $C$ 决定？最简单的情况是 $B$ 同构于 $A$ 和 $C$ 的[直和](@entry_id:156782) $A \oplus C$。当这种情况发生时，我们称该短[正合序列](@entry_id:151503)是**分裂的 (split)**。

一个短[正合序列](@entry_id:151503)是否分裂，可以通过**[分裂引理](@entry_id:150631) (Splitting Lemma)** 来判断。该引理断言，对于一个短[正合序列](@entry_id:151503) $0 \to A \xrightarrow{f} B \xrightarrow{g} C \to 0$，以下三个陈述是等价的：

1.  存在一个同态 $r: B \to A$（称为**收缩 (retraction)**），使得 $r \circ f = \text{id}_A$（$A$上的恒等映射）。
2.  存在一个同态 $s: C \to B$（称为**[截面](@entry_id:154995) (section)**），使得 $g \circ s = \text{id}_C$（$C$上的恒等映射）。
3.  $B$ 同构于直和 $A \oplus C$。

让我们通过一个例子来理解这一点。假设我们有一个短[正合序列](@entry_id:151503) $0 \to A \xrightarrow{f} B \xrightarrow{g} C \to 0$，其中 $A = \mathbb{Z}_2$，$C = \mathbb{Z}_2$，并且存在一个收缩 $r: B \to A$ 满足 $r \circ f = \text{id}_A$。根据[分裂引理](@entry_id:150631)，我们应该能断定 $B$ 的结构。具体地，我们可以证明 $B \cong A \oplus C$。构造一个映射 $\varphi: A \oplus C \to B$。然而，更直接的方法是证明 $B$ 的每个元素可以唯一地分解为一个来自“$A$的部分”和一个来自“$C$的部分”。确实，任何 $b \in B$ 都可以写作 $b = f(r(b)) + (b - f(r(b)))$。第一项 $f(r(b))$ 在 $\text{Im}(f)$ 中。第二项 $b - f(r(b))$ 在 $\text{Ker}(r)$ 中。可以证明 $B$ 是这两个[子模](@entry_id:148922)的[内直和](@entry_id:153328)，$\text{Im}(f)$ 同构于 $A$，$\text{Ker}(r)$ 同构于 $C$。因此，$B \cong A \oplus C$。在 $A = C = \mathbb{Z}_2$ 的情况下，我们必有 $B \cong \mathbb{Z}_2 \oplus \mathbb{Z}_2$ [@problem_id:1792313]。

然而，并非所有短[正合序列](@entry_id:151503)都是分裂的。一个经典的非分裂例子正是我们之前遇到的序列：
$$ 0 \to \mathbb{Z} \xrightarrow{f} \mathbb{Z} \xrightarrow{g} \mathbb{Z}_n \to 0 $$
其中 $f(x) = nx$ 且 $n > 1$。如果这个序列分裂，那么根据[分裂引理](@entry_id:150631)，中间的模 $\mathbb{Z}$ 必须同构于两端[模的直和](@entry_id:156308)，即 $\mathbb{Z} \cong \mathbb{Z} \oplus \mathbb{Z}_n$。这是不可能的。$\mathbb{Z} \oplus \mathbb{Z}_n$ 中包含非零的**[挠元](@entry_id:148301) (torsion element)**，例如 $(0, [1]_n)$ 的阶为 $n$。而 $\mathbb{Z}$ 作为一个阿贝尔群，除了 $0$ 之外没有任何有限阶的元素（即它是[无挠的](@entry_id:161664)）。因为同构会保持[挠元](@entry_id:148301)的存在性，所以 $\mathbb{Z}$ 和 $\mathbb{Z} \oplus \mathbb{Z}_n$ 不可能同构。因此，这个序列不分裂。这也可以通过证明不存在[分裂引理](@entry_id:150631)中的[截面](@entry_id:154995) $s: \mathbb{Z}_n \to \mathbb{Z}$ 或收缩 $r: \mathbb{Z} \to \mathbb{Z}$ 来得出 [@problem_id:1792302]。

### 用[函子](@entry_id:150427)探测正合性

代数中的一个强大技术是使用**[函子](@entry_id:150427) (functor)** 将一个[代数结构](@entry_id:137052)范畴中的对象和态射映射到另一个范畴。当我们对一个[正合序列](@entry_id:151503)应用[函子](@entry_id:150427)时，一个核心问题是：[函子](@entry_id:150427)是否保持正合性？一个将任意短[正合序列](@entry_id:151503)都映为短[正合序列](@entry_id:151503)的函子称为**正合函子 (exact functor)**。然而，许多重要的[函子](@entry_id:150427)并非完全正合，但它们以一种可预测的方式“部分”保持正合性。

#### Hom 函子

考虑协变 Hom [函子](@entry_id:150427) $F(-) = \text{Hom}_R(M, -)$ 和[逆变](@entry_id:192290) Hom 函子 $G(-) = \text{Hom}_R(-, M)$。这两个函子都是**左正合的 (left exact)**。对于协变函子，这意味着若 $0 \to A \to B \to C$ 是一个[正合序列](@entry_id:151503)，则序列 $0 \to \text{Hom}_R(M, A) \to \text{Hom}_R(M, B) \to \text{Hom}_R(M, C)$ 也是正合的。但是，原序列末尾的满射不一定能保持。

我们可以通过将 $F(-) = \text{Hom}_{\mathbb{Z}}(\mathbb{Z}_n, -)$ 应用于非分裂的短[正合序列](@entry_id:151503) $0 \to \mathbb{Z} \xrightarrow{\mu_n} \mathbb{Z} \xrightarrow{\pi} \mathbb{Z}_n \to 0$ (其中 $\mu_n$ 是乘以 $n$) 来观察这一现象。应用[函子](@entry_id:150427)后，我们得到序列：
$$ \text{Hom}_{\mathbb{Z}}(\mathbb{Z}_n, \mathbb{Z}) \xrightarrow{(\mu_n)_*} \text{Hom}_{\mathbb{Z}}(\mathbb{Z}_n, \mathbb{Z}) \xrightarrow{\pi_*} \text{Hom}_{\mathbb{Z}}(\mathbb{Z}_n, \mathbb{Z}_n) $$
首先，任何从 $\mathbb{Z}_n$ 到 $\mathbb{Z}$ 的同态都必须是零同态，因为 $\mathbb{Z}_n$ 中的每个元素都是[挠元](@entry_id:148301)，而 $\mathbb{Z}$ 是[无挠的](@entry_id:161664)。所以 $\text{Hom}_{\mathbb{Z}}(\mathbb{Z}_n, \mathbb{Z}) = 0$。其次，从 $\mathbb{Z}_n$到自身的同态由生成元 $[1]_n$ 的像决定，因此 $\text{Hom}_{\mathbb{Z}}(\mathbb{Z}_n, \mathbb{Z}_n) \cong \mathbb{Z}_n$。于是，得到的序列是 $0 \xrightarrow{(\mu_n)_*} 0 \xrightarrow{\pi_*} \mathbb{Z}_n$。映射 $\pi_*$ 的定义域是零群，所以它的像也必然是零。因此，$\pi_*$ 不是满射，序列在 $\text{Hom}_{\mathbb{Z}}(\mathbb{Z}_n, \mathbb{Z}_n)$ 处不正合。其**上核 (cokernel)**，$\text{coker}(\pi_*) = \text{Hom}_{\mathbb{Z}}(\mathbb{Z}_n, \mathbb Z_n) / \text{Im}(\pi_*) \cong \mathbb{Z}_n / \{0\} \cong \mathbb{Z}_n$，度量了正合性的“失效”程度 [@problem_id:1792298]。

#### [张量积](@entry_id:140694)[函子](@entry_id:150427)

另一个重要的函子是[张量积](@entry_id:140694)[函子](@entry_id:150427) $F(-) = - \otimes_R M$。与 Hom [函子](@entry_id:150427)不同，[张量积](@entry_id:140694)函子是**右正合的 (right exact)**。这意味着如果 $A \to B \to C \to 0$ 是一个[正合序列](@entry_id:151503)，那么 $A \otimes_R M \to B \otimes_R M \to C \otimes_R M \to 0$ 也是一个[正合序列](@entry_id:151503)。然而，它通常不保持左端的[单射](@entry_id:183792)。

让我们将函子 $- \otimes_{\mathbb{Z}} \mathbb{Z}_2$ 应用于短[正合序列](@entry_id:151503) $0 \to \mathbb{Z} \xrightarrow{f} \mathbb{Z} \xrightarrow{g} \mathbb{Z}_2 \to 0$，其中 $f$是乘以 $2$。得到的序列的前半部分是：
$$ \mathbb{Z} \otimes_{\mathbb{Z}} \mathbb{Z}_2 \xrightarrow{\bar{f}} \mathbb{Z} \otimes_{\mathbb{Z}} \mathbb{Z}_2 $$
我们知道对于任何 $\mathbb{Z}$-模 $A$，都有 $\mathbb{Z} \otimes_{\mathbb{Z}} A \cong A$。因此上述序列简化为 $\mathbb{Z}_2 \xrightarrow{\bar{f}} \mathbb{Z}_2$。现在我们来计算 $\bar{f}$ 的作用。对于一个典型元素 $z \otimes \overline{a} \in \mathbb{Z} \otimes_{\mathbb{Z}} \mathbb{Z}_2$，我们有 $\bar{f}(z \otimes \overline{a}) = f(z) \otimes \overline{a} = 2z \otimes \overline{a}$。利用[张量积](@entry_id:140694)的性质，我们可将标量 $2$ 移到另一边，得到 $z \otimes 2\overline{a}$。但在 $\mathbb{Z}_2$ 中，$2\overline{a} = \overline{0}$。所以 $z \otimes 2\overline{a} = z \otimes \overline{0} = 0$。这意味着 $\bar{f}$ 是零映射。因此，$\bar{f}$ 的核是整个定义域 $\mathbb{Z}_2$。由于原序列中 $f$ 是单射，而 $\bar{f}$ 却不是，这表明[张量积](@entry_id:140694)函子不是左正合的 [@problem_id:1792310]。

### [连接同态](@entry_id:160713)与长正合序列

[函子](@entry_id:150427)在保持正合性上的“失败”并非缺陷，而是通向更深刻结构——**[长正合序列](@entry_id:153438) (long exact sequence)** 的门户。这种失效由所谓的**[连接同态](@entry_id:160713) (connecting homomorphism)** 精确地度量。

#### 蛇形引理

[长正合序列](@entry_id:153438)最经典和具体的来源是**蛇形引理 (Snake Lemma)**。它适用于一个行正合的[交换图](@entry_id:747516)：
$$
\begin{array}{ccccccccc}
  A  \xrightarrow{f}  B  \xrightarrow{g}  C  \longrightarrow  0 \\
  \downarrow \alpha   \downarrow \beta   \downarrow \gamma   \\
0  \longrightarrow  A'  \xrightarrow{f'}  B'  \xrightarrow{g'}  C'  
\end{array}
$$
蛇形引理断言，存在一个连接了垂直映射的核与上核的长正合序列：
$$ \ker(\alpha) \to \ker(\beta) \to \ker(\gamma) \xrightarrow{\delta} \text{coker}(\alpha) \to \text{coker}(\beta) \to \text{coker}(\gamma) $$
其中最关键的部分就是**[连接同态](@entry_id:160713)** $\delta$。它的构造过程，即所谓的“[图追踪](@entry_id:263851) (diagram chasing)”，是理解其本质的最好方式。

让我们在一个具体的例子中构造 $\delta$。考虑如下的 $\mathbb{Z}$-模[交换图](@entry_id:747516)，其行是短[正合序列](@entry_id:151503) $0 \to \mathbb{Z} \xrightarrow{\times 2} \mathbb{Z} \to \mathbb{Z}/2\mathbb{Z} \to 0$：
$$
\begin{array}{ccccccccc}
0  \longrightarrow  \mathbb{Z}  \xrightarrow{f}  \mathbb{Z}  \xrightarrow{g}  \mathbb{Z}/2\mathbb{Z}  \longrightarrow  0 \\
  \downarrow \alpha   \downarrow \beta   \downarrow \gamma   \\
0  \longrightarrow  \mathbb{Z}  \xrightarrow{f'}  \mathbb{Z}  \xrightarrow{g'}  \mathbb{Z}/2\mathbb{Z}  \longrightarrow  0
\end{array}
$$
其中 $f(x)=2x$，$f'(x)=2x$，$g, g'$ 是模2的投影，$\alpha(x)=2x$，$\beta(y)=2y$，$\gamma$ 是零映射。我们想计算 $\delta$ 对 $\ker(\gamma)$ 中一个元素的作用。由于 $\gamma=0$, $\ker(\gamma) = \mathbb{Z}/2\mathbb{Z}$。取非零元 $z = 1 + 2\mathbb{Z} \in \ker(\gamma)$。

1.  **向上追溯**：我们在 $B=\mathbb{Z}$ 中找到一个[原像](@entry_id:150899) $b$，使得 $g(b)=z$。一个简单的选择是 $b=1$。
2.  **向下映射**：将 $b$ 通过 $\beta$ 映到 $B'=\mathbb{Z}$，得到 $\beta(b) = \beta(1) = 2$。
3.  **验证与向左追溯**：由于图是交换的，$g'(\beta(b)) = \gamma(g(b)) = \gamma(z) = 0$。这意味着 $\beta(b)$ 在 $\ker(g')$ 中。因为下行正合，$\ker(g') = \text{Im}(f')$，所以存在一个唯一的 $a' \in A'=\mathbb{Z}$ 使得 $f'(a') = \beta(b)$。我们解方程 $2a' = 2$，得到 $a'=1$。
4.  **定义与向下投射**：[连接同态](@entry_id:160713) $\delta(z)$ 被定义为 $a'$ 在上核 $\text{coker}(\alpha) = A'/\text{Im}(\alpha)$ 中的等价类。这里 $\text{Im}(\alpha) = 2\mathbb{Z}$。所以，$\delta(z) = a' + \text{Im}(\alpha) = 1 + 2\mathbb{Z}$。

这个具体的计算过程 [@problem_id:1792316] 展示了 $\delta$ 如何“蜿蜒”穿过图，将上行右侧的信息 ($C$) 与下行左侧的信息 ($A'$) 联系起来。

#### 同调长正合序列

蛇形引理可以被推广到**[链复形](@entry_id:150246) (chain complex)** 的范畴。一个[链复形](@entry_id:150246) $\mathcal{A} = (A_n, \partial_n)$ 是一列模和[微分](@entry_id:158718)映射 $\dots \to A_{n+1} \xrightarrow{\partial_{n+1}} A_n \xrightarrow{\partial_n} A_{n-1} \to \dots$ 使得 $\partial_n \circ \partial_{n+1} = 0$。[链复形](@entry_id:150246)的**同调群 (homology group)** $H_n(\mathcal{A}) = \ker(\partial_n) / \text{Im}(\partial_{n+1})$ 度量了复形在 $n$ 次偏离正合的程度。

一个[链复形](@entry_id:150246)的短[正合序列](@entry_id:151503) $0 \to \mathcal{A} \xrightarrow{f} \mathcal{B} \xrightarrow{g} \mathcal{C} \to 0$ 会诱导出一个**同调长正合序列**：
$$ \dots \to H_n(\mathcal{A}) \to H_n(\mathcal{B}) \to H_n(\mathcal{C}) \xrightarrow{\delta_n} H_{n-1}(\mathcal{A}) \to \dots $$
这里的[连接同态](@entry_id:160713) $\delta_n$ 是蛇形引理中 $\delta$ 的高维推广。它揭示了不同复形的同调群之间深刻的内在联系。

我们可以通过一个实例来考察这个强大的工具 [@problem_id:1792315]。考虑一个由三个[链复形](@entry_id:150246)构成的短[正合序列](@entry_id:151503) $0 \to \mathcal{A} \to \mathcal{B} \to \mathcal{C} \to 0$，其中复形只在次数 0 和 1 非零。假设 $A_1=A_0=\mathbb{Z}$，$\partial_1^A(k)=2k$；$C_1=C_0=\mathbb{Z}$，$\partial_1^C=0$。通过具体的[图追踪](@entry_id:263851)构造，我们可以计算出[连接同态](@entry_id:160713) $\delta_1: H_1(\mathcal{C}) \to H_0(\mathcal{A})$。
首先计算相关的同调群：
-   $H_1(\mathcal{C}) = \ker(\partial_1^C)/\text{Im}(\partial_2^C) = C_1/0 \cong \mathbb{Z}$。
-   $H_0(\mathcal{A}) = \ker(\partial_0^A)/\text{Im}(\partial_1^A) = A_0/\text{Im}(\partial_1^A) = \mathbb{Z}/2\mathbb{Z}$。
通过追踪一个代表 $H_1(\mathcal{C})$ 中元素 $k \in \mathbb{Z}$ 的循环 $k \in C_1$，我们可以发现它在 $H_0(\mathcal{A})$ 中的像恰好是 $k \pmod 2$。因此，[连接同态](@entry_id:160713) $\delta_1$ 就是从 $\mathbb{Z}$到 $\mathbb{Z}/2\mathbb{Z}$ 的典范投影。它的核是所有偶数组成的[子群](@entry_id:146164) $2\mathbb{Z}$。这个例子清晰地展示了同调[长正合序列](@entry_id:153438)如何将不同复形、不同维度的代数信息联系起来，使其成为整个同调代数的基石。