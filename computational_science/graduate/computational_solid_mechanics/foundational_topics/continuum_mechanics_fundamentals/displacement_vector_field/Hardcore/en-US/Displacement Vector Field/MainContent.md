## Introduction
The [displacement vector](@entry_id:262782) field is a foundational concept in the study of [deformable bodies](@entry_id:201887), serving as the primary descriptor of motion and deformation in continuum mechanics. Its significance cannot be overstated; it is the kinematic bridge connecting a material's undeformed [reference state](@entry_id:151465) to its current, deformed configuration under applied loads. However, moving from this fundamental definition to its robust application in advanced [computational solid mechanics](@entry_id:169583) reveals a landscape of mathematical nuance and practical challenges. A deep understanding is required to distinguish between different descriptive frameworks, linear and nonlinear regimes, and the conditions that ensure physically meaningful solutions.

This article addresses the need for a cohesive understanding by exploring the [displacement vector](@entry_id:262782) field in its full theoretical and computational context. Over the next three sections, you will build a comprehensive mastery of this critical topic. We will begin in "Principles and Mechanisms" by establishing the core definitions, including the crucial Lagrangian and Eulerian viewpoints, and exploring the relationship between displacement, strain, and rotation. We will then examine the mathematical requirements for [well-posed problems](@entry_id:176268) and the computational hurdles encountered in advanced analysis. Following this, "Applications and Interdisciplinary Connections" will showcase the power of the [displacement field](@entry_id:141476) in solving complex engineering problems, modeling phenomena like fracture and contact, and bridging solid mechanics with fields like materials science and medical imaging. Finally, "Hands-On Practices" will provide the opportunity to apply these principles, solidifying your understanding by working through concrete examples that highlight the subtleties of deformation analysis.

## Principles and Mechanisms

The [displacement vector](@entry_id:262782) field is a cornerstone of continuum mechanics, providing the fundamental kinematic link between a body's initial, undeformed state and its final, deformed state. This chapter delves into the principles governing this field and the mechanisms by which it is described, analyzed, and applied in the context of [computational solid mechanics](@entry_id:169583). We will move from foundational definitions in different [reference frames](@entry_id:166475) to the nuances of local deformation, the mathematical requirements for physical consistency, and the advanced computational strategies needed to address complex material behaviors and [large deformations](@entry_id:167243).

### Defining Displacement: The Material and Spatial Viewpoints

To describe the motion of a continuous body, we must track the position of every material particle. We begin by identifying a **reference configuration**, an undeformed state of the body at time $t=0$, which we denote by $\mathcal{B}_0$. A material particle is uniquely identified by its position vector $\mathbf{X}$ in this configuration. The coordinates $\mathbf{X}$ are known as **material coordinates** or **Lagrangian coordinates**.

As the body deforms and moves through space, the particle originally at $\mathbf{X}$ will occupy a new position $\mathbf{x}$ at time $t$. The mapping that describes this relationship is the **motion**, denoted $\boldsymbol{\varphi}$:
$$
\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)
$$
The coordinates $\mathbf{x}$ are known as **spatial coordinates** or **Eulerian coordinates**.

The **displacement vector** for a particle is simply the vector connecting its original position to its current position. The description of this vector as a field, however, can adopt two different perspectives, a distinction that is critical in continuum mechanics.

The **material description**, or **Lagrangian description**, expresses the displacement as a function of the material coordinate $\mathbf{X}$ and time $t$. The displacement vector field, denoted $\mathbf{u}$, is defined as:
$$
\mathbf{u}(\mathbf{X}, t) = \boldsymbol{\varphi}(\mathbf{X}, t) - \mathbf{X}
$$
Here, the field $\mathbf{u}$ is defined over the reference configuration $\mathcal{B}_0$. This is the natural and most common perspective in solid mechanics, as material properties are typically tied to specific material particles, which are tracked by their initial coordinate $\mathbf{X}$. 

Conversely, the **spatial description**, or **Eulerian description**, expresses physical quantities as functions of the spatial coordinate $\mathbf{x}$ and time $t$. To define a displacement field from this perspective, we must first answer the question: "What is the displacement of the material particle that is *currently* at the spatial position $\mathbf{x}$?" To do this, we must first identify the particle's original position $\mathbf{X}$. This requires the motion $\boldsymbol{\varphi}$ to be invertible, allowing us to define an inverse mapping $\boldsymbol{\chi} = \boldsymbol{\varphi}^{-1}$, such that $\mathbf{X} = \boldsymbol{\chi}(\mathbf{x}, t)$. The spatial [displacement field](@entry_id:141476), which we can denote $\hat{\mathbf{u}}$, is then defined as the current position minus the original position of the particle now at $\mathbf{x}$:
$$
\hat{\mathbf{u}}(\mathbf{x}, t) = \mathbf{x} - \boldsymbol{\chi}(\mathbf{x}, t)
$$
The field $\hat{\mathbf{u}}$ is defined over the current, deformed configuration of the body. The two fields describe the same physical quantity but are expressed as functions of different [independent variables](@entry_id:267118). The relationship between them is one of composition: $\hat{\mathbf{u}}(\boldsymbol{\varphi}(\mathbf{X}, t), t) = \mathbf{u}(\mathbf{X}, t)$. Mixing these variables in a single expression, such as writing $\mathbf{u}(\mathbf{x}, t) = \mathbf{x} - \mathbf{X}$, is a common but fundamental error, as the independent variable on the left must determine all quantities on the right.  

### Local Deformation: The Displacement Gradient

The displacement field provides a global picture of the deformation. To understand the local deformation—stretching, shearing, and rotation of the material at a point—we must examine its gradient. The primary measure of local deformation is the **[deformation gradient tensor](@entry_id:150370)**, $\mathbf{F}$, defined as the gradient of the motion with respect to the material coordinates:
$$
\mathbf{F} = \nabla_{\mathbf{X}} \mathbf{x} = \frac{\partial \boldsymbol{\varphi}}{\partial \mathbf{X}}
$$
An infinitesimal material vector $d\mathbf{X}$ in the reference configuration is mapped to a vector $d\mathbf{x}$ in the current configuration by the relation $d\mathbf{x} = \mathbf{F} d\mathbf{X}$.

The deformation gradient is intimately related to the **[displacement gradient](@entry_id:165352)**, which we denote $\mathbf{H}$. By taking the material gradient of the Lagrangian displacement definition, we find:
$$
\mathbf{H} = \nabla_{\mathbf{X}} \mathbf{u} = \nabla_{\mathbf{X}}(\mathbf{x} - \mathbf{X}) = \frac{\partial \mathbf{x}}{\partial \mathbf{X}} - \frac{\partial \mathbf{X}}{\partial \mathbf{X}} = \mathbf{F} - \mathbf{I}
$$
where $\mathbf{I}$ is the second-order identity tensor. This simple relationship, $\mathbf{F} = \mathbf{I} + \mathbf{H}$, is of central importance, connecting the displacement field directly to the full measure of local deformation.  

Just as the fields themselves can be transformed between descriptions, so can their gradients. Using the [chain rule](@entry_id:147422), the spatial gradient of the Eulerian displacement field $\hat{\mathbf{u}}$ can be related to the material [displacement gradient](@entry_id:165352) $\mathbf{H}$. The result is a fundamental transformation rule:
$$
\nabla_{\mathbf{x}} \hat{\mathbf{u}} = (\nabla_{\mathbf{X}} \mathbf{u}) (\nabla_{\mathbf{x}} \mathbf{X}) = \mathbf{H} \mathbf{F}^{-1} = (\mathbf{F} - \mathbf{I}) \mathbf{F}^{-1} = \mathbf{I} - \mathbf{F}^{-1}
$$
This expression demonstrates how gradients in the current configuration are obtained from those in the reference configuration via post-multiplication by the inverse [deformation gradient](@entry_id:163749). 

### The Small-Deformation Regime: Linearized Kinematics

In many engineering applications, deformations are small. This allows for a significant simplification of the kinematics by assuming that the displacement gradients are small compared to unity, i.e., $\|\mathbf{H}\| \ll 1$. In this **small-strain** or **small-deformation** regime, we can linearize the [kinematics](@entry_id:173318) and gain profound insight into the physical meaning of the [displacement gradient](@entry_id:165352).

A key step is the additive decomposition of the [displacement gradient tensor](@entry_id:748571) $\mathbf{H}$ into its symmetric and skew-symmetric parts:
$$
\mathbf{H} = \boldsymbol{\varepsilon} + \mathbf{\Omega}
$$
where
$$
\boldsymbol{\varepsilon} = \frac{1}{2}(\mathbf{H} + \mathbf{H}^{\top}) = \frac{1}{2}(\nabla_{\mathbf{X}}\mathbf{u} + (\nabla_{\mathbf{X}}\mathbf{u})^{\top})
$$
$$
\mathbf{\Omega} = \frac{1}{2}(\mathbf{H} - \mathbf{H}^{\top}) = \frac{1}{2}(\nabla_{\mathbf{X}}\mathbf{u} - (\nabla_{\mathbf{X}}\mathbf{u})^{\top})
$$
The symmetric tensor $\boldsymbol{\varepsilon}$ is the **[infinitesimal strain tensor](@entry_id:167211)**, and the [skew-symmetric tensor](@entry_id:199349) $\mathbf{\Omega}$ is the **[infinitesimal rotation tensor](@entry_id:192754)** (or [spin tensor](@entry_id:187346)). This decomposition beautifully separates the local deformation into two distinct physical effects. 

The [infinitesimal strain tensor](@entry_id:167211) $\boldsymbol{\varepsilon}$ exclusively governs the change in shape (shear) and size (stretch) of a material element, to first order. This can be seen by examining the change in the squared length of a material line element $d\mathbf{X}$, which deforms to $d\mathbf{x} = \mathbf{F}d\mathbf{X}$. The change in squared length is $\|d\mathbf{x}\|^2 - \|d\mathbf{X}\|^2 = d\mathbf{X}^{\top}(\mathbf{F}^{\top}\mathbf{F} - \mathbf{I})d\mathbf{X}$. Substituting $\mathbf{F} = \mathbf{I} + \mathbf{H}$ and neglecting second-order terms in $\mathbf{H}$ yields:
$$
\|d\mathbf{x}\|^2 - \|d\mathbf{X}\|^2 \approx d\mathbf{X}^{\top}(\mathbf{H} + \mathbf{H}^{\top})d\mathbf{X} = 2 d\mathbf{X}^{\top}\boldsymbol{\varepsilon}d\mathbf{X}
$$
This shows that, to first order, only the symmetric part of the [displacement gradient](@entry_id:165352) contributes to length changes. The diagonal components of $\boldsymbol{\varepsilon}$ represent normal strains (stretches along coordinate axes), while the off-diagonal components represent shear strains (changes in angle). Furthermore, the local change in volume is given by $\det(\mathbf{F}) - 1$. For small deformations, this can be approximated as $\det(\mathbf{I} + \mathbf{H}) - 1 \approx \mathrm{tr}(\mathbf{H}) = \mathrm{tr}(\boldsymbol{\varepsilon})$, as the trace of the [skew-symmetric tensor](@entry_id:199349) $\mathbf{\Omega}$ is always zero. 

The [infinitesimal rotation tensor](@entry_id:192754) $\mathbf{\Omega}$ describes the local [rigid-body rotation](@entry_id:268623) of the material element, to first order. Any [skew-symmetric tensor](@entry_id:199349) in three dimensions has an associated **[axial vector](@entry_id:191829)** $\boldsymbol{\omega}$ such that its action on any vector $\mathbf{v}$ is given by the [cross product](@entry_id:156749): $\mathbf{\Omega}\mathbf{v} = \boldsymbol{\omega} \times \mathbf{v}$. This vector $\boldsymbol{\omega}$ represents the axis and magnitude of the infinitesimal rotation. A remarkable connection exists between this rotation vector and the displacement field itself:
$$
\boldsymbol{\omega} = \frac{1}{2} \nabla_{\mathbf{X}} \times \mathbf{u}
$$
Thus, the local material rotation is directly related to the curl of the [displacement field](@entry_id:141476). A [displacement field](@entry_id:141476) with zero curl is said to be irrotational, at least at the infinitesimal level.  For a given [displacement field](@entry_id:141476), such as $\mathbf{u}(\mathbf{X}) = (0.002YZ + 0.001X, -0.003XZ + 0.002Y^2, 0.004XY)^{\top}$, one can directly compute the rotation vector at any point by taking the [partial derivatives](@entry_id:146280) and applying this formula. 

This linearized decomposition also approximates the **polar decomposition** of the [deformation gradient](@entry_id:163749), $\mathbf{F} = \mathbf{R}\mathbf{U}$, which multiplicatively separates deformation into a pure stretch ($\mathbf{U}$, a [symmetric tensor](@entry_id:144567)) followed by a rigid rotation ($\mathbf{R}$, an orthogonal tensor). For small deformations, these tensors are approximated by:
$$
\mathbf{U} \approx \mathbf{I} + \boldsymbol{\varepsilon} \quad \text{and} \quad \mathbf{R} \approx \mathbf{I} + \mathbf{\Omega}
$$
This confirms the distinct roles of $\boldsymbol{\varepsilon}$ as the measure of stretch and $\mathbf{\Omega}$ as the [generator of rotation](@entry_id:201605) in the linearized setting. It is important to note, however, that for a finite rigid rotation, such as $\mathbf{x} = \mathbf{Q}\mathbf{X}$, the [infinitesimal strain tensor](@entry_id:167211) $\boldsymbol{\varepsilon} = \frac{1}{2}(\mathbf{Q} + \mathbf{Q}^{\top}) - \mathbf{I}$ is generally not zero unless the rotation is trivial ($\mathbf{Q}=\mathbf{I}$). This highlights that $\boldsymbol{\varepsilon}$ is truly a measure of strain only in the small-deformation limit. 

### From Strain to Displacement: The Compatibility Conditions

We have seen that a given displacement field uniquely determines a strain field. A more profound question is the inverse: given a tensor field $\boldsymbol{\varepsilon}(\mathbf{x})$ that purports to be a strain field, does a single-valued [displacement field](@entry_id:141476) $\mathbf{u}(\mathbf{x})$ exist from which it could be derived? The answer is no, not for an arbitrary tensor field. The strain components cannot be independent of each other.

Since the six independent components of the symmetric [strain tensor](@entry_id:193332) $\boldsymbol{\varepsilon}$ are derived from only three independent components of the displacement vector $\mathbf{u}$, there must be conditions that the strain components must satisfy. These are the **Saint-Venant [compatibility conditions](@entry_id:201103)**. They arise from the simple mathematical fact that [mixed partial derivatives](@entry_id:139334) must commute for a sufficiently [smooth function](@entry_id:158037) (i.e., $u_{i,jk} = u_{i,kj}$). By differentiating the [strain-displacement relations](@entry_id:173321) and manipulating the terms to eliminate $\mathbf{u}$, one can derive the following set of 81 equations (of which only 6 are independent):
$$
\varepsilon_{ij,kl} + \varepsilon_{kl,ij} - \varepsilon_{ik,jl} - \varepsilon_{jl,ik} = 0
$$
where the comma denotes [partial differentiation](@entry_id:194612) (e.g., $\varepsilon_{ij,kl} = \partial^2 \varepsilon_{ij} / \partial x_k \partial x_l$). These equations are a necessary condition for a strain field to be derivable from a [displacement field](@entry_id:141476).

The role of domain topology is crucial here. On a **[simply connected domain](@entry_id:197423)** (one with no "holes"), these [compatibility conditions](@entry_id:201103) are not only necessary but also **sufficient** to guarantee the existence of a single-valued [displacement field](@entry_id:141476) $\mathbf{u}$. The [displacement field](@entry_id:141476), however, is not unique; it is determined only up to an arbitrary infinitesimal [rigid body motion](@entry_id:144691) (a constant translation and rotation), as such motions produce no strain. If the domain is not simply connected (e.g., a torus), satisfying the [compatibility conditions](@entry_id:201103) is not sufficient to ensure a single-valued displacement; multi-valued displacements, known as dislocations, can arise. 

### Displacement Fields in Boundary Value Problems

In [solid mechanics](@entry_id:164042), the [displacement field](@entry_id:141476) is the unknown solution to a [boundary value problem](@entry_id:138753) (BVP). The governing equation is typically the [balance of linear momentum](@entry_id:193575), which in the static case is $\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}$, where $\boldsymbol{\sigma}$ is the Cauchy stress tensor and $\mathbf{b}$ is the [body force](@entry_id:184443) per unit volume. To solve this, we must specify boundary conditions.

The modern approach to solving such [partial differential equations](@entry_id:143134), particularly with the Finite Element Method (FEM), relies on a **weak** or **[variational formulation](@entry_id:166033)**. This is derived by multiplying the governing equation by a suitable test function (a [virtual displacement](@entry_id:168781)) $\mathbf{w}$ and integrating over the domain. Applying [integration by parts](@entry_id:136350) (the [divergence theorem](@entry_id:145271)) is a key step that accomplishes two things: it reduces the order of differentiation required of the solution, and it naturally incorporates certain types of boundary conditions.

This process reveals a fundamental distinction between two types of boundary conditions. **Essential boundary conditions**, also known as **Dirichlet conditions**, are those that prescribe the value of the primary field variable—in this case, the displacement $\mathbf{u}$—on a part of the boundary, $\Gamma_u$. These conditions must be enforced directly on the space of possible solutions (the [trial space](@entry_id:756166)). Consequently, the corresponding [test functions](@entry_id:166589) $\mathbf{w}$ must vanish on $\Gamma_u$. 

**Natural boundary conditions**, also known as **Neumann conditions**, arise "naturally" from the integration-by-parts procedure. In elasticity, these are conditions on the [surface traction](@entry_id:198058) vector, $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$, prescribed on a boundary portion $\Gamma_t$. The traction term appears explicitly as a boundary integral in the weak formulation. Unlike essential conditions, they are not imposed on the [function space](@entry_id:136890) but are instead satisfied in an average sense by the [variational equation](@entry_id:635018) itself. 

The requirement that the total strain energy of the body must be finite imposes a strict mathematical constraint on the set of admissible displacement fields. The [strain energy density](@entry_id:200085) is a quadratic function of the strain tensor, which contains first derivatives of the displacement. For the total energy, $\int_{\Omega} W(\boldsymbol{\varepsilon}(\mathbf{u})) dV$, to be finite, the displacement field $\mathbf{u}$ and its first [weak derivatives](@entry_id:189356) must be square-integrable. The space of all such [vector fields](@entry_id:161384) is the **Sobolev space** $[H^1(\Omega)]^d$. This is the natural "energy space" for linear elasticity.  For a conforming FEM approximation, the discrete displacement field must belong to this space. For [piecewise polynomial](@entry_id:144637) elements, this implies that the displacement must be continuous across element boundaries, a condition known as $C^0$ continuity. Discontinuous elements would have infinite [strain energy](@entry_id:162699) at the interfaces and are thus non-conforming in this standard setting. 

Finally, for a solution to the elasticity BVP to be unique, the formulation must be **coercive**. This means that the strain energy must control the [displacement field](@entry_id:141476) in a meaningful way. Since [rigid body motions](@entry_id:200666) produce zero strain energy, they are "invisible" to the energy. **Korn's inequality** is the crucial theorem that ensures coercivity once [rigid body motions](@entry_id:200666) are accounted for. In one form, it states that for any displacement field $\mathbf{u} \in [H^1(\Omega)]^d$, there exists a constant $C$ such that:
$$
\|\nabla \mathbf{u}\|_{L^{2}(\Omega)} \leq C\big(\|\boldsymbol{\varepsilon}(\mathbf{u})\|_{L^{2}(\Omega)} + \|\mathbf{u}\|_{L^{2}(\Omega)}\big)
$$
This inequality guarantees that if the [strain energy](@entry_id:162699) (which controls $\|\boldsymbol{\varepsilon}(\mathbf{u})\|$) is bounded, the [displacement field](@entry_id:141476) is also controlled, preventing unphysical deformations. For problems with only [traction boundary conditions](@entry_id:167112) (pure Neumann problems), the solution is unique only up to a [rigid body motion](@entry_id:144691). To obtain a unique numerical solution, one must work in a [quotient space](@entry_id:148218) $H^1/\mathcal{R}$ or explicitly apply constraints to remove these [rigid body modes](@entry_id:754366). Korn's inequality is what makes this procedure mathematically sound. 

### Advanced Mechanisms and Computational Challenges

While the linear theory provides a robust framework, computational practice often encounters situations where its direct application fails or is insufficient. Two such cases are of particular importance: [near-incompressibility](@entry_id:752381) and [large rotations](@entry_id:751151).

#### Volumetric Locking in Nearly Incompressible Materials

Many materials, such as rubber or living tissue, are **[nearly incompressible](@entry_id:752387)**. In the context of [isotropic linear elasticity](@entry_id:185899), this means their [bulk modulus](@entry_id:160069) $K$ is much larger than their [shear modulus](@entry_id:167228) $\mu$. As $K \to \infty$, the material approaches the ideal limit of perfect incompressibility, where the volume cannot change. This imposes the kinematic constraint $\nabla \cdot \mathbf{u} = 0$.

When using a standard, low-order, displacement-based FEM, this constraint leads to a catastrophic failure known as **volumetric locking**. The discrete space of possible displacement fields is often too poor to satisfy the [divergence-free constraint](@entry_id:748603) adequately. For example, with linear triangular or [tetrahedral elements](@entry_id:168311), the strain is constant within each element. The condition $\nabla \cdot \mathbf{u}^h = 0$ becomes a system of algebraic constraints, one for each element. This system is often so restrictive that it allows only the trivial solution $\mathbf{u}^h = \mathbf{0}$, effectively "locking" the mesh and preventing any meaningful deformation. The result is a numerical solution that is orders of magnitude too stiff and physically useless. The large penalty term $\frac{1}{2}K \int (\nabla \cdot \mathbf{u}^h)^2 dV$ in the energy functional is the direct source of this artificial stiffness. 

The standard remedy is to move to a **mixed displacement-pressure formulation**. Here, the pressure $p$ is introduced as an independent field that acts as a Lagrange multiplier to enforce the [incompressibility constraint](@entry_id:750592). The weak form becomes a [saddle-point problem](@entry_id:178398), seeking a pair $(\mathbf{u}, p)$. The resulting [bilinear form](@entry_id:140194) for the nearly incompressible problem is:
$$
\int_{\Omega} 2\mu \, \mathrm{dev}(\boldsymbol{\varepsilon}(\mathbf{u})) : \mathrm{dev}(\boldsymbol{\varepsilon}(\mathbf{v})) \, dV - \int_{\Omega} p (\nabla \cdot \mathbf{v}) \, dV - \int_{\Omega} q (\nabla \cdot \mathbf{u}) \, dV - \int_{\Omega} \frac{1}{K} p q \, dV
$$
where $\mathbf{v}$ and $q$ are the test functions for displacement and pressure, respectively. This formulation effectively decouples the deviatoric (shape-changing) response from the volumetric (pressure) response, circumventing the locking issue and providing stable, accurate solutions. 

#### Large Rotations in Nonlinear Analysis

When deformations are large, the linear theory breaks down. One of the most significant challenges in [nonlinear solid mechanics](@entry_id:171757) is the correct treatment of large rigid-body rotations. While a large rotation should produce no strain and no stress, naive [numerical schemes](@entry_id:752822) can fail to preserve this property, leading to **spurious strains**.

Consider a body undergoing a large rigid rotation in a **Total Lagrangian (TL)** formulation, where all quantities are referred back to the initial configuration. If the incremental displacement $\Delta \mathbf{u}$ is updated additively at each step of a simulation ($ \mathbf{u}_{k+1} = \mathbf{u}_k + \Delta \mathbf{u}_k $), rotations are treated as vectors that can be added. However, finite rotations are not additive; they are multiplicative operations. For example, applying two successive rotations $R(\theta/2)$ is equivalent to a single rotation $R(\theta) = R(\theta/2)R(\theta/2)$. An additive scheme approximates the final deformation gradient as $F \approx I + \sum \Delta F_i$, which is not an orthogonal tensor and will therefore produce a non-zero Green-Lagrange strain, $E = \frac{1}{2}(F^T F - I) \neq 0$, even for a pure rigid motion. This is a purely numerical artifact that introduces fake energy into the system. 

The robust solution is to adopt a **corotational framework**. The core idea is to multiplicatively decompose the [deformation gradient](@entry_id:163749) at each element into a stretch and a rotation using the polar decomposition, $F=RU$. Strains and stresses are computed in a "corotated" coordinate system that rotates with the material element. The total rotation is then updated multiplicatively, $R_{k+1} = \Delta R R_k$, where $\Delta R$ is the rotational part of the incremental [deformation gradient](@entry_id:163749). This approach explicitly separates the [rigid motion](@entry_id:155339) from the pure deformation at every step, ensuring that large rigid rotations produce no spurious strains and correctly modeling the physics of large-deformation kinematics. 