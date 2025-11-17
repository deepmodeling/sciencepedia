## Introduction
Second-order elliptic equations are foundational to modeling a vast array of physical phenomena, from heat conduction and fluid flow to [structural mechanics](@entry_id:276699). While traditional conforming Finite Element Methods (FEM) have long been the standard for obtaining numerical solutions, they face significant challenges when dealing with complex geometries, [non-conforming meshes](@entry_id:752550), or problems with discontinuous material properties. The requirement of solution continuity across element boundaries imposes constraints that can limit flexibility and complicate implementation. This knowledge gap calls for a more adaptable numerical framework.

The Discontinuous Galerkin (DG) method emerges as a powerful and versatile alternative that resolves these limitations by embracing, rather than avoiding, discontinuity. By allowing the approximate solution to be discontinuous across element interfaces, DG methods offer unparalleled flexibility in mesh design, polynomial degree selection, and handling of complex physics. This article serves as a comprehensive guide to the theory and application of DG methods for second-order elliptic problems.

Across the following chapters, you will gain a deep understanding of this robust numerical technique. We will begin in "Principles and Mechanisms" by dissecting the core mathematical concepts, from the broken function spaces to the derivation of the widely used Symmetric Interior Penalty Galerkin (SIPG) scheme and its variants. Next, the "Applications and Interdisciplinary Connections" chapter will demonstrate the method's practical utility in advanced scenarios, including [adaptive mesh refinement](@entry_id:143852) for singular problems and the solution of [eigenvalue problems](@entry_id:142153). Finally, "Hands-On Practices" will offer a chance to engage with the material directly, solidifying your understanding of the key computational mechanisms. We begin our exploration with the essential principles that underpin the entire DG methodology.

## Principles and Mechanisms

The Discontinuous Galerkin (DG) methodology for second-order elliptic problems represents a paradigm shift from traditional conforming Finite Element Methods (FEM). Where conforming methods build approximations from function spaces that enforce continuity across element boundaries, DG methods embrace discontinuity. This choice grants significant flexibility, particularly for handling complex geometries, [non-conforming meshes](@entry_id:752550), and variable polynomial degrees. However, this freedom comes at a cost: the mathematical framework must be carefully constructed to control the discontinuities and ensure a stable, convergent numerical scheme. This chapter elucidates the core principles and mechanisms that form the foundation of these powerful methods.

### The Discontinuous Approximation Space

The first step in constructing a DG method is to define the function space in which we seek our approximate solution. Instead of the standard Sobolev space $H^1(\Omega)$, which contains functions that are continuous across element interfaces, we work in a larger, more flexible space.

We begin with a partition, or mesh, $\mathcal{T}_h$ of the problem domain $\Omega$ into a set of non-overlapping elements $K$. The fundamental idea of DG is to build a solution that is a polynomial *within* each element, without initially imposing any conditions on how the solution behaves across the boundaries between elements. This leads to the definition of the **broken Sobolev space**, denoted as $H^1(\mathcal{T}_h)$:

$H^1(\mathcal{T}_h) = \{ v \in L^2(\Omega) : v|_K \in H^1(K) \text{ for all } K \in \mathcal{T}_h \}$

A function $v$ in $H^1(\mathcal{T}_h)$ is globally square-integrable, and its restriction $v|_K$ to any element $K$ possesses a square-integrable [weak gradient](@entry_id:756667) on that element. Crucially, the definition does not require the traces of $v$ from adjacent elements to match on their shared boundary [@problem_id:3377353]. This is the "discontinuous" nature of the space. Correspondingly, we define the **broken gradient**, $\nabla_h v$, as the operator that computes the gradient element-by-element: $(\nabla_h v)|_K = \nabla(v|_K)$. Since the gradient is well-defined and square-integrable on each of the finite number of elements, the resulting broken gradient $\nabla_h v$ is a member of $L^2(\Omega)^d$ [@problem_id:3377353].

It is clear from these definitions that the standard Sobolev space $H^1(\Omega)$ is a proper subspace of the broken space $H^1(\mathcal{T}_h)$. Any function in $H^1(\Omega)$ is by definition also in $L^2(\Omega)$ and its restriction to any element $K$ is in $H^1(K)$. The key difference is that for a function $w \in H^1(\Omega)$, the traces on any interior face are single-valued, meaning the function is continuous across element boundaries [@problem_id:3377353]. This property of continuity is abandoned in the larger space $H^1(\mathcal{T}_h)$.

### Derivation of the Discrete Form: Jumps and Averages

To derive the DG formulation for a model elliptic problem, such as the Poisson equation $-\nabla \cdot (\kappa \nabla u) = f$, we follow the standard Galerkin procedure. We multiply the equation by a test function $v_h$ from our discrete approximation space (a subspace of $H^1(\mathcal{T}_h)$ consisting of [piecewise polynomials](@entry_id:634113)) and integrate over each element $K$:

$\int_K (-\nabla \cdot (\kappa \nabla u)) v_h \, d\mathbf{x} = \int_K f v_h \, d\mathbf{x}$

Applying Green's first identity (integration by parts) on each element yields:

$\int_K \kappa \nabla u \cdot \nabla v_h \, d\mathbf{x} - \int_{\partial K} (\kappa \nabla u \cdot \mathbf{n}_K) v_h \, d\mathbf{x} = \int_K f v_h \, d\mathbf{x}$

Here, $\mathbf{n}_K$ is the outward-pointing [unit normal vector](@entry_id:178851) on the boundary $\partial K$ of the element. Summing over all elements $K \in \mathcal{T}_h$ gives:

$\sum_{K \in \mathcal{T}_h} \int_K \kappa \nabla u \cdot \nabla v_h \, d\mathbf{x} - \sum_{K \in \mathcal{T}_h} \int_{\partial K} (\kappa \nabla u \cdot \mathbf{n}_K) v_h \, d\mathbf{x} = \int_{\Omega} f v_h \, d\mathbf{x}$

The first term is a sum of element-wise integrals that is straightforward to handle. The second term, a sum of integrals over all element boundaries, requires careful treatment. For a continuous solution $u$, the flux $\kappa \nabla u \cdot \mathbf{n}$ is single-valued across any interior face, and the contributions from adjacent elements would partially cancel. However, for a [discontinuous function](@entry_id:143848) $u_h \in H^1(\mathcal{T}_h)$, both the function value $u_h$ and its gradient $\nabla_h u_h$ can have different values on either side of a face.

To manage this, we introduce the concepts of **jumps** and **averages** across faces. Let $F$ be an interior face shared by two elements, $K^-$ and $K^+$. We denote the trace of a function $w$ on $F$ approached from $K^-$ as $w^-$ and from $K^+$ as $w^+$. Let $\mathbf{n}^-$ and $\mathbf{n}^+$ be the outward unit normals to $F$ from $K^-$ and $K^+$, respectively, noting that $\mathbf{n}^- = -\mathbf{n}^+$. We define the jump and average of a scalar function $v$ and a vector flux $\mathbf{q}$ as follows [@problem_id:3377352]:

- **Scalar Jump:** $[v] = v^- - v^+$
- **Scalar Average:** $\{v\} = \frac{1}{2}(v^- + v^+)$
- **Vector Flux Average:** $\{\mathbf{q} \cdot \mathbf{n}\} = \frac{1}{2}(\mathbf{q}^- \cdot \mathbf{n}^- + \mathbf{q}^+ \cdot \mathbf{n}^+)$

With these definitions, the sum of boundary integrals over all interior faces can be artfully rewritten. For each interior face $F$, the sum contains two terms: $\int_F (\kappa \nabla u \cdot \mathbf{n}^-) v^- \, ds$ and $\int_F (\kappa \nabla u \cdot \mathbf{n}^+) v^+ \, ds$. The continuous problem provides a single condition for the flux, but the discontinuous setting requires us to design a **[numerical flux](@entry_id:145174)** to replace the term $\kappa \nabla u \cdot \mathbf{n}$ at the interfaces, thereby linking the solution between adjacent elements.

### The Symmetric Interior Penalty Galerkin (SIPG) Method

The Symmetric Interior Penalty Galerkin (SIPG) method is a popular and foundational DG scheme that arises from a specific choice of [numerical flux](@entry_id:145174). The final discrete [bilinear form](@entry_id:140194) $a_h(u_h, v_h)$ for finding a solution $u_h \in V_h \subset H^1(\mathcal{T}_h)$ is composed of three parts:

$a_h(u_h, v_h) = \sum_{K \in \mathcal{T}_h} \int_K \kappa \nabla_h u_h \cdot \nabla_h v_h \, d\mathbf{x} - \sum_{F \in \mathcal{F}_i \cup \mathcal{F}_b} \int_F \left( \{\kappa \nabla_h u_h \cdot \mathbf{n}\} [v_h] + \{\kappa \nabla_h v_h \cdot \mathbf{n}\} [u_h] \right) \, ds + \sum_{F \in \mathcal{F}_i \cup \mathcal{F}_b} \int_F \frac{\sigma}{h_F} [u_h] [v_h] \, ds$

(On boundary faces $\mathcal{F}_b$, the jump and average operators are defined by setting the exterior value and flux to the data prescribed by boundary conditions.)

Let's dissect this form:
1.  **Element-wise Diffusion:** The first term, $\sum_K \int_K \kappa \nabla_h u_h \cdot \nabla_h v_h \, d\mathbf{x}$, is the natural [weak form](@entry_id:137295) of the [diffusion operator](@entry_id:136699) inside each element.
2.  **Symmetry and Consistency:** The second term, involving averages of fluxes and jumps of functions, ensures that the formulation is **consistent** (i.e., the exact solution to the continuous problem satisfies the discrete equations) and **symmetric** (i.e., $a_h(u_h, v_h) = a_h(v_h, u_h)$).
3.  **Penalty:** The third term is the **interior penalty**. It is a crucial addition that penalizes the jump of the solution across faces. Here, $\sigma$ is a positive, user-defined **[penalty parameter](@entry_id:753318)**, and $h_F$ is a characteristic length of the face $F$.

To illustrate these terms in action, consider a simple numerical example. Let $\Omega = (0,2) \times (0,1)$ be divided into two elements $K_1 = (0,1) \times (0,1)$ and $K_2 = (1,2) \times (0,1)$, separated by the interior face $F$ at $x=1$. Let the diffusion coefficient be $\kappa=2$ on $K_1$ and $\kappa=3$ on $K_2$. For discontinuous linear functions like $u_h(x,y)=x+2y$ on $K_1$ and $u_h(x,y)=4-2x+y$ on $K_2$, we can compute all the necessary components on face $F$: the traces $u_h^- = 1+2y$ and $u_h^+ = 2+y$; the jump $[u_h] = (1+2y)-(2+y) = y-1$; the normal fluxes $\kappa^- \nabla u_h^- \cdot \mathbf{n}^- = 2$ and $\kappa^+ \nabla u_h^+ \cdot \mathbf{n}^+ = 6$; and the average flux $\{\kappa \nabla u_h \cdot \mathbf{n}\} = \frac{1}{2}(2+6)=4$. These ingredients can then be integrated over the face to compute its contribution to the global system [@problem_id:3377352].

#### Stability and the Penalty Parameter

The penalty term is not merely a technicality; it is essential for the stability and [well-posedness](@entry_id:148590) of the entire method. The term $\sum_K \|\nabla_h v\|_{L^2(K)}^2$ on its own is only a semi-norm on the broken space $H^1(\mathcal{T}_h)$. It is zero for any piecewise [constant function](@entry_id:152060), not just the zero function. For example, a function that is 1 on one element and 0 on all others has a zero broken gradient but is not the zero function [@problem_id:3377353]. This means the diffusion term alone cannot guarantee a unique solution.

The penalty term rectifies this. By adding the sum of squared jumps over all faces, we create a DG norm, typically of the form:

$\|v\|_{\mathrm{DG}}^2 = \sum_{K \in \mathcal{T}_h} \|\nabla v\|_{L^2(K)}^2 + \sum_{F \in \mathcal{F}_i \cup \mathcal{F}_b} \frac{\sigma}{h_F} \|[v]\|_{L^2(F)}^2$

This expression is a true norm on the discrete space. If $\|v\|_{\mathrm{DG}}=0$, the first term implies $v$ is piecewise constant. The second term then implies the jumps are zero, meaning the constants on all adjacent elements must be equal. For a [connected domain](@entry_id:169490), this means $v$ is a single global constant. If the domain has a boundary where Dirichlet conditions are enforced (e.g., $u=0$), the boundary penalty term will force this constant to be zero. Thus, only the zero function has a zero DG norm [@problem_id:3377353].

For the [bilinear form](@entry_id:140194) $a_h(\cdot, \cdot)$ to be coercive with respect to this norm (i.e., $a_h(v_h, v_h) \ge C \|v_h\|_{\mathrm{DG}}^2$), the [penalty parameter](@entry_id:753318) $\sigma$ must be chosen sufficiently large. A rigorous analysis involving an [inverse trace inequality](@entry_id:750809) shows that $\sigma$ must be large enough to control terms arising from the consistency part of the form. A [sufficient condition for stability](@entry_id:271243) is to choose $\sigma$ on each face $F$ such that:

$\sigma \ge C p^2 \max_{K \in \mathcal{T}_h(F)} \kappa_K$

where $C$ is a constant depending only on the [shape-regularity](@entry_id:754733) of the mesh. The dependence on $p^2$ is needed to balance the norm of a polynomial's gradient on an element with its trace on the boundary. The dependence on $\max(\kappa_K)$ is critical for problems with high contrast in material properties, ensuring the penalty is strong enough to control the flux from the more diffusive side of the interface.

### Computational Mechanisms

The theoretical formulation must be translated into a computational algorithm. This involves representing functions, transforming coordinates, and approximating integrals.

#### Basis Functions and Mappings

In practice, all calculations are performed on a standard **reference element**, $\widehat{K}$ (e.g., the square $[-1,1]^2$ or the reference triangle). A mapping $T_K: \widehat{K} \to K$ relates the reference coordinates $(\xi, \eta)$ to the physical coordinates $(x,y)$ on each element $K$. The discrete solution $u_h$ on $K$ is represented as a linear combination of basis functions $\phi_i$ defined on the physical element, which are themselves [pullbacks](@entry_id:160469) of reference basis functions $\widehat{\phi}_i$ on $\widehat{K}$. Common choices for basis functions include tensor products of **Legendre polynomials** (a [modal basis](@entry_id:752055)) or **Lagrange interpolants** at specific nodes like Gauss-Lobatto-Legendre points (a nodal basis) [@problem_id:3377356].

To compute the volume integral $\int_K \kappa \nabla u_h \cdot \nabla v_h \, d\mathbf{x}$, we must transform both the [gradient operator](@entry_id:275922) and the differential [area element](@entry_id:197167) to the reference domain. The chain rule connects the physical gradient $\nabla_x$ to the reference gradient $\nabla_\xi$ via the **Jacobian matrix** $J$ of the mapping: $\nabla_x u = (J^{-1})^T \nabla_\xi \widehat{u}$. The [area element](@entry_id:197167) transforms as $d\mathbf{x} = \det(J) \, d\boldsymbol{\xi}$. For an [affine mapping](@entry_id:746332), the Jacobian is constant, simplifying the calculation considerably. For instance, the stiffness matrix entry for the [basis function](@entry_id:170178) $\phi_{10}$ (corresponding to $\widehat{\phi}_{10}(\xi,\eta) = \xi$) on a rectangular element of size $h_x \times h_y$ can be derived from first principles to be $a_K(\phi_{10}, \phi_{10}) = 4\kappa \frac{h_y}{h_x}$ [@problem_id:3377356].

#### Assembly, Quadrature, and Sparsity

The integrals defining the bilinear form are rarely computed analytically; instead, they are approximated using **[numerical quadrature](@entry_id:136578)** rules. A quadrature rule with an **exactness degree** of $m$ can exactly integrate any polynomial of degree up to $m$. To integrate the SIPG [bilinear form](@entry_id:140194) exactly, one must determine the highest polynomial degree of the integrands.
-   For the volume term $\int_K \kappa \nabla u_h \cdot \nabla v_h$, if $u_h, v_h$ are polynomials of degree $p$, their gradients are of degree $p-1$, and the product is of degree $2p-2$. Thus, the volume quadrature must be exact to degree $m_{\text{vol}} = 2p-2$.
-   For the face penalty term $\int_F \frac{\sigma}{h_F} [u_h] [v_h]$, the traces are of degree $p$, so their product is of degree $2p$. This term dictates the face quadrature requirement: $m_{\text{face}} = 2p$ [@problem_id:3377365].

Using a [quadrature rule](@entry_id:175061) with insufficient [exactness](@entry_id:268999) (under-integration) constitutes a "[variational crime](@entry_id:178318)." While the symmetry of the SIPG form is preserved even with under-integration (since the integrands are pointwise symmetric), consistency is lost. The algebraic cancellation that allows the method to exactly reproduce the continuous solution fails, potentially degrading the method's accuracy and convergence order [@problem_id:3377365].

The final step is to assemble the global linear system $A \mathbf{u} = \mathbf{b}$. The [stiffness matrix](@entry_id:178659) $A$ is built by looping over all elements and faces and adding their respective integral contributions to the appropriate matrix entries. A key feature of DG methods is the **sparsity pattern** of $A$. Because the [bilinear form](@entry_id:140194) only involves integrals over an element or a face, the degrees of freedom (DoFs) associated with an element $K$ are only coupled to the DoFs on $K$ itself and to the DoFs on its immediate face-neighbors. This results in a block-sparse matrix, where each block corresponds to the interactions between two elements. For a 2D [triangulation](@entry_id:272253), each element block couples to itself and its three neighbors. Increasing the polynomial degree $p$ increases the size of these blocks and the number of non-zeros per row, but it does not change the fundamental block-adjacency pattern of the matrix [@problem_id:3377402]. This highly localized coupling is a major advantage for parallel computing.

### Variants and Extensions

The SIPG method is but one member of the broader DG family. Other formulations offer different advantages in terms of computational structure, accuracy, and physical properties.

#### Local Discontinuous Galerkin (LDG) Method

The LDG method approaches the problem by first rewriting the second-order PDE as a first-order system. For $-\nabla \cdot (\kappa \nabla u) = f$, we introduce an auxiliary flux variable $\mathbf{q} = -\kappa \nabla u$, leading to the system:
1.  $\mathbf{q} + \kappa \nabla u = 0$
2.  $-\nabla \cdot \mathbf{q} = f$

The DG method is then applied to this [first-order system](@entry_id:274311). A key advantage of this approach is that it is inherently **locally conservative**. By design, the numerical flux out of any element exactly balances the source term within it, a property that is often desirable in physical simulations. The standard SIPG method, by contrast, does not produce a locally conservative flux without a special post-processing step. While the mixed form of the LDG system is non-symmetric, special choices of [numerical fluxes](@entry_id:752791) can lead to a primal system for $u_h$ that is symmetric and, under specific conditions (uniform mesh, constant $\kappa$, matching penalty parameters), can even be identical to the SIPG system [@problem_id:3377363].

#### Hybridizable Discontinuous Galerkin (HDG) Method

The HDG method offers a significant computational advantage by reducing the size of the globally coupled system. It introduces a new "hybrid" unknown, $\hat{u}_h$, which represents the trace of the solution on the mesh skeleton (the union of all faces). The brilliant insight of HDG is that the unknowns *inside* each element ($u_h$ and the flux $\mathbf{q}_h$) can be solved for entirely in terms of the trace variable $\hat{u}_h$ on the element's boundary. This process, known as **[static condensation](@entry_id:176722)**, allows one to formulate local problems on each element that are independent of each other, given the face data.

The global system is then formed by enforcing flux continuity across interior faces, resulting in a linear system for the hybrid face unknowns $\hat{u}_h$ only. Since the number of face unknowns is significantly smaller than the number of element unknowns (especially for high polynomial degrees $p$), the resulting global system is much smaller than in a standard DG formulation [@problem_id:3377360] [@problem_id:3377374]. For a simplicial mesh in $d$ dimensions, HDG offers a reduction in global unknowns when $p > d$. Furthermore, the resulting global matrix has a better condition number, scaling as $\mathcal{O}(h^{-1})$ compared to the $\mathcal{O}(h^{-2})$ scaling of standard DG methods, making it easier to solve iteratively [@problem_id:3377360].

#### Bassi-Rebay 2 (BR2) Method

The BR2 method is another stabilization technique that, like HDG, avoids explicit penalty terms in the final bilinear form. It achieves this by defining a **[lifting operator](@entry_id:751273)** $\mathbf{r}_F$. This operator takes the jump of a function on a face, $[u_h]$, and "lifts" it to a vector field that lives in the volume of the adjacent elements. The stabilization is then achieved by adding a term like $\sum_F \int_\Omega \kappa \, \mathbf{r}_F([u_h]) \cdot \mathbf{r}_F([v_h]) \, d\mathbf{x}$ to the bilinear form. This volume integral can be shown to be equivalent to a face-based penalty on the jump, but its formulation entirely in terms of element-based quantities can be computationally advantageous in some contexts [@problem_id:3377371].

In summary, the principles of Discontinuous Galerkin methods are built upon a rigorous mathematical foundation that extends weak formulations to discontinuous spaces. The mechanisms of jumps, averages, and [numerical fluxes](@entry_id:752791) provide the tools to couple elements, while penalty or stabilization terms ensure the overall stability and convergence of the scheme. The rich variety of methods within the DG family, from SIPG to LDG and HDG, offers a versatile and powerful toolkit for solving complex scientific and engineering problems.