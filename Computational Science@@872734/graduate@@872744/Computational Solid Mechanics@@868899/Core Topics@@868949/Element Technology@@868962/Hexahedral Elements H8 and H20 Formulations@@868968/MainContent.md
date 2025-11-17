## Introduction
Hexahedral elements are a cornerstone of modern [finite element analysis](@entry_id:138109) (FEA), prized for their accuracy and efficiency in simulating complex three-dimensional structures. However, effectively harnessing their power requires more than a superficial understanding. Practitioners often face significant challenges, from accurately modeling curved geometries to navigating numerical pathologies like locking and [hourglassing](@entry_id:164538), which can render simulation results meaningless. This article serves as a comprehensive guide to the formulation and practical use of the two most common [hexahedral elements](@entry_id:174602): the 8-node trilinear (H8) and the 20-node quadratic (H20).

This article is structured to build your expertise progressively. In the "Principles and Mechanisms" chapter, we will delve into the theoretical foundations, starting with the isoparametric concept, [shape functions](@entry_id:141015), and the critical role of numerical integration. Next, "Applications and Interdisciplinary Connections" will bridge theory and practice, exploring how element choice and advanced formulations impact accuracy in real-world problems involving bending, [near-incompressibility](@entry_id:752381), and contact. Finally, the "Hands-On Practices" section offers targeted exercises to reinforce these key concepts. We begin by examining the core principles that govern the behavior of these powerful computational tools.

## Principles and Mechanisms

This chapter delves into the fundamental principles and operational mechanisms of isoparametric hexahedral finite elements, focusing on the two most common formulations: the 8-node trilinear (H8) and the 20-node serendipity quadratic (H20) elements. We will proceed from the foundational concept of [isoparametric mapping](@entry_id:173239) to the specific properties of each element type, and conclude with an in-depth examination of the numerical challenges that arise in practice and the advanced techniques used to overcome them.

### The Isoparametric Formulation

The **isoparametric concept** is a cornerstone of modern [finite element analysis](@entry_id:138109). It provides a powerful and elegant framework for formulating elements that can conform to complex, curved geometries while maintaining mathematical rigor. The central idea is to use a single, canonical element shape—the **[reference element](@entry_id:168425)** or parent element—and to map it into the desired shape and size in the physical domain. For [hexahedral elements](@entry_id:174602), the [reference element](@entry_id:168425) is a cube defined in a local, dimensionless coordinate system $(\xi, \eta, \zeta)$, where each coordinate ranges from $-1$ to $1$.

The same set of [algebraic functions](@entry_id:187534), known as **[shape functions](@entry_id:141015)** or basis functions, are used for two distinct but related purposes:
1.  **Geometric Mapping**: To define the physical coordinates $(x,y,z)$ of any point within the element as an interpolation of the physical coordinates of its nodes, $\mathbf{x}_i$.
    $$
    \mathbf{x}(\xi, \eta, \zeta) = \sum_{i=1}^{n} N_i(\xi, \eta, \zeta) \mathbf{x}_i
    $$
2.  **Field Variable Interpolation**: To approximate a field variable, such as the displacement vector $\mathbf{u}$, within the element as an interpolation of its nodal values, $\mathbf{u}_i$.
    $$
    \mathbf{u}(\xi, \eta, \zeta) = \sum_{i=1}^{n} N_i(\xi, \eta, \zeta) \mathbf{u}_i
    $$

Here, $n$ is the number of nodes in the element, and $N_i(\xi, \eta, \zeta)$ is the shape function associated with node $i$. These shape functions are constructed to have the **Kronecker-delta property** at the nodes of the [reference element](@entry_id:168425): $N_i(\boldsymbol{\xi}_j) = \delta_{ij}$, where $\boldsymbol{\xi}_j$ are the coordinates of node $j$. This property ensures that the interpolated geometry passes through the physical nodes and the interpolated field matches the prescribed nodal values.

A crucial quantity in this formulation is the **Jacobian matrix**, $\mathbf{J}$, which relates the derivatives in the physical coordinate system to those in the reference system:
$$
\mathbf{J} = \frac{\partial \mathbf{x}}{\partial \boldsymbol{\xi}} = \begin{pmatrix} \frac{\partial x}{\partial \xi} & \frac{\partial x}{\partial \eta} & \frac{\partial x}{\partial \zeta} \\ \frac{\partial y}{\partial \xi} & \frac{\partial y}{\partial \eta} & \frac{\partial y}{\partial \zeta} \\ \frac{\partial z}{\partial \xi} & \frac{\partial z}{\partial \eta} & \frac{\partial z}{\partial \zeta} \end{pmatrix}
$$
The Jacobian matrix is fundamental for two operations: transforming the gradient of a field variable (necessary for computing strains) and transforming the differential volume element for [numerical integration](@entry_id:142553):
$$
\nabla_{\mathbf{x}} (\cdot) = \mathbf{J}^{-\mathsf{T}} \nabla_{\boldsymbol{\xi}} (\cdot) \quad \text{and} \quad dV = \det(\mathbf{J}) \, d\xi \, d\eta \, d\zeta
$$
For a valid, physically meaningful mapping, the element must not "turn inside out." This requires that the determinant of the Jacobian, $\det(\mathbf{J})$, be positive everywhere within the element domain. It is a common misconception that checking for $\det(\mathbf{J}) > 0$ only at the element's corners is sufficient. The Jacobian determinant is a polynomial function of the reference coordinates, and it can become zero or negative at an interior point even if it is positive at all corners. This possibility of element distortion necessitates more robust checks in practice [@problem_id:3570552].

### The 8-Node Trilinear Hexahedron (H8)

The H8 element is the simplest hexahedral element, defined by eight nodes located at the corners of the reference cube.

#### Shape Functions and Interpolation
The [shape functions](@entry_id:141015) for the H8 element are required to be **trilinear**, meaning they are linear in each coordinate direction. A general form for the [shape functions](@entry_id:141015) can be derived by enforcing the Kronecker-delta property. For a node $i$ with reference coordinates $(\xi_i, \eta_i, \zeta_i)$, where each coordinate is either $-1$ or $1$, the shape function is:
$$
N_i(\xi, \eta, \zeta) = \frac{1}{8} (1 + \xi_i \xi) (1 + \eta_i \eta) (1 + \zeta_i \zeta)
$$
For instance, the node located at the physical vertex corresponding to $(\xi, \eta, \zeta) = (-1, -1, -1)$ in the reference domain would have the shape function $N_1 = \frac{1}{8}(1-\xi)(1-\eta)(1-\zeta)$ [@problem_id:3570574].

The polynomial basis spanned by these eight [shape functions](@entry_id:141015) includes all constant and linear terms ($1, \xi, \eta, \zeta$) as well as bilinear and trilinear terms ($\xi\eta, \eta\zeta, \xi\zeta, \xi\eta\zeta$). The presence of the complete linear basis is a critical property. It guarantees that the H8 element can exactly represent any affine geometric mapping (which maps the reference cube to a physical parallelepiped) and any linear displacement field. This property is the reason the H8 element passes the fundamental **patch test**, which requires an element to reproduce a state of constant strain exactly, a [necessary condition for convergence](@entry_id:157681) [@problem_id:3570577] [@problem_id:3570546].

However, the H8 element is a **lower-order element**. Its basis does not contain complete quadratic terms like $\xi^2$, $\eta^2$, or $\zeta^2$. Consequently, it cannot exactly represent a [quadratic field](@entry_id:636261). If one attempts to interpolate a function like $u(x,y,z) = x^2$ using an H8 element, there will be a non-zero [interpolation error](@entry_id:139425) [@problem_id:3570546]. This limitation leads to a theoretical convergence rate for the displacement error in the $L^2$ norm of $O(h^2)$, where $h$ is the characteristic element size. This is often referred to as [quadratic convergence](@entry_id:142552), as the error decreases by a factor of four when the mesh size is halved [@problem_id:3570546].

### The 20-Node Serendipity Hexahedron (H20)

To improve accuracy and convergence, [higher-order elements](@entry_id:750328) are used. The H20 element is a popular choice, offering a significant improvement over the H8 without the full complexity of a 27-node tri-quadratic Lagrange element. It is defined by 20 nodes: the 8 corners of the hexahedron plus 12 nodes located at the midpoint of each edge.

#### Shape Functions and Interpolation
The H20 element belongs to the **serendipity** family of elements, which are constructed to achieve a certain [polynomial completeness](@entry_id:177462) with fewer nodes than their Lagrange counterparts. The [shape functions](@entry_id:141015) are quadratic. Along any edge of the element, the interpolation reduces to a one-dimensional, three-node quadratic function [@problem_id:3570564]. This allows H20 elements to model curved geometries with quadratic edges and faces, a significant advantage over the straight-edged H8 element [@problem_id:3570552].

A key property of all standard [isoparametric elements](@entry_id:173863), including H8 and H20, is the **partition of unity**, meaning the [shape functions](@entry_id:141015) sum to one everywhere in the element: $\sum_{i=1}^{n} N_i(\xi, \eta, \zeta) = 1$. This property, combined with the element's ability to reproduce linear fields, ensures that it passes the constant-strain patch test, even for distorted (non-affine) geometries [@problem_id:3570564].

The polynomial basis of the H20 element contains all linear and quadratic monomials ($1, \xi, \dots, \xi^2, \dots, \xi\eta, \dots$). This means it can represent any [quadratic field](@entry_id:636261) variable, such as $u(x,y,z)=x^2$, with zero [interpolation error](@entry_id:139425) [@problem_id:3570546]. Its increased representational power also means it can capture more complex applied loads more accurately. For a traction distribution that is quadratic, an H20 element will yield a different, and generally more accurate, consistent nodal force at a corner node compared to an H8 element under the same load [@problem_id:3570541].

Because the H20 element is complete for quadratic polynomials (a $p=2$ element), its theoretical convergence rate in the $L^2$ norm is $O(h^{p+1}) = O(h^3)$, or [cubic convergence](@entry_id:168106). This faster convergence rate means that for smooth problems, H20 elements can achieve a given level of accuracy with far fewer elements than H8 elements [@problem_id:3570546].

It is important to note that both H8 and H20 elements provide only $C^0$ continuity of the displacement field across element boundaries. That is, the displacements are continuous, but their derivatives (and thus strains and stresses) are generally discontinuous [@problem_id:3570564].

### Numerical Integration and the Stiffness Matrix

The [element stiffness matrix](@entry_id:139369), $\mathbf{K}^e$, is central to the finite element method. It relates nodal displacements to nodal forces and is computed by integrating the [strain energy](@entry_id:162699) over the element's volume. Using the [isoparametric formulation](@entry_id:171513), this integral is transformed to the reference domain:
$$
\mathbf{K}^e = \int_{V^e} \mathbf{B}^{\mathsf{T}} \mathbf{C} \mathbf{B} \, dV = \int_{-1}^{1}\int_{-1}^{1}\int_{-1}^{1} \mathbf{B}(\boldsymbol{\xi})^{\mathsf{T}} \mathbf{C} \mathbf{B}(\boldsymbol{\xi}) \det(\mathbf{J}) \, d\boldsymbol{\xi}
$$
where $\mathbf{C}$ is the material [constitutive matrix](@entry_id:164908) and $\mathbf{B}$ is the [strain-displacement matrix](@entry_id:163451). This integral is almost always evaluated numerically using **Gauss-Legendre quadrature**. A tensor-product Gauss rule with $n \times n \times n$ points is exact for any integrand that is a polynomial of degree up to $2n-1$ in each of the coordinate directions $\xi, \eta, \zeta$ *separately*.

The choice of the number of integration points is a critical trade-off between accuracy and computational cost.
*   **For an H8 element** with an affine map (a parallelepiped), the Jacobian is constant. The entries of the $\mathbf{B}$ matrix are linear in the reference coordinates. Therefore, the integrand for the stiffness matrix contains terms that are quadratic in each coordinate (e.g., $\xi^2$). To integrate a degree-2 polynomial exactly requires a rule with $2n-1 \ge 2$, meaning $n=2$ points. Thus, a **$2 \times 2 \times 2$ Gauss rule** is the standard **full integration** scheme for H8 elements, as it integrates the [stiffness matrix](@entry_id:178659) exactly for affine elements [@problem_id:3570551] [@problem_id:3570584].

*   **For an H20 element** with an affine map, the entries of the $\mathbf{B}$ matrix are quadratic in the reference coordinates. The stiffness integrand is therefore a polynomial of up to degree 4 (quartic) in each direction. To integrate this exactly requires $2n-1 \ge 4$, which means $n=3$ points are necessary. Thus, a **$3 \times 3 \times 3$ Gauss rule** is the standard **full integration** scheme for H20 elements [@problem_id:3570551]. Using a $2 \times 2 \times 2$ rule for a quartic integrand can lead to significant underestimation of the element's stiffness, with errors potentially as large as 44% for certain deformation modes [@problem_id:3570584].

The cost increases significantly with the integration order. A $2 \times 2 \times 2$ rule requires 8 evaluations of the integrand, while a $3 \times 3 \times 3$ rule requires 27 evaluations—a more than threefold increase in computational effort for forming the [stiffness matrix](@entry_id:178659) [@problem_id:3570584].

### Numerical Pathologies and Their Remedies

Despite their power, [isoparametric elements](@entry_id:173863) are susceptible to several numerical problems, particularly in lower-order formulations or under specific physical conditions.

#### Hourglassing and Rank Deficiency

When an H8 element's stiffness is computed with **[reduced integration](@entry_id:167949)**—using fewer points than required for full integration—a serious [pathology](@entry_id:193640) can emerge. The most common form is using a single Gauss point at the element's center ($1 \times 1 \times 1$ rule). While computationally cheap, this scheme fails to "sense" certain deformation modes. These modes, which produce zero strain at the element center but are not rigid-body motions, are called **[hourglass modes](@entry_id:174855)** or [spurious zero-energy modes](@entry_id:755267).

An H8 element has 24 degrees of freedom (DOFs). After accounting for 6 rigid-body modes, its stiffness matrix must have a rank of 18 to be stable. However, when integrated with a single point, the rank of the [stiffness matrix](@entry_id:178659) collapses to 6. This [rank deficiency](@entry_id:754065) of $18-6=12$ corresponds to 12 independent [hourglass modes](@entry_id:174855) [@problem_id:3570597]. An unstabilized mesh of such elements can exhibit wild, non-physical oscillations with a checkerboard pattern, rendering the solution useless.

The remedy is **[hourglass stabilization](@entry_id:750386)**. This involves adding a small, artificial stiffness that penalizes only the [hourglass modes](@entry_id:174855) while leaving the physical deformation modes and rigid-body modes unaffected. This can be achieved by mathematically identifying the hourglass subspace—the part of the element's [nullspace](@entry_id:171336) that is orthogonal to the rigid-body subspace—and constructing a stabilization matrix that acts only within that subspace. A properly stabilized single-point-integration H8 element can be computationally efficient and accurate [@problem_id:3570597].

#### Volumetric Locking

Another common [pathology](@entry_id:193640), **volumetric locking**, occurs when modeling [nearly incompressible materials](@entry_id:752388) (e.g., rubber, or metals in plastic flow), where the Poisson's ratio $\nu$ approaches $0.5$. In this limit, the material's [bulk modulus](@entry_id:160069) $K$ becomes very large, heavily penalizing any volume change. The [incompressibility constraint](@entry_id:750592), $\nabla \cdot \mathbf{u} = \mathrm{tr}(\boldsymbol{\varepsilon}) \approx 0$, must be satisfied.

A standard, fully-integrated H8 element locks because its trilinear [displacement field](@entry_id:141476) can only produce a linear strain field. Enforcing the incompressibility constraint at all eight Gauss points simultaneously over-constrains the element. It cannot deform in modes like bending without producing spurious volumetric strains, leading to an artificially high stiffness that "locks" the mesh, preventing it from deforming correctly [@problem_id:3570575]. Contrary to some intuition, the higher-order H20 element also suffers from [volumetric locking](@entry_id:172606) when fully integrated, as its linear strain field is similarly over-constrained by the 27 Gauss points [@problem_id:3570575].

Several effective remedies exist:
*   **Reduced Integration**: Using a $1 \times 1 \times 1$ rule for the H8 element is a simple way to alleviate locking. By enforcing the constraint at only one point, the element gains the kinematic freedom to deform without penalty. However, as discussed, this introduces hourglass instability, creating a need for stabilization [@problem_id:3570551].

*   **Selective Reduced Integration (SRI)**: This more sophisticated technique provides the benefits of reduced integration without the instability. The [strain energy](@entry_id:162699) (and thus the stiffness matrix) is decomposed into a deviatoric (shape-changing) part and a volumetric (volume-changing) part. The volumetric part, which causes locking, is integrated with a reduced rule (e.g., $1 \times 1 \times 1$ for H8). The deviatoric part is fully integrated (e.g., $2 \times 2 \times 2$ for H8). This full integration of the deviatoric stiffness provides the necessary rank to prevent [hourglass modes](@entry_id:174855), resulting in an element that is both stable and locking-free [@problem_id:3570551] [@problem_id:3570575]. Applying reduced integration to the deviatoric part and full integration to the volumetric part is incorrect and would be counterproductive [@problem_id:3570575].

*   **The $\bar{B}$ (B-bar) Method**: This is a widely used alternative to SRI. Instead of modifying the integration, the formulation of the volumetric strain itself is modified. The standard, locally varying volumetric strain, $\mathrm{tr}(\boldsymbol{\varepsilon}) = \nabla \cdot \mathbf{u}$, is replaced by a projected field, $\overline{\mathrm{tr}(\boldsymbol{\varepsilon})}$, typically a constant value averaged over the element. This replaces the many pointwise [incompressibility](@entry_id:274914) constraints with a single, weaker, integral constraint on the element's total volume change. This modification applies only to the volumetric part of the [constitutive law](@entry_id:167255), preserving the element's shear response while effectively eliminating locking [@problem_id:3570575].

By understanding these fundamental principles, from basic interpolation to the nuances of numerical integration and stability, the practitioner can effectively leverage the power of H8 and H20 elements to solve complex problems in solid mechanics.