## Introduction
In the field of continuum mechanics, accurately describing a material's response under [large deformations](@entry_id:167243) and rotations is a central challenge. A cornerstone of any valid physical theory is that the constitutive laws governing material behavior must be independent of the observer's frame of reference. This concept, known as the [principle of material frame-indifference](@entry_id:188488), is violated when using the simple [material time derivative](@entry_id:190892) of stress in rate-type [constitutive models](@entry_id:174726). This fundamental failing can lead to the prediction of non-physical stresses and highlights a critical knowledge gap that must be addressed for robust modeling. This article provides a comprehensive exploration of objective stress rates—the essential mathematical tools designed to solve this problem.

Across the following chapters, you will gain a deep understanding of this advanced topic. The "Principles and Mechanisms" chapter will first establish why objectivity is necessary and demonstrate the non-objectivity of the standard time derivative, then detail the construction of various [objective rates](@entry_id:198692) like the Jaumann, Green-Naghdi, and Truesdell rates. Following this, the "Applications and Interdisciplinary Connections" chapter will explore the profound consequences of choosing a specific rate in fields like plasticity and computational mechanics, weighing the pros and cons of [hypoelastic models](@entry_id:184632) against modern hyperelastic frameworks. Finally, the "Hands-On Practices" chapter will offer practical problems to solidify your command of these concepts. We will begin by examining the fundamental principles that mandate the use of these specialized rates.

## Principles and Mechanisms

In formulating [constitutive laws](@entry_id:178936) for materials undergoing large deformations, a central challenge is to ensure that these laws are independent of the observer. A physical response, such as stress, should not depend on the arbitrary motion of the frame of reference from which it is measured. This fundamental principle, known as the **[principle of material frame-indifference](@entry_id:188488)** or **[material objectivity](@entry_id:177919)**, imposes rigorous mathematical constraints on the structure of our [constitutive equations](@entry_id:138559). When we consider rate-type material models, where the rate of change of stress is related to the rate of deformation, this principle mandates the use of specialized time derivatives known as **objective stress rates**. This chapter elucidates the necessity, construction, and properties of these essential tools in continuum mechanics.

### The Principle of Material Frame-Indifference

Let us begin by formalizing the concept of an observer. We consider two observers, one in a "stationary" frame and another in a "moving" frame. The position of a material point $\boldsymbol{x}$ at time $t$ in the stationary frame is related to its position $\boldsymbol{x}^*$ in the [moving frame](@entry_id:274518) by a superposed [rigid body motion](@entry_id:144691):

$$
\boldsymbol{x}^*(t) = \boldsymbol{c}(t) + \boldsymbol{Q}(t)\boldsymbol{x}(t)
$$

Here, $\boldsymbol{c}(t)$ is a time-dependent translation vector, and $\boldsymbol{Q}(t)$ is a time-dependent **proper orthogonal tensor** ($\boldsymbol{Q}^T\boldsymbol{Q} = \boldsymbol{I}$ and $\det(\boldsymbol{Q})=1$), representing the rotation of the moving frame relative to the stationary one.

The [principle of material frame-indifference](@entry_id:188488) states that a [constitutive equation](@entry_id:267976) must have the same form for all observers. A physical quantity is said to be **objective** if its value in the moving frame is related to its value in the stationary frame solely through the [geometric transformation](@entry_id:167502) appropriate for its tensorial order. For a vector $\boldsymbol{v}$ and a second-order tensor $\boldsymbol{T}$, this means:

$$
\boldsymbol{v}^* = \boldsymbol{Q}\boldsymbol{v} \quad \text{and} \quad \boldsymbol{T}^* = \boldsymbol{Q}\boldsymbol{T}\boldsymbol{Q}^T
$$

This transformation rule is the definition of an objective tensor [@problem_id:2666106]. Consider a [constitutive law](@entry_id:167255) relating the Cauchy stress $\boldsymbol{\sigma}$ to the rate of deformation $\boldsymbol{D}$, expressed by a function $\mathcal{H}$ as $\boldsymbol{\sigma} = \mathcal{H}(\boldsymbol{D})$. For this law to be frame-indifferent, it must hold in the moving frame as well, i.e., $\boldsymbol{\sigma}^* = \mathcal{H}(\boldsymbol{D}^*)$. As can be shown by deriving the transformation rules for the relevant kinematic quantities, both the Cauchy stress $\boldsymbol{\sigma}$ and the [rate of deformation tensor](@entry_id:182598) $\boldsymbol{D}$ are objective tensors, meaning $\boldsymbol{\sigma}^* = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T$ and $\boldsymbol{D}^* = \boldsymbol{Q}\boldsymbol{D}\boldsymbol{Q}^T$ [@problem_id:2905934]. Substituting these into the [constitutive law](@entry_id:167255) yields the condition that the function $\mathcal{H}$ must satisfy:

$$
\boldsymbol{Q}\mathcal{H}(\boldsymbol{D})\boldsymbol{Q}^T = \mathcal{H}(\boldsymbol{Q}\boldsymbol{D}\boldsymbol{Q}^T)
$$

This is the mathematical statement of [frame-indifference](@entry_id:197245) for this class of [constitutive laws](@entry_id:178936), which requires the constitutive function to be an [isotropic tensor](@entry_id:189108) function of its arguments [@problem_id:2666103].

### The Non-Objectivity of the Material Time Derivative

In the development of **rate-type [constitutive models](@entry_id:174726)**, such as those used in [hypoelasticity](@entry_id:204371) or [elastoplasticity](@entry_id:193198), we seek a relationship of the form:

$$
\text{rate of stress} = \mathbb{C} : \boldsymbol{D}
$$

where $\mathbb{C}$ is a fourth-order tensor of material moduli. A natural candidate for the "rate of stress" is the [material time derivative](@entry_id:190892) of the Cauchy stress, $\dot{\boldsymbol{\sigma}}$. However, a critical problem arises: the [material time derivative](@entry_id:190892) is not an objective quantity.

To demonstrate this, we differentiate the transformation rule for the Cauchy stress, $\boldsymbol{\sigma}^* = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T$, with respect to time, applying the product rule:

$$
\dot{\boldsymbol{\sigma}}^* = \frac{d}{dt}(\boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T) = \dot{\boldsymbol{Q}}\boldsymbol{\sigma}\boldsymbol{Q}^T + \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^T + \boldsymbol{Q}\boldsymbol{\sigma}\dot{\boldsymbol{Q}}^T
$$

Let us define the **spin of the observer's frame** as the [skew-symmetric tensor](@entry_id:199349) $\boldsymbol{\Omega} = \dot{\boldsymbol{Q}}\boldsymbol{Q}^T$. Using this definition and the relations $\boldsymbol{\sigma} = \boldsymbol{Q}^T\boldsymbol{\sigma}^*\boldsymbol{Q}$ and $\dot{\boldsymbol{Q}}^T = -\boldsymbol{Q}^T\boldsymbol{\Omega}$, the expression can be rewritten as:

$$
\dot{\boldsymbol{\sigma}}^* = \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^T + \boldsymbol{\Omega}\boldsymbol{\sigma}^* - \boldsymbol{\sigma}^*\boldsymbol{\Omega}
$$

The transformation rule for $\dot{\boldsymbol{\sigma}}$ contains additional terms, $[\boldsymbol{\Omega}, \boldsymbol{\sigma}^*] = \boldsymbol{\Omega}\boldsymbol{\sigma}^* - \boldsymbol{\sigma}^*\boldsymbol{\Omega}$, that depend on the observer's spin $\boldsymbol{\Omega}$. Since these terms are generally non-zero, $\dot{\boldsymbol{\sigma}}^*$ does not transform as an objective tensor, i.e., $\dot{\boldsymbol{\sigma}}^* \neq \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^T$. Therefore, the [material time derivative](@entry_id:190892) $\dot{\boldsymbol{\sigma}}$ is **not objective** [@problem_id:2905931].

The physical consequence of this mathematical failure is profound. Consider a simple [hypoelastic model](@entry_id:750490) using this non-objective rate, $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$. If we subject a body to a pure rigid rotation, the deformation is zero ($\boldsymbol{D}=\boldsymbol{0}$), so the model predicts $\dot{\boldsymbol{\sigma}}=\boldsymbol{0}$. This means the components of the stress tensor in the [laboratory frame](@entry_id:166991) remain constant. Physically, however, the stress tensor represents an intrinsic material property that should rotate with the body. The non-objective model fails to capture this rotation and instead predicts the generation of spurious, non-physical stresses required to keep the stress tensor fixed in the [laboratory frame](@entry_id:166991) [@problem_id:2666090]. This demonstrates that a [constitutive model](@entry_id:747751) of the form $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$ violates the [principle of material frame-indifference](@entry_id:188488).

### Construction of Objective Rates

To resolve this issue, we must construct a new definition of a stress rate that is, by construction, objective. The non-objective terms in the transformation of $\dot{\boldsymbol{\sigma}}$ arise because the [material time derivative](@entry_id:190892) measures changes with respect to a fixed [laboratory frame](@entry_id:166991), thus confounding the intrinsic change in stress with the apparent change due to the material's rotation. An objective rate should measure the change of stress in a frame that **corotates** with the material.

This leads to the concept of a **[corotational stress rate](@entry_id:747894)**, generally defined as:

$$
\mathring{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\Lambda}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\Lambda}
$$

Here, $\boldsymbol{\Lambda}$ is a [skew-symmetric tensor](@entry_id:199349) representing the spin of the chosen corotating frame. For $\mathring{\boldsymbol{\sigma}}$ to be objective, the [spin tensor](@entry_id:187346) $\boldsymbol{\Lambda}$ cannot be objective itself. Instead, it must transform in a specific way that precisely cancels the non-objective terms from $\dot{\boldsymbol{\sigma}}$. The required transformation rule for $\boldsymbol{\Lambda}$ is [@problem_id:2666126]:

$$
\boldsymbol{\Lambda}^* = \boldsymbol{Q}\boldsymbol{\Lambda}\boldsymbol{Q}^T + \boldsymbol{\Omega}
$$

This shows that the spin measured by the moving observer, $\boldsymbol{\Lambda}^*$, is the sum of the rotated material spin, $\boldsymbol{Q}\boldsymbol{\Lambda}\boldsymbol{Q}^T$, and the observer's own spin, $\boldsymbol{\Omega}$. By choosing a [spin tensor](@entry_id:187346) $\boldsymbol{\Lambda}$ that satisfies this transformation property, the resulting [corotational rate](@entry_id:193173) $\mathring{\boldsymbol{\sigma}}$ becomes objective, satisfying $\mathring{\boldsymbol{\sigma}}^* = \boldsymbol{Q}\mathring{\boldsymbol{\sigma}}\boldsymbol{Q}^T$. A [constitutive model](@entry_id:747751) of the form $\mathring{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$ can then be frame-indifferent, as both sides of the equation are objective tensors [@problem_id:2905949].

### A Menagerie of Objective Rates

The choice of the corotating spin $\boldsymbol{\Lambda}$ is not unique, leading to a variety of different objective stress rates used in the literature. Each represents a different physical assumption about the appropriate [rotating frame](@entry_id:155637) to use as a reference.

#### The Jaumann Rate

Perhaps the most common choice for the corotating spin is the material's own **[spin tensor](@entry_id:187346)**, $\boldsymbol{W}$, which is the skew-symmetric part of the velocity gradient $\boldsymbol{L} = \nabla\boldsymbol{v}$.
$$
\boldsymbol{\Lambda} = \boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^T)
$$
The [spin tensor](@entry_id:187346) $\boldsymbol{W}$ can be shown to satisfy the required transformation rule $\boldsymbol{W}^* = \boldsymbol{Q}\boldsymbol{W}\boldsymbol{Q}^T + \boldsymbol{\Omega}$ [@problem_id:2905934]. The resulting objective rate is the **Jaumann rate** (or Zaremba-Jaumann rate), denoted $\boldsymbol{\sigma}^{\nabla J}$:
$$
\boldsymbol{\sigma}^{\nabla J} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}
$$

#### The Green-Naghdi Rate

Another choice is to use the spin of the [rotation tensor](@entry_id:191990) $\boldsymbol{R}$ from the [polar decomposition](@entry_id:149541) of the [deformation gradient](@entry_id:163749) ($\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$). This spin is defined as $\boldsymbol{\Omega}_{GN} = \dot{\boldsymbol{R}}\boldsymbol{R}^T$.
$$
\boldsymbol{\Lambda} = \boldsymbol{\Omega}_{GN} = \dot{\boldsymbol{R}}\boldsymbol{R}^T
$$
This spin also satisfies the objectivity condition, leading to the **Green-Naghdi rate**, $\boldsymbol{\sigma}^{\nabla G}$:
$$
\boldsymbol{\sigma}^{\nabla G} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\Omega}_{GN}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\Omega}_{GN}
$$
This rate measures stress changes relative to a frame defined by the material's rigid rotation part of its deformation.

#### The Truesdell Rate

The **Truesdell rate**, $\boldsymbol{\sigma}^{\nabla T}$, is constructed differently and is not of the simple corotational form shown above. It is derived from the [material time derivative](@entry_id:190892) of the second Piola-Kirchhoff stress, pushed forward to the current configuration. In terms of Cauchy stress, it is defined as:
$$
\boldsymbol{\sigma}^{\nabla T} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{L}^T + (\text{tr}(\boldsymbol{D}))\boldsymbol{\sigma}
$$
where $\boldsymbol{L}$ is the full velocity gradient. Despite its different structure, the Truesdell rate can be rigorously shown to be objective [@problem_id:2905949].

A fundamental property shared by all valid [objective rates](@entry_id:198692) is that they vanish for a pure [rigid body motion](@entry_id:144691) where no actual [material deformation](@entry_id:169356) occurs. For a motion where $\boldsymbol{F}(t)=\boldsymbol{R}(t)$, it can be shown that $\boldsymbol{\sigma}^{\nabla J} = \boldsymbol{0}$, $\boldsymbol{\sigma}^{\nabla G} = \boldsymbol{0}$, and $\boldsymbol{\sigma}^{\nabla T} = \boldsymbol{0}$. This confirms that they correctly register "no change" when the material is simply rotating without straining, unlike the non-objective [material time derivative](@entry_id:190892) [@problem_id:2905958].

### Comparison and Consequences

Since multiple [objective rates](@entry_id:198692) exist, a crucial question arises: does the choice of rate matter? The answer is yes. Different [objective rates](@entry_id:198692) lead to different predictions in [constitutive models](@entry_id:174726), especially under large shear deformations.

Comparing the **Truesdell and Jaumann rates**, we find their difference is given by:
$$
\boldsymbol{\sigma}^{\nabla T} - \boldsymbol{\sigma}^{\nabla J} = (\text{tr}(\boldsymbol{D}))\boldsymbol{\sigma} - (\boldsymbol{D}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{D})
$$
This difference depends on both the stress $\boldsymbol{\sigma}$ and the rate of deformation $\boldsymbol{D}$. For a [simple shear](@entry_id:180497) flow, for example, this difference can be significant, meaning a hypoelastic material model using the Jaumann rate will predict a different [stress response](@entry_id:168351) than one using the Truesdell rate [@problem_id:2666095].

A more subtle and insightful comparison exists between the **Jaumann and Green-Naghdi rates**. Their difference is:
$$
\boldsymbol{\sigma}^{\nabla G} - \boldsymbol{\sigma}^{\nabla J} = [\boldsymbol{\sigma}, (\boldsymbol{\Omega}_{GN} - \boldsymbol{W})]
$$
where the square brackets denote the commutator. A key property of a commutator of a [symmetric tensor](@entry_id:144567) ($\boldsymbol{\sigma}$) with a [skew-symmetric tensor](@entry_id:199349) ($\boldsymbol{\Omega}_{GN} - \boldsymbol{W}$) is that its diagonal components are zero in the principal basis of the [symmetric tensor](@entry_id:144567).

This has a profound consequence for isotropic [hypoelastic models](@entry_id:184632) of the form $\mathring{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$. The rate of change of the principal stress values, $\dot{s}_i$, depends only on the diagonal components of $\dot{\boldsymbol{\sigma}}$, which in turn depend only on the diagonal components of the chosen objective rate $\mathring{\boldsymbol{\sigma}}$. Since the difference between the Jaumann and Green-Naghdi rates has zero on its diagonal in the [principal stress](@entry_id:204375) basis, the two rates give the *exact same prediction* for the evolution of the [principal stress](@entry_id:204375) magnitudes. The difference lies entirely in the off-diagonal terms, which govern the predicted rate of rotation of the principal stress axes [@problem_id:2666116]. This highlights that the choice of objective rate is fundamentally a choice about how to model the evolution of [material anisotropy](@entry_id:204117) or, in this case, the orientation of the [principal stress](@entry_id:204375) state.

In summary, the [principle of material frame-indifference](@entry_id:188488) is a non-negotiable cornerstone of continuum mechanics. For rate-type [constitutive laws](@entry_id:178936), this principle forbids the use of the simple [material time derivative](@entry_id:190892) and necessitates the use of objective stress rates. The construction of these rates involves correcting for material spin, but the choice of spin is not unique. This leads to a variety of [objective rates](@entry_id:198692), such as the Jaumann, Green-Naghdi, and Truesdell rates, each with distinct properties. The differences between these rates are not merely academic; they lead to different predictions for material behavior, particularly concerning the evolution of principal stress directions under [large deformation](@entry_id:164402). The selection of the most appropriate rate for a given material and application remains a subject of careful consideration in advanced [material modeling](@entry_id:173674).