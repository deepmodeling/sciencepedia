## Introduction
Thermal energy storage (TES) is a cornerstone technology for creating flexible, efficient, and sustainable energy systems. By bridging the temporal gap between energy availability and demand, TES enhances the integration of renewable sources and improves the performance of industrial processes and buildings. However, harnessing its full potential requires the ability to accurately predict and optimize its behavior, a task that hinges on robust mathematical modeling. This article provides a comprehensive guide to TES modeling, addressing the need for a structured understanding that connects first principles to real-world engineering challenges.

The journey begins in the "Principles and Mechanisms" chapter, where we will build a solid foundation based on thermodynamics and transport phenomena, deriving the governing equations for various storage types. Next, the "Applications and Interdisciplinary Connections" chapter will demonstrate how these models are applied to design high-performance components and optimize the economic operation of TES within larger energy systems, revealing surprising connections to other scientific fields. Finally, the "Hands-On Practices" section provides an opportunity to solidify this knowledge by tackling concrete modeling problems. This structured exploration will equip you with the essential tools to analyze, design, and innovate in the vital field of thermal energy storage.

## Principles and Mechanisms

The modeling of thermal energy storage (TES) systems is fundamentally grounded in the principles of thermodynamics and transport phenomena. A robust model must accurately capture the dynamics of energy transfer and storage, which involves understanding the interplay of various physical mechanisms. This chapter elucidates these core principles, beginning with the modes of heat transfer that govern energy exchange with the surroundings, progressing through the dynamic modeling of thermal response, delving into the thermodynamics of different storage media, and concluding with a second-law analysis of system efficiency.

### Fundamental Modes of Heat Transfer

The transfer of thermal energy is quantified by the **heat flux**, denoted by the vector $\mathbf{q}$, which represents the rate of energy transfer per unit area. In the context of TES, three primary mechanisms govern the movement of heat: conduction, convection, and radiation. The dominance of each mechanism depends critically on the material properties, geometry, and thermodynamic state of the system.

**Conduction** is the transfer of heat through a stationary medium, driven by a temperature gradient. In solids, this occurs via lattice vibrations (phonons) and the migration of free electrons. The constitutive relation for conduction is **Fourier's Law**, which states that the heat flux is proportional to the negative of the temperature gradient:

$$
\mathbf{q}_{\text{cond}} = -k\nabla T
$$

Here, $k$ is the **thermal conductivity** of the material, a transport property measured in $\mathrm{W}\cdot\mathrm{m}^{-1}\cdot\mathrm{K}^{-1}$ that quantifies the material's ability to conduct heat. The negative sign ensures that heat flows from regions of higher temperature to regions of lower temperature, in accordance with the Second Law of Thermodynamics.

**Convection** is the transfer of heat between a surface and a moving fluid (gas or liquid). This mode combines the effects of conduction at the fluid-solid interface and bulk fluid motion, known as advection. The governing empirical relation is **Newton's Law of Cooling**:

$$
q_{\text{conv}} = h(T_s - T_\infty)
$$

In this expression, $q_{\text{conv}}$ is the heat flux from the surface, $T_s$ is the surface temperature, and $T_\infty$ is the bulk temperature of the fluid far from the surface. The **convective heat transfer coefficient**, $h$, given in $\mathrm{W}\cdot\mathrm{m}^{-2}\cdot\mathrm{K}^{-1}$, is a complex parameter that encapsulates the fluid properties, flow velocity, and geometry of the surface. It is typically much higher for forced convection (e.g., pumped fluid) than for natural convection (buoyancy-driven flow).

**Radiation** is the transfer of energy via electromagnetic waves (or photons) emitted by matter due to its temperature. Unlike conduction and convection, radiation does not require a medium and can occur across a vacuum. For a "diffuse-gray" surface (one that emits and absorbs radiation uniformly in all directions and over all wavelengths), the net radiative heat flux from a surface at temperature $T_s$ to large surroundings at temperature $T_{\text{sur}}$ is given by the **Stefan-Boltzmann Law**:

$$
q_{\text{rad}} = \epsilon\sigma(T_s^4 - T_{\text{sur}}^4)
$$

Here, $\sigma$ is the Stefan-Boltzmann constant ($\approx 5.67 \times 10^{-8}\,\mathrm{W}\cdot\mathrm{m}^{-2}\cdot\mathrm{K}^{-4}$), and $\epsilon$ is the **emissivity** of the surface, a dimensionless property ($0 \le \epsilon \le 1$) representing the ratio of the surface's radiative power to that of an ideal blackbody at the same temperature.

The relative importance of these three modes is highly dependent on the operating conditions of the TES system [@problem_id:4130029]. For example, in low-temperature applications (e.g., $T_s \approx 350\,\mathrm{K}$), conduction and natural convection often dominate heat loss. As the storage temperature increases (e.g., $T_s = 600\,\mathrm{K}$), the $T^4$ dependence of radiation causes it to become a significant, and often dominant, mode of heat transfer. In high-temperature storage systems or applications in vacuum environments where convection is absent, radiation becomes the principal mechanism of heat exchange with the surroundings. Conversely, in systems with aggressive fluid flow, such as a liquid-cooled battery pack, high convective heat transfer coefficients can make forced convection the dominant mode, even at moderate temperatures [@problem_id:4130029].

### System Dynamics: From Lumped to Distributed Models

Modeling the transient behavior of a TES unit requires solving an energy balance equation over time. The complexity of this model depends on the spatial temperature variations within the storage element.

#### The Lumped Capacitance Model

For systems where internal temperature gradients are negligible, the entire TES element can be treated as a single node with a uniform, time-varying temperature, $T(t)$. This is known as the **lumped capacitance model**. It is derived from the First Law of Thermodynamics for a fixed-mass control volume, which states that the rate of change of internal energy equals the net rate of heat transfer into the system:

$$
\frac{dE}{dt} = \dot{Q}_{\text{net}}
$$

For a solid or an incompressible fluid, the change in internal energy is related to the change in temperature via the **thermal capacitance**, $C_{\text{th}} = mc_p$, where $m$ is the mass and $c_p$ is the specific heat capacity. The net heat rate is the sum of any heat input, $\dot{Q}_{\text{in}}(t)$, and heat exchange with the environment, typically through convection, $-\dot{Q}_{\text{loss}} = -UA(T - T_\infty)$, where $UA$ represents the overall heat transfer coefficient-area product. Combining these terms yields the governing first-order ordinary differential equation (ODE) for the lumped model [@problem_id:4130052]:

$$
C_{\text{th}} \frac{dT}{dt} = \dot{Q}_{\text{in}}(t) - UA(T - T_\infty)
$$

This model describes a first-order dynamic system whose response to a step change in heat input is an exponential approach to a new steady-state temperature. The characteristic time of this response is the **thermal time constant**, $\tau = C_{\text{th}} / (UA) = (mc_p)/(UA)$, which represents the time required for the system to reach approximately $63.2\%$ of its total temperature change. For instance, if a system at $T_\infty$ is suddenly subjected to a constant heat input $Q_0$, its temperature evolves as [@problem_id:4130052]:

$$
T(t) = T_{\infty} + \frac{Q_{0}}{UA} \left( 1 - \exp\left(-\frac{t}{\tau}\right) \right)
$$

#### The Criterion for Lumped Analysis: The Biot Number

The validity of the simple lumped capacitance model hinges on the assumption of a spatially uniform internal temperature. The question of when this assumption is justified is answered by comparing the resistance to heat conduction *within* the body to the resistance to heat convection *at its surface*. This ratio is quantified by a dimensionless parameter called the **Biot number**, $Bi$ [@problem_id:4130059].

The Biot number is defined as:

$$
\mathrm{Bi} = \frac{hL_c}{k}
$$

where $h$ is the convective heat transfer coefficient, $k$ is the thermal conductivity of the solid, and $L_c$ is a characteristic length of the body (often defined as the volume divided by the surface area, $L_c = V/A$). The Biot number can be interpreted as the ratio of internal conductive resistance to external convective resistance:

$$
\mathrm{Bi} = \frac{R_{\text{cond}}}{R_{\text{conv}}} = \frac{L_c/k}{1/h}
$$

A small Biot number ($Bi \ll 1$, typically taken as $Bi  0.1$) implies that the internal resistance to heat flow is much smaller than the external resistance. Heat diffuses very quickly within the object compared to the rate at which it is exchanged with the surroundings. Consequently, any temperature gradients inside the body are small, and the lumped capacitance model provides an accurate approximation of the system's transient behavior [@problem_id:4130059].

#### The Distributed Model and the Fourier Number

When the Biot number is not small ($Bi \gtrsim 0.1$), internal temperature gradients are significant, and the lumped model is no longer valid. In this case, the temperature is a function of both space and time, $T(\mathbf{x}, t)$, and we must solve the partial differential equation for heat conduction, known as the **heat diffusion equation**. For one-dimensional conduction in a slab with constant properties, this equation is [@problem_id:4129978] [@problem_id:4130009]:

$$
\frac{\partial T}{\partial t} = \alpha \frac{\partial^2 T}{\partial x^2}
$$

Here, $\alpha = k/(\rho c_p)$ is the **thermal diffusivity** (in $\mathrm{m}^2/\mathrm{s}$), which measures the material's ability to conduct heat relative to its capacity to store it.

The dynamics of transient conduction are governed by another critical dimensionless parameter, the **Fourier number**, $Fo$. By nondimensionalizing the heat equation, the Fourier number emerges as the dimensionless time variable [@problem_id:4130009]:

$$
\mathrm{Fo} = \frac{\alpha t}{L_c^2}
$$

The Fourier number represents the ratio of the elapsed physical time, $t$, to the characteristic timescale for heat diffusion across the length $L_c$. It provides a measure of how far a thermal perturbation has penetrated into the body.
- If $Fo \ll 1$, heat has only penetrated a short distance, and the core of the object is unaffected by boundary changes.
- If $Fo \approx 1$, the thermal front has propagated through the entire body, and the temperature profile is fully transient. The condition $Fo=1$ marks the point where the elapsed time equals the characteristic diffusion time, $t = L_c^2/\alpha$ [@problem_id:4130009].
- If $Fo \gg 1$, the system is approaching a steady-state temperature profile.

#### Boundary Conditions for Distributed Models

To obtain a unique solution for the heat diffusion equation, one must specify conditions at the physical boundaries of the domain. These **boundary conditions** mathematically describe the thermal interaction of the TES element with its environment. There are three fundamental types [@problem_id:4130055]:

1.  **Dirichlet Condition (Type 1):** The temperature at the boundary is prescribed as a function of time, $T(0, t) = T_s(t)$. This applies when the surface is in contact with a high-capacity thermal reservoir, such as a boiling fluid or a large, thermostatically controlled plate.

2.  **Neumann Condition (Type 2):** The heat flux normal to the boundary is prescribed, $-k \frac{\partial T}{\partial x}\big|_{x=0} = q_0''(t)$. This is used for surfaces with a known heating rate (e.g., from an electric heater or solar radiation) or for perfectly insulated (adiabatic) surfaces, where the flux is zero: $\frac{\partial T}{\partial x}\big|_{x=0} = 0$.

3.  **Robin Condition (Type 3 or Mixed):** A relationship between the boundary temperature and its gradient is specified. The most common example is convection at the surface, where the conductive flux from the interior equals the convective flux to the surroundings: $-k \frac{\partial T}{\partial x}\big|_{x=L} = h[T(L,t) - T_\infty]$.

When nondimensionalized, the Robin condition naturally reveals the Biot number, linking the governing PDE to its boundary interactions [@problem_id:4129978]. The dimensionless form of the Robin condition becomes $-\frac{\partial \theta}{\partial x^*}\big|_{x^*=1} = \mathrm{Bi} \cdot \theta(1, t^*)$, elegantly demonstrating that the Biot number controls the balance between internal energy transport and boundary exchange in distributed systems.

### Thermodynamic Principles of Storage Media

The effectiveness of a TES system is intrinsically tied to the thermodynamic properties of the storage medium. Energy can be stored as sensible heat, latent heat, or thermochemical potential.

#### Latent Heat Storage in Phase Change Materials (PCMs)

While sensible heat storage involves changing a material's temperature, **latent heat storage** utilizes the enthalpy of phase transition (e.g., solid to liquid) to store large amounts of energy at a nearly constant temperature. Materials used for this purpose are known as **Phase Change Materials (PCMs)**.

For a constant-pressure process, the heat added to a system is equal to the change in its specific enthalpy, $h$. The total enthalpy of a PCM can be modeled as the sum of its sensible and latent components [@problem_id:4130068]. For a PCM that melts over a temperature range $[T_s, T_l]$ (a "mushy" zone), the enthalpy is given by:

$$
h(T) = h(T_{\text{ref}}) + \int_{T_{\text{ref}}}^T c_p(\theta) d\theta + \chi(T)L
$$

Here, the integral term represents the accumulated sensible heat, $L$ is the latent heat of fusion, and $\chi(T)$ is the **phase fraction** (the mass fraction of liquid), which smoothly increases from $0$ to $1$ as the temperature rises from the solidus ($T_s$) to the liquidus ($T_l$).

This formulation leads to the **apparent heat capacity method**, where the rate of enthalpy change is expressed in terms of a temperature derivative. The apparent (or effective) heat capacity, $c_{\text{eff}}$, is defined as:

$$
c_{\text{eff}}(T) = \frac{dh}{dT} = c_p(T) + L\frac{d\chi}{dT}
$$

This expression shows that the latent heat absorption is modeled as a large peak in the heat capacity within the melting range, capturing the high energy storage density of the phase transition [@problem_id:4130068].

For numerical modeling, two primary strategies exist: the **enthalpy method** and the **effective heat capacity method**. The enthalpy method solves the energy equation using $h$ as the primary variable and recovers temperature from the $T(h)$ relationship. This approach is inherently conservative, ensuring that latent heat is perfectly accounted for within each control volume, and can sharply resolve the phase front [@problem_id:4130045]. The effective heat capacity method solves for $T$ directly but introduces an artificial melting temperature range $\Delta T$ to avoid the singularity in $c_{\text{eff}}$ for pure substances. While simpler to implement in some codes, this method can diffuse the phase front and may fail to conserve energy if the time steps are too large relative to $\Delta T$, a phenomenon known as "latent heat skipping" [@problem_id:4130045].

#### Thermochemical Energy Storage (TCES)

**Thermochemical Energy Storage (TCES)** utilizes reversible chemical reactions to store and release energy. An endothermic reaction absorbs heat to break chemical bonds, storing energy in the products. The reverse, exothermic reaction releases this heat on demand. TCES offers very high energy densities and the potential for long-term storage with minimal heat loss.

Modeling TCES requires understanding chemical thermodynamics and reaction equilibrium. For a reversible gas-phase reaction like $A \rightleftharpoons 2B$, the composition of the mixture at equilibrium depends on temperature and pressure. The equilibrium state is governed by the **equilibrium constant**, $K_p$, which is related to the standard Gibbs free energy of reaction, $\Delta G^\circ$:

$$
\Delta G^\circ = -RT \ln K_p
$$

Since $\Delta G^\circ = \Delta H^\circ - T\Delta S^\circ$, where $\Delta H^\circ$ and $\Delta S^\circ$ are the standard enthalpy and entropy of reaction, we can write the van 't Hoff relation:

$$
\ln K_p = -\frac{\Delta H^\circ}{RT} + \frac{\Delta S^\circ}{R}
$$

This equation shows that for an endothermic reaction ($\Delta H^\circ > 0$), increasing the temperature shifts the equilibrium towards the products, thereby storing more energy. The equilibrium constant is also related to the partial pressures of the reactants and products through the law of mass action. By combining these thermodynamic relationships, one can derive an expression for the equilibrium **conversion**, $X$, which quantifies the state of charge of the TCES system as a function of temperature and pressure [@problem_id:4129984].

### Second Law Analysis: Quantifying Irreversibility

While the First Law governs energy conservation, the Second Law of Thermodynamics addresses energy *quality* and the inherent inefficiencies in thermal processes. All real-world processes, including heat transfer across a finite temperature difference, are irreversible and result in the generation of **entropy**.

The total entropy generation rate, $\dot{S}_{\text{gen}}$, for a process where heat $\dot{Q}$ is transferred from a hot boundary at $T_s$ to a cold ambient at $T_\infty$ is given by [@problem_id:4130008]:

$$
\dot{S}_{\text{gen}} = \dot{Q}\left(\frac{1}{T_\infty} - \frac{1}{T_s}\right)
$$

This entropy generation represents a loss of thermodynamic potential. This loss is more formally quantified by **exergy**, or availability, which is the maximum theoretical useful work that can be obtained from a system as it comes into equilibrium with a reference environment at temperature $T_0$. Irreversibilities destroy exergy. According to the **Gouy-Stodola theorem**, the rate of exergy destruction, $\dot{B}_{\text{destroyed}}$, is directly proportional to the rate of entropy generation:

$$
\dot{B}_{\text{destroyed}} = T_0 \dot{S}_{\text{gen}}
$$

For the heat transfer process above, with the reference environment being the ambient itself ($T_0 = T_\infty$), the exergy destruction rate becomes [@problem_id:4130008]:

$$
\dot{B}_{\text{destroyed}} = T_\infty \left[\dot{Q}\left(\frac{1}{T_\infty} - \frac{1}{T_s}\right)\right] = \dot{Q}\left(1 - \frac{T_\infty}{T_s}\right)
$$

This quantity, also known as the Carnot heat engine efficiency factor applied to the heat loss $\dot{Q}$, represents the rate at which the potential to do useful work is irrecoverably lost. Minimizing exergy destruction by reducing temperature differences and other irreversibilities is a key goal in the design of efficient thermal energy storage systems.