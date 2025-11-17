## Introduction
In the realm of solid mechanics, understanding how materials deform under load is paramount. While classical theories based on infinitesimal strains serve well for stiff structures undergoing small displacements, they fall short when describing the behavior of soft materials, ductile metals, or structures experiencing [large rotations](@entry_id:751151). The field of **Finite Deformation Kinematics** provides the rigorous mathematical language needed to navigate these complex scenarios, offering a precise description of motion and distortion irrespective of the forces involved. This article addresses the fundamental challenge of quantifying large deformations by developing a framework that correctly distinguishes true material distortion from [rigid body motion](@entry_id:144691). Over the next three chapters, we will construct this framework from the ground up. We will begin in **Principles and Mechanisms** by defining the foundational concepts, including the [deformation gradient](@entry_id:163749), polar decomposition, and objective [strain measures](@entry_id:755495). Next, in **Applications and Interdisciplinary Connections**, we will explore how these kinematic tools form the bedrock of modern [constitutive modeling](@entry_id:183370) for [hyperelasticity](@entry_id:168357) and plasticity, and their use in fields from biomechanics to computational engineering. Finally, **Hands-On Practices** will offer the opportunity to apply these principles to concrete problems, bridging the gap between abstract theory and practical implementation.

## Principles and Mechanisms

The kinematics of [finite deformation](@entry_id:172086) provide the mathematical language to describe the motion and distortion of a continuous body, irrespective of the forces that cause them. This chapter lays the foundational principles and mechanisms for this description, moving from the local mapping of infinitesimal elements to comprehensive measures of strain, rotation, and their rates of change. We establish a rigorous framework that serves as the essential geometric prelude to the study of material constitutive behavior.

### The Deformation Gradient

The cornerstone of [finite deformation](@entry_id:172086) [kinematics](@entry_id:173318) is the **[deformation gradient tensor](@entry_id:150370)**, denoted by $\mathbf{F}$. Consider a body occupying a reference configuration $\mathcal{B}_0$ at time $t=0$ and a current configuration $\mathcal{B}_t$ at time $t$. The motion is a smooth mapping $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$ that takes a material point from its position $\mathbf{X}$ in $\mathcal{B}_0$ to its position $\mathbf{x}$ in $\mathcal{B}_t$. The deformation gradient is defined as the gradient of this mapping with respect to the material (or referential) coordinates:

$$
\mathbf{F}(\mathbf{X}, t) = \frac{\partial \boldsymbol{\chi}(\mathbf{X}, t)}{\partial \mathbf{X}} \equiv \nabla_{\mathbf{X}} \boldsymbol{\chi}(\mathbf{X}, t)
$$

In component form, with respect to a Cartesian basis, this reads $F_{iI} = \frac{\partial x_i}{\partial X_I}$. Here, we adopt the convention of using uppercase indices for referential coordinates and lowercase indices for spatial coordinates.

The fundamental physical interpretation of $\mathbf{F}$ is that it describes the local deformation at a material point. It is the unique linear transformation that maps an infinitesimal material [line element](@entry_id:196833) $d\mathbf{X}$ originating at $\mathbf{X}$ to its corresponding spatial [line element](@entry_id:196833) $d\mathbf{x}$ at the deformed position $\mathbf{x}$. This relationship can be seen from a first-order Taylor [series expansion](@entry_id:142878) of the motion for a neighboring point $\mathbf{X} + d\mathbf{X}$:

$$
\boldsymbol{\chi}(\mathbf{X} + d\mathbf{X}, t) = \boldsymbol{\chi}(\mathbf{X}, t) + \nabla_{\mathbf{X}} \boldsymbol{\chi}(\mathbf{X}, t) \, d\mathbf{X} + o(\|d\mathbf{X}\|)
$$

Recognizing that $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$ and the spatial line element is $d\mathbf{x} = \boldsymbol{\chi}(\mathbf{X} + d\mathbf{X}, t) - \boldsymbol{\chi}(\mathbf{X}, t)$, we arrive at the pivotal relationship [@problem_id:2639558]:

$$
d\mathbf{x} = \mathbf{F} \, d\mathbf{X}
$$

This equation reveals that $\mathbf{F}$ acts as a local [linear map](@entry_id:201112) on [tangent vectors](@entry_id:265494), pushing them forward from the [tangent space](@entry_id:141028) of the reference configuration to the [tangent space](@entry_id:141028) of the current configuration. For this reason, $\mathbf{F}$ is often called a **two-point tensor**, as it connects quantities defined at two different points in spacetime ($\mathbf{X}$ and $\mathbf{x}$).

### Physical Admissibility and Compatibility

While any [tensor field](@entry_id:266532) $\mathbf{F}(\mathbf{X})$ can be conceived mathematically, a physically realistic deformation must satisfy certain conditions of admissibility. The primary local condition relates to the **Jacobian** of the deformation, $J = \det \mathbf{F}$. From linear algebra, we know that the volume of an infinitesimal parallelepiped spanned by three material vectors $\{d\mathbf{X}_1, d\mathbf{X}_2, d\mathbf{X}_3\}$ transforms according to $dV_t = (\det \mathbf{F}) dV_0$. This means $J$ is the local ratio of the current volume to the reference volume.

For a physical deformation, we require that matter does not penetrate itself and that orientation is preserved. This leads to the condition of **local admissibility** [@problem_id:2639570]:

$$
J = \det \mathbf{F} > 0
$$

A value of $J  0$ would imply an inversion of the material element (a right-handed set of basis vectors becomes left-handed), which is physically untenable for real materials. A value of $J=0$ implies that a [finite volume](@entry_id:749401) of material has been compressed into a surface or line of zero volume. For any material with an initial mass density $\rho_0 > 0$, conservation of mass, $\rho_t = \rho_0 / J$, would demand an infinite density $\rho_t$ at that point, which is also physically impossible. Therefore, $J>0$ is a necessary local condition. However, it is not sufficient for global admissibility, as a mapping can satisfy $J>0$ everywhere yet still feature self-penetration, requiring the stronger condition of global [injectivity](@entry_id:147722) [@problem_id:2639570] [@problem_id:2639523].

An inverse question of profound importance is: given a [tensor field](@entry_id:266532) $\mathbf{F}(\mathbf{X})$, does a corresponding single-valued deformation mapping $\boldsymbol{\chi}(\mathbf{X})$ exist such that $\mathbf{F} = \nabla_{\mathbf{X}}\boldsymbol{\chi}$? For this to be true, the field $\mathbf{F}$ must be **compatible**. For a continuously differentiable $\mathbf{F}$ on a [simply connected domain](@entry_id:197423), the necessary and sufficient condition is that the curl of each row of $\mathbf{F}$ must vanish. This is a direct consequence of the equality of [mixed partial derivatives](@entry_id:139334) ($\partial^2 \chi_i / \partial X_J \partial X_K = \partial^2 \chi_i / \partial X_K \partial X_J$). This condition is written compactly as:

$$
\operatorname{Curl} \mathbf{F} = \mathbf{0}
$$

Geometrically, this condition ensures that the [line integral](@entry_id:138107) $\oint_\gamma \mathbf{F} \, d\mathbf{X}$ is zero for any closed loop $\gamma$ in a [simply connected domain](@entry_id:197423). In materials science, a non-zero value of this integral is known as the **Burgers vector**, which quantifies the geometric misfit associated with a crystallographic defect like a dislocation. An incompatible field, $\operatorname{Curl} \mathbf{F} \neq \mathbf{0}$, thus describes a body containing a [continuous distribution](@entry_id:261698) of such defects [@problem_id:2639523].

### Polar Decomposition: Stretch and Rotation

The [deformation gradient](@entry_id:163749) $\mathbf{F}$ encapsulates all local information about the deformation: both stretching (change in shape and size) and rigid rotation. The **[polar decomposition theorem](@entry_id:753554)** provides a unique and powerful way to separate these two effects. Any invertible tensor $\mathbf{F}$ can be multiplicatively decomposed in two ways:

$$
\mathbf{F} = \mathbf{R} \mathbf{U} \quad \text{(Right Polar Decomposition)}
$$
$$
\mathbf{F} = \mathbf{V} \mathbf{R} \quad \text{(Left Polar Decomposition)}
$$

Here, $\mathbf{R}$ is a **proper orthogonal tensor** ($\mathbf{R}^\mathsf{T}\mathbf{R} = \mathbf{I}$ and $\det\mathbf{R}=1$), representing a pure rotation. $\mathbf{U}$ and $\mathbf{V}$ are symmetric, positive-definite tensors known as the **[right stretch tensor](@entry_id:193756)** and **[left stretch tensor](@entry_id:197330)**, respectively.

The right decomposition, $\mathbf{F}=\mathbf{R}\mathbf{U}$, can be interpreted as a two-step process: first, the material element is stretched and sheared by $\mathbf{U}$ in the reference configuration, and then the resulting element is rigidly rotated by $\mathbf{R}$. Conversely, the left decomposition, $\mathbf{F}=\mathbf{V}\mathbf{R}$, can be seen as a rotation by $\mathbf{R}$ followed by a stretch by $\mathbf{V}$ in the spatial configuration. The stretch tensors $\mathbf{U}$ and $\mathbf{V}$ are related by $\mathbf{V} = \mathbf{R}\mathbf{U}\mathbf{R}^\mathsf{T}$, meaning they have the same [principal values](@entry_id:189577) (the [principal stretches](@entry_id:194664)) but different principal directions.

To compute these tensors, we introduce two fundamental [symmetric tensors](@entry_id:148092). The **right Cauchy-Green deformation tensor** is a [material tensor](@entry_id:196294) defined as:

$$
\mathbf{C} = \mathbf{F}^\mathsf{T} \mathbf{F}
$$

And the **left Cauchy-Green (or Finger) deformation tensor** is a [spatial tensor](@entry_id:185799) defined as:

$$
\mathbf{b} = \mathbf{F} \mathbf{F}^\mathsf{T}
$$

Substituting the polar decompositions, we find $\mathbf{C} = (\mathbf{R}\mathbf{U})^\mathsf{T}(\mathbf{R}\mathbf{U}) = \mathbf{U}^\mathsf{T}\mathbf{R}^\mathsf{T}\mathbf{R}\mathbf{U} = \mathbf{U}^2$ and similarly $\mathbf{b} = \mathbf{V}^2$. Since $\mathbf{C}$ and $\mathbf{b}$ are symmetric and [positive definite](@entry_id:149459), their square roots $\mathbf{U}$ and $\mathbf{V}$ are uniquely defined. The standard procedure is to first compute $\mathbf{C}$, then find its unique positive-definite square root to obtain $\mathbf{U}$, and finally solve for the rotation as $\mathbf{R} = \mathbf{F} \mathbf{U}^{-1}$.

As a concrete illustration, consider the simple shear deformation given by $\mathbf{F} = \mathbf{I} + \gamma \mathbf{e}_1 \otimes \mathbf{e}_2$. A detailed calculation shows that the right stretch and rotation tensors are [@problem_id:2886430]:
$$
\mathbf{U} = \frac{1}{\sqrt{\gamma^2+4}} \begin{pmatrix} 2  \gamma  0 \\ \gamma  \gamma^2+2  0 \\ 0  0  \sqrt{\gamma^2+4} \end{pmatrix}, \quad \mathbf{R} = \begin{pmatrix} \frac{2}{\sqrt{\gamma^2+4}}  \frac{\gamma}{\sqrt{\gamma^2+4}}  0 \\ -\frac{\gamma}{\sqrt{\gamma^2+4}}  \frac{2}{\sqrt{\gamma^2+4}}  0 \\ 0  0  1 \end{pmatrix}
$$
This rotation matrix $\mathbf{R}$ corresponds to a rotation about the $\mathbf{e}_3$ axis by an angle $\theta(\gamma) = \arctan(-\gamma/2)$. This example highlights that even a "simple" shear deformation involves both non-trivial stretching and a material rotation.

### Measures of Strain

While $\mathbf{F}$ contains all information, it is not a direct measure of strain because $\mathbf{F}=\mathbf{I}$ for the undeformed state, but $\mathbf{F}=\mathbf{Q} \neq \mathbf{I}$ for a pure [rigid body rotation](@entry_id:167024), which involves no actual material distortion. True [strain measures](@entry_id:755495) must be zero for any [rigid body motion](@entry_id:144691). The Cauchy-Green tensors serve this purpose, as under a rigid rotation ($\mathbf{F}=\mathbf{Q}$), $\mathbf{C} = \mathbf{Q}^\mathsf{T}\mathbf{Q} = \mathbf{I}$ and $\mathbf{b} = \mathbf{Q}\mathbf{Q}^\mathsf{T} = \mathbf{I}$.

The most common [finite strain measures](@entry_id:185716) are derived by quantifying the change in the squared length of a line element. The squared length of a material element $d\mathbf{X}$ is $dS^2 = d\mathbf{X} \cdot d\mathbf{X}$, while its deformed counterpart $d\mathbf{x} = \mathbf{F}d\mathbf{X}$ has squared length $ds^2 = d\mathbf{x} \cdot d\mathbf{x} = (\mathbf{F}d\mathbf{X}) \cdot (\mathbf{F}d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{F}^\mathsf{T}\mathbf{F} d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{C} d\mathbf{X})$.

The change in squared length is therefore $ds^2 - dS^2 = d\mathbf{X} \cdot (\mathbf{C} - \mathbf{I}) d\mathbf{X}$. This motivates the definition of the **Green-Lagrange strain tensor** $\mathbf{E}$ [@problem_id:2639539]:

$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) \quad \text{such that} \quad \frac{1}{2}(ds^2 - dS^2) = d\mathbf{X} \cdot \mathbf{E} \, d\mathbf{X}
$$

$\mathbf{E}$ is a material (or Lagrangian) tensor, as it is defined on the reference configuration and measures strain with respect to material line elements.

Alternatively, we can express the same change in length relative to the current configuration. Using $d\mathbf{X} = \mathbf{F}^{-1} d\mathbf{x}$, we find $dS^2 = d\mathbf{x} \cdot (\mathbf{F}^{-\mathsf{T}}\mathbf{F}^{-1} d\mathbf{x}) = d\mathbf{x} \cdot (\mathbf{b}^{-1} d\mathbf{x})$. The change in squared length is $ds^2 - dS^2 = d\mathbf{x} \cdot (\mathbf{I} - \mathbf{b}^{-1}) d\mathbf{x}$. This motivates the definition of the **Euler-Almansi strain tensor** $\mathbf{e}$ [@problem_id:2639539]:

$$
\mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{b}^{-1}) \quad \text{such that} \quad \frac{1}{2}(ds^2 - dS^2) = d\mathbf{x} \cdot \mathbf{e} \, d\mathbf{x}
$$

$\mathbf{e}$ is a spatial (or Eulerian) tensor, as it is defined on the current configuration and acts on spatial line elements. These two strain tensors represent the same physical strain, but are expressed in different coordinate systems. They are related through the [deformation gradient](@entry_id:163749) via **push-forward** and **pull-back** operations. The operation $\mathbf{E} = \mathbf{F}^\mathsf{T} \mathbf{e} \mathbf{F}$ pulls back the [spatial tensor](@entry_id:185799) $\mathbf{e}$ to the [material configuration](@entry_id:183091), while $\mathbf{e} = \mathbf{F}^{-\mathsf{T}} \mathbf{E} \mathbf{F}^{-1}$ pushes the [material tensor](@entry_id:196294) $\mathbf{E}$ forward to the spatial configuration [@problem_id:2639539] [@problem_id:2639526].

### The Principle of Objectivity

A fundamental principle in continuum mechanics is the **[principle of material frame-indifference](@entry_id:188488)**, or **objectivity**. It states that constitutive laws must be independent of the observer. An observer's frame of reference is related to another by a time-dependent [rigid body motion](@entry_id:144691) ([rotation and translation](@entry_id:175994)). If a motion is described by $\mathbf{x}(\mathbf{X}, t)$, a different observer sees the motion as $\mathbf{x}^*(\mathbf{X}, t) = \mathbf{Q}(t) \mathbf{x}(\mathbf{X}, t) + \mathbf{c}(t)$, where $\mathbf{Q}(t)$ is a proper orthogonal tensor and $\mathbf{c}(t)$ is a translation vector.

Under such a transformation, the [deformation gradient](@entry_id:163749) transforms as $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$. A scalar quantity $\phi(\mathbf{F})$ is said to be **objective** if its value is independent of the observer, meaning $\phi(\mathbf{F}^*) = \phi(\mathbf{F})$. This gives the criterion [@problem_id:2639522]:

$$
\phi(\mathbf{Q}\mathbf{F}) = \phi(\mathbf{F}) \quad \text{for all } \mathbf{Q} \in SO(3)
$$

Quantities that depend directly on $\mathbf{F}$, like $\operatorname{tr}(\mathbf{F})$, are generally not objective. However, the right Cauchy-Green tensor $\mathbf{C}$ transforms as $\mathbf{C}^* = (\mathbf{Q}\mathbf{F})^\mathsf{T}(\mathbf{Q}\mathbf{F}) = \mathbf{F}^\mathsf{T}\mathbf{Q}^\mathsf{T}\mathbf{Q}\mathbf{F} = \mathbf{F}^\mathsf{T}\mathbf{F} = \mathbf{C}$. Because $\mathbf{C}$ is invariant under superposed rotations, any scalar function of $\mathbf{C}$ is automatically objective. This includes the Green-Lagrange strain $\mathbf{E}$ and the **[principal invariants](@entry_id:193522) of C**, defined from its [characteristic polynomial](@entry_id:150909) $\det(\mathbf{C} - \lambda\mathbf{I}) = -\lambda^3 + I_1\lambda^2 - I_2\lambda + I_3 = 0$:
$$
I_1 = \operatorname{tr}(\mathbf{C})
$$
$$
I_2 = \frac{1}{2}[(\operatorname{tr}\mathbf{C})^2 - \operatorname{tr}(\mathbf{C}^2)]
$$
$$
I_3 = \det(\mathbf{C}) = J^2
$$
These invariants are fundamental in the formulation of [strain energy](@entry_id:162699) functions for [hyperelastic materials](@entry_id:190241) [@problem_id:2639576].

Spatial tensors have a different transformation rule. For example, the left Cauchy-Green tensor transforms as $\mathbf{b}^* = \mathbf{Q}\mathbf{b}\mathbf{Q}^\mathsf{T}$, and the Euler-Almansi strain as $\mathbf{e}^* = \mathbf{Q}\mathbf{e}\mathbf{Q}^\mathsf{T}$. Tensors that follow these rules are called objective spatial tensors.

### Rates of Deformation

To describe dynamic processes and rate-dependent material behavior, we need to define rates of kinematic quantities. The velocity of a material point is $\mathbf{v} = \dot{\mathbf{x}}$, where the dot denotes the [material time derivative](@entry_id:190892) (holding $\mathbf{X}$ constant). The spatial gradient of the velocity field is the **[velocity gradient tensor](@entry_id:270928)** $\mathbf{L}$:

$$
\mathbf{L} = \nabla_{\mathbf{x}} \mathbf{v}
$$

Using the chain rule, one can derive the crucial relationship connecting $\mathbf{L}$ to the rate of change of the [deformation gradient](@entry_id:163749) [@problem_id:2639571]:

$$
\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}
$$

The velocity gradient $\mathbf{L}$ can be additively decomposed into its symmetric and skew-symmetric parts:
$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$
where $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^\mathsf{T})$ is the **[rate-of-deformation tensor](@entry_id:184787)** (or stretching tensor), and $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^\mathsf{T})$ is the **[spin tensor](@entry_id:187346)** (or [vorticity tensor](@entry_id:189621)).

The tensor $\mathbf{D}$ describes the instantaneous rate of stretching and shearing of material line elements, with its trace, $\operatorname{tr}(\mathbf{D}) = \nabla_{\mathbf{x}}\cdot\mathbf{v}$, representing the rate of volume change per unit current volume (the dilatation rate). The tensor $\mathbf{W}$ describes the [instantaneous angular velocity](@entry_id:171936) of the material element. For example, in a [simple shear](@entry_id:180497) flow $\mathbf{v} = (\dot{\gamma} x_2, 0, 0)$, both $\mathbf{D}$ and $\mathbf{W}$ are non-zero, indicating that the flow involves both stretching and rotation [@problem_id:2639571].

The objectivity of these rate measures is critical. Under a superposed [rigid body motion](@entry_id:144691), the [rate-of-deformation tensor](@entry_id:184787) $\mathbf{D}$ transforms as an objective [spatial tensor](@entry_id:185799): $\mathbf{D}^* = \mathbf{Q}\mathbf{D}\mathbf{Q}^\mathsf{T}$. However, the [spin tensor](@entry_id:187346) is not objective, transforming as $\mathbf{W}^* = \mathbf{Q}\mathbf{W}\mathbf{Q}^\mathsf{T} + \dot{\mathbf{Q}}\mathbf{Q}^\mathsf{T}$. The additional term $\dot{\mathbf{Q}}\mathbf{Q}^\mathsf{T}$ represents the angular velocity of the observer's frame itself [@problem_id:2639571]. This non-objectivity complicates the use of $\mathbf{W}$ in constitutive laws and motivates the development of [objective time derivatives](@entry_id:189677).

Finally, the [rate-of-deformation tensor](@entry_id:184787) $\mathbf{D}$ is related to the material time rate of the Green-Lagrange [strain tensor](@entry_id:193332), $\dot{\mathbf{E}}$. The relationship is not a simple equality but a [pull-back operation](@entry_id:753859): $\dot{\mathbf{E}} = \mathbf{F}^\mathsf{T}\mathbf{D}\mathbf{F}$. This shows that $\dot{\mathbf{E}}$ is the material representation of the same physical rate of straining that $\mathbf{D}$ represents in the spatial configuration [@problem_id:2639571].

### The Multiplicative Decomposition of Deformation

For materials that undergo permanent, irrecoverable deformation (e.g., [plastic deformation in metals](@entry_id:180560)), it is conceptually useful to introduce a further decomposition of the [deformation gradient](@entry_id:163749). The **[multiplicative decomposition](@entry_id:199514)** is a kinematic postulate that factorizes $\mathbf{F}$ into an elastic part, $\mathbf{F}_e$, and a plastic part, $\mathbf{F}_p$ [@problem_id:2639566]:

$$
\mathbf{F} = \mathbf{F}_e \mathbf{F}_p
$$

This decomposition imagines a conceptual two-step process. First, the material is deformed "plastically" by $\mathbf{F}_p$ into a fictitious, unstressed **intermediate configuration**. Then, this intermediate configuration is deformed "elastically" by $\mathbf{F}_e$ into the final, current configuration. A key insight is that while the total deformation $\mathbf{F}$ must be compatible (i.e., integrable to a global displacement field, $\operatorname{Curl}\mathbf{F}=\mathbf{0}$), the plastic part $\mathbf{F}_p$ need not be. An incompatible $\mathbf{F}_p$ represents a state where the material has been rearranged at the microscopic level in a way that cannot be described by a smooth global mapping, as is the case when dislocations move and create geometric misfits. The elastic deformation $\mathbf{F}_e$ must then accommodate this incompatibility to produce a compatible total deformation.

This kinematic framework is purely conceptual and does not depend on constitutive assumptions. For instance, the common assumption of volume-preserving plasticity, $\det\mathbf{F}_p=1$, is a material-specific constraint, not a general kinematic law. Furthermore, the decomposition $\mathbf{F} = \mathbf{F}_e\mathbf{F}_p$ is not unique; a key part of any [plasticity theory](@entry_id:177023) is to provide evolution equations that specify how $\mathbf{F}_p$ changes, thereby resolving this ambiguity. From this decomposition, important relations follow, such as the expression for the right Cauchy-Green tensor: $\mathbf{C} = \mathbf{F}^\mathsf{T}\mathbf{F} = \mathbf{F}_p^\mathsf{T} (\mathbf{F}_e^\mathsf{T}\mathbf{F}_e) \mathbf{F}_p = \mathbf{F}_p^\mathsf{T} \mathbf{C}_e \mathbf{F}_p$, where $\mathbf{C}_e$ is the elastic right Cauchy-Green tensor [@problem_id:2639566]. This powerful kinematic structure forms the basis for modern theories of [elastoplasticity](@entry_id:193198) at finite strains.