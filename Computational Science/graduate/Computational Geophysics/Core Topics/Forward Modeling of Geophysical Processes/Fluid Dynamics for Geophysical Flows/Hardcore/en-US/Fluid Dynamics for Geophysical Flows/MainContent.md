## Introduction
Geophysical fluid dynamics (GFD) is the cornerstone for understanding the motion of atmospheres, oceans, and even the molten and solid interiors of planets. These natural flows are distinguished from classical fluid mechanics by the profound influence of planetary rotation and density stratification. To accurately model and predict phenomena ranging from weather patterns and ocean currents to the tectonic engine driving our planet, we must develop a specialized theoretical framework that incorporates these large-scale effects. This article bridges the gap between fundamental physics and complex [planetary dynamics](@entry_id:753475), providing a systematic guide to the principles that govern geophysical flows.

Over the course of this article, you will build a comprehensive understanding of GFD. The first chapter, **"Principles and Mechanisms,"** lays the mathematical groundwork, deriving the governing equations of motion from first principles and introducing the critical effects of rotation and stratification that define the discipline. Following this, the **"Applications and Interdisciplinary Connections"** chapter demonstrates how these theories are applied to explain real-world phenomena across the Earth sciences, from the dynamics of the Gulf Stream to the slow creep of [mantle convection](@entry_id:203493). Finally, the **"Hands-On Practices"** section presents concrete problems that challenge you to apply and test these concepts, solidifying your theoretical knowledge through practical application.

## Principles and Mechanisms

This chapter delineates the fundamental principles and mechanisms that govern geophysical fluid flows. We will begin by establishing the mathematical language used to describe fluid motion, focusing on the derivation of general conservation laws. We will then formulate the specific laws of mass and momentum conservation, introducing the concepts of stress and viscosity. Subsequently, we will incorporate the defining features of geophysical flows—planetary rotation and density stratification—and explore their profound consequences. Finally, we will introduce the major approximations and reduced dynamical systems, such as the Boussinesq, shallow-water, and quasi-geostrophic models, that form the bedrock of theoretical and [computational geophysics](@entry_id:747618). Throughout this chapter, we will use nondimensional parameters to classify [flow regimes](@entry_id:152820) and understand the balance of forces at play.

### The Kinematics of Fluid Motion: From Parcels to Fields

To describe the motion of a fluid, one can adopt two distinct perspectives. The **Lagrangian description** follows individual fluid parcels, tracking their properties (e.g., position, velocity, temperature) as functions of time. In contrast, the **Eulerian description** observes the fluid from fixed points in space, describing how [fluid properties](@entry_id:200256) at these points change over time. Geophysical fluid dynamics predominantly employs the Eulerian framework, as we are typically interested in the state of the atmosphere or ocean at specific locations rather than tracking innumerable individual parcels.

The crucial link between these two descriptions is the **[material derivative](@entry_id:266939)**, denoted as $\frac{\mathrm{D}}{\mathrm{D}t}$. It represents the total rate of change of a property for a fluid parcel as it moves through a flow field. Consider a scalar property, such as temperature, represented by the Eulerian field $\phi(\boldsymbol{x}, t)$. A fluid parcel's position is given by the trajectory $\boldsymbol{x}(t)$. The rate of change of $\phi$ for this parcel is found by applying the [multivariable chain rule](@entry_id:146671):

$$
\frac{\mathrm{D}\phi}{\mathrm{D}t} \equiv \frac{\mathrm{d}}{\mathrm{d}t} \phi(\boldsymbol{x}(t), t) = \frac{\partial \phi}{\partial t} + \frac{\partial \phi}{\partial x_i} \frac{\mathrm{d}x_i}{\mathrm{d}t}
$$

Recognizing that $\frac{\mathrm{d}\boldsymbol{x}}{\mathrm{d}t}$ is the [fluid velocity](@entry_id:267320) $\boldsymbol{u}(\boldsymbol{x}, t)$, we can write this in vector notation:

$$
\frac{\mathrm{D}\phi}{\mathrm{D}t} = \frac{\partial \phi}{\partial t} + \boldsymbol{u} \cdot \nabla\phi
$$

This fundamental expression shows that the total rate of change experienced by a parcel (the [material derivative](@entry_id:266939)) is the sum of the local rate of change at a fixed point ($\frac{\partial \phi}{\partial t}$) and the **advective rate of change** ($\boldsymbol{u} \cdot \nabla\phi$), which arises from the parcel moving to a new location with a different value of $\phi$.

The same principle applies to a vector field, such as the velocity $\boldsymbol{u}$ itself. Applying the derivative to each component of the vector in a fixed Cartesian basis yields the material derivative of the vector field :

$$
\frac{\mathrm{D}\boldsymbol{u}}{\mathrm{D}t} = \frac{\partial \boldsymbol{u}}{\partial t} + (\boldsymbol{u} \cdot \nabla)\boldsymbol{u}
$$

The term $(\boldsymbol{u} \cdot \nabla)\boldsymbol{u}$ is the nonlinear **advection of momentum**, a source of much of the complexity in fluid dynamics.

### From Integral Statements to Differential Equations: The Reynolds Transport Theorem

The fundamental laws of physics (conservation of mass, momentum, and energy) are often first expressed for a distinct body of matter—in our case, a fluid volume composed of the same set of fluid parcels for all time, known as a **material control volume** $\Omega(t)$. To transform these [integral conservation laws](@entry_id:202878) into local, pointwise differential equations that are more amenable to analysis, we employ the **Reynolds Transport Theorem (RTT)**.

The RTT relates the time derivative of an integral over a material volume to an integral over a fixed volume. For a generic intensive property $\psi$ whose density is $\rho\psi$, the total amount in a material volume is $\int_{\Omega(t)} \rho\psi \, \mathrm{d}V$. The RTT states:

$$
\frac{\mathrm{d}}{\mathrm{d}t} \int_{\Omega(t)} \rho\psi \, \mathrm{d}V = \int_{\Omega(t)} \left( \frac{\partial (\rho\psi)}{\partial t} + \nabla \cdot (\rho\psi \boldsymbol{u}) \right) \, \mathrm{d}V
$$

The integrand on the right-hand side represents the local rate of change of the property's density plus the net flux out of an infinitesimal volume. If a quantity is conserved within the volume (i.e., its total material rate of change is zero), the left-hand side vanishes. Because this must hold for any arbitrary material volume $\Omega(t)$, the integrand itself must be zero everywhere, assuming it is continuous. This **localization principle** gives the general [differential form](@entry_id:174025) of a conservation law:

$$
\frac{\partial (\rho\psi)}{\partial t} + \nabla \cdot (\rho\psi \boldsymbol{u}) = 0
$$

This equation states that the local increase in the density of a property must be balanced by a [net convergence](@entry_id:150788) of its flux. Using the product rule and the continuity equation (derived below), this can be re-expressed in terms of the material derivative, providing a powerful link between conservation principles and the kinematics of fluid parcels .

### The Governing Equations of Motion

#### Conservation of Mass and the Incompressibility Condition

Applying the RTT to mass itself (where the property per unit mass, $\psi$, is simply 1), the conservation of mass for a material volume, $\frac{\mathrm{d}}{\mathrm{d}t} \int_{\Omega(t)} \rho \, \mathrm{d}V = 0$, immediately yields the **[continuity equation](@entry_id:145242)**:

$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \boldsymbol{u}) = 0
$$

This can be expanded using the material derivative to give $\frac{\mathrm{D}\rho}{\mathrm{D}t} + \rho(\nabla \cdot \boldsymbol{u}) = 0$. This form reveals that the divergence of the velocity field, $\nabla \cdot \boldsymbol{u}$, represents the fractional rate of change of volume of a fluid parcel.

For many geophysical flows, particularly in the ocean, density variations are small. A powerful simplification is to treat the fluid as **incompressible**, which means the density of a fluid parcel does not change as it moves, $\frac{\mathrm{D}\rho}{\mathrm{D}t} = 0$. This immediately implies that the flow must be **[divergence-free](@entry_id:190991)**:

$$
\nabla \cdot \boldsymbol{u} = 0
$$

This condition means that the volume of any fluid parcel is conserved. It is a mathematical constraint that filters out sound waves, which involve compression and rarefaction. In a hypothetical flow field such as $\mathbf{v}(x, y, z) = (C_x x) \mathbf{i} + (\beta y) \mathbf{j} + (C_z z) \mathbf{k}$, the condition $\nabla \cdot \mathbf{v} = C_x + \beta + C_z = 0$ must be satisfied for the flow to be incompressible, constraining the model's parameters .

#### Conservation of Momentum and the Stress Tensor

Newton's second law, when applied to a fluid, becomes the Cauchy [momentum equation](@entry_id:197225). The [material acceleration](@entry_id:270992) of a fluid parcel is driven by the net force acting upon it. These forces are categorized as **[body forces](@entry_id:174230)** (acting on the volume, like gravity) and **[surface forces](@entry_id:188034)** (acting on the parcel's boundary, like pressure and friction).

The [surface forces](@entry_id:188034) are described by the **Cauchy stress tensor**, $\boldsymbol{\sigma}$. The force per unit area on a surface with normal $\boldsymbol{n}$ is given by $\boldsymbol{\sigma} \cdot \boldsymbol{n}$. For a fluid at rest, the stress is isotropic and directed inward, given by $\boldsymbol{\sigma} = -p\boldsymbol{I}$, where $p$ is the thermodynamic pressure and $\boldsymbol{I}$ is the identity tensor. For a moving fluid, additional stresses arise from viscous effects due to velocity gradients. The stress tensor is generally decomposed into its isotropic and deviatoric (traceless) parts. The isotropic part is associated with pressure, while the **[deviatoric stress tensor](@entry_id:267642)**, $\boldsymbol{\tau}$, represents the stresses that cause the fluid to deform .

$$
\boldsymbol{\sigma} = -p_{m}\boldsymbol{I} + \boldsymbol{\tau}
$$

Here, $p_m = -\frac{1}{3}\text{tr}(\boldsymbol{\sigma})$ is the mechanical pressure. For a **Newtonian fluid**, the deviatoric stress is linearly proportional to the fluid's rate of deformation. This relationship is the fluid analog of Hooke's law for solids. The rate of deformation is described by the **[rate-of-strain tensor](@entry_id:260652)**, $\boldsymbol{S}$, which is the symmetric part of the [velocity gradient tensor](@entry_id:270928), $\boldsymbol{S} = \frac{1}{2}(\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^T)$. The anti-symmetric part of $\nabla\boldsymbol{u}$ represents local [rigid-body rotation](@entry_id:268623), which, for an isotropic fluid, does not generate stress. The [constitutive relation](@entry_id:268485) for a compressible, isotropic Newtonian fluid is:

$$
\boldsymbol{\tau} = 2\mu \boldsymbol{S} + \lambda (\nabla \cdot \boldsymbol{u}) \boldsymbol{I}
$$

Here, $\mu$ is the **dynamic viscosity** (or [shear viscosity](@entry_id:141046)), which measures resistance to shearing motions, and $\lambda$ is the **second coefficient of viscosity**, related to resistance to [volumetric expansion](@entry_id:144241) or contraction. The full **Navier-Stokes equations** for [momentum conservation](@entry_id:149964) are then:

$$
\rho \frac{\mathrm{D}\boldsymbol{u}}{\mathrm{D}t} = -\nabla p + \nabla \cdot \boldsymbol{\tau} + \rho\boldsymbol{g} = -\nabla p + \mu \nabla^2 \boldsymbol{u} + (\lambda+\mu)\nabla(\nabla \cdot \boldsymbol{u}) + \rho\boldsymbol{g}
$$

where we have combined the thermodynamic pressure and the dilatational stress into a single pressure term $p$. For an [incompressible flow](@entry_id:140301) where $\nabla \cdot \boldsymbol{u} = 0$, the viscous term simplifies significantly to $\mu \nabla^2 \boldsymbol{u}$.

### The Heart of GFD: Rotation and Stratification

Geophysical fluids are fundamentally distinguished by two features: they exist on a rotating planet, and they are stably stratified by density.

#### The Effect of a Rotating Frame

Observing motion in a frame rotating with [angular velocity](@entry_id:192539) $\boldsymbol{\Omega}$ (e.g., the Earth), two apparent accelerations emerge in the momentum equation. These are not true forces but inertial effects arising from the non-inertial nature of the reference frame .

1.  **Coriolis Acceleration**: $-2\boldsymbol{\Omega} \times \boldsymbol{u}$. This acceleration acts perpendicular to both the rotation axis and the velocity vector. It deflects moving objects to the right in the Northern Hemisphere ($\boldsymbol{\Omega}$ points "up") and to the left in the Southern Hemisphere. It is a dominant effect for large-scale, slow flows.

2.  **Centrifugal Acceleration**: $-\boldsymbol{\Omega} \times (\boldsymbol{\Omega} \times \boldsymbol{r})$. This acceleration is directed radially outward from the axis of rotation.

The centrifugal acceleration is a **[conservative field](@entry_id:271398)**, meaning it can be written as the gradient of a scalar potential, $\boldsymbol{a}_{\mathrm{cf}} = -\nabla \Phi_{\mathrm{cf}}$, where $\Phi_{\mathrm{cf}} = -\frac{1}{2}|\boldsymbol{\Omega} \times \boldsymbol{r}|^2$. This potential depends on the square of the perpendicular distance from the rotation axis. Because both gravity ($\boldsymbol{g} = -\nabla \Phi_g$) and the centrifugal force are conservative, they are almost always combined into a single **[effective gravity](@entry_id:188792)**, $\boldsymbol{g}_{\mathrm{eff}} = -\nabla\Phi_g^{\star}$, where $\Phi_g^{\star} = \Phi_g + \Phi_{\mathrm{cf}}$ is the **geopotential**. The geopotential defines surfaces of constant effective gravitational potential, and "level" surfaces on Earth are geopotential surfaces, not perfect spheres.

In contrast, the Coriolis acceleration is generally non-conservative and cannot be written as the gradient of a potential. It acts as a source of [vorticity](@entry_id:142747) and is responsible for a vast array of geophysical phenomena.

#### The Effect of Stratification and Buoyancy

Most geophysical fluids are **stably stratified**, meaning density generally decreases with height. This stratification provides a powerful restoring mechanism for vertical motion. Consider a fluid parcel at rest in a background density field $\bar{\rho}(z)$. If the parcel is displaced vertically by a small distance $\zeta$ without mixing with its surroundings, it retains its original density. The ambient density at its new location is $\bar{\rho}(z+\zeta)$. The density anomaly of the parcel relative to its new surroundings is $\rho' \approx -\zeta \frac{\mathrm{d}\bar{\rho}}{\mathrm{d}z}$.

This density difference results in a **[buoyancy force](@entry_id:154088)**. If the background is stably stratified ($\frac{\mathrm{d}\bar{\rho}}{\mathrm{d}z}  0$), a parcel displaced upward ($\zeta > 0$) becomes denser than its surroundings ($\rho' > 0$ if density decreases with height) and is forced back down. Conversely, a parcel displaced downward becomes lighter and is forced back up. The vertical acceleration of the parcel is given by the [buoyancy force](@entry_id:154088) per unit mass, $a_z = -\frac{\rho'g}{\rho_0}$, where $\rho_0$ is a reference density. This leads to the equation for [simple harmonic motion](@entry_id:148744) :

$$
\frac{\mathrm{d}^2\zeta}{\mathrm{d}t^2} = - \left( -\frac{g}{\rho_0}\frac{\mathrm{d}\bar{\rho}}{\mathrm{d}z} \right) \zeta = -N^2 \zeta
$$

The quantity $N$ is the **[buoyancy](@entry_id:138985) frequency** (or Brunt–Väisälä frequency), defined as:

$$
N^2 = -\frac{g}{\rho_0}\frac{\mathrm{d}\bar{\rho}}{\mathrm{d}z}
$$

For a stably [stratified fluid](@entry_id:201059), $\frac{\mathrm{d}\bar{\rho}}{\mathrm{d}z}  0$, so $N^2 > 0$, and the parcel oscillates vertically with frequency $N$. The [buoyancy](@entry_id:138985) frequency is thus a direct measure of the "stiffness" of the stratification. If the fluid is unstably stratified ($\frac{\mathrm{d}\bar{\rho}}{\mathrm{d}z} > 0$), then $N^2  0$, and small vertical displacements grow exponentially, leading to convection . The highest frequency of [internal waves](@entry_id:261048) supported by a [stratified fluid](@entry_id:201059) is limited by $N$, which has profound implications for numerical modeling: [explicit time-stepping](@entry_id:168157) schemes must use a time step $\Delta t \lesssim C/N$ to remain stable .

### Key Dynamical Approximations in GFD

The full Navier-Stokes equations in a rotating, stratified framework are exceedingly complex. GFD makes progress by deriving simplified, or reduced, sets of equations that are valid in specific dynamical regimes.

#### The Boussinesq Approximation

For many oceanic and atmospheric flows, density variations are small relative to a reference density ($\rho = \rho_0 + \rho'$, with $|\rho'|/\rho_0 \ll 1$). The **Boussinesq approximation** leverages this fact by systematically simplifying the equations of motion . The core assumptions are:
1.  Density variations are neglected in all terms *except* where they are multiplied by gravity. This means $\rho$ is replaced by the constant $\rho_0$ in the inertial term ($\rho \frac{\mathrm{D}\boldsymbol{u}}{\mathrm{D}t} \to \rho_0 \frac{\mathrm{D}\boldsymbol{u}}{\mathrm{D}t}$).
2.  The effect of the density perturbation $\rho'$ is retained only in the gravitational term, where it appears as the **[buoyancy force](@entry_id:154088)**, $\rho'\boldsymbol{g}$.
3.  The flow is treated as kinematically incompressible, $\nabla \cdot \boldsymbol{u} = 0$, filtering out acoustic waves.

This leads to the Boussinesq system of equations :
$$
\rho_0\frac{\mathrm{D}\boldsymbol{u}}{\mathrm{D}t} = -\nabla p' + \rho_0 b \hat{\boldsymbol{z}} + \mu \nabla^2 \boldsymbol{u}
$$
$$
\nabla\cdot \boldsymbol{u} = 0
$$

Here, $p'$ is the **[dynamic pressure](@entry_id:262240)** (the deviation from the [hydrostatic pressure](@entry_id:141627) of the reference state), and $b$ is the **[buoyancy](@entry_id:138985)**, defined as $b = -g\rho'/\rho_0$. This system must be closed with an additional equation for the evolution of buoyancy (e.g., an [advection-diffusion equation](@entry_id:144002) for temperature or salinity).

The validity of the Boussinesq approximation hinges on three scaling conditions :
-   Small density variations: $|\rho'|/\rho_0 \ll 1$.
-   Low Mach number: $\mathrm{Ma} = U/c_s \ll 1$, where $U$ is a characteristic flow speed and $c_s$ is the sound speed. This justifies filtering acoustic waves.
-   Shallow vertical motions: The characteristic vertical scale of motion $H$ must be much smaller than the density [scale height](@entry_id:263754), $H \ll H_\rho$.

These conditions are excellently met in the deep ocean. In the atmosphere, they hold for shallow phenomena (e.g., boundary layer convection) but break down for deep motions spanning the troposphere, where the background density changes by a large fraction .

#### The Shallow-Water Equations

When a fluid's horizontal scale is much larger than its vertical scale, and the fluid is vertically well-mixed (homogeneous), its dynamics can be described by the **[shallow-water equations](@entry_id:754726)**. This model is derived from the 3D equations by assuming **[hydrostatic balance](@entry_id:263368)** in the vertical and that the horizontal velocity is independent of depth (**columnar motion**) . The resulting system describes the evolution of the fluid depth, $h(x,y,t)$, and the depth-averaged horizontal velocity, $\boldsymbol{u}(x,y,t)$:

$$
\frac{\partial h}{\partial t}+\nabla\cdot\left(h\boldsymbol{u}\right)=0
$$
$$
\frac{\partial \boldsymbol{u}}{\partial t}+\left(\boldsymbol{u}\cdot\nabla\right)\boldsymbol{u}+f\hat{\boldsymbol{k}}\times\boldsymbol{u}=-g\nabla\eta
$$

Here, $\eta = h+b$ is the free surface elevation, and $b$ is the bottom topography. This system has three key inviscid conservation laws:
1.  **Mass**: Total mass $\int \rho h \, \mathrm{d}A$ is conserved.
2.  **Potential Vorticity (PV)**: The quantity $q = (\zeta+f)/h$, where $\zeta = \hat{\boldsymbol{k}}\cdot\nabla\times\boldsymbol{u}$ is the relative [vorticity](@entry_id:142747), is materially conserved: $\frac{\mathrm{D}q}{\mathrm{D}t} = 0$. This is perhaps the most important dynamical invariant in GFD, linking changes in [vorticity](@entry_id:142747) to changes in fluid depth and planetary latitude.
3.  **Energy**: The total energy, comprising kinetic and potential energy, $\mathcal{H}=\int \left(\tfrac{1}{2}\rho h|\boldsymbol{u}|^2+\rho g(\tfrac{1}{2}h^2+bh)\right)\mathrm{d}A$, is conserved.

#### The Quasi-Geostrophic (QG) Equations

For large-scale, slow flows, the Coriolis force and the [pressure gradient force](@entry_id:262279) are nearly in balance. This state is called **[geostrophic balance](@entry_id:161927)**. The **Quasi-Geostrophic (QG)** approximation describes flows that are a small departure from this balance. The key scaling assumption is a small **Rossby number**, $\mathrm{Ro} = U/(f_0 L) \ll 1$, which measures the ratio of inertia to Coriolis forces .

Under this scaling, the leading-order velocity is geostrophic and nondivergent, and can be described by a **streamfunction** $\psi$ such that $\boldsymbol{u}_g = (-\partial_y\psi, \partial_x\psi)$. The dynamics of the system reduce to a single elegant equation for the evolution of **QG [potential vorticity](@entry_id:276663)**, which is advected by the [geostrophic flow](@entry_id:166112). For a barotropic (depth-independent) flow on a **beta-plane** (where the Coriolis parameter is approximated as a linear function of latitude, $f = f_0 + \beta y$), the QG [potential vorticity](@entry_id:276663) is :

$$
q = \nabla^2\psi + \beta y
$$

The term $\nabla^2\psi$ is the geostrophic relative [vorticity](@entry_id:142747), and $\beta y$ represents the [planetary vorticity](@entry_id:265327) gradient. The QG equation is simply $\frac{\mathrm{D}_g q}{\mathrm{D}t} = 0$, where the [material derivative](@entry_id:266939) is taken with the geostrophic velocity. This model filters [gravity waves](@entry_id:185196) and captures the essential dynamics of large-scale eddies and Rossby waves.

### Characterizing Flow Regimes: Nondimensional Numbers

The behavior of geophysical fluids is determined by the relative importance of various forces: inertia, viscosity, rotation, and buoyancy. This balance is quantified by a set of canonical nondimensional numbers, derived by scaling the governing equations .

-   **Reynolds Number ($\mathrm{Re} = UL/\nu$):** Ratio of advective inertia to [viscous forces](@entry_id:263294). High $\mathrm{Re}$ flows are turbulent, with viscosity important only in thin [boundary layers](@entry_id:150517).
-   **Rossby Number ($\mathrm{Ro} = U/(fL)$):** Ratio of advective inertia to Coriolis force. $\mathrm{Ro} \ll 1$ indicates rotationally dominated, nearly [geostrophic flow](@entry_id:166112).
-   **Froude Number ($\mathrm{Fr} = U/(NL)$):** Ratio of kinetic energy to potential energy in a [stratified fluid](@entry_id:201059). $\mathrm{Fr} \ll 1$ indicates that stratification is strong and vertical motions are suppressed.
-   **Ekman Number ($\mathrm{Ek} = \nu/(fL^2)$):** Ratio of viscous forces to Coriolis force. Small $\mathrm{Ek}$ indicates that the interior flow is inviscid, but viscosity becomes crucial in boundary layers.
-   **Rayleigh Number ($\mathrm{Ra} = g\alpha\Delta T L^3/(\nu\kappa)$):** Ratio of buoyancy driving to diffusive damping in [thermal convection](@entry_id:144912). High $\mathrm{Ra}$ signals the onset of vigorous convection.
-   **Prandtl Number ($\mathrm{Pr} = \nu/\kappa$):** Ratio of [momentum diffusivity](@entry_id:275614) ($\nu$) to thermal diffusivity ($\kappa$). It determines the relative thickness of viscous and thermal boundary layers.

A classic example of a [force balance](@entry_id:267186) dictated by these numbers is the **Ekman layer**, which forms at the top (or bottom) of a rotating fluid subject to stress. In this layer, a steady balance exists between the Coriolis force and the vertical diffusion of momentum (viscous stress). The characteristic thickness of this layer scales as $\delta_E = \sqrt{2\nu/|f|}$ . A key result is that the net, depth-integrated transport of water in this layer, the **Ekman transport**, is directed exactly $90^\circ$ to the right of the applied wind stress in the Northern Hemisphere and $90^\circ$ to the left in the Southern Hemisphere. This transport is given by:

$$
\boldsymbol{T}_E = \frac{\boldsymbol{\tau}_s \times \hat{\boldsymbol{k}}}{\rho f}
$$

where $\boldsymbol{\tau}_s$ is the surface wind stress. This mechanism is fundamental to driving large-scale [ocean gyres](@entry_id:180204).