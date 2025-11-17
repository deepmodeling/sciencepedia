## 引言
[模态逻辑](@entry_id:149086)是现代逻辑的一个核心分支，它通过扩展[经典逻辑](@entry_id:264911)的语言，使我们能够形式化地推理关于必然性、可能性、知识、信念、义务等多种“模态”概念。传统[命题逻辑](@entry_id:143535)只关心命题的真假，但在日常语言和科学探索中，我们经常需要表达“某事是必须的”或“某事是可能的”，这种表达的[真值](@entry_id:636547)并不仅仅取决于其组成部分的真值。如何为这些复杂的内涵概念（intensional concepts）提供一个严谨、统一的语义框架，正是[模态逻辑](@entry_id:149086)要解决的核心问题。可能世界语义，作为 Saul Kripke 的革命性贡献，为此提供了强大而直观的解决方案。

本文旨在系统地介绍[模态逻辑](@entry_id:149086)及其可能世界语义。我们将通过三个章节的探索，带领读者从理论基础走向实际应用。在第一章“原理与机制”中，我们将构建[模态逻辑](@entry_id:149086)的[形式语言](@entry_id:265110)，并深入讲解可能世界语义的核心——Kripke模型，揭示模态公理与框架属性间的对应关系。接着，在第二章“应用与跨学科连接”中，我们将展示这一理论框架如何被广泛应用于哲学、计算机科学、数学和语言学等多个领域，以解决从知识论到[程序验证](@entry_id:264153)的各类问题。最后，在第三章“动手实践”中，你将通过具体的练习来巩固所学知识，亲手构建和分析Kripke模型。通过这段旅程，你将掌握一个分析复杂推理模式的强大工具。

## 原理与机制

继前一章对[模态逻辑](@entry_id:149086)的直观背景和历史动机进行介绍之后，本章将深入探讨其形式化的核心：命题[模态逻辑](@entry_id:149086)的句法结构与基于可能世界语义的解释机制。我们将系统地构建这一理论框架，从最基本的语言定义出发，逐步引入其语义模型，并最终揭示句法公理与语义属性之间深刻的对应关系。

### [模态逻辑](@entry_id:149086)的语言

与任何形式系统一样，我们的探索始于精确定义其语言。命题[模态逻辑](@entry_id:149086)的语言是在标准[命题逻辑](@entry_id:143535)的基础上，通过引入新的算子来增强其表达能力的。

其形式化定义如下。语言的构件包括：

1.  一个可数无穷的**命题变量（propositional variables）**集合，记作 $\mathsf{Prop} = \{p_0, p_1, p_2, \ldots\}$。这些变量代表基本的原子命题，如“天是蓝的”或“$x=5$”。
2.  一组**布尔联结词（Boolean connectives）**，包括 $\neg$ （否定）、$\wedge$ （合取）、$\vee$ （析取）和 $\rightarrow$ （蕴含）。
3.  两个一元的**模态算子（modal operators）**：$\Box$ （必然性）和 $\Diamond$ （可能性）。
4.  用于消除歧义的括号 `(` 和 `)`。

基于这些构件，**[合式公式](@entry_id:636348)（well-formed formulas, WFFs）**的集合，记作 $\mathsf{Fm}$，可以通过归纳法来定义。它是满足以下条件的最小集合 [@problem_id:3046658]：

*   **基础情形**：如果 $p \in \mathsf{Prop}$，那么 $p \in \mathsf{Fm}$。这意味着任何命题变量本身都是一个[合式公式](@entry_id:636348)。
*   **[归纳步骤](@entry_id:144594)**：
    *   如果 $\varphi \in \mathsf{Fm}$，那么 $(\neg \varphi)$、$ (\Box \varphi)$ 和 $(\Diamond \varphi)$ 也属于 $\mathsf{Fm}$。
    *   如果 $\varphi, \psi \in \mathsf{Fm}$，那么 $(\varphi \wedge \psi)$、$(\varphi \vee \psi)$ 和 $(\varphi \rightarrow \psi)$ 也属于 $\mathsf{Fm}$。

这一定义可以用更紧凑的**巴科斯-诺尔[范式](@entry_id:161181) (Backus-Naur Form, BNF)** 等价地表达：
$$ \varphi ::= p \mid (\neg \varphi) \mid (\varphi \wedge \psi) \mid (\varphi \vee \psi) \mid (\varphi \rightarrow \psi) \mid (\Box \varphi) \mid (\Diamond \varphi) $$
其中 $p$ 是任意命题变量，$ \varphi $ 和 $ \psi $ 是任意[合式公式](@entry_id:636348)。在实践中，为了可读性，最外层的括号通常会被省略。

### 可能世界语义

仅仅定义了语言的句法，公式本身并无意义。我们需要一个语义框架来解释这些公式的真假。在现代[模态逻辑](@entry_id:149086)中，标准的方法是 **Kripke 语义**，或称**可能世界语义 (Possible Worlds Semantics)**。其核心思想是，一个公式的真值不是绝对的，而是相对于一个特定的“世界”或“状态”而言的。

#### Kripke 框架与模型

Kripke 语义的基本结构是 **Kripke 框架（Kripke frame）**，它是一个偶对 $\mathcal{F} = (W, R)$，其中 [@problem_id:3046679]：

*   $W$ 是一个非空的**世界（worlds）**集合。这些“世界”可以被直观地理解为不同的情境、时间点、知识状态或计算状态。
*   $R \subseteq W \times W$ 是一个[二元关系](@entry_id:270321)，称为**可及关系（accessibility relation）**。如果 $(w, v) \in R$（也记作 $wRv$），我们就说世界 $v$ 是从世界 $w$ 可及的。这个关系是解释模态算子的关键：它限定了在评估 $w$ 处的模态陈述时，我们需要考虑哪些“相关的”或“可能的”世界 [@problem_id:3046636]。

一个框架仅仅提供了世界的结构。为了评估包含具体命题的公式，我们需要知道每个原子命题在哪个世界为真。这通过**赋值函数（valuation function）** $V$ 来实现。将赋值函数添加到框架中，我们便得到了一个 **[Kripke 模型](@entry_id:153269)（Kripke model）**，它是一个三元组 $\mathcal{M} = (W, R, V)$，其中：

*   $(W, R)$ 是一个 Kripke 框架。
*   $V: \mathsf{Prop} \to \mathcal{P}(W)$ 是一个函数，它将每个命题变量 $p$ 映射到 $W$ 的一个[子集](@entry_id:261956) $V(p)$。这个[子集](@entry_id:261956) $V(p)$ 就是命题 $p$ 为真的所有世界的集合 [@problem_id:3046679]。

#### 满足关系

有了 [Kripke 模型](@entry_id:153269)，我们便可以精确定义一个公式 $\varphi$ 在模型 $\mathcal{M}$ 的某个世界 $w$ 中为真，记作 $\mathcal{M}, w \vDash \varphi$。这个**满足关系（satisfaction relation）**同样是归纳定义的 [@problem_id:3046685]：

1.  **原子命题**：对于命题变量 $p$，$\mathcal{M}, w \vDash p$ 当且仅当 $w \in V(p)$。这直接将原子命题的真值与赋值函数关联起来。

2.  **布尔联结词**：这些联结词的解释是经典和“局部”的，即它们的[真值](@entry_id:636547)完全由其组分在当前世界 $w$ 的真值决定：
    *   $\mathcal{M}, w \vDash \neg \varphi$ 当且仅当 $\mathcal{M}, w \nvDash \varphi$ （即 $\mathcal{M}, w \vDash \varphi$ 不成立）。
    *   $\mathcal{M}, w \vDash \varphi \wedge \psi$ 当且仅当 $\mathcal{M}, w \vDash \varphi$ 并且 $\mathcal{M}, w \vDash \psi$。
    *   $\mathcal{M}, w \vDash \varphi \rightarrow \psi$ 当且仅当 $\mathcal{M}, w \nvDash \varphi$ 或者 $\mathcal{M}, w \vDash \psi$。

3.  **模态算子**：这是 Kripke 语义的核心。与布尔联结词不同，模态算子的真值依赖于其他可及世界的情况。它们将评估的“上下文”从当前世界 $w$ “转移”到了其可及的世界 [@problem_id:3046685]：
    *   $\mathcal{M}, w \vDash \Box \varphi$ （在 $w$ **必然**有 $\varphi$）当且仅当对于所有世界 $v \in W$，如果 $wRv$，那么 $\mathcal{M}, v \vDash \varphi$。换言之，$\varphi$ 在所有从 $w$ 可及的世界中都必须为真。
    *   $\mathcal{M}, w \vDash \Diamond \varphi$ （在 $w$ **可能**有 $\varphi$）当且仅当存在某个世界 $v \in W$，使得 $wRv$ 并且 $\mathcal{M}, v \vDash \varphi$。换言之，至少存在一个从 $w$ 可及的世界，$\varphi$ 在其中为真。

为了具体理解这些定义，我们来看一个例子 [@problem_id:3046679]。考虑模型 $\mathcal{M}=(W,R,V)$，其中 $W=\{w_0, w_1, w_2\}$, $R=\{(w_0,w_1), (w_0,w_2), (w_1,w_1)\}$, 且 $V(p)=\{w_0, w_2\}$, $V(q)=\{w_1\}$。

*   $\mathcal{M}, w_0 \vDash \Diamond p$ 是否成立？
    我们需要检查是否存在一个从 $w_0$ 可及的世界 $v$ 使得 $\mathcal{M}, v \vDash p$。从 $R$ 可知，$w_0$ 可及的世界是 $w_1$ 和 $w_2$。
    *   对于 $v=w_1$，$w_1 \notin V(p)$，所以 $\mathcal{M}, w_1 \nvDash p$。
    *   对于 $v=w_2$，$w_2 \in V(p)$，所以 $\mathcal{M}, w_2 \vDash p$。
    因为我们找到了一个这样的世界 ($w_2$)，所以 $\mathcal{M}, w_0 \vDash \Diamond p$ 成立。

*   $\mathcal{M}, w_1 \vDash \Box q$ 是否成立？
    我们需要检查所有从 $w_1$ 可及的世界 $v$ 是否都满足 $\mathcal{M}, v \vDash q$。从 $R$ 可知，唯一从 $w_1$ 可及的世界是 $w_1$ 本身。因为 $w_1 \in V(q)$，所以 $\mathcal{M}, w_1 \vDash q$。由于所有（仅有一个）可及世界都满足条件，因此 $\mathcal{M}, w_1 \vDash \Box q$ 成立。

*   $\mathcal{M}, w_2 \vDash \Box q$ 是否成立？
    从 $R$ 中我们看到，没有任何关系以 $w_2$ 开头，所以 $w_2$ 没有任何可及的世界。在这种情况下，"所有从 $w_2$ 可及的世界都满足..." 这一条件是**无风险地（vacuously）**为真的，因为它没有反例。因此，$\mathcal{M}, w_2 \vDash \Box q$ 成立。

### 基本语义属性

#### 算子对偶性

在[经典逻辑](@entry_id:264911)中，[全称量词](@entry_id:145989) $\forall$ 和[存在量词](@entry_id:144554) $\exists$ 是对偶的，即 $\exists x \, \phi(x) \equiv \neg \forall x \, \neg \phi(x)$。模态算子 $\Diamond$ 和 $\Box$ 之间也存在完全类似的**对偶关系（duality）**。我们可以将 $\Diamond$ 算子看作是 $\Box$ 和 $\neg$ 的一个缩写：$\Diamond\varphi$ 是 $\neg\Box\neg\varphi$ 的简便写法。

我们可以严格地从语义上证明这种等价性 [@problem_id:3046704]。在一个任意模型 $\mathcal{M}$ 和世界 $w$ 中：
$\mathcal{M}, w \vDash \neg\Box\neg\varphi$
$\iff$ $\mathcal{M}, w \nvDash \Box\neg\varphi$ (根据 $\neg$ 的语义)
$\iff$ 不是“对于所有满足 $wRv$ 的 $v$，都有 $\mathcal{M}, v \vDash \neg\varphi$” (根据 $\Box$ 的语义)
$\iff$ 存在某个 $v$ 使得 $wRv$ 并且 $\mathcal{M}, v \nvDash \neg\varphi$ (量词取反)
$\iff$ 存在某个 $v$ 使得 $wRv$ 并且 $\mathcal{M}, v \vDash \varphi$ (根据 $\neg$ 的语义)
$\iff$ $\mathcal{M}, w \vDash \Diamond\varphi$ (根据 $\Diamond$ 的语义)

这一推导表明，$\Diamond\varphi \equiv \neg\Box\neg\varphi$ 在任何 [Kripke 模型](@entry_id:153269)中都成立，无论可及关系 $R$ 有何种性质。同样地，我们也可以证明其逆对偶关系：$\Box\varphi \equiv \neg\Diamond\neg\varphi$ [@problem_id:3046704]。因此，我们可以在只保留一个模态算子作为基础的同时，通过定义得到另一个，而不损失任何[表达能力](@entry_id:149863)。

#### 不同层级的“真”

在使用[模态逻辑](@entry_id:149086)时，精确区分不同层级的“真”或“有效性”至关重要 [@problem_id:3046664]。

*   **局部满足性 (Local Satisfiability)**：即我们一直在讨论的 $\mathcal{M}, w \vDash \varphi$。它指的是一个公式在特定模型的特定世界中为真。

*   **全局满足性 (Global Satisfiability / Truth in a model)**：记作 $\mathcal{M} \vDash \varphi$。它指的是一个公式在特定模型 $\mathcal{M}$ 的**所有**世界中都为真。即 $\forall w \in W, \mathcal{M}, w \vDash \varphi$。一个公式可能在某模型中是局部满足的，但非全局满足的。例如，在之前的模型中，$\mathcal{M}, w_0 \vDash \Diamond p$ 成立，但 $\mathcal{M}, w_1 \nvDash \Diamond p$，因此 $\mathcal{M} \nvDash \Diamond p$ [@problem_id:3046664]。

*   **框架有效性 (Validity on a Frame Class)**：记作 $\mathsf{F} \vDash \varphi$。它指的是一个公式在属于某个框架类 $\mathsf{F}$ 的**所有框架**上都是有效的。这意味着，对于 $\mathsf{F}$ 中的任何框架 $\mathcal{F}$ 和任何可能的赋值函数 $V$，公式 $\varphi$ 在模型 $\mathcal{M}=(\mathcal{F}, V)$ 中都是全局满足的。这是一个关于框架结构的强有力断言。

*   **[语义推论](@entry_id:637166) (Semantic Consequence)**：记作 $\Gamma \vDash \varphi$。它指的是真值的保持。标准的（局部）定义是：对于任何模型 $\mathcal{M}$ 和任何世界 $w$，如果所有在前提集合 $\Gamma$ 中的公式都在 $(\mathcal{M}, w)$ 处为真，那么结论 $\varphi$ 也必须在 $(\mathcal{M}, w)$ 处为真。例如，$\{\Box(p \rightarrow q), \Box p\} \vDash \Box q$ 是一个基本的[语义推论](@entry_id:637166)。这是因为，如果在 $w$ 处 $\Box(p \rightarrow q)$ 和 $\Box p$ 都为真，意味着在所有可及世界 $v$ 中，$p \rightarrow q$ 和 $p$ 都为真。根据[命题逻辑](@entry_id:143535)，在所有这些 $v$ 中 $q$ 也必须为真。因此，根据 $\Box$ 的定义，$\Box q$ 在 $w$ 处为真 [@problem_id:3046664]。

### 可及关系的角色：对应理论

我们已经看到，可及关系 $R$ 在解释模态算子时起着核心作用。通过对 $R$ 施加不同的约束条件，我们可以得到具有不同逻辑属性的模态系统。**对应理论（Correspondence Theory）**研究的就是模态公理模式与可及关系的一阶属性之间的系统性联系。

以下是一些最常见的关系属性及其[一阶逻辑](@entry_id:154340)定义 [@problem_id:3046649] [@problem_id:3050570]：

*   **[自反性](@entry_id:137262) (Reflexivity)**：每个世界都可以到达自身。
    *   FO 定义: $\forall x \, R(x,x)$
    *   对应公理 (T): $\Box\varphi \rightarrow \varphi$
    *   语义解释：如果必然为真的事物（在所有可及世界中为真），那么它在当前世界也为真（因为当前世界是可及的）[@problem_id:3046679]。

*   **对称性 (Symmetry)**：如果 $w$ 可以到达 $v$，那么 $v$ 也可以到达 $w$。
    *   FO 定义: $\forall x \forall y \, (R(x,y) \rightarrow R(y,x))$
    *   对应公理 (B): $\varphi \rightarrow \Box\Diamond\varphi$

*   **传递性 (Transitivity)**：如果 $w$ 能到 $v$，$v$ 能到 $u$，那么 $w$ 就能到 $u$。
    *   FO 定义: $\forall x \forall y \forall z \, ((R(x,y) \wedge R(y,z)) \rightarrow R(x,z))$
    *   对应公理 (4): $\Box\varphi \rightarrow \Box\Box\varphi$
    *   一个简单的非传递关系例子是 $R=\{(0,1), (1,2)\}$ 在 $W=\{0,1,2\}$ 上。这里 $0 \to 1$ 且 $1 \to 2$，但 $0 \not\to 2$ [@problem_id:3046649]。而整数上的“小于等于”关系 $\leq$ 则是[传递性](@entry_id:141148)的 [@problem_id:3046649]。

*   **序列性 (Seriality)**：每个世界至少可以到达一个世界。
    *   FO 定义: $\forall x \exists y \, R(x,y)$
    *   对应公理 (D): $\Box\varphi \rightarrow \Diamond\varphi$
    *   语义解释：如果某事是必然的（在所有可及世界为真），那么它也必然是可能的（因为至少存在一个可及世界）。

*   **欧几里得性 (Euclideanness)**：从同一个世界可及的任意两个世界之间是相互可及的。
    *   FO 定义: $\forall x \forall y \forall z \, ((R(x,y) \wedge R(x,z)) \rightarrow R(y,z))$
    *   对应公理 (5): $\Diamond\varphi \rightarrow \Box\Diamond\varphi$

例如，考虑一个由四个世界组成的环状结构 $W=\{1,2,3,4\}$, $R=\{(1,2),(2,1),(2,3),(3,2),(3,4),(4,3),(4,1),(1,4)\}$。我们可以检验，这个关系是序列性的（每个点都有出口）和对称性的（每条边都是双向的），但它不是自反的（没有自环）、传递的（例如 $1 \to 2$ 且 $2 \to 3$，但 $1 \not\to 3$）或欧几里得的（例如 $1 \to 2$ 且 $1 \to 4$，但 $2 \not\to 4$）[@problem_id:3050570]。不同的[模态逻辑](@entry_id:149086)系统，如 **T**, **S4**, **S5** 等，正是通过组合这些公理（及其对应的框架条件）来定义的。

### 公理系统

除了通过 Kripke 语义进行定义，[模态逻辑](@entry_id:149086)也可以通过**公理系统（Axiomatic Systems）**从纯句法的角度进行刻画。一个公理系统由一组公理（或公理模式）和一组推导规则组成。

最基础的[正规模态逻辑](@entry_id:634221)系统是 **K 系统**。它被设计为在所有 Kripke 框架上都是可靠和完备的，即一个公式在 K 系统中是可证的，当且仅当它在所有 [Kripke 模型](@entry_id:153269)中都有效。K 系统的 Hilbert 式公理化包含以下部分 [@problem_id:3046709]：

1.  **公理模式**:
    *   所有**[命题逻辑](@entry_id:143535)的重言式 (Tautologies)** 的实例。这确保了所有经典命题推理都有效。
    *   **K 公理模式 (Distribution Axiom)**: $\Box(\varphi \rightarrow \psi) \rightarrow (\Box\varphi \rightarrow \Box\psi)$。
        *   **语义辩护**：这个公理是有效的，因为它精确地捕捉了 $\Box$ 算子在任意可及关系上的行为。如果在当前世界 $w$，我们知道“$\varphi \rightarrow \psi$ 在所有可及世界为真”并且“$\varphi$ 在所有可及世界为真”，那么在任何一个可及世界 $v$ 中，$\varphi$ 和 $\varphi \rightarrow \psi$ 都成立，因此 $v$ 处的 $\psi$ 也必然成立。由于这对所有可及世界都成立，所以 $\Box\psi$ 在 $w$ 处成立。

2.  **推导规则**:
    *   **分离规则 (Modus Ponens, MP)**: 从 $\varphi$ 和 $\varphi \rightarrow \psi$ 可以推导出 $\psi$。
        *   **语义辩护**：此规则保持有效性。如果 $\varphi$ 和 $\varphi \rightarrow \psi$ 在所有模型的所有世界中都为真，那么 $\psi$ 也必然如此。
    *   **必然化规则 (Necessitation, NEC)**: 如果 $\varphi$ 是一个定理（即 $\vdash \varphi$），那么可以推导出 $\vdash \Box\varphi$。
        *   **语义辩护**：此规则同样保持有效性。如果 $\varphi$ 是一个定理，意味着它在所有模型的**所有**世界中都为真（即 $\varphi$ 是普遍有效的）。那么，对于任何世界 $w$，它的所有可及世界自然也满足 $\varphi$。因此，$\Box\varphi$ 在 $w$ 处也为真。由于 $w$ 是任意的，所以 $\Box\varphi$ 也是普遍有效的。

通过在 K 系统上添加 T、B、4、5 等公理，我们便可以得到其他更强的[正规模态逻辑](@entry_id:634221)系统。

### [表达能力](@entry_id:149863)与[不变性](@entry_id:140168)：[互模拟](@entry_id:156097)

我们自然会问：[模态逻辑](@entry_id:149086)究竟能表达什么样的性质？它的[表达能力](@entry_id:149863)的界限在哪里？**[互模拟](@entry_id:156097)（Bisimulation）**这一概念为我们提供了回答此问题的关键工具。

直观上，如果两个 [Kripke 模型](@entry_id:153269)中的两个世界在结构上无法被[模态逻辑](@entry_id:149086)公式区分，我们就说它们是**[互模拟](@entry_id:156097)的 (bisimilar)**。形式上，给定两个模型 $\mathcal{M}_1=(W_1,R_1,V_1)$ 和 $\mathcal{M}_2=(W_2,R_2,V_2)$，一个非空关系 $Z \subseteq W_1 \times W_2$ 是一个[互模拟](@entry_id:156097)，如果对于所有 $(w,u) \in Z$，满足以下三个条件 [@problem_id:3046646]：

1.  **原子和谐 (Atomic harmony)**：对于所有命题变量 $p$，$\mathcal{M}_1, w \vDash p$ 当且仅当 $\mathcal{M}_2, u \vDash p$。即两个世界在原子命题上达成一致。
2.  **“去”条件 (Forth condition)**：如果 $w$ 在 $\mathcal{M}_1$ 中有一个后继 $w'$（即 $wR_1w'$），那么 $u$ 必须在 $\mathcal{M}_2$ 中有一个后继 $u'$，使得 $w'$ 和 $u'$ 也被 $Z$ 关联（即 $(w', u') \in Z$）。
3.  **“回”条件 (Back condition)**：对称地，如果 $u$ 在 $\mathcal{M}_2$ 中有一个后继 $u'$，那么 $w$ 必须在 $\mathcal{M}_1$ 中有一个后继 $w'$，使得 $(w', u') \in Z$。

一个核心的定理是**[互模拟](@entry_id:156097)下的模态[不变性](@entry_id:140168)（Modal Invariance under Bisimulation）**：如果两个点 $(w, u)$ 是[互模拟](@entry_id:156097)的，那么它们满足完全相同的模态公式。证明思路是通过对公式结构进行归纳。基础情形由“原子和谐”保证。[归纳步骤](@entry_id:144594)中，“去”和“回”条件完美地对应了 $\Diamond$ 和 $\Box$ 算子的语义需求 [@problem_id:3046646]。

[互模拟](@entry_id:156097)是一个比[图同构](@entry_id:143072)更弱的概念。例如，一个世界 $a$ 有两个后继 $b, c$，它们都满足 $p$；另一个世界 $x$ 只有一个后继 $y$，它满足 $p$。尽管这两个模型结构不同（一个有2个后继，一个有1个），但它们可以是[互模拟](@entry_id:156097)的 [@problem_id:3046646]。这表明基础[模态逻辑](@entry_id:149086)无法“计数”后继的数量。

这一观察引出了[模态逻辑](@entry_id:149086)中一个里程碑式的结论——**van Benthem 特征定理 (van Benthem's Characterization Theorem)**。该定理指出，在所有 [Kripke 模型](@entry_id:153269)上，一个一阶逻辑公式 $\phi(x)$ (带一个[自由变量](@entry_id:151663)) 是在[互模拟](@entry_id:156097)下保持不变的，当且仅当它等价于某个模态公式的标准翻译。

其意义是深远的：它精确地刻画了模态[逻辑的表达能力](@entry_id:152092)。[模态逻辑](@entry_id:149086)正是**[一阶逻辑](@entry_id:154340)中对[互模拟](@entry_id:156097)不变的片段** [@problem_id:3046640]。它不是[一阶逻辑](@entry_id:154340)的一个随意[子集](@entry_id:261956)，而是一个在模型论上极其自然的片段，它所能表达的恰好是那些在“忽略[互模拟](@entry_id:156097)可区分的结构差异”后仍然成立的性质。