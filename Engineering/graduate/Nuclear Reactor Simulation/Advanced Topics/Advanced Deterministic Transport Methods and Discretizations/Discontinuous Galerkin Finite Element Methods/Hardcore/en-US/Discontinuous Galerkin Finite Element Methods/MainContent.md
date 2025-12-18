## Introduction
The Discontinuous Galerkin (DG) [finite element method](@entry_id:136884) has emerged as a cornerstone of modern computational science and engineering, offering a powerful and flexible framework for solving complex partial differential equations. Its significance is particularly pronounced in fields like nuclear reactor analysis, where high-fidelity simulation demands methods that are both accurate and scalable on [high-performance computing](@entry_id:169980) architectures. Traditional numerical methods, such as Continuous Galerkin (CG) or low-order Finite Volume (FV) schemes, often face limitations—CG struggles with transport-dominated problems and mesh non-conformities, while FV methods are typically difficult to extend to high order. The DG method addresses this gap by ingeniously combining the [local conservation](@entry_id:751393) properties of FV methods with the [high-order accuracy](@entry_id:163460) and geometric flexibility of finite element techniques. This article provides a comprehensive guide to understanding and applying DG methods. The journey begins with **Principles and Mechanisms**, where we deconstruct the mathematical core of DG, exploring the broken [function spaces](@entry_id:143478) and the pivotal role of [numerical fluxes](@entry_id:752791). Next, **Applications and Interdisciplinary Connections** demonstrates the method's practical power in solving complex problems in reactor physics and highlights its relevance in other fields like computational fluid dynamics. Finally, **Hands-On Practices** offers opportunities to apply these concepts through guided implementation exercises. We begin by diving into the fundamental principles that give the DG method its unique character and strength.

## Principles and Mechanisms

Having established the motivation for Discontinuous Galerkin (DG) methods in the introduction, we now delve into the principles and mechanisms that define their formulation and govern their behavior. The core strength and versatility of DG methods stem from a fundamental shift in perspective: abandoning the requirement of global continuity for the solution approximation. This section will deconstruct this idea, showing how a collection of disconnected, or "broken," element-wise approximations can be systematically and rigorously stitched together to form a highly effective numerical scheme. We will explore how this local viewpoint allows for tailored treatments of different physical phenomena—such as [neutron transport](@entry_id:159564) and diffusion—and leads to computational properties that are exceptionally well-suited for modern, large-scale reactor simulations.

### The Broken Function Space: A Local Perspective

The foundational departure of DG from traditional Continuous Galerkin (CG) [finite element methods](@entry_id:749389) lies in the choice of the discrete function space. Instead of seeking an approximate solution within a space of globally continuous functions, such as the Sobolev space $H^1(\Omega)$, the DG method operates on a much larger **broken Sobolev space**.

For a given partition, or mesh, $\mathcal{T}_h$ of the computational domain $\Omega$ into non-overlapping elements $K$, the broken [polynomial space](@entry_id:269905) for degree $p$ is defined as:
$$
V_h := \left\{ v \in L^2(\Omega) \;:\; v|_K \in \mathbb{P}^p(K) \text{ for all } K \in \mathcal{T}_h \right\}
$$
where $\mathbb{P}^p(K)$ is the space of polynomials of a specified type (e.g., total degree $p$) on element $K$. The key feature of this space is that a function $v_h \in V_h$ is a well-defined polynomial within each element, but it is not required to be continuous across the boundaries, or **faces**, between elements.

This discontinuity necessitates a new mathematical toolkit to define how information is passed between elements. Since a function $v_h$ can have two different values at a point on an interior face $F$ shared by elements $K^+$ and $K^-$, we must consider its two **traces**, $v_h^+$ and $v_h^-$, taken as the limits from the interior of $K^+$ and $K^-$, respectively. From these traces, we define two essential operators: the **jump** and the **average**.

For a scalar function $w$, the jump across face $F$ is defined with respect to a fixed [unit normal vector](@entry_id:178851) $\boldsymbol{n}$ (e.g., pointing from $K^+$ to $K^-$):
$$
[w] := w^+ - w^-
$$
For a vector function $\boldsymbol{q}$, the jump is defined as:
$$
\llbracket \boldsymbol{q} \rrbracket := \boldsymbol{q}^+ \cdot \boldsymbol{n} + \boldsymbol{q}^- \cdot (-\boldsymbol{n}) = \boldsymbol{q}^+ \cdot \boldsymbol{n} - \boldsymbol{q}^- \cdot \boldsymbol{n}
$$
A special case, frequently used in formulations, is the vector jump of a scalar, which is defined as $\llbracket w \rrbracket := w^+ \boldsymbol{n}^+ + w^- \boldsymbol{n}^-$, where $\boldsymbol{n}^+$ and $\boldsymbol{n}^-$ are the outward normals from $K^+$ and $K^-$ respectively .

The corresponding average operators are defined as:
$$
\{w\} := \frac{1}{2}(w^+ + w^-), \qquad \{\boldsymbol{q}\} := \frac{1}{2}(\boldsymbol{q}^+ + \boldsymbol{q}^-)
$$
If the exact solution to a differential equation is sufficiently smooth, its jump across any interior face will be zero. These jump and average operators are the fundamental tools that allow us to formulate inter-element coupling and enforce physical conservation laws in a weak sense.

### Deriving DG Formulations: The Numerical Flux

The derivation of any DG scheme begins by multiplying the partial differential equation (PDE) by a test function $v_h \in V_h$ and integrating over a single element $K$. Applying [integration by parts](@entry_id:136350) (Green's identities) transfers derivatives from the trial solution $u_h$ to the [test function](@entry_id:178872) $v_h$. This process yields two types of terms: an integral over the volume of the element $K$, and an integral over its boundary $\partial K$.

After summing over all elements $K \in \mathcal{T}_h$, the element boundary integrals are reorganized into a sum over all faces in the mesh. For an interior face, this sum will contain two contributions—one from each adjacent element. It is at this stage that the DG method introduces its most critical component: the **numerical flux**. The terms arising from [integration by parts](@entry_id:136350), which involve the unknown traces of the solution and its derivatives, are replaced by a uniquely defined numerical flux function, denoted $\widehat{u}$ or $\widehat{\boldsymbol{f}}(u_h)$.

The [numerical flux](@entry_id:145174) has two primary responsibilities:
1.  **Consistency**: It must be designed such that, if the exact, smooth solution of the PDE is inserted into the formula, the [numerical flux](@entry_id:145174) reduces to the true physical flux. This ensures that the numerical method does not fundamentally alter the underlying equation.
2.  **Stability**: It must be formulated to ensure the stability of the overall numerical scheme, typically by introducing dissipation or penalties that control the non-physical jumps in the solution across element faces.

The specific form of the [numerical flux](@entry_id:145174) depends intimately on the character of the underlying PDE, leading to distinct formulations for hyperbolic (transport-like) and elliptic (diffusion-like) problems.

### DG for First-Order Hyperbolic Problems: The Upwind Flux

Neutron transport is governed by the first-order linear Boltzmann equation, a hyperbolic PDE. The fundamental principle for such equations is that information propagates along characteristics, which for neutron transport are straight lines in the direction of particle motion $\boldsymbol{\Omega}$. A stable numerical method must respect this direction of information flow. This is achieved through an **upwind numerical flux** .

Consider the steady, monoenergetic transport equation:
$$
\boldsymbol{\Omega}\cdot\nabla \psi(\mathbf{x},\boldsymbol{\Omega}) + \sigma_t(\mathbf{x})\,\psi(\mathbf{x},\boldsymbol{\Omega}) = q(\mathbf{x},\boldsymbol{\Omega})
$$
After multiplying by a [test function](@entry_id:178872) $v_h$ and integrating by parts over an element $K$, the streaming term $\boldsymbol{\Omega}\cdot\nabla \psi$ gives rise to a face integral $\int_{\partial K} (\boldsymbol{\Omega} \cdot \boldsymbol{n}_K) \psi v_h \, \mathrm{d}s$. In the DG formulation, the trace of the angular flux, $\psi$, is replaced by a numerical trace $\widehat{\psi}$. The [upwind principle](@entry_id:756377) dictates that $\widehat{\psi}$ must be taken from the element from which neutrons are flowing *to* the face.

The direction of flow is determined by the sign of $\boldsymbol{\Omega} \cdot \boldsymbol{n}$, where $\boldsymbol{n}$ is the outward normal from the element in question:
*   **Outflow**: If $\boldsymbol{\Omega} \cdot \boldsymbol{n} > 0$, neutrons are leaving the element across the face. The "upwind" direction is the interior of the element.
*   **Inflow**: If $\boldsymbol{\Omega} \cdot \boldsymbol{n}  0$, neutrons are entering the element across the face. The "upwind" direction is the exterior of the element.

Based on this principle, the upwind numerical trace $\widehat{\psi}$ is defined as follows :
*   On an **interior face** $F$ between elements $K^-$ and $K^+$, with outward normal $\boldsymbol{n}^-$ from $K^-$, the [numerical flux](@entry_id:145174) used in the weak form for element $K^-$ is:
    $$
    \widehat{\psi} = \begin{cases} \psi^{-}  \text{if } \boldsymbol{\Omega}\cdot\boldsymbol{n}^{-} \ge 0 \quad (\text{outflow from } K^-) \\ \psi^{+}  \text{if } \boldsymbol{\Omega}\cdot\boldsymbol{n}^{-}  0 \quad (\text{inflow to } K^-) \end{cases}
    $$
*   On a **boundary face** $F \subset \partial\Omega$ with outward domain normal $\boldsymbol{n}$ and prescribed incident flux $\psi^{\mathrm{inc}}$:
    $$
    \widehat{\psi} = \begin{cases} \psi  \text{if } \boldsymbol{\Omega}\cdot\boldsymbol{n} \ge 0 \quad (\text{outflow from domain}) \\ \psi^{\mathrm{inc}}  \text{if } \boldsymbol{\Omega}\cdot\boldsymbol{n}  0 \quad (\text{inflow to domain}) \end{cases}
    $$

This physically motivated choice is not merely intuitive; it is essential for stability. An energy analysis shows that the [upwind flux](@entry_id:143931) introduces a non-negative dissipation term proportional to the square of the jump in the solution, $\sum_F \frac{|\boldsymbol{\Omega} \cdot \boldsymbol{n}|}{2} [ \psi_h ]^2$. This term penalizes oscillations and stabilizes the method . In stark contrast, the standard Continuous Galerkin method, which enforces continuity and has no face terms, is notoriously unstable for transport problems and requires special modifications (like SUPG/Petrov-Galerkin methods) to prevent severe, non-physical oscillations. The innate stability of the upwind DG method is one of its most significant advantages in [neutron transport](@entry_id:159564) applications .

### DG for Second-Order Elliptic Problems: The Interior Penalty Method

The neutron diffusion equation is a second-order, elliptic PDE. Its discretization requires a different approach, known as the **Interior Penalty (IP)** method. Because the operator involves a second derivative, a single integration by parts is not sufficient to symmetrically distribute derivatives between the trial and [test functions](@entry_id:166589). The IP method is derived by applying integration by parts once, introducing [numerical fluxes](@entry_id:752791), and then carefully constructing these fluxes to mimic the properties of a second [integration by parts](@entry_id:136350), while adding terms to ensure stability.

Consider the neutron diffusion equation:
$$
- \nabla \cdot \left( D(\boldsymbol{x}) \,\nabla u(\boldsymbol{x}) \right) + \Sigma_a(\boldsymbol{x}) \, u(\boldsymbol{x}) = s(\boldsymbol{x})
$$
The most common IP variant is the **Symmetric Interior Penalty Galerkin (SIPG)** method. Its [weak formulation](@entry_id:142897) seeks $u_h \in V_h$ such that for all $v_h \in V_h$, the following holds (omitting boundary terms for clarity):
$$
\sum_{K \in \mathcal{T}_h} \int_K \left( D \nabla u_h \cdot \nabla v_h + \Sigma_a u_h v_h \right) \mathrm{d}\boldsymbol{x}
- \sum_{F \in \mathcal{F}_h^{\mathrm{int}}} \int_F \left( \{ D \nabla u_h \} \cdot \llbracket v_h \rrbracket + \{ D \nabla v_h \} \cdot \llbracket u_h \rrbracket \right) \mathrm{d}s
+ \sum_{F \in \mathcal{F}_h^{\mathrm{int}}} \int_F \frac{\eta_F}{h_F} \llbracket u_h \rrbracket \cdot \llbracket v_h \rrbracket \mathrm{d}s
= \int_\Omega s v_h \mathrm{d}\boldsymbol{x}
$$
This formulation appears complex, but each term has a distinct purpose :
1.  **Element-wise Integrals**: These are the standard Galerkin terms that arise directly from the PDE.
2.  **Consistency and Symmetry Terms**: The two terms preceded by a minus sign, $-\int_F ( \{ D \nabla u_h \} \cdot \llbracket v_h \rrbracket + \{ D \nabla v_h \} \cdot \llbracket u_h \rrbracket ) \, \mathrm{d}s$, enforce consistency and symmetry. The first term ensures that the exact solution satisfies the equation. The second term, involving the test function's gradient $\nabla v_h$, is added to make the [bilinear form](@entry_id:140194) symmetric. A symmetric form leads to a [symmetric positive-definite](@entry_id:145886) stiffness matrix, which is highly desirable for solver efficiency and for achieving optimal convergence rates.
3.  **Penalty Term**: The final face term, $+\int_F \frac{\eta_F}{h_F} \llbracket u_h \rrbracket \cdot \llbracket v_h \rrbracket \, \mathrm{d}s$, is the "interior penalty." It penalizes jumps in the solution across element faces. The [penalty parameter](@entry_id:753318) $\eta_F$ must be chosen sufficiently large to counteract negative terms arising from the consistency terms in the stability analysis, thereby guaranteeing the [coercivity](@entry_id:159399) (and thus stability) of the method. The scaling with inverse face size, $h_F^{-1}$, is crucial for [consistency and convergence](@entry_id:747723).

The SIPG formulation belongs to a broader family of IP methods, which can be parameterized by a single value $\theta$ . The general consistency/symmetry term is written as $-\int_F ( \{ D \nabla u_h \cdot \boldsymbol{n} \} [v_h] + \theta \{ D \nabla v_h \cdot \boldsymbol{n} \} [u_h] ) \, \mathrm{d}s$.
*   $\theta = 1$ gives **SIPG**, which is symmetric and adjoint-consistent. This is essential for proving optimal-order error estimates in the $L^2$-norm.
*   $\theta = -1$ gives the **Non-symmetric IPG (NIPG)** method. The [bilinear form](@entry_id:140194) is not symmetric, leading to suboptimal convergence in the $L^2$-norm. However, it is [unconditionally stable](@entry_id:146281) for any [penalty parameter](@entry_id:753318) $\eta_F > 0$, whereas SIPG requires $\eta_F$ to be above a certain threshold.
*   $\theta = 0$ gives the **Incomplete IPG (IIPG)** method, which is also non-symmetric.

For most applications, the superior convergence properties of SIPG make it the preferred choice.

### DG for Advection-Diffusion Problems: A Unified Approach

Many problems in reactor physics, such as those derived from higher-order transport approximations, involve both advection (first-order) and diffusion (second-order) terms. DG methods are uniquely adept at handling these [mixed-type equations](@entry_id:167751) by simply combining the techniques described above: the advection term is discretized using an [upwind flux](@entry_id:143931), and the diffusion term is discretized using an interior penalty formulation.

An important synergy arises in this combination. Consider an advection-diffusion problem where advection is dominant (i.e., the Péclet number $\mathrm{Pe} = \frac{|a|h}{2D}$ is large). While the IP penalty term ensures the [coercivity](@entry_id:159399) of the diffusive part, the [upwind flux](@entry_id:143931) for the advective part introduces **numerical dissipation** that is critical for suppressing non-physical oscillations. A central flux for the advection term, $\widehat{f}_c = a n \{u\}$, is consistent but introduces no dissipation. An [upwind flux](@entry_id:143931), such as the Lax-Friedrichs flux $\widehat{f}_u = a n \{u\} - \frac{|a n|}{2}[u]$, adds a dissipation term to the energy balance proportional to $[u]^2$. This term, controlled by the advective speed $|a|$, effectively dampens oscillations and produces more stable, physically realistic solutions in advection-dominated regimes .

### Implementation Fundamentals

The theoretical framework of DG must be translated into a practical computational algorithm. This involves two key choices: the basis functions used to represent the solution within each element, and the [numerical quadrature](@entry_id:136578) rules used to evaluate the integrals in the [weak form](@entry_id:137295).

#### Choice of Basis Functions: Modal vs. Nodal

Within each element $K$, the solution $u_h|_K$ is a polynomial. This polynomial can be represented in different bases. The two most common choices are modal and nodal bases .

*   **Modal Bases**: The solution is represented as a sum of pre-defined polynomial basis functions, often chosen to be orthogonal. A standard choice on the [reference interval](@entry_id:912215) $[-1,1]$ is the set of **Legendre polynomials**, $\{P_k(x)\}$. If these are scaled to be orthonormal with respect to the $L^2$ inner product, i.e., $\phi_k(x) = \sqrt{\frac{2k+1}{2}} P_k(x)$, then the element-local **mass matrix**, with entries $M_{ij} = \int_K \phi_i \phi_j \, \mathrm{d}x$, becomes the identity matrix, $M_{ij} = \delta_{ij}$ . This diagonality greatly simplifies implementation, particularly for time-dependent problems or when inverting the [mass matrix](@entry_id:177093). Modal bases are also naturally hierarchical, making them ideal for spectral filtering (damping high-order modes) and for $p$-adaptive schemes where the polynomial degree can be changed easily.

*   **Nodal Bases**: The solution is represented by its values at a set of specific points within the element, called nodes. A **Lagrange basis**, $\{\ell_i(x)\}$, is constructed such that $\ell_i(\xi_j) = \delta_{ij}$ at the chosen nodes $\{\xi_j\}$. A judicious choice of nodes, such as the Gauss-Lobatto points, places nodes at the element boundaries. This significantly simplifies implementation, as evaluating the solution's trace on a face simply means accessing the corresponding nodal value, with no further computation needed .

The choice between them is a trade-off. Nodal bases simplify face evaluations and are more intuitive, but can lead to less well-conditioned matrices. Orthonormal modal bases yield optimally conditioned mass matrices and are better for adaptivity, but require evaluation to find face values. Transformations between the two bases are possible via Vandermonde-like matrices, but the conditioning of these matrices degrades with increasing polynomial degree $p$ .

#### Numerical Quadrature

The integrals in the DG [weak form](@entry_id:137295) are rarely computed analytically; they are approximated using **[numerical quadrature](@entry_id:136578)**. To preserve the theoretical accuracy of the DG method, the [quadrature rule](@entry_id:175061) must be sufficiently accurate to avoid introducing significant errors, a phenomenon known as aliasing. This means the rule must exactly integrate the polynomials that appear in the integrands.

Let's analyze the integrands for a DG method using $\mathbb{Q}_p$ polynomials (tensor-products of degree $p$ polynomials) .
*   **Element Integrals**: Terms like $D \nabla u_h \cdot \nabla v_h$ and $\Sigma_a u_h v_h$ involve products of polynomials of degree up to $p$ (for $u_h, v_h$) or their derivatives (degree $p-1$). The resulting integrand is a polynomial of degree up to $2p$ in each coordinate direction.
*   **Face Integrals**: The traces of $\mathbb{Q}_p$ functions onto faces are one-dimensional polynomials of degree $p$. Terms like $[u_h][v_h]$ or $\{\nabla u_h \cdot \boldsymbol{n}\} [v_h]$ are therefore products of 1D polynomials of degree $p$, resulting in a 1D polynomial integrand of degree up to $2p$.

A standard $N$-point Gauss-Legendre [quadrature rule](@entry_id:175061) integrates 1D polynomials of degree up to $2N-1$ exactly. To integrate a polynomial of degree $2p$ exactly, we need $2N-1 \ge 2p$, which implies $N \ge p + 1/2$. The minimum integer number of points is thus $N = p+1$.

Therefore, to avoid aliasing errors in the assembly of the DG [stiffness matrix](@entry_id:178659), one should use a **tensor-product $(p+1)$-point Gauss-Legendre rule** for element integrals and a **$(p+1)$-point Gauss-Legendre rule** for face integrals . Using a more accurate rule (e.g., with $p+2$ points) is also valid but computationally less efficient.

### Computational Characteristics of DG Methods

Finally, we compare the computational properties of the linear system $A \boldsymbol{x} = \boldsymbol{b}$ generated by DG methods with that of traditional CG methods, focusing on the implications for large-scale reactor simulation .

*   **Matrix Size and Sparsity**: For the same mesh and polynomial degree $p$, a DG method has significantly more degrees of freedom (DOFs) than a CG method, because DOFs are not shared between elements. For example, on a 2D [structured mesh](@entry_id:170596) of $N \times N$ elements of degree $p$, the DG DOF count is $N^2(p+1)^2$, while the CG count is approximately $(Np)^2$. The resulting DG matrix is much larger. Furthermore, because every element is coupled to its face-neighbors, the number of non-zero entries per row is also larger in DG.

*   **Solver Performance**: The larger size and higher density of DG matrices mean they are more expensive to work with.
    *   **Direct Solvers**: Sparse [direct solvers](@entry_id:152789) (like LU factorization) suffer from significantly more "fill-in," increasing memory and computational costs.
    *   **Iterative Solvers**: The cost per iteration of a Krylov solver (like Conjugate Gradient) is higher due to the greater number of nonzeros in the [matrix-vector product](@entry_id:151002). Moreover, the condition number of a DG matrix is typically worse than its CG counterpart, partly due to the [penalty parameter](@entry_id:753318) $\eta$. An excessively large $\eta$ severely degrades conditioning. This means an unpreconditioned DG system generally requires more iterations to converge than a CG system.

*   **Parallel Scalability**: Despite the aforementioned drawbacks, DG's greatest strength lies in its **outstanding [parallel scalability](@entry_id:753141)**. Because DOFs are local to each element, the [global stiffness matrix](@entry_id:138630) has a natural block structure. When the mesh is partitioned among many processors (domain decomposition), the only communication required is between processors sharing a domain boundary to compute the face integrals. This localized, "face-only" communication pattern is minimal and highly efficient on modern parallel architectures. This structure makes DG methods exceptionally well-suited for scalable domain decomposition [preconditioners](@entry_id:753679) (e.g., Additive Schwarz methods), which are crucial for solving the massive [linear systems](@entry_id:147850) that arise in full-core reactor simulations. This [scalability](@entry_id:636611) is often the decisive factor that makes DG the method of choice for high-performance computing in nuclear engineering .