## Introduction
In the study of geometry, we often encounter objects that exist within a larger, [ambient space](@entry_id:184743)—a sphere embedded in three-dimensional space, a curve on a surface, or a configuration space constrained within a higher-dimensional state space. A fundamental question arises: how does the geometry of the larger space bestow a geometric structure upon the object living inside it? This article addresses this by introducing one of the most crucial tools in [differential geometry](@entry_id:145818): the **[induced metric](@entry_id:160616)**.

The [induced metric](@entry_id:160616) formalizes the intuitive idea of inheriting geometry. It provides the mathematical machinery to measure distances, angles, and areas on a submanifold, using the metric of the space it inhabits. This allows us to treat any [submanifold](@entry_id:262388) not just as a subset of points, but as a rich geometric space in its own right. This article will guide you through the theory, computation, and application of this powerful concept.

Our exploration is structured into three chapters. The first, **Principles and Mechanisms**, establishes the rigorous definition of the [induced metric](@entry_id:160616) as a [pullback](@entry_id:160816), explores its essential properties, and details the methods for its computation. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the utility of the [induced metric](@entry_id:160616) by examining the intrinsic geometry of familiar surfaces and exploring its profound connections to physics, abstract algebra, and information theory. Finally, **Hands-On Practices** will provide opportunities to solidify your understanding through targeted exercises. We begin by laying the foundational principles of this inherited geometry.

## Principles and Mechanisms

In our study of Riemannian manifolds, we frequently encounter situations where one manifold resides within another. A sphere sits inside three-dimensional Euclidean space; a torus can be visualized in the same ambient space. These "submanifolds" naturally inherit a geometric structure from the larger space they inhabit. Our objective in this chapter is to formalize this notion of inherited geometry. We will define the **[induced metric](@entry_id:160616)**—the primary tool for quantifying the intrinsic geometry of a submanifold—and explore its fundamental properties, computational methods, and profound geometric consequences.

### The Pullback as a Foundational Principle

The mechanism for endowing a submanifold with a metric is a general and powerful construction in differential geometry known as the **pullback**. Let us first consider a general scenario before specializing to submanifolds.

Suppose we have two [smooth manifolds](@entry_id:160799), $N$ and $M$, and a [smooth map](@entry_id:160364) $f: N \to M$. If $(M,g)$ is a Riemannian manifold, meaning $g$ is a smooth field of inner products on the tangent spaces of $M$, we can use the map $f$ to "pull back" the metric structure of $g$ from $M$ to $N$. The result is a $(0,2)$-tensor field on $N$, denoted $f^*g$, defined as follows. For any point $p \in N$ and any pair of tangent vectors $v, w \in T_p N$, the value of the [pullback](@entry_id:160816) tensor $(f^*g)_p$ is given by:

$$
(f^*g)_p(v,w) \coloneqq g_{f(p)}(df_p(v), df_p(w))
$$
[@problem_id:3051556]

Let us dissect this definition. The vectors $v$ and $w$ originate in the tangent space of $N$ at $p$. The differential of the map, $df_p: T_p N \to T_{f(p)} M$, pushes these vectors forward into the tangent space of $M$ at the image point $f(p)$. Once there, their inner product is computed using the metric $g$ that is native to the ambient manifold $M$. This result is then assigned as the value of the inner product of $v$ and $w$ on $N$. In essence, we measure vectors in $N$ by first mapping them into $M$ and measuring them there.

Now, we apply this principle to the case of an [embedded submanifold](@entry_id:273162) $S \subset M$. The natural map from the [submanifold](@entry_id:262388) to the ambient manifold is the **inclusion map**, denoted $i: S \hookrightarrow M$, which simply sends each point $p \in S$ to itself, $i(p)=p$. The [induced metric](@entry_id:160616) on $S$, which we shall denote by $g^S$, is defined as the [pullback](@entry_id:160816) of the ambient metric $g$ by this inclusion map:

**Definition:** The **induced Riemannian metric** $g^S$ on a [submanifold](@entry_id:262388) $S \subset (M,g)$ is the [pullback](@entry_id:160816) $g^S \coloneqq i^*g$.

Applying the general [pullback](@entry_id:160816) formula, the pointwise expression for the [induced metric](@entry_id:160616) at a point $p \in S$ for vectors $u, v \in T_p S$ is:

$$
g^S_p(u,v) = g_{i(p)}(di_p(u), di_p(v))
$$
[@problem_id:3051532, 3053356]

Here, the differential $di_p: T_p S \to T_p M$ is the canonical identification of the [tangent space](@entry_id:141028) of the submanifold as a linear subspace of the [tangent space](@entry_id:141028) of the ambient manifold. Since $S$ is an [embedded submanifold](@entry_id:273162), the inclusion map $i$ is an immersion, which means its differential $di_p$ is an injective [linear map](@entry_id:201112) at every point $p \in S$.

It is crucial to distinguish this rigorous definition from a common, informal turn of phrase. One often hears that the [induced metric](@entry_id:160616) is obtained by "restricting the metric $g$ to the tangent spaces of $S$". While this captures the spirit of the construction, it is formally imprecise. A true restriction of $g$ to the points of $S$, which we might denote $g|_S$, would still be a field of inner products on the full [tangent spaces](@entry_id:199137) $T_p M$ for $p \in S$. The [pullback](@entry_id:160816) $g^S = i^*g$, by contrast, is a new [tensor field](@entry_id:266532) on $S$, whose value at each $p \in S$ is an inner product on the smaller space $T_p S$ [@problem_id:3051512]. However, because $di_p$ is simply the inclusion of $T_p S$ into $T_p M$, the formula simplifies in practice. After identifying the vectors $u,v \in T_p S$ with their images in $T_p M$, the definition becomes $g^S_p(u,v) = g_p(u,v)$. This notational convenience is what gives rise to the "restriction" language, but the pullback formalism is the true underlying mechanism.

### Fundamental Properties of the Induced Metric

#### Non-degeneracy and Regularity

A central question is whether the induced tensor $g^S$ is itself a legitimate Riemannian metric on $S$. A Riemannian metric must be a smooth, symmetric, and positive-definite $(0,2)$-[tensor field](@entry_id:266532). The smoothness of $g^S = i^*g$ follows from the smoothness of $i$ and $g$. Symmetry is also inherited directly from the symmetry of $g$:
$g^S_p(u,v) = g_p(di_p(u), di_p(v)) = g_p(di_p(v), di_p(u)) = g^S_p(v,u)$.

The critical property is **[positive-definiteness](@entry_id:149643)**. To show that $g^S_p(u,u) > 0$ for any non-zero vector $u \in T_p S$, we rely on the fact that the inclusion map $i: S \hookrightarrow M$ is an immersion. This means its differential $di_p$ is injective. Therefore, if $u \neq 0$, its image $di_p(u)$ is also a non-[zero vector](@entry_id:156189) in $T_p M$. Since the ambient metric $g$ is positive-definite, we must have $g_p(di_p(u), di_p(u)) > 0$. By definition, this value is $g^S_p(u,u)$, so the [induced metric](@entry_id:160616) is positive-definite [@problem_id:3053356].

This reveals a deep connection: the [pullback](@entry_id:160816) of a Riemannian metric $g$ by a [smooth map](@entry_id:160364) $f: N \to M$ produces a bona fide Riemannian metric on $N$ if and only if the map $f$ is an **immersion** (i.e., $df_p$ is injective at every point $p \in N$). If $f$ fails to be an immersion at some point $p_0$, meaning there exists a non-[zero vector](@entry_id:156189) $v_0 \in T_{p_0}N$ such that $df_{p_0}(v_0) = 0$, then the [pullback metric](@entry_id:161465) becomes **degenerate** at that point [@problem_id:3051556]. For such a vector $v_0$, we have:

$$
(f^*g)_{p_0}(v_0, v_0) = g_{f(p_0)}(df_{p_0}(v_0), df_{p_0}(v_0)) = g_{f(p_0)}(0, 0) = 0
$$

This violates [positive-definiteness](@entry_id:149643). A map that is not an immersion at a point is sometimes said to have a singularity. For example, consider the map $\sigma: \mathbb{R}^2 \to \mathbb{R}^3$ given by $\sigma(u,v) = (uv, u, v^2)$. Its differential fails to be injective at the origin $(0,0)$. Correspondingly, the [induced metric](@entry_id:160616) on the [parameter space](@entry_id:178581) $\mathbb{R}^2$ is positive-definite everywhere except at the origin, where its determinant vanishes, indicating degeneracy [@problem_id:3053355]. Such a degeneracy is an intrinsic feature of the geometry at the image point and cannot be removed simply by changing the parametrization.

#### Invariance and Coordinate Representations

The definition of the [induced metric](@entry_id:160616), $g^S = i^*g$, is entirely coordinate-free. It is constructed from the intrinsic geometric objects $S$, $M$, and $g$. This means that the [induced metric](@entry_id:160616) $g^S$ is itself an intrinsic geometric object on $S$. It does not depend on any particular choice of parametrization or [coordinate chart](@entry_id:263963) for $S$ [@problem_id:3051546].

While the metric itself is invariant, its representation changes with the choice of coordinates. A parametrization $\phi: U \subset \mathbb{R}^k \to S$ provides [local coordinates](@entry_id:181200) on a patch of the submanifold. The coordinate representation of the metric $g^S$ is given by the [pullback](@entry_id:160816) $\phi^*g^S$. If we have another [parametrization](@entry_id:272587) $\psi: V \to S$ related to the first by a change-of-coordinates [diffeomorphism](@entry_id:147249) $F: V \to U$ (so that $\psi = \phi \circ F$), the new coordinate representation is $\psi^*g^S$. These two representations are not identical, but are related by the [tensor transformation law](@entry_id:160511):

$$
\psi^*g^S = (\phi \circ F)^*g^S = F^*(\phi^*g^S)
$$
[@problem_id:3051546]

This consistent transformation rule is the hallmark of a well-defined tensor field. It confirms that the different coordinate matrices are merely different "views" of the same underlying coordinate-independent tensor, the [induced metric](@entry_id:160616) $g^S$.

### Methods of Computation

While the abstract definition is powerful, practical applications require concrete computation. The method depends on how the submanifold is described.

#### Parametrized Submanifolds

The most common scenario is a [submanifold](@entry_id:262388) defined by a parametrization $\phi: U \subset \mathbb{R}^k \to M$, where $U$ has coordinates $(u^1, \dots, u^k)$ and $M$ has [local coordinates](@entry_id:181200) $(x^1, \dots, x^n)$. The [induced metric](@entry_id:160616) $h$ on the parameter domain $U$ is the [pullback](@entry_id:160816) of $g$ via the composite map $\phi: U \to M$. Its components $h_{ij}$ are found by evaluating the metric on the basis vectors $\frac{\partial}{\partial u^i}$ and $\frac{\partial}{\partial u^j}$. A direct application of the [chain rule](@entry_id:147422) and the [pullback](@entry_id:160816) definition yields the master formula for the [induced metric](@entry_id:160616) components [@problem_id:3051519, 3051556]:

$$
h_{ij}(u) = g_{\alpha\beta}(\phi(u)) \frac{\partial \phi^\alpha}{\partial u^i}(u) \frac{\partial \phi^\beta}{\partial u^j}(u)
$$

Here, Einstein summation over the Greek indices $\alpha, \beta$ from $1$ to $n$ is implied. The components $g_{\alpha\beta}$ are those of the ambient metric, evaluated at the point $\phi(u)$ on the [submanifold](@entry_id:262388), and the partial derivatives are the components of the Jacobian matrix of the parametrization $\phi$.

As an example, consider the ambient manifold $M=\mathbb{R}^3$ with the non-Euclidean metric $g = dx^2 + dy^2 + \exp(2x) dz^2$. Let $S$ be a surface parametrized by $\phi(u,v) = (u, v, uv)$. Using the formula above, one can compute the components of the [induced metric](@entry_id:160616) matrix $h(u,v)$ on the parameter domain $\mathbb{R}^2$ to be:
$$
h(u,v) = \begin{pmatrix} 1 + v^2\exp(2u) & uv\exp(2u) \\ uv\exp(2u) & 1 + u^2\exp(2u) \end{pmatrix}
$$
[@problem_id:3051519]

This matrix provides the complete local geometric information of the surface.

#### Surfaces in Euclidean Space: The First Fundamental Form

A historically important and highly intuitive special case is that of a surface $S$ in Euclidean space $\mathbb{R}^3$ with its standard dot [product metric](@entry_id:637352). For a parametrization $\phi(u,v)$, the [tangent vectors](@entry_id:265494) to the coordinate curves are $\phi_u = \frac{\partial \phi}{\partial u}$ and $\phi_v = \frac{\partial \phi}{\partial v}$. The components of the [induced metric](@entry_id:160616) are given by the dot products of these vectors [@problem_id:3051550]:

-   $E(u,v) = \phi_u \cdot \phi_u = |\phi_u|^2$
-   $F(u,v) = \phi_u \cdot \phi_v$
-   $G(u,v) = \phi_v \cdot \phi_v = |\phi_v|^2$

These coefficients, $E, F, G$, are the components of the **first fundamental form**, a classical term for the [induced metric](@entry_id:160616) on a surface. They have direct geometric interpretations: $\sqrt{E}$ and $\sqrt{G}$ are the speeds at which one travels along the surface when moving along the $u$- and $v$-coordinate curves, respectively. The coefficient $F$ is related to the angle $\theta$ between these coordinate curves by $F = \sqrt{EG} \cos\theta$. Thus, the coordinate system is orthogonal on the surface if and only if $F=0$.

#### Implicitly Defined Submanifolds

Submanifolds can also be defined as the [level set](@entry_id:637056) of a [regular value](@entry_id:188218). Let $\Phi: M \to \mathbb{R}^r$ be a [smooth map](@entry_id:160364) and $c \in \mathbb{R}^r$ be a [regular value](@entry_id:188218). Then $S = \Phi^{-1}(c)$ is a smooth [embedded submanifold](@entry_id:273162) of $M$. A fundamental result states that the tangent space to $S$ at a point $p \in S$ is precisely the kernel of the differential of $\Phi$ at that point:

$$
T_p S = \ker d\Phi_p
$$
[@problem_id:3051517]

The [induced metric](@entry_id:160616) $g^S$ on $S$ is, as always, the [pullback](@entry_id:160816) $i^*g$. This means that at each point $p$, $g^S_p$ is the inner product obtained by restricting the ambient inner product $g_p$ to the subspace $\ker d\Phi_p \subset T_p M$. The dimension of this subspace, and hence the dimension of the submanifold $S$, is given by the [rank-nullity theorem](@entry_id:154441) as $\dim M - r$.

### Geometric Consequences

The [induced metric](@entry_id:160616) is not just a computational device; it is the key to understanding all intrinsic geometric properties of a [submanifold](@entry_id:262388).

#### Arc Length, Area, and Volume

The length of a smooth curve $\gamma: [a,b] \to S$ is defined by integrating its speed, as measured by the [induced metric](@entry_id:160616) $g^S$:

$$
L_S(\gamma) = \int_a^b \sqrt{g^S_{\gamma(t)}(\dot{\gamma}(t), \dot{\gamma}(t))} \, dt
$$
[@problem_id:3053378]

By the very definition of the [induced metric](@entry_id:160616), the term under the square root is $g_{\gamma(t)}(di_{\gamma(t)}(\dot{\gamma}(t)), di_{\gamma(t)}(\dot{\gamma}(t)))$. This is precisely the squared speed of the curve when viewed in the ambient manifold $M$. Consequently, the length of a curve in a submanifold is exactly the same as its length in the ambient space. The [induced metric](@entry_id:160616) is constructed to ensure this consistency, making the inclusion map $i: (S, g^S) \to (M, g)$ an **[isometric immersion](@entry_id:272242)**.

Similarly, the area of a patch on a surface, or more generally the volume of a region in a $k$-dimensional submanifold, is computed by integrating the **[volume element](@entry_id:267802)** derived from the [induced metric](@entry_id:160616). In [local coordinates](@entry_id:181200) $(u^1, \dots, u^k)$, this volume element is given by:

$$
d\text{vol}_S = \sqrt{\det(h_{ij})} \, du^1 \dots du^k
$$

For a surface in $\mathbb{R}^3$, this familiar expression becomes $dA = \sqrt{EG-F^2} \, du \, dv$ [@problem_id:3051550]. This quantity represents the area of the infinitesimal parallelogram on the surface spanned by the [tangent vectors](@entry_id:265494) corresponding to infinitesimal displacements in the coordinate directions.

#### Metric Completeness

A deeper topological property determined by the metric is completeness. A Riemannian manifold $(S, g^S)$ is **metrically complete** if every Cauchy sequence with respect to its [intrinsic distance](@entry_id:637359) function $d_{g^S}$ converges to a point within $S$. The [intrinsic distance](@entry_id:637359) $d_{g^S}(p,q)$ is the [infimum](@entry_id:140118) of the lengths of all curves in $S$ connecting points $p$ and $q$.

A remarkable theorem connects the topological properties of a submanifold of Euclidean space with its [metric completeness](@entry_id:186235). It can be shown that for any two points $p, q$ in a [submanifold](@entry_id:262388) $S \subset \mathbb{R}^n$, the [intrinsic distance](@entry_id:637359) $d_g(p,q)$ is always greater than or equal to the straight-line Euclidean distance $\|p-q\|$. This implies that any sequence that is Cauchy with respect to the [intrinsic distance](@entry_id:637359) is also Cauchy in the Euclidean metric. If the submanifold $S$ is also a **closed subset** of $\mathbb{R}^n$, then the following argument holds [@problem_id:3051497]:

1.  A Cauchy sequence in $(S, d_g)$ is also a Cauchy sequence in $\mathbb{R}^n$.
2.  Since $\mathbb{R}^n$ is complete, this sequence converges to a limit point $p \in \mathbb{R}^n$.
3.  Because $S$ is a [closed set](@entry_id:136446), this [limit point](@entry_id:136272) $p$ must lie within $S$.
4.  It can further be shown that convergence in the Euclidean distance implies convergence in the [intrinsic distance](@entry_id:637359).

Therefore, we have the powerful result: **Any closed [embedded submanifold](@entry_id:273162) of Euclidean space is metrically complete with respect to its [induced metric](@entry_id:160616).** This theorem guarantees, for example, that a sphere or an infinite cylinder is metrically complete, whereas a sphere with a point removed (which is not a closed subset of $\mathbb{R}^3$) is not. This property is crucial for the study of geodesics and the global structure of manifolds.