## Introduction
In the vast landscape of the finite element method (FEM), the ability to efficiently discretize complex three-dimensional geometries is paramount. While hexahedral and [tetrahedral elements](@entry_id:168311) form the backbone of most analyses, a significant challenge arises when attempting to connect structured and unstructured portions of a mesh. Wedge and pyramid elements emerge as the indispensable solution to this problem, serving as geometric bridges that ensure mesh conformity and solution continuity. Their unique topologies make them essential tools for advanced applications, from resolving thin boundary layers in fluid dynamics to modeling intricate structural junctions.

This article provides a graduate-level exploration into the formulation and application of these vital [transitional elements](@entry_id:167948). It addresses the knowledge gap between standard element theory and the practical necessity of hybrid [meshing](@entry_id:269463). Over the next three chapters, you will gain a comprehensive understanding of these specialized elements. The journey begins with **Principles and Mechanisms**, where we will dissect the mathematical foundations, including the derivation of shape functions, the [isoparametric mapping](@entry_id:173239), and the notorious Jacobian singularity of pyramid elements. Next, **Applications and Interdisciplinary Connections** will showcase their practical utility in solid mechanics, fluid dynamics, and computational physics, emphasizing their role in advanced meshing and adaptive refinement strategies. Finally, the **Hands-On Practices** section will offer a chance to solidify this knowledge through targeted problems, bridging theory with practical implementation.

## Principles and Mechanisms

In the finite element method, the [discretization](@entry_id:145012) of complex three-dimensional domains often necessitates the use of specialized elements to create a conformal mesh between regions meshed with different element types. While tetrahedral (tets) and hexahedral (hex) elements are the standard workhorses for 3D analysis, connecting a [structured mesh](@entry_id:170596) of hexahedra to an unstructured mesh of tetrahedra poses a geometric challenge. **Wedge** and **pyramid** elements serve as essential [transitional elements](@entry_id:167948) to bridge this gap, ensuring mesh conformity and solution continuity without resorting to complex constraints. This chapter elucidates the fundamental principles and formulation mechanisms of these vital elements.

### The Wedge (Prismatic) Element

The wedge, or triangular prism, element is the natural choice for transitioning between quadrilateral faces of hexahedra and triangular faces of tetrahedra. Its geometry consists of two parallel triangular faces and three quadrilateral faces connecting them.

#### Geometric and Parametric Definition

The **reference [wedge element](@entry_id:175456)** is typically defined in a parametric coordinate system $(\xi, \eta, \zeta)$. The domain is a right triangular prism where the triangular cross-section is parameterized in $(\xi, \eta)$ and the extrusion or thickness is parameterized along the $\zeta$-axis. A common definition for the reference domain is the set of points where the base lies in a standard reference triangle and the thickness coordinate spans a standard interval:
$$ \hat{\Omega}_w = \{(\xi, \eta, \zeta) \mid \xi \ge 0, \eta \ge 0, \xi + \eta \le 1, -1 \le \zeta \le 1 \} $$
This element has $6$ vertices, $9$ edges, and $5$ faces (two triangles and three quadrilaterals). For practical implementation in finite element codes, a consistent local numbering of these entities is critical for the assembly of global matrices and the application of boundary conditions. A standardized convention, for instance, might number the vertices of the "bottom" triangular face ($\zeta=-1$) as 1-2-3 and the corresponding vertices of the "top" face ($\zeta=1$) as 4-5-6. The orientation of faces, defined by an ordered list of its vertices, must be consistently chosen to produce [outward-pointing normal](@entry_id:753030) vectors, which is crucial for evaluating [surface integrals](@entry_id:144805) for flux or pressure loads. [@problem_id:2611731]

#### Linear (6-Node) Wedge Formulation

The formulation of [shape functions](@entry_id:141015) for the [wedge element](@entry_id:175456) can be elegantly achieved through a **tensor product** of shape functions from lower-dimensional elements. For the 6-node linear wedge, we combine the linear shape functions of a 3-node triangle with the linear shape functions of a 1D line element.

The [shape functions](@entry_id:141015) for the reference triangle, expressed in [barycentric coordinates](@entry_id:155488), are:
$$ \lambda_1(\xi, \eta) = 1 - \xi - \eta, \quad \lambda_2(\xi, \eta) = \xi, \quad \lambda_3(\xi, \eta) = \eta $$
The linear Lagrange polynomials for the interval $\zeta \in [-1, 1]$ are:
$$ L_{-1}(\zeta) = \frac{1-\zeta}{2}, \quad L_{+1}(\zeta) = \frac{1+\zeta}{2} $$
The six shape functions for the [wedge element](@entry_id:175456) are formed by taking the product of the appropriate triangular and linear functions. Assuming nodes 1, 2, and 3 correspond to the vertices of the bottom triangle (at $\zeta=-1$) and nodes 4, 5, and 6 are their counterparts on the top triangle (at $\zeta=1$), the shape functions $N_i(\xi, \eta, \zeta)$ are:

For the bottom nodes ($i=1, 2, 3$):
$$ N_i(\xi, \eta, \zeta) = \lambda_i(\xi, \eta) L_{-1}(\zeta) = \lambda_i(\xi, \eta) \frac{1-\zeta}{2} $$
For the top nodes ($i=4, 5, 6$), where node $i+3$ is above node $i$:
$$ N_{i+3}(\xi, \eta, \zeta) = \lambda_i(\xi, \eta) L_{+1}(\zeta) = \lambda_i(\xi, \eta) \frac{1+\zeta}{2} $$

These functions inherently satisfy the **Kronecker-delta property**, $N_i(\boldsymbol{\xi}_j) = \delta_{ij}$, where $\boldsymbol{\xi}_j$ is the [coordinate vector](@entry_id:153319) of node $j$. For instance, at node 1 (e.g., $(\xi, \eta, \zeta)=(0,0,-1)$ if $\lambda_1$ corresponds to the origin), $\lambda_1=1$ and $L_{-1}(-1)=1$, making $N_1=1$, while all other shape functions evaluate to zero. They also form a **partition of unity**, $\sum_{i=1}^6 N_i = 1$, which is essential for representing [rigid body motion](@entry_id:144691) correctly. [@problem_id:2611759]

#### Isoparametric Mapping and the Jacobian

The **isoparametric concept** maps the simple reference wedge geometry into a potentially curved wedge in physical space. The physical coordinates $\mathbf{x}$ of any point within the element are interpolated from the nodal coordinates $\mathbf{X}_i$ using the very same shape functions:
$$ \mathbf{x}(\xi, \eta, \zeta) = \sum_{i=1}^{6} N_i(\xi, \eta, \zeta) \mathbf{X}_i $$
The transformation between the physical gradient of a function and its parametric gradient is governed by the **Jacobian matrix**, $\mathbf{J}$, defined as:
$$ \mathbf{J} = \frac{\partial \mathbf{x}}{\partial (\xi, \eta, \zeta)} = \begin{pmatrix} \frac{\partial x}{\partial \xi} & \frac{\partial x}{\partial \eta} & \frac{\partial x}{\partial \zeta} \\ \frac{\partial y}{\partial \xi} & \frac{\partial y}{\partial \eta} & \frac{\partial y}{\partial \zeta} \\ \frac{\partial z}{\partial \xi} & \frac{\partial z}{\partial \eta} & \frac{\partial z}{\partial \zeta} \end{pmatrix} = \sum_{i=1}^{6} \mathbf{X}_i (\nabla_{\boldsymbol{\xi}} N_i)^\mathsf{T} $$
The determinant of the Jacobian, $\det(\mathbf{J})$, represents the local volume scaling factor between the parametric and physical domains ($dV_{phys} = \det(\mathbf{J}) dV_{param}$). For a valid mapping, $\det(\mathbf{J})$ must be strictly positive throughout the element.

For a straight-sided [wedge element](@entry_id:175456) whose vertical edges are parallel (a right prism), the Jacobian matrix becomes constant. For example, consider a wedge with base nodes $\mathbf{X}_1=(0,0,0)$, $\mathbf{X}_2=(2,0,0)$, $\mathbf{X}_3=(0,1,0)$ and top nodes directly above at a height of 3: $\mathbf{X}_4=(0,0,3)$, $\mathbf{X}_5=(2,0,3)$, $\mathbf{X}_6=(0,1,3)$. The Jacobian matrix for this geometry is constant:
$$ \mathbf{J} = \begin{pmatrix} 2 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 3/2 \end{pmatrix} $$
The determinant is $\det(\mathbf{J}) = 3$, indicating a constant volume ratio of 3 between the physical element (volume = Area $\times$ height = $\frac{1}{2}(2)(1) \times 3 = 3$) and the reference element (volume = $\frac{1}{2}(1)(1) \times 2 = 1$). [@problem_id:2611748]

In applications such as solid mechanics, the essential task is to compute strains from nodal displacements. This requires the spatial derivatives of the shape functions in the physical coordinate system. These are obtained via the chain rule, which in matrix form gives:
$$ \nabla_{\mathbf{x}} N_i = (\mathbf{J}^\mathsf{T})^{-1} \nabla_{\boldsymbol{\xi}} N_i = \mathbf{J}^{-\mathsf{T}} \nabla_{\boldsymbol{\xi}} N_i $$
Once the physical gradients $(\partial N_i/\partial x, \partial N_i/\partial y, \partial N_i/\partial z)$ are known, the [strain-displacement matrix](@entry_id:163451) $\mathbf{B}$ can be assembled, which relates the vector of nodal displacements to the vector of strain components. [@problem_id:2611734]

### The Pyramid Element

The [pyramid element](@entry_id:174636), with one quadrilateral face and four triangular faces meeting at an apex, is indispensable for creating a conformal transition between hexahedral and [tetrahedral elements](@entry_id:168311). Unlike the wedge, its formulation is notoriously more complex and presents unique challenges.

#### Geometric Definition

A common **reference [pyramid element](@entry_id:174636)** is defined on a domain with a square base. For example, we can define the pyramid as the set of points $(\xi, \eta, \zeta)$ satisfying a system of inequalities:
$$ \hat{K}_p = \{(\xi, \eta, \zeta) \mid 0 \le \zeta \le 1, -1+\zeta \le \xi \le 1-\zeta, -1+\zeta \le \eta \le 1-\zeta \} $$
In this definition, the base is a square of side length 2 in the $\zeta=0$ plane, and the element tapers linearly to a single point, the **apex**, at $(\xi, \eta, \zeta) = (0,0,1)$. This polyhedron has 5 vertices (four at the base, one apex), 8 edges (four on the base, four lateral), and 5 faces (one quadrilateral base, four triangular sides). The equations for these geometric entities can be systematically derived by activating the inequalities in the definition. For instance, the base face is defined by $\zeta=0$ with $-1 \le \xi, \eta \le 1$, and a side face is defined by an equation like $\xi = 1-\zeta$ with the remaining variables bounded accordingly. [@problem_id:2611762]

#### Linear (5-Node) Pyramid Formulation

The lack of a simple prismatic structure means that pyramid [shape functions](@entry_id:141015) cannot be formed by a simple [tensor product](@entry_id:140694). Several formulations exist, with a common and instructive one being the **collapsed coordinate method**. In this approach, one can conceptualize the pyramid as a degenerated hexahedron where all four vertices of the top face have been collapsed into a single point.

This leads to a mapping from a "parent" cube or prism with coordinates, say, $(a,b,\zeta)$ where $(a,b) \in [-1,1]^2$ define the square cross-section and $\zeta \in [0,1]$ is the height coordinate. The pyramid's [natural coordinates](@entry_id:176605) $(\xi, \eta, \zeta)$ are then defined by a "collapse" map:
$$ \xi = a(1-\zeta), \quad \eta = b(1-\zeta) $$
Points on the base of the prism ($\zeta=0$) map directly, with $\xi=a$ and $\eta=b$. The entire top face of the prism ($\zeta=1$) collapses to the origin $(\xi, \eta) = (0,0)$, which becomes the pyramid's apex in the [natural coordinate system](@entry_id:168947).

To construct the shape functions for a 5-node linear pyramid, we can enforce the [partition of unity](@entry_id:141893) property. A particularly simple and common choice is to define the shape function for the apex node (node 5) to be linear with height:
$$ N_5(\xi, \eta, \zeta) = \zeta $$
The partition of unity requires $\sum_{i=1}^5 N_i = 1$, which implies that the sum of the base node shape functions must be $\sum_{i=1}^4 N_i = 1 - N_5 = 1-\zeta$. If we assume the base node [shape functions](@entry_id:141015) are constructed from the standard bilinear functions $\widehat{N}_i(a,b)$ on the square base, modified by a factor of $(1-\zeta)$, we can write:
$$ N_i(\xi, \eta, \zeta) = (1-\zeta) \widehat{N}_i(a,b) = (1-\zeta) \widehat{N}_i\left(\frac{\xi}{1-\zeta}, \frac{\eta}{1-\zeta}\right) \quad \text{for } i=1,2,3,4 $$
Substituting the expression for a bilinear function, for example $\widehat{N}_1(a,b) = \frac{1}{4}(1-a)(1-b)$, yields a [rational function](@entry_id:270841) for the base node shape function:
$$ N_1(\xi, \eta, \zeta) = (1-\zeta) \frac{1}{4} \left(1-\frac{\xi}{1-\zeta}\right) \left(1-\frac{\eta}{1-\zeta}\right) = \frac{(1-\zeta-\xi)(1-\zeta-\eta)}{4(1-\zeta)} $$
These expressions are regular (infinitely differentiable) everywhere inside the element ($0 \le \zeta  1$) but have a formal singularity at the apex plane $\zeta=1$. [@problem_id:2611735]

#### The Jacobian Singularity

This rational nature of the shape functions, or more fundamentally, the [geometric collapse](@entry_id:188123) of a face to a point, leads to a **Jacobian singularity** at the apex. The Jacobian determinant for pyramid mappings derived from collapsed hexahedra can be shown to vanish quadratically as the apex is approached. The general form is:
$$ \det(\mathbf{J}) = \frac{(1-\zeta)^2}{C} \left( \frac{\partial \mathbf{X}_b}{\partial \xi} \times \frac{\partial \mathbf{X}_b}{\partial \eta} \right) \cdot (\mathbf{X}_5 - \mathbf{X}_b(\xi, \eta)) $$
where $\mathbf{X}_b$ is the [bilinear mapping](@entry_id:746795) of the base, $\mathbf{X}_5$ is the apex position, and $C$ is a constant. The term $(1-\zeta)^2$ clearly shows that $\det(\mathbf{J}) = \mathcal{O}((1-\zeta)^2)$, meaning the volume element collapses quadratically fast at the apex. This is an intrinsic property of such formulations. While this singularity is integrable and does not necessarily invalidate the element, it requires careful treatment. To avoid element inversion ($\det(\mathbf{J}) \le 0$), the geometry must satisfy the condition that the apex $\mathbf{X}_5$ lies strictly on the positive side of the tangent plane to the (possibly warped) base surface at every point on that surface. [@problem_id:2611691]

The computation of physical gradients for pyramid elements is also complicated by the chain of mappings. To find the physical gradient $\nabla_{\mathbf{x}}N_i$, one must apply the chain rule twice, transforming first from the collapsed coordinates $(a,b,\zeta)$ to the [natural coordinates](@entry_id:176605) $(\xi, \eta, \zeta)$, and then from natural to physical coordinates $\mathbf{x}$. This involves the inverse transpose of two separate Jacobian matrices. [@problem_id:2611715]

### Advanced Topics and Practical Considerations

#### Higher-Order Elements

Higher-order wedge and pyramid elements can be constructed to improve accuracy. For wedges, this is relatively straightforward. For instance, a quadratic wedge can be formed by a tensor product of a 6-node quadratic triangle ($P_2$) and a 3-node quadratic line element ($P_2$), resulting in an 18-node element with a [polynomial space](@entry_id:269905) $P_2(\xi,\eta) \otimes P_2(\zeta)$.

A common alternative is the 15-node **serendipity wedge**, which omits the three nodes from the interior of the mid-plane quadrilateral face. Its [polynomial space](@entry_id:269905) is a union of smaller tensor product spaces, $S_{15} = (P_2(\xi,\eta) \otimes P_1(\zeta)) \cup (P_1(\xi,\eta) \otimes P_2(\zeta))$. This element is **quadratically complete**, meaning it can exactly represent any polynomial of total degree 2, which is sufficient for passing the patch test and ensuring optimal convergence rates for second-order problems. However, it cannot represent the full $P_2 \otimes P_2$ space of the 18-node element; specifically, it lacks the monomials $\xi^2\zeta^2$, $\eta^2\zeta^2$, and $\xi\eta\zeta^2$. This is a classic trade-off between reducing the number of nodes (and computational cost) and the richness of the interpolation space. [@problem_id:2611689]

#### Numerical Integration

The formulation of pyramid elements introduces a significant practical challenge for numerical integration (quadrature). When computing element matrices, such as the [stiffness matrix](@entry_id:178659) $K_{ij} = \int \kappa (\nabla N_i \cdot \nabla N_j) dV$, the integrand must be evaluated in the reference domain. The integrand becomes:
$$ \mathcal{I}_{ij}(\xi, \eta, \zeta) = \kappa (\nabla_{\mathbf{x}} N_i \cdot \nabla_{\mathbf{x}} N_j) \det(\mathbf{J}) $$
Due to the Jacobian singularity and [rational shape functions](@entry_id:178215), this integrand is not a simple polynomial in $(\xi, \eta, \zeta)$. For the common collapsed [coordinate mappings](@entry_id:747874), the physical gradients $\nabla_{\mathbf{x}}N_i$ can be shown to be polynomials due to cancellation effects, but the [volume element](@entry_id:267802) contains the Jacobian determinant, e.g., $\det(\mathbf{J}) \propto (1-\zeta)^2$. The full integrand therefore takes the form of a polynomial multiplied by a weight function:
$$ \mathcal{I}_{ij} = P_{ij}(\xi, \eta, \zeta) (1-\zeta)^2 $$
Applying a standard numerical integration scheme, like a [tensor product](@entry_id:140694) of Gauss-Legendre rules, is not optimal because it treats the entire expression as a single high-degree polynomial. This can lead to inaccuracy or require an excessively high quadrature order. The correct and most efficient method is to use a **weighted Gaussian quadrature**. In this case, a [tensor product](@entry_id:140694) rule is employed using Gauss-Legendre quadrature for the $\xi$ and $\eta$ directions, and a **Gauss-Jacobi** quadrature for the $\zeta$ direction, which is specifically designed to exactly integrate functions of the form $\text{Polynomial} \times (1-t)^\alpha (1+t)^\beta$. This tailored approach correctly handles the singular behavior of the mapping and ensures accurate computation of the element matrices. [@problem_id:2611754]