## Introduction
In the study of [computational solid mechanics](@entry_id:169583), describing how a body moves, deforms, and responds to forces is the central challenge. While we may have an intuitive grasp of these phenomena, a rigorous predictive science requires a precise mathematical framework. This article addresses the foundational knowledge gap between the qualitative idea of deformation and its quantitative description. It establishes the essential language and principles needed to analyze the kinematics of [deformable bodies](@entry_id:201887).

The journey begins in the first chapter, **Principles and Mechanisms**, which formalizes the concept of a continuum body, defines its reference and current configurations, and introduces the cornerstone of kinematic analysis: the deformation gradient. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the profound utility of these principles, bridging theory to practice by showing how they underpin the Finite Element Method, inform solutions to complex numerical challenges like [incompressibility](@entry_id:274914), and provide a common language for fields ranging from materials science to [medical imaging](@entry_id:269649). Finally, the **Hands-On Practices** section offers practical exercises to solidify your understanding of these core concepts. By progressing through these chapters, you will build a robust understanding of the kinematic bedrock upon which all of modern [continuum mechanics](@entry_id:155125) rests.

## Principles and Mechanisms

In the preceding chapter, we introduced the overarching goals of continuum mechanics. We now embark on a more rigorous journey, laying the mathematical and physical foundations required to describe the behavior of [deformable bodies](@entry_id:201887). This chapter formalizes the central concepts of a continuum body, its configurations, and the kinematic quantities used to describe its motion and deformation. A precise understanding of these principles is the bedrock upon which the entire edifice of [computational solid mechanics](@entry_id:169583) is built.

### The Continuum Body: Abstraction and Reality

The fundamental entity in our study is the **continuum body**. At a formal level, we may define a body $\mathcal{B}$ as a set of elements, called **material points** or particles, which is endowed with a mathematical structure (specifically, that of a [differentiable manifold](@entry_id:266623)) that allows us to speak of [continuity and differentiability](@entry_id:160718). A **configuration** of the body is a mapping of this abstract set into the three-dimensional Euclidean space $\mathbb{R}^3$, representing a physical placement of the body in space. Kinematic and physical quantities, such as velocity and stress, are then described by continuous fields defined on the body .

This definition, while mathematically elegant, may seem disconnected from the physical reality of materials, which are composed of discrete atoms and molecules. The bridge between the discrete microscopic world and our continuous macroscopic model is the **[continuum hypothesis](@entry_id:154179)**. This hypothesis is not a universal truth but an assumption, the validity of which rests on a clear **separation of scales**.

For the continuum model to be meaningful, we must be able to define a **Representative Volume Element (RVE)**. The characteristic length scale of this element, let us call it $\ell$, must be large enough to contain a vast number of atoms and microstructural features (like grains or voids), so that properties averaged over this volume, such as mass density, are statistically stable and representative of the material as a whole. At the same time, $\ell$ must be small enough to be considered a mathematical "point" with respect to the macroscopic dimensions of the problem.

This leads to a fundamental set of inequalities that must be satisfied for a continuum description to be valid. Let $a$ be the scale of the discrete lattice (e.g., atomic spacing), $\xi$ be the [characteristic length](@entry_id:265857) of the [microstructure](@entry_id:148601) (e.g., [grain size](@entry_id:161460) or correlation length), $L$ be a characteristic macroscopic dimension of the body, and $\lambda$ be the wavelength of any dynamic phenomena (like stress waves) we wish to resolve. The coarse-graining length $\ell$ of our continuum model must satisfy:

$$ a, \xi \ll \ell \ll \min\{L, \lambda\} $$

Furthermore, for a scale $\ell$ to be truly representative, the fluctuation of averaged properties over volumes of size $\ell^3$ must be below some acceptable tolerance. For instance, consider a crystalline solid with [lattice spacing](@entry_id:180328) $a = 5 \times 10^{-10}$ m, microstructural [correlation length](@entry_id:143364) $\xi = 5 \times 10^{-8}$ m, and a macroscopic size $L = 10^{-2}$ m. Suppose it is subjected to ultrasonic waves with a wavelength $\lambda = 10^{-3}$ m. A [coarse-graining](@entry_id:141933) scale of $\ell = 10^{-6}$ m would be a valid choice if the material properties are statistically representative at this scale. It satisfies the separation of scales, as $5 \times 10^{-8} \text{ m} \ll 10^{-6} \text{ m} \ll 10^{-3} \text{ m}$. If, for example, the measured fluctuation in mass density at this scale is below a tolerance of $1\%$, the [continuum hypothesis](@entry_id:154179) is well justified . In contrast, attempting to model the wave phenomenon with a coarse-graining length $\ell \ge \lambda$ would fail, as the model would be spatially too coarse to resolve the wave's oscillations.

It is critical to recognize that a material point in [continuum mechanics](@entry_id:155125) is not an atom. It is an abstraction representing the RVE. Conservation laws, such as mass conservation, are not applied by tracking individual atoms but by formulating balance equations for continuous fields like the mass density $\rho$ .

### Configuration and Motion: Describing Deformation

To describe the deformation of a body, we track the positions of its material points over time. This is accomplished within the **Lagrangian** or **material description**.

We select a specific, fixed configuration of the body as our **reference configuration**, denoted by the region $\mathcal{B}_0 \subset \mathbb{R}^3$. The position vector of a material point in this configuration, $\mathbf{X}$, is called the **material coordinate**. This vector serves as a permanent, time-independent label for that material point.

As the body deforms, it occupies a sequence of **current configurations**, $\mathcal{B}_t \subset \mathbb{R}^3$, at each time $t$. The position of the material point $\mathbf{X}$ at time $t$ is given by the **spatial coordinate** $\mathbf{x}$. The relationship between these coordinates is described by the **motion**, which is a map $\boldsymbol{\varphi}$:

$$ \mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t) $$

This map takes a material point label $\mathbf{X}$ from the reference configuration and gives its spatial position $\mathbf{x}$ in the current configuration at time $t$ .

For a motion to be physically admissible, the map $\boldsymbol{\varphi}(\cdot, t)$ must satisfy several key properties for each time $t$. It must be sufficiently smooth to allow for the definition of derivatives. Crucially, it must be **injective** (one-to-one), meaning that two distinct material points cannot occupy the same spatial location at the same time. If $\mathbf{X}_1 \neq \mathbf{X}_2$, then we must have $\boldsymbol{\varphi}(\mathbf{X}_1, t) \neq \boldsymbol{\varphi}(\mathbf{X}_2, t)$. This is the mathematical expression of the axiom of **impenetrability of matter**. A failure of injectivity implies a physically impossible self-overlap or interpenetration of the material . Finally, the mapping must be **orientation-preserving**, a concept we will quantify shortly. In mathematical terms, a physically admissible motion is a time-dependent **embedding** of $\mathcal{B}_0$ into $\mathbb{R}^3$.

### The Deformation Gradient: A Local Measure of Deformation

The motion $\boldsymbol{\varphi}$ describes the deformation globally. To characterize the deformation locally—at a single material point—we introduce the **deformation gradient**, denoted by the tensor $\mathbf{F}$. It is defined as the gradient of the motion map with respect to the material coordinates:

$$ \mathbf{F}(\mathbf{X}, t) = \nabla_{\mathbf{X}}\boldsymbol{\varphi}(\mathbf{X}, t) \quad \text{or in components,} \quad F_{ij} = \frac{\partial x_i}{\partial X_j} $$

The deformation gradient $\mathbf{F}$ is a two-point tensor, as it relates quantities in two different configurations. Its fundamental role is that of a **[tangent map](@entry_id:203492)**: it linearly transforms an infinitesimal vector element $d\mathbf{X}$ originating from the material point $\mathbf{X}$ in the reference configuration into the corresponding vector element $d\mathbf{x}$ at the spatial point $\mathbf{x}$ in the current configuration.

$$ d\mathbf{x} = \mathbf{F} \, d\mathbf{X} $$

This relationship is exact for infinitesimal vectors and forms the basis for understanding how lengths and angles are transformed during deformation.

To make this concrete, consider a motion given by $\boldsymbol{\varphi}(\mathbf{X},t) = ((1+t)X_1 + 2tX_2, (1+t^2)X_2, (1+t)X_3 + 3tX_1 X_2)^{\mathsf{T}}$. The [deformation gradient tensor](@entry_id:150370) is the matrix of partial derivatives:
$$ \mathbf{F}(\mathbf{X},t) = \begin{bmatrix} 1+t & 2t & 0 \\ 0 & 1+t^2 & 0 \\ 3tX_2 & 3tX_1 & 1+t \end{bmatrix} $$
At time $t=1$ and the material point $\mathbf{X}=(1,2,0)^{\mathsf{T}}$, this tensor becomes:
$$ \mathbf{F} = \begin{bmatrix} 2 & 2 & 0 \\ 0 & 2 & 0 \\ 6 & 3 & 2 \end{bmatrix} $$
If we consider a material line element $d\mathbf{X} = (1, -1, 2)^{\mathsf{T}}$ at this point, its deformed counterpart $d\mathbf{x}$ is found by the [matrix-vector product](@entry_id:151002):
$$ d\mathbf{x} = \mathbf{F} \, d\mathbf{X} = \begin{bmatrix} 2 & 2 & 0 \\ 0 & 2 & 0 \\ 6 & 3 & 2 \end{bmatrix} \begin{bmatrix} 1 \\ -1 \\ 2 \end{bmatrix} = \begin{bmatrix} 0 \\ -2 \\ 7 \end{bmatrix} $$
This calculation demonstrates how $\mathbf{F}$ captures the local stretching and rotation that transforms the material element $d\mathbf{X}$ into the spatial element $d\mathbf{x}$ .

#### The Jacobian Determinant

A particularly important scalar quantity derived from the deformation gradient is its determinant, known as the **Jacobian**, $J$:

$$ J(\mathbf{X}, t) = \det \mathbf{F}(\mathbf{X}, t) $$

The Jacobian has several crucial physical interpretations :
1.  **Volume Ratio**: It represents the local change in volume. An infinitesimal [volume element](@entry_id:267802) $dV$ in the reference configuration is mapped to a volume element $dv$ in the current configuration according to the relation $dv = J \, dV$. Thus, $J$ is the local ratio of current volume to reference volume.
2.  **Orientation**: A physically admissible motion must be orientation-preserving, which requires that $J > 0$. A positive Jacobian ensures that a right-handed set of basis vectors in the material remains right-handed after deformation. A negative Jacobian would imply a local inversion of material, turning it "inside-out," which is considered physically impossible for real matter.
3.  **Mass Conservation**: The principle of conservation of mass for a material volume implies a direct pointwise relationship between the [current density](@entry_id:190690) $\rho(\mathbf{x}, t)$ and the reference density $\rho_0(\mathbf{X})$:
    $$ \rho J = \rho_0 \quad \text{or} \quad \rho(\boldsymbol{\varphi}(\mathbf{X}, t), t) = \frac{\rho_0(\mathbf{X})}{J(\mathbf{X}, t)} $$
    This equation shows that as a material expands ($J>1$), its density decreases, and as it contracts ($J1$), its density increases.
4.  **Incompressibility**: A material is said to be **incompressible** if its volume does not change during deformation. This kinematic constraint implies that $dv = dV$ everywhere, which requires $J=1$ for all $\mathbf{X}$ and $t$. Consequently, for an [incompressible material](@entry_id:159741), the density remains constant: $\rho = \rho_0$. A deformation such as $\mathbf{F} = \mathrm{diag}(2, 1/2, 1)$ results in $J = 2 \times 0.5 \times 1 = 1$ and is thus locally volume-preserving (isochoric) .

#### Advanced Topic: On Global Injectivity

It is a common misconception that the condition $J0$ everywhere is sufficient to guarantee the non-interpenetration of matter. The [inverse function theorem](@entry_id:138570) ensures that $J0$ implies the motion $\boldsymbol{\varphi}$ is *locally* one-to-one. However, it does not prevent two distant material points from being mapped to the same spatial location, which would violate *global* injectivity. For instance, a sheet can be rolled into a cylinder, a motion where $J0$ everywhere, but if the sheet overlaps itself, the mapping is not globally injective.

The rigorous mathematical conditions for ensuring global [injectivity](@entry_id:147722) ([almost everywhere](@entry_id:146631)) are more subtle. For a sufficiently [smooth map](@entry_id:160364) $\boldsymbol{\varphi}$, a key result from Ciarlet and Nečas establishes that in addition to $J0$ and [injectivity](@entry_id:147722) on the body's boundary, the mapping must satisfy the inequality:
$$ \int_{\mathcal{B}_0} J(\mathbf{X}) \, dV \le \mathcal{L}^3(\boldsymbol{\varphi}(\mathcal{B}_0)) $$
where $\mathcal{L}^3$ is the Lebesgue measure (volume) of the deformed domain. Since the [change of variables](@entry_id:141386) formula from [geometric measure theory](@entry_id:187987) always guarantees the reverse inequality, imposing this condition forces equality, which in turn implies that the mapping is one-to-one almost everywhere. Failure to meet these conditions is the precise mathematical statement of material interpenetration .

### Kinematics: Rates of Motion and Deformation

To formulate [constitutive laws](@entry_id:178936) for materials like viscous fluids or to study dynamic problems, we must describe the *rates* at which deformation occurs. This involves analyzing the [velocity field](@entry_id:271461) and its gradients.

The **material velocity** is the time derivative of the position of a material point $\mathbf{X}$, given by $\mathbf{V}(\mathbf{X}, t) = \frac{\partial}{\partial t}\boldsymbol{\varphi}(\mathbf{X}, t)$. However, it is often more convenient to express the velocity as a function of the current spatial position, $\mathbf{x}$. This gives the **spatial velocity** field $\mathbf{v}(\mathbf{x}, t)$. The spatial gradient of this [velocity field](@entry_id:271461), $\mathbf{L} = \nabla_{\mathbf{x}}\mathbf{v}$, is known as the **velocity gradient**. It plays a role in the current configuration analogous to that of $\mathbf{F}$ in the reference configuration.

A fundamental relationship connects the [material time derivative](@entry_id:190892) of the deformation gradient, $\dot{\mathbf{F}}$, to the [spatial velocity gradient](@entry_id:187198) $\mathbf{L}$ :
$$ \dot{\mathbf{F}} = \mathbf{L} \mathbf{F} \quad \implies \quad \mathbf{L} = \dot{\mathbf{F}} \mathbf{F}^{-1} $$
This identity is a cornerstone of [finite deformation kinematics](@entry_id:195826), linking the material and spatial descriptions of motion.

The [velocity gradient](@entry_id:261686) $\mathbf{L}$ can be additively decomposed into its symmetric and skew-symmetric parts:
$$ \mathbf{L} = \mathbf{D} + \mathbf{W} $$
where
- $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\mathsf{T}})$ is the **[rate-of-deformation tensor](@entry_id:184787)** (or stretching tensor).
- $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^{\mathsf{T}})$ is the **[spin tensor](@entry_id:187346)** (or [vorticity tensor](@entry_id:189621)).

This decomposition has a profound physical meaning. The [rate-of-deformation tensor](@entry_id:184787) $\mathbf{D}$ describes the rate at which material line elements are being stretched or sheared. The rate of change of the squared length of a spatial [line element](@entry_id:196833) $d\mathbf{x}$ is given exclusively by $\mathbf{D}$:
$$ \frac{d}{dt}(\|d\mathbf{x}\|^2) = 2 d\mathbf{x} \cdot \mathbf{D} d\mathbf{x} $$
The [spin tensor](@entry_id:187346) $\mathbf{W}$, being skew-symmetric, makes no contribution to the rate of change of length, as $d\mathbf{x} \cdot \mathbf{W} d\mathbf{x} = 0$. Instead, $\mathbf{W}$ describes the average rate of [rigid-body rotation](@entry_id:268623) (vorticity) of the material at a point .

The incompressibility condition, which states that volume is preserved, can also be expressed in terms of these rate measures. The rate of change of a volume element is given by $d\dot{v} = (\mathrm{tr}(\mathbf{L})) dv$. Therefore, incompressibility requires $\mathrm{tr}(\mathbf{L})=0$. Since the trace of any [skew-symmetric tensor](@entry_id:199349) is zero ($\mathrm{tr}(\mathbf{W})=0$), we have $\mathrm{tr}(\mathbf{L}) = \mathrm{tr}(\mathbf{D})$. The [incompressibility constraint](@entry_id:750592) is thus equivalent to the condition that the trace of the [rate-of-deformation tensor](@entry_id:184787) is zero:
$$ \mathrm{tr}(\mathbf{D}) = 0 $$

### Objectivity and Frame-Indifference

Physical laws cannot depend on the observer. In mechanics, this is formalized as the **[principle of material objectivity](@entry_id:191727)** or [frame-indifference](@entry_id:197245). It states that [constitutive equations](@entry_id:138559) must be invariant under a change of frame, which is represented by a time-dependent [rigid-body motion](@entry_id:265795). If a motion is described by $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$ in one frame, an observer in a different frame, rotating with orientation $\mathbf{Q}(t)$ and translating by $\mathbf{c}(t)$ relative to the first, would describe the same motion as:
$$ \hat{\mathbf{x}} = \mathbf{c}(t) + \mathbf{Q}(t) \mathbf{x} $$
where $\mathbf{Q}(t)$ is a proper orthogonal tensor ($\mathbf{Q}^{\mathsf{T}}\mathbf{Q} = \mathbf{I}$, $\det\mathbf{Q}=1$).

Applying this transformation, we can find how various kinematic quantities change between frames. A quantity is said to be **objective** if its transformation law accounts only for the rigid rotation of the spatial frame.

-   **Objective Vectors and Tensors**: A spatial vector $\mathbf{u}$ transforms as $\hat{\mathbf{u}} = \mathbf{Q}\mathbf{u}$. An objective spatial second-order tensor $\mathbf{T}$ transforms as $\hat{\mathbf{T}} = \mathbf{Q}\mathbf{T}\mathbf{Q}^{\mathsf{T}}$. 
-   **Transformation of Kinematic Measures**:
    -   Deformation Gradient: $\hat{\mathbf{F}} = \mathbf{Q}\mathbf{F}$. (Not objective)
    -   Right Cauchy-Green Tensor $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$: $\hat{\mathbf{C}} = \hat{\mathbf{F}}^{\mathsf{T}}\hat{\mathbf{F}} = (\mathbf{Q}\mathbf{F})^{\mathsf{T}}(\mathbf{Q}\mathbf{F}) = \mathbf{F}^{\mathsf{T}}\mathbf{Q}^{\mathsf{T}}\mathbf{Q}\mathbf{F} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = \mathbf{C}$. The tensor $\mathbf{C}$ is a [material tensor](@entry_id:196294) and is inherently objective (invariant).
    -   Left Cauchy-Green Tensor $\mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}}$: $\hat{\mathbf{B}} = \hat{\mathbf{F}}\hat{\mathbf{F}}^{\mathsf{T}} = (\mathbf{Q}\mathbf{F})(\mathbf{Q}\mathbf{F})^{\mathsf{T}} = \mathbf{Q}(\mathbf{F}\mathbf{F}^{\mathsf{T}})\mathbf{Q}^{\mathsf{T}} = \mathbf{Q}\mathbf{B}\mathbf{Q}^{\mathsf{T}}$. The tensor $\mathbf{B}$ is an objective [spatial tensor](@entry_id:185799).
    -   Velocity Gradient: $\hat{\mathbf{L}} = \mathbf{Q}\mathbf{L}\mathbf{Q}^{\mathsf{T}} + \dot{\mathbf{Q}}\mathbf{Q}^{\mathsf{T}}$. The affine term $\dot{\mathbf{Q}}\mathbf{Q}^{\mathsf{T}}$ (the [angular velocity](@entry_id:192539) of the frame change) means $\mathbf{L}$ is not objective.
    -   Rate-of-Deformation and Spin: From the transformation of $\mathbf{L}$, it follows that $\hat{\mathbf{D}} = \mathbf{Q}\mathbf{D}\mathbf{Q}^{\mathsf{T}}$ (objective) and $\hat{\mathbf{W}} = \mathbf{Q}\mathbf{W}\mathbf{Q}^{\mathsf{T}} + \dot{\mathbf{Q}}\mathbf{Q}^{\mathsf{T}}$ (not objective) .

The [principle of objectivity](@entry_id:185412) places a strict constraint on [constitutive modeling](@entry_id:183370): any proposed material law must relate objective quantities only. For example, a constitutive law for stress must express an objective stress measure as a function of an [objective strain measure](@entry_id:752864).

### Mapping Between Configurations: Push-Forward and Pull-Back

Since [physical quantities](@entry_id:177395) can be defined in either the reference or the current configuration, we need a systematic way to map them from one to the other. These operations are known as **push-forward** (from reference to current) and **pull-back** (from current to reference). The [deformation gradient](@entry_id:163749) $\mathbf{F}$ and its inverse $\mathbf{F}^{-1}$ are the fundamental tools for these mappings .

-   **Vectors**: As we have seen, a material vector $\mathbf{V}$ is pushed forward to a spatial vector $\mathbf{v}$ via $\mathbf{v} = \mathbf{F}\mathbf{V}$. Conversely, a spatial vector $\mathbf{v}$ is pulled back to a material vector $\mathbf{V}$ via $\mathbf{V} = \mathbf{F}^{-1}\mathbf{v}$.

-   **Gradients of Scalar Fields**: Let $f$ be a [scalar field](@entry_id:154310), with spatial representation $f(\mathbf{x})$ and material representation $\hat{f}(\mathbf{X}) = f(\boldsymbol{\varphi}(\mathbf{X}))$. Using the [chain rule](@entry_id:147422), their gradients are related by $\nabla_{\mathbf{X}}\hat{f} = \mathbf{F}^{\mathsf{T}} \nabla_{\mathbf{x}}f$. This can be rearranged to express the pull-back of the spatial [gradient operator](@entry_id:275922):
    $$ \nabla_{\mathbf{x}}f = \mathbf{F}^{-\mathsf{T}} \nabla_{\mathbf{X}}\hat{f} $$
    The appearance of the inverse transpose, $\mathbf{F}^{-\mathsf{T}}$, is a general feature when transforming covariant quantities like gradients.

-   **Second-Order Tensors**: The transformation rule for a tensor depends on its physical nature (e.g., whether it acts on vectors, co-vectors, or is a bilinear form). For a tensor $\boldsymbol{\tau}$ in the current configuration that acts as a linear operator on spatial vectors, its pull-back $\mathbf{T}$ to the reference configuration is found by ensuring the mapping diagram commutes, which yields:
    $$ \mathbf{T} = \mathbf{F}^{-1} \boldsymbol{\tau} \mathbf{F} $$
    This is different from the transformation rule for other types of tensors, such as stress tensors.

#### Stress Tensors and Work Conjugacy

The concept of pull-back is essential for defining [stress measures](@entry_id:198799) that are independent of rigid-body rotations. While the **Cauchy stress** $\boldsymbol{\sigma}$ is the most intuitive stress measure—it is symmetric and relates forces and areas in the current configuration—it is not ideal for formulating constitutive laws in [solid mechanics](@entry_id:164042) because both the stress and the body's configuration change during deformation. It is often preferable to relate a stress measure defined on the fixed reference configuration to a strain measure also defined on the reference configuration.

This leads to the introduction of two other important stress tensors:
1.  The **First Piola-Kirchhoff (1st PK) Stress** $\mathbf{P}$: This is a two-point tensor that relates the force in the current configuration to the area in the reference configuration. It is the pull-back of the Cauchy stress via the relation $\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-\mathsf{T}}$. Note that $\mathbf{P}$ is generally not symmetric.
2.  The **Second Piola-Kirchhoff (2nd PK) Stress** $\mathbf{S}$: This is a fully [material tensor](@entry_id:196294), obtained by pulling back the 1st PK stress: $\mathbf{S} = \mathbf{F}^{-1}\mathbf{P} = J \mathbf{F}^{-1}\boldsymbol{\sigma}\mathbf{F}^{-\mathsf{T}}$. The 2nd PK stress is symmetric and is energetically conjugate to the Green-Lagrange [strain tensor](@entry_id:193332), making it extremely useful in [hyperelasticity](@entry_id:168357).

The choice of [stress and strain](@entry_id:137374) measures is not arbitrary; they must be **energetically conjugate**. The principle of virtual power states that the internal [power density](@entry_id:194407) must be independent of the configuration in which it is expressed. This leads to the following work-conjugate pairs :
$$ \frac{dW_{int}}{dt} = \int_{\mathcal{B}_t} \boldsymbol{\sigma} : \mathbf{D} \, dv = \int_{\mathcal{B}_0} \mathbf{P} : \dot{\mathbf{F}} \, dV = \int_{\mathcal{B}_0} \mathbf{S} : \dot{\mathbf{E}} \, dV $$
Here, $\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I})$ is the Green-Lagrange strain tensor and $\dot{\mathbf{E}}$ is its [material time derivative](@entry_id:190892). This reveals the fundamental pairings: $(\boldsymbol{\sigma}, \mathbf{D})$, $(\mathbf{P}, \dot{\mathbf{F}})$, and $(\mathbf{S}, \dot{\mathbf{E}})$.

### The Reference Configuration: A Deeper Look

In classical elasticity, we often assume the existence of a **natural state**—a reference configuration $\mathcal{B}_0$ that the body occupies when it is free of all external loads and internal stresses. However, for many important classes of materials and processes, such a global stress-free configuration may not exist. This occurs in materials with **residual stresses**, which may arise from [plastic deformation](@entry_id:139726), thermal processing, or, in biological tissues, [differential growth](@entry_id:274484).

This situation can be elegantly described using a [multiplicative decomposition](@entry_id:199514) of the deformation gradient, $F=F_e F_g$, where $F_e$ is the elastic deformation that generates stress, and $F_g$ is a prescribed, generally incompatible, inelastic deformation (e.g., plastic strain or growth). A stress-free state would require the elastic part $F_e$ to be a pure [rigid-body rotation](@entry_id:268623) everywhere. This, in turn, implies that the total deformation $F = R F_g$ (for some rotation field $R$) must be a compatible gradient, meaning there must exist a motion $\varphi$ such that $\nabla\varphi = R F_g$.

A fundamental result from [differential geometry](@entry_id:145818) states that a [tensor field](@entry_id:266532) can be the gradient of a mapping on a [simply connected domain](@entry_id:197423) if and only if its curl is zero. The existence of a stress-free configuration is therefore equivalent to the existence of a rotation field $R(\mathbf{X})$ such that $\mathrm{Curl}(R(\mathbf{X})F_g(\mathbf{X})) = 0$. For a general, non-uniform inelastic field $F_g$, such a rotation field does not exist. Geometrically, this is equivalent to stating that the Riemannian manifold described by the metric tensor $\bar{g} = F_g^{\mathsf{T}} F_g$ is not flat (i.e., its Riemann curvature tensor is non-zero). Such a manifold cannot be isometrically embedded in Euclidean space without generating elastic strain, and thus stress .

The non-existence of a stress-free state has profound implications for computational modeling. Since we cannot start our simulation from a physically realizable stress-free body, we must choose a reference configuration and explicitly account for the initial, self-equilibrated residual stresses. A common and consistent practice is to use the body's known, as-is configuration as the reference $\mathcal{B}_0$. The simulation is then initialized with a non-zero, self-equilibrated [initial stress](@entry_id:750652) field $P_0$ (satisfying $\mathrm{Div} P_0=0$) or an incompatible inelastic field $F_g$ from which the [initial stress](@entry_id:750652) can be calculated. Ignoring this fact and simply assuming a stress-free initial state for a body with an incompatible inelastic history will lead to an incorrect prediction of its mechanical response .