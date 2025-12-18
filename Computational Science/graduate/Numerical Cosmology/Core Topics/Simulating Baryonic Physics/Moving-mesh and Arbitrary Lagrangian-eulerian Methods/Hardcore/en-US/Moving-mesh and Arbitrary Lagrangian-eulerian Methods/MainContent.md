## Introduction
In the realm of computational science, simulating systems with vast dynamic ranges, large-scale bulk flows, and sharp, evolving features presents a persistent challenge. Traditional numerical methods often force a difficult choice: the fixed-grid Eulerian approach, which suffers from [numerical diffusion](@entry_id:136300) that can wash out critical details, or the flow-following Lagrangian approach, which offers superior accuracy but is prone to catastrophic mesh tangling in complex flows. The Arbitrary Lagrangian-Eulerian (ALE) and moving-mesh methodologies emerge as a sophisticated solution to this dilemma, providing a powerful hybrid framework designed to capture the best of both worlds. This article addresses the need for more accurate and robust simulation techniques by providing a deep dive into the principles and applications of these advanced methods.

Over the following chapters, you will embark on a structured journey through the world of moving-mesh simulations. The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork, deriving the ALE equations and explaining key concepts like the Geometric Conservation Law (GCL) and the profound advantages of [mesh motion](@entry_id:163293) for accuracy and efficiency. Next, **Applications and Interdisciplinary Connections** will showcase the versatility of these methods through real-world examples in astrophysics, cosmology, and multiphysics problems, illustrating how they enable new scientific discoveries. Finally, **Hands-On Practices** will point towards practical exercises designed to solidify the core numerical concepts. We begin by exploring the fundamental kinematic frameworks that underpin all moving-mesh hydrodynamics.

## Principles and Mechanisms

The Arbitrary Lagrangian-Eulerian (ALE) methodology represents a powerful synthesis of two classical descriptions of [continuum mechanics](@entry_id:155125), designed to harness the strengths of both while mitigating their respective weaknesses. This chapter elucidates the fundamental principles of the ALE framework, explores the mechanisms by which it operates, and discusses the key advantages and challenges associated with its implementation in [numerical cosmology](@entry_id:752779).

### Kinematic Frameworks: From Eulerian to Arbitrary Lagrangian-Eulerian

To understand the mechanics of a fluid, we must first establish a frame of reference in which to describe the evolution of its properties, such as density $\rho(\boldsymbol{r}, t)$ or velocity $\boldsymbol{u}(\boldsymbol{r}, t)$. The choice of framework dictates the mathematical form of the governing equations.

#### The Material Derivative

The most fundamental concept is the rate of change of a quantity as experienced by an observer moving with a fluid parcel. This is known as the **material derivative** or **Lagrangian derivative**, denoted by $\frac{D}{Dt}$. For any [scalar field](@entry_id:154310) $q(\boldsymbol{r}, t)$, its total differential is $dq = \frac{\partial q}{\partial t} dt + \nabla q \cdot d\boldsymbol{r}$. Dividing by $dt$ along the trajectory of a fluid parcel, where $\frac{d\boldsymbol{r}}{dt} = \boldsymbol{u}$, we obtain the material derivative:

$$
\frac{Dq}{Dt} \equiv \frac{\partial q}{\partial t} + \boldsymbol{u} \cdot \nabla q
$$

The first term, $\frac{\partial q}{\partial t}$, is the local rate of change at a fixed point in space, while the second term, $\boldsymbol{u} \cdot \nabla q$, is the **[convective derivative](@entry_id:262900)**, accounting for the change in $q$ due to the fluid parcel's motion into a region with a different value of $q$.

#### Eulerian Description (Fixed Frame)

The **Eulerian** framework is the most common description, where [fluid properties](@entry_id:200256) are observed at fixed spatial locations $\boldsymbol{r}$. A computational grid in this frame is static. The rate of change of a quantity for a fluid element is expressed using the material derivative operator, which explicitly contains both the local time derivative and the convective term. For a conserved quantity $q$ with no sources or sinks, its evolution equation is $\frac{Dq}{Dt} = 0$, which in the Eulerian frame is written as:

$$
\frac{\partial q}{\partial t} + \boldsymbol{u} \cdot \nabla q = 0
$$

While conceptually straightforward, this formulation introduces the convective term, which is notoriously difficult to discretize accurately and is a primary source of numerical diffusion in simulations.

#### Lagrangian Description (Following the Flow)

In the **Lagrangian** framework, the observer (and the computational mesh) moves with the fluid. Each mesh cell contains the same fluid element for all time. The position of a fluid parcel becomes a time-[dependent variable](@entry_id:143677), $\boldsymbol{X}(t)$. Since the observer's velocity is the [fluid velocity](@entry_id:267320), $\boldsymbol{u}$, the convective term vanishes by definition. The rate of change of a quantity $q$ for a fluid parcel is simply its [material derivative](@entry_id:266939), which reduces to a simple time derivative along the parcel's path:

$$
\frac{Dq}{Dt} = \text{Rate of change for the fluid parcel}
$$

This description is exceptionally powerful for tracking fluid flows, [contact discontinuities](@entry_id:747781), and [material interfaces](@entry_id:751731), as it eliminates numerical advection errors by construction. However, its major drawback is that if the flow undergoes significant shear, compression, or rotation, the [computational mesh](@entry_id:168560) can become severely distorted, leading to large [discretization errors](@entry_id:748522) and eventual code failure.

#### The Arbitrary Lagrangian-Eulerian (ALE) Description

The ALE method provides a continuous bridge between the Eulerian and Lagrangian extremes. In this framework, the [computational mesh](@entry_id:168560) is allowed to move with an arbitrary velocity $\boldsymbol{w}(\boldsymbol{r}, t)$, which is prescribed by the user. This velocity is independent of the fluid velocity $\boldsymbol{u}$. The goal is to move the mesh intelligently—to follow the bulk motion of the fluid to minimize advection errors (like a Lagrangian scheme) while simultaneously adjusting the mesh to maintain good cell quality (like an Eulerian scheme).

To derive the governing equations in this frame, we consider the rate of change of a quantity $q$ as seen by an observer on the [moving mesh](@entry_id:752196), $(\frac{\partial q}{\partial t})_{\text{mesh}}$. Using the chain rule, this is related to the Eulerian partial derivative by:

$$
\left(\frac{\partial q}{\partial t}\right)_{\text{mesh}} = \frac{\partial q}{\partial t} + \boldsymbol{w} \cdot \nabla q
$$

We can solve for the Eulerian derivative, $\frac{\partial q}{\partial t} = (\frac{\partial q}{\partial t})_{\text{mesh}} - \boldsymbol{w} \cdot \nabla q$, and substitute it into the [material derivative](@entry_id:266939) expression. Adopting the convention that $\partial_t$ now represents the time derivative on the [moving mesh](@entry_id:752196), the [material derivative](@entry_id:266939) becomes :

$$
\frac{Dq}{Dt} = \left(\frac{\partial q}{\partial t} - \boldsymbol{w} \cdot \nabla q\right) + \boldsymbol{u} \cdot \nabla q = \frac{\partial q}{\partial t} + (\boldsymbol{u} - \boldsymbol{w}) \cdot \nabla q
$$

The advection equation for a conserved quantity in the ALE frame is therefore:

$$
\frac{\partial q}{\partial t} + (\boldsymbol{u} - \boldsymbol{w}) \cdot \nabla q = 0
$$

This is the cornerstone of the ALE method. It shows that advection is driven by the **[relative velocity](@entry_id:178060)** between the fluid and the mesh, $\boldsymbol{u} - \boldsymbol{w}$. The Eulerian case is recovered when $\boldsymbol{w}=0$, and the Lagrangian case is recovered when $\boldsymbol{w}=\boldsymbol{u}$, causing the advection term to vanish.

### Conservation Laws in the ALE Framework

#### The General Form of ALE Equations

The principle derived for a scalar can be extended to a system of conservation laws, such as the Euler equations, which have the generic Eulerian form $\partial_t \boldsymbol{U} + \nabla \cdot \boldsymbol{F}(\boldsymbol{U}) = \boldsymbol{S}$, where $\boldsymbol{U}$ is the vector of [conserved variables](@entry_id:747720), $\boldsymbol{F}$ is the flux tensor, and $\boldsymbol{S}$ is a [source term](@entry_id:269111). The corresponding integral form for a fixed volume $V$ is $\frac{d}{dt}\int_V \boldsymbol{U} dV + \oint_{\partial V} \boldsymbol{F} \cdot d\boldsymbol{A} = \int_V \boldsymbol{S} dV$.

Using the Reynolds [transport theorem](@entry_id:176504) for a volume $V(t)$ moving with the mesh velocity $\boldsymbol{w}$, the time derivative term becomes $\frac{d}{dt}\int_{V(t)} \boldsymbol{U} dV = \int_{V(t)} \frac{\partial \boldsymbol{U}}{\partial t} dV + \oint_{\partial V(t)} \boldsymbol{U}(\boldsymbol{w} \cdot \boldsymbol{n}) dA$. Combining these leads to the differential form of the conservation law in the ALE framework:

$$
\frac{\partial \boldsymbol{U}}{\partial t} + \nabla \cdot (\boldsymbol{F} - \boldsymbol{w} \otimes \boldsymbol{U}) = \boldsymbol{S}
$$

The effective flux in the ALE frame is $\boldsymbol{F}_{\text{ALE}} = \boldsymbol{F} - \boldsymbol{w} \otimes \boldsymbol{U}$, which includes the physical flux $\boldsymbol{F}$ and an additional [convective flux](@entry_id:158187) term due to the motion of the mesh itself.

#### The Geometric Conservation Law (GCL) and Mesh Evolution

Since the mesh cells are moving and deforming, their volumes are changing in time. This geometric evolution must be accounted for with perfect consistency. The rate of change of a cell's volume $V_i$ is governed by the motion of its boundaries. Applying the Reynolds [transport theorem](@entry_id:176504) with a constant field of unity gives the **Geometric Conservation Law (GCL)**:

$$
\frac{dV_i}{dt} = \oint_{\partial V_i} \boldsymbol{w} \cdot \boldsymbol{n} \, dA
$$

where $\boldsymbol{n}$ is the outward normal of the cell's boundary $\partial V_i$. This law is not a physical conservation law but a mathematical identity that must be satisfied by any valid [numerical discretization](@entry_id:752782) to ensure, for example, that a uniform state is preserved on a [moving mesh](@entry_id:752196).

#### Jacobian Evolution and Volume Change

A deeper understanding of volume change comes from analyzing the evolution of the Jacobian of the mapping from a time-independent reference (or Lagrangian) coordinate system $\boldsymbol{\xi}$ to the physical coordinates $\boldsymbol{x}(\boldsymbol{\xi}, t)$. In one dimension, the Jacobian is simply the local cell metric factor $J(\xi, t) = \partial_{\xi} x(\xi, t)$, representing the physical width of a cell that has unit width in the reference coordinate. The evolution of the mesh points is given by $\partial_t x(\xi, t) = w(x(\xi, t), t)$. By taking the time derivative of the Jacobian definition and swapping the order of partial derivatives, we can derive the Jacobian evolution equation :

$$
\partial_t J = \partial_t (\partial_{\xi} x) = \partial_{\xi} (\partial_t x) = \partial_{\xi} (w) = (\partial_x w)(\partial_{\xi} x) = (\nabla \cdot \boldsymbol{w}) J
$$

This fundamental relation, $\partial_t J = (\nabla \cdot \boldsymbol{w}) J$, shows that the local volume element, represented by $J$, expands or contracts at a rate given by the divergence of the mesh [velocity field](@entry_id:271461). For instance, in a 1D scenario with a linear [velocity field](@entry_id:271461) $w(x) = ax$ (where $a$ is a constant), the divergence is simply $\partial_x w = a$. The Jacobian equation becomes $\partial_t J = a J$, which integrates to $J(t) = J(0) \exp(at)$, showing [exponential growth](@entry_id:141869) or decay of the [cell size](@entry_id:139079). This is directly analogous to the evolution of comoving volumes in an [expanding universe](@entry_id:161442), where $\boldsymbol{w} = H(t)\boldsymbol{x}$ and $\nabla \cdot \boldsymbol{w} = d \cdot H(t)$ in $d$ dimensions .

### Advantages of Mesh Motion

The primary motivation for employing [moving-mesh methods](@entry_id:752194) is to gain a significant advantage in accuracy and efficiency over traditional fixed-grid Eulerian codes, especially in astrophysical contexts characterized by supersonic flows and the hierarchical [growth of structure](@entry_id:158527).

#### Mitigating Numerical Diffusion: The Quasi-Lagrangian Advantage

Numerical diffusion is a pervasive artifact in Eulerian simulations that artificially smooths out sharp features like shocks and [contact discontinuities](@entry_id:747781). This error arises from the [discretization](@entry_id:145012) of the advection term. A first-order Godunov-type scheme, for instance, introduces a [numerical diffusion](@entry_id:136300) coefficient that is proportional to the advection speed and the grid [cell size](@entry_id:139079).

In the ALE framework, advection is governed by the [relative velocity](@entry_id:178060) $|u_n - w_n|$, where the subscript $n$ denotes the component normal to a cell face. The leading-order [numerical diffusion](@entry_id:136300) coefficient can be shown to scale as $\nu_{\mathrm{num}} \approx \frac{1}{2} |u_n - w_n| \Delta x_n$ . By choosing a mesh velocity $\boldsymbol{w}$ that closely tracks the fluid velocity $\boldsymbol{u}$, the relative speed $|u_n - w_n|$ can be made very small. This drastically reduces [numerical diffusion](@entry_id:136300).

A perfect example is the preservation of a [contact discontinuity](@entry_id:194702). If the mesh faces are aligned with the contact and move with the fluid's normal velocity ($w_n = u_n$), the [relative velocity](@entry_id:178060) is zero. The contact becomes stationary in the mesh frame, and a Godunov-type solver will compute zero mass flux across the interface, thereby preserving the discontinuity with minimal smearing. In contrast, on a fixed Eulerian mesh ($w_n = 0$), the contact moves at speed $|u_n|$ relative to the grid, leading to significant diffusion. A quantitative, dimensionless measure of this "contact rest error" can be defined as $\varepsilon_c \equiv |u_n - w_n| \Delta t / \Delta x_n$, which is the Courant number of the contact relative to the mesh. The goal of a quasi-Lagrangian method is to minimize this error .

#### Overcoming the CFL Timestep Limitation in Supersonic Flows

Perhaps the most compelling advantage for cosmology is the relaxation of the Courant-Friedrichs-Lewy (CFL) stability condition. The CFL condition requires that the numerical timestep, $\Delta t$, must be small enough that the fastest-moving wave does not cross a grid cell in a single step. For the Euler equations in the ALE frame, the maximum signal speed normal to a cell face is the sum of the sound speed $c_s$ and the magnitude of the relative fluid velocity normal to the face. The timestep limit is thus:

$$
\Delta t \le C_{\text{CFL}} \min_f \left( \frac{R_f}{|(\boldsymbol{u}-\boldsymbol{w})\cdot\boldsymbol{n}_f| + c_s} \right)
$$

where $R_f$ is the characteristic size of face $f$ and $C_{\text{CFL}}$ is the Courant number (typically less than 1).

In [cosmological simulations](@entry_id:747925), large-scale bulk flows are often highly supersonic, meaning the fluid velocity $|\boldsymbol{u}|$ is much larger than the sound speed $c_s$. In an Eulerian code ($\boldsymbol{w}=0$), the timestep is severely limited by the large [fluid velocity](@entry_id:267320) term: $\Delta t_{\text{E}} \propto R / (|\boldsymbol{u}| + c_s)$. However, in a Lagrangian scheme where the mesh moves with the fluid ($\boldsymbol{w}=\boldsymbol{u}$), the [relative velocity](@entry_id:178060) term vanishes, and the timestep is limited only by the sound speed: $\Delta t_{\text{L}} \propto R / c_s$.

The improvement factor is the ratio of these timesteps, $F = \Delta t_{\text{L}} / \Delta t_{\text{E}}$. In a [supersonic flow](@entry_id:262511) with Mach number $M = |\boldsymbol{u}|/c_s$, this factor becomes :

$$
F(M) = \frac{|\boldsymbol{u}| + c_s}{c_s} = \frac{|\boldsymbol{u}|}{c_s} + 1 = M + 1
$$

For a flow with $M=10$, a Lagrangian scheme can take a timestep that is 11 times larger than an Eulerian scheme, resulting in a dramatic increase in [computational efficiency](@entry_id:270255) without sacrificing stability.

### Numerical Implementation with Finite-Volume Methods

The practical power of ALE methods is realized through their implementation within a finite-volume framework, where cell-averaged quantities are evolved based on fluxes computed at cell interfaces.

#### The ALE Riemann Problem and Godunov's Method

Godunov-type schemes compute interface fluxes by solving a local Riemann problem—the evolution of an initial discontinuity—at each face. In the ALE framework, the governing equations for the Riemann problem are based on the relative velocity $\boldsymbol{u}-\boldsymbol{w}$. The [characteristic speeds](@entry_id:165394) of the system are shifted, becoming $u_n - w_n$, $u_n - w_n \pm c_s$ for the normal components.

A significant complication arises if the mesh velocity $\boldsymbol{w}$ is discontinuous across a cell face, which can occur when different [mesh motion](@entry_id:163293) strategies are used in adjacent cells. In this case, the flux function itself becomes discontinuous. A robust [numerical flux](@entry_id:145174), such as one based on the Harten-Lax-van Leer (HLL) approximate Riemann solver, must be constructed using the side-dependent ALE fluxes $F_L^{\text{ALE}} = F(\boldsymbol{U}_L) - w_L \boldsymbol{U}_L$ and $F_R^{\text{ALE}} = F(\boldsymbol{U}_R) - w_R \boldsymbol{U}_R$. The signal speeds for the HLL formula must also be estimated using the relative velocities on each side, e.g., $S_L = \min(u_{n,L}-w_{n,L}-c_{s,L}, u_{n,R}-w_{n,R}-c_{s,R})$ .

#### Ensuring Consistency: The Geometric Conservation Law in Discrete Form

As mentioned, the GCL is a critical [consistency condition](@entry_id:198045). In a semi-discrete finite-volume scheme, the volume of a cell $i$ is updated based on the motion of its faces: $V_i^{n+1} = V_i^n + \Delta t \sum_f A_f w_{f,n}$. The update for a conserved quantity $\boldsymbol{U}$ involves the ALE fluxes. For the scheme to preserve a uniform state ($\boldsymbol{U}_i = \text{const}$ for all $i$), the numerical flux must be consistent with the geometry update. This requires that for a uniform state $\boldsymbol{U}$, the numerical ALE flux at a face moving with velocity $w_f$ must be $\boldsymbol{F}_{\text{ALE}} = \boldsymbol{F}(\boldsymbol{U}) - w_f \boldsymbol{U}$.

If the mesh velocity is discontinuous, the face velocity $w_f$ itself must be defined consistently. For an HLL-type scheme, this consistency requirement leads to a specific weighted average for the face velocity based on the estimated signal speeds :

$$
w_f = \frac{S_R w_L - S_L w_R}{S_R - S_L}
$$

Satisfying the discrete GCL is non-trivial and is essential for preventing the generation of spurious sources or sinks of [conserved quantities](@entry_id:148503) due to [mesh motion](@entry_id:163293) alone.

#### GCL and Time Integration in Cosmological Flows

The challenge of maintaining the GCL extends to the choice of time integrator. Consider the evolution of cell volumes in a Hubble flow, where $\boldsymbol{w} = H(t)\boldsymbol{x}$. As derived earlier, this leads to the ODE $\frac{dV}{dt} = d H(t) V(t)$. A numerical scheme for the fluid dynamics equations must use a [time integration](@entry_id:170891) method for geometry that is consistent with the method used for the fluid state. For example, if a second-order Runge-Kutta method is used, the conditions on its coefficients required for [second-order accuracy](@entry_id:137876) for the ODE problem must be met. For a general two-stage explicit RK method, this imposes the condition $b_2 c_2 = 1/2$, where $b_2$ is a weight and $c_2$ is the time of the second stage, to correctly capture the evolution of a time-varying $H(t)$ to second order. Failure to ensure such consistency can lead to errors that violate the GCL at the order of the [time integration](@entry_id:170891) accuracy .

### Advanced Challenges and Solutions

While offering significant advantages, [moving-mesh methods](@entry_id:752194) introduce their own set of complex challenges that have driven modern algorithm development.

#### Preserving Equilibria: Well-Balanced Schemes for Gravity

Many astrophysical systems, from [stellar interiors](@entry_id:158197) to galactic disks, exist in a state of near-[hydrostatic equilibrium](@entry_id:146746), where the [pressure gradient force](@entry_id:262279) is delicately balanced by gravity, $\nabla p = -\rho \nabla \Phi$. Standard finite-volume schemes can struggle to maintain this balance, as the discrete pressure gradient and the discrete source term are computed independently and may not cancel to machine precision. This can generate spurious velocities and disrupt the [equilibrium state](@entry_id:270364).

**Well-balanced** schemes are designed to overcome this by modifying the numerical method to exactly preserve a discrete [hydrostatic equilibrium](@entry_id:146746). A powerful technique involves reformulating the Riemann problem at each cell face. Instead of using the cell-centered states directly, one maps them to the face by accounting for the change in gravitational potential. For a barotropic fluid where equilibrium is defined by $H(\rho) + \Phi = \text{const}$ (with $H$ being the [specific enthalpy](@entry_id:140496)), one can define reconstructed states at the face, $\rho_{L/R}^*$, such that $H(\rho_{L/R}^*) = H(\rho_{i/j}) + \Phi_{i/j} - \Phi_f$. In a state of discrete equilibrium, this mapping ensures that $\rho_L^*=\rho_R^*$ and $p_L^*=p_R^*$.

The Riemann solver then returns a single pressure $p_f^*$ at the face. To complete the balance, the gravity source term is discretized not at the cell center, but in a way that is perfectly coupled to the pressure fluxes: $V_i S_i^{(\text{mom})} = \sum_f A_f p_f^* \boldsymbol{n}_f$. This construction ensures that the sum of discrete pressure forces and the [discrete gravity](@entry_id:198242) source term cancel exactly, preserving the [hydrostatic balance](@entry_id:263368) to machine precision, even on a [moving mesh](@entry_id:752196) .

#### The Problem of Mesh Distortion and Tangling

The greatest challenge for quasi-Lagrangian methods is maintaining [mesh quality](@entry_id:151343). While a purely Lagrangian scheme ($\boldsymbol{w}=\boldsymbol{u}$) is ideal for accuracy, realistic fluid flows involving shear, [vorticity](@entry_id:142747), and compression can rapidly deform cells into highly skewed, flattened, or tangled shapes. This leads to large [discretization errors](@entry_id:748522) and, eventually, non-positive cell volumes (inversion), which crashes the simulation. For example, while a pure [shear flow](@entry_id:266817) $\boldsymbol{u}=(0, Sx)$ does not cause cell inversion (the Jacobian remains constant), it progressively shears quadrilateral cells into long, thin slivers, degrading accuracy .

#### Strategies for Mesh Management

To prevent mesh degradation, the mesh velocity $\boldsymbol{w}$ must deviate from the [fluid velocity](@entry_id:267320) $\boldsymbol{u}$. This introduces relative motion and some numerical advection, but it is a necessary compromise to ensure the long-term stability and validity of the simulation. Two primary strategies have emerged.

##### Continuous Regularization and Variational Methods

One approach is to define the mesh velocity field at each timestep as the solution to a [global optimization](@entry_id:634460) problem. The goal is to find a velocity field $\boldsymbol{w}$ that both tracks the flow and keeps the mesh as regular as possible. This can be formulated as a variational problem where one minimizes an objective functional, $\mathcal{F}[w]$. This functional typically combines a "deformation energy" term that penalizes mesh distortion (e.g., $E[\boldsymbol{w}] = \int ||\nabla \boldsymbol{w}||^2 dV$) with a "tracking" term that penalizes deviations from a target velocity field (e.g., $J[\boldsymbol{w}] = \int \beta ||\boldsymbol{w}-\boldsymbol{v}||^2 dV$). The weight function $\beta$ can be designed to concentrate mesh resolution in regions of interest, such as areas with high vorticity .

The Euler-Lagrange equations for this minimization problem yield a system of [elliptic partial differential equations](@entry_id:141811) for the components of $\boldsymbol{w}$, such as $-\Delta \boldsymbol{w} + \lambda \beta \boldsymbol{w} = \lambda \beta \boldsymbol{v}$. Solving these PDEs at each step provides a smooth mesh velocity field that optimally balances the competing demands of tracking and regularity. An alternative regularization approach is to define the mesh velocity as $\boldsymbol{w}=\boldsymbol{u}+R[\boldsymbol{u}]$, where $R[\boldsymbol{u}]$ is a regularization term designed to smooth the mesh. A common choice is $R[\boldsymbol{u}] \propto \nabla^2 \boldsymbol{u}$, which has the desirable property of vanishing for affine flows (uniform strain, shear, and rotation), thus allowing the mesh to follow these large-scale motions exactly while resisting small-scale, irregular deformations .

##### Discrete Rezoning and Conservative Remapping

An alternative and widely used paradigm, especially with unstructured meshes like a Voronoi tessellation, is to operate in discrete cycles of Lagrangian evolution and mesh correction. The procedure at each timestep is:
1.  **Lagrangian Step:** Advance the mesh vertices and the fluid state over a timestep $\Delta t$ using a purely Lagrangian update ($\boldsymbol{w}=\boldsymbol{u}$). This step is highly accurate but may distort the mesh.
2.  **Rezone Step:** At the end of the step, discard the distorted mesh geometry. Generate a new, high-quality mesh at the same time $t^{n+1}$ that covers the same domain. This is often achieved by generating a centroidal Voronoi tessellation (CVT) from the mass distribution, which naturally places smaller cells in denser regions.
3.  **Remap Step:** The final, crucial step is to transfer the conserved quantities from the old, distorted cells to the new, regular cells. This transfer must be **exactly conservative** to prevent artificial creation or destruction of mass, momentum, and energy. Assuming the data in each old cell $K_i^{old}$ is represented by its cell average $\bar{\boldsymbol{U}}_i^{old}$, the new cell average $\bar{\boldsymbol{U}}_j^{new}$ is computed by summing the contributions from all overlapping old cells :

$$
\bar{\boldsymbol{U}}^{new}_{j} = \frac{1}{|\hat{K}_{j}|} \sum_{i} \bar{\boldsymbol{U}}^{old}_{i} |K_{i} \cap \hat{K}_{j}|
$$

Here, $|K|$ is the cell volume, and $|K_i \cap \hat{K}_j|$ is the intersection volume between old cell $i$ and new cell $j$. This remapping formula, based on a [piecewise-constant reconstruction](@entry_id:753441) of the data, guarantees that the total integrated quantity in the domain remains unchanged. This "Lagrange-plus-remap" approach is the engine behind successful cosmological codes like AREPO, combining the accuracy of Lagrangian advection with the robust [mesh quality](@entry_id:151343) of a grid that adapts to the flow.