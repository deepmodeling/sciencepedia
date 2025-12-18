## Introduction
The vast and complex motions of Earth's oceans and atmosphere, from global-scale currents to swirling weather systems, are all governed by a common set of physical laws. The Governing Equations of Geophysical Fluid Dynamics provide the mathematical framework for describing and predicting these phenomena. However, the complete equations are immensely complex, encompassing processes across a vast range of scales, from molecular interactions to planetary-scale waves. The central challenge lies in systematically simplifying this framework to isolate the key dynamics relevant to large-scale circulation without losing essential physics. This article addresses this challenge by providing a comprehensive exploration of these foundational equations. It begins by deriving the equations from first principles and introducing the critical approximations that make them tractable. It then demonstrates how these simplified models are applied to explain and predict key features of ocean and [atmospheric circulation](@entry_id:199425), from [wind-driven gyres](@entry_id:1134086) to deep overturning. Finally, it provides hands-on exercises to solidify these theoretical concepts. We will begin our journey in the "Principles and Mechanisms" chapter, starting with the core assumption of a fluid continuum and building towards the powerful conservation laws that govern our fluid planet.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that govern the motion of fluids in the geophysical context of oceans and atmospheres. Building upon the introductory concepts, we will derive the governing equations from first principles of physics, introduce the critical approximations that render them tractable for large-scale phenomena, and explore the dominant dynamical balances that emerge. Our journey will progress from the foundational assumption of a fluid continuum to the powerful, integrated conservation laws that explain the [large-scale structure](@entry_id:158990) of planetary circulations.

### The Foundational Framework

The description of a planet's oceans and atmosphere as a fluid system begins with a set of core physical assumptions and mathematical formulations. These transform the discrete, molecular reality into a continuous medium whose behavior can be described by partial differential equations.

#### The Continuum Hypothesis

The very first step in formulating the equations of fluid dynamics is the **continuum hypothesis**. This principle asserts that we can treat a fluid, such as seawater or air, as a continuous substance, or a **continuum**, ignoring its discrete molecular nature. In this view, fluid properties like density, pressure, and velocity are considered to be well-defined functions of space and time, averaged over a volume that is infinitesimal from a macroscopic viewpoint but still contains an enormous number of molecules.

The validity of this hypothesis depends on the separation of scales between the microscopic world of molecules and the macroscopic world of the flow phenomena being studied. This separation is quantified by a dimensionless parameter known as the **Knudsen number**, $K_n$, defined as:

$K_n = \frac{\lambda}{L}$

Here, $\lambda$ is a characteristic microscopic length scale of the fluid (such as the mean free path for gases or an effective molecular correlation length for liquids), and $L$ is the characteristic macroscopic length scale of the flow or the measurement probe. The [continuum hypothesis](@entry_id:154179) is valid when the Knudsen number is very small, typically $K_n \ll 1$. A common threshold for the accurate application of standard continuum mechanics (i.e., the Navier-Stokes equations) is $K_n \lesssim 10^{-2}$.

To illustrate this, consider two scenarios in oceanography . First, a high-resolution computational ocean model that resolves turbulent eddies down to a grid scale of $L_g = 1 \text{ mm}$. For seawater, the effective molecular length scale is approximately $\lambda \approx 0.3 \text{ nm}$. The Knudsen number for this simulation is $K_{n,g} = (0.3 \times 10^{-9} \text{ m}) / (1 \times 10^{-3} \text{ m}) = 3 \times 10^{-7}$. Since this value is vastly smaller than $10^{-2}$, the [continuum hypothesis](@entry_id:154179) is unequivocally justified, allowing us to use differential conservation laws to model the flow.

In contrast, consider a hypothetical scenario of a thin brine film trapped in marine sediments, with a thickness of $L_n = 3 \text{ nm}$. Here, the macroscopic scale is comparable to the molecular scale. The Knudsen number is $K_{n,n} = (0.3 \times 10^{-9} \text{ m}) / (3 \times 10^{-9} \text{ m}) = 0.1$. This value is not much smaller than 1 and falls into a regime where the continuum approximation breaks down. To describe the fluid behavior in such nanoconfined spaces, one would need to resort to methods that explicitly account for molecular dynamics. For the vast majority of oceanic and atmospheric phenomena, however, the scales are such that $K_n \ll 1$, and the [continuum hypothesis](@entry_id:154179) provides a robust foundation.

#### The Complete Governing Equations in a Rotating Frame

With the [continuum hypothesis](@entry_id:154179) established, we can state the laws of conservation of mass, momentum, and energy in their differential form. For geophysical fluids, it is essential to formulate these laws in a reference frame that rotates with the planet. This introduces [apparent forces](@entry_id:1121068)—the **Coriolis force** and the **[centrifugal force](@entry_id:173726)**—that are crucial for understanding the dynamics.

In vector form, the conservation of momentum (Newton's Second Law) in a frame rotating with angular velocity $\boldsymbol{\Omega}$ is:

$\frac{D \boldsymbol{u}}{D t} + 2 \boldsymbol{\Omega} \times \boldsymbol{u} = -\frac{1}{\rho}\nabla p + \boldsymbol{g} + \boldsymbol{F}_{visc}$

Here, $\boldsymbol{u}$ is the velocity vector relative to the rotating frame, $\rho$ is the density, $p$ is the pressure, $\boldsymbol{g}$ is the true gravitational acceleration, and $\boldsymbol{F}_{visc}$ represents viscous forces. The term $\frac{D \boldsymbol{u}}{D t} \equiv \frac{\partial \boldsymbol{u}}{\partial t} + (\boldsymbol{u} \cdot \nabla)\boldsymbol{u}$ is the **[material derivative](@entry_id:266939)**, representing the acceleration of a fluid parcel. The term $2 \boldsymbol{\Omega} \times \boldsymbol{u}$ is the Coriolis acceleration. The centrifugal force is typically absorbed into an "[effective gravity](@entry_id:188792)" term, which we will also denote by $\boldsymbol{g}$.

To appreciate the full complexity of these equations, it is instructive to write them in a coordinate system natural to a spherical planet, such as [spherical coordinates](@entry_id:146054) $(\lambda, \phi, r)$ corresponding to longitude, latitude, and radial distance. When expanded, the component equations include **metric terms** that arise from the curvature of the coordinate system. For example, under the **Boussinesq and traditional approximations** (which we will discuss later), the full momentum and continuity equations take a complex form . The zonal ($u$), meridional ($v$), and radial ($w$) momentum equations become:

$\frac{D u}{D t} - \frac{u v \tan\phi}{r} + \frac{u w}{r} - f v = - \frac{1}{\rho_0} \frac{1}{r \cos\phi} \frac{\partial p}{\partial \lambda}$

$\frac{D v}{D t} + \frac{u^2 \tan\phi}{r} + \frac{v w}{r} + f u = - \frac{1}{\rho_0} \frac{1}{r} \frac{\partial p}{\partial \phi}$

$\frac{D w}{D t} - \frac{u^2 + v^2}{r} = - \frac{1}{\rho_0} \frac{\partial p}{\partial r} - g$

The material derivative itself expands as $\frac{D}{D t} = \frac{\partial}{\partial t} + \frac{u}{r \cos\phi} \frac{\partial}{\partial \lambda} + \frac{v}{r} \frac{\partial}{\partial \phi} + w \frac{\partial}{\partial r}$. The Coriolis parameter is $f(\phi) = 2 \Omega \sin\phi$, and its northward gradient is $\beta(\phi) = \frac{1}{r}\frac{\partial f}{\partial \phi} = \frac{2 \Omega \cos\phi}{r}$. The complexity of this full system motivates the search for systematic simplifications and approximations that are valid for specific classes of geophysical motions.

#### The Equation of State and Buoyancy

The density $\rho$ is not an [independent variable](@entry_id:146806) but is determined by the composition, temperature, and pressure of the fluid. This relationship is encapsulated in the **equation of state**. For seawater, density is a function of salinity $S$, temperature $T$, and pressure $p$:

$\rho = \rho(S, T, p)$

The sensitivity of density to changes in temperature and salinity is of paramount importance, as these density variations drive buoyancy forces. We can quantify this sensitivity by defining two key coefficients around a [reference state](@entry_id:151465) $(S_0, T_0, p_0)$ :

1.  The **[coefficient of thermal expansion](@entry_id:143640)**, $\alpha$, is the fractional change in density per unit change in temperature at constant salinity and pressure. It is formally defined as:
    $\alpha \equiv -\frac{1}{\rho}\left(\frac{\partial \rho}{\partial T}\right)_{S,p}$
    For most oceanic conditions, warming a water parcel causes it to expand and its density to decrease, so $(\partial \rho / \partial T)$ is negative, making $\alpha > 0$.

2.  The **coefficient of haline contraction**, $\beta$, is the fractional change in density per unit change in salinity at constant temperature and pressure:
    $\beta \equiv \frac{1}{\rho}\left(\frac{\partial \rho}{\partial S}\right)_{T,p}$
    Adding salt increases the mass more than the volume, so density always increases with salinity. Thus, $(\partial \rho / \partial S)$ is positive, making $\beta > 0$.

For small deviations ($T'$, $S'$) from a reference state $(T_0, S_0)$, the density perturbation $\rho'$ can be approximated by a linearized equation of state:

$\rho' \approx \left(\frac{\partial \rho}{\partial T}\right) T' + \left(\frac{\partial \rho}{\partial S}\right) S' = -\rho_0 \alpha T' + \rho_0 \beta S'$

This linearized form is the cornerstone for studying **buoyancy**, which is the force exerted on a fluid parcel due to its density difference with the surrounding fluid. The stability of the water column to vertical displacements is measured by the **Brunt-Väisälä frequency** (or buoyancy frequency), $N$, whose square is given by:

$N^2 \approx g \left( \alpha \frac{\partial T}{\partial z} - \beta \frac{\partial S}{\partial z} \right)$

where $z$ is the vertical coordinate (positive upwards). A stable stratification ($N^2 > 0$) is promoted by temperature decreasing with depth and/or salinity increasing with depth.

#### Conservation of Tracers: The Advection-Diffusion Equation

The principles of conservation can be extended to any scalar quantity $C$ carried by the fluid, such as heat (temperature), salt (salinity), or a chemical constituent. If the tracer is **passive**, it means its concentration does not affect the fluid's momentum (i.e., its density). The concentration $C(\boldsymbol{x}, t)$ evolves due to three processes: transport by the resolved flow (**advection**), transport by unresolved, small-scale turbulent motions (**diffusion**), and local sources or sinks.

The governing equation for a passive tracer, known as the **[advection-diffusion equation](@entry_id:144002)**, can be written in terms of the material derivative :

$\frac{D C}{D t} = \nabla \cdot (\boldsymbol{\kappa} \nabla C) + S$

Let's break down each term:
-   $\frac{D C}{D t} \equiv \frac{\partial C}{\partial t} + \boldsymbol{u} \cdot \nabla C$ is the **material tendency**, representing the rate of change of the tracer concentration experienced by a fluid parcel as it moves with the flow. The term $\boldsymbol{u} \cdot \nabla C$ is the **advective flux convergence**.
-   $\nabla \cdot (\boldsymbol{\kappa} \nabla C)$ is the convergence of the diffusive flux. Following **Fick's law**, diffusion is a down-gradient process, so the [diffusive flux](@entry_id:748422) is given by $\boldsymbol{q}_d = -\boldsymbol{\kappa} \nabla C$. The term $\boldsymbol{\kappa}$ is the **diffusivity tensor**, which can be anisotropic (e.g., mixing is much stronger horizontally than vertically in a stratified ocean) and vary in space and time.
-   $S$ represents the net rate of tracer addition or removal per unit volume from non-conservative processes, such as biogeochemical reactions, air-sea exchange, or [radioactive decay](@entry_id:142155).

This single equation is fundamental to modeling the distribution of virtually all properties other than momentum in the ocean and atmosphere.

### Key Approximations for Large-Scale Flows

The full governing equations are immensely complex and describe a vast range of phenomena, including those that are irrelevant for large-scale climate dynamics, such as sound waves. To focus on the motions of interest, a hierarchy of systematic approximations is employed.

#### The Boussinesq Approximation: Filtering Sound, Retaining Buoyancy

For most oceanic and many atmospheric flows, the characteristic flow speeds are much smaller than the speed of sound (i.e., the Mach number is small). This implies that density variations due to pressure changes (compressibility) are dynamically insignificant for the fluid's inertia. However, the small density variations due to temperature and salinity are the very source of buoyancy, which is a primary driving force.

The **Boussinesq approximation** elegantly reconciles these facts . It involves a selective simplification of the role of density:
1.  In the **inertia term** of the momentum equation ($\rho \frac{D\boldsymbol{u}}{Dt}$), density variations are considered negligible. The total density $\rho = \rho_0 + \rho'$ is replaced by a constant reference density $\rho_0$. This is justified because $|\rho'|/\rho_0 \ll 1$.
2.  In the **gravity term** ($-\rho g \hat{\boldsymbol{z}}$), the density variation is retained. The term is split into $-(\rho_0 + \rho')g \hat{\boldsymbol{z}} = -\rho_0 g \hat{\boldsymbol{z}} - \rho' g \hat{\boldsymbol{z}}$. The large background term, $-\rho_0 g \hat{\boldsymbol{z}}$, is assumed to be balanced by a background hydrostatic pressure field, and the small perturbation, $-\rho' g \hat{\boldsymbol{z}}$, is retained as the crucial **[buoyancy force](@entry_id:154088)**.
3.  This set of assumptions filters out sound waves and simplifies the continuity equation. The full mass conservation equation, $\frac{D\rho}{Dt} + \rho \nabla \cdot \boldsymbol{u} = 0$, is replaced by the much simpler **[incompressibility constraint](@entry_id:750592)**:
    $\nabla \cdot \boldsymbol{u} = 0$

This approximation distinguishes GFD from the study of a strictly incompressible, homogeneous fluid. In a fully [incompressible fluid](@entry_id:262924), density is constant everywhere ($\rho' = 0$), and there can be no buoyancy forces. The Boussinesq approximation describes a fluid that is dynamically incompressible with respect to inertia but retains the thermodynamic density variations that drive motion.

#### The Diagnostic Role of Pressure in Incompressible Flow

The simplification of the continuity equation to $\nabla \cdot \boldsymbol{u} = 0$ has a profound consequence for the role of pressure . In a compressible fluid, pressure is a thermodynamic state variable determined by an equation of state, e.g., $p = \rho R T$. In an incompressible (or Boussinesq) fluid, the continuity equation is a kinematic constraint on the velocity field, not an evolution equation for density. There is no independent prognostic equation for pressure.

Instead, pressure becomes a **diagnostic variable**. It instantaneously adjusts throughout the fluid domain to ensure that the velocity field remains divergence-free at all times. Mathematically, pressure acts as a **Lagrange multiplier** for the [incompressibility constraint](@entry_id:750592).

This can be seen by taking the divergence of the non-hydrostatic Boussinesq momentum equation. Since $\nabla \cdot (\frac{\partial \boldsymbol{u}}{\partial t})$ must be zero to maintain incompressibility, the operation yields a relationship that the pressure must satisfy at every instant:

$\nabla^2 p = \nabla \cdot \left( -\rho_0(\boldsymbol{u} \cdot \nabla) \boldsymbol{u} - \rho_0 f \hat{\boldsymbol{z}} \times \boldsymbol{u} - \rho' g \hat{\boldsymbol{z}} + \dots \right)$

This is a **Pressure Poisson Equation (PPE)**. It is an elliptic partial differential equation, meaning the pressure at any point is influenced by the entire velocity and buoyancy field at that moment. In non-hydrostatic numerical models, solving this [elliptic equation](@entry_id:748938) is a critical and computationally intensive step required at every time increment to enforce the incompressibility constraint.

#### The Hydrostatic Approximation: A World of Thin Layers

Geophysical fluids are often arranged in thin layers, with horizontal scales ($L$) vastly greater than their vertical scales ($H$). For the large-scale ocean, $L$ might be thousands of kilometers while $H$ is a few kilometers, giving a very small **aspect ratio** $\delta = H/L \ll 1$.

In such systems, a scale analysis of the vertical momentum equation reveals that the vertical acceleration terms are typically many orders of magnitude smaller than the [vertical pressure gradient](@entry_id:1133794) and gravity terms . This leads to the **[hydrostatic approximation](@entry_id:1126281)**, where the vertical momentum equation is simplified to a balance between the vertical pressure gradient and gravity:

$\frac{\partial p}{\partial z} = -\rho g$

This balance states that the pressure at any depth is determined by the weight of the fluid column above it. This approximation is exceptionally accurate for most large-scale oceanic and atmospheric motions.

#### The Hydrostatic Primitive Equations

Combining the Boussinesq and hydrostatic approximations yields the **[hydrostatic primitive equations](@entry_id:1126284)**, which are the workhorse of large-scale ocean and climate modeling. The set of equations for an [inviscid fluid](@entry_id:198262) on an [f-plane](@entry_id:265625) is :

-   **Horizontal Momentum:**
    $\frac{D u}{D t} - fv = -\frac{1}{\rho_0}\frac{\partial p}{\partial x}$
    $\frac{D v}{D t} + fu = -\frac{1}{\rho_0}\frac{\partial p}{\partial y}$
-   **Hydrostatic Balance:**
    $\frac{\partial p}{\partial z} = -\rho g$
-   **Continuity:**
    $\frac{\partial u}{\partial x} + \frac{\partial v}{\partial y} + \frac{\partial w}{\partial z} = 0$
-   **Tracer Conservation:**
    $\frac{D C}{D t} = 0$ (for an ideal tracer)

In this system, the vertical velocity $w$ is no longer a prognostic variable with its own momentum equation. Instead, it becomes a **diagnostic variable**. It must be calculated from the horizontal velocity field by integrating the continuity equation vertically:

$w(z) = w(z_{bottom}) - \int_{z_{bottom}}^{z} \left( \frac{\partial u}{\partial x} + \frac{\partial v}{\partial y} \right) dz'$

This reflects the fact that in a hydrostatic fluid, vertical motion is a secondary consequence of the convergence or divergence of the primary horizontal flows.

### Dominant Balances and Their Consequences

Within the framework of the primitive equations, specific dynamical balances dominate in different regions and under different conditions. These balances explain the most prominent features of geophysical circulation.

#### Geostrophic Balance: The Heart of the Interior Flow

In the vast interior of the ocean and atmosphere, far from boundaries and for motions with long time scales, the acceleration and friction terms in the horizontal momentum equations are small compared to the Coriolis and pressure gradient forces. The ratio of acceleration to the Coriolis force is quantified by the **Rossby number**, $Ro = U / (fL)$. For large-scale flows, $Ro \ll 1$.

In this limit, the horizontal momentum equations reduce to a simple but powerful diagnostic relationship known as **geostrophic balance** :

$f \hat{\boldsymbol{k}} \times \boldsymbol{u}_g = -\frac{1}{\rho_0} \nabla_h p$

Here, $\boldsymbol{u}_g$ is the **geostrophic velocity** and $\nabla_h$ is the horizontal [gradient operator](@entry_id:275922). This balance states that the Coriolis force acts to precisely oppose the horizontal pressure [gradient force](@entry_id:166847). This has profound consequences:
-   The flow is directed **parallel** to lines of constant pressure (isobars), not down the pressure gradient.
-   In the Northern Hemisphere ($f>0$), the [geostrophic flow](@entry_id:166112) is such that higher pressure is to its **right**. In the Southern Hemisphere ($f0$), higher pressure is to its **left**.

Geostrophic balance is the fundamental organizing principle of the large-scale, slowly-varying circulation in the mid-latitude oceans and atmosphere.

#### The Thermal Wind Relation: Connecting Flow and Stratification

The hydrostatic and geostrophic balances are deeply intertwined. By combining them, we can relate the vertical structure of the flow to the horizontal structure of the density field. This is the **[thermal wind relation](@entry_id:192206)**.

The derivation involves taking the vertical derivative of the geostrophic balance and the horizontal derivative of the hydrostatic balance. The result is a remarkable equation linking the [vertical shear](@entry_id:1133795) of the geostrophic current to the horizontal density gradient:

$f \frac{\partial \boldsymbol{u}_g}{\partial z} = \frac{g}{\rho_0} \hat{\boldsymbol{k}} \times \nabla_h \rho$

This means that if there is a horizontal gradient in density (e.g., cold, dense water next to warm, light water), there must be a [vertical shear](@entry_id:1133795) in the geostrophic current. The thermal wind relation is immensely powerful: if the three-dimensional density field of the ocean is known from measurements, one can calculate the geostrophic velocity field at all depths relative to the velocity at a single reference level.

#### The Breakdown of Foundational Balances

Understanding the limits of these approximations is as important as understanding the balances themselves. The hydrostatic approximation, and by extension the [thermal wind relation](@entry_id:192206), fails when vertical accelerations become significant . This occurs under two main conditions:
1.  **High Vertical Froude Number:** In phenomena with strong vertical motion, such as deep convective plumes or thunderstorms, the vertical velocity $W$ is large. The breakdown occurs when the vertical Froude number, $Fr_v = W/\sqrt{g'H}$ (where $g'$ is reduced gravity), approaches unity.
2.  **Aspect Ratio of Order One:** For phenomena where the horizontal scale $L$ is comparable to the vertical scale $H$ ($\delta \sim 1$), such as flow over steep topography or small-scale internal waves, the shallow-atmosphere assumption is violated and the flow becomes non-hydrostatic.

When hydrostatic balance fails, the direct link between the [vertical pressure gradient](@entry_id:1133794) and density is broken. Consequently, the **thermal wind relation is no longer valid**. The vertical shear of the flow is no longer constrained by the horizontal density gradients, and other dynamical processes, such as ageostrophic circulations and [inertia-gravity waves](@entry_id:1126476), can produce strong vertical shear independent of the thermal structure. It is crucial to note that the geostrophic and hydrostatic balances are independent; a flow can be geostrophic ($Ro \ll 1$) but non-hydrostatic ($Fr_v \sim 1$), as might be the case in a rapidly rotating convective system.

### Integrated Dynamics and Conservation Principles

Beyond local force balances, the large-scale behavior of geophysical fluids is governed by powerful integrated conservation laws, particularly those related to vorticity.

#### Vorticity Balances: The Sverdrup Relation

Wind blowing over the ocean surface exerts a stress, $\boldsymbol{\tau}$, which transfers momentum and vorticity to the water. To understand the basin-scale response to this forcing, we can examine the depth-integrated [vorticity balance](@entry_id:1133913). For a steady, linear (low Rossby number) flow over a flat-bottomed ocean on a $\beta$-plane (where $f$ varies linearly with latitude), a remarkable balance emerges, known as the **Sverdrup balance** :

$\beta V = \frac{1}{\rho_0} \hat{\boldsymbol{k}} \cdot (\nabla_h \times \boldsymbol{\tau})$

Here, $V = \int_{-H}^0 v dz$ is the total depth-integrated meridional (north-south) transport, and $\beta$ is the northward gradient of the Coriolis parameter. This equation states that the northward transport in the ocean interior is directly determined by the curl of the wind stress. The term $\beta V$ represents the change in planetary vorticity experienced by a water column as it moves north or south. In Sverdrup balance, this change is balanced by the vorticity input from the wind. This simple relation explains the broad, slow, interior flow of the great subtropical and subpolar ocean gyres.

#### The Ultimate Conservation Law: Potential Vorticity

Perhaps the most powerful unifying concept in all of geophysical fluid dynamics is the principle of **potential vorticity (PV) conservation**. Potential vorticity is a scalar quantity that combines information about the fluid's rotation (vorticity) and its stratification. For a Boussinesq fluid, the **Ertel potential vorticity**, $q$, is defined as:

$q = (\nabla \times \boldsymbol{u} + 2\boldsymbol{\Omega}) \cdot \nabla b = \boldsymbol{\omega}_a \cdot \nabla b$

Here, $\boldsymbol{\omega}_a$ is the [absolute vorticity](@entry_id:262794) vector (relative plus planetary) and $\nabla b$ is the gradient of a [conserved scalar](@entry_id:1122921) property, such as buoyancy $b$ (or potential temperature in the atmosphere).

The power of PV lies in **Ertel's theorem**, which states that $q$ is materially conserved for a fluid parcel under ideal conditions :

$\frac{Dq}{Dt} = 0 \quad \text{if the flow is inviscid and adiabatic.}$

This means that in the absence of friction and diabatic processes (heating/cooling), each fluid parcel retains its value of $q$ as it moves through the ocean or atmosphere. This conservation law acts as a powerful "dynamical tracer" and imposes a strong constraint on the fluid's motion. For example, if a column of fluid is stretched vertically (increasing the distance between surfaces of constant buoyancy, thus decreasing $|\nabla b|$), its [absolute vorticity](@entry_id:262794) must increase to conserve $q$. This principle explains a vast array of phenomena, including the intensification of currents on the western sides of ocean basins (western boundary currents), the behavior of atmospheric Rossby waves, and the stability of large-scale flows. Any force that has a non-zero curl (like friction) or any diabatic source of buoyancy can act as a source or sink of potential vorticity.

By understanding this hierarchy of principles—from the continuum assumption to the conservation of potential vorticity—we gain a systematic and powerful framework for interpreting and predicting the complex motions of the Earth's oceans and atmosphere.