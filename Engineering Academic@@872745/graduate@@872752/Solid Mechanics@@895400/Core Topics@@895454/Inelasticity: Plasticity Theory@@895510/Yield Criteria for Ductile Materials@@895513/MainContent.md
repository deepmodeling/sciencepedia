## Introduction
In solid mechanics, understanding the transition from elastic to [plastic deformation](@entry_id:139726) is critical for designing safe and reliable structures. While a simple [uniaxial tension test](@entry_id:195375) can identify a clear [yield point](@entry_id:188474) for a material, most engineering components face complex, multiaxial states of stress where predicting the onset of permanent deformation is far from straightforward. This challenge is addressed by **[yield criteria](@entry_id:178101)**—sophisticated mathematical frameworks that define the limit of elastic behavior under any combination of stresses. These criteria are the cornerstone of [plasticity theory](@entry_id:177023), enabling engineers to prevent failure and optimize the use of ductile materials like metals.

This article provides a comprehensive exploration of the theory and application of [yield criteria](@entry_id:178101). It bridges the gap between abstract principles and practical engineering problems by detailing how these mathematical models are formulated, what physical mechanisms they represent, and how they are applied in [modern analysis](@entry_id:146248) and design. Across three chapters, you will gain a graduate-level understanding of this essential topic.

The journey begins in **"Principles and Mechanisms,"** where we establish the theoretical foundation. You will learn about the concept of a [yield surface](@entry_id:175331) in [stress space](@entry_id:199156), the critical principle of pressure-insensitivity for metals, and the [associated flow rule](@entry_id:201731) that governs the direction of plastic deformation. This chapter will introduce the two most important classical models, the Tresca and von Mises criteria, and extend the theory to include hardening and [material anisotropy](@entry_id:204117).

Next, **"Applications and Interdisciplinary Connections"** demonstrates the practical utility of these concepts. We will explore how [yield criteria](@entry_id:178101) are used to design and analyze structural components, perform [limit analysis](@entry_id:188743) to determine collapse loads, and inform advanced fields such as manufacturing [process simulation](@entry_id:634927), [fracture mechanics](@entry_id:141480), and [fatigue analysis](@entry_id:191624).

Finally, **"Hands-On Practices"** allows you to solidify your knowledge through guided problems. These exercises will take you from calculating fundamental stress components to applying different [yield criteria](@entry_id:178101) and implementing a core numerical algorithm used in modern finite element software, providing a concrete link between theory and computational practice.

## Principles and Mechanisms

The transition from elastic to plastic deformation is a cornerstone of [solid mechanics](@entry_id:164042), particularly for ductile materials like metals. When a material is subjected to a simple uniaxial tensile load, this transition is marked by a well-defined [yield point](@entry_id:188474) on the [stress-strain curve](@entry_id:159459). However, under the complex, multiaxial states of stress encountered in most engineering applications, predicting the onset of permanent deformation requires a more sophisticated framework. A **yield criterion** is a mathematical hypothesis that defines the limit of elastic behavior for any possible combination of stresses. This chapter elucidates the fundamental principles that govern the formulation of these criteria and the physical mechanisms they represent.

### The General Framework: Yield Surfaces and Hardening

To generalize the concept of yielding from a single stress value to a multiaxial stress state, we must work in the six-dimensional space of the symmetric **Cauchy stress tensor**, $\boldsymbol{\sigma}$. Within this space, we can define a boundary that separates purely elastic behavior from the domain where [plastic deformation](@entry_id:139726) is possible. This boundary is known as the **[yield surface](@entry_id:175331)**.

The formal mathematical tool for this is the **[yield function](@entry_id:167970)**, a scalar-valued function of the stress tensor and a set of internal variables that describe the material's history, denoted here by a single scalar **hardening variable** $\kappa$. The yield function is conventionally written as $f(\boldsymbol{\sigma}, \kappa)$. This function allows us to define three distinct regions in stress space [@problem_id:2711759]:

1.  The **Elastic Domain**, $\mathcal{E}$: This is the set of all stress states that the material can sustain purely elastically. It is defined by the condition $f(\boldsymbol{\sigma}, \kappa) \lt 0$. Any loading path that remains strictly inside this domain will produce no permanent deformation.

2.  The **Yield Surface**, $\partial\mathcal{E}$: This is the boundary of the elastic domain, defined by the level set $f(\boldsymbol{\sigma}, \kappa) = 0$. For a stress state to cause [plastic deformation](@entry_id:139726), it must lie on this surface.

3.  The **Inadmissible Domain**: In the theory of [rate-independent plasticity](@entry_id:754082), stress states for which $f(\boldsymbol{\sigma}, \kappa) \gt 0$ are considered physically unattainable. If a loading path reaches the [yield surface](@entry_id:175331), any further attempt to load "outside" the surface will be counteracted by [plastic deformation](@entry_id:139726), causing the stress state to remain on the evolving surface.

The hardening variable $\kappa$ captures the evolution of the material's resistance to [plastic flow](@entry_id:201346). For example, in **[isotropic hardening](@entry_id:164486)**, the [yield surface](@entry_id:175331) expands uniformly in all directions as plastic deformation accumulates. In this case, $\kappa$ could represent the accumulated equivalent plastic strain, and its increase leads to a larger elastic domain. This models the common observation that metals become stronger (i.e., have a higher [yield stress](@entry_id:274513)) after being plastically deformed.

A crucial geometric property of the [yield surface](@entry_id:175331) is its normal vector. At any smooth point $\boldsymbol{\sigma}$ on the yield surface, the gradient of the [yield function](@entry_id:167970) with respect to the stress tensor defines a tensor $\mathbf{n} = \frac{\partial f}{\partial \boldsymbol{\sigma}}$. This tensor is, by definition, normal (orthogonal) to the [yield surface](@entry_id:175331) at that point with respect to the standard [tensor inner product](@entry_id:190619) [@problem_id:2711716]. As we will see, this normal direction plays a profound role in determining the direction of [plastic flow](@entry_id:201346).

### The Direction of Plastic Flow: Stability and the Associated Flow Rule

Once the stress state reaches the yield surface, plastic deformation can begin. A central question then arises: for a given stress state on the yield surface, in which "direction" will plastic strain evolve? The answer is provided by a **[flow rule](@entry_id:177163)**, which relates the plastic strain rate, $\dot{\boldsymbol{\varepsilon}}^p$, to the current state of stress.

For a vast class of materials, particularly metals, the [flow rule](@entry_id:177163) is given by the **[associated flow rule](@entry_id:201731)**, also known as the **[normality rule](@entry_id:182635)**. This rule postulates that the plastic [strain rate tensor](@entry_id:198281) is directed along the outward normal to the yield surface [@problem_id:2711781]:

$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$

Here, $\dot{\lambda}$ is a non-negative scalar called the **[plastic multiplier](@entry_id:753519)** or consistency parameter. It is non-zero only when plastic deformation is actively occurring, a condition governed by the Kuhn-Tucker loading/unloading conditions: $f \le 0$, $\dot{\lambda} \ge 0$, and $\dot{\lambda} f = 0$. Geometrically, this rule means the "vector" of plastic strain increment is perpendicular to the [yield surface](@entry_id:175331) at the point of loading [@problem_id:2711716].

This rule is not an arbitrary choice; it is deeply rooted in [thermodynamic principles](@entry_id:142232) of [material stability](@entry_id:183933). **Drucker's stability postulate** asserts that a stable material cannot spontaneously expend energy during a cycle of loading and unloading [@problem_id:2711718]. A key consequence of this postulate is that for a material at a yield state $\boldsymbol{\sigma}$, the incremental [plastic work](@entry_id:193085) done by the difference between this stress and any other elastically admissible stress state $\boldsymbol{\sigma}^*$ must be non-negative: $(\boldsymbol{\sigma} - \boldsymbol{\sigma}^*) : \dot{\boldsymbol{\varepsilon}}^p \ge 0$.

For this inequality to hold for any admissible $\boldsymbol{\sigma}^*$ inside a **[convex yield surface](@entry_id:203690)**, the plastic strain rate vector $\dot{\boldsymbol{\varepsilon}}^p$ must be directed along the outward normal. Therefore, the combination of [material stability](@entry_id:183933) (Drucker's Postulate) and a convex elastic domain logically implies the [associated flow rule](@entry_id:201731) [@problem_id:2711781]. Conversely, the combination of a [convex yield surface](@entry_id:203690) and an [associated flow rule](@entry_id:201731) ensures that the incremental [plastic work](@entry_id:193085), $\dot{W}^p = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p$, is always non-negative, satisfying the condition for stability [@problem_id:2711718]. An equivalent formulation, the **principle of maximum [plastic dissipation](@entry_id:201273)**, also leads to the same normality structure [@problem_id:2711781].

### A Cornerstone of Metal Plasticity: Pressure-Insensitivity

A remarkable experimental observation for most fully dense ductile metals is that their yielding behavior is nearly independent of the applied **[hydrostatic pressure](@entry_id:141627)**. A metal bar under immense hydrostatic pressure in the deep sea will have almost the same tensile [yield strength](@entry_id:162154) as it does at atmospheric pressure. This physical principle imposes a powerful constraint on the mathematical form of the yield function. Its justification comes from both microscopic and macroscopic viewpoints.

From a microscopic, physics-based perspective, plastic deformation in crystalline metals is overwhelmingly dominated by [dislocation glide](@entry_id:275474) on specific [crystallographic slip](@entry_id:196486) systems. The driving force for this glide is the **[resolved shear stress](@entry_id:201022)** on a [slip system](@entry_id:155264). A pure [hydrostatic stress](@entry_id:186327) state, represented by the tensor $\boldsymbol{\sigma} = -p\mathbf{I}$ (where $p$ is pressure and $\mathbf{I}$ is the identity tensor), produces a traction vector on any plane that is purely normal to that plane. It has no shear component. Consequently, hydrostatic pressure produces zero [resolved shear stress](@entry_id:201022) on any conceivable [slip system](@entry_id:155264) and thus cannot, by itself, cause plastic yielding via [dislocation glide](@entry_id:275474) [@problem_id:2711755] [@problem_id:2711750].

From a macroscopic, continuum perspective, we can examine the rate of plastic work dissipation, $\dot{W}^p = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p$. By decomposing the stress tensor into its hydrostatic part ($-p\mathbf{I}$) and its **deviatoric** part ($\mathbf{s} = \boldsymbol{\sigma} + p\mathbf{I}$), the work rate becomes $\dot{W}^p = \mathbf{s}:\dot{\boldsymbol{\varepsilon}}^p - p\,\mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p)$. Experiments show that plastic flow in dense metals is very nearly **isochoric** (volume-preserving), meaning the volumetric plastic strain rate, $\mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p)$, is zero. This leaves $\dot{W}^p = \mathbf{s}:\dot{\boldsymbol{\varepsilon}}^p$. This demonstrates that the hydrostatic part of the stress does no [plastic work](@entry_id:193085). Since yielding marks the onset of this dissipation, it is physically justified that the yield criterion should depend only on the [deviatoric stress](@entry_id:163323) $\mathbf{s}$, not the pressure $p$ [@problem_id:2711755].

For an isotropic material, this pressure-insensitivity means the [yield function](@entry_id:167970) $f$ must be a function of the invariants of the [deviatoric stress tensor](@entry_id:267642), typically the second invariant $J_2 = \frac{1}{2}\mathbf{s}:\mathbf{s}$ and the third invariant $J_3 = \det(\mathbf{s})$.

It is crucial to note that this principle applies to fully dense materials. In materials with voids or pores, [hydrostatic pressure](@entry_id:141627) can contribute to plastic work by causing void growth or collapse. For such materials, the [yield criterion](@entry_id:193897) becomes pressure-dependent, and more advanced models (e.g., the Gurson model) are required [@problem_id:2711755].

### Classical Isotropic Yield Criteria

Based on these principles, several classical criteria have been proposed for isotropic ductile metals. The two most prominent are the Tresca and von Mises criteria.

#### The Tresca Criterion (Maximum Shear Stress)

Postulated by Henri Tresca, this criterion is based on the simple physical idea that yielding begins when the maximum shear stress at any point in the material reaches a critical value. The maximum shear stress, $\tau_{\max}$, at a point can be expressed in terms of the [principal stresses](@entry_id:176761) $(\sigma_1, \sigma_2, \sigma_3)$ as [@problem_id:2711776]:

$$
\tau_{\max} = \frac{1}{2}\max\left\{ |\sigma_1 - \sigma_2|, |\sigma_2 - \sigma_3|, |\sigma_3 - \sigma_1| \right\}
$$

The Tresca criterion states that yielding occurs when $\tau_{\max}$ equals the material's yield strength in pure shear, $k$. This critical value $k$ is typically determined from a simple [uniaxial tension test](@entry_id:195375). At yield in such a test, the stress state is $\sigma_1 = \sigma_y$ and $\sigma_2 = \sigma_3 = 0$. The maximum shear stress is therefore $\tau_{\max} = \frac{1}{2} |\sigma_y - 0| = \frac{\sigma_y}{2}$. Thus, the critical shear stress is half the uniaxial [yield stress](@entry_id:274513), $k = \sigma_y/2$.

The yield condition for a general stress state is then $\tau_{\max} = \sigma_y/2$, which leads to the Tresca [yield function](@entry_id:167970):

$$
f(\boldsymbol{\sigma}) = 2\tau_{\max} - \sigma_y = \max\left\{ |\sigma_1 - \sigma_2|, |\sigma_2 - \sigma_3|, |\sigma_3 - \sigma_1| \right\} - \sigma_y = 0
$$

Geometrically, the Tresca [yield surface](@entry_id:175331) is a hexagonal prism in the [principal stress space](@entry_id:184388).

#### The von Mises Criterion (Maximum Distortion Energy)

The von Mises criterion, also associated with Huber and Hencky, proposes that yielding begins when the **elastic distortional [strain energy density](@entry_id:200085)**, $U_d$, reaches a critical value. The total elastic strain energy in a body can be decomposed into a volumetric part (associated with volume change) and a distortional part (associated with shape change). Since plastic flow in metals is a process of pure distortion (shape change) at constant volume, it is physically plausible that the energy of distortion governs its onset.

For a linear elastic [isotropic material](@entry_id:204616), the distortional energy density is directly proportional to the second invariant of the [deviatoric stress](@entry_id:163323), $J_2$:

$$
U_d = \frac{1}{2G} J_2 \quad \text{where} \quad J_2 = \frac{1}{2}\mathbf{s}:\mathbf{s}
$$

and $G$ is the shear modulus. The [yield criterion](@entry_id:193897) $U_d = \text{constant}$ is thus equivalent to $J_2 = \text{constant}$ [@problem_id:2711750]. This form also arises naturally if one seeks the simplest possible (quadratic) smooth [yield function](@entry_id:167970) that is consistent with [isotropy](@entry_id:159159) and pressure-insensitivity [@problem_id:2711754].

Calibrating with the [uniaxial tension test](@entry_id:195375) gives the standard form of the von Mises criterion:

$$
f(\boldsymbol{\sigma}) = \sqrt{3J_2} - \sigma_y = 0
$$

Geometrically, this equation describes a right circular cylinder in [principal stress space](@entry_id:184388), with its axis aligned with the hydrostatic line $\sigma_1 = \sigma_2 = \sigma_3$. All stress states with the same $J_2$ value are predicted to be equally close to yielding, regardless of their hydrostatic component [@problem_id:2711754].

A powerful feature of the von Mises criterion, when combined with the [associated flow rule](@entry_id:201731), is its [self-consistency](@entry_id:160889). The normal to the $J_2$ [yield surface](@entry_id:175331) is proportional to the [deviatoric stress tensor](@entry_id:267642), $\mathbf{n} \propto \mathbf{s}$ [@problem_id:2711716]. The [associated flow rule](@entry_id:201731), $\dot{\boldsymbol{\varepsilon}}^p \propto \mathbf{s}$, then automatically predicts volume-preserving plastic flow, since $\mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p) \propto \mathrm{tr}(\mathbf{s}) = 0$. This aligns perfectly with the macroscopic physical arguments for pressure-insensitivity [@problem_id:2711781].

### Beyond Simple Isotropy: Hardening and Anisotropy

The classical Tresca and von Mises criteria describe the *initial* yielding of an isotropic material. Real material behavior is more complex, involving changes in the yield surface with ongoing [plastic deformation](@entry_id:139726).

#### Kinematic Hardening and the Bauschinger Effect

While [isotropic hardening](@entry_id:164486) describes a uniform expansion of the yield surface, many metals exhibit a directional hardening phenomenon known as the **Bauschinger effect**. This effect is characterized by a reduced yield strength when the direction of loading is reversed. For instance, a metal bar pulled into the plastic regime will subsequently yield in compression at a stress magnitude lower than its initial tensile yield strength [@problem_id:2711785].

This macroscopic behavior is a manifestation of **long-range internal stresses** that develop at the microstructural level due to the formation of polarized dislocation structures, such as pile-ups at grain boundaries. These internal stresses oppose the initial direction of loading but assist deformation upon reversal.

In continuum plasticity, this is modeled by **[kinematic hardening](@entry_id:172077)**, where the [yield surface](@entry_id:175331) translates in [stress space](@entry_id:199156) without changing its size or shape. This is achieved by introducing a tensor-valued internal variable called the **backstress**, $\boldsymbol{\alpha}$, which represents the center of the yield surface. The [yield function](@entry_id:167970) is then written in terms of an [effective stress](@entry_id:198048), $\boldsymbol{\sigma}' = \boldsymbol{\sigma} - \boldsymbol{\alpha}$:

$$
f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = \phi(\mathbf{s} - \boldsymbol{\alpha}') - Y_0 = 0
$$

where $\boldsymbol{\alpha}'$ is the deviatoric part of the [backstress](@entry_id:198105). The evolution of the backstress with plastic strain can be described by various laws, with non-[linear models](@entry_id:178302) (e.g., Armstrong-Frederick) capturing the eventual saturation of the Bauschinger effect during [cyclic loading](@entry_id:181502) by incorporating a "[dynamic recovery](@entry_id:200182)" term that models dislocation rearrangement and annihilation [@problem_id:2711785].

#### Anisotropy and Textured Materials

Many engineering materials are not isotropic. Manufacturing processes like cold rolling or extrusion align the crystallographic lattices of the constituent grains into a non-random distribution, known as a **[crystallographic texture](@entry_id:186522)**. Because plastic slip at the crystal level is highly anisotropic (occurring only on specific planes), this [preferred orientation](@entry_id:190900) at the micro-scale leads to direction-dependent [mechanical properties](@entry_id:201145) at the macro-scale [@problem_id:2711761].

This means the [yield strength](@entry_id:162154) and post-yield plastic flow will depend on the direction of loading relative to the manufacturing axes (e.g., rolling direction, transverse direction). Isotropic criteria like von Mises, which depend only on [stress invariants](@entry_id:170526), cannot capture this behavior as they predict the same yield strength in all directions.

To model such materials, **[anisotropic yield criteria](@entry_id:181680)** are required. For a material with orthotropic symmetry, like a rolled sheet, the [yield function](@entry_id:167970) must be constructed to respect this symmetry. A widely used example is Hill's 1948 quadratic [yield criterion](@entry_id:193897), which is a generalization of the von Mises criterion:

$$
F(\sigma_{22}-\sigma_{33})^2 + G(\sigma_{33}-\sigma_{11})^2 + H(\sigma_{11}-\sigma_{22})^2 + 2L\sigma_{23}^2 + 2M\sigma_{31}^2 + 2N\sigma_{12}^2 = 1
$$

The coefficients $F, G, H, L, M, N$ are material parameters that characterize the anisotropy. These parameters are determined by fitting the model to experimental data, such as yield stresses and plastic strain ratios (Lankford coefficients) measured in different orientations [@problem_id:2711761]. When combined with an [associated flow rule](@entry_id:201731), such anisotropic yield functions can successfully predict both the direction-dependent yield strengths and the anisotropic [plastic flow](@entry_id:201346) observed in textured metals.