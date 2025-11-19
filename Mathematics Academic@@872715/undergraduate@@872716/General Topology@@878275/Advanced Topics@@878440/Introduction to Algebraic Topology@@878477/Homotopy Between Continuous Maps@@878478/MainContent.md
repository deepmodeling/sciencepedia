## Introduction
In the field of topology, we are often less concerned with rigid geometric properties like distance and angle and more interested in the essential "shape" of an object. A central question is: when are two functions between [topological spaces](@entry_id:155056) fundamentally the same? Intuitively, we might say two maps are equivalent if one can be continuously deformed into the other without any tearing or cutting. The concept of **homotopy** provides the precise mathematical framework for this idea, serving as a powerful tool for classifying maps and, by extension, the spaces themselves. It addresses the knowledge gap between the intuitive notion of "[continuous deformation](@entry_id:151691)" and a formal, workable definition that can be used to prove theorems and build deeper theories.

This article will guide you through the theory and application of homotopy. In the first chapter, **Principles and Mechanisms**, we will establish the formal definition of homotopy, prove that it forms an equivalence relation, and explore crucial related concepts such as null-homotopy and relative homotopy. Next, in **Applications and Interdisciplinary Connections**, we will see how these principles are applied to classify spaces through homotopy equivalence, understand the properties of contractible spaces, and bridge the gap to algebraic topology by creating invariants like degree and the fundamental group. Finally, the **Hands-On Practices** section will offer opportunities to solidify your understanding by working through concrete problems that highlight the core properties of homotopy.

## Principles and Mechanisms

In topology, we are often concerned not just with the properties of spaces themselves, but with the [continuous maps](@entry_id:153855) between them. A central theme is the classification of maps into categories based on their essential geometric features, ignoring superficial differences. The concept of **homotopy** provides the [formal language](@entry_id:153638) for this classification, allowing us to define what it means for one continuous map to be "continuously deformed" into another.

### The Formal Definition of Homotopy

Let $X$ and $Y$ be [topological spaces](@entry_id:155056), and consider two [continuous maps](@entry_id:153855), $f: X \to Y$ and $g: X \to Y$. We say that **$f$ is homotopic to $g$**, denoted $f \simeq g$, if there exists a continuous map
$$
H: X \times [0, 1] \to Y
$$
such that for all $x \in X$,
$$
H(x, 0) = f(x) \quad \text{and} \quad H(x, 1) = g(x).
$$

The map $H$ is called a **homotopy** between $f$ and $g$. The second parameter of $H$, which we can denote by $t \in [0, 1]$, can be intuitively thought of as "time". At time $t=0$, the map is $f$. As $t$ increases, the map continuously transforms, and at time $t=1$, it becomes $g$. For each intermediate time $t \in (0, 1)$, we have a [continuous map](@entry_id:153772) $H_t: X \to Y$ defined by $H_t(x) = H(x, t)$. The continuity of $H$ ensures that this family of maps changes smoothly from $f$ to $g$.

A particularly simple yet powerful construction arises when the codomain $Y$ is a convex subset of a Euclidean space $\mathbb{R}^n$. In this case, for any two maps $f, g: X \to Y$, the **straight-line homotopy** is given by
$$
H(x, t) = (1-t)f(x) + tg(x).
$$
Since $Y$ is convex, for any $x \in X$, the entire line segment connecting $f(x)$ and $g(x)$ lies within $Y$. Thus, $H(x, t) \in Y$ for all $t \in [0, 1]$. This map is continuous because $f$, $g$, and scalar multiplication are continuous. At $t=0$, we have $H(x, 0) = f(x)$, and at $t=1$, we have $H(x, 1) = g(x)$. Therefore, any two [continuous maps](@entry_id:153855) into a convex space are homotopic.

### Homotopy as an Equivalence Relation

The homotopy relation $\simeq$ on the set of all [continuous maps](@entry_id:153855) from $X$ to $Y$, denoted $C(X, Y)$, is an **equivalence relation**. To establish this, we must verify that it is reflexive, symmetric, and transitive.

*   **Reflexivity ($f \simeq f$):** For any continuous map $f: X \to Y$, we can define the "stationary" homotopy $H(x, t) = f(x)$ for all $t \in [0, 1]$. This map is continuous and satisfies $H(x, 0) = f(x)$ and $H(x, 1) = f(x)$. Thus, every map is homotopic to itself.

*   **Symmetry ($f \simeq g \implies g \simeq f$):** Suppose $f \simeq g$ via a homotopy $H: X \times [0, 1] \to Y$. We can construct a homotopy from $g$ to $f$ by "running the deformation backwards". Let $H'(x, t) = H(x, 1-t)$. Since $H$ and the map $t \mapsto 1-t$ are continuous, $H'$ is continuous. Furthermore, $H'(x, 0) = H(x, 1) = g(x)$ and $H'(x, 1) = H(x, 0) = f(x)$. Thus, $g \simeq f$.

*   **Transitivity ($f \simeq g$ and $g \simeq h \implies f \simeq h$):** Suppose $f \simeq g$ via a homotopy $F: X \times [0, 1] \to Y$, and $g \simeq h$ via a homotopy $G: X \times [0, 1] \to Y$. We can construct a homotopy from $f$ to $h$ by performing the first homotopy on the time interval $[0, 1/2]$ and the second on $[1/2, 1]$. This requires re-scaling the time parameter for each part. The resulting concatenated homotopy $K: X \times [0, 1] \to Y$ is defined piecewise:
    $$
    K(x,t) = \begin{cases} F(x, 2t)  &\text{if } 0 \le t \le \frac{1}{2} \\ G(x, 2t-1) &\text{if } \frac{1}{2} \le t \le 1 \end{cases}
    $$
    At $t=0$, $K(x, 0) = F(x, 0) = f(x)$. At $t=1$, $K(x, 1) = G(x, 1) = h(x)$. At the crucial midpoint $t=1/2$, the first piece gives $F(x, 1) = g(x)$ and the second gives $G(x, 0) = g(x)$. Since the definitions agree on the overlap, the pasting lemma ensures that $K$ is continuous. Thus, $f \simeq h$. For example, given maps $f(x) = x^3+1$, $g(x) = 2x+1$, and $h(x) = \sin(\frac{\pi}{2}x) + 2x$ from $\mathbb{R}$ to $\mathbb{R}$, and straight-line homotopies $F(x,t) = (1-t)f(x)+tg(x)$ and $G(x,t) = (1-t)g(x)+th(x)$, this construction yields the explicit homotopy from $f$ to $h$ [@problem_id:1557532].

Since $\simeq$ is an equivalence relation, it partitions the set $C(X, Y)$ into disjoint **homotopy classes**. The set of these equivalence classes is denoted by $[X, Y]$. This set is a central object of study in algebraic topology, as its structure often reveals deep information about the spaces $X$ and $Y$.

### Fundamental Concepts and Specialized Homotopies

The general definition of homotopy gives rise to several crucial concepts that classify not only maps but also spaces themselves.

A map $f: X \to Y$ is said to be **[null-homotopic](@entry_id:153762)** if it is homotopic to a constant map $c_p: X \to Y$, where $c_p(x) = p$ for some fixed point $p \in Y$. This means that the image of $X$ under $f$ can be continuously shrunk to a single point in $Y$.

A space $X$ is called **contractible** if its identity map, $\text{id}_X: X \to X$, is [null-homotopic](@entry_id:153762). This is equivalent to saying that the entire space $X$ can be continuously deformed within itself to a single point. For instance, any convex subset of $\mathbb{R}^n$ is contractible. The unit disk $D^2 \subset \mathbb{R}^2$ is a canonical example. A homotopy demonstrating its contractibility to the origin $p=(0,0)$ is given by $H(v, t) = (1-t)v$ for $v \in D^2$ and $t \in [0,1]$ [@problem_id:1557542]. Here, $H(v,0) = v = \text{id}_{D^2}(v)$, and $H(v,1) = 0 = c_p(v)$. Each point $v$ moves along a straight line towards the origin, completing the contraction at $t=1$.

In many situations, we require a deformation to leave a certain part of the domain fixed. This leads to the notion of a **relative homotopy**. Let $A$ be a subspace of $X$, and let $f, g: X \to Y$ be two maps that agree on $A$ (i.e., $f(a) = g(a)$ for all $a \in A$). A **homotopy relative to $A$** between $f$ and $g$ is a homotopy $H: X \times [0, 1] \to Y$ that additionally satisfies the condition $H(a, t) = f(a)$ for all $a \in A$ and $t \in [0, 1]$. This means the deformation does not move the points in the image of the subspace $A$. For example, consider the maps $f(\mathbf{x}) = \mathbf{x}$ and $g(\mathbf{x}) = \|\mathbf{x}\|\mathbf{x}$ from the unit disk $D^2$ to itself. On the boundary circle $S^1$, where $\|\mathbf{x}\|=1$, both maps agree: $f(\mathbf{x}) = g(\mathbf{x}) = \mathbf{x}$. The function $H(\mathbf{x}, t) = (1-t+t\|\mathbf{x}\|)\mathbf{x}$ provides a homotopy between them that keeps the boundary $S^1$ fixed, thus qualifying as a homotopy relative to $S^1$ [@problem_id:1557531].

### An Alternative Viewpoint: Paths in Function Spaces

The definition of homotopy has a powerful and intuitive reinterpretation in the language of function spaces. The set of [continuous maps](@entry_id:153855) $C(X, Y)$ can itself be endowed with a topology, making it a [topological space](@entry_id:149165). The most common and useful such topology is the **[compact-open topology](@entry_id:153876)**, which is generated by [subbasis](@entry_id:151637) sets of the form $S(K, U) = \{f \in C(X, Y) \mid f(K) \subseteq U\}$, where $K \subset X$ is compact and $U \subset Y$ is open.

Within this framework, a path in the space $C(X, Y)$ is a continuous map $\gamma: [0, 1] \to C(X, Y)$. If $\gamma(0) = f$ and $\gamma(1) = g$, then $\gamma$ is a path from $f$ to $g$.

A fundamental theorem, sometimes called the exponential law, establishes a direct correspondence between homotopies and paths in function spaces. For a locally compact Hausdorff space $X$, there is a natural bijection between [continuous maps](@entry_id:153855) from the [product space](@entry_id:151533) $X \times [0,1]$ to $Y$ and [continuous maps](@entry_id:153855) from the interval $[0,1]$ to the [function space](@entry_id:136890) $C(X,Y)$. A homotopy $H: X \times [0, 1] \to Y$ is associated with its **[adjoint map](@entry_id:191705)** $\hat{H}: [0, 1] \to C(X, Y)$, defined by $(\hat{H}(t))(x) = H(x, t)$. The theorem states that $H$ is continuous if and only if $\hat{H}$ is continuous.

Let's examine the meaning of $\hat{H}$. It is a map that assigns to each time $t \in [0, 1]$ the corresponding map $H_t \in C(X, Y)$. The condition $H(x, 0) = f(x)$ translates to $\hat{H}(0) = f$, and $H(x, 1) = g(x)$ translates to $\hat{H}(1) = g$. Therefore, a homotopy between $f$ and $g$ is precisely equivalent to a path from $f$ to $g$ in the [function space](@entry_id:136890) $C(X, Y)$ equipped with the [compact-open topology](@entry_id:153876) [@problem_id:1557494]. This perspective provides a powerful geometric intuition: two functions are homotopic if one can "walk" from one to the other along a continuous path within the space of all continuous functions.

### Homotopy and Composition

Homotopy behaves compatibly with the composition of maps, a property that is essential for its use in algebraic settings. Specifically, if we have two pairs of homotopic maps, their compositions are also homotopic.

**Theorem:** Let $f_0, f_1: X \to Y$ and $g_0, g_1: Y \to Z$ be [continuous maps](@entry_id:153855). If $f_0 \simeq f_1$ and $g_0 \simeq g_1$, then the composite maps are homotopic: $g_0 \circ f_0 \simeq g_1 \circ f_1$.

A proof of this can be constructed by breaking down the total deformation into stages. Let $F$ be the homotopy from $f_0$ to $f_1$ and $G$ be the homotopy from $g_0$ to $g_1$. The goal is to deform $g_0(f_0(x))$ into $g_1(f_1(x))$. One way to achieve this is to first deform the "outer" map from $g_0$ to $g_1$ while keeping the "inner" map fixed at $f_0$, and then deform the "inner" map from $f_0$ to $f_1$ while keeping the "outer" map fixed at $g_1$. By concatenating these two steps, we can build the required homotopy $H: X \times [0,1] \to Z$ [@problem_id:1557508].

The concept of homotopy is also central to the study of the fundamental group, $\pi_1(X, x_0)$. An important result describes how the homomorphism induced by a map changes if the map is homotoped in a way that moves the basepoint. If $f, g: (X, x_0) \to (Y, y_0)$ are two maps and $H$ is a homotopy between them, the path traced by the basepoint is given by $\gamma(t) = H(x_0, t)$. This path $\gamma$ is a loop in $Y$ based at $y_0$. The relationship between the [induced homomorphisms](@entry_id:266478) $f_*$ and $g_*$ on the fundamental groups is then given by conjugation: for any loop class $[\alpha] \in \pi_1(X, x_0)$,
$$
g_*([\alpha]) = [\gamma] \cdot f_*([\alpha]) \cdot [\gamma]^{-1}
$$
where $[\gamma]$ is the homotopy class of the loop $\gamma$ in $\pi_1(Y, y_0)$. This formula is a crucial tool for understanding how algebraic invariants behave under deformations of maps [@problem_id:1581645].

### Properties and Applications

The classification of maps into homotopy classes has profound consequences and applications throughout topology.

One of the most important applications is in the theory of **map extensions**. A classic question asks: given a map $f: A \to Y$ defined on a subspace $A \subseteq X$, can it be extended to a [continuous map](@entry_id:153772) $F: X \to Y$ such that $F|_A = f$? Homotopy provides a powerful criterion for the case where $X$ is a disk and $A$ is its boundary sphere.

**Theorem:** A continuous map $f: S^{n-1} \to Y$ can be extended to a continuous map $F: D^n \to Y$ if and only if $f$ is [null-homotopic](@entry_id:153762).

Intuitively, if $f$ can be extended to the disk $D^n$, the image of the boundary $S^{n-1}$ under $f$ can be "filled in" by the image of the disk. This "filling" provides the blueprint for a homotopy that shrinks the image of $f$ to a point (the image of the disk's center). Conversely, a null-homotopy for $f$ can be used to construct the extension over the disk. We can apply this theorem to maps from the circle $S^1$ into the [punctured plane](@entry_id:150262) $Y = \mathbb{R}^2 \setminus \{(0,0)\}$. A map $f: S^1 \to Y$ is [null-homotopic](@entry_id:153762) in $Y$ if and only if its winding number around the origin is zero. Therefore, a map from the circle to the punctured plane can be extended to the disk if and only if its [winding number](@entry_id:138707) is zero [@problem_id:1557515].

A [topological property](@entry_id:141605) is called a **homotopy invariant** if, whenever two spaces $X$ and $Y$ have the same homotopy type (meaning there exist maps $f: X \to Y$ and $g: Y \to X$ such that $g \circ f \simeq id_X$ and $f \circ g \simeq id_Y$), $X$ has the property if and only if $Y$ does. For instance, [path-connectedness](@entry_id:142695) is a homotopy invariant.

It is equally important to understand which properties are *not* preserved by homotopy. For example, the property of a map having a dense image is not invariant under homotopy. To see this, consider maps from the contractible space $X=(0, \infty)$ to the circle $Y=S^1$. Since $X$ is contractible, any two maps from $X$ to the [path-connected space](@entry_id:156428) $S^1$ are homotopic. Consider the map $f(t) = (\cos(2\pi/t), \sin(2\pi/t))$, whose image wraps infinitely often around the circle as $t \to 0^+$, making its image dense in $S^1$. Now consider the constant map $g(t) = (1, 0)$, whose image is a single point and thus not dense. Since $f \simeq g$, we have found a pair of homotopic maps where one has a dense image and the other does not. This demonstrates that having a dense image is not a homotopy invariant property of a map [@problem_id:1557499].

Finally, the concept of homotopy interacts well with analytic notions like uniform convergence. The set of maps belonging to a single homotopy class is a closed set with respect to the topology of [uniform convergence](@entry_id:146084).

**Theorem:** Let $X$ be a [compact space](@entry_id:149800) and $(Y, d)$ a metric space. If a sequence of [continuous maps](@entry_id:153855) $f_n: X \to Y$ converges uniformly to a map $f: X \to Y$, and if all $f_n$ belong to the same homotopy class (i.e., $f_n \simeq g$ for a fixed map $g$), then $f$ is also homotopic to $g$.

The proof relies on the fact that for a sufficiently large integer $N$, uniform convergence implies $f$ is "close" to $f_N$. This closeness allows the construction of a (straight-line) homotopy $K$ between $f$ and $f_N$. Since we are given that $f_N \simeq g$ via some homotopy $H_N$, we can concatenate $K$ and $H_N$ to form a homotopy from $f$ to $g$, proving that $f \simeq g$ [@problem_id:1557504]. This result is fundamental, showing that homotopy classes are robust under the process of taking uniform limits.