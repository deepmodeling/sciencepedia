## Introduction
Heat transfer in [porous media](@entry_id:154591) is a fundamental process governing the performance of countless natural and engineered systems, from geothermal energy extraction to advanced electronics cooling. The intricate geometry of a porous structure, with its complex network of solid fibers and fluid-filled pores, makes a direct, pore-by-pore simulation of heat flow computationally intractable for most real-world applications. This creates a critical knowledge gap: how can we accurately and efficiently predict the bulk thermal behavior of these materials? The answer lies in [continuum modeling](@entry_id:169465), but the common assumption of [local thermal equilibrium](@entry_id:147993) (LTE), where solid and fluid share a single temperature, often fails in demanding scenarios.

This article addresses this challenge by providing a comprehensive overview of the Local Thermal Non-Equilibrium (LTNE) model, a more powerful framework where the solid and fluid phases can possess distinct, coexisting temperatures. Across three chapters, you will gain a deep understanding of this essential concept. First, "Principles and Mechanisms" will unpack the theoretical foundations of the LTNE model, starting from the volume-averaging technique used to upscale from the pore scale and leading to the development of the governing two-temperature equations. Next, "Applications and Interdisciplinary Connections" will bridge theory and practice by exploring how the LTNE model is applied to solve complex problems in high-performance heat exchangers, chemical reactors, and other advanced thermal systems. Finally, "Hands-On Practices" will offer concrete exercises to reinforce your understanding of [model parameterization](@entry_id:752079) and numerical implementation challenges. We begin by delving into the core principles that allow us to transition from the microscopic chaos of the pore space to an elegant and predictive macroscopic model.

## Principles and Mechanisms

The study of [heat transfer in porous media](@entry_id:156095) necessitates a transition from a microscopic description, where every solid fiber and fluid-filled pore is resolved, to a macroscopic continuum model that captures the bulk thermal behavior of the system. This upscaling is essential for practical engineering analysis, where resolving the intricate pore-scale geometry is computationally prohibitive. The principles of Local Thermal Non-Equilibrium (LTNE) are founded upon a rigorous methodology for this transition, known as [volume averaging](@entry_id:1133895).

### From Pore Scale to Continuum: The Volume Averaging Framework

At the heart of modeling [transport in porous media](@entry_id:756134) lies the concept of the **Representative Elementary Volume (REV)**. The REV is an intermediate volume scale, imagined at every macroscopic point $\mathbf{x}$ in the domain. Its size, $\ell_{REV}$, must be large enough to contain a statistically [representative sample](@entry_id:201715) of the pore structure, yet small enough to be considered a "point" with respect to the macroscopic length scale, $L$, over which bulk properties like temperature vary. This fundamental requirement is the **principle of scale separation**: $\ell_p \ll \ell_{REV} \ll L$, where $\ell_p$ is the characteristic pore size .

Within this REV, we can define macroscopic properties by averaging the corresponding microscopic fields. The most fundamental geometric property is the **porosity**, $\varepsilon$, defined as the fraction of the REV's total volume, $V$, that is occupied by the fluid phase, $V_f$:
$$
\varepsilon(\mathbf{x}) = \frac{V_f(\mathbf{x})}{V(\mathbf{x})}
$$
Consequently, the solid phase occupies a volume fraction of $(1-\varepsilon)$.

To describe the thermal state of the medium, we do not average the temperature over the entire REV. Instead, we define separate macroscopic temperatures for the fluid and solid phases. These are the **intrinsic phase-averaged temperatures**, which are the spatial averages of the microscopic temperature fields, $\theta_f$ and $\theta_s$, over their respective subdomains within the REV :
$$
T_f(\mathbf{x},t) = \frac{1}{V_f(\mathbf{x})} \int_{V_f(\mathbf{x})} \theta_f(\mathbf{y},t) \, \mathrm{d}V
$$
$$
T_s(\mathbf{x},t) = \frac{1}{V_s(\mathbf{x})} \int_{V_s(\mathbf{x})} \theta_s(\mathbf{y},t) \, \mathrm{d}V
$$
Here, $\mathbf{y}$ is the microscale coordinate within the REV centered at the macroscale point $\mathbf{x}$. These definitions produce two distinct, continuous temperature fields, $T_f(\mathbf{x},t)$ and $T_s(\mathbf{x},t)$, defined throughout the macroscopic domain. The core premise of Local Thermal Non-Equilibrium is that these two temperatures are not necessarily equal.

### The Two-Temperature Model

The condition that distinguishes LTNE from the simpler Local Thermal Equilibrium (LTE) model is precisely that $T_s(\mathbf{x},t) \neq T_f(\mathbf{x},t)$ . The adjective **local** in LTNE refers to this phenomenon occurring at the REV scale; at the same macroscopic location $\mathbf{x}$, the two coexisting continua—solid and fluid—can possess different temperatures because the heat exchange between them is not infinitely fast .

By applying the volume-averaging procedure to the fundamental microscale energy conservation laws for each phase, one derives a pair of coupled macroscopic energy equations. This **[two-temperature model](@entry_id:180856)** forms the basis of LTNE analysis . In the absence of [phase change](@entry_id:147324) and [internal heat generation](@entry_id:1126624), the general form of these equations is:

Solid phase:
$$
(1-\varepsilon) \rho_s c_{ps} \frac{\partial T_s}{\partial t} = \nabla \cdot (k_{s,\text{eff}} \nabla T_s) + h_{sf} a_{sf}(T_f - T_s)
$$

Fluid phase:
$$
\varepsilon \rho_f c_{pf} \frac{\partial T_f}{\partial t} + \rho_f c_{pf} \mathbf{u}_D \cdot \nabla T_f = \nabla \cdot (k_{f,\text{eff}} \nabla T_f) + h_{sf} a_{sf}(T_s - T_f)
$$

Here, $\rho_\beta$ and $c_{p\beta}$ are the density and [specific heat](@entry_id:136923) of phase $\beta \in \{f,s\}$, $k_{\beta,\text{eff}}$ are the effective thermal conductivities of each phase within the porous structure, and $\mathbf{u}_D$ is the superficial (or Darcy) velocity of the fluid.

Each equation is a statement of energy conservation for its respective continuum. The term on the left-hand side of the solid equation represents the rate of [thermal energy storage](@entry_id:1132994) in the solid matrix. For the fluid, the left-hand side includes both energy storage and [energy transport](@entry_id:183081) due to bulk fluid motion (advection). The first term on the right-hand side of each equation represents heat diffusion via conduction. The final term, the interfacial exchange term, is the heart of the LTNE model.

### Modeling Interfacial Heat Exchange

The volume-averaging process formally yields an integral term representing the net heat flux across the vast internal interface between the solid and fluid phases. This term depends on unresolved pore-scale details, creating a **closure problem**. To make the model tractable, this term must be expressed using the macroscopic variables $T_s$ and $T_f$ .

Under the assumption of scale separation, the standard closure model takes the form of Newton's law of cooling, postulating that the volumetric rate of heat exchange is proportional to the difference between the two phase temperatures :
$$
q'''_{sf} = h_{sf} a_{sf} (T_s - T_f)
$$
This term has the dimensions of a volumetric heat source, typically $\text{W}/\text{m}^3$ . Physically, it represents the rate of energy transfer from the solid to the fluid per unit of total porous medium volume. By the principle of energy conservation, this term must appear with opposite signs in the two energy equations: it is a source for the fluid ($+h_{sf} a_{sf} (T_s - T_f)$ if $T_s > T_f$) and an equal and opposite sink for the solid ($-h_{sf} a_{sf} (T_s - T_f)$, which is equivalent to $+h_{sf} a_{sf} (T_f - T_s)$) .

This closure introduces two crucial [phenomenological coefficients](@entry_id:183619):

The **interfacial [area density](@entry_id:636104)**, $a_{sf}$, is a purely geometric property of the porous medium, defined as the total solid-fluid interfacial area, $A_{sf}$, per unit of total REV volume, $V$. Its unit is $\text{m}^{-1}$. For a simple, idealized geometry such as a packed bed of identical spherical particles of diameter $d_p$, it can be shown that $a_{sf}$ is given by :
$$
a_{sf} = \frac{6(1-\varepsilon)}{d_p}
$$
This relation highlights that finer particles (smaller $d_p$) or lower porosity (denser packing) lead to a higher interfacial [area density](@entry_id:636104), providing more surface for heat exchange.

The **[interfacial heat transfer coefficient](@entry_id:153982)**, $h_{sf}$, is an effective transport coefficient with units of $\text{W}/(\text{m}^2 \cdot \text{K})$. It encapsulates all the complex physics of heat transfer at the pore scale, including conduction through the fluid and the effects of the local fluid velocity field (micro-convection) near the interface. It is not a simple material property but depends on the flow regime, often characterized by correlations involving the pore-scale Nusselt number .

The product $h_{sf} a_{sf}$ represents the volumetric coupling strength between the two phases. In the limit where this product becomes infinitely large ($h_{sf} a_{sf} \to \infty$), the thermal resistance between the phases vanishes. To maintain a finite heat flux, the temperature difference must approach zero ($T_s - T_f \to 0$). This is the mathematical limit where the LTNE model rigorously reduces to the single-temperature LTE model .

### Criteria for Non-Equilibrium: A Timescale Perspective

The practical decision of whether to use the simpler LTE model or the more complex LTNE model depends on the physical circumstances. The key to this decision lies in a comparison of the characteristic timescales governing the thermal processes . LTNE effects become significant when the time required for the two phases to thermally equilibrate with each other is comparable to, or longer than, the time over which the macroscopic temperature field is changing due to transport or external forcing.

We can define several key timescales:

1.  **Macroscopic Transport/Forcing Timescales ($t_{macro}$)**: These characterize how quickly temperature changes are imposed on the system. Examples include:
    -   **Advective Timescale**: The time for fluid to traverse the system, $t_{adv} \sim L/U$.
    -   **Diffusive Timescale**: The time for heat to conduct across the system, $t_{diff} \sim L^2/\alpha_{eff}$.
    -   **Forcing Timescale**: The characteristic time of a change in boundary conditions, such as the period of an oscillating inlet temperature, $t_{force} \sim 1/\omega$ .

2.  **Interphase Equilibration Timescales ($t_{int}$)**: These characterize the speed of heat exchange between the phases. We can look at this from the perspective of each phase's thermal inertia. The **[thermal relaxation time](@entry_id:148108)** for a phase is the ratio of its volumetric heat capacity to the volumetric [interfacial heat transfer coefficient](@entry_id:153982) :
    -   Solid Relaxation Time: $\tau_s = \frac{(1-\varepsilon)\rho_s c_{ps}}{h_{sf} a_{sf}}$
    -   Fluid Relaxation Time: $\tau_f = \frac{\varepsilon \rho_f c_{pf}}{h_{sf} a_{sf}}$

The LTE model is justified when $t_{int} \ll t_{macro}$. This means the phases equilibrate locally almost instantly compared to the rate at which the bulk temperature changes. Conversely, the LTNE model is necessary when $t_{int} \gtrsim t_{macro}$.

This [timescale analysis](@entry_id:262559) reveals several conditions that promote significant thermal non-equilibrium:

-   **High Thermal Inertia of One Phase**: A large disparity in thermal [relaxation times](@entry_id:191572), for example $\tau_s \gg \tau_f$, which occurs when the solid's heat capacity per unit volume is much greater than the fluid's, is a primary cause of LTNE. If a thermal transient occurs on a timescale $t_{force}$ such that $\tau_f \ll t_{force} \ll \tau_s$, the fluid temperature can respond to and track the change, while the high-inertia solid temperature lags significantly behind, creating a large and sustained temperature difference  .

-   **Rapid Transients**: A very fast external forcing ($t_{force}$ is small) makes it more likely that $t_{force} \lesssim t_{int}$, meaning neither phase can fully respond, and a temperature difference will develop. For example, applying a sinusoidal inlet temperature with a high frequency $\omega$ can drive the system into LTNE, even if it would be in equilibrium under steady conditions .

-   **High Flow Velocities**: While a higher fluid velocity $U$ often increases the [interfacial heat transfer coefficient](@entry_id:153982) $h_{sf}$ (which tends to reduce $t_{int}$), it also dramatically reduces the advective timescale $t_{adv} = L/U$. In many systems, the reduction in $t_{adv}$ is more significant, causing the ratio $t_{int}/t_{adv}$ to increase. This means the fluid is swept through the domain too quickly to exchange sufficient heat with the solid, leading to stronger non-equilibrium effects. This counter-intuitive result highlights the importance of comparing all relevant timescales .

-   **Low Interfacial Coupling**: A low value of the product $h_{sf}a_{sf}$, due to either poor heat transfer at the interface or a small [specific surface area](@entry_id:158570) (e.g., large particles), directly increases the equilibration time $t_{int}$ and promotes LTNE .

It is crucial to recognize that transport mechanisms *within* a phase, such as high solid thermal conductivity $k_s$, do not guarantee inter-phase equilibrium. High $k_s$ may ensure a solid particle is nearly isothermal, but it does not eliminate the thermal resistance at the fluid-solid interface that gives rise to the temperature difference $T_s-T_f$ .

### Quantifying Non-Equilibrium with Dimensionless Numbers

The timescale comparisons can be formalized through [nondimensionalization](@entry_id:136704) of the governing equations. This process yields dimensionless groups that quantify the relative importance of different physical mechanisms.

In an **advection-dominated** system, the key competition is between the rate of heat advected by the fluid and the rate of heat exchanged with the solid. Nondimensionalizing the fluid [energy equation](@entry_id:156281) reveals a dimensionless group, a form of Stanton number, that governs this balance :
$$
\Pi = \frac{h_{sf} a_{sf} L}{\rho_f c_{pf} U} = \frac{L/U}{\rho_f c_{pf} / (h_{sf} a_{sf})} = \frac{\tau_{conv}}{\tau_{exch}}
$$
This parameter is the ratio of the convective residence timescale to the fluid's thermal exchange timescale. When $\Pi \gg 1$, the fluid resides in the system long enough to equilibrate with the solid, and LTE is approached. When $\Pi \ll 1$, advection is too fast for significant exchange, and strong LTNE prevails.

In a **conduction-dominated** system (negligible flow), the competition is between heat conduction through the porous medium and interfacial exchange. Nondimensionalization of the [two-temperature model](@entry_id:180856) yields the **phase exchange Biot number** :
$$
\mathrm{Bi}_{sf} = \frac{h_{sf} a_{sf} L^2}{k_{eff}} = \frac{L^2 / \alpha_{eff}}{(\rho c)_{eff} / (h_{sf} a_{sf})} = \frac{\tau_{cond}}{\tau_{ex}}
$$
where $k_{eff}$ and $\alpha_{eff}$ are an [effective thermal conductivity](@entry_id:152265) and diffusivity for the composite medium. This number compares the characteristic time for heat to conduct across the domain to the time for the phases to equilibrate. When $\mathrm{Bi}_{sf} \gg 1$, interphase exchange is fast compared to macroscopic conduction, and the system behaves as if in LTE. When $\mathrm{Bi}_{sf} \ll 1$, local temperature differences persist because heat cannot be exchanged between phases as fast as it is redistributed by conduction, necessitating an LTNE model.

These dimensionless parameters provide a powerful and concise way to predict the thermal behavior of a porous medium, encapsulating the complex interplay of geometry, material properties, and flow conditions that determine the extent of [local thermal non-equilibrium](@entry_id:149868).