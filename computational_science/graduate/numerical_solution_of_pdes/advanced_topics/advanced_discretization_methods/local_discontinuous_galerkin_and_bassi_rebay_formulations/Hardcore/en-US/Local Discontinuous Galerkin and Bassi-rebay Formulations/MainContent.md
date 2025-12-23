## Introduction
The accurate numerical solution of [partial differential equations](@entry_id:143134) (PDEs) is a cornerstone of modern science and engineering. Among the most powerful and flexible techniques developed in recent decades are discontinuous Galerkin (DG) methods. By relaxing the strict continuity requirements of traditional [finite element methods](@entry_id:749389), DG formulations offer superior performance for problems involving complex geometries, [high-order accuracy](@entry_id:163460), and transport-dominated physics. This article focuses on two prominent and closely related families of DG methods for second-order problems: the Local Discontinuous Galerkin (LDG) and the Bassi-Rebay (BR) formulations.

These methods address the fundamental challenge of discretizing second-order operators, such as diffusion, in a manner that is both stable and locally conservative, even when the solution itself is discontinuous. By rewriting the problem as a [first-order system](@entry_id:274311) or by reconstructing gradients from discontinuous data, they provide a robust framework for tackling a wide array of physical phenomena. Across the following chapters, you will gain a comprehensive understanding of the theory, application, and practical implementation of these advanced numerical schemes.

The journey begins in **Principles and Mechanisms**, where we will build the LDG and BR methods from first principles. We will explore the critical concepts of numerical fluxes, jump and average operators, and the two main philosophies of stabilization: direct jump penalization and [gradient reconstruction](@entry_id:749996) via lifting operators. In **Applications and Interdisciplinary Connections**, we will demonstrate the remarkable versatility of these methods by applying them to challenging problems in continuum mechanics, computational fluid dynamics, and multi-scale physics, uncovering surprising connections to [kinetic theory](@entry_id:136901) and even graph-based data science. Finally, the **Hands-On Practices** section provides concrete computational exercises to compare the numerical properties of these formulations and solidify your understanding.

## Principles and Mechanisms

This chapter delves into the fundamental principles and operational mechanisms of discontinuous Galerkin (DG) methods for second-order elliptic problems, with a particular focus on the Local Discontinuous Galerkin (LDG) and Bassi-Rebay formulations. We will build these methods from first principles, exploring the critical roles of [numerical fluxes](@entry_id:752791), stabilization, and lifting operators. The discussion will elucidate the theoretical underpinnings of these methods and examine their practical implications for accuracy, computational cost, and solver design.

### The Discontinuous Galerkin Framework for Diffusion

Let us consider a model scalar diffusion problem on a bounded domain $\Omega \subset \mathbb{R}^d$:
$$
- \nabla \cdot (\kappa \nabla u) = f \quad \text{in } \Omega,
$$
subject to appropriate boundary conditions. Here, $u$ is the unknown scalar field (e.g., temperature or pressure), $\kappa$ is the [diffusion tensor](@entry_id:748421) (e.g., thermal conductivity), and $f$ is a [source term](@entry_id:269111). The core idea of DG methods is to seek an approximate solution $u_h$ in a finite element space $V_h$ of functions that are polynomials on each element $K$ of a mesh $\mathcal{T}_h$, but are not required to be continuous across element boundaries.

To derive the formulation, we multiply the PDE by a [test function](@entry_id:178872) $v_h \in V_h$ and integrate over a single element $K$:
$$
- \int_K (\nabla \cdot (\kappa \nabla u_h)) v_h \, d\mathbf{x} = \int_K f v_h \, d\mathbf{x}.
$$

Applying Green's first identity (integration by parts) to the left-hand side allows us to transfer a derivative from the [trial function](@entry_id:173682) $u_h$ to the test function $v_h$:
$$
\int_K \kappa \nabla u_h \cdot \nabla v_h \, d\mathbf{x} - \int_{\partial K} v_h (\kappa \nabla u_h \cdot \mathbf{n}_K) \, dS = \int_K f v_h \, d\mathbf{x},
$$
where $\mathbf{n}_K$ is the outward unit normal to the boundary $\partial K$.

A crucial difficulty arises at this point. Because $u_h$ is discontinuous across element interfaces, its gradient $\nabla u_h$ is not well-defined on $\partial K$. The term $\kappa \nabla u_h \cdot \mathbf{n}_K$ represents a physical flux, but it is ambiguous at the interface between two elements. DG methods resolve this ambiguity by replacing the physical flux with a **[numerical flux](@entry_id:145174)**, denoted $\widehat{\mathbf{q}}_h \cdot \mathbf{n}_K$. The [numerical flux](@entry_id:145174) is a function defined on the faces of the mesh that depends on the (discontinuous) values of $u_h$ from the elements sharing the face. Summing the element-wise equation over all elements $K \in \mathcal{T}_h$ yields the global DG weak formulation: find $u_h \in V_h$ such that for all $v_h \in V_h$,
$$
\sum_{K \in \mathcal{T}_h} \int_K \kappa \nabla u_h \cdot \nabla v_h \, d\mathbf{x} - \sum_{K \in \mathcal{T}_h} \int_{\partial K} v_h (\widehat{\mathbf{q}}_h \cdot \mathbf{n}_K) \, dS = \int_\Omega f v_h \, d\mathbf{x}.
$$

To systematically define the numerical flux, we introduce **jump** and **average** operators. For an interior face $F$ shared by elements $K^+$ and $K^-$, with corresponding outward normals $\mathbf{n}^+$ and $\mathbf{n}^-$, we define the jump of a scalar function $w$ and the average of a vector field $\boldsymbol{\xi}$ as:
$$
[[w]] := w^+ \mathbf{n}^+ + w^- \mathbf{n}^- \quad \text{and} \quad \{\!\{\boldsymbol{\xi}\}\!\!\} := \frac{1}{2}(\boldsymbol{\xi}^+ + \boldsymbol{\xi}^-).
$$
With these definitions, the boundary term in the global formulation can be elegantly rewritten as a sum over all faces $\mathcal{F}_h$:
$$
\sum_{F \in \mathcal{F}_h} \int_F \widehat{\mathbf{q}}_h \cdot [[v_h]] \, dS.
$$

#### Fundamental Properties: Consistency and Local Conservation

For a DG method to be a valid approximation of the original PDE, its [numerical flux](@entry_id:145174) must satisfy certain fundamental properties.

First is **consistency**. A [numerical flux](@entry_id:145174) is consistent if, when evaluated with the exact, smooth solution $u$ of the PDE, it reproduces the true physical flux. For the diffusion problem, this means $\widehat{\mathbf{q}}_h(u, \nabla u) = \kappa \nabla u$. Consistency ensures that if the exact solution happens to lie in our finite element space, the method will find it, and it is a prerequisite for convergence as the mesh size $h \to 0$.

Second is **[local conservation](@entry_id:751393)**. A key strength of DG methods is that they are locally (or element-wise) conservative. This property can be seen by choosing a specific test function in the element-wise weak formulation: $v_h = 1$ on a given element $K$ and zero elsewhere. Since $V_h$ contains element-wise polynomials, this is a valid choice provided the polynomial degree $p \ge 0$. With $v_h = 1$, its gradient $\nabla v_h$ is zero. The weak formulation for element $K$ then simplifies dramatically:
$$
\int_K \kappa \nabla u_h \cdot \mathbf{0} \, d\mathbf{x} - \int_{\partial K} 1 \cdot (\widehat{\mathbf{q}}_h \cdot \mathbf{n}_K) \, dS = \int_K f \cdot 1 \, d\mathbf{x},
$$
which rearranges to
$$
- \int_{\partial K} \widehat{\mathbf{q}}_h \cdot \mathbf{n}_K \, dS = \int_K f \, d\mathbf{x}.
$$
This equation is a perfect statement of conservation on element $K$: the net [numerical flux](@entry_id:145174) out of the element's boundary exactly balances the total source within the element. This property, which holds by construction for any DG method of this form, is crucial for accurately capturing problems where local balances are important, such as in fluid dynamics and transport phenomena .

### Stabilized Formulations: The Symmetric Interior Penalty Method

The choice of numerical flux dictates the properties of the resulting DG scheme. A simple and intuitive choice is the **central flux**, where we simply average the fluxes from both sides: $\widehat{\mathbf{q}}_h = \{\!\{\kappa \nabla u_h\}\!\}$. While this choice is consistent, it leads to a numerical scheme that is unstable. The resulting [bilinear form](@entry_id:140194) is not coercive, meaning it cannot control spurious, high-frequency oscillations in the solution.

To remedy this, we must add a **stabilization** term. The **Symmetric Interior Penalty Galerkin (SIPG)** method does this by adding a term that penalizes the jumps in the solution $u_h$ across faces. The SIPG [numerical flux](@entry_id:145174) is defined as:
$$
\widehat{\mathbf{q}}_h\big|_F := \{\!\{\kappa \nabla u_h\}\!\} - \sigma_F [[u_h]].
$$
Here, $\sigma_F$ is a positive penalty parameter. Substituting this flux into the global [weak formulation](@entry_id:142897) and arranging terms symmetrically gives the SIPG [bilinear form](@entry_id:140194) $a_h(u,v)$:
$$
a_h(u,v) := \sum_{K \in \mathcal{T}_h} \int_K \kappa \nabla u \cdot \nabla v \, d\mathbf{x} - \sum_{F \in \mathcal{F}_h} \int_F \left( \{\!\{\kappa \nabla u\}\!\} \cdot [[v]] + \{\!\{\kappa \nabla v\}\!\} \cdot [[u]] \right) \, dS + \sum_{F \in \mathcal{F}_h} \int_F \sigma_F [[u]] \cdot [[v]] \, dS.
$$
The final term is the **penalty term**, which is essential for the stability and [coercivity](@entry_id:159399) of the method.

To understand why, we examine the coercivity requirement: we must show that $a_h(v,v) \ge c |||v|||^2$ for some positive constant $c$ and a suitable norm $|||\cdot|||$. Setting $u=v$ in the bilinear form gives:
$$
a_h(v,v) = \sum_{K} \int_K \kappa |\nabla v|^2 \, d\mathbf{x} - 2\sum_{F} \int_F \{\!\{\kappa \nabla v\}\!\} \cdot [[v]] \, dS + \sum_{F} \int_F \sigma_F |[[v]]|^2 \, dS.
$$
The first and third terms are positive and contribute to a norm. The middle term, however, is not sign-definite and can be negative. We must ensure that this "bad" term can be controlled by the positive terms. Using the Cauchy-Schwarz inequality, we can bound its magnitude:
$$
\left| -2\int_F \{\!\{\kappa \nabla v\}\!\} \cdot [[v]] \right| \le \frac{1}{\delta_F} \|\{\!\{\kappa \nabla v\}\!\}\|_{L^2(F)}^2 + \delta_F \|[[v]]\|_{L^2(F)}^2,
$$
for any $\delta_F > 0$. The crucial step is to relate the face norm of the gradient, $\|\{\!\{\kappa \nabla v\}\!\}\|_{L^2(F)}^2$, back to the volume norm of the gradient, $\|\nabla v\|_{L^2(K)}^2$. This is achieved via a **[trace inequality](@entry_id:756082)**, a standard result in [finite element analysis](@entry_id:138109), which for polynomials of degree $p$ on an element of size $h$ states:
$$
\|\nabla v\|_{L^2(\partial K)}^2 \le C_{tr} \frac{p^2}{h} \|\nabla v\|_{L^2(K)}^2.
$$
A careful application of these inequalities reveals that to absorb the negative term and ensure coercivity, the [penalty parameter](@entry_id:753318) $\sigma_F$ must be sufficiently large. Specifically, it must scale with the mesh size $h_F$ and polynomial degree $p$ as:
$$
\sigma_F \ge C \frac{p^2}{h_F} \kappa_{avg},
$$
where $C$ is a constant depending only on mesh regularity and $\kappa_{avg}$ is a suitable local average of the diffusion coefficient. This scaling demonstrates that a larger penalty is required on smaller elements or for higher polynomial degrees to control the jumps and guarantee stability .

### Formulations Based on Reconstructed Gradients: LDG and Bassi-Rebay

An alternative philosophy to direct jump penalization is to first construct a better, continuous-like approximation of the gradient from the discontinuous solution $u_h$, and then use this reconstructed gradient in a [weak formulation](@entry_id:142897). This is the central idea behind the LDG and Bassi-Rebay (BR) families of methods.

#### The Lifting Operator

The key mechanism for this reconstruction is the **[lifting operator](@entry_id:751273)**. A [lifting operator](@entry_id:751273) maps a function defined only on the faces of the mesh (like the jump $[[u_h]]$) into a vector-valued polynomial field within the element interiors. For a face $F \subset \partial K$, the local [lifting operator](@entry_id:751273) $\mathcal{R}_F^K$ is defined implicitly as the Riesz representer of a face functional: find $\mathcal{R}_F^K(g) \in [\mathbb{P}_p(K)]^d$ such that
$$
\int_K \mathcal{R}_F^K(g) \cdot \boldsymbol{\tau}_h \, d\mathbf{x} = \int_F g (\boldsymbol{\tau}_h \cdot \mathbf{n}_K) \, dS \quad \forall \boldsymbol{\tau}_h \in [\mathbb{P}_p(K)]^d.
$$
This allows us to replace face integrals with [volume integrals](@entry_id:183482). For example, a consistency term like $\int_F \{\!\{\kappa \nabla v\}\!\} \cdot [[u]] \, dS$ can be transformed into a volume integral of the form $\int_K (\kappa \nabla v) \cdot \mathcal{R}_F^K([[u]]) \, d\mathbf{x}$. This transformation is the cornerstone of the following methods .

#### The Local Discontinuous Galerkin (LDG) Method

The LDG method is most naturally introduced as a mixed method for the [first-order system](@entry_id:274311):
$$
\boldsymbol{q} = -\kappa \nabla u, \qquad \nabla \cdot \boldsymbol{q} = f.
$$
We seek approximations $u_h \in V_h$ and $\boldsymbol{q}_h \in \boldsymbol{\Sigma}_h = [\mathbb{P}_p(\mathcal{T}_h)]^d$. Two separate DG equations are formulated, one for each equation in the system, requiring [numerical fluxes](@entry_id:752791) $\widehat{u}_h$ and $\widehat{\boldsymbol{q}}_h$. A common choice is to use **alternating fluxes**: on a face $F$, the flux for one variable is taken from one side (e.g., "upwind"), while the flux for the other variable is taken from the other side. This careful choice of communication between elements leads to a stable and locally [conservative scheme](@entry_id:747714). By algebraically eliminating the auxiliary variable $\boldsymbol{q}_h$, the LDG method can be rewritten as a primal method for $u_h$ alone, where the stabilization is implicitly provided by local lifting operators.

#### The Bassi-Rebay (BR) Family

The Bassi-Rebay methods explicitly define a **reconstructed gradient** $\boldsymbol{G}_h(u_h)$ by correcting the broken (element-wise) gradient $\nabla_h u_h$ with a lifting of the solution jumps:
$$
\boldsymbol{G}_h(u_h) = \nabla_h u_h + \mathcal{R}([[u_h]]).
$$
The properties of the scheme depend critically on the type of [lifting operator](@entry_id:751273) used.

*   **BR1 (Original Bassi-Rebay):** The original method used a *global* [lifting operator](@entry_id:751273), where the lifted field on one element depended on the jumps over the entire mesh. The [numerical flux](@entry_id:145174) was then defined by averaging the reconstructed gradients from adjacent elements: $\widehat{\mathbf{q}}_h = -\{\!\{\kappa \boldsymbol{G}_h(u_h)\}\!\}$. While innovative, this approach has a significant practical drawback. To compute the residual on an element $K$, one needs the reconstructed gradient on its neighbors. But the global nature of the lifting means the neighbor's gradient depends on *its* neighbors, which may not be neighbors of $K$. This creates a non-compact, "two-ring" computational stencil (coupling neighbors-of-neighbors), which is undesirable for performance and implementation complexity .

*   **BR2 (Modern Formulation):** The BR2 method rectifies this by using purely *local* lifting operators, where the lifting on element $K$ depends only on the jumps on its own boundary $\partial K$. This results in a reconstructed gradient $\boldsymbol{G}_h(u_h)|_K$ that depends only on the solution in $K$ and its immediate face-neighbors. The resulting [bilinear form](@entry_id:140194) has a compact, nearest-neighbor stencil, which is much more efficient. A particularly elegant and stable symmetric formulation, the BR2 scheme, can be written entirely in terms of [volume integrals](@entry_id:183482) of these locally reconstructed gradients :
    $$
    a_{BR2}(u,v) = \sum_{K \in \mathcal{T}_h} \int_K \kappa \boldsymbol{G}_h(u)|_K \cdot \boldsymbol{G}_h(v)|_K \, d\mathbf{x}.
    $$
    Expanding this compact form reveals that it implicitly contains the standard volume gradient term, consistency terms, and a [stabilization term](@entry_id:755314) of the form $\int \kappa \mathcal{R}([[u]]) \cdot \mathcal{R}([[v]]) \, d\mathbf{x}$. The [lifting operator](@entry_id:751273) thus provides a powerful mechanism for implementing stabilization entirely through [volume integrals](@entry_id:183482).

### Practical and Advanced Considerations

Beyond the basic formulation, the practical performance of DG methods depends on several factors, from the choice of polynomial basis to the design of efficient linear solvers.

#### Conditioning and Optimal Penalization

The [linear systems](@entry_id:147850) arising from DG methods can be ill-conditioned, especially for high polynomial degrees or fine meshes. The condition number $\kappa(A)$ of the stiffness matrix $A$ directly impacts the convergence of [iterative solvers](@entry_id:136910). For methods like SIPG or BR2, the condition number is dominated by two effects: the penalty term and the element-wise behavior of polynomials.

The largest eigenvalue, $\lambda_{max}$, is governed by polynomial inverse inequalities. These inequalities state that for a polynomial of degree $p$ on an element of size $h$, the norm of its derivative is bounded by its own norm, with a scaling factor of $p^2/h$. This leads to $\lambda_{max} \sim p^4/h^2$. The smallest eigenvalue, $\lambda_{min}$, is governed by a discrete Poincaré-type inequality, which, for a stable method, ensures $\lambda_{min}$ is bounded below by a constant independent of $h$ and $p$.

Combining these results, the condition number scales as $\kappa(A) \approx \lambda_{max} / \lambda_{min} \sim p^4/h^2$. This scaling is achieved when the penalty or [stabilization parameter](@entry_id:755311) is chosen optimally to balance all terms in the [coercivity](@entry_id:159399) analysis, which corresponds to the scaling $\tau \sim p^2/h$ we identified earlier . This provides a rigorous justification for the choice of the [penalty parameter](@entry_id:753318) and a clear picture of how conditioning deteriorates with [mesh refinement](@entry_id:168565) and increasing polynomial order.

#### Choice of Basis and Implementation Costs

The choice of basis functions for the [polynomial space](@entry_id:269905) $\mathbb{P}_p(K)$ has a major impact on implementation cost and [numerical stability](@entry_id:146550), particularly for lifting-based methods like BR2.

*   **Modal Orthonormal Basis:** Using a [basis of polynomials](@entry_id:148579) that are orthogonal with respect to the $L^2$ inner product on the reference element (e.g., integrated Legendre polynomials) is highly advantageous. For affinely mapped elements, the element [mass matrix](@entry_id:177093) becomes a simple scaled identity matrix. Inverting this matrix, which is required to apply the [lifting operator](@entry_id:751273), is trivial. This makes the assembly of lifting operators computationally efficient, with a per-element cost scaling like $O(p^{2d-1})$ for tensor-product elements .

*   **Nodal Lagrange Basis:** Using a basis of Lagrange polynomials defined at a set of nodes (e.g., equispaced or Gauss-Lobatto points) is popular for its simplicity. However, unless special "[mass lumping](@entry_id:175432)" techniques are used, the resulting element mass matrix is dense and can be very ill-conditioned, especially for [equispaced nodes](@entry_id:168260) and high $p$. Applying the [lifting operator](@entry_id:751273) now requires solving a dense linear system on each element. This involves a costly precomputation of the inverse mass matrix ($O(p^{3d})$) and a more expensive application cost per face ($O(p^{2d})$), significantly increasing the overall computational effort and numerical sensitivity .

#### Solver Design for DG Systems

The large, sparse, and often [ill-conditioned linear systems](@entry_id:173639) from DG methods require specialized solvers, such as geometric or [algebraic multigrid](@entry_id:140593) methods. A key component of a [multigrid solver](@entry_id:752282) is the **smoother**, a simple iterative method designed to damp high-frequency error components. The effectiveness of a smoother depends on the coupling structure of the [stiffness matrix](@entry_id:178659).

For SIPG, the inter-element coupling is realized through face integrals. This coupling is relatively weak, and simple **element-block Jacobi smoothers** (which solve for all unknowns on an element simultaneously while lagging information from neighbors) can be effective .

In contrast, for BR2, the lifting-based stabilization creates a much stronger and denser coupling between adjacent elements through [volume integrals](@entry_id:183482) over two-element patches. An element-block smoother fails to address this strong coupling and performs poorly. For BR2, it is crucial to use a smoother that respects this structure, such as a **face-based patch smoother** (e.g., non-overlapping Schwarz). This type of smoother solves small problems on two-element patches simultaneously, thereby implicitly treating the strong inter-element coupling and effectively damping the jump-dominated error modes that are characteristic of BR2 .

#### A Comparative Overview

Different DG methods offer distinct trade-offs. Comparing BR2 and LDG with the **Hybridizable Discontinuous Galerkin (HDG)** method reveals different strengths . HDG introduces an additional unknown on the mesh skeleton (the faces) and uses [static condensation](@entry_id:176722) to produce a smaller global system involving only these face unknowns, a significant advantage for high polynomial degrees ($k \ge 2$). Furthermore, HDG solutions admit a simple element-wise post-processing step that elevates the accuracy from $O(h^{k+1})$ to $O(h^{k+2})$, making it exceptionally efficient for achieving very high accuracy . However, this comes at the cost of a more complex local computation (the [static condensation](@entry_id:176722)), which can be a bottleneck for nonlinear problems where local matrices must be repeatedly re-formed and factorized . In contrast, primal methods like BR2 have a larger global system size for high $k$ but a simpler assembly process, making them attractive in different scenarios.

### Advanced Topic: Structure-Preserving Properties

A growing area of research is the design of numerical methods that preserve important mathematical or physical structures of the underlying PDE. The Helmholtz decomposition theorem states that any sufficiently smooth vector field can be uniquely decomposed into a curl-free (gradient) part and a [divergence-free](@entry_id:190991) part.

When we use a [lifting operator](@entry_id:751273) $\mathcal{R}([[u]])$ to construct a gradient correction, the resulting vector field is not guaranteed to be a pure gradient; it may contain a spurious divergence-free component. This can be viewed as a modeling inconsistency. It is possible to "improve" the [lifting operator](@entry_id:751273) by projecting its output onto the space of discrete gradients. One can define an improved lifting $\widetilde{\mathbf{R}}$ by finding the $L^2$-orthogonal projection of the standard lifting $\mathbf{R}$ onto the space of gradients $\nabla V_h$ . This ensures that the reconstructed gradient is, by construction, a gradient, thereby better preserving the mathematical structure of the problem. This illustrates how the fundamental building blocks of DG methods can be refined to design more robust and structure-preserving schemes.