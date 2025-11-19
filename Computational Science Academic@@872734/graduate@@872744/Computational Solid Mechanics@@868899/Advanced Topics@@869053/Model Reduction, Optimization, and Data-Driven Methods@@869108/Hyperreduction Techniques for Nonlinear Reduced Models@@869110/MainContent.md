## Introduction
In the world of [computational solid mechanics](@entry_id:169583), Reduced-Order Models (ROMs) have emerged as indispensable tools for accelerating complex simulations. By projecting high-dimensional governing equations onto a low-dimensional subspace, ROMs promise to deliver results orders of magnitude faster than traditional full-order models. However, when faced with material or [geometric nonlinearity](@entry_id:169896), a significant challenge arises: the computational cost of evaluating nonlinear forces does not scale down with the model's dimension, creating a persistent bottleneck that undermines the very purpose of model reduction.

This article addresses this critical knowledge gap by providing a comprehensive exploration of **[hyperreduction](@entry_id:750481)**, a family of secondary approximation techniques designed specifically to make nonlinear ROMs computationally efficient. By mastering these methods, engineers and scientists can unlock the full potential of model reduction for rapid design, optimization, and uncertainty quantification in complex physical systems.

This guide is structured to build your expertise systematically. The first chapter, **"Principles and Mechanisms,"** will dissect the computational bottleneck and introduce the core mathematical machinery behind seminal [hyperreduction](@entry_id:750481) techniques. Following this, **"Applications and Interdisciplinary Connections"** will showcase the practical power of these methods across a range of challenging problems in mechanics and beyond. Finally, the **"Hands-On Practices"** section will provide you with opportunities to apply these concepts and solidify your understanding through targeted exercises. We will begin by examining the fundamental principles that motivate the need for [hyperreduction](@entry_id:750481) and govern its various forms.

## Principles and Mechanisms

Having established the motivation for employing Reduced-Order Models (ROMs) in [computational solid mechanics](@entry_id:169583), we now delve into the principles and mechanisms that govern their construction and, crucially, their efficient implementation. A central challenge arises in nonlinear problems, where the promise of computational speed-up offered by [dimensionality reduction](@entry_id:142982) can be undermined by the very nature of nonlinearity. This chapter will dissect this challenge and introduce the class of techniques known as **[hyperreduction](@entry_id:750481)**, which are essential for realizing the full potential of nonlinear ROMs.

### The Computational Bottleneck in Nonlinear Reduced-Order Models

The foundation of [projection-based model reduction](@entry_id:753807) lies in approximating the high-dimensional state vector of a system, such as the [displacement vector](@entry_id:262782) $u \in \mathbb{R}^{n}$ from a Finite Element (FE) model, within a low-dimensional subspace. This is achieved by expressing the state as a [linear combination](@entry_id:155091) of pre-computed basis vectors, which form the columns of a [basis matrix](@entry_id:637164) $\Phi \in \mathbb{R}^{n \times r}$, where $r \ll n$. The approximation takes the form:

$$
u \approx \Phi q
$$

Here, $q \in \mathbb{R}^{r}$ is the vector of reduced coordinates. The governing equations of the [full-order model](@entry_id:171001) (FOM), which may represent [static equilibrium](@entry_id:163498) or dynamic motion, are generally expressed in terms of a [residual vector](@entry_id:165091) $r(u) \in \mathbb{R}^{n}$ that must be nullified. For instance, in a quasi-static problem, we seek to solve $r(u) = f_{\text{ext}} - f_{\text{int}}(u) = 0$, where $f_{\text{ext}}$ and $f_{\text{int}}$ are the external and internal force vectors, respectively.

Instead of solving this system in the high-dimensional space, a ROM solves a much smaller system by enforcing a weighted residual condition. The most common approach is the **Galerkin projection**, where the residual is made orthogonal to the trial subspace itself. This results in the reduced system of $r$ equations for the $r$ unknowns in $q$:

$$
\Phi^{T} r(\Phi q) = 0
$$

At first glance, this appears to be a small system of nonlinear equations that should be fast to solve. However, a critical computational bottleneck emerges. The internal force vector, $f_{\text{int}}(u)$, is assembled by integrating contributions from all elements in the FE mesh, a process formally written as $f_{\text{int}}(u) = \sum_{e=1}^{N_{el}} f_{e}(u)$, where $N_{el}$ is the total number of elements [@problem_id:3572703]. Consequently, to evaluate the term $r(\Phi q)$, one must first construct the full-dimensional state $\Phi q$, then compute the internal force $f_{\text{int}}(\Phi q)$ by iterating over all $N_{el}$ elements, and only then project the resulting $n$-dimensional vector onto the reduced space via pre-multiplication by $\Phi^{T}$. The computational cost of evaluating the nonlinear function $r(\cdot)$ still scales with the size of the [full-order model](@entry_id:171001), $n$, rendering the ROM ineffective for significant speed-up in the nonlinear regime [@problem_id:3572662].

**Hyperreduction** refers to a class of secondary approximation techniques designed specifically to overcome this bottleneck. The core idea is to approximate the expensive nonlinear term $r(\Phi q)$ with a surrogate, $\hat{r}(\Phi q)$, whose evaluation cost is independent of the FOM size $n$ and scales instead with the reduced dimension $r$ (or a similarly small number).

### Projection Frameworks: Galerkin and Petrov-Galerkin Methods

Before examining specific [hyperreduction](@entry_id:750481) techniques, it is essential to formalize the projection framework. The Galerkin method is a specific instance of a broader class of [weighted residual methods](@entry_id:165159). We seek an approximate solution $u_r = \Phi q$ in the trial subspace $\mathcal{V}_r = \text{span}\{\Phi\}$. The [weighted residual method](@entry_id:756686) requires the residual $r(u_r)$ to be orthogonal to a chosen *test subspace*, $\mathcal{W}_r$. If the test subspace is spanned by the columns of a [basis matrix](@entry_id:637164) $W \in \mathbb{R}^{n \times r}$, the reduced system becomes:

$$
W^{T} r(\Phi q) = 0
$$

This is known as a **Petrov-Galerkin projection**. The Galerkin method is the special case where the test subspace is identical to the trial subspace, i.e., $W = \Phi$ [@problem_id:3572682].

While Galerkin projection is most common due to its optimality properties for self-adjoint problems, Petrov-Galerkin methods offer additional flexibility. For example, the **Least-Squares Petrov-Galerkin (LSPG)** method seeks to minimize the Euclidean norm of the full-order residual, $\frac{1}{2} \| r(\Phi q) \|_2^2$, at each solution step. The [first-order optimality condition](@entry_id:634945) for this minimization problem is $\frac{\partial}{\partial q} (\frac{1}{2} \| r(\Phi q) \|_2^2) = 0$, which yields:

$$
\Phi^{T} J(\Phi q)^{T} r(\Phi q) = 0
$$

where $J(u) = \partial r(u) / \partial u$ is the Jacobian of the residual. This shows that LSPG is a Petrov-Galerkin method with a state-dependent test basis $W(q) = J(\Phi q) \Phi$ [@problem_id:3572682]. The choice of projection framework has implications for [hyperreduction](@entry_id:750481), as the goal is ultimately to approximate the projected quantities, $W^T r(\Phi q)$, efficiently.

### Core Mechanism I: Approximation via Subspace Projection and Interpolation

One major family of [hyperreduction](@entry_id:750481) techniques approximates the nonlinear function vector itself, be it the internal force $f_{\text{int}}(u)$ or the entire residual $r(u)$. These methods are data-driven and operate within an offline/online paradigm.

#### The Offline/Online Computational Strategy

The core premise is that while the vector $f_{\text{int}}(u)$ can point in any direction in $\mathbb{R}^n$, the set of all force vectors encountered during a simulation, $\{f_{\text{int}}(u(t)) | t \in [0, T]\}$, lies on or near a low-dimensional nonlinear manifold. The offline stage is dedicated to finding a linear subspace that effectively approximates this manifold.

1.  **Offline Stage (Training):** A set of high-fidelity FOM simulations is performed for representative parameter values $\mu_j$ and operating conditions. During these simulations, snapshots of the quantity to be approximated (e.g., the internal force vector) are collected at various time instances $t_k$: $\mathbf{S}_{f} = [ f_{\text{int}}(u(t_1;\mu_1)) | f_{\text{int}}(u(t_2;\mu_1)) | \dots ]$ [@problem_id:3572710].

2.  **Basis Construction:** **Proper Orthogonal Decomposition (POD)**, which is mathematically equivalent to computing the Singular Value Decomposition (SVD) of the snapshot matrix $\mathbf{S}_{f}$, is used to extract a set of orthonormal basis vectors. These vectors, forming the columns of a **collateral basis** matrix $U \in \mathbb{R}^{n \times m}$ (where $m$ is typically much smaller than the number of snapshots), span a subspace that optimally captures the variance in the training data.

3.  **Sampling Scheme Construction:** Based on the collateral basis $U$, a sampling or interpolation rule is created. This rule dictates which few components of the nonlinear vector need to be evaluated in the online stage.

4.  **Online Stage (Execution):** For a new simulation with a new parameter $\mu$, the pre-computed basis $U$ and sampling rule are used to construct an approximation $\hat{f}_{\text{int}}(u)$ at a cost proportional to $m$ rather than $n$.

#### Discrete Empirical Interpolation Method (DEIM)

The **Discrete Empirical Interpolation Method (DEIM)** is a prominent technique that realizes this strategy through interpolation. Given the collateral basis $U$ of rank $m$, the goal is to find an approximation $\hat{f}(u)$ of the form $\hat{f}(u) = U c(u)$, where $c(u) \in \mathbb{R}^m$ is a vector of coefficients. To avoid computing the full vector $f(u)$, DEIM determines $c(u)$ by enforcing that the approximation matches the true function at just $m$ cleverly selected component indices, $\{i_1, \dots, i_m\}$ [@problem_id:3572661].

This interpolation constraint can be written using a sampling matrix $P \in \mathbb{R}^{n \times m}$, whose $k$-th column is the canonical basis vector $e_{i_k}$. The constraint is $P^T \hat{f}(u) = P^T f(u)$. Substituting $\hat{f}(u) = U c(u)$, we get a small $m \times m$ linear system for the coefficients:

$$
(P^T U) c(u) = P^T f(u)
$$

The interpolation indices (which define $P$) are selected via a greedy algorithm in the offline stage to ensure the matrix $P^T U$ is well-conditioned and thus invertible. The coefficients are then $c(u) = (P^T U)^{-1} P^T f(u)$, leading to the DEIM approximation:

$$
\hat{f}(u) = U (P^T U)^{-1} P^T f(u)
$$

The computational advantage is clear: the only term on the right-hand side that depends on the current state $u$ is $P^T f(u)$, which is a small vector containing only the $m$ sampled entries of the full vector $f(u)$. This circumvents the need to evaluate all $n$ components. It is crucial to distinguish this from [orthogonal projection](@entry_id:144168), $\hat{f}_{\text{proj}} = U U^T f(u)$, which provides the best fit in the $L_2$ norm but requires the full vector $f(u)$ to compute the projection coefficients $U^T f(u)$ [@problem_id:3572661].

#### Gappy POD and Least-Squares Reconstruction

DEIM is a specific instance of a broader concept. Instead of selecting exactly $m$ samples for $m$ basis vectors, one can choose to use more samples, $s > m$. In this case, the interpolation system $(P^T U) c = P^T f$ becomes an overdetermined $s \times m$ system. A solution can be found in a least-squares sense by minimizing the error in the sampled components: $\| P^T(Uc - f) \|_2$ [@problem_id:3572723].

This leads to the normal equations, whose solution for the coefficients is $c(u) = (P^T U)^{\dagger} P^T f(u)$, where $(\cdot)^{\dagger}$ denotes the Moore-Penrose [pseudoinverse](@entry_id:140762). The resulting reconstruction is:

$$
\hat{f}(u) = U (P^T U)^{\dagger} P^T f(u)
$$

This method is often called **gappy POD**. For uniqueness, the matrix $P^T U$ must have full column rank, a condition typically satisfied when $s \geq m$. Thus, DEIM is an interpolatory approach requiring a square, invertible system ($s=m$), while gappy POD is a [least-squares](@entry_id:173916) approach typically used with an [overdetermined system](@entry_id:150489) ($s > m$) for enhanced stability [@problem_id:3572723]. The **Gauss-Newton with Approximated Tensors (GNAT)** method can be understood as an application of this least-squares reconstruction principle, often applied to the entire [residual vector](@entry_id:165091) $R$ rather than just the internal force term $f_{\text{int}}$ [@problem_id:3572727].

### Core Mechanism II: Approximation via Empirical Quadrature

An alternative approach to [hyperreduction](@entry_id:750481) does not approximate the force vector directly, but rather approximates the integral that defines it. This is particularly natural in the context of the Finite Element Method, where the internal force vector is assembled from element-level contributions:

$$
f_{\text{int}}(u) = \int_{\Omega_0} B^T P(F) \, \mathrm{d}\Omega_0 = \sum_{e=1}^{N_{el}} \int_{\Omega_e} B^T P(F) \, \mathrm{d}\Omega_0 = \sum_{e=1}^{N_{el}} f_e(u)
$$

Here, the assembly process involves a sum over all elements, which is the source of the computational bottleneck. The idea of empirical quadrature is to replace this full sum with a weighted sum over a small subset of sampled elements $\mathcal{S} \subset \{1, \dots, N_{el}\}$:

$$
f_{\text{int}}(u) \approx \hat{f}_{\text{int}}(u) = \sum_{e \in \mathcal{S}} w_e f_e(u)
$$

where $\{w_e\}$ are non-negative weights. These sampled contributions are then mapped into the global vector using standard FEM assembly (scatter) operators [@problem_id:3572703]. The key question is how to select the sample set $\mathcal{S}$ and the weights $\{w_e\}$.

#### Energy-Conserving Sampling and Weighting (ECSW)

The **Energy-Conserving Sampling and Weighting (ECSW)** method provides a systematic way to determine these samples and weights based on a physical principle. For [hyperelastic materials](@entry_id:190241), the internal force is the gradient of a stored energy potential, $f_{\text{int}}(u) = \nabla_u \Pi_{\text{int}}(u)$. In a Galerkin ROM, this structure is preserved: the reduced internal force $f_r(q) = \Phi^T f_{\text{int}}(\Phi q)$ is the gradient of the reduced potential energy $\Pi_r(q) = \Pi_{\text{int}}(\Phi q)$, which guarantees that a conservative FOM leads to a conservative ROM.

The central idea of ECSW is to construct a hyperreduced model that also possesses a potential, thereby conserving a discrete energy measure. This is achieved by defining an approximate reduced potential as a weighted sum of element-level potentials over the sampled set:

$$
\hat{\Pi}_r(q) = \sum_{e \in \mathcal{S}} w_e \Pi_e(\Phi q)
$$

The corresponding hyperreduced force, $\hat{f}_r(q) = \nabla_q \hat{\Pi}_r(q)$, is then guaranteed to be conservative. The weights are determined in an offline stage by requiring that the hyperreduced model reproduces the [internal virtual work](@entry_id:172278) of the full ROM on the training data. Specifically, for a set of training states $a^k$ and virtual displacements $\Delta a^k$, the weights $\{w_e \ge 0\}$ and sample set $\mathcal{S}$ are found by solving a [constrained optimization](@entry_id:145264) problem that enforces, as closely as possible, the constraints [@problem_id:3572698]:

$$
\Delta a^{k\,T} V^{T} r(V a^{k}) \;=\; \sum_{e \in \mathcal{S}} w_{e}\, \Delta a^{k\,T} V^{T} r_{e}(V a^{k}), \quad k=1,\dots,N_{\text{tr}}
$$

The non-negativity constraint on the weights, $w_e \ge 0$, is crucial. It ensures that if the element [tangent stiffness](@entry_id:166213) matrices are [positive semi-definite](@entry_id:262808), the resulting hyperreduced [tangent stiffness matrix](@entry_id:170852) will also be [positive semi-definite](@entry_id:262808). This preserves the stability of the underlying mechanical system and is highly beneficial for the robustness of [iterative solvers](@entry_id:136910) [@problem_id:3572698] [@problem_id:3572727].

### Implications, Consistency, and Analysis

The choice of [hyperreduction](@entry_id:750481) strategy has profound implications for the accuracy, stability, and structure of the resulting [reduced-order model](@entry_id:634428).

#### Consistency and Accuracy

A primary goal in constructing a hyperreduced model is to ensure it is **consistent** with the original FOM. A fundamental consistency requirement is that the hyperreduced model should exactly reproduce the solutions from the [training set](@entry_id:636396) [@problem_id:3572692]. If $u_k = \Phi q_k$ is a FOM solution from the training data (i.e., $r(u_k;\mu_k)=0$), then $q_k$ should also be an equilibrium solution of the hyperreduced ROM (i.e., $\Phi^T \hat{r}(\Phi q_k; \mu_k)=0$). This is typically achieved by construction in methods like DEIM and ECSW, which are explicitly fit to the training data. For example, if the [hyperreduction](@entry_id:750481) is exact on the training set, $\hat{r}(u_k;\mu_k) = r(u_k;\mu_k) = 0$, this consistency is immediately satisfied.

It is crucial to understand that consistency on the [training set](@entry_id:636396) provides no guarantee of accuracy for new, "unseen" parameters. The predictive error of an HROM for a query parameter depends on two main factors: the [approximation error](@entry_id:138265) of the reduced basis $\Phi$, and the approximation error of the [hyperreduction](@entry_id:750481) scheme $\hat{r}$. For a stable problem, the error in the HROM solution, $\|q^{\widehat{\star}} - q^{\star}\|$, can be bounded by the [hyperreduction](@entry_id:750481) [approximation error](@entry_id:138265) in the residual, $\|r - \hat{r}\|$, multiplied by a stability constant related to the inverse of the reduced Jacobian. This shows a direct link between the quality of the [hyperreduction](@entry_id:750481) approximation and the accuracy of the final solution [@problem_id:3572692].

Error can be assessed in two ways [@problem_id:3572678]:
-   **A priori bounds** are theoretical estimates that depend on the best-approximation properties of the bases ($\Phi$ and the collateral basis $U$) and stability constants of the operators. They quantify the potential accuracy of the method before a solution is computed.
-   **A posteriori estimators** are computable quantities, evaluated after a solution $u_r$ is found, that provide a bound on the state error $\|u - u_r\|$. They are typically based on the norm of the full-order residual evaluated at the reduced solution, $\|R(u_r)\|$. In an HROM context, since the full residual is not computed, these estimators must rely on the sampled residual information to form a surrogate for the [residual norm](@entry_id:136782).

#### Structure Preservation and Solver Performance

In [nonlinear solid mechanics](@entry_id:171757), the internal force is derived from a [strain energy potential](@entry_id:755493), $f_{\text{int}} = \nabla_u \Psi$. This gives rise to a symmetric [tangent stiffness matrix](@entry_id:170852) $K = \partial f_{\text{int}} / \partial u = \nabla_u^2 \Psi$. This symmetry is a critical structure that enables the use of highly efficient [iterative solvers](@entry_id:136910) (e.g., Conjugate Gradient) within a Newton-Raphson solution scheme.

Hyperreduction methods interact with this structure in different ways [@problem_id:3572727]:
-   **DEIM and GNAT:** These methods generally **destroy symmetry**. The Jacobian of the approximated force, $\hat{K} = \partial \hat{f}_{\text{int}} / \partial u$, is typically non-symmetric even if the original $K$ is symmetric. This forces the use of more expensive and less robust non-symmetric solvers (e.g., GMRES).
-   **ECSW:** By preserving a potential structure and using non-negative weights, ECSW **preserves symmetry and positive semi-definiteness**. The hyperreduced tangent stiffness matrix remains symmetric, allowing for the continued use of efficient symmetric solvers.

Furthermore, to retain the quadratic convergence of Newton's method, the tangent matrix used in the solver must be the exact derivative of the approximated residual function being solved [@problem_id:3572716]. For any [hyperreduction](@entry_id:750481) method, this means the approximation of the tangent must be consistent with the approximation of the residual.

By understanding these principles and mechanisms, practitioners can make informed choices about which [hyperreduction](@entry_id:750481) technique is most suitable for a given problem, balancing the trade-offs between accuracy, computational cost, and the preservation of crucial physical and mathematical structures.