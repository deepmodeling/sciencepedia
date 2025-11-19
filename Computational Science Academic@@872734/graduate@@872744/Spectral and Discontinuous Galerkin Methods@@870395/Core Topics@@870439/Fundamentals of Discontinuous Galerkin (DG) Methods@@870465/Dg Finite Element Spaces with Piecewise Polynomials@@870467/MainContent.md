## Introduction
The Discontinuous Galerkin (DG) method represents a powerful and flexible class of numerical techniques for [solving partial differential equations](@entry_id:136409), finding widespread use in fields from fluid dynamics to electromagnetics. Its significance lies in its ability to elegantly handle complex geometries, varying polynomial degrees, and solution discontinuities by relaxing the strict inter-[element continuity](@entry_id:165046) imposed by traditional [finite element methods](@entry_id:749389). This article addresses the foundational question of how these flexible approximation spaces are formally constructed. By delving into the architecture of DG spaces, it bridges the gap between the abstract concept of "allowing discontinuities" and the concrete mathematical machinery required for a robust implementation.

This article will guide you through the essential components of DG finite element spaces. In the "Principles and Mechanisms" section, you will learn how to build these spaces from the ground up, starting with the mesh, defining broken [function spaces](@entry_id:143478) with [piecewise polynomials](@entry_id:634113), and introducing the critical jump and average operators. Following this, the "Applications and Interdisciplinary Connections" section will demonstrate how this unique construction enables a vast range of applications, from solving classic PDEs to tackling cutting-edge problems in data science and uncertainty quantification. Finally, the "Hands-On Practices" section will offer you the opportunity to solidify your understanding by working through concrete exercises on key concepts like [polynomial space](@entry_id:269905) dimensions and [numerical quadrature](@entry_id:136578).

## Principles and Mechanisms

The Discontinuous Galerkin (DG) methodology is built upon a unique finite element framework that replaces the strict continuity requirements of traditional methods with a more flexible element-wise construction. This chapter elucidates the core principles and mechanisms underpinning DG finite element spaces. We will begin by defining the properties of the computational mesh, proceed to construct the "broken" function spaces that reside upon it, and then detail the essential operators and transformations required for analysis and implementation.

### The Domain Discretization: Meshes and Their Properties

The foundation of any finite element method is the partitioning of the computational domain $\Omega \subset \mathbb{R}^d$ into a collection of smaller, non-overlapping geometric shapes called elements. This partition, or **mesh**, is denoted by $\mathcal{T}_h$.

Let $\mathcal{T}_h$ be a collection of open, connected polyhedral subdomains $K$ (the elements) with pairwise disjoint interiors, such that their closures cover the domain, i.e., $\overline{\Omega} = \bigcup_{K \in \mathcal{T}_h} \overline{K}$. The subscript $h$ represents a [characteristic length](@entry_id:265857) scale of the mesh, typically defined as the maximum element diameter, $h := \max_{K \in \mathcal{T}_h} h_K$, where $h_K := \operatorname{diam}(K)$.

In the analysis of [finite element methods](@entry_id:749389), several key properties of the mesh family $\{\mathcal{T}_h\}_h$ are crucial.

- **Conforming Meshes**: A mesh is called **conforming** if the intersection of the [closures](@entry_id:747387) of any two distinct elements, $\overline{K} \cap \overline{K'}$, is either empty or a common lower-dimensional [simplex](@entry_id:270623) (i.e., a shared face, edge, or vertex). This condition precludes "[hanging nodes](@entry_id:750145)," where a vertex of one element lies in the interior of a face or edge of an adjacent element. While traditional continuous Galerkin methods strictly require conforming meshes, DG methods are more flexible, as we will see later.

- **Shape-Regularity**: A family of meshes is said to be **shape-regular** if the elements do not degenerate as the mesh is refined ($h \to 0$). This is formalized by requiring that the ratio of an element's diameter $h_K$ to the diameter of the largest inscribed ball (the inradius, $\rho_K$) remains uniformly bounded. That is, there exists a constant $\sigma > 0$, independent of $h$, such that for all $K \in \mathcal{T}_h$ across the entire family of meshes, we have $h_K / \rho_K \le \sigma$. Shape-regularity prevents elements from becoming arbitrarily "skinny" or "flat," which is essential for preserving the approximation quality of the finite element space. A critical consequence of [shape-regularity](@entry_id:754733) is that the diameter of any face $F$ of an element $K$, denoted $h_F$, is guaranteed to be proportional to the diameter of the element itself, i.e., $h_F \approx h_K$ [@problem_id:3375091].

- **Quasi-Uniformity**: A family of meshes is **quasi-uniform** if all elements in any given mesh have roughly the same size. Formally, there exists a constant $c > 0$ such that $h_K \ge c h$ for all elements $K \in \mathcal{T}_h$. This implies that element diameters are uniformly comparable to the global mesh parameter $h$. It is important to distinguish this from [shape-regularity](@entry_id:754733): a mesh can be shape-regular (all elements are well-shaped) but highly non-quasi-uniform if it features regions of extreme local refinement, as is common in adaptive simulations.

### Broken Function Spaces

The defining characteristic of the DG methodology is its use of function spaces that permit discontinuities across element interfaces. This is formalized through the concept of a **broken Sobolev space**.

Given a mesh $\mathcal{T}_h$, the broken Sobolev space $H^s(\mathcal{T}_h)$ for an integer $s \ge 0$ is defined as the set of functions that are globally square-integrable and possess $H^s$ regularity *within each element*:
$$
H^s(\mathcal{T}_h) := \{ v \in L^2(\Omega) : v|_K \in H^s(K) \text{ for all } K \in \mathcal{T}_h \}
$$
Here, $v|_K$ denotes the restriction of the function $v$ to the element $K$. This space is equipped with a natural norm given by the sum of the local norms: $\|v\|_{H^s(\mathcal{T}_h)}^2 := \sum_{K \in \mathcal{T}_h} \|v\|_{H^s(K)}^2$. Correspondingly, we can define a **broken gradient** $\nabla_h v$, which is a vector field defined piecewise by $(\nabla_h v)|_K := \nabla(v|_K)$ for each $K \in \mathcal{T}_h$.

The fundamental distinction between this broken space and the standard global Sobolev space $H^1(\Omega)$ is the relaxation of continuity constraints [@problem_id:3375102]. Any function $v \in H^1(\Omega)$ is, by definition, also in $H^1(\mathcal{T}_h)$, as its restriction to any element $K$ will be in $H^1(K)$. Thus, $H^1(\Omega)$ is a subspace of $H^1(\mathcal{T}_h)$. The converse is not true. A function $v \in H^1(\mathcal{T}_h)$ belongs to the global space $H^1(\Omega)$ if and only if its **traces** match across all interior element interfaces. A function in $H^1(\mathcal{T}_h)$ that does not satisfy this condition will exhibit **jumps** at the boundaries between elements. It is precisely this allowance for jumps that gives DG methods their name and much of their flexibility.

### Piecewise Polynomial Finite Element Spaces

For computational purposes, we work with finite-dimensional subspaces of the broken Sobolev spaces. The most common choice is to construct a space of [piecewise polynomials](@entry_id:634113). The **discontinuous finite element space** of degree $k$, denoted $V_h$, is defined as:
$$
V_h := \{ v \in L^2(\Omega) : v|_K \in \mathbb{P}_k(K) \text{ for all } K \in \mathcal{T}_h \}
$$
where $\mathbb{P}_k(K)$ is the space of polynomials of total degree at most $k$ on the element $K$. Since polynomials are infinitely differentiable on any bounded element, it is clear that $V_h \subset H^s(\mathcal{T}_h)$ for any $s \ge 0$.

The choice of [polynomial space](@entry_id:269905) on each element can significantly impact the method's performance, especially on non-simplicial elements like quadrilaterals or hexahedra. Two common choices are:
-   **Total-degree polynomials**, $\mathbb{P}_k$: The space of polynomials whose total degree of monomials is at most $k$. For example, in 2D, $x^{\alpha}y^{\beta}$ is included if $\alpha + \beta \le k$.
-   **Tensor-product polynomials**, $\mathbb{Q}_k$: The space of polynomials whose degree in each coordinate direction is at most $k$. In 2D, $x^{\alpha}y^{\beta}$ is included if $\alpha \le k$ and $\beta \le k$.

For $d>1$ and $k \ge 1$, $\mathbb{P}_k$ is a proper subspace of $\mathbb{Q}_k$. The larger $\mathbb{Q}_k$ space contains more basis functions (e.g., $x^k y^k$ is in $\mathbb{Q}_k$ but not $\mathbb{P}_k$), offering greater approximation power at a higher computational cost. For instance, when solving the [linear advection equation](@entry_id:146245), the superior approximation capability of $\mathbb{Q}_k$ spaces is particularly evident for waves propagating obliquely to the mesh axes. By capturing more terms in the multivariate Taylor expansion of the [plane wave solution](@entry_id:181082), $\mathbb{Q}_k$ bases can lead to significantly lower [numerical dispersion and dissipation](@entry_id:752783) compared to $\mathbb{P}_k$ bases of the same degree [@problem_id:3375139].

### Operators on the Mesh Skeleton: Jumps and Averages

To formulate a DG method, we must be able to quantify the discontinuities at element interfaces. This is achieved through jump and average operators defined on the **mesh skeleton**, which is the union of all element boundaries. The skeleton $\mathcal{F}_h$ is composed of interior faces $\mathcal{F}_h^{\mathrm{i}}$ and boundary faces $\mathcal{F}_h^{\partial}$.

Consider an interior face $F \in \mathcal{F}_h^{\mathrm{i}}$ shared by two elements, $K^-$ and $K^+$. We denote the unit outward normal vectors to the respective elements on this face as $\mathbf{n}^-$ and $\mathbf{n}^+$, noting that $\mathbf{n}^+ = -\mathbf{n}^-$. For a function $v \in H^s(\mathcal{T}_h)$ with $s > 1/2$, its **traces** on $F$ from the interior of each element, denoted $v^-$ and $v^+$, are well-defined.

With these conventions, we define the following fundamental operators [@problem_id:3375129]:

-   **Scalar Functions ($v$)**:
    -   **Average**: $\{ v \} := \frac{1}{2} (v^- + v^+)$
    -   **Jump**: $\llbracket v \rrbracket := v^- \mathbf{n}^- + v^+ \mathbf{n}^+$. This is a vector quantity pointing in the normal direction. A commonly used scalar jump is defined by choosing a fixed normal $\mathbf{n}$ (e.g., $\mathbf{n}=\mathbf{n}^+$) and writing $[v] = v^- - v^+$.

-   **Vector-Valued Functions ($\mathbf{q}$)**:
    -   **Average**: $\{ \mathbf{q} \} := \frac{1}{2} (\mathbf{q}^- + \mathbf{q}^+)$
    -   **Jump (Normal Component)**: $\llbracket \mathbf{q} \rrbracket := \mathbf{q}^- \cdot \mathbf{n}^- + \mathbf{q}^+ \cdot \mathbf{n}^+$. This is a scalar quantity measuring the jump in the normal flux.

On a **boundary face** $F \in \mathcal{F}_h^{\partial}$, which is part of only one element $K$, the operators are defined by convention, typically setting the "exterior" trace to a value determined by the boundary condition. For homogeneous Dirichlet conditions, for instance, the exterior trace is taken as zero, leading to: $\{ v \} := v$, $\llbracket v \rrbracket := v \mathbf{n}$, $\{ \mathbf{q} \} := \mathbf{q}$, and $\llbracket \mathbf{q} \rrbracket := \mathbf{q} \cdot \mathbf{n}$.

These definitions are not arbitrary. They arise naturally from element-wise [integration by parts](@entry_id:136350). For problems whose solutions naturally reside in the space $H(\mathrm{div}, \Omega)$ (e.g., fluid flux, [electric displacement field](@entry_id:203286)), the physically continuous quantity across interfaces is the normal component. The integration-by-parts formula for the [divergence operator](@entry_id:265975) indeed produces boundary terms involving the normal flux $\mathbf{q} \cdot \mathbf{n}$. Consequently, DG methods for such problems are designed to weakly enforce the continuity of the normal component by penalizing or formulating [numerical fluxes](@entry_id:752791) based on its jump, $\llbracket \mathbf{q} \rrbracket$ [@problem_id:3375120]. Similarly, for problems in $H(\mathrm{curl}, \Omega)$ (e.g., magnetic fields), the continuous quantity is the tangential component, and the **tangential jump**, $\llbracket \mathbf{q} \rrbracket_{\boldsymbol{t}} := \mathbf{n}^- \times \mathbf{q}^- + \mathbf{n}^+ \times \mathbf{q}^+$, becomes the central object in the DG formulation.

### The Reference Element Framework

Practical implementation of DG methods relies heavily on the **[reference element](@entry_id:168425)** concept. All computations, such as evaluating integrals and derivatives, are performed on a single, fixed [reference element](@entry_id:168425) $\hat{K}$ (e.g., the unit simplex or the cube $[-1, 1]^d$) and then mapped to the corresponding physical element $K$ in the mesh.

This is accomplished via a smooth, invertible **element map** $F_K: \hat{K} \to K$.
-   For **[simplices](@entry_id:264881)**, this map is typically an **affine map** of the form $F_K(\hat{x}) = x_1 + B_K \hat{x}$, where $B_K$ is a constant matrix determined by the vertices of the physical [simplex](@entry_id:270623) [@problem_id:3375140].
-   For elements with **curved boundaries**, a non-affine **isoparametric map** is used, where the geometry itself is represented by the same polynomial basis functions used for the solution: $F_K(\hat{x}) = \sum_{i=1}^N x_i \varphi_i(\hat{x})$, where $\{x_i\}$ are control points and $\{\varphi_i\}$ are basis functions on $\hat{K}$.

This mapping framework requires transforming all derivatives and integrals between the physical and reference coordinate systems. The key object governing these transformations is the **Jacobian matrix** of the map, $J_K(\hat{x}) = \nabla_{\hat{x}} F_K(\hat{x})$.

-   **Transformation of Derivatives**: The [chain rule](@entry_id:147422) gives a fundamental relationship between the gradient in physical coordinates ($\nabla_x$) and reference coordinates ($\nabla_{\hat{x}}$). For a scalar function $\phi(x) = \hat{\phi}(\hat{x})$ where $x=F_K(\hat{x})$, the gradients are related by [@problem_id:3375113]:
    $$
    \nabla_x \phi(x) = J_K(\hat{x})^{-T} \nabla_{\hat{x}} \hat{\phi}(\hat{x})
    $$
    where $J_K^{-T}$ is the transpose of the inverse of the Jacobian matrix.

-   **Transformation of Integrals**: The standard change-of-variables formula applies for [volume integrals](@entry_id:183482):
    $$
    \int_K \phi(x) \, dx = \int_{\hat{K}} \phi(F_K(\hat{x})) |\det(J_K(\hat{x}))| \, d\hat{x}
    $$
    The transformation for [surface integrals](@entry_id:144805) over a face $F=F_K(\hat{F})$ is more complex. The relationship between a physical surface element $n \, ds_x$ and a reference surface element $\hat{n} \, d\hat{s}$ is given by **Nanson's formula**:
    $$
    n \, ds_x = \det(J_K) J_K^{-T} \hat{n} \, d\hat{s}
    $$
    This identity reveals both the transformation of the normal vector, $n \propto J_K^{-T}\hat{n}$, and the scaling factor for the surface [area element](@entry_id:197167), $ds_x = |\det(J_K)| \|J_K^{-T} \hat{n}\| \, d\hat{s} = \|\operatorname{cof}(J_K) \hat{n}\| \, d\hat{s}$ [@problem_id:3375140]. This scaling factor is the surface Jacobian that must be included when evaluating face integrals on the reference element.

An important consequence arises when the map $F_K$ is non-affine (e.g., for [curved elements](@entry_id:748117)). In this case, $J_K$ is not constant. If we pull back a polynomial [basis function](@entry_id:170178) $\hat{\phi}$ from $\hat{K}$ to $K$, the resulting function $\phi(x) = \hat{\phi}(F_K^{-1}(x))$ is generally a [rational function](@entry_id:270841), not a polynomial. This means that integrands in the DG [weak form](@entry_id:137295), such as $\nabla_x \phi_i \cdot \nabla_x \phi_j |\det(J_K)|$, become complicated rational functions on the reference element. Standard numerical quadrature schemes like Gaussian quadrature are not exact for such integrands, leading to a **[quadrature error](@entry_id:753905)** that can affect the overall accuracy of the method [@problem_id:3375113].

### Basis Representations

Within a given [polynomial space](@entry_id:269905) on the reference element, e.g., $\mathbb{Q}_k([-1,1]^d)$, we can choose different sets of basis functions. The choice can have profound implications for the structure of the resulting discrete system and the efficiency of the method.

-   **Modal Bases**: A basis is **modal** if its functions have a direct physical or mathematical meaning, such as representing different frequency modes. A common choice is a basis of orthogonal polynomials, like the Legendre polynomials on $[-1,1]$. A [tensor product](@entry_id:140694) of 1D Legendre polynomials forms an [orthogonal basis](@entry_id:264024) for $\mathbb{Q}_k([-1,1]^d)$ with respect to the $L^2$ inner product. A key advantage of an orthogonal [modal basis](@entry_id:752055) is that the **mass matrix**, $M_{\alpha\beta} = \int_{\hat{K}} \phi_\alpha \phi_\beta \, d\hat{x}$, is **diagonal** [@problem_id:3375086]. This property simplifies some theoretical analyses and decouples equations for certain problems.

-   **Nodal Bases**: A basis is **nodal** if each basis function is associated with a specific point (node) in the element and has the value 1 at its own node and 0 at all others. The most common example is the Lagrange basis. For a nodal basis built on an arbitrary set of points, the [mass matrix](@entry_id:177093) is generally dense.

A powerful synergy between these concepts is achieved by using a nodal basis constructed at a specific set of points: the **Gauss-Lobatto-Legendre (GLL) points**. While the exact [mass matrix](@entry_id:177093) for a GLL nodal basis is not diagonal, a remarkable property emerges when the [mass matrix](@entry_id:177093) integral is computed numerically using GLL quadrature with the basis nodes themselves as quadrature points. Due to the interpolatory property of the Lagrange basis functions, the resulting quadrature-based [mass matrix](@entry_id:177093), $M^q$, becomes perfectly diagonal [@problem_id:3375086]. This phenomenon, known as **[mass lumping](@entry_id:175432)**, is extremely beneficial computationally, as it makes inverting the [mass matrix](@entry_id:177093) trivial. This is a cornerstone of efficient time-domain spectral element and DG methods.

### Norms and Nonconforming Meshes

We conclude by touching upon two important topics that build upon the preceding principles: the [mathematical analysis](@entry_id:139664) of stability and the practical handling of complex geometries.

#### A Norm for Discontinuous Spaces

To prove the stability and convergence of a DG method, it is essential to equip the finite element space $V_h$ with a suitable norm that captures the essential features of the [discretization](@entry_id:145012). A standard choice is the **DG energy norm**, defined as:
$$
\|v\|_{DG}^2 := \sum_{K \in \mathcal{T}_h} \|\nabla_h v\|_{L^2(K)}^2 + \sum_{F \in \mathcal{F}_h} \sigma_F h_F^{-1} \|\llbracket v \rrbracket\|_{L^2(F)}^2
$$
Here, $\sigma_F > 0$ are penalty parameters that can be chosen to ensure stability. For this expression to be a true norm on $V_h$, it must be [positive definite](@entry_id:149459); that is, $\|v\|_{DG} = 0$ must imply $v \equiv 0$. Let's trace the argument [@problem_id:3375141]:
1.  If $\|v\|_{DG} = 0$, both terms in the sum must be zero.
2.  $\sum_{K} \|\nabla_h v\|_{L^2(K)}^2 = 0$ implies that $\nabla v = 0$ on every element $K$. Since $v|_K$ is a polynomial, this means $v$ must be a piecewise [constant function](@entry_id:152060), i.e., $v|_K = c_K$.
3.  $\sum_{F \in \mathcal{F}_h^{\mathrm{i}}} \sigma_F h_F^{-1} \|\llbracket v \rrbracket\|_{L^2(F)}^2 = 0$ implies the jump is zero on all interior faces. For a piecewise [constant function](@entry_id:152060), this means $c_K = c_{K'}$ for any two adjacent elements.
4.  If the domain $\Omega$ (and thus the mesh) is connected, this forces all constants to be equal: $v(x) = C$ for some global constant $C$.
5.  Finally, $\sum_{F \in \mathcal{F}_h^{\partial}} \sigma_F h_F^{-1} \|\llbracket v \rrbracket\|_{L^2(F)}^2 = 0$ implies the jump on the boundary is zero. By our convention, this means the trace of $v$ on the boundary is zero. For a constant function $v=C$, this requires $C=0$.

Therefore, under the conditions of a [connected domain](@entry_id:169490) and the inclusion of penalties on jumps across *all* faces (interior and boundary), the DG energy expression is a norm on the space $V_h$.

#### Nonconforming Meshes and Hanging Nodes

One of the great practical advantages of the DG framework is its ability to naturally handle **nonconforming meshes** containing **[hanging nodes](@entry_id:750145)**. This feature is critical for efficient local [mesh refinement](@entry_id:168565) ($h$-adaptivity).

The presence of [hanging nodes](@entry_id:750145) does not alter the fundamental definition of the broken Sobolev space $H^s(\mathcal{T}_h)$, which is based purely on element-wise properties [@problem_id:3375094]. However, it requires a careful redefinition of the mesh skeleton used for jump and average operators. An interface involving a [hanging node](@entry_id:750144) (e.g., where one large face abuts two smaller faces) cannot be treated as a single face, because it is not shared by exactly two elements.

The correct procedure is to decompose such nonconforming interfaces into a collection of **subfaces**. Each subface is defined as a maximal open set shared by the boundaries of exactly two elements. On each of these subfaces, a pair of opposing normal vectors is well-defined, and the standard jump and average operators can be applied without ambiguity [@problem_id:3375094]. By summing face integrals over this refined set of subfaces, the entire DG formulation extends seamlessly to nonconforming meshes, providing a powerful tool for complex simulations.