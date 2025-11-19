## Introduction
Discontinuous Galerkin (DG) methods have emerged as a versatile and powerful class of numerical techniques for [solving partial differential equations](@entry_id:136409), bridging the gap between finite element and [finite volume methods](@entry_id:749402). Traditional methods often struggle with complex geometries, discontinuous phenomena like [wave propagation](@entry_id:144063) across sharp interfaces, or achieving high efficiency on parallel computers due to strict global continuity requirements. The DG method addresses this knowledge gap by relaxing the continuity constraint, opening up a new framework for [high-order accuracy](@entry_id:163460) and remarkable flexibility. This article serves as a comprehensive guide to understanding and applying DG methods. In the first chapter, **Principles and Mechanisms**, we will deconstruct the core theory, exploring the broken [function spaces](@entry_id:143478), numerical fluxes, and stabilization techniques that define the method. Following this theoretical foundation, **Applications and Interdisciplinary Connections** will showcase the method's prowess in solving challenging problems in [geophysics](@entry_id:147342), seismology, and materials science. Finally, the **Hands-On Practices** chapter will provide an opportunity to solidify these concepts through guided exercises, transitioning theory into practical skill. We begin our exploration by delving into the fundamental principles that give the DG method its distinctive power.

## Principles and Mechanisms

The Discontinuous Galerkin (DG) method represents a powerful class of numerical techniques for [solving partial differential equations](@entry_id:136409), blending features of both finite element and [finite volume methods](@entry_id:749402). Its defining characteristic is the use of approximation spaces that permit discontinuities across element boundaries. This seemingly simple departure from the required continuity in standard [finite element methods](@entry_id:749389) grants DG methods several advantageous properties, including [local conservation](@entry_id:751393), [high-order accuracy](@entry_id:163460) on complex geometries, and a high degree of parallelizability. This chapter elucidates the fundamental principles and mechanisms that underpin the DG framework.

### The Discontinuous Galerkin Philosophy: Broken Spaces and Weak Enforcement

Traditional continuous Galerkin (CG) [finite element methods](@entry_id:749389) are founded upon trial and test function spaces that are subspaces of global Sobolev spaces, such as $H^1(\Omega)$. A critical implication of this choice is that the functions are globally continuous, ensuring that their **trace**, or value on an interface between two elements, is single-valued [almost everywhere](@entry_id:146631). Continuity is thus strongly enforced by the construction of the [function space](@entry_id:136890) itself [@problem_id:3584974].

The DG method begins by relaxing this constraint. Instead of a single, globally-defined function space, we consider a collection of local function spaces defined on a mesh $\mathcal{T}_h$ partitioning the domain $\Omega$. The DG trial and [test functions](@entry_id:166589) are chosen from a **broken Sobolev space**, typically denoted $H^1(\mathcal{T}_h)$. This space is formally defined as the set of functions which are square-integrable on the global domain $\Omega$ and whose restriction to each individual element $K \in \mathcal{T}_h$ belongs to the classical Sobolev space $H^1(K)$:
$$
H^1(\mathcal{T}_h) = \{ v \in L^2(\Omega) : v|_K \in H^1(K) \text{ for each } K \in \mathcal{T}_h \}
$$
The crucial difference is that functions in $H^1(\mathcal{T}_h)$ are not required to be continuous across the boundaries of the elements $K$. Consequently, at any interior face $F$ shared by two elements $K^+$ and $K^-$, a function $v_h \in H^1(\mathcal{T}_h)$ generally possesses two distinct traces, denoted $v_h^+$ and $v_h^-$.

This double-valued nature of the solution at interfaces necessitates a new language for inter-element communication. We define two fundamental operators at each interior face: the **average** $\{\!\{\cdot\}\!\}$ and the **jump** $\llbracket \cdot \rrbracket$. For a scalar function $v$, they are defined as:
$$
\{\!\{v\}\!\} = \frac{1}{2}(v^+ + v^-) \qquad \text{and} \qquad \llbracket v \rrbracket = v^+ \mathbf{n}^+ + v^- \mathbf{n}^-
$$
where $\mathbf{n}^+$ and $\mathbf{n}^-$ are the outward unit normal vectors for elements $K^+$ and $K^-$, respectively. Note that on an interior face, $\mathbf{n}^- = -\mathbf{n}^+$. If we fix one normal direction, say $\mathbf{n} = \mathbf{n}^+$, the jump of a scalar simplifies to $\llbracket v \rrbracket = v^+ - v^-$ (up to a sign convention). For a vector function $\mathbf{v}$, the definitions are analogous.

In the DG framework, inter-[element continuity](@entry_id:165046) is not imposed *a priori* by the function space. Instead, it is enforced *weakly* through the [variational formulation](@entry_id:166033) itself. This is achieved by designing special coupling terms, known as **[numerical fluxes](@entry_id:752791)**, which serve to penalize the jumps in the solution and drive them towards zero as the mesh is refined, thereby ensuring convergence to the physically continuous, correct solution [@problem_id:3584974]. The power of the DG method lies in the great flexibility offered by the design of these numerical fluxes.

### Formulation for Hyperbolic Problems: The Advection Equation

Hyperbolic conservation laws, which model transport phenomena like [wave propagation](@entry_id:144063), are a natural fit for the DG method. We illustrate the core derivation using the one-dimensional [linear advection equation](@entry_id:146245) with constant positive speed $a > 0$:
$$
\frac{\partial u}{\partial t} + a \frac{\partial u}{\partial x} = 0
$$
To construct the DG [semi-discretization](@entry_id:163562), we seek an approximate solution $u_h$ that is a [piecewise polynomial](@entry_id:144637) within each element $K_i$ of a mesh $\mathcal{T}_h$. The process begins by multiplying the PDE by a test function $v_h$ from the same broken [polynomial space](@entry_id:269905) and integrating over a single element $K_i$ [@problem_id:3584931]:
$$
\int_{K_i} \left( \frac{\partial u_h}{\partial t} + a \frac{\partial u_h}{\partial x} \right) v_h \, dx = 0
$$
Applying [integration by parts](@entry_id:136350) to the spatial derivative term transfers the derivative from the (potentially discontinuous) [trial function](@entry_id:173682) $u_h$ to the smooth [test function](@entry_id:178872) $v_h$:
$$
\int_{K_i} \frac{\partial u_h}{\partial t} v_h \, dx - \int_{K_i} a u_h \frac{\partial v_h}{\partial x} \, dx + \left[ a u_h v_h \right]_{\partial K_i} = 0
$$
The boundary term, evaluated at the element endpoints $x_{i+1/2}$ and $x_{i-1/2}$, becomes $a u_h(x_{i+1/2}^-) v_h(x_{i+1/2}^-) - a u_h(x_{i-1/2}^+) v_h(x_{i-1/2}^+)$. Here lies the central challenge and innovation of DG: the flux $a u_h$ at the interface is not uniquely defined.

The DG method resolves this ambiguity by replacing the physical flux trace $a u_h$ at the element boundaries with a **[numerical flux](@entry_id:145174)**, denoted $\widehat{au_h}$, which is a single-valued function determined by the states on both sides of the interface ($u_h^-$ and $u_h^+$). The [weak form](@entry_id:137295) becomes:
$$
\int_{K_i} \frac{\partial u_h}{\partial t} v_h \, dx - \int_{K_i} a u_h \frac{\partial v_h}{\partial x} \, dx + \widehat{au_h}|_{x_{i+1/2}} v_h(x_{i+1/2}^-) - \widehat{au_h}|_{x_{i-1/2}} v_h(x_{i-1/2}^+) = 0
$$
A physically motivated and widely used choice for hyperbolic problems is the **[upwind flux](@entry_id:143931)**. It recognizes that for $a > 0$, information propagates from left to right. Therefore, the flux at an interface should be determined by the state on the "upwind" side, which is the left side. For an interior interface at $x_{i+1/2}$, the [upwind flux](@entry_id:143931) is $\widehat{au_h} = a u_h(x_{i+1/2}^-)$. At an inflow boundary (e.g., $x_L$), the upwind state is given by the boundary data $g(t)$, so $\widehat{au_h} = a g(t)$ [@problem_id:3584931].

By summing the element-wise weak forms over all elements in the mesh, we obtain the global semi-discrete system. The interface terms elegantly couple adjacent elements, with the contribution at an interior interface $x_{i+1/2}$ being $\widehat{au_h}(v_h^- - v_h^+) = \widehat{au_h} \llbracket v_h \rrbracket$. This formulation is locally conservative and provides a robust framework for simulating advective transport.

### Formulation for Elliptic Problems: The Diffusion Equation and Interior Penalty Methods

The formulation for second-order elliptic problems, such as the [steady-state diffusion](@entry_id:154663) equation $-\nabla \cdot (\kappa \nabla u) = f$, requires a different approach. A simple upwind-like flux is insufficient. Instead, a family of methods known as **Interior Penalty (IP)** methods are commonly used.

The most prevalent of these is the **Symmetric Interior Penalty Galerkin (SIPG)** method. The derivation again begins with element-wise integration by parts, which yields a volume term and a boundary integral involving the normal flux, $\mathbf{q} \cdot \mathbf{n} = -\kappa \nabla u \cdot \mathbf{n}$. To construct the scheme, we must define [numerical fluxes](@entry_id:752791) for both the solution $u$ and the physical flux $\mathbf{q}$. For consistency, these are typically based on averages: $\widehat{u}_h = \{\!\{u_h\}\!\}$ and $\widehat{\mathbf{q}}_h = \{\!\{\mathbf{q}_h\}\!\}$.

The SIPG formulation is constructed to be consistent with the original PDE and symmetric, which is desirable for self-adjoint problems. A direct derivation leads to a bilinear form $a_h(u_h, v_h)$ that contains three main components: a standard stiffness-like term from the [volume integrals](@entry_id:183482), and two interface terms arising from the [numerical fluxes](@entry_id:752791). However, this symmetric formulation is not inherently stable (coercive). Stability is achieved by adding a crucial third interface term: a **penalty term**. This term penalizes jumps in the solution across element faces and takes the form:
$$
\sum_{F \in \mathcal{F}_h} \int_F \sigma_F \llbracket u_h \rrbracket \cdot \llbracket v_h \rrbracket \, ds
$$
The **[penalty parameter](@entry_id:753318)**, $\sigma_F$, must be chosen sufficiently large to enforce [coercivity](@entry_id:159399) and thus stability of the discrete system. Its scaling depends on local mesh size $h$, material properties $\kappa$, and the polynomial degree $p$ of the approximation, typically $\sigma_F \sim \kappa p^2/h$ [@problem_id:3584992].

Boundary conditions are imposed weakly in the same spirit. For a Neumann boundary condition $\kappa \nabla u \cdot \mathbf{n} = g_N$, the physical flux in the boundary integral is simply replaced by the prescribed data $g_N$. For a Dirichlet boundary condition $u = g_D$, a formulation analogous to the interior face treatment is used, often known as **Nitsche's method**. It involves consistency, symmetry, and penalty terms that weakly enforce the condition $u_h = g_D$ on the boundary $\Gamma_D$ [@problem_id:3584992]. The resulting boundary terms for the [bilinear form](@entry_id:140194) $a_h(\cdot, \cdot)$ and [linear form](@entry_id:751308) $\ell_h(\cdot)$ are:
$$
a_{\Gamma_D}(u_h, v_h) = - \int_{\Gamma_D} (\kappa \partial_n u_h) v_h \, ds - \int_{\Gamma_D} (\kappa \partial_n v_h) u_h \, ds + \int_{\Gamma_D} \frac{\eta \kappa}{h} u_h v_h \, ds
$$
$$
\ell_{\Gamma_D}(v_h) = - \int_{\Gamma_D} (\kappa \partial_n v_h) g_D \, ds + \int_{\Gamma_D} \frac{\eta \kappa}{h} g_D v_h \, ds
$$
Here, $\eta$ is a sufficiently large penalty constant. This weak imposition of boundary conditions is one of the most flexible and powerful features of the DG method.

### The Role of the Numerical Flux: Stability, Dissipation, and Accuracy

The choice of numerical flux is arguably the most critical design decision in a DG scheme, dictating its stability, accuracy, and dissipative properties. While dozens of fluxes exist, they can be broadly categorized.

*   **Central Flux:** This is the simplest choice, using the arithmetic average of the states, e.g., $\widehat{\mathbf{F}} = \{\!\{\mathbf{F}(\mathbf{q}_h)\}\!\}$. While simple, a pure central flux is generally unstable for [hyperbolic systems](@entry_id:260647) as it provides no mechanism to dissipate energy associated with spurious high-frequency oscillations [@problem_id:3584978].

*   **Upwind and Lax-Friedrichs Fluxes:** These fluxes introduce **[numerical dissipation](@entry_id:141318)** to stabilize the scheme. An [upwind flux](@entry_id:143931), as seen for the [advection equation](@entry_id:144869), uses characteristic information to select the physically relevant state. A Lax-Friedrichs type flux achieves a similar effect by adding a penalty term proportional to the jump in the solution, e.g., $\widehat{\mathbf{F}} = \{\!\{\mathbf{F}(\mathbf{q}_h)\}\!\} + \alpha \llbracket \mathbf{q}_h \rrbracket$, where $\alpha$ is related to the maximum local wave speed. This added term guarantees that the discrete energy is non-increasing, ensuring robustness, especially in problems with high-contrast material properties [@problem_id:3584978].

*   **Riemann-based Fluxes:** For complex systems like linear [elastodynamics](@entry_id:175818), the most accurate fluxes are derived from the solution of a local, one-dimensional **Riemann problem** at the interface. Such a flux correctly models the physical wave interactions, such as reflection, transmission, and [mode conversion](@entry_id:197482) at [material interfaces](@entry_id:751731). For problems with strong heterogeneity and anisotropy, Riemann-based fluxes can dramatically reduce spurious reflections compared to simpler penalty-based fluxes [@problem_id:3584978], leading to much higher accuracy.

The stability imparted by dissipative fluxes comes at a cost. The introduction of numerical dissipation, which damps high-frequency content, also affects the eigenvalue spectrum of the semi-discrete spatial operator. For the advection equation, a central flux results in a purely imaginary spectrum (energy-conservative), whereas an [upwind flux](@entry_id:143931) shifts the eigenvalues into the left-half of the complex plane (dissipative) [@problem_id:3584981]. While this ensures stability, it is a known result that the **[spectral radius](@entry_id:138984)** (the largest eigenvalue magnitude) of the upwind DG operator is larger than that of the central flux operator. For [explicit time-stepping](@entry_id:168157) schemes, the maximum [stable time step](@entry_id:755325) is inversely proportional to the spectral radius (the **CFL condition**). Therefore, a scheme with an [upwind flux](@entry_id:143931) paradoxically requires a smaller time step than its (unstable) central flux counterpart [@problem_id:3584981]. This reveals a fundamental trade-off between stability, dissipation, and computational cost.

### High-Order Representation and Practical Implementation

A key appeal of DG methods is their ability to easily achieve high orders of accuracy. This requires representing the solution within each element as a polynomial of degree $p$.

#### Basis Functions and Transformations

The polynomial solution $u_h(\xi)$ on a reference element $E$ (e.g., $E=[-1,1]$) can be represented in different bases.
A **[modal basis](@entry_id:752055)** expresses the solution as a sum of [orthogonal polynomials](@entry_id:146918), such as orthonormal Legendre polynomials $\{\phi_n(\xi)\}_{n=0}^p$:
$$
u_h(\xi) = \sum_{n=0}^{p} a_n \phi_n(\xi)
$$
The unknowns are the [modal coefficients](@entry_id:752057) $\{a_n\}$. A **nodal basis** is often more convenient for implementation, especially with nonlinear problems. Here, the unknowns are the values of the solution at a set of specific points $\{\xi_i\}$ within the element, typically chosen as the nodes of a [quadrature rule](@entry_id:175061).

The transformation between the vector of [modal coefficients](@entry_id:752057) $\mathbf{a}$ and the vector of nodal values $\mathbf{U}$ is linear and is given by a **Vandermonde matrix**, $\mathbf{V}$, whose entries are the [modal basis](@entry_id:752055) functions evaluated at the [nodal points](@entry_id:171339): $V_{i,n+1} = \phi_n(\xi_i)$ [@problem_id:3584959]. For example, for $p=2$ and three Gauss-Legendre nodes on $[-1,1]$, this matrix allows one to convert between the physical space representation (nodal values) and the abstract [spectral representation](@entry_id:153219) ([modal coefficients](@entry_id:752057)) [@problem_id:3584959].

#### Numerical Quadrature

In practice, all integrals in the DG [weak form](@entry_id:137295) are computed using numerical quadrature. A [quadrature rule](@entry_id:175061) is said to have a [degree of exactness](@entry_id:175703) $q$ if it can integrate any polynomial of degree up to $q$ exactly. To avoid introducing quadrature errors that could compromise the theoretical properties of the scheme, the [quadrature rule](@entry_id:175061) must be chosen to be exact for the highest-degree polynomial appearing in the integrands.

For example, when assembling the stiffness matrix for the [diffusion equation](@entry_id:145865), the volume integral is $\int_K (\nabla \phi_i \cdot \nabla \phi_j) dx$. If the basis functions $\phi_i, \phi_j$ are polynomials of degree $p$, their gradients are polynomials of degree $p-1$. The integrand, being a product of two such terms, is a polynomial of degree up to $(p-1) + (p-1) = 2p-2$. Therefore, to compute the [stiffness matrix](@entry_id:178659) exactly, the volume [quadrature rule](@entry_id:175061) must have a [degree of exactness](@entry_id:175703) of at least $q_{\min} = 2p-2$ [@problem_id:3584984]. Similarly, the mass matrix integral $\int_K \phi_i \phi_j dx$ involves an integrand of degree up to $2p$, requiring a higher-order quadrature rule.

#### Strong vs. Weak Forms and SBP

The DG formulation derived via integration by parts is often called the **weak form**. An alternative, the **strong form**, is derived without applying [integration by parts](@entry_id:136350) to the volume term. The two forms are algebraically equivalent if and only if a discrete version of the integration-by-parts formula holds true for the chosen discrete operators ([mass matrix](@entry_id:177093) $M$, [differentiation matrix](@entry_id:149870) $D$, etc.). This property is known as the **Summation-By-Parts (SBP)** property [@problem_id:3584991]. For exact quadrature on affine meshes with constant coefficients, this property holds automatically. However, on [curvilinear meshes](@entry_id:748122) or with variable coefficients, standard [quadrature rules](@entry_id:753909) may fail to satisfy the discrete identity, a phenomenon known as [aliasing error](@entry_id:637691). This can break the equivalence of the strong and weak forms and, more critically, can lead to numerical instability. SBP-DG methods are specifically designed to retain a discrete conservation property even in the presence of such errors, ensuring robustness [@problem_id:3584947].

### Handling Discontinuities: Slope Limiting

While high-order polynomial representations are excellent for smooth solutions, they are prone to producing spurious, non-physical oscillations near sharp gradients or discontinuities, a manifestation of the Gibbs phenomenon. To maintain physical realism, these oscillations must be controlled. This is typically done via a nonlinear post-processing step called **limiting**.

A limiter modifies the polynomial solution in "troubled" cells to satisfy a monotonicity constraint. A common goal is to make the scheme **Total Variation Diminishing (TVD)**, which ensures that no new [local extrema](@entry_id:144991) are created. This is often achieved by adjusting the slope (and [higher-order moments](@entry_id:266936)) of the polynomial. For a piecewise linear ($p=1$) solution, a standard TVD [slope limiter](@entry_id:136902) replaces the computed slope $s_i$ with a limited slope $\tilde{s}_i$:
$$
\tilde{s}_i = \operatorname{minmod}\left(s_i, \frac{\bar{u}_{i+1} - \bar{u}_i}{h}, \frac{\bar{u}_i - \bar{u}_{i-1}}{h}\right)
$$
The `[minmod](@entry_id:752001)` function selects the argument with the smallest magnitude if all arguments share the same sign, and returns zero otherwise. This aggressively flattens the solution to prevent overshoots.

However, this aggressive flattening has a significant drawback: at smooth [extrema](@entry_id:271659) (e.g., the crest of a sine wave), the neighboring cell average differences have opposite signs. The `[minmod](@entry_id:752001)` function would therefore return zero, completely flattening the solution and degrading the accuracy to first-order [@problem_id:3584940].

To remedy this, the **Total Variation Bounded (TVB)** modification was introduced. The TVB limiter includes a "switch" that decides whether to apply the aggressive `[minmod](@entry_id:752001)` limiting. The limiter is deactivated if the cell is likely to contain a smooth extremum. This decision is based on a criterion that checks if the deviation of the solution at the cell boundary from the cell average is small. Specifically, if the deviation is less than a threshold $Mh^2$, limiting is skipped:
$$
\text{If } |u_h(x_{i\pm1/2}) - \bar{u}_i| \le M h^2, \text{ do not limit.}
$$
This criterion works because for a smooth solution, this deviation is of order $O(h^2)$ at an extremum, but of order $O(h)$ elsewhere. The parameter $M$ is a user-chosen constant that tunes the [limiter](@entry_id:751283)'s sensitivity. By using this TVB criterion, the scheme can distinguish between genuine shocks that require limiting and smooth extrema that should be preserved, thus retaining [high-order accuracy](@entry_id:163460) in smooth regions while robustly capturing discontinuities [@problem_id:3584940].