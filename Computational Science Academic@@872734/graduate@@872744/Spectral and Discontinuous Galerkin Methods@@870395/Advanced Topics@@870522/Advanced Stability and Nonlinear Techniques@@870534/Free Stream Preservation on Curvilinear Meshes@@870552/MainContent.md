## Introduction
The accurate simulation of physical systems governed by conservation laws, from atmospheric flows to aerospace vehicle aerodynamics, often requires meshes that curve and conform to complex geometries. While [curvilinear meshes](@entry_id:748122) offer this essential flexibility, they introduce a fundamental numerical challenge: ensuring that the algorithm remains faithful to the underlying physics and is not corrupted by the grid's own geometry. The most basic test of this fidelity is the principle of **free-stream preservation**, which demands that a numerical scheme must perfectly maintain a uniform, constant state without generating artificial sources or sinks. The failure to do so results in a loss of consistency and prevents a simulation from converging to the correct solution.

This article provides a comprehensive exploration of this critical property. It addresses the knowledge gap between the theoretical necessity of free-stream preservation and the practical techniques required to achieve it in modern, [high-order numerical methods](@entry_id:142601). Across three chapters, you will gain a deep understanding of this topic.

The first chapter, **Principles and Mechanisms**, breaks down the mathematical origin of the problem, deriving the continuous and discrete forms of the Geometric Conservation Law (GCL) and explaining the severe consequences of its violation. Following this theoretical foundation, the **Applications and Interdisciplinary Connections** chapter demonstrates the principle's importance in computational fluid dynamics, its extension to [viscous flows](@entry_id:136330) and complex interfaces, and its surprising connections to fields like differential geometry and robotics. Finally, the **Hands-On Practices** section provides guided exercises to implement and verify the core concepts, cementing your understanding of how to build robust, geometrically consistent numerical schemes.

## Principles and Mechanisms

The accurate numerical simulation of physical phenomena described by conservation laws on domains with curved boundaries necessitates the use of [curvilinear meshes](@entry_id:748122). While this approach provides geometric flexibility, it introduces a significant challenge: the numerical scheme must remain faithful to the underlying physics even in the presence of non-trivial, spatially varying geometric factors. A fundamental test of this fidelity is the principle of **free-stream preservation**. This principle dictates that if the physical system is in a uniform, constant state (a "free stream"), the [numerical approximation](@entry_id:161970) must recognize this as an exact, steady solution and produce zero time evolution. Failure to do so results in the generation of spurious, non-physical [sources and sinks](@entry_id:263105) purely from the interaction of the algorithm with the grid, leading to a catastrophic loss of accuracy. This chapter elucidates the principles governing free-stream preservation, the mechanisms by which it is achieved, and the consequences of its violation.

### The Continuous Foundation: Coordinate Transformation and Metric Identities

To understand the challenge at the discrete level, we must first review the transformation of a conservation law from physical to computational coordinates. Consider a general system of [hyperbolic conservation laws](@entry_id:147752) in a physical domain with Cartesian coordinates $\boldsymbol{x} \in \mathbb{R}^d$:
$$
\frac{\partial \boldsymbol{u}}{\partial t} + \nabla_{\boldsymbol{x}} \cdot \boldsymbol{F}(\boldsymbol{u}) = \boldsymbol{0}
$$
where $\boldsymbol{u}$ is the vector of conserved [state variables](@entry_id:138790) and $\boldsymbol{F}$ is the physical flux tensor.

Numerical methods like the Discontinuous Galerkin (DG) or Spectral Element Method (SEM) are typically formulated on a simple, fixed reference element, such as a cube or triangle, with computational coordinates $\boldsymbol{\xi} \in \Omega_{\xi}$. A smooth, invertible mapping $\boldsymbol{x} = \boldsymbol{x}(\boldsymbol{\xi})$ connects the [reference element](@entry_id:168425) to a curved physical element. This transformation necessitates a [change of variables](@entry_id:141386) for the [differential operators](@entry_id:275037).

The relationship between derivatives in the two coordinate systems is given by the [chain rule](@entry_id:147422), which involves the Jacobian matrix of the mapping, $\boldsymbol{J}_{\text{mat}} = \frac{\partial \boldsymbol{x}}{\partial \boldsymbol{\xi}}$. The columns of this matrix are the **[covariant basis](@entry_id:198968) vectors**, $\boldsymbol{a}_{\alpha} = \frac{\partial \boldsymbol{x}}{\partial \xi_{\alpha}}$, which are tangent to the coordinate lines in the physical domain [@problem_id:3388162]. The volume of an infinitesimal element transforms according to the **Jacobian determinant**, $J = \det(\boldsymbol{J}_{\text{mat}})$.

Using the Piola identity, the [divergence operator](@entry_id:265975) can be transformed into a [conservative form](@entry_id:747710) in the reference coordinates:
$$
\nabla_{\boldsymbol{x}} \cdot \boldsymbol{F}(\boldsymbol{u}) = \frac{1}{J} \sum_{\alpha=1}^d \frac{\partial}{\partial \xi_{\alpha}} \left( \boldsymbol{F}_{\text{contra}}^{\alpha} \right)
$$
Here, $\boldsymbol{F}_{\text{contra}}^{\alpha}$ are the **contravariant flux components**, defined by contracting the physical flux with geometric factors representing the scaled face normals of the [reference element](@entry_id:168425) [@problem_id:3388212]. These factors are the **contravariant basis vectors**, $\boldsymbol{a}^{\alpha}$, scaled by the Jacobian:
$$
\boldsymbol{F}_{\text{contra}}^{\alpha}(\boldsymbol{u}) = J (\boldsymbol{a}^{\alpha} \cdot \boldsymbol{F}(\boldsymbol{u}))
$$
The contravariant vectors are related to the gradients of the reference coordinates, $\boldsymbol{a}^{\alpha} = \nabla_{\boldsymbol{x}} \xi_{\alpha}$, and can be computed from the [covariant vectors](@entry_id:263917). For instance, in 3D, $J\boldsymbol{a}^1 = \boldsymbol{a}_2 \times \boldsymbol{a}_3$.

Now, consider a free-stream state, where the solution is constant everywhere: $\boldsymbol{u}(\boldsymbol{x}, t) \equiv \boldsymbol{u}_0$. In this case, the physical flux $\boldsymbol{F}(\boldsymbol{u}_0)$ is also a constant tensor. The divergence in physical space is trivially zero. In the transformed coordinates, this implies:
$$
\frac{1}{J} \sum_{\alpha=1}^d \frac{\partial}{\partial \xi_{\alpha}} \left( J \boldsymbol{a}^{\alpha} \cdot \boldsymbol{F}(\boldsymbol{u}_0) \right) = \boldsymbol{0}
$$
Since $\boldsymbol{F}(\boldsymbol{u}_0)$ is constant, we can factor it out of the derivatives:
$$
\frac{1}{J} \left( \sum_{\alpha=1}^d \frac{\partial (J \boldsymbol{a}^{\alpha})}{\partial \xi_{\alpha}} \right) \cdot \boldsymbol{F}(\boldsymbol{u}_0) = \boldsymbol{0}
$$
For this equation to hold for *any* possible free-stream state $\boldsymbol{u}_0$, the geometric term itself must vanish. This gives rise to the fundamental **continuous metric identities**, also known as the **Geometric Conservation Law (GCL)** for a static mesh [@problem_id:3388230]:
$$
\sum_{\alpha=1}^d \frac{\partial (J \boldsymbol{a}^{\alpha})}{\partial \xi_{\alpha}} = \boldsymbol{0}
$$
This identity states that the field of Jacobian-scaled contravariant vectors is divergence-free in the computational domain. It is not a coincidence; it is a direct consequence of the definition of these vectors and the smoothness of the mapping, which ensures that [mixed partial derivatives](@entry_id:139334) commute (e.g., $\partial_{\xi_1}\partial_{\xi_2}\boldsymbol{x} = \partial_{\xi_2}\partial_{\xi_1}\boldsymbol{x}$) [@problem_id:3388212].

### The Discrete Challenge and the Discrete Geometric Conservation Law

When we discretize the transformed conservation law, the continuous derivatives $\partial/\partial \xi_{\alpha}$ are replaced by discrete differentiation operators, such as the Summation-By-Parts (SBP) differentiation matrices $\boldsymbol{D}_{\alpha}$ used in DGSEM. A numerical scheme is said to be **free-stream preserving** if, when initialized with a constant state $\boldsymbol{u}_h \equiv \boldsymbol{u}_0$, the semi-discrete residual at every degree of freedom is exactly zero [@problem_id:3388220].

The discrete residual, $\boldsymbol{\mathcal{R}}(\boldsymbol{u}_h)$, which approximates the flux divergence term, is composed of volume and surface contributions. For a constant state, the volume contribution becomes:
$$
\boldsymbol{\mathcal{R}}_{\text{vol}}(\boldsymbol{u}_0) = \sum_{\alpha=1}^d \boldsymbol{D}_{\alpha} \left( (J \boldsymbol{a}^{\alpha})_h \cdot \boldsymbol{F}(\boldsymbol{u}_0) \right) = \left( \sum_{\alpha=1}^d \boldsymbol{D}_{\alpha} (J \boldsymbol{a}^{\alpha})_h \right) \cdot \boldsymbol{F}(\boldsymbol{u}_0)
$$
where $(J \boldsymbol{a}^{\alpha})_h$ are the metric terms evaluated at the discretization nodes. For the total residual (including surface terms, which cancel for a constant state in a consistent scheme) to be zero for any arbitrary free-stream, the coefficient of $\boldsymbol{F}(\boldsymbol{u}_0)$ must be zero. This imposes a strict algebraic constraint on the discrete operators and the discrete geometric factors, known as the **Discrete Geometric Conservation Law (DGCL)** [@problem_id:3388163]:
$$
\sum_{\alpha=1}^d \boldsymbol{D}_{\alpha} (J \boldsymbol{a}^{\alpha})_h = \boldsymbol{0}
$$
This condition is the discrete analogue of the continuous metric identity. Crucially, its satisfaction is **not** automatic. Even if the mapping is smooth and the metric terms are evaluated exactly at the nodes, applying a discrete differentiation operator to the array of nodal metric values will not, in general, yield zero. This is due to [discretization error](@entry_id:147889), or aliasing, which arises when a discrete operator acts on the product of functions (here, the geometry and the flux).

### Consequences of Failure: Inconsistency and Loss of Accuracy

The failure to satisfy the DGCL is not a minor inaccuracy; it fundamentally compromises the numerical scheme. To understand why, consider a smooth solution that is a small perturbation around a constant state: $\boldsymbol{u}(\boldsymbol{x}) = \boldsymbol{u}_0 + \varepsilon \boldsymbol{v}(\boldsymbol{x})$ for small $\varepsilon$ [@problem_id:3388172].

If a scheme violates the DGCL, its discrete spatial operator $L_h$ produces a non-zero residual for the constant part: $L_h(\boldsymbol{u}_0) = \boldsymbol{E}_{GCL} \neq \boldsymbol{0}$. This residual $\boldsymbol{E}_{GCL}$ is a **grid-induced source term** whose magnitude depends on the grid curvature and the properties of the discrete operator, but critically, it does not depend on the mesh size $h$. When the operator is applied to the full solution $\boldsymbol{u}$, by linearity, the residual is approximately $L_h(\boldsymbol{u}) \approx \boldsymbol{E}_{GCL} + \varepsilon L_h(\boldsymbol{v})$.

The [truncation error](@entry_id:140949) of the scheme is the difference between the discrete operator acting on the exact solution and the [continuous operator](@entry_id:143297) acting on it, $\tau = L_h(\boldsymbol{u}) - L(\boldsymbol{u})$. Since the [continuous operator](@entry_id:143297) gives $L(\boldsymbol{u}_0) = \boldsymbol{0}$, the truncation error contains the term $\boldsymbol{E}_{GCL}$, which is of order $O(1)$ and does not vanish as the mesh is refined ($h \to 0$). A scheme whose [truncation error](@entry_id:140949) does not go to zero is formally **inconsistent** with the partial differential equation it is meant to solve. An inconsistent scheme cannot converge to the correct solution.

This failure can be viewed through the lens of [polynomial reproduction](@entry_id:753580). High-order methods derive their accuracy from the ability to exactly represent or operate on polynomials up to a certain degree. A constant state is a polynomial of degree 0. If a scheme cannot exactly preserve this simplest of all solutions on a curved grid, it has failed the most basic test of [polynomial reproduction](@entry_id:753580) in the physical, mapped space. This failure at degree 0 contaminates all higher-order approximations and prevents the scheme from achieving its designed [order of accuracy](@entry_id:145189).

A practical example of this failure arises when the metric terms are computed with a different level of precision or polynomial representation than the discrete derivative operators. For instance, if the mapping contains cubic terms, the metric factors may be polynomials of a degree higher than what the discrete derivative operator can differentiate exactly. When the operator is applied to these higher-degree metric polynomials, [aliasing error](@entry_id:637691) results in a non-zero discrete divergence, creating the spurious residual [@problem_id:3388229]. A more elementary failure occurs if [geometric scaling](@entry_id:272350) is ignored entirely, for example, in the calculation of boundary flux integrals, which also leads to a non-zero residual for a constant state [@problem_id:3388216].

### Achieving Free-Stream Preservation: Mimetic Discretization

The key to satisfying the DGCL lies in the principle of **[mimetic discretization](@entry_id:751986)**: the discrete operators and geometric terms must be constructed in a mutually consistent manner that preserves, or mimics, the algebraic structure of the continuous identities.

The continuous GCL, $\sum \partial_{\alpha}(J \boldsymbol{a}^{\alpha}) = \boldsymbol{0}$, holds because of the identity that the [divergence of a curl](@entry_id:271562) is zero, combined with the fact that the metric flux field $J\boldsymbol{a}$ can be expressed as the curl of a vector potential. A mimetic approach constructs the [discrete metric](@entry_id:154658) terms in a way that preserves this "[divergence of a curl](@entry_id:271562)" structure at the discrete level.

For DGSEM schemes on tensor-product elements (like hexahedra), a robust method is to use the **conservative curl-form** for the metric terms [@problem_id:3388178]. In this approach, the [discrete metric](@entry_id:154658) fluxes are not computed by first differentiating the mapping $\boldsymbol{x}_h$ and then forming cross products. Instead, they are defined directly via a discrete curl operation involving the discrete mapping coordinates $\boldsymbol{x}_h$ and the discrete differentiation operators $\boldsymbol{D}_{\alpha}$ themselves. For example:
$$
(J \boldsymbol{a}^{\xi})_h = \frac{1}{2} \left( \boldsymbol{D}_{\eta}(\boldsymbol{x}_h \times \boldsymbol{D}_{\zeta}\boldsymbol{x}_h) - \boldsymbol{D}_{\zeta}(\boldsymbol{x}_h \times \boldsymbol{D}_{\eta}\boldsymbol{x}_h) \right)
$$
with similar expressions for the other components. When the discrete divergence is applied to this construction, i.e., $\sum \boldsymbol{D}_{\alpha}(J \boldsymbol{a}^{\alpha})_h$, the terms rearrange. Because the discrete operators $\boldsymbol{D}_{\alpha}$ for a tensor-product grid commute (e.g., $\boldsymbol{D}_{\xi}\boldsymbol{D}_{\eta} = \boldsymbol{D}_{\eta}\boldsymbol{D}_{\xi}$), all terms cancel out exactly, and the DGCL is satisfied identically at every node. This ensures free-stream preservation by construction. This powerful result highlights that consistency between the discrete geometry and the discrete operators is paramount, more so than the "[exactness](@entry_id:268999)" of the metric terms in isolation.

### Broader Context and Related Properties

Free-stream preservation is a foundational property, but it is important to understand its place among other desirable features of a numerical scheme.

**Static vs. Moving Meshes:** The discussion thus far has focused on static meshes. For problems involving moving or deforming domains, such as in [fluid-structure interaction](@entry_id:171183), an **Arbitrary Lagrangian-Eulerian (ALE)** formulation is used. This introduces grid velocity into the equations and requires satisfaction of an additional time-dependent GCL identity, which relates the time rate of change of the cell volume, $\partial_t J$, to the divergence of the grid velocity field [@problem_id:3388230]. Both the static and time-dependent GCLs must be satisfied discretely for a scheme to be robust on moving [curvilinear meshes](@entry_id:748122).

**Distinction from Other Properties:** It is essential to distinguish free-stream preservation from other concepts of numerical stability and conservation [@problem_id:3388220].
*   **Mass Conservation:** A [conservative scheme](@entry_id:747714) ensures that the total mass (or any conserved quantity) within the domain changes only due to flux through the boundaries. This is a *global, integral* property. A scheme can be globally conservative yet fail to be free-stream preserving, allowing a constant state to evolve into spurious oscillations whose integral is zero.
*   **Energy Stability:** This property guarantees that a discrete norm of the solution (an "energy") does not grow unbounded in time. It provides a crucial form of stability against blow-up but does not guarantee accuracy. A scheme can be energy-stable but still corrupt a free-stream solution due to geometric errors.

**Compatibility with Entropy Stability:** For [nonlinear systems](@entry_id:168347) like the compressible Euler equations, a critical property for physical realism is **[entropy stability](@entry_id:749023)**, which ensures the numerical solution satisfies a discrete version of the Second Law of Thermodynamics. This is typically achieved by designing the discrete fluxes (both volume and surface) to be entropy-conservative or appropriately dissipative. A key result in modern numerical methods is that free-stream preservation and [entropy stability](@entry_id:749023) are **compatible** properties [@problem_id:3388224]. The constraints for satisfying the DGCL are purely geometric, while the constraints for [entropy stability](@entry_id:749023) concern the discretization of the physical flux terms. A robust scheme can and should be designed to satisfy both sets of constraints simultaneously, leading to a method that is high-order accurate, stable for nonlinear problems, and free of spurious grid-induced errors.