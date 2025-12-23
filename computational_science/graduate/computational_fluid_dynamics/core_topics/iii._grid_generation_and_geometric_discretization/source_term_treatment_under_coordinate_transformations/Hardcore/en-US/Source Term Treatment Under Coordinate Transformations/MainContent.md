## Introduction
Computational Fluid Dynamics (CFD) relies on accurately solving the governing conservation laws of [fluid motion](@entry_id:182721). While these laws are universal, simulating flows in realistic, complex geometries—from aircraft wings to riverbeds—necessitates a departure from simple Cartesian grids. The use of [curvilinear coordinate systems](@entry_id:172561) provides the flexibility to map these intricate physical domains onto structured, computationally efficient grids. However, this powerful transformation introduces a critical challenge: the proper treatment of source terms.

The mishandling of source terms during [coordinate transformation](@entry_id:138577) is a common pitfall that can lead to profound simulation errors, including the violation of fundamental conservation principles, the generation of non-physical flows, and [numerical instability](@entry_id:137058). This article provides a comprehensive guide to mastering the theory and practice of [source term treatment](@entry_id:755077) in [curvilinear coordinates](@entry_id:178535). It bridges the gap between the abstract mathematics of [tensor calculus](@entry_id:161423) and the practical demands of building robust and accurate CFD solvers.

Across three chapters, you will gain a deep understanding of this crucial topic. The "Principles and Mechanisms" section will establish the foundational theory, deriving how conservation laws and source terms transform, and introducing key concepts like the Jacobian, geometric sources, and the Geometric Conservation Law. Following this, "Applications and Interdisciplinary Connections" will showcase these principles in action, exploring their role in modeling atmospheric flows, [turbomachinery](@entry_id:276962), and the design of [well-balanced schemes](@entry_id:756694) that preserve delicate physical equilibria. Finally, the "Hands-On Practices" section will offer guided exercises to translate theoretical knowledge into practical coding skills, ensuring you can implement these techniques correctly and avoid common numerical artifacts.

## Principles and Mechanisms

In the study of fluid dynamics, the governing conservation laws form the bedrock of our mathematical models. While these laws are universal, their expression changes with the coordinate system used to describe the physical domain. The use of [curvilinear coordinates](@entry_id:178535) is indispensable for modeling flows in and around complex geometries, but this powerful technique introduces new terms and considerations, particularly regarding the treatment of sources. This chapter delineates the fundamental principles governing the transformation of conservation laws and their associated source terms, and explores the mechanisms by which accuracy and stability are maintained in numerical simulations.

### The Foundation: Conservation in Curvilinear Coordinates

The most robust starting point for our analysis is the integral form of a conservation law, which holds true even across discontinuities. For a scalar conserved quantity $u(\mathbf{x},t)$ in a fixed physical [control volume](@entry_id:143882) $\Omega$ with boundary $\partial\Omega$, this law states:

$$
\frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega} u\,\mathrm{d}V + \int_{\partial\Omega}\mathbf{F}\cdot\mathbf{n}\,\mathrm{d}A = \int_{\Omega} S_{\text{phys}}\,\mathrm{d}V
$$

Here, $\mathbf{F}$ is the flux of $u$, $\mathbf{n}$ is the outward unit normal on the boundary, and $S_{\text{phys}}$ is the physical source term, representing the rate of production or consumption of $u$ per unit physical volume.

To solve problems involving complex geometries, we often employ a coordinate transformation $\mathbf{x} = \mathbf{x}(\boldsymbol{\xi})$, which maps a simple, structured computational domain (e.g., a cube) with coordinates $\boldsymbol{\xi} = (\xi^1, \xi^2, \xi^3)$ to the complex physical domain. This mapping introduces several key geometric quantities that are essential for transforming the conservation law. The **[covariant basis](@entry_id:198968) vectors**, which are tangent to the coordinate lines in the physical domain, are defined as:

$$
\mathbf{a}_i = \frac{\partial \mathbf{x}}{\partial \xi^i}
$$

The volume of an infinitesimal parallelepiped in physical space spanned by these basis vectors is given by $dV = (\mathbf{a}_1 \cdot (\mathbf{a}_2 \times \mathbf{a}_3)) \, d\xi^1 d\xi^2 d\xi^3$. The [scalar triple product](@entry_id:152997) is the determinant of the Jacobian matrix of the transformation, denoted as the **Jacobian determinant**, $J = \det(\partial\mathbf{x}/\partial\boldsymbol{\xi})$. Thus, the relationship between physical and computational volume elements is $dV = J \, dV_{\xi}$, where $dV_{\xi} = d\xi^1 d\xi^2 d\xi^3$.

To transform the [flux integral](@entry_id:138365), we also need the **reciprocal basis vectors** (or **contravariant basis vectors**), $\mathbf{a}^i$, which are normal to the surfaces of constant $\xi^i$. They are defined by the duality relationship $\mathbf{a}^i \cdot \mathbf{a}_j = \delta^i_j$, where $\delta^i_j$ is the Kronecker delta. A crucial identity relates the reciprocal basis to the gradient of the computational coordinates: $\mathbf{a}^i = \nabla_{\mathbf{x}} \xi^i$.

With these tools, we can transform the [integral conservation law](@entry_id:175062). Applying the [change of variables theorem](@entry_id:160749) ($dV = J \, dV_{\xi}$) and the [divergence theorem](@entry_id:145271), one can derive the differential form of the conservation law in computational coordinates. This process reveals that the physical [divergence operator](@entry_id:265975), $\nabla_{\mathbf{x}} \cdot (\cdot)$, transforms into a new [divergence operator](@entry_id:265975) in computational space :

$$
\nabla_{\mathbf{x}} \cdot \mathbf{F} = \frac{1}{J} \frac{\partial}{\partial \xi^i} \left( J (\mathbf{F} \cdot \mathbf{a}^i) \right)
$$

(Here, and throughout, we use the Einstein [summation convention](@entry_id:755635) where repeated indices are summed over.) Applying this to the original PDE, $\partial_t u + \nabla_{\mathbf{x}} \cdot \mathbf{F} = S_{\text{phys}}$, and multiplying by $J$ yields the **strong conservation form**:

$$
\frac{\partial (J u)}{\partial t} + \frac{\partial}{\partial \xi^i} \left( J (\mathbf{F} \cdot \mathbf{a}^i) \right) = J S_{\text{phys}}
$$

This equation is fundamental. It expresses the conservation law in a form where the divergence of transformed fluxes in the computational domain is balanced by a transformed [source term](@entry_id:269111). The quantity $J u$ is the conserved density per unit computational volume, and the terms $J (\mathbf{F} \cdot \mathbf{a}^i)$ are the **contravariant fluxes**, representing the flux across surfaces of constant $\xi^i$. This form is called "conservative" because the spatial derivative term is a perfect divergence, which is critical for numerical methods that aim to preserve the conserved quantity.

### The Nature of Source Terms in Transformed Equations

The term on the right-hand side of the transformed equation, $J S_{\text{phys}}$, is the computational source density. A careful classification and correct transformation of all source terms is paramount for the physical fidelity of a simulation. We can broadly classify sources into two categories: physical and geometric.

#### Physical versus Geometric Sources

A **physical source** is a term that represents an actual physical process of creation or destruction of the conserved quantity, such as chemical reactions, gravitational [body forces](@entry_id:174230), or volumetric heating. These sources exist regardless of the coordinate system used. As derived above, a physical source density $S_{\text{phys}}$ (defined per unit physical volume) transforms to $J S_{\text{phys}}$ in the [conservative form](@entry_id:747710) of the equation .

A **geometric source**, by contrast, is an apparent source term that arises purely as an artifact of the coordinate system's curvature or motion. These terms do not represent physical production or consumption. For a [scalar conservation law](@entry_id:754531) in a stationary grid, all geometric effects are absorbed into the transformed fluxes, and no separate geometric source terms appear on the right-hand side. For example, in [cylindrical coordinates](@entry_id:271645), factors of the radius $r$ appear within the [divergence operator](@entry_id:265975) but do not constitute a standalone source term .

The situation becomes more complex for vector or tensor equations, such as the momentum equations. The use of [curvilinear coordinates](@entry_id:178535) introduces terms related to the spatial variation of the basis vectors, which are mathematically described by Christoffel symbols. These terms, such as the centrifugal and Coriolis-like terms that appear in [cylindrical coordinates](@entry_id:271645), are kinematic in nature and are properly classified as geometric sources. They vanish if the equations are expressed in a Cartesian frame . We will explore these in greater detail in a later section.

Furthermore, if the [coordinate mapping](@entry_id:156506) is time-dependent, $\mathbf{x} = \mathbf{x}(\boldsymbol{\xi}, t)$, as in Arbitrary Lagrangian-Eulerian (ALE) methods, the grid itself moves with a velocity $\mathbf{w} = (\partial\mathbf{x}/\partial t)_{\boldsymbol{\xi}}$. The transformation of the time derivative and flux terms introduces additional contributions involving the grid velocity and the rate of change of the Jacobian, $\partial J/\partial t$. These terms are purely geometric consequences of the moving frame of reference and must be carefully distinguished from the physical source $S_{\text{phys}}$ .

#### Transformation of Physical Source Densities

The factor $J$ is central to the correct treatment of physical sources. To illustrate its role, consider a simple case where the physical source is spatially uniform, $S(\mathbf{x}) = S_0$ . When viewed as a function of the computational coordinates, the value of the source at any point is still $S_0$, i.e., $S(\mathbf{x}(\boldsymbol{\xi})) = S_0$. However, to preserve the integral balance, the transformed source term density in the conservative equation must be $J(\boldsymbol{\xi}) S_0$. If the grid is non-uniform, the Jacobian $J(\boldsymbol{\xi})$ varies in space, and thus the *computational source density* is non-uniform, even though the physical source is uniform. This ensures that a larger physical cell (with a larger $J$) contributes a proportionally larger amount of the source to the overall balance.

In practice, source terms may be specified in two distinct ways :
1.  **Per Unit Physical Volume ($S_{phys}$):** This is the most common case, where the source represents a physical rate per unit of physical volume. As we have seen, the correct source term in the transformed conservative equation is $S_\xi = J S_{phys}$.
2.  **Per Unit Computational Volume ($S_{comp}$):** In some contexts, a source might be defined directly in the computational domain. In this case, the total source contribution is already specified as an integral over the computational volume, and the source term in the transformed equation is simply $S_\xi = S_{comp}$.

It is crucial for the practitioner to know how a [source term](@entry_id:269111) is defined to apply the correct transformation.

#### Transformation of Vector Sources

Many physical source terms, such as body forces, are vectors. For instance, the [gravitational force](@entry_id:175476) per unit mass is a constant vector in a global Cartesian frame, $\mathbf{f} = (0, 0, -g)$. When the momentum equations are formulated in [curvilinear coordinates](@entry_id:178535), this vector source must be expressed in components relative to the curvilinear basis.

If the equations are solved for the contravariant components of momentum, for instance, the source vector $\mathbf{f}$ must also be expressed in its contravariant components, $f^i$. These components are found by projecting the vector onto the reciprocal basis vectors :

$$
f^i = \mathbf{f} \cdot \mathbf{a}^i
$$

Given that the Cartesian components of $\mathbf{f}$ are $(f_x, f_y, f_z)$ and the reciprocal basis vectors are $\mathbf{a}^i = \nabla \xi^i$, this transformation can be written explicitly using the chain rule:

$$
f^i = f_x \frac{\partial \xi^i}{\partial x} + f_y \frac{\partial \xi^i}{\partial y} + f_z \frac{\partial \xi^i}{\partial z}
$$

The terms $\partial \xi^i / \partial x_j$ are the metrics of the inverse transformation and must be computed from the grid mapping $\mathbf{x}(\boldsymbol{\xi})$. An analogous procedure yields the covariant components, $f_i = \mathbf{f} \cdot \mathbf{a}_i$, if they are needed.

### Advanced Topics: Ensuring Accuracy and Stability

Correctly transforming the governing equations is only the first step. To develop robust [numerical schemes](@entry_id:752822), we must address several advanced issues where the interplay between geometry and source terms can profoundly impact the accuracy and stability of the solution.

#### Geometric Sources in Vector Equations

As previously mentioned, the transformation of vector conservation laws, such as the momentum equations, gives rise to geometric source terms. Let's examine the compressible, inviscid momentum equation for the covariant [momentum density](@entry_id:271360), $\rho u_i$. Starting from the [non-conservative form](@entry_id:752551) and rearranging it into a conservative structure generates source terms on the right-hand side that depend on the Christoffel symbols of the second kind, $\Gamma^k_{ij}$. These symbols encode the spatial rate of change of the basis vectors.

The resulting geometric source density (per unit physical volume) for the $i$-th covariant momentum equation can be shown to be :

$$
s_{i, \text{geom}} = \rho u^j u_k \Gamma^k_{ij} + p \Gamma^j_{ji}
$$

The first term, $\rho u^j u_k \Gamma^k_{ij}$, arises from the curvilinear expression of the [convective acceleration](@entry_id:263153), representing inertial effects like centrifugal forces. The second term, $p \Gamma^j_{ji}$, arises from the pressure gradient in a curved geometry. These terms are not physical [body forces](@entry_id:174230); they are purely kinematic effects that must be accurately accounted for in the numerical scheme.

#### The Geometric Conservation Law (GCL)

When a numerical method is implemented on a moving or [non-uniform grid](@entry_id:164708), it is not sufficient that the continuous equations are correct. The discrete approximations of the various geometric terms must also satisfy a fundamental [consistency condition](@entry_id:198045), known as the **Geometric Conservation Law (GCL)**.

The purpose of the GCL is to ensure that the numerical scheme does not create artificial sources or sinks of a conserved quantity due to the geometry of the grid itself. The most basic requirement is that a uniform flow field (a "free-stream" state) with zero physical sources should remain perfectly uniform when simulated by the scheme.

At the continuous level, the GCL is a set of mathematical identities. For a stationary grid, the identity is :
$$
\frac{\partial}{\partial \xi^i} (J \mathbf{a}^i) = \mathbf{0}
$$
This states that the divergence of the contravariant metric vectors is zero. For a time-dependent (ALE) grid, an additional identity is required, which relates the rate of change of the cell volume to the fluxes of the grid velocity through the cell faces :
$$
\frac{\partial J}{\partial t} + \frac{\partial}{\partial \xi^i} (J w^i) = 0
$$
where $w^i = \mathbf{w} \cdot \mathbf{a}^i$ are the contravariant components of the grid velocity.

In a numerical scheme, if the discrete approximations of the Jacobian, metric terms, and differential operators are not mutually consistent, the discrete version of the GCL will not be satisfied. A non-zero residual will be generated, which acts as a **spurious numerical source term**. This artificial source can corrupt the solution, especially in simulations of small perturbations around a uniform state, by violating free-stream preservation [@problem_id:3363921, @problem_id:3363896].

#### Well-Balanced Schemes

Many physical phenomena are characterized by steady-state equilibria where a non-zero flux gradient is precisely balanced by a physical source term. A classic example is the [hydrostatic balance](@entry_id:263368) in atmospheric or oceanic models, where the vertical pressure gradient balances the force of gravity. The continuous equation for this equilibrium is $\nabla \cdot \mathbf{F}(U^\star) = S(U^\star)$.

When this equation is transformed to [curvilinear coordinates](@entry_id:178535) and discretized, a subtle but critical challenge emerges. Standard finite volume or [finite difference schemes](@entry_id:749380) typically discretize the flux divergence term ($\partial_{\xi_i} \widehat{F}_i$) and the [source term](@entry_id:269111) ($J S$) using different methods or stencils. On a [non-uniform grid](@entry_id:164708), this leads to an inconsistent discretization of the physical flux gradient and the [source term](@entry_id:269111), breaking their delicate balance. The consequence is a spurious numerical residual that is often of order one, meaning it does not decrease as the grid is refined. This can completely overwhelm the true physics of the problem.

A numerical scheme is called **well-balanced** if it is specifically designed to preserve such physical equilibria exactly (to machine precision) at the discrete level . Achieving this requires that the discrete flux divergence and the discrete [source term](@entry_id:269111) cancel each other out perfectly when evaluated for the equilibrium solution:
$$
D_i \widehat{F}_i^h(U_h^\star) = J^h S^h(U_h^\star)
$$
Constructing a [well-balanced scheme](@entry_id:756693) often involves reformulating the source term or modifying the numerical flux function to ensure this discrete consistency. Satisfying the GCL is a necessary prerequisite for [well-balancing](@entry_id:756695), but [well-balancing](@entry_id:756695) is a more stringent condition that addresses the interplay between flux gradients and physical sources.

#### Source Term Stiffness

The final consideration is [numerical stability](@entry_id:146550). When a system of conservation laws is semi-discretized in space, it yields a large system of coupled [ordinary differential equations](@entry_id:147024) (ODEs) in time. The stability of explicit time-integration methods for this system is limited by the fastest time scale present. While transport phenomena (advection and diffusion) impose their own time step constraints (e.g., the CFL condition), source terms can introduce much faster, and often disparate, time scales.

This is particularly true for problems involving fast chemical reactions or [phase changes](@entry_id:147766), where the [source term](@entry_id:269111) $S(\phi)$ changes rapidly with the state variable $\phi$. Such a system is termed **stiff**. To analyze this, we can consider the semi-discrete ODE for the average value of a scalar $\bar{\phi}_P$ in a computational cell $P$ :

$$
m_P \frac{\mathrm{d}\bar{\phi}_P}{\mathrm{d}t} = - \mathcal{R}_P(\bar{\phi}_P) + \int_{\Omega_{\boldsymbol{\xi},P}} J S_V(\bar{\phi}_P) \mathrm{d}\boldsymbol{\xi}
$$

Here, $m_P = \int_{\Omega_{\boldsymbol{\xi},P}} J \rho \mathrm{d}\boldsymbol{\xi}$ is the total mass in the cell, and $\mathcal{R}_P$ is the net flux residual. The [characteristic time scale](@entry_id:274321) associated with the [source term](@entry_id:269111), $\tau_{S,P}$, is determined by linearizing the source term around the current state. This analysis reveals that the time scale is the inverse of the spectral radius (largest eigenvalue magnitude) of the linearized source operator, scaled by the cell mass:

$$
\tau_{S,P} = \frac{m_P}{\left|\lambda_{\max}\left(\int_{\Omega_{\boldsymbol{\xi},P}} J \frac{\partial S_V}{\partial \phi} \mathrm{d}\boldsymbol{\xi}\right)\right|}
$$

Here, $\partial S_V/\partial \phi$ is the Jacobian of the source term. A very small $\tau_{S,P}$ indicates a stiff source term, which would necessitate extremely small time steps for an explicit method to remain stable. The presence of the coordinate transformation Jacobian $J$ in this expression highlights that grid non-uniformity can directly influence the local stiffness of the system. Recognizing and properly treating [source term](@entry_id:269111) stiffness, often through implicit or semi-[implicit time integration](@entry_id:171761) methods, is essential for the efficient simulation of many real-world problems.