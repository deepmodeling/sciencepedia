## Introduction
Rate-independent plasticity is a cornerstone of modern [solid mechanics](@entry_id:164042), providing a powerful theoretical framework for describing the permanent, irreversible deformation of materials subjected to loading beyond their [elastic limit](@entry_id:186242). Its significance is particularly profound in [computational geomechanics](@entry_id:747617), where it is indispensable for modeling the complex behavior of soils, rocks, and other [granular media](@entry_id:750006). However, bridging the gap from fundamental principles to practical application can be challenging, as it requires a deep understanding of thermodynamics, advanced mathematics, and computational methods. This article addresses this challenge by providing a systematic journey through the world of [rate-independent plasticity](@entry_id:754082).

This article will guide you through the essential aspects of the theory in three comprehensive chapters. First, in "Principles and Mechanisms," we will deconstruct the theory into its fundamental components, starting from its thermodynamic roots and building up to the key constitutive postulates and the mathematical framework required for both small and large deformations. Next, "Applications and Interdisciplinary Connections" will showcase the theory's versatility by exploring its use in classic and advanced geomaterial models, its crucial role in coupled problems like [poromechanics](@entry_id:175398), and its algorithmic implementation in computational mechanics. Finally, "Hands-On Practices" will offer a chance to solidify this knowledge through targeted problems that bridge theory with practical implementation.

## Principles and Mechanisms

This chapter delves into the core principles and governing mechanisms of [rate-independent plasticity](@entry_id:754082) theory. Building upon the introduction, we will systematically construct the theoretical edifice of plasticity, starting from its thermodynamic roots and progressing to the specific constitutive postulates that enable the modeling of complex inelastic behavior in [geomaterials](@entry_id:749838). We will explore the mathematical framework that ensures [consistency and stability](@entry_id:636744), and conclude by extending the theory from the domain of infinitesimal deformations to the more general and challenging realm of finite strains.

### Thermodynamic Foundations and the Principle of Rate-Independence

The theory of plasticity is not an ad-hoc collection of rules but is rigorously grounded in the principles of thermodynamics. For an [isothermal process](@entry_id:143096), the second law of thermodynamics, expressed by the Clausius-Duhem inequality, mandates that the [mechanical dissipation](@entry_id:169843) per unit volume, $\mathcal{D}$, must be non-negative. This dissipation represents the energy converted into heat or consumed by microstructural rearrangement during inelastic deformation.

Let us consider a small-strain formulation where the total strain tensor $\boldsymbol{\varepsilon}$ is additively decomposed into an elastic part $\boldsymbol{\varepsilon}^e$ and a plastic part $\boldsymbol{\varepsilon}^p$. The state of the material is described by the elastic strain and a set of internal variables, denoted collectively by $\boldsymbol{\alpha}$, which capture the history of plastic deformation (e.g., hardening). The Helmholtz free energy per unit volume, $\psi$, is a function of this state, i.e., $\psi = \psi(\boldsymbol{\varepsilon}^e, \boldsymbol{\alpha})$. The Cauchy stress $\boldsymbol{\sigma}$ and the thermodynamic forces $\mathbf{A}$ conjugate to the internal variables are derived from the free energy:

$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^e}, \quad \mathbf{A} = -\frac{\partial \psi}{\partial \boldsymbol{\alpha}}
$$

The Clausius-Duhem inequality for an [isothermal process](@entry_id:143096) is $\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0$. By applying the chain rule to $\dot{\psi}$ and using the additive [strain decomposition](@entry_id:186005), this inequality reduces to a remarkably clear statement about the source of dissipation :

$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p + \mathbf{A} \cdot \dot{\boldsymbol{\alpha}} \ge 0
$$

This fundamental result reveals that dissipation arises solely from the inelastic processes: the rate of plastic work, $\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p$, and the work done by the thermodynamic forces over the rates of the internal variables, $\mathbf{A} \cdot \dot{\boldsymbol{\alpha}}$. The elastic response, by definition, is non-dissipative.

The "rate-independent" nature of the theory can be given a precise mathematical meaning within this thermodynamic framework. The evolution of the inelastic rates, which we can collect into a single vector $\dot{\boldsymbol{\gamma}} = (\dot{\boldsymbol{\varepsilon}}^p, \dot{\boldsymbol{\alpha}})$, is governed by a **dissipation potential**, $\mathcal{R}(\dot{\boldsymbol{\gamma}})$. Rate-independence is characterized by the requirement that this potential be a **positively homogeneous function of degree one**:

$$
\mathcal{R}(\lambda \dot{\boldsymbol{\gamma}}) = \lambda \mathcal{R}(\dot{\boldsymbol{\gamma}}) \quad \text{for any scalar } \lambda > 0
$$

The [constitutive law](@entry_id:167255) relating the generalized rates $\dot{\boldsymbol{\gamma}}$ to the generalized stresses $\mathbf{X} = (\boldsymbol{\sigma}, \mathbf{A})$ is derived from this potential. Due to the 1-homogeneity of $\mathcal{R}$, the resulting generalized stresses $\mathbf{X}$ are homogeneous of degree zero in the rates. This means that the stresses depend only on the *direction* of [plastic flow](@entry_id:201346), not its speed or magnitude. Doubling the rate of straining does not change the stress required to sustain the flow. This invariance to [time-scaling](@entry_id:190118) is the very essence of [rate-independent plasticity](@entry_id:754082) .

### The Three Pillars of Elasto-Plasticity

Any complete model of [rate-independent plasticity](@entry_id:754082) is built upon three fundamental constitutive components: a [yield criterion](@entry_id:193897), a [flow rule](@entry_id:177163), and a [hardening law](@entry_id:750150).

#### The Yield Criterion: Defining the Elastic Domain

The **[yield criterion](@entry_id:193897)** delineates the boundary between purely elastic behavior and the onset of [plastic deformation](@entry_id:139726). It is defined by a scalar-valued **yield function**, $f(\boldsymbol{\sigma}, \boldsymbol{\alpha})$, which depends on the current stress state $\boldsymbol{\sigma}$ and the internal variables $\boldsymbol{\alpha}$. The set of all stress states for which the material behaves elastically, known as the **elastic domain**, is defined by the inequality :

$$
\mathcal{K}(\boldsymbol{\alpha}) = \{ \boldsymbol{\sigma} \mid f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) \le 0 \}
$$

The boundary of this domain, $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = 0$, is the **yield surface**. Stress states for which $f > 0$ are considered plastically inadmissible and cannot be reached.

For an isotropic material, the [principle of material objectivity](@entry_id:191727) requires that the [yield function](@entry_id:167970) depend only on the invariants of the stress tensor. For [geomaterials](@entry_id:749838), whose behavior is strongly dependent on confining pressure and shear stress, it is conventional and physically insightful to use a specific set of invariants: the [mean stress](@entry_id:751819) $p$, a measure of deviatoric stress $q$, and the Lode angle $\theta$ . These are defined as:

*   **Mean Stress:** $p = \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma}) = \frac{1}{3}I_1$, where $I_1$ is the first invariant of $\boldsymbol{\sigma}$. This invariant captures the hydrostatic or volumetric component of stress.
*   **Deviatoric Stress Invariant:** $q = \sqrt{3J_2}$, where $J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s}$ is the second invariant of the [deviatoric stress tensor](@entry_id:267642) $\boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I}$. This [invariant measures](@entry_id:202044) the magnitude of the shear stresses.
*   **Lode Angle:** $\theta = \frac{1}{3} \arccos \left( \frac{3\sqrt{3}}{2} \frac{J_3}{J_2^{3/2}} \right)$, where $J_3 = \det(\boldsymbol{s})$ is the third invariant of the deviatoric stress. The Lode angle characterizes the influence of the intermediate [principal stress](@entry_id:204375) and describes the "shape" of the stress state on the deviatoric plane.

The strength of [geomaterials](@entry_id:749838) is highly sensitive to pressure due to inter-particle friction and mechanisms like grain crushing. Furthermore, experiments show that strength often depends on the value of the intermediate [principal stress](@entry_id:204375). Therefore, a realistic [yield function](@entry_id:167970) for soils or rocks must be expressed as $f(p, q, \theta, \boldsymbol{\alpha})$ .

Yield surfaces can be either smooth or non-smooth. **Smooth surfaces**, like the Drucker-Prager criterion, are continuously differentiable. **Non-smooth surfaces**, like the Mohr-Coulomb or Tresca criteria, feature "corners" and "edges" where the gradient is not uniquely defined. These non-smooth models are often more accurate in capturing the behavior of frictional materials but require a more sophisticated mathematical treatment, as we will see later .

#### The Flow Rule: Governing Plastic Deformation

When the stress state lies on the yield surface and loading continues, plastic strain develops. The **[flow rule](@entry_id:177163)** is the [constitutive equation](@entry_id:267976) that specifies the direction and evolution of the plastic strain rate, $\dot{\boldsymbol{\varepsilon}}^p$. The direction of plastic straining is assumed to be normal to the [level surfaces](@entry_id:196027) of a second function, the **[plastic potential](@entry_id:164680)** $g(\boldsymbol{\sigma})$. This is expressed as:

$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$

where $\dot{\lambda} \ge 0$ is the [plastic multiplier](@entry_id:753519) rate, which determines the magnitude of the plastic strain increment. Two cases are distinguished :

1.  **Associated Flow:** If the [plastic potential](@entry_id:164680) is chosen to be the same as the [yield function](@entry_id:167970) ($g = f$), the flow is termed **associated**. In this case, the plastic [strain rate](@entry_id:154778) vector is normal to the [yield surface](@entry_id:175331) itself. This is a common assumption for metals and is motivated by Drucker's stability postulate.

2.  **Non-Associated Flow:** If the [plastic potential](@entry_id:164680) differs from the yield function ($g \neq f$), the flow is **non-associated**. The plastic strain rate vector is normal to the [level surfaces](@entry_id:196027) of $g$, not $f$.

For [geomaterials](@entry_id:749838), [non-associated flow](@entry_id:202786) is not an exception but the rule. Experiments on soils consistently show that using an [associated flow rule](@entry_id:201731) for a pressure-sensitive yield criterion (like Drucker-Prager or Mohr-Coulomb) grossly over-predicts the amount of volume increase (dilatancy) during shear. A more realistic model is achieved by defining a [plastic potential](@entry_id:164680) $g$ that is distinct from the yield function $f$. The pressure-dependence of $f$ is related to the material's **[angle of internal friction](@entry_id:197521)**, $\phi$, while the pressure-dependence of $g$ defines the **angle of [dilatancy](@entry_id:201001)**, $\psi$. For most soils, it is observed that $\psi  \phi$. The sign of $\psi$ controls whether the material compacts ($\psi  0$) or dilates ($\psi  0$) during plastic shearing .

#### The Hardening Law: Evolution of the Yield Surface

The **[hardening law](@entry_id:750150)** describes how the [yield surface](@entry_id:175331) evolves as [plastic deformation](@entry_id:139726) accumulates. This evolution is captured by the internal variables $\boldsymbol{\alpha}$. The two classical forms of hardening are :

1.  **Isotropic Hardening:** This mechanism describes a uniform expansion or contraction of the yield surface, without changing its shape or center. It is typically governed by a scalar internal variable, $\kappa$, often taken as a measure of accumulated [plastic work](@entry_id:193085) or accumulated plastic strain, e.g., $\dot{\kappa} = \sqrt{\frac{2}{3} \dot{\boldsymbol{\varepsilon}}^p_{dev}:\dot{\boldsymbol{\varepsilon}}^p_{dev}}$. The [yield function](@entry_id:167970) takes a form like $f(\boldsymbol{\sigma}) - k(\kappa) \le 0$, where an increase in the hardening variable $\kappa$ leads to an increase in the [yield strength](@entry_id:162154) $k$.

2.  **Kinematic Hardening:** This mechanism describes a translation of the [yield surface](@entry_id:175331) in stress space, without changing its size or shape. This is essential for modeling phenomena like the Bauschinger effect in cyclic loading. It is governed by a tensorial internal variable called the **backstress**, $\boldsymbol{X}$. In deviatoric plasticity, $\boldsymbol{X}$ must be a [deviatoric tensor](@entry_id:185837). The hardening is implemented by replacing the deviatoric stress $\boldsymbol{s}$ with an "effective" [deviatoric stress](@entry_id:163323), $\boldsymbol{s}-\boldsymbol{X}$, in the yield function, for example: $f(\boldsymbol{s}-\boldsymbol{X}, \dots) \le 0$. The evolution law for $\dot{\boldsymbol{X}}$ is a [constitutive equation](@entry_id:267976) that must itself be thermodynamically consistent.

Many advanced models for [geomaterials](@entry_id:749838) combine both [isotropic and kinematic hardening](@entry_id:195752) to capture complex loading-history effects.

### The Mathematical Framework: Consistency and Stability

The three pillars of plasticity are bound together by a rigorous mathematical framework that ensures the model is predictive and physically consistent.

#### Loading-Unloading Conditions and Consistency

The transition between elastic and plastic behavior is governed by a set of rules known as the **Karush-Kuhn-Tucker (KKT) conditions**. These are a cornerstone of [rate-independent plasticity](@entry_id:754082) and its numerical implementation . For a [plastic multiplier](@entry_id:753519) rate $\dot{\lambda}$, they are:

1.  **Admissibility:** $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) \le 0$
2.  **Non-negative Dissipation:** $\dot{\lambda} \ge 0$
3.  **Complementarity (or Switching) Condition:** $\dot{\lambda} f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = 0$

The [complementarity condition](@entry_id:747558) elegantly states that either the stress state is strictly inside the elastic domain ($f  0$) and there is no [plastic flow](@entry_id:201346) ($\dot{\lambda} = 0$), or there is [plastic flow](@entry_id:201346) ($\dot{\lambda}  0$) and the stress state must be exactly on the yield surface ($f=0$).

When plastic flow occurs, the stress state must remain on the evolving [yield surface](@entry_id:175331). This imposes an additional constraint known as the **[consistency condition](@entry_id:198045)** :

$$
\dot{f}(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = 0 \quad \text{during plastic loading}
$$

Expanding this with the [chain rule](@entry_id:147422), $\dot{f} = \frac{\partial f}{\partial\boldsymbol{\sigma}}:\dot{\boldsymbol{\sigma}} + \frac{\partial f}{\partial\boldsymbol{\alpha}}\cdot\dot{\boldsymbol{\alpha}} = 0$, provides the crucial equation used to determine the unknown [plastic multiplier](@entry_id:753519) rate $\dot{\lambda}$.

In computational practice, these conditions form the basis of the **elastic-predictor, plastic-corrector** algorithm. For a given strain increment, a trial stress is computed assuming purely elastic behavior. If this trial stress lies outside the current [yield surface](@entry_id:175331) ($f^{trial}  0$), it means [plastic loading](@entry_id:753518) must occur. The [consistency condition](@entry_id:198045) is then invoked to solve for the amount of plastic strain needed to "return" the stress state back to the yield surface .

#### Material Stability: Drucker's Postulate

For a material model to be physically realistic, it must be stable. A key stability criterion in plasticity is **Drucker's postulate**. In its simplest form, it states that for any cycle of stress that begins and ends in a given state $\boldsymbol{\sigma}_0$, the net plastic work done must be non-negative. A more local and powerful statement follows from this: the incremental [plastic work](@entry_id:193085) must be non-negative.

This concept finds its most elegant and general expression in the language of convex analysis . If the elastic domain $\mathcal{K}$ is a [convex set](@entry_id:268368) and the flow is associative, then the [flow rule](@entry_id:177163) mapping (from stress to plastic [strain rate](@entry_id:154778)) is a **[monotone operator](@entry_id:635253)**. This means that for any two admissible stress states $\boldsymbol{\sigma}_a$ and $\boldsymbol{\sigma}_b$ and their corresponding plastic strain rates $\dot{\boldsymbol{\varepsilon}}^p_a$ and $\dot{\boldsymbol{\varepsilon}}^p_b$, the following inequality holds:

$$
\langle \boldsymbol{\sigma}_a - \boldsymbol{\sigma}_b, \dot{\boldsymbol{\varepsilon}}^p_a - \dot{\boldsymbol{\varepsilon}}^p_b \rangle \ge 0
$$

where $\langle \cdot, \cdot \rangle$ denotes the inner product (work-conjugacy pairing). In the differential limit, this implies $\langle \delta\boldsymbol{\sigma}, \delta\boldsymbol{\varepsilon}^p \rangle \ge 0$. This non-negativity of [second-order plastic work](@entry_id:754602) guarantees [material stability](@entry_id:183933). Thus, the convexity of the yield surface in associative plasticity is not merely a convenient assumption, but a direct guarantor of [material stability](@entry_id:183933).

#### A Deeper Look at Non-Smooth Yield Surfaces

As mentioned, many realistic [yield criteria](@entry_id:178101) for [geomaterials](@entry_id:749838), such as Mohr-Coulomb, are non-smooth. At an "edge" or "corner" of the [yield surface](@entry_id:175331), the gradient is not uniquely defined. Convex analysis provides the tools to generalize the [flow rule](@entry_id:177163) to these points .

The gradient is replaced by the **subdifferential**, $\partial f(\boldsymbol{\sigma})$. At a point $\boldsymbol{\sigma}$ where $f$ is smooth, $\partial f(\boldsymbol{\sigma})$ is a singleton set containing just the gradient, $\{\nabla f(\boldsymbol{\sigma})\}$. At a non-smooth point, $\partial f(\boldsymbol{\sigma})$ is a closed, [convex set](@entry_id:268368) containing all the "limiting gradients" from nearby smooth points .

The [flow rule](@entry_id:177163), which states that the plastic strain rate must be normal to the elastic domain, is generalized using the concept of the **[normal cone](@entry_id:272387)**, $N_\mathcal{K}(\boldsymbol{\sigma})$. The [normal cone](@entry_id:272387) at a point $\boldsymbol{\sigma}$ on the boundary of a convex set $\mathcal{K}$ is the set of all outward-pointing vectors that form an angle of $90^{\circ}$ or more with any vector pointing from $\boldsymbol{\sigma}$ into $\mathcal{K}$.

A crucial theorem connects these concepts: the [normal cone](@entry_id:272387) to the elastic domain is the cone generated by the subdifferential of the [yield function](@entry_id:167970) :

$$
N_\mathcal{K}(\boldsymbol{\sigma}) = \{ \lambda \boldsymbol{\xi} \mid \boldsymbol{\xi} \in \partial f(\boldsymbol{\sigma}), \lambda \ge 0 \}
$$

The [associative flow rule](@entry_id:163391) is then generalized to the set-valued inclusion:

$$
\dot{\boldsymbol{\varepsilon}}^p \in N_\mathcal{K}(\boldsymbol{\sigma})
$$

This means that at a corner, where the [subdifferential](@entry_id:175641) contains multiple vectors, the plastic strain rate is no longer restricted to a single direction but can lie anywhere within the cone generated by these vectors. This provides a determinate, albeit multi-valued, [flow rule](@entry_id:177163) even at non-smooth points on the [yield surface](@entry_id:175331).

### Kinematics: From Small to Large Deformations

The formulation of [plasticity theory](@entry_id:177023) depends critically on the kinematic assumptions regarding the magnitude of strains and rotations.

#### The Small-Strain Framework

For many engineering problems, deformations are small enough to justify the framework of [infinitesimal strain](@entry_id:197162) theory. Here, the key kinematic assumption is the **additive decomposition of the total strain tensor** :

$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p
$$

This linear superposition is computationally convenient and physically accurate under the restrictive conditions of both small strains and small rotations. For many serviceability analyses in geomechanics, such as predicting the settlement of a foundation under working loads, this framework is sufficient.

#### The Finite-Strain Framework and Objectivity

When a material undergoes [large deformations](@entry_id:167243) or, critically, large rigid-body rotations, the additive [strain decomposition](@entry_id:186005) is no longer valid or objective. A more general theory is required, founded on the **[multiplicative decomposition](@entry_id:199514) of the [deformation gradient](@entry_id:163749)**, $F$ . This decomposition, proposed by Lee, postulates the existence of a conceptual, stress-free **intermediate configuration**:

$$
F = F^e F^p
$$

Here, $F^p$ represents the irreversible [plastic deformation](@entry_id:139726) mapping the reference configuration to the unstressed intermediate configuration, while $F^e$ is the subsequent [elastic deformation](@entry_id:161971) that brings the body to its final, stressed configuration.

The primary motivation for this multiplicative structure is the principle of **[material frame indifference](@entry_id:166014) (objectivity)**, which demands that [constitutive laws](@entry_id:178936) be independent of the observer's [rigid-body motion](@entry_id:265795) . The [multiplicative decomposition](@entry_id:199514) naturally satisfies this principle. Under a superimposed rotation $Q$, the elastic part transforms as $F^e \to Q F^e$, while the plastic part $F^p$, representing intrinsic material change, is assumed to be unaffected. This ensures that the stress response, which depends on the elastic deformation, rotates correctly with the body.

For [geomaterials](@entry_id:749838), this framework must accommodate plastic volume changes. Unlike in [metal plasticity](@entry_id:176585) where [plastic flow](@entry_id:201346) is often assumed to be isochoric ($\det(F^p) = 1$), soils can undergo significant plastic compaction or dilation. A finite-strain model for [geomaterials](@entry_id:749838) must therefore allow for $\det(F^p) \ne 1$. This framework is essential for problems involving large geometric changes, such as [slope stability](@entry_id:190607) and post-failure run-out, [shear band localization](@entry_id:754756), or pile installation analysis .

#### Objective Formulations in Finite-Strain Plasticity

Implementing an objective [finite-strain plasticity](@entry_id:185352) model requires careful choices of [stress and strain](@entry_id:137374) measures. There are two prevalent approaches :

1.  **Spatial (Eulerian) Formulations:** These models evolve [stress measures](@entry_id:198799) in the current configuration, such as the Cauchy stress $\boldsymbol{\sigma}$ or Kirchhoff stress $\boldsymbol{\tau}$. Since the simple [material time derivative](@entry_id:190892) ($\dot{\boldsymbol{\sigma}}$) is not objective, it must be replaced by an **[objective stress rate](@entry_id:168809)**, such as the Jaumann or Green-Naghdi rate. These rates are constructed to correctly account for the rotation of the material, but the choice of rate can affect the predicted response, especially in non-[proportional loading](@entry_id:191744).

2.  **Intermediate Configuration Formulations:** A more modern and conceptually elegant approach is to formulate the constitutive laws in the intermediate configuration. The key is to use [stress measures](@entry_id:198799) that are naturally objective. The **Mandel stress**, $M = C_e S = F_e^T \boldsymbol{\tau} F_e^{-T}$ (where $C_e$ is the elastic right Cauchy-Green tensor and $S$ is the 2nd Piola-Kirchhoff stress), is invariant under superposed [rigid motions](@entry_id:170523). By defining the [yield function](@entry_id:167970) and an [associative flow rule](@entry_id:163391) for the plastic rate of deformation $D_p$ in terms of the Mandel stress, objectivity is guaranteed by construction.

Within the finite-strain framework, one must also specify the **[plastic spin](@entry_id:188692)**, $W_p = \text{skew}(\dot{F}_p F_p^{-1})$. The [plastic spin](@entry_id:188692) describes the rotation of the material's underlying [microstructure](@entry_id:148601). Importantly, it is not determined by the [dissipation inequality](@entry_id:188634) or the [principle of objectivity](@entry_id:185412). It is a separate constitutive choice. A common, simple assumption is $W_p = 0$ (the isoclinic assumption), which is a valid choice. However, for materials with evolving anisotropy (e.g., [kinematic hardening](@entry_id:172077)), the evolution of [plastic spin](@entry_id:188692) becomes physically significant, as it governs the rotation of the anisotropy's reference directions .