## Introduction
The Discontinuous Galerkin (DG) method has emerged as a powerful technique for [solving partial differential equations](@entry_id:136409), particularly for problems dominated by convection. However, the [discretization](@entry_id:145012) of second-order operators, which govern physical processes like viscosity and diffusion, presents a significant challenge. Unlike first-order terms where [upwinding](@entry_id:756372) provides a natural stabilization, a naive application of DG principles to viscous terms often leads to unstable schemes that produce non-physical oscillations. This creates a critical knowledge gap: how can we construct a DG formulation for viscous fluxes that is consistent, conservative, and robustly stable?

This article explores an elegant and influential solution to this problem: the family of Bassi-Rebay (BR) schemes. By reformulating the second-order equation into a system of first-order equations, these methods introduce a novel mechanism to ensure stability and accuracy. Across the following chapters, you will gain a comprehensive understanding of this powerful approach.

- The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork. It introduces the first-order system formulation, explains the necessity of stabilization beyond simple central fluxes, and details the core concept of the "[lifting operator](@entry_id:751273)." This chapter culminates in a deep dive into the second Bassi-Rebay (BR2) scheme, a widely adopted method known for its robustness and algorithmic elegance.

- The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the practical power of BR schemes. We will explore their use in Computational Fluid Dynamics (CFD), their generalization to [anisotropic materials](@entry_id:184874) and curved geometries, and their fascinating connections to fields like high-performance computing, [error estimation](@entry_id:141578), and even graph theory.

- The final chapter, **Hands-On Practices**, provides an opportunity to solidify these concepts through guided exercises. You will work through the practical implementation details, analyze the stability of a complete system, and uncover the deep connections between BR2 and other DG viscous formulations.

## Principles and Mechanisms

The [discretization](@entry_id:145012) of second-order elliptic or parabolic operators, such as the Laplacian that governs diffusion and viscosity, presents a unique set of challenges within the Discontinuous Galerkin (DG) framework. Unlike first-order hyperbolic problems where [upwinding](@entry_id:756372) provides a natural and physically motivated stabilization, the treatment of viscous terms requires a more deliberate construction to ensure consistency, stability, and conservation. The Bassi-Rebay schemes offer an influential and elegant approach to this problem, centered on the idea of reconstructing a high-quality [discrete gradient](@entry_id:171970). This chapter elucidates the principles and mechanisms of this family of schemes, with a particular focus on the widely used second variant, BR2.

### The First-Order System Formulation

A common and systematic starting point for discretizing second-order operators is to reformulate the problem as a system of first-order equations. Consider, for instance, the scalar heat equation on a domain $\Omega$, partitioned by a mesh $\mathcal{T}_h$ into non-overlapping elements $K$. By introducing an auxiliary variable $\boldsymbol{q}$ to represent the flux, the equation $\partial_t u = \nabla \cdot (\kappa \nabla u)$ can be written as:

$$
\boldsymbol{q} = \nabla u
$$
$$
\partial_t u = \nabla \cdot (\kappa \boldsymbol{q})
$$

Here, $u$ is the primary scalar field (e.g., temperature), $\boldsymbol{q}$ is its gradient, and $\kappa > 0$ is the thermal conductivity, which may be spatially variable.

Within the DG method, we seek approximate solutions $u_h$ and $\boldsymbol{q}_h$ in a finite-dimensional space of discontinuous, [piecewise polynomials](@entry_id:634113) of degree at most $p$ on each element $K$. The weak formulation is derived by multiplying each equation by a suitable [test function](@entry_id:178872) ($v_h$ for the gradient equation, $\phi_h$ for the time-evolution equation) from the same [polynomial space](@entry_id:269905) and integrating over each element $K$:

$$
\int_K \boldsymbol{q}_h \cdot v_h \, d\boldsymbol{x} = \int_K (\nabla u_h) \cdot v_h \, d\boldsymbol{x}
$$
$$
\int_K (\partial_t u_h) \phi_h \, d\boldsymbol{x} = \int_K (\nabla \cdot (\kappa \boldsymbol{q}_h)) \phi_h \, d\boldsymbol{x}
$$

Applying integration by parts to the right-hand side of both equations transforms them into the canonical DG form, exposing the element boundary terms that are the hallmark of the method:

$$
\int_K \boldsymbol{q}_h \cdot v_h \, d\boldsymbol{x} = - \int_K u_h (\nabla \cdot v_h) \, d\boldsymbol{x} + \int_{\partial K} \widehat{u} (v_h \cdot \boldsymbol{n}) \, ds
$$
$$
\int_K (\partial_t u_h) \phi_h \, d\boldsymbol{x} = - \int_K \kappa \boldsymbol{q}_h \cdot (\nabla \phi_h) \, d\boldsymbol{x} + \int_{\partial K} (\kappa \widehat{\boldsymbol{q}} \cdot \boldsymbol{n}) \phi_h \, ds
$$

Here, $\boldsymbol{n}$ is the outward unit normal on the element boundary $\partial K$. The terms $\widehat{u}$ and $\widehat{\boldsymbol{q}}$ represent the **numerical fluxes** (or numerical traces), which are single-valued functions defined on the mesh skeleton that serve to couple the otherwise independent elements. The choice of these [numerical fluxes](@entry_id:752791) is the defining feature of any DG scheme and dictates its fundamental properties.

### Foundations of Numerical Fluxes for Diffusive Problems

To be viable, a [numerical flux](@entry_id:145174) must satisfy several fundamental properties. For viscous discretizations, three are paramount: **consistency**, **conservation**, and **stability**.

**Consistency** requires that for a sufficiently smooth exact solution $(u, \boldsymbol{q})$, the numerical flux reduces to the analytical flux. For example, if $u$ is continuous, we must have $\widehat{u} = u$. This ensures that in the limit of [mesh refinement](@entry_id:168565), the discrete scheme converges to the correct continuous PDE.

**Conservation** demands that the flux be single-valued across any interior face. If we consider two adjacent elements, $K^+$ and $K^-$, sharing a face $F$, the flux leaving $K^+$ through $F$ must equal the flux entering $K^-$ through $F$. This is typically achieved by designing the [numerical flux](@entry_id:145174) function to be symmetric with respect to an exchange of the left and right states.

A natural and simple choice for the numerical traces is the arithmetic average of the values from the two adjacent elements. For an interior face, we define the average as $\{\{w\}\} = \frac{1}{2}(w^+ + w^-)$. This choice for $\widehat{u}$ is not arbitrary. One can show that if we model the numerical trace as a general [linear combination](@entry_id:155091) $\widehat{u} = \omega_L u^- + \omega_R u^+$, the dual requirements of consistency ($\omega_L + \omega_R = 1$) and symmetry ($\omega_L = \omega_R$) uniquely determine the weights to be $\omega_L = \omega_R = \frac{1}{2}$ .

This leads to the **central flux** formulation, where both numerical traces are taken as averages:
$$
\widehat{u} = \{\{u_h\}\}, \quad \widehat{\boldsymbol{q}} \cdot \boldsymbol{n} = \{\{\boldsymbol{q}_h\}\} \cdot \boldsymbol{n}
$$
This choice is consistent and ensures [local conservation](@entry_id:751393). However, it harbors a critical flaw: it is **unstable**. An energy analysis, which involves setting the [test functions](@entry_id:166589) equal to the solution variables ($v_h = \boldsymbol{q}_h, \phi_h = u_h$) and summing over all elements, reveals that the central flux formulation produces no term to control the growth of discontinuities, or jumps $[[u_h]] = u_h^+ - u_h^-$, at element interfaces. The resulting semi-discrete energy equation may take the form $\frac{d}{dt} \|u_h\|^2 = -2\nu \|\boldsymbol{q}_h\|^2$, which provides no control over non-constant functions $u_h$ for which $\boldsymbol{q}_h$ might be zero or small, allowing for the unbounded growth of [spurious oscillations](@entry_id:152404) .

To remedy this, a stabilization mechanism must be introduced. One common approach is to add a penalty term to the numerical flux, such as in the Local Discontinuous Galerkin (LDG) method, where the flux for the gradient is modified to $\widehat{\boldsymbol{q}} \cdot \boldsymbol{n} = \{\{\boldsymbol{q}_h\}\} \cdot \boldsymbol{n} - \tau_F [[u_h]]$. This penalizes jumps in the solution and, with an appropriately chosen penalty parameter $\tau_F$, ensures [energy stability](@entry_id:748991) . The Bassi-Rebay schemes provide an alternative, structurally different approach to achieve the same goal.

### The Lifting Operator: A Bridge from Faces to Volumes

The central tool in the Bassi-Rebay philosophy is the **[lifting operator](@entry_id:751273)**. A [lifting operator](@entry_id:751273) is a mechanism that takes function data defined only on element faces and "lifts" it into the element's interior, producing a polynomial field defined on the element volume. Formally, for a function $\psi$ defined on the boundary $\partial K$, its lifting $\mathcal{R}(\psi)$ is a polynomial field in the element's interior that satisfies a specific weak identity.

For example, a vector-valued [lifting operator](@entry_id:751273) $\boldsymbol{r}_F$ associated with a face $F$ maps a scalar function on that face, such as the jump $[[u_h]]$, into a vector field supported on the two elements $\mathcal{N}(F)$ adjacent to $F$. Its defining property is given by the variational relation: for any [test vector](@entry_id:172985) field $\boldsymbol{\phi}_h$ in the [discrete space](@entry_id:155685),
$$
(\boldsymbol{r}_F([[u_h]]), \boldsymbol{\phi}_h)_{\mathcal{N}(F)} = -\langle [[u_h]], \{\{\boldsymbol{\phi}_h\}\}\cdot \boldsymbol{n}_F\rangle_F
$$
where $(\cdot,\cdot)_{\mathcal{N}(F)}$ is the $L^2$ inner product over the elements adjacent to $F$, and $\langle \cdot, \cdot \rangle_F$ is the $L^2$ inner product on the face $F$. The operator essentially acts as the Riesz representer of the face integral [linear functional](@entry_id:144884).

To make this abstract concept concrete, consider a one-dimensional reference element $K = [-1, 1]$ with [polynomial space](@entry_id:269905) $\mathbb{P}^1(K)$. Let's construct a scalar [lifting operator](@entry_id:751273) $r(x) \in \mathbb{P}^1(K)$ from boundary data $\psi_L = a$ at $x=-1$ and $\psi_R=b$ at $x=1$. Its defining [weak form](@entry_id:137295) is:
$$
\int_{-1}^{1} r(x) v(x) \, dx = \psi_R v(1) n_R + \psi_L v(-1) n_L = b v(1) - a v(-1)
$$
for all [test functions](@entry_id:166589) $v(x) \in \mathbb{P}^1(K)$. Since $r(x)$ is linear, we can write $r(x) = c_0 + c_1 x$. By testing with a basis for $\mathbb{P}^1(K)$, such as $\{1, x\}$, we can solve for the coefficients $c_0$ and $c_1$.
- Testing with $v(x)=1$: $\int_{-1}^{1} (c_0 + c_1 x) \cdot 1 \, dx = 2c_0$. The right side is $b(1) - a(1) = b-a$. Thus, $c_0 = \frac{b-a}{2}$.
- Testing with $v(x)=x$: $\int_{-1}^{1} (c_0 + c_1 x) \cdot x \, dx = \frac{2}{3}c_1$. The right side is $b(1) - a(-1) = b+a$. Thus, $c_1 = \frac{3}{2}(b+a)$.
The explicit lifting is therefore $r(x) = \frac{b-a}{2} + \frac{3}{2}(b+a)x$ . This demonstrates that the [lifting operator](@entry_id:751273) is simply a specific, uniquely defined polynomial constructed to satisfy a face-to-volume balance.

### The Bassi-Rebay Schemes: BR1 and BR2

The Bassi-Rebay schemes use lifting operators to construct the [discrete gradient](@entry_id:171970) $\boldsymbol{q}_h$ in a way that inherently incorporates stabilization.

#### The First Bassi-Rebay Scheme (BR1)

The original scheme, BR1, constructs the [discrete gradient](@entry_id:171970) $\boldsymbol{q}_h$ using a lifting of the difference between the interior solution trace and the average trace at the boundary. This approach uses central fluxes but lacks an explicit, tunable penalty parameter. While an improvement over the simple central flux method, BR1 is not robustly stable for all polynomial degrees and mesh types and can be inconsistent for non-constant coefficients  .

#### The Second Bassi-Rebay Scheme (BR2)

The second scheme, BR2, is a widely adopted and robust method that achieves stability by modifying the [discrete gradient](@entry_id:171970) with a lifting of the solution jump. It is algorithmically elegant and can be described by the following sequence of operations :

1.  **Compute the Broken Gradient:** In each element $K$, compute the standard element-wise (broken) gradient of the solution, $\nabla_h u_h$.

2.  **Lift the Solution Jumps:** For each interior face $F$ in the mesh, compute the jump in the solution, $[[u_h]]$, and apply the local vector-valued [lifting operator](@entry_id:751273) $\boldsymbol{r}_F$ to obtain the stabilization field $\boldsymbol{r}_F([[u_h]])$.

3.  **Form the Stabilized Gradient:** Construct a new, "stabilized" [discrete gradient](@entry_id:171970), denoted $\tilde{\boldsymbol{q}}_h$, by augmenting the broken gradient with a weighted sum of the lifted jump fields:
    $$
    \tilde{\boldsymbol{q}}_h = \nabla_h u_h + \sum_{F \in \mathcal{F}_h^{\text{int}}} \eta_F \boldsymbol{r}_F([[u_h]])
    $$
    Here, $\mathcal{F}_h^{\text{int}}$ is the set of all interior faces, and $\eta_F$ is a face-dependent [stabilization parameter](@entry_id:755311).

4.  **Discretize with the Stabilized Gradient:** Use this new gradient $\tilde{\boldsymbol{q}}_h$ in the DG [weak form](@entry_id:137295). The [numerical flux](@entry_id:145174) for the viscous term is now simply the central flux (average) of this stabilized gradient:
    $$
    \widehat{\kappa \boldsymbol{q} \cdot \boldsymbol{n}} = \kappa \{\{\tilde{\boldsymbol{q}}_h\}\} \cdot \boldsymbol{n}
    $$

This procedure elegantly embeds the jump penalty within the gradient definition itself. The scheme remains locally conservative because it uses a single-valued (average) flux, and the [lifting operator](@entry_id:751273) provides the necessary stabilization to ensure [energy stability](@entry_id:748991) .

### Analysis and Implementation of the BR2 Scheme

#### Stability and the Stabilization Parameter

The stability of the BR2 scheme hinges on the choice of the [stabilization parameter](@entry_id:755311) $\eta_F$. Its role is to make the [stabilization term](@entry_id:755314) strong enough to control unfavorable terms that arise from integration by parts. A formal stability analysis, relying on polynomial trace and inverse inequalities, reveals the necessary scaling for $\eta_F$. The analysis shows that to guarantee coercivity of the discrete bilinear form uniformly with respect to mesh size $h$ and polynomial degree $p$, the parameter must scale as  :
$$
\eta_F \propto \frac{p^2}{h_F}
$$
where $h_F$ is the characteristic size of the face $F$. This scaling ensures that the method provides a discrete energy estimate of the form $\frac{d}{dt} \|u_h\|^2 \le 0$, preventing the unphysical growth of numerical errors and guaranteeing stability .

#### Relationship to Other DG Methods

The BR2 scheme is not an isolated concept; it is closely related to other well-known DG methods for elliptic problems. In fact, for certain simplified cases, the BR2 [stabilization term](@entry_id:755314) is algebraically equivalent to the penalty term used in the Symmetric Interior Penalty Galerkin (SIPG) method. For a one-dimensional problem with piecewise linear ($p=1$) polynomials on a uniform mesh, the BR2 [stabilization term](@entry_id:755314), $\tau \sum_K \int_K r_e([[u]]) r_e([[v]]) \, dx$, can be shown to be identical to the SIPG penalty term, $\frac{\sigma}{h} \sum_e [[u]][[v]]$, provided the penalty parameters are related by $\sigma = 2\tau$ . This equivalence highlights that different DG formalisms, while appearing structurally distinct, often achieve stabilization through mathematically related mechanisms.

#### Quadrature and Accuracy

In a practical implementation, the integrals in the [weak form](@entry_id:137295) must be computed using [numerical quadrature](@entry_id:136578). To preserve the theoretical [high-order accuracy](@entry_id:163460) of the DG scheme, the [quadrature rules](@entry_id:753909) must be sufficiently exact. The required level of [exactness](@entry_id:268999) is determined by the highest polynomial degree of any integrand in the formulation. The BR2 [weak form](@entry_id:137295) involves the volume integral of $\kappa \tilde{\boldsymbol{q}}_h \cdot \nabla\phi_h$, where $\phi_h$ is a [test function](@entry_id:178872). The stabilized gradient, $\tilde{\boldsymbol{q}}_h = \nabla_h u_h + \sum \eta_F \boldsymbol{r}_F([[u_h]])$, is a polynomial of degree $p$, as it is the sum of the broken gradient (degree $p-1$) and the lifted jumps (degree $p$). The [test function](@entry_id:178872) gradient, $\nabla\phi_h$, is degree $p-1$. If the diffusion coefficient $\kappa$ is a polynomial of degree $r$, the integrand has a degree of $r+p+(p-1) = r+2p-1$. Additionally, a fully symmetric formulation of BR2 (equivalent to SIPG) contains a [stabilization term](@entry_id:755314) that is equivalent to a volume integral of $\eta_F (\boldsymbol{r}_F([[u_h]])) \cdot (\boldsymbol{r}_F([[v_h]]))$, which has a polynomial degree of $2p$. To avoid **[aliasing error](@entry_id:637691)**, which can corrupt not only accuracy but also stability, the volume [quadrature rule](@entry_id:175061) must be exact for polynomials of degree at least $\max(r+2p-1, 2p)$. For instance, with a constant diffusion coefficient ($r=0$), the rule must be exact for polynomials of degree $2p$. A Gauss-Legendre rule with $p+1$ points is exact for polynomials of degree $2p+1$, which is sufficient.

#### The Resulting Linear System

The BR2 discretization of a [steady-state diffusion](@entry_id:154663) problem results in a large sparse linear system of equations, $A \boldsymbol{U} = \boldsymbol{F}$. The properties of the matrix $A$ are crucial for selecting an efficient solver. Because the BR2 [bilinear form](@entry_id:140194) is symmetric and, with the proper stabilization, coercive, the resulting [stiffness matrix](@entry_id:178659) $A$ is **Symmetric Positive Definite (SPD)**.

This is a highly desirable property, as it permits the use of the efficient **Conjugate Gradient (CG)** [iterative method](@entry_id:147741). However, like most DG discretizations, the system is often ill-conditioned, especially for high polynomial degrees or fine meshes. Therefore, a robust preconditioner is essential. The compact stencil of the BR2 scheme (coupling is limited to immediate neighbors) makes it amenable to powerful [preconditioning techniques](@entry_id:753685) like **[algebraic multigrid](@entry_id:140593) (AMG)**. For high-order methods on tensor-product elements, matrix-free implementations using sum-factorization can further enhance efficiency, reducing the operator application cost from $\mathcal{O}(p^{2d})$ to $\mathcal{O}(p^{d+1})$ per element, where $d$ is the spatial dimension .

In summary, the Bassi-Rebay 2 scheme provides a robust, accurate, and algorithmically elegant framework for discretizing viscous and diffusive terms. By embedding stabilization directly into the [gradient reconstruction](@entry_id:749996) via local lifting operators, it achieves stability while maintaining a compact, symmetric formulation that leads to efficient and well-behaved numerical systems.