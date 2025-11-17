## 引言
在[测度论](@entry_id:139744)的宏伟框架中，仅仅定义集合的“大小”是远远不够的；我们还需要一套理论来处理定义在这些集合上的函数。并非所有函数都能与底层的测度结构和谐共存，[黎曼积分](@entry_id:142508)在处理[不连续函数](@entry_id:143848)时也暴露出其局限性。为了建立一个更强大、更普适的积分理论——[勒贝格积分](@entry_id:140189)，我们必须首先回答一个基本问题：哪些函数是“足够好”的，可以被积分？**可测函数 (measurable functions)** 正是这一问题的答案。

本文旨在系统性地介绍可测函数这一[数学分析](@entry_id:139664)中的核心概念。我们将从其基本定义出发，逐步揭示其深刻的内涵与广泛的应用。通过学习本文，读者将能够：
*   在 **“原则与机理”** 一章中，掌握可测函数的正式定义、等价条件以及在代数运算、复合和极限下的重要性质。本章将重点介绍如何通过简单函数来构造和逼近更复杂的可测函数，为理解[勒贝格积分](@entry_id:140189)奠定基础。
*   在 **“应用与跨学科联系”** 一章中，探索可测函数如何作为一种通用语言，在概率论（定义[随机变量](@entry_id:195330)）、泛函分析（构建 $L^p$ 空间）和动力系统等多个数学分支中发挥关键作用。
*   在 **“动手实践”** 一章中，通过一系列精心设计的问题，将理论知识应用于具体计算和证明中，从而加深对可测函数概念的理解。

这趟旅程将带领我们从抽象的定义走向具体的应用，展示可测函数如何成为连接测度、积分与现代数学诸多领域的关键桥梁。让我们首先深入其核心，探究可测函数的原则与机理。

## 原则与机理

在上一章中，我们已经建立了 Lebesgue 测度和 $\sigma$-代数的基本框架。现在，我们将注意力转向定义在这些[可测空间](@entry_id:189701)上的函数。并非所有函数都与底层的测度结构良好地“兼容”。**可测函数 (measurable functions)** 构成了一个至关重要的函数类别，它们足够广泛，包含了分析学中遇到的大多数函数，同时又具有足够强的结构性质，使得我们能够在其上建立一个强大的积分理论，即 Lebesgue 积分。本章旨在系统地阐述可测函数的定义、核心性质及其构造机理。

### 可测函数的定义

我们如何从数学上刻画一个函数与测度结构的“兼容性”？其核心思想在于，函数值的性质应该能够转化为定义域中集合的性质。具体而言，我们要求，对于函[数值域](@entry_id:752817)中的任何“简单”集合，其在定义域中的原像（preimage）都必须是可测的。

设 $(X, \mathcal{M})$ 是一个[可测空间](@entry_id:189701)，其中 $X$ 是一个集合，$\mathcal{M}$ 是 $X$ 上的一个 $\sigma$-代数。一个函数 $f: X \to \mathbb{R}$ 被称为 **($\mathcal{M}$-)可测的 (measurable)**，如果对于任意实数 $\alpha \in \mathbb{R}$，集合 $\{x \in X \mid f(x) > \alpha\}$ 都是 $\mathcal{M}$ 中的一个元素。也就是说，
$$
\{x \in X \mid f(x) > \alpha\} \in \mathcal{M} \quad \forall \alpha \in \mathbb{R}
$$

这个定义虽然简洁，但其选择（为何是[开区间](@entry_id:157577) $(\alpha, \infty)$？）似乎有些武断。幸运的是，一系列等价的定义表明，这种选择是稳健的，并且可以灵活替换。

**定理1 ([可测性](@entry_id:199191)的等价条件)** 设 $f: X \to \mathbb{R}$ 是一个函数。以下陈述是等价的：
1. 对任意 $\alpha \in \mathbb{R}$，$\{x \mid f(x) > \alpha\} \in \mathcal{M}$ (定义)。
2. 对任意 $\alpha \in \mathbb{R}$，$\{x \mid f(x) \ge \alpha\} \in \mathcal{M}$。
3. 对任意 $\alpha \in \mathbb{R}$，$\{x \mid f(x)  \alpha\} \in \mathcal{M}$。
4. 对任意 $\alpha \in \mathbb{R}$，$\{x \mid f(x) \le \alpha\} \in \mathcal{M}$。

这些等价性源于 $\sigma$-代数对[补集](@entry_id:161099)和可数交并运算的封闭性。例如，从条件 (1) 到 (4) 的推导非常直接：
$$
\{x \mid f(x) \le \alpha\} = X \setminus \{x \mid f(x)  \alpha\}
$$
由于 $\mathcal{M}$ 对补集运算是封闭的，如果 $\{x \mid f(x)  \alpha\} \in \mathcal{M}$，那么它的补集也必然在 $\mathcal{M}$ 中。反之亦然。

从严格不等号到非严格不等号的转换则巧妙地利用了可数运算。例如，我们可以将集合 $\{f \ge \alpha\}$ 表示为一列集合的可数交集：
$$
\{x \mid f(x) \ge \alpha\} = \bigcap_{n=1}^{\infty} \left\{x \mid f(x)  \alpha - \frac{1}{n}\right\}
$$
如果对任意 $\beta \in \mathbb{R}$，集合 $\{x \mid f(x)  \beta\}$ 都是可测的，那么上式右边的每个集合都是可测的。由于 $\sigma$-代数对可数交集封闭，所以左边的集合 $\{x \mid f(x) \ge \alpha\}$ 也是可测的。[@problem_id:1869720]

更有趣的是，我们甚至不需要对所有实数 $\alpha$ 进行检验。由于有理数集 $\mathbb{Q}$ 在实数集 $\mathbb{R}$ 中是稠密的，我们只需在所有有理数上检验即可。

**定理2 ([可测性](@entry_id:199191)的有理数判据)** 一个函数 $f: X \to \mathbb{R}$ 是可测的，当且仅当对任意有理数 $q \in \mathbb{Q}$，集合 $\{x \mid f(x)  q\}$ 都是可测的。

证明思路在于，对于任意实数 $\alpha$，我们可以找到一个递减趋向于 $\alpha$ 的有理数序列，或者直接利用稠密性写出：
$$
\{x \mid f(x)  \alpha\} = \bigcup_{q \in \mathbb{Q}, q  \alpha} \{x \mid f(x)  q\}
$$
由于满足 $q  \alpha$ 的有理数 $q$ 是一个可数集合，上式右边是一个可数个[可测集](@entry_id:159173)的并集。由于 $\sigma$-代数对可数并封闭，因此左边的集合也是可测的。这极大地简化了验证一个函数是否可测的理论过程。[@problem_id:1869720]

### 可测函数的经典范例

理论的生命力在于实例。下面我们介绍几类基本的、无处不在的可测函数。

**常数函数 (Constant Functions)**
最简单的非平凡函数莫过于常数函数。设 $f(x) = c_0$ 对所有 $x \in D$ 成立，其中 $D$ 是一个[可测集](@entry_id:159173)。为了检验其可测性，我们考察任意开区间 $I=(a, b)$ 的[原像](@entry_id:150899) $f^{-1}(I)$。
$$
f^{-1}((a,b)) = \{x \in D \mid a  f(x)  b\} = \{x \in D \mid a  c_0  b\}
$$
这个集合的结构非常简单：
*   如果 $c_0$ 位于区间 $(a,b)$ 内，即 $a  c_0  b$，那么原像就是整个定义域 $D$。
*   如果 $c_0$ 不在区间 $(a,b)$ 内，那么原像就是[空集](@entry_id:261946) $\emptyset$。

因为 $D$ 是可测集，[空集](@entry_id:261946) $\emptyset$ 也总是可测集，所以无论何种情况，原像都是可测的。因此，任何[常数函数](@entry_id:152060)都是可测的。[@problem_id:15455]

**特征函数 (Characteristic Functions)**
给定[可测空间](@entry_id:189701) $(X, \mathcal{M})$ 和一个[子集](@entry_id:261956) $A \subseteq X$，集合 $A$ 的**[特征函数](@entry_id:186820) (characteristic function)** $\chi_A$ 定义为：
$$
\chi_A(x) = \begin{cases} 1  \text{if } x \in A \\ 0  \text{if } x \notin A \end{cases}
$$
函数 $\chi_A$ 是否可测？我们根据定义来检验。对于任意 $\alpha \in \mathbb{R}$：
*   如果 $\alpha \ge 1$，则 $\{x \mid \chi_A(x)  \alpha\} = \emptyset$。
*   如果 $0 \le \alpha  1$，则 $\{x \mid \chi_A(x)  \alpha\} = A$。
*   如果 $\alpha  0$，则 $\{x \mid \chi_A(x)  \alpha\} = X$。
在所有情况下，得到的集合 $\emptyset, A, X$ 都需要是可测的。$\emptyset$ 和 $X$ 总是 $\mathcal{M}$ 的成员。因此，$\chi_A$ 是可测函数的充要条件是集合 $A$ 本身是可测的 ($A \in \mathcal{M}$)。[特征函数](@entry_id:186820)是构建更复杂可测函数的基石。

**[单调函数](@entry_id:145115) (Monotonic Functions)**
定义在 $\mathbb{R}$ 上的单调函数（非减或非增）总是 Borel 可测的（即关于 Borel $\sigma$-代数 $\mathcal{B}(\mathbb{R})$ 可测）。这是一个非常重要的结论，因为它涵盖了大量[初等函数](@entry_id:181530)。

以非减函数 $f: \mathbb{R} \to \mathbb{R}$ 为例。我们考察集合 $S = \{x \in \mathbb{R} \mid f(x)  c\}$。可以证明，$S$ 必然是一个区间（或[空集](@entry_id:261946)，或全集 $\mathbb{R}$）。为什么呢？假设 $x_1, x_2 \in S$ 且 $x_1  x_2$。对于任何满足 $x_1  z  x_2$ 的点 $z$，由于 $f$ 非减，我们有 $f(z) \ge f(x_1)$。又因为 $x_1 \in S$，所以 $f(x_1)  c$。因此 $f(z)  c$，这意味着 $z \in S$。这个“中间点”的性质正是区间的定义。一个集合若是 $\mathbb{R}$ 中的区间，它必然是 Borel 集。因此，任何[单调函数](@entry_id:145115)的 Borel [可测性](@entry_id:199191)得证。[@problem_id:1869737]

### [可测函数的性质](@entry_id:198711)与运算

可测函数之所以如此有用，一个关键原因在于它们在常见的函数运算下是封闭的。这意味着由可测函数通过代数运算、复合和极限等方式构造出的新函数，通常也是可测的。

#### 代数运算

如果 $f$ 和 $g$ 是定义在同一[可测空间](@entry_id:189701) $(X, \mathcal{M})$ 上的可测函数， $c$ 是一个常数，那么以下函数也都是可测的：
1.  $c \cdot f$
2.  $f+g$
3.  $f-g$
4.  $f \cdot g$
5.  $f^2$

证明这些性质需要一些技巧。例如，要证明 $f^2$ 是可测的，我们考察 $\{x \mid f(x)^2  \alpha\}$。若 $\alpha  0$，该集合为全集 $X$。若 $\alpha \ge 0$，则
$$
\{x \mid f(x)^2  \alpha\} = \{x \mid f(x)  \sqrt{\alpha}\} \cup \{x \mid f(x)  -\sqrt{\alpha}\}
$$
由于 $f$ 可测，右侧是两个可测集的并集，因此 $f^2$ 也是可测的。[@problem_id:485528]

对于和 $f+g$ 的可测性，其证明利用了有理数的稠密性：
$$
\{x \mid f(x) + g(x)  \alpha\} = \bigcup_{q \in \mathbb{Q}} (\{x \mid f(x)  q\} \cap \{x \mid g(x)  \alpha - q\})
$$
右侧是可数个[可测集](@entry_id:159173)的交集和并集，其结果仍在 $\sigma$-代数内。

一个具体的例子可以加深理解。考虑两个[特征函数](@entry_id:186820) $f(x) = \chi_{[0,a]}(x)$ 和 $g(x) = \chi_{[b,c]}(x)$，其中 $0  b  c  a  1$。它们的差 $h(x) = f(x) - g(x)$ 是可测的。我们来分析集合 $\{x \mid h(x)  0\}$。这等价于 $\{x \mid f(x)=1 \text{ and } g(x)=0\}$。通过分析区间，我们发现这个集合是 $[0, b) \cup (c, a]$，它显然是一个 Lebesgue [可测集](@entry_id:159173)。[@problem_id:485562]

#### [函数复合](@entry_id:144881)

[函数复合](@entry_id:144881)的可测性则更为微妙，它取决于内外函数的性质。

一个非常重要的正面结果是：**[连续函数](@entry_id:137361)与[可测函数的复合](@entry_id:204359)是可测的**。
**定理3** 设 $f: (X, \mathcal{M}) \to \mathbb{R}$ 是一个可测函数， $g: \mathbb{R} \to \mathbb{R}$ 是一个[连续函数](@entry_id:137361)。则[复合函数](@entry_id:147347) $h = g \circ f$ 是可测的。

**证明思路**: 我们需要证明对任意 $\alpha \in \mathbb{R}$，集合 $h^{-1}((\alpha, \infty))$ 是可测的。
$$
h^{-1}((\alpha, \infty)) = (g \circ f)^{-1}((\alpha, \infty)) = f^{-1}(g^{-1}((\alpha, \infty)))
$$
因为 $g$ 是[连续函数](@entry_id:137361)，开集 $(\alpha, \infty)$ 在 $g$ 下的[原像](@entry_id:150899) $g^{-1}((\alpha, \infty))$ 也是 $\mathbb{R}$ 中的一个开集。任何 $\mathbb{R}$ 中的开集都可以表示为一族可数个互不相交的[开区间](@entry_id:157577)的并。设 $g^{-1}((\alpha, \infty)) = \bigcup_{i=1}^\infty I_i$。于是
$$
f^{-1}\left(\bigcup_{i=1}^\infty I_i\right) = \bigcup_{i=1}^\infty f^{-1}(I_i)
$$
由于 $f$ 是可测函数，每个开区间 $I_i$ 的原像 $f^{-1}(I_i)$ 都是可测集。因此，整个原像是一个可数个可测集的并，故其本身也是可测的。[@problem_id:1869766]

然而，调换 $f$ 和 $g$ 的位置，结论就不一定成立了。即**可测函数与[连续函数的复合](@entry_id:139194)不一定是可测的**。构造一个反例需要一些精巧的工具，其中最著名的是利用 Cantor-Lebesgue 函数。

**一个重要的反例** [@problem_id:1869749]:
1.  令 $c(x)$ 为 Cantor-Lebesgue 函数，并构造一个严格递增的[连续函数](@entry_id:137361) $\phi(x) = x + c(x)$。它是一个从 $[0,1]$ 到 $[0,2]$ 的同胚映射。其逆函数 $f = \phi^{-1}$ 也是连续的。
2.  Cantor 集 $C$ 在 $\phi$ 映射下的像 $\phi(C)$ 是一个 Lebesgue 测度为 1 的集合。我们知道，任何正测度集都包含一个非 Lebesgue 可测的[子集](@entry_id:261956) $S$。
3.  令 $g = \chi_A$，其中 $A = \phi^{-1}(S)$。由于 $A \subseteq C$ 且 $C$ 的[测度为零](@entry_id:137864)，所以 $A$ 是一个零测度集，因此 $A$ 是 Lebesgue 可测的。这意味着 $g$ 是一个可测函数。
4.  现在我们考察[复合函数](@entry_id:147347) $g \circ f$。其定义域为 $[0,2]$。
    $$
    (g \circ f)(x) = \chi_A(f(x))
    $$
    这个函数取值为 1 当且仅当 $f(x) \in A$，这等价于 $x \in f^{-1}(A)$。因为 $f^{-1} = \phi$，所以 $f^{-1}(A) = \phi(A) = \phi(\phi^{-1}(S)) = S$。
5.  因此，$g \circ f = \chi_S$。由于我们选择了 $S$ 为非 Lebesgue 可测集，它的[特征函数](@entry_id:186820) $\chi_S$ 不是一个可测函数。

这个例子清晰地表明：$f$ 是连续的，$g$ 是可测的，但它们的复合 $g \circ f$ 却不是可测的。

#### 极限运算

可测函数类最重要的性质之一，就是它在[逐点极限](@entry_id:193549)运算下是封闭的。这与[连续函数](@entry_id:137361)类形成鲜明对比（连续[函数的极限](@entry_id:158708)不一定是连续的）。

**定理4** 设 $\{f_n\}_{n=1}^\infty$ 是一列定义在 $(X, \mathcal{M})$ 上的可测函数。那么以下函数也都是可测的：
*   $\sup_{n} f_n$
*   $\inf_{n} f_n$
*   $\limsup_{n \to \infty} f_n$
*   $\liminf_{n \to \infty} f_n$

**推论**: 如果 $f_n(x) \to f(x)$ 对所有 $x$ 成立，那么极限函数 $f$ 也是可测的。

证明同样依赖于 $\sigma$-代数的性质。例如，对于[上确界](@entry_id:140512)函数：
$$
\{x \mid \sup_{n} f_n(x)  \alpha\} = \bigcup_{n=1}^{\infty} \{x \mid f_n(x)  \alpha\}
$$
右边是可数个可测集的并，所以结果是可测的。对于上极限函数，其表达式稍微复杂一些：
$$
\limsup_{n \to \infty} f_n = \inf_{k \ge 1} \sup_{n \ge k} f_n
$$
利用这个定义和已证的关于 $\sup$ 和 $\inf$ 的结论，通过两步操作即可证明 $\limsup f_n$ 也是可测的。等价地，我们可以直接分析其[水平集](@entry_id:751248) [@problem_id:1869751]：
$$
\left\{x \mid \limsup_{n \to \infty} f_n(x)  \alpha \right\} = \bigcap_{k=1}^{\infty} \bigcup_{n=k}^{\infty} \{x \mid f_n(x)  \alpha\}
$$
这个表达式再次完美地展示了 $\sigma$-代数对可数交并封闭的强大威力。

### 通往积分的桥梁：[简单函数](@entry_id:137521)

在定义 Lebesgue 积[分时](@entry_id:274419)，我们不是直接从任意可测函数开始，而是通过一类结构更简单的函数作为桥梁，这就是**[简单函数](@entry_id:137521) (simple functions)**。

一个函数 $\phi: X \to \mathbb{R}$ 被称为**简单函数**，如果它的值域是一个有限集合，并且对值域中的每个非零值 $a_i$，其原像 $\{x \mid \phi(x) = a_i\}$ 都是[可测集](@entry_id:159173)。任何一个简单函数都可以写成标准形式：
$$
\phi(x) = \sum_{i=1}^{n} a_i \chi_{A_i}(x)
$$
其中 $a_i$ 是 $\phi$ 的不同非零值，$A_i = \{x \mid \phi(x) = a_i\}$ 是互不相交的可测集。

[简单函数](@entry_id:137521)与一般可测函数之间的关系，由以下里程碑式的定理阐明。

**定理5 (可测[函数逼近](@entry_id:141329)定理)** 任何[非负可测函数](@entry_id:192146) $f: X \to [0, \infty]$ 都是一列非负[简单函数](@entry_id:137521) $\{s_n\}$ 单调递增的[逐点极限](@entry_id:193549)。即，存在一列简单函数 $s_n$，使得对任意 $x \in X$：
$$
0 \le s_1(x) \le s_2(x) \le \dots \le f(x), \quad \text{且} \quad \lim_{n \to \infty} s_n(x) = f(x)
$$

这个定理的证明是构造性的，它提供了一种标准的方法来构建这样的逼近序列 $\{s_n\}$ [@problem_id:1869764]。对每个整数 $n \ge 1$：
1.  我们将[函数的值域](@entry_id:161901) $[0, \infty]$ 进行划分。首先关注 $[0, n)$ 区间，将其分割成 $n \cdot 2^n$ 个长度为 $1/2^n$ 的小区间：$[\frac{k-1}{2^n}, \frac{k}{2^n})$，其中 $k=1, 2, \dots, n \cdot 2^n$。
2.  对每个小区间，我们找出其[原像](@entry_id:150899)：$E_{n,k} = \left\{x \in X \mid \frac{k-1}{2^n} \le f(x)  \frac{k}{2^n}\right\}$。
3.  我们还需要处理函数值较大的部分，定义“[溢出](@entry_id:172355)”集合 $F_n = \{x \in X \mid f(x) \ge n\}$。
4.  [简单函数](@entry_id:137521) $s_n$ 在每个[原像](@entry_id:150899)集上被赋予一个常数值，即对应区间范围的下界：
    $$
    s_n(x) = \sum_{k=1}^{n \cdot 2^n} \frac{k-1}{2^n} \chi_{E_{n,k}}(x) + n \chi_{F_n}(x)
    $$

让我们通过一个具体的例子 $f(x) = x^2$ (定义在 $[0, \infty)$ 上) 来理解这个构造过程，并计算 $s_2(x)$ [@problem_id:1869764]。
根据上述方案，当 $n=2$ 时：
*   我们划分的区间范围是 $[0, 2)$，步长是 $1/2^2 = 1/4$。
*   “溢出”集合是 $F_2 = \{x \mid f(x) \ge 2\} = \{x \mid x^2 \ge 2\} = \{x \mid x \ge \sqrt{2}\}$。对于这部分 $x$，$s_2(x) = 2$。
*   对于 $0 \le f(x)  2$ 的部分，即 $0 \le x  \sqrt{2}$，我们有 $\frac{k-1}{4} \le x^2  \frac{k}{4}$。这意味着 $s_2(x) = \frac{k-1}{4}$。从不等式 $k-1 \le 4x^2  k$ 可以看出，$k-1$ 正是 $4x^2$ 的整数部分，即 $k-1 = \lfloor 4x^2 \rfloor$。
*   因此，对于 $0 \le x  \sqrt{2}$，我们有 $s_2(x) = \frac{1}{4}\lfloor 4x^2 \rfloor$。

综上所述，逼近函数 $s_2(x)$ 的表达式为：
$$
s_2(x) = \begin{cases} \frac{1}{4} \lfloor 4x^2 \rfloor  \text{if } 0 \le x  \sqrt{2} \\ 2  \text{if } x \ge \sqrt{2} \end{cases}
$$
这个具体的构造不仅证明了定理的存在性，也为后续定义 Lebesgue 积分奠定了坚实的基础。

### 深入探讨：[Lebesgue可测](@entry_id:192844)与[Borel可测](@entry_id:140719)

到目前为止，我们谈论的“可测”通常是指相对于 Lebesgue $\sigma$-代数 $\mathcal{L}$ 的[可测性](@entry_id:199191)。然而，还存在一个更“精细”的 $\sigma$-代数，即由所有开集生成的 Borel $\sigma$-代数 $\mathcal{B}$。

*   一个函数 $h$ 是 **Borel 可测的**，如果对每个开集 $V$，原像 $h^{-1}(V)$ 都是一个 Borel 集。
*   一个函数 $h$ 是 **Lebesgue 可测的**，如果对每个开集 $V$，[原像](@entry_id:150899) $h^{-1}(V)$ 都是一个 Lebesgue [可测集](@entry_id:159173)。

由于每个 Borel 集都是 Lebesgue [可测集](@entry_id:159173)（即 $\mathcal{B} \subset \mathcal{L}$），所以**任何 Borel 可测函数都必然是 Lebesgue 可测的**。例如，所有[连续函数](@entry_id:137361)和[单调函数](@entry_id:145115)都是 Borel 可测的，因此它们也是 Lebesgue 可测的。

一个自然的问题是：是否存在一个函数，它是 Lebesgue 可测的，但不是 Borel 可测的？答案是肯定的。这揭示了 Lebesgue $\sigma$-代数比 Borel $\sigma$-代数要“大”得多。

构造这样的函数，同样需要借助 Cantor-Lebesgue 函数 $F(x)$。[@problem_id:1869717]
考虑函数 $h(x) = \chi_N(F(x))$，其中 $N \subset [0,1]$ 是一个非 Lebesgue 可测集。

**为什么 $h(x)$ 是 Lebesgue 可测的？**
我们需要考察 $h$ 对开集的[原像](@entry_id:150899)。唯一有趣的情况是 $h^{-1}((1/2, 3/2)) = \{x \mid h(x) = 1\} = \{x \mid F(x) \in N\} = F^{-1}(N)$。一个深刻的结论是：对于 Cantor-Lebesgue 函数 $F$，**任何**集合（即使是[不可测集](@entry_id:161390)）$Y \subset [0,1]$ 的[原像](@entry_id:150899) $F^{-1}(Y)$ 都是 Lebesgue 可测的。这是因为 $F^{-1}(Y)$ 可以被分解为两部分：一部分是它与 Cantor 集 $C$ 的交集，作为零测度集的[子集](@entry_id:261956)，这部分是可测的；另一部分是它与 $C$ 的补集的交集，而 $C$ 的补集是可数个[开区间](@entry_id:157577)的并， $F$ 在每个这样的[开区间](@entry_id:157577)上是常数，因此这部分[原像](@entry_id:150899)也是可数个开区间的并，故也是可测的。

**为什么 $h(x)$ 不是 Borel 可测的？**
如果 $h$ 是 Borel 可测的，那么集合 $F^{-1}(N)$ 就必须是一个 Borel 集。Cantor-Lebesgue 函数 $F$ 将 Cantor 集 $C$ 连续地映满 $[0,1]$。根据[描述集合论](@entry_id:154758)中的一个高级结果（[连续函数](@entry_id:137361)将 Borel 集映为所谓的“[解析集](@entry_id:156221)”，而 $\mathbb{R}$ 中的[解析集](@entry_id:156221)都是 Lebesgue 可测的），如果 $F^{-1}(N)$ 是 Borel 集，那么它在 $F$ 下的像，特别是 $F(F^{-1}(N) \cap C) = N \cap F(C) = N \cap [0,1] = N$，就必须是 Lebesgue 可测的。但这与我们最初的假设——$N$ 是非 Lebesgue [可测集](@entry_id:159173)——相矛盾。因此， $h$ 不可能是 Borel 可测的。

这个例子清楚地划分了这两种可测性，并展示了测度论中一些深刻而迷人的联系。