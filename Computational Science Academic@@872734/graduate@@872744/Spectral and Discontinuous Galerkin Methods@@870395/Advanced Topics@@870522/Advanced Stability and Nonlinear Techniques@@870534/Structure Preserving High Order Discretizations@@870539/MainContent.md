## Introduction
Modern [high-order numerical methods](@entry_id:142601) offer exceptional accuracy for [solving partial differential equations](@entry_id:136409) (PDEs), yet this accuracy does not always guarantee physical realism. Conventional discretizations, while convergent, can fail to respect the fundamental laws of physics inherent in the governing equations, leading to non-physical artifacts like [energy drift](@entry_id:748982) or spurious oscillations. This creates a critical knowledge gap: how can we build [high-order schemes](@entry_id:750306) that are not only accurate but also structurally sound and robust, especially for long-time simulations?

This article addresses this challenge by providing a comprehensive overview of structure-preserving [high-order discretizations](@entry_id:750302). You will learn how to design numerical methods that inherit the essential mathematical properties—conservation laws, symmetries, and geometric constraints—of the continuous models they approximate. The following sections will guide you through this advanced topic. First, "Principles and Mechanisms" will dissect the foundational structures worth preserving and the sophisticated numerical machinery, such as SBP operators and [entropy-stable fluxes](@entry_id:749015), used to enforce them. Next, "Applications and Interdisciplinary Connections" will showcase how these methods are revolutionizing fields from fluid dynamics to [plasma physics](@entry_id:139151) by enabling more faithful and stable simulations. Finally, "Hands-On Practices" will offer practical exercises to solidify your understanding of these powerful computational tools.

## Principles and Mechanisms

The introduction introduced the motivation for structure-preserving discretizations: the observation that conventional numerical methods, while convergent in the limit of refinement, often fail to respect the fundamental physical laws and mathematical structures inherent in the governing [partial differential equations](@entry_id:143134) (PDEs). This failure can lead to qualitatively incorrect results, such as non-physical oscillations, [energy drift](@entry_id:748982), or the inability to maintain steady states. This chapter delves into the principles and mechanisms that underpin the construction of [high-order methods](@entry_id:165413) designed to overcome these deficiencies. We will first identify the key structures worth preserving and then explore the sophisticated numerical machinery developed to enforce these structures at the discrete level.

### Foundational Structures and Their Invariants

At the heart of structure preservation lies the identification of an essential property of the continuous PDE that must be mirrored by the discrete approximation. These properties range from fundamental conservation laws to more subtle geometric or topological constraints.

#### Conservation of Physical Quantities

The most fundamental structure of many PDEs in physics and engineering is the conservation of a physical quantity, such as mass, momentum, or energy. For a scalar quantity $u$ governed by a conservation law, $\partial_t u + \nabla \cdot \mathbf{f}(u) = 0$, the total amount of $u$ within any fixed volume $V$, $\int_V u \, \mathrm{d}x$, changes only due to the flux of $\mathbf{f}(u)$ across the boundary $\partial V$. A numerical method should ideally replicate this behavior.

In the context of Discontinuous Galerkin (DG) methods, this principle is separated into two concepts: **[local conservation](@entry_id:751393)** and **global conservation**. A DG method partitions the domain $\Omega$ into a set of non-overlapping elements $K$. The semi-discrete DG formulation for an element $K$ is derived by multiplying the PDE by a test function $v_h$ and integrating by parts, yielding:
$$
\int_K \frac{\partial u_h}{\partial t} v_h \, \mathrm{d}x - \int_K \mathbf{f}(u_h) \cdot \nabla v_h \, \mathrm{d}x + \int_{\partial K} \widehat{\mathbf{F}}(u_h^-, u_h^+; \mathbf{n}) v_h^- \, \mathrm{d}s = 0
$$
where $u_h^-$ is the solution trace from within element $K$, $u_h^+$ is the trace from the neighboring element, $\mathbf{n}$ is the outward unit normal, and $\widehat{\mathbf{F}}$ is a **[numerical flux](@entry_id:145174)** that resolves the ambiguity of the discontinuous solution at the interface.

**Local conservation** is achieved if the rate of change of the total quantity within a single element $K$ equals the net [numerical flux](@entry_id:145174) across its boundary. This is revealed by choosing a constant [test function](@entry_id:178872), $v_h=1$, for which $\nabla v_h = 0$. The DG formulation then simplifies to:
$$
\frac{\mathrm{d}}{\mathrm{d}t} \int_K u_h \, \mathrm{d}x = - \int_{\partial K} \widehat{\mathbf{F}}(u_h^-, u_h^+; \mathbf{n}) \, \mathrm{d}s
$$
This property is automatically satisfied by any standard DG method, provided the [test space](@entry_id:755876) contains constants.

**Global conservation**, the conservation of $\int_\Omega u_h \, \mathrm{d}x$, requires an additional condition on the [numerical flux](@entry_id:145174). When summing the [local conservation law](@entry_id:261997) over all elements $K$, the sum of the boundary integrals over all interior faces must vanish. Consider an interior face shared by elements $K_1$ and $K_2$, with normals $\mathbf{n}_1$ and $\mathbf{n}_2 = -\mathbf{n}_1$. The total contribution from this face is $\int_e (\widehat{\mathbf{F}}(u_1, u_2; \mathbf{n}_1) + \widehat{\mathbf{F}}(u_2, u_1; \mathbf{n}_2)) \, \mathrm{d}s$. For this to be zero, the [numerical flux](@entry_id:145174) must be single-valued (or conservative) in the sense that the flux leaving $K_1$ is the same as the flux entering $K_2$. This imposes the algebraic condition:
$$
\widehat{\mathbf{F}}(a, b; \mathbf{n}) = - \widehat{\mathbf{F}}(b, a; -\mathbf{n})
$$
for any two states $a$ and $b$. Furthermore, for the scheme to approximate the correct PDE, the numerical flux must be **consistent** with the physical flux, meaning $\widehat{\mathbf{F}}(w, w; \mathbf{n}) = \mathbf{f}(w) \cdot \mathbf{n}$ when the solution is continuous. These two conditions—consistency and the single-valued property—are the foundational requirements for a [numerical flux](@entry_id:145174) in a conservative [finite volume](@entry_id:749401) or DG scheme [@problem_id:3421724].

#### Entropy Stability for Hyperbolic Systems

For nonlinear [hyperbolic systems](@entry_id:260647), conservation laws alone are not sufficient to guarantee a unique, physically relevant solution. Weak solutions can include non-physical phenomena, such as expansion shocks. The second law of thermodynamics provides an additional constraint: the physical solution must satisfy an **[entropy inequality](@entry_id:184404)**.

For a system of conservation laws $\partial_t \mathbf{u} + \partial_x \mathbf{f}(\mathbf{u}) = 0$, an **entropy pair** $(U, F)$ consists of a convex scalar function $U(\mathbf{u})$, called the entropy, and an associated entropy flux $F(\mathbf{u})$. They are linked by a compatibility condition, $(\nabla U)^\top \nabla \mathbf{f} = (\nabla F)^\top$. For smooth solutions, this implies an additional conservation law, $\partial_t U(\mathbf{u}) + \partial_x F(\mathbf{u}) = 0$. For non-smooth physical solutions, this becomes the inequality $\partial_t U(\mathbf{u}) + \partial_x F(\mathbf{u}) \le 0$, indicating that total entropy can only be produced, not destroyed.

A [structure-preserving discretization](@entry_id:755564) should mimic this inequality at the discrete level. This leads to the concepts of **entropy-conservative** and **entropy-stable** schemes [@problem_id:3421663]. The key is again the numerical flux. A two-point numerical flux $\widehat{f}^{\mathrm{ec}}(u_L, u_R)$ is called entropy-conservative with respect to the pair $(U,F)$ if it produces zero numerical entropy at the interface. This is guaranteed if it satisfies Tadmor's condition:
$$
(\mathbf{v}_L - \mathbf{v}_R)^\top \widehat{f}^{\mathrm{ec}}(\mathbf{u}_L, \mathbf{u}_R) = \psi(\mathbf{u}_L) - \psi(\mathbf{u}_R)
$$
where $\mathbf{v}(\mathbf{u}) = (\nabla U(\mathbf{u}))^\top$ is the vector of entropy variables and $\psi(\mathbf{u})$ is a flux potential.

An entropy-[conservative scheme](@entry_id:747714) is a crucial building block, but to capture the physical dissipation of shocks, one needs an **entropy-stable** scheme. This is constructed by adding a carefully designed numerical dissipation term to an entropy-conservative flux:
$$
\widehat{f}^{\mathrm{es}}(\mathbf{u}_L, \mathbf{u}_R) = \widehat{f}^{\mathrm{ec}}(\mathbf{u}_L, \mathbf{u}_R) - \frac{1}{2} D(\mathbf{u}_L, \mathbf{u}_R)(\mathbf{v}_R - \mathbf{v}_L)
$$
where $D$ is a symmetric [positive semi-definite matrix](@entry_id:155265) that scales the amount of dissipation. This construction ensures that the numerical entropy production at the interface is non-positive, leading to a scheme where the total discrete entropy is non-increasing, thus satisfying a discrete analogue of the [second law of thermodynamics](@entry_id:142732).

#### Preservation of Equilibrium States: Well-Balanced Schemes

Many physical systems exhibit non-trivial [steady-state solutions](@entry_id:200351) where fluxes are perfectly balanced by source terms. A classic example is a lake at rest under gravity, governed by the [shallow water equations](@entry_id:175291) with a variable bottom topography $b(x)$ [@problem_id:3421678]:
$$
\partial_t h + \partial_x (h u) = 0
$$
$$
\partial_t (h u) + \partial_x \left(h u^2 + \tfrac{1}{2} g h^2\right) = - g h\, \partial_x b
$$
The "lake-at-rest" steady state is characterized by zero velocity ($u=0$) and a constant free surface elevation ($\eta = h+b = \text{const}$). In this state, the [momentum equation](@entry_id:197225) reduces to a perfect balance between the hydrostatic pressure gradient and the force from the bottom slope: $\partial_x (\frac{1}{2} g h^2) = -g h \partial_x b$.

A standard [numerical discretization](@entry_id:752782) often fails to preserve this delicate balance. Discretizing the flux gradient and the source term independently can introduce truncation errors that are misinterpreted as physical forces, generating spurious oscillations even in a perfectly still body of water. A **well-balanced** scheme is a structure-preserving method designed to maintain such steady states exactly at the discrete level.

Achieving this requires a careful, [compatible discretization](@entry_id:747533) of both the flux and source terms. A powerful technique is to rewrite the continuous balance identity, $g h \partial_x h + g h \partial_x b = 0$, and discretize it in a "split form" that algebraically preserves the cancellation. For a nodal collocation scheme with [differentiation matrix](@entry_id:149870) $D$, the volume contribution to the momentum residual can be formulated as $-g\,\mathrm{diag}(\mathbf{h}) (D\mathbf{h} + D\mathbf{b})$, where $\mathbf{h}$ and $\mathbf{b}$ are vectors of nodal values. This becomes $-g\,\mathrm{diag}(\mathbf{h}) D(\mathbf{h}+\mathbf{b}) = -g\,\mathrm{diag}(\mathbf{h}) D\boldsymbol{\eta}$. If the discrete state represents a constant surface elevation, then $D\boldsymbol{\eta} = \mathbf{0}$, and the residual contribution from the element's interior vanishes. This must be paired with a numerical flux at element interfaces that is also designed to respect this balance, ensuring that no spurious forces are generated at the boundaries between elements.

#### Preservation of Physical Admissibility: Positivity

Solutions to many physical models are only meaningful within a specific region of state space, known as the **admissible set**. For the compressible Euler equations, this means the density $\rho$ and pressure $p$ must be strictly positive. Standard [high-order methods](@entry_id:165413) can produce oscillations (Gibbs phenomenon) near sharp gradients, which may lead to undershoots that violate these physical constraints, causing the simulation to fail.

A **positivity-preserving** scheme is a structure-preserving method that guarantees the numerical solution remains within the admissible set [@problem_id:3421665]. For the Euler equations, the admissible set is $\mathcal{G} = \{ \mathbf{U} : \rho > 0, p(\mathbf{U}) > 0 \}$. A crucial mathematical property is that this set $\mathcal{G}$ is **convex**. This means for any two admissible states $\mathbf{U}_1, \mathbf{U}_2 \in \mathcal{G}$, any state on the line segment connecting them, $\theta \mathbf{U}_1 + (1-\theta) \mathbf{U}_2$ for $\theta \in [0,1]$, is also in $\mathcal{G}$.

This convexity is the foundation of modern [positivity-preserving limiters](@entry_id:753610). A typical strategy involves a two-step process:
1.  Ensure the cell-average solution is admissible. This can often be achieved by using a robust, positivity-preserving first-order scheme (like one using a monotone flux) as a baseline, under a suitable time-step restriction.
2.  Modify the high-order polynomial within the cell. If the high-order polynomial solution $\mathbf{U}_h(x)$ violates positivity at some point, it is corrected using a scaling [limiter](@entry_id:751283). For example, the solution is modified to $\mathbf{U}_h^{\text{new}}(x) = \theta \mathbf{U}_h(x) + (1-\theta) \overline{\mathbf{U}}$, where $\overline{\mathbf{U}}$ is the (admissible) cell average. Due to [convexity](@entry_id:138568), a scaling factor $\theta \in [0,1)$ can always be found to pull the entire polynomial solution back into the admissible set $\mathcal{G}$ while maintaining the original cell average, thereby preserving conservation.

This concept is fundamentally different from a maximum principle. A maximum principle for a scalar equation $u_t + \nabla \cdot \mathbf{f}(u) = 0$ enforces a two-sided bound, $u_{\min} \le u(x,t) \le u_{\max}$, on the solution variable itself. In contrast, positivity for the Euler system involves one-sided bounds on quantities ($\rho$ and $p$) that are nonlinear functions of the conserved [state vector](@entry_id:154607), and its enforcement relies critically on the [convexity](@entry_id:138568) of the state space.

### Core Discretization Mechanisms

To build schemes that preserve the structures described above, a specific set of numerical tools is required. These mechanisms are designed to provide discrete analogues of fundamental calculus operations, allowing the algebraic structure of the discrete equations to mimic the analytic structure of the PDEs.

#### The Summation-By-Parts (SBP) Property

A cornerstone of many modern [structure-preserving methods](@entry_id:755566) is the **Summation-By-Parts (SBP)** property. It is a discrete analogue of the integration-by-parts formula, which is fundamental to deriving conservation and stability properties of PDEs.

For a one-dimensional [spectral collocation](@entry_id:139404) method on an interval, we have a set of nodes, a [diagonal mass matrix](@entry_id:173002) $H$ containing positive [quadrature weights](@entry_id:753910), and a [differentiation matrix](@entry_id:149870) $D$ [@problem_id:3421636]. The discrete inner product of two grid functions $u$ and $v$ is defined as $(u, v)_H = u^\top H v$. The pair $(H,D)$ is said to satisfy the SBP property if the matrix $Q = HD$ is "almost" skew-symmetric. More precisely, it must satisfy:
$$
H D + D^\top H = B
$$
where $B$ is a [boundary operator](@entry_id:160216). For an interval $[-1, 1]$ with nodes at the endpoints, $B = e_n e_n^\top - e_1 e_1^\top$, where $e_1$ and $e_n$ are [standard basis vectors](@entry_id:152417) picking out the boundary points. This matrix identity is equivalent to the discrete integration-by-parts formula for any grid vectors $u$ and $v$:
$$
u^\top H (Dv) + (Du)^\top H v = u_n v_n - u_1 v_1
$$
This precisely mimics the continuous identity $\int_{-1}^1 (u v' + u' v) \, dx = u(1)v(1) - u(-1)v(-1)$. For [periodic domains](@entry_id:753347), the boundary terms cancel, and the SBP property simplifies to $HD + D^\top H = 0$, meaning $HD$ is skew-symmetric. This property is crucial for constructing discretizations that conserve quadratic quantities like energy. For nodal sets based on Gauss-Lobatto-Legendre points, the SBP property holds exactly for polynomials up to a certain degree, making it a powerful tool for [spectral methods](@entry_id:141737).

#### Split-Form Discretizations

Many of the structures discussed, such as [entropy stability](@entry_id:749023) and [well-balancing](@entry_id:756695), are achieved through a clever formulation of the nonlinear terms in the PDE, known as a **split form**. A nonlinear term can often be written in multiple, continuously equivalent ways. For example, the convective term in Burgers' equation, $(\frac{1}{2}u^2)_x$, can also be written as $u u_x$. At the discrete level, these forms are not equivalent. The "[conservative form](@entry_id:747710)" discretizes $(\frac{1}{2}u^2)_x$ directly as $D(\frac{1}{2}u \odot u)$, while the "advective form" discretizes $u u_x$ as $U D u$, where $U=\mathrm{diag}(u)$.

Neither of these forms may preserve the desired structure. A split-form discretization takes a convex combination of these (and potentially other) forms [@problem_id:3421661]. For Burgers' equation, a one-parameter family of split forms is:
$$
S_h^{(\alpha)}(u) = \alpha D\left(\frac{1}{2}u \odot u\right) + (1-\alpha) (U D u)
$$
By choosing the parameter $\alpha$ judiciously, we can enforce specific conservation properties. For example, to conserve the discrete kinetic energy $K_h(u) = \frac{1}{2} u^\top H u$ on a periodic domain (where the SBP property gives $HD = -D^\top H$), one must satisfy $u^\top H S_h^{(\alpha)}(u) = 0$. A detailed derivation shows that this condition holds for any $u$ if and only if $\alpha = 2/3$. The resulting split form, $S_h(u) = \frac{2}{3} D(\frac{1}{2}u \odot u) + \frac{1}{3} (U D u)$, is a kinetic-energy-preserving scheme. This technique of tuning a split form to satisfy a discrete conservation law is a powerful and widely used mechanism in [structure-preserving methods](@entry_id:755566).

#### Consistency on Curvilinear Grids: The Geometric Conservation Law

When applying [high-order methods](@entry_id:165413) to realistic problems, the computational domain is typically composed of curvilinear elements. This requires a mapping $\mathbf{x}(\boldsymbol{\xi})$ from a simple reference element (e.g., a cube) with coordinates $\boldsymbol{\xi}$ to the physical, curved element with coordinates $\mathbf{x}$. When the PDE is transformed to the reference element, geometric factors such as the Jacobian determinant $J$ and metric terms appear.

For the numerical scheme to be consistent, it must be able to exactly reproduce a uniform flow, or "free-stream" solution (e.g., $\mathbf{u}=\text{const}, p=\text{const}$). A naive [discretization](@entry_id:145012) on a curved mesh can fail to do this, leading to spurious solutions generated by the grid curvature itself. A scheme that correctly preserves a free-stream solution is said to satisfy the **Geometric Conservation Law (GCL)** [@problem_id:3421692].

The continuous GCL is a set of identities, known as the Piola identities, satisfied by the metric terms of the transformation: $\sum_i \frac{\partial}{\partial \xi^i} (J a_j^i) = 0$ for each physical direction $j=1, \dots, d$, where $J a_j^i$ are the scaled contravariant metric components. A structure-preserving scheme must satisfy the discrete analogue of these identities. If the scheme uses differentiation matrices $D_i$ to approximate $\partial/\partial \xi^i$, the discrete GCL takes the form of a set of algebraic constraints on the discretized metric terms:
$$
\sum_{i=1}^d D_i (J \mathbf{a}_j^i) = \mathbf{0} \quad \text{for each } j=1, \dots, d
$$
Here, $(J \mathbf{a}_j^i)$ is the vector of nodal values of the corresponding metric component. Satisfying this condition is non-trivial and requires that the geometry be represented and differentiated in a manner consistent with the [discretization](@entry_id:145012) of the solution variables. Using an isoparametric approach, where the geometry is represented by the same basis functions as the solution, and ensuring the same differentiation matrices are used for both the flux divergence and the GCL, is a key strategy for constructing robust [high-order schemes](@entry_id:750306) on [curvilinear grids](@entry_id:748121).

### Advanced Frameworks for Structure Preservation

While the mechanisms above provide specific tools for specific problems, a deeper understanding and more systematic construction of [structure-preserving methods](@entry_id:755566) can be achieved by appealing to higher-level mathematical frameworks that describe the geometry of the underlying equations.

#### Hamiltonian and Lagrangian Mechanics

Many conservative PDEs can be formulated within the framework of Lagrangian or Hamiltonian mechanics. A [semi-discretization](@entry_id:163562) that respects this structure leads to a system of ordinary differential equations (ODEs) that is also Lagrangian or Hamiltonian. This opens the door to the vast toolbox of **[geometric numerical integration](@entry_id:164206)**.

A semi-discrete system in canonical Hamiltonian form is written as $\dot{\mathbf{y}} = J \nabla H(\mathbf{y})$, where $H$ is the Hamiltonian (energy) and $J$ is a constant, [skew-symmetric matrix](@entry_id:155998). The exact flow of this system is a **symplectic map**, a transformation that preserves the geometric structure (the symplectic 2-form) of the phase space. A numerical time integrator is called **symplectic** if its one-step map is also a symplectic map.

Symplectic integrators, such as **Gauss-Legendre Runge-Kutta methods**, do not generally conserve the Hamiltonian $H$ exactly (unless $H$ is a quadratic function). However, they exhibit excellent long-time behavior, conserving a nearby "shadow" Hamiltonian and showing no long-term [energy drift](@entry_id:748982). Crucially, symplectic integrators exactly preserve all linear and quadratic [first integrals](@entry_id:261013) of the system [@problem_id:3421708]. For many semi-discrete PDEs, quantities like the discrete mass or momentum correspond to quadratic invariants. Therefore, applying a symplectic time integrator to the semi-discrete system guarantees the exact conservation of these important [physical quantities](@entry_id:177395), a property that is not shared by most conventional [time-stepping schemes](@entry_id:755998).

An even more foundational approach is provided by **[variational integrators](@entry_id:174311)** [@problem_id:3421641]. These methods are derived not by discretizing the [equations of motion](@entry_id:170720), but by first discretizing Hamilton's [principle of stationary action](@entry_id:151723). One defines a discrete Lagrangian $L_d(q_k, q_{k+1})$ that approximates the [action integral](@entry_id:156763) over one time step. The numerical trajectory is then found by extremizing the total discrete action, leading to the discrete Euler-Lagrange equations. This procedure automatically yields a symplectic (and momentum-preserving) integrator. Furthermore, this framework comes with a discrete version of **Noether's theorem**: if the discrete Lagrangian $L_d$ is invariant under a symmetry (e.g., phase rotation), then the numerical scheme possesses an exactly conserved discrete [momentum map](@entry_id:161822). This provides a profound and systematic connection between [symmetry and conservation](@entry_id:154858) at the fully discrete level.

#### A Unifying Topological Framework: Finite Element Exterior Calculus

Perhaps the most elegant and encompassing framework for structure-preserving [spatial discretization](@entry_id:172158) is **Finite Element Exterior Calculus (FEEC)** [@problem_id:3421688]. This framework uses the language of [differential forms](@entry_id:146747) and algebraic topology to build finite element spaces that inherently respect the structure of differential operators like gradient, curl, and divergence.

FEEC starts with the de Rham sequence, which for $\mathbb{R}^3$ connects the key function spaces of [vector calculus](@entry_id:146888):
$$
H^1 \xrightarrow{\nabla} H(\text{curl}) \xrightarrow{\nabla \times} H(\text{div}) \xrightarrow{\nabla \cdot} L^2
$$
This sequence is **exact**, meaning the image of each operator is the kernel of the next (e.g., the curl of any gradient is zero). FEEC constructs a corresponding sequence of finite element spaces $V_h^0 \subset H^1$, $V_h^1 \subset H(\text{curl})$, etc., that are compatible, meaning the discrete operators also form an [exact sequence](@entry_id:149883).

This is achieved by designing spaces where the degrees of freedom have a direct geometric interpretation (e.g., values at points, integrals along edges, fluxes across faces) and constructing a **discrete exterior derivative**, $d_h$, that is defined purely by the [mesh topology](@entry_id:167986) (its matrix representation consists only of 0, +1, and -1, encoding how mesh entities bound each other). This ensures the fundamental [topological property](@entry_id:141605) $d_h \circ d_h = 0$ holds. In contrast, the metric properties of the system are encapsulated in a separate operator, the **discrete Hodge star** $*_h$, which is represented by a [mass matrix](@entry_id:177093) that depends on the geometry of the elements. By separating the topological aspects (in $d_h$) from the metric aspects (in $*_h$), FEEC provides a powerful and systematic way to construct discretizations that preserve the deep geometric and topological structures of the underlying PDEs.