## Introduction
High-order spectral and discontinuous Galerkin (DG) methods offer exceptional accuracy for [solving partial differential equations](@entry_id:136409), but their power comes with a significant computational challenge. A naive application of differential operators leads to prohibitively expensive calculations that scale exponentially with spatial dimension, creating a bottleneck that severely limits the practicality of these methods for large-scale problems. This article addresses this critical performance gap by detailing sum factorization, a powerful algorithmic technique that unlocks the efficiency of [high-order methods](@entry_id:165413).

Across the following chapters, you will gain a comprehensive understanding of this essential technique. The first chapter, "Principles and Mechanisms," delves into the mathematical foundation of sum factorization, explaining how the tensor-product structure of polynomial bases on specific elements allows for the decomposition of large, multi-dimensional operators into a sequence of efficient one-dimensional actions. The second chapter, "Applications and Interdisciplinary Connections," demonstrates how this principle serves as the computational engine for modern PDE solvers in fields like fluid dynamics and electromagnetism, and enables advanced algorithms and high-performance computing strategies. Finally, the "Hands-On Practices" section provides targeted problems to solidify your understanding of the theory and its quantitative benefits. We begin by exploring the fundamental principles that make this remarkable efficiency possible.

## Principles and Mechanisms

High-order spectral and discontinuous Galerkin (DG) methods achieve their remarkable accuracy through the use of high-degree polynomial approximations within each element. However, this power comes at a potential computational cost. A naive implementation of the associated operators—such as differentiation, interpolation, or the assembly of [mass and stiffness matrices](@entry_id:751703)—can lead to prohibitively expensive calculations, scaling poorly with both the polynomial degree and the spatial dimension. The key to unlocking the efficiency of these methods on structured, tensor-product elements (such as quadrilaterals and hexahedra) lies in a powerful algorithmic technique known as **sum factorization**. This chapter elucidates the fundamental principles of sum factorization, from its theoretical underpinnings in tensor-[product spaces](@entry_id:151693) to its practical application and performance implications.

### The Foundation: Separability and Tensor-Product Spaces

The efficacy of sum factorization is intrinsically linked to the mathematical structure of the approximation spaces used on certain element geometries. For [reference elements](@entry_id:754188) that are hypercubes, such as the interval $[-1,1]$ in one dimension, the square $[-1,1]^2$ in two, or the cube $[-1,1]^3$ in three, the natural choice for a polynomial approximation space is the **tensor-product space**, denoted $Q_p$.

A polynomial $u(\boldsymbol{\xi})$ on the $d$-dimensional [hypercube](@entry_id:273913) $\hat{K} = [-1,1]^d$ belongs to the space $Q_p(\hat{K})$ if it can be expressed as a linear combination of basis functions that are themselves products of one-dimensional polynomials of degree at most $p$. If $P_p([-1,1])$ denotes the space of univariate polynomials of degree up to $p$, then $Q_p(\hat{K})$ is formally the $d$-fold [tensor product](@entry_id:140694) of this space with itself:

$$
Q_p([-1,1]^d) = \bigotimes_{k=1}^d P_p([-1,1])
$$

This means that any basis for $Q_p$ can be constructed by taking all possible products of basis functions from the one-dimensional space $P_p$. For instance, if $\{ \phi_i(x) \}_{i=0}^p$ is a basis for $P_p([-1,1])$, then a basis for $Q_p([-1,1]^d)$ is given by $\{ \prod_{k=1}^d \phi_{i_k}(\xi_k) \}_{0 \le i_1, \dots, i_d \le p}$. The indices $i_1, \dots, i_d$ vary independently, forming a rectangular (or hypercubic) [index set](@entry_id:268489). This separability is the cornerstone of sum factorization [@problem_id:3422293].

The dimension of this space is the product of the dimensions of the constituent 1D spaces. Since $\dim(P_p) = p+1$, the dimension of $Q_p([-1,1]^d)$ is $(p+1)^d$. This space should not be confused with the **total-degree [polynomial space](@entry_id:269905)**, $P_p(\hat{K})$, which consists of all polynomials where the sum of the degrees in all variables is at most $p$. For example, in 2D, the monomial $\xi_1^p \xi_2^p$ is in $Q_p$ but not in $P_p$ for $p \ge 1$, because its total degree is $2p$. The dimension of $P_p([-1,1]^d)$ is $\binom{p+d}{d}$, which is significantly smaller than $(p+1)^d$ for large $p$ and $d>1$ [@problem_id:3422293]. While $P_p$ is the natural space for simplicial elements like triangles and tetrahedra, $Q_p$ is the appropriate choice for quadrilaterals and hexahedra.

Two common choices for the 1D basis functions $\phi_i(x)$ give rise to two families of bases for $Q_p$ [@problem_id:3422289]:

1.  **Nodal Basis:** The basis functions are one-dimensional Lagrange polynomials $\{\ell_i(\xi)\}_{i=0}^p$ associated with a set of $p+1$ distinct nodes on $[-1,1]$, such as the Gauss-Lobatto-Legendre (GLL) points. The resulting $d$-dimensional basis functions, $h_{\boldsymbol{i}}(\boldsymbol{\xi}) = \prod_{k=1}^d \ell_{i_k}(\xi_k)$, have the convenient property that they are equal to one at a single node of the tensor-product grid and zero at all others. This allows a function to be represented directly by its values at these grid points.

2.  **Modal Basis:** The basis functions are chosen from a family of [orthogonal polynomials](@entry_id:146918), such as Legendre polynomials $\{L_i(\xi)\}_{i=0}^p$. The $d$-dimensional basis functions are $\Phi_{\boldsymbol{a}}(\boldsymbol{\xi}) = \prod_{k=1}^d L_{a_k}(\xi_k)$. A function is represented by a set of [modal coefficients](@entry_id:752057), which correspond to the weights of these basis "modes".

Both basis types are constructed as tensor products and are therefore compatible with sum factorization. As we will see, it is possible to transform efficiently between these representations.

### The Mechanism of Sum Factorization

To appreciate the efficiency gained by sum factorization, we must first consider the computational cost of a naive approach.

#### The Prohibitive Cost of Naive Operator Application

Consider the task of evaluating the [partial derivatives](@entry_id:146280) of a function $u \in Q_p$ at the $(p+1)^d$ nodes of a tensor-product grid. In a naive implementation, one would construct a global [differentiation matrix](@entry_id:149870) for each coordinate direction. This matrix would have dimensions $(p+1)^d \times (p+1)^d$. A [matrix-vector multiplication](@entry_id:140544) to compute the nodal values of the derivative would therefore cost $O(((p+1)^d)^2) = O((p+1)^{2d})$ floating-point operations (FLOPs). For a three-dimensional problem ($d=3$) with a modest polynomial degree of $p=7$ (so $n=p+1=8$), the matrix size is $512 \times 512$, but the operation count is on the order of $(8^3)^2 \approx 262,000$. For $p=15$ ($n=16$), this balloons to $(16^3)^2 \approx 16.7$ million FLOPs *per operator application, per element*. This scaling renders [high-order methods](@entry_id:165413) impractical for many problems [@problem_id:3422311], [@problem_id:3422300].

#### The Sum Factorization Solution

Sum factorization avoids the explicit formation of these large, $d$-dimensional matrices. Instead, it exploits the tensor-product structure to decompose the operation into a sequence of small, one-dimensional operations.

**The One-Dimensional Building Block**

Let's begin in one dimension. A polynomial $u(\xi) \in P_p$ is represented by its values $u_j$ at a set of $n=p+1$ nodes $\{\xi_j\}_{j=1}^n$. The values of its derivative, $u'(\xi_i)$, at these same nodes can be computed exactly via a matrix-vector product:

$$
u'(\xi_i) = \sum_{j=1}^{n} D_{ij} u_j
$$

Here, $D$ is the $n \times n$ **one-dimensional [differentiation matrix](@entry_id:149870)**, whose entries are given by $D_{ij} = \ell_j'(\xi_i)$, where $\ell_j$ is the $j$-th Lagrange basis polynomial. This operation is a single contraction, forming the fundamental building block of sum factorization. For example, for $p=4$ ($n=5$) on Gauss-Lobatto-Legendre nodes, one can explicitly construct the matrix $D$ and verify that it exactly differentiates any polynomial up to degree 4 [@problem_id:3422352].

**Extension to Higher Dimensions**

Now, consider a function $u(\xi, \eta, \zeta) \in Q_p$ in three dimensions, represented by its nodal values $U_{ijk}$ on an $n \times n \times n$ tensor-product grid. To compute its partial derivative with respect to $\xi$ at the grid points, we differentiate its [series representation](@entry_id:175860) and evaluate at a node $(\xi_a, \eta_b, \zeta_c)$:

$$
\partial_{\xi} u(\xi_a, \eta_b, \zeta_c) = \sum_{i,j,k} U_{ijk} \ell_i'(\xi_a) \ell_j(\eta_b) \ell_k(\zeta_c)
$$

Due to the Kronecker delta property of the Lagrange basis, $\ell_j(\eta_b) = \delta_{jb}$ and $\ell_k(\zeta_c) = \delta_{kc}$, the summations over $j$ and $k$ collapse, leaving:

$$
(\partial_{\xi} U)_{abc} = \sum_{i=1}^{n} U_{ibc} \ell_i'(\xi_a) = \sum_{i=1}^{n} (D_{\xi})_{ai} U_{ibc}
$$

This remarkable result shows that the 3D differentiation is not a monolithic operation. Instead, it is a series of 1D differentiations. For each fixed pair of indices $(b,c)$, we take the "pencil" of data along the $\xi$-axis and multiply it by the small 1D [differentiation matrix](@entry_id:149870) $D_{\xi}$. Since there are $n^2$ such pencils, the total work is $n^2$ applications of an $n \times n$ matrix, not one application of an $n^3 \times n^3$ matrix [@problem_id:3422353].

**The Algebraic Viewpoint: Kronecker Products**

The efficiency of sum factorization has a firm algebraic foundation in the properties of the **Kronecker product**. If the nodal values of $u$ are flattened into a single vector $\mathbf{u}$ of length $n^d$, the operator for [partial differentiation](@entry_id:194612) with respect to coordinate $k$, $\mathcal{D}_k$, can be written as a Kronecker product of 1D matrices:

$$
\mathcal{D}_k = I \otimes \cdots \otimes I \otimes D^{(k)} \otimes I \otimes \cdots \otimes I
$$

where $D^{(k)}$ is the 1D [differentiation matrix](@entry_id:149870) for the $k$-th coordinate and $I$ is the $n \times n$ identity matrix. Applying an operator with this structure to a vector is mathematically equivalent to the procedure described above: reshaping the vector into a $d$-dimensional tensor and applying the small matrix $D^{(k)}$ along the $k$-th mode. This avoids ever forming the enormous $n^d \times n^d$ matrix $\mathcal{D}_k$ [@problem_id:3422293].

**Complexity Analysis**

This restructuring of the computation leads to a dramatic reduction in cost. The cost of applying the $n \times n$ matrix $D^{(k)}$ to a single data pencil is $O(n^2)$. Since there are $n^{d-1}$ such pencils in a $d$-dimensional grid, the total cost for differentiation with respect to one coordinate is $O(n^{d-1} \cdot n^2) = O(n^{d+1})$. To compute a full gradient, which involves $d$ such operations, the cost becomes $O(d \cdot n^{d+1})$.

The comparison is stark:
-   **Naive Application:** $O(n^{2d})$
-   **Sum Factorization:** $O(d \cdot n^{d+1})$

For $d>1$, the exponent $d+1$ is strictly less than $2d$. This means that as the polynomial degree $p$ (and thus $n$) increases, the advantage of sum factorization grows immense.

### Application to High-Order Operators: The Stiffness Matrix

The principles of sum factorization extend beyond simple differentiation to the application of more complex operators, such as the element stiffness operator arising from the discretization of a PDE like the Laplace equation, $-\nabla^2 u = f$. The action of the [element stiffness matrix](@entry_id:139369) $K$ on a vector of nodal values $u$, which is a necessary step in [iterative solvers](@entry_id:136910) like Conjugate Gradient, can be performed "matrix-free".

The full operator is a sum of contributions from each spatial direction, $K = \sum_{i=1}^d K_i$. The action of a single directional component, say $K_1 u$, for an isotropic Laplacian on a reference element involves a sequence of three sum-factorized steps:
1.  Apply the 1D derivative matrix $D$ along dimension 1 to all data pencils.
2.  Multiply the result pointwise by the [tensor-product quadrature](@entry_id:145940) weights.
3.  Apply the transpose of the derivative matrix, $D^T$, along dimension 1 to all resulting data pencils.

This process is repeated and accumulated for all $d$ directions.

#### A Quantitative Cost Comparison

A detailed analysis of the computational costs further highlights the superiority of the sum-factorized, matrix-free approach [@problem_id:3422311], [@problem_id:3422300].

**Floating-Point Operations (FLOPs):**
Let $n=p+1$. The FLOP count for applying the full stiffness operator scales as:
-   **Dense Matrix Application:** $F_{\text{dense}}(n,d) = O(n^{2d})$
-   **Sum Factorization Application:** $F_{\text{sf}}(n,d) = O(d \cdot n^{d+1})$

For a 3D problem ($d=3$), the costs are $O(n^6)$ versus $O(n^4)$. To find the break-even point where sum factorization becomes cheaper, we can set the detailed operation counts equal: $2n^6 = 12n^4 + 6n^3$. Solving this for $n>1$ yields a root between 2 and 3. This implies that for any polynomial degree $p \ge 2$ ($n \ge 3$), the sum factorization approach is already more efficient in terms of raw computations. For high $p$, the difference is astronomical.

**Memory Traffic:**
The most significant advantage of the matrix-free approach is often the reduction in memory usage.
-   **Dense Matrix Storage:** Requires storing the $n^d \times n^d$ matrix, which costs $O(n^{2d})$ memory locations.
-   **Sum Factorization Storage:** Avoids storing the large matrix entirely. It only requires storing the small 1D operators ($O(d n^2)$) and geometric/quadrature data at the grid points ($O(n^d)$).

For a 3D problem with $p=15$ ($n=16$), the [dense matrix](@entry_id:174457) requires $(16^3)^2 \approx 16.7$ million double-precision numbers per element, equating to over 134 MB. The sum factorization approach requires storing only a few small matrices and grid data, totaling on the order of $16^3 \approx 4096$ numbers, a reduction factor of thousands [@problem_id:3422311], [@problem_id:3422300]. This makes high-order computations feasible on systems with limited memory.

It is crucial to note that while [matrix-free methods](@entry_id:145312) dramatically reduce the cost *per iteration* of a solver, they do not change the underlying mathematical operator. Therefore, the number of iterations required for a Krylov solver to converge is identical for both the matrix-based and matrix-free implementations of the same discretization [@problem_id:3422300].

### Practical Considerations and Algorithmic Variants

The core mechanism of sum factorization can be adapted and optimized based on the choice of basis, quadrature rule, and stability requirements.

#### Nodal versus Modal Bases

As mentioned, both nodal and modal bases are built on tensor products and support sum factorization. The transformation from a vector of [modal coefficients](@entry_id:752057) to a vector of nodal values is itself a separable operation. The $d$-dimensional transform matrix is the Kronecker product of the 1D Vandermonde matrix $V^{(1)}$ (whose entries are $L_a(\xi_i)$). Consequently, this basis transform can be computed efficiently using sum factorization with a complexity of $O(d(p+1)^{d+1})$. This allows algorithms to switch between representations, for example, to treat nonlinear terms easily in nodal space while leveraging the [diagonal mass matrix](@entry_id:173002) of the [modal basis](@entry_id:752055) in other parts of a calculation [@problem_id:3422289].

#### Collocation and Quadrature Rules

The choice of quadrature rule and its relation to the nodal set has important implications for the implementation of sum factorization [@problem_id:3422344], [@problem_id:3422361].

-   **Collocated Configuration:** A common choice is to use Gauss-Lobatto-Legendre (GLL) points for both the nodal locations and the quadrature points ($n_q = n_u = p+1$). This is called a **collocated** scheme. Its main advantage is simplicity: the interpolation from nodes to quadrature points becomes the identity operation and can be omitted from the sum factorization algorithm. However, an $n$-point GLL rule is only exact for polynomials of degree up to $2n-3 = 2p-1$. This is sufficient to integrate the stiffness matrix exactly for constant-coefficient problems (integrand degree $2p-2$) but not the [mass matrix](@entry_id:177093) (integrand degree $2p$). This under-integration, however, results in a diagonal, or "lumped", [mass matrix](@entry_id:177093), which can be highly advantageous in time-dependent problems.

-   **Non-collocated Configuration:** To improve accuracy, one can use a more precise [quadrature rule](@entry_id:175061), such as Gauss-Legendre (GL), which is exact for polynomials up to degree $2n-1 = 2p+1$. If the nodes remain at GLL points, the scheme is **non-collocated**. This configuration can exactly integrate both [mass and stiffness matrices](@entry_id:751703) for constant coefficients and can handle variable coefficients of higher degree before aliasing errors occur [@problem_id:3422361]. The price is increased [computational complexity](@entry_id:147058): the sum factorization algorithm must now include explicit, non-trivial steps for interpolating data from the nodal grid (GLL) to the quadrature grid (GL) and projecting it back. While the asymptotic scaling remains $O(d n^{d+1})$, the constant factor is larger.

These choices also affect face integrals in DG methods. A GLL volume basis naturally has nodes on the element faces, which can be made to coincide with a GLL face [quadrature rule](@entry_id:175061), again avoiding interpolation. A GL volume basis has no nodes on the faces, necessitating an interpolation step to evaluate terms on the boundary [@problem_id:3422344].

#### Numerical Stability

The repeated application of differentiation matrices in sum factorization, especially in [time-stepping schemes](@entry_id:755998), raises concerns about numerical stability. We can quantify this by analyzing the [amplification factor](@entry_id:144315) of the 1D differentiation operator, defined in the supremum norm as $\mathcal{A}_p = \sup_{u \in P_p} \frac{\|u'\|_{\infty}}{\|u\|_{\infty}}$. A classic result from approximation theory, **Markov's inequality**, states that for any polynomial $u$ of degree $p$ on $[-1,1]$, $\|u'\|_{\infty} \le p^2 \|u\|_{\infty}$. This bound is sharp and is achieved by the Chebyshev polynomials.

Therefore, the [amplification factor](@entry_id:144315) is $\mathcal{A}_p = p^2$. An operator composed of $d$ such transformations could amplify errors by as much as $(p^2)^d$. This growth, which is very rapid for high $p$, can lead to instability. To ensure dimension-independent stability, one can introduce a simple scaling. By multiplying each 1D differentiation operator by a scaling factor of $s(p) = 1/p^2$, the resulting scaled operator becomes non-expansive in the [supremum norm](@entry_id:145717), i.e., its amplification factor is at most 1. This guarantees that repeated applications will not unboundedly amplify initial errors [@problem_id:3422336].

### Beyond the Ideal Case: Adapting Sum Factorization

The power of sum factorization is most apparent for operators with separable coefficients on tensor-product elements. However, its principles can be extended to more complex scenarios.

#### Non-Separable Coefficients

Many real-world problems involve variable material properties, leading to a [diffusion operator](@entry_id:136699) with a non-separable coefficient $a(\boldsymbol{\xi})$. In this case, the pointwise multiplication by $a(\boldsymbol{\xi})$ in the operator application breaks the perfect Kronecker product structure. A powerful strategy to recover efficiency is to approximate the coefficient function with a **low-rank separated representation**:

$$
a(\boldsymbol{\xi}) \approx a_R(\boldsymbol{\xi}) = \sum_{r=1}^R \prod_{k=1}^d a_k^{(r)}(\xi_k)
$$

This represents the coefficient as a short sum of separable terms. Such an approximation can be found using [tensor decomposition](@entry_id:173366) techniques like the Canonical Polyadic (CP) or Tensor-Train (TT) decompositions. The stiffness operator then becomes a sum of $R$ Kronecker-structured terms. Each term can be applied efficiently via sum factorization, leading to a total complexity of $O(R \cdot d \cdot n^{d+1})$. If a good [low-rank approximation](@entry_id:142998) exists (i.e., $R$ is small), this approach largely restores the benefits of sum factorization. Careful control of the [approximation error](@entry_id:138265) is necessary to ensure the stability and accuracy of the overall scheme [@problem_id:3422304].

#### Non-Tensor-Product Elements

For geometrically complex domains, meshes may contain non-tensor-product elements like triangles and tetrahedra ([simplices](@entry_id:264881)). The natural [polynomial space](@entry_id:269905) on these elements is the total-degree space $P_p$, which, as discussed, lacks a pure tensor-product structure due to the coupled index constraint (e.g., $i+j+k \le p$ for a tetrahedron).

Standard sum factorization is not directly applicable. However, the underlying idea of decomposing multi-dimensional operations can be adapted through a **partial sum-factorization** strategy. By using a "collapsed coordinate" mapping from a cube to the simplex and employing special hierarchical, orthogonal polynomial bases (e.g., based on Jacobi polynomials), the operator application can be structured as a sequence of 1D-like transforms with triangularly shrinking index ranges. This leads to an operation count for the volume term operator of $O(p^4)$ on tetrahedra and $O(p^3)$ for face terms. While not as efficient as on hexahedra (where volume terms are also $O(p^4)$ but with smaller constants), this is still a vast improvement over naive methods and makes high-order methods on tetrahedral meshes computationally viable [@problem_id:3422299].