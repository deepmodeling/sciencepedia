## Introduction
High-fidelity simulation of complex physical systems, such as [lithium-ion batteries](@entry_id:150991), provides invaluable insight but comes at a tremendous computational cost. This expense often makes such models impractical for applications requiring rapid iteration, like automated design optimization, real-time control, or digital twin deployment. The central challenge is to drastically reduce simulation time without sacrificing the essential physics captured by the governing equations. Model Order Reduction (MOR) provides a powerful set of techniques to address this, and among them, Galerkin projection stands out as a foundational, physics-based approach. It offers a systematic way to transform a large, computationally intensive model into a small, fast-executing surrogate that retains a strong connection to the original system.

This article provides a detailed exploration of Galerkin projection for [model reduction](@entry_id:171175). We begin in the "Principles and Mechanisms" chapter by building the method from its mathematical foundations in [weighted residuals](@entry_id:1134032), exploring its application to linear and nonlinear systems, and detailing how to construct an [optimal basis](@entry_id:752971) from data using Proper Orthogonal Decomposition (POD). The second chapter, "Applications and Interdisciplinary Connections," moves from theory to practice, demonstrating how these techniques are adapted to the complex, multiphysics environment of battery engineering, addressing challenges like parametric dependencies and nonlinearities, and highlighting methods that preserve crucial physical structures. Finally, the "Hands-On Practices" section offers targeted problems to solidify your understanding of the core concepts, from basis construction to ensuring physical constraints are met in the reduced model.

## Principles and Mechanisms

This chapter elucidates the fundamental principles and mechanisms of Galerkin projection for [model order reduction](@entry_id:167302). We will begin by establishing the foundational concept of [weighted residual methods](@entry_id:165159), from which Galerkin projection emerges as a specific and powerful instance. We will then systematically explore its application to linear, nonlinear, and dynamical systems, and discuss the critical task of constructing an effective reduced basis from data. Finally, we will delve into the practical advantages of the offline-online computational paradigm and address advanced topics essential for creating robust and physically faithful reduced-order models, particularly in the context of electrochemical systems like batteries.

### The Foundation: The Method of Weighted Residuals

At its core, [model order reduction](@entry_id:167302) via projection addresses the challenge of solving a complex system of equations, often arising from the spatial [discretization of partial differential equations](@entry_id:748527) (PDEs), which we can abstractly write as:
$$
\mathcal{A}(u) = f
$$
Here, $u$ is the unknown state vector residing in a high-dimensional Hilbert space $H$ (e.g., $\mathbb{R}^N$ for a discrete system of dimension $N$), $\mathcal{A}$ is a linear or nonlinear operator, and $f$ is a source or [forcing term](@entry_id:165986). The dimension $N$ can be exceedingly large (millions or more), making repeated solution of this system computationally prohibitive.

The central idea of projection-based reduction is to seek an approximate solution, $u_r$, that does not live in the full space $H$, but rather in a much smaller, carefully chosen low-dimensional subspace $V \subset H$, known as the **trial subspace**. Let this subspace be of dimension $r \ll N$. Since $u_r$ is constrained to $V$, it can be expressed as a [linear combination](@entry_id:155091) of a set of basis vectors $\{\phi_i\}_{i=1}^r$ that span $V$:
$$
u_r = \sum_{j=1}^r a_j \phi_j
$$
where $a_j$ are the unknown scalar coefficients, or reduced coordinates.

Because the true solution $u$ is generally not in $V$, the approximation $u_r$ will not satisfy the original equation exactly. Substituting $u_r$ into the equation yields a non-zero **residual**, $R(u_r)$:
$$
R(u_r) = \mathcal{A}(u_r) - f \neq 0
$$
The **Method of Weighted Residuals** provides a principled way to determine the unknown coefficients $a_j$ by enforcing a condition on this residual. We demand that the residual be "small" by making it orthogonal to a second chosen subspace, $W \subset H$, known as the **test subspace**. Orthogonality is defined with respect to a chosen inner product $(\cdot, \cdot)$ on the space $H$. The governing condition is:
$$
(R(u_r), w) = 0, \quad \forall w \in W
$$
This single statement represents $r$ scalar equations, obtained by testing against each [basis vector](@entry_id:199546) of $W$ (assuming $\dim(W) = r$), which is precisely the number needed to solve for the $r$ unknown coefficients $a_j$.

The specific choice of the [test space](@entry_id:755876) $W$ relative to the [trial space](@entry_id:756166) $V$ defines the particular projection method .

-   **Galerkin Projection**: In the standard Galerkin (or Bubnov-Galerkin) method, the test subspace is chosen to be identical to the trial subspace, i.e., $W = V$. This choice is particularly natural and advantageous when the operator $\mathcal{A}$ possesses symmetry properties, as it often leads to a reduced system that inherits this stability and structure.

-   **Petrov-Galerkin Projection**: This is the more general case where the test subspace is different from the trial subspace, $W \neq V$. This additional freedom is powerful and often necessary. For instance, in problems with non-[self-adjoint operators](@entry_id:152188), such as those in convection-dominated fluid dynamics, a cleverly chosen [test space](@entry_id:755876) $W$ can introduce [artificial diffusion](@entry_id:637299) that stabilizes the reduced model, a feat the standard Galerkin method might fail to achieve.

Throughout this chapter, we will primarily focus on the Galerkin method, but the distinction is a crucial one in the broader field of numerical methods.

### Galerkin Projection for Linear Systems

Let us first consider a linear operator equation $\mathcal{A}u = b$, where $\mathcal{A}$ is a [linear operator](@entry_id:136520). The Galerkin condition becomes: find $u_r \in V$ such that
$$
(\mathcal{A}u_r - b, v) = 0, \quad \forall v \in V
$$
By the linearity of the inner product, this is equivalent to $(\mathcal{A}u_r, v) = (b, v)$ for all $v \in V$. Expressing $u_r$ in terms of its basis, $u_r = \sum_{j=1}^r a_j \phi_j$, and testing against each basis function $\phi_i \in V$, we obtain:
$$
\sum_{j=1}^r (\mathcal{A}\phi_j, \phi_i) a_j = (b, \phi_i), \quad \text{for } i=1, \dots, r
$$
This is a linear system of $r \times r$ equations for the unknown coefficients $a_j$.

In many practical applications, such as those arising from a Finite Element Method (FEM) discretization of a PDE, the problem is already in a discrete matrix form, $Au = b$, where $A \in \mathbb{R}^{N \times N}$ and $u, b \in \mathbb{R}^{N}$. Furthermore, the inner product itself may be weighted to reflect physical properties of the system. For instance, in a battery electrode model, the inner product might be weighted by the local capacity density $\rho(x)$, leading to a discrete inner product $(u,v)_M = u^T M v$, where $M$ is a [symmetric positive definite](@entry_id:139466) **[mass matrix](@entry_id:177093)** .

Let the basis for the trial subspace $V$ be represented by the columns of a matrix $\Phi \in \mathbb{R}^{N \times r}$. The reduced-order solution is then $u_r = \Phi a$, where $a \in \mathbb{R}^r$ is the vector of reduced coordinates. The Galerkin condition, tested against the basis vectors (the columns of $\Phi$), becomes:
$$
\Phi^T M (A (\Phi a) - b) = 0
$$
Rearranging this gives the reduced linear system:
$$
(\Phi^T M A \Phi) a = \Phi^T M b
$$
The reduced system matrix is $A_r = \Phi^T M A \Phi$ and the reduced right-hand side is $b_r = \Phi^T M b$. This is an $r \times r$ system, which is trivial to solve if $r$ is small.

A powerful theoretical property underpins the Galerkin method for certain classes of operators. If the operator $A$ is **self-adjoint** (symmetric) and **[positive definite](@entry_id:149459)** with respect to the inner product—a common case for diffusion and [structural mechanics](@entry_id:276699) problems—then the Galerkin projection provides the best possible approximation in the **[energy norm](@entry_id:274966)** . The [energy norm](@entry_id:274966) is defined as $\|e\|_A = \sqrt{(Ae, e)}$. The Galerkin solution $u_r$ is the unique vector in the subspace $V$ that minimizes the error $\|u - u_r\|_A$. This optimality provides a strong justification for its use in these contexts.

This framework extends directly to [linear dynamical systems](@entry_id:150282), which are common in [battery modeling](@entry_id:746700) after linearization. For a semi-discretized system of the form
$$
M \dot{x}(t) + K x(t) = f(t)
$$
where $M$ and $K$ are the full-order [mass and stiffness matrices](@entry_id:751703), we apply the approximation $x(t) \approx \Phi x_r(t)$. The Galerkin projection (using the standard Euclidean inner product for simplicity, i.e., $M=I$ in the [projection formula](@entry_id:152164)) requires the residual to be orthogonal to the basis $\Phi$:
$$
\Phi^T (M \Phi \dot{x}_r + K \Phi x_r - f) = 0
$$
This immediately yields the reduced-order dynamical system :
$$
M_r \dot{x}_r(t) + K_r x_r(t) = f_r(t)
$$
where the reduced operators are $M_r = \Phi^T M \Phi$, $K_r = \Phi^T K \Phi$, and $f_r(t) = \Phi^T f(t)$. The original $N$-dimensional system of ODEs is thus transformed into an $r$-dimensional system.

### Galerkin Projection for Nonlinear Systems

The principle of Galerkin projection applies equally well to nonlinear problems, which are ubiquitous in high-fidelity [battery modeling](@entry_id:746700) due to phenomena like Butler-Volmer [reaction kinetics](@entry_id:150220). Consider a spatially discretized nonlinear system written in residual form:
$$
F(u) = 0
$$
where $F: \mathbb{R}^N \to \mathbb{R}^N$ is a nonlinear map. We again seek an approximate solution $u_r$ in a low-dimensional representation. It is often useful to define this approximation relative to a [reference state](@entry_id:151465) $u_{\text{ref}}$, forming an **affine trial manifold**:
$$
u_r = u_{\text{ref}} + \Phi a
$$
The Galerkin condition requires the residual, evaluated at the approximate solution, to be orthogonal to the [test space](@entry_id:755876) $V$ (spanned by the columns of $\Phi$). Using a [mass-weighted inner product](@entry_id:178170), this is stated as :
$$
(F(u_r), v)_M = 0, \quad \forall v \in V
$$
Substituting the expression for $u_r$ and testing against the basis vectors in $\Phi$, we arrive at the compact matrix form:
$$
\Phi^T M F(u_{\text{ref}} + \Phi a) = 0
$$
This is a system of $r$ nonlinear algebraic equations for the $r$ unknown reduced coordinates in the vector $a$. This small nonlinear system must then be solved using an iterative method, such as Newton-Raphson. The key is that the computationally intensive work is shifted from solving an $N$-dimensional system to solving an $r$-dimensional one.

### Constructing the Optimal Basis: Proper Orthogonal Decomposition

Thus far, we have assumed the existence of a "good" basis $\Phi$. The quality of the reduced-order model is entirely dependent on how well the subspace $V$ can represent the true solutions of the system. A generic basis (e.g., Fourier modes or random vectors) is unlikely to be efficient. **Proper Orthogonal Decomposition (POD)**, also known as Principal Component Analysis (PCA), provides a systematic method for constructing an [optimal basis](@entry_id:752971) from data.

The procedure begins by generating data. We run the high-fidelity model for a representative set of inputs and parameters, and we collect the state vectors at various points in time. These are called **snapshots**. Let's say we have $m$ snapshots, which we arrange as columns in a **[snapshot matrix](@entry_id:1131792)** $X \in \mathbb{R}^{N \times m}$.

The goal of POD is to find an $r$-dimensional orthonormal basis that is optimal in the sense that it minimizes the total squared projection error of the snapshots onto that basis. For a standard Euclidean norm, we want to find a subspace $V$ that minimizes:
$$
\mathcal{E}(V) = \sum_{j=1}^m \|x_j - P_V x_j\|_2^2
$$
where $P_V$ is the orthogonal projector onto $V$. The Eckart-Young-Mirsky theorem from linear algebra provides the solution to this problem: the [optimal basis](@entry_id:752971) is given by the first $r$ [left singular vectors](@entry_id:751233) of the [snapshot matrix](@entry_id:1131792) $X$. These vectors are obtained from the **Singular Value Decomposition (SVD)** of $X$:
$$
X = U \Sigma W^T
$$
The columns of $U \in \mathbb{R}^{N \times N}$ are the [left singular vectors](@entry_id:751233), the diagonal entries of $\Sigma \in \mathbb{R}^{N \times m}$ ($\sigma_1 \ge \sigma_2 \ge \dots \ge 0$) are the singular values, and the columns of $W \in \mathbb{R}^{m \times m}$ are the [right singular vectors](@entry_id:754365). The optimal POD basis of rank $r$ is simply the matrix $\Phi = U_r$ containing the first $r$ columns of $U$.

The singular values provide a powerful guide for choosing the dimension $r$ of the reduced model. The total "energy" of the snapshots, measured by the squared Frobenius norm, is equal to the sum of the squares of the singular values: $\|X\|_F^2 = \sum_i \sigma_i^2$. The energy captured by a rank-$r$ POD basis is $\sum_{i=1}^r \sigma_i^2$. We can therefore choose $r$ to capture a desired fraction of the total energy, for example, by finding the smallest $r$ such that :
$$
\frac{\sum_{i=1}^{r} \sigma_i^2}{\sum_{i=1}^{p} \sigma_i^2} \ge \alpha
$$
where $p$ is the rank of $X$ and $\alpha$ is a threshold close to 1 (e.g., $0.99999$). The singular values also provide explicit [error bounds](@entry_id:139888). The error of the best rank-$r$ approximation to the snapshot set is given by the truncated singular values. In the operator [2-norm](@entry_id:636114), this error is simply the first truncated [singular value](@entry_id:171660), $\sigma_{r+1}$, which also serves as a uniform bound on the projection error for any individual snapshot .

In many physical systems, variables may have different units and scales. It is often crucial to scale the rows of the [snapshot matrix](@entry_id:1131792) to non-dimensionalize the states before performing POD. This is mathematically equivalent to performing POD with a weighted norm induced by a diagonal [scaling matrix](@entry_id:188350) . More generally, when working with models from FEM, the natural norm is the one induced by the mass matrix, $\|x\|_M^2 = x^T M x$. In this case, the [optimal basis](@entry_id:752971) is found by computing the SVD of the weighted [snapshot matrix](@entry_id:1131792), $\tilde{X} = M^{1/2} X$, and the resulting basis vectors are $\Phi = M^{-1/2} U_r$ . A common and effective practice is also to center the data by subtracting the mean snapshot before computing the SVD; this yields an optimal affine subspace for approximation .

### The Offline-Online Computational Strategy

The true power of [projection-based model reduction](@entry_id:753807) is realized in a two-phase computational workflow, particularly for [parametric models](@entry_id:170911) where simulations must be run for many different design or operating parameters $\mu$.

The **offline phase** is computationally intensive and performed only once. It involves all the expensive calculations that depend on the full-system dimension $N$:
1.  **Training:** Run the high-fidelity model for a curated set of training parameters $\mu_{\text{train}}$ to generate a rich set of snapshots.
2.  **Basis Computation:** Use POD on the snapshots to compute the reduced basis $\Phi$.
3.  **Operator Projection:** For parametric [linear operators](@entry_id:149003) with an affine decomposition (e.g., $M(\mu) = \sum_q \theta_q(\mu) M_q$), pre-compute the constant reduced matrices $\Phi^T M_q \Phi$ for each component $q$.
4.  **Hyper-reduction:** For nonlinear terms, the evaluation of $g_r(a; \mu) = \Phi^T g(\Phi a; \mu)$ still depends on the large dimension $N$. To break this dependency, [hyper-reduction](@entry_id:163369) techniques like the **Discrete Empirical Interpolation Method (DEIM)** are used. DEIM constructs a separate basis for the nonlinear term and identifies a small number of critical evaluation points, allowing the reduced nonlinear term to be approximated rapidly without ever forming the full $N$-dimensional vector .

The **online phase** is computationally cheap and can be executed rapidly for any new parameter $\mu$.
1.  **Assembly:** Evaluate the scalar coefficient functions $\theta_q(\mu)$ and assemble the small $r \times r$ reduced matrices from the pre-computed offline components.
2.  **Simulation:** Solve the small $r$-dimensional reduced-order model (ROM). The cost of this step is independent of the original dimension $N$.

This [offline-online decomposition](@entry_id:177117) enables the use of high-fidelity physics in applications that demand near-real-time performance, such as automated design optimization, state estimation in battery management systems, and control.

### Advanced Topics and Fidelity Considerations

While the core methodology is broadly applicable, creating high-fidelity ROMs often requires addressing more subtle aspects of the underlying model structure.

#### Commutativity of Discretization and Projection

We have primarily focused on a "discretize-then-project" approach, where we start with a discrete high-dimensional system and reduce it. One could also imagine a "project-then-discretize" approach, where one first projects the continuous PDE onto a functional basis and then discretizes the resulting low-dimensional system. A fundamental result in numerical analysis states that these two procedures yield identical reduced models if and only if two conditions are met: (1) the reduced basis functions are exactly representable in the discretization basis (e.g., for FEM, the reduced basis is a subspace of the FE space, $V \subset V_h$), and (2) the integrals defining the operators are computed exactly (or with identical, sufficiently accurate [quadrature rules](@entry_id:753909)) in both procedures . This provides theoretical justification for the common "discretize-then-project" workflow.

#### Preservation of Physical Structure I: Conservation Laws

Physical models often embed fundamental conservation laws (e.g., conservation of mass, charge, or energy). A standard Galerkin projection does not automatically guarantee that the ROM will respect these laws, which can lead to unphysical behavior like a slow drift in total mass over time.

For a conserved quantity that can be expressed as a [linear functional](@entry_id:144884) of the state, $J(y) = m^T y$, conservation in a closed system means $\frac{dJ}{dt} = m^T \dot{y} = 0$. In a system derived from FEM, this conservation is a structural property of the discrete operators. To ensure the ROM, with state $y_r = \Phi a$, preserves this property, i.e., $m^T \Phi \dot{a} = 0$, a specific condition must be imposed on the projection. The ROM is guaranteed to be conservative if the [test space](@entry_id:755876) $W$ is augmented to include the conservation vector itself, represented in the [dual space](@entry_id:146945) of the inner product. For an inner product defined by the [mass matrix](@entry_id:177093) $M$, this condition is :
$$
M^{-1}m \in \text{span}(W)
$$
Including this vector in the [test space](@entry_id:755876) explicitly builds the conservation law into the reduced equations.

#### Preservation of Physical Structure II: Differential-Algebraic Equations

Many multi-physics models, including the canonical Newman-type models for batteries, are not pure systems of Ordinary Differential Equations (ODEs) after spatial discretization. Instead, they form **Differential-Algebraic Equations (DAEs)**. This occurs when some [state variables](@entry_id:138790) are governed by dynamic [evolution equations](@entry_id:268137) (containing time derivatives) while others are subject to instantaneous algebraic constraints.

In a [porous electrode model](@entry_id:1129960), for example, the concentrations of lithium in the solid and electrolyte phases ($c_s$, $c_e$) are **differential variables**, governed by parabolic diffusion equations. In contrast, assuming negligible double-layer capacitance, the electric potentials in each phase ($\phi_s$, $\phi_e$) are **algebraic variables**, determined by elliptic charge-balance equations that must hold at every instant in time . After discretization, the system takes the form:
$$
E \dot{x} = A x + B u
$$
where the **descriptor matrix** $E$ is singular because the rows corresponding to the algebraic constraints are zero. Such systems, particularly the index-1 DAEs common in [battery models](@entry_id:1121428), have a saddle-point structure. A naive Galerkin projection can be unstable. Stability often requires a **[mixed formulation](@entry_id:171379)** where the [trial and test spaces](@entry_id:756164) for the algebraic components are chosen carefully to satisfy a discrete [inf-sup condition](@entry_id:174538). Furthermore, the [gauge freedom](@entry_id:160491) of the potentials must be fixed to ensure the algebraic part of the system is uniquely solvable .

A robust strategy for reducing index-1 DAEs is to only reduce the differential part of the state, while retaining the algebraic constraints exactly. For a state partitioned as $x = [x_d^T, x_a^T]^T$, this can be achieved by using a block-structured [projection matrix](@entry_id:154479) of the form :
$$
\Phi = \begin{pmatrix} \Phi_d  0 \\ 0  I \end{pmatrix}
$$
where $\Phi_d$ is the POD basis for the differential states and $I$ is the identity matrix. This special structure ensures that the reduced system preserves the index-1 DAE form and the original algebraic constraints, leading to a much more stable and accurate ROM.