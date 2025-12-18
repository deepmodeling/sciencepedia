## Introduction
When a ductile material like metal is stressed beyond its [elastic limit](@entry_id:186242), it undergoes permanent, or plastic, deformation. This process fundamentally alters the material's internal state, causing its subsequent response to loading to change—a phenomenon known as hardening. Accurately modeling this behavior is a cornerstone of [computational solid mechanics](@entry_id:169583), essential for predicting the performance, durability, and failure of engineering structures. The central challenge lies in mathematically describing how the material's elastic domain, defined by its yield surface, evolves with ongoing plastic deformation. Simple models fall short in capturing complex behaviors like the Bauschinger effect or ratcheting, creating a knowledge gap that more sophisticated theories must address.

This article provides a graduate-level exploration of the two classical frameworks for modeling this evolution: [isotropic and kinematic hardening](@entry_id:195752). Across three comprehensive chapters, you will build a deep and practical understanding of these critical concepts.

The first chapter, **Principles and Mechanisms**, will dissect the theoretical foundations, starting from the von Mises yield criterion and developing the mathematical formulations for both [isotropic and kinematic hardening](@entry_id:195752), from simple linear rules to advanced nonlinear and multi-component models.

The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the practical importance of these models, showing how the choice of [hardening law](@entry_id:750150) is critical for accurately simulating structural fatigue, manufacturing springback, and crack growth, with connections to materials science and geotechnical engineering.

Finally, the **Hands-On Practices** chapter will bridge theory and computation, guiding you through key numerical exercises like implementing the [radial return algorithm](@entry_id:169742) and deriving the [consistent tangent modulus](@entry_id:168075), which are essential skills for developing and using finite element codes.

## Principles and Mechanisms

The elastic domain, within which a material's deformation is fully recoverable, is defined in [stress space](@entry_id:199156) by a **yield surface**. For metallic materials, yielding is primarily driven by shear stresses and is largely unaffected by moderate hydrostatic pressure. This physical observation motivates the decomposition of the Cauchy stress tensor, $\boldsymbol{\sigma}$, into its hydrostatic part, $\frac{1}{3}(\mathrm{tr}\,\boldsymbol{\sigma})\boldsymbol{I}$, and its **deviatoric** part, $\boldsymbol{s} = \boldsymbol{\sigma} - \frac{1}{3}(\mathrm{tr}\,\boldsymbol{\sigma})\boldsymbol{I}$, where $\boldsymbol{I}$ is the second-order identity tensor. Plasticity models for metals are thus typically formulated in terms of invariants of this [deviatoric stress tensor](@entry_id:267642).

The most widely used criterion for isotropic metals is the **von Mises yield criterion**, which posits that yielding begins when the second invariant of the [deviatoric stress](@entry_id:163323), $J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s}$, reaches a critical value. The yield function, which defines the boundary of the elastic domain by the condition $f=0$, is expressed as:
$$
f(\boldsymbol{\sigma}) = \sigma_{eq} - \sigma_{y0} = \sqrt{3J_2} - \sigma_{y0} = 0
$$
Here, $\sigma_{y0}$ is the initial yield stress of the material as measured in a simple [uniaxial tension test](@entry_id:195375), and $\sigma_{eq} = \sqrt{3J_2}$ is the von Mises [equivalent stress](@entry_id:749064). By substituting the definition of $J_2$, the [equivalent stress](@entry_id:749064) can be written directly in terms of the [deviatoric stress tensor](@entry_id:267642):
$$
\sigma_{eq} = \sqrt{\frac{3}{2}\boldsymbol{s}:\boldsymbol{s}}
$$
Geometrically, in the [principal stress space](@entry_id:184388), the von Mises yield surface is a circular cylinder whose axis is the hydrostatic line ($\sigma_1=\sigma_2=\sigma_3$), reflecting its independence from hydrostatic pressure. A key mathematical feature of the von Mises surface is that it is smooth and continuously differentiable everywhere except at the origin, which ensures a uniquely defined outward normal vector for use in flow rules. This contrasts with other criteria, such as the Tresca criterion, which is based on maximum shear stress. The Tresca surface is a hexagonal cylinder that exhibits sharp corners, or vertices, where the normal is not unique. Furthermore, while the von Mises criterion depends only on $J_2$, the Tresca criterion depends on both $J_2$ and the third deviatoric invariant, $J_3 = \det(\boldsymbol{s})$ .

When [plastic deformation](@entry_id:139726) occurs, the material's internal state changes, leading to an evolution of the [yield surface](@entry_id:175331). This phenomenon is known as **hardening**. The two classical idealizations for this evolution are [isotropic hardening](@entry_id:164486) and [kinematic hardening](@entry_id:172077). Graphically, in a two-dimensional representation of [deviatoric stress](@entry_id:163323) space (the $\pi$-plane), an initial circular yield locus can either expand while remaining centered at the origin ([isotropic hardening](@entry_id:164486)), translate its center without changing its size ([kinematic hardening](@entry_id:172077)), or undergo a combination of both (mixed hardening) .

### Isotropic Hardening

**Isotropic hardening** describes the phenomenon where plastic deformation causes a uniform expansion of the [yield surface](@entry_id:175331). The center of the surface remains fixed at the origin of deviatoric stress space, but its size increases, signifying that the material becomes stronger in all stress directions.

This is modeled by allowing the [yield stress](@entry_id:274513), $\sigma_y$, to be a function of a scalar internal variable, $\kappa$, which quantifies the amount of plastic deformation. A common choice for $\kappa$ is the **accumulated equivalent plastic strain**, defined as $\kappa = \int \sqrt{\frac{2}{3}d\boldsymbol{\varepsilon}^p:d\boldsymbol{\varepsilon}^p}$. The yield function for von Mises plasticity with [isotropic hardening](@entry_id:164486) then becomes:
$$
f(\boldsymbol{\sigma}, \kappa) = \sqrt{3J_2} - \sigma_y(\kappa) = 0
$$
As plastic strain accumulates, $\kappa$ increases, and for a hardening material, $\sigma_y(\kappa)$ is a monotonically increasing function. This causes the radius of the cylindrical [yield surface](@entry_id:175331) to expand.

The specific functional form of $\sigma_y(\kappa)$ defines the character of the hardening response. Two common forms are:
1.  **Linear Isotropic Hardening**: This is the simplest model, where the [yield stress](@entry_id:274513) increases linearly with accumulated plastic strain:
    $$
    \sigma_y(\kappa) = \sigma_{y0} + H\kappa
    $$
    Here, $H$ is the constant hardening modulus. The hardening rate, $\frac{d\sigma_y}{d\kappa}$, is simply $H$. While simple, this model predicts that the stress can grow without bound, which is physically unrealistic for [large strains](@entry_id:751152) .

2.  **Saturation Hardening (Voce Law)**: A more realistic model allows the hardening rate to decrease as plastic strain accumulates, eventually leading to a saturation of the [yield stress](@entry_id:274513). The Voce law describes this behavior:
    $$
    \sigma_y(\kappa) = \sigma_{sat} - (\sigma_{sat} - \sigma_{y0})\exp(-b\kappa)
    $$
    In this model, the initial hardening modulus is $\left.\frac{d\sigma_y}{d\kappa}\right|_{\kappa=0} = b(\sigma_{sat}-\sigma_{y0})$, and the yield stress asymptotically approaches a saturation stress, $\sigma_{sat}$, as $\kappa \to \infty$. A special case is [perfect plasticity](@entry_id:753335), with no hardening, which is recovered by setting $H=0$ in the linear law or $b=0$ in the Voce law .

These phenomenological laws can be rationalized from a microstructural perspective. The strength of a metal is closely related to its dislocation density, $\rho$, through the Taylor relation, $\sigma_y \propto \sqrt{\rho}$. The evolution of [dislocation density](@entry_id:161592) with plastic strain, $\kappa$, can be modeled as a competition between dislocation storage (generation) and [dynamic recovery](@entry_id:200182) ([annihilation](@entry_id:159364)). A common model for this evolution is $\frac{d\rho}{d\kappa} = k_1\sqrt{\rho} - k_2\rho$. By solving this differential equation and substituting the result into the Taylor relation, one can show that the case with no [dynamic recovery](@entry_id:200182) ($k_2=0$) leads directly to a linear [hardening law](@entry_id:750150), $\sigma_y(\kappa) = \sigma_0 + H\kappa$. Including the [dynamic recovery](@entry_id:200182) term ($k_2 > 0$) leads to a Voce-type saturation law. This approach provides a physical justification for the observed macroscopic hardening behaviors .

### Kinematic Hardening and the Bauschinger Effect

While [isotropic hardening](@entry_id:164486) captures the general increase in strength due to [plastic work](@entry_id:193085), it fails to describe a crucial experimental observation known as the **Bauschinger effect**. This effect refers to the reduction of yield strength in the direction of reverse loading after a material has been plastically deformed in the forward direction. For example, if a metal is pulled in tension past its [yield point](@entry_id:188474) and then loaded in compression, it will yield at a compressive stress magnitude that is significantly lower than its initial yield stress .

Pure [isotropic hardening](@entry_id:164486) predicts the opposite: having yielded in tension, the yield surface expands, so the compressive [yield strength](@entry_id:162154) should *increase*. The physical origin of the Bauschinger effect lies in the heterogeneous nature of [plastic deformation](@entry_id:139726) at the microscale, leading to the buildup of internal residual stresses. The model that captures this phenomenon at the macroscopic level is **[kinematic hardening](@entry_id:172077)**.

In [kinematic hardening](@entry_id:172077), the yield surface does not change its size or shape; instead, it translates in stress space. This translation is governed by a second-order tensorial internal variable called the **[backstress](@entry_id:198105)**, $\boldsymbol{\alpha}$, which represents the center of the yield surface. The [yield function](@entry_id:167970) for von Mises plasticity with pure [kinematic hardening](@entry_id:172077) is:
$$
f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = \sqrt{\frac{3}{2}(\boldsymbol{s} - \boldsymbol{\alpha}):(\boldsymbol{s} - \boldsymbol{\alpha})} - \sigma_{y0} = 0
$$
Here, $\boldsymbol{\alpha}$ is assumed to be a [deviatoric tensor](@entry_id:185837) to maintain pressure-insensitivity, and $\sigma_{y0}$ is the initial (constant) [yield stress](@entry_id:274513). In deviatoric stress space, this equation describes a hypersphere centered at $\boldsymbol{\alpha}$ with a radius proportional to $\sigma_{y0}$ .

The Bauschinger effect is a natural consequence of this formulation. Consider a uniaxial tensile test. As the material yields and deforms plastically in tension, the backstress $\boldsymbol{\alpha}$ evolves in the direction of loading. The [yield surface](@entry_id:175331) translates along with the stress state. When the load is reversed, the stress state begins moving from a point on the "front" of the translated yield surface toward the "back". Because the center has shifted, the distance to the reverse-side yield boundary is now shorter than it was initially, resulting in a lower compressive yield magnitude. The [kinematic hardening](@entry_id:172077) model is thus essential for accurately modeling [cyclic loading](@entry_id:181502) and reverse-yielding phenomena  .

### Evolution Laws for Kinematic Hardening

The predictive power of a [kinematic hardening](@entry_id:172077) model is determined by the **evolution law** prescribed for the [backstress](@entry_id:198105), $\dot{\boldsymbol{\alpha}}$. This law dictates how the yield surface translates as a function of the plastic [strain rate](@entry_id:154778), $\dot{\boldsymbol{\varepsilon}}^p$.

A foundational approach is to invoke thermodynamic principles. Starting from a Helmholtz free energy function that includes a quadratic term for energy storage in the backstress, $\psi_{\alpha} = \frac{1}{2c}\boldsymbol{\alpha}:\boldsymbol{\alpha}$, and applying Ziegler's orthogonality postulate, one can derive the simplest plausible evolution law. This postulate states that the dissipative internal processes evolve in a way that maximizes the rate of dissipation. For associative von Mises plasticity, this leads to the conclusion that $\dot{\boldsymbol{\alpha}}$ must be collinear with $\dot{\boldsymbol{\varepsilon}}^p$. This gives rise to the **Prager linear [kinematic hardening](@entry_id:172077) rule**:
$$
\dot{\boldsymbol{\alpha}} = C \dot{\boldsymbol{\varepsilon}}^p
$$
where $C$ is a constant hardening modulus. Integration shows that the backstress grows linearly and without bound with plastic strain. This model predicts a Bauschinger effect, but it cannot capture the experimental observation that the effect saturates with increasing prestrain. The predicted reverse-yield stress continues to change linearly with prestrain indefinitely .

To introduce the physically observed saturation, a non-linear evolution law is required. The **Armstrong-Frederick (AF) model** modifies the Prager rule by adding a "[dynamic recovery](@entry_id:200182)" term:
$$
\dot{\boldsymbol{\alpha}} = C \dot{\boldsymbol{\varepsilon}}^p - \gamma \boldsymbol{\alpha} |\dot{\boldsymbol{\varepsilon}}^p|
$$
where $\gamma$ is a material parameter that controls the rate of recovery and $|\dot{\boldsymbol{\varepsilon}}^p| = \sqrt{\frac{2}{3}\dot{\boldsymbol{\varepsilon}}^p:\dot{\boldsymbol{\varepsilon}}^p}$ is the equivalent plastic strain rate. The recovery term, $-\gamma \boldsymbol{\alpha} |\dot{\boldsymbol{\varepsilon}}^p|$, opposes the growth of the backstress, with its magnitude increasing as $\boldsymbol{\alpha}$ becomes larger. This leads to an exponential saturation of the [backstress](@entry_id:198105) towards a limiting value. Consequently, the AF model provides a much more realistic description of the Bauschinger effect, correctly predicting that the reverse [yield stress](@entry_id:274513) approaches a stable, saturated value after sufficient prestraining .

### Advanced Concepts and Model Limitations

Real material behavior is often more complex than what can be captured by pure isotropic or pure [kinematic hardening](@entry_id:172077). For many applications, a **[combined hardening](@entry_id:186067)** model is employed, where the yield surface both expands and translates. This is achieved by combining the formulations:
$$
f(\boldsymbol{\sigma}, \boldsymbol{\alpha}, \kappa) = \sqrt{\frac{3}{2}(\boldsymbol{s} - \boldsymbol{\alpha}):(\boldsymbol{s} - \boldsymbol{\alpha})} - \sigma_y(\kappa) = 0
$$
Here, both the [backstress](@entry_id:198105) $\boldsymbol{\alpha}$ and the [yield surface](@entry_id:175331) size $\sigma_y$ evolve according to their respective [hardening laws](@entry_id:183802) .

Even with [combined hardening](@entry_id:186067), the standard models face challenges under complex loading conditions. A critical test for any plasticity model is its performance under **non-[proportional loading](@entry_id:191744)**, where the principal axes of the stress or [strain tensor](@entry_id:193332) rotate during deformation. Under such paths, the linear Prager rule exhibits a critical flaw: for certain closed-loop strain paths (e.g., a square path in strain space), it predicts that the [backstress](@entry_id:198105) returns to its starting value after a single cycle, implying immediate cyclic stabilization. Experiments, however, show that materials exhibit significant additional hardening under non-[proportional loading](@entry_id:191744), with a gradual approach to a stable state. The single-component AF model improves on this but is often insufficient. A more powerful solution is the **Chaboche model**, which decomposes the total [backstress](@entry_id:198105) into a sum of several AF-type components, $\boldsymbol{\alpha} = \sum_{j} \boldsymbol{\alpha}_j$, each with its own set of parameters $(C_j, \gamma_j)$. By using a spectrum of recovery rates, the model acquires a more sophisticated "memory" of the strain path, allowing it to capture the gradual stabilization and additional hardening observed in non-proportional cyclic tests .

Finally, all the models discussed so far, which are based on the $J_2$ invariant, share a fundamental limitation: they assume the yield surface maintains its shape (a circle in the $\pi$-plane). However, experiments involving sharp turns in the strain path—for example, large tensile prestraining followed by pure shear—reveal that the [yield surface](@entry_id:175331) not only translates and expands but also **distorts**. The surface may develop a "nose" in the direction of recent loading and a flattened region on the opposite side. This phenomenon is known as **distortional hardening**.

No combination of [isotropic and kinematic hardening](@entry_id:195752) within a $J_2$ framework can capture this change in shape. To model this, the assumption of a fixed [yield surface](@entry_id:175331) shape must be abandoned. This can be achieved using a more general [yield function](@entry_id:167970), such as the Hill quadratic form, where the metric of the stress space itself is allowed to evolve. This involves introducing a fourth-order tensor, $\mathbf{H}$, as an internal variable:
$$
f(\mathbf{s}, \boldsymbol{\alpha}, \mathbf{H}) = \sqrt{(\mathbf{s} - \boldsymbol{\alpha}) : \mathbf{H} : (\mathbf{s} - \boldsymbol{\alpha})} - \sigma_{y0} = 0
$$
By defining an evolution law for $\mathbf{H}$ that depends on the plastic flow direction, the model can capture the development of [plastic anisotropy](@entry_id:203119) and the complex distortion of the yield surface observed under non-[proportional loading](@entry_id:191744) paths .