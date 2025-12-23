## Introduction
Simulating physical phenomena in domains that change shape over time, such as in fluid-structure interaction or free-surface flows, presents a significant computational challenge. Standard fixed-grid (Eulerian) or material-following (Lagrangian) methods are often inadequate for these complex scenarios. The Arbitrary Lagrangian-Eulerian (ALE) framework provides a flexible and powerful solution, allowing the computational grid to move independently to optimize solution quality while conforming to moving boundaries.

However, correctly applying conservation laws on a moving grid is non-trivial; a naive approach can introduce numerical errors that violate the very physics being modeled. This article addresses this gap by providing a comprehensive guide to the formulation and implementation of ALE methods, specifically within the highly accurate Discontinuous Galerkin (DG) framework.

Across the following chapters, you will build a foundational understanding of this advanced numerical technique. The journey begins in **Principles and Mechanisms**, where we will dissect the kinematic foundations of the ALE description, derive the modified conservation laws, and explore the critical role of the Geometric Conservation Law (GCL) in high-order DG schemes. Next, **Applications and Interdisciplinary Connections** will showcase the framework's versatility, demonstrating its use in diverse fields from aerospace engineering to computational electromagnetics. Finally, the **Hands-On Practices** section will allow you to solidify your knowledge by tackling concrete problems related to mesh [kinematics](@entry_id:173318), conservation, and [time integration](@entry_id:170891).

## Principles and Mechanisms

The Arbitrary Lagrangian-Eulerian (ALE) framework provides a powerful and flexible methodology for simulating physical phenomena governed by conservation laws in domains that change shape and size over time. Unlike a purely Eulerian description where the computational grid is fixed, or a purely Lagrangian description where the grid moves with the material, the ALE approach allows the grid motion to be prescribed independently. This freedom is essential for a vast range of applications, from [fluid-structure interaction](@entry_id:171183) to free-surface flows, where it is advantageous to have mesh nodes that conform to moving boundaries while allowing the interior mesh to adapt for [optimal solution](@entry_id:171456) quality. This chapter elucidates the fundamental principles and mechanisms underpinning ALE formulations, with a specific focus on their implementation within the Discontinuous Galerkin (DG) framework.

### Kinematic Foundations of the ALE Description

The mathematical description of a moving domain begins with a mapping. We define a smooth, invertible map, $\boldsymbol{\chi}$, that connects a fixed, time-independent **reference domain**, $\Omega_0$, to the time-dependent **physical domain**, $\Omega(t)$. A point $\mathbf{X}$ in the reference domain is mapped to a point $\mathbf{x}$ in the physical domain at time $t$ by the relation:
$$
\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)
$$
This mapping forms the kinematic basis of the entire ALE framework. From it, we derive several key quantities that describe the local deformation and motion of the grid.

The **[deformation gradient tensor](@entry_id:150370)**, denoted by $F$, measures how an infinitesimal vector in the reference domain is stretched and rotated into the physical domain. It is defined as the gradient of the mapping with respect to the reference coordinates:
$$
F(\mathbf{X},t) = \nabla_\mathbf{X} \boldsymbol{\chi}(\mathbf{X},t)
$$
In component form, its entries are $F_{ij} = \partial x_i / \partial X_j$.

The local change in volume due to the mapping is quantified by the **Jacobian determinant**, $J$. It is the determinant of the [deformation gradient tensor](@entry_id:150370), $J(\mathbf{X},t) = \det(F(\mathbf{X},t))$. The Jacobian relates an infinitesimal volume element $dV_X$ in the reference domain to its corresponding [volume element](@entry_id:267802) $dV_x$ in the physical domain via the fundamental relation $dV_x = J \, dV_X$. For the mapping to be physically meaningful and orientation-preserving, the Jacobian must be strictly positive, $J>0$.

The velocity of the computational grid itself is a central concept in the ALE method. The **grid velocity** (or mesh velocity), $\mathbf{w}$, is defined as the velocity of a point that has a fixed reference coordinate $\mathbf{X}$. It is therefore the partial time derivative of the mapping function holding $\mathbf{X}$ constant:
$$
\mathbf{w}(\mathbf{X},t) = \frac{\partial \boldsymbol{\chi}(\mathbf{X},t)}{\partial t} \bigg|_{\mathbf{X}}
$$
While naturally defined as a function on the reference domain, the grid velocity is typically needed as a field on the physical domain, $\mathbf{w}(\mathbf{x},t)$. This is achieved by composing the function with the inverse mapping, i.e., $\mathbf{w}(\mathbf{x},t) = \mathbf{w}(\boldsymbol{\chi}^{-1}(\mathbf{x},t), t)$. 

These kinematic quantities are not independent. A crucial relationship, known as the **Geometric Conservation Law (GCL)** in its differential form, connects the rate of change of the Jacobian to the grid velocity. This identity, also known as Euler's expansion formula, is derived using Jacobi's formula for the derivative of a determinant and can be shown to be:
$$
\frac{\partial J(\mathbf{X},t)}{\partial t} \bigg|_{\mathbf{X}} = J(\mathbf{X},t) \left( \nabla_x \cdot \mathbf{w}(\mathbf{x},t) \right)
$$
where $\nabla_x \cdot$ is the [divergence operator](@entry_id:265975) with respect to the physical coordinates $\mathbf{x}$. This law states that the rate of change of an infinitesimal [volume element](@entry_id:267802) is proportional to its current volume and the divergence of the [velocity field](@entry_id:271461) of its boundaries. As we will see, satisfying a discrete analog of the GCL is arguably the most critical aspect of a robust numerical ALE scheme. 

### Conservation Laws on Moving Grids

The primary challenge in ALE methods is to correctly formulate the conservation law to account for the grid motion. A naive application of a fixed-grid solver to a [moving mesh](@entry_id:752196) will lead to spurious sources or sinks, violating the very conservation principle we aim to model. The correct formulation is derived from the integral form of the conservation law over a [moving control volume](@entry_id:265261).

#### The Reynolds Transport Theorem and the Relative Flux

Let us consider a general [scalar conservation law](@entry_id:754531) in the physical domain, $\partial_t q + \nabla \cdot \mathbf{f}(q) = 0$. The **Reynolds Transport Theorem** provides a formula for the time derivative of the total amount of a quantity $q$ integrated over a [moving control volume](@entry_id:265261) $K(t)$ whose boundary moves with velocity $\mathbf{w}$:
$$
\frac{d}{dt} \int_{K(t)} q \, dV = \int_{K(t)} \frac{\partial q}{\partial t} \, dV + \int_{\partial K(t)} q (\mathbf{w} \cdot \mathbf{n}) \, dS
$$
where $\mathbf{n}$ is the outward unit normal to the boundary $\partial K(t)$. By substituting the term $\int_{K(t)} (\partial q / \partial t) \, dV$ from the original conservation law, we arrive at the integral form of the conservation law in the ALE framework:
$$
\frac{d}{dt} \int_{K(t)} q \, dV + \int_{\partial K(t)} (\mathbf{f}(q) - q\mathbf{w}) \cdot \mathbf{n} \, dS = 0
$$
This fundamental equation reveals that the change in the total quantity within the moving volume is balanced by the net flux across its moving boundary. The effective flux is not the physical flux $\mathbf{f}(q)$ alone, but rather the **ALE relative flux**, defined as $\mathbf{f}_{rel} = \mathbf{f}(q) - q\mathbf{w}$.   This relative flux represents the transport of the quantity $q$ as seen by an observer moving with the grid.

For a vector system of conservation laws, $\partial_t U + \nabla \cdot \mathbf{F}(U) = 0$, where $U \in \mathbb{R}^m$ is the state vector and $\mathbf{F}(U) \in \mathbb{R}^{m \times d}$ is the flux tensor, the same principle applies. The modified [convective flux](@entry_id:158187) tensor is given by $\mathbf{F}_{ALE}(U) = \mathbf{F}(U) - U\mathbf{w}^T$, where $U\mathbf{w}^T$ is the [outer product](@entry_id:201262) of the state vector and the grid velocity. For instance, for the one-dimensional compressible Euler equations with [state vector](@entry_id:154607) $U = (\rho, \rho u, E)^T$, the ALE [flux vector](@entry_id:273577) becomes: 
$$
F_{\text{ALE}}(U) = F(U) - wU = \begin{pmatrix} \rho u - w\rho \\ \rho u^2 + p - w\rho u \\ (E+p)u - wE \end{pmatrix} = \begin{pmatrix} \rho(u-w) \\ \rho u(u-w) + p \\ E(u-w) + pu \end{pmatrix}
$$
Each component of the ALE flux is seen to depend on the relative fluid velocity, $u-w$.

### Principles of ALE Discontinuous Galerkin Discretization

The DG method's reliance on element-local formulations and inter-element communication via [numerical fluxes](@entry_id:752791) makes it particularly well-suited for the ALE framework. However, the grid motion necessitates careful modifications to the standard DG machinery.

#### Numerical Fluxes for Relative Motion

A cornerstone of DG methods is the use of [numerical fluxes](@entry_id:752791) (e.g., Riemann solvers) at element interfaces to handle discontinuities in the solution. In an ALE context, the [numerical flux](@entry_id:145174) must be consistent with the relative flux, not the physical flux. This means that all characteristic information about wave propagation must be considered relative to the moving grid interface.

For a [linear advection equation](@entry_id:146245) with [constant velocity](@entry_id:170682) $a$, the relative transport speed is $a-w$. An [upwind flux](@entry_id:143931) must therefore be based on the sign of $(a-w)n$, where $n$ is the interface normal. This has profound implications:
- In an **Eulerian frame** ($w=0$), [upwinding](@entry_id:756372) depends on the sign of $an$, as is standard.
- In a **Lagrangian frame** ($w=a$), the relative speed is zero. There is no advective flux across element boundaries, and information is "locked" within each element as it moves with the flow.
- In a general **ALE frame**, the upwind direction depends on the competition between fluid velocity and grid velocity. It is entirely possible for the fluid to flow out of an element in an absolute sense ($an>0$), but for the grid boundary to move outward even faster ($wn>an$). In this case, the relative motion is *into* the element, and an [upwind flux](@entry_id:143931) must take the state from the neighboring element. 

This principle extends to systems of equations. For example, the celebrated Roe flux is an approximate Riemann solver built from the eigenstructure of the flux Jacobian. For an ALE formulation, the Roe flux is adapted by considering the Jacobian of the relative flux, $F_n(U) - w_n U$. The Jacobian of this relative flux is simply $A(U) - w_n I$, where $A(U)$ is the physical flux Jacobian and $I$ is the identity matrix. A remarkable consequence is that the eigenvectors of the system (the characteristic fields) are unchanged by the grid motion; only the eigenvalues (the [characteristic speeds](@entry_id:165394)) are shifted by the normal grid velocity $w_n$. The ALE Roe flux can thus be written as: 
$$
F^{*}_{\text{ALE}} = \frac{1}{2}(F_{n}(U_{L}) + F_{n}(U_{R})) - \frac{1}{2}w_{n}(U_{L} + U_{R}) - \frac{1}{2}R|\Lambda - w_{n}I|R^{-1}(U_{R} - U_{L})
$$
where $R$ and $\Lambda$ are the eigenvector and eigenvalue matrices of the physical flux Jacobian. This provides a systematic way to construct [numerical fluxes](@entry_id:752791) for ALE simulations.

#### The Geometric Conservation Law: A Cornerstone of ALE Methods

The continuous GCL, $\partial_t J = J(\nabla_x \cdot \mathbf{w})$, must be respected by the [numerical discretization](@entry_id:752782). Failure to do so results in a scheme that cannot even preserve a trivial constant solution (a "free-stream" state) on a [moving mesh](@entry_id:752196), as the grid motion itself will generate spurious sources and sinks. A numerical scheme that correctly preserves a constant state is said to satisfy the **discrete GCL**.

To see how a violation occurs, consider a nodal DG [discretization](@entry_id:145012) where spatial derivatives are approximated by a [differentiation matrix](@entry_id:149870) $D$. The continuous GCL, $\partial_t J = \partial_X w$ in 1D, suggests a discrete counterpart $J_{t,i} = (D w)_i$ at each node $i$. The problem arises when these two terms are computed inconsistently. For example, one might compute the grid velocity derivative $D w$ using the [differentiation matrix](@entry_id:149870), but compute the Jacobian time derivative $J_t$ by first finding an analytical formula for $J_t(X,t)$ and then evaluating it at the nodes. Because the [differentiation matrix](@entry_id:149870) $D$ is only exact for polynomials up to a certain degree, if $w(X)$ is not a polynomial (e.g., if it contains trigonometric functions), then the numerical derivative $D w$ will not equal the exact analytical derivative. This mismatch, $J_{t,i} - (D w)_i \neq 0$, creates a non-zero residual for a constant solution, destroying conservation. 

A robust ALE scheme must therefore ensure that:
1. The numerical flux at an interface is single-valued (conservative) and consistent with the ALE relative flux.
2. The grid velocity used by two neighboring elements at their common interface is identical.
3. A discrete GCL is satisfied, ensuring that the numerical operators for [geometry and physics](@entry_id:265497) are compatible. 

### High-Order ALE-DG Formulations

For [high-order accuracy](@entry_id:163460), the details of the weak formulation and its interaction with [numerical quadrature](@entry_id:136578) and [time integration](@entry_id:170891) become paramount.

#### The Weak Form on Reference Elements and Quadrature

The DG weak form is naturally constructed on the fixed [reference element](@entry_id:168425) $\hat{K}$. Terms in the weak form, such as the [mass matrix](@entry_id:177093), involve integrals of the form:
$$
\int_{\hat{K}} J(\mathbf{X},t) u(\mathbf{X},t) v(\mathbf{X},t) \, d\mathbf{X}
$$
where $u$ is the [trial function](@entry_id:173682) and $v$ is the test function. In practice, these integrals are computed using numerical quadrature. For the discrete scheme to maintain its formal order of accuracy and, crucially, to satisfy the GCL, these integrals often need to be computed exactly.

For methods using tensor-product elements (e.g., quadrilaterals or hexahedra) and tensor-product basis polynomials, this requires careful consideration of [quadrature rules](@entry_id:753909). A [tensor-product quadrature](@entry_id:145940) rule, built from a 1D rule with $n$ points, is exact if the degree of the integrand *in each coordinate direction separately* is within the range of [exactness](@entry_id:268999) of the 1D rule.
- A 1D $n$-point **Gauss-Legendre** rule integrates polynomials of degree up to $2n-1$ exactly.
- A 1D $n$-point **Gauss-Lobatto-Legendre** rule integrates polynomials of degree up to $2n-3$ exactly.

Therefore, for a tensor-product polynomial integrand $Juv$ with per-coordinate degrees $r_\ell, p_\ell, q_\ell$, the condition for exact integration with Gauss-Legendre quadrature is $r_\ell + p_\ell + q_\ell \le 2n-1$ for every coordinate $\ell$. Using a rule that is not exact (e.g., is under-integrated) can introduce quadrature errors that violate the discrete GCL, leading to a loss of conservation.  The transformation of fluxes to the [reference element](@entry_id:168425) also requires the computation of **contravariant basis vectors**, which are geometric quantities derived from the mapping $\boldsymbol{\chi}$ and are essential for correctly formulating the flux divergence in the transformed coordinate system. 

#### Time Integration of ALE Systems

The semi-discrete ALE-DG formulation results in a system of ordinary differential equations of the form:
$$
M(t) \dot{\mathbf{u}}(t) = \mathbf{r}(\mathbf{u}(t), t)
$$
where the mass matrix $M(t)$ is time-dependent due to the term $\int J(t) \dots d\mathbf{X}$. Standard explicit Runge-Kutta (RK) methods cannot be applied directly, as they are designed for systems of the form $\dot{\mathbf{u}} = f(\mathbf{u}, t)$.

The correct approach is to formulate the time-stepping scheme for the conserved variable $\mathbf{w}(t) = M(t)\mathbf{u}(t)$. Differentiating this product gives the equation to be integrated:
$$
\dot{\mathbf{w}}(t) = \dot{M}(t)\mathbf{u}(t) + M(t)\dot{\mathbf{u}}(t) = \dot{M}(t)\mathbf{u}(t) + \mathbf{r}(\mathbf{u}(t), t)
$$
An explicit RK method is then applied to this equation for $\mathbf{w}$. At each stage, one computes an intermediate value for $\mathbf{w}$, recovers the corresponding state $\mathbf{u}$ by solving a linear system with the mass matrix at that stage's time, and then evaluates the right-hand-side to find the stage derivative.  

Finally, the temporal integration must also satisfy a GCL condition. For the overall scheme to be freestream-preserving, the [time integration](@entry_id:170891) rule must be exact for the geometric terms. This imposes a condition on the RK method: the [quadrature rule](@entry_id:175061) defined by the RK coefficients $\{b_i, c_i\}$ must exactly integrate the time derivative of the mass matrix over one time step. This is the temporal GCL condition:
$$
\Delta t \sum_{i=1}^{s} b_i \dot{M}(t^n + c_i \Delta t) = \int_{t^n}^{t^{n+1}} \dot{M}(t) \, dt = M(t^{n+1}) - M(t^n)
$$
Satisfying this condition ensures that the time integrator's approximation of the total volume change is exact, thereby closing the loop and guaranteeing a fully conservative high-order ALE-DG scheme. 