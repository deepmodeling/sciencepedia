## Introduction
Predicting the onset and evolution of material failure is a central goal of [computational solid mechanics](@entry_id:169583). For ductile materials, failure is not an isolated event but a complex process involving the interplay of irreversible plastic deformation and the progressive loss of material integrity, or damage. While conceptually distinct, these mechanisms are deeply intertwined. However, modeling this coupled behavior presents a significant challenge: as damage accumulates, materials often exhibit softening, where stress decreases with increasing strain. In standard local [continuum models](@entry_id:190374), this leads to a critical breakdown, producing simulation results that are physically meaningless and pathologically dependent on the computational mesh.

This article provides a comprehensive guide to the advanced theoretical framework designed to overcome this challenge: [coupled plasticity-damage models](@entry_id:747972) with [nonlocal regularization](@entry_id:752666). We will navigate from first principles to practical application, equipping you with the knowledge to build robust and predictive simulations of material failure. The first chapter, **Principles and Mechanisms**, establishes the thermodynamic foundation of these models, explores the different ways plasticity and damage can be coupled, and details the theory of [nonlocal regularization](@entry_id:752666) that restores physical realism. The second chapter, **Applications and Interdisciplinary Connections**, showcases the framework's power and versatility by applying it to real-world problems in structural engineering, [battery degradation](@entry_id:264757), and [interface mechanics](@entry_id:750731). Finally, the **Hands-On Practices** chapter offers a series of guided problems to solidify your understanding and bridge the gap between theory and numerical implementation.

## Principles and Mechanisms

This chapter delves into the fundamental principles and theoretical mechanisms that govern [coupled plasticity-damage models](@entry_id:747972). Building upon the introduction to the subject, we will formulate the constitutive theory from first principles of thermodynamics, explore the various ways in which plasticity and damage processes interact, and address the critical issue of [material softening](@entry_id:169591) and the resulting need for [nonlocal regularization](@entry_id:752666). Finally, we will examine the consequences of these advanced models and situate them within the broader context of [computational fracture mechanics](@entry_id:203605).

### Thermodynamic Foundations of Coupled Models

A rigorous and predictive model for material behavior must be consistent with the fundamental laws of thermodynamics. For the isothermal processes typically considered in solid mechanics, the framework is built upon two pillars: a **Helmholtz free energy density** function, $\psi$, which encapsulates the stored energy in the material, and the **Clausius-Duhem inequality**, which expresses the [second law of thermodynamics](@entry_id:142732) and ensures that dissipation is always non-negative.

The state of the material at a point is described not only by the observable total strain, $\boldsymbol{\varepsilon}$, but also by a set of **[internal state variables](@entry_id:750754)** that capture the history of irreversible microstructural changes. In a coupled plasticity-damage model, these variables typically include the plastic [strain tensor](@entry_id:193332), $\boldsymbol{\varepsilon}^p$, one or more hardening variables (which we will represent generically by a scalar $\alpha$), and a [scalar damage variable](@entry_id:196275), $d \in [0, 1]$, where $d=0$ represents the virgin material and $d=1$ signifies a complete loss of integrity.

The Helmholtz free energy density, $\psi$, is postulated as a function of these state variables. A common form, which we will use as a basis for our discussion, is:

$$ \psi(\boldsymbol{\varepsilon}, \boldsymbol{\varepsilon}^p, \alpha, d) = \psi_e(\boldsymbol{\varepsilon}^e, d) + \psi_p(\alpha) + \psi_d(d) $$

where $\boldsymbol{\varepsilon}^e = \boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^p$ is the [elastic strain](@entry_id:189634). The term $\psi_e$ represents the stored elastic strain energy, which is affected by damage. The term $\psi_p$ represents the energy stored due to plastic hardening, and $\psi_d$ is an energy associated with the creation of damage itself.

A prevalent approach is to model the effect of damage as a degradation of the material's elastic stiffness. This is achieved by introducing a **degradation function**, $g(d)$, which is a monotonically decreasing function with $g(0)=1$. For an isotropic material with an initial [elastic stiffness tensor](@entry_id:196425) $\mathbb{C}$, the stored elastic energy density might take the form [@problem_id:3589089]:

$$ \psi_e(\boldsymbol{\varepsilon}^e, d) = \frac{1}{2} g(d) \boldsymbol{\varepsilon}^e : \mathbb{C} : \boldsymbol{\varepsilon}^e $$

Another common choice for the degradation factor is $(1-d)^2$, which can be motivated by micromechanical considerations and offers certain advantages in variational formulations [@problem_id:3589056]. The hardening energy is often a simple quadratic function, such as $\psi_p(\alpha) = \frac{1}{2} H \alpha^2$, where $H$ is a hardening modulus.

The Clausius-Duhem inequality for isothermal processes states that the rate of dissipation, $\mathcal{D}$, must be non-negative:

$$ \mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0 $$

where $\boldsymbol{\sigma}$ is the Cauchy stress tensor and an overdot denotes a [material time derivative](@entry_id:190892). By applying the [chain rule](@entry_id:147422) to $\dot{\psi}$ and using the standard Coleman-Noll argument, one can systematically derive the [constitutive relations](@entry_id:186508) for the reversible parts of the response and an expression for the dissipation. This procedure identifies the stress tensor $\boldsymbol{\sigma}$ as the thermodynamic conjugate to the total strain $\boldsymbol{\varepsilon}$:

$$ \boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^e} $$

For the energy potential discussed above, this yields the stress-damage relation [@problem_id:3589089]:

$$ \boldsymbol{\sigma} = g(d) \mathbb{C} : (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^p) $$

This equation elegantly expresses the physical notion that damage reduces the stress-carrying capacity of the material. The term $\mathbb{C} : (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^p)$ can be interpreted as an "effective" stress in the undamaged material, which is then scaled down by the degradation function $g(d)$ to give the true (or Cauchy) stress $\boldsymbol{\sigma}$.

The reduced [dissipation inequality](@entry_id:188634) then takes the form:

$$ \mathcal{D} = - \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^p} : \dot{\boldsymbol{\varepsilon}}^p - \frac{\partial \psi}{\partial \alpha} \dot{\alpha} - \frac{\partial \psi}{\partial d} \dot{d} \ge 0 $$

Each term in this expression represents a dissipative mechanism. The quantities multiplying the rates of the internal variables are the **[thermodynamic forces](@entry_id:161907)** driving their evolution. Of particular interest is the **[damage energy release rate](@entry_id:195626)**, or the [thermodynamic force](@entry_id:755913) conjugate to damage, commonly denoted by $Y$:

$$ Y = - \frac{\partial \psi}{\partial d} $$

For the free energy form we have been considering, this force is [@problem_id:3589089] [@problem_id:3589056]:

$$ Y = - \frac{1}{2} g'(d) \boldsymbol{\varepsilon}^e : \mathbb{C} : \boldsymbol{\varepsilon}^e - \frac{\partial \psi_d}{\partial d} $$

This force $Y$ represents the energetic "gain" from an incremental increase in damage. The [damage evolution law](@entry_id:181934) is then formulated by relating $\dot{d}$ to $Y$, for instance, by positing that damage grows only when $Y$ exceeds a certain material-dependent threshold. Note that $Y$ is a [state function](@entry_id:141111) and does not depend on rates like the [plastic multiplier](@entry_id:753519) increment, but it does depend on the accumulated plastic strain $\boldsymbol{\varepsilon}^p$ through its effect on the [elastic strain](@entry_id:189634) $\boldsymbol{\varepsilon}^e$ [@problem_id:3589089].

### The Spectrum of Plasticity-Damage Coupling

The term "coupling" refers to the bi-directional influence between the mechanisms of plastic deformation and material damage. There are several distinct ways this interaction can be modeled, each with profound implications for the predicted material response.

#### Damage-Affected Elasticity and Plasticity

The most direct form of coupling is the degradation of [mechanical properties](@entry_id:201145) by damage. As we have seen, the elastic stiffness is reduced, leading to a softer elastic response. Beyond this, damage can also influence the plastic behavior itself. A key concept here is the **effective stress**, which is the stress measure used to evaluate the [yield criterion](@entry_id:193897). Two primary approaches exist:

1.  **Simo-Ju Coupling:** In this framework, plasticity is assumed to be driven by the stress state in the *undamaged* material skeleton. The [yield function](@entry_id:167970), $f$, is evaluated on an [effective stress](@entry_id:198048) tensor defined as $\tilde{\boldsymbol{\sigma}} = \mathbb{C} : (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^p)$. Consequently, the yield condition $f(\tilde{\boldsymbol{\sigma}}, \alpha) \le 0$ is completely independent of the [damage variable](@entry_id:197066) $d$. Damage only affects the macroscopic Cauchy stress, $\boldsymbol{\sigma} = g(d) \tilde{\boldsymbol{\sigma}}$. An important consequence is that for a fixed strain state, an increase in damage relaxes the [true stress](@entry_id:190985) but does not bring the material point closer to or further from yielding [@problem_id:3589089].

2.  **Lemaitre-Type Coupling:** This approach is motivated by the idea that stress is carried by the "effective" or undamaged area of the material. The yield function is evaluated using an effective stress defined as $\tilde{\boldsymbol{\sigma}} = \boldsymbol{\sigma} / (1-d)$ or a similar form. For instance, a one-dimensional yield condition might be written as $f = |\tilde{\sigma}| - (\sigma_{y0} + H \varepsilon^p) \le 0$, which is equivalent to $|\sigma| - (1-d)(\sigma_{y0} + H \varepsilon^p) \le 0$ [@problem_id:3589067]. Here, an increase in damage directly shrinks the [yield surface](@entry_id:175331) in the true stress space, promoting further plastic flow.

Furthermore, damage can also degrade the plastic hardening response. For example, the [yield stress](@entry_id:274513) evolution may be modeled as $\sigma_y = \sigma_{y0} + (1-\bar{d})H\alpha$, where the hardening contribution is diminished as damage accumulates [@problem_id:3589098].

#### Plasticity-Driven Damage

The reciprocal coupling effect is the driving of damage by [plastic deformation](@entry_id:139726). While elastic strains can cause damage ([brittle fracture](@entry_id:158949)), in ductile materials, damage and void growth are predominantly fueled by plastic straining. This is captured by making the [damage energy release rate](@entry_id:195626), $Y$, a function of plastic [state variables](@entry_id:138790). For example, in the expression for $Y$ derived previously, the dependence on $\boldsymbol{\varepsilon}^e$ makes [damage evolution](@entry_id:184965) implicitly linked to plasticity. Some models make this link more explicit by defining the damage-driving quantity directly in terms of plastic work or the equivalent plastic strain, $\kappa$. This is a crucial modeling choice to prevent premature damage in ductile materials where significant [plastic flow](@entry_id:201346) precedes failure [@problem_id:3589064].

Another important consideration is **unilateral effects**, where damage is active in tension but not in compression. This is vital for materials like concrete. In such models, the damage-driving force is defined using only the tensile part of the strain or stress tensor, ensuring that compressive loading does not cause [damage evolution](@entry_id:184965) [@problem_id:3589065].

### The Challenge of Softening and Nonlocal Regularization

A major challenge in modeling failure arises from **[material softening](@entry_id:169591)**, a regime where stress decreases with increasing strain. This can be caused by damage accumulation or by intrinsic plastic softening phenomena. In a standard (local) continuum model, softening leads to the loss of ellipticity of the governing [partial differential equations](@entry_id:143134). Numerically, this manifests as a **[pathological mesh dependency](@entry_id:184469)** in finite element simulations: the deformation localizes into a zone whose width is determined by the element size. As the mesh is refined, this zone becomes infinitesimally thin, and the predicted energy dissipated during failure spuriously drops to zero.

To remedy this unphysical behavior, the continuum model must be **regularized** by introducing an **internal length scale**, $\ell$. This parameter reflects the characteristic length of microstructural interactions (e.g., [grain size](@entry_id:161460), particle spacing) and ensures that the width of the localization band is a material property, not a numerical artifact. This is the essence of **nonlocal models**.

There are two main families of [nonlocal regularization](@entry_id:752666):

#### Integral Nonlocal Models

In an integral model, a local field variable, $\phi(\boldsymbol{x})$, is replaced by a nonlocal counterpart, $\bar{\phi}(\boldsymbol{x})$, obtained by a weighted average over a neighborhood:

$$ \bar{\phi}(\boldsymbol{x}) = \int_V \omega(\boldsymbol{x}-\boldsymbol{s}) \phi(\boldsymbol{s}) \, dV_s $$

where $\omega$ is a weighting kernel (e.g., a Gaussian or [exponential function](@entry_id:161417)) whose characteristic width defines the internal length scale $\ell$. For example, a nonlocal [damage variable](@entry_id:197066) can be computed by convolving a local damage field with an exponential kernel $A(r) = \frac{1}{2\ell}\exp(-|r|/\ell)$ [@problem_id:3589098]. The model's constitutive laws are then formulated in terms of this smoothed variable $\bar{\phi}$. This approach, while conceptually straightforward, can be computationally demanding due to the evaluation of the integral.

#### Gradient-Enhanced Nonlocal Models

A more computationally efficient alternative is the [gradient-enhanced model](@entry_id:749989). It can be shown that, for certain kernels, the integral formulation is equivalent to solving a Helmholtz-type partial differential equation for the nonlocal variable:

$$ \bar{\phi} - \ell^2 \nabla^2 \bar{\phi} = \phi $$

This approach can be derived directly from a [thermodynamic potential](@entry_id:143115) by including a term dependent on the gradient of the variable to be regularized. For instance, if we regularize the [damage variable](@entry_id:197066) $d$, the Helmholtz free energy can be augmented with a gradient energy term [@problem_id:3589056] [@problem_id:3589096]:

$$ \psi(\dots, d, \nabla d) = \dots + \frac{1}{2} c \ell^2 |\nabla d|^2 $$

where $c$ is a regularization modulus. Following the thermodynamic procedure, the conjugate force $Y$ now includes a contribution from this nonlocal term. The [microforce balance](@entry_id:202908) equation, derived from the [stationarity](@entry_id:143776) of the total energy, becomes a [partial differential equation](@entry_id:141332) (PDE) for the damage field $d(\boldsymbol{x})$ [@problem_id:3589096]:

$$ Y_{\text{local}}(d, \boldsymbol{\varepsilon}^e, \dots) - c \ell^2 \nabla^2 d = 0 $$

This equation, along with the standard [mechanical equilibrium](@entry_id:148830) equation, forms a coupled system of PDEs that must be solved over the domain. The damage field itself becomes a primary unknown field in the [finite element analysis](@entry_id:138109).

### What to Regularize: A Critical Modeling Choice

The decision of which internal variable to make nonlocal is not trivial. The goal is to regularize the source of the softening instability.

*   **Regularizing Damage Variables:** This is the most common strategy. Since damage is the physical source of degradation, regularizing the [damage variable](@entry_id:197066) $d$ or its driving force $Y$ is a natural choice [@problem_id:3589056] [@problem_id:3589098] [@problem_id:3589065].

*   **Regularizing Plastic Variables:** When softening is strongly coupled to plasticity, it may be necessary to regularize a plastic variable.
    *   **Regularizing Accumulated Plastic Strain ($\kappa$):** Here, a nonlocal equivalent plastic strain, $\bar{\kappa}$, is computed and used in the yield function, e.g., $f(\boldsymbol{\sigma}, \bar{\kappa}) \le 0$. The [plastic flow](@entry_id:201346) is still governed by a local multiplier $\lambda$ determined from the consistency condition on this nonlocal [yield surface](@entry_id:175331) [@problem_id:3589067]. Because $\bar{\kappa}$ is an integrated quantity, this method regularizes the history of plastic flow.
    *   **Regularizing the Plastic Multiplier ($\lambda$):** In this approach, the [plastic multiplier](@entry_id:753519) itself is considered the source of a nonlocal field $\bar{\lambda}$, governed by $\bar{\lambda} - \ell^2 \nabla^2 \bar{\lambda} = \lambda$. The plastic flow rate is then given by $\dot{\boldsymbol{\varepsilon}}^p = \bar{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}$.

The choice has significant consequences, especially in complex scenarios [@problem_id:3589084]. Regularizing the rate-like multiplier $\lambda$ directly targets the *instantaneous* source of instability within a load step. This can be more effective at suppressing [numerical oscillations](@entry_id:163720), particularly when softening is strongly rate-dependent or when loading paths are non-proportional. In contrast, regularizing the history-[dependent variable](@entry_id:143677) $\kappa$ can introduce a "lag" in the stabilizing mechanism, as the nonlocal field reflects the smoothed past and may not respond quickly enough to a newly developing instability.

### Consequences and Context

#### The Size Effect

One of the most important physical consequences of [nonlocal regularization](@entry_id:752666) is the prediction of a **[size effect](@entry_id:145741)**. Local [continuum mechanics](@entry_id:155125) is scale-free, but real quasi-brittle materials exhibit a size effect: larger structures are proportionally weaker and more brittle than geometrically similar smaller ones. Nonlocal models naturally capture this phenomenon. The internal length $\ell$ fixes the width of the failure process zone. In a small specimen, this zone occupies a large portion of the body, allowing for significant redistribution of stress and a more "ductile" overall response. In a large specimen, the failure zone is small relative to the overall size, and the vast amount of stored elastic energy is released abruptly upon localization, leading to a more brittle failure at a lower [nominal stress](@entry_id:201335).

This is often captured by a [size effect law](@entry_id:171636), such as the one proposed for a bar under tension, where the peak [nominal stress](@entry_id:201335) $\sigma_{\text{peak}}$ depends on the specimen length $L$ [@problem_id:3589067]:

$$ \sigma_{\text{peak}}(L;\ell) = \sigma_{\text{ref}} \frac{L}{L + 2\ell} $$

Such laws are not just a theoretical consequence; they provide a powerful link to experimental reality. By conducting tests on specimens of different sizes and fitting the measured peak stresses to the model's prediction, one can determine the value of the internal length scale $\ell$, thereby calibrating the model against physical observation.

#### Context: Damage-Plasticity vs. Phase-Field Models

Coupled damage-plasticity (DP) models are part of a broader class of methods for simulating fracture. A prominent alternative is the **Phase-Field Fracture (PFF)** approach. While both use a scalar field to represent cracking, their foundations and typical applications differ [@problem_id:3589064].

PFF models are typically rooted in a [variational formulation](@entry_id:166033) of Griffith's theory of fracture. The total energy balances a degraded elastic energy with a fracture energy, $G_c$, which is regularized over a length scale $\ell$ by the phase field. A key result is that the tensile strength predicted by such models scales with material properties as $\sigma_c \sim \sqrt{E G_c / \ell}$.

In contrast to PFF models, which primarily describe [brittle fracture](@entry_id:158949), DP models are designed to capture the interplay of plastic deformation and damage, which is characteristic of [ductile fracture](@entry_id:161045). In DP models, energy is dissipated through both plastic flow and [damage evolution](@entry_id:184965). Both frameworks can be formulated within a consistent energetic and variational structure, and modern research often seeks to combine their strengths to model the full spectrum of failure from brittle to ductile.