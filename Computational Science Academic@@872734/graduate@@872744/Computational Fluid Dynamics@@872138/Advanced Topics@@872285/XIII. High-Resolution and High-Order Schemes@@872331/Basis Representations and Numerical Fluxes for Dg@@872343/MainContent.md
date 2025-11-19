## Introduction
The Discontinuous Galerkin (DG) method has emerged as a preeminent numerical framework in [computational fluid dynamics](@entry_id:142614) (CFD), valued for its ability to combine the [high-order accuracy](@entry_id:163460) of [finite element methods](@entry_id:749389) with the shock-capturing robustness and [local conservation](@entry_id:751393) properties of [finite volume methods](@entry_id:749402). Its exceptional geometric flexibility makes it a powerful tool for simulating complex flows across science and engineering. However, harnessing the full potential of DG requires a deep understanding of its core components: how the solution is represented within each computational element and how these discrete elements communicate with each other to form a coherent global solution.

This article addresses the fundamental choices and trade-offs inherent in designing a DG scheme. It demystifies the concepts of basis representations and [numerical fluxes](@entry_id:752791), which are central to the method's performance, stability, and physical fidelity. The reader will gain a clear understanding of the distinctions between modal and nodal bases and learn how the design of the numerical flux governs everything from stability and dissipation to the accurate resolution of complex wave phenomena.

The article is structured to build knowledge progressively. The first section, **Principles and Mechanisms**, establishes the theoretical foundation, deriving the DG weak formulation, exploring different basis representations, and detailing the properties of numerical fluxes. The following section, **Applications and Interdisciplinary Connections**, showcases how these principles are put into practice to handle complex geometries, ensure physical constraints like positivity and [entropy stability](@entry_id:749023), and tackle multi-physics problems. Finally, **Hands-On Practices** provides targeted problems to reinforce the key computational concepts discussed.

## Principles and Mechanisms

The Discontinuous Galerkin (DG) method is a powerful numerical framework for [solving partial differential equations](@entry_id:136409), particularly those of a hyperbolic nature such as the equations of fluid dynamics. Its strength lies in a unique combination of features from both finite element and [finite volume methods](@entry_id:749402). This chapter delves into the core principles and mechanisms that underpin the DG method, focusing on how solutions are represented within computational elements and how these elements are coupled together. We will explore the derivation of the governing discrete equations, the crucial role of basis functions, and the theory and practice of [numerical fluxes](@entry_id:752791) that ensure stability and accuracy.

### The Discontinuous Galerkin Weak Formulation

The starting point for any DG [discretization](@entry_id:145012) is the [weak formulation](@entry_id:142897) of the governing partial differential equation (PDE) on a single computational element. Let us consider a general [scalar conservation law](@entry_id:754531) in one dimension, a foundational model for many phenomena in CFD:
$$
\partial_t u + \partial_x f(u) = 0 \quad \text{for } x \in K
$$
Here, $u(x,t)$ is a conserved quantity, $f(u)$ is the corresponding flux function, and $K$ is a single element (an interval) in our [computational mesh](@entry_id:168560). The DG method seeks an approximate solution, $u_h(x,t)$, that, within each element $K$, is a polynomial of degree at most $k$. The space of such functions is denoted $\mathbb{P}^k(K)$.

To derive the [weak form](@entry_id:137295), we follow the standard Galerkin procedure: we multiply the PDE by a polynomial test function $v(x) \in \mathbb{P}^k(K)$ and integrate over the element $K$:
$$
\int_{K} (\partial_t u_h) v \,dx + \int_{K} (\partial_x f(u_h)) v \,dx = 0
$$

The critical step in the DG formulation is applying integration by parts to the second term, which contains the spatial derivative. This "weakens" the formulation by transferring the derivative from the potentially discontinuous solution $u_h$ to the smooth polynomial test function $v$:
$$
\int_K \partial_x f(u_h) \, v \, dx = [f(u_h) v]_{\partial K} - \int_K f(u_h) \, \partial_x v \, dx
$$
The boundary term $[f(u_h) v]_{\partial K}$ represents the evaluation of the product $f(u_h) v$ at the endpoints of the interval $K$. Substituting this back into our integrated equation, we get:
$$
\int_{K} (\partial_t u_h) v \,dx - \int_K f(u_h) \, \partial_x v \, dx + [f(u_h) v]_{\partial K} = 0
$$

A fundamental challenge now arises. The solution $u_h$ is, by design, allowed to be discontinuous across element boundaries. At an interface between two elements, the trace of $u_h$ (its value at the boundary) can differ depending on whether it is approached from the left or the right. Consequently, the physical flux $f(u_h)$ is not uniquely defined at the interface.

To resolve this ambiguity and properly couple adjacent elements, the DG method replaces the physical flux $f(u_h)$ at the boundary with a **[numerical flux](@entry_id:145174)**, denoted $\hat{f}$. This [numerical flux](@entry_id:145174) is a function that takes the two states on either side of the interface, the interior trace $u_h^-$ and the exterior trace $u_h^+$, and produces a single, uniquely defined value for the flux. The choice of this function is critical to the stability and accuracy of the entire scheme.

Incorporating the numerical flux, the final semi-discrete DG [weak formulation](@entry_id:142897) on an element $K_i=(x_{i-1/2}, x_{i+1/2})$ for any [test function](@entry_id:178872) $v \in \mathbb{P}^k(K_i)$ is expressed as [@problem_id:3295168]:
$$
\int_{K_i} (\partial_t u_h) v \,dx - \int_{K_i} f(u_h) (\partial_x v) \,dx + \hat{f}(x_{i+1/2})v(x_{i+1/2}^-) - \hat{f}(x_{i-1/2})v(x_{i-1/2}^+) = 0
$$
where $\hat{f}(x_{i+1/2})$ is the numerical flux at the right boundary, computed from $u_h^-(x_{i+1/2})$ and $u_h^+(x_{i+1/2})$, and so on. A more general and robust representation uses the outward [unit normal vector](@entry_id:178851) $n_i$ for element $K_i$. At the right boundary $x_{i+1/2}$, $n_i=+1$, and at the left boundary $x_{i-1/2}$, $n_i=-1$. The boundary term can then be written as a sum over the boundary points, $\sum_{x \in \partial K_i} \hat{f}_n(u_h^-, u_h^+; n_i) v(x^-)$, where $\hat{f}_n$ is the numerical normal flux. This leads to the [canonical form](@entry_id:140237):
$$
\int_{K_i} (\partial_t u_h) v \,dx - \int_{K_i} f(u_h) (\partial_x v) \,dx + \sum_{x \in \partial K_i} \hat{f}_n(u_h^-(x), u_h^+(x); n_i(x)) v(x^-) = 0
$$
This equation forms the foundation of the DG method. It is an evolution equation for the polynomial representation of the solution within a single element, coupled to its neighbors only through the [numerical flux](@entry_id:145174) at its boundaries.

### Basis Representations: The Building Blocks of the Solution

Within each element, the polynomial solution $u_h \in \mathbb{P}^k$ must be represented by a finite number of degrees of freedom. The choice of basis functions to span the [polynomial space](@entry_id:269905) $\mathbb{P}^k$ has significant practical implications for the structure and efficiency of the resulting numerical algorithm. Two common choices are modal and nodal bases [@problem_id:3295140].

#### Modal Basis Representation

A **[modal basis](@entry_id:752055)** represents a function as a weighted sum of a set of prescribed polynomial "modes". For DG methods, a particularly advantageous choice is a basis of [orthogonal polynomials](@entry_id:146918). On the [reference element](@entry_id:168425) $\xi \in [-1, 1]$, the Legendre polynomials, $\{P_m(\xi)\}_{m=0}^k$, are a standard choice. They satisfy the orthogonality relation:
$$
\int_{-1}^{1} P_m(\xi) P_n(\xi) \, d\xi = \frac{2}{2m+1} \delta_{mn}
$$
where $\delta_{mn}$ is the Kronecker delta. A function $u_h(\xi) \in \mathbb{P}^k$ is represented as:
$$
u_h(\xi) = \sum_{m=0}^k \hat{u}_m P_m(\xi)
$$
The degrees of freedom are the **[modal coefficients](@entry_id:752057)** $\{\hat{u}_m\}$, each representing the "amount" of mode $P_m$ present in the solution. For instance, $\hat{u}_0$ is related to the element average, $\hat{u}_1$ to the linear slope, and so on.

#### Nodal Basis Representation

A **nodal basis** represents a function by its values at a specific set of points, or nodes, within the element. For a polynomial of degree $k$, we need $k+1$ distinct nodes. A powerful choice for DG methods is the set of $k+1$ **Gauss-Lobatto-Legendre (GLL)** points, $\{\xi_i\}_{i=0}^k$. These points include the endpoints $\xi_0 = -1$ and $\xi_k = 1$, with the interior points chosen as the roots of $P_k'(\xi)$, the derivative of the degree-$k$ Legendre polynomial.

The corresponding basis functions are the Lagrange interpolation polynomials, $\{\ell_i(\xi)\}_{i=0}^k$, defined by the property $\ell_i(\xi_j) = \delta_{ij}$. A function $u_h(\xi) \in \mathbb{P}^k$ is then represented as:
$$
u_h(\xi) = \sum_{i=0}^k u(\xi_i) \ell_i(\xi)
$$
The degrees of freedom are the **nodal values** $\{u(\xi_i)\}$, which are the physically intuitive values of the solution at the specified nodes.

#### From Modal to Nodal: A Change of Basis

The modal and nodal representations are simply two different perspectives on the same polynomial. One can always transform from one set of degrees of freedom to the other. The relationship is given by evaluating the modal expansion at the [nodal points](@entry_id:171339):
$$
u(\xi_i) = \sum_{m=0}^k \hat{u}_m P_m(\xi_i)
$$
This defines a linear transformation. For instance, for $k=3$, the GLL points are $\{-1, -1/\sqrt{5}, 1/\sqrt{5}, 1\}$ and the Legendre polynomials are $P_0(\xi)=1$, $P_1(\xi)=\xi$, $P_2(\xi)=\frac{1}{2}(3\xi^2-1)$, and $P_3(\xi)=\frac{1}{2}(5\xi^3-3\xi)$. The [transformation matrix](@entry_id:151616) $T$ that maps the vector of [modal coefficients](@entry_id:752057) $\mathbf{\hat{u}}$ to the vector of nodal values $\mathbf{u}_{\text{nodal}}$ has entries $T_{im} = P_m(\xi_i)$. A direct calculation yields [@problem_id:3295140]:
$$
T = \begin{pmatrix}
1  -1  1  -1 \\
1  -1/\sqrt{5}  -1/5  1/\sqrt{5} \\
1  1/\sqrt{5}  -1/5  -1/\sqrt{5} \\
1  1  1  1
\end{pmatrix}
$$

### From Weak Form to a System of ODEs

Substituting the [basis expansion](@entry_id:746689) for $u_h$ into the DG [weak form](@entry_id:137295) and choosing the [test functions](@entry_id:166589) $v$ to be each of the basis functions in turn, we transform the PDE into a system of [ordinary differential equations](@entry_id:147024) (ODEs) for the vector of degrees of freedom, $\mathbf{u}(t)$. For an expansion $u_h(x,t) = \sum_j u_j(t) \phi_j(x)$, the semi-discrete system takes the form [@problem_id:3295138]:
$$
\mathbf{M} \frac{d\mathbf{u}}{dt} = \mathbf{R}(\mathbf{u})
$$
where the right-hand side vector $\mathbf{R}(\mathbf{u})$ contains the spatial derivative and flux terms, and $\mathbf{M}$ is the **mass matrix**. Its entries are given by the inner products of the basis functions:
$$
M_{ij} = \int_K \phi_i(x) \phi_j(x) \, dx
$$
The structure of this mass matrix is profoundly affected by the choice of basis.

-   With a **modal Legendre basis**, the orthogonality of the polynomials makes the mass matrix **diagonal** when integrated exactly. For example, for $k=1$ with basis $\{\phi_0=1, \phi_1=x\}$ on $[-1,1]$, the [mass matrix](@entry_id:177093) is [@problem_id:3295138]:
    $$
    \mathbf{M} = \begin{pmatrix} \int_{-1}^1 1 \cdot 1 \,dx  \int_{-1}^1 1 \cdot x \,dx \\ \int_{-1}^1 x \cdot 1 \,dx  \int_{-1}^1 x \cdot x \,dx \end{pmatrix} = \begin{pmatrix} 2  0 \\ 0  2/3 \end{pmatrix}
    $$
    A [diagonal mass matrix](@entry_id:173002) is trivial to invert, making [explicit time-stepping](@entry_id:168157) schemes extremely efficient.

-   With a **nodal Lagrange basis**, the exact [mass matrix](@entry_id:177093) is generally dense. However, a major computational advantage emerges if the integrals are approximated using numerical quadrature at the same GLL nodes that define the basis. This practice, common in DG [spectral element methods](@entry_id:755171), leads to a phenomenon called **[mass lumping](@entry_id:175432)**. The quadrature approximation of the mass matrix becomes diagonal [@problem_id:3295117]:
    $$
    M_{ij} = \int_K \ell_i \ell_j \, dx \approx \sum_{p=0}^k w_p \ell_i(\xi_p) \ell_j(\xi_p) = \sum_{p=0}^k w_p \delta_{ip} \delta_{jp} = w_i \delta_{ij}
    $$
    where $w_i$ are the [quadrature weights](@entry_id:753910). This "collocation" approach also yields a [diagonal mass matrix](@entry_id:173002), retaining the high computational efficiency for time evolution. This duality—the naturally orthogonal [modal basis](@entry_id:752055) versus the conveniently "lumpable" nodal basis—represents a fundamental design choice in implementing a DG code [@problem_id:3295140].

### The Role of the Numerical Flux

The [numerical flux](@entry_id:145174) $\hat{f}$ is the glue that holds the DG discretization together. Its design is paramount, as it governs the stability of the scheme and its ability to accurately capture physical phenomena like shock waves. A well-designed [numerical flux](@entry_id:145174) for a hyperbolic conservation law must satisfy several key properties [@problem_id:3295131].

#### Fundamental Properties: Consistency and Conservation

-   **Consistency**: The numerical flux must be consistent with the physical flux. That is, if the states on the left and right of the interface are identical ($u_L = u_R = u$), the [numerical flux](@entry_id:145174) must return the physical flux: $\hat{f}(u, u) = f(u)$. This ensures that the [discretization](@entry_id:145012) converges to the correct PDE as the mesh is refined.

-   **Conservation**: The scheme must be conservative, meaning that the total amount of the conserved quantity $u$ in the domain can only change due to fluxes at the physical boundaries of the domain. In the DG framework, this is achieved structurally. At any interior interface between elements $K_j$ and $K_{j+1}$, the outward normal of $K_j$ is the negative of the outward normal of $K_{j+1}$. Because a single-valued numerical flux is used at the interface, its contribution to the global sum of all element equations cancels out perfectly. Summing the [local conservation](@entry_id:751393) equations (derived below) over all elements yields a [telescoping sum](@entry_id:262349) of interior fluxes, leaving only the fluxes at the domain boundaries. This guarantees global conservation, which is essential for computing correct shock speeds [@problem_id:3295184].

A remarkable property of the DG method is that it is **locally conservative**. By choosing a [test function](@entry_id:178872) $v=1$ (which is always in $\mathbb{P}^k(K)$ for $k \ge 0$), the term $\int_K f(u_h) (\partial_x v) \, dx$ in the [weak form](@entry_id:137295) vanishes. The remaining equation is a perfect statement of conservation for the element average $\bar{u}_h = \frac{1}{|K|}\int_K u_h dx$ [@problem_id:3295168] [@problem_id:3295184]:
$$
\frac{d}{dt} \int_{K_i} u_h \,dx + \hat{f}(x_{i+1/2}) - \hat{f}(x_{i-1/2}) = 0
$$
This states that the rate of change of the total amount of $u_h$ in element $K_i$ is perfectly balanced by the net flux through its boundaries. This property is not generally shared by standard Continuous Galerkin (CG) methods, which couple equations across elements and do not yield a simple conservation statement for a single element.

#### Upwinding, Stability, and Dissipation

For hyperbolic problems, where information propagates along characteristics, the numerical scheme must respect the direction of information flow. This is achieved through **[upwinding](@entry_id:756372)**. Consider the [linear advection equation](@entry_id:146245) $u_t + a u_x = 0$ with $a>0$. Information flows from left to right.

-   The **[upwind flux](@entry_id:143931)** simply selects the state from the upwind direction: $\hat{f}(u_L, u_R) = f(u_L) = a u_L$. This choice introduces a numerical dissipation that is crucial for the stability of the scheme.

-   In contrast, a simple **central flux**, $\hat{f}(u_L, u_R) = \frac{1}{2}(f(u_L) + f(u_R))$, is not dissipative and leads to an unstable scheme for DG when applied to hyperbolic problems [@problem_id:3295184].

-   A more general-purpose flux is the **Rusanov flux** (or Local Lax-Friedrichs flux), given by $\hat{f}(u_L, u_R) = \frac{1}{2}(f(u_L) + f(u_R)) - \frac{1}{2}c(u_R - u_L)$, where $c$ is a local estimate of the maximum wave speed. For the [linear advection equation](@entry_id:146245) with $a>0$, if we choose $c=|a|=a$, the Rusanov flux becomes:
    $$
    \hat{f}_{\text{Rusanov}} = \frac{1}{2}(a u_L + a u_R) - \frac{1}{2}a(u_R - u_L) = a u_L
    $$
    In this simple case, the Rusanov flux is identical to the [upwind flux](@entry_id:143931) [@problem_id:3295144]. This highlights that more complex, general-purpose fluxes often reduce to simpler, optimal forms for specific problems.

#### Fluxes for Systems: The Euler Equations

For [systems of conservation laws](@entry_id:755768), like the compressible Euler equations, the choice of flux becomes even more critical. The Euler equations possess a richer wave structure, typically consisting of two acoustic waves and a contact/shear wave. The ability of a numerical flux to resolve these distinct wave families depends on its underlying "approximate Riemann solver".

-   The **HLL flux** (Harten-Lax-van Leer) is a simple and robust two-wave solver. It only models the fastest left- and right-propagating waves, smearing out any intermediate wave structures. As a result, it is excessively dissipative for [contact discontinuities](@entry_id:747781) and shear layers, which are carried by the middle wave of the Euler system [@problem_id:3295207].

-   The **HLLC flux** (HLL-Contact) is an extension that reintroduces the middle contact wave. This allows it to resolve contact and shear waves with much greater accuracy and less smearing. Similarly, the **Roe flux** is based on a [local linearization](@entry_id:169489) that resolves all wave families. A test problem consisting of a pure [contact discontinuity](@entry_id:194702) (where velocity and pressure are constant, but density jumps) starkly reveals this difference: an HLL flux will smear the density jump across several cells, while HLLC and Roe fluxes can maintain a sharp interface [@problem_id:3295207].

### Advanced Principles

The flexibility of the DG framework gives rise to a rich set of theoretical properties and advanced techniques that are topics of active research and are crucial for developing cutting-edge CFD solvers.

#### Entropy Stability

For [nonlinear conservation laws](@entry_id:170694), especially those that develop shocks, ensuring convergence to the physically relevant solution requires satisfying an **[entropy condition](@entry_id:166346)**. This is a mathematical expression of the [second law of thermodynamics](@entry_id:142732). A [numerical flux](@entry_id:145174) is considered **monotone** if it is non-decreasing in its first argument ($u_L$) and non-increasing in its second ($u_R$). This property is sufficient to guarantee that a first-order scheme ($k=0$) will not generate [spurious oscillations](@entry_id:152404) and will converge to the correct solution. For higher-order DG ($k \ge 1$), which is inherently non-monotone, stability is often achieved with limiters that locally enforce a monotonicity property, building upon the stability of the underlying monotone flux [@problem_id:3295131].

A more refined concept is that of **[entropy stability](@entry_id:749023)**. An entropy pair $(\eta(u), q(u))$ consists of a convex entropy function $\eta$ and a corresponding entropy flux $q$ that are compatible with the PDE. A [numerical flux](@entry_id:145174) is **entropy conservative** if it is designed to conserve not just the quantity $u$ but also the entropy $\eta$ at the discrete level. For Burgers' equation, $u_t + (u^2/2)_x = 0$, with the canonical entropy $\eta(u) = u^2/2$, the unique entropy-conservative flux is given by [@problem_id:3295156]:
$$
\hat{f}^{\text{ec}}(u_L, u_R) = \frac{1}{6}(u_L^2 + u_L u_R + u_R^2)
$$
Practical, [entropy-stable fluxes](@entry_id:749015) are then constructed by adding a carefully calibrated amount of numerical dissipation to such an entropy-conservative base flux.

#### Summation-By-Parts and Energy Conservation

An alternative path to proving stability, particularly popular in high-order nodal DG methods, involves the algebraic structure of the discrete operators. The [differentiation matrix](@entry_id:149870) $D$ associated with GLL nodes, when combined with the [diagonal mass matrix](@entry_id:173002) $W$, satisfies a discrete analogue of [integration by parts](@entry_id:136350) known as the **Summation-by-Parts (SBP)** property: $W D + D^T W = B$, where $B$ is a boundary matrix with non-zero entries only corresponding to the endpoints.

This property can be exploited to construct discretizations of nonlinear terms that are discretely energy-conservative. For example, by writing the nonlinear term of Burgers' equation in a skew-symmetric "split form", one can show that the volume contribution to the energy evolution is identically zero, meaning the scheme is non-dissipative in the interior. The total energy can then only change through the dissipative action of the [numerical flux](@entry_id:145174) at the boundaries [@problem_id:3295117].

#### Superconvergence

A celebrated and somewhat surprising property of DG methods is **superconvergence**. While the global error for a smooth solution is typically of order $\mathcal{O}(h^{k+1})$, the error at certain specific points within each element can be much smaller. For the one-dimensional [linear advection equation](@entry_id:146245) with [upwind flux](@entry_id:143931), a careful [error analysis](@entry_id:142477) reveals that the leading-order error is not a generic polynomial but has a specific structure proportional to a **Radau polynomial**. The interior roots of this polynomial are therefore points of superconvergence, where the pointwise error is of order $\mathcal{O}(h^{k+2})$—one full order higher than the global optimum.

For instance, for polynomial degree $k=1$, the superconvergence point on the reference element $\xi \in [-1,1]$ is located at $\xi = -1/3$. For $k=2$, there are two such points, at $\xi = (-1 \pm \sqrt{6})/5$. At these specific "downwind-biased" locations, the DG solution is exceptionally accurate [@problem_id:3295134]. This phenomenon is not just a theoretical curiosity; it can be exploited for applications like [adaptive mesh refinement](@entry_id:143852), where highly accurate [error indicators](@entry_id:173250) are needed.

In summary, the principles of the Discontinuous Galerkin method involve a carefully constructed weak formulation, a flexible choice of basis representations, and the critical design of a [numerical flux](@entry_id:145174) to couple elements. These components give rise to a method that is locally conservative, robust for hyperbolic problems, and amenable to [high-order accuracy](@entry_id:163460), with a rich underlying mathematical structure that ensures stability and admits advanced properties like [entropy conservation](@entry_id:749018) and superconvergence.