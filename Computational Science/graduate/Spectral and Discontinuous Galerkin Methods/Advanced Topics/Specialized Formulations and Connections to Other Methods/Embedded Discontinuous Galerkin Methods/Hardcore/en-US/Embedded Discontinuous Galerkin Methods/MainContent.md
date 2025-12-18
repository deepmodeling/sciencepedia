## Introduction
The numerical solution of partial differential equations (PDEs) is a cornerstone of modern science and engineering, but it presents a constant trade-off between accuracy, geometric flexibility, and computational cost. Discontinuous Galerkin (DG) methods have emerged as a powerful class of techniques, celebrated for their [local conservation](@entry_id:751393) properties, robustness, and ability to handle complex geometries with high-order polynomials. However, this power comes at a significant price: a very large number of globally coupled degrees of freedom, which can make computations prohibitively expensive.

This article addresses this critical challenge by exploring the Embedded Discontinuous Galerkin (EDG) method, an advanced formulation within the hybridizable DG family designed to overcome the computational bottlenecks of traditional DG schemes. By introducing a globally continuous trace variable, EDG drastically reduces the size of the final system of equations, creating a method that marries the physical fidelity and [high-order accuracy](@entry_id:163460) of DG with the computational efficiency of classical Continuous Galerkin (CG) methods.

Across the following chapters, you will gain a deep understanding of this innovative technique. The first chapter, **Principles and Mechanisms**, will dissect the core formulation of the EDG method, explaining the [hybridization](@entry_id:145080) principle, the role of [function spaces](@entry_id:143478), and the [static condensation](@entry_id:176722) process that is key to its efficiency. Following this, **Applications and Interdisciplinary Connections** will showcase the method's versatility by applying it to challenging problems in fluid mechanics, [solid mechanics](@entry_id:164042), and wave propagation. Finally, the **Hands-On Practices** section offers a chance to solidify your knowledge by working through key theoretical and practical derivations. This journey will illuminate how EDG provides a robust, accurate, and efficient paradigm for computational modeling.

## Principles and Mechanisms

The Embedded Discontinuous Galerkin (EDG) method represents a sophisticated evolution within the family of discontinuous Galerkin methods. It is a form of **hybridizable discontinuous Galerkin (HDG)** method, engineered to retain the principal advantages of DG formulations—such as [local conservation](@entry_id:751393) and flexibility with high-order polynomials and complex geometries—while mitigating their primary drawback: a large number of globally coupled degrees of freedom. This chapter elucidates the core principles that define the EDG method, details the mechanisms by which it operates, and explores the theoretical underpinnings that govern its performance and efficiency.

### The Hybridization Principle and Motivation for EDG

At the heart of all hybridizable DG methods lies the concept of **[hybridization](@entry_id:145080)**. Instead of directly coupling the degrees of freedom (DOFs) of neighboring elements, which leads to large, sparse global systems, [hybridization](@entry_id:145080) introduces an auxiliary variable defined only on the mesh skeleton (the collection of all element faces). This new variable, often called a **trace** or **hybrid variable**, serves as the sole conduit for information between elements. The original element-interior variables can then be "condensed out" locally, a process known as **[static condensation](@entry_id:176722)**, resulting in a global system of equations posed exclusively for the trace variable.

The primary motivation for this approach is [computational efficiency](@entry_id:270255) . The size of the final linear system to be solved is determined entirely by the number of DOFs in the trace space. This is where the Embedded Discontinuous Galerkin method distinguishes itself. Whereas a standard HDG method employs a trace space that is discontinuous at the boundaries of faces (i.e., at vertices in 2D and edges in 3D), the EDG method enforces global continuity on the trace variable. This choice dramatically reduces the size of the trace space and, consequently, the size of the final global system. The resulting system's size and sparsity pattern become comparable to those of a traditional Continuous Galerkin (CG) method, representing a significant computational advantage over other DG variants .

### Core Formulation of the EDG Method

To formalize the principles of the EDG method, let us consider a [canonical model](@entry_id:148621) problem: the scalar [diffusion equation](@entry_id:145865) on a bounded Lipschitz domain $\Omega \subset \mathbb{R}^d$ :
$$
-\nabla \cdot (\kappa \nabla u) = f \quad \text{in } \Omega, \qquad u=g \quad \text{on } \partial \Omega,
$$
where $\kappa(\boldsymbol{x})$ is a uniformly positive and bounded diffusion coefficient. The first step is to rewrite this second-order equation as a first-order system by introducing the flux, $\boldsymbol{q} := -\kappa \nabla u$. This yields the pair of equations:
$$
\begin{cases}
\kappa^{-1}\boldsymbol{q} + \nabla u = \boldsymbol{0} \\
\nabla \cdot \boldsymbol{q} = f
\end{cases}
$$
The EDG formulation is constructed on an element-by-element basis. Let $\mathcal{T}_h$ be a mesh of the domain $\Omega$. On any element $K \in \mathcal{T}_h$, we multiply the two equations by [test functions](@entry_id:166589) $\boldsymbol{v}$ and $w$, respectively, and integrate by parts:
$$
(\kappa^{-1}\boldsymbol{q}, \boldsymbol{v})_K - (u, \nabla \cdot \boldsymbol{v})_K + \langle u, \boldsymbol{v} \cdot \boldsymbol{n} \rangle_{\partial K} = 0,
$$
$$
-(\boldsymbol{q}, \nabla w)_K + \langle \boldsymbol{q} \cdot \boldsymbol{n}, w \rangle_{\partial K} = (f,w)_K.
$$
Here, $(\cdot, \cdot)_K$ is the $L^2$ inner product over the element $K$, $\langle \cdot, \cdot \rangle_{\partial K}$ is the $L^2$ inner product on its boundary $\partial K$, and $\boldsymbol{n}$ is the outward unit normal on $\partial K$.

In the discrete setting, we seek approximations $(u_h, \boldsymbol{q}_h)$ in finite-dimensional [polynomial spaces](@entry_id:753582) on each element. The key innovation of hybridizable methods is to replace the exact traces $u$ and $\boldsymbol{q} \cdot \boldsymbol{n}$ on the boundary with **[numerical fluxes](@entry_id:752791)**. In the EDG framework, a new hybrid variable, $\widehat{u}_h$, is introduced to approximate the trace of $u$ on the mesh skeleton. The numerical flux for the primal variable $u$ is simply taken to be this new variable, $\widehat{u}_h$.

The numerical flux for the normal component of $\boldsymbol{q}$ is designed for [consistency and stability](@entry_id:636744). A standard choice for symmetric problems is:
$$
\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n} := \boldsymbol{q}_h \cdot \boldsymbol{n} - \tau(u_h - \widehat{u}_h)
$$
where $\tau > 0$ is a user-defined **[stabilization parameter](@entry_id:755311)** that penalizes the mismatch between the interior solution $u_h$ and the trace variable $\widehat{u}_h$. Substituting these numerical fluxes into the weak form yields the local EDG problem on each element $K \in \mathcal{T}_h$: find $(u_h|_K, \boldsymbol{q}_h|_K)$ such that for all test functions $(\boldsymbol{v}, w)$:
$$
(\kappa^{-1}\boldsymbol{q}_h, \boldsymbol{v})_K - (u_h, \nabla \cdot \boldsymbol{v})_K + \langle \widehat{u}_h, \boldsymbol{v} \cdot \boldsymbol{n} \rangle_{\partial K} = 0,
$$
$$
-(\boldsymbol{q}_h, \nabla w)_K + \langle \boldsymbol{q}_h \cdot \boldsymbol{n} - \tau(u_h - \widehat{u}_h), w \rangle_{\partial K} = (f,w)_K.
$$
These equations define the local solutions $(u_h, \boldsymbol{q}_h)$ entirely in terms of the source term $f$ and the trace variable $\widehat{u}_h$ on the boundary $\partial K$.

A crucial property of this formulation is that it is **locally conservative**. By choosing the [test function](@entry_id:178872) $w$ to be the [constant function](@entry_id:152060) $w=1$ (which is contained in standard [polynomial spaces](@entry_id:753582)), its gradient vanishes. The second equation then simplifies to:
$$
\int_{\partial K} \widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n} \, dS = \int_K f \, dV.
$$
This equation is a discrete statement of the [divergence theorem](@entry_id:145271), ensuring that the total flux exiting an element perfectly balances the source within it. This property is essential for accurately modeling conservation laws and is retained in EDG without any special effort, thanks to the structure of the weak formulation .

### Function Spaces and Degrees of Freedom

The behavior of the EDG method is dictated by the choice of discrete function spaces. For a given polynomial degree $k \ge 1$, the spaces are defined as follows :

-   **Local Scalar Space $V_h^k$**: For the primal variable $u_h$, this is the space of [discontinuous functions](@entry_id:139518) that, on each element $K$, are polynomials of total degree at most $k$. We denote this space on a single element as $P^k(K)$.

-   **Local Vector Space $\boldsymbol{W}_h^k$**: For the flux variable $\boldsymbol{q}_h$, this is the space of discontinuous vector fields whose components on each element $K$ are polynomials of total degree at most $k$. This is $[P^k(K)]^d$.

-   **Trace Space $\widehat{V}_h^k$**: For the hybrid variable $\widehat{u}_h$, this space is the defining feature of EDG. It consists of functions defined on the mesh skeleton $\mathcal{E}_h$ that are globally continuous and are polynomials of degree at most $k$ on each face $F \in \mathcal{E}_h$. Formally, $\widehat{V}_h^k \subset C^0(\mathcal{E}_h)$. This space is often constructed as the trace of a standard $H^1$-conforming continuous Lagrange finite element space on the mesh .

To make these definitions concrete, consider a 2D mesh of triangles. The number of [local basis](@entry_id:151573) functions (and thus local DOFs) for polynomial degree $k$ can be determined from first principles :
-   The dimension of the scalar space $P^k(K)$ on a triangle $K$ is $\dim(P^k(K)) = \frac{(k+1)(k+2)}{2}$.
-   The dimension of the vector space $[P^k(K)]^2$ is simply twice that of the scalar space: $\dim([P^k(K)]^2) = (k+1)(k+2)$.
-   The dimension of the trace space $P^k(e)$ on a single edge $e$ (a 1D interval) is $\dim(P^k(e)) = k+1$.

The continuity of the trace space $\widehat{V}_h^k$ is the key to creating an efficient global system.

### The Global System: Assembly and Static Condensation

The local EDG equations define the interior unknowns $(u_h|_K, \boldsymbol{q}_h|_K)$ in terms of the trace unknown $\widehat{u}_h$ on $\partial K$. The final piece of the formulation is the global equation that determines $\widehat{u}_h$. This is derived by enforcing the conservation of flux weakly across all interior faces of the mesh. Since the numerical flux $\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n}$ is single-valued on each face, the sum of its integrals over all element boundaries must vanish on the interior skeleton. This yields the global problem: find $\widehat{u}_h \in \widehat{V}_h^k$ (satisfying boundary conditions) such that for all test functions $\mu \in \widehat{V}_h^k$:
$$
\sum_{K \in \mathcal{T}_h} \langle \widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n}, \mu \rangle_{\partial K} = 0.
$$
The genius of the hybridizable framework lies in its algebraic structure . Let $x_K$ be the vector of coefficients for the interior unknowns $(u_h|_K, \boldsymbol{q}_h|_K)$ and $\lambda_K$ be the vector of coefficients for the trace unknown $\widehat{u}_h$ on $\partial K$. The local equations can be written as a block system:
$$
\begin{pmatrix} A_K  B_K \\ B_K^T  D_K \end{pmatrix}
\begin{pmatrix} x_K \\ \lambda_K \end{pmatrix}
=
\begin{pmatrix} b_K \\ g_K \end{pmatrix}.
$$
Since the interior variables $x_K$ are local to element $K$, the matrix $A_K$ is invertible. We can solve for $x_K$ from the first block row:
$$
x_K = A_K^{-1}(b_K - B_K \lambda_K).
$$
Substituting this into the second block row eliminates $x_K$ and yields a relationship solely between the trace variables and the source terms:
$$
\left( D_K - B_K^T A_K^{-1} B_K \right) \lambda_K = g_K - B_K^T A_K^{-1} b_K.
$$
The matrix $S_K := D_K - B_K^T A_K^{-1} B_K$ is the **Schur complement** of the local system. It represents the condensed [stiffness matrix](@entry_id:178659) for element $K$. The global system for the coefficients of the global trace variable $\widehat{u}_h$ is formed by assembling these local Schur complements from all elements. For coercive problems, the resulting global matrix is symmetric and [positive definite](@entry_id:149459), leading to a well-posed and efficiently solvable system.

### A Quantitative Comparison of System Size

The primary motivation for EDG—reducing the number of global unknowns—can be quantified by directly comparing the DOFs for EDG, CG, and HDG methods . For a conforming [triangulation](@entry_id:272253) of a 2D domain with $N_v$ vertices and $N_e$ elements, Euler's formula for planar graphs tells us the number of edges is $N_{edges} = N_v + N_e - 1$. The number of globally coupled DOFs for polynomial degree $k$ in each method is:

-   **EDG**: The DOFs correspond to a continuous, [piecewise polynomial](@entry_id:144637) of degree $k$ on the mesh skeleton. This gives $N_{EDG} = k N_v + (k-1)N_e - k + 1$.

-   **CG**: The DOFs correspond to a globally continuous, [piecewise polynomial](@entry_id:144637) of degree $k$ on the 2D elements. This results in $N_{CG} = k N_v + \frac{k(k-1)}{2}N_e - k + 1$.

-   **HDG**: The DOFs correspond to a discontinuous, [piecewise polynomial](@entry_id:144637) of degree $k$ on each edge, treated independently. This gives $N_{HDG} = (k+1)N_{edges} = (k+1)(N_v + N_e - 1)$.

For a typical large mesh where $N_e \approx 2N_v$ and $N_{edges} \approx 3N_v$, the number of HDG DOFs is significantly larger than for EDG and CG, whose DOF counts are of the same order. This analysis quantitatively confirms the efficiency of the EDG approach.

### The Role and Choice of the Stabilization Parameter $\tau$

The [stabilization parameter](@entry_id:755311) $\tau$ is not merely a theoretical device; it is a critical parameter that governs the stability and accuracy of the method. Its role can be understood from several perspectives.

First, it acts as a penalty parameter. In the limit as $\tau \to \infty$, the penalty term $\tau(u_h - \widehat{u}_h)$ forces the mismatch on the skeleton to zero. This effectively imposes the constraint that the trace of the discontinuous solution $u_h$ must match the continuous trace $\widehat{u}_h$. The EDG solution therefore approaches the solution of a standard Continuous Galerkin method in this limit .

Second, the penalty mechanism in EDG is closely related to that of other DG methods. Consider a 1D problem on an element of size $h$. After [static condensation](@entry_id:176722), the EDG stabilization mechanism at an interior face can be shown to be equivalent to an effective penalty on the jump of the solution, $[u_h]$. This reveals a direct relationship between the EDG stabilization $\tau$ and the penalty parameter $\sigma$ used in the Symmetric Interior Penalty Galerkin (SIPG) method: $\sigma = \frac{\tau h}{2}$ .

In practice, choosing $\tau$ to be very large leads to an ill-conditioned linear system. The optimal choice involves balancing stability requirements against conditioning. Theoretical analysis provides principled [scaling laws](@entry_id:139947) for $\tau$. For diffusion-dominated problems, stability requires $\tau$ to balance the [diffusive flux](@entry_id:748422), leading to the scaling $\tau \sim \frac{\kappa p^2}{h}$, where $p$ is the polynomial degree and $h$ is the mesh size. For [advection-dominated problems](@entry_id:746320), $\tau$ should be scaled with the local advective strength, $\tau \sim |\boldsymbol{\beta} \cdot \boldsymbol{n}|$, to provide the necessary upwind stabilization .

### Convergence Properties and Spectral Accuracy

Like other well-formulated DG methods, EDG achieves optimal convergence rates with respect to the mesh size $h$ for smooth solutions. A more profound property, particularly relevant for high-order methods, is its behavior under $p$-refinement, where the polynomial degree $k$ is increased on a fixed mesh.

For problems with analytic solutions, the EDG method can achieve **spectral (or exponential) convergence**, meaning the error decreases exponentially with $k$. This remarkable rate of convergence is contingent on three conditions :
1.  **Analyticity of the solution**: The exact solution must be analytic within each element.
2.  **Sufficiently accurate quadrature**: The integrals in the [weak formulation](@entry_id:142897) involve products of polynomials. For degree $k$ basis functions, the integrands can be polynomials of degree up to $2k$. To avoid introducing quadrature errors that would pollute the solution and destroy Galerkin orthogonality, the [quadrature rules](@entry_id:753909) must be exact for polynomials of at least this degree.
3.  **Robust stabilization**: The stability constants of the method must not degrade as $k$ increases. This requires the [stabilization parameter](@entry_id:755311) $\tau$ to be scaled appropriately, typically as $\tau \sim k^2/h$.

When these conditions are met, Céa's Lemma, combined with the exponential decay of the best polynomial approximation error for [analytic functions](@entry_id:139584), guarantees that $\|u - u_h\|_E \le C e^{-\alpha k}$ for some constants $C, \alpha > 0$, confirming [spectral convergence](@entry_id:142546).

### Summary: EDG as an $H^1$-Embedded Hybrid Method

In conclusion, the Embedded Discontinuous Galerkin method can be viewed as an **$H^1$-embedded hybrid method** . It leverages the hybridizable DG construction with discontinuous element-wise fields $(\boldsymbol{q}_h, u_h)$ but constrains the skeleton trace variable $\widehat{u}_h$ to a globally continuous space that is the trace of an $H^1$-conforming Lagrange space.

This elegant design provides a powerful synthesis:
-   It **retains [local conservation](@entry_id:751393)**, a key physical property often lost in standard CG methods.
-   It allows for **high-order polynomial approximations** on general meshes, with the potential for [spectral accuracy](@entry_id:147277).
-   Through [static condensation](@entry_id:176722), it produces a **globally coupled system of equations** whose size and structure are comparable to that of a standard CG method, making it computationally competitive.

The continuity of the trace variable $\widehat{u}_h$ is the central mechanism that "glues" the otherwise independent local solutions together, enforcing compatibility across element faces in a weak yet effective manner. By merging the most desirable features of both continuous and discontinuous Galerkin methods, EDG stands as a robust, accurate, and efficient paradigm for the numerical solution of [partial differential equations](@entry_id:143134).