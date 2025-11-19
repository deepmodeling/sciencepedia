## Introduction
In the field of algebraic topology, one of the primary goals is to distinguish and classify [topological spaces](@entry_id:155056) using algebraic invariants. While the absolute homology of a space provides a powerful signature, it often fails to capture the intricate relationship between a space and its subspaces. How does the topology of a subspace $A$ influence the topology of the larger space $X$? To answer this, topologists developed the concept of [relative homology](@entry_id:159348), which focuses on the topological features of $X$ that are not contained within $A$. The central tool for understanding and computing this relationship is the [long exact sequence of a pair](@entry_id:158857).

This article provides a detailed exploration of this foundational structure. It addresses the challenge of bridging the gap between the known homology of a space and its subspace by introducing a canonical, interlocking sequence of groups and homomorphisms. By navigating this sequence, we can extract profound insights and perform complex computations that would otherwise be intractable.

The journey through this topic is structured into three main chapters. In "Principles and Mechanisms," you will learn the formal definition of the [long exact sequence](@entry_id:153438), dissect its constituent maps—including the critical [connecting homomorphism](@entry_id:160713)—and explore the deep geometric meaning behind its algebraic exactness. Following this, "Applications and Interdisciplinary Connections" will demonstrate the sequence's power in action, from calculating the homology of spheres and proving the non-existence of retractions to its surprising connections with knot theory and homotopy groups. Finally, "Hands-On Practices" will give you the opportunity to solidify your understanding by working through concrete problems and computations. We begin by constructing the algebraic engine that drives all of these applications: the [long exact sequence](@entry_id:153438) itself.

## Principles and Mechanisms

The transition from absolute to [relative homology](@entry_id:159348) is one of the most powerful steps in algebraic topology. It allows us to isolate the topological features of a space $X$ relative to a subspace $A$, providing a potent tool for both computation and theoretical development. Central to this theory is the existence of a canonical algebraic structure known as the [long exact sequence of a pair](@entry_id:158857). This chapter will detail the structure of this sequence, explore the geometric meaning of its constituent maps, and demonstrate its profound consequences through a series of foundational results and applications.

### The Structure of the Long Exact Sequence

For any pair of topological spaces $(X, A)$ where $A$ is a subspace of $X$, there exists a long exact sequence of [singular homology](@entry_id:158380) groups with integer coefficients. This sequence connects the homology of $A$, the homology of $X$, and the [relative homology](@entry_id:159348) of the pair $(X, A)$ in a precise, interlocking pattern. It is given by the following infinite sequence of [abelian groups](@entry_id:145145) and group homomorphisms:

$$ \dots \to H_{n+1}(X, A) \xrightarrow{\partial_{n+1}} H_n(A) \xrightarrow{i_*} H_n(X) \xrightarrow{j_*} H_n(X, A) \xrightarrow{\partial_n} H_{n-1}(A) \to \dots $$

The maps in this sequence are fundamental:

1.  The map $i_*: H_n(A) \to H_n(X)$ is induced by the **inclusion map** $i: A \hookrightarrow X$. It takes a homology class in $A$ and considers it as a homology class in the larger space $X$.

2.  The map $j_*: H_n(X) \to H_n(X, A)$ is induced by the inclusion of pairs $j: (X, \emptyset) \hookrightarrow (X, A)$. It takes a cycle in $X$ and views it as a relative cycle in $(X, A)$.

3.  The map $\partial_n: H_n(X, A) \to H_{n-1}(A)$ is the **[connecting homomorphism](@entry_id:160713)**. Its construction is less immediate but forms the crucial link between different dimensions. A [relative homology](@entry_id:159348) class in $H_n(X, A)$ is represented by an $n$-chain $c$ in $X$ whose boundary, $\partial c$, is an $(n-1)$-chain entirely contained within $A$. The [connecting homomorphism](@entry_id:160713) maps the class of $c$ to the class of its boundary, $[\partial c]$, in $H_{n-1}(A)$. One can show this map is well-defined.

The most important property of this sequence is its **exactness**. An exact sequence is a sequence of groups and homomorphisms such that at each group, the image of the incoming map is precisely equal to the kernel of the outgoing map. For instance, exactness at the group $H_n(A)$ in the sequence above means that the kernel of the map $i_*: H_n(A) \to H_n(X)$ is identical to the image of the [connecting homomorphism](@entry_id:160713) $\partial_{n+1}: H_{n+1}(X, A) \to H_n(A)$. That is, $\ker(i_*) = \operatorname{im}(\partial_{n+1})$ [@problem_id:1687323]. This single property is the engine that drives nearly all applications of the sequence.

### Geometric Interpretation of the Sequence

The algebraic definition of [exactness](@entry_id:268999) has profound geometric content. By understanding what each map and its [kernel and image](@entry_id:151957) represent, we can translate the algebraic machinery into topological insight.

Let us focus on the segment $H_n(A) \xrightarrow{i_*} H_n(X) \xrightarrow{j_*} H_n(X, A)$. Exactness at $H_n(X)$ asserts that $\operatorname{im}(i_*) = \ker(j_*)$. What does it mean for a homology class $[z] \in H_n(X)$ to be in the image of $i_*$? By definition, it means there exists a class $[w] \in H_n(A)$ such that $i_*([w]) = [z]$. Geometrically, this signifies that the $n$-cycle $z$ in $X$ is homologous to a cycle $w$ that is contained entirely within the subspace $A$ [@problem_id:1687270].

Now consider the condition $[z] \in \ker(j_*)$. This means that the image of $[z]$ in the [relative homology](@entry_id:159348) group $H_n(X, A)$ is zero. This happens if the cycle $z$, when considered as a relative cycle, is the boundary of some $(n+1)$-chain relative to $A$. The exactness condition $\operatorname{im}(i_*) = \ker(j_*)$ thus provides a beautiful equivalence: a homology class in $X$ is trivial in the relative sense if and only if it is homologous to a class coming from the subspace $A$.

The [connecting homomorphism](@entry_id:160713) $\partial$ also has a clear geometric meaning, best illustrated by a classic example. Consider the pair $(D^n, S^{n-1})$, the closed $n$-disk and its boundary sphere, for $n \ge 1$. The group $H_n(D^n, S^{n-1})$ can be shown to be isomorphic to $\mathbb{Z}$, generated by a class $[\sigma]$ which can be visualized as the disk itself. This class is represented by a relative cycle $\sigma$ (e.g., a single $n$-simplex filling the disk) whose boundary lies in $S^{n-1}$. The [connecting homomorphism](@entry_id:160713) $\partial_*: H_n(D^n, S^{n-1}) \to H_{n-1}(S^{n-1})$ acts on this generator by taking its boundary. The boundary of the entire $n$-disk is its boundary sphere, $S^{n-1}$. Therefore, $\partial_*([\sigma])$ is the homology class in $H_{n-1}(S^{n-1})$ represented by the sphere itself, which is a generator of $H_{n-1}(S^{n-1}) \cong \mathbb{Z}$ (for $n \ge 2$). In fact, the [long exact sequence](@entry_id:153438) for this pair shows that this [connecting homomorphism](@entry_id:160713) is an isomorphism. This provides a fundamental link between the [relative homology](@entry_id:159348) of a disk and the absolute homology of its boundary sphere [@problem_id:1687313].

### Applications and Consequences of Exactness

The rigid structure imposed by exactness allows us to deduce powerful conclusions about homology groups by "chasing" elements around the sequence diagram.

A primary application is to understand the relationship between absolute and [relative homology](@entry_id:159348). Suppose we have a pair $(X, A)$ where all [relative homology groups](@entry_id:159711) are trivial, i.e., $H_n(X, A) = \{0\}$ for all $n \ge 0$. Let's examine a segment of the long exact sequence:
$$ H_{n+1}(X, A) \to H_n(A) \xrightarrow{i_*} H_n(X) \to H_n(X, A) $$
Substituting our assumption, this becomes:
$$ \{0\} \to H_n(A) \xrightarrow{i_*} H_n(X) \to \{0\} $$
Exactness at $H_n(A)$ implies $\ker(i_*) = \operatorname{im}(\{0\} \to H_n(A)) = \{0\}$, so $i_*$ is injective. Exactness at $H_n(X)$ implies $\operatorname{im}(i_*) = \ker(H_n(X) \to \{0\}) = H_n(X)$, so $i_*$ is surjective. A map that is both injective and surjective is an isomorphism. Therefore, if all [relative homology groups](@entry_id:159711) of a pair vanish, the inclusion map induces an [isomorphism](@entry_id:137127) on all absolute homology groups: $H_n(A) \cong H_n(X)$ for all $n$ [@problem_id:1687281]. This shows that, from the perspective of homology, the space $X$ is equivalent to the subspace $A$.

We can perform more subtle analyses. Suppose we only know that for a specific integer $k$, the map $i_*: H_k(A) \to H_k(X)$ is an isomorphism. The long exact sequence allows us to precisely describe the [relative homology groups](@entry_id:159711) in adjacent dimensions in terms of the inclusion maps in other dimensions [@problem_id:1687285]. A careful diagram chase reveals:
- $H_k(X,A) \cong \ker(i_*: H_{k-1}(A) \to H_{k-1}(X))$
- $H_{k+1}(X,A) \cong \operatorname{coker}(i_*: H_{k+1}(A) \to H_{k+1}(X))$, where the cokernel of a map $f: G \to H$ is defined as $H/\operatorname{im}(f)$.
This remarkable result shows that the [relative homology groups](@entry_id:159711) measure the failure of the inclusion map to be an isomorphism in adjacent degrees.

As a final example of this type of reasoning, consider the case where the [connecting homomorphism](@entry_id:160713) $\partial: H_n(X, A) \to H_{n-1}(A)$ is an isomorphism for some $n > 0$. The long exact sequence again yields significant structural information. By analyzing the segments centered around $H_n(X)$ and $H_{n-1}(X)$, we can deduce that $i_*: H_n(A) \to H_n(X)$ must be surjective, making $H_n(X)$ a quotient group of $H_n(A)$. Furthermore, we find that $j_*: H_{n-1}(X) \to H_{n-1}(X, A)$ must be injective, meaning $H_{n-1}(X)$ is isomorphic to a subgroup of $H_{n-1}(X, A)$ [@problem_id:1687296]. These examples demonstrate the deep interconnections that the long exact sequence establishes among the various homology groups.

### Naturality and Structural Theorems

The [long exact sequence](@entry_id:153438) is not just a property of a single pair; it is a **natural** construction. This means it respects maps between pairs. A [continuous map](@entry_id:153772) $f: X \to Y$ that sends a subspace $A \subset X$ into a subspace $B \subset Y$ is called a **map of pairs**, denoted $f: (X, A) \to (Y, B)$. Such a map induces homomorphisms between the respective homology groups, which arrange themselves into a commutative diagram, often called a "ladder":

$$
\begin{array}{ccccccc}
\dots \to  H_n(A)  \xrightarrow{i_*}  H_n(X)  \xrightarrow{j_*}  H_n(X,A)  \to \dots \\
 \downarrow f_A   \downarrow f_*   \downarrow f_{rel}  \\
\dots \to  H_n(B)  \xrightarrow{i_*}  H_n(Y)  \xrightarrow{j_*}  H_n(Y,B)  \to \dots
\end{array}
$$

The statement that this diagram commutes means that for any square, composing the maps along either path from the top-left to the bottom-right corner yields the same result. This [naturality](@entry_id:270302) property, combined with a powerful algebraic tool called the **Five Lemma**, has profound implications. The Five Lemma states that for such a commutative ladder with exact rows, if four of the five vertical maps are isomorphisms, then the middle one must also be an [isomorphism](@entry_id:137127).

Applying this to our homology ladder, suppose the map of pairs $f: (X, A) \to (Y, B)$ induces isomorphisms $f_A: H_n(A) \to H_n(B)$ and $f_*: H_n(X) \to H_n(Y)$ for all $n$. The Five Lemma then immediately implies that the [induced map](@entry_id:271712) on [relative homology](@entry_id:159348), $f_{rel}: H_n(X, A) \to H_n(Y, B)$, must also be an isomorphism for all $n$ [@problem_id:1687291]. This provides a standard method for proving that two [relative homology groups](@entry_id:159711) are isomorphic.

Naturality also manifests in other contexts. For instance, if a group $G$ acts on a CW pair $(X, A)$, each element $g \in G$ defines a map of pairs $g: (X, A) \to (X, A)$. Naturality ensures that all maps in the [long exact sequence](@entry_id:153438) are $G$-module homomorphisms. In particular, the [connecting homomorphism](@entry_id:160713) respects the action: $\partial(g \cdot z) = g \cdot \partial(z)$ for any class $z \in H_n(X, A)$ [@problem_id:1687273].

A special structural result occurs when the subspace $A$ is a **retract** of $X$. This means there is a [continuous map](@entry_id:153772) $r: X \to A$ such that $r(a) = a$ for all $a \in A$. On the level of homology, the [induced map](@entry_id:271712) $r_*: H_n(X) \to H_n(A)$ serves as a left-inverse to $i_*: H_n(A) \to H_n(X)$, since $r_* \circ i_* = (r \circ i)_* = (\text{id}_A)_* = \text{id}$. The existence of this left-inverse implies that the short [exact sequences](@entry_id:151503) that make up the [long exact sequence](@entry_id:153438) will *split*. For each $n$, we have a [short exact sequence](@entry_id:137930):
$$ 0 \to H_n(A) \xrightarrow{i_*} H_n(X) \xrightarrow{j_*} H_n(X, A) \to 0 $$
The splitting of this sequence implies a [direct sum decomposition](@entry_id:263004): $H_n(X) \cong H_n(A) \oplus H_n(X, A)$. This provides a complete description of the homology of $X$ in terms of the homology of $A$ and the [relative homology](@entry_id:159348) of the pair [@problem_id:1687271].

### Generalization: The Long Exact Sequence of a Triple

The concept of a long exact sequence can be extended to a **triple** of spaces $(X, A, B)$ where $B \subset A \subset X$. This gives rise to a [long exact sequence](@entry_id:153438) connecting the [relative homology groups](@entry_id:159711) of the pairs $(A, B)$, $(X, B)$, and $(X, A)$:

$$ \dots \to H_n(A, B) \xrightarrow{i_*} H_n(X, B) \xrightarrow{j_*} H_n(X, A) \xrightarrow{\partial} H_{n-1}(A, B) \to \dots $$

Here, $i_*$ and $j_*$ are induced by the obvious inclusion maps of pairs. The new [connecting homomorphism](@entry_id:160713) $\partial$ can be thought of as taking a class in $H_n(X,A)$ represented by a chain $c \in C_n(X)$ with $\partial c \in C_{n-1}(A)$, and mapping it to the class of $\partial c$ in $H_{n-1}(A,B)$.

This sequence is a powerful computational tool. For instance, consider the triple $(X, A, B) = (D^3, S^2, S^1)$, where $D^3$ is the 3-ball, $S^2$ is its boundary, and $S^1$ is the equator of the sphere. We can use the long exact sequence of this triple to compute the homology groups $H_n(X, A) = H_n(D^3, S^2)$. Given information about the homology of the other pairs, $(A, B)=(S^2, S^1)$ and $(X, B)=(D^3, S^1)$, we can substitute these known groups into the sequence and use [exactness](@entry_id:268999) to solve for the unknown groups $H_n(D^3, S^2)$. This process might reveal, for example, that $H_3(D^3, S^2) \cong \mathbb{Z}$ and $H_2(D^3, S^2) = 0$, demonstrating the sequence's utility in breaking down complex topological problems into more manageable algebraic ones [@problem_id:1687320].

In summary, the [long exact sequence of a pair](@entry_id:158857) is a fundamental and indispensable structure in algebraic topology. It provides a bridge between the homology of a space, a subspace, and their relative structure, enabling computation, proving foundational theorems, and providing deep geometric insight.