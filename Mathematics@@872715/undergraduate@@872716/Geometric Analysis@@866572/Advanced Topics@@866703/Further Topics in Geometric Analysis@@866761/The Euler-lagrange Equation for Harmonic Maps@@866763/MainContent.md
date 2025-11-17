## Introduction
Harmonic maps are a central object of study in geometric analysis, representing a natural generalization of geodesics and harmonic functions to the context of maps between Riemannian manifolds. They are not defined by an arbitrary equation, but arise organically as extremals of a fundamental geometric quantity: the Dirichlet energy. This variational perspective provides a powerful framework for understanding their properties and applications. This article demystifies the theory of [harmonic maps](@entry_id:187821) by focusing on their governing partial differential equation. It addresses the fundamental question of what equation a map must satisfy to be a critical point of the energy functional. The journey begins in the "Principles and Mechanisms" chapter, where we will use the calculus of variations to derive the Euler-Lagrange equation for the Dirichlet energy, revealing the crucial role of the [tension field](@entry_id:188540). Following this, the "Applications and Interdisciplinary Connections" chapter will explore the profound impact of this equation, showing how it connects to minimal surfaces, drives [existence and regularity](@entry_id:635920) theory, and appears in theoretical physics. Finally, the "Hands-On Practices" section will provide an opportunity to solidify these concepts by solving concrete problems and analyzing key examples.

## Principles and Mechanisms

In the study of maps between Riemannian manifolds, [harmonic maps](@entry_id:187821) occupy a place of central importance, analogous to that of geodesics in the study of curves or [harmonic functions](@entry_id:139660) in classical analysis. They arise not from an ad-hoc definition, but as the natural outcome of a variational principle. This chapter elucidates the foundational principles and mechanisms that govern [harmonic maps](@entry_id:187821), starting from their definition as critical points of an energy functional and culminating in their governing Euler-Lagrange equation.

### The Variational Principle for Harmonic Maps

The concept of a harmonic map is fundamentally variational. It is a map that extremizes, or is a critical point of, a natural geometric energy.

#### The Dirichlet Energy Functional

Let $(M,g)$ be a compact, oriented Riemannian manifold of dimension $m$, and let $(N,h)$ be another Riemannian manifold of dimension $n$. For any [smooth map](@entry_id:160364) $u: M \to N$, its differential at a point $x \in M$, denoted $\mathrm{d}u_x$, is a [linear map](@entry_id:201112) from the [tangent space](@entry_id:141028) $T_xM$ to the tangent space $T_{u(x)}N$. The metrics $g$ on $M$ and $h$ on $N$ allow us to measure the "stretching" effect of this differential. We define the **energy density** of the map $u$ at $x$ as the squared Hilbert-Schmidt norm of its differential, given by
$$
e(u)(x) = \frac{1}{2}|\mathrm{d}u_x|^2 = \frac{1}{2} \operatorname{trace}_g(u^*h).
$$
In plainer terms, if $\{e_i\}_{i=1}^m$ is a local [orthonormal basis](@entry_id:147779) for $T_xM$, the energy density is the sum of the squared lengths of the images of these basis vectors in $T_{u(x)}N$:
$$
e(u)(x) = \frac{1}{2} \sum_{i=1}^{m} h(\mathrm{d}u_x(e_i), \mathrm{d}u_x(e_i)).
$$
The total **Dirichlet energy** of the map $u$ is obtained by integrating this density over the entire domain manifold $M$:
$$
E(u) = \int_M e(u)(x) \, \mathrm{d}\mu_g = \frac{1}{2} \int_M |\mathrm{d}u|^2 \, \mathrm{d}\mu_g,
$$
where $\mathrm{d}\mu_g$ is the Riemannian volume measure on $(M,g)$. This functional assigns a non-negative real number to each map, quantifying its total "stretching". A constant map, for which $\mathrm{d}u=0$, has zero energy, which is the absolute minimum.

#### Variations and Critical Points

A **[harmonic map](@entry_id:192561)** is defined as a critical point of the Dirichlet [energy functional](@entry_id:170311) $E(u)$. To understand what this means, we employ the calculus of variations. Consider a **smooth variation** of $u$, which is a one-parameter family of maps $u_t: M \to N$ (for $t$ in some interval $(-\varepsilon, \varepsilon)$) such that $u_0 = u$. The "velocity" of this variation at $t=0$ is a vector field $V$ along the map $u$, defined by $V(x) = \left.\frac{\partial u_t(x)}{\partial t}\right|_{t=0}$. Such a $V$ is a section of the [pullback bundle](@entry_id:159346) $u^{-1}TN$. For our purposes, we consider variations that are compactly supported, meaning $u_t(x)=u(x)$ for all $x$ outside a compact set $K \subset M$. This implies the variation field $V$ has [compact support](@entry_id:276214).

A map $u$ is a **critical point** of the energy $E$ if, for every such smooth compactly supported variation $u_t$, the first derivative of the energy vanishes at $t=0$:
$$
\left.\frac{\mathrm{d}}{\mathrm{d}t}\right|_{t=0} E(u_t) = 0.
$$
This is the foundational principle defining a [harmonic map](@entry_id:192561). It is crucial to note that this is a condition on the first derivative only. A critical point is not necessarily a [local minimum](@entry_id:143537) of the energy; it could also be a [local maximum](@entry_id:137813) or, more commonly, a saddle point. The statement that a critical point must be a local minimizer is a common misconception [@problem_id:3047440].

### The Euler-Lagrange Equation: The Tension Field

The condition that the [first variation of energy](@entry_id:635793) vanishes for all admissible variations can be translated, via [integration by parts](@entry_id:136350), into a partial differential equation (PDE) that the map $u$ must satisfy. This PDE is the Euler-Lagrange equation of the [energy functional](@entry_id:170311).

#### Derivation of the First Variation Formula

Let's compute the [first variation](@entry_id:174697) of the energy $E(u_t)$. By differentiating under the integral sign, we obtain:
$$
\left.\frac{\mathrm{d}}{\mathrm{d}t}\right|_{t=0} E(u_t) = \int_M \langle \nabla V, \mathrm{d}u \rangle_h \, \mathrm{d}\mu_g.
$$
Here, $\nabla V$ is the covariant derivative of the variation field $V$ along the map $u$, and the inner product is the natural one on the bundle $T^*M \otimes u^{-1}TN$. To obtain an equation for $u$, we must move the derivative off the arbitrary variation field $V$ and onto the map $u$. This is accomplished using integration by parts, which on a manifold is codified by the Divergence Theorem (or Green's identity). This procedure yields the general **[first variation](@entry_id:174697) formula** [@problem_id:3068612]:
$$
\left.\frac{\mathrm{d}}{\mathrm{d}t}\right|_{t=0} E(u_t) = - \int_M h(\tau(u), V) \, \mathrm{d}\mu_g + \int_{\partial M} h(\mathrm{d}u(\nu), V) \, \mathrm{d}S.
$$
Here, $\nu$ is the outward unit normal to the boundary $\partial M$, $\mathrm{d}S$ is the [volume element](@entry_id:267802) on the boundary, and $\tau(u)$ is a specific vector field along $u$ that results from the [integration by parts](@entry_id:136350). This object, the **[tension field](@entry_id:188540)** of $u$, is the Euler-Lagrange expression for the [energy functional](@entry_id:170311).

#### The Tension Field as the Euler-Lagrange Expression

If the domain manifold $M$ is compact and has no boundary ($\partial M = \emptyset$), the boundary integral vanishes. Similarly, if we consider variations that are fixed on the boundary (a Dirichlet problem), then the variation field $V$ must vanish on $\partial M$, and the boundary integral again vanishes [@problem_id:3068612]. In these common scenarios, the [first variation](@entry_id:174697) formula simplifies to:
$$
\left.\frac{\mathrm{d}}{\mathrm{d}t}\right|_{t=0} E(u_t) = - \int_M h(\tau(u), V) \, \mathrm{d}\mu_g.
$$
The condition that $u$ be a critical point is that this integral must be zero for all admissible compactly supported variation fields $V$. By the fundamental lemma of the calculus of variations, this can only be true if the part of the integrand independent of $V$ is identically zero. Thus, the Euler-Lagrange equation for the Dirichlet energy is simply:
$$
\tau(u) = 0.
$$
A map $u: M \to N$ is harmonic if and only if its [tension field](@entry_id:188540) vanishes everywhere. The [tension field](@entry_id:188540) can be interpreted as the "force" pulling the map towards a configuration of lower energy; a harmonic map is one that is perfectly "in tension," with no [net force](@entry_id:163825) acting on it [@problem_id:3047440] [@problem_id:3068612].

### The Anatomy of the Tension Field in Local Coordinates

To make the condition $\tau(u)=0$ useful for practical computation, we must understand the structure of the [tension field](@entry_id:188540).

#### Invariant Definition and Local Coordinate Expression

Invariantly, the [tension field](@entry_id:188540) is defined as the trace with respect to the metric $g$ of the [second covariant derivative](@entry_id:193368) of the map $u$, denoted $\nabla \mathrm{d}u$:
$$
\tau(u) = \operatorname{trace}_g(\nabla \mathrm{d}u).
$$
Here, $\nabla \mathrm{d}u$ is a [tensor field](@entry_id:266532) that measures how the differential $\mathrm{d}u$ changes from point to point, taking into account the geometry of both the domain $M$ and the target $N$ through their respective Levi-Civita connections [@problem_id:3068867] [@problem_id:3035505].

To compute this in [local coordinates](@entry_id:181200), let $(x^i)$ be coordinates on $M$ and $(y^\alpha)$ be coordinates on $N$. Let $\Gamma^k_{ij}$ be the Christoffel symbols of $(M,g)$ and $\tilde{\Gamma}^\alpha_{\beta\gamma}$ be the Christoffel symbols of $(N,h)$. A detailed calculation based on the definition of the [covariant derivative](@entry_id:152476) on [tensor bundles](@entry_id:203012) shows that the $\alpha$-th component of the [tension field](@entry_id:188540) is given by [@problem_id:3068860] [@problem_id:3035505]:
$$
\tau(u)^\alpha = g^{ij}\Big(\partial_i\partial_j u^\alpha - \Gamma^k_{ij}\,\partial_k u^\alpha + \tilde{\Gamma}^\alpha_{\beta\gamma}(u)\,\partial_i u^\beta\,\partial_j u^\gamma\Big).
$$
The [harmonic map equation](@entry_id:184475) is therefore the system of second-order, [elliptic partial differential equations](@entry_id:141811) $\tau(u)^\alpha = 0$ for $\alpha = 1, \dots, n$.

#### Geometric Interpretation of Terms

The local coordinate formula for the [tension field](@entry_id:188540) can be dissected into two main parts, revealing how the geometry of both the domain and target manifolds contribute [@problem_id:3035505] [@problem_id:3034975].

1.  **The Domain Contribution (The Laplacian Term):** The first part of the expression,
    $$
    g^{ij}(\partial_i\partial_j u^\alpha - \Gamma^k_{ij}\,\partial_k u^\alpha),
    $$
    is precisely the formula for the **Laplace-Beltrami operator** of $(M,g)$ acting on the scalar component function $u^\alpha$. This term, denoted $\Delta_g u^\alpha$, represents the contribution from the geometry of the domain manifold $M$. It corrects the ordinary second partial derivatives for the fact that the coordinate system on $M$ is not generally Cartesian.

2.  **The Target Contribution (The Nonlinear Term):** The second part of the expression,
    $$
    g^{ij}\tilde{\Gamma}^\alpha_{\beta\gamma}(u)\,\partial_i u^\beta\,\partial_j u^\gamma,
    $$
    is a term that is quadratic in the first derivatives of $u$. It arises from the curvature of the target manifold $(N,h)$, as encoded in its Christoffel symbols $\tilde{\Gamma}^\alpha_{\beta\gamma}$. This term measures the tendency of the image of the map to "accelerate" or curve within the target space.

Thus, the [harmonic map equation](@entry_id:184475) $\tau(u)=0$ can be written as:
$$
\Delta_g u^\alpha + g^{ij}\tilde{\Gamma}^\alpha_{\beta\gamma}(u)\,\partial_i u^\beta\,\partial_j u^\gamma = 0.
$$
This reveals that a harmonic map is a solution to a system of nonlinear PDEs, where the nonlinearity arises precisely from the curvature of the target manifold.

### Geometric Interpretations and Fundamental Examples

The abstract equation $\tau(u)=0$ gains considerable intuitive power when examined in specific geometric contexts.

#### Harmonic Maps into Euclidean Space: Harmonic Functions

The simplest case is when the target manifold is Euclidean space, $(N,h) = (\mathbb{R}^k, \delta)$, where $\delta$ is the standard flat metric. In this case, the geometry is trivial, and the Christoffel symbols of the target vanish: $\tilde{\Gamma}^\alpha_{\beta\gamma} = 0$. The nonlinear term in the [tension field](@entry_id:188540) disappears, and the [harmonic map equation](@entry_id:184475) reduces to:
$$
\Delta_g u^\alpha = 0 \quad \text{for } \alpha = 1, \dots, k.
$$
This means that a map into Euclidean space is harmonic if and only if each of its component functions is a **[harmonic function](@entry_id:143397)** on the domain $(M,g)$ [@problem_id:3068612] [@problem_id:3068867]. This demonstrates that the theory of [harmonic maps](@entry_id:187821) is a direct generalization of classical [potential theory](@entry_id:141424).

#### Harmonic Maps from One-Dimensional Domains: Geodesics

Consider the case where the domain is a one-dimensional manifold, such as an interval $(M,g) = (I \subset \mathbb{R}, \mathrm{d}t^2)$. A map $u: I \to N$ is simply a curve $\gamma(t)$ in the target manifold $N$. The domain is flat, so $\Gamma^k_{ij}=0$. The trace operation $\operatorname{trace}_g$ reduces to taking the single component corresponding to the time direction $t$. The [harmonic map equation](@entry_id:184475) $\tau(\gamma)=0$ simplifies to [@problem_id:3047429] [@problem_id:3068867]:
$$
\frac{\mathrm{d}^2\gamma^\alpha}{\mathrm{d}t^2} + \tilde{\Gamma}^\alpha_{\beta\gamma}(\gamma)\,\frac{\mathrm{d}\gamma^\beta}{\mathrm{d}t}\frac{\mathrm{d}\gamma^\gamma}{\mathrm{d}t} = 0.
$$
This is precisely the local coordinate expression for the **[geodesic equation](@entry_id:136555)** on $(N,h)$, which states that the covariant acceleration of the curve is zero: $D_t \dot{\gamma} = 0$. Thus, [harmonic maps](@entry_id:187821) of a 1D domain are exactly the geodesics of the target manifold.

#### Isometric Immersions: Minimal Submanifolds

If the map $u: M^m \to N$ is an [isometric immersion](@entry_id:272242), meaning it preserves lengths of [tangent vectors](@entry_id:265494), then the [tension field](@entry_id:188540) has a profound geometric meaning. It can be shown that the [tension field](@entry_id:188540) of an [isometric immersion](@entry_id:272242) is equal to the dimension of the domain times the **[mean curvature vector](@entry_id:199617)** $H$ of the [immersed submanifold](@entry_id:264923) $u(M) \subset N$:
$$
\tau(u) = mH.
$$
The harmonic map condition $\tau(u)=0$ is therefore equivalent to the condition $H=0$. Submanifolds with vanishing [mean curvature](@entry_id:162147) are known as **[minimal submanifolds](@entry_id:204492)**. These are surfaces that locally minimize area. Therefore, an [isometric immersion](@entry_id:272242) is a harmonic map if and only if its image is a [minimal submanifold](@entry_id:200568) in the target [@problem_id:3068867]. This connects the theory of [harmonic maps](@entry_id:187821) to the classical problem of finding area-minimizing surfaces.

#### A Key Nonlinear Example: Maps into Spheres

A crucial example that illustrates the nonlinearity of the [harmonic map equation](@entry_id:184475) is when the target is a sphere, e.g., $u: \Omega \subset \mathbb{R}^m \to \mathbb{S}^{k-1} \subset \mathbb{R}^k$. The domain $\Omega$ is a flat open set, so the Laplace-Beltrami operator $\Delta_g$ is the standard Laplacian $\Delta$. The target $\mathbb{S}^{k-1}$, however, is curved.

The [harmonic map equation](@entry_id:184475) in this context can be derived via the method of Lagrange multipliers [@problem_id:3068863]. To find a critical point of the energy $E(u) = \frac{1}{2}\int_\Omega |\nabla u|^2 \, dx$ subject to the pointwise constraint $|u(x)|^2 = 1$, one finds that the solution must satisfy $\Delta u = \lambda(x) u$ for some scalar function $\lambda(x)$, which acts as the Lagrange multiplier. This states that the vector $\Delta u$ must be normal to the sphere at every point.

To determine $\lambda(x)$, we differentiate the constraint $|u|^2=1$ twice. This yields the identity $u \cdot \Delta u + |\nabla u|^2 = 0$. Taking the dot product of $\Delta u = \lambda(x) u$ with $u$ gives $u \cdot \Delta u = \lambda(x)|u|^2 = \lambda(x)$. Comparing these two expressions reveals that the Lagrange multiplier must be $\lambda(x) = -|\nabla u(x)|^2$. Substituting this back into the equation gives the celebrated [harmonic map equation](@entry_id:184475) for maps into a sphere [@problem_id:3068869] [@problem_id:3068863]:
$$
\Delta u + |\nabla u|^2 u = 0.
$$
This is a semilinear elliptic PDE, where the nonlinearity $|\nabla u|^2$ arises directly from the curvature of the target sphere.

### Analytical Perspectives: Weak Formulation and Gradient Flow

Beyond the classical differential-geometric viewpoint, the study of [harmonic maps](@entry_id:187821) relies heavily on the tools of partial differential equations and analysis.

#### Weakly Harmonic Maps

To prove existence of solutions, it is often necessary to work in spaces of maps with lower regularity, such as Sobolev spaces. A map $u \in H^1(\Omega, N)$ is a **weakly harmonic map** if it is a critical point of the [energy functional](@entry_id:170311) with respect to variations in the Sobolev space setting. The Euler-Lagrange equation then takes an integral, or weak, form. For a map $u \in H^1(\Omega, \mathbb{S}^{k-1})$, the [criticality condition](@entry_id:201918) with respect to variations $\psi \in C_c^\infty(\Omega, \mathbb{R}^k)$ that are tangential to the sphere (i.e., $\langle \psi, u \rangle = 0$) is [@problem_id:3068861]:
$$
\int_{\Omega} \langle \nabla u, \nabla \psi \rangle \, dx = 0.
$$
By using a projection argument, this can be shown to be equivalent to an equation that must hold for all arbitrary (not necessarily tangential) test functions $\varphi \in C_c^\infty(\Omega, \mathbb{R}^k)$:
$$
\int_{\Omega} \langle \nabla u, \nabla \varphi \rangle \, dx = - \int_{\Omega} |\nabla u|^2 \langle u, \varphi \rangle \, dx.
$$
This is the weak formulation of the equation $\Delta u + |\nabla u|^2 u = 0$. The equivalence of these forms is a cornerstone of the modern analytical theory [@problem_id:3068861].

#### The Harmonic Map Heat Flow

One of the most powerful tools for finding [harmonic maps](@entry_id:187821) is the method of gradient flow. The **[harmonic map heat flow](@entry_id:200511)** is an evolution equation that deforms an initial map $u_0: M \to N$ in the direction of the negative $L^2$-gradient of the energy functional. This evolution equation is given by [@problem_id:3034975]:
$$
\frac{\partial u}{\partial t} = \tau(u).
$$
This is a parabolic system of PDEs. The hope is that as time $t \to \infty$, the solution $u(t)$ will converge to a steady state where $\frac{\partial u}{\partial t}=0$. A steady state must satisfy $\tau(u)=0$, and is therefore a [harmonic map](@entry_id:192561). For maps into manifolds with [non-positive sectional curvature](@entry_id:275356), Eells and Sampson famously used this method to prove that any initial map can be evolved into a unique [harmonic map](@entry_id:192561) in its homotopy class. For functions mapping to $\mathbb{R}$, where $\tau(f) = \Delta_g f$, this flow reduces to the classical heat equation, $\frac{\partial f}{\partial t} = \Delta_g f$ [@problem_id:3034975].