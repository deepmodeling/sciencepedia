## Introduction
The discontinuous Galerkin (DG) method represents a powerful and flexible class of numerical techniques for [solving partial differential equations](@entry_id:136409) (PDEs), distinguished by its core principle: the use of function spaces composed of polynomials that are allowed to be discontinuous across element boundaries. While traditional conforming [finite element methods](@entry_id:749389) enforce continuity, this constraint can introduce significant complexity when dealing with [advection-dominated problems](@entry_id:746320), complex geometries, or [adaptive mesh refinement](@entry_id:143852). The DG framework overcomes these challenges by embracing discontinuity, shifting the burden of inter-element coupling from rigid nodal connections to a more flexible mechanism of numerical fluxes defined on element interfaces.

This article provides a thorough exploration of this modern numerical methodology. Over the next three chapters, you will gain a deep understanding of the DG method from its theoretical underpinnings to its practical applications. We will begin by examining the foundational **Principles and Mechanisms**, where we define the discontinuous [polynomial spaces](@entry_id:753582) and derive the canonical DG formulations for key model problems. Next, we will explore **Applications and Interdisciplinary Connections**, showcasing the method's versatility in fields ranging from fluid dynamics to data science. Finally, a series of **Hands-On Practices** will offer the opportunity to solidify your comprehension of core computational aspects. We begin our journey by delving into the foundational principles that define the DG space and its unique properties.

## Principles and Mechanisms

This chapter delves into the foundational principles and operational mechanisms of discontinuous Galerkin (DG) [finite element methods](@entry_id:749389). We will formally define the function spaces of discontinuous polynomials, explore the profound consequences of this discontinuity on the algebraic structure of the problem, and detail the construction of DG formulations through the crucial concept of [numerical fluxes](@entry_id:752791).

### Foundations: The Broken Polynomial Space

The cornerstone of the discontinuous Galerkin methodology is its unique choice of finite element space. Unlike traditional conforming [finite element methods](@entry_id:749389) (FEM), which construct globally continuous or more regular [function spaces](@entry_id:143478), DG methods embrace discontinuity. This is achieved by building the approximation space on an element-by-element basis without enforcing any continuity constraints across the boundaries of the elements.

Let $\Omega \subset \mathbb{R}^d$ be a bounded Lipschitz domain, which is partitioned into a mesh $\mathcal{T}_h$ of non-overlapping open elements $K$ (e.g., triangles, quadrilaterals, tetrahedra, or hexahedra). For the stability and convergence theory of DG methods to hold, this mesh is typically assumed to be **shape-regular**. A family of meshes is shape-regular if there exists a constant $C_{\mathrm{sr}} \ge 1$, independent of the characteristic mesh size $h$, such that for every element $K \in \mathcal{T}_h$, the ratio of its diameter $h_K$ to the radius $\rho_K$ of the largest ball that can be inscribed within it is uniformly bounded: $h_K / \rho_K \le C_{\mathrm{sr}}$. This condition prevents elements from becoming arbitrarily thin or stretched as the mesh is refined, which is essential for preserving the quality of the approximation.

On such a mesh, the DG space of discontinuous polynomials, denoted $V_h$, is defined as the set of functions that are square-integrable over the entire domain $\Omega$ and whose restriction to each element $K$ is a polynomial of a specified degree . For a uniform polynomial degree $p$, this is written as:
$$
V_h = \{ v \in L^2(\Omega) : v|_K \in \mathbb{P}_p(K) \ \forall K \in \mathcal{T}_h \}
$$
Here, $\mathbb{P}_p(K)$ represents the space of polynomials on element $K$ with a total degree of at most $p$. On tensor-product elements like quadrilaterals or hexahedra, the local space is often chosen as the tensor-product [polynomial space](@entry_id:269905) $\mathbb{Q}_p(K)$, which consists of polynomials of degree at most $p$ in each coordinate direction.

The critical feature of $V_h$ is that it imposes no matching conditions on the function values at the interfaces between elements. A function $v \in V_h$ is generally discontinuous across these interfaces. This has a profound implication for the regularity of functions in $V_h$. While a polynomial is infinitely differentiable within its element, a function in $V_h$ is generally not in the global Sobolev space $H^1(\Omega)$, because its [weak derivative](@entry_id:138481) is not a well-defined $L^2(\Omega)$ function due to the jumps at interfaces.

To properly analyze functions in $V_h$, we introduce the concept of a **broken Sobolev space**. The broken Sobolev space $H^s(\mathcal{T}_h)$ is the space of functions whose restriction to each element $K$ lies in the standard Sobolev space $H^s(K)$:
$$
H^s(\mathcal{T}_h) = \{ v \in L^2(\Omega) : v|_K \in H^s(K) \ \forall K \in \mathcal{T}_h \}
$$
This space is equipped with a norm that sums the local contributions, for example, $\| v \|_{H^s(\mathcal{T}_h)}^2 = \sum_{K \in \mathcal{T}_h} \| v \|_{H^s(K)}^2$. Since polynomials are infinitely smooth on their domain of definition, any function $v \in V_h$ has the property that its restriction $v|_K$ belongs to $H^s(K)$ for any $s \ge 0$. Consequently, the DG space $V_h$ is a subspace of the broken Sobolev space $H^s(\mathcal{T}_h)$ for any $s \ge 0$ .

### Structural Consequences of Discontinuity

The decision to abandon inter-[element continuity](@entry_id:165046) has far-reaching and often advantageous consequences for the structure of the resulting discrete problem. This departure from conforming methods alters everything from the counting of degrees of freedom to the sparsity pattern of the system matrices .

#### Degrees of Freedom and Space Dimension

In a conforming finite element method, degrees of freedom (DoFs) located on shared vertices, edges, or faces are identified to enforce continuity, thereby coupling adjacent elements. In a DG method, this is not the case. The basis for $V_h$ is constructed as a simple union of local bases defined on each element. Each [basis function](@entry_id:170178) has a support that is strictly confined to a single element $K$.

As a result, the degrees of freedom are entirely local to each element. This means the global DG space $V_h$ is mathematically a [direct sum](@entry_id:156782) of the local [polynomial spaces](@entry_id:753582) on each element:
$$
V_h = \bigoplus_{K \in \mathcal{T}_h} V(K)
$$
where $V(K)$ is the local [polynomial space](@entry_id:269905) (e.g., $\mathbb{P}_p(K)$ or $\mathbb{Q}_p(K)$) on element $K$. The dimension of a [direct sum](@entry_id:156782) is the sum of the dimensions of the constituent spaces. Therefore, the total number of degrees of freedom in a DG method is simply the sum of the local DoFs over all elements in the mesh.

For instance, consider a 2D mesh composed of $N_T$ triangles and $N_Q$ quadrilaterals, with a uniform polynomial degree $p$ . The local space on triangles is $\mathbb{P}_p$, whose dimension is $\dim(\mathbb{P}_p) = \binom{p+2}{2} = \frac{(p+2)(p+1)}{2}$. The local space on quadrilaterals is $\mathbb{Q}_p$, whose dimension is $\dim(\mathbb{Q}_p) = (p+1)^2$. The dimension of the global DG space $V_h$ is therefore:
$$
\dim V_h = N_T \cdot \dim(\mathbb{P}_p) + N_Q \cdot \dim(\mathbb{Q}_p) = N_T \frac{(p+2)(p+1)}{2} + N_Q (p+1)^2
$$
For a mesh with $N_T=58$ triangles, $N_Q=17$ quadrilaterals, and a polynomial degree of $p=4$, the dimension of the space would be $58 \cdot \frac{6 \cdot 5}{2} + 17 \cdot 5^2 = 58 \cdot 15 + 17 \cdot 25 = 870 + 425 = 1295$. This simple summation stands in stark contrast to conforming methods, where the global dimension depends on a complex count of shared vertices, edges, and faces.

#### Matrix Structure

The local nature of the basis functions imparts a special and highly desirable structure to the global matrices that arise in DG discretizations .

The **global mass matrix**, $M$, whose entries are given by $M_{ij} = \int_{\Omega} \phi_i \phi_j \, d\boldsymbol{x}$ for [global basis functions](@entry_id:749917) $\phi_i, \phi_j$, becomes **block-diagonal**. If $\phi_i$ and $\phi_j$ are basis functions associated with different elements, their supports are disjoint, and the integral of their product is zero. Non-zero entries only appear when both basis functions belong to the same element. If we order the degrees of freedom element by element, the mass matrix takes the form:
$$
M = \begin{pmatrix} M_{K_1}  & 0  & \dots  & 0 \\ 0  & M_{K_2}  & \dots  & 0 \\ \vdots  & \vdots  & \ddots  & \vdots \\ 0  & 0  & \dots  & M_{K_N} \end{pmatrix}
$$
where each $M_K$ is the dense local mass matrix for element $K$. This structure is computationally very powerful, especially for time-dependent problems, as the inverse of $M$ is simply the [block-diagonal matrix](@entry_id:145530) of the inverses of the small local matrices $M_K$.

The **global stiffness matrix** (or, more generally, the operator matrix), $A$, arising from the discretization of [differential operators](@entry_id:275037), has a different but equally important structure. The coupling between elements in a DG method is mediated exclusively through integrals over the shared faces. Consequently, an entry $A_{ij}$ of the global operator matrix can be non-zero only if the basis functions $\phi_i$ and $\phi_j$ either belong to the same element or belong to two different elements that share a common face. This results in an **element-block sparse** matrix, where the pattern of non-zero blocks mirrors the adjacency graph of the mesh elements. There are no couplings between elements that share only a vertex or an edge (in 3D), because such connections are of a lower dimension than a face and are not explicitly included in the [variational formulation](@entry_id:166033).

#### Mass Matrix Diagonalization

The block-diagonal nature of the [mass matrix](@entry_id:177093) can be further exploited. For [explicit time-stepping](@entry_id:168157) methods, solving a system with $M$ at each step is required. If $M$ can be made diagonal (a procedure often called **[mass lumping](@entry_id:175432)**), its inversion becomes trivial. This can be achieved through careful choices of local bases and [numerical quadrature](@entry_id:136578) .

One strategy involves constructing a [local basis](@entry_id:151573) that is orthonormal with respect to the $L^2(K)$ inner product. If $\{\phi_i^K\}$ is such a basis, then the exact local [mass matrix](@entry_id:177093) $M^K$, with entries $M^K_{ij} = \int_K \phi_i^K \phi_j^K \, d\boldsymbol{x}$, is the identity matrix $I$. For affine elements (where the element map from a reference element has a constant Jacobian determinant $|J_K|$), one can use a basis $\{\hat{\psi}_i\}$ orthonormal on the reference element $\hat{K}$. The corresponding physical basis on $K$ is not orthonormal, but the local mass matrix becomes a simple scaling of the identity, $M^K = |J_K| I$.

A more direct approach to obtaining a diagonal discrete [mass matrix](@entry_id:177093) is to use a specific combination of a nodal basis and a [quadrature rule](@entry_id:175061). If we choose the [local basis](@entry_id:151573) functions $\{\phi_i^K\}$ to be the Lagrange polynomials associated with the nodes $\{\boldsymbol{x}_j\}$ of a [numerical quadrature](@entry_id:136578) rule, then $\phi_i^K(\boldsymbol{x}_j) = \delta_{ij}$. When the [mass matrix](@entry_id:177093) is assembled using this same [quadrature rule](@entry_id:175061), the resulting discrete [mass matrix](@entry_id:177093) becomes diagonal automatically. This is because the entry $(M_h^K)_{ij} = \sum_m w_m \phi_i^K(\boldsymbol{x}_m) \phi_j^K(\boldsymbol{x}_m)$ is non-zero only if $i=j$. This technique provides a [diagonal mass matrix](@entry_id:173002) regardless of whether the basis is truly orthonormal, at the cost of using a potentially inexact integration scheme.

### Inter-element Communication: Jumps, Averages, and Numerical Fluxes

Since functions in $V_h$ are discontinuous, operators involving derivatives (like the gradient or divergence) cannot be applied in the classical weak sense across the whole domain. The DG method circumvents this by applying integration by parts (the divergence theorem) on each element $K$ individually. This process moves derivatives from the [trial function](@entry_id:173682) $u_h$ to the test function $v_h$ within each element, but it also generates boundary terms on the faces $\partial K$.

It is these face integrals that provide the mechanism for communication between elements. At an interface $F$ between two elements $K^+$ and $K^-$, the solution $u_h$ is two-valued. We must define a **numerical flux**, denoted $\hat{u}$ or $\hat{\boldsymbol{q}}$, which is a single-valued function defined on the face that approximates the true solution or its flux. This numerical flux replaces the ambiguous multi-valued terms in the face integrals and uniquely determines the interaction between the elements.

The construction of numerical fluxes relies on two fundamental operators: the **jump** and the **average** . For an interior face $F = \partial K^+ \cap \partial K^-$, let $\boldsymbol{n}^+$ and $\boldsymbol{n}^-$ be the unit normal vectors pointing outward from $K^+$ and $K^-$, respectively, so $\boldsymbol{n}^- = -\boldsymbol{n}^+$. Let $w^\pm$ be the traces of a scalar function $w$ on $F$ from within $K^\pm$. The vector jump and scalar average are defined as:
$$
[w] := w^+ \boldsymbol{n}^+ + w^- \boldsymbol{n}^- \qquad \{w\} := \frac{w^+ + w^-}{2}
$$
These definitions are constructed to be independent of the arbitrary labeling of elements as $+$ or $-$. For a vector function $\boldsymbol{q}$, the analogous operators are a scalar jump and a vector average:
$$
[\boldsymbol{q}] := \boldsymbol{q}^+ \cdot \boldsymbol{n}^+ + \boldsymbol{q}^- \cdot \boldsymbol{n}^- \qquad \{\boldsymbol{q}\} := \frac{\boldsymbol{q}^+ + \boldsymbol{q}^-}{2}
$$
On boundary faces, these operators are typically defined as $[w] := w \boldsymbol{n}$ and $\{w\} := w$, where $\boldsymbol{n}$ is the outward normal of the domain $\Omega$. These definitions allow for a unified formulation across both interior and boundary faces.

If a function $u$ happens to be continuous across a face $F$, its jump $[u]$ is zero, and its average $\{u\}$ is simply the value of the function on the face. These operators thus provide a precise way to measure and handle the discontinuities inherent in the DG space.

### Canonical Formulations: Advection and Diffusion

The choice of [numerical flux](@entry_id:145174) is problem-dependent and is critical for the stability and accuracy of the resulting scheme. We illustrate this with two canonical examples.

#### Hyperbolic Problems: The Advection Equation

Consider the [linear advection equation](@entry_id:146245) $u_t + \boldsymbol{a} \cdot \nabla u = 0$, where $\boldsymbol{a}$ is a [constant velocity](@entry_id:170682) field. The flux is $\boldsymbol{F} = \boldsymbol{a} u$. A DG scheme for this equation can be built using different [numerical fluxes](@entry_id:752791) for the advective term $\hat{F}_n = \widehat{\boldsymbol{a} u} \cdot \boldsymbol{n}$. Two simple choices are the central flux and the [upwind flux](@entry_id:143931) .

The **central flux** uses the average of the states from both sides: $\hat{F}_n^{\text{cen}} = \{\boldsymbol{a} u\} \cdot \boldsymbol{n} = \boldsymbol{a} \cdot \boldsymbol{n} \{u\}$. While simple and consistent, this flux is known to be unstable for pure advection problems. An energy analysis of a simple DG scheme (piecewise constant polynomials, forward Euler time stepping) reveals that the discrete energy of the system strictly increases at each time step for any non-trivial solution, indicating an unconditional instability.

The **[upwind flux](@entry_id:143931)**, in contrast, introduces numerical dissipation necessary for stability. It selects the state from the "upwind" direction, i.e., the direction from which the flow originates. For a face with normal $\boldsymbol{n}$, the flux is $\hat{F}_n^{\text{up}} = (\boldsymbol{a} \cdot \boldsymbol{n}) u^{\text{up}}$, where $u^{\text{up}}$ is the trace of $u$ from the upstream element. The same energy analysis shows that this scheme is stable provided the time step $\Delta t$ is small enough to satisfy a Courant-Friedrichs-Lewy (CFL) condition, typically of the form $a \Delta t / h \le 1$. The [upwind flux](@entry_id:143931) effectively dissipates energy by penalizing oscillations, leading to a robust scheme.

#### Elliptic Problems: The Diffusion Equation

For a second-order elliptic problem like the Poisson equation, $-\nabla \cdot (\kappa \nabla u) = f$, the DG formulation must correctly handle the [second-order derivative](@entry_id:754598). The **Interior Penalty (IP)** family of methods is a popular choice . The general bilinear form for these methods can be written as:
$$
a_h(u,v) = \sum_{K \in \mathcal{T}_h} \int_K \kappa \nabla u \cdot \nabla v \,d\boldsymbol{x} - \sum_{F \in \mathcal{F}_h} \int_F \Big( \{\kappa \nabla u\} \cdot [v] + \theta \{\kappa \nabla v\} \cdot [u] \Big) \,ds + \sum_{F \in \mathcal{F}_h} \int_F \frac{\sigma_F}{h_F} [u] \cdot [v] \,ds
$$
Here, the first term arises from element-wise integration by parts. The second set of terms are **consistency terms** that ensure the formulation is correct for smooth solutions. The final term is a **penalty term** that penalizes jumps in the solution and is crucial for stability. The parameter $\theta$ distinguishes the three classical variants:

1.  **Symmetric (SIPG), $\theta = 1$:** The resulting bilinear form is symmetric ($a_h(u,v) = a_h(v,u)$). It is coercive and thus stable, but only if the [penalty parameter](@entry_id:753318) $\sigma_F$ is chosen sufficiently large.
2.  **Non-symmetric (NIPG), $\theta = -1$:** The form is non-symmetric. A remarkable property is that the consistency terms cancel out when $u=v$, making the method coercive for any positive penalty parameter $\sigma_F > 0$.
3.  **Incomplete (IIPG), $\theta = 0$:** This non-symmetric variant omits the second consistency term. Like SIPG, it requires a sufficiently large penalty parameter for stability.

The choice between these methods involves a trade-off between the convenience of a symmetric system (SIPG) and the [unconditional stability](@entry_id:145631) with respect to the [penalty parameter](@entry_id:753318) (NIPG).

### Key Advantages and Implementation Details

The principles outlined above give rise to several practical advantages that make DG methods attractive for a wide range of applications.

#### Flexibility: $hp$-Adaptivity and Nonconforming Meshes

One of the most significant advantages of DG is its inherent flexibility in handling complex mesh configurations . Because coupling is handled weakly through face fluxes and no continuity is enforced, DG methods seamlessly accommodate:
-   **Nonconforming meshes with [hanging nodes](@entry_id:750145):** Where a vertex of one element lies in the interior of a face of a neighbor. DG methods require no special treatment or [constraint equations](@entry_id:138140) for such nodes, unlike conforming FEM. The flux formulation naturally applies to the sub-faces created by the [hanging node](@entry_id:750144).
-   **Variable polynomial degree ($p$-adaptivity):** The polynomial degree $p_K$ can be varied from one element to the next without any modifications to the formulation. The [numerical flux](@entry_id:145174) naturally mediates the interaction between a high-degree polynomial on one side and a low-degree polynomial on the other.

This combined `hp`-adaptivity allows for highly efficient and localized refinement, concentrating computational effort where it is most needed. This is particularly powerful for problems with singularities or complex multi-scale features. When using `hp`-refinement, care must be taken in choosing the [penalty parameter](@entry_id:753318) for IP methods. Stability typically requires $\sigma_F$ to scale with the maximum of the local penalty scaling factors, e.g., $\sigma_F \propto \max(p_1^2/h_1, p_2^2/h_2)$ on a face between two elements, to control the jumps from the more challenging side.

#### Implementation: Numerical Quadrature

In practice, the integrals appearing in the DG bilinear form must be evaluated numerically using [quadrature rules](@entry_id:753909). The accuracy of this quadrature is critical for the stability and convergence of the method . To preserve the theoretical properties of the scheme, the [quadrature rules](@entry_id:753909) must be able to exactly integrate the polynomials that appear in the integrands.

By analyzing the polynomial degree of each term in the bilinear form, we can determine the minimum required quadrature order. For the SIPG method on an affine mesh with degree-$p$ polynomials, the analysis is as follows:
-   **Volume term $\int_K \kappa \nabla u_h \cdot \nabla v_h \,d\boldsymbol{x}$:** The integrand has degree at most $(p-1)+(p-1) = 2p-2$. The volume quadrature rule must be exact for polynomials of degree $q_{\text{vol}} = 2p-2$.
-   **Consistency terms $\int_F \{\kappa \nabla u_h\} \cdot [v_h] \,ds$:** The integrand has degree at most $(p-1)+p = 2p-1$.
-   **Penalty term $\int_F \sigma [u_h] \cdot [v_h] \,ds$:** The integrand has degree at most $p+p = 2p$.

The most stringent requirement comes from the penalty term. Therefore, to exactly integrate the entire bilinear form, the face quadrature rule must be exact for polynomials of degree $q_{\text{face}} = 2p$. Using a rule with a lower order (**under-integration**) can compromise the method. For example, failing to exactly integrate the penalty term can reduce the effective [coercivity constant](@entry_id:747450), potentially leading to instability unless the penalty parameter $\sigma_F$ is increased to compensate. It can also introduce aliasing errors that degrade the optimal [order of convergence](@entry_id:146394). Careful selection of [quadrature rules](@entry_id:753909) is therefore a paramount practical consideration in any DG implementation.