## Introduction
In the field of [computational geomechanics](@entry_id:747617), predicting the complex behavior of materials like soils and rocks is a central challenge. Cap plasticity models provide a powerful theoretical framework to achieve this, capturing the intricate interplay between pressure, shear stress, and volume change that defines these materials. Simpler [constitutive models](@entry_id:174726) often fail to account for critical phenomena such as pressure-dependent strength, irreversible compaction under load, and the memory of past stress history. Cap plasticity was developed to address this knowledge gap, offering a unified approach to model these essential features.

This article provides a graduate-level exploration of [cap plasticity](@entry_id:747120), guiding you from fundamental theory to practical application. In the first chapter, **Principles and Mechanisms**, we will deconstruct the model into its core components, including the representation of stress, the definition of the composite yield surface, the [plastic flow rule](@entry_id:189597), and the [hardening law](@entry_id:750150). Next, in **Applications and Interdisciplinary Connections**, we will see how this framework is applied to solve real-world problems in geotechnical engineering, used in advanced numerical simulations, and connected to diverse fields like planetary science and [chemo-mechanics](@entry_id:191304). Finally, the **Hands-On Practices** section will allow you to solidify your understanding by working through targeted problems on key concepts.

## Principles and Mechanisms

The mechanical behavior of [geomaterials](@entry_id:749838) such as soils and rocks is characterized by complex phenomena including pressure-dependent shear strength, irreversible [compaction](@entry_id:267261), and shear-induced volume change ([dilatancy](@entry_id:201001)). Cap plasticity models provide a comprehensive theoretical framework to capture these essential features within the theory of continuum [elastoplasticity](@entry_id:193198). This chapter elucidates the fundamental principles and constitutive mechanisms that form the basis of modern [cap plasticity](@entry_id:747120) formulations, progressing from the representation of stress to the complete system of equations governing plastic evolution.

### The Language of Description: Stress Invariant Space

To formulate a [constitutive model](@entry_id:747751) that is independent of the observer's coordinate system, the mechanical response of an [isotropic material](@entry_id:204616) must be expressed in terms of quantities that are invariant under coordinate rotations. For the Cauchy stress tensor $\boldsymbol{\sigma}$, this is achieved by using its invariants. In [cap plasticity](@entry_id:747120), it is standard practice to decompose the stress tensor into its volumetric (or hydrostatic) and deviatoric (or shear) components.

The **[mean effective stress](@entry_id:751815)**, $p$, represents the hydrostatic part of the stress state. It is defined as one-third of the first invariant of the stress tensor, $I_1 = \text{tr}(\boldsymbol{\sigma})$. In [geomechanics](@entry_id:175967), it is conventional to adopt a compression-positive sign convention. Thus, we have:

$p = \frac{1}{3} \text{tr}(\boldsymbol{\sigma}) = \frac{1}{3}(\sigma_{11} + \sigma_{22} + \sigma_{33})$

where $\sigma_{11}, \sigma_{22}, \sigma_{33}$ are the normal stress components. In terms of principal stresses $(\sigma_1, \sigma_2, \sigma_3)$, this is $p = \frac{1}{3}(\sigma_1 + \sigma_2 + \sigma_3)$.

The **[deviatoric stress tensor](@entry_id:267642)**, $\boldsymbol{s}$, represents the part of the stress state that causes distortion or shear deformation. It is defined as:

$\boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I}$

where $\boldsymbol{I}$ is the second-order identity tensor. A key property of the [deviatoric stress](@entry_id:163323) is that its trace is zero, $\text{tr}(\boldsymbol{s}) = 0$.

To represent the magnitude of the deviatoric stress with a single scalar value, we use an invariant of $\boldsymbol{s}$. The second invariant of [deviatoric stress](@entry_id:163323), $J_2$, is commonly used:

$J_2 = \frac{1}{2} \text{tr}(\boldsymbol{s}^2) = \frac{1}{2} s_{ij}s_{ij}$

In terms of principal stresses, this becomes $J_2 = \frac{1}{6}[(\sigma_1 - \sigma_2)^2 + (\sigma_2 - \sigma_3)^2 + (\sigma_3 - \sigma_1)^2]$. From $J_2$, a general measure of deviatoric stress, often called the **equivalent shear stress** or **von Mises [equivalent stress](@entry_id:749064)**, is defined as:

$q = \sqrt{3J_2}$

The pair of invariants $(p, q)$ forms a convenient two-dimensional space for representing the stress state. For an isotropic material whose yield behavior is assumed to be independent of the third deviatoric invariant $J_3 = \det(\boldsymbol{s})$, the entire mechanical response can be projected onto and fully described within the $p-q$ plane. This assumption implies that the [yield surface](@entry_id:175331) has a circular cross-section in the deviatoric plane (the $\pi$-plane), which simplifies the model while remaining sufficiently accurate for many applications. Even for models that do depend on $J_3$ (i.e., exhibit Lode angle dependence), the $p-q$ plane provides a useful meridional representation, which becomes exact for axisymmetric stress states (where $\sigma_2 = \sigma_3$) .

### The Yield Surface: Bounding the Elastic Domain

The boundary between reversible (elastic) and irreversible (plastic) deformation is defined by a **[yield surface](@entry_id:175331)** in stress space. For a rate-independent material, the stress state must always remain on or within this surface. This condition is expressed by a **yield function**, $f(\boldsymbol{\sigma}, \kappa)$, where $\kappa$ represents a set of [internal state variables](@entry_id:750754) (hardening variables) that describe the history of [plastic deformation](@entry_id:139726). The admissible stress states satisfy the inequality:

$f(\boldsymbol{\sigma}, \kappa) \le 0$

A key feature of [geomaterials](@entry_id:749838) is that they can fail in shear or compact under [hydrostatic pressure](@entry_id:141627). Cap plasticity models are designed to capture this dual behavior by employing a composite yield surface, typically consisting of a shear failure surface and a [compaction](@entry_id:267261) cap.

#### The Compaction Cap

The "cap" is the part of the [yield surface](@entry_id:175331) that bounds the elastic domain at high mean stresses. Its primary function is to model the phenomenon of irreversible volumetric compaction that occurs when a soil is compressed beyond its previous maximum stress level. A common and effective choice for the cap is an ellipse in the $p-q$ plane, symmetric about the $p$-axis. The general equation for such an elliptical cap can be constructed from its geometric properties .

Consider an ellipse centered at $(p_c, 0)$ on the $p$-axis. The parameter $p_c$ is the **[preconsolidation pressure](@entry_id:203717)**, a critical hardening variable that represents the maximum [mean stress](@entry_id:751819) the material has experienced. The size of the ellipse is often scaled by $p_c$. If the semi-axis in the $q$-direction is $M$ and the semi-axis in the $p$-direction is $R p_c$, where $R$ is a dimensionless [aspect ratio](@entry_id:177707), the [yield function](@entry_id:167970) for the cap can be written as:

$f_c(p, q, p_c) = \left(\frac{q}{M}\right)^2 + \left(\frac{p - p_c}{R p_c}\right)^2 - 1 = 0$

Here, $M$ defines the deviatoric "height" of the cap, and $R$ controls its aspect ratio. As the material undergoes plastic compaction, $p_c$ increases, causing the cap to expand along the $p$-axis. This expansion represents [material hardening](@entry_id:175896).

#### Composite Surfaces and Smooth Transitions

The complete [yield surface](@entry_id:175331) is formed by combining the cap surface (e.g., an ellipse) with a shear failure surface (e.g., a Drucker-Prager or Mohr-Coulomb criterion) that bounds the elastic domain at lower mean stresses and higher shear stresses. The overall [yield criterion](@entry_id:193897) is a multi-surface criterion. For computational robustness and theoretical consistency, it is desirable that the composite surface be smooth, particularly at the junction where the cap and shear surfaces meet.

A smooth transition is achieved by enforcing a [tangency condition](@entry_id:173083) at the intersection point $(p^*, q^*)$ in the $p-q$ plane. This requires that at this point, the slopes of the two surfaces are identical, or equivalently, their normal vectors are collinear. By imposing this geometric constraint, a relationship is established between the parameters of the cap and shear surfaces, ensuring the existence of a continuously varying outward normal across the entire yield boundary. This is not merely a geometric convenience; it is essential for numerical algorithms that rely on the gradient of the yield function to determine the direction of [plastic flow](@entry_id:201346) . For models with sharp corners, special numerical treatments are required, or the corner may be regularized by replacing it with a smooth blending surface to ensure a unique [normal vector](@entry_id:264185) exists everywhere .

### Plastic Flow: The Evolution of Irreversible Strain

When the stress state reaches the yield surface and loading continues, [plastic deformation](@entry_id:139726) occurs. The evolution of the plastic strain tensor, $\boldsymbol{\varepsilon}^p$, is governed by a **[flow rule](@entry_id:177163)**.

#### The Flow Rule and Plastic Potential

The direction of plastic strain increment is assumed to be normal to a second surface in [stress space](@entry_id:199156), known as the **[plastic potential](@entry_id:164680)**, $g(\boldsymbol{\sigma})$. The general form of the [flow rule](@entry_id:177163) is:

$\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}}$

where $\dot{\lambda} \ge 0$ is the **[plastic multiplier](@entry_id:753519)**, a scalar rate-like variable that determines the magnitude of the plastic strain increment. Plastic flow occurs only when $\dot{\lambda} > 0$.

A crucial distinction is made based on the choice of the [plastic potential](@entry_id:164680) $g$:
- **Associated Flow Rule**: If the [plastic potential](@entry_id:164680) is chosen to be the same as the [yield function](@entry_id:167970) ($g = f$), the [flow rule](@entry_id:177163) is termed **associated**. In this case, the plastic strain increment is normal to the yield surface. Associated plasticity has a strong theoretical basis in Drucker's stability postulate and guarantees non-negative [plastic dissipation](@entry_id:201273) for convex yield surfaces.
- **Non-Associated Flow Rule**: If the [plastic potential](@entry_id:164680) is different from the yield function ($g \neq f$), the [flow rule](@entry_id:177163) is **non-associated**. This provides additional flexibility to model material behavior more accurately. For many [geomaterials](@entry_id:749838), an [associated flow rule](@entry_id:201731) overestimates the amount of shear-induced volume change (dilatancy). A non-associated rule allows the modeler to decouple the plastic flow direction from the yield criterion, providing a more realistic prediction of volumetric strains without altering the predicted material strength .

#### Control of Dilatancy

The power of the [plastic potential](@entry_id:164680) concept is evident in its control over dilatancy. By applying the chain rule to the [flow rule](@entry_id:177163), it can be shown that the rates of plastic volumetric strain, $\dot{\varepsilon}_v^p = \text{tr}(\dot{\boldsymbol{\varepsilon}}^p)$, and equivalent plastic [shear strain](@entry_id:175241), $\dot{\varepsilon}_s^p$, are given by:

$\dot{\varepsilon}_v^p = \dot{\lambda} \frac{\partial g}{\partial p}$

$\dot{\varepsilon}_s^p = \dot{\lambda} \frac{\partial g}{\partial q}$

The ratio of these two quantities, known as the **dilatancy rate**, $\psi$, is:

$\psi = \frac{\dot{\varepsilon}_v^p}{\dot{\varepsilon}_s^p} = \frac{\partial g / \partial p}{\partial g / \partial q}$

This equation demonstrates that the [dilatancy](@entry_id:201001) is directly controlled by the slope of the [plastic potential](@entry_id:164680) surface in the $p-q$ plane. A positive value of $\partial g / \partial p$ corresponds to plastic compaction (volume decrease, as per the compression-positive convention), while a negative value corresponds to plastic dilation (volume increase) . By choosing a [plastic potential](@entry_id:164680) $g$ with a shape different from the [yield surface](@entry_id:175331) $f$, one can independently calibrate the model's predicted strength and its dilatant behavior. For instance, setting $\partial g / \partial p = 0$ along a shear failure line results in purely isochoric (constant volume) [plastic flow](@entry_id:201346) during shear, a key feature of [critical state soil mechanics](@entry_id:748062) .

#### Loading, Unloading, and the Kuhn-Tucker Conditions

The activation of [plastic flow](@entry_id:201346) is governed by a set of logical conditions known as the **Kuhn-Tucker (KKT) complementarity conditions**. These form the mathematical basis for distinguishing between elastic and plastic behavior in numerical algorithms . For a [yield function](@entry_id:167970) $f$ and a [plastic multiplier](@entry_id:753519) rate $\dot{\lambda}$, these conditions are:

1.  **Admissibility**: $f(\boldsymbol{\sigma}, \kappa) \le 0$
2.  **Non-negativity**: $\dot{\lambda} \ge 0$
3.  **Complementarity**: $\dot{\lambda} f(\boldsymbol{\sigma}, \kappa) = 0$

The condition $\dot{\lambda} \ge 0$ is a statement of the second law of thermodynamics, ensuring that plastic deformation is an irreversible, dissipative process. The [complementarity condition](@entry_id:747558) $\dot{\lambda}f=0$ elegantly encodes the loading/unloading logic:
- If the stress state is strictly inside the [yield surface](@entry_id:175331) ($f  0$), then complementarity requires that $\dot{\lambda} = 0$. No plastic flow occurs, and the response is purely **elastic**.
- If plastic flow occurs ($\dot{\lambda} > 0$), then complementarity requires that $f = 0$. The stress state must lie on the [yield surface](@entry_id:175331). This is the state of **[plastic loading](@entry_id:753518)**.
- It is also possible to have a state on the yield surface ($f=0$) with no [plastic flow](@entry_id:201346) ($\dot{\lambda}=0$). This is known as **neutral loading**.

### Hardening: The Evolution of the Yield Surface

As a material deforms plastically, its internal structure evolves, leading to a change in its subsequent mechanical response. This phenomenon is modeled through **hardening** (or softening), which corresponds to the evolution of the yield surface. In cap models, the primary hardening mechanism is the expansion of the cap due to plastic [compaction](@entry_id:267261).

This evolution is mathematically described by a **[hardening law](@entry_id:750150)**, which relates the rate of change of the hardening variable, $\dot{\kappa}$, to the plastic flow. For a [cap model](@entry_id:201886) where the [preconsolidation pressure](@entry_id:203717) $p_c$ is the hardening variable, the law typically takes the form:

$\dot{p}_c = h(p, q, p_c) \dot{\lambda}$

where $h$ is the hardening function. Since cap expansion is driven by plastic volume change, it is natural to relate the evolution of $p_c$ to the plastic volumetric strain, $\varepsilon_v^p$. A widely used [hardening law](@entry_id:750150), derived from the principles of Critical State Soil Mechanics, takes an exponential form :

$p_c = p_{c0} \exp\left(\frac{\varepsilon_v^p}{\lambda - \kappa_{el}}\right)$

where $p_{c0}$ is the initial [preconsolidation pressure](@entry_id:203717), and $\lambda$ and $\kappa_{el}$ are the compression and swelling indices of the soil, respectively.

The sensitivity of the cap size to plastic straining is captured by the **volumetric plastic hardening modulus**, which is the derivative of $p_c$ with respect to $\varepsilon_v^p$. For the exponential law above, this modulus is:

$\frac{dp_c}{d\varepsilon_v^p} = \frac{p_c}{\lambda - \kappa_{el}}$

This simple but powerful result shows that the rate of hardening is proportional to the current size of the cap ($p_c$) and inversely proportional to the plastic [compressibility](@entry_id:144559) index ($\lambda - \kappa_{el}$). A more compressible soil (larger $\lambda - \kappa_{el}$) requires more plastic [compaction](@entry_id:267261) to achieve the same increase in strength, thus hardening more slowly .

### The Complete Constitutive System and Its Numerical Implementation

The principles of elasticity, plasticity, and hardening are integrated into a complete system of equations that can be solved in a computational setting. During continuous [plastic loading](@entry_id:753518), the stress state must remain on the evolving [yield surface](@entry_id:175331). This enforces the **consistency condition**, $\dot{f}=0$. Expanding this with the chain rule gives:

$\dot{f} = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \dot{\boldsymbol{\sigma}} + \frac{\partial f}{\partial p_c} \dot{p}_c = 0$

This equation is the linchpin of [rate-independent plasticity](@entry_id:754082) theory. By substituting the elastic stress-strain relation ($\dot{\boldsymbol{\sigma}} = \mathbb{C}^e:(\dot{\boldsymbol{\varepsilon}}-\dot{\boldsymbol{\varepsilon}}^p)$), the [flow rule](@entry_id:177163), and the [hardening law](@entry_id:750150) into the [consistency condition](@entry_id:198045), one can solve for the unknown [plastic multiplier](@entry_id:753519) rate $\dot{\lambda}$ in terms of the total [strain rate](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}$ and the current state. This yields the full [elastoplastic tangent modulus](@entry_id:189492) and governs the evolution of the system .

In computational mechanics, where solutions are advanced in [discrete time](@entry_id:637509) (or load) steps, the continuous theory is implemented via a numerical integration scheme, most commonly the **[return mapping algorithm](@entry_id:173819)**. This algorithm is an [elastic predictor-plastic corrector](@entry_id:748860) procedure:

1.  **Elastic Predictor**: For a given total strain increment $\Delta \boldsymbol{\varepsilon}$, a "trial" stress state $(\boldsymbol{\sigma}^{\text{tr}})$ is computed by assuming the response is purely elastic: $\boldsymbol{\sigma}^{\text{tr}} = \boldsymbol{\sigma}^n + \mathbb{C}^e : \Delta\boldsymbol{\varepsilon}$.
2.  **Yield Check**: The trial stress is checked against the yield condition: $f(\boldsymbol{\sigma}^{\text{tr}}, \kappa^n) \le 0$. If satisfied, the step is elastic, and the final state is the trial state.
3.  **Plastic Corrector**: If $f(\boldsymbol{\sigma}^{\text{tr}}, \kappa^n)  0$, the trial state is inadmissible. Plastic deformation must have occurred. The final stress state $\boldsymbol{\sigma}^{n+1}$ must be "returned" to the updated [yield surface](@entry_id:175331). For associative plasticity, this return path is a **[closest-point projection](@entry_id:168047)** of the trial stress onto the [yield surface](@entry_id:175331), measured in a norm defined by the [elastic moduli](@entry_id:171361).

This projection leads to a system of algebraic equations for the updated state $(p^{n+1}, q^{n+1}, \kappa^{n+1})$ in terms of the unknown [plastic multiplier](@entry_id:753519) increment, $\Delta\lambda$:

$p^{n+1} = p^{\text{tr}} - K \Delta\lambda \frac{\partial g}{\partial p}$

$q^{n+1} = q^{\text{tr}} - 3G \Delta\lambda \frac{\partial g}{\partial q}$

$\kappa^{n+1} = \kappa^{n} + \Delta\lambda \frac{\partial g}{\partial p}$

The entire system is closed by substituting these expressions into the final consistency condition, $f(p^{n+1}, q^{n+1}, \kappa^{n+1}) = 0$. This results in a single, non-linear scalar equation for the single unknown $\Delta\lambda$. Solving this equation (typically with a Newton-Raphson scheme) determines the magnitude of the plastic increment, and thus the final state of the material at the end of the step .