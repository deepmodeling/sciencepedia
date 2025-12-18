## Introduction
The vertical transport of heat, moisture, and momentum by convective clouds is a fundamental driver of weather and climate, yet these processes occur at scales far too small to be explicitly resolved by modern global models. To bridge this gap, atmospheric scientists rely on [convection parameterization](@entry_id:1123019)—a set of physical principles and mathematical formalisms that represent the net effect of these subgrid-scale motions. This article provides a comprehensive overview of modern [convection parameterization](@entry_id:1123019), focusing on the widely used [mass-flux framework](@entry_id:1127656) and the pivotal roles of [entrainment and detrainment](@entry_id:1124548). It addresses the central challenge of linking the unresolved, fast-acting convection to the resolved, slowly evolving large-scale atmospheric state.

Over the next three chapters, you will gain a deep, graduate-level understanding of this critical field. The journey begins in **Principles and Mechanisms**, where we will build the theoretical foundation from basic [thermodynamic variables](@entry_id:160587) to the complete mass-flux [plume model](@entry_id:1129836), including the physics of lateral mixing and the conceptual problem of [convective closure](@entry_id:1123027). Next, in **Applications and Interdisciplinary Connections**, we will explore how these theories are implemented in numerical models to influence weather patterns, [climate feedbacks](@entry_id:188394), and even the atmospheres of other planets. Finally, **Hands-On Practices** will provide an opportunity to apply these concepts through guided numerical exercises, solidifying your understanding of how model choices translate into physical outcomes. We will begin by delineating the fundamental principles and mathematical formalisms that underpin these powerful schemes.

## Principles and Mechanisms

This chapter delineates the fundamental physical principles and mathematical formalisms that underpin modern parameterizations of moist and dry convection. We will proceed from the [thermodynamic variables](@entry_id:160587) that govern buoyant motion to the development of a bulk [mass-flux framework](@entry_id:1127656). Subsequently, we will explore the critical roles of [entrainment and detrainment](@entry_id:1124548), analyzing both their physical origins and their profound impacts on convective development. Finally, we will address advanced topics, including the incorporation of ice-phase thermodynamics and the conceptual challenge of [convective closure](@entry_id:1123027), which links subgrid-scale convection to the resolved large-scale atmospheric state.

### Thermodynamic State Variables for Convection

The vertical motion of air parcels, which lies at the heart of convection, is governed by buoyancy and constrained by the laws of thermodynamics. To describe these processes, it is essential to define [state variables](@entry_id:138790) that are conserved under specific conditions, as these conserved quantities simplify the mathematical description of parcel ascent and mixing. Three such variables are of paramount importance: dry potential temperature, [virtual potential temperature](@entry_id:1133825), and moist static energy.

The **dry potential temperature**, denoted by $\theta$, is the temperature a parcel of dry air would attain if brought adiabatically (i.e., without exchange of heat with its surroundings) from its initial pressure $p$ to a reference pressure $p_0$ (typically $1000$ hPa). It is defined as:
$$
\theta = T\left(\frac{p_0}{p}\right)^{\kappa}
$$
where $T$ is the [absolute temperature](@entry_id:144687) and $\kappa = R_d/c_{p_d}$ is the ratio of the gas constant for dry air to the [specific heat](@entry_id:136923) of dry air at constant pressure. The material derivative of $\theta$ is zero, $D\theta/Dt = 0$, for any process that is both adiabatic and dry (no condensation or evaporation). The release of latent heat during condensation or its absorption during evaporation are diabatic processes from the perspective of dry air thermodynamics; consequently, $\theta$ is not conserved during [moist convection](@entry_id:1128092). Likewise, mixing with environmental air via entrainment or detrainment will alter a plume's $\theta$.

To account for the effect of water vapor on air density, we introduce the concept of **[virtual temperature](@entry_id:1133832)**, $T_v$. Moist air is less dense than dry air at the same temperature and pressure because the molecular weight of water is less than that of the mean molecular weight of dry air. The [virtual temperature](@entry_id:1133832) is the temperature that dry air would need to have to equal the density of a given sample of moist air at the same pressure. The effect of condensed water (liquid or ice), which adds mass without contributing to pressure, also affects density. The **[virtual potential temperature](@entry_id:1133825)**, $\theta_v$, combines these effects and is defined as the potential temperature corresponding to the virtual temperature. To a first-order approximation, it is given by:
$$
\theta_v \approx \theta\left(1+0.61\,q_v - q_l\right)
$$
where $q_v$ is the water vapor mixing ratio and $q_l$ is the cloud liquid water mixing ratio. The constant $0.61$ is an approximation for $R_v/R_d - 1$, where $R_v$ is the gas constant for water vapor. The term $\theta_v$ is directly proportional to buoyancy. It is materially conserved only under the restrictive conditions of dry adiabatic motion where the composition of the parcel ($q_v$, $q_l$) remains constant—that is, in unsaturated ascent without [phase changes](@entry_id:147766) or mixing .

To find a variable that remains conserved during moist adiabatic processes where [phase changes](@entry_id:147766) occur, we must account for latent heat. This leads to the **moist static energy** ($h$), which represents the sum of a parcel's [specific enthalpy](@entry_id:140496) ($c_{p}T$) and its geopotential energy ($gz$), augmented by the latent energy of its water vapor ($L_v q_v$). It is defined as:
$$
h = c_{p_d}T + gz + L_v q_v
$$
Here, $g$ is the acceleration due to gravity, $z$ is the height, and $L_v$ is the latent heat of vaporization. The material derivative of $h$ is $Dh/Dt=Q$, where $Q$ represents external [diabatic heating](@entry_id:1123650) sources like radiation or friction. In the absence of such external sources, $h$ is conserved ($Dh/Dt = 0$) even when condensation or evaporation occurs, because the latent heat released or absorbed is precisely balanced by a change in the parcel's sensible heat. This conservation property makes $h$ an exceptionally powerful tool for analyzing [moist convection](@entry_id:1128092). However, like $\theta$ and $\theta_v$, $h$ is not conserved when a plume mixes with environmental air, as [entrainment and detrainment](@entry_id:1124548) act as sources or sinks .

### The Mass-Flux Framework

To represent the collective effect of subgrid-scale convective plumes in a large-scale model, parameterizations often employ a **mass-flux** approach. This framework idealizes convection as being composed of one or more one-dimensional "bulk" plumes, representing the [ensemble average](@entry_id:154225) of all updrafts within a model grid cell. These plumes interact with their large-scale environment through lateral mixing.

The intensity of vertical transport within a plume is quantified by the **convective mass flux**, $M(z)$, defined as the net upward [mass flow](@entry_id:143424) per unit horizontal area at height $z$. For a plume occupying a fractional area $a(z)$ with density $\rho(z)$ and mean vertical velocity $w_u(z)$, the mass flux is:
$$
M(z) = \rho(z)\, a(z)\, w_u(z)
$$
As a plume ascends, its mass flux changes due to two primary processes: **[entrainment](@entry_id:275487)**, the mixing of environmental air into the plume, and **detrainment**, the expulsion of plume air into the environment. Let $e(z)$ and $d(z)$ be the mass [entrainment and detrainment](@entry_id:1124548) rates per unit height, respectively. By considering mass conservation for an infinitesimally thin horizontal slab of the plume, we can derive the fundamental mass continuity equation for a steady-state plume :
$$
\frac{dM}{dz} = e(z) - d(z)
$$
This equation states that the vertical gradient of the mass flux is equal to the net lateral mass exchange rate.

This framework can be extended to any scalar quantity, $\chi$, that is conserved following fluid motion in the absence of mixing. Examples include the [thermodynamic variables](@entry_id:160587) discussed previously (like moist static energy, $h$) or chemical tracers. Let the plume-mean value of the scalar be $\chi_u(z)$ and the environmental value be $\chi_e(z)$. The flux of this scalar within the plume is $M\chi_u$. Considering the fluxes into and out of a control volume, including the transport of $\chi$ by entrained and detrained air, yields the scalar budget equation :
$$
\frac{d}{dz}\left(M\chi_u\right) = e(z)\chi_e(z) - d(z)\chi_u(z)
$$
This equation is pivotal: it describes how the vertical profile of any property within the plume evolves due to vertical advection and dilution through mixing with the environment. Expanding the left-hand side using the [product rule](@entry_id:144424) and substituting the mass continuity equation reveals the change in the plume's property itself:
$$
M\frac{d\chi_u}{dz} = e(z)\left(\chi_e(z) - \chi_u(z)\right)
$$
This form clearly shows that [entrainment](@entry_id:275487) drives the plume's property $\chi_u$ towards the environmental value $\chi_e$.

### The Physics of Lateral Mixing: Entrainment and Detrainment

The rates of [entrainment and detrainment](@entry_id:1124548), $e(z)$ and $d(z)$, are not known from first principles and must be parameterized. These parameterizations are a critical source of uncertainty in climate and weather models.

It is often convenient to define a **fractional entrainment rate**, $\epsilon$, as the [entrainment](@entry_id:275487) rate per unit of internal mass flux:
$$
\epsilon(z) = \frac{e(z)}{M(z)}
$$
The units of $\epsilon$ are inverse length ($\mathrm{m}^{-1}$). A classic hypothesis, originating from the work of Morton, Taylor, and Turner, posits that the velocity at which environmental air is drawn into a turbulent plume is proportional to the plume's own vertical velocity. For an idealized top-hat plume of radius $r$, this hypothesis leads to a simple and powerful scaling law. By equating the mass entrained across the plume's perimeter with the definition of fractional [entrainment](@entry_id:275487), we find that the fractional entrainment rate is inversely proportional to the plume radius :
$$
\epsilon = \frac{2\kappa}{r}
$$
where $\kappa$ is a dimensionless [entrainment](@entry_id:275487) coefficient. This result is physically intuitive: wider plumes have a smaller surface-area-to-volume ratio and thus mix less efficiently with their surroundings, allowing them to remain more buoyant and penetrate to greater heights.

Detrainment, the process of mass leaving the plume, is often parameterized based on its underlying physical drivers. Two principal mechanisms are commonly distinguished :
1.  **Thermal Detrainment:** This occurs when a plume parcel becomes negatively buoyant relative to its environment (i.e., its density becomes greater than the environmental density). This loss of buoyancy causes the parcel to decelerate and be shed from the main updraft. A parameterization for this process would typically activate only when buoyancy $B(z)$ is negative and scale with the magnitude of this negative buoyancy.
2.  **Mechanical Detrainment:** This form of detrainment is caused by the stripping of air from the edges of the plume due to vertical shear in the horizontal environmental wind ($S(z) = \partial U / \partial z$). The turbulent eddies generated at the plume-environment interface effectively tear mass away from the updraft. A parameterization would typically scale with the strength of the shear.

A physically-based parameterization for total detrainment, $d(z)$, might combine these effects. Based on [dimensional analysis](@entry_id:140259) and scaling arguments, a plausible form for the fractional detrainment rate $\delta = d/M$ can be constructed :
$$
\delta(z) = c_{th} \frac{\max(-B(z), 0)}{w(z)^2} + c_m \frac{S(z)}{w(z)}
$$
where $c_{th}$ and $c_m$ are dimensionless coefficients. This formulation captures the ideas that thermal detrainment increases with negative buoyancy and mechanical detrainment increases with shear, with both effects being modulated by the plume's vertical velocity $w(z)$.

### Consequences of Entrainment for Convective Development

The primary effect of entrainment is the dilution of the plume's properties with environmental air. Since convective plumes are typically warmer and moister than their surroundings, entrainment systematically erodes the plume's positive buoyancy, weakening the convection.

We can quantify this effect by examining the evolution of the plume's [virtual potential temperature](@entry_id:1133825) anomaly, $\Delta\theta_v(z) = \theta_{v,u}(z) - \theta_{v,e}(z)$, which is directly proportional to buoyancy. Consider a plume ascending into a stably stratified environment where $\theta_{v,e}$ increases with height. Using the scalar budget equation for $\theta_{v,u}$, we find that the anomaly $\Delta\theta_v$ is governed by a first-order differential equation that includes both dilution due to entrainment and the effect of the environmental stratification . The solution reveals that the buoyancy anomaly decays exponentially due to [entrainment](@entry_id:275487), causing the plume to reach its level of [neutral buoyancy](@entry_id:271501) and terminate at a much lower altitude than a non-entraining, purely adiabatic parcel. This [dilution effect](@entry_id:187558) is the single most important factor limiting the height of real-world convective clouds.

The impact of [entrainment](@entry_id:275487) can also be analyzed through integrated quantities like **Convective Available Potential Energy (CAPE)** and **Convective Inhibition (CIN)**. CAPE represents the total work a buoyant parcel can do on its environment, and is defined as the vertical integral of buoyancy from the level of [free convection](@entry_id:197869) (LFC) to the level of [neutral buoyancy](@entry_id:271501) (LNB). Entrainment reduces buoyancy at every level, which not only lowers the LNB but also reduces the value of the integrand. The net effect is a substantial reduction in the effective CAPE available to an entraining plume compared to the idealized CAPE calculated for an undiluted parcel . Similarly, CIN, the energy barrier that must be overcome for a parcel to reach its LFC, is also modulated by [entrainment](@entry_id:275487). The amount of mixing in the sub-cloud layer can alter the buoyancy profile and the height of the LFC, thereby changing the CIN value .

These concepts can be synthesized to understand the conditions required to trigger deep convection. For a plume to reach a significant altitude and produce precipitation, its initial properties (e.g., surface temperature and humidity) must be sufficient to provide an initial buoyancy that can withstand dilution by entrainment over a deep layer. By linking the required buoyancy at a certain target altitude back to the initial conditions at the surface via the entraining plume equations, one can calculate a critical surface humidity or temperature anomaly needed for convective initiation. This provides a quantitative link between surface forcing, atmospheric stability, entrainment, and the likelihood of [deep convection](@entry_id:1123472) .

### The Role of Ice Microphysics in Deep Convection

For [deep convection](@entry_id:1123472) that extends above the freezing level ($T \approx 273.15$ K), the thermodynamics must be expanded to include the [phase changes](@entry_id:147766) between liquid water and ice. The freezing of liquid water releases the [latent heat of fusion](@entry_id:144988), $L_f$, providing an additional source of buoyancy that can reinvigorate an ascending plume.

This process poses a challenge for conserved-variable frameworks. The traditional moist static energy, $h_m = c_p T + gz + L_v q_v$, is not conserved during freezing. The release of latent heat, $L_f \Delta q_i$ (where $\Delta q_i$ is the mass of newly formed ice), increases the parcel's sensible heat ($c_p T$), causing $h_m$ to jump discontinuously to a higher value. This introduces a spurious energy source in a numerical model unless explicitly accounted for.

To address this, an **ice-aware moist static energy**, often called frozen moist static energy or liquid-ice static energy, can be defined. This variable includes a term representing the potential energy of the ice phase:
$$
h_i = c_p T + gz + L_v q_v - L_f q_i
$$
where $q_i$ is the ice [mixing ratio](@entry_id:1127970). The negative sign indicates that energy is required to melt the ice. With this definition, when freezing occurs, the increase in sensible heat ($c_p T$) is precisely offset by the decrease in the potential energy term ($-L_f q_i$ becomes more negative). As a result, $h_i$ remains continuous and is conserved during adiabatic freezing and melting processes, provided the condensate is retained in the parcel . Using $h_i$ as the prognostic thermodynamic variable in a mass-flux scheme allows for a more elegant and accurate energy budget, as the internal microphysical sources and sinks related to fusion are absorbed into the definition of the conserved variable itself . While small non-conservation can arise from the temperature dependence of $L_f$ and $c_p$, using $h_i$ is a substantial improvement over $h_m$ for budget closure in models with ice physics .

### The Convective Closure Problem

The mass-flux equations presented thus far—the continuity equation and the scalar budget—describe the vertical structure of a plume and its properties relative to the cloud-base mass flux, $M_b$. However, they do not determine the [absolute magnitude](@entry_id:157959) of $M_b$. The intensity of convection in a model grid cell remains an undetermined degree of freedom. The physical principle or equation used to determine this amplitude is known as the **[convective closure](@entry_id:1123027)** .

The need for a closure arises because convection operates on timescales much faster than a typical large-scale model's time step. For instance, the characteristic adjustment timescale for convection might be on the order of 15 minutes ($\approx 900$ s), while a model time step can be 30 minutes or longer . This "stiffness" implies that any instability generated by large-scale processes would be consumed almost instantaneously by convection from the model's perspective. The closure, therefore, seeks to diagnose the convective intensity that is in equilibrium with the large-scale forcing. Several families of closure have been developed, each based on a different physical hypothesis .

1.  **CAPE-based Closure:** This is the most intuitive approach. It assumes that the strength of convection, and thus $M_b$, is related to the amount of thermodynamic instability present, as measured by CAPE. In its simplest form, the scheme predicts an $M_b$ that is proportional to CAPE, acting to relax the CAPE back towards zero over a prescribed adjustment timescale, $\tau$.

2.  **Moisture-Convergence Closure:** This approach is rooted in the water budget of an atmospheric column. It posits that, in equilibrium, the rate at which convection removes water from the column via precipitation must balance the rate at which water is supplied by large-scale moisture convergence and surface evaporation. The closure then determines the $M_b$ required to produce a precipitation rate that balances this large-scale moisture supply.

3.  **Quasi-Equilibrium Closure:** This is a more sophisticated instability-based closure. It formalizes the idea that convection responds very rapidly to large-scale forcing. It assumes that the atmospheric state is in a statistical "[quasi-equilibrium](@entry_id:1130431)" where the rate of generation of CAPE by large-scale processes (e.g., advection, radiation) is almost exactly balanced by the rate of consumption of CAPE by convection. The closure problem then becomes finding the value of $M_b$ that produces a convective sink of CAPE that cancels the diagnosed large-scale source, thereby keeping the CAPE tendency close to zero.

In all these closure schemes, the processes of [entrainment and detrainment](@entry_id:1124548) play a crucial secondary role. They do not set the overall convective intensity, but they modulate the efficiency with which a given mass flux $M_b$ can stabilize the atmosphere, produce precipitation, or transport heat and moisture, thereby influencing the calculation within the closure itself .