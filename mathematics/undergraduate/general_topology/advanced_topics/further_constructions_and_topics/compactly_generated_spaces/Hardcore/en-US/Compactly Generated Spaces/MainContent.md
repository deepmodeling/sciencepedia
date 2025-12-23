## Introduction
In the study of topology, a central challenge is finding a category of spaces that is broad enough to be widely applicable, yet structured enough to ensure that fundamental constructions behave predictably. While metric spaces or locally compact Hausdorff spaces offer a solid foundation for analysis, they can be too restrictive for the abstract needs of fields like algebraic topology. This creates a knowledge gap: how can we work effectively with continuity, quotients, and [function spaces](@entry_id:143478) in a more general setting?

This article introduces **compactly generated spaces**, or **k-spaces**, as a powerful answer to this question. These spaces form a "[convenient category](@entry_id:149536)" where the topological structure is elegantly determined by its compact subsets. Over the next three chapters, you will gain a comprehensive understanding of this essential concept. First, **Principles and Mechanisms** will lay the groundwork by presenting the formal definition of a [k-space](@entry_id:142033), the core theorem for testing continuity, and the landscape of spaces that fall into this class. Next, **Applications and Interdisciplinary Connections** will explore the utility of k-spaces in algebraic topology and contrast their role with other mathematical domains like functional analysis. Finally, **Hands-On Practices** will provide a series of targeted exercises to reinforce your learning and test your comprehension.

We begin by delving into the foundational principles that define what a [compactly generated space](@entry_id:152396) is and why it provides such a useful framework for modern topology.

## Principles and Mechanisms

In our study of topology, we often seek to work within categories of spaces that possess desirable properties, particularly concerning the behavior of maps and standard topological constructions like products and quotients. While many fundamental theorems of analysis and geometry are developed in the context of [metric spaces](@entry_id:138860) or locally compact Hausdorff spaces, these categories can be overly restrictive for more abstract fields like algebraic topology. Compactly generated spaces, or **k-spaces**, provide a broader, more "convenient" category of spaces that retain many of the essential tools for working with continuity. This chapter elucidates the definition, core principles, and key mechanisms of these spaces.

### The Definition of a k-Space

The concept of a [compactly generated space](@entry_id:152396) is founded on the idea that the topological structure of the space is entirely determined by its compact subsets. This is formalized in the following definition.

A [topological space](@entry_id:149165) $X$ is a **[compactly generated space](@entry_id:152396)** (or **[k-space](@entry_id:142033)**) if its closed sets are precisely those that are recognized as closed by every [compact subspace](@entry_id:153124). More formally, a subset $A \subseteq X$ is closed in $X$ if and only if for every compact subset $K \subseteq X$, the intersection $A \cap K$ is closed in the subspace topology of $K$.

The "if" direction of this statement—that if $A$ is closed in $X$, then $A \cap K$ is closed in $K$—is true for any [topological space](@entry_id:149165), as the intersection of a [closed set](@entry_id:136446) with any subspace is closed in the subspace topology. The power of the k-space definition lies in the "only if" direction: if a set behaves like a closed set on every compact "test probe" $K$, then it must be closed in the entire space $X$. This property is sometimes called the **[weak topology](@entry_id:154352) with respect to compact subsets**.

To build intuition, consider a scenario where a set fails to be closed. A set $A$ is not closed if and only if there exists a [limit point](@entry_id:136272) of $A$ that is not contained in $A$. For $X$ to be a [k-space](@entry_id:142033), this failure to be closed must be "witnessed" by some compact subset. That is, if $x \in \overline{A} \setminus A$, there must exist some [compact set](@entry_id:136957) $K$ containing $x$ for which $x$ is also a [limit point](@entry_id:136272) of $A \cap K$. This means $A \cap K$ is not closed in $K$.

A concrete visualization of this principle can be constructed within the familiar space $\mathbb{R}^2$. Let $A$ be the open right half-plane, $A = \{(x, y) \in \mathbb{R}^2 \mid x > 0\}$. This set is not closed in $\mathbb{R}^2$; its boundary, the y-axis, contains limit points not in $A$. For instance, the origin $(0,0)$ is in $\overline{A} \setminus A$. Since $\mathbb{R}^2$ is a [metric space](@entry_id:145912) and therefore a [k-space](@entry_id:142033) (as we will soon prove), there must exist a compact set $K$ for which $A \cap K$ is not closed in $K$. A simple choice for such a $K$ is a sequence of points in $A$ that converges to the origin, along with the origin itself. For example, let $p_n = (1/n, 0)$ for $n \in \mathbb{Z}^+$, and define $K = \{(0,0)\} \cup \{p_n \mid n \in \mathbb{Z}^+\}$. This set $K$ is compact. The intersection $A \cap K = \{p_n \mid n \in \mathbb{Z}^+\}$ consists of all points in the sequence, but not their [limit point](@entry_id:136272) $(0,0)$. Thus, $(0,0)$ is a limit point of $A \cap K$ that is in $K$ but not in $A \cap K$, proving that $A \cap K$ is not closed in $K$. The existence of such a compact "witness" $K$ is guaranteed by the [k-space](@entry_id:142033) property.

### Continuity and Compactly Generated Spaces

One of the principal motivations for defining k-spaces is to simplify the analysis of continuity. In general, to prove a function $f: X \to Y$ is continuous, one must verify that the preimage of every [closed set](@entry_id:136446) in $Y$ is closed in $X$. For k-spaces, this condition can be tested on compact subsets.

**Theorem (The Continuity Test for k-spaces):** Let $X$ be a [k-space](@entry_id:142033) and $Y$ be any [topological space](@entry_id:149165). A function $f: X \to Y$ is continuous if and only if its restriction $f|_K: K \to Y$ is continuous for every compact subset $K \subseteq X$.

**Proof:** The forward direction ("only if") is trivial, as the restriction of a [continuous map](@entry_id:153772) to any subspace is continuous. For the reverse direction ("if"), assume that $f|_K$ is continuous for every compact $K \subseteq X$. To show $f$ is continuous, we take an arbitrary closed set $C \subseteq Y$ and show that its preimage $f^{-1}(C)$ is closed in $X$. Since $X$ is a [k-space](@entry_id:142033), we can do this by showing that for every compact $K \subseteq X$, the intersection $f^{-1}(C) \cap K$ is closed in $K$.

The restriction $f|_K$ is continuous by hypothesis. The [preimage](@entry_id:150899) of $C$ under this restricted map is $(f|_K)^{-1}(C)$. By definition of the restriction, a point $x \in K$ is in $(f|_K)^{-1}(C)$ if and only if $f(x) \in C$. This is equivalent to $x \in f^{-1}(C)$. Therefore, $(f|_K)^{-1}(C) = f^{-1}(C) \cap K$. Since $f|_K$ is continuous and $C$ is closed, this set must be closed in the domain of $f|_K$, which is $K$. As this holds for all compact $K$, the definition of a [k-space](@entry_id:142033) ensures that $f^{-1}(C)$ is closed in $X$. Thus, $f$ is continuous.

This theorem provides the central "mechanism" of k-spaces: the often difficult task of verifying continuity on an entire complex space can be reduced to checking it on its simpler, compact parts.

### The Landscape of k-Spaces

To effectively use k-spaces, we must understand which familiar [topological spaces](@entry_id:155056) belong to this class and how the [k-space](@entry_id:142033) property relates to other common topological properties.

#### Broad Classes of k-Spaces

Many spaces encountered in analysis and geometry are k-spaces. Two major results establish this.

**1. First-Countable Spaces:** Every [first-countable space](@entry_id:148307) is a [k-space](@entry_id:142033). Consequently, **every metric space is a [k-space](@entry_id:142033)**.
The proof follows the same logic as our introductory example. Let $X$ be a [first-countable space](@entry_id:148307), and let $A \subseteq X$ be a set such that $A \cap K$ is closed for every compact $K \subseteq X$. If $A$ were not closed, we could find a point $x \in \overline{A} \setminus A$. Because $X$ is first-countable, there exists a sequence $(a_n)_{n \in \mathbb{N}}$ of points in $A$ that converges to $x$. The set $K = \{x\} \cup \{a_n \mid n \in \mathbb{N}\}$ is compact. The intersection $A \cap K = \{a_n \mid n \in \mathbb{N}\}$ is not closed in $K$ because its [limit point](@entry_id:136272) $x$ is in $K$ but not in $A \cap K$. This contradicts our assumption. Therefore, $A$ must be closed, and $X$ is a k-space.

**2. Locally Compact Hausdorff Spaces:** Every locally compact Hausdorff space is a k-space.
The proof strategy here is different and does not rely on sequences. Let $X$ be a locally compact Hausdorff space, and let $A \subseteq X$ satisfy the condition that $A \cap K$ is closed for all compact $K$. To show $A$ is closed, we show its complement $X \setminus A$ is open. Let $x \in X \setminus A$. Since $X$ is locally compact, $x$ has a [compact neighborhood](@entry_id:269058) $C$. Let $U_0$ be an open set such that $x \in U_0 \subseteq C$. Now, $C$ is a compact subset of $X$, so by our assumption, $A \cap C$ is closed in $C$. This means $C \setminus (A \cap C) = C \setminus A$ is open in the subspace topology of $C$. So, there exists an open set $V$ in $X$ such that $C \setminus A = V \cap C$. The set $U = U_0 \cap V$ is an open neighborhood of $x$. Any point $z \in U$ is in $U_0 \subseteq C$ and in $V$, so $z \in V \cap C = C \setminus A$. Thus, $z \notin A$. This shows $U \subseteq X \setminus A$. Since we have found an open neighborhood of $x$ contained entirely in $X \setminus A$, and $x$ was an arbitrary point in the complement, $X \setminus A$ is open. Hence, $A$ is closed, and $X$ is a k-space.

#### Distinguishing k-Spaces from Other Classes

While many familiar spaces are k-spaces, the class of k-spaces is distinct.
- A k-space is not necessarily locally compact. The set of rational numbers $\mathbb{Q}$ with the subspace topology from $\mathbb{R}$ is a standard [counterexample](@entry_id:148660). $\mathbb{Q}$ is a metric space, hence it is a [k-space](@entry_id:142033). However, no point in $\mathbb{Q}$ has a [compact neighborhood](@entry_id:269058). Any neighborhood of a point $q \in \mathbb{Q}$ contains an open interval $(q-r, q+r) \cap \mathbb{Q}$. The closure of this set in $\mathbb{Q}$ is $[q-r, q+r] \cap \mathbb{Q}$, which is not compact because it is not a closed subset of $\mathbb{R}$ (it is missing all the [irrational numbers](@entry_id:158320) in the interval).

- A k-space is not necessarily first-countable. While the initial examples of k-spaces often rely on sequences, the property is more general. A classic example is the "bouquet of countably many circles". This space is constructed by taking a countable collection of intervals, $I_n = [0,1]$, and identifying all their starting points, $\{ (0,n) \mid n \in \mathbb{N} \}$, to a single point $p$. The resulting [quotient space](@entry_id:148218) $X$ is a [k-space](@entry_id:142033) (as we will see below), but it is not first-countable at the point $p$. Any countable collection of neighborhoods of $p$ can be used to construct a new neighborhood of $p$ not contained in any element of the collection, via a [diagonal argument](@entry_id:202698).

### Behavior of k-Spaces Under Topological Operations

A key reason for the utility of k-spaces is their well-behaved nature with respect to several fundamental topological constructions.

**Quotient Spaces:** The class of k-spaces is closed under taking quotients. If $X$ is a k-space and $p: X \to Y$ is a [quotient map](@entry_id:140877), then $Y$ is also a k-space. This is an extremely powerful property, as quotient constructions are central to geometry and algebraic topology (e.g., in forming cell complexes or identifying boundaries to create spheres and tori). The proof follows directly from the definitions: to check if a set $B \subseteq Y$ is closed, we test $B \cap L$ for all compact $L \subseteq Y$. This test can be lifted via the map $p$ to a test on compact sets in $X$, where the k-space property of $X$ gives the desired result.

**Topological Sums:** The topological sum (disjoint union) of any family of k-spaces is a k-space. This property is straightforward to prove by recalling that a subset of a topological sum is compact if and only if it intersects only finitely many of the constituent spaces, and its intersection with each of those is compact.

**Subspaces:** The [k-space](@entry_id:142033) property is **not** hereditary; an arbitrary subspace of a k-space is not necessarily a [k-space](@entry_id:142033). This is a notable limitation. However, closed subspaces of k-spaces are k-spaces.

**Product Spaces:** The behavior with respect to products is the most subtle and, in many ways, the primary motivation for the entire theory. The Cartesian product of two k-spaces, endowed with the standard product topology, is **not** necessarily a [k-space](@entry_id:142033). This failure is closely related to another [pathology](@entry_id:193640) of the standard product topology. A function $f: X \times Y \to Z$ is called **separately continuous** if for each fixed $x_0 \in X$, the map $y \mapsto f(x_0, y)$ is continuous, and for each fixed $y_0 \in Y$, the map $x \mapsto f(x, y_0)$ is continuous. While joint continuity always implies separate continuity, the converse is false, even for products of "nice" spaces like k-spaces.

A classic example is the function $f: \mathbb{Q} \times \mathbb{Q} \to \mathbb{R}$:
$$
f(x, y) = \begin{cases} \frac{2xy}{x^2+y^2}  \text{if } (x,y) \neq (0,0) \\ 0  \text{if } (x,y) = (0,0) \end{cases}
$$
This function is separately continuous everywhere. For any fixed $x_0 \neq 0$, the function of $y$ is a rational function with a non-zero denominator, hence continuous. If $x_0 = 0$, the function is identically zero. The same holds by symmetry for fixed $y_0$. However, $f$ is not jointly continuous at the origin. Approaching the origin along the line $y=x$ (using a sequence of rational points like $(1/n, 1/n)$), we have $f(x,x) = \frac{2x^2}{2x^2} = 1$. The limit along this path is $1$, which does not equal $f(0,0)=0$.

This failure has significant consequences. To remedy this, topologists define a different topology on the product $X \times Y$, the **compactly generated product topology**, which is finer than the standard [product topology](@entry_id:154786) and guarantees that the product of two k-spaces is a k-space. In this "[convenient category](@entry_id:149536)," the exponential law $Z^{X \times Y} \cong (Z^Y)^X$ holds, which is essential for homotopy theory.

There is, however, a crucial positive result for the standard product topology: if $X$ is a k-space and $Y$ is a locally compact Hausdorff space, then the product $X \times Y$ with the usual [product topology](@entry_id:154786) is a [k-space](@entry_id:142033).

Finally, we mention another important result concerning continuity, which provides an alternative path to proving continuity without directly using the definition.

**Theorem (A Closed Graph Condition):** Let $f: X \to Y$ be a function from a [topological space](@entry_id:149165) $X$ to a **compact** space $Y$. If the graph of the function, $\Gamma_f = \{(x, f(x)) \mid x \in X\}$, is a closed subset of the [product space](@entry_id:151533) $X \times Y$, then $f$ is continuous.

The proof relies on the fact that the projection map $p_X: X \times Y \to X$ is a [closed map](@entry_id:150357) when $Y$ is compact. For any closed set $C \subseteq Y$, the [preimage](@entry_id:150899) $f^{-1}(C)$ can be expressed as $p_X(\Gamma_f \cap (X \times C))$, which is the projection of a [closed set](@entry_id:136446) and therefore closed.

In summary, compactly generated spaces form a class of spaces broad enough to include metric and locally compact Hausdorff spaces, yet structured enough to ensure that continuity can be tested on compact sets and that quotients behave predictably. Their study reveals the subtleties of the [product topology](@entry_id:154786) and provides the foundation for more advanced constructions in modern topology.