## Introduction
In the study of Riemannian geometry, a fundamental pursuit is to find "optimal" or "canonical" maps between manifolds. The theory of [harmonic maps](@entry_id:187821) provides a powerful framework for this quest by employing the principles of the calculus of variations. At its core, this theory seeks to minimize a quantity known as the Dirichlet energy, a functional that measures the total "stretch" of a map. This approach, however, introduces significant analytical challenges, such as defining energy for non-[smooth maps](@entry_id:203730) and ensuring the [existence and regularity](@entry_id:635920) of energy-minimizers.

This article provides a comprehensive introduction to the energy functional and its [critical points](@entry_id:144653). The first chapter, **Principles and Mechanisms**, will lay the analytical groundwork by defining the Dirichlet energy functional on Sobolev spaces, deriving its Euler-Lagrange equation to define [harmonic maps](@entry_id:187821), and analyzing their stability using the first and second variations. The second chapter, **Applications and Interdisciplinary Connections**, will explore how [harmonic maps](@entry_id:187821) generalize classical concepts like geodesics, connect topology with analysis, and serve as fundamental objects in theoretical physics, highlighting the profound role of curvature in their existence and uniqueness. Finally, **Hands-On Practices** offers concrete problems to solidify understanding of the core computational and theoretical concepts discussed.

## Principles and Mechanisms

### The Dirichlet Energy Functional and Sobolev Maps

At the heart of the theory of [harmonic maps](@entry_id:187821) lies a variational principle. We seek maps between two Riemannian manifolds, $(M, g)$ and $(N, h)$, that are "optimal" in a certain sense. The standard measure of optimality is the **Dirichlet energy** (or simply, energy) of a map $u: M \to N$. For a [smooth map](@entry_id:160364), this energy is defined as the integral of its pointwise energy density over the domain manifold $M$:

$$
E(u) = \frac{1}{2} \int_M |du|^2_x \, d\mathrm{vol}_g
$$

Here, $d\mathrm{vol}_g$ is the volume element induced by the metric $g$ on $M$. The term $|du|^2_x$ represents the squared Hilbert-Schmidt norm of the differential of the map, $du_x: T_xM \to T_{u(x)}N$, at a point $x \in M$. This norm is computed using the metrics of both manifolds. If $\{e_i\}$ is a local [orthonormal basis](@entry_id:147779) for $T_xM$, then the energy density is given by $|du|^2_x = \sum_i |du_x(e_i)|_h^2$, where $|\cdot|_h$ is the norm on $T_{u(x)}N$ induced by the metric $h$.

A fundamental property of the energy functional is its [geometric invariance](@entry_id:637068). It is defined intrinsically using the Riemannian structures of the domain and target. A practical consequence of this is that its value does not depend on any particular [coordinate systems](@entry_id:149266) used for computation, nor on how the target manifold $(N,h)$ might be realized as a submanifold of a larger Euclidean space [@problem_id:3068578]. For instance, if we consider $(N,h)$ to be isometrically embedded in a Euclidean space $\mathbb{R}^k$, the energy computed for a map $u: M \to N \subset \mathbb{R}^k$ is independent of the choice of this embedding. This is because the metric $h$ on the tangent spaces of $N$ is precisely the one inherited from the ambient Euclidean metric, which is all that is required to compute the norm $|du|^2_x$.

The [calculus of variations](@entry_id:142234), however, requires a functional-analytic setting that is more general than the space of [smooth maps](@entry_id:203730). To guarantee the [existence of minimizers](@entry_id:199472), we need a space of maps that is complete with respect to a suitable norm. This leads us to the **Sobolev space of maps**, denoted $W^{1,2}(M,N)$. Informally, this space consists of maps from $M$ to $N$ that are square-integrable and whose first derivatives are also square-integrable in a "weak" sense.

The definition of the weak differential, $du$, for a map between manifolds can be made precise in two equivalent ways [@problem_id:3068620].
1.  **Intrinsic Definition via Charts:** We can cover $M$ and $N$ with local [coordinate charts](@entry_id:262338). For a map $u$, its local representative $u_{loc}$ is a map between open sets in Euclidean spaces, e.g., $u_{loc}: \mathbb{R}^m \supset U \to V \subset \mathbb{R}^n$. We say $u \in W^{1,2}(M,N)$ if all such local representatives belong to the standard Sobolev space $W^{1,2}(U,V)$. The weak differential $du$ is then assembled from the weak Jacobians of these local maps, using the appropriate transformation rules involving the derivatives of the chart maps.
2.  **Extrinsic Definition via Embedding:** By the Nash Embedding Theorem, any Riemannian manifold $(N,h)$ can be isometrically embedded in some Euclidean space $\mathbb{R}^k$. We can then define $W^{1,2}(M,N)$ as the set of maps $u: M \to \mathbb{R}^k$ in the standard Sobolev space $W^{1,2}(M,\mathbb{R}^k)$ whose image lies in $N$ [almost everywhere](@entry_id:146631). The weak differential $DU$ of $u$ as a map into $\mathbb{R}^k$ is a section of $T^*M \otimes \mathbb{R}^k$. The intrinsic differential $du$ is then recovered by orthogonally projecting $DU$ onto the tangent bundle of $N$. That is, for almost every $x \in M$, $du_x = \Pi_{u(x)} \circ DU_x$, where $\Pi_{u(x)}: \mathbb{R}^k \to T_{u(x)}N$ is the projection. Crucially, the resulting object $du$ and the energy $E(u)$ are independent of the choice of [isometric embedding](@entry_id:152303).

The Sobolev framework is powerful precisely because it does not require maps to be continuous. The space $W^{1,2}(M,N)$ is well-defined even for maps that are only defined "[almost everywhere](@entry_id:146631)" [@problem_id:3068620]. When the target manifold is simply Euclidean space, $(N,h) = (\mathbb{R}^n, \delta)$, where $\delta$ is the standard metric, both of these general definitions reduce to the familiar notion of a vector-valued function whose components have weak [partial derivatives](@entry_id:146280) that are square-integrable [@problem_id:3068620].

### The First Variation and Harmonic Maps

The central principle of the [calculus of variations](@entry_id:142234) is that a map which minimizes (or, more generally, is a critical point of) the energy functional must satisfy the associated **Euler-Lagrange equation**. This equation is found by computing the **[first variation](@entry_id:174697)** of the energy, which measures how the energy changes under infinitesimal perturbations of the map.

An **admissible variation** of a map $u: M \to N$ is a smooth one-parameter family of maps $u_t: M \to N$, defined for $t$ in a small interval around $0$, such that $u_0 = u$. The infinitesimal change at $t=0$ is captured by the **variational vector field** $V(x) = \left.\frac{d}{dt}\right|_{t=0} u_t(x)$. Since each $u_t(x)$ is a curve in $N$, its velocity vector $V(x)$ must be a [tangent vector](@entry_id:264836) to $N$ at the point $u_0(x) = u(x)$. Thus, $V$ is a section of the pullback tangent bundle $u^{-1}TN$. In many problems, such as the Dirichlet problem, we seek a minimizer with prescribed boundary values. If $u$ is required to match a given map $\phi$ on the boundary $\partial M$, then any admissible variation $u_t$ must also satisfy $u_t|_{\partial M} = \phi$ for all $t$. This implies that the variational vector field must vanish on the boundary: $V|_{\partial M} = 0$ [@problem_id:3068611]. A powerful method to construct such variations is to embed $N$ in $\mathbb{R}^k$ and consider variations of the form $u_t = \pi(u+tW)$, where $W: M \to \mathbb{R}^k$ is an ambient vector field with $W|_{\partial M}=0$ and $\pi$ is the nearest-point projection onto $N$ [@problem_id:3068611].

The condition for $u$ to be a critical point is that the [first variation of energy](@entry_id:635793) vanishes for all admissible variations: $\left.\frac{d}{dt}\right|_{t=0} E(u_t) = 0$. A direct calculation shows that the [first variation](@entry_id:174697) can be expressed as an integral involving the differential of the map $u$ and the [covariant derivative](@entry_id:152476) of the variation field $V$ [@problem_id:3068593]:
$$
\left.\frac{d}{dt}\right|_{t=0} E(u_t) = \int_M \langle du, \nabla V \rangle \, d\mathrm{vol}_g = 0
$$
This is the **weak formulation** of the Euler-Lagrange equation. The inner product $\langle \cdot, \cdot \rangle$ here is on the bundle $T^*M \otimes u^{-1}TN$. This formulation is particularly important in the Sobolev space setting, where maps may not be smooth enough for the strong form of the equation to hold everywhere.

By applying integration by parts (more precisely, the [divergence theorem on manifolds](@entry_id:190198)), we can shift the derivative from the variation field $V$ onto the differential $du$. Assuming for simplicity that $M$ is compact and has no boundary (or that $V$ vanishes on the boundary), the [first variation](@entry_id:174697) becomes [@problem_id:3068612] [@problem_id:3068616]:
$$
\left.\frac{d}{dt}\right|_{t=0} E(u_t) = -\int_M \langle \tau(u), V \rangle_h \, d\mathrm{vol}_g
$$
This calculation naturally introduces a crucial geometric object: the **[tension field](@entry_id:188540)** of the map $u$, denoted $\tau(u)$. The [tension field](@entry_id:188540) is defined as the trace of the [second covariant derivative](@entry_id:193368) of $u$:
$$
\tau(u) = \mathrm{trace}_g(\nabla du)
$$
Here, $\nabla du$ is the [covariant derivative](@entry_id:152476) of the section $du \in \Gamma(T^*M \otimes u^{-1}TN)$, taken with respect to the Levi-Civita connections on both $(M,g)$ and $(N,h)$.

The [first variation](@entry_id:174697) formula reveals the profound geometric meaning of the [tension field](@entry_id:188540): it is the negative of the **$L^2$-gradient** of the [energy functional](@entry_id:170311) [@problem_id:3068559]. In the [infinite-dimensional space](@entry_id:138791) of maps, the [tension field](@entry_id:188540) points in the direction of the steepest descent for the energy.

For the [first variation](@entry_id:174697) to be zero for all admissible variations $V$, the fundamental lemma of calculus of variations implies that the integrand must be identically zero. Therefore, the Euler-Lagrange equation for the energy functional is simply:
$$
\tau(u) = 0
$$
A [smooth map](@entry_id:160364) $u: M \to N$ that satisfies this equation is called a **harmonic map**. Thus, [harmonic maps](@entry_id:187821) are precisely the smooth [critical points](@entry_id:144653) of the Dirichlet energy functional [@problem_id:3068612].

In [local coordinates](@entry_id:181200) $(x^i)$ on $M$ and $(y^\alpha)$ on $N$, the [harmonic map equation](@entry_id:184475) takes the form of a system of second-order, quasi-[linear partial differential equations](@entry_id:171085) [@problem_id:3068616]:
$$
g^{ij}\left( \frac{\partial^2 u^\alpha}{\partial x^i \partial x^j} - \Gamma^k_{ij} \frac{\partial u^\alpha}{\partial x^k} + \tilde{\Gamma}^\alpha_{\beta\gamma}(u) \frac{\partial u^\beta}{\partial x^i} \frac{\partial u^\gamma}{\partial x^j} \right) = 0 \quad \text{for each } \alpha
$$
Here, $g^{ij}$ are the components of the [inverse metric](@entry_id:273874) on $M$, while $\Gamma^k_{ij}$ and $\tilde{\Gamma}^\alpha_{\beta\gamma}$ are the Christoffel symbols of the connections on $M$ and $N$, respectively. The first two terms represent the action of the Laplace-Beltrami operator on each component function $u^\alpha$, while the third, non-linear term involves the geometry of the target manifold $N$.

If the target manifold is Euclidean space $(\mathbb{R}^n, \delta)$, its Christoffel symbols are zero, and the [harmonic map equation](@entry_id:184475) simplifies significantly to the linear system $\Delta_g u = 0$, where $\Delta_g$ is the Laplace-Beltrami operator on $(M,g)$. In this case, a map is harmonic if and only if each of its component functions is a harmonic function on $M$ [@problem_id:3068616]. It is critical, however, not to confuse the intrinsic condition $\tau(u)=0$ with the condition that the ambient Laplacian vanishes. If $u$ is a [harmonic map](@entry_id:192561) into a curved [submanifold](@entry_id:262388) $N \subset \mathbb{R}^k$, it is generally *not* true that $\Delta_g u = 0$ in the [ambient space](@entry_id:184743). The ambient Laplacian will have a component normal to $N$, which is dictated by the second fundamental form of $N$ in $\mathbb{R}^k$ [@problem_id:3068578].

### The Second Variation and Stability

Once a critical point—a [harmonic map](@entry_id:192561)—has been found, the next natural question is to determine its nature. Is it a local minimum, a local maximum, or a saddle point of the energy functional? This is answered by examining the **second variation** of energy. For a harmonic map $u$, the second variation in the direction of a variational field $V$ is given by $\delta^2 E(u)[V,V] = \left.\frac{d^2}{dt^2}\right|_{t=0} E(u_t)$.

A detailed calculation reveals a beautiful formula that connects the stability of the map to the geometry of the domain and, particularly, the target. For a [harmonic map](@entry_id:192561) $u$ on a [compact domain](@entry_id:139725) $M$ without boundary, the second variation is given by [@problem_id:3068625]:
$$
\delta^2 E(u)[V,V] = \int_M \left( |\nabla V|^2 - \langle \mathrm{tr}_g(R^N(V,du)du), V \rangle_h \right) \, d\mathrm{vol}_g
$$
The first term, $|\nabla V|^2 = \sum_i |\nabla_{e_i} V|_h^2$, is the squared norm of the covariant derivative of the variation field. It is always non-negative and can be seen as the energy of the variation itself. The second term involves the Riemann [curvature tensor](@entry_id:181383) $R^N$ of the target manifold. It couples the variation field $V$ with the differential of the map $du$, weighted by the curvature of $N$. This term can be positive or negative and reflects how the curvature of the [target space](@entry_id:143180) affects the energy of nearby maps. For instance, if the target manifold has negative sectional curvature, the curvature term tends to be positive, which reinforces the positivity of the whole expression.

A harmonic map $u$ is said to be **stable** if its second variation is non-negative for all admissible variations $V$:
$$
\delta^2 E(u)[V,V] \ge 0
$$
Geometrically, a stable [harmonic map](@entry_id:192561) is a local minimizer of energy, at least to second order [@problem_id:3068565]. This condition is analogous to the [second derivative test](@entry_id:138317) in ordinary calculus.

The [second variation formula](@entry_id:180586) defines a [symmetric bilinear form](@entry_id:148281), often called the [index form](@entry_id:183467), which can be represented by a self-adjoint elliptic [differential operator](@entry_id:202628) $J$ acting on sections of $u^{-1}TN$, known as the **Jacobi operator**. The stability condition $\delta^2 E(u)[V,V] \ge 0$ is equivalent to the Jacobi operator being a non-negative operator, which means all of its eigenvalues must be non-negative. The number of negative eigenvalues of $J$ is called the **Morse index** of the [harmonic map](@entry_id:192561). Therefore, a [harmonic map](@entry_id:192561) is stable if and only if its Morse index is zero [@problem_id:3068565]. It is important to note that stability allows for the possibility of zero eigenvalues, corresponding to directions of variation (Jacobi fields) along which the energy does not change to second order. This is a weaker condition than strict stability, which would require $\delta^2 E(u)[V,V] > 0$ for all non-zero $V$. Consequently, a stable harmonic map is not necessarily an isolated energy minimizer; for example, any constant map is stable but is part of a continuous family of maps with the same minimal energy of zero [@problem_id:3068565].

### A Fundamental Computational Tool: The Bochner Identity

A cornerstone of the analytical study of [harmonic maps](@entry_id:187821) is a powerful computational formula known as the **Bochner identity**. This identity relates the Laplacian of the energy density $|du|^2$ to the geometry of the map and the curvatures of the manifolds involved. For any smooth [harmonic map](@entry_id:192561) $u: (M,g) \to (N,h)$, the identity is [@problem_id:3068600]:
$$
\frac{1}{2}\Delta_g |du|^2 = |\nabla du|^2 + \sum_{i,j} \mathrm{Ric}^M(e_i, e_j) \langle du(e_i), du(e_j) \rangle - \sum_{i,j} \langle R^N(du(e_i), du(e_j))du(e_i), du(e_j) \rangle
$$
Let us dissect this formula:
- $\Delta_g |du|^2$ is the Laplace-Beltrami operator on $M$ acting on the scalar function given by the energy density of the map.
- $|\nabla du|^2$ is the squared Hilbert-Schmidt norm of the [second covariant derivative](@entry_id:193368) of $u$. This term is always non-negative and measures how far the map is from being **[totally geodesic](@entry_id:183906)** (a condition where $\nabla du = 0$).
- The term involving $\mathrm{Ric}^M$ is a coupling between the Ricci curvature of the domain $M$ and the differential of the map.
- The final term involves the sectional curvatures of the target manifold $N$ on the 2-planes spanned by pairs of vectors in the image of $du$.

The Bochner identity is a type of Weitzenböck formula and is derived by a careful commutation of covariant derivatives. Its power lies in providing a differential equation for the energy density itself. On a [compact domain](@entry_id:139725) $M$, we can integrate this identity and apply the maximum principle. For example, if $M$ has non-negative Ricci curvature and $N$ has [non-positive sectional curvature](@entry_id:275356), then every term on the right-hand side is non-negative. Integrating over the [compact manifold](@entry_id:158804) $M$ shows that the integral of $\Delta_g |du|^2$ is non-negative, but by the divergence theorem, this integral is zero. This forces all terms on the right-hand side to be zero everywhere. In particular, it forces $|\nabla du|^2 = 0$, implying that the map must be [totally geodesic](@entry_id:183906). This is a classic example of a rigidity theorem derived from the Bochner identity.

### Core Analytical Themes: Existence and Regularity

This chapter has focused on the principles defining [harmonic maps](@entry_id:187821) and analyzing their properties. Two deeper analytical questions underpin the entire theory: [existence and regularity](@entry_id:635920).

**Existence:** Does a harmonic map always exist, for instance, one that satisfies a given boundary condition? A primary tool for proving existence is the **direct method in the calculus of variations**. The strategy is to take a sequence of maps $\{u_j\}$ whose energies approach the [infimum](@entry_id:140118) energy, and then show that a subsequence converges to a limit map $u$ which achieves this [infimum](@entry_id:140118). The key ingredient for this method to work is a compactness property. For maps between Riemannian manifolds, it can be shown that if $M$ and $N$ are compact, any sequence $\{u_j\}$ in $W^{1,2}(M,N)$ with uniformly bounded energy admits a subsequence that converges weakly in $W^{1,2}$ and strongly in $L^2$ to a limit map $u \in W^{1,2}(M,N)$ [@problem_id:3068578]. This weak limit is a candidate for an energy-minimizing map.

**Regularity:** The direct method yields a minimizer $u$ in the Sobolev space $W^{1,2}(M,N)$. Such a map is a weak solution to the [harmonic map equation](@entry_id:184475), but it is not a priori smooth. The question of **regularity** asks: is this weak solution actually a classical, smooth harmonic map? The answer is subtle and dimension-dependent. For domain dimension $m=2$, any energy-minimizing map is indeed smooth. However, for dimensions $m \ge 3$, this is no longer true. There exist examples of energy-minimizing maps that are not continuous, but have a [finite set](@entry_id:152247) of point singularities. The study of the formation and structure of these singularities is a deep and active area of research in [geometric analysis](@entry_id:157700) [@problem_id:3068578].