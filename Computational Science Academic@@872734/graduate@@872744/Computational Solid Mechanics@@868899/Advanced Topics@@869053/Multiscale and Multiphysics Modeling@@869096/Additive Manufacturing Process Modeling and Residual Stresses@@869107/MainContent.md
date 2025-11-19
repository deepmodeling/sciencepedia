## Introduction
Additive manufacturing (AM) has revolutionized component design and production, yet its widespread industrial adoption is often hindered by the formation of detrimental residual stresses. These internal stresses, generated during the layer-by-layer fabrication process, can lead to part distortion, cracking, and premature failure, compromising performance and reliability. Controlling these effects requires a deep, predictive understanding of the complex, coupled physical phenomena at play—a knowledge gap that computational modeling is uniquely positioned to fill.

This article provides a graduate-level overview of the principles, applications, and practices for modeling residual stresses in AM. Across the following chapters, we will delve into the foundational physics, explore practical applications, and engage with hands-on problems. The "Principles and Mechanisms" chapter will establish the core theoretical framework, from the governing thermo-mechanical equations to the constitutive laws that capture complex material behavior. The "Applications and Interdisciplinary Connections" chapter will then bridge theory with practice, demonstrating how these models are used for predictive simulation, mitigation strategy development, and experimental validation. Finally, the "Hands-On Practices" section offers targeted exercises to solidify these concepts, empowering readers to apply this knowledge to solve real-world engineering challenges.

## Principles and Mechanisms

The prediction of residual stresses in additively manufactured components is a quintessential [multiphysics](@entry_id:164478) problem, residing at the intersection of heat transfer, solid mechanics, and materials science. To construct robust computational models, one must first grasp the fundamental principles governing the coupled thermo-mechanical phenomena and the mechanisms by which stresses are generated and evolve. This chapter elucidates these core principles, moving from the governing continuum equations to the specific constitutive behaviors and numerical strategies that define modern process simulations.

### The Governing Field Equations: A Coupled Thermo-Mechanical System

At its heart, the simulation of [additive manufacturing](@entry_id:160323) (AM) processes involves solving a coupled initial-boundary value problem. The [primary fields](@entry_id:153633) of interest are the temperature field $T(\boldsymbol{x}, t)$, which dictates the [thermal history](@entry_id:161499), and the displacement field $\boldsymbol{u}(\boldsymbol{x}, t)$, which describes the mechanical deformation. These fields are governed by the fundamental laws of conservation of mass, momentum, and energy. For a material subdomain where consolidation has already occurred, these laws can be stated in their local (differential) form [@problem_id:3542584].

The **balance of mass**, or the [continuity equation](@entry_id:145242), in the spatial (Eulerian) description is given by:
$$
\dot{\rho} + \rho (\nabla \cdot \boldsymbol{v}) = 0
$$
where $\rho$ is the material density, $\boldsymbol{v}$ is the velocity, and $\dot{(\cdot)}$ denotes the [material time derivative](@entry_id:190892). In the context of small-strain solid mechanics, the velocity of a material point is the time derivative of its displacement, $\boldsymbol{v} = \dot{\boldsymbol{u}}$.

The **[balance of linear momentum](@entry_id:193575)** is given by Cauchy's first law of motion. For the vast majority of AM processes, the rates of change are such that [inertial forces](@entry_id:169104) are negligible compared to [internal and external forces](@entry_id:170589). This justifies the **[quasi-static approximation](@entry_id:167818)**, where the acceleration term is neglected. The momentum balance thus reduces to a statement of [mechanical equilibrium](@entry_id:148830):
$$
\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \boldsymbol{0}
$$
Here, $\boldsymbol{\sigma}$ is the symmetric Cauchy stress tensor, representing the [internal forces](@entry_id:167605) per unit area, and $\boldsymbol{b}$ is the body force per unit current volume (e.g., gravity), which is often negligible in AM simulations. This equation mandates that the stress field must be self-equilibrated at all times.

The **balance of energy**, expressed as an equation for heat conduction, is derived from the [first law of thermodynamics](@entry_id:146485). It relates the rate of temperature change to heat diffusion and any heat sources or sinks:
$$
\rho c \dot{T} - \nabla \cdot (k \nabla T) = Q
$$
In this equation, $c$ is the specific heat capacity, $k$ is the thermal conductivity, and $Q$ is the net volumetric heat source rate. $Q$ typically represents the energy deposited by the laser or electron beam, but it can also include contributions from [latent heat](@entry_id:146032) of [phase transformations](@entry_id:200819). Note that the material properties $\rho$, $c$, and $k$ are generally strong functions of temperature.

The crucial link between the mechanical and thermal problems—the **[thermo-mechanical coupling](@entry_id:176786)**—is established primarily through the constitutive law. As will be detailed, temperature changes induce thermal strains that drive mechanical deformation and stress. Conversely, mechanical work can generate heat (e.g., [plastic dissipation](@entry_id:201273)), though this mechanical-to-thermal feedback is often considered a secondary effect in metallic AM compared to the immense energy input from the heat source [@problem_id:3542584].

### The Genesis of Residual Stress: Eigenstrain and Incompatibility

While the governing equations set the stage, they do not, by themselves, explain why stresses remain in a component after it has been manufactured and cooled to a uniform temperature, free of all external loads. The origin of this phenomenon lies in the concept of **[eigenstrain](@entry_id:198120)**, also known as inelastic or stress-free strain [@problem_id:3542597].

An **eigenstrain**, denoted $\boldsymbol{\varepsilon}^{\ast}$, is any strain that is not induced by mechanical stress. It is the strain a small, unconstrained element of material would exhibit due to a change in its internal state. The primary sources of [eigenstrain](@entry_id:198120) in AM are:
*   **Thermal Strain ($\boldsymbol{\varepsilon}^{\text{th}}$)**: Expansion and contraction due to temperature changes.
*   **Plastic Strain ($\boldsymbol{\varepsilon}^{\text{p}}$)**: Irreversible deformation that occurs when stresses exceed the material's temperature-dependent yield strength.
*   **Transformation Strain ($\boldsymbol{\varepsilon}^{\text{tr}}$)**: Volumetric and shear strains associated with solid-state [phase transformations](@entry_id:200819).

The total strain $\boldsymbol{\varepsilon}$ can be additively decomposed into a reversible elastic part $\boldsymbol{\varepsilon}^{e}$ and the [eigenstrain](@entry_id:198120) $\boldsymbol{\varepsilon}^{\ast}$:
$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^{e} + \boldsymbol{\varepsilon}^{\ast}
$$
Stress is generated only by the elastic part of the strain, according to the material's elastic [constitutive law](@entry_id:167255) (e.g., Hooke's Law for a linear elastic material, $\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}^{e}$). This gives the fundamental relation:
$$
\boldsymbol{\sigma} = \mathbb{C} : (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{\ast})
$$

The key to [residual stress](@entry_id:138788) generation lies in the geometric concept of **compatibility**. For a strain field to be derivable from a continuous, single-valued displacement field ($\boldsymbol{\varepsilon} = \operatorname{sym}(\nabla\boldsymbol{u})$), it must be **compatible**. This condition can be expressed mathematically using the Saint-Venant incompatibility operator, $\operatorname{inc}(\boldsymbol{\varepsilon}) = \boldsymbol{0}$.

A self-equilibrated [residual stress](@entry_id:138788) field arises in a body free of external loads precisely when the [eigenstrain](@entry_id:198120) field $\boldsymbol{\varepsilon}^{\ast}$ is **incompatible**, i.e., $\operatorname{inc}(\boldsymbol{\varepsilon}^{\ast}) \neq \boldsymbol{0}$. An incompatible eigenstrain field cannot be accommodated by a simple stress-free deformation. Because the *total* strain $\boldsymbol{\varepsilon}$ must remain compatible, the material is forced to develop an [elastic strain](@entry_id:189634) field $\boldsymbol{\varepsilon}^{e}$ whose own incompatibility exactly cancels that of the eigenstrain:
$$
\operatorname{inc}(\boldsymbol{\varepsilon}) = \operatorname{inc}(\boldsymbol{\varepsilon}^{e} + \boldsymbol{\varepsilon}^{\ast}) = \boldsymbol{0} \implies \operatorname{inc}(\boldsymbol{\varepsilon}^{e}) = - \operatorname{inc}(\boldsymbol{\varepsilon}^{\ast})
$$
Since $\operatorname{inc}(\boldsymbol{\varepsilon}^{\ast})$ is non-zero, $\operatorname{inc}(\boldsymbol{\varepsilon}^{e})$ must also be non-zero. This necessitates a non-zero elastic strain field, which in turn generates a non-zero, self-equilibrated [residual stress](@entry_id:138788) field $\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}^{e}$ [@problem_id:3542597]. In AM, the rapid, localized heating and cooling cycles create highly non-uniform plastic and [thermal strain](@entry_id:187744) fields, which are the primary source of this incompatibility.

### Constitutive Modeling: Capturing Material Behavior

To accurately predict the evolution of the eigenstrain field, we must employ [constitutive models](@entry_id:174726) that capture the material's complex behavior under the extreme thermal cycles of AM.

#### Thermo-Elasto-Plasticity

The dominant mechanism for generating incompatible eigenstrains in metals is thermo-[elasto-plasticity](@entry_id:748865). Within the small-strain framework, the total strain is decomposed as:
$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^{e} + \boldsymbol{\varepsilon}^{p} + \boldsymbol{\varepsilon}^{th}
$$
The [thermal strain](@entry_id:187744) $\boldsymbol{\varepsilon}^{\text{th}}$ is reversible and depends on the temperature history. For an [isotropic material](@entry_id:204616) with a temperature-dependent [coefficient of thermal expansion](@entry_id:143640) (CTE), $\alpha(T)$, the [thermal strain](@entry_id:187744) relative to a stress-free reference temperature $T_0$ is given by:
$$
\boldsymbol{\varepsilon}^{\text{th}} = \left( \int_{T_0}^{T} \alpha(T') \, \mathrm{d}T' \right) \mathbf{I}
$$
where $\mathbf{I}$ is the identity tensor [@problem_id:3542625].

The plastic strain $\boldsymbol{\varepsilon}^{p}$ is irreversible and path-dependent. Plastic flow is initiated when a scalar measure of stress, the [equivalent stress](@entry_id:749064) $\sigma_{\text{eq}}$, reaches the material's yield strength, $\sigma_y$. A critical feature in AM modeling is **[thermal softening](@entry_id:187731)**: the yield strength of metals decreases significantly at elevated temperatures. This is captured by a temperature-dependent [yield function](@entry_id:167970), $f(\boldsymbol{\sigma}, T) = \sigma_{\text{eq}} - \sigma_y(T) \le 0$. During local heating, thermal expansion is constrained by the surrounding cooler material, inducing compressive stresses. Due to the low [yield strength](@entry_id:162154) at high temperature, these stresses easily cause localized compressive plastic yielding. Upon cooling, the region contracts, but this contraction is now superimposed on the permanent compressive plastic strain, leading to the development of high tensile stresses. It is this accumulated, incompatible field of plastic strain, $\boldsymbol{\varepsilon}^{p}$, that remains after the part has cooled to room temperature and is the principal source of [residual stress](@entry_id:138788) [@problem_id:3542625].

#### High-Temperature Creep and Stress Relaxation

At temperatures approaching the solidus, time-dependent inelastic deformation, or **creep**, can become significant. Creep provides a mechanism for [stress relaxation](@entry_id:159905). A common model for this behavior is the Norton [power-law creep](@entry_id:198473) model, where the [creep strain rate](@entry_id:187109) $\dot{\boldsymbol{\varepsilon}}^{cr}$ is a function of stress and temperature:
$$
\dot{\varepsilon}^{\text{cr}} = A(T) \sigma^{m}
$$
where $\sigma$ is the [equivalent stress](@entry_id:749064), $m$ is the creep [stress exponent](@entry_id:183429) (typically > 1), and $A(T)$ is a material parameter that increases strongly with temperature. During periods of the thermal cycle where the material is held at a high temperature (a dwell), such as the time between subsequent laser passes, accumulated stresses can relax. Under a total strain constraint ($\dot{\varepsilon} = 0$), the accumulation of creep strain must be balanced by a decrease in elastic strain, leading to a reduction in stress. The governing equation for [stress relaxation](@entry_id:159905) in a simple one-dimensional case is $\dot{\sigma} = -E \dot{\varepsilon}^{cr} = -E A(T_d) \sigma^m$, where $T_d$ is the dwell temperature. This relaxation can significantly reduce the magnitude of stresses carried over to the cooling phase, thereby mitigating the final [residual stress](@entry_id:138788) state [@problem_id:3542647].

#### Process-Induced Anisotropy

The directional [solidification](@entry_id:156052) inherent in many AM processes, particularly with linear scan strategies, often results in the growth of columnar grains. This creates a strong [crystallographic texture](@entry_id:186522), causing the macroscopic mechanical and thermal properties of the deposited material to become **anisotropic**. A common and effective representation is an **[orthotropic material](@entry_id:191640) model**, where properties differ along three mutually orthogonal [principal directions](@entry_id:276187), often aligned with the build, scan, and transverse directions [@problem_id:3542665].

In an orthotropic model, the elastic response is described by directional Young's moduli (e.g., $E_x, E_y$) and Poisson's ratios (e.g., $\nu_{xy}, \nu_{yx}$), which are related by the reciprocity condition $\nu_{xy}/E_x = \nu_{yx}/E_y$. Thermal expansion may also be anisotropic, with different CTEs ($\alpha_x, \alpha_y$). This directionality has a direct impact on the resulting stress field. For instance, in a biaxially constrained layer undergoing uniform cooling, a higher stiffness in the scan direction ($E_x$) will naturally lead to a higher residual stress component in that direction ($\sigma_{xx}$), as more stress is required to resist the same amount of thermal contraction. Accounting for this process-induced anisotropy is a key step toward more predictive simulations.

### Modeling the Additive Process: Thermal and Numerical Aspects

The accuracy of any [residual stress](@entry_id:138788) prediction is contingent on the accuracy of the underlying thermal simulation, which itself depends on how the physics of the process are translated into a mathematical model.

#### Heat Source and Boundary Conditions

The energy input from the laser or electron beam is the primary driver of the entire process. Two common approaches to modeling this are the **surface flux model** and the **volumetric source model** [@problem_id:3542579].
*   A **surface flux model** treats the energy deposition as a Neumann boundary condition on the top surface. A common representation is a moving 2D Gaussian distribution, whose integral over the surface equals the total [absorbed power](@entry_id:265908), $\eta P$, where $P$ is the incident laser power and $\eta$ is the material's [absorptivity](@entry_id:144520).
*   A **volumetric source model** distributes the energy into the material's volume. A physically-motivated choice is to combine the surface Gaussian distribution with a Beer-Lambert [exponential decay](@entry_id:136762) in the depth direction, governed by a characteristic penetration depth, $d$. This distributes the same total power $\eta P$ over a volume, leading to lower peak temperatures and gentler near-surface thermal gradients compared to a surface flux model.

A classic, albeit highly idealized, model is the **Rosenthal solution**, which provides an analytical expression for the quasi-steady temperature field around a moving point heat source in a semi-infinite medium [@problem_id:3542621]. While its assumptions—a point source, constant material properties, and no [phase change](@entry_id:147324)—are gross simplifications of a real AM process, it provides invaluable physical insight into the teardrop shape of the thermal field, showing a compressed gradient ahead of the source and a long, trailing wake behind it. Its limitations underscore the need for more sophisticated numerical models.

These numerical models must also incorporate realistic boundary conditions. Heat is lost from the free surfaces of the part to the surrounding environment (e.g., inert gas) and the chamber walls. This is modeled by a combined Robin boundary condition that accounts for both **convection** and **radiation** [@problem_id:3542591]:
$$
-k \nabla T \cdot \boldsymbol{n} = h(T - T_{\infty}) + \epsilon \sigma_B (T^4 - T_{\text{amb}}^4)
$$
where $\boldsymbol{n}$ is the outward normal, $h$ is the [convective heat transfer coefficient](@entry_id:151029), $T_{\infty}$ is the ambient gas temperature, $\epsilon$ is the surface emissivity, $\sigma_B$ is the Stefan-Boltzmann constant, and $T_{\text{amb}}$ is the temperature of the surrounding chamber. Mechanically, the model must reflect the physical constraints, such as a **clamped** base ($\boldsymbol{u} = \boldsymbol{0}$) where the part is attached to the rigid build plate, and **symmetry** planes ($u_n = 0$, zero tangential traction) where applicable.

#### Handling Phase Change and Material Addition

Two critical numerical challenges are modeling the physics of melting/[solidification](@entry_id:156052) and the layer-by-layer addition of material.

Phase change involves the absorption or release of a large amount of energy—the [latent heat of fusion](@entry_id:144988), $L$—over a small temperature range. Explicitly tracking the moving [solid-liquid interface](@entry_id:201674) is complex. A more robust and common approach is the **enthalpy method**, where the [latent heat](@entry_id:146032) is embedded into an **effective [specific heat](@entry_id:136923)**, $c^{\text{eff}}(T)$ [@problem_id:3542596]. In the [mushy zone](@entry_id:147943) between the solidus ($T_s$) and liquidus ($T_l$) temperatures, $c^{\text{eff}}$ is augmented to account for the energy of transformation:
$$
c^{\text{eff}}(T) = (1-f_l)c_s + f_l c_l + L \frac{df_l}{dT}
$$
where $f_l(T)$ is the liquid fraction, and $c_s$ and $c_l$ are the specific heats of the solid and liquid phases. This allows the standard heat equation to be solved without explicit [interface tracking](@entry_id:750734).

To simulate the "additive" nature of the process, the **birth-death element method** is widely employed [@problem_id:3542669]. In this approach, a [finite element mesh](@entry_id:174862) of the final part geometry is created at the outset. Elements corresponding to material not yet deposited are "killed" by assigning them near-zero stiffness, mass, and thermal properties. As the simulated heat source moves and deposits new layers, the corresponding elements are "born" by reactivating their true material properties. This results in a monotonic increase of the global [mass and stiffness matrices](@entry_id:751703) over the course of the simulation. Each new element is born in a stress-free state, and its stress history begins at its moment of activation.

### Linking Process to Performance: The Role of Key Parameters

Computational models provide a powerful tool to understand how controllable process parameters influence the [thermal history](@entry_id:161499) and, ultimately, the final residual stress state. A first-order analysis reveals several key relationships [@problem_id:3542595].

*   **Hatch Spacing ($h$)**: This is the distance between adjacent scan lines in a layer. Decreasing $h$ reduces the time between scanning adjacent tracks. If this time is short compared to the [thermal diffusion](@entry_id:146479) time, the new track is laid on pre-heated ground. This reduces the local thermal gradients between tracks, leading to a more uniform temperature field within the layer and tending to reduce in-plane residual stresses.

*   **Scan Strategy (Rotation $\phi$)**: The orientation of the scan vectors can be rotated between successive layers. A non-zero **scan rotation** (e.g., $67^\circ$ or $90^\circ$) prevents the monotonic build-up of [anisotropic stress](@entry_id:161403). By varying the direction of the principal thermal gradients from layer to layer, stress is more evenly distributed, and its peak magnitude is typically mitigated.

*   **Interlayer Time ($\Delta t$)**: This is the dwell time between the completion of one layer and the start of the next. A long interlayer time allows the part to cool substantially. When the next layer is deposited, the temperature difference between the new melt and the cold substrate is very large, leading to steep vertical thermal gradients and, consequently, higher residual stresses. Conversely, a short interlayer time (as in a continuous build) minimizes these vertical gradients and tends to reduce [residual stress](@entry_id:138788), at the cost of greater overall heat accumulation in the part.

Understanding these principles and mechanisms is the foundation upon which predictive, physically-based modeling of additive manufacturing is built. They empower the engineer not only to forecast the formation of residual stresses but also to devise strategies for their mitigation.