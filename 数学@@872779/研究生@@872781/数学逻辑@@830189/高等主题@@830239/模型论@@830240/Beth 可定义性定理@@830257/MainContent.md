## 引言
在数理逻辑和数学哲学中，一个核心问题是：一个概念在何种意义上可以被一种[形式语言](@entry_id:265110)精确地“捕获”？可定义性（Definability）理论正是为了回答这一问题而生。它试图区分那些能够被语言清晰界定的概念和那些本质上模糊或超越语言[表达能力](@entry_id:149863)的概念。这一探索自然引出了两种核心的可定义性观念：一种是语义上的唯一性，即一个概念的含义被理论的整体结构所唯一固定，这被称为“[隐式可定义性](@entry_id:152992)”；另一种是句法上的构造性，即存在一个具体的公式来直接描述这个概念，这被称为“[显式可定义性](@entry_id:149730)”。

一个自然而深刻的问题随之而来：这两种可定义性之间有何关系？直观上，显式定义似乎更为苛刻，但语义上的唯一性是否也足以保证我们总能找到一个具体的定义公式呢？Beth可定义性定理正是解答这一关键问题的基石，它断言在一阶逻辑这一被广泛应用的框架中，两种可定义性实际上是等价的。本文旨在全面剖析Beth可定义性定理。在“原理与机制”一章中，我们将深入其核心定义，并详细拆解其依赖于[克雷格插值定理](@entry_id:148559)的精妙证明。随后的“应用与跨学科关联”一章将视野拓宽，探讨该定理如何与逻辑的边界（如塔斯基定理）和[集合论](@entry_id:137783)的基础（如哥德尔的构造性宇宙）产生深刻共鸣。最后，通过“动手实践”部分，读者将有机会通过具体练习来巩固和深化对可定义性这一核心逻辑概念的理解。

## 原理与机制

在介绍性章节之后，我们现在深入探讨 Beth 可定义性定理的核心原理与证明机制。本章将首先精确阐述两种核心的可定义性概念——[显式可定义性](@entry_id:149730)与[隐式可定义性](@entry_id:152992)，并阐明它们所依赖的基础模型论操作。随后，我们将陈述 Beth 可定义性定理，并详细剖析其关键证明，该证明巧妙地运用了 Craig [插值定理](@entry_id:173911)。最后，本章将探讨该定理的深远意义，包括其在逻辑学基本原理中的地位、向[带参数可定义性](@entry_id:150254)的扩展，以及它与[模型论](@entry_id:150447)中其他基石（如 Löwenheim-Skolem 定理和[模型完备性](@entry_id:149630)）的相互作用。

### 可定义性的核心概念

在数学和逻辑中，“可定义”这一概念旨在捕捉一个对象或关系能否完全用一种给定语言的资源来描述。在[模型论](@entry_id:150447)的框架下，这一直观想法被精确化为两种形式：[显式可定义性](@entry_id:149730)与[隐式可定义性](@entry_id:152992)。

为了建立讨论的背景，我们假设 $L$ 是一个[一阶语言](@entry_id:151821)，$R$ 是一个不属于 $L$ 的新 $n$ 元关系符号。我们将扩展后的语言记为 $L' = L \cup \{R\}$。我们考虑一个在 $L'$ 语言中的理论 $T'$，它描述了我们感兴趣的结构。

#### [显式可定义性](@entry_id:149730) (Explicit Definability)

**[显式可定义性](@entry_id:149730)** (explicit definability) 是最直观的可定义性概念。它断言，新的关系 $R$ 可以通过一个仅使用原语言 $L$ 中符号的公式来直接“写出来”。

形式上，我们说关系符号 $R$ 在理论 $T'$ 中是**显式可定义**的，如果存在一个 $L$-公式 $\varphi(\bar{x})$（其中 $\bar{x}$ 是 $n$ 个自由变元的元组），使得：
$$ T' \models \forall \bar{x}\,(R(\bar{x}) \leftrightarrow \varphi(\bar{x})) $$
这个[逻辑推论](@entry_id:155068)意味着，在 $T'$ 的任何模型中，$R$ 的解释都精确地由公式 $\varphi(\bar{x})$ 在该模型的 $L$-归约 (L-reduct) 中定义的集合所决定。换言之，如果我们有一个 $T'$ 的模型 $\mathcal{N}$，其 $L$-归约记为 $\mathcal{M} = \mathcal{N} \upharpoonright L$，那么 $R$ 在 $\mathcal{N}$ 中的解释 $R^{\mathcal{N}}$ 必须满足：
$$ R^{\mathcal{N}} = \{\bar{a} \in M^{n} : \mathcal{M} \models \varphi(\bar{a})\} $$
这里，$M$ 是模型的[论域](@entry_id:265834)。这个定义是统一的，即同一个 $L$-公式 $\varphi$ 对 $T'$ 的所有模型都有效。因此，[显式可定义性](@entry_id:149730)提供了一个从 $L$-结构到 $R$ 的解释的“配方”或“蓝图”[@problem_id:2969276]。

#### [隐式可定义性](@entry_id:152992) (Implicit Definability)

与[显式可定义性](@entry_id:149730)提供一个直接构造不同，**[隐式可定义性](@entry_id:152992)** (implicit definability) 通过唯一性来刻画概念。它断言，尽管我们可能没有一个直接定义 $R$ 的公式，但理论 $T'$ 对 $L$-结构的约束已经强大到足以唯一地“固定” $R$ 的解释。

要精确地陈述这一点，我们需要引入 $L'$-扩张 ($L'$-expansion) 的概念。一个 $L$-结构 $\mathcal{A}$ 的 $L'$-扩张是一个 $L'$-结构 $\mathcal{A}'$，其 $L$-归约恰好是 $\mathcal{A}$，即 $\mathcal{A}' \upharpoonright L = \mathcal{A}$。由于 $\mathcal{A}$ 已经给定了 $L$ 中所有符号的解释，一个扩张 $\mathcal{A}'$ 完全由它对新符号 $R$ 的解释所决定。

据此，我们说 $R$ 在理论 $T'$ 中是**隐式可定义**的，当且仅当对于任何一个作为 $T'$ 某个模型之归约的 $L$-结构 $\mathcal{A}$，任何两个作为 $T'$ 模型的 $\mathcal{A}$ 的 $L'$-扩张，它们对 $R$ 的解释必须相同。更形式化地讲 [@problem_id:2969285]：

对于每一个作为 $T'$ 某个模型之 $L$-归约的 $L$-结构 $\mathcal{A}$，若 $\mathcal{A}'_{1}$ 和 $\mathcal{A}'_{2}$ 是 $\mathcal{A}$ 的任意两个 $L'$-扩张，且它们都满足理论 $T'$（即 $\mathcal{A}'_{1} \models T'$ 且 $\mathcal{A}'_{2} \models T'$），则必须有 $R^{\mathcal{A}'_{1}} = R^{\mathcal{A}'_{2}}$。

这个定义的核心是**唯一性** (uniqueness)。它并不要求每个相关的 $L$-结构都 *必须* 能扩张成 $T'$ 的模型，但如果可以，那么扩张的方式必须是唯一的。仅仅要求每个 $L$-结构都 *存在* 至少一个扩张是不足够的，这只描述了存在性而非唯一性 [@problem_id:2969276]。[隐式可定义性](@entry_id:152992)断言，$L$-归约已经包含了确定 $R$ 的所有信息，理论 $T'$ 只是揭示了这一隐藏的约束。

#### 基础机制：归约操作

上述两种可定义性的定义都隐含地依赖于归约 (reduct) 操作的良好性质。归约操作 $\mathcal{M} \upharpoonright L_0$ 指的是从一个 $L_1$-结构 $\mathcal{M}$（其中 $L_0 \subseteq L_1$）通过“遗忘”所有不属于 $L_0$ 的符号的解释而得到的 $L_0$-结构。这个操作有几个至关重要的特性：

1.  **[传递性](@entry_id:141148) (Transitivity):** 归约操作是传递的。对于嵌套的语言 $L \subseteq L'' \subseteq L'$ 和一个 $L'$-结构 $\mathcal{N}$，我们总是有 $(\mathcal{N} \upharpoonright L'') \upharpoonright L = \mathcal{N} \upharpoonright L$。这意味着从一个丰富的语言逐步归约到一个基础语言，其结果与一次性直接归约是相同的。这个属性保证了“$L$-归约”这个概念是明确无误的，为[隐式可定义性](@entry_id:152992)的定义提供了坚实的基础 [@problem_id:2969272]。

2.  **[真值](@entry_id:636547)保持 (Truth Preservation):** 对于一个 $L$-句子 $\sigma$ 和一个 $L'$-结构 $\mathcal{N}$，$\sigma$ 在 $\mathcal{N}$ 中的[真值](@entry_id:636547)仅取决于其 $L$-归约 $\mathcal{N} \upharpoonright L$。更一般地，对于任何语言扩张和归约，我们有 $\mathcal{N} \models \sigma \iff \mathcal{N} \upharpoonright L \models \sigma \iff \mathcal{N} \upharpoonright L'' \models \sigma$。这个性质保证了在显式定义的表达式 $\forall \bar{x}\,(R(\bar{x}) \leftrightarrow \varphi(\bar{x}))$ 中，$\varphi(\bar{x})$ 的[真值](@entry_id:636547)可以安全地在其 $L$-归约中进行评估 [@problem_id:2969272]。

### Beth 可定义性定理：连接隐式与显式

直观上，[显式可定义性](@entry_id:149730)似乎比[隐式可定义性](@entry_id:152992)更强。如果一个关系有明确的“配方”，那么它的解释自然是唯一的。然而，反过来是否成立呢？如果一个关系被唯一确定，我们是否总能找到一个描述它的公式？Beth 可定义性定理给出了一个深刻而肯定的回答。

#### 定理的陈述

**Beth 可定义性定理**断言，在[一阶逻辑](@entry_id:154340)中，[隐式可定义性](@entry_id:152992)与[显式可定义性](@entry_id:149730)是等价的。

**定理 (Beth, 1953):** 设 $T'$ 是一个 $L' = L \cup \{R\}$ 理论。关系符号 $R$ 被 $T'$ 隐式定义（相对于 $L$），当且仅当 $R$ 被 $T'$ 显式定义（使用一个 $L$-公式）。

这个定理包含两个方向：

-   **显式 $\implies$ 隐式：** 这是较为平凡的方向。如果存在一个 $L$-公式 $\varphi(\bar{x})$ 使得 $T' \models \forall \bar{x}\,(R(\bar{x}) \leftrightarrow \varphi(\bar{x}))$，那么对于任何作为 $T'$ 模型归约的 $L$-结构 $\mathcal{M}$，其任何满足 $T'$ 的扩张中 $R$ 的解释都必须是 $\{\bar{a} : \mathcal{M} \models \varphi(\bar{a})\}$。这个集合完全由 $\mathcal{M}$ 和 $\varphi$ 决定，因此是唯一的。这直接满足了[隐式可定义性](@entry_id:152992)的要求 [@problem_id:2969276]。

-   **隐式 $\implies$ 显式：** 这是定理深刻之处。它表明，只要一个理论能以某种方式保证唯一性，无论多么间接，一阶[逻辑的表达能力](@entry_id:152092)都足以将这种唯一性“编译”成一个具体的、显式的定义公式。这个方向的证明是本节的核心 [@problem_id:2969276] [@problem_id:2969284]。

需要注意的是，这个定义性的断言是由理论 $T'$ 保证的，而不是在基础理论 $T$（若有）或空理论中成立。定义公式是 $L$-公式，但其与 $R$ 的等价性是 $T'$ 的一个推论 [@problem_id:2969276]。

#### 证明机制：Craig [插值定理](@entry_id:173911)

Beth 定理（从隐式到显式）的经典证明依赖于另一个一阶逻辑的基石——**Craig [插值定理](@entry_id:173911) (Craig Interpolation Theorem, CIT)**，以及[紧致性定理](@entry_id:148512)。

**定理 (Craig, 1957):** 若 $\psi \models \theta$ 是一个有效的[逻辑推论](@entry_id:155068)，则存在一个**插值式 (interpolant)** $\chi$，其所有非逻辑符号都同时出现在 $\psi$ 和 $\theta$ 中，使得 $\psi \models \chi$ 且 $\chi \models \theta$。

Beth 定理的证明巧妙地构建了一个[逻辑推论](@entry_id:155068)，其插值式恰好就是我们寻求的定义公式 $\varphi$。以下是证明的概要 [@problem_id:2969289] [@problem_id:2969290] [@problem_id:2969284]：

1.  **“[双拷贝](@entry_id:150182)”论证 (The "Two-Copy" Argument):** 假设 $R$ 被 $T'$ 隐式定义。为了找到一个显式定义，我们通过反证法，利用隐式定义性来构造一个矛盾。我们引入一个与 $R$ “同构”的新关系符号 $R'$，并考虑语言 $L \cup \{R, R'\}$。设 $T''$ 是将 $T'$ 中所有出现的 $R$ 替换为 $R'$ 后得到的理论。

2.  **构造矛盾理论:** 考虑理论 $\Sigma = T' \cup T'' \cup \{\exists \bar{x} (R(\bar{x}) \land \neg R'(\bar{x}))\}$。我们断言该理论是**不一致的** (inconsistent)。
    -   **证明:** 假设 $\Sigma$ 是一致的，那么它有一个模型 $\mathcal{A}$。令 $\mathcal{M} = \mathcal{A} \upharpoonright L$ 为其 $L$-归约。
    -   我们构造两个 $T'$ 的模型：$\mathcal{N}_1 = (\mathcal{M}, R^{\mathcal{A}})$ 和 $\mathcal{N}_2 = (\mathcal{M}, R'^{\mathcal{A}})$。由于 $\mathcal{A} \models T'$ 且 $\mathcal{A} \models T''$，因此 $\mathcal{N}_1$ 和 $\mathcal{N}_2$ 都是 $T'$ 的模型。
    -   $\mathcal{N}_1$ 和 $\mathcal{N}_2$ 拥有完全相同的 $L$-归约 $\mathcal{M}$。根据[隐式可定义性](@entry_id:152992)的假设，它们对 $R$ 的解释必须相同。但在我们的构造中，这意味着 $R^{\mathcal{A}} = R'^{\mathcal{A}}$。
    -   然而，模型 $\mathcal{A}$ 也满足 $\exists \bar{x} (R(\bar{x}) \land \neg R'(\bar{x}))$，这意味着 $R^{\mathcal{A}} \neq R'^{\mathcal{A}}$。这便导出了矛盾。
    -   因此，理论 $\Sigma$ 必然是不一致的。

3.  **应用紧致性与[插值定理](@entry_id:173911):** 既然 $\Sigma$ 不一致，即 $T' \cup T'' \cup \{\exists \bar{x} (R(\bar{x}) \land \neg R'(\bar{x}))\} \models \bot$（$\bot$ 代表矛盾），我们可以重新[排列](@entry_id:136432)得到 $T' \cup T'' \models \forall \bar{x} (R(\bar{x}) \to R'(\bar{x}))$。
    -   根据**[紧致性定理](@entry_id:148512) (Compactness Theorem)**，此推论仅依赖于 $T'$ 和 $T''$ 的有限多个公理。为简化论证，我们可以（通过引入新常量 $\bar{c}$）得到一个形如 $\Gamma_1(R, \bar{c}) \models \Gamma_2(R', \bar{c})$ 的推论。
    -   这里的 $\Gamma_1$ 属于语言 $L \cup \{R, \bar{c}\}$，而 $\Gamma_2$ 属于语言 $L \cup \{R', \bar{c}\}$。它们的公共语言是 $L \cup \{\bar{c}\}$。
    -   根据 Craig [插值定理](@entry_id:173911)，存在一个插值式 $\varphi(\bar{c})$，其语言为 $L \cup \{\bar{c}\}$（即 $\varphi$ 是一个 $L$-公式），使得：
        -   $\Gamma_1(R, \bar{c}) \models \varphi(\bar{c})$
        -   $\varphi(\bar{c}) \models \Gamma_2(R', \bar{c})$

4.  **提取显式定义:** 这两个推论可以被“翻译”回关于理论 $T'$ 的陈述。
    -   第一个推论意味着 $T' \models \forall \bar{x} (R(\bar{x}) \to \varphi(\bar{x}))$。
    -   第二个推论，由于其在逻辑上对所有 $R'$ 成立，我们可以用 $R$ 替换 $R'$，从而得到 $T' \models \forall \bar{x} (\varphi(\bar{x}) \to R(\bar{x}))$。
    -   两者结合，我们得到了 $T' \models \forall \bar{x} (R(\bar{x}) \leftrightarrow \varphi(\bar{x}))$。
    -   这个 $L$-公式 $\varphi(\bar{x})$ 就是我们寻求的显式定义。

这个证明精妙地展示了模型论中语法（公式、证明）与语义（模型、真理）之间的深刻联系。

### 范围、扩展与意义

Beth 可定义性定理不仅是一个孤立的技术结果，它处于一阶逻辑核心性质的交汇点，并对我们理解逻辑系统的表达能力有着重要启示。

#### 基本原理的等价性

在一阶逻辑的[元理论](@entry_id:638043)中，Beth 可定义性定理、Craig [插值定理](@entry_id:173911)和 Robinson 联合一致性定理 (Robinson's Joint Consistency Theorem) 构成了等价的三驾马车。这意味着，在一个逻辑系统中，只要其中一个成立，另外两个也必然成立。这些定理的证明通常都离不开[紧致性定理](@entry_id:148512)，显示了紧致性在[一阶逻辑](@entry_id:154340)中的核心地位。因此，Beth 定理本身不是仅靠 Gödel [完备性定理](@entry_id:151598)就能推导出的初等结果 [@problem_id:2969284] [@problem_id:2969274]。

#### 带参数的可定义性

在实践中，我们常常关心一个关系是否能用“给定的参数”来定义。例如，在[域论](@entry_id:155241)中，一个元素是否代数，取决于它是否是某个以有理数为系数的[多项式的根](@entry_id:154615)。这里的“有理数”就是参数。Beth 定理可以自然地扩展到**带参数的可定义性** (definability with parameters)。

标准做法是通过扩展语言来处理参数。如果我们想允许使用集合 $A$ 中的元素作为参数，我们可以为 $A$ 中的每个元素引入一个新的常量符号，从而将基础语言从 $L$ 扩展到 $L(A)$。然后，我们直接将 Beth 定理应用于这个新的语言对：$L(A)$ 和 $L(A) \cup \{R\}$。定理的结论将保证存在一个 $L(A)$-公式 $\varphi(\bar{x})$（即一个可能包含来自 $A$ 的常量符号的公式）来显式定义 $R$。这个过程依赖于[一阶逻辑](@entry_id:154340)及其基本定理（如紧致性）对于任意基数大小的语言都成立的事实 [@problem_id:2969279]。

#### [基数](@entry_id:754020)、模型与 Löwenheim-Skolem

Beth 定理的结论是一个关于理论和公式的语法陈述（$T' \models \dots$），但它的力量在于它对所有模型都成立，无论模型的大小。**Löwenheim-Skolem 定理**在理解这一点上扮演了重要角色。

假设我们有一个 $T'$ 的不[可数模型](@entry_id:152788) $\mathfrak{M}$。由于 $L'$（在通常假设下）是可数的，向下 Löwenheim-Skolem 定理保证存在一个可数的**[初等子结构](@entry_id:155222) (elementary substructure)** $\mathfrak{N} \preccurlyeq \mathfrak{M}$。
-   作为一个 $T'$ 的模型，$\mathfrak{N}$ 必须满足 Beth 定理的结论，即 $\mathfrak{N} \models \forall \bar{x} (R(\bar{x}) \leftrightarrow \varphi(\bar{x}))$ 对某个 $L$-公式 $\varphi$ 成立。
-   “$\forall \bar{x} (R(\bar{x}) \leftrightarrow \varphi(\bar{x}))$” 是一个单一的 $L'$-句子。[初等子结构](@entry_id:155222)的定义保证了任何 $L'$-句子在 $\mathfrak{N}$ 中为真当且仅当它在 $\mathfrak{M}$ 中为真。
-   因此，该定义在原始的不[可数模型](@entry_id:152788) $\mathfrak{M}$ 中也必须成立。

这个论证模式展示了 Beth 定理的健壮性：定义的存在性是一个不依赖于模型基数的理论层面的属性。我们可以通过在[可数模型](@entry_id:152788)中进行核心的插值论证，然后利用初等性将结果“提升”到任意模型 [@problem_id:2969282]。

#### 可定义性的局限

Beth 定理的成立高度依赖于[一阶逻辑](@entry_id:154340)的紧致性。在缺乏紧致性的逻辑系统中，该定理通常会失效。一个典型的例子是**[无穷逻辑](@entry_id:148205) (infinitary logic)** $L_{\omega_1, \omega}$，它允许可数无穷个析取和合取。

在 $L_{\omega_1, \omega}$ 中，我们可以写出像 $\forall x (P(x) \leftrightarrow \bigvee_{i \in \omega} (x = c_i))$ 这样的公理，它将 $P$ 的解释唯一地固定为所有常量 $c_i$ 的集合。因此，$P$ 是隐式可定义的。然而，这个由无限个点构成的集合通常不能被任何一个**有限的**一阶 $L$-公式所定义。因此，在 $L_{\omega_1, \omega}$ 的语境下，[隐式可定义性](@entry_id:152992)并不蕴含（有限的）[显式可定义性](@entry_id:149730) [@problem_id:2969284]。

#### 与[模型完备性](@entry_id:149630)的联系

Beth 定理还与[模型论](@entry_id:150447)中的其他重要概念相互关联。例如，如果基础理论 $T$ 是**模型完备的 (model complete)**（即模型间的任何嵌入都是[初等嵌入](@entry_id:155980)），那么显式定义可以被进一步精化。在这种情况下，我们可以选择一个语法形式更简单的定义公式 $\varphi(\bar{x})$，例如一个**存在公式 (existential formula)**。这表明基础理论的结构性质可以影响到由 Beth 定理所保证的定义公式的复杂性 [@problem_id:2969284]。