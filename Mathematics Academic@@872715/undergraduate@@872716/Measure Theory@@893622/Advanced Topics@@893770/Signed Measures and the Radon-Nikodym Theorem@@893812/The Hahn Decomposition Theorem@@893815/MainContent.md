## Introduction
In measure theory, while positive measures like length or area are intuitive, many real-world phenomena in fields like finance and physics require the concept of a **[signed measure](@entry_id:160822)**, which can assign both positive and negative values. This generalization raises a fundamental question: how can we systematically understand the structure of a space under such a measure? Is it possible to cleanly separate the regions contributing positive value from those contributing negative value? This article provides a comprehensive answer through the lens of the Hahn Decomposition Theorem, a cornerstone result in analysis.

The following chapters will guide you through a complete understanding of this theorem. In **Principles and Mechanisms**, we will define the core concepts of positive, negative, and [null sets](@entry_id:203073), state the Hahn Decomposition Theorem, and explore its critical connection to the Jordan decomposition. Next, in **Applications and Interdisciplinary Connections**, we will see how this abstract theorem provides a powerful analytical tool in probability theory, [functional analysis](@entry_id:146220), and beyond. Finally, the **Hands-On Practices** section will allow you to solidify your knowledge by working through concrete examples and problems.

## Principles and Mechanisms

In our study of [measure theory](@entry_id:139744), we have become familiar with positive measures, which assign a non-negative value to every [measurable set](@entry_id:263324), embodying intuitive notions like length, area, or probability. However, many applications in fields such as physics, finance, and probability theory require a more general concept: the **[signed measure](@entry_id:160822)**. A [signed measure](@entry_id:160822), $\nu$, defined on a [measurable space](@entry_id:147379) $(X, \mathcal{M})$, is a countably [additive function](@entry_id:636779) $\nu: \mathcal{M} \to [-\infty, \infty]$ with $\nu(\emptyset) = 0$. It is permitted to take on at most one of the values $+\infty$ or $-\infty$. In this chapter, we will primarily focus on **finite [signed measures](@entry_id:198637)**, where the range is contained within $\mathbb{R}$, as they provide a clear and accessible context for the foundational principles.

A [signed measure](@entry_id:160822) can be thought of as representing a net quantity, like electrical charge or financial credit and debt. Some regions of the space may contribute positively to the total "charge," while others contribute negatively. The central challenge, and the main subject of this chapter, is to understand if we can systematically and cleanly separate the underlying space into these regions of positivity and negativity. The affirmative answer is given by one of the cornerstones of measure theory: the Hahn Decomposition Theorem.

### Positive, Negative, and Null Sets: A Foundational Trichotomy

To formalize the idea of "regions of positivity and negativity," we must introduce three crucial definitions. Let $\nu$ be a [signed measure](@entry_id:160822) on a [measurable space](@entry_id:147379) $(X, \mathcal{M})$.

-   A set $P \in \mathcal{M}$ is called a **positive set** with respect to $\nu$ if for every measurable subset $E \subseteq P$, we have $\nu(E) \ge 0$.

-   A set $N \in \mathcal{M}$ is called a **negative set** with respect to $\nu$ if for every measurable subset $E \subseteq N$, we have $\nu(E) \le 0$.

-   A set $Z \in \mathcal{M}$ is called a **[null set](@entry_id:145219)** (or a $\nu$-[null set](@entry_id:145219)) if it is simultaneously a positive set and a negative set. This implies that for every measurable subset $E \subseteq Z$, we have $\nu(E) = 0$.

A common point of confusion arises from the stringent nature of these definitions. One might mistakenly assume that if a set $A$ has a positive measure, i.e., $\nu(A) \ge 0$, it must be a positive set. This is not true. The definition demands that *every* measurable subset of $A$ must have a non-negative measure.

Consider a [signed measure](@entry_id:160822) on the space $X = [-2, 2]$ defined by $\nu(E) = \int_E x \, d\lambda(x)$, where $\lambda$ is the Lebesgue measure. Let's examine the set $A = (-1, 2]$. A direct calculation shows $\nu(A) = \int_{-1}^2 x \, dx = \frac{3}{2} > 0$. However, $A$ is not a positive set. To see why, we can find a measurable subset of $A$ with a negative measure. For instance, consider the subset $E = (-1, 0) \subseteq A$. Its measure is $\nu(E) = \int_{-1}^0 x \, dx = -\frac{1}{2}  0$. The existence of this single subset with a negative measure is sufficient to disqualify $A$ from being a positive set [@problem_id:1452264]. The definition requires an unwavering positivity across all its parts.

To build intuition on a more discrete level, let's consider the space $X = \{1, 2, 3\}$ with the [power set](@entry_id:137423) $\mathcal{A} = \mathcal{P}(X)$ as the sigma-algebra. Define a [signed measure](@entry_id:160822) $\nu$ by its values on the singletons: $\nu(\{1\}) = 4$, $\nu(\{2\}) = -7$, and $\nu(\{3\}) = 2$. By additivity, the measure of any set is the sum of the measures of its elements.

Let's test some subsets against our definitions [@problem_id:1452278]:
-   Is $A = \{1, 3\}$ a positive set? Its measurable subsets are $\emptyset, \{1\}, \{3\}, \{1, 3\}$. Their measures are $\nu(\emptyset)=0$, $\nu(\{1\})=4$, $\nu(\{3\})=2$, and $\nu(\{1, 3\}) = 4+2=6$. Since all are non-negative, $A$ is indeed a positive set.
-   Is $B = \{2\}$ a negative set? Its subsets are $\emptyset$ and $\{2\}$, with measures $0$ and $-7$. Both are non-positive, so $B$ is a negative set.
-   What about $C = \{2, 3\}$? This set is neither positive nor negative. It contains the subset $\{3\}$ with a positive measure ($\nu(\{3\}) = 2$), so it cannot be a negative set. It also contains the subset $\{2\}$ with a negative measure ($\nu(\{2\}) = -7$), so it cannot be a positive set.

This simple example illustrates the trichotomy: a given set can be positive, negative, or neither. The goal of the Hahn decomposition is to show that the entire space $X$ can be partitioned into just two pieces: one that is purely positive and one that is purely negative.

### Properties of Positive and Negative Sets

Positive and negative sets have several elementary but important properties that follow directly from their definitions.

First, any measurable subset of a positive set is also a positive set. The same holds for negative sets. Second, the collection of positive sets is closed under countable unions. If $\{P_i\}_{i=1}^\infty$ is a sequence of positive sets, their union $P = \bigcup_{i=1}^\infty P_i$ is also a positive set. To prove this for two sets $A$ and $B$, consider any measurable subset $E \subseteq A \cup B$. We can write $E$ as a disjoint union $E = (E \cap A) \cup (E \setminus A)$. Since $E \cap A \subseteq A$, we have $\nu(E \cap A) \ge 0$. Since $E \setminus A = E \cap A^c \subseteq B$, we also have $\nu(E \setminus A) \ge 0$. By additivity, $\nu(E) = \nu(E \cap A) + \nu(E \setminus A) \ge 0+0=0$. This argument can be extended to countable unions [@problem_id:1452244].

A particularly important structural property concerns the intersection of positive and negative sets. Let $P_0$ be a positive set and $N_0$ be a negative set. What can be said about their intersection, $A = P_0 \cap N_0$? Consider any measurable subset $E \subseteq A$. Because $E$ is also a subset of the positive set $P_0$, we must have $\nu(E) \ge 0$. Simultaneously, because $E$ is a subset of the negative set $N_0$, we must have $\nu(E) \le 0$. The only way to satisfy both conditions is if $\nu(E) = 0$. Since this holds for *every* measurable subset $E$ of $A$, the set $A$ is, by definition, a [null set](@entry_id:145219) [@problem_id:1452243]. This simple but powerful result is a key lemma in proving the uniqueness of the Hahn decomposition.

### The Hahn Decomposition Theorem

We now arrive at the central theorem, named after the Austrian mathematician Hans Hahn.

**Theorem (Hahn Decomposition):** Let $\nu$ be a [signed measure](@entry_id:160822) on a [measurable space](@entry_id:147379) $(X, \mathcal{M})$. Then there exists a partition of $X$ into two [measurable sets](@entry_id:159173), $P$ and $N$, such that $P$ is a positive set for $\nu$ and $N$ is a negative set for $\nu$. This means $X = P \cup N$ and $P \cap N = \emptyset$. The pair $(P, N)$ is called a **Hahn decomposition** of $X$ with respect to $\nu$.

The proof of existence is non-trivial and typically involves a constructive argument that seeks out a positive set with maximal measure. The key insight is that such a maximal set must exist and that its complement must be a negative set.

#### The Question of Uniqueness

A natural question is whether this decomposition is unique. If we find one such pair $(P, N)$, are there others? The answer is that the decomposition is not strictly unique, but it is "unique up to $\nu$-[null sets](@entry_id:203073)".

More formally, if $(P_1, N_1)$ and $(P_2, N_2)$ are two Hahn decompositions for the same [signed measure](@entry_id:160822) $\nu$, then the symmetric differences $P_1 \Delta P_2 = (P_1 \setminus P_2) \cup (P_2 \setminus P_1)$ and $N_1 \Delta N_2$ are $\nu$-[null sets](@entry_id:203073). This means that any two valid positive sets can only differ by a set that is, for all intents and purposes, invisible to the measure $\nu$.

Let's explore this. Suppose $(P, N)$ is a Hahn decomposition and $P'$ is any other positive set. What can we say about the set $P' \setminus P$? Since $P' \setminus P = P' \cap P^c = P' \cap N$, this set is the intersection of a positive set ($P'$) and a negative set ($N$). As we proved earlier, such an intersection must be a $\nu$-[null set](@entry_id:145219). Therefore, $\nu(E)=0$ for any measurable $E \subseteq P' \setminus P$ [@problem_id:1452257].

This near-uniqueness is often observed in practice. For instance, consider a measure $\nu$ on $\mathbb{R}$ given by the density function $f(x) = (1-2x^2)\exp(-x^2)$ with respect to the Lebesgue measure. The sign of $f(x)$ is determined by the term $1-2x^2$, which is non-negative on $[-1/\sqrt{2}, 1/\sqrt{2}]$. We can propose two different Hahn decompositions:
1.  $P_1 = [-1/\sqrt{2}, 1/\sqrt{2}]$ and its complement $N_1$.
2.  $P_2 = (-1/\sqrt{2}, 1/\sqrt{2})$ and its complement $N_2$.
These two decompositions differ only by the two-point set $\{-1/\sqrt{2}, 1/\sqrt{2}\}$. Since $\nu$ is defined by an integral with respect to Lebesgue measure, and this two-point set has Lebesgue measure zero, it is also a $\nu$-[null set](@entry_id:145219). Thus, both are valid Hahn decompositions, illustrating that the decomposition is unique only up to such [null sets](@entry_id:203073) [@problem_id:1452271].

### Applications and Interpretations of the Hahn Decomposition

The Hahn decomposition is far more than a mere curiosity; it is a powerful tool for dissecting [signed measures](@entry_id:198637) and understanding their structure.

#### The Extremal Property

The partition provided by the Hahn theorem is not arbitrary; it separates the space in a way that maximizes and minimizes the measure. Let $(P, N)$ be a Hahn decomposition for a finite [signed measure](@entry_id:160822) $\nu$. For any [measurable set](@entry_id:263324) $A \subseteq X$, we can write:
$\nu(A) = \nu(A \cap P) + \nu(A \cap N)$.

Since $A \cap P$ is a subset of the positive set $P$, we have $\nu(A \cap P) \ge 0$. Likewise, $\nu(A \cap N) \le 0$. This implies that $\nu(A) = \nu(A \cap P) + \nu(A \cap N) \le \nu(A \cap P)$. Furthermore, since the union of positive sets is positive, we know that for any two positive sets $P_1, P_2$, $\nu(P_1 \cup P_2) = \nu(P_1) + \nu(P_2 \setminus P_1) \ge \nu(P_1)$. This suggests that the measure is largest on the "biggest" positive set.

In fact, one of the most profound interpretations of the Hahn decomposition is that the set $P$ is a set that achieves the maximum possible value for $\nu$. That is:
$\nu(P) = \sup\{\nu(A) \mid A \in \mathcal{M}\}$.

To illustrate, consider the [signed measure](@entry_id:160822) on $[0, 1]$ with density $f(x) = \cos(2\pi x)$. The [supremum](@entry_id:140512) of $\nu(A) = \int_A \cos(2\pi x) \, dx$ over all [measurable sets](@entry_id:159173) $A$ is obtained by choosing $A$ to be the set where the integrand is non-negative. This set is precisely the positive set $P$ from the Hahn decomposition, $P = \{x \in [0, 1] \mid \cos(2\pi x) \ge 0\} = [0, 1/4] \cup [3/4, 1]$. The supremum value is then $\nu(P) = \int_P \cos(2\pi x) \, dx = 1/\pi$ [@problem_id:1452286]. Symmetrically, the [infimum](@entry_id:140118) of $\nu(A)$ is achieved on the negative set $N$, so $\nu(N) = \inf\{\nu(A) \mid A \in \mathcal{M}\}$. This extremal property endows the Hahn decomposition with deep significance.

#### Connection to the Jordan Decomposition

Perhaps the most important application of the Hahn Decomposition Theorem is that it provides a direct and [constructive proof](@entry_id:157587) of the **Jordan Decomposition Theorem**. This theorem states that any [signed measure](@entry_id:160822) $\nu$ can be uniquely decomposed into the difference of two positive, [mutually singular measures](@entry_id:186656).

Given a Hahn decomposition $(P, N)$ for $\nu$, we can define two positive measures, the **positive variation** $\nu^+$ and the **negative variation** $\nu^-$:
-   $\nu^+(A) = \nu(A \cap P)$
-   $\nu^-(A) = -\nu(A \cap N)$

For any measurable set $A$, $\nu^+(A) \ge 0$ because $A \cap P$ is a subset of the positive set $P$. Similarly, $\nu^-(A) \ge 0$ because $A \cap N$ is a subset of the negative set $N$, making $\nu(A \cap N) \le 0$. These two measures are mutually singular because $\nu^+$ lives on $P$ and $\nu^-$ lives on $N$, and $P \cap N = \emptyset$.

Crucially, they reconstruct the original measure $\nu$:
$\nu(A) = \nu(A \cap P) + \nu(A \cap N) = \nu^+(A) - \nu^-(A)$.

This decomposition, $\nu = \nu^+ - \nu^-$, is the **Jordan decomposition**. The uniqueness of the Jordan decomposition is a powerful result, and it relies on the near-uniqueness of the Hahn decomposition. The fact that any choice of Hahn decomposition yields the same $\nu^+$ and $\nu^-$ is a consequence of the fact that different positive sets $P_1, P_2$ differ only by a $\nu$-[null set](@entry_id:145219) [@problem_id:1452271].

The total "magnitude" of the [signed measure](@entry_id:160822), ignoring sign, is captured by the **[total variation measure](@entry_id:193822)**, denoted $|\nu|$, which is defined as $|\nu| = \nu^+ + \nu^-$. Using the definitions derived from the Hahn decomposition, the total variation of the entire space $X$ has a particularly elegant form:
$|\nu|(X) = \nu^+(X) + \nu^-(X) = \nu(X \cap P) + (-\nu(X \cap N)) = \nu(P) - \nu(N)$ [@problem_id:1452269].

This formula beautifully demonstrates the role of the Hahn decomposition: it partitions the space into the set $P$ that contributes all of the positive variation and the set $N$ that contributes all of the negative variation. The difference $\nu(P) - \nu(N)$ captures the sum of their magnitudes, giving the total variation of the space. For example, in the case of a measure defined by a density $f$, i.e., $\nu(E) = \int_E f \, d\mu$, the positive set is $P=\{x \mid f(x) \ge 0\}$ and the negative set is $N=\{x \mid f(x)  0\}$. The positive and negative variations correspond to integrals over these sets, and the [total variation measure](@entry_id:193822) is given by $|\nu|(E) = \int_E |f| \, d\mu$. The value $\nu(P) = \int_P f \, d\mu$ represents the total positive contribution of $f$ [@problem_id:1452248], while $-\nu(N) = \int_N -f \, d\mu$ represents the total positive contribution of $-f$.

In summary, the Hahn Decomposition Theorem provides the essential mechanism for dissecting a [signed measure](@entry_id:160822). It guarantees that any space can be partitioned into domains of pure positivity and pure negativity. This separation is not only conceptually clarifying but also serves as the functional basis for the extremal properties of the measure and for the fundamental Jordan decomposition into positive and negative variations.