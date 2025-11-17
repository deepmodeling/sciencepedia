## Introduction
The geometry of a curved surface, like the Earth, is fundamentally different from that of a flat plane. But how do we precisely measure distances, angles, and areas on such an object when it lives inside a larger space? The answer lies in the concept of the **[induced metric](@entry_id:160616)**, a central tool in differential geometry that allows us to quantify the intrinsic geometry of a [submanifold](@entry_id:262388) using the structure of the [ambient space](@entry_id:184743) it inhabits. This article addresses the fundamental challenge of translating geometric properties from a larger manifold to a smaller one embedded within it.

This exploration is divided into three parts. First, in **Principles and Mechanisms**, we will rigorously define the [induced metric](@entry_id:160616) using the [pullback](@entry_id:160816) operation, explore its essential properties like [positive-definiteness](@entry_id:149643), and learn how to compute it as the first fundamental form. Next, in **Applications and Interdisciplinary Connections**, we will see how this concept is applied to understand the geometry of familiar surfaces, and how it serves as a unifying principle in fields ranging from Einstein's [theory of relativity](@entry_id:182323) to modern information theory. Finally, **Hands-On Practices** will provide you with concrete exercises to solidify your understanding and build practical computational skills. By the end, you will have a robust grasp of how to define, calculate, and apply induced metrics to analyze the rich world of submanifolds.

## Principles and Mechanisms

The geometry of a submanifold is intrinsically linked to the geometry of the [ambient space](@entry_id:184743) in which it resides. The primary tool for quantifying this relationship is the **[induced metric](@entry_id:160616)**. This chapter elucidates the formal mechanism for defining the [induced metric](@entry_id:160616)—the [pullback](@entry_id:160816) of a tensor—and explores its properties and applications, from the local computation of lengths and areas to global topological consequences.

### The Pullback of a Tensor: A General Mechanism

Before specializing to [submanifolds](@entry_id:159439), we must first understand the general operation of **pullback**. Let $N$ and $M$ be [smooth manifolds](@entry_id:160799) and let $f: N \to M$ be a [smooth map](@entry_id:160364). This map allows us to "pull back" [covariant tensor](@entry_id:198677) fields from the target manifold $M$ to the source manifold $N$.

Consider a covariant $(0,k)$-tensor field $\omega$ on $M$. At each point $q \in M$, $\omega_q$ is a [multilinear map](@entry_id:274221) that takes $k$ tangent vectors from $T_qM$ and produces a real number. We wish to define a new tensor field on $N$, called the [pullback](@entry_id:160816) of $\omega$ by $f$ and denoted $f^*\omega$, which performs a similar function on the tangent spaces of $N$.

The definition is constructed as follows: for any point $p \in N$, the pullback tensor $(f^*\omega)_p$ must be a [multilinear map](@entry_id:274221) on the tangent space $T_pN$. Its arguments will be vectors $v_1, \dots, v_k \in T_pN$. We can use the differential of $f$ at $p$, denoted $df_p: T_pN \to T_{f(p)}M$, to transport these vectors into the [tangent space](@entry_id:141028) of $M$ at the point $f(p)$. Once they are in $T_{f(p)}M$, we can apply the original tensor $\omega_{f(p)}$ to them.

This leads to the formal definition. The **pullback** $(f^*\omega)_p$ at a point $p \in N$ is a $(0,k)$-tensor on $T_pN$ defined by:
$$ (f^*\omega)_p(v_1, \dots, v_k) := \omega_{f(p)}(df_p(v_1), \dots, df_p(v_k)) $$
for all $v_1, \dots, v_k \in T_pN$. This construction is valid for any [smooth map](@entry_id:160364) $f$ and any [covariant tensor](@entry_id:198677) field $\omega$.

Our primary interest is in Riemannian metrics, which are symmetric $(0,2)$-[tensor fields](@entry_id:190170). If $g$ is a metric on $M$, its [pullback](@entry_id:160816) $f^*g$ is a $(0,2)$-[tensor field](@entry_id:266532) on $N$ given by the rule [@problem_id:3051556]:
$$ (f^*g)_p(v,w) := g_{f(p)}(df_p v, df_p w) \quad \text{for all } v,w \in T_p N. $$

In [local coordinates](@entry_id:181200), this abstract definition takes a concrete form. Let $y = (y^1, \dots, y^n)$ be [local coordinates](@entry_id:181200) on an open set in $N$, and $x = (x^1, \dots, x^m)$ be [local coordinates](@entry_id:181200) on an open set in $M$. The map $f$ is expressed as $x^a = f^a(y)$, and the metric $g$ has components $g_{ab}(x)$. The components of the pullback tensor, $(f^*g)_{ij}$, are found by evaluating it on the basis vectors $\frac{\partial}{\partial y^i}$ and $\frac{\partial}{\partial y^j}$. A direct calculation using the chain rule, which gives $df_p(\frac{\partial}{\partial y^i}) = \frac{\partial f^a}{\partial y^i} \frac{\partial}{\partial x^a}$, yields the coordinate expression [@problem_id:3051556]:
$$ (f^*g)_{ij}(p) = \sum_{a,b} g_{ab}(f(p)) \frac{\partial f^a}{\partial y^i}(p) \frac{\partial f^b}{\partial y^j}(p). $$
This formula is often recognized from physics and engineering as the transformation rule for the metric tensor under a change of coordinates, which is a specific application of the pullback.

### The Induced Metric on a Submanifold

We now apply this powerful mechanism to the specific context of a smooth [embedded submanifold](@entry_id:273162) $S \subset M$. An [embedded submanifold](@entry_id:273162) comes with a natural [smooth map](@entry_id:160364): the **inclusion map** $i: S \hookrightarrow M$, defined by $i(p) = p$ for all $p \in S$. The [induced metric](@entry_id:160616) on $S$ is defined precisely as the [pullback](@entry_id:160816) of the ambient metric $g$ by this inclusion map.

Let $g^S$ denote the [induced metric](@entry_id:160616) on $S$. By definition:
$$ g^S := i^*g. $$
At any point $p \in S$, for any two [tangent vectors](@entry_id:265494) $u,v \in T_pS$, the value of the [induced metric](@entry_id:160616) is given by the general [pullback](@entry_id:160816) formula [@problem_id:3053356]:
$$ g^S_p(u,v) = (i^*g)_p(u,v) = g_{i(p)}(di_p u, di_p v). $$

To fully appreciate this definition, we must understand the nature of the tangent space $T_pS$ and the differential $di_p$. For an [embedded submanifold](@entry_id:273162), the tangent space $T_pS$ can be intrinsically defined (for example, via [equivalence classes](@entry_id:156032) of smooth curves $\gamma: (-\epsilon, \epsilon) \to S$ with $\gamma(0)=p$). The differential of the inclusion map, $di_p: T_pS \to T_pM$, takes such a curve-based [tangent vector](@entry_id:264836) $[ \gamma ]_S$ and maps it to $[ i \circ \gamma ]_M$, which is a tangent vector in the ambient space. A key property of an embedding is that it is an **immersion**, meaning $di_p$ is an injective [linear map](@entry_id:201112) for all $p \in S$. This injectivity allows us to canonically identify the "abstract" tangent space $T_pS$ with its image, a linear subspace of the "concrete" [tangent space](@entry_id:141028) $T_pM$ [@problem_id:3051532].

Under this identification, where we consider $u \in T_pS$ as being the same as its image $di_p u \in T_pM$, and noting that $i(p)=p$, the definition of the [induced metric](@entry_id:160616) simplifies to a very intuitive form:
$$ g^S_p(u,v) = g_p(u,v) \quad \text{for } u,v \in T_pS. $$
This simplification often leads to the informal phrase "the [induced metric](@entry_id:160616) is the restriction of the ambient metric to the submanifold." While intuitively useful, this phrasing can be misleading. A simple restriction of $g$ to points in $S$, denoted $g|_S$, would still be a field of [bilinear forms](@entry_id:746794) on the ambient [tangent spaces](@entry_id:199137) $T_pM$. The pullback $i^*g$ is the rigorous operation that correctly produces a new [tensor field](@entry_id:266532) $g^S$ whose domain at each point $p \in S$ is the smaller space $T_pS \times T_pS$, thus defining a metric *on* the [submanifold](@entry_id:262388) $S$ [@problem_id:3051512]. The elegance of the pullback is that it automatically handles this change in domain.

### Key Properties of the Induced Metric

#### Positive-Definiteness and Degeneracy

For $g^S$ to be a true Riemannian metric on $S$, it must be positive-definite at every point. That is, for any non-[zero vector](@entry_id:156189) $v \in T_pS$, we must have $g^S_p(v,v) > 0$. This property is inherited from the ambient metric $g$ because the inclusion map $i: S \hookrightarrow M$ is an immersion.

Let's examine the condition: $g^S_p(v,v) = g_p(di_p v, di_p v)$. Since $v \neq 0$ and $di_p$ is injective, its image $di_p v$ is a non-zero vector in $T_pM$. Because $g$ is a Riemannian metric on $M$, it is positive-definite, which means $g_p(di_p v, di_p v) > 0$. Thus, $g^S_p(v,v) > 0$, confirming that the [induced metric](@entry_id:160616) on an [embedded submanifold](@entry_id:273162) is indeed a Riemannian metric [@problem_id:3053356].

This contrasts sharply with the pullback of a metric by a map that is *not* an immersion. If a [smooth map](@entry_id:160364) $f: N \to M$ is not an immersion at a point $p \in N$, its differential $df_p$ has a non-trivial kernel. This means there exists a non-zero vector $v_0 \in T_pN$ such that $df_p(v_0) = 0$. For such a vector, the pullback form yields:
$$ (f^*g)_p(v_0, v_0) = g_{f(p)}(df_p v_0, df_p v_0) = g_{f(p)}(0, 0) = 0. $$
Since we have found a non-zero vector on which the [pullback](@entry_id:160816) form evaluates to zero, the form $(f^*g)_p$ is not positive-definite; it is called **degenerate**.

For a concrete example, consider the map $f: \mathbb{R} \to \mathbb{R}^2$ given by $f(t) = (t^3, t^2)$, and let $\mathbb{R}^2$ have the standard Euclidean metric $g$. At $t=0$, the differential is $df_0(\partial_t) = (3t^2, 2t)|_{t=0} = (0,0)$. The map is not an immersion at this point. The pullback of the metric, when evaluated on the [basis vector](@entry_id:199546) $\partial_t \in T_0\mathbb{R}$, gives $(f^*g)_0(\partial_t, \partial_t) = g_{(0,0)}((0,0), (0,0)) = 0$. The resulting pullback [tensor field](@entry_id:266532) is degenerate at $t=0$ and fails to be a Riemannian metric there [@problem_id:3051492].

#### Coordinate Invariance

A fundamental property of the [induced metric](@entry_id:160616) is that it is an **intrinsic** geometric object on the [submanifold](@entry_id:262388) $S$. Its definition, $g^S = i^*g$, is entirely independent of any choice of coordinates or [parametrization](@entry_id:272587) for $S$. Different parametrizations will lead to different component matrices for the metric, but they are all representations of the same underlying tensor field.

To see this more formally, let $h=g^S$ be the [induced metric](@entry_id:160616) tensor on $S$. Consider two different parametrizations (charts) for $S$, $\varphi: U \subset \mathbb{R}^k \to S$ and $\psi: V \subset \mathbb{R}^k \to S$, related by a change-of-coordinates diffeomorphism $F: V \to U$ such that $\psi = \varphi \circ F$.

The coordinate expression of the metric $h$ in the $\psi$ chart is the pullback $\psi^*h$. The coordinate expression in the $\varphi$ chart is $\varphi^*h$. Using the property that [pullback](@entry_id:160816) commutes with composition, we have:
$$ \psi^*h = (\varphi \circ F)^*h = F^*(\varphi^*h). $$
This is the standard transformation law for the components of a $(0,2)$-tensor. It shows that the components in one coordinate system can be systematically derived from the components in another. The existence of this consistent transformation rule is the hallmark of a well-defined [tensor field](@entry_id:266532) on the manifold, independent of any particular chart [@problem_id:3051496]. The [induced metric](@entry_id:160616) depends only on the ambient metric $g$ and the structure of $S$ as a [submanifold](@entry_id:262388), not on how we choose to describe it with coordinates [@problem_id:3051546].

### The First Fundamental Form: Computation and Geometry

While the abstract definition is powerful, practical calculations often require working in [local coordinates](@entry_id:181200). When a submanifold is given by a [parametrization](@entry_id:272587), the [induced metric](@entry_id:160616)'s components are known as the coefficients of the **[first fundamental form](@entry_id:274022)**.

Consider a surface $S$ in $\mathbb{R}^3$ parametrized by a map $\sigma: U \subset \mathbb{R}^2 \to S$, where $U$ is an open set in the $(u,v)$-plane. The ambient metric on $\mathbb{R}^3$ is the standard dot product. The tangent vectors to the coordinate curves on the surface are given by the [partial derivatives](@entry_id:146280) $\sigma_u = \frac{\partial \sigma}{\partial u}$ and $\sigma_v = \frac{\partial \sigma}{\partial v}$. These two vectors form a basis for the [tangent space](@entry_id:141028) $T_{\sigma(u,v)}S$ (where the [parametrization](@entry_id:272587) is regular).

The components of the [induced metric](@entry_id:160616) matrix in this $(u,v)$ coordinate system are computed by taking the dot products of these basis vectors. Classically, these components are denoted $E, F, G$:
- $E(u,v) = \langle \sigma_u, \sigma_u \rangle = |\sigma_u|^2$
- $F(u,v) = \langle \sigma_u, \sigma_v \rangle$
- $G(u,v) = \langle \sigma_v, \sigma_v \rangle$

The metric can then be written as the differential form $ds^2 = E\,du^2 + 2F\,du\,dv + G\,dv^2$, which is the first fundamental form. For example, for the surface parametrized by $\sigma(u,v) = ((u+c)\cos v, (u-c)\sin v, k v)$, the [tangent vectors](@entry_id:265494) are $\sigma_u = (\cos v, \sin v, 0)$ and $\sigma_v = (-(u+c)\sin v, (u-c)\cos v, k)$. The coefficients are then computed as dot products [@problem_id:3053362]:
$$ g^S = \begin{pmatrix} E & F \\ F & G \end{pmatrix} = \begin{pmatrix} 1 & -c \sin(2v) \\ -c \sin(2v) & u^2 + c^2 + k^2 - 2uc \cos(2v) \end{pmatrix}. $$

These coefficients have direct geometric meaning [@problem_id:3051550]:
- $\sqrt{E}\,du$ is the infinitesimal length along a curve where $v$ is constant.
- $\sqrt{G}\,dv$ is the infinitesimal length along a curve where $u$ is constant.
- $F$ measures the [non-orthogonality](@entry_id:192553) of the coordinate curves. The angle $\theta$ between the $u$-curve and the $v$-curve on the surface is given by $\cos\theta = \frac{F}{\sqrt{EG}}$. If $F=0$, the coordinate system is orthogonal.

### Applications: Measuring the Intrinsic World

The [induced metric](@entry_id:160616) is the fundamental tool for performing geometric measurements on a submanifold, such as calculating lengths, angles, and areas, entirely in terms of the [submanifold](@entry_id:262388)'s own coordinates.

#### Length, Area, and Submanifolds as Level Sets

The **length** of a smooth curve $\gamma: [a,b] \to S$ is defined by integrating its speed, where speed is measured using the [induced metric](@entry_id:160616) $g^S$:
$$ L_S(\gamma) = \int_{a}^{b} \sqrt{g^S_{\gamma(t)}(\dot{\gamma}(t), \dot{\gamma}(t))} \,dt. $$
A crucial consistency check is to compare this "intrinsic" length with the length of the curve as viewed in the ambient manifold $M$. The curve in $M$ is $i \circ \gamma$, and its [tangent vector](@entry_id:264836) is $d(i\circ\gamma)/dt = di_{\gamma(t)}(\dot\gamma(t))$. The ambient length is:
$$ L_M(i \circ \gamma) = \int_{a}^{b} \sqrt{g_{i(\gamma(t))}(di_{\gamma(t)}(\dot{\gamma}(t)), di_{\gamma(t)}(\dot{\gamma}(t)))} \,dt. $$
By the very definition of the [induced metric](@entry_id:160616) $g^S$, the integrands of these two expressions are identical. Therefore, the length of a curve in a [submanifold](@entry_id:262388) is precisely its length in the [ambient space](@entry_id:184743): $L_S(\gamma) = L_M(i \circ \gamma)$ [@problem_id:3053378]. This is not a special property of certain curves or [submanifolds](@entry_id:159439); it is a direct consequence of the definition.

The **area** of a region on a parametrized surface is found by integrating the infinitesimal area element, $dA$. For a surface parametrized by $(u,v)$, the area element is the area of the infinitesimal parallelogram spanned by $\sigma_u du$ and $\sigma_v dv$, which is $|\sigma_u \times \sigma_v| \,du\,dv$. Using Lagrange's identity, this magnitude can be expressed in terms of the first fundamental form coefficients: $|\sigma_u \times \sigma_v|^2 = |\sigma_u|^2 |\sigma_v|^2 - \langle \sigma_u, \sigma_v \rangle^2 = EG - F^2$. Thus, the area element is $dA = \sqrt{EG-F^2}\,du\,dv$. The total area is then $\iint_U \sqrt{EG-F^2}\,du\,dv$. For the paraboloid $\phi(u,v) = (u\cos v, u\sin v, bu^2)$, one finds $E=1+4b^2u^2, F=0, G=u^2$, so the area over a disk of radius $R$ is found by computing the integral $\int_0^{2\pi} \int_0^R u\sqrt{1+4b^2u^2} \,du\,dv$ [@problem_id:3051550].

Submanifolds are also frequently defined implicitly as the **level set** of a [regular value](@entry_id:188218). If $\Phi: M \to \mathbb{R}^r$ is a [smooth map](@entry_id:160364) and $c \in \mathbb{R}^r$ is a [regular value](@entry_id:188218), then $S = \Phi^{-1}(c)$ is an $(n-r)$-dimensional submanifold of $M$. In this case, the tangent space $T_pS$ is elegantly characterized as the kernel of the differential: $T_pS = \ker d\Phi_p$. This means a vector $X \in T_pM$ is tangent to $S$ if and only if $d\Phi_p(X) = 0$ [@problem_id:3051517]. The [induced metric](@entry_id:160616) on $S$ is then simply the restriction of the ambient metric $g$ to this subspace.

#### Global Properties: Completeness

The [induced metric](@entry_id:160616) determines not only local geometry but also global [topological properties](@entry_id:154666). One such property is **[metric completeness](@entry_id:186235)**. A Riemannian manifold is complete if every Cauchy sequence of points converges to a point within the manifold. While a compact manifold like the unit sphere $S^2 \subset \mathbb{R}^3$ is always complete with its [induced metric](@entry_id:160616), its submanifolds need not be.

Consider the punctured sphere $M = S^2 \setminus \{p\}$, where $p$ is the north pole. $M$ is a smooth submanifold of $S^2$ (and of $\mathbb{R}^3$) and inherits an [induced metric](@entry_id:160616). However, $(M, g^M)$ is not a complete metric space. To see this, consider a sequence of points $x_n$ in $M$ on a meridian, approaching the north pole $p$. For instance, let $x_n$ have colatitude $\theta_n = 1/n$. The Riemannian distance between two points $x_m$ and $x_n$ is the length of the [great circle](@entry_id:268970) arc connecting them, which is simply $|\theta_m - \theta_n| = |1/m - 1/n|$. This sequence is a Cauchy sequence. However, it does not converge to any point *in M*, because its limit point in the larger space $S^2$ is the puncture $p$, which has been removed [@problem_id:3051502]. This demonstrates that removing even a single point can destroy the global property of completeness.