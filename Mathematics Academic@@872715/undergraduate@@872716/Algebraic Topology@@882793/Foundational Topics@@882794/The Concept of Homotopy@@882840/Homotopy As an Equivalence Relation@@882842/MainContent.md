## Introduction
In the field of topology, understanding the properties of spaces often involves studying the [continuous maps](@entry_id:153855) between them. However, focusing on individual maps can be too rigid. The more profound insights arise when we can group maps that are "essentially the same." The concept of **homotopy** provides the mathematical framework for this idea, formalizing the intuitive notion of continuously deforming one map into another without tearing or breaking it. This allows us to classify not just maps, but the [topological spaces](@entry_id:155056) themselves in a more flexible and powerful way.

This article addresses the foundational principle that makes homotopy such an effective classification tool: the fact that it forms an equivalence relation. By establishing this property, we can partition the infinite set of all [continuous maps](@entry_id:153855) between two spaces into a finite or countably infinite set of distinct [equivalence classes](@entry_id:156032), paving the way for the creation of algebraic invariants.

Across the following chapters, you will gain a comprehensive understanding of this cornerstone of algebraic topology.
-   **Chapter 1: Principles and Mechanisms** will introduce the formal definition of homotopy, prove that it satisfies the properties of an [equivalence relation](@entry_id:144135) (reflexivity, symmetry, and [transitivity](@entry_id:141148)), and explore important variations like relative and [path-homotopy](@entry_id:153567).
-   **Chapter 2: Applications and Interdisciplinary Connections** will demonstrate how the [equivalence classes](@entry_id:156032) of homotopy are used to classify maps, define homotopy invariants like the [winding number](@entry_id:138707), and construct [algebraic structures](@entry_id:139459) such as the fundamental group.
-   **Chapter 3: Hands-On Practices** will provide you with the opportunity to apply these concepts to concrete problems, solidifying your grasp of how homotopies are constructed and manipulated.

## Principles and Mechanisms

In the study of topology, we are often interested not in the properties of a single [continuous map](@entry_id:153772), but in the relationships between different maps. The concept of **homotopy** provides a rigorous framework for understanding when one map can be "continuously deformed" into another. This notion of [continuous deformation](@entry_id:151691) is one of the central organizing principles of algebraic topology, allowing us to classify maps and, by extension, the spaces themselves.

### The Formal Definition of Homotopy

Let $X$ and $Y$ be topological spaces. A **homotopy** between two [continuous maps](@entry_id:153855) $f: X \to Y$ and $g: X \to Y$ is a [continuous map](@entry_id:153772) $H: X \times I \to Y$, where $I$ is the unit interval $[0, 1]$, that satisfies two conditions:
1.  For all $x \in X$, $H(x, 0) = f(x)$.
2.  For all $x \in X$, $H(x, 1) = g(x)$.

If such a map $H$ exists, we say that $f$ is **homotopic** to $g$, and we write $f \simeq g$. The map $H$ can be thought of as a family of maps $H_t: X \to Y$ for $t \in I$, defined by $H_t(x) = H(x, t)$. Here, the parameter $t$ can be interpreted as "time," with the deformation starting at the map $f = H_0$ and ending at the map $g = H_1$.

The most crucial and subtle aspect of this definition is the requirement that $H$ be continuous on the [product space](@entry_id:151533) $X \times I$ with its standard product topology [@problem_id:1557305]. It is not sufficient for the map to be continuous in each variable separately—that is, for each fixed $t_0 \in I$, the map $x \mapsto H(x, t_0)$ is continuous, and for each fixed $x_0 \in X$, the path $t \mapsto H(x_0, t)$ is continuous. Joint continuity is a stronger condition and is essential for the theory to have its full power.

### An Alternative Viewpoint: Paths in Function Spaces

A powerful way to conceptualize homotopy is to consider the set of all [continuous maps](@entry_id:153855) from $X$ to $Y$, denoted $C(X, Y)$ or $Y^X$. This set can be given a topology, most commonly the **[compact-open topology](@entry_id:153876)**, turning it into a [topological space](@entry_id:149165) in its own right, known as a **function space**.

From this perspective, a single continuous map $f: X \to Y$ is just a single point in the space $C(X, Y)$. A homotopy $H: X \times I \to Y$ between two maps $f$ and $g$ can then be reinterpreted. For each time $t \in I$, we have a map $H_t \in C(X, Y)$. The continuity of the full map $H$ ensures that the assignment $t \mapsto H_t$ defines a [continuous path](@entry_id:156599) $\gamma: I \to C(X, Y)$ that starts at $\gamma(0) = f$ and ends at $\gamma(1) = g$ [@problem_id:1557303].

This correspondence is a [bijection](@entry_id:138092) under suitable conditions on the spaces (specifically, when $X$ is locally compact Hausdorff). Therefore, two maps $f$ and $g$ are homotopic if and only if they belong to the same **path-component** of the [function space](@entry_id:136890) $C(X, Y)$. The set of homotopy classes of maps from $X$ to $Y$, denoted $[X, Y]$, is precisely the set of [path-components](@entry_id:145705) of $C(X, Y)$.

This viewpoint can have profound consequences. For instance, consider maps into a **convex subset** $Y$ of a Euclidean space, such as $Y = \mathbb{R}^n$. For any two maps $f, g: X \to Y$, the function space $C(X, Y)$ is also convex. The "straight-line" path between the points $f$ and $g$ in this space, given by $\gamma(t) = (1-t)f + tg$, is a continuous path. This corresponds to the **straight-line homotopy** $H(x, t) = (1-t)f(x) + tg(x)$, which is continuous. This implies that the function space $C(X, Y)$ is path-connected, meaning there is only one homotopy class of maps from $X$ to $Y$ [@problem_id:1655949]. Any two such maps are homotopic. A map homotopic to a constant map is called **[null-homotopic](@entry_id:153762)**. Therefore, for a convex [target space](@entry_id:143180) $Y$, all maps are [null-homotopic](@entry_id:153762).

### Homotopy as an Equivalence Relation

The true utility of homotopy as a classification tool comes from the fact that it forms an [equivalence relation](@entry_id:144135) on the set of [continuous maps](@entry_id:153855) $C(X, Y)$. This means the homotopy relation partitions $C(X, Y)$ into disjoint [equivalence classes](@entry_id:156032). We now verify the three required properties.

**Reflexivity:** Any map $f$ is homotopic to itself ($f \simeq f$).
To prove this, we must construct a homotopy from $f$ to $f$. The most natural choice is the **stationary homotopy**, where the map does not change over time. We define $H: X \times I \to Y$ by $H(x, t) = f(x)$ for all $(x, t) \in X \times I$. This map satisfies the boundary conditions, since $H(x, 0) = f(x)$ and $H(x, 1) = f(x)$. Its continuity follows from the fact that $H$ is the composition of the continuous projection map $p_X: X \times I \to X$ and the [continuous map](@entry_id:153772) $f: X \to Y$ [@problem_id:1655981].

**Symmetry:** If $f \simeq g$, then $g \simeq f$.
Suppose $f \simeq g$ via a homotopy $H: X \times I \to Y$. To show that $g \simeq f$, we need a homotopy that deforms $g$ back into $f$. We can achieve this by simply "running the clock backwards" on the original homotopy. We define a new map $\bar{H}: X \times I \to Y$ by $\bar{H}(x, t) = H(x, 1-t)$.
This map is continuous because it is the composition of $H$ and the continuous map $(x, t) \mapsto (x, 1-t)$. Let's check the boundary conditions:
- At $t=0$: $\bar{H}(x, 0) = H(x, 1) = g(x)$.
- At $t=1$: $\bar{H}(x, 1) = H(x, 0) = f(x)$.
Thus, $\bar{H}$ is a valid homotopy from $g$ to $f$, establishing symmetry [@problem_id:1655993].

**Transitivity:** If $f \simeq g$ and $g \simeq h$, then $f \simeq h$.
Let $F$ be a homotopy from $f$ to $g$, and let $G$ be a homotopy from $g$ to $h$. We need to construct a single homotopy $K$ from $f$ to $h$. The idea is to concatenate the two deformations: first, perform the deformation from $f$ to $g$ in the time interval $[0, 1/2]$, and then perform the deformation from $g$ to $h$ in the time interval $[1/2, 1]$. To do this, we must re-scale the time parameter for each homotopy.
We define $K: X \times I \to Y$ piecewise [@problem_id:1655983]:
$$
K(x, t) = \begin{cases}
F(x, 2t)  & \text{if } 0 \le t \le \frac{1}{2} \\
G(x, 2t - 1)  & \text{if } \frac{1}{2} \le t \le 1
\end{cases}
$$
The boundary conditions are met: $K(x, 0) = F(x, 0) = f(x)$ and $K(x, 1) = G(x, 1) = h(x)$. The function is continuous on $X \times [0, 1/2]$ and $X \times [1/2, 1]$ separately. At the junction where $t=1/2$, the two definitions agree, since $F(x, 2(1/2)) = F(x, 1) = g(x)$ and $G(x, 2(1/2) - 1) = G(x, 0) = g(x)$. By the **Pasting Lemma**, since the definitions agree on the closed overlapping set $X \times \{1/2\}$, the combined function $K$ is continuous on all of $X \times I$.

An immediate and important consequence of these properties is that if two maps $f$ and $g$ are both [null-homotopic](@entry_id:153762) to the same constant map $c_{y_0}$, then they are homotopic to each other. We are given $f \simeq c_{y_0}$ and $g \simeq c_{y_0}$. By symmetry, $c_{y_0} \simeq g$. By transitivity, $f \simeq c_{y_0}$ and $c_{y_0} \simeq g$ implies $f \simeq g$. The explicit homotopy is constructed by concatenating the homotopy from $f$ to $c_{y_0}$ with the *reverse* of the homotopy from $g$ to $c_{y_0}$ [@problem_id:1557269].

It is insightful to note that these proofs for the [equivalence relation](@entry_id:144135) properties rely only on constructions (stationary map, [time reversal](@entry_id:159918), [concatenation](@entry_id:137354)) that preserve continuity in each variable separately. This means that even if we were to weaken the definition of homotopy to only require separate continuity instead of joint continuity, the resulting relation would still be an equivalence relation [@problem_id:1557281]. This highlights the robustness of the algebraic structure that homotopy imposes.

### Constrained Deformations: Relative and Path Homotopy

In many applications, we need a more restrictive notion of homotopy where the deformation is not allowed to alter the map on a certain part of its domain. This leads to the idea of **relative homotopy**.

Let $A$ be a subspace of $X$. Two maps $f, g: X \to Y$ that agree on $A$ (i.e., $f(a) = g(a)$ for all $a \in A$) are said to be **homotopic relative to $A$**, written $f \simeq_A g$, if there exists a homotopy $H$ from $f$ to $g$ that also satisfies the additional constraint:
$$H(a, t) = f(a) \quad \text{for all } a \in A \text{ and all } t \in I.$$
This means that for any point in the subspace $A$, its image remains fixed throughout the entire deformation.

The most important example of this concept is **[path-homotopy](@entry_id:153567)**. A path in a space $X$ is a [continuous map](@entry_id:153772) $\gamma: I \to X$. A **[path-homotopy](@entry_id:153567)** is a homotopy between two paths $\gamma_0$ and $\gamma_1$ that is relative to the subspace of endpoints $A = \{0, 1\} \subset I$. This requires that the two paths share the same starting point and the same ending point, and that these endpoints remain fixed during the homotopy. Specifically, if $\gamma_0(0) = \gamma_1(0) = x_0$ and $\gamma_0(1) = \gamma_1(1) = x_1$, a [path-homotopy](@entry_id:153567) $H: I \times I \to X$ must satisfy $H(s, 0) = \gamma_0(s)$, $H(s, 1) = \gamma_1(s)$, and also $H(0, t) = x_0$ and $H(1, t) = x_1$ for all $s, t \in I$.

It is crucial to distinguish between a general homotopy and a [path-homotopy](@entry_id:153567), as the latter is a much stronger condition. For example, consider two parallel paths in the plane, $f(t) = (t, -1)$ and $g(t) = (t, 1)$ for $t \in [0, 1]$. These paths are homotopic via the straight-line homotopy $H(t, s) = (t, -1+2s)$. However, they are not path-homotopic because they do not even share the same endpoints: $f(0) = (0, -1)$ while $g(0) = (0, 1)$ [@problem_id:1655972].

This distinction becomes paramount when studying **loops**, which are paths that start and end at the same point, $\gamma(0) = \gamma(1) = x_0$. For two loops $f$ and $g$ based at $x_0$, a [path-homotopy](@entry_id:153567) (often called a **based homotopy**) requires the basepoint to remain fixed at $x_0$ throughout the deformation. A general homotopy (often called a **free homotopy**) allows the intermediate paths $H_t$ to be non-loops whose endpoints can wander.

Consider the figure-eight space, $X = S^1 \vee S^1$, with basepoint $x_0$ at the junction. Let $a$ be a loop traversing the first circle and $b$ be a loop traversing the second. The loop $f=a$ is not path-homotopic to the loop $g = b \cdot a \cdot b^{-1}$ (which represents conjugating $a$ by $b$). No based homotopy can untangle the $b$ and $b^{-1}$ from around $a$. However, $f$ and $g$ *are* freely homotopic; one can imagine "sliding" the basepoint of loop $a$ around the loop $b$, which transforms it into $g$ [@problem_id:1557291]. This distinction is the foundation of the fundamental group $\pi_1(X, x_0)$, whose elements are [path-homotopy](@entry_id:153567) classes of loops, and where free homotopy classes correspond to conjugacy classes within the group.

### Homotopy Equivalence of Spaces

Finally, we can elevate the concept of homotopy from an equivalence relation on maps to an [equivalence relation](@entry_id:144135) on the class of all topological spaces. This captures the idea of two spaces being "topologically the same" from the perspective of homotopy.

Two spaces $X$ and $Y$ are said to have the same **homotopy type**, or are **homotopy equivalent**, written $X \simeq Y$, if there exist [continuous maps](@entry_id:153855) $f: X \to Y$ and $g: Y \to X$ such that:
- $g \circ f$ is homotopic to the identity map on $X$ ($g \circ f \simeq \text{id}_X$).
- $f \circ g$ is homotopic to the identity map on $Y$ ($f \circ g \simeq \text{id}_Y$).

The maps $f$ and $g$ are called **homotopy equivalences**. This relation is indeed an equivalence relation on the class of topological spaces.
- **Reflexivity ($X \simeq X$):** Obvious by choosing $f = g = \text{id}_X$.
- **Symmetry (If $X \simeq Y$, then $Y \simeq X$):** Follows directly from the symmetric nature of the definition.
- **Transitivity (If $X \simeq Y$ and $Y \simeq Z$, then $X \simeq Z$):** If $f_1:X \to Y, g_1:Y \to X$ and $f_2:Y \to Z, g_2:Z \to Y$ are the respective homotopy equivalences, we must construct maps between $X$ and $Z$. The correct choices are the compositions $F = f_2 \circ f_1: X \to Z$ and $G = g_1 \circ g_2: Z \to X$. One can then verify that $G \circ F \simeq \text{id}_X$ and $F \circ G \simeq \text{id}_Z$, using the properties of the intermediate homotopies [@problem_id:1655926]. For instance,
$$G \circ F = (g_1 \circ g_2) \circ (f_2 \circ f_1) = g_1 \circ (g_2 \circ f_2) \circ f_1 \simeq g_1 \circ \text{id}_Y \circ f_1 = g_1 \circ f_1 \simeq \text{id}_X.$$
Homotopy equivalence is a weaker relation than [homeomorphism](@entry_id:146933) (a homeomorphism is always a homotopy equivalence, but not vice versa), and it forms the fundamental notion of "sameness" in algebraic topology.