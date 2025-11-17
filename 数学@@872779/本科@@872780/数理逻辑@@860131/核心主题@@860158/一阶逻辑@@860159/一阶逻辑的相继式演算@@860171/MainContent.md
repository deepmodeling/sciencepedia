## 引言
在数学逻辑的宏伟殿堂中，形式化证明不仅是确立真理的基石，其自身的结构和属性也蕴含着深刻的洞见。然而，要精确分析证明的内在机制，我们需要一个比日常数学推理更精细的框架。正是在这一需求下，[Gerhard Gentzen](@entry_id:150492) 发展的[矢列演算](@entry_id:154229)（Sequent Calculus）应运而生，它以其独特的对称性和分析能力，成为了现代[证明论](@entry_id:151111)的核心支柱。

本文将系统性地引导您深入探索[一阶逻辑](@entry_id:154340)的[矢列演算](@entry_id:154229)。在第一章“原理与机制”中，我们将从矢列的基本构造和推演规则入手，逐步揭示其运作方式，并最终触及[证明论](@entry_id:151111)的顶峰——切削消除定理。随后的第二章“应用与跨学科联系”将展示该理论的强大实践价值，探讨它如何连接不同逻辑、驱动[自动定理证明](@entry_id:154648)，并为解决数学基础中的重大问题提供关键工具。最后，在“动手实践”部分，您将有机会通过解决具体问题，将理论知识转化为实际的证明构建和分析技能，从而真正掌握这一强大的逻辑工具。

## 原理与机制

在介绍了一阶逻辑的句法和语义之后，我们现在转向一个核心的[证明论](@entry_id:151111)工具：[矢列演算](@entry_id:154229)（Sequent Calculus）。由 [Gerhard Gentzen](@entry_id:150492) 在20世纪30年代发展的[矢列演算](@entry_id:154229)，为逻辑推理提供了一个极其精细和对称的框架。与自然演绎（Natural Deduction）等其他证明系统相比，[矢列演算](@entry_id:154229)的结构使其特别适合用于分析证明本身的属性，例如一致性和[可判定性](@entry_id:152003)。本章将深入探讨[矢列演算](@entry_id:154229)的基本原理和关键机制，从其推演规则到其最深刻的[元理论](@entry_id:638043)结果——切削消除定理。

### 矢列的构造与推演规则

[矢列演算](@entry_id:154229)的核心是**矢列（sequent）**这一概念。一个矢列具有如下形式：
$$ \Gamma \vdash \Delta $$
其中 $\Gamma$ 和 $\Delta$ 都是有限的公式集合（或多重集）。$\Gamma$ 被称为**前件（antecedent）**，$\Delta$ 被称为**后件（succedent）**。这个矢列的直观语义是：“$\Gamma$ 中所有公式的合取，蕴涵了 $\Delta$ 中所有公式的析取”。换言之，如果我们接受 $\Gamma$ 中的所有假设，那么至少有一个 $\Delta$ 中的结论必须成立。

一个形式化的证明，在[矢列演算](@entry_id:154229)中，是一个以**公理（axioms）**为叶节点，以目标矢列为根节点的推导树。树中的每一个节点都通过一个**推演规则（inference rule）**从其父节点（向上读）或子节点（向下读）得到。

#### 公理与结构规则

证明必须从某个地方开始。在[矢列演算](@entry_id:154229)中，最基本的出发点是**初始矢列（initial sequents）**或**[同一性公理](@entry_id:140517)（identity axioms）**。它们的形式为：
$$ A \vdash A $$
对于任何公式 $A$。其含义是显而易见的：假设 $A$ 成立，那么 $A$ 必然成立。这是所有逻辑推理的基石。

除了逻辑规则外，还有一组**结构规则（structural rules）**，它们不涉及任何[逻辑连接词](@entry_id:146395)，只管理矢列中公式的“位置和数量”。主要的结构规则包括：
*   **弱化规则（Weakening）**：允许在前件或后件中加入一个任意的公式。
    $$ \frac{\Gamma \vdash \Delta}{\Gamma, A \vdash \Delta} (\text{左弱化}) \quad \frac{\Gamma \vdash \Delta}{\Gamma \vdash \Delta, A} (\text{右弱化}) $$
    这表示如果一个结论可以从一组前提中得出，那么增加一个前提或一个可能的结论不会使该推导失效。
*   **缩约规则（Contraction）**：允许将前件或后件中两个相同的公式合并为一个。
    $$ \frac{\Gamma, A, A \vdash \Delta}{\Gamma, A \vdash \Delta} (\text{左缩约}) \quad \frac{\Gamma \vdash \Delta, A, A}{\Gamma \vdash \Delta, A} (\text{右缩约}) $$
*   **[交换规则](@entry_id:184421)（Exchange）**：允许改变前件或后件中公式的顺序。

这些规则确保了我们可以将前件和后件视为公式的集合，而不必过分关注它们的顺序或重复次数。

#### 逻辑规则

逻辑规则是[矢列演算](@entry_id:154229)的精髓，它们定义了每个[逻辑连接词](@entry_id:146395)和[量词](@entry_id:159143)的含义。每个连接词都有一对规则：一个用于在后件中引入它（右规则），一个用于在前件中引入它（左规则）。这种对称性是 Gentzen 设计的一大亮点。

以下是[经典逻辑](@entry_id:264911)（LK）中一些命题连接词的规则：
*   **合取（$\land$）**
    $$ \frac{\Gamma, A, B \vdash \Delta}{\Gamma, A \land B \vdash \Delta} (\land L) \quad \frac{\Gamma \vdash \Delta, A \quad \Gamma \vdash \Delta, B}{\Gamma \vdash \Delta, A \land B} (\land R) $$
    左规则（$\land L$）表明，要从合取式 $A \land B$ 推导出结论，等同于将 $A$ 和 $B$ 同时作为前提进行推导。右规则（$\land R$）表明，要证明 $A \land B$，必须分别证明 $A$ 和 $B$。
*   **析取（$\lor$）**
    $$ \frac{\Gamma, A \vdash \Delta \quad \Gamma, B \vdash \Delta}{\Gamma, A \lor B \vdash \Delta} (\lor L) \quad \frac{\Gamma \vdash \Delta, A, B}{\Gamma \vdash \Delta, A \lor B} (\lor R) $$
    请注意右规则（$\lor R$）的常见形式：要证明 $A \lor B$，只需证明 $A$ 或 $B$ 即可。这里的形式将 $A$ 和 $B$ 都放在后件中，其[语义等价](@entry_id:754673)于析取。
*   **蕴涵（$\to$）**
    $$ \frac{\Gamma \vdash \Delta, A \quad B, \Pi \vdash \Sigma}{\Gamma, \Pi, A \to B \vdash \Delta, \Sigma} (\to L) \quad \frac{\Gamma, A \vdash B, \Delta}{\Gamma \vdash A \to B, \Delta} (\to R) $$
    右规则（$\to R$）是[演绎定理](@entry_id:635762)的体现：要证明 $A \to B$，只需假设 $A$ 并从中证明 $B$。左规则（$\to L$）类似于假言推理（Modus Ponens）：如果我们有 $A \to B$，为了使用它，我们需要证明 $A$（第一个子目标），然后我们就可以假设 $B$ 成立了（第二个子目标）。

#### 证明的构建：一个实例

为了感受这些规则如何协同工作，我们来构建一个**无切削（cut-free）**证明。证明过程通常是**从下到上（bottom-up）**进行的，从要证明的目标矢列开始，逆向应用规则，直到所有分支都达到初始公理。

考虑证明以下重言式，这是一个蕴涵[传递性](@entry_id:141148)的例子 [@problem_id:3052306]：
$$ \vdash \left(((P \to Q) \land (Q \to R)) \land (R \to S)\right) \to (P \to S) $$
我们的目标是计算完成此证明所需的最少逻辑规则应用次数。

1.  根矢列的主连接词是 $\to$。唯一适用的规则是 $\to R$。这消耗了我们第一次逻辑规则应用。
    $$ \frac{((P \to Q) \land (Q \to R)) \land (R \to S) \vdash P \to S}{\vdash \left(((P \to Q) \land (Q \to R)) \land (R \to S)\right) \to (P \to S)} (\to R, 1) $$
2.  新的目标矢列的后件仍然是一个蕴涵式 $P \to S$。我们再次应用 $\to R$ 规则（第2次应用）。
    $$ \frac{P, ((P \to Q) \land (Q \to R)) \land (R \to S) \vdash S}{((P \to Q) \land (Q \to R)) \land (R \to S) \vdash P \to S} (\to R, 2) $$
3.  现在，我们需要处理前件中的复杂公式。最外层的连接词是 $\land$。我们应用 $\land L$ 规则（第3次应用）来分解它。
    $$ \frac{P, (P \to Q) \land (Q \to R), R \to S \vdash S}{P, ((P \to Q) \land (Q \to R)) \land (R \to S) \vdash S} (\land L, 3) $$
4.  前件中还有一个合取式 $(P \to Q) \land (Q \to R)$。我们再次应用 $\land L$（第4次应用）。
    $$ \frac{P, P \to Q, Q \to R, R \to S \vdash S}{P, (P \to Q) \land (Q \to R), R \to S \vdash S} (\land L, 4) $$
5.  至此，我们得到了矢列 $P, P \to Q, Q \to R, R \to S \vdash S$。所有公式都已被分解为原子命题或简单的蕴涵式。我们的目标是从前提中推导出 $S$。这需要我们依次“激活”这些蕴涵式。我们从 $P \to Q$ 开始，应用 $\to L$ 规则（第5次应用）。此规则将证明分支。
    $$ \frac{P, Q \to R, R \to S \vdash P, S \quad (\text{分支 1}) \qquad Q, P, Q \to R, R \to S \vdash S \quad (\text{分支 2})}{P, P \to Q, Q \to R, R \to S \vdash S} (\to L, 5) $$
    分支1，$P, Q \to R, R \to S \vdash P, S$，是一个公理，因为 $P$ 同时出现在前件和后件中。此分支关闭。我们只需关注分支2。
6.  在分支2中，我们现在有前提 $Q$。我们利用它来激活 $Q \to R$，再次应用 $\to L$ 规则（第6次应用）。
    $$ \frac{Q, P, R \to S \vdash Q, S \quad (\text{分支 2a}) \qquad R, Q, P, R \to S \vdash S \quad (\text{分支 2b})}{Q, P, Q \to R, R \to S \vdash S} (\to L, 6) $$
    分支2a，$Q, P, R \to S \vdash Q, S$，由于 $Q$ 的存在而是公理。我们继续处理分支2b。
7.  在分支2b中，我们有了前提 $R$。最后，我们使用 $R \to S$，应用 $\to L$ 规则（第7次应用）。
    $$ \frac{R, Q, P \vdash R, S \quad (\text{分支 2b-i}) \qquad S, R, Q, P \vdash S \quad (\text{分支 2b-ii})}{R, Q, P, R \to S \vdash S} (\to L, 7) $$
    这两个最终的分支都是公理（分别因为 $R$ 和 $S$）。所有分支都已关闭。

我们总共应用了 $2$ 次 $\to R$， $2$ 次 $\land L$ 和 $3$ 次 $\to L$ 规则，合计 $7$ 次。由于每一步都是分解公式所必需的，这个数字是最小的。这个例子生动地展示了无切削证明的**[解析性](@entry_id:140716)（analyticity）**：证明过程系统地分解目标公式，直到达到不言自明的公理。

### [经典逻辑](@entry_id:264911)与[直觉主义逻辑](@entry_id:152074)：后件的角色

Gentzen 的一个深刻洞见是，[经典逻辑](@entry_id:264911)与非经典的[直觉主义逻辑](@entry_id:152074)之间的根本差异，可以被一个简单的句法限制所捕获。

*   在**经典[矢列演算](@entry_id:154229)（LK）**中，后件 $\Delta$ 可以包含任意多个公式。
*   在**直觉主义[矢列演算](@entry_id:154229)（LJ）**中，后件被限制为最多只能包含一个公式。

这个看似微小的改动，却带来了深远的影响 [@problem_id:3052307]。

一个形如 $\Gamma \vdash A, B$ 的矢列在经典上意味着“如果 $\Gamma$ 成立，则 $A$ 或 $B$ 成立”。这种析取性的结论是经典推理的特征，例如，**[排中律](@entry_id:635086)（Law of Excluded Middle）**，即 $\vdash A \lor \neg A$。在 LK 中，这个矢列很容易证明：
$$
\frac{\frac{A \vdash A}{\vdash A, \neg A}(\neg R)}{\vdash A \lor \neg A}(\lor R)
$$
注意，中间步骤 $\vdash A, \neg A$ 的后件包含两个公式，这在 LK 中是允许的，但在 LJ 中是被禁止的。因此，在 LJ 中无法通过这种方式证明[排中律](@entry_id:635086)。事实上，对于任意公式 $\varphi$，$\vdash \varphi \lor \neg \varphi$ 在 LJ 中是不可证的。这就是 LJ 捕获直觉主义（或构造性）数学精神的方式：我们不能仅仅通过排除所有其他可能性来断言一个事物的存在，而必须给出一个构造性的证明。

这个后件限制还影响了结构规则。例如，右缩约规则 $ \frac{\Gamma \vdash A, A}{\Gamma \vdash A} $ 和右弱化规则 $ \frac{\Gamma \vdash \varphi}{\Gamma \vdash \varphi, \psi} $ 的前提或结论在 LJ 中都是不合法的矢列，因此这些规则在 LJ 中既不是基本规则，也不是可容许的（admissible）规则。

### 演算的核心：切削规则及其消除

到目前为止，我们只考虑了无切削的证明。然而，在数学实践中，我们经常使用一种更自然的推理方式，即证明并使用**引理（lemma）**。在[矢列演算](@entry_id:154229)中，这种思想被**切削规则（Cut Rule）**所捕获：
$$
\frac{\Gamma \vdash \Delta, A \quad A, \Pi \vdash \Sigma}{\Gamma, \Pi \vdash \Delta, \Sigma} (\text{Cut})
$$
切削规则表明，如果我们能从 $\Gamma$ 证明 $A$（以及其他可能的 $\Delta$），并且能用 $A$（以及 $\Pi$）来证明 $\Sigma$，那么我们就可以“切掉”中间公式 $A$，直接从 $\Gamma$ 和 $\Pi$ 证明 $\Sigma$。这个规则极其强大，使得证明可以模块化，大大缩短证明的长度。

然而，切削规则也有一个缺点：公式 $A$（**切削公式**）可以是任意复杂的，与最终结论 $\Gamma, \Pi \vdash \Delta, \Sigma$ 可能毫无关系。这破坏了我们之前观察到的解析性。一个带有切削的证明不再是一个简单的自上而下的分析过程。

Gentzen 最重要的贡献，即他的**Hauptsatz（[主定理](@entry_id:267632)）**或**切削消除定理（Cut-Elimination Theorem）**，表明切削规则在逻辑上是冗余的。该定理指出：

> **在 LK 和 LJ 中，任何使用切削规则的证明，都可以被有效地转换为一个不使用切削规则的、证明相同矢列的证明。**

换句话说，切削规则是**可容许的（admissible）** [@problem_id:3052307]。虽然它在实践中很有用，但在理论上不是必需的。

切削消除定理是[证明论](@entry_id:151111)的基石，它有几个至关重要的推论：
1.  **[子公式性质](@entry_id:156458)（Subformula Property）**：一个无切削证明中出现的所有公式，都是其最终结论（根矢列）中公式的子公式。这极大地限制了寻找证明的搜索空间，是自动化定理证明的基础。
2.  **一致性（Consistency）**：利用切削消除，我们可以轻易地证明逻辑系统的一致性。例如，要证明矛盾（即空矢列 $\vdash$）是不可导出的。如果 $\vdash$ 可导，那么根据切削消除，它必然有一个无切削证明。但检查所有无切削规则可以发现，没有一个规则可以从公理（非空）推导出空矢列。因此，矛盾不可导出，系统是一致的。

切削消除的证明本身是一个精妙的归纳论证。其核心思想是通过一系列**约简步骤（reduction steps）**，逐步降低切削的“复杂度”，直到它被完全消除。复杂度通常通过两个度量来衡量：切削公式的复杂度和切削规则在证明树中的高度。

让我们通过一个具体的例子来观察这个约简过程 [@problem_id:3052309]。假设我们定义一个公式的**秩（rank）**，$|\varphi|$，来衡量其复杂度（例如，原子公式的秩为1，每个连接词或量词使其子公式的秩之和加1）。现在，假设一个证明中有一个切削，其切削公式为：
$$ \chi = \forall x\,(P(x) \land (\neg Q \lor R)) $$
其中 $P, Q, R$ 是原子公式。我们可以计算出这个公式的秩：
*   $|Q|=1, |R|=1, |P(x)|=1$
*   $|\neg Q| = 1 + |Q| = 2$
*   $|\neg Q \lor R| = 1 + |\neg Q| + |R| = 1 + 2 + 1 = 4$
*   $|P(x) \land (\neg Q \lor R)| = 1 + |P(x)| + |\neg Q \lor R| = 1 + 1 + 4 = 6$
*   $|\chi| = |\forall x\,(P(x) \land (\neg Q \lor R))| = 1 + |P(x) \land (\neg Q \lor R)| = 1 + 6 = 7$

初始证明的**切削秩（cut-rank）**为7。切削消除的第一步是处理主连接词 $\forall$。这会将对 $\forall x A(x)$ 的切削替换为一个对其实例 $A(t)$ 的切削。在这个例子中，对 $\chi$ 的切削被替换为对以下公式的切削：
$$ \chi_1 = P(t) \land (\neg Q \lor R) $$
这个新切削公式的秩为 $|\chi_1|=6$，严格小于7。

接下来，我们对这个新的切削进[行约简](@entry_id:153590)。其主连接词是 $\land$。对 $A \land B$ 的切削通常被替换为两个更简单的切削：一个对 $A$，另一个对 $B$。因此，对 $\chi_1$ 的切削被替换为对以下两个公式的切削：
*   $\chi_2 = P(t)$
*   $\chi_3 = \neg Q \lor R$

我们计算这两个新切削公式的秩：$|\chi_2| = 1$，$|\chi_3| = 4$。经过这两步约简，原来的一个秩为7的切削被替换为两个新的切削，其秩分别为1和4。新证明的最大切削秩为 $\max(1, 4) = 4$，也严格小于之前的6。通过反复应用这样的约简步骤，最终所有切削都可以被消除。

### 应用与进阶主题

[矢列演算](@entry_id:154229)及其切削消除定理不仅是深刻的理论成果，也为连接不同逻辑系统和自动化推理等应用领域提供了强大的工具。

#### 连接不同逻辑：否定翻译

我们已经看到，[经典逻辑](@entry_id:264911)比[直觉主义逻辑](@entry_id:152074)更“强”（例如，它可以证明[排中律](@entry_id:635086)）。然而，这两种逻辑之间存在着深刻的联系。通过所谓的**否定翻译（Negative Translation）**，可以将任何经典的定理转换为一个在[直觉主义逻辑](@entry_id:152074)中可证的定理。

**哥德尔-根岑否定翻译（Gödel–Gentzen negative translation）**是其中最著名的一种。它将每个公式 $\varphi$ 映射到一个新公式 $N(\varphi)$。一个典型的定义如下 [@problem_id:3052311]：
*   原子公式 $A$：$N(A) := \neg \neg A$
*   $N(\varphi \land \psi) := N(\varphi) \land N(\psi)$
*   $N(\varphi \lor \psi) := \neg \neg (N(\varphi) \lor N(\psi))$
*   $N(\varphi \to \psi) := N(\varphi) \to N(\psi)$
*   $N(\forall x\,\varphi) := \forall x\, N(\varphi)$
*   $N(\exists x\,\varphi) := \neg \neg \exists x\, N(\varphi)$

这个翻译的核心思想是通过策略性地插入双重否定（$\neg\neg$）来模拟经典推理。在[直觉主义逻辑](@entry_id:152074)中，$\neg\neg A$ 比 $A$ 更弱，但它保留了 $A$ 的许多“经典”属性。

让我们分析一个具体的例子。考虑以下经典公式，它本质上是[排中律](@entry_id:635086)的 $n$ 次合取 [@problem_id:3052311]：
$$ \varphi_{n} := \bigwedge_{i=1}^{n} \exists x_{i}\,\Bigl( P_{i}(x_{i}) \lor \forall y\,\bigl(P_{i}(y)\to \bot\bigr) \Bigr) $$
这里的 $\forall y\,(P_i(y) \to \bot)$ 正是 $\neg P_i(y)$ 的一种写法，所以内部是 $\exists x_i (P_i(x_i) \lor \neg P_i(x_i))$ 的变体。让我们计算其翻译 $N(\varphi_n)$ 中否定符号 $\neg$ 的总数。

我们首先分析单个合取项 $\psi_i = \exists x_{i}\,( P_{i}(x_{i}) \lor \neg P_i(x_i) )$ 的翻译会引入多少个 $\neg$。
1.  原子公式 $P_i(x_i)$ 和 $P_i(y)$ 的翻译 $N(P_i(x_i))$ 和 $N(P_i(y))$ 各引入2个 $\neg$。
2.  $\bot$ 的翻译是自身，引入0个 $\neg$。
3.  $\neg P_i(y)$ 即 $P_i(y) \to \bot$。其翻译为 $N(P_i(y)) \to N(\bot)$，引入的 $\neg$ 数量为 $2 + 0 = 2$。
4.  $\forall y\,(P_i(y) \to \bot)$ 的翻译不额外增加 $\neg$，所以贡献仍为2个。
5.  析取 $P_{i}(x_{i}) \lor \neg P_i(y)$ 的翻译是 $\neg\neg(N(P_i(x_i)) \lor N(\neg P_i(y)))$。它自身引入2个 $\neg$，加上其子公式的贡献，总共是 $2 + 2 + 2 = 6$ 个 $\neg$。
6.  [存在量词](@entry_id:144554) $\exists x_i$ 的翻译 $N(\exists x_i (\dots))$ 是 $\neg\neg \exists x_i N(\dots)$。它自身引入2个 $\neg$，加上其作用域内的6个，总共是 $2 + 6 = 8$ 个 $\neg$。

因此，每个 $\psi_i$ 的翻译 $N(\psi_i)$ 包含8个否定符号。由于合取 $\land$ 的翻译不增加额外的否定，$\varphi_n$ 的翻译 $N(\varphi_n)$ 中否定符号的总数就是 $n$ 个子项的总和，即 $8n$。这个结果量化了将一个典型的经典原理嵌入到构造性框架中所付出的“句法代价”。

存在多种不同的否定翻译定义 [@problem_id:3052308]，但它们都共享相同的基本思想：通过增加否定来弥合[经典逻辑](@entry_id:264911)和[直觉主义逻辑](@entry_id:152074)之间的鸿沟。

#### 从证明到反驳：Herbrand 定理

[矢列演算](@entry_id:154229)，特别是其无切削形式，与[自动定理证明](@entry_id:154648)领域紧密相关。许多[自动推理](@entry_id:151826)系统不是直接构造证明，而是采用**反驳（refutation）**的方法。为了证明一个矢列 $\Gamma \vdash \Delta$ 是有效的，我们转而证明公式集合 $\Gamma \cup \{\neg \delta \mid \delta \in \Delta\}$ 是**不可满足的（unsatisfiable）**。

一阶逻辑的**Herbrand 定理**为这种方法提供了理论基础。它将[一阶逻辑](@entry_id:154340)的不[可满足性问题](@entry_id:262806)规约为了[命题逻辑](@entry_id:143535)的不[可满足性问题](@entry_id:262806)。其大致内容是：一个[量词](@entry_id:159143)已被消除（通过**[Skolem化](@entry_id:154933)**）的公式集合是不可满足的，当且仅当，从其**Herbrand域**（由公式中的常量和函数符号构成的所有项的集合）中抽取的有限个**基面实例（ground instances）**是命题上不可满足的。

让我们通过一个例子来理解这个过程 [@problem_id:3052315]。假设我们要证明以下矢列的有效性，其中 $m \geq 1$：
$$ \exists x\, P(x),\, \forall y\,(P(y) \to P(f(y))) \vdash \exists z\, P(f^{m}(z)) $$
这表达了一个简单的[归纳推理](@entry_id:138221)：如果某个属性 $P$ 对某个对象成立，并且 $P$ 会沿着函数 $f$ 传递，那么经过 $m$ 次 $f$ 的应用后，该属性仍然对某个对象成立。

为了通过反驳来证明它，我们考虑以下三个公式的集合是否不可满足：
1.  $\phi_1: \exists x\, P(x)$
2.  $\phi_2: \forall y\,(P(y) \to P(f(y)))$
3.  $\phi_3: \neg \exists z\, P(f^{m}(z))$, 等价于 $\forall z\, \neg P(f^{m}(z))$

首先，我们进行 **[Skolem化](@entry_id:154933)** 来消除[存在量词](@entry_id:144554)。$\phi_1$ 中的 $\exists x$ 被替换为一个新的Skolem常量 $c$。于是我们得到：
*   $S_1: P(c)$
*   $S_2: \forall y\,(P(y) \to P(f(y)))$
*   $S_3: \forall z\, \neg P(f^{m}(z))$

接下来，我们构建 Herbrand 域，即由常量 $c$ 和函数 $f$ 生成的所有基面项：$H = \{c, f(c), f(f(c)), \dots, f^k(c), \dots\}$。

Herbrand 定理告诉我们，上述集合 $\{S_1, S_2, S_3\}$ 不可满足，当且仅当存在一个由它们的基面实例组成的有限集合，该集合在命题层面上是矛盾的。我们的任务是找到导致矛盾所需的最少的 $S_2$ 的实例数量。

我们的推理链如下：
*   我们从 $S_1$ 的实例 $P(c)$ 出发。
*   为了从 $P(c)$ 推导出 $P(f(c))$，我们需要 $S_2$ 在 $y=c$ 处的实例：$P(c) \to P(f(c))$。
*   为了从 $P(f(c))$ 推导出 $P(f^2(c))$，我们需要 $S_2$ 在 $y=f(c)$ 处的实例：$P(f(c)) \to P(f^2(c))$。
*   ...
*   为了最终推导出 $P(f^m(c))$，我们需要一个从 $P(c)$ 开始，长度为 $m$ 的蕴涵链。这总共需要 $m$ 个 $S_2$ 的不同实例，即 $y$ 分别取值为 $c, f(c), \dots, f^{m-1}(c)$ 时的实例。

通过这 $m$ 个实例和初始事实 $P(c)$，我们可以得出结论 $P(f^m(c))$。

现在，我们来看 $S_3$。为了产生矛盾，我们需要 $\neg P(f^m(c))$。这可以通过将 $S_3$ 中的 $z$ 实例化为 $c$ 来得到：$\neg P(f^m(c))$。

这样，我们就找到了一个命题上矛盾的基面实例集合。这个集合包含了 $P(c)$、$\neg P(f^m(c))$ 以及 $m$ 个形式为 $P(f^k(c)) \to P(f^{k+1}(c))$ 的蕴涵式。如果缺少这 $m$ 个实例中的任何一个，推理链就会中断，我们就无法推导出 $P(f^m(c))$，也就无法与 $\neg P(f^m(c))$ 产生矛盾。因此，完成这个反驳证明所需的最少 $S_2$ 实例数量恰好是 $m$。

这个例子完美地展示了[证明论](@entry_id:151111)（[矢列演算](@entry_id:154229)中的证明长度）和[模型论](@entry_id:150447)（Herbrand展开的规模）之间的深刻联系，并揭示了[自动定理证明](@entry_id:154648)背后的计算原理。