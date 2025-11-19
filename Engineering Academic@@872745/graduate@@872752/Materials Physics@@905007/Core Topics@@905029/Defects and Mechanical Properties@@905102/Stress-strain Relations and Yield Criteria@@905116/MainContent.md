## Introduction
Understanding the relationship between applied forces and resulting deformation is the cornerstone of [mechanical design](@entry_id:187253) and materials science. While a simple tension test provides a one-dimensional glimpse into a material's response, real-world components experience complex, multi-axial states of stress. To predict material behavior—from reversible elastic stretching to permanent plastic deformation and ultimate failure—we need a rigorous mathematical framework. This article bridges the gap between empirical observation and predictive theory by developing the principles of stress-strain relations and [yield criteria](@entry_id:178101) from the ground up.

Throughout the following chapters, you will gain a comprehensive understanding of this critical subject. We will begin in **Principles and Mechanisms** by formally defining stress and strain as tensors, deriving the laws of [linear elasticity](@entry_id:166983), and establishing the criteria that govern the onset of plastic yield. Next, in **Applications and Interdisciplinary Connections**, we will explore how these fundamental models are applied across diverse fields, from analyzing pressure vessels and predicting buckling in structures to informing multiscale material design and [fracture mechanics](@entry_id:141480). Finally, the **Hands-On Practices** section will offer a chance to solidify your knowledge by working through concrete problems in [stress transformation](@entry_id:184474) and yield analysis. This structured journey will equip you with the essential tools to analyze and predict the mechanical response of solid materials.

## Principles and Mechanisms

The mechanical response of a solid material is described by the relationship between the internal forces acting within it and the deformation it undergoes. This chapter establishes the fundamental principles and mathematical frameworks used to model these relationships, focusing on the transition from reversible elastic behavior to irreversible [plastic deformation](@entry_id:139726). We will define the core measures of stress and strain, formulate the laws of elasticity, and then explore the criteria that govern the onset of plastic yield and the rules that describe subsequent [plastic flow](@entry_id:201346) and hardening.

### Fundamental Measures of Stress and Strain

To quantify the state of internal forces at a point within a continuous body, we introduce the concept of **stress**. Imagine an infinitesimal plane surface element passing through a point $\mathbf{x}$ within a body, characterized by its area $dA$ and its [unit normal vector](@entry_id:178851) $\mathbf{n}$. The material on one side of this surface exerts a force, or traction, on the material on the other side. The **[traction vector](@entry_id:189429)**, denoted $\mathbf{t}(\mathbf{n})$, is defined as this force per unit of current area.

A fundamental result of continuum mechanics, known as **Cauchy's Theorem**, states that the traction vector $\mathbf{t}$ is a linear function of the normal vector $\mathbf{n}$. This linear relationship is expressed through a second-order tensor, the **Cauchy stress tensor** $\boldsymbol{\sigma}$. The existence of this tensor can be demonstrated by considering the force balance on an infinitesimal tetrahedron. In the limit as the tetrahedron shrinks to a point, the [surface forces](@entry_id:188034) dominate the body and [inertial forces](@entry_id:169104). The equilibrium requirement then leads directly to the relationship:

$$
\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma} \mathbf{n}
$$

The Cauchy stress tensor $\boldsymbol{\sigma}(\mathbf{x}, t)$ is a field quantity that completely characterizes the state of stress at any point $\mathbf{x}$ and time $t$. Its components $\sigma_{ij}$ represent the force in the $i$-th direction acting on a plane whose normal is in the $j$-th direction. A further consequence, derived from the [balance of angular momentum](@entry_id:181848) in the absence of internal body couples, is that the Cauchy stress tensor must be symmetric, i.e., $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$ [@problem_id:2861600].

It is crucial to distinguish the Cauchy stress, often called **[true stress](@entry_id:190985)**, from the **[engineering stress](@entry_id:188465)** commonly used in uniaxial testing. Engineering stress is defined as the applied force divided by the *initial* cross-sectional area of the specimen. While convenient to measure, it is a scalar quantity, not a tensor, and it does not accurately represent the force intensity on the actual, deformed area. The Cauchy stress, which uses the *current* area, is the physically rigorous measure required for formulating general three-dimensional constitutive laws [@problem_id:2861600].

To describe deformation, we use the concept of **strain**. The deformation of a body is described by the [displacement field](@entry_id:141476) $\mathbf{u}(\mathbf{x})$, which maps each material point from its reference position to its current position. The local deformation is captured by the **[displacement gradient tensor](@entry_id:748571)**, $\nabla \mathbf{u}$. For small deformations, this tensor can be additively decomposed into its symmetric and skew-symmetric parts:

$$
\nabla\mathbf{u} = \boldsymbol{\varepsilon} + \boldsymbol{\omega}
$$

where

$$
\boldsymbol{\varepsilon} = \frac{1}{2} \left( \nabla\mathbf{u} + (\nabla\mathbf{u})^T \right)
$$

$$
\boldsymbol{\omega} = \frac{1}{2} \left( \nabla\mathbf{u} - (\nabla\mathbf{u})^T \right)
$$

The symmetric part, $\boldsymbol{\varepsilon}$, is the **[infinitesimal strain tensor](@entry_id:167211)** (or small [strain tensor](@entry_id:193332)). It measures the actual change in shape and size of a material element, such as elongation and changes in angles. The skew-symmetric part, $\boldsymbol{\omega}$, is the **[infinitesimal rotation tensor](@entry_id:192754)**, representing the local [rigid-body rotation](@entry_id:268623) of the material element without any change in shape. Since stress is generated by deformation, not by rigid motion, the [constitutive laws](@entry_id:178936) of materials relate stress to the strain tensor $\boldsymbol{\varepsilon}$, not to the full [displacement gradient](@entry_id:165352) or the [rotation tensor](@entry_id:191990) $\boldsymbol{\omega}$ [@problem_id:2861631]. The components of the strain tensor, $\varepsilon_{ij}$, have direct physical meaning. For example, the off-diagonal component $\varepsilon_{xy}$ is related to the **engineering [shear strain](@entry_id:175241)** $\gamma_{xy}$, which measures the change in angle between two initially orthogonal lines. The precise relationship is $\gamma_{xy} = 2\varepsilon_{xy}$ [@problem_id:2861631].

### Linear Elastic Constitutive Behavior

For many materials subjected to small strains, the relationship between [stress and strain](@entry_id:137374) is linear and reversible. This is the domain of elasticity. For a **linearly elastic and isotropic** material, the most general relationship between the symmetric [stress and strain](@entry_id:137374) tensors is given by **Hooke's Law**:

$$
\boldsymbol{\sigma} = \lambda \, \mathrm{tr}(\boldsymbol{\varepsilon})\mathbf{I} + 2\mu\boldsymbol{\varepsilon}
$$

Here, $\mathbf{I}$ is the second-order identity tensor, $\mathrm{tr}(\boldsymbol{\varepsilon})$ is the trace of the [strain tensor](@entry_id:193332) (representing the [volumetric strain](@entry_id:267252)), and $\lambda$ and $\mu$ are the two [independent elastic constants](@entry_id:203649) known as the **Lamé parameters**. The parameter $\mu$ is also known as the **[shear modulus](@entry_id:167228)**, often denoted by $G$.

It is often illuminating to decompose the [stress and strain](@entry_id:137374) tensors into their **spherical** (or volumetric) and **deviatoric** (or distortional) parts. The spherical part represents a state of uniform hydrostatic pressure, while the deviatoric part represents [shear deformation](@entry_id:170920).
The mean stress is $\sigma_m = \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})$, and the [volumetric strain](@entry_id:267252) is $\varepsilon_v = \mathrm{tr}(\boldsymbol{\varepsilon})$. The tensors are decomposed as:

$$
\boldsymbol{\sigma} = \boldsymbol{s} + \sigma_m \mathbf{I}
$$

$$
\boldsymbol{\varepsilon} = \boldsymbol{e} + \frac{1}{3}\varepsilon_v \mathbf{I}
$$

where $\boldsymbol{s}$ and $\boldsymbol{e}$ are the [deviatoric stress](@entry_id:163323) and strain tensors, respectively, both of which are traceless. With this decomposition, Hooke's Law decouples into two independent relations [@problem_id:2861604]:

$$
\sigma_m = K \varepsilon_v \quad \text{and} \quad \boldsymbol{s} = 2G \boldsymbol{e}
$$

Here, $K = \lambda + \frac{2}{3}\mu$ is the **bulk modulus**, which governs the material's resistance to volume change, and $G=\mu$ is the shear modulus, governing its resistance to shape change. These theoretically derived constants can be related to the more familiar [engineering elastic constants](@entry_id:182223): **Young's modulus** ($E$) and **Poisson's ratio** ($\nu$). By considering a simple [uniaxial tension test](@entry_id:195375), one can derive the following essential relationships [@problem_id:2861630]:

$$
\mu = G = \frac{E}{2(1+\nu)}, \quad K = \frac{E}{3(1-2\nu)}, \quad \lambda = \frac{E\nu}{(1+\nu)(1-2\nu)}
$$

These equations form a self-consistent set that fully characterizes the behavior of an isotropic, linearly elastic material.

### The Yield Criterion: Boundary of Elasticity

When the load on a material exceeds a certain limit, it may undergo permanent, irreversible deformation known as [plastic flow](@entry_id:201346). The boundary in [stress space](@entry_id:199156) that separates the purely elastic domain from the elastoplastic domain is called the **[yield surface](@entry_id:175331)**. This boundary is mathematically described by a **yield function**, $f(\boldsymbol{\sigma}, \boldsymbol{q}) \le 0$, where $\boldsymbol{q}$ represents a set of internal variables that describe the history of [plastic deformation](@entry_id:139726). The purely elastic states are those for which $f \lt 0$, while the onset of plasticity, or yielding, occurs when the stress state reaches the [yield surface](@entry_id:175331), i.e., $f = 0$ [@problem_id:2861618].

#### Anisotropic Yielding in Single Crystals

At the microscopic level, plastic deformation in crystalline materials occurs through the motion of dislocations on specific [crystallographic planes](@entry_id:160667) and in specific directions. A **[slip system](@entry_id:155264)** is defined by the pair of a slip plane [normal vector](@entry_id:264185) $\mathbf{n}^{\alpha}$ and a slip direction vector $\mathbf{m}^{\alpha}$. The driving force for slip is not the full stress tensor, but the component of the traction on the [slip plane](@entry_id:275308) that is resolved along the slip direction. This is the **[resolved shear stress](@entry_id:201022) (RSS)**, $\tau^{\alpha}$, given by:

$$
\tau^{\alpha} = \mathbf{m}^{\alpha} \cdot \boldsymbol{\sigma} \cdot \mathbf{n}^{\alpha}
$$

**Schmid's Law** is the simplest yield criterion for single crystals. It postulates that slip is initiated on a given system $\alpha$ when the magnitude of the [resolved shear stress](@entry_id:201022) reaches a critical material-specific value, the **[critical resolved shear stress](@entry_id:159240) (CRSS)**, $\tau_c$. Macroscopic yielding of the crystal occurs when $\max_{\alpha}|\tau^{\alpha}| = \tau_c$ [@problem_id:2861593]. For a uniaxial tensile stress $\sigma$ applied along a direction $\mathbf{l}$, the RSS is $\tau^{\alpha} = \sigma (\mathbf{l} \cdot \mathbf{m}^{\alpha}) (\mathbf{l} \cdot \mathbf{n}^{\alpha})$. The term $s^{\alpha} = (\mathbf{l} \cdot \mathbf{m}^{\alpha}) (\mathbf{l} \cdot \mathbf{n}^{\alpha})$ is the **Schmid factor**. The macroscopic yield stress is then $\sigma_y = \tau_c / s_{\max}$, where $s_{\max}$ is the maximum Schmid factor over all possible [slip systems](@entry_id:136401). Because $s_{\max}$ depends on the loading orientation $\mathbf{l}$, the [yield strength](@entry_id:162154) of a single crystal is inherently **anisotropic**. For instance, an FCC single crystal loaded along the $[111]$ direction is significantly stronger than when loaded along the $[001]$ or $[011]$ directions, because the former orientation results in a lower maximum Schmid factor [@problem_id:2861593].

#### Macroscopic Yield Criteria for Isotropic Materials

While single crystals are anisotropic, most engineering materials are polycrystalline aggregates with randomly oriented grains. At the macroscopic scale, their behavior can often be approximated as isotropic. The two most common [yield criteria](@entry_id:178101) for isotropic, ductile metals are the Tresca and von Mises criteria. A key experimental observation for these materials is that yielding is largely independent of [hydrostatic pressure](@entry_id:141627).

The **Tresca criterion**, or maximum shear stress criterion, postulates that yielding occurs when the maximum shear stress in the material reaches a critical value, $k$. By considering a [uniaxial tension test](@entry_id:195375), where the principal stresses at yield are $(\sigma_y, 0, 0)$, the maximum shear stress is found to be $\tau_{\max} = \frac{1}{2}(\sigma_y - 0) = \sigma_y/2$. Thus, the critical shear stress is $k = \sigma_y/2$. The Tresca [yield criterion](@entry_id:193897) is therefore:

$$
\tau_{\max} = \frac{1}{2} \max|\sigma_i - \sigma_j| = \frac{\sigma_y}{2} \quad \text{or equivalently} \quad \max|\sigma_i - \sigma_j| = \sigma_y
$$

where $\sigma_i$ are the principal stresses. In the three-dimensional [principal stress space](@entry_id:184388) $(\sigma_1, \sigma_2, \sigma_3)$, this equation describes a right hexagonal prism whose axis is the hydrostatic line $\sigma_1=\sigma_2=\sigma_3$ [@problem_id:2861615].

The **von Mises criterion**, also known as the maximum distortional [energy criterion](@entry_id:748980), provides an alternative model. It postulates that yielding begins when the distortional (or shear) part of the [elastic strain energy](@entry_id:202243) density reaches a critical value, which can be calibrated from a [uniaxial tension test](@entry_id:195375). This physical argument leads to a condition on the second invariant of the [deviatoric stress tensor](@entry_id:267642), $J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s}$. The criterion is given by:

$$
\sqrt{3J_2} = \sigma_y
$$

The quantity $\sigma_{\text{eq}} = \sqrt{3J_2} = \sqrt{\frac{1}{2}[(\sigma_1-\sigma_2)^2 + (\sigma_2-\sigma_3)^2 + (\sigma_3-\sigma_1)^2]}$ is the **von Mises [equivalent stress](@entry_id:749064)**. Since this criterion depends only on the deviatoric stress, it is inherently independent of hydrostatic pressure [@problem_id:2861604]. In [principal stress space](@entry_id:184388), the von Mises criterion describes a right circular cylinder, also aligned with the hydrostatic axis.

A comparison of the two criteria shows that in the deviatoric plane (a plane perpendicular to the hydrostatic axis), the Tresca hexagon is inscribed within the von Mises circle. This means the two criteria agree for uniaxial and equibiaxial stress states, but for other states, particularly pure shear, Tresca is more conservative. For a pure shear state, Tresca predicts yielding at $\tau = \sigma_y/2$, while von Mises predicts it at $\tau = \sigma_y/\sqrt{3} \approx 0.577\sigma_y$ [@problem_id:2861615].

### Modeling Plastic Flow and Hardening

Once the stress state reaches the [yield surface](@entry_id:175331), a **[flow rule](@entry_id:177163)** is needed to determine the direction of the plastic strain increment, and a **hardening rule** is required to describe the evolution of the [yield surface](@entry_id:175331) itself.

#### The Direction of Plastic Flow: Associated and Non-Associated Rules

The general form of a [plastic flow rule](@entry_id:189597) for [rate-independent plasticity](@entry_id:754082) connects the rate of plastic strain, $\dot{\boldsymbol{\varepsilon}}^p$, to the current stress state via a **plastic [potential function](@entry_id:268662)**, $g(\boldsymbol{\sigma}, \boldsymbol{q})$:

$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$

Here, $\dot{\lambda}$ is the non-negative **[plastic multiplier](@entry_id:753519) rate**, which governs the magnitude of the plastic flow. The gradient $\partial g / \partial \boldsymbol{\sigma}$ dictates the direction of the plastic strain rate vector in stress space.

If the plastic potential function is chosen to be the same as the [yield function](@entry_id:167970) ($g=f$), the [flow rule](@entry_id:177163) is called an **[associated flow rule](@entry_id:201731)**. In this case, the plastic [strain rate](@entry_id:154778) is normal to the yield surface. If $g \neq f$, the [flow rule](@entry_id:177163) is **non-associated**, and the flow direction is normal to the [level surfaces](@entry_id:196027) of the [plastic potential](@entry_id:164680) $g$ [@problem_id:2861591].

Associated flow is a common assumption for metals, but [non-associated flow](@entry_id:202786) is crucial for modeling certain materials, such as soils, rocks, and concrete. For example, [pressure-sensitive materials](@entry_id:753710) often exhibit **[plastic dilatancy](@entry_id:188905)**, meaning they expand in volume when sheared plastically. A [non-associated flow rule](@entry_id:172454) with a suitable potential, such as a Drucker-Prager potential of the form $g = q + \beta p - c(\kappa)$, can capture this phenomenon. The parameter $\beta$ directly controls the ratio of plastic [volumetric strain rate](@entry_id:272471) to equivalent plastic [shear strain rate](@entry_id:189459), $\dot{\varepsilon}_{v}^{p}/\dot{\varepsilon}_{\text{eq}}^{p} = \beta$ [@problem_id:2861591].

#### The Framework of Rate-Independent Plasticity

The complete constitutive framework for rate-independent [elastoplasticity](@entry_id:193198) is elegantly summarized by the **Kuhn-Tucker-Karush complementarity conditions** and the **consistency condition**. For a given state, the following conditions must hold [@problem_id:2861618]:

1.  **Admissibility:** $f(\boldsymbol{\sigma}, \boldsymbol{q}) \le 0$. The stress state must lie within or on the yield surface.
2.  **Non-negative plastic flow:** $\dot{\lambda} \ge 0$. Plastic deformation is an irreversible process.
3.  **Complementarity:** $\dot{\lambda} f(\boldsymbol{\sigma}, \boldsymbol{q}) = 0$. This ensures that [plastic flow](@entry_id:201346) ($\dot{\lambda} > 0$) can only occur when the stress state is on the yield surface ($f=0$).
4.  **Consistency:** During [plastic loading](@entry_id:753518), the state must remain on the evolving yield surface. This requires that the rate of change of the yield function is zero, i.e., $\dot{f}=0$ whenever $\dot{\lambda} > 0$. This condition is used to determine the value of the [plastic multiplier](@entry_id:753519) $\dot{\lambda}$.

#### Evolution of the Yield Surface: Hardening Models

As a material deforms plastically, its resistance to further yielding often changes. This phenomenon is known as **hardening** (or softening) and is modeled by the evolution of the yield surface. The most common models are based on two internal variables: a scalar $\kappa$ (often related to accumulated plastic strain) and a second-order tensor $\boldsymbol{\alpha}$ (the backstress).

**Isotropic hardening** describes a uniform expansion of the [yield surface](@entry_id:175331), representing an increase in the [yield stress](@entry_id:274513) in all directions. The center of the yield surface remains fixed in stress space. This is modeled by letting the yield stress $\sigma_y$ be a function of $\kappa$, e.g., $f = \Phi(\boldsymbol{s}) - \sigma_y(\kappa)$.

**Kinematic hardening** describes a translation of the yield surface in [stress space](@entry_id:199156), without any change in its size or shape. This is useful for modeling the **Bauschinger effect**, where the [yield stress](@entry_id:274513) in the reverse direction of loading decreases after initial [plastic deformation](@entry_id:139726). This is modeled by introducing a **backstress tensor** $\boldsymbol{\alpha}$, which represents the center of the [yield surface](@entry_id:175331): $f = \Phi(\boldsymbol{s}-\boldsymbol{\alpha}) - \sigma_{y0}$. To preserve pressure-insensitivity for von Mises or Tresca models, the [backstress](@entry_id:198105) $\boldsymbol{\alpha}$ must be deviatoric ($\mathrm{tr}(\boldsymbol{\alpha})=0$) [@problem_id:2861616].

**Mixed hardening** (or [combined hardening](@entry_id:186067)) is a superposition of both effects, where the [yield surface](@entry_id:175331) both expands and translates. The yield function takes the general form $f = \Phi(\boldsymbol{s}-\boldsymbol{\alpha}) - \sigma_y(\kappa)$, providing a more realistic description of cyclic plastic behavior [@problem_id:2861616].

### Principles of Stability in Plasticity

The [constitutive models](@entry_id:174726) for plasticity must not only match experimental data but also adhere to fundamental principles of stability to ensure that they are physically realistic and lead to well-posed mathematical problems.

A cornerstone of [stability theory](@entry_id:149957) is **Drucker's Stability Postulate**. In its simplest rate form, it states that for any infinitesimal process of [plastic loading](@entry_id:753518), the work done by the increment of stress on the resulting plastic strain increment must be non-negative: $\dot{\boldsymbol{\sigma}} : \dot{\boldsymbol{\varepsilon}}^p \ge 0$. This postulate has profound implications: for materials with a smooth [yield surface](@entry_id:175331), it implies that the [yield surface](@entry_id:175331) must be convex and that the [flow rule](@entry_id:177163) must be associated (normality) [@problem_id:2861602]. It provides a strong thermodynamic justification for the common assumption of associated plasticity, as it can be shown to be equivalent to the principle of maximum [plastic dissipation](@entry_id:201273) [@problem_id:2861591].

It is important to note that Drucker's postulate is a stronger condition than the basic requirement of non-negative dissipation from the [second law of thermodynamics](@entry_id:142732), $\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p \ge 0$. A material can be dissipative but still unstable.

Another critical concept is that of uniqueness and incremental stability of a solution to a boundary-value problem. **Hill's Criterion** provides a condition for uniqueness. It states that the incremental solution is unique if the second-order work is strictly positive for any two distinct, kinematically admissible incremental fields. This is linked to the properties of the **[elastoplastic tangent modulus](@entry_id:189492)**, $\mathbb{C}_{ep}$, which relates the total stress rate to the total strain rate ($\dot{\boldsymbol{\sigma}} = \mathbb{C}_{ep} : \dot{\boldsymbol{\varepsilon}}$). Uniqueness and stability are generally guaranteed if the symmetric part of $\mathbb{C}_{ep}$ is [positive definite](@entry_id:149459). Loss of this property, which can occur during [strain softening](@entry_id:185019), can lead to non-uniqueness of the solution and the formation of instabilities such as [shear bands](@entry_id:183352) or localization of deformation [@problem_id:2861602].