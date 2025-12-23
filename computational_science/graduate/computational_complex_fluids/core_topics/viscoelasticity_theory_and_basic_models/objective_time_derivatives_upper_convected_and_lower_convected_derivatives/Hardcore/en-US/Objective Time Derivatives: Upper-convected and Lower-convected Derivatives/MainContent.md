## Introduction
Modeling the flow of complex materials like polymer melts and biological fluids requires [constitutive equations](@entry_id:138559) that relate stress to deformation history. A cornerstone of this field is the principle that these physical laws must be independent of the observer, a concept known as [material frame-indifference](@entry_id:178419). While the [material time derivative](@entry_id:190892) seems the natural choice for describing how tensor quantities like stress evolve, it fundamentally violates this principle, yielding different results for observers in relative rotation. This failure presents a major obstacle in continuum mechanics, necessitating a more sophisticated mathematical framework.

This article tackles this challenge by introducing [objective time derivatives](@entry_id:189677), the essential tools for creating physically valid constitutive models. The first chapter, "Principles and Mechanisms," establishes the theoretical foundation, demonstrating why the [material derivative](@entry_id:266939) fails and how [objective rates](@entry_id:198692) like the upper- and lower-convected derivatives are constructed from flow kinematics. The second chapter, "Applications and Interdisciplinary Connections," explores how these derivatives are used in foundational [viscoelastic models](@entry_id:192483), linking theoretical choices to predictable material behaviors, computational challenges like the High-Weissenberg Number Problem, and applications in fields from polymer science to geophysics. Finally, "Hands-On Practices" provides targeted exercises to solidify understanding of these abstract concepts through practical calculation and numerical thinking. We begin by delving into the [principle of material frame-indifference](@entry_id:188488) and its profound consequences for the mathematics of [complex fluids](@entry_id:198415).

## Principles and Mechanisms

In the study of continuum mechanics, particularly for complex fluids exhibiting elastic and viscous properties, constitutive models are essential for relating stress to deformation and flow history. A fundamental requirement for any physically valid [constitutive law](@entry_id:167255) is the **[principle of material frame-indifference](@entry_id:188488)** (MFI), also known as the [principle of material objectivity](@entry_id:191727). This principle, articulated by Noll, posits that the constitutive response of a material should be independent of the observer. An observer's frame of reference might be translating or rotating, but these rigid-body motions should not alter the intrinsic material properties being modeled . This chapter explores the mathematical consequences of this principle for time derivatives of tensor quantities, leading to the formulation of [objective rates](@entry_id:198692) essential for modeling complex fluids.

### The Requirement of Objectivity and the Failure of the Material Derivative

To formalize the principle of MFI, we consider two observers. The position of a material point as seen by the first observer is $\boldsymbol{x}$, and by the second observer is $\boldsymbol{x}^*$. A change of frame is described by a superposed [rigid-body motion](@entry_id:265795):
$$
\boldsymbol{x}^*(t) = \boldsymbol{Q}(t)\boldsymbol{x}(t) + \boldsymbol{c}(t)
$$
where $\boldsymbol{c}(t)$ is a time-dependent translation vector, and $\boldsymbol{Q}(t)$ is a time-dependent proper orthogonal tensor, satisfying $\boldsymbol{Q}(t)\boldsymbol{Q}^T(t) = \boldsymbol{I}$ and $\det(\boldsymbol{Q}) = 1$, representing a rotation.

Physical quantities must transform between frames in a consistent manner. A scalar is invariant, a vector transforms as $\boldsymbol{u}^* = \boldsymbol{Q}\boldsymbol{u}$, and a second-order [spatial tensor](@entry_id:185799), such as the Cauchy stress tensor $\boldsymbol{\sigma}$ or a polymer [conformation tensor](@entry_id:1122882) $\boldsymbol{A}$, must transform according to the rule:
$$
\boldsymbol{A}^*(\boldsymbol{x}^*, t) = \boldsymbol{Q}(t) \boldsymbol{A}(\boldsymbol{x}, t) \boldsymbol{Q}^T(t)
$$
This transformation rule ensures that the tensor's physical meaning is preserved regardless of the observer's orientation.

A [constitutive model](@entry_id:747751) often involves a time derivative of a tensor. For the [constitutive equation](@entry_id:267976) itself to be frame-indifferent, any operator within it, including the time derivative, must also be objective. An objective time-derivative operator, which we denote by $\mathcal{D}$, must yield a result that transforms as a proper tensor. That is, if $\mathcal{D}[\boldsymbol{A}]$ is the rate of change of $\boldsymbol{A}$ in the original frame, and $(\mathcal{D}[\boldsymbol{A}])^*$ is the rate in the new frame (constructed with the new frame's kinematics), the objectivity requirement is :
$$
(\mathcal{D}[\boldsymbol{A}])^* = \boldsymbol{Q}(t) (\mathcal{D}[\boldsymbol{A}]) \boldsymbol{Q}^T(t)
$$

The most intuitive time derivative is the **[material time derivative](@entry_id:190892)**, which measures the rate of change of a quantity following a material particle. For a [spatial tensor](@entry_id:185799) field $\boldsymbol{A}(\boldsymbol{x},t)$, it is defined as:
$$
\dot{\boldsymbol{A}} = \frac{D\boldsymbol{A}}{Dt} = \frac{\partial \boldsymbol{A}}{\partial t} + (\boldsymbol{v} \cdot \nabla)\boldsymbol{A}
$$
where $\boldsymbol{v}$ is the fluid velocity. Despite its clear physical meaning, the material derivative is not objective. We can demonstrate this by taking the material derivative of the [tensor transformation rule](@entry_id:185176) $\boldsymbol{A}^* = \boldsymbol{Q}\boldsymbol{A}\boldsymbol{Q}^T$:
$$
\dot{\boldsymbol{A}}^* = \frac{D}{Dt}(\boldsymbol{Q}\boldsymbol{A}\boldsymbol{Q}^T) = \dot{\boldsymbol{Q}}\boldsymbol{A}\boldsymbol{Q}^T + \boldsymbol{Q}\dot{\boldsymbol{A}}\boldsymbol{Q}^T + \boldsymbol{Q}\boldsymbol{A}\dot{\boldsymbol{Q}}^T
$$
Introducing the [spin tensor](@entry_id:187346) of the superposed rotation, $\boldsymbol{W}^*(t) = \dot{\boldsymbol{Q}}\boldsymbol{Q}^T$, which is skew-symmetric ($\boldsymbol{W}^{*T} = -\boldsymbol{W}^*$), we can rewrite the transformation as:
$$
\dot{\boldsymbol{A}}^* = \boldsymbol{W}^*\boldsymbol{A}^* + \boldsymbol{Q}\dot{\boldsymbol{A}}\boldsymbol{Q}^T - \boldsymbol{A}^*\boldsymbol{W}^*
$$
The objectivity condition $\dot{\boldsymbol{A}}^* = \boldsymbol{Q}\dot{\boldsymbol{A}}\boldsymbol{Q}^T$ is violated by the presence of the terms $\boldsymbol{W}^*\boldsymbol{A}^* - \boldsymbol{A}^*\boldsymbol{W}^*$. These terms represent the apparent rate of change of $\boldsymbol{A}$ due solely to the rotation of the observer's frame. For instance, if a [tensor field](@entry_id:266532) $\boldsymbol{A}$ is constant in the un-rotated frame ($\dot{\boldsymbol{A}} = \boldsymbol{0}$), an observer in a rotating frame ($\boldsymbol{W}^* \neq \boldsymbol{0}$) would measure a non-zero rate of change $\dot{\boldsymbol{A}}^* = \boldsymbol{W}^*\boldsymbol{A}^* - \boldsymbol{A}^*\boldsymbol{W}^*$. This is physically unacceptable for a constitutive law; a material's state cannot depend on how we choose to look at it .

### Kinematic Foundations for Objective Rates

To construct an objective derivative, we must subtract correction terms from the material derivative $\dot{\boldsymbol{A}}$ that precisely cancel the spurious rotational contributions. These correction terms must be built from the flow's own kinematic properties. The key kinematic quantity is the **[velocity gradient tensor](@entry_id:270928)**, $\boldsymbol{L} = \nabla\boldsymbol{v}$. It can be decomposed into its symmetric and anti-symmetric parts:

*   The **[rate-of-deformation tensor](@entry_id:184787)**, $\boldsymbol{D} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^T)$, which describes local stretching and shearing rates.
*   The **[vorticity tensor](@entry_id:189621)** (or [spin tensor](@entry_id:187346)), $\boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^T)$, which describes the local angular velocity of the fluid.

To understand how to use these tensors for correction, we must know how they transform under a superposed [rigid-body motion](@entry_id:265795). Through a standard kinematic derivation, one can show their transformation rules are :
$$
\boldsymbol{L}^* = \boldsymbol{Q}\boldsymbol{L}\boldsymbol{Q}^T + \boldsymbol{W}^*
$$
$$
\boldsymbol{D}^* = \boldsymbol{Q}\boldsymbol{D}\boldsymbol{Q}^T
$$
This analysis reveals a critical insight: the [rate-of-deformation tensor](@entry_id:184787) $\boldsymbol{D}$ is itself an objective tensor. In contrast, the [velocity gradient](@entry_id:261686) $\boldsymbol{L}$ and the [vorticity tensor](@entry_id:189621) $\boldsymbol{W}$ are not objective; their transformation laws pick up the spin $\boldsymbol{W}^*$ of the superposed rotation. This "flaw" in their transformation is precisely what can be exploited to correct the non-objectivity of the material derivative.

### A Family of Objective Derivatives

By combining the material derivative $\dot{\boldsymbol{A}}$ with terms involving $\boldsymbol{L}$ and its components, we can construct an infinite number of [objective rates](@entry_id:198692). Three of these are most prominent in the literature due to their physical and geometric interpretations.

#### The Corotational (Jaumann) Derivative
The simplest way to achieve objectivity is to remove the apparent rotation of the tensor $\boldsymbol{A}$ caused by the local [fluid rotation](@entry_id:273789) $\boldsymbol{W}$. This leads to the **corotational** or **Jaumann derivative**, defined as :
$$
\overset{\circ}{\boldsymbol{A}} = \dot{\boldsymbol{A}} - \boldsymbol{W}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{W}
$$
This derivative measures the rate of change of $\boldsymbol{A}$ in a frame that is co-rotating with the local angular velocity of the fluid. Its correction term, $-\boldsymbol{W}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{W}$, precisely cancels the spurious spin contribution from a superposed rotation.

#### The Convected Derivatives
Two other crucial [objective rates](@entry_id:198692) are the upper- and lower-convected derivatives. They are not only objective but are also deeply connected to the deformation of the material itself.

The **[upper-convected derivative](@entry_id:756365)**, also known as the Oldroyd-A derivative, is defined as :
$$
\stackrel{\nabla}{\boldsymbol{A}} = \dot{\boldsymbol{A}} - \boldsymbol{L}\boldsymbol{A} - \boldsymbol{A}\boldsymbol{L}^T
$$

The **[lower-convected derivative](@entry_id:1127499)**, sometimes called the Oldroyd-B derivative, is defined as :
$$
\stackrel{\triangle}{\boldsymbol{A}} = \dot{\boldsymbol{A}} + \boldsymbol{L}^T\boldsymbol{A} + \boldsymbol{A}\boldsymbol{L}
$$

A proof of objectivity for these derivatives follows by substituting the transformation rules for $\dot{\boldsymbol{A}}$ and $\boldsymbol{L}$ into their definitions in the starred frame. The non-objective terms involving $\boldsymbol{W}^*$ from the observer's rotation invariably cancel out, satisfying the objectivity criterion .

The relationship between these three rates becomes clearer when the convected derivatives are expressed in terms of $\boldsymbol{D}$ and $\boldsymbol{W}$. Substituting $\boldsymbol{L} = \boldsymbol{D} + \boldsymbol{W}$ into their definitions reveals :
$$
\stackrel{\nabla}{\boldsymbol{A}} = (\dot{\boldsymbol{A}} - \boldsymbol{W}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{W}) - (\boldsymbol{D}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{D}) = \overset{\circ}{\boldsymbol{A}} - (\boldsymbol{D}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{D})
$$
$$
\stackrel{\triangle}{\boldsymbol{A}} = (\dot{\boldsymbol{A}} - \boldsymbol{W}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{W}) + (\boldsymbol{D}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{D}) = \overset{\circ}{\boldsymbol{A}} + (\boldsymbol{D}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{D})
$$
This decomposition elegantly shows that all three derivatives correct for local [fluid rotation](@entry_id:273789) in the same way (the Jaumann part). They differ only in how they account for the rate of deformation $\boldsymbol{D}$. The [upper-convected derivative](@entry_id:756365) subtracts the stretching contribution, while the [lower-convected derivative](@entry_id:1127499) adds it. This difference is not arbitrary; it is tied to the fundamental geometric nature of the tensor being differentiated.

### Geometric and Microstructural Interpretation

The choice of which objective derivative to use in a constitutive model is not a matter of preference but a physical modeling decision. The correct choice depends on the nature of the tensor quantity being described. This is best understood through the geometric interpretation of the convected derivatives, which connects them to how material line segments and surface elements are transported and deformed by the flow.

#### The Upper-Convected Derivative: Frame of Line Elements
The upper-convected derivative is the natural rate for **contravariant** tensors. These are tensors associated with the deformation of material **line elements**. A prime example is the configuration tensor $\boldsymbol{C} = \langle \boldsymbol{q} \otimes \boldsymbol{q} \rangle$ in a polymer model, where $\boldsymbol{q}$ is the end-to-end vector of a polymer chain. Since $\boldsymbol{q}$ is a material line segment, $\boldsymbol{C}$ is a contravariant tensor, and its objective evolution must be described by the [upper-convected derivative](@entry_id:756365) .

The deeper geometric meaning comes from considering the deformation mapping $\boldsymbol{x} = \boldsymbol{\chi}(\boldsymbol{X}, t)$, where $\boldsymbol{X}$ is a material point in a reference configuration. Let $\boldsymbol{F} = \nabla_X \boldsymbol{\chi}$ be the deformation gradient. A spatial contravariant tensor $\boldsymbol{A}$ can be "pulled back" to a [material tensor](@entry_id:196294) in the reference configuration via the transformation $\boldsymbol{A}_R = \boldsymbol{F}^{-1} \boldsymbol{A} \boldsymbol{F}^{-T}$. The rate of change of this [material tensor](@entry_id:196294) is simply its partial time derivative $\partial \boldsymbol{A}_R / \partial t$. If we "push forward" this rate back to the spatial frame, we obtain the [upper-convected derivative](@entry_id:756365) :
$$
\stackrel{\nabla}{\boldsymbol{A}} = \boldsymbol{F} \left( \frac{\partial \boldsymbol{A}_R}{\partial t} \right) \boldsymbol{F}^T
$$
This means the [upper-convected derivative](@entry_id:756365) measures the rate of change of a contravariant quantity as seen by an observer whose [coordinate basis](@entry_id:270149) vectors are convected and stretched affinely with the material. A remarkable consequence of this is that the [upper-convected derivative](@entry_id:756365) of the **left Cauchy-Green tensor** $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^T$, which itself describes the deformation of material line elements, is identically zero :
$$
\stackrel{\nabla}{\boldsymbol{B}} = \dot{\boldsymbol{B}} - \boldsymbol{L}\boldsymbol{B} - \boldsymbol{B}\boldsymbol{L}^T = (\boldsymbol{L}\boldsymbol{B} + \boldsymbol{B}\boldsymbol{L}^T) - (\boldsymbol{L}\boldsymbol{B} + \boldsymbol{B}\boldsymbol{L}^T) = \boldsymbol{0}
$$

#### The Lower-Convected Derivative: Frame of Surface Elements
In a parallel manner, the [lower-convected derivative](@entry_id:1127499) is the natural rate for **covariant** tensors. These are tensors associated with gradients or the deformation of material **surface elements**. The area vector of a material surface transforms covariantly.

The geometric interpretation for the [lower-convected derivative](@entry_id:1127499) mirrors that of its upper-convected counterpart. A spatial [covariant tensor](@entry_id:198677) $\boldsymbol{S}$ can be pulled back to the reference configuration as $\boldsymbol{S}_R = \boldsymbol{F}^T \boldsymbol{S} \boldsymbol{F}$. The push-forward of the [material time derivative](@entry_id:190892) of $\boldsymbol{S}_R$ is precisely the [lower-convected derivative](@entry_id:1127499) of $\boldsymbol{S}$ :
$$
\stackrel{\triangle}{\boldsymbol{S}} = \boldsymbol{F}^{-T} \left( \frac{\partial \boldsymbol{S}_R}{\partial t} \right) \boldsymbol{F}^{-1}
$$
Therefore, the [lower-convected derivative](@entry_id:1127499) measures the rate of change of a covariant quantity as seen by an observer whose basis is convected with material surface elements. An important example of a [covariant tensor](@entry_id:198677) is the **Finger tensor**, $\boldsymbol{B}^{-1}$, which is related to the deformation of surface elements. Just as $\stackrel{\nabla}{\boldsymbol{B}}=\boldsymbol{0}$, it can be shown that the [lower-convected derivative](@entry_id:1127499) of the Finger tensor is zero: $\stackrel{\triangle}{(\boldsymbol{B}^{-1})}=\boldsymbol{0}$.

In summary, the [principle of material frame-indifference](@entry_id:188488) forces us to abandon the simple material derivative in [constitutive modeling](@entry_id:183370). In its place, a family of objective derivatives emerges, each with a distinct mathematical structure and physical interpretation. The choice between the upper- and lower-convected derivatives is dictated by whether the tensor in question represents a quantity that deforms with material lines (contravariant) or with material surfaces (covariant), a distinction that is fundamental to the predictive power of any rheological model.