## Introduction
In the study of [computability](@entry_id:276011), not all unsolvable problems are created equal. To understand the intricate landscape of what can and cannot be computed, we need a formal way to compare the intrinsic difficulty of different problems. This is the role of **reducibility**, a concept that formalizes the notion of one problem being 'no harder than' another. Many-one and Turing reducibility are the two most fundamental forms of this comparison, each offering a distinct perspective on relative computation and revealing a rich structure within the universe of unsolvable problems.

This article addresses how these reducibilities are defined, how they differ in power, and what consequences these differences have for both computability and complexity theory. It provides a comprehensive exploration of this foundational topic, guiding the reader from first principles to profound applications. The first chapter, **Principles and Mechanisms**, lays the groundwork by introducing the formal definitions of many-one, Turing, and other related reducibilities, examining the hierarchy they form and the algebraic structure of the [degrees of unsolvability](@entry_id:150067). The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the power of these tools in practice, showing how they are used to classify [undecidable problems](@entry_id:145078), define completeness for complexity classes like NP, and investigate the very limits of formal proof. Finally, **Hands-On Practices** will allow you to apply these concepts to concrete problems, solidifying your understanding of their theoretical and practical implications.

## Principles and Mechanisms

In our study of [computability](@entry_id:276011), we classify computational problems, represented as sets of [natural numbers](@entry_id:636016), based on their intrinsic difficulty. The primary tools for this classification are **reducibilities**, which formalize the notion that one problem is "no harder than" another. This chapter delves into the principles and mechanisms of the most fundamental types of reducibility, exploring their definitions, the relationships between them, and the rich algebraic and hierarchical structures they induce. Our set-theoretic universe consists of all subsets of the natural numbers, $\mathcal{P}(\mathbb{N})$, and our notion of "computation" is grounded in a fixed, standard effective enumeration of all partial [computable functions](@entry_id:152169), $(\varphi_e)_{e \in \mathbb{N}}$ [@problem_id:2976636].

### Fundamental Notions of Reducibility

At the heart of [computability theory](@entry_id:149179) lie two foundational concepts of reduction: [many-one reducibility](@entry_id:153891), which involves transforming problem instances, and Turing reducibility, which involves simulating a solution with oracle help.

#### Many-one Reducibility

A **[many-one reducibility](@entry_id:153891)** (or **[mapping reducibility](@entry_id:262207)**), denoted $A \leq_m B$, formalizes the idea of solving problem $A$ by transforming its instances into instances of problem $B$.

**Definition:** A set $A \subseteq \mathbb{N}$ is many-one reducible to a set $B \subseteq \mathbb{N}$, written $A \leq_m B$, if there exists a **total computable function** $f: \mathbb{N} \to \mathbb{N}$ such that for all $x \in \mathbb{N}$:
$$x \in A \iff f(x) \in B$$

The function $f$ acts as a uniform translator. To determine if $x$ is in $A$, one first computes $y = f(x)$ and then asks whether $y$ is in $B$. The answer to the second question is guaranteed to be the answer to the first.

The requirement that the reduction function $f$ be **total** is of paramount importance [@problem_id:2976633]. If $f$ were a partial function that failed to halt on some input $x_0$, our reduction procedure would fail. We could not compute the corresponding instance of $B$, and thus could not decide membership in $A$ for $x_0$. This totality ensures that properties like decidability and [computable enumerability](@entry_id:634007) are properly transferred. If $B$ is decidable (recursive), then $A$ must also be decidable, because the two-step algorithm—1) compute $f(x)$, 2) decide if $f(x) \in B$—is guaranteed to halt for every input $x$. Likewise, if $B$ is [computably enumerable](@entry_id:155267) (c.e.), so is $A$. Totality also guarantees that the relation $\leq_m$ is transitive: if $A \leq_m B$ via $f$ and $B \leq_m C$ via $g$, then $A \leq_m C$ via the composition $h(x) = g(f(x))$, which is itself a total computable function.

#### Turing Reducibility

While [many-one reducibility](@entry_id:153891) involves a single transformation before querying, **Turing reducibility**, denoted $A \leq_T B$, provides a more general and powerful model of relative computation. It captures the idea that an algorithm for $B$ can be used as a subroutine, or an **oracle**, within an algorithm for $A$.

**Definition:** A set $A$ is Turing reducible to a set $B$, written $A \leq_T B$, if there exists an **Oracle Turing Machine** (OTM) which, when given access to an oracle for $B$, computes the [characteristic function](@entry_id:141714) of $A$, $\chi_A$. The oracle for $B$ can answer any query of the form "Is $y \in B$?" in a single step.

Formally, within our framework of partial [computable functions](@entry_id:152169), this is equivalent to stating that there exists an index $e$ such that the OTM $\varphi_e$ with oracle $B$, denoted $\varphi_e^B$, is a total function and $\varphi_e^B = \chi_A$ [@problem_id:2976636]. The OTM can make multiple queries to the oracle, and the choice of subsequent queries can depend on the answers to previous ones—a process known as **adaptive querying**.

### The Hierarchy of Reducibilities

Turing reducibility is strictly more powerful than [many-one reducibility](@entry_id:153891). Any many-one reduction can be viewed as a simple Turing reduction: on input $x$, compute $f(x)$, make a single query to the oracle for $B$ about $f(x)$, and return the answer. Thus, for any sets $A$ and $B$, $A \leq_m B \implies A \leq_T B$ [@problem_id:2976636].

The converse, however, is not true. Consider the acceptance problem for Turing machines, $A_{TM} = \{ \langle M, w \rangle \mid M \text{ accepts } w \}$, which is [computably enumerable](@entry_id:155267) but not decidable. Its complement, $\overline{A_{TM}}$, is not [computably enumerable](@entry_id:155267). We can easily show that $A_{TM} \leq_T \overline{A_{TM}}$, since an oracle for $\overline{A_{TM}}$ can be used to decide $A_{TM}$ simply by negating the oracle's answer to the query "Is $\langle M, w \rangle \in \overline{A_{TM}}$?". However, we have $A_{TM} \not\leq_m \overline{A_{TM}}$. If such a reduction existed, its contrapositive would imply $\overline{A_{TM}} \leq_m A_{TM}$. Since $A_{TM}$ is c.e., and the property of being c.e. is preserved under many-one preimages, this would mean $\overline{A_{TM}}$ is also c.e. But if a set and its complement are both c.e., the set must be decidable, which contradicts the known [undecidability](@entry_id:145973) of $A_{TM}$ [@problem_id:1377296]. This classic example demonstrates a fundamental separation between the two notions of reducibility.

This separation motivates the study of a finer hierarchy of reducibilities that lie between $\leq_m$ and $\leq_T$.

#### One-one and Truth-Table Reducibilities

A natural strengthening of [many-one reducibility](@entry_id:153891) is **one-one reducibility** ($A \leq_1 B$), which requires the reduction function $f$ to be **injective** [@problem_id:2976632]. This constraint means that distinct elements of the domain map to distinct elements in the [codomain](@entry_id:139336). This has important consequences; for instance, if $A \leq_1 B$ and $B$ is a [finite set](@entry_id:152247), the [injectivity](@entry_id:147722) of the reduction function implies that $A$ must also be finite. This is not true for [many-one reducibility](@entry_id:153891), where an infinite set like $\mathbb{N}$ can be mapped to a [finite set](@entry_id:152247) like $\{0\}$ via the [constant function](@entry_id:152060) $f(x)=0$ [@problem_id:2976632].

A significant weakening of Turing reducibility is **truth-table reducibility** ($A \leq_{tt} B$). In a Turing reduction, the queries can be adaptive. A truth-table reduction removes this adaptivity.

**Definition:** $A \leq_{tt} B$ if there is an algorithm that, for any input $x$, computably generates a finite list of queries $(y_1, \dots, y_k)$ and a [boolean function](@entry_id:156574) $\theta_x$ (a "[truth table](@entry_id:169787)"), such that $\chi_A(x) = \theta_x(\chi_B(y_1), \dots, \chi_B(y_k))$ [@problem_id:2976631]. Crucially, the entire set of queries must be determined before any are answered by the oracle.

Every many-one reduction is a truth-table reduction where $k=1$, the query is $f(x)$, and the [truth table](@entry_id:169787) is the [identity function](@entry_id:152136). And every truth-table reduction is a Turing reduction. This gives us the chain $A \leq_m B \implies A \leq_{tt} B \implies A \leq_T B$. The separations are strict. As seen with the complement of [the halting problem](@entry_id:265241), $\overline{K}$, we have $\overline{K} \leq_{tt} K$ (via the NOT function), but $\overline{K} \not\leq_m K$, showing that $\leq_{tt}$ is strictly more general than $\leq_m$ [@problem_id:2976631].

#### Weak Truth-Table Reducibility

Between truth-table and Turing reducibility lies **weak truth-table reducibility** ($A \leq_{wtt} B$). This type of reduction allows for adaptive queries, like a full Turing reduction, but imposes a computable bound on the scope of those queries.

**Definition:** $A \leq_{wtt} B$ if there is an OTM $M$ and a total computable function $g$ (the **use function**) such that for all inputs $x$, $M^B(x)$ decides $A(x)$, and every oracle query made during the computation is to an index less than $g(x)$ [@problem_id:2976627].

This can be expressed functionally: $A \leq_{wtt} B$ if there exist total [computable functions](@entry_id:152169) $g$ and $\psi$ such that for all $x$, $A(x) = \psi(x, B \upharpoonright g(x))$, where $B \upharpoonright n$ denotes the initial segment of $B$ of length $n$ [@problem_id:2976627]. Because a truth-table reduction computes its finite query set $Q_x$ in advance, we can computably find the maximum query $\max(Q_x)$, thus providing a computable use bound. This shows that every truth-table reduction is a weak truth-table reduction [@problem_id:2976627].

In summary, we have a strict hierarchy of common reducibilities:
$$ \leq_1 \subset \leq_m \subset \leq_{tt} \subset \leq_{wtt} \subset \leq_T $$

### The Algebraic Structure of Degrees

Defining equivalence classes of sets under mutual reducibility ($A \equiv_* B \iff A \leq_* B \land B \leq_* A$) gives rise to the **[degrees of unsolvability](@entry_id:150067)**. The structure of these degrees reveals profound truths about the universe of computation.

#### Complementation and Degrees

The behavior of set complementation, $\overline{A} = \mathbb{N} \setminus A$, sharply distinguishes many-one degrees from Turing degrees. For [many-one reducibility](@entry_id:153891), the reduction condition $x \in A \iff f(x) \in B$ is logically equivalent to its contrapositive, $x \notin A \iff f(x) \notin B$. This means the *same* function $f$ that witnesses $A \leq_m B$ also witnesses $\overline{A} \leq_m \overline{B}$. Therefore, $A \leq_m B \iff \overline{A} \leq_m \overline{B}$ [@problem_id:2976628].

Turing degrees behave very differently. Given an oracle for a set $B$, we can trivially simulate an oracle for its complement $\overline{B}$ by simply negating the answers. This means that an oracle for $B$ and an oracle for $\overline{B}$ provide the same computational power. Consequently, for any set $A$, if $A \leq_T B$, then we also have $A \leq_T \overline{B}$. Furthermore, an OTM that decides $A$ using oracle $B$ can be modified to decide $\overline{A}$ by simply flipping its final output. This implies if $A \leq_T B$, then $\overline{A} \leq_T B$. Combining these facts, we arrive at a fundamental property of Turing reducibility: for any set $B$, $B \equiv_T \overline{B}$ [@problem_id:2976628]. A set and its complement always occupy the same Turing degree. This is not true for m-degrees, as exemplified by [the halting problem](@entry_id:265241) $K$ and its complement $\overline{K}$.

#### The Join Operation and Upper Bounds

To understand the structure of degrees, we need a way to combine the information from two sets. This is accomplished by the **join** operation.

**Definition:** The join of two sets $A$ and $B$ is $A \oplus B = \{2x \mid x \in A\} \cup \{2x+1 \mid x \in B\}$.

This operation encodes $A$ onto the even numbers and $B$ onto the odd numbers. It is straightforward to show that $A \leq_m A \oplus B$ (via $f(x)=2x$) and $B \leq_m A \oplus B$ (via $g(x)=2x+1$). Since $\leq_m$ implies $\leq_T$, the same holds for Turing reducibility. This means the degree of $A \oplus B$ is an **upper bound** for the degrees of $A$ and $B$ [@problem_id:2976634].

More importantly, the join provides the **least upper bound** (or supremum). If $C$ is any set such that $A \leq_* C$ and $B \leq_* C$ (for $* \in \{m, T\}$), then it can be shown that $A \oplus B \leq_* C$. The proof for [many-one reducibility](@entry_id:153891) involves constructing a new reduction function that dispatches to the functions for $A \leq_m C$ and $B \leq_m C$ based on parity. The proof for Turing reducibility is analogous, constructing a new OTM that simulates the appropriate machine based on parity [@problem_id:2976634]. The existence of a least upper bound for any pair of degrees means that both the m-degrees and the T-degrees form **upper semi-lattices**.

### The Turing Jump and Relativization

The hierarchy of degrees is not flat; it has a rich vertical structure, which is explored using the Turing jump and the principle of [relativization](@entry_id:274907).

#### The Turing Jump

The **Turing jump** of a set $A$, denoted $A'$, is the set that represents [the halting problem](@entry_id:265241) for oracle Turing machines using $A$ as an oracle.

**Definition:** The jump of $A$ is the set $A' = \{ e \in \mathbb{N} \mid \varphi_e^A(e) \text{ halts} \}$.

The [jump operator](@entry_id:155707) is a uniform way of producing a set that is computationally harder than the original. The relativized version of the [undecidability](@entry_id:145973) of [the halting problem](@entry_id:265241) shows that for any set $A$, $A' \not\leq_T A$ [@problem_id:2976630]. The [jump operator](@entry_id:155707) maps each Turing degree to a strictly higher degree.

The jump also serves as a canonical complete set for the class of problems that are "[computably enumerable](@entry_id:155267) relative to $A$". This class, denoted $\Sigma_1^0(A)$, consists of all sets $S$ for which there is an $A$-decidable predicate $R(x,y)$ such that $x \in S \iff \exists y R(x,y)$. The jump $A'$ is itself in $\Sigma_1^0(A)$, and more importantly, it is **many-one complete** for this class. That is, for any set $S$:
$$ S \in \Sigma_1^0(A) \iff S \leq_m A' $$
This provides a powerful characterization of the first level of the [arithmetical hierarchy](@entry_id:155689) relative to any oracle [@problem_id:2976630].

#### The Principle of Relativization

A remarkable feature of Turing reducibility is that the entire theory of degrees can be "relativized" to an arbitrary oracle $X$. This means we can study what computation looks like from the perspective of an observer who has free access to all the information in $X$.

Relativized Turing reducibility, $A \leq_T^X B$, is defined as the existence of an OTM that decides $A$ with access to both $B$ and $X$ as oracles. This is equivalent to ordinary Turing reducibility to the join of the oracles: $A \leq_T^X B \iff A \leq_T B \oplus X$ [@problem_id:2976629].

This [relativization](@entry_id:274907) provides a powerful structural insight: the partial ordering of the relativized Turing degrees (the $\leq_T^X$-degrees) is isomorphic to the partial ordering of the ordinary Turing degrees located "above" $X$ (the set of degrees $\{ \mathbf{d} \mid \text{deg}(X) \leq_T \mathbf{d} \}$). The map $A \mapsto A \oplus X$ provides this [isomorphism](@entry_id:137127). The [jump operator](@entry_id:155707) also relativizes smoothly, obeying the law $(A \oplus X)' \equiv_T A' \oplus X'$ [@problem_id:2976629]. This principle implies that any theorem about the structure of Turing degrees that can be proven using methods that relativize holds true not just for the entire structure, but also for the structure of degrees within any "upper cone" above a given degree. This reveals a profound [self-similarity](@entry_id:144952) in the intricate and complex hierarchy of unsolvability.