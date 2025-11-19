## Introduction
Fluid-structure interaction (FSI) describes the complex interplay between a deformable structure and an internal or surrounding fluid flow. This phenomenon is central to a vast range of applications, from the aerodynamic [flutter](@entry_id:749473) of an aircraft wing to the mechanics of a heart valve. The primary challenge in this field lies in developing robust, accurate, and efficient [numerical algorithms](@entry_id:752770) to solve the tightly coupled governing equations on domains with moving and deforming boundaries. This gap between physical reality and computational simulation is a critical hurdle for predictive engineering.

This article provides a comprehensive overview of the algorithms at the heart of modern FSI simulation. You will begin in the "Principles and Mechanisms" chapter by exploring the fundamental governing equations and the Arbitrary Lagrangian-Eulerian (ALE) formulation, which provides a framework for handling moving domains. We will then dissect the two primary algorithmic architectures: robust [monolithic schemes](@entry_id:171266) and modular partitioned schemes. The "Applications and Interdisciplinary Connections" chapter will delve into the practical challenges encountered in real-world scenarios, with a particular focus on the notorious [added-mass instability](@entry_id:174360) and the advanced strategies developed to overcome it. Finally, the "Hands-On Practices" section offers a series of focused problems to solidify your understanding of these theoretical concepts.

We begin our exploration by establishing the mathematical and physical foundations that underpin all FSI simulations.

## Principles and Mechanisms

Fluid-structure interaction (FSI) problems are governed by the fundamental laws of [continuum mechanics](@entry_id:155125) applied to both a fluid and a solid, coupled by conditions that must be satisfied at their shared, and often moving, interface. The development of robust and accurate [numerical algorithms](@entry_id:752770) to solve these coupled equations requires a careful consideration of the mathematical formulation, the [discretization](@entry_id:145012) strategy, and the algorithmic architecture used to handle the interplay between the two physical domains. This chapter elucidates the core principles and mechanisms underpinning modern FSI algorithms.

### The Coupled FSI Problem: Governing Equations and Interface Conditions

At the heart of any FSI problem lies a system of partial differential equations describing the behavior of the constituent media. Typically, the fluid is described in an **Eulerian** (spatial) frame, where the governing equations are posed at fixed points in space, while the solid is described in a **Lagrangian** (material) frame, where equations track the motion of individual material particles.

For an incompressible Newtonian fluid occupying a time-dependent domain $\Omega_f(t)$, the governing equations are the Navier-Stokes equations, which express conservation of mass ([incompressibility](@entry_id:274914)) and [linear momentum](@entry_id:174467):
$$ \nabla \cdot \boldsymbol{u}_f = 0 $$
$$ \rho_f \left( \frac{\partial \boldsymbol{u}_f}{\partial t} + (\boldsymbol{u}_f \cdot \nabla)\boldsymbol{u}_f \right) = \nabla \cdot \boldsymbol{\sigma}_f + \rho_f \boldsymbol{b}_f $$
Here, $\boldsymbol{u}_f(\boldsymbol{x},t)$ is the fluid velocity at spatial position $\boldsymbol{x}$ and time $t$, $\rho_f$ is the constant fluid density, and $\boldsymbol{b}_f$ is the [body force](@entry_id:184443) per unit mass. The fluid's Cauchy stress tensor, $\boldsymbol{\sigma}_f$, is given by:
$$ \boldsymbol{\sigma}_f = -p \boldsymbol{I} + \mu_f\left( \nabla \boldsymbol{u}_f + (\nabla \boldsymbol{u}_f)^{\top} \right) $$
where $p(\boldsymbol{x},t)$ is the fluid pressure, $\boldsymbol{I}$ is the identity tensor, and $\mu_f$ is the [dynamic viscosity](@entry_id:268228).

For a hyperelastic solid, we typically track its motion relative to a reference configuration $\Omega_s^0$. The position of a solid particle at time $t$ is given by the motion $\boldsymbol{x} = \boldsymbol{\phi}_s(\boldsymbol{X},t) = \boldsymbol{X} + \boldsymbol{d}_s(\boldsymbol{X},t)$, where $\boldsymbol{X}$ is its position in the reference configuration and $\boldsymbol{d}_s$ is the [displacement field](@entry_id:141476). The solid's deformation is characterized by the [deformation gradient tensor](@entry_id:150370), $\boldsymbol{F} = \nabla_{\boldsymbol{X}} \boldsymbol{d}_s + \boldsymbol{I}$. The [conservation of linear momentum](@entry_id:165717) in the reference frame is:
$$ \rho_s^0 \frac{\partial^2 \boldsymbol{d}_s}{\partial t^2} = \nabla_{\boldsymbol{X}} \cdot \boldsymbol{P}_s + \rho_s^0 \boldsymbol{B}_s $$
where $\rho_s^0$ is the reference density, $\boldsymbol{B}_s$ is the reference [body force](@entry_id:184443), and $\boldsymbol{P}_s$ is the first Piola-Kirchhoff (PK1) stress tensor. For a [hyperelastic material](@entry_id:195319), $\boldsymbol{P}_s$ is derived from a [stored-energy function](@entry_id:197811) $W(\boldsymbol{F})$ as $\boldsymbol{P}_s = \frac{\partial W}{\partial \boldsymbol{F}}$.

These two physical systems are coupled at their common, moving interface $\Gamma(t)$. Two fundamental conditions must be enforced on $\Gamma(t)$:
1.  **Kinematic Condition**: For a viscous fluid, the no-slip and [no-penetration condition](@entry_id:191795) dictates that the [fluid velocity](@entry_id:267320) at the interface must equal the velocity of the solid boundary.
    $$ \boldsymbol{u}_f(\boldsymbol{x},t) = \frac{\partial \boldsymbol{d}_s}{\partial t}(\boldsymbol{X},t) \quad \text{for } \boldsymbol{x} = \boldsymbol{\phi}_s(\boldsymbol{X},t) $$
2.  **Dynamic Condition**: Newton's third law requires that the traction (force per unit area) exerted by the fluid on the solid is equal and opposite to the traction exerted by the solid on the fluid. This is expressed as the continuity of traction vectors across the interface. When stated in the current configuration, this is:
    $$ \boldsymbol{\sigma}_f(\boldsymbol{x},t) \boldsymbol{n}(\boldsymbol{x},t) = \boldsymbol{\sigma}_s(\boldsymbol{x},t) \boldsymbol{n}(\boldsymbol{x},t) $$
    Here, $\boldsymbol{n}$ is the [unit normal vector](@entry_id:178851) on the interface, and $\boldsymbol{\sigma}_s$ is the Cauchy stress in the solid, related to the PK1 stress by the transformation $\boldsymbol{\sigma}_s = J_s^{-1} \boldsymbol{P}_s \boldsymbol{F}^{\top}$, with $J_s = \det(\boldsymbol{F})$.

The core challenge of FSI is to simultaneously solve these two sets of governing equations while satisfying the kinematic and dynamic coupling conditions on a boundary whose position is itself part of the solution [@problem_id:3566594].

### The Arbitrary Lagrangian-Eulerian (ALE) Formulation

The dual Lagrangian and Eulerian perspectives pose a significant challenge for [numerical discretization](@entry_id:752782), especially for the fluid. If the fluid mesh is fixed in space (Eulerian), the interface cuts through grid cells, complicating the application of boundary conditions. If the fluid mesh moves with the fluid particles (Lagrangian), it can become excessively distorted.

The **Arbitrary Lagrangian-Eulerian (ALE)** formulation resolves this dilemma. It introduces a third coordinate system: a reference domain $\widehat{\Omega}_f$ which is mapped to the current, physical fluid domain $\Omega_f(t)$ by a time-dependent mapping $\boldsymbol{x} = \boldsymbol{\chi}(\boldsymbol{X}, t)$. The key idea is that the motion of the reference coordinates $\boldsymbol{X}$ is arbitrary and can be chosen for numerical convenience, for example, to keep the mesh nodes well-distributed.

The velocity of a point with a fixed reference coordinate is the **mesh velocity**, $\boldsymbol{w}(\boldsymbol{x}, t) = \frac{\partial \boldsymbol{\chi}}{\partial t}\big|_{\boldsymbol{X}}$. This is distinct from the fluid material velocity $\boldsymbol{u}_f$. The time derivative of a fluid property $f(\boldsymbol{x}, t)$ as seen by an observer moving with the ALE mesh is given by the ALE time derivative, which relates the time derivative at a fixed reference point $\boldsymbol{X}$ to the standard Eulerian time derivative at a fixed spatial point $\boldsymbol{x}$:
$$ \frac{\partial \widehat{f}}{\partial t}(\boldsymbol{X},t) \equiv \frac{\partial f}{\partial t}\bigg|_{\boldsymbol{X}} = \frac{\partial f}{\partial t}\bigg|_{\boldsymbol{x}} + (\boldsymbol{w} \cdot \nabla_{\boldsymbol{x}}) f $$
This allows us to rewrite the fluid [momentum equation](@entry_id:197225). The [material derivative](@entry_id:266939), which represents the acceleration of a fluid particle, becomes:
$$ \frac{D\boldsymbol{u}_f}{Dt} = \frac{\partial \boldsymbol{u}_f}{\partial t}\bigg|_{\boldsymbol{x}} + (\boldsymbol{u}_f \cdot \nabla_{\boldsymbol{x}})\boldsymbol{u}_f = \frac{\partial \widehat{\boldsymbol{u}}_f}{\partial t}\bigg|_{\boldsymbol{X}} + ((\boldsymbol{u}_f - \boldsymbol{w}) \cdot \nabla_{\boldsymbol{x}})\boldsymbol{u}_f $$
The term $\boldsymbol{c} = \boldsymbol{u}_f - \boldsymbol{w}$ is the **convective velocity**—the velocity of the fluid relative to the [moving mesh](@entry_id:752196). This is the velocity that is responsible for advective transport in the ALE frame [@problem_id:3566527].

A critical aspect of the ALE formulation is ensuring that the computational fluid domain conforms to the moving solid boundary. This is achieved by imposing a kinematic condition on the [mesh motion](@entry_id:163293) at the interface. Specifically, we require the mesh velocity to match the solid velocity on $\Gamma(t)$:
$$ \boldsymbol{w} = \dot{\boldsymbol{d}}_s \quad \text{on } \Gamma(t) $$
This condition ensures **grid conformity**. By setting the velocity of the fluid mesh boundary points equal to the velocity of the structural boundary points, we ensure that their trajectories are governed by the same ordinary differential equation. If they start at the same position, the uniqueness of the solution to this ODE guarantees they will remain coincident for all time [@problem_id:3566517].

This choice has a profound consequence for the physics at the interface. On the no-slip interface $\Gamma(t)$, we must satisfy both the physical condition $\boldsymbol{u}_f = \dot{\boldsymbol{d}}_s$ and the mesh-conformity condition $\boldsymbol{w} = \dot{\boldsymbol{d}}_s$. It immediately follows that:
$$ \boldsymbol{u}_f = \boldsymbol{w} \quad \text{on } \Gamma(t) $$
This implies that the convective velocity $\boldsymbol{c} = \boldsymbol{u}_f - \boldsymbol{w}$ is zero at the interface. As a result, there is no advective flux of mass, momentum, or energy across the moving boundary. All physical transport of force and energy between the fluid and the structure occurs through the diffusive terms: pressure and viscous stresses. This is a fundamental property of conforming-mesh FSI formulations [@problem_id:3566528].

### Algorithmic Architectures

With a suitable mathematical framework like ALE, the discretized FSI equations must be solved at each time step. The choice of solution strategy leads to two main families of algorithms: monolithic and partitioned.

#### Monolithic Schemes

In a **monolithic** (or fully coupled) approach, the discrete equations for the fluid, the solid, and the [interface conditions](@entry_id:750725) are assembled into a single, large algebraic system. All primary unknowns—such as the fluid velocity $\boldsymbol{u}_f$, [fluid pressure](@entry_id:270067) $p$, and solid displacement $\boldsymbol{d}_s$—are solved for simultaneously.

After linearization (e.g., via the Newton-Raphson method), a typical monolithic system for the unknown updates $(\delta \boldsymbol{u}, \delta \boldsymbol{d}, \delta \boldsymbol{\lambda})$ can be written in a [block matrix](@entry_id:148435) form. For instance, when using Lagrange multipliers $\boldsymbol{\lambda}$ to enforce the kinematic constraint, the system often takes a characteristic saddle-point structure [@problem_id:3566503]:
$$
\begin{bmatrix}
\boldsymbol{A}_f  & \boldsymbol{0}  & \boldsymbol{C}_f^T \\
\boldsymbol{0}  & \boldsymbol{A}_s  & \boldsymbol{C}_s^T \\
\boldsymbol{C}_f  & \boldsymbol{C}_s  & \boldsymbol{0}
\end{bmatrix}
\begin{bmatrix}
\delta \boldsymbol{u} \\
\delta \boldsymbol{d} \\
\delta \boldsymbol{\lambda}
\end{bmatrix}
=
\begin{bmatrix}
\boldsymbol{r}_f \\
\boldsymbol{r}_s \\
\boldsymbol{r}_i
\end{bmatrix}
$$
In this system:
- $\boldsymbol{A}_f$ and $\boldsymbol{A}_s$ are the tangent matrices (Jacobians) arising from the fluid and solid governing equations, respectively. $\boldsymbol{A}_f$ is typically non-symmetric due to fluid advection, while $\boldsymbol{A}_s$ can be symmetric for simple elastic models.
- $\boldsymbol{C}_f$ and $\boldsymbol{C}_s$ are coupling matrices that arise from the linearization of the kinematic constraint at the interface.
- $\boldsymbol{C}_f^T$ and $\boldsymbol{C}_s^T$ represent the contribution of the interface tractions (represented by the Lagrange multiplier $\boldsymbol{\lambda}$) to the fluid and solid momentum equations.
- $\boldsymbol{r}_f$, $\boldsymbol{r}_s$, and $\boldsymbol{r}_i$ are the residual vectors, representing the current imbalance in the fluid momentum, solid momentum, and interface [kinematic equations](@entry_id:173032).
- The zero blocks on the main diagonal reflect that the fluid and solid domain equations do not directly depend on each other's variables (the coupling is through the interface), and the kinematic constraint does not depend on the Lagrange multiplier.

The primary advantage of [monolithic schemes](@entry_id:171266) is their **robustness and stability**. By treating all coupling terms implicitly, they can handle strong physical coupling, such as interactions between a dense fluid and a light structure, without the [numerical stability](@entry_id:146550) constraints that affect partitioned methods. Their main disadvantage is the high implementation complexity and computational cost associated with assembling and solving the large, ill-conditioned, non-symmetric coupled system.

#### Partitioned Schemes

In a **partitioned** (or segregated) approach, the fluid and solid are treated as separate subproblems, each solved with a dedicated, optimized solver. Information is exchanged across the interface iteratively within each time step until the [interface conditions](@entry_id:750725) are satisfied. This modularity allows for the reuse of existing, highly developed CFD and CSD software.

A classic example is the **Dirichlet-Neumann** scheme [@problem_id:3566598]. At each time step, an iteration loop proceeds as follows:
1.  **Predict**: An initial prediction is made for the interface motion.
2.  **Fluid Solve**: The fluid solver is run using the predicted interface motion as a kinematic (Dirichlet-type) boundary condition.
3.  **Data Transfer**: The fluid solver computes the resulting hydrodynamic forces (tractions) on the interface.
4.  **Solid Solve**: These forces are applied as a dynamic (Neumann-type) boundary condition to the structure, and the solid solver computes the resulting structural displacement and velocity.
5.  **Convergence Check**: The newly computed structural velocity at the interface is compared with the velocity used in the fluid solve (Step 2). If they match within a prescribed tolerance, the time step has converged. Otherwise, the interface motion is updated, and the process repeats from Step 2.

This iterative process is a form of [fixed-point iteration](@entry_id:137769) on the interface. **Loosely coupled** schemes perform this sequence only once per time step, which is computationally cheap but often inaccurate and prone to instability. **Strongly coupled** schemes iterate until convergence, which is more robust but computationally more expensive [@problem_id:3566567].

### The Added-Mass Effect and Numerical Stability

While partitioned schemes are attractive for their modularity, they can suffer from severe [numerical instability](@entry_id:137058), particularly in problems involving [incompressible fluids](@entry_id:181066) and light structures (e.g., blood flow, [aeroelasticity](@entry_id:141311)). This instability is a numerical artifact caused by the explicit treatment of a physical phenomenon known as the **[added-mass effect](@entry_id:746267)**.

#### Physical Origin of Added Mass

When a body accelerates through an [incompressible fluid](@entry_id:262924), it must displace the fluid in its path. This requires accelerating a certain volume of the surrounding fluid. The work done to accelerate this fluid manifests as a hydrodynamic reaction force on the body that is proportional to its acceleration. This force acts as if the body has an extra inertia, or an **added mass**.

In the idealized case of an inviscid, [irrotational flow](@entry_id:159258), the [hydrodynamic force](@entry_id:750449) $\boldsymbol{F}$ on a body accelerating with $\ddot{\boldsymbol{x}}(t)$ can be shown to be:
$$ \boldsymbol{F}(t) = - \boldsymbol{M_a} \ddot{\boldsymbol{x}}(t) $$
where $\boldsymbol{M_a}$ is the **added-mass tensor**, a symmetric, [positive-definite tensor](@entry_id:204409) that depends only on the body's geometry and the fluid density $\rho_f$. An equivalent definition can be derived from the kinetic energy $T_f$ of the fluid set in motion by the body moving at a [constant velocity](@entry_id:170682) $\boldsymbol{U}$:
$$ T_f = \frac{1}{2} \boldsymbol{U}^T \boldsymbol{M_a} \boldsymbol{U} $$
For a sphere of radius $R$ in an unbounded fluid, the added mass for [translational motion](@entry_id:187700) is a scalar $M_a = \frac{1}{2} \rho_f (\frac{4}{3}\pi R^3)$, which is exactly half the mass of the fluid displaced by the sphere [@problem_id:3566542].

#### The Added-Mass Instability in Partitioned Schemes

The [added-mass effect](@entry_id:746267) creates a strong, instantaneous coupling between the structural acceleration and the fluid pressure. In a conventional [partitioned scheme](@entry_id:172124) like the Dirichlet-Neumann method, this coupling is treated explicitly. The structural solver receives a force based on the fluid state from the *previous* sub-iteration, and it computes an acceleration without immediate feedback from the fluid's inertial reaction.

This explicit treatment can lead to a disastrous numerical instability. Consider a simple 1D model of a piston of mass $m_s$ coupled to a slug of fluid of mass $m_a = \rho_f A L$. The monolithic system's equation of motion is $(m_s + m_a)\ddot{y} + k_s y = 0$. A loosely coupled [partitioned scheme](@entry_id:172124), however, can be shown to correspond to a [fixed-point iteration](@entry_id:137769) for the acceleration $a = \ddot{y}$ with an amplification factor of $\lambda = -m_a / m_s$. The iteration is only stable if $|\lambda|  1$, which requires:
$$ m_a  m_s $$
Whenever the [added mass](@entry_id:267870) of the fluid is greater than the structural mass, the scheme becomes unstable, with errors growing exponentially at each iteration. This is the notorious **[added-mass instability](@entry_id:174360)** [@problem_id:3566532].

### Strategies for Stable Partitioned Coupling

Several strategies exist to overcome the [added-mass instability](@entry_id:174360) and create robust partitioned algorithms.

#### Iterative Coupling and Relaxation

The most direct approach is to use a **strongly coupled** scheme, iterating between the fluid and solid solvers until the interface residuals are driven to zero. While this does not change the fundamental properties of the fixed-point map, it can be combined with **interface relaxation**. For example, in a Dirichlet-Neumann scheme, the traction passed to the solid solver in iteration $k$ can be a weighted average of the newly computed traction and the traction from the previous iteration, $k-1$:
$$ \boldsymbol{t}^{(k)} = (1-\theta)\boldsymbol{t}^{(k-1)} + \theta \boldsymbol{t}_{\text{new}} $$
Using a [relaxation parameter](@entry_id:139937) $\theta  1$ under-relaxes the update, effectively damping the iterations and potentially stabilizing a scheme that would otherwise diverge [@problem_id:3566567]. More advanced schemes replace this simple relaxation with quasi-Newton methods that build an approximation of the interface Jacobian to accelerate convergence.

#### Enhanced Interface Conditions: Robin Coupling

A more sophisticated approach involves modifying the boundary conditions exchanged between solvers to make the coupling more implicit. Instead of exchanging pure Dirichlet or Neumann data, one can use **Robin-type** (or mixed) boundary conditions. For example, the fluid subproblem could be solved with a boundary condition of the form:
$$ p + \alpha \boldsymbol{u}_f \cdot \boldsymbol{n} = g $$
where $\alpha$ is a parameter and $g$ is a value computed from the structural solver. The goal is to choose $\alpha$ such that the Robin condition approximates the true response of the structural sub-problem. An "optimal" choice of $\alpha$ can make the [partitioned scheme](@entry_id:172124) unconditionally stable and significantly accelerate convergence, sometimes achieving convergence in a single iteration for linear problems. For the 1D fluid-slug model, the optimal Robin parameter that perfectly mimics the discrete structural response can be derived as $\alpha = \frac{\rho_f L}{\Delta t}$ [@problem_id:3566532].

### Advanced Discretization and Coupling Methods

Beyond the fundamental algorithmic architecture, practical FSI simulations often require advanced techniques to handle complex geometries and to ensure physical conservation laws are respected at the discrete level.

#### Coupling on Non-Matching Meshes with Mortar Methods

For complex problems, it is often impractical or inefficient to use a single, [conforming mesh](@entry_id:162625) that matches perfectly at the FSI interface. The fluid and solid may have vastly different length scales, requiring different mesh resolutions. The **[mortar method](@entry_id:167336)** is a powerful and mathematically rigorous framework for coupling non-matching discretizations.

The core idea is to enforce the interface constraint (e.g., kinematic continuity) in a weak, integral sense, rather than at discrete points. This is typically done using Lagrange multipliers. The discrete coupling matrices, which relate the degrees of freedom on the two sides of the interface, are computed by integrating products of [shape functions](@entry_id:141015) from the two meshes. For example, a matrix entry might look like $(\mathbf{C}_f)_{ja} = \int_{\Gamma} \Phi_j N_{fa} \, d\Gamma$, where $\Phi_j$ is a [basis function](@entry_id:170178) for the Lagrange multiplier and $N_{fa}$ is a [basis function](@entry_id:170178) for the fluid interface. A key advantage of this formulation is that, with a proper choice of basis functions and exact integration, it can be proven to be **discretely conservative**, meaning that the work (or power) exchanged across the interface is exactly zero, preventing the creation of spurious energy by the numerical coupling scheme. The resulting linear algebra allows for the construction of a **mortar [projection operator](@entry_id:143175)** that maps data from one mesh to the other in a stable and conservative manner [@problem_id:3566604].

#### Non-Conforming Methods: The Immersed Boundary Approach

An entirely different approach to FSI, which avoids the complexities of moving and deforming meshes altogether, is the **Immersed Boundary (IB) method**. In this framework, the fluid equations are solved on a fixed, often Cartesian, Eulerian grid that does not conform to the structure's geometry. The structure is represented as a Lagrangian object that moves through this fixed grid.

The [two-way coupling](@entry_id:178809) is achieved through two operations that use a **[regularized delta function](@entry_id:754211)**, $\delta_h$, which is a smooth approximation of the Dirac delta function with a [compact support](@entry_id:276214) related to the grid spacing $h$.
1.  **Force Spreading**: The Lagrangian forces $\boldsymbol{\lambda}$ generated by the structure are spread onto the nearby Eulerian grid nodes to create a fluid body [force field](@entry_id:147325) $\boldsymbol{f}$.
    $$ \boldsymbol{f}(\boldsymbol{x}_i, t) = \sum_q \boldsymbol{\lambda}_q(t) \, \delta_h(\boldsymbol{x}_i - \boldsymbol{\varphi}_q(t)) \, \Delta S_q $$
2.  **Velocity Interpolation**: The local [fluid velocity](@entry_id:267320) is interpolated from the Eulerian grid to the Lagrangian points of the structure to enforce the no-slip kinematic condition.
    $$ \boldsymbol{U}_q(t) = \sum_i \boldsymbol{u}(\boldsymbol{x}_i, t) \, \delta_h(\boldsymbol{x}_i - \boldsymbol{\varphi}_q(t)) \, h^d $$
A critical property for the stability of the IB method is that these two operators must be formal adjoints of each other with respect to the discrete inner products. This ensures that the discrete rate of work done by the structure is exactly equal to the rate of work done by the resulting [body force](@entry_id:184443) on the fluid, guaranteeing [energy conservation](@entry_id:146975) at the coupling level. This adjoint property is achieved if the *same* [regularized delta function](@entry_id:754211) is used for both spreading and interpolation. Furthermore, to ensure conservation of linear and angular momentum, the chosen [delta function](@entry_id:273429) must satisfy certain discrete [moment conditions](@entry_id:136365), including a [partition of unity](@entry_id:141893) property [@problem_id:3566578].