## Introduction
In the design and analysis of mechanical components, predicting the transition from elastic to permanent, plastic deformation is a critical task. For complex, multiaxial stress states, this requires a scalar measure—an **[equivalent stress](@entry_id:749064)**—to compare the loading intensity against a material's known yield strength from a simple test. This article addresses the fundamental need for such a measure by providing a deep dive into the two most prevalent [yield criteria](@entry_id:178101) for ductile metals: the von Mises and Tresca criteria.

This exploration will illuminate the core principles that differentiate these two powerful models and guide their proper application. Throughout three comprehensive chapters, you will gain a robust understanding of these foundational concepts. The first chapter, **Principles and Mechanisms**, will deconstruct the stress tensor and build the theoretical framework for both criteria from the ground up, focusing on [stress invariants](@entry_id:170526) and the physical meaning of distortion. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how these theories are applied to solve real-world engineering problems in [structural design](@entry_id:196229), fracture mechanics, and computational simulation, highlighting where the models agree and diverge. Finally, the **Hands-On Practices** chapter will bridge theory and practice, challenging you to implement and test these concepts through guided computational exercises. By progressing through these sections, you will move from foundational theory to practical mastery of [equivalent stress](@entry_id:749064) analysis.

## Principles and Mechanisms

In the study of solid mechanics, particularly in the theory of plasticity, it is essential to establish a scalar measure that quantifies the "intensity" of a multiaxial stress state and allows for comparison with a simple, canonical state, such as [uniaxial tension](@entry_id:188287). This measure, known as an **[equivalent stress](@entry_id:749064)**, forms the core of a [yield criterion](@entry_id:193897), a function that defines the boundary between elastic and plastic deformation. For ductile metals, two such criteria have achieved prominence due to their physical basis and predictive success: the von Mises and Tresca criteria. This chapter elucidates the fundamental principles and mechanics that underpin these two measures.

### Stress Decomposition: Hydrostatic and Deviatoric Components

A general state of stress at a point, represented by the symmetric Cauchy stress tensor $\boldsymbol{\sigma}$, can be uniquely decomposed into two physically distinct components: a **hydrostatic** (or volumetric) part and a **deviatoric** (or distortional) part.

The hydrostatic component represents an average [normal stress](@entry_id:184326), akin to pressure, and is defined by the **[mean stress](@entry_id:751819)** or **[hydrostatic stress](@entry_id:186327)**, $p$:
$$
p = \frac{1}{3} \mathrm{tr}(\boldsymbol{\sigma}) = \frac{1}{3} (\sigma_{11} + \sigma_{22} + \sigma_{33})
$$
where $\mathrm{tr}(\cdot)$ denotes the trace of the tensor. This component is associated with a change in volume (dilatation or compression) of the material element, without any change in shape. The hydrostatic part of the stress tensor is $p\mathbf{I}$, where $\mathbf{I}$ is the second-order identity tensor.

The remaining part of the stress tensor, known as the **[deviatoric stress tensor](@entry_id:267642)**, $\mathbf{s}$, captures the components of stress that cause distortion or change in shape ([shear deformation](@entry_id:170920)) at constant volume. It is defined as:
$$
\mathbf{s} = \boldsymbol{\sigma} - p\mathbf{I}
$$
By construction, the [deviatoric stress tensor](@entry_id:267642) is traceless, i.e., $\mathrm{tr}(\mathbf{s}) = 0$. For instance, consider the stress state given by the tensor :
$$
\boldsymbol{\sigma} = \begin{pmatrix} 120 & 30 & -10 \\ 30 & 80 & 20 \\ -10 & 20 & 50 \end{pmatrix} \, \text{MPa}
$$
The [mean stress](@entry_id:751819) is $p = \frac{1}{3}(120 + 80 + 50) = \frac{250}{3}$ MPa. The corresponding [deviatoric stress tensor](@entry_id:267642) is:
$$
\mathbf{s} = \begin{pmatrix} 120 - \frac{250}{3} & 30 & -10 \\ 30 & 80 - \frac{250}{3} & 20 \\ -10 & 20 & 50 - \frac{250}{3} \end{pmatrix} = \begin{pmatrix} \frac{110}{3} & 30 & -10 \\ 30 & -\frac{10}{3} & 20 \\ -10 & 20 & -\frac{100}{3} \end{pmatrix} \, \text{MPa}
$$
This decomposition is fundamental because the plastic deformation of ductile metals is observed to be primarily a process of distortion.

### The Principle of Pressure Insensitivity and Material Objectivity

A cornerstone of [classical plasticity theory](@entry_id:167389) for ductile metals is the experimental observation that the onset of yielding is overwhelmingly dependent on the distortional component of stress and is negligibly affected by the level of [hydrostatic stress](@entry_id:186327) . Applying a uniform [hydrostatic pressure](@entry_id:141627) to a metal specimen does not, to a very good approximation, bring it closer to or further from its [yield point](@entry_id:188474). This is the **principle of pressure insensitivity**.

This principle has a profound implication: any valid [yield criterion](@entry_id:193897) for such materials must be a function of the [deviatoric stress tensor](@entry_id:267642) $\mathbf{s}$ alone, and must be independent of the hydrostatic stress $p$. If we consider a stress state $\boldsymbol{\sigma}$ and add a purely hydrostatic component $q\mathbf{I}$ to it, creating a new state $\boldsymbol{\sigma}' = \boldsymbol{\sigma} + q\mathbf{I}$, the deviatoric part remains unchanged . The new [mean stress](@entry_id:751819) is $p' = p+q$, but the new [deviatoric tensor](@entry_id:185837) is $\mathbf{s}' = \boldsymbol{\sigma}' - p'\mathbf{I} = (\boldsymbol{\sigma} + q\mathbf{I}) - (p+q)\mathbf{I} = \boldsymbol{\sigma} - p\mathbf{I} = \mathbf{s}$. Consequently, both the von Mises and Tresca equivalent stresses, being measures of distortion, remain invariant under the addition of hydrostatic stress. This property sharply contrasts with the behavior of frictional materials like soils, rocks, or concrete, where compressive hydrostatic pressure significantly increases the material's shear strength. For these [geomaterials](@entry_id:749838), pressure-dependent criteria such as the Drucker-Prager model are required .

A second fundamental principle is that of **[material objectivity](@entry_id:177919)** or **[frame-indifference](@entry_id:197245)**. This principle states that constitutive laws must be independent of the observer's [rigid-body motion](@entry_id:265795). For a scalar measure like [equivalent stress](@entry_id:749064), this means its value must not change if the material and its stress field are subjected to a rigid rotation. Mathematically, if a stress tensor $\boldsymbol{\sigma}$ is transformed to $\boldsymbol{\sigma}' = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T$ by a [rotation tensor](@entry_id:191990) $\mathbf{Q}$, the [equivalent stress](@entry_id:749064) must be the same for both $\boldsymbol{\sigma}$ and $\boldsymbol{\sigma}'$. This is guaranteed if the [equivalent stress](@entry_id:749064) is a function of the **[principal stresses](@entry_id:176761)** (the eigenvalues of $\boldsymbol{\sigma}$), as eigenvalues are invariant under such orthogonal transformations. This invariance is a key property of both von Mises and Tresca criteria, as can be explicitly verified by computing the equivalent stresses for two different component representations of the same physical stress state  .

### Stress Invariants as a Foundation for Yield Criteria

To formalize the dependence on the deviatoric stress state in an objective manner, we turn to the scalar **invariants** of the [deviatoric stress tensor](@entry_id:267642) $\mathbf{s}$. An invariant is a quantity whose value does not change with rotations of the coordinate system. Since the yield criterion must be independent of the observer, it must be expressible as a function of these invariants. The three [principal invariants](@entry_id:193522) of $\mathbf{s}$ are:

-   The first invariant: $J_1 = \mathrm{tr}(\mathbf{s}) = 0$ (by definition).
-   The second invariant: $J_2 = \frac{1}{2} \mathrm{tr}(\mathbf{s}^2) = \frac{1}{2} \mathbf{s}:\mathbf{s} = \frac{1}{2} s_{ij}s_{ij}$. This [invariant measures](@entry_id:202044) the magnitude of the deviatoric stress.
-   The third invariant: $J_3 = \det(\mathbf{s})$. This invariant is related to the "mode" or "type" of [shear deformation](@entry_id:170920).

The pressure-insensitivity of yielding means that equivalent stresses for ductile metals must be functions of only $J_2$ and $J_3$, and independent of the first invariant of the full stress tensor, $I_1 = \mathrm{tr}(\boldsymbol{\sigma}) = 3p$ .

### The von Mises Criterion: A Measure of Distortional Energy

The **von Mises yield criterion** is motivated by the hypothesis that yielding begins when the **distortional [strain energy density](@entry_id:200085)**, $U_d$, reaches a critical value. For an isotropic linear elastic material, this energy is given by $U_d = \frac{1}{2G}J_2$, where $G$ is the [shear modulus](@entry_id:167228). The criterion is therefore equivalent to stating that yielding occurs when $J_2$ reaches a critical value.

The **von Mises [equivalent stress](@entry_id:749064)**, $\sigma_{\mathrm{vM}}$, is defined as the value of uniaxial tensile stress that produces the same distortional energy as the general multiaxial stress state. For a simple tension test with stress $\sigma_{\mathrm{vM}}$, the principal stresses are $(\sigma_{\mathrm{vM}}, 0, 0)$, and a direct calculation shows that $J_2 = \frac{1}{3}\sigma_{\mathrm{vM}}^2$. Equating this to the general expression for $J_2$, we obtain the definitive formula for the von Mises [equivalent stress](@entry_id:749064):
$$
\sigma_{\mathrm{vM}} = \sqrt{3J_2}
$$
This can be expressed in terms of the components of the [deviatoric tensor](@entry_id:185837) $\mathbf{s}$ or, more commonly, in terms of the components of the full Cauchy stress tensor $\boldsymbol{\sigma}$ :
$$
\sigma_{\mathrm{vM}} = \sqrt{\frac{1}{2}\left[ (\sigma_{11}-\sigma_{22})^2 + (\sigma_{22}-\sigma_{33})^2 + (\sigma_{33}-\sigma_{11})^2 \right] + 3(\sigma_{12}^2 + \sigma_{23}^2 + \sigma_{31}^2)}
$$
Or, in terms of principal stresses $\sigma_1, \sigma_2, \sigma_3$:
$$
\sigma_{\mathrm{vM}} = \sqrt{\frac{1}{2}\left[ (\sigma_1 - \sigma_2)^2 + (\sigma_2 - \sigma_3)^2 + (\sigma_3 - \sigma_1)^2 \right]}
$$
The most crucial feature of the von Mises criterion is that it depends **only on the second deviatoric invariant, $J_2$** .

### The Tresca Criterion: A Measure of Maximum Shear Stress

The **Tresca [yield criterion](@entry_id:193897)**, also known as the maximum shear stress theory, is based on the earlier physical insight that [plastic deformation](@entry_id:139726) is a result of [crystallographic slip](@entry_id:196486), which is driven by shear stress. The criterion postulates that yielding begins when the **maximum shear stress**, $\tau_{\max}$, at a point reaches a critical value.

In any stress state, the maximum shear stress can be found from the [principal stresses](@entry_id:176761):
$$
\tau_{\max} = \frac{\sigma_{\max} - \sigma_{\min}}{2} = \frac{1}{2} \max(|\sigma_1 - \sigma_2|, |\sigma_2 - \sigma_3|, |\sigma_3 - \sigma_1|)
$$
where $\sigma_{\max}$ and $\sigma_{\min}$ are the maximum and minimum [principal stresses](@entry_id:176761), respectively. The **Tresca [equivalent stress](@entry_id:749064)**, $\sigma_T$, is defined to equal the applied stress in a [uniaxial tension test](@entry_id:195375) at yield. This is achieved by setting:
$$
\sigma_T = 2\tau_{\max} = \sigma_{\max} - \sigma_{\min}
$$
Like the von Mises stress, the Tresca stress is independent of [hydrostatic pressure](@entry_id:141627) because adding a constant pressure $q$ to all [principal stresses](@entry_id:176761) leaves their differences unchanged: $(\sigma_i+q) - (\sigma_j+q) = \sigma_i - \sigma_j$ .

### A Comparative Analysis: Geometry, Smoothness, and the Lode Angle

The fundamental difference between the von Mises and Tresca criteria lies in their dependence on the deviatoric invariants. While both are independent of $I_1$, von Mises depends only on $J_2$, whereas Tresca depends on both $J_2$ and $J_3$ .

This difference is best visualized by examining the yield surfaces in the **deviatoric plane** (also known as the $\pi$-plane), a plane in [principal stress space](@entry_id:184388) perpendicular to the hydrostatic axis $(\sigma_1 = \sigma_2 = \sigma_3)$.
-   The **von Mises yield surface** is a **circle** in the deviatoric plane. This circular shape is a direct consequence of its sole dependence on $J_2$, which acts as a radial measure in this plane.
-   The **Tresca [yield surface](@entry_id:175331)** is a **regular hexagon** in the deviatoric plane.

This geometric difference means the Tresca criterion is sensitive to the "mode" of the [deviatoric stress](@entry_id:163323). This mode can be characterized by the **Lode angle**, $\theta$, which is defined by the ratio of the deviatoric invariants:
$$
\cos(3\theta) = \frac{3\sqrt{3}}{2}\frac{J_3}{J_2^{3/2}}
$$
Since the von Mises criterion depends only on $J_2$, it is independent of the Lode angle. The Tresca criterion, with its hexagonal shape, explicitly depends on $\theta$ . The ratio of the two equivalent stresses varies with the Lode angle. The Tresca hexagon is inscribed within the von Mises circle, touching at the corners. The ratio $\sigma_T / \sigma_{\mathrm{vM}}$ ranges from a minimum of $1$ for axisymmetric stress states like [uniaxial tension](@entry_id:188287) ($\theta=0$, corresponding to the corners of the hexagon) to a maximum of $2/\sqrt{3} \approx 1.155$ for pure shear states ($\theta=\pi/6$, corresponding to the midpoints of the hexagon's faces) . This implies that the Tresca criterion is always more conservative than (or equal to) the von Mises criterion.

The mathematical structure of the criteria also reveals a critical distinction. The von Mises criterion arises from a [quadratic form](@entry_id:153497) ($J_2$), resulting in a **smooth** and **strictly convex** yield surface. In contrast, the Tresca criterion arises from a `max` operator, leading to a **piecewise linear** [yield surface](@entry_id:175331) that is convex but not strictly convex. It possesses **corners** and **edges** where the function is not differentiable .

### Computational Implications of Non-Smoothness in the Tresca Criterion

The non-[differentiability](@entry_id:140863) of the Tresca [yield surface](@entry_id:175331) at its corners and edges has significant consequences for [computational plasticity](@entry_id:171377). Many numerical algorithms, such as the **return-mapping algorithms** used in the Finite Element Method (FEM), rely on [gradient-based methods](@entry_id:749986) like the Newton-Raphson scheme to solve the nonlinear equations of plastic flow.

At a smooth point on the yield surface, the direction of plastic flow (for an [associated flow rule](@entry_id:201731)) is uniquely defined by the outward [normal vector](@entry_id:264185) (the gradient of the yield function). At a corner or edge of the Tresca surface, where multiple linear yield functions are simultaneously active, the gradient is not unique. Instead, one must consider the **[subdifferential](@entry_id:175641)**, which is the set of all possible outward normal directions, forming a "fan" of vectors . For example, at a point corresponding to [uniaxial tension](@entry_id:188287), two of the six Tresca yield planes intersect, and the [plastic flow](@entry_id:201346) direction can be any convex combination of the normals to these two planes .

This non-uniqueness means that the [consistent tangent modulus](@entry_id:168075), which is the Jacobian required for the Newton-Raphson method, is not uniquely defined at these points. Naive use of a gradient from a single active branch can lead to oscillatory behavior near corners and a loss of the quadratic convergence rate that makes the Newton-Raphson method so efficient . Robust implementation of the Tresca model requires specialized algorithms that can handle this non-smoothness, such as:
-   **Active-set strategies** that explicitly manage the set of active yield planes.
-   **Multi-surface plasticity formulations** that solve the Karush-Kuhn-Tucker (KKT) conditions for all active surfaces simultaneously .
-   The use of smooth approximations to the Tresca hexagon.

### Application in Finite Strain Plasticity

When extending plasticity models to the geometrically nonlinear regime of **finite strains**, careful consideration must be given to the choice of stress measure. The physical mechanisms of plastic flow, such as [dislocation motion](@entry_id:143448), occur in the **current (deformed) configuration** of the material. Therefore, any physically-based yield criterion must be formulated in terms of the **Cauchy stress tensor $\boldsymbol{\sigma}$**, which is the [true stress](@entry_id:190985) acting on the deformed body.

Other stress tensors, such as the **Kirchhoff stress $\boldsymbol{\tau} = J\boldsymbol{\sigma}$** (where $J=\det \mathbf{F}$ is the determinant of the [deformation gradient](@entry_id:163749) $\mathbf{F}$) or the **second Piola-Kirchhoff stress $\mathbf{S}$**, are defined with respect to the reference configuration and are essential for computational formulations. However, one cannot naively apply the [equivalent stress](@entry_id:749064) formulas to these tensors and expect a physically meaningful result .

For example, computing an [equivalent stress](@entry_id:749064) from the Kirchhoff stress $\boldsymbol{\tau}$ yields a value that is scaled by $J$ compared to the true [equivalent stress](@entry_id:749064): $\sigma_{\mathrm{eq}}(\boldsymbol{\tau}) = J \sigma_{\mathrm{eq}}(\boldsymbol{\sigma})$. Applying the formulas to $\mathbf{S}$ gives a result that is not, in general, related to the true [equivalent stress](@entry_id:749064) in any simple way.

The correct procedure in a [finite strain](@entry_id:749398) computational context is always to work with the objective Cauchy stress. This typically involves:
1.  Computing a trial stress in a suitable reference-frame measure (e.g., $\mathbf{S}$).
2.  Pushing the trial stress forward to the current configuration to obtain a trial Cauchy stress $\boldsymbol{\sigma}^{\text{trial}}$.
3.  Applying the [return-mapping algorithm](@entry_id:168456) and the [yield criterion](@entry_id:193897) to the Cauchy stress.
4.  Pulling the updated Cauchy stress back to the reference configuration if necessary.

This workflow ensures that the material's yielding behavior is evaluated based on the true physical stresses in the current configuration, respecting the principles of objectivity and the physical basis of the [yield criteria](@entry_id:178101) .