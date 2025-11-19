## Introduction
First-order logic stands as the universal language of modern mathematics and computer science, offering unparalleled expressive power to formalize complex theories. However, its expressiveness raises a crucial question: How can we move beyond intuitive arguments to mechanically verify logical truth and consequence? The answer lies in [formal proof systems](@entry_id:636313)—rigorous, syntactic engines for deduction. This article bridges the gap between the semantic notion of truth and the syntactic act of proving. We will embark on a structured exploration, beginning with the foundational "Principles and Mechanisms" of [proof systems](@entry_id:156272), where we will define the language of [first-order logic](@entry_id:154340) and survey the major deductive paradigms. Following this, the "Applications and Interdisciplinary Connections" chapter will illuminate how these formalisms drive progress in [automated reasoning](@entry_id:151826), [software verification](@entry_id:151426), and foundational mathematics. Finally, the "Hands-On Practices" section will offer practical exercises to ground these theoretical concepts in concrete problem-solving.

## Principles and Mechanisms

Having established the foundational importance of [first-order logic](@entry_id:154340), we now turn to the formal machinery that underpins its use. This chapter delves into the principles and mechanisms of first-order [proof systems](@entry_id:156272). We will begin by precisely defining the [syntax and semantics](@entry_id:148153) of the logical language itself, which provides the objects of our study—formulas—and the standard against which we measure truth—models. We will then introduce the crucial meta-logical concepts of [soundness and completeness](@entry_id:148267), which connect the syntactic world of proofs with the semantic world of truth. Finally, we will survey the major paradigms of deductive systems—Hilbert systems, Natural Deduction, Sequent Calculus, and Semantic Tableaux—examining the unique rules and philosophical approaches of each.

### Preliminaries: The Language of First-Order Logic

A [proof system](@entry_id:152790) is a formal apparatus for manipulating syntactic objects. To understand any such system, we must first have a rigorous and unambiguous definition of the language it operates upon. This involves two components: the syntax, which specifies how to form well-formed expressions, and the semantics, which specifies how to interpret them.

#### Syntax: Building Well-Formed Expressions

The vocabulary of a specific [first-order language](@entry_id:151821) is determined by its **signature**. A signature, denoted by $\Sigma$, specifies the non-logical symbols that give the language its [expressive power](@entry_id:149863) for a particular [domain of discourse](@entry_id:266125).

Formally, a **first-order signature** $\Sigma$ consists of a set $\mathcal{F}$ of function symbols and a set $\mathcal{R}$ of relation symbols. Crucially, each symbol is assigned a specific non-negative integer, its **arity**, which dictates how many arguments it must take. This is captured by an arity function, $\operatorname{ar}: \mathcal{F} \cup \mathcal{R} \to \mathbb{N}_0$. A symbol with arity $n$ is called an $n$-ary symbol. Constant symbols are a special case; they can be treated as a distinct set of symbols or, more elegantly, as function symbols of arity 0.

In addition to the signature-specific symbols, the language includes a fixed, countably infinite set of **variables** $\mathcal{V} = \{x, y, z, \dots\}$, [logical connectives](@entry_id:146395) (e.g., $\neg, \land, \lor, \to$), quantifiers ($\forall, \exists$), and punctuation. The equality symbol, $=$, is typically treated as a logical [binary relation](@entry_id:260596) symbol with a fixed interpretation.

With these building blocks, we can inductively define the two primary categories of expressions: terms and formulas.

The set of **$\Sigma$-terms** is the smallest set satisfying these rules:
1.  Every variable $v \in \mathcal{V}$ is a term.
2.  Every constant symbol $c$ (i.e., a function symbol with $\operatorname{ar}(c) = 0$) is a term.
3.  If $f \in \mathcal{F}$ is an $n$-ary function symbol ($n>0$) and $t_1, \dots, t_n$ are terms, then the string $f(t_1, \dots, t_n)$ is a term.

Terms are the "nouns" of our language; they are intended to denote objects in the [domain of discourse](@entry_id:266125).

The set of **$\Sigma$-formulas** is defined in two stages. First, we define **atomic formulas**, the most basic statements:
1.  If $R \in \mathcal{R}$ is an $n$-ary relation symbol and $t_1, \dots, t_n$ are terms, then $R(t_1, \dots, t_n)$ is an atomic formula.
2.  If $t_1$ and $t_2$ are terms, then $(t_1 = t_2)$ is an atomic formula.

Then, the set of all [well-formed formulas](@entry_id:636348) is the smallest set satisfying:
1.  Every atomic formula is a formula.
2.  If $\varphi$ and $\psi$ are formulas, then so are $\neg\varphi$, $(\varphi \land \psi)$, $(\varphi \lor \psi)$, and $(\varphi \to \psi)$.
3.  If $\varphi$ is a formula and $x \in \mathcal{V}$ is a variable, then $\forall x\,\varphi$ and $\exists x\,\varphi$ are formulas.

Formulas are the "sentences" of our language; they are intended to denote truth-values (true or false). The strict arity of symbols is what ensures that every term and formula has a unique [parse tree](@entry_id:273136). This property, known as **unique readability**, is fundamental, as it enables us to define semantics recursively and to prove properties of the language using [structural induction](@entry_id:150215) [@problem_id:2979676].

#### A Technical Aside: Substitution and Variable Capture

Before we can properly state the rules for quantifiers, we must address the delicate operation of substitution. Let $\varphi[t/x]$ denote the formula obtained by replacing every **free occurrence** of the variable $x$ in $\varphi$ with the term $t$. An occurrence of a variable is free if it is not bound by a quantifier.

A naive replacement can lead to a logical error known as **variable capture**. Consider the formula $\varphi \equiv \exists y (x \neq y)$, which states that there exists an object different from $x$. This is true in any domain with at least two elements. Suppose we substitute the term $t \equiv y$ for $x$. A naive substitution yields $\exists y (y \neq y)$, which is universally false. The free variable $y$ in the term $t$ has been "captured" by the [existential quantifier](@entry_id:144554), radically changing the formula's meaning.

To prevent this, we must define the condition under which a substitution is safe. We say a term $t$ is **free for** a variable $x$ in a formula $\varphi$ if and only if no free occurrence of $x$ in $\varphi$ lies within the scope of a quantifier $Qy$ where $y$ is a variable that appears in $t$ (i.e., $y \in \mathrm{FV}(t)$).

More formally, the [recursive definition](@entry_id:265514) of [capture-avoiding substitution](@entry_id:149148), $\varphi[t/x]$, proceeds as follows. It is straightforward for atomic formulas and Boolean connectives. The crucial case is for a quantified formula $Qy\,\psi$:
1.  If $y = x$, the substitution does nothing, as all occurrences of $x$ in $\psi$ are bound: $(Qx\,\psi)[t/x] = Qx\,\psi$.
2.  If $y \neq x$ and the variable $y$ is not in the term $t$ ($y \notin \mathrm{FV}(t)$), the substitution is safe: $(Qy\,\psi)[t/x] = Qy\,(\psi[t/x])$.
3.  If $y \neq x$ and $y \in \mathrm{FV}(t)$, we must rename the bound variable $y$ to avoid capture. We choose a fresh variable $z$ that does not appear in $\psi$ or $t$. The original formula $Qy\,\psi$ is logically equivalent to $Qz\,(\psi[z/y])$. We can now safely substitute into this equivalent formula: $(Qy\,\psi)[t/x] = Qz\,((\psi[z/y])[t/x])$.

This careful definition of substitution is essential for the soundness of quantifier rules in all standard [proof systems](@entry_id:156272) [@problem_id:2979696].

#### Semantics: Assigning Meaning

Syntax alone is just symbol manipulation. Semantics connects these symbols to mathematical reality. The standard approach for first-order logic is **Tarskian semantics**, which interprets formulas in mathematical structures.

For a given signature $\Sigma$, a **$\Sigma$-structure** (or model) $\mathcal{M}$ consists of:
1.  A non-[empty set](@entry_id:261946) $|\mathcal{M}|$, called the **domain** or universe of the structure.
2.  An **interpretation function** that assigns meaning to the non-logical symbols:
    -   For each constant symbol $c$, an element $c^{\mathcal{M}} \in |\mathcal{M}|$.
    -   For each $n$-ary function symbol $f$, a total function $f^{\mathcal{M}}: |\mathcal{M}|^n \to |\mathcal{M}|$.
    -   For each $n$-ary relation symbol $R$, a relation $R^{\mathcal{M}} \subseteq |\mathcal{M}|^n$.

To interpret formulas with free variables, we need a **variable assignment** (or environment) $s$, which is a function that maps each variable $v \in \mathcal{V}$ to an element $s(v) \in |\mathcal{M}|$.

The denotation of a term $t$ in a structure $\mathcal{M}$ under an assignment $s$, written $t^{\mathcal{M},s}$, is defined recursively:
-   If $t$ is a variable $x$, then $x^{\mathcal{M},s} = s(x)$.
-   If $t$ is a constant symbol $c$, then $c^{\mathcal{M},s} = c^{\mathcal{M}}$.
-   If $t$ is $f(t_1, \dots, t_n)$, then $t^{\mathcal{M},s} = f^{\mathcal{M}}(t_1^{\mathcal{M},s}, \dots, t_n^{\mathcal{M},s})$.

The core of Tarskian semantics is the **satisfaction relation**, $\mathcal{M}, s \models \varphi$, which means "$\varphi$ is true in structure $\mathcal{M}$ with assignment $s$". It is also defined recursively:
-   For an atomic formula $R(t_1, \dots, t_n)$: $\mathcal{M}, s \models R(t_1, \dots, t_n)$ if and only if $(t_1^{\mathcal{M},s}, \dots, t_n^{\mathcal{M},s}) \in R^{\mathcal{M}}$.
-   For equality: $\mathcal{M}, s \models t_1 = t_2$ if and only if $t_1^{\mathcal{M},s} = t_2^{\mathcal{M},s}$.
-   For [logical connectives](@entry_id:146395):
    -   $\mathcal{M}, s \models \neg\varphi$ iff it is not the case that $\mathcal{M}, s \models \varphi$.
    -   $\mathcal{M}, s \models \varphi \land \psi$ iff $\mathcal{M}, s \models \varphi$ and $\mathcal{M}, s \models \psi$. (And similarly for other connectives).
-   For quantifiers:
    -   $\mathcal{M}, s \models \forall x\,\varphi$ iff for every element $a \in |\mathcal{M}|$, we have $\mathcal{M}, s[x \mapsto a] \models \varphi$. Here, $s[x \mapsto a]$ is the assignment that is identical to $s$ except that it maps $x$ to $a$.
    -   $\mathcal{M}, s \models \exists x\,\varphi$ iff there exists some element $a \in |\mathcal{M}|$ such that $\mathcal{M}, s[x \mapsto a] \models \varphi$.

For example, consider a sentence $\psi = \forall x \, \exists y \, R(f(y), x)$ in a structure where the domain is $\mathbb{Z}$, $f^{\mathcal{M}}(n) = 2n+3$, and $R^{\mathcal{M}}$ is the "less than" relation $$. To check if $\mathcal{M} \models \psi$, we must ask: for every integer $a$, does there exist an integer $b$ such that $f^{\mathcal{M}}(b)  a$? This means $2b+3  a$, or $b  (a-3)/2$. Since for any integer $a$, one can always find an integer $b$ smaller than $(a-3)/2$, the sentence $\psi$ is true in this structure [@problem_id:2979666].

### The Core Meta-Logical Concepts

With the notions of syntax and semantics in place, we can define the central concepts that govern the relationship between proofs and truth.

**Semantic Entailment**: A set of formulas $\Gamma$ **semantically entails** a formula $\varphi$, written $\Gamma \models \varphi$, if every structure and assignment that makes all formulas in $\Gamma$ true also makes $\varphi$ true. Formally: for every structure $\mathcal{M}$ and assignment $s$, if $\mathcal{M}, s \models \gamma$ for all $\gamma \in \Gamma$, then $\mathcal{M}, s \models \varphi$. A formula $\varphi$ that is true in all structures (i.e., $\emptyset \models \varphi$) is called **valid** or a **tautology**.

**Syntactic Derivability**: Given a specific proof system $\mathcal{P}$, a **proof** of $\varphi$ from a set of premises $\Gamma$ is a finite sequence of formulas where each formula in the sequence is either an axiom of $\mathcal{P}$, a member of $\Gamma$, or follows from previous formulas in the sequence by one of the system's inference rules. If such a proof exists, we say $\varphi$ is **derivable** from $\Gamma$ in $\mathcal{P}$, written $\Gamma \vdash_{\mathcal{P}} \varphi$.

These two notions live in different worlds: $\models$ is about truth in all possible models, while $\vdash$ is about syntactic manipulation according to fixed rules. The goal of a proof system is to bridge this gap. This is captured by the two most important meta-logical properties a proof system can have: soundness and completeness [@problem_id:2979684].

-   A proof system $\mathcal{P}$ is **sound** if it only proves things that are semantically true. That is, for any $\Gamma$ and $\varphi$:
    $$ \text{If } \Gamma \vdash_{\mathcal{P}} \varphi, \text{ then } \Gamma \models \varphi. $$
    Soundness ensures that our proof system does not lead to falsehoods.

-   A proof system $\mathcal{P}$ is **complete** if it can prove everything that is semantically true. That is, for any $\Gamma$ and $\varphi$:
    $$ \text{If } \Gamma \models \varphi, \text{ then } \Gamma \vdash_{\mathcal{P}} \varphi. $$
    Completeness, famously established for first-order logic by Gödel's Completeness Theorem (1929), ensures that our [proof system](@entry_id:152790) is powerful enough to capture all logical consequences. It should not be confused with Gödel's later Incompleteness Theorems (1931), which concern the limits of formal theories capable of expressing arithmetic.

These properties have a profound consequence when connected to the notion of consistency. A theory $T$ (a set of sentences) is **syntactically consistent** if it's impossible to derive a contradiction from it, i.e., $T \nvdash_{\mathcal{D}} \bot$ (where $\bot$ is a sentence that is always false). A theory is **semantically consistent** if it has a model. Soundness and completeness together establish a fundamental equivalence:
-   **Soundness** implies that if a theory has a model, it must be syntactically consistent. (Contrapositively: If $T \vdash \bot$, then by soundness $T \models \bot$, which means $T$ has no model).
-   **Completeness** implies that if a theory is syntactically consistent, it must have a model. (Contrapositively: If $T$ has no model, then $T \models \bot$, and by completeness $T \vdash \bot$).

Thus, for any sound and complete [proof system](@entry_id:152790), a theory is syntactically consistent if and only if it is semantically consistent. This is one of the most significant results in modern logic, connecting pure syntax to the existence of mathematical structures [@problem_id:2979693].

### Paradigms of Proof: An Overview of Deductive Systems

Logicians have developed several distinct styles of [proof systems](@entry_id:156272), each with its own philosophical motivations and technical advantages. We will now survey the four major paradigms.

#### Hilbert Systems: Axioms and Inference Rules

Hilbert-style systems, also known as axiomatic systems, are characterized by a large number of axiom schemata and a very small number of [inference rules](@entry_id:636474). They are prized for their theoretical elegance and are well-suited for studying the properties of logic itself.

A typical Hilbert system for classical first-order logic uses the connectives $\to$ and $\neg$ and the quantifier $\forall$ as primitives. It includes:
-   **Axiom Schemata for Propositional Logic**:
    -   $A1: \alpha \to (\beta \to \alpha)$
    -   $A2: (\alpha \to (\beta \to \gamma)) \to ((\alpha \to \beta) \to (\alpha \to \gamma))$
    -   $A3: (\neg\beta \to \neg\alpha) \to (\alpha \to \beta)$ (Contraposition)
-   **Axiom Schemata for Quantifiers**:
    -   $Q1: \forall x\, \varphi \to \varphi[t/x]$ (Universal Instantiation), with the crucial side condition that the term $t$ must be **free for** $x$ in $\varphi$.
    -   $Q2: \forall x\, (\varphi \to \psi) \to (\varphi \to \forall x\, \psi)$, with the side condition that the variable $x$ must not occur free in $\varphi$.
-   **Inference Rules**:
    -   **Modus Ponens**: From $\varphi$ and $\varphi \to \psi$, infer $\psi$.
    -   **Generalization**: From $\varphi$, infer $\forall x\, \varphi$.

When proving theorems from a set of premises $\Gamma$, the Generalization rule must be restricted to be sound: one may infer $\forall x\, \varphi$ from $\varphi$ only if the variable $x$ does not occur free in any premise in $\Gamma$ [@problem_id:2979695].

#### Natural Deduction: Reasoning with Assumptions

Developed by Gerhard Gentzen, Natural Deduction aims to mirror the structure of informal logical arguments. Its key feature is the ability to introduce temporary assumptions and later "discharge" them within a sub-proof. The system is based on harmonious pairs of **introduction** and **elimination** rules for each logical operator.

-   **Conjunction ($\land$)**: The introduction rule ($\land$I) states that from proofs of $A$ and $B$, one can infer $A \land B$. The elimination rule ($\land$E) states that from $A \land B$, one can infer both $A$ and $B$.
-   **Implication ($\to$)**: The introduction rule ($\to$I) is central: if, by assuming $A$, one can derive $B$ in a sub-proof, one can conclude $A \to B$ and discharge the assumption $A$. The elimination rule ($\to$E), or **[modus ponens](@entry_id:268205)**, states that from $A$ and $A \to B$, one can infer $B$.
-   **Disjunction ($\lor$)**: The introduction rule ($\lor$I) states that from $A$, one can infer $A \lor B$. The elimination rule ($\lor$E), or proof by cases, states that if $C$ can be derived from an assumption $A$ and also from an assumption $B$, then from $A \lor B$ one can infer $C$, discharging both assumptions.
-   **Universal Quantifier ($\forall$)**: The introduction rule ($\forall$I) formalizes reasoning about an arbitrary element. From a proof of $\varphi(x)$, one can infer $\forall x\, \varphi(x)$ provided that $x$ is an **eigenvariable**—a variable that does not occur free in any undischarged assumption. This ensures $x$ is truly arbitrary. The elimination rule ($\forall$E) allows one to infer $\varphi(t)$ from $\forall x\, \varphi(x)$, provided $t$ is free for $x$ in $\varphi$.
-   **Existential Quantifier ($\exists$)**: The introduction rule ($\exists$I) allows one to infer $\exists x\, \varphi(x)$ from a proof of a specific instance $\varphi(t)$ (where $t$ is free for $x$ in $\varphi$). The elimination rule ($\exists$E) captures how to use an existential statement. From $\exists x\, \varphi(x)$, one can assume $\varphi(c)$ for a fresh **eigenparameter** $c$ to derive a conclusion $\psi$. If $\psi$ does not contain $c$, one can infer $\psi$, discharging the assumption $\varphi(c)$ [@problem_id:2979664].

#### Sequent Calculus: A Symmetrical Approach

Also developed by Gentzen, the Sequent Calculus (system LK for [classical logic](@entry_id:264911)) offers a more symmetrical and structurally pure framework. Its central objects are **sequents** of the form $\Gamma \Rightarrow \Delta$, where $\Gamma$ (the antecedent) and $\Delta$ (the succedent) are finite multisets of formulas. A sequent is semantically valid if it's impossible for all formulas in $\Gamma$ to be true while all formulas in $\Delta$ are false.

Proofs in LK are trees of sequents built from an initial axiom, typically $A \Rightarrow A$. The rules introduce [logical operators](@entry_id:142505) on either the left or the right side of the sequent arrow.

-   **Conjunction Rules**: To prove $\Gamma \Rightarrow \Delta, A \land B$, one must have proofs for both $\Gamma \Rightarrow \Delta, A$ and $\Gamma \Rightarrow \Delta, B$ ($\land$R). To use $A \land B$ on the left, one simply adds both conjuncts: from $\Gamma, A, B \Rightarrow \Delta$, infer $\Gamma, A \land B \Rightarrow \Delta$ ($\land$L).
-   **Implication Rules**: To prove $A \to B$ on the right, one assumes $A$ and proves $B$: from $\Gamma, A \Rightarrow \Delta, B$, infer $\Gamma \Rightarrow \Delta, A \to B$ ($\to$R). To use $A \to B$ on the left, one splits the proof: from proofs of $\Gamma \Rightarrow \Delta, A$ and $\Gamma, B \Rightarrow \Delta$, one can infer $\Gamma, A \to B \Rightarrow \Delta$ ($\to$L).
-   **Quantifier Rules**: The [quantifier](@entry_id:151296) rules exhibit a beautiful duality.
    -   To prove $\forall x\, A(x)$ on the right ($\forall$R), one must prove $A(y)$ for an arbitrary $y$. This requires an **eigenvariable condition**: from $\Gamma \Rightarrow \Delta, A(y)$, infer $\Gamma \Rightarrow \Delta, \forall x\, A(x)$, provided $y$ is not free in $\Gamma, \Delta$.
    -   To use $\forall x\, A(x)$ on the left ($\forall$L), one can instantiate it with any term $t$: from $\Gamma, A(t) \Rightarrow \Delta$, infer $\Gamma, \forall x\, A(x) \Rightarrow \Delta$, provided $t$ is free for $x$ in $A$.
    -   The rules for $\exists$ are dual: existential introduction on the right ($\exists$R) is like $\forall$L (instantiation with a term), and existential introduction on the left ($\exists$L) is like $\forall$R (requires an eigenvariable) [@problem_id:2979692].

The perfect symmetry and structural purity of [sequent calculus](@entry_id:154229) make it the system of choice for many deep proof-theoretic investigations, such as Gentzen's famous Cut-Elimination Theorem.

#### Semantic Tableaux: The Search for a Countermodel

The semantic tableaux method is a refutation-based system that works by systematically searching for a countermodel. To prove a formula $\varphi$, one starts a tree with $\neg\varphi$ and applies decomposition rules that mirror the semantics of the connectives.

-   **Conjunctive Rules ($\alpha$-rules)**: A formula like $\varphi \land \psi$ on a branch extends the branch with both $\varphi$ and $\psi$.
-   **Disjunctive Rules ($\beta$-rules)**: A formula like $\varphi \lor \psi$ on a branch causes the branch to split into two new branches, one extended with $\varphi$ and the other with $\psi$.
-   A branch is **closed** if it contains an atomic formula and its negation (e.g., $P(c)$ and $\neg P(c)$). If all branches of a tableau close, the initial formula is proved (as its negation is unsatisfiable).
-   A branch that does not close is **open**.

Quantifiers are handled with parameter-based rules that are crucial for completeness:
-   **Universal Quantifier ($\gamma$-rule)**: If $\forall x\,\varphi(x)$ appears on a branch, one may add $\varphi(p)$ to that branch for *any* parameter $p$ that has already appeared on the branch. This formula is never "used up" and can be instantiated multiple times.
-   **Existential Quantifier ($\delta$-rule)**: If $\exists x\,\varphi(x)$ appears on a branch, one must introduce a **fresh parameter** $p$ (one not yet used on that branch) and add $\varphi(p)$ to the branch.

If a fair application of these rules results in a completed open branch, that branch provides all the information needed to construct a **[canonical model](@entry_id:148621)** that satisfies the initial formula. The domain of this model is the set of all parameters appearing on the branch, and a predicate $P$ holds for a tuple of parameters if and only if the corresponding atomic formula appears on the branch. This direct link between proof search and model construction makes tableaux a particularly intuitive and algorithmically useful system [@problem_id:2979672].

### Proof, Truth, and Computation

The existence of sound and complete [proof systems](@entry_id:156272) has profound implications for the computational nature of logic. A [proof system](@entry_id:152790) is **recursively axiomatizable** or **effective** if an algorithm (a Turing machine) can decide whether any given finite sequence of formulas constitutes a valid proof. All the standard systems we have reviewed—Hilbert systems, Natural Deduction, Sequent Calculus, and Tableaux—are effective.

This leads to a fundamental result: **first-order validity is semi-decidable**.

To see why, consider the following proof-search procedure for a given sentence $\varphi$:
1.  Systematically enumerate all possible finite strings of symbols from the language.
2.  For each string, use the effective verifier of our [proof system](@entry_id:152790) $\mathcal{P}$ to check if it is a valid proof.
3.  If the string is a valid proof and its conclusion is $\varphi$, halt and accept.

Let's analyze this procedure's behavior:
-   If $\varphi$ is valid ($\models \varphi$), then by the **completeness** of $\mathcal{P}$, a finite proof of $\varphi$ exists. This proof will eventually be generated by our enumeration, and the procedure will find it, halt, and correctly report that $\varphi$ is valid.
-   If $\varphi$ is not valid ($\not\models \varphi$), then by the **soundness** of $\mathcal{P}$, no proof of $\varphi$ exists. The search will never find such a proof and will continue forever.

This procedure describes an algorithm that halts on all valid inputs and may diverge on invalid inputs. This is the definition of a **semi-decidable** (or recursively enumerable) set. Church's Theorem (1936) further shows that validity is not fully decidable—no algorithm exists that is guaranteed to halt for *all* inputs, correctly identifying both valid and invalid sentences. This limitation is not a failure of our [proof systems](@entry_id:156272), but an inherent property of the richness and expressive power of first-order logic itself [@problem_id:2979674].