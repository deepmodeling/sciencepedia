## Introduction
In the study of mechanics, the concept of a [rigid body motion](@entry_id:144691) represents the simplest form of movement, describing a change in position and orientation without any change in size or shape. However, its importance extends far beyond the analysis of non-deforming bodies. For a deformable continuum, [rigid body motion](@entry_id:144691) serves as the fundamental baseline against which all true deformation—stretching, shearing, and twisting—is measured. The primary challenge in advanced [computational mechanics](@entry_id:174464) is to robustly and accurately distinguish genuine, stress-inducing deformation from large, stress-free [rigid motions](@entry_id:170523). Failure to do so results in physically incorrect simulations and [numerical instability](@entry_id:137058).

This article provides a comprehensive exploration of the theory and application of rigid body motions, essential for any graduate student or researcher in [computational solid mechanics](@entry_id:169583). It bridges the gap between abstract kinematic theory and its critical implementation in modern engineering software. Across three chapters, you will gain a deep understanding of this foundational topic. The first chapter, "Principles and Mechanisms," will establish the rigorous mathematical framework, defining [rigid motion](@entry_id:155339) through the deformation gradient, exploring its algebraic group structure, and analyzing the resulting velocity and acceleration fields. The second chapter, "Applications and Interdisciplinary Connections," will demonstrate how these principles are applied to ensure physical realism in [finite element analysis](@entry_id:138109), from enforcing objectivity in [constitutive models](@entry_id:174726) to designing [stable numerical schemes](@entry_id:755322) and connecting with fields like computer graphics and data science. Finally, the "Hands-On Practices" section will provide concrete computational problems to solidify your understanding of key concepts like objectivity, numerical integration, and [strain measures](@entry_id:755495) in the presence of [large rotations](@entry_id:751151).

## Principles and Mechanisms

In the study of [continuum mechanics](@entry_id:155125), the concept of a [rigid body motion](@entry_id:144691) serves as a fundamental reference against which all deformation is measured. It represents a transformation that alters the position and orientation of a body in space without changing its size or shape. Understanding the principles and mechanisms of rigid body motions is not only crucial for describing the kinematics of non-deforming bodies but is also essential for formulating physically meaningful constitutive laws for deformable materials. This chapter elucidates the mathematical definition of rigid motion, explores its algebraic structure, analyzes the resulting velocity and acceleration fields, and discusses its profound implications for the theory of [constitutive modeling](@entry_id:183370).

### The Kinematic Definition of a Rigid Body Motion

A motion is mathematically described by a mapping $\boldsymbol{x} = \boldsymbol{\chi}(\boldsymbol{X}, t)$ that gives the current, or **spatial**, position $\boldsymbol{x}$ of a material point that occupied the **material** position $\boldsymbol{X}$ in a reference configuration. A motion is defined as **rigid** if it preserves the distance between any two material points at all times. Formally, for any pair of points $\boldsymbol{X}_1$ and $\boldsymbol{X}_2$ in the body, the following condition must hold for all time $t$:

$$
\|\boldsymbol{\chi}(\boldsymbol{X}_1, t) - \boldsymbol{\chi}(\boldsymbol{X}_2, t)\| = \|\boldsymbol{X}_1 - \boldsymbol{X}_2\|
$$

This defining property has immediate and profound consequences for the kinematic quantities that describe deformation [@problem_id:3596971]. To see this, let us consider an infinitesimal material vector $d\boldsymbol{X}$. Under the motion $\boldsymbol{\chi}$, this vector is mapped to a spatial vector $d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$, where $\boldsymbol{F} = \partial\boldsymbol{\chi}/\partial\boldsymbol{X}$ is the **[deformation gradient tensor](@entry_id:150370)**. The distance preservation condition, when applied to the squared norms of these infinitesimal vectors, requires that $d\boldsymbol{x} \cdot d\boldsymbol{x} = d\boldsymbol{X} \cdot d\boldsymbol{X}$. Substituting the relation for $d\boldsymbol{x}$ yields:

$$
(\boldsymbol{F}d\boldsymbol{X}) \cdot (\boldsymbol{F}d\boldsymbol{X}) = d\boldsymbol{X} \cdot (\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} d\boldsymbol{X}) = d\boldsymbol{X} \cdot d\boldsymbol{X}
$$

Since this must hold for any arbitrary vector $d\boldsymbol{X}$, it follows that the tensor within the parentheses must be the identity tensor. This leads to a fundamental algebraic constraint on the [deformation gradient](@entry_id:163749) for any rigid motion:

$$
\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} = \boldsymbol{I}
$$

where $\boldsymbol{I}$ is the second-order identity tensor. This result indicates that the deformation gradient $\boldsymbol{F}$ must be an **orthogonal tensor**. The tensor $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$ is known as the **right Cauchy-Green deformation tensor**, which measures the squared change in length of material line elements. For a [rigid motion](@entry_id:155339), $\boldsymbol{C} = \boldsymbol{I}$. Consequently, the **Green-Lagrange [strain tensor](@entry_id:193332)**, defined as $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I})$, vanishes completely: $\boldsymbol{E} = \boldsymbol{0}$. This is the mathematical statement of "no deformation" or "no strain" [@problem_id:3596973]. Conversely, if $\boldsymbol{E}=\boldsymbol{0}$ everywhere in a body, the motion is an isometry.

A physical motion must also preserve the orientation of the material, precluding transformations like reflections. This is enforced by requiring the Jacobian of the mapping, $J = \det(\boldsymbol{F})$, to be positive. For an orthogonal tensor, we know that $(\det \boldsymbol{F})^2 = \det(\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}) = \det(\boldsymbol{I}) = 1$, which implies $\det(\boldsymbol{F}) = \pm 1$. The orientation-preservation condition thus selects the positive root:

$$
\det(\boldsymbol{F}) = +1
$$

An orthogonal tensor with a determinant of $+1$ is known as a **proper orthogonal tensor** or a **[rotation tensor](@entry_id:191990)**. The set of all such $3 \times 3$ tensors forms the **Special Orthogonal Group**, denoted $\mathrm{SO}(3)$ [@problem_id:3597022].

A final piece of reasoning from [continuum kinematics](@entry_id:747813), stemming from [compatibility conditions](@entry_id:201103) on the displacement field, establishes that if $\boldsymbol{F}$ is a field of rotation tensors, it must be constant throughout the material body at any given instant. That is, $\boldsymbol{F}$ is independent of $\boldsymbol{X}$ and can be written solely as a function of time, $\boldsymbol{F}(t) = \boldsymbol{R}(t)$, where $\boldsymbol{R}(t) \in \mathrm{SO}(3)$. Integrating the relation $\partial\boldsymbol{\chi}/\partial\boldsymbol{X} = \boldsymbol{R}(t)$ with respect to $\boldsymbol{X}$ gives the most general form of a [rigid body motion](@entry_id:144691):

$$
\boldsymbol{x}(t) = \boldsymbol{R}(t)\boldsymbol{X} + \boldsymbol{c}(t)
$$

This is the celebrated theorem of Euler on the motion of a rigid body, stating that any rigid displacement can be decomposed into a rotation $\boldsymbol{R}(t)$ about the origin, followed by a translation $\boldsymbol{c}(t)$ [@problem_id:3596975].

### The Algebraic Structure of Rigid Motions

The set of all rigid motions forms a mathematical group known as the **Special Euclidean Group**, denoted $\mathrm{SE}(3)$. Understanding this group structure is essential for composing and inverting motions. A [rigid motion](@entry_id:155339) can be represented by the pair $(\boldsymbol{R}, \boldsymbol{c})$, where $\boldsymbol{R} \in \mathrm{SO}(3)$ and $\boldsymbol{c} \in \mathbb{R}^3$.

Consider two successive [rigid motions](@entry_id:170523). The first, $\mathcal{T}_1$, maps a point $\boldsymbol{x}_0$ to $\boldsymbol{x}_1 = \boldsymbol{R}_1 \boldsymbol{x}_0 + \boldsymbol{c}_1$. The second, $\mathcal{T}_2$, maps $\boldsymbol{x}_1$ to $\boldsymbol{x}_2 = \boldsymbol{R}_2 \boldsymbol{x}_1 + \boldsymbol{c}_2$. The composite motion $\mathcal{T}_2 \circ \mathcal{T}_1$ maps $\boldsymbol{x}_0$ directly to $\boldsymbol{x}_2$:

$$
\boldsymbol{x}_2 = \mathcal{T}_2(\mathcal{T}_1(\boldsymbol{x}_0)) = \boldsymbol{R}_2(\boldsymbol{R}_1 \boldsymbol{x}_0 + \boldsymbol{c}_1) + \boldsymbol{c}_2 = (\boldsymbol{R}_2\boldsymbol{R}_1)\boldsymbol{x}_0 + (\boldsymbol{R}_2\boldsymbol{c}_1 + \boldsymbol{c}_2)
$$

This reveals the composition rule for elements of $\mathrm{SE}(3)$:

$$
(\boldsymbol{R}_2, \boldsymbol{c}_2) \circ (\boldsymbol{R}_1, \boldsymbol{c}_1) = (\boldsymbol{R}_2\boldsymbol{R}_1, \boldsymbol{R}_2\boldsymbol{c}_1 + \boldsymbol{c}_2)
$$

A crucial feature of this composition is its general **non-commutativity**. That is, the order of operations matters. If we compose the motions in the reverse order, we obtain $(\boldsymbol{R}_1\boldsymbol{R}_2, \boldsymbol{R}_1\boldsymbol{c}_2 + \boldsymbol{c}_1)$, which is generally different. This is because matrix multiplication for rotations in three dimensions is not commutative ($\boldsymbol{R}_1\boldsymbol{R}_2 \neq \boldsymbol{R}_2\boldsymbol{R}_1$), and the translation vector of the first motion is transformed by the rotation of the second. For example, a rotation of $\pi/2$ about the z-axis followed by a rotation of $\pi/2$ about the x-axis yields a different final orientation than performing these operations in reverse order [@problem_id:3596967] [@problem_id:3596968].

The group structure also requires the existence of an inverse for every motion. The inverse motion maps the final configuration back to the initial one. Given $\boldsymbol{x}' = \boldsymbol{R}\boldsymbol{x} + \boldsymbol{c}$, we solve for $\boldsymbol{x}$:

$$
\boldsymbol{x} = \boldsymbol{R}^{-1}(\boldsymbol{x}' - \boldsymbol{c}) = \boldsymbol{R}^{\mathsf{T}}\boldsymbol{x}' - \boldsymbol{R}^{\mathsf{T}}\boldsymbol{c}
$$

Here we have used the property that the inverse of a rotation matrix is its transpose, $\boldsymbol{R}^{-1} = \boldsymbol{R}^{\mathsf{T}}$. Thus, the inverse of the motion $(\boldsymbol{R}, \boldsymbol{c})$ is $(\boldsymbol{R}^{\mathsf{T}}, -\boldsymbol{R}^{\mathsf{T}}\boldsymbol{c})$. Since $\boldsymbol{R}^{\mathsf{T}}$ is also a [proper rotation](@entry_id:141831), the inverse of a [rigid motion](@entry_id:155339) is itself a rigid motion, confirming the group property [@problem_id:3597007].

For computational purposes, it is often convenient to represent these transformations using $4 \times 4$ **homogeneous transformation matrices**:

$$
\boldsymbol{H} = \begin{pmatrix} \boldsymbol{R} & \boldsymbol{c} \\ \boldsymbol{0}^{\mathsf{T}} & 1 \end{pmatrix}
$$

In this formalism, composition of motions becomes simple [matrix multiplication](@entry_id:156035), and the inverse is given by $\boldsymbol{H}^{-1} = \begin{pmatrix} \boldsymbol{R}^{\mathsf{T}} & -\boldsymbol{R}^{\mathsf{T}}\boldsymbol{c} \\ \boldsymbol{0}^{\mathsf{T}} & 1 \end{pmatrix}$ [@problem_id:3597007].

### Velocity and Acceleration in Rigid Motion

The [time evolution](@entry_id:153943) of a rigid body's configuration is described by the velocity and acceleration of its constituent points. Differentiating the general form of the motion $\boldsymbol{x}(t) = \boldsymbol{R}(t)\boldsymbol{X} + \boldsymbol{c}(t)$ with respect to time gives the velocity of a material particle $\boldsymbol{X}$:

$$
\boldsymbol{V}(\boldsymbol{X}, t) = \dot{\boldsymbol{x}}(t) = \dot{\boldsymbol{R}}(t)\boldsymbol{X} + \dot{\boldsymbol{c}}(t)
$$

To express this in terms of spatial coordinates, we use $\boldsymbol{X} = \boldsymbol{R}^{\mathsf{T}}(t)(\boldsymbol{x}(t) - \boldsymbol{c}(t))$ to obtain the spatial velocity field $\boldsymbol{v}(\boldsymbol{x}, t)$:

$$
\boldsymbol{v}(\boldsymbol{x}, t) = \dot{\boldsymbol{R}}(t)\boldsymbol{R}^{\mathsf{T}}(t)(\boldsymbol{x}(t) - \boldsymbol{c}(t)) + \dot{\boldsymbol{c}}(t)
$$

The tensor $\boldsymbol{W}(t) = \dot{\boldsymbol{R}}(t)\boldsymbol{R}^{\mathsf{T}}(t)$ is the **spatial angular velocity tensor**, also known as the **[spin tensor](@entry_id:187346)**. By differentiating the identity $\boldsymbol{R}\boldsymbol{R}^{\mathsf{T}} = \boldsymbol{I}$ with respect to time, we find $\dot{\boldsymbol{R}}\boldsymbol{R}^{\mathsf{T}} + \boldsymbol{R}\dot{\boldsymbol{R}}^{\mathsf{T}} = \boldsymbol{0}$, which implies $\boldsymbol{W} + \boldsymbol{W}^{\mathsf{T}} = \boldsymbol{0}$. This proves that $\boldsymbol{W}$ is a **[skew-symmetric tensor](@entry_id:199349)** [@problem_id:3597034].

The [spatial velocity gradient](@entry_id:187198) is $\boldsymbol{L} = \nabla_{\boldsymbol{x}}\boldsymbol{v}$. From the expression for $\boldsymbol{v}(\boldsymbol{x}, t)$, we find $\boldsymbol{L}(t) = \dot{\boldsymbol{R}}(t)\boldsymbol{R}^{\mathsf{T}}(t) = \boldsymbol{W}(t)$. This is a remarkable result: for a [rigid body motion](@entry_id:144691), the entire [velocity gradient](@entry_id:261686) is skew-symmetric. Its symmetric part, the **[rate-of-deformation tensor](@entry_id:184787)** $\boldsymbol{D} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^{\mathsf{T}})$, is identically zero. This is consistent with the notion that a rigid body does not deform; there is no stretching or shearing [@problem_id:3596971].

Any $3 \times 3$ [skew-symmetric tensor](@entry_id:199349) $\boldsymbol{W}$ can be associated with a unique **[axial vector](@entry_id:191829)** $\boldsymbol{\omega}$ such that for any vector $\boldsymbol{y}$, the action $\boldsymbol{W}\boldsymbol{y}$ is equivalent to the cross product $\boldsymbol{\omega} \times \boldsymbol{y}$. Using this, the velocity field takes its familiar form:

$$
\boldsymbol{v}(\boldsymbol{x}, t) = \dot{\boldsymbol{c}}(t) + \boldsymbol{\omega}(t) \times (\boldsymbol{x}(t) - \boldsymbol{c}(t))
$$

This is the fundamental equation for the velocity of a point in a rigid body, decomposed into the translational velocity of a reference point and the velocity due to rotation about that point. This leads directly to the **[transport theorem](@entry_id:176504)** for a vector $\boldsymbol{a}$ that is fixed in the [rotating frame](@entry_id:155637) (i.e., $\boldsymbol{a}(t) = \boldsymbol{R}(t)\boldsymbol{A}$ for a constant $\boldsymbol{A}$). Its time derivative as seen from the spatial frame is $\dot{\boldsymbol{a}}(t) = \boldsymbol{\omega}(t) \times \boldsymbol{a}(t)$ [@problem_id:3596976].

Differentiating the velocity field once more yields the acceleration $\boldsymbol{a}(t) = \dot{\boldsymbol{v}}(t)$. A careful application of the product rule and substitution gives:

$$
\boldsymbol{a}(t) = \ddot{\boldsymbol{c}}(t) + \dot{\boldsymbol{\omega}}(t) \times (\boldsymbol{x}(t) - \boldsymbol{c}(t)) + \boldsymbol{\omega}(t) \times (\boldsymbol{\omega}(t) \times (\boldsymbol{x}(t) - \boldsymbol{c}(t)))
$$

The three terms on the right-hand side represent, respectively, the acceleration of the reference point, the **[tangential acceleration](@entry_id:173884)** due to changing angular velocity, and the **[centripetal acceleration](@entry_id:190458)** directed towards the axis of rotation [@problem_id:3597034].

### Parameterization and Linearization

While a rotation matrix $\boldsymbol{R}$ has nine components, it only represents three independent degrees of freedom due to the six constraints imposed by orthogonality. For computational and theoretical analysis, it is often desirable to use a minimal parameterization. A powerful choice is the **rotation vector** (or exponential coordinates) $\boldsymbol{\theta} \in \mathbb{R}^3$. The direction of $\boldsymbol{\theta}$ specifies the axis of rotation, and its magnitude $\|\boldsymbol{\theta}\|$ gives the angle of rotation in radians. The [rotation matrix](@entry_id:140302) is recovered via the **exponential map** from the Lie algebra $\mathfrak{so}(3)$ (the space of [skew-symmetric matrices](@entry_id:195119)) to the Lie group $\mathrm{SO}(3)$:

$$
\boldsymbol{R}(\boldsymbol{\theta}) = \exp(\hat{\boldsymbol{\theta}})
$$

where $\hat{\boldsymbol{\theta}}$ is the [skew-symmetric matrix](@entry_id:155998) associated with the [axial vector](@entry_id:191829) $\boldsymbol{\theta}$. The full configuration of a rigid body can thus be minimally described by a 6-parameter vector containing the three components of $\boldsymbol{\theta}$ and the three components of the translation vector $\boldsymbol{c}$ [@problem_id:3596975].

For small rotations, where $\|\boldsymbol{\theta}\| \ll 1$, the exponential map can be linearized to first order: $\boldsymbol{R}(\boldsymbol{\theta}) \approx \boldsymbol{I} + \hat{\boldsymbol{\theta}}$. Substituting this into the definition of the displacement field $\boldsymbol{u}(\boldsymbol{X}) = \boldsymbol{x}(\boldsymbol{X}) - \boldsymbol{X}$ yields:

$$
\boldsymbol{u}(\boldsymbol{X}) = (\boldsymbol{R}(\boldsymbol{\theta})\boldsymbol{X} + \boldsymbol{c}) - \boldsymbol{X} \approx ((\boldsymbol{I} + \hat{\boldsymbol{\theta}})\boldsymbol{X} + \boldsymbol{c}) - \boldsymbol{X} = \boldsymbol{c} + \hat{\boldsymbol{\theta}}\boldsymbol{X}
$$

Expressing the action of the [skew-symmetric matrix](@entry_id:155998) as a [cross product](@entry_id:156749), we arrive at the linearized [displacement field](@entry_id:141476) for a small [rigid body motion](@entry_id:144691):

$$
\boldsymbol{u}(\boldsymbol{X}) \approx \boldsymbol{c} + \boldsymbol{\theta} \times \boldsymbol{X}
$$

This approximation is central to linear [structural analysis](@entry_id:153861) and small-strain theories [@problem_id:3597015]. An important consequence of this [linearization](@entry_id:267670) is that [infinitesimal rotations](@entry_id:166635) commute. To first order, the composition of two small rotations $\boldsymbol{\theta}_1$ and $\boldsymbol{\theta}_2$ is simply $(\boldsymbol{I} + \hat{\boldsymbol{\theta}}_1)(\boldsymbol{I} + \hat{\boldsymbol{\theta}}_2) \approx \boldsymbol{I} + \hat{\boldsymbol{\theta}}_1 + \hat{\boldsymbol{\theta}}_2$, which is symmetric in $\boldsymbol{\theta}_1$ and $\boldsymbol{\theta}_2$. This contrasts sharply with the [non-commutativity](@entry_id:153545) of finite rotations and justifies the vector addition of angular velocities and [infinitesimal rotations](@entry_id:166635) in many engineering contexts [@problem_id:3596968].

### Rigid Motions and the Principle of Objectivity

The study of [rigid motions](@entry_id:170523) transcends kinematics; it forms the bedrock of the **Principle of Material Frame Indifference**, also known as the **Principle of Objectivity**. This axiom of continuum mechanics states that the constitutive laws governing a material's response must be independent of the observer. A change of observer is modeled as a superposed [rigid body motion](@entry_id:144691), where a new observer tracks points with coordinates $\boldsymbol{x}^*(t) = \boldsymbol{R}(t)\boldsymbol{x}(t) + \boldsymbol{c}(t)$, for some arbitrary time-dependent rotation $\boldsymbol{R}(t)$ and translation $\boldsymbol{c}(t)$ [@problem_id:3597041].

This principle imposes severe restrictions on the form of [constitutive equations](@entry_id:138559). Physical quantities are classified by how they transform under such an observer change. A scalar quantity $\phi$ is objective if $\phi^* = \phi$. A vector $\boldsymbol{v}$ is objective if $\boldsymbol{v}^* = \boldsymbol{R}\boldsymbol{v}$. A second-order tensor $\boldsymbol{T}$ is objective if $\boldsymbol{T}^* = \boldsymbol{R}\boldsymbol{T}\boldsymbol{R}^{\mathsf{T}}$. Analysis of the key kinematic and kinetic tensors reveals that:
- The deformation gradient $\boldsymbol{F}$ is **not objective**: $\boldsymbol{F}^* = \boldsymbol{R}\boldsymbol{F}$.
- The right Cauchy-Green tensor $\boldsymbol{C}$ is **objective**: $\boldsymbol{C}^* = (\boldsymbol{F}^*)^{\mathsf{T}}\boldsymbol{F}^* = (\boldsymbol{R}\boldsymbol{F})^{\mathsf{T}}(\boldsymbol{R}\boldsymbol{F}) = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R}\boldsymbol{F} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} = \boldsymbol{C}$.
- The Cauchy stress tensor $\boldsymbol{\sigma}$ is **objective**: $\boldsymbol{\sigma}^* = \boldsymbol{R}\boldsymbol{\sigma}\boldsymbol{R}^{\mathsf{T}}$.
- The [rate-of-deformation tensor](@entry_id:184787) $\boldsymbol{D}$ is **objective**: $\boldsymbol{D}^* = \boldsymbol{R}\boldsymbol{D}\boldsymbol{R}^{\mathsf{T}}$.
- The [spin tensor](@entry_id:187346) $\boldsymbol{W}$ is **not objective**: $\boldsymbol{W}^* = \boldsymbol{R}\boldsymbol{W}\boldsymbol{R}^{\mathsf{T}} + \dot{\boldsymbol{R}}\boldsymbol{R}^{\mathsf{T}}$.

The principle demands that if a [constitutive law](@entry_id:167255) relates a set of quantities, e.g., $\boldsymbol{\sigma} = \mathcal{T}(\boldsymbol{F}, \boldsymbol{D})$, then the same functional form must hold for the observer in the starred frame: $\boldsymbol{\sigma}^* = \mathcal{T}(\boldsymbol{F}^*, \boldsymbol{D}^*)$. This requires the function $\mathcal{T}$ to satisfy a specific covariance property. For example, since quantities like the scalar [stored-energy function](@entry_id:197811) $\psi$ must be objective ($\psi^* = \psi$), any dependence on the non-objective [deformation gradient](@entry_id:163749) $\boldsymbol{F}$ is constrained. Objectivity for $\psi(\boldsymbol{F})$ implies that $\psi(\boldsymbol{F}) = \psi(\boldsymbol{R}\boldsymbol{F})$ for all $\boldsymbol{R} \in \mathrm{SO}(3)$. This is satisfied if and only if $\psi$ depends on $\boldsymbol{F}$ only through the objective tensor $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$, leading to a reduced form $\psi = \widehat{\psi}(\boldsymbol{C})$ [@problem_id:3597041].

Similarly, for rate-dependent materials, the non-objectivity of the [spin tensor](@entry_id:187346) $\boldsymbol{W}$ (due to its dependence on the observer's spin $\dot{\boldsymbol{R}}\boldsymbol{R}^{\mathsf{T}}$) implies that constitutive laws for stress cannot depend on the spin part of the [velocity gradient](@entry_id:261686). They can, however, depend on the objective [rate-of-deformation tensor](@entry_id:184787) $\boldsymbol{D}$. This is why viscosity in a fluid generates stress in response to shearing and stretching rates ($\boldsymbol{D}$), but not in response to a pure [rigid body rotation](@entry_id:167024) ($\boldsymbol{W}$).

In [computational solid mechanics](@entry_id:169583), these principles are paramount. Numerical algorithms must respect objectivity. Furthermore, detecting whether a computed deformation is genuinely a deformation or merely a large [rigid motion](@entry_id:155339) is a practical challenge. Diagnostics for near-rigidity are often based on objective measures, such as the norm of the Green-Lagrange [strain tensor](@entry_id:193332), $\|\boldsymbol{E}\|_F$, or the distance of the computed [deformation gradient](@entry_id:163749) $\boldsymbol{F}$ from its closest [rotation matrix](@entry_id:140302) in $\mathrm{SO}(3)$. If such measures fall below a small tolerance, the motion at that point can be considered effectively rigid [@problem_id:3596973].