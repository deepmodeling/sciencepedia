## 引言
在拓扑学的世界里，[分离公理](@entry_id:154482)是用于区分和理解不同空间结构的核心工具。从$T_1$到$T_4$（[正规空间](@entry_id:152381)），我们逐步增强了[分离点](@entry_id:265082)与集合的能力。然而，[正规空间](@entry_id:152381)仅能保证分离不相交的**[闭集](@entry_id:136446)**，这在处理更一般的拓扑问题时暴露了其局限性。当两个集合互不相交但彼此“紧贴”时，我们如何才能精确地描述和分离它们？这正是本篇文章旨在解决的知识缺口。本文将引入一个更强大的分离性质——完全正规性（$T_5$空间），它为分析复杂的拓扑结构提供了更精细的工具。

通过接下来的三个章节，你将踏上一段深入的探索之旅。在“原理与机制”一章中，我们将从“[分离集](@entry_id:152848)”的概念出发，严格定义[完全正规空间](@entry_id:155337)，并证明其与“遗传正规性”的深刻[等价关系](@entry_id:138275)。接着，在“应用与跨学科联系”一章中，我们将考察这一性质在[度量空间](@entry_id:138860)、线性序空间等重要数学对象中的自然体现，并探讨其在拓扑乘积和[商空间](@entry_id:274314)等构造下的行为，揭示其优势与局限。最后，“动手实践”部分将通过一系列精心设计的问题，帮助你将理论知识应用于具体情境，巩固对[完全正规空间](@entry_id:155337)这一核心概念的理解。

## 原理与机制

在本章中，我们将深入探讨拓扑学中一个重要且精妙的分离性质——完全正规性。此前的章节已经介绍了[正规空间](@entry_id:152381)（$T_4$ 空间）的概念，即任意两个不相交的[闭集](@entry_id:136446)都可以被不相交的开集分离。然而，拓扑学家们很快发现，在处理不一定是[闭集](@entry_id:136446)的[子集](@entry_id:261956)时，需要一个更具[一般性](@entry_id:161765)的分离概念。完全正规性正是为了满足这一需求而引入的，它为我们提供了一个更强大的工具来分析和分类[拓扑空间](@entry_id:155056)。

### 从不相交到分离：拓展分离概念

我们首先回顾，一个拓扑空间被称为**正规的 (normal)**，如果对于任意两个不相交的[闭集](@entry_id:136446) $A$ 和 $B$（即 $A \cap B = \emptyset$），都存在不相交的开集 $U$ 和 $V$ 使得 $A \subseteq U$ 且 $B \subseteq V$。这个定义的核心在于集合 $A$ 和 $B$ 必须是**[闭集](@entry_id:136446)**。但在许多拓扑分析的情境中，我们感兴趣的集合未必是[闭集](@entry_id:136446)。这启发我们思考：对于两个不相交但非闭的集合，我们如何刻画它们“彼此不接触”的程度？

仅仅要求 $A \cap B = \emptyset$ 是不够的。例如，在实数空间 $\mathbb{R}$（赋予[标准拓扑](@entry_id:152252)）中，考虑开区间 $A = (0, 1)$ 和单点集 $B = \{1\}$。它们显然不相交。然而，$1$ 这个点虽然不属于 $A$，但它是 $A$ 的一个聚点（limit point）。换言之，$B$ 中的点“紧贴”着 $A$。从拓扑的角度看，它们并非真正意义上的“分离”。

为了精确捕捉这种“互不接触”的直观想法，我们引入了**[分离集](@entry_id:152848) (separated sets)** 的概念。

**定义 ([分离集](@entry_id:152848)):** 在一个拓扑空间 $X$ 中，如果两个[子集](@entry_id:261956) $A$ 和 $B$ 满足条件 $\overline{A} \cap B = \emptyset$ 且 $A \cap \overline{B} = \emptyset$，那么我们称 $A$ 和 $B$ 是**分离的**。

这个定义蕴含着双重约束：首先，$B$ 中的任意一点都不能是 $A$ 的聚点（或属于 $A$）；其次，$A$ 中的任意一点也不能是 $B$ 的[聚点](@entry_id:177089)（或属于 $B$）。值得注意的是，任意两个不相交的[闭集](@entry_id:136446) $F_1, F_2$ 都是分离的，因为 $\overline{F_1} = F_1$ 且 $\overline{F_2} = F_2$，所以 $\overline{F_1} \cap F_2 = F_1 \cap F_2 = \emptyset$ 且 $F_1 \cap \overline{F_2} = F_1 \cap F_2 = \emptyset$。因此，“分离”是“[不相交闭集](@entry_id:152178)”概念的自然推广。

然而，仅仅不相交的两个集合远非都是分离的。考察一些例子可以加深理解 [@problem_id:1539891]。在 $\mathbb{R}$ 中：
- 令 $A = \{1\}$，$B = (1, 2)$。它们不相交。我们有 $\overline{A} = \{1\}$，所以 $\overline{A} \cap B = \{1\} \cap (1, 2) = \emptyset$。但是，$\overline{B} = [1, 2]$，所以 $A \cap \overline{B} = \{1\} \cap [1, 2] = \{1\} \neq \emptyset$。因此，$A$ 和 $B$ 不是分离的。
- 令 $A = \{0\}$，$B = \{\frac{1}{n} \mid n \in \mathbb{Z}, n > 0\}$。它们不相交。$\overline{A} = \{0\}$，因此 $\overline{A} \cap B = \emptyset$。然而，$B$ 的[聚点](@entry_id:177089)集合包含 $0$，所以 $\overline{B} = B \cup \{0\}$。这样一来，$A \cap \overline{B} = \{0\} \cap (B \cup \{0\}) = \{0\} \neq \emptyset$。因此，$A$ 和 $B$ 也不是分离的。

一个更具启发性的例子来自二维欧几里得空间 $\mathbb{R}^2$ [@problem_id:1539879]。考虑两个集合：
$$S_1 = \{(x, y) \in \mathbb{R}^2 \mid y=0 \text{ and } x \leq 0\}$$
$$S_2 = \{(x, y) \in \mathbb{R}^2 \mid y = \sin(1/x) \text{ and } x > 0\}$$
$S_1$ 是非正x轴，$S_2$ 是著名的“[拓扑学家的正弦曲线](@entry_id:142923)”的一部分。$S_1$ 和 $S_2$ 显然不相交。由于 $S_1$ 是[闭集](@entry_id:136446)，我们有 $\overline{S_1} = S_1$，因此 $\overline{S_1} \cap S_2 = \emptyset$。然而，当 $x$ 从正方向趋近于 $0$ 时，$1/x$ 趋向于 $+\infty$，使得 $\sin(1/x)$ 在 $[-1, 1]$ 之间无限[振荡](@entry_id:267781)。这导致 $S_2$ 的[闭包](@entry_id:148169) $\overline{S_2}$ 不仅包含 $S_2$ 自身，还包含了线段 $\{(0, y) \mid -1 \leq y \leq 1\}$。因此，$S_1 \cap \overline{S_2}$ 包含了原点 $(0,0)$，故非空。所以，$S_1$ 和 $S_2$ 尽管不相交，但并不是分离的。

### [完全正规空间](@entry_id:155337)：定义与定位

有了[分离集](@entry_id:152848)的概念，我们就可以定义一类比[正规空间](@entry_id:152381)更强的[拓扑空间](@entry_id:155056)。

**定义 ([完全正规空间](@entry_id:155337)):** 一个[拓扑空间](@entry_id:155056) $X$ 被称为**完全正规的 (completely normal)**，如果对于 $X$ 中的任意两个[分离集](@entry_id:152848) $A$ 和 $B$，都存在不相交的开集 $U$ 和 $V$ 使得 $A \subseteq U$ 且 $B \subseteq V$。[@problem_id:1663441]

一个**$T_5$ 空间**被定义为一个完全正规的 $T_1$ 空间。

这个定义清楚地表明，完全正规性是对正规性的强化。正规性要求分离不相交的**[闭集](@entry_id:136446)**，而完全正规性要求分离**[分离集](@entry_id:152848)**。正如我们所见，任何一对不相交的[闭集](@entry_id:136446)都是分离的，所以如果一个空间是完全正规的，它必然是正规的。

这一事实帮助我们将[完全正规空间](@entry_id:155337)置于[分离公理](@entry_id:154482)的层级体系中。回忆一下，$T_i$ 公理之间存在蕴含关系。对于一个 $T_1$ 空间：
1.  **$T_5 \implies T_4$**: 如上所述，一个完全正规的 $T_1$ 空间（$T_5$）必然是正规的 $T_1$ 空间（$T_4$），因为不相交的[闭集](@entry_id:136446)是[分离集](@entry_id:152848)的一种特殊情况。
2.  **$T_4 \implies T_3$**: 任何 $T_4$ 空间都是 $T_3$ 空间（即正则的 $T_1$ 空间）。要证明这一点，考虑 $X$ 中任意[闭集](@entry_id:136446) $F$ 和不属于 $F$ 的点 $x$。由于 $X$ 是 $T_1$ 空间，单点集 $\{x\}$ 是[闭集](@entry_id:136446)。现在我们有两个不相交的[闭集](@entry_id:136446) $\{x\}$ 和 $F$。根据 $X$ 的正规性，存在不相交的开集 $U$ 和 $V$ 使得 $x \in U$ 且 $F \subseteq V$。这正是正则性的定义。[@problem_id:1539920]
3.  **$T_3 \implies T_2$**: 任何 $T_3$ 空间都是 $T_2$ 空间（Hausdorff 空间）。证明过程类似，考虑任意两个不同的点 $x, y$。由于空间是 $T_1$ 的，$\{y\}$ 是[闭集](@entry_id:136446)且 $x \notin \{y\}$。根据正则性，存在不相交的开集 $U, V$ 分别包含 $x$ 和 $\{y\}$。这满足了 Hausdorff 条件。[@problem_id:1539899]

综上所述，我们得到了[分离公理](@entry_id:154482)的一个重要链条：
$$T_5 \implies T_4 \implies T_3 \implies T_2 \implies T_1$$
因此，一个完全正规的 $T_1$ 空间（$T_5$）自动满足所有较低阶的 $T_i$ [分离公理](@entry_id:154482)，它既是正规的，也是正则的，还是 Hausdorff 空间。

### 核心等价关系：完全正规性与遗传正规性

拓扑性质的一个重要方面是它们是否能被[子空间](@entry_id:150286)继承。如果一个空间 $X$ 所具有的某种性质 $P$，对于 $X$ 的[任意子](@entry_id:143753)空间 $Y$（赋予[子空间拓扑](@entry_id:147159)）都成立，那么性质 $P$ 被称为**[遗传性质](@entry_id:151340) (hereditary property)**。例如，$T_1$ 和 $T_2$ (Hausdorff) 性质都是遗传的。然而，正规性（$T_4$）却是一个著名的非[遗传性质](@entry_id:151340)。存在一些[正规空间](@entry_id:152381)，其某些[子空间](@entry_id:150286)并非正规的。

这就引出了一个自然的问题：哪些空间的**所有**[子空间](@entry_id:150286)都是正规的？这样的空间被称为**[遗传正规空间](@entry_id:149845) (hereditarily normal space)**。令人惊讶的是，这个性质与我们刚刚定义的完全正规性紧密相连。事实上，它们是等价的。

**定理:** 一个[拓扑空间](@entry_id:155056) $X$ 是完全正规的，当且仅当它是遗传正规的。[@problem_id:1539904]

**证明:**

($\Rightarrow$) **完全正规 $\implies$ 遗传正规**

假设 $X$ 是一个[完全正规空间](@entry_id:155337)。我们需要证明它的[任意子](@entry_id:143753)空间 $Y \subseteq X$ 都是正规的。令 $C$ 和 $D$ 是 $Y$ 中任意两个不相交的[闭集](@entry_id:136446)。根据[子空间拓扑](@entry_id:147159)中[闭集](@entry_id:136446)的定义，存在 $X$ 中的[闭集](@entry_id:136446) $C_X$ 和 $D_X$ 使得 $C = Y \cap C_X$ 且 $D = Y \cap D_X$。更重要的是，在[子空间拓扑](@entry_id:147159)中，$C$ 和 $D$ 的[闭包](@entry_id:148169)就是它们自身，即 $\text{cl}_Y(C) = C$ 和 $\text{cl}_Y(D) = D$。

现在，我们来验证 $C$ 和 $D$ 作为 $X$ 的[子集](@entry_id:261956)是分离的。
$$ \text{cl}_X(C) \cap D = (\text{cl}_X(C) \cap Y) \cap D = \text{cl}_Y(C) \cap D = C \cap D = \emptyset $$
同理可得 $C \cap \text{cl}_X(D) = \emptyset$。因此，$C$ 和 $D$ 在 $X$ 中是分离的。

由于 $X$ 是完全正规的，存在 $X$ 中不相交的开集 $U$ 和 $V$ 使得 $C \subseteq U$ 且 $D \subseteq V$。令 $U_Y = U \cap Y$ 且 $V_Y = V \cap Y$。$U_Y$ 和 $V_Y$ 是 $Y$ 中的开集，它们不相交，并且分别包含 $C$ 和 $D$。这证明了 $Y$ 是一个[正规空间](@entry_id:152381)。因为 $Y$ 是任意子空间，所以 $X$ 是遗传正规的。

($\Leftarrow$) **遗传正规 $\implies$ 完全正规**

假设 $X$ 是一个[遗传正规空间](@entry_id:149845)。我们需要证明对于 $X$ 中任意两个[分离集](@entry_id:152848) $A$ 和 $B$，存在不相交的开集可以将它们分离。

令 $A, B$ 是 $X$ 中分离的两个集合，即 $\overline{A} \cap B = \emptyset$ 且 $A \cap \overline{B} = \emptyset$。这里的[闭包](@entry_id:148169) $\overline{A}$ 和 $\overline{B}$ 是在 $X$ 中计算的。注意 $\overline{A}$ 和 $\overline{B}$ 可能相交。考虑[子空间](@entry_id:150286) $Y = X \setminus (\overline{A} \cap \overline{B})$。由于 $X$ 是遗传正规的，$Y$ 是一个[正规空间](@entry_id:152381)。

现在我们在[子空间](@entry_id:150286) $Y$ 中考察集合 $\overline{A} \cap Y$ 和 $\overline{B} \cap Y$。它们是 $Y$ 中的[闭集](@entry_id:136446)（因为它们是 $X$ 中的[闭集](@entry_id:136446)与 $Y$ 的交集）。同时，它们在 $Y$ 中不相交：
$$ (\overline{A} \cap Y) \cap (\overline{B} \cap Y) = \overline{A} \cap \overline{B} \cap Y = \overline{A} \cap \overline{B} \cap (X \setminus (\overline{A} \cap \overline{B})) = \emptyset $$
由于 $Y$ 是正规的，存在 $Y$ 中不相交的开集 $U'$ 和 $V'$ 使得 $\overline{A} \cap Y \subseteq U'$ 和 $\overline{B} \cap Y \subseteq V'$。

因为 $A \subseteq \overline{A}$ 且 $A \cap \overline{B} = \emptyset$，我们有 $A \subseteq \overline{A} \setminus \overline{B} \subseteq X \setminus \overline{B}$。特别地，$A$ 中没有点属于 $\overline{A} \cap \overline{B}$，所以 $A \subseteq Y$。因此 $A \subseteq \overline{A} \cap Y \subseteq U'$。同理，$B \subseteq V'$。

根据[子空间拓扑](@entry_id:147159)的定义，$U' = U \cap Y$，$V' = V \cap Y$，其中 $U, V$ 是 $X$ 中的开集。现在我们构造 $X$ 中的所需开集。令：
$$ U_0 = U \setminus \overline{B} \quad \text{and} \quad V_0 = V \setminus \overline{A} $$
这两个集合都是 $X$ 中的开集（一个开集减去一个[闭集](@entry_id:136446)）。我们已经知道 $A \subseteq U$ 且 $A \cap \overline{B} = \emptyset$，所以 $A \subseteq U \setminus \overline{B} = U_0$。同理 $B \subseteq V_0$。

最后，验证 $U_0$ 和 $V_0$ 是否不相交：
$$ U_0 \cap V_0 = (U \setminus \overline{B}) \cap (V \setminus \overline{A}) = (U \cap V) \setminus (\overline{A} \cup \overline{B}) $$
由于 $U'$ 和 $V'$ 在 $Y$ 中不相交，所以 $U \cap V \cap Y = \emptyset$。这意味着 $U \cap V \subseteq X \setminus Y = \overline{A} \cap \overline{B}$。因此：
$$ U_0 \cap V_0 \subseteq (\overline{A} \cap \overline{B}) \setminus (\overline{A} \cup \overline{B}) = \emptyset $$
我们成功找到了 $X$ 中不相交的开集 $U_0, V_0$ 分离了 $A$ 和 $B$。所以 $X$ 是完全正规的。 $\blacksquare$

这个深刻的[等价关系](@entry_id:138275)是理解[完全正规空间](@entry_id:155337)的关键。它直接导出一个重要推论：

**推论:** 完全正规性是一个[遗传性质](@entry_id:151340)。[@problem_id:1539921]
**证明:** [假设空间](@entry_id:635539) $X$ 是完全正规的，那么根据上述定理，它也是遗传正规的。这意味着 $X$ 的所有[子空间](@entry_id:150286)都是正规的。现在考虑 $X$ 的任意子空间 $Y$。我们需要证明 $Y$ 也是完全正规的。根据定理，这等价于证明 $Y$ 是遗传正规的，即 $Y$ 的所有[子空间](@entry_id:150286) $Z \subseteq Y$ 都是正规的。但由于 $Z$ 也是 $X$ 的一个[子空间](@entry_id:150286)，而 $X$ 是遗传正规的，所以 $Z$ 必然是正规的。因此，$Y$ 是遗传正规的，从而也是完全正规的。

### 深度性质与等价刻画

与[正规空间](@entry_id:152381)拥有[Urysohn引理](@entry_id:150431)和[Tietze扩张定理](@entry_id:151716)等强大的函数分离工具类似，[完全正规空间](@entry_id:155337)也具有类似的深刻性质，这些性质通常通过构造[连续函数](@entry_id:137361)来体现。

**Urysohn型引理 (适用于[完全正规空间](@entry_id:155337)):** 一个 $T_1$ 空间 $X$ 是完全正规的，当且仅当对于任意两个[分离集](@entry_id:152848) $A$ 和 $B$，都存在一个[连续函数](@entry_id:137361) $f: X \to [0, 1]$ 使得对于所有 $x \in A$，有 $f(x)=0$；对于所有 $y \in B$，有 $f(y)=1$。[@problem_id:1539902]

这个定理为我们分析[完全正规空间](@entry_id:155337)提供了强大的分析工具。我们可以利用它来证明一些更强的分离性质。

#### 更强的分离性质

在[正规空间](@entry_id:152381)中，我们可以将任意两个不相交的[闭集](@entry_id:136446)用不相交的开集分离。在[完全正规空间](@entry_id:155337)中，我们不仅可以分离[分离集](@entry_id:152848)，还能保证这些[开邻域](@entry_id:268496)的[闭包](@entry_id:148169)也是不相交的。

**定理:** 在一个[完全正规空间](@entry_id:155337) $X$ 中，对于任意两个[分离集](@entry_id:152848) $A$ 和 $B$，都存在不相交的开集 $U, V$ 使得 $A \subseteq U$, $B \subseteq V$ 且 $\overline{U} \cap \overline{V} = \emptyset$。[@problem_id:1539889]

**证明:** 设 $A, B$ 是 $X$ 中的[分离集](@entry_id:152848)。由于 $X$ 是完全正规的，根据上述Urysohn型引理，存在一个[连续函数](@entry_id:137361) $f: X \to [0, 1]$ 使得 $f(A) = \{0\}$ 且 $f(B) = \{1\}$。现在考虑区间 $[0, 1]$ 中的两个不相交的开集 $[0, 1/3)$ 和 $(2/3, 1]$。令：
$$ U = f^{-1}([0, 1/3)) \quad \text{and} \quad V = f^{-1}((2/3, 1]) $$
由于 $f$ 连续，$[0, 1/3)$ 和 $(2/3, 1]$ 是 $[0,1]$ 中的开集（在[子空间拓扑](@entry_id:147159)中），它们的[逆像](@entry_id:154161) $U$ 和 $V$ 是 $X$ 中的开集。它们显然是不相交的，并且 $A \subseteq U, B \subseteq V$。

现在考虑它们的闭包。根据[连续函数](@entry_id:137361)的基本性质，我们知道 $\overline{f^{-1}(S)} \subseteq f^{-1}(\overline{S})$。因此：
$$ \overline{U} = \overline{f^{-1}([0, 1/3))} \subseteq f^{-1}(\overline{[0, 1/3)}) = f^{-1}([0, 1/3]) $$
$$ \overline{V} = \overline{f^{-1}((2/3, 1])} \subseteq f^{-1}(\overline{(2/3, 1]}) = f^{-1}([2/3, 1]) $$
由于 $[0, 1/3]$ 和 $[2/3, 1]$ 这两个[闭区间](@entry_id:136474)不相交，它们的[逆像](@entry_id:154161) $f^{-1}([0, 1/3])$ 和 $f^{-1}([2/3, 1])$ 也不相交。因此，$\overline{U} \cap \overline{V} = \emptyset$。 $\blacksquare$

#### 分离多个集合

函数分离工具的威力还体现在处理多个集合的情况。例如，如果我们有三个**两两分离**的集合 $A_1, A_2, A_3$，我们能否构造一个[连续函数](@entry_id:137361)将它们映射到不同的值？答案是肯定的。[@problem_id:1539902]

假设 $A_1, A_2, A_3$ 是 $X$ 中两两分离的非空[子集](@entry_id:261956)。我们可以构造一个[连续函数](@entry_id:137361) $h: X \to [0, 1]$ 使得 $h(A_1) = \{0\}$, $h(A_2) = \{1/2\}$, $h(A_3) = \{1\}$。

构造过程如下：
1.  首先，证明集合 $A_1$ 与 $A_2 \cup A_3$ 是分离的。
    -   $\overline{A_1} \cap (A_2 \cup A_3) = (\overline{A_1} \cap A_2) \cup (\overline{A_1} \cap A_3) = \emptyset \cup \emptyset = \emptyset$ (因为 $A_1, A_2$ 分离且 $A_1, A_3$ 分离)。
    -   $A_1 \cap \overline{A_2 \cup A_3} = A_1 \cap (\overline{A_2} \cup \overline{A_3}) = (A_1 \cap \overline{A_2}) \cup (A_1 \cap \overline{A_3}) = \emptyset \cup \emptyset = \emptyset$。
    因此，存在[连续函数](@entry_id:137361) $f_1: X \to [0, 1]$ 使得 $f_1(A_1)=\{0\}$ 且 $f_1(A_2 \cup A_3)=\{1\}$。
2.  同理，可以证明集合 $A_3$ 与 $A_1 \cup A_2$ 是分离的。因此存在[连续函数](@entry_id:137361) $f_3: X \to [0, 1]$ 使得 $f_3(A_3)=\{1\}$ 且 $f_3(A_1 \cup A_2)=\{0\}$。
3.  现在定义函数 $h(x) = \frac{f_1(x) + f_3(x)}{2}$。由于 $f_1, f_3$ 连续， $h$ 也连续。我们来检查它在 $A_1, A_2, A_3$ 上的取值：
    -   对于 $x \in A_1$，$h(x) = \frac{0 + 0}{2} = 0$。
    -   对于 $x \in A_2$，$h(x) = \frac{1 + 0}{2} = 1/2$。
    -   对于 $x \in A_3$，$h(x) = \frac{1 + 1}{2} = 1$。
    这样就成功构造了所需的函数 $h$。

这个巧妙的构造进一步揭示了完全正规性与连通性之间的有趣联系。如果一个空间 $X$ 是**连通的**，那么它不能被分解为两个不相交的非空开集之并。[连续函数](@entry_id:137361)的一个基本性质是它将[连通集](@entry_id:136460)映射到[连通集](@entry_id:136460)。在上面的例子中，如果 $X$ 是连通的，并且 $X = A_1 \cup A_2 \cup A_3$，那么 $h(X) = h(A_1 \cup A_2 \cup A_3) = \{0, 1/2, 1\}$。但是 $\{0, 1/2, 1\}$ 是一个[离散集](@entry_id:146023)，因此是不连通的。这与 $h(X)$ 必须是连通的（作为[连通空间](@entry_id:156017) $X$ 的连续像）事实相矛盾。因此，我们得到一个结论：如果一个[完全正规空间](@entry_id:155337) $X$ 是连通的，那么它不可能是三个两两分离的非[空集](@entry_id:261946)合的并。换句话说，$X \setminus (A_1 \cup A_2 \cup A_3)$ 必须非空。

总之，完全正规性不仅通过其与遗传正规性的等价关系统一了拓扑学中的一个重要概念，还通过强大的函数分离性质，为我们分析和理解[拓扑空间](@entry_id:155056)的[精细结构](@entry_id:140861)提供了有力的工具。