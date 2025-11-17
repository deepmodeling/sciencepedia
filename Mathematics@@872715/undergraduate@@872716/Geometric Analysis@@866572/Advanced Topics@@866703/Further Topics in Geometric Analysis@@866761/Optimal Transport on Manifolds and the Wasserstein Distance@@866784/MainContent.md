## Introduction
The problem of optimally transporting mass from one configuration to another is a concept as intuitive as it is profound. First envisioned by Gaspard Monge in the 18th century, the theory of optimal transport has evolved into a cornerstone of modern mathematics, providing a powerful lens through which to analyze and compare probability distributions. Its significance lies in its unique ability to incorporate the underlying geometry of the space, measuring not just if distributions differ, but how much 'work' is required to transform one into the other. This article addresses the extension of these ideas to the curved and complex world of Riemannian manifolds, exploring the deep geometric structures that emerge.

This exploration will unfold across three distinct chapters. First, in **Principles and Mechanisms**, we will delve into the core theoretical machinery, from the foundational Kantorovich problem and Brenier's theorem to the revolutionary dynamic formulation that recasts transport as a [geodesic flow](@entry_id:270369). Next, in **Applications and Interdisciplinary Connections**, we will witness the theory in action, uncovering its remarkable impact on fields as diverse as machine learning, partial differential equations, and modern geometric analysis. Finally, a series of **Hands-On Practices** will provide concrete exercises to solidify your understanding of these powerful concepts.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that govern the theory of [optimal transport](@entry_id:196008) and the geometry of Wasserstein space. We move from the foundational static formulations of the transport problem to its dynamic interpretation as a flow, culminating in an exploration of the rich geometric structure this framework imparts upon the space of probability measures.

### The Kantorovich Formulation: From Mass Splitting to Transport Plans

The central problem of [optimal transport](@entry_id:196008) is to find the most efficient way to morph one distribution of mass, represented by a probability measure $\mu$, into another, $\nu$, on a given space. On a Riemannian manifold $(M,g)$, the "effort" or "cost" of moving a unit of mass from a point $x$ to a point $y$ is typically quantified by a [cost function](@entry_id:138681). A particularly important choice, which underpins the $2$-Wasserstein distance, is the squared Riemannian distance, $c(x,y) = d(x,y)^2$.

The original formulation of this problem, posed by Gaspard Monge in the 18th century, sought a **transport map** $T: M \to M$. This map would specify the exact destination $T(x)$ for each particle of mass starting at $x$. The goal was to find a map $T$ that "pushes" $\mu$ onto $\nu$ (denoted $T_\#\mu = \nu$) while minimizing the total transport cost, $\int_M d(x, T(x))^2 \, \mathrm{d}\mu(x)$. However, the Monge formulation has a critical limitation: it cannot accommodate scenarios where mass from a single point must be split and distributed to multiple destinations.

To see this, consider a simple hypothetical scenario on the unit circle $S^1$. Suppose we wish to transport a single concentration of mass, $\mu = \delta_{x_0}$, to a target distribution that is split between two points, for instance, $\nu = \frac{3}{5}\delta_{x_1} + \frac{2}{5}\delta_{x_2}$ [@problem_id:3058018]. A map $T$ must assign a single destination $T(x_0)$ to the mass at $x_0$. The resulting pushed-forward measure would be $\delta_{T(x_0)}$, a single [point mass](@entry_id:186768). It is impossible for such a measure to equal $\nu$, which is supported on two distinct points. The Monge problem has no solution in this case.

This limitation motivated the modern formulation by Leonid Kantorovich. Instead of a deterministic map, Kantorovich proposed a more flexible object: a **transport plan** (or **coupling**), which is a [joint probability](@entry_id:266356) measure $\pi$ on the [product space](@entry_id:151533) $M \times M$. A transport plan $\pi$ is considered *admissible* if it has $\mu$ and $\nu$ as its marginal distributions. This means that for any measurable set $A \subset M$, the total mass of the plan in the strip $A \times M$ must equal $\mu(A)$, and the mass in the strip $M \times A$ must equal $\nu(A)$. We denote the set of all such admissible plans as $\Pi(\mu, \nu)$. The quantity $\pi(A \times B)$ can be interpreted as the amount of mass that is moved from the set $A$ to the set $B$.

With this more general object, the **squared $2$-Wasserstein distance** is defined as the minimal cost achievable over all possible plans:
$$
W_2^2(\mu, \nu) = \inf_{\pi \in \Pi(\mu, \nu)} \int_{M \times M} d(x,y)^2 \, \mathrm{d}\pi(x,y).
$$

Let us revisit the mass-splitting example [@problem_id:3058018]. Here, $\mu = \delta_{x_0}$ and $\nu = \frac{3}{5}\delta_{x_1} + \frac{2}{5}\delta_{x_2}$. Any admissible plan $\pi$ must have its support within the product of the supports of its marginals, i.e., $\mathrm{supp}(\pi) \subseteq \{x_0\} \times \{x_1, x_2\}$. This forces $\pi$ to be of the form $\pi = c_1 \delta_{(x_0, x_1)} + c_2 \delta_{(x_0, x_2)}$. The marginal constraints uniquely determine the coefficients. The first marginal constraint on $\mu$ implies $c_1 + c_2 = \mu(\{x_0\}) = 1$. The second marginal constraint on $\nu$ implies $c_1 = \nu(\{x_1\}) = 3/5$ and $c_2 = \nu(\{x_2\}) = 2/5$. Thus, there is only one admissible transport plan:
$$
\pi = \frac{3}{5} \delta_{(x_0, x_1)} + \frac{2}{5} \delta_{(x_0, x_2)}.
$$
Since this is the only plan in $\Pi(\mu, \nu)$, it is trivially the optimal one. The Wasserstein distance is then found by evaluating the cost integral for this plan, which becomes a simple sum:
$$
W_2^2(\mu, \nu) = \frac{3}{5} d(x_0, x_1)^2 + \frac{2}{5} d(x_0, x_2)^2.
$$
This example crystallizes the power of the Kantorovich formulation: it provides a robust framework that guarantees a solution by allowing for probabilistic couplings, elegantly handling cases like mass splitting where the deterministic Monge picture breaks down.

### From Maps to Potentials: Brenier's Theorem and Duality

While the Kantorovich formulation is more general, in many important situations the [optimal transport](@entry_id:196008) plan is, in fact, induced by a map. This brings us back to the Monge problem. A cornerstone result, **Brenier's Theorem**, provides a precise condition for the existence and structure of an optimal transport map. In its classical setting on Euclidean space $\mathbb{R}^n$ with the quadratic cost $c(x,y) = \frac{1}{2}|x-y|^2$, the theorem states that if the source measure $\mu$ is absolutely continuous with respect to the Lebesgue measure (i.e., it has a density and no point masses), then there exists a unique optimal transport map $T$ from $\mu$ to any target $\nu \in \mathcal{P}_2(\mathbb{R}^n)$. Astonishingly, this map is not arbitrary; it is the gradient of a convex function $\psi: \mathbb{R}^n \to \mathbb{R}$, so that $T(x) = \nabla \psi(x)$.

This result has a profound generalization to Riemannian manifolds, established by McCann [@problem_id:3058009]. On a complete, connected Riemannian manifold $(M,g)$, if the source measure $\mu$ is absolutely continuous with respect to the Riemannian volume measure, then a unique optimal map $T$ exists for the quadratic cost. This map is characterized by a [potential function](@entry_id:268662) $\varphi$, and for $\mu$-almost every $x \in M$, the destination $T(x)$ is given by the Riemannian **exponential map**:
$$
T(x) = \exp_x(-\nabla \varphi(x)).
$$
This means that the optimal path for a particle starting at $x$ is to travel for unit time along the geodesic with initial velocity given by the negative gradient of the potential $\varphi$. The function $\varphi$ is not arbitrary; it must be *c-convex*, a notion we will encounter again in the context of duality. It is crucial to note that the [absolute continuity](@entry_id:144513) of the *source* measure $\mu$ is the key hypothesis; no such assumption on the target measure $\nu$ is needed [@problem_id:3058009].

The existence of a map $T$ that pushes $\mu$ to $\nu$ (denoted $T_\#\mu = \nu$) has direct consequences for the densities. The **[change of variables](@entry_id:141386) formula** relates the density of the source measure, $\rho_\mu$, to that of the target measure, $\rho_\nu$:
$$
\rho_\nu(y) = \rho_\mu(T^{-1}(y)) |\det(J_{T^{-1}}(y))|,
$$
where $J_{T^{-1}}$ is the Jacobian of the inverse map. For a simple affine map $T(x) = ax+b$ on $\mathbb{R}$ with $a>0$, the inverse is $T^{-1}(y) = (y-b)/a$ and the Jacobian determinant is $1/a$. If $\mu$ is the uniform measure on $[0,1]$, its density $\rho_\mu$ is 1 on that interval. The [pushforward measure](@entry_id:201640) $\nu = T_\#\mu$ will have density $\rho_\nu(y) = 1 \cdot (1/a)$ on the interval $[b, a+b]$ [@problem_id:3058006].

When an optimal map $T$ exists, the Wasserstein distance calculation simplifies. The infimum is attained, and the integral is computed over the graph of the map: $W_2^2(\mu,\nu) = \int_M d(x, T(x))^2 \, \mathrm{d}\mu(x)$. For measures on the real line, the optimal map for quadratic cost is simply the non-decreasing rearrangement of mass, given by $T(x) = F_\nu^{-1}(F_\mu(x))$, where $F_\mu$ and $F_\nu$ are the cumulative distribution functions. One can verify that for the affine map $T(x)=ax+b$ ($a>0$) and uniform measures, this condition holds, confirming that $T$ is indeed the optimal map [@problem_id:3058006].

Even with these powerful existence results, challenges remain. The smoothness of the manifold and the densities does not guarantee smoothness of the optimal map $T$. The structure $T(x) = \exp_x(-\nabla \varphi(x))$ reveals that singularities can arise from the [exponential map](@entry_id:137184) itself, which is known to be non-smooth at the **[cut locus](@entry_id:161337)** of a point. Curvature effects can cause geodesics starting from nearby points to cross, creating discontinuities in the transport map [@problem_id:3058009]. The sphere $\mathbb{S}^n$, despite its perfect smoothness and symmetry, is a classic example where such singularities occur.

Parallel to the primal problem of minimizing cost, there exists a dual formulation. **Kantorovich duality** reframes the problem as a maximization:
$$
W_2^2(\mu, \nu) = \sup_{\phi, \psi} \left\{ \int_M \phi \, \mathrm{d}\mu + \int_M \psi \, \mathrm{d}\nu \right\},
$$
subject to the constraint that the pair of **Kantorovich potentials** $(\phi, \psi)$ satisfies $\phi(x) + \psi(y) \le c(x,y)$ for all $(x,y) \in M \times M$. A key result is that, under general conditions, there is no [duality gap](@entry_id:173383): the maximum of the dual problem equals the minimum of the primal problem. This is immensely useful, as constructing any admissible pair $(\phi, \psi)$ provides a lower bound on the transport cost.

The potentials are related through the concept of **$c$-conjugation**. For instance, one can define $\phi$ as the $c$-transform of $\psi$: $\phi(x) = \inf_y \{ c(x,y) - \psi(y) \}$. A function that can be represented this way is called **$c$-concave**. Finding a pair of potentials for which the dual objective value matches the cost of a known transport plan proves the optimality of both. For example, in a symmetric problem on the circle $S^1$ with cost $c(x,y)=d(x,y)$, one might find that the [cost matrix](@entry_id:634848) is constant. This immediately gives an upper bound on the transport cost. By explicitly constructing a pair of dual potentials and calculating the dual objective, one can show this upper bound is met, thereby rigorously proving its optimality via duality [@problem_id:3058017]. No special boundary conditions are required for these potentials on a [manifold with boundary](@entry_id:160030) [@problem_id:3058014].

### The Dynamic Formulation: Transport as a Geodesic Flow

A revolutionary perspective, developed by Benamou and Brenier, recasts the static optimal transport problem into a dynamic one. It defines the squared $2$-Wasserstein distance as the minimum "kinetic energy" required to evolve the density $\rho_0$ of $\mu$ into the density $\rho_1$ of $\nu$ over a time interval, say $t \in [0,1]$.

This formulation considers a time-dependent probability density $\rho_t(x)$ and a time-dependent [velocity field](@entry_id:271461) $v_t(x)$. For mass to be conserved throughout the evolution, the pair must satisfy the **continuity equation**:
$$
\partial_t \rho_t + \nabla \cdot (\rho_t v_t) = 0.
$$
This equation states that the rate of change of density at a point is equal to the negative divergence of the mass flux $\rho_t v_t$. The total kinetic energy of such a flow is defined by the [action functional](@entry_id:169216):
$$
\mathcal{A}[\rho, v] = \int_0^1 \int_M |v_t(x)|_g^2 \, \rho_t(x) \, \mathrm{dvol}(x) \, \mathrm{d}t.
$$
The **Benamou-Brenier formula** then states that the squared Wasserstein distance is the infimum of this action over all admissible paths $(\rho_t, v_t)$ that connect $\rho_0$ and $\rho_1$:
$$
W_2^2(\mu_0, \mu_1) = \inf_{(\rho_t, v_t)} \mathcal{A}[\rho, v].
$$
The path that achieves this minimum is a **geodesic** in the space of probability measures. This formulation provides a powerful intuition: the Wasserstein distance is the length of the shortest path between two distributions in a space where the geometry is defined by the principles of mass conservation and minimal kinetic energy.

A simple, illustrative example is a rigid rotation on the circle $S^1$ [@problem_id:3058012]. Let the initial density be $\rho_0(\theta)$ and the final density be a rotated version, $\rho_1(\theta) = \rho_0(\theta - \alpha)$. A natural candidate for the transport flow is a constant-speed rotation: the velocity field is constant, $v_t(\theta) = \alpha$, and the density at time $t$ is $\rho_t(\theta) = \rho_0(\theta - \alpha t)$. One can directly verify that this pair $(\rho_t, v_t)$ satisfies the continuity equation. The kinetic action for this flow can be calculated:
$$
\mathcal{A}[\rho,v] = \int_0^1 \int_{S^1} \rho_t(\theta) \alpha^2 \, \mathrm{d}\theta \, \mathrm{d}t = \int_0^1 \alpha^2 \left( \int_{S^1} \rho_t(\theta) \, \mathrm{d}\theta \right) \mathrm{d}t = \int_0^1 \alpha^2 \cdot 1 \, \mathrm{d}t = \alpha^2.
$$
To show this is minimal, one can use the Cauchy-Schwarz inequality, which implies that for any path $\gamma(t)$ connecting two points, its energy $\int |\dot{\gamma}|^2 dt$ is always greater than or equal to the squared length of the path, which in turn is greater than or equal to the squared [geodesic distance](@entry_id:159682) between its endpoints. Equality holds if the path is a [constant-speed geodesic](@entry_id:634525). The proposed flow corresponds to every particle of mass traveling along a [constant-speed geodesic](@entry_id:634525) of length $\alpha$. Therefore, its action $\alpha^2$ achieves the theoretical minimum, and we can conclude that $W_2^2(\rho_0, \rho_1) = \alpha^2$ [@problem_id:3058012].

This dynamic view is particularly important when considering transport on manifolds with boundaries. To ensure that mass is conserved within the domain, the continuity equation must be supplemented with a **[no-flux boundary condition](@entry_id:168487)**, $v_t \cdot n = 0$, where $n$ is the normal to the boundary. This ensures no mass crosses the boundary and corresponds to the static formulation where the distance is the intrinsic [geodesic distance](@entry_id:159682) within the domain [@problem_id:3058014].

### The Geometry of Wasserstein Space and its Applications

The Benamou-Brenier formula does more than just provide an alternative definition for the distance; it reveals that the space of probability measures (with finite second moments), $(\mathcal{P}_2(M), W_2)$, possesses the structure of an infinite-dimensional Riemannian manifold. This perspective, often called **Otto calculus**, has been extraordinarily fruitful.

In this framework, the [tangent space](@entry_id:141028) at a point $\rho \in \mathcal{P}_2(M)$ can be identified with functions $\sigma$ that represent infinitesimal changes in density (satisfying $\int \sigma = 0$). The Riemannian metric, or inner product, between two [tangent vectors](@entry_id:265494) is defined via the kinetic energy. Specifically, any valid perturbation $\sigma$ can be generated from a [velocity field](@entry_id:271461) $v = -\nabla \phi$ via the linearized continuity equation $\sigma = \nabla \cdot (\rho \nabla \phi)$. The squared norm of the [tangent vector](@entry_id:264836) $\sigma$ is then defined as the minimal kinetic energy required to produce it: $\|\sigma\|_\rho^2 = \int_M |\nabla \phi|_g^2 \, \rho \, \mathrm{dvol}$.

This formal structure can be used for concrete calculations. For two densities $\rho_0$ and $\rho_1$ that are very close, the squared [geodesic distance](@entry_id:159682) $W_2^2(\rho_0, \rho_1)$ can be approximated by the squared norm of the "[tangent vector](@entry_id:264836)" that connects them, i.e., their difference $\sigma = \rho_1 - \rho_0$. To compute this, one must first find the potential $\phi$ by solving the Poisson equation $-\nabla \cdot (\rho_0 \nabla \phi) = \rho_1 - \rho_0$. The squared distance is then approximately $\int |\nabla \phi|^2 \rho_0$. For small perturbations around the uniform density on a flat torus, this becomes a straightforward exercise in Fourier analysis, allowing for explicit computation of the leading-order term in the Wasserstein distance [@problem_id:3058019].

One of the most powerful applications of this geometric viewpoint is the theory of **[gradient flows](@entry_id:635964)**. A gradient flow is the continuous-time analogue of [gradient descent](@entry_id:145942), describing a path that always moves in the direction of [steepest descent](@entry_id:141858) of some energy functional $\mathcal{E}(\mu)$. In Wasserstein space, this corresponds to a curve of measures $(\mu_t)$ that solves the evolution equation $\partial_t \mu_t = -\mathrm{grad}_{W_2} \mathcal{E}(\mu_t)$. This equation turns out to be a [partial differential equation](@entry_id:141332) of Fokker-Planck type.

A practical way to approximate this continuous flow is the **Jordan-Kinderlehrer-Otto (JKO) scheme**, a time-discretized implicit Euler scheme for the [gradient flow](@entry_id:173722). Given a state $\mu^k$ at time step $k$, the next state $\mu^{k+1}$ is found by solving the following minimization problem:
$$
\mu^{k+1} \in \operatorname{arg\,min}_{\mu \in \mathcal{P}_2(M)} \left\{ \frac{1}{2\tau} W_2^2(\mu, \mu^k) + \mathcal{E}(\mu) \right\},
$$
where $\tau$ is the time step size. This scheme finds a new measure $\mu$ that strikes a balance between being close to the previous measure $\mu^k$ (the $W_2^2$ term) and having low energy (the $\mathcal{E}(\mu)$ term). For certain choices of functionals and families of measures, this minimization becomes tractable. A classic example is the evolution of a Gaussian measure under the [gradient flow](@entry_id:173722) of the second moment functional $\mathcal{E}(\mu) = \frac{1}{2} \int |x|^2 \mathrm{d}\mu$. The JKO scheme reduces to a simple, explicit update rule for the mean and variance of the Gaussian, providing a beautiful link between a variational scheme, [optimal transport](@entry_id:196008), and the solution to the Ornstein-Uhlenbeck equation [@problem_id:3058008].

The geometric curvature of Wasserstein space is also deeply connected to the curvature of the underlying manifold $M$. The celebrated Bakry-Émery theory shows that if the Ricci curvature of $M$ is bounded below by $\kappa$, then the [relative entropy](@entry_id:263920) functional $H(\cdot|\nu)$ (for a suitable reference measure $\nu$) is $\kappa$-convex along the geodesics of Wasserstein space. This property can be used to derive powerful [functional inequalities](@entry_id:203796) that link entropy, information, and transport distance. The **HWI inequality** is a prime example, providing a relationship of the form:
$$
H(\mu | \nu) \le W_2(\mu, \nu) \sqrt{I(\mu | \nu)} - \frac{\kappa}{2} W_2^2(\mu, \nu),
$$
where $I(\mu|\nu)$ is the relative Fisher information. This inequality neatly encapsulates how the dissipation of entropy is controlled by the transport distance and Fisher information, with the rate modulated by the curvature of the space. For certain pairs of measures, such as translated Gaussians on $\mathbb{R}^n$, this inequality is saturated, providing a sharp and explicit relationship between these three fundamental quantities [@problem_id:3058011].

### Advanced Structural Properties

The theory of optimal transport is rich with further structural results. On a complete, separable (i.e., Polish) manifold, the existence of an [optimal coupling](@entry_id:264340) is guaranteed for measures with finite second moments. Furthermore, the Wasserstein space $(\mathcal{P}_2(M), W_2)$ is itself a geodesic space: any two measures can be connected by a minimal geodesic, which can be constructed via "displacement interpolation" from an optimal plan [@problem_id:3058014].

Finally, transport plans can be composed. The **gluing lemma** states that if one has a transport plan $\pi_{12}$ from $\mu$ to $\nu$ and another plan $\pi_{23}$ from $\nu$ to $\eta$, a "glued" probability measure $\gamma$ can be constructed on the three-fold product space $M \times M \times M$ that is consistent with both plans. By integrating out the intermediate variable, one can obtain an induced transport plan $\pi_{13}$ from $\mu$ to $\eta$. This process, known as the **disintegration of measures**, provides a mechanism for understanding the composition of transport pathways, albeit the resulting plan is not necessarily optimal for the $(\mu, \eta)$ problem [@problem_id:3058010]. These properties underscore the robust and versatile mathematical structure underlying optimal transport, making it a powerful tool across pure and applied mathematics.