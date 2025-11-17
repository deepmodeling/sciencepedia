## Introduction
The analysis of free vibration is a cornerstone of modern engineering, crucial for ensuring the safety, stability, and performance of everything from bridges and aircraft to microscopic devices. At its heart lies a fundamental question: how can we predict the [natural frequencies](@entry_id:174472) and [characteristic modes](@entry_id:747279) of oscillation for a complex structure? The answer is found in the generalized eigenvalue problem, a powerful mathematical formulation that bridges the gap between the continuous physics of a vibrating body and the discrete, computable world of the [finite element method](@entry_id:136884) (FEM). This article provides a comprehensive exploration of this pivotal topic, designed for graduate-level engineers and scientists.

The journey begins in the "Principles and Mechanisms" chapter, where we derive the governing equations from first principles of continuum mechanics, discretize them using FEM to form the [algebraic eigenvalue problem](@entry_id:169099) $K\phi = \lambda M\phi$, and investigate the [critical properties](@entry_id:260687) of the resulting stiffness and mass matrices. We will also confront common numerical pathologies that can arise in practice. The "Applications and Interdisciplinary Connections" chapter then expands our view, showcasing how this single mathematical framework is applied to solve real-world challenges in [structural design](@entry_id:196229), stability analysis, [rotordynamics](@entry_id:163706), and even computational chemistry. Finally, the "Hands-On Practices" section provides an opportunity to solidify this knowledge by working through practical problems that reinforce the core theoretical concepts.

## Principles and Mechanisms

The analysis of free vibration is fundamental to understanding the dynamic behavior of structures and continua. In the [finite element method](@entry_id:136884), this analysis culminates in the formulation and solution of a [generalized eigenvalue problem](@entry_id:151614). This chapter elucidates the principles and mechanisms governing this problem, from its origins in continuum mechanics to the properties of its discrete algebraic representation and the numerical artifacts that can arise in practice.

### From Continuum Mechanics to the Variational Formulation

The starting point for any dynamic analysis of a solid body is the [balance of linear momentum](@entry_id:193575). For a linear elastic continuum occupying a domain $\Omega$ with mass density $\rho$, and in the absence of external body forces, this principle is expressed by Cauchy's [equation of motion](@entry_id:264286):
$$
\nabla \cdot \boldsymbol{\sigma} = \rho \frac{\partial^2 \mathbf{u}}{\partial t^2}
$$
where $\mathbf{u}(\mathbf{x}, t)$ is the [displacement vector field](@entry_id:196067) and $\boldsymbol{\sigma}$ is the Cauchy stress tensor. For small deformations, the stress is related to the strain $\boldsymbol{\varepsilon}$ through the linear [constitutive relation](@entry_id:268485) (Hooke's Law), $\boldsymbol{\sigma} = \boldsymbol{C} : \boldsymbol{\varepsilon}$, where $\boldsymbol{C}$ is the [fourth-order elasticity tensor](@entry_id:188318). The strain itself is kinematically related to the displacement by the [small-strain tensor](@entry_id:754968), $\boldsymbol{\varepsilon}(\mathbf{u}) = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^\top)$.

In free [vibration analysis](@entry_id:169628), we are interested in the [natural modes](@entry_id:277006) of oscillation of the system. These are harmonic motions, which we can express by seeking solutions of the form $\mathbf{u}(\mathbf{x}, t) = \mathbf{u}(\mathbf{x}) e^{\mathrm{i}\omega t}$, where $\mathbf{u}(\mathbf{x})$ is the spatially varying [mode shape](@entry_id:168080) and $\omega$ is the angular frequency of vibration. Substituting this *ansatz* into the [equation of motion](@entry_id:264286) yields a time-independent [partial differential equation](@entry_id:141332):
$$
\nabla \cdot \boldsymbol{\sigma}(\mathbf{u}) + \omega^2 \rho \mathbf{u} = \mathbf{0}
$$

To render this problem suitable for [finite element analysis](@entry_id:138109), we transform it into a weak, or variational, form. Following the Galerkin procedure, we multiply the equation by an arbitrary vector-valued test function $\mathbf{v}$ and integrate over the domain $\Omega$. The [test function](@entry_id:178872) $\mathbf{v}$ is required to belong to a suitable function space that respects the essential (Dirichlet) boundary conditions of the problem. If displacements are prescribed as zero on a portion of the boundary $\Gamma_D$, the [test functions](@entry_id:166589) must also vanish there. Applying the [divergence theorem](@entry_id:145271) to the first term allows us to transfer a derivative from the stress tensor to the [test function](@entry_id:178872), yielding:
$$
\int_{\Omega} \boldsymbol{\sigma}(\mathbf{u}) : \nabla \mathbf{v} \, \mathrm{d}x = \omega^2 \int_{\Omega} \rho \mathbf{u} \cdot \mathbf{v} \, \mathrm{d}x - \int_{\partial\Omega} (\boldsymbol{\sigma}(\mathbf{u}) \cdot \mathbf{n}) \cdot \mathbf{v} \, \mathrm{d}S
$$
The boundary integral vanishes if, on the part of the boundary $\Gamma_N$ where displacements are not prescribed, the natural (Neumann) boundary condition of zero traction ($\boldsymbol{\sigma} \cdot \mathbf{n} = \mathbf{0}$) is applied. The test function $\mathbf{v}$ is already zero on $\Gamma_D$.

Leveraging the symmetry of the stress tensor $\boldsymbol{\sigma}$ and the [elasticity tensor](@entry_id:170728) $\boldsymbol{C}$, the term $\boldsymbol{\sigma}(\mathbf{u}) : \nabla \mathbf{v}$ can be written as $\boldsymbol{\varepsilon}(\mathbf{u}) : \boldsymbol{C} : \boldsymbol{\varepsilon}(\mathbf{v})$. This leads to the weak form of the continuous free vibration eigenproblem [@problem_id:2562501]. Let us define two [bilinear forms](@entry_id:746794): the **stiffness bilinear form** $a(\cdot, \cdot)$, representing the [virtual work](@entry_id:176403) of internal stresses, and the **mass [bilinear form](@entry_id:140194)** $m(\cdot, \cdot)$, representing the [virtual work](@entry_id:176403) of [inertial forces](@entry_id:169104).

$$
a(\mathbf{u}, \mathbf{v}) := \int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{u}) : \boldsymbol{C} : \boldsymbol{\varepsilon}(\mathbf{v}) \, \mathrm{d}x
$$
$$
m(\mathbf{u}, \mathbf{v}) := \int_{\Omega} \rho \mathbf{u} \cdot \mathbf{v} \, \mathrm{d}x
$$

The problem then becomes: find the eigenvalue $\lambda = \omega^2$ and the corresponding non-trivial [mode shape](@entry_id:168080) $\mathbf{u} \in V$ such that for all test functions $\mathbf{v} \in V$:
$$
a(\mathbf{u}, \mathbf{v}) = \lambda \, m(\mathbf{u}, \mathbf{v})
$$
The [function space](@entry_id:136890) $V$ is typically a Sobolev space, such as $[H^1(\Omega)]^d$, containing functions with square-integrable first derivatives, further constrained to satisfy the homogeneous [essential boundary conditions](@entry_id:173524) (e.g., $V = \{\mathbf{v} \in [H^1(\Omega)]^d : \mathbf{v} = \mathbf{0} \text{ on } \Gamma_D\}$).

### Finite Element Discretization and the Algebraic Eigenproblem

The continuous variational problem provides the foundation for the [finite element formulation](@entry_id:164720). The core idea of FEM is to approximate the infinite-dimensional [function space](@entry_id:136890) $V$ with a finite-dimensional subspace $V_h \subset V$. We discretize the domain $\Omega$ into a mesh of elements and approximate the [displacement field](@entry_id:141476) $\mathbf{u}(\mathbf{x})$ within this subspace using a [linear combination](@entry_id:155091) of basis functions, known as **[shape functions](@entry_id:141015)** $N_i(\mathbf{x})$.
$$
\mathbf{u}(\mathbf{x}) \approx \mathbf{u}_h(\mathbf{x}) = \sum_{i=1}^{N} \boldsymbol{\phi}_i N_i(\mathbf{x})
$$
Here, $\boldsymbol{\phi}_i$ represents the vector of nodal displacement values (degrees of freedom, DOFs) associated with the basis function $N_i$, and $N$ is the total number of DOFs in the model. Collecting all nodal DOFs into a single global vector $\boldsymbol{\phi}$, we can write this as $\mathbf{u}_h(\mathbf{x}) = \mathbf{N}(\mathbf{x})\boldsymbol{\phi}$.

Substituting this approximation into the [bilinear forms](@entry_id:746794) $a(\cdot, \cdot)$ and $m(\cdot, \cdot)$ transforms the continuous problem into a discrete one. The strain energy, associated with the stiffness form, becomes a quadratic form of the nodal displacements:
$$
a(\mathbf{u}_h, \mathbf{v}_h) = \boldsymbol{\psi}^\top \mathbf{K} \boldsymbol{\phi}
$$
where $\boldsymbol{\phi}$ and $\boldsymbol{\psi}$ are the nodal DOF vectors for $\mathbf{u}_h$ and the test function $\mathbf{v}_h$, respectively. The **[global stiffness matrix](@entry_id:138630)** $\mathbf{K}$ is defined by:
$$
\mathbf{K} = \int_{\Omega} \mathbf{B}^\top \mathbf{D} \mathbf{B} \, \mathrm{d}x
$$
Here, $\mathbf{D}$ is the matrix representation of the [elasticity tensor](@entry_id:170728) $\boldsymbol{C}$, and $\mathbf{B}$ is the [strain-displacement matrix](@entry_id:163451), which contains spatial derivatives of the shape functions and relates strain to nodal displacements, $\boldsymbol{\varepsilon}_h = \mathbf{B}\boldsymbol{\phi}$.

Similarly, the kinetic energy, associated with the mass form, becomes:
$$
m(\mathbf{u}_h, \mathbf{v}_h) = \boldsymbol{\psi}^\top \mathbf{M} \boldsymbol{\phi}
$$
where the **global [mass matrix](@entry_id:177093)** $\mathbf{M}$ is given by:
$$
\mathbf{M} = \int_{\Omega} \rho \mathbf{N}^\top \mathbf{N} \, \mathrm{d}x
$$

The global matrices $\mathbf{K}$ and $\mathbf{M}$ are assembled by summing the contributions from individual element matrices, $\mathbf{K}^e$ and $\mathbf{M}^e$, according to the mesh connectivity. For example, consider a simple bar modeled with two linear elements connecting nodes 1-2 and 2-3. The contributions of element 1 (nodes 1,2) and element 2 (nodes 2,3) are added into the global system. The entry at the intersection of the row and column for the shared node 2 is the sum of contributions from both adjacent elements [@problem_id:2562448].

With these [matrix representations](@entry_id:146025), the [weak form](@entry_id:137295) $a(\mathbf{u}_h, \mathbf{v}_h) = \lambda m(\mathbf{u}_h, \mathbf{v}_h)$ becomes $\boldsymbol{\psi}^\top \mathbf{K} \boldsymbol{\phi} = \lambda \boldsymbol{\psi}^\top \mathbf{M} \boldsymbol{\phi}$. Since this must hold for any [test function](@entry_id:178872) $\mathbf{v}_h$ (and thus for any vector $\boldsymbol{\psi}$), we arrive at the **generalized [algebraic eigenvalue problem](@entry_id:169099)** for free vibration [@problem_id:2562593]:
$$
\mathbf{K}\boldsymbol{\phi} = \lambda \mathbf{M}\boldsymbol{\phi}
$$
The solutions to this problem are the eigenpairs $(\lambda_i, \boldsymbol{\phi}_i)$, where the eigenvalues $\lambda_i = \omega_i^2$ are the squares of the [natural frequencies](@entry_id:174472), and the eigenvectors $\boldsymbol{\phi}_i$ are the corresponding discrete [mode shape](@entry_id:168080) vectors.

### Properties of the Discrete System

The algebraic structure of the problem $\mathbf{K}\boldsymbol{\phi} = \lambda \mathbf{M}\boldsymbol{\phi}$ imparts several crucial properties to its solutions, all of which have direct physical interpretations.

#### Symmetry and Definiteness

The stiffness and mass matrices are inherently tied to the system's energy. The [strain energy](@entry_id:162699) of the discrete system is $U = \frac{1}{2}\boldsymbol{\phi}^\top \mathbf{K} \boldsymbol{\phi}$, and the kinetic energy is $T = \frac{1}{2}\dot{\boldsymbol{\phi}}^\top \mathbf{M} \dot{\boldsymbol{\phi}}$. Based on these energy definitions and the properties of the underlying physical materials (symmetric elasticity tensor, positive mass density), both $\mathbf{K}$ and $\mathbf{M}$ are real and symmetric matrices [@problem_id:2562518].

*   The **mass matrix $\mathbf{M}$** is **[symmetric positive definite](@entry_id:139466) (SPD)**. Since mass density $\rho$ is strictly positive, the kinetic energy must be positive for any non-zero motion ($\dot{\boldsymbol{\phi}} \neq \mathbf{0}$), implying $\dot{\boldsymbol{\phi}}^\top \mathbf{M} \dot{\boldsymbol{\phi}} > 0$.

*   The **[stiffness matrix](@entry_id:178659) $\mathbf{K}$** is **symmetric positive semidefinite (SPSD)**. The strain energy must be non-negative. It can, however, be zero for non-zero displacements if the displacement corresponds to a **[rigid-body motion](@entry_id:265795)**, which induces no strain.

#### Rigid-Body Modes

For a structure that is not sufficiently constrained (e.g., an airplane in flight or a satellite in orbit, idealized with free-free boundary conditions), it can translate or rotate as a whole without deforming. These motions produce no strain energy, so $U = \frac{1}{2}\boldsymbol{\phi}^\top \mathbf{K} \boldsymbol{\phi} = 0$. The vectors $\boldsymbol{\phi}$ describing these motions form the **nullspace** of $\mathbf{K}$. For a general 3D solid body, there are six such independent rigid-body motions: three translations and three rotations. The [nullspace](@entry_id:171336) of $\mathbf{K}$ therefore has a dimension of six [@problem_id:2562607]. Substituting $\mathbf{K}\boldsymbol{\phi}=\mathbf{0}$ into the eigenvalue problem gives $\mathbf{0} = \lambda \mathbf{M}\boldsymbol{\phi}$. Since $\mathbf{M}$ is SPD and $\boldsymbol{\phi}$ is non-zero, this equation can only be satisfied if $\lambda = 0$. Thus, unconstrained structures possess a number of zero-frequency modes equal to the number of rigid-body motions.

To analyze the [vibrational modes](@entry_id:137888) (the flexible modes), these rigid-body motions must be removed by applying sufficient **[essential boundary conditions](@entry_id:173524)** (e.g., fixing a point or line). This is done by eliminating the corresponding rows and columns from the matrices or by using methods like the penalty approach [@problem_id:2562448]. Once constrained, the [stiffness matrix](@entry_id:178659) $\mathbf{K}$ becomes positive definite for the remaining free DOFs, and all resulting eigenvalues $\lambda$ will be strictly positive.

#### Orthogonality and Normalization

A key property of the symmetric [generalized eigenvalue problem](@entry_id:151614) is the orthogonality of its eigenvectors. For two distinct eigenpairs $(\lambda_i, \boldsymbol{\phi}_i)$ and $(\lambda_j, \boldsymbol{\phi}_j)$ where $\lambda_i \neq \lambda_j$, it can be shown that:
$$
\boldsymbol{\phi}_j^\top \mathbf{M} \boldsymbol{\phi}_i = 0 \quad (\text{M-orthogonality or mass-orthogonality})
$$
$$
\boldsymbol{\phi}_j^\top \mathbf{K} \boldsymbol{\phi}_i = 0 \quad (\text{K-orthogonality or stiffness-orthogonality})
$$
This means the mode shapes are orthogonal with respect to the inner products defined by the [mass and stiffness matrices](@entry_id:751703). Physically, this property is the foundation of [modal analysis](@entry_id:163921), as it allows the total dynamic response of a system to be decoupled into the responses of independent single-degree-of-freedom oscillators.

Since the eigenvectors are only defined up to a scalar multiple, it is customary to normalize them. A common and useful convention is **[mass normalization](@entry_id:178966)**, where each eigenvector $\boldsymbol{\phi}_i$ is scaled such that its "modal mass" is unity:
$$
\boldsymbol{\phi}_i^\top \mathbf{M} \boldsymbol{\phi}_i = 1
$$
With this normalization, the stiffness orthogonality relation becomes $\boldsymbol{\phi}_i^\top \mathbf{K} \boldsymbol{\phi}_i = \lambda_i$, meaning the "modal stiffness" is equal to the eigenvalue [@problem_id:2562593].

This modal decoupling property is elegantly preserved even when [viscous damping](@entry_id:168972) is introduced, provided the damping is **proportional** (also known as Rayleigh damping). A damping matrix of the form $\mathbf{C} = \alpha \mathbf{M} + \beta \mathbf{K}$ can be simultaneously diagonalized by the undamped [mode shapes](@entry_id:179030), preserving the uncoupled nature of the [equations of motion](@entry_id:170720) in modal coordinates [@problem_id:2562518].

### The Mass Matrix: Consistent vs. Lumped Formulations

While the [stiffness matrix](@entry_id:178659) is almost universally derived as described, there are two common approaches to formulating the [mass matrix](@entry_id:177093), leading to an important practical choice.

The [mass matrix](@entry_id:177093) $\mathbf{M}$ derived directly from the Galerkin procedure, $\mathbf{M} = \int \rho \mathbf{N}^\top \mathbf{N} \, \mathrm{d}x$, is known as the **[consistent mass matrix](@entry_id:174630)**. It is termed "consistent" because it uses the same shape functions that were used to derive the [stiffness matrix](@entry_id:178659). This matrix is generally fully populated and couples the inertial effects between nodes. For a 1D linear [bar element](@entry_id:746680), the [consistent mass matrix](@entry_id:174630) is [@problem_id:2562450]:
$$
\mathbf{M}^e_{\text{cons}} = \frac{\rho A L}{6} \begin{pmatrix} 2  1 \\ 1  2 \end{pmatrix}
$$

An alternative is the **[lumped mass matrix](@entry_id:173011)**, which is a [diagonal approximation](@entry_id:270948). The simplest lumping scheme is to sum the entries of each row of the [consistent mass matrix](@entry_id:174630) and place the sum on the diagonal, setting all off-diagonal terms to zero. This procedure conserves the total mass of the element. For the 1D [bar element](@entry_id:746680), this results in:
$$
\mathbf{M}^e_{\text{lump}} = \frac{\rho A L}{2} \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}
$$
This physically corresponds to simply splitting the total element mass and assigning it to the nodes.

From a theoretical standpoint, the [consistent mass matrix](@entry_id:174630) is superior. Its derivation is variationally consistent with Hamilton's principle. This means the discrete kinetic energy $\frac{1}{2}\dot{\boldsymbol{\phi}}^\top \mathbf{M}_{\text{cons}} \dot{\boldsymbol{\phi}}$ is exactly equal to the kinetic energy of the continuous velocity field represented by the [finite element approximation](@entry_id:166278), $T(\dot{\mathbf{u}}_h)$ [@problem_id:2562574]. This **energy equivalence** ensures that the finite element method with a [consistent mass matrix](@entry_id:174630) is a true Rayleigh-Ritz variational method.

In contrast, the [lumped mass matrix](@entry_id:173011) breaks this equivalence. The resulting system of equations is no longer the direct result of a consistent [variational principle](@entry_id:145218). This has significant theoretical consequences, which we explore next.

### Variational Principles and Convergence

The eigenvalues of the system can be characterized by the **Rayleigh quotient**:
$$
R(\boldsymbol{\phi}) = \frac{\boldsymbol{\phi}^\top \mathbf{K} \boldsymbol{\phi}}{\boldsymbol{\phi}^\top \mathbf{M} \boldsymbol{\phi}} = \frac{a(\mathbf{u}_h, \mathbf{u}_h)}{m(\mathbf{u}_h, \mathbf{u}_h)}
$$
Physically, this represents the ratio of the maximum potential energy to the maximum kinetic energy during a harmonic vibration in the shape $\boldsymbol{\phi}$. The eigenvalues $\lambda_i$ are the stationary values of this quotient.

The **Courant-Fischer min-max theorem** provides a powerful formal characterization of these eigenvalues. For the $k$-th ordered eigenvalue $\lambda_k$, it states:
$$
\lambda_k = \min_{\substack{S \subset \mathbb{R}^n \\ \dim S = k}} \max_{\substack{\boldsymbol{\phi} \in S \\ \boldsymbol{\phi} \neq \mathbf{0}}} R(\boldsymbol{\phi})
$$
When FEM with a [consistent mass matrix](@entry_id:174630) is used, the discrete problem is a Rayleigh-Ritz approximation of the continuous problem. This has profound implications for the accuracy of the computed eigenvalues [@problem_id:2562602]:

1.  **Upper Bound Property**: The computed discrete eigenvalues $\tilde{\lambda}_k$ are guaranteed to be upper bounds on the true eigenvalues $\lambda_k$ of the underlying continuous system. That is, $\lambda_k \le \tilde{\lambda}_k$. The finite element model is "stiffer" than the continuum it approximates because the [trial space](@entry_id:756166) $V_h$ restricts the possible deformation modes.

2.  **Monotonic Convergence**: If we refine the mesh such that the new [trial space](@entry_id:756166) $V_{H}$ contains the old one ($V_h \subset V_H$), the new approximate eigenvalues $\tilde{\lambda}^{(H)}_k$ will be less than or equal to the old ones: $\tilde{\lambda}^{(H)}_k \le \tilde{\lambda}^{(h)}_k$. This means that as we refine the mesh, our approximate eigenvalues monotonically decrease, converging towards the true values from above.

These guarantees are lost when a [lumped mass matrix](@entry_id:173011) is used, as the method is no longer a strict Rayleigh-Ritz procedure. Although lumped mass can sometimes produce surprisingly accurate results for coarse meshes, this is often due to a fortuitous cancellation of errors (the error from [mass lumping](@entry_id:175432) offsetting the stiffening error from displacement [discretization](@entry_id:145012)), not due to theoretical superiority [@problem_id:2562574].

### Numerical Pathologies in Eigenvalue Problems

While the [finite element method](@entry_id:136884) is a powerful and robust tool, improper element formulation can lead to numerical artifacts that corrupt the eigenvalue spectrum and produce non-physical results. Two of the most notorious pathologies are [hourglassing](@entry_id:164538) and [shear locking](@entry_id:164115).

#### Spurious Zero-Energy Modes (Hourglassing)

In an effort to reduce computational cost or remedy other issues like locking, it is common to use **[reduced integration](@entry_id:167949)**, where the stiffness matrix integrand is evaluated at fewer quadrature points than required for exact integration. While often effective, this can introduce artificial [zero-energy modes](@entry_id:172472), known as **[hourglass modes](@entry_id:174855)**.

These are deformation patterns that produce zero strain at the reduced set of integration points, and thus zero strain energy, even though they are not rigid-body motions. For example, a bilinear [quadrilateral element](@entry_id:170172) evaluated with a single Gauss point at its center will have two such [hourglass modes](@entry_id:174855) in addition to its three rigid-body modes [@problem_id:2562519]. These modes appear in the discrete eigenvalue spectrum as additional, non-physical zero-frequency modes. This renders the element unstable, as it can deform in these patterns without resistance, which can contaminate the dynamic solution of a larger structure.

#### Shear Locking

Another critical [pathology](@entry_id:193640), particularly relevant in beam and plate/[shell elements](@entry_id:176094), is **[shear locking](@entry_id:164115)**. This occurs when an element formulation is unable to correctly represent the behavior of the structure in a particular limit, such as a beam becoming very thin.

Consider a Timoshenko [beam element](@entry_id:177035) that includes [shear deformation](@entry_id:170920), modeled with equal-order [linear interpolation](@entry_id:137092) for both transverse displacement and cross-section rotation. In the thin-beam limit ($h \to 0$), the physics dictates that the [shear strain](@entry_id:175241) should vanish. The element's stiffness matrix contains a shear energy term that becomes a dominant penalty term as the thickness $h$ decreases. To minimize this enormous energy penalty, the discrete element tries to enforce a near-zero shear strain condition. However, due to the impoverished linear interpolation, the element can only achieve this by also suppressing physical bending curvature. This results in an element that is artificially and non-physically stiff in bending. This phenomenon is [shear locking](@entry_id:164115) [@problem_id:2562463].

The consequence for [vibration analysis](@entry_id:169628) is a dramatic **overestimation of the natural frequencies**, especially for higher modes. As the beam thickness tends to zero for a fixed mesh, the computed eigenvalues can spuriously diverge. Shear locking is a stiffness-related pathology and is not resolved by changing the mass matrix formulation. It must be addressed through improved element technology, such as using selective/[reduced integration](@entry_id:167949) for the shear term or employing more sophisticated [mixed formulations](@entry_id:167436).