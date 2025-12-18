## Introduction
After spatially discretizing a partial differential equation using the Discontinuous Galerkin (DG) framework, we are left with a large system of coupled [ordinary differential equations](@entry_id:147024) (ODEs). The method chosen to integrate these ODEs in time is a fundamental decision that profoundly impacts the stability, accuracy, and [computational efficiency](@entry_id:270255) of the entire simulation. This choice is not a mere technical detail but a critical step in tailoring the numerical method to the physics of the problem at hand. Different problems, from hyperbolic [wave propagation](@entry_id:144063) to stiff [reaction-diffusion systems](@entry_id:136900), present unique challenges that render a one-size-fits-all approach impractical.

This article provides a comprehensive guide to navigating the complex landscape of [time integration](@entry_id:170891) for DG methods. It addresses the core challenge of stiffness, whether it arises from the mesh, the high polynomial degree of the DG basis, or the underlying physical phenomena. By understanding the trade-offs between different time-stepping families, you will be equipped to select and implement the most appropriate strategy for your specific application. The following chapters are structured to build this expertise progressively. First, **Principles and Mechanisms** will dissect the core mechanics of explicit, implicit, and implicit-explicit (IMEX) schemes, analyzing their stability and computational cost. Next, **Applications and Interdisciplinary Connections** will illustrate how these methods are deployed to solve real-world problems in computational fluid dynamics, [mathematical biology](@entry_id:268650), and [geophysics](@entry_id:147342). Finally, a series of **Hands-On Practices** will provide opportunities to apply these concepts and solidify your understanding of the algorithms.

## Principles and Mechanisms

Having established the spatial [discretization of partial differential equations](@entry_id:748527) using the Discontinuous Galerkin (DG) framework, we now turn our attention to the crucial task of advancing the solution in time. The [method of lines](@entry_id:142882) transforms a PDE into a large system of coupled ordinary differential equations (ODEs), which can be written in the general form:

$$M \frac{dU}{dt} = \mathcal{L}(U, t)$$

Here, $U(t)$ is the global vector containing all the polynomial basis coefficients (degrees of freedom) for the solution $U_h$ across all elements in the mesh. The matrix $M$ is the [block-diagonal mass matrix](@entry_id:140573), resulting from the inner product of basis functions within each element, and $\mathcal{L}(U, t)$ is the spatial operator, representing the DG weak form of the PDE's spatial derivatives and fluxes. The choice of how to integrate this ODE system in time is not merely a technical detail; it is a fundamental decision that profoundly impacts the stability, accuracy, and [computational efficiency](@entry_id:270255) of the entire simulation. This chapter elucidates the principles and mechanisms of the three major families of [time integration schemes](@entry_id:165373) used in conjunction with DG methods: explicit, implicit, and implicit-explicit (IMEX).

### Explicit Time Integration

Explicit [time integration schemes](@entry_id:165373) are characterized by their computational simplicity. The solution at a new time level, $U^{n+1}$, is computed directly from information at previous time levels, primarily $U^n$, without the need to solve any systems of equations.

#### The Courant-Friedrichs-Lewy (CFL) Condition in DG Methods

The prototypical explicit method is the Forward Euler scheme:

$$M \frac{U^{n+1} - U^n}{\Delta t} = \mathcal{L}(U^n)$$

which can be rearranged to give the update formula:

$$U^{n+1} = U^n + \Delta t M^{-1} \mathcal{L}(U^n)$$

While simple, this method reveals the primary limitation of all explicit schemes: [conditional stability](@entry_id:276568). The numerical solution remains bounded only if the time step $\Delta t$ is smaller than a certain threshold, dictated by the Courant-Friedrichs-Lewy (CFL) condition. This condition ensures that the [numerical domain of dependence](@entry_id:163312) contains the physical domain of dependence. For DG methods, the maximum [stable time step](@entry_id:755325) is constrained by the largest eigenvalues of the operator $M^{-1}\mathcal{L}$. The scaling of this time step limit reveals the inherent **stiffness** of DG discretizations .

For an advection problem with [wave speed](@entry_id:186208) $c$ on a mesh of element size $h$ using polynomials of degree $p$, the explicit time step is typically restricted by:

$$\Delta t \le C \frac{h}{c (p+1)^2}$$

For a diffusion problem with diffusivity $\nu$, the restriction is far more severe:

$$\Delta t \le C \frac{h^2}{\nu (p+1)^4}$$

These [scaling laws](@entry_id:139947) highlight several critical aspects. The time step must shrink linearly with the element size $h$ for advection and quadratically for diffusion. More strikingly, the dependence on the polynomial degree $p$ is severe, with the time step decreasing as $1/p^2$ for advection and $1/p^4$ for diffusion. This stiffness, particularly the strong dependence on $p$, often makes purely explicit methods impractical for diffusion-dominated problems or for simulations employing very high polynomial degrees. Furthermore, the stability limit is degraded by geometric factors on curved or distorted elements, which increase the norm of the discrete operator .

#### High-Order Explicit Methods and Strong Stability

To achieve higher-order accuracy in time, one typically employs multi-stage methods like explicit Runge-Kutta (RK) schemes. However, for [hyperbolic conservation laws](@entry_id:147752), where solutions may contain shocks or sharp gradients, accuracy is not the only concern. We require the scheme to be non-oscillatory. This has led to the development of **Strong Stability Preserving (SSP)** methods.

The principle of SSP methods is to construct a high-order scheme that is guaranteed to be stable under a chosen semi-norm (e.g., the Total Variation, TV) if the simple Forward Euler method is stable under the same semi-norm. This is achieved by ensuring that each stage of the high-order method can be written as a convex combination of forward Euler steps. If the forward Euler step is Total Variation Diminishing (TVD), meaning $\mathrm{TV}(U^{n+1}) \le \mathrm{TV}(U^n)$, and the TV semi-norm is convex, then the high-order SSP method will also be TVD.

A widely used example is the third-order, three-stage SSPRK(3,3) method. In its Shu-Osher representation, it is given by :
1. $U^{(1)} = U^n + \Delta t F(U^n)$
2. $U^{(2)} = \frac{3}{4} U^n + \frac{1}{4} \left( U^{(1)} + \Delta t F(U^{(1)}) \right)$
3. $U^{n+1} = \frac{1}{3} U^n + \frac{2}{3} \left( U^{(2)} + \Delta t F(U^{(2)}) \right)$
where $F(U) = M^{-1}\mathcal{L}(U)$. Each stage is a convex combination of previous results. For example, the second stage is a combination of the initial data $U^n$ and a forward Euler step applied to the first stage result, $U^{(1)}$. By repeatedly applying the convexity and the TVD property of the forward Euler step, one can prove that $\mathrm{TV}(U^{n+1}) \le \mathrm{TV}(U^n)$. This proof holds for general nonlinear operators $F$, provided the forward Euler step is TVD under a time step $\Delta t_{\mathrm{FE}}$ . The SSP coefficient, $c$, of a method is the factor by which its [stable time step](@entry_id:755325) relates to the forward Euler step: $\Delta t \le c \cdot \Delta t_{\mathrm{FE}}$. For the SSPRK(3,3) method, the SSP coefficient is $c=1$, meaning it maintains stability up to the same time step limit as forward Euler.

#### Computational Efficiency of Explicit DG

The principal advantage of explicit methods is their low cost per time step. Each step requires one or more evaluations of the spatial operator $\mathcal{L}(U)$ and an application of the inverse [mass matrix](@entry_id:177093), $M^{-1}$. For DG methods, these operations can be made remarkably efficient.

First, consider the mass [matrix inversion](@entry_id:636005). For a general choice of basis functions, $M$ is a [dense block](@entry_id:636480) within each element, and its inversion would be computationally expensive. However, a judicious choice of basis and quadrature can diagonalize $M$, a process often called **[mass lumping](@entry_id:175432)**. Specifically, if one uses a nodal basis of Lagrange polynomials defined on the points of a [quadrature rule](@entry_id:175061), and then uses that same quadrature rule to approximate the [mass matrix](@entry_id:177093) integral, the resulting matrix is diagonal . A prime example is the use of a nodal basis on the Legendre-Gauss-Lobatto (LGL) points, with LGL quadrature for the [mass matrix](@entry_id:177093) integration. The Kronecker-delta property of the Lagrange basis at the nodes, $\ell_i(\boldsymbol{\xi}_j) = \delta_{ij}$, ensures that the quadrature-approximated [mass matrix](@entry_id:177093) becomes diagonal. The cost of applying $M^{-1}$ collapses from $\mathcal{O}((p+1)^{2d})$ for a dense matrix to a trivial $\mathcal{O}((p+1)^d)$ for a diagonal one, a massive saving that is crucial to the efficiency of explicit DG methods .

Second, the evaluation of the spatial operator $\mathcal{L}(U)$ itself can be accelerated. For elements with a tensor-product structure (e.g., quadrilaterals in 2D, hexahedra in 3D), the required [multidimensional integrals](@entry_id:184252) and transformations can be performed as a sequence of one-dimensional operations. This technique, known as **sum factorization**, reduces the [computational complexity](@entry_id:147058) of applying the operator from $\mathcal{O}((p+1)^{2d})$ for a naive dense contraction to $\mathcal{O}(d(p+1)^{d+1})$ . This gain is so substantial that it makes high-order DG methods competitive with low-order methods in terms of computational cost for a given accuracy.

A final practical challenge arises on [curvilinear meshes](@entry_id:748122). A naive discretization of the transformed governing equations can violate a discrete version of the **Geometric Conservation Law (GCL)**. This leads to a non-zero residual for a uniform flow (a failure of free-stream preservation) and can introduce spurious instabilities. Enforcing the discrete GCL, for instance through the use of entropy-stable split forms or Summation-By-Parts (SBP) operators, is necessary to restore stability and accuracy. These techniques effectively make the discrete operator more skew-adjoint, improving the stability of explicit [time integrators](@entry_id:756005) .

### Implicit Time Integration

Implicit methods are designed to overcome the stringent stability constraints of their explicit counterparts, making them indispensable for [stiff problems](@entry_id:142143).

#### Motivation and A-Stability

An implicit scheme computes the new state $U^{n+1}$ using information from the same time level. The prototypical [implicit method](@entry_id:138537) is the Backward Euler scheme:

$$M \frac{U^{n+1} - U^n}{\Delta t} = \mathcal{L}(U^{n+1})$$

Rearranging, we see that $U^{n+1}$ is the solution of a system of equations:

$$(M - \Delta t \mathcal{L})(U^{n+1}) = M U^n$$

If the operator $\mathcal{L}$ is nonlinear, this is a nonlinear algebraic system, typically solved iteratively using a method like Newton's method. Each Newton iteration, in turn, requires the solution of a large, sparse linear system involving the Jacobian matrix.

The great advantage of this approach is its superior stability. To analyze this, we consider the scalar test equation $u' = \lambda u$ for $\lambda \in \mathbb{C}$. A [time integration](@entry_id:170891) method is called **A-stable** if its [stability region](@entry_id:178537)—the set of $z = \Delta t \lambda$ for which the numerical solution does not grow—contains the entire open left half-plane ($\mathrm{Re}(z)  0$). Backward Euler is A-stable, making it suitable for [stiff systems](@entry_id:146021) where eigenvalues $\lambda$ have large negative real parts. Explicit methods, by contrast, have [stability regions](@entry_id:166035) that are small, bounded subsets of the left half-plane.

#### Singly Diagonally Implicit Runge-Kutta (SDIRK) Methods

For higher-order implicit integration, a popular choice is the family of Singly Diagonally Implicit Runge-Kutta (SDIRK) methods. These schemes have a lower-triangular Butcher tableau with a constant value $\gamma$ on the diagonal, meaning each stage requires solving a linear system of the same form:

$$(M - \Delta t \gamma \mathcal{J}) \Delta U^{(i)} = \text{residual}^{(i)}$$

where $\mathcal{J}$ is the Jacobian of the spatial operator. This allows for reuse of matrix factorizations or [preconditioners](@entry_id:753679) across stages, improving efficiency.

A classic example is a 2-stage SDIRK method designed for [second-order accuracy](@entry_id:137876) and excellent stability , . A particularly effective version is also **stiffly accurate**, which means the final solution is identical to the last stage value, $U^{n+1} = U^{(s)}$. This property is highly desirable for stiff problems. For a 2-stage stiffly accurate SDIRK method, the stage equations for the DG system are:
1. Solve for $U^{(1)}$: $(M - \Delta t \gamma \mathcal{L})(U^{(1)}) = M U^n$
2. Solve for $U^{(2)}$: $(M - \Delta t \gamma \mathcal{L})(U^{(2)}) = M U^n + \Delta t(1-\gamma)\mathcal{L}(U^{(1)})$
3. Update: $U^{n+1} = U^{(2)}$

To satisfy the [second-order accuracy](@entry_id:137876) condition, the coefficient $\gamma$ must be a root of the quadratic equation $2\gamma^2 - 4\gamma + 1 = 0$. The two solutions are $\gamma = 1 \pm \frac{\sqrt{2}}{2}$. The choice $\gamma = 1 - \frac{\sqrt{2}}{2}$ is preferred as it leads to smaller truncation errors and ensures all RK weights are positive .

This specific method is not just A-stable, but also **L-stable**. L-stability is a stronger condition requiring that the stability function $R(z)$ satisfies $|R(z)| \le 1$ for $\mathrm{Re}(z)  0$ and additionally $\lim_{\mathrm{Re}(z) \to -\infty} |R(z)| = 0$. This means the method not only [damps](@entry_id:143944) stiff components but annihilates them in the limit of infinite stiffness. This is a direct consequence of the [stability function](@entry_id:178107) for this method, $R(z) = \frac{1+z(1-2\gamma)}{(1-z\gamma)^2}$, whose magnitude approaches zero as $|z| \to \infty$ .

#### The Challenge of Implicit Solves

The power of implicit methods comes at a significant computational cost: the need to solve large linear systems of the form $J U = F$, where $J = M + \Delta t A$ and $A$ is the stiffness matrix from the linearized spatial operator. The condition number of the DG stiffness matrix $A$ is notoriously poor, scaling badly with both $h$ and $p$. For the Symmetric Interior Penalty Galerkin (SIPG) discretization of the diffusion equation, stability requires a [penalty parameter](@entry_id:753318) that scales as $p^2/h$. This, combined with the underlying DG operator, leads to a [stiffness matrix](@entry_id:178659) whose condition number grows like $p^4/h^2$ .

Solving such [ill-conditioned systems](@entry_id:137611) requires sophisticated iterative methods (e.g., GMRES) coupled with powerful **[preconditioners](@entry_id:753679)**. A good [preconditioner](@entry_id:137537) $P$ is an approximation of the Jacobian $J$ that is cheap to invert, such that the preconditioned system $P^{-1}J U = P^{-1}F$ is much better-conditioned. Designing robust and [scalable preconditioners](@entry_id:754526) for $hp$-DG systems is a major area of research. Effective strategies often involve multilevel methods (both $h$-multigrid and $p$-[multigrid](@entry_id:172017)) and [domain decomposition](@entry_id:165934) techniques that correctly capture the local $hp$-scaling of the operator, including the face penalty terms .

### Implicit-Explicit (IMEX) Time Integration

Many physical systems, such as [advection-diffusion](@entry_id:151021) or [compressible flows](@entry_id:747589), contain a mix of stiff and non-stiff components. Treating all terms implicitly is inefficient, while treating all terms explicitly is prohibitively restrictive. Implicit-Explicit (IMEX) methods provide a tailored compromise.

The core idea is to split the spatial operator into an explicit part $\mathcal{L}_E$ and an implicit part $\mathcal{L}_I$:

$$M \frac{dU}{dt} = \mathcal{L}_E(U) + \mathcal{L}_I(U)$$

The [time integration](@entry_id:170891) scheme then treats each part differently. The simplest example is the first-order forward-backward Euler scheme:

$$M \frac{U^{n+1} - U^n}{\Delta t} = \mathcal{L}_E(U^n) + \mathcal{L}_I(U^{n+1})$$

This approach is extended to higher order via additive Runge-Kutta methods. The motivation is to place the non-stiff terms (like advection) in $\mathcal{L}_E$ and the stiff terms (like diffusion or reaction) in $\mathcal{L}_I$.

Consider a model [advection-diffusion](@entry_id:151021) problem, where the DG [semi-discretization](@entry_id:163562) leads to eigenvalues of the form $\lambda = \lambda_E + \lambda_I$, with $\lambda_E = ia$ from advection and $\lambda_I = -b$ from diffusion. Using the forward-backward Euler scheme leads to a stability function $R(z_E, z_I) = \frac{1+z_E}{1-z_I}$. The stability analysis for this scheme yields a time step restriction of the form :

$$\Delta t \le \frac{2b}{a^2-b^2} \quad (\text{for } a>b)$$

Crucially, the severe $\Delta t \sim h^2/p^4$ restriction from the diffusion term has been eliminated. The stability is now governed by the advection term, which is much less restrictive.

When applying IMEX methods to complex systems like the compressible Navier-Stokes equations, the split must be done carefully. A natural choice is to treat the convective fluxes explicitly and the viscous and heat conduction fluxes implicitly. For the resulting fully-discrete scheme to be conservative, it is essential that the splitting itself is conservative. This means that both the explicit residual operator $R_c$ and the implicit residual operator $R_v$ must individually satisfy the flux-cancellation property at element interfaces. This is achieved by using standard conservative DG formulations for each part of the split physical flux .

### Summary and Choosing a Method

The choice between explicit, implicit, and IMEX methods is a trade-off between per-step cost and stability.

- **Explicit methods** are simple to implement and have a very low cost per time step, especially on tensor-product elements using [mass lumping](@entry_id:175432) and sum factorization. They are the method of choice for purely hyperbolic problems on meshes that do not have extreme refinement. Their utility is limited by strict CFL conditions, especially for high polynomial degrees or problems with any stiffness.

- **Implicit methods** offer [unconditional stability](@entry_id:145631) (for well-chosen schemes), allowing for time steps orders of magnitude larger than explicit methods. This makes them essential for [stiff problems](@entry_id:142143) (e.g., diffusion) or for efficiently finding [steady-state solutions](@entry_id:200351). This power comes at the high cost of solving large, ill-conditioned [nonlinear systems](@entry_id:168347) at every time step.

- **IMEX methods** provide a powerful compromise for problems with mixed stiffness. By treating non-stiff terms explicitly and stiff terms implicitly, they can overcome the most restrictive stability limits while avoiding the full cost of a purely implicit solve. They are often the most efficient choice for a wide range of multi-physics problems, such as [advection-diffusion](@entry_id:151021) and [compressible fluid](@entry_id:267520) dynamics.

The break-even point between a matrix-free explicit method and a matrix-free implicit method depends on the physics and the solver. An implicit step is advantageous if the allowed increase in time step, $s = \Delta t_{\mathrm{imp}}/\Delta t_{\mathrm{exp}}$, is greater than the number of [iterative solver](@entry_id:140727) iterations, $m$, required for the implicit solve. Optimizations like sum factorization speed up both [matrix-free methods](@entry_id:145312), making high-order DG more competitive overall, but do not fundamentally alter this relative $s/m$ balance . Ultimately, the optimal choice of time integrator is inextricably linked to the physics of the problem and the available computational tools for solving the resulting algebraic systems.