## Introduction
In the study of materials undergoing [large deformations](@entry_id:167243) and rotations, formulating [constitutive laws](@entry_id:178936) that are independent of the observer is a cornerstone of continuum mechanics. This principle, known as [material frame-indifference](@entry_id:178419) or objectivity, ensures that a material's intrinsic response is described consistently, regardless of the observer's motion. However, a significant challenge arises when using rate-type [constitutive equations](@entry_id:138559), common in plasticity and [viscoelasticity](@entry_id:148045), as the standard [material time derivative](@entry_id:190892) of stress is inherently non-objective. This article addresses this fundamental problem by providing a comprehensive exploration of objective stress rates.

Across the following chapters, you will gain a deep understanding of this critical topic. The "Principles and Mechanisms" chapter will first demonstrate why the [material time derivative](@entry_id:190892) is inadequate and then detail the mathematical construction and physical interpretation of key [objective rates](@entry_id:198692) like the Jaumann, Green-Naghdi, and Truesdell rates. Subsequently, "Applications and Interdisciplinary Connections" will bridge theory and practice, exploring how the choice of rate impacts [thermodynamic consistency](@entry_id:138886), [numerical stability](@entry_id:146550) in [computational mechanics](@entry_id:174464), and the formulation of models for [finite strain plasticity](@entry_id:175182). Finally, the "Hands-On Practices" section will offer practical exercises to apply these concepts and solidify your understanding of their behavior in common deformation scenarios.

## Principles and Mechanisms

In the study of materials undergoing [large deformations](@entry_id:167243), a central challenge lies in formulating [constitutive laws](@entry_id:178936)—the mathematical relationships between stress and strain—that are valid irrespective of the observer's motion. The material's response to deformation is an intrinsic property and should not depend on whether it is being observed from a stationary laboratory or a rotating spacecraft. This fundamental requirement is known as the **[principle of material frame-indifference](@entry_id:188488)**, or **objectivity**. When we formulate constitutive laws in a rate-type form, which is common for describing plasticity, [viscoelasticity](@entry_id:148045), and incremental elasticity, this principle demands the use of special mathematical constructs known as **objective stress rates**. This chapter elucidates why these rates are necessary, how they are constructed, and what their physical and theoretical implications are.

### The Problem of the Material Time Derivative

In [continuum mechanics](@entry_id:155125), the simplest measure of the rate of change of a quantity associated with a material particle is the **[material time derivative](@entry_id:190892)**, denoted by a superposed dot (e.g., $\dot{\boldsymbol{\sigma}}$ for the Cauchy stress tensor $\boldsymbol{\sigma}$). This derivative follows the particle as it moves through space. A natural first attempt at a rate-type [constitutive law](@entry_id:167255) might be to relate this material derivative of stress directly to the rate of deformation $\boldsymbol{D}$, the symmetric part of the [spatial velocity gradient](@entry_id:187198) $\boldsymbol{L}$.

However, such a law would violate the [principle of material frame-indifference](@entry_id:188488). To see why, consider two observers. The "current" observer measures positions $\boldsymbol{x}$, velocities $\boldsymbol{v}$, and stresses $\boldsymbol{\sigma}$. A second, "starred" observer is related to the first by a time-dependent [rigid body motion](@entry_id:144691) (a translation $\boldsymbol{c}(t)$ and a rotation $\boldsymbol{Q}(t)$), such that the position of a particle in the starred frame is $\boldsymbol{x}^{\ast}(t) = \boldsymbol{c}(t) + \boldsymbol{Q}(t)\boldsymbol{x}(t)$.

For the physical description to be consistent, tensor quantities measured by the two observers must be related by the rotation $\boldsymbol{Q}$. For the second-order Cauchy stress tensor, this transformation is $\boldsymbol{\sigma}^{\ast} = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}$. A quantity is defined as **objective** if it transforms in this proper tensorial manner between any two such observers. The stress tensor $\boldsymbol{\sigma}$ is, by its physical nature, an objective tensor. Similarly, the [rate of deformation tensor](@entry_id:182598) $\boldsymbol{D}$ can be shown to be objective, transforming as $\boldsymbol{D}^{\ast} = \boldsymbol{Q}\boldsymbol{D}\boldsymbol{Q}^{\mathsf{T}}$.

Now, let us examine the transformation of the [material time derivative](@entry_id:190892) of stress, $\dot{\boldsymbol{\sigma}}$. By applying the product rule of differentiation to the transformation rule for $\boldsymbol{\sigma}$, we find:
$$
\dot{\boldsymbol{\sigma}}^{\ast} = \frac{d}{dt}(\boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}) = \dot{\boldsymbol{Q}}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{Q}\boldsymbol{\sigma}\dot{\boldsymbol{Q}}^{\mathsf{T}}
$$
This expression can be rewritten by introducing the **spin of the observer frame**, a [skew-symmetric tensor](@entry_id:199349) defined as $\boldsymbol{\Omega} = \dot{\boldsymbol{Q}}\boldsymbol{Q}^{\mathsf{T}}$. The result is the fundamental transformation rule for the material stress rate:
$$
\dot{\boldsymbol{\sigma}}^{\ast} = \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}\boldsymbol{\sigma}^{\ast} - \boldsymbol{\sigma}^{\ast}\boldsymbol{\Omega}
$$
The objectivity requirement for a stress rate, let's call it $\mathring{\boldsymbol{\sigma}}$, is that it must transform as a proper tensor: $\mathring{\boldsymbol{\sigma}}^{\ast} = \boldsymbol{Q}\mathring{\boldsymbol{\sigma}}\boldsymbol{Q}^{\mathsf{T}}$. Comparing this definition with the transformation of $\dot{\boldsymbol{\sigma}}$, we see that the [material time derivative](@entry_id:190892) fails to be objective due to the presence of the additional commutator term, $[\boldsymbol{\Omega}, \boldsymbol{\sigma}^{\ast}] = \boldsymbol{\Omega}\boldsymbol{\sigma}^{\ast} - \boldsymbol{\sigma}^{\ast}\boldsymbol{\Omega}$. This term represents the rate of change of stress as perceived by the starred observer due solely to their own rotation, an artifact that has no physical bearing on the material's constitutive response.

Consequently, a naive constitutive law of the form $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$, where $\mathbb{C}$ is a tensor of material constants, would not be frame-indifferent. The left side is non-objective, while the right side is objective. The equation cannot hold for all observers. This necessitates the construction of objective stress rates that are "purified" of the observer-dependent rotational effects inherent in the [material time derivative](@entry_id:190892).

### Corotational Rates: The Jaumann and Green-Naghdi Rates

The non-objective terms in the transformation of $\dot{\boldsymbol{\sigma}}$ are purely rotational. This suggests a strategy for correction: define a new rate by subtracting the apparent rate of change of stress caused by a particular choice of material rotation. This family of rates is known as **[corotational rates](@entry_id:183217)**.

A general [corotational rate](@entry_id:193173) can be expressed in the form:
$$
\mathring{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}_{spin}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}_{spin}
$$
where $\boldsymbol{W}_{spin}$ is some [skew-symmetric tensor](@entry_id:199349) representing a chosen spin. The term $\boldsymbol{W}_{spin}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}_{spin}$ is the rate of change of $\boldsymbol{\sigma}$ due to its rotation with spin $\boldsymbol{W}_{spin}$. For the resulting rate $\mathring{\boldsymbol{\sigma}}$ to be objective, it can be proven that the chosen [spin tensor](@entry_id:187346) $\boldsymbol{W}_{spin}$ must transform between observers according to the rule $\boldsymbol{W}_{spin}^{\ast} = \boldsymbol{Q}\boldsymbol{W}_{spin}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}$. This transformation shows that the observer's spin $\boldsymbol{\Omega}$ adds directly to the material spin measured by that observer. It is this additive structure that allows for the cancellation of the non-objective terms.

Different choices of spin that satisfy this transformation rule lead to different, but equally valid, [objective rates](@entry_id:198692). Two of the most common are the Jaumann and Green-Naghdi rates.

#### The Jaumann Rate

The **Jaumann rate** (or Zaremba-Jaumann rate) uses the **material [spin tensor](@entry_id:187346)** $\boldsymbol{W}$, which is the skew-symmetric part of the velocity gradient: $\boldsymbol{W} = \mathrm{skw}(\boldsymbol{L}) = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^{\mathsf{T}})$. This tensor represents the instantaneous rate of rotation of the material element itself. It can be shown that $\boldsymbol{W}$ transforms as $\boldsymbol{W}^{\ast} = \boldsymbol{Q}\boldsymbol{W}\boldsymbol{Q}^{\mathsf{T}} + \boldsymbol{\Omega}$, satisfying the condition for objectivity.

The Jaumann rate is therefore defined as:
$$
\boldsymbol{\sigma}^{\nabla J} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}
$$
This rate measures the change of stress in a frame that is instantaneously rotating with the continuum material element.

#### The Green-Naghdi Rate

The **Green-Naghdi rate** takes a different approach. It considers the **[polar decomposition](@entry_id:149541)** of the [deformation gradient](@entry_id:163749), $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$, where $\boldsymbol{R}$ is a proper orthogonal tensor representing the rotation of the material element's [principal axes of strain](@entry_id:188315), and $\boldsymbol{U}$ is the symmetric [right stretch tensor](@entry_id:193756). The Green-Naghdi rate uses the spin of this material rotation, $\boldsymbol{\Omega}_{\boldsymbol{R}} = \dot{\boldsymbol{R}}\boldsymbol{R}^{\mathsf{T}}$. This spin also satisfies the required transformation rule, making the corresponding rate objective.

The Green-Naghdi rate is defined as:
$$
\boldsymbol{\sigma}^{\nabla {GN}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\Omega}_{\boldsymbol{R}}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\Omega}_{\boldsymbol{R}}
$$
This rate measures the change of stress in a frame that co-rotates with the principal axes of material stretch. Since $\boldsymbol{W}$ and $\boldsymbol{\Omega}_{\boldsymbol{R}}$ are generally not identical, the Jaumann and Green-Naghdi rates represent distinct physical quantities.

### Convected Rates: The Truesdell Rate

Another major class of [objective rates](@entry_id:198692) arises from a more abstract consideration of how tensor quantities are "pulled back" to the reference configuration, where time differentiation is performed, and then "pushed forward" to the current configuration. These are known as **convected rates**.

The most prominent example is the **Truesdell rate** of the Cauchy stress, which is closely related to the **Oldroyd [upper-convected derivative](@entry_id:756365)**. For a general second-order tensor field $\boldsymbol{A}$, the Oldroyd [upper-convected derivative](@entry_id:756365) is defined as:
$$
\overset{\triangledown}{\boldsymbol{A}} = \dot{\boldsymbol{A}} - \boldsymbol{L}\boldsymbol{A} - \boldsymbol{A}\boldsymbol{L}^{\mathsf{T}}
$$
This rate can be shown to be objective through a direct, albeit tedious, application of the transformation rules for $\dot{\boldsymbol{A}}$ and $\boldsymbol{L}$. The Truesdell rate of the Cauchy stress is a slight variation, given by:
$$
\boldsymbol{\sigma}^{\nabla T} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{L}^{\mathsf{T}} + (\mathrm{tr}\boldsymbol{D})\boldsymbol{\sigma}
$$
This rate also proves to be objective and is often used in models of [viscoelastic fluids](@entry_id:198948) and in certain formulations of plasticity.

### Comparison and Physical Interpretation

The existence of multiple [objective rates](@entry_id:198692) raises a critical question: which one is "correct"? The answer is that they are all mathematically valid, but they represent different physical perspectives and lead to different predictions in [constitutive models](@entry_id:174726).

A baseline test for any objective rate is its behavior during a [rigid body motion](@entry_id:144691). If a material is undergoing a pure rigid rotation with [velocity field](@entry_id:271461) $\boldsymbol{v} = \boldsymbol{\omega} \times \boldsymbol{x}$ (where $\boldsymbol{\omega}$ is the angular velocity vector), then the [velocity gradient](@entry_id:261686) $\boldsymbol{L}$ is purely skew-symmetric, such that $\boldsymbol{L} = \boldsymbol{W}$ and $\boldsymbol{D} = \mathbf{0}$. If a stress field $\boldsymbol{\sigma}(t)$ is simply being carried along by this rotation (i.e., it is constant in a [co-rotating frame](@entry_id:146008)), then its [material time derivative](@entry_id:190892) is $\dot{\boldsymbol{\sigma}} = \boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}$. Substituting this into the definitions of the Jaumann, Green-Naghdi, and Truesdell rates reveals that all three vanish: $\boldsymbol{\sigma}^{\nabla J} = \boldsymbol{\sigma}^{\nabla {GN}} = \boldsymbol{\sigma}^{\nabla T} = \mathbf{0}$. This is a crucial consistency check: an objective rate must register zero change for a stress that is merely being reoriented by a rigid rotation.

However, in a general deformation involving stretch ($\boldsymbol{D} \neq \mathbf{0}$), the rates differ. The difference between the Truesdell and Jaumann rates is:
$$
\boldsymbol{\sigma}^{\nabla T} - \boldsymbol{\sigma}^{\nabla J} = (\mathrm{tr}\boldsymbol{D})\boldsymbol{\sigma} - (\boldsymbol{D}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{D})
$$
This difference depends explicitly on the rate of deformation $\boldsymbol{D}$. The difference between the Green-Naghdi and Jaumann rates is even more physically insightful:
$$
\boldsymbol{\sigma}^{\nabla {GN}} - \boldsymbol{\sigma}^{\nabla J} = [\boldsymbol{\sigma}, \boldsymbol{\Omega}_{\boldsymbol{R}} - \boldsymbol{W}]
$$
The difference is the commutator of the stress with the difference in spins, $\boldsymbol{\Omega}_{\boldsymbol{R}} - \boldsymbol{W}$. The spatial spin $\boldsymbol{W}$ represents the average rotation of a material element, while the material spin $\boldsymbol{\Omega}_{\boldsymbol{R}}$ represents the rotation of the [principal axes of strain](@entry_id:188315). The difference $\boldsymbol{\Omega}_{\boldsymbol{R}} - \boldsymbol{W}$ is non-zero when the principal axes of stretch rotate relative to the material itself. It can be shown that this occurs if and only if the [right stretch tensor](@entry_id:193756) $\boldsymbol{U}$ and its [material time derivative](@entry_id:190892) $\dot{\boldsymbol{U}}$ are not coaxial (i.e., do not share the same principal directions).

### Implications for Constitutive Modeling and Hypoelasticity

These differences have profound consequences. When we formulate a **hypoelastic** constitutive law of the form $\mathring{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$, the choice of the objective rate $\mathring{\boldsymbol{\sigma}}$ will dictate the predicted [stress response](@entry_id:168351) for a given deformation history.

An important subtlety arises when considering the evolution of [principal stresses](@entry_id:176761). If we analyze the difference between the Green-Naghdi and Jaumann rates in the principal basis of the stress tensor $\boldsymbol{\sigma}$, the difference tensor $[\boldsymbol{\sigma}, \boldsymbol{\Omega}_{\boldsymbol{R}} - \boldsymbol{W}]$ is found to be purely off-diagonal. This means its diagonal components are zero. Consequently, in an isotropic [hypoelastic model](@entry_id:750490), the predicted instantaneous rates of change of the [principal stress](@entry_id:204375) values, $\dot{s}_i$, are identical whether the Jaumann or Green-Naghdi rate is used. The choice of rate affects the predicted rate of rotation of the [principal stress](@entry_id:204375) axes, but not the rate of change of the principal stress magnitudes themselves.

A final, crucial consideration is that of **[integrability](@entry_id:142415)**. A truly elastic material is **hyperelastic**, meaning its stress state is uniquely determined by its current deformation state, derivable from a stored elastic energy potential. Hypoelastic laws, being rate-based, must be integrated over a deformation history to find the final stress. The question is whether this integration is path-independent. If not, the material is not hyperelastic.

It is a famous result that the simple Jaumann-rate model, $\boldsymbol{\sigma}^{\nabla J} = \lambda(\mathrm{tr}\boldsymbol{D})\boldsymbol{I} + 2\mu\boldsymbol{D}$, is generally *not* integrable. When subjected to a finite simple [shear deformation](@entry_id:170920), this law predicts an unphysical oscillatory shear [stress response](@entry_id:168351), demonstrating that the stress depends on the deformation path, not just the final configuration. This pathological behavior reveals that objectivity, while necessary, is not sufficient to guarantee a physically realistic elastic model. Path-independence for this model is recovered only for special classes of motion, such as irrotational pure stretches where $\boldsymbol{W}=\mathbf{0}$. This limitation of simple hypoelastic formulations has motivated the development of more sophisticated constitutive theories for large-deformation elasticity.