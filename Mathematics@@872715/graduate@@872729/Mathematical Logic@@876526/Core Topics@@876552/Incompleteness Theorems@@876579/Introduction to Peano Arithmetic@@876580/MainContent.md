## Introduction
Peano Arithmetic (PA) stands as a landmark achievement in the foundations of mathematics, providing a rigorous axiomatic framework for the natural numbers. While seemingly straightforward, this system is the source of some of the most profound and counterintuitive results in modern logic. Its significance lies not only in what it can prove but, more importantly, in what it cannot. This article addresses the fundamental tension between the intuitive truths of arithmetic and the limitations of formal proof, exploring how a [finite set](@entry_id:152247) of axioms can describe an infinite structure and yet fall short of capturing all of its truths.

This exploration is divided into three parts. First, in **Principles and Mechanisms**, we will build Peano Arithmetic from the ground up, defining its formal language, detailing its axioms, and examining its capacity to represent computation. This section culminates in a confrontation with its inherent limits: the existence of [non-standard models](@entry_id:151939) and Gödel's famous incompleteness theorems. Next, **Applications and Interdisciplinary Connections** will demonstrate how logicians harness the structure of PA to analyze the very nature of proof and computation, leading to the development of [provability logic](@entry_id:149023) and the [ordinal analysis](@entry_id:151596) of axiomatic systems. Finally, **Hands-On Practices** will provide opportunities to engage directly with the core concepts through guided problems.

We begin our journey by dissecting the formal principles and logical mechanisms that give Peano Arithmetic its remarkable power and define its ultimate boundaries.

## Principles and Mechanisms

Having introduced the historical and philosophical context of Peano Arithmetic (PA), we now turn to a rigorous examination of its formal structure. This chapter will dissect the principles upon which PA is built and the mechanisms through which it derives its extraordinary expressive power and, as we shall see, its inherent limitations. We will begin by defining the precise language of arithmetic and its intended interpretation. We will then detail the axioms that give this language its mathematical substance, paying special attention to the celebrated axiom schema of induction. Subsequently, we will explore the remarkable capacity of PA to represent computation, a cornerstone of modern logic. Finally, we will confront the profound limits of this formal system, exploring the existence of [non-standard models](@entry_id:151939) and the incompleteness phenomena discovered by Kurt Gödel.

### The Formal Language and Standard Model of Arithmetic

The study of any formal system must begin with a precise specification of its syntax (the language) and its semantics (the meaning or interpretation). For Peano Arithmetic, these are the language of arithmetic, denoted $L_{PA}$, and its standard interpretation in the natural numbers, the structure $\mathbb{N}$.

#### The Language $L_{PA}$

The language of Peano Arithmetic, $L_{PA}$, is a specific instance of a [first-order language](@entry_id:151821) with equality. This means its vocabulary and grammar are constrained by the rules of [first-order logic](@entry_id:154340). The logical symbols are standard: a countably infinite set of variables (e.g., $x, y, z, \dots$), the [logical connectives](@entry_id:146395) ($\neg, \land, \lor, \to, \leftrightarrow$), the [quantifiers](@entry_id:159143) ($\forall, \exists$), and the equality symbol $=$. The modern convention, which we adopt, treats equality as a logical symbol with a fixed interpretation as the identity relation.

The distinctive character of $L_{PA}$ comes from its **non-logical symbols**, which constitute its signature. These are the symbols specific to the theory of arithmetic [@problem_id:2974920]:

*   A constant symbol: $0$. This symbol, formally a function symbol of arity zero, is intended to name a specific element in the domain, the number zero.

*   A unary function symbol: $S$. This symbol is intended to represent the successor function, which maps a number to the next one (i.e., $n \mapsto n+1$).

*   Two binary function symbols: $+$ and $\cdot$. These symbols are intended to represent the operations of addition and multiplication, respectively.

From this vocabulary, we can inductively define the **terms** of the language. The set of terms is the smallest set containing the constant $0$ and all variables, and is closed under the application of function symbols. That is, if $t$ and $u$ are terms, then $S(t)$, $(t+u)$, and $(t \cdot u)$ are also terms. For example, $S(0)$, $S(S(0))$, and $(x + S(y)) \cdot z$ are all well-formed terms.

A particularly important class of terms are the **numerals**. For each natural number $n \in \mathbb{N}$, the numeral $\overline{n}$ is the closed term (a term with no variables) that canonically represents $n$. Numerals are constructed recursively: $\overline{0}$ is the constant symbol $0$, and $\overline{n+1}$ is the term $S(\overline{n})$ [@problem_id:2974919]. Thus, $\overline{1}$ is $S(0)$, $\overline{2}$ is $S(S(0))$, and so on. The term $\overline{n}$ can be abbreviated as $S^n(0)$.

The **atomic formulas** of $L_{PA}$ are the most basic statements that can be true or false. Since equality is the only predicate symbol in our language, all atomic formulas are equations of the form $t_1 = t_2$, where $t_1$ and $t_2$ are terms. For instance, $S(S(0)) = \overline{2}$ and $x+y = y+x$ are atomic formulas. More complex formulas are built from these using [logical connectives](@entry_id:146395) and quantifiers, as in $\forall x \exists y (x=y+y \lor x=S(y+y))$.

It is crucial to be able to define specific numbers within any structure, not just the standard one. The most direct formula $\varphi_n(x)$ that is true of exactly the element denoted by the term $\overline{n}$ is the atomic formula $x = \overline{n}$. An equivalent, though more complex, way to define this is recursively: let $\mathrm{Num}_0(x)$ be $x=0$, and $\mathrm{Num}_{k+1}(x)$ be $\exists y (\mathrm{Num}_k(y) \land x=S(y))$. The formula $\mathrm{Num}_n(x)$ then serves the same purpose as $x = \overline{n}$ in any $L_{PA}$-structure [@problem_id:2974919].

#### The Standard Model $\mathbb{N}$

While the language $L_{PA}$ provides the syntax, it remains an uninterpreted formal calculus until we provide a structure in which to interpret it. The **[standard model](@entry_id:137424)** of arithmetic, denoted $\mathcal{N}$ (or simply $\mathbb{N}$), is the structure where the symbols are given their intended meanings [@problem_id:2974902].

A structure for $L_{PA}$ consists of a non-empty set called the domain and an interpretation for each non-logical symbol. The [standard model](@entry_id:137424) $\mathcal{N}$ is defined as follows:

*   The domain is the set of natural numbers, $\mathbb{N} = \{0, 1, 2, \dots\}$.

*   The interpretation of the constant symbol $0$, denoted $0^{\mathcal{N}}$, is the number $0 \in \mathbb{N}$.

*   The interpretation of the unary function symbol $S$, denoted $S^{\mathcal{N}}$, is the successor function on $\mathbb{N}$: $S^{\mathcal{N}}(n) = n+1$ for all $n \in \mathbb{N}$.

*   The interpretation of the binary function symbol $+$, denoted $+^{\mathcal{N}}$, is the [standard addition](@entry_id:194049) function on $\mathbb{N}$: $+^{\mathcal{N}}(m,n) = m+n$ for all $m,n \in \mathbb{N}$.

*   The interpretation of the binary function symbol $\cdot$, denoted $\cdot^{\mathcal{N}}$, is the standard multiplication function on $\mathbb{N}$: $\cdot^{\mathcal{N}}(m,n) = m \cdot n$ for all $m,n \in \mathbb{N}$.

When we say a sentence $\varphi$ is "true in arithmetic," we formally mean that it is true in the [standard model](@entry_id:137424), written $\mathcal{N} \models \varphi$. For example, $\mathcal{N} \models \forall x \forall y (x+y = y+x)$ because addition is indeed commutative on the natural numbers. The central goal of Peano Arithmetic is to find a set of axioms that are all true in $\mathcal{N}$ and are strong enough to prove as many other true statements as possible.

### The Axioms of Peano Arithmetic (PA)

Peano Arithmetic is the first-order theory consisting of a specific set of non-logical axioms in the language $L_{PA}$. These axioms are designed to capture the fundamental properties of the [natural numbers](@entry_id:636016) as described by the standard model $\mathcal{N}$. They can be grouped into axioms for the successor function, [recursive definitions](@entry_id:266613) for addition and multiplication, and the powerful axiom schema of induction [@problem_id:2974928].

#### The Foundational Axioms

The first group of axioms establishes the basic properties of the successor, addition, and multiplication operations.

**Successor Axioms:** These two axioms establish that the numbers start at $0$ and proceed in a simple, non-repeating chain.
1.  $\forall x (\neg(S(x) = 0))$
    *   (Zero is not the successor of any number.)
2.  $\forall x \forall y (S(x) = S(y) \to x = y)$
    *   (The successor function is injective; different numbers have different successors.)

**Addition Axioms:** These axioms define addition recursively.
3.  $\forall x (x + 0 = x)$
    *   (Adding zero does not change a number.)
4.  $\forall x \forall y (x + S(y) = S(x + y))$
    *   (Adding the successor of $y$ is the same as taking the successor of the sum with $y$. This is the formal equivalent of $x+(y+1) = (x+y)+1$.)

**Multiplication Axioms:** These axioms define multiplication recursively, relying on the prior definition of addition.
5.  $\forall x (x \cdot 0 = 0)$
    *   (Multiplying by zero yields zero.)
6.  $\forall x \forall y (x \cdot S(y) = x \cdot y + x)$
    *   (Multiplying by the successor of $y$ is the same as multiplying by $y$ and adding $x$ once more. This is the formal equivalent of $x(y+1) = xy+x$.)

These seven axioms (sometimes called the axioms of Robinson Arithmetic, or Q) are sufficient to prove many basic facts of arithmetic and to show that any computable function is representable (a point we will return to). However, they are famously weak and cannot prove even simple truths like the commutativity of addition. For that, we need induction.

#### The Axiom Schema of Induction

The [principle of mathematical induction](@entry_id:158610) is the engine that drives PA. In first-order logic, this principle cannot be stated as a single axiom. Instead, it is expressed as an **axiom schema**, an infinite collection of axioms, one for each formula in the language $L_{PA}$.

**Axiom Schema of Induction:** For every formula $\varphi(x, \vec{u})$ in $L_{PA}$ with [free variables](@entry_id:151663) $x$ and a tuple of parameters $\vec{u}$, the universal closure of the following formula is an axiom:
$$ (\varphi(0, \vec{u}) \land \forall x (\varphi(x, \vec{u}) \to \varphi(S(x), \vec{u}))) \to \forall z \varphi(z, \vec{u}) $$

This schema formalizes the intuitive principle: if a property $\varphi$ holds for $0$ (the [base case](@entry_id:146682)), and if whenever it holds for a number $x$, it also holds for its successor $S(x)$ (the [inductive step](@entry_id:144594)), then the property must hold for all numbers.

To illustrate, consider the property "is an even number," which can be expressed by the formula $\varphi(x) \equiv \exists y (x = y+y)$. The induction axiom for this specific formula would be [@problem_id:2974928]:
$$ \left( \exists y(0 = y+y) \land \forall x \left( \exists y(x = y+y) \to \exists y(S(x) = y+y) \right) \right) \to \forall z \exists y (z = y+y) $$
This axiom asserts that if $0$ is even, and if $x$ being even implies $S(x)$ is even, then all numbers are even. (Of course, the [inductive step](@entry_id:144594) here is false, so this axiom does not force the incorrect conclusion that all numbers are even).

#### The Justification for Induction

A natural question is why we should accept this infinite collection of axioms. The justification comes from the fact that every single instance of the induction schema is true in the [standard model](@entry_id:137424) $\mathcal{N}$. This can be demonstrated by appealing to the set-theoretic construction of the natural numbers [@problem_id:2974909].

In modern set theory (like ZFC), the natural numbers are constructed such that $\mathbb{N}$ is the *least inductive set*. A set $I$ is defined as **inductive** if it contains $0$ (the empty set $\emptyset$) and is closed under the successor operation ($n \mapsto n \cup \{n\}$). $\mathbb{N}$ is then the intersection of all inductive sets.

Now, consider any property expressible by an $L_{PA}$-formula $\varphi(x)$. This formula defines a set $A_{\varphi} = \{ n \in \mathbb{N} \mid \mathcal{N} \models \varphi(\overline{n}) \}$. The premises of the induction axiom for $\varphi$ are:
1.  Base Case: $\mathcal{N} \models \varphi(0)$, which means $0 \in A_{\varphi}$.
2.  Inductive Step: $\mathcal{N} \models \forall x (\varphi(x) \to \varphi(S(x)))$, which means for any $n \in A_{\varphi}$, we have $S(n) \in A_{\varphi}$.

These two conditions are precisely the definition of $A_{\varphi}$ being an inductive set. But $A_{\varphi}$ is a subset of $\mathbb{N}$, and $\mathbb{N}$ is the *least* inductive set. This means any inductive set that is a subset of $\mathbb{N}$ must be $\mathbb{N}$ itself. Therefore, $A_{\varphi} = \mathbb{N}$. This means that $\mathcal{N} \models \forall x \varphi(x)$, which is the conclusion of the induction axiom. This argument confirms that every induction axiom is true in the [standard model](@entry_id:137424), justifying our choice to include them in our theory.

### The Expressive Power of Peano Arithmetic: Representing Computation

One of the most profound discoveries in 20th-century logic was that the seemingly simple language and axioms of PA are sufficient to describe the entirety of what we now call computation. This is formalized through the concept of representability.

#### Primitive Recursive Functions

To speak of computation, we must first define a formal class of "computable" functions. The first such class to be rigorously studied was the class of **primitive recursive (PR) functions**. This class is built from a simple base of initial functions using a finite number of applications of two construction rules: composition and [primitive recursion](@entry_id:638015) [@problem_id:2974907].

**Initial Functions:**
1.  **Successor Function:** $S(x) = x+1$.
2.  **Zero Function:** $Z(x) = 0$. (And by composition, $Z^k(x_1, \dots, x_k) = 0$ for any arity $k$).
3.  **Projection Functions:** $U_i^k(x_1, \dots, x_k) = x_i$ for any arity $k$ and $1 \le i \le k$.

**Closure Operations:**
1.  **Composition:** If $g_1, \dots, g_m$ are PR functions of arity $k$ and $f$ is a PR function of arity $m$, then the function $h(\vec{x}) = f(g_1(\vec{x}), \dots, g_m(\vec{x}))$ is also PR.
2.  **Primitive Recursion:** If $f$ is a PR function of arity $k$ and $g$ is a PR function of arity $k+2$, then the function $h$ of arity $k+1$ defined by the following schema is PR:
    *   $h(\vec{x}, 0) = f(\vec{x})$
    *   $h(\vec{x}, S(y)) = g(\vec{x}, y, h(\vec{x}, y))$

The class of PR functions is the smallest class containing the initial functions and closed under these two operations. This class includes all the functions one would typically consider "computable" in an elementary sense. For example, addition is primitive recursive. It can be defined by the schema with $k=1$:
*   $add(x, 0) = x$
*   $add(x, S(y)) = S(add(x, y))$

Here, the base function is $f(x) = U_1^1(x) = x$, and the [step function](@entry_id:158924) is $g(x, y, z) = S(U_3^3(x, y, z)) = S(z)$. Both are built from initial functions, so addition is PR. Similarly, multiplication can be defined from addition using [primitive recursion](@entry_id:638015), establishing that it, too, is a PR function [@problem_id:2974907].

#### Representability in PA

The bridge between the abstract world of [computability](@entry_id:276011) and the [formal system](@entry_id:637941) of PA is the concept of **representability**. A function $f: \mathbb{N}^k \to \mathbb{N}$ is said to be **strongly representable** in PA if there exists a formula $\varphi_f(\vec{x}, y)$ in the language $L_{PA}$ such that [@problem_id:2974914]:
1.  For all $\vec{n}, m \in \mathbb{N}$, we have $f(\vec{n}) = m$ if and only if $\mathcal{N} \models \varphi_f(\overline{\vec{n}}, \overline{m})$. (The formula correctly describes the function in the standard model).
2.  PA proves that for any input, there is a unique output: $\mathrm{PA} \vdash \forall \vec{x} \exists! y \, \varphi_f(\vec{x}, y)$.

A central theorem of [mathematical logic](@entry_id:140746), first established by Gödel, states that:

**Every primitive [recursive function](@entry_id:634992) is strongly representable in Peano Arithmetic.**

The proof of this theorem is constructive. For any given PR function $f$, one can construct a representing formula. This formula is typically a **$\Sigma_1$ formula**, which is a formula of the form $\exists \vec{w} \, \delta(\dots)$, where $\delta$ contains only bounded quantifiers (e.g., $\forall z \le t$ or $\exists z \le t$).

The construction is a masterpiece of logical ingenuity [@problem_id:2974914]. The core idea is to formalize the notion of a computation history. A computation of $f(\vec{n})$ is a finite sequence of numbers representing the step-by-step evaluation according to its primitive [recursive definition](@entry_id:265514). Using a clever coding device known as **Gödel's $\beta$-function**, one can encode any finite sequence of numbers into a single natural number, let's call it $w$. The crucial property of the $\beta$-function is that the relation "$z$ is the $i$-th element of the sequence coded by $w$" is itself representable by a $\Delta_0$ formula (one with only bounded quantifiers).

The representing formula $\varphi_f(\vec{x}, y)$ for a function $f$ can then be written as:
$$ \varphi_f(\vec{x}, y) \equiv \exists w \, \delta(\vec{x}, y, w) $$
Here, $\delta$ is a $\Delta_0$ formula which states that:
*   "$w$ is the code of a valid computation sequence."
*   "The initial values of the sequence correspond to the inputs $\vec{x}$."
*   "Each subsequent value in the sequence is correctly generated from previous values according to the rules of composition or [recursion](@entry_id:264696) defining $f$."
*   "The final value of the sequence is $y$."

The fact that all [primitive recursive functions](@entry_id:155169) are representable in PA is the technical key that unlocks Gödel's incompleteness theorems. It means that PA can talk about its own syntax, formulas, and proofs, by assigning numbers to them (Gödel numbering) and then using representing formulas to describe relations between these numbers.

### The Inherent Limitations of Peano Arithmetic

Despite its immense expressive power, first-order Peano Arithmetic is fundamentally limited. These limitations manifest as a lack of [categoricity](@entry_id:151177) and, most famously, as incompleteness.

#### The Problem of Categoricity: The Existence of Non-Standard Models

A theory is **categorical** if all of its models are isomorphic. Categoricity is a desirable property, as it means the axioms have pinned down a unique mathematical structure. Second-order Peano Arithmetic, with its single induction axiom quantifying over all subsets of the domain, is categorical [@problem_id:2974948].

In contrast, first-order PA is **not categorical**. It has models that are not isomorphic to the standard model $\mathbb{N}$. These are called **[non-standard models](@entry_id:151939)**. The reason for this difference lies in the expressive weakness of [first-order logic](@entry_id:154340) compared to second-order logic. The first-order induction schema only guarantees induction for the countably many subsets of $\mathbb{N}$ that are definable by a first-order formula. It says nothing about the uncountably many other subsets. This "loophole" allows for the existence of models containing "non-standard" elements.

The existence of [non-standard models](@entry_id:151939) is a direct consequence of the **Compactness Theorem** for [first-order logic](@entry_id:154340). We can prove their existence with the following elegant argument [@problem_id:2974948]:
1.  Augment the language $L_{PA}$ with a new constant symbol, $c$.
2.  Consider the theory $T'$ formed by taking all the axioms of PA and adding an infinite set of new axioms: $\{c \neq \overline{0}, c \neq \overline{1}, c \neq \overline{2}, \dots \}$.
3.  Now consider any finite subset $\Delta$ of $T'$. It contains the axioms of PA and a finite number of axioms of the form $c \neq \overline{n_i}$. Let $N$ be the largest such $n_i$. We can satisfy $\Delta$ in the standard model $\mathcal{N}$ by interpreting $c$ as the number $N+1$. Since this works for any finite subset, by the Compactness Theorem, the entire theory $T'$ must have a model, let's call it $\mathcal{M}^*$.
4.  This model $\mathcal{M}^*$ is a model of PA. However, the element interpreting $c$ is, by construction, different from the interpretation of every standard numeral $\overline{n}$. This element $c$ is a non-standard number.

The model $\mathcal{M}^*$ thus contains a copy of the standard [natural numbers](@entry_id:636016), but also other elements "beyond infinity." Such a model cannot be isomorphic to $\mathbb{N}$, proving that PA is not categorical.

#### Incompleteness I: Undecidable Sentences

The most celebrated limitation of PA is its **incompleteness**, discovered by Kurt Gödel. A theory is incomplete if there is a sentence $\varphi$ in its language such that the theory can neither prove $\varphi$ nor its negation $\neg \varphi$. Such a sentence is called **undecidable** by the theory.

Gödel's First Incompleteness Theorem states that any consistent, recursively axiomatized theory strong enough to represent all [primitive recursive functions](@entry_id:155169) (a condition PA satisfies) is necessarily incomplete. The proof involves constructing a sentence that, in effect, asserts its own unprovability.

A clearer example is the **Rosser sentence**, $R_{PA}$, a refinement of Gödel's original sentence. $R_{PA}$ is a self-referential sentence that asserts: "For any proof of me, there exists a shorter proof of my negation." [@problem_id:2974951]. A careful analysis shows that if PA is consistent, it can neither prove nor refute $R_{PA}$. However, we, standing outside the system, can see that $R_{PA}$ must be true in the [standard model](@entry_id:137424) $\mathbb{N}$. Since there is no proof of $R_{PA}$ in PA, the statement "for any proof of me..." is vacuously true.

Beyond such self-referential sentences, there are natural mathematical statements, true in $\mathbb{N}$, that are undecidable in PA. Famous examples include:
*   **Goodstein's Theorem:** A statement from number theory about sequences that always terminate. Its proof requires [transfinite induction](@entry_id:153920) up to the ordinal $\varepsilon_0$, a principle which is known to be unprovable in PA.
*   **The Paris-Harrington Principle:** A strengthening of the finite Ramsey theorem from combinatorics.

The unprovability of these sentences is typically established via Gödel's Second Incompleteness Theorem, which states that if PA is consistent, it cannot prove its own consistency statement, $\mathrm{Con(PA)}$. It can be shown that both Goodstein's Theorem and the Paris-Harrington Principle, if added as axioms to PA, would allow for a proof of $\mathrm{Con(PA)}$. Therefore, they cannot have been provable in PA in the first place [@problem_id:2974951].

#### Incompleteness II: $\omega$-Incompleteness and Non-Standard Models

A related and revealing form of incompleteness is **$\omega$-incompleteness**. A consistent theory $T$ is $\omega$-incomplete if there is a formula $\psi(x)$ such that $T$ proves $\psi(\overline{n})$ for every single natural number $n \in \mathbb{N}$, yet $T$ fails to prove the [universal generalization](@entry_id:276449) $\forall x \psi(x)$.

PA itself is not $\omega$-incomplete (assuming it's consistent), but we can use this concept to beautifully illustrate the connection between incompleteness and [non-standard models](@entry_id:151939). Consider the formula [@problem_id:2974912]:
$$ \psi(x) \equiv \neg \mathrm{Prf}_{\mathrm{PA}}(x, \ulcorner 0=1 \urcorner) $$
This formula formalizes the statement "$x$ is not the Gödel number of a proof of a contradiction (i.e., of $0=1$)".

Let's analyze this formula in PA:
1.  **Provability of Instances:** For any standard natural number $n$, we can mechanically check whether it codes a proof of $0=1$. Since PA is consistent, we will find that it does not. Because this is a checkable property of a primitive recursive relation, PA is strong enough to formalize this check and prove it. Thus, for every $n \in \mathbb{N}$, we have $\mathrm{PA} \vdash \psi(\overline{n})$.

2.  **Unprovability of the Universal:** The universal statement $\forall x \psi(x)$ is $\forall x \neg \mathrm{Prf}_{\mathrm{PA}}(x, \ulcorner 0=1 \urcorner)$, which is logically equivalent to $\neg \exists x \mathrm{Prf}_{\mathrm{PA}}(x, \ulcorner 0=1 \urcorner)$. This is precisely the formal consistency statement, $\mathrm{Con(PA)}$. By Gödel's Second Incompleteness Theorem, if PA is consistent, then $\mathrm{PA} \nvdash \mathrm{Con(PA)}$. Therefore, $\mathrm{PA} \nvdash \forall x \psi(x)$.

This is a stunning result. PA can prove that $0$ is not a proof of a contradiction, $1$ is not a proof of a contradiction, and so on for every standard number we can name. Yet, it cannot take the final step and conclude that *no* number is a proof of a contradiction.

The existence of [non-standard models](@entry_id:151939) provides the explanation. Consider a non-[standard model](@entry_id:137424) $\mathcal{M}^*$ of the theory $\mathrm{PA} + \neg \mathrm{Con(PA)}$. This model satisfies all the axioms of PA. But it also satisfies $\neg \mathrm{Con(PA)}$, which means there is some element $c$ in its domain such that $\mathcal{M}^* \models \mathrm{Prf}_{\mathrm{PA}}(c, \ulcorner 0=1 \urcorner)$. This element $c$ must be a non-standard number. In this model, the statement $\forall x \psi(x)$ is false, and $c$ is the [counterexample](@entry_id:148660). The model "believes" that $c$ is the code for a proof of a contradiction, even while it agrees that no standard number can be such a code. This divergence between what is true for all standard numbers and what can be proven for *all* numbers in the domain is the essence of incompleteness.