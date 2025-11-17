## Introduction
In the study of geometric analysis, a central task is to find "canonical" or "best" maps between two [curved spaces](@entry_id:204335), or Riemannian manifolds. Just as geodesics represent the straightest possible paths within a single manifold, [harmonic maps](@entry_id:187821) provide a natural generalization to the setting of functions between manifolds. They are defined via a [variational principle](@entry_id:145218) as the [critical points](@entry_id:144653) of the Dirichlet energy, an integral that measures the total distortion or "stretch" of a map. This principle gives rise to the [harmonic map equation](@entry_id:184475), a challenging system of semilinear [elliptic partial differential equations](@entry_id:141811) whose solutions exhibit a remarkably rich and complex structure. Understanding these solutions addresses the fundamental problem of how the geometry of the domain and target manifolds influences the existence, smoothness, and behavior of mappings between them.

This article provides a comprehensive exploration of this foundational topic. In the first chapter, **Principles and Mechanisms**, we will lay the theoretical groundwork by defining the Dirichlet energy, deriving the [harmonic map equation](@entry_id:184475), and investigating the core analytical challenges of [existence and regularity](@entry_id:635920), including the celebrated partial regularity theorem and the phenomenon of "bubbling." Next, in **Applications and Interdisciplinary Connections**, we will see how this abstract theory provides powerful tools and insights in other fields, revealing deep connections to [conformal geometry](@entry_id:186351), [minimal surface](@entry_id:267317) theory, and physics. Finally, the **Hands-On Practices** section offers a set of targeted problems designed to solidify your understanding by applying the core concepts to concrete, instructive examples. Together, these chapters will build a robust picture of [harmonic maps](@entry_id:187821) as a central and unifying concept in modern geometry.

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms governing the theory of [harmonic maps](@entry_id:187821). We will begin by precisely defining the central object of study, the Dirichlet [energy functional](@entry_id:170311), and derive its Euler-Lagrange equation, which defines the [harmonic map](@entry_id:192561). Subsequently, we will explore the fundamental questions of [existence and regularity](@entry_id:635920) of solutions, leading us to the rich analytical structure of the theory, including the direct method of [calculus of variations](@entry_id:142234), the challenge of singularities, and the remarkable phenomenon of bubbling. Finally, we will introduce the related concepts of the [harmonic map heat flow](@entry_id:200511) and the stability of [harmonic maps](@entry_id:187821).

### The Dirichlet Energy Functional

The concept of a harmonic map arises from a variational principle. We consider a [smooth map](@entry_id:160364) $u: (M,g) \to (N,h)$ between two Riemannian manifolds. The map $u$ can be thought of as "stretching" the manifold $M$ as it maps it into $N$. The Dirichlet energy, $E(u)$, is a functional that quantifies the total "stretching" or distortion produced by the map. It is defined as the integral of an energy density over the domain manifold $M$:

$$
E(u) = \frac{1}{2} \int_M |du|^2 \, \mathrm{dvol}_g
$$

Here, $\mathrm{dvol}_g$ is the Riemannian volume form of the metric $g$ on $M$, and $|du|^2$ is the pointwise squared norm of the differential of $u$. The differential at a point $x \in M$, denoted $du_x$, is a linear map from the [tangent space](@entry_id:141028) of the domain to the tangent space of the target: $du_x: T_xM \to T_{u(x)}N$. The metrics $g_x$ and $h_{u(x)}$ equip these [tangent spaces](@entry_id:199137) with inner products, allowing us to define the norm of this [linear map](@entry_id:201112).

There are several equivalent ways to define the energy density $|du|^2$, each offering a different geometric or algebraic perspective [@problem_id:3035482].

One fundamental definition views $|du|^2$ as the squared **Hilbert-Schmidt norm** of the differential $du_x$. For any $g_x$-[orthonormal basis](@entry_id:147779) $\{e_i\}_{i=1}^m$ of $T_xM$, this is given by the sum of the squared lengths of the images of the basis vectors in the target tangent space:
$$
|du|^2(x) = \sum_{i=1}^m h_{u(x)}(du_x(e_i), du_x(e_i))
$$
This definition transparently shows that the energy density measures the average stretching of lengths by the map.

A more intrinsic formulation involves the **pullback tensor**. The map $u$ pulls back the metric $h$ on $N$ to a symmetric $(0,2)$-tensor $u^*h$ on $M$. This tensor is defined for [vector fields](@entry_id:161384) $X, Y$ on $M$ by $(u^*h)_x(X, Y) = h_{u(x)}(du_x X, du_x Y)$. The energy density is then simply the trace of this pullback tensor with respect to the domain metric $g$:
$$
|du|^2(x) = \operatorname{tr}_g((u^*h)_x)
$$
This expression highlights how the energy density compares the geometry induced by the map ($u^*h$) with the intrinsic geometry of the domain ($g$).

In [local coordinates](@entry_id:181200), these invariant definitions take on a more concrete form. Let $(x^i)$ be [local coordinates](@entry_id:181200) on $M$ and $(y^\alpha)$ be [local coordinates](@entry_id:181200) on $N$. The metrics are given by their component matrices $g_{ij}(x)$ and $h_{\alpha\beta}(y)$, and the map is represented by functions $u^\alpha(x) = y^\alpha \circ u(x)$. The energy density becomes:
$$
|du|^2(x) = g^{ij}(x) h_{\alpha\beta}(u(x)) \frac{\partial u^\alpha}{\partial x^i} \frac{\partial u^\beta}{\partial x^j}
$$
Here, $g^{ij}$ is the inverse of the metric matrix $g_{ij}$, and the Einstein [summation convention](@entry_id:755635) is used. This formula is invaluable for calculations and for analyzing the [partial differential equations](@entry_id:143134) associated with [harmonic maps](@entry_id:187821).

Finally, a useful operator-theoretic viewpoint involves the **metric adjoint** of the differential. For each $x \in M$, the [adjoint map](@entry_id:191705) $du_x^*: T_{u(x)}N \to T_xM$ is defined by the relation $g_x(v, du_x^* w) = h_{u(x)}(du_x v, w)$ for all $v \in T_xM$ and $w \in T_{u(x)}N$. It is a standard result from linear algebra that the squared Hilbert-Schmidt norm of a linear map $L$ can be expressed as either $\operatorname{tr}(L^*L)$ or $\operatorname{tr}(LL^*)$. Applying this to $du_x$, we get two equivalent expressions for the energy density:
$$
|du|^2(x) = \operatorname{tr}_g(du_x^* \circ du_x) = \operatorname{tr}_h(du_x \circ du_x^*)
$$
The operator $du_x^* \circ du_x$ is a self-adjoint endomorphism of $T_xM$, while $du_x \circ du_x^*$ is a self-adjoint endomorphism of $T_{u(x)}N$. This duality will reappear in various contexts throughout the theory.

### The Harmonic Map Equation

A map $u: M \to N$ is defined to be a **[harmonic map](@entry_id:192561)** if it is a critical point of the Dirichlet energy functional $E(u)$. That is, for any smooth one-parameter variation of maps $u_t: M \to N$ with $u_0 = u$ and with the variation fixing the boundary values (if $M$ has a boundary), the [first variation of energy](@entry_id:635793) vanishes:
$$
\left.\frac{d}{dt}\right|_{t=0} E(u_t) = 0
$$

The calculation of this [first variation](@entry_id:174697) yields the Euler-Lagrange equation for the [energy functional](@entry_id:170311). Let $V = \left.\frac{d}{dt}\right|_{t=0} u_t$ be the variation vector field along $u$, which is a section of the [pullback bundle](@entry_id:159346) $u^{-1}TN$. A standard calculation involving integration by parts (Green's identity on manifolds) shows that the [first variation](@entry_id:174697) is given by:
$$
\left.\frac{d}{dt}\right|_{t=0} E(u_t) = - \int_M \langle \tau(u), V \rangle_h \, \mathrm{dvol}_g
$$
(Here we assume $M$ is compact without boundary, or that the variation $V$ is compactly supported in the interior of $M$, so that boundary terms vanish.)

For the [first variation](@entry_id:174697) to be zero for all admissible variations $V$, the fundamental lemma of calculus of variations implies that the term multiplying $V$ in the integrand must be identically zero. This gives rise to the **[harmonic map equation](@entry_id:184475)**:
$$
\tau(u) = 0
$$

The quantity $\tau(u)$ is known as the **[tension field](@entry_id:188540)** of the map $u$. It is a vector field along the map $u$, i.e., a section of the [pullback bundle](@entry_id:159346) $u^{-1}TN$. Invariantly, the [tension field](@entry_id:188540) is defined as the trace of the [second covariant derivative](@entry_id:193368) of $u$ [@problem_id:3035496]:
$$
\tau(u) = \operatorname{trace}_g(\nabla du)
$$
Here, $\nabla$ is the connection on the tensor bundle $T^*M \otimes u^{-1}TN$, induced by the Levi-Civita connections on $(M,g)$ and $(N,h)$.

To understand the structure of this equation, it is instructive to derive its local coordinate expression [@problem_id:3035505]. Let $\Gamma^k_{ij}$ be the Christoffel symbols of $(M,g)$ and $\tilde{\Gamma}^\alpha_{\beta\gamma}$ be the Christoffel symbols of $(N,h)$. The $\alpha$-th component of the [tension field](@entry_id:188540), $\tau^\alpha(u)$, is given by:
$$
\tau^\alpha(u) = g^{ij} \left( \frac{\partial^2 u^\alpha}{\partial x^i \partial x^j} - \Gamma^k_{ij} \frac{\partial u^\alpha}{\partial x^k} + \tilde{\Gamma}^\alpha_{\beta\gamma}(u) \frac{\partial u^\beta}{\partial x^i} \frac{\partial u^\gamma}{\partial x^j} \right)
$$
This expression reveals the geometric origins of the equation.
1.  The term $g^{ij} \left( \frac{\partial^2 u^\alpha}{\partial x^i \partial x^j} - \Gamma^k_{ij} \frac{\partial u^\alpha}{\partial x^k} \right)$ is precisely the coordinate expression for the **Laplace-Beltrami operator** on $M$ acting on the component function $u^\alpha$, denoted $\Delta_M u^\alpha$. This part of the equation is linear in $u$ and arises from the geometry of the domain manifold.
2.  The term $g^{ij} \tilde{\Gamma}^\alpha_{\beta\gamma}(u) \frac{\partial u^\beta}{\partial x^i} \frac{\partial u^\gamma}{\partial x^j}$ is a nonlinear term that is quadratic in the first derivatives of $u$. This term arises from the curvature of the target manifold, as encoded by its Christoffel symbols.

The full [harmonic map equation](@entry_id:184475) can thus be written as:
$$
\tau(u) = \Delta_M u + \operatorname{Tr}_g(\tilde{\Gamma}(u)(du, du)) = 0
$$
This is a system of second-order, semilinear [elliptic partial differential equations](@entry_id:141811). If the target manifold $(N,h)$ is flat (e.g., Euclidean space $\mathbb{R}^n$), then its Christoffel symbols are zero, and the [harmonic map equation](@entry_id:184475) reduces to the familiar Laplace equation $\Delta_M u = 0$, which must be satisfied by each component of $u$. For a general curved target, however, the nonlinear term makes the equation significantly more complex.

### Existence of Harmonic Maps: The Variational Approach

Once the [harmonic map equation](@entry_id:184475) is established, a fundamental question is whether solutions exist. Given a domain $(M,g)$, a target $(N,h)$, and perhaps some boundary conditions or a specified homotopy class, can we find a harmonic map? The primary method for proving existence is the **direct method in the [calculus of variations](@entry_id:142234)**. The goal is to find a map that minimizes the Dirichlet energy within a given class of admissible maps; such a minimizer will automatically be a critical point and thus a harmonic map.

This approach requires moving from the smooth setting of $C^\infty$ maps to a functional-analytic framework based on Sobolev spaces. A map $u: M \to N$ is said to be in the Sobolev space $W^{1,2}(M, N)$ if, after an [isometric embedding](@entry_id:152303) $N \hookrightarrow \mathbb{R}^K$, the resulting $\mathbb{R}^K$-valued map has components in the standard Sobolev space $W^{1,2}(M)$. The [energy functional](@entry_id:170311) $E(u)$ is well-defined for such maps.

A map $u \in W^{1,2}(M,N)$ is a **weakly harmonic map** if it satisfies the Euler-Lagrange equation in an integral sense. This means that for every compactly supported smooth test section $\varphi \in C_c^\infty(u^{-1}TN)$, we have [@problem_id:3035485]:
$$
\int_M \langle du, d\varphi \rangle \, \mathrm{dvol}_g = 0
$$
By [integration by parts](@entry_id:136350), this is equivalent to stating that the [tension field](@entry_id:188540) vanishes in the sense of distributions: $\int_M \langle \tau(u), \varphi \rangle \, \mathrm{dvol}_g = 0$.

The direct method to find an energy minimizer proceeds in three steps [@problem_id:3035491]:
1.  **Minimizing Sequence**: Take a sequence of maps $\{u_j\}$ in the desired admissible class (e.g., a fixed homotopy class with prescribed boundary data) such that their energies converge to the infimum of the energy in that class: $E(u_j) \to \inf E$.
2.  **Convergence**: Show that this sequence has a subsequence that converges to a limit map $u$. Since the energy bounds the $W^{1,2}$-norm, we can typically only expect **weak convergence** in $W^{1,2}$ and strong convergence in $L^2$.
3.  **Lower Semicontinuity and Closure**: Show that the limit map $u$ remains in the admissible class and that the energy of the limit is no greater than the limit of the energies: $E(u) \le \liminf E(u_j)$.

If all three steps are successful, one concludes that $u$ is an energy minimizer and therefore a weakly [harmonic map](@entry_id:192561). However, step 2 and step 3 present a major obstacle. Weak convergence in $W^{1,2}$ is generally not strong enough to ensure that the limit map $u$ stays in the same homotopy class as the sequence $\{u_j\}$. Topological information can be lost in the weak limit through a phenomenon known as **bubbling**, which we will explore later.

Fortunately, there are important geometric conditions under which this problem can be overcome. A celebrated theorem, originating with Eells and Sampson, asserts that if the target manifold $(N,h)$ has **[non-positive sectional curvature](@entry_id:275356)**, the direct method works [@problem_id:3035493]. The [non-positive curvature](@entry_id:203441) of the target endows the [energy functional](@entry_id:170311) with certain [convexity](@entry_id:138568) properties. This ensures that any minimizing sequence is in fact precompact in the strong $W^{1,2}$ topology. Strong convergence is sufficient to preserve the homotopy class, allowing the direct method to succeed and prove the existence of an energy-minimizing [harmonic map](@entry_id:192561) in any given homotopy class. Another significant result, by Schoen and Uhlenbeck, shows that the direct method also works if the dimension of the domain is $m \ge 3$, regardless of the target's curvature [@problem_id:3035491].

### Regularity and Singularities of Harmonic Maps

Even when the [variational method](@entry_id:140454) yields a [weak solution](@entry_id:146017) $u \in W^{1,2}(M,N)$, it is not immediately clear if this solution is a [smooth map](@entry_id:160364). The study of the smoothness of [weak solutions](@entry_id:161732) is known as **[regularity theory](@entry_id:194071)**. For a nonlinear system like the [harmonic map equation](@entry_id:184475), solutions may not be smooth everywhere; they can develop singularities.

The groundbreaking work of Schoen and Uhlenbeck on energy-minimizing maps, later extended by Evans and Bethuel to the broader class of **stationary [harmonic maps](@entry_id:187821)** ([critical points](@entry_id:144653) with respect to domain variations as well as map variations), established a beautiful **partial regularity theorem** [@problem_id:3035492]. The theorem states that a stationary [harmonic map](@entry_id:192561) is smooth [almost everywhere](@entry_id:146631). More precisely, the set of points where the map is not smooth, called the **[singular set](@entry_id:187696)** $\Sigma$, is a [closed set](@entry_id:136446) of small dimension.

**Partial Regularity Theorem**: Let $u \in W^{1,2}(B_1, N)$ be a stationary [harmonic map](@entry_id:192561) from the unit ball $B_1 \subset \mathbb{R}^n$ to a closed manifold $N$. Then there exists a [closed set](@entry_id:136446) $\Sigma \subset B_1$, the [singular set](@entry_id:187696), such that $u$ is smooth ($C^\infty$) on the regular set $B_1 \setminus \Sigma$. Furthermore, the Hausdorff dimension of the [singular set](@entry_id:187696) is bounded by:
$$
\dim_{\mathcal{H}}(\Sigma) \le n-3
$$
This dimensional bound has profound consequences. It implies that for domains of dimension $n=1$ or $n=2$, stationary [harmonic maps](@entry_id:187821) are always smooth everywhere ($\Sigma$ is empty). For $n=3$, the [singular set](@entry_id:187696) has dimension at most 0, meaning it consists of at most a discrete set of isolated points. For higher dimensions, the [singular set](@entry_id:187696) can be more complex (e.g., curves or surfaces) but is still a "small" subset of the domain.

The proof of this theorem hinges on a crucial **$\varepsilon$-regularity** result. It states that there exists a universal constant $\varepsilon > 0$ such that if the scaled energy of the map in a small ball $B_r(x)$ is below this threshold,
$$
r^{2-n} \int_{B_r(x)} |du|^2 \, \mathrm{dvol}_g \le \varepsilon
$$
then the map $u$ must be smooth in the smaller, concentric ball $B_{r/2}(x)$. The [singular set](@entry_id:187696) $\Sigma$ is precisely the set of points where this condition fails for all sufficiently small radii $r$.

### Bubbling Phenomena in the Critical Dimension

The dimension bound $\dim_{\mathcal{H}}(\Sigma) \le n-3$ identifies the domain dimension $n=2$ as a critical case. While stationary [harmonic maps](@entry_id:187821) from surfaces are always regular, the existence of energy minimizers is not guaranteed, particularly when the target manifold has [positive curvature](@entry_id:269220). This is where the phenomenon of **bubbling** becomes most apparent [@problem_id:3035499].

Let's consider maps from a closed Riemann surface $(\Sigma, h)$ to the standard 2-sphere $(S^2, h_{std})$. The energy of any map $u: \Sigma \to S^2$ is bounded below by its [topological degree](@entry_id:264252):
$$
E(u) \ge 4\pi |\deg(u)|
$$
This inequality becomes an equality if and only if the map $u$ is conformal or anti-conformal.

Now, consider a sequence of maps $\{u_j\}$ in a fixed homotopy class (e.g., $\deg(u)=1$) that is a minimizing sequence for the energy, i.e., $E(u_j) \to \inf E = 4\pi$. Such a sequence can be constructed by taking a standard degree-1 [conformal map](@entry_id:159718) from $S^2$ to $S^2$ (like the identity map) and concentrating it at a point $p \in \Sigma$ using a scaling parameter. As the scaling parameter tends to infinity, the maps $u_j$ converge pointwise everywhere except at $p$ to a constant map, say to the South Pole.

The weak limit of this sequence, $u_\infty$, is this constant map. The energy of the weak limit is $E(u_\infty) = 0$, and its degree is $\deg(u_\infty) = 0$. However, the limit of the energies is $\lim E(u_j) = 4\pi$. The energy and the [topological degree](@entry_id:264252) have been lost in the weak limit.

This loss is explained by the formation of a **bubble**. By rescaling the sequence of maps around the concentration point $p$, we can see in the limit a non-trivial harmonic map from $S^2$ to $S^2$. This limiting map on the rescaled domain is the "bubble". In our example, the bubble is a degree-1 conformal map from $S^2$ to $S^2$. The energy of this bubble map is precisely the "lost" energy, $4\pi$. The bubble tree limit consists of the weak limit map on the original domain plus the collection of bubble maps on spheres. The total energy and degree are conserved across this tree:
$$
\lim_{j\to\infty} E(u_j) = E(u_\infty) + \sum_{\text{bubbles } v_i} E(v_i) \quad \text{and} \quad \deg(u_j) = \deg(u_\infty) + \sum_{\text{bubbles } v_i} \deg(v_i)
$$
This phenomenon explains why the direct method fails for $m=2$: the space of maps in a given homotopy class is not closed under [weak convergence](@entry_id:146650).

### Advanced Topics: The Heat Flow and Stability

The challenges posed by bubbling and the failure of the direct method motivate alternative approaches to constructing [harmonic maps](@entry_id:187821). One of the most powerful is the parabolic or evolution method, known as the **[harmonic map heat flow](@entry_id:200511)**.

#### The Harmonic Map Heat Flow

The [harmonic map heat flow](@entry_id:200511) is the $L^2$-[gradient flow](@entry_id:173722) of the Dirichlet [energy functional](@entry_id:170311). The idea is to start with an arbitrary initial map $u_0: M \to N$ and deform it over time $t$ in the direction of the [steepest descent](@entry_id:141858) of energy. The evolution equation is given by [@problem_id:3035510]:
$$
\frac{\partial u}{\partial t} = - \nabla_{L^2} E(u)
$$
As we saw earlier, the $L^2$-gradient of the energy is $\nabla_{L^2} E(u) = -\tau(u)$. Therefore, the [harmonic map heat flow](@entry_id:200511) equation is:
$$
\frac{\partial u}{\partial t} = \tau(u)
$$
This is a parabolic system of PDEs. One hopes that as $t \to \infty$, the solution $u(\cdot, t)$ will converge to a steady state, where $\frac{\partial u}{\partial t} = 0$. Such a steady state must satisfy $\tau(u)=0$, and is therefore a [harmonic map](@entry_id:192561).

This approach transforms the problem of solving a difficult elliptic system into studying the long-time behavior of a parabolic system. This method has been extremely successful. For example, when the target has [non-positive curvature](@entry_id:203441), Eells and Sampson proved that for any initial map $u_0$, the flow exists for all time and converges to a smooth harmonic map in the same homotopy class as $u_0$.

The flow is studied as an initial-boundary value problem. Two [natural boundary conditions](@entry_id:175664) arise from the variational structure of the energy functional:
1.  **Dirichlet boundary condition**: The map is fixed on the boundary, $u|_{\partial M \times [0,T)} = \varphi$, for a given time-independent map $\varphi: \partial M \to N$. The initial data $u_0$ must be compatible, i.e., $u_0|_{\partial M} = \varphi$.
2.  **Neumann boundary condition**: The map has a "free" boundary, which corresponds to the condition that the normal derivative of the map vanishes: $du(\nu) = 0$ on $\partial M$, where $\nu$ is the outward unit normal.

#### Stability of Harmonic Maps

Since [harmonic maps](@entry_id:187821) are critical points of the energy functional, it is natural to classify them as local minima, local maxima, or saddle points. This is determined by the sign of the **[second variation of energy](@entry_id:201932)**. A [harmonic map](@entry_id:192561) $u$ is said to be **stable** if the second variation is non-negative for all admissible variations [@problem_id:3035473]:
$$
\delta^2 E(u)(V) = \left.\frac{d^2}{dt^2}\right|_{t=0} E(u_t) \ge 0
$$
If the inequality is strict for all non-zero variations $V$, the map is **strictly stable**.

The second variation can be expressed as an integral involving a linear, self-adjoint, second-order [elliptic operator](@entry_id:191407) $J_u$, known as the **Jacobi operator**:
$$
\delta^2 E(u)(V) = \int_M \langle J_u V, V \rangle_h \, \mathrm{dvol}_g
$$
The operator $J_u$ acts on [vector fields](@entry_id:161384) along $u$ (sections of $u^{-1}TN$) and its definition involves the curvature of the target manifold. A harmonic map is stable if and only if its Jacobi operator is non-negative, meaning it has no negative eigenvalues.

The relationship between stability and energy minimization is crucial:
-   Any map that is a local energy minimizer in its homotopy class must be a stable [harmonic map](@entry_id:192561).
-   The converse is not true in general. A stable harmonic map is a local minimizer but may not be the global energy minimizer in its homotopy class. There could be multiple stable [harmonic maps](@entry_id:187821) in a single homotopy class, with only one (or some) being the absolute energy minimizer.

However, under the strong condition of [non-positive sectional curvature](@entry_id:275356) on the target manifold $(N,h)$, the theory simplifies dramatically. In this case, the energy functional is convex along [geodesic variations](@entry_id:182043), which implies that any [harmonic map](@entry_id:192561) is not only stable but is in fact the unique global energy minimizer in its homotopy class.