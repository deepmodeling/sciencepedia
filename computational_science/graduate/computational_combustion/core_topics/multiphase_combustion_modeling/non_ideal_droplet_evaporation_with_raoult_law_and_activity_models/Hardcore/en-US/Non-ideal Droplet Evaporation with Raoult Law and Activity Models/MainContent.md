## Introduction
The evaporation of multicomponent fuel droplets is a fundamental process at the heart of many technologies, from internal combustion engines to industrial spray systems. Accurately predicting how these complex liquid blends vaporize is crucial for optimizing efficiency, controlling emissions, and ensuring stable operation. However, many foundational models rely on the simplifying assumption of ideal liquid behavior, a premise that often fails for modern fuels containing diverse chemical families like [alcohols](@entry_id:204007) and aromatics. This discrepancy between [ideal theory](@entry_id:184127) and real-world behavior creates a significant challenge for [predictive modeling](@entry_id:166398), leading to inaccuracies in evaporation rates, fuel vapor composition, and overall system performance.

This article bridges that gap by providing a comprehensive exploration of [non-ideal droplet evaporation](@entry_id:1128796). The journey begins in the "Principles and Mechanisms" chapter, where we will deconstruct the ideal Raoult's law to understand its limitations and then build a more robust framework using the concept of [activity coefficients](@entry_id:148405). In the "Applications and Interdisciplinary Connections" chapter, we will apply these principles to practical scenarios, demonstrating their critical role in modeling biofuel combustion and understanding atmospheric aerosol physics. Finally, the "Hands-On Practices" section will offer opportunities to solidify these concepts through targeted problems. We begin by establishing the thermodynamic first principles that govern the complex interactions at the liquid-gas interface.

## Principles and Mechanisms

The evaporation of multicomponent fuel droplets is a process governed by the interplay of thermodynamics and [transport phenomena](@entry_id:147655) at the liquid-gas interface. While introductory models often assume ideal behavior, real fuel blends exhibit significant non-idealities that profoundly influence their vaporization characteristics. This chapter elucidates the principles and mechanisms governing [non-ideal droplet evaporation](@entry_id:1128796), beginning with the ideal baseline of Raoult's law and systematically introducing the thermodynamic framework required to describe real mixtures.

### Vapor-Liquid Equilibrium and the Ideal Solution: Raoult's Law

The cornerstone of modeling droplet evaporation is the assumption of **[vapor-liquid equilibrium](@entry_id:182756) (VLE)** at the droplet surface. This principle posits that for each component $i$ in the mixture, its escaping tendency from the liquid phase is equal to its escaping tendency from the gas phase. In the language of thermodynamics, this is expressed as the equality of the chemical potential, $\mu_i$, or equivalently, the [fugacity](@entry_id:136534), $f_i$, of each component across the interface:

$$\mu_i^{\ell}(T, P, \{x_j\}) = \mu_i^{v}(T, P, \{y_j\})$$

where the superscripts $\ell$ and $v$ denote the liquid and vapor phases, respectively, $T$ is the interfacial temperature, $P$ is the total pressure, and $\{x_j\}$ and $\{y_j\}$ are the sets of mole fractions in the liquid and vapor phases.

To translate this fundamental condition into a practical algebraic relation, a series of assumptions must be made about the nature of each phase. The simplest and most idealized model results in **Raoult's law**. For a component $i$ in a mixture, Raoult's law relates its [partial pressure](@entry_id:143994) in the vapor, $p_i$, to its mole fraction in the liquid, $x_i$, and its pure-component saturation pressure, $P_i^{\text{sat}}(T)$. By combining Raoult's law ($p_i = x_i P_i^{\text{sat}}(T)$) with Dalton's law for an [ideal gas mixture](@entry_id:149212) ($p_i = y_i P$), we arrive at the familiar expression for interfacial equilibrium :

$$y_i P = x_i P_i^{\text{sat}}(T)$$

The apparent simplicity of this equation belies a strict set of underlying assumptions. For this relation to be valid, the following minimal conditions must be met:
1.  **Local Thermodynamic Equilibrium**: The interface is assumed to be in a state of thermodynamic equilibrium.
2.  **Ideal Liquid Solution**: The intermolecular forces between all molecular species (like-like and unlike) are assumed to be identical. This implies that the mixing process is athermal and has no volume change.
3.  **Ideal Gas Mixture**: The vapor phase is assumed to behave as a mixture of ideal gases, where each component's fugacity is equal to its [partial pressure](@entry_id:143994).
4.  **Negligible Curvature Effect**: The interface is treated as planar, ignoring the **Kelvin effect**, which elevates the vapor pressure over a curved surface. This assumption is valid for droplets with a sufficiently large radius.
5.  **Negligible Pressure Effect**: The effect of total system pressure on the liquid's chemical potential, known as the **Poynting correction**, is assumed to be negligible. This is a reasonable approximation when the system pressure is not significantly higher than the component saturation pressures.

While Raoult's law provides a valuable baseline, its assumptions, particularly that of an ideal liquid solution, are frequently violated by real fuel blends, which often consist of chemically diverse molecules like [alcohols](@entry_id:204007), [alkanes](@entry_id:185193), and aromatics .

### Departure from Ideality: The Activity Coefficient

The assumption of an ideal liquid solution fails when the intermolecular forces between unlike molecules differ from those between like molecules. For instance, in a mixture of a polar alcohol and a nonpolar alkane, the strong [hydrogen bonding](@entry_id:142832) between alcohol molecules is disrupted by the presence of [alkanes](@entry_id:185193), leading to behavior that deviates significantly from ideality . To account for such deviations, thermodynamics provides a more general framework based on the concept of **activity**.

The chemical potential of a species $i$ in a real liquid mixture is written in a form that preserves the mathematical structure of the [ideal solution](@entry_id:147504) expression, but replaces the mole fraction $x_i$ with the activity $a_i$ :

$$\mu_i^{\ell} = \mu_i^{\ell, \text{ref}} + RT \ln a_i$$

Here, $\mu_i^{\ell, \text{ref}}$ is the chemical potential in a defined reference state. The **activity coefficient**, $\gamma_i$, is then introduced as a correction factor that relates activity to [mole fraction](@entry_id:145460):

$$a_i = \gamma_i x_i$$

The activity coefficient $\gamma_i$ quantifies the deviation from ideal behavior. Its value reflects the nature of the [intermolecular interactions](@entry_id:750749) in the liquid phase :
*   $\boldsymbol{\gamma_i = 1}$: The solution behaves ideally with respect to component $i$.
*   $\boldsymbol{\gamma_i > 1}$: This indicates a **positive deviation** from Raoult's law. The [cohesive forces](@entry_id:274824) between unlike molecules are weaker than the average forces between like molecules. This increases the "escaping tendency" (fugacity) of component $i$ compared to an ideal solution, resulting in a higher [vapor pressure](@entry_id:136384). Mixtures of polar and nonpolar components, such as ethanol and hexane, typically exhibit positive deviations.
*   $\boldsymbol{\gamma_i  1}$: This indicates a **negative deviation** from Raoult's law. Strong attractive forces exist between unlike molecules, such as [hydrogen bonding](@entry_id:142832) or complex formation (e.g., in acetone-[chloroform](@entry_id:896276) mixtures). This reduces the escaping tendency of the components, resulting in a lower vapor pressure than predicted by Raoult's law.

By incorporating the activity coefficient into the VLE derivation, we arrive at the **modified Raoult's law**, which is the central governing equation for non-ideal VLE at low to moderate pressures :

$$y_i P = \gamma_i x_i P_i^{\text{sat}}(T)$$

This equation forms the boundary condition for species transport in computational models of [non-ideal droplet evaporation](@entry_id:1128796). For a known liquid-phase state at the interface (composition $\{x_{i,s}\}$ and temperature $T_s$), the corresponding equilibrium vapor-phase mole fractions $\{y_{i,s}\}$ can be calculated directly.

For example, consider a binary droplet interface at a temperature $T_s = 370\,\mathrm{K}$ and total pressure $P = 1\,\mathrm{atm}$. Let the interfacial liquid composition be $x_{A,s} = 0.60$ and $x_{B,s} = 0.40$. The pure-component saturation pressures are $P_A^{\text{sat}} = 0.30\,\mathrm{atm}$ and $P_B^{\text{sat}} = 0.05\,\mathrm{atm}$. Due to non-ideal interactions, the [activity coefficients](@entry_id:148405) are calculated to be $\gamma_A = 1.20$ and $\gamma_B = 1.80$. The interfacial vapor mole fractions are then determined as follows :

For component A: $$y_{A,s} = \frac{\gamma_A x_{A,s} P_A^{\text{sat}}}{P} = \frac{1.20 \times 0.60 \times 0.30\,\mathrm{atm}}{1\,\mathrm{atm}} = 0.216$$

For component B: $$y_{B,s} = \frac{\gamma_B x_{B,s} P_B^{\text{sat}}}{P} = \frac{1.80 \times 0.40 \times 0.05\,\mathrm{atm}}{1\,\mathrm{atm}} = 0.036$$

The remainder of the gas phase at the interface would be composed of the ambient carrier gas, so that $\sum y_{j,s} = 1$. It is crucial to recognize that in a full evaporation simulation, the interfacial liquid composition $\{x_{i,s}\}$ and temperature $T_s$ are themselves unknowns that must be determined by solving the coupled [conservation equations](@entry_id:1122898) for mass and energy.

### Thermodynamic Consistency and Advanced VLE Concepts

#### The Gibbs-Duhem Equation

The activity coefficients for the different components in a mixture are not independent of one another. They are constrained by a fundamental thermodynamic consistency relation known as the **Gibbs-Duhem equation**. For a multicomponent mixture at constant temperature and pressure, this relation takes the form :

$$\sum_{i=1}^{N} x_i\,\mathrm{d}\ln\gamma_i = 0$$

This equation is a mathematical consequence of the fact that all [activity coefficients](@entry_id:148405) are derived from a single parent function: the total **excess Gibbs energy** of the mixture, $G^E$. The excess Gibbs energy represents the difference in Gibbs energy between a real mixture and an ideal solution at the same temperature, pressure, and composition, and is directly related to the [activity coefficients](@entry_id:148405) by $G^E = RT \sum_i n_i \ln \gamma_i$ . The Gibbs-Duhem equation ensures that any analytical or empirical model for activity coefficients (such as the Wilson, NRTL, or UNIQUAC models) is thermodynamically sound. It implies that for a [binary mixture](@entry_id:174561), if the functional form of $\gamma_1$ with respect to composition is known, the form of $\gamma_2$ is automatically determined. This constraint is vital for ensuring that simulations of transient evaporation, where liquid composition continuously evolves, remain physically consistent.

#### Limiting Laws: Henry's Law for Dilute Species

While the modified Raoult's law framework is general, it is useful to consider its behavior in the limits of concentration. For the component that acts as the **solvent** (e.g., component $A$ as its [mole fraction](@entry_id:145460) $x_A \to 1$), its environment approaches that of the pure liquid. In this limit, the solution behaves ideally with respect to the solvent, and its [activity coefficient](@entry_id:143301) approaches unity, $\gamma_A \to 1$.

Conversely, for a component that is a dilute **solute** (e.g., component $B$ as $x_B \to 0$), each solute molecule is surrounded exclusively by solvent molecules. In this limit, the [activity coefficient](@entry_id:143301) approaches a constant value known as the **[activity coefficient](@entry_id:143301) at infinite dilution**, $\gamma_B^{\infty}$, which is generally not equal to one. The VLE for the solute is no longer described by Raoult's law but by **Henry's law** :

$$y_B P = H_B x_B$$

The **Henry's constant**, $H_B$, represents the proportionality between the [partial pressure](@entry_id:143994) and the liquid mole fraction for a dilute solute. It is not an independent parameter but is related to the Raoult's law framework through the [activity coefficient](@entry_id:143301) at infinite dilution:

$$H_B = \gamma_B^{\infty} P_B^{\text{sat}}(T)$$

The key distinction between Raoult's and Henry's laws lies in the **[reference state](@entry_id:151465)** used to define the chemical potential. Raoult's law is based on a pure-liquid reference state, appropriate for a solvent. Henry's law is based on a hypothetical infinite-dilution reference state, appropriate for a solute. For fuel blends containing trace additives or for later stages of evaporation where some components become highly dilute, applying the correct limiting law is essential for accurate predictions .

#### Azeotropes: A Hallmark of Non-Ideality

One of the most striking consequences of non-ideal liquid behavior is the formation of **azeotropes**. An [azeotrope](@entry_id:146150) is a liquid mixture of a specific composition that boils at a constant temperature, producing a vapor of the exact same composition as the liquid ($x_i = y_i$ for all components) . During evaporation, an azeotropic mixture behaves like a [pure substance](@entry_id:150298).

This phenomenon cannot occur in typical [ideal solutions](@entry_id:148303). The condition for an [azeotrope](@entry_id:146150) can be derived directly from the modified Raoult's law. By setting $y_i = x_i$, we find:

$$x_i P = \gamma_i x_i P_i^{\text{sat}}(T)$$

For a non-[trivial solution](@entry_id:155162) ($x_i \ne 0$), this simplifies to $P = \gamma_i P_i^{\text{sat}}(T)$. Since this must hold for all components in the mixture, the condition for an [azeotrope](@entry_id:146150) in a [binary system](@entry_id:159110) is:

$$\gamma_1 P_1^{\text{sat}}(T) = \gamma_2 P_2^{\text{sat}}(T) = P$$

The formation of an [azeotrope](@entry_id:146150) depends on the specific values of the activity coefficients (which are functions of composition) and the pure-component saturation pressures. For example, a [minimum-boiling azeotrope](@entry_id:143101) often occurs in systems with strong positive deviations from Raoult's law (e.g., ethanol-water), where the mixture's total vapor pressure is higher than that of either pure component. The existence of azeotropes can dramatically alter the evaporation sequence of a fuel blend, potentially causing it to vaporize congruently rather than preferentially losing its more volatile component.

### Coupling to the Interfacial Energy Balance

The thermodynamics of [non-ideal mixtures](@entry_id:178975) are not only coupled to [mass transfer](@entry_id:151080) but also to the energy balance at the droplet interface. Evaporation is an [endothermic process](@entry_id:141358), and the heat required must be supplied from the hot ambient gas and/or the droplet's interior. For a quasi-steady evaporation process, the heat flux supplied to the interface must balance the energy consumed by phase change :

$$q_{\text{in}} = q_{\text{vap}}$$

The heat supplied from the gas, $q_{\text{in}}$, is typically modeled as $h(T_\infty - T_s)$, where $h$ is the heat [transfer coefficient](@entry_id:264443) and $T_\infty$ is the far-field gas temperature. The energy consumed by vaporization, $q_{\text{vap}}$, must account for both the latent heat of vaporization and the heat effects associated with non-[ideal mixing](@entry_id:150763).

This latter effect is quantified by the **[excess enthalpy](@entry_id:173873)**, $h^E$, also known as the **heat of mixing**. It is defined as the difference between the enthalpy of a real liquid mixture and that of an [ideal solution](@entry_id:147504) at the same conditions :

$$h^E(T, P, x) \equiv h_{\text{real}}(T, P, x) - h_{\text{ideal}}(T, P, x)$$

An endothermic mixing process ($h^E > 0$) absorbs heat, while an [exothermic process](@entry_id:147168) ($h^E  0$) releases heat. Crucially, the [excess enthalpy](@entry_id:173873) is not an independent quantity but is thermodynamically linked to the temperature dependence of the activity coefficients through the Gibbs-Helmholtz equation:

$$h^E = - R T^2 \sum_{i} x_i \left(\frac{\partial \ln \gamma_i}{\partial T}\right)_{P,x}$$

This powerful relation shows that if the activity coefficients of a mixture are temperature-dependent, there must be a non-zero heat of mixing. When a non-ideal liquid evaporates, the composition at the interface changes, which can be thought of as a continuous "unmixing" process. The energy associated with this unmixing contributes to the total energy required for [phase change](@entry_id:147324). The interfacial energy balance is therefore written as :

$$h(T_\infty - T_s) = \sum_i N_i \Delta h_{v,i}(T_s) + q_{\text{mix}}$$

Here, $N_i$ is the [molar flux](@entry_id:156263) of species $i$, $\Delta h_{v,i}$ is its molar latent heat of vaporization, and $q_{\text{mix}}$ represents the heat flux associated with non-[ideal mixing](@entry_id:150763) effects at the interface (related to $h^E$). This term effectively modifies the latent heat of the mixture. A proper description of a droplet's thermal behavior thus requires an activity coefficient model that accurately captures not only the composition dependence of VLE but also its temperature dependence.