## 引言
[子集](@entry_id:261956)、[真子集](@entry_id:152276)和幂集是现代数学语言的基石，是[集合论](@entry_id:137783)中最基本也是最强大的概念之一。理解这些概念不仅是学习抽象数学的入门要求，更是通往拓扑学、[抽象代数](@entry_id:145216)和计算机科学等高级领域的桥梁。然而，许多学习者常常停留在对这些概念的表面定义上，未能深入理解其背后的原理、丰富的内部结构以及它们在不同数学分支中扮演的关键角色。本文旨在填补这一空白，从“是什么”的定义出发，深入探索“为什么”的原理以及“如何用”的应用。在接下来的章节中，我们将首先在“原理与机制”中系统介绍[子集与幂集](@entry_id:152826)的基本定义、组合原理以及它们所形成的代数与序结构。随后，我们将在“应用与跨学科联系”中展示这些基础概念如何成为拓扑学、测度论和[抽象代数](@entry_id:145216)等领域中不可或缺的工具。最后，通过“动手实践”中的具体问题，读者将有机会巩固所学知识。通过这次探索，您将构建一个关于[子集和](@entry_id:634263)幂集的完整知识体系，并深刻体会到这些基础概念在整个数学大厦中的核心地位。

## 原理与机制

在介绍完[集合论](@entry_id:137783)的基本概念之后，本章将深入探讨[子集](@entry_id:261956)、[真子集](@entry_id:152276)以及[幂集](@entry_id:137423)这些核心概念的原理与机制。我们将从基本定义出发，逐步揭示这些概念在[组合计数](@entry_id:141086)、[代数结构](@entry_id:137052)和序理论中的深刻内涵。我们的目标是不仅理解这些“是什么”，更要探究其“为什么”如此，从而构建一个系统而严谨的知识框架。

### 基本概念：[子集与幂集](@entry_id:152826)

#### [子集](@entry_id:261956)与[真子集](@entry_id:152276)的定义

我们首先形式化地定义[子集](@entry_id:261956)关系。对于任意两个集合 $A$ 和 $B$，如果集合 $A$ 中的每一个元素也都是集合 $B$ 中的元素，那么我们称 $A$ 是 $B$ 的**[子集](@entry_id:261956)** (subset)，记作 $A \subseteq B$。用逻辑语言表述为：

$A \subseteq B \iff (\forall x, x \in A \implies x \in B)$

例如，若 $A = \{1, 2\}$ 且 $B = \{1, 2, 3\}$，则 $A \subseteq B$。根据这个定义，任何集合都是其自身的[子集](@entry_id:261956)，即 $A \subseteq A$。此外，**空集** (empty set) $\emptyset$ 不包含任何元素，因此“$x \in \emptyset$”这个前提总是假的，从而蕴涵式“$x \in \emptyset \implies x \in B$”对任何集合 $B$ 都恒为真。因此，空集是任何集合的[子集](@entry_id:261956)。

一个更严格的概念是**[真子集](@entry_id:152276)** (proper subset)。如果 $A$ 是 $B$ 的[子集](@entry_id:261956)，并且 $A$ 不等于 $B$（即存在至少一个元素属于 $B$ 但不属于 $A$），那么我们称 $A$ 是 $B$ 的[真子集](@entry_id:152276)，记作 $A \subset B$ 或 $A \subsetneq B$。其形式化定义为：

$A \subset B \iff (A \subseteq B \land A \neq B)$

#### 幂集：一个由集合构成的集合

基于[子集](@entry_id:261956)的概念，我们可以定义一个给定集合的**幂集** (power set)。一个集合 $S$ 的幂集，记作 $\mathcal{P}(S)$，是 $S$ 的所有[子集](@entry_id:261956)构成的集合。[幂集](@entry_id:137423)的元素本身就是集合。

例如，如果 $S = \{1, 2\}$，那么 $S$ 的所有[子集](@entry_id:261956)是：空集 $\emptyset$，单元素[子集](@entry_id:261956) $\{1\}$ 和 $\{2\}$，以及 $S$ 本身 $\{1, 2\}$。因此， $S$ 的幂集为：

$\mathcal{P}(S) = \{\emptyset, \{1\}, \{2\}, \{1, 2\}\}$

[幂集](@entry_id:137423)的一个基本性质是其基数（即元素的数量）。如果一个有限集 $S$ 的[基数](@entry_id:754020)为 $|S| = n$，那么其[幂集的基数](@entry_id:152099)为 $|\mathcal{P}(S)| = 2^n$。这个结论可以通过[组合论证](@entry_id:266316)得出：对于 $S$ 中的每一个元素，我们在构造一个[子集](@entry_id:261956)时都有两种选择——包含该元素或不包含该元素。由于 $S$ 中有 $n$ 个元素，且每个元素的选择是独立的，因此总共可以构造出 $2 \times 2 \times \dots \times 2$（$n$ 次），即 $2^n$ 个不同的[子集](@entry_id:261956)。

#### 集合的层级：元素 vs. [子集](@entry_id:261956)

初学者常常混淆**属于**关系 ($\in$) 和**包含**关系 ($\subseteq$)。$\in$ 描述的是元素与集合之间的关系，而 $\subseteq$ 描述的是两个集合之间的关系。幂集的概念是理解这一区别的关键。

考虑一个非[空集](@entry_id:261946)合 $X$。$\mathcal{P}(X)$ 是一个集合，它的*元素*是 $X$ 的*[子集](@entry_id:261956)*。让我们来分析一个看似棘手的问题：是否存在一个集合，它总是 $\mathcal{P}(\mathcal{P}(X))$ 的元素，但绝不是 $\mathcal{P}(X)$ 的元素？ [@problem_id:1823715]

要成为 $\mathcal{P}(\mathcal{P}(X))$ 的元素，一个集合 $A$ 必须满足 $A \subseteq \mathcal{P}(X)$。
要成为 $\mathcal{P}(X)$ 的元素，一个集合 $A$ 必须满足 $A \subseteq X$。

让我们来考察 $\mathcal{P}(X)$ 本身。
1.  根据[子集](@entry_id:261956)的定义，任何集合都是其自身的[子集](@entry_id:261956)，所以 $\mathcal{P}(X) \subseteq \mathcal{P}(X)$ 恒成立。根据[幂集](@entry_id:137423)的定义，这意味着 $\mathcal{P}(X) \in \mathcal{P}(\mathcal{P}(X))$。
2.  $\mathcal{P}(X)$ 是否是 $\mathcal{P}(X)$ 的元素？这需要 $\mathcal{P}(X) \subseteq X$。然而，根据著名的 Cantor 定理，任何集合的[幂集的基数](@entry_id:152099)都严格大于原集合的[基数](@entry_id:754020)，即 $|\mathcal{P}(X)| > |X|$。既然 $\mathcal{P}(X)$ 的元素比 $X$ 多，$\mathcal{P}(X)$ 就不可能是 $X$ 的[子集](@entry_id:261956)（除非在某些非标准集合论中）。因此，$\mathcal{P}(X) \notin \mathcal{P}(X)$。

结论是，$\mathcal{P}(X)$ 本身就是一个满足条件的集合。这个例子深刻地揭示了集合、其幂集、其幂集的幂集之间逐级递升的层级关系。

我们可以通过一个[递归定义](@entry_id:266613)的[集合序列](@entry_id:184571)来进一步探索这种层级结构 [@problem_id:1823719]。令 $S_0 = \emptyset$，并且对所有 $k \ge 0$，定义 $S_{k+1} = \mathcal{P}(S_k)$。这个序列的前几项是：
$S_0 = \emptyset$
$S_1 = \mathcal{P}(S_0) = \mathcal{P}(\emptyset) = \{\emptyset\}$
$S_2 = \mathcal{P}(S_1) = \mathcal{P}(\{\emptyset\}) = \{\emptyset, \{\emptyset\}\}$
$S_3 = \mathcal{P}(S_2) = \{\emptyset, \{\emptyset\}, \{\{\emptyset\}\}, \{\emptyset, \{\emptyset\}\}\}$

现在，我们来分析关系 $S_n \in S_m$ 成立的条件。根据[幂集](@entry_id:137423)的定义，$S_n \in S_m$ 等价于 $S_n \subseteq S_{m-1}$ (对于 $m \ge 1$)。通过归纳法可以证明，该序列是单调递增的，即 $S_i \subseteq S_j$ 当且仅当 $i \le j$。因此，$S_n \subseteq S_{m-1}$ 等价于 $n \le m-1$，也即 $n  m$。这个优美的结论将抽象的集合归属关系转化为了简单的整数不等式，清晰地展示了由[幂集](@entry_id:137423)运算所构建的无限层级。

### [子集](@entry_id:261956)的组合原理

掌握了[子集和](@entry_id:634263)幂集的基本定义后，我们转向与计数相关的组合问题。

#### 带约束条件的[子集](@entry_id:261956)计数

计算一个集合的[子集](@entry_id:261956)数量是组合数学的基本问题。正如我们所知，一个 $n$ 元集合有 $2^n$ 个[子集](@entry_id:261956)。当问题增加一些约束条件时，计数方法也需要相应调整。

一个常见的约束是要求[子集](@entry_id:261956)必须包含某个特定的元素。例如，在一个集合 $S_2$ 中，要计算包含特定元素 $s \in S_2$ 的[子集](@entry_id:261956)数量，我们可以这样思考：在构造[子集](@entry_id:261956)时，元素 $s$ 是必须被选中的，我们没有选择的余地。而对于 $S_2$ 中其余的 $|S_2| - 1$ 个元素，每一个我们仍然可以自由选择“包含”或“不包含”。因此，包含 $s$ 的[子集](@entry_id:261956)数量为 $2^{|S_2|-1}$。

让我们看一个更复杂的例子 [@problem_id:1823728]。假设 $S_1$ 是 $S_2$ 的[真子集](@entry_id:152276)，其中 $|S_1|=n$ 且 $|S_2 \setminus S_1|=k$ ($n, k \ge 1$)。我们要计算满足以下三个条件的 $S_2$ 的[子集](@entry_id:261956) $T$ 的数量：
1. $T$ 是 $S_2$ 的[真子集](@entry_id:152276)。
2. $T$ 不是 $S_1$ 的[子集](@entry_id:261956)。
3. $T$ 包含一个固定的元素 $s \in S_2 \setminus S_1$。

分析这些条件：条件3是核心。任何包含 $s$ 的集合 $T$ 都不可能是 $S_1$ 的[子集](@entry_id:261956)，因为 $s \notin S_1$。因此，条件3自动满足了条件2。问题简化为：计算包含 $s$ 的 $S_2$ 的[真子集](@entry_id:152276)的数量。

$S_2$ 的[基数](@entry_id:754020)为 $|S_2| = |S_1| + |S_2 \setminus S_1| = n+k$。包含 $s$ 的 $S_2$ [子集](@entry_id:261956)的总数是 $2^{(n+k)-1}$。这些[子集](@entry_id:261956)中，只有一个不是[真子集](@entry_id:152276)，那就是 $S_2$ 本身。根据条件1，我们必须排除这个集合。因此，满足所有条件的[子集](@entry_id:261956)数量为 $2^{n+k-1}-1$。

#### 在代数背景下应用[子集](@entry_id:261956)计数

[子集](@entry_id:261956)计数不仅是组合学中的练习，它也是一种可以应用于其他数学分支（如抽象代数）的强大工具。

考虑在模12的[整数环](@entry_id:181003) $\mathbb{Z}_{12} = \{0, 1, \dots, 11\}$ 中的一个问题 [@problem_id:1823711]。我们定义两个集合：
- $A$ 是 $\mathbb{Z}_{12}$ 中所有乘法单位元（即有乘法[逆元](@entry_id:140790)的元素）的集合。
- $B$ 是 $\mathbb{Z}_{12}$ 中所有不是零因子的元素（根据问题定义，包括0）的集合。

任务是确定 $B$ 的[子集](@entry_id:261956)中，有多少个不是 $A$ 的[子集](@entry_id:261956)。

首先，我们需要确定集合 $A$ 和 $B$。一个元素 $u \in \mathbb{Z}_{12}$ 是单位元当且仅当 $\gcd(u, 12)=1$。这些元素是 $\{1, 5, 7, 11\}$，所以 $A=\{1, 5, 7, 11\}$。一个非零元素 $x$ 是**零因子**当且仅当 $\gcd(x, 12)>1$。因此，$\mathbb{Z}_{12}$ 中的[零因子](@entry_id:151051)是单位元之外的非零元素。根据定义，[零因子](@entry_id:151051)不包括0，因此零因子在 $\mathbb{Z}_{12}$ 中的[补集](@entry_id:161099)（即集合 $B$）包含所有单位元以及元素0。所以 $B=\{0, 1, 5, 7, 11\}$。

我们发现 $A \subset B$，且 $B \setminus A = \{0\}$。一个 $B$ 的[子集](@entry_id:261956)如果不是 $A$ 的[子集](@entry_id:261956)，那么它必须至少包含一个不在 $A$ 中的元素。在这里，这个元素只能是 $0$。因此，问题转化为：计算 $B$ 中有多少个包含元素 $0$ 的[子集](@entry_id:261956)。

这与我们之前讨论的计数原理完全相同。要构造一个包含 $0$ 的 $B$ 的[子集](@entry_id:261956)，我们必须选择 $0$，然后可以从 $B \setminus \{0\} = A$ 中任意选择一个[子集](@entry_id:261956)与之组合。$A$ 的[基数](@entry_id:754020)是4，所以有 $2^{|A|} = 2^4 = 16$ 种选择。因此，有16个 $B$ 的[子集](@entry_id:261956)不是 $A$ 的[子集](@entry_id:261956)。

### [幂集](@entry_id:137423)的[代数结构](@entry_id:137052)

[幂集](@entry_id:137423)不仅是一个集合的集合，它还可以被赋予丰富的[代数结构](@entry_id:137052)。

#### 与标准[集合运算](@entry_id:143311)的相互作用

一个自然的问题是，幂集运算 $\mathcal{P}$ 如何与标准的[集合运算](@entry_id:143311)（如交 $\cap$、并 $\cup$、差 $\setminus$、[笛卡尔积](@entry_id:154642) $\times$）相互作用？系统地考察这些关系可以加深我们对[幂集](@entry_id:137423)的理解 [@problem_id:1823729]。

1.  **[幂集](@entry_id:137423)与交集**：$\mathcal{P}(A \cap B) = \mathcal{P}(A) \cap \mathcal{P}(B)$ 是否成立？
    一个集合 $X$ 是 $\mathcal{P}(A \cap B)$ 的元素，当且仅当 $X \subseteq A \cap B$。这又等价于 $X \subseteq A$ 且 $X \subseteq B$。而这正好是 $X \in \mathcal{P}(A)$ 且 $X \in \mathcal{P}(B)$ 的定义，也即 $X \in \mathcal{P}(A) \cap \mathcal{P}(B)$。因此，这个等式**恒成立**。

2.  **幂集与并集**：$\mathcal{P}(A \cup B) = \mathcal{P}(A) \cup \mathcal{P}(B)$ 是否成立？
    如果 $X \in \mathcal{P}(A) \cup \mathcal{P}(B)$，那么 $X \subseteq A$ 或 $X \subseteq B$。在这两种情况下，都有 $X \subseteq A \cup B$，所以 $X \in \mathcal{P}(A \cup B)$。这说明 $\mathcal{P}(A) \cup \mathcal{P}(B) \subseteq \mathcal{P}(A \cup B)$ 总是成立的。
    然而，反向包含不一定成立。考虑一个简单的反例 [@problem_id:1823706]：设 $A=\{a\}$，$B=\{b\}$，其中 $a \neq b$。那么 $A \cup B = \{a, b\}$。
    $\mathcal{P}(A) = \{\emptyset, \{a\}\}$
    $\mathcal{P}(B) = \{\emptyset, \{b\}\}$
    $\mathcal{P}(A) \cup \mathcal{P}(B) = \{\emptyset, \{a\}, \{b\}\}$
    $\mathcal{P}(A \cup B) = \{\emptyset, \{a\}, \{b\}, \{a, b\}\}$
    显然，集合 $\{a, b\}$ 是 $\mathcal{P}(A \cup B)$ 的元素，但它不是 $\mathcal{P}(A)$ 或 $\mathcal{P}(B)$ 的元素。因此，这个等式**不恒成立**。

3.  **[幂集](@entry_id:137423)与集合差**：$\mathcal{P}(A \setminus B) = \mathcal{P}(A) \setminus \mathcal{P}(B)$ 是否成立？
    这个等式几乎永远不成立。[空集](@entry_id:261946) $\emptyset$ 是任何集合的[子集](@entry_id:261956)，所以 $\emptyset \in \mathcal{P}(A \setminus B)$。然而，在等式右边，$\mathcal{P}(A) \setminus \mathcal{P}(B)$ 的定义是属于 $\mathcal{P}(A)$ 但不属于 $\mathcal{P}(B)$ 的集合。由于 $\emptyset \in \mathcal{P}(B)$，所以 $\emptyset \notin \mathcal{P}(A) \setminus \mathcal{P}(B)$。两边一个包含空集一个不包含，所以它们不相等。

4.  **幂集与笛卡尔积**：对于非空[有限集](@entry_id:145527) $A$ 和 $B$，$|\mathcal{P}(A \times B)| = |\mathcal{P}(A)| \cdot |\mathcal{P}(B)|$ 是否成立？
    利用基数公式，等式左边是 $2^{|A \times B|} = 2^{|A| \cdot |B|}$。等式右边是 $2^{|A|} \cdot 2^{|B|} = 2^{|A| + |B|}$。要使等式成立，需要指数相等，即 $|A| \cdot |B| = |A| + |B|$。这个方程可以改写为 $(|A|-1)(|B|-1)=1$。由于[基数](@entry_id:754020)是正整数，唯一的解是 $|A|=2$ 且 $|B|=2$。因为该命题声称对所有非空有限集都成立，而我们找到了反例（例如 $|A|=1, |B|=3$），所以这个等式**不恒成立**。

#### 另一种视角：特征函数

表示[子集](@entry_id:261956)有一种非常强大的代数方法，即使用**[特征函数](@entry_id:186820)** (characteristic function) [@problem_id:1823734]。对于一个[全集](@entry_id:264200) $S$，任何[子集](@entry_id:261956) $A \subseteq S$ 都可以由其[特征函数](@entry_id:186820) $f_A: S \to \{0, 1\}$ 唯一确定：
$f_A(s) = \begin{cases} 1  \text{if } s \in A \\ 0  \text{if } s \notin A \end{cases}$

这种表示法在 $\mathcal{P}(S)$ 与所有从 $S$ 到 $\{0, 1\}$ 的函数的集合之间建立了[一一对应](@entry_id:143935)。这也为[幂集的基数](@entry_id:152099)公式提供了另一种解释：对于 $|S|=n$ 的情况，构造一个这样的函数需要为 $n$ 个输入中的每一个指定一个输出（0或1），总共有 $2^n$ 种可能性。

更重要的是，[集合运算](@entry_id:143311)可以被翻译成特征函数上的算术运算。例如，对于任意 $s \in S$：
- **交集**：$s \in A \cap B$ 当且仅当 $s \in A$ 且 $s \in B$。这对应于 $f_{A \cap B}(s) = f_A(s) \cdot f_B(s)$。
- **[补集](@entry_id:161099)**：$s \in S \setminus A$ 当且仅当 $s \notin A$。这对应于 $f_{S \setminus A}(s) = 1 - f_A(s)$。
- **[对称差](@entry_id:156264)**：一个特别优雅的对应关系出现在**[对称差](@entry_id:156264)** (symmetric difference) 运算中。$A \Delta B = (A \cup B) \setminus (A \cap B)$，即属于 $A$ 或 $B$ 但不属于两者交集的元素构成的集合。一个元素 $s$ 属于 $A \Delta B$ 当且仅当它恰好属于 $A$ 和 $B$ 中的一个。这对应于[特征函数](@entry_id:186820)值之和为1。在模2算术下，这可以简洁地表示为：
$f_{A \Delta B}(s) = (f_A(s) + f_B(s)) \pmod 2$
这个关系是连接集合论和抽象代数的关键桥梁。

#### [对称差](@entry_id:156264)下的[群结构](@entry_id:146855)

利用[特征函数](@entry_id:186820)的视角，我们可以揭示 $(\mathcal{P}(S), \Delta)$ 构成一个**[阿贝尔群](@entry_id:150284)** (abelian group) [@problem_id:1823727]。我们来验证群的公理：

1.  **封闭性 (Closure)**：对于任意 $A, B \in \mathcal{P}(S)$，$A \Delta B$ 仍然是 $S$ 的一个[子集](@entry_id:261956)，因此属于 $\mathcal{P}(S)$。
2.  **结合律 (Associativity)**：我们需要证明 $(A \Delta B) \Delta C = A \Delta (B \Delta C)$。使用[特征函数](@entry_id:186820)，这相当于证明 $(f_A+f_B)+f_C \equiv f_A+(f_B+f_C) \pmod 2$。由于模2加法满足[结合律](@entry_id:151180)，所以[对称差](@entry_id:156264)运算也满足[结合律](@entry_id:151180)。
3.  **单位元 (Identity Element)**：我们需要找到一个集合 $E$ 使得对任意 $A \in \mathcal{P}(S)$ 都有 $A \Delta E = A$。我们发现[空集](@entry_id:261946) $\emptyset$ 满足这个要求：$A \Delta \emptyset = (A \cup \emptyset) \setminus (A \cap \emptyset) = A \setminus \emptyset = A$。因此，$\emptyset$ 是单位元。
4.  **[逆元](@entry_id:140790) (Inverse Element)**：对于每个 $A \in \mathcal{P}(S)$，我们需要找到一个 $A^{-1}$ 使得 $A \Delta A^{-1} = \emptyset$。一个惊人的事实是，每个元素都是其自身的逆元：$A \Delta A = (A \cup A) \setminus (A \cap A) = A \setminus A = \emptyset$。
5.  **[交换律](@entry_id:141214) (Commutativity)**：$A \Delta B = (A \cup B) \setminus (A \cap B) = (B \cup A) \setminus (B \cap A) = B \Delta A$。因此，该运算是可交换的。

由于满足以上所有公理，$(\mathcal{P}(S), \Delta)$ 构成一个阿贝尔群。在这个群中，每个[元素的阶](@entry_id:145276)都是2（除了单位元），这是一个非常特殊的结构。需要注意的是，一个集合 $A$ 的[逆元](@entry_id:140790)是它自身，而不是它的补集 $S \setminus A$。因为 $A \Delta (S \setminus A) = (A \cup (S \setminus A)) \setminus (A \cap (S \setminus A)) = S \setminus \emptyset = S$，而 $S$ 只有在 $S=\emptyset$ 时才是单位元。

### [幂集](@entry_id:137423)的序结构

除了[代数结构](@entry_id:137052)，幂集在其元素之间还具有自然的序结构，这为研究格论 (lattice theory) 提供了原型。

#### 幂集上的偏[序关系](@entry_id:138937)

一个关系被称为**偏序** (partial order) 如果它满足[自反性](@entry_id:137262)、[反对称性](@entry_id:261893)和传递性。

让我们考虑在 $\mathcal{P}(S)$ 上的[子集](@entry_id:261956)包含关系 $\subseteq$。
- **[自反性](@entry_id:137262) (Reflexivity)**：对任意 $A \in \mathcal{P}(S)$，$A \subseteq A$ 成立。
- **反对称性 (Antisymmetry)**：如果 $A \subseteq B$ 且 $B \subseteq A$，那么根据集合外延性公理，必有 $A=B$。
- **传递性 (Transitivity)**：如果 $A \subseteq B$ 且 $B \subseteq C$，那么 $A$ 的每个元素都在 $B$ 中，而 $B$ 的每个元素都在 $C$ 中，因此 $A$ 的每个元素也都在 $C$ 中，即 $A \subseteq C$。

由于 $\subseteq$ 满足这三个性质，$(\mathcal{P}(S), \subseteq)$ 是一个**[偏序集](@entry_id:274760)** (partially ordered set, or poset)。

与此相对，[真子集](@entry_id:152276)关系 $\subset$ 具有不同的性质 [@problem_id:2309708]。它显然不是自反的，因为 $A \subset A$ 要求 $A \neq A$，这是不可能的。然而，它仍然是反对称的（因为前提 $A \subset B$ 和 $B \subset A$ 不可能同时成立，所以蕴含式是[空真](@entry_id:262024) (vacuously true) 的）和传递的。不满足[自反性](@entry_id:137262)的这种关系被称为**严格[偏序](@entry_id:145467)** (strict partial order)。

#### 幂集作为完备有界格

在偏序集 $(\mathcal{P}(S), \subseteq)$ 中，我们可以定义[任意子](@entry_id:143753)集族的[上确界](@entry_id:140512)和[下确界](@entry_id:140118)。对于 $\mathcal{P}(S)$ 的一个[子集](@entry_id:261956)（即一个集合的集合）$\mathcal{C} \subseteq \mathcal{P}(S)$：
- 其**[上确界](@entry_id:140512)** (supremum) 或**并** (join) 是 $\mathcal{C}$ 中所有集合的并集：$\sup(\mathcal{C}) = \bigcup_{X \in \mathcal{C}} X$。这是包含 $\mathcal{C}$ 中所有集合的“最小”集合。
- 其**下确界** (infimum) 或**交** (meet) 是 $\mathcal{C}$ 中所有集合的交集：$\inf(\mathcal{C}) = \bigcap_{X \in \mathcal{C}} X$。这是被 $\mathcal{C}$ 中所有集合包含的“最大”集合。

例如，考虑 $S = \{1, 2, \dots, 20\}$，以及一个集合族 $\mathcal{F} = \{F_1, F_2, F_3, F_4\}$，其中 $F_k = \{n \in S \mid n \ge k\}$ [@problem_id:1823720]。这个族的[下确界](@entry_id:140118)是：
$M_F = \inf(\mathcal{F}) = \bigcap_{k=1}^4 F_k = F_1 \cap F_2 \cap F_3 \cap F_4$
由于 $F_4 \subset F_3 \subset F_2 \subset F_1$，它们的交集就是最小的那个集合，即 $M_F = F_4 = \{4, 5, \dots, 20\}$。

因为对于 $\mathcal{P}(S)$ 的*任意*子族（无论有限还是无限），其上确界（并集）和[下确界](@entry_id:140118)（交集）都存在于 $\mathcal{P}(S)$ 中，所以我们称 $(\mathcal{P}(S), \subseteq)$ 是一个**完备格** (complete lattice)。此外，这个格存在一个[最大元](@entry_id:276547)（[全集](@entry_id:264200) $S$）和一个[最小元](@entry_id:265018)（[空集](@entry_id:261946) $\emptyset$），因此它也是一个**有界格** (bounded lattice)。

[幂集](@entry_id:137423)作为完备有界格的性质，使其成为[布尔代数](@entry_id:168482)的一个典型模型，并在逻辑学、计算机科学和拓扑学等领域扮演着基础性的角色。