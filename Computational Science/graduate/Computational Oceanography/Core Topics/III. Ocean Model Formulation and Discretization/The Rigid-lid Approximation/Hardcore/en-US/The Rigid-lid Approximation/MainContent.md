## Introduction
In the vast toolkit of computational oceanography, few simplifications have been as influential or as elegant as the [rigid-lid approximation](@entry_id:1131032). This foundational technique addresses a fundamental computational bottleneck in ocean modeling: the prohibitively small time steps required to numerically resolve fast-propagating external gravity waves in models with a free sea surface. For scientists aiming to simulate ocean circulation over decades or centuries, this constraint poses a significant barrier. The [rigid-lid approximation](@entry_id:1131032) offers a powerful solution by fundamentally altering the physics of the model to filter out these fast waves, enabling a dramatic increase in computational efficiency.

This article provides a comprehensive examination of the [rigid-lid approximation](@entry_id:1131032), from its theoretical underpinnings to its practical applications and limitations. By navigating through its core concepts, you will gain a deep understanding of this crucial trade-off between physical fidelity and computational feasibility. The discussion is structured to guide you from foundational theory to advanced application. In "Principles and Mechanisms," we will dissect the mathematical formulation and physical justification for replacing the dynamic free surface with a fixed lid. Following this, "Applications and Interdisciplinary Connections" explores how this approximation is used in large-scale climate models, its connection to numerical linear algebra and data assimilation, and the sophisticated hybrid strategies it enables. Finally, "Hands-On Practices" will offer concrete problems to solidify your understanding of the [scale analysis](@entry_id:1131264), computational advantages, and numerical implementation of the rigid-lid model.

## Principles and Mechanisms

In the hierarchy of approximations used to construct computationally tractable ocean models, the **[rigid-lid approximation](@entry_id:1131032)** stands as a classic and powerful tool. It is designed to address a specific and severe computational challenge inherent in models that include a freely evolving sea surface: the propagation of fast external gravity waves. This chapter elucidates the principles behind this approximation, its mathematical and computational implementation, and its physical consequences.

### The Free-Surface Model and Its Computational Constraint

Ocean models that resolve the evolution of the sea-surface elevation, $\eta(x,y,t)$, are known as free-surface models. The dynamics of the free surface are governed by the vertically integrated mass conservation (continuity) equation. For a fluid of total depth $D = H + \eta$, where $H$ is the resting depth, the continuity equation $\nabla_h \cdot \mathbf{u} + \partial_z w = 0$ can be integrated from the sea floor at $z=-H$ to the free surface at $z=\eta$. Applying the kinematic boundary conditions—no normal flow at the bottom, $w = 0$ at $z=-H$, and the material surface condition $w = D\eta/Dt$ at $z=\eta$—yields the prognostic equation for the free surface:
$$
\frac{\partial \eta}{\partial t} + \nabla_h \cdot \int_{-H}^{\eta} \mathbf{u} \, \mathrm{d}z = 0
$$
where $\mathbf{u}$ is the horizontal velocity vector.

This equation, coupled with the momentum equations, supports the propagation of surface gravity waves. In the limit of long wavelengths, the phase speed of these waves, known as the external or **barotropic gravity waves**, is given by $c_0 = \sqrt{gH}$. For a typical mid-latitude ocean basin with a depth of $H = 4000 \text{ m}$, this speed is approximately $c_0 \approx \sqrt{9.81 \, \mathrm{m/s^2} \times 4000 \, \mathrm{m}} \approx 200 \, \mathrm{m/s}$.

The existence of these fast-moving waves places a stringent constraint on the time step, $\Delta t$, of any explicit [numerical integration](@entry_id:142553) scheme. According to the **Courant-Friedrichs-Lewy (CFL) stability condition**, the time step must be small enough that information does not travel more than one grid cell, $\Delta x$, in a single step. Mathematically, $\Delta t \lesssim \Delta x / c_0$. For a model with a grid spacing of $\Delta x = 10 \text{ km}$, the time step would be limited to $\Delta t \lesssim (10 \times 10^3 \, \mathrm{m}) / (200 \, \mathrm{m/s}) = 50 \text{ s}$. This is computationally prohibitive for long-term climate simulations, where the dynamical phenomena of interest, such as [ocean gyres](@entry_id:180204) and [mesoscale eddies](@entry_id:1127814), evolve on time scales of days to years. The [rigid-lid approximation](@entry_id:1131032) is designed to circumvent this very constraint. 

### The Rigid-Lid Constraint: Formulation and Justification

The [rigid-lid approximation](@entry_id:1131032) directly filters external gravity waves by removing their physical mechanism: the evolution of the free surface. This is achieved by imposing the mathematical constraint that the free-surface elevation is fixed at its mean level for all time and space:
$$
\eta(x,y,t) \equiv 0
$$
This constraint transforms the upper boundary of the ocean from a moving surface to a fixed, impermeable "lid" at $z=0$. Consequently, the kinematic boundary condition at the surface becomes identical to that at the bottom: $w(x,y,0,t) = 0$. 

With this new boundary condition, the prognostic equation for $\eta$ becomes a diagnostic constraint on the fluid motion. The vertically integrated continuity equation now reads:
$$
\nabla_h \cdot \int_{-H}^{0} \mathbf{u} \, \mathrm{d}z = 0
$$
This equation mandates that the depth-integrated, or **barotropic**, horizontal transport must be non-divergent at every point and at all times. Any horizontal convergence of mass into a water column must be exactly balanced by horizontal divergence elsewhere in the column, without any change in the column's height.

The physical justification for this seemingly drastic approximation stems from a [scaling analysis](@entry_id:153681) of the governing equations. For large-scale, low-frequency ocean dynamics, the characteristic horizontal velocity $U$ is much smaller than the external gravity [wave speed](@entry_id:186208) $\sqrt{gH}$. The dimensionless parameter that governs the validity of the approximation is the square of the **Froude number**, $Fr = U/\sqrt{gH}$. By non-dimensionalizing the [primitive equations](@entry_id:1130162), one can show that the characteristic amplitude of the free-surface elevation, $E$, scales as $E \sim U^2/g$. The ratio of this elevation to the total depth is therefore:
$$
\epsilon = \frac{E}{H} \sim \frac{U^2}{gH} = Fr^2
$$
For typical oceanic parameters ($U \approx 0.1 \, \mathrm{m/s}$, $H \approx 4000 \, \mathrm{m}$), the Froude number is very small ($Fr \approx 5 \times 10^{-4}$), and thus $\epsilon$ is exceedingly small. This indicates that for many dynamical regimes, the free-surface variations are negligible compared to the total ocean depth, validating the rigid-lid assumption. 

### The Surface Pressure as a Lagrange Multiplier

Imposing the rigid-lid constraint $\nabla_h \cdot \int \mathbf{u} \, \mathrm{d}z = 0$ on the primitive equations, which prognostically determine the velocity field $\mathbf{u}$, creates an over-determined system. The equations of motion do not inherently guarantee that the resulting velocity field will satisfy this global, diagnostic constraint. To resolve this, a new variable is introduced: a depth-independent pressure field, $\pi(x,y,t)$, often called the **surface pressure** or **barotropic pressure**.

This pressure acts as a **Lagrange multiplier**. Its purpose is to adjust the horizontal flow at each time step to ensure the non-divergence constraint is met. In a rigid-lid model, the total pressure field $p(x,y,z,t)$ is decomposed into three components:
$$
p(x,y,z,t) = \underbrace{p_a - \rho_0 g z}_{\text{Reference Hydrostatic}} \;+\; \underbrace{\int_{z}^{0} g \rho'(x,y,z',t) \,\mathrm{d}z'}_{\text{Baroclinic}} \;+\; \underbrace{\pi(x,y,t)}_{\text{Surface (Barotropic)}}
$$
Here, $p_a$ is a constant atmospheric pressure, $\rho_0$ is the reference density, and $\rho'$ is the density anomaly. The horizontal gradient of this pressure field, which drives the flow, is:
$$
-\frac{1}{\rho_0}\nabla_h p = -\frac{g}{\rho_0}\nabla_h \left( \int_{z}^{0} \rho' \,\mathrm{d}z' \right) - \frac{1}{\rho_0}\nabla_h \pi(x,y,t)
$$
The first term is the depth-dependent **[baroclinic pressure gradient](@entry_id:1121347)**, which drives internal motions. The second term is the depth-independent **barotropic pressure gradient**, which adjusts the depth-averaged flow. The surface pressure $\pi$ has no prognostic equation of its own; it is determined diagnostically at each instant to enforce the rigid-lid constraint. This reformulation fundamentally alters the structure of the model's variables: the prognostic variable $\eta$ is eliminated, and its role is assumed by the diagnostic variable $\pi$. The core prognostic variables of the [primitive equations](@entry_id:1130162)—horizontal velocity $(u,v)$ and tracers such as potential temperature $(\theta)$ and salinity $(S)$—remain prognostic.  

### Computational Mechanism: The Elliptic Problem

The diagnostic determination of the [surface pressure](@entry_id:152856) $\pi$ is the central computational task in a rigid-lid model. This is typically accomplished using a **[projection method](@entry_id:144836)**. In a [discrete time](@entry_id:637509)-stepping scheme, the horizontal momentum equations are first advanced over a time step $\Delta t$ using all known forces (advection, Coriolis, [baroclinic pressure gradient](@entry_id:1121347), friction) to obtain a provisional, or "predicted," velocity field, $\mathbf{u}^*$. This provisional field will not, in general, satisfy the rigid-lid constraint.

Let the provisional depth-integrated transport be $\mathbf{T}^* = \int_{-H}^{0} \mathbf{u}^* \mathrm{d}z$. The final, corrected transport at the new time step, $\mathbf{T}^{n+1}$, is obtained by adding the effect of the unknown [surface pressure](@entry_id:152856) gradient:
$$
\mathbf{T}^{n+1} = \mathbf{T}^* - \Delta t \cdot \nabla_h \pi^{n+1}
$$
(Here, for simplicity, we have absorbed the constant factor of depth $H$ into the definition of $\pi$). We then enforce the rigid-lid constraint, $\nabla_h \cdot \mathbf{T}^{n+1} = 0$:
$$
\nabla_h \cdot (\mathbf{T}^* - \Delta t \cdot \nabla_h \pi^{n+1}) = 0
$$
This leads directly to a two-dimensional **Poisson equation** for the [surface pressure](@entry_id:152856) $\pi^{n+1}$:
$$
\nabla_h^2 \pi^{n+1} = \frac{1}{\Delta t} \nabla_h \cdot \mathbf{T}^*
$$
This elliptic partial differential equation must be solved over the entire horizontal domain. The source term on the right-hand side is the divergence of the provisional transport, which the pressure field must eliminate. At solid lateral boundaries where there can be no normal flow, $\mathbf{n} \cdot \mathbf{T}^{n+1} = 0$, which yields a **Neumann boundary condition** for the pressure:
$$
\frac{\partial \pi^{n+1}}{\partial n} = \frac{1}{\Delta t} \mathbf{n} \cdot \mathbf{T}^*
$$
Solving this elliptic [boundary-value problem](@entry_id:1121801) is computationally intensive, but it allows the use of a much larger time step than in an explicit free-surface model, leading to significant overall efficiency for long simulations. 

An alternative but related approach exists for simply connected domains. Since the final transport field $\mathbf{T}$ is non-divergent, it can be represented by a **[barotropic streamfunction](@entry_id:1121352)**, $\psi$, such that $\mathbf{T} = \hat{\mathbf{k}} \times \nabla_h \psi$. The relationship between the provisional transport and the final state can be seen as a Helmholtz decomposition. Instead of solving a Poisson equation for the [pressure potential](@entry_id:154481) $\pi$ (sourced by the divergence of $\mathbf{T}^*$), one can solve a Poisson equation for the [streamfunction](@entry_id:1132499) $\psi$ (sourced by the curl of $\mathbf{T}^*$). The [streamfunction](@entry_id:1132499) formulation is particularly elegant for closed basins, where the no-normal-flow condition simplifies to a constant-value (Dirichlet) boundary condition, which is often easier to solve numerically than the Neumann problem for pressure. The pressure formulation, however, is more versatile and more easily accommodates open boundary conditions. 

### Physical and Energetic Consequences

The primary physical consequence of the [rigid-lid approximation](@entry_id:1131032) is the complete filtering of any phenomena that fundamentally depend on sea-surface elevation changes. This includes:

-   **External (Barotropic) Tides**: The long gravity waves that constitute the ocean's tides are eliminated.
-   **Tsunamis**: These are also long [surface gravity waves](@entry_id:1132678) and are therefore filtered.
-   **Storm Surge**: The large-scale rise in sea level due to wind and atmospheric pressure is suppressed.

Conversely, the approximation retains motions that do not require net divergence of the water column. These include:

-   **Geostrophic Circulation**: The large-scale, slow, balanced flows that form [ocean gyres](@entry_id:180204) are well-represented. The barotropic component of this circulation is described by the non-divergent transport field.
-   **Internal Waves and Tides**: These waves propagate on density surfaces within the ocean interior. Their dynamics are governed by stratification and are compatible with the $w=0$ condition at the top and bottom boundaries. 

From an energetic perspective, the [rigid-lid approximation](@entry_id:1131032) removes the kinetic and potential energy associated with the external (barotropic) mode of motion. The total energy of the fluid can be partitioned among the external mode and a series of internal (baroclinic) modes. The energy of a wave mode is related to the square of its phase speed. As shown in the 'Timestep Advantage' example, the barotropic wave speed ($c_0 \approx 200$ m/s) is vastly larger than the first baroclinic [wave speed](@entry_id:186208) ($c_1 \approx 3$ m/s). Since kinetic energy is proportional to velocity squared, the barotropic mode contains the vast majority of the system's energy for a given amplitude of motion. By filtering this high-energy mode, the [rigid-lid approximation](@entry_id:1131032) retains only the much lower-energy internal dynamics, which is consistent with its focus on slow, evolving ocean currents. 

### A Quantitative Example: The Timestep Advantage

To quantify the computational advantage, we can compare the limiting time steps for a rigid-lid model versus a free-surface model. The free-surface model's time step is limited by the barotropic wave speed, $c_0 = \sqrt{gH}$. A rigid-lid model's time step is limited by the next fastest processes, typically the first [baroclinic mode](@entry_id:1121345) gravity waves, with speed $c_1$, or the advective velocity, $U$.

Consider an ocean with the following typical parameters: $H=4000$ m, upper layer thickness $H_1=500$ m, lower layer thickness $H_2=3500$ m, density jump $\Delta\rho=2 \text{ kg/m}^3$ over a reference density $\rho_0=1025 \text{ kg/m}^3$, and a characteristic current speed $U=0.5 \text{ m/s}$.

-   The barotropic [wave speed](@entry_id:186208) is $c_0 = \sqrt{gH} \approx 198 \text{ m/s}$.
-   The reduced gravity is $g' = g \frac{\Delta\rho}{\rho_0} \approx 0.0191 \text{ m/s}^2$.
-   The first baroclinic [wave speed](@entry_id:186208) is $c_1 = \sqrt{g' \frac{H_1 H_2}{H_1+H_2}} \approx 2.9 \text{ m/s}$.

The limiting speed for internal dynamics is $V_{\text{int}} = \max\{c_1, U\} = \max\{2.9, 0.5\} = 2.9 \text{ m/s}$. The ratio of the maximum allowable time step in a rigid-lid model to that in an explicit free-surface model is therefore:
$$
m = \frac{\Delta t_{\text{rigid-lid}}}{\Delta t_{\text{free-surface}}} = \frac{c_0}{V_{\text{int}}} = \frac{198}{2.9} \approx 68.5
$$
This means that a rigid-lid model can take a time step that is nearly 70 times larger than a simple explicit free-surface model. Modern free-surface models mitigate this cost using a "split-explicit" technique, where the barotropic mode is integrated with $m$ small time steps for every one large time step of the [baroclinic mode](@entry_id:1121345). The number $m$ thus represents the number of fast-mode substeps required, and the calculation highlights the fundamental timescale separation that motivates either the rigid-lid or the split-explicit approach. 

### Consistency with the Boussinesq Approximation

The [rigid-lid approximation](@entry_id:1131032) is almost always paired with the **Boussinesq approximation**, and this pairing is not coincidental. The Boussinesq approximation is valid when density variations are small, and its primary dynamical effect is to filter acoustically compressible sound waves, which travel at a speed of $\approx 1500 \text{ m/s}$. An ocean model is a hierarchy of filters:

1.  The Boussinesq approximation filters acoustic waves ($c \approx 1500 \text{ m/s}$).
2.  The [rigid-lid approximation](@entry_id:1131032) filters external gravity waves ($c_0 \approx 200 \text{ m/s}$).

Applying both approximations creates a computationally efficient system for studying the remaining slow dynamics: internal waves ($c_1 \approx 3 \text{ m/s}$), eddies, and basin-scale gyres. Using a rigid lid without the Boussinesq approximation would be of limited value, as the time step would still be severely constrained by the sound speed. The two approximations are consistent under the ordering that holds for large-scale oceanography: $U \ll c_1 \ll c_0 \ll c_{\text{sound}}$. Their joint application forms the basis of many foundational and modern ocean circulation models. 