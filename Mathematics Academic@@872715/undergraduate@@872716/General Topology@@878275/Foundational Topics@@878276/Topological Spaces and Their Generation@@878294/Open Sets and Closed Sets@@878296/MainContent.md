## Introduction
In the study of mathematics, the concepts of [open and closed sets](@entry_id:140356) form the bedrock of [general topology](@entry_id:152375). They provide a powerful language to generalize intuitive ideas of "nearness," "continuity," and "limits" from the familiar context of the [real number line](@entry_id:147286) and Euclidean space to far more abstract settings. This article addresses the fundamental shift from an intuitive, distance-based understanding of these concepts to a rigorous, axiomatic framework that does not require a metric. By mastering this abstract foundation, you will gain the tools to analyze the intrinsic structure of spaces in diverse fields of modern mathematics.

This article will guide you through the essential theory and application of [open and closed sets](@entry_id:140356) across three chapters. In "Principles and Mechanisms," we will establish the axiomatic definition of a topology, explore the dual nature of [open and closed sets](@entry_id:140356), and introduce the crucial operators of interior, closure, and boundary. Following this, "Applications and Interdisciplinary Connections" will showcase how these foundational ideas are deployed in real analysis, functional analysis, and linear algebra, demonstrating their role in defining continuity and characterizing important mathematical structures. Finally, "Hands-On Practices" will provide a series of targeted problems to solidify your understanding and test your ability to apply these concepts in various topological contexts.

## Principles and Mechanisms

This chapter delves into the foundational concepts of [general topology](@entry_id:152375): [open and closed sets](@entry_id:140356). We will move beyond the intuitive notions from calculus and analysis to establish a rigorous, axiomatic framework. This framework allows us to generalize ideas like continuity and convergence to settings far more abstract than the real number line. We will first define a [topological space](@entry_id:149165) through its collection of open sets and then explore the dual concept of closed sets. Subsequently, we will introduce the essential tools for analyzing the structure of subsets within a topological space: the interior, closure, and boundary operators.

### The Axiomatic Definition of a Topology

In analysis, an open set in $\mathbb{R}^n$ is typically defined as a set where every point has a small [open ball](@entry_id:141481) around it that is still contained within the set. While this is a powerful and intuitive starting point, its reliance on a metric (a distance function) is restrictive. General topology seeks to capture the essential properties of "openness" without needing a concept of distance. It achieves this by abstracting the key behaviors of collections of open sets into a set of axioms.

A **topology** on a non-empty set $X$ is a collection $\mathcal{T}$ of subsets of $X$, called **open sets**, that satisfies the following three axioms:

1.  The [empty set](@entry_id:261946) $\emptyset$ and the entire space $X$ are open (i.e., $\emptyset \in \mathcal{T}$ and $X \in \mathcal{T}$).
2.  The union of any arbitrary collection of open sets is open (i.e., if $\{A_i\}_{i \in I}$ is a collection of sets in $\mathcal{T}$, then $\bigcup_{i \in I} A_i \in \mathcal{T}$).
3.  The intersection of any finite collection of open sets is open (i.e., if $\{A_i\}_{i=1}^n$ is a finite collection of sets in $\mathcal{T}$, then $\bigcap_{i=1}^n A_i \in \mathcal{T}$).

The pair $(X, \mathcal{T})$ is called a **[topological space](@entry_id:149165)**. The choice of $\mathcal{T}$ is crucial; a single set $X$ can be endowed with many different topologies, each giving rise to a different topological space with unique properties.

To make this definition concrete, let's examine a specific construction. Consider the set $X = \{w, x, y, z\}$. We can propose different collections of subsets and test them against the axioms. Let's analyze the collection $\mathcal{T}_1 = \{A \subseteq X \mid w \in A \text{ and } x \in A \} \cup \{\emptyset\}$.

1.  **Axiom 1**: By its explicit definition, $\emptyset \in \mathcal{T}_1$. The entire set $X = \{w, x, y, z\}$ contains both $w$ and $x$, so $X \in \mathcal{T}_1$. This axiom holds.
2.  **Axiom 2 (Arbitrary Unions)**: Let $\{A_i\}_{i \in I}$ be a collection of sets from $\mathcal{T}_1$. If all $A_i$ are the empty set, their union is $\emptyset$, which is in $\mathcal{T}_1$. If at least one $A_i$ is non-empty, then this $A_i$ must contain both $w$ and $x$. Consequently, the union $\bigcup_{i \in I} A_i$ must also contain both $w$ and $x$, placing it in $\mathcal{T}_1$. This axiom holds.
3.  **Axiom 3 (Finite Intersections)**: Let $A_1, A_2 \in \mathcal{T}_1$. If either set is $\emptyset$, the intersection is $\emptyset \in \mathcal{T}_1$. If both are non-empty, then both must contain $w$ and $x$. It follows that their intersection $A_1 \cap A_2$ must also contain $w$ and $x$, which means $A_1 \cap A_2 \in \mathcal{T}_1$. This axiom holds for two sets, and by induction, for any finite number of sets.

Since all three axioms are satisfied, $\mathcal{T}_1$ is a valid topology on $X$.

Not every plausible-looking collection forms a topology. Consider another collection on the same set $X$: $\mathcal{T}_2 = \{A \subseteq X \mid A \cap \{y, z\} \neq \emptyset\} \cup \{\emptyset\}$. While it satisfies the first two axioms, it fails the third. For example, let $A = \{w, y\}$ and $B = \{w, z\}$. Both sets are in $\mathcal{T}_2$ because $A \cap \{y, z\} = \{y\}$ and $B \cap \{y, z\} = \{z\}$, both non-empty. However, their intersection is $A \cap B = \{w\}$. Since $\{w\} \cap \{y, z\} = \emptyset$, the set $\{w\}$ is not in $\mathcal{T}_2$. This failure to be closed under finite intersections demonstrates that $\mathcal{T}_2$ is not a topology on $X$ [@problem_id:1565336].

### Closed Sets and the Dual Axioms

Having defined open sets axiomatically, we can define **[closed sets](@entry_id:137168)** in a very simple way: a subset $F$ of a [topological space](@entry_id:149165) $(X, \mathcal{T})$ is closed if its complement, $X \setminus F$, is open.

This definition, combined with the axioms for open sets and De Morgan's laws, implies a corresponding set of axioms for the collection of all closed sets, which we can denote by $\mathcal{F}$.

1.  Since $\emptyset$ and $X$ are open, their complements, $X \setminus \emptyset = X$ and $X \setminus X = \emptyset$, are closed. Thus, $\emptyset \in \mathcal{F}$ and $X \in \mathcal{F}$.
2.  From the axiom of arbitrary unions for open sets, it follows that the intersection of an arbitrary collection of [closed sets](@entry_id:137168) is closed.
3.  From the axiom of finite intersections for open sets, it follows that the union of a finite collection of [closed sets](@entry_id:137168) is closed.

It is crucial to note the switch: arbitrary unions for open sets corresponds to arbitrary intersections for [closed sets](@entry_id:137168), and finite intersections for open sets corresponds to finite unions for [closed sets](@entry_id:137168). One can, in fact, define a topology by specifying a collection of subsets $\mathcal{F}$ to be the "closed sets" if they satisfy these three dual axioms. The open sets are then defined as the complements of the sets in $\mathcal{F}$.

Let's consider an example of this dual approach. Let $X$ be any set and fix a point $p \in X$. Let us define a collection $\mathcal{F} = \{A \subseteq X \mid p \notin A\} \cup \{X\}$ and propose it as the collection of closed sets for a topology [@problem_id:1565352]. We verify the axioms for closed sets:

1.  **Axiom 1**: The point $p$ is not in the [empty set](@entry_id:261946), so $\emptyset \in \mathcal{F}$. By definition, $X \in \mathcal{F}$. This holds.
2.  **Axiom 2 (Arbitrary Intersections)**: Let $\{A_i\}_{i \in I}$ be a collection of sets from $\mathcal{F}$. The intersection is $\bigcap_{i \in I} A_i$. If any of the $A_i$ do not contain $p$, then the intersection, being a subset of that $A_i$, cannot contain $p$ either. In this case, the intersection is in $\mathcal{F}$. The only other possibility is that all $A_i$ are equal to $X$, in which case their intersection is also $X$, which is in $\mathcal{F}$. This holds.
3.  **Axiom 3 (Finite Unions)**: Let $A_1, \dots, A_n$ be a finite collection of sets from $\mathcal{F}$. If any $A_k = X$, their union is $X$, which is in $\mathcal{F}$. If all $A_i$ are proper subsets of $X$, then $p \notin A_i$ for all $i$. Consequently, $p$ cannot be in their union $\bigcup_{i=1}^n A_i$. Thus, the union is in $\mathcal{F}$. This holds.

Since $\mathcal{F}$ satisfies the axioms for closed sets, it validly defines a topology on $X$. This topology is known as the **excluded point topology**. The open sets in this topology are the complements of the sets in $\mathcal{F}$, which are $\{A^c \mid p \notin A\} \cup \{X^c\} = \{B \subseteq X \mid p \in B\} \cup \{\emptyset\}$. This is called the **particular point topology**.

### Generating Topologies from a Basis

Specifying every single open set to define a topology can be cumbersome, especially for infinite sets. A more efficient method is to specify a **basis** for the topology. A collection of open sets $\mathcal{B} \subseteq \mathcal{T}$ is a basis for the topology $\mathcal{T}$ if every open set in $\mathcal{T}$ can be expressed as a union of elements from $\mathcal{B}$.

This is analogous to how in $\mathbb{R}^2$, all open sets can be constructed by taking unions of open disks. The collection of all open disks thus forms a basis for the [standard topology](@entry_id:152252) on $\mathbb{R}^2$.

Given a collection of subsets $\mathcal{B}$ of a set $X$, it can be used to *generate* a topology if it satisfies two conditions: (1) for every $x \in X$, there is some $B \in \mathcal{B}$ with $x \in B$, and (2) for any two basis elements $B_1, B_2 \in \mathcal{B}$ and any point $x \in B_1 \cap B_2$, there exists a third basis element $B_3 \in \mathcal{B}$ such that $x \in B_3 \subseteq B_1 \cap B_2$. If these hold, the topology $\mathcal{T}$ generated by $\mathcal{B}$ is defined as the collection of all possible unions of elements of $\mathcal{B}$.

Let's see this in action on a finite set $X = \{a, b, c\}$. Consider the basis $\mathcal{B} = \{\{a\}, \{a,b\}, \{c\}\}$. The open sets are all possible unions of these basis elements [@problem_id:1565356]:
-   The empty union: $\emptyset$
-   Single elements: $\{a\}$, $\{a,b\}$, $\{c\}$
-   Unions of two elements: $\{a\} \cup \{a,b\} = \{a,b\}$, $\{a\} \cup \{c\} = \{a,c\}$, $\{a,b\} \cup \{c\} = \{a,b,c\} = X$
-   Union of all three: $\{a\} \cup \{a,b\} \cup \{c\} = X$

Collecting these and removing duplicates, the topology generated by $\mathcal{B}$ is:
$\mathcal{T} = \{\emptyset, \{a\}, \{c\}, \{a,b\}, \{a,c\}, X\}$

Now, we can find the collection of all closed sets by taking the complements of these open sets with respect to $X$:
-   $X \setminus \emptyset = X$
-   $X \setminus \{a\} = \{b,c\}$
-   $X \setminus \{c\} = \{a,b\}$
-   $X \setminus \{a,b\} = \{c\}$
-   $X \setminus \{a,c\} = \{b\}$
-   $X \setminus X = \emptyset$

So, the collection of closed sets is $\mathcal{F} = \{\emptyset, \{b\}, \{c\}, \{a,b\}, \{b,c\}, X\}$. This exercise demonstrates the complete chain of logic from a basis to the open sets and finally to the [closed sets](@entry_id:137168).

### Interior, Closure, and Boundary

With a topology in place, we can now define operators that describe the relationship between a subset and the space around it. The three most fundamental operators are the interior, the closure, and the boundary.

The **interior** of a set $A$, denoted $A^\circ$ or $\text{Int}(A)$, is the union of all open sets contained within $A$. By the union axiom for open sets, this union is itself an open set. It is therefore the largest open set contained in $A$. Intuitively, the interior consists of all points of $A$ that are "safely" inside $A$, surrounded only by other points of $A$.

The **closure** of a set $A$, denoted $\overline{A}$ or $\text{cl}(A)$, is the intersection of all closed sets containing $A$. By the [intersection axiom](@entry_id:274406) for [closed sets](@entry_id:137168), this intersection is itself a closed set. It is therefore the smallest closed set containing $A$. The closure of $A$ can also be characterized as the set of all **adherent points** of $A$. A point $x \in X$ is an adherent point of $A$ if every open set containing $x$ (i.e., every **neighborhood** of $x$) has a non-empty intersection with $A$.

The **boundary** of a set $A$, denoted $\partial A$, consists of all points that are, in a topological sense, "stuck" between $A$ and its complement, $A^c = X \setminus A$. Formally, the boundary is the set of points that belong to the closure of $A$ and also to the closure of its complement:
$$ \partial A = \overline{A} \cap \overline{A^c} $$
An equivalent and often useful definition is $\partial A = \overline{A} \setminus A^\circ$. A point $x$ is in the boundary of $A$ if and only if every neighborhood of $x$ contains at least one point from $A$ and at least one point from $A^c$.

### Exploring the Operators: Key Examples and Properties

The behavior of these operators reveals deep properties of the [topological space](@entry_id:149165) and its subsets. Let's investigate their properties using some critical examples.

#### Interior and Unions

One might naively assume that the interior operator distributes over unions; that is, $\text{Int}(A \cup B) = \text{Int}(A) \cup \text{Int}(B)$. A powerful counterexample shows this is false. Consider $\mathbb{R}$ with its [standard topology](@entry_id:152252). Let $A = \mathbb{Q}$, the set of rational numbers, and $B = \mathbb{R} \setminus \mathbb{Q}$, the set of irrational numbers [@problem_id:1565340].

The union is $A \cup B = \mathbb{R}$. Since $\mathbb{R}$ is an open set in its own topology, $\text{Int}(A \cup B) = \text{Int}(\mathbb{R}) = \mathbb{R}$.

Now, what is the interior of $\mathbb{Q}$? An open set in $\mathbb{R}$ must contain an [open interval](@entry_id:144029) $(a,b)$ with $a  b$. However, it is a fundamental property of the real numbers that every such interval contains [irrational numbers](@entry_id:158320). Therefore, no non-empty open set can be a subset of $\mathbb{Q}$. This implies $\text{Int}(\mathbb{Q}) = \emptyset$. Similarly, every open interval $(a,b)$ also contains rational numbers, so no non-empty open set can be a subset of $\mathbb{R} \setminus \mathbb{Q}$. Thus, $\text{Int}(\mathbb{R} \setminus \mathbb{Q}) = \emptyset$.

Combining these results, we find:
$$ \text{Int}(A) \cup \text{Int}(B) = \emptyset \cup \emptyset = \emptyset $$
Clearly, $\text{Int}(A \cup B) = \mathbb{R}$ is not equal to $\text{Int}(A) \cup \text{Int}(B) = \emptyset$. This example dramatically illustrates that the interior of a union can be much larger than the union of the interiors.

#### Closure and Limit Points

The [closure of a set](@entry_id:143367) consists of the set itself plus all of its "limit points." A **[limit point](@entry_id:136272)** (or **accumulation point**) of a set $A$ is a point $x$ such that every neighborhood of $x$ intersects $A$ at a point *other than* $x$ itself. The set of all [limit points](@entry_id:140908) of $A$ is called the **derived set**, denoted $A'$. A key theorem states that $\overline{A} = A \cup A'$.

Let's find the [closure of a set](@entry_id:143367) defined by a sequence in $\mathbb{R}$ with the standard topology [@problem_id:1565338]. Consider the set $S = \{ x_n = \frac{(-1)^n}{n} + \sin(\frac{n\pi}{2}) \mid n \in \mathbb{Z}^+ \}$. To understand this set, we analyze its behavior for different values of $n$:
-   For even $n=2m$, $x_n = \frac{1}{2m} + \sin(m\pi) = \frac{1}{2m}$. This subsequence approaches $0$.
-   For $n \equiv 1 \pmod{4}$, $x_n = -\frac{1}{n} + \sin(\frac{n\pi}{2}) = 1 - \frac{1}{n}$. This subsequence approaches $1$. (Note for $n=1$, $x_1=0$, so $0 \in S$).
-   For $n \equiv 3 \pmod{4}$, $x_n = -\frac{1}{n} + \sin(\frac{n\pi}{2}) = -1 - \frac{1}{n}$. This subsequence approaches $-1$.

The set $S$ is a [countable set](@entry_id:140218) of points. As such, it cannot contain any open interval, so its interior is empty: $\text{Int}(S) = \emptyset$.

The [limit points](@entry_id:140908) of $S$ are the values approached by its subsequences: $0$, $1$, and $-1$. Therefore, the derived set is $S' = \{-1, 0, 1\}$. The closure is the union of the set and its limit points:
$$ \overline{S} = S \cup S' = S \cup \{-1, 0, 1\} $$

#### The Nature of Boundaries

The boundary of a set can sometimes be surprising. Let's return to the set of rational numbers in the plane, $S = \mathbb{Q}^2$, considered as a subset of $\mathbb{R}^2$ with the standard topology [@problem_id:1565343].
-   **Closure of $\mathbb{Q}^2$**: Any open disk in $\mathbb{R}^2$ contains points where both coordinates are rational. This is due to the density of $\mathbb{Q}$ in $\mathbb{R}$. Therefore, every point in $\mathbb{R}^2$ is an adherent point of $\mathbb{Q}^2$, which means $\overline{\mathbb{Q}^2} = \mathbb{R}^2$.
-   **Interior of $\mathbb{Q}^2$**: Any open disk in $\mathbb{R}^2$ also contains points where at least one coordinate is irrational. Therefore, no non-empty open set is contained within $\mathbb{Q}^2$, which means $\text{Int}(\mathbb{Q}^2) = \emptyset$.

Using the formula $\partial S = \overline{S} \setminus S^\circ$, we find the boundary of $\mathbb{Q}^2$ to be:
$$ \partial(\mathbb{Q}^2) = \overline{\mathbb{Q}^2} \setminus \text{Int}(\mathbb{Q}^2) = \mathbb{R}^2 \setminus \emptyset = \mathbb{R}^2 $$
This remarkable result states that *every* point in the plane is a boundary point of the set of points with rational coordinates. This is a consequence of both $\mathbb{Q}^2$ and its complement being **dense** in $\mathbb{R}^2$ (a set is dense if its closure is the entire space).

This phenomenon is not limited to uncountable spaces. Consider a finite space $X = \{a, b, c, d, e, f\}$ with the topology generated by the basis $\mathcal{B} = \{\{a, b\}, \{c, d\}, \{e, f\}\}$. This basis partitions $X$ into three blocks. The open sets (and also the closed sets) are unions of these blocks. Let $S = \{a, c, e\}$. The smallest closed set containing $S$ must include every block that $S$ intersects. Since $S$ has one point in each block, the smallest [closed set](@entry_id:136446) containing $S$ is the union of all blocks, which is $X$. Thus, $\overline{S} = X$. The complement is $S^c = \{b, d, f\}$, which also intersects every block. By the same logic, $\overline{S^c} = X$. The boundary is therefore [@problem_id:1565349]:
$$ \partial S = \overline{S} \cap \overline{S^c} = X \cap X = X $$
Here again, every point in the space is a boundary point.

### Comparative Topologies and Metric Spaces

The properties of a set depend entirely on the chosen topology. A set can be open in one topology but not in another.

#### Finer and Coarser Topologies

Given two topologies $\mathcal{T}_1$ and $\mathcal{T}_2$ on the same set $X$, we say that $\mathcal{T}_2$ is **finer** than $\mathcal{T}_1$ (or $\mathcal{T}_1$ is **coarser** than $\mathcal{T}_2$) if $\mathcal{T}_1 \subseteq \mathcal{T}_2$. A finer topology has "more" open sets.

A classic example on $\mathbb{R}$ involves the **[standard topology](@entry_id:152252)** $\mathcal{T}_s$, generated by [open intervals](@entry_id:157577) $(a,b)$, and the **[lower limit topology](@entry_id:152239)** $\mathcal{T}_l$ (also called the Sorgenfrey topology), generated by half-open intervals $[a,b)$. Any standard [open interval](@entry_id:144029) can be written as a union of lower-limit basis elements: $(a,b) = \bigcup_{x \in (a,b)} [x, b)$. This shows that any open set in $\mathcal{T}_s$ is also open in $\mathcal{T}_l$, so $\mathcal{T}_s \subseteq \mathcal{T}_l$. The inclusion is strict, since $[0,1)$ is open in $\mathcal{T}_l$ but not in $\mathcal{T}_s$. Thus, the [lower limit topology](@entry_id:152239) is strictly finer than the [standard topology](@entry_id:152252).

This relationship has a direct consequence for closed sets. If a set $F$ is closed in the coarser topology ($\mathcal{T}_s$), its complement $\mathbb{R} \setminus F$ is open in $\mathcal{T}_s$. Since every set open in $\mathcal{T}_s$ is also open in the finer topology $\mathcal{T}_l$, $\mathbb{R} \setminus F$ must be open in $\mathcal{T}_l$. This, by definition, means $F$ is closed in $\mathcal{T}_l$. This leads to an important conclusion: any set closed in the standard topology on $\mathbb{R}$ is also closed in the [lower limit topology](@entry_id:152239). It is therefore impossible to find a set that is closed in $\mathcal{T}_s$ but not in $\mathcal{T}_l$ [@problem_id:1565364].

The [lower limit topology](@entry_id:152239) has interesting features. For instance, the basis elements $[a, b)$ are not only open by definition, but they are also closed. The complement is $\mathbb{R} \setminus [a,b) = (-\infty, a) \cup [b, \infty)$. The set $(-\infty, a)$ is open in $\mathcal{T}_l$ (it's a union of basis elements like $[x,a)$ for $x  a$), and the set $[b, \infty)$ is open in $\mathcal{T}_l$ (it's a union of basis elements like $[y, y+1)$ for $y \ge b$). Since the complement is a union of open sets, it is open, which means $[a, b)$ is a [closed set](@entry_id:136446). Such sets that are both open and closed are called **clopen** sets. In the [lower limit topology](@entry_id:152239) on $\mathbb{R}$, there are infinitely many non-trivial [clopen sets](@entry_id:156588). This contrasts with the standard topology on $\mathbb{R}$, where the only [clopen sets](@entry_id:156588) are the trivial ones, $\emptyset$ and $\mathbb{R}$ itself.