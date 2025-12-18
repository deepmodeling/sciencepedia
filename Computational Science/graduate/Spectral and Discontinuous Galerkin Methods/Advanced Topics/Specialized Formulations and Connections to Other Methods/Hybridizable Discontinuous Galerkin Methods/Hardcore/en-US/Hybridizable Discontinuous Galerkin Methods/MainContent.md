## Introduction
The Hybridizable Discontinuous Galerkin (HDG) method stands as a powerful and sophisticated numerical technique within the broader family of [finite element methods](@entry_id:749389). By ingeniously combining features from discontinuous Galerkin and [mixed methods](@entry_id:163463), HDG offers a unique framework that excels in computational efficiency, accuracy, and versatility. Its significance lies in its ability to solve complex [partial differential equations](@entry_id:143134) while maintaining [local conservation](@entry_id:751393), [high-order accuracy](@entry_id:163460), and a structure that is exceptionally amenable to modern high-performance computing. This article addresses the need for a unified understanding of this method, bridging the gap between its abstract formulation and its practical application across scientific disciplines.

Over the next few sections, you will gain a deep and structured understanding of the HDG method. The journey begins in the **Principles and Mechanisms** section, which deconstructs the core formulation using a model problem, explaining the pivotal roles of the hybrid variable, [static condensation](@entry_id:176722), and superconvergence. Following this, the **Applications and Interdisciplinary Connections** section demonstrates the method's power in action, exploring its use in fluid dynamics, solid mechanics, and [multiphysics](@entry_id:164478) problems, and highlighting its connections to fields like [uncertainty quantification](@entry_id:138597) and [model order reduction](@entry_id:167302). Finally, the **Hands-On Practices** section provides targeted exercises to solidify your comprehension of key concepts, from deriving local solvers to analyzing [computational complexity](@entry_id:147058).

This structure is designed to guide you from the foundational theory to the cutting-edge applications of one of today's most innovative computational methods.

## Principles and Mechanisms

The Hybridizable Discontinuous Galerkin (HDG) method represents a significant development in the field of finite element techniques, blending ideas from classical discontinuous Galerkin (DG) and [mixed finite element methods](@entry_id:165231) to create a framework with unique computational advantages. This chapter elucidates the core principles and mechanisms of the HDG method, building from its fundamental formulation to its advanced properties such as superconvergence and its relationship with other [numerical schemes](@entry_id:752822). We will use the scalar [diffusion equation](@entry_id:145865) as a model problem to illustrate these concepts.

### Core Formulation: The Hybrid Variable and Local Problems

Let us consider a model diffusion problem on a bounded polyhedral domain $\Omega \subset \mathbb{R}^d$:
$$
- \nabla \cdot (\kappa \nabla u) = f \quad \text{in } \Omega,
$$
subject to suitable boundary conditions, where $\kappa(\boldsymbol{x})$ is a uniformly positive and bounded diffusion coefficient. The first step in formulating an HDG method is to recast this second-order equation as a first-order system by introducing the flux, $\boldsymbol{q} = -\kappa \nabla u$. This yields the system:
$$
\begin{cases}
\kappa^{-1} \boldsymbol{q} + \nabla u = \mathbf{0} \\
\nabla \cdot \boldsymbol{q} = f
\end{cases}
$$

The central innovation of the HDG method lies in its choice of discrete variables. On a mesh $\mathcal{T}_h$ of the domain $\Omega$, we introduce three distinct approximations :

1.  An element-wise, discontinuous [polynomial approximation](@entry_id:137391) $\boldsymbol{q}_h$ for the flux $\boldsymbol{q}$.
2.  An element-wise, discontinuous [polynomial approximation](@entry_id:137391) $u_h$ for the scalar field $u$.
3.  A **[hybrid trace variable](@entry_id:750438)** $\widehat{u}_h$, which is an approximation to the trace of $u$ on the mesh skeleton $\mathcal{F}_h$ (the union of all element faces).

The crucial feature of $\widehat{u}_h$ is that it is defined as a **single-valued** function on each face of the mesh . This stands in stark contrast to standard DG methods, where the trace of the solution is inherently double-valued on any interior face (one value from each of the two adjacent elements). In HDG, there is no ambiguity about the value on a face, as $\widehat{u}_h$ is the sole representation. The continuity of $\widehat{u}_h$ is not enforced; it is single-valued by its very definition in the chosen finite element space on the skeleton .

With these variables, the HDG method is constructed from two main components: a set of independent local problems on each element and a single global problem that couples them.

For any element $K \in \mathcal{T}_h$, we define a local weak formulation. Given the trace variable $\widehat{u}_h$ on the boundary $\partial K$, we seek $(\boldsymbol{q}_h, u_h)$ within $K$ that satisfy the [weak form](@entry_id:137295) of the [first-order system](@entry_id:274311). By testing against appropriate vector and scalar test functions $(\boldsymbol{v}, w)$ and integrating by parts, we obtain:
$$
\int_K \kappa^{-1} \boldsymbol{q}_h \cdot \boldsymbol{v} \, d\boldsymbol{x} - \int_K u_h (\nabla \cdot \boldsymbol{v}) \, d\boldsymbol{x} + \int_{\partial K} \widehat{u}_h (\boldsymbol{v} \cdot \boldsymbol{n}) \, dS = 0
$$
$$
- \int_K \boldsymbol{q}_h \cdot \nabla w \, d\boldsymbol{x} + \int_{\partial K} (\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n}) w \, dS = \int_K f w \, d\boldsymbol{x}
$$
Here, we have replaced the trace of $u$ in the boundary integrals with our hybrid variable $\widehat{u}_h$. Furthermore, the normal component of the flux, $\boldsymbol{q} \cdot \boldsymbol{n}$, has been replaced by a **numerical flux**, denoted $\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n}$. A common and defining choice for this [numerical flux](@entry_id:145174) is:
$$
\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n} = \boldsymbol{q}_h \cdot \boldsymbol{n} + \tau (u_h - \widehat{u}_h)
$$
The term $\tau > 0$ is a **[stabilization parameter](@entry_id:755311)**. Its role is to weakly enforce consistency between the interior solution $u_h$ and the trace solution $\widehat{u}_h$ at the element boundary. This numerical flux depends only on the variables local to the element $K$ ($\boldsymbol{q}_h, u_h$) and the shared trace variable $\widehat{u}_h$.

### Hybridization and Static Condensation

The structure of the local problems is the key to the efficiency of the HDG method. For a given trace function $\widehat{u}_h$ on the skeleton, the problem for $(\boldsymbol{q}_h, u_h)$ on each element $K$ is completely independent of all other elements. The only information an element needs from the "outside world" is the value of $\widehat{u}_h$ on its own boundary.

The element-wise solutions are coupled together through a single global transmission condition: the [numerical flux](@entry_id:145174) $\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n}$ must be conserved across interior faces. This is imposed weakly by requiring that for any test function $\mu_h$ in the space of the trace variable (vanishing on the Dirichlet boundary), the sum of the [numerical fluxes](@entry_id:752791) over all element boundaries vanishes:
$$
\sum_{K \in \mathcal{T}_h} \int_{\partial K} (\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n}) \mu_h \, dS = \int_{\Gamma_N} g_N \mu_h \, dS
$$
where $\Gamma_N$ is the Neumann boundary and $g_N$ is the prescribed Neumann data. This single equation is the only constraint that globally couples the degrees of freedom of $\widehat{u}_h$ .

This decoupling of the local problems enables a powerful algebraic procedure known as **[static condensation](@entry_id:176722)**. Because the local solutions $(\boldsymbol{q}_h, u_h)$ on an element $K$ depend linearly on the trace data $\widehat{u}_h|_{\partial K}$, we can formally solve the local system to express the degrees of freedom for $\boldsymbol{q}_h$ and $u_h$ in terms of the degrees of freedom for $\widehat{u}_h$. Substituting these expressions into the global flux conservation equation eliminates all element-interior unknowns, yielding a global linear system for the degrees of freedom of the trace variable $\widehat{u}_h$ alone. This global system is often called the **Schur complement** system .

The result is a significant reduction in the size of the globally coupled problem. Instead of solving for all degrees of freedom in the entire domain at once (as in standard DG methods), we first solve a smaller system for the interface unknowns and then recover the element-interior solutions in a final, perfectly parallelizable, element-by-element post-processing step . The variable $\widehat{u}_h$ can be interpreted as a Lagrange multiplier that weakly enforces the continuity of the [numerical flux](@entry_id:145174) across element faces .

### Distinctions from Other Finite Element Methods

The unique structure of HDG becomes clearer when contrasted with other established methods .

-   **Versus Standard DG Methods:** In a typical DG method for diffusion, the element-interior unknowns are coupled directly to the unknowns in neighboring elements through the numerical flux. The resulting global system is large, involving all degrees of freedom for $u_h$ across all elements. HDG, through its introduction of the single-valued hybrid variable $\widehat{u}_h$, avoids this direct coupling and allows for [static condensation](@entry_id:176722).

-   **Versus Classical Mixed Methods:** A classical mixed method (e.g., using Raviart-Thomas or BDM elements) also seeks approximations for both the flux $\boldsymbol{q}$ and the scalar $u$. However, it enforces normal flux continuity *strongly* by choosing the flux approximation space $\boldsymbol{V}_h$ to be a subspace of $H(\mathrm{div}; \Omega)$. This leads to a large, globally coupled saddle-point system for the degrees of freedom of both $\boldsymbol{q}_h$ and $u_h$. HDG, in contrast, uses fully discontinuous spaces and enforces flux continuity weakly via the global equation for $\widehat{u}_h$.

### Key Algorithmic Ingredients

The performance and theoretical properties of an HDG method depend critically on the choice of its constituent parts: the [polynomial spaces](@entry_id:753582) and the [stabilization parameter](@entry_id:755311).

#### Choice of Polynomial Spaces and Superconvergence

A remarkable property of HDG methods is the ability to achieve superconvergence. This requires a judicious choice of polynomial approximation spaces. For the diffusion problem, a standard choice that enables this property is to use polynomials of the same degree $k$ for all three variables :
$$
\boldsymbol{q}_h|_K \in [\mathcal{P}_k(K)]^d, \quad u_h|_K \in \mathcal{P}_k(K), \quad \widehat{u}_h|_F \in \mathcal{P}_k(F)
$$
With this choice (and sufficient solution regularity), the HDG method exhibits optimal convergence rates of $\mathcal{O}(h^{k+1})$ for all variables. However, a special property of the method is that the computed flux, $\boldsymbol{q}_h$, and trace, $\widehat{u}_h$, are particularly accurate.

This high-accuracy solution can be leveraged in a local **post-processing** step to obtain a globally discontinuous scalar approximation $u_h^\star$ that is superconvergent. On each element $K$, one finds $u_h^\star \in \mathcal{P}_{k+1}(K)$ by solving a local Neumann-type problem that uses the computed HDG solution as data :
$$
\begin{cases}
(\nabla u_h^\star, \nabla w)_K = (-\kappa^{-1}\boldsymbol{q}_h, \nabla w)_K \quad \forall w \in \mathcal{P}_{k+1}(K), \\
(u_h^\star, 1)_K = (u_h, 1)_K.
\end{cases}
$$
The first equation makes $\nabla u_h^\star$ the [best approximation](@entry_id:268380) to $-\kappa^{-1}\boldsymbol{q}_h$ in the space of gradients of $\mathcal{P}_{k+1}$ polynomials, while the second equation fixes the mean value. Because the "data" for this problem ($\boldsymbol{q}_h$ and $u_h$) are highly accurate approximations of the true solution's flux and mean, the resulting $u_h^\star$ inherits this high accuracy, achieving an optimal $L^2$ error of $\mathcal{O}(h^{k+2})$.

#### The Stabilization Parameter $\tau$

The [stabilization parameter](@entry_id:755311) $\tau$ is not arbitrary; its magnitude is crucial for the method's stability and convergence. A proper choice of $\tau$ must balance several terms that arise in the stability analysis, particularly those originating from polynomial inverse and trace inequalities. For the method to be robust with respect to both the mesh size $h$ and the polynomial degree $p=k$, the [stabilization parameter](@entry_id:755311) on a face $F$ must scale as :
$$
\tau_F \sim c \, \frac{\kappa \, p^2}{h_F}
$$
where $h_F$ is the diameter of the face and $c$ is a constant independent of $h$, $p$, and $\kappa$. The $h_F^{-1}$ dependence balances the scaling of derivatives, while the $p^2$ dependence is required to control the growth of norms of polynomials on element boundaries relative to their interior, a phenomenon captured by polynomial trace-inverse estimates.

Further insight into the nature of the HDG method can be gained by examining the limiting behavior of $\tau$ :
-   As $\boldsymbol{\tau \to 0}$, the [stabilization term](@entry_id:755314) vanishes. The [numerical flux](@entry_id:145174) becomes $\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n} = \boldsymbol{q}_h \cdot \boldsymbol{n}$, and the global equation enforces weak continuity of the physical flux $\boldsymbol{q}_h$. This is precisely the formulation of a **hybridized mixed method**. For this limit to be stable, the [polynomial spaces](@entry_id:753582) for $(\boldsymbol{q}_h, u_h)$ must form a stable mixed-element pair (satisfying the LBB condition).

-   As $\boldsymbol{\tau \to \infty}$, the [stabilization term](@entry_id:755314) dominates. For the [numerical flux](@entry_id:145174) to remain bounded, the difference $(u_h - \widehat{u}_h)$ must tend to zero. This effectively imposes a Dirichlet condition $u_h = \widehat{u}_h$ on the boundary of each element. The method becomes a **primal hybrid method**, where the global system for $\widehat{u}_h$ is formed by assembling local Dirichlet-to-Neumann maps.

### An Illustrative Example: 1D HDG for $k=0$

To make the concept of [static condensation](@entry_id:176722) concrete, let us derive the skeleton system for a 1D diffusion problem on $\Omega=(0,1)$ with a uniform mesh of size $h$, constant $\kappa$, and polynomial degree $k=0$ . Here, $q_h$ and $u_h$ are constants on each element $K_j=(x_{j-1}, x_j)$, denoted $q_j$ and $u_j$. The trace $\widehat{u}_h$ consists of values at each node, $\widehat{u}_j$. The local equations on element $K_j$ for [test functions](@entry_id:166589) $v=1, w=1$ become:
$$
h\kappa^{-1}q_j + (\widehat{u}_j - \widehat{u}_{j-1}) = 0 \implies q_j = -\frac{\kappa}{h}(\widehat{u}_j - \widehat{u}_{j-1})
$$
$$
[q_j + \tau(u_j - \widehat{u}_j)] - [q_j + \tau(u_j - \widehat{u}_{j-1})] = 0 \implies u_j = \frac{1}{2}(\widehat{u}_j + \widehat{u}_{j-1})
$$
These are the local solvers, expressing the interior unknowns $(q_j, u_j)$ in terms of the trace unknowns $(\widehat{u}_{j-1}, \widehat{u}_j)$. The global system arises from flux continuity at each interior node $x_j$: $(\widehat{q}_h\cdot n)|_{K_j} + (\widehat{q}_h\cdot n)|_{K_{j+1}} = 0$. This gives:
$$
(q_j + \tau(u_j - \widehat{u}_j)) + (-q_{j+1} + \tau(u_{j+1} - \widehat{u}_j)) = 0
$$
Substituting the expressions for the local unknowns and simplifying leads to a three-point stencil for the trace variables:
$$
(1+\frac{\alpha}{2})\widehat{u}_{j-1} - (2+\alpha)\widehat{u}_j + (1+\frac{\alpha}{2})\widehat{u}_{j+1} = 0
$$
where we have used the scaling $\tau=\alpha\kappa/h$. This equation forms the rows of the global [tridiagonal system](@entry_id:140462) for the trace variables, explicitly demonstrating how the elimination of interior variables leads to a smaller, sparser system on the mesh skeleton. The analysis of this matrix shows that its condition number scales as $\mathcal{O}(h^{-2})$, typical for 1D elliptic problems. In higher dimensions ($d \ge 2$), a key advantage of HDG emerges: the condition number of the skeleton system typically scales as $\mathcal{O}(h^{-1})$, which is better than the $\mathcal{O}(h^{-2})$ scaling of systems from standard conforming [finite element methods](@entry_id:749389).

### Summary and Equivalences

The Hybridizable Discontinuous Galerkin method offers a powerful and flexible framework for [solving partial differential equations](@entry_id:136409). Its defining features are:
-   The use of a **single-valued [hybrid trace variable](@entry_id:750438)** $\widehat{u}_h$ that decouples element-wise problems.
-   The ability to perform **[static condensation](@entry_id:176722)**, leading to a smaller, globally coupled system involving only the trace degrees of freedom.
-   The attainment of **superconvergent** solutions for the flux and trace, which can be transferred to the scalar solution via a local post-processing step.

Furthermore, HDG methods are deeply connected to other [numerical schemes](@entry_id:752822). As we have seen, the [stabilization parameter](@entry_id:755311) $\tau$ acts as a bridge between mixed and primal formulations. It can also be shown that specific choices of HDG spaces and parameters result in methods that are algebraically equivalent to certain hybridized [mixed methods](@entry_id:163463), such as those based on Brezzi-Douglas-Marini (BDM) or Raviart-Thomas (RT) elements . This reveals HDG not merely as a standalone technique, but as a unifying framework that encapsulates and generalizes concepts from across the landscape of [finite element methods](@entry_id:749389).