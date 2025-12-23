## Introduction
Sprays are central to countless engineering systems, from gas turbines and rocket engines to industrial furnaces and [pharmaceutical production](@entry_id:193177). Simulating these complex multiphase flows presents a significant challenge, requiring a framework that can capture the intricate interplay between a continuous gas phase and a dispersed liquid phase. The Eulerian-Eulerian (EE) [two-fluid model](@entry_id:139846) offers a powerful and computationally efficient approach by treating both phases as interpenetrating continua, each governed by its own set of conservation laws. This article addresses the knowledge gap between the abstract mathematical formulation of the EE model and its practical application, providing a detailed guide to its principles, uses, and implementation challenges.

Across the following chapters, you will gain a robust understanding of this versatile modeling technique. The first chapter, **"Principles and Mechanisms,"** lays the theoretical groundwork, explaining the concept of interpenetrating continua, deriving the averaged [conservation equations](@entry_id:1122898), and justifying critical modeling choices like the single-pressure assumption through [timescale analysis](@entry_id:262559). The second chapter, **"Applications and Interdisciplinary Connections,"** demonstrates the model's utility by exploring its application in [spray combustion](@entry_id:1132216), discussing advanced [closure models](@entry_id:1122505) for phenomena like droplet breakup and multi-component evaporation, and examining its connection to fields like turbulence theory. Finally, the third chapter, **"Hands-On Practices,"** provides a set of targeted problems designed to solidify your understanding of numerical implementation, [interphase](@entry_id:157879) physics, and the practical aspects of setting up a stable and accurate simulation. This structured journey will equip you with the knowledge to effectively deploy the Eulerian-Eulerian model for complex spray simulations.

## Principles and Mechanisms

The Eulerian-Eulerian [two-fluid model](@entry_id:139846) provides a powerful and computationally tractable framework for simulating multiphase flows such as sprays, where a [dispersed phase](@entry_id:748551) (liquid droplets) interacts with a continuous phase (gas). This approach avoids the high computational cost of tracking individual droplets, as is done in Lagrangian methods, by treating both phases as fully interpenetrating continua. Each continuum has its own set of field variables and governing equations defined at every point in the domain. This chapter elucidates the fundamental principles upon which this model is built and the key mechanisms that govern its behavior.

### The Interpenetrating Continua Concept

The conceptual cornerstone of the two-fluid model is the treatment of distinct phases as **interpenetrating continua**. Imagine a control volume within the spray that is large enough to contain many droplets but small enough relative to the overall scale of the combustor. Within this volume, both gas and liquid are present. Instead of describing the complex, sharp interface between them, we define averaged properties for each phase that are continuous functions of space and time.

To formalize this, we can begin at the microscopic level with a **phase [indicator function](@entry_id:154167)**, $\chi_k(\mathbf{x}, t)$. This function is defined to be $1$ if the point $(\mathbf{x}, t)$ is occupied by phase $k$, and $0$ otherwise. For a two-phase system of gas ($g$) and liquid ($\ell$) with no voids, at any microscopic point, it must be that one phase or the other is present. This leads to the microscopic identity :
$$
\chi_g(\mathbf{x}, t) + \chi_\ell(\mathbf{x}, t) = 1
$$
This statement asserts that the two phases are **mutually exclusive** (a point cannot be both gas and liquid) and **[collectively exhaustive](@entry_id:262286)** (the entire volume is filled by either gas or liquid).

The macroscopic fields of the Eulerian-Eulerian model are obtained by applying a local averaging operator, denoted by $\langle \cdot \rangle$, over a spatio-temporal volume. The most fundamental of these fields is the **phase [volume fraction](@entry_id:756566)**, $\alpha_k$, defined as the average of the [indicator function](@entry_id:154167):
$$
\alpha_k(\mathbf{x}, t) = \langle \chi_k(\mathbf{x}, t) \rangle
$$
The [volume fraction](@entry_id:756566) $\alpha_k$ represents the fraction of volume occupied by phase $k$ within the averaging region around point $\mathbf{x}$. By applying the averaging operator to the microscopic identity and leveraging the linearity of averaging, we obtain a crucial macroscopic constraint [@problem_id:4023883, @problem_id:4023919]:
$$
\alpha_g(\mathbf{x}, t) + \alpha_\ell(\mathbf{x}, t) = \langle \chi_g + \chi_\ell \rangle = \langle 1 \rangle = 1
$$
This identity, $\alpha_g + \alpha_\ell = 1$, is a purely geometric [closure relation](@entry_id:747393) that must hold at every point in the domain for a two-phase system. It is a direct consequence of how space is partitioned at the microscale and does not depend on dynamic assumptions like [incompressibility](@entry_id:274914), [phase change](@entry_id:147324), or kinematic equilibrium.

Other phasic properties are defined as intrinsic, or phase-conditional, averages. For a general property $\psi_k$, its macroscopic field is defined as $\langle \chi_k \psi_k \rangle / \langle \chi_k \rangle$. This leads to the definition of the macroscopic fields for each phase $k$:
-   **Intrinsic density** $\rho_k$: The material density of the substance in phase $k$.
-   **Phasic velocity** $\mathbf{u}_k$: The [average velocity](@entry_id:267649) of the material in phase $k$.
-   **Phasic temperature** $T_k$: The average temperature of the material in phase $k$.

The interpenetrating continua assumption means that for any computational cell, both phases can coexist. The model solves for two sets of fields—$(\alpha_g, \rho_g, \mathbf{u}_g, T_g)$ and $(\alpha_\ell, \rho_\ell, \mathbf{u}_\ell, T_\ell)$—at each point in space. This allows for phenomena like **slip**, where $\mathbf{u}_g \neq \mathbf{u}_\ell$, and thermal non-equilibrium, where $T_g \neq T_\ell$, which are critical in describing spray dynamics.

### The Averaged Conservation Equations

With the macroscopic fields defined, a set of [conservation equations](@entry_id:1122898) for mass, momentum, and energy is formulated for each phase. These equations are derived by averaging the local, instantaneous conservation laws over a control volume.

#### Mass Conservation

The conservation of mass for phase $k$ is expressed by the phasic continuity equation. The mass of phase $k$ per unit *mixture* volume is the phasic density, $\alpha_k \rho_k$. The transport of this quantity is governed by the phasic velocity $\mathbf{u}_k$. The equation takes the form :
$$
\frac{\partial}{\partial t}(\alpha_k \rho_k) + \nabla \cdot (\alpha_k \rho_k \mathbf{u}_k) = \Gamma_k
$$
Here, $\Gamma_k$ is the volumetric mass source term, representing the rate of [mass transfer](@entry_id:151080) into phase $k$ per unit volume (in units of $\mathrm{kg} \cdot \mathrm{m}^{-3} \cdot \mathrm{s}^{-1}$). For a spray undergoing evaporation, mass is transferred from the liquid phase to the gas phase. By convention, a source term is positive when mass is added to a phase. Therefore, during evaporation, the liquid phase loses mass ($\Gamma_\ell  0$) and the gas phase gains mass ($\Gamma_g > 0$). In a closed system without external mass sources, total mass is conserved, which requires the [interphase mass transfer](@entry_id:151239) terms to sum to zero:
$$
\Gamma_g + \Gamma_\ell = 0 \quad \implies \quad \Gamma_g = -\Gamma_\ell
$$
Summing the continuity equations for both phases recovers the mixture continuity equation, where the total mass source is zero .

#### Momentum and Energy Conservation

Similarly, [conservation equations](@entry_id:1122898) are derived for momentum and energy. The phasic momentum equation for phase $k$ is:
$$
\frac{\partial}{\partial t}(\alpha_k \rho_k \mathbf{u}_k) + \nabla \cdot (\alpha_k \rho_k \mathbf{u}_k \mathbf{u}_k) = -\alpha_k \nabla p + \nabla \cdot \boldsymbol{\tau}_k + \alpha_k \rho_k \mathbf{g} + \mathbf{M}_k + \Gamma_k \mathbf{u}_{k,i}
$$
The terms on the right-hand side represent, respectively, the pressure gradient force, the viscous stress force, the gravitational body force, the [interphase](@entry_id:157879) momentum exchange (e.g., drag), and the momentum advected due to [phase change](@entry_id:147324) (where $\mathbf{u}_{k,i}$ is the velocity at the interface).

The phasic energy equation takes a similar form, accounting for heat conduction, work done by pressure and [viscous forces](@entry_id:263294), and [interphase](@entry_id:157879) heat exchange. A key challenge in the [two-fluid model](@entry_id:139846) is the formulation of physically accurate closure relations for the [interphase](@entry_id:157879) exchange terms ($\Gamma_k$, $\mathbf{M}_k$, and the energy exchange $Q_k$), as well as justifying simplifying assumptions about the pressure and temperature fields.

### Interphase Coupling and Mechanical Equilibrium

A pivotal modeling decision in the two-fluid framework concerns the treatment of pressure. While one could, in principle, solve for two separate pressure fields, $p_g$ and $p_\ell$, the vast majority of models for sprays employ a **single, shared pressure field**, $p$. This reduces the complexity from a seven-equation model (adding a transport equation for $\alpha_\ell$) to a six-equation model and resolves mathematical difficulties related to ill-posedness.

The justification for this assumption rests on a separation of characteristic timescales . In a typical spray system, the time required for pressure information to propagate across a computational cell of size $L$ is the **acoustic timescale**, $\tau_{ac} \sim L/c_g$, where $c_g$ is the gas-phase speed of sound. In contrast, the time for a droplet to respond to changes in the gas flow due to drag is the **particle momentum relaxation time**, $\tau_p$. For a fine spray with droplets of diameter $d_\ell \approx 2 \times 10^{-5}\, \mathrm{m}$ in a combustor environment, $\tau_{ac}$ is on the order of microseconds, while $\tau_p$ is on the order of milliseconds. Since $\tau_{ac} \ll \tau_p$, pressure equilibrates between the phases almost instantaneously compared to the time it takes for their velocities to equilibrate. This provides a strong physical basis for assuming a state of local [mechanical equilibrium](@entry_id:148830) in pressure ($p_g \approx p_\ell = p$), even while the velocities remain distinct ($\mathbf{u}_g \neq \mathbf{u}_\ell$).

A more rigorous analysis based on acoustics reinforces this conclusion . For an acoustic wave of frequency $\omega$ propagating through the spray, two conditions must be met. First, the droplet diameter $d$ must be much smaller than the acoustic wavelength $\lambda_g$, a condition expressed non-dimensionally as $kd \ll 1$, where $k=\omega/c_g$ is the wavenumber. This ensures the droplet experiences a spatially uniform external pressure. Second, the time for pressure waves to traverse the droplet's interior, $\sim d/c_\ell$, must be much shorter than the acoustic period, expressed as $\omega d/c_\ell \ll 1$. When these conditions hold, as they do for typical acoustic frequencies in combustors and micron-sized droplets, the pressure gradient across both phases becomes identical. Even though the absolute pressures may differ due to surface tension (the Laplace pressure, $p_\ell - p_g = 4\sigma/d$), this difference is spatially constant for a monodisperse spray, and its gradient is zero. Thus, $\nabla p_\ell = \nabla p_g$, justifying the use of a single pressure gradient term $-\alpha_k \nabla p$ in each momentum equation.

More complex formulations, such as the **Baer-Nunziato model**, do solve for separate phasic pressures but include a source term that models the relaxation of $p_g$ towards $p_\ell$. In the limit where the pressure relaxation time is very short—the "stiff" limit applicable to most sprays—these advanced models asymptotically reduce to the simpler and more common single-pressure model .

### Interphase Coupling and Thermal Equilibrium

A similar decision must be made for the temperature fields: should one assume [local thermal equilibrium](@entry_id:147993) ($T_g = T_\ell$) and solve a single mixture [energy equation](@entry_id:156281), or solve separate energy equations for each phase? The answer, again, lies in a comparison of timescales . The key comparison is between the **flow residence time**, $\tau_{res}$, and the **droplet [thermal equilibration](@entry_id:1132996) time**, $\tau_{th}$.

If $\tau_{th} \ll \tau_{res}$, the droplets have ample time to reach the same temperature as the surrounding gas, and a shared temperature model is justified. If $\tau_{th}$ is comparable to or larger than $\tau_{res}$, significant temperature differences will persist, mandating the use of two separate energy equations.

The [thermal equilibration](@entry_id:1132996) time $\tau_{th}$ is determined by two resistances in series: the external convective heat transfer from the gas to the droplet surface and the internal conductive heat transfer within the droplet. The relative importance of these resistances is quantified by the **Biot number**, $\mathrm{Bi} = hL_c/k_\ell$, where $h$ is the convective heat transfer coefficient, $L_c$ is a characteristic length (e.g., $d/6$ for a sphere), and $k_\ell$ is the liquid thermal conductivity.

-   If $\mathrm{Bi} \ll 0.1$, internal resistance is negligible. The droplet is nearly isothermal, and the equilibration time is governed by convection: $\tau_{th} \approx \tau_{conv} = (\rho_\ell c_{p,\ell} d) / (6h)$.
-   If $\mathrm{Bi}  0.1$, internal temperature gradients are significant. The internal conduction time, $\tau_{cond} \sim d^2/\alpha_\ell$ (where $\alpha_\ell$ is the liquid thermal diffusivity), becomes important and often rate-limiting. The total equilibration time $\tau_{th}$ is then a combination of $\tau_{conv}$ and $\tau_{cond}$.

For instance, consider a $50\,\mu\mathrm{m}$ n-dodecane droplet in a hot air stream flowing through a $0.5\,\mathrm{m}$ duct with a residence time of $\tau_{res} = 50\,\mathrm{ms}$. A detailed calculation  reveals a Biot number of approximately $0.24$, indicating that internal conduction is not negligible. The characteristic time for internal conduction is about $7.7\,\mathrm{ms}$, which is a significant fraction of the $50\,\mathrm{ms}$ residence time. Therefore, in this practical scenario, the assumption of thermal equilibrium is invalid, and separate energy equations are required to accurately capture the physics of droplet heating.

### Two-Way Coupling and Turbulence Modulation

The Eulerian-Eulerian framework is inherently a **two-way coupled** model. This means it not only accounts for the effect of the gas on the droplets (e.g., drag force causing acceleration) but also for the reciprocal effect of the droplets on the gas. This back-reaction is captured by the equal-and-opposite nature of the [interphase](@entry_id:157879) exchange terms . For momentum, the total force exerted by the gas on the liquid, $\mathbf{M}_\ell$, is accompanied by an opposite reaction force on the gas, $\mathbf{M}_g = -\mathbf{M}_\ell$. This ensures that the total momentum of the mixture is conserved.

A critical aspect of two-way coupling in turbulent flows is **[turbulence modulation](@entry_id:756227)**. The presence of droplets can significantly alter the turbulence structure of the carrier gas, either enhancing it (e.g., through wake shedding behind large droplets) or attenuating it (e.g., by acting as an inertial sink for the kinetic energy of small eddies). In turbulence modeling frameworks like Reynolds-Averaged Navier-Stokes (RANS) or Large-Eddy Simulation (LES), this effect appears as additional source or sink terms in the transport equations for turbulence quantities.

For example, in a RANS model, the transport equation for the gas-phase turbulent kinetic energy, $k_g$, will contain a source term arising from the correlation between the fluctuating gas velocity, $\mathbf{u}'_g$, and the fluctuating [interphase momentum transfer](@entry_id:750762), $\mathbf{f}'_{gl}$. This term, which can be written as $S_k^{ip} = -\overline{\mathbf{u}'_g \cdot \mathbf{f}'_{gl}}$, represents the rate of work done by the fluctuating drag forces, effectively transferring energy between the turbulent eddies and the [dispersed phase](@entry_id:748551). Similar terms appear in the energy equation, where fluctuating heat transfer can impact temperature variance and, in [variable-density flows](@entry_id:1133710), modulate [turbulence production](@entry_id:189980) through buoyancy . Modeling these correlation terms is a key challenge in developing accurate [closures](@entry_id:747387) for turbulent sprays.

### Advanced Models and Physical Closures

The governing equations contain several terms, such as $\Gamma_k$ and $\mathbf{M}_k$, that are not closed and depend on the microscale physics of the spray. The development of accurate **closure relations** for these terms is the essence of physical modeling within the Eulerian-Eulerian framework.

#### Polydisperse Sprays: The Multi-Fluid Sectional Method

Real sprays are **polydisperse**, containing a wide range of droplet sizes. A simple two-fluid model using a single representative diameter is often inadequate, as droplets of different sizes have vastly different inertial and thermal responses. To address this, the model can be extended to a **multi-fluid sectional approach** .

In this method, the dispersed liquid phase is partitioned into $N$ discrete size classes, or sections. Each section $i$ is treated as a distinct fluid phase, with its own volume fraction $\alpha_{\ell,i}$ and velocity field $\mathbf{u}_{\ell,i}$. This results in a system of $1+2N$ conservation equations (one gas phase, $N$ liquid phases). The volume fraction constraint becomes $\alpha_g + \sum_{i=1}^N \alpha_{\ell,i} = 1$.

The mass and momentum equations for each liquid class $i$ are coupled not only to the gas phase via drag but also to each other via source terms that model droplet breakup and coalescence. For instance, the mass equation for class $i$ includes a source term $S^{\mathrm{br}}_i$ representing the net rate of mass entering the class from the breakup of larger droplets and leaving the class as its own droplets break up into smaller ones. Crucially, these inter-class transfer processes must conserve total liquid mass and momentum, requiring that the source terms sum to zero across all classes:
$$
\sum_{i=1}^N S^{\mathrm{br}}_i = 0 \quad \text{and} \quad \sum_{i=1}^N \mathbf{M}^{\mathrm{br}}_i = \mathbf{0}
$$
where $\mathbf{M}^{\mathrm{br}}_i$ is the momentum source from breakup. A physically consistent model for $\mathbf{M}^{\mathrm{br}}_i$ ensures that momentum from a parent droplet is correctly transferred to its children droplets .

#### Closure for Droplet Evaporation

As a concrete example of a closure model, consider the volumetric [evaporation rate](@entry_id:148562), $\Gamma_\ell$. This term must be derived from the underlying physics of single-droplet evaporation. A widely used model for this is the **$d^2$-law**, which states that the square of a droplet's diameter decreases linearly with time: $\mathrm{d}(d_p^2)/\mathrm{d}t = -K$, where $K$ is the evaporation constant.

To translate this Lagrangian law into an Eulerian source term, we first find the [mass loss](@entry_id:188886) rate of a single droplet, $\mathrm{d}m_p/\mathrm{d}t$. For a spherical droplet of density $\rho_\ell$, this is found to be $\mathrm{d}m_p/\mathrm{d}t = -(\pi \rho_\ell K / 4)d_p$. The volumetric source term $\Gamma_\ell$ is then the single-droplet rate multiplied by the number of droplets per unit volume, $n_\ell$:
$$
\Gamma_\ell = n_\ell \frac{\mathrm{d}m_p}{\mathrm{d}t} = -\frac{\pi \rho_\ell K}{4} n_\ell d_p
$$
This expression still contains the unclosed variable $d_p$. To close it, we use the geometric relationship between the solved fields $\alpha_\ell$ and $n_\ell$ for a monodisperse spray: $\alpha_\ell = n_\ell (\pi d_p^3 / 6)$. Solving for $d_p$ and substituting yields the final, closed expression for the source term :
$$
\Gamma_\ell = - \frac{\pi \rho_\ell K}{4} n_\ell \left(\frac{6 \alpha_\ell}{\pi n_\ell}\right)^{1/3}
$$
This process of upscaling a microscale physical law into a macroscopic [closure relation](@entry_id:747393) in terms of the solved field variables is a general paradigm in Eulerian modeling.

#### Closure for Droplet Breakup

Droplet breakup is driven by the competition between the deforming aerodynamic forces from the gas and the restorative forces of surface tension, modulated by the dissipative effects of liquid viscosity. This physics is captured by two key dimensionless numbers .

The **Weber number**, $We$, is the ratio of the aerodynamic [dynamic pressure](@entry_id:262240) to the surface tension pressure:
$$
We = \frac{\rho_g |\mathbf{u}_g - \mathbf{u}_\ell|^2 d_p}{\sigma}
$$
Breakup is initiated when $We$ exceeds a critical value, $We_c$, signifying that aerodynamic forces are strong enough to overcome surface tension. For low-viscosity liquids, the onset of "bag-type" breakup occurs around $We_c \approx 12$.

The **Ohnesorge number**, $Oh$, quantifies the importance of liquid viscosity in resisting deformation. It is defined as the ratio of viscous forces to the [geometric mean](@entry_id:275527) of inertial and surface tension forces:
$$
Oh = \frac{\mu_\ell}{\sqrt{\rho_\ell \sigma d_p}}
$$
A large $Oh$ indicates that [viscous forces](@entry_id:263294) are dominant and will damp out shape oscillations, making the droplet more resistant to breakup. Consequently, the critical Weber number for breakup, $We_c$, is not a constant but increases with the Ohnesorge number. Breakup regime maps, plotted in the $We-Oh$ plane, are used as closure models to predict whether and how droplets will break up based on the local values of the solved fields.