## Introduction
When we study a curved surface, how can we describe its geometry? We can consider its properties relative to the space it sits in—its [extrinsic geometry](@entry_id:262461)—or we can explore properties that an inhabitant of the surface could measure without ever leaving it. This latter perspective, known as intrinsic geometry, deals with fundamental quantities like the length of a path, the angle between intersecting curves, and the area of a region. The primary mathematical tool for this task is the **first fundamental form**, a concept that formalizes the notion of a metric on a curved space. This article provides a comprehensive exploration of this pivotal object, addressing the central problem of how to quantify a surface’s inherent geometric structure.

This exploration is divided into three parts. First, the chapter on **Principles and Mechanisms** will introduce the [first fundamental form](@entry_id:274022) from its abstract definition as a [pullback metric](@entry_id:161465) to its concrete application for surfaces in $\mathbb{R}^3$, detailing how its coefficients encode length, angle, and area. Next, **Applications and Interdisciplinary Connections** will showcase its utility beyond basic computations, demonstrating its role in curvature theory through Gauss's Theorema Egregium and its foundational importance in fields like general relativity, materials science, and [numerical analysis](@entry_id:142637). Finally, **Hands-On Practices** will offer a series of guided problems to solidify these concepts, from computing the metric for spheres and tori to understanding [conformal mappings](@entry_id:165890).

## Principles and Mechanisms

The geometry of a surface embedded within a higher-dimensional space, such as a two-dimensional surface in three-dimensional Euclidean space, can be studied from two perspectives. The **[extrinsic geometry](@entry_id:262461)** concerns properties that depend on how the surface is situated in the ambient space, such as its curvature relative to a normal direction. In contrast, the **intrinsic geometry** concerns properties that can be measured by an observer confined to the surface itself, without any reference to the surrounding space. These properties include the lengths of curves, angles between intersecting curves, and the area of regions. The primary tool for quantifying this [intrinsic geometry](@entry_id:158788) is the **first fundamental form**, which is a Riemannian metric induced on the surface by the metric of the ambient space. This chapter delineates the principles and mechanisms governing this fundamental object.

### The Induced Metric as a Pullback

Let us begin with the general setting. Suppose $(N, h)$ is a smooth $k$-dimensional Riemannian manifold, where $h$ is a smooth field of symmetric, positive-definite [bilinear forms](@entry_id:746794)—an inner product—on each [tangent space](@entry_id:141028) $T_qN$. Let $M$ be an $m$-dimensional [smooth manifold](@entry_id:156564) and $X: M \to N$ be a smooth **immersion**, meaning that for every point $p \in M$, the differential (or [pushforward](@entry_id:158718)) $dX_p: T_pM \to T_{X(p)}N$ is an injective [linear map](@entry_id:201112).

How can we endow the manifold $M$ with a metric structure derived from $(N, h)$? The immersion $X$ provides a natural way to do so. For any pair of [tangent vectors](@entry_id:265494) $v, w \in T_pM$, their images under the differential, $dX_p(v)$ and $dX_p(w)$, are vectors in the [tangent space](@entry_id:141028) $T_{X(p)}N$. Since $T_{X(p)}N$ is equipped with the inner product $h_{X(p)}$, we can simply compute the inner product of these pushed-forward vectors. This procedure defines a metric on $M$, known as the **[induced metric](@entry_id:160616)**, which we denote by $g$.

Formally, the [induced metric](@entry_id:160616) $g$ is the **pullback** of the ambient metric $h$ by the immersion $X$, written as $g = X^*h$. At each point $p \in M$, its action on tangent vectors $v, w \in T_pM$ is defined as:
$$ g_p(v,w) = (X^*h)_p(v,w) := h_{X(p)}(dX_p(v), dX_p(w)) $$
[@problem_id:2996618] [@problem_id:2996614]

This definition gives $g$ the structure of a Riemannian metric on $M$. Its [bilinearity](@entry_id:146819) and symmetry are inherited directly from the [bilinearity](@entry_id:146819) and symmetry of $h$. The crucial property of [positive-definiteness](@entry_id:149643), $g_p(v,v) > 0$ for any non-zero vector $v$, is also guaranteed. Since $h$ is positive-definite, $g_p(v,v) = h_{X(p)}(dX_p(v), dX_p(v)) \ge 0$. This value is zero if and only if $dX_p(v) = 0$. However, because $X$ is an immersion, the map $dX_p$ is injective, meaning its kernel is trivial. Thus, $dX_p(v) = 0$ if and only if $v=0$. Consequently, for any non-zero $v \in T_pM$, $g_p(v,v)$ is strictly positive.

### The First Fundamental Form of a Surface in $\mathbb{R}^3$

The classical and most illustrative application of this concept is to a smooth surface $S$ immersed in three-dimensional Euclidean space, $\mathbb{R}^3$. Here, the ambient manifold is $N = \mathbb{R}^3$, and its metric $h$ is the standard Euclidean inner product, $\langle \cdot, \cdot \rangle$. The immersion is a map $X: U \to \mathbb{R}^3$, where $U$ is an open subset of $\mathbb{R}^2$. The [induced metric](@entry_id:160616) on $U$ (and by extension, on the surface $S=X(U)$) is called the **[first fundamental form](@entry_id:274022)**, traditionally denoted by $I$.

Specializing the general definition, the [first fundamental form](@entry_id:274022) at a point $p \in S$ is a bilinear form $I_p$ on the [tangent plane](@entry_id:136914) $T_pS$ that, for any two tangent vectors $v, w \in T_pS$, is given by:
$$ I_p(v,w) = \langle v, w \rangle $$
This simple yet profound statement reveals the true nature of the first fundamental form: it is nothing more than the **restriction of the ambient Euclidean inner product to the [tangent plane](@entry_id:136914) of the surface** [@problem_id:2996627]. This coordinate-free definition makes it evident that the first fundamental form depends only on the [tangent plane](@entry_id:136914) $T_pS$ and the ambient metric, not on any particular choice of [parametrization](@entry_id:272587) used to describe the surface.

Let us now connect this abstract definition to a local coordinate representation. Let the surface be parametrized by $X(u,v)$ for $(u,v) \in U$. The [partial derivatives](@entry_id:146280) with respect to the parameters, $X_u = \frac{\partial X}{\partial u}$ and $X_v = \frac{\partial X}{\partial v}$, are vectors in $\mathbb{R}^3$ that form a basis for the [tangent plane](@entry_id:136914) $T_{X(u,v)}S$. Any [tangent vector](@entry_id:264836) can be expressed as a linear combination of these basis vectors. The components of the first fundamental form in this basis are captured by a $2 \times 2$ matrix whose entries are the inner products of these basis vectors. Following the classical notation of Gauss, these coefficients are:
$$ E = \langle X_u, X_u \rangle = \|X_u\|^2 $$
$$ F = \langle X_u, X_v \rangle $$
$$ G = \langle X_v, X_v \rangle = \|X_v\|^2 $$
The matrix of the [first fundamental form](@entry_id:274022) is thus given by:
$$ [g_{ij}] = \begin{pmatrix} E & F \\ F & G \end{pmatrix} $$
This matrix is precisely the **Gram matrix** of the basis vectors $\{X_u, X_v\}$ [@problem_id:2996629].

### Geometric Interpretation and Applications

The coefficients $E, F, G$ are not merely abstract quantities; they encode the fundamental geometric properties of the surface.

**Arc Length:** Consider an [infinitesimal displacement](@entry_id:202209) on the surface corresponding to a change $(du, dv)$ in the parameters. The corresponding [displacement vector](@entry_id:262782) in the tangent plane is $dX = X_u du + X_v dv$. The squared length of this vector, known as the **[line element](@entry_id:196833)** $ds^2$, is given by its inner product with itself:
$$ ds^2 = \langle dX, dX \rangle = \langle X_u du + X_v dv, X_u du + X_v dv \rangle $$
Expanding this using the [bilinearity](@entry_id:146819) of the inner product yields:
$$ ds^2 = \langle X_u, X_u \rangle du^2 + 2\langle X_u, X_v \rangle du dv + \langle X_v, X_v \rangle dv^2 $$
$$ ds^2 = E\,du^2 + 2F\,du\,dv + G\,dv^2 $$
[@problem_id:2996626] The length of any curve $\gamma(t)$ on the surface can be found by integrating the square root of this expression along the curve: $L(\gamma) = \int \sqrt{ds^2/dt^2} \, dt$.

**Angles:** The coefficients also determine the angle $\theta$ between the coordinate curves (the curves obtained by holding one parameter constant). Since these curves have tangent vectors $X_u$ and $X_v$, the angle between them is given by the standard inner product formula:
$$ \cos\theta = \frac{\langle X_u, X_v \rangle}{\|X_u\|\|X_v\|} = \frac{F}{\sqrt{EG}} $$
The coordinate system is orthogonal at a point if and only if $F=0$ at that point.

**Area:** The area of an infinitesimal parallelogram on the surface spanned by the vectors $X_u du$ and $X_v dv$ is given by the magnitude of their cross product, $\|X_u du \times X_v dv\| = \|X_u \times X_v\| du dv$. Using Lagrange's identity, $\|a \times b\|^2 = \|a\|^2 \|b\|^2 - \langle a, b \rangle^2$, we find:
$$ \|X_u \times X_v\|^2 = \|X_u\|^2 \|X_v\|^2 - \langle X_u, X_v \rangle^2 = EG - F^2 $$
Thus, the infinitesimal [area element](@entry_id:197167) is $dA = \sqrt{EG - F^2} \,du\,dv$. The total area of a region on the surface is found by integrating this quantity over the corresponding parameter domain [@problem_id:2996618]:
$$ \text{Area} = \iint_U \sqrt{EG - F^2} \,du\,dv $$

### Invariance, Transformation, and Regularity

The [first fundamental form](@entry_id:274022) possesses crucial invariance properties. It is **invariant under rigid motions of the ambient space** $\mathbb{R}^3$. If $R: \mathbb{R}^3 \to \mathbb{R}^3$ is an isometry (a rotation followed by a translation), the first fundamental form of the transformed surface $R \circ X$ is identical to that of the original surface $X$. This confirms that the first fundamental form captures the intrinsic "shape" of the surface, independent of its position and orientation in space [@problem_id:2996614].

The first fundamental form is also **independent of [parametrization](@entry_id:272587)**. While the geometric object itself is invariant, its components $E, F, G$ are not; they transform in a systematic way under a change of coordinates. If we change coordinates from $(u^1, u^2)$ to $(\tilde{u}^1, \tilde{u}^2)$, the components $\tilde{g}_{\alpha\beta}$ of the metric in the new system are related to the old components $g_{ij}$ by the tensorial transformation law for a covariant rank-2 tensor:
$$ \tilde{g}_{\alpha\beta} = \sum_{i,j=1}^2 g_{ij} \frac{\partial u^i}{\partial \tilde{u}^\alpha} \frac{\partial u^j}{\partial \tilde{u}^\beta} $$
This transformation ensures that the calculated lengths, angles, and areas remain the same regardless of the coordinate system used [@problem_id:2996605] [@problem_id:2996629].

The quantity $\det(g) = EG - F^2$ has a special transformation property. It is not a [scalar invariant](@entry_id:159606) but a **[scalar density](@entry_id:161438) of weight 2**. Under a coordinate change, it transforms as:
$$ \det(\tilde{g}) = \left(\det\left(\frac{\partial u}{\partial \tilde{u}}\right)\right)^2 \det(g) $$
where $\frac{\partial u}{\partial \tilde{u}}$ is the Jacobian matrix of the [coordinate transformation](@entry_id:138577). This property is precisely what makes the Riemannian [area element](@entry_id:197167), $\mathrm{vol}_g = \sqrt{\det g} \,du^1 \wedge du^2$, a coordinate-invariant object, ensuring that the computed area does not depend on the [parametrization](@entry_id:272587) [@problem_id:2996607].

Finally, the [first fundamental form](@entry_id:274022) provides the test for **regularity**. A parametrization $X(u,v)$ is an immersion at a point if and only if the [tangent vectors](@entry_id:265494) $X_u$ and $X_v$ are linearly independent. This is equivalent to their Gram matrix $[g_{ij}]$ being positive-definite, which in turn is equivalent to its determinant being positive:
$$ EG - F^2 > 0 $$
A point where $EG - F^2 = 0$ is a **singular point** of the parametrization. At such a point, the vectors $X_u$ and $X_v$ become linearly dependent, and the [tangent plane](@entry_id:136914) degenerates from a two-dimensional plane to a line or a single point. The [first fundamental form](@entry_id:274022) ceases to be an inner product at such points [@problem_id:2996616].

### The Role of the First Fundamental Form in Curvature Theory

One of the most profound results in [differential geometry](@entry_id:145818) is Gauss's **Theorema Egregium** (Remarkable Theorem). It states that the Gaussian curvature $K$ of a surface—a measure of its intrinsic "curvedness" at a point—is determined entirely by the first fundamental form and its derivatives.

The curvature of a surface can also be described extrinsically by the **[second fundamental form](@entry_id:161454)** ($II$, with coefficients $L, M, N$), which measures how the surface [normal vector](@entry_id:264185) changes as one moves along the surface. This extrinsic information is encoded in the **[shape operator](@entry_id:264703)** $S$. The Theorema Egregium establishes a direct link between these concepts:
$$ K = \det(S) = \frac{LN - M^2}{EG - F^2} $$
The remarkable fact is that while $L, M, N$ depend on the extrinsic embedding, the specific combination on the right-hand side, the Gaussian curvature $K$, depends only on $E, F, G$ and their first and second derivatives. Therefore, any two surfaces that are **isometric**—that is, they have the same first fundamental form—must have the same Gaussian curvature at corresponding points. For instance, a flat plane ($K=0$) and a cylinder (which can be unrolled into a plane, $K=0$) are locally isometric, even though the cylinder is clearly "curved" in an extrinsic sense (its second fundamental form is non-zero) while the plane is not [@problem_id:2996620].

This leads to the **Fundamental Theorem of Surface Theory**. While the [first fundamental form](@entry_id:274022) $I$ determines the intrinsic geometry, it does not uniquely determine the surface in $\mathbb{R}^3$. To do that, one also needs the second fundamental form $II$. The theorem states that given a metric $I$ and a [symmetric tensor](@entry_id:144567) $II$ on a [simply connected domain](@entry_id:197423), there exists an immersion with these as its fundamental forms if and only if they satisfy a set of compatibility equations (the **Gauss and Codazzi-Mainardi equations**). Furthermore, this immersion is unique up to a [rigid motion](@entry_id:155339) in $\mathbb{R}^3$. In essence, the two fundamental forms, subject to compatibility, provide a complete local description of a surface's geometry, both intrinsic and extrinsic [@problem_id:2996610]. The [first fundamental form](@entry_id:274022) lays the groundwork upon which this entire structure is built.