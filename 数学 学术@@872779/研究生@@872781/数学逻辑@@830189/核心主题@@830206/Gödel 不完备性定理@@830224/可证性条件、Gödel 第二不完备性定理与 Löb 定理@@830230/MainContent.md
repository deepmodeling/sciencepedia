## 引言
[哥德尔不完备性定理](@entry_id:153511)从根本上改变了我们对数学、逻辑和[计算极限](@entry_id:138209)的理解。这些深刻的结论，连同同样反直觉的[勒布定理](@entry_id:154850)，揭示了[形式系统](@entry_id:634057)在进行[自我参照](@entry_id:170448)时固有的局限性。然而，这些定理的哲学震撼力有时会掩盖其背后严谨而精密的数学机制。理解这些定理并非停留在“有些事无法证明”的模糊认知上，而是需要深入探究“可证性”这一概念本身是如何在形式系统内部被精确定义和操控的。本文旨在填补这一空白，从[元数学](@entry_id:155387)的哲学思辨转向其坚实的算术基础。

为此，我们将系统地展开一次探索之旅。在第一章“原理与机制”中，我们将通过算术化构建可证性谓词，详细推导希尔伯特-伯奈斯-勒布（HBL）可证性条件，并在此基础上严格证明[哥德尔第二不完备性定理](@entry_id:149390)和[勒布定理](@entry_id:154850)。接着，在第二章“应用与跨学科联系”中，我们将展示这些核心原理如何催生了[可证明性逻辑](@entry_id:149023)（GL）这一全新领域，并探讨它们如何用于衡量[理论强度](@entry_id:189300)，以及与[计算理论](@entry_id:273524)和[证明论](@entry_id:151111)的深刻联系。最后，在第三章“动手实践”中，你将通过一系列精心设计的问题，将理论知识付诸实践，加深对[自指](@entry_id:153268)、[不动点](@entry_id:156394)和形式证明的理解。

## 原理与机制

在“引言”章节中，我们概述了[哥德尔不完备性定理](@entry_id:153511)的历史背景和哲学意涵。现在，我们将深入探讨支撑这些深刻结果的数学原理和形式机制。本章的目标是系统地构建可证性的概念，阐明其必须满足的关键条件，并推导出[哥德尔第二不完备性定理](@entry_id:149390)和 Löb 定理。我们将看到，这些结果并非源于模糊的哲学思辨，而是形式系统内在逻辑的精确、必然的推论。

### 可证性的形式化：可证性谓词

哥德尔革命性洞见的基石在于意识到，关于一个[形式系统](@entry_id:634057)（如[皮亚诺算术](@entry_id:150593) PA）的[元数学](@entry_id:155387)陈述（例如，“句子 $\varphi$ 是可证的”）本身可以被编码为该系统内部的算术陈述。这一过程称为**算术化** (arithmetization)。为了严格地讨论可证性，我们必须首先在算术语言中精确地定义它。

第一步是定义一个**证明谓词** (proof predicate)，记作 $\mathrm{Proof}_T(y, x)$。这是一个[二元关系](@entry_id:270321)，其直观含义是“自然数 $y$ 是理论 $T$ 中公式 $x$ 的一个证明的[哥德尔](@entry_id:637876)数”。一个证明本质上是一个公式的有限序列，其中每个公式要么是 $T$ 的一条公理，要么是通过[推理规则](@entry_id:273148)（如**[肯定前件式](@entry_id:268205)**，Modus Ponens）从序列中前面的公式推导出来的。证明的最后一行就是被证明的公式。

我们可以利用算术的基本构件（如素数、幂运算）将这种序列结构和验证过程完全形式化。例如，我们可以将一个公式序列 $\langle \varphi_0, \dots, \varphi_{n-1} \rangle$ 编码为一个自然数 $y$。然后，$\mathrm{Proof}_T(y, x)$ 这个谓词会断言以下几点 [@problem_id:2971579]：
1.  $y$ 编码了一个长度为 $n$ 的良构公式序列。
2.  该序列的最后一个公式的哥德尔数是 $x$。
3.  对于序列中的每一个公式 $\varphi_i$（其中 $i  n$），$\varphi_i$ 要么是 $T$ 的一条公理（我们可以通过一个公理谓词 $\mathrm{Ax}_T$ 来检查），要么存在 $j, k  i$，使得 $\varphi_j$ 是蕴含式 $\varphi_k \to \varphi_i$。

由于理论 $T$ 的公理集是递归的（或递归可枚举的），并且检查一个公式序列是否符合证明的定义是一个纯粹的机械过程，所以关系 $\mathrm{Proof}_T(y, x)$ 是一个**[原始递归](@entry_id:638015)关系**。在算术理论中，所有[原始递归](@entry_id:638015)关系都可以被**有界公式**（$\Delta_0$ 公式）所表达。这意味着 $\mathrm{Proof}_T(y, x)$ 可以在算术语言中被一个不含无界量词的公式所定义。

有了证明谓词，我们就可以定义核心的**可证性谓词** (provability predicate)，记作 $\mathrm{Prov}_T(x)$。它的定义非常直观：
$$
\mathrm{Prov}_T(x) \equiv \exists y\, \mathrm{Proof}_T(y, x)
$$
这个公式的含义是“存在一个 $y$，使得 $y$ 是公式 $x$ 的一个证明的哥德尔数”，或者简而言之，“$x$ 在 $T$ 中是可证的”。

这个定义的关键后果在于其句法形式。由于 $\mathrm{Proof}_T(y, x)$ 是一个 $\Delta_0$（或至少是 $\Delta_1$）公式，在其前面加上一个[存在量词](@entry_id:144554) $\exists y$ 就使得 $\mathrm{Prov}_T(x)$ 成为了一个 $\Sigma_1$ **公式**。这个观察看似技术性，但正如我们将看到的，可证性谓词的 $\Sigma_1$ 特性是其后续所有重要性质的根源 [@problem_id:2971578]。

### Hilbert-Bernays-Löb 可证性条件

一个自然的问题是：这个通过算术化构造出来的标准可证性谓词 $\mathrm{Prov}_T(x)$ 具有哪些性质？它是否准确地“捕捉”了我们关于“可证”这个概念的直观理解？Hilbert、Bernays 和后来的 Löb 确定了三个关键条件，现在被称为 **Hilbert-Bernays-Löb (HBL) 可证性条件**。任何一个“行为良好”的可证性谓词都应在理论 $T$ 内部被证明满足这些条件。

对于所有句子 $\varphi$ 和 $\psi$，
-   **(D1)** 如果 $T \vdash \varphi$，那么 $T \vdash \mathrm{Prov}_T(\ulcorner \varphi \urcorner)$。
-   **(D2)** $T \vdash \mathrm{Prov}_T(\ulcorner \varphi \to \psi \urcorner) \to (\mathrm{Prov}_T(\ulcorner \varphi \urcorner) \to \mathrm{Prov}_T(\ulcorner \psi \urcorner))$。
-   **(D3)** $T \vdash \mathrm{Prov}_T(\ulcorner \varphi \urcorner) \to \mathrm{Prov}_T(\ulcorner \mathrm{Prov}_T(\ulcorner \varphi \urcorner) \urcorner)$。

这里，$\ulcorner \varphi \urcorner$ 表示句子 $\varphi$ 的[哥德尔](@entry_id:637876)数。让我们来解析这些条件的含义和其背后的机制。

**(D1)** 是最基本的条件。它表明，如果一个句子在 $T$ 中确实有一个证明，那么 $T$ 本身就能够证明“该句子是可证的”这一事实。这本质上是说，可证性谓词正确地**表示** (represents) 了 $T$ 的定理集。其证明机制很简单：如果 $T \vdash \varphi$，就存在一个具体的证明，其[哥德尔](@entry_id:637876)数为 $p$。$T$ 作为一个足够强的算术理论，可以验证 $\mathrm{Proof}_T(\bar{p}, \ulcorner \varphi \urcorner)$ 这个具体的[原始递归](@entry_id:638015)陈述，然后通过[存在量词](@entry_id:144554)引入得到 $\exists y\, \mathrm{Proof}_T(y, \ulcorner \varphi \urcorner)$，也就是 $\mathrm{Prov}_T(\ulcorner \varphi \urcorner)$。

**(D2)** 被称为**内化的[肯定前件式](@entry_id:268205)**。它表明 $T$ 知道其可证性概念对于[肯定前件式](@entry_id:268205)是封闭的。换句话说，$T$ 能证明：如果它能证明一个蕴含式和它的前件，那么它也能证明它的后件。这个条件的证明机制非常直观 [@problem_id:2971590]。我们可以在 $T$ 内部进行推理：假设我们有 $\varphi \to \psi$ 的一个证明（编码为 $p$）和 $\varphi$ 的一个证明（编码为 $q$）。我们可以通过将这两个证明序列拼接起来，并在末尾加上一行 $\psi$（理由是[肯定前件式](@entry_id:268205)）来构造一个新的序列（编码为 $r$）。这个构造过程是[原始递归](@entry_id:638015)的。然后，我们需要在 $T$ 内部证明这个新序列 $r$ 的确是 $\psi$ 的一个合法证明。这需要通过对 $r$ 的行数进行归纳来验证每一行都是合法的。这个证明可以在一个相对较弱的算术系统，如**有界算术** ($I\Delta_0$) 加上指数函数公理 ($\mathrm{Exp}$) 中完成。其中 $\mathrm{Exp}$ 保证了序列编码的可能性，而 $I\Delta_0$ 提供了必要的有界归纳原理。

**(D3)** 是这三个条件中最微妙的一个。它断言 $T$ 能够证明：如果一个句子是可证的，那么“它是可证的”这个事实本身也是可证的。D3 的证明依赖于 $\mathrm{Prov}_T(x)$ 的 $\Sigma_1$ 形式。其核心是一个更一般性的原则，称为**可证的 $\Sigma_1$-完备性** (provable $\Sigma_1$-completeness) [@problem_id:2971591]。该原则指出，对于任何 $\Sigma_1$ 句子 $\sigma$，理论 $T$ 都能证明 $\sigma \to \mathrm{Prov}_T(\ulcorner \sigma \urcorner)$。其内在逻辑是：如果一个 $\Sigma_1$ 句子 $\sigma \equiv \exists y\, \delta(y)$ 为真，那么就存在一个见证者 $n$ 使得 $\delta(\bar{n})$ 为真。由于 $\delta$ 是一个 $\Delta_0$ 公式，其[真值](@entry_id:636547)是可以在 $T$ 中被验证的，所以 $T \vdash \delta(\bar{n})$。从 $\delta(\bar{n})$ 的证明，我们可以构造出 $\exists y\, \delta(y)$ 即 $\sigma$ 的证明。这个从“真”到“可证”的整个过程对于 $\Sigma_1$ 句子是可以在 $T$ 内部形式化的。现在，回到 D3：$T \vdash \mathrm{Prov}_T(\ulcorner \varphi \urcorner) \to \mathrm{Prov}_T(\ulcorner \mathrm{Prov}_T(\ulcorner \varphi \urcorner) \urcorner)$。我们只需注意到，句子 $\mathrm{Prov}_T(\ulcorner \varphi \urcorner)$ 本身就是一个 $\Sigma_1$ 句子。因此，D3 就是可证的 $\Sigma_1$-完备性原则应用于 $\mathrm{Prov}_T(\ulcorner \varphi \urcorner)$ 自身的一个特例。

### 标准定义的不可或缺性

我们已经看到，标准的 $\Sigma_1$ 可证性谓词 $\mathrm{Prov}_T(x)$ 满足 HBL 条件。但是，这种选择是唯一的吗？是否存在其他在标准模型 $\mathbb{N}$ 中同样能正确描述 $T$ 的定理集，但句法形式不同的谓词？如果存在，它们也满足 HBL 条件吗？

答案是否定的。HBL 条件对可证性谓词的句法形式极其敏感。许多与 $\mathrm{Prov}_T(x)$ **外延等价** (extensionally equivalent)（即在标准模型中指代相同集合）的谓词，却无法满足 HBL 条件。这表明我们对 $\mathrm{Prov}_T(x)$ 的标准定义并非任意，而是其 $\Sigma_1$ 形式对于推导不完备性至关重要。

让我们看几个例子：
-   **一个失败 D1 的谓词**：考虑 $T$ 的一致性陈述 $\mathrm{Con}(T) \equiv \neg \mathrm{Prov}_T(\ulcorner 0=1 \urcorner)$。现在定义一个新的谓词 $\mathrm{Prv}'(x) \equiv \mathrm{Prov}_T(x) \land \mathrm{Con}(T)$ [@problem_id:2971578]。如果 $T$ 是一致的，那么 $\mathrm{Con}(T)$ 在标准模型中为真，因此 $\mathrm{Prv}'(x)$ 与 $\mathrm{Prov}_T(x)$ 外延等价。但是，这个谓词是否满足 D1？如果满足，那么对于任何 $T$ 的定理 $\varphi$，我们必须有 $T \vdash \mathrm{Prv}'(\ulcorner \varphi \urcorner)$，即 $T \vdash \mathrm{Prov}_T(\ulcorner \varphi \urcorner) \land \mathrm{Con}(T)$。这将意味着 $T \vdash \mathrm{Con}(T)$。然而，[哥德尔第二不完备性定理](@entry_id:149390)恰恰指出，一个一致的理论 $T$ 无法证明其自身的一致性。因此，$\mathrm{Prv}'(x)$ 必然无法满足 D1。

-   **一个失败 D2 的谓词**：考虑著名的 **Rosser 可证性谓词** [@problem_id:2971569]。其定义为 $\mathrm{Prv}_R(x) \equiv \exists y (\mathrm{Proof}_T(y, x) \land \forall z  y, \neg \mathrm{Proof}_T(z, \ulcorner \neg x \urcorner))$。这个谓词断言“存在一个 $x$ 的证明，并且不存在一个哥德尔数更小的关于 $\neg x$ 的证明”。在一致的理论中，这个谓词与标准谓词[外延](@entry_id:161930)等价。然而，它不满足 D2。D2 的证明依赖于能够将 $\varphi \to \psi$ 的证明和 $\varphi$ 的证明拼接成一个 $\psi$ 的证明。虽然我们可以构造出 $\psi$ 的证明，但我们无法在 $T$ 中保证这个新构造出的证明仍然满足 Rosser 条件——即，它比所有可能的 $\neg \psi$ 的证明都要“小”。这个“最小性”条件在[肯定前件式](@entry_id:268205)下无法被内在地保持。

-   **一个失败 D3 的谓词**：Rosser 谓词同样也失败 D3 [@problem_id:2971581]。D3 的证明依赖于一个从 $\varphi$ 的证明到 $\mathrm{Prov}_T(\ulcorner \varphi \urcorner)$ 的证明的统一构造过程。对于 Rosser 谓词，这意味着从一个满足 Rosser 条件的 $\varphi$ 的证明，我们需要构造一个同样满足 Rosser 条件的 $\mathrm{Prv}_R(\ulcorner \varphi \urcorner)$ 的证明。这个构造过程会产生一个哥德尔数很大的新证明，我们无法在 $T$ 内部保证这个新证明相对于其否定的所有可能证明是“最小的”。另一个更简单的例子是“偶数证明谓词” $\mathrm{Prv}_{\text{even}}(x) \equiv \exists y (\mathrm{Proof}_T(y, x) \land \mathrm{Even}(y))$。我们无法保证从一个偶数编码的证明出发，构造出的新证明其编码仍然是偶数。

这些例子清晰地表明，HBL 可证性条件，尤其是 D2 和 D3，深刻地依赖于标准可证性谓词纯粹的 $\Sigma_1$ 结构。任何附加的、在证明构造过程中无法被形式系统证明其得以保持的条件，都可能破坏这些关键性质。

### [哥德尔第二不完备性定理](@entry_id:149390)再探

有了满足 HBL 条件的标准可证性谓词 $\mathrm{Prov}_T(x)$，我们就可以精确地陈述并证明**[哥德尔第二不完备性定理](@entry_id:149390)**。

首先，我们定义理论 $T$ 的**一致性陈述** (consistency statement) $\mathrm{Con}(T)$：
$$
\mathrm{Con}(T) \equiv \neg \mathrm{Prov}_T(\ulcorner 0=1 \urcorner)
$$
这个算术句子断言“句子 $0=1$ 在 $T$ 中是不可证的”，这是对 $T$ 不会推导出矛盾的直接形式化表达。

**[哥德尔第二不完备性定理](@entry_id:149390)**：如果一个递归公理化的理论 $T$ 包含了足够强的算术（如 PA），并且是一致的，那么 $T$ 无法证明其自身的一致性。形式化地：
$$
\text{若 } T \text{ 是一致的，则 } T \nvdash \mathrm{Con}(T)
$$

让我们来分析 $\mathrm{Con}(T)$ 这个句子 [@problem_id:2971573]。由于 $\mathrm{Prov}_T(x)$ 是 $\Sigma_1$ 公式，它的否定 $\neg \mathrm{Prov}_T(x)$ 就是一个 $\Pi_1$ **公式**。因此，$\mathrm{Con}(T)$ 是一个 $\Pi_1$ 句子。如果我们相信 $T$（比如 PA）是一致的，那么在标准模型 $\mathbb{N}$ 中就不存在 $0=1$ 的证明，所以 $\mathrm{Con}(T)$ 是一个**真**的 $\Pi_1$ 句子。[哥德尔第二不完备性定理](@entry_id:149390)告诉我们，尽管 $\mathrm{Con}(T)$ 是真的，但 $T$ 本身却无法证明它。这提供了一个具体的例子，反驳了“一个足够强的理论能证明所有真的算术陈述”这一幼稚的信念，甚至是对看似更弱的“能证明所有真的 $\Pi_1$ 陈述”这一信念的反驳。

第二不[完备性定理](@entry_id:151598)可以被看作是第一不[完备性定理](@entry_id:151598)的一个推论。第一不[完备性定理](@entry_id:151598)的证明（即哥德尔句子 $G_T$ 的不可证性）本身是纯粹的句法和算术论证，因此它可以在 $T$ 内部被形式化。这个形式化的论证证明了蕴含式 $\mathrm{Con}(T) \to G_T$。直观上，它说的是“如果理论是一致的，那么哥德尔句子是不可证的”，而哥德尔句子本身就断言自己不可证，所以它应该是真的。如果 $T$ 能够证明 $\mathrm{Con}(T)$，那么通过[肯定前件式](@entry_id:268205)，它就能证明 $G_T$。但这与第一不[完备性定理](@entry_id:151598)（在 $T$ 一致的前提下，$T \nvdash G_T$）相矛盾。因此，唯一的结论是 $T$ 无法证明 $\mathrm{Con}(T)$。

### Löb 定理与可证性逻辑

HBL 条件不仅能推导出[哥德尔第二不完备性定理](@entry_id:149390)，还能揭示一个更深刻、更令人惊讶的关于[自指](@entry_id:153268)和可证性的结果——**Löb 定理**。

一个非常自然的想法是，一个可靠的理论应该“信任”自己的证明。也就是说，如果 $T$ 能证明 $\varphi$，那么 $\varphi$ 应该是真的。这个想法可以被形式化为一个**反射模式** (reflection schema)：$\mathrm{Prov}_T(\ulcorner \varphi \urcorner) \to \varphi$。我们可能会期望一个一致的理论 $T$ 能够证明这个模式的所有实例。

然而，Löb 在 1955 年证明了事实并非如此。他提出了一个惊人的问题：对于哪些句子 $\varphi$，理论 $T$ 能够证明它自己的[反射原理](@entry_id:148504) $\mathrm{Prov}_T(\ulcorner \varphi \urcorner) \to \varphi$？答案出人意料地简单而深刻。

**Löb 定理**：对于任何句子 $\varphi$， $T \vdash \mathrm{Prov}_T(\ulcorner \varphi \urcorner) \to \varphi$ 当且仅当 $T \vdash \varphi$。 [@problem_id:2971582] [@problem_id:2971596]

这个定理的“仅当”部分是微不足道的：如果 $T$ 已经证明了 $\varphi$，那么根据[经典逻辑](@entry_id:264911)，$T$ 当然能证明任何形如 $A \to \varphi$ 的句子。真正的力量在于“当”这个方向：一个理论 $T$ 能够证明关于某个句子 $\varphi$ 的[反射原理](@entry_id:148504)的**唯一情况**是，它已经有了一个直接的 $\varphi$ 的证明！

Löb 定理的推论是深远的：
-   对于任何尚未被 $T$ 证明的猜想（比如[哥德巴赫猜想](@entry_id:187293)，记作 $\varphi$），$T$ 也**无法**证明蕴含式 $\mathrm{Prov}_T(\ulcorner \varphi \urcorner) \to \varphi$。换句话说，你不能绕过对 $\varphi$ 的[直接证明](@entry_id:141172)，而试图先证明“如果 $\varphi$ 可证，那它就是真的”。

-   Löb 定理提供了一个极其简洁的[哥德尔第二不完备性定理](@entry_id:149390)的证明。令 $\varphi$ 为一个矛盾句（例如 $0=1$，记作 $\bot$）。Löb 定理的一个实例是：$T \vdash \mathrm{Prov}_T(\ulcorner \bot \urcorner) \to \bot$ 当且仅当 $T \vdash \bot$。左边的蕴含式 $\mathrm{Prov}_T(\ulcorner \bot \urcorner) \to \bot$ 在逻辑上等价于 $\neg \mathrm{Prov}_T(\ulcorner \bot \urvenir)$，也就是 $\mathrm{Con}(T)$。因此，Löb 定理表明 $T \vdash \mathrm{Con}(T)$ 当且仅当 $T \vdash \bot$。由于一个一致的理论 $T$ 满足 $T \nvdash \bot$，我们立即得到 $T \nvdash \mathrm{Con}(T)$ [@problem_id:2971573]。

-   理论 $T$ 也无法证明关于其自身一致性陈述的[反射原理](@entry_id:148504)，即 $T \nvdash \mathrm{Prov}_T(\ulcorner \mathrm{Con}(T) \urcorner) \to \mathrm{Con}(T)$。如果它可以，根据 Löb 定理，它就必须能证明 $\mathrm{Con}(T)$，而这是不可能的 [@problem_id:2971582]。

值得注意的是，Löb 定理是关于在 $T$ **内部可证性**的陈述。它并不排斥在[元理论](@entry_id:638043)中，或者在标准模型 $\mathbb{N}$ 中，[反射原理](@entry_id:148504)是**真**的。例如，如果一个理论 $T$ 是 $\Sigma_1$-可靠的（即它证明的每个 $\Sigma_1$ 句子都是真的），那么对于任何 $\Sigma_1$ 句子 $\sigma$，蕴含式 $\mathrm{Prov}_T(\ulcorner \sigma \urcorner) \to \sigma$ 在标准模型中都是真的。然而，这组无穷多的真句子（称为 $\Sigma_1$ 反射模式）作为一个整体，并不能在 $T$ 中被证明，因为它蕴含了 $\mathrm{Con}(T)$ [@problem_id:2971589]。这再次凸显了理论内部证明能力与外部真理之间的鸿沟。

### 可证性的[不动点](@entry_id:156394)：Gödel 与 Henkin

Löb 定理的证明本身就利用了**[对角引理](@entry_id:149289)** (Diagonal Lemma)，这是所有[自指](@entry_id:153268)悖论和不完备性结果的核心技术工具。[对角引理](@entry_id:149289)断言，对于算术语言中的任何一元公式 $\psi(x)$，都存在一个句子 $\sigma$，使得 $T \vdash \sigma \leftrightarrow \psi(\ulcorner \sigma \urcorner)$。这个句子 $\sigma$ 是谓词 $\psi$ 的一个**[不动点](@entry_id:156394)**。

哥德尔的第一不[完备性定理](@entry_id:151598)正是通过为谓词 $\neg \mathrm{Prov}_T(x)$ 构造一个[不动点](@entry_id:156394)而产生的。这个[不动点](@entry_id:156394)，即**哥德尔句子** $G_T$，满足：
$$
T \vdash G_T \leftrightarrow \neg \mathrm{Prov}_T(\ulcorner G_T \urcorner)
$$
$G_T$ 实际上是在说：“我自身在理论 $T$ 中是不可证的”。第一不[完备性定理](@entry_id:151598)表明，如果 $T$ 是一致的，那么 $G_T$ 确实是不可证的。

现在，一个自然的问题是：如果我们为可证性谓词 $\mathrm{Prov}_T(x)$ 本身构造一个[不动点](@entry_id:156394)会发生什么？[对角引理](@entry_id:149289)保证存在这样一个句子，我们称之为**Henkin 句子** $\theta_T$，它满足：
$$
T \vdash \theta_T \leftrightarrow \mathrm{Prov}_T(\ulcorner \theta_T \urcorner)
$$
这个句子 $\theta_T$ 实际上是在说：“我自身在理论 $T$ 中是可证的”。

这个句子的命运是什么？它可证吗？不可证吗？还是独立的？Löb 定理给出了一个直接而优雅的答案 [@problem_id:2971596]。
Henkin 句子的定义 $T \vdash \theta_T \leftrightarrow \mathrm{Prov}_T(\ulcorner \theta_T \urcorner)$ 蕴含了 $T \vdash \mathrm{Prov}_T(\ulcorner \theta_T \urvenir) \to \theta_T$。这恰好是 Löb 定理的**前提**（当 $\varphi = \theta_T$ 时）。因此，我们可以立即应用 Löb 定理的结论，得到：
$$
T \vdash \theta_T
$$
这是一个令人惊叹的结果。与断言自身不可证的哥德尔句子（它是不可证的）形成鲜明对比，断言自身可证的 Henkin 句子恰恰是**可证的**。这种对称性揭示了可证性逻辑的深刻内在结构。一个理论不能断言自己的[无能](@entry_id:201612)（不可证性），但可以成功地断言自己的能力（可证性）。

重要的是，Henkin 句子的可证性与 $T$ 的一致性完全兼容，并且它并不意味着 $T$ 可以证明其自身的一致性 [@problem_id:2971596]。这再次表明，尽管[形式系统](@entry_id:634057)存在着深刻的局限性（如哥德尔定理所示），但它们内部的逻辑结构远比我们最初想象的要丰富和微妙。