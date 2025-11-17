## Introduction
Modeling the initiation and propagation of cracks is one of the most enduring challenges in solid mechanics. Classical approaches often rely on local, stress-based criteria that struggle to predict complex crack topologies like branching or merging without ad-hoc rules. The variational approach to fracture offers a powerful and elegant alternative, recasting the entire problem in terms of energy. This framework posits that a crack will evolve in a way that minimizes the total energy of the system, providing a single, unified principle that governs both initiation and the subsequent crack path. This article addresses the fundamental question of how this energetic perspective can be translated into a robust and predictive computational tool for a vast range of fracture phenomena.

This article will guide you through the theory and application of this transformative approach. We will begin by exploring the foundational concepts in **Principles and Mechanisms**, starting with the Griffith-Francfort-Marigo energy functional for sharp cracks and detailing its regularization into a more computationally tractable [phase-field model](@entry_id:178606). Next, in **Applications and Interdisciplinary Connections**, we will demonstrate the framework's remarkable versatility by examining its extension to [ductile fracture](@entry_id:161045), dynamic shattering, [anisotropic materials](@entry_id:184874), and coupled multi-physics problems. Finally, the **Hands-On Practices** section provides concrete problems that bridge theory with implementation, focusing on [model calibration](@entry_id:146456), mesh requirements, and numerical solution strategies, equipping you with the essential knowledge to apply these methods in your own work.

## Principles and Mechanisms

This chapter delineates the fundamental principles and mechanics that form the basis of the variational approach to fracture. We begin by establishing the [energetic formulation](@entry_id:199250) for a body containing sharp cracks, as originally envisioned by Griffith and later formalized in a rigorous variational framework. We then transition to the powerful concept of phase-field regularization, which approximates sharp discontinuities with a continuous field, making the problem more amenable to numerical solution. Finally, we explore key properties and essential refinements of these [phase-field models](@entry_id:202885), providing a comprehensive understanding of their behavior and application.

### The Energetic Formulation of Brittle Fracture

The variational approach to [brittle fracture](@entry_id:158949) is rooted in a single, powerful idea first proposed by A.A. Griffith: [crack propagation](@entry_id:160116) is governed by a competition between the release of stored elastic energy and the energy consumed to create new fracture surfaces. The system seeks a state of minimum [total potential energy](@entry_id:185512). This principle provides a holistic criterion for both crack initiation and propagation, replacing the local, stress-based criteria of classical mechanics with a global, energetic perspective.

#### The Griffith-Francfort-Marigo Energy Functional

For a linearly elastic solid occupying a domain $\Omega \subset \mathbb{R}^d$ and containing a crack set $\Gamma$, the total potential energy of a configuration, defined by the displacement field $u$ and the crack set $\Gamma$, can be expressed by the functional [@problem_id:2709367] [@problem_id:2667954]:
$$
\Pi(u,\Gamma) \;=\; \underbrace{\int_{\Omega \setminus \Gamma} \psi(\varepsilon(u))\, \mathrm{d}x}_{\text{Stored Elastic Energy}} \; \underbrace{-\; \int_{\partial_N \Omega} t \cdot u \, \mathrm{d}s}_{\text{Potential of External Loads}} \;+\; \underbrace{G_c\, \mathcal{H}^{d-1}(\Gamma)}_{\text{Fracture Surface Energy}}.
$$
Let us dissect each term to understand its physical and mathematical significance.

The first term, $\int_{\Omega \setminus \Gamma} \psi(\varepsilon(u))\, \mathrm{d}x$, represents the total **stored elastic energy** within the body. The integration is performed over the intact material, $\Omega \setminus \Gamma$, as the strain field $\varepsilon(u)$ is only well-defined as a regular function in this region. The function $\psi$ is the strain-energy density. For a small-strain, linearly elastic material, this is a quadratic function of the [infinitesimal strain tensor](@entry_id:167211) $\varepsilon(u) = \frac{1}{2}(\nabla u + \nabla u^\top)$:
$$
\psi(\varepsilon(u)) = \frac{1}{2}\,\varepsilon(u):\mathbb{C}:\varepsilon(u),
$$
where $\mathbb{C}$ is the [fourth-order elasticity tensor](@entry_id:188318), which is assumed to be symmetric and positive-definite to ensure [material stability](@entry_id:183933) [@problem_id:2709367].

The second term, $-\int_{\partial_N \Omega} t \cdot u \, \mathrm{d}s$, represents the **potential energy of the prescribed external [surface tractions](@entry_id:169207)** $t$ acting on the Neumann boundary $\partial_N \Omega$. Consistent with the [principle of minimum potential energy](@entry_id:173340), this term is the negative of the work done by these external forces. The negative sign is crucial; it ensures that configurations where the body deforms in the direction of the applied forces are energetically favored [@problem_id:2709367]. If body forces $b$ are present, an additional term $-\int_{\Omega} b \cdot u \, \mathrm{d}x$ is included.

The final term, $G_c\, \mathcal{H}^{d-1}(\Gamma)$, is the heart of Griffith's theory: the **fracture [surface energy](@entry_id:161228)**. It postulates an energetic cost for creating new surfaces. The material parameter $G_c > 0$ is the **[fracture toughness](@entry_id:157609)** or **critical energy release rate**, representing the energy required to create a unit of fracture surface. Its units are energy per area (e.g., J/m$^2$) in three dimensions. The term $\mathcal{H}^{d-1}(\Gamma)$ is the $(d-1)$-dimensional **Hausdorff measure** of the crack set $\Gamma$. This provides a rigorous way to measure the "area" of the crack in 3D or its "length" in 2D, even for geometrically complex crack paths. Admissible crack sets $\Gamma$ are generally taken from the class of closed, countably $(d-1)$-[rectifiable sets](@entry_id:635569) with finite Hausdorff measure, a standard choice in [geometric measure theory](@entry_id:187987) that is general enough to include branching and kinking cracks [@problem_id:2709367].

#### Function Spaces and Variational Principles

A key challenge in this "free discontinuity" problem is identifying a suitable mathematical space for the [displacement field](@entry_id:141476) $u$. A crack is, by definition, a displacement discontinuity. Standard Sobolev spaces like $H^1(\Omega)$, which are fundamental to the [theory of elasticity](@entry_id:184142) on [continuous bodies](@entry_id:168586), do not permit such jump discontinuities. The natural [function space](@entry_id:136890) for the Griffith energy functional is the space of **Special Functions of Bounded Variation**, denoted $SBV(\Omega; \mathbb{R}^d)$ [@problem_id:2709412].

A function $u \in L^1(\Omega; \mathbb{R}^d)$ belongs to the broader class of [functions of bounded variation](@entry_id:144591), $BV$, if its [distributional derivative](@entry_id:271061) $Du$ is a finite matrix-valued Radon measure. This measure can be decomposed into three distinct parts: an absolutely continuous part (with density $\nabla u$), a jump part concentrated on the discontinuity set $J_u$, and a Cantor part. The Griffith energy only penalizes the first two parts. The space $SBV$ is precisely the subset of $BV$ where the un-penalized Cantor part of the derivative is zero. Therefore, for $u \in SBV$, the derivative consists only of a bulk gradient $\nabla u$ and a jump set $J_u$, perfectly aligning the structure of the [function space](@entry_id:136890) with the structure of the [energy functional](@entry_id:170311). This alignment is crucial for proving the existence of energy-minimizing solutions [@problem_id:2709412].

Minimizing the functional $\Pi(u, \Gamma)$ with respect to its arguments yields the governing principles of the system:

1.  **Equilibrium**: For a fixed crack set $\Gamma$, finding the displacement field $u$ that minimizes $\Pi$ is equivalent to solving the [linear elasticity](@entry_id:166983) problem on the cracked domain $\Omega \setminus \Gamma$. The [stationarity condition](@entry_id:191085) yields the [equilibrium equation](@entry_id:749057) $\nabla \cdot \sigma = 0$ in the bulk and, as a [natural boundary condition](@entry_id:172221), the traction-free state $\sigma \cdot n = 0$ on the crack faces $\Gamma$ [@problem_id:2709367].

2.  **Propagation**: The evolution of the crack set $\Gamma$ is also governed by energy minimization. This leads to the concept of **[configurational forces](@entry_id:188113)**, which are the thermodynamic driving forces for changes in the material's configuration (i.e., crack growth). The [stationarity](@entry_id:143776) of $\Pi$ with respect to variations of $\Gamma$ recovers the classical Griffith criterion: the crack is in equilibrium if the energy release rate $G$ (the amount of elastic energy released per unit new crack area) is equal to the [fracture toughness](@entry_id:157609) $G_c$. The crack will advance when $G \ge G_c$ [@problem_id:2709394].

This energetic framework elegantly unifies the mechanical response and the fracture process. An important consequence of this formulation is the prediction of a **[size effect](@entry_id:145741)**. For geometrically similar bodies of different sizes, scaled by a factor $\lambda$, the releasable bulk [energy scales](@entry_id:196201) with volume ($\sim\lambda^d$) while the fracture energy cost scales with area ($\sim\lambda^{d-1}$). This implies that larger structures are more prone to [brittle fracture](@entry_id:158949) than smaller ones, as the energetic gain from cracking outweighs the cost more easily at larger scales [@problem_id:2709394].

Finally, for a [quasi-static process](@entry_id:151741) under time-varying loads, the Francfort-Marigo formulation posits that the evolution of the system is a sequence of states $(u(t), \Gamma(t))$ that minimize the energy functional at each time $t$. This evolution is subject to a crucial physical constraint: **[irreversibility](@entry_id:140985)**. Cracks in brittle materials do not heal. This is enforced by requiring that the crack set can only grow over time: $\Gamma(t_1) \subseteq \Gamma(t_2)$ for any $t_1  t_2$ [@problem_id:2667954] [@problem_id:2709367]. This is not a term in the energy functional, but a constraint on the set of admissible crack configurations at each step of the evolution.

### Regularization: The Phase-Field Approach

While the sharp-crack [variational formulation](@entry_id:166033) is theoretically elegant, its numerical implementation is formidable, requiring the explicit tracking of complex, evolving discontinuities. The phase-field approach provides a powerful alternative by **regularizing** the problem. It replaces the sharp, lower-dimensional crack set $\Gamma$ with a continuous scalar field $d(x)$, called the **phase-field** or damage field, defined over the entire domain $\Omega$. This field varies smoothly from $d=0$ (intact material) to $d=1$ (fully broken material).

The total energy functional is reformulated in terms of the displacement $u$ and the phase-field $d$. This new functional is constructed to approximate the Griffith energy in a specific mathematical sense (that of $\Gamma$-convergence) as a [regularization parameter](@entry_id:162917) goes to zero. A typical phase-field energy functional has the form [@problem_id:2667993]:
$$
\mathcal{E}(u,d) = \int_{\Omega} g(d)\,\psi(\varepsilon(u))\,\mathrm{d}x + \int_{\Omega} \gamma_c(d, \nabla d) \,\mathrm{d}x.
$$

The first term is the **degraded elastic energy**. The function $g(d)$ is a **degradation function** that interpolates the material's stiffness between the intact and broken states. To be physically meaningful, it must be a monotonically non-increasing function satisfying $g(0)=1$ and $g(1)=0$ (or a small residual stiffness $\kappa > 0$ for numerical stability). A common choice is a quadratic function $g(d) = (1-d)^2 + \kappa$. The specific algebraic form of $g(d)$ influences the material behavior at finite damage but, crucially, does not prevent the model from converging to the Griffith limit [@problem_id:2487758].

The second term, $\int_{\Omega} \gamma_c(d, \nabla d)\,\mathrm{d}x$, is the **regularized surface energy**. It approximates the term $G_c \mathcal{H}^{d-1}(\Gamma)$. A widely used form, inspired by the work of Ambrosio and Tortorelli on the Mumford-Shah functional from [image processing](@entry_id:276975), is given by [@problem_id:2709368]:
$$
\gamma_c(d, \nabla d) = G_c \left( \frac{w(d)}{\ell} + \ell\,|\nabla d|^2 \right).
$$
This formulation introduces two key ingredients: a potential function $w(d)$ and a regularization length scale $\ell$.

#### The Role of the Length Scale $\ell$

The internal length scale $\ell > 0$ is a regularization parameter that governs the width of the diffuse crack zone. To see this, consider a one-dimensional transition from $d=0$ to $d=1$ across a crack. The optimal profile $d(x)$ must balance the energy from the potential term $w(d)/\ell$ (which favors sharp transitions to minimize the volume where $w(d)0$) and the gradient term $\ell|\nabla d|^2$ (which penalizes sharp gradients). A simple scaling analysis shows that these two terms are of the same order of magnitude when the characteristic width of the transition zone is proportional to $\ell$ [@problem_id:2709416]. Thus, $\ell$ directly controls the thickness of the regularized crack. As $\ell \to 0$, the diffuse crack sharpens and approaches a true discontinuity.

#### The Bridge: Calibration and $\Gamma$-Convergence

For the [phase-field model](@entry_id:178606) to be a valid approximation of [brittle fracture](@entry_id:158949), the total energy of the regularized crack must converge to the Griffith surface energy $G_c$ per unit area in the limit $\ell \to 0$. This is ensured by the mathematical theory of **$\Gamma$-convergence** [@problem_id:2709368].

A remarkable result from a one-[dimensional analysis](@entry_id:140259) of the surface functional is that the total energy required to form a transition from $d=0$ to $d=1$ is independent of $\ell$ if the terms are scaled as $1/\ell$ and $\ell$ respectively [@problem_id:2709416]. This energy can be calculated as:
$$
\mathcal{E}_{\text{1D-crack}} = \int_{-\infty}^{\infty} G_c \left( \frac{w(d(x))}{\ell} + \ell [d'(x)]^2 \right) dx = G_c \cdot c_w, \quad \text{where } c_w = \int_0^1 2\sqrt{w(s)}\,\mathrm{d}s.
$$
To ensure the model recovers the correct [fracture toughness](@entry_id:157609) $G_c$, the potential function $w(d)$ must be chosen or the functional must be normalized such that this integrated energy equals $G_c$. This typically means choosing $w(d)$ such that the constant $c_w = \int_0^1 2\sqrt{w(s)}\,\mathrm{d}s$ equals 1, or by dividing the surface energy density by this constant. This **calibration** process is fundamental to ensuring the quantitative accuracy of the [phase-field model](@entry_id:178606) [@problem_id:2487758] [@problem_id:2709368]. With this calibration, the phase-field functional is guaranteed to $\Gamma$-converge to the sharp-crack Griffith functional as $\ell \to 0$.

### Properties and Refinements of Phase-Field Models

The phase-field framework, while being an approximation, possesses several powerful features and can be refined to capture complex physical phenomena.

#### Emergent Crack Topology

One of the most significant advantages of the variational approach, particularly in its phase-field form, is that it does not require any *ad hoc* criterion for crack initiation, kinking, or branching. The evolution of the [displacement field](@entry_id:141476) $u$ and the damage field $d$ is found by solving a coupled system of partial differential equations that arise from the minimization of the total [energy functional](@entry_id:170311) $\mathcal{E}(u,d)$. Because the minimization is performed over the entire function space for $d(x)$, the procedure simultaneously explores all possible crack paths and geometries. The resulting crack pattern is an emergent property of the system, corresponding to the path that provides the most efficient means of dissipating energy. The theory naturally predicts where a crack will start, in which direction it will propagate, and whether it will curve or branch, all from a single energetic principle [@problem_id:2667993].

#### Irreversibility Constraint

Just as in the sharp-crack model, the physical principle of crack irreversibility must be enforced. For the phase-field $d$, this translates to the simple pointwise constraint that damage can only increase over time: $d(x, t_2) \ge d(x, t_1)$ for $t_2 > t_1$, or in rate form, $\dot{d} \ge 0$. In a common time-discretized, incremental solution scheme, this constraint is implemented at each time step $n$ by seeking a solution $d^n$ within the admissible set of functions that satisfy $d^n(x) \ge d^{n-1}(x)$ for all $x$. This turns the [damage evolution](@entry_id:184965) problem into a [constrained optimization](@entry_id:145264) problem, which is mathematically formulated as a **[variational inequality](@entry_id:172788)** or, equivalently, using Karush-Kuhn-Tucker (KKT) conditions with a Lagrange multiplier that enforces the constraint [@problem_id:2709388].

#### Crack Nucleation: AT1 vs. AT2 Models

The choice of the potential function $w(d)$ in the surface energy has a profound impact on the model's behavior, particularly concerning [crack nucleation](@entry_id:748035). Two canonical choices define the **AT1** and **AT2** models [@problem_id:2709417]:
*   **AT1 Model**: $w(d) = d$. The [surface energy](@entry_id:161228) density has a term linear in $d$.
*   **AT2 Model**: $w(d) = d^2$. The [surface energy](@entry_id:161228) density has a term quadratic in $d$.

Consider a homogeneous body under increasing load. The stability of the undamaged state ($d=0$) determines when fracture initiates. An analysis of the [energy functional](@entry_id:170311) for a homogeneous state shows that:
*   In the **AT2 model**, for any non-zero applied load, the energy of the system decreases if an infinitesimal amount of damage is introduced. This means the undamaged state is always unstable under load, and damage begins to accumulate immediately. The AT2 model has a **zero nucleation threshold**.
*   In the **AT1 model**, the term linear in $d$ provides an initial energetic barrier to damage. The undamaged state remains stable until the stored elastic energy density reaches a critical value. This value is proportional to $G_c/\ell$. Therefore, the AT1 model exhibits a **finite stress threshold** for [crack nucleation](@entry_id:748035).

This distinction is critical: the AT1 model better represents the behavior of a truly brittle material that resists any damage up to a [critical load](@entry_id:193340), whereas the AT2 model resembles a more ductile or cohesive response where "damage" initiates at very low loads.

#### Tension-Compression Asymmetry

A crucial physical aspect of fracture is its asymmetry with respect to tension and compression. Cracks are driven by tensile stresses, and their faces should not interpenetrate under compression. The basic phase-field [energy functional](@entry_id:170311), which degrades the full elastic energy $\psi(\varepsilon)$, is symmetric and fails to capture this behavior, leading to unphysical predictions of damage growth in compressive states.

To remedy this, the elastic energy density $\psi_0$ is split into a **tensile part** $\psi_0^+$ and a **compressive part** $\psi_0^-$, such that $\psi_0 = \psi_0^+ + \psi_0^-$. The degradation function is then applied only to the tensile part:
$$
\psi_{\text{degraded}}(d, \varepsilon) = g(d)\psi_0^+(\varepsilon) + \psi_0^-(\varepsilon).
$$
A common and consistent way to perform this split is based on the [spectral decomposition](@entry_id:148809) of the strain tensor $\varepsilon = \sum_{i=1}^3 \varepsilon_i \mathbf{n}_i \otimes \mathbf{n}_i$. A widely used formulation defines [@problem_id:2709373]:
$$
\psi_0^+(\varepsilon) = \frac{\lambda}{2} \langle \mathrm{tr}\,\varepsilon \rangle_+^2 + \mu \sum_{i=1}^3 \langle \varepsilon_i \rangle_+^2,
$$
$$
\psi_0^-(\varepsilon) = \frac{\lambda}{2} \langle \mathrm{tr}\,\varepsilon \rangle_-^2 + \mu \sum_{i=1}^3 \langle \varepsilon_i \rangle_-^2,
$$
where $\langle x \rangle_+$ and $\langle x \rangle_-$ are the positive and negative parts of $x$ (Macaulay brackets). With this decomposition, any purely compressive strain state (all $\varepsilon_i \le 0$) results in $\psi_0^+ = 0$. Consequently, the [thermodynamic driving force for damage](@entry_id:182386), which is proportional to $\psi_0^+$, vanishes, correctly preventing crack growth under compression. This refinement is essential for realistic simulations of structures under complex loading conditions.