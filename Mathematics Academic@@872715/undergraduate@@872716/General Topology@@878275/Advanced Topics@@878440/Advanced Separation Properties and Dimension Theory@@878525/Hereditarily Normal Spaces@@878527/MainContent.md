## Introduction
In the classification of [topological spaces](@entry_id:155056), [separation axioms](@entry_id:154482) provide a crucial ladder of increasing structural refinement. Among these, normality stands out for its role in proving foundational theorems. A natural question in topology is how properties behave when restricted to subspaces. While many properties are hereditary, passed down to every subspace, normality surprisingly is not. This failure reveals a gap in our topological toolkit and necessitates the introduction of a stronger, more robust property: hereditary normality.

This article provides a comprehensive exploration of hereditarily [normal spaces](@entry_id:154073). The journey is structured into three parts. In "Principles and Mechanisms," we will first demonstrate why normality is not hereditary using the classic Tychonoff plank counterexample, then formally define hereditary normality and introduce its powerful equivalent characterization as complete normality. In "Applications and Interdisciplinary Connections," we will investigate which spaces possess this property—including the broad classes of metrizable and ordered spaces—and which do not, exploring its behavior under operations like products and quotients. Finally, "Hands-On Practices" will offer you the chance to solidify your understanding by working through concrete problems and examples. We begin by examining the principles that underpin this important topological concept.

## Principles and Mechanisms

In the study of topological spaces, the [separation axioms](@entry_id:154482) provide a hierarchical framework for [classifying spaces](@entry_id:148422) based on their ability to distinguish points and closed sets. The property of **normality**, which guarantees that any two [disjoint closed sets](@entry_id:152178) can be enclosed in [disjoint open sets](@entry_id:150704), is particularly significant, as it underpins fundamental results like Urysohn's Lemma and the Tietze Extension Theorem. A natural and important question arises regarding how such properties behave with respect to subspaces. While many foundational properties like the Hausdorff ($T_2$) condition are **hereditary**—meaning they are passed down to all subspaces—normality, surprisingly, is not. This observation necessitates the introduction of a stronger condition, leading us to the concept of hereditarily [normal spaces](@entry_id:154073).

### The Non-Hereditary Nature of Normality

To appreciate the need for a concept stronger than normality, we must first demonstrate that normality is not a [hereditary property](@entry_id:151340). We can do so by constructing a space that is normal but contains a subspace that fails to be normal. A canonical example of such a space is built from ordered sets.

Consider the [ordinal numbers](@entry_id:152575). Let $[0, \omega]$ denote the set of non-negative integers along with a [maximal element](@entry_id:274677) $\omega$, endowed with the [order topology](@entry_id:143222). This space is homeomorphic to a familiar convergent sequence $\{1 - \frac{1}{n}\}_{n=1}^\infty \cup \{1\}$. Similarly, let $[0, \Omega]$ be the set of all countable ordinals together with the [first uncountable ordinal](@entry_id:156023), $\Omega$, as its maximum element, also with the [order topology](@entry_id:143222). A crucial feature of $[0, \Omega]$ is that any *countable* collection of [ordinals](@entry_id:150084) less than $\Omega$ has an upper bound that is also less than $\Omega$. Both $[0, \omega]$ and $[0, \Omega]$ are compact Hausdorff spaces.

Now, let us define the [product space](@entry_id:151533) $X = [0, \Omega] \times [0, \omega]$. As the product of two compact Hausdorff spaces, $X$ is itself a compact Hausdorff space. A cornerstone theorem of topology states that every compact Hausdorff space is normal. Thus, $X$ is a [normal space](@entry_id:154487).

The counterexample emerges when we consider a specific subspace of $X$. Let $Y$ be the space $X$ with the "top-right corner" point removed:
$$ Y = X \setminus \{(\Omega, \omega)\} $$
This subspace $Y$ is famously known as the **Tychonoff plank**. Since $Y$ is a subspace of the Hausdorff space $X$, $Y$ is also Hausdorff. Furthermore, since $X$ is also completely regular (a property of all compact Hausdorff spaces) and complete regularity is hereditary, $Y$ is completely regular, which implies it is regular ($T_3$). The critical question is whether $Y$ retains normality [@problem_id:1556917].

To show that $Y$ is not normal, we must find two [disjoint sets](@entry_id:154341) in $Y$ that are closed in the subspace topology but cannot be separated by disjoint open sets. Consider the following two subsets of $Y$:
$$ A = \{(\Omega, n) \mid n \in [0, \omega)\} = \{(\Omega, 0), (\Omega, 1), (\Omega, 2), \dots\} $$
$$ B = \{(x, \omega) \mid x \in [0, \Omega)\} $$
The set $A$ is the "right edge" of the plank (without the corner), and $B$ is the "top edge" (also without the corner). One can verify that both $A$ and $B$ are closed sets in $Y$. In the parent space $X$, the only accumulation point of both $A$ and $B$ is the single point $(\Omega, \omega)$. Since this point is not in $Y$, the sets $A$ and $B$ contain all of their [accumulation points](@entry_id:177089) within $Y$, and are therefore closed in $Y$. They are also clearly disjoint.

The proof that $A$ and $B$ cannot be separated in $Y$ hinges on the differing cardinalities of the index sets defining the "edges". Suppose, for the sake of contradiction, that there exist disjoint open sets $U$ and $V$ in $Y$ with $A \subseteq U$ and $B \subseteq V$.

For each point $(\Omega, n) \in A$, its containment in the open set $U$ implies the existence of a basic [open neighborhood](@entry_id:268496) $(\alpha_n, \Omega] \times \{n\}$ that is fully contained in $U$, for some ordinal $\alpha_n  \Omega$. This gives us a *countable* collection of ordinals $\{\alpha_n\}_{n  \omega}$. By the defining property of $\Omega$, their supremum $\beta = \sup_{n  \omega} \{\alpha_n\}$ must be a countable ordinal, so $\beta  \Omega$.

Now, consider the point $p = (\beta, \omega)$, which belongs to the set $B$ and therefore to $V$. Since $V$ is open, there must be a basic open neighborhood of $p$ contained entirely within $V$. This neighborhood must contain a set of the form $(\gamma, \delta) \times (m, \omega]$, where $\gamma  \beta  \delta \le \Omega$ and $m  \omega$.

This is where the contradiction materializes. Since $\beta$ is the *[supremum](@entry_id:140512)* of the set $\{\alpha_n\}$, there must be some integer $k > m$ for which $\alpha_k > \gamma$. Now, let's examine the point $q = (\alpha_k+1, k)$ (assuming $\alpha_k+1  \delta$, which we can ensure by picking a large enough $k$ and potentially a smaller $\delta$).
- Is $q \in U$? Since $\alpha_k  \alpha_k+1$, the point $q$ lies in $(\alpha_k, \Omega] \times \{k\}$, which is a subset of $U$. Thus, $q \in U$.
- Is $q \in V$? Since $\gamma  \alpha_k  \beta  \delta$, we have $\alpha_k+1 \in (\gamma, \delta)$. Also, $k > m$. Thus, the point $q$ also lies in $(\gamma, \delta) \times (m, \omega]$, which is a subset of $V$. Thus, $q \in V$.

We have found a point $q$ that belongs to both $U$ and $V$, contradicting our assumption that they are disjoint. Therefore, the disjoint closed sets $A$ and $B$ cannot be separated in $Y$. This demonstrates that the Tychonoff plank $Y$ is not a normal space, and consequently, normality is not a [hereditary property](@entry_id:151340) [@problem_id:1556415].

### Hereditarily Normal and Completely Normal Spaces

The failure of normality to be hereditary motivates the definition of a stronger property.

**Definition:** A topological space $X$ is **hereditarily normal** if every subspace of $X$ is a normal space.

This definition is straightforward. If a space is hereditarily normal, then any subspace, and indeed any subspace of a subspace, is guaranteed to be normal. This follows from the fact that being a subspace is a transitive relation: if $Z \subseteq Y$ and $Y \subseteq X$, then $Z$ is also a subspace of $X$ [@problem_id:1556446].

While the definition is simple, applying it directly by checking every subspace is impractical. A more powerful, equivalent characterization is needed. This is found through the concept of *[separated sets](@entry_id:152848)*.

**Definition:** Two subsets $A$ and $B$ of a topological space $X$ are said to be **separated** if the closure of each is disjoint from the other set. Formally, $A$ and $B$ are separated if
$$ (\bar{A} \cap B) \cup (A \cap \bar{B}) = \emptyset $$
Note that any two [disjoint closed sets](@entry_id:152178) are separated. However, [separated sets](@entry_id:152848) need not be closed. Their [closures](@entry_id:747387) are permitted to intersect each other, as long as the intersection does not contain points from the original sets. This leads to a crucial characterization.

**Definition:** A space $X$ is **completely normal** if for any two [separated sets](@entry_id:152848) $A$ and $B$ in $X$, there exist disjoint open sets $U$ and $V$ such that $A \subseteq U$ and $B \subseteq V$.

For instance, consider the space $X = \{w, x, y, z\}$ with the topology $\tau = \{\emptyset, X, \{w\}, \{y\}, \{w,y\}, \{w,x,y\}, \{w,y,z\}\}$. The sets $A = \{x\}$ and $B = \{z\}$ are both closed, so they are certainly separated. However, any open set containing $x$ must be $\{w,x,y\}$ or $X$, and any open set containing $z$ must be $\{w,y,z\}$ or $X$. Any pair of such open sets has a non-empty intersection. Thus, in this space, the [separated sets](@entry_id:152848) $A$ and $B$ cannot be separated by [disjoint open sets](@entry_id:150704), meaning the space is not completely normal [@problem_id:1556465].

The concepts of hereditary normality and complete normality are, in fact, one and the same.

**Theorem:** A topological space is hereditarily normal if and only if it is completely normal.

*Proof Sketch:*

($\Rightarrow$) Assume $X$ is hereditarily normal. Let $A$ and $B$ be [separated sets](@entry_id:152848) in $X$. Our goal is to find [disjoint open sets](@entry_id:150704) separating them. The key insight is to move to a subspace where $A$ and $B$ become part of [disjoint closed sets](@entry_id:152178). Consider the subspace $Y = X \setminus (\bar{A} \cap \bar{B})$. Since $A$ and $B$ are separated, neither $A$ nor $B$ intersects the set $\bar{A} \cap \bar{B}$, so both are contained in $Y$. Within the subspace $Y$, one can show that the sets $\bar{A} \cap Y$ and $\bar{B} \cap Y$ are disjoint closed sets containing $A$ and $B$ respectively. Since $X$ is hereditarily normal, the subspace $Y$ is normal. Thus, there exist [disjoint sets](@entry_id:154341) $U_Y, V_Y$ that are open *in Y* and separate $\bar{A} \cap Y$ and $\bar{B} \cap Y$. These sets can then be used to construct the required [disjoint open sets](@entry_id:150704) in $X$ that separate $A$ and $B$ [@problem_id:1556444] [@problem_id:1556427].

($\Leftarrow$) Assume $X$ is completely normal (i.e., it separates [separated sets](@entry_id:152848)). To show $X$ is hereditarily normal, we must show that an arbitrary subspace $Y \subseteq X$ is normal. Let $C$ and $D$ be any two [disjoint closed sets](@entry_id:152178) in $Y$. The crucial step is to show that $C$ and $D$, when viewed as sets in the parent space $X$, are separated. Since $C$ is closed in $Y$, we have $C = \bar{C}^Y = \bar{C}^X \cap Y$. As $C$ and $D$ are disjoint and $D \subseteq Y$, it follows that $\bar{C}^X \cap D = \emptyset$. By a symmetrical argument, $C \cap \bar{D}^X = \emptyset$. Thus, $C$ and $D$ are [separated sets](@entry_id:152848) in $X$ [@problem_id:1556456]. By our assumption of complete normality, there exist [disjoint open sets](@entry_id:150704) $U$ and $V$ in $X$ such that $C \subseteq U$ and $D \subseteq V$. The intersections $U \cap Y$ and $V \cap Y$ are then [disjoint open sets](@entry_id:150704) in the subspace $Y$ that separate $C$ and $D$. Therefore, $Y$ is normal. Since $Y$ was arbitrary, $X$ is hereditarily normal.

This equivalence is powerful because it recasts a condition about all subspaces into a single separation property within the parent space. For $T_1$ spaces, another useful characterization exists: a $T_1$ space is hereditarily normal if and only if every one of its *open* subspaces is normal [@problem_id:1556427].

### The Position of Hereditary Normality

With these characterizations in hand, we can situate hereditarily [normal spaces](@entry_id:154073) within the broader landscape of [topological properties](@entry_id:154666).

#### Relationship to Other Separation Axioms

If a space $X$ is both hereditarily normal and $T_1$, it must also be **regular**. Recall that a space is regular if a point and a disjoint closed set can be separated by open sets. In a $T_1$ space, any singleton set $\{x\}$ is closed. To separate a point $x$ from a [closed set](@entry_id:136446) $C$ not containing it, we simply have two [disjoint closed sets](@entry_id:152178), $\{x\}$ and $C$. Since a [hereditarily normal space](@entry_id:155619) is itself normal, these sets can be separated by disjoint open sets. This directly satisfies the condition for regularity [@problem_id:1556418].

#### Perfectly Normal Spaces

An even stronger condition is that of perfect normality. A space $X$ is **perfectly normal** if it is normal and every closed set in $X$ is a **$G_\delta$ set** (a countable intersection of open sets). This property has a strong connection to hereditary normality.

**Theorem:** Every [perfectly normal space](@entry_id:151492) is hereditarily normal.

This follows from the fact that perfect normality is itself a [hereditary property](@entry_id:151340). If $X$ is perfectly normal, any subspace $Y$ can be shown to be perfectly normal, and therefore normal. This provides a significant source of hereditarily [normal spaces](@entry_id:154073) [@problem_id:1556431]. For example, every **[metrizable space](@entry_id:153011)** is perfectly normal. In a [metric space](@entry_id:145912) $(X, d)$, any closed set $F$ can be written as the $G_\delta$ set $\bigcap_{n=1}^\infty \{x \in X \mid d(x, F)  1/n\}$. Since metric spaces are also normal, they are perfectly normal, and thus hereditarily normal.

The converse is not true; there exist hereditarily [normal spaces](@entry_id:154073) that are not perfectly normal. This establishes a clear hierarchy:
$$ \text{Metrizable} \implies \text{Perfectly Normal} \implies \text{Hereditarily Normal} \implies \text{Normal} $$

#### Sufficient Conditions for Hereditary Normality

Beyond perfect normality, other conditions can guarantee that a [normal space](@entry_id:154487) is also hereditarily normal. One important result involves second-[countability](@entry_id:148500).

**Theorem:** Every normal, [second-countable space](@entry_id:141954) is hereditarily normal.

A space is **second-countable** if its topology has a [countable basis](@entry_id:155278). The proof of this theorem relies on two key facts: (1) second-[countability](@entry_id:148500) is a [hereditary property](@entry_id:151340), and (2) a space that is regular and Lindelöf is normal. (A space is Lindelöf if every open cover has a countable [subcover](@entry_id:151408); second-[countability](@entry_id:148500) implies the Lindelöf property). Given a normal, [second-countable space](@entry_id:141954) $X$, any subspace $Y$ is also second-countable and regular (since regularity is hereditary from the normal space $X$). As $Y$ is second-countable, it is Lindelöf. Being both regular and Lindelöf, $Y$ must be normal. Since $Y$ was an arbitrary subspace, $X$ is hereditarily normal [@problem_id:1556447]. This theorem provides a practical tool for identifying a large class of well-behaved spaces that satisfy this strong separation property.