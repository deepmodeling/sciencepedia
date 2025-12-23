## Introduction
In the numerical solution of partial differential equations, the [finite element method](@entry_id:136884) (FEM) stands as a cornerstone, typically relying on "conforming" approximations where the discrete function space is a subset of the continuous [solution space](@entry_id:200470). This approach guarantees certain theoretical properties, like Galerkin orthogonality, which simplify error analysis. However, constructing these conforming spaces can be intricate and restrictive, particularly for complex problems in fluid dynamics or solid mechanics, presenting a significant challenge for both theory and implementation.

This article introduces the Crouzeix-Raviart (CR) element, a canonical example of a "nonconforming" method that elegantly sidesteps these difficulties by relaxing the strict continuity requirements at element interfaces. By operating in a larger "broken" [function space](@entry_id:136890), the CR element offers simpler construction, improved stability for certain problems, and unique computational advantages. This article provides a graduate-level exploration of this powerful method, guiding you from its fundamental principles to its practical application.

Across three chapters, you will gain a deep understanding of this essential numerical tool. The first chapter, **Principles and Mechanisms**, will lay the theoretical groundwork, defining the broken Sobolev spaces and jump operators necessary to formalize the element and its properties. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the method's power by exploring its use in solving the Stokes equations, modeling linear elasticity, and analyzing [wave propagation](@entry_id:144063). Finally, **Hands-On Practices** will offer a set of targeted problems to solidify your understanding of the element's construction, assembly, and core theoretical properties.

## Principles and Mechanisms

In the [finite element analysis](@entry_id:138109) of partial differential equations, a foundational choice is the finite-dimensional space of functions used to approximate the true solution. A standard requirement for this space, say $V_h$, is that it be a subspace of the [solution space](@entry_id:200470) $V$ of the continuous problem (e.g., $V=H^1_0(\Omega)$). Such methods are termed **conforming [finite element methods](@entry_id:749389)**. This inclusion, $V_h \subset V$, is crucial as it allows any function from the discrete space $V_h$ to be used as a valid test function in the continuous weak formulation, leading to the elegant property of Galerkin orthogonality and straightforward error analysis via Céa's lemma.

However, constructing conforming finite element spaces can be complex, particularly for [higher-order elements](@entry_id:750328) or for certain classes of problems such as the Stokes equations for fluid flow or [plate bending](@entry_id:184758) problems. This motivates the study of **nonconforming [finite element methods](@entry_id:749389)**, where the condition $V_h \subset V$ is deliberately relaxed. While these methods lose the automatic guarantee of Galerkin orthogonality, they can offer benefits such as simpler element construction, fewer degrees of freedom for a given approximation order, and improved stability properties for specific problems. The Crouzeix-Raviart element is the canonical example of this approach. To properly analyze such methods, we must work in a more general setting of **broken Sobolev spaces** .

### Broken Sobolev Spaces and Jump Operators

Let $\Omega \subset \mathbb{R}^d$ be a domain partitioned into a mesh $\mathcal{T}_h$ of non-overlapping elements $K$ (e.g., triangles in 2D or tetrahedra in 3D). A conforming finite element space enforces continuity across the boundaries of these elements, ensuring that any function $v_h \in V_h$ is globally continuous and thus resides in a space like $H^1(\Omega)$.

Nonconforming methods begin by relaxing this constraint. We define the broken Sobolev space $H^1(\mathcal{T}_h)$ as the set of functions that are square-integrable on $\Omega$ and whose restriction to each element $K \in \mathcal{T}_h$ belongs to the standard Sobolev space $H^1(K)$ :
$$
H^1(\mathcal{T}_h) := \{ v \in L^2(\Omega) : v|_K \in H^1(K) \text{ for all } K \in \mathcal{T}_h \}
$$
Functions in $H^1(\mathcal{T}_h)$ may be discontinuous across the interior faces (edges in 2D) of the mesh. To quantify this discontinuity, we introduce the **[jump operator](@entry_id:155707)**. For an interior face $E$ shared by two elements $K^+$ and $K^-$, we define the traces of a function $v \in H^1(\mathcal{T}_h)$ from each side as $v^+ = v|_{K^+}|_E$ and $v^- = v|_{K^-}|_E$. The jump of $v$ across $E$ is then defined as the difference of these traces:
$$
\llbracket v \rrbracket_E := v^+ - v^-
$$
The core idea of nonconforming elements like the Crouzeix-Raviart element is to build a finite element space within $H^1(\mathcal{T}_h)$ that is not a subspace of $H^1(\Omega)$ but enforces a continuity condition that is just strong enough to ensure convergence.

### The Crouzeix-Raviart Element

The Crouzeix-Raviart (CR) element, introduced by Michel Crouzeix and Pierre-Arnaud Raviart in 1973, is the simplest nonconforming element for second-order elliptic problems. Let us first define it precisely in two dimensions on a [triangular mesh](@entry_id:756169) $\mathcal{T}_h$.

#### Definition and Degrees of Freedom

The CR finite element space is built from functions that are linear polynomials on each triangle $K \in \mathcal{T}_h$. A key distinction from the standard conforming $\mathbb{P}_1$ element, whose degrees of freedom (DoFs) are the function values at the vertices, is the choice of DoFs for the CR element. For a triangle $K$, the local CR element is defined by:
1.  **Local function space:** The space of linear (affine) polynomials $\mathbb{P}_1(K)$.
2.  **Degrees of freedom:** The function values at the midpoints of the three edges of $K$.

A linear polynomial in two variables is uniquely determined by its values at three non-collinear points. Since the edge midpoints of a non-degenerate triangle are non-collinear, these DoFs are **unisolvent** for $\mathbb{P}_1(K)$.

The global space $V_h^{\mathrm{CR}}$ is then constructed by "gluing" these local elements together. Continuity is enforced by requiring that for any interior edge $E$, the function value at its midpoint is single-valued, i.e., shared by the functions on the two adjacent triangles  . Homogeneous Dirichlet boundary conditions are imposed weakly by requiring the DoFs on all boundary edges to be zero.

This construction leads to an important observation: continuity is only enforced at a single point on each edge. The function value may jump across the rest of the edge, including at the vertices. This is why, in general, $V_h^{\mathrm{CR}} \not\subset C^0(\Omega)$ and therefore $V_h^{\mathrm{CR}} \not\subset H^1(\Omega)$ .

#### Equivalent Integral Formulation

The definition based on midpoint values has an elegant and powerful equivalent formulation based on edge integrals. For any linear function $p(s)$ on a one-dimensional interval (an edge), its value at the midpoint is equal to its average value over the interval. Thus, for a function $v_h$ that is piecewise linear, the condition of being continuous at the midpoint of an interior edge $E$ is equivalent to the condition that its average value is continuous across $E$:
$$
v_h^+(m_E) = v_h^-(m_E) \quad \iff \quad \frac{1}{|E|} \int_E v_h^+(s) \, \mathrm{d}s = \frac{1}{|E|} \int_E v_h^-(s) \, \mathrm{d}s
$$
where $|E|$ is the length of edge $E$. This, in turn, is equivalent to the condition that the integral of the jump across the edge is zero . This gives us a more general and formal definition of the CR space (with [homogeneous boundary conditions](@entry_id:750371))  :
$$
V_h^{\mathrm{CR}} := \left\{ v_h \in L^2(\Omega) \,\middle|\, 
\begin{aligned}
v_h|_K \in \mathbb{P}_1(K) \quad \forall K \in \mathcal{T}_h, \\
\int_E \llbracket v_h \rrbracket \, \mathrm{d}s = 0 \quad \forall E \in \mathcal{E}_h^{\mathrm{int}}, \\
\int_E v_h \, \mathrm{d}s = 0 \quad \forall E \in \mathcal{E}_h^{\mathrm{bdy}}
\end{aligned}
\right\}
$$
where $\mathcal{E}_h^{\mathrm{int}}$ and $\mathcal{E}_h^{\mathrm{bdy}}$ are the sets of interior and boundary edges, respectively.

### Basis Functions and Interpolation

To better understand the structure of the CR element, it is instructive to construct its basis functions.

#### Local Basis Functions

Consider a single triangle $T$ with vertices $\boldsymbol{x}_1, \boldsymbol{x}_2, \boldsymbol{x}_3$ and [barycentric coordinates](@entry_id:155488) $\lambda_1, \lambda_2, \lambda_3$. Let $e_i$ be the edge opposite to vertex $\boldsymbol{x}_i$. The [local basis](@entry_id:151573) functions $\{\varphi_1, \varphi_2, \varphi_3\} \subset \mathbb{P}_1(T)$ are defined by the duality condition that the average of $\varphi_i$ over edge $e_j$ is $\delta_{ij}$. As shown in , these basis functions have a remarkably simple form in terms of [barycentric coordinates](@entry_id:155488):
$$
\varphi_i = 1 - 2\lambda_i, \quad \text{for } i=1,2,3.
$$
For example, for $\varphi_1$, we check its average value on edge $e_1$. On $e_1$, $\lambda_1 = 0$, so $\varphi_1 = 1$. Its average is 1. On edge $e_2$, $\lambda_3=0$, so $\varphi_1 = 1 - 2\lambda_1$. Since $\lambda_1$ varies linearly from $1$ to $0$ along $e_2$, the average of $\varphi_1$ is $1 - 2 \times \text{avg}(\lambda_1) = 1 - 2 \times \frac{1+0}{2} = 0$. The same holds for $e_3$. These functions form a basis for $\mathbb{P}_1(T)$. A concrete calculation of [stiffness matrix](@entry_id:178659) entries, such as in , relies on the gradients of these basis functions, for instance, $\nabla \varphi_i = -2 \nabla \lambda_i$.

#### Global Basis and Dimension of the Space

The global basis for $V_h^{\mathrm{CR}}$ is constructed from these local representations. For each interior edge $E_j \in \mathcal{E}_h^{\mathrm{int}}$, there is a corresponding global basis function $\phi_j \in V_h^{\mathrm{CR}}$ whose average value over $E_j$ is 1 and whose average value over all other edges is 0. A crucial property of this basis function $\phi_j$ is its local support. As demonstrated in , the support of $\phi_j$ is confined to the two triangles that share the edge $E_j$.

Since there is one basis function for each interior edge (as the DoFs on boundary edges are set to zero), the dimension of the CR space is simply the number of interior edges in the mesh :
$$
\dim(V_h^{\mathrm{CR}}) = |\mathcal{E}_h^{\mathrm{int}}|
$$

#### The Crouzeix-Raviart Interpolant

The basis allows us to define an interpolation operator $\mathcal{I}_{\mathrm{CR}}: H^2(T) \to \mathbb{P}_1(T)$ which maps a function $u$ to the unique linear polynomial whose edge-mean values match those of $u$. A vital property of this operator is that it is **exact for linear polynomials**; that is, if $p \in \mathbb{P}_1(T)$, then $\mathcal{I}_{\mathrm{CR}}p = p$. This can be proven by showing that the error $p - \mathcal{I}_{\mathrm{CR}}p$ is a linear polynomial whose average over every edge is zero, which implies it must be the zero polynomial . This exactness property is fundamental to the [error analysis](@entry_id:142477) of the method and is a key part of what makes the element work despite its nonconformity. Error estimates for this interpolant, such as $\|u - \mathcal{I}_{\mathrm{CR}}u\|_{1,T} \le C_T |u|_{2,T}$, are central to the finite element theory, and the sharp constant $C_T$ can even be computed explicitly on a reference element .

### Galerkin Method and the Consistency Error

When we apply a nonconforming element to solve a PDE like the Poisson equation, $-\Delta u = f$, we encounter a new theoretical challenge. The standard conforming Galerkin method seeks a solution $u_h \in V_h \subset H^1_0(\Omega)$ such that $a(u_h, v_h) = \ell(v_h)$ for all $v_h \in V_h$. Since $V_h \subset H^1_0(\Omega)$, we can subtract this from the continuous weak form $a(u, v_h) = \ell(v_h)$ to obtain the Galerkin orthogonality relation $a(u - u_h, v_h) = 0$.

This argument breaks down for a nonconforming method. The [discrete space](@entry_id:155685) $V_h^{\mathrm{CR}}$ is not a subspace of $H^1_0(\Omega)$, so a function $v_h \in V_h^{\mathrm{CR}}$ is not a valid [test function](@entry_id:178872) for the continuous problem. The bilinear form must be redefined over the broken space, typically as a sum of element-wise integrals:
$$
a_h(w_h, v_h) := \sum_{K \in \mathcal{T}_h} \int_K \nabla w_h \cdot \nabla v_h \, \mathrm{d}x
$$
The CR Galerkin method then seeks $u_h \in V_h^{\mathrm{CR}}$ such that $a_h(u_h, v_h) = \int_\Omega f v_h \, \mathrm{d}x$ for all $v_h \in V_h^{\mathrm{CR}}$. To analyze the error $u - u_h$, we examine the term $a_h(u - u_h, v_h) = a_h(u, v_h) - a_h(u_h, v_h) = a_h(u, v_h) - \int_\Omega f v_h \, \mathrm{d}x$.

By applying integration by parts element-wise to $a_h(u, v_h)$ and using the fact that $-\Delta u = f$, we find that Galerkin orthogonality does not hold. Instead, we obtain the fundamental identity for the nonconforming error :
$$
a_h(u - u_h, v_h) = \sum_{E \in \mathcal{E}_h} \int_E (\nabla u \cdot \mathbf{n}_E) \llbracket v_h \rrbracket \, \mathrm{d}s \quad \text{for all } v_h \in V_h^{\mathrm{CR}}
$$
The right-hand side is the **[consistency error](@entry_id:747725)**. It represents the extent to which the exact solution $u$ fails to satisfy the discrete equations. For a [conforming method](@entry_id:165982), the jump $\llbracket v_h \rrbracket$ would be identically zero and we would recover Galerkin orthogonality.

For the Crouzeix-Raviart method, this [consistency error](@entry_id:747725) term does not vanish in general. However, it can be bounded and shown to converge to zero as the mesh size $h \to 0$. This is the foundation of **Strang's Lemma**, which provides the framework for proving convergence of nonconforming methods. The key property of the CR space, $\int_E \llbracket v_h \rrbracket \mathrm{d}s = 0$, ensures that the method passes the **patch test**: if the solution $u$ is a linear polynomial, then its gradient $\nabla u$ is a constant vector. The flux term $\nabla u \cdot \mathbf{n}_E$ is constant on each edge $E$. The [consistency error](@entry_id:747725) on that edge becomes $(\nabla u \cdot \mathbf{n}_E) \int_E \llbracket v_h \rrbracket \mathrm{d}s = 0$. Thus, the method is exact for linear solutions, a crucial property for convergence.

### Extensions and Advanced Perspectives

#### Connection to Discontinuous Galerkin (DG) Methods

The [consistency error](@entry_id:747725) can be viewed as a defect of the simple nonconforming formulation. Discontinuous Galerkin (DG) methods provide a systematic way to remedy this. By modifying the [bilinear form](@entry_id:140194) to include terms that explicitly penalize the jumps and enforce the flux conditions weakly, one can formulate a method that is consistent by construction. For instance, the Symmetric Interior Penalty Galerkin (SIPG) method uses a form $a_h(\cdot, \cdot)$ that includes terms like $\int_E \{\!\{\nabla w \cdot \mathbf{n}\}\!\} [z] \mathrm{d}s$ and penalty terms $\int_E [w][z] \mathrm{d}s$ . Such a formulation leads to true Galerkin orthogonality $a_h(u-u_h, v_h) = 0$ (under suitable regularity assumptions) and a corresponding [best-approximation property](@entry_id:166240) in a mesh-dependent [energy norm](@entry_id:274966). The Crouzeix-Raviart method can thus be seen as a precursor to modern DG methods.

#### Extension to Three Dimensions

The principles defining the Crouzeix-Raviart element extend naturally to higher dimensions. In three dimensions, the mesh $\mathcal{T}_h$ consists of tetrahedra. The local [function space](@entry_id:136890) is again $\mathbb{P}_1(T)$. A linear polynomial on a tetrahedron is uniquely defined by 4 degrees of freedom. The CR element associates these DoFs with the 4 faces of the tetrahedron .

The degrees of freedom are the average values of the function over each face, or equivalently, the function values at the [barycenter](@entry_id:170655) of each face. The continuity condition becomes a requirement that the integral of the jump vanishes over each interior face, $\int_F \llbracket v_h \rrbracket \mathrm{d}S = 0$. This ensures that the element passes the 3D patch test and provides a robust and effective nonconforming element for three-dimensional problems.