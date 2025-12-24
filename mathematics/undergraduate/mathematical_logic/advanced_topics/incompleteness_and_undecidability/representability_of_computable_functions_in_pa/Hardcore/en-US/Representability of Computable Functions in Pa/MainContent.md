## Introduction
The relationship between abstract computation and formal logical proof stands as one of the most significant discoveries in modern mathematics. At its heart is a profound question: how can a formal system of arithmetic, with its simple rules for manipulating symbols, talk about the sophisticated processes of algorithms and even its own structure? This capacity, known as representability, bridges the gap between the world of numbers and the world of syntax, providing the engine for Kurt Gödel's revolutionary incompleteness theorems. This article delves into this critical concept, exploring the technical machinery that allows a theory like Peano Arithmetic (PA) to formally express and prove facts about any computable function.

Across three chapters, we will unravel the theory and application of representability. The journey begins with **Principles and Mechanisms**, where we will formally define representability, introduce the necessary tools like [arithmetization](@entry_id:268283) and the [arithmetical hierarchy](@entry_id:155689), and demonstrate how a representing formula can be constructed for any computable function. Following this, the chapter on **Applications and Interdisciplinary Connections** will showcase the power of this concept, detailing its role in proving the limitative theorems of Gödel and Tarski and forging deep connections with [computability theory](@entry_id:149179) and computer science. Finally, **Hands-On Practices** will offer a series of guided problems to translate these abstract ideas into concrete skills, from arithmetizing a simple computation to understanding the proof that all [primitive recursive functions](@entry_id:155169) are representable.

## Principles and Mechanisms

The capacity of a formal system like Peano Arithmetic (PA) to discuss its own syntax and prove facts about computation is one of the most profound discoveries of modern logic. This capability, known as [arithmetization](@entry_id:268283), hinges on the ability to represent [computable functions](@entry_id:152169) within the theory itself. This chapter elucidates the principles and mechanisms that make such representation possible, exploring the bridge between the semantic world of numbers and functions and the syntactic world of formal proofs.

### The Language of Arithmetic and Numerals

To understand how a formal theory can speak about numbers, we must first be precise about its language. Peano Arithmetic is a first-order theory whose language, denoted $\mathcal{L}_{\mathrm{PA}}$, is built upon a simple yet powerful signature. The non-logical symbols of $\mathcal{L}_{\mathrm{PA}}$ are:

- A constant symbol: $0$ (zero)
- A unary function symbol: $S$ (the successor function)
- Two binary function symbols: $+$ (addition) and $\cdot$ (multiplication)

The underlying logic is standard [first-order logic](@entry_id:154340) with equality ($=$). From these symbols, terms are constructed inductively. For instance, $S(0)$, $S(S(0))$, and $(S(0) + S(S(0)))$ are all terms in the language.

A critical component of this framework is the system of **numerals**. For each natural number $n \in \mathbb{N}$ in our [meta-theory](@entry_id:638043), we define a corresponding canonical term in $\mathcal{L}_{\mathrm{PA}}$, denoted $\overline{n}$. These numerals are defined inductively:
- $\overline{0}$ is the term $0$.
- $\overline{n+1}$ is the term $S(\overline{n})$.

Thus, $\overline{1}$ is $S(0)$, $\overline{2}$ is $S(S(0))$, and so on. This systematic naming convention provides a direct and unambiguous way for the formal theory of arithmetic to refer to each specific natural number. This ability to name numbers internally is not merely a convenience; it is an indispensable prerequisite for the entire project of [arithmetization](@entry_id:268283). To express syntactic properties of the theory within the theory itself—the essence of Gödel's method—we must first assign numerical codes (Gödel numbers) to symbols, formulas, and proofs. To reason about these codes within PA, we must have a way to refer to them, which is precisely the role fulfilled by the numerals.

### Defining Representability

With a system of numerals in place, we can formally define what it means for the theory PA to capture the behavior of relations and functions on the [natural numbers](@entry_id:636016). It is crucial to distinguish the syntactic notion of **representability** from the semantic notion of **definability**.

#### Definability in the Standard Model

A relation $R \subseteq \mathbb{N}^k$ is **definable** in the [standard model](@entry_id:137424) of arithmetic, $\mathbb{N}$, if there exists a formula $\varphi(x_1, \dots, x_k)$ in $\mathcal{L}_{\mathrm{PA}}$ such that for any tuple of [natural numbers](@entry_id:636016) $(n_1, \dots, n_k)$:
$$ R(n_1, \dots, n_k) \text{ is true} \quad \iff \quad \mathbb{N} \models \varphi(\overline{n_1}, \dots, \overline{n_k}) $$
Definability is a statement about *truth* in a specific interpretation (the [standard model](@entry_id:137424)). It simply asserts that the formula $\varphi$ correctly partitions the tuples of numbers according to whether they belong to the relation $R$.

#### Representability in Peano Arithmetic

Representability, by contrast, is a much stronger, syntactic condition based on **provability** within the formal system PA.

A relation $R \subseteq \mathbb{N}^k$ is **represented** (or strongly represented) in PA by a formula $\varphi(x_1, \dots, x_k)$ if for every tuple of [natural numbers](@entry_id:636016) $(n_1, \dots, n_k)$:
1. If $R(n_1, \dots, n_k)$ is true, then $\mathrm{PA} \vdash \varphi(\overline{n_1}, \dots, \overline{n_k})$.
2. If $R(n_1, \dots, n_k)$ is false, then $\mathrm{PA} \vdash \neg\varphi(\overline{n_1}, \dots, \overline{n_k})$.

Here, $\mathrm{PA} \vdash \psi$ signifies that the sentence $\psi$ is a theorem of Peano Arithmetic. These two conditions are known as the requirements of **numeralwise correctness**. They demand that PA can *formally prove* the correctness of the formula for every single instance.

Definability does not imply representability. For example, let $G$ be a true but unprovable sentence of PA (the existence of which is guaranteed by Gödel's First Incompleteness Theorem). Consider the simple function $f(x)=0$ and the formula $\psi(x, y) \equiv (y=\overline{0} \land G)$. In the [standard model](@entry_id:137424) $\mathbb{N}$, $G$ is true, so $\psi(x, y)$ is true if and only if $y=0$. Thus, $\psi$ *defines* the graph of $f$. However, to represent $f$, PA would need to prove $\psi(\overline{n}, \overline{0})$ for any $n$. This would require PA to prove $G$, which it cannot do. Hence, $\psi$ defines $f$ but does not represent it.

The concept of representability extends naturally from relations to functions by considering the function's graph. A total function $f: \mathbb{N}^k \to \mathbb{N}$ is **represented** in PA by a formula $\varphi(\vec{x}, y)$ if the formula represents the graph of the function, $G_f = \{(\vec{n}, m) \mid f(\vec{n})=m\}$, and furthermore, PA can prove that for every input, the output exists and is unique. This is typically captured by requiring that for every $\vec{n} \in \mathbb{N}^k$:
$$ \mathrm{PA} \vdash \exists!y \, \varphi(\overline{\vec{n}}, y) $$
This condition of instance-wise provable totality and uniqueness is the crucial link from the representability of a relation to the representability of a function.

A powerful consequence of this definition relates syntax to semantics. By the Soundness Theorem of [first-order logic](@entry_id:154340), any statement provable in PA must be true in every model of PA. This includes nonstandard models, which contain "infinite" numbers alongside the standard ones. Because representability ensures PA proves $\forall y(\varphi(\overline{n}, y) \leftrightarrow y=\overline{f(n)})$, this statement must hold in any model $M$. Therefore, for any standard input $\overline{n}$, the unique element satisfying the representing formula in any model $M$ must be the standard element $\overline{f(n)}$. The formal power of representation thus guarantees that computations on standard numbers are immune to any potential interference from nonstandard elements.

### The Engine of Representability: Arithmetizing Computation

The central question is: which functions are representable in PA? The astonishing answer is that the class of representable functions is precisely the class of **[computable functions](@entry_id:152169)**. To demonstrate this, we must show how to construct a representing formula for any given computable function.

#### The Arithmetical Hierarchy

The construction of these formulas relies on classifying them according to their logical complexity. This gives rise to the **[arithmetical hierarchy](@entry_id:155689)**. At its base are the **$\Delta_0$ formulas**, which are formulas where all [quantifiers](@entry_id:159143) are **bounded**, i.e., of the form $\forall x \le t$ or $\exists x \le t$, where $t$ is a term. Relations defined by $\Delta_0$ formulas are computationally very simple.

The next levels are built upon this base:
- A formula is **$\Sigma_1$** if it is of the form $\exists x_1 \dots \exists x_k \, \psi$, where $\psi$ is a $\Delta_0$ formula.
- A formula is **$\Pi_1$** if it is of the form $\forall x_1 \dots \forall x_k \, \psi$, where $\psi$ is a $\Delta_0$ formula.

These classes have deep connections to [computability theory](@entry_id:149179), established by Post's Theorem:
- A relation is **[computably enumerable](@entry_id:155267) (c.e.)** if and only if it is definable by a $\Sigma_1$ formula.
- A relation is **computable (decidable)** if and only if it is definable by both a $\Sigma_1$ formula and a $\Pi_1$ formula (making it **$\Delta_1$**).

#### Constructing Representing Formulas

The proof that every computable function is representable is constructive. It proceeds by "arithmetizing" the process of computation. For any computable function $f$, there exists a Turing machine (or equivalent formal [model of computation](@entry_id:637456)) that computes it. A computation for a given input $\vec{n}$ is a finite sequence of configurations. The key insight, due to Gödel, is that any finite sequence of numbers can be encoded by a single natural number.

Using Gödel's $\beta$-function, a primitive recursive device, we can encode a full computation history—a sequence of machine states—as a single number, let's call it $s$. The property "$s$ encodes a valid computation of function $f$ on input $\vec{x}$ that halts with output $y$" can then be checked with a formula. This check involves verifying:
1. The initial configuration in the sequence encoded by $s$ is correct.
2. Each subsequent configuration follows from the previous one according to the machine's transition rules.
3. The final configuration is a halting state, and the output is $y$.

Crucially, all these checks can be formulated using only bounded quantifiers, because they only involve inspecting parts of the finite sequence encoded by $s$. This means the entire condition can be expressed by a $\Delta_0$ formula, which we can call $\theta(\vec{x}, y, s)$.

The graph of the function $f$, the relation $f(\vec{x}) = y$, can now be defined by the assertion that *there exists* such a computation code:
$$ \varphi_f(\vec{x}, y) \equiv \exists s \, \theta(\vec{x}, y, s) $$
By its very structure, this is a $\Sigma_1$ formula. This demonstrates that the graph of any computable function is $\Sigma_1$-definable.

### The Main Theorem and Its Limitations

With the constructive mechanism in place, we can state the main result and explore its profound limits.

#### Representability of Computable Functions

The fundamental theorem is that a function is representable in PA if and only if it is computable. The proof sketch above gives the direction from computable to representable. It relies on a key property of Peano Arithmetic: **$\Sigma_1$-completeness**. PA is strong enough to prove every true $\Sigma_1$ sentence. Since for any computation $f(\vec{n}) = m$, the statement $\exists s \, \theta(\overline{\vec{n}}, \overline{m}, s)$ is a true $\Sigma_1$ sentence, it is provable in PA. PA is also strong enough to formalize a proof of uniqueness for each instance, thus fulfilling the conditions for representability.

#### The Limit: Provable Totality

This leads to a subtle but critical question. We know that for any *specific* standard number $n$, PA proves $\exists y \, \varphi_f(\overline{n}, y)$. Does this imply that PA can prove the single, universally quantified sentence asserting the function's totality?
$$ \forall x \, \exists y \, \varphi_f(x, y) $$
The answer is no. While we can prove totality for each instance, we cannot necessarily prove the general principle. The reason lies in the logical complexity of the totality statement. Since $\varphi_f(x, y)$ is a $\Sigma_1$ formula, the statement $\forall x \, \exists y \, \varphi_f(x, y)$ is a **$\Pi_2$ sentence**.

Gödel's Incompleteness Theorems imply that PA is not $\Pi_2$-complete; there are true $\Pi_2$ sentences that are unprovable in PA. It is possible to construct a total computable function $f$ whose totality is equivalent to a known true-but-unprovable statement (such as the consistency of PA, Con(PA)). For such a function, the totality statement $\forall x \, \exists y \, \varphi_f(x, y)$ is true in the [standard model](@entry_id:137424) $\mathbb{N}$ but is not a theorem of PA.

This reveals the distinction between simple representability and **strong representability** (or provable totality). All total [computable functions](@entry_id:152169) are representable in PA. However, only a [proper subset](@entry_id:152276) of them—the **provably total recursive functions** of PA—are strongly representable.

This limitation has a clear model-theoretic explanation. If PA cannot prove the totality of $f$, then there must exist a nonstandard model $M$ of PA containing a nonstandard element $c$ for which the computation of $f(c)$ does not halt from the model's perspective, i.e., $M \models \neg\exists y \, \varphi_f(c,y)$. For standard inputs, however, the computation is always finite and has a standard code $t$. While a nonstandard model might also contain nonstandard codes $s$ for the same computation (e.g., padded with nonstandard amounts of junk data), the uniqueness of the *output* is secure, as this property is provable in PA.

An important positive result is that the class of **[primitive recursive functions](@entry_id:155169)**, a large and natural class of [computable functions](@entry_id:152169) including addition, multiplication, and exponentiation, is fully contained within the provably total recursive functions. For any primitive [recursive function](@entry_id:634992), its totality can be proven within PA by using the axiom of induction to mirror the function's own [recursive definition](@entry_id:265514).

In summary, Peano Arithmetic provides a remarkably powerful framework for formalizing computation. It can represent every computable function, proving every particular fact about its behavior. Yet, its vision is not absolute; it cannot prove the totality of every function it can compute, a limitation that perfectly illustrates the profound boundaries discovered by Gödel.