## Introduction
In the pursuit of highly accurate and efficient numerical simulations, high-order methods such as Discontinuous Galerkin (DG) and spectral methods have become indispensable tools. The performance of these schemes, however, hinges critically on the choice of polynomial basis functions used to represent the solution within each computational element. While various bases exist, hierarchical polynomial bases offer a unique structural advantage that dramatically simplifies advanced algorithms and enhances computational performance.

Unlike traditional nodal bases, which must be completely rebuilt when changing the polynomial degree, hierarchical bases are built on a principle of [nestedness](@entry_id:194755). This property addresses the core challenge of creating flexible and efficient adaptive algorithms, where the approximation order can be changed locally without costly reprojections.

This article provides a comprehensive exploration of hierarchical polynomial bases. The first chapter, **Principles and Mechanisms**, delves into their fundamental definition, construction from [orthogonal polynomials](@entry_id:146918), and the resulting computational benefits like [static condensation](@entry_id:176722) and effortless [p-adaptivity](@entry_id:138508). The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these properties are leveraged in `hp`-adaptive PDE solvers, advanced computational methods like `p`-[multigrid](@entry_id:172017), and across diverse fields from computational fluid dynamics to [uncertainty quantification](@entry_id:138597). Finally, the **Hands-On Practices** chapter provides concrete coding problems to translate theoretical knowledge into practical skill. By the end, you will have a deep understanding of why hierarchical bases are a cornerstone of modern computational science.

## Principles and Mechanisms

In the application of [high-order numerical methods](@entry_id:142601), such as spectral and Discontinuous Galerkin (DG) methods, the choice of basis functions for approximating the solution within each element is of paramount importance. This choice influences not only the accuracy of the approximation but also the efficiency and stability of the entire computational scheme. While many bases can represent polynomials, **hierarchical polynomial bases** offer a unique set of properties that are particularly advantageous for advanced numerical algorithms. This chapter delves into the principles defining these bases, the mechanisms by which they are constructed, and the profound consequences of their structure on computational practice.

### The Defining Property of Hierarchical Bases

The fundamental concept that distinguishes a hierarchical basis from other polynomial bases, such as the commonly used nodal Lagrange basis, is the property of **degree-wise [nestedness](@entry_id:194755)**. A basis for the space of polynomials of degree at most $N$, $\mathbb{P}_N$, given by an ordered set of functions $\{\phi_0, \phi_1, \ldots, \phi_N\}$, is defined as hierarchical if, for every integer $k$ from $0$ to $N$, the subset of the first $k+1$ functions, $\{\phi_0, \phi_1, \ldots, \phi_k\}$, forms a complete basis for the [polynomial space](@entry_id:269905) $\mathbb{P}_k$. Mathematically, this is expressed as:
$$
\mathrm{span}\{\phi_0, \phi_1, \ldots, \phi_k\} = \mathbb{P}_k \quad \forall k \in \{0, 1, \ldots, N\}
$$
For this property to hold, it is generally required that the degree of each basis function $\phi_k$ is exactly $k$. This structure implies that the basis for a lower-degree [polynomial space](@entry_id:269905) is a [proper subset](@entry_id:152276) of the basis for any higher-degree space. Such bases are often termed **modal bases**, as each function $\phi_k$ can be viewed as a distinct "mode" of the solution, adding a specific polynomial degree to the approximation. A canonical example is the set of scaled Legendre polynomials on the interval $[-1, 1]$ [@problem_id:3390225].

This nested structure stands in stark contrast to that of nodal bases, such as the Lagrange polynomials constructed on Gauss-Lobatto points. A Lagrange basis $\{\ell_j^{(N)}\}_{j=0}^N$ for the space $\mathbb{P}_N$ is defined by a set of $N+1$ distinct nodes $\{x_j^{(N)}\}_{j=0}^N$. However, the set of Gauss-Lobatto nodes for degree $N$ is not, in general, a superset of the nodes for degree $N-1$. Because the basis functions are intrinsically tied to the locations of these nodes, the Lagrange basis for $\mathbb{P}_{N-1}$ is not a subset of the Lagrange basis for $\mathbb{P}_N$. Consequently, increasing the polynomial degree from $N-1$ to $N$ requires discarding the old basis entirely and constructing a new one based on a new set of nodes. This lack of [nestedness](@entry_id:194755) makes nodal bases non-hierarchical in the sense defined above [@problem_id:3390225].

### Construction and Properties in One Dimension

The advantages of hierarchical bases become clear when we examine their properties, particularly in the context of forming the [linear systems](@entry_id:147850) that arise from DG or spectral formulations.

#### Orthogonality and the Mass Matrix

The most common and useful hierarchical bases are constructed from [orthogonal polynomials](@entry_id:146918). On the reference interval $[-1, 1]$, the Legendre polynomials, $\{P_n(x)\}_{n \ge 0}$, form a basis for the [polynomial space](@entry_id:269905) and are orthogonal with respect to the standard $L^2$ inner product:
$$
\int_{-1}^{1} P_m(x) P_n(x) \,dx = \frac{2}{2n+1} \delta_{mn}
$$
where $\delta_{mn}$ is the Kronecker delta. By scaling these polynomials, we can create an orthonormal hierarchical basis $\phi_n(x) = \sqrt{n + \frac{1}{2}} P_n(x)$, such that $\int_{-1}^1 \phi_m(x) \phi_n(x) \,dx = \delta_{mn}$ [@problem_id:3390227].

This [orthonormality](@entry_id:267887) has a profound impact on the **element [mass matrix](@entry_id:177093)**, $M$, whose entries are defined as $M_{ij} = \int_K \phi_i \phi_j \,dx$. When using an orthonormal hierarchical basis on an element $K$ that is an [affine mapping](@entry_id:746332) of the reference interval, the mass matrix becomes the identity matrix, $M_{ij} = \delta_{ij}$. The condition number of this matrix is $\kappa(M) = 1$, which is optimal and, crucially, independent of the polynomial degree $p$. In contrast, the exact mass matrix for a nodal basis on Gauss-Lobatto points is a dense, [ill-conditioned matrix](@entry_id:147408) whose condition number grows rapidly with $p$ [@problem_id:3390279]. This property makes modal hierarchical bases highly attractive for time-dependent problems solved with [explicit time-stepping](@entry_id:168157) schemes.

#### Differentiation and Sparsity

The structure of hierarchical bases also leads to efficiencies in representing derivatives. Consider the operator that maps the coefficients of a polynomial $u(x) = \sum_j a_j \phi_j(x)$ to the coefficients of its derivative $u'(x) = \sum_i b_i \phi_i(x)$. The [matrix representation](@entry_id:143451) of this operator has entries $D_{ij} = \int_{-1}^1 \phi_i(x) \phi'_j(x) \,dx$. Since $\phi'_j(x)$ is a polynomial of degree $j-1$ and $\phi_i(x)$ is orthogonal to all polynomials of degree less than $i$, it follows that $D_{ij} = 0$ for all $i \ge j$. Furthermore, due to the parity properties of Legendre polynomials, the derivative $\phi'_j(x)$ can only be expressed as a sum of basis functions $\phi_i(x)$ where $i$ and $j$ have opposite parity. The resulting [differentiation matrix](@entry_id:149870) is therefore strictly upper-triangular and sparse, with a "checkerboard" pattern of non-zero entries. This contrasts sharply with the [differentiation matrix](@entry_id:149870) for a nodal basis, which is dense [@problem_id:3390279].

The properties of orthogonal hierarchical bases are also instrumental in computing entries of stiffness matrices. For instance, consider the [bilinear form](@entry_id:140194) $a(u, v) = \int_{-1}^1 (1-x^2) u'(x) v'(x) \,dx$, which arises in the study of second-order operators. The diagonal entries of the corresponding [stiffness matrix](@entry_id:178659), $s_n = a(\phi_n, \phi_n)$, can be found by leveraging the Sturm-Liouville properties of the underlying Legendre polynomials. Through [integration by parts](@entry_id:136350) and using the Legendre differential equation, one can derive the exact, elegant result that $s_n = n(n+1)$ [@problem_id:3390227].

### The Core Advantage: Effortless p-Adaptivity

Perhaps the most celebrated advantage of hierarchical bases is the simplicity they bring to **[p-adaptivity](@entry_id:138508)**, the process of locally increasing the polynomial degree to better resolve complex features in a solution.

Suppose we have an approximate solution $u_h = \sum_{j=0}^{N-1} c_j \phi_j$ in the space $\mathbb{P}_{N-1}(K)$ and wish to enrich the approximation by moving to the space $\mathbb{P}_N(K)$. Since the hierarchical basis for $\mathbb{P}_{N-1}$ is a subset of the basis for $\mathbb{P}_N$, the function $u_h$ is already expressed in terms of the first $N$ basis functions of the new space. Its representation in $\mathbb{P}_N(K)$ is simply:
$$
u_h = c_0\phi_0 + c_1\phi_1 + \dots + c_{N-1}\phi_{N-1} + 0 \cdot \phi_N
$$
Because the representation of a vector in a given basis is unique, this means the original coefficients $\{c_0, \ldots, c_{N-1}\}$ are perfectly preserved. The enrichment process simply involves adding new basis functions (e.g., $\phi_N$) with their own coefficients, which can be determined by solving a smaller system for the "new" part of the solution. This is a purely algebraic consequence of the nested basis structure. It does not require orthogonality, though orthogonality simplifies the numerics of finding the new coefficients [@problem_id:3390244]. This seamless enrichment stands in contrast to the projection required when using non-hierarchical nodal bases.

### Structural Decomposition and Static Condensation

For practical implementations, especially in multiple dimensions, it is highly advantageous to decompose the hierarchical basis according to the behavior of its functions on the element boundary. This leads to a powerful computational technique known as **[static condensation](@entry_id:176722)**.

A standard hierarchical basis can be separated into:
1.  **Boundary Modes**: Functions that are non-zero on the element boundary $\partial K$.
2.  **Interior (or Bubble) Modes**: Functions that are identically zero on the entire boundary $\partial K$.

In one dimension, interior modes for the interval $[-1, 1]$ can be constructed by taking a set of polynomials and multiplying them by a factor that vanishes at the endpoints, such as $(1-x^2)$. A standard construction uses Jacobi polynomials, which are orthogonal with respect to a [weighted inner product](@entry_id:163877), defining bubble modes of degree $n$ as $\psi_n(x) = (1-x^2)P_{n-2}^{(1,1)}(x)$ for $n \ge 2$ [@problem_id:3390236].

The power of this decomposition is realized in the DG [weak formulation](@entry_id:142897). The coupling between adjacent elements occurs through integrals over the element boundary involving a [numerical flux](@entry_id:145174). When the weak form is tested with an interior mode $\psi_n$, which is zero everywhere on the boundary, the entire boundary integral term vanishes.
$$
\int_{\partial K} \psi_n \, \widehat{\boldsymbol{f}} \, dS = 0
$$
This means that the equations for the coefficients of the interior modes are decoupled from all neighboring elements; they depend only on other degrees of freedom within the same element. This results in a block-structured linear system where the sub-matrix corresponding to interior modes can be inverted locally. The interior degrees of freedom can be expressed in terms of the boundary degrees of freedom and "eliminated" from the global system, which then only involves the coupled boundary modes. This process of [static condensation](@entry_id:176722) can dramatically reduce the size and cost of solving the global linear system [@problem_id:3390254].

### Extension to Higher Dimensions

The principles of hierarchical bases extend naturally to higher dimensions, although the constructions become more intricate.

#### Tensor Product Elements

For quadrilateral or [hexahedral elements](@entry_id:174602), a 2D or 3D basis can be formed by taking all possible tensor products of a 1D hierarchical basis. This leads to a [natural classification](@entry_id:265169) of modes based on their support on the element boundary. On a square, for example, a basis constructed from 1D vertex-based functions ($\phi^v$) and 1D edge-based (interior) functions ($\phi^e$) yields three families of 2D modes [@problem_id:3390278]:
*   **Vertex Modes**: 4 modes of the form $\phi^v(x)\phi^v(y)$, each non-zero at a single vertex.
*   **Edge Modes**: $4(p-1)$ modes of the forms $\phi^v(x)\phi^e_n(y)$ and $\phi^e_m(x)\phi^v(y)$, which are non-zero along a single edge and vanish at all vertices.
*   **Interior Modes**: $(p-1)^2$ modes of the form $\phi^e_m(x)\phi^e_n(y)$, which vanish on the entire boundary of the square.

This decomposition is the foundation for [static condensation](@entry_id:176722) in 2D and 3D, where vertex, edge, and face degrees of freedom are coupled globally, while all interior modes are eliminated locally.

#### Simplicial Elements

For triangles and tetrahedra, the tensor product construction is not applicable. Instead, specialized bases are constructed, often using [barycentric coordinates](@entry_id:155488) and families of Jacobi polynomials. For the reference triangle, edge modes are constructed to vanish at the vertices of their associated edge, and interior modes are constructed to vanish on all three edges. For example, a family of edge modes of total degree at most $p$ can be defined using a factor $\lambda_i\lambda_j$ (where $\lambda_i, \lambda_j$ are [barycentric coordinates](@entry_id:155488)) to ensure vanishing at two vertices, combined with a properly scaled Jacobi polynomial $P_k^{(1,1)}$. Similarly, interior modes use a factor $\lambda_1\lambda_2\lambda_3$ to ensure vanishing on the entire boundary, combined with a product of two Jacobi polynomials of specifically chosen parameters to maintain polynomiality and desirable orthogonality properties [@problem_id:3390264].

### Practical Challenges: Curvature and Nonlinearity

While powerful, the application of hierarchical bases is not without its challenges, particularly when dealing with realistic physical problems.

#### Curved Element Geometries

The ideal properties of modal bases, such as the diagonality of the [mass matrix](@entry_id:177093), rely on the element being an affine map of the reference element. If an element is curved, the [isoparametric mapping](@entry_id:173239) $x = \chi(\hat{x})$ from the reference coordinate $\hat{x}$ is non-affine. The [change of variables](@entry_id:141386) introduces a non-constant Jacobian determinant $J(\hat{x})$ into the integrals:
$$
M_{ij} = \int_{\hat{K}} \phi_i(\hat{x}) \phi_j(\hat{x}) J(\hat{x}) \,d\hat{x}
$$
Since $J(\hat{x})$ is not a constant, the orthogonality of the basis functions is destroyed. For instance, for a simple quadratic map $x(\hat{x}) = \hat{x} + \alpha \hat{x}^2$, the Jacobian is $J(\hat{x}) = 1 + 2\alpha\hat{x}$. The resulting [mass matrix](@entry_id:177093) contains non-zero off-diagonal entries. The entry $M_{12}$ for the Legendre basis can be explicitly calculated as $\frac{4\alpha\sqrt{15}}{15}$, directly quantifying the [loss of orthogonality](@entry_id:751493) due to the geometric curvature $\alpha$ [@problem_id:3390267]. While the mass matrix is no longer the identity, it typically remains sparse, block-structured, and well-conditioned for mild curvature.

#### Nonlinearities and Aliasing

A second challenge arises in problems with nonlinear terms, such as the [convective flux](@entry_id:158187) $u^2$ in fluid dynamics. When projecting a nonlinear term onto the basis via integration, e.g., $c_k = \int u^2 \phi_k \,dx$, numerical quadrature is typically employed. A Gauss quadrature rule with $N_q$ points is exact only for polynomial integrands up to degree $2N_q-1$. If $u \in \mathbb{P}_p$, the integrand $u^2 \phi_k$ can have a degree as high as $2p+k$. If the quadrature rule is not sufficient for this degree, **[aliasing](@entry_id:146322)** occurs, where high-frequency components of the integrand are erroneously represented as low-frequency components, potentially leading to [numerical instability](@entry_id:137058).

The hierarchical nature of the basis provides a clear way to analyze and mitigate this problem. The condition for the coefficient $c_k$ to be computed without [aliasing](@entry_id:146322) is $2p+k \le 2N_q-1$. This inequality allows us to identify precisely which [modal coefficients](@entry_id:752057) are potentially contaminated by [quadrature error](@entry_id:753905). For any mode $k > 2N_q-1-2p$, the computed coefficient may be inaccurate. A robust stabilization strategy is to apply a **hierarchical modal filter**, which simply sets the coefficients of all contaminated high-degree modes to zero, effectively projecting the nonlinear term onto a de-aliased subspace. This surgical removal of aliased energy is a powerful tool for stabilizing spectral computations of nonlinear problems [@problem_id:3390273].