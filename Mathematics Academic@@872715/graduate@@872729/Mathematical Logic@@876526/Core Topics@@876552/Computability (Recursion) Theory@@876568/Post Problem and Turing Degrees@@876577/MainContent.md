## Introduction
In the landscape of [computability theory](@entry_id:149179), the concept of a Turing degree provides a fundamental way to classify the intrinsic complexity of problems. By comparing sets based on relative [computability](@entry_id:276011), we can organize them into a rich algebraic structure. However, the nature of this structure, particularly for the important class of [computably enumerable](@entry_id:155267) (c.e.) sets, was once a profound mystery. This gap in knowledge was crystallized in a famous question posed by Emil Post: are there any problems that are uncomputable, yet not as complex as [the halting problem](@entry_id:265241)? This is the essence of Post's Problem, and its solution ushered in a new era of [computability theory](@entry_id:149179).

This article provides a graduate-level exploration of Post's Problem and the theory of Turing degrees. Across three chapters, you will gain a deep understanding of this pivotal area of mathematical logic. The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork, formalizing the structure of Turing degrees and introducing the finite-injury priority method, the revolutionary technique that solved Post's Problem. Next, **Applications and Interdisciplinary Connections** explores the far-reaching consequences of this solution, revealing the intricate [fine structure](@entry_id:140861) of the c.e. degrees and building bridges to other domains such as descriptive set theory and reverse mathematics. Finally, **Hands-On Practices** will challenge you to apply these concepts, guiding you through constructions that form the bedrock of modern [computability theory](@entry_id:149179).

## Principles and Mechanisms

This chapter delves into the structural properties of Turing degrees, with a particular focus on the degrees of [computably enumerable sets](@entry_id:148947). We will begin by formalizing the algebraic structure formed by the Turing degrees, then state the central historical question known as Post's Problem. The resolution of this problem required the invention of a powerful new proof technique—the priority method—which we will explore in detail. Finally, we will examine the finer structural properties of the [computably enumerable](@entry_id:155267) degrees that were uncovered using this method, touching upon key results and enduring open questions.

### The Algebraic Structure of Turing Degrees

The concept of Turing reducibility, denoted $A \le_T B$, establishes a preorder on the subsets of the natural numbers, $\mathcal{P}(\mathbb{N})$. By factoring this preorder by the equivalence relation of mutual reducibility, $A \equiv_T B$, we obtain a partial order on the resulting [equivalence classes](@entry_id:156032), which are the **Turing degrees**. We denote the [partially ordered set](@entry_id:155002) of Turing degrees by $(\mathcal{D}, \le_T)$. This structure is more than a mere [partial order](@entry_id:145467); it possesses a rich algebraic character.

A key operation on this structure is the **join**. Given two sets, $A$ and $B$, their join, denoted $A \oplus B$, is defined as:
$$
A \oplus B = \{ 2n \mid n \in A \} \cup \{ 2n+1 \mid n \in B \}
$$
The Turing degree of $A \oplus B$ represents the least upper bound (or supremum) of the degrees of $A$ and $B$. Let $\mathbf{a} = \deg(A)$ and $\mathbf{b} = \deg(B)$. The degree $\mathbf{a} \vee \mathbf{b} = \deg(A \oplus B)$ is an upper bound because both $A \le_T A \oplus B$ and $B \le_T A \oplus B$. For instance, to decide if $n \in A$, one simply queries an oracle for $A \oplus B$ about the membership of $2n$. It is the *least* upper bound because if some other degree $\mathbf{c} = \deg(C)$ is an upper bound for both $\mathbf{a}$ and $\mathbf{b}$ (i.e., $A \le_T C$ and $B \le_T C$), then $A \oplus B \le_T C$. An algorithm to decide membership in $A \oplus B$ using a $C$-oracle can, for any input $m$, first check if $m$ is even ($m=2n$) or odd ($m=2n+1$) and then use the reduction from $A$ to $C$ or from $B$ to $C$, respectively. This property ensures that $(\mathcal{D}, \le_T)$ is an **upper semi-lattice** [@problem_id:2986079].

Another fundamental concept is the **Turing jump**. For any set $A$, its jump, denoted $A'$, is the set that encodes [the halting problem](@entry_id:265241) relative to an oracle for $A$:
$$
A' = \{ e \in \mathbb{N} \mid \Phi_e^A(e) \downarrow \}
$$
Here, $\Phi_e^A$ represents the $e$-th oracle Turing machine with oracle $A$. The jump of the [empty set](@entry_id:261946), $\emptyset'$, is of particular importance. Since computations relative to $\emptyset$ are simply standard Turing computations, $\emptyset'$ is equivalent to the ordinary [halting problem](@entry_id:137091), $K = \{ e \mid \varphi_e(e) \downarrow \}$. The degree of $\emptyset'$ is denoted $\mathbf{0'}$. It is a foundational result that for any set $A$, $A$ is strictly less complex than its jump: $A \lt_T A'$. This means $A \le_T A'$ but $A' \not\le_T A$. In degree-theoretic terms, $\deg(A) \lt \deg(A')$. A direct consequence of this **Jump Theorem** is that there is no greatest Turing degree. Given any degree $\mathbf{d}$, its jump $\mathbf{d}'$ is strictly greater. This gives rise to an infinite ascending chain of degrees starting from the degree of computable sets, $\mathbf{0}$:
$$
\mathbf{0} \lt \mathbf{0'} \lt \mathbf{0''} \lt \mathbf{0'''} \lt \dots
$$
where $\mathbf{0}^{(n+1)} = (\mathbf{0}^{(n)})'$. Thus, $\mathbf{0'}$ is not the greatest of all Turing degrees [@problem_id:2986079].

### Post's Problem and the Computably Enumerable Degrees

While the universe of all Turing degrees is vast and unbounded, [computability theory](@entry_id:149179) has historically paid special attention to the degrees of **[computably enumerable](@entry_id:155267) (c.e.) sets**. A set is c.e. if a Turing machine can list its members. Let $\mathcal{D}_{\text{c.e.}}$ be the set of all c.e. degrees.

A cornerstone result, known as **Post's Theorem**, states that a set $A$ is [computably enumerable](@entry_id:155267) if and only if it is Turing reducible to [the halting problem](@entry_id:265241), $A \le_T K$. In degree-theoretic terms, this means that every c.e. degree $\mathbf{a}$ satisfies $\mathbf{a} \le \mathbf{0'}$. This establishes $\mathbf{0'}$ as the maximum element within the structure of c.e. degrees, $(\mathcal{D}_{\text{c.e.}}, \le_T)$.

In the 1940s, all known c.e. sets fell into two classes: the computable sets (of degree $\mathbf{0}$) and the Turing-complete sets, such as $K$ itself, which were equivalent in power to [the halting problem](@entry_id:265241) (of degree $\mathbf{0'}$). This led Emil Post to pose what is now known as **Post's Problem**:

> Does there exist a [computably enumerable](@entry_id:155267) set that is neither computable nor Turing-complete?

In the language of degrees, the question is whether the structure of c.e. degrees is trivial, containing only $\mathbf{0}$ and $\mathbf{0'}$, or if it contains intermediate degrees. Formally, Post's Problem asks whether there exists a c.e. degree $\mathbf{a}$ such that $\mathbf{0} \lt \mathbf{a} \lt \mathbf{0'}$ [@problem_id:2978708].

Post's own attempts to solve this problem involved defining various classes of c.e. sets based on the properties of their complements. One of the most notable of these is the class of **simple sets**. A c.e. set $A$ is **simple** if its complement $\overline{A}$ is infinite but "immune," meaning $\overline{A}$ contains no infinite c.e. subset. By this definition, a simple set cannot be computable (as its infinite complement would then be a c.e. subset of itself). Thus, every simple set has a degree strictly greater than $\mathbf{0}$. Post hoped that this algebraic property would be strong enough to also guarantee Turing incompleteness (i.e., degree strictly less than $\mathbf{0'}$), which would solve his problem. However, this turned out not to be the case. It was later shown that there exist simple sets that are Turing-complete, having degree $\mathbf{0'}$. Therefore, the property of simplicity alone is insufficient to guarantee an intermediate degree, demonstrating that a more powerful, computational approach was required [@problem_id:2978713].

### The Priority Method: A Solution to Post's Problem

The definitive, positive solution to Post's Problem was provided independently by Albert Friedberg and Andrei Muchnik in the mid-1950s. They developed a novel and powerful technique known as the **finite-injury priority method**. The core idea is to construct c.e. sets not by defining their global properties, but by building them stage by stage, satisfying an infinite list of requirements along the way.

To construct a c.e. set $A$ of intermediate degree, one must ensure two things:
1.  $A$ is not computable ($\deg(A) > \mathbf{0}$).
2.  $A$ is not Turing-complete ($\deg(A)  \mathbf{0'}$).

By Post's Theorem, an r.e. set $A$ is Turing-complete if and only if $K \le_T A$. Thus, the second condition is equivalent to ensuring $K \not\le_T A$ [@problem_id:2978721]. The full Friedberg-Muchnik construction is even more ambitious: it builds two c.e. sets, $A$ and $B$, that are **Turing-incomparable** ($A \not\le_T B$ and $B \not\le_T A$). The existence of such sets immediately implies a positive answer to Post's problem, as neither $A$ nor $B$ can have degree $\mathbf{0}$ or $\mathbf{0'}$.

Let us outline the construction of these incomparable sets. To ensure incomparability, we must satisfy two infinite families of requirements for every possible Turing reduction, indexed by $e \in \mathbb{N}$:
-   $R_e: \chi_B \neq \Phi_e^A$ (to ensure $B \not\le_T A$)
-   $S_e: \chi_A \neq \Phi_e^B$ (to ensure $A \not\le_T B$)

The construction proceeds in stages $s=0, 1, 2, \dots$, building finite approximations $A_s$ and $B_s$ of the final sets $A = \bigcup_s A_s$ and $B = \bigcup_s B_s$.

#### The Diagonalization Strategy and Its Conflict

Consider a single requirement, say $S_e: \chi_A \neq \Phi_e^B$. The basic strategy is to diagonalize against the purported reduction $\Phi_e^B$.
1.  **Appoint a Witness:** We choose a fresh, large number $x$ (not yet in $A$ or $B$) as a "witness" for $S_e$.
2.  **Wait for Convergence:** We wait for a stage $s$ where the computation $\Phi_{e,s}^{B_s}(x)$ converges, and let's say its output is $0$. At this stage, $\chi_{A_s}(x) = 0$ as well, so the reduction appears to be correct so far.
3.  **Act to Disagree:** To ensure $\chi_A(x) \neq \Phi_e^B(x)$, we can enumerate $x$ into $A$ at stage $s+1$. This makes $\chi_{A_{s+1}}(x) = 1$, creating a disagreement.

The fundamental conflict arises here. The computation $\Phi_{e,s}^{B_s}(x)$ depended on the oracle $B_s$. If, at a later stage, we act to satisfy some other requirement, say $R_j$, by enumerating an element into $B$, we might change the oracle $B$ in a way that alters the outcome of the $\Phi_e^B(x)$ computation. For example, the computation might now diverge, or converge to $1$, destroying the disagreement we worked to create for $S_e$. This event is called an **injury** to the requirement $S_e$.

#### The Priority Solution

The genius of the Friedberg-Muchnik method lies in how it resolves these infinite potential conflicts.

1.  **Priority Ordering:** The requirements are arranged in a fixed linear priority ordering, for instance: $R_0 \succ S_0 \succ R_1 \succ S_1 \succ R_2 \succ S_2 \succ \cdots$. At any stage, only the highest-priority requirement that needs attention is allowed to act [@problem_id:2978719].

2.  **Restraints for Preservation:** When a requirement acts, it imposes a **restraint** to protect its victory. When our strategy for $S_e$ enumerates witness $x$ into $A$ after seeing $\Phi_{e,s}^{B_s}(x) \downarrow = 0$, it notes the **use** of the computation, $u$, which is the largest number queried on the oracle $B_s$. To preserve the computation's outcome, the strategy for $S_e$ now imposes a restraint on $B$: it forbids any number less than or equal to $u$ from entering $B$ for the sake of any requirement with *lower priority* than $S_e$ [@problem_id:2978700] [@problem_id:2978719].

3.  **The Finite-Injury Argument:** This combination of priorities and restraints guarantees that every requirement is ultimately satisfied. Consider any requirement, say $P_k$ in the priority list. It can be injured only by the actions of higher-priority requirements $P_0, \dots, P_{k-1}$. The crucial insight is that each of these higher-priority requirements will act at most once. Once $P_j$ acts and imposes a restraint, it is satisfied forever and will not act again. Therefore, by induction, there is a stage after which all requirements of higher priority than $P_k$ will have finished their work and their restraints will be permanent. After this stage, $P_k$ will never be injured again. It can then choose a permanent witness, wait for convergence, and if it needs to act, it will do so once, imposing its own permanent restraint, and be satisfied forever. Since each requirement is injured only a finite number of times, this is called a **finite-injury** priority argument [@problem_id:2978715].

This elegant mechanism ensures that all requirements $R_e$ and $S_e$ are met, resulting in the successful construction of two non-computable, [computably enumerable](@entry_id:155267), and Turing-incomparable sets. This not only provided a resounding positive answer to Post's Problem but also introduced a powerful toolkit for building complex computable objects.

### The Fine Structure of the c.e. Degrees

The priority method opened the floodgates for a detailed investigation into the structure of $\mathcal{D}_{\text{c.e.}}$. The picture that emerged was one of immense complexity.

#### Low and High Degrees

One way to classify c.e. degrees is by the complexity of their jump. Recall that for any set $A$, we have $\mathbf{0'} \le_T A'$. For a c.e. set $A$, it is also known that $A' \le_T \mathbf{0''}$. These provide lower and [upper bounds](@entry_id:274738) on the complexity of the jump of a c.e. set.

-   A c.e. set $A$ is **low** if its jump is as simple as possible, i.e., $A' \equiv_T \mathbf{0'}$.
-   A c.e. set $A$ is **high** if its jump is as complex as possible, i.e., $A' \equiv_T \mathbf{0''}$. (Note that for c.e. sets, the condition $A' \ge_T \mathbf{0''}$ is equivalent to $A' \equiv_T \mathbf{0''}$.)

Intuitively, a low set is "close to computable" in the sense that relativizing [the halting problem](@entry_id:265241) to it yields no new computational power. A high set, in contrast, is "close to complete," as its own [halting problem](@entry_id:137091) is as complex as [the halting problem](@entry_id:265241) for [the halting problem](@entry_id:265241) ($K' \equiv_T \mathbf{0''}$) [@problem_id:2978710]. These concepts provide another route to solving Post's Problem. If a c.e. set $A$ is low, its degree $\mathbf{a}$ must satisfy $\mathbf{a}' = \mathbf{0'}$. By the Jump Theorem, $\mathbf{a} \lt \mathbf{a}'$. If we had $\mathbf{a}=\mathbf{0'}$, then we would have $\mathbf{a}' = (\mathbf{0'})' = \mathbf{0''} \neq \mathbf{0'}$, a contradiction. Therefore, any low c.e. degree must be strictly below $\mathbf{0'}$. The existence of non-computable low c.e. sets (including low simple sets), proven via priority arguments, provides another construction of intermediate degrees [@problem_id:2978713].

#### Sacks's Density Theorem

A natural question following the discovery of intermediate degrees is: how many are there? Are there pairs of c.e. degrees with nothing in between? Sacks answered this in 1964 with his **Density Theorem**:

 For any two [computably enumerable](@entry_id:155267) degrees $\mathbf{a}$ and $\mathbf{b}$ with $\mathbf{a} \lt \mathbf{b}$, there exists a [computably enumerable](@entry_id:155267) degree $\mathbf{c}$ such that $\mathbf{a} \lt \mathbf{c} \lt \mathbf{b}$.

This theorem states that the [partial order](@entry_id:145467) of c.e. degrees is **dense**. The proof is a significantly more complex priority argument. To construct the intermediate set $C$ with degree $\mathbf{c}$, one must satisfy four families of requirements simultaneously:
1.  $A \le_T C$ (Coding $A$ into $C$)
2.  $C \le_T B$ (Permitting $C$ by $B$)
3.  $C \not\le_T A$ (Diagonalization)
4.  $B \not\le_T C$ (Diagonalization)

The interactions between these requirements are far more intricate than in the Friedberg-Muchnik construction. For example, the need to code $A$ into $C$ conflicts with the restraints imposed to ensure $B \not\le_T C$. These conflicts are managed on a **priority tree**, where different branches correspond to different possible outcomes of strategies. The final result is established by showing that along the "true path" of the construction (the leftmost path visited infinitely often), all requirements are satisfied [@problem_id:2978702].

#### Global Structure and Automorphisms

The array of results proved with priority arguments paints a picture of $\mathcal{D}_{\text{c.e.}}$ as a dense upper semi-lattice with a minimum ($\mathbf{0}$) and maximum ($\mathbf{0'}$). A deep question about any mathematical structure is its symmetry, which is captured by the notion of **automorphisms**. An [automorphism](@entry_id:143521) of $\mathcal{D}_{\text{c.e.}}$ is a bijection $\Phi: \mathcal{D}_{\text{c.e.}} \to \mathcal{D}_{\text{c.e.}}$ that preserves the order relation $\le_T$. Since $\mathcal{D}_{\text{c.e.}}$ is an upper semi-lattice, any order-preserving [bijection](@entry_id:138092) automatically preserves the join operation $\vee$ as well.

Certain properties of degrees are **definable** in the language of partial orders. For example, $\mathbf{0}$ is the unique minimum element and $\mathbf{0'}$ is the unique maximum element. Any automorphism must map an element with a definable property to another element with the same property. Since these properties are unique to $\mathbf{0}$ and $\mathbf{0'}$, any [automorphism](@entry_id:143521) $\Phi$ of $\mathcal{D}_{\text{c.e.}}$ must fix them: $\Phi(\mathbf{0}) = \mathbf{0}$ and $\Phi(\mathbf{0'}) = \mathbf{0'}$ [@problem_id:2978714].

The central open question in this area is the **Rigidity Conjecture**, which posits that $\mathcal{D}_{\text{c.e.}}$ is rigid, meaning the only [automorphism](@entry_id:143521) is the identity map. To date, no non-trivial automorphism has ever been found. Attempts to construct one, for example by defining a map from a permutation $p$ of the indices of c.e. sets, $\Phi_p([W_e]_T) = [W_{p(e)}]_T$, face a severe **well-definedness problem**: for the map to be well-defined on degrees, one must have $W_e \equiv_T W_{e'} \implies W_{p(e)} \equiv_T W_{p(e')}$, a condition that fails for arbitrary computable [permutations](@entry_id:147130). While trivial index permutations that induce the identity automorphism exist, the existence of a permutation inducing a non-trivial automorphism is not known and is widely conjectured to be false [@problem_id:2978714]. This illustrates that despite the power of the priority method to construct individual degrees with specific properties, understanding the global symmetries of the structure they form remains one of the deepest challenges in [computability theory](@entry_id:149179).