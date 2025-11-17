## Introduction
In [computational solid mechanics](@entry_id:169583), the Finite Element Method (FEM) provides a powerful framework for analyzing complex structures. While real-world problems are three-dimensional, many can be simplified to two-dimensional models without significant loss of accuracy, drastically reducing computational cost. This simplification relies on two key assumptions: [plane stress and plane strain](@entry_id:172357). Understanding how to correctly formulate the [element stiffness matrix](@entry_id:139369)—the fundamental building block of an FEA model—under these conditions is a critical skill for any engineer or scientist. This article addresses the core challenge of translating continuous [elasticity theory](@entry_id:203053) into discrete, computable element matrices for 2D analysis.

This article will guide you through this essential process in three parts. The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork. We will derive the constitutive relationships for [plane stress and plane strain](@entry_id:172357), formulate the [strain-displacement matrix](@entry_id:163451), and detail the integration procedure for element stiffness matrices, including the numerical challenges of locking and [hourglassing](@entry_id:164538). The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these foundational concepts are applied to solve real-world problems, from analyzing [anisotropic materials](@entry_id:184874) and coupled-field physics to ensuring structural integrity through fracture and [buckling analysis](@entry_id:168558). Finally, the **Hands-On Practices** section provides targeted problems to solidify your understanding of key computational steps, such as evaluating the Jacobian, analyzing [constitutive matrix](@entry_id:164908) behavior, and verifying element properties through eigenanalysis. By the end, you will have a comprehensive understanding of both the theory and practice of formulating element stiffness matrices for 2D FEM.

## Principles and Mechanisms

The formulation of element stiffness matrices for two-dimensional problems is a cornerstone of [computational solid mechanics](@entry_id:169583). While the physical world is three-dimensional, many engineering problems can be effectively simplified to two dimensions under specific assumptions. This chapter elucidates the principles and mechanisms governing the transition from three-dimensional [elasticity theory](@entry_id:203053) to the practical computation of element stiffness matrices for two common idealizations: **[plane stress](@entry_id:172193)** and **[plane strain](@entry_id:167046)**. We will explore the kinematic and kinetic foundations of these assumptions, derive the corresponding constitutive matrices, and detail the procedures for formulating and integrating element stiffness matrices for both simple and advanced elements. Finally, we will examine the critical numerical phenomena of locking and [hourglassing](@entry_id:164538) that arise from these formulations.

### Fundamental Assumptions for 2D Elasticity

The reduction of a 3D problem to a 2D one hinges on assumptions about the stress or strain state in the out-of-plane direction. The validity of these assumptions is directly linked to the geometry of the body and the nature of the applied loads.

#### Plane Stress

The **[plane stress](@entry_id:172193)** assumption is suitable for thin, plate-like structures where the dimension in one direction (say, the $z$-direction) is significantly smaller than the dimensions in the other two directions (the $x$-$y$ plane). A classic example is a thin sheet of metal subjected to in-plane forces. [@problem_id:2554515]

The formal definition of plane stress arises from considering the [traction boundary conditions](@entry_id:167112) on the large, free faces of the thin plate. If these faces are traction-free, the stress components normal and tangential to these faces must be zero at the boundary. For a thin body, it is a reasonable and powerful idealization to assume these stress components are zero throughout the entire thickness. This leads to the defining kinetic constraint of plane stress [@problem_id:2554519]:
$$
\sigma_{zz} = \sigma_{xz} = \sigma_{yz} = 0
$$
A crucial consequence of this assumption concerns the out-of-[plane strain](@entry_id:167046), $\epsilon_{zz}$. While the out-of-plane stresses are zero, the strain is not. Due to the Poisson effect, in-plane stresses will induce an out-of-[plane strain](@entry_id:167046), causing a change in the body's thickness. For a linear, isotropic, elastic material, the 3D Hooke's Law for the $z$-direction [normal strain](@entry_id:204633) is:
$$
\epsilon_{zz} = \frac{1}{E} [ \sigma_{zz} - \nu (\sigma_{xx} + \sigma_{yy}) ]
$$
Applying the [plane stress condition](@entry_id:168184) $\sigma_{zz} = 0$, we find that $\epsilon_{zz}$ is generally non-zero:
$$
\epsilon_{zz} = -\frac{\nu}{E}(\sigma_{xx} + \sigma_{yy})
$$
This can also be expressed in terms of the in-plane strains, which after some algebraic manipulation yields the important relation [@problem_id:2554568]:
$$
\epsilon_{zz} = -\frac{\nu}{1 - \nu} (\epsilon_{xx} + \epsilon_{yy})
$$
Therefore, under [plane stress](@entry_id:172193), the non-zero components are the in-plane stresses ($\sigma_{xx}, \sigma_{yy}, \sigma_{xy}$) and all three normal strains plus the in-plane shear strain ($\epsilon_{xx}, \epsilon_{yy}, \epsilon_{zz}, \gamma_{xy}$).

#### Plane Strain

The **[plane strain](@entry_id:167046)** assumption applies to bodies that are very long in one direction (the $z$-direction) compared to their cross-sectional dimensions, and whose geometry and loading are uniform along this length. Examples include a long dam, a tunnel, or a retaining wall. The material far from the ends is constrained by the adjacent material, preventing movement or deformation in the out-of-plane direction. [@problem_id:2554515]

This physical situation is idealized by a kinematic constraint: all out-of-plane strain components are assumed to be zero. This defines the [plane strain](@entry_id:167046) condition [@problem_id:2554519]:
$$
\epsilon_{zz} = \gamma_{xz} = \gamma_{yz} = 0
$$
In this case, a non-zero out-of-plane [normal stress](@entry_id:184326), $\sigma_{zz}$, must develop to enforce the zero-strain constraint. We can find this stress from the 3D Hooke's Law:
$$
\epsilon_{zz} = \frac{1}{E} [ \sigma_{zz} - \nu (\sigma_{xx} + \sigma_{yy}) ] = 0
$$
Solving for $\sigma_{zz}$ gives:
$$
\sigma_{zz} = \nu (\sigma_{xx} + \sigma_{yy})
$$
This restraining stress is generally non-zero and is proportional to the sum of the in-plane normal stresses. [@problem_id:2554568] Thus, under plane strain, the potentially non-zero components are the in-plane strains ($\epsilon_{xx}, \epsilon_{yy}, \gamma_{xy}$) and all three [normal stresses](@entry_id:260622) plus the in-plane shear stress ($\sigma_{xx}, \sigma_{yy}, \sigma_{zz}, \sigma_{xy}$).

### The Constitutive Relationship: Stress-Strain Matrices

The relationship between stress and strain, $\boldsymbol{\sigma} = \mathbf{D} \boldsymbol{\epsilon}$, is defined by the [constitutive matrix](@entry_id:164908) $\mathbf{D}$. The assumptions of [plane stress and plane strain](@entry_id:172357) lead to different reduced forms of this matrix. For an [isotropic material](@entry_id:204616), arranging the in-plane components into vectors $\boldsymbol{\sigma} = [\sigma_{xx}, \sigma_{yy}, \sigma_{xy}]^T$ and $\boldsymbol{\epsilon} = [\epsilon_{xx}, \epsilon_{yy}, \gamma_{xy}]^T$, we can derive the respective matrices.

For **[plane stress](@entry_id:172193)**, by inverting the strain-stress relations under the condition $\sigma_{zz}=0$, we obtain:
$$
\mathbf{D}_{ps} = \frac{E}{1-\nu^2} \begin{pmatrix} 1  \nu  0 \\ \nu  1  0 \\ 0  0  \frac{1-\nu}{2} \end{pmatrix}
$$

For **[plane strain](@entry_id:167046)**, by directly using the stress-strain relations with $\epsilon_{zz}=0$, we get:
$$
\mathbf{D}_{pe} = \frac{E}{(1+\nu)(1-2\nu)} \begin{pmatrix} 1-\nu  \nu  0 \\ \nu  1-\nu  0 \\ 0  0  \frac{1-2\nu}{2} \end{pmatrix}
$$
These distinct matrices are the fundamental reason why [plane stress and plane strain](@entry_id:172357) problems yield different results, even for the same geometry and material properties ($E$ and $\nu$).

### From Continuum to Element: The Strain-Displacement Matrix

The [finite element method](@entry_id:136884) discretizes a continuous body into a collection of elements. Within each element, the [displacement field](@entry_id:141476) $\mathbf{u}(x,y) = [u(x,y), v(x,y)]^T$ is interpolated from the nodal displacements $\mathbf{d}_e$ using shape functions $\mathbf{N}$: $\mathbf{u} = \mathbf{N} \mathbf{d}_e$.

The link between these nodal displacements and the continuum strain field is the **[strain-displacement matrix](@entry_id:163451)**, $\mathbf{B}$. It is derived from the fundamental definitions of small strain, which relate strain components to spatial gradients of the [displacement field](@entry_id:141476) [@problem_id:2554583]:
$$
\epsilon_{xx} = \frac{\partial u}{\partial x}, \quad \epsilon_{yy} = \frac{\partial v}{\partial y}, \quad \gamma_{xy} = \frac{\partial u}{\partial y} + \frac{\partial v}{\partial x}
$$
By substituting the interpolated [displacement field](@entry_id:141476) into these definitions and performing the differentiation, we arrive at the matrix relationship $\boldsymbol{\epsilon} = \mathbf{B} \mathbf{d}_e$.

For example, consider a simple three-node **Constant Strain Triangle (CST)** element. The linear shape functions lead to a $\mathbf{B}$ matrix that is constant throughout the element, meaning the strain state is uniform. For a CST with nodes at $(0,0)$, $(1,0)$, and $(0,1)$, the $\mathbf{B}$ matrix can be shown to be [@problem_id:2554529]:
$$
\mathbf{B} = \begin{pmatrix} -1  0  1  0  0  0 \\ 0  -1  0  0  0  1 \\ -1  -1  0  1  1  0 \end{pmatrix}
$$
This simple, constant matrix provides a clear foundation for understanding how element stiffness is constructed.

### The Element Stiffness Matrix: Formulation and Computation

The [principle of virtual work](@entry_id:138749) leads to the definition of the [element stiffness matrix](@entry_id:139369), $\mathbf{K}_e$, which relates the nodal displacements $\mathbf{d}_e$ to the nodal forces $\mathbf{f}_e$. For a 2D element of constant thickness $t$, its form is:
$$
\mathbf{K}_e = \int_{\Omega_e} \mathbf{B}^T \mathbf{D} \mathbf{B} \, t \, d\Omega
$$
where $\Omega_e$ is the area of the element. For the CST element, since $\mathbf{B}$, $\mathbf{D}$, and $t$ are all constant, the integral simplifies to $\mathbf{K}_e = (\mathbf{B}^T \mathbf{D} \mathbf{B}) \, t A$, where $A$ is the element area.

A direct comparison of the stiffness matrices for plane stress ($\mathbf{K}_{ps}$) and plane strain ($\mathbf{K}_{pe}$) reveals a critical insight. Using the same $\mathbf{B}$ matrix but the different constitutive matrices $\mathbf{D}_{ps}$ and $\mathbf{D}_{pe}$, one finds that the [plane strain](@entry_id:167046) element is stiffer. This can be quantified by computing the [strain energy](@entry_id:162699) $U_e = \frac{1}{2} \mathbf{d}_e^T \mathbf{K}_e \mathbf{d}_e$ for a given deformation. For the same nodal displacements, the [strain energy](@entry_id:162699) stored in the [plane strain](@entry_id:167046) element will be higher. [@problem_id:2554529] This is because the [plane strain assumption](@entry_id:186003) kinematically constrains the element from deforming out-of-plane ($\epsilon_{zz}=0$), requiring additional stress ($\sigma_{zz}$) and thus additional energy to impose an in-plane deformation. In contrast, the plane stress element is free to deform in the thickness direction, offering less resistance.

For more complex elements like the four-node **isoparametric quadrilateral (Q4)**, the $\mathbf{B}$ matrix is no longer constant. These elements use an **[isoparametric mapping](@entry_id:173239)** to transform a simple "parent" element (typically a square in $(\xi, \eta)$ coordinates from $-1$ to $+1$) into a general quadrilateral shape in physical $(x,y)$ coordinates. The geometry itself is interpolated using the same shape functions as the displacement field [@problem_id:2554559]:
$$
x(\xi,\eta) = \sum_{i=1}^{4} N_i(\xi,\eta) x_i, \quad y(\xi,\eta) = \sum_{i=1}^{4} N_i(\xi,\eta) y_i
$$
The derivatives required for the $\mathbf{B}$ matrix must be computed using the [chain rule](@entry_id:147422), which involves the inverse of the **Jacobian matrix** of the mapping, $\mathbf{J} = \partial(x,y)/\partial(\xi,\eta)$. The stiffness integral is also transformed to the [parent domain](@entry_id:169388):
$$
\mathbf{K}_e = \int_{-1}^{1}\int_{-1}^{1} \mathbf{B}(\xi,\eta)^T \mathbf{D} \mathbf{B}(\xi,\eta) \, \det\mathbf{J}(\xi,\eta) \, t \, d\xi d\eta
$$
The integrand is now a complex function of $\xi$ and $\eta$, necessitating numerical integration.

### Numerical Integration and Its Consequences

The standard method for evaluating the stiffness integral for [isoparametric elements](@entry_id:173863) is **Gauss-Legendre Quadrature**. This technique approximates the integral as a weighted sum of the integrand's values at specific locations called Gauss points. The power of this method is its high accuracy; an $n$-point rule can exactly integrate a polynomial of degree up to $2n-1$. The common 1D rules are [@problem_id:2554588]:
*   **1-point:** Node at $x_1=0$, weight $w_1=2$.
*   **2-point:** Nodes at $x_{1,2}=\pm 1/\sqrt{3}$, weights $w_{1,2}=1$.
*   **3-point:** Nodes at $x_1=0, x_{2,3}=\pm \sqrt{3/5}$, weights $w_1=8/9, w_{2,3}=5/9$.

For a 2D [quadrilateral element](@entry_id:170172), a **[tensor product](@entry_id:140694)** rule is used, applying the 1D rule in each direction. The 2D integration points are all combinations $(\xi_i, \eta_j)$ of the 1D nodes, and the corresponding weights are products $W_{ij} = w_i w_j$. [@problem_id:2554588]

For the Q4 element, the standard choice is a **2x2 Gauss quadrature**. The justification lies in the polynomial degree of the integrand. For the special case where the element is a parallelogram (an [affine mapping](@entry_id:746332)), the Jacobian determinant $\det\mathbf{J}$ is constant and the $\mathbf{B}$ matrix entries are linear in $\xi$ and $\eta$. The integrand $\mathbf{B}^T \mathbf{D} \mathbf{B} \det\mathbf{J}$ is therefore a quadratic polynomial. Since a 2-point 1D rule integrates up to cubics exactly, the 2x2 tensor product rule easily integrates the quadratic 2D integrand exactly. Thus, 2x2 integration is considered **full integration** for a Q4 element and is exact for parallelograms. [@problem_id:2554560]

However, [numerical integration](@entry_id:142553) can introduce pathologies, particularly in limiting cases.

#### Volumetric Locking

In plane strain problems, as Poisson's ratio $\nu$ approaches $0.5$, the material becomes [nearly incompressible](@entry_id:752387). The terms in the [constitutive matrix](@entry_id:164908) $\mathbf{D}_{pe}$ related to the [bulk modulus](@entry_id:160069) diverge to infinity. When using full 2x2 integration for a Q4 element, the stiffness formulation effectively tries to enforce the incompressibility condition ($\epsilon_{xx} + \epsilon_{yy} = 0$) at all four Gauss points. The bilinear displacement field of the Q4 element lacks the kinematic freedom to satisfy these four independent constraints without becoming trivially rigid. This leads to an artificially stiff response, a phenomenon known as **[volumetric locking](@entry_id:172606)**. The element "locks" and cannot accurately represent deformations like bending. Notably, this issue does not arise in [plane stress](@entry_id:172193), as the material is free to deform out-of-plane, and the coefficients of $\mathbf{D}_{ps}$ remain bounded as $\nu \to 0.5$. [@problem_id:2554494]

#### Reduced Integration and Hourglassing

A common remedy for [volumetric locking](@entry_id:172606) is **reduced integration**, where a lower-order quadrature rule is used than what full integration would dictate. For the Q4 element, this means using a single Gauss point (1x1 integration). This imposes only one [incompressibility constraint](@entry_id:750592) at the element center, which the element's [displacement field](@entry_id:141476) can easily accommodate, thus alleviating locking. More advanced techniques like **[selective reduced integration](@entry_id:168281)** apply reduced integration only to the volumetric part of the stiffness matrix while fully integrating the deviatoric part. [@problem_id:2554494]

The downside of reduced integration is that it can fail to detect certain deformation modes, leading to spurious **[zero-energy modes](@entry_id:172472)**. These are non-rigid-body displacement patterns that produce zero strain at the integration point(s) and thus store zero strain energy. For a Q4 element with 1x1 integration, there are two such modes, known as **[hourglass modes](@entry_id:174855)**. These modes correspond to displacement fields that are proportional to the bilinear term $\xi\eta$ in the parent coordinates. The nodal displacement patterns for these modes are [@problem_id:2554501]:
1.  A horizontal hourglass motion: $[u_1, u_2, u_3, u_4] = [+1, -1, +1, -1]$ with zero vertical displacements.
2.  A vertical hourglass motion: $[v_1, v_2, v_3, v_4] = [+1, -1, +1, -1]$ with zero horizontal displacements.

These modes can pollute the solution with oscillations and must be controlled, often through stabilization techniques.

### Assembly of the Global System

After computing the stiffness matrix $\mathbf{K}_e$ for each element, the final step is to assemble them into a single global stiffness matrix $\mathbf{K}$ for the entire structure. This **assembly process** is a direct summation of the element contributions into the appropriate locations in the global matrix.

The mapping from an element's local degrees of freedom (DOFs) to the system's global DOFs is governed by the element's **connectivity** (the list of global node numbers for that element) and the chosen global DOF ordering. This mapping can be formally represented by a Boolean **selector matrix** $\mathbf{L}_e$, which "gathers" the relevant DOFs from the global displacement vector $\mathbf{d}$ into the local element vector: $\mathbf{d}_e = \mathbf{L}_e \mathbf{d}$. [@problem_id:2554525]

Based on the [principle of virtual work](@entry_id:138749), the [global stiffness matrix](@entry_id:138630) is formed by "scattering" each element matrix using the transpose of the selector matrix:
$$
\mathbf{K} = \sum_{e} \mathbf{L}_e^T \mathbf{K}_e \mathbf{L}_e
$$
This operation ensures that the stiffness contribution from a shared node is correctly accumulated from all adjacent elements. For instance, consider a mesh of two [triangular elements](@entry_id:167871) $e_1(1,2,3)$ and $e_2(2,4,3)$. The entry in the [global stiffness matrix](@entry_id:138630) corresponding to the interaction between the $u$-displacement of node 2 and the $v$-displacement of node 3 will receive contributions from both $\mathbf{K}_{e_1}$ and $\mathbf{K}_{e_2}$, as nodes 2 and 3 are shared. [@problem_id:2554525]

It is crucial to recognize that this assembly process is purely topological. The selector matrices $\mathbf{L}_e$ depend only on the mesh connectivity and DOF numbering scheme. They are identical for a [plane stress](@entry_id:172193) or a [plane strain](@entry_id:167046) analysis. The physical distinction between the two is entirely contained within the element stiffness matrices $\mathbf{K}_e$ through the use of the appropriate [constitutive matrix](@entry_id:164908) $\mathbf{D}$. [@problem_id:2554525]