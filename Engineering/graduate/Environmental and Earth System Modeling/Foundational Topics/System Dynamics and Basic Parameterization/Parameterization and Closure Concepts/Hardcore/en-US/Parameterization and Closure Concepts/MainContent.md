## Introduction
Earth system models are indispensable tools for understanding and predicting the behavior of our planet's climate. These complex numerical simulations solve the fundamental equations of fluid motion, chemistry, and biology on a computational grid. However, a critical limitation arises from this discretization: processes occurring at scales smaller than the grid cell—from the turbulent eddies that mix the ocean to the formation of individual cloud droplets—cannot be explicitly resolved. Yet, the cumulative effect of these **subgrid-scale** processes is crucial for the large-scale dynamics of the entire system.

This gap between resolved and unresolved scales gives rise to one of the most persistent and foundational challenges in computational science: the **closure problem**. The core of this issue lies in representing the net impact of the unresolved, subgrid-scale world using only the information available at the resolved, grid scale. This process of representation is known as **parameterization**.

This article provides a comprehensive exploration of parameterization and closure concepts, designed for graduate-level study. Over the next three chapters, you will delve into this critical topic.
- **Principles and Mechanisms** will unpack the mathematical origins of the closure problem, introduce foundational concepts like the [eddy viscosity hypothesis](@entry_id:1124144), and explore key theoretical frameworks such as the TKE budget and Monin-Obukhov Similarity Theory.
- **Applications and Interdisciplinary Connections** will demonstrate the practical application of these principles across diverse domains, including atmospheric cloud microphysics, ocean eddy transport, and land-[biosphere](@entry_id:183762) interactions, revealing the unifying nature of the closure challenge.
- **Hands-On Practices** will provide opportunities to apply these concepts through guided problems, solidifying your understanding by calculating fluxes and comparing different closure assumptions.

By progressing through these chapters, you will gain a deep, functional understanding of why parameterization is necessary, how different closure schemes are developed and justified, and where the frontiers of this vital research area lie.

## Principles and Mechanisms

The governing equations of fluid motion, while comprehensive, describe phenomena across a [continuous spectrum](@entry_id:153573) of spatial and temporal scales. In Earth system modeling, computational constraints necessitate a discretization of these equations onto a grid, introducing a fundamental division: processes that are resolved by the grid and those that are unresolved, or **subgrid-scale**. The influence of these subgrid-scale processes on the resolved flow cannot be ignored, as they are responsible for [critical energy](@entry_id:158905) transformations and transport. **Parameterization** is the procedure of representing the net effect of these unresolved processes in terms of the resolved-scale variables. The central challenge in this endeavor is the **closure problem**, a direct consequence of applying scale-separation techniques to [nonlinear systems](@entry_id:168347).

### The Closure Problem: A Consequence of Averaging Nonlinearity

To formalize the [separation of scales](@entry_id:270204), we introduce a filtering or averaging operator, denoted by $\overline{(\cdot)}$. This operator can represent an ensemble average, as in Reynolds-Averaged Navier-Stokes (RANS) modeling, or a spatial low-pass filter with a characteristic width $\Delta$, as in Large Eddy Simulation (LES). The operator effectively filters out motions smaller than a certain scale, leaving behind the resolved field, $\overline{\phi}$.

Consider the conservation law for a scalar quantity $\phi(\boldsymbol{x},t)$, such as temperature or the concentration of a chemical tracer, being transported by a velocity field $\boldsymbol{u}(\boldsymbol{x},t)$:
$$
\frac{\partial \phi}{\partial t} + \nabla \cdot (\boldsymbol{u}\phi) = S_{\text{lin}}(\phi) + S_{\text{ext}}
$$
Here, $S_{\text{lin}}(\phi)$ represents linear processes, such as molecular diffusion (e.g., $\kappa \nabla^2 \phi$), and $S_{\text{ext}}$ represents external sources or sinks.

Applying the filter operator to this equation, and assuming the operator is linear and commutes with derivatives, we obtain:
$$
\frac{\partial \overline{\phi}}{\partial t} + \nabla \cdot \overline{(\boldsymbol{u}\phi)} = \overline{S_{\text{lin}}(\phi)} + \overline{S_{\text{ext}}}
$$
The difficulty arises from the [nonlinear advection](@entry_id:1128854) term, $\nabla \cdot (\boldsymbol{u}\phi)$. Because the filter is linear, we can write $\overline{S_{\text{lin}}(\phi)} = S_{\text{lin}}(\overline{\phi})$. For instance, $\overline{\kappa \nabla^2 \phi} = \kappa \nabla^2 \overline{\phi}$. If the governing equation were entirely linear, the filtered equation would be expressed solely in terms of filtered variables and would thus be **closed** .

However, for the [nonlinear advection](@entry_id:1128854) term, the average of a product is not equal to the product of the averages:
$$
\overline{\boldsymbol{u}\phi} \neq \overline{\boldsymbol{u}}\,\overline{\phi}
$$
This inequality is the fundamental origin of the closure problem. To form a prognostic equation for the resolved field $\overline{\phi}$, we must rearrange the filtered advection term:
$$
\nabla \cdot \overline{(\boldsymbol{u}\phi)} = \nabla \cdot (\overline{\boldsymbol{u}}\,\overline{\phi}) + \nabla \cdot (\overline{\boldsymbol{u}\phi} - \overline{\boldsymbol{u}}\,\overline{\phi})
$$
The filtered conservation equation thus becomes:
$$
\frac{\partial \overline{\phi}}{\partial t} + \nabla \cdot (\overline{\boldsymbol{u}}\,\overline{\phi}) = S_{\text{lin}}(\overline{\phi}) + \overline{S_{\text{ext}}} - \nabla \cdot \boldsymbol{\tau}_{\phi}
$$
where
$$
\boldsymbol{\tau}_{\phi} \equiv \overline{\boldsymbol{u}\phi} - \overline{\boldsymbol{u}}\,\overline{\phi}
$$
is the **subgrid-scale (SGS) flux** or **[turbulent flux](@entry_id:1133512)**. This term represents the transport of the scalar $\phi$ by the unresolved motions. Since it contains correlations between unresolved quantities (e.g., in RANS, if we let $\phi = \overline{\phi} + \phi'$ and $\boldsymbol{u} = \overline{\boldsymbol{u}} + \boldsymbol{u}'$, then $\boldsymbol{\tau}_{\phi} = \overline{\boldsymbol{u}'\phi'}$), it cannot be calculated directly from the resolved fields $\overline{\phi}$ and $\overline{\boldsymbol{u}}$. The closure problem is the challenge of finding a model, or **parameterization**, for this unclosed term as a function of the resolved variables .

Furthermore, in practical applications on variable-resolution grids or curved geometries, the assumption that the filter operator commutes with [spatial derivatives](@entry_id:1132036) may break down. This can introduce additional **commutation errors** that also require parameterization, distinct from the subgrid-scale terms arising from nonlinearity .

### First-Order Closure and the Eddy Viscosity/Diffusivity Hypothesis

The most direct and widely used approach to the closure problem is **first-order closure**, which postulates that the [turbulent flux](@entry_id:1133512) is proportional to the gradient of the mean quantity, in analogy to [molecular diffusion](@entry_id:154595).

For momentum transport, the unclosed term is the Reynolds stress tensor, $\tau_{ij} = \overline{u_i'u_j'}$. The **Boussinesq hypothesis** relates the anisotropic part of this tensor to the mean [rate-of-strain tensor](@entry_id:260652), $S_{ij} = \frac{1}{2} (\partial_j \overline{u_i} + \partial_i \overline{u_j})$:
$$
\overline{u_i' u_j'} - \frac{2}{3}k\delta_{ij} = -2\nu_t S_{ij}
$$
Here, $k \equiv \frac{1}{2}\overline{u_l'u_l'}$ is the turbulent kinetic energy (TKE), $\delta_{ij}$ is the Kronecker delta, and $\nu_t$ is the **eddy viscosity**, a parameter representing the diffusivity of momentum by turbulence . The term $\frac{2}{3}k\delta_{ij}$ represents the isotropic part of the stress.

This model is appealing in its simplicity. For a [simple shear flow](@entry_id:1131665) with [mean velocity](@entry_id:150038) $U(z)$ in the x-direction, it predicts a momentum flux $\overline{u'w'} = -\nu_t \frac{\partial U}{\partial z}$, representing a physically intuitive down-gradient transfer of momentum. However, the Boussinesq hypothesis has a profound limitation: it assumes the eddy viscosity $\nu_t$ is a scalar, which forces the principal axes of the Reynolds stress tensor to be aligned with those of the mean strain-rate tensor. It also predicts that the normal stresses are equal (i.e., $\overline{u'^2} = \overline{v'^2} = \overline{w'^2} = \frac{2}{3}k$), implying [isotropic turbulence](@entry_id:199323). In many geophysical flows, such as those near boundaries or under stable stratification, turbulence is strongly anisotropic, a feature this model cannot capture by design .

Similarly, for a scalar $\phi$, the [turbulent flux](@entry_id:1133512) is modeled using an **eddy diffusivity** $K_{\phi}$:
$$
\overline{u_i'\phi'} = -K_{\phi} \frac{\partial \overline{\phi}}{\partial x_i}
$$
This is often referred to as a **K-theory** or **gradient-diffusion** model.

### Determining the Eddy Viscosity: Energetic and Scale Arguments

First-order closures shift the problem from modeling the unknown flux to modeling the unknown eddy viscosity $\nu_t$ (or diffusivity $K_\phi$). This can be accomplished through various levels of complexity.

#### The Turbulent Kinetic Energy Budget

A more physically comprehensive approach is to derive a prognostic equation for the turbulent kinetic energy (TKE), $k$. By manipulating the Navier-Stokes equations, one can derive the exact TKE budget equation. For an incompressible fluid under the Boussinesq approximation, this equation takes the form :
$$
\frac{\partial k}{\partial t} + \bar{u}_j \frac{\partial k}{\partial x_j} = -\overline{u_i' u_j'}\frac{\partial \bar{u}_i}{\partial x_j} + \beta\overline{w' \theta'} - \varepsilon - \frac{\partial}{\partial x_j}\left(\frac{\overline{u_j' p'}}{\rho_0} + \frac{1}{2}\overline{u_i' u_i' u_j'} - \nu\frac{\partial k}{\partial x_j}\right)
$$
The terms on the right-hand side represent:
1.  **Shear Production ($P$):** $-\overline{u_i' u_j'}\frac{\partial \bar{u}_i}{\partial x_j}$, the rate at which TKE is extracted from the mean flow shear.
2.  **Buoyancy Production/Destruction ($B$):** $\beta\overline{w' \theta'}$, where $\beta$ is the buoyancy parameter. This term generates TKE in unstable stratification (upward heat flux) and destroys it in stable stratification.
3.  **Viscous Dissipation ($\varepsilon$):** $\varepsilon = \nu\overline{\frac{\partial u_i'}{\partial x_j}\frac{\partial u_i'}{\partial x_j}}$, the rate at which TKE is converted to internal energy by molecular viscosity.
4.  **Transport ($T$):** The divergence term, which represents the spatial redistribution of TKE by turbulent pressure fluctuations, velocity fluctuations (triple correlations), and molecular diffusion.

This equation reveals the energetic pathways of turbulence, but it does not solve the closure problem. In fact, it introduces new, higher-order unclosed terms: the Reynolds stress in the production term, the turbulent heat flux, the dissipation rate, and the turbulent and pressure transport terms. In a **one-equation closure**, one models these new terms to solve prognostically for $k$. The eddy viscosity can then be related to TKE and a characteristic length scale $l_m$ (the mixing length), e.g., $\nu_t \propto \sqrt{k} \cdot l_m$.

#### Scaling Arguments in Large Eddy Simulation

In LES, the filter scale $\Delta$ provides a natural length scale for closure. The **Smagorinsky model** is a classic example, founded on the assumption that the unresolved scales are in a state of local equilibrium, where the production of subgrid TKE is balanced by its dissipation. On dimensional grounds, the eddy viscosity $\nu_t$ must be constructed from the filter width $\Delta$ (units of length) and a characteristic velocity gradient of the smallest resolved eddies, captured by the magnitude of the resolved [strain-rate tensor](@entry_id:266108), $|\tilde{S}| = \sqrt{2\tilde{S}_{ij}\tilde{S}_{ij}}$ (units of inverse time). This leads to the model :
$$
\nu_t = (C_s \Delta)^2 |\tilde{S}|
$$
Here, $C_s$ is the dimensionless **Smagorinsky constant**. This constant is not arbitrary; it can be derived theoretically by assuming the filtered scales lie within an [inertial subrange](@entry_id:273327) described by Kolmogorov's [energy spectrum](@entry_id:181780), $E(k) = C_K \varepsilon^{2/3} k^{-5/3}$. By demanding that the mean subgrid-scale dissipation predicted by the model, $\langle -\tau_{ij} \tilde{S}_{ij} \rangle$, equals the true mean [energy cascade](@entry_id:153717) rate $\varepsilon$, one can derive an expression for $C_s$ in terms of the Kolmogorov constant $C_K$, establishing a link between the parameterization and fundamental [turbulence theory](@entry_id:264896) .

### Case Studies in Geophysical Parameterization

The abstract principles of closure find concrete application in a wide array of geophysical phenomena.

#### The Atmospheric Surface Layer and Monin-Obukhov Similarity

The [atmospheric surface layer](@entry_id:1121210)—the lowest tens of meters of the atmosphere—is characterized by strong vertical gradients and turbulence that is strongly influenced by surface friction and heat flux. **Monin-Obukhov Similarity Theory (MOST)** provides a powerful framework for parameterizing fluxes in this region. MOST posits that the structure of turbulence, when non-dimensionalized by appropriate surface-layer scales, is a universal function of a single stability parameter, $\zeta$.

The key scaling parameters are the **[friction velocity](@entry_id:267882)** $u_* = \sqrt{-\overline{u'w'}|_s}$ and the characteristic temperature scale $\theta_* = -\overline{w'\theta'_v}|_s / u_*$, derived from the surface fluxes of momentum and [virtual potential temperature](@entry_id:1133825). These combine with gravity to form the **Monin-Obukhov length** :
$$
L = -\frac{u_*^3}{\kappa g (\overline{w'\theta'_v}/\theta_v)}
$$
where $\kappa$ is the von Kármán constant. The length scale $|L|$ has a profound physical meaning: it is the approximate height at which the shear production of TKE becomes comparable to the buoyancy production/destruction . The sign of $L$ indicates stability: $L  0$ for unstable (convective) conditions, $L > 0$ for stable conditions, and $|L| \to \infty$ for neutral conditions.

The dimensionless stability parameter $\zeta = z/L$ relates the height $z$ to this stability scale. According to MOST, the dimensionless wind shear and temperature gradient are universal functions of $\zeta$:
$$
\frac{\kappa z}{u_*} \frac{\partial U}{\partial z} = \phi_m(\zeta) \quad \text{and} \quad \frac{\kappa z}{\theta_*} \frac{\partial \Theta_v}{\partial z} = \phi_h(\zeta)
$$
The functions $\phi_m$ and $\phi_h$ are empirical **stability functions**. In neutral conditions ($\zeta \to 0$), $\phi_m, \phi_h \to 1$, recovering the classic logarithmic profiles. In stable conditions ($\zeta > 0$), turbulence is suppressed, mixing is inefficient, and $\phi_m, \phi_h > 1$. In unstable conditions ($\zeta  0$), turbulent mixing is enhanced by buoyancy, and $\phi_m, \phi_h  1$ .

#### The Convective Boundary Layer and Nonlocal Closure

While K-theory is useful in many contexts, it fails spectacularly in the daytime **Convective Boundary Layer (CBL)**. A CBL is characterized by strong surface heating that drives large, coherent thermal plumes. These plumes transport heat from the surface upward through the mixed layer. Within the bulk of this mixed layer, vigorous mixing leads to a nearly uniform mean potential temperature profile, $\partial\overline{\theta}/\partial z \approx 0$.

A local gradient-diffusion model, $\overline{w'\theta'} = -K_h \partial\overline{\theta}/\partial z$, would predict zero heat flux in this region. However, observations and simulations show a significant upward heat flux throughout most of the mixed layer. In fact, near the top of the CBL, [entrainment](@entry_id:275487) of warmer air from the free troposphere above can create a weakly stable gradient ($\partial\overline{\theta}/\partial z > 0$) co-existing with an upward heat flux ($\overline{w'\theta'} > 0$) . This phenomenon, where [turbulent flux](@entry_id:1133512) is directed against the mean gradient, is known as **[counter-gradient flux](@entry_id:1123121)**.

This constitutes a fundamental failure of local [closure models](@entry_id:1122505). For the equality $\overline{w'\theta'} = -K_h \partial\overline{\theta}/\partial z$ to hold in this case, the eddy diffusivity $K_h$ would have to be negative, a physically untenable result implying "un-mixing." The physical reason for this failure is that the transport is **nonlocal**: the properties of the large thermal plumes responsible for the flux are determined by their origin near the surface, not by the local gradient at their current height.

To address this, **nonlocal closure** schemes are required. These can take the form of an added counter-gradient term, e.g., $\overline{w'\theta'} = -K_h(\partial\overline{\theta}/\partial z - \gamma)$, where $\gamma$ represents the nonlocal flux driven by large eddies. This is not merely a mathematical fix; it has critical energetic implications. The upward transport of heat is the primary source of TKE that fuels mixing and drives entrainment at the boundary layer top. A local K-theory model, by incorrectly predicting near-zero flux in the mixed layer, starves the [entrainment](@entry_id:275487) process of energy and severely under-predicts boundary layer growth .

#### Moist Convection and Mass-Flux Schemes

Moist convection, such as in thunderstorms, occurs on scales far too small to be resolved by global climate models. Its parameterization is one of the most challenging aspects of climate modeling. Instead of viewing subgrid transport as a diffusive process, **[mass-flux parameterization](@entry_id:1127657)** schemes represent convection as an ensemble of distinct updrafts and downdrafts embedded within a slowly-varying environment.

The core of this approach is the bulk [plume model](@entry_id:1129836). For a single updraft plume, we define its mass flux $M(z) = \rho(z) a(z) w(z)$, where $a$ is the fractional area and $w$ is the vertical velocity. The plume exchanges mass with its environment through **[entrainment](@entry_id:275487)** (environmental air flowing into the plume) and **detrainment** (plume air flowing out). These are represented by fractional rates per unit height, $\epsilon(z)$ and $\delta(z)$. The mass budget for the plume is then :
$$
\frac{dM}{dz} = (\epsilon - \delta) M
$$
The budget for a conserved scalar $\chi$ (e.g., moist static energy) with mean value $\chi_c$ in the plume and $\chi_e$ in the environment is given by considering the fluxes into and out of a control volume:
$$
\frac{d}{dz}(M\chi_c) = \epsilon M \chi_e - \delta M \chi_c
$$
Expanding this and using the mass budget equation reveals the change in the plume's own properties: $M \frac{d\chi_c}{dz} = \epsilon M (\chi_e - \chi_c)$. This shows that the plume's scalar concentration is diluted by the [entrainment](@entry_id:275487) of environmental air. This framework provides a physically intuitive alternative to eddy diffusion for representing organized, buoyant transport .

### Overarching Principles in Parameterization Development

Beyond specific schemes, two overarching principles guide the development of robust parameterizations.

#### Conservation Constraints

Numerical models are built upon fundamental conservation laws. It is imperative that parameterized tendencies do not spuriously create or destroy conserved quantities like mass, momentum, energy, or total tracer amounts. The most reliable way to enforce conservation is to formulate parameterized tendencies in a **flux-[divergence form](@entry_id:748608)**. For a subgrid flux $\boldsymbol{F}_p$, the tendency $T_p = -\nabla \cdot \boldsymbol{F}_p$, when integrated over a domain with no-flux boundaries, vanishes by the divergence theorem.

Furthermore, budgets must be closed consistently. For example, the kinetic energy removed by a parameterized drag or turbulent stress must appear as a source of internal energy ([frictional heating](@entry_id:201286)) in the thermodynamic equation to conserve total energy. Similarly, for tracers undergoing [phase changes](@entry_id:147766) (e.g., water species), a sink in one category must be a source in another to conserve the total amount of the substance .

#### Structural vs. Parametric Uncertainty

Finally, it is crucial to distinguish two sources of error in parameterization. **Parametric uncertainty** refers to the uncertainty in the values of the parameters within a given model structure (e.g., the exact value of the Smagorinsky constant $C_s$ or an [entrainment](@entry_id:275487) rate $\epsilon$). These can be constrained, though not eliminated, through calibration with observations.

**Structural uncertainty**, on the other hand, arises from the choice of the model formulation itself—the underlying physical hypotheses. For example, one might model convection using a quasi-equilibrium adjustment scheme, where precipitation is a function of the thermodynamic instability (e.g., CAPE), or using a mass-flux scheme, where precipitation is tied to large-scale moisture convergence. These two schemes represent fundamentally different assumptions about what controls convection. It is often possible to tune the parameters of both schemes so that they produce the same output for a given set of conditions. This phenomenon, known as **equifinality**, does not mean the models are equivalent. It highlights structural uncertainty: our limited understanding of the system allows for multiple, plausible, and potentially contradictory hypotheses to co-exist, each capable of explaining a limited set of observations . Recognizing structural uncertainty is a hallmark of a mature understanding of Earth system modeling, reminding us that parameterizations are not just curve-fitting exercises but simplified expressions of physical hypotheses.