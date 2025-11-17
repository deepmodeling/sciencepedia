## Introduction
In the pursuit of classifying topological spaces, mathematicians seek to understand their essential shape, ignoring trivial deformations. The standard notion of homotopy, while powerful, can be too flexible to capture fine details. To build more sophisticated algebraic tools for this classification, a simple but profound enhancement is needed: anchoring our deformations to a fixed point. This is the central idea behind [pointed spaces](@entry_id:273706) and based homotopy. This article provides a comprehensive exploration of this foundational concept in algebraic topology. The first chapter, "Principles and Mechanisms," will formally define [pointed spaces](@entry_id:273706), based maps, and based homotopy, establishing the core properties that make this framework so effective. The second chapter, "Applications and Interdisciplinary Connections," will demonstrate how these principles are used to construct the fundamental group and [higher homotopy groups](@entry_id:159688), and reveal the deep connections this theory forges with algebra and [category theory](@entry_id:137315). Finally, the "Hands-On Practices" section will offer concrete exercises to solidify your understanding of these abstract concepts.

## Principles and Mechanisms

In our exploration of topological spaces, a central goal is to classify them up to [continuous deformation](@entry_id:151691). However, the notion of deformation, or **homotopy**, can sometimes be too flexible. To build more refined algebraic invariants, such as the fundamental group, we introduce a simple yet powerful structural enhancement: the designation of a **basepoint**. By requiring that all maps and deformations preserve this point, we gain the ability to compose paths and construct group structures, paving the way for the powerful tools of algebraic topology.

### The Pointed Category: Spaces, Maps, and Homotopies

A **[pointed space](@entry_id:265918)**, or **based space**, is a pair $(X, x_0)$ consisting of a [topological space](@entry_id:149165) $X$ and a chosen point $x_0 \in X$, referred to as the **basepoint**. This basepoint acts as an anchor, a reference point that must be respected by the maps and homotopies we consider.

A continuous map $f: X \to Y$ between two [pointed spaces](@entry_id:273706), $(X, x_0)$ and $(Y, y_0)$, is called a **based map** if it preserves the basepoints, meaning $f(x_0) = y_0$. This simple requirement ensures that the structure we have added is maintained.

The concept of continuous deformation is similarly refined. A **based homotopy** between two based maps $f_0, f_1: (X, x_0) \to (Y, y_0)$ is a [continuous map](@entry_id:153772) $H: X \times [0, 1] \to Y$ satisfying three conditions:
1.  $H(x, 0) = f_0(x)$ for all $x \in X$ (the homotopy starts at $f_0$).
2.  $H(x, 1) = f_1(x)$ for all $x \in X$ (the homotopy ends at $f_1$).
3.  $H(x_0, t) = y_0$ for all $t \in [0, 1]$ (the basepoint is fixed throughout the deformation).

If such a based homotopy exists, we say that $f_0$ and $f_1$ are **based homotopic**, denoted $f_0 \simeq_* f_1$.

It is a fundamental fact that based homotopy defines an [equivalence relation](@entry_id:144135) on the set of all based maps from $(X, x_0)$ to $(Y, y_0)$. Reflexivity is given by the stationary homotopy $H(x, t) = f(x)$, and symmetry is achieved by reversing the time parameter, $H'(x, t) = H(x, 1-t)$. Transitivity is the most instructive property: if $f_0 \simeq_* f_1$ via a homotopy $H_1$ and $f_1 \simeq_* f_2$ via a homotopy $H_2$, we can "stack" these homotopies to form a homotopy from $f_0$ to $f_2$. This is done by traversing $H_1$ at double speed for the first half of the time interval and $H_2$ at double speed for the second half. The new homotopy $H: X \times [0,1] \to Y$ is formally defined as:
$$
H(x, t) = \begin{cases}
H_1(x, 2t)  & \text{if } 0 \le t \le 1/2 \\
H_2(x, 2t-1)  & \text{if } 1/2 \le t \le 1
\end{cases}
$$
The continuity of this concatenated homotopy is guaranteed by the pasting lemma, as the definitions agree at $t=1/2$, where $H_1(x, 1) = f_1(x)$ and $H_2(x, 0) = f_1(x)$. Critically, the basepoint condition holds for all $t$ because it holds for both $H_1$ and $H_2$.

This [equivalence relation](@entry_id:144135) partitions the set of based maps into **based homotopy classes**. The set of these classes is denoted $[(X, x_0), (Y, y_0)]_*$. The study of these sets is a primary occupation of homotopy theory.

### Based Contractibility and Its Consequences

Some spaces have a particularly simple structure from the perspective of based homotopy. A [pointed space](@entry_id:265918) $(X, x_0)$ is called **based contractible** if the identity map $\text{id}_X: (X, x_0) \to (X, x_0)$ is based homotopic to the constant map $c_{x_0}: (X, x_0) \to (X, x_0)$, where $c_{x_0}(x) = x_0$ for all $x \in X$. This means the entire space can be continuously shrunk to its basepoint while keeping the basepoint itself fixed.

A classic example of a based contractible space is any **star-shaped** subset $S \subseteq \mathbb{R}^n$ with its center $p_0$ as the basepoint. A set $S$ is star-shaped with respect to $p_0$ if for every point $x \in S$, the line segment connecting $p_0$ and $x$ is entirely contained in $S$. The based contraction is given by the intuitive **straight-line homotopy**:
$$
H(x, t) = (1-t)x + t p_0
$$
At $t=0$, we have $H(x, 0) = x$, the identity map. At $t=1$, we have $H(x, 1) = p_0$, the constant map. For the basepoint, $H(p_0, t) = (1-t)p_0 + t p_0 = p_0$ for all $t \in [0,1]$. The star-shaped property ensures that for any $x \in S$ and $t \in [0,1]$, the point $H(x,t)$ remains in $S$, so the homotopy is well-defined.

The property of being based contractible has a profound impact on maps *into* such a space. If the [target space](@entry_id:143180) $(X, x_0)$ is based contractible, then the set of based homotopy classes $[(A, a_0), (X, x_0)]_*$ contains exactly one element, regardless of the [pointed space](@entry_id:265918) $(A, a_0)$. To see this, let $f: (A, a_0) \to (X, x_0)$ be any based map. Let $K: X \times [0,1] \to X$ be the based contraction of $X$ to $x_0$. We can construct a based homotopy from $f$ to the constant map $c_{x_0}$ by first applying $f$ and then applying the contraction:
$$
H(a, t) = K(f(a), t)
$$
This map $H$ is a valid based homotopy:
- $H(a, 0) = K(f(a), 0) = f(a)$ (since $K$ starts at the identity on $X$).
- $H(a, 1) = K(f(a), 1) = x_0$ (since $K$ ends at the constant map).
- $H(a_0, t) = K(f(a_0), t) = K(x_0, t) = x_0$ (since $f$ is a based map and $K$ is a based homotopy).

Since every based map $f$ is based homotopic to the constant map $c_{x_0}$, all based maps are based homotopic to each other by transitivity. Thus, there is only one based homotopy class. Such spaces are considered "homotopically trivial" in the pointed category.

### Functorial Properties and the Fundamental Group

The true power of based homotopy emerges when we consider its interaction with composition. Based homotopy is compatible with map composition in two ways:

1.  **Pre-composition**: If $f_1, f_2: (X, x_0) \to (Y, y_0)$ are based homotopic via $H$, and $g: (Z, z_0) \to (X, x_0)$ is any based map, then the compositions $f_1 \circ g$ and $f_2 \circ g$ are based homotopic. The homotopy is given by $G(z, t) = H(g(z), t)$.

2.  **Post-composition**: If $g_1, g_2: (Z, z_0) \to (X, x_0)$ are based homotopic via $G$, and $f: (X, x_0) \to (Y, y_0)$ is any based map, then $f \circ g_1$ and $f \circ g_2$ are based homotopic via the homotopy $H(z, t) = f(G(z, t))$.

These properties ensure that composition is well-defined on homotopy classes: $[f] \circ [g] \equiv [f \circ g]$. This behavior is central to the concept of a **[functor](@entry_id:260898)** in [category theory](@entry_id:137315).

The most important application of this structure is the definition of the **fundamental group**. A **loop** based at $x_0$ is a based map from the pointed circle $(S^1, s_0)$ to $(X, x_0)$. The **fundamental group** of $(X, x_0)$, denoted $\pi_1(X, x_0)$, is the set of based homotopy classes of such loops, i.e., $\pi_1(X, x_0) = [(S^1, s_0), (X, x_0)]_*$. A group structure is defined on this set via [concatenation](@entry_id:137354) of loops.

Any based map $f: (X, x_0) \to (Y, y_0)$ induces a function between the fundamental groups, $f_*: \pi_1(X, x_0) \to \pi_1(Y, y_0)$. Given a homotopy class $[\gamma] \in \pi_1(X, x_0)$ represented by a loop $\gamma: (S^1, s_0) \to (X, x_0)$, its image under $f_*$ is defined by post-composition:
$$
f_*([\gamma]) = [f \circ \gamma]
$$
The composition $f \circ \gamma$ is indeed a loop based at $y_0$, since $(f \circ \gamma)(s_0) = f(\gamma(s_0)) = f(x_0) = y_0$. The well-definedness of $f_*$ on homotopy classes is a direct consequence of the compatibility of homotopy with post-composition. Furthermore, this [induced map](@entry_id:271712) $f_*$ is a [group homomorphism](@entry_id:140603).

As an example, consider the product space $S^1 \times S^1$ with basepoint $(1, 1)$. Its fundamental group is known to be isomorphic to $\mathbb{Z} \times \mathbb{Z}$. A map $f: (S^1, 1) \to (S^1 \times S^1, (1, 1))$ is determined by its component maps, $f(z) = (f_1(z), f_2(z))$, where $f_1, f_2: (S^1, 1) \to (S^1, 1)$ are themselves based loops. The element in $\pi_1(S^1 \times S^1, (1, 1))$ corresponding to $[f]$ is the pair of integers $(k_1, k_2)$, where $k_1$ is the degree ([winding number](@entry_id:138707)) of $f_1$ and $k_2$ is the degree of $f_2$. For instance, the map $f(z) = (z^2, \bar{z}^3)$ has component maps $f_1(z) = z^2$ (degree 2) and $f_2(z) = \bar{z}^3 = z^{-3}$ (degree -3). Therefore, the homotopy class $[f]$ corresponds to the pair $(2, -3)$ in $\mathbb{Z} \times \mathbb{Z}$.

### Based Homotopy Equivalence

The concept of "sameness" in homotopy theory is captured by homotopy equivalence. A based map $f: (X, x_0) \to (Y, y_0)$ is a **based homotopy equivalence** if there exists a based map $g: (Y, y_0) \to (X, x_0)$, called a **based homotopy inverse**, such that:
- $g \circ f \simeq_* \text{id}_X$
- $f \circ g \simeq_* \text{id}_Y$

Spaces that are connected by a based homotopy equivalence are considered equivalent in the pointed homotopy category. A key theorem states that if $f: (X, x_0) \to (Y, y_0)$ is a based homotopy equivalence, then for any [pointed space](@entry_id:265918) $(A, a_0)$, the [induced map](@entry_id:271712) $f_*: [(A, a_0), (X, x_0)]_* \to [(A, a_0), (Y, y_0)]_*$ given by $f_*([\alpha]) = [f \circ \alpha]$ is a bijection. The inverse of this map is simply $g_*$, induced by the homotopy inverse $g$. This means that from the perspective of mapping from any space $A$, the spaces $X$ and $Y$ are indistinguishable. As a special case when $A=S^1$, this implies that a based homotopy equivalence induces an [isomorphism](@entry_id:137127) of fundamental groups.

An important special type of homotopy equivalence is a **[deformation retraction](@entry_id:148036)**. A pointed subspace $(A, x_0)$ is a **based [deformation retract](@entry_id:154224)** of $(X, x_0)$ if there exists a homotopy $H: X \times [0,1] \to X$ that continuously shrinks $X$ onto $A$ while keeping $x_0$ fixed. If, in addition, the points within $A$ are kept fixed throughout the entire deformation (i.e., $H(a,t)=a$ for all $a \in A$), the retraction is called a **strong based [deformation retraction](@entry_id:148036)**. For example, the unit circle $S^1$ is a strong based [deformation retract](@entry_id:154224) of the punctured plane $\mathbb{R}^2 \setminus \{(0,0)\}$ with basepoint $(1,0)$. The radial projection homotopy $H_1((\rho, \theta), t) = ((1-t)\rho + t, \theta)$ demonstrates this, as points on the circle (where $\rho=1$) remain fixed for all $t$. In contrast, a homotopy like $H_2((\rho, \theta), t) = ((1-t)\rho + t, \theta + \sin(\pi t)\sin(\theta))$ also defines a [deformation retraction](@entry_id:148036) to the circle, but it is not strong because points on the circle (with $\sin(\theta) \neq 0$) "wobble" during the homotopy before settling back to their original positions at $t=1$.

### The Influence of the Basepoint

The entire structure we have built depends on the choice of basepoint. A natural question arises: what is the relationship between fundamental groups based at different points in the same space?

If the space $X$ is **path-connected**, then the fundamental groups $\pi_1(X, x_0)$ and $\pi_1(X, x_1)$ for any two points $x_0, x_1 \in X$ are isomorphic. The [isomorphism](@entry_id:137127), however, depends on the choice of a path between them. Let $\alpha: [0,1] \to X$ be a path from $x_0$ to $x_1$. This path induces an [isomorphism](@entry_id:137127) $\beta_{\alpha}: \pi_1(X, x_0) \to \pi_1(X, x_1)$ defined by "conjugation". For any loop $f$ based at $x_0$, representing $[f] \in \pi_1(X, x_0)$, the corresponding loop at $x_1$ is constructed by traversing the path $\alpha$ in reverse (from $x_1$ to $x_0$), performing the loop $f$, and then traversing $\alpha$ forward (from $x_0$ back to $x_1$). This new loop is $\bar{\alpha} * f * \alpha$, where $\bar{\alpha}(s) = \alpha(1-s)$ is the reverse path and $*$ denotes path [concatenation](@entry_id:137354). The induced [isomorphism](@entry_id:137127) is thus given by:
$$
\beta_{\alpha}([f]) = [\bar{\alpha} * f * \alpha]
$$
The inverse isomorphism from $\pi_1(X, x_1)$ to $\pi_1(X, x_0)$ is similarly given by $[g] \mapsto [\alpha * g * \bar{\alpha}]$.

The hypothesis of [path-connectedness](@entry_id:142695) is essential. If a space $X$ is not path-connected, the fundamental groups at basepoints in different [path-components](@entry_id:145705) can be completely unrelated in this sense. Consider a space $X$ consisting of two disjoint circles, $C_1$ and $C_2$. Let $p_1 \in C_1$ and $p_2 \in C_2$ be basepoints. Since $S^1$ is connected, any [continuous map](@entry_id:153772) $f: (S^1, s_0) \to (X, p_1)$ must have its image entirely contained within $C_1$. Similarly, any loop based at $p_2$ must lie entirely within $C_2$. Therefore, the set of based homotopy classes of loops at $p_1$, which is $\pi_1(X, p_1)$, is just $\pi_1(C_1, p_1) \cong \mathbb{Z}$. Likewise, $\pi_1(X, p_2)$ is $\pi_1(C_2, p_2) \cong \mathbb{Z}$. While these two groups are abstractly isomorphic, the sets of maps themselves are disjoint, and there is no path within $X$ connecting $p_1$ and $p_2$ to induce the "conjugation" isomorphism. The choice of basepoint fundamentally determines which part of the space is being probed by the fundamental group.