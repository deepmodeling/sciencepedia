## Introduction
In the field of [numerical ocean modeling](@entry_id:1128987), one of the most fundamental design choices is how to represent the ocean's upper boundary—the dynamic interface with the atmosphere. This decision leads to two classical approaches: the prognostic [free-surface formulation](@entry_id:1125301), which allows sea level to evolve freely, and the [rigid-lid approximation](@entry_id:1131032), which assumes a fixed upper surface. This choice creates a critical trade-off between physical fidelity and computational cost, dictating a model's suitability for different scientific questions, from simulating tsunamis to predicting long-term climate change. This article addresses this core dilemma by providing a detailed examination of both formulations.

Across the following chapters, you will gain a thorough understanding of these two foundational techniques. The first chapter, **Principles and Mechanisms**, will dissect the governing equations and numerical consequences of each approach, explaining how the free-surface model supports fast-propagating gravity waves and why the rigid-lid model was developed to filter them. The second chapter, **Applications and Interdisciplinary Connections**, will explore the practical ramifications, showing why certain applications like climate modeling favor the rigid-lid while coastal dynamics demand a free surface, and how this choice impacts fields like data assimilation. Finally, the **Hands-On Practices** section provides targeted problems to solidify your comprehension of the theoretical and computational concepts discussed.

## Principles and Mechanisms

In the study of oceanic circulation through numerical modeling, a fundamental choice must be made regarding the representation of the ocean's upper boundary: the interface between the ocean and the atmosphere. This choice dictates how changes in sea level are handled and has profound implications for both the physical fidelity and the computational cost of the model. The two classical approaches are the **prognostic free-surface** formulation, which explicitly calculates the evolution of the sea surface height, and the **rigid-lid** approximation, which assumes a fixed, non-evolving upper boundary. This chapter delves into the principles and mechanisms underpinning these two formulations, exploring their governing equations, numerical consequences, and respective domains of applicability.

### The Free-Surface Formulation: A Complete Physical Representation

The most physically complete representation of the large-scale ocean within the hydrostatic Boussinesq framework is the free-surface model. It treats the sea surface elevation, denoted by $\eta(x,y,t)$, as a fully prognostic variable of the system, allowing it to evolve in space and time in response to oceanic and atmospheric forcing.

#### Governing Equations

The dynamics of a rotating, stratified ocean are described by the **primitive equations**. Under the Boussinesq and hydrostatic approximations, a standard set of these equations for a free-surface model is as follows :

The **horizontal momentum equations** describe the balance of forces acting on a fluid parcel in the horizontal plane:
$$
\frac{Du}{Dt} - fv = -\frac{1}{\rho_0}\frac{\partial p}{\partial x} + \mathcal{D}_u
$$
$$
\frac{Dv}{Dt} + fu = -\frac{1}{\rho_0}\frac{\partial p}{\partial y} + \mathcal{D}_v
$$
Here, $\mathbf{u}_h = (u,v)$ is the horizontal velocity vector, $\frac{D}{Dt} = \frac{\partial}{\partial t} + u\frac{\partial}{\partial x} + v\frac{\partial}{\partial y} + w\frac{\partial}{\partial z}$ is the material derivative, $f$ is the Coriolis parameter, $\rho_0$ is a constant reference density, $p$ is the pressure, and $\mathcal{D}_u, \mathcal{D}_v$ represent frictional and mixing terms.

The **hydrostatic balance** dictates that in the vertical, the pressure gradient force is balanced by gravity. For a fluid with density $\rho = \rho_0 + \rho'$, where $\rho'$ is the density anomaly, this is:
$$
\frac{\partial p}{\partial z} = -\rho g = -(\rho_0 + \rho')g
$$
Here, $g$ is the gravitational acceleration. The density anomaly is related to the buoyancy, $b$, often defined as $b = -g\rho'/\rho_0$.

The **[incompressibility](@entry_id:274914) condition** for a Boussinesq fluid simplifies mass conservation to the statement that the velocity field is [divergence-free](@entry_id:190991):
$$
\frac{\partial u}{\partial x} + \frac{\partial v}{\partial y} + \frac{\partial w}{\partial z} = 0
$$

The transport of tracers, such as potential temperature ($\theta$) and salinity ($S$), which determine the density anomaly, is governed by an **[advection-diffusion equation](@entry_id:144002)**:
$$
\frac{D\theta}{Dt} = \mathcal{D}_\theta, \quad \frac{DS}{Dt} = \mathcal{D}_S
$$

The evolution of the free surface itself is governed by the **kinematic free-surface condition**. This condition states that a fluid particle on the surface remains on the surface. At $z=\eta(x,y,t)$, this gives:
$$
w = \frac{\partial \eta}{\partial t} + u \frac{\partial \eta}{\partial x} + v \frac{\partial \eta}{\partial y}
$$
By integrating the incompressibility equation over the depth of the water column (from the bottom at $z=-H(x,y)$ to the surface at $z=\eta$) and applying the kinematic boundary conditions at both the surface and the bottom, we obtain the prognostic equation for the free-surface elevation:
$$
\frac{\partial \eta}{\partial t} + \frac{\partial}{\partial x}\left(\int_{-H}^{\eta} u\,dz\right) + \frac{\partial}{\partial y}\left(\int_{-H}^{\eta} v\,dz\right) = 0
$$
This equation is paramount: it demonstrates that the rate of change of the sea surface height is directly coupled to the divergence of the depth-integrated horizontal transport. In this formulation, the sea surface height $\eta$ is a **prognostic variable**, meaning its future state is determined by integrating a time-evolution equation, alongside the prognostic variables of horizontal velocity ($u,v$) and tracers ($\theta, S$). In contrast, vertical velocity ($w$) and pressure ($p$) are **diagnostic variables**, calculated from the prognostic fields at each instant in time .

#### External Gravity Waves and the Computational Cost

The coupling between the free surface and the barotropic (depth-averaged) flow gives rise to a class of motions known as **external gravity waves**. These are the fastest-propagating waves in the hydrostatic ocean. For long waves, where the wavelength is much greater than the water depth, their phase speed $c$ is given by:
$$
c = \sqrt{gH}
$$
This result can be rigorously derived from the linearized [shallow-water equations](@entry_id:754726)  or by taking the long-wave limit ($kH \to 0$, where $k$ is the wavenumber) of the more general dispersion relation for non-hydrostatic [surface waves](@entry_id:755682), $\omega^2 = gk \tanh(kH)$ . When rotation is included, these waves are known as **[inertia-gravity waves](@entry_id:1126476)** or **Poincaré waves**, with a dispersion relation $\omega^2 = f^2 + gH(k^2 + \ell^2)$ for horizontal wavenumbers $k$ and $\ell$ .

The existence of these fast waves poses a significant computational challenge. Explicit [numerical time-stepping](@entry_id:1128999) schemes, which are computationally simple per step, are subject to a stability constraint known as the **Courant-Friedrichs-Lewy (CFL) condition**. For wave propagation, this condition requires that the [numerical domain of dependence](@entry_id:163312) must contain the physical domain of dependence, which for a simple explicit scheme takes the form:
$$
\frac{c \Delta t}{\Delta x} \le 1
$$
where $\Delta t$ is the time step and $\Delta x$ is the horizontal grid spacing. Given a typical deep-ocean depth of $H = 4000 \ \mathrm{m}$, the external gravity wave speed is $c \approx \sqrt{9.81 \ \mathrm{m\,s^{-2}} \times 4000 \ \mathrm{m}} \approx 200 \ \mathrm{m\,s^{-1}}$. For a model with a grid spacing of $\Delta x = 25 \ \mathrm{km}$, the maximum allowable time step would be $\Delta t_{\max} \approx \Delta x / c = 25000 \ \mathrm{m} / 200 \ \mathrm{m\,s^{-1}} = 125 \ \mathrm{s}$ . This is an extremely short time step for simulations of climate-scale phenomena that evolve over decades or centuries, rendering such an explicit free-surface model computationally prohibitive for many applications.

### The Rigid-Lid Approximation: A Computational Expedient

To circumvent the stringent [time-step constraint](@entry_id:174412) imposed by external gravity waves, early [ocean general circulation models](@entry_id:1129060) (OGCMs) developed the **[rigid-lid approximation](@entry_id:1131032)**. This approach fundamentally alters the upper boundary condition to filter out the problematic fast waves.

#### The Core Principle and its Consequences

The [rigid-lid approximation](@entry_id:1131032) consists of replacing the dynamic free surface with a flat, impenetrable "lid" at a fixed vertical level, typically $z=0$. Mathematically, this imposes two constraints :
1.  The sea surface elevation is set to zero for all time and space: $\eta(x,y,t) \equiv 0$.
2.  Consequently, the kinematic boundary condition at the surface becomes a [no-penetration condition](@entry_id:191795): $w(x,y,0,t) = 0$.

By eliminating the prognostic evolution of $\eta$, the mechanism that supports external gravity waves is removed from the [model physics](@entry_id:1128046). A linear wave analysis of the rigid-lid system shows that for any non-zero wavenumber, the only possible solutions are steady (frequency $\omega=0$), corresponding to geostrophic flows. All time-dependent, propagating barotropic wave solutions are filtered out .

With $\eta$ removed, the prognostic equation for surface height is replaced by a diagnostic constraint on the flow. The depth-integrated continuity equation now becomes:
$$
\nabla_h \cdot \left(\int_{-H}^{0} \mathbf{u}_h \, dz\right) = 0
$$
This equation states that the barotropic volume transport must be **non-divergent**. This is a powerful constraint, but the momentum equations do not guarantee it will be satisfied on their own. The system is over-constrained unless a new degree of freedom is introduced.

#### The Role of Surface Pressure as a Lagrange Multiplier

To satisfy the non-divergence constraint, a new, depth-independent pressure field is introduced. This is often called the **surface pressure** or **barotropic pressure**, and we will denote it here by $\pi(x,y,t)$. This variable acts as a **Lagrange multiplier** whose purpose is to adjust the flow field at each time step to enforce the constraint of zero barotropic divergence  .

The total pressure $p$ is decomposed into a barotropic surface component $\pi$ and a baroclinic component that depends on the internal density structure. A consistent decomposition under the rigid-lid and hydrostatic approximations is :
$$
p(x,y,z,t) = p_a - \rho_0 g z + \int_{z}^{0} g \rho'(x,y,z',t) \,dz' + \pi(x,y,t)
$$
where $p_a$ is the (assumed constant) atmospheric pressure. The first two terms represent the reference [hydrostatic pressure](@entry_id:141627), the integral term is the baroclinic pressure anomaly due to stratification, and $\pi(x,y,t)$ is the new surface pressure.

The crucial point is that $\pi$ is a function of horizontal position and time only ($\partial \pi / \partial z = 0$). In the horizontal momentum equations, the pressure gradient term $-\frac{1}{\rho_0}\nabla_h p$ now contains the term $-\frac{1}{\rho_0}\nabla_h \pi$, which acts as a depth-independent forcing. The [surface pressure](@entry_id:152856) $\pi$ is determined diagnostically at each time step by taking the divergence of the depth-integrated momentum equations and substituting the constraint $\nabla_h \cdot \mathbf{U} = 0$. This procedure results in a two-dimensional **elliptic (Poisson-type) equation** for $\pi$. Solving this global elliptic equation is computationally demanding, but for long climate integrations, it is far more efficient than taking the extremely small time steps required by an explicit free-surface model  .

### A Critical Comparison of Formulations

The choice between a free-surface and a rigid-lid formulation involves a fundamental trade-off between physical fidelity and computational cost .

-   **Rigid-Lid Formulation:**
    -   **Pros:** Allows for a much larger time step (typically limited by advection or internal wave speeds), making it computationally efficient for long-term, global climate simulations focused on baroclinic dynamics and thermohaline circulation.
    -   **Cons:** Filters out external gravity waves, rendering it incapable of simulating phenomena that depend on sea-level variations, such as tides, tsunamis, and storm surges. It also requires a global elliptic solve for the surface pressure, which can be a bottleneck on parallel computers.

-   **Free-Surface Formulation:**
    -   **Pros:** Physically more complete, as it retains the prognostic free surface and the associated barotropic dynamics. It is essential for modeling sea-level variability, tides, and coastal processes.
    -   **Cons:** When used with a simple explicit time-stepping scheme, it is subject to a very restrictive CFL time-step limit, making it extremely expensive for large-scale, long-term simulations.

The theoretical consistency of the [rigid-lid approximation](@entry_id:1131032) is often considered in tandem with the Boussinesq approximation. The validity of the rigid lid is justified by a small **Froude number** ($Fr = U/\sqrt{gH} \ll 1$), which indicates that flow speeds are much slower than external wave speeds. The validity of the Boussinesq approximation is justified by small density variations ($|\rho'| \ll \rho_0$). Together, they form a consistent framework for modeling slow, nearly incompressible oceanic flows by filtering the fastest modes: acoustic waves (via Boussinesq) and external gravity waves (via rigid lid) .

### Limitations and Advanced Implementations

While the [rigid-lid approximation](@entry_id:1131032) is a powerful computational tool, it is not without its own set of challenges, particularly in regions of steep topography.

#### The Pressure Gradient Error over Topography

A significant artifact of the [rigid-lid approximation](@entry_id:1131032) is the generation of spurious barotropic vorticity over rapidly varying bathymetry. This is often termed the **[pressure gradient error](@entry_id:1130147)**. The source of barotropic vorticity in the [primitive equations](@entry_id:1130162) comes from the curl of the depth-integrated pressure gradient force. This force has two main components: one from the sea surface slope and one from the internal density field interacting with the bottom slope. The latter is known as the **Joint Effect of Baroclinicity And Relief (JEBAR)**. In the real ocean, the free surface $\eta$ adjusts dynamically such that the torque from the surface slope tends to cancel the torque from the JEBAR term.

A rigid-lid model, by enforcing $\eta \equiv 0$, artificially removes the compensating surface torque term. This leaves the JEBAR term unbalanced, acting as a large, spurious source of barotropic vorticity in the model, which can drive unrealistic currents along isobaths . Correcting for this error requires careful and consistent treatment of the baroclinic pressure forcing in the [barotropic mode](@entry_id:1121351) equations, or abandoning the [rigid-lid approximation](@entry_id:1131032) altogether.

#### Modern Solutions: The Semi-Implicit Free Surface

Modern ocean models have largely moved beyond the strict dichotomy of explicit free-surface versus rigid-lid. The preferred method is often a **semi-implicit** (or **split-explicit**) [free-surface formulation](@entry_id:1125301) . In this approach, the terms in the governing equations responsible for the fast propagation of external gravity waves—the [surface pressure](@entry_id:152856) gradient and the divergence of barotropic transport—are treated implicitly in time. This means they are evaluated at the future time step, leading to an elliptic Helmholtz equation for the surface elevation $\eta$ at the new time.

This method combines the best of both worlds:
-   It retains the prognostic free surface $\eta$, allowing for the accurate simulation of tides and other sea-level phenomena.
-   By treating the fast modes implicitly, it removes the strict CFL [time-step constraint](@entry_id:174412) associated with external gravity waves, allowing for time steps comparable to those of a rigid-lid model.

The semi-implicit [free-surface formulation](@entry_id:1125301) preserves the phase speed of gravity waves with [second-order accuracy](@entry_id:137876) in the time step while remaining stable, and has become the state-of-the-art for a wide range of ocean modeling applications  .