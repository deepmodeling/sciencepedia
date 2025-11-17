## Introduction
In the realm of numerical solutions for partial differential equations, Discontinuous Galerkin (DG) methods are prized for their [local conservation](@entry_id:751393) properties, [high-order accuracy](@entry_id:163460), and geometric flexibility. However, their primary drawback lies in the large number of globally coupled degrees of freedom, which can lead to computationally expensive [linear systems](@entry_id:147850). The Hybridizable Discontinuous Galerkin (HDG) method emerges as an elegant and powerful solution to this challenge, retaining the benefits of DG methods while drastically improving their computational efficiency. This article provides a comprehensive exploration of HDG, focusing on its primal and [mixed formulations](@entry_id:167436) and the pivotal role of [static condensation](@entry_id:176722).

Across the following chapters, you will gain a deep understanding of the HDG framework. "Principles and Mechanisms" will dissect the core concepts of hybridization, the formulation of local and global problems, and the algebraic process of [static condensation](@entry_id:176722) that lies at the heart of the method's efficiency. "Applications and Interdisciplinary Connections" will demonstrate the versatility of HDG by applying it to complex problems in fluid dynamics and wave physics, and reveal its profound connections to other major numerical theories like domain decomposition and boundary integral methods. Finally, "Hands-On Practices" will ground these concepts through guided exercises designed to build practical implementation skills. We begin by examining the fundamental principles that make the HDG method a cornerstone of modern computational engineering.

## Principles and Mechanisms

The Hybridizable Discontinuous Galerkin (HDG) method represents a significant evolution in the landscape of finite element techniques. It retains the principal advantages of standard Discontinuous Galerkin (DG) methods—such as [local conservation](@entry_id:751393), flexibility for complex geometries, and suitability for high-order polynomials—while overcoming their primary drawback: a large number of globally coupled degrees of freedom. This chapter delineates the core principles and mechanisms that enable this efficiency, focusing on the concepts of hybridization, [static condensation](@entry_id:176722), and the properties of the resulting numerical systems.

### The Hybridization Philosophy: Separating Local and Global Problems

The foundational idea of HDG is to introduce a new, auxiliary unknown that lives exclusively on the mesh skeleton, which is the collection of all element faces (or edges in two dimensions). This unknown, typically denoted as $\widehat{u}_h$, is called the **hybrid variable** or **trace variable**. Its role is to approximate the solution $u$ on the boundaries of the mesh elements.

By design, this hybrid variable becomes the sole conduit for information between adjacent elements. The original partial differential equation is consequently reformulated into two distinct sets of problems:

1.  A collection of **local problems**, one for each element $K$ in the mesh $\mathcal{T}_h$. These problems are entirely independent of one another. The solution on each element is computed using only the data from the [source term](@entry_id:269111) $f$ within that element and the values of the hybrid variable $\widehat{u}_h$ on its boundary, $\partial K$.

2.  A single **global problem**, which couples the degrees of freedom of the hybrid variable $\widehat{u}_h$ across the entire mesh skeleton. This global system is derived from physical conservation principles (e.g., continuity of flux) imposed weakly across element faces.

This decoupling is the essence of [hybridization](@entry_id:145080). It transforms a large, intricately connected system into a structure where the vast majority of computations can be performed in a perfectly parallelizable, element-by-element fashion.

### Formulations: Primal and Mixed HDG

The HDG philosophy can be applied to different formulations of the governing PDE. We will examine the two most common variants for a model second-order elliptic problem, $-\nabla \cdot (\kappa \nabla u) = f$.

#### Mixed HDG Formulation

The mixed approach begins by rewriting the second-order PDE as a first-order system. This is achieved by introducing the [diffusive flux](@entry_id:748422), $\boldsymbol{q} = -\kappa \nabla u$, as an independent variable. The system becomes:
$$
\kappa^{-1} \boldsymbol{q} + \nabla u = \boldsymbol{0}
$$
$$
\nabla \cdot \boldsymbol{q} = f
$$

In the mixed HDG method, we seek discrete approximations for both the scalar field $u$ and the vector flux $\boldsymbol{q}$ within each element, alongside the hybrid trace $\widehat{u}_h$ on the faces [@problem_id:3410450]. Let $\boldsymbol{q}_h$ and $u_h$ be polynomial approximations within an element $K$. The local [weak formulation](@entry_id:142897) on $K$ is derived by multiplying the two equations by test functions and integrating by parts. Crucially, all boundary terms that arise from integration by parts are expressed using the hybrid trace $\widehat{u}_h$ and a **[numerical flux](@entry_id:145174)**.

A canonical choice for the numerical normal flux on $\partial K$ is:
$$
\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n} = \boldsymbol{q}_h \cdot \boldsymbol{n} + \tau (u_h - \widehat{u}_h)
$$
Here, $\boldsymbol{n}$ is the outward unit normal to $\partial K$, and $\tau > 0$ is a user-defined **[stabilization parameter](@entry_id:755311)**. This parameter has units of conductivity divided by length and acts as a penalty, weakly enforcing the consistency between the interior solution $u_h$ and the trace approximation $\widehat{u}_h$. The local problem on an element $K$ is then: find $(\boldsymbol{q}_h, u_h)$ on $K$, given $\widehat{u}_h$ on $\partial K$, such that for all suitable [test functions](@entry_id:166589) $(\boldsymbol{r}, v)$:
$$
\int_K (\kappa^{-1} \boldsymbol{q}_h \cdot \boldsymbol{r} - u_h \nabla \cdot \boldsymbol{r}) \, \mathrm{d}\boldsymbol{x} + \int_{\partial K} \widehat{u}_h (\boldsymbol{r} \cdot \boldsymbol{n}) \, \mathrm{d}s = 0
$$
$$
- \int_K \boldsymbol{q}_h \cdot \nabla v \, \mathrm{d}\boldsymbol{x} + \int_{\partial K} (\boldsymbol{q}_h \cdot \boldsymbol{n} + \tau(u_h - \widehat{u}_h)) v \, \mathrm{d}s = \int_K f v \, \mathrm{d}\boldsymbol{x}
$$
The global problem is then established by enforcing the continuity of the [numerical flux](@entry_id:145174) across each interior face: the sum of $\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n}$ from the two elements sharing a face must be zero. This condition provides the equations that determine the global unknown $\widehat{u}_h$.

#### Primal HDG Formulation

The primal HDG formulation works directly with the original second-order equation, $-\nabla \cdot (\kappa \nabla u) = f$. The unknowns are the element-wise scalar approximation $u_h$ and the hybrid trace $\widehat{u}_h$ [@problem_id:3410450]. Integrating by parts against a [test function](@entry_id:178872) $v$ on an element $K$ yields:
$$
\int_K \kappa \nabla u_h \cdot \nabla v \, \mathrm{d}\boldsymbol{x} - \int_{\partial K} (\kappa \nabla u_h \cdot \boldsymbol{n}) v \, \mathrm{d}s = \int_K f v \, \mathrm{d}\boldsymbol{x}
$$
As before, the boundary integral term is replaced by a numerical flux that incorporates the hybrid variable $\widehat{u}_h$ and the [stabilization parameter](@entry_id:755311) $\tau$. A common choice for this numerical normal flux, denoted $\widehat{\boldsymbol{\sigma}}_h \cdot \boldsymbol{n}$, is:
$$
\widehat{\boldsymbol{\sigma}}_h \cdot \boldsymbol{n} = -\kappa \nabla u_h \cdot \boldsymbol{n} + \tau(u_h - \widehat{u}_h)
$$
Substituting this into the [weak form](@entry_id:137295) gives the local problem for the primal HDG method. The global system for $\widehat{u}_h$ is again formed by enforcing the continuity of this [numerical flux](@entry_id:145174) across element faces.

In contrast to both HDG formulations, standard DG methods do not introduce the independent trace variable $\widehat{u}_h$. Instead, face integrals in the weak form directly couple the degrees of freedom of $u_h$ from adjacent elements. This results in a much larger and more densely coupled global system, as all element-interior unknowns are part of the global solve. HDG's introduction of $\widehat{u}_h$ is the key that enables the separation of local and global concerns.

### The Engine of Efficiency: Static Condensation

The true computational power of HDG is unlocked by a procedure known as **[static condensation](@entry_id:176722)**. This is an algebraic elimination technique that leverages the decoupled structure of the method to dramatically reduce the size of the final linear system that must be solved.

#### The Mechanism

The core observation is that the local equations on an element $K$ define the interior unknowns (e.g., $\boldsymbol{q}_h$ and $u_h$) entirely in terms of the trace unknown $\widehat{u}_h$ on the boundary $\partial K$. This means we can, in principle, solve the local problem to express the coefficients of the interior unknowns as an explicit function of the coefficients of the trace unknown.

Let us formalize this [@problem_id:3410462]. Denote the vector of coefficients for the element-interior unknowns on $K$ by $\boldsymbol{x}$ and the vector of coefficients for the trace unknown on $\partial K$ by $\widehat{\boldsymbol{u}}$. The local problem can be written in [block matrix](@entry_id:148435) form as:
$$
K \boldsymbol{x} + R \widehat{\boldsymbol{u}} = \boldsymbol{b}
$$
where $K$ is an invertible matrix representing the coupling between interior unknowns, $R$ represents the coupling of interior unknowns to the trace, and $\boldsymbol{b}$ contains source terms. We can formally solve for $\boldsymbol{x}$:
$$
\boldsymbol{x} = K^{-1}(\boldsymbol{b} - R \widehat{\boldsymbol{u}})
$$
This equation is a **local solver**; it maps the trace data $\widehat{\boldsymbol{u}}$ to the interior solution $\boldsymbol{x}$.

The global flux conservation equation, which couples the system, also involves both $\boldsymbol{x}$ and $\widehat{\boldsymbol{u}}$. On element $K$, the contribution to the global [flux balance](@entry_id:274729) can be written as:
$$
W \boldsymbol{x} + S \widehat{\boldsymbol{u}} = \boldsymbol{h}
$$
where $\boldsymbol{h}$ is the vector of [numerical flux](@entry_id:145174) coefficients on $\partial K$. By substituting the expression for $\boldsymbol{x}$ into this [flux balance](@entry_id:274729) equation, we eliminate the interior variable:
$$
W (K^{-1}(\boldsymbol{b} - R \widehat{\boldsymbol{u}})) + S \widehat{\boldsymbol{u}} = \boldsymbol{h}
$$
Rearranging gives a system relating the fluxes $\boldsymbol{h}$ directly to the traces $\widehat{\boldsymbol{u}}$:
$$
(S - W K^{-1} R) \widehat{\boldsymbol{u}} = \boldsymbol{h} - W K^{-1} \boldsymbol{b}
$$
The matrix $\boldsymbol{S}_K = S - W K^{-1} R$ is the **local Schur complement**. It is a dense matrix that couples all trace degrees of freedom on the boundary of element $K$. The global system for the entire hybrid variable is assembled by summing up these local Schur complement contributions from every element in the mesh. The only globally coupled unknowns are those for $\widehat{u}_h$, resulting in a drastically smaller system than in standard DG methods.

#### Illustrative Example: 1D Primal HDG

To build intuition, consider the primal HDG method for the 1D Poisson equation on a single element $K=(0, h)$ with linear polynomials ($k=1$) [@problem_id:3410473]. The interior solution $u_K$ is a linear function, and the trace unknown $\widehat{u}$ consists of two values, $(\widehat{u}_0, \widehat{u}_h)$, at the endpoints. Following the [static condensation](@entry_id:176722) procedure, one can explicitly compute the local Schur complement matrix that relates the [numerical fluxes](@entry_id:752791) at the endpoints to the trace values. For a particular primal HDG formulation, this matrix takes a remarkably simple form:
$$
\boldsymbol{S}_K = \frac{1}{h} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}
$$
This is precisely the stiffness matrix of a mechanical spring or the conductance matrix of a resistor connecting the two endpoints. The parameter $\alpha_{\mathrm{eq}} = 1/h$ represents the effective stiffness (or conductance) of the element. This elegant result provides a powerful physical interpretation: [static condensation](@entry_id:176722) distills the complex behavior within an element down to a simple, intuitive relationship between boundary fluxes and boundary values. Notably, for this specific formulation, the result is independent of the [stabilization parameter](@entry_id:755311) $\tau$.

#### Physical Interpretation: The Neumann-to-Dirichlet Map

The local Schur complement can also be interpreted as a discrete **Neumann-to-Dirichlet (NtD) map**. It takes Neumann data (fluxes) at the boundary and maps them to Dirichlet data (traces) at the boundary. Consider again a 1D diffusion problem on $(0,h)$ solved with a mixed HDG method using piecewise constant basis functions [@problem_id:3410477]. The Schur complement relates the [numerical flux](@entry_id:145174) magnitude $t$ at the element endpoints to the jump in the trace values, $\Delta \widehat{u} = \widehat{u}(h) - \widehat{u}(0)$. The derived relationship is:
$$
\Delta \widehat{u} = \frac{2h}{2k + \tau h} t
$$
where $k$ is the diffusion coefficient. The continuous problem, in contrast, yields the relationship $\Delta u = \frac{h}{k} t$. The ratio of the discrete to the continuous NtD operator is:
$$
R = \frac{2k}{2k + \tau h} = \frac{1}{1 + \frac{\tau h}{2k}}
$$
This shows that the discrete operator correctly approximates the continuous one ($R \to 1$ as $h \to 0$). It also reveals the role of the [stabilization parameter](@entry_id:755311) $\tau$: it introduces a discrepancy that vanishes with [mesh refinement](@entry_id:168565). This analysis provides concrete insight into the consistency of the HDG method and the function of its parameters.

### Properties of the Condensed System

The global matrix assembled from the local Schur complements possesses several important structural properties that are crucial for the development of efficient and robust solvers.

#### Symmetry and Positive Definiteness

For self-adjoint elliptic problems, such as the Poisson equation, the global condensed matrix for the trace unknown $\widehat{u}_h$ is **Symmetric and Positive Definite (SPD)**. This is a vital property, as it guarantees a unique solution exists and allows for the use of highly efficient [iterative solvers](@entry_id:136910) like the Conjugate Gradient method.

Interestingly, this SPD property arises through different mechanisms in the primal and [mixed formulations](@entry_id:167436) [@problem_id:3410492].
*   In **primal HDG**, the underlying variational form is typically coercive. The local element operator $K$ that is inverted during [static condensation](@entry_id:176722) is itself SPD. The Schur complement of an SPD matrix is also SPD, so the resulting global system is SPD.
*   In **mixed HDG**, the local problem for $(\boldsymbol{q}_h, u_h)$ has an indefinite **saddle-point structure**. The local operator $K$ is therefore symmetric but indefinite. Despite this, a key theoretical result of HDG is that the specific structure of the method ensures the final Schur complement matrix $\boldsymbol{S}_K$ is nevertheless SPD. This robustness is a remarkable and powerful feature of the mixed HDG framework.

#### Sparsity and Bandwidth

The structure of the global condensed matrix is determined by a simple topological rule: two trace degrees of freedom are coupled (i.e., the corresponding matrix entry is non-zero) if and only if they belong to faces that are part of the boundary of a common element [@problem_id:3410516].

This implies that the **sparsity pattern** of the global matrix is identical for both primal and mixed HDG formulations, provided they use the same mesh and the same trace approximation space. The underlying graph of connections is determined by the mesh connectivity alone. Consequently, if the same numbering scheme is used for the trace unknowns, the **bandwidth** of the global matrices will also be identical. The differences between the primal and [mixed methods](@entry_id:163463) manifest only in the numerical values of the non-[zero matrix](@entry_id:155836) entries, which in turn affects properties like the condition number, but not the overall matrix structure.

### Advanced Features and Considerations

The HDG framework enables several advanced capabilities and requires attention to certain implementation details for optimal performance.

#### Superconvergence and Local Post-processing

A celebrated feature of certain HDG methods is **superconvergence**. This phenomenon occurs when a computed quantity, such as the flux $\boldsymbol{q}_h$, converges to the true solution at a rate faster than what standard approximation theory would predict for the [polynomial space](@entry_id:269905) used. For instance, for the mixed HDG method with polynomial degree $k$ spaces, the flux error often behaves as $\| \boldsymbol{q} - \boldsymbol{q}_h \|_{L^2} = \mathcal{O}(h^{k+1})$.

This highly accurate flux can be leveraged in a purely local **post-processing** step to obtain a much better approximation for the scalar solution $u$ [@problem_id:3410486]. After the global HDG system is solved and the interior solutions $(u_h, \boldsymbol{q}_h)$ are reconstructed, one can compute a new, enriched approximation $u_h^\star$ in a higher-order [polynomial space](@entry_id:269905) (e.g., $\mathcal{P}_{k+1}(K)$) on each element. This $u_h^\star$ is defined as the solution of a small, local problem that enforces two conditions:
1.  Its gradient, $\nabla u_h^\star$, provides the best possible match to the superconvergent flux $-\kappa^{-1} \boldsymbol{q}_h$ in an $L^2$ sense.
2.  Its mean value is constrained to match the mean of the original solution $u_h$, preserving [local conservation](@entry_id:751393).

The error in this post-processed solution can be shown to satisfy $\| u - u_h^\star \|_{L^2} = \mathcal{O}(h^{k+2})$. This one-order gain in accuracy, achieved via an inexpensive and fully parallelizable local computation, is one of the most attractive features of HDG.

It is critical to note, however, that this superconvergence property is not universal. It depends delicately on the choice of discrete spaces for the interior and trace variables. For example, the standard mixed HDG choice of $(\mathcal{P}_k, [\mathcal{P}_k]^d, \mathcal{P}_k)$ for $(u_h, \boldsymbol{q}_h, \widehat{u}_h)$ possesses the necessary structure (related to a concept called **M-decomposition**) to achieve this result. Other choices, such as a primal HDG method using $\mathcal{P}_k$ for both $u_h$ and $\widehat{u}_h$, may lack this structure, leading to a suboptimal flux approximation and a post-processed solution that converges at a slower rate, e.g., $\mathcal{O}(h^{k+1})$ [@problem_id:3410513].

#### Implementation: Choice of Basis Functions

The efficiency of [static condensation](@entry_id:176722) hinges on the inversion of the local matrix $K$. The choice of basis functions for the *interior* [polynomial spaces](@entry_id:753582) has a profound impact on the structure of this matrix and the cost of its inversion [@problem_id:3410506].

*   **Modal Basis**: If one uses a basis of **orthonormal polynomials** (e.g., integrated Legendre polynomials) for the interior unknowns, the local mass matrix on an affine reference element becomes a multiple of the identity matrix. Its condition number is 1, and its inverse is trivial to compute. This makes the [static condensation](@entry_id:176722) step extremely fast and numerically stable.

*   **Nodal Basis**: If one uses a standard **Lagrange nodal basis**, the corresponding mass matrix is dense and its condition number grows rapidly with the polynomial degree $p$. Inverting this [ill-conditioned matrix](@entry_id:147408) is computationally expensive and can introduce significant floating-point errors, which may contaminate the accuracy of the computed Schur complement and the final solution.

Therefore, while the final condensed system is theoretically independent of the interior basis, the practical choice is clear: modal [orthonormal bases](@entry_id:753010) are strongly preferred for the interior variables to ensure an efficient and robust [static condensation](@entry_id:176722) procedure.

#### A Caveat: Spurious Modes in Eigenvalue Problems

While [static condensation](@entry_id:176722) is highly effective for source problems, its application to other problem types, like [eigenvalue problems](@entry_id:142153), requires care. When applied to an eigenproblem $-\nabla \cdot (\kappa \nabla u) = \lambda u$, the local operator $K$ that must be inverted during [static condensation](@entry_id:176722) becomes dependent on the eigenvalue, i.e., $K(\lambda)$ [@problem_id:3410469].

The global condensed system becomes a [nonlinear eigenvalue problem](@entry_id:752640) for $\widehat{u}_h$. A computed global eigenvalue $\lambda_h$ is deemed **spurious** if it happens to be an eigenvalue of the *local* problem on any element $K$. In such a case, the local operator $K(\lambda_h)$ is singular, and the reconstruction of the interior solution $(\boldsymbol{q}_h, u_h)$ from the trace $\widehat{u}_h$ is ill-posed. The computed global mode does not correspond to a valid solution of the full discrete system.

Fortunately, there is a simple diagnostic: for each computed global eigenpair $(\lambda_h, \widehat{u}_h)$, one must attempt to solve the local reconstruction problem on every element. If the local system is found to be singular (or numerically ill-conditioned) on any element, the mode is spurious and should be discarded. This illustrates that [static condensation](@entry_id:176722), while powerful, is a formal algebraic manipulation whose validity must be re-assessed based on the structure of the underlying PDE.