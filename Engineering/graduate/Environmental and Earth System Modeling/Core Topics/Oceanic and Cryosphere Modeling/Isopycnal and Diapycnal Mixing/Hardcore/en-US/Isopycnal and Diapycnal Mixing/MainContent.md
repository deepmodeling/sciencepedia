## Introduction
The transport of heat, salt, and biogeochemical tracers throughout the world's oceans is fundamental to the Earth's climate system. This transport is accomplished by a combination of large-scale advection and smaller-scale mixing. A crucial concept in physical oceanography is that this mixing is highly anisotropic: it occurs far more easily along surfaces of constant density than across them. This distinction gives rise to two critical processes: **[isopycnal mixing](@entry_id:1126775)** (along-density) and **[diapycnal mixing](@entry_id:1123661)** (across-density). Understanding the disparate mechanisms, energetics, and scales that govern these two modes of transport, and how to represent them in models, is a central challenge in ocean and climate science.

This article provides a comprehensive exploration of [anisotropic mixing](@entry_id:1121023). The first chapter, **"Principles and Mechanisms,"** delves into the fundamental physics, defining the density surfaces that form the [natural coordinate system](@entry_id:168947) for mixing, the role of stratification, and the energetic frameworks like the Osborn model that govern diapycnal transport. It also contrasts this with the vigorous eddy-driven nature of [isopycnal mixing](@entry_id:1126775). The second chapter, **"Applications and Interdisciplinary Connections,"** examines how these principles are implemented as parameterizations in numerical climate models and explores their profound impact on large-scale ocean circulation, the maintenance of the thermocline, and crucial [biogeochemical cycles](@entry_id:147568). Finally, the **"Hands-On Practices"** section provides an opportunity to engage directly with key theoretical and modeling concepts through guided problems.

## Principles and Mechanisms

The transport and distribution of heat, salt, carbon, and other biogeochemical tracers in the ocean are governed by a combination of advection by the large-scale circulation and mixing by smaller-scale, typically turbulent, processes. A foundational principle in [physical oceanography](@entry_id:1129648) is that this mixing is profoundly **anisotropic**. In a stably [stratified fluid](@entry_id:201059) like the ocean, it is energetically far easier to stir properties along surfaces of constant density than it is to mix them across these surfaces. This gives rise to two distinct modes of turbulent transport: **[isopycnal mixing](@entry_id:1126775)**, which occurs along surfaces of constant density, and **diapycnal mixing**, which occurs across them. Understanding the principles and mechanisms that govern these two modes of mixing is essential for accurately modeling the ocean's structure, circulation, and role in the global climate system.

### The Coordinate System of Mixing: Density Surfaces and Stratification

To properly describe oceanic mixing, we must first define the surfaces along which and across which it occurs. The strong gravitational stratification of the ocean makes density the natural vertical coordinate for analyzing fluid parcel movement and mixing.

#### Density, Potential Density, and Neutral Surfaces

The local or **in situ density** of seawater, denoted $\rho(S, T, p)$, is a complex, nonlinear function of salinity ($S$), in situ temperature ($T$), and pressure ($p$). Because seawater is compressible, in situ density increases significantly with depth due to pressure alone. This makes it unsuitable for comparing the intrinsic density of water parcels from different depths. To overcome this, oceanographers use **[potential density](@entry_id:1129991)**, denoted $\rho_{\theta}$. This is the density a parcel would have if it were moved adiabatically (without exchange of heat or salt) from its in situ pressure to a common reference pressure, $p_0$. The temperature it would attain at $p_0$ is its **potential temperature**, $\theta$. The potential density is then $\rho_{\theta} = \rho(S, \theta, p_0)$. A commonly used quantity is the **potential density anomaly**, $\sigma_{\theta} = \rho_{\theta} - 1000 \, \mathrm{kg\,m^{-3}}$. 

A surface of constant potential density is known as an **isopycnal surface**. While conceptually useful, these surfaces are not perfectly "neutral." A truly **neutral displacement** is one for which a fluid parcel, when moved infinitesimally, remains neutrally buoyant relative to its new surroundings. The set of all such displacement vectors at a point defines the **neutral [tangent plane](@entry_id:136914)**. An **isoneutral surface** is the surface that is everywhere tangent to this plane. 

Isopycnal and isoneutral surfaces do not perfectly coincide. The discrepancy arises from the nonlinearity of the equation of state, particularly the pressure dependence of the [thermal expansion](@entry_id:137427) and haline contraction coefficients—an effect known as **thermobaricity**. As a result, moving a parcel along a surface of constant potential density (an isopycnal) can generate a small buoyant restoring force. While often small, this misalignment is critical for accurately modeling [tracer transport](@entry_id:1133278) over large vertical and horizontal scales. To address this, ocean models often use more sophisticated density variables, such as **neutral density** ($\gamma^n$), which is constructed to be a scalar whose gradient is, as closely as possible, parallel to the local neutral vector. This allows the [diffusion tensor](@entry_id:748421) in a model to be aligned more accurately with the true neutral direction, minimizing spurious numerical diapycnal mixing. A complementary variable, **spiciness**, can be constructed to describe variations in temperature and salinity along these neutral surfaces. 

#### Quantifying Stratification: The Buoyancy Frequency

The "energetic cost" of [diapycnal mixing](@entry_id:1123661) is directly related to the strength of the vertical density stratification. The fundamental measure of this is the **Brunt–Väisälä frequency**, or **[buoyancy frequency](@entry_id:1121933)**, $N$. Its square, $N^2$, is defined from the restoring force on a fluid parcel displaced vertically in a density gradient. For a parcel displaced vertically by a small distance $\eta$ from its [equilibrium position](@entry_id:272392), the net buoyancy acceleration is $a = -(N^2)\eta$. This describes [simple harmonic motion](@entry_id:148744) with a frequency $N$. The formal definition is:

$$
N^2 = -\frac{g}{\rho_0} \frac{\partial \rho}{\partial z}
$$

where $g$ is the acceleration due to gravity, $\rho_0$ is a reference density, and $z$ is the vertical coordinate (positive upward). For a statically stable water column, density must decrease with height, so $\partial \rho / \partial z  0$ and $N^2 > 0$. If $N^2  0$, the water column is gravitationally unstable and will overturn. The buoyancy frequency is therefore the intrinsic frequency of vertical oscillations in a stratified fluid and represents the fundamental timescale for internal dynamics. It sets the upper frequency limit for freely propagating **[internal gravity waves](@entry_id:185206)**, which play a crucial role in mediating energy transport for mixing. 

### Diapycnal Mixing: Crossing the Density Barrier

Diapycnal mixing involves the irreversible transport of fluid parcels across isopycnal surfaces. This process requires work to be done against the stabilizing [buoyancy force](@entry_id:154088), thereby increasing the potential energy of the water column. This energy must be supplied by the dissipation of [turbulent kinetic energy](@entry_id:262712).

#### The Energetics of Stratified Turbulence

In a region of stationary, homogeneous, [stratified turbulence](@entry_id:1132493), the turbulent kinetic energy (TKE) budget simplifies to a balance between production and destruction. TKE is typically produced by shear in the mean flow ($P$) and is lost to two primary sinks: conversion into potential energy by working against buoyancy (the [buoyancy flux](@entry_id:261821), $B$) and [viscous dissipation](@entry_id:143708) into heat ($\varepsilon$). The budget is:

$$
P = B + \varepsilon
$$

The **buoyancy flux** $B = \overline{w'b'}$ represents the rate of work done by turbulent vertical velocity fluctuations ($w'$) against buoyancy fluctuations ($b' = -g\rho'/\rho_0$). This term represents an energy conversion from kinetic to potential form. The **flux Richardson number**, $R_f = B/P$, quantifies the fraction of TKE production that is diverted to buoyancy flux. The **mixing efficiency**, often denoted $\Gamma$, is a crucial parameter that relates the [buoyancy flux](@entry_id:261821) to the [dissipation rate](@entry_id:748577). A common definition is $\Gamma = B/\varepsilon$, which represents the ratio of energy gained by the potential energy field to that lost to viscosity. Using the TKE budget, these quantities are related by $R_f = \Gamma / (1 + \Gamma)$. 

It is critical to distinguish between the total buoyancy flux, which may include reversible parcel motions associated with [internal waves](@entry_id:261048), and the *irreversible* component that leads to a permanent change in the background potential energy. True [diapycnal mixing](@entry_id:1123661) is an irreversible process. The efficiency of this irreversible mixing, often defined as the ratio of the rate of potential energy increase to the total energy dissipated ($\varepsilon$), is observed in laboratory and numerical studies to be approximately $\Gamma \approx 0.2$ for a wide range of conditions. 

#### The Osborn Model for Diapycnal Diffusivity

The connection between these energetic considerations and a practical [mixing coefficient](@entry_id:1127968) is made through a flux-gradient relationship. The turbulent density flux is parameterized as $\overline{w'\rho'} = -K_\rho (\partial \bar{\rho}/\partial z)$, where $K_\rho$ is the diapycnal diffusivity. Combining this with the definitions of $B$ and $N^2$ yields a direct link between buoyancy flux and diffusivity: $B = K_\rho N^2$.

By equating this with the energetic supply for mixing, expressed through the mixing efficiency $\Gamma$, we arrive at the seminal **Osborn model**:

$$
K_\rho = \frac{\Gamma \varepsilon}{N^2}
$$

This relation is a cornerstone of modern mixing parameterization. It states that the diapycnal diffusivity is proportional to the rate of TKE dissipation and the mixing efficiency, but inversely proportional to the strength of the stratification.   This inverse dependence on $N^2$ is physically intuitive: for a fixed rate of energy supply ($\varepsilon$), a more strongly stratified fluid (larger $N^2$) is more resistant to vertical mixing, resulting in a smaller diffusivity. For example, if two adjacent water patches experience the same rate of [turbulent dissipation](@entry_id:261970), but the buoyancy frequency in patch B is twice that in patch A, the resulting diapycnal diffusivity will be four times smaller ($K_{\rho,B} = K_{\rho,A}/4$). 

#### Sources of Turbulent Energy for Mixing

The Osborn model highlights the need to identify the sources of [turbulent dissipation](@entry_id:261970), $\varepsilon$, throughout the ocean. While wind forcing and buoyancy fluxes at the surface are major sources, they cannot account for the observed mixing in the deep ocean interior. A primary energy source for abyssal mixing is the tide.

When the large-scale, barotropic (depth-independent) tidal flow moves across rough bottom topography like mid-ocean ridges, it forces water parcels to move vertically. This oscillation at tidal frequencies generates **internal tides**, which are [internal gravity waves](@entry_id:185206) that propagate away from the topography, carrying energy into the ocean interior. This represents a conversion of barotropic tidal energy to baroclinic [wave energy](@entry_id:164626). These [internal waves](@entry_id:261048) can then break due to instabilities, wave-wave interactions, or reflections from other topographic features. This breaking process creates patches of intense, small-scale turbulence, providing the local dissipation $\varepsilon$ needed to drive [diapycnal mixing](@entry_id:1123661). 

For instance, consider a region where the radiated energy flux from internal tides is $F_i = 2.0 \times 10^{-2} \, \mathrm{W\,m^{-2}}$. If a fraction $f=0.30$ of this energy is dissipated locally in a layer of thickness $\Delta z = 1000 \, \mathrm{m}$, the average [dissipation rate](@entry_id:748577) per unit mass is $\varepsilon = f F_i / (\rho_0 \Delta z) \approx 5.9 \times 10^{-9} \, \mathrm{W\,kg^{-1}}$. For a typical deep-[ocean stratification](@entry_id:1129077) of $N = 2 \times 10^{-3} \, \mathrm{s}^{-1}$ and a mixing efficiency of $\Gamma = 0.2$, the Osborn model predicts a diapycnal diffusivity of $K_\rho \approx 2.9 \times 10^{-4} \, \mathrm{m^2\,s^{-1}}$. This value, while small, is orders of magnitude larger than molecular diffusivity and is critical for maintaining the global abyssal stratification and driving the deep overturning circulation. 

#### Double Diffusion

Not all diapycnal mixing is driven by mechanical turbulence. **Double diffusion** is a process that arises in statically stable water columns where both temperature and salinity contribute to the density gradient, driven by the fact that heat diffuses molecularly about 100 times faster than salt ($\kappa_T \gg \kappa_S$). Susceptibility to double diffusion requires that the stabilizing effect of one tracer is opposed by the destabilizing effect of the other. 

Two main regimes exist:
1.  **Salt Fingering**: This occurs when warm, salty water overlies cooler, fresher water ($\partial_z T > 0, \partial_z S > 0$). The stratification is stable overall, but the salinity profile is gravitationally unstable. A vertically displaced parcel loses its excess heat much faster than its excess salt, making it anomalously dense (if displaced down) or light (if displaced up) and causing the initial perturbation to grow. This leads to the formation of tall, thin vertical "fingers" that efficiently transport salt and heat vertically. This regime corresponds to a **density ratio** $R_\rho = \frac{\alpha \partial_z T}{\beta \partial_z S} > 1$, where $\alpha$ and $\beta$ are the [thermal expansion](@entry_id:137427) and haline contraction coefficients, respectively. 
2.  **Diffusive Convection**: This occurs when colder, fresher water overlies warmer, saltier water ($\partial_z T  0, \partial_z S  0$). Here, the temperature profile is unstable but is compensated by a stable salinity gradient. The rapid diffusion of heat across an interface between layers can drive convection within the layers, leading to a "staircase" structure in temperature and salinity profiles. This regime corresponds to $0  R_\rho  1$. 

Both [salt fingering](@entry_id:153510) and diffusive convection are important mechanisms for [diapycnal mixing](@entry_id:1123661) in specific regions of the ocean, such as the subtropical thermocline and polar regions.

#### Observational Estimates of Diapycnal Mixing

The theoretical models for [diapycnal mixing](@entry_id:1123661) are validated and driven by direct observations. Specialized instruments called **microstructure profilers** measure velocity and temperature fluctuations at centimeter scales.
*   **Direct Dissipation Estimate**: By measuring the vertical shear of horizontal velocity ($\partial u/\partial z, \partial v/\partial z$) at dissipation scales, one can directly compute the TKE dissipation rate, $\varepsilon$. Separately, by measuring the spectrum of the vertical temperature gradient and fitting it to the theoretical **Batchelor spectrum**, one can estimate the thermal variance [dissipation rate](@entry_id:748577), $\chi$. This allows for an estimate of the [thermal diffusivity](@entry_id:144337), $K_T = \chi / [2(\partial \bar{T}/\partial z)^2]$, which serves as a proxy for $K_\rho$ when temperature dominates the stratification. 
*   **Overturn-based Estimate**: An alternative method uses high-resolution density profiles to identify gravitationally unstable "overturns". By calculating the root-mean-square vertical displacement required to re-sort the [density profile](@entry_id:194142) into a stable state—a length scale known as the **Thorpe scale**, $L_T$—one can infer the energy of the overturning eddies. Empirical relations connect the Thorpe scale to the [dissipation rate](@entry_id:748577), typically through a scaling like $\varepsilon \propto L_T^2 N^3$. This estimate of $\varepsilon$ can then be used in the Osborn model to calculate $K_\rho$. 

These observational methods confirm that typical open-ocean interior values for diapycnal diffusivity are very small, on the order of $K_\rho \sim 10^{-5} \text{ to } 10^{-4} \, \mathrm{m^2\,s^{-1}}$. 

### Isopycnal Mixing: Stirring Along Density Surfaces

In stark contrast to the energetically constrained [diapycnal mixing](@entry_id:1123661), [isopycnal mixing](@entry_id:1126775) is a far more vigorous process. It is dominated by the stirring action of the oceanic eddy field.

#### Eddy Stirring and Isopycnal Diffusivity

Mesoscale and submesoscale eddies, with scales of tens to hundreds of kilometers, contain the vast majority of the ocean's kinetic energy. The motions within these eddies are [quasi-geostrophic](@entry_id:1130434) and largely adiabatic, meaning they tend to stir water parcels along isopycnal surfaces. This chaotic stirring process is highly effective at mixing tracers along these surfaces. Because this process does not involve working against the mean stratification, it is not subject to the same energetic constraints as [diapycnal mixing](@entry_id:1123661). The resulting effective **isopycnal diffusivity**, $K_{\text{iso}}$, is many orders of magnitude larger than the diapycnal diffusivity, with typical values in ocean models ranging from $K_{\text{iso}} \sim 10^2 \text{ to } 10^3 \, \mathrm{m^2\,s^{-1}}$. This dramatic difference, $K_{\text{iso}} \gg K_{\text{dia}}$, is the fundamental reason for the extreme anisotropy of oceanic mixing. 

#### Isopycnal Mixing and Potential Vorticity Homogenization

The effect of [isopycnal mixing](@entry_id:1126775) is profound not only for passive tracers but also for key dynamical quantities. One of the most important is **Ertel's Potential Vorticity (PV)**, defined for a Boussinesq fluid as:

$$
q = \frac{1}{\rho_0} (\nabla \times \mathbf{u} + f\hat{\mathbf{k}}) \cdot \nabla b
$$

where $\boldsymbol{\omega}_a = \nabla \times \mathbf{u} + f\hat{\mathbf{k}}$ is the [absolute vorticity](@entry_id:262794) and $\nabla b$ is the buoyancy gradient. Under adiabatic and inviscid conditions, Ertel's PV is materially conserved ($Dq/Dt = 0$). It can therefore be treated as a tracer that is carried by the large-scale flow.

The sub-grid scale process of isopycnal eddy stirring can be modeled as a diffusion process acting on tracers along isopycnal surfaces. Since PV is conserved by the large-scale flow, it is subject to this [isopycnal mixing](@entry_id:1126775). The effect of diffusion is always to flux a property down its gradient, thereby smoothing out spatial variations. Mathematically, the rate of change of the variance of PV on an isopycnal surface due to mixing can be shown to be a negative-definite quantity:

$$
\frac{d}{dt} \int_A \frac{1}{2} (q - \bar{q})^2 \,dA = - \int_A K_{\text{iso}} |\nabla_i q|^2 \,dA \le 0
$$

Here, the integration is over the area $A$ of the isopycnal surface, $\bar{q}$ is the mean PV on that surface, and $\nabla_i$ is the [gradient operator](@entry_id:275922) along the surface. This equation shows that [isopycnal mixing](@entry_id:1126775) acts systematically to destroy PV gradients, driving the potential vorticity field toward a state of homogenization on each density surface.  This tendency for PV homogenization is a powerful organizing principle for the large-scale ocean circulation, shaping the structure of the [wind-driven gyres](@entry_id:1134086) and setting the pathways of the global [thermohaline circulation](@entry_id:182297).