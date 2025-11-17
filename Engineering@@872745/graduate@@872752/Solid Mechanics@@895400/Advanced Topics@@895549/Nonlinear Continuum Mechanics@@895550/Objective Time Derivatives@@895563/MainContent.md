## Introduction
In the [mechanics of materials](@entry_id:201885) undergoing large deformations, a fundamental requirement is that physical laws remain independent of the observer's reference frame—a concept known as the [principle of material frame-indifference](@entry_id:188488) or objectivity. While this principle is easily satisfied for static quantities, it presents a significant challenge for time-dependent quantities. The standard [material time derivative](@entry_id:190892), used to measure rates of change, fails to be objective, as it incorrectly incorporates the spin of the observer's frame into the material's response. This article addresses this critical knowledge gap by providing a thorough exploration of objective time derivatives.

Across the following chapters, you will gain a deep understanding of this essential topic. The journey begins in the **Principles and Mechanisms** chapter, where we will formally define objectivity, demonstrate why the material derivative fails, and systematically construct the most common [objective rates](@entry_id:198692), including the Jaumann, Green-Naghdi, and Truesdell derivatives. Next, the **Applications and Interdisciplinary Connections** chapter will explore the profound practical consequences of choosing a specific rate in the fields of [solid mechanics](@entry_id:164042), rheology, and computational modeling, revealing how this choice dictates the predicted material behavior. Finally, the **Hands-On Practices** section provides targeted exercises to solidify your understanding, allowing you to directly calculate and compare different rates and witness their impact within a [constitutive model](@entry_id:747751).

## Principles and Mechanisms

In the study of [continuum mechanics](@entry_id:155125), particularly for materials undergoing [large deformations](@entry_id:167243), it is essential that our physical laws and [constitutive models](@entry_id:174726) are independent of the observer. This fundamental requirement, known as the **[principle of material frame-indifference](@entry_id:188488)** or the **[principle of objectivity](@entry_id:185412)**, dictates that the internal response of a material cannot depend on the arbitrary [rigid body motion](@entry_id:144691) of the observer's reference frame. While this principle is straightforward to apply to static quantities, it introduces profound complexities when dealing with time rates of change. This chapter elucidates the principles governing objective time derivatives and details the mechanisms by which they are constructed.

### The Principle of Material Frame-Indifference

The concept of objectivity is formalized by considering two observers who describe the same physical motion. Their coordinate systems are related by a time-dependent [rigid body motion](@entry_id:144691), often called a **superposed [rigid body motion](@entry_id:144691)**. Mathematically, if an observer in a frame uses coordinates $\boldsymbol{x}$ to describe a material point at time $t$, a second observer in a "starred" frame describes the same point with coordinates $\boldsymbol{x}^{\ast}$ given by:

$\boldsymbol{x}^{\ast}(t) = \boldsymbol{c}(t) + \boldsymbol{Q}(t)\boldsymbol{x}(t)$

Here, $\boldsymbol{c}(t)$ is a time-dependent translation vector representing the shift of the origin, and $\boldsymbol{Q}(t)$ is a time-dependent proper orthogonal tensor, $\boldsymbol{Q}(t) \in \mathrm{SO}(3)$, meaning it satisfies $\boldsymbol{Q}^T\boldsymbol{Q} = \boldsymbol{I}$ and $\det(\boldsymbol{Q})=1$. The condition $\det(\boldsymbol{Q})=1$ ensures that the transformation preserves orientation (i.e., it is a pure rotation, not a reflection).

The [principle of objectivity](@entry_id:185412) requires that physical quantities measured by the two observers transform in a consistent manner. A scalar quantity $\phi$, such as temperature, must be invariant: $\phi^{\ast} = \phi$. A vector quantity $\boldsymbol{u}$ representing a physical direction must rotate with the frame: $\boldsymbol{u}^{\ast} = \boldsymbol{Q}\boldsymbol{u}$. For a second-order [spatial tensor](@entry_id:185799) field $\boldsymbol{T}$, such as the Cauchy stress tensor, the transformation rule is derived by requiring that scalar products representing physical work rates remain invariant. This leads to the transformation law [@problem_id:2666493]:

$\boldsymbol{T}^{\ast}(\boldsymbol{x}^{\ast}, t) = \boldsymbol{Q}(t) \boldsymbol{T}(\boldsymbol{x}, t) \boldsymbol{Q}(t)^T$

It is crucial to distinguish [material frame-indifference](@entry_id:178419) from **Galilean invariance**. Galilean invariance is a more restrictive principle that applies to the fundamental balance laws of mechanics (e.g., conservation of linear and angular momentum), requiring them to hold their form only under transformations between **[inertial frames](@entry_id:200622)**. These transformations involve [constant velocity](@entry_id:170682) translations, $\boldsymbol{x}' = \boldsymbol{x} + \boldsymbol{u}_0 t$. In contrast, [material frame-indifference](@entry_id:178419) is a requirement placed on **[constitutive equations](@entry_id:138559)**—the equations that describe material behavior—and it must hold for a much larger class of observer changes, including arbitrarily time-dependent rotations and accelerations [@problem_id:2666514].

### The Non-Objectivity of the Material Time Derivative

A central challenge in formulating rate-type constitutive laws arises because the standard [material time derivative](@entry_id:190892) is not an objective operation. The [material derivative](@entry_id:266939), denoted by a superposed dot (e.g., $\dot{\boldsymbol{T}}$), represents the rate of change of a quantity following a specific material particle. While a [tensor field](@entry_id:266532) $\boldsymbol{T}$ may be objective, its material derivative $\dot{\boldsymbol{T}}$ is generally not.

To demonstrate this, we can differentiate the transformation rule for $\boldsymbol{T}$ with respect to time:

$\dot{\boldsymbol{T}}^{\ast} = \frac{d}{dt} \left( \boldsymbol{Q} \boldsymbol{T} \boldsymbol{Q}^T \right) = \dot{\boldsymbol{Q}}\boldsymbol{T}\boldsymbol{Q}^T + \boldsymbol{Q}\dot{\boldsymbol{T}}\boldsymbol{Q}^T + \boldsymbol{Q}\boldsymbol{T}\dot{\boldsymbol{Q}}^T$

Let us define the [skew-symmetric tensor](@entry_id:199349) $\boldsymbol{\Omega}(t) = \dot{\boldsymbol{Q}}(t)\boldsymbol{Q}(t)^T$, which represents the angular velocity of the starred frame relative to the unstarred frame. Using this and the relation $\boldsymbol{Q}\dot{\boldsymbol{Q}}^T = -\boldsymbol{\Omega}$, we can rewrite the expression as [@problem_id:2666493]:

$\dot{\boldsymbol{T}}^{\ast} = \boldsymbol{Q}\dot{\boldsymbol{T}}\boldsymbol{Q}^T + \boldsymbol{\Omega}\boldsymbol{T}^{\ast} - \boldsymbol{T}^{\ast}\boldsymbol{\Omega}$

If the [material derivative](@entry_id:266939) were objective, the transformation would simply be $\dot{\boldsymbol{T}}^{\ast} = \boldsymbol{Q}\dot{\boldsymbol{T}}\boldsymbol{Q}^T$. The presence of the additional terms $\boldsymbol{\Omega}\boldsymbol{T}^{\ast} - \boldsymbol{T}^{\ast}\boldsymbol{\Omega}$ demonstrates its non-objectivity. These terms are spurious contributions arising purely from the relative spin of the observer's frame.

A concrete example illustrates this failure vividly [@problem_id:658176]. Consider a [simple shear](@entry_id:180497) flow given by the velocity field $\boldsymbol{v} = (ky, 0, 0)$ in a fixed frame. The [rate-of-strain tensor](@entry_id:260652) $\boldsymbol{D} = \frac{1}{2}(\nabla\boldsymbol{v} + (\nabla\boldsymbol{v})^T)$ is constant in this frame. Consequently, its material derivative $\frac{D\boldsymbol{D}}{Dt}$ is zero. However, if this same steady flow is observed from a frame rotating with a constant angular velocity $\omega$ about the $z$-axis, a direct calculation reveals that the material derivative of the transformed tensor, $\frac{D\boldsymbol{D}'}{Dt}$, is non-zero. The non-zero result does not reflect any change in the physical deformation process but is instead an artifact of the observer's rotation. This clearly shows that the [material time derivative](@entry_id:190892) is an unsuitable measure for rate-type [constitutive laws](@entry_id:178936) that must be frame-indifferent.

### The Construction of Objective Time Rates

To remedy this, we must construct **objective time rates**, which are operators that, when applied to an objective tensor, yield another objective tensor. Let $\mathcal{D}[\boldsymbol{T}]$ denote an objective time rate of $\boldsymbol{T}$. By definition, it must satisfy the transformation rule [@problem_id:2666493]:

$\mathcal{D}[\boldsymbol{T}]^{\ast} = \boldsymbol{Q}(t) \mathcal{D}[\boldsymbol{T}] \boldsymbol{Q}(t)^T$

The general strategy is to modify the [material time derivative](@entry_id:190892) $\dot{\boldsymbol{T}}$ by adding correction terms that precisely cancel the non-objective terms arising from the observer's spin. This has led to the development of several different, but equally valid, [objective rates](@entry_id:198692), each with its own physical interpretation and mathematical properties. These rates fall into two main families: corotational and convected rates.

### Corotational Rates

Corotational rates are designed based on the idea of measuring the rate of change of a tensor in a frame that rotates along with the material in some defined sense. The general form of a [corotational rate](@entry_id:193173) is given by [@problem_id:2666477]:

$\overset{\circ}{\boldsymbol{T}} = \dot{\boldsymbol{T}} + \boldsymbol{T}\boldsymbol{\omega} - \boldsymbol{\omega}\boldsymbol{T}$

where $\boldsymbol{\omega}$ is a [skew-symmetric tensor](@entry_id:199349) representing the spin of the chosen corotating frame. The term $\boldsymbol{\omega}\boldsymbol{T} - \boldsymbol{T}\boldsymbol{\omega}$ is the Lie bracket or commutator, often denoted $[\boldsymbol{\omega}, \boldsymbol{T}]$. This rate is objective if and only if the [spin tensor](@entry_id:187346) $\boldsymbol{\omega}$ transforms according to:

$\boldsymbol{\omega}^{\ast} = \boldsymbol{Q}\boldsymbol{\omega}\boldsymbol{Q}^T + \dot{\boldsymbol{Q}}\boldsymbol{Q}^T$

This transformation rule ensures that the spin $\boldsymbol{\omega}$ correctly accounts for both the intrinsic material spin and the superposed spin of the observer. Different choices of objective spin $\boldsymbol{\omega}$ lead to different [objective rates](@entry_id:198692).

#### The Jaumann Rate

The most common [corotational rate](@entry_id:193173) is the **Jaumann rate**, obtained by selecting the [spin tensor](@entry_id:187346) $\boldsymbol{\omega}$ to be the material [spin tensor](@entry_id:187346) $\boldsymbol{W}$, which is the skew-symmetric part of the velocity gradient $\boldsymbol{L} = \nabla\boldsymbol{v}$:

$\boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^T)$

The Jaumann rate of a tensor $\boldsymbol{T}$ is thus:

$\overset{\circ}{\boldsymbol{T}} = \dot{\boldsymbol{T}} + \boldsymbol{T}\boldsymbol{W} - \boldsymbol{W}\boldsymbol{T}$

One can verify that the material spin $\boldsymbol{W}$ satisfies the required transformation law, making the Jaumann rate objective [@problem_id:2666477], [@problem_id:2666504].

#### The Green-Naghdi Rate

Another important [corotational rate](@entry_id:193173) is the **Green–Naghdi rate**. It is defined by choosing a spin that is tied to the rotation of the material itself, as captured by the [polar decomposition](@entry_id:149541) of the deformation gradient, $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$. Here, $\boldsymbol{R}$ is the [rotation tensor](@entry_id:191990) and $\boldsymbol{U}$ is the [right stretch tensor](@entry_id:193756). The Green-Naghdi spin is defined as $\boldsymbol{\Omega}_{GN} = \dot{\boldsymbol{R}}\boldsymbol{R}^T$. The corresponding objective rate is [@problem_id:2666476]:

$\overset{\circ}{\boldsymbol{\sigma}}_{GN} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\boldsymbol{\Omega}_{GN} - \boldsymbol{\Omega}_{GN}\boldsymbol{\sigma}$

The Green-Naghdi rate can also be interpreted as the [material derivative](@entry_id:266939) of the stress tensor viewed in a frame that corotates with $\boldsymbol{R}$, subsequently pushed forward to the spatial frame. This is expressed elegantly as [@problem_id:2666476]:

$\overset{\circ}{\boldsymbol{\sigma}}_{GN} = \boldsymbol{R} \left( \frac{d}{dt} \left( \boldsymbol{R}^T \boldsymbol{\sigma} \boldsymbol{R} \right) \right) \boldsymbol{R}^T$

The spins $\boldsymbol{W}$ and $\boldsymbol{\Omega}_{GN}$ are not generally identical. Their equality holds only under the specific kinematic condition that the [right stretch tensor](@entry_id:193756) $\boldsymbol{U}$ and its rate of change $\dot{\boldsymbol{U}}$ commute, i.e., $[\dot{\boldsymbol{U}}, \boldsymbol{U}] = \boldsymbol{0}$. This corresponds to physical situations where the principal directions of stretch do not rotate relative to the material, such as in isotropic expansion [@problem_id:2666494]. In general motions like simple shear, these two spins differ, and consequently, the Jaumann and Green-Naghdi rates yield different results.

### Convected Rates

A different class of [objective rates](@entry_id:198692), known as convected rates, arises naturally from considering how [tensor fields](@entry_id:190170) are transported by the material flow.

#### The Oldroyd Rates

The **upper convected Oldroyd rate** (or simply upper convected rate) of a tensor $\boldsymbol{A}$ is defined as:

$\overset{\triangledown}{\boldsymbol{A}} = \dot{\boldsymbol{A}} - \boldsymbol{L}\boldsymbol{A} - \boldsymbol{A}\boldsymbol{L}^T$

Its counterpart is the **lower convected Oldroyd rate**:

$\check{\boldsymbol{A}} = \dot{\boldsymbol{A}} + \boldsymbol{L}^T\boldsymbol{A} + \boldsymbol{A}\boldsymbol{L}$

Both of these rates can be proven to be objective [@problem_id:2666504]. The upper convected rate has a particularly important property: the upper convected rate of the left Cauchy-Green tensor $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^T$ is identically zero, $\overset{\triangledown}{\boldsymbol{B}} = \boldsymbol{0}$. This reflects the fact that the tensor $\boldsymbol{B}$ is intrinsically "convected" with the material flow.

#### The Truesdell Rate

The upper convected rate is fundamental to defining another widely used rate: the **Truesdell rate** of the Cauchy stress $\boldsymbol{\sigma}$. The derivation begins with the **Kirchhoff stress** tensor, $\boldsymbol{\tau} = J\boldsymbol{\sigma}$, where $J = \det(\boldsymbol{F})$ is the determinant of the deformation gradient, representing the ratio of current volume to reference volume. If we postulate that the "natural" objective rate for the Kirchhoff stress is its upper convected derivative, $\overset{\triangledown}{\boldsymbol{\tau}}$, we can define the Truesdell rate of Cauchy stress, $\overset{\triangle}{\boldsymbol{\sigma}}$, via the consistency relation $\overset{\triangledown}{\boldsymbol{\tau}} = J\overset{\triangle}{\boldsymbol{\sigma}}$.

By expanding this definition and using the kinematic identity for the rate of change of volume, $\dot{J} = J\,\mathrm{tr}(\boldsymbol{L})$, we arrive at the expression for the Truesdell rate [@problem_id:2666484]:

$\overset{\triangle}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{L}^T + (\mathrm{tr}\,\boldsymbol{L})\boldsymbol{\sigma}$

The final term, $(\mathrm{tr}\,\boldsymbol{L})\boldsymbol{\sigma}$, which distinguishes the Truesdell rate from the upper convected rate of Cauchy stress, arises directly from accounting for the rate of change of volume in the relationship between Kirchhoff and Cauchy stress.

### Advanced Perspectives and Practical Implications

The array of different [objective rates](@entry_id:198692) can be unified and better understood through the lens of [differential geometry](@entry_id:145818). The **Lie derivative** of a [tensor field](@entry_id:266532) $\boldsymbol{T}$ along the [velocity field](@entry_id:271461) $\boldsymbol{v}$, denoted $\mathcal{L}_{\boldsymbol{v}}\boldsymbol{T}$, provides a coordinate-free definition of the intrinsic rate of change of the tensor as it is dragged along by the material flow. The Lie derivative is inherently objective [@problem_id:2666508]. The Truesdell rate, for instance, can be defined compactly and elegantly as the Lie derivative of the Kirchhoff stress density, scaled by $J^{-1}$: $\overset{\triangle}{\boldsymbol{\sigma}} = J^{-1} \mathcal{L}_{\boldsymbol{v}}\boldsymbol{\tau}$.

The choice of objective rate is not a mere mathematical subtlety; it has profound consequences in [constitutive modeling](@entry_id:183370). When formulating **hypoelastic** models, where an [objective stress rate](@entry_id:168809) is related to the rate of deformation $\boldsymbol{D}$ (e.g., $\overset{\circ}{\boldsymbol{\tau}} = \mathcal{C}:\boldsymbol{D}$), the choice of rate matters.

In the regime of **small elastic strains but arbitrarily [large rotations](@entry_id:751151)**, which is common in many engineering applications, most [corotational rates](@entry_id:183217) (like the Jaumann and Green-Naghdi) yield predictions for stress that agree to the first order. The differences between them appear only at the second order in strain [@problem_id:2666516]. However, beyond this regime, the differences become significant.

A crucial issue is **[integrability](@entry_id:142415)**. A [hypoelastic model](@entry_id:750490) is said to be integrable if it can be derived from a stored energy potential, in which case it is equivalent to a **hyperelastic** model. This ensures that the material is path-independent and does not spuriously generate or dissipate energy in a closed deformation cycle. It is a classic result that simple hypoelastic laws based on the Jaumann or Green-Naghdi rates are generally *not* integrable. In contrast, rates like the logarithmic rate are constructed specifically to be integrable with simple [isotropic elasticity](@entry_id:203237) laws, providing a direct link to [hyperelasticity](@entry_id:168357) [@problem_id:2666516]. All [objective rates](@entry_id:198692) correctly predict that a pre-existing stress in a body will simply rotate with the body during a pure [rigid body motion](@entry_id:144691) ($\boldsymbol{D}=\boldsymbol{0}$), without generating spurious stresses.

In summary, the non-objectivity of the standard [material time derivative](@entry_id:190892) necessitates the construction of objective time rates for use in [finite deformation](@entry_id:172086) mechanics. While many such rates exist, each mathematically valid, their physical interpretations differ, and their use in [constitutive models](@entry_id:174726) leads to distinct predictions, particularly at finite strains. The choice of an objective rate is therefore a fundamental part of the physical modeling of material behavior.