## Introduction
Mesoscale ocean eddies, the swirling 'weather' of the sea, are fundamental components of the global ocean circulation, playing a critical role in transporting heat, salt, carbon, and momentum. However, their relatively small scale—tens to hundreds of kilometers—has historically made them a significant challenge for global climate models, which often operate at resolutions too coarse to capture their dynamics. This creates a knowledge gap, as the collective effects of these unresolved eddies are crucial for a realistic simulation of the ocean state. This article provides a graduate-level guide to the theory and practice of ocean eddy-resolving modeling, the primary tool for overcoming this challenge.

The journey begins in the **Principles and Mechanisms** chapter, where we will derive the governing equations and explore the fundamental fluid dynamics of eddy generation, evolution, and decay. Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate how these models are used as powerful diagnostic tools to observe the eddy field, quantify its energetics, and understand its impact on the broader climate system. Finally, the **Hands-On Practices** section will bridge theory and application with practical exercises in calculating key parameters and implementing diagnostic algorithms, solidifying your understanding of this vital field in modern oceanography.

## Principles and Mechanisms

### The Governing Equations of Motion

To model [ocean eddies](@entry_id:1129056), we must begin with the fundamental equations governing fluid motion on a rotating, stratified planet. For the scales relevant to [mesoscale eddies](@entry_id:1127814) (tens to hundreds of kilometers), the full Navier-Stokes equations can be simplified under a set of well-justified approximations, leading to the **Hydrostatic Primitive Equations (HPEs)**. These equations form the dynamical core of most modern [ocean general circulation models](@entry_id:1129060). The key approximations are the **Boussinesq approximation** and the **hydrostatic approximation**.

The Boussinesq approximation simplifies the dynamics by assuming that density variations are small relative to a constant reference density, $\rho_0$. Consequently, density variations are neglected in the inertial terms (those involving acceleration) but are retained where they are multiplied by gravity, as this buoyancy effect is the primary driver of [stratified flows](@entry_id:265379). The [hydrostatic approximation](@entry_id:1126281) assumes that on the large scales of interest, the [vertical pressure gradient](@entry_id:1133794) force is almost perfectly balanced by the force of gravity, meaning vertical accelerations are negligible.

Under these approximations, for a flow described by velocity $\boldsymbol{u}=(u,v,w)$, pressure $p$, and density $\rho$ on a [rotating frame](@entry_id:155637) with Coriolis parameter $f$, the HPEs are as follows :

1.  **Horizontal Momentum Equations:** These govern the evolution of horizontal currents.
    $$ \frac{\partial \boldsymbol{u}_h}{\partial t} + (\boldsymbol{u}\cdot\nabla) \boldsymbol{u}_h + f \hat{\boldsymbol{k}} \times \boldsymbol{u}_h = -\frac{1}{\rho_0}\nabla_h p + \boldsymbol{F}_h $$
    Here, $\boldsymbol{u}_h=(u,v)$ is the horizontal velocity vector, $\hat{\boldsymbol{k}}$ is the local vertical unit vector, $\nabla_h$ is the horizontal gradient operator, and $\boldsymbol{F}_h$ represents frictional forces, typically parameterized as eddy viscosity. The crucial terms for eddy dynamics are the nonlinear **advection** term, $(\boldsymbol{u}\cdot\nabla) \boldsymbol{u}_h$, which is responsible for the complex evolution and interaction of eddies, and the **Coriolis force**, $f \hat{\boldsymbol{k}} \times \boldsymbol{u}_h$, which constrains the flow to a near-rotational balance. The **horizontal pressure gradient**, $-\frac{1}{\rho_0}\nabla_h p$, is the primary driving force for the currents.

2.  **Hydrostatic Balance:** This equation replaces the full vertical momentum equation.
    $$ \frac{\partial p}{\partial z} = -\rho g $$
    This simple balance is a cornerstone of large-scale ocean modeling. It provides a direct link between the fluid's density structure and its pressure field. As we will see, horizontal variations in density (stratification) create horizontal pressure gradients that drive the flow.

3.  **Continuity Equation:** The Boussinesq approximation implies that the flow is effectively incompressible.
    $$ \nabla \cdot \boldsymbol{u} = \frac{\partial u}{\partial x} + \frac{\partial v}{\partial y} + \frac{\partial w}{\partial z} = 0 $$
    In HPE models, this equation serves a critical diagnostic role. Since the horizontal velocities $(u,v)$ are determined by the momentum equations, the continuity equation can be integrated vertically to find the vertical velocity, $w$. Any horizontal convergence of flow ($\nabla_h \cdot \boldsymbol{u}_h  0$) must be balanced by vertical stretching ($\partial w/\partial z > 0$). This links the horizontal and vertical motions and is essential for capturing the upwelling and downwelling associated with eddies.

4.  **Tracer Conservation Equations:** The ocean's density is determined by its temperature and salinity. These are treated as active tracers that are advected by the flow and mixed by smaller-scale processes.
    $$ \frac{\partial \theta}{\partial t} + \boldsymbol{u}\cdot\nabla \theta = \mathcal{D}_\theta + Q_\theta $$
    $$ \frac{\partial S}{\partial t} + \boldsymbol{u}\cdot\nabla S = \mathcal{D}_S + Q_S $$
    Here, $\theta$ is potential temperature, $S$ is salinity, $\mathcal{D}$ represents mixing and diffusion terms, and $Q$ represents sources and sinks (e.g., surface heating/cooling or precipitation/evaporation).

5.  **Equation of State:** This provides the crucial link that closes the system of equations.
    $$ \rho = \rho(\theta, S, p) $$
    The tracer fields determine the density, the density sets the pressure field via hydrostatic balance, and the pressure field drives the currents via the momentum equations. The currents, in turn, advect the tracers. This feedback loop is the heart of [ocean dynamics](@entry_id:1129055) and is what enables the generation of eddies from the potential energy stored in the density field.

### Fundamental Balances and Characteristic Scales

Within the framework of the [primitive equations](@entry_id:1130162), several key balances and [characteristic scales](@entry_id:144643) emerge that govern the behavior of [mesoscale eddies](@entry_id:1127814).

#### Geostrophic Balance

For the slow, large-scale motions typical of [mesoscale eddies](@entry_id:1127814), the Rossby number—the ratio of inertial to Coriolis forces, $Ro = U/(fL)$—is small. In this limit, the acceleration and friction terms in the horizontal momentum equations are small compared to the Coriolis and pressure gradient forces. This leads to the leading-order balance known as **geostrophic balance** :
$$ f \hat{\boldsymbol{k}} \times \boldsymbol{u}_g = -\frac{1}{\rho_0}\nabla_h p $$
where $\boldsymbol{u}_g$ is the geostrophic velocity. This can be solved for the velocity:
$$ \boldsymbol{u}_g = -\frac{1}{\rho_0 f} \hat{\boldsymbol{k}} \times \nabla_h p $$
This equation implies that [geostrophic currents](@entry_id:1125618) flow along lines of constant pressure (isobars).

A powerful application of this balance is its connection to the sea surface height, $\eta$. By integrating the hydrostatic equation from a depth $z$ up to the surface $z=\eta$, we can relate the pressure at depth to the sea surface height. Just below the surface, the horizontal pressure gradient is dominated by the slope of the sea surface: $\nabla_h p \approx g \rho_0 \nabla_h \eta$. Substituting this into the geostrophic velocity equation gives a direct relationship between the surface height gradient and the surface geostrophic velocity:
$$ \boldsymbol{u}_g(\text{surface}) = -\frac{g}{f} \hat{\boldsymbol{k}} \times \nabla_h \eta $$
This relationship is fundamental to [satellite altimetry](@entry_id:1131208), which measures sea surface height and allows us to map the ocean's surface [geostrophic currents](@entry_id:1125618) from space. It is important to remember that a real flow field from an eddy-resolving model contains both the balanced [geostrophic flow](@entry_id:166112) and unbalanced, high-frequency motions (like gravity waves and inertial oscillations). To diagnose the geostrophic component, the model output must be temporally filtered over periods longer than the inertial period ($T \gg f^{-1}$) .

In regions of strong currents and high curvature, such as in the core of a tight eddy, the Rossby number may not be small, and the [centrifugal force](@entry_id:173726) becomes important. This leads to a higher-order balance known as **gradient-wind balance** or cyclogeostrophic balance, which provides a more accurate estimate of the velocity .

#### The Rossby Radius of Deformation

The characteristic horizontal scale of [mesoscale eddies](@entry_id:1127814) is not arbitrary; it is set by a fundamental length scale of rotating, [stratified fluids](@entry_id:181098) known as the **Rossby radius of deformation**. This scale represents the distance over which geostrophic adjustment occurs; it is the length scale at which rotational effects become as important as buoyancy (stratification) effects.

To understand this scale, we can analyze the behavior of long waves in a stratified ocean. The vertical structure of these waves can be described by a set of orthogonal **vertical modes**, $\Phi_n(z)$, which are solutions to a Sturm-Liouville [eigenvalue problem](@entry_id:143898) derived from the linearized [primitive equations](@entry_id:1130162). For an ocean of depth $H$ with a rigid lid and flat bottom (implying vertical velocity $w=0$ at the top and bottom), the equation for the vertical modes is :
$$ \frac{d}{dz}\left(\frac{1}{N^2(z)} \frac{d\Phi_n}{dz}\right) + \frac{1}{c_n^2} \Phi_n = 0 $$
with boundary conditions $\frac{d\Phi_n}{dz} = 0$ at $z=0$ and $z=-H$. Here, $N(z)$ is the **Brunt-Väisälä frequency** (or [buoyancy frequency](@entry_id:1121933)), defined by $N^2 = -\frac{g}{\rho_0} \frac{d\bar{\rho}}{dz}$, which measures the strength of the stratification. The eigenvalues of this problem, $c_n$, are the phase speeds of long internal gravity waves for each vertical mode $n=1, 2, ...$.

The $n=0$ mode is the **[barotropic mode](@entry_id:1121351)**, which is depth-independent and has a very fast wave speed $c_0 = \sqrt{gH}$. The modes $n \ge 1$ are the **[baroclinic modes](@entry_id:1121346)**, which have vertical structure. For the first [baroclinic mode](@entry_id:1121345) ($n=1$), which typically contains most of the eddy energy, the [wave speed](@entry_id:186208) $c_1$ depends on the stratification profile. For the simplified case of constant stratification $N(z) \equiv N_0$, the solution yields $c_1 = \frac{N_0 H}{\pi}$. This shows that stronger stratification (larger $N_0$) and greater depth ($H$) lead to faster [internal waves](@entry_id:261048).

The first baroclinic Rossby radius of deformation, $R_1$, is then defined as:
$$ R_1 = \frac{c_1}{f} $$
Substituting the constant-stratification result, $R_1 = \frac{N_0 H}{\pi f}$. This scale is crucial: it is the natural length scale for [baroclinic instability](@entry_id:200061), the primary mechanism that generates eddies. Thus, [mesoscale eddies](@entry_id:1127814) have a characteristic size on the order of $R_1$. In the mid-latitude ocean, $R_1$ is typically between 10 and 50 km.

### Eddy Generation and Energetics

Mesoscale eddies are not random fluctuations; they are coherent structures that draw energy from the large-scale ocean circulation through fluid dynamical instabilities. The two primary mechanisms are baroclinic and [barotropic instability](@entry_id:264411).

#### Baroclinic and Barotropic Instability

**Baroclinic instability** is the dominant source of eddy energy in the mid-latitude oceans. It is a process that releases the **Mean Available Potential Energy (MAPE)** stored in the large-scale horizontal density gradients of the ocean. Through the **[thermal wind balance](@entry_id:192157)** ($f \frac{\partial \overline{U}}{\partial z} = -\frac{\partial \overline{b}}{\partial y}$, where $b$ is buoyancy), these horizontal density gradients are associated with a [vertical shear](@entry_id:1133795) of the mean geostrophic flow, $\partial \overline{U}/\partial z$. Baroclinic instability taps into this potential energy source. The [energy conversion](@entry_id:138574) pathway is from MAPE to **Eddy Potential Energy (EPE)**, and then to **Eddy Kinetic Energy (EKE)**. This conversion is characterized by a downgradient eddy flux of buoyancy (flattening the mean density surfaces) and a positive correlation between vertical velocity and buoyancy fluctuations, $\overline{w'b'} > 0$. This positive flux signifies that, on average, less dense water rises and denser water sinks, releasing potential energy and converting it into the kinetic energy of the growing eddies .

**Barotropic instability**, in contrast, is a process that extracts energy directly from the **Mean Kinetic Energy (MKE)** of the large-scale flow. It is associated with the horizontal shear of the mean flow, $\partial \overline{U}/\partial y$. The [energy conversion](@entry_id:138574) from MKE to EKE occurs through the work done by eddy momentum fluxes (also known as **Reynolds stresses**) against the mean shear. This conversion term is given by $-\overline{u'v'} \frac{\partial \overline{U}}{\partial y}$. For instability to occur, this term must be positive, meaning the [eddy momentum flux](@entry_id:1124142) systematically extracts energy from the mean flow's shear. A necessary condition for [barotropic instability](@entry_id:264411) of a zonal jet on a [beta-plane](@entry_id:1121523) (the **Rayleigh-Kuo criterion**) is that the meridional gradient of the mean potential vorticity must change sign somewhere in the flow .

#### Eddy-Mean Flow Interaction and Reynolds Stresses

The interaction between eddies and the mean flow can be formalized using **Reynolds decomposition**, where the velocity field is split into a time- or zonal-mean component ($\overline{\boldsymbol{u}}$) and a fluctuating eddy component ($\boldsymbol{u}'$). When this decomposition is applied to the momentum equations, terms representing the effects of the eddies on the mean flow emerge.

Specifically, for a zonal-mean flow $\overline{u}(y)$, the mean zonal momentum equation becomes :
$$ \frac{\partial \overline{u}}{\partial t} = -\frac{\partial}{\partial y}(\overline{u'v'}) + \text{other terms (forcing, friction, etc.)} $$
The term $-\frac{\partial}{\partial y}(\overline{u'v'})$ is the **convergence of the [eddy momentum flux](@entry_id:1124142)**. It represents the net acceleration or deceleration of the mean flow by the eddies. Where this term is positive, the eddies accelerate the mean flow; where it is negative, they decelerate it.

A remarkable feature of [geostrophic turbulence](@entry_id:1125619) is that eddies can systematically transport momentum *up* the mean [velocity gradient](@entry_id:261686), acting as a "negative viscosity." For a typical eastward jet, eddies generated on its flanks transport eastward momentum from the flanks into the jet core. This results in a positive convergence ($-\partial_y \overline{u'v'} > 0$) at the jet axis, strengthening the jet, and a divergence on the flanks, decelerating them. This up-gradient [momentum transport](@entry_id:139628) is a key mechanism by which eddies sharpen and maintain strong ocean currents like the Gulf Stream or the Antarctic Circumpolar Current against frictional dissipation .

### Eddy Propagation and Evolution in Geostrophic Turbulence

Once formed, the evolution and propagation of eddies are governed by fundamental principles of rotating, [stratified fluids](@entry_id:181098), including [potential vorticity conservation](@entry_id:270380) and wave dynamics.

#### The Beta-Effect and Rossby Waves

The Earth's [sphericity](@entry_id:913074) causes the Coriolis parameter $f$ to vary with latitude. In a simplified model on a [tangent plane](@entry_id:136914) (a **[beta-plane](@entry_id:1121523)**), this variation is approximated as linear: $f = f_0 + \beta y$, where $y$ is the meridional coordinate and $\beta = df/dy$ is the constant planetary vorticity gradient. This seemingly small variation has profound consequences.

The $\beta$-effect provides a restoring mechanism for meridional displacements, giving rise to large-scale [planetary waves](@entry_id:195650) known as **Rossby waves**. The dispersion relation for baroclinic Rossby waves, derived from the linearized Quasi-Geostrophic (QG) potential vorticity equation, is :
$$ \omega = -\frac{\beta k}{k^2 + l^2 + 1/R_d^2} $$
where $\omega$ is the frequency, $(k,l)$ are the zonal and meridional wavenumbers, and $R_d$ is the Rossby deformation radius. A key feature of this relation is that the zonal phase speed, $c_p = \omega/k$, is always negative (westward).

Mesoscale eddies, while nonlinear, are strongly influenced by this underlying wave dynamic. Their propagation is often described as a "beta-drift"—an intrinsic tendency to propagate westward. In the long-wave limit (wavelengths much larger than $R_d$), the zonal [group velocity](@entry_id:147686) (the speed of [energy propagation](@entry_id:202589)) is also westward, with a magnitude of $\beta R_d^2$. This westward propagation is a robust feature seen in both observations and eddy-resolving models .

#### Potential Vorticity Conservation

A more general and powerful principle for understanding rotating, [stratified flows](@entry_id:265379) is the conservation of **Potential Vorticity (PV)**. For an inviscid, adiabatic fluid, a specific scalar quantity combining vorticity and stratification is materially conserved, meaning it is carried along with fluid parcels. The most general form is **Ertel's Potential Vorticity**, defined as :
$$ q = (\boldsymbol{\omega} + f\hat{\boldsymbol{k}}) \cdot \nabla b $$
where $\boldsymbol{\omega} = \nabla \times \boldsymbol{u}$ is the relative vorticity and $b$ is the buoyancy. Under the conditions of inviscid, adiabatic, and [incompressible flow](@entry_id:140301), its material derivative is zero:
$$ \frac{Dq}{Dt} = \frac{\partial q}{\partial t} + \boldsymbol{u} \cdot \nabla q = 0 $$
The conservation of PV acts as a powerful dynamical constraint, often referred to as a "dynamical tracer." It governs the evolution of vortices, the generation of waves, and the process of geostrophic adjustment. In eddy-resolving models, non-conservation of PV arises from explicit frictional and diabatic (mixing) terms, as well as from numerical [truncation errors](@entry_id:1133459).

#### The Dual Cascade of Geostrophic Turbulence

The behavior of a field of interacting eddies can be understood through the theory of **[geostrophic turbulence](@entry_id:1125619)**. A key finding of this theory is the **[dual cascade](@entry_id:183385)** phenomenon. Unlike three-dimensional turbulence where energy cascades from large scales to small scales (a forward cascade), two-dimensional and quasi-[geostrophic turbulence](@entry_id:1125619) have two conserved quantities in the inviscid limit: energy and (potential) enstrophy (mean squared vorticity) .

The dual conservation law forces the [turbulent cascade](@entry_id:1133502) to split. When energy is injected at an intermediate scale (e.g., the Rossby radius $R_1$), the **energy** cascades preferentially to larger scales (an **inverse energy cascade**), while the **potential enstrophy** cascades to smaller scales (a **forward [enstrophy cascade](@entry_id:1124542)**). The [inverse energy cascade](@entry_id:266118) is responsible for the self-organization of turbulent eddies into larger, coherent structures, including strong zonal jets. The forward [enstrophy cascade](@entry_id:1124542) carries variance to very small scales, where it must ultimately be dissipated by friction.

The [energy spectrum](@entry_id:181780) $E(k)$ reflects this duality. In the inverse energy cascade range, the spectrum typically follows a $k^{-5/3}$ slope. In the forward [enstrophy cascade](@entry_id:1124542) range, it follows a steeper $k^{-3}$ slope.

This idealized picture is modified by stratification and the $\beta$-effect:
-   **Stratification ($R_d$):** The deformation radius $R_d$ marks the transition scale. For scales much smaller than $R_d$, the dynamics are akin to 2D turbulence, exhibiting the $k^{-3}$ [enstrophy cascade](@entry_id:1124542). For scales larger than $R_d$, the inverse energy cascade operates, building larger structures .
-   **Beta-effect ($\beta$):** The [inverse energy cascade](@entry_id:266118) does not proceed to infinitely large scales. When eddies grow to a size where their turnover time becomes comparable to the period of a Rossby wave, the turbulent motions become wave-like. This arrests the upscale cascade at a characteristic scale known as the **Rhines scale**, $L_R \sim (U/\beta)^{1/2}$. This arrest is anisotropic, primarily halting the meridional growth of eddies, and is a key mechanism for the formation of zonally-oriented jets .

### Numerical Considerations in Eddy-Resolving Models

Translating these physical principles into a working numerical model requires careful consideration of grid resolution, time-stepping, and the parameterization of unresolved processes.

#### Grid Resolution

To be "eddy-resolving," a model's horizontal grid spacing, $\Delta x$, must be fine enough to represent the structure of [mesoscale eddies](@entry_id:1127814). Since the characteristic scale of these eddies is the first baroclinic Rossby radius, $R_1$, the grid spacing must be a fraction of this scale. A common rule of thumb is to require at least four grid points across the deformation radius, leading to the criterion :
$$ \Delta x \lesssim \frac{R_1}{4} $$
Resolutions coarser than this will lead to severe [numerical dispersion and dissipation](@entry_id:752783), preventing the model from accurately simulating eddy generation and dynamics. Since $R_1 = c_1/f$, the required grid spacing becomes smaller at higher latitudes (where $f$ is larger) and in regions of weaker stratification (where $c_1$ is smaller).

#### Time-Stepping and the CFL Condition

Numerical stability of [explicit time-stepping](@entry_id:168157) schemes is governed by the **Courant-Friedrichs-Lewy (CFL) condition**. This condition states that the [numerical domain of dependence](@entry_id:163312) must contain the physical domain of dependence, which means that information cannot travel more than one grid cell in a single time step, $\Delta t$. The condition is generally expressed as $C = \frac{v_{prop} \Delta t}{\Delta x} \le 1$, where $v_{prop}$ is the speed of the fastest-propagating signal in the system.

In an ocean model, two key processes impose CFL limits:
1.  **Advection:** The advective CFL limit is set by the fluid velocity itself, $\Delta t_{adv} \le \Delta x / |u|_{max}$. For a typical eddy velocity of $1$ m/s and $\Delta x = 1$ km, this gives a limit of $\Delta t_{adv} \le 1000$ s.
2.  **Gravity Waves:** The fastest waves in a hydrostatic model are the external (barotropic) gravity waves, with speed $c = \sqrt{gH}$. For a typical ocean depth of $H=4000$ m, this speed is $c \approx 200$ m/s. The corresponding CFL limit is $\Delta t_{grav} \le \Delta x / c$. With $\Delta x = 1$ km, this yields a much stricter limit of $\Delta t_{grav} \le 5$ s .

Clearly, the barotropic gravity waves impose the most severe constraint on the time step for an explicit model. This computational bottleneck is why many ocean models employ **split-explicit** schemes (where fast waves and slow advection are treated with different time steps) or **implicit** schemes for the terms governing fast waves.

#### Subgrid-Scale Dissipation

In any numerical model with a finite grid, there must be a mechanism to remove energy and variance that cascades to the smallest resolved scales. In [geostrophic turbulence](@entry_id:1125619), the forward [enstrophy cascade](@entry_id:1124542) continuously moves variance towards the grid scale ($\sim \Delta x$), where it would otherwise accumulate and cause numerical instability. This physical process is represented by explicit **lateral viscosity** and **diffusivity** terms added to the momentum and tracer equations.

Two common forms of dissipation are:
-   **Laplacian dissipation:** This adds a term of the form $+\nu_h \nabla^2 \boldsymbol{u}$ to the momentum equation. It has a spectral damping rate proportional to $\nu_h k^2$.
-   **Biharmonic dissipation ([hyperviscosity](@entry_id:1126308)):** This adds a term of the form $-A_4 \nabla^4 \boldsymbol{u}$, with a spectral damping rate proportional to $A_4 k^4$.

The biharmonic form is more **scale-selective**. Because its damping rate increases with the fourth power of the wavenumber ($k^4$), it is highly effective at damping noise at the grid scale while having a much smaller impact on the larger, physically-resolved scales of the eddies. Laplacian ($k^2$) dissipation is less selective and can excessively damp the eddies themselves.

The coefficients ($\nu_h$, $A_4$) are chosen to ensure that dissipation acts primarily at the grid scale. A common method is to set a grid-scale Reynolds number to be of order one. For Laplacian viscosity, this implies $\nu_h \sim U \Delta$; for [biharmonic viscosity](@entry_id:1121563), it implies $A_4 \sim U \Delta^3$ .

#### Computational Cost

The combination of fine horizontal resolution and short time steps makes eddy-resolving ocean modeling computationally intensive. The total cost is proportional to the number of grid points divided by the time step. We can estimate the scaling of cost with latitude. The required grid spacing scales as $\Delta x \propto R_1 = c/f$, so the number of horizontal grid points for a fixed area scales as $1/\Delta x^2 \propto f^2/c^2$. The time step, when constrained by the eddy-resolving criterion and internal wave CFL, scales as $\Delta t \propto \Delta x/c \propto 1/f$. Therefore, the total computational cost scales as :
$$ \text{Cost} \propto \frac{1}{\Delta x^2} \frac{1}{\Delta t} \propto \left(\frac{f^2}{c^2}\right) \left(f\right) = \frac{f^3}{c^2} $$
This strong dependence on the Coriolis parameter ($f^3$) means that high-latitude ocean modeling is substantially more expensive than mid-latitude modeling, as eddies become smaller and time steps must be shorter. For example, moving from a mid-latitude region to a high-latitude region can increase the computational cost per simulated day by a factor of nearly 7 .