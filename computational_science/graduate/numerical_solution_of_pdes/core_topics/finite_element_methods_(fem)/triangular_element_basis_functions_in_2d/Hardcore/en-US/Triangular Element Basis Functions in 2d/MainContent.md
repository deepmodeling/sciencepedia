## Introduction
In the vast field of computational science, the finite element method (FEM) stands as a cornerstone for simulating complex physical phenomena governed by partial differential equations (PDEs). A fundamental challenge in applying FEM is accurately representing solutions on intricate two-dimensional domains, a problem elegantly solved through triangulation. However, this raises a critical question: how do we define functions on these simple triangular building blocks in a way that is mathematically sound and computationally efficient? This article addresses this gap by providing a comprehensive exploration of triangular element basis functions, the very language of the finite element method.

You will embark on a structured journey through this essential topic. The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork, introducing barycentric coordinates and demonstrating how to construct the ubiquitous linear and higher-order Lagrange elements. It delves into the crucial concept of conformity, explaining what makes a finite element space mathematically valid for solving second-order PDEs. The second chapter, **Applications and Interdisciplinary Connections**, showcases the immense versatility of these constructs, exploring their central role in computational mechanics, their connection to computer-aided design, and their adaptation in advanced frameworks like mixed, non-conforming, and discontinuous Galerkin methods. Finally, the **Hands-On Practices** chapter provides an opportunity to solidify your understanding by tackling concrete problems related to the construction and properties of these essential functions.

## Principles and Mechanisms

In the numerical solution of partial differential equations (PDEs) using the finite element method (FEM), the choice of basis functions is paramount. These functions, defined locally on each element of a mesh, dictate the approximation power of the method, the continuity properties of the global solution, and the structure of the resulting algebraic system. For two-dimensional problems defined on complex geometries, triangular elements offer exceptional flexibility. This chapter delves into the fundamental principles and mechanisms governing the construction and application of basis functions on triangular elements, starting from the simplest linear case and extending to higher-order polynomials and vector-valued formulations.

### The Foundation: Barycentric Coordinates and Linear Basis Functions

The natural language for describing locations and functions on a triangle is not the global Cartesian system, but an intrinsic system known as **barycentric coordinates**. For any non-degenerate triangle $T$ with vertices $\boldsymbol{x}_1, \boldsymbol{x}_2, \boldsymbol{x}_3$, any point $\boldsymbol{x} \in T$ can be uniquely expressed as an affine combination of the vertices:
$$
\boldsymbol{x} = \lambda_1(\boldsymbol{x})\boldsymbol{x}_1 + \lambda_2(\boldsymbol{x})\boldsymbol{x}_2 + \lambda_3(\boldsymbol{x})\boldsymbol{x}_3
$$
subject to the constraint that the coefficients sum to unity, $\lambda_1(\boldsymbol{x}) + \lambda_2(\boldsymbol{x}) + \lambda_3(\boldsymbol{x}) = 1$. The three functions $\lambda_1, \lambda_2, \lambda_3$ are the barycentric coordinates of the point $\boldsymbol{x}$. They are affine (linear plus a constant) functions of the Cartesian coordinates and possess several crucial geometric properties:
1.  **Vertex Property**: At a vertex $\boldsymbol{x}_j$, the corresponding barycentric coordinate is one, while the others are zero. That is, $\lambda_i(\boldsymbol{x}_j) = \delta_{ij}$, where $\delta_{ij}$ is the Kronecker delta.
2.  **Edge Property**: Along the edge of the triangle opposite to vertex $\boldsymbol{x}_i$, the coordinate $\lambda_i$ is identically zero.
3.  **Interior Property**: For any point $\boldsymbol{x}$ strictly inside the triangle, all three barycentric coordinates are strictly positive: $\lambda_i(\boldsymbol{x}) > 0$ for $i=1,2,3$.

These properties make barycentric coordinates ideal for constructing **nodal basis functions** for the space of linear polynomials, denoted $\mathbb{P}_1(T)$. If we define a set of local basis functions, often called shape functions, as $N_i := \lambda_i$ for $i=1,2,3$, we see that they satisfy the nodal interpolation property $N_i(\boldsymbol{x}_j) = \delta_{ij}$. This means that the function $N_i$ is equal to $1$ at node $i$ and $0$ at all other nodes. Any linear function $p(\boldsymbol{x}) \in \mathbb{P}_1(T)$ can then be written as a linear combination of these basis functions, with the coefficients being the function's values at the vertices:
$$
p(\boldsymbol{x}) = p(\boldsymbol{x}_1)N_1(\boldsymbol{x}) + p(\boldsymbol{x}_2)N_2(\boldsymbol{x}) + p(\boldsymbol{x}_3)N_3(\boldsymbol{x})
$$
These functions, $\{N_i = \lambda_i\}_{i=1}^3$, form the basis for the ubiquitous **linear Lagrange triangular element** [@problem_id:3458212].

### Conformity in $H^1(\Omega)$: The Requirement of Continuous Traces

In the context of solving second-order PDEs like the Poisson equation, the solution space is typically the Sobolev space $H^1(\Omega)$, which consists of functions that are square-integrable and have square-integrable first-order weak derivatives. A finite element method is said to be **conforming** if the discrete space of trial and test functions is a true subspace of the continuous solution space, e.g., $V_h \subset H^1(\Omega)$.

For a function built by "stitching together" polynomials on a mesh of triangles, a critical question arises: what condition ensures the global function belongs to $H^1(\Omega)$? The answer lies in the definition of the weak derivative. Applying element-wise integration by parts (Green's identity) to the definition of a weak derivative reveals that the global weak derivative of a piecewise polynomial function is equal to its piecewise classical derivative if and only if the sum of all boundary integrals involving jumps in the function's value vanishes [@problem_id:3458257]. For this to hold for arbitrary test functions, the jump in the function value must be zero across every interior edge of the mesh. In other words, an $H^1$-conforming finite element space must be composed of functions that are globally continuous, a property known as $C^0$ continuity.

The linear Lagrange element elegantly satisfies this requirement. The restriction of a linear function $N_i$ to any edge of the triangle is a one-dimensional linear polynomial. Such a 1D polynomial is uniquely determined by its values at the two endpoints of the edge. When two adjacent triangles, $T_1$ and $T_2$, share an edge, they also share the two vertices at its ends. By constructing the global basis functions such that they are associated with the global mesh vertices, the nodal values at shared vertices are single-valued by definition. This ensures that the linear traces of the function from both $T_1$ and $T_2$ match at the endpoints, and therefore must be identical along the entire shared edge [@problem_id:3458212]. This guarantees the required $C^0$ continuity for $H^1$-conformity.

The necessity of this continuity can be starkly illustrated by considering a non-conforming construction. Imagine two adjacent triangles, $T_L$ and $T_R$, where we use linear ($P_1$) elements on $T_L$ but quadratic ($P_2$) elements on $T_R$. If we only enforce continuity at the shared vertices but allow the additional midpoint node on the shared edge from $T_R$ to be independent, we create a "hanging node". A function can be constructed that is zero at both vertices but has a value of $1$ at the midpoint node. Its trace from $T_L$ will be identically zero, while its trace from $T_R$ will be a non-zero quadratic "bubble" function. This creates a jump discontinuity, violating $H^1$-conformity and leading to an inconsistent numerical method that may not converge to the correct solution [@problem_id:3458224]. Such situations can be remedied, either by enforcing kinematic constraints (e.g., setting the midpoint value to be the average of the vertex values) or by using more advanced techniques like discontinuous Galerkin or mortar methods that modify the variational formulation to handle the jumps [@problem_id:3458224].

### Generalization to Higher-Order Lagrange Elements

The principles of Lagrange interpolation can be extended to construct basis functions for higher-degree polynomial spaces, $\mathbb{P}_k(T)$, which consist of all polynomials of total degree at most $k$. The dimension of this space is given by $\dim(\mathbb{P}_k) = \frac{(k+1)(k+2)}{2}$. This space is spanned by the set of **barycentric monomials** of the form $\lambda_1^a\lambda_2^b\lambda_3^c$ where the non-negative integers $a, b, c$ sum to $k$ [@problem_id:3458231].

To construct a nodal basis for $\mathbb{P}_k(T)$, one must first define a **unisolvent** set of nodes—a set of $\dim(\mathbb{P}_k)$ points such that any polynomial in $\mathbb{P}_k(T)$ is uniquely determined by its values at these points. For Lagrange elements, these nodes are typically arranged in a regular lattice on the triangle.

Let's examine the quadratic case, $k=2$, where $\dim(\mathbb{P}_2)=6$. The standard set of nodes for the $P_2$ element consists of the three vertices and the three midpoints of the edges. A nodal basis function associated with a given node must be a quadratic polynomial that is equal to $1$ at that node and $0$ at the other five nodes.

This property provides a direct way to construct the basis functions. For example, consider the basis function $N_{12}^{(e)}$ associated with the midpoint of the edge connecting vertices $\boldsymbol{x}_1$ and $\boldsymbol{x}_2$. This function must be zero at all other five nodes, including the vertices $\boldsymbol{x}_3$ and all nodes on the other two edges. The edge opposite $\boldsymbol{x}_1$ is the line where $\lambda_1=0$, and the edge opposite $\boldsymbol{x}_2$ is where $\lambda_2=0$. A simple quadratic polynomial that vanishes on both these lines is the product $\lambda_1 \lambda_2$. Let's test this: it is zero at all vertices (since at least one of $\lambda_1$ or $\lambda_2$ is zero) and at the midpoints of the other two edges (where either $\lambda_1=0$ or $\lambda_2=0$). It is non-zero at the target midpoint, whose barycentric coordinates are $(\frac{1}{2}, \frac{1}{2}, 0)$. To ensure the function is $1$ at this node, we simply normalize it.
$$
N_{12}^{(e)}(\lambda_1, \lambda_2, \lambda_3) = C \cdot \lambda_1 \lambda_2
$$
$$
1 = C \cdot \left(\frac{1}{2}\right)\left(\frac{1}{2}\right) \implies C=4
$$
Thus, the basis function for the edge 1-2 midpoint is $N_{12}^{(e)} = 4\lambda_1\lambda_2$ [@problem_id:3458231]. A similar logic can be used to construct the basis functions for the vertices. The function for vertex $\boldsymbol{x}_1$, $N_1^{(v)}$, must vanish on the opposite edge ($\lambda_1=0$) and at the midpoints of the two adjacent edges. The line passing through these two midpoints has the equation $2\lambda_1 - 1 = 0$. The product of these two linear factors, $\lambda_1(2\lambda_1-1)$, gives a quadratic that vanishes at the required five nodes. After normalization, we find $N_1^{(v)} = \lambda_1(2\lambda_1-1)$.

The full set of six basis functions for the $P_2$ Lagrange element is:
-   **Vertex functions**: $N_i^{(v)} = \lambda_i(2\lambda_i - 1)$ for $i=1,2,3$.
-   **Edge functions**: $N_{ij}^{(e)} = 4\lambda_i\lambda_j$ for $\{i,j\} \in \{\{1,2\}, \{2,3\}, \{3,1\}\}$.

By evaluating each of these six functions at each of the six nodes, one can verify that they form a nodal basis, as the resulting evaluation matrix is the identity matrix [@problem_id:3458226]. The principle of $H^1$-conformity extends directly: the trace of a $P_k$ polynomial on an edge is a 1D polynomial of degree $k$, which is uniquely determined by the $k+1$ nodes on that edge. Sharing these nodes between adjacent elements guarantees trace continuity [@problem_id:3458257].

### Practical Implementation: The Role of the Reference Element

To avoid re-deriving basis functions and re-computing integrals for every uniquely shaped triangle in a mesh, practical FEM implementations perform most computations on a single, fixed **reference element**, $\hat{T}$. A common choice for $\hat{T}$ is the right triangle with vertices at $(0,0)$, $(1,0)$, and $(0,1)$ in a reference coordinate system $(\hat{\xi}, \hat{\eta})$.

Any physical triangle $T$ in the mesh can be generated from $\hat{T}$ via an **affine map** $\boldsymbol{x} = F(\hat{\boldsymbol{x}}) = J\hat{\boldsymbol{x}} + \boldsymbol{b}$, where $J$ is a constant $2 \times 2$ **Jacobian matrix** and $\boldsymbol{b}$ is a translation vector. The columns of $J$ and the vector $\boldsymbol{b}$ are determined by mapping the vertices of $\hat{T}$ to the vertices of $T$ [@problem_id:3458228]. This mapping is the cornerstone of FEM implementation, as it allows us to relate integrals and derivatives between the physical and reference domains.

The **change of variables** theorem relates integrals over $T$ and $\hat{T}$:
$$
\int_{T} f(\boldsymbol{x}) \, d\boldsymbol{x} = \int_{\hat{T}} f(F(\hat{\boldsymbol{x}})) |\det J| \, d\hat{\boldsymbol{x}}
$$
The term $|\det J|$ is a constant scaling factor that relates the area of the two triangles: $|\det J| = |T|/|\hat{T}|$. For the standard reference triangle with area $|\hat{T}| = 1/2$, this means $|\det J| = 2|T|$ [@problem_id:3458228].

Similarly, derivatives transform according to the multivariate chain rule. The gradient of a function $N$ in physical coordinates, $\nabla_{\boldsymbol{x}} N$, is related to the gradient of its counterpart $\hat{N}$ on the reference element, $\nabla_{\hat{\boldsymbol{x}}} \hat{N}$, by the inverse-transpose of the Jacobian:
$$
\nabla_{\boldsymbol{x}} N = J^{-T} \nabla_{\hat{\boldsymbol{x}}} \hat{N}
$$
This transformation, sometimes called a **Piola transform**, is crucial. It correctly accounts for the geometric distortion (stretching, shearing, rotation) introduced by the map $F$. The inverse relationship shows, for example, that if an element is stretched in one direction (large corresponding entry in $J$), the rate of change of a function in that direction will decrease (small corresponding entry in $J^{-1}$) [@problem_id:3458204].

These two transformation rules allow us to compute the fundamental element matrices, the mass matrix ($M_{ij} = \int_T N_i N_j \,dx$) and the stiffness matrix ($S_{ij} = \int_T \nabla N_i \cdot \nabla N_j \,dx$), entirely on the reference element, where the basis functions $\hat{N}_i$ and their gradients $\nabla_{\hat{\boldsymbol{x}}} \hat{N}_i$ are fixed and known:
$$
M_{ij} = |\det J| \int_{\hat{T}} \hat{N}_i(\hat{\boldsymbol{x}}) \hat{N}_j(\hat{\boldsymbol{x}}) \, d\hat{\boldsymbol{x}}
$$
$$
S_{ij} = |\det J| \int_{\hat{T}} (J^{-T} \nabla_{\hat{\boldsymbol{x}}} \hat{N}_i) \cdot (J^{-T} \nabla_{\hat{\boldsymbol{x}}} \hat{N}_j) \, d\hat{\boldsymbol{x}}
$$
The matrix $J^{-T}J^{-1}$ inside the stiffness matrix integral is often referred to as the pullback of the metric tensor.

### Numerical Integration and Quadrature

The integrals over the reference element are typically computed using **numerical quadrature**. A quadrature rule approximates an integral by a weighted sum of function evaluations at specific points. A rule is said to have a **degree of polynomial exactness** $p$ if it integrates every polynomial of total degree up to $p$ exactly.

To ensure that the element matrices are computed without error, the quadrature rule must be exact for the polynomial degree of the integrand.
-   For the **mass matrix** using $P_k$ elements, the integrand $N_i N_j$ is the product of two polynomials of degree $k$, resulting in a polynomial of degree up to $2k$. Thus, the minimal required exactness is $p_{\text{mass}} = 2k$.
-   For the **stiffness matrix**, the integrand involves products of the components of the gradients, $\nabla N_i \cdot \nabla N_j$. The derivative of a degree-$k$ polynomial is a degree-$(k-1)$ polynomial. The product of two such derivatives is therefore a polynomial of degree up to $(k-1) + (k-1) = 2k-2$. The minimal required exactness is $p_{\text{stiff}} = 2k-2$ [@problem_id:3458240].

Choosing a quadrature rule with at least this degree of exactness is essential for preserving the theoretical accuracy of the finite element method.

### Beyond $H^1$-Conformity: Alternative Element Formulations

While $H^1$-conforming Lagrange elements are the workhorses of FEM for scalar second-order PDEs, other problems and contexts demand different types of basis functions.

#### Non-conforming $H^1$ Elements
In some applications, strict $C^0$ continuity can be relaxed. The **Crouzeix–Raviart (CR) element** is a classic example of a non-conforming element. It uses the same local polynomial space as the linear Lagrange element, $\mathbb{P}_1(T)$, but defines its degrees of freedom at the **midpoints of the edges**. The basis function associated with edge $e_i$ is $\phi_i = 1-2\lambda_i$. For a linear polynomial, the value at the midpoint is identical to its average value over the edge [@problem_id:3458249].

When CR elements are assembled, continuity is only enforced for the midpoint values (or edge averages). This is not sufficient to guarantee pointwise continuity along the entire edge. A CR function can have a jump across an interior edge, meaning the CR space is not a subspace of $H^1(\Omega)$. However, the jump is specifically constructed to have a zero average over the edge. This property is just enough to ensure consistency and convergence for certain problems, making the CR element a useful tool, particularly in computational fluid dynamics [@problem_id:3458249].

#### $H(\text{div})$-conforming Elements
For problems involving vector fields, such as fluxes or velocities, the relevant function space is often $H(\text{div}, \Omega)$, which contains vector-valued functions $\boldsymbol{v}$ such that both $\boldsymbol{v}$ and its divergence $\nabla \cdot \boldsymbol{v}$ are square-integrable. Conformity in this space requires the continuity of the **normal component** ($\boldsymbol{v} \cdot \boldsymbol{n}$) across inter-element edges.

The lowest-order **Raviart-Thomas element**, denoted $RT_0$, is designed to achieve this. The local function space on a triangle $T$ consists of vector fields of the form $\boldsymbol{v}(\boldsymbol{x}) = \boldsymbol{a} + b\boldsymbol{x}$, where $\boldsymbol{a} \in \mathbb{R}^2$ is a vector and $b \in \mathbb{R}$ is a scalar. The degrees of freedom are the normal fluxes across the three edges, $\int_{e_i} \boldsymbol{v} \cdot \boldsymbol{n}_i \, ds$. The basis function associated with edge $e_i$ (opposite vertex $\boldsymbol{x}_i$) is given by $\boldsymbol{\psi}_i(\boldsymbol{x}) = \frac{1}{2|T|}(\boldsymbol{x} - \boldsymbol{x}_i)$.

A key property of the $RT_0$ space is that the normal component of any function $\boldsymbol{v}$ is constant along each edge. Therefore, enforcing continuity of the integral flux DOF automatically enforces pointwise continuity of the normal component, guaranteeing $H(\text{div})$-conformity [@problem_id:3458232]. These elements are fundamental in mixed finite element methods for problems in fluid mechanics and Darcy flow.

In summary, the design of basis functions on triangular elements is a rich and systematic field. By carefully choosing the local polynomial space and the corresponding degrees of freedom, one can construct elements that satisfy the precise conformity requirements demanded by the underlying partial differential equation, enabling the development of robust and accurate numerical methods.