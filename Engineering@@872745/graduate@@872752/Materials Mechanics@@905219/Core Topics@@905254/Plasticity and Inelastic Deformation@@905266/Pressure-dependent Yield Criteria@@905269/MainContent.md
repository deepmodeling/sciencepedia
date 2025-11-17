## Introduction
While many engineering materials like metals yield based on shear stress alone, a vast and critical class of materials—including soils, rocks, concrete, and polymers—exhibit strength that is highly dependent on confining pressure. Standard [yield criteria](@entry_id:178101) like von Mises are insufficient for these materials, creating a knowledge gap that must be addressed for safe and efficient engineering design. This article provides a comprehensive introduction to pressure-dependent [yield criteria](@entry_id:178101), offering the theoretical tools needed to understand and predict the behavior of these complex materials. The discussion unfolds over three chapters. First, "Principles and Mechanisms" will establish the fundamental mathematical framework using [stress invariants](@entry_id:170526) and detail the two cornerstone models: the Mohr-Coulomb and Drucker-Prager criteria. Next, "Applications and Interdisciplinary Connections" will demonstrate the practical utility of these models in fields ranging from [geomechanics](@entry_id:175967) to polymer science. Finally, "Hands-On Practices" will solidify your understanding through applied problem-solving, bridging the gap between theory and application.

## Principles and Mechanisms

In the preceding chapter, we introduced the concept of yielding as the transition from elastic to [plastic deformation](@entry_id:139726). For a significant class of materials, including metals and some polymers under typical conditions, the onset of yielding is largely independent of the applied [hydrostatic pressure](@entry_id:141627). However, for a broad and important category of engineering materials—notably [geomaterials](@entry_id:749838) such as soils, rocks, and concrete, as well as some polymers and [metallic glasses](@entry_id:184761)—the [shear strength](@entry_id:754762) is strongly dependent on the level of confining pressure. This chapter delves into the principles and mechanisms governing this pressure-dependent yielding behavior. We will establish the necessary mathematical framework, explore the physical origins of this phenomenon, and detail the two most fundamental criteria used to model it: the Mohr-Coulomb and Drucker-Prager models.

### Stress Invariants for Pressure-Dependent Models

To describe material behavior that is independent of the observer's coordinate system, we must formulate our models in terms of [scalar invariants](@entry_id:193787) of the stress tensor, $\boldsymbol{\sigma}$. For pressure-dependent materials, it is particularly insightful to decompose the stress tensor into two parts: a **spherical** or **hydrostatic** component, which relates to changes in volume, and a **deviatoric** component, which relates to changes in shape (distortion).

The spherical part is defined by the **[mean stress](@entry_id:751819)**, $p$, which is one-third of the first invariant of the stress tensor, $I_1$:
$$p = \frac{1}{3} I_1 = \frac{1}{3} \mathrm{tr}(\boldsymbol{\sigma}) = \frac{1}{3}(\sigma_{11} + \sigma_{22} + \sigma_{33})$$
Following the standard mechanics convention, a positive value of $p$ denotes mean tension. In [geomechanics](@entry_id:175967), it is common to use an alternative convention where [mean stress](@entry_id:751819) is positive in compression. The spherical stress tensor is then $p\boldsymbol{I}$, where $\boldsymbol{I}$ is the second-order identity tensor.

The **[deviatoric stress tensor](@entry_id:267642)**, $\boldsymbol{s}$, is what remains after subtracting the spherical part from the total stress:
$$\boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I}$$
By its definition, the [deviatoric stress tensor](@entry_id:267642) is traceless, i.e., $\mathrm{tr}(\boldsymbol{s}) = 0$. It represents the state of pure shear stress at a point.

The magnitude of the deviatoric stress is quantified by the **second invariant of the [deviatoric stress tensor](@entry_id:267642)**, $J_2$:
$$J_2 = \frac{1}{2} \mathrm{tr}(\boldsymbol{s}^2) = \frac{1}{2} s_{ij}s_{ij}$$
While $J_2$ is a fundamental invariant, it is often more convenient in plasticity to work with an **equivalent shear stress**, commonly denoted by $q$. This quantity is defined such that it has a direct physical interpretation in common loading scenarios. A standard definition for $q$ is one that equates it to the difference between axial and confining stress, $\sigma_1 - \sigma_3$, in a uniaxial compression test ($\sigma_1 > 0, \sigma_2 = \sigma_3 = 0$). To establish a general relationship between $q$ and $J_2$, we can analyze a more general axisymmetric state where the principal stresses are $(\sigma_1, \sigma_3, \sigma_3)$ [@problem_id:2911486].

For this state, the mean stress is $p = \frac{1}{3}(\sigma_1 + 2\sigma_3)$. The principal deviatoric stresses are $s_1 = \sigma_1 - p = \frac{2}{3}(\sigma_1 - \sigma_3)$ and $s_2 = s_3 = \sigma_3 - p = -\frac{1}{3}(\sigma_1 - \sigma_3)$. The invariant $J_2$ is then:
$$J_2 = \frac{1}{2}(s_1^2 + s_2^2 + s_3^2) = \frac{1}{2} \left[ \left(\frac{2}{3}(\sigma_1-\sigma_3)\right)^2 + 2\left(-\frac{1}{3}(\sigma_1-\sigma_3)\right)^2 \right] = \frac{1}{3}(\sigma_1 - \sigma_3)^2$$
If we impose the condition that the [equivalent stress](@entry_id:749064) $q$ must equal the stress difference $\sigma_1 - \sigma_3$ for this state, we find the relationship $J_2 = \frac{1}{3}q^2$. Solving for $q$ (which is a magnitude and thus non-negative) gives the general definition:
$$q = \sqrt{3J_2}$$
The stress state of a material can thus be effectively characterized by the mean stress $p$ and the equivalent shear stress $q$. The [yield criteria](@entry_id:178101) for pressure-dependent materials are fundamentally relationships between these two quantities.

### The Micro-mechanical Origins of Frictional Strength

Before formalizing mathematical models, it is instructive to ask *why* some materials get stronger under pressure. The answer lies at the micro-scale. Materials like sand, gravel, and rock are assemblies of individual grains or particles held in contact. When this granular assembly is sheared, particles must slide and roll over their neighbors.

This sliding is resisted by friction at the contacts. The fundamental principle of solid friction, first studied by Amontons and Coulomb, states that the maximum [frictional force](@entry_id:202421) is proportional to the [normal force](@entry_id:174233) pressing the surfaces together. When a granular material is subjected to an external confining pressure, this pressure is transmitted through the contact network, increasing the normal forces between particles. A higher normal force at a contact means a greater tangential force is required to cause sliding.

Therefore, the overall [shear strength](@entry_id:754762) of the material, which is a macroscopic manifestation of countless micro-scale sliding events, increases with confining pressure. This is the essence of **frictional strength**. This concept can be formalized through micro-to-macro averaging theories, which show that the macroscopic [stress ratio](@entry_id:195276) at yield ($q/p$) is directly related to the inter-particle friction coefficient, as well as anisotropies that develop in the distribution of contact orientations and contact forces [@problem_id:2911544]. In essence, a more organized, pressure-stiffened "fabric" of force-carrying contacts can resist shear more effectively.

### The Mohr-Coulomb Criterion

The oldest and most widely used criterion for pressure-dependent materials is the **Mohr-Coulomb criterion**. It is an empirical model that elegantly captures the [linear relationship](@entry_id:267880) between shear strength and [normal stress](@entry_id:184326) observed in laboratory tests.

#### Definition and Physical Interpretation

In its most direct form, derived from experiments like the direct shear test, the Mohr-Coulomb criterion states that failure occurs on a plane when the shear stress, $\tau_f$, on that plane reaches a critical value that depends linearly on the effective [normal stress](@entry_id:184326), $\sigma'_n$, acting on the same plane [@problem_id:2911541]:
$$\tau_f = c + \sigma'_n \tan\phi$$
The two material parameters in this equation have clear physical interpretations:

*   **Cohesion ($c$)**: This is the intrinsic shear strength of the material when the effective [normal stress](@entry_id:184326) is zero. It represents the resistance to shear from sources other than friction, such as cementation between rock grains or electrochemical bonds in clay soils. For dry, uncemented [granular materials](@entry_id:750005) like sand, [cohesion](@entry_id:188479) is approximately zero.

*   **Angle of Internal Friction ($\phi$)**: This parameter quantifies the pressure-dependent component of strength. The term $\tan\phi$ acts as a coefficient of internal friction. An increase in the effective normal stress $\sigma'_n$ across a potential failure plane increases the shear resistance on that plane by an amount $\sigma'_n \tan\phi$. This frictional resistance arises from both inter-particle sliding and geometric interlocking, which may cause the material to expand in volume (**dilate**) during shear.

#### Yield Surface Geometry

The Mohr-Coulomb criterion can be generalized to a three-dimensional yield surface in [principal stress space](@entry_id:184388). The criterion posits that yielding is governed only by the maximum and minimum principal stresses, $\sigma_1$ and $\sigma_3$ (with $\sigma_1 \ge \sigma_2 \ge \sigma_3$). The full yield surface is a **hexagonal pyramid** whose axis coincides with the hydrostatic axis ($\sigma_1 = \sigma_2 = \sigma_3$).

The key feature of this hexagonal geometry is that the [yield surface](@entry_id:175331) is not a [surface of revolution](@entry_id:261378). A cross-section of the surface in the deviatoric plane (a plane of constant mean stress $p$, often called the $\pi$-plane) is an irregular hexagon [@problem_id:2911584]. The distance from the center of the hexagon to the yield locus depends on the direction of loading in this plane. This direction is parameterized by the **Lode angle**, $\theta$, which depends on the intermediate [principal stress](@entry_id:204375), $\sigma_2$.

This **sensitivity to the intermediate principal stress** is a defining characteristic of the Mohr-Coulomb model [@problem_id:2911443]. It means that the model predicts different yield strengths for different loading paths, such as triaxial compression ($\sigma_1 > \sigma_2 = \sigma_3$) and triaxial extension ($\sigma_1 = \sigma_2 > \sigma_3$), even if they have the same mean stress $p$. The corners of the hexagon correspond to these triaxial states, representing points where the active failure mechanism switches [@problem_id:2911584]. This Lode angle dependence is in stark contrast to pressure-independent criteria like the von Mises model, which is circular in the deviatoric plane, but shares this feature with the Tresca criterion.

### The Drucker-Prager Criterion

While the Mohr-Coulomb criterion is physically intuitive and captures key features of frictional materials, its hexagonal shape, with sharp corners and edges, makes it mathematically cumbersome for analytical and numerical calculations. The **Drucker-Prager criterion** was proposed as a smooth, simplified alternative.

#### Definition and Geometry

The Drucker-Prager criterion is a [simple extension](@entry_id:152948) of the von Mises criterion that includes a [linear dependence](@entry_id:149638) on [hydrostatic pressure](@entry_id:141627). It can be expressed directly in terms of the [stress invariants](@entry_id:170526) $I_1$ and $J_2$:
$$f(\boldsymbol{\sigma}) = \sqrt{J_2} + \alpha I_1 - k = 0$$
where $\alpha$ and $k$ are positive material constants. The parameter $\alpha$ controls the pressure sensitivity, and $k$ is related to cohesion.

The geometric representation of the Drucker-Prager yield surface in [principal stress space](@entry_id:184388) is a perfect, right circular **cone** [@problem_id:2911556]. The axis of the cone is the hydrostatic axis, and its apex lies on this axis at a point corresponding to a hydrostatic tensile stress (or high compressive stress, depending on convention and the sign of $\alpha$).

The most important consequence of this conical geometry is that the [yield surface](@entry_id:175331) is **axisymmetric**. Its cross-section in any deviatoric plane is a circle. This means the Drucker-Prager criterion is, by its very construction, **independent of the Lode angle $\theta$** [@problem_id:2911546]. In this model, the [yield strength](@entry_id:162154) depends only on the [mean stress](@entry_id:751819) $p$ and the magnitude of the shear stress $q$, but not on the intermediate principal stress $\sigma_2$.

### A Comparative Study: Mohr-Coulomb and Drucker-Prager

The choice between the Mohr-Coulomb and Drucker-Prager models involves a fundamental trade-off between physical realism and mathematical simplicity.

#### Lode Angle Dependence and Physical Accuracy

The primary difference lies in their treatment of the intermediate [principal stress](@entry_id:204375). The hexagonal Mohr-Coulomb surface predicts that materials are typically stronger in triaxial compression than in triaxial extension, a behavior observed in many [geomaterials](@entry_id:749838). The circular Drucker-Prager criterion cannot capture this difference; it predicts the same yield strength for any stress state with the same $(p,q)$ values [@problem_id:2911546]. Because of this, the Drucker-Prager model is often considered a less accurate, [first-order approximation](@entry_id:147559) for materials with significant Lode angle dependence.

#### Drucker-Prager as an Approximation of Mohr-Coulomb

Given the prevalence of Mohr-Coulomb parameters ($c, \phi$), the Drucker-Prager model is often calibrated to approximate the Mohr-Coulomb criterion. This involves "fitting" the Drucker-Prager circle to the Mohr-Coulomb hexagon in the deviatoric plane [@problem_id:2911597]. There are two common approaches:

1.  **Matching Triaxial Compression**: The DP circle is made to pass through the outer vertices of the MC hexagon. This matches the strength in triaxial compression but results in a DP surface that *circumscribes* the MC surface. This model over-predicts the material's strength for all other stress states and is therefore non-conservative.

2.  **Matching Triaxial Extension**: The DP circle is made to be tangent to the flat sides of the MC hexagon. This matches the strength in triaxial extension and results in a DP surface that is *inscribed* within the MC surface. This model is conservative, as it never over-predicts strength, but it can significantly underestimate the strength in triaxial compression.

This dependency of the DP parameters on the fitting choice highlights that it is an approximation, not an equivalent representation.

#### Consequences of Geometric Regularity

The geometric difference—corners versus smoothness—has profound implications for both physical predictions and numerical implementation [@problem_id:2911477].

*   **Plastic Flow Direction**: Under an **[associated flow rule](@entry_id:201731)** (discussed below), the direction of plastic strain is normal to the [yield surface](@entry_id:175331). For the smooth Drucker-Prager cone, this normal is uniquely defined at every point. For Mohr-Coulomb, the normal is also unique on the flat faces, but at the corners and edges, the concept of a normal is replaced by a *set* of possible directions (a [normal cone](@entry_id:272387)). This predicts a non-unique [plastic flow](@entry_id:201346) response at these specific stress states, which can be interpreted as allowing multiple simultaneous shear systems.

*   **Numerical Implementation**: The smoothness of the Drucker-Prager surface makes it far easier to implement in computational mechanics codes. Standard **return-mapping algorithms** for integrating [plastic deformation](@entry_id:139726) work robustly. In contrast, the corners and apex of the Mohr-Coulomb surface require special, complex algorithms to handle the return to these [singular points](@entry_id:266699), significantly complicating the development of a robust and efficient numerical model [@problem_id:2911597] [@problem_id:2911477].

### Plastic Flow and Volumetric Change (Dilatancy)

Beyond predicting the onset of yielding, a complete plasticity model must describe the evolution of plastic strain once yielding begins. This is governed by a **[flow rule](@entry_id:177163)**, which is often expressed in terms of a **[plastic potential](@entry_id:164680)**, $g(\boldsymbol{\sigma})$. The plastic strain rate, $\dot{\boldsymbol{\varepsilon}}^p$, is assumed to be proportional to the gradient of this potential:
$$\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}}$$
where $\dot{\lambda}$ is a non-negative [plastic multiplier](@entry_id:753519).

If the [plastic potential](@entry_id:164680) is chosen to be the same as the [yield function](@entry_id:167970) ($g = f$), the model is said to have an **[associated flow rule](@entry_id:201731)**. If $g \neq f$, the [flow rule](@entry_id:177163) is **non-associated**.

For pressure-dependent materials, the yield function depends on the mean stress $p$. For an [associated flow rule](@entry_id:201731), this has a critical consequence: the gradient $\partial f/\partial \boldsymbol{\sigma}$ has a hydrostatic component, meaning that the plastic [strain rate](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}^p$ will have a non-zero trace. This signifies that plastic shear deformation is coupled with plastic volume change, a phenomenon known as **dilatancy** (volume increase) or compaction (volume decrease).

A common measure of this effect is the **[dilatancy angle](@entry_id:748435)**, $\psi$. For a model expressed in $(p,q)$ space, it can be shown that $\tan\psi = - (\partial g / \partial p) / (\partial g / \partial q)$.

A classic result of associated Mohr-Coulomb plasticity is that this framework predicts a [dilatancy angle](@entry_id:748435) equal to the friction angle, i.e., $\psi = \phi$ [@problem_id:2911493]. While frictional materials do dilate, this prediction often significantly overestimates the amount of volume expansion observed experimentally.

To resolve this, [non-associated flow](@entry_id:202786) rules are widely used in [geomechanics](@entry_id:175967). A common approach is to use the Mohr-Coulomb criterion as the [yield function](@entry_id:167970) $f$ (to accurately predict strength) but to use a smooth Drucker-Prager-type function for the [plastic potential](@entry_id:164680) $g$:
$$g(q, p) = q - M_p p$$
In this formulation, the parameter $M_p = \tan\psi$ directly controls the amount of [dilatancy](@entry_id:201001), which can now be specified independently of the friction angle $\phi$ that governs the strength in $f$. A common choice is to set $\psi=0$ (meaning $M_p=0$), which results in purely deviatoric (isochoric) plastic flow and completely removes the unrealistic dilation predicted by the associated model [@problem_id:2911493]. This decoupling of strength from flow [kinematics](@entry_id:173318) is a crucial tool for the realistic modeling of [pressure-sensitive materials](@entry_id:753710).