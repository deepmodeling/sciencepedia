## 引言
在人类的推理与语言中，“必然”、“可能”、“应当”等模态概念无处不在。然而，[经典逻辑](@entry_id:264911)主要处理真假命题，难以捕捉这些微妙而关键的推理维度。正规[模态逻辑](@entry_id:149086)正是为了填补这一空白而生，它提供了一个强大而灵活的形式框架，用以精确分析和推理涉及必然性、可能性、知识、信念、义务等各种模态的论证。本文旨在系统性地引导读者进入正规[模态逻辑](@entry_id:149086)的世界，从其基础构建到前沿应用，揭示其深刻的理论内涵与广泛的实践价值。

为了实现这一目标，我们将分三个核心章节展开探讨。在**“原理与机制”**一章中，我们将从零开始构建正规[模态逻辑](@entry_id:149086)的形式语言，深入剖析由Saul Kripke提出的革命性的可能世界语义，并介绍其公理化的[证明系统](@entry_id:156272)。本章将重点阐明句法和语义之间的核心桥梁——[可靠性与完备性定理](@entry_id:149316)。接下来，在**“应用与[交叉](@entry_id:147634)学科关联”**一章中，我们将展示这套理论的强大威力，探索它如何被用于模拟哲学中的知识与信念（[认知逻辑](@entry_id:153770)）、数学基础中的证明（[可证明性逻辑](@entry_id:149023)），以及它在计算机科学中如何帮助我们理解计算过程与表达能力的边界。最后，通过**“动手实践”**部分，读者将有机会通过解决具体问题来检验和巩固所学知识，将抽象理论转化为扎实的分析技能。

## 原理与机制

本章旨在深入探讨正规[模态逻辑](@entry_id:149086)的核心原理与机制。在前一章介绍其哲学动机与历史背景的基础上，我们将系统地构建正规[模态逻辑](@entry_id:149086)的[形式语言](@entry_id:265110)、语义和[证明论](@entry_id:151111)。本章的目标是不仅阐明这些组成部分的定义，更要揭示它们之间深刻的内在联系，特别是语义有效性与句法可证性之间的桥梁——[可靠性与完备性定理](@entry_id:149316)。我们将从最基本的构造块出发，逐步引领读者进入一个能够精确刻画必然性、可能性及其他模态概念的丰富理论框架。

### [模态逻辑](@entry_id:149086)的语言

任何[形式逻辑](@entry_id:263078)系统的第一步都是精确定义其语言。正规[模态逻辑](@entry_id:149086)的语言建立在经典[命题逻辑](@entry_id:143535)的基础之上，并通过引入新的算子来增强其[表达能力](@entry_id:149863)。

语言的基本成分包括：
1.  一个可数的**命题变量（propositional variables）**集合，通常记为 $\mathsf{Prop}$。这些变量，如 $p, q, r, \dots$，代表可以被赋予真或假的基本陈述。
2.  一组**布尔联结词（Boolean connectives）**。为保持理论的简洁性，我们通常只将否定（$\neg$）和蕴涵（$\to$）作为原始联结词。其他标准联结词，如合取（$\wedge$）、析取（$\vee$）和等价（$\leftrightarrow$），可以通过它们的标准定义引入作为缩写。例如，$A \wedge B$ 是 $\neg(A \to \neg B)$ 的缩写。
3.  一个一元的**模态算子（modal operator）** $\Box$，通常读作“必然地”。

基于这些成分，我们可以通过归纳法精确定义**[合式公式](@entry_id:636348)（well-formed formulas, WFFs）**的集合，该语言通常记为 $\mathcal{L}_{\Box}$。这个集合是满足以下条件的最小集合 [@problem_id:3047620]：
*   如果 $p \in \mathsf{Prop}$，那么 $p$ 是一个[合式公式](@entry_id:636348)。
*   如果 $\varphi$ 是一个[合式公式](@entry_id:636348)，那么 $\neg\varphi$ 也是一个[合式公式](@entry_id:636348)。
*   如果 $\varphi$ 和 $\psi$ 是[合式公式](@entry_id:636348)，那么 $(\varphi \to \psi)$ 也是一个[合式公式](@entry_id:636348)。
*   如果 $\varphi$ 是一个[合式公式](@entry_id:636348)，那么 $\Box\varphi$ 也是一个[合式公式](@entry_id:636348)。

除了必然性算子 $\Box$ 外，我们还有一个与之密切相关的算子——可能性算子 $\Diamond$，读作“可能地”。在大多数正规[模态逻辑](@entry_id:149086)系统中，$\Diamond$ 并非原始符号，而是通过 $\Box$ 定义的缩写。这种定义源于一个深刻的哲学和[逻辑对偶性](@entry_id:260908)：某事为可能是指“其否定不必然为假”。形式上，我们定义：

$\Diamond\varphi := \neg\Box\neg\varphi$

这个定义在功能上类似于数理逻辑中[存在量词](@entry_id:144554)（$\exists$）和[全称量词](@entry_id:145989)（$\forall$）之间的关系，即 $\exists x P(x) \leftrightarrow \neg\forall x \neg P(x)$。正如存在量化是对全称量化的对偶，可能性也是对必然性的对偶。将 $\Diamond$ 作为缩写引入，并不会增加语言的[表达能力](@entry_id:149863)，但它极大地增强了语言的便利性和直观性。从[证明论](@entry_id:151111)的角度看，将这一对偶性作为定义或公理，会产生一个对原始语言的**保守扩张（conservative extension）**，意味着在扩展后的系统中，任何不含 $\Diamond$ 的公式如果是可证的，那么它在原始的纯 $\Box$ 系统中也一定是可证的 [@problem_id:3047620]。

### 克里普克语义：[可能世界模型](@entry_id:154360)

[模态逻辑](@entry_id:149086)的现代语义学，即**克里普克语义（Kripke semantics）**，由 Saul Kripke 在20世纪中叶提出，它彻底改变了我们理解模态概念的方式。其核心思想是将公式的[真值](@entry_id:636547)与一个由“可能世界”构成的网络关联起来。

#### 框架与模型

克里普克语义的基础是两个结构：框架和模型。

一个**克里普克框架（Kripke frame）**是一个二元组 $\mathcal{F} = (W, R)$，其中 [@problem_id:3047632]：
*   $W$ 是一个非[空集](@entry_id:261946)合，其元素 $w, v, \dots$ 被称为**可能世界（possible worlds）**或状态。
*   $R$ 是 $W$ 上的一个[二元关系](@entry_id:270321)，即 $R \subseteq W \times W$，被称为**可及关系（accessibility relation）**。$wRv$ 通常被解读为“世界 $v$ 从世界 $w$ 是可及的”或“在世界 $w$ 中，世界 $v$ 是一个可能的未来/备选状态”。

一个框架描绘了可能世界之间的结[构性关系](@entry_id:195492)，但并未说明在每个世界中哪些基本命题是真的。为此，我们需要在框架上叠加一个赋值函数，从而得到一个模型。

一个**[克里普克模型](@entry_id:153269)（Kripke model）**是一个三元组 $\mathcal{M} = (W, R, V)$，其中 $(W, R)$ 是一个克里普克框架，而 $V$ 是一个**赋值函数（valuation function）**。赋值函数的作用是为每个命题变量指定其为真的世界的集合。它的形式化定义有几种等价的方式 [@problem_id:3047632]：
*   $V: \mathsf{Prop} \to \mathcal{P}(W)$，其中 $\mathcal{P}(W)$ 是 $W$ 的幂集。对于每个命题变量 $p$， $V(p)$ 就是 $p$ 为真的世界的集合。
*   $V: W \to \mathcal{P}(\mathsf{Prop})$，对于每个世界 $w$， $V(w)$ 就是在 $w$ 中为真的所有命题变量的集合。
*   $V: W \times \mathsf{Prop} \to \{0, 1\}$，对于每个世界-命题对 $(w, p)$，$V(w, p) = 1$ 表示 $p$ 在 $w$ 中为真，$V(w, p) = 0$ 表示为假。

这些定义在本质上是等价的，只是记法上的差异。在本书中，我们主要采用第一种定义。

#### 满足关系

有了模型之后，我们便可以定义一个公式 $\varphi$ 在模型 $\mathcal{M}$ 的某个世界 $w$ 中为真，记为 $\mathcal{M}, w \models \varphi$。这个**满足关系（satisfaction relation）**通过对公式的结构进行归纳来定义：

*   对于命题变量 $p \in \mathsf{Prop}$：$\mathcal{M}, w \models p$ 当且仅当 $w \in V(p)$。
*   对于布尔联结词：
    *   $\mathcal{M}, w \models \neg\varphi$ 当且仅当 $\mathcal{M}, w \not\models \varphi$。
    *   $\mathcal{M}, w \models \varphi \to \psi$ 当且仅当 (如果 $\mathcal{M}, w \models \varphi$，则 $\mathcal{M}, w \models \psi$)。
*   对于模态算子 $\Box$：
    $\mathcal{M}, w \models \Box\varphi$ 当且仅当对于所有 $v \in W$，如果 $wRv$，那么 $\mathcal{M}, v \models \varphi$。

$\Box$ 的语义条款是克里普克语义的核心。它精确地捕捉了“必然性”的直观概念：一个陈述 $\varphi$ 在当前世界 $w$ 是必然的，当且仅当它在所有从 $w$ 可及的可能世界中都为真 [@problem_id:3047632]。

基于 $\Box$ 的语义和 $\Diamond$ 的定义 $\Diamond\varphi := \neg\Box\neg\varphi$，我们可以推导出 $\Diamond$ 的语义条款 [@problem_id:3047620]：
$\mathcal{M}, w \models \Diamond\varphi$
当且仅当 $\mathcal{M}, w \models \neg\Box\neg\varphi$
当且仅当 $\mathcal{M}, w \not\models \Box\neg\varphi$
当且仅当 “对于所有 $v \in W$，如果 $wRv$，则 $\mathcal{M}, v \models \neg\varphi$” 这句话不成立
当且仅当 存在某个 $v \in W$ 使得 $wRv$ 并且 $\mathcal{M}, v \not\models \neg\varphi$
当且仅当 存在某个 $v \in W$ 使得 $wRv$ 并且 $\mathcal{M}, v \models \varphi$。

因此，$\Diamond\varphi$ 的真值条件是：
$\mathcal{M}, w \models \Diamond\varphi$ 当且仅当 存在某个 $v \in W$ 使得 $wRv$ 并且 $\mathcal{M}, v \models \varphi$。
这同样精确地捕捉了“可能性”的直观概念：一个陈述 $\varphi$ 在当前世界 $w$ 是可能的，当且仅当存在至少一个从 $w$ 可及的可能世界，在那个世界里 $\varphi$ 为真。

#### 有效性

在克里普克语义中，我们区分不同层级的“真理”：

*   **在一个模型中为真（Truth in a model）**：如果 $\varphi$ 在模型 $\mathcal{M}$ 的所有世界中都为真，我们称 $\varphi$ 在 $\mathcal{M}$ 中有效，记为 $\mathcal{M} \models \varphi$。
*   **在一个框架中有效（Validity in a frame）**：如果 $\varphi$ 在基于框架 $\mathcal{F}$ 的所有模型中都有效，我们称 $\varphi$ 在 $\mathcal{F}$ 中有效，记为 $\mathcal{F} \models \varphi$。这意味着无论我们如何为命题变量赋值，$\varphi$ 在该框架的结构下总是真的 [@problem_id:3047621]。
*   **在某一类框架中有效（Validity over a class of frames）**：如果 $\varphi$ 在某一类框架（例如，所有框架，或所有自反的框架）的每一个框架中都有效，我们称 $\varphi$ 在该类框架中有效。如果一个公式在所有克里普克框架中都有效，我们称其为**普遍有效（universally valid）**。

### [证明论](@entry_id:151111)：正规[模态逻辑](@entry_id:149086)的公理系统

与通过模型来定义真理的语义学方法相对的是**[证明论](@entry_id:151111)（proof theory）**，它通过一套公理和[推理规则](@entry_id:273148)来定义哪些公式是**定理（theorems）**。对于正规[模态逻辑](@entry_id:149086)，最常见的[证明系统](@entry_id:156272)是希尔伯特风格的公理系统。

#### 最小正规[模态逻辑](@entry_id:149086) K

所有正规[模态逻辑](@entry_id:149086)都共享一个共同的基础，这个基础就是被称为 **K** 的系统，以 Saul Kripke 的名字命名。系统 **K** 的定义如下 [@problem_id:3047636]：

**公理模式（Axiom Schemas）**：
1.  所有经典[命题逻辑](@entry_id:143535)的**重言式（tautologies）**的实例。
2.  **分配公理 K（Distribution Axiom K）**：$\Box(\varphi \to \psi) \to (\Box\varphi \to \Box\psi)$。

**[推理规则](@entry_id:273148)（Rules of Inference）**：
1.  **分离规则（Modus Ponens）**：从 $\varphi$ 和 $\varphi \to \psi$ 可以推出 $\psi$。
2.  **必然化规则（Rule of Necessitation）**：如果 $\varphi$ 是一个定理（记为 $\vdash \varphi$），那么 $\Box\varphi$ 也是一个定理（可以推出 $\vdash \Box\varphi$）。

公理K直观上意味着必然性算子在蕴涵上是可分配的。如果“若 $\varphi$ 则 $\psi$”是必然的，并且 $\varphi$ 本身是必然的，那么 $\psi$ 也必须是必然的。

一个[模态逻辑](@entry_id:149086)如果其定理集包含所有[重言式](@entry_id:143929)和所有K公理的实例，并且对分离规则和必然化规则封闭，就被称为**正规[模态逻辑](@entry_id:149086)（normal modal logic）** [@problem_id:3047636]。因此，系统 **K** 是最弱或最小的正规[模态逻辑](@entry_id:149086)。其他更强的正规[模态逻辑](@entry_id:149086)，如 **T**、**S4** 和 **S5**，都是通过在 **K** 的基础上添加新的公理模式而得到的。

#### 必然化规则的深层含义

必然化规则是正规[模态逻辑](@entry_id:149086)的一个标志性特征，但它也常常被误解。我们必须精确地理解它的含义和使用条件。

该规则陈述为：从 $\vdash \varphi$ 可以推出 $\vdash \Box\varphi$ [@problem_id:3047643]。这里的符号 $\vdash$ 表示“是可证的”或“是一个定理”。这意味着，只有当一个公式 $\varphi$ 能够从公理出发、不依赖任何前提假设而被证明时，我们才能对其应用必然化规则，得到 $\Box\varphi$ 也是一个定理。

其语义上的对应物是：如果 $\varphi$ 是普遍有效的（在所有相关模型的每个世界中都为真），那么 $\Box\varphi$ 也一定是普遍有效的。这个语义性质是可靠的，因为如果 $\varphi$ 在 *所有* 世界都为真，那么在一个任意世界 $w$ 的 *所有可及* 世界中，$\varphi$ 也必然为真，这正是 $\Box\varphi$ 在 $w$ 为真的定义 [@problem_id:3047643]。值得注意的是，这个论证不依赖于可及关系 $R$ 的任何特定性质（如[自反性](@entry_id:137262)、[传递性](@entry_id:141148)等），因此必然化规则在所有正规[模态逻辑](@entry_id:149086)中都是可靠的。

一个至关重要的警示是：**必然化不能应用于未被消除的假设**。例如，从前提 $p$ 推导出 $p$ 本身是平凡的，这可以写成 $p \vdash p$。如果我们错误地对这个推导中的结论应用必然化，就会得到 $p \vdash \Box p$。根据[演绎定理](@entry_id:635762)，这等价于 $\vdash p \to \Box p$。然而，$p \to \Box p$ 并不是一个普遍有效的公式。考虑一个简单的反例模型：$W = \{w_1, w_2\}$, $R = \{(w_1, w_2)\}$, $V(p) = \{w_1\}$。在世界 $w_1$ 中，$p$ 为真，但 $\Box p$ 为假（因为在可及的世界 $w_2$ 中 $p$ 为假）。因此，蕴涵式 $p \to \Box p$ 在 $w_1$ 处为假。这意味着允许对假设进行必然化会导致一个不可靠的（unsound）[证明系统](@entry_id:156272) [@problem_id:3047643]。

### 桥梁：[可靠性与完备性](@entry_id:148267)

[模态逻辑](@entry_id:149086)理论的真正魅力在于连接[证明论](@entry_id:151111)和语义学的桥梁：[可靠性与完备性定理](@entry_id:149316)。这些定理确保了我们句法上的符号操作（证明）与语义上的真理概念（有效性）是精确匹配的。

#### 后承关系

在讨论这些定理之前，我们需要澄清不同类型的**后承关系（consequence relations）**。

*   **句法后承（Syntactic Consequence）** ($\Gamma \vdash_L \varphi$): 表示在逻辑系统 $L$ 中，可以从前提集合 $\Gamma$ 通过公理和[推理规则](@entry_id:273148)推导出公式 $\varphi$。
*   **局部[语义后承](@entry_id:637166)（Local Semantic Consequence）** ($\Gamma \models_{\text{local}} \varphi$): 对于任何模型 $\mathcal{M}$ 和其中的任何世界 $w$，如果 $\mathcal{M}, w \models \Gamma$ (即 $\Gamma$ 中所有公式在 $w$ 处都为真)，那么 $\mathcal{M}, w \models \varphi$ [@problem_id:3047623]。这是一种在“一个情境点”上保持[真值](@entry_id:636547)的后承。
*   **全局[语义后承](@entry_id:637166)（Global Semantic Consequence）** ($\Gamma \models_{\text{glob}} \varphi$): 对于任何模型 $\mathcal{M}$，如果 $\mathcal{M} \models \Gamma$ (即 $\Gamma$ 中所有公式在该模型的 *所有* 世界中都为真)，那么 $\mathcal{M} \models \varphi$ [@problem_id:3047623]。这是一种在“整个模型”中保持[真值](@entry_id:636547)的后承。

局部后承比全局后承更强。如果一个推论在任何一个世界都成立，那么它自然也在那些前提在所有世界都成立的模型中成立。然而，反之不真。一个经典的例子是：$\{p\} \models_{\text{glob}} \Box p$ 成立，但 $\{p\} \models_{\text{local}} \Box p$ 不成立 [@problem_id:3047623]。
*   **全局后承成立**：假设在一个模型 $\mathcal{M}$ 中，$p$ 在所有世界都为真。那么对于任何世界 $w$，它的所有可及世界 $v$ 中的 $p$ 也都为真。因此，$\Box p$ 在 $w$ 处为真。由于 $w$ 是任意的，$\Box p$ 在该模型的所有世界中都为真。
*   **局部后承不成立**：我们在前文已经用过的反例模型 $W = \{w_1, w_2\}$, $R = \{(w_1, w_2)\}$, $V(p) = \{w_1\}$ 表明，在世界 $w_1$，$p$ 为真，但 $\Box p$ 为假。

大多数标准[模态逻辑](@entry_id:149086)的证明系统（如 **K**）在与局部[语义后承](@entry_id:637166)相对应时是可靠和完备的，这有时被称为**强可靠性/完备性**。

#### 对应理论：公理与框架性质

正规[模态逻辑](@entry_id:149086)最引人入胜的方面之一是某些公理模式与可及关系的特定性质之间的精确对应关系，这被称为**对应理论（correspondence theory）**。

*   **公理 K: $\Box(\varphi \to \psi) \to (\Box\varphi \to \Box\psi)$**
    正如我们所见，这个公理在**所有**克里普克框架上都是有效的 [@problem_id:3047621]。这解释了为什么它是所有正规[模态逻辑](@entry_id:149086)的“最小”公理。它不要求可及关系具有任何特殊性质。

*   **公理 T: $\Box\varphi \to \varphi$**
    这个公理表达了“必然为真的事物必然是真的”。它对应的框架性质是**自反性（reflexivity）**：对于所有 $w \in W$，都有 $wRw$。
    - **证明**：在一个自反框架中，若 $\mathcal{M}, w \models \Box\varphi$，意味着 $\varphi$ 在所有 $w$ 的可及世界中为真。由于 $w$ 自身也是可及的（$wRw$），所以 $\mathcal{M}, w \models \varphi$ 成立。因此 $\Box\varphi \to \varphi$ 在所有自反框架中有效。
    - **反例**：在一个非自反的世界 $w$（即 $\neg(wRw)$），我们可以构建一个模型使得 $\Box\varphi$ 在 $w$ 为真，但 $\varphi$ 为假。例如，让 $w$ 没有任何可及世界，此时 $\Box\varphi$ 在 $w$ 处（对任何 $\varphi$）都**空[虚地](@entry_id:269132)（vacuously）**为真。但我们可以让赋值函数使得 $\varphi$ 在 $w$ 为假 [@problem_id:3047621]。

*   **公理 4: $\Box\varphi \to \Box\Box\varphi$**
    这个公理表达了“如果某事是必然的，那么它是必然必然的”。它对应的框架性质是**[传递性](@entry_id:141148)（transitivity）**：对于所有 $x, y, z \in W$，如果 $xRy$ 且 $yRz$，那么 $xRz$。
    - **证明**：在一个传递框架中，若 $\mathcal{M}, w \models \Box\varphi$，我们要证明 $\mathcal{M}, w \models \Box\Box\varphi$。这意味着要证明对于所有 $w$ 的后继 $v$（$wRv$），都有 $\mathcal{M}, v \models \Box\varphi$。而这又需要证明对于所有 $v$ 的后继 $u$（$vRu$），都有 $\mathcal{M}, u \models \varphi$。根据传递性，从 $wRv$ 和 $vRu$ 可以得出 $wRu$。由于我们最初假设 $\mathcal{M}, w \models \Box\varphi$，这意味着 $\varphi$ 在 $w$ 的所有后继中都为真，自然也包括 $u$。因此 $\mathcal{M}, u \models \varphi$ 成立 [@problem_id:3047603]。
    - 该公理的对偶形式是 $\Diamond\Diamond\varphi \to \Diamond\varphi$ [@problem_id:3047603]。

通过向 **K** 系统添加这些公理，我们构建出了一系列著名的逻辑系统，如：
*   **T** = **K** + (T)
*   **S4** = **T** + (4)
*   **S5** = **S4** + (B: $\varphi \to \Box\Diamond\varphi$) 或 **S4** + (5: $\Diamond\varphi \to \Box\Diamond\varphi$)

每个系统都对应于一类具有特定性质的框架（例如，**S4** 对应于所有自反且传递的框架）。这种对应关系是双向的：公理在该类框架上是有效的，并且该逻辑对于该类框架是完备的。

#### K的[完备性定理](@entry_id:151598)与[典范模型](@entry_id:198268)

[模态逻辑](@entry_id:149086)的中心结果之一是**[完备性定理](@entry_id:151598)（Completeness Theorem）**。对于系统 **K**，它表明：
一个公式 $\varphi$ 在 **K** 中是可证的（$\vdash_K \varphi$），当且仅当 $\varphi$ 在所有克里普克框架中是有效的 [@problem_id:3047619]。

这个定理的“从左到右”部分是**可靠性（soundness）**，证明相对直接，只需验证所有公理在所有框架上有效，且[推理规则](@entry_id:273148)保持有效性即可。而“从右到左”的**完备性（completeness）**则要困难得多，其标准证明方法是**[典范模型](@entry_id:198268)构造（canonical model construction）**。

这个构造的精妙之处在于它完全利用了逻辑的句法成分来构建一个语义模型，并证明这个模型能“反映”逻辑自身。其关键步骤如下 [@problem_id:3047604]：
1.  **世界**：[典范模型](@entry_id:198268)的世界 $W^c$ 是该逻辑所有**[极大一致集](@entry_id:156183)（maximal consistent sets）**的集合。一个公式集是极大一致的，如果它是无矛盾的，并且添加任何不属于它的公式都会导致矛盾。
2.  **可及关系**：典范可及关系 $R^c$ 定义为：$w R^c v$ 当且仅当对于所有公式 $\varphi$，如果 $\Box\varphi \in w$，那么 $\varphi \in v$。这个定义看似晦涩，但它被精确地设计成在后续证明中能完美处理 $\Box$ 算子。
3.  **赋值**：典范赋值 $V^c$ 定义为：$p \in V^c(w)$ 当且仅当 $p \in w$。即，一个命题变量在某个“世界”（[极大一致集](@entry_id:156183)）中为真，当且仅当它本身就是那个集合的成员。
4.  **真理引理（Truth Lemma）**：通过对公式复杂度的归纳，可以证明一个惊人的结果：对于任何公式 $\varphi$ 和任何世界 $w \in W^c$，我们有 $\mathcal{M}^c, w \models \varphi$ 当且仅当 $\varphi \in w$ [@problem_id:3047604]。这个引理是连接句法（集合成员关系）和语义（模型满足关系）的终极桥梁。

有了真理引理，完备性证明就变得很简单了：如果一个公式 $\varphi$ 不是 **K** 的定理，那么 $\{\neg\varphi\}$ 就是一个 **K**-[一致集](@entry_id:747726)。通过林登鲍姆引理，它可以被扩展成一个[极大一致集](@entry_id:156183) $w$。根据真理引理，在[典范模型](@entry_id:198268) $\mathcal{M}^c$ 的世界 $w$ 中，$\neg\varphi$ 为真，这意味着 $\varphi$ 为假。因此，我们找到了一个使 $\varphi$ 为假的模型，所以 $\varphi$ 不是普遍有效的。

#### 超越K：典范性与萨尔奎斯特完备性

[典范模型](@entry_id:198268)方法的美妙之处在于其普适性。对于许多由公理集合 $\Sigma$ 扩展 **K** 得到的逻辑 $L = \mathbf{K} + \Sigma$，我们可以证明 $L$ 的典范框架 $\mathcal{F}^c_L$ 恰好满足 $\Sigma$ 中公理所对应的框架性质。这个良好的性质被称为**典范性（canonicity）**。

例如，如果我们的逻辑包含公理T（$\Box\varphi \to \varphi$），那么可以证明其典范框架是自反的。然而，并非所有公理都是典范的。幸运的是，一个被称为**萨尔奎斯特公式（Sahlqvist formulas）**的庞大且易于识别的公式类别被证明总是典范的 [@problem_id:3047642]。这个类别包含了几乎所有常见的模态公理，如 T、D、4、5、B 等。

**萨尔奎斯特[完备性定理](@entry_id:151598)**指出，任何由萨尔奎斯特公式公理化的正规[模态逻辑](@entry_id:149086)，都对于其对应的（一阶可定义的）框架类是完备的。这个强大的元定理意味着，对于一大批有用的[模态逻辑](@entry_id:149086)，我们可以通过统一的[典范模型](@entry_id:198268)方法自动获得其完备性证明，而无需为每个逻辑都重新设计复杂的证明 [@problem_id:3047642]。这充分展示了本章所讨论的形式机制的深刻性与力量。