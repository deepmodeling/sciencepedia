## Introduction
The upper few meters of the ocean, the so-called ocean surface boundary layer, is a region of intense physical and biogeochemical activity, mediating the crucial exchange of heat, momentum, and gases between the atmosphere and the ocean interior. While wind-driven shear is a well-known driver of turbulence in this layer, a more subtle yet powerful mechanism, Langmuir turbulence, profoundly enhances vertical mixing. This process, driven by the interaction between surface waves and currents, is often underrepresented or omitted in standard ocean models, leading to significant biases in the prediction of mixed layer depth, surface temperatures, and biogeochemical cycling. This article provides a graduate-level guide to understanding and parameterizing Langmuir turbulence in computational ocean models. The "Principles and Mechanisms" chapter will dissect the core physics, from the wave-induced Stokes drift to the energetic consequences and dimensionless scaling. Following this, the "Applications and Interdisciplinary Connections" chapter explores the far-reaching impacts on the upper ocean structure and air-sea exchange, and details how these effects are captured in models. Finally, the "Hands-On Practices" section offers practical exercises to solidify these concepts, enabling a deeper, quantitative understanding of this critical oceanographic process.

## Principles and Mechanisms

This chapter delineates the fundamental principles governing Langmuir turbulence, beginning with its causal mechanism—the interaction between wave-induced Stokes drift and a mean current. We will explore the energetic consequences of this interaction, develop the key [dimensionless parameters](@entry_id:180651) used for its scaling, and detail how these principles are translated into parameterizations for computational ocean models. Finally, we will examine how Langmuir turbulence is modulated by other physical processes, such as stratification and [wave breaking](@entry_id:268639).

### The Genesis of Langmuir Turbulence: Stokes Drift and the Vortex Force

Langmuir turbulence is a distinct form of organized turbulent motion in the upper ocean that arises from the interaction of surface gravity waves with a mean current, typically driven by wind. The mechanism is not a direct result of the waves' orbital motion but rather emerges from a more subtle, second-order wave effect known as **Stokes drift**.

Stokes drift, denoted by the vector field $\boldsymbol{u}_s$, is the net Lagrangian drift velocity of fluid parcels in a wave field. While fluid parcels undergo nearly closed [elliptical orbits](@entry_id:160366) at the linear (first) order, a small, unclosed portion of their trajectory results in a net forward motion in the direction of wave propagation. This drift is strongest at the surface and decays with depth. For a simple monochromatic deep-water wave with amplitude $a$, angular frequency $\omega$, and wavenumber $k$, the horizontal Stokes drift $u_s$ at a depth $z$ (where $z \le 0$) can be derived from the first-order [wave kinematics](@entry_id:756646) . The result is a purely horizontal drift in the direction of wave propagation, with a magnitude given by:

$u_s(z) = \omega k a^2 e^{2kz}$

It is crucial to note that this is a second-order effect, proportional to the wave steepness squared ($a^2k^2$), and its vertical decay rate, characterized by the $e^{2kz}$ term, is twice as fast as that of the first-order wave orbital velocities (which decay as $e^{kz}$). This [vertical shear](@entry_id:1133795) in the Stokes drift profile, $\partial_z u_s$, is a critical ingredient for the generation of Langmuir turbulence.

The core mechanism linking Stokes drift to organized turbulence was elucidated by Craik and Leibovich. Their theory revealed that the interaction between the wave-induced Stokes drift, $\boldsymbol{u}_s$, and the vorticity of the Eulerian mean flow, $\boldsymbol{\omega} = \nabla \times \boldsymbol{u}$, generates a [non-conservative force](@entry_id:169973) within the fluid. This force, known as the **Craik-Leibovich (CL) vortex force**, is given by the [cross product](@entry_id:156749):

$\boldsymbol{F}_{CL} = \boldsymbol{u}_s \times \boldsymbol{\omega}$

This vortex force acts to tilt the mean shear vorticity into streamwise rolls, the characteristic [coherent structures](@entry_id:182915) known as Langmuir cells. To see how this force enters the governing equations, we consider the Reynolds-averaged Navier-Stokes (RANS) equations modified to include wave effects. The effect of the waves on the mean flow, derived from a Generalized Lagrangian Mean (GLM) framework, can be decomposed into conservative pressure-like terms and the non-conservative vortex force. The resulting Eulerian-mean momentum equation for an incompressible Boussinesq fluid in a rotating frame is :

$\dfrac{\partial \boldsymbol{u}}{\partial t} + \left(\boldsymbol{u}\cdot\nabla\right)\boldsymbol{u} + f\,\hat{\boldsymbol{z}}\times\boldsymbol{u} = -\nabla \tilde{p} + b\,\hat{\boldsymbol{z}} + \nu\,\nabla^2\boldsymbol{u} + \boldsymbol{u}_s\times\boldsymbol{\omega}$

Here, $\boldsymbol{u}$ is the Eulerian mean velocity, $f$ is the Coriolis parameter, $\hat{\boldsymbol{z}}$ is the vertical unit vector, $b$ is the buoyancy, $\nu$ is the kinematic viscosity, and $\tilde{p}$ is a modified pressure that has absorbed all conservative wave-induced forces. The final term, $\boldsymbol{u}_s\times\boldsymbol{\omega}$, is the CL vortex force. Its presence as a source term in the mean momentum equation provides the driving mechanism for Langmuir circulations and the associated enhancement of turbulent mixing.

### The Energetics of Wave-Current Interaction

The CL vortex force acts as a pathway for energy to be transferred from the surface wave field to the turbulent motions of the mean flow. This can be rigorously quantified by examining the budget for **Turbulent Kinetic Energy (TKE)**, defined as $k = \frac{1}{2} \langle u_i' u_i' \rangle$, where $u_i'$ are the turbulent velocity fluctuations and angle brackets denote averaging. The TKE budget equation describes the local rate of change of TKE as a balance of production, transport, and dissipation:

$\dfrac{\partial k}{\partial t} = P_S + P_B + P_L - \varepsilon + T$

Here, $P_S$ is the production of TKE from the shear of the mean flow, $P_B$ is the production or destruction of TKE by buoyancy forces, $\varepsilon$ is the [viscous dissipation](@entry_id:143708) rate, and $T$ represents all transport terms (turbulent, pressure, and [viscous diffusion](@entry_id:187689)). The inclusion of the CL vortex force introduces an additional production term, $P_L$, known as **Langmuir production** . This term represents the rate of work done by the fluctuating vortex force, and it can be shown to be equivalent to the work done by the Reynolds stresses against the shear of the Stokes drift profile:

$P_L = -\langle u_i' u_j' \rangle \partial_j u_{s,i}$

This form is particularly insightful as it shows a direct analogy to standard shear production, $P_S = -\langle u_i' u_j' \rangle \partial_j U_i$. Langmuir production extracts energy from the mean wave field (as embodied by $\boldsymbol{u}_s$) via the turbulent stresses, injecting it into the TKE budget.

For the common case of horizontally homogeneous conditions with the mean wind and waves aligned in the $x$-direction, the Stokes drift is $\boldsymbol{u}_s = (U_s(z), 0, 0)$. The [dominant term](@entry_id:167418) in the Langmuir production then becomes the interaction of the vertical flux of horizontal momentum, $\langle u'w' \rangle$, with the [vertical shear](@entry_id:1133795) of the Stokes drift :

$P_L(z) = -\langle u' w' \rangle \dfrac{d U_s}{dz}$

Since wind stress drives a downward flux of momentum ($\langle u'w' \rangle  0$, making $-\langle u'w' \rangle > 0$) and the Stokes drift shear $dU_s/dz$ is positive (as $U_s$ decreases with depth, and $z$ is typically positive upwards), $P_L$ is a [positive definite](@entry_id:149459) production term. For typical mid-latitude open-ocean conditions, this energy input can be substantial. For example, for a wave field with a period of $8\,\mathrm{s}$ and an amplitude of $0.75\,\mathrm{m}$ interacting with wind-driven turbulence characterized by a [friction velocity](@entry_id:267882) of $u_* = 0.015\,\mathrm{m\,s^{-1}}$, the local Langmuir production rate at a depth of $5\,\mathrm{m}$ can be on the order of $3 \times 10^{-7}\,\mathrm{W\,kg^{-1}}$. The vertically integrated energy transfer from the waves to the turbulence over the upper $10\,\mathrm{m}$ can be approximately $5 \times 10^{-3}\,\mathrm{W\,m^{-2}}$, a value comparable to the direct energy input from the wind .

### Dimensionless Scaling: The Langmuir Number

To parameterize the effects of Langmuir turbulence, it is essential to develop a dimensionless number that quantifies its strength relative to standard shear-driven turbulence. This is achieved by forming a ratio of the [characteristic scales](@entry_id:144643) of the CL vortex force and the shear-driven turbulent stress .

The CL vortex force per unit mass, $\boldsymbol{u}_s \times \boldsymbol{\omega}$, scales as $u_s U / L$, where $U$ and $L$ are characteristic velocity and length scales of the turbulence. The shear-driven turbulent stress, which drives shear production, scales as $u_*^2 / L$, where $u_*$ is the [friction velocity](@entry_id:267882). The natural velocity scale for turbulence in a wind-driven boundary layer is $U \sim u_*$. The ratio of these two forces is therefore:

$\dfrac{\text{CL force scale}}{\text{Shear stress scale}} \sim \dfrac{u_s u_*/L}{u_*^2/L} = \dfrac{u_s}{u_*}$

This ratio, $u_s/u_*$, compares the strength of the wave-driven forcing to the wind-driven forcing. The standard convention in oceanography is to define a parameter that becomes small when wave effects are strong. This leads to the definition of the **turbulent Langmuir number**, $La_t$, as the square root of the inverse of this ratio:

$La_t = \sqrt{\dfrac{u_*}{U_{s0}}}$

where $U_{s0}$ is the surface value of the Stokes drift. According to this definition, strong Langmuir turbulence (large $U_{s0}$ relative to $u_*$) corresponds to small $La_t$.

The physical significance of this scaling can be understood by examining the ratio of the TKE production terms, $P_L/P_S$ . Using scaling laws for a neutral boundary layer, the shear of the mean current scales as $\partial_z U \sim u_*/|z|$, while the shear of the Stokes drift scales as $\partial_z U_s \sim k U_s$. The ratio of production terms is then:

$\dfrac{P_L}{P_S} \sim \dfrac{-\langle u'w' \rangle \partial_z U_s}{-\langle u'w' \rangle \partial_z U} \sim \dfrac{k U_s(z)}{u_*/|z|}$

Evaluating this at a characteristic depth for wave influence, $|z| \sim (2k)^{-1}$, where $U_s \sim U_{s0} e^{-1}$, we find:

$\dfrac{P_L}{P_S} \sim \dfrac{U_{s0}}{u_*} = \dfrac{1}{La_t^2} = La_t^{-2}$

This powerful result demonstrates that the relative contribution of Langmuir production to the TKE budget scales as $La_t^{-2}$. When $La_t \ll 1$, Langmuir production dominates over shear production, and the turbulence is Langmuir-type. When $La_t \gg 1$, shear production dominates, and the turbulence behaves as in a classic wind-driven boundary layer.

### Parameterizing Enhanced Mixing in Ocean Models

The primary effect of the additional TKE production from Langmuir turbulence is a significant enhancement of vertical mixing in the ocean surface boundary layer. In large-scale ocean models that cannot resolve turbulent eddies directly, this mixing is parameterized using an **eddy viscosity**, $K_m$, and an **eddy diffusivity**, $K_h$, which relate turbulent fluxes to mean gradients:

$\overline{w'u'} = -K_m \dfrac{\partial U}{\partial z} \quad \text{and} \quad \overline{w'\theta'} = -K_h \dfrac{\partial \theta}{\partial z}$

Langmuir turbulence enhances the magnitude of $K_m$ and $K_h$. The physical mechanism for this enhancement is the enlargement of the characteristic size of the turbulent eddies. The organized Langmuir cells are [coherent structures](@entry_id:182915) that can span the entire mixed layer, leading to a much larger effective **[mixing length](@entry_id:199968)**, $l_{eff}$, than would be expected from shear turbulence alone . Since eddy viscosity scales with the mixing length and a turbulent velocity scale, $K_m \sim l_{eff} q$, an increase in $l_{eff}$ directly leads to an increase in $K_m$.

Sophisticated parameterization schemes like the **K-Profile Parameterization (KPP)** prescribe the eddy diffusivity profile based on boundary layer scales: $K(z) = h \cdot w \cdot G(z/h)$, where $h$ is the boundary layer depth and $G$ is a non-dimensional shape function . To incorporate Langmuir turbulence, the baseline KPP diffusivities are multiplied by an enhancement factor, $f_L$, that is a function of the Langmuir number:

$K^{\text{Langmuir}}_{m,h} = K^{\text{KPP}}_{m,h} \cdot f_L(La_t, z)$

Based on the scaling of the production ratio $P_L/P_S \sim La_t^{-2}$, a common and physically-motivated form for this enhancement factor is:

$f_L(z) = 1 + \beta_L \, La_t^{-2} \, \Phi(z/h)$

Here, $\beta_L$ is an empirical constant of order one, and $\Phi(z/h)$ is a depth-dependent shape function that weights the enhancement towards the surface, mirroring the decay of the Stokes drift profile. This approach allows ocean models to capture the leading-order effect of Langmuir turbulence—enhanced vertical mixing—without explicitly resolving the complex dynamics of the CL vortex force.

### Modulation by Stratification and Distinction from Wave Breaking

The intensity and structure of Langmuir turbulence are modulated by other physical processes, most notably stable stratification and [wave breaking](@entry_id:268639).

**Stable Stratification:** In a stably stratified fluid, vertical motions must work against gravity, which extracts energy from the turbulence. This is represented by a negative buoyancy production term, $P_B  0$, in the TKE budget. The strength of this suppression is quantified by the squared **Brunt-Väisälä frequency**, $N^2 = -(g/\rho_0) \partial_z \bar{\rho}$, where $\bar{\rho}$ is the mean density. A larger $N^2$ indicates stronger stratification and a more effective sink for TKE. This suppresses all forms of turbulence, including Langmuir turbulence.

The competition between stabilizing buoyancy forces and destabilizing shear forces is captured by the gradient Richardson number, $Ri_g = N^2/S^2$. Langmuir turbulence provides an additional source of production, making the flow more susceptible to turbulence for a given stratification. This is captured by a **modified gradient Richardson number**, $Ri_g^*$, which includes the Stokes drift shear, $S_s^2 = \|\partial_z \boldsymbol{u}_s\|^2$ :

$Ri_g^* = \dfrac{N^2}{S^2 + \alpha S_s^2}$

where $\alpha$ is a coupling coefficient. The presence of the Stokes shear term $S_s^2$ in the denominator reduces the Richardson number, correctly reflecting that Langmuir forcing helps overcome the stabilizing effect of stratification.

**Wave Breaking:** It is critical to distinguish the bulk production mechanism of Langmuir turbulence (which can be generated by non-breaking waves) from the direct injection of turbulence at the surface by breaking waves .
- **Langmuir Turbulence** is a *bulk phenomenon*. The CL vortex force and the associated TKE production term $P_L$ are active throughout the near-surface layer where Stokes drift shear is significant. In a one-dimensional model without breaking, the appropriate boundary condition at the free surface ($z=0$) is a [zero-flux condition](@entry_id:182067) for TKE, i.e., $\partial k/\partial z = 0$.
- **Wave Breaking** is a *surface phenomenon*. It injects TKE directly at the air-sea interface. In a model, this is represented not as a bulk source term, but as a downward **[flux boundary condition](@entry_id:749480)** for TKE at $z=0$. This flux is typically parameterized to scale with the [friction velocity](@entry_id:267882) cubed, e.g., $\Phi_k|_{z=0} \propto u_*^3$. This requires a corresponding large [dissipation rate](@entry_id:748577) at the surface, leading to a Dirichlet boundary condition for $\varepsilon$, often scaled as $\varepsilon(0) \sim u_*^3/z_0$, where $z_0$ is a surface roughness length.

In summary, Langmuir turbulence and [wave breaking](@entry_id:268639) are distinct physical processes that are represented differently in turbulence models: one as a depth-dependent source term in the TKE equation, and the other as a flux condition at the surface boundary. Both contribute significantly to mixing in the ocean surface boundary layer, but their underlying principles and mechanisms are not the same.