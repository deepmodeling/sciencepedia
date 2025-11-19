## Introduction
In the study of topology, [quotient spaces](@entry_id:274314) represent a fundamental construction, allowing us to create new spaces by identifying or "gluing together" points of an existing space. This process, governed by an [equivalence relation](@entry_id:144135), raises a crucial question: how does the structure of the original space relate to the structure of the new [quotient space](@entry_id:148218)? The bridge connecting these two worlds is the concept of a **[saturated set](@entry_id:155857)**. These special subsets of the original space are perfectly aligned with the equivalence relation, providing the essential building blocks for defining and understanding the [quotient topology](@entry_id:150384).

This article offers a deep dive into the theory and application of saturated sets. Across the following chapters, you will gain a robust understanding of this pivotal concept.
- **Principles and Mechanisms** will introduce the formal definition of saturated sets, their relationship to the [quotient map](@entry_id:140877), their algebraic properties, and their central role in defining the [quotient topology](@entry_id:150384).
- **Applications and Interdisciplinary Connections** will showcase the utility of saturated sets in diverse mathematical fields, including geometry, number theory, and functional analysis, demonstrating how this abstract idea provides concrete insights.
- **Hands-On Practices** will provide an opportunity to solidify your knowledge by working through targeted exercises that test your ability to identify and construct saturated sets in various contexts.

## Principles and Mechanisms

In our study of [quotient spaces](@entry_id:274314), we transition from viewing an equivalence relation as a [partition of a set](@entry_id:147307) to understanding how it induces a new topological space with its own structure. The foundational concept that bridges the original space $X$ and the [quotient space](@entry_id:148218) $X/\!\sim$ is that of a **[saturated set](@entry_id:155857)**. These sets are the subsets of $X$ that are 'well-behaved' with respect to the equivalence relation, and they form the building blocks for understanding the topology of the [quotient space](@entry_id:148218).

### Defining Saturated Sets

Let $X$ be a set and let $\sim$ be an equivalence relation on $X$. This relation partitions $X$ into disjoint [equivalence classes](@entry_id:156032). For any element $x \in X$, its equivalence class is the set $[x] = \{y \in X \mid y \sim x\}$.

A subset $S \subseteq X$ is said to be **saturated** with respect to the [equivalence relation](@entry_id:144135) $\sim$ if, for any element $x$ in $S$, the entire equivalence class $[x]$ is also contained within $S$. That is:
$$ \text{If } x \in S, \text{ then } [x] \subseteq S $$
Intuitively, a [saturated set](@entry_id:155857) cannot contain only a part of an [equivalence class](@entry_id:140585); it must contain either the entire class or none of it. This leads to an equivalent and often more useful characterization: **a subset of $X$ is saturated if and only if it is a union of [equivalence classes](@entry_id:156032).**

To make this concept concrete, consider a non-topological example. Let $S = \{x_1, x_2, x_3\}$ and let our space be its power set, $X = \mathcal{P}(S)$. Define an [equivalence relation](@entry_id:144135) $\sim$ on $X$ such that for two subsets $A, B \in X$, $A \sim B$ if and only if they have the same cardinality, $|A|=|B|$. The equivalence classes are the collections of all subsets of a given size:
- $E_0 = \{\emptyset\}$
- $E_1 = \{\{x_1\}, \{x_2\}, \{x_3\}\}$
- $E_2 = \{\{x_1, x_2\}, \{x_1, x_3\}, \{x_2, x_3\}\}$
- $E_3 = \{\{x_1, x_2, x_3\}\}$

A subset of $\mathcal{P}(S)$ is saturated if it is a union of some of these classes. For example, the set $U_C = \{\{x_1\}, \{x_2\}, \{x_3\}\}$ is saturated because it is precisely the equivalence class $E_1$. Similarly, $U_B = \{\emptyset, \{x_1, x_2, x_3\}\}$ is saturated because it is the union $E_0 \cup E_3$. However, a set like $U_A = \{\{x_1\}, \{x_1, x_2\}\}$ is not saturated. It contains $\{x_1\} \in E_1$, but it does not contain the rest of $E_1$ (namely, $\{x_2\}$ and $\{x_3\}$) [@problem_id:1572475].

The nature of the saturated sets is entirely determined by the equivalence relation. Consider two extreme cases on a set $X$ with at least two points [@problem_id:1572464]:
1.  **The Trivial Relation**: $x \sim_1 y$ for all $x, y \in X$. Here, there is only one equivalence class: the entire set $X$. The only possible unions of [equivalence classes](@entry_id:156032) are the empty union, $\emptyset$, and the union of the single class, $X$. Thus, the only saturated sets are $\emptyset$ and $X$.
2.  **The Identity Relation**: $x \sim_2 y$ if and only if $x=y$. Here, every equivalence class is a singleton, i.e., $[x] = \{x\}$ for all $x \in X$. Since any subset of $X$ can be written as the union of its constituent singletons, *every* subset of $X$ is saturated.

These examples illustrate that a "coarser" equivalence relation (with larger classes) leads to fewer saturated sets, while a "finer" relation (with smaller classes) allows for more saturated sets.

### Saturation and the Quotient Map

The formal connection between $X$ and $X/\!\sim$ is the **canonical projection map** (or [quotient map](@entry_id:140877)) $\pi: X \to X/\!\sim$, defined by $\pi(x) = [x]$. This map sends each element to the [equivalence class](@entry_id:140585) containing it.

Saturated sets have a fundamental relationship with this map. A subset $S \subseteq X$ is saturated if and only if it is the [preimage](@entry_id:150899) of some subset of the quotient space $X/\!\sim$. More specifically, for any set $A \subseteq X/\!\sim$, its preimage $\pi^{-1}(A)$ is, by definition, the set of all $x \in X$ such that $\pi(x) \in A$. This is equivalent to the union of all equivalence classes $[x]$ that are elements of $A$. As a union of [equivalence classes](@entry_id:156032), $\pi^{-1}(A)$ is always a [saturated set](@entry_id:155857) [@problem_id:1572491].

Conversely, if a set $S$ is saturated, it is the union of some collection of [equivalence classes](@entry_id:156032). Let this collection of classes, viewed as a subset of $X/\!\sim$, be $A_S = \{\,[x] \mid x \in S\,\}$. Then $S = \pi^{-1}(A_S)$. This establishes a crucial correspondence: **the saturated subsets of $X$ are precisely the preimages of all subsets of $X/\!\sim$ under the [quotient map](@entry_id:140877).** An immediate consequence is that a set $S$ is saturated if and only if $S = \pi^{-1}(\pi(S))$.

This relationship allows us to define the **saturation** of an arbitrary subset $A \subseteq X$, denoted $\text{Sat}(A)$, as the smallest [saturated set](@entry_id:155857) containing $A$. This set can be constructed in two equivalent ways:
1.  As the union of all [equivalence classes](@entry_id:156032) that have a non-empty intersection with $A$: $\text{Sat}(A) = \bigcup_{x \in A} [x]$.
2.  Using the [quotient map](@entry_id:140877): $\text{Sat}(A) = \pi^{-1}(\pi(A))$.

Let's visualize this process. Consider $X = \mathbb{R}^2$ with the [equivalence relation](@entry_id:144135) $p_1 \sim p_2$ if $p_1$ and $p_2$ are equidistant from the origin. The equivalence classes are circles centered at the origin. Let $A$ be the rectangle $[1, 2] \times [3, 4]$. To find the saturation of $A$, we must take the union of all circles that intersect $A$. The points in $A$ have squared distances to the origin, $r^2 = x^2+y^2$, ranging from a minimum of $1^2+3^2=10$ (at the corner $(1,3)$) to a maximum of $2^2+4^2=20$ (at the corner $(2,4)$). Because the function $f(x,y)=x^2+y^2$ is continuous on the connected set $A$, it attains all values between its minimum and maximum. Therefore, $\pi(A)$ corresponds to the set of circles with squared radii in the interval $[10, 20]$. The saturation, $\text{Sat}(A) = \pi^{-1}(\pi(A))$, is the union of all these circles, which forms the closed annulus $\{(x,y) \in \mathbb{R}^2 \mid 10 \le x^2+y^2 \le 20\}$ [@problem_id:1572489].

Similarly, if the equivalence relation on $\mathbb{R}^2$ is defined by $P_1 \sim P_2$ if $x_1+y_1=x_2+y_2$, the [equivalence classes](@entry_id:156032) are lines of the form $x+y=c$. The saturation of the open [unit disk](@entry_id:172324) $D = \{(x,y) \mid x^2+y^2  1\}$ is the union of all lines $x+y=c$ that intersect $D$. The condition for a line to intersect the disk is that the distance from the origin to the line, which is $|c|/\sqrt{2}$, must be less than 1. This gives $|c|  \sqrt{2}$. Thus, $\text{Sat}(D)$ is the infinite open strip $\{(x,y) \in \mathbb{R}^2 \mid -\sqrt{2}  x+y  \sqrt{2}\}$ [@problem_id:1572500].

### The Algebra of Saturated Sets

The collection of all saturated subsets of $X$ exhibits a remarkable structure. Let $\mathcal{S}$ be this collection. We find that $\mathcal{S}$ is closed under the fundamental [set operations](@entry_id:143311) of union, intersection, and complement [@problem_id:1572427] [@problem_id:1572472]:

*   **Union**: If $\{S_i\}$ is a collection of saturated sets, their union $\bigcup S_i$ is saturated. If $x \in \bigcup S_i$, then $x \in S_k$ for some index $k$. Since $S_k$ is saturated, $[x] \subseteq S_k$, and thus $[x] \subseteq \bigcup S_i$.

*   **Intersection**: If $\{S_i\}$ is a collection of saturated sets, their intersection $\bigcap S_i$ is saturated. If $x \in \bigcap S_i$, then $x \in S_i$ for all $i$. Since each $S_i$ is saturated, $[x] \subseteq S_i$ for all $i$, and thus $[x] \subseteq \bigcap S_i$.

*   **Complement**: If $S$ is a [saturated set](@entry_id:155857), its complement $X \setminus S$ is also saturated. To prove this, let $x \in X \setminus S$. We must show that $[x] \subseteq X \setminus S$. Suppose for contradiction that there is some $y \in [x]$ such that $y \in S$. Since $S$ is saturated, the entire class $[y]$ must be in $S$. But since $y \sim x$, we have $[y]=[x]$. This implies $[x] \subseteq S$, which means $x \in S$, contradicting our initial assumption. Therefore, the class $[x]$ must be entirely contained in $X \setminus S$ [@problem_id:1572454].

Since the collection of saturated sets is closed under arbitrary unions and intersections, it forms a topology on $X$. Furthermore, being closed under complements means it is also a **$\sigma$-algebra**.

### Saturated Sets and the Quotient Topology

The true power of saturated sets emerges when we introduce topology. The **[quotient topology](@entry_id:150384)** on $X/\!\sim$ is defined as follows: a subset $V \subseteq X/\!\sim$ is open if and only if its preimage $\pi^{-1}(V)$ is an open set in $X$.

Combining this definition with our previous findings yields the central principle of this chapter: since the preimages $\pi^{-1}(V)$ are precisely the saturated subsets of $X$, the open sets in the [quotient space](@entry_id:148218) $X/\!\sim$ correspond one-to-one with the **saturated open subsets** of the original space $X$.

To understand the open sets of $X/\!\sim$, one must identify the subsets of $X$ that are both saturated with respect to $\sim$ and open in the topology of $X$.

A canonical example is the construction of the **real projective $n$-space**, $\mathbb{R}P^n$. This space is defined as the [quotient space](@entry_id:148218) of the $n$-sphere $S^n \subseteq \mathbb{R}^{n+1}$ under the [equivalence relation](@entry_id:144135) that identifies [antipodal points](@entry_id:151589): $x \sim -x$. The equivalence classes are pairs of opposite points $\{x, -x\}$. A subset $U \subseteq S^n$ is saturated with respect to this relation if, for every point $x \in U$, its antipode $-x$ is also in $U$. Such a set is often called **antipodally symmetric**. Therefore, the open sets of $\mathbb{R}P^n$ are in [one-to-one correspondence](@entry_id:143935) with the open, antipodally symmetric subsets of $S^n$ [@problem_id:1542574].

### Interaction with Topological Operations

While the algebraic properties of saturated sets are straightforward, their interaction with topological operations like closure can be subtle. A natural question arises: do the operations of saturation and closure commute? That is, for a subset $A \subseteq X$, is it always true that $\overline{\text{Sat}(A)} = \text{Sat}(\overline{A})$?

The answer is no. Let's explore a [counterexample](@entry_id:148660). Consider $\mathbb{R}^2$ with the projection map $\pi(x,y)=x$. The equivalence classes are vertical lines. Let $A$ be the set $A = \{ (x, y) \in \mathbb{R}^2 \mid 0 \le x  1 \text{ and } y(1 - x) = 1 \}$. This is the graph of the hyperbola $y = 1/(1-x)$ over the interval $[0, 1)$.

Let's compute the two sets in question, $S_1 = \overline{\text{Sat}(A)}$ and $S_2 = \text{Sat}(\overline{A})$ [@problem_id:1572479].

1.  **Saturation first, then closure ($S_1$):**
    The image of $A$ under $\pi$ is $\pi(A) = [0, 1)$.
    The saturation of $A$ is $\text{Sat}(A) = \pi^{-1}(\pi(A)) = \pi^{-1}([0, 1)) = [0, 1) \times \mathbb{R}$. This is an infinite vertical strip, open on the right.
    The closure of this strip in $\mathbb{R}^2$ includes its boundary, so $S_1 = \overline{\text{Sat}(A)} = [0, 1] \times \mathbb{R}$.

2.  **Closure first, then saturation ($S_2$):**
    First, we find the closure of $A$. As a point $(x_n, y_n) \in A$ approaches the line $x=1$ from the left (i.e., $x_n \to 1^-$), its $y$-coordinate $y_n = 1/(1-x_n)$ tends to infinity. The sequence has no [limit point](@entry_id:136272) in $\mathbb{R}^2$. Any convergent sequence from $A$ must converge to a point within $A$ itself. Therefore, the set $A$ is closed in $\mathbb{R}^2$, meaning $\overline{A} = A$.
    Now we saturate this closure: $S_2 = \text{Sat}(\overline{A}) = \text{Sat}(A) = [0, 1) \times \mathbb{R}$.

Comparing the results, we have $S_1 = [0, 1] \times \mathbb{R}$ and $S_2 = [0, 1) \times \mathbb{R}$. Clearly, $S_2$ is a [proper subset](@entry_id:152276) of $S_1$. This demonstrates that the operations of saturation and closure do not generally commute. In general, one can show that $\text{Sat}(\overline{A}) \subseteq \overline{\text{Sat}(A)}$, but the inclusion can be strict, as this example shows. The process of saturation can introduce new boundary points (the line $\{1\}\times\mathbb{R}$ in this case) that were not in the closure of the original set. This subtlety is a crucial reminder to be careful when interchanging operations in the context of [quotient spaces](@entry_id:274314).