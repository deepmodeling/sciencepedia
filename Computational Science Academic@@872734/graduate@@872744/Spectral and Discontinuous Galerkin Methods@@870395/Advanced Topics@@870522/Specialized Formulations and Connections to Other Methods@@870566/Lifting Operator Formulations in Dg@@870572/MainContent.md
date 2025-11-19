## Introduction
The Discontinuous Galerkin (DG) method is a powerful numerical technique for [solving partial differential equations](@entry_id:136409), but its flexibility hinges on the complex task of designing [numerical fluxes](@entry_id:752791) at element interfaces. Lifting operators offer a systematic and elegant solution to this challenge, providing a unified framework for handling inter-element communication by transforming boundary information into volumetric corrections. This approach not only simplifies theoretical analysis but also unlocks significant computational efficiencies and reveals deep connections between seemingly disparate numerical schemes.

This article provides a comprehensive exploration of [lifting operator](@entry_id:751273) formulations. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, explaining how lifting operators are defined and used to construct stable DG schemes. The second chapter, "Applications and Interdisciplinary Connections," broadens the perspective, showcasing the operator's versatility in complex physics, [high-performance computing](@entry_id:169980), and its role in unifying different stabilization techniques. Finally, the "Hands-On Practices" chapter provides practical exercises to solidify understanding and bridge theory with implementation. By the end of this exploration, the reader will have a robust understanding of lifting operators as a cornerstone of modern DG methods. We begin by examining the fundamental principles that govern their construction and function.

## Principles and Mechanisms

In the Discontinuous Galerkin (DG) framework, the interaction between neighboring elements is mediated entirely through integrals over the faces that separate them. A central challenge and a source of great flexibility in DG methods is the design of these face terms, known as [numerical fluxes](@entry_id:752791). Lifting operators provide a powerful and elegant mechanism for handling these face contributions by systematically converting them into volumetric integrals. This conversion not only offers a unified theoretical perspective, linking various DG formulations, but also leads to practical computational advantages. In this chapter, we will explore the fundamental principles of lifting operators, their role in constructing stable and consistent DG schemes, and their deep connections to other advanced methods like Hybridizable DG (HDG).

### The Lifting Operator: From Faces to Volumes

At its core, a **[lifting operator](@entry_id:751273)** is a mathematical construct that maps a function defined on the boundary of an element (a face) to a function defined over the element's interior (its volume). This operation is formally established through the **Riesz [representation theorem](@entry_id:275118)**, which guarantees that in a Hilbert space, every [continuous linear functional](@entry_id:136289) can be represented as an inner product with a unique element of that space.

Consider a finite-dimensional [polynomial space](@entry_id:269905) $V_h(K)$ on an element $K$, equipped with the standard $L^2(K)$ inner product, denoted $(\cdot, \cdot)_K$. For a given function $g$ defined on the boundary $\partial K$, the mapping $v \mapsto \langle g, v \rangle_{\partial K}$ constitutes a linear functional on $V_h(K)$, where $\langle \cdot, \cdot \rangle_{\partial K}$ is the $L^2$ duality pairing on the boundary. The Riesz [representation theorem](@entry_id:275118) ensures the existence of a unique element in $V_h(K)$, which we call the lifting of $g$, that represents this functional.

Let's formalize this. The **scalar boundary [lifting operator](@entry_id:751273)** $L_{\partial K}: L^2(\partial K) \to V_h(K)$ is defined for any $g \in L^2(\partial K)$ as the unique function $L_{\partial K} g \in V_h(K)$ that satisfies
$$
\big(L_{\partial K} g, v\big)_K = \langle g, v \rangle_{\partial K} \quad \text{for all } v \in V_h(K).
$$
This definition effectively "lifts" the boundary function $g$ into the volume of the element $K$, encoding its information within the polynomial $L_{\partial K} g$. [@problem_id:3396012]

To make this abstract definition concrete, let us compute a [lifting operator](@entry_id:751273) for a simple one-dimensional case. Consider the [reference element](@entry_id:168425) $K = [-1, 1]$ and the space of linear polynomials $V_h = \mathbb{P}_1(K)$, which has a basis $\{1, x\}$. We wish to find the lifting of a function $g$ defined on the face $F=\{1\}$, where $g=1$. Let the lifted function be $L_F(g)(x) = c_0 + c_1 x$. The defining relation is:
$$
\int_{-1}^{1} (c_0 + c_1 x) v(x) \, dx = \int_{\{1\}} 1 \cdot v(s) \, ds = v(1) \quad \text{for all } v \in \mathbb{P}_1(K).
$$
We enforce this for each [basis function](@entry_id:170178).
For $v(x) = 1$:
$$
\int_{-1}^{1} (c_0 + c_1 x) \cdot 1 \, dx = 2c_0 = v(1) = 1 \implies c_0 = \frac{1}{2}.
$$
For $v(x) = x$:
$$
\int_{-1}^{1} (c_0 + c_1 x) \cdot x \, dx = \frac{2}{3}c_1 = v(1) = 1 \implies c_1 = \frac{3}{2}.
$$
Thus, the lifted function is $L_F(g)(x) = \frac{1}{2} + \frac{3}{2}x$. This simple polynomial now carries the information of the boundary data at $x=1$ into the volume. [@problem_id:3395997]

### Vector Liftings and Interior Faces

The concept of lifting can be extended to [vector-valued functions](@entry_id:261164) and is particularly crucial for interior faces, where information is exchanged between two adjacent elements. For an element $K$ with outward unit normal $\boldsymbol{n}_K$ on a face $F$, the **element-wise vector [lifting operator](@entry_id:751273)** $r_F^K: L^2(F) \to [V_h(K)]^d$ is defined for a scalar function $g \in L^2(F)$ by finding $r_F^K g \in [V_h(K)]^d$ such that
$$
(r_F^K g, \boldsymbol{w})_K = \langle g, \boldsymbol{w} \cdot \boldsymbol{n}_K \rangle_F \quad \text{for all } \boldsymbol{w} \in [V_h(K)]^d.
$$
This operator lifts a scalar face function $g$ into a vector-valued polynomial field within the element.

For an interior face $F$ shared by two elements, $F = \partial K^+ \cap \partial K^-$, we define a patch-based [lifting operator](@entry_id:751273) $R_F$ that acts on the union of the elements, $\omega_F = K^+ \cup K^-$. This is done by summing the contributions from each element. We define $R_F g$ piece-wise such that its restriction to each element $K^\pm$ is the corresponding element-wise lifting:
$$
R_F g \big|_{K^\pm} = r_F^{K^\pm} g.
$$
For any test function $\boldsymbol{w}$ on the patch space $[V_h(\omega_F)]^d$, the inner product with the lifted function becomes:
$$
(R_F g, \boldsymbol{w})_{\omega_F} = (r_F^{K^+} g, \boldsymbol{w}|_{K^+})_{K^+} + (r_F^{K^-} g, \boldsymbol{w}|_{K^-})_{K^-} = \langle g, (\boldsymbol{w}|_{K^+}) \cdot \boldsymbol{n}_{K^+} \rangle_F + \langle g, (\boldsymbol{w}|_{K^-}) \cdot \boldsymbol{n}_{K^-} \rangle_F.
$$
Since the normals are outward-pointing from each element, $\boldsymbol{n}_{K^-} = -\boldsymbol{n}_{K^+}$. The expression simplifies to:
$$
(R_F g, \boldsymbol{w})_{\omega_F} = \langle g, (\boldsymbol{w}|_{K^+} - \boldsymbol{w}|_{K^-}) \cdot \boldsymbol{n}_{K^+} \rangle_F = \langle g, [\![\boldsymbol{w}]\!] \cdot \boldsymbol{n}_{K^+} \rangle_F,
$$
where $[\![\boldsymbol{w}]\!] = \boldsymbol{w}|_{K^+} - \boldsymbol{w}|_{K^-}$ is the **jump** of the vector function $\boldsymbol{w}$ across the face $F$. This elegant result shows that the patch lifting of a scalar function $g$ is designed to represent the functional associated with the jump of the vector test function. [@problem_id:3395996]

### The Role of Lifting in DG Formulations

The primary purpose of lifting operators is to transform face integrals into [volume integrals](@entry_id:183482), providing an alternative but equivalent way to express and analyze the coupling terms in DG methods. This equivalence is not merely a notational convenience; it reveals deep structural properties of the [discretization](@entry_id:145012).

A fundamental property is that the sum of lifted face contributions on an element precisely balances the boundary integral terms that arise from integration by parts. Consider a [test vector](@entry_id:172985) $\boldsymbol{\tau}$ and the sum of the lifted jump $\llbracket u_h \rrbracket$ over all faces of an element $K$. By the definition of the [lifting operator](@entry_id:751273) (with an appropriate sign convention), we have:
$$
\sum_{F \subset \partial K} \int_{K} r_{F}(\llbracket u_h \rrbracket) \cdot \boldsymbol{\tau} \, dx = - \sum_{F \subset \partial K} \int_F \llbracket u_h \rrbracket (\boldsymbol{\tau} \cdot \boldsymbol{n}_K) \, ds = - \int_{\partial K} \llbracket u_h \rrbracket (\boldsymbol{\tau} \cdot \boldsymbol{n}_K) \, ds.
$$
This demonstrates that the volumetric term created by the sum of liftings is equal and opposite to the original boundary integral term. [@problem_id:3395988]

This principle is at the heart of many DG formulations. Let's examine two key applications.

#### Symmetric Interior Penalty Galerkin (SIPG) Method

The SIPG method for the Poisson equation is a cornerstone of DG literature. Its [bilinear form](@entry_id:140194) contains element gradient terms, consistency terms, and a penalty term. The consistency terms, which ensure the formulation is correct for smooth solutions, are:
$$
- \sum_{F \in \mathcal{F}_i} \int_F \{\!\!\{\nabla u_h\}\!\!\} \cdot \boldsymbol{n}_F \, [v_h] \, ds - \sum_{F \in \mathcal{F}_i} \int_F \{\!\!\{\nabla v_h\}\!\!\} \cdot \boldsymbol{n}_F \, [u_h] \, ds,
$$
where $\{\!\!\{\cdot\}\!\!\}$ denotes the average. Using an appropriately defined [lifting operator](@entry_id:751273) $R_h$ that lifts face jumps, these face integrals can be re-expressed as [volume integrals](@entry_id:183482). For instance, the first term can be written as $\int_{\Omega} R_h [v_h] \cdot \nabla u_h \, dx$. The entire bilinear form can then be cast into a form where face jump data is seen to provide a volumetric correction to the element-wise gradients. This perspective is invaluable for theoretical analysis, particularly for proving stability. Stability (coercivity) for the SIPG method requires the inclusion of a penalty term that penalizes the jump $[u_h]$, with a [penalty parameter](@entry_id:753318) $\eta_F$ that must be sufficiently large. Theory shows that $\eta_F$ must scale like $C p^2 h_F^{-1}$ to overcome terms arising from inverse inequalities, where $p$ is the polynomial degree and $h_F$ is the face size. [@problem_id:3395987]

#### Weak Imposition of Boundary Conditions

Lifting operators are also instrumental in the weak imposition of boundary conditions, such as in Nitsche's method. In a symmetric Nitsche-type formulation for a diffusion problem, boundary terms like $-\langle \kappa \nabla u_h \cdot \boldsymbol{n}, v_h \rangle_{\partial \Omega}$ and the penalty term $\langle (\eta/h) u_h, v_h \rangle_{\partial \Omega}$ arise. Using the scalar boundary [lifting operator](@entry_id:751273) $L_{\partial K}$, these face integrals can be rewritten as element-wise [volume integrals](@entry_id:183482):
$$
-\big(L_{\partial K}(\kappa \nabla u_h \cdot \boldsymbol{n}), v_h\big)_K \quad \text{and} \quad \big(L_{\partial K}((\eta/h_K)u_h), v_h\big)_K.
$$
This converts all boundary contributions into a standard volumetric form, which can simplify implementation. The stability of the [lifting operator](@entry_id:751273) itself is a key component in the stability analysis of the overall method. It can be shown via inverse trace inequalities that the [operator norm](@entry_id:146227) of $L_{\partial K}$ is bounded, with a characteristic dependence on the mesh size: $\|L_{\partial K} g\|_{0,K} \le C h_K^{-1/2} \|g\|_{0, \partial K}$. [@problem_id:3396012]

### Advanced Formulations and Equivalences

The concept of lifting operators enables the formulation of entire DG schemes and reveals profound connections between seemingly different methods.

#### The Bassi-Rebay 2 (BR2) Method

The **Bassi-Rebay 2 (BR2) method** is a prominent DG scheme where the stabilization is defined directly in terms of lifting operators. The [bilinear form](@entry_id:140194) for the Poisson problem is given by:
$$
a(u_h, v_h) = \sum_{K} \int_{K} \nabla u_h \cdot \nabla v_h \, dx - \sum_{F} \int_{\omega_F} (r_F([u_h]) \cdot \nabla v_h + r_F([v_h]) \cdot \nabla u_h) \, dx + \sum_{F} \eta_F \int_{\omega_F} r_F([u_h]) \cdot r_F([v_h]) \, dx.
$$
Here, the consistency terms are formulated using lifted jumps $r_F([u_h])$ and $r_F([v_h])$, and the penalty term is a volumetric inner product of these same lifted functions. Coercivity of this form requires the [stabilization parameter](@entry_id:755311) $\eta_F$ to be sufficiently large. For certain classes of meshes, such as nonobtuse triangulations, the minimum value for coercivity can be proven to be $\eta_F = 3$. [@problem_id:3396013]

Remarkably, for simple cases, the BR2 stabilization can be shown to be equivalent to the SIPG penalty. For a 1D problem with piecewise constant elements, the BR2 [stabilization term](@entry_id:755314) $\mu \int_K R_F([u]) R_F([v]) dx$ simplifies to $(\mu/2h)[u][v]$. This is directly proportional to the SIPG penalty term $\sigma[u][v]$. By choosing the parameters such that $\sigma = \mu/(2h)$, the two stabilization energies become identical, revealing that BR2 and SIPG are deeply related. [@problem_id:3396032]

#### Connection to Hybridizable DG (HDG)

The relationship extends even further to the family of **Hybridizable Discontinuous Galerkin (HDG) methods**. HDG methods introduce an additional unknown, the numerical trace $\hat{u}_h$, which lives only on the mesh skeleton. The element-interior unknowns $(u_h, \boldsymbol{q}_h)$ are then solved for locally in terms of $\hat{u}_h$. This process, known as **[static condensation](@entry_id:176722)**, can be viewed in two ways. One can eliminate the interior unknowns to get a small global system for $\hat{u}_h$, which is the standard HDG approach.

Alternatively, one can eliminate the hybrid variable $\hat{u}_h$ to obtain a global system purely for the discontinuous interior variables $(u_h, \boldsymbol{q}_h)$. When this is done, the face-based penalty term in the HDG formulation, $\langle \tau(u_h - \hat{u}_h), v_h \rangle_{\partial K}$, is transformed into a volumetric coupling term. This resulting volumetric correction is precisely the lifting of the face residual $u_h - \hat{u}_h$. [@problem_id:3396001] In essence, a primal DG method with lifting-based stabilization can be interpreted as the condensed form of an underlying HDG method. This equivalence can be shown explicitly. For a 1D diffusion problem with linear elements, both the HDG and a primal DG method, after condensation to a single degree of freedom at the interface, yield the identical stiffness coefficient, which for a two-element setup is $2/h$. [@problem_id:3395993]

### Computational Implementation

From a practical standpoint, we must be able to compute the lifted function efficiently. Let's consider the vector lifting $r_F(g)$, which is defined by $(r_F(g), \boldsymbol{w})_K = \langle g, \boldsymbol{w} \cdot \boldsymbol{n}_F \rangle_F$. To find its representation in a basis $\{\boldsymbol{\psi}_j\}_{j=1}^{N_K}$ for $[V_h(K)]^d$, we write $r_F(g) = \sum_j \rho_j \boldsymbol{\psi}_j$. We also expand the face function $g$ in a face basis $\{\phi_q\}$, $g = \sum_q g_q \phi_q$.

By choosing the [test functions](@entry_id:166589) $\boldsymbol{w}$ to be the basis functions $\boldsymbol{\psi}_i$, we obtain a linear system for the coefficient vector $\boldsymbol{\rho}$:
$$
\sum_{j=1}^{N_K} \rho_j (\boldsymbol{\psi}_j, \boldsymbol{\psi}_i)_K = \sum_{q=1}^{N_F} g_q \langle \phi_q, \boldsymbol{\psi}_i \cdot \boldsymbol{n}_F \rangle_F.
$$
This is a matrix system of the form
$$
M_K \boldsymbol{\rho} = C_F^\top \mathbf{g},
$$
where $M_K$ is the element **[mass matrix](@entry_id:177093)** with entries $(M_K)_{ij} = (\boldsymbol{\psi}_i, \boldsymbol{\psi}_j)_K$, and $C_F$ is a **[coupling matrix](@entry_id:191757)** with entries $(C_F)_{qi} = \langle \phi_q, \boldsymbol{\psi}_i \cdot \boldsymbol{n}_F \rangle_F$.

The key to efficiency is that the mass matrix $M_K$ depends only on the element geometry and the chosen basis, not on the specific face $F$. Therefore, its inverse or LU factorization can be pre-computed once per element at a cost of $\mathcal{O}(N_K^3)$. To compute the lifting for any given face function $\mathbf{g}$, one first forms the right-hand side vector $C_F^\top \mathbf{g}$ and then solves the system using the pre-computed factorization. This solve step costs only $\mathcal{O}(N_K^2)$. This makes the application of lifting operators a computationally feasible and efficient part of a DG solver implementation. [@problem_id:3396020]