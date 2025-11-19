## Introduction
In the design and analysis of mechanical components, understanding the transition from elastic to plastic deformation is paramount. This transition, known as yielding, signifies the onset of permanent, irreversible changes in a material's shape, and predicting the stress state that triggers it is a cornerstone of solid mechanics. For ductile metals, which form the backbone of modern engineering, this prediction is governed by mathematical models called [yield criteria](@entry_id:178101). These criteria define a boundary in stress space, separating safe, elastic behavior from the onset of [plastic deformation](@entry_id:139726).

While numerous models exist, the Tresca (maximum shear stress) and von Mises (maximum [distortion energy](@entry_id:198925)) criteria have become the two most widely accepted and applied theories. Though both are rooted in the physical observation that shear drives plastic flow in metals, they offer different mathematical formulations and, consequently, different predictions under complex loading conditions. This article provides a comprehensive examination of these two pivotal criteria, clarifying their theoretical underpinnings, practical consequences, and computational nuances.

The journey begins in the **Principles and Mechanisms** chapter, where we will deconstruct the stress tensor, introduce the critical concepts of [stress invariants](@entry_id:170526) and pressure insensitivity, and derive the mathematical forms of both the Tresca and von Mises criteria. Next, the **Applications and Interdisciplinary Connections** chapter will bridge theory and practice, exploring how the choice between these criteria impacts engineering design, manufacturing processes like autofrettage, fracture mechanics, and their implementation in [finite element analysis](@entry_id:138109). Finally, the **Hands-On Practices** section provides an opportunity to apply these concepts through guided problems, reinforcing theoretical knowledge with practical calculation and interpretation skills.

## Principles and Mechanisms

The onset of plastic deformation, or yielding, marks the transition from reversible elastic behavior to permanent, irreversible deformation. Predicting the stress state at which this transition occurs is a cornerstone of solid mechanics and engineering design. A yield criterion is a mathematical function, $F(\boldsymbol{\sigma})$, of the Cauchy stress tensor $\boldsymbol{\sigma}$, which defines a boundary in stress space. States for which $F(\boldsymbol{\sigma}) \lt 0$ are elastic, states with $F(\boldsymbol{\sigma}) = 0$ are on the verge of yielding, and states with $F(\boldsymbol{\sigma}) \gt 0$ are inadmissible in classical [rate-independent plasticity](@entry_id:754082) theory. This chapter elucidates the fundamental principles underpinning the two most widely used [yield criteria](@entry_id:178101) for ductile metals: the Tresca and von Mises criteria.

### Stress Invariants and the Hydrostatic-Deviatoric Decomposition

The state of stress at a material point is described by the symmetric second-order Cauchy stress tensor, $\boldsymbol{\sigma}$. While the components of this tensor depend on the chosen coordinate system, its physical essence does not. For an **isotropic** material, whose properties are independent of direction, any physically meaningful [response function](@entry_id:138845), such as a [yield criterion](@entry_id:193897), must also be independent of the coordinate system. This requires that the [yield function](@entry_id:167970) be expressed in terms of quantities that are themselves invariant under [coordinate transformations](@entry_id:172727).

A fundamental theorem of [continuum mechanics](@entry_id:155125) states that any scalar-valued isotropic function of a [symmetric tensor](@entry_id:144567) can be expressed as a function of its **[principal invariants](@entry_id:193522)**. For the stress tensor $\boldsymbol{\sigma}$, these are:

1.  $I_1 = \mathrm{tr}(\boldsymbol{\sigma}) = \sigma_{kk}$
2.  $I_2 = \frac{1}{2} [(\mathrm{tr}(\boldsymbol{\sigma}))^2 - \mathrm{tr}(\boldsymbol{\sigma}^2)]$
3.  $I_3 = \det(\boldsymbol{\sigma})$

Equivalently, these can be expressed in terms of the **[principal stresses](@entry_id:176761)** ($\sigma_1, \sigma_2, \sigma_3$), which are the eigenvalues of $\boldsymbol{\sigma}$. The requirement of [isotropy](@entry_id:159159) means that the [yield function](@entry_id:167970) must be a symmetric function of the [principal stresses](@entry_id:176761), $F(\sigma_1, \sigma_2, \sigma_3)$, since permuting the principal stresses is physically indistinguishable from a reorientation of the coordinate axes in an [isotropic material](@entry_id:204616) [@problem_id:2706989].

A more physically insightful approach is to decompose the stress tensor into two parts that govern distinct modes of deformation. It is observed experimentally that applying a uniform, all-around pressure to a ductile metal primarily causes a change in its volume (a **volumetric** or **dilatational** response), while shear stresses cause a change in its shape (a **distortional** or **deviatoric** response). This motivates the decomposition of the stress tensor $\boldsymbol{\sigma}$ into a **hydrostatic** part and a **deviatoric** part:

$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}_{\mathrm{h}} + \boldsymbol{s}
$$

The hydrostatic part, $\boldsymbol{\sigma}_{\mathrm{h}} = p \boldsymbol{I}$, represents the [mean stress](@entry_id:751819) at the point, where $p$ is the **[mean stress](@entry_id:751819)** (or hydrostatic pressure) and $\boldsymbol{I}$ is the identity tensor. The [mean stress](@entry_id:751819) is directly related to the first stress invariant:

$$
p = \frac{1}{3} (\sigma_{11} + \sigma_{22} + \sigma_{33}) = \frac{1}{3} I_1
$$

The remaining part, $\boldsymbol{s}$, is the **[deviatoric stress tensor](@entry_id:267642)**, which represents the portion of the stress state that causes distortion. It is defined as:

$$
\boldsymbol{s} = \boldsymbol{\sigma} - p \boldsymbol{I}
$$

By construction, the [deviatoric stress tensor](@entry_id:267642) is traceless, i.e., $\mathrm{tr}(\boldsymbol{s}) = 0$. For example, consider a stress state given by the principal stresses $\boldsymbol{\sigma} = \mathrm{diag}(160, 90, 50)$ MPa. The mean stress is $p = \frac{1}{3}(160+90+50) = 100$ MPa. The hydrostatic stress tensor is $\boldsymbol{\sigma}_{\mathrm{h}} = \mathrm{diag}(100, 100, 100)$ MPa, and the [deviatoric stress tensor](@entry_id:267642) is $\boldsymbol{s} = \mathrm{diag}(160-100, 90-100, 50-100) = \mathrm{diag}(60, -10, -50)$ MPa [@problem_id:2707001].

Just like the full stress tensor, the [deviatoric stress tensor](@entry_id:267642) also has a set of invariants. The most important for [plasticity theory](@entry_id:177023) are its second and third invariants, denoted $J_2$ and $J_3$:

$$
J_2 = \frac{1}{2} \boldsymbol{s}:\boldsymbol{s} = \frac{1}{2} s_{ij}s_{ij}
$$

$$
J_3 = \det(\boldsymbol{s})
$$

The invariant $J_2$ is a measure of the overall magnitude of the [deviatoric stress](@entry_id:163323). For a given stress tensor $\boldsymbol{\sigma}$, one can compute these invariants systematically [@problem_id:2707003].

### The Principle of Pressure Insensitivity

A central tenet of classical plasticity for dense metals is that yielding is driven by distortion, not by volumetric change. The microscopic mechanism for plastic flow in crystalline metals is [dislocation glide](@entry_id:275474)—the sliding of atomic planes past one another. This is fundamentally a shear process that, to a very high degree of accuracy, conserves volume. Such a volume-preserving deformation is termed **isochoric** [@problem_id:2707071] [@problem_id:2707005].

Since the hydrostatic component of stress, $p\boldsymbol{I}$, is associated with volumetric change and the deviatoric component, $\boldsymbol{s}$, is associated with distortional change, it follows that the onset of plastic yield in dense metals should be independent of the hydrostatic stress. This is the **principle of pressure insensitivity**. Mathematically, this means that adding a uniform [hydrostatic stress](@entry_id:186327) to any given stress state should not affect whether the material yields. If two stress states, $\boldsymbol{\sigma}^{(1)}$ and $\boldsymbol{\sigma}^{(2)}$, are related by $\boldsymbol{\sigma}^{(2)} = \boldsymbol{\sigma}^{(1)} + q\boldsymbol{I}$ for some scalar pressure $q$, a pressure-insensitive yield criterion must give the same prediction for both [@problem_id:2612503].

This has a profound consequence for the mathematical form of the [yield function](@entry_id:167970). For an isotropic and pressure-insensitive material, the [yield function](@entry_id:167970) $F$ cannot depend on the first stress invariant $I_1 = 3p$. It must instead be a function only of the invariants of the [deviatoric stress tensor](@entry_id:267642), $J_2$ and $J_3$ [@problem_id:2706989]:

$$
F(\boldsymbol{\sigma}) = \hat{F}(J_2, J_3) = 0
$$

This principle elegantly separates the physics of yielding (distortion, governed by $\boldsymbol{s}$) from the physics of elastic compression (volumetric change, governed by $p$).

### The Von Mises Yield Criterion

The **von Mises criterion**, also known as the maximum [distortion energy](@entry_id:198925) criterion, is one of the most widely used models for ductile metals. It posits that yielding begins when the distortional strain energy per unit volume stored in the material reaches a critical value. For an isotropic linear elastic material, the distortional [strain energy density](@entry_id:200085), $W_d$, is directly proportional to the second deviatoric invariant, $J_2$:

$$
W_d = \frac{J_2}{2G}
$$

where $G$ is the shear modulus. The von Mises criterion thus simplifies to the postulate that yielding occurs when $J_2$ reaches a critical value, which we can write as $k^2$, where $k$ is the material's yield stress in pure shear.

$$
J_2 = k^2
$$

To make this criterion practical for engineering design, it is calibrated against the yield strength, $\sigma_Y$, obtained from a simple [uniaxial tension test](@entry_id:195375). For a tensile stress state $\sigma_{11} = \sigma_Y$ (with all other components zero), the value of $J_2$ is $\frac{1}{3}\sigma_Y^2$. Equating this to the yield condition gives the calibrated form of the criterion:

$$
J_2 = \frac{1}{3}\sigma_Y^2
$$

This leads to the definition of the **von Mises [equivalent stress](@entry_id:749064)**, $\sigma_{vM}$, a scalar measure of the "effective" stress that can be compared directly to $\sigma_Y$.

$$
\sigma_{vM} = \sqrt{3J_2}
$$

Yielding is predicted to occur when $\sigma_{vM} = \sigma_Y$. Using the definition of $J_2$ in terms of [principal stresses](@entry_id:176761), an equivalent and very common expression for the von Mises stress is obtained [@problem_id:2612503]:

$$
\sigma_{vM} = \sqrt{\frac{1}{2} \left[ (\sigma_1 - \sigma_2)^2 + (\sigma_2 - \sigma_3)^2 + (\sigma_3 - \sigma_1)^2 \right]}
$$

Another physical interpretation arises from the concept of the **[octahedral shear stress](@entry_id:200691)**, $\tau_{oct}$. This is the shear stress acting on a plane whose normal is equally inclined to the three principal stress axes. It can be shown from first principles that $\tau_{oct}$ is directly proportional to $\sqrt{J_2}$ [@problem_id:2706973]. The von Mises criterion is therefore equivalent to stating that yielding occurs when the [octahedral shear stress](@entry_id:200691) reaches a critical value.

### The Tresca Yield Criterion

The **Tresca criterion**, also known as the maximum shear stress theory, offers an alternative, more direct physical argument. Based on the observation that plastic flow is a shearing phenomenon, Tresca proposed that yielding begins when the maximum shear stress, $\tau_{max}$, at any point in the material reaches a critical value.

From an analysis of the [stress transformation](@entry_id:184474) equations, it can be proven that the maximum shear stress at a point is always equal to half the difference between the maximum and minimum principal stresses [@problem_id:2706973]:

$$
\tau_{max} = \frac{\sigma_1 - \sigma_3}{2}
$$

where the [principal stresses](@entry_id:176761) are ordered $\sigma_1 \ge \sigma_2 \ge \sigma_3$.

Like the von Mises criterion, the Tresca criterion is calibrated using the uniaxial tensile yield strength $\sigma_Y$. In a uniaxial test, the [principal stresses](@entry_id:176761) are $(\sigma_Y, 0, 0)$, so $\tau_{max} = \frac{\sigma_Y - 0}{2} = \frac{\sigma_Y}{2}$. This value is taken as the critical shear stress for the material. The Tresca yield criterion is thus:

$$
\tau_{max} = \frac{\sigma_Y}{2} \quad \text{or equivalently} \quad \sigma_1 - \sigma_3 = \sigma_Y
$$

This leads to the definition of the **Tresca [equivalent stress](@entry_id:749064)**, $\sigma_{Tr} = \sigma_1 - \sigma_3$. Yielding occurs when $\sigma_{Tr} = \sigma_Y$.

The pressure insensitivity of the Tresca criterion is immediately apparent from its definition. Adding a hydrostatic stress $p$ shifts all [principal stresses](@entry_id:176761) by the same amount ($\sigma_i \rightarrow \sigma_i + p$), leaving their differences, and thus $\tau_{max}$, unchanged [@problem_id:2612503].

### Comparison and Interpretation

While both criteria are based on sound physical principles of shear-driven, pressure-insensitive yielding, they are not identical. Their differences can be understood by examining their predictions in various stress states and their geometric representations.

#### Geometric Representation in the Deviatoric Plane

A powerful way to visualize and compare [yield criteria](@entry_id:178101) is to plot their yield surfaces in stress space. Since both criteria are pressure-insensitive, we can examine their intersection with the **deviatoric plane** (or **$\pi$-plane**), which is the plane in [principal stress space](@entry_id:184388) defined by $I_1 = \sigma_1 + \sigma_2 + \sigma_3 = \text{const}$.

*   The **von Mises** criterion, $\sigma_{vM} = \text{const}$, which is equivalent to $J_2 = \text{const}$, traces a perfect **circle** in the deviatoric plane. This reflects its complete indifference to the relative magnitudes of the principal deviatoric stresses, so long as their mean-square value ($J_2$) is constant [@problem_id:2612460].

*   The **Tresca** criterion, $\sigma_1 - \sigma_3 = \text{const}$ (and its permutations), traces a **regular hexagon** in the deviatoric plane. The vertices and sides of the hexagon correspond to different stress states where different pairs of principal stresses define the maximum shear [@problem_id:2612460].

When calibrated to agree in [uniaxial tension](@entry_id:188287), the Tresca hexagon is inscribed within the von Mises circle, touching it at the six points corresponding to [uniaxial tension](@entry_id:188287)/compression and related states. This geometry immediately reveals that for all other stress states, the Tresca criterion is more **conservative**—it predicts yielding at a lower stress magnitude than von Mises. The largest discrepancy occurs at the midpoints of the hexagon's sides, which correspond to states of pure shear. In pure shear, Tresca predicts yielding at a stress level that is approximately $1 - \sqrt{3}/2 \approx 13.4\%$ lower than that predicted by von Mises [@problem_id:2706973]. The ratio of the two equivalent stresses is bounded by $\frac{\sqrt{3}}{2} \le \frac{\sigma_{Tr}}{\sigma_{vM}} \le 1$, or conversely, $1 \le \frac{\sigma_{vM}}{\sigma_{Tr}} \le \frac{2}{\sqrt{3}} \approx 1.155$ [@problem_id:2707001].

#### Lode Angle Dependence

The difference between the hexagonal and circular shapes has a deeper physical meaning related to the third deviatoric invariant, $J_3$. The position on the yield locus in the $\pi$-plane is parameterized by the **Lode angle**, which depends on the ratio of $J_3$ to $J_2^{3/2}$.

*   The **von Mises** criterion depends only on $J_2$. Its circular shape in the $\pi$-plane signifies its independence from $J_3$ and thus from the Lode angle. It treats all [deviatoric stress](@entry_id:163323) states with the same $J_2$ as equivalent.

*   The **Tresca** criterion, in contrast, can be shown to depend on both $J_2$ and $J_3$. Its hexagonal shape reflects this **Lode angle dependence**. This can be demonstrated by considering two deviatoric stress states with the same $J_2$ but different $J_3$. For example, the pure shear state $(\sigma, 0, -\sigma)$ and the axisymmetric state $(\sigma/\sqrt{3}, \sigma/\sqrt{3}, -2\sigma/\sqrt{3})$ have identical values of $J_2$ but different values of $J_3$. A calculation shows they also have different values of $\tau_{max}$. The von Mises criterion predicts they are equally close to yielding, while the Tresca criterion does not [@problem_id:2707052].

For most ductile metals, experimental data tends to fall between the Tresca hexagon and the von Mises circle, with the von Mises criterion often providing a slightly better overall fit. The choice between them can depend on the application, with the mathematical simplicity and conservatism of the Tresca criterion being attractive in some contexts.

#### Mathematical Properties and the Flow Rule

A final important distinction lies in their mathematical smoothness. The von Mises [yield surface](@entry_id:175331) is smooth and continuously differentiable everywhere. The Tresca surface, being a hexagon, has sharp **corners** and **edges**. This non-differentiability has important implications for the **[associated flow rule](@entry_id:201731)**, which states that the direction of the plastic strain increment must be normal to the yield surface.

At a smooth point on the surface, this normal is unique. At a corner or edge of the Tresca surface, however, the normal is not uniquely defined. Using the tools of convex analysis, the set of all possible normal directions forms a **[normal cone](@entry_id:272387)**. For example, at an edge where two facets of the hexagon meet, the admissible [plastic flow](@entry_id:201346) directions lie in the "fan" spanned by the normals to the two active facets. This ensures that the [plastic flow](@entry_id:201346) remains incompressible, as the trace of any vector in the [normal cone](@entry_id:272387) is zero, but introduces a non-uniqueness in the flow direction that must be handled in numerical simulations [@problem_id:2707002].

### Scope and Limitations

It is critical to recognize the assumptions underlying these classical criteria.

*   **Isotropy**: Both models assume the material is isotropic. For materials with a strong preferred crystallographic orientation (**texture**), often resulting from processes like rolling or drawing, the yield strength becomes directional. In such cases, these isotropic criteria are inadequate, and more complex **[anisotropic yield criteria](@entry_id:181680)** (e.g., Hill's quadratic criterion) must be employed, which depend not just on [stress invariants](@entry_id:170526) but on the stress components in a material-specific coordinate system [@problem_id:2706989].

*   **Pressure Insensitivity**: While an excellent approximation for dense metals under typical engineering pressures, the assumption of pressure insensitivity breaks down in several important cases [@problem_id:2707071]:
    *   **Porous Materials**: In materials with internal voids, such as sintered metals, hydrostatic tension can cause voids to grow, which is a dissipative plastic mechanism. This makes yielding sensitive to pressure. Micromechanical models like the Gurson-Tvergaard-Needleman (GTN) criterion are designed for such materials.
    *   **Frictional Materials**: For [geomaterials](@entry_id:749838) like soils and rocks, frictional sliding is a key mechanism, and their strength is strongly dependent on the confining (hydrostatic) pressure. Pressure-sensitive criteria like Mohr-Coulomb and Drucker-Prager are used for these materials.
    *   **High-Pressure Regimes**: Even for fully dense metals, at extremely high pressures (on the order of GPa), the fundamental properties of the crystal lattice and dislocations can be altered, introducing a genuine pressure dependence on yielding.

In summary, the Tresca and von Mises criteria represent two elegant and powerful models for predicting the onset of plasticity in isotropic, ductile metals. They are rooted in the fundamental physical principle that yielding is a shear-driven, volume-preserving process, but they differ in their specific mathematical formulation, leading to slightly different predictions and capturing different levels of detail about the stress state's influence.