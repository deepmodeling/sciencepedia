## Introduction
Combustion within [porous media](@entry_id:154591) represents a pivotal technology for enhancing energy efficiency, controlling emissions, and enabling novel [chemical synthesis](@entry_id:266967) routes. By confining reactions within a solid matrix, engineers can exploit exceptional heat transfer characteristics to achieve extended flammability limits, higher power densities, and greater flame stability compared to conventional open-flame systems. However, the inherent complexity of these systems—arising from the tight coupling of fluid flow, [heat and mass transfer](@entry_id:154922), and chemical kinetics across microscopic pores and macroscopic reactor scales—poses a significant challenge for predictive modeling and design.

This article provides a comprehensive guide to the simulation of [porous media combustion](@entry_id:1129963), bridging fundamental theory with practical application. It systematically builds the knowledge required to understand, develop, and apply computational models for these complex [multiphysics](@entry_id:164478) problems. You will learn to navigate the theoretical landscape and appreciate its real-world implications across three focused chapters.

The journey begins in **Principles and Mechanisms**, where we will deconstruct the core of [porous media modeling](@entry_id:1129964). This chapter establishes the volume-averaging framework and derives the macroscopic transport equations for momentum, energy, and species, including critical concepts like permeability, [local thermal non-equilibrium](@entry_id:149868), and effective properties. Next, **Applications and Interdisciplinary Connections** demonstrates how these foundational models are applied to design and analyze practical systems such as high-efficiency burners, catalytic converters, and even to understand natural phenomena like wildland fires. Finally, **Hands-On Practices** will challenge you to apply this knowledge through targeted problems, reinforcing your understanding of [dimensionless analysis](@entry_id:188181), code verification, and the relationship between micro- and macro-scale velocities.

By progressing through these sections, you will gain a robust understanding of the physics and computational methods that govern [porous media combustion](@entry_id:1129963), preparing you to tackle advanced problems in this exciting field. We begin by laying the groundwork: the principles and mechanisms that translate pore-scale complexity into a tractable continuum model.

## Principles and Mechanisms

The simulation of combustion in [porous media](@entry_id:154591) relies on a [multiscale modeling framework](@entry_id:1128335) that translates the complex physics occurring at the microscopic pore level into a tractable set of macroscopic continuum equations. This chapter elucidates the fundamental principles and mechanisms that underpin this translation, covering the theoretical basis for [volume averaging](@entry_id:1133895), the development of macroscopic transport models for momentum, mass, and energy, and the formulation of [chemical reaction kinetics](@entry_id:274455) in a multiphase system.

### The Continuum Approach: Volume Averaging

The transition from a detailed, pore-scale description of a porous medium to a macroscopic, continuum model is achieved through a process of **[volume averaging](@entry_id:1133895)**. This method smooths out the microscopic heterogeneities of the solid matrix and the interstitial fluid phases, allowing them to be treated as co-located, interpenetrating continua described by averaged field variables.

The cornerstone of this approach is the **Representative Elementary Volume (REV)**. The REV is an averaging volume, conceptually centered at a point $\mathbf{x}$ in the macroscopic domain, that must satisfy a crucial **scale separation** condition. Let $\ell_p$ be the characteristic length scale of the microstructure (e.g., the pore diameter or particle size) and $L_c$ be the macroscopic length scale over which the averaged properties (like mean temperature or velocity) vary significantly. The size of the REV, $L_{\mathrm{REV}}$, must be much larger than the pore scale but much smaller than the macroscopic gradient scale: $\ell_p \ll L_{\mathrm{REV}} \ll L_c$. This ensures that the REV is large enough to contain a statistically [representative sample](@entry_id:201715) of the pore structure, making averaged properties independent of small shifts in its position, yet small enough to be treated as a point in the macroscopic description, enabling the resolution of macroscopic gradients .

Within an REV of total volume $V_{\mathrm{REV}}$, the volume occupied by the gas phase is $V_g$ and by the solid phase is $V_s$. The most fundamental structural property derived from this is the **porosity**, $\varepsilon$, defined as the volume fraction of the void (gas) phase:
$$
\varepsilon = \frac{V_g}{V_{\mathrm{REV}}}
$$
The solid volume fraction is correspondingly $(1-\varepsilon)$.

For any scalar, vector, or [tensor field](@entry_id:266532) $\phi(\mathbf{x}, t)$ defined within a specific phase (e.g., the gas phase), we can define two types of averages. The **intrinsic phase average**, denoted $\langle \phi \rangle^g$, is the average of the quantity over the volume of the phase in which it exists. For a gas-phase quantity, it is:
$$
\langle \phi \rangle^g = \frac{1}{V_g} \int_{V_g} \phi(\mathbf{x}, t) \, dV
$$
This represents the physically experienced average value of the quantity within the gas phase itself.

In contrast, the **superficial average** (or volume average), denoted $\langle \phi \rangle$, is the average of the quantity taken over the entire volume of the REV. Since $\phi$ is only defined in the gas phase, the [integral domain](@entry_id:147487) is still $V_g$, but the normalization is by $V_{\mathrm{REV}}$:
$$
\langle \phi \rangle = \frac{1}{V_{\mathrm{REV}}} \int_{V_g} \phi(\mathbf{x}, t) \, dV
$$
This quantity represents the amount of $\phi$ per unit of total porous medium volume. The [conservation equations](@entry_id:1122898) in [porous media modeling](@entry_id:1129964) are typically written in terms of these superficial averages.

The relationship between these two averages is direct and fundamental. By substituting the definition of the integral from the intrinsic average, $\int_{V_g} \phi \, dV = V_g \langle \phi \rangle^g$, into the definition of the superficial average, we find:
$$
\langle \phi \rangle = \frac{V_g}{V_{\mathrm{REV}}} \langle \phi \rangle^g
$$
Recognizing that $V_g / V_{\mathrm{REV}} = \varepsilon$, we arrive at the crucial link between the two averages:
$$
\langle \phi \rangle = \varepsilon \langle \phi \rangle^g
$$
This simple relation is essential for interpreting simulation results and for moving between the physical quantities within the fluid and the [conserved variables](@entry_id:747720) of the macroscopic model .

### Macroscopic Transport Models

With the volume-averaging framework established, we can develop macroscopic [closure models](@entry_id:1122505) for the transport of momentum, heat, and mass. These models replace the need to resolve complex pore-scale geometries and flow fields with effective parameters that represent the bulk behavior of the medium.

#### Momentum Transport: From Darcy to Forchheimer and Brinkman

The flow of fluid through the tortuous paths of a porous medium results in a drag force exerted by the solid matrix on the fluid. The macroscopic momentum equation is essentially a balance between this drag force and the [driving pressure](@entry_id:893623) gradient. The form of the drag model depends on the flow regime, characterized by the pore-scale Reynolds number, $\mathrm{Re}_p = \rho U \ell_p / \mu$, where $U$ is a characteristic [superficial velocity](@entry_id:152020).

**Darcy's Law:** For slow, viscous-dominated flows where pore-scale [inertial forces](@entry_id:169104) are negligible ($\mathrm{Re}_p \ll 1$), the relationship between the pressure gradient, $-\nabla p$, and the [superficial velocity](@entry_id:152020), $\boldsymbol{u}$, is linear. This is **Darcy's Law**:
$$
-\nabla p = \frac{\mu}{\kappa} \boldsymbol{u}
$$
Here, $\mu$ is the fluid's [dynamic viscosity](@entry_id:268228) and $\kappa$ is the **permeability** of the porous medium. Permeability is a crucial property with units of area ($m^2$) that quantifies the ease with which a fluid can flow through the medium. It depends only on the geometry of the solid matrix. Darcy's law is a bulk model valid far from boundaries and assumes strong scale separation, $\ell_p \ll L_{\mathrm{REV}} \ll L_c$ .

**The Forchheimer Extension:** As the flow velocity increases into the moderate Reynolds number regime ($\mathrm{Re}_p \ge 1$), pore-scale inertial effects become significant. The flow separates and forms eddies in the pore wakes, leading to an additional "form drag" that is non-linear with velocity. The **Forchheimer model** accounts for this by adding a quadratic term to Darcy's law:
$$
-\nabla p = \frac{\mu}{\kappa} \boldsymbol{u} + \rho \beta |\boldsymbol{u}| \boldsymbol{u}
$$
The parameter $\beta$, known as the **Forchheimer coefficient** or [inertial coefficient](@entry_id:151636), depends on the pore geometry. This model, like Darcy's law, is a bulk model that requires scale separation and does not resolve boundary layers at interfaces .

For many practical applications, such as packed beds of particles, empirical correlations are used to relate $\kappa$ and $\beta$ to the microstructural properties. A classic example is the **Ergun equation** for a packed bed of monodisperse spheres of diameter $d_p$ and porosity $\varepsilon$. By comparing the Darcy-Forchheimer equation with the Ergun equation, the permeability and Forchheimer coefficient can be identified as:
$$
\kappa = \frac{\varepsilon^3 d_p^2}{150 (1-\varepsilon)^2} \quad \text{and} \quad \beta = \frac{1.75 (1-\varepsilon)}{\varepsilon^3 d_p}
$$
These expressions provide a direct link from measurable microstructural parameters to the macroscopic momentum [transport coefficients](@entry_id:136790) required for simulation .

**The Brinkman Equation:** Both the Darcy and Forchheimer models are algebraic and lack second-order spatial derivatives. Consequently, they cannot satisfy boundary conditions related to shear stress, such as the [no-slip condition](@entry_id:275670) at a solid wall or continuity of shear at an interface between the porous medium and a clear fluid. The **Brinkman model** addresses this by adding a macroscopic viscous shear term, analogous to the viscous term in the Navier-Stokes equations, to Darcy's law:
$$
-\nabla p + \mu_{\mathrm{eff}} \nabla^2 \boldsymbol{u} = \frac{\mu}{\kappa} \boldsymbol{u}
$$
This equation is typically justified for [creeping flow](@entry_id:263844) ($\mathrm{Re}_p \ll 1$) in situations where boundary layers are important, such as in high-porosity media or near interfaces. The **[effective viscosity](@entry_id:204056)**, $\mu_{\mathrm{eff}}$, reflects the volume-averaged shear effects and is often taken as a function of the [fluid viscosity](@entry_id:261198) and porosity. The inclusion of the $\nabla^2 \boldsymbol{u}$ term allows for the satisfaction of shear-related boundary conditions, enabling a smooth transition of the velocity profile from within the porous medium to an adjacent clear-fluid region .

#### Interphase Exchange: Heat and Mass Transfer

In [non-equilibrium systems](@entry_id:193856), particularly in combustion where large temperature and concentration gradients exist, the exchange of heat and mass between the gas and solid phases is a critical process. This exchange is modeled using interfacial transfer coefficients.

The rate of heat or [mass transfer](@entry_id:151080) is proportional to the total interfacial area available. We define the **[specific surface area](@entry_id:158570)**, $a_s$, as the total solid-gas interfacial area per unit total volume of the porous medium ($m^2/m^3 = m^{-1}$). For a packed bed of monodisperse spheres of diameter $d_p$, this can be derived from geometric considerations as:
$$
a_s = \frac{6(1-\varepsilon)}{d_p}
$$
This shows that a finer packing (smaller $d_p$) or lower porosity (denser packing) leads to a larger specific surface area .

The volumetric heat exchange rate between solid and gas, $\dot{q}_{sg}'''$, is modeled using Newton's law of cooling, scaled by the [specific surface area](@entry_id:158570):
$$
\dot{q}_{sg}''' = h_{sg} a_s (T_s - T_g)
$$
Here, $T_s$ and $T_g$ are the local average solid and gas temperatures, and $h_{sg}$ is the **[interfacial heat transfer coefficient](@entry_id:153982)** ($W \cdot m^{-2} \cdot K^{-1}$). The value of $h_{sg}$ is not constant; it depends on the flow conditions and [fluid properties](@entry_id:200256). This dependence is captured by the dimensionless **Nusselt number**, $Nu = h_{sg} d_p / k_g$, where $k_g$ is the gas thermal conductivity. For forced convection, the Nusselt number is a function of the Reynolds number ($Re$) and the Prandtl number ($Pr$), i.e., $Nu = f(Re, Pr)$. Typically, $Nu$ (and thus $h_{sg}$) increases with increasing flow velocity ($Re$) because the higher flow thins the thermal boundary layers at the particle surfaces, enhancing heat transfer .

Analogously, the volumetric mass exchange rate for a species $i$ due to heterogeneous reactions is coupled to interfacial mass transfer. The flux of species from the bulk gas to the surface is modeled as:
$$
J_i = k_{sg} (C_{i,g} - C_{i,s})
$$
where $C_{i,g}$ and $C_{i,s}$ are the bulk gas and surface concentrations, and $k_{sg}$ is the **interfacial mass transfer coefficient** ($m \cdot s^{-1}$). Its dependence on flow is captured by the dimensionless **Sherwood number**, $Sh = k_{sg} L / D_{\mathrm{eff}}$, where $L$ is a characteristic length and $D_{\mathrm{eff}}$ is the effective [mass diffusivity](@entry_id:149206) in the porous medium. The Sherwood number is the mass transfer analogue of the Nusselt number and is a function of the Reynolds number and the Schmidt number, $Sc$ .

#### Energy Transport: Thermal Equilibrium and Non-Equilibrium

A central decision in modeling [porous media combustion](@entry_id:1129963) is whether to assume the solid and gas phases are at the same temperature locally.

The **Local Thermal Equilibrium (LTE)** assumption posits that $T_s = T_g$ at every point in the domain. This is justified when [interfacial heat transfer](@entry_id:1126604) is extremely efficient compared to all other thermal processes, rapidly eliminating any temperature difference between the phases. Under LTE, a single [energy equation](@entry_id:156281) for a unified temperature field $T(x)$ is sufficient, greatly simplifying the model.

The **Local Thermal Non-Equilibrium (LTNE)** model does not make this assumption, allowing for $T_s \neq T_g$. This requires solving two separate, coupled energy equations—one for the gas and one for the solid—which are linked by the interfacial heat exchange term, $h_{sg} a_s (T_s - T_g)$. LTNE is necessary when the mechanisms generating temperature differences are fast or strong compared to the mechanism of [interphase](@entry_id:157879) equilibration .

The validity of LTE versus LTNE can be assessed using [dimensionless analysis](@entry_id:188181). One key parameter is the **interfacial Biot number**, which compares the rate of [interphase](@entry_id:157879) heat exchange to the rate of intraphase conduction at the pore scale, $L$. For each phase $\beta \in \{g, s\}$, we can define:
$$
Bi_{\beta} = \frac{h_{sg} a_s L^2}{k_{\beta}}
$$
where $k_{\beta}$ is the intrinsic thermal conductivity of the phase. If $Bi_g \gg 1$ and $Bi_s \gg 1$, [interphase transfer](@entry_id:1126635) is much faster than intraphase conduction, the phases are tightly coupled, and LTE is a good assumption. Conversely, if either $Bi_g \lesssim 1$ or $Bi_s \lesssim 1$, significant temperature gradients can be sustained within a phase before the heat is transferred to the other phase, necessitating an LTNE model.

A second criterion involves comparing timescales. The characteristic time for thermal relaxation between phases, $\tau_{sg}$, must be much shorter than other relevant timescales, such as the fluid advection time, $\tau_{adv} = L/U$, or the chemical reaction time, $\tau_{chem}$. If $\tau_{sg}$ is not negligible compared to $\tau_{adv}$ or $\tau_{chem}$, the phases will not have time to equilibrate, and an LTNE model is required. This is often the case in fast combustion processes where heat is released rapidly into the gas phase, causing its temperature to rise much faster than the solid's .

#### Advanced Models for Effective Thermal Conductivity

In the volume-averaged energy equations, the conductive heat flux for each phase $\beta$ is modeled using Fourier's law with an **effective thermal conductivity tensor**, $\mathbf{k}_{\beta, \mathrm{eff}}$. This tensor lumps several physical transport mechanisms into a single constitutive parameter. For a general LTNE model, we have $\mathbf{k}_{\beta, \mathrm{eff}} = \mathbf{k}_{\beta, \mathrm{cond}} + \mathbf{k}_{\beta, \mathrm{rad}} + \mathbf{k}_{\beta, \mathrm{disp}}$.

1.  **Conduction ($\mathbf{k}_{\beta, \mathrm{cond}}$):** This represents molecular conduction through the phase. It is modeled by scaling the intrinsic conductivity of the material ($k_g$ or $k_s$) by its [volume fraction](@entry_id:756566) ($\varepsilon$ or $1-\varepsilon$) and a **tortuosity factor** that accounts for the non-straight paths for heat flow.

2.  **Radiation ($\mathbf{k}_{\beta, \mathrm{rad}}$):** At high temperatures, thermal radiation is a significant mode of heat transfer. For an [optically thick medium](@entry_id:752966), radiative transfer can be approximated as a diffusive process, contributing an isotropic term to the effective conductivity, proportional to $T^3$. For the gas phase, this depends on the gas's [radiative properties](@entry_id:150127) (e.g., Rosseland mean absorption coefficient). For the solid phase, it represents surface-to-surface radiation across the pores.

3.  **Dispersion ($\mathbf{k}_{\beta, \mathrm{disp}}$):** This term exists only for the flowing phase (the gas). **Thermal dispersion** is a convective phenomenon where the complex micro-velocity field within the pores enhances thermal mixing. This enhanced transport, when volume-averaged, appears as a diffusive-like flux. This contribution is velocity-dependent and anisotropic—stronger in the direction of mean flow than transverse to it.

A complete model for the effective conductivity tensors might therefore take the form :
$$
\mathbf{k}_{g,\mathrm{eff}} = \underbrace{\varepsilon \tau_g k_g \mathbf{I}}_{\text{Conduction}} + \underbrace{\mathbf{k}_{g, \mathrm{rad}}(T)}_{\text{Radiation}} + \underbrace{\mathbf{k}_{g, \mathrm{disp}}(\boldsymbol{u})}_{\text{Dispersion}}
$$
$$
\mathbf{k}_{s,\mathrm{eff}} = \underbrace{(1-\varepsilon) \tau_s k_s \mathbf{I}}_{\text{Conduction}} + \underbrace{\mathbf{k}_{s, \mathrm{rad}}(T)}_{\text{Radiation}}
$$
where the detailed expressions for the radiation and dispersion tensors depend on the specific models chosen.

### Chemical Reactions in Porous Media

The final component of a [porous media combustion](@entry_id:1129963) model is the representation of chemical reactions, which act as source or sink terms in the species and energy conservation equations.

#### Homogeneous and Heterogeneous Reactions

Reactions in [porous media](@entry_id:154591) can occur in two distinct locations:

-   **Homogeneous reactions** take place in the bulk gas phase within the pore volume. Their rates, $R_k^g$, are typically functions of the gas-phase temperature, $T_g$, and the gas-phase species concentrations, $\{C_j\}$.
-   **Heterogeneous reactions** take place on the surface of the solid matrix, which may be catalytically active. Their rates, $R_m^s$, are defined per unit of surface area and are functions of the solid-phase (surface) temperature, $T_s$, and the species concentrations at the surface.

In a volume-averaged model, both types of reactions contribute to the net production rate of a species $i$, $\omega_i^{g, \text{kin}}$, in the gas-phase species balance. The homogeneous rate is already volumetric, but the heterogeneous (areal) rate must be multiplied by the [specific surface area](@entry_id:158570), $a_s$, to convert it to a volumetric source term.
$$
\omega_i^{g, \text{kin}} = \sum_{k} \nu_{i,k} R_k^g(T_g, \{C_j\}) + a_s \sum_{m} \nu_{i,m} R_m^s(T_s, \{C_j\})
$$
where $\nu_{i,k}$ and $\nu_{i,m}$ are the stoichiometric coefficients.

Crucially, under the LTNE framework, the heat released by these reactions must be assigned to the phase in which they occur. Heat from homogeneous reactions, $\dot{q}_g^{\text{kin}}$, is released directly into the gas. Heat from heterogeneous reactions, $\dot{q}_s^{\text{kin}}$, is released directly to the solid matrix.
$$
\dot{q}_g^{\text{kin}} = - \sum_{k} \Delta h_k R_k^g \qquad \text{and} \qquad \dot{q}_s^{\text{kin}} = - a_s \sum_{m} \Delta h_m R_m^s
$$
where $\Delta h$ is the [enthalpy of reaction](@entry_id:137819) (negative for exothermic). This correct partitioning of energy sources is a defining feature of LTNE [combustion modeling](@entry_id:201851) .

#### Dimensionless Analysis: The Damköhler Number

The **Damköhler number (Da)** is a powerful dimensionless group that compares a characteristic transport timescale to a characteristic chemical reaction timescale, $\mathrm{Da} = \tau_{\text{trans}} / \tau_{\text{chem}}$. It quantifies the relative importance of reaction versus transport.

In a porous reactor of length $L$ with [superficial velocity](@entry_id:152020) $U$, the convective residence time is $\tau_{\text{conv}} = L/U$. For a first-order gas-phase reaction with rate constant $k_c$, the chemical time is $\tau_{\text{chem}, g} = 1/k_c$. For a first-order surface reaction with effective volumetric rate constant $a_s k_s$, the chemical time is $\tau_{\text{chem}, s} = 1/(a_s k_s)$. This allows us to define separate Damköhler numbers for each pathway:
$$
\mathrm{Da}_g = \frac{\tau_{\text{conv}}}{\tau_{\text{chem}, g}} = \frac{k_c L}{U} \qquad \text{and} \qquad \mathrm{Da}_s = \frac{\tau_{\text{conv}}}{\tau_{\text{chem}, s}} = \frac{a_s k_s L}{U}
$$
The magnitude of these numbers helps classify the combustion regime :
-   If $\mathrm{Da}_g \ll 1$ and $\mathrm{Da}_s \ll 1$, transport is much faster than reaction. The residence time is too short for significant reaction to occur.
-   If $\mathrm{Da}_g \gg 1$ and $\mathrm{Da}_s \ll 1$, the process is dominated by homogeneous gas-phase combustion.
-   If $\mathrm{Da}_s \gg 1$ and $\mathrm{Da}_g \ll 1$, the process is dominated by heterogeneous (catalytic) combustion.
-   If both are large, both pathways are significant.

It is important to recognize that while Damköhler numbers are essential for assessing [reaction kinetics](@entry_id:150220), they are not sufficient to predict the overall behavior, especially stability. A complete analysis also requires considering other dimensionless groups, such as the Péclet number (comparing advection to diffusion) and parameters quantifying heat transport and heat losses .

#### Coupled Transport and Reaction: Emergent Phenomena

The rich and often complex behavior of [porous media](@entry_id:154591) combustors arises from the tight coupling between chemical reactions and the unique transport mechanisms within the porous matrix.

For a heterogeneous reaction, the overall rate can be limited either by the intrinsic [surface chemistry](@entry_id:152233) or by the rate at which reactants can be transported from the bulk gas to the reactive surface. At steady state, the flux to the surface must equal the consumption rate at the surface. For a [first-order reaction](@entry_id:136907) ($r'' = k_s C_s$) with [mass transfer](@entry_id:151080) modeled by $J = k_{sg}(C_g - C_s)$, this balance yields an overall effective reaction rate per unit area:
$$
r''_{\text{eff}} = \frac{k_s k_{sg}}{k_s + k_{sg}} C_g
$$
This expression reveals two limits. If mass transfer is very fast ($k_{sg} \to \infty$, or $Sh \to \infty$), then $r''_{\text{eff}} \to k_s C_g$, and the process is under **[kinetic control](@entry_id:154879)**. If the intrinsic reaction is very fast ($k_s \to \infty$), then $r''_{\text{eff}} \to k_{sg} C_g$, and the process is under **[mass transfer](@entry_id:151080) control** .

Perhaps the most significant emergent phenomenon is the existence of **[multiple steady states](@entry_id:1128326)** and hysteresis, often visualized as an "S-curve". This behavior is a direct consequence of the powerful [thermal feedback](@entry_id:1132998) provided by the solid matrix. In a porous burner, heat released from the combustion zone is conducted very efficiently through the solid matrix both upstream and downstream. The upstream heat conduction serves to **recirculate heat**, [preheating](@entry_id:159073) the incoming fresh fuel-air mixture to a temperature well above its initial inlet temperature.

This positive feedback loop creates the potential for [multiplicity](@entry_id:136466). The steady state of the system is found at the intersection of the heat generation rate curve, $\dot{q}_{\text{chem}}(T)$, and the net heat loss rate curve, $\dot{q}_{\text{loss}}(T)$. The [chemical heat release](@entry_id:1122340), governed by Arrhenius kinetics, is a strongly non-linear, S-shaped function of temperature. The heat loss, which includes upstream advection and conduction as well as external losses, is often a more linear function of temperature. The combination of a non-linear S-shaped generation curve and a linear loss line can result in one, two (at tangency), or three intersection points. These correspond to a stable low-temperature (unburnt) state, an unstable intermediate state, and a stable high-temperature (burning) state . The transitions between having one and three solutions correspond to **ignition** and **extinction** points. These are fold bifurcations where the heat generation and heat loss curves are tangent, meaning their rates and their first derivatives with respect to temperature are equal:
$$
\dot{q}_{\text{chem}}(T_{\text{fold}}) = \dot{q}_{\text{loss}}(T_{\text{fold}}) \quad \text{and} \quad \frac{d\dot{q}_{\text{chem}}}{dT}\bigg|_{T_{\text{fold}}} = \frac{d\dot{q}_{\text{loss}}}{dT}\bigg|_{T_{\text{fold}}}
$$
This fundamental balance between non-linear heat release and [heat recirculation](@entry_id:1125982) and loss is the primary mechanism governing the stability, ignition, and extinction behavior of [porous media](@entry_id:154591) combustors .