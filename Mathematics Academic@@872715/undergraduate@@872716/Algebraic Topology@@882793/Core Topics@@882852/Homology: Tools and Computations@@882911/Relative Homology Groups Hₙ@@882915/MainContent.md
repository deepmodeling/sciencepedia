## Introduction
In algebraic topology, homology groups provide powerful invariants for distinguishing spaces. However, the story is incomplete if we only consider spaces in isolation. A deeper understanding often requires examining how a subspace is embedded within a larger space—a question that absolute homology alone cannot fully answer. This article addresses this gap by introducing [relative homology](@entry_id:159348), a refined tool designed to capture the [topological properties](@entry_id:154666) of a space $X$ "relative to" a subspace $A$.

We will embark on a structured exploration of this concept. The first chapter, **Principles and Mechanisms**, will lay the algebraic groundwork, defining relative chain groups and deriving the pivotal [long exact sequence of a pair](@entry_id:158857). The second chapter, **Applications and Interdisciplinary Connections**, will showcase how this machinery is used to solve concrete geometric problems, compute the homology of spheres, and form the basis for more advanced theories like [cellular homology](@entry_id:157864). Finally, **Hands-On Practices** will offer opportunities to apply these theoretical insights to specific examples, solidifying your understanding of this essential topological tool.

## Principles and Mechanisms

In our exploration of algebraic topology, we have thus far associated homology groups with individual [topological spaces](@entry_id:155056). However, much of the richness of topology comes from understanding the relationship between a space and its subspaces. How does a subspace sit inside a larger space? What features are created when we consider a space but "ignore" what happens inside a given subspace? To answer these questions, we introduce the powerful concept of **[relative homology](@entry_id:159348)**.

### The Algebraic Definition of Relative Homology

Let $(X, A)$ be a **pair of spaces**, which consists of a [topological space](@entry_id:149165) $X$ and a subspace $A \subseteq X$. Our goal is to construct homology groups that capture the topology of $X$ relative to $A$. The construction parallels that of [singular homology](@entry_id:158380), but with a crucial modification at the level of chain groups.

Recall that the singular $n$-chain group of a space $X$, denoted $C_n(X)$, is the free [abelian group](@entry_id:139381) on the set of all singular $n$-[simplices](@entry_id:264881) in $X$. Since $A$ is a subspace of $X$, any [singular simplex](@entry_id:265569) in $A$ is also a [singular simplex](@entry_id:265569) in $X$. This induces an inclusion of chain groups $C_n(A) \hookrightarrow C_n(X)$, allowing us to view $C_n(A)$ as a subgroup of $C_n(X)$.

The fundamental idea of [relative homology](@entry_id:159348) is to treat chains contained entirely in $A$ as trivial. We formalize this by defining the **relative $n$-chain group** as the [quotient group](@entry_id:142790):
$$ C_n(X, A) = \frac{C_n(X)}{C_n(A)} $$
An element of $C_n(X, A)$ is a coset $[c] = c + C_n(A)$, where $c \in C_n(X)$. Two chains $c_1$ and $c_2$ in $X$ represent the same relative chain in $C_n(X, A)$ if and only if their difference, $c_1 - c_2$, is a chain in $A$. Intuitively, we are declaring that we "cannot distinguish" two chains if they only differ by a part that lies within the subspace $A$.

Next, we need a [boundary operator](@entry_id:160216) on these relative chain groups. The standard [boundary operator](@entry_id:160216) $\partial_n: C_n(X) \to C_{n-1}(X)$ maps the subgroup $C_n(A)$ into $C_{n-1}(A)$. This compatibility allows us to define an **induced [boundary operator](@entry_id:160216)** $\bar{\partial}_n: C_n(X, A) \to C_{n-1}(X, A)$ on the [quotient groups](@entry_id:145113) by the rule:
$$ \bar{\partial}_n([c]) = [\partial_n c] $$
A straightforward check confirms that $\bar{\partial}_{n-1} \circ \bar{\partial}_n = 0$, so the sequence of relative chain groups and induced boundary operators forms a [chain complex](@entry_id:150246), $(C_\bullet(X, A), \bar{\partial})$.

With this [chain complex](@entry_id:150246), we can define [relative homology groups](@entry_id:159711) in the standard way:
-   A **relative $n$-cycle** for the pair $(X, A)$ is an element of $\ker(\bar{\partial}_n)$. An element $[c] \in C_n(X, A)$ is a relative cycle if $\bar{\partial}_n([c]) = 0$, which means $[\partial_n c] = 0$. By the definition of the quotient group, this is equivalent to the condition that $\partial_n c \in C_{n-1}(A)$. Thus, a relative $n$-cycle is a chain in $X$ whose boundary lies entirely within the subspace $A$.
-   A **relative $n$-boundary** for the pair $(X, A)$ is an element of $\operatorname{Im}(\bar{\partial}_{n+1})$.

The **$n$-th [relative homology](@entry_id:159348) group** of the pair $(X, A)$ with integer coefficients is then defined as the quotient:
$$ H_n(X, A) = \frac{\ker(\bar{\partial}_n)}{\operatorname{Im}(\bar{\partial}_{n+1})} $$

Let us make this concrete with a foundational example. Consider the pair $(X, A)$ where $X$ is the closed interval $[0,1]$ and $A$ is its boundary subspace $\{0, 1\}$. What does a generator of $H_1(X, A)$ look like? A relative 1-cycle is a 1-chain in $[0,1]$ whose boundary lies in $A$. Let $\sigma: \Delta^1 \to [0,1]$ be the singular 1-[simplex](@entry_id:270623) defined by the identity map $\sigma(t) = t$. This is a path from 0 to 1. Its boundary is $\partial_1 \sigma = \sigma(1) - \sigma(0) = 1 - 0$. Since both 0 and 1 are points in $A$, $\partial_1 \sigma$ is a 0-chain in $A$. Therefore, $\sigma$ is a relative 1-cycle. It is not a relative boundary, as there are no 2-chains in the 1-dimensional space $[0,1]$. Furthermore, any other path from 0 to 1 is homologous to $\sigma$ within this relative context. Thus, the homology class $[\sigma]$ is a generator for $H_1([0,1], \{0,1\}) \cong \mathbb{Z}$ [@problem_id:1670784]. This simple case illustrates the core idea: [relative homology](@entry_id:159348) captures chains that represent paths or surfaces "connecting" points or regions within the subspace $A$.

### The Long Exact Sequence of a Pair

Relative homology groups are rarely computed directly from their definition. Their true power is revealed through their relationship with the absolute homology groups of $X$ and $A$. This relationship is elegantly encapsulated in a fundamental algebraic tool: the **[long exact sequence of a pair](@entry_id:158857)**.

For any pair $(X, A)$, there exists a long exact sequence of [abelian groups](@entry_id:145145):
$$ \dots \to H_n(A) \xrightarrow{i_*} H_n(X) \xrightarrow{j_*} H_n(X, A) \xrightarrow{\partial_*} H_{n-1}(A) \xrightarrow{i_*} H_{n-1}(X) \to \dots \to H_0(X, A) \to 0 $$
The property of **[exactness](@entry_id:268999)** at a group means that the image of the incoming homomorphism is precisely equal to the kernel of the outgoing homomorphism. This single property makes the sequence an incredibly powerful computational and theoretical device. For instance, by definition, [exactness](@entry_id:268999) at $H_n(X)$ means that $\operatorname{Im}(i_*) = \ker(j_*)$ [@problem_id:1670808]. This equality gives us an algebraic formula connecting the three types of homology groups.

Let's examine the homomorphisms in this sequence:
-   The map $i_*: H_n(A) \to H_n(X)$ is induced by the inclusion map $i: A \hookrightarrow X$. It tells us how cycles in $A$ are considered as cycles in the larger space $X$. A cycle in $A$ might become a boundary in $X$, in which case its class would be in $\ker(i_*)$.
-   The map $j_*: H_n(X) \to H_n(X, A)$ is induced by the natural projection of chains $c \in C_n(X)$ to their cosets $[c] \in C_n(X, A)$. It takes a cycle in $X$ and considers it as a relative cycle.
-   The map $\partial_*: H_n(X, A) \to H_{n-1}(A)$ is the **[connecting homomorphism](@entry_id:160713)**. This is the most remarkable piece of the structure. Its definition is geometric and intuitive. A class in $H_n(X,A)$ is represented by a relative $n$-cycle $c$, which is a chain in $X$ with $\partial c \in C_{n-1}(A)$. Since $\partial(\partial c) = 0$, the chain $\partial c$ is itself a cycle in $A$. The [connecting homomorphism](@entry_id:160713) is defined by $\partial_*([c]) = [\partial c] \in H_{n-1}(A)$. It takes a relative cycle in $(X, A)$ and maps it to the homology class of its boundary in $A$.

A classic illustration of the [connecting homomorphism](@entry_id:160713) is the pair $(D^2, S^1)$, where $D^2$ is the closed 2-disk and $S^1$ is its boundary circle [@problem_id:1670811]. The disk itself, viewed as a 2-chain $\iota_{D^2}$, is a relative 2-cycle because its boundary, $\partial \iota_{D^2}$, is a 1-chain representing the circle $S^1$, which lies entirely in the subspace $S^1$. The [connecting homomorphism](@entry_id:160713) $\partial_*: H_2(D^2, S^1) \to H_1(S^1)$ acts on the class $[\iota_{D^2}]$ by taking its boundary. The result is the class $[\partial \iota_{D^2}]$, which is precisely the generator of $H_1(S^1) \cong \mathbb{Z}$. In this case, the [long exact sequence](@entry_id:153438) reveals that $\partial_*$ is an [isomorphism](@entry_id:137127), providing a deep link between the relative 2-homology of the disk and the 1-homology of its boundary.

### Applications and Geometric Interpretations

The long exact sequence (LES) is not merely a theoretical construct; it is the primary engine for computing [relative homology groups](@entry_id:159711) and for deriving profound geometric consequences.

#### Computation via the Long Exact Sequence

If we know the homology of two out of the three spaces ($X$, $A$, and $(X,A)$), the LES often allows us to determine the third. Consider the pair $(S^2, S^1)$, where $S^2$ is the 2-sphere and $S^1$ is its equator [@problem_id:1670806]. We know $H_2(S^2) \cong \mathbb{Z}$, $H_1(S^2)=0$, $H_1(S^1) \cong \mathbb{Z}$, and $H_2(S^1)=0$. Let's examine the relevant portion of the LES:
$$ \underbrace{H_2(S^1)}_{0} \to \underbrace{H_2(S^2)}_{\mathbb{Z}} \to H_2(S^2, S^1) \to \underbrace{H_1(S^1)}_{\mathbb{Z}} \to \underbrace{H_1(S^2)}_{0} $$
This simplifies to the [short exact sequence](@entry_id:137930):
$$ 0 \to \mathbb{Z} \to H_2(S^2, S^1) \to \mathbb{Z} \to 0 $$
For free [abelian groups](@entry_id:145145), such a sequence splits, meaning $H_2(S^2, S^1) \cong \mathbb{Z} \oplus \mathbb{Z}$. Geometrically, this makes sense: the quotient space $S^2/S^1$ is formed by collapsing the equator to a point, which results in two 2-spheres joined at a point (a [wedge sum](@entry_id:270607) $S^2 \vee S^2$), and the second homology of this space is indeed $\mathbb{Z} \oplus \mathbb{Z}$.

Similarly, looking at a lower degree in the sequence:
$$ \dots \to H_1(S^2, S^1) \to \underbrace{H_0(S^1)}_{\mathbb{Z}} \xrightarrow{i_*} \underbrace{H_0(S^2)}_{\mathbb{Z}} \to H_0(S^2, S^1) \to 0 $$
The map $i_*: H_0(S^1) \to H_0(S^2)$ is an [isomorphism](@entry_id:137127) because the inclusion of the equator into the sphere maps the single path-component of $S^1$ to the single path-component of $S^2$. By exactness, this implies $H_1(S^2, S^1)=0$ and $H_0(S^2, S^1)=0$.

#### Homological Conditions and Their Consequences

The LES allows us to translate homological conditions into geometric properties. For instance, what does it mean if all [relative homology groups](@entry_id:159711) of a pair are trivial, i.e., $H_n(X, A) = 0$ for all $n$? The LES for $(X, A)$ becomes:
$$ \dots \to H_n(A) \xrightarrow{i_*} H_n(X) \to 0 \to H_{n-1}(A) \to \dots $$
Exactness at $H_n(X)$ implies that $\operatorname{Im}(i_*) = \ker(0) = H_n(X)$, so $i_*$ is surjective. Exactness at $H_n(A)$ implies that $\ker(i_*) = \operatorname{Im}(0) = 0$, so $i_*$ is injective. Thus, if all [relative homology groups](@entry_id:159711) vanish, the inclusion map $i: A \hookrightarrow X$ induces isomorphisms $H_n(A) \cong H_n(X)$ for all $n$. In this case, $A$ and $X$ are homologically indistinguishable [@problem_id:1670821].

Conversely, what if the subspace $A$ is topologically trivial? Suppose $A$ is **contractible** (homotopy equivalent to a point). Then $H_k(A) = 0$ for all $k \ge 1$. For any $n > 1$, the portion of the LES looks like:
$$ \dots \to \underbrace{H_n(A)}_{0} \to H_n(X) \xrightarrow{j_*} H_n(X, A) \to \underbrace{H_{n-1}(A)}_{0} \to \dots $$
Exactness implies that $j_*: H_n(X) \to H_n(X, A)$ is an [isomorphism](@entry_id:137127) for all $n > 1$ [@problem_id:1670829]. This confirms our intuition: the homology of $X$ relative to a contractible subspace is the same as the homology of $X$ itself (in higher degrees), as we are "quotienting out" a topologically trivial piece. This is a key step in showing that for a "good pair" $(X,A)$, the [relative homology](@entry_id:159348) $H_n(X,A)$ is isomorphic to the [reduced homology](@entry_id:274187) of the quotient space $\tilde{H}_n(X/A)$.

#### Unveiling Hidden Structures

Perhaps most strikingly, [relative homology](@entry_id:159348) can be non-trivial even when the corresponding absolute homology groups are zero. This reveals that [relative homology](@entry_id:159348) detects more subtle relationships about how a subspace is embedded. Consider a solid torus $X = S^1 \times D^2$ and its boundary $A = S^1 \times S^1$ (a 2-torus) [@problem_id:1670830]. Let's look at the third homology groups. Since $X$ is homotopy equivalent to a circle and $A$ is a 2-dimensional surface, their third homology groups are both zero: $H_3(X) = 0$ and $H_3(A)=0$. However, the LES gives us:
$$ \underbrace{H_3(X)}_{0} \to H_3(X, A) \xrightarrow{\partial_*} \underbrace{H_2(A)}_{\mathbb{Z}} \to \underbrace{H_2(X)}_{0} $$
By [exactness](@entry_id:268999), the [connecting homomorphism](@entry_id:160713) $\partial_*: H_3(X, A) \to H_2(A)$ is an isomorphism. Therefore, $H_3(X, A) \cong \mathbb{Z}$.
This non-trivial group has a beautiful geometric meaning. The generator of $H_2(A)$ is the [fundamental class](@entry_id:158335) of the torus surface. This surface does not bound anything *within A*, but it does bound the solid torus $X$. The [relative homology](@entry_id:159348) group $H_3(X,A)$ precisely captures this fact: it contains a class whose boundary is the [fundamental class](@entry_id:158335) of $A$.

As a further exercise, the same LES shows that $H_2(X,A) \cong \ker(i_*: H_1(A) \to H_1(X))$. The map $i_*$ from $H_1(S^1 \times S^1) \cong \mathbb{Z} \oplus \mathbb{Z}$ to $H_1(S^1 \times D^2) \cong \mathbb{Z}$ sends one generator (the meridian loop) to zero, as it bounds a disk in $X$. The kernel is therefore $\mathbb{Z}$, and so $H_2(X,A) \cong \mathbb{Z}$.

Finally, the LES provides a rigorous interpretation for geometric statements. If $H_1(X, A) = 0$, the sequence segment $\dots \to H_1(X) \to H_1(X, A) \to H_0(A) \to \dots$ implies that any path in $X$ whose endpoints lie in $A$ is homologous in $X$ to a path that lies entirely within $A$ [@problem_id:1670828]. This transforms an abstract algebraic condition into a concrete statement about paths.

### Functoriality and Homotopy Invariance

Just like absolute homology, [relative homology](@entry_id:159348) is a functor. A **map of pairs** $f: (X, A) \to (Y, B)$ is a [continuous map](@entry_id:153772) $f: X \to Y$ such that $f(A) \subseteq B$. Such a map induces homomorphisms on the [relative homology groups](@entry_id:159711), $f_*: H_n(X, A) \to H_n(Y, B)$.

For this [induced map](@entry_id:271712) to be well-defined at the chain level, we must ensure that the [chain map](@entry_id:266133) $f_\#: C_n(X) \to C_n(Y)$ gives a [well-defined map](@entry_id:136264) on the quotients, $\bar{f}_\#: C_n(X, A) \to C_n(Y, B)$. This requires that if a chain $c$ is in the subgroup $C_n(A)$, its image $f_\#(c)$ must be in the subgroup $C_n(B)$. This is guaranteed precisely by the condition that $f(A) \subseteq B$, as any [simplex](@entry_id:270623) in $A$ is mapped by $f$ into a [simplex](@entry_id:270623) in $B$ [@problem_id:1670768].

The most important property of this [induced map](@entry_id:271712) is its **homotopy invariance**. If two maps of pairs $f, g: (X, A) \to (Y, B)$ are homotopic through a map of pairs, then they induce the same homomorphism on [relative homology](@entry_id:159348), $f_* = g_*$. A direct and powerful corollary is that if two pairs $(X, A)$ and $(Y, B)$ are **homotopy equivalent as pairs**, then their [relative homology groups](@entry_id:159711) are isomorphic for all $n$:
$$ H_n(X, A) \cong H_n(Y, B) \quad \text{for all } n \ge 0 $$
This principle allows us to compute the [relative homology](@entry_id:159348) of a complicated pair by replacing it with a simpler, homotopy equivalent one. For example, consider the pair $(X,A)$ where $X$ is a cylinder and $A$ is a line segment along its side. This pair can be deformed into the pair $(Y,B)$ where $Y$ is a circle and $B$ is a point on it. By homotopy invariance, $H_n(X,A) \cong H_n(Y,B)$. Using the LES for the simple pair $(S^1, \{\text{pt}\})$, we can easily find that its only non-[trivial homology](@entry_id:265875) is in degree 1, where $H_1(S^1, \{\text{pt}\}) \cong \mathbb{Z}$. Thus, the same must be true for the more complex-looking cylinder-and-line pair [@problem_id:1670773].

In summary, [relative homology groups](@entry_id:159711), defined through a simple algebraic quotient, give rise to a rich theoretical structure centered on the long exact sequence. This sequence not only provides a powerful computational engine but also connects abstract algebra to concrete geometric intuition, allowing us to understand the intricate ways in which spaces and their subspaces relate.