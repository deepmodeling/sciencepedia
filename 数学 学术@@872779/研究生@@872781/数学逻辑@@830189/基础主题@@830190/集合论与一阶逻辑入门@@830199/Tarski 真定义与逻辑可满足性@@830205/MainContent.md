## 引言
“一个语句是真的，当且仅当其所言为实。”这个符合直觉的真理观念，在面对自我指涉的悖论（如说谎者悖论）时，显得脆弱不堪。20世纪的逻辑学家 Alfred Tarski 通过引入一套严格的数学方法，成功地为[形式语言](@entry_id:265110)赋予了精确的语义，从而解决了这一难题。他的工作不仅为现代[数理逻辑](@entry_id:636840)奠定了坚实的语义基础，也深刻影响了计算机科学、语言学和哲学等领域。本文旨在系统性地阐述塔斯基的真理定义与[逻辑可满足性](@entry_id:155102)理论，揭示其如何将抽象的哲学概念转化为精确的数学工具。

本文分为三个核心章节。在“原理与机制”中，我们将深入塔斯基理论的内部，从[一阶逻辑](@entry_id:154340)的句法和语义构件出发，通过递归方法定义核心的“满足”关系，并最终确立模型中“真理”的概念及其[元理论](@entry_id:638043)推论。接着，在“应用与跨学科联系”部分，我们将展示这一理论框架的强大威力，探讨它如何作为逻辑系统的基石，如何与计算复杂性理论和[自动推理](@entry_id:151826)产生深刻联系，以及它在数学基础和哲学思辨中引发的重要讨论。最后，“动手实践”部分将提供一系列练习，帮助读者将理论知识转化为解决具体问题的能力。通过这一结构化的学习路径，读者将全面掌握塔斯基语义学的精髓及其广泛的应用价值。

## 原理与机制

继引言之后，本章旨在深入剖析一阶逻辑中真理与满足性的核心原理与机制。我们将遵循 Alfred Tarski 的开创性工作，构建一个精确的语义框架。这一框架不仅为形式语句赋予了明确的意义，也揭示了关于语言、真理与可定义性之间关系的深刻见解。我们将从最基本的句法和语义构件开始，通过递归方法定义满足关系，最终达到对模型中真理概念的理解，并探讨其在[元数学](@entry_id:155387)中的重大推论。

### 句法与语义：[形式语言](@entry_id:265110)的基础

为了在数学上严格地讨论“真理”，我们首先必须精确定义我们所谈论的语言及其解释。一阶逻辑语言的表达能力源于其结构化的句法，而其意义则来自于在特定数学结构中的语义解释。

#### 项和公式的归纳构造

[一阶语言](@entry_id:151821) $L$ 的表达单位分为两类：**项 (terms)** 和 **公式 (formulas)**。项旨在指代[论域](@entry_id:265834)中的个体对象，而公式则旨在做出关于这些对象的断言，这些断言可以被判定为真或假。两者都是通过归纳法（或称递归法）来定义的。

**项** 的集合是满足以下规则的最小集合：
1.  任何变量 $x \in \mathrm{Var}$ 都是一个项。
2.  任何常量符号 $c$ 都是一个项。
3.  如果 $f$ 是一个 $n$-元函数符号，并且 $t_1, \dots, t_n$ 是项，那么 $f(t_1, \dots, t_n)$ 也是一个项。

**公式** 的集合同样由归纳法构造：
1.  **原子公式**：
    *   如果 $R$ 是一个 $n$-元关系符号，并且 $t_1, \dots, t_n$ 是项，那么 $R(t_1, \dots, t_n)$ 是一个原子公式。
    *   如果等号 $\,=\,$ 属于语言 $L$，且 $t_1, t_2$ 是项，那么 $t_1 = t_2$ 也是一个原子公式。
2.  **复合公式**：
    *   如果 $\varphi$ 和 $\psi$ 是公式，那么 $\neg \varphi$ (否定), $(\varphi \wedge \psi)$ (合取), $(\varphi \vee \psi)$ (析取), 和 $(\varphi \to \psi)$ (蕴含) 都是公式。
    *   如果 $\varphi$ 是一个公式且 $x$ 是一个变量，那么 $\forall x\,\varphi$ (全称量化) 和 $\exists x\,\varphi$ (存在量化) 都是公式。

这套严谨的构造规则构成了我们分析真理概念的句法基础 [@problem_id:2983789]。项是语言中的“名词”，而公式则是“句子”。

#### L-结构与解释

仅有句法是不够的；我们需要为这些符号串赋予意义。这通过 **$L$-结构 (L-structure)** (或称为模型) $\mathcal{M}$ 来实现。一个 $L$-结构由两部分组成：一个非空集合，称为**[论域](@entry_id:265834) (domain)** $M$，以及一个解释函数，它将语言 $L$ 中的非逻辑符号映射到[论域](@entry_id:265834) $M$ 上的具体数学对象。

具体来说，结构 $\mathcal{M}$ 为每个符号提供了如下解释：
*   对于每个常量符号 $c$，其解释 $c^{\mathcal{M}}$ 是[论域](@entry_id:265834) $M$ 中的一个特定元素。
*   对于每个 $n$-元函数符号 $f$，其解释 $f^{\mathcal{M}}$ 是一个从 $M^n$ 到 $M$ 的 $n$-元函数，即 $f^{\mathcal{M}}: M^n \to M$。
*   对于每个 $n$-元关系符号 $R$，其解释 $R^{\mathcal{M}}$ 是 $M^n$ 的一个[子集](@entry_id:261956)，即一个 $n$-元关系 $R^{\mathcal{M}} \subseteq M^n$。
*   如果语言包含等号 $\,=\,$，它总是被解释为 $M$ 上的**恒等关系**，即 $\{\langle a, a \rangle \mid a \in M\}$。

注意，关系符号被解释为关系（集合），而不是函数。例如，将一个[二元关系](@entry_id:270321)符号 $P$ 解释为 $M^2$ 的一个[子集](@entry_id:261956) $P^{\mathcal{M}}$，而不是一个函数 $M^2 \to M$，这是一个关键区别 [@problem_id:2983791]。

### 满足关系：塔斯基真理理论的核心

有了句法结构和语义解释，我们如何确定一个公式在给定结构中是真是假？对于包含变量的公式，其真假可能取决于变量代表什么。Tarski 的核心洞见在于，真理的定义必须是递归的，并且必须通过一个中介概念——**满足 (satisfaction)**——来处理变量。

#### 变量赋值的角色

为了给带有**自由变量 (free variables)**（即未被量词约束的变量）的公式赋予意义，我们需要一个**变量赋值 (variable assignment)** 函数 $s$。这是一个从变量集合 $\mathrm{Var}$ 到[论域](@entry_id:265834) $M$ 的函数，即 $s: \mathrm{Var} \to M$。它为每个变量指定了其在当前语境下所指代的[论域](@entry_id:265834)中的元素。

#### 项的求值

在定义公式的满足性之前，我们首先需要能够在给定结构 $\mathcal{M}$ 和变量赋值 $s$ 的情况下，计算出任何项所指代的确切域元素。我们将一个项 $t$ 的求值结果记为 $\llbracket t \rrbracket^{\mathcal{M},s}$。这个求值过程同样是[递归定义](@entry_id:266613)的 [@problem_id:2983775]：

1.  **基例（变量）**: 如果项 $t$ 是一个变量 $x$，其值由赋值函数 $s$ 直接给出：
    $\llbracket x \rrbracket^{\mathcal{M},s} = s(x)$。

2.  **基例（常量）**: 如果项 $t$ 是一个常量符号 $c$，其值由结构 $\mathcal{M}$ 给出，与赋值 $s$ 无关：
    $\llbracket c \rrbracket^{\mathcal{M},s} = c^{\mathcal{M}}$。

3.  **[归纳步骤](@entry_id:144594)（函数应用）**: 如果项 $t$ 的形式是 $f(t_1, \dots, t_n)$，我们首先递归地计算出所有子项 $t_i$ 的值，然后将解释后的函数 $f^{\mathcal{M}}$ 应用于这些值：
    $\llbracket f(t_1, \dots, t_n) \rrbracket^{\mathcal{M},s} = f^{\mathcal{M}}(\llbracket t_1 \rrbracket^{\mathcal{M},s}, \dots, \llbracket t_n \rrbracket^{\mathcal{M},s})$。

这个定义是良构的，因为任何项都是由有限步骤构成的。它清晰地展示了语法（项的结构）和语义（解释和赋值）之间的相互作用。一个常见的错误是混淆语法和语义，例如将语法上的子项直接作为语义函数 $f^{\mathcal{M}}$ 的输入；正确的做法是必须先对子项求值 [@problem_id:2983775]。

#### 满足关系的[递归定义](@entry_id:266613)

现在我们可以定义核心概念：在结构 $\mathcal{M}$ 中，赋值 $s$ **满足**公式 $\varphi$，记为 $\mathcal{M}, s \models \varphi$。这个定义递归地依据公式的结构进行 [@problem_id:2983772]。

##### 原子公式

这是递归的基石。
*   对于关系公式 $R(t_1, \dots, t_n)$，我们首先计算出每个项 $t_i$ 的值，然后检查由这些值构成的元组是否属于关系 $R^{\mathcal{M}}$：
    $\mathcal{M}, s \models R(t_1, \dots, t_n) \quad \text{当且仅当} \quad (\llbracket t_1 \rrbracket^{\mathcal{M},s}, \dots, \llbracket t_n \rrbracket^{\mathcal{M},s}) \in R^{\mathcal{M}}$。
    例如，对于公式 $P(h(c), x)$，在给定赋值 $g$ 下，我们首先计算项 $h(c)$ 的值为 $h^{\mathcal{M}}(c^{\mathcal{M}})$，项 $x$ 的值为 $g(x)$。然后，该公式被满足的条件是元组 $(h^{\mathcal{M}}(c^{\mathcal{M}}), g(x))$ 属于关系 $P^{\mathcal{M}}$。参数的顺序至关重要 [@problem_id:2983791]。

*   对于等式 $t_1 = t_2$，我们计算两个项的值，并检查它们是否是[论域](@entry_id:265834)中的同一个元素：
    $\mathcal{M}, s \models t_1 = t_2 \quad \text{当且仅当} \quad \llbracket t_1 \rrbracket^{\mathcal{M},s} = \llbracket t_2 \rrbracket^{\mathcal{M},s}$。

##### [逻辑联结词](@entry_id:146395)

对于通过布尔联结词连接的复合公式，其满足条件遵循标准的[真值表](@entry_id:145682)逻辑：
*   $\mathcal{M}, s \models \neg \varphi \quad \text{当且仅当} \quad \text{并非 } \mathcal{M}, s \models \varphi$。
*   $\mathcal{M}, s \models \varphi \wedge \psi \quad \text{当且仅当} \quad \mathcal{M}, s \models \varphi \text{ 并且 } \mathcal{M}, s \models \psi$。
*   $\mathcal{M}, s \models \varphi \vee \psi \quad \text{当且仅当} \quad \mathcal{M}, s \models \varphi \text{ 或 } \mathcal{M}, s \models \psi$。
*   $\mathcal{M}, s \models \varphi \to \psi \quad \text{当且仅当} \quad \text{如果 } \mathcal{M}, s \models \varphi \text{ 则 } \mathcal{M}, s \models \psi$ (这等价于“并非 $\mathcal{M}, s \models \varphi$”或“$\mathcal{M}, s \models \psi$”)。

##### [量词](@entry_id:159143)

[量词](@entry_id:159143)的处理是 Tarski 定义中最精妙的部分。它引入了对变量赋值进行局部修改的概念。我们用 $s[x \mapsto a]$ 表示一个与 $s$ 几乎完全相同的新赋值，唯一的区别在于它将变量 $x$ 映射到[论域](@entry_id:265834)元素 $a$。

*   **[存在量词](@entry_id:144554)**: 公式 $\exists x\,\varphi$ 在赋值 $s$ 下被满足，意味着我们可以在[论域](@entry_id:265834) $M$ 中**至少找到一个**元素 $a$，如果我们将变量 $x$ 的值临时改为 $a$（而不改变其他变量的值），那么新公式 $\varphi$ 在这个修改后的赋值下是满足的：
    $\mathcal{M}, s \models \exists x\,\varphi \quad \text{当且仅当} \quad \text{存在某个 } a \in M \text{ 使得 } \mathcal{M}, s[x \mapsto a] \models \varphi$。

*   **[全称量词](@entry_id:145989)**: 公式 $\forall x\,\varphi$ 在赋值 $s$ 下被满足，则要求更为严格：对于[论域](@entry_id:265834) $M$ 中的**每一个**元素 $a$，如果我们将 $x$ 的值临时改为 $a$，公式 $\varphi$ 都必须被满足：
    $\mathcal{M}, s \models \forall x\,\varphi \quad \text{当且仅当} \quad \text{对于所有 } a \in M, \mathcal{M}, s[x \mapsto a] \models \varphi$。

这个使用已修改赋值 $s[x \mapsto a]$ 的机制，优雅地处理了变量的“绑定”效应，是 Tarski 语义理论的标志性特征 [@problem_id:2983815] [@problem_id:2983772]。

### 从满足到真理：一个关键的跃迁

我们已经建立了技术性的“满足”概念，现在可以将其与更直观的“真理”概念联系起来。

#### [自由变量与约束变量](@entry_id:636101)

一个变量在一个公式中的出现，可能是**自由的 (free)** 或**约束的 (bound)**。一个约束变量的出现，是指它位于某个量词（如 $\forall x$ 或 $\exists x$）的作用域内。否则，它的出现就是自由的。同一个变量符号在同一个公式中可能既有自由出现也有约束出现。

例如，考虑公式 $\varphi(x) := \bigl(\forall y\,(R(x,y)\rightarrow P(y))\bigr) \;\wedge\; \bigl(\exists x\,P(x)\bigr)$ [@problem_id:2983814]。
*   在第一个合取项 $\forall y\,(R(x,y)\rightarrow P(y))$ 中，$x$ 的出现是自由的，因为没有 $\forall x$ 或 $\exists x$ 来约束它。它的语义值必须由变量赋值 $s$ 提供，即 $s(x)$。
*   在第二个合取项 $\exists x\,P(x)$ 中，$x$ 的出现是被 $\exists x$ [量词](@entry_id:159143)约束的。在评估这个子句时，变量 $x$ 的值不再由外部的赋值 $s$ 决定；相反，语义规则要求我们遍历[论域](@entry_id:265834)中的元素来寻找一个满足 $P(x)$ 的见证者。这个 $x$ 与第一个合取项中的自由变量 $x$ 只是恰好使用了相同的符号，但在语义上是独立的。

混淆[自由变量和约束变量](@entry_id:149665)是初学者常见的错误。Tarski 的定义通过赋值 $s$ 和赋值更新 $s[x \mapsto a]$ 的机制，精确地捕捉了这种区别。

#### 语句与模型中的真理

一个没有自由变量的公式被称为一个**语句 (sentence)**。语句的妙处在于，它们的满足性与具体的变量赋值无关。如果一个语句 $\sigma$ 在某个赋值 $s$ 下被满足，那么它在任何其他赋值 $s'$ 下也一定被满足。这是因为公式中没有[自由变量](@entry_id:151663)需要赋值来提供其指代。

这一特性使我们能够定义一个更简洁、更符合直觉的“真理”概念。我们说一个语句 $\sigma$ 在结构 $\mathcal{M}$ 中为**真 (true)**，记为 $\mathcal{M} \models \sigma$，当且仅当对于任意（等价地，某个）变量赋值 $s$，都有 $\mathcal{M}, s \models \sigma$。

因此，$\mathcal{M}, s \models \varphi$（满足）是适用于所有公式（包括带[自由变量](@entry_id:151663)的）的通用技术概念，而 $\mathcal{M} \models \sigma$（真理）是专门针对语句（封闭的断言）的、更符合哲学的概念 [@problem_id:2983814]。

#### 真语句集 $\mathrm{True}_{\mathcal{M}}$ 的性质

对于一个给定的 $L$-结构 $\mathcal{M}$，我们可以考虑所有在该结构中为真的语句的集合，记为 $\mathrm{True}_{\mathcal{M}}$:
$$ \mathrm{True}_{\mathcal{M}} := \{\sigma \in \mathrm{Sent}_L \mid \mathcal{M} \models \sigma\} $$
这个集合具有一些非常重要的逻辑性质，这些性质直接源于 Tarski 语义的[递归定义](@entry_id:266613) [@problem_id:2983795]：
*   **闭合性**: $\mathrm{True}_{\mathcal{M}}$ 在[逻辑联结词](@entry_id:146395)下是闭合的。例如：
    *   如果 $\varphi, \psi \in \mathrm{True}_{\mathcal{M}}$，那么 $\varphi \wedge \psi \in \mathrm{True}_{\mathcal{M}}$。
    *   如果 $\varphi \in \mathrm{Sent}_L$，那么 $\varphi \in \mathrm{True}_{\mathcal{M}}$ 当且仅当 $\neg \varphi \notin \mathrm{True}_{\mathcal{M}}$。这体现了[经典逻辑](@entry_id:264911)的[排中律](@entry_id:635086)和无矛盾律。
    *   如果 $\varphi \vee \psi \in \mathrm{True}_{\mathcal{M}}$，那么必然有 $\varphi \in \mathrm{True}_{\mathcal{M}}$ 或者 $\psi \in \mathrm{True}_{\mathcal{M}}$。
*   **[量词](@entry_id:159143)的处理**:
    *   $\forall x\,\varphi(x) \in \mathrm{True}_{\mathcal{M}}$ 当且仅当对于[论域](@entry_id:265834) $M$ 中的每一个元素 $a$，用指代 $a$ 的常量符号替换 $\varphi(x)$ 中的 $x$ 后得到的语句（如果语言中有这样的常量）为真。更精确地说，对于每一个 $a \in M$，在任何将 $x$ 映射到 $a$ 的赋值下，$\varphi(x)$ 都被满足。
    *   $\exists x\,\varphi(x) \in \mathrm{True}_{\mathcal{M}}$ 当且仅当存在[论域](@entry_id:265834) $M$ 中的某个元素 $a$，使得在任何将 $x$ 映射到 $a$ 的赋值下，$\varphi(x)$ 都被满足。
*   **在[逻辑后承](@entry_id:155068)下闭合**: 如果 $\mathrm{True}_{\mathcal{M}}$ 中的所有语句集合在逻辑上蕴含某个语句 $\varphi$，那么 $\varphi$ 本身也必须在 $\mathrm{True}_{\mathcal{M}}$ 中。形式上，如果 $\mathrm{True}_{\mathcal{M}} \models \varphi$，那么 $\varphi \in \mathrm{True}_{\mathcal{M}}$。这是因为 $\mathcal{M}$ 本身就是 $\mathrm{True}_{\mathcal{M}}$ 的一个模型。

值得注意的是，标准的一阶逻辑（FOL）只允许有限长度的公式。因此，即使我们有一个无限的语句序列 $\{\varphi_i\}_{i \in \mathbb{N}}$ 且每个 $\varphi_i$都在 $\mathrm{True}_{\mathcal{M}}$ 中，无限合取 $\bigwedge_{i \in \mathbb{N}} \varphi_i$ 也不是一个合法的 FOL 公式，因此也就不在 $\mathrm{True}_{\mathcal{M}}$ 中 [@problem_id:2983795]。

### [元理论](@entry_id:638043)考量及其深刻推论

Tarski 的定义不仅是一个技术工具，它还为我们思考语言和真理的本质提供了深刻的框架，并带来了一些惊人的[元理论](@entry_id:638043)结果。

#### 非空[论域](@entry_id:265834)的约定

在标准的[模型论](@entry_id:150447)中，我们总是假定 $L$-结构的[论域](@entry_id:265834) $M$ 是**非空的**。这并非一个随意的技术设定，而是为了保证一些基础的逻辑有效式成立。其中最著名的一个例子是 $\forall x\,\varphi(x) \to \exists x\,\varphi(x)$。这个公式表达了“如果某性质对所有事物都成立，那么它至少对某个事物成立”。

现在，让我们设想一个空的[论域](@entry_id:265834) $M = \emptyset$ [@problem_id:2983815]。
*   $\mathcal{M} \models \forall x\,\varphi(x)$ 的条件是“对于所有 $a \in M, \dots$”。由于 $M$ 是空的，这个条件是**空洞为真 (vacuously true)** 的。
*   $\mathcal{M} \models \exists x\,\varphi(x)$ 的条件是“存在某个 $a \in M, \dots$”。由于 $M$ 是空的，找不到这样的 $a$，所以这个条件是**假的**。

因此，在空[论域](@entry_id:265834)中，$\forall x\,\varphi(x)$ 为真，而 $\exists x\,\varphi(x)$ 为假。这使得蕴含式 $\forall x\,\varphi(x) \to \exists x\,\varphi(x)$ 为假。然而，在大多数标准的[一阶逻辑](@entry_id:154340)证明系统中，这个蕴含式都是一个定理。为了保证逻辑系统的**可靠性 (soundness)**（即所有可证的语句在所有模型中都为真），我们必须排除那些会使定理失效的模型。最简单的办法就是约定所有[论域](@entry_id:265834)都必须非空。

#### 约定T与语言层级

Tarski 在着手定义真理时，首先思考了一个问题：一个成功的真理定义应该满足什么标准？他提出了**约定T (Convention T)** 作为“实质恰当性 (material adequacy)”的标准 [@problem_id:2983771]。

约定T要求，对于一个我们试图为其定义真理的**对象语言 (object language)** $\mathcal{L}$，我们的真理定义（用一种更丰富的**[元语言](@entry_id:153750) (metalanguage)** 表述）必须能够推导出所有形如以下的语句：

> 语句 “p” 是真的，当且仅当 p。

这里，引号内的 “p” 是对象语言中的一个语句的名字（例如，它的[哥德尔](@entry_id:637876)数 $\ulcorner p \urcorner$），而引号外的 p 则是该语句在[元语言](@entry_id:153750)中的翻译或其本身的陈述。形式上，如果我们用[元语言](@entry_id:153750)中的谓词 $T(x)$ 来表达“x 是一个真语句的名字”，那么对于对象语言中的每一个语句 $\varphi$，[元语言](@entry_id:153750)必须能够证明：
$$ T(\ulcorner \varphi \urcorner) \leftrightarrow \varphi^{\mathcal{I}} $$
其中 $\varphi^{\mathcal{I}}$ 是 $\varphi$ 在[元语言](@entry_id:153750)中关于其意向结构 $\mathcal{I}$ 的陈述。

这个看似简单的[双条件句](@entry_id:276428)，精确地捕捉了真理的“[符合论](@entry_id:634661)”直觉：说一个语句是真的，无非就是断言这个语句所描述的事态确实如此。约定T本身不是一个定义，而是对任何候选定义的一个检验标准。Tarski 的[递归定义](@entry_id:266613)之所以被认为是成功的，正是因为它满足了约定T。

#### [真理的不可定义性](@entry_id:152489)定理

Tarski 工作中最惊人的结果是，对于一个足够丰富的语言（例如，能够表达基本算术的语言），其自身的真理概念是无法在该语言**内部**定义的。这就是**[真理的不可定义性](@entry_id:152489)定理 (Tarski's Undefinability of Truth Theorem)**。

这一定理的证明，巧妙地形式化了古老的**说谎者悖论 (Liar Paradox)** [@problem_id:2983792] [@problem_id:2983813]。其论证策略如下：

1.  **前提**: 假设我们有一个足够丰富的对象语言 $\mathcal{L}$（例如，包含[皮亚诺算术](@entry_id:150593) PA 的语言），并且我们**假设**可以在 $\mathcal{L}$ 内部定义一个真理谓词 $T(x)$。这意味着存在一个 $\mathcal{L}$ 的公式 $T(x)$，使得对于 $\mathcal{L}$ 中的任何语句 $\varphi$，$T(\ulcorner \varphi \urcorner)$ 为真当且仅当 $\varphi$ 为真。

2.  **[对角化](@entry_id:147016)**: 语言 $\mathcal{L}$ 的丰富性保证了**[对角引理](@entry_id:149289) (Diagonal Lemma)** 的成立。该引理断言，对于任何只有一个[自由变量](@entry_id:151663) $x$ 的公式 $\psi(x)$，都存在一个语句 $\lambda$，使得系统（如 PA）可以证明：
    $$ \lambda \leftrightarrow \psi(\ulcorner \lambda \urcorner) $$
    这个语句 $\lambda$ [实质](@entry_id:149406)上是在说“我具有性质 $\psi$”。

3.  **构造说谎者语句**: 让我们将[对角引理](@entry_id:149289)应用于公式 $\neg T(x)$。引理保证存在一个语句 $L$（即“说谎者语句”），使得：
    $$ L \leftrightarrow \neg T(\ulcorner L \urcorner) $$
    这个语句 $L$ 的直观意思是：“本语句不是真的”。

4.  **推导矛盾**: 现在我们来分析 $L$ 的[真值](@entry_id:636547)：
    *   如果 $L$ 是真的，那么根据我们假设的真理谓词 $T$ 的性质，$T(\ulcorner L \urcorner)$ 也必须是真的。但是，根据 $L$ 的构造，$L$ 为真意味着 $\neg T(\ulcorner L \urcorner)$ 为真，即 $T(\ulcorner L \urcorner)$ 为假。矛盾。
    *   如果 $L$ 是假的，那么根据 $T$ 的性质，$T(\ulcorner L \urcorner)$ 必须为假。但根据 $L$ 的构造，$L$ 为假意味着 $\neg T(\ulcorner L \urcorner)$ 为假，即 $T(\ulcorner L \urcorner)$ 为真。再次矛盾。

由于无论假设 $L$ 为真还是为假都会导致矛盾，这说明我们最初的假设——即一个适用于 $\mathcal{L}$ 的真理谓词 $T(x)$ 可以在 $\mathcal{L}$ 内部定义——必定是错误的。

这一深刻结果意味着，我们无法创建一个“在语言上封闭”的、可以谈论自身全部真理的通用语言。任何关于一个语言真理的讨论，都必须在一个表达能力更强的[元语言](@entry_id:153750)中进行。这建立了一个无限的语言层级，每一层的真理都在更高的一层中定义。Tarski 的工作不仅为[数理逻辑](@entry_id:636840)提供了坚实的语义基础，也为哲学、语言学和计算机科学带来了深远的影响。