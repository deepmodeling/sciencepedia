## Introduction
The interaction between atmospheric flow and mountainous terrain exerts a powerful retarding force, or drag, that profoundly influences the planet's weather and climate. This [orographic drag](@entry_id:1129206) is a critical sink of momentum in the atmosphere, yet the mountains and valleys that generate it are often too small to be explicitly represented in global climate and [weather prediction models](@entry_id:1134022). This discrepancy creates a significant knowledge gap, as neglecting this drag leads to major errors in simulating [atmospheric circulation](@entry_id:199425), such as excessively strong surface winds and a poorly represented stratosphere. The solution lies in [orographic drag](@entry_id:1129206) parameterization—a sophisticated set of methods designed to represent the effects of this unresolved topography.

This article provides a comprehensive exploration of [orographic drag](@entry_id:1129206) parameterization, structured to build understanding from fundamental concepts to practical application. The first chapter, "Principles and Mechanisms," delves into the core physics, distinguishing between low-level flow blocking and vertically propagating gravity waves, and introduces the key parameters that govern their behavior. The second chapter, "Applications and Interdisciplinary Connections," examines how these principles are implemented in Earth system models, addressing challenges like numerical stability and energy conservation, and explores the far-reaching impacts on global circulation and connections to fields like oceanography. Finally, "Hands-On Practices" offers a series of guided problems to solidify theoretical knowledge and provide practical experience in building and analyzing these crucial schemes.

## Principles and Mechanisms

Atmospheric flow interacting with underlying topography experiences a retarding force, or drag, which significantly impacts the large-scale momentum budget of the atmosphere. This [orographic drag](@entry_id:1129206) is not a single phenomenon but a composite of several physical processes whose relative importance depends on the characteristics of both the flow and the terrain. In numerical models of the atmosphere, particularly General Circulation Models (GCMs) and climate models, the grid resolution is often too coarse to explicitly resolve the mountains and valleys that generate this drag. Therefore, the effects of this subgrid-scale orography must be represented through a set of physical approximations known as a **parameterization**. This chapter details the fundamental principles and mechanisms that form the basis of modern [orographic drag](@entry_id:1129206) parameterizations.

### The Fundamental Origin of Orographic Drag: Form Drag

At its most basic level, the drag exerted by a mountain on the atmosphere is a type of **[form drag](@entry_id:152368)**, also known as [pressure drag](@entry_id:269633). This force arises from an asymmetric [pressure distribution](@entry_id:275409) on the surface of the obstacle. When a fluid flows past a solid body, the flow is decelerated on the upwind (windward) side, leading to an increase in surface pressure. Conversely, on the downwind (leeward) side, the flow may accelerate and separate from the surface, creating a turbulent, low-pressure wake. 

This pressure difference, with higher pressure on the windward face and lower pressure on the leeward face, results in a [net force](@entry_id:163825) exerted by the fluid on the mountain in the direction of the flow. By Newton's third law, the mountain exerts an equal and opposite force on the fluid, acting as a drag that removes momentum from the flow. Mathematically, the total horizontal drag force, $\mathcal{D}$, on a terrain feature described by the height field $h(x,y)$ is the integral of the [surface pressure](@entry_id:152856) $p_s$ acting against the terrain slope:

$$
\mathcal{D} = - \iint_{\text{domain}} p_s \nabla_h h \cdot \hat{\mathbf{u}} \, dA
$$

where $\nabla_h$ is the horizontal gradient operator and $\hat{\mathbf{u}}$ is the unit vector in the direction of the mean flow. In a numerical model, the effect of this subgrid-scale force is represented as a negative tendency term in the grid-mean momentum equation, acting as a sink of large-scale momentum concentrated near the surface.

While all [orographic drag](@entry_id:1129206) is fundamentally form drag, its physical manifestation and vertical structure depend critically on the atmospheric conditions. For the purpose of parameterization, it is essential to distinguish between two dominant regimes: low-level drag due to flow blocking, and drag associated with the vertical propagation of [internal gravity waves](@entry_id:185206). 

### The Two Regimes of Orographic Drag

The response of [stratified flow](@entry_id:202356) to an obstacle is governed by the balance between the fluid's kinetic energy and the potential energy required to lift it over the terrain against the stable stratification. This balance is encapsulated by the dimensionless **Froude number**, defined as:

$$
Fr = \frac{U}{N H}
$$

where $U$ is the characteristic speed of the flow impinging on the mountain, $H$ is the characteristic height of the mountain, and $N$ is the **Brunt–Väisälä frequency**, which measures the [static stability](@entry_id:1132318) of the atmosphere. A higher value of $N$ indicates stronger stratification.

#### Low-Level Blocking Drag

When the Froude number is small ($Fr \lesssim 1$), the oncoming flow has insufficient kinetic energy to surmount the potential energy barrier posed by the mountain. The stably [stratified fluid](@entry_id:201059) resists vertical displacement. Consequently, the low-level flow stagnates on the windward slope and is deflected horizontally around the obstacle. This process is known as **flow blocking**.  This blocking creates a significant high-pressure anomaly on the windward face, leading to a large form drag that is exerted primarily in the lower levels of the atmosphere. In this regime, the atmospheric disturbance created by the mountain does not typically propagate far into the vertical, and the drag is largely confined near the surface.

#### Gravity Wave Drag

When the Froude number is larger ($Fr \gtrsim 1$), the flow has sufficient kinetic energy to travel over the mountain. As air parcels are forced upward over the windward slope and downward on the leeward slope, the stable stratification provides a restoring force, setting up oscillations in the lee of the mountain. These oscillations are known as **internal gravity waves** or, in this context, **[mountain waves](@entry_id:1128215)**.

A key feature of these waves is their ability to transport momentum. Vertically propagating [mountain waves](@entry_id:1128215) carry a vertical flux of horizontal momentum, given by $\mathcal{F} = \rho \overline{u' w'}$, where $\rho$ is the air density and $u'$ and $w'$ are the perturbation horizontal and vertical velocities, respectively.  This momentum is extracted from the mean flow near the surface and transported upwards. The drag itself is not exerted until the wave dissipates and deposits its momentum at some higher altitude. The resulting drag on the mean flow, $\overline{U}$, at a given height is determined by the vertical divergence of this [momentum flux](@entry_id:199796):

$$
\frac{\partial \overline{U}}{\partial t} \bigg|_{\text{drag}} \approx - \frac{1}{\rho} \frac{\partial \mathcal{F}}{\partial z}
$$

This mechanism is fundamentally different from blocking drag because it displaces the drag from the surface to potentially very high levels in the atmosphere, including the stratosphere and mesosphere, where it can have a profound impact on the global circulation.

### The Physics of Mountain Wave Propagation

To understand when gravity wave drag is an important mechanism, we must first understand the conditions under which [mountain waves](@entry_id:1128215) can propagate vertically.

#### Linear Mountain Wave Theory

We can gain significant insight by considering a simplified, two-dimensional model of steady, inviscid, Boussinesq flow with constant wind speed $U$ and stability $N$ over a small-amplitude sinusoidal ridge, $h(x) = a \cos(kx)$.  The flow is governed by a set of linearized equations for the perturbations. The validity of this linearization rests on two key assumptions: the mountain slope must be small ($|ak| \ll 1$), and the dimensionless mountain height must be small ($aN/U \ll 1$), implying that fluid parcels are not vertically displaced by a large fraction of the intrinsic vertical wavelength of the flow.

Under these assumptions, the linearized equations can be combined into a single governing equation for the vertical structure of the waves. For a more general background state where the wind $U(z)$ and stability $N(z)$ vary with height, this takes the form of the **Taylor-Goldstein equation**:

$$
\frac{d^2 \hat{w}}{dz^2} + m^2(z) \hat{w} = 0
$$

where $\hat{w}(z)$ is the [complex amplitude](@entry_id:164138) of the vertical velocity and $m^2(z)$ is the square of the local vertical wavenumber.

#### The Scorer Parameter and the Propagation Condition

The vertical wavenumber, $m(z)$, determines the vertical structure of the wave. For vertically propagating waves, $m$ must be real, implying $m^2 > 0$. If $m$ is imaginary ($m^2  0$), the solution is an exponential function, representing a vertically trapped or **[evanescent wave](@entry_id:147449)** that decays with height and cannot transport momentum to the upper atmosphere.

The vertical wavenumber squared is given by the relation:

$$
m^2(z) = l^2(z) - k^2
$$

where $k$ is the horizontal wavenumber of the forcing terrain, and $l(z)$ is the **Scorer parameter**, a crucial quantity that characterizes the atmospheric waveguide: 

$$
l^2(z) = \frac{N^2(z)}{U^2(z)} - \frac{1}{U(z)} \frac{d^2 U}{dz^2}
$$

The Scorer parameter consists of two terms: a buoyancy term ($N^2/U^2$) and a wind curvature term ($-U''/U$). Vertical propagation ($m^2 > 0$) is possible only if the Scorer parameter is large enough to overcome the horizontal wavenumber of the terrain, i.e., $l^2 > k^2$. This means that short horizontal waves (large $k$) are less likely to propagate vertically than long horizontal waves (small $k$).

This propagation condition provides another criterion for distinguishing the drag regimes. Approximating the dominant wavenumber of a mountain by its half-width $L$ as $k \sim 1/L$, the condition for propagation becomes $1/L^2  N^2/U^2$ (ignoring the curvature term for simplicity), which can be rearranged to $U/(NL)  1$. 
Thus, a parameterization must consider two conditions:
1.  **Low-Level Blocking Drag** dominates when the flow is blocked ($Fr \lesssim 1$) and the waves are evanescent ($U/(NL) \gtrsim 1$).
2.  **Gravity Wave Drag** is active when the flow can surmount the terrain and the waves can propagate vertically ($U/(NL)  1$).

### Vertical Propagation and Momentum Deposition

Once a gravity wave is launched and propagates upward, its momentum flux is conserved with height until it encounters a region where it dissipates or "breaks." This deposition can occur through several mechanisms.

#### Wave Saturation

In an anelastic atmosphere, density $\rho(z)$ decreases approximately exponentially with height. For the vertical momentum flux $\mathcal{F} = \rho \overline{u' w'}$ to be conserved, the magnitude of the velocity perturbations ($u', w'$) must grow as $\rho^{-1/2}$. This [exponential growth](@entry_id:141869) cannot continue indefinitely. Eventually, the wave amplitude becomes so large that the wave-induced shear or [temperature lapse rate](@entry_id:275316) renders the flow locally unstable, leading to turbulence and dissipation. This process is called **saturation** or **wave breaking**.  When a wave saturates, its amplitude is limited, its momentum flux is reduced, and the lost momentum is deposited into the mean flow, creating a drag force.

#### Critical Levels

A wave can also be absorbed at a **critical level**. For a stationary wave (with ground-based frequency $\omega=0$), its frequency relative to the moving fluid, the **intrinsic frequency**, is $\hat{\omega} = - \mathbf{k} \cdot \mathbf{U}(z)$. A critical level is defined as the height $z_c$ where the intrinsic frequency goes to zero. For a simple 2D case, this occurs where the background wind component parallel to the [wave vector](@entry_id:272479) vanishes, i.e., $U(z_c) = 0$. 

As a wave approaches a critical level, its vertical wavenumber becomes very large, and its vertical wavelength shrinks to zero. This leads to extremely efficient wave dissipation through viscous or thermal effects, even if they are very small. As a result, the wave is almost completely absorbed, and its momentum flux is deposited in a thin layer just below the critical level.

#### Turning Levels and Reflection

The atmosphere can also feature layers where waves are evanescent, bounded by **turning levels** where $m^2(z) = 0$. If a propagating wave encounters a finite-depth evanescent layer (a region where $l^2  k^2$), it will be partially reflected. A portion of the [wave energy](@entry_id:164626) will "tunnel" through the barrier and continue propagating above it, but the transmitted [momentum flux](@entry_id:199796) is exponentially reduced.  The [transmission coefficient](@entry_id:142812) $T$ through a barrier from height $z_1$ to $z_2$ is approximately:

$$
T \approx \exp\left(-2 \int_{z_{1}}^{z_{2}} |m(z')| \, dz'\right)
$$

This process is conservative and does not itself deposit momentum, but it can significantly reduce the amount of momentum that reaches the upper atmosphere.

### Principles of a Modern Orographic Drag Parameterization

Synthesizing these physical mechanisms leads to the general structure of a modern [orographic drag](@entry_id:1129206) [parameterization scheme](@entry_id:1129328). 

1.  **Characterize Subgrid Orography:** The scheme must first quantify the unresolved terrain within each model grid box. This is done by analyzing a high-resolution Digital Elevation Model (DEM). Key statistical metrics are computed, including the standard deviation, slope, and importantly, the anisotropy and orientation of the subgrid ridges. Directional properties are typically extracted from the [eigenvalues and eigenvectors](@entry_id:138808) of the **structure tensor**, $S = \overline{\nabla h (\nabla h)^\top}$. 

2.  **Launch and Propagate:** At the lowest model level, the scheme calculates a [surface stress](@entry_id:191241). This stress is partitioned. A portion is assigned to low-level blocking drag, which is applied locally based on criteria like the Froude number. The remaining stress launches a spectrum of vertically propagating gravity waves. The [momentum flux](@entry_id:199796) of each wave component is then propagated upward from one model level to the next.

3.  **Deposit Momentum:** At each vertical level, the scheme checks for dissipation mechanisms. It calculates the height of the next critical level ($z_c$) and the height at which the wave would saturate due to amplitude growth ($z_s$). The wave is assumed to break at the lower of these two altitudes, $z_* = \min(z_s, z_c)$.  The momentum flux is then depleted, and the corresponding drag is applied to the mean flow at that level.

4.  **Scale Awareness:** A crucial principle for any robust parameterization is **scale awareness**. The total physical drag exerted by the real orography is invariant. A model partitions this total drag into a resolved part (handled by the model's dynamics interacting with the resolved grid-scale terrain) and an unresolved part (handled by the parameterization). As [model resolution](@entry_id:752082) increases, the grid length $\Delta x$ decreases, and more of the terrain becomes explicitly resolved. A [scale-aware parameterization](@entry_id:1131257) must recognize this. The amount of parameterized drag must decrease as resolution increases to avoid "double-counting" the drag from topographic features that are now explicitly represented by the model's dynamics.  This ensures that the sum of the resolved and parameterized drag remains a consistent approximation of the total drag across a range of model resolutions.