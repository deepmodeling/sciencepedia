## Introduction
In the study of [continuum mechanics](@entry_id:155125), understanding how bodies move and deform is paramount. While the classical theory of infinitesimal strains provides a powerful tool for many engineering applications, its validity is restricted to problems involving very small displacements and rotations. When a material undergoes significant changes in shape or orientation—as seen in [metal forming](@entry_id:188560), [soft tissue mechanics](@entry_id:199866), or the behavior of elastomers—a more general and rigorous framework is required. This is the domain of [finite deformation kinematics](@entry_id:195826).

This article addresses the fundamental challenge of describing and quantifying deformation without the simplifying assumptions of linear theory. It builds a complete kinematic language capable of handling arbitrarily [large strains](@entry_id:751152) and rotations, providing the necessary foundation for the advanced study of [solid mechanics](@entry_id:164042).

Over the course of three chapters, you will embark on a systematic exploration of this topic. The first chapter, **"Principles and Mechanisms,"** lays the mathematical groundwork, introducing the [deformation gradient tensor](@entry_id:150370) and its fundamental polar decomposition into pure stretch and rotation. The second chapter, **"Applications and Interdisciplinary Connections,"** demonstrates the power of this framework by showing how it is applied to construct physically meaningful [constitutive models](@entry_id:174726), develop robust computational methods in plasticity, and analyze complex phenomena in materials science. Finally, **"Hands-On Practices"** will solidify your understanding through targeted problems that bridge theory and computation. We begin by delving into the core principles that govern the geometry of finite motion.

## Principles and Mechanisms

In this chapter, we delve into the core principles and mathematical machinery that describe the motion and deformation of a continuous body. Moving beyond the infinitesimal-strain framework, we will develop a rigorous kinematic description capable of handling arbitrarily large displacements, rotations, and strains. Our central object of study will be the **[deformation gradient](@entry_id:163749)**, a tensor that provides a complete local description of the deformation. We will see how this single entity can be decomposed into measures of pure stretch and pure rotation, leading to a family of strain tensors suitable for formulating the physical laws that govern material behavior under [finite deformation](@entry_id:172086).

### The Deformation Gradient

The motion of a continuous body is described by a mapping, $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$, that gives the current spatial position $\mathbf{x}$ of a material point that was located at position $\mathbf{X}$ in a fixed-in-time **reference configuration**. The fundamental measure of the local deformation at a material point $\mathbf{X}$ is the **[deformation gradient tensor](@entry_id:150370)**, denoted by $\mathbf{F}$. It is defined as the gradient of the motion with respect to the material coordinates $\mathbf{X}$:

$$
\mathbf{F}(\mathbf{X}, t) = \nabla_{\mathbf{X}}\boldsymbol{\chi}(\mathbf{X}, t) \quad \text{or in component form,} \quad F_{ij} = \frac{\partial x_i}{\partial X_j}
$$

The primary physical meaning of $\mathbf{F}$ is that it provides a [linear transformation](@entry_id:143080) that maps an infinitesimal material vector $\mathrm{d}\mathbf{X}$ in the reference configuration to its corresponding infinitesimal spatial vector $\mathrm{d}\mathbf{x}$ in the current configuration [@problem_id:2922110]. This relationship, derived from a first-order Taylor expansion of the motion, is given by:

$$
\mathrm{d}\mathbf{x} = \mathbf{F} \mathrm{d}\mathbf{X}
$$

When the deformation is the same at every point, it is called a **homogeneous deformation**. In this case, the motion takes the affine form $\mathbf{x} = \mathbf{A}\mathbf{X} + \mathbf{b}$, where $\mathbf{A}$ is a constant tensor and $\mathbf{b}$ is a constant vector representing a rigid translation. For such a motion, the deformation gradient is constant throughout the body and is simply $\mathbf{F} = \mathbf{A}$ [@problem_id:2886421].

For a motion to be physically admissible, it must not allow two distinct material points to occupy the same spatial location, nor can it cause a [finite volume](@entry_id:749401) of material to collapse to zero or negative volume. This is ensured by requiring the mapping $\boldsymbol{\chi}$ to be locally invertible. Mathematically, this translates to the condition that the determinant of the [deformation gradient](@entry_id:163749), known as the **Jacobian** of the deformation ($J = \det\mathbf{F}$), must be strictly positive:

$$
J = \det\mathbf{F} > 0
$$

A Jacobian $J \lt 0$ would imply a local "inversion" of the material, like turning a glove inside out, which is considered physically impossible for a continuous motion starting from an undeformed state where $\mathbf{F}=\mathbf{I}$ and $J=1$ [@problem_id:2886418] [@problem_id:2886421].

The Jacobian also quantifies the local change in volume. An infinitesimal volume element $\mathrm{d}V$ in the reference configuration is mapped to a [volume element](@entry_id:267802) $\mathrm{d}v$ in the current configuration according to the relation $\mathrm{d}v = J \mathrm{d}V$ [@problem_id:2922110]. A deformation is termed **isochoric**, or volume-preserving, if $J=1$ everywhere.

The transformation of oriented area elements is also governed by $\mathbf{F}$. An [area element](@entry_id:197167) with magnitude $\mathrm{d}A$ and unit normal $\mathbf{N}$ in the reference configuration is mapped to an area element with magnitude $\mathrm{d}a$ and unit normal $\mathbf{n}$ in the current configuration. The relationship, known as **Nanson's formula**, is given by [@problem_id:2922110]:

$$
\mathbf{n}\,\mathrm{d}a = J \mathbf{F}^{-T} \mathbf{N}\,\mathrm{d}A
$$

where $\mathbf{F}^{-T}$ is the inverse transpose of $\mathbf{F}$. This formula is essential for converting integrals over surfaces in the current configuration to integrals over surfaces in the reference configuration, a common operation in the formulation of balance laws.

### Polar Decomposition: Separating Stretch from Rotation

The [deformation gradient](@entry_id:163749) $\mathbf{F}$ contains combined information about the local stretching and rotation of the material. The **[polar decomposition theorem](@entry_id:753554)** provides a powerful and intuitive way to uniquely separate these two effects. The theorem states that any invertible tensor $\mathbf{F}$ can be multiplicatively decomposed in two ways:

1.  **Right Polar Decomposition**: $\mathbf{F} = \mathbf{R}\mathbf{U}$
2.  **Left Polar Decomposition**: $\mathbf{F} = \mathbf{V}\mathbf{R}$

Here, $\mathbf{R}$ is a **proper orthogonal tensor** (a rotation), meaning it satisfies $\mathbf{R}^T\mathbf{R} = \mathbf{I}$ and $\det\mathbf{R}=+1$. The tensors $\mathbf{U}$ and $\mathbf{V}$ are symmetric ($\mathbf{U}^T=\mathbf{U}$, $\mathbf{V}^T=\mathbf{V}$) and positive-definite (all their eigenvalues are positive). They are known as the **[right stretch tensor](@entry_id:193756)** and **[left stretch tensor](@entry_id:197330)**, respectively.

The physical interpretation of the right polar decomposition is that the total deformation can be seen as a two-step process: first, a pure stretch described by $\mathbf{U}$ is applied in the reference configuration, followed by a rigid rotation described by $\mathbf{R}$ to bring the stretched element to its final orientation in the current configuration [@problem_id:2922110]. Similarly, the left decomposition can be interpreted as a rotation $\mathbf{R}$ followed by a stretch $\mathbf{V}$ in the spatial configuration.

The requirement that $\mathbf{R}$ must be a [proper rotation](@entry_id:141831) (an element of the [special orthogonal group](@entry_id:146418), $\mathrm{SO}(3)$) is a direct consequence of the physical [admissibility condition](@entry_id:200767) $J>0$. From the decomposition $\mathbf{F}=\mathbf{R}\mathbf{U}$, we have $\det\mathbf{F} = (\det\mathbf{R})(\det\mathbf{U})$. Since $\mathbf{U}$ is positive-definite, its determinant (the product of its positive eigenvalues) must be positive, $\det\mathbf{U}>0$. Therefore, for $\det\mathbf{F}$ to be positive, $\det\mathbf{R}$ must also be positive. As $\mathbf{R}$ is orthogonal, its determinant can only be $+1$ or $-1$. The [admissibility condition](@entry_id:200767) thus forces $\det\mathbf{R}=+1$, excluding improper rotations like reflections [@problem_id:2886418].

A simple deformation involving only a rigid rotation of the body, $\mathbf{x} = \mathbf{R}_0\mathbf{X}$ where $\mathbf{R}_0$ is a constant [rotation tensor](@entry_id:191990), results in a [deformation gradient](@entry_id:163749) $\mathbf{F}=\mathbf{R}_0$. In this case, there is no stretch, so $\mathbf{U}=\mathbf{I}$, and the rotation part of the decomposition is simply $\mathbf{R}_0$ itself [@problem_id:2922110].

Conversely, consider a pure uniaxial stretch along the $\mathbf{e}_1$ axis, given by the deformation gradient $\mathbf{F} = \operatorname{diag}(\lambda, 1, 1)$, with $\lambda > 0$ [@problem_id:2886394]. In this case, the tensor $\mathbf{F}$ is already symmetric and positive-definite. By the uniqueness of the polar decomposition, we can identify the stretch and rotation tensors. The [stretch tensor](@entry_id:193200) $\mathbf{U}$ must be $\mathbf{F}$ itself, and consequently, the [rotation tensor](@entry_id:191990) $\mathbf{R}$ must be the identity tensor $\mathbf{I}$. This confirms the intuitive notion that a pure stretch along a coordinate axis involves no rotation.

### Measures of Finite Strain

While $\mathbf{F}$ describes the entire deformation, for many purposes, particularly in [constitutive modeling](@entry_id:183370), we need measures that isolate the material's stretching from its rigid rotation. The polar decomposition provides the foundation for defining such measures.

#### The Stretch Tensors and Principal Deformations

The [right stretch tensor](@entry_id:193756) $\mathbf{U}$ and [left stretch tensor](@entry_id:197330) $\mathbf{V}$ are the most fundamental measures of pure strain. They are formally defined from $\mathbf{F}$ as:

$$
\mathbf{U} = \sqrt{\mathbf{F}^T\mathbf{F}} \quad \text{and} \quad \mathbf{V} = \sqrt{\mathbf{F}\mathbf{F}^T}
$$

where the square root denotes the unique positive-definite symmetric root. The tensors $\mathbf{U}$ and $\mathbf{V}$ are related by the rotation $\mathbf{R}$ via a [similarity transformation](@entry_id:152935): $\mathbf{V} = \mathbf{R}\mathbf{U}\mathbf{R}^T$.

As [symmetric tensors](@entry_id:148092), $\mathbf{U}$ and $\mathbf{V}$ possess a set of real eigenvalues and an [orthonormal basis of eigenvectors](@entry_id:180262). The eigenvalues, denoted $\lambda_i$, are called the **[principal stretches](@entry_id:194664)**. The corresponding orthonormal eigenvectors of $\mathbf{U}$, denoted $\mathbf{E}_i$, are called the **Lagrangian principal directions** of stretch, which reside in the reference configuration. The eigenvectors of $\mathbf{V}$, denoted $\mathbf{e}_i$, are the **Eulerian principal directions**, which reside in the current configuration [@problem_id:2918196].

A crucial insight is that $\mathbf{U}$ and $\mathbf{V}$ share the same set of eigenvalues—the [principal stretches](@entry_id:194664) $\lambda_i$. Their [principal directions](@entry_id:276187), however, are generally different. They are related by the [rotation tensor](@entry_id:191990) from the [polar decomposition](@entry_id:149541) [@problem_id:2918196]:

$$
\mathbf{e}_i = \mathbf{R}\mathbf{E}_i
$$

This elegantly shows that the [principal axes of strain](@entry_id:188315) in the material are rotated by the deformation. The action of the full deformation gradient on a principal direction in the reference frame is to stretch it by the corresponding principal stretch and rotate it into the new principal direction in the current frame [@problem_id:2918196]:

$$
\mathbf{F}\mathbf{E}_i = (\mathbf{R}\mathbf{U})\mathbf{E}_i = \mathbf{R}(\lambda_i \mathbf{E}_i) = \lambda_i(\mathbf{R}\mathbf{E}_i) = \lambda_i\mathbf{e}_i
$$

For the uniaxial stretch deformation $\mathbf{F}=\operatorname{diag}(\lambda,1,1)$, the [right stretch tensor](@entry_id:193756) is $\mathbf{U}=\mathbf{F}$. Its eigenvalues are the [principal stretches](@entry_id:194664) $\lambda_1=\lambda$, $\lambda_2=1$, and $\lambda_3=1$. The corresponding [principal directions](@entry_id:276187) are the basis vectors $\mathbf{E}_1=\mathbf{e}_1$, $\mathbf{E}_2=\mathbf{e}_2$, and $\mathbf{E}_3=\mathbf{e}_3$ [@problem_id:2886394].

#### The Cauchy-Green Deformation Tensors

Two other widely used tensors are the **right Cauchy-Green tensor** $\mathbf{C}$ and the **left Cauchy-Green (or Finger) tensor** $\mathbf{B}$. They are defined as:

$$
\mathbf{C} = \mathbf{F}^T\mathbf{F} = \mathbf{U}^2 \quad \text{and} \quad \mathbf{B} = \mathbf{F}\mathbf{F}^T = \mathbf{V}^2
$$

Since $\mathbf{U}$ and $\mathbf{V}$ are measures of pure stretch, so too are $\mathbf{C}$ and $\mathbf{B}$. They are insensitive to the rotational part $\mathbf{R}$ of the deformation. The eigenvalues of both $\mathbf{C}$ and $\mathbf{B}$ are the squares of the [principal stretches](@entry_id:194664), $\lambda_i^2$ [@problem_id:2918196].

The **[principal invariants](@entry_id:193522)** of $\mathbf{C}$ and $\mathbf{B}$ are often used in [constitutive models](@entry_id:174726) for [isotropic materials](@entry_id:170678), as they provide a complete description of the strain magnitude, independent of the orientation of the principal axes. The three invariants are:
$I_1 = \mathrm{tr}(\mathbf{C})$, $I_2 = \frac{1}{2}[(\mathrm{tr}(\mathbf{C}))^2 - \mathrm{tr}(\mathbf{C}^2)]$, and $I_3 = \det(\mathbf{C})$.

To illustrate what these invariants measure, consider a homogeneous simple shear deformation given by $\mathbf{F} = \mathbf{I} + \gamma \mathbf{e}_1 \otimes \mathbf{e}_2$ [@problem_id:2886401]. The right Cauchy-Green tensor is $\mathbf{C} = \begin{pmatrix} 1 & \gamma & 0 \\ \gamma & 1+\gamma^2 & 0 \\ 0 & 0 & 1 \end{pmatrix}$. A direct calculation shows that the invariants of $\mathbf{C}$ (and $\mathbf{B}$) are $I_1 = 3+\gamma^2$, $I_2 = 3+\gamma^2$, and $I_3 = 1$. The fact that $I_1$ and $I_2$ depend on $\gamma^2$ shows that they capture the magnitude of the shear but are insensitive to its direction (the sign of $\gamma$). The invariant $I_3 = (\det\mathbf{F})^2 = J^2 = 1$ confirms that simple shear is an [isochoric deformation](@entry_id:196451).

#### Lagrangian and Eulerian Strain Tensors

From the Cauchy-Green tensors, we can define strain tensors that are zero in the undeformed state. The two most common are the **Green-Lagrange [strain tensor](@entry_id:193332)** $\mathbf{E}$ and the **Almansi strain tensor** $\mathbf{e}$.

$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I})
$$

$$
\mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{B}^{-1}) = \frac{1}{2}(\mathbf{I} - (\mathbf{F}\mathbf{F}^T)^{-1})
$$

It is critical to recognize that $\mathbf{E}$ is a **Lagrangian** quantity, measuring strain with respect to the geometry of the reference configuration. In contrast, $\mathbf{e}$ is an **Eulerian** quantity, measuring strain with respect to the geometry of the current, deformed configuration.

Consider again the uniaxial stretch $\mathbf{F}=\operatorname{diag}(\lambda,1,1)$ [@problem_id:2886403]. A straightforward calculation yields the strain tensors:
$$
\mathbf{E} = \frac{1}{2} \begin{pmatrix} \lambda^2 - 1 & 0 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix} \quad \text{and} \quad \mathbf{e} = \frac{1}{2} \begin{pmatrix} 1 - \lambda^{-2} & 0 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix}
$$
The [axial strain](@entry_id:160811) components are $E_{11} = \frac{1}{2}(\lambda^2 - 1)$ and $e_{11} = \frac{1}{2}(1 - \lambda^{-2})$. These expressions are numerically different for any $\lambda \neq 1$, yet they describe the exact same physical state of stretch. The difference arises purely from the choice of reference frame for measurement: $\mathbf{E}$ quantifies the change in squared length relative to the initial length, whereas $\mathbf{e}$ quantifies it relative to the final length.

### The Kinematics of Rates

To study the time-dependent behavior of materials, we must analyze the rates of change of kinematic quantities. The **[spatial velocity gradient](@entry_id:187198) tensor** $\mathbf{L}$ is central to this analysis. It is defined as the gradient of the velocity field $\mathbf{v}$ with respect to the current spatial coordinates $\mathbf{x}$:

$$
\mathbf{L} = \nabla_{\mathbf{x}}\mathbf{v}
$$

The velocity gradient can be related to the rate of change of the [deformation gradient](@entry_id:163749) by the fundamental expression $\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}$.

A key result in kinematics is that any tensor can be uniquely decomposed into its symmetric and skew-symmetric parts. Applying this to $\mathbf{L}$, we have an additive decomposition [@problem_id:2886428]:

$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$

where $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T)$ is the symmetric **[rate of deformation tensor](@entry_id:182598)** (or stretching tensor), and $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^T)$ is the skew-symmetric **[spin tensor](@entry_id:187346)**.

These two tensors have distinct physical interpretations. The rate of deformation $\mathbf{D}$ exclusively governs the rate at which material line elements stretch. For an infinitesimal material fiber with current length $\mathrm{d}\ell$ and orientation $\mathbf{n}$, its rate of change of length is given by $\frac{\mathrm{d}}{\mathrm{d}t}(\mathrm{d}\ell) = (\mathbf{n} \cdot \mathbf{D} \mathbf{n})\mathrm{d}\ell$ [@problem_id:2886428]. The [spin tensor](@entry_id:187346) $\mathbf{W}$, on the other hand, describes the average angular velocity, or spin, of the material at a point.

In the special case of a pure [rigid body motion](@entry_id:144691), there is no stretching of material elements, so the [rate of deformation tensor](@entry_id:182598) is zero, $\mathbf{D}=\mathbf{0}$. The [velocity gradient](@entry_id:261686) is purely skew-symmetric, $\mathbf{L}=\mathbf{W}$, and the [spin tensor](@entry_id:187346) $\mathbf{W}$ coincides with the [angular velocity](@entry_id:192539) tensor of the rigid motion [@problem_id:2886428] [@problem_id:2886400]. The rates $\mathbf{D}$ and $\mathbf{W}$ can also be expressed in terms of the rates of the factors from the [polar decomposition](@entry_id:149541), revealing a more complex relationship than a simple one-to-one correspondence, for instance $\mathbf{W}$ is not in general equal to $\dot{\mathbf{R}}\mathbf{R}^T$ [@problem_id:2886428].

### Objectivity and Compatibility

The kinematic framework we have developed has profound implications for the formulation of physical laws and for understanding the geometric constraints on possible deformations.

#### Frame Indifference and Objectivity

A fundamental principle of physics, known as the **[principle of material frame indifference](@entry_id:194378)** or **objectivity**, states that [constitutive equations](@entry_id:138559) must be independent of the observer. An observer is modeled as a reference frame that can translate and rotate rigidly relative to the laboratory frame. A superposed rigid motion is given by $\mathbf{x}^* = \mathbf{Q}(t)\mathbf{x} + \mathbf{c}(t)$, where $\mathbf{Q}(t)$ is a time-dependent rotation.

Kinematic quantities are classified based on how they transform under such a change of observer. For example, the deformation gradient transforms as $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$, which depends on the observer's rotation $\mathbf{Q}$. It is therefore **not objective**. In contrast, the right Cauchy-Green tensor $\mathbf{C}$ is objective, as $\mathbf{C}^* = (\mathbf{F}^*)^T\mathbf{F}^* = (\mathbf{Q}\mathbf{F})^T(\mathbf{Q}\mathbf{F}) = \mathbf{F}^T\mathbf{Q}^T\mathbf{Q}\mathbf{F} = \mathbf{F}^T\mathbf{F} = \mathbf{C}$.

For rate quantities, the [rate of deformation tensor](@entry_id:182598) $\mathbf{D}$ is objective, transforming as a proper tensor: $\mathbf{D}^* = \mathbf{Q}\mathbf{D}\mathbf{Q}^T$. The [spin tensor](@entry_id:187346) $\mathbf{W}$, however, is not objective; its transformation law includes a term related to the observer's own spin: $\mathbf{W}^* = \mathbf{Q}\mathbf{W}\mathbf{Q}^T + \dot{\mathbf{Q}}\mathbf{Q}^T$ [@problem_id:2886428].

This non-objectivity has critical consequences for [constitutive modeling](@entry_id:183370). A rate-type [constitutive model](@entry_id:747751) relating stress rate to the rate of deformation must use an [objective stress rate](@entry_id:168809). A model naively formulated with the simple [material time derivative](@entry_id:190892) of the Cauchy stress, $\dot{\boldsymbol{\sigma}}$, such as $\dot{\boldsymbol{\sigma}} = \lambda \operatorname{tr}(\mathbf{D})\mathbf{I} + 2\mu\mathbf{D}$, violates [frame indifference](@entry_id:749567) [@problem_id:2886400]. If such a model is applied to a body undergoing a pure rigid rotation (for which $\mathbf{D}=\mathbf{0}$), it incorrectly predicts that the stress remains constant ($\dot{\boldsymbol{\sigma}}=\mathbf{0}$). The physically correct stress, however, must rotate with the body. This failure to account for the rotation of the stress tensor itself leads to the prediction of spurious stresses and demonstrates the necessity of using [objective rates](@entry_id:198692) (such as the Jaumann or Truesdell rate) in Eulerian constitutive formulations.

#### Compatibility of the Deformation Gradient Field

Finally, we must consider whether any arbitrary tensor field $\mathbf{F}(\mathbf{X})$ can represent a physically possible deformation. For a field $\mathbf{F}$ to be derivable from a single-valued, continuous motion field $\boldsymbol{\chi}(\mathbf{X})$, i.e., $\mathbf{F} = \nabla\boldsymbol{\chi}$, it must satisfy certain [integrability conditions](@entry_id:158502). These are known as **[compatibility conditions](@entry_id:201103)**. For a simply connected body, the necessary and sufficient condition is that the curl of the deformation gradient field must vanish:

$$
\operatorname{Curl}\mathbf{F} = \mathbf{0}
$$

This condition arises from the mathematical requirement that [mixed partial derivatives](@entry_id:139334) of the motion field must commute, $\partial^2 \boldsymbol{\chi} / \partial X_k \partial X_j = \partial^2 \boldsymbol{\chi} / \partial X_j \partial X_k$. A [tensor field](@entry_id:266532) $\mathbf{F}$ that violates this condition is called **incompatible**.

Consider a field defined as a spatially varying rotation, $\mathbf{F}(\mathbf{X}) = \mathbf{R}(\gamma X_3)$, where $\mathbf{R}$ is a rotation about the $X_3$-axis by an angle proportional to $X_3$ [@problem_id:2886397]. This field represents a state of pure local rotation ($\mathbf{U}=\mathbf{I}$) and is volume-preserving ($\det\mathbf{F}=1$). However, a direct calculation shows that $\operatorname{Curl}\mathbf{F} \neq \mathbf{0}$ if $\gamma \neq 0$. This field is therefore incompatible and cannot be generated by a smooth, [continuous deformation](@entry_id:151691) of a body. Physically, such incompatible fields are used to model [material defects](@entry_id:159283), such as a [continuous distribution](@entry_id:261698) of dislocations, where the material no longer fits together perfectly.