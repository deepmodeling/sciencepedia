## 引言
在数学的宏伟版图中，集合论是现代数学几乎所有分支赖以建立的基石。而在集合论的核心，**[子集](@entry_id:261956)**与**幂集**的概念不仅定义了集合之间最基本的关系，更是一种强大的构造工具，能够从简单的对象生成无法想象的复杂宇宙。尽管概念初看简单，但深入其中会发现，对元素与[子集](@entry_id:261956)关系的混淆，以及对幂集所蕴含的深刻结构与广泛应用的忽视，是许多学习者面临的普遍障碍。本文旨在填补这一认知鸿沟，引领读者从基础原理走向前沿应用。

本文将分为三个部分，系统地展开对[子集与幂集](@entry_id:152826)的探索。在“**原理与机制**”一章中，我们将从最基本的定义和符号出发，厘清关键区别，探讨[幂集的基数](@entry_id:152099)性质、核心的[康托定理](@entry_id:141918)，以及其内在的代数与序结构。接着，在“**应用与跨学科联系**”一章中，我们将展示这些抽象概念如何在**计算机科学**的组合优化、**[抽象代数](@entry_id:145216)**的群与[格理论](@entry_id:147950)，以及**拓扑学**与**分析学**的空间构造中焕发活力。最后，“**动手实践**”部分将通过一系列精心设计的问题，帮助你将理论知识转化为解决实际问题的能力。通过这次学习，你将不仅掌握[子集与幂集](@entry_id:152826)的技术细节，更将体会到它们作为一种通用语言，在描述和构建数学[世界时](@entry_id:275204)所展现出的力量与美感。

## 原理与机制

本章旨在深入探讨[集合论](@entry_id:137783)的基石性概念：[子集与幂集](@entry_id:152826)。我们将从基本定义出发，系统地阐明这些概念的内在属性、它们之间的相互作用，以及它们在构建更复杂数学结构时所扮演的关键角色。本章内容假定读者已对集合的基本概念有所了解。

### 基本概念：[子集与幂集](@entry_id:152826)

在[集合论](@entry_id:137783)中，两个集合之间最基本的关系之一是包含关系。如果集合 $A$ 中的每一个元素也都是集合 $B$ 的元素，我们称 $A$ 是 $B$ 的一个**[子集](@entry_id:261956)** (subset)，记作 $A \subseteq B$。如果 $A$ 是 $B$ 的[子集](@entry_id:261956)，并且 $A$ 不等于 $B$（即，存在至少一个元素属于 $B$ 但不属于 $A$），那么我们称 $A$ 是 $B$ 的一个**[真子集](@entry_id:152276)** (proper subset)，记作 $A \subsetneq B$。

一个初学者极易混淆的概念是**元素关系** ($\in$) 与**[子集](@entry_id:261956)关系** ($\subseteq$)。元素关系描述的是一个对象与一个集合之间的关系，而[子集](@entry_id:261956)关系描述的是两个集合之间的关系。考察以下几个普遍性命题可以帮助我们澄清这一区别 [@problem_id:1823699]：

(I)  **$S \in \mathcal{P}(S)$**：此命题是否对任意集合 $S$ 恒成立？
(II)  **$S \subseteq \mathcal{P}(S)$**：此命题是否对任意集合 $S$ 恒成立？
(III)  **$\emptyset \in S$**：此命题是否对任意集合 $S$ 恒成立？
(IV)  **$\emptyset \subseteq \mathcal{P}(S)$**：此命题是否对任意集合 $S$ 恒成立？

为了回答这些问题，我们首先需要引入**幂集** (power set) 的定义。对于任意集合 $S$，其幂集 $\mathcal{P}(S)$ 是一个由 $S$ 的所有[子集](@entry_id:261956)构成的集合。形式化地，$\mathcal{P}(S) = \{A : A \subseteq S\}$。这个定义是理解上述命题的关键。从定义可知，一个集合 $A$ 是 $S$ 的[子集](@entry_id:261956)，当且仅当 $A$ 是[幂集](@entry_id:137423) $\mathcal{P}(S)$ 的一个元素，即 $A \subseteq S \iff A \in \mathcal{P}(S)$。

现在我们可以逐一分析这些命题。对于命题 (I)，$S \in \mathcal{P}(S)$ 等价于 $S \subseteq S$。根据[子集](@entry_id:261956)的定义，任何集合都是其自身的[子集](@entry_id:261956)（自反性），因此 $S \subseteq S$ 恒成立。故命题 (I) 是普遍为真的。

对于命题 (II)，$S \subseteq \mathcal{P}(S)$ 意为 $S$ 的每一个元素也都是 $\mathcal{P}(S)$ 的元素。换言之，对于任意 $x \in S$，都必须有 $x \in \mathcal{P}(S)$，这又等价于 $x \subseteq S$。这个要求并非普遍成立。例如，若 $S = \{1, 2\}$，其元素 $1$ 和 $2$ 通常被视为原子元素（urelements），而非集合，因此谈论 $1 \subseteq S$ 是没有意义的。所以命题 (II) 不是普遍为真的。

对于命题 (III)，$\emptyset \in S$ 意为空集是集合 $S$ 的一个元素。这显然不是对所有集合都成立的。例如，集合 $S = \{1, 2\}$ 就不包含空集作为其元素。因此，命题 (III) 不是普遍为真的。

对于命题 (IV)，$\emptyset \subseteq \mathcal{P}(S)$ 意为[空集](@entry_id:261946)是幂集 $\mathcal{P}(S)$ 的一个[子集](@entry_id:261956)。一个基本公理是，[空集](@entry_id:261946)是任何集合的[子集](@entry_id:261956)。这是因为“空集中的每一个元素都属于另一个集合”这一陈述是**虚真** (vacuously true) 的——因为[空集](@entry_id:261946)中没有任何元素可以违反这个陈述。由于 $\mathcal{P}(S)$ 本身是一个集合，所以[空集](@entry_id:261946)必然是它的[子集](@entry_id:261956)。故命题 (IV) 是普遍为真的。

从[公理化集合论](@entry_id:156777)（如[Zermelo-Fraenkel集合论](@entry_id:154200)，简称ZF）的视角来看，[幂集](@entry_id:137423)的存在性是由**幂集公理** (Axiom of Power Set) 所保证的。该公理断言，对任意存在的集合 $A$，总存在一个集合 $P$，其元素恰好是 $A$ 的所有[子集](@entry_id:261956) [@problem_id:3052609]。而**[外延公理](@entry_id:151419)** (Axiom of Extensionality) 保证了具有相同元素的两个集合是相等的，这确保了任意集合 $A$ 的[幂集](@entry_id:137423)是唯一的。

### 基数与[组合性](@entry_id:637804)质

一个直接的问题是，如果一个集合 $S$ 是有限的，它的幂集有多大？假设集合 $S$ 的**基数** (cardinality) 为 $|S| = n$，其中 $n$ 是一个非负整数。我们可以通过一个简单的[组合论证](@entry_id:266316)来确定 $|\mathcal{P}(S)|$。要构造 $S$ 的一个[子集](@entry_id:261956)，我们需要对 $S$ 中的每一个元素做出一个决定：是将其包含在这个[子集](@entry_id:261956)中，还是不包含。由于 $S$ 中有 $n$ 个元素，每个元素都有 2 种选择，且这些选择是相互独立的。根据[乘法原理](@entry_id:273377)，总共可以构造出 $2 \times 2 \times \dots \times 2$ ($n$ 次) 个不同的[子集](@entry_id:261956)。因此，我们得到基本公式：

$|S| = n \implies |\mathcal{P}(S)| = 2^n$

这个结论可以通过**特征函数** (characteristic function) 的概念得到更严谨的表述 [@problem_id:3052609]。对于[任意子](@entry_id:143753)集 $A \subseteq S$，我们可以定义其特征函数 $\chi_A: S \to \{0, 1\}$ 如下：
$$
\chi_A(x) = \begin{cases} 1  \text{if } x \in A, \\ 0  \text{if } x \notin A. \end{cases}
$$
每个[子集](@entry_id:261956) $A$ 唯一地对应一个特征函数 $\chi_A$，反之，每个从 $S$ 到 $\{0, 1\}$ 的函数也唯一地定义了 $S$ 的一个[子集](@entry_id:261956)（即所有使得函数值为1的元素的集合）。因此，在 $\mathcal{P}(S)$ 与所有这类特征函数构成的集合之间存在一个**[双射](@entry_id:138092)** (bijection)。如果 $|S|=n$，从一个 $n$ 元集到一个 2 元集的函数总数是 $2^n$，这再次证明了 $|\mathcal{P}(S)| = 2^n$。

这一结果引出了一个更深刻的问题：对于[无限集](@entry_id:137163)，其[基数](@entry_id:754020)与[幂集的基数](@entry_id:152099)之间有何关系？**[康托定理](@entry_id:141918)** (Cantor's Theorem) 给出了惊人的答案：对于任何集合 $A$（无论有限还是无限），它的基数严格小于其[幂集的基数](@entry_id:152099)，即 $|A|  |\mathcal{P}(A)|$。这意味着不存在从 $A$ 到 $\mathcal{P}(A)$ 的[满射函数](@entry_id:138553)。

我们可以通过一个精妙的[对角论证](@entry_id:262483)来理解这个定理。考虑任意一个函数 $f: X \to \mathcal{P}(X)$。我们的目标是证明 $f$ 不可能是满射，即存在 $\mathcal{P}(X)$ 中的某个元素，它不在 $f$ 的值域中。为了构造这样一个元素，我们定义一个特殊的“对角”集合 $D$ [@problem_id:1576791]：
$$
D = \{ x \in X : x \notin f(x) \}
$$
这个集合 $D$ 由所有不属于其在 $f$ 下的像的元素 $x$ 构成。现在我们来论证 $D$ 不可能等于任何一个 $f(k)$，其中 $k \in X$。我们用[反证法](@entry_id:276604)：假设存在某个 $k \in X$ 使得 $f(k) = D$。那么我们可以问：元素 $k$ 是否属于 $D$？

-   如果 $k \in D$，根据 $D$ 的定义，必然有 $k \notin f(k)$。但我们假设了 $f(k)=D$，这导致 $k \notin D$。这是一个矛盾。
-   如果 $k \notin D$，根据 $D$ 的定义，必然有 $k \in f(k)$。同样，因为 $f(k)=D$，这导致 $k \in D$。这又是一个矛盾。

由于无论哪种情况都会导出矛盾，我们最初的假设“存在 $k \in X$ 使得 $f(k) = D$”必定是错误的。这意味着我们构造的集合 $D$ 不在函数 $f$ 的值域中。由于 $f$ 是任意选择的，这就证明了不存在从 $X$到 $\mathcal{P}(X)$ 的满射。[康托定理](@entry_id:141918)揭示了无限基数存在着一个无穷的阶梯：$|A|  |\mathcal{P}(A)|  |\mathcal{P}(\mathcal{P}(A))|  \dots$。

[幂集](@entry_id:137423)的[组合性](@entry_id:637804)质是解决许多计数问题的有力工具。例如，考虑这样一个问题：给定一个 $n$ 元集 $X$，包含多少对有序[子集](@entry_id:261956) $(A, B)$ 使得 $A \cup B = X$ 且 $A \cap B \neq \emptyset$？[@problem_id:3052605]

解决这个问题的有效策略是考察 $X$ 中的每一个元素 $x$ 可能的归属。对于一个[有序对](@entry_id:269702) $(A, B)$，每个元素 $x$ 有四种可能的位置：
1.  $x \in A$ 且 $x \notin B$ (即 $x \in A \setminus B$)
2.  $x \notin A$ 且 $x \in B$ (即 $x \in B \setminus A$)
3.  $x \in A$ 且 $x \in B$ (即 $x \in A \cap B$)
4.  $x \notin A$ 且 $x \notin B$ (即 $x \notin A \cup B$)

第一个条件 $A \cup B = X$ 排除了第四种可能性。因此，对于满足此条件的每一对 $(A, B)$，$X$ 中的每个元素必须位于前三种区域之一。由于有 $n$ 个元素，每个元素有 3 种独立选择，满足 $A \cup B = X$ 的[有序对](@entry_id:269702)总数为 $3^n$。

第二个条件是 $A \cap B \neq \emptyset$。直接计数较为复杂，我们转而计算其补集，即满足 $A \cup B = X$ 且 $A \cap B = \emptyset$ 的[有序对](@entry_id:269702)数量。条件 $A \cap B = \emptyset$ 意味着第三种区域（$A \cap B$）必须为空，即任何元素都不能归属于此。因此，对于满足这两个补集条件的每一对 $(A, B)$，$X$ 中的每个元素只有两种选择：属于 $A \setminus B$ 或属于 $B \setminus A$。这样的[有序对](@entry_id:269702)总数为 $2^n$。

最后，我们所求的数量等于满足第一个条件的对数减去不满足第二个条件的对数。所以，满足条件的[有序对](@entry_id:269702) $(A, B)$ 的总数为 $3^n - 2^n$。

另一个例子可以进一步展示组合推理的力量 [@problem_id:1823728]。设 $S_1 \subsetneq S_2$，$|S_1| = n \ge 1$，$|S_2 \setminus S_1| = k \ge 1$。我们要计算 $S_2$ 的[子集](@entry_id:261956)中，满足以下所有条件的数量：(1) 是 $S_2$ 的[真子集](@entry_id:152276)；(2) 不是 $S_1$ 的[子集](@entry_id:261956)；(3) 包含一个特定的元素 $s \in S_2 \setminus S_1$。
首先，任何包含元素 $s$ 的[子集](@entry_id:261956)必然不是 $S_1$ 的[子集](@entry_id:261956)，因为 $s \notin S_1$。因此，条件 (2) 被条件 (3) 自动满足。问题简化为计算包含 $s$ 的 $S_2$ 的[真子集](@entry_id:152276)的数量。
$S_2$ 的总基数为 $n+k$。要构造一个包含 $s$ 的[子集](@entry_id:261956)，我们只需对 $S_2$ 中除了 $s$ 以外的 $n+k-1$ 个元素做选择（包含或不包含）。因此，包含 $s$ 的[子集](@entry_id:261956)总数为 $2^{n+k-1}$。
最后，条件 (1) 要求这是一个[真子集](@entry_id:152276)，所以我们需要排除 $S_2$ 本身。在这 $2^{n+k-1}$ 个[子集](@entry_id:261956)中，只有一个是 $S_2$ 自身（即选择了所有 $n+k-1$ 个其他元素）。因此，最终答案是 $2^{n+k-1} - 1$。

### [幂集](@entry_id:137423)的代数

幂集运算与标准的[集合运算](@entry_id:143311)（并、交、补）之间存在着重要的代数关系。理解这些关系对于在集合论框架内进行推理至关重要。

首先，我们考察幂集与**交集** ($\cap$) 的关系。一个关键的性质是，[幂集](@entry_id:137423)运算在交集上是**分配**的 [@problem_id:3052603] [@problem_id:1823729]：
$$
\mathcal{P}(A \cap B) = \mathcal{P}(A) \cap \mathcal{P}(B)
$$
我们可以通过证明双向包含来验证这个等式。
-   证明 $\mathcal{P}(A \cap B) \subseteq \mathcal{P}(A) \cap \mathcal{P}(B)$：任取 $X \in \mathcal{P}(A \cap B)$，这意味着 $X \subseteq A \cap B$。根据交集的定义，$X \subseteq A$ 且 $X \subseteq B$。前者意味着 $X \in \mathcal{P}(A)$，后者意味着 $X \in \mathcal{P}(B)$。因此，$X \in \mathcal{P}(A) \cap \mathcal{P}(B)$。
-   证明 $\mathcal{P}(A) \cap \mathcal{P}(B) \subseteq \mathcal{P}(A \cap B)$：任取 $Y \in \mathcal{P}(A) \cap \mathcal{P}(B)$，这意味着 $Y \in \mathcal{P}(A)$ 且 $Y \in \mathcal{P}(B)$。这等价于 $Y \subseteq A$ 且 $Y \subseteq B$。因此，$Y$ 的所有元素都必须同时在 $A$ 和 $B$ 中，这意味着 $Y \subseteq A \cap B$。所以，$Y \in \mathcal{P}(A \cap B)$。
由于双向包含成立，等式得证。

然而，[幂集](@entry_id:137423)运算与**并集** ($\cup$) 的关系则不同。[幂集](@entry_id:137423)运算在并集上并**不**分配。也就是说，等式 $\mathcal{P}(A \cup B) = \mathcal{P}(A) \cup \mathcal{P}(B)$ 通常是不成立的 [@problem_id:3052603] [@problem_id:1823729]。
正确的包含关系是 $\mathcal{P}(A) \cup \mathcal{P}(B) \subseteq \mathcal{P}(A \cup B)$。这是因为 $A$ 的任何[子集](@entry_id:261956)也是 $A \cup B$ 的[子集](@entry_id:261956)，同理 $B$ 的任何[子集](@entry_id:261956)也是 $A \cup B$ 的[子集](@entry_id:261956)。
为了说明等式为何不成立，我们只需给出一个简单的反例 [@problem_id:1823706]。令 $A=\{a\}$，$B=\{b\}$，其中 $a \neq b$。
-   $A \cup B = \{a, b\}$，其幂集为 $\mathcal{P}(A \cup B) = \{\emptyset, \{a\}, \{b\}, \{a, b\}\}$。
-   $\mathcal{P}(A) = \{\emptyset, \{a\}\}$，$\mathcal{P}(B) = \{\emptyset, \{b\}\}$。
-   $\mathcal{P}(A) \cup \mathcal{P}(B) = \{\emptyset, \{a\}, \{b\}\}$。
比较两边的结果，集合 $\{a, b\}$ 属于 $\mathcal{P}(A \cup B)$，但不属于 $\mathcal{P}(A) \cup \mathcal{P}(B)$。这个集合包含了来自 $A$ 和 $B$ 的元素，但它既不是 $A$ 的[子集](@entry_id:261956)，也不是 $B$ 的[子集](@entry_id:261956)。

对于**集差** ($\setminus$)，情况更为直接。$\mathcal{P}(A \setminus B) = \mathcal{P}(A) \setminus \mathcal{P}(B)$ 恒不成立。一个简单的反驳理由是 [@problem_id:1823729]，空集 $\emptyset$ 总是 $A \setminus B$ 的[子集](@entry_id:261956)，因此 $\emptyset \in \mathcal{P}(A \setminus B)$。然而，$\mathcal{P}(A) \setminus \mathcal{P}(B)$ 的定义是所有属于 $\mathcal{P}(A)$ 但不属于 $\mathcal{P}(B)$ 的集合。由于[空集](@entry_id:261946)也是 $B$ 的[子集](@entry_id:261956)，所以 $\emptyset \in \mathcal{P}(B)$。因此，$\emptyset$ 永远不会属于 $\mathcal{P}(A) \setminus \mathcal{P}(B)$。

最后，我们来看幂集与**笛卡尔积** ($\times$) 的基数关系。对于非空[有限集](@entry_id:145527) $A$ 和 $B$，等式 $|\mathcal{P}(A \times B)| = |\mathcal{P}(A)| \cdot |\mathcal{P}(B)|$ 也是不成立的 [@problem_id:1823729]。左边的[基数](@entry_id:754020)是 $2^{|A \times B|} = 2^{|A| \cdot |B|}$，而右边的基数是 $2^{|A|} \cdot 2^{|B|} = 2^{|A|+|B|}$。只有在极特殊情况下（例如 $|A|=|B|=2$），$|A| \cdot |B| = |A|+|B|$ 才会成立，但这远非普遍情况。

### 幂集内的序与结构

[子集](@entry_id:261956)关系 $\subseteq$ 不仅定义了集合间的包含，还在任意集合 $S$ 的幂集 $\mathcal{P}(S)$ 上建立了一个**偏[序关系](@entry_id:138937)** (partial order)。这个序结构是[幂集](@entry_id:137423)最重要的特性之一。

[幂集](@entry_id:137423)运算在这个[序关系](@entry_id:138937)下表现出**单调性** (monotonicity)。
-   $A \subseteq B \implies \mathcal{P}(A) \subseteq \mathcal{P}(B)$。这个命题的证明很简单 [@problem_id:1823728]：任取一个 $X \in \mathcal{P}(A)$，这意味着 $X \subseteq A$。根据[子集](@entry_id:261956)关系的[传递性](@entry_id:141148)，由 $X \subseteq A$ 和 $A \subseteq B$ 可得 $X \subseteq B$。这反过来意味着 $X \in \mathcal{P}(B)$。因此，$\mathcal{P}(A)$ 的所有元素也都在 $\mathcal{P}(B)$ 中。

事实上，这个关系是双向的，构成了一个等价关系 [@problem_id:3052603]：
$$
A \subseteq B \iff \mathcal{P}(A) \subseteq \mathcal{P}(B)
$$
我们已经证明了从左到右的蕴含。对于从右到左的蕴含，假设 $\mathcal{P}(A) \subseteq \mathcal{P}(B)$。我们知道 $A \subseteq A$，所以 $A \in \mathcal{P}(A)$。由于 $\mathcal{P}(A)$ 是 $\mathcal{P}(B)$ 的[子集](@entry_id:261956)，那么 $A$ 也必须是 $\mathcal{P}(B)$ 的一个元素，即 $A \in \mathcal{P}(B)$。根据[幂集](@entry_id:137423)的定义，这恰恰意味着 $A \subseteq B$。

这个[等价关系](@entry_id:138275)可以进一步加强到[真子集](@entry_id:152276)：
$$
A \subsetneq B \iff \mathcal{P}(A) \subsetneq \mathcal{P}(B)
$$
这一关系同样来自对双向蕴含的证明 [@problem_id:3052603]。如果 $A \subsetneq B$，我们已知 $\mathcal{P}(A) \subseteq \mathcal{P}(B)$。此外，因为 $A \neq B$，必有元素 $b \in B$ 但 $b \notin A$。因此 $B$ 本身是 $\mathcal{P}(B)$ 的元素，但不是 $\mathcal{P}(A)$ 的元素，故 $\mathcal{P}(A) \neq \mathcal{P}(B)$。反之，如果 $\mathcal{P}(A) \subsetneq \mathcal{P}(B)$，我们已知 $A \subseteq B$。如果假设 $A=B$，则 $\mathcal{P}(A)=\mathcal{P}(B)$，与前提矛盾，故必有 $A \neq B$。

这个偏序结构 $(\mathcal{P}(S), \subseteq)$ 实际上是一个**完备格** (complete lattice) [@problem_id:1823720]。对于 $\mathcal{P}(S)$ 的任何[子集](@entry_id:261956)族（即[子集](@entry_id:261956)的集合） $\mathcal{C} \subseteq \mathcal{P}(S)$，其**上确界** (supremum) 或称**并** (join) 由其中所有集合的并集 $\bigcup_{X \in \mathcal{C}} X$ 给出，而其**[下确界](@entry_id:140118)** (infimum) 或称**交** (meet) 由其中所有集合的交集 $\bigcap_{X \in \mathcal{C}} X$ 给出。由于任意数量集合的并集和交集仍然是定义明确的集合，这个格是完备的。在这个格中，[空集](@entry_id:261946) $\emptyset$ 是[最小元](@entry_id:265018)（底），而[全集](@entry_id:264200) $S$ 是[最大元](@entry_id:276547)（顶）。

这种结构性的观点非常强大。例如，我们可以利用它来构建和理解更复杂的集合。在Z[F理论](@entry_id:184208)中，我们可以从一个已有的集合（如 $\mathcal{P}(A)$）中分离出满足特定性质的元素，形成一个新的集合。这由**[分离公理](@entry_id:154482)模式** (Axiom Schema of Separation) 保证。一个例子是，给定集合 $A$ 和其上的一个[二元关系](@entry_id:270321) $R$，我们可以定义一个由所有 $R$-闭合子集构成的集合 $B$ [@problem_id:3052609]：
$$
B = \{ X \in \mathcal{P}(A) : \forall x \in X, \forall y \in A, (\langle x,y \rangle \in R \rightarrow y \in X) \}
$$
[分离公理](@entry_id:154482)确保了 $B$ 是一个合法的、存在的集合，因为它是从已存在的集合 $\mathcal{P}(A)$ 中通过一个明确的一阶逻辑公式筛选出来的。

最后，[幂集](@entry_id:137423)的结构之美在其代数对称性中得到了深刻体现。[幂集](@entry_id:137423) $\mathcal{P}(X)$ 与并、交、补运算一起构成了一个**[布尔代数](@entry_id:168482)** (Boolean algebra)。一个有趣的问题是，这个[代数结构](@entry_id:137052)上有多少种自同构？一个**布尔代数[自同构](@entry_id:155390)** $\varphi: \mathcal{P}(X) \to \mathcal{P}(X)$ 是一个保持所有布尔运算（并、交、补）的双射。如果我们增加一个看似自然的条件，即该[自同构](@entry_id:155390)将单元素集映射到单元素集，那么可以证明，这种自同构的数量恰好是 $n!$，其中 $n=|X|$ [@problem_id:3052611]。

其原因在于，任何一个[子集](@entry_id:261956) $A \subseteq X$ 都可以表示为其单元素[子集](@entry_id:261956)的并集。由于自同构 $\varphi$ 保持并集运算，因此 $\varphi$ 的行为完全由它对所有单元素集 $\{\{x\} : x \in X\}$ 的作用所决定。条件规定 $\varphi(\{x\})$ 必须是某个单元素集 $\{y\}$。这定义了一个函数 $f: X \to X$，使得 $\varphi(\{x\}) = \{f(x)\}$。由于 $\varphi$ 还必须保持交集运算（特别是，不相交的[集合的像](@entry_id:140317)也必须不相交），可以推断出函数 $f$ 必须是[单射](@entry_id:183792)的。对于有限集 $X$，任何从 $X$到自身的单射也是满射，因此 $f$ 必须是 $X$ 上的一个**[置换](@entry_id:136432)** (permutation)。反之，任何 $X$ 上的[置换](@entry_id:136432) $f$ 都能诱导一个满足条件的[布尔代数](@entry_id:168482)[自同构](@entry_id:155390)。因此，这类自同构与 $X$ 上的[置换](@entry_id:136432)[一一对应](@entry_id:143935)，其总数就是 $n!$。这一结果揭示了幂集的[代数结构](@entry_id:137052)与底层集合的对称性之间的深刻联系。