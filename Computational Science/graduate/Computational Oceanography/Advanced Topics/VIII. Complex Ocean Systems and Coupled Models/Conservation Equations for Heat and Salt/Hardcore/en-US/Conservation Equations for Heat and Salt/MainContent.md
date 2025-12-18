## Introduction
The distribution of heat and salt governs the ocean's density structure, drives global circulation, and fundamentally regulates Earth's climate. Understanding and predicting these patterns requires a robust framework built upon the physical laws of conservation. While the core concept is simple, its application to the dynamic oceanic environment is complex, involving the unique thermodynamic properties of seawater, the chaotic stirring of turbulent eddies, and the intricate exchanges at the ocean's boundaries. This article bridges the gap between abstract theory and practical application, providing a comprehensive guide to the conservation equations for heat and salt.

We will begin in "Principles and Mechanisms" by deriving the general [advection-diffusion equation](@entry_id:144002) and adapting it for the unique properties of oceanic heat and salt, introducing the modern and highly accurate TEOS-10 framework. Next, "Applications and Interdisciplinary Connections" will explore how these laws are applied to model real-world phenomena, from [air-sea fluxes](@entry_id:1120895) and eddy parameterizations to their relevance in fields beyond oceanography. Finally, "Hands-On Practices" will provide an opportunity to translate theory into practice, tackling common challenges in the numerical implementation of these foundational equations.

## Principles and Mechanisms

The transport and distribution of heat and salt are fundamental to the dynamics of the global ocean, shaping its circulation, stratification, and role in the Earth's climate system. Understanding the evolution of these properties requires a firm grasp of the underlying conservation laws that govern their behavior. This chapter details these principles, starting from the general conservation equation for a scalar tracer and progressively incorporating the physical mechanisms and thermodynamic intricacies specific to the oceanic environment.

### The General Conservation Equation for a Scalar Tracer

The evolution of any scalar concentration, denoted by $C(\mathbf{x}, t)$, within a fluid is governed by a fundamental conservation principle. We can describe this evolution from two perspectives: Eulerian and Lagrangian. The **Eulerian** perspective observes changes at a fixed point in space, $\mathbf{x}$, whereas the **Lagrangian** perspective follows the changes experienced by a moving fluid parcel along its trajectory, $\mathbf{X}(t)$. The rate of change experienced by the parcel is given by the **[material derivative](@entry_id:266939)**, which links these two viewpoints. Applying the [multivariable chain rule](@entry_id:146671), the [material derivative](@entry_id:266939) is defined as:

$$
\frac{DC}{Dt} = \frac{\partial C}{\partial t} + \mathbf{u} \cdot \nabla C
$$

Here, $\partial C/\partial t$ is the local (Eulerian) rate of change at a fixed point, and $\mathbf{u} \cdot \nabla C$ is the **advective** term, representing the change in concentration a parcel experiences by moving through a spatially varying field. 

The comprehensive statement of conservation, derived from the Reynolds [transport theorem](@entry_id:176504) for a fixed control volume, is expressed in differential form as:

$$
\frac{\partial C}{\partial t} + \nabla \cdot (\mathbf{u}C) = \nabla \cdot (\mathbf{F}_{\text{diff}}) + S_C
$$

This equation states that the local rate of change of a tracer concentration (the **local storage** term, $\partial C/\partial t$) is balanced by three processes :

1.  **Advective Flux Divergence**: The term $\nabla \cdot (\mathbf{u}C)$ represents the net transport of the tracer into or out of a point by the mean fluid velocity $\mathbf{u}$. Using the product rule, this can be expanded to $C(\nabla \cdot \mathbf{u}) + \mathbf{u} \cdot \nabla C$. For many oceanographic applications, the **Boussinesq approximation** is invoked, which assumes the fluid is [nearly incompressible](@entry_id:752387), such that $\nabla \cdot \mathbf{u} \approx 0$. Under this approximation, the [flux divergence](@entry_id:1125154) term simplifies to the familiar advection term, $\mathbf{u} \cdot \nabla C$. The conservation law then takes the advective form: $\frac{DC}{Dt} = \nabla \cdot (\mathbf{F}_{\text{diff}}) + S_C$. This shows that in an incompressible fluid, the concentration of a moving parcel changes only due to diffusion and sources/sinks. 

2.  **Diffusive Flux Divergence**: The term $\nabla \cdot (\mathbf{F}_{\text{diff}})$ represents the net transport of the tracer due to unresolved, typically small-scale, motions. This flux is commonly parameterized using a Fickian diffusion model, where the flux is proportional to the negative of the tracer gradient: $\mathbf{F}_{\text{diff}} = -\mathbf{K} \nabla C$. Here, $\mathbf{K}$ is the diffusivity tensor. The full term becomes $\nabla \cdot (\mathbf{K} \nabla C)$. This term accounts for mixing by both molecular processes and turbulent eddies.

3.  **Sources and Sinks**: The term $S_C$ represents any volumetric sources or sinks that create or destroy the tracer within the fluid itself, such as from chemical reactions or radiative absorption.

Combining these elements, the general [tracer conservation equation](@entry_id:1133277) under the Boussinesq approximation can be written as:

$$
\frac{\partial C}{\partial t} + \mathbf{u} \cdot \nabla C = \nabla \cdot (\mathbf{K} \nabla C) + S_C
$$

### Application to Salinity and Heat

While the general equation provides the template, its specific form and interpretation depend critically on the tracer in question. In oceanography, a tracer is considered **conservative** if its total amount within a material control volume changes only due to fluxes across the boundary, with no sources or sinks in the interior. 

#### Salinity Conservation

Salinity, as a [mass fraction](@entry_id:161575) of dissolved salts, is an archetypal [conservative tracer](@entry_id:1122920) in the ocean interior. There are no significant chemical or biological processes in the water column that produce or consume salt. Therefore, for salinity ($C=S$), the interior source/sink term is effectively zero: $S_S \approx 0$.

Changes in salinity are driven by fluxes of freshwater at the ocean's boundaries: evaporation, precipitation, river runoff, and the melting or freezing of sea ice. These processes are not interior sources or sinks but are treated as **boundary conditions**. In numerical models, for instance, a net surface freshwater flux is often implemented as a "virtual salt flux" in the top model layer to ensure salt conservation, but this is a numerical representation of a boundary process. 

#### Heat Conservation and the Thermodynamic Equation of Seawater (TEOS-10)

The conservation of "heat" is substantially more complex than that of salt. A common misconception is that in-situ temperature ($T$) is a [conservative tracer](@entry_id:1122920). This is not the case, primarily due to the effects of pressure. As a water parcel moves vertically, it undergoes [adiabatic compression](@entry_id:142708) or expansion, which changes its in-situ temperature even without any heat being added or removed. This pressure-work effect means $T$ is not materially conserved. 

To address this, oceanographers have historically used **potential temperature ($\theta$)**, defined as the temperature a parcel would have if moved adiabatically to a reference pressure (usually the sea surface, $p_0=0$ dbar). While $\theta$ removes the large, reversible temperature changes due to pressure, it is still not a perfectly conservative variable, especially with respect to mixing.

The modern and most accurate framework for seawater thermodynamics is the **Thermodynamic Equation of Seawater 2010 (TEOS-10)**. This framework introduces variables that are truly conservative.

-   **Absolute Salinity ($S_A$)**: This is the mass fraction of dissolved inorganic material in seawater. It provides a more accurate measure of salt content than older, conductivity-based Practical Salinity, as it accounts for variations in seawater composition.

-   **Conservative Temperature ($\Theta$)**: This is the variable representing heat content in TEOS-10. It is defined to be directly proportional to **potential enthalpy ($h^0$)**, which is the specific enthalpy a parcel would have if moved isentropically to the reference pressure $p_0$. The defining relation is $\Theta = h^0 / c_p^0$, where $c_p^0$ is a chosen constant reference heat capacity. 

The superiority of $\Theta$ over $\theta$ lies in its conservation properties. The [first law of thermodynamics](@entry_id:146485) shows that for an idealized adiabatic and [reversible process](@entry_id:144176), potential enthalpy is materially conserved ($Dh^0/Dt = 0$). Because $\Theta$ is linearly proportional to $h^0$, it follows that $D\Theta/Dt = 0$. In contrast, potential temperature $\theta$ is not strictly conserved under the same conditions ($D\theta/Dt \neq 0$) because the specific heat capacity of seawater ($c_p$) is a function of temperature, salinity, and pressure. The non-linearity in $c_p$ means that $\theta$ is not a linear function of the conserved quantity, enthalpy. 

Therefore, for accurate heat conservation, especially in compressible, non-Boussinesq models or models involving [phase changes](@entry_id:147766) like sea ice formation, the prognostic variable should be an enthalpy-based quantity like $\Theta$. In-situ temperature is then diagnosed from the prognostic values of $\Theta$, $S_A$, and pressure. 

Furthermore, unlike salinity, heat has true volumetric sources. While surface exchanges of sensible and latent heat are boundary conditions, incoming shortwave solar radiation penetrates the surface and is absorbed over depth, acting as an interior source term ($S_\Theta > 0$) in the upper ocean. Geothermal heating from the seafloor and [viscous dissipation](@entry_id:143708) of kinetic energy are also small but non-zero interior heat sources. 

### The Physics of Mixing

The [diffusive flux](@entry_id:748422) term $\nabla \cdot (\mathbf{K} \nabla C)$ encompasses a range of physical processes that mix heat and salt, spanning from the molecular scale to the scale of large ocean eddies.

#### Molecular vs. Turbulent Diffusion

At the smallest scales, mixing is driven by the random motion of molecules. The molecular diffusivity of heat in seawater ($\kappa_T \approx 1.4 \times 10^{-7} \, \mathrm{m}^2\,\mathrm{s}^{-1}$) is about two orders of magnitude greater than the molecular diffusivity of salt ($\kappa_S \approx 1.0 \times 10^{-9} \, \mathrm{m}^2\,\mathrm{s}^{-1}$).

However, in the vast and energetic ocean, the dominant mixing agent is **turbulence** generated by instabilities in the flow. In large-scale ocean models, the effects of unresolved turbulent eddies are parameterized as an **eddy diffusion** process. The corresponding eddy diffusivity, $K_{\text{eddy}}$, is vastly larger than molecular diffusivity. For vertical mixing in the ocean interior, a typical value is $K_{\text{eddy}} \approx 3 \times 10^{-5} \, \mathrm{m}^2\,\mathrm{s}^{-1}$.

A simple comparison shows the overwhelming dominance of turbulent mixing for the mean tracer budget. The ratio of vertical molecular flux to vertical eddy flux is given by the ratio of their diffusivities, $\kappa_{\text{mol}} / K_{\text{eddy}}$. For heat, this ratio is approximately $4.67 \times 10^{-3}$, and for salt, it is a mere $3.33 \times 10^{-5}$.  This vast [separation of scales](@entry_id:270204) justifies the common practice in large-scale models of neglecting [molecular diffusion](@entry_id:154595) in the governing equations for the mean fields.

#### Double Diffusion

Despite its weakness, [molecular diffusion](@entry_id:154595) can play a crucial role in specific circumstances through a process known as **double diffusion**. This phenomenon can lead to instability even in a fluid column that is, on average, stably stratified. It arises because heat diffuses much faster than salt ($\kappa_T \gg \kappa_S$). Two primary forms exist:

1.  **Salt Fingering**: This occurs in regions where warm, salty water overlies cooler, fresher water ($T_z > 0$, $S_z > 0$, where $z$ is height). If a parcel is displaced downward, it is initially warmer and saltier than its surroundings. It rapidly loses its excess heat to the environment but retains its excess salt. This makes the parcel denser than its surroundings, causing it to sink further and creating long, thin "fingers" of sinking fluid. This instability requires the overall stratification to be stable (i.e., the stabilizing effect of temperature outweighs the destabilizing effect of salt). 

2.  **Diffusive Layering**: This occurs where cool, fresh water overlies warm, salty water ($T_z  0$, $S_z  0$). If a parcel is displaced downward, it is cooler and fresher than its surroundings. It rapidly gains heat from the environment, but only slowly gains salt. This makes the parcel less dense than its new surroundings, causing it to rise, often overshooting its original position. This process can organize the fluid into a series of well-mixed convective layers separated by sharp, diffusive interfaces. 

### Anisotropic Mixing in a Stratified Ocean

Turbulent mixing in the ocean is highly **anisotropic** (direction-dependent). Due to stable density stratification, it is energetically far easier for fluid motions to stir properties along surfaces of constant density (**isopycnals**) than across them. Moving a fluid parcel across isopycnals requires work against the buoyancy force, which strongly suppresses vertical motion. This is particularly true for the large, geostrophically balanced [mesoscale eddies](@entry_id:1127814) that dominate ocean transport, which are characterized by small Rossby ($Ro \ll 1$) and Froude ($Fr \ll 1$) numbers. Their motion is overwhelmingly quasi-horizontal, following isopycnal surfaces. 

To represent this physical reality in models, the scalar diffusivity $K$ is replaced by a second-order **diffusion tensor $\mathbf{K}$**. This tensor is constructed to apply a large diffusivity, $K_{iso}$, along isopycnal surfaces and a much smaller diffusivity, $K_{dia}$, across them (**diapycnal** mixing). If $\mathbf{n}$ is the unit vector normal to the local isopycnal surface, the tensor can be expressed as:

$$
\mathbf{K} = K_{iso}(\mathbf{I} - \mathbf{n}\mathbf{n}^T) + K_{dia}\mathbf{n}\mathbf{n}^T
$$

where $\mathbf{I}$ is the identity tensor, and the terms $(\mathbf{I} - \mathbf{n}\mathbf{n}^T)$ and $\mathbf{n}\mathbf{n}^T$ are [projection operators](@entry_id:154142) onto the isopycnal and diapycnal directions, respectively. In this framework, the diffusive flux $\mathbf{F}_{\text{diff}} = -\mathbf{K}\nabla C$ is preferentially aligned along isopycnals. 

For the diffusive process to be physically realistic, it must be dissipative—that is, it must always act to reduce tracer gradients and decrease tracer variance. This imposes a mathematical constraint on the diffusion tensor: $\mathbf{K}$ must be **symmetric and [positive semi-definite](@entry_id:262808)**. This ensures that the rate of change of total tracer variance, $\frac{d}{dt}\int \frac{1}{2}C^2 dV$, is always less than or equal to zero. 

### Effects of a Non-linear Equation of State

The final layer of complexity in heat and salt conservation arises from the fact that the [equation of state for seawater](@entry_id:1124595), $\rho = \rho(S_A, \Theta, p)$, is non-linear. This nonlinearity gives rise to two important phenomena that can cause density changes even when mixing appears to conserve density.

-   **Cabbeling**: This is the process where the mixing of two water parcels with the same density, but different temperature and salinity properties, results in a mixture that is denser than the original parcels. A Taylor [series expansion](@entry_id:142878) of the equation of state shows that this density increase, $\Delta\rho_{\text{cab}}$, is a result of the second-order (curvature) terms in the EOS. Geometrically, isopycnals in T-S space are curved, and the straight line connecting two points on an isopycnal passes through a region of higher density. 

-   **Thermobaricity**: This refers to the pressure dependence of the thermodynamic coefficients, particularly the [thermal expansion coefficient](@entry_id:150685) ($\alpha$) and the haline contraction coefficient ($\beta$). Because these coefficients change with pressure, isopycnal surfaces are not parallel but tilt relative to each other with depth. Consequently, mixing two water parcels that lie on the same neutral surface but at different pressures can result in a mixture with a different density. This effect is captured by cross-derivative terms in the Taylor expansion of the EOS, such as $\rho_{Tp} = \partial^2\rho/\partial T \partial p$. 

These nonlinear effects underscore the importance of using thermodynamically consistent variables. As Conservative Temperature ($\Theta$) is proportional to potential enthalpy, it is a linearly mixing quantity. When two parcels mix, the $\Theta$ of the mixture is the mass-weighted average of the initial values. In contrast, potential temperature ($\theta$) does not mix linearly due to the [non-linearity](@entry_id:637147) of heat capacity. This means that mixing processes like [cabbeling](@entry_id:1121979) act as a source or sink for $\theta$, but not for $\Theta$. This provides another compelling reason for the adoption of the TEOS-10 framework in modern ocean modeling. 