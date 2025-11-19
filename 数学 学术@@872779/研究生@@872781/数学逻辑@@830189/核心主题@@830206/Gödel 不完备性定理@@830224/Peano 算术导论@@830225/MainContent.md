## 引言
[皮亚诺算术](@entry_id:150593)（Peano Arithmetic, PA）是数理逻辑的基石，它提供了一个严谨的形式框架，旨在公理化我们关于自然数及其运算的直观理解。其意义远超出了基础算术，它不仅是现代数论研究的出发点，更是我们探索计算、证明与逻辑本身界限的强大熔炉。然而，将无限的算术真理封装在一个有限的公理系统内，引出了一个根本性的问题：这样一个[形式系统](@entry_id:634057)能在多大程度上捕捉我们关于数字的全部知识？它的[表达能力](@entry_id:149863)和证明能力的极限又在哪里？

本文旨在系统性地解答这些问题。通过三个循序渐进的章节，读者将踏上一段从基础构建到深刻洞见的逻辑之旅。在“原理与机制”一章中，我们将奠定技术基础，详细介绍 PA 的[形式语言](@entry_id:265110)、九条基本公理以及强大的归纳公理模式，并揭示其如何表示计算过程，同时也会初次窥见其[非标准模型](@entry_id:151939)所暗示的局限性。接下来，“应用与跨学科联系”一章将展示 PA 最深刻的应用——算术化，这一技术使得 PA 能够“谈论”自身的语法和可证性，从而成为推导[哥德尔不完备性定理](@entry_id:153511)的关键工具，并建立起与计算机科学、[证明论](@entry_id:151111)及[模态逻辑](@entry_id:149086)等领域的桥梁。最后，在“动手实践”部分，精心设计的问题将帮助读者巩固对这些抽象概念的理解。通过本次学习，我们将理解为何 PA 既是人类理性构建的辉煌成就，也成为了揭示形式系统内在局限性的不朽例证。

## 原理与机制

本章旨在深入探讨[皮亚诺算术](@entry_id:150593)（Peano Arithmetic, PA）的形式化原理及其内在机制。继绪论之后，我们将不再赘述其历史背景，而是直接进入该理论的技术核心。我们将从其[形式语言](@entry_id:265110)和公理系统开始，进而探索其表达计算的能力，并最终揭示其固有的局限性，即[哥德尔不完备性定理](@entry_id:153511)的深刻体现。

### 算术的语言和标准模型

任何形式理论的构建都始于一种精确定义的语言。对于[皮亚诺算术](@entry_id:150593)，这种语言旨在捕捉关于自然数的基本论述。

#### 形式语言 $L_{PA}$

[皮亚诺算术](@entry_id:150593)的语言，记作 $L_{PA}$，是一种带等词的[一阶语言](@entry_id:151821)。其非逻辑符号集（或称“签名”）由以下部分构成：

*   一个**常数符号**：$0$。其意图是表示数字零。形式上，常数符号可以被视为一个$0$-元函数符号。
*   一个**一元函数符号**：$S$。它代表**后继** (successor) 函数，意图是将一个数映射到它的下一个数，即 $n \mapsto n+1$。
*   两个**二元函数符号**：$+$ 和 $\cdot$。它们分别代表**加法**和**乘法**运算。

基于这些符号，我们可以递归地构造 $L_{PA}$ 的**项 (term)**。项是语言中表示“对象”（即数字）的表达式。变量是项，$0$ 是项；如果 $t$ 是一个项，那么 $S(t)$ 也是一个项；如果 $t_1$ 和 $t_2$ 是项，那么 $(t_1 + t_2)$ 和 $(t_1 \cdot t_2)$ 也是项。

$L_{PA}$ 语言中唯一的谓词符号是逻辑符号等号 $=$。因此，**原子公式 (atomic formula)** 的形式是 $t_1 = t_2$，其中 $t_1$ 和 $t_2$ 是任意的项。所有更复杂的公式都是通过使用[逻辑联结词](@entry_id:146395)（如 $\neg, \land, \lor, \to$）和量词（$\forall, \exists$）从原子公式复合而成。值得注意的是，诸如小于关系 $$ 等符号并不属于 $L_{PA}$ 的基本语言，但它们可以在理论内部被定义。例如，$x  y$ 可以被定义为 $\exists z (S(z) + x = y)$。[@problem_id:2974920]

#### 数码：为数字命名

为了在形式语言中指代特定的自然数，我们引入**数码 (numeral)** 的概念。对于任意自然数 $n \in \mathbb{N}$，其对应的数码 $\overline{n}$ 是一个**闭项**（不含自由变量的项），定义如下：
*   $\overline{0}$ 就是常数符号 $0$。
*   $\overline{n+1}$ 是项 $S(\overline{n})$。

因此，$\overline{1}$ 是 $S(0)$，$\overline{2}$ 是 $S(S(0))$，以此类推。$\overline{n}$ 就是将符号 $S$ 作用于符号 $0$ 上 $n$ 次所得到的项。这样，每个自然数都在形式语言中有了一个唯一的“名字”。

一个断言“变量 $x$ 的值等于自然数 $n$”的公式，最直接的表达方式就是原子公式 $x = \overline{n}$。这个简单的公式在任何 $L_{PA}$-结构中都精确地刻画了与数码 $\overline{n}$ 的指称相同的元素。[@problem_id:2974919] 另一种等价但更复杂的构造方式是通过递归定义一系列公式 $\mathrm{Num}_k(x)$：
*   $\mathrm{Num}_0(x) :\equiv x = 0$
*   $\mathrm{Num}_{k+1}(x) :\equiv \exists y\,(\mathrm{Num}_k(y) \wedge x = S(y))$
通过归纳法可以证明，$\mathrm{Num}_n(x)$ 在任何结构中都与 $x = \overline{n}$ 等价。[@problem_id:2974919]

#### 标准模型 $\mathbb{N}$

语言的语法只有在赋予其语义解释后才具有意义。$L_{PA}$ 的**标准模型**，通常记作 $\mathcal{N}$，旨在捕捉我们关于自然数的直观理解。其定义如下：
*   **论域 (domain)** 是自然数集合 $\mathbb{N} = \{0, 1, 2, \dots\}$。
*   **符号的解释**：
    *   常数符号 $0$ 被解释为数字 $0 \in \mathbb{N}$。我们记作 $0^{\mathcal{N}} = 0$。
    *   函数符号 $S$ 被解释为后继函数，即对于任意 $n \in \mathbb{N}$，$S^{\mathcal{N}}(n) = n+1$。
    *   函数符号 $+$ 被解释为标准的加法运算，即对于任意 $m,n \in \mathbb{N}$，$+^{\mathcal{N}}(m,n) = m+n$。
    *   函数符号 $\cdot$ 被解释为标准的乘法运算，即对于任意 $m,n \in \mathbb{N}$，$\cdot^{\mathcal{N}}(m,n) = m \cdot n$。

这个结构 $\mathcal{N}$ 是皮亚诺算术公理旨在描述的“目标”数学实体。任何对 $L_{PA}$ 符号的非标准解释，例如将 $0$ 解释为 $1$，或将 $S$ 解释为 $n \mapsto n+2$，都会产生一个不同于标准模型的结构，并且这样的结构通常不会满足下面将要介绍的皮亚诺算术的所有公理。[@problem_id:2974902]

### 皮亚诺算术（PA）的公理

皮亚诺算术理论由一组旨在刻画标准模型 $\mathcal{N}$ 属性的公理构成。这些公理分为几个部分。

#### 基础公理

这些公理规定了后继函数、加法和乘法的基本属性。等词的性质（自反性、对称性、传递性）和函数关于等词的协调性（即**合同关系**）通常被视为底层逻辑的一部分。如果将它们明确列为非逻辑公理，则必须包含如下内容：
*   **等词公理**：自反性 $\forall x (x=x)$ 以及 $S, +, \cdot$ 的合同公理，例如 $\forall x \forall y (x=y \to S(x)=S(y))$。

PA 的核心非逻辑公理如下：

1.  **后继函数公理**：
    *   (S1) $\forall x\,(\neg(S(x) = 0))$ （$0$ 不是任何数的后继）
    *   (S2) $\forall x\,\forall y\,(S(x) = S(y) \rightarrow x = y)$ （后继函数是单射）

2.  **加法公理** (递归定义)：
    *   (A1) $\forall x\,(x + 0 = x)$
    *   (A2) $\forall x\,\forall y\,(x + S(y) = S(x + y))$

3.  **乘法公理** (递归定义)：
    *   (M1) $\forall x\,(x \cdot 0 = 0)$
    *   (M2) $\forall x\,\forall y\,(x \cdot S(y) = x \cdot y + x)$

[@problem_id:2974928]

#### 一阶归纳公理模式

PA 最具威力也最具特色的部分是**归纳公理模式 (axiom schema of induction)**。它不是一条单一的公理，而是无穷多条公理的集合，每条公理对应 $L_{PA}$ 中的一个公式。

对于 $L_{PA}$ 语言中的**任意**公式 $\varphi(x, \bar{u})$（其中 $x$ 是归纳变量，$\bar{u}$ 代表一组任意的参数变量），以下公式的**全称闭包**是一个公理：
$$ \big(\varphi(0, \bar{u}) \wedge \forall x\,(\varphi(x, \bar{u}) \rightarrow \varphi(S(x), \bar{u}))\big) \rightarrow \forall z\,\varphi(z, \bar{u}) $$

该模式断言：如果一个由公式 $\varphi$ 定义的性质对 $0$ 成立（**基础情形**），并且只要它对某个数 $x$ 成立就能推出它对 $x$ 的后继 $S(x)$ 也成立（**归纳步骤**），那么该性质对所有数都成立。

例如，让我们为公式 $\varphi(x) \equiv \exists y\,(x = y + y)$ （即“$x$ 是一个偶数”）写出对应的归纳公理实例。这里没有参数 $\bar{u}$。
*   基础情形 $\varphi(0)$ 是 $\exists y\,(0 = y + y)$。
*   归纳步骤是 $\forall x\,\big(\exists y\,(x = y + y) \rightarrow \exists y\,(S(x) = y + y)\big)$。
*   结论是 $\forall x\,\exists y\,(x = y + y)$。
完整的归纳公理实例是：
$$ \Big(\exists y\,(0 = y + y) \wedge \forall x\,\big(\exists y\,(x = y + y) \rightarrow \exists y\,(S(x) = y + y)\big)\Big) \rightarrow \forall x\,\exists y\,(x = y + y) $$
这个特定的公理实例断言“如果 $0$ 是偶数，并且‘$x$ 是偶数’蕴涵‘$x+1$ 是偶数’，那么所有数都是偶数。”（当然，这个实例的归纳步骤前提是假的，但它仍然是公理模式的一个有效实例）。[@problem_id:2974928]

### PA 的表达能力与固有局限

归纳公理模式赋予了 PA 强大的证明能力，但它作为一阶理论的本质也带来了深刻的限制。

#### 公理的合理性：来自标准模型的视角

我们为何相信 PA 的公理是“正确”的？答案在于它们在标准模型 $\mathbb{N}$ 中为真。特别是，归纳公理模式的真确性，源于自然数集在集合论中的构造方式。

在策梅洛-弗兰克尔集合论 (ZFC) 中，自然数可以被定义为**最小的归纳集**。一个集合 $I$ 被称为**归纳集**，如果它包含空集 $\emptyset$（代表 $0$），并且对于其中每个元素 $n$，它也包含 $n \cup \{n\}$（代表后继 $S(n)$）。自然数集 $\mathbb{N}$ (或记为 $\omega$) 就是所有归纳集的交集，因此是包含于任何其他归纳集的最小归纳集。

现在，考虑归纳公理模式的任意实例，对应于某个公式 $\varphi(x, \bar{a})$（其中参数已在 $\mathbb{N}$ 中被解释为 $\bar{a}$）。我们可以定义一个集合 $A_\varphi = \{ n \in \mathbb{N} \mid \mathbb{N} \models \varphi(\overline{n}, \bar{a}) \}$。这个集合包含了所有在标准模型中满足性质 $\varphi$ 的自然数。

*   如果归纳的基础情形 $\mathbb{N} \models \varphi(0, \bar{a})$ 为真，那么 $0 \in A_\varphi$。
*   如果归纳步骤 $\mathbb{N} \models \forall x (\varphi(x, \bar{a}) \to \varphi(S(x), \bar{a}))$ 为真，那么对于任何 $n \in A_\varphi$，都有 $S(n) \in A_\varphi$。

这两个条件正好说明 $A_\varphi$ 是一个归纳集。但由于 $\mathbb{N}$是**最小的**归纳集，且 $A_\varphi \subseteq \mathbb{N}$，我们必然得出 $A_\varphi = \mathbb{N}$。这就意味着 $\mathbb{N} \models \forall x \varphi(x, \bar{a})$，即归纳的结论为真。这个论证表明，一阶归纳公理模式是标准模型 $\mathbb{N}$ 的一个基本属性的直接推论。[@problem_id:2974909]

#### 一阶理论的局限：非范畴性与非标准模型

归纳公理模式的强大之处在于它适用于无穷多个由公式定义的性质。然而，它的“软肋”在于它**仅仅**适用于那些可以用 $L_{PA}$ **一阶公式定义的性质**。由于 $L_{PA}$ 的公式集是可数的，这意味着 PA 的归纳公理只保证了对可数多个子集的归纳。然而，$\mathbb{N}$ 的所有子集构成的幂集是不可数的。

相比之下，**二阶算术 (Second-Order Arithmetic, PA2)** 用一条单一的、更强的二阶公理取代了一阶归纳模式：
$$ \forall X \big((0 \in X \wedge \forall x(x \in X \to S(x) \in X)) \to \forall x (x \in X)\big) $$
在这里，变量 $X$ 在所有子集上量化。这条公理确保了归纳法对**任意**子集都成立。其结果是，PA2 是**范畴的 (categorical)**，意味着它的任何两个模型都必然同构。它唯一地刻画了标准模型 $\mathbb{N}$ 的结构。

然而，PA 作为一阶理论，是不范畴的。除了标准模型 $\mathcal{N}$，它还存在许多**非标准模型 (nonstandard models)**。这些模型在结构上与 $\mathcal{N}$ 不同构。我们可以通过应用一阶逻辑的**紧致性定理 (Compactness Theorem)** 来证明非标准模型的存在。

考虑这样一个构造：在 $L_{PA}$ 中加入一个新的常数符号 $c$。然后构造一个新的理论 $T'$，它包含 PA 的所有公理，再加上无穷多个新公理：
$$ \Sigma = \{ c \neq \overline{0}, c \neq \overline{1}, c \neq \overline{2}, \dots \} $$
现在，考虑 $T'$ 的任意一个有限子集 $\Delta$。$\Delta$ 包含 PA 的公理和有限多个形如 $c \neq \overline{n_i}$ 的公理。我们可以在标准模型 $\mathcal{N}$ 中为 $\Delta$ 找到一个模型：只需将 $c$ 解释为一个比所有 $\Delta$ 中出现的 $n_i$ 都大的自然数即可。由于 $T'$ 的每个有限子集都有模型，根据紧致性定理，$T'$ 本身也有一个模型，我们称之为 $\mathcal{M}$。

这个模型 $\mathcal{M}$ 是 PA 的一个模型，并且它包含一个元素（$c$ 的解释）不同于任何一个标准自然数（$\overline{n}$ 的解释）。这个元素 $c$ 就是一个**非标准数**。$\mathcal{M}$ 的论域包含一个标准部分的副本（同构于 $\mathbb{N}$），以及像 $c$ 这样的“无穷大”的非标准元素。非标准模型正是 PA 无法完全捕捉我们关于自然数的所有直观（例如“每个数都是从0经过有限次后继得到的”）的明证。[@problem_id:2974948]

### PA 内部的计算与可表示性

尽管 PA 存在模型的局限性，但它在形式化和推理计算方面却异常强大。

#### 形式化计算：原始递归函数

**原始递归函数 (Primitive Recursive Functions, PRF)** 类是一个重要且庞大的可计算函数类。它被定义为包含以下**初始函数**并对**复合 (composition)** 和**原始递归 (primitive recursion)** 运算封闭的最小函数类：

1.  **初始函数**:
    *   **零函数**: $Z(x) = 0$。
    *   **后继函数**: $S(x) = x+1$。
    *   **投影函数**: $U_i^k(x_1, \dots, x_k) = x_i$。

2.  **闭包运算**:
    *   **复合**: 若 $f$ 是 $m$ 元 PRF，$g_1, \dots, g_m$ 是 $k$ 元 PRF，则 $h(\bar{x}) = f(g_1(\bar{x}), \dots, g_m(\bar{x}))$ 是 $k$ 元 PRF。
    *   **原始递归**: 若 $f$ 是 $k$ 元 PRF，$g$ 是 $k+2$ 元 PRF，则由以下方式定义的 $k+1$ 元函数 $h$ 是 PRF：
        $$ h(\bar{x}, 0) = f(\bar{x}) $$
        $$ h(\bar{x}, S(y)) = g(\bar{x}, y, h(\bar{x}, y)) $$

PA 的基本运算自身就是[原始递归](@entry_id:638015)的。例如，加法 $add(x,y)=x+y$ 可以通过[原始递归](@entry_id:638015)定义：
*   $add(x, 0) = x$
*   $add(x, S(y)) = S(add(x,y))$
这符合[原始递归](@entry_id:638015)模式，其中 $f(x) = U_1^1(x) = x$，$g(x,y,z) = S(U_3^3(x,y,z)) = S(z)$。由于 $f$ 和 $g$ 都是 PRF，加法也是 PRF。[@problem_id:2974907]

类似地，乘法 $mult(x,y)=x \cdot y$ 可以从加法定义：
*   $mult(x, 0) = 0$
*   $mult(x, S(y)) = add(mult(x,y), x)$
这同样符合[原始递归](@entry_id:638015)模式，其中 $f(x)=Z(x)=0$，$g(x,y,z) = add(z,x)$。因此，乘法也是 PRF。[@problem_id:2974907]

#### [可表示性](@entry_id:635277)定理

PA 与计算理论之间的核心桥梁是**[可表示性](@entry_id:635277) (Representability)**。一个 $k$ 元函数 $f: \mathbb{N}^k \to \mathbb{N}$ 被称为在 PA 中是**强可表示的**，如果存在一个公式 $\varphi_f(\vec{x}, y)$ 使得：
1.  PA 能够证明 $f$ 是一个全函数：$PA \vdash \forall \vec{x} \exists! y\, \varphi_f(\vec{x}, y)$ (即对任意输入 $\vec{x}$，存在唯一的 $y$ 满足 $\varphi_f$)。
2.  $\varphi_f$ 在标准模型中正确地刻画了 $f$ 的函数图像：对于所有 $\vec{n}, m \in \mathbb{N}$，$\mathbb{N} \models \varphi_f(\overline{\vec{n}}, \overline{m})$ 当且仅当 $m=f(\vec{n})$。

一个里程碑式的定理断言：
**所有[原始递归函数](@entry_id:155169)都在 PA 中是强可表示的。**

更进一步，这个表示公式 $\varphi_f$ 可以被构造成一个特定的形式，即 **$\Sigma_1$ 公式**。$\Sigma_1$ 公式是指形如 $\exists \vec{w} \delta(\dots)$ 的公式，其中 $\delta$ 是一个 **$\Delta_0$ 公式**（即所有[量词](@entry_id:159143)都是有界的，如 $\forall z \le t$ 或 $\exists z \le t$）。

这个定理的证明是构造性的，其核心思想是**算术化 (arithmetization)**。对于任意给定的[原始递归函数](@entry_id:155169) $f$，我们可以构造一个 $\Sigma_1$ 公式 $\varphi_f(\vec{x}, y)$，它断言“存在一个数 $w$，这个 $w$ **编码**了一个计算序列，该序列记录了计算 $f(\vec{x})$ 的全过程，并且计算的最终结果是 $y$”。这个编码过程可以通过哥德尔的 $\beta$-函数技巧实现，它允许用单个自然数编码任意长度的有限数字序列。验证[编码序列](@entry_id:204828)的正确性（例如，初始值是否正确，每一步是否遵循 $f$ 的[递归定义](@entry_id:266613)）只需要有界[量词](@entry_id:159143)，因此可以用 $\Delta_0$ 公式表达。PA 的归纳公理足够强大，可以证明这样的计算序列总是存在且唯一的。[@problem_id:2974914]

### 不完备性：PA 不能证明什么

PA 强大的表达能力吊诡地导致了其固有的不完备性。

#### $\omega$-不完备性

[哥德尔](@entry_id:637876)的第一不[完备性定理](@entry_id:151598)的一个惊人表现是 PA 的 **$\omega$-不完备性**。一个理论如果能证明 $\psi(\overline{0}), \psi(\overline{1}), \psi(\overline{2}), \dots$（即对每个标准自然数都证明 $\psi$ 成立），但却无法证明 $\forall x \psi(x)$，则称该理论是 $\omega$-不完备的。

一个经典的例子与 PA 自身的一致性陈述有关。令 $\mathrm{Prf}_{\mathrm{PA}}(p, y)$ 是一个表示“$p$ 是对 Gödel 数为 $y$ 的公式的一个 PA 证明的编码”的[原始递归](@entry_id:638015)谓词。PA 的一致性可以形式化为句子 $\mathrm{Con}(\mathrm{PA}) \equiv \neg \exists p \,\mathrm{Prf}_{\mathrm{PA}}(p, \ulcorner 0=1 \urcorner)$。

现在考虑公式 $\psi(x) \equiv \neg \mathrm{Prf}_{\mathrm{PA}}(x, \ulcorner 0=1 \urcorner)$。
*   对于任何一个标准自然数 $n \in \mathbb{N}$，我们可以通过有限的检查来验证 $n$ 并不是一个对 $0=1$ 的证明的编码（假设 PA 一致）。由于这个检查是[原始递归](@entry_id:638015)的，PA 能够形式化这个验证过程并证明 $\neg \mathrm{Prf}_{\mathrm{PA}}(\overline{n}, \ulcorner 0=1 \urcorner)$。也就是说，$PA \vdash \psi(\overline{n})$ 对所有 $n \in \mathbb{N}$ 成立。
*   然而，全称陈述 $\forall x \psi(x)$，即 $\forall x \neg \mathrm{Prf}_{\mathrm{PA}}(x, \ulcorner 0=1 \urcorner)$，逻辑上等价于 $\mathrm{Con}(\mathrm{PA})$。根据[哥德尔第二不完备性定理](@entry_id:149390)，如果 PA 是一致的，那么 $PA \nvdash \mathrm{Con}(\mathrm{PA})$。因此，$PA \nvdash \forall x \psi(x)$。

这个现象在[非标准模型](@entry_id:151939)中得到了清晰的解释。一个满足 $PA + \neg \mathrm{Con}(\mathrm{PA})$ 的[非标准模型](@entry_id:151939) $\mathcal{M}$ 必然包含一个非标准元素 $c$，使得 $\mathcal{M} \models \mathrm{Prf}_{\mathrm{PA}}(c, \ulcorner 0=1 \urcorner)$。这个非标准的“证明”$c$ 充当了 $\forall x \psi(x)$ 的一个反例，尽管它不对应任何真实的、我们可以在[元数学](@entry_id:155387)中写出的证明。类似的例子还有 $\psi(x) \equiv \neg \exists p \le x\, \mathrm{Prf}_{\mathrm{PA}}(p, \ulcorner 0=1 \urcorner)$，其全称量化也等价于 $\mathrm{Con}(\mathrm{PA})$。[@problem_id:2974912]

#### 真而不可证的句子

PA 的不完备性意味着存在着一些在标准模型 $\mathbb{N}$ 中为真，但在 PA 中却无法被证明的算术句子。

*   **哥德尔-罗瑟句子 (Gödel-Rosser Sentence)**：通过对角线引理构造出的[自指](@entry_id:153268)句子 $R_{\mathrm{PA}}$，它断言“任何对我的 PA 证明，都存在一个 Gödel 数更小的对我的否定的 PA 证明”。可以证明，如果 PA 是一致的，那么 $R_{\mathrm{PA}}$ 在 $\mathbb{N}$ 中为真，但 PA 既不能证明 $R_{\mathrm{PA}}$ 也不能证明 $\neg R_{\mathrm{PA}}$。这是一个纯粹由逻辑构造产生的不可判定句。[@problem_id:2974951]

更令人惊讶的是，一些看似“自然”的数学命题也被发现是 PA 不可判定的。

*   **古德斯坦定理 (Goodstein's Theorem)**：这是一个关于特定整数序列（古德斯坦序列）必定终止于 $0$ 的组合定理。这个定理在标准模型 $\mathbb{N}$ 中为真，其标准证明需要用到超穷归纳法直到序数 $\varepsilon_0$。因为在弱基础理论中，此定理可以推出 PA 的一致性，根据[哥德尔第二不完备性定理](@entry_id:149390)，PA 无法证明古德斯坦定理。[@problem_id:2974951]

*   **巴黎-哈灵顿原理 (Paris-Harrington Principle)**：这是有限[拉姆齐定理](@entry_id:269184)的一个加强版。它同样在 $\mathbb{N}$ 中为真，但无法在 PA 中被证明，原因与古德斯坦定理类似：它可以被用来证明 PA 的一致性。[@problem_id:2974951]

这些例子深刻地表明，任何像 PA 这样的一致、可递归公理化且足够强的形式系统，都无法捕捉到全部的算术真理。总会有一些真实的数学事实，游离于该系统的证明能力之外。