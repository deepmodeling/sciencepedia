## Introduction
In solid mechanics, accurately predicting when a material will yield and fail is a foundational challenge. While classical models like the von Mises criterion successfully describe the behavior of metals, they fall short when applied to a vast class of materials whose strength is intrinsically tied to the applied pressure. Geomaterials such as soils, rocks, and concrete exhibit this pressure-sensitive behavior, where an increase in confining pressure enhances their shear strength. This article provides a comprehensive exploration of the theories developed to capture this critical phenomenon. It addresses the gap left by pressure-insensitive models by focusing on yield criteria specifically designed for frictional materials.

This article is structured to build your expertise progressively. In the first chapter, **Principles and Mechanisms**, we will delve into the physical origins of pressure sensitivity and establish the mathematical framework of stress invariants, leading to the formulation of the Drucker-Prager and Mohr-Coulomb criteria. The second chapter, **Applications and Interdisciplinary Connections**, will bridge theory and practice by demonstrating how these models are calibrated from experimental data and applied in geotechnical engineering and computational simulations. Finally, the **Hands-On Practices** section offers practical exercises to solidify your understanding of these advanced concepts. Let us begin by examining the core principles that govern the mechanics of pressure-sensitive materials.

## Principles and Mechanisms

This chapter elucidates the fundamental principles and mechanics governing the behavior of pressure-sensitive materials. We will establish the physical basis for pressure-dependent yielding, construct the necessary mathematical framework using stress invariants, and explore the formulation and application of two canonical pressure-sensitive yield criteria: the Drucker-Prager and Mohr-Coulomb models. Subsequently, we will examine the rules that dictate the direction of plastic flow and conclude with an analysis of special considerations for yield surfaces with geometric singularities.

### The Physical Origins of Pressure Sensitivity

The question of whether a material's strength depends on the applied hydrostatic pressure lies at the heart of constitutive modeling. The answer is rooted in the material's microscopic structure and the dominant mechanisms of deformation. A comparison between polycrystalline metals and granular geomaterials provides a stark and informative contrast [@problem_id:2674264].

In crystalline metals, plastic deformation is primarily driven by the motion of dislocations on specific crystallographic planes, known as slip systems. The onset of this motion, or slip, is governed by the resolved shear stress on the slip system, a principle formalized by **Schmid's law**. A crucial insight is that a state of pure hydrostatic stress, whether tensile or compressive, exerts no shear stress on any plane within the material. Consequently, the hydrostatic component of a general stress state does not contribute to the resolved shear stress that drives dislocation glide. Yielding in metals is therefore almost entirely dependent on the deviatoric (shape-changing) part of the stress tensor. This physical reality is reflected in classical yield criteria like the **von Mises** and **Tresca** criteria, for which the yield function $f$ is independent of the hydrostatic stress, leading to the condition $\partial f / \partial I_1 = 0$, where $I_1$ is the first invariant of the stress tensor [@problem_id:2674264].

Geomaterials, such as soils, rocks, and concrete, exhibit a profoundly different behavior. These materials are typically composed of discrete grains or particles held in contact. Macroscopic deformation involves sliding and rearrangement of these particles. At the microscale, the resistance to sliding between two grains is governed by **Coulomb's law of friction**. This law posits that the tangential force required to initiate slip is proportional to the normal force pressing the grains together. When a granular assembly is subjected to a macroscopic stress, the hydrostatic component of this stress directly relates to the average normal forces at the grain contacts. An increase in confining pressure increases these normal forces, which in turn increases the frictional resistance to sliding at each contact. The macroscopic shear strength of the material is the collective result of this inter-granular resistance. Therefore, unlike metals, the shear strength of a geomaterial is intrinsically linked to the level of hydrostatic confinement. This phenomenon is termed **pressure sensitivity**, and it requires that the material's yield function $f$ has a significant dependence on the hydrostatic stress, such that $\partial f / \partial I_1 \neq 0$ [@problem_id:2674264].

### A Framework for Isotropic Plasticity: Stress Invariants

To mathematically describe the behavior of isotropic materials, it is advantageous to express the yield criterion not in terms of the components of the stress tensor $\boldsymbol{\sigma}$, which depend on the coordinate system, but in terms of its **invariants**, which are scalar quantities that remain unchanged under coordinate rotations. For an isotropic material, any yield function $f(\boldsymbol{\sigma})$ can be fully expressed as a function of a set of independent invariants, a representation that elegantly separates the influences of pressure and shear [@problem_id:2674218].

The stress tensor $\boldsymbol{\sigma}$ can be uniquely decomposed into a **hydrostatic** part, which causes volume change, and a **deviatoric** part, which causes shape change (distortion).
The hydrostatic part is described by the **mean pressure** $p$, defined in terms of the first principal invariant of stress, $I_1 = \mathrm{tr}(\boldsymbol{\sigma}) = \sigma_{kk}$. Adopting the standard geomechanics sign convention where compression is positive, the mean pressure is:
$$
p = \frac{1}{3} I_1 = \frac{1}{3}(\sigma_1 + \sigma_2 + \sigma_3)
$$
where $\sigma_1, \sigma_2, \sigma_3$ are the principal stresses. The **deviatoric stress tensor**, $\boldsymbol{s}$, is then defined as the remainder:
$$
\boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I}
$$
where $\boldsymbol{I}$ is the second-order identity tensor. By its construction, the deviatoric stress is traceless, i.e., $\mathrm{tr}(\boldsymbol{s}) = 0$. A purely hydrostatic change in stress, $\Delta\boldsymbol{\sigma} = \Delta p \boldsymbol{I}$, alters $p$ but leaves the deviatoric stress tensor $\boldsymbol{s}$ unchanged [@problem_id:2674218].

The intensity of the deviatoric stress is most commonly quantified by its second invariant, $J_2$:
$$
J_2 = \frac{1}{2} \boldsymbol{s}:\boldsymbol{s} = \frac{1}{2} s_{ij}s_{ij}
$$
where $s_{ij}$ are the components of $\boldsymbol{s}$. The quantity $\sqrt{J_2}$ is a measure of the average shear stress. In plasticity, it is often convenient to work with the **von Mises equivalent shear stress**, denoted by $q$, which is proportional to $\sqrt{J_2}$:
$$
q = \sqrt{3J_2}
$$
The equivalent stress $q$ has a clear expression in terms of principal stresses, which can be derived from its definition [@problem_id:2674266]:
$$
q = \sqrt{\frac{1}{2} [(\sigma_1 - \sigma_2)^2 + (\sigma_2 - \sigma_3)^2 + (\sigma_3 - \sigma_1)^2]}
$$
The pair $(p, q)$ provides a powerful two-dimensional representation of the stress state, cleanly separating the hydrostatic component ($p$) from the overall magnitude of the shear component ($q$).

While $p$ and $q$ are sufficient for many models, a complete description of the deviatoric stress state requires a third invariant, $J_3$, which describes the "mode" of shear. It is defined as the determinant of the deviatoric stress tensor:
$$
J_3 = \det(\boldsymbol{s}) = s_1 s_2 s_3
$$
where $s_1, s_2, s_3$ are the principal deviatoric stresses. The invariant $J_3$ is often expressed through the **Lode angle**, $\theta$, defined by:
$$
\cos(3\theta) = \frac{3\sqrt{3}}{2} \frac{J_3}{J_2^{3/2}}
$$
The Lode angle, which conventionally takes values in the range $\theta \in [0, \pi/3]$, distinguishes between different stress states that have the same mean pressure $p$ and the same shear intensity $q$ [@problem_id:2674256]. For instance, a state of axisymmetric (or triaxial) compression, where $\sigma_1 > \sigma_2 = \sigma_3$, corresponds to a Lode angle of $\theta=0$. Conversely, a state of axisymmetric (or triaxial) extension, where $\sigma_1 = \sigma_2 > \sigma_3$, corresponds to $\theta=\pi/3$. Stress states like pure shear, where the intermediate principal stress is the average of the major and minor ones, result in $J_3=0$ and correspond to $\theta=\pi/6$ [@problem_id:2674256].

The complete set of invariants $(I_1, J_2, J_3)$, or equivalently $(p, q, \theta)$, provides a full and objective basis for describing any stress state for an isotropic material [@problem_id:2674218].

### The Drucker-Prager Criterion: A Linear Model of Pressure Sensitivity

The simplest smooth yield criterion that captures pressure sensitivity is the **Drucker-Prager (DP) criterion**. It proposes a linear relationship between the measure of shear stress, $\sqrt{J_2}$, and the measure of hydrostatic stress, $I_1$. Using a tension-positive convention for stress, which is common in continuum mechanics, the DP yield function is written as:
$$
f_{\text{DP}} = \sqrt{J_2} + \alpha I_1 - k = 0
$$
Here, $k$ is a material parameter related to the cohesion of the material, representing its shear strength when the hydrostatic stress is zero ($I_1=0$). The parameter $\alpha$ governs the material's sensitivity to pressure. For a frictional material that gains strength under compression ($I_1  0$), the parameter $\alpha$ must be positive. This ensures that as $I_1$ becomes more negative, a larger value of $\sqrt{J_2}$ is required to reach yield [@problem_id:2674239]. Setting $\alpha=0$ recovers the pressure-insensitive von Mises criterion, $f_{\text{VM}} = \sqrt{J_2} - k = 0$.

It is often necessary to work with a pressure convention where compression is positive, as is standard in soil mechanics. This requires careful handling of signs. If we define mean pressure $p = -I_1/3$ (so $p0$ in compression), the DP criterion can be transformed into the $p-q$ plane. Substituting $\sqrt{J_2} = q/\sqrt{3}$ and $I_1 = -3p$ into the yield function gives:
$$
\frac{q}{\sqrt{3}} + \alpha(-3p) - k = 0 \implies q = 3\sqrt{3}\alpha p + \sqrt{3}k
$$
This equation describes a straight line in the $p-q$ plane, known as a **yield meridian**. Its slope, $M = 3\sqrt{3}\alpha$, is proportional to the friction parameter $\alpha$, and its intercept, $d = \sqrt{3}k$, is proportional to the cohesion parameter $k$ [@problem_id:2674239], [@problem_id:2674224].

A key characteristic of the DP model is that its yield function depends only on $I_1$ and $J_2$, with no dependence on $J_3$. This means that for a given mean pressure $p$, the yield strength is the same for all modes of shearing. Geometrically, this implies that the yield surface in principal stress space is a right circular cone, and its cross-section in the deviatoric plane (the $\pi$-plane) is a circle. The DP criterion is thus independent of the Lode angle $\theta$ [@problem_id:2674239].

### The Mohr-Coulomb Criterion: A Refined Frictional Model

While the Drucker-Prager model provides a simple and useful first approximation, many geomaterials exhibit strength that depends on the Lode angle. The classical **Mohr-Coulomb (MC) criterion** captures this effect. It is based on the physical postulate that slip occurs on a plane when the shear stress $\tau$ on that plane reaches a critical value that depends linearly on the normal stress $\sigma_n$ (compression positive) acting on that same plane:
$$
|\tau| \le c + \sigma_n \tan\varphi
$$
Here, $c$ is the material's **cohesion** and $\varphi$ is its **angle of internal friction**. In a general three-dimensional stress state, this condition is governed by the major and minor principal stresses, $\sigma_1$ and $\sigma_3$.

The practical importance of pressure sensitivity is vividly illustrated by a simple thought experiment [@problem_id:2674220]. Consider two different states of triaxial compression on a geomaterial with $c = 5\,\mathrm{MPa}$ and $\varphi = 30^{\circ}$:
*   **State A:** Confining stress $\sigma_3 = 50\,\mathrm{MPa}$, axial stress $\sigma_1 = 165\,\mathrm{MPa}$.
*   **State B:** Confining stress $\sigma_3 = 10\,\mathrm{MPa}$, axial stress $\sigma_1 = 125\,\mathrm{MPa}$.

For both states, the deviatoric stress measure is identical: $q = \sigma_1 - \sigma_3 = 115\,\mathrm{MPa}$. A pressure-insensitive criterion like von Mises, which depends only on $q$, would assess both states as being equally close to failure [@problem_id:2674220]. However, the mean pressures are vastly different: $p_A = \frac{1}{3}(165 + 2 \times 50) \approx 88.3\,\mathrm{MPa}$, while $p_B = \frac{1}{3}(125 + 2 \times 10) \approx 48.3\,\mathrm{MPa}$. According to the Mohr-Coulomb criterion, State A is stable (elastic), while State B has far exceeded the material's strength. This is because the higher confining pressure in State A provides significantly greater frictional strength, allowing it to sustain the same level of shear stress $q$ that causes failure in the less confined State B. This example underscores that for pressure-sensitive materials, specifying shear stress alone is insufficient to assess failure; the hydrostatic stress state is equally critical.

When expressed in terms of stress invariants, the MC criterion reveals its dependence on the Lode angle $\theta$. This yields an irregular hexagonal pyramid in principal stress space. The yield strength is greatest in triaxial compression ($\theta=0$) and smallest in triaxial extension ($\theta=\pi/3$). This dependence can be captured by writing the yield meridian in the $p-q$ plane as a function of $\theta$ [@problem_id:2674219]:
$$
q = p \cdot M(\theta) + k(\theta)
$$
where the slope $M(\theta)$ and intercept $k(\theta)$ are functions of the Lode angle. For the triaxial compression path ($\theta=0$), the expressions derived from the MC condition are:
$$
M(0) = \frac{6\sin\varphi}{3-\sin\varphi} \quad \text{and} \quad k(0) = \frac{6c\cos\varphi}{3-\sin\varphi}
$$
Similar, but different, expressions hold for other values of $\theta$. This explicit dependence on $\theta$ is the primary distinction between the Mohr-Coulomb and Drucker-Prager criteria. If a DP cone is calibrated to match the MC criterion along the triaxial compression meridian (the strongest condition), it will circumscribe the MC hexagon. This means the DP model will significantly overpredict the material's strength in other stress states, such as triaxial extension and pure shear [@problem_id:2674239].

### Plastic Flow and the Role of the Plastic Potential

The yield criterion defines the boundary of the elastic domain. To describe the material's behavior during plastic deformation, we need a **flow rule**, which specifies the direction of the plastic strain rate, $\dot{\boldsymbol{\varepsilon}}^p$. In the framework of rate-independent plasticity, the flow rule is given by:
$$
\dot{\boldsymbol{\varepsilon}}^p = \lambda \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$
where $\lambda \ge 0$ is the plastic multiplier (a scalar that is non-zero only during plastic loading), and $g(\boldsymbol{\sigma})$ is a scalar function known as the **plastic potential**. The gradient of the plastic potential, $\partial g / \partial \boldsymbol{\sigma}$, defines the direction of the plastic flow in stress space.

A critical distinction is made based on the choice of the plastic potential $g$ [@problem_id:2674251]:
1.  **Associated Flow:** If the plastic potential is chosen to be the same as the yield function ($g=f$), the flow rule is said to be **associated**. This implies that the vector of plastic strain rate is normal to the yield surface. This is a common and simplifying assumption, often called the normality rule.
2.  **Non-Associated Flow:** If the plastic potential is different from the yield function ($g \neq f$), the flow rule is **non-associated**. In this case, the yield function $f$ still governs the onset of yielding, but the separate potential function $g$ independently governs the direction of plastic flow.

This distinction is of paramount importance for pressure-sensitive materials. A key component of plastic strain is the plastic volume change, or **dilatancy**, quantified by the plastic volumetric strain rate, $\dot{\varepsilon}_v^p = \mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p)$. It can be shown that this quantity is directly related to the derivative of the plastic potential with respect to the mean pressure [@problem_id:2674251]:
$$
\dot{\varepsilon}_v^p = \lambda \frac{\partial g}{\partial p}
$$
For a pressure-sensitive yield criterion like Mohr-Coulomb, the derivative $\partial f / \partial p$ is significant. If an associated flow rule ($g=f$) is used, this leads to a prediction of large plastic volume expansion (dilatancy) during shear. Experimental evidence for many soils and rocks shows that while they do dilate, the amount is often much less than predicted by an associated flow rule.

Non-associated plasticity provides the necessary theoretical flexibility. By defining a plastic potential $g$ that is different from the yield function $f$, we can decouple the modeling of strength from the modeling of plastic flow. A common practice is to use a Mohr-Coulomb yield function with friction angle $\varphi$, but to define a Mohr-Coulomb-like plastic potential with a separate **dilatancy angle** $\psi$, where typically $0 \le \psi \le \varphi$. The ratio of the plastic volumetric strain rate to the plastic shear strain rate can then be shown to be a function of $\psi$, not $\varphi$ [@problem_id:2674229]. For instance, under triaxial compression, this ratio is given by:
$$
\frac{d\varepsilon_v^p}{d\varepsilon_s^p} = \frac{-6\sin\psi}{3-\sin\psi}
$$
Choosing $\psi  \varphi$ allows for a more realistic, reduced level of dilatancy, while the material's strength is still correctly governed by the friction angle $\varphi$ in the yield function. A choice of $\psi=0$ corresponds to a non-dilatant, or purely deviatoric, plastic flow.

### Advanced Topic: Plastic Flow at Yield Surface Corners

The Mohr-Coulomb yield surface, being a hexagonal pyramid, is not smooth. It possesses edges and corners where the gradient is not uniquely defined. For a stress state $\boldsymbol{\sigma}^\star$ located at such a **corner**, where multiple smooth yield faces intersect, the standard normality rule breaks down.

In the framework of convex analysis, the set of all possible outward normal directions at a corner is called the **normal cone**. This cone is formed by the **convex hull** of the gradients of all the smooth faces that are active at that corner [@problem_id:2674198]. This means that the associative flow rule does not provide a single direction for the plastic strain rate, but rather a cone of possible directions.

To resolve this ambiguity, a higher-order principle is invoked: the **Principle of Maximum Plastic Dissipation**. This principle, rooted in thermodynamics, states that among all kinematically possible plastic strain rates, the one that actually occurs is the one that maximizes the rate of plastic work, $D = \boldsymbol{\sigma}^\star : \dot{\boldsymbol{\varepsilon}}^p$.

Since the dissipation rate $D$ is a linear function of the plastic strain rate, and the set of possible strain rate directions is a convex polyhedron (the base of the normal cone), the maximum of $D$ must be achieved at one of the vertices of this set. The vertices are simply the normal vectors of the individual intersecting faces. This leads to **Koiter's rule**, which states that the plastic flow is associated with the single active yield criterion that maximizes the dissipation. A non-unique flow direction can still occur, but only in the degenerate case where the stress vector $\boldsymbol{\sigma}^\star$ is such that two or more face normals result in the same maximum dissipation rate [@problem_id:2674198]. This provides a robust and thermodynamically consistent method for handling the complexities of non-smooth yield surfaces.