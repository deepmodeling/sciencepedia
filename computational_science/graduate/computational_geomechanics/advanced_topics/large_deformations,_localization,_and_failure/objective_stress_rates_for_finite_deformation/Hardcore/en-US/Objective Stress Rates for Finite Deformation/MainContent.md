## Introduction
When analyzing materials subjected to [large strains](@entry_id:751152) and rotations, as is common in geomechanics and [nonlinear solid mechanics](@entry_id:171757), a fundamental challenge arises: how do we correctly formulate [constitutive laws](@entry_id:178936) that relate the rate of stress to the rate of deformation? The intuitive approach of using the simple [material time derivative](@entry_id:190892) of the stress tensor fails spectacularly, as it violates a core physical principle known as Material Frame Indifference (MFI). This principle demands that the material's response must be independent of the observer, yet the standard stress rate is contaminated by the observer's own rotation, leading to physically absurd predictions like stress generation from pure rotation.

This article provides a comprehensive exploration of **[objective stress rates](@entry_id:199282)**, the mathematically rigorous and physically consistent solution to this problem. By constructing stress rates that are invariant to the observer's motion, we can build robust [constitutive models](@entry_id:174726) capable of accurately predicting material behavior under [finite deformation](@entry_id:172086). Across three chapters, you will gain a deep understanding of this crucial topic. The "Principles and Mechanisms" chapter will lay the theoretical groundwork, explaining why objectivity is necessary and deriving the most common [objective stress rates](@entry_id:199282). The "Applications and Interdisciplinary Connections" chapter will demonstrate the practical consequences of choosing a specific rate in fields from [computational plasticity](@entry_id:171377) to [geophysics](@entry_id:147342). Finally, "Hands-On Practices" will offer exercises to solidify your understanding of these concepts.

## Principles and Mechanisms

### The Principle of Material Frame Indifference

In the analysis of materials undergoing [large deformations](@entry_id:167243), a foundational requirement for any valid [constitutive model](@entry_id:747751) is the **Principle of Material Frame Indifference (MFI)**, also known as the [principle of objectivity](@entry_id:185412). This principle asserts that the intrinsic response of a material—such as the relationship between stress and deformation—cannot depend on the observer. More formally, the [constitutive equations](@entry_id:138559) must be invariant in form under any change of observer, where such a change is represented by a superposed time-dependent [rigid-body motion](@entry_id:265795) (a [rotation and translation](@entry_id:175994)).

Let us consider two observers. The motion of a material point as seen by the first observer is described by its [position vector](@entry_id:168381) $\mathbf{x}(t)$ in the current configuration. The second observer is in a frame of reference that moves rigidly relative to the first. The position of the same material point as seen by this second observer, $\mathbf{x}^*(t)$, is given by:

$$
\mathbf{x}^*(t) = \mathbf{Q}(t)\mathbf{x}(t) + \mathbf{c}(t)
$$

Here, $\mathbf{c}(t)$ is a time-dependent translation vector, and $\mathbf{Q}(t)$ is a time-dependent proper orthogonal tensor representing a rotation, satisfying $\mathbf{Q}^T\mathbf{Q} = \mathbf{I}$ and $\det(\mathbf{Q})=1$. The MFI principle demands that if we transform all relevant physical quantities to the new observer's frame, the constitutive law must retain its mathematical form. To understand the implications of this, we must determine how key kinematic and kinetic tensors transform under this change of frame .

The velocity of the material point in the starred frame, $\mathbf{v}^*$, is the [material time derivative](@entry_id:190892) of $\mathbf{x}^*$:
$$
\mathbf{v}^*(\mathbf{x}^*, t) = \frac{d\mathbf{x}^*}{dt} = \dot{\mathbf{Q}}\mathbf{x} + \mathbf{Q}\mathbf{v} + \dot{\mathbf{c}}
$$
where $\mathbf{v}$ is the velocity in the original frame. To find the [spatial velocity gradient](@entry_id:187198) in the starred frame, $\mathbf{L}^* = \nabla_{\mathbf{x}^*}\mathbf{v}^*$, we apply the chain rule, noting that $\mathbf{x} = \mathbf{Q}^T(\mathbf{x}^* - \mathbf{c})$. This derivation yields:
$$
\mathbf{L}^* = \mathbf{Q}\mathbf{L}\mathbf{Q}^T + \dot{\mathbf{Q}}\mathbf{Q}^T
$$
Let us define the **observer spin** tensor as $\boldsymbol{\Omega}(t) = \dot{\mathbf{Q}}(t)\mathbf{Q}^T(t)$. Differentiating the [orthogonality condition](@entry_id:168905) $\mathbf{Q}\mathbf{Q}^T=\mathbf{I}$ shows that $\dot{\mathbf{Q}}\mathbf{Q}^T + \mathbf{Q}\dot{\mathbf{Q}}^T = \mathbf{0}$, which implies that $\boldsymbol{\Omega}$ is skew-symmetric. The transformation rule for the [velocity gradient](@entry_id:261686) thus becomes:
$$
\mathbf{L}^* = \mathbf{Q}\mathbf{L}\mathbf{Q}^T + \boldsymbol{\Omega}
$$
This result is significant. It shows that the [spatial velocity gradient](@entry_id:187198) is *not* an objective tensor; its transformation law includes an additional additive term, the observer spin $\boldsymbol{\Omega}$.

In contrast, the **Cauchy stress tensor**, $\boldsymbol{\sigma}$, is an objective tensor. This can be shown by considering the Cauchy traction principle, $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$. Both the traction vector $\mathbf{t}$ and the [normal vector](@entry_id:264185) $\mathbf{n}$ must transform as objective vectors under a change of observer (i.e., $\mathbf{t}^* = \mathbf{Q}\mathbf{t}$ and $\mathbf{n}^* = \mathbf{Q}\mathbf{n}$). Applying the traction principle in both frames ($\mathbf{t}^* = \boldsymbol{\sigma}^*\mathbf{n}^*$) leads directly to the transformation rule for the Cauchy stress :
$$
\boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T
$$
This is the standard transformation rule for a second-order tensor, with no additive spin terms. A tensor that transforms in this manner is termed **objective**.

### The Need for Objective Stress Rates

The non-objectivity of the [velocity gradient](@entry_id:261686) has a profound consequence for rate-form [constitutive models](@entry_id:174726). Such models, common in geomechanics for describing plasticity and complex material history, often relate a *rate* of stress to a *rate* of deformation. A natural first choice for a stress rate might be the simple [material time derivative](@entry_id:190892) of the Cauchy stress, $\dot{\boldsymbol{\sigma}}$. However, let us examine its transformation rule. By differentiating the transformation law for $\boldsymbol{\sigma}$, we find:
$$
\dot{\boldsymbol{\sigma}}^* = \mathbf{Q}\dot{\boldsymbol{\sigma}}\mathbf{Q}^T + \boldsymbol{\Omega}\boldsymbol{\sigma}^* - \boldsymbol{\sigma}^*\boldsymbol{\Omega}
$$
Like the [velocity gradient](@entry_id:261686), the [material time derivative](@entry_id:190892) of Cauchy stress is not objective due to the presence of the spin-dependent terms. A constitutive law of the form $\dot{\boldsymbol{\sigma}} = f(\mathbf{D})$, where $\mathbf{D}$ is the (objective) [rate-of-deformation tensor](@entry_id:184787), would therefore violate the MFI principle. It would predict different material responses for different observers, which is physically untenable.

This leads to the central concept of an **[objective stress rate](@entry_id:168809)**. An [objective stress rate](@entry_id:168809), which we may denote generically as $\overset{\circ}{\boldsymbol{\sigma}}$, is a carefully constructed measure of the rate of change of stress that *is* objective. It is designed to measure the rate of change of stress in a frame that co-rotates with the material, thereby isolating the change in stress due to deformation from the change due to pure rigid rotation. The general form of such a **[corotational rate](@entry_id:193173)** is:
$$
\overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\Xi}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\Xi}
$$
where $\boldsymbol{\Xi}$ is a chosen skew-symmetric **[spin tensor](@entry_id:187346)** that characterizes the rotation of the [corotational frame](@entry_id:747893). The terms involving $\boldsymbol{\Xi}$ are designed to cancel the non-objective terms that arise in the transformation of $\dot{\boldsymbol{\sigma}}$. Different choices for the [spin tensor](@entry_id:187346) $\boldsymbol{\Xi}$ lead to different definitions of [objective stress rates](@entry_id:199282), each with its own physical interpretation and mathematical properties.

The fundamental purpose of an objective rate can be powerfully illustrated by considering a pure [rigid-body rotation](@entry_id:268623). In such a motion, the material is merely rotating without any change in shape or size, meaning there is no deformation. Consequently, the [rate-of-deformation tensor](@entry_id:184787) $\mathbf{D}$ is zero. A physically sound constitutive law of the form $\overset{\circ}{\boldsymbol{\sigma}} = \mathbb{C}:\mathbf{D}$ must predict a zero stress increment for this motion . Since $\mathbf{D}=\mathbf{0}$, the model correctly predicts $\overset{\circ}{\boldsymbol{\sigma}} = \mathbf{0}$. This demonstrates that [objective rates](@entry_id:198692) ensure no spurious stresses are generated by mere changes in orientation.

The consequences of failing to use an objective formulation can be severe. Consider a hypothetical energy calculation based on the non-objective [material time derivative](@entry_id:190892) $\dot{\boldsymbol{\sigma}}$. If one were to postulate an "energy rate" of the form $\dot{w} = \boldsymbol{\sigma}:\mathbb{A}:\dot{\boldsymbol{\sigma}}$, where $\mathbb{A}$ is a fixed tensor, it can be shown that a closed cycle of pure rigid rotation (e.g., from $\theta=0$ to $\theta=2\pi$) can lead to a net non-zero "work" being done . This implies a [spontaneous generation](@entry_id:138395) or [dissipation of energy](@entry_id:146366) simply by observing the object from a different angle, a violation of the [first law of thermodynamics](@entry_id:146485) and a clear physical absurdity. This highlights that objectivity is not just a matter of mathematical elegance but a prerequisite for physical consistency.

### Defining Key Kinematic Quantities: Deformation Rate and Spin

To construct and understand specific [objective rates](@entry_id:198692), we must first precisely define the kinematic tensors from which they are built. The primary quantity describing the motion in the current configuration is the **[spatial velocity gradient](@entry_id:187198)**, $\mathbf{L}$, defined as the gradient of the velocity field $\mathbf{v}$ with respect to the current spatial coordinates $\mathbf{x}$:
$$
\mathbf{L} = \nabla\mathbf{v}
$$
The [velocity gradient](@entry_id:261686) can be related to the [deformation gradient](@entry_id:163749) $\mathbf{F}$ through the fundamental kinematic identity $\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}$. This identity is crucial for deriving $\mathbf{L}$ from a known motion mapping $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$. For example, for a motion described by $x_1 = a(t)[X_1 + \gamma(t)X_2]$ and $x_2 = a(t)X_2$, we can first compute $\mathbf{F} = \partial\mathbf{x}/\partial\mathbf{X}$, its inverse $\mathbf{F}^{-1}$, and its time derivative $\dot{\mathbf{F}}$, and then combine them to find $\mathbf{L}$. For this specific motion, this procedure yields :
$$
\mathbf{L} = \begin{pmatrix} \frac{\dot{a}}{a}  \dot{\gamma}  0 \\ 0  \frac{\dot{a}}{a}  0 \\ 0  0  \frac{\dot{a}}{a} \end{pmatrix}
$$
The tensor $\mathbf{L}$ encapsulates all local information about the rate of deformation and rotation. It can be additively decomposed into its symmetric and skew-symmetric parts:
$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$
The symmetric part, $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T)$, is the **[rate-of-deformation tensor](@entry_id:184787)** (or stretching tensor). It describes the rate of change of shape and volume of a material element. Its diagonal components represent the rates of stretching along the coordinate axes, and its off-diagonal components represent half the rate of change of the angle between the axes (the rate of [shear deformation](@entry_id:170920)).

The skew-symmetric part, $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^T)$, is the **[spin tensor](@entry_id:187346)** (or [vorticity tensor](@entry_id:189621)). It describes the average instantaneous rate of rigid rotation of the material element.

For the example motion given above, these tensors are found to be :
$$
\mathbf{D} = \begin{pmatrix} \frac{\dot{a}}{a}  \frac{\dot{\gamma}}{2}  0 \\ \frac{\dot{\gamma}}{2}  \frac{\dot{a}}{a}  0 \\ 0  0  \frac{\dot{a}}{a} \end{pmatrix} \quad \text{and} \quad \mathbf{W} = \begin{pmatrix} 0  \frac{\dot{\gamma}}{2}  0 \\ -\frac{\dot{\gamma}}{2}  0  0 \\ 0  0  0 \end{pmatrix}
$$
Both $\mathbf{D}$ and $\mathbf{W}$ are objective tensors, making them suitable building blocks for objective constitutive laws.

### Commonly Used Objective Stress Rates

The choice of the [spin tensor](@entry_id:187346) $\boldsymbol{\Xi}$ in the general form of a [corotational rate](@entry_id:193173) is what distinguishes one objective rate from another. We will now examine the most common choices and their implications.

#### The Zaremba–Jaumann Rate

Perhaps the most intuitive choice for the [spin tensor](@entry_id:187346) is the continuum spin $\mathbf{W}$ itself. This choice leads to the **Zaremba–Jaumann rate**, or simply the **Jaumann rate**, denoted $\overset{\circ}{\boldsymbol{\sigma}}$ or $\boldsymbol{\sigma}^{\nabla J}$:
$$
\overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \mathbf{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\mathbf{W}
$$
This rate measures the rate of change of stress in a frame that rotates with the average angular velocity of the material continuum at a point. Due to its straightforward definition, it has been widely used. However, it exhibits a significant, physically unrealistic behavior in certain important deformation paths.

Consider a hypoelastic material subjected to simple shear, described by the motion $x_1 = X_1 + \gamma(t)X_2$. For a constant shear rate, the Jaumann-rate-based constitutive law $\overset{\circ}{\boldsymbol{\sigma}} = 2G\mathbf{D}$ can be solved analytically. The solution reveals that the shear stress component $\sigma_{12}$ does not increase monotonically with the [shear strain](@entry_id:175241) $\gamma$. Instead, it follows a sinusoidal path :
$$
\sigma_{12}(\gamma) = G \sin(\gamma)
$$
This result is pathological. It implies that after a certain amount of [shear strain](@entry_id:175241) ($\gamma = \pi/2$), the material's resistance to further shear would decrease, eventually becoming zero and then negative. This oscillatory response is not observed in real materials like soils or metals. This behavior arises because the continuum spin $\mathbf{W}$ in [simple shear](@entry_id:180497) represents a constant rotation rate, which, when integrated over [large strains](@entry_id:751152), leads the Jaumann rate to "over-rotate" the stress tensor relative to the underlying material fabric. The error relative to the expected small-strain response $\sigma_{12} = G\gamma$ can be quantified as $(\sin(\gamma)/\gamma) - 1$, which becomes substantial for large $\gamma$ . This makes the Jaumann rate unsuitable for analyses involving large shear deformations.

#### The Green–Naghdi Rate

An alternative spin can be derived from the [polar decomposition](@entry_id:149541) of the deformation gradient, $\mathbf{F} = \mathbf{R}\mathbf{U}$. Here, $\mathbf{U}$ is the symmetric [right stretch tensor](@entry_id:193756) that describes the pure deformation from the reference state, and $\mathbf{R}$ is the proper orthogonal [rotation tensor](@entry_id:191990) that describes the rigid rotation of the principal stretch axes. The spin associated with this material rotation is $\boldsymbol{\Omega} = \dot{\mathbf{R}}\mathbf{R}^T$. Using this as the corotational spin, $\boldsymbol{\Xi} = \boldsymbol{\Omega}$, defines the **Green–Naghdi rate** (or polar rate), denoted $\overset{\triangle}{\boldsymbol{\sigma}}$:
$$
\overset{\triangle}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{\Omega}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{\Omega}
$$
This rate measures the stress change in a frame that rotates precisely with the principal axes of the material's deformation. To understand its relationship to the Jaumann rate, we can derive the connection between their respective spins, $\mathbf{W}$ and $\boldsymbol{\Omega}$ . Starting from $\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}$ and substituting $\mathbf{F} = \mathbf{R}\mathbf{U}$, one can show that:
$$
\mathbf{W} = \boldsymbol{\Omega} + \mathrm{skw}\left(\mathbf{R}(\dot{\mathbf{U}}\mathbf{U}^{-1})\mathbf{R}^T\right)
$$
where $\mathrm{skw}(\cdot)$ denotes the skew-symmetric part. This equation reveals that the continuum spin $\mathbf{W}$ is the sum of the material rotation spin $\boldsymbol{\Omega}$ and a spin generated by the non-coaxiality of the stretch rate $\dot{\mathbf{U}}$ with the stretch $\mathbf{U}$ itself. The two rates, Jaumann and Green-Naghdi, coincide ($\mathbf{W} = \boldsymbol{\Omega}$) if and only if the second term is zero. This occurs when the principal axes of the stretch rate tensor $\dot{\mathbf{U}}$ are aligned with the principal axes of the [stretch tensor](@entry_id:193200) $\mathbf{U}$—a condition known as **coaxial stretch evolution**. Since [simple shear](@entry_id:180497) is a non-coaxial deformation, the two rates differ, which explains their different predictions for that case. The Green-Naghdi rate does not produce the unphysical oscillations of the Jaumann rate in simple shear, making it a more robust choice.

#### The Truesdell and Upper-Convected Rates

A third family of rates is motivated by establishing a direct link between spatial rate-form equations and [hyperelasticity](@entry_id:168357) defined on the reference configuration. This is crucial for energy consistency. The key insight is to work with quantities expressed per unit of *reference* volume rather than *current* volume .

The [mechanical power](@entry_id:163535) per unit current volume is $P_v = \boldsymbol{\sigma}:\mathbf{D}$. To get the power per unit reference volume, $P_V$, we multiply by the Jacobian determinant $J = \det(\mathbf{F})$, so $P_V = J(\boldsymbol{\sigma}:\mathbf{D}) = (J\boldsymbol{\sigma}):\mathbf{D}$. This motivates the definition of the **Kirchhoff stress**, $\boldsymbol{\tau} = J\boldsymbol{\sigma}$. The Kirchhoff stress $\boldsymbol{\tau}$ and the rate of deformation $\mathbf{D}$ form a **power-conjugate pair** with respect to the reference volume.

For a [hyperelastic material](@entry_id:195319) with [stored energy function](@entry_id:166355) $\Psi_0$ per unit reference volume, we must have $\dot{\Psi}_0 = P_V = \boldsymbol{\tau}:\mathbf{D}$. The stress in the reference configuration is the second Piola-Kirchhoff stress $\mathbf{S}$, which is related to $\boldsymbol{\tau}$ by the push-forward operation $\boldsymbol{\tau} = \mathbf{F}\mathbf{S}\mathbf{F}^T$. The objective rate that naturally arises from taking the [material time derivative](@entry_id:190892) of $\mathbf{S}$ and pushing it forward to the current configuration is the **upper-convected rate** (or Oldroyd rate) of the Kirchhoff stress:
$$
\overset{\nabla}{\boldsymbol{\tau}} = \dot{\boldsymbol{\tau}} - \mathbf{L}\boldsymbol{\tau} - \boldsymbol{\tau}\mathbf{L}^T
$$
A hypoelastic law of the form $\overset{\nabla}{\boldsymbol{\tau}} = \mathbb{C}:\mathbf{D}$ is therefore energetically consistent with [hyperelasticity](@entry_id:168357). The **Truesdell rate** of the Cauchy stress, $\overset{\triangledown}{\boldsymbol{\sigma}}$, is defined to maintain this consistency:
$$
\overset{\triangledown}{\boldsymbol{\sigma}} = J^{-1}\overset{\nabla}{\boldsymbol{\tau}} = J^{-1}(\dot{\boldsymbol{\tau}} - \mathbf{L}\boldsymbol{\tau} - \boldsymbol{\tau}\mathbf{L}^T)
$$
This family of rates is theoretically appealing because of its strong connection to thermodynamics and [hyperelasticity](@entry_id:168357), making it a preferred choice for developing advanced [constitutive models](@entry_id:174726), especially for compressible materials where the distinction between reference and current volumes ($J \neq 1$) is critical.

### Further Theoretical and Practical Considerations

#### Preservation of Symmetry

The [balance of angular momentum](@entry_id:181848) requires the Cauchy stress tensor $\boldsymbol{\sigma}$ to be symmetric. A valid [constitutive model](@entry_id:747751) must preserve this symmetry. If we start with a symmetric stress $\boldsymbol{\sigma}(t_0)$ and use a rate-form law $\overset{\circ}{\boldsymbol{\sigma}} = \mathbf{S}$, where the prescribed rate $\mathbf{S}$ is symmetric (as is the case for $\mathbf{S} = \mathbb{C}:\mathbf{D}$ with an [isotropic tensor](@entry_id:189108) $\mathbb{C}$), will $\boldsymbol{\sigma}(t)$ remain symmetric for all $t > t_0$?

The evolution of the skew-symmetric part of the stress, $\mathrm{skw}(\dot{\boldsymbol{\sigma}})$, can be derived from the general rate definition. If $\boldsymbol{\sigma}$ is symmetric at a given time, this evolution is governed by:
$$
\mathrm{skw}(\dot{\boldsymbol{\sigma}}) = \mathrm{skw}(\boldsymbol{\Xi}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{\Xi})
$$
This expression is non-trivial. For the stress to remain symmetric, this term must be zero, which requires that the commutator $[\boldsymbol{\Xi}, \boldsymbol{\sigma}] = \boldsymbol{\Xi}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{\Xi}$ must be a symmetric tensor. This condition is not guaranteed for an arbitrary stress state and deformation path. For instance, if $\boldsymbol{\sigma}$ has distinct [principal values](@entry_id:189577), it will only commute with spin tensors that share its principal directions, making the commutator zero and thus preserving symmetry. This reveals a subtle potential issue with some rate-form models, although for many practical applications the generated asymmetry may be small.

#### Incremental Objectivity in Numerical Implementation

When implementing a rate-based [constitutive model](@entry_id:747751) in a numerical framework like the Finite Element Method, the continuum-level objectivity must be inherited by the [discrete time](@entry_id:637509)-integration algorithm. This property is known as **[incremental objectivity](@entry_id:750600)** or algorithmic [frame-indifference](@entry_id:197245) .

Consider a numerical scheme that updates the stress from a known state at time $t_n$ to time $t_{n+1}$ based on the deformation history, $\boldsymbol{\sigma}_{n+1} = \mathcal{A}(\boldsymbol{\sigma}_n, \mathbf{F}_n, \mathbf{F}_{n+1})$. For this algorithm $\mathcal{A}$ to be incrementally objective, it must satisfy the following condition for any superposed rigid rotation $\mathbf{Q}(t)$:
$$
\mathcal{A}(\mathbf{Q}_n \boldsymbol{\sigma}_n \mathbf{Q}_n^T, \mathbf{Q}_n \mathbf{F}_n, \mathbf{Q}_{n+1} \mathbf{F}_{n+1}) = \mathbf{Q}_{n+1} \left( \mathcal{A}(\boldsymbol{\sigma}_n, \mathbf{F}_n, \mathbf{F}_{n+1}) \right) \mathbf{Q}_{n+1}^T
$$
This condition states that if the algorithm is given inputs that have been transformed to a new observer's frame, its output must be the correctly transformed stress tensor in that new frame. The transformation of the final stress $\boldsymbol{\sigma}_{n+1}$ must use the rotation at the end of the step, $\mathbf{Q}_{n+1}$.

A crucial test for any proposed numerical scheme is its behavior under a pure rigid rotation increment. If the deformation over the step is a pure rotation, $\mathbf{F}_{n+1} = \mathbf{R}_{\Delta}\mathbf{F}_n$, where $\mathbf{R}_{\Delta}$ is the incremental [rotation tensor](@entry_id:191990), then there is no actual deformation. An incrementally objective algorithm must exactly reproduce the physical result, which is the rigid rotation of the stress tensor:
$$
\boldsymbol{\sigma}_{n+1} = \mathbf{R}_{\Delta} \boldsymbol{\sigma}_n \mathbf{R}_{\Delta}^T
$$
Failure to satisfy this condition means the numerical scheme will introduce spurious, non-physical stresses when elements undergo [large rotations](@entry_id:751151), even if the underlying continuum rate is objective. Ensuring [incremental objectivity](@entry_id:750600) is therefore a critical step in the development of robust computational tools for [finite deformation](@entry_id:172086) geomechanics.