## Introduction
Continuum mechanics provides the essential mathematical language for describing how materials deform, flow, and fail. For students and researchers in computational materials science, a deep understanding of its foundational principles is not merely an academic exercise—it is the prerequisite for developing predictive models of advanced materials and complex physical systems. While introductory mechanics often focuses on small deformations, modern challenges in areas like [soft matter](@entry_id:150880), biomechanics, and manufacturing demand a robust framework capable of handling [large strains](@entry_id:751152), intricate material responses, and multi-physics coupling. This article is designed to bridge this gap, providing a comprehensive guide to the core tenets of [continuum mechanics](@entry_id:155125).

The journey begins in the "Principles and Mechanisms" chapter, where we will rigorously establish the mathematical framework, from the kinematics of motion and deformation to the concepts of stress and the fundamental balance laws. We will then explore the crucial principles of [constitutive modeling](@entry_id:183370) that govern material behavior. Next, the "Applications and Interdisciplinary Connections" chapter will showcase the power of this framework, demonstrating how it is used to model [hyperelasticity](@entry_id:168357), plasticity, material failure, and even complex phenomena in geophysics and biology. Finally, the "Hands-On Practices" section offers a series of targeted problems, providing an opportunity to translate theoretical knowledge into practical computational skill. By navigating these chapters, the reader will gain a unified understanding of [continuum mechanics](@entry_id:155125), from abstract theory to its powerful application in modern science and engineering.

## Principles and Mechanisms

This chapter delineates the fundamental principles and mechanisms that form the bedrock of continuum mechanics, providing the essential framework for the computational modeling of materials. We begin with the mathematical description of motion and deformation, proceed to the concepts of stress and the governing laws of mechanics and thermodynamics, and conclude by establishing the core principles of [constitutive modeling](@entry_id:183370) for both elastic and inelastic materials.

### Kinematics: The Description of Motion

The primary goal of kinematics is to provide a precise mathematical description of the motion and deformation of a continuous body, independent of the forces that cause them.

#### Configurations and the Motion Map

We consider a **continuum body**, $\mathcal{B}$, as a set of material points. The configuration of the body at a particular instant is its placement in three-dimensional Euclidean space, $\mathbb{R}^3$. It is standard practice to select one such configuration as a fixed, undeformed state, known as the **reference configuration**, denoted $\mathcal{B}_0$. This configuration is an open set in $\mathbb{R}^3$, and the position of a material point in this configuration is labeled by the vector $\boldsymbol{X}$, often called the material or Lagrangian coordinate.

As the body moves and deforms over time $t$, it occupies a sequence of **current configurations**, $\mathcal{B}_t$. The position of the same material point $\boldsymbol{X}$ in the current configuration is given by the spatial or Eulerian coordinate $\boldsymbol{x}$. The relationship between these two descriptions is provided by the **motion**, a sufficiently smooth function $\boldsymbol{\varphi}$:
$$ \boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t) $$
For a physically realistic motion, the map $\boldsymbol{\varphi}$ must satisfy several key properties. It must be **bijective** (one-to-one and onto its image $\mathcal{B}_t$), ensuring that matter is impenetrable—two distinct material points cannot occupy the same spatial position simultaneously. The map and its inverse, $\boldsymbol{X} = \boldsymbol{\varphi}^{-1}(\boldsymbol{x}, t)$, must be sufficiently smooth to allow for differentiation. Furthermore, the local orientation of the material must be preserved, a condition enforced by requiring the determinant of the mapping's gradient to be strictly positive .

#### The Deformation Gradient

The local deformation at a material point is characterized by the **deformation gradient**, $\mathbf{F}$, defined as the gradient of the motion with respect to the material coordinates:
$$ \mathbf{F}(\boldsymbol{X}, t) = \nabla_{\boldsymbol{X}} \boldsymbol{\varphi}(\boldsymbol{X}, t) \quad \text{or in components, } F_{iJ} = \frac{\partial \varphi_i}{\partial X_J} $$
The deformation gradient is a fundamental two-point tensor that maps vectors from the reference configuration's [tangent space](@entry_id:141028) to the current configuration's [tangent space](@entry_id:141028). Its primary physical interpretation arises from considering an infinitesimal material line element $d\boldsymbol{X}$ in $\mathcal{B}_0$. Under the motion, this element is mapped to a spatial [line element](@entry_id:196833) $d\boldsymbol{x}$ in $\mathcal{B}_t$ according to the linear transformation:
$$ d\boldsymbol{x} = \mathbf{F} \, d\boldsymbol{X} $$
This relationship shows that $\mathbf{F}$ contains all the local information about the stretch and rotation of material fibers .

The determinant of the deformation gradient, $J = \det \mathbf{F}$, has a direct physical meaning. It represents the local ratio of an infinitesimal [volume element](@entry_id:267802) in the current configuration, $dv$, to its corresponding volume element in the reference configuration, $dV$:
$$ dv = J \, dV $$
The physical requirement that matter cannot be compressed to zero volume or be turned inside-out translates to the mathematical constraint $J > 0$. This condition of **[local invertibility](@entry_id:143266)** is essential for all [continuum models](@entry_id:190374)  . A deformation for which $J=1$ is called **isochoric** or volume-preserving.

Finally, for a [deformation gradient](@entry_id:163749) field $\mathbf{F}(\boldsymbol{X})$ to be derivable from a single-valued, continuous motion field $\boldsymbol{\varphi}(\boldsymbol{X})$, it must satisfy the **[compatibility condition](@entry_id:171102)**. On a [simply connected domain](@entry_id:197423), this condition is met if the curl of the tensor field is zero:
$$ \mathrm{Curl} \, \mathbf{F} = \mathbf{0} $$
This ensures that the [mixed partial derivatives](@entry_id:139334) of the motion commute, guaranteeing that integrating $d\boldsymbol{x} = \mathbf{F} d\boldsymbol{X}$ from a point A to a point B yields a result independent of the path taken .

### Measures of Strain

The [deformation gradient](@entry_id:163749) $\mathbf{F}$ contains information about both local rotation and pure deformation (stretch). To isolate the deformation, which is what generates stress in a material, we introduce several [strain measures](@entry_id:755495).

#### Polar Decomposition and Stretch Tensors

The **[polar decomposition theorem](@entry_id:753554)** provides a unique way to factorize the [deformation gradient](@entry_id:163749) into a pure rotation and a pure stretch. For any invertible $\mathbf{F}$, there exist a proper orthogonal tensor $\mathbf{R} \in \mathrm{SO}(3)$ (where $\mathbf{R}^{\mathsf{T}}\mathbf{R}=\mathbf{I}$ and $\det\mathbf{R}=1$) and two [symmetric positive-definite](@entry_id:145886) stretch tensors, $\mathbf{U}$ and $\mathbf{V}$, such that:
$$ \mathbf{F} = \mathbf{R}\mathbf{U} = \mathbf{V}\mathbf{R} $$
Here, $\mathbf{R}$ represents the [rigid body rotation](@entry_id:167024) of the material element. The **[right stretch tensor](@entry_id:193756)** $\mathbf{U}$ acts on vectors in the reference configuration, describing the pure stretch *before* the rotation. The **[left stretch tensor](@entry_id:197330)** $\mathbf{V}$ acts on vectors in the rotated configuration, describing the pure stretch *after* the rotation. The uniqueness of this decomposition is a cornerstone of [finite strain theory](@entry_id:176941). A key insight is that the [rotation tensor](@entry_id:191990) $\mathbf{R}$ is the "closest" rotation to $\mathbf{F}$ in a [least-squares](@entry_id:173916) sense, as it minimizes the Frobenius norm $\|\mathbf{F} - \mathbf{Q}\|_F$ over all rotations $\mathbf{Q} \in \mathrm{SO}(3)$ .

#### Cauchy-Green Deformation Tensors

While the stretch tensors $\mathbf{U}$ and $\mathbf{V}$ have clear physical meaning, they can be computationally cumbersome to work with as they require finding the square root of a tensor. More convenient measures of strain are the **right Cauchy–Green tensor** $\mathbf{C}$ and the **left Cauchy–Green tensor** $\mathbf{B}$, defined as:
$$ \mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F} $$
$$ \mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}} $$
By substituting the polar decomposition, we find direct relationships to the stretch tensors:
$$ \mathbf{C} = (\mathbf{R}\mathbf{U})^{\mathsf{T}}(\mathbf{R}\mathbf{U}) = \mathbf{U}^{\mathsf{T}}\mathbf{R}^{\mathsf{T}}\mathbf{R}\mathbf{U} = \mathbf{U}^2 $$
$$ \mathbf{B} = (\mathbf{V}\mathbf{R})(\mathbf{V}\mathbf{R})^{\mathsf{T}} = \mathbf{V}\mathbf{R}\mathbf{R}^{\mathsf{T}}\mathbf{V}^{\mathsf{T}} = \mathbf{V}^2 $$
Thus, $\mathbf{U}$ and $\mathbf{V}$ are the unique positive-definite square roots of $\mathbf{C}$ and $\mathbf{B}$, respectively .

The tensor $\mathbf{C}$ is a purely [material tensor](@entry_id:196294), as it is defined with respect to the reference configuration. It measures the squared change in length of material fibers. For two material vectors $d\boldsymbol{X}_1$ and $d\boldsymbol{X}_2$, the dot product of their deformed counterparts is $d\boldsymbol{x}_1 \cdot d\boldsymbol{x}_2 = (\mathbf{F}d\boldsymbol{X}_1) \cdot (\mathbf{F}d\boldsymbol{X}_2) = d\boldsymbol{X}_1 \cdot (\mathbf{F}^{\mathsf{T}}\mathbf{F}d\boldsymbol{X}_2) = d\boldsymbol{X}_1 \cdot \mathbf{C}d\boldsymbol{X}_2$. This shows how $\mathbf{C}$ fully characterizes the local change in lengths and angles. Critically, because $\mathbf{C} = \mathbf{U}^2$, it is independent of the rotation $\mathbf{R}$ and thus represents a pure measure of deformation. Tensors $\mathbf{C}$ and $\mathbf{B}$ are related by $\mathbf{B} = \mathbf{R}\mathbf{C}\mathbf{R}^{\mathsf{T}}$ and thus share the same eigenvalues (the squares of the [principal stretches](@entry_id:194664)) but have different eigenvectors, which are rotated by $\mathbf{R}$ .

### Transformation of Fields and Geometric Entities

In [computational mechanics](@entry_id:174464), it is often necessary to transform quantities between the reference and current configurations. These transformations are known as **push-forward** (from reference to current) and **pull-back** (from current to reference) operations.

For a [scalar field](@entry_id:154310), such as temperature, we have a material description $T(\boldsymbol{X})$ and a spatial description $\hat{T}(\boldsymbol{x})$. They are related by composition with the motion: $T(\boldsymbol{X}) = \hat{T}(\boldsymbol{\varphi}(\boldsymbol{X}))$. This defines the material field as the pull-back of the spatial field. Conversely, the spatial field is the push-forward of the material field: $\hat{T}(\boldsymbol{x}) = T(\boldsymbol{\varphi}^{-1}(\boldsymbol{x}))$. The gradients of these fields are related via the chain rule, which in [tensor notation](@entry_id:272140) is $\nabla_{\boldsymbol{X}} T = \mathbf{F}^{\mathsf{T}} \nabla_{\boldsymbol{x}} \hat{T}$.

Vectors and [covectors](@entry_id:157727) ([one-forms](@entry_id:270392), like gradients) transform differently. A material [tangent vector](@entry_id:264836) $\boldsymbol{V}$ is pushed forward to a spatial [tangent vector](@entry_id:264836) $\boldsymbol{v}$ by the rule derived from the mapping of line elements:
$$ \boldsymbol{v} = \mathbf{F} \boldsymbol{V} \quad (\text{Push-forward of a vector}) $$
A spatial [covector](@entry_id:150263) $\boldsymbol{a}$ is pulled back to a material [covector](@entry_id:150263) $\boldsymbol{A}$ by a rule that preserves the [scalar product](@entry_id:175289) with a vector. This results in:
$$ \boldsymbol{A} = \mathbf{F}^{\mathsf{T}} \boldsymbol{a} \quad (\text{Pull-back of a covector}) $$
These distinct transformation rules for vectors (contravariant quantities) and [covectors](@entry_id:157727) (covariant quantities) are crucial for deriving consistent constitutive laws and are a common source of error if not respected .

A key example of these transformations is the mapping of area elements. An oriented [area element](@entry_id:197167) in the reference configuration, described by its normal vector $\mathbf{N}$ and area $dA$, maps to an oriented [area element](@entry_id:197167) in the current configuration ($\mathbf{n}$, $da$). The relationship, known as **Nanson's formula**, is:
$$ \mathbf{n} \, da = J \, \mathbf{F}^{-\mathsf{T}} \mathbf{N} \, dA $$
This formula is fundamental for relating tractions and deriving different [stress measures](@entry_id:198799) .

### Kinetics: Stress and Balance Laws

Kinetics relates the motion of a body to the forces acting upon it. The central concept in this domain is stress.

#### Traction and the Cauchy Stress Tensor

The internal forces within a continuum are described by the **traction vector**, $\mathbf{t}$, defined as the force per unit area acting on an imaginary internal surface. The traction depends on both the location $\boldsymbol{x}$ and the orientation of the surface, defined by its [unit normal vector](@entry_id:178851) $\mathbf{n}$. **Cauchy's Stress Theorem** states that the traction vector is a linear function of the normal vector. This theorem, derived from the [balance of linear momentum](@entry_id:193575) applied to an infinitesimal tetrahedron, is a cornerstone of continuum mechanics . It establishes the existence of the **Cauchy stress tensor**, $\boldsymbol{\sigma}$, a second-order [tensor field](@entry_id:266532) that completely characterizes the state of stress at a point:
$$ \mathbf{t}(\boldsymbol{x}, t, \mathbf{n}) = \boldsymbol{\sigma}(\boldsymbol{x}, t) \mathbf{n} $$
The Cauchy stress is a [spatial tensor](@entry_id:185799), defined per unit area in the current configuration. Balance of angular momentum further shows that, in the absence of body couples, the Cauchy stress tensor must be symmetric ($\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$).

#### Alternative Stress Measures for Finite Strain

While Cauchy stress has a direct physical meaning, it is defined on the deformed configuration, which is often unknown in advance. For computational analyses, especially those formulated in the reference configuration, other [stress measures](@entry_id:198799) are more convenient. These are all related through the deformation gradient $\mathbf{F}$.

1.  **First Piola-Kirchhoff (PK1) Stress, $\mathbf{P}$**: This is a two-point tensor that relates the reference [area element](@entry_id:197167) to the force vector in the current configuration. The nominal traction $\mathbf{T}$ (force per unit reference area) is given by $\mathbf{T} = \mathbf{P}\mathbf{N}$. The PK1 stress is related to the Cauchy stress via:
    $$ \mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-\mathsf{T}} $$
    This tensor is generally not symmetric. It is the natural stress measure that appears in the material form of the momentum balance equation  .

2.  **Second Piola-Kirchhoff (PK2) Stress, $\mathbf{S}$**: This is a fully material stress tensor, obtained by pulling back the force vector itself to the reference configuration. It is related to the PK1 stress by:
    $$ \mathbf{P} = \mathbf{F}\mathbf{S} \quad \implies \quad \mathbf{S} = \mathbf{F}^{-1}\mathbf{P} $$
    The PK2 stress is symmetric if the Cauchy stress is symmetric. Its primary utility is that it is work-conjugate to the rate of change of the right Cauchy-Green tensor, $\frac{1}{2} \dot{\mathbf{C}}$, making it the natural stress measure for [hyperelastic materials](@entry_id:190241) defined in the reference configuration.

3.  **Kirchhoff Stress, $\boldsymbol{\tau}$**: This is a [spatial tensor](@entry_id:185799) defined as a scaled version of the Cauchy stress:
    $$ \boldsymbol{\tau} = J \boldsymbol{\sigma} $$
    The Kirchhoff stress is often used in the theory of plasticity at finite strains.

These [stress measures](@entry_id:198799) are all interconnected. The push-forward/pull-back relationship between the fully material PK2 stress $\mathbf{S}$ and the fully spatial Cauchy stress $\boldsymbol{\sigma}$ is particularly important:
$$ \boldsymbol{\sigma} = \frac{1}{J} \mathbf{F} \mathbf{S} \mathbf{F}^{\mathsf{T}} $$
This demonstrates how the material stress $\mathbf{S}$ is transformed by the deformation $\mathbf{F}$ and pushed forward into the spatial configuration to produce the [true stress](@entry_id:190985) $\boldsymbol{\sigma}$ .

### Governing Equations and Variational Principles

The behavior of a continuum is governed by fundamental balance laws. For computational purposes, these are often expressed in a weak or variational form.

#### Local Balance Laws

The local form of the **[balance of linear momentum](@entry_id:193575)** in the spatial (Eulerian) description is:
$$ \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b} = \rho \dot{\mathbf{v}} $$
where $\rho$ is the current mass density, $\mathbf{b}$ is the [body force](@entry_id:184443) per unit mass, and $\dot{\mathbf{v}}$ is the [material acceleration](@entry_id:270992). In a **quasi-static** analysis, the inertial term $\rho\dot{\mathbf{v}}$ is neglected.

The **[first law of thermodynamics](@entry_id:146485)** ([conservation of energy](@entry_id:140514)) in local form relates the rate of change of specific internal energy, $e$, to the [stress power](@entry_id:182907), heat flux, and heat sources:
$$ \rho \dot{e} = \boldsymbol{\sigma}:\mathbf{D} - \nabla \cdot \mathbf{q} + \rho r $$
Here, $\mathbf{D} = \mathrm{sym}(\nabla\mathbf{v})$ is the [rate of deformation tensor](@entry_id:182598), $\boldsymbol{\sigma}:\mathbf{D}$ is the [stress power](@entry_id:182907) per unit volume, $\mathbf{q}$ is the heat flux vector, and $r$ is the specific heat supply per unit mass .

The **second law of thermodynamics**, expressed as the Clausius-Duhem inequality, places a fundamental constraint on all physical processes. It states that the rate of entropy production must be non-negative:
$$ \rho \dot{\eta} + \nabla \cdot (\mathbf{q}/\theta) - \rho r/\theta \ge 0 $$
where $\eta$ is the specific entropy and $\theta$ is the [absolute temperature](@entry_id:144687). This inequality is the starting point for deriving thermodynamically consistent [constitutive relations](@entry_id:186508) for dissipative materials like plastics .

#### The Principle of Virtual Work

The **[principle of virtual work](@entry_id:138749)** is a powerful alternative statement of equilibrium, forming the basis for the Finite Element Method. It is derived from the balance of [momentum equation](@entry_id:197225). In a quasi-[static analysis](@entry_id:755368) formulated in the reference configuration, the principle states that for any kinematically admissible [virtual displacement](@entry_id:168781) $\delta\mathbf{u}$ (which must vanish on parts of the boundary where displacements are prescribed), the [internal virtual work](@entry_id:172278) must equal the external virtual work:
$$ \int_{\mathcal{B}_0} \mathbf{P} : \delta \mathbf{F} \, \mathrm{d}V = \int_{\mathcal{B}_0} \rho_0 \mathbf{b} \cdot \delta \mathbf{u} \, \mathrm{d}V + \int_{\partial_t \mathcal{B}_0} \bar{\mathbf{T}} \cdot \delta \mathbf{u} \, \mathrm{d}A $$
Here, the left-hand side is the [internal virtual work](@entry_id:172278), with $\mathbf{P}$ being the PK1 stress and $\delta \mathbf{F} = \nabla_0 \delta\mathbf{u}$ being the virtual [deformation gradient](@entry_id:163749). The right-hand side is the external [virtual work](@entry_id:176403) done by body forces $\mathbf{b}$ and prescribed nominal tractions $\bar{\mathbf{T}}$ on the boundary $\partial_t \mathcal{B}_0$ .

### Principles of Constitutive Modeling

Constitutive equations describe the specific response of a material, relating stress to strain. Their formulation is governed by several key principles.

#### Objectivity

The principle of **[material frame indifference](@entry_id:166014)**, or **objectivity**, states that the material response must be independent of the observer. An observer moving with a time-dependent [rigid body motion](@entry_id:144691) sees a different current configuration, $\boldsymbol{x}^* = \mathbf{Q}(t)\boldsymbol{x} + \mathbf{c}(t)$. An objective constitutive law must yield a stress that transforms correctly under this change of observer. For a law of the form $\boldsymbol{\sigma} = \mathbf{f}(\mathbf{F})$, objectivity requires that:
$$ \mathbf{f}(\mathbf{Q}\mathbf{F}) = \mathbf{Q} \mathbf{f}(\mathbf{F}) \mathbf{Q}^{\mathsf{T}} $$
for all proper orthogonal tensors $\mathbf{Q}$. This is a fundamental constraint on the functional form of any valid [constitutive equation](@entry_id:267976). A simple way to satisfy objectivity is to formulate the [constitutive law](@entry_id:167255) using only material tensors, such as expressing the PK2 stress $\mathbf{S}$ as a function of the right Cauchy-Green tensor $\mathbf{C}$, i.e., $\mathbf{S} = \mathbf{g}(\mathbf{C})$ .

#### Material Symmetry: Isotropy and Anisotropy

Objectivity should not be confused with **[material symmetry](@entry_id:173835)**, which is a property of the material itself. Material symmetry describes the invariance of the material's response under rotations of the material in its reference configuration.

A material is **isotropic** if its response is independent of the orientation of the reference frame. For a [hyperelastic material](@entry_id:195319) with [stored energy function](@entry_id:166355) $W$, this means that $W(\mathbf{F}) = W(\mathbf{F}\mathbf{Q}_0)$ for any constant rotation $\mathbf{Q}_0$. This, combined with objectivity, implies that the energy can only be a function of the **[principal invariants](@entry_id:193522)** of the strain tensor. For the right Cauchy-Green tensor $\mathbf{C}$, these are:
$$ I_1 = \mathrm{tr}(\mathbf{C}) $$
$$ I_2 = \frac{1}{2}[(\mathrm{tr}\,\mathbf{C})^2 - \mathrm{tr}(\mathbf{C}^2)] $$
$$ I_3 = \det(\mathbf{C}) = J^2 $$
Thus, for an isotropic [hyperelastic material](@entry_id:195319), $W = \widehat{W}(I_1, I_2, I_3)$. The stress can then be derived by applying the chain rule, for instance, for the PK2 stress :
$$ \mathbf{S} = 2 \frac{\partial \widehat{W}}{\partial \mathbf{C}} = 2\left(\frac{\partial \widehat{W}}{\partial I_1}\mathbf{I} + \frac{\partial \widehat{W}}{\partial I_2}(I_1\mathbf{I} - \mathbf{C}) + \frac{\partial \widehat{W}}{\partial I_3}\,I_3\,\mathbf{C}^{-1}\right) $$
A material that is not isotropic is **anisotropic**. A common case is **[transverse isotropy](@entry_id:756140)**, where the material has a single preferred direction, such as the fiber direction in a composite. This direction is represented by a unit vector $\mathbf{a}_0$ in the reference configuration. The material response is invariant only to rotations about this axis. The [stored energy function](@entry_id:166355) must then depend on additional invariants that capture the interaction of the deformation with this direction. These are typically taken as:
$$ I_4 = \mathbf{a}_0 \cdot \mathbf{C} \mathbf{a}_0 = \|\mathbf{F}\mathbf{a}_0\|^2 $$
$$ I_5 = \mathbf{a}_0 \cdot \mathbf{C}^2 \mathbf{a}_0 $$
The invariant $I_4$ represents the squared stretch of the fiber itself. The energy function for a transversely isotropic material is thus written as $W = \widehat{W}(I_1, I_2, I_3, I_4, I_5)$ .

### Application: Finite Strain Elastoplasticity

The principles discussed thus far culminate in advanced [constitutive models](@entry_id:174726), such as those for [finite strain plasticity](@entry_id:175182). A standard approach uses the **[multiplicative decomposition](@entry_id:199514)** of the deformation gradient into elastic and plastic parts:
$$ \mathbf{F} = \mathbf{F}_e \mathbf{F}_p $$
Here, $\mathbf{F}_p$ represents an imagined deformation that creates plastic distortions, mapping the reference configuration to a stress-free **intermediate configuration**. $\mathbf{F}_e$ is the subsequent elastic deformation that introduces stress. For [metal plasticity](@entry_id:176585), [plastic flow](@entry_id:201346) is assumed to be isochoric, leading to the constraint $\det(\mathbf{F}_p) = 1$.

The thermodynamic framework requires identifying the stress-like quantity that drives plastic flow. This is found to be the **Mandel stress**, a [material tensor](@entry_id:196294) in the intermediate configuration defined as $\mathbf{M} = \mathbf{C}_e \mathbf{S}_e$, where $\mathbf{C}_e=\mathbf{F}_e^{\mathsf{T}}\mathbf{F}_e$ and $\mathbf{S}_e$ is the PK2 stress in the elastic configuration. The plastic flow is then governed by a [yield criterion](@entry_id:193897) and a [flow rule](@entry_id:177163). For classic $J_2$ (von Mises) plasticity, this framework becomes :
-   **Yield Function**: $f(\mathbf{M}, \kappa) = \sqrt{\frac{3}{2}}\|\mathrm{dev}\,\mathbf{M}\| - \sigma_y(\kappa) \le 0$, where $\sigma_y$ is the yield strength and $\kappa$ is a hardening variable.
-   **Associative Flow Rule**: The rate of plastic deformation in the intermediate configuration, $\mathbf{D}_p = \mathrm{sym}(\dot{\mathbf{F}}_p\mathbf{F}_p^{-1})$, is given by $\mathbf{D}_p = \lambda \frac{\partial f}{\partial \mathbf{M}}$, where $\lambda \ge 0$ is the [plastic multiplier](@entry_id:753519).
-   **Kuhn-Tucker Conditions**: The loading/unloading conditions are specified by $\lambda \ge 0$, $f \le 0$, and $\lambda f = 0$.

This advanced model elegantly combines the [kinematic decomposition](@entry_id:751020), [thermodynamic principles](@entry_id:142232), and constitutive assumptions of yield and flow within a single, objective, and consistent framework, demonstrating the power of the foundational principles of [continuum mechanics](@entry_id:155125).