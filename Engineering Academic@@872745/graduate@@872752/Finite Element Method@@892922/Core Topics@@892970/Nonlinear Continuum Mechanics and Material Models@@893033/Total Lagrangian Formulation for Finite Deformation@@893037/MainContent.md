## Introduction
The analysis of systems undergoing [large deformations](@entry_id:167243) and rotations is a fundamental challenge in [computational solid mechanics](@entry_id:169583), where the assumptions of [linear elasticity](@entry_id:166983) break down. The Total Lagrangian (TL) formulation provides a powerful and robust framework to address this challenge. Its core principle is to describe the entire motion and the resulting stresses and strains with respect to the body's initial, undeformed configuration, creating a fixed reference frame for analysis. This approach resolves the complexities of a moving and deforming domain inherent in large-strain problems, but introduces new kinematic and kinetic measures necessary to accurately capture the physics. This article serves as a comprehensive guide to understanding and applying the Total Lagrangian formulation.

Across three distinct sections, this article will guide you from fundamental theory to practical application. The first chapter, **Principles and Mechanisms**, dissects the kinematic and kinetic foundations of the TL method, defining critical concepts like the deformation gradient, Green-Lagrange strain, and the various Piola-Kirchhoff stress tensors, and culminates in the [finite element discretization](@entry_id:193156). The second chapter, **Applications and Interdisciplinary Connections**, explores how this framework is used to model advanced materials like composites and elastomers, tackle dynamic and stability problems, and connect to other fields such as [electromechanics](@entry_id:276577). Finally, the **Hands-On Practices** section provides targeted exercises to solidify your understanding of the core computational concepts, bridging the gap between theory and implementation.

## Principles and Mechanisms

The Total Lagrangian (TL) formulation is a cornerstone of [computational solid mechanics](@entry_id:169583) for analyzing problems involving large deformations and rotations. Its central premise is that all kinematic and kinetic quantities, as well as the governing [equations of equilibrium](@entry_id:193797), are systematically referred back to the initial, undeformed configuration of the body. This approach provides a fixed, time-independent domain for [spatial discretization](@entry_id:172158) and integration, which is a significant advantage in numerical implementations. In this chapter, we will dissect the fundamental principles and mechanisms that constitute this powerful framework, from the kinematic description of motion to the nuances of its finite element implementation.

### Kinematics of Finite Deformation: A Lagrangian Perspective

To describe the deformation of a continuum, we begin by identifying each material particle by its [position vector](@entry_id:168381) $\boldsymbol{X}$ in a **reference configuration**, denoted $\mathcal{B}_0$. This configuration is typically the undeformed state of the body at time $t=0$. As the body deforms, the particle originally at $\boldsymbol{X}$ moves to a new position $\boldsymbol{x}$ in the **current configuration** $\mathcal{B}_t$. The mapping that connects these configurations is the **motion**, $\boldsymbol{\varphi}$:

$$ \boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t) $$

The **displacement** of the particle is the vector difference between its current and reference positions: $\boldsymbol{u}(\boldsymbol{X}, t) = \boldsymbol{x} - \boldsymbol{X}$.

#### The Deformation Gradient

The most fundamental quantity in [finite deformation kinematics](@entry_id:195826) is the **[deformation gradient](@entry_id:163749)**, $\boldsymbol{F}$. It is the spatial gradient of the motion with respect to the material coordinates $\boldsymbol{X}$:

$$ \boldsymbol{F} = \frac{\partial \boldsymbol{\varphi}}{\partial \boldsymbol{X}} = \nabla_{\!X} \boldsymbol{\varphi} $$

The deformation gradient is a two-point tensor that locally linearizes the deformation. It maps an infinitesimal material vector $d\boldsymbol{X}$ in the reference configuration to its corresponding spatial vector $d\boldsymbol{x}$ in the current configuration: $d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$. From the definition of displacement, we can also express $\boldsymbol{F}$ as $\boldsymbol{F} = \boldsymbol{I} + \nabla_{\!X} \boldsymbol{u}$, where $\boldsymbol{I}$ is the second-order identity tensor.

A key physical constraint on $\boldsymbol{F}$ is that it must represent a locally invertible mapping, meaning no two material points can occupy the same spatial position. This requires its determinant, known as the **Jacobian** of the deformation, to be strictly positive:

$$ J = \det(\boldsymbol{F}) > 0 $$

The Jacobian $J$ has a direct physical interpretation: it measures the local change in volume. An infinitesimal [volume element](@entry_id:267802) $dV$ in the reference configuration is mapped to a [volume element](@entry_id:267802) $dv$ in the current configuration according to the relation $dv = J \, dV$. A deformation is termed **isochoric**, or volume-preserving, if $J=1$ everywhere. [@problem_id:2607098]

#### Measures of Strain

In [linear elasticity](@entry_id:166983), strain is defined using the symmetric part of the [displacement gradient](@entry_id:165352). For large deformations, however, this measure is inadequate as it is not objective—it does not remain invariant under rigid body rotations. We require a strain measure that quantifies deformation purely, independent of rigid motion. In the Total Lagrangian formulation, this is achieved through strain tensors defined entirely in the reference configuration.

The first step is to define the **right Cauchy-Green tensor**, $\boldsymbol{C}$. This tensor measures the change in the squared length of material fibers:

$$ \boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} $$

Consider a material fiber $d\boldsymbol{X}$. Its squared length in the reference configuration is $|d\boldsymbol{X}|^2 = d\boldsymbol{X} \cdot d\boldsymbol{X}$. In the current configuration, its squared length is $|d\boldsymbol{x}|^2 = d\boldsymbol{x} \cdot d\boldsymbol{x} = (\boldsymbol{F}d\boldsymbol{X}) \cdot (\boldsymbol{F}d\boldsymbol{X}) = d\boldsymbol{X} \cdot (\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}d\boldsymbol{X}) = d\boldsymbol{X} \cdot (\boldsymbol{C}d\boldsymbol{X})$. The tensor $\boldsymbol{C}$ is a symmetric, [positive-definite tensor](@entry_id:204409) defined in the reference configuration, making it a natural material measure of deformation.

From $\boldsymbol{C}$, we define the **Green-Lagrange [strain tensor](@entry_id:193332)**, $\boldsymbol{E}$:

$$ \boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I}) = \frac{1}{2}(\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} - \boldsymbol{I}) $$

The Green-Lagrange [strain tensor](@entry_id:193332) is the preferred strain measure in many TL formulations for several critical reasons [@problem_id:2607102]:

1.  **Objectivity**: $\boldsymbol{E}$ is invariant under superposed [rigid body motions](@entry_id:200666). If we apply a rotation $\boldsymbol{Q}$ to the current configuration, the motion becomes $\boldsymbol{\varphi}^* = \boldsymbol{Q}\boldsymbol{\varphi}$, and the [deformation gradient](@entry_id:163749) becomes $\boldsymbol{F}^* = \boldsymbol{Q}\boldsymbol{F}$. The new right Cauchy-Green tensor is $\boldsymbol{C}^* = (\boldsymbol{F}^*)^{\mathsf{T}}\boldsymbol{F}^* = (\boldsymbol{Q}\boldsymbol{F})^{\mathsf{T}}(\boldsymbol{Q}\boldsymbol{F}) = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}\boldsymbol{F} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} = \boldsymbol{C}$. Since $\boldsymbol{C}$ is unchanged, $\boldsymbol{E}$ is also unchanged. This confirms that $\boldsymbol{E}$ measures pure deformation, unaffected by rigid rotations. A direct consequence is that for a pure [rigid body rotation](@entry_id:167024), where $\boldsymbol{F}=\boldsymbol{Q}$, we have $\boldsymbol{C}=\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}=\boldsymbol{I}$, and thus $\boldsymbol{E}=\boldsymbol{0}$.

2.  **Consistency with Linear Theory**: For small displacement gradients ($\|\nabla_{\!X}\boldsymbol{u}\| \ll 1$), the Green-Lagrange strain tensor reduces to the classical [infinitesimal strain tensor](@entry_id:167211) $\boldsymbol{\varepsilon}$. Substituting $\boldsymbol{F} = \boldsymbol{I} + \nabla_{\!X}\boldsymbol{u}$ into the definition of $\boldsymbol{E}$ yields:
    $$ \boldsymbol{E} = \frac{1}{2}\left( (\boldsymbol{I} + \nabla_{\!X}\boldsymbol{u})^{\mathsf{T}}(\boldsymbol{I} + \nabla_{\!X}\boldsymbol{u}) - \boldsymbol{I} \right) = \frac{1}{2}\left( \nabla_{\!X}\boldsymbol{u} + (\nabla_{\!X}\boldsymbol{u})^{\mathsf{T}} + (\nabla_{\!X}\boldsymbol{u})^{\mathsf{T}}(\nabla_{\!X}\boldsymbol{u}) \right) $$
    The term $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla_{\!X}\boldsymbol{u} + (\nabla_{\!X}\boldsymbol{u})^{\mathsf{T}})$ is the [infinitesimal strain](@entry_id:197162). The quadratic term $(\nabla_{\!X}\boldsymbol{u})^{\mathsf{T}}(\nabla_{\!X}\boldsymbol{u})$ is negligible for small gradients. This consistency is crucial, as it ensures that a general nonlinear code will recover the correct linear elastic solution in the small deformation limit.

3.  **Material Measure**: Both $\boldsymbol{C}$ and $\boldsymbol{E}$ are defined with respect to the reference configuration, making them inherently suitable for a Lagrangian description where the material coordinates $\boldsymbol{X}$ are the independent variables.

### Kinetics: Stress Measures for Finite Deformation

The concept of stress becomes more complex in [finite deformation theory](@entry_id:202998), as one must be precise about which area (reference or current) and which force vector (reference or current) is being used. This leads to several distinct but related [stress measures](@entry_id:198799).

The most physically intuitive stress is the **Cauchy stress tensor**, $\boldsymbol{\sigma}$. It is the "true" stress, defined in the current configuration. It relates the [traction vector](@entry_id:189429) $\boldsymbol{t}$ (force per unit *current* area $da$) to the surface normal $\boldsymbol{n}$ in the current configuration via Cauchy's law: $\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$. A fundamental principle of continuum mechanics, the [balance of angular momentum](@entry_id:181848), requires that $\boldsymbol{\sigma}$ be a [symmetric tensor](@entry_id:144567).

While intuitive, $\boldsymbol{\sigma}$ is a spatial quantity, living in the deforming domain $\mathcal{B}_t$, which makes it less convenient for a Total Lagrangian formulation. We therefore introduce material [stress measures](@entry_id:198799).

The **first Piola-Kirchhoff stress tensor**, $\boldsymbol{P}$, is a mixed or "two-point" tensor. It relates the force $d\boldsymbol{f}$ acting on the current configuration to the area element $d\boldsymbol{A}$ in the reference configuration: $d\boldsymbol{f} = \boldsymbol{P}\boldsymbol{N} d\boldsymbol{A}$, where $\boldsymbol{N}$ is the normal in the reference configuration. This makes it the natural stress measure for describing tractions applied to the reference surface. [@problem_id:2607082]

The **second Piola-Kirchhoff stress tensor**, $\boldsymbol{S}$, is a fully material stress measure. It is constructed by pulling the force vector itself back to the reference configuration ($d\boldsymbol{f}_0 = \boldsymbol{F}^{-1}d\boldsymbol{f}$) and relating it to the reference area: $d\boldsymbol{f}_0 = \boldsymbol{S}\boldsymbol{N} d\boldsymbol{A}$.

These three stress tensors are rigorously connected through the [deformation gradient](@entry_id:163749) $\boldsymbol{F}$ and its Jacobian $J$. The key transformation relations are [@problem_id:2607082]:

$$ \boldsymbol{P} = \boldsymbol{F}\boldsymbol{S} $$
$$ \boldsymbol{\sigma} = J^{-1}\boldsymbol{P}\boldsymbol{F}^{\mathsf{T}} = J^{-1}\boldsymbol{F}\boldsymbol{S}\boldsymbol{F}^{\mathsf{T}} $$

An important and often misunderstood point concerns the symmetry of these tensors. While the symmetry of $\boldsymbol{\sigma}$ is a physical axiom, the symmetry of the other tensors is a derived property. Using the transformation laws, one can show that the second Piola-Kirchhoff stress $\boldsymbol{S}$ is always symmetric if $\boldsymbol{\sigma}$ is. However, the first Piola-Kirchhoff stress $\boldsymbol{P}$ is, in general, **not symmetric**. The transpose of $\boldsymbol{P}$ is $\boldsymbol{P}^{\mathsf{T}} = (\boldsymbol{F}\boldsymbol{S})^{\mathsf{T}} = \boldsymbol{S}^{\mathsf{T}}\boldsymbol{F}^{\mathsf{T}} = \boldsymbol{S}\boldsymbol{F}^{\mathsf{T}}$. Since $\boldsymbol{F}$ is not generally orthogonal, $\boldsymbol{F}\boldsymbol{S} \neq \boldsymbol{S}\boldsymbol{F}^{\mathsf{T}}$. The condition for objectivity ([frame-indifference](@entry_id:197245)) is not that $\boldsymbol{P}$ must be symmetric, but rather that the tensor $\boldsymbol{P}\boldsymbol{F}^{\mathsf{T}}$ must be symmetric. This is indeed satisfied, as $\boldsymbol{P}\boldsymbol{F}^{\mathsf{T}} = (\boldsymbol{F}\boldsymbol{S})\boldsymbol{F}^{\mathsf{T}} = \boldsymbol{F}\boldsymbol{S}\boldsymbol{F}^{\mathsf{T}} = J\boldsymbol{\sigma}$, which is symmetric. [@problem_id:2607127]

### The Governing Equations in the Total Lagrangian Formulation

The foundation for the TL formulation is the **[principle of virtual work](@entry_id:138749)**. In its spatial form, it states that for a body in equilibrium, the [internal virtual work](@entry_id:172278) equals the external [virtual work](@entry_id:176403) for any kinematically admissible [virtual displacement](@entry_id:168781) $\delta\boldsymbol{u}$:

$$ \int_{\mathcal{B}_t} \boldsymbol{\sigma} : \nabla_x\delta\boldsymbol{u} \, dv = \text{External Virtual Work} $$
where $\nabla_x\delta\boldsymbol{u}$ is the spatial gradient of the [virtual displacement](@entry_id:168781), which is the virtual [rate of deformation tensor](@entry_id:182598) $\delta\boldsymbol{d}$.

The essence of the Total Lagrangian method is to transform this equation into an integral over the fixed reference domain $\mathcal{B}_0$. This is achieved by systematically pulling back each term. Using the relationships $dv = J \, dV_0$, $\boldsymbol{\sigma} = J^{-1}\boldsymbol{F}\boldsymbol{S}\boldsymbol{F}^{\mathsf{T}}$, and the kinematic identity $\nabla_x\delta\boldsymbol{u} = (\nabla_X\delta\boldsymbol{u})\boldsymbol{F}^{-1}$, the internal work term becomes:

$$ \int_{\mathcal{B}_t} \boldsymbol{\sigma} : \nabla_x\delta\boldsymbol{u} \, dv = \int_{\mathcal{B}_0} \left(J^{-1}\boldsymbol{F}\boldsymbol{S}\boldsymbol{F}^{\mathsf{T}}\right) : \left( (\nabla_X\delta\boldsymbol{u})\boldsymbol{F}^{-1} \right) J \, dV_0 $$

After algebraic simplification and recognizing that $\delta\boldsymbol{E} = \frac{1}{2}(\boldsymbol{F}^{\mathsf{T}}\nabla_X\delta\boldsymbol{u} + (\nabla_X\delta\boldsymbol{u})^{\mathsf{T}}\boldsymbol{F})$, the integral beautifully simplifies to:

$$ \int_{\mathcal{B}_0} \boldsymbol{S} : \delta\boldsymbol{E} \, dV_0 $$

This reveals the fundamental pairing in the TL formulation: the second Piola-Kirchhoff stress $\boldsymbol{S}$ is **energetically conjugate** to the Green-Lagrange strain $\boldsymbol{E}$. This means their double contraction integrated over the reference volume gives the [internal virtual work](@entry_id:172278). [@problem_id:2607098] More generally, we can identify two primary work-conjugate pairs based on the [stress power](@entry_id:182907) per unit reference volume, $\mathfrak{p}_0$:

$$ \mathfrak{p}_0 = \boldsymbol{S} : \dot{\boldsymbol{E}} = \boldsymbol{P} : \dot{\boldsymbol{F}} $$

For **[hyperelastic materials](@entry_id:190241)**, where stress is derived from a stored energy density function $\Psi$, objectivity requires that $\Psi$ depends on deformation only through an objective measure like $\boldsymbol{C}$. For $\Psi = \hat{\Psi}(\boldsymbol{C})$, the constitutive law for $\boldsymbol{S}$ is given by:

$$ \boldsymbol{S} = 2 \frac{\partial \hat{\Psi}}{\partial \boldsymbol{C}} $$

This direct relationship makes the $(S, E)$ pair particularly natural for implementing hyperelastic models. [@problem_id:2607102]

The complete [weak form](@entry_id:137295) of the [equilibrium equations](@entry_id:172166) in the TL formulation is:
$$ \int_{\mathcal{B}_0} \boldsymbol{S} : \delta\boldsymbol{E} \, dV_0 = \int_{\mathcal{B}_0} \boldsymbol{B}_0 \cdot \delta\boldsymbol{u} \, dV_0 + \int_{\Gamma_{0,t}} \boldsymbol{T}_0 \cdot \delta\boldsymbol{u} \, dA_0 $$
where $\boldsymbol{B}_0$ is the [body force](@entry_id:184443) per unit reference volume and $\boldsymbol{T}_0$ is the prescribed **nominal traction** (force per unit reference area) on the boundary portion $\Gamma_{0,t}$. This leads to the definition of boundary conditions in the reference configuration:
-   **Essential (Displacement) Boundary Condition:** $ \boldsymbol{u}(\boldsymbol{X}) = \bar{\boldsymbol{u}}(\boldsymbol{X}) $ on $\Gamma_{0,u}$.
-   **Natural (Traction) Boundary Condition:** The traction term in the weak form gives rise to the [natural boundary condition](@entry_id:172221), which relates the [internal stress](@entry_id:190887) state to the applied [surface traction](@entry_id:198058). This is given by $\boldsymbol{P}\boldsymbol{N}_0 = \boldsymbol{T}_0$ on $\Gamma_{0,t}$. Note the use of the first Piola-Kirchhoff stress $\boldsymbol{P}$, as it naturally relates to nominal traction. The force itself is invariant, so the relationship between spatial traction $\boldsymbol{t}$ and nominal traction $\boldsymbol{T}_0$ is one of force equivalence on corresponding area elements: $\boldsymbol{t} \, da = \boldsymbol{T}_0 \, dA_0$. [@problem_id:2607105]

### Finite Element Discretization

To solve the TL weak form numerically, we discretize the domain $\mathcal{B}_0$ into finite elements. The principles of the formulation are then applied at the element level.

#### The Isoparametric Element in a TL Context

In the isoparametric concept, the geometry and the [primary fields](@entry_id:153633) are interpolated using the same set of [shape functions](@entry_id:141015), $N_a$, which are defined on a standardized parent element in isoparametric coordinates $\boldsymbol{\xi} = (\xi, \eta, \zeta)$. For the Total Lagrangian formulation, this concept is applied as follows [@problem_id:2607092]:

1.  **Geometry Interpolation:** The reference coordinates $\boldsymbol{X}$ within an element are interpolated from the nodal reference coordinates $\boldsymbol{X}_a$:
    $$ \boldsymbol{X}(\boldsymbol{\xi}) = \sum_{a=1}^{n_{nodes}} N_a(\boldsymbol{\xi}) \boldsymbol{X}_a $$

2.  **Displacement Interpolation:** The displacement field $\boldsymbol{u}$ is interpolated from the nodal displacements $\boldsymbol{d}_a$:
    $$ \boldsymbol{u}(\boldsymbol{\xi}) = \sum_{a=1}^{n_{nodes}} N_a(\boldsymbol{\xi}) \boldsymbol{d}_a $$

For an 8-node trilinear hexahedral element, the [parent domain](@entry_id:169388) is the cube $[-1, 1]^3$, and the [shape functions](@entry_id:141015) are given by $N_a(\xi,\eta,\zeta) = \frac{1}{8}(1+\xi\xi_a)(1+\eta\eta_a)(1+\zeta\zeta_a)$, where $(\xi_a, \eta_a, \zeta_a)$ are the coordinates of node $a$ in the [parent domain](@entry_id:169388) (i.e., $\pm 1$).

#### The Strain-Displacement Operator and Internal Force Vector

The core of the numerical implementation is to express the virtual strain $\delta\boldsymbol{E}$ in terms of the nodal virtual displacements $\delta\boldsymbol{d}$. This defines the nonlinear [strain-displacement matrix](@entry_id:163451), $\boldsymbol{B}_L$. We start from the expression for the variation of the Green-Lagrange strain:

$$ \delta\boldsymbol{E} = \frac{1}{2} \left( (\nabla_X\delta\boldsymbol{u})^{\mathsf{T}}\boldsymbol{F} + \boldsymbol{F}^{\mathsf{T}}(\nabla_X\delta\boldsymbol{u}) \right) $$

By substituting the finite element interpolation for $\delta\boldsymbol{u}$ and its gradient, we can write the vectorized form of the virtual strain, $\widehat{\delta\boldsymbol{E}}$, as:

$$ \widehat{\delta\boldsymbol{E}} = \boldsymbol{B}_L \delta\boldsymbol{d} $$

Unlike in linear analysis, the strain-displacement operator $\boldsymbol{B}_L$ is not constant; it depends on the current state of deformation via the [deformation gradient](@entry_id:163749) $\boldsymbol{F}$. For an 8-node hexahedral element, the matrix $\boldsymbol{B}_L$ is a $6 \times 24$ matrix composed of eight $6 \times 3$ blocks, $\boldsymbol{B}_{La}$, one for each node. Each block takes the form [@problem_id:2607113]:
$$ \boldsymbol{B}_{La} = \begin{pmatrix} F_{11} N_{a,1} & F_{21} N_{a,1} & F_{31} N_{a,1} \\ F_{12} N_{a,2} & F_{22} N_{a,2} & F_{32} N_{a,2} \\ F_{13} N_{a,3} & F_{23} N_{a,3} & F_{33} N_{a,3} \\ \frac{1}{2}(F_{12}N_{a,1}+F_{11}N_{a,2}) & \frac{1}{2}(F_{22}N_{a,1}+F_{21}N_{a,2}) & \frac{1}{2}(F_{32}N_{a,1}+F_{31}N_{a,2}) \\ \frac{1}{2}(F_{13}N_{a,2}+F_{12}N_{a,3}) & \frac{1}{2}(F_{23}N_{a,2}+F_{22}N_{a,3}) & \frac{1}{2}(F_{33}N_{a,2}+F_{32}N_{a,3}) \\ \frac{1}{2}(F_{13}N_{a,1}+F_{11}N_{a,3}) & \frac{1}{2}(F_{23}N_{a,1}+F_{21}N_{a,3}) & \frac{1}{2}(F_{33}N_{a,1}+F_{31}N_{a,3}) \end{pmatrix} $$
where $N_{a,I} = \partial N_a / \partial X_I$.

With this, the [internal virtual work](@entry_id:172278) $\delta W_{int} = \int \boldsymbol{S}:\delta\boldsymbol{E} \, dV_0$ can be written in discrete form as $\delta\boldsymbol{d}^{\mathsf{T}} \boldsymbol{f}_{int}$, which defines the element **internal force vector** $\boldsymbol{f}_{int}$:

$$ \boldsymbol{f}_{int} = \int_{\Omega_{0}^e} \boldsymbol{B}_L^{\mathsf{T}} \widehat{\boldsymbol{S}} \, dV_0 $$

Here, $\widehat{\boldsymbol{S}}$ is the vectorized form of the second Piola-Kirchhoff stress. The exact vectorization scheme depends on the definition of $\boldsymbol{B}_L$. For example, if the shear components of $\widehat{\delta\boldsymbol{E}}$ contain factors of 2 (engineering strain), then the shear components of $\widehat{\boldsymbol{S}}$ would not. The key is to ensure the equivalence $\boldsymbol{S}:\delta\boldsymbol{E} = \widehat{\boldsymbol{S}}^{\mathsf{T}}\widehat{\delta\boldsymbol{E}}$. [@problem_id:2607117]

For [hyperelastic materials](@entry_id:190241), implementing the nonlinear system requires **[consistent linearization](@entry_id:747732)** of the internal force vector to obtain the tangent stiffness matrix. Here, the choice of stress measure becomes important. Using the $(S, E)$ pair typically yields a symmetric tangent stiffness matrix for hyperelastic laws derived from $\Psi(C)$, which is computationally advantageous. Using the $(P, F)$ pair, while leading to a non-symmetric tangent, can be algebraically simpler for certain classes of material models (like polyconvex energies) and simplifies the application of nominal [traction boundary conditions](@entry_id:167112). [@problem_id:2607115]

### Numerical Mechanisms and Pathologies: Volumetric Locking

A key mechanism to understand in the practical application of the TL formulation is **[volumetric locking](@entry_id:172606)**. This numerical [pathology](@entry_id:193640) occurs when using low-order elements, like the 8-node hexahedron, to model [nearly incompressible materials](@entry_id:752388).

The phenomenon arises from a mismatch between the element's kinematic capabilities and the constraints imposed by the material behavior. For a nearly [incompressible material](@entry_id:159741), the [bulk modulus](@entry_id:160069) $K$ is much larger than the shear modulus $\mu$. The volumetric part of the strain energy, which penalizes deviations of $J$ from 1, becomes dominant. When the internal force vector is computed using a standard full Gauss quadrature scheme (e.g., $2 \times 2 \times 2 = 8$ points for a hexahedron), the weak form effectively enforces the incompressibility constraint $J \approx 1$ at *each* of the 8 integration points.

The trilinear [displacement field](@entry_id:141476) of an 8-node element, however, is too simple. It lacks the kinematic richness to satisfy these 8 independent constraints simultaneously while also representing a general deformation mode like bending or shear. The element becomes "locked" in a state of spurious [volumetric strain](@entry_id:267252), making it artificially and excessively stiff. This manifests as an inability to deform correctly under shear or bending loads. [@problem_id:2607095]

Several remedies exist to alleviate volumetric locking, all of which aim to reduce the number of effective incompressibility constraints:

-   **Selective Reduced Integration (SRI):** This popular technique involves using a lower-order [quadrature rule](@entry_id:175061) for the volumetric part of the internal [work integral](@entry_id:181218), while retaining full integration for the deviatoric (shear) part. For an 8-node hexahedron, one might use a single Gauss point ($1 \times 1 \times 1$) for the volumetric term. This imposes only one, averaged incompressibility constraint on the element, which the trilinear field can easily accommodate.

-   **Assumed Strain Methods (e.g., $\bar{B}$ Method):** These methods directly modify the strain-displacement operator $\boldsymbol{B}_L$. Instead of using the compatible volumetric strain derived from the displacement field at each Gauss point, a "projected" or averaged volumetric strain field is used for the entire element. This again replaces multiple pointwise constraints with a single, less restrictive constraint, preventing locking.

It is crucial to recognize that locking is a problem of **over-constraint**, which is distinct from the problem of **under-constraint** ([rank deficiency](@entry_id:754065)) that causes spurious zero-energy or "hourglass" modes in [under-integrated elements](@entry_id:756301). The remedies for these two opposing issues are fundamentally different. [@problem_id:2607095]