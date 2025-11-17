## Introduction
The behavior of many engineering materials, particularly polymers, elastomers, and biological tissues, cannot be adequately described by purely elastic or viscous models. These materials exhibit [viscoelasticity](@entry_id:148045), a complex time- and history-dependent response that combines features of both elastic solids and viscous fluids. Accurately modeling this behavior is critical for designing and predicting the performance of components in fields ranging from aerospace engineering to [biomechanics](@entry_id:153973). The central challenge lies in developing a constitutive framework that is not only physically accurate and thermodynamically consistent but also computationally tractable for complex engineering simulations, especially when deformations become large.

This article provides a detailed exploration of [viscoelasticity](@entry_id:148045), focusing on the powerful and widely used Prony [series representation](@entry_id:175860). We will bridge the gap between fundamental theory and practical application. In the first chapter, **Principles and Mechanisms**, we establish the mathematical foundations, starting with the [hereditary integrals](@entry_id:186265) of [linear viscoelasticity](@entry_id:181219) and deriving the Prony series from the generalized Maxwell model. We will then extend these concepts to the [finite strain](@entry_id:749398) regime and incorporate the effects of temperature through the principle of [time-temperature superposition](@entry_id:141843). Following this theoretical development, the **Applications and Interdisciplinary Connections** chapter demonstrates how this model is used in the real world—from characterizing materials via experimental data to predicting structural responses like residual stress and its robust implementation in finite element software. Finally, the **Hands-On Practices** section offers a set of targeted problems to solidify your understanding of these core concepts, guiding you through derivations and practical calculations.

## Principles and Mechanisms

This chapter delves into the fundamental principles and theoretical mechanisms that govern the behavior of [viscoelastic materials](@entry_id:194223). We begin by establishing the mathematical framework for [linear viscoelasticity](@entry_id:181219), centered on the concept of [hereditary integrals](@entry_id:186265) and the Prony [series representation](@entry_id:175860). We then derive the thermodynamic constraints that ensure physical admissibility, providing a rigorous basis for the model parameters. Subsequently, we extend these concepts to the more complex domain of finite strains, exploring the necessary kinematic and constitutive adaptations. Finally, we introduce the principle of [time-temperature superposition](@entry_id:141843) to account for [thermo-mechanical coupling](@entry_id:176786) effects.

### Linear Viscoelasticity: The Hereditary Formulation

Unlike purely elastic materials, which exhibit an instantaneous and time-independent response to load, or purely viscous fluids, whose stress depends only on the rate of deformation, [viscoelastic materials](@entry_id:194223) exhibit a response that depends on the entire history of deformation. This "memory" is the hallmark of viscoelasticity and is mathematically captured by the **Boltzmann [superposition principle](@entry_id:144649)**.

For a one-dimensional, small-strain scenario, the stress $\sigma(t)$ at time $t$ is not simply proportional to the current strain $\epsilon(t)$, but is instead a [linear functional](@entry_id:144884) of the strain history $\epsilon(s)$ for all past times $s \le t$. This relationship is expressed through a **[hereditary integral](@entry_id:199438)**, also known as a [convolution integral](@entry_id:155865). Assuming the material is quiescent for $t  0$, the stress can be written as:
$$
\sigma(t) = \int_{0}^{t} G(t-s) \frac{d\epsilon(s)}{ds} ds
$$
Here, $G(t)$ is the **[stress relaxation modulus](@entry_id:181332)**, a fundamental material function that characterizes the decay of stress over time following the application of a sudden, constant strain. Specifically, if a unit step strain $\epsilon(t) = H(t)$ is applied (where $H(t)$ is the Heaviside [step function](@entry_id:158924)), the resulting stress is precisely $\sigma(t) = G(t)$.

#### The Relaxation Modulus and Creep Compliance

The dual concept to stress relaxation is **creep**, which describes the gradual increase in strain over time under a constant applied stress. The material function characterizing this behavior is the **[creep compliance](@entry_id:182488)**, $J(t)$. It is defined as the strain response to a unit step stress, $\sigma(t) = H(t)$ [@problem_id:3578005]. The strain history for a general stress history $\sigma(s)$ can be written in a form analogous to the [stress relaxation](@entry_id:159905) integral:
$$
\epsilon(t) = \int_{0}^{t} J(t-s) \frac{d\sigma(s)}{ds} ds
$$
The [relaxation modulus](@entry_id:189592) $G(t)$ and [creep compliance](@entry_id:182488) $J(t)$ are not independent. Their relationship can be elegantly established using the Laplace transform. Denoting the Laplace transform of a function $f(t)$ as $\tilde{f}(s)$, the convolution integrals for stress and strain become algebraic expressions in the Laplace domain. For zero initial conditions, they are $\tilde{\sigma}(s) = s\tilde{G}(s)\tilde{\epsilon}(s)$ and $\tilde{\epsilon}(s) = s\tilde{J}(s)\tilde{\sigma}(s)$. Substituting one into the other immediately reveals their interdependence [@problem_id:3578005]:
$$
s^2 \tilde{G}(s) \tilde{J}(s) = 1
$$
This fundamental identity shows that if one of the functions is known, the other is uniquely determined. This relationship can also be expressed in the time domain through a pair of Volterra integral equations, which state that the convolution of one function with the time derivative of the other yields the Heaviside step function.

#### Isotropic Decomposition: Shear and Bulk Response

For three-dimensional, isotropic linear [viscoelastic materials](@entry_id:194223), the constitutive response can be conveniently decoupled into a **deviatoric** (shape-changing) part and a **spherical** or **volumetric** (volume-changing) part. This is a direct extension of the structure of [isotropic linear elasticity](@entry_id:185899) [@problem_id:3578046].

The stress tensor $\boldsymbol{\sigma}$ and the [infinitesimal strain tensor](@entry_id:167211) $\boldsymbol{\epsilon}$ are additively decomposed into their deviatoric and spherical components:
$$
\boldsymbol{\sigma} = \boldsymbol{s} + p\boldsymbol{I}, \quad \text{where } \boldsymbol{s} = \operatorname{dev}(\boldsymbol{\sigma}) \text{ and } p = \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})
$$
$$
\boldsymbol{\epsilon} = \boldsymbol{\epsilon}_{\mathrm{dev}} + \epsilon_{\mathrm{vol}}\boldsymbol{I}, \quad \text{where } \boldsymbol{\epsilon}_{\mathrm{dev}} = \operatorname{dev}(\boldsymbol{\epsilon}) \text{ and } \epsilon_{\mathrm{vol}} = \frac{1}{3}\operatorname{tr}(\boldsymbol{\epsilon})
$$
Here, $\boldsymbol{s}$ is the [deviatoric stress tensor](@entry_id:267642), $p$ is the mean stress (or pressure), $\boldsymbol{\epsilon}_{\mathrm{dev}}$ is the [deviatoric strain](@entry_id:201263), $\epsilon_{\mathrm{vol}}$ is the volumetric strain, and $\boldsymbol{I}$ is the second-order identity tensor.

The Boltzmann [superposition principle](@entry_id:144649) is then applied separately to each part. The deviatoric stress is related to the history of the [deviatoric strain](@entry_id:201263) via the **shear [relaxation modulus](@entry_id:189592)**, $G(t)$, while the [mean stress](@entry_id:751819) is related to the history of the [volumetric strain](@entry_id:267252) via the **bulk [relaxation modulus](@entry_id:189592)**, $K(t)$.
$$
\boldsymbol{s}(t) = 2 \int_{0}^{t} G(t-s) \dot{\boldsymbol{\epsilon}}_{\mathrm{dev}}(s) ds
$$
$$
p(t) = 3 \int_{0}^{t} K(t-s) \dot{\epsilon}_{\mathrm{vol}}(s) ds
$$
The factors of $2$ and $3$ arise from the standard conventions in [elasticity theory](@entry_id:203053). This powerful decomposition allows the complex time-dependent behavior of an [isotropic material](@entry_id:204616) to be fully characterized by just two scalar functions, $G(t)$ and $K(t)$.

### The Physical Basis of Viscoelastic Relaxation: Prony Series

While $G(t)$ and $K(t)$ can be any functions that satisfy certain mathematical and physical constraints, a particularly useful and physically motivated representation is the **Prony series** (also known as a generalized Dirichlet series). This represents the [relaxation modulus](@entry_id:189592) as a sum of decaying exponential functions.

#### The Generalized Maxwell Model

The Prony series form can be directly derived from a simple rheological model known as the **generalized Maxwell model** (or Wiechert model) [@problem_id:3578037]. This model consists of a purely elastic spring placed in parallel with several **Maxwell elements**. Each Maxwell element, in turn, consists of an elastic spring and a viscous dashpot connected in series.

For a shear deformation, if we have one main spring with shear modulus $G_\infty$ and $N$ Maxwell elements, where the $i$-th element has a spring with modulus $G_i$ and a dashpot with viscosity $\eta_i$, the total shear stress is the sum of the stresses in the parallel branches. Upon application of a step strain, the stress in the purely elastic branch is constant, while the stress in each Maxwell branch relaxes exponentially. The resulting total shear [relaxation modulus](@entry_id:189592) takes the form of a Prony series:
$$
G(t) = G_{\infty} + \sum_{i=1}^{N} G_{i} e^{-t/\tau_{i}}
$$
Here, $G_{\infty}$ is the [shear modulus](@entry_id:167228) of the main spring, representing the **long-time equilibrium modulus**—the stiffness remaining after all relaxation processes have completed. Each $G_i$ is a **partial modulus** corresponding to a non-equilibrium relaxation mode, and $\tau_{i} = \eta_i / G_i$ is the **relaxation time** of the $i$-th Maxwell element, characterizing the timescale of its decay process. A similar Prony series can be constructed for the [bulk modulus](@entry_id:160069) $K(t)$.

#### Thermodynamic Constraints and Admissibility

The parameters in the Prony series are not arbitrary; they are constrained by fundamental physical principles, primarily the Second Law of Thermodynamics, which dictates that mechanical [energy dissipation](@entry_id:147406) must be non-negative in any [isothermal process](@entry_id:143096) [@problem_id:3577995]. This is formalized by the **Clausius-Duhem inequality**.

For the generalized Maxwell model, dissipation occurs only in the dashpots. Using an internal variable formulation, where internal variables represent the strains in the Maxwell elements, the [dissipation rate](@entry_id:748577) $\mathcal{D}$ can be rigorously derived. For the deviatoric response, this derivation yields:
$$
\mathcal{D}_{\mathrm{dev}} = \sum_{i=1}^{N} \frac{2G_i}{\tau_i} (\tau_i \dot{\boldsymbol{\alpha}}_i) : (\tau_i \dot{\boldsymbol{\alpha}}_i) = \sum_{i=1}^{N} 2 G_{i} \tau_{i} (\dot{\boldsymbol{\alpha}}_{i} : \dot{\boldsymbol{\alpha}}_{i}) \ge 0
$$
where $\boldsymbol{\alpha}_i$ is the internal strain variable for the $i$-th Maxwell element. Since the term $\dot{\boldsymbol{\alpha}}_{i} : \dot{\boldsymbol{\alpha}}_{i}$ is a squared norm and thus always non-negative, the inequality must hold for any arbitrary deformation history. This is only possible if each term in the sum is individually non-negative. As [relaxation times](@entry_id:191572) $\tau_i$ must be positive for a dissipative process, this directly imposes the constraints:
$$
G_i \ge 0 \quad \text{for all } i=1, \dots, N
$$
Furthermore, [material stability](@entry_id:183933) requires that the long-term equilibrium modulus be non-negative, $G_\infty \ge 0$. These conditions, along with $\tau_i  0$, ensure not only non-negative dissipation but also that the Helmholtz free energy function is convex and non-negative, guaranteeing [material stability](@entry_id:183933).

More generally, the principles of causality, fading memory, and [thermodynamic consistency](@entry_id:138886) impose strong mathematical requirements on the form of the relaxation functions [@problem_id:3578069]. They require that the [relaxation modulus](@entry_id:189592) $G(t)$ must be a **completely [monotone function](@entry_id:637414)**, meaning it is non-negative, non-increasing, and convex ($G(t) \ge 0$, $G'(t) \le 0$, $G''(t) \ge 0$, and so on for all higher derivatives). The conditions $G_\infty \ge 0$, $G_i \ge 0$, and $\tau_i  0$ are precisely what ensure that the Prony [series representation](@entry_id:175860) of $G(t)$ satisfies this strict requirement. Similarly, the [creep compliance](@entry_id:182488) $J(t)$ must be a **Bernstein function**, meaning it is non-negative and its first derivative is completely monotone.

### The Realm of Finite Strains

The linear theory described above is built on the **[infinitesimal strain tensor](@entry_id:167211)**, $\boldsymbol{\epsilon} = \frac{1}{2}(\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^\top)$, where $\boldsymbol{u}$ is the [displacement field](@entry_id:141476). The validity of this theory is restricted to problems where the [displacement gradient](@entry_id:165352) $\nabla\boldsymbol{u}$ is small, i.e., $\|\nabla\boldsymbol{u}\| \ll 1$. This implies that both strains and material rotations must be small. When deformations or rotations become large, this linearized kinematic framework is no longer adequate, and a finite-strain formulation is required [@problem_id:3577989].

#### Kinematic and Energetic Preliminaries

Finite-strain mechanics involves a more complex set of kinematic and [stress measures](@entry_id:198799). The fundamental measure of deformation is the **deformation gradient**, $\boldsymbol{F}$, which maps vectors from the undeformed (reference) configuration to the deformed (current) configuration.

A key principle in formulating constitutive laws is **[material frame-indifference](@entry_id:178419)** (or objectivity), which asserts that material response must be independent of the observer's [rigid-body motion](@entry_id:265795). This requires the use of objective tensors. Several [stress measures](@entry_id:198799) are used, each with a specific definition and purpose [@problem_id:3577999]:
-   The **Cauchy stress** $\boldsymbol{\sigma}$ is the true stress in the current configuration. It is symmetric and objective.
-   The **First Piola-Kirchhoff stress** $\boldsymbol{P}$ relates forces in the current configuration to areas in the reference configuration. It is not symmetric in general.
-   The **Second Piola-Kirchhoff stress** $\boldsymbol{S}$ is a symmetric stress tensor defined in the reference configuration. It is related to the Cauchy stress via $\boldsymbol{S} = J\boldsymbol{F}^{-1}\boldsymbol{\sigma}\boldsymbol{F}^{-\top}$, where $J = \det(\boldsymbol{F})$.
-   The **Kirchhoff stress** $\boldsymbol{\tau} = J\boldsymbol{\sigma}$ is an objective stress measure in the current configuration, energetically conjugate to the rate of deformation.

The [mechanical power](@entry_id:163535) (rate of work) per unit reference volume, $P_R$, can be expressed in terms of work-conjugate pairs:
$$
P_R = \boldsymbol{P}:\dot{\boldsymbol{F}} = \boldsymbol{S}:\dot{\boldsymbol{E}} = \boldsymbol{\tau}:\boldsymbol{d}
$$
where $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{F}^\top\boldsymbol{F} - \boldsymbol{I})$ is the objective Green-Lagrange strain tensor and $\boldsymbol{d}$ is the **[rate of deformation tensor](@entry_id:182598)**, the symmetric part of the [spatial velocity gradient](@entry_id:187198) $\boldsymbol{L} = \dot{\boldsymbol{F}}\boldsymbol{F}^{-1}$. The pair $(\boldsymbol{\tau}, \boldsymbol{d})$ is particularly important for modeling viscous effects, as $\boldsymbol{d}$ is an objective measure of the rate of stretching and shearing in the current configuration [@problem_id:3577994].

#### The Isochoric-Volumetric Split: A Framework for Nonlinear Modeling

A powerful strategy for modeling compressible materials at [finite strain](@entry_id:749398), especially polymers and elastomers, is to assume that the material's response can be uncoupled into a volumetric part (related to volume change) and an isochoric part (related to shape change at constant volume) [@problem_id:3578018]. This is achieved through a **[multiplicative decomposition](@entry_id:199514) of the [deformation gradient](@entry_id:163749)**:
$$
\boldsymbol{F} = \boldsymbol{F}_{\text{iso}} \boldsymbol{F}_{\text{vol}}
$$
A standard choice is to define the volumetric part as a pure spherical stretch that accounts for all volume change, $\boldsymbol{F}_{\text{vol}} = J^{1/3}\boldsymbol{I}$, where $J = \det(\boldsymbol{F})$. This implies the isochoric part is $\boldsymbol{F}_{\text{iso}} = J^{-1/3}\boldsymbol{F}$, which has the property $\det(\boldsymbol{F}_{\text{iso}}) = 1$.

This kinematic split enables an **additive decomposition of the Helmholtz free energy** density, $\psi$, into an isochoric part dependent on the isochoric strain and a volumetric part dependent on the volume change:
$$
\psi(\boldsymbol{F}) = \psi_{\text{iso}}(\bar{\boldsymbol{C}}) + \psi_{\text{vol}}(J)
$$
where $\bar{\boldsymbol{C}} = J^{-2/3}\boldsymbol{C} = \boldsymbol{F}_{\text{iso}}^\top\boldsymbol{F}_{\text{iso}}$ is the isochoric right Cauchy-Green tensor. This framework naturally leads to an additive split of the Kirchhoff stress into a deviatoric part derived from $\psi_{\text{iso}}$ and a spherical part derived from $\psi_{\text{vol}}$ [@problem_id:3578018].

### Constitutive Models for Finite Strain Viscoelasticity

The isochoric-volumetric split provides a robust foundation for extending linear [viscoelastic models](@entry_id:192483) to the [finite strain](@entry_id:749398) regime. It is common to associate [viscoelasticity](@entry_id:148045) (i.e., rate-dependence and dissipation) primarily with the isochoric (deviatoric) response, while modeling the volumetric response as purely elastic. This aligns with the physical observation that many materials, like elastomers, exhibit significant shear relaxation but behave nearly elastically under [hydrostatic pressure](@entry_id:141627).

One common approach is **[quasi-linear viscoelasticity](@entry_id:753957)**, where the [hereditary integral](@entry_id:199438) is generalized to operate on objective, finite-strain stress or [strain measures](@entry_id:755495) derived from a hyperelastic potential [@problem_id:3578001]. For instance, the total deviatoric Kirchhoff stress can be expressed as a convolution of a normalized relaxation function $g(t) = G(t)/G(0)$ with the rate of the instantaneous deviatoric hyperelastic stress:
$$
\operatorname{dev}(\boldsymbol{\tau}(t)) = \int_0^t g(\xi(t)-\xi(s)) \frac{d}{ds} \left[ \operatorname{dev}(\boldsymbol{\tau}_{\text{e,iso}}(s)) \right] ds
$$
where $\boldsymbol{\tau}_{\text{e,iso}}$ is the instantaneous isochoric stress derived from $\psi_{\text{iso}}$, and the time argument is replaced by reduced time differences to account for temperature effects, as discussed below. This formulation correctly reduces to the linear model at small strains and preserves [frame-indifference](@entry_id:197245).

### Thermo-Viscoelasticity: Time-Temperature Superposition

The [mechanical properties](@entry_id:201145) of many [viscoelastic materials](@entry_id:194223), especially polymers, are highly sensitive to temperature. The **Time-Temperature Superposition (TTS)** principle provides a framework for modeling this dependence for a class of materials known as **thermorheologically simple**. The core idea is that increasing temperature accelerates [molecular motion](@entry_id:140498), having the same effect on the [relaxation modulus](@entry_id:189592) as compressing the timescale [@problem_id:3578054].

This effect is quantified by a **[shift factor](@entry_id:158260)**, $a_T(T)$, which depends on the temperature $T$. For a non-[isothermal process](@entry_id:143096) with a temperature history $T(t)$, we define a **reduced time** (or material time), $\xi(t)$, which represents the time that would have elapsed if the process had occurred at a constant reference temperature, $T_{\text{ref}}$. A common convention defines its rate of change as:
$$
\frac{d\xi}{dt} = a_T(T(t))
$$
Integrating this gives the reduced time at time $t$: $\xi(t) = \int_0^t a_T(T(s)) ds$.

The [hereditary integral](@entry_id:199438) for stress is then modified by replacing the chronological time difference $(t-s)$ with the reduced time difference $(\xi(t) - \xi(s))$:
$$
\boldsymbol{\sigma}(t) = \int_0^t G_{\text{ref}}(\xi(t)-\xi(s)) \dot{\boldsymbol{\epsilon}}(s) ds
$$
where $G_{\text{ref}}$ is the [relaxation modulus](@entry_id:189592) measured at the reference temperature. When $G_{\text{ref}}$ is a Prony series, each exponential term transforms as $e^{-(t-s)/\tau_i} \rightarrow e^{-(\xi(t)-\xi(s))/\tau_i}$. This ensures that the entire [relaxation spectrum](@entry_id:192983) is shifted uniformly.

A widely used empirical model for the [shift factor](@entry_id:158260) in polymers above their glass transition temperature is the **Williams-Landel-Ferry (WLF) equation** [@problem_id:3578011]:
$$
\log_{10} a_T = \frac{C_1 (T - T_{\text{ref}})}{C_2 + (T - T_{\text{ref}})}
$$
where $C_1$ and $C_2$ are material-specific constants. With this convention for $a_T$, lower temperatures ($T  T_{\text{ref}}$) yield $a_T  1$, corresponding to a slowing of the reduced time clock and slower relaxation. An alternative convention (often used in finite element software) inverts the definition, resulting in $a_T > 1$ for $T  T_{\text{ref}}$. Regardless of convention, the physical result is the same: the effective relaxation time at temperature $T$ is scaled relative to the reference [relaxation time](@entry_id:142983) $\tau_i^{\text{ref}}$. For example, for the WLF convention above, $\tau_i(T) = \tau_i^{\text{ref}} / a_T(T)$, such that for $T  T_{\text{ref}}$, $a_T  1$ and the effective [relaxation time](@entry_id:142983) $\tau_i(T)$ increases, correctly modeling slower [relaxation kinetics](@entry_id:191610) at lower temperatures. This principle applies identically to both linear and properly formulated finite-strain models [@problem_id:3578011].