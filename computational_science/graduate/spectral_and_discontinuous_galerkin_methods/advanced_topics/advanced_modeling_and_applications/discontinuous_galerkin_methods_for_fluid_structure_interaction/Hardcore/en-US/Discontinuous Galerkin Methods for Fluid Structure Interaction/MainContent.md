## Introduction
Fluid-structure interaction (FSI) is a ubiquitous phenomenon governing the complex interplay between a moving fluid and a deformable solid. Its accurate prediction is critical in fields ranging from [aerospace engineering](@entry_id:268503), where it determines aircraft wing [flutter](@entry_id:749473), to biomechanics, where it describes blood flow through [heart valves](@entry_id:154991). However, simulating these interactions poses significant numerical challenges, including handling complex, moving geometries and robustly enforcing the tight coupling between disparate physical domains. The discontinuous Galerkin (DG) method has emerged as a particularly powerful and flexible framework for overcoming these hurdles, offering [high-order accuracy](@entry_id:163460), superior geometric flexibility, and a natural mechanism for [local adaptation](@entry_id:172044). This article provides a graduate-level exploration of DG methods for FSI, addressing the knowledge gap between single-physics solvers and the integrated approach required for coupled problems.

Over the next three chapters, you will build a comprehensive understanding of this cutting-edge technique. The journey begins in **"Principles and Mechanisms"**, which lays the essential theoretical and numerical foundation. Here, we will derive the governing equations, introduce the crucial Arbitrary Lagrangian-Eulerian (ALE) framework for moving domains, dissect the core principles of DG [discretization](@entry_id:145012), and analyze the critical stability issues that define modern FSI research, such as the notorious [added-mass instability](@entry_id:174360). Next, **"Applications and Interdisciplinary Connections"** showcases the remarkable versatility of the DG framework. We will explore its application to a wide range of advanced problems, including compressible and multiphase flows, [turbulence modeling](@entry_id:151192), and [contact mechanics](@entry_id:177379), highlighting its role as a key enabler for [multiphysics simulation](@entry_id:145294). Finally, **"Hands-On Practices"** will transition from theory to application, presenting a series of guided problems designed to solidify your understanding of key concepts, from analyzing basis functions to implementing a functional, albeit simplified, DG-FSI solver. We begin by establishing the fundamental principles that form the bedrock of this powerful methodology.

## Principles and Mechanisms

This chapter delineates the fundamental principles and numerical mechanisms underpinning the application of discontinuous Galerkin (DG) methods to [fluid-structure interaction](@entry_id:171183) (FSI) problems. We begin by establishing the mathematical model of the coupled physical system. Subsequently, we introduce the Arbitrary Lagrangian-Eulerian (ALE) framework, which is essential for computations on moving domains. The core of the chapter is then devoted to the principles of DG [spatial discretization](@entry_id:172158), including the treatment of second-order operators and the weak imposition of [interface conditions](@entry_id:750725). This is followed by a critical analysis of temporal [coupling strategies](@entry_id:747985), with a particular focus on the notorious [added-mass instability](@entry_id:174360) that challenges partitioned schemes. Finally, we conclude with a discussion of [energy stability](@entry_id:748991), which provides a unifying theoretical framework for designing robust DG-FSI solvers.

### Governing Equations of the Coupled System

A [fluid-structure interaction](@entry_id:171183) problem is fundamentally a [multiphysics](@entry_id:164478) problem defined over a composite domain that is partitioned into fluid and solid subdomains. A complete mathematical description requires specifying the governing equations within each subdomain along with the conditions that couple them across their common interface.

#### The Fluid Subdomain

We consider an incompressible, viscous Newtonian fluid occupying a time-dependent domain $\Omega_f(t)$. The motion of the fluid is governed by the incompressible Navier-Stokes equations, which represent the conservation of mass and linear momentum.

The **[conservation of mass](@entry_id:268004)** for an incompressible fluid is expressed as a kinematic constraint on the [velocity field](@entry_id:271461) $\boldsymbol{u}_f$:
$$
\nabla \cdot \boldsymbol{u}_f = 0 \quad \text{in } \Omega_f(t)
$$
This equation states that the [velocity field](@entry_id:271461) must be [divergence-free](@entry_id:190991), reflecting the assumption that fluid density $\rho_f$ is constant.

The **[conservation of linear momentum](@entry_id:165717)** is Newton's second law applied to a fluid continuum. In an Eulerian (spatial) frame of reference, it takes the form:
$$
\rho_f \left( \frac{\partial \boldsymbol{u}_f}{\partial t} + (\boldsymbol{u}_f \cdot \nabla) \boldsymbol{u}_f \right) = \nabla \cdot \boldsymbol{\sigma}_f + \boldsymbol{f}_f \quad \text{in } \Omega_f(t)
$$
Here, the left-hand side represents the mass times the acceleration of a fluid particle (the material derivative of velocity), while the right-hand side is the sum of [surface forces](@entry_id:188034), represented by the divergence of the Cauchy stress tensor $\boldsymbol{\sigma}_f$, and body forces per unit volume, $\boldsymbol{f}_f$. For a Newtonian fluid, the Cauchy stress is related to the fluid pressure $p_f$ and the [velocity field](@entry_id:271461) by the [constitutive relation](@entry_id:268485):
$$
\boldsymbol{\sigma}_f = -p_f \boldsymbol{I} + 2\mu_f \boldsymbol{\varepsilon}(\boldsymbol{u}_f)
$$
where $\boldsymbol{I}$ is the identity tensor, $\mu_f$ is the [dynamic viscosity](@entry_id:268228), and $\boldsymbol{\varepsilon}(\boldsymbol{u}_f)$ is the symmetric [rate-of-strain tensor](@entry_id:260652), defined as $\boldsymbol{\varepsilon}(\boldsymbol{u}_f) = \frac{1}{2} (\nabla \boldsymbol{u}_f + (\nabla \boldsymbol{u}_f)^\top)$.

#### The Solid Subdomain

The deformable structure is modeled as a linearly elastic solid occupying a domain $\Omega_s$. For many FSI problems, particularly in biomechanics and aerospace, the structural displacements are small, justifying the use of linear [elastodynamics](@entry_id:175818). The governing equation is the [conservation of linear momentum](@entry_id:165717):
$$
\rho_s \frac{\partial^2 \boldsymbol{d}_s}{\partial t^2} = \nabla \cdot \boldsymbol{\sigma}_s + \boldsymbol{f}_s \quad \text{in } \Omega_s
$$
Here, $\rho_s$ is the solid density, $\boldsymbol{d}_s$ is the [displacement field](@entry_id:141476), $\frac{\partial^2 \boldsymbol{d}_s}{\partial t^2}$ is the [local acceleration](@entry_id:272847), $\boldsymbol{\sigma}_s$ is the Cauchy stress tensor in the solid, and $\boldsymbol{f}_s$ represents body forces.

For a linear, isotropic elastic material under the small-strain assumption, the stress is related to the strain by Hooke's law:
$$
\boldsymbol{\sigma}_s = \lambda_s \mathrm{tr}(\boldsymbol{\varepsilon}(\boldsymbol{d}_s)) \boldsymbol{I} + 2\mu_s \boldsymbol{\varepsilon}(\boldsymbol{d}_s)
$$
where $\lambda_s$ and $\mu_s$ are the Lamé parameters of the solid, and $\boldsymbol{\varepsilon}(\boldsymbol{d}_s)$ is the [infinitesimal strain tensor](@entry_id:167211), given by $\boldsymbol{\varepsilon}(\boldsymbol{d}_s) = \frac{1}{2} (\nabla \boldsymbol{d}_s + (\nabla \boldsymbol{d}_s)^\top)$.

#### The Fluid-Structure Interface

The fluid and solid subdomains are coupled by physical conditions on their shared interface, $\Gamma_{fs}(t)$. These conditions enforce the continuity of motion and the balance of forces .

The **kinematic condition** dictates that the fluid and solid must move together at the interface, without separation or interpenetration. This implies that their velocities must be identical. The velocity of the fluid at the interface is the trace of $\boldsymbol{u}_f$, while the material velocity of the solid is the time derivative of its displacement, $\dot{\boldsymbol{d}}_s = \frac{\partial \boldsymbol{d}_s}{\partial t}$. Thus, the kinematic condition is a no-slip condition:
$$
\boldsymbol{u}_f = \dot{\boldsymbol{d}}_s \quad \text{on } \Gamma_{fs}(t)
$$
This vector equation enforces the equality of both normal and tangential velocity components.

The **dynamic condition** enforces the equilibrium of forces across the interface, as required by Newton's third law ([action-reaction principle](@entry_id:195494)). The force per unit area exerted by one medium on another is the [traction vector](@entry_id:189429), $\boldsymbol{t} = \boldsymbol{\sigma} \boldsymbol{n}$, where $\boldsymbol{n}$ is the unit normal to the surface. Let us define a single unit normal $\boldsymbol{n}$ on $\Gamma_{fs}(t)$ that points from the fluid domain into the solid domain. The outward normal for the fluid is thus $\boldsymbol{n}_f = \boldsymbol{n}$, and the outward normal for the solid is $\boldsymbol{n}_s = -\boldsymbol{n}$.
The traction exerted by the fluid on the solid is $\boldsymbol{t}_f = \boldsymbol{\sigma}_f \boldsymbol{n}_f = \boldsymbol{\sigma}_f \boldsymbol{n}$.
The traction exerted by the solid on the fluid is $\boldsymbol{t}_s = \boldsymbol{\sigma}_s \boldsymbol{n}_s = \boldsymbol{\sigma}_s (-\boldsymbol{n})$.
Newton's third law requires that these tractions be equal and opposite: $\boldsymbol{t}_f = -\boldsymbol{t}_s$. Substituting the expressions gives:
$$
\boldsymbol{\sigma}_f \boldsymbol{n} = -(\boldsymbol{\sigma}_s (-\boldsymbol{n})) \implies \boldsymbol{\sigma}_f \boldsymbol{n} = \boldsymbol{\sigma}_s \boldsymbol{n}
$$
This fundamental result states that the traction vector must be continuous across the interface. This single vector equation ensures the continuity of both [normal and tangential components](@entry_id:166204) of the traction.

### The Arbitrary Lagrangian-Eulerian (ALE) Formulation

A central challenge in FSI is that the fluid domain $\Omega_f(t)$ deforms in time. A purely Eulerian description (fixed grid) is ill-suited for tracking the moving interface, while a purely Lagrangian description (grid moves with fluid particles) can suffer from severe mesh distortion. The **Arbitrary Lagrangian-Eulerian (ALE)** formulation provides a powerful hybrid approach.

In the ALE framework, the computational mesh is allowed to move with an arbitrary velocity $\boldsymbol{w}$, independent of the fluid material velocity $\boldsymbol{u}_f$. This provides the flexibility to have the mesh conform to the moving fluid-structure interface (i.e., $\boldsymbol{w} = \dot{\boldsymbol{d}}_s$ on $\Gamma_{fs}(t)$) while smoothly deforming in the interior of the domain to maintain [mesh quality](@entry_id:151343).

To formalize this, we introduce a time-independent **reference domain** $\hat{\Omega}$ with coordinates $\boldsymbol{\xi}$. The time-dependent **physical domain** $\Omega(t)$ with coordinates $\boldsymbol{x}$ is described by an invertible **ALE mapping** $\boldsymbol{\chi}$:
$$
\boldsymbol{x} = \boldsymbol{\chi}(\boldsymbol{\xi}, t), \quad \Omega(t) = \boldsymbol{\chi}(\hat{\Omega}, t)
$$
The **mesh velocity** $\boldsymbol{w}$ is the velocity of a point with a fixed reference coordinate $\boldsymbol{\xi}$:
$$
\boldsymbol{w}(\boldsymbol{x}, t) = \frac{\partial \boldsymbol{\chi}}{\partial t} \bigg|_{\boldsymbol{\xi} = \boldsymbol{\chi}^{-1}(\boldsymbol{x},t)}
$$
The governing equations must be reformulated to account for this [mesh motion](@entry_id:163293). Starting from a generic conservation law in Eulerian form, $\partial_t U + \nabla \cdot F(U) = 0$, the corresponding conservative ALE form can be derived using the Reynolds Transport Theorem for a [moving control volume](@entry_id:265261) . The result is:
$$
\frac{\partial U}{\partial t}\bigg|_{\boldsymbol{x}} + \nabla \cdot (F(U) - U \otimes \boldsymbol{w}) = 0
$$
The term $(\boldsymbol{u}_f - \boldsymbol{w})$ is the **convective velocity**, representing the velocity of the fluid relative to the [moving mesh](@entry_id:752196). The flux $F(U)$ is thus corrected by the term $-U \otimes \boldsymbol{w}$, which accounts for the flux of the quantity $U$ due to the motion of the control volume boundary itself. For the Navier-Stokes [momentum equation](@entry_id:197225), this results in the convective term $\nabla \cdot (\rho_f \boldsymbol{u}_f \otimes (\boldsymbol{u}_f - \boldsymbol{w}))$.

A critical component of a stable ALE formulation is the satisfaction of the **Geometric Conservation Law (GCL)**. This law ensures that the numerical scheme correctly accounts for the change in an element's volume due to [mesh motion](@entry_id:163293). Let $J = \det(\nabla_{\boldsymbol{\xi}} \boldsymbol{\chi})$ be the Jacobian determinant of the ALE mapping. The GCL is a kinematic identity relating the [time evolution](@entry_id:153943) of $J$ to the divergence of the mesh velocity $\boldsymbol{w}$:
$$
\frac{\partial J}{\partial t} - \nabla_{\boldsymbol{\xi}} \cdot (J \boldsymbol{G}^{-1} \boldsymbol{w}) = 0 \quad \text{or equivalently} \quad \frac{\partial J}{\partial t} - J (\nabla_{\boldsymbol{x}} \cdot \boldsymbol{w}) = 0
$$
where $\boldsymbol{G} = \nabla_{\boldsymbol{\xi}} \boldsymbol{\chi}$ is the Jacobian matrix. A numerical scheme must satisfy a discrete version of the GCL. Failure to do so can lead to the creation of artificial mass or momentum simply due to [mesh motion](@entry_id:163293), violating the fundamental principle of **free-stream preservation**, which requires that a [uniform flow](@entry_id:272775) field remains undisturbed by the computation .

For high-order DG methods on domains with curved boundaries, the geometry itself is represented by polynomials. In an **[isoparametric mapping](@entry_id:173239)**, the same polynomial basis used for the solution is used to represent the geometry. In this case, free-stream preservation requires not only satisfying the GCL for moving meshes, but also satisfying certain stationary metric identities, such as the **Piola identity** ($\nabla_{\boldsymbol{\xi}} \cdot (J \boldsymbol{G}^{-\top}) = \boldsymbol{0}$), in a discrete sense. These identities are automatically satisfied for exact mappings but must be carefully preserved by the discrete representation to avoid introducing geometric errors .

### Discontinuous Galerkin Discretization Principles

Discontinuous Galerkin methods are particularly well-suited for FSI problems due to their [high-order accuracy](@entry_id:163460), [local conservation](@entry_id:751393) properties, robustness on complex geometries, and flexibility in handling [hanging nodes](@entry_id:750145) and varying polynomial degrees ($p$-adaptivity). The core idea of DG is to seek a solution in a space of functions that are polynomials within each element but are allowed to be discontinuous across element boundaries. Communication between elements is achieved weakly through **numerical fluxes** that replace the true solution values and their derivatives at the interfaces.

#### Discretization of Second-Order Elliptic Operators

A key challenge in DG methods is the discretization of second-order terms, such as the viscous operator $-\nabla \cdot (2\mu \boldsymbol{\varepsilon}(\boldsymbol{u}))$ in the fluid and the elastic operator in the solid. Several families of methods exist, each with different trade-offs in terms of computational cost, implementation complexity, and mathematical properties .

The **Symmetric Interior Penalty Galerkin (SIPG)** method is a widely used and well-understood approach. It is derived by integrating the [weak form](@entry_id:137295) by parts twice, leading to a symmetric formulation. To ensure [coercivity](@entry_id:159399) and stability, the formulation must be augmented with a penalty term that acts on the jump of the solution across element faces. For a viscous term, the [numerical flux](@entry_id:145174) involves a penalty proportional to $\eta_f [[\boldsymbol{u}_h]]$, where $[[\cdot]]$ denotes the [jump operator](@entry_id:155707) and the penalty parameter $\eta_f$ must be sufficiently large, typically scaling as $\eta_f \sim \mu_f k^2/h$ for polynomial degree $k$ and element size $h$. SIPG is consistent, symmetric, and locally conservative.

Alternative approaches are based on rewriting the second-order equation as a system of first-order equations. The **Local Discontinuous Galerkin (LDG)** method introduces an auxiliary variable for the gradient (e.g., $\boldsymbol{q} = \nabla \boldsymbol{u}_h$) and solves a coupled [first-order system](@entry_id:274311). Stability is achieved through a careful choice of alternating upwind/downwind numerical fluxes for the primal and auxiliary variables. This avoids the need for a large penalty parameter but increases the number of unknowns. The resulting system for the primal variable alone is generally non-symmetric but remains locally conservative.

The **Bassi-Rebay 2 (BR2)** method provides a compromise that avoids both the large explicit penalties of SIPG and the auxiliary variables of LDG . The BR2 method constructs a stable, high-order approximation to the gradient within each element by augmenting the element-wise gradient with a correction term. This correction is computed using a **local [lifting operator](@entry_id:751273)**, which maps the jump of the solution on the element boundary to a polynomial within the element's volume. This reconstructed gradient is then used to define the [viscous stress](@entry_id:261328). Stability is achieved implicitly through this reconstruction, as the [lifting operator](@entry_id:751273) provides control over the solution jumps. Like SIPG, the BR2 method is symmetric and locally conservative.

#### Weak Imposition of Boundary and Interface Conditions

A powerful feature of DG methods is their ability to impose boundary conditions weakly through the numerical flux machinery. This is particularly advantageous for the Dirichlet-type kinematic condition $\boldsymbol{u}_f = \dot{\boldsymbol{d}}_s$ at the fluid-structure interface.

**Nitsche's method** is a general and elegant technique for weakly enforcing such conditions . For the FSI problem, it involves modifying the viscous and elastic terms in the weak form at the interface $\Gamma_{fs}$. The symmetric Nitsche formulation for the viscous operator on the fluid side includes three boundary integrals over $\Gamma_{fs}$:
1.  The standard consistency term, $-\int_{\Gamma_{fs}} (2\mu_f \boldsymbol{\varepsilon}(\boldsymbol{u}_h)\boldsymbol{n}) \cdot \boldsymbol{v} \, ds$, arising from [integration by parts](@entry_id:136350).
2.  An [adjoint consistency](@entry_id:746293) (or symmetry) term, $-\int_{\Gamma_{fs}} (2\mu_f \boldsymbol{\varepsilon}(\boldsymbol{v})\boldsymbol{n}) \cdot (\boldsymbol{u}_h - \dot{\boldsymbol{d}}_s) \, ds$, which ensures symmetry of the resulting [bilinear form](@entry_id:140194).
3.  A penalty term, $+\int_{\Gamma_{fs}} \tau (\boldsymbol{u}_h - \dot{\boldsymbol{d}}_s) \cdot \boldsymbol{v} \, ds$, which penalizes the violation of the kinematic condition.

For stability, the penalty parameter $\tau$ must be sufficiently large, scaling similarly to the SIPG penalty, i.e., $\tau \sim \mu_f k^2/h$. This method is both consistent (an exact solution satisfying the condition makes the extra terms vanish) and stable.

For convective terms at external boundaries, weak imposition is achieved via **upwind fluxes** in the ALE frame. Whether a boundary is an inflow or outflow boundary depends on the sign of the normal component of the *[relative velocity](@entry_id:178060)*. For a boundary with normal $\boldsymbol{n}$:
-   If $(\boldsymbol{u}_f - \boldsymbol{w}) \cdot \boldsymbol{n} \ge 0$, it is an **outflow** boundary, and the state for the flux should be taken from the interior of the domain.
-   If $(\boldsymbol{u}_f - \boldsymbol{w}) \cdot \boldsymbol{n}  0$, it is an **inflow** boundary, and the state should be taken from prescribed exterior/far-field data .

### Temporal Coupling Strategies and Stability

After [spatial discretization](@entry_id:172158), the FSI problem becomes a large system of [ordinary differential equations](@entry_id:147024) (ODEs) in time. The strategy for solving this coupled system is a critical design choice that profoundly impacts stability, accuracy, and computational cost. Two main approaches exist: monolithic and partitioned.

#### Monolithic vs. Partitioned Schemes

In a **monolithic** approach, the discrete equations for the fluid, the structure, and the [interface coupling](@entry_id:750728) are assembled into a single, large algebraic system to be solved simultaneously at each time step.
-   **Advantages**: This tight coupling fully captures the interaction between the sub-domains. As a result, [monolithic schemes](@entry_id:171266) are generally more robust and stable, especially for challenging problems. They satisfy the [interface conditions](@entry_id:750725) up to the tolerance of the algebraic solver at each time step without requiring sub-iterations .
-   **Disadvantages**: The primary drawback is complexity and cost. It requires developing a specialized solver for the large, multi-physics matrix system, which is often non-symmetric and ill-conditioned. Efficient solution almost always necessitates advanced, problem-specific **[block preconditioners](@entry_id:163449)** that approximate the inverse of the system or its Schur complement.

In a **partitioned** (or staggered) approach, the fluid and solid sub-problems are solved sequentially within each time step. Data, such as interface position and traction, are exchanged between the solvers.
-   **Advantages**: The main appeal of partitioned schemes is **modularity**. They allow for the reuse of existing, highly optimized single-physics solvers for the fluid and solid domains. This significantly simplifies implementation .
-   **Disadvantages**: The explicit treatment of the [interface coupling](@entry_id:750728) introduces a lag, which can lead to numerical instabilities and inaccuracies. To achieve the same level of accuracy and consistency as a [monolithic scheme](@entry_id:178657), multiple **interface iterations** (e.g., Gauss-Seidel or Jacobi fixed-point iterations) are typically required within each time step until the [interface conditions](@entry_id:750725) converge.

#### The Added-Mass Instability in Partitioned Schemes

The most significant challenge for partitioned schemes is the **[added-mass instability](@entry_id:174360)**. This instability arises in problems where a light structure is coupled with a dense, incompressible fluid (e.g., blood flow with leaflets, parachutes in air).

The physical origin of the **[added mass](@entry_id:267870)** is the inertia of the fluid that is accelerated or decelerated by the moving structure. When the structure moves, it must displace the surrounding fluid, and the resulting pressure field exerts a reaction force on the structure that is proportional to the structure's acceleration. In a simplified 1D model of a piston of mass $m_s$ driving an [incompressible fluid](@entry_id:262924) of density $\rho_f$ in a channel of length $L$ and area $A$, this reaction force results in an effective inertial term, the [added mass](@entry_id:267870) $m_a = \rho_f A L$. The [equation of motion](@entry_id:264286) for the structure becomes $(m_s + m_a)\ddot{\eta} + \dots = 0$ .

In an explicit [partitioned scheme](@entry_id:172124), the fluid force (containing the [added-mass effect](@entry_id:746267)) used to update the structure at the current time step is calculated using data from a previous time step or iteration. This lag in the inertial coupling is the source of the [numerical instability](@entry_id:137058). A stability analysis of a simple [partitioned scheme](@entry_id:172124) shows that the interface iterations diverge if the added-mass ratio $r = m_a/m_s$ is greater than one [@problem_id:3379607, @problem_id:3379666]. The amplification factor of the error in successive iterations scales as $-m_a/m_s$. Therefore, if $m_a > m_s$, the scheme is unconditionally unstable, regardless of how small the time step $\Delta t$ is made.

This explains why problems with light structures (small $m_s$) and dense fluids (large $\rho_f$, leading to large $m_a$) are so challenging for partitioned schemes. While refining the mesh near the interface can reduce the effective numerical added mass (which scales with the element size $h$), it cannot guarantee stability if the physical mass ratio is unfavorable . In contrast, [monolithic schemes](@entry_id:171266) or strongly-coupled partitioned schemes that iterate to convergence correctly place the added mass term on the left-hand side of the algebraic system, implicitly coupling the fluid and structural inertia and thus completely avoiding this instability [@problem_id:3379666, @problem_id:3379681].

### Energy Stability of the Coupled DG-FSI System

A powerful approach for analyzing and designing robust numerical schemes is to mimic the energy conservation/dissipation properties of the underlying physical system. For a closed FSI system with no external work, the total energy (fluid kinetic + solid kinetic + solid elastic potential) should not increase over time; it should only be dissipated by viscosity. A DG-FSI scheme can be designed to satisfy a discrete analogue of this principle, guaranteeing its non-linear stability .

The semi-discrete total energy for the coupled system is defined as:
$$
E_h(t) := \sum_{K \subset \Omega_f} \int_K \frac{1}{2} \rho_f |\boldsymbol{u}_h|^2 \, dx + \sum_{K \subset \Omega_s} \int_K \left( \frac{1}{2} \rho_s |\boldsymbol{v}_h^s|^2 + \mu_s \boldsymbol{\varepsilon}(\boldsymbol{d}_h) : \boldsymbol{\varepsilon}(\boldsymbol{d}_h) \right) dx
$$
To ensure that $\frac{d}{dt} E_h(t) \le 0$, each component of the DG formulation must contribute in an energy-stable manner when the discrete momentum equations are tested with the corresponding velocity fields:

1.  **Convective Term**: The discrete fluid convection operator must not produce energy. This is often achieved by writing it in a skew-symmetric form, which contributes zero to the [energy balance](@entry_id:150831) for a [divergence-free flow](@entry_id:748605).

2.  **Pressure Terms**: The [pressure-velocity coupling](@entry_id:155962) must do no [net work](@entry_id:195817). This is naturally satisfied in DG formulations where the discrete divergence and gradient operators are skew-adjoint.

3.  **Viscous/Elastic Dissipation**: The discretization of the viscous and elastic stress terms must be dissipative. This is ensured by using coercive formulations like SIPG, where the associated [bilinear form](@entry_id:140194) is [positive semi-definite](@entry_id:262808). The required penalty terms contribute non-negative dissipation.

4.  **Interface Coupling**: The numerical fluxes at the fluid-structure interface must not generate energy. A symmetric, adjoint-consistent Nitsche-type coupling ensures that the power exchanged between the fluid and the solid sums to a non-positive quantity. The non-penalty terms cancel out in an action-reaction manner, while the penalty term provides a non-negative dissipation proportional to the square of the velocity mismatch at the interface.

By carefully selecting each component of the numerical scheme to satisfy these properties, one can construct a DG-FSI method that is provably energy-stable by design. This provides a high degree of confidence in the robustness of the method, particularly for long-time simulations of complex, non-linear interactions.