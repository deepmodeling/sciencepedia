## Introduction
In the pursuit of higher accuracy and computational efficiency within the Finite Element Method (FEM), hierarchical and p-version [shape functions](@entry_id:141015) present a powerful alternative to traditional [mesh refinement](@entry_id:168565). While standard low-order elements improve accuracy by decreasing element size ($h$-refinement), this approach can be computationally prohibitive and inefficient, particularly for problems with smooth solutions or localized singularities. Furthermore, increasing the polynomial degree with standard nodal bases is a cumbersome process, requiring a complete re-formulation of the element basis. This article addresses these limitations by providing a comprehensive exploration of the hierarchical approach, where accuracy is enhanced by increasing the polynomial degree ($p$-refinement) in a structured and efficient manner.

Across the following chapters, you will gain a deep understanding of this advanced FEM technique. We will begin in "Principles and Mechanisms" by dissecting the fundamental theory, exploring how hierarchical functions are constructed in one, two, and three dimensions to create nested approximation spaces. Next, "Applications and Interdisciplinary Connections" will showcase the power of this framework in practice, from enabling intelligent adaptive algorithms and robust multiphysics formulations to unlocking high-performance solver strategies like [static condensation](@entry_id:176722) and [p-multigrid](@entry_id:753055). Finally, "Hands-On Practices" will offer a series of guided problems to translate theoretical knowledge into practical skill. We begin our journey by examining the foundational principles that make this hierarchical construction so elegant and effective.

## Principles and Mechanisms

This chapter delves into the foundational principles and operational mechanisms of [hierarchical shape functions](@entry_id:169076), which are the cornerstone of the $p$-version and $hp$-version of the Finite Element Method (FEM). Building upon the introductory concepts, we will systematically dissect how these functions are constructed, how they ensure inter-[element continuity](@entry_id:165046), and how their unique properties influence the structure of the resulting algebraic systems and enable advanced computational strategies.

### The Hierarchical Principle

The primary goal of higher-order finite elements is to improve approximation accuracy not by refining the mesh size ($h$), but by increasing the polynomial degree ($p$) of the [shape functions](@entry_id:141015) within each element. While standard nodal (Lagrangian) [shape functions](@entry_id:141015) can be constructed for any polynomial degree, they suffer from a practical drawback: changing the polynomial degree requires a complete redefinition of all [shape functions](@entry_id:141015) and degrees of freedom (DOFs) for an element. For instance, transitioning from a linear to a quadratic Lagrangian element discards the original linear basis and introduces a new set of three functions and three nodal values.

Hierarchical bases offer a more elegant and efficient alternative. The core idea is to construct the polynomial approximation space in a nested or **hierarchical** manner. One begins with a low-order basis, typically the standard linear nodal basis, and then systematically augments it with higher-order functions that enrich the approximation without altering the lower-order space or the interpretation of its associated DOFs.

Let us consider the simplest non-trivial case: a one-dimensional quadratic ($p=2$) element on the reference domain $\xi \in [-1, 1]$ . The journey begins with the linear ($p=1$) basis, which consists of the two nodal [shape functions](@entry_id:141015):

$$
N_1(\xi) = \frac{1-\xi}{2}, \quad N_2(\xi) = \frac{1+\xi}{2}
$$

These functions satisfy the familiar Kronecker-delta property at the element's nodes, $\xi_1 = -1$ and $\xi_2 = 1$, i.e., $N_i(\xi_j) = \delta_{ij}$. The linear approximation of a field $u(\xi)$ is $u_h^{(p=1)}(\xi) = d_1 N_1(\xi) + d_2 N_2(\xi)$, where the DOFs $d_1$ and $d_2$ are precisely the nodal values, $u_h(-1)$ and $u_h(1)$.

To create a hierarchical quadratic basis, we augment the linear set $\{N_1, N_2\}$ with a single quadratic function, $N_3(\xi)$, often called an **internal mode** or **[bubble function](@entry_id:179039)**. The [quadratic approximation](@entry_id:270629) is then:

$$
u_h^{(p=2)}(\xi) = d_1 N_1(\xi) + d_2 N_2(\xi) + d_3 N_3(\xi)
$$

The fundamental requirement of the hierarchical principle is that the original DOFs, $d_1$ and $d_2$, must retain their physical meaning as the nodal values of the *new* [quadratic approximation](@entry_id:270629). Let's enforce this. Evaluating at the node $\xi = -1$:

$$
u_h^{(p=2)}(-1) = d_1 N_1(-1) + d_2 N_2(-1) + d_3 N_3(-1) = d_1(1) + d_2(0) + d_3 N_3(-1) = d_1 + d_3 N_3(-1)
$$

For $u_h^{(p=2)}(-1)$ to equal $d_1$, the term $d_3 N_3(-1)$ must be zero. Similarly, evaluating at $\xi = 1$:

$$
u_h^{(p=2)}(1) = d_1 N_1(1) + d_2 N_2(1) + d_3 N_3(1) = d_1(0) + d_2(1) + d_3 N_3(1) = d_2 + d_3 N_3(1)
$$

For $u_h^{(p=2)}(1)$ to equal $d_2$, the term $d_3 N_3(1)$ must be zero. Since the internal DOF $d_3$ can be any non-zero value, these conditions can only be satisfied for all possible approximations if the [bubble function](@entry_id:179039) $N_3(\xi)$ itself vanishes at the endpoints:

$$
N_3(-1) = 0 \quad \text{and} \quad N_3(1) = 0
$$

This is the paramount property of hierarchical internal modes: they must be zero at all nodes of the lower-order element they enrich. This ensures that the enrichment is "transparent" to the original nodal DOFs. For the quadratic case, any polynomial of the form $C(\xi^2-1)$ for a non-zero constant $C$ is a valid candidate. For instance, $1-\xi^2$ or $\frac{1}{2}(\xi^2 - 1)$ are common choices . This principle extends to all higher orders: the cubic mode must vanish at the endpoints, the quartic mode must vanish, and so on.

### Constructing Hierarchical Bases in Higher Dimensions

The hierarchical principle extends naturally to two and three dimensions. The key is to organize basis functions according to the topological entities of the element: **vertices**, **edges**, **faces** (in 3D), and the element **interior**.

#### Tensor-Product Elements: Quadrilaterals and Hexahedra

For elements that are topological products of intervals, like quadrilaterals and hexahedra, the basis functions can be constructed via tensor products of 1D hierarchical functions . Let us define a 1D hierarchical basis on $[-1,1]$ as consisting of:
- **Vertex modes:** $b_-(\xi) = \frac{1-\xi}{2}$ and $b_+(\xi) = \frac{1+\xi}{2}$.
- **Internal (edge) modes:** A set of polynomials $\phi_k(\xi)$ of degree $k$ for $k=2, \dots, p$, each satisfying $\phi_k(\pm 1)=0$. A common choice is derived from Legendre polynomials, such as $\phi_k(\xi) = \int_{-1}^\xi P_{k-1}(t) \,dt$ or functions proportional to $(1-\xi^2)P_{k-2}(\xi)$.

A 3D [basis function](@entry_id:170178) on the reference hexahedron $\hat{\Omega}=[-1,1]^3$ is then a product $\Psi(\xi, \eta, \zeta) = f(\xi)g(\eta)h(\zeta)$, where $f, g, h$ are chosen from the 1D set. The [topological classification](@entry_id:154529) arises from how many [bubble functions](@entry_id:176111) are in the product:

- **Vertex Modes:** A product of three vertex modes, e.g., $N_v(\xi, \eta, \zeta) = b_-(\xi)b_+(\eta)b_-(\zeta)$. This function is equal to 1 at the vertex $(-1, 1, -1)$ and zero at all other seven vertices. There are 8 such modes.

- **Edge Modes:** A product of one 1D internal mode and two 1D vertex modes, e.g., $N_e(\xi, \eta, \zeta) = \phi_k(\xi) b_-(\eta)b_-(\zeta)$. This function is associated with the edge defined by $\eta=-1, \zeta=-1$. The factors $b_-(\eta)$ and $b_-(\zeta)$ ensure it vanishes on all faces not containing this edge. The factor $\phi_k(\xi)$ ensures it vanishes at the endpoints of the edge itself (at $\xi = \pm 1$). For a polynomial degree $p$, there are $p-1$ such modes (for $k=2, \dots, p$) for each of the 12 edges.

- **Face Modes:** A product of two 1D internal modes and one 1D vertex mode, e.g., $N_f(\xi, \eta, \zeta) = b_+(\xi) \phi_j(\eta)\phi_k(\zeta)$. This function is associated with the face at $\xi=1$. The factor $b_+(\xi)$ confines its support, while the bubble factors $\phi_j(\eta)$ and $\phi_k(\zeta)$ ensure it vanishes on the boundary (edges) of that face. There are $(p-1)^2$ such modes for each of the 6 faces.

- **Interior Modes:** A product of three 1D internal modes, e.g., $N_i(\xi, \eta, \zeta) = \phi_i(\xi)\phi_j(\eta)\phi_k(\zeta)$. This function vanishes on the entire boundary $\partial\hat{\Omega}$ of the hexahedron. There are $(p-1)^3$ such modes.

Summing these up, the total number of degrees of freedom for a $Q_p$ hexahedral element is $D(p) = 8 + 12(p-1) + 6(p-1)^2 + (p-1)^3 = (p+1)^3$, confirming that this hierarchical construction spans the complete tensor-product [polynomial space](@entry_id:269905) .

#### Simplicial Elements: Triangles and Tetrahedra

For triangles and tetrahedra, the [natural coordinate system](@entry_id:168947) is the set of [barycentric coordinates](@entry_id:155488). The vanishing principle is upheld by using products of these coordinates, as the [zero-set](@entry_id:150020) of $\lambda_i$ is the face opposite to vertex $i$ . For a reference tetrahedron with vertices $V_1, \dots, V_4$ and coordinates $\lambda_1, \dots, \lambda_4$:

- **Vertex Modes:** These are simply the [barycentric coordinates](@entry_id:155488) themselves: $\varphi_i^{(v)} = \lambda_i$. This function is 1 at vertex $V_i$ and 0 at all other vertices.

- **Edge Modes:** For an edge connecting vertices $V_i$ and $V_j$, the modes must vanish on all faces not containing this edge. This is achieved by the product $\lambda_i \lambda_j$. This product also conveniently vanishes at the endpoints of the edge ($V_i$ and $V_j$), creating a bubble along the edge. Higher-order modes are generated by multiplying by polynomials in a 1D coordinate along the edge, e.g., $\varphi_{ij,m}^{(e)} = \lambda_i \lambda_j P_m(\frac{\lambda_i-\lambda_j}{\lambda_i+\lambda_j})$.

- **Face Modes:** For a face defined by vertices $V_i, V_j, V_k$, the modes must vanish on its boundary edges. This is achieved by the product $\lambda_i \lambda_j \lambda_k$. Higher-order modes are generated by multiplying by 2D polynomials defined on the face, e.g., $\varphi_{ijk,\alpha,\beta}^{(f)} = \lambda_i \lambda_j \lambda_k P_{\alpha,\beta}(\text{face coords})$.

- **Interior Modes:** For modes that vanish on the entire boundary of the tetrahedron, we require the product of all four [barycentric coordinates](@entry_id:155488): $\varphi^{(b)}_\ell = \lambda_1 \lambda_2 \lambda_3 \lambda_4 q_\ell(\lambda)$, where $q_\ell$ is some polynomial.

This systematic construction ensures that increasing the polynomial degree $p$ simply involves adding new edge, face, and interior modes, preserving the nested structure of the approximation spaces.

### Inter-element Conformity and Assembly

For a [finite element approximation](@entry_id:166278) to be valid in the context of second-order problems (like elasticity), the approximation space must be a subspace of $H^1(\Omega)$. For polynomial-based elements, this is equivalent to requiring the approximation to be globally $C^0$-continuous. This means the traces of the solution from adjacent elements must match perfectly along their shared interface .

The topological organization of hierarchical bases makes enforcing this condition remarkably clear. The trace of a function on an element's boundary is determined only by those basis functions whose support extends to the boundary.

- **Interior (Bubble) Modes:** By their very construction, interior modes for edges, faces, and volumes have zero trace on the boundary of the entity they are defined within (e.g., face modes are zero on the edges of that face; volume modes are zero on all faces). Consequently, **interior DOFs are purely local to an element**. They do not participate in inter-element coupling and are not shared between elements.

- **Vertex, Edge, and Face Modes:** These modes have non-zero traces. To ensure continuity, the degrees of freedom associated with any shared topological entity must be **single-valued across the entire mesh**. That is, all elements sharing a vertex must share the same vertex DOF. All elements sharing an edge must share the same set of edge DOFs. All elements sharing a face (in 3D) must share the same set of face DOFs.

A crucial subtlety arises for edge and face modes. These modes are typically defined using polynomials in a local coordinate system on the edge or face. However, two adjacent elements may parameterize their shared boundary with opposite orientations. For example, element 1 may define a shared edge from vertex A to B, while element 2 defines it from B to A .

Let the local coordinate on the shared edge for element 1 be $s^{(1)}$ and for element 2 be $s^{(2)}$. Their relationship is $s^{(2)} = \sigma s^{(1)}$, where $\sigma \in \{-1, +1\}$ is an orientation flag. Let the edge modes be built from a basis $\{B_k(s)\}$ with parity $B_k(-s) = (-1)^{k-1} B_k(s)$. The continuity requirement for the edge mode contributions is:
$$
\sum_{k=2}^{p} a_k^{(1)} B_k(s^{(1)}) = \sum_{k=2}^{p} a_k^{(2)} B_k(s^{(2)}) = \sum_{k=2}^{p} a_k^{(2)} B_k(\sigma s^{(1)}) = \sum_{k=2}^{p} a_k^{(2)} \sigma^{k-1} B_k(s^{(1)})
$$
Due to the orthogonality of the basis functions $\{B_k\}$, this equality can only hold if the coefficients are related term-by-term:
$$
a_k^{(1)} = \sigma^{k-1} a_k^{(2)} \quad \text{for } k=2, \dots, p
$$
This means the DOFs are shared, but possibly with a sign flip for modes of certain parity, depending on the relative orientation. A consistent orientation convention across the mesh is therefore essential for correct assembly.

### Consequences of Isoparametric Mapping

In practice, physical elements are rarely perfect squares or tetrahedra. We map them from a reference element using an **[isoparametric transformation](@entry_id:750863)**, where the geometry is interpolated using the same shape functions as the solution field. This mapping, while powerful, has profound consequences for hierarchical bases.

First, the calculation of derivatives, necessary for forming the stiffness matrix, requires the [chain rule](@entry_id:147422). The gradient of a shape function in physical coordinates $\mathbf{x}$ is related to its gradient in reference coordinates $\hat{\boldsymbol{\xi}}$ via the Jacobian matrix of the mapping, $\mathbf{J} = \frac{\partial \mathbf{x}}{\partial \hat{\boldsymbol{\xi}}}$ :
$$
\nabla_{\mathbf{x}} N = (\mathbf{J}^{-1})^T \nabla_{\hat{\boldsymbol{\xi}}} \hat{N}
$$
This transformation is a standard mechanical step in any isoparametric FEM code.

A more subtle consequence is the **[loss of orthogonality](@entry_id:751493)** . Many hierarchical bases are constructed to be orthogonal with respect to the $L^2$ inner product on the reference element. This is desirable as it can lead to diagonal or block-diagonal element mass matrices, simplifying computations. However, when we compute an inner product (e.g., for a mass matrix) on the physical element $\Omega$, we must transform the integral back to the reference element $\hat{K}$:
$$
\langle F, G \rangle_{\Omega} = \int_{\Omega} F G \, d\Omega = \int_{\hat{K}} \hat{F} \hat{G} (\det \mathbf{J}) \, d\hat{K}
$$
The integral on the [reference element](@entry_id:168425) now contains a weighting function, the Jacobian determinant $\det \mathbf{J}$. For a general bilinear isoparametric quadrilateral, $\det \mathbf{J}$ is a non-constant bilinear polynomial in $\xi$ and $\eta$. The presence of this non-constant weight function destroys the orthogonality that the basis functions $\hat{F}$ and $\hat{G}$ enjoyed on the [reference element](@entry_id:168425). Orthogonality on the physical element is preserved *if and only if* $\det \mathbf{J}$ is constant. This occurs only when the mapping is affine, i.e., the physical element is a parallelogram (for quads) or has constant Jacobian (for tets).

The practical implication is that for general distorted meshes, the element [mass and stiffness matrices](@entry_id:751703) computed with hierarchical bases will be fully-populated, not diagonal. The geometric distortion introduces coupling between all modes.

### Implications for Solvers and System Structure

Despite the [loss of orthogonality](@entry_id:751493) on distorted elements, the hierarchical structure provides significant advantages at the solver stage.

#### Static Condensation

The most important advantage is the natural framework for **[static condensation](@entry_id:176722)** . Since interior (bubble) modes are, by definition, entirely local to an element and not shared, their corresponding DOFs can be eliminated at the element level before [global assembly](@entry_id:749916). We can partition the [element stiffness matrix](@entry_id:139369) and force vector based on interface DOFs ($I$) and bubble DOFs ($B$):
$$
\begin{pmatrix} \mathbf{K}_{II} & \mathbf{K}_{IB} \\ \mathbf{K}_{BI} & \mathbf{K}_{BB} \end{pmatrix} \begin{pmatrix} \mathbf{u}_I \\ \mathbf{u}_B \end{pmatrix} = \begin{pmatrix} \mathbf{f}_I \\ \mathbf{f}_B \end{pmatrix}
$$
From the second row, we can solve for the bubble DOFs in terms of the interface DOFs: $\mathbf{u}_B = \mathbf{K}_{BB}^{-1} (\mathbf{f}_B - \mathbf{K}_{BI} \mathbf{u}_I)$. Substituting this into the first row yields a reduced system involving only the interface DOFs:
$$
(\mathbf{K}_{II} - \mathbf{K}_{IB} \mathbf{K}_{BB}^{-1} \mathbf{K}_{BI}) \mathbf{u}_I = \mathbf{f}_I - \mathbf{K}_{IB} \mathbf{K}_{BB}^{-1} \mathbf{f}_B
$$
This smaller, condensed system is assembled and solved globally. The bubble DOFs are then recovered element-by-element via back-substitution. This procedure dramatically reduces the size of the global system, leading to substantial savings in memory and computation time. While algebraically possible for any basis, [static condensation](@entry_id:176722) is cumbersome with nodal bases but is a natural and straightforward procedure with hierarchical bases due to their topological organization.

#### Equivalence of Nodal and Modal Viewpoints

It is important to recognize that for a given polynomial degree $p$ and element type, a hierarchical [modal basis](@entry_id:752055) and a high-order Lagrange nodal basis (e.g., using Gauss-Lobatto points) span the exact same space of polynomials. They are simply two different bases for the same vector space. As such, there exists an [invertible linear transformation](@entry_id:149915) between the vector of [modal coefficients](@entry_id:752057) $\mathbf{a}$ and the vector of nodal values $\mathbf{u}$ :
$$
\mathbf{u} = \mathbf{V} \mathbf{a}
$$
The [transformation matrix](@entry_id:151616) $\mathbf{V}$, a generalized Vandermonde matrix, is formed by evaluating the [modal basis](@entry_id:752055) functions at the [nodal points](@entry_id:171339). This equivalence implies that, up to a permutation of DOFs, the global stiffness matrices for nodal and hierarchical bases have identical sparsity patterns, as connectivity is a [topological property](@entry_id:141605) of the mesh, not the basis choice .

### Advanced Applications and Considerations

The power of hierarchical bases is most evident in their ability to facilitate advanced adaptive strategies and to remedy numerical pathologies.

#### The $p$- and $hp$-Versions for Singular Problems

Solutions to engineering problems often exhibit singularities, for instance, at re-entrant corners in a domain. Near such a corner, the solution behaves like $r^\lambda$ where $r$ is the distance to the corner and $\lambda  1$. This non-smooth behavior severely limits the convergence rate of standard FEM. Uniformly refining the mesh ($h$-refinement) or uniformly increasing the polynomial degree ($p$-refinement) results in slow, suboptimal algebraic convergence .

The optimal strategy, known as **$hp$-refinement**, adapts the [discretization](@entry_id:145012) to the local character of the solution.
- In regions **away** from the singularity, where the solution is smooth, large elements with **high polynomial degree $p$** are used to achieve rapid, [exponential convergence](@entry_id:142080).
- In the region **near** the singularity, a **geometrically [graded mesh](@entry_id:136402)** is used, with element sizes decreasing exponentially toward the corner, while the polynomial degree is kept **low and fixed**.

This combined strategy can recover a global exponential [rate of convergence](@entry_id:146534) for the energy error, e.g., $\mathcal{O}(\exp(-\gamma N^{1/3}))$. Hierarchical bases are the ideal tool for implementing such schemes, as they allow for local and variable $p$-enrichment without redesigning the mesh [data structure](@entry_id:634264).

#### Mitigating Volumetric Locking

In the analysis of [nearly incompressible materials](@entry_id:752388) ($\nu \to 0.5$), the standard displacement-based FEM formulation suffers from **[volumetric locking](@entry_id:172606)**, where the discrete model becomes overly stiff and produces inaccurate results. This occurs because the discrete [incompressibility constraint](@entry_id:750592), $\text{div}(\mathbf{u}_h) = 0$, is too restrictive for standard [polynomial spaces](@entry_id:753582).

Hierarchical bases, while not immune to locking, provide a natural framework for robust, locking-free formulations .
- **Mixed Formulations:** One can introduce the pressure as an independent field, leading to a mixed displacement-pressure formulation. A proven stable and locking-free choice is to use a continuous hierarchical displacement space of degree $p$ and a *discontinuous* pressure space of degree $p-1$. This $\mathcal{V}_h^{(p)} - \mathcal{Q}_h^{(p-1)}$ pairing satisfies the critical Ladyzhenskaya–Babuška–Brezzi (LBB) stability condition for $p \ge 1$ (on affine meshes) or $p \ge 2$ (on isoparametric meshes).
- **Assumed Strain Methods:** Alternatively, methods like the $\bar{B}$ formulation modify the volumetric part of the [strain energy](@entry_id:162699). This is often equivalent to a statically condensed mixed method and provides another robust route to circumvent locking.

These advanced formulations are readily implemented within the hierarchical framework, demonstrating its flexibility and power in addressing challenging problems in [computational solid mechanics](@entry_id:169583).