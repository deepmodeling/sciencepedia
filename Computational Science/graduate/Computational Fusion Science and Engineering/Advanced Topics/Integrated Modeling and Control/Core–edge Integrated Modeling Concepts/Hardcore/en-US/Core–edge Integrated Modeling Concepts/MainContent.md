## Introduction
To achieve sustained nuclear fusion, a plasma must be heated to extreme temperatures while being effectively confined. In a tokamak, this creates a system of stark contrasts, from the intensely hot, well-confined core where fusion reactions occur, to the cooler, turbulent edge region that interfaces with material walls. Historically, these regions have been studied with specialized models tailored to their unique physics. However, treating them in isolation creates a fundamental knowledge gap; the core and edge are not independent but form a single, deeply interconnected system where the behavior of one region directly influences the other. A predictive understanding of a fusion device as a whole is therefore impossible without a model that self-consistently couples these domains.

This article provides a comprehensive overview of the concepts and methods behind [core–edge integrated modeling](@entry_id:1123076). It bridges the gap between isolated component-level physics and a unified, systems-level view of the plasma. By exploring this topic, you will gain a foundational understanding of the multi-scale, multi-physics challenges in fusion simulation and the strategies being developed to overcome them. The following sections will guide you through this complex landscape. The **Principles and Mechanisms** section will lay the groundwork, detailing the magnetic geometry, transport physics, and boundary conditions that govern the core-edge system. The **Applications and Interdisciplinary Connections** section will demonstrate how these principles are applied to predict tokamak performance, optimize operational scenarios, and study complex transient events. Finally, the **Hands-On Practices** appendix will offer opportunities to engage directly with the core concepts through targeted problems. We begin by examining the fundamental physical and geometric stage upon which this complex interplay unfolds.

## Principles and Mechanisms

### The Physical and Geometric Landscape of Core-Edge Integration

A comprehensive understanding of core-edge integrated modeling begins with an appreciation of the complex magnetic geometry that defines the distinct plasma regions. The behavior of a magnetically confined plasma is intrinsically tied to the structure of the magnetic field, which serves as the stage for all [transport phenomena](@entry_id:147655).

#### Magnetic Topology: The Stage for Transport

In an axisymmetric tokamak, the magnetic field can be conveniently described using a **[poloidal magnetic flux](@entry_id:1129914) function**, denoted by $\psi(R,Z)$, where $R$ is the major radius and $Z$ is the vertical position. By definition, magnetic field lines lie on surfaces of constant $\psi$. In the core of a typical tokamak, these surfaces form a set of nested tori, centered on the magnetic axis.

Modern high-performance tokamaks employ a "diverted" magnetic configuration to manage [plasma-wall interactions](@entry_id:187149). This is achieved by introducing a null in the poloidal magnetic field, $\mathbf{B}_p$, at a specific location. This location is known as an **X-point**. Mathematically, the X-point is a saddle point of the flux function $\psi$, where its gradient vanishes: $\nabla \psi = \mathbf{0}$. It is crucial to note a common misconception: while the poloidal field is zero at the X-point, the toroidal field component, $B_\phi$, remains finite. Thus, the total magnetic field magnitude $|\mathbf{B}|$ does not vanish.

This topological boundary, known as the **[separatrix](@entry_id:175112)**, is formally the magnetic surface that passes through the X-point. Its significance cannot be overstated: it partitions the plasma into two regions with fundamentally different transport physics. Inside the separatrix, magnetic field lines are **closed**, forming nested toroidal surfaces that do not intersect any material boundaries. Plasma particles and energy on these surfaces are well-confined, and transport across the magnetic field (radial transport) is a relatively slow process.

In stark contrast, field lines outside the [separatrix](@entry_id:175112) are **open**; they extend from the main plasma and terminate on specially designed material surfaces in the **divertor**. This region of open field lines is broadly known as the **edge plasma**. This dichotomy dictates that transport on open field lines is dominated by rapid parallel losses to these material boundaries, a process orders of magnitude faster than the [perpendicular transport](@entry_id:1129533) that governs core confinement.

The edge plasma itself is further subdivided. The region of open field lines just outside the [separatrix](@entry_id:175112), which "scrapes off" heat and particles leaving the core, is termed the **Scrape-Off Layer (SOL)**. In a single-null divertor configuration, the region of open field lines located beneath the X-point and bounded by the separatrix legs is called the **Private Flux Region (PFR)**. Plasma in both the SOL and PFR flows along field lines to the divertor targets, where it is neutralized. Understanding the interplay between slow [perpendicular transport](@entry_id:1129533) from the core into the SOL and rapid parallel transport within the SOL to the divertor is the central challenge of core-edge physics .

#### Flux Coordinates: The Language of Plasma Modeling

To model the transport processes that are so strongly influenced by the magnetic field, it is advantageous to use a coordinate system aligned with the physics. Instead of the standard [cylindrical coordinates](@entry_id:271645) $(R, \phi, Z)$, [tokamak modeling](@entry_id:1133221) predominantly employs **[flux coordinates](@entry_id:1125149)**. A common choice is $(\psi, \theta, \phi)$, where $\psi$ is the poloidal flux label that identifies a magnetic surface, $\theta$ is a poloidal angle-like coordinate that parameterizes the surface, and $\phi$ is the standard toroidal angle.

The transformation from these [flux coordinates](@entry_id:1125149) to the physical space of [cylindrical coordinates](@entry_id:271645) is given by the mapping $\mathbf{x}(\psi, \theta, \phi)$. For an axisymmetric equilibrium, this mapping can be expressed as:
$$
\mathbf{x}(\psi,\theta,\phi) = R(\psi,\theta)\,\hat{\mathbf{e}}_{R}(\phi) + Z(\psi,\theta)\,\hat{\mathbf{e}}_{Z}
$$
where $\hat{\mathbf{e}}_{R}(\phi)$ and $\hat{\mathbf{e}}_{Z}$ are the [unit vectors](@entry_id:165907) in the cylindrical system. From this mapping, we can define the geometric quantities required to write the transport equations in a general, coordinate-independent form. The [covariant basis](@entry_id:198968) vectors are given by the partial derivatives of the [position vector](@entry_id:168381):
$$
\partial_{\psi}\mathbf{x} = \frac{\partial R}{\partial \psi}\,\hat{\mathbf{e}}_{R} + \frac{\partial Z}{\partial \psi}\,\hat{\mathbf{e}}_{Z}
$$
$$
\partial_{\theta}\mathbf{x} = \frac{\partial R}{\partial \theta}\,\hat{\mathbf{e}}_{R} + \frac{\partial Z}{\partial \theta}\,\hat{\mathbf{e}}_{Z}
$$
$$
\partial_{\phi}\mathbf{x} = R\,\hat{\mathbf{e}}_{\phi}
$$
The dot products of these basis vectors form the **covariant metric tensor coefficients**, $g_{ij} = \partial_i \mathbf{x} \cdot \partial_j \mathbf{x}$. The non-zero components for this axisymmetric system are:
$$
g_{\psi\psi} = \left(\frac{\partial R}{\partial \psi}\right)^2 + \left(\frac{\partial Z}{\partial \psi}\right)^2
$$
$$
g_{\theta\theta} = \left(\frac{\partial R}{\partial \theta}\right)^2 + \left(\frac{\partial Z}{\partial \theta}\right)^2
$$
$$
g_{\psi\theta} = \frac{\partial R}{\partial \psi}\frac{\partial R}{\partial \theta} + \frac{\partial Z}{\partial \psi}\frac{\partial Z}{\partial \theta}
$$
$$
g_{\phi\phi} = R^2
$$
Note that $g_{\psi\theta}$ is generally non-zero for the shaped flux surfaces in a tokamak, indicating that the $\psi$ and $\theta$ coordinates are not orthogonal. The [volume element](@entry_id:267802) in this coordinate system is given by the **Jacobian** of the transformation, $J = (\partial_{\psi}\mathbf{x} \times \partial_{\theta}\mathbf{x}) \cdot \partial_{\phi}\mathbf{x}$, which evaluates to:
$$
J = R \left( \frac{\partial Z}{\partial \psi}\frac{\partial R}{\partial \theta} - \frac{\partial R}{\partial \psi}\frac{\partial Z}{\partial \theta} \right)
$$
These metric coefficients and the Jacobian are essential for consistently formulating physical laws, such as conservation equations and [differential operators](@entry_id:275037) like the divergence and gradient, in the flux coordinate system used by both core and edge simulation codes .

### Governing Physics of Plasma Transport

With the geometric stage set, we now turn to the physical mechanisms that drive the movement of particles and energy across the magnetic field.

#### Transport Mechanisms: Neoclassical and Turbulent Fluxes

Radial transport in a tokamak is the result of complex processes that are broadly categorized into two main types: neoclassical and turbulent.

**Neoclassical transport** is the irreducible, baseline transport that arises from particle-particle collisions in the complex [toroidal geometry](@entry_id:756056) of a tokamak. In a simple straight cylinder, collisions cause a [simple random walk](@entry_id:270663) across field lines, known as classical transport. In a torus, however, the magnetic field is non-uniform on a flux surface ($B \propto 1/R$). This, along with the field line curvature, causes charged particles to undergo [guiding-center](@entry_id:200181) drifts. These drifts, in combination with collisions that scatter particles between different types of orbits (e.g., trapped "banana" orbits and passing orbits), lead to a net radial transport that is significantly enhanced over the classical prediction. This collision-driven transport in a toroidal geometry is what we call neoclassical.

**Turbulent transport**, on the other hand, is an "anomalous" process that arises from collective plasma instabilities. Small-scale [microinstabilities](@entry_id:751966), driven by gradients in [plasma density](@entry_id:202836), temperature, or velocity, create rapidly fluctuating electric and magnetic fields. The primary mechanism for turbulent transport is the fluctuating $\mathbf{E} \times \mathbf{B}$ drift, where correlations between density fluctuations and electric field fluctuations lead to a net radial particle flux, $\Gamma^{\text{turb}} = \langle \delta n \delta v_{E,r} \rangle$. Similar correlations drive turbulent fluxes of heat and momentum. In most high-performance tokamak regimes, turbulent transport rates are significantly larger than neoclassical rates and are the dominant cause of plasma loss from the core.

For modeling purposes, the total radial flux of any quantity (particles $\Gamma_s$, heat $Q_s$, or toroidal momentum $\Pi$) is expressed as the sum of these two contributions:
$$
\Gamma_s = \Gamma_s^{\mathrm{nc}} + \Gamma_s^{\mathrm{turb}}
$$
$$
Q_s = Q_s^{\mathrm{nc}} + Q_s^{\mathrm{turb}}
$$
$$
\Pi = \Pi^{\mathrm{nc}} + \Pi^{\mathrm{turb}}
$$
Distinguishing these mechanisms is critical, but as we will see, for the purpose of ensuring a [conservative coupling](@entry_id:747708) between core and edge models, it is the **total net flux** that matters .

#### The H-mode Pedestal: A Transport Barrier at the Edge

A key feature of high-performance (H-mode) tokamak operation is the formation of a **pedestal**, an insulating layer at the plasma edge, just inside the separatrix, characterized by strongly suppressed transport and steep pressure gradients. The pedestal structure is defined by the radial profile of the pressure gradient, or equivalently, its inverse scale length $L_p^{-1}(r) \equiv |\partial \ln p / \partial r|$.

The pedestal consists of three main regions:
1.  The **pedestal top**, which marks the inner boundary where the weak gradients of the core begin to steepen.
2.  The **gradient region**, the defining part of the pedestal with the steepest pressure gradient and thus the smallest value of $L_p(r)$.
3.  The **pedestal foot**, the outer boundary near the [separatrix](@entry_id:175112) where the gradient relaxes as the profile connects to the SOL.

The physics of transport in the pedestal is distinct from that in the core. The steep pressure gradient in the pedestal drives a strong, sheared [radial electric field](@entry_id:194700) ($E_r$). This $E_r$ shear is highly effective at tearing apart the large-scale turbulent eddies characteristic of core turbulence, such as Ion Temperature Gradient (ITG) and Trapped Electron Modes (TEM). This shear suppression is the origin of the "[transport barrier](@entry_id:756131)".

However, the pedestal pressure cannot grow indefinitely. It is limited by other, more violent instabilities. The pedestal gradient is primarily constrained by **Peeling-Ballooning (P-B) modes**, a class of ideal Magnetohydrodynamic (MHD) instabilities driven by the strong edge pressure gradient (the "ballooning" part) and the associated edge current (the "peeling" part). When the pedestal exceeds a critical height and width, these modes can be triggered, leading to a rapid ejection of particles and energy known as an Edge Localized Mode (ELM). Within the gradient region, transport may also be regulated by **Kinetic Ballooning Modes (KBMs)**, which are thought to set the maximum achievable pressure gradient.

The [plasma collisionality](@entry_id:753486), which depends strongly on temperature as $\nu^* \propto n/T^2$, plays a crucial role. Since temperature drops steeply from the core to the edge, collisionality is low in the core and increases significantly across the pedestal. Near the cold, dense pedestal foot, the high collisionality can enable **Resistive Ballooning Modes (RBMs)**, which can contribute to transport in this specific region .

### Boundary Conditions and Coupling Principles

The successful integration of core and edge models hinges on the physically and mathematically consistent formulation of boundary conditions at the interfaces between domains.

#### The Plasma-Wall Interface: Sheath Physics and Divertor Boundary Conditions

The ultimate sink for particles and energy leaving the confined plasma is the material wall of the divertor. The interaction between the SOL plasma and this material surface is mediated by a thin, electrostatically charged boundary layer known as the **plasma sheath**. The physics of the sheath provides the downstream boundary conditions for any fluid model of the SOL.

Two key principles govern this interaction:
1.  The **Bohm criterion**: For a stable, monotonic potential drop to form in the sheath (which serves to repel the mobile electrons and accelerate the heavier ions), ions must enter the sheath from the quasi-neutral plasma with a velocity at least equal to the local ion sound speed. In fluid models, this is imposed as a strict equality at the sheath entrance (denoted by subscript $s$):
    $$
    u_{\parallel,s} = c_s
    $$
    For a plasma with [ion temperature](@entry_id:191275) $T_i$ and electron temperature $T_e$, the ion sound speed is $c_s = \sqrt{(Z k_B T_e + k_B T_i)/m_i}$, where $Z$ is the ion charge number and $m_i$ is the ion mass. This condition dictates the parallel flow velocity at the divertor boundary.

2.  The **Sheath Heat Transmission Coefficient**: The total energy flux (heat flux) $q_{\parallel,s}$ that is transmitted through the sheath to the wall is proportional to the particle flux and the thermal energy at the sheath entrance. This relationship is quantified by the [sheath heat transmission coefficient](@entry_id:1131561), $\gamma$. The total heat flux is the sum of electron and ion contributions:
    $$
    q_{\parallel,s} = q_{e,s} + q_{i,s} = \gamma_e n_{e,s} k_B T_{e,s} c_s + \gamma_i n_{i,s} k_B T_{i,s} c_s
    $$
    For a typical absorbing, floating surface, kinetic theory and simulations find $\gamma_e \approx 5$ and $\gamma_i \approx 2$. This relation does not fix the temperature at the wall temperature; rather, it provides a Robin-type boundary condition that links the temperature values at the sheath entrance to their gradients, as the heat flux from the upstream SOL (driven by conduction and convection) must match this transmitted flux.

These two principles form the fundamental boundary conditions for SOL fluid models at the divertor targets: the flow becomes sonic, and the heat flux is governed by the sheath transmission model. The [plasma density](@entry_id:202836) $n_s$ at this boundary is not prescribed; it is determined by the upstream plasma solution, which must deliver a particle flux $\Gamma_{\parallel,s} = n_s u_{\parallel,s} = n_s c_s$ to the wall .

#### Core-Edge Coupling: The Principle of Flux Conservation

The interface between the core and edge domains is the separatrix. For a coupled model to be physically meaningful, it must obey the fundamental laws of conservation for particles, momentum, and energy. The integral form of a conservation law for a quantity with density $U$ and flux $\mathbf{F}$ over a volume $V$ states that the rate of change of the total inventory equals the volumetric sources minus the net flux through the boundary $\partial V$.

When we partition the total plasma volume into a core domain $V_c$ and an edge domain $V_e$, they share a common boundary: the [separatrix](@entry_id:175112) surface $\Sigma$. For global conservation to hold, the flux of any conserved quantity leaving the core domain across $\Sigma$ must be exactly equal to the flux entering the edge domain across $\Sigma$.

This principle has a direct and critical implication for coupling numerical codes: the total net flux of particles ($\Gamma_s$), heat ($Q_s$), and toroidal momentum ($\Pi$) must be continuous across the interface. When a core code calculates the radial fluxes at the [separatrix](@entry_id:175112), it is calculating the sum of all physical contributions, $\mathbf{F} = \mathbf{F}^{\text{nc}} + \mathbf{F}^{\text{turb}}$. It is this **total net flux** that must be provided to the edge code as a boundary source term. Passing only the turbulent component, for example, would implicitly assume the neoclassical flux stops at the separatrix, artificially breaking conservation. Similarly, passing [state variables](@entry_id:138790) like temperature and density and allowing each code to compute its own boundary flux is not guaranteed to be conservative, as different [numerical schemes](@entry_id:752822) will yield different flux values .

In some simplified modeling contexts, the physics of the SOL and sheath are abstracted into a direct boundary condition at the separatrix for the core model. In a "sheath-limited" regime, where the SOL is assumed to be a source-free, collisionless region, the Bohm criterion and sheath heat transmission are applied directly at the separatrix. This leads to a boundary condition for the core model where the outflow velocity is set to the sound speed and the heat flux is given by the sheath transmission formula, evaluated at the separatrix conditions .

### Computational Models and Coupling Strategies

Implementing these physical principles in a computational framework requires specific mathematical models and [robust numerical algorithms](@entry_id:754393).

#### Models for the Edge: Drift-Reduced Braginskii Equations

The plasma in the SOL is a highly complex environment, characterized by strong turbulence, large-amplitude fluctuations, and strong gradients. While a full six-dimensional kinetic description is computationally prohibitive for routine simulations, fluid models offer a tractable alternative. However, the full fluid equations (e.g., Braginskii equations) are also challenging to solve.

For SOL turbulence, it is common to use **[drift-reduced fluid models](@entry_id:1123985)**. These models are derived from the full Braginskii equations by applying a systematic ordering scheme appropriate for low-frequency, electrostatic turbulence with long parallel wavelengths ($k_\| \ll k_\perp$). Key assumptions include neglecting electron inertia and assuming the perpendicular fluid velocity is dominated by the $\mathbf{E} \times \mathbf{B}$ drift.

This reduction procedure simplifies the complex system into a more manageable set of equations that still captures the essential physics of drift-wave and ballooning-type turbulence. Two of the key resulting equations are:
1.  The **parallel Ohm's law**: Derived from the electron parallel momentum equation by neglecting electron inertia, it relates the parallel electric field to the electron pressure gradient and resistive effects:
    $$
    \partial_\| \phi = \frac{1}{n e} \partial_\| p_e - \eta J_\|
    $$
    Here $\phi$ is the electrostatic potential, $p_e$ is the electron pressure, $\eta$ is the parallel resistivity, and $J_\|$ is the parallel current density.

2.  The **vorticity equation**: Derived from the current continuity equation $\nabla \cdot \mathbf{J} = 0$, it describes the evolution of plasma vorticity $\Omega \equiv \nabla_\perp^2 \phi$. In the drift-reduced limit, the divergence of the perpendicular current is dominated by the ion [polarization current](@entry_id:196744), leading to an equation of the form:
    $$
    \frac{m_i n}{B^2} \left( \frac{\partial}{\partial t} + \mathbf{u}_E \cdot \nabla \right) \nabla_{\perp}^2 \phi = \partial_\| J_\|
    $$
    This equation couples the perpendicular dynamics (driven by the $\mathbf{u}_E \cdot \nabla$ advection of vorticity) to the parallel dynamics (driven by the divergence of the parallel current). These equations, along with continuity and energy equations, form the basis for many modern edge turbulence codes .

#### Numerical Implementation of Conservative Coupling

Translating the principle of flux conservation into a working numerical algorithm requires a precise protocol. As established, the flux out of the core must equal the flux into the edge at the discrete level.

A protocol that guarantees this property must feature several key elements:
-   **Exchanged Quantity**: The codes must exchange the **area-integrated interface fluxes** themselves (e.g., total particles/second, total Watts). One code calculates the flux, and the other code uses that exact numerical value as its boundary source/sink term. This [direct exchange](@entry_id:145804) of flux is the most robust way to enforce conservation.
-   **Synchronization**: The coupled codes must advance with the same time step, $\Delta t$, and use a consistent time-centering scheme for the exchanged boundary flux. Mismatches in timing would break discrete conservation.
-   **Geometric Consistency**: If pointwise fluxes are exchanged, the codes must share an identical discretization of the interface surface and use the same area elements to ensure that the integrated flux is identical in both.

To verify that the implementation is correct, two types of numerical diagnostics, or checksums, are essential:
1.  An **interface [antisymmetry](@entry_id:261893) residual**: If $\Phi^{\Sigma,c}$ is the integrated flux leaving the core and $\Phi^{\Sigma,e}$ is the integrated flux entering the edge, the coupling contract requires $\Phi^{\Sigma,c} = \Phi^{\Sigma,e}$. A residual defined as $R_{\Sigma} = \Phi^{\Sigma,c}_{\text{out}} + \Phi^{\Sigma,e}_{\text{out}}$ (where both fluxes are defined with respect to their domain's outward normal) must be zero to machine precision.
2.  A **global balance residual**: After each time step, the total change in the inventory of a conserved quantity over the entire simulated volume ($V_c \cup V_e$) must equal the total volumetric sources minus the losses at the external physical boundaries (the divertor and wall). A residual defined as:
    $$
    R_{\text{global}} = [\text{Total inventory change}] - \Delta t \times [\text{Total sources} - \text{Wall losses}]
    $$
    must also be zero to numerical precision. Monitoring these residuals is a critical step in verifying the correctness of a coupled simulation .

#### Advanced Coupling Strategies

Beyond the basic flux-exchange protocol, various computational strategies exist for structuring the coupled solve.

**Domain Decomposition Methods**
The way boundary information is exchanged can be viewed through the lens of [domain decomposition methods](@entry_id:165176) from applied mathematics.
-   **Non-overlapping Decomposition**: The domains meet at a sharp interface. A simple **Dirichlet-Neumann** iteration involves passing the state (e.g., temperature $T$) from the core to the edge (a Dirichlet condition), and the resulting flux $q$ from the edge back to the core (a Neumann condition). This process is iterated until both $T$ and $q$ are continuous, ensuring conservation at convergence. A more advanced **Robin-Robin** scheme, which exchanges a linear combination of the state and the flux, can significantly accelerate convergence while still guaranteeing conservation.
-   **Overlapping Decomposition**: The domains overlap in a finite region. In a classical **Schwarz iteration**, each code solves its problem using boundary data taken from the other code's solution inside the overlap region. For example, the core code solves on $[0, x_I+\delta]$ using a Dirichlet boundary condition at $x_I+\delta$ provided by the edge code's solution. As the iteration converges, the solutions in the overlap region become identical, which implicitly ensures the continuity of both the state and its flux, thereby achieving a [conservative coupling](@entry_id:747708) without explicit [flux exchange](@entry_id:1125155) .

**Hybrid Kinetic-Fluid Coupling**
Coupling models based on different physical descriptions, such as a **gyrokinetic (GK) core** and a **fluid edge**, introduces further complexity. The boundary condition must respect the mathematical nature of both models. The gyrokinetic equation, being a form of the Vlasov equation, is a first-order [hyperbolic partial differential equation](@entry_id:1126291) in a 5D phase space.

The fundamental rule for such equations is that boundary data can only be specified on the **inflow** portion of the boundary—that is, for phase-space coordinates corresponding to characteristics that are entering the computational domain. For a GK core simulation with its boundary at the separatrix, inflow corresponds to gyrocenters with a radial velocity $\dot{\psi}  0$. The distribution function $f_s$ for these inflowing particles is prescribed, typically by constructing a distribution whose low-order [velocity moments](@entry_id:1133763) (density, flow, temperature) match those provided by the adjacent fluid edge model.

The distribution function on the **outflow** part of the boundary ($\dot{\psi} > 0$) must not be prescribed; it is determined by the characteristics exiting from the core interior. The total radial flux across the separatrix is the sum of contributions from both the prescribed inflow and the internally determined outflow. For a [conservative coupling](@entry_id:747708), the parameters of the inflow distribution must be adjusted such that this total GK flux matches the flux provided by the fluid edge model. This creates a highly non-linear, self-consistent boundary condition that respects both the kinetic physics and the global conservation laws .