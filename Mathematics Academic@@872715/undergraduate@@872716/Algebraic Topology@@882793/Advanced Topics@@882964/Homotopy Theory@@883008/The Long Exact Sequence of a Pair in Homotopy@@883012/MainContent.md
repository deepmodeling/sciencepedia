## Introduction
In the study of algebraic topology, a central goal is to translate complex geometric questions into more tractable algebraic problems. When dealing with a [topological space](@entry_id:149165) $X$ and a subspace $A$, we are naturally led to ask how the topological features of $A$ relate to those of $X$. The [long exact sequence of a pair](@entry_id:158857) in homotopy is the primary algebraic machine designed to answer this question. It provides a deep and computable relationship between the homotopy groups of $A$, $X$, and the pair $(X, A)$ itself.

This sequence addresses the fundamental problem of quantifying the difference between the homotopy structure of a space and its subspace. It allows us to understand, for instance, which loops in a subspace become contractible in the larger space, or how attaching new geometric pieces to a space alters its homotopy groups.

This article will guide you through this powerful tool in three stages. First, in "Principles and Mechanisms," we will construct the sequence piece by piece, defining the crucial concepts of [relative homotopy groups](@entry_id:261406) and the [connecting homomorphism](@entry_id:160713), and we will unpack the power contained in the algebraic property of exactness. Next, "Applications and Interdisciplinary Connections" will showcase the sequence in action, demonstrating its use in computing challenging homotopy groups and analyzing the structure of [topological spaces](@entry_id:155056), while also linking it to cellular homotopy and homology theory. Finally, "Hands-On Practices" will give you the opportunity to apply these principles to solve concrete problems.

## Principles and Mechanisms

Having introduced the concept of a pair of [topological spaces](@entry_id:155056) $(X, A)$ and the fundamental questions that arise concerning their relationship, we now develop the primary algebraic tool for investigating these questions: the [long exact sequence of a pair](@entry_id:158857) in homotopy. This sequence provides a rigorous and computable link between the homotopy groups of the space $X$, the subspace $A$, and the [relative homotopy groups](@entry_id:261406) that capture the structure of $X$ "relative to" $A$.

### Constructing the Sequence

The long exact sequence is built from three types of groups and the homomorphisms that connect them. The cornerstone of this construction is the definition of [relative homotopy groups](@entry_id:261406).

#### Relative Homotopy Groups

For a pair of topological spaces $(X, A)$ with a chosen basepoint $x_0 \in A$, the **$n$-th relative homotopy group**, denoted $\pi_n(X, A, x_0)$, is the set of homotopy classes of [continuous maps](@entry_id:153855) of pairs $\alpha: (D^n, S^{n-1}, s_0) \to (X, A, x_0)$. Let us unpack this definition.

A representative map $\alpha$ takes the closed $n$-dimensional disk, $D^n$, into the larger space $X$. However, it is constrained on its boundary, the $(n-1)$-sphere $S^{n-1}$, which must be mapped entirely into the subspace $A$. Furthermore, a designated basepoint $s_0$ on the boundary $S^{n-1}$ must map to the basepoint $x_0$ of our pair, so $\alpha(s_0) = x_0$. Two such maps, $\alpha_0$ and $\alpha_1$, are considered homotopic if there exists a continuous family of maps $H_t: (D^n, S^{n-1}) \to (X, A)$ connecting them, such that for every $t \in [0,1]$, the boundary condition $H_t(S^{n-1}) \subseteq A$ is maintained.

For $n \ge 2$, the set $\pi_n(X, A, x_0)$ forms a group under a composition rule analogous to that for absolute homotopy groups. For $n=1$, it is a pointed set. These groups measure how $n$-dimensional spheres can be mapped into $X$ with their "equator" (or a similar boundary) confined to $A$.

#### The Three Fundamental Homomorphisms

The [long exact sequence](@entry_id:153438) braids together the absolute homotopy groups $\pi_n(A)$ and $\pi_n(X)$ with the relative groups $\pi_n(X, A)$ via three fundamental homomorphisms. For simplicity, we will often suppress the basepoint from the notation.

1.  **The Inclusion-Induced Map $i_*$**: The inclusion map $i: A \hookrightarrow X$ is continuous. Any map representing an element of $\pi_n(A)$, say $\alpha: S^n \to A$, can be composed with $i$ to yield a map $i \circ \alpha: S^n \to X$, which represents an element of $\pi_n(X)$. This defines a homomorphism $i_*: \pi_n(A) \to \pi_n(X)$. This map simply treats a loop or sphere in $A$ as a loop or sphere in the larger space $X$.

2.  **The Relative Inclusion Map $j_*$**: An element of $\pi_n(X)$ is represented by a map $\beta: S^n \to X$. We can view this as a map of pairs $\beta: (S^n, \emptyset) \to (X, A)$. Using the fact that $S^n$ is homeomorphic to $D^n / S^{n-1}$, we can construct a representative map $(D^n, S^{n-1}) \to (X, A)$ where the entire boundary $S^{n-1}$ is mapped to the basepoint $x_0 \in A$. This process defines a homomorphism $j_*: \pi_n(X) \to \pi_n(X, A)$, which essentially takes a sphere in $X$ and views it as a "relative sphere" whose boundary is trivially contained in $A$.

3.  **The Connecting Homomorphism $\partial$**: This is the most crucial and least obvious map in the sequence. It connects groups of different dimensions, making the sequence long. Given an element $[\alpha] \in \pi_n(X, A)$ represented by a map $\alpha: (D^n, S^{n-1}) \to (X, A)$, the [connecting homomorphism](@entry_id:160713) $\partial$ is defined by restricting $\alpha$ to its boundary. The map $\alpha|_{S^{n-1}}: S^{n-1} \to A$ represents an element in $\pi_{n-1}(A)$. We define $\partial([\alpha]) = [\alpha|_{S^{n-1}}]$. This provides a homomorphism $\partial: \pi_n(X, A) \to \pi_{n-1}(A)$.

The geometric meaning of $\partial$ is profound [@problem_id:1687525]. It takes a relative $n$-cell in $X$ and extracts its boundary, which is an $(n-1)$-sphere living entirely inside $A$. Consequently, an element $[\alpha] \in \pi_n(X, A)$ lies in the **kernel** of $\partial$ if and only if its boundary map, $\alpha|_{S^{n-1}}$, is [null-homotopic](@entry_id:153762) within $A$ [@problem_id:1687518]. This means the boundary, while geometrically present, is homotopically trivial from the perspective of the subspace $A$.

#### Statement of the Long Exact Sequence

These groups and homomorphisms fit together into a sequence that extends infinitely in one direction:
$$ \dots \to \pi_n(A) \xrightarrow{i_*} \pi_n(X) \xrightarrow{j_*} \pi_n(X, A) \xrightarrow{\partial} \pi_{n-1}(A) \xrightarrow{i_*} \pi_{n-1}(X) \to \dots \to \pi_1(X, A) \xrightarrow{\partial} \pi_0(A) $$
The remarkable property of this sequence is that it is **exact**.

### The Power of Exactness: A User's Guide

The statement that the sequence is "exact" is a concise algebraic declaration with powerful geometric consequences. At any group $G_k$ in the sequence $\dots \to G_{k+1} \xrightarrow{f} G_k \xrightarrow{g} G_{k-1} \to \dots$, exactness means that the image of the incoming map is equal to the kernel of the outgoing map: $\operatorname{Im}(f) = \operatorname{Ker}(g)$.

Let's explore what this means at each position in our homotopy sequence.

-   **Exactness at $\pi_n(X)$**: We have the segment $\pi_n(A) \xrightarrow{i_*} \pi_n(X) \xrightarrow{j_*} \pi_n(X, A)$. Exactness here means $\operatorname{Im}(i_*) = \operatorname{Ker}(j_*)$. Geometrically, this says that a sphere in $X$ becomes homotopically trivial when viewed as a relative sphere in $(X, A)$ if and only if it is homotopic to a sphere that came from the subspace $A$.

-   **Exactness at $\pi_n(X, A)$**: For the segment $\pi_n(X) \xrightarrow{j_*} \pi_n(X, A) \xrightarrow{\partial} \pi_{n-1}(A)$, exactness implies $\operatorname{Im}(j_*) = \operatorname{Ker}(\partial)$. This tells us that a relative $n$-cell has a homotopically trivial boundary in $A$ if and only if it is homotopic (as a relative cell) to a sphere that came from $X$ via the map $j_*$.

-   **Exactness at $\pi_n(A)$**: For $\pi_{n+1}(X, A) \xrightarrow{\partial} \pi_n(A) \xrightarrow{i_*} \pi_n(X)$, we have $\operatorname{Im}(\partial) = \operatorname{Ker}(i_*)$. This is one of the most useful parts of the sequence. It states that an $n$-sphere in $A$ becomes [null-homotopic](@entry_id:153762) when considered in the larger space $X$ if and only if it is the boundary of some relative $(n+1)$-cell in $(X, A)$.

This final point allows us to deduce information about one map from another. For example, if we know that the map $i_*: \pi_k(A) \to \pi_k(X)$ is not injective for some $k$, its kernel must be non-trivial. By [exactness](@entry_id:268999), this immediately implies that the image of $\partial: \pi_{k+1}(X, A) \to \pi_k(A)$ must be precisely this non-trivial kernel, and therefore $\partial$ cannot be the zero map [@problem_id:1687535]. Conversely, if $i_*: \pi_n(A) \to \pi_n(X)$ is surjective, the First Isomorphism Theorem for groups implies $\pi_n(A) / \ker(i_*) \cong \pi_n(X)$. Using exactness, we can substitute $\ker(i_*) = \operatorname{Im}(\partial)$, which yields the remarkable conclusion that the cokernel of the boundary map, $\pi_n(A) / \operatorname{Im}(\partial)$, is isomorphic to $\pi_n(X)$ [@problem_id:1687574].

### Canonical Applications and Computations

The true utility of the [long exact sequence](@entry_id:153438) is revealed when we apply it to specific pairs of spaces. Often, one of the spaces in the pair $(X, A)$ has a simple homotopy structure, causing parts of the sequence to vanish and revealing isomorphisms between the remaining groups.

#### Contractible Spaces

A contractible space is homotopy equivalent to a point, meaning all its homotopy groups $\pi_k$ are trivial for $k \ge 1$.

-   **Contractible Subspace $A$**: If $A$ is a contractible subspace, then $\pi_n(A) = 0$ for all $n \ge 1$. The [long exact sequence](@entry_id:153438) contains segments of the form:
    $$ \dots \to \pi_n(A) \to \pi_n(X) \to \pi_n(X, A) \to \pi_{n-1}(A) \to \dots $$
    Substituting the trivial groups, we get:
    $$ \dots \to 0 \to \pi_n(X) \xrightarrow{j_*} \pi_n(X, A) \to 0 \to \dots $$
    Exactness at $\pi_n(X)$ means $\ker(j_*)$ is the image of the map from the zero group, so $\ker(j_*) = 0$ and $j_*$ is injective. Exactness at $\pi_n(X, A)$ means $\operatorname{Im}(j_*)$ is the kernel of the map to the zero group, so $\operatorname{Im}(j_*) = \pi_n(X, A)$ and $j_*$ is surjective. Thus, for all $n \ge 2$, $j_*: \pi_n(X) \to \pi_n(X, A)$ is an isomorphism. A careful check of the sequence at the low-dimensional end confirms this also holds for $n=1$ [@problem_id:1687534].
    A key instance of this is the pair $(X, \{x_0\})$, where the subspace is a single point (which is contractible). The sequence gives $\pi_n(X, \{x_0\}) \cong \pi_n(X, x_0)$ for $n \ge 2$, confirming that [relative homotopy groups](@entry_id:261406) are a natural generalization of absolute ones.

-   **Contractible Space $X$**: If the [ambient space](@entry_id:184743) $X$ is contractible, then $\pi_n(X) = 0$ for all $n \ge 1$. The sequence now contains segments like:
    $$ \dots \to \pi_n(X) \to \pi_n(X, A) \to \pi_{n-1}(A) \to \pi_{n-1}(X) \to \dots $$
    Substituting the trivial groups gives:
    $$ \dots \to 0 \to \pi_n(X, A) \xrightarrow{\partial} \pi_{n-1}(A) \to 0 \to \dots $$
    By the same logic as before, $\partial: \pi_n(X, A) \to \pi_{n-1}(A)$ must be an [isomorphism](@entry_id:137127) for all $n \ge 2$ [@problem_id:1687563]. This "dimension-shifting" isomorphism is an incredibly powerful computational tool. For instance, by considering the pair $(D^n, S^{n-1})$, where $D^n$ is a contractible disk, we immediately get $\pi_k(D^n, S^{n-1}) \cong \pi_{k-1}(S^{n-1})$. This relationship is a cornerstone of the methods used to compute the famously complex homotopy groups of spheres.

#### Other Simplifying Conditions

-   **Trivial Relative Homotopy Groups**: Suppose a pair $(X, A)$ has the property that all its [relative homotopy groups](@entry_id:261406) $\pi_k(X, A)$ are trivial for $k \ge 1$. This implies that any sphere in $X$ with its equator in $A$ can be deformed, relative to $A$, to a sphere entirely within $A$. The [long exact sequence](@entry_id:153438) becomes:
    $$ \dots \to \pi_n(A) \xrightarrow{i_*} \pi_n(X) \to 0 \to \pi_{n-1}(A) \xrightarrow{i_*} \pi_{n-1}(X) \to \dots $$
    For any $n \ge 1$, we look at the segment centered on $\pi_n(X)$: $ \pi_n(A) \xrightarrow{i_*} \pi_n(X) \to \pi_n(X,A)=0 $. Exactness implies $i_*$ is surjective. Now look at the segment centered on $\pi_n(A)$: $ \pi_{n+1}(X,A)=0 \to \pi_n(A) \xrightarrow{i_*} \pi_n(X) $. Exactness implies $i_*$ is injective. Therefore, $i_*: \pi_n(A) \to \pi_n(X)$ is an [isomorphism](@entry_id:137127) for all $n \ge 1$ [@problem_id:1687536]. This result, a special case of the Whitehead Theorem, tells us that if a space has no "relative homotopy" with respect to a subspace, then the subspace captures all the homotopy information of the ambient space.

-   **Subspaces with Trivial Higher Homotopy**: Consider a pair $(X, A)$ where $\pi_k(A) = 0$ for all $k \ge 1$. This is weaker than contractibility, as $A$ might not be path-connected (i.e., $\pi_0(A)$ could be non-trivial). For $n \ge 2$, the situation is identical to the contractible case, as both $\pi_n(A)$ and $\pi_{n-1}(A)$ are trivial. This yields an [isomorphism](@entry_id:137127) $j_*: \pi_n(X) \xrightarrow{\cong} \pi_n(X, A)$ for all $n \ge 2$. However, for $n=1$, the sequence is:
    $$ \dots \to \pi_1(A)=0 \to \pi_1(X) \xrightarrow{j_*} \pi_1(X, A) \xrightarrow{\partial} \pi_0(A) \to \dots $$
    Exactness at $\pi_1(X)$ implies $j_*$ is injective. But since $\pi_0(A)$ is not necessarily a single point, $\partial$ may not be the zero map. Therefore, $\operatorname{Im}(j_*) = \ker(\partial)$ may be a [proper subgroup](@entry_id:141915) of $\pi_1(X, A)$, meaning $j_*$ is not necessarily surjective [@problem_id:1687555]. This subtlety highlights the importance of analyzing the entire sequence.

### Structural Properties of the Sequence

Beyond its computational power, the long exact sequence possesses fundamental structural properties that ensure its consistency and wide applicability.

#### Naturality

The construction of the [long exact sequence](@entry_id:153438) is **natural**. This means that it respects maps between pairs of spaces. Let $f: (X, A) \to (Y, B)$ be a continuous map of pairs (meaning $f:X \to Y$ and $f(A) \subseteq B$). This single map induces a homomorphism between each corresponding group in the respective long [exact sequences](@entry_id:151503). Naturality asserts that these induced maps form a "ladder," where every square commutes.

$$
\begin{array}{ccccccc}
\dots \to  \pi_n(A)  \xrightarrow{i_{X*}}  \pi_n(X)  \xrightarrow{j_{X*}}  \pi_n(X, A)  \xrightarrow{\partial_X}  \pi_{n-1}(A)  \to \dots \\
 \downarrow f_{A*}   \downarrow f_{X*}   \downarrow f_*   \downarrow f_{A*}  \\
\dots \to  \pi_n(B)  \xrightarrow{i_{Y*}}  \pi_n(Y)  \xrightarrow{j_{Y*}}  \pi_n(Y, B)  \xrightarrow{\partial_Y}  \pi_{n-1}(B)  \to \dots
\end{array}
$$

The most significant part of this statement is the commutativity of the square involving the connecting homomorphisms: $f_{A*} \circ \partial_X = \partial_Y \circ f_*$. Let's verify this from the geometric definitions [@problem_id:1687538]. Take an element $[\alpha] \in \pi_n(X, A)$.
- Following the top-right path, we first apply $\partial_X$ to get $[\alpha|_{S^{n-1}}] \in \pi_{n-1}(A)$, then apply $f_{A*}$ to get $[f \circ (\alpha|_{S^{n-1}})] \in \pi_{n-1}(B)$.
- Following the left-bottom path, we first apply $f_*$ to get $[f \circ \alpha] \in \pi_n(Y, B)$, then apply $\partial_Y$ to get the class of its boundary, which is $[(f \circ \alpha)|_{S^{n-1}}] \in \pi_{n-1}(B)$.
Since [composition of functions](@entry_id:148459) is associative, $f \circ (\alpha|_{S^{n-1}}) = (f \circ \alpha)|_{S^{n-1}}$, so the two paths yield the same result. This [naturality](@entry_id:270302) ensures that relationships derived from the sequence are preserved under maps, making it a robust theoretical tool.

### A Deeper Perspective: The Puppe Sequence (Advanced)

The [long exact sequence of a pair](@entry_id:158857) is not an isolated miracle. It arises as a special case of a more general construction in homotopy theory. For any based map $i: A \to X$, one can construct its **[mapping cone](@entry_id:261103)**, $C_i$. This space is formed by taking the cylinder on $A$ and gluing its base to $X$ along the map $i$. This construction gives rise to the **Puppe sequence**:
$$ A \xrightarrow{i} X \xrightarrow{q} C_i \xrightarrow{\delta} \Sigma A \xrightarrow{\Sigma i} \Sigma X \to \dots $$
Here, $q$ is the inclusion of $X$ into the cone, $\Sigma$ denotes the [reduced suspension](@entry_id:264688), and $\delta$ is a map that collapses $X$ inside $C_i$ to a point, producing a suspension of $A$.

Applying the functor $\pi_k(-)$ to this sequence of spaces and maps yields a [long exact sequence of homotopy groups](@entry_id:273540). The key insight is that for the pair $(X, A)$, where $i$ is the inclusion, there is a canonical homotopy equivalence between the [mapping cone](@entry_id:261103) $C_i$ and the [quotient space](@entry_id:148218) $X/A$ (under suitable conditions). The [relative homotopy groups](@entry_id:261406) are related to absolute groups of this [quotient space](@entry_id:148218). More directly, there is an isomorphism $\pi_n(X, A) \cong \pi_n(C_i)$ for $n \ge 2$.

Under this identification, the maps in the long exact sequence of the pair correspond to maps in the [long exact sequence](@entry_id:153438) from the Puppe construction. Most revealing is the nature of the [connecting homomorphism](@entry_id:160713) $\partial_n: \pi_n(X, A) \to \pi_{n-1}(A)$. It corresponds precisely to the composition of the map $\delta_*: \pi_n(C_i) \to \pi_n(\Sigma A)$ from the Puppe sequence and the [suspension isomorphism](@entry_id:156388) $S_n: \pi_n(\Sigma A) \xrightarrow{\cong} \pi_{n-1}(A)$. That is, up to a sign convention, we have the identification [@problem_id:1687519]:
$$ \partial_n \longleftrightarrow S_n \circ \delta_* $$
This reveals that the mysterious dimension-shifting boundary map of the pair sequence is, from a more abstract viewpoint, a composition of a geometrically natural collapse map ($\delta$) and a fundamental isomorphism of homotopy theory (the [suspension isomorphism](@entry_id:156388)). This deeper connection situates the [long exact sequence of a pair](@entry_id:158857) within the powerful and general framework of [cofibrations](@entry_id:276022) and their associated Puppe sequences.