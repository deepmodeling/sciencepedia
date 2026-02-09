## Introduction
The study of how materials change shape and move under external forces is a cornerstone of mechanics. While the motion of rigid bodies can be described simply by translation and rotation, the analysis of deformable bodies—the realm of continuum mechanics—requires a far more sophisticated mathematical language. This is the domain of deformation kinematics: the precise, geometric description of motion, stretching, and distortion, independent of the forces that cause them. A central challenge in this field is choosing the right descriptive tools, as the simplified assumptions valid for small, infinitesimal deformations break down dramatically when a body undergoes large rotations or strains. This article bridges this critical gap, providing a rigorous foundation in both finite and infinitesimal deformation theories.

This article is structured to build your understanding progressively. In "Principles and Mechanisms," we will establish the fundamental mathematical framework, starting from the deformation gradient and developing key measures of strain, stretch, and rotation. We will explore the critical concept of objectivity and the kinematics of deformation rates. Following this theoretical foundation, "Applications and Interdisciplinary Connections" will demonstrate how these principles are applied in diverse fields such as material modeling, computational mechanics, and biomechanics, highlighting the necessity of finite strain theory. Finally, "Hands-On Practices" offers a set of guided problems to solidify your understanding of these essential concepts.

## Principles and Mechanisms

The transition from a rigid body description to that of a deformable continuum requires a rigorous mathematical framework to quantify how a body changes its shape and size. This chapter establishes the fundamental principles and mechanisms of deformation kinematics, providing the language to describe motion, strain, rotation, and their rates of change. We begin with the foundational concept of the deformation gradient and proceed to develop more specialized measures essential for constructing physically meaningful constitutive laws.

### The Deformation Gradient and Displacement

The cornerstone of finite deformation kinematics is the **deformation gradient tensor**, denoted by $\mathbf{F}$. It is a second-order tensor that provides a complete local description of the deformation. Consider a body occupying a reference (or material) configuration $\Omega_0$ at time $t=0$. A material point is identified by its position vector $\mathbf{X}$ in this configuration. The motion of the body is described by a smooth, invertible mapping $\boldsymbol{\varphi}$ which takes each material point $\mathbf{X}$ to its corresponding position $\mathbf{x}$ in the current (or spatial) configuration $\Omega_t$ at time $t$.

$\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$

The deformation gradient $\mathbf{F}$ is defined as the gradient of the motion $\boldsymbol{\varphi}$ with respect to the material coordinates $\mathbf{X}$:

$\mathbf{F}(\mathbf{X}, t) = \nabla_\mathbf{X} \boldsymbol{\varphi}(\mathbf{X}, t)$

In component form, this is $F_{iJ} = \frac{\partial x_i}{\partial X_J}$, where $x_i$ are the components of $\mathbf{x}$ and $X_J$ are the components of $\mathbf{X}$. The tensor $\mathbf{F}$ maps an infinitesimal material line element $d\mathbf{X}$ in the reference configuration to its corresponding spatial line element $d\mathbf{x}$ in the current configuration:

$d\mathbf{x} = \mathbf{F} d\mathbf{X}$

While the motion $\boldsymbol{\varphi}$ describes the absolute position of points, it is often more insightful to focus on the **displacement** of points relative to their reference position. The **Lagrangian displacement field**, $\mathbf{u}$, is defined from the perspective of an observer fixed in the material frame:

$\mathbf{u}(\mathbf{X}, t) = \boldsymbol{\varphi}(\mathbf{X}, t) - \mathbf{X}$

Taking the material gradient of this definition provides a direct and fundamental relationship between the deformation gradient and the **displacement gradient**, $\nabla_\mathbf{X} \mathbf{u}$ [@problem_id:3772224].

$\nabla_\mathbf{X} \mathbf{u} = \nabla_\mathbf{X} (\boldsymbol{\varphi} - \mathbf{X}) = \nabla_\mathbf{X} \boldsymbol{\varphi} - \nabla_\mathbf{X} \mathbf{X} = \mathbf{F} - \mathbf{I}$

Here, $\mathbf{I}$ is the second-order identity tensor. This affine relationship, $\mathbf{F} = \mathbf{I} + \nabla_\mathbf{X} \mathbf{u}$, is exact and reveals that the deformation gradient is a measure of how much the displacement gradient deviates from zero. It is crucial to note that while this relationship is linear, many important quantities derived from $\mathbf{F}$ will be nonlinear functions of the displacement gradient, as we shall see.

A key physical property encoded in the deformation gradient is the local change in volume. This is quantified by the determinant of $\mathbf{F}$, known as the **Jacobian** of the deformation, $J$:

$J = \det \mathbf{F}$

The Jacobian relates an infinitesimal volume element $dV$ in the reference configuration to its deformed counterpart $dv$ in the current configuration via the relation $dv = J dV$ [@problem_id:4167610]. For a physical deformation of matter, interpenetration is impossible. This axiom requires that a left-handed coordinate system in the material cannot become a right-handed one in the spatial frame, which mathematically translates to the constraint that the Jacobian must be strictly positive:

$J > 0$

A deformation is termed **isochoric** or **volume-preserving** if $J=1$. If $0 < J < 1$, the material undergoes local compression, and if $J > 1$, it undergoes local expansion. The conservation of mass for a material element, $\rho_0 dV = \rho dv$, where $\rho_0$ and $\rho$ are the reference and current mass densities, can be expressed using the Jacobian as $\rho_0 = \rho J$, or $\rho = \rho_0 / J$.

### Measures of Strain: Finite vs. Infinitesimal

The deformation gradient $\mathbf{F}$ contains information about both local stretching (strain) and local rigid-body rotation. For formulating constitutive laws (e.g., relating stress to deformation), it is essential to isolate a pure measure of strain that is insensitive to rigid-body motions.

A rigid-body motion applied to the reference configuration can be described by $\mathbf{x} = \mathbf{R}\mathbf{X} + \mathbf{c}$, where $\mathbf{R}$ is a constant, proper orthogonal rotation tensor ($\mathbf{R}^\mathsf{T} \mathbf{R} = \mathbf{I}$, $\det \mathbf{R} = 1$) and $\mathbf{c}$ is a constant translation vector. For such a motion, the deformation gradient is simply $\mathbf{F} = \nabla_\mathbf{X}(\mathbf{R}\mathbf{X}+\mathbf{c}) = \mathbf{R}$. A pure measure of strain should be zero for this deformation.

The **Green-Lagrange strain tensor**, $\mathbf{E}$, is a fundamental finite strain measure that satisfies this requirement. It is defined in the material frame as:

$\mathbf{E} = \frac{1}{2}(\mathbf{F}^\mathsf{T} \mathbf{F} - \mathbf{I})$

Let us verify its behavior under the rigid-body motion $\mathbf{F}=\mathbf{R}$. Substituting this gives $\mathbf{E} = \frac{1}{2}(\mathbf{R}^\mathsf{T} \mathbf{R} - \mathbf{I}) = \frac{1}{2}(\mathbf{I} - \mathbf{I}) = \mathbf{0}$. Thus, $\mathbf{E}$ correctly registers zero strain for any rigid motion, making it an **objective** strain measure [@problem_id:3517509].

By substituting $\mathbf{F} = \mathbf{I} + \nabla_\mathbf{X} \mathbf{u}$ into the definition of $\mathbf{E}$, we can express the Green-Lagrange strain in terms of the displacement gradient:

$\mathbf{E} = \frac{1}{2}((\mathbf{I} + \nabla_\mathbf{X} \mathbf{u})^\mathsf{T} (\mathbf{I} + \nabla_\mathbf{X} \mathbf{u}) - \mathbf{I}) = \frac{1}{2}(\nabla_\mathbf{X} \mathbf{u} + (\nabla_\mathbf{X} \mathbf{u})^\mathsf{T} + (\nabla_\mathbf{X} \mathbf{u})^\mathsf{T} \nabla_\mathbf{X} \mathbf{u})$

This expression explicitly shows the nonlinear, quadratic dependence of $\mathbf{E}$ on the displacement gradient. For many engineering applications, deformations are small. The assumption of **geometrically linear kinematics** is based on the condition that the magnitude of the displacement gradient is much less than unity, i.e., $\|\nabla_\mathbf{X} \mathbf{u}\| \ll 1$. Under this assumption, the quadratic term $(\nabla_\mathbf{X} \mathbf{u})^\mathsf{T} \nabla_\mathbf{X} \mathbf{u}$ can be neglected, leading to the **infinitesimal strain tensor**, also known as the **Cauchy strain tensor**, $\boldsymbol{\varepsilon}$:

$\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla_\mathbf{X} \mathbf{u} + (\nabla_\mathbf{X} \mathbf{u})^\mathsf{T})$

This tensor is simply the symmetric part of the material displacement gradient [@problem_id:3517509]. It serves as the primary strain measure in the theory of linear elasticity. However, its validity is strictly limited. For a finite rotation, $\nabla_\mathbf{X} \mathbf{u} = \mathbf{R} - \mathbf{I}$, and the infinitesimal strain tensor becomes $\boldsymbol{\varepsilon} = \frac{1}{2}(\mathbf{R}+\mathbf{R}^\mathsf{T}) - \mathbf{I}$, which is generally non-zero. This demonstrates that $\boldsymbol{\varepsilon}$ is not objective under finite rotations and will incorrectly predict strains (and thus stresses in an elastic material) for a body that is merely rotating without deforming.

This distinction between the linear theory based on $\boldsymbol{\varepsilon}$ and the nonlinear theory based on $\mathbf{E}$ has profound implications for modeling. For instance, in multiphysics problems involving inelastic effects, the linear theory typically employs an **additive decomposition of strains** (e.g., total strain is the sum of elastic and thermal strains, $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}_e + \boldsymbol{\varepsilon}_{th}$). In contrast, finite deformation theories for phenomena like plasticity are fundamentally based on a **multiplicative decomposition of the deformation gradient** (e.g., $\mathbf{F} = \mathbf{F}_e \mathbf{F}_p$), as additive splits of finite strain tensors like $\mathbf{E}$ are physically and theoretically problematic [@problem_id:3517509].

### Decomposition of Deformation: Stretch and Rotation

The **polar decomposition theorem** provides a powerful and intuitive tool for uniquely separating the local deformation described by $\mathbf{F}$ into a pure stretch and a rigid rotation. For any invertible tensor $\mathbf{F}$ with $\det \mathbf{F} > 0$, there exist two unique decompositions:

1.  **Right Polar Decomposition**: $\mathbf{F} = \mathbf{R}\mathbf{U}$
2.  **Left Polar Decomposition**: $\mathbf{F} = \mathbf{V}\mathbf{R}$

In these decompositions:
- $\mathbf{R}$ is a **proper orthogonal tensor** ($\mathbf{R}^\mathsf{T} \mathbf{R} = \mathbf{I}$, $\det \mathbf{R} = 1$) called the **rotation tensor**.
- $\mathbf{U}$ and $\mathbf{V}$ are symmetric, positive-definite tensors known as the **right stretch tensor** and the **left stretch tensor**, respectively.

The right decomposition, $\mathbf{F}=\mathbf{R}\mathbf{U}$, can be interpreted as a two-step process on a material vector $d\mathbf{X}$: first, a pure stretch is applied by $\mathbf{U}$ in the reference configuration to produce an intermediate vector, which is then rigidly rotated by $\mathbf{R}$ to its final orientation in the spatial configuration [@problem_id:3772243]. Conversely, the left decomposition, $\mathbf{F}=\mathbf{V}\mathbf{R}$, represents a rigid rotation by $\mathbf{R}$ first, followed by a pure stretch applied by $\mathbf{V}$ in the spatial configuration [@problem_id:3772262].

The stretch tensors are directly related to two other fundamental kinematic tensors. The **right Cauchy-Green tensor** $\mathbf{C}$ and the **left Cauchy-Green tensor** (or Finger tensor) $\mathbf{B}$ are defined as:

$\mathbf{C} = \mathbf{F}^\mathsf{T} \mathbf{F}$
$\mathbf{B} = \mathbf{F}\mathbf{F}^\mathsf{T}$

Substituting the polar decompositions reveals their relationship to the stretch tensors:

$\mathbf{C} = (\mathbf{R}\mathbf{U})^\mathsf{T} (\mathbf{R}\mathbf{U}) = \mathbf{U}^\mathsf{T} \mathbf{R}^\mathsf{T} \mathbf{R} \mathbf{U} = \mathbf{U}^\mathsf{T} \mathbf{U} = \mathbf{U}^2$
$\mathbf{B} = (\mathbf{V}\mathbf{R}) (\mathbf{V}\mathbf{R})^\mathsf{T} = \mathbf{V} \mathbf{R} \mathbf{R}^\mathsf{T} \mathbf{V}^\mathsf{T} = \mathbf{V} \mathbf{V}^\mathsf{T} = \mathbf{V}^2$

Thus, $\mathbf{U} = \sqrt{\mathbf{C}}$ and $\mathbf{V} = \sqrt{\mathbf{B}}$ are the unique symmetric positive-definite square roots of their respective Cauchy-Green tensors. Since $\mathbf{C}$ is a tensor defined on the material configuration (it measures squared length changes of material fibers), its square root $\mathbf{U}$ is also a material tensor. Similarly, $\mathbf{B}$ is a spatial tensor, and so is $\mathbf{V}$.

The physical meaning of stretch is captured by the eigenvalues of $\mathbf{U}$ and $\mathbf{V}$. It can be shown that $\mathbf{U}$ and $\mathbf{V}$ are related by a similarity transformation, $\mathbf{V} = \mathbf{R}\mathbf{U}\mathbf{R}^\mathsf{T}$, which implies they share the same eigenvalues. These eigenvalues, denoted $\lambda_1, \lambda_2, \lambda_3$, are called the **principal stretches**. Their corresponding eigenvectors, $\mathbf{e}_i$ for $\mathbf{U}$ and $\mathbf{n}_i=\mathbf{R}\mathbf{e}_i$ for $\mathbf{V}$, represent the **principal directions of stretch** in the reference and current configurations, respectively. These are the specific orthogonal directions that remain orthogonal after deformation and experience only stretching without any shear [@problem_id:3772262].

### The Kinematics of Rates: Deformation Rate and Spin

To describe the evolution of deformation over time, we must consider rate quantities. The velocity of a material point is $\mathbf{v}(\mathbf{x},t)$. The **spatial velocity gradient**, $\mathbf{L}$, is the gradient of the velocity field with respect to the spatial coordinates $\mathbf{x}$:

$\mathbf{L} = \nabla_\mathbf{x} \mathbf{v}$

The material time derivative of the deformation gradient, $\dot{\mathbf{F}}$, is related to $\mathbf{L}$ through the fundamental kinematic identity:

$\dot{\mathbf{F}} = \mathbf{L} \mathbf{F}$

This equation shows how the spatial velocity gradient drives the evolution of the deformation gradient over time. Just as $\mathbf{F}$ contains information about both stretch and rotation, $\mathbf{L}$ describes both the rate of stretching and the rate of rotation. It is therefore natural to decompose $\mathbf{L}$ into its symmetric and skew-symmetric parts:

$\mathbf{L} = \mathbf{D} + \mathbf{W}$

where:
- $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^\mathsf{T})$ is the **rate of deformation tensor** (or stretching tensor).
- $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^\mathsf{T})$ is the **spin tensor**.

The physical meaning of this decomposition can be understood by examining the rate of change of the squared length, $\ell^2 = d\mathbf{x} \cdot d\mathbf{x}$, of an infinitesimal material fiber $d\mathbf{x}$. The material time derivative is given by [@problem_id:3772264]:

$\frac{d}{dt}(\ell^2) = \frac{d}{dt}(d\mathbf{x} \cdot d\mathbf{x}) = 2 \frac{d(d\mathbf{x})}{dt} \cdot d\mathbf{x} = 2(\mathbf{L}d\mathbf{x}) \cdot d\mathbf{x} = d\mathbf{x} \cdot (\mathbf{L}^\mathsf{T}+\mathbf{L})d\mathbf{x} = 2 d\mathbf{x} \cdot \mathbf{D} d\mathbf{x}$

Notice that the skew-symmetric spin tensor $\mathbf{W}$ makes no contribution to the change in length, as $d\mathbf{x} \cdot \mathbf{W} d\mathbf{x} = 0$ for any vector $d\mathbf{x}$. This confirms that $\mathbf{D}$ exclusively governs the rate of stretching and shearing (i.e., deformation), while $\mathbf{W}$ is associated with the rigid-body part of the instantaneous motion (spin). The rate of stretching of a fiber aligned with a unit vector $\mathbf{n}$ is given by the quadratic form $\frac{1}{\ell}\frac{d\ell}{dt} = \mathbf{n} \cdot \mathbf{D} \mathbf{n}$ [@problem_id:3772264].

### Fundamental Kinematic Constraints

In many physical scenarios, the deformation is not arbitrary but must satisfy certain constraints. These constraints translate into specific mathematical conditions on the kinematic quantities we have defined.

#### Incompressibility

A common constraint in fluid dynamics and for modeling materials like rubber is **incompressibility**, which means that the local volume of any material element remains constant throughout the motion. Kinematically, this is expressed as the Jacobian being equal to unity for all time: $J(t) \equiv 1$.

To find the implication of this constraint, we compute the material time derivative of $J$. Using Jacobi's formula for the derivative of a determinant and the relation $\dot{\mathbf{F}}=\mathbf{L}\mathbf{F}$, we arrive at the elegant evolution equation for the Jacobian [@problem_id:3772233]:

$\dot{J} = J \operatorname{tr}(\mathbf{L})$

Here, $\operatorname{tr}(\mathbf{L})$ is the trace of the spatial velocity gradient, which is equal to the divergence of the velocity field, $\nabla \cdot \mathbf{v}$. If a motion is incompressible, then $J=1$ and $\dot{J}=0$, which immediately implies that the velocity field must be divergence-free:

$\operatorname{tr}(\mathbf{L}) = 0$

Conversely, if $\operatorname{tr}(\mathbf{L})=0$ at all times, then $\dot{J}=0$, implying that $J$ is constant. The motion preserves volume, though not necessarily with $J=1$ unless it starts from an undeformed state. This constraint is also equivalent to $\operatorname{tr}(\mathbf{D})=0$, as the trace of the skew-symmetric spin tensor $\mathbf{W}$ is always zero.

This kinematic constraint has important consequences for numerical simulations. The exact solution for the Jacobian over a time step $\Delta t = t_{n+1}-t_n$ is $J_{n+1} = J_n \exp(\int_{t_n}^{t_{n+1}} \operatorname{tr}(\mathbf{L}) d\tau)$. Numerical methods for updating $\mathbf{F}$ must be chosen carefully to respect this. For example, a simple explicit Euler update $\mathbf{F}_{n+1} = (\mathbf{I} + \Delta t \mathbf{L}_n)\mathbf{F}_n$ does not preserve volume exactly even if $\operatorname{tr}(\mathbf{L}_n)=0$, because $\det(\mathbf{I}+\Delta t \mathbf{L}_n) \approx 1 - \frac{1}{2}\Delta t^2 \operatorname{tr}(\mathbf{L}_n^2)$. In contrast, an exponential map update, $\mathbf{F}_{n+1} = \exp(\Delta t \mathbf{L}_n) \mathbf{F}_n$, does preserve volume exactly when $\operatorname{tr}(\mathbf{L}_n)=0$, since $\det(\exp(\mathbf{A})) = \exp(\operatorname{tr}(\mathbf{A}))$ [@problem_id:3772233].

#### Compatibility and Material Defects

Another fundamental constraint is that of **compatibility**. For a given tensor field $\mathbf{F}(\mathbf{X})$ to be a valid deformation gradient corresponding to a continuous, single-valued motion $\boldsymbol{\varphi}(\mathbf{X})$, it must satisfy certain integrability conditions. Since $\mathbf{F} = \nabla_\mathbf{X} \boldsymbol{\varphi}$, or $F_{iJ} = \partial \varphi_i / \partial X_J$, the rows of $\mathbf{F}$ are themselves gradient fields. A necessary condition for a vector field to be the gradient of a scalar potential is that its curl must vanish. Applying this row-wise, we obtain the compatibility condition for $\mathbf{F}$:

$\operatorname{Curl}(\mathbf{F}) = \mathbf{0}$

On a simply connected domain, this condition is also sufficient to guarantee the existence of a single-valued motion $\boldsymbol{\varphi}$ [@problem_id:3772260].

The geometric meaning of this condition is revealed by Stokes' theorem. The line integral of $\mathbf{F}$ around any closed material loop $C$ must be zero. This integral is known as the **Burgers vector** for the loop $C$.

$\mathbf{b} = \oint_C \mathbf{F} d\mathbf{X}$

If $\mathbf{F}$ is compatible, this integral vanishes for any contractible loop, signifying that if you traverse a closed path in the reference configuration, its image in the deformed configuration is also a closed path.

When $\operatorname{Curl}(\mathbf{F}) \neq \mathbf{0}$, the deformation field is incompatible. This is not just a mathematical curiosity; it is the basis for the continuum theory of defects. The presence of crystalline defects, such as dislocations, manifests at the continuum scale as an incompatible deformation gradient. In this case, the Burgers vector $\mathbf{b}$ is non-zero and represents the "closure failure" of the mapped loop, a direct measure of the net dislocation content threading the loop [@problem_id:3772260].

### Objectivity and Changes of Observer

Constitutive laws must provide a physical description of material behavior that is independent of the observer. This principle of **material objectivity** requires that the constitutive equations be invariant under superposed rigid-body motions. To formalize this, we must understand how kinematic quantities transform under a change of observer.

A general change of observer is described by a time-dependent rigid-body motion, where positions in a new (starred) frame are related to positions in the old (unstarred) frame by:

$\mathbf{x}^*(t) = \mathbf{c}(t) + \mathbf{Q}(t)\mathbf{x}(t)$

Here, $\mathbf{c}(t)$ is a time-dependent translation and $\mathbf{Q}(t)$ is a time-dependent proper orthogonal rotation tensor. A spatial tensor field $\mathbf{A}$ is said to be **objective** if its components in the new frame are related to its components in the old frame by the standard tensor transformation rule: $\mathbf{A}^* = \mathbf{Q} \mathbf{A} \mathbf{Q}^\mathsf{T}$.

By applying this transformation to the velocity field and taking the spatial gradient, one can derive the transformation rules for $\mathbf{L}$, $\mathbf{D}$, and $\mathbf{W}$ [@problem_id:3772245]. The result is:

$\mathbf{L}^* = \mathbf{Q} \mathbf{L} \mathbf{Q}^\mathsf{T} + \dot{\mathbf{Q}}\mathbf{Q}^\mathsf{T}$
$\mathbf{D}^* = \mathbf{Q} \mathbf{D} \mathbf{Q}^\mathsf{T}$
$\mathbf{W}^* = \mathbf{Q} \mathbf{W} \mathbf{Q}^\mathsf{T} + \dot{\mathbf{Q}}\mathbf{Q}^\mathsf{T}$

The term $\dot{\mathbf{Q}}\mathbf{Q}^\mathsf{T}$ is a skew-symmetric tensor representing the angular velocity of the moving frame. Its presence in the transformation rules for $\mathbf{L}$ and $\mathbf{W}$ shows that these tensors are **not objective**. Their values depend on the rotational velocity of the observer. In contrast, the transformation for $\mathbf{D}$ is precisely that of an objective tensor.

This result is of paramount importance. The rate of deformation tensor $\mathbf{D}$ is an objective measure of the rate of straining, making it a suitable candidate to appear in objective constitutive laws. A hypothetical law relating stress to the non-objective velocity gradient $\mathbf{L}$, for example, would predict different stresses for the same material deformation depending on how fast the observer is rotating—a physically untenable conclusion.

This issue becomes particularly clear when considering **rate-type constitutive models** (hypoelasticity), which relate a stress *rate* to the rate of deformation $\mathbf{D}$. A crucial question is which stress rate to use. The simple material time derivative of the Cauchy stress, $\dot{\boldsymbol{\sigma}}$, is **not objective**. A pure rigid rotation of a stressed body, for which $\mathbf{D}=\mathbf{0}$, will induce a non-zero $\dot{\boldsymbol{\sigma}}$ simply because the components of the stress tensor are changing in the fixed spatial frame [@problem_id:3772259].

To remedy this, **objective stress rates** are constructed. One of the most common is the **Jaumann rate**, defined as:

$\overset{\triangledown}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \mathbf{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\mathbf{W}$

This rate is constructed precisely to be objective and to vanish for a rigid rotation when $\mathbf{D}=\mathbf{0}$. By using such objective rates in constitutive laws of the form $\overset{\triangledown}{\boldsymbol{\sigma}} = \mathbb{C}:\mathbf{D}$, one ensures that stress is generated only by actual deformation ($\mathbf{D}$) and not by spurious observer-dependent effects or pure spin ($\mathbf{W}$).