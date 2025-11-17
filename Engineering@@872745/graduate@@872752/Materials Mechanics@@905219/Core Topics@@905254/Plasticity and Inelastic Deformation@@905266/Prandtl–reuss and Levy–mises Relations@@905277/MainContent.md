## Introduction
The ability of ductile metals to deform permanently without fracturing is a cornerstone of modern engineering, enabling everything from the shaping of automobile body panels to the energy absorption of structures during impact. Understanding and predicting this behavior, known as plasticity, is critical for safe and efficient design. However, developing a mathematical framework that accurately captures the transition from recoverable [elastic deformation](@entry_id:161971) to permanent plastic flow presents a significant challenge. This article addresses this gap by providing a rigorous exploration of the classical [rate-independent plasticity](@entry_id:754082) theories for ductile metals.

This article is structured to build your understanding from the ground up. In **Principles and Mechanisms**, we will dissect the foundational concepts, starting with the decomposition of stress into hydrostatic and deviatoric parts and introducing the von Mises yield criterion. We will then derive the celebrated Lévy–Mises and Prandtl–Reuss relations, which govern the direction and evolution of plastic flow, and extend these ideas to the more complex [finite strain](@entry_id:749398) regime. Next, **Applications and Interdisciplinary Connections** will bridge theory and practice by demonstrating how these relations are used to characterize materials, enable powerful computational simulations using the Finite Element Method, and analyze structural stability. Finally, **Hands-On Practices** will allow you to solidify your knowledge by working through guided problems that apply these concepts to concrete engineering scenarios.

## Principles and Mechanisms

The behavior of ductile metals under load is characterized by an initial elastic phase, where deformation is recoverable, followed by a plastic phase, where deformation is permanent. This chapter elucidates the fundamental principles and mathematical machinery used to model this elastoplastic response, focusing on the classical rate-independent theories for small strains, known as the Lévy–Mises and Prandtl–Reuss relations, before providing a rigorous extension to the [finite strain](@entry_id:749398) regime.

### The Role of Deviatoric Stress in Yielding

A central empirical observation in [metal plasticity](@entry_id:176585) is that the onset of irreversible deformation is primarily governed by shear stresses that cause distortion, while being largely insensitive to hydrostatic pressure that causes volume change. To embed this physical insight into a mathematical framework, the Cauchy stress tensor, $\boldsymbol{\sigma}$, is additively decomposed into two parts: a **[hydrostatic stress](@entry_id:186327)** tensor and a **[deviatoric stress](@entry_id:163323)** tensor.

The hydrostatic component is represented by the [mean stress](@entry_id:751819), $p$, which is one-third of the trace of the stress tensor.
$$
p = \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma}) = \frac{1}{3}\sigma_{kk}
$$
The [deviatoric stress tensor](@entry_id:267642), $\boldsymbol{s}$, is then defined as the total stress minus its hydrostatic part:
$$
s_{ij} = \sigma_{ij} - p \delta_{ij}
$$
where $\delta_{ij}$ is the Kronecker delta. By this definition, the [deviatoric stress tensor](@entry_id:267642) is inherently trace-free, i.e., $s_{kk} = s_{11} + s_{22} + s_{33} = 0$. This decomposition, $\boldsymbol{\sigma} = \boldsymbol{s} + p\boldsymbol{I}$, separates the stress state into a component responsible for distortion or change in shape ($\boldsymbol{s}$) and a component responsible for dilation or change in volume ($p\boldsymbol{I}$).

For example, consider a stress state given by the tensor [@problem_id:2911226]:
$$
\boldsymbol{\sigma} = \begin{pmatrix} 120  30  0 \\ 30  80  0 \\ 0  0  60 \end{pmatrix} \text{ MPa}
$$
The mean stress is $p = \frac{1}{3}(120 + 80 + 60) = \frac{260}{3}$ MPa. The [deviatoric stress tensor](@entry_id:267642) is then:
$$
\boldsymbol{s} = \begin{pmatrix} 120 - \frac{260}{3}  30  0 \\ 30  80 - \frac{260}{3}  0 \\ 0  0  60 - \frac{260}{3} \end{pmatrix} = \begin{pmatrix} \frac{100}{3}  30  0 \\ 30  -\frac{20}{3}  0 \\ 0  0  -\frac{80}{3} \end{pmatrix} \text{ MPa}
$$
A quick check confirms that the trace of $\boldsymbol{s}$ is $\frac{100}{3} - \frac{20}{3} - \frac{80}{3} = 0$.

The **von Mises yield criterion** formalizes the idea of pressure-independent yielding. It postulates that plastic flow begins when a [scalar invariant](@entry_id:159606) of the [deviatoric stress](@entry_id:163323) reaches a critical value. This invariant is the **second invariant of the deviatoric stress**, denoted $J_2$:
$$
J_2 = \frac{1}{2}s_{ij}s_{ji} = \frac{1}{2} \mathrm{tr}(\boldsymbol{s}^2)
$$
To create a measure with units of stress that can be directly compared to experimental data from, for example, a [uniaxial tension test](@entry_id:195375), the **von Mises [equivalent stress](@entry_id:749064)**, $\sigma_e$, is defined:
$$
\sigma_e = \sqrt{3J_2} = \sqrt{\frac{3}{2}s_{ij}s_{ji}}
$$
The factor of $\sqrt{3}$ is a calibration constant. For a simple [uniaxial tension test](@entry_id:195375) where $\sigma_{11} = \sigma$ and all other components are zero, the [deviatoric stress](@entry_id:163323) components are $s_{11} = \frac{2}{3}\sigma$ and $s_{22}=s_{33}=-\frac{1}{3}\sigma$. This gives $J_2 = \frac{1}{3}\sigma^2$, and thus $\sigma_e = \sqrt{3(\frac{1}{3}\sigma^2)} = |\sigma|$. This ensures that the [equivalent stress](@entry_id:749064) matches the applied tensile stress, providing a direct link between multiaxial stress states and simple experimental data. Since $\sigma_e$ depends only on $J_2$, which in turn depends only on $\boldsymbol{s}$, superposing any amount of [hydrostatic pressure](@entry_id:141627) on a stress state will not change its deviatoric part and therefore will not change the value of $\sigma_e$ or affect the onset of yielding [@problem_id:2911195].

The state of the material can be described by a **yield function**, $f$. For a material that yields when the von Mises stress reaches a material-specific [yield strength](@entry_id:162154), $\sigma_y$, the [yield function](@entry_id:167970) is:
$$
f(\boldsymbol{\sigma}) = \sigma_e - \sigma_y \le 0
$$
The condition $f  0$ defines an elastic state, while $f=0$ defines a plastic state on the [yield surface](@entry_id:175331). Stress states for which $f > 0$ are inadmissible.

### The Kinematics and Flow Rule at Small Strains

To develop a complete [constitutive model](@entry_id:747751), we need to describe the evolution of strain. In the context of small deformations (where displacement gradients are much less than unity), the kinematics of [elastoplasticity](@entry_id:193198) are built upon the cornerstone of the **additive decomposition of the strain rate** [@problem_id:2911191]. The total [strain rate tensor](@entry_id:198281), $\dot{\boldsymbol{\varepsilon}}$, is assumed to be the sum of a recoverable elastic part, $\dot{\boldsymbol{\varepsilon}}^e$, and a permanent plastic part, $\dot{\boldsymbol{\varepsilon}}^p$:
$$
\dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^e + \dot{\boldsymbol{\varepsilon}}^p
$$
The elastic strain rate is governed by a rate form of Hooke's law, while the plastic strain rate requires a new constitutive law known as a **[flow rule](@entry_id:177163)**.

In the theory of associative plasticity, the direction of the plastic strain rate in strain space is assumed to be normal to the [yield surface](@entry_id:175331) in stress space. This is known as the **[normality rule](@entry_id:182635)** or **[associative flow rule](@entry_id:163391)**. It states that the plastic [strain rate](@entry_id:154778) is proportional to the gradient of the [yield function](@entry_id:167970) with respect to the stress tensor:
$$
\dot{\varepsilon}^p_{ij} = \dot{\lambda} \frac{\partial f}{\partial \sigma_{ij}}
$$
Here, $\dot{\lambda} \ge 0$ is a scalar known as the **[plastic multiplier](@entry_id:753519)**, which determines the magnitude of the plastic flow. For the von Mises yield function $f = \sigma_e - \sigma_y$, the gradient is [@problem_id:2911195] [@problem_id:2911208]:
$$
\frac{\partial f}{\partial \sigma_{ij}} = \frac{\partial \sigma_e}{\partial \sigma_{ij}} = \frac{\partial \sqrt{3J_2}}{\partial \sigma_{ij}} = \frac{\sqrt{3}}{2\sqrt{J_2}}\frac{\partial J_2}{\partial \sigma_{ij}} = \frac{3}{2\sigma_e} s_{ij}
$$
Substituting this into the [flow rule](@entry_id:177163) gives the celebrated **Lévy–Mises relations**:
$$
\dot{\varepsilon}^p_{ij} = \left(\frac{3\dot{\lambda}}{2\sigma_e}\right) s_{ij}
$$
This fundamental result provides the [constitutive law](@entry_id:167255) for the plastic [strain rate](@entry_id:154778). It mathematically encodes the principle that plastic flow is proportional to the [deviatoric stress](@entry_id:163323) and is thus a purely distortional phenomenon.

A direct and profound consequence of the Lévy–Mises relations is the principle of **[plastic incompressibility](@entry_id:183440)**. The rate of plastic volume change is the trace of the plastic [strain rate tensor](@entry_id:198281), $\dot{\varepsilon}^p_{kk}$. Since $\dot{\varepsilon}^p_{ij}$ is proportional to $s_{ij}$ and the deviatoric stress is trace-free ($s_{kk}=0$), it follows immediately that:
$$
\dot{\varepsilon}^p_{kk} = 0
$$
This means that plastic deformation occurs at constant volume. It is crucial, however, to distinguish this from the total volume change. The total [volumetric strain rate](@entry_id:272471), $\dot{\varepsilon}_{kk}$, is the sum of its elastic and plastic parts [@problem_id:2911233]:
$$
\dot{\varepsilon}_{kk} = \dot{\varepsilon}^e_{kk} + \dot{\varepsilon}^p_{kk} = \dot{\varepsilon}^e_{kk}
$$
The elastic [volumetric strain rate](@entry_id:272471) is related to the rate of change of mean stress via the bulk modulus, $K$: $\dot{\varepsilon}^e_{kk} = \dot{p}/K$. Therefore, even during a [plastic deformation](@entry_id:139726) process, the material will experience a net volume change if the hydrostatic component of the stress is changing. For instance, if a material with $K = 160$ GPa is subjected to a loading process where the mean stress increases at a rate of $\dot{p} = 12$ MPa/s, the total [volumetric strain rate](@entry_id:272471) will be $\dot{\varepsilon}_{kk} = (12 \text{ MPa/s}) / (160 \times 10^3 \text{ MPa}) = 7.5 \times 10^{-5} \text{ s}^{-1}$, entirely due to elastic compression, even as plastic flow occurs simultaneously without any volume change of its own.

### The Complete Prandtl-Reuss Constitutive Model

The Lévy–Mises relations provide the direction of plastic flow, but to form a complete theory, we must integrate them with elasticity and establish a rule for the magnitude of plastic flow. The resulting framework is known as the **Prandtl–Reuss theory**.

The model is built from three components [@problem_id:2911223]:
1.  **Elastic Law:** The stress rate is related to the elastic strain rate via the fourth-order isotropic [elastic stiffness tensor](@entry_id:196425) $\mathbb{C}$. For a [hypoelastic model](@entry_id:750490), this is $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\dot{\boldsymbol{\varepsilon}}^e$.
2.  **Strain Rate Decomposition:** $\dot{\boldsymbol{\varepsilon}}^e = \dot{\boldsymbol{\varepsilon}} - \dot{\boldsymbol{\varepsilon}}^p$.
3.  **Flow Rule:** $\dot{\varepsilon}^p_{ij} = \dot{\lambda} \frac{3}{2\sigma_e} s_{ij}$.

Substituting the second and third components into the first yields the elastoplastic [constitutive law](@entry_id:167255) in rate form:
$$
\dot{\sigma}_{ij} = C_{ijkl} \left( \dot{\varepsilon}_{kl} - \dot{\lambda} \frac{3 s_{kl}}{2\sigma_e} \right)
$$
This equation relates the stress rate to the total strain rate, but it contains the as-yet-unknown [plastic multiplier](@entry_id:753519) $\dot{\lambda}$. The determination of $\dot{\lambda}$ is governed by a set of logical conditions known as the **Karush–Kuhn–Tucker (KKT) conditions** of plasticity [@problem_id:2911220]:
-   **Yield Condition:** $f(\boldsymbol{\sigma}, \kappa) \le 0$. The stress state must be admissible (inside or on the [yield surface](@entry_id:175331)). $\kappa$ is an internal variable representing the hardening state of the material.
-   **Flow Condition:** $\dot{\lambda} \ge 0$. This ensures that [plastic dissipation](@entry_id:201273) is non-negative, a requirement of the second law of thermodynamics.
-   **Complementarity Condition:** $\dot{\lambda} f = 0$. This is the crucial "switching" condition. It dictates that if the stress state is strictly elastic ($f  0$), there is no [plastic flow](@entry_id:201346) ($\dot{\lambda}=0$). Conversely, if there is [plastic flow](@entry_id:201346) ($\dot{\lambda}>0$), the stress state must be on the [yield surface](@entry_id:175331) ($f=0$).

During a process of continued [plastic loading](@entry_id:753518) ($\dot{\lambda} > 0$), the stress state must remain on the [yield surface](@entry_id:175331). This requirement is enforced by the **consistency condition**, $\dot{f}=0$. Expanding this with the [chain rule](@entry_id:147422) gives:
$$
\dot{f} = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \dot{\boldsymbol{\sigma}} + \frac{\partial f}{\partial \kappa} \dot{\kappa} = 0
$$
This [consistency condition](@entry_id:198045) becomes the governing equation from which the value of the [plastic multiplier](@entry_id:753519) $\dot{\lambda}$ is determined for a given [strain rate](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}$.

To make the model fully predictive, we need to connect the abstract multiplier $\dot{\lambda}$ to a [physical measure](@entry_id:264060) of plastic strain and specify how the material hardens. The **equivalent plastic strain**, $\kappa$ (often denoted $\varepsilon^p_{eq}$), is a scalar measure of accumulated [plastic deformation](@entry_id:139726), defined in rate form as $\dot{\kappa} = \sqrt{\frac{2}{3}\dot{\varepsilon}^p_{ij}\dot{\varepsilon}^p_{ij}}$. For the specific definitions used in von Mises plasticity, substituting the [flow rule](@entry_id:177163) into this definition proves that the [plastic multiplier](@entry_id:753519) is identical to the rate of equivalent plastic strain: $\dot{\lambda} = \dot{\kappa}$ [@problem_id:2911208] [@problem_id:2911199]. The [flow rule](@entry_id:177163) can then be written in the physically transparent form:
$$
\dot{\varepsilon}^p_{ij} = \dot{\kappa} \, \frac{3s_{ij}}{2\sigma_e}
$$
Hardening describes the evolution of the yield surface with plastic deformation. In **[isotropic hardening](@entry_id:164486)**, the [yield surface](@entry_id:175331) expands uniformly in all directions, so the [yield function](@entry_id:167970) takes the form $f = \sigma_e - \sigma_y(\kappa)$, where $\sigma_y(\kappa)$ is an increasing function. In **[kinematic hardening](@entry_id:172077)**, the [yield surface](@entry_id:175331) translates in [stress space](@entry_id:199156), described by a backstress tensor $\boldsymbol{\alpha}$, with a yield function like $f = \sigma_e(\boldsymbol{\sigma}-\boldsymbol{\alpha}) - \sigma_{y0}$. While [isotropic hardening](@entry_id:164486) is simpler, it cannot capture phenomena like the **Bauschinger effect**—the reduction in [yield strength](@entry_id:162154) upon load reversal—which requires the [yield surface](@entry_id:175331) translation provided by [kinematic hardening](@entry_id:172077) [@problem_id:2911199].

### Formulations for Finite Strains

Extending [plasticity theory](@entry_id:177023) to finite strains and rotations presents significant challenges. The additive decomposition of strain is no longer kinematically valid, and ensuring that [constitutive laws](@entry_id:178936) are independent of the observer's reference frame (**[material frame indifference](@entry_id:166014)** or **objectivity**) requires careful formulation.

#### Hypoelastic-Plastic Formulations

A direct extension of the Prandtl–Reuss theory involves postulating a rate-type constitutive law in the current configuration. The kinematics are based on an additive split of the **[rate of deformation tensor](@entry_id:182598)** (the symmetric part of the velocity gradient, $\mathbf{L}$), $\mathbf{d} = \mathbf{d}^e + \mathbf{d}^p$. The constitutive law relates a stress rate to the elastic part of the deformation rate, $\mathbf{d}^e$.

A critical issue arises because the simple [material time derivative](@entry_id:190892) of the Cauchy stress, $\dot{\boldsymbol{\sigma}}$, is not an objective tensor; its value depends on the rotation of the observer. To satisfy [frame indifference](@entry_id:749567), a hypoelastic law must use an **[objective stress rate](@entry_id:168809)**, such as the **Jaumann rate**, $\overset{\nabla}{\boldsymbol{\sigma}}$ [@problem_id:2911179]:
$$
\overset{\nabla}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\omega}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\omega}
$$
where $\boldsymbol{\omega}$ is the [spin tensor](@entry_id:187346) (the skew-symmetric part of $\mathbf{L}$). This rate is constructed to be objective and, importantly, vanishes during a pure [rigid body rotation](@entry_id:167024) of a stressed body, reflecting that no new stresses are generated by such a motion. The hypoelastic-plastic law takes the form $\overset{\nabla}{\boldsymbol{\sigma}} = \mathbb{C}:\mathbf{d}^e$. While widely used, this formulation is not guaranteed to be thermodynamically consistent, as the work done in a closed elastic strain cycle may not be zero [@problem_id:2911227].

#### Hyperelastic-Plastic Formulations

The modern, thermodynamically rigorous approach to [finite strain plasticity](@entry_id:175182) is based on a hyperelastic framework. This theory is built on two key concepts [@problem_id:2911191] [@problem_id:2911227]:

1.  **Multiplicative Decomposition of the Deformation Gradient:** The total deformation gradient $\mathbf{F}$ is decomposed into a plastic part $\mathbf{F}^p$ and an elastic part $\mathbf{F}^e$:
    $$
    \mathbf{F} = \mathbf{F}^e \mathbf{F}^p
    $$
    This imagines the deformation process as a sequence: first, a [plastic deformation](@entry_id:139726) maps the reference configuration to a conceptual, stress-free **intermediate configuration**; second, an elastic deformation maps the intermediate configuration to the final, current configuration. Plastic incompressibility is enforced by the constraint $\det(\mathbf{F}^p)=1$.

2.  **Thermodynamic Potential:** The elastic response is derived from a **Helmholtz free energy** function, $\Psi$, which is a [state function](@entry_id:141111) of the [elastic deformation](@entry_id:161971). For an [isotropic material](@entry_id:204616), this is a function of an [elastic strain](@entry_id:189634) measure, typically the elastic right Cauchy-Green tensor $\mathbf{C}^e = (\mathbf{F}^e)^T\mathbf{F}^e$. This guarantees that the elastic response is path-independent and thermodynamically consistent. Stress measures are then derived via **[work conjugacy](@entry_id:194957)**. For instance, the Kirchhoff stress $\boldsymbol{\tau} = J\boldsymbol{\sigma}$ (where $J=\det(\mathbf{F})$) is work-conjugate to the rate of deformation $\mathbf{d}$.

Within this robust framework, the Lévy–Mises relations remain valid and applicable. The [associative flow rule](@entry_id:163391) is formulated using appropriate, thermodynamically [conjugate variables](@entry_id:147843). For an isotropic $J_2$ material, the yield surface is defined in terms of the Kirchhoff stress, $f(\boldsymbol{\tau}, \kappa)=0$. The plastic rate of deformation $\mathbf{d}^p$ is then found to be proportional to the deviatoric part of the Kirchhoff stress, $\boldsymbol{\tau}'$:
$$
\mathbf{d}^p \propto \boldsymbol{\tau}'
$$
This generalization preserves the essential physical principle of the Lévy–Mises theory—that plastic flow is a distortional, [isochoric process](@entry_id:138993) driven by the [deviatoric stress](@entry_id:163323)—while embedding it within a framework that is fully consistent with the [kinematics](@entry_id:173318) and thermodynamics of finite deformations.