## Introduction
In the study of differential geometry, understanding the global structure of manifolds is as crucial as analyzing their local Euclidean nature. One of the most fundamental global properties is connectivity—the idea that a space is a single, unbroken piece. While intuitive, this concept requires a precise mathematical formulation to be useful. This article bridges that gap by introducing [path-connectedness](@entry_id:142695), a rigorous and powerful tool for describing the topological [cohesion](@entry_id:188479) of geometric objects.

Across three focused chapters, you will build a comprehensive understanding of this concept. The first chapter, **Principles and Mechanisms**, establishes the formal definitions of a path and a path-connected set, explores methods for proving [path-connectedness](@entry_id:142695), and clarifies its relationship with the more general notion of connectedness. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these principles are applied to classify fundamental manifolds, analyze Lie groups, and serve as a gateway to algebraic topology. Finally, **Hands-On Practices** provides a series of targeted exercises to solidify your ability to construct paths, identify [topological obstructions](@entry_id:634492), and apply these concepts to concrete problems.

## Principles and Mechanisms

In our study of manifolds, understanding their topological structure is paramount. While the local structure is, by definition, Euclidean, the global structure can be extraordinarily complex. One of the most fundamental global properties is connectivity. This chapter moves beyond the introductory notion of a single, unbroken piece to a more rigorous and geometrically intuitive concept: **[path-connectedness](@entry_id:142695)**. We will explore its definition, establish methods for proving it, and examine its relationship with the more general topological notion of connectedness.

### The Definition of a Path and Path-Connectedness

The intuitive idea of connecting two points can be formalized mathematically through the concept of a path.

**Definition (Path):** Let $X$ be a topological space. A **path** in $X$ from a point $p \in X$ to a point $q \in X$ is a [continuous map](@entry_id:153772) $\gamma: [0, 1] \to X$ such that $\gamma(0) = p$ and $\gamma(1) = q$. The interval $[0, 1]$ represents the "time" parameter for traversing the path.

The requirement that $\gamma$ be continuous is crucial; it ensures the path has no "jumps" and corresponds to our intuitive understanding of continuous motion. With this definition, we can precisely define what it means for a set to be path-connected.

**Definition (Path-Connected Set):** A [topological space](@entry_id:149165) $X$ is **path-connected** if for any two points $p, q \in X$, there exists a path in $X$ from $p$ to $q$.

For example, any interval in $\mathbb{R}$ is path-connected. The entire Euclidean space $\mathbb{R}^n$ is path-connected. In contrast, the set $(-\infty, 0) \cup (0, \infty) \subset \mathbb{R}$ is not path-connected, as no continuous path can cross the "gap" at $0$ without leaving the set. This follows from the Intermediate Value Theorem. If a path $\gamma: [0, 1] \to \mathbb{R} \setminus \{0\}$ existed from a negative number to a positive number, there would have to be some $t \in (0,1)$ where $\gamma(t)=0$, a contradiction [@problem_id:1657930].

The nature of the paths allowed can drastically alter whether a set is considered connected. Consider a hypothetical constraint where paths are restricted to finite sequences of horizontal and vertical line segments (an "HV-path"). An open square in $\mathbb{R}^2$ is HV-path-connected, as is the union of the coordinate axes. However, a circle is not HV-path-connected, because no non-trivial straight line segment, horizontal or vertical, can be contained within it [@problem_id:2311301]. This illustrates that [path-connectedness](@entry_id:142695) depends intrinsically on the geometry of the set and the types of continuous deformations it permits.

### Methods for Establishing Path-Connectedness

Proving that a set is path-connected typically involves either constructing paths directly or using powerful theorems about continuous functions.

#### Direct Path Construction

The most fundamental method is to provide an explicit formula for a path between any two arbitrary points.

A simple yet powerful case involves **[convex sets](@entry_id:155617)**. A set $S \subseteq \mathbb{R}^n$ is convex if for any two points $p, q \in S$, the straight line segment connecting them is entirely contained in $S$. This segment can be parameterized as $\gamma(t) = (1-t)p + tq$ for $t \in [0, 1]$. This map is continuous, and by the definition of [convexity](@entry_id:138568), its image lies in $S$. Therefore, every convex set is path-connected.

This principle has profound implications in [differential geometry](@entry_id:145818). For any point $p$ on a manifold $M$, the [tangent space](@entry_id:141028) $T_pM$ is a real vector space. All finite-dimensional real [vector spaces](@entry_id:136837) are convex. Consequently, for any two tangent vectors $v, w \in T_pM$, the path $\gamma(t) = (1-t)v + tw$ is a [continuous path](@entry_id:156599) within $T_pM$ connecting them. This establishes that **every [tangent space](@entry_id:141028) $T_pM$ is inherently path-connected**, a fact that stems directly from its vector space structure, not from the properties of the manifold $M$ itself [@problem_id:1657979].

This idea can be extended to **star-shaped sets**. A set $S$ is star-shaped with respect to a point $p_0 \in S$ if for every $p \in S$, the line segment from $p_0$ to $p$ lies in $S$. Any two points $p_1, p_2$ in a [star-shaped set](@entry_id:154094) can be connected by concatenating the path from $p_1$ to $p_0$ with the path from $p_0$ to $p_2$. For instance, the set $S_A = \{ (x, y) \in \mathbb{R}^2 \mid x^4 + y^6 \le 1 \}$ is star-shaped with respect to the origin and is therefore path-connected [@problem_id:2311287].

In more complex sets, paths may need to be constructed by piecing together multiple segments. A useful example is the "[comb space](@entry_id:155329)," defined as $S_D = ([0,1] \times \{0\}) \cup (\{0\} \times [0,1]) \cup \bigcup_{n=1}^{\infty} (\{1/n\} \times [0,1])$. Any point in one of the vertical "teeth" of the comb can be connected to the horizontal "spine" by a vertical path. Since the spine itself is path-connected, any two points in the comb can be joined by a path consisting of at most three segments (down to the spine, across the spine, and up to the destination), demonstrating that the entire space is path-connected [@problem_id:2311292].

#### Invariance under Continuous Mappings

A more abstract and often more powerful method relies on the behavior of [path-connectedness](@entry_id:142695) under continuous functions.

**Theorem:** The continuous image of a path-connected set is path-connected.

*Proof:* Let $f: X \to Y$ be a continuous map, and let $X$ be path-connected. We want to show that the image, $f(X)$, is path-connected. Let $y_1, y_2$ be any two points in $f(X)$. By definition of the image, there exist points $x_1, x_2 \in X$ such that $f(x_1) = y_1$ and $f(x_2) = y_2$. Since $X$ is path-connected, there is a path $\gamma: [0, 1] \to X$ with $\gamma(0) = x_1$ and $\gamma(1) = x_2$. Now consider the composite map $\gamma' = f \circ \gamma$. Since $f$ and $\gamma$ are continuous, their composition $\gamma'$ is a continuous map from $[0, 1]$ to $Y$. Furthermore, $\gamma'(0) = f(\gamma(0)) = f(x_1) = y_1$ and $\gamma'(1) = f(\gamma(1)) = f(x_2) = y_2$. The image of this path lies entirely within $f(X)$. Thus, $\gamma'$ is a path in $f(X)$ connecting $y_1$ and $y_2$. Since $y_1$ and $y_2$ were arbitrary, $f(X)$ is path-connected. [@problem_id:2311287] [@problem_id:1657940]

This theorem is immensely useful. For example, the graph of a continuous function $g: \mathbb{R} \to \mathbb{R}$, such as $y = \sin(x)$, is path-connected because it is the image of the path-[connected domain](@entry_id:169490) $\mathbb{R}$ under the [continuous map](@entry_id:153772) $x \mapsto (x, \sin(x))$ [@problem_id:2311287]. Similarly, the 2-torus $T^2 = S^1 \times S^1$ is path-connected because it is the product of [path-connected spaces](@entry_id:152443) (and products of [path-connected spaces](@entry_id:152443) are path-connected) [@problem_id:1657940].

It is critical to note that the *preimage* of a path-connected set under a [continuous map](@entry_id:153772) is **not** necessarily path-connected. A canonical counterexample is the function $f: \mathbb{R}\setminus\{0\} \to \mathbb{R}$ defined by $f(x) = x^2$. The image set $V = (0, \infty)$ is an interval and thus path-connected. However, its preimage is $f^{-1}(V) = \{x \in \mathbb{R}\setminus\{0\} \mid x^2 > 0\} = \mathbb{R}\setminus\{0\}$, which consists of two disjoint intervals and is not path-connected [@problem_id:1657930]. This principle is relevant when studying Lie groups; the determinant map $\det: GL(n, \mathbb{R}) \to \mathbb{R} \setminus \{0\}$ is continuous. The codomain $\mathbb{R} \setminus \{0\}$ is not path-connected. This implies that the domain, the [general linear group](@entry_id:141275) $GL(n, \mathbb{R})$, cannot be path-connected either, as its continuous image under the determinant map would have to be path-connected if it were [@problem_id:1657940].

### Path-Components as Equivalence Classes

The concept of [path-connectedness](@entry_id:142695) naturally partitions a space into its maximal path-connected subsets. This is formalized by defining a relation on the points of a space.

Let $X$ be a topological space. For any two points $p, q \in X$, we write $p \sim q$ if and only if there exists a path in $X$ from $p$ to $q$. This relation $\sim$ is an **equivalence relation** [@problem_id:2311327]:

1.  **Reflexivity ($p \sim p$):** The constant path $\gamma(t) = p$ for all $t \in [0, 1]$ is continuous and connects $p$ to itself.
2.  **Symmetry ($p \sim q \implies q \sim p$):** If $\gamma: [0, 1] \to X$ is a path from $p$ to $q$, then the reversed path $\tilde{\gamma}(t) = \gamma(1-t)$ is a continuous path from $q$ to $p$.
3.  **Transitivity ($p \sim q$ and $q \sim r \implies p \sim r$):** If $\gamma_1$ is a path from $p$ to $q$ and $\gamma_2$ is a path from $q$ to $r$, we can concatenate them. The path $\gamma(t)$ defined as $\gamma_1(2t)$ for $t \in [0, 1/2]$ and $\gamma_2(2t-1)$ for $t \in [1/2, 1]$ is a continuous path from $p$ to $r$.

The [equivalence classes](@entry_id:156032) of this relation are called the **[path-components](@entry_id:145705)** of the space. Each path-component is, by construction, a path-connected subset, and it is maximal in the sense that any path-connected subset containing a point from that component is entirely contained within it. A space is path-connected if and only if it has exactly one path-component.

To find the path-[components of a space](@entry_id:265862), one often identifies subsets that cannot be connected by a path. For example, consider the 1-manifold $M$ in $\mathbb{R}^2$ defined by $(x^2 - y^2)^2 = 1$. This equation is equivalent to $x^2 - y^2 = 1$ or $x^2 - y^2 = -1$. These two sets are disjoint hyperbolas. A [continuous path](@entry_id:156599) cannot move between them. Furthermore, each hyperbola has two disjoint branches (e.g., for $x^2 - y^2 = 1$, the branches are $x > 0$ and $x  0$). No path can connect points on opposite branches without crossing the line $x=0$, which is not part of the set. Each of these four branches is itself path-connected (e.g., via hyperbolic trigonometric parameterizations). Therefore, the manifold $M$ has exactly four [path-components](@entry_id:145705) [@problem_id:1657942].

### The Relationship Between Path-Connectedness and Connectedness

Path-[connectedness](@entry_id:142066) is often confused with the more general topological concept of connectedness. While related, they are not identical.

**Definition (Connected Set):** A topological space $X$ is **connected** if it cannot be expressed as the union of two disjoint, non-empty, open subsets.

#### Path-Connectedness Implies Connectedness

Every [path-connected space](@entry_id:156428) is also connected. We can prove this by contradiction.

*Proof:* Assume $X$ is path-connected but not connected. Since $X$ is not connected, there exist two disjoint, non-empty, open sets $U$ and $V$ such that $X = U \cup V$. Because $U$ and $V$ are non-empty, we can choose a point $p \in U$ and a point $q \in V$. Since $X$ is path-connected, there exists a path $\gamma: [0, 1] \to X$ from $p$ to $q$. Now consider the preimages of $U$ and $V$ under $\gamma$, namely $\gamma^{-1}(U)$ and $\gamma^{-1}(V)$. Because $\gamma$ is continuous and $U,V$ are open in $X$, their preimages are open in $[0,1]$. They are non-empty since $0 \in \gamma^{-1}(U)$ and $1 \in \gamma^{-1}(V)$. They are disjoint since $U$ and $V$ are disjoint. Their union is $\gamma^{-1}(U) \cup \gamma^{-1}(V) = \gamma^{-1}(U \cup V) = \gamma^{-1}(X) = [0, 1]$. Thus, we have expressed the interval $[0, 1]$ as the union of two disjoint, non-empty, open sets. This contradicts the known fact that $[0, 1]$ is connected. Therefore, our initial assumption must be false, and $X$ must be connected. [@problem_id:1657970]

#### A Fundamental Counterexample: The Topologist's Sine Curve

The converse of the above theorem is false: a connected space is not necessarily path-connected. The standard example is the **[topologist's sine curve](@entry_id:142923)**. Consider the set $S \subset \mathbb{R}^2$ defined as the union of the graph $A = \{ (x, \sin(1/x)) \mid x \in (0, 1] \}$ and the vertical line segment $B = \{ (0, y) \mid y \in [-1, 1] \}$ [@problem_id:1657925].

This set $S$ is **connected**. The graph portion, $A$, is the continuous image of the connected interval $(0, 1]$ and is therefore connected. The full set $S$ is the closure of $A$, and a fundamental theorem of topology states that the closure of a connected set is connected.

However, $S$ is **not path-connected**. While any two points within $A$ can be connected, and any two points within $B$ can be connected, no path can connect a point in $A$ to a point in $B$. To see why, suppose a path $\gamma(t) = (x(t), y(t))$ starts at a point in $B$ (say, $(0,0)$) and ends at a point in $A$. Let $t_0 = \sup\{ t \mid x(t) = 0 \}$. By continuity, $x(t_0) = 0$, so $\gamma(t_0)$ is in $B$. For any $t > t_0$, we must have $x(t) > 0$, so $\gamma(t)$ is in $A$, which means $y(t) = \sin(1/x(t))$. As $t$ approaches $t_0$ from the right, $x(t)$ approaches $0$. The value of $\sin(1/x(t))$ oscillates infinitely rapidly between $-1$ and $1$. This means that $\lim_{t \to t_0^+} y(t)$ does not exist. This violates the continuity of the component function $y(t)$ at $t_0$. The contradiction implies that no such path can exist [@problem_id:1657925] [@problem_id:2311292].

This example also brilliantly illustrates another subtlety: the closure of a path-connected set need not be path-connected. The set $A = \{ (x, \cos(1/x)) \mid x \in (0, 1] \}$ is path-connected (being the continuous image of an interval). Its closure, $\bar{A}$, is precisely the [topologist's sine curve](@entry_id:142923) (with cosine), which we have argued is not path-connected [@problem_id:2311273]. This distinction between [connectedness](@entry_id:142066) and [path-connectedness](@entry_id:142695), and their behavior with respect to topological operations like [closures](@entry_id:747387), is a key theme in the study of topological spaces and manifolds.