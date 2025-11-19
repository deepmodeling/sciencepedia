## Introduction
Modeling materials like metals, polymers, and soils that undergo large, permanent deformations is a central challenge in [solid mechanics](@entry_id:164042). When deformations are large, the simple additive [strain decomposition](@entry_id:186005) of small-strain theory breaks down, both kinematically and physically. A more robust and rigorous framework is required to accurately capture the complex interplay between recoverable elastic response and irreversible [plastic flow](@entry_id:201346). This article provides a systematic development of modern [finite strain](@entry_id:749398) [plasticity theory](@entry_id:177023), building the concepts from the ground up to form a cohesive and powerful predictive tool.

The "Principles and Mechanisms" chapter establishes the theoretical bedrock, introducing the [kinematics](@entry_id:173318) of large deformations, the crucial concept of [multiplicative decomposition](@entry_id:199514), and the [thermodynamic principles](@entry_id:142232) that govern all consistent [constitutive models](@entry_id:174726). Following this, the "Applications and Interdisciplinary Connections" chapter demonstrates the framework's power by exploring its use in modeling anisotropy, [crystal plasticity](@entry_id:141273), [geomechanics](@entry_id:175967), and [ductile fracture](@entry_id:161045), connecting the abstract theory to real-world material behaviors. Finally, the "Hands-On Practices" section offers opportunities to apply these concepts by tackling key problems in the computational implementation of [finite strain](@entry_id:749398) plasticity models, bridging the gap between theory and numerical simulation.

## Principles and Mechanisms

This chapter delves into the fundamental principles and theoretical mechanisms that constitute the modern framework of [finite strain](@entry_id:749398) plasticity. We will move from the essential [kinematics](@entry_id:173318) of [large deformations](@entry_id:167243) to the cornerstone concept of [multiplicative decomposition](@entry_id:199514), and then establish a rigorous thermodynamic basis for constructing robust [constitutive models](@entry_id:174726). The objective is to build a systematic understanding of how materials deform permanently when subjected to [large strains](@entry_id:751152), bridging physical concepts with their mathematical representations.

### Kinematics of Large Deformations

The study of any deformation begins with a precise description of motion. We consider a body occupying a region $\mathcal{B}_0$ in a **reference configuration** at time $t=0$. The position of a material point in this configuration is denoted by the vector $\mathbf{X}$. The motion of the body is described by a smooth mapping $\boldsymbol{\chi}$ that assigns to each material point $\mathbf{X}$ and time $t$ a new position $\mathbf{x}$ in the **current (or spatial) configuration**:

$\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$

The most fundamental measure of local deformation is the **deformation gradient**, denoted by the tensor $\mathbf{F}$. It is defined as the gradient of the motion map with respect to the reference position:

$\mathbf{F}(\mathbf{X}, t) = \nabla_{\mathbf{X}} \boldsymbol{\chi}(\mathbf{X}, t)$

In component form, this is written as $F_{ij} = \frac{\partial x_i}{\partial X_j}$. The [deformation gradient](@entry_id:163749) has a profound geometric meaning: it is the linear [tangent map](@entry_id:203492) that transforms an infinitesimal material line element $\mathrm{d}\mathbf{X}$ in the reference configuration into its corresponding spatial [line element](@entry_id:196833) $\mathrm{d}\mathbf{x}$ in the current configuration. This relationship is expressed by the first-order approximation:

$\mathrm{d}\mathbf{x} \approx \mathbf{F} \, \mathrm{d}\mathbf{X}$

Thus, $\mathbf{F}$ maps vectors from the [tangent space](@entry_id:141028) of the reference body, $T_{\mathbf{X}}\mathcal{B}_0$, to the tangent space of the current body, $T_{\mathbf{x}}\mathcal{B}$. It locally characterizes all changes in length and orientation of material fibers. A deformation is only possible if it preserves the orientation of material elements, which requires the Jacobian of the transformation, $J = \det(\mathbf{F})$, to be positive.

A critical requirement for any constitutive law in [continuum mechanics](@entry_id:155125) is the principle of **[material frame-indifference](@entry_id:178419)**, or **objectivity**. This principle states that the material response should not depend on the observer, which means it must be invariant under a superposed [rigid body motion](@entry_id:144691). Such a motion is described by a time-dependent rotation $\mathbf{Q}(t)$ and translation $\mathbf{c}(t)$, transforming the current position $\mathbf{x}$ to $\mathbf{x}^* = \mathbf{Q}\mathbf{x} + \mathbf{c}$. Under this transformation, the new [deformation gradient](@entry_id:163749) $\mathbf{F}^*$ becomes:

$\mathbf{F}^* = \nabla_{\mathbf{X}} \mathbf{x}^* = \nabla_{\mathbf{X}}(\mathbf{Q}\mathbf{x} + \mathbf{c}) = \mathbf{Q} \nabla_{\mathbf{X}}\mathbf{x} = \mathbf{Q}\mathbf{F}$

The [deformation gradient](@entry_id:163749) itself is clearly not objective, as it rotates with the observer. This makes it an unsuitable measure of strain for direct use in [constitutive equations](@entry_id:138559). We must therefore construct [strain measures](@entry_id:755495) that are immune to these superposed rotations. A primary example is the **right Cauchy-Green tensor**, $\mathbf{C}$:

$\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$

Under a superposed rigid motion, $\mathbf{C}$ transforms as $\mathbf{C}^* = (\mathbf{F}^*)^{\mathsf{T}}\mathbf{F}^* = (\mathbf{Q}\mathbf{F})^{\mathsf{T}}(\mathbf{Q}\mathbf{F}) = \mathbf{F}^{\mathsf{T}}\mathbf{Q}^{\mathsf{T}}\mathbf{Q}\mathbf{F} = \mathbf{F}^{\mathsf{T}}\mathbf{I}\mathbf{F} = \mathbf{C}$. Because $\mathbf{C}$ is invariant, it is an objective tensor, and any scalar function of its components (such as its invariants) will also be objective. This property makes it a suitable candidate for defining strain and formulating constitutive laws. For instance, the **Green-Lagrange [strain tensor](@entry_id:193332)**, $\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I})$, is also objective and measures the deviation from a rigid motion. In contrast, measures based on the displacement field $\mathbf{u} = \mathbf{x} - \mathbf{X}$, like the **material [displacement gradient](@entry_id:165352)** $\mathbf{H} = \nabla_{\mathbf{X}}\mathbf{u} = \mathbf{F} - \mathbf{I}$, are not objective and are therefore less suitable for [finite deformation](@entry_id:172086) theories.

### The Multiplicative Decomposition and the Intermediate Configuration

In small strain plasticity, it is common to additively decompose the total strain into elastic and plastic parts: $\boldsymbol{\epsilon} = \boldsymbol{\epsilon}_e + \boldsymbol{\epsilon}_p$. This simple split is conceptually and kinematically invalid for [large deformations](@entry_id:167243). The correct framework, introduced by Lee and Liu, is the **[multiplicative decomposition](@entry_id:199514)** of the [deformation gradient](@entry_id:163749):

$\mathbf{F} = \mathbf{F}_{e} \mathbf{F}_{p}$

This decomposition introduces a conceptual, local, stress-free **intermediate configuration**. The tensor $\mathbf{F}_{p}$ represents the plastic part of the deformation, mapping material neighborhoods from the reference configuration to this intermediate configuration. This mapping accounts for permanent, irreversible changes in the material's microstructure, such as those caused by dislocation motion. The tensor $\mathbf{F}_{e}$ represents the elastic part, mapping from the stress-free intermediate configuration to the final, stressed current configuration. This part accounts for the recoverable stretching and rotation of the crystal lattice.

The intermediate configuration is a powerful but abstract concept with several key properties:
1.  **Incompatibility**: In general, the plastically deformed local neighborhoods do not fit together to form a continuous body. This means the [tensor field](@entry_id:266532) $\mathbf{F}_{p}$ is not the gradient of a global vector field, a condition mathematically expressed as $\mathrm{Curl}(\mathbf{F}_{p}) \neq \mathbf{0}$. This incompatibility has a clear physical interpretation: it represents the continuum-level manifestation of a net density of **[geometrically necessary dislocations](@entry_id:187571)** (GNDs), which accommodate the [lattice misfit](@entry_id:196802) between differently deformed regions. A theory that required $\mathbf{F}_p$ to be compatible would be severely limited.

2.  **Non-Uniqueness**: The intermediate configuration is not unique. Since it is a conceptual stress-free state, its orientation is arbitrary. For any orthogonal tensor $\mathbf{Q}$ (a rotation), we can define a new pair of elastic and plastic deformation gradients $(\tilde{\mathbf{F}}_{e}, \tilde{\mathbf{F}}_{p}) = (\mathbf{F}_{e}\mathbf{Q}, \mathbf{Q}^{\mathsf{T}}\mathbf{F}_{p})$. The product remains the same: $\tilde{\mathbf{F}}_{e}\tilde{\mathbf{F}}_{p} = \mathbf{F}_{e}\mathbf{Q}\mathbf{Q}^{\mathsf{T}}\mathbf{F}_{p} = \mathbf{F}$. This rotational freedom means that the constitutive laws must be formulated in a way that is insensitive to the choice of orientation of the intermediate configuration.

3.  **Crystal Symmetry**: For [crystalline materials](@entry_id:157810), the non-uniqueness is even greater. The crystal lattice is invariant under a set of [symmetry operations](@entry_id:143398) (rotations, reflections) that form the crystal's point group. If $\mathbf{G}$ is such a symmetry operation, then the state described by $\mathbf{F}_p$ is physically indistinguishable from that described by $\mathbf{G}^{-1}\mathbf{F}_p$. Consequently, the decomposition is equivalent up to these [discrete symmetries](@entry_id:158714): $(\mathbf{F}_{e}\mathbf{G}, \mathbf{G}^{-1}\mathbf{F}_{p})$ produces the same total deformation $\mathbf{F}$ and the same physical state.

For many metals, [plastic deformation](@entry_id:139726) occurs primarily via dislocation slip, a shear mechanism that conserves volume. This physical observation is modeled by imposing the constraint of **[plastic incompressibility](@entry_id:183440)**, or that the plastic deformation is **isochoric**:

$\det(\mathbf{F}_{p}) = 1$

From the property $\det(\mathbf{F}) = \det(\mathbf{F}_{e}\mathbf{F}_{p}) = \det(\mathbf{F}_{e})\det(\mathbf{F}_{p})$, this constraint implies that the total volume change $J = \det(\mathbf{F})$ is entirely due to the [elastic deformation](@entry_id:161971): $J = J_e = \det(\mathbf{F}_{e})$. This assumption provides a clean separation where all volumetric response is elastic, and the plastic response is purely deviatoric (shape-changing).

### Stress Measures and Work Conjugacy

To connect [kinematics](@entry_id:173318) with dynamics and thermodynamics, we must establish the relationship between [stress and strain](@entry_id:137374) rates through the concept of [mechanical power](@entry_id:163535). The rate of work done by internal stresses per unit volume, or **[power density](@entry_id:194407)**, must be an objective scalar, independent of the choice of coordinate system or configuration in which it is expressed.

In the current configuration, the [power density](@entry_id:194407) $p$ is given by the double contraction of the symmetric **Cauchy stress** $\boldsymbol{\sigma}$ (the "true" stress, force per current area) and the **[rate of deformation tensor](@entry_id:182598)** $\mathbf{D}$, which is the symmetric part of the [spatial velocity gradient](@entry_id:187198) $\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}$.

$p = \boldsymbol{\sigma} : \mathbf{D}$

The pair $(\boldsymbol{\sigma}, \mathbf{D})$ is said to be **work-conjugate**. Since the skew-symmetric part of $\mathbf{L}$ (the [spin tensor](@entry_id:187346) $\mathbf{W}$) represents a rigid rotation rate, it does no work when contracted with the symmetric stress tensor ($\boldsymbol{\sigma} : \mathbf{W} = 0$).

Often, it is more convenient to express power density with respect to the reference volume, $P_0$. Since an infinitesimal current volume $dv$ is related to the reference volume $dV$ by $dv = J dV$, we have $P_0 = J p = J (\boldsymbol{\sigma} : \mathbf{D})$. This motivates the definition of the **Kirchhoff stress** $\boldsymbol{\tau}$:

$\boldsymbol{\tau} = J \boldsymbol{\sigma}$

The Kirchhoff stress is work-conjugate to $\mathbf{D}$ for power per unit reference volume: $P_0 = \boldsymbol{\tau} : \mathbf{D}$.

For developing constitutive laws based on reference configuration quantities, we can perform a "pull-back" operation. The power per reference volume can be equivalently written as:

$P_0 = \mathbf{S} : \dot{\mathbf{E}}$

Here, $\mathbf{E}$ is the Green-Lagrange strain tensor, and $\mathbf{S}$ is the **second Piola-Kirchhoff stress** tensor. $\mathbf{S}$ is related to the other [stress measures](@entry_id:198799) via the pull-back transformation:

$\mathbf{S} = \mathbf{F}^{-1} \boldsymbol{\tau} \mathbf{F}^{-\mathsf{T}} = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-\mathsf{T}}$

The tensor $\mathbf{S}$ is objective and symmetric. It is work-conjugate to the rate of the Green-Lagrange strain, $\dot{\mathbf{E}} = \frac{1}{2}\dot{\mathbf{C}}$. The existence of these different but energetically [equivalent stress](@entry_id:749064)-[strain rate](@entry_id:154778) pairs is fundamental to [finite strain theory](@entry_id:176941), as it allows for the formulation of physical laws in the most convenient configuration.

### A Thermodynamic Foundation for Plasticity

Plasticity is an inherently dissipative process. The Second Law of Thermodynamics, in the form of the **Clausius-Duhem inequality** (CDI), provides the fundamental constraint that the rate of internal dissipation must be non-negative. For an [isothermal process](@entry_id:143096), the CDI per unit reference volume states:

$\mathcal{D} = \mathbf{P} : \dot{\mathbf{F}} - \dot{\psi} \ge 0$

where $\mathbf{P}$ is the first Piola-Kirchhoff stress, and $\psi$ is the Helmholtz free energy density per unit reference volume. We postulate that the free energy is a function of the state variables that characterize the material's stored energy. In [elastoplasticity](@entry_id:193198), these are the elastic strain and a set of internal variables describing the plastic state (e.g., hardening). A standard choice is $\psi = \psi(\mathbf{C}_e, \boldsymbol{\alpha})$, where $\mathbf{C}_e = \mathbf{F}_e^{\mathsf{T}}\mathbf{F}_e$ is the elastic right Cauchy-Green tensor and $\boldsymbol{\alpha}$ is a set of internal variables.

The **Coleman-Noll procedure** is a systematic method to exploit the CDI. By expanding $\dot{\psi}$ using the chain rule and substituting the kinematic relations derived from $\mathbf{F} = \mathbf{F}_e \mathbf{F}_p$, we can separate the terms in the inequality. The procedure argues that since the inequality must hold for any process, including purely elastic ones where plastic rates are zero, the coefficients of the elastic rates must vanish. This yields two crucial results:
1.  An **elastic constitutive law** for stress, which relates stress to the derivative of the free energy with respect to the [elastic strain](@entry_id:189634) measure. For example, it provides a hyperelastic relation for the first Piola-Kirchhoff stress $\mathbf{P}$.
2.  A **reduced [dissipation inequality](@entry_id:188634)**, which governs the irreversible, plastic processes.

This reduced inequality takes a remarkably structured form when expressed in the intermediate configuration:

$\mathcal{D}_{\mathrm{int}} = \mathbf{M} : \mathbf{L}_{p} + \mathbf{A} : \dot{\boldsymbol{\alpha}} \ge 0$

Here, $\mathbf{L}_{p} = \dot{\mathbf{F}}_{p}\mathbf{F}_{p}^{-1}$ is the **plastic [velocity gradient](@entry_id:261686)**, which describes the rate of [plastic deformation](@entry_id:139726) in the intermediate configuration. The tensor $\mathbf{M}$ is the **Mandel stress**, and $\mathbf{A}$ represents the thermodynamic forces conjugate to the rates of the internal variables $\dot{\boldsymbol{\alpha}}$.

The Mandel stress is defined as $\mathbf{M} = \mathbf{C}_e \mathbf{S}_e$, where $\mathbf{S}_e = 2 \frac{\partial\psi}{\partial\mathbf{C}_e}$ is the second Piola-Kirchhoff-like stress defined with respect to the elastic deformation. The central importance of the Mandel stress is that it is the stress measure in the intermediate configuration that is power-conjugate to the plastic velocity gradient $\mathbf{L}_p$. This makes it the natural stress measure for formulating [plastic flow](@entry_id:201346) laws.

The plastic [velocity gradient](@entry_id:261686) $\mathbf{L}_p$ can be decomposed into its symmetric part, $\mathbf{D}_p = \mathrm{sym}(\mathbf{L}_p)$, the **plastic rate of deformation**, and its skew-symmetric part, $\mathbf{W}_p = \mathrm{skw}(\mathbf{L}_p)$, the **[plastic spin](@entry_id:188692)**. $\mathbf{D}_p$ describes the rate of plastic stretching and shearing, while $\mathbf{W}_p$ describes the rate of plastic rotation of the material's substructure. Assuming the Mandel stress is symmetric (which is true for [isotropic elasticity](@entry_id:203237)), the [plastic dissipation](@entry_id:201273) depends only on the symmetric part: $\mathbf{M} : \mathbf{L}_p = \mathbf{M} : \mathbf{D}_p$.

### Constitutive Laws for Plastic Flow

The thermodynamic framework provides the stage; the constitutive laws are the actors that define a specific material's behavior. A complete model requires a yield condition, a [flow rule](@entry_id:177163), and a [hardening law](@entry_id:750150).

#### Yield Condition

The **yield condition** defines the boundary of the elastic domain in [stress space](@entry_id:199156). For [finite strain](@entry_id:749398) plasticity, it is most appropriately formulated in the intermediate configuration using the Mandel stress. A general form is $f(\mathbf{M}, \boldsymbol{\alpha}) \le 0$.

A widely used model for metals is the **$J_2$ or von Mises yield criterion**. This criterion posits that yielding is independent of hydrostatic pressure and depends only on the second invariant of the [deviatoric stress](@entry_id:163323). In the context of the Mandel stress, it is written as:

$f(\mathbf{M}, \kappa) = \Phi(\mathbf{M}) - \sigma_y(\kappa) = \sqrt{\frac{3}{2}} \|\mathbf{M}'\| - \sigma_y(\kappa) \le 0$

Here, $\mathbf{M}'$ is the deviatoric part of the Mandel stress, $\|\cdot\|$ is the Frobenius norm, $\kappa$ is a scalar internal variable representing [isotropic hardening](@entry_id:164486), and $\sigma_y$ is the current [yield strength](@entry_id:162154). This form is justified because [plastic incompressibility](@entry_id:183440) ($\det(\mathbf{F}_p)=1$) implies $\mathrm{tr}(\mathbf{D}_p)=0$. Since the hydrostatic part of the stress, $\mathrm{tr}(\mathbf{M})$, does no work on the trace-free plastic rate of deformation, it does not contribute to [plastic dissipation](@entry_id:201273) and should not influence yielding.

#### Hardening Law

The evolution of the yield surface is described by **[hardening laws](@entry_id:183802)**. For [isotropic hardening](@entry_id:164486), the yield surface expands uniformly. This is modeled by letting the yield stress $\sigma_y$ depend on an internal variable, such as the accumulated plastic strain $\kappa$. The thermodynamic framework provides a rigorous way to define this dependence. If we include a stored energy of hardening $\psi_h(\kappa)$ in the Helmholtz free energy, such that $\psi = \psi_e(\mathbf{C}_e) + \psi_h(\kappa)$, the reduced [dissipation inequality](@entry_id:188634) becomes:

$\mathcal{D}_{\mathrm{int}} = \mathbf{M} : \mathbf{D}_{p} - R(\kappa) \dot{\kappa} \ge 0$

where $R(\kappa) = \frac{d\psi_h}{d\kappa}$ is the **thermodynamic hardening force** conjugate to the rate $\dot{\kappa}$. This force represents the material's energetic resistance to further [plastic deformation](@entry_id:139726). The [yield strength](@entry_id:162154) is then expressed as $\sigma_y(\kappa) = \sigma_0 + R(\kappa)$, where $\sigma_0$ is the initial yield strength. For a given hardening energy function, such as a mixed linear-Voce form, the hardening force $R(\kappa)$ can be computed directly by differentiation.

#### Flow Rule

The **[flow rule](@entry_id:177163)** specifies the direction of [plastic flow](@entry_id:201346) once the yield condition is met. The principle of maximum dissipation leads to the powerful concept of an **[associative flow rule](@entry_id:163391)**, where the plastic rates are normal to the [yield surface](@entry_id:175331). This is formalized by defining a convex dissipation potential, which for standard [rate-independent plasticity](@entry_id:754082) is the indicator function of the elastic domain. Using convex analysis, this leads to the **[normality rule](@entry_id:182635)**: the plastic fluxes are given by the gradient of the yield function with respect to the conjugate [thermodynamic forces](@entry_id:161907), scaled by a non-negative consistency parameter or **[plastic multiplier](@entry_id:753519)**, $\lambda$.

This results in:
-   **Flow rule for plastic deformation**: $\mathbf{L}_p = \lambda \frac{\partial f}{\partial \mathbf{M}}$
-   **Evolution law for hardening**: $\dot{\kappa} = \lambda \frac{\partial f}{\partial (-R)}$

These equations are supplemented by the Karush-Kuhn-Tucker (KKT) complementarity conditions:
$\lambda \ge 0, \quad f(\mathbf{M}, \kappa) \le 0, \quad \lambda f(\mathbf{M}, \kappa) = 0$

These conditions ensure that plastic flow ($\lambda > 0$) occurs only when the stress state is on the yield surface ($f=0$), and no flow occurs inside the elastic domain ($f < 0$). This structure automatically satisfies the [dissipation inequality](@entry_id:188634). For a [yield function](@entry_id:167970) of the form $f = \Phi(\mathbf{M}) - (\sigma_0 + R(\kappa))$, the dissipation rate during plastic flow simplifies to $\mathcal{D} = \lambda \sigma_0$, directly linking dissipation to the initial material properties and the rate of plastic flow.

### Advanced Constitutive Considerations

#### Crystal Plasticity

The general framework finds a natural application in **[crystal plasticity](@entry_id:141273)**, which models the behavior of single crystals. Here, [plastic deformation](@entry_id:139726) occurs by slip on discrete [crystallographic slip](@entry_id:196486) systems. In the intermediate configuration, each [slip system](@entry_id:155264) $\alpha$ is defined by a slip direction $\mathbf{s}^{\alpha}$ and a [slip plane](@entry_id:275308) normal $\mathbf{m}^{\alpha}$. The plastic [velocity gradient](@entry_id:261686) is the sum of contributions from all active [slip systems](@entry_id:136401):

$\mathbf{L}_{p} = \sum_{\alpha} \dot{\gamma}^{\alpha} \mathbf{s}^{\alpha} \otimes \mathbf{m}^{\alpha}$

where $\dot{\gamma}^{\alpha}$ is the shear rate on system $\alpha$. The thermodynamic driving force for this slip is the **[resolved shear stress](@entry_id:201022)** $\tau^{\alpha}$. From the [plastic dissipation](@entry_id:201273) expression $\mathcal{D} = \mathbf{M} : \mathbf{L}_p = \sum_{\alpha} \tau^{\alpha} \dot{\gamma}^{\alpha}$, we can identify the [resolved shear stress](@entry_id:201022) as the projection of the Mandel stress onto the [slip system](@entry_id:155264):

$\tau^{\alpha} = \mathbf{M} : (\mathbf{s}^{\alpha} \otimes \mathbf{m}^{\alpha}) = \mathbf{M} : \mathbf{S}^{\alpha}$

where $\mathbf{S}^{\alpha} = \mathrm{sym}(\mathbf{s}^{\alpha} \otimes \mathbf{m}^{\alpha})$ is the symmetric Schmid tensor. This explicitly shows why the Mandel stress is the physically correct stress measure for driving plastic slip in the intermediate configuration.

#### Volumetric and Deviatoric Responses

For [isotropic materials](@entry_id:170678), it is common to decompose the elastic free energy into a **volumetric part**, which depends only on the elastic volume change $J_e$, and an **isochoric (or deviatoric) part**, which depends on the volume-preserving part of the elastic deformation, $\bar{\mathbf{C}}_e = J_e^{-2/3} \mathbf{C}_e$.

$\Psi_e(\mathbf{C}_e) = \Psi_{\mathrm{vol}}(J_e) + \Psi_{\mathrm{iso}}(\bar{\mathbf{C}}_e)$

This additive split of the energy function leads to a corresponding additive split of the Kirchhoff stress into a purely hydrostatic (spherical) part and a purely deviatoric part:

$\boldsymbol{\tau} = p \mathbf{I} + \boldsymbol{\tau}_{\mathrm{dev}}$

where the pressure $p$ is derived from $\Psi_{\mathrm{vol}}$ and the [deviatoric stress](@entry_id:163323) $\boldsymbol{\tau}_{\mathrm{dev}}$ is derived from $\Psi_{\mathrm{iso}}$. It is crucial to recognize that this elastic split does *not* predetermine the nature of plastic volume change. The plastic [volumetric strain rate](@entry_id:272471), $\mathrm{tr}(\mathbf{d}_p)$, is governed by the pressure-dependence of the **[plastic potential](@entry_id:164680)**, not the elastic energy. If the [yield criterion](@entry_id:193897) and [flow rule](@entry_id:177163) are pressure-insensitive (as in $J_2$ plasticity), the plastic flow is isochoric. However, for materials like soils or granular aggregates, where yielding is pressure-dependent (e.g., Drucker-Prager models), the [flow rule](@entry_id:177163) will generally predict plastic volume changes ([dilatancy](@entry_id:201001) or compaction), even with this elastic energy structure.