## Introduction
In the pursuit of accurate and efficient numerical simulations, particularly with high-order spectral and discontinuous Galerkin (DG) methods, the choice of polynomial basis functions is a cornerstone of the entire algorithm. While [simplices](@entry_id:264881)—triangles in 2D and tetrahedra in 3D—offer unparalleled flexibility for [meshing](@entry_id:269463) complex geometries, they present a significant challenge: their geometry lacks the [simple tensor](@entry_id:201624)-product structure of quadrilaterals, making the construction of stable and efficient polynomial bases a non-trivial task. Using a naive monomial basis leads to dense, ill-conditioned matrices that cripple numerical stability and performance, creating a critical knowledge gap that must be addressed for robust [high-order methods](@entry_id:165413).

This article provides a comprehensive exploration of orthogonal polynomial bases on simplices, demonstrating how they overcome these challenges to enable powerful computational tools. Across the following chapters, you will gain a deep understanding of this essential topic:

- **Principles and Mechanisms** will lay the theoretical foundation, explaining why orthogonality is paramount for diagonalizing the mass matrix and exploring robust construction methods like the Koornwinder-Dubiner basis that sidestep the pitfalls of the Gram-Schmidt process.
- **Applications and Interdisciplinary Connections** will bridge theory and practice, showing how these bases are leveraged within DG methods to achieve computational speed-ups via sum-factorization and to design stable schemes for problems in fluid dynamics and electromagnetism.
- **Hands-On Practices** will guide you through the practical implementation of these concepts, from building a canonical Dubiner basis to constructing specialized bases for weighted inner products and analyzing their properties.

## Principles and Mechanisms

In the implementation of high-order spectral and discontinuous Galerkin (DG) methods, the choice of polynomial basis functions within each element is a decision of paramount importance. This choice profoundly influences the structure of the resulting discrete system, its numerical stability, and the overall [computational efficiency](@entry_id:270255) of the scheme. While [simplices](@entry_id:264881)—triangles in two dimensions and tetrahedra in three—are highly versatile for meshing complex geometries, they lack the tensor-product structure of quadrilaterals and hexahedra, which complicates the construction of efficient and stable basis functions. This chapter delves into the principles governing the construction and application of orthogonal polynomial bases on [simplices](@entry_id:264881), which are indispensable for the development of robust [high-order methods](@entry_id:165413).

### Foundations of Polynomial Approximation on Simplices

#### The Case Against Monomials

A seemingly natural choice for a basis for the space of polynomials of total degree at most $N$ on an element $K$ is the set of monomials. For a triangle in the $xy$-plane, this would be the set $\{x^i y^j : i,j \ge 0, i+j \le N\}$. These functions are simple to write down and their derivatives are easy to compute. However, for the purposes of Galerkin methods, this basis possesses a critical flaw: its elements are not mutually orthogonal with respect to the standard $L^2$ inner product.

The **$L^2$ inner product** of two real-valued functions $f$ and $g$ over a domain $K$ is defined as:
$$
\langle f, g \rangle_K = \int_K f(\mathbf{x}) g(\mathbf{x}) \, d\mathbf{x}
$$
A set of functions $\{\phi_k\}$ is said to be **orthogonal** if the inner product of any two distinct functions in the set is zero, i.e., $\langle \phi_i, \phi_j \rangle_K = 0$ for all $i \neq j$. Furthermore, for any non-zero function $\phi_i$ in an orthogonal set, its squared norm $\langle \phi_i, \phi_i \rangle_K$ must be strictly positive. [@problem_id:3407074] If, in addition, the norm of every basis function is unity, i.e., $\langle \phi_i, \phi_i \rangle_K = 1$ for all $i$, the basis is termed **orthonormal**, a property succinctly expressed as $\langle \phi_i, \phi_j \rangle_K = \delta_{ij}$, where $\delta_{ij}$ is the Kronecker delta.

The monomial basis fails the [orthogonality condition](@entry_id:168905). To see this, consider the two simplest non-constant monomials, $1$ and $x$, on the standard reference triangle $\widehat{T} = \{(x,y) : x \ge 0, y \ge 0, x+y \le 1\}$. Their inner product is:
$$
\langle 1, x \rangle_{\widehat{T}} = \int_0^1 \int_0^{1-x} x \, dy \, dx = \int_0^1 x(1-x) \, dx = \left[ \frac{x^2}{2} - \frac{x^3}{3} \right]_0^1 = \frac{1}{6}
$$
Since this inner product is non-zero, the functions are not orthogonal. In general, the inner products of most pairs of distinct monomials are non-zero. [@problem_id:3407019] This [non-orthogonality](@entry_id:192553) leads to a Gram matrix (the matrix of inner products, also known as the [mass matrix](@entry_id:177093)) that is dense and, for high polynomial degrees, severely ill-conditioned. The practical consequences are twofold: numerical instability, where small [rounding errors](@entry_id:143856) can be greatly amplified, and computational inefficiency, as [solving linear systems](@entry_id:146035) involving dense, ill-conditioned matrices is expensive. This motivates the search for alternative bases that are orthogonal by construction.

#### Polynomial Spaces and Their Dimensions

Before constructing such bases, we must first precisely define the function spaces we are working with. For a simplex $K$ (a triangle or tetrahedron), the natural [polynomial space](@entry_id:269905) is the space of total degree at most $N$, denoted $P^N(K)$. In two dimensions, this is:
$$
P^N(K) = \left\{ p(x,y) = \sum_{i,j \ge 0, \, i+j \le N} a_{ij} x^i y^j \right\}
$$
The dimension of this space is the number of distinct monomials $x^i y^j$ that satisfy the condition on the exponents. This is a classic combinatorial problem: counting the number of [non-negative integer solutions](@entry_id:261624) to the inequality $i+j \le N$. By introducing a [slack variable](@entry_id:270695) $k = N - (i+j)$, this is equivalent to finding the number of [non-negative integer solutions](@entry_id:261624) to the equation $i+j+k=N$. Using a "[stars and bars](@entry_id:153651)" argument, this is the number of ways to arrange $N$ items (stars) in $3$ bins, which is given by the [binomial coefficient](@entry_id:156066) $\binom{N+3-1}{3-1} = \binom{N+2}{2}$.

Therefore, the dimension of the [polynomial space](@entry_id:269905) on a triangle is:
$$
\dim P^N(\text{triangle}) = \frac{(N+1)(N+2)}{2}
$$
By a similar argument for a tetrahedron in three dimensions ($i+j+k \le N$), the dimension is $\dim P^N(\text{tetrahedron}) = \binom{N+3}{3} = \frac{(N+1)(N+2)(N+3)}{6}$.

It is instructive to contrast this with the [polynomial space](@entry_id:269905) typically used on quadrilaterals, the tensor-product space $Q^N(S)$:
$$
Q^N(S) = \left\{ q(x,y) = \sum_{i=0}^N \sum_{j=0}^N b_{ij} x^i y^j \right\}
$$
Here, the exponents $i$ and $j$ can each range from $0$ to $N$ independently. There are $(N+1)$ choices for $i$ and $(N+1)$ choices for $j$, giving a total dimension of $\dim Q^N(\text{square}) = (N+1)^2$. [@problem_id:3407064] The simplicity of this tensor-product structure is key to the relative ease of constructing orthogonal bases on quadrilaterals and hexahedra. Our challenge is to find an analogous structure for [simplices](@entry_id:264881).

### The Role of Orthogonality in Galerkin Methods

The primary motivation for using orthogonal bases in DG methods stems from their effect on the **element mass matrix**. For a given basis $\{\phi_j\}$ on an element $K$, the mass matrix entries are defined by the inner products of the basis functions:
$$
M_{ij}^{(K)} = \langle \phi_i, \phi_j \rangle_K = \int_K \phi_i(\mathbf{x}) \phi_j(\mathbf{x}) \, d\mathbf{x}
$$
In an [explicit time-stepping](@entry_id:168157) scheme for a time-dependent problem, each step requires solving a linear system of the form $M^{(K)} \dot{\mathbf{u}}^{(K)} = \mathbf{r}^{(K)}$, where $\dot{\mathbf{u}}^{(K)}$ is the vector of time derivatives of the [modal coefficients](@entry_id:752057) and $\mathbf{r}^{(K)}$ is the residual vector. Inverting the mass matrix $M^{(K)}$ is a key computational kernel.

If the basis $\{\phi_i\}$ is **orthonormal** on $K$, then by definition $M_{ij}^{(K)} = \delta_{ij}$. The [mass matrix](@entry_id:177093) becomes the identity matrix, $M^{(K)} = I$. In this case, the linear system becomes trivial to solve: $\dot{\mathbf{u}}^{(K)} = \mathbf{r}^{(K)}$. No [matrix inversion](@entry_id:636005) is required. This massive simplification is the central benefit of an orthonormal [modal basis](@entry_id:752055).

#### Geometric Mappings and Their Effect on Inner Products

In practice, computations are not performed on every physical element in the mesh directly. Instead, a canonical **reference element** $\widehat{K}$ (e.g., the unit triangle or tetrahedron) is used, and a geometric mapping $\mathbf{F}_K: \widehat{K} \to K$ relates the [reference element](@entry_id:168425) to each physical element $K$. Basis functions are defined on $\widehat{K}$, and their behavior on $K$ is induced by this mapping.

The transformation of the inner product under this mapping is governed by the [change of variables theorem](@entry_id:160749), which introduces the **Jacobian determinant** of the map, $J_K(\widehat{\mathbf{x}}) = \det(\nabla \mathbf{F}_K(\widehat{\mathbf{x}}))$. The inner product on the physical element $K$ is related to a [weighted inner product](@entry_id:163877) on the reference element $\widehat{K}$:
$$
\langle f, g \rangle_K = \int_K f g \, d\mathbf{x} = \int_{\widehat{K}} (f \circ \mathbf{F}_K)(\widehat{\mathbf{x}}) (g \circ \mathbf{F}_K)(\widehat{\mathbf{x}}) |J_K(\widehat{\mathbf{x}})| \, d\widehat{\mathbf{x}}
$$

**Affine Mappings:** For many meshes, the elements $K$ are simple affine transformations of $\widehat{K}$ (i.e., they are triangles and tetrahedra, not curved shapes). In this case, the mapping is of the form $\mathbf{F}_K(\widehat{\mathbf{x}}) = A\widehat{\mathbf{x}} + \mathbf{b}$, and the Jacobian determinant $J_K = |\det(A)|$ is a positive constant over the entire element. [@problem_id:3407047] The inner product relation simplifies to:
$$
\langle f, g \rangle_K = J_K \int_{\widehat{K}} (f \circ \mathbf{F}_K) (g \circ \mathbf{F}_K) \, d\widehat{\mathbf{x}} = J_K \langle f \circ \mathbf{F}_K, g \circ \mathbf{F}_K \rangle_{\widehat{K}}
$$
Now, suppose we have an orthonormal basis $\{\widehat{\phi}_i\}$ on the reference element $\widehat{K}$, so $\langle \widehat{\phi}_i, \widehat{\phi}_j \rangle_{\widehat{K}} = \delta_{ij}$. Let us define a basis on the physical element $K$ by pullback, $\phi_i = \widehat{\phi}_i \circ \mathbf{F}_K^{-1}$. Then the inner product of these physical basis functions is:
$$
\langle \phi_i, \phi_j \rangle_K = J_K \langle \phi_i \circ \mathbf{F}_K, \phi_j \circ \mathbf{F}_K \rangle_{\widehat{K}} = J_K \langle \widehat{\phi}_i, \widehat{\phi}_j \rangle_{\widehat{K}} = J_K \delta_{ij}
$$
This shows that for an affine element, an orthonormal basis on the [reference element](@entry_id:168425) gives rise to an **orthogonal** (but not orthonormal) basis on the physical element. The resulting physical mass matrix is diagonal: $M^{(K)} = J_K I$. [@problem_id:3407038] Its inverse is simply $(1/J_K)I$, so the computational advantage is retained. To obtain a truly [orthonormal basis](@entry_id:147779) on $K$, one simply needs to scale the basis functions by $J_K^{-1/2}$. [@problem_id:3407047]

**Curvilinear Mappings:** When modeling domains with curved boundaries, we use non-affine, or **curvilinear**, mappings to generate [curved elements](@entry_id:748117). In this case, the Jacobian determinant $J_K(\widehat{\mathbf{x}})$ is no longer constant but varies as a function of position on the reference element. The inner product on $K$ corresponds to an inner product on $\widehat{K}$ with a non-constant weight function $w(\widehat{\mathbf{x}}) = |J_K(\widehat{\mathbf{x}})|$. [@problem_id:3407010]

A basis $\{\widehat{\phi}_i\}$ that is orthonormal with respect to the unweighted inner product on $\widehat{K}$ will not, in general, be orthogonal with respect to this new, [weighted inner product](@entry_id:163877). Consequently, the mass matrix for a curved element, whose entries are $M_{ij}^{(K)} = \int_{\widehat{K}} \widehat{\phi}_i \widehat{\phi}_j |J_K(\widehat{\mathbf{x}})| \, d\widehat{\mathbf{x}}$, will be dense and non-diagonal. [@problem_id:3407056] The simplicity of the [diagonal mass matrix](@entry_id:173002) is lost on [curved elements](@entry_id:748117) when using a standard reference basis.

### Methods for Constructing Orthogonal Bases

#### The Gram-Schmidt Process: A Naive but Instructive Approach

The classical **Gram-Schmidt process** is a general algorithm for converting any set of [linearly independent](@entry_id:148207) vectors into an orthogonal set. One could apply this procedure to the monomial basis $\{x^i y^j z^k : i+j+k \le N\}$ on the reference tetrahedron to generate an orthogonal basis. While theoretically sound, this approach is disastrous in practice for two main reasons.

First, as noted earlier, the monomial basis is notoriously **ill-conditioned**. For high polynomial degrees, the basis functions become nearly linearly dependent in [finite-precision arithmetic](@entry_id:637673). Applying the Gram-Schmidt process to such a set is numerically unstable and leads to a catastrophic [loss of orthogonality](@entry_id:751493) in the resulting basis due to rounding errors. The condition number of the monomial Gram matrix grows exponentially with the polynomial degree $N$. [@problem_id:3407026]

Second, the [computational complexity](@entry_id:147058) is prohibitive. A careful analysis shows that orthogonalizing a basis of size $M = \mathcal{O}(N^3)$ on a tetrahedron using Gram-Schmidt requires $\mathcal{O}(M^2 \cdot Q) = \mathcal{O}((N^3)^2 \cdot N^3) = \mathcal{O}(N^9)$ [floating-point operations](@entry_id:749454), where $Q = \mathcal{O}(N^3)$ is the number of quadrature points needed. [@problem_id:3407026] This high cost makes the method impractical for [high-order discretizations](@entry_id:750302). These severe drawbacks necessitate a more sophisticated and stable construction.

#### The Koornwinder-Dubiner Construction via Duffy's Transform

A far more elegant and robust approach is to construct the basis analytically. The key idea is to map a tensor-product domain, where orthogonal bases are easy to construct, onto the [simplex](@entry_id:270623) of interest. This is achieved using a **Duffy-type transformation**.

Consider the reference triangle $\widehat{T}$. The Duffy map $D: [0,1]^2 \to \widehat{T}$ is given by:
$$
(x,y) = D(u,v) = (u(1-v), v)
$$
This map transforms the unit square in the $(u,v)$-plane to the unit triangle in the $(x,y)$-plane. Its Jacobian matrix is $J_D = \begin{pmatrix} 1-v & -u \\ 0 & 1 \end{pmatrix}$, and its determinant is $\det(J_D) = 1-v$. The integral of a function $f$ over the triangle is thus transformed into a weighted integral over the square: [@problem_id:3407073]
$$
\int_{\widehat{T}} f(x,y) \, dx \, dy = \int_0^1 \int_0^1 f(u(1-v), v) (1-v) \, du \, dv
$$
This is a remarkable result. An integral over a coupled, non-rectangular domain has been transformed into an integral over a simple, rectangular domain. The price is the introduction of the weight function $(1-v)$. The problem of finding an orthogonal polynomial basis on the triangle is now equivalent to finding an [orthogonal basis](@entry_id:264024) on the square with respect to the [weighted inner product](@entry_id:163877) $\langle f, g \rangle_w = \int_0^1 \int_0^1 f g (1-v) \, du \, dv$.

Because the weight depends only on $v$, the integral separates. We need a basis that is orthogonal in $u$ with weight $1$ and orthogonal in $v$ with weight $(1-v)$. This leads directly to the use of one-dimensional **Jacobi polynomials**, $P_n^{(\alpha, \beta)}(z)$, which are orthogonal on $[-1,1]$ with respect to the weight $(1-z)^\alpha (1+z)^\beta$. After appropriate affine scaling of the variables, a suitable orthogonal basis on the square is formed by products of Legendre polynomials (Jacobi with $\alpha=\beta=0$) in the first variable and Jacobi polynomials with $\alpha=1, \beta=0$ in the second variable. This construction results in the celebrated **Dubiner polynomials**, a specific type of **Koornwinder polynomials** for the triangle. [@problem_id:3407049]

This entire procedure can be generalized to three dimensions. A Duffy map from the unit cube $[0,1]^3$ to the reference tetrahedron $\widehat{K}$ is given by:
$$
(x,y,z) = D(u,v,w) = (u(1-v)(1-w), v(1-w), w)
$$
The Jacobian determinant of this map is $|J| = (1-v)(1-w)^2$. [@problem_id:3407023] This again transforms the integral over the tetrahedron to a weighted integral over the cube, which can be handled by a [tensor product](@entry_id:140694) of three different families of 1D Jacobi polynomials.

The resulting Koornwinder-Dubiner bases are orthogonal by construction. Crucially, their evaluation is both efficient and stable, relying on [three-term recurrence](@entry_id:755957) relations for the underlying 1D Jacobi polynomials. The total cost to evaluate all $M = \mathcal{O}(N^3)$ basis functions at $Q = \mathcal{O}(N^3)$ quadrature points is only $\mathcal{O}(M \cdot Q) = \mathcal{O}(N^6)$, a dramatic improvement over the $\mathcal{O}(N^9)$ cost of Gram-Schmidt. Moreover, the construction is numerically stable, avoiding the exponential [ill-conditioning](@entry_id:138674) of the monomial basis. [@problem_id:3407026]

### Advanced Topics and Practical Considerations

#### Restoring Orthogonality on Curved Elements

As established, when using a standard reference basis on a curved element with a non-constant Jacobian $J(\widehat{\mathbf{x}})$, the mass matrix becomes dense. One approach to recover the benefits of orthogonality is to construct, for each curved element, a new basis that is orthogonal with respect to that element's specific Jacobian weight.

This can be achieved by applying the Gram-Schmidt procedure to a stable starting basis (such as the standard Koornwinder basis) using the [weighted inner product](@entry_id:163877) $\langle f, g \rangle_J = \int_{\widehat{K}} f g J(\widehat{\mathbf{x}}) \, d\widehat{\mathbf{x}}$. For this to be done exactly, the integrals involved must be computed exactly. If the original basis is composed of polynomials of degree at most $p$, and the Jacobian $J$ is a polynomial of degree $r$ (as is common in isoparametric mappings), then the integrand $f g J$ is a polynomial of degree at most $2p+r$. Therefore, a quadrature rule exact for polynomials of this degree is required to perform the [orthogonalization](@entry_id:149208) accurately. [@problem_id:3407056]

An equivalent and often more stable approach is algebraic. One first computes the dense weighted mass matrix $M_{ij} = \langle \widehat{\phi}_i, \widehat{\phi}_j \rangle_J$ using the original basis $\widehat{\phi}_i$. Since this matrix is symmetric and positive-definite, it admits a Cholesky factorization $M = LL^T$. The new, [orthogonal basis](@entry_id:264024) can then be expressed as a [linear combination](@entry_id:155091) of the old basis, with the transformation matrix being $L^{-T}$. This matrix-based procedure is a robust way to perform the weighted [orthogonalization](@entry_id:149208). [@problem_id:3407056]

#### Modal vs. Nodal Bases: A Fundamental Trade-off

The discussion so far has centered on **modal bases**, where the degrees of freedom are the coefficients of the expansion in terms of orthogonal polynomials. It is important to contrast this with **nodal bases**, where the basis functions are Lagrange polynomials associated with a set of nodes within the element, and the degrees of freedom are the function values at these nodes.

The choice between these two types of bases involves a fundamental computational trade-off: [@problem_id:3407038]

- **Modal Basis (Orthogonal):** As we have seen, this choice leads to a [diagonal mass matrix](@entry_id:173002) on affine elements, making its inversion trivial. This is a major advantage for [explicit time-stepping](@entry_id:168157). However, computing the [numerical flux](@entry_id:145174) on element faces requires evaluating the polynomial expansion at face quadrature points. This operation corresponds to a dense [matrix-[vector produc](@entry_id:151002)t](@entry_id:156672) (a Vandermonde-like matrix multiplication), which can be computationally intensive.

- **Nodal Basis (Lagrangian):** This choice typically leads to a dense [mass matrix](@entry_id:177093). While it can be approximated by a [diagonal matrix](@entry_id:637782) through a procedure called **[mass lumping](@entry_id:175432)**, this introduces an approximation error. The great advantage of a nodal basis is in the flux computation. If the basis nodes include nodes on the element faces, the solution values needed for the flux are directly available as degrees of freedom, requiring no expensive interpolation or projection.

It is also worth noting that even with an orthonormal [modal basis](@entry_id:752055), other system matrices, such as the **[stiffness matrix](@entry_id:178659)** arising from discretizing second-order operators (e.g., $\int_K \nabla \phi_i \cdot \nabla \phi_j \, d\mathbf{x}$), are generally dense. Orthogonality of the functions does not imply orthogonality of their gradients.

In summary, the construction of orthogonal polynomial bases on [simplices](@entry_id:264881) is a cornerstone of modern, high-order spectral and discontinuous Galerkin methods. While the non-tensor-product nature of [simplices](@entry_id:264881) makes this task more challenging than on quadrilaterals, the development of analytic constructions like the Koornwinder-Dubiner basis provides a pathway to creating methods that are simultaneously efficient, stable, and geometrically flexible.