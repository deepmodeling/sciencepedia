## Introduction
In the quest for greater accuracy and efficiency in [computational fluid dynamics](@entry_id:142614) (CFD), [high-order numerical methods](@entry_id:142601) have become indispensable tools. Among these, the Flux Reconstruction (FR) method has emerged as a particularly powerful and versatile framework. While many [high-order schemes](@entry_id:750306), such as Discontinuous Galerkin (DG) and Spectral Difference (SD), were developed with distinct formulations, a key challenge has been to understand the deep connections between them. The FR framework addresses this by providing a unifying mathematical structure that not only encompasses these methods but also offers a systematic way to analyze, design, and optimize them. This article provides a comprehensive journey into the world of Flux Reconstruction. The first chapter, **Principles and Mechanisms**, will lay the theoretical groundwork, deconstructing the method from the fundamental principle of conservation to the core idea of flux correction and exploring its unifying power. Building on this foundation, the second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the framework's practical utility in solving complex problems, from handling [curvilinear meshes](@entry_id:748122) and shock waves to enabling high-performance computing strategies. Finally, the **Hands-On Practices** chapter will offer guided exercises to translate theory into practice, solidifying your understanding of the core concepts and their implementation.

## Principles and Mechanisms

This chapter delves into the foundational principles and operational mechanisms of the Flux Reconstruction (FR) method. We transition from the conceptual overview provided in the introduction to a rigorous examination of how the framework is constructed, starting from the fundamental requirement of conservation, building the reconstruction machinery, and exploring its unification of other methods. We will then address advanced topics crucial for practical application, including the treatment of nonlinearities, viscous effects, stability analysis, and shock capturing.

### The Foundational Requirement: The Conservation Form

High-order methods that permit discontinuities at element interfaces, such as FR and Discontinuous Galerkin (DG) methods, derive their structure directly from the integral form of a conservation law. Consider a [scalar conservation law](@entry_id:754531) in one dimension:

$$
\frac{\partial u}{\partial t} + \frac{\partial f(u)}{\partial x} = 0
$$

Integrating this equation over a single computational element $I_k = [x_{k-1/2}, x_{k+1/2}]$ yields:

$$
\frac{d}{dt} \int_{x_{k-1/2}}^{x_{k+1/2}} u(x,t) \,dx + \int_{x_{k-1/2}}^{x_{k+1/2}} \frac{\partial f(u)}{\partial x} \,dx = 0
$$

Applying the Fundamental Theorem of Calculus (the one-dimensional Divergence Theorem) to the second term, we arrive at an exact statement about the rate of change of the total amount of $u$ within the element:

$$
\frac{d\bar{u}_k}{dt} \cdot \Delta x_k + f(u(x_{k+1/2}, t)) - f(u(x_{k-1/2}, t)) = 0
$$

where $\bar{u}_k$ is the element-averaged value of the solution and $\Delta x_k$ is the element width. This equation states that the time-rate-of-change of the average quantity in an element is perfectly balanced by the flux entering and leaving through its boundaries.

In a discontinuous framework, the solution approximation $u_h$ is not continuous across element boundaries. At an interface like $x_{k+1/2}$, there are two distinct solution values: the trace from the left element, $u_h(x_{k+1/2}^-)$, and the trace from the right, $u_h(x_{k+1/2}^+)$. Consequently, the physical flux $f(u_h)$ is also two-valued. To resolve this ambiguity and define a unique mechanism for inter-element communication, a **numerical flux function**, denoted $f^*$, is introduced. This function takes the two solution states at an interface, $f^*(u^-, u^+)$, and returns a single, unique flux value for that interface.

By replacing the physical flux traces with this single-valued numerical flux, the discrete balance for element $I_k$ becomes:

$$
\frac{d\bar{u}_k^h}{dt} \cdot \Delta x_k + f^*_{k+1/2} - f^*_{k-1/2} = 0
$$

This property is known as **[local conservation](@entry_id:751393)**. When we sum this equation over all elements in the domain, the [numerical flux](@entry_id:145174) terms at internal interfaces cancel in a [telescoping series](@entry_id:161657) (e.g., the $f^*_{k+1/2}$ from element $k$ cancels with the $-f^*_{k+1/2}$ from element $k+1$). This cancellation ensures that the total amount of the conserved quantity over the entire domain changes only due to fluxes at the domain's physical boundaries, a property known as **global conservation**. This entire procedure is contingent on the governing equation being expressed in the **conservation form** (or [flux form](@entry_id:273811)), as this is what allows the spatial derivative term to be integrated into a boundary [flux balance](@entry_id:274729) [@problem_id:3320599].

### The Core Idea: Correction via Reconstruction

The central mechanism of the FR framework is to construct, within each element, a new flux polynomial that is continuous and consistent with the numerical fluxes at the element boundaries. Let us examine this process in one dimension on a reference element $\xi \in [-1, 1]$ [@problem_id:3320651].

1.  **Solution Representation**: Within an element, the approximate solution $u^h(\xi)$ is represented as a polynomial of degree $p$, typically defined by its values at a set of $p+1$ **solution points**.

2.  **Discontinuous Flux**: The physical flux function $f(u)$ is applied to the solution polynomial $u^h(\xi)$ to create an initial, **discontinuous flux polynomial**, which we denote as $f^d(\xi) = f(u^h(\xi))$. This flux polynomial is generally of a higher degree than $u^h(\xi)$ if $f$ is nonlinear, and its values at the element boundaries, $f^d(-1)$ and $f^d(1)$, do not necessarily match those of its neighbors.

3.  **Flux Correction**: The goal is to "correct" $f^d(\xi)$ to create a new **reconstructed flux polynomial**, $f^r(\xi)$, such that its values at the element boundaries match the single-valued numerical fluxes, $\hat{f}_-$ and $\hat{f}_+$.
    $$
    f^r(-1) = \hat{f}_- \quad \text{and} \quad f^r(1) = \hat{f}_+
    $$
    This is achieved by adding a correction polynomial, $\delta f(\xi)$, to the discontinuous flux:
    $$
    f^r(\xi) = f^d(\xi) + \delta f(\xi)
    $$

4.  **Correction Functions**: The correction polynomial $\delta f(\xi)$ is constructed from a set of pre-defined **correction functions**. For the one-dimensional case, we need a left correction function, $g_L(\xi)$, and a right correction function, $g_R(\xi)$. These are universal polynomials of degree $p+1$ (or higher) with specific properties:
    -   $g_L(\xi)$ is 1 at the left boundary and 0 at the right: $g_L(-1)=1$, $g_L(1)=0$.
    -   $g_R(\xi)$ is 0 at the left boundary and 1 at the right: $g_R(-1)=0$, $g_R(1)=1$.

    The total correction is a linear combination of these functions, weighted by the mismatch between the numerical flux and the discontinuous flux at each boundary.
    $$
    \delta f(\xi) = \big(\hat{f}_- - f^d(-1)\big) g_L(\xi) + \big(\hat{f}_+ - f^d(1)\big) g_R(\xi)
    $$
    By construction, the correction for the left boundary vanishes at the right boundary, and vice versa, thereby isolating the corrections to their respective interfaces.

The final reconstructed flux polynomial is therefore:
$$
f^r(\xi) = f^d(\xi) + \big(\hat{f}_- - f^d(-1)\big) g_L(\xi) + \big(\hat{f}_+ - f^d(1)\big) g_R(\xi)
$$
This polynomial $f^r(\xi)$ is continuous within the element, matches the required numerical fluxes at the boundaries, and is typically of degree $p+1$. The semi-discrete update for the solution is then performed using the divergence of this reconstructed flux, e.g., in a collocation sense at the solution points.

### A Rigorous Formulation: The Semi-Discrete System

To generalize the FR methodology to multiple dimensions and establish its rigorous mathematical foundation, we return to the [weak form](@entry_id:137295) of the conservation law. For a test function $v$, the [weak form](@entry_id:137295) on a reference element $E$ is:
$$
\int_E v \left( J \partial_t u + \nabla_{\boldsymbol{\xi}} \cdot \tilde{\boldsymbol{f}} \right) d\boldsymbol{\xi} = 0
$$
where $J$ is the mapping Jacobian and $\tilde{\boldsymbol{f}}$ is the contravariant flux.

Applying the [divergence theorem](@entry_id:145271) (integration by parts) to the spatial term gives two equivalent forms for the spatial residual. The form that underpins the FR/DG framework is [@problem_id:3320643]:
$$
\int_E v (\nabla_{\boldsymbol{\xi}} \cdot \tilde{\boldsymbol{f}}^v) d\boldsymbol{\xi} + \oint_{\partial E} v ((\tilde{\boldsymbol{f}}^s - \tilde{\boldsymbol{f}}^v) \cdot \hat{\boldsymbol{n}}) dS_{\boldsymbol{\xi}}
$$
Here, $\tilde{\boldsymbol{f}}^v$ is the discontinuous volume flux polynomial, and $\tilde{\boldsymbol{f}}^s$ is the single-valued [numerical flux](@entry_id:145174) on the element boundary $\partial E$. This formulation is exceptionally insightful: it expresses the residual as the sum of a **volume contribution** (the divergence of the uncorrected interior flux) and a **surface correction** that "lifts" the flux discrepancy at the boundary into the element's interior.

When discretized using a nodal polynomial basis $\{\ell_i\}$, this weak form leads directly to the semi-discrete system of [ordinary differential equations](@entry_id:147024) for the vector of nodal solution values $\boldsymbol{u}$:
$$
M \frac{d\boldsymbol{u}}{dt} = -\boldsymbol{r}
$$
The vector $\boldsymbol{r}$ is the residual, and its components are given by the discretized weak form. The final matrix-vector expression for the residual is:
$$
\boldsymbol{r} = \sum_{k=1}^{d} S_k \tilde{\boldsymbol{f}}_k^v + \sum_{f=1}^{N_{faces}} B_f \left( \sum_{k=1}^{d} \hat{n}_{f,k} (\tilde{\boldsymbol{f}}_{k,f}^s - \tilde{\boldsymbol{f}}_{k,f}^v) \right)
$$
In this equation:
-   $d$ is the number of spatial dimensions.
-   $\tilde{\boldsymbol{f}}_k^v$ is the vector of nodal values of the $k$-th component of the interior contravariant flux.
-   $(\tilde{\boldsymbol{f}}_{k,f}^s - \tilde{\boldsymbol{f}}_{k,f}^v)$ is the vector of nodal values of the flux jump on face $f$.
-   $S_k$ are the **stiffness matrices**, arising from the volume term $\int_E \ell_i \partial_{\xi_k} \ell_j d\boldsymbol{\xi}$.
-   $B_f$ are the **face lifting matrices**, arising from the surface integral term $\int_{\partial E_f} \ell_i \ell_{\mu}^{(f)} dS_{\boldsymbol{\xi}}$, which project the face-based flux jump into the element volume.

This equation is the computational heart of the FR method. It explicitly shows how the solution evolves due to both the interior dynamics (via $S_k$) and the inter-element coupling enforced through the boundary corrections (via $B_f$).

### The Power of a Unifying Framework

The true power of Flux Reconstruction lies in its generality. By varying the three key components—the locations of the solution points, the locations of the **flux points** (points where the flux is defined or corrected), and the definition of the correction functions—the FR framework can recover a wide variety of existing [high-order schemes](@entry_id:750306).

#### Recovering the Spectral Difference Method

A prime example of FR's unifying nature is its connection to the **Spectral Difference (SD) method** [@problem_id:3320607]. The SD method is formulated differently, starting with distinct sets of solution points and flux points. Within an element, a global flux polynomial $Q(\xi)$ of degree $p+1$ is constructed to directly interpolate known flux values at $p+2$ flux points. These flux points typically consist of the two element interfaces and $p$ interior points. The flux values used for interpolation are the [numerical fluxes](@entry_id:752791) at the interfaces and the physical flux $f(u^h)$ at the interior flux points.

This entire SD procedure can be shown to be equivalent to a specific choice within the FR framework. If we identify the FR reconstructed flux $f^r(\xi)$ with the SD global flux interpolant $Q(\xi)$, we establish a direct link. The semi-discrete update in a collocation scheme is given by the derivative of the reconstructed flux evaluated at the solution points $\xi_i$:
$$
\frac{du_i}{dt} = -\frac{1}{J_e} \left. \frac{d}{d\xi} f^r(\xi) \right|_{\xi=\xi_i}
$$
By setting $f^r(\xi) \equiv Q(\xi)$, where $Q(\xi) = \sum_{m=0}^{p+1} \phi_m(\xi) \hat{f}_m$ is the Lagrange interpolant over the flux points, the update becomes:
$$
\frac{du_i}{dt} = -\frac{1}{J_e} \sum_{m=0}^{p+1} \phi'_m(\xi_i) \hat{f}_m
$$
This demonstrates that the SD scheme is a member of the FR family, corresponding to a particular method of defining the reconstructed flux.

#### Tuning Scheme Properties via Correction Functions

The correction functions $g_L(\xi)$ and $g_R(\xi)$ are not unique; any polynomial of degree $p+1$ or higher satisfying the boundary constraints can be used. This freedom provides a powerful mechanism for tuning the numerical properties of the scheme, such as its dispersion and dissipation characteristics.

For instance, one can define a family of correction functions parameterized by a constant $\kappa$. By performing a von Neumann stability analysis, we can derive the scheme's amplification and phase speed errors as a function of this parameter $\kappa$ [@problem_id:3320645]. This allows a designer to select a value of $\kappa$ that optimizes the scheme for a specific purpose. For example, one could choose $\kappa$ to minimize the phase error for a particular range of wavenumbers, or to introduce a certain amount of dissipation to damp high-frequency oscillations. A hypothetical design criterion might be to perfectly match the exact continuum phase speed at the highest resolvable [wavenumber](@entry_id:172452) ($\theta = \pi$), which yields a specific value for $\kappa$ (e.g., $\kappa = (1+\pi^2)/16$ for a particular $p=1$ scheme). This tunability is a hallmark of the FR framework, transforming it from a fixed method into a flexible design tool.

### Advanced Mechanisms for Practical Applications

While the core principles provide a complete foundation, deploying FR methods for complex real-world problems in computational fluid dynamics requires addressing several advanced topics.

#### Nonlinear Fluxes: Aliasing and Stability

When the flux function $f(u)$ is nonlinear (e.g., the $u^2/2$ flux in the Burgers' equation), a new challenge arises: **polynomial [aliasing](@entry_id:146322)** [@problem_id:3320620]. If the solution approximation $u_h$ is a polynomial of degree $p$, a nonlinear flux like $f(u_h) = (u_h)^m$ results in a polynomial of degree $mp$. Standard FR methods that project this high-degree polynomial back into the degree-$p$ space via interpolation can misrepresent the energy in the higher modes, folding it back into the lower modes. This [aliasing](@entry_id:146322) effect can introduce spurious energy and lead to catastrophic [numerical instability](@entry_id:137058).

Two primary strategies exist to combat this:

1.  **De-aliasing by Over-integration**: One can use an $L^2$ projection instead of interpolation to define the flux polynomial. This requires computing inner products of the form $\int \phi_i f(u_h) dx$. To prevent [aliasing](@entry_id:146322), these integrals must be computed exactly. A Gauss-Legendre quadrature rule with $N_q$ points is exact for polynomials of degree up to $2N_q-1$. For a flux $f(u_h) = (u_h)^m$ and basis functions $\phi_i \in \mathbb{P}^p$, the integrand $\phi_i f(u_h)$ has a degree of $(m+1)p$. Therefore, to eliminate [aliasing](@entry_id:146322), the number of quadrature points must satisfy $2N_q - 1 \ge (m+1)p$, which means a minimum of $N_q = \lceil \frac{(m+1)p+1}{2} \rceil$ points are needed. This procedure is often called **over-integration**.

2.  **Split-Form Discretizations**: An alternative and often more robust approach is to modify the discretization of the nonlinear term itself. So-called **split forms** rewrite the volume integral term $\int v \nabla \cdot f(u_h) dx$ in a symmetric or skew-symmetric way that discretely mimics the energy or [entropy conservation](@entry_id:749018) properties of the continuous PDE. For example, for a quadratic entropy, one can construct an entropy-conservative [numerical flux](@entry_id:145174) that, when used to build the discrete operator, guarantees that the [volume integrals](@entry_id:183482) do not spuriously generate entropy, thereby ensuring stability.

#### Viscous and Diffusive Phenomena

To solve the Navier-Stokes equations, one must accurately discretize second-order viscous and diffusive terms like $\nu u_{xx}$. Within the FR framework, this is typically handled using a **Local Discontinuous Galerkin (LDG)** approach [@problem_id:3320640]. The second-order equation is rewritten as a system of first-order equations by introducing an auxiliary variable for the gradient, $q = u_x$. The FR methodology is then applied to this [first-order system](@entry_id:274311).

The choice of [numerical fluxes](@entry_id:752791) for this system gives rise to different schemes with varying stability properties and computational costs. Two classic examples are:
-   **Bassi-Rebay 1 (BR1)**: This scheme uses simple averaging for all numerical fluxes. An energy analysis reveals that it is stable without any additional penalty terms. However, its computational stencil is non-compact, coupling an element to its second-nearest neighbors, which increases communication overhead.
-   **Bassi-Rebay 2 (BR2)**: This scheme, a variant of the Symmetric Interior Penalty Galerkin (SIPG) method, uses a more sophisticated [numerical flux](@entry_id:145174) for the gradient that includes a **penalty term** proportional to the jump in the solution, $\llbracket u \rrbracket$. This penalty term introduces dissipation at the element interfaces, directly controlling solution jumps and ensuring [robust stability](@entry_id:268091). The required [penalty parameter](@entry_id:753318) must scale like $(p+1)^2/h$ to guarantee stability for all $p$ and $h$. A key advantage of BR2 is that it results in a **compact stencil**, coupling only immediate neighbors.

#### Numerical Stability and Element Geometry

For time-dependent problems solved with an [explicit time-stepping](@entry_id:168157) scheme, the maximum allowable time step $\Delta t$ is limited by the Courant-Friedrichs-Lewy (CFL) condition. This condition is directly related to the **[spectral radius](@entry_id:138984)** (largest eigenvalue magnitude) of the semi-discrete spatial operator, $\rho(\mathbf{L}_{\text{phys}})$.

The spectral radius of the physical operator is influenced by the physical parameters of the problem (e.g., advection speed) and the geometry of the computational mesh [@problem_id:3320633]. Through a coordinate transformation from the physical element to the reference element, one can derive how $\rho(\mathbf{L}_{\text{phys}})$ scales. For a 2D [linear advection](@entry_id:636928) problem on an anisotropic [quadrilateral element](@entry_id:170172) with side lengths $h_x$ and $h_y$, the spectral radius is given by:
$$
\rho_{\text{phys}} = 2 \left( \frac{|a_x|}{h_x} + \frac{|a_y|}{h_y} \right) \rho_{\text{ref}}(p)
$$
where $\rho_{\text{ref}}(p)$ is the spectral radius of the 1D reference operator. This formula clearly shows that the stability limit is most constrained by the smallest element dimension in the direction of flow. Highly stretched or **anisotropic** elements can therefore impose severe time step restrictions, a critical consideration in practical [mesh generation](@entry_id:149105) and simulation.

#### Handling Discontinuities: Filtering and Conservation

A well-known challenge for [high-order methods](@entry_id:165413) is the appearance of non-physical Gibbs oscillations near sharp gradients or shocks. A common remedy is to apply a **filter** to the solution, which selectively damps the high-frequency modal content within an element.

However, indiscriminate filtering can be problematic [@problem_id:3320621]. A filter operator $S$ does not generally commute with the FR correction operator $C$. Filtering the solution can alter its values at the element faces, thereby changing the [numerical fluxes](@entry_id:752791) and breaking the delicate inter-element [flux balance](@entry_id:274729) that guarantees conservation.

A more sophisticated and conservative approach is to use a **hybrid shock-capturing strategy**:
1.  A **shock sensor** is used to identify "troubled" cells containing discontinuities.
2.  In these cells, a modal filter is activated.
3.  Critically, the filter is restricted to act only on the **bubble subspace**—the space of polynomials that are zero on all element faces. By not affecting the polynomial modes that contribute to the face values, the filter preserves the element's trace.
4.  If the filter also preserves the element's mean (the 0-th mode), it modifies the solution's shape *within* the element without altering its total mass or the fluxes it communicates to its neighbors.

This strategy effectively suppresses oscillations where needed while rigorously maintaining both local and global conservation, representing a state-of-the-art technique for robust high-order simulations.

#### Mathematical Well-Posedness of Reconstruction

Finally, a brief technical point on the reconstruction process itself is warranted. The construction of the reconstructed flux, whether through correction functions or through a global interpolant as in the SD method, relies on a well-posed linear algebraic system. For example, constructing a degree-$(p+1)$ flux polynomial from its values at $p+2$ distinct flux points is equivalent to solving a Vandermonde system [@problem_id:3320601]. The determinant of a Vandermonde matrix is non-zero if and only if all the points are distinct. This guarantees that the reconstruction operator is invertible (for a square system) or has full column rank, ensuring that a unique reconstructed flux polynomial always exists. This condition—the use of distinct flux points—is a fundamental requirement for the FR framework to be well-defined.