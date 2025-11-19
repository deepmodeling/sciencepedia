## Introduction
While shear viscosity is a cornerstone of fluid dynamics, describing a fluid's resistance to changes in shape, a second, equally fundamental property often remains in the background: the second coefficient of viscosity, or bulk viscosity. This coefficient governs a fluid's resistance to changes in volume and is essential for accurately modeling [compressible flows](@entry_id:747589), acoustic phenomena, and shock waves. Its physical origins, however, are less direct than those of [shear viscosity](@entry_id:141046), stemming from complex microscopic relaxation processes that create a lag between pressure and density. This article demystifies the concept of [second viscosity](@entry_id:189253) by providing a comprehensive exploration of its theoretical foundations and practical implications.

The journey begins in the "Principles and Mechanisms" chapter, where we will derive the macroscopic formulation from continuum mechanics and delve into the microscopic origins, from internal [energy relaxation](@entry_id:136820) in polyatomic gases to the [fluctuation-dissipation theorem](@entry_id:137014). Following this, the "Applications and Interdisciplinary Connections" chapter will showcase the critical role of bulk viscosity across diverse fields, including [acoustics](@entry_id:265335), [chemical physics](@entry_id:199585), and cosmology. Finally, the "Hands-On Practices" section will offer a series of targeted problems to reinforce these concepts and bridge the gap between theory and application.

## Principles and Mechanisms

### Macroscopic Formulation: Stress, Strain, and Volumetric Viscosity

In the study of fluid dynamics, the relationship between stress and the [rate of strain](@entry_id:267998) is fundamental. For an incompressible Newtonian fluid, this relationship is elegantly simple: the [viscous stress](@entry_id:261328) is linearly proportional to the [rate-of-strain tensor](@entry_id:260652). However, when a fluid's density is permitted to change, the physics becomes richer, necessitating the introduction of a second, independent viscosity coefficient that governs the fluid's response to volumetric deformation.

#### The Constitutive Relation for a Compressible Fluid

Let us begin with the general description of a compressible, isotropic Newtonian fluid. The total stress within the fluid is described by the Cauchy stress tensor, $\boldsymbol{\sigma}$, which can be decomposed into an [isotropic pressure](@entry_id:269937) component and a [viscous stress](@entry_id:261328) component, $\boldsymbol{\tau}$:
$$
\boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\tau}
$$
Here, $p$ is the thermodynamic pressure that would exist in the fluid at [local equilibrium](@entry_id:156295), and $\mathbf{I}$ is the identity tensor. The [viscous stress](@entry_id:261328) tensor, $\boldsymbol{\tau}$, represents the stresses that arise from [fluid motion](@entry_id:182721), specifically from spatial gradients in the velocity field $\mathbf{v}$.

For a Newtonian fluid, the relationship between $\boldsymbol{\tau}$ and the velocity gradients is linear. The relevant measure of deformation rate is the symmetric [rate-of-strain tensor](@entry_id:260652), $\mathbf{D}$:
$$
\mathbf{D} = \frac{1}{2}\left(\nabla\mathbf{v} + (\nabla\mathbf{v})^T\right)
$$
The most general linear and isotropic relationship between the two second-rank tensors $\boldsymbol{\tau}$ and $\mathbf{D}$ involves two scalar material constants. This relationship is expressed as:
$$
\boldsymbol{\tau} = \lambda (\text{tr}(\mathbf{D})) \mathbf{I} + 2\mu \mathbf{D}
$$
where $\mu$ is the familiar **dynamic viscosity** (or [shear viscosity](@entry_id:141046)), and $\lambda$ is the **second coefficient of viscosity**. The trace of the [rate-of-strain tensor](@entry_id:260652), $\text{tr}(\mathbf{D})$, is equivalent to the divergence of the [velocity field](@entry_id:271461), $\nabla \cdot \mathbf{v}$, which represents the rate of [volumetric strain](@entry_id:267252) per unit volume.

#### The Second Coefficient ($\lambda$) and Bulk Viscosity ($\kappa$)

The term proportional to $\mu$ describes the resistance to shearing motions (changes in shape), while the term proportional to $\lambda$ describes an additional isotropic stress that arises during [volumetric expansion](@entry_id:144241) or compression. To better understand the physical roles of these coefficients, it is instructive to decompose the [viscous stress](@entry_id:261328) tensor into its isotropic and deviatoric (traceless) parts. This leads to an alternative, and often more physically transparent, formulation.

Let us define the **[bulk viscosity](@entry_id:187773)**, often denoted by $\kappa$ or $\zeta$, through the relationship between the mean [normal stress](@entry_id:184326) and the thermodynamic pressure. The mean normal stress, $\bar{\sigma}$, is one-third of the trace of the total stress tensor:
$$
\bar{\sigma} = \frac{1}{3}\text{tr}(\boldsymbol{\sigma}) = \frac{1}{3}\text{tr}(-p\mathbf{I} + \boldsymbol{\tau}) = -p + \frac{1}{3}\text{tr}(\boldsymbol{\tau})
$$
The **mechanical pressure**, $p_m$, is defined as the negative of the mean [normal stress](@entry_id:184326), $p_m = -\bar{\sigma}$. The difference between the mechanical and thermodynamic pressures is attributed to viscous effects during volume change and is phenomenologically defined by the [bulk viscosity](@entry_id:187773), $\kappa$:
$$
p_m - p = -\kappa(\nabla \cdot \mathbf{v})
$$
From the expression for $p_m$, we have $p_m - p = -\frac{1}{3}\text{tr}(\boldsymbol{\tau})$. Equating these two relations gives $\kappa(\nabla \cdot \mathbf{v}) = \frac{1}{3}\text{tr}(\boldsymbol{\tau})$. We can find the trace of $\boldsymbol{\tau}$ from its [constitutive relation](@entry_id:268485):
$$
\text{tr}(\boldsymbol{\tau}) = \text{tr}(\lambda (\nabla \cdot \mathbf{v}) \mathbf{I} + 2\mu \mathbf{D}) = \lambda (\nabla \cdot \mathbf{v}) \text{tr}(\mathbf{I}) + 2\mu \text{tr}(\mathbf{D}) = 3\lambda(\nabla \cdot \mathbf{v}) + 2\mu(\nabla \cdot \mathbf{v}) = (3\lambda + 2\mu)(\nabla \cdot \mathbf{v})
$$
Substituting this into our equation for $\kappa$ yields:
$$
\kappa(\nabla \cdot \mathbf{v}) = \frac{1}{3}(3\lambda + 2\mu)(\nabla \cdot \mathbf{v})
$$
This must hold for any arbitrary compression or expansion, so we arrive at the fundamental relationship between the three viscosity coefficients [@problem_id:656236]:
$$
\kappa = \lambda + \frac{2}{3}\mu
$$
Using this relation, we can rewrite the viscous stress tensor in a form that explicitly separates the contributions from volume change (dilation) and shape change (shear):
$$
\boldsymbol{\tau} = 2\mu \left(\mathbf{D} - \frac{1}{3}(\nabla \cdot \mathbf{v})\mathbf{I}\right) + \kappa (\nabla \cdot \mathbf{v})\mathbf{I}
$$
The first term involves the traceless part of the [rate-of-strain tensor](@entry_id:260652) and is purely a shear stress, scaled by the shear viscosity $\mu$. The second term is an isotropic stress, proportional to the rate of volume change and scaled by the [bulk viscosity](@entry_id:187773) $\kappa$. This form makes the physical meaning of $\kappa$ clear: it is the coefficient of proportionality between the isotropic part of the viscous stress and the rate of dilation.

As a concrete example, consider a one-dimensional, steady, compressible flow where the velocity is only in the $x$-direction, $\mathbf{v} = u(x)\hat{\mathbf{i}}$ [@problem_id:1795098]. In this case, the only non-zero component of the [rate-of-strain tensor](@entry_id:260652) is $D_{xx} = du/dx$, and the divergence is $\nabla \cdot \mathbf{v} = du/dx$. The viscous [normal stress](@entry_id:184326) in the flow direction, $\tau_{xx}$, is then:
$$
\tau_{xx} = \lambda (\nabla \cdot \mathbf{v}) + 2\mu D_{xx} = \lambda \frac{du}{dx} + 2\mu \frac{du}{dx} = (2\mu + \lambda)\frac{du}{dx}
$$
Expressed in terms of the bulk viscosity $\kappa$, this becomes $\tau_{xx} = (2\mu + \kappa - \frac{2}{3}\mu)\frac{du}{dx} = (\frac{4}{3}\mu + \kappa)\frac{du}{dx}$. The coefficient $(\frac{4}{3}\mu + \kappa)$ is often called the **longitudinal viscosity** and is relevant for the damping of [longitudinal waves](@entry_id:172335) (sound).

### Energetic Consequences and Physical Manifestation

The presence of viscosity implies that mechanical energy is irreversibly converted into internal energy (heat) as the fluid deforms. This process is known as **[viscous dissipation](@entry_id:143708)**. The bulk viscosity contributes a unique term to this [energy dissipation](@entry_id:147406), a term that is active only during volumetric changes.

#### The Viscous Dissipation Function

The rate at which [mechanical energy](@entry_id:162989) is converted into internal energy per unit volume is given by the [viscous dissipation](@entry_id:143708) function, $\Phi$. It can be derived from the [transport equation](@entry_id:174281) for internal energy, $e$, which is obtained by subtracting the kinetic energy equation from the total [energy equation](@entry_id:156281). The resulting equation for internal energy is:
$$
\rho \frac{De}{Dt} = -p(\nabla \cdot \mathbf{v}) - \nabla \cdot \mathbf{q} + \Phi
$$
where the dissipation function $\Phi$ is the work done by the viscous stresses per unit volume, given by the full contraction of the [viscous stress](@entry_id:261328) tensor with the [velocity gradient tensor](@entry_id:270928), $\Phi = \boldsymbol{\tau} : \nabla\mathbf{v}$. Since $\boldsymbol{\tau}$ is symmetric, this is equivalent to $\Phi = \boldsymbol{\tau} : \mathbf{D}$.

Substituting the [constitutive relation](@entry_id:268485) for $\boldsymbol{\tau}$ in terms of $\kappa$ and $\mu$:
$$
\Phi = \left[ 2\mu \left(\mathbf{D} - \frac{1}{3}(\nabla \cdot \mathbf{v})\mathbf{I}\right) + \kappa (\nabla \cdot \mathbf{v})\mathbf{I} \right] : \mathbf{D}
$$
Expanding this expression and using the properties of the trace operation, we find that the dissipation function separates into two distinct, non-negative terms [@problem_id:620847]:
$$
\Phi = 2\mu \left( \mathbf{D} - \frac{1}{3}(\nabla \cdot \mathbf{v})\mathbf{I} \right) : \left( \mathbf{D} - \frac{1}{3}(\nabla \cdot \mathbf{v})\mathbf{I} \right) + \kappa (\nabla \cdot \mathbf{v})^2
$$
In [index notation](@entry_id:191923), this is $\Phi = 2\mu D'_{ij} D'_{ij} + \kappa (\nabla \cdot \mathbf{v})^2$, where $D'_{ij}$ is the deviatoric part of the [rate-of-strain tensor](@entry_id:260652).

The first term represents dissipation due to shearing motions, while the second term, $\kappa (\nabla \cdot \mathbf{v})^2$, represents dissipation due to volumetric changes. This form shows unequivocally that both shear and bulk viscosity lead to an increase in internal energy (and thus entropy), as $\Phi$ must be non-negative for any possible fluid motion, which in turn requires $\mu \ge 0$ and $\kappa \ge 0$.

#### Illustrative Example: Pure Volumetric Expansion

The unique role of bulk viscosity is most clearly demonstrated in a flow with zero shear. Consider a uniform, purely radial expansion of a fluid sphere, where the [velocity field](@entry_id:271461) is given by $\mathbf{v} = \beta \mathbf{r}$ for some constant expansion rate $\beta > 0$ [@problem_id:623159]. For this flow, the [velocity gradient tensor](@entry_id:270928) is $\nabla\mathbf{v} = \beta\mathbf{I}$, which is already symmetric, so $\mathbf{D} = \beta\mathbf{I}$. The rate of [volumetric expansion](@entry_id:144241) is $\nabla \cdot \mathbf{v} = \text{tr}(\beta\mathbf{I}) = 3\beta$.

The deviatoric part of the [rate-of-strain tensor](@entry_id:260652) is:
$$
\mathbf{D}' = \mathbf{D} - \frac{1}{3}(\nabla \cdot \mathbf{v})\mathbf{I} = \beta\mathbf{I} - \frac{1}{3}(3\beta)\mathbf{I} = \mathbf{0}
$$
Since there is no rate of shear, the shear viscosity $\mu$ contributes nothing to the [viscous stress](@entry_id:261328). The entire [viscous stress](@entry_id:261328) tensor is purely isotropic and determined by the bulk viscosity:
$$
\boldsymbol{\tau} = \kappa (\nabla \cdot \mathbf{v})\mathbf{I} = 3\beta\kappa\mathbf{I}
$$
The viscous dissipation is then:
$$
\Phi = \kappa(\nabla \cdot \mathbf{v})^2 = \kappa(3\beta)^2 = 9\beta^2\kappa
$$
This shows that even in the complete absence of shear, a fluid with non-zero bulk viscosity will dissipate energy if its volume is changing. The rate of irreversible entropy production per unit volume is $\dot{s}_{gen} = \Phi/T$, where $T$ is the local temperature. This dissipation manifests as a resistance to compression or expansion, contributing significantly to phenomena like the attenuation of sound waves in polyatomic gases.

### Microscopic Origins of Bulk Viscosity

The macroscopic framework introduces $\kappa$ as a phenomenological coefficient. To truly understand its significance, we must investigate its microscopic origins. This inquiry reveals that the value of $\kappa$ is intimately tied to the internal structure of the fluid's constituent particles and the nature of their interactions.

#### The Case of Dilute Monatomic Gases: Stokes' Hypothesis

A crucial starting point is the [ideal monatomic gas](@entry_id:138760). From a physical perspective, the particles of such a gas are simple point masses with only [translational kinetic energy](@entry_id:174977). When the gas is compressed, energy is added to these translational modes. Since there are no internal degrees of freedom (like rotation or vibration) to which this energy must be redistributed, the system can adjust to volume changes almost instantaneously. There is no internal relaxation process that could cause a lag and thus dissipation. This leads to the conjecture that for a dilute [monatomic gas](@entry_id:140562), the bulk viscosity should be zero.

This conjecture is known as **Stokes' hypothesis**. In terms of the viscosity coefficients, it states that $\kappa = 0$, which implies $\lambda = -2/3 \mu$. Under this hypothesis, the mechanical pressure $p_m$ is always equal to the thermodynamic pressure $p$.

This physical intuition is rigorously confirmed by the [kinetic theory of gases](@entry_id:140543). The Chapman-Enskog method, which solves the Boltzmann equation to derive transport coefficients, shows that for a dilute [monatomic gas](@entry_id:140562), the [viscous stress](@entry_id:261328) tensor $\tau_{ij}$ arises from the [first-order correction](@entry_id:155896) to the Maxwell-Boltzmann distribution function, $f^{(1)}$. A key result of this analysis is that the part of $f^{(1)}$ dependent on velocity gradients is proportional to a [traceless tensor](@entry_id:274053) combination of peculiar velocities, $(c_i c_j - \frac{1}{3}c^2 \delta_{ij})$ [@problem_id:623233]. When calculating the trace of the viscous stress tensor, $\tau_{kk}$, one integrates $c^2 f^{(1)}$ over all [velocity space](@entry_id:181216). Due to the traceless nature of the underlying velocity term, this integral vanishes identically.
$$
\tau_{kk} = m \int c^2 f^{(1)} d^3\mathbf{c} = 0
$$
From the macroscopic definition, we know that $\tau_{kk} = (3\lambda + 2\mu) \nabla \cdot \mathbf{v}$. However, we also have $\tau_{kk} = 3 \kappa (\nabla \cdot \mathbf{v})$. For this to be zero for any arbitrary flow (i.e., any $\nabla \cdot \mathbf{v}$), the bulk viscosity must be zero:
$$
\kappa = 0
$$
This foundational result confirms that bulk viscosity is intrinsically linked to more complex molecular processes not present in an ideal point-particle gas.

#### Mechanism 1: Internal Energy Relaxation in Polyatomic Gases

The situation changes dramatically for polyatomic gases. Molecules in these gases possess internal degrees of freedom—[rotational and vibrational energy](@entry_id:143118) states—in addition to [translational kinetic energy](@entry_id:174977). When such a gas is rapidly compressed, the work done primarily increases the [translational kinetic energy](@entry_id:174977) of the molecules, raising the "translational temperature," $T_{tr}$. The internal energy modes, however, do not adjust instantaneously. Energy is transferred from the translational modes to the internal modes through collisions, a process that occurs over a finite **[relaxation time](@entry_id:142983)**, $\tau$.

During this relaxation process, the system is not in full [thermodynamic equilibrium](@entry_id:141660). The pressure, which is mainly determined by $T_{tr}$, is temporarily higher than the equilibrium pressure that would correspond to the same total energy. This pressure difference, a direct consequence of the relaxation lag, acts as a dissipative force.

This mechanism can be modeled quantitatively to derive an expression for the bulk viscosity [@problem_id:623180]. The lag of an internal state variable $\xi$ behind its equilibrium value $\xi_{eq}$ leads to an irreversible pressure $p_{irr}$ that is proportional to the rate of volume change. This analysis provides a profound connection between the macroscopic bulk viscosity $\kappa$ and the microscopic relaxation dynamics, known as the **Mandel'shtam-Leontovich formula**:
$$
\kappa = \rho_0 \tau (c_\infty^2 - c_0^2)
$$
Here, $\tau$ is the internal [energy relaxation](@entry_id:136820) time, $\rho_0$ is the equilibrium density, $c_\infty$ is the "frozen" sound speed (at frequencies much higher than $1/\tau$, where internal modes do not have time to react), and $c_0$ is the equilibrium sound speed (at frequencies much lower than $1/\tau$, where the system is always in internal equilibrium). The [bulk viscosity](@entry_id:187773) is directly proportional to the [relaxation time](@entry_id:142983) and the dispersion in the speed of sound, which quantifies the strength of the coupling between volume and the internal energy modes.

A simplified kinetic theory model provides a useful estimate for the magnitude of $\kappa$ relative to $\mu$. The **Eucken relation** [@problem_id:623240] is derived by balancing the rate of mechanical work done during compression against the rate of energy transfer to internal modes. This yields a relation for the ratio $\kappa/\mu$ in terms of thermodynamic properties and collision dynamics:
$$
\frac{\kappa}{\mu} = \frac{(\gamma-1)^2}{C_\mu} \frac{c_{v,int}}{R} Z_{int}
$$
In a slightly different simplified derivation provided in the problem, the Eucken relation can be expressed as $\frac{\kappa}{\mu} = \frac{(\gamma-1)Z_{int}}{C_\mu}$. In both formulations, $\gamma$ is the [specific heat ratio](@entry_id:145177), $Z_{int}$ is the "collision number" (the average number of collisions needed for an internal energy transition), and $C_\mu$ is a constant of order one. Since $Z_{int}$ can be large for some molecules (especially for [vibrational modes](@entry_id:137888)), the [bulk viscosity](@entry_id:187773) can be significantly larger than the shear viscosity, i.e., $\kappa \gg \mu$.

#### Mechanism 2: Collisional Effects in Dense Fluids

Bulk viscosity is not exclusively a feature of polyatomic fluids. Even for monatomic fluids, a non-zero [bulk viscosity](@entry_id:187773) can arise at high densities. The proof that $\kappa=0$ for a [monatomic gas](@entry_id:140562) relies on the "dilute" approximation, where collisions are treated as instantaneous, binary events between point particles.

In a dense gas or liquid, this picture is no longer valid. Particles have finite size, and the duration of a collision is non-negligible. More importantly, there is a mechanism known as **collisional transfer**, where momentum and energy are transferred across a surface not just by particles crossing it (kinetic contribution), but also by the [intermolecular forces](@entry_id:141785) acting between pairs of particles on opposite sides of the surface.

The Enskog kinetic theory for a dense gas of hard spheres provides the simplest model that captures this effect [@problem_id:623168]. It predicts a non-zero [bulk viscosity](@entry_id:187773), $\kappa_E$ (using the problem's notation), that is a direct consequence of accounting for the finite size of particles and the change in [collision frequency](@entry_id:138992) with density. The leading term in the density ($n$) expansion for the Enskog [bulk viscosity](@entry_id:187773) is:
$$
\kappa_E = \frac{4}{9} n^2 d^4 g(d) (\pi m k_B T)^{1/2}
$$
where $d$ is the particle diameter and $g(d)$ is the [pair correlation function](@entry_id:145140) at contact, which is itself a function of density. Unlike the dilute gas case, where viscosity is independent of density, the Enskog bulk viscosity grows approximately as $n^2$ at low to moderate densities. This reveals a second, distinct physical mechanism for [bulk viscosity](@entry_id:187773): it can arise from the finite duration and spatial extent of intermolecular collisions in a dense system, creating a dissipative lag even without internal [molecular structure](@entry_id:140109).

### Advanced Perspective: The Fluctuation-Dissipation Theorem

The most fundamental understanding of [transport coefficients](@entry_id:136790) comes from the field of statistical mechanics, through the **fluctuation-dissipation theorem**. This theorem establishes a profound link: a system's dissipative response to an external perturbation (like deformation) is determined by the statistical properties of its microscopic fluctuations at thermal equilibrium. In essence, the way a system returns to equilibrium after a spontaneous, random fluctuation dictates how it will dissipate energy when forced away from equilibrium.

#### The Green-Kubo Formalism

For transport coefficients like viscosity, this theorem takes the form of the **Green-Kubo relations**. These formulas express the transport coefficient as the time-integral of an equilibrium time-[autocorrelation function](@entry_id:138327). For [bulk viscosity](@entry_id:187773) $\kappa$, the relevant fluctuating quantity is the microscopic pressure. Specifically, the part of the stress tensor that couples to a change in volume.

The Green-Kubo formula for bulk viscosity is [@problem_id:623198]:
$$
\kappa = \frac{V}{k_B T} \int_0^\infty \langle \delta P(t) \delta P(0) \rangle_0 dt
$$
Here, $V$ is the volume, $k_B$ is the Boltzmann constant, $T$ is the temperature, and $\delta P(t)$ is the fluctuation of the isotropic part of the stress tensor around its equilibrium average, $\langle P \rangle_0$. The term $\langle \delta P(t) \delta P(0) \rangle_0$ is the **pressure fluctuation autocorrelation function**, which measures how long a spontaneous fluctuation in pressure "persists" or remains correlated with itself over time.

This formula provides a powerful conceptual and computational tool. It states that [bulk viscosity](@entry_id:187773) is proportional to the total "memory" of pressure fluctuations in the system. A fluid where fluctuations decay very rapidly has a short memory and low [bulk viscosity](@entry_id:187773), while a system with long-lived correlations (e.g., due to slow relaxation processes) will exhibit a large [bulk viscosity](@entry_id:187773).

As a concrete application, if we have a model for the dynamics of the autocorrelation function $C(t) = \langle \delta P(t) \delta P(0) \rangle_0$, we can directly calculate $\kappa$. For instance, if $C(t)$ is assumed to obey the dynamics of a damped harmonic oscillator, its governing equation can be integrated directly to find the value of the integral in the Green-Kubo formula. For a system governed by $\ddot{C} + 2\gamma \dot{C} + \omega_0^2 C = 0$, the [bulk viscosity](@entry_id:187773) is found to be [@problem_id:623198]:
$$
\kappa = \frac{V}{k_B T} \frac{2\gamma C(0)}{\omega_0^2}
$$
where $C(0)$ is the mean-squared pressure fluctuation, $\gamma$ is the damping constant, and $\omega_0$ is the characteristic frequency. This demonstrates how a specific microscopic dynamical model can be translated directly into a value for a macroscopic transport coefficient, providing a complete bridge from the microscopic to the continuum world.