## Introduction
In the field of [computational mechanics](@entry_id:174464), accurately predicting a material's response to loading is paramount. A critical aspect of this is understanding the transition from reversible elastic deformation to permanent plastic deformation. This transition is governed by [yield criteria](@entry_id:178101), which form the mathematical and physical foundation of [plasticity theory](@entry_id:177023). These models define the boundary of elasticity in stress space, providing the essential rules for simulating everything from [metal forming](@entry_id:188560) to geotechnical stability. This article addresses the need for a cohesive understanding of the most prevalent [yield criteria](@entry_id:178101) used in engineering analysis.

This article provides a comprehensive exploration of four key yield models. The first chapter, **Principles and Mechanisms**, delves into the theoretical underpinnings, explaining how [stress invariants](@entry_id:170526) are used to build objective models and distinguishing between pressure-independent criteria like Tresca and von Mises, ideal for metals, and pressure-sensitive criteria like Drucker-Prager and Modified Cam-Clay, crucial for [geomaterials](@entry_id:749838). The second chapter, **Applications and Interdisciplinary Connections**, bridges theory and practice by demonstrating how these models are calibrated and applied in fields like geotechnical and [structural engineering](@entry_id:152273), with a focus on their implementation within the Finite Element Method. Finally, the **Hands-On Practices** section offers practical exercises for calculating key parameters and understanding the [numerical algorithms](@entry_id:752770) that bring these theories to life.

## Principles and Mechanisms

The transition of a material from elastic to plastic behavior is governed by a yield criterion, which defines the boundary of the elastic domain in stress space. This boundary is known as the **yield surface**. For a material to deform plastically, its stress state must reach and then attempt to move beyond this surface. The principles governing the mathematical formulation of these surfaces and the subsequent plastic flow are fundamental to [computational plasticity](@entry_id:171377).

### The Role of Stress Invariants in Isotropic Plasticity

A core tenet of [continuum mechanics](@entry_id:155125) is the principle of **[material frame-indifference](@entry_id:178419)**, which asserts that constitutive laws must be independent of the observer's reference frame. For an [isotropic material](@entry_id:204616), whose properties are the same in all directions, this implies that the yield criterion cannot depend on the orientation of the coordinate system used to describe the stress state. Consequently, the [yield function](@entry_id:167970), denoted as $f(\boldsymbol{\sigma})$, must be expressed in terms of quantities that are invariant under orthogonal [coordinate transformations](@entry_id:172727). The most fundamental set of such quantities are the scalar **invariants of the Cauchy stress tensor** $\boldsymbol{\sigma}$.

Any symmetric second-order tensor, including $\boldsymbol{\sigma}$, is fully characterized by its three [principal stresses](@entry_id:176761), $\sigma_1, \sigma_2, \sigma_3$, which are the eigenvalues of the tensor. While the components of $\boldsymbol{\sigma}$ change with the coordinate system, its [principal values](@entry_id:189577) do not. Therefore, any function of only the principal stresses, $f(\sigma_1, \sigma_2, \sigma_3)$, is inherently frame-indifferent.

For analytical and computational convenience, it is often more practical to work with a different set of invariants derived from the tensor components. A critical step is the decomposition of the stress tensor into two parts with distinct physical interpretations: a **hydrostatic** component responsible for volume changes and a **deviatoric** component responsible for shape changes (distortion). This decomposition is expressed as:

$$
\boldsymbol{\sigma} = p\boldsymbol{I} + \boldsymbol{s}
$$

Here, $\boldsymbol{I}$ is the second-order identity tensor, $p$ is the **mean stress** (or hydrostatic stress), and $\boldsymbol{s}$ is the **[deviatoric stress tensor](@entry_id:267642)**. The mean stress is defined as one-third of the trace of the stress tensor:

$$
p = \frac{1}{3} \text{tr}(\boldsymbol{\sigma}) = \frac{1}{3}(\sigma_{11} + \sigma_{22} + \sigma_{33})
$$

The [trace of a tensor](@entry_id:190669) is its first principal invariant, often denoted $I_1 = \text{tr}(\boldsymbol{\sigma})$, so $p = I_1/3$. The [deviatoric stress](@entry_id:163323) is then what remains: $\boldsymbol{s} = \boldsymbol{\sigma} - \frac{1}{3}I_1\boldsymbol{I}$. A key property of the [deviatoric stress tensor](@entry_id:267642) is that its trace is always zero, reflecting its role in pure distortion without volume change.

Using this decomposition, the standard set of invariants used in [plasticity theory](@entry_id:177023) for [isotropic materials](@entry_id:170678) is constructed. These are scalar quantities that remain unchanged when the stress tensor is transformed to a new basis by an orthogonal tensor $\boldsymbol{Q}$ (i.e., $\boldsymbol{\sigma}' = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}$). The three fundamental invariants are [@problem_id:2612486]:

1.  **The first invariant of the stress tensor, $I_1$**:
    $$I_1 = \text{tr}(\boldsymbol{\sigma})$$
    This invariant is directly related to the mean stress and governs the hydrostatic component of the stress state.

2.  **The second invariant of the [deviatoric stress tensor](@entry_id:267642), $J_2$**:
    $$J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s} = \frac{1}{2}s_{ij}s_{ij}$$
    where ':' denotes the Frobenius inner product of two tensors. $J_2$ quantifies the magnitude of the deviatoric stress, or the intensity of distortional stress. It is a measure of the [elastic strain energy](@entry_id:202243) of distortion.

3.  **The third invariant of the [deviatoric stress tensor](@entry_id:267642), $J_3$**:
    $$J_3 = \det(\boldsymbol{s})$$
    $J_3$ is related to the "type" of deviatoric stress state, often characterized by the **Lode angle**, which distinguishes between stress states like triaxial compression, pure shear, and triaxial extension, even if they have the same $I_1$ and $J_2$.

The invariance of $I_1$, $J_2$, and $J_3$ under any [orthogonal transformation](@entry_id:155650) $\boldsymbol{Q}$ (where $\boldsymbol{Q}\boldsymbol{Q}^{\mathsf{T}}=\boldsymbol{I}$ and $\det(\boldsymbol{Q})=\pm 1$) stems from the fundamental properties of the trace, determinant, and Frobenius product operations [@problem_id:2612486]. By formulating [yield criteria](@entry_id:178101) in terms of these invariants, we ensure the material model is objective and respects isotropy.

### Yield Criteria for Pressure-Independent Materials

For many [crystalline materials](@entry_id:157810), such as ductile metals, plastic deformation is primarily driven by dislocation slip, a shearing mechanism that is largely unaffected by [hydrostatic pressure](@entry_id:141627). Yield criteria for these materials are therefore formulated to be independent of the mean stress $p$ (and thus $I_1$), depending only on the [deviatoric stress](@entry_id:163323) invariants, typically $J_2$ and sometimes $J_3$.

#### The Von Mises Yield Criterion

The **von Mises criterion**, also known as the $J_2$ plasticity or maximum [distortion energy](@entry_id:198925) criterion, is a smooth and mathematically convenient model that provides excellent agreement with experimental data for many ductile metals. It postulates that yielding occurs when the second invariant of the deviatoric stress, $J_2$, reaches a critical value. The [yield function](@entry_id:167970) is commonly written as:

$$
f(\boldsymbol{\sigma}, \sigma_y) = \sqrt{3J_2} - \sigma_y = 0
$$

Here, $\sigma_y$ is the uniaxial yield stress of the material, which may be a constant (for [perfect plasticity](@entry_id:753335)) or a function of [plastic work](@entry_id:193085) (for hardening). The quantity $\sigma_{eq} = \sqrt{3J_2}$ is known as the **von Mises [equivalent stress](@entry_id:749064)**. This formulation ensures that in a simple [uniaxial tension test](@entry_id:195375) ($\boldsymbol{\sigma}$ has only one non-zero component $\sigma_{11}$), yielding occurs when $\sigma_{11} = \sigma_y$.

Because the von Mises criterion depends only on $J_2$, it is completely independent of hydrostatic pressure [@problem_id:2612510]. A purely [hydrostatic stress](@entry_id:186327) state ($\boldsymbol{s}=\boldsymbol{0}$, so $J_2=0$) can never cause yielding in a von Mises material. Geometrically, the [yield surface](@entry_id:175331) is an infinite cylinder in [principal stress space](@entry_id:184388), with its axis aligned with the hydrostatic line ($\sigma_1=\sigma_2=\sigma_3$). The intersection of this cylinder with the **deviatoric plane** (also called the $\pi$-plane), which is a plane perpendicular to the hydrostatic axis, is a circle [@problem_id:2612460]. The radius of this circle in the space of principal deviatoric stresses $(s_1, s_2, s_3)$ is $\sqrt{2J_2}$.

#### The Tresca Yield Criterion

The **Tresca criterion** is based on a more direct physical hypothesis: that yielding begins when the maximum shear stress at any point reaches a critical value. The maximum shear stress in a material is given by half the difference between the largest and smallest [principal stresses](@entry_id:176761). With principal stresses ordered as $\sigma_1 \ge \sigma_2 \ge \sigma_3$, the Tresca [yield function](@entry_id:167970) is:

$$
f(\boldsymbol{\sigma}, k) = \frac{\sigma_1 - \sigma_3}{2} - k = 0
$$

Here, $k$ is the material's yield stress in pure shear. We can relate $k$ to the uniaxial tensile yield stress $\sigma_y$ by considering the stress state at yield in a tension test: $\sigma_1 = \sigma_y$, and $\sigma_2 = \sigma_3 = 0$. Substituting these into the yield condition gives $\frac{\sigma_y - 0}{2} = k$, so $k = \sigma_y / 2$ [@problem_id:2612537]. The [yield function](@entry_id:167970) can then be expressed in terms of the maximum difference between any two principal stresses:

$$
f(\boldsymbol{\sigma}, \sigma_y) = \max(|\sigma_1-\sigma_2|, |\sigma_2-\sigma_3|, |\sigma_3-\sigma_1|) - \sigma_y = 0
$$

Like the von Mises criterion, the Tresca criterion is independent of hydrostatic pressure because $\sigma_i - \sigma_j = s_i - s_j$. In the deviatoric plane, the Tresca yield surface is a **regular hexagon** [@problem_id:2612460]. This hexagon is inscribed within the von Mises circle, touching it at the vertices corresponding to pure shear states. The ratio of the circumscribed radius (distance to a vertex) to the inscribed radius (distance to the middle of a side) of this hexagon is $2/\sqrt{3} \approx 1.155$ [@problem_id:2612460]. This geometric difference means the two criteria predict slightly different yield points, with Tresca being more conservative for most multiaxial stress states. The corners of the Tresca hexagon introduce non-smoothness into the [yield function](@entry_id:167970), which requires special treatment in numerical algorithms [@problem_id:2612497].

### The Plastic Flow Rule and Hardening Mechanisms

A [yield criterion](@entry_id:193897) defines the onset of plasticity, but a complete model must also specify the evolution of plastic strain once yielding occurs. This is governed by a **[flow rule](@entry_id:177163)**, which dictates the direction of the plastic [strain rate tensor](@entry_id:198281) $\dot{\boldsymbol{\varepsilon}}^p$. A general form of the [flow rule](@entry_id:177163) is:

$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$

where $\dot{\lambda} \ge 0$ is the **[plastic multiplier](@entry_id:753519)**, a scalar rate parameter that is non-zero only during [plastic loading](@entry_id:753518), and $g(\boldsymbol{\sigma})$ is a scalar function known as the **[plastic potential](@entry_id:164680)**. The gradient $\partial g / \partial \boldsymbol{\sigma}$ defines a direction normal to the [level surfaces](@entry_id:196027) of $g$ in [stress space](@entry_id:199156).

If the [plastic potential](@entry_id:164680) is chosen to be the same as the [yield function](@entry_id:167970) ($g=f$), the flow is termed **associative**. In this case, the plastic strain rate vector is normal to the yield surface itself. If $g \neq f$, the flow is **non-associative**.

For the von Mises criterion, an [associative flow rule](@entry_id:163391) is almost always used. The gradient of the [yield function](@entry_id:167970) $f = \sqrt{3J_2} - \sigma_y$ is:

$$
\frac{\partial f}{\partial \boldsymbol{\sigma}} = \frac{\partial \sqrt{3J_2}}{\partial \boldsymbol{\sigma}} = \frac{3}{2\sqrt{3J_2}}\frac{\partial J_2}{\partial \boldsymbol{\sigma}} = \frac{3}{2q}\boldsymbol{s}
$$

where $q = \sqrt{3J_2}$ is the von Mises [equivalent stress](@entry_id:749064) [@problem_id:2612467]. Since the flow direction is proportional to the [deviatoric stress tensor](@entry_id:267642) $\boldsymbol{s}$, it is itself purely deviatoric. This has a profound physical consequence: the volumetric part of the plastic [strain rate](@entry_id:154778) is zero.

$$
\text{tr}(\dot{\boldsymbol{\varepsilon}}^p) = \dot{\lambda} \cdot \text{tr}\left(\frac{3}{2q}\boldsymbol{s}\right) = \frac{3\dot{\lambda}}{2q} \cdot \text{tr}(\boldsymbol{s}) = 0
$$

This demonstrates that associative $J_2$ plasticity predicts incompressible, or **isochoric**, [plastic flow](@entry_id:201346) [@problem_id:2612467, @problem_id:2612510].

The [yield surface](@entry_id:175331) is not necessarily static. **Hardening** (or softening) describes the evolution of the [yield surface](@entry_id:175331) with ongoing plastic deformation. In **[isotropic hardening](@entry_id:164486)**, the yield surface expands uniformly, maintaining its shape and center. This is modeled by making the [yield strength](@entry_id:162154) a function of a scalar internal variable, $\kappa$, which typically measures the accumulated plastic strain. For the von Mises model, this would be $f(\boldsymbol{\sigma}, \kappa) = \sqrt{3J_2} - \sigma_y(\kappa)$. As $\kappa$ increases, $\sigma_y$ increases, and the elastic domain grows [@problem_id:2612510]. Isotropic hardening is appropriate for monotonic loading but cannot capture phenomena like the **Bauschinger effect** (reduced [yield strength](@entry_id:162154) upon load reversal), which requires more complex models like [kinematic hardening](@entry_id:172077) where the [yield surface](@entry_id:175331) translates in [stress space](@entry_id:199156).

The entire elastoplastic process is governed by a set of constraints known as the **Karush-Kuhn-Tucker (KKT) conditions**:
1.  **Admissibility**: $f(\boldsymbol{\sigma}, \kappa) \le 0$ (The stress state must be inside or on the yield surface).
2.  **Non-negative plastic flow**: $\dot{\lambda} \ge 0$.
3.  **Complementarity**: $\dot{\lambda} f(\boldsymbol{\sigma}, \kappa) = 0$.

These conditions elegantly state that plastic flow ($\dot{\lambda} > 0$) can only occur when the stress state is precisely on the [yield surface](@entry_id:175331) ($f=0$). If the state is strictly elastic ($f  0$), no [plastic flow](@entry_id:201346) occurs ($\dot{\lambda}=0$) [@problem_id:2612497].

### Yield Criteria for Pressure-Sensitive Materials

For [geomaterials](@entry_id:749838) like soils, rocks, and concrete, mechanical strength and stiffness are strongly dependent on the confining pressure. An increase in hydrostatic compression generally increases the material's [shear strength](@entry_id:754762). Yield criteria for these materials must therefore be **pressure-sensitive**, meaning their yield functions depend on both the first stress invariant $I_1$ (or mean stress $p$) and a deviatoric invariant like $J_2$.

#### The Drucker-Prager Criterion

The **Drucker-Prager criterion** is the simplest extension of the von Mises model to include pressure sensitivity. It defines a smooth conical yield surface in [principal stress space](@entry_id:184388). A common form of the [yield function](@entry_id:167970) is:

$$
f(\boldsymbol{\sigma}) = \alpha I_1 + \sqrt{J_2} - k = 0
$$

where $\alpha$ and $k$ are positive material constants.
*   The parameter $\alpha$ controls the **pressure sensitivity**. A larger $\alpha$ means the material's [shear strength](@entry_id:754762) (related to $\sqrt{J_2}$) increases more rapidly with hydrostatic compression (as $I_1$ becomes more negative).
*   The parameter $k$ represents the material's **cohesion**, defining the yield strength in pure shear ($I_1=0$). For a cohesionless material like dry sand, $k$ can be zero, and the yield cone passes through the origin of the stress space [@problem_id:2612468].

This criterion is often used as a smooth approximation to the non-smooth Mohr-Coulomb criterion. The parameters $\alpha$ and $k$ can be calibrated by matching the Drucker-Prager line to the Mohr-Coulomb envelope in the $p-q$ plane, where $q = \sqrt{3J_2}$ and $p=-I_1/3$ (using a compression-positive convention for $p$). Because the Mohr-Coulomb surface is irregular in the deviatoric plane (a hexagon), different calibrations are obtained depending on whether the matching is performed for triaxial compression or triaxial extension stress states [@problem_id:2612468].

A critical feature of models for [geomaterials](@entry_id:749838) is the choice between associative and non-associative flow. For a Drucker-Prager model, an [associative flow rule](@entry_id:163391) predicts a plastic [volumetric strain rate](@entry_id:272471) (dilatancy) that is often much larger than observed in experiments. To overcome this, a **non-associative** model is commonly used, where the [plastic potential](@entry_id:164680) $g$ has a different form from the yield function $f$:

$$
f = \alpha I_1 + \sqrt{J_2} - k \quad \text{and} \quad g = \alpha_g I_1 + \sqrt{J_2}
$$

The plastic [volumetric strain](@entry_id:267252) increment, $d\varepsilon_v^p = \text{tr}(d\boldsymbol{\varepsilon}^p)$, can be shown to be $d\varepsilon_v^p = 3\alpha_g d\lambda$ [@problem_id:2612502]. This demonstrates that the amount of plastic dilation or compaction is controlled by the parameter $\alpha_g$ from the [potential function](@entry_id:268662), independent of the pressure sensitivity parameter $\alpha$ from the [yield function](@entry_id:167970). Choosing $\alpha_g  \alpha$ allows for a realistic prediction of both strength and plastic volume change. This flexibility comes at a computational cost: a non-[associative flow rule](@entry_id:163391) generally results in an **unsymmetric consistent elastoplastic tangent matrix**, requiring more computationally expensive solvers in implicit [finite element analysis](@entry_id:138109) [@problem_id:2612502].

#### The Modified Cam-Clay Model

Developed within the framework of **Critical State Soil Mechanics (CSSM)**, the **Modified Cam-Clay (MCC)** model is a more sophisticated elastoplastic model for normally consolidated or lightly over-consolidated clays. It provides a unified framework for describing compression, [shear deformation](@entry_id:170920), and the coupling between them.

The MCC yield surface is an ellipse in the $p'-q$ plane (where $p'$ is the mean *effective* stress and $q$ is the von Mises [equivalent stress](@entry_id:749064)). Its equation is:

$$
f(p', q, p'_c) = \frac{q^2}{M^2} + p'(p' - p'_c) = 0
$$

The key variables are:
*   $M$: A material constant representing the slope of the **[critical state line](@entry_id:748061)** in the $p'-q$ plane.
*   $p'_c$: The **[preconsolidation pressure](@entry_id:203717)**, which acts as the sole [isotropic hardening](@entry_id:164486) variable. It defines the current size of the yield ellipse.

The hardening mechanism in MCC is directly linked to plastic [volumetric strain](@entry_id:267252). The size of the yield ellipse, determined by $p'_c$, evolves according to the **[hardening law](@entry_id:750150)**:

$$
\frac{\mathrm{d}p'_c}{p'_c} = \frac{\mathrm{d}\varepsilon_v^p}{\lambda - \kappa}
$$

where $\lambda$ and $\kappa$ are the soil's compression and swelling indices, respectively, and $\mathrm{d}\varepsilon_v^p$ is the increment of plastic volumetric strain [@problem_id:2612534]. This law dictates that plastic [compaction](@entry_id:267261) ($\mathrm{d}\varepsilon_v^p > 0$) causes hardening ($\mathrm{d}p'_c > 0$), which corresponds to a homothetic (uniform) expansion of the yield ellipse about the origin [@problem_id:2612534].

The [associated flow rule](@entry_id:201731) for MCC provides a rich description of soil behavior. The normal to the ellipse has both horizontal and vertical components, meaning that plastic flow generally involves both shear and volumetric strains.
*   On the "wet" side of the critical state ($p'  p'_c/2$), the outward normal points towards increasing $p'$, and [plastic deformation](@entry_id:139726) is **contractive** (compactive), leading to hardening.
*   On the "dry" side ($p' > p'_c/2$), the outward normal points towards decreasing $p'$, and [plastic deformation](@entry_id:139726) is **dilative** (volume-increasing), leading to softening.
*   Precisely at the apex of the ellipse, where $p' = p'_c/2$, the normal to the [yield surface](@entry_id:175331) is vertical. Here, plastic flow is purely deviatoric ($\mathrm{d}\varepsilon_v^p=0$), and no hardening or softening occurs ($\mathrm{d}p'_c=0$). This state of steady-state shearing at constant volume and stress is the **critical state** [@problem_id:2612488].

Numerically, the MCC model presents its own challenges. Although the yield function is a smooth polynomial, its [level set](@entry_id:637056) (the ellipse) has an infinite slope at the origin ($p'=0$). This strong [geometric nonlinearity](@entry_id:169896), rather than a lack of [differentiability](@entry_id:140863), can pose difficulties for the convergence of numerical integration schemes like return-mapping algorithms [@problem_id:2612544].

### Numerical Implementation: The Return-Mapping Algorithm

In implicit finite element simulations, the enforcement of the KKT conditions over a [discrete time](@entry_id:637509) (or load) step is typically achieved using an **elastic predictor / plastic corrector** algorithm, commonly known as a **return-mapping** algorithm [@problem_id:2612497]. For a given total strain increment $\Delta\boldsymbol{\varepsilon}$ at a material point, the algorithm proceeds in two main stages:

1.  **Elastic Predictor**: An elastic "trial" stress state is computed by assuming the entire strain increment is elastic: $\boldsymbol{\sigma}_{\text{trial}} = \boldsymbol{\sigma}_n + \mathbb{C}:\Delta\boldsymbol{\varepsilon}$, where $\boldsymbol{\sigma}_n$ is the stress at the beginning of the step and $\mathbb{C}$ is the [elastic stiffness tensor](@entry_id:196425).

2.  **Plastic Corrector**: The yield function is evaluated at the trial state, $f_{\text{trial}} = f(\boldsymbol{\sigma}_{\text{trial}}, \kappa_n)$.
    *   If $f_{\text{trial}} \le 0$, the trial state is admissible. The step is declared elastic, the updated stress is $\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}_{\text{trial}}$, and the [plastic multiplier](@entry_id:753519) increment $\Delta\lambda$ is zero.
    *   If $f_{\text{trial}} > 0$, the trial state lies outside the [yield surface](@entry_id:175331) and is inadmissible. A plastic correction is necessary. This involves solving a system of nonlinear algebraic equations to find the state $(\boldsymbol{\sigma}_{n+1}, \kappa_{n+1})$ and the [plastic multiplier](@entry_id:753519) increment $\Delta\lambda > 0$ that simultaneously satisfy the discretized flow and [hardening laws](@entry_id:183802), as well as the **consistency condition** $f(\boldsymbol{\sigma}_{n+1}, \kappa_{n+1}) = 0$.

Geometrically, this correction "returns" the inadmissible trial stress point back to the [yield surface](@entry_id:175331). The direction of this return path is dictated by the [flow rule](@entry_id:177163). For von Mises, it is a simple [radial return](@entry_id:754007) in the deviatoric plane. For Drucker-Prager and Cam-Clay, it is a more complex return to a cone or an ellipse, respectively. For non-smooth criteria like Tresca, the return direction may not be unique at corners or edges, requiring more advanced methods based on [subgradient calculus](@entry_id:637686) [@problem_id:2612497]. For the global Newton-Raphson [iterative solver](@entry_id:140727) to maintain its quadratic convergence rate, it is essential to compute the **[consistent algorithmic tangent](@entry_id:166068)**, which is the exact linearization of the discrete stress update with respect to the total strain increment.