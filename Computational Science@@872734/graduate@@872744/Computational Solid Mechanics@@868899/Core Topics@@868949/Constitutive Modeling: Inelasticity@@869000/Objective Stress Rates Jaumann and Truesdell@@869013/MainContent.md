## Introduction
Accurately modeling materials undergoing large deformations is a paramount challenge across many scientific and engineering disciplines. Constitutive laws, which describe a material's stress response, must be formulated in a way that is independent of the observer's motion—a principle known as [material frame-indifference](@entry_id:178419) or objectivity. A critical problem arises when we try to express the rate of change of stress over time; the standard [material time derivative](@entry_id:190892) of the Cauchy stress tensor fails this test of objectivity, making it unsuitable for use in fundamental material laws. This article addresses this knowledge gap by providing a comprehensive exploration of [objective stress rates](@entry_id:199282), which are mathematical constructs designed to measure the true, intrinsic rate of stress change. In the following chapters, you will first delve into the **Principles and Mechanisms** behind objectivity, exploring the kinematic foundations and the distinct corotational (Jaumann) and convected (Truesdell) formulations. Next, you will examine the far-reaching **Applications and Interdisciplinary Connections**, understanding how the choice of stress rate impacts [numerical stability](@entry_id:146550), [thermodynamic consistency](@entry_id:138886), and model predictions in fields from geomechanics to [rheology](@entry_id:138671). Finally, the **Hands-On Practices** section will allow you to solidify your understanding by deriving key results and analyzing the practical behavior of these rates. We begin by establishing the core principles that necessitate the use of [objective stress rates](@entry_id:199282).

## Principles and Mechanisms

In the study of materials undergoing [large deformations](@entry_id:167243), [constitutive laws](@entry_id:178936) must relate the state of stress to the history of deformation. When formulating these laws in the current, deformed configuration (an Eulerian description), we immediately face a fundamental challenge: how to properly express the rate of change of stress. This chapter elucidates the principles governing the time derivatives of tensors in a deforming medium and introduces the mechanisms by which physically meaningful, or **objective**, stress rates are constructed.

### The Problem of Objectivity and the Material Time Derivative

In [continuum mechanics](@entry_id:155125), the rate of change of a physical quantity associated with a specific material particle is given by the **[material time derivative](@entry_id:190892)**. For a general [spatial tensor](@entry_id:185799) field $\boldsymbol{A}(\boldsymbol{x}, t)$, which depends on the spatial position $\boldsymbol{x}$ and time $t$, its [material time derivative](@entry_id:190892), denoted $\dot{\boldsymbol{A}}$, is the rate of change following the particle's motion. Applying the chain rule yields:

$$
\dot{\boldsymbol{A}} = \frac{\partial \boldsymbol{A}}{\partial t} + (\nabla \boldsymbol{A}) \cdot \boldsymbol{v}
$$

Here, $\frac{\partial \boldsymbol{A}}{\partial t}$ is the local rate of change at a fixed point in space, $\boldsymbol{v}$ is the velocity of the material particle currently at $\boldsymbol{x}$, and $\nabla \boldsymbol{A}$ is the spatial gradient of $\boldsymbol{A}$. This formula applies to scalars, vectors, and tensors of any order.

A fundamental requirement for any valid constitutive law is the **[principle of material frame-indifference](@entry_id:188488)**, also known as the [principle of objectivity](@entry_id:185412). This principle states that the response of a material is independent of the observer. A change of observer is mathematically described by a superposed [rigid-body motion](@entry_id:265795), where the position of a point in a new frame, $\boldsymbol{x}^*$, is related to its position in the old frame, $\boldsymbol{x}$, by:

$$
\boldsymbol{x}^*(t) = \boldsymbol{c}(t) + \boldsymbol{Q}(t)\boldsymbol{x}(t)
$$

where $\boldsymbol{c}(t)$ is a time-dependent translation and $\boldsymbol{Q}(t)$ is a time-dependent proper orthogonal [rotation tensor](@entry_id:191990) (i.e., $\boldsymbol{Q}^T\boldsymbol{Q}=\boldsymbol{I}$ and $\det(\boldsymbol{Q})=1$). A second-order tensor, such as the **Cauchy stress tensor** $\boldsymbol{\sigma}$, is said to be **objective** if its components transform between frames according to the standard [tensor transformation rule](@entry_id:185176):

$$
\boldsymbol{\sigma}^* = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T
$$

The central problem arises when we consider the rate of change of stress. Is the [material time derivative](@entry_id:190892) of the Cauchy stress, $\dot{\boldsymbol{\sigma}}$, an objective tensor? To answer this, we differentiate the transformation rule for $\boldsymbol{\sigma}$ with respect to time:

$$
\dot{\boldsymbol{\sigma}}^* = \frac{d}{dt}(\boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T) = \dot{\boldsymbol{Q}}\boldsymbol{\sigma}\boldsymbol{Q}^T + \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^T + \boldsymbol{Q}\boldsymbol{\sigma}\dot{\boldsymbol{Q}}^T
$$

For $\dot{\boldsymbol{\sigma}}$ to be objective, its transformation rule would have to be $\dot{\boldsymbol{\sigma}}^* = \boldsymbol{Q}\dot{\boldsymbol{\sigma}}\boldsymbol{Q}^T$. A comparison reveals that the calculated transformation of $\dot{\boldsymbol{\sigma}}^*$ contains two extra terms, $\dot{\boldsymbol{Q}}\boldsymbol{\sigma}\boldsymbol{Q}^T$ and $\boldsymbol{Q}\boldsymbol{\sigma}\dot{\boldsymbol{Q}}^T$. These terms are non-zero whenever the observer's frame is rotating ($\dot{\boldsymbol{Q}} \neq \boldsymbol{0}$). Therefore, the [material time derivative](@entry_id:190892) of the Cauchy stress, $\dot{\boldsymbol{\sigma}}$, is not objective. This means that $\dot{\boldsymbol{\sigma}}$ depends on the observer's motion and cannot be directly used in a constitutive law intended to represent intrinsic material behavior.

This necessitates the construction of new quantities, known as **[objective stress rates](@entry_id:199282)**, which measure the intrinsic rate of change of stress, purged of the effects of the observer's rotation. An [objective stress rate](@entry_id:168809), which we may denote generically by $\stackrel{\circ}{\boldsymbol{\sigma}}$, must by definition be a tensor that satisfies the objectivity requirement:

$$
\stackrel{\circ}{\boldsymbol{\sigma}}^* = \boldsymbol{Q}\stackrel{\circ}{\boldsymbol{\sigma}}\boldsymbol{Q}^T
$$

### Kinematic Foundations: Spin and Deformation Rate

To construct [objective rates](@entry_id:198692), we must first analyze the local [kinematics](@entry_id:173318) of the deformation. The motion of a material neighborhood is fully characterized by the **[spatial velocity gradient](@entry_id:187198)**, $\boldsymbol{L} = \nabla\boldsymbol{v}$. This tensor can be additively decomposed into its symmetric and skew-symmetric parts:

$$
\boldsymbol{L} = \boldsymbol{D} + \boldsymbol{W}
$$

The symmetric part, $\boldsymbol{D} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^T)$, is the **[rate-of-deformation tensor](@entry_id:184787)** (or stretching tensor). It describes how material line elements stretch and how the angles between them change, representing the rate of pure deformation. The skew-symmetric part, $\boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^T)$, is the **[spin tensor](@entry_id:187346)**. It describes the [instantaneous angular velocity](@entry_id:171936) of the material at a point.

The significance of this decomposition is vividly illustrated in a pure [rigid-body rotation](@entry_id:268623). For such a motion, described by a velocity field $\boldsymbol{v}(t) = \dot{\boldsymbol{Q}}(t)\boldsymbol{Q}(t)^T\boldsymbol{x}$, there is no change in shape or size of material elements. A direct calculation shows that the [velocity gradient](@entry_id:261686) is $\boldsymbol{L} = \dot{\boldsymbol{Q}}\boldsymbol{Q}^T$, which is a [skew-symmetric tensor](@entry_id:199349). Consequently, its symmetric part, the rate of deformation, is zero: $\boldsymbol{D} = \boldsymbol{0}$. The [spin tensor](@entry_id:187346) becomes equal to the entire velocity gradient: $\boldsymbol{W} = \boldsymbol{L}$. This confirms that the [spin tensor](@entry_id:187346) $\boldsymbol{W}$ correctly isolates the rotational part of the motion.

### Corotational and Convected Derivatives: Two Geometrical Viewpoints

Objective stress rates are constructed by augmenting the material derivative $\dot{\boldsymbol{\sigma}}$ with terms involving kinematic tensors ($\boldsymbol{L}$, $\boldsymbol{D}$, $\boldsymbol{W}$) and the stress $\boldsymbol{\sigma}$ itself, designed to cancel the non-objective parts. The specific form of these correction terms depends on the underlying geometric interpretation of how the stress tensor is transported along with the deforming material. This leads to two primary families of [objective rates](@entry_id:198692).

1.  **Corotational Derivatives**: This approach seeks to measure the rate of change of stress as viewed by an observer situated in a reference frame that rotates with the material. The [angular velocity](@entry_id:192539) of this frame is identified with the material spin $\boldsymbol{W}$. The time derivative of a tensor in a frame rotating with spin $\boldsymbol{W}$ introduces a Lie bracket (or commutator) term. This philosophy gives rise to rates where $\dot{\boldsymbol{\sigma}}$ is corrected by terms involving $\boldsymbol{W}$.

2.  **Convected Derivatives**: This approach is rooted in the idea of mapping tensor quantities between the reference (material) configuration and the current (spatial) configuration. A rate is defined in the objective material frame and then "pushed forward" to the spatial frame. The time derivative of this push-forward operation, which involves the [deformation gradient](@entry_id:163749) $\boldsymbol{F}$, naturally introduces the velocity gradient $\boldsymbol{L} = \dot{\boldsymbol{F}}\boldsymbol{F}^{-1}$. This philosophy leads to rates where $\dot{\boldsymbol{\sigma}}$ is corrected by terms involving $\boldsymbol{L}$.

A crucial property shared by all valid [objective rates](@entry_id:198692) is that they must evaluate to zero for a stress state that is merely undergoing a rigid rotation without any change in its intensity or orientation relative to the material itself. In such a scenario, where $\boldsymbol{D}=\boldsymbol{0}$ and the stress evolves as $\boldsymbol{\sigma}(t) = \boldsymbol{Q}(t)\boldsymbol{\sigma}_0\boldsymbol{Q}(t)^T$, any well-constructed objective rate $\stackrel{\circ}{\boldsymbol{\sigma}}$ must be zero, correctly identifying the absence of any true change in the material's stress state.

### The Jaumann Rate: A Corotational Formulation

The most common [corotational rate](@entry_id:193173) is the **Jaumann rate** (also known as the Zaremba-Jaumann rate), defined as:

$$
\overset{\nabla}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}
$$

The term $\boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}$ is precisely the correction required to remove the apparent change in $\boldsymbol{\sigma}$ due to the material's spin. If a hypoelastic law states that the Jaumann rate is zero in the absence of deformation (i.e., $\overset{\nabla}{\boldsymbol{\sigma}} = \boldsymbol{0}$ when $\boldsymbol{D} = \boldsymbol{0}$), this implies the differential equation $\dot{\boldsymbol{\sigma}} = \boldsymbol{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{W}$. The solution to this equation for a constant spin $\boldsymbol{W}$ is $\boldsymbol{\sigma}(t) = \boldsymbol{R}(t)\boldsymbol{\sigma}_0\boldsymbol{R}(t)^T$, where $\boldsymbol{R}(t) = \exp(t\boldsymbol{W})$ is the [rotation tensor](@entry_id:191990). This confirms that the Jaumann rate correctly interprets a pure rotation of the stress tensor as a state of zero [intrinsic stress](@entry_id:193721) change.

Despite its intuitive appeal, the Jaumann rate exhibits a significant, physically unrealistic artifact in certain deformations. When used in a simple linear hypoelastic law, $\overset{\nabla}{\boldsymbol{\sigma}} = 2\mu\boldsymbol{D} + \kappa \operatorname{tr}(\boldsymbol{D})\boldsymbol{I}$, for a sustained simple shear flow, it predicts that the stress components will oscillate spuriously as the [shear strain](@entry_id:175241) increases. For a constant shear rate $\dot{\gamma}$, the shear stress $\sigma_{12}$ and the [normal stresses](@entry_id:260622) $\sigma_{11}, \sigma_{22}$ do not grow monotonically but instead oscillate sinusoidally with the total [shear strain](@entry_id:175241) $\gamma = \dot{\gamma}t$. This pathological behavior arises because the material spin $\boldsymbol{W}$ in simple shear is constant, while the material line elements undergo unbounded rotation. The Jaumann rate, fixed to the spin $\boldsymbol{W}$, effectively over-rotates the stress relative to the material fibers, leading to the oscillations.

### The Truesdell Rate: A Convected Formulation

An important example of a convected derivative is the **Truesdell rate** of the Cauchy stress, which is defined as:

$$
\stackrel{\triangle}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{L}^T + \operatorname{tr}(\boldsymbol{L})\boldsymbol{\sigma}
$$

Note that $\operatorname{tr}(\boldsymbol{L}) = \operatorname{tr}(\boldsymbol{D})$. This rate can be derived by considering the [material time derivative](@entry_id:190892) of the objective second Piola-Kirchhoff stress tensor and pushing the result forward to the current configuration. It is also directly related to the Oldroyd [upper-convected derivative](@entry_id:756365) of the Kirchhoff stress $\boldsymbol{\tau} = J\boldsymbol{\sigma}$, where $J = \det(\boldsymbol{F})$.

By substituting $\boldsymbol{L} = \boldsymbol{D} + \boldsymbol{W}$, we can find the relationship between the Truesdell and Jaumann rates:

$$
\stackrel{\triangle}{\boldsymbol{\sigma}} = \overset{\nabla}{\boldsymbol{\sigma}} - (\boldsymbol{D}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{D}) + \operatorname{tr}(\boldsymbol{D})\boldsymbol{\sigma}
$$

This shows that the two rates differ by terms that depend on the rate-of-deformation $\boldsymbol{D}$. When the motion is a pure rigid rotation ($\boldsymbol{D} = \boldsymbol{0}$), the difference vanishes and the Truesdell and Jaumann rates coincide, as they must.

### Hypoelasticity, Hyperelasticity, and Energy Consistency

Objective stress rates are the building blocks for **hypoelastic** [constitutive models](@entry_id:174726), which are rate-type laws of the general form $\stackrel{\circ}{\boldsymbol{\sigma}} = \mathcal{F}(\boldsymbol{\sigma}, \boldsymbol{D})$. While a law like $\stackrel{\circ}{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{D}$ (with a constant [isotropic elasticity](@entry_id:203237) tensor $\mathbb{C}$) satisfies the [principle of material frame-indifference](@entry_id:188488), it suffers from a major thermodynamic deficiency.

For a material to be purely elastic, the work done over any closed deformation cycle must be zero. This requires the existence of a stored elastic energy potential $\psi$, a state function from which the stress can be derived. Such materials are termed **hyperelastic**. Hypoelastic laws, in general, are not integrable; the stress at a given deformation depends on the path taken to reach it. This path-dependence means they can predict non-zero work in closed cycles, which corresponds to spurious energy generation or dissipation.

Therefore, objectivity does not imply energy consistency. The choice of an objective rate does not, by itself, guarantee a thermodynamically sound elastic model. However, rate-type formulations are essential for true [hyperelastic materials](@entry_id:190241) as well. It can be shown that if a hyperelastic potential exists, its corresponding rate form is naturally expressed using the Truesdell rate (or the equivalent Oldroyd rate of Kirchhoff stress). In this case, the tangent modulus $\mathbb{C}$ is not constant but is itself a function of the current deformation state. In [computational mechanics](@entry_id:174464), integrating this consistent rate form allows one to numerically recover the path-independent response of the underlying [hyperelastic material](@entry_id:195319).

In summary, [objective stress rates](@entry_id:199282) are a mathematical necessity for formulating [constitutive laws](@entry_id:178936) in a spatially-fixed frame. While different rates like the Jaumann and Truesdell rates are kinematically valid, they arise from different geometric viewpoints and lead to models with profoundly different behaviors, particularly under large shear and in the context of [thermodynamic consistency](@entry_id:138886).