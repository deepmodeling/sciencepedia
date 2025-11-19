## Introduction
In topology, we often seek to understand the essential shape of objects, ignoring fine geometric details in favor of properties that persist under continuous stretching and bending. The concept of "[continuous deformation](@entry_id:151691)" is not just an intuitive aid but a rigorously defined mathematical idea known as **homotopy**. Homotopy provides a powerful framework for classifying continuous functions by grouping them into [equivalence classes](@entry_id:156032) of mutually deformable maps. The central problem this approach solves is how to transition from an informal picture of "sameness" to a formal, workable structure.

This article establishes homotopy as a cornerstone of modern topology. We will embark on a journey through three chapters designed to build a comprehensive understanding of this concept:

-   First, in **Principles and Mechanisms**, we will establish the formal definition of homotopy and meticulously prove that it satisfies the three properties of an equivalence relation: reflexivity, symmetry, and transitivity.
-   Next, in **Applications and Interdisciplinary Connections**, we will explore the profound consequences of this classification, examining how it leads to the creation of algebraic invariants, helps us understand the structure of spaces, and forges links with other areas of mathematics.
-   Finally, in **Hands-On Practices**, you will have the opportunity to solidify your understanding by working through concrete examples and constructing homotopies in various settings.

By the end, you will not only grasp the definition of homotopy but also appreciate why its status as an [equivalence relation](@entry_id:144135) is the engine that drives much of algebraic topology.

## Principles and Mechanisms

In the study of topology, we are often less concerned with the precise geometric details of objects and more with their fundamental, structural properties that are preserved under [continuous deformation](@entry_id:151691). This notion of "[continuous deformation](@entry_id:151691)" is not merely an intuitive guide; it is a rigorously defined concept known as **homotopy**. Homotopy allows us to classify continuous functions, or maps, by grouping them into collections that are mutually deformable into one another. The most crucial property of this classification scheme is that it forms an [equivalence relation](@entry_id:144135), partitioning the set of all [continuous maps](@entry_id:153855) between two spaces into distinct **homotopy classes**. This chapter will establish the formal definition of homotopy, prove that it constitutes an [equivalence relation](@entry_id:144135), and explore its deeper interpretations and variations.

### The Formal Definition of Homotopy

Let $X$ and $Y$ be [topological spaces](@entry_id:155056). Intuitively, two [continuous maps](@entry_id:153855), $f: X \to Y$ and $g: X \to Y$, are homotopic if we can continuously transform $f$ into $g$. To make this precise, we can imagine this transformation occurring over a period of time, which we can normalize to the unit interval $I = [0, 1]$. For each "moment in time" $t \in I$, we have an intermediate map $f_t: X \to Y$. The transformation starts with $f_0 = f$ and ends with $f_1 = g$.

The key requirement is that this entire process must be continuous, not just at each moment, but across both space and time. We formalize this by combining the family of maps $\{f_t\}_{t \in I}$ into a single function $H$.

A **homotopy** between two [continuous maps](@entry_id:153855) $f, g: X \to Y$ is a continuous map $H: X \times I \to Y$ such that for every point $x \in X$:
1. $H(x, 0) = f(x)$
2. $H(x, 1) = g(x)$

If such a map $H$ exists, we say that $f$ is **homotopic** to $g$, denoted $f \simeq g$.

The condition that $H$ must be continuous is of paramount importance. The domain $X \times I$ is endowed with the **product topology**. The continuity of $H$ is **joint continuity** in both variables, $x$ and $t$. This is a significantly stronger condition than requiring $H$ to be continuous in each variable separately [@problem_id:1557305]. For instance, requiring that each intermediate map $f_t(x) = H(x,t)$ is continuous and that for each fixed $x$, the path $t \mapsto H(x,t)$ is continuous, is not sufficient to guarantee that $H$ is continuous on $X \times I$. A classic counterexample from analysis is the function $F(x, y) = \frac{xy}{x^2 + y^2}$ (with $F(0,0)=0$), which is continuous along every horizontal and vertical line through the origin but is not jointly continuous at $(0,0)$. The definition of homotopy demands this stronger, joint continuity to truly capture the idea of a single, unified deformation process.

### An Alternative Viewpoint: Paths in Function Spaces

A powerful way to conceptualize homotopy is to shift our perspective from a map on a [product space](@entry_id:151533) to a path in a space of functions. Let $C(X, Y)$, sometimes denoted $Y^X$, be the set of all continuous functions from $X$ to $Y$. This set can itself be given a topology, most commonly the **[compact-open topology](@entry_id:153876)**, turning it into a **function space**.

In this context, a homotopy $H: X \times I \to Y$ can be reinterpreted. For each $t \in I$, the map $H_t(x) = H(x, t)$ is an element of $C(X, Y)$. We can thus define a map $\gamma: I \to C(X, Y)$ by setting $\gamma(t) = H_t$. The continuity of the original homotopy $H$ is equivalent to the continuity of this new map $\gamma$.

Therefore, a homotopy between two maps $f$ and $g$ is precisely a **path** in the [function space](@entry_id:136890) $C(X, Y)$ that starts at the point $f$ and ends at the point $g$ [@problem_id:1557303]. From this viewpoint, two functions are homotopic if and only if they belong to the same **path-component** of the function space $C(X, Y)$. The set of homotopy classes, denoted $[X, Y]$, is therefore in [one-to-one correspondence](@entry_id:143935) with the set of [path-components](@entry_id:145705) of $C(X, Y)$.

This perspective can yield profound insights. For example, consider the space $C(S^1, \mathbb{R}^2)$ of all [continuous maps](@entry_id:153855) from a circle to the plane. The target space $\mathbb{R}^2$ is a [convex set](@entry_id:268368). This [convexity](@entry_id:138568) is inherited by the [function space](@entry_id:136890) $C(S^1, \mathbb{R}^2)$ under pointwise operations. For any two maps $f, g \in C(S^1, \mathbb{R}^2)$, the **straight-line homotopy** $H(x, t) = (1-t)f(x) + tg(x)$ is a valid, continuous homotopy from $f$ to $g$. In the [function space](@entry_id:136890) view, this corresponds to a straight-line path from $f$ to $g$. Because such a path always exists, the entire space $C(S^1, \mathbb{R}^2)$ is path-connected. Consequently, there is only one homotopy class of maps from $S^1$ to $\mathbb{R}^2$. Any map from the circle to the plane can be continuously deformed into any other [@problem_id:1655949].

### Homotopy as an Equivalence Relation

The true classificatory power of homotopy stems from the fact that it is an **equivalence relation**. This means it partitions the set $C(X, Y)$ into disjoint [equivalence classes](@entry_id:156032), which are precisely the homotopy classes. To establish this, we must prove that the relation $\simeq$ is reflexive, symmetric, and transitive.

#### Reflexivity: $f \simeq f$

For any continuous map $f: X \to Y$, we must show it is homotopic to itself. The construction is straightforward: we define a homotopy that does not change the map at all over the time interval. This is known as the **stationary homotopy** [@problem_id:1655981].

Let $H: X \times I \to Y$ be defined by $H(x, t) = f(x)$ for all $(x, t) \in X \times I$.
1.  **Continuity:** The map $H$ is the composition of the projection map $p_X: X \times I \to X$, given by $p_X(x, t) = x$, followed by the map $f: X \to Y$. Since both $p_X$ and $f$ are continuous, their composition $H = f \circ p_X$ is also continuous.
2.  **Boundary Conditions:** At $t=0$, we have $H(x, 0) = f(x)$. At $t=1$, we have $H(x, 1) = f(x)$.

Both conditions are met, proving that $f \simeq f$. Every map is homotopic to itself.

#### Symmetry: If $f \simeq g$, then $g \simeq f$

Suppose we have a homotopy $F: X \times I \to Y$ from $f$ to $g$. To show symmetry, we need to construct a homotopy from $g$ back to $f$. The natural idea is to "run the deformation backwards." We can achieve this by reversing the time parameter.

Let $F$ be a homotopy from $f$ to $g$. Define a new map $G: X \times I \to Y$ by $G(x, t) = F(x, 1-t)$ [@problem_id:1655993].
1.  **Continuity:** The map $t \mapsto 1-t$ is continuous. Thus, the map $(x, t) \mapsto (x, 1-t)$ is a continuous self-map of $X \times I$. Since $G$ is the composition of this map with the [continuous map](@entry_id:153772) $F$, $G$ is continuous.
2.  **Boundary Conditions:** At $t=0$, we have $G(x, 0) = F(x, 1-0) = F(x, 1) = g(x)$. At $t=1$, we have $G(x, 1) = F(x, 1-1) = F(x, 0) = f(x)$.

Thus, $G$ is a valid homotopy from $g$ to $f$, proving that if $f \simeq g$, then $g \simeq f$.

#### Transitivity: If $f \simeq g$ and $g \simeq h$, then $f \simeq h$

Suppose we have a homotopy $F: X \times I \to Y$ from $f$ to $g$, and another homotopy $G: X \times I \to Y$ from $g$ to $h$. To prove transitivity, we must construct a single homotopy from $f$ to $h$. The strategy is to concatenate the two homotopies: perform the first deformation from $t=0$ to $t=1/2$, and the second from $t=1/2$ to $t=1$.

We define a new map $H: X \times I \to Y$ as follows [@problem_id:1655983]:
$$
H(x, t) = \begin{cases}
F(x, 2t)  & \text{if } 0 \le t \le \frac{1}{2} \\
G(x, 2t - 1)  & \text{if } \frac{1}{2} \le t \le 1
\end{cases}
$$
1.  **Continuity:** This map is defined piecewise. On the closed set $X \times [0, 1/2]$, the map $(x, t) \mapsto (x, 2t)$ is continuous, so the composition with $F$ is continuous. Similarly, on the [closed set](@entry_id:136446) $X \times [1/2, 1]$, the map is continuous. For the overall map $H$ to be continuous, the two definitions must agree on the overlap, which is the set $X \times \{1/2\}$.
    At $t = 1/2$, the first rule gives $F(x, 2(1/2)) = F(x, 1) = g(x)$.
    The second rule gives $G(x, 2(1/2) - 1) = G(x, 0) = g(x)$.
    Since the pieces agree on their common boundary, the **Pasting Lemma** guarantees that the combined map $H$ is continuous on the entire domain $X \times I$.
2.  **Boundary Conditions:** At $t=0$, we use the first rule: $H(x, 0) = F(x, 0) = f(x)$. At $t=1$, we use the second rule: $H(x, 1) = G(x, 1) = h(x)$.

Thus, $H$ is a homotopy from $f$ to $h$, proving transitivity. Since homotopy is reflexive, symmetric, and transitive, it is an equivalence relation. This partitioning of $C(X,Y)$ into homotopy classes $[X,Y]$ is a cornerstone of algebraic topology. The structure of an [equivalence relation](@entry_id:144135) implies that if a collection of maps are all homotopic to a single "mediating" map, they must all be homotopic to one another, forming part of a single [equivalence class](@entry_id:140585) [@problem_id:1655978].

### Refinements of the Homotopy Relation

While the general definition of homotopy is powerful, it is often necessary to impose additional constraints to study more refined [topological properties](@entry_id:154666). This leads to important variations of the homotopy concept.

#### Relative Homotopy

In many situations, we want to deform a map while keeping it fixed on a certain subset of its domain. Let $A$ be a subset of $X$. A **homotopy relative to A** between two maps $f, g: X \to Y$ (which are assumed to agree on $A$) is a homotopy $H: X \times I \to Y$ from $f$ to $g$ that additionally satisfies:
$$
H(a, t) = f(a) = g(a) \quad \text{for all } a \in A \text{ and all } t \in I.
$$
This relation is denoted $f \simeq_A g$. It is a simple exercise to verify that the constructions used to prove reflexivity, symmetry, and transitivity for general homotopy also preserve this additional condition. For instance, the stationary homotopy is constant on $A$, the reverse homotopy inherits the fixed property from the original, and the concatenated homotopy is fixed on $A$ if its constituent parts are. Therefore, homotopy relative to $A$ is also an [equivalence relation](@entry_id:144135) [@problem_id:1557311].

#### Path Homotopy and Free Homotopy

A particularly important case of relative homotopy arises when studying paths and loops. A **path** in a space $Y$ is a map $\gamma: I \to Y$. A **loop based at $y_0 \in Y$** is a path $\gamma$ such that $\gamma(0) = \gamma(1) = y_0$.

A **[path-homotopy](@entry_id:153567)** (or **based homotopy**) between two loops $f, g: I \to Y$ based at $y_0$ is a homotopy relative to the boundary of the interval, $A=\{0, 1\}$. This means the homotopy $H: I \times I \to Y$ must satisfy $H(s, 0) = f(s)$, $H(s, 1) = g(s)$, and critically, the basepoint remains fixed throughout the deformation:
$$
H(0, t) = y_0 \quad \text{and} \quad H(1, t) = y_0 \quad \text{for all } t \in I.
$$
This is a much stricter condition than a general homotopy between the loops $f$ and $g$, which is sometimes called a **free homotopy**. A free homotopy allows the endpoints of the intermediate paths to move during the deformation.

The distinction is not trivial. Two loops can be freely homotopic but not path-homotopic [@problem_id:1557291]. For example, in the figure-eight space (two circles joined at a point $x_0$), let $a$ be the loop traversing the first circle and $b$ be the loop traversing the second. The loop $a$ is *not* path-homotopic to the loop $g = b \cdot a \cdot b^{-1}$ (traverse $b$, then $a$, then $b$ in reverse). The basepoint prevents the loop $a$ from being "slid" around the second circle. However, $a$ and $g$ *are* freely homotopic. The relation between free and based homotopy classes is deep: two loops are freely homotopic if and only if their based homotopy classes are conjugate elements in the fundamental group $\pi_1(X, x_0)$.

### A Deeper Look at Continuity

We conclude by revisiting the role of continuity in the definition of homotopy. We defined homotopy using a *jointly continuous* function $H: X \times I \to Y$. What if we were to relax this? Consider a "weak homotopy" relation, $f \sim_w g$, defined by a function $H(x,t)$ that is only required to be **separately continuous**: continuous in $x$ for each fixed $t$, and continuous in $t$ for each fixed $x$.

Surprisingly, this weaker relation $\sim_w$ is also an equivalence relation. The standard constructions for reflexivity, symmetry, and [transitivity](@entry_id:141148) preserve the property of separate continuity [@problem_id:1557281]. For example, in the transitivity proof, the concatenated map $H_3(x, t)$ is continuous in $x$ for any fixed $t$ (since it is either $H_1(x, 2t)$ or $H_2(x, 2t-1)$), and it is continuous in $t$ for any fixed $x$ (by the Pasting Lemma for single-variable functions).

This result does not diminish the importance of joint continuity in the standard definition. Joint continuity is essential for the interpretation of a homotopy as a single, coherent deformation and for its correspondence with a [continuous path](@entry_id:156599) in a [function space](@entry_id:136890). However, the fact that the formal algebraic properties of an [equivalence relation](@entry_id:144135) can be established with a weaker condition deepens our understanding of the structures at play. It separates the topological essence of the deformation from the algebraic properties of the resulting relation.