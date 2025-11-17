## Introduction
Constitutive models are the mathematical heart of modern mechanics, providing the essential link between force and deformation that enables engineers and scientists to predict how materials behave under load. While simple [linear elasticity](@entry_id:166983) is useful, real-world applications often involve complex phenomena such as large, reversible deformations (elasticity) and permanent, irreversible changes in shape (plasticity). Understanding and modeling these behaviors is critical for designing safe and efficient structures, from aerospace components to geotechnical systems.

This article provides a comprehensive, graduate-level exploration of this field. We will begin in "Principles and Mechanisms" by building the theoretical framework from the ground up, starting with thermodynamics and [kinematics](@entry_id:173318), then developing robust models for both [finite elasticity](@entry_id:181775) and plasticity. Following this, "Applications and Interdisciplinary Connections" will demonstrate how these theories are applied to solve real-world problems in engineering, geophysics, and [multiphysics](@entry_id:164478). Finally, "Hands-On Practices" will offer concrete exercises to implement and solidify these core concepts. Let's begin our exploration by examining the fundamental physical and mathematical principles that govern all material response.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that form the bedrock of [constitutive modeling](@entry_id:183370) for both elastic and plastic material behavior. We will begin with the universal laws of thermodynamics that govern all material response, establish the rigorous mathematical language of kinematics and stress for describing deformation, and then construct the specific constitutive frameworks for elasticity and plasticity. Our journey will span from the linear theories applicable to small deformations to the more general and complex theories required for finite strains and rotations.

### Thermodynamic Foundations of Constitutive Modeling

At its core, a [constitutive model](@entry_id:747751) is a mathematical expression of a material's thermodynamic response to external stimuli. The development of physically consistent models must, therefore, be grounded in the laws of thermodynamics. For a deformable continuum undergoing a reversible process, the first and second laws of thermodynamics can be combined to state that the change in internal energy density, $\mathcal{U}$, is a function of the change in entropy density, $S$, and the change in strain, $\boldsymbol{\varepsilon}$. In the small-strain regime, this is expressed as:

$$d\mathcal{U} = T\,dS + \boldsymbol{\sigma} : d\boldsymbol{\varepsilon}$$

Here, $T$ is the absolute temperature, and $\boldsymbol{\sigma}$ is the Cauchy stress tensor. This fundamental relation reveals the thermodynamic [conjugacy](@entry_id:151754) between the [state variables](@entry_id:138790) and their corresponding fluxes or forces: temperature $T$ is conjugate to entropy $S$, and stress $\boldsymbol{\sigma}$ is conjugate to strain $\boldsymbol{\varepsilon}$. When internal energy $\mathcal{U}$ is expressed as a function of its **[natural variables](@entry_id:148352)**, $S$ and $\boldsymbol{\varepsilon}$, i.e., $\mathcal{U}(S, \boldsymbol{\varepsilon})$, the [conjugate variables](@entry_id:147843) can be recovered by [partial differentiation](@entry_id:194612):

$$T = \frac{\partial \mathcal{U}}{\partial S} \quad \text{and} \quad \boldsymbol{\sigma} = \frac{\partial \mathcal{U}}{\partial \boldsymbol{\varepsilon}}$$

While internal energy is a fundamental potential, it is often more convenient to work with a different set of [independent variables](@entry_id:267118), such as temperature and strain, or temperature and stress. The mathematical tool for systematically changing the [natural variables](@entry_id:148352) of a potential is the **Legendre transform** [@problem_id:3439481]. To switch the independent variable from entropy $S$ to temperature $T$, we define the **Helmholtz free energy** density, $\psi$, as:

$$\psi(T, \boldsymbol{\varepsilon}) = \mathcal{U} - TS$$

The differential of this new potential becomes $d\psi = d\mathcal{U} - TdS - SdT$. Substituting the expression for $d\mathcal{U}$, we find:

$$d\psi = (TdS + \boldsymbol{\sigma}:d\boldsymbol{\varepsilon}) - TdS - SdT = -SdT + \boldsymbol{\sigma}:d\boldsymbol{\varepsilon}$$

From this, the [constitutive relations](@entry_id:186508) for entropy and stress are given by derivatives of the Helmholtz potential with respect to its new [natural variables](@entry_id:148352), $(T, \boldsymbol{\varepsilon})$:

$$S = -\frac{\partial \psi}{\partial T} \quad \text{and} \quad \boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}$$

This demonstrates a powerful paradigm: if we can formulate a physically realistic function for the Helmholtz free energy in terms of temperature and strain, the corresponding stress-strain relationship is obtained directly by differentiation. This is the foundation of the [hyperelasticity](@entry_id:168357) framework we will explore later.

Similarly, we can perform a Legendre transform on both thermodynamic pairs to define a **generalized Gibbs free energy** density, $G(T, \boldsymbol{\sigma})$, whose [natural variables](@entry_id:148352) are temperature and stress:

$$G(T, \boldsymbol{\sigma}) = \mathcal{U} - TS - \boldsymbol{\sigma}:\boldsymbol{\varepsilon}$$

Its differential is $dG = -SdT - \boldsymbol{\varepsilon}:d\boldsymbol{\sigma}$, which yields the [constitutive relations](@entry_id:186508) for entropy and *strain*:

$$S = -\frac{\partial G}{\partial T} \quad \text{and} \quad \boldsymbol{\varepsilon} = -\frac{\partial G}{\partial \boldsymbol{\sigma}}$$

This framework, where constitutive laws are derived from [thermodynamic potentials](@entry_id:140516), ensures that the resulting models are intrinsically consistent with the laws of thermodynamics, preventing unphysical behaviors like the creation of energy in a closed cycle.

### Kinematics of Deformation: Describing Material Motion

To build models based on strain, we first need a rigorous way to quantify it. The primary tool is the **[deformation gradient](@entry_id:163749)**, $\mathbf{F}$, which maps a differential line element $d\mathbf{X}$ from the undeformed (reference) configuration to its counterpart $d\mathbf{x}$ in the deformed (current) configuration: $d\mathbf{x} = \mathbf{F} d\mathbf{X}$.

In the **small-strain regime**, where displacements and their gradients are infinitesimal, deformation is captured by the symmetric **[infinitesimal strain tensor](@entry_id:167211)**, $\boldsymbol{\varepsilon}$, defined as the symmetric part of the [displacement gradient](@entry_id:165352) $\nabla\mathbf{u}$:

$$\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^{\mathrm{T}})$$

However, when deformations or, critically, rotations are large, the [infinitesimal strain tensor](@entry_id:167211) is inadequate. Consider a pure [rigid body rotation](@entry_id:167024) described by the motion $\mathbf{x} = \mathbf{Q}\mathbf{X}$, where $\mathbf{Q}$ is a [rotation tensor](@entry_id:191990). Since a rigid rotation induces no stretching or distortion, any valid measure of strain must be zero. For this motion, the deformation gradient is $\mathbf{F} = \mathbf{Q}$, and the displacement is $\mathbf{u} = (\mathbf{Q}-\mathbf{I})\mathbf{X}$. The [infinitesimal strain tensor](@entry_id:167211) becomes $\boldsymbol{\varepsilon} = \frac{1}{2}(\mathbf{Q} + \mathbf{Q}^{\mathrm{T}} - 2\mathbf{I})$, which is non-zero for any rotation other than identity [@problem_id:3439444]. This spurious strain indicates that $\boldsymbol{\varepsilon}$ conflates rigid rotation with true deformation, rendering it unsuitable for finite rotation analysis.

To overcome this, we require a **[finite strain](@entry_id:749398)** measure that is objective, meaning it is invariant under superposed [rigid body motions](@entry_id:200666). A robust way to define such a measure is to compare the squared length of a material [line element](@entry_id:196833) before and after deformation. The change in squared length, $ds^2 - ds_0^2$, is given by:

$$ds^2 - ds_0^2 = d\mathbf{x}^{\mathrm{T}}d\mathbf{x} - d\mathbf{X}^{\mathrm{T}}d\mathbf{X} = (\mathbf{F}d\mathbf{X})^{\mathrm{T}}(\mathbf{F}d\mathbf{X}) - d\mathbf{X}^{\mathrm{T}}d\mathbf{X} = d\mathbf{X}^{\mathrm{T}}(\mathbf{F}^{\mathrm{T}}\mathbf{F} - \mathbf{I})d\mathbf{X}$$

This expression introduces two fundamental tensors defined in the reference configuration. The **right Cauchy-Green deformation tensor**, $\mathbf{C} = \mathbf{F}^{\mathrm{T}}\mathbf{F}$, measures the local change in shape. The **Green-Lagrange [strain tensor](@entry_id:193332)**, $\mathbf{E}$, is defined as:

$$\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I})$$

The key property of $\mathbf{E}$ is its **objectivity**. If the current configuration undergoes a rigid rotation $\mathbf{Q}$, the new deformation gradient is $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$. The new right Cauchy-Green tensor is $\mathbf{C}^* = (\mathbf{F}^*)^{\mathrm{T}}\mathbf{F}^* = (\mathbf{Q}\mathbf{F})^{\mathrm{T}}(\mathbf{Q}\mathbf{F}) = \mathbf{F}^{\mathrm{T}}\mathbf{Q}^{\mathrm{T}}\mathbf{Q}\mathbf{F} = \mathbf{F}^{\mathrm{T}}\mathbf{F} = \mathbf{C}$. Since $\mathbf{C}$ is unchanged, $\mathbf{E}$ is also unchanged [@problem_id:3439444]. This confirms that $\mathbf{E}$ measures pure deformation, independent of [rigid body motion](@entry_id:144691), making it a cornerstone of [finite strain mechanics](@entry_id:749400).

It is often physically insightful to decompose a deformation into a part that changes volume and a part that changes shape at constant volume. This is accomplished via the **multiplicative volumetric-isochoric decomposition** of the [deformation gradient](@entry_id:163749) [@problem_id:3439461]. The volume change is quantified by the Jacobian, $J = \det(\mathbf{F})$. The decomposition is:

$$\mathbf{F} = J^{1/3} \bar{\mathbf{F}}$$

Here, the scalar $J^{1/3}$ represents a uniform [volumetric expansion](@entry_id:144241), while the tensor $\bar{\mathbf{F}} = J^{-1/3}\mathbf{F}$ is the **isochoric** (volume-preserving) part of the deformation, satisfying $\det(\bar{\mathbf{F}}) = 1$. This split is crucial for formulating [constitutive models](@entry_id:174726) that treat volumetric and deviatoric (shape-changing) responses independently.

### Measures of Stress: Quantifying Internal Forces

Just as [strain measures](@entry_id:755495) must be chosen carefully in [finite deformation](@entry_id:172086), so must [stress measures](@entry_id:198799). The most intuitive is the **Cauchy stress** $\boldsymbol{\sigma}$, the "true" stress, which relates the force vector $\mathbf{t}$ acting on a surface in the *deformed* configuration to the surface's normal vector $\mathbf{n}$ and area $da$: $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$.

While physically intuitive, Cauchy stress acts on the deformed geometry, which is often unknown in advance. For [constitutive modeling](@entry_id:183370), especially when strain is measured relative to the reference configuration, it is convenient to use [stress measures](@entry_id:198799) defined on the *reference* configuration.

The **First Piola-Kirchhoff (PK1) stress** $\mathbf{P}$ relates the force in the current configuration to the area in the reference configuration. It is sometimes called the "nominal" stress. The **Second Piola-Kirchhoff (PK2) stress** $\mathbf{S}$ is a more abstract but mathematically powerful measure, obtained by pulling back the PK1 stress to the reference configuration.

The relationships between these tensors can be derived from the equivalence of the force vector $d\mathbf{f}$ transmitted across a material surface, regardless of the configuration in which it is measured [@problem_id:3439465]. This derivation employs **Nanson's relation**, which connects area elements between the reference and current configurations. The resulting transformations are fundamental:

$$\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-\mathrm{T}}$$
$$\mathbf{S} = \mathbf{F}^{-1}\mathbf{P} = J \mathbf{F}^{-1}\boldsymbol{\sigma}\mathbf{F}^{-\mathrm{T}}$$

An essential property of the PK2 stress $\mathbf{S}$ is that it is work-conjugate to the Green-Lagrange strain $\mathbf{E}$. This means that the [stress power](@entry_id:182907) per unit reference volume is simply $\mathbf{S}:\dot{\mathbf{E}}$, making the pair $(\mathbf{S}, \mathbf{E})$ the natural choice for formulating finite-strain hyperelastic models. If $\boldsymbol{\sigma}$ is symmetric, then $\mathbf{S}$ is also symmetric.

### Elasticity: Reversible Material Response

Elasticity describes material behavior that is fully reversible and path-independent. When loads are removed, the material returns to its original shape, and the work done is stored as potential energy.

#### Linear Isotropic Elasticity

In the small-strain regime, the relationship between [stress and strain](@entry_id:137374) is linear. For an isotropic material, the material properties are independent of direction. By imposing the requirements of material isotropy and the inherent symmetries of the stress and strain tensors on the general linear law $\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\varepsilon}$, the [fourth-order elasticity tensor](@entry_id:188318) $\mathbb{C}$ can be reduced to a form containing just two independent material constants [@problem_id:3439484]. This is the familiar **generalized Hooke's Law**:

$$\boldsymbol{\sigma} = \lambda \operatorname{tr}(\boldsymbol{\varepsilon})\mathbf{I} + 2G \boldsymbol{\varepsilon}$$

Here, $\lambda$ and $G$ are the **Lamé parameters**. The parameter $G$ is the **shear modulus** (also denoted $\mu$), which governs the resistance to shear distortion. The parameters can be related to the more common [engineering constants](@entry_id:199413), Young's modulus $E$ and Poisson's ratio $\nu$, by considering a simple thought experiment like a [uniaxial tension test](@entry_id:195375). The resulting relationships are:

$$\lambda = \frac{E\nu}{(1+\nu)(1-2\nu)} \quad \text{and} \quad G = \frac{E}{2(1+\nu)}$$

#### Hyperelasticity: The Potential-Based Approach to Finite Elasticity

For large deformations, the linear Hooke's law is insufficient. The proper framework is **[hyperelasticity](@entry_id:168357)**, which formalizes the concept of stored elastic energy using the [thermodynamic potentials](@entry_id:140516) discussed earlier. The constitutive law is derived from a **[strain-energy density function](@entry_id:755490)**, $W$, which represents the Helmholtz free energy per unit reference volume, $\psi$. For an [isotropic material](@entry_id:204616), $W$ must be a function of the invariants of a [strain tensor](@entry_id:193332) to ensure objectivity. It is conventionally written as a function of the invariants of $\mathbf{C}$ or the left Cauchy-Green tensor $\mathbf{B} = \mathbf{F}\mathbf{F}^{\mathrm{T}}$. As shown previously, if $W$ depends on $\mathbf{F}$ only through the invariants of $\mathbf{C}$, it is automatically objective [@problem_id:3439518].

The PK2 stress is then obtained by differentiating $W$ with respect to its work-conjugate strain measure, $\mathbf{E}$, or equivalently:

$$\mathbf{S} = 2\frac{\partial W}{\partial \mathbf{C}}$$

The Cauchy stress $\boldsymbol{\sigma}$ can then be found using the push-forward transformation $\boldsymbol{\sigma} = J^{-1}\mathbf{F}\mathbf{S}\mathbf{F}^{\mathrm{T}}$. This potential-based framework guarantees that the elastic response is path-independent and energy-conservative.

A powerful strategy for constructing strain-energy functions is to separate the volumetric and isochoric responses, motivated by the kinematic split of $\mathbf{F}$ [@problem_id:3439461, @problem_id:3439508]. The energy is written as an additive sum:

$$W(\mathbf{F}) = U(J) + \bar{W}(\bar{\mathbf{F}})$$

where $U(J)$ governs the volumetric response (resistance to volume change) and $\bar{W}(\bar{\mathbf{F}})$ governs the isochoric response (resistance to shape change). For example, a simple **compressible neo-Hookean** model takes the form:

$$\psi = \frac{G}{2}(\bar{I}_1 - 3) + \frac{\kappa}{2}(J - 1)^2$$

where $\bar{I}_1 = \operatorname{tr}(\bar{\mathbf{B}})$ is the first invariant of the isochoric left Cauchy-Green tensor $\bar{\mathbf{B}}=J^{-2/3}\mathbf{B}$, $G$ is the [shear modulus](@entry_id:167228), and $\kappa$ is the bulk modulus. Differentiating this potential yields a Cauchy stress that also naturally splits into a hydrostatic (volumetric) part and a deviatoric (isochoric) part [@problem_id:3439508]:

$$\boldsymbol{\sigma} = \kappa (J - 1) \mathbf{I} + \frac{G}{J^{5/3}} \left( \mathbf{B} - \frac{1}{3} I_1 \mathbf{I} \right)$$

For materials that are nearly **incompressible**, such as rubber, the constraint $J=1$ is enforced. This can be done approximately using a [penalty method](@entry_id:143559) with a large bulk modulus $\kappa$, or exactly using a **Lagrange multiplier**, which represents the indeterminate hydrostatic pressure $p$ [@problem_id:3439461]. For an incompressible **Mooney-Rivlin** material, with $W = C_{10}(I_1-3) + C_{01}(I_2-3)$, the Cauchy stress is derived as [@problem_id:34518]:

$$\boldsymbol{\sigma} = -p\mathbf{I} + 2(C_{10} + I_1 C_{01}) \mathbf{B} - 2C_{01}\mathbf{B}^2$$

#### The Pathology of Hypoelasticity

An alternative, older framework for [finite elasticity](@entry_id:181775) is **[hypoelasticity](@entry_id:204371)**, which postulates a linear relationship between an objective stress *rate* and the rate of deformation, $\mathbf{D}$. A common choice is the **Jaumann rate**, $\dot{\boldsymbol{\sigma}}^{\mathrm{J}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\mathbf{W} - \mathbf{W}\boldsymbol{\sigma}$, where $\mathbf{W}$ is the [spin tensor](@entry_id:187346). While objective, [hypoelastic models](@entry_id:184632) are generally not integrable to a strain-energy potential. This has a severe pathological consequence: when subjected to a finite [rigid body rotation](@entry_id:167024) ($\mathbf{D}=\mathbf{0}$), numerical integration of the hypoelastic [rate equation](@entry_id:203049) produces spurious, non-physical stresses [@problem_id:3439479]. A hyperelastic model, in contrast, correctly predicts zero stress change in the material frame. This demonstrates the critical importance and superiority of the hyperelastic framework for modeling elastic behavior.

### Plasticity: Irreversible Material Response

Plasticity describes permanent, irreversible deformation that occurs when a material is stressed beyond its [elastic limit](@entry_id:186242). The formulation of [rate-independent plasticity](@entry_id:754082) rests on three key components: a [yield criterion](@entry_id:193897), a [flow rule](@entry_id:177163), and a [hardening law](@entry_id:750150).

#### The Yield Surface and Stability

The elastic domain is defined by a **[yield function](@entry_id:167970)**, $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) \le 0$, where $\boldsymbol{\alpha}$ represents a set of [internal state variables](@entry_id:750754) (e.g., describing hardening). The boundary of this domain, $f=0$, is the **[yield surface](@entry_id:175331)**. For a material model to be physically and mathematically stable, certain conditions must be met. **Drucker's stability postulate**, which arises from thermodynamic considerations, requires that the incremental work done during a plastic cycle is non-negative. For models with an **[associative flow rule](@entry_id:163391)** (where plastic flow is normal to the yield surface), this stability requirement leads to a crucial geometric condition: the [yield surface](@entry_id:175331) must be **convex** in [stress space](@entry_id:199156) [@problem_id:3439464].

If the [yield surface](@entry_id:175331) is non-convex, the incremental boundary value problem can become ill-posed. A non-convex potential can possess multiple local minima, leading to non-unique solutions for the stress state and catastrophic failure of numerical solution algorithms [@problem_id:3439464]. Therefore, the [convexity](@entry_id:138568) of the yield surface is a cornerstone of [classical plasticity theory](@entry_id:167389).

#### The Flow Rule and Consistency Condition

The total [strain rate](@entry_id:154778) is assumed to be additively composed of an elastic part and a plastic part: $\dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^e + \dot{\boldsymbol{\varepsilon}}^p$. The **[flow rule](@entry_id:177163)** specifies the direction of plastic straining, while the **[hardening law](@entry_id:750150)** describes the evolution of the [yield surface](@entry_id:175331). For an **associative** material, the plastic strain rate is normal to the [yield surface](@entry_id:175331):

$$\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}$$

where $\dot{\lambda} \ge 0$ is the **[plastic multiplier](@entry_id:753519)**, which is non-zero only during [plastic loading](@entry_id:753518). During plastic deformation, the stress state must remain on the yield surface. This is enforced by the **Kuhn-Tucker-Karush (KKT)** loading/unloading conditions and the **consistency condition**, $\dot{f}=0$.

By combining the elastic stress-rate law, the [flow rule](@entry_id:177163), and the [consistency condition](@entry_id:198045), one can derive an explicit expression for the [plastic multiplier](@entry_id:753519) $\dot{\lambda}$. For the widely used **von Mises ($J_2$) plasticity** model with linear [isotropic hardening](@entry_id:164486) ($H$), this procedure yields [@problem_id:3439475]:

$$\dot{\lambda} = \frac{\langle \boldsymbol{N} : \dot{\boldsymbol{s}}_{\mathrm{tr}} \rangle}{3G + H}$$

where $\boldsymbol{N} = \sqrt{3/2}\boldsymbol{s}/\|\boldsymbol{s}\|$ is the flow direction, $\dot{\boldsymbol{s}}_{\mathrm{tr}} = 2G \operatorname{dev}(\dot{\boldsymbol{\varepsilon}})$ is the elastic trial [deviatoric stress](@entry_id:163323) rate, $G$ is the shear modulus, and the Macauley brackets $\langle \cdot \rangle$ indicate that [plastic flow](@entry_id:201346) occurs only when the trial stress state attempts to move outside the yield surface. This equation elegantly encapsulates the interaction between the elastic properties ($G$), the plastic properties ($H$), and the applied strain rate in determining the magnitude of the plastic response.

#### Strain Softening, Localization, and Regularization

In some materials, the [yield stress](@entry_id:274513) decreases with further plastic strain, a phenomenon known as **[strain softening](@entry_id:185019)** ($H0$). While physically observed, softening behavior poses a profound mathematical challenge. If the softening is sufficiently strong, the governing partial differential equations of the [boundary value problem](@entry_id:138753) can lose their **[strong ellipticity](@entry_id:755529)**. This mathematical event corresponds to a physical instability where deformation localizes into infinitesimally thin bands, or **[shear bands](@entry_id:183352)** [@problem_id:3439462].

The loss of [ellipticity](@entry_id:199972) occurs when the **[acoustic tensor](@entry_id:200089)**, $\mathbf{Q}(\mathbf{k})$, ceases to be positive definite for some orientation vector $\mathbf{k}$. This signals the formation of a stationary wave, or shear band, with normal $\mathbf{k}$. For a material in pure shear under [plane strain](@entry_id:167046) conditions, the critical softening modulus $h_{cr}$ at which ellipticity is lost can be explicitly calculated [@problem_id:3439462]. For a shear band oriented at $45^\circ$, this critical value is:

$$h_{cr} = -\frac{3G(\lambda+G)}{\lambda+2G}$$

Once [ellipticity](@entry_id:199972) is lost, the standard local continuum model becomes ill-posed, and numerical solutions become pathologically dependent on the [mesh discretization](@entry_id:751904). To remedy this, **regularization** techniques are employed. **Gradient plasticity** models augment the free energy or yield function with terms involving gradients of internal variables, such as the equivalent plastic strain $\kappa$. A typical term might be $\frac{1}{2}\eta \ell^2 |\nabla\kappa|^2$, where $\ell$ is an [internal material length scale](@entry_id:197915). This non-local term penalizes sharp gradients in plastic strain, restoring [ellipticity](@entry_id:199972) to the system and ensuring that [shear bands](@entry_id:183352) have a finite, physically realistic width related to $\ell$ [@problem_id:3439462]. This allows for the robust modeling of material failure and localization phenomena.

Finally, when extending plasticity to the [finite strain](@entry_id:749398) regime, the **[multiplicative decomposition](@entry_id:199514)** of the [deformation gradient](@entry_id:163749), $\mathbf{F} = \mathbf{F}_e \mathbf{F}_p$, is commonly employed. The total deformation is viewed as a plastic deformation $\mathbf{F}_p$ followed by an elastic deformation $\mathbf{F}_e$. A standard assumption, particularly for metals, is that [plastic flow](@entry_id:201346) is isochoric, i.e., $\det(\mathbf{F}_p) = 1$. This implies that all volume change is elastic, $J = \det(\mathbf{F}) = \det(\mathbf{F}_e)$ [@problem_id:3439461], neatly connecting the [finite strain plasticity](@entry_id:175182) framework back to the principles of [hyperelasticity](@entry_id:168357) developed for the elastic response.