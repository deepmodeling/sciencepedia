## Introduction
In the field of [computational geomechanics](@entry_id:747617), accurately modeling the complex behavior of geological materials presents a persistent challenge. Traditional numerical techniques, such as the standard Finite Element Method, often struggle with the intricate geometries of rock masses, the presence of faults and fractures, and the extreme variations in material properties. This creates a critical knowledge gap, demanding more flexible and robust simulation tools. The Discontinuous Galerkin (DG) and Virtual Element Methods (VEM) have emerged as powerful answers to this call, offering a paradigm shift in how we approach [discretization](@entry_id:145012) for geomechanical problems.

This article provides a comprehensive exploration of these two state-of-the-art numerical methods. Across three chapters, you will gain a deep understanding of their theoretical underpinnings and practical utility. The first chapter, **Principles and Mechanisms**, will dissect the core ideas that grant DG and VEM their flexibility, moving from the concept of broken function spaces to the design of [numerical fluxes](@entry_id:752791) and virtual element projectors. Subsequently, the **Applications and Interdisciplinary Connections** chapter will showcase how these principles are applied to solve advanced problems, including [material failure](@entry_id:160997), multi-physics coupling in fractured media, and [wave propagation](@entry_id:144063). Finally, **Hands-On Practices** will offer practical exercises to solidify your understanding of key implementation concepts. We begin by examining the foundational principles that set DG and VEM apart from their classical counterparts.

## Principles and Mechanisms

The theoretical and practical power of Discontinuous Galerkin (DG) and Virtual Element Methods (VEM) stems from a deliberate departure from the strict conformity requirements of traditional Finite Element Methods. By relaxing the insistence on global continuity of the approximation space, these methods gain immense flexibility in handling complex geometries, [material discontinuities](@entry_id:751728), and a wider range of physical phenomena. This chapter delves into the fundamental principles and core mechanisms that enable this flexibility, exploring how continuity is replaced by a system of weak coupling, how stability is maintained, and how these methods are tailored to specific and challenging problems in [computational geomechanics](@entry_id:747617).

### The Foundational Shift: Broken Function Spaces

Standard conforming [finite element methods](@entry_id:749389) construct approximation spaces as subspaces of global Sobolev spaces, such as $H^1(\Omega)$, which enforce continuity across element boundaries by definition. This framework, while powerful, becomes restrictive when dealing with domains containing faults, fractures, or [material interfaces](@entry_id:751731) where physical fields like displacement are naturally discontinuous. DG and VEM begin by embracing this possibility, building their approximation spaces from functions that are defined on an element-by-element basis. This necessitates the concept of a **[broken function space](@entry_id:746988)**.

Let $\Omega$ be a domain in $\mathbb{R}^d$ and let $\mathcal{T}_h$ be a tessellation (or mesh) of $\Omega$ into non-overlapping elements $K$. The cornerstone of discontinuous methods is the **broken Sobolev space**, denoted $H^1(\mathcal{T}_h)$. This space is formally defined as the set of all square-integrable functions on $\Omega$ whose restriction to each element $K \in \mathcal{T}_h$ belongs to the standard Sobolev space $H^1(K)$. That is:
$$
H^1(\mathcal{T}_h) = \{ v \in L^2(\Omega) \mid \forall K \in \mathcal{T}_h, v|_K \in H^1(K) \}
$$
This space is equipped with a norm that sums the contributions from each element:
$$
\|v\|_{H^1(\mathcal{T}_h)}^2 = \sum_{K \in \mathcal{T}_h} \|v\|_{H^1(K)}^2 = \sum_{K \in \mathcal{T}_h} \left( \|v\|_{L^2(K)}^2 + \|\nabla(v|_K)\|_{L^2(K)}^2 \right)
$$

The crucial distinction between $H^1(\mathcal{T}_h)$ and the standard $H^1(\Omega)$ lies in the behavior of the gradient. Recall that for a function $v$ to be in $H^1(\Omega)$, its weak (or distributional) gradient must be a square-[integrable function](@entry_id:146566) over the entire domain $\Omega$. If a function $v \in H^1(\mathcal{T}_h)$ has a jump discontinuity across an interface between two elements, its distributional gradient contains a singular part. Specifically, the [distributional derivative](@entry_id:271061) of $v$ can be shown to be the sum of the element-wise gradient (often called the broken gradient, $\nabla_h v$) and a series of Dirac delta distributions supported on the interfaces, weighted by the magnitude of the jumps. This singular component is not an $L^2(\Omega)$ function, and therefore, such a [discontinuous function](@entry_id:143848) $v$ is not in $H^1(\Omega)$ [@problem_id:3518357].

In essence, $H^1(\Omega)$ is a proper subspace of $H^1(\mathcal{T}_h)$ containing only those functions in $H^1(\mathcal{T}_h)$ that happen to be continuous across all inter-element boundaries. By moving to the larger space $H^1(\mathcal{T}_h)$, we gain the ability to represent discontinuities directly, but we lose the inherent coupling between elements. The central challenge of discontinuous methods, therefore, is to devise a new mechanism to connect the discrete solution across element boundaries.

### The Discontinuous Galerkin Method: A Framework for Weak Coupling

The Discontinuous Galerkin method provides a systematic framework for coupling element-wise approximations. It achieves this by replacing the strong enforcement of continuity with a weak enforcement mediated by **[numerical fluxes](@entry_id:752791)** at the element interfaces.

Let us consider a model elliptic problem, such as [steady-state diffusion](@entry_id:154663) or [linear elasticity](@entry_id:166983). Starting with the governing partial differential equation on an element $K$, multiplying by a test function $v_h$ from a discrete space, and integrating by parts (applying Green's first identity) yields:
$$
\int_K \boldsymbol{\sigma}(u_h) : \boldsymbol{\varepsilon}(v_h) \, dx - \int_{\partial K} (\boldsymbol{\sigma}(u_h)\mathbf{n}_K) \cdot v_h \, ds = \int_K \mathbf{f} \cdot v_h \, dx
$$
where $\boldsymbol{\sigma}(u_h)$ is the flux tensor (e.g., stress in elasticity, $-\kappa\nabla u_h$ in diffusion), $\mathbf{f}$ is a [source term](@entry_id:269111), and $\mathbf{n}_K$ is the outward unit normal to the boundary $\partial K$. When we sum this equation over all elements $K \in \mathcal{T}_h$, the boundary integrals on interior faces do not cancel as they would in a conforming formulation. Instead, for each interior face $F$ shared by elements $K^+$ and $K^-$, we have two contributions, one from each side. The flux $\boldsymbol{\sigma}(u_h)\mathbf{n}_K$ is double-valued on $F$, and a rule must be established to define a unique, single-valued numerical flux, denoted $\widehat{\boldsymbol{\sigma}\mathbf{n}}$, to replace it.

#### Jump and Average Operators

The construction of numerical fluxes is elegantly handled using **jump** and **average** operators. Let $F$ be an interior face between elements $K^+$ and $K^-$, and let $\mathbf{n}^+$ and $\mathbf{n}^-$ be the outward unit normals from each element on $F$. By convention, we fix a single normal for the face, $\mathbf{n}_F = \mathbf{n}^+$, so that $\mathbf{n}^- = -\mathbf{n}_F$. For a scalar field $p$ with traces $p^+$ and $p^-$ on $F$, and a vector field $\mathbf{v}$ with traces $\mathbf{v}^+$ and $\mathbf{v}^-$, a common and consistent set of definitions is as follows [@problem_id:3518367]:

- **Average of a scalar:** A scalar. $\\{\!\\{p\\}\!\\} := \frac{1}{2}(p^+ + p^-)$.
- **Jump of a scalar:** A vector. $[\\![p]\\!] := p^+\mathbf{n}^+ + p^-\mathbf{n}^- = (p^+ - p^-)\mathbf{n}_F$.

- **Average of a vector:** A vector. $\\{\!\\{\mathbf{v}\\}\!\\} := \frac{1}{2}(\mathbf{v}^+ + \mathbf{v}^-)$.
- **Jump of a vector:** A second-order tensor. $[\\![\mathbf{v}]\\!] := \mathbf{v}^+ \otimes \mathbf{n}^+ + \mathbf{v}^- \otimes \mathbf{n}^- = (\mathbf{v}^+ - \mathbf{v}^-)\otimes \mathbf{n}_F$.

- **Average of a tensor:** A tensor. $\\{\!\\{\boldsymbol{\tau}\\}\!\\} := \frac{1}{2}(\boldsymbol{\tau}^+ + \boldsymbol{\tau}^-)$.
- **Jump of a tensor:** A vector. $[\\![\boldsymbol{\tau}]\\!] := \boldsymbol{\tau}^+\mathbf{n}^+ + \boldsymbol{\tau}^-\mathbf{n}^- = (\boldsymbol{\tau}^+ - \boldsymbol{\tau}^-)\mathbf{n}_F$.

These definitions are tensorial in nature, with the [jump operator](@entry_id:155707) typically increasing the tensorial order by one. They provide the fundamental vocabulary for designing DG formulations.

#### The Symmetric Interior Penalty Galerkin (SIPG) Method

One of the most widely used DG formulations for elliptic problems is the **Symmetric Interior Penalty Galerkin (SIPG)** method. It provides a blueprint for constructing the numerical flux to ensure both consistency with the original PDE and stability of the resulting discrete system. The SIPG [bilinear form](@entry_id:140194) is composed of three types of terms:

1.  **The Standard Galerkin Term:** This is the sum of the element-wise integrals of the fluxes, $\sum_K \int_K \boldsymbol{\sigma}(u_h) : \boldsymbol{\varepsilon}(v_h) \, dx$. This term arises naturally from the weak formulation on each element.

2.  **Consistency and Symmetry Terms:** These terms approximate the flux exchange across interfaces. For consistency, the [numerical flux](@entry_id:145174) should approximate the true physical flux. This is achieved by using the average of the flux, e.g., $\\{\!\\{\boldsymbol{\sigma}(u_h)\\}\!\\}$. To ensure the final bilinear form is symmetric, which is desirable for defining a potential energy and for using efficient symmetric solvers, terms involving both trial and [test functions](@entry_id:166589) are included. A typical symmetric formulation involves terms like $-\int_F \big(\\{\!\\{\boldsymbol{\sigma}(u_h)\\}\!\} : [\\![v_h]\\!] + \\{\!\\{\boldsymbol{\sigma}(v_h)\\}\!\} : [\\![u_h]\\!]\big) \, ds$.

3.  **The Penalty (or Stabilization) Term:** This is the key to stability. The terms above are not sufficient to guarantee [coercivity](@entry_id:159399) of the [bilinear form](@entry_id:140194). The method is stabilized by adding a term that penalizes the jump in the primary variable across element faces. This term takes the form $\int_F \eta [\\![u_h]\\!] \cdot [\\![v_h]\\!] \, ds$ for a scalar problem or $\int_F \eta [\\![u_h]\\!] : [\\![v_h]\\!] \, ds$ for a vector problem. Here, $\eta$ is the **penalty parameter**, which must be sufficiently large to ensure coercivity. This term weakly enforces continuity by making jumps energetically costly.

The combination of these terms results in a method that is consistent, stable, and symmetric, forming a robust foundation for solving a wide variety of elliptic problems in [geomechanics](@entry_id:175967) [@problem_id:3518367].

### Adapting the DG Framework: Advanced Applications

The flexibility of the DG framework allows for specialized designs tailored to the physics of the problem at hand. We explore three such adaptations: [upwinding](@entry_id:756372) for hyperbolic transport, robustness for [heterogeneous media](@entry_id:750241), and energy conservation for wave dynamics.

#### Hyperbolic Problems and Upwinding

For advection-dominated transport problems, which are hyperbolic in nature, the symmetric fluxes of SIPG are not appropriate. Information in a hyperbolic system propagates in a specific direction, and the numerical scheme must respect this directionality to be stable. A prime example from [geomechanics](@entry_id:175967) is the saturation equation in immiscible [two-phase flow](@entry_id:153752), which governs the movement of fluid fronts [@problem_id:3518377].

The principle of **[upwinding](@entry_id:756372)** dictates that the numerical flux across an interface should be determined by the state in the "upstream" element. The upstream direction is defined by the sign of the advective velocity normal to the face, $u_n = \mathbf{u} \cdot \mathbf{n}_F$. The upwind numerical flux $F^*$ for a convective term $u_n f(S)$ (where $S$ is a conserved quantity like saturation and $f(S)$ is a fractional flow function) is defined as:

$$
F^* =
\begin{cases}
u_n f(S^-)  \text{if } u_n \ge 0 \quad (\text{flow from } K^- \text{ to } K^+) \\
u_n f(S^+)  \text{if } u_n  0 \quad (\text{flow from } K^+ \text{ to } K^-)
\end{cases}
$$

This logic extends to boundary faces. If flow is directed into the domain ($u_n  0$, an inflow boundary), the flux is determined by the prescribed boundary condition. If flow is directed out of the domain ($u_n \ge 0$, an outflow boundary), the flux is determined by the interior solution trace. This simple but powerful mechanism introduces numerical dissipation that stabilizes the scheme against the non-physical oscillations that would be produced by a central (averaged) flux.

#### Robustness for Highly Heterogeneous Media

Geological media are often characterized by extreme variations in material properties, such as Young's modulus or permeability, with jumps of many orders of magnitude across interfaces. A robust numerical method must maintain its stability and accuracy in the presence of such high contrast. In the SIPG framework, this robustness is critically dependent on the choice of the penalty parameter $\eta$ [@problem_id:3518398].

A naive choice, such as one based on the [arithmetic mean](@entry_id:165355) of the material property $E$ across an interface between elements $K_L$ and $K_R$, can lead to a loss of stability. For instance, the penalty $\eta^{\text{arith}} = \alpha \frac{\frac{1}{2}(E_L + E_R)}{\frac{1}{2}(h_L+h_R)}$ can become dominated by the stiffer material, potentially under-penalizing the jump on the softer side, which can compromise the [coercivity](@entry_id:159399) of the bilinear form.

A much more robust choice is to use the **harmonic average** of the material property:
$$
\eta^{\text{harm}} = \alpha \frac{\frac{2}{1/E_L + 1/E_R}}{\frac{1}{2}(h_L+h_R)}
$$
The harmonic mean is naturally weighted towards the smaller of the two values, ensuring that the penalty scales appropriately with the stiffness of the more compliant material, which typically governs the transmission of flux across the interface. This choice leads to a stability (coercivity) constant that is bounded independently of the contrast ratio $E_R/E_L$, making the method robust for highly heterogeneous problems. The "[stability margin](@entry_id:271953)" can be precisely quantified by solving a [generalized eigenvalue problem](@entry_id:151614), confirming the superior performance of [harmonic averaging](@entry_id:750175) [@problem_id:3518398].

#### Time-Dependent Problems and Energy Conservation

For time-dependent wave propagation problems, such as linear [elastodynamics](@entry_id:175818), it is often desirable for the numerical scheme to conserve a discrete analogue of the [mechanical energy](@entry_id:162989). The DG framework allows for the design of such [conservative schemes](@entry_id:747715). Consider the semi-discrete DG formulation for [elastodynamics](@entry_id:175818), $\rho \ddot{\mathbf{u}}_h - \nabla_h \cdot \boldsymbol{\sigma}_h(\mathbf{u}_h) = \mathbf{0}$, where the element coupling is handled by a [numerical flux](@entry_id:145174). If a non-dissipative flux, such as a central flux, is used, the resulting bilinear form $a_c(\cdot, \cdot)$ is symmetric [@problem_id:3518397].

The semi-discrete [mechanical energy](@entry_id:162989) can be defined as:
$$
E_h(t) = \frac{1}{2} \sum_{K \in \mathcal{T}_h} \int_K \rho |\partial_t \mathbf{u}_h|^2 \, dx + \frac{1}{2} a_c(\mathbf{u}_h(t), \mathbf{u}_h(t))
$$
This consists of a kinetic energy term and a potential energy term defined by the symmetric DG bilinear form. Differentiating with respect to time yields:
$$
\frac{d}{dt} E_h(t) = \sum_{K \in \mathcal{T}_h} \int_K \rho \partial_{tt} \mathbf{u}_h \cdot \partial_t \mathbf{u}_h \, dx + a_c(\mathbf{u}_h, \partial_t \mathbf{u}_h)
$$
The key insight is that the semi-discrete [weak formulation](@entry_id:142897) must hold for any test function $v_h$ in the [discrete space](@entry_id:155685). Since $\partial_t \mathbf{u}_h$ is a valid member of this space, we can choose $v_h = \partial_t \mathbf{u}_h$. Substituting this choice into the weak form gives an expression that is exactly the negative of the right-hand side of the [energy derivative](@entry_id:268961) equation. Thus, in the absence of external forces and with conservative boundary conditions, we find that $\frac{d}{dt} E_h(t) = 0$. This demonstrates that the DG method, when designed with appropriate symmetric fluxes, can exactly conserve a discrete energy, a crucial property for long-time simulations of wave phenomena.

### The Virtual Element Method: A New Paradigm for Polygonal Meshes

While DG methods excel on general meshes, the Virtual Element Method (VEM) offers an alternative, conforming approach that is particularly elegant. The defining feature of VEM is that it operates **without ever explicitly constructing or evaluating the basis functions** inside the polygonal elements. The space is "virtual" in this sense, and all computations are performed using only the degrees of freedom (DoFs) of the functions.

#### The Core Mechanism: Projection and Stabilization

The [computability](@entry_id:276011) of VEM hinges on a two-part strategy: **projection** and **stabilization** [@problem_id:3518393]. For a given local VEM space $\mathbf{V}_h(E)$ on an element $E$, the method does not compute the exact [bilinear form](@entry_id:140194) $a_E(\mathbf{u}_h, \mathbf{v}_h)$, as this would require knowing the functions $\mathbf{u}_h$ and $\mathbf{v}_h$ everywhere. Instead, it computes a discrete approximation, $a_E^h(\mathbf{u}_h, \mathbf{v}_h)$.

1.  **The Polynomial Projector:** The first step is to define a [projection operator](@entry_id:143175), $\Pi_k^\nabla$, that maps any function $\mathbf{v}_h \in \mathbf{V}_h(E)$ to a unique polynomial $\Pi_k^\nabla \mathbf{v}_h$ in the space of vector polynomials of degree at most $k$, $\mathbb{P}_k(E)^d$. This projector is defined implicitly through the relation:
    $$
    a_E(\Pi_k^\nabla \mathbf{v}_h, \mathbf{q}) = a_E(\mathbf{v}_h, \mathbf{q}) \quad \forall \mathbf{q} \in \mathbb{P}_k(E)^d
    $$
    The genius of VEM is that the right-hand side of this equation, $a_E(\mathbf{v}_h, \mathbf{q})$, *is* computable using only the DoFs of $\mathbf{v}_h$. By applying integration by parts, the integral is transformed into a sum of boundary integrals over the edges and a volume integral involving the Laplacian of the polynomial $\mathbf{q}$. The VEM degrees of freedom are specifically designed to be moments of the function (and its derivatives) against polynomials on the boundary and in the interior, allowing these integrals to be computed exactly without knowing $\mathbf{v}_h$ itself.

2.  **The Discrete Bilinear Form:** With the polynomial projection $\Pi_k^\nabla \mathbf{u}_h$ now computable, the first part of the discrete [bilinear form](@entry_id:140194) is defined as $a_E(\Pi_k^\nabla \mathbf{u}_h, \Pi_k^\nabla \mathbf{v}_h)$. This term is fully computable because it is just an integral involving known polynomials. This part ensures **consistency**, meaning the method will be exact for any solution that is a polynomial of degree $k$.

However, this term alone is not stable, as it is zero for any function in the kernel of the projector. Therefore, a **stabilization** term, $S_E$, must be added. The full discrete form is:
$$
a_E^h(\mathbf{u}_h, \mathbf{v}_h) = a_E(\Pi_k^\nabla \mathbf{u}_h, \Pi_k^\nabla \mathbf{v}_h) + S_E((I - \Pi_k^\nabla)\mathbf{u}_h, (I - \Pi_k^\nabla)\mathbf{v}_h)
$$
The [stabilization term](@entry_id:755314) $S_E$ acts on the non-polynomial part of the functions, ensures coercivity of the total form, and must itself be computable solely from the DoFs. A common choice is a simple scaled inner product of the DoF vectors corresponding to the non-polynomial fluctuations.

#### Defining the VEM Space and its Degrees of Freedom

The computability described above is only possible if the discrete space and its DoFs are chosen correctly. A standard conforming VEM space for a scalar diffusion problem, $V_k(E)$, is defined implicitly as the set of functions $v \in H^1(E)$ that satisfy two key conditions [@problem_id:3518392]:
- The trace of $v$ on each edge of the polygon is a one-dimensional polynomial of degree at most $k$.
- The Laplacian of $v$, $\Delta v$, is a polynomial of degree at most $k-2$ inside the element.

This space is then endowed with a set of degrees of freedom sufficient to uniquely identify any function within it and to compute the polynomial projector. For order $k$, these typically include:
- The values of the function at each vertex of the polygon.
- For $k \ge 2$, moments of the function against polynomials of degree up to $k-2$ on each edge.
- For $k \ge 2$, moments of the function against polynomials of degree up to $k-2$ in the element interior.

This careful co-design of the abstract space and its concrete degrees of freedom is the essence of the VEM construction.

#### VEM vs. DG: The Cost of Assembly

A practical advantage often cited for VEM is its "quadrature-free" assembly [@problem_id:3518360]. This does not mean no integrals are computed, but rather that the assembly of the stiffness matrix does not require numerical quadrature of complex, non-polynomial basis functions over the volume of the polygon. The consistency part involves exact integrals of polynomials, which can be pre-computed from geometric moments of the element, and the stabilization is purely algebraic on the DoFs.

In contrast, a standard DG method requires numerical quadrature to evaluate both the [volume integrals](@entry_id:183482) (e.g., $\int_K \boldsymbol{\sigma}(u_h):\boldsymbol{\varepsilon}(v_h) dx$) and the face integrals for the numerical flux. The computational cost per element for DG thus scales with the number of basis functions and the number of quadrature points required in the volume and on the faces. VEM's cost, on the other hand, is dominated by algebraic operations involving the number of DoFs and the size of the [polynomial space](@entry_id:269905). In many practical cases, especially for low-to-moderate polynomial degrees on elements with many sides, VEM can offer a significant computational advantage in the assembly phase compared to DG [@problem_id:3518360].

### Shared Challenges and Advanced Formulations

Despite their different philosophies, DG and VEM face similar challenges and can be adapted in sophisticated ways to address difficult problems in geomechanics.

#### Geometric Constraints on Mesh Elements

The theoretical guarantees of stability and convergence for VEM are not unconditional; they rely on certain assumptions about the geometry of the mesh elements. The primary condition is that each element must be uniformly **star-shaped** with respect to an internal ball. This property is quantified by the **chunkiness parameter**, $\gamma_K = h_K / \rho_K$, where $h_K$ is the element diameter and $\rho_K$ is the radius of the largest such ball. For the method to be robust, this parameter must be uniformly bounded across the entire mesh [@problem_id:3518364].

Highly skewed or distorted elements, such as long and thin polygons, have a large chunkiness parameter. This degradation in shape regularity leads to large constants in the fundamental analytical inequalities (like Poincaré and trace inequalities) upon which the method's stability proofs rely. In practice, this manifests as ill-conditioning of the local matrices used to compute the polynomial projections, leading to a loss of numerical accuracy and potentially compromising the stability of the entire simulation.

#### Volumetric Locking in Near-Incompressible Elasticity

A classic challenge in [computational solid mechanics](@entry_id:169583) is **[volumetric locking](@entry_id:172606)**, which occurs when standard displacement-based finite elements are used to model near-[incompressible materials](@entry_id:175963) (where the Poisson's ratio approaches $0.5$, or Lamé parameter $\lambda \gg \mu$). In this regime, the material must deform with nearly zero volume change, imposing the kinematic constraint $\nabla \cdot \mathbf{u} \approx 0$. For low-order [conforming elements](@entry_id:178102), this constraint is too restrictive for the [discrete space](@entry_id:155685), which lacks enough degrees of freedom to satisfy it non-trivially. This leads to an artificially stiff response where the model "locks" and predicts near-zero displacement [@problem_id:3518423].

Both DG and VEM offer powerful solutions to this problem.
- In **DG methods**, locking can be addressed using [mixed formulations](@entry_id:167436), where pressure is introduced as an [independent variable](@entry_id:146806) to enforce the incompressibility constraint. The stability of such methods then depends on the displacement and pressure approximation spaces satisfying the crucial Ladyzhenskaya–Babuška–Brezzi (LBB) inf-sup condition.
- **VEM** provides a more direct and elegant solution within a purely displacement-based framework. The strategy is to modify the volumetric part of the discrete [bilinear form](@entry_id:140194). Instead of using the full volumetric energy term, one uses a term based on a projection of the divergence onto a lower-order [polynomial space](@entry_id:269905). For example, the term $\int_E \lambda (\nabla \cdot \mathbf{u}_h)(\nabla \cdot \mathbf{v}_h) dx$ is replaced by $\int_E \lambda (\Pi^0(\nabla \cdot \mathbf{u}_h))(\Pi^0(\nabla \cdot \mathbf{v}_h)) dx$, where $\Pi^0$ is the projector onto piecewise constants. This has an effect analogous to the [selective reduced integration](@entry_id:168281) techniques used in traditional FEM, but it is performed in a more rigorous manner that preserves the [polynomial consistency](@entry_id:753572) of the method. This relaxation of the volumetric constraint is sufficient to completely eliminate locking [@problem_id:3518423].

This ability to rationally design and modify the discrete bilinear form at the most fundamental level showcases the profound advantage of modern numerical methods like DG and VEM for tackling the complex, multi-physics problems encountered in [computational geomechanics](@entry_id:747617).