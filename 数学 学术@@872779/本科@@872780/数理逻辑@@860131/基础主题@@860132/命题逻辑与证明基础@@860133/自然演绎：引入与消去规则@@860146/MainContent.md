## 引言
逻辑推理是人类智识的核心，但我们如何确保推理过程的每一步都是有效和严谨的？在寻求对这一问题的形式化回答中，自然演绎（Natural Deduction）提供了一个优雅而直观的答案。与依赖公理和外部[真值](@entry_id:636547)定义的系统不同，自然演绎旨在通过一套直接反映我们思维方式的规则——引入规则与排除规则——来捕捉逻辑的内在结构。它解决了如何从内部定义[逻辑联结词](@entry_id:146395)的意义，并使形式化证明更贴近数学和哲学论证的自然流程。

本文将系统地引导您进入自然演绎的世界。在“原理与机制”一章中，您将学习构建证明的基本构件：针对合取、蕴含、析取、否定及[量词](@entry_id:159143)的引入与排除规则，并理解假设管理的核心机制。接下来，在“应用与跨学科关联”一章中，我们将探讨这些规则的深远影响，从其哲学语义基础到与计算机科学中“证明即程序”的惊人同构。最后，通过“动手实践”部分，您将有机会运用所学知识，解决具体问题，加深对规则精确性的理解。

## 原理与机制

自然演绎（Natural Deduction）的精髓在于，[逻辑联结词](@entry_id:146395)的意义并非由真值表这类外部语义工具所定义，而是由其自身的**引入规则**（introduction rules）和**排除规则**（elimination rules）所内在地确定。引入规则规定了我们可以在何种充分条件下断言一个包含该联结词的复合公式；而排除规则则指明了当我们已经断言了这样一个复合公式后，可以如何使用它来推导出新的结论。这套规则系统共同构成了联结词的“操作性”定义。一个设计良好的自然演绎系统，其引入和排除规则之间应存在一种深刻的“和谐”（harmony）：排除规则的效力不应超出引入规则所赋予的意义。

自然演绎中的证明，是一个从前提（或临时假设）出发，通过一系列[推理规则](@entry_id:273148)的应用，最终达到结论的公式序列。与公理系统不同，自然演绎的核心机制是**假设的引入与解除**。这通常通过**子证明**（subproof）的结构来体现。为了理解这一点，我们可以将其与另一种[证明论](@entry_id:151111)框架——Gentzen风格的[相继式演算](@entry_id:154229)（sequent calculus）进行对比。在[相继式演算](@entry_id:154229)中，一个可推导性判断（judgment of derivability）显式地写为 $\Gamma \vdash A$ 的形式，其中 $\Gamma$ 是一个明确列出所有当前有效的、未被解除的假设的集合。证明的每一步都是对整个相继式（sequent）的变换。

然而，在Fitch风格的自然演绎中，证明是线性的，上下文 $\Gamma$ 是隐式的。我们不需在每一步都重复书写所有有效的假设。取而代之的是，通过子证明的范围界定（scoping）来追踪假设的依赖关系。当我们开启一个子证明时，我们引入一个**临时假设**（temporary assumption）。在该子证明范围内的所有推论都可以依赖于这个假设。当某个规则（如蕴含引入）应用并结束该子证明时，这个临时假设就被**解除**（discharged）了。这意味着，在该子证明之外，该假设及其仅依赖于它的推论都变得不再可用，但我们得到了一个不依赖于该假设的新结论。那些在整个证明开始时就给出的前提，以及在推导过程中引入但尚未被解除的假设，统称为**未解除的假设**（undischarged assumptions）。任何一行推论的有效性，都取决于所有包含它的范围内的未解除假设。这种通过范围和解除来管理假设的方式，被认为更接近数学家进行非形式化证明时的思维过程。[@problem_id:3047470]

### 命题联结词：构建推理的基石

我们首先考察[命题逻辑](@entry_id:143535)中的联结词。它们的规则直接体现了其逻辑功能。

#### 合取 (Conjunction: $\land$)：联合断言

合取联结词 $\land$ 的意义在于**联合断言**（joint assertion）。断言 $\varphi \land \psi$ 在语义上等价于同时断言 $\varphi$ 和 $\psi$。这一理念直接体现在其引入和排除规则中。[@problem_id:3047476]

**合取引入 ($\land$I)** 规则指出，要断言合取式 $\varphi \land \psi$，我们必须首先分别拥有 $\varphi$ 和 $\psi$ 的证明。换言之，我们需要两个前提来构造一个合取。

$$
\frac{\varphi \quad \psi}{\varphi \land \psi} \quad (\land\text{I})
$$

**合取排除 ($\land$E)** 规则则反映了联合断言的另一面：一旦我们拥有了合取式 $\varphi \land \psi$ 的断言，我们就有权从中分别提取出每一个合取项。因此，存在两个排除规则。

$$
\frac{\varphi \land \psi}{\varphi} \quad (\land\text{E}_1)
\qquad \text{and} \qquad
\frac{\varphi \land \psi}{\psi} \quad (\land\text{E}_2)
$$

这些规则构成了一个完美的整体：引入规则告诉我们如何“构建”合取，排除规则告诉我们如何“拆解”它，两者精确地对应了合取的语义。

#### 蕴含 (Implication: $\to$)：假设性推理

蕴含是自然演绎中最具特色的部分，因为它直接将**假设性推理**（hypothetical reasoning）的形式结构内化为一条[推理规则](@entry_id:273148)。

**蕴含引入 ($\to$I)**，也称为**条件证明**（Conditional Proof），是演绎的核心机制。要证明一个蕴含式 $A \to B$，我们进行一次“思想实验”：我们临时假设前提 $A$ 成立，然后在这个假设下，通过一系列推理，如果我们能够成功推导出结论 $B$，那么我们就完成了这个思想实验。此时，我们可以关闭这个子证明，并得出结论 $A \to B$。这个结论不再依赖于我们临时假设的 $A$——$A$ 被解除了。这个过程精确地捕捉了“如果A，那么B”的推理模式。[@problem_id:3047472]

$$
\frac{\begin{array}{c} [A]^1 \\ \vdots \\ B \end{array}}{A \to B} \quad (\to\text{I})^1
$$

在这里，$[A]^1$ 表示被标记为 1 的假设 $A$，规则下方的上标 1 表示该标记的假设被此规则的应用所解除。值得注意的是，推导 $B$ 的过程中可能还依赖于其他未解除的假设 $\Gamma$。在这种情况下，最终的结论 $A \to B$ 将依赖于 $\Gamma$。同时，规则允许**空洞解除**（vacuous discharge），即即使在推导 $B$ 的过程中并未使用假设 $A$，我们仍然可以应用此规则得到 $A \to B$。[@problem_id:3047472, solution snippet E]

**蕴含排除 ($\to$E)**，更为人熟知的名字是**[肯定前件式](@entry_id:268205)**（Modus Ponens）。它规定，如果我们有一个蕴含式 $A \to B$ 和它的前件 $A$，我们就可以断言其后件 $B$。

$$
\frac{A \to B \quad A}{B} \quad (\to\text{E})
$$

在使用此规则时，结论 $B$ 的依赖项是推导 $A \to B$ 和推导 $A$ 所需的未解除假设的并集。例如，如果 $A \to B$ 依赖于假设集 $\Gamma$，而 $A$ 依赖于假设集 $\Delta$，那么推导出的 $B$ 将依赖于 $\Gamma \cup \Delta$。[@problem_id:3047472, solution snippet C]

#### 析取 (Disjunction: $\lor$)：[分情况证明](@entry_id:270222)

析取 $\varphi \lor \psi$ 的语义是：至少有一个析取项为真。

**析取引入 ($\lor$I)** 规则直接反映了这一点。如果我们已经证明了 $\varphi$，那么 $\varphi \lor \psi$ 自然成立（不论 $\psi$ 是什么）。同理，如果我们有 $\psi$，$\varphi \lor \psi$ 也成立。因此，有两个引入规则。[@problem_id:3047478]

$$
\frac{\varphi}{\varphi \lor \psi} \quad (\lor\text{I}_1)
\qquad \text{and} \qquad
\frac{\psi}{\varphi \lor \psi} \quad (\lor\text{I}_2)
$$

**析取排除 ($\lor$E)** 规则形式化了强大的**[分情况证明](@entry_id:270222)**（Proof by Cases）方法。如果我们已知 $\varphi \lor \psi$ 成立，但我们不确定是哪一个析取项为真，我们可以分别考虑两种情况。我们开启两个子证明：在第一个子证明中，我们假设 $\varphi$ 成立，并推导出一个结论 $\chi$；在第二个子证明中，我们假设 $\psi$ 成立，并再次推导出**同一个结论** $\chi$。如果两种情况都能得到 $\chi$，那么无论最初是 $\varphi$ 还是 $\psi$ 为真，$\chi$ 都必然成立。此时，我们可以结束这两个子证明，并断言 $\chi$。

$$
\frac{\varphi \lor \psi \quad \begin{array}{c} [\varphi]^1 \\ \vdots \\ \chi \end{array} \quad \begin{array}{c} [\psi]^2 \\ \vdots \\ \chi \end{array}}{\chi} \quad (\lor\text{E})^{1,2}
$$

这条规则的**旁侧条件**（side condition）至关重要：两个子证明必须推导出完全相同的结论。如果在一个情况下推导出 $\chi$，而在另一个情况下推导出 $\theta$，我们不能仅凭 $\varphi \lor \psi$ 就断言 $\chi$ 或 $\theta$。这是因为，例如，如果实际上是 $\psi$ 为真，我们没有理由相信 $\chi$ 成立。[@problem_id:3047478]

#### 否定 (Negation: $\neg$) 与荒谬 (Absurdity: $\bot$)

在许多现代自然演绎系统中，否定不是一个基本联结词，而是通过一个特殊的原子命题——**荒谬**（$\bot$, Falsum）来定义。$\bot$ 代表一个逻辑矛盾。否定式 $\neg \varphi$ 被定义为 $\varphi \to \bot$ 的简写，即“$\varphi$ 蕴含着矛盾”。[@problem_id:3047487]

**否定引入 ($\neg$I)** 基于上述定义，其规则实际上是蕴含引入的一个特例。要证明 $\neg \varphi$（即 $\varphi \to \bot$），我们需要假设 $\varphi$ 并从中推导出 $\bot$。这就是经典的**[归谬法](@entry_id:276604)**（Reductio ad Absurdum）的其中一种形式。

$$
\frac{\begin{array}{c} [\varphi]^1 \\ \vdots \\ \bot \end{array}}{\neg \varphi} \quad (\neg\text{I})^1
$$

**否定排除 ($\neg$E)** 同样是蕴含排除的特例。从 $\varphi$ 和 $\neg \varphi$（即 $\varphi \to \bot$）出发，通过[肯定前件式](@entry_id:268205)，我们可以推导出 $\bot$。这条规则体现了**非矛盾律**（Principle of Non-Contradiction）。

$$
\frac{\varphi \quad \neg \varphi}{\bot} \quad (\neg\text{E})
$$

### 量词：对个体进行推理

将自然演绎从[命题逻辑](@entry_id:143535)扩展到一阶逻辑（FOL），需要引入处理[量词](@entry_id:159143)的规则。这引入了新的复杂性，特别是关于变量的处理。

#### 预备知识：变量、代换与捕获

在一阶逻辑的语言中，变量可以被量词**约束**（bound）或保持**自由**（free）。一个变量的出现，如果在某个量词（如 $\forall x$ 或 $\exists x$）的作用域内，且该变量就是[量词](@entry_id:159143)所作用的变量 $x$，则称这次出现是约束的。否则，它是自由的。一个公式的**[自由变量](@entry_id:151663)集**（set of free variables），记作 $FV(\varphi)$，是所有在 $\varphi$ 中至少有一次自由出现的变量的集合。例如，在公式 $\forall y \,(P(x) \land Q(y))$ 中，$x$ 是自由的，而 $y$ 是约束的。因此，$FV(\forall y \,(P(x) \land Q(y))) = \{x\}$。

**代换**（substitution）是将一个公式中某个变量的所有自由出现替换为一个项（term）的操作。我们将“在公式 $\varphi$ 中用项 $t$ 代换变量 $x$ 的自由出现”记作 $\varphi[t/x]$。这个操作必须小心处理，以避免**变量捕获**（variable capture）的问题。变量捕获是指，如果项 $t$ 中包含一个[自由变量](@entry_id:151663) $y$，而在代换后，$t$ 被置于一个约束 $y$ 的[量词](@entry_id:159143)（$\forall y$ 或 $\exists y$）的作用域内，那么 $t$ 中原本自由的 $y$ 就被意外地“捕获”了，从而改变了公式的原意。

为避免捕获，我们引入了**免捕获代换**（capture-avoiding substitution）的严格定义。在执行 $\varphi[t/x]$ 时，如果 $x$ 的某次自由出现位于某个[量词](@entry_id:159143) $Qy$ 的作用域内，且 $y \in FV(t)$，那么在代换之前，我们必须先对该量词的约束变量进行**重命名**。我们会选择一个“新鲜”的变量 $z$（$z$ 不在 $t$ 和 $\varphi$ 中自由出现），将 $Qy\,(\dots)$ 替换为 $\alpha$-等价的 $Qz\,(\dots[z/y]\dots)$，然后再执行代换。[@problem_id:3047465]

#### [全称量词](@entry_id:145989) (Universal Quantifier: $\forall$)：从任意到一般

**全称引入 ($\forall$I)**，也称作**全称概括**（Universal Generalization），旨在从一个个例的证明推广到一个普遍的结论。要证明 $\forall x\,\varphi(x)$，我们必须证明 $\varphi(a)$ 对于一个**任意的**（arbitrary）个体 $a$ 成立。个体 $a$ 的“任意性”通过一条关键的旁侧条件来保证：**本征变量条件**（eigenvariable condition）。该条件规定，参数 $a$（称为本征变量）不能在推导 $\varphi(a)$ 所依赖的任何未解除假设中自由出现。[@problem_id:3047471]

$$
\frac{\varphi(a)}{\forall x\,\varphi(x)} \quad (\forall\text{I})
$$
*旁侧条件：$a$ 不在 $\varphi(a)$ 的任何未解除假设中自由出现。*

违反此条件将导致谬误。例如，从前提 $P(a)$（“个体 $a$ 具有性质P”）出发，我们可以直接推导出 $P(a)$。如果此时允许应用 $\forall$I，我们就能得到 $\forall x\,P(x)$（“所有个体都具有性质P”），这显然是无效的推理。正是本征变量条件阻止了这种从特殊到一般的非法推广。[@problem_id:3047474]

**全称排除 ($\forall$E)**，也称作**全称例示**（Universal Instantiation），其思想是：如果一个性质对所有个体都成立，那么它必然对我们能用任意一个项 $t$ 指称的任何特定个体成立。

$$
\frac{\forall x\,\varphi(x)}{\varphi[t/x]} \quad (\forall\text{E})
$$
*旁侧条件：项 $t$ 对于变量 $x$ 在 $\varphi(x)$ 中是**自由的**（free for $x$ in $\varphi(x)$）。*

这里的“自由的”条件正是为了防止变量捕获。它要求在将 $t$ 代入 $\varphi(x)$ 后，$t$ 中的任何自由变量都不会被 $\varphi(x)$ 内部的量词所约束。[@problem_id:3047471]

#### [存在量词](@entry_id:144554) (Existential Quantifier: $\exists$)：见证与匿名

**存在引入 ($\exists$I)** 是最直观的量词规则。如果我们能为一个性质 $\varphi$ 找到一个**见证**（witness），即一个项 $t$，使得 $\varphi(t)$ 成立，那么我们就可以断言存在至少一个个体满足该性质。

$$
\frac{\varphi[t/x]}{\exists x\,\varphi(x)} \quad (\exists\text{I})
$$
这个规则是构造性的，它从一个具体的例子出发，断言存在性。[@problem_id:3047464, solution snippet C]

**存在排除 ($\exists$E)** 是另一条精巧的规则，它处理如何从一个存在性断言出发进行推理。如果我们知道 $\exists x\,\varphi(x)$，我们只知道“存在某个体满足 $\varphi$”，但我们不知道它的具体身份。因此，我们不能直接例示为一个我们已知的个体。规则允许我们开启一个子证明，并假设 $\varphi(a)$ 成立，其中 $a$ 是一个代表那个匿名见证的**新鲜**参数。如果我们能从这个假设出发，推导出一个不依赖于 $a$ 的任何具体信息的结论 $\psi$，那么这个结论 $\psi$ 就可以被认为是 $\exists x\,\varphi(x)$ 的一个有效推论。

$$
\frac{\exists x\,\varphi(x) \quad \begin{array}{c} [\varphi(a)]^1 \\ \vdots \\ \psi \end{array}}{\psi} \quad (\exists\text{E})^1
$$
*旁侧条件：*
1.  *本征变量 $a$ 不在 $\exists x\,\varphi(x)$、$\psi$ 以及推导 $\psi$ 所依赖的除 $\varphi(a)$ 之外的任何其他未解除假设中自由出现。*

第一条条件保证了 $a$ 的“新鲜性”（它不能是我们已经知道的某个个体）和结论的“独立性”（结论不能谈论这个我们虚构出来的 $a$）。例如，从 $\exists x\,P(x)$ 直接推导出 $P(c)$ 是错误的，因为我们强行给未知的见证赋予了一个特定的身份 $c$。[@problem_id:3047464, solution snippet B] [@problem_id:3047474] 第二条则防止了将这个见证与别的假设中的个体混淆。例如，从 $\exists x\,(P(x) \land R)$ 推导出 $R$ 是有效的，因为 $R$ 中不含 $a$。但从 $\exists x\,P(x)$ 和 $\forall x\,(P(x) \to Q(x))$ 推导出 $\forall x\,Q(x)$ 则是无效的，因为在子证明中推导出的 $Q(a)$ 中的 $a$ 是一个特定的（尽管未知）的个体，不具有全称概括所需的“任意性”。[@problem_id:3047464, solution snippets D, E]

### 逻辑谱系：极小、直觉与经典

自然演绎框架的强大之处在于其模块化。通过增删某些关于否定和矛盾的规则，我们可以构建出具有不同哲学基础和证明能力的逻辑系统。

**极小逻辑 (Minimal Logic)** 是最基础的系统。它只包含上文所述的 $\land, \lor, \to$ 的引入和排除规则，以及由 $\neg A \equiv A \to \bot$ 定义的否定规则（$\neg$I 和 $\neg$E）。在极小逻辑中，$\bot$ 只是一个普通的、不可被满足的命题，从 $\bot$ 本身我们不能推导出任何其他命题。

**[直觉主义逻辑](@entry_id:152074) (Intuitionistic Logic)** 在极小逻辑的基础上，增加了一条关于 $\bot$ 的强大规则——**爆炸律**（Principle of Explosion），也称为**任意推论**（Ex Falso Quodlibet, EFQ）或 $\bot$-排除。

$$
\frac{\bot}{A} \quad (\bot\text{E} \text{ or EFQ})
$$

这条规则规定，从一个矛盾可以推导出任何命题 $A$。这是[直觉主义逻辑](@entry_id:152074)与极小逻辑的关键区别。然而，[直觉主义逻辑](@entry_id:152074)仍然拒绝一些[经典逻辑](@entry_id:264911)的核心原则，如[排中律](@entry_id:635086)（$A \lor \neg A$）。

**[经典逻辑](@entry_id:264911) (Classical Logic)** 是最常见和最强大的逻辑系统。它可以从[直觉主义逻辑](@entry_id:152074)出发，通过添加任何一个与[排中律](@entry_id:635086)等价的公理或规则得到。常见的添加项包括：

-   **双重否定排除 (Double Negation Elimination, DNE):**
    $$
    \frac{\neg\neg A}{A} \quad (\neg\neg\text{E})
    $$

-   **强[归谬法](@entry_id:276604) (Reductio ad Absurdum, RAA):**
    $$
    \frac{\begin{array}{c} [\neg A]^1 \\ \vdots \\ \bot \end{array}}{A} \quad (\text{RAA})^1
    $$
    注意这与我们之前看到的 $\neg$I 不同，RAA 的结论是 $A$ 而不是 $\neg A$。

在[直觉主义逻辑](@entry_id:152074)的框架下，DNE 和 RAA 是可以相互推导的。添加其中任何一个，都会使整个系统获得完全的[经典逻辑](@entry_id:264911)证明力。这三个系统——极小、直觉、经典——形成了一个强度递增的谱系，而区分它们的正是它们如何处理矛盾和否定的核心机制。[@problem_id:3047468]