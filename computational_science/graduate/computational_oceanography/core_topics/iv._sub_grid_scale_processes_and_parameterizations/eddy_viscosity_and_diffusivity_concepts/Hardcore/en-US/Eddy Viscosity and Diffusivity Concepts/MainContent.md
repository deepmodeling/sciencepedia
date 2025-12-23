## Introduction
Modeling the ocean is a multiscale challenge of immense proportions. The governing equations of fluid motion apply across a vast spectrum, from basin-wide gyres spanning thousands of kilometers to millimeter-scale turbulent eddies where energy is ultimately dissipated. Fully resolving this entire range of motion is computationally impossible for realistic ocean simulations. This creates a fundamental knowledge gap: how can we account for the collective effect of the unresolved, small-scale turbulent motions on the large-scale circulation that our models can resolve? The concepts of eddy viscosity and eddy diffusivity provide the most widely used framework for addressing this problem.

This article provides a comprehensive exploration of this framework, guiding you from fundamental theory to practical application. The first chapter, **"Principles and Mechanisms,"** delves into the theoretical origins of the turbulence closure problem through Reynolds decomposition and introduces the foundational Boussinesq hypothesis. The second chapter, **"Applications and Interdisciplinary Connections,"** examines how these concepts are implemented in various parameterization schemes within ocean models and used to interpret observational data across different oceanic regimes. Finally, the **"Hands-On Practices"** chapter offers practical exercises to solidify your understanding by applying these principles to computational problems. We begin by establishing the fundamental principles that make these powerful concepts necessary.

## Principles and Mechanisms

The equations of fluid motion, the Navier-Stokes equations, provide a complete description of oceanic flows. However, their direct numerical solution for realistic ocean basins is computationally prohibitive, as the range of motion spans from [global circulation patterns](@entry_id:1125664) down to millimeter-scale turbulence. Consequently, computational ocean models must operate at resolutions that are too coarse to resolve the smallest, most turbulent motions. The effect of these unresolved "sub-grid scale" processes on the resolved, large-scale flow must be parameterized. This chapter elucidates the fundamental principles and mechanisms underlying the most common approach to this challenge: the concept of eddy viscosity and eddy diffusivity.

### The Turbulence Closure Problem

To formalize the separation of scales, we employ **Reynolds decomposition**. Any instantaneous flow variable, such as a velocity component $u_i$, is decomposed into a mean part, $\overline{u}_i$, and a fluctuating part, $u_i'$. The mean, denoted by the overbar, represents the large-scale flow resolved by the model, while the fluctuation represents the unresolved turbulent part.

$u_i = \overline{u}_i + u_i'$

This decomposition is meaningful under a set of rules known as the **Reynolds axioms**. The averaging operator must be linear ($\overline{a+b} = \overline{a}+\overline{b}$) and idempotent ($\overline{\overline{a}} = \overline{a}$). A direct and crucial consequence is that the average of a fluctuation is, by definition, zero: $\overline{u_i'} = 0$ . Furthermore, when averaging products of variables, we find that the average of the product is the product of the averages plus the average of the product of the fluctuations:

$\overline{ab} = \overline{(\overline{a}+a')(\overline{b}+b')} = \overline{a}\overline{b} + \overline{a'b'}$

The term $\overline{a'b'}$ is the covariance between the fluctuations, which represents the net transport accomplished by the turbulent motions.

When this averaging procedure is applied to the nonlinear advection term ($u_j \partial_j u_i$) in the Navier-Stokes equations, a new term emerges in the equation for the mean flow . The averaged advection term becomes:

$\overline{u_j \partial_j u_i} = \overline{(\overline{u}_j+u_j') \partial_j (\overline{u}_i+u_i')} = \overline{u}_j \partial_j \overline{u}_i + \overline{u_j' \partial_j u_i'}$

For an incompressible fluid, where the divergence of the fluctuating velocity field is zero ($\partial_j u_j' = 0$), this new term can be written as the [divergence of a tensor](@entry_id:191736): $\overline{u_j' \partial_j u_i'} = \partial_j(\overline{u_i' u_j'})$. The Reynolds-Averaged Navier-Stokes (RANS) equation for the $i$-th component of mean momentum can then be written as:

$\partial_t \overline{u}_i + \overline{u}_j \partial_j \overline{u}_i = - \frac{1}{\rho_0} \partial_i \overline{p} + \nu \partial_{jj} \overline{u}_i - \partial_j(\overline{u_i' u_j'})$

The term $\overline{u_i' u_j'}$ is the **kinematic Reynolds stress tensor**. Its appearance means that the equations for the mean flow now contain new unknown variables—the correlations of the unresolved fluctuations. The system of equations is no longer closed. The **turbulence closure problem** is the challenge of finding a way to express these unknown Reynolds stresses in terms of the known, resolved mean flow variables.

### The Boussinesq Hypothesis: A Down-Gradient Closure

The simplest and most widely used approach to the closure problem is the **Boussinesq hypothesis**, which draws an analogy between turbulent transport and [molecular transport](@entry_id:195239). In a fluid, molecular motions cause viscosity, which is the diffusion of momentum. This [molecular transport](@entry_id:195239) is driven by velocity gradients. The Boussinesq hypothesis posits that turbulent eddies act in a similar manner, producing an "eddy" viscosity that is much larger and more effective at transporting momentum than its molecular counterpart .

It is critical to distinguish between these two viscosities. **Molecular viscosity**, $\nu$, is a thermodynamic property of the fluid itself, arising from intermolecular collisions. For seawater, its kinematic value is nearly constant, $\nu \approx 10^{-6} \, \mathrm{m}^2\,\mathrm{s}^{-1}$. In contrast, **eddy viscosity**, $\nu_t$, is not a fluid property but a *flow* property. It represents the efficiency of momentum transport by turbulent eddies and depends strongly on the characteristics of the flow, such as velocity, shear, and stratification. Its magnitude is typically many orders of magnitude larger than $\nu$.

The formal statement of the Boussinesq hypothesis relates the Reynolds stress tensor to the mean [rate-of-strain tensor](@entry_id:260652), $\overline{S}_{ij} = \frac{1}{2}(\partial_j \overline{u}_i + \partial_i \overline{u}_j)$ . For an [incompressible fluid](@entry_id:262924), the closure is written as:

$\overline{u_i' u_j'} = -\nu_t(\partial_j \overline{u}_i + \partial_i \overline{u}_j) + \frac{2}{3}k \delta_{ij}$

Here, $\delta_{ij}$ is the Kronecker delta and $k = \frac{1}{2}\overline{u_l' u_l'}$ is the **[turbulent kinetic energy](@entry_id:262712)** (TKE) per unit mass. The first term on the right-hand side models the anisotropic part of the Reynolds stress, while the second term accounts for the isotropic part, which is often absorbed into the pressure term. For a simple parallel [shear flow](@entry_id:266817), such as a mean current $\overline{u}(z)$ that varies only with depth, this complex tensorial relationship simplifies considerably. The vertical flux of horizontal momentum becomes:

$\overline{u' w'} = -\nu_t \frac{\partial \overline{u}}{\partial z}$

This is a **down-gradient** relationship: the [turbulent flux](@entry_id:1133512) acts to transport momentum from regions of high [mean velocity](@entry_id:150038) to regions of low [mean velocity](@entry_id:150038), thereby reducing the mean [velocity gradient](@entry_id:261686).

The same principle is applied to the turbulent transport of scalars like temperature ($T$) or salinity ($S$), a concept known as the **[gradient-diffusion hypothesis](@entry_id:156064)** . The turbulent vertical flux of a scalar $C$ is parameterized as:

$\overline{w' C'} = -K_C \frac{\partial \overline{C}}{\partial z}$

where $K_C$ is the **eddy diffusivity** for that scalar, with dimensions of $\mathrm{m^2\,\mathrm{s}^{-1}}$. The negative sign is fundamental: it ensures the flux is down-gradient, acting to smooth out mean gradients. For instance, in a stably stratified ocean where mean potential temperature $\overline{T}$ increases with height ($\partial_z \overline{T} > 0$), turbulence will mix warmer water downward ($w'0, T'>0$) and colder water upward ($w'>0, T'0$), resulting in a net negative (downward) correlation, $\overline{w'T'}  0$. The formula correctly predicts this, provided the eddy diffusivity $K_T$ is positive . The ratio of the eddy viscosity to the eddy diffusivity, known as the **turbulent Prandtl number** $Pr_t = \nu_t / K_T$, quantifies the [relative efficiency](@entry_id:165851) of turbulence in mixing momentum versus a scalar tracer. While often assumed to be of order one, it is not necessarily equal to one .

### The Influence of Stratification and Anisotropy

The Boussinesq hypothesis, in its simplest form, assumes a single, isotropic eddy viscosity. However, the ocean is fundamentally anisotropic due to the effects of gravity on a density-[stratified fluid](@entry_id:201059) and Earth's rotation.

#### Stratification and the Richardson Number

Vertical motion in a stably stratified ocean is strongly resisted by buoyancy forces. Turbulence can only be sustained if there is a strong enough source of energy to overcome this stabilizing effect. The primary source of energy for small-scale turbulence is the shear of the large-scale flow. The balance between these two effects is described by the **Turbulent Kinetic Energy (TKE) budget** . For a simplified steady state, the budget balances the rate of TKE production by shear, $P$, the rate of TKE destruction by buoyancy, $B$, and the rate of [viscous dissipation](@entry_id:143708), $\varepsilon$:

$P + B - \varepsilon = 0$

Using the down-gradient [closures](@entry_id:747387), the shear production term is $P = -\overline{u'w'} \partial_z \overline{u} = \nu_t (\partial_z \overline{u})^2$, which is always a source of TKE. The buoyancy flux term, in a stably [stratified fluid](@entry_id:201059) with buoyancy frequency $N$ (where $N^2 = \frac{g}{\rho_0} \frac{\partial \overline{\rho}}{\partial z} > 0$), is $B = \overline{b'w'} = -K_\rho N^2$, which represents a sink of TKE as turbulent motions do work against the stable density gradient.

The competition between the stabilizing stratification and the destabilizing shear is quantified by the dimensionless **gradient Richardson number**:

$Ri_g = \frac{N^2}{(\partial_z \overline{u})^2}$

A small $Ri_g$ indicates that shear dominates, allowing turbulence to thrive. A large $Ri_g$ indicates that stratification dominates, strongly suppressing vertical turbulence. For turbulence to be sustained, shear production must overcome the buoyancy sink ($P > |B|$). This leads to the conclusion that turbulence can only persist for $Ri_g$ below a critical value, $Ri_{cr}$. Theory and observations place this critical value near $0.25$. Turbulence closure schemes in ocean models must account for this by parameterizing the eddy coefficients $\nu_t$ and $K_T$ as sharply decreasing functions of $Ri_g$.

#### Anisotropy of Eddy Viscosity

The strong suppression of vertical motion by stratification leads to a profound anisotropy in turbulent mixing . We can estimate the characteristic scales of vertical and horizontal mixing separately.

Vertical mixing is limited by the largest eddy size that can overturn against the buoyancy force. This is the **Ozmidov scale**, $L_O = (\varepsilon/N^3)^{1/2}$. For typical ocean interior values of $\varepsilon \sim 10^{-9} \, \mathrm{m}^2\mathrm{s}^{-3}$ and $N \sim 10^{-3} \, \mathrm{s}^{-1}$, the Ozmidov scale is only about $1$ meter. The vertical eddy viscosity, scaling as $\nu_t^{(v)} \sim u_t L_t$, is correspondingly small, typically on the order of $10^{-5}$ to $10^{-3} \, \mathrm{m}^2\mathrm{s}^{-1}$ .

Horizontal mixing, in contrast, is dominated by large, energetic mesoscale eddies with horizontal length scales $L_h$ of tens of kilometers and velocity scales $U$ of tens of centimeters per second. The horizontal eddy viscosity, scaling as $\nu_t^{(h)} \sim U L_h$, is therefore much larger, with typical values of $10^2$ to $10^4 \, \mathrm{m}^2\mathrm{s}^{-1}$.

This enormous difference—where $\nu_t^{(h)}$ can be a million times larger than $\nu_t^{(v)}$—is a fundamental feature of [ocean dynamics](@entry_id:1129055) and a critical consideration for numerical modeling. It is also seen in energetic boundary layers, where turbulence is more vigorous, leading to vertical eddy viscosities of $10^{-3}$ to $10^{-1} \, \mathrm{m}^2\mathrm{s}^{-1}$, still much smaller than typical horizontal values but orders of magnitude larger than both interior vertical values and the molecular viscosity .

### Limitations and Advanced Concepts

The Boussinesq hypothesis provides a powerful and intuitive framework, but its underlying assumptions—that turbulent transport is a local, linear, down-gradient process—are often violated in the complex oceanic environment. Understanding these limitations is crucial for interpreting model results and developing more sophisticated parameterizations .

#### Failure of the Local Gradient-Diffusion Model

The relationship between [turbulent flux](@entry_id:1133512) and the mean gradient can break down under several conditions:

*   **Strongly Anisotropic Flows:** In regions of strong stratification ($Ri_g \gg 1$) or rapid rotation (low Rossby number, $Ro \ll 1$), the turbulence becomes highly anisotropic and organized, for example, into quasi-two-dimensional "pancake" eddies or columnar vortices. The relationship between stress and strain becomes tensorial and cannot be captured by a single scalar eddy viscosity.

*   **Non-local Transport and Counter-Gradient Fluxes:** The gradient-diffusion model is local, assuming that the flux at a point depends only on the gradient at that point. This fails when transport is dominated by large, coherent structures that can carry fluid parcels over significant distances before mixing. This can lead to **counter-gradient fluxes**, where the net transport is *up* the mean gradient. For instance, powerful convective plumes rising from a mixed layer can overshoot into the stable thermocline above, carrying warm water into a region that is already warmer, resulting in a positive, or counter-gradient, heat flux where the down-gradient model would predict a negative one . Other examples include transport within submesoscale fronts, by [internal gravity waves](@entry_id:185206), or in double-diffusive regimes where the differing molecular diffusivities of heat and salt drive instabilities.

#### Beyond Diffusivity: Advective Parameterizations

The recognition that not all eddy effects are purely diffusive has led to more advanced parameterizations that distinguish between irreversible mixing and reversible stirring. A key example in ocean modeling is the separation of eddy effects on tracers into a diffusive part (**Redi scheme**) and an advective part (**Gent-McWilliams scheme**, or GM) .

To understand the distinction, one must consider the effect on the total tracer variance, $\int \frac{1}{2} \overline{C}^2 dV$. A true diffusive process, by its nature, is irreversible and must always act to decrease tracer variance (i.e., smooth out gradients). The **Redi parameterization**, which models down-gradient mixing along isopycnal (constant density) surfaces, is a true diffusivity in this sense. Its mathematical operator is symmetric and negative-definite, ensuring variance decay.

The **GM parameterization**, however, represents the adiabatic stirring effect of eddies, which tends to flatten isopycnal surfaces. It is formulated as an additional advection by an "eddy-induced" or **bolus velocity**. An advective process, by itself, does not dissipate variance; it merely rearranges the tracer field. Mathematically, the GM operator is skew-symmetric, a property that guarantees it makes zero net contribution to the change in total tracer variance. Therefore, although the GM coefficient has units of diffusivity ($\mathrm{m}^2\mathrm{s}^{-1}$), it is fundamentally not a diffusivity but an advection. These two processes—the irreversible mixing of Redi and the reversible slumping of isopycnals by GM—are physically distinct, and their separation represents a significant conceptual advance over the simple eddy diffusivity model.