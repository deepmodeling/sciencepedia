## Introduction
Reduced-Order Models (ROMs) have become a cornerstone of modern computational science and engineering, offering a pathway to rapidly simulate and analyze complex physical systems. By projecting the governing equations onto a low-dimensional subspace, ROMs can achieve dramatic speed-ups over high-fidelity, full-order models. However, for systems governed by [nonlinear partial differential equations](@entry_id:168847), a standard Galerkin projection is insufficient. A critical computational bottleneck emerges, as the evaluation of the nonlinear terms remains dependent on the size of the [full-order model](@entry_id:171001), negating the primary benefit of [model reduction](@entry_id:171175).

This article addresses this challenge directly by providing a comprehensive exploration of **[hyper-reduction](@entry_id:163369)**, a class of techniques specifically designed to create truly efficient nonlinear ROMs. By approximating the nonlinear operators themselves, [hyper-reduction](@entry_id:163369) severs the link to the [full-order model](@entry_id:171001)'s complexity during the online simulation phase. In the following sections, you will gain a deep understanding of these powerful methods.

The journey begins in **Principles and Mechanisms**, where we will dissect the computational bottleneck and introduce the core ideas behind the two major families of [hyper-reduction](@entry_id:163369): interpolation-based methods like DEIM and quadrature-based methods like ECSW. We will explore their theoretical foundations, offline/online decomposition, and crucial properties like stability and structure preservation. Next, in **Applications and Interdisciplinary Connections**, we will showcase the versatility of these techniques across a range of challenging domains, including [nonlinear structural dynamics](@entry_id:169437), path-dependent plasticity, and [coupled multiphysics](@entry_id:747969) and multiscale systems. Finally, **Hands-On Practices** will provide opportunities to solidify your knowledge by working through targeted problems that illuminate the practical implementation and theoretical consequences of applying [hyper-reduction](@entry_id:163369).

## Principles and Mechanisms

This section delves into the core principles and mechanisms of [hyper-reduction](@entry_id:163369), a class of techniques indispensable for creating computationally efficient Reduced-Order Models (ROMs) for [nonlinear systems](@entry_id:168347). We begin by quantifying the computational bottleneck that arises in standard projection-based ROMs for nonlinear problems. We then explore two major families of [hyper-reduction](@entry_id:163369) techniques: those based on interpolation of the assembled force vector, and those based on modifying the numerical quadrature of the underlying [weak form](@entry_id:137295). Throughout, we will emphasize the theoretical underpinnings, practical implementation via offline/online decomposition, and crucial properties such as stability and structure preservation.

### The Computational Bottleneck in Nonlinear Reduced-Order Models

In the context of [nonlinear mechanics](@entry_id:178303), a semi-discretized system arising from the Finite Element Method (FEM) often takes the form of a system of [ordinary differential equations](@entry_id:147024):

$$
M \ddot{u}(t) + f_{\text{int}}(u(t)) = f_{\text{ext}}(t)
$$

Here, $u(t) \in \mathbb{R}^{N}$ is the vector of $N$ displacement degrees of freedom, $M$ is the mass matrix, $f_{\text{ext}}(t)$ is the external force vector, and $f_{\text{int}}(u(t)): \mathbb{R}^{N} \to \mathbb{R}^{N}$ is the nonlinear internal force vector. This nonlinearity, which may stem from material behavior or large deformations, is the central challenge.

A projection-based ROM approximates the high-dimensional state $u(t)$ in a low-dimensional subspace. This is achieved by defining a [basis matrix](@entry_id:637164) $V \in \mathbb{R}^{N \times r}$ with $r \ll N$, whose columns span the subspace. The state is then approximated as $u(t) \approx V q(t)$, where $q(t) \in \mathbb{R}^{r}$ is the vector of reduced coordinates. Applying a Galerkin projection—that is, enforcing that the residual of the governing equation is orthogonal to the trial subspace spanned by $V$—yields the [reduced-order model](@entry_id:634428) [@problem_id:2566927]:

$$
M_{r} \ddot{q}(t) + g(q(t)) = f_{r}(t)
$$

where $M_{r} = V^{T} M V \in \mathbb{R}^{r \times r}$ is the [reduced mass](@entry_id:152420) matrix, $f_{r}(t) = V^{T} f_{\text{ext}}(t) \in \mathbb{R}^{r}$ is the reduced external force, and $g(q) = V^{T} f_{\text{int}}(V q(t)) \in \mathbb{R}^{r}$ is the reduced nonlinear internal force.

While this system involves only $r$ unknowns, a critical computational bottleneck remains hidden within the term $g(q)$. The evaluation of this term requires three steps:
1.  **Reconstruction (or "lifting"):** Compute the full-dimensional state approximation, $u_{approx} = Vq$.
2.  **Full-Order Evaluation:** Evaluate the nonlinear function on the full-order state, $f_{\text{int}}(u_{approx})$.
3.  **Projection:** Project the resulting vector back to the reduced space, $g(q) = V^{T} f_{\text{int}}(u_{approx})$.

The second step, the evaluation of $f_{\text{int}}(Vq)$, is the source of the problem. The function $f_{\text{int}}$ is defined by the full-order finite element model. Its evaluation involves looping over all elements and quadrature points in the mesh. Consequently, the computational cost of this step scales with the size of the [full-order model](@entry_id:171001), $N$, not the size of the reduced model, $r$. This dependence on $N$ during the online simulation phase negates the primary benefit of [model reduction](@entry_id:171175) for [nonlinear systems](@entry_id:168347).

To make this explicit, consider the online [floating-point](@entry_id:749453) operation (flop) count for assembling the reduced residual $g(q)$ and its Jacobian, the reduced [tangent stiffness matrix](@entry_id:170852) $K_{r}(q) = V^{T} K_{T}(Vq) V$, in a single Newton iteration for a quasi-static problem [@problem_id:2566923]. Here, $K_T(u) = \partial f_{\text{int}} / \partial u$. The assembly involves a loop over the total number of quadrature points, $N_{\text{q}}$. At each quadrature point, we must:
1.  Calculate the strain from the reduced coordinates: $\varepsilon = (BV)q$. This costs $O(mr)$ [flops](@entry_id:171702), where $m$ is the number of strain components.
2.  Evaluate the stress $\sigma(\varepsilon)$ and the [consistent tangent modulus](@entry_id:168075) $C(\varepsilon)$.
3.  Assemble contributions to the reduced residual and tangent.

Summing these operations over all $N_{\text{q}}$ quadrature points reveals that the total online cost is proportional to $N_{\text{q}}$. For instance, a detailed analysis shows a cost of $N_{\text{q}} ( c_{\sigma} + c_{C} + 4mr + 2m^{2}r + 2r^{2}m)$, where $c_{\sigma}$ and $c_C$ are costs of constitutive evaluations [@problem_id:2566923]. Since $N_{\text{q}}$ is a characteristic of the [full-order model](@entry_id:171001), the online cost remains coupled to $N$.

The central objective of **[hyper-reduction](@entry_id:163369)** is to sever this link. It aims to approximate the nonlinear term $g(q)$ and its Jacobian in such a way that the evaluation cost is independent of $N$ and scales only polynomially with the reduced dimension $r$ and other small parameters related to the approximation itself [@problem_id:2566927].

### Decoupling State and Operator Approximation: The Two-Basis Approach

The key insight enabling [hyper-reduction](@entry_id:163369) is the recognition that we must approximate not only the solution state but also the nonlinear operator itself. The state basis $V$ is constructed to efficiently represent the *solution manifold*, the set of all possible state vectors $\{u(t)\}$. This is typically done by performing Proper Orthogonal Decomposition (POD) on a collection of state snapshots, $\{u^{(1)}, u^{(2)}, \dots, u^{(k)}\}$, gathered from high-fidelity simulations [@problem_id:2566948]. These snapshots are arranged column-wise into a state snapshot matrix $X = [u^{(1)} \dots u^{(k)}] \in \mathbb{R}^{N \times k}$. POD on $X$ yields the [optimal basis](@entry_id:752971) $V \in \mathbb{R}^{N \times r}$ for representing these states.

However, the nonlinear function $f_{\text{int}}$ maps the solution manifold to a different manifold in $\mathbb{R}^{N}$, the *force manifold*. The space required to accurately represent the force vectors $\{f_{\text{int}}(u^{(i)})\}$ is generally not the same as the space spanned by $V$ [@problem_id:2566928]. For example, in [solid mechanics](@entry_id:164042), the columns of $V$ represent characteristic displacement shapes, while the vectors $f_{\text{int}}(u)$ represent internal force distributions, which have different physical units and mathematical structure.

Therefore, a second, "collateral" basis is needed to approximate the nonlinear force term. This force basis, which we denote by $U \in \mathbb{R}^{N \times s}$ (where $s$ is the basis size), is constructed to efficiently represent the force manifold. Analogous to the state basis, $U$ is typically built by applying POD to a set of force snapshots, $\{f_{\text{int}}(u^{(1)}), \dots, f_{\text{int}}(u^{(k)})\}$. These are collected into a force snapshot matrix $F = [f_{\text{int}}(u^{(1)}) \dots f_{\text{int}}(u^{(k)})] \in \mathbb{R}^{N \times k}$ [@problem_id:2566948].

The dual-basis approach is the foundation of many [hyper-reduction](@entry_id:163369) methods:
-   The **state basis $V$** controls the state approximation error, $\|u - Vq\|$.
-   The **force basis $U$** (in conjunction with a sampling or integration scheme) controls the operator [approximation error](@entry_id:138265), enabling computational decoupling from $N$ [@problem_id:2566928].

With this framework, we can now explore specific mechanisms for achieving an $N$-independent online evaluation.

### Mechanism I: Interpolation-Based Hyper-reduction

The first major class of [hyper-reduction](@entry_id:163369) methods approximates the fully assembled, $N$-dimensional force vector, $f_{\text{int}}(Vq)$, within the low-dimensional subspace spanned by the force basis $U$. The challenge is to find the coefficients of this approximation cheaply. The **Discrete Empirical Interpolation Method (DEIM)** is the canonical example of this approach.

#### The Discrete Empirical Interpolation Method (DEIM)

DEIM constructs an approximation $\hat{f}(u)$ to a vector $f(u) \in \mathbb{R}^N$ that satisfies two conditions [@problem_id:2566937]:
1.  **Range Condition:** The approximation must lie in the subspace spanned by the force basis, i.e., $\hat{f}(u) \in \text{span}(U)$.
2.  **Interpolation Condition:** The approximation must match the [true vector](@entry_id:190731) $f(u)$ at a small number of pre-selected components, or "sample points".

From the range condition, we can write the approximation as $\hat{f}(u) = U c(u)$ for some unknown coefficient vector $c(u) \in \mathbb{R}^{s}$. The interpolation condition is enforced using a sampling matrix $P \in \mathbb{R}^{N \times s}$, whose columns are canonical basis vectors selecting $s$ rows. The condition is $P^T \hat{f}(u) = P^T f(u)$.

Combining these two conditions yields a small linear system for the coefficients $c(u)$:
$$
P^T (U c(u)) = P^T f(u) \implies (P^T U) c(u) = P^T f(u)
$$
Assuming the matrix $P^T U \in \mathbb{R}^{s \times s}$ is invertible (which is ensured by the greedy algorithm used to select the sample points in the DEIM procedure), we can solve for the coefficients [@problem_id:2566937, part A]:
$$
c(u) = (P^T U)^{-1} P^T f(u)
$$
Substituting this back gives the explicit DEIM approximation:
$$
\hat{f}_{\text{int}}(u) = U (P^T U)^{-1} P^T f_{\text{int}}(u)
$$
This expression reveals the structure of a DEIM-based hyper-reduced model. The approximation consists of three actions: (1) evaluate only the $s$ sampled entries of the full force vector, $P^T f_{\text{int}}(u)$; (2) solve a small system to find the coefficients; and (3) reconstruct the approximation in the force basis $U$.

This leads to a powerful [offline-online decomposition](@entry_id:177117) [@problem_id:2566898]. The reduced nonlinear force becomes:
$$
g(q) = V^T f_{\text{int}}(Vq) \approx V^T \hat{f}_{\text{int}}(Vq) = \left( V^T U (P^T U)^{-1} \right) \left( P^T f_{\text{int}}(Vq) \right)
$$
-   **Offline Stage:** All quantities independent of the online state $q(t)$ are precomputed. This includes the state basis $V$, the force basis $U$, the sampling matrix $P$, and most importantly, the reduced operator $C_r = V^T U (P^T U)^{-1} \in \mathbb{R}^{r \times s}$.
-   **Online Stage:** At each time step, given $q(t)$:
    1.  Evaluate only the $s$ required entries of the internal force, $f_s(q) = P^T f_{\text{int}}(Vq)$. This step is designed to be $N$-independent, as it only requires element-level computations for those elements containing the sample points.
    2.  Compute the approximate reduced force via a small matrix-vector product: $g(q) \approx C_r f_s(q)$. The cost of this mapping is $O(rs)$.

The total online cost is now independent of $N$, achieving the goal of [hyper-reduction](@entry_id:163369) [@problem_id:2566898].

#### Properties and Stability of DEIM

The DEIM operator $\Pi_{\text{DEIM}} = U (P^T U)^{-1} P^T$ is an **oblique projector**. It projects onto the subspace $\text{span}(U)$ along the kernel of the sampling operator, $\ker(P^T)$ [@problem_id:2566937, part B]. A key property of any projector is that it is an identity operator for vectors already in its target subspace. Thus, if a force vector $f_{\text{int}}(u)$ happens to lie exactly in $\text{span}(U)$, DEIM will reconstruct it perfectly (in exact arithmetic) [@problem_id:2566937, part F].

In practice, the numerical stability of this reconstruction is paramount. The process involves solving the linear system $(P^T U)c = P^T f$. The stability of this solution is governed by the condition number of the matrix $A = P^T U$. A large condition number, $\kappa_2(P^T U)$, implies that small perturbations in the sampled data $P^T f$ (due to measurement noise or [floating-point error](@entry_id:173912)) can be amplified into large errors in the computed coefficients $c$, and thus in the final approximation $\hat{f}$ [@problem_id:2566896]. The relative error in the reconstruction is bounded by:
$$
\frac{\|\delta_{\hat{f}}\|_2}{\|\hat{f}\|_2} \le \kappa_2(P^T U) \frac{\|\delta_s\|_2}{\|P^T f\|_2}
$$
where $\delta_s$ is the perturbation in the samples. The standard DEIM point-[selection algorithm](@entry_id:637237) is designed to keep this condition number from becoming excessively large. For example, for the simple case with $U = \begin{pmatrix} 1/2  -1/(2\sqrt{3}) \\ 1/2  3/(2\sqrt{3}) \\ 1/\sqrt{2}  -1/\sqrt{6} \end{pmatrix}$ and $P$ selecting the first two rows, the condition number is a modest $\kappa_2(P^T U) = \sqrt{3}$ [@problem_id:2566896].

### Mechanism II: Quadrature-Based Hyper-reduction

A second, philosophically different family of [hyper-reduction](@entry_id:163369) methods operates not on the assembled force vector, but at a more fundamental level: the [numerical integration](@entry_id:142553) of the [weak form](@entry_id:137295). Instead of approximating the vector $f_{\text{int}}$, these methods approximate the integral that defines it.

The internal force vector can be written as an assembly of contributions from all quadrature points in the mesh:
$$
f_{\text{int}}(u) = \sum_{k=1}^{N_q} w_k \Phi_k(u)
$$
where $k$ is a global index over all $N_q$ quadrature points, $w_k$ is the corresponding quadrature weight (including the Jacobian of the element mapping), and $\Phi_k(u)$ is a vector-valued integrand (related to the product of the [basis function](@entry_id:170178) gradients and the stress). The reduced internal force is then:
$$
g_i(q) = V_{:,i}^T f_{\text{int}}(Vq) = \sum_{k=1}^{N_q} w_k \left( V_{:,i}^T \Phi_k(Vq) \right) = \sum_{k=1}^{N_q} w_k g_{i,k}(q)
$$
The high computational cost comes from summing over all $N_q$ points. Quadrature-based [hyper-reduction](@entry_id:163369) replaces this full sum with a sparse one over a small, specially selected subset of $m \ll N_q$ quadrature points.

#### The Empirical Cubature Method (ECM)

The **Empirical Cubature Method (ECM)** formulates this as a problem of finding a new, sparse quadrature rule. Given a set of training integrands (e.g., $g_{i,k}(q_{\text{train}})$ for various training states $q_{\text{train}}$), ECM seeks a small subset of quadrature points $\mathcal{S} \subset \{1, \dots, N_q\}$ with $|\mathcal{S}|=m$ and a new set of positive weights $\{\alpha_p\}_{p \in \mathcal{S}}$ such that the sparse rule accurately approximates the full integral [@problem_id:2566910]:
$$
\sum_{k=1}^{N_q} w_k g(x_k) \approx \sum_{p \in \mathcal{S}} \alpha_p g(x_p)
$$
The points and weights are typically found by solving a [constrained least-squares](@entry_id:747759) problem that forces the approximation to be exact for all integrands in the training set. The constraint that the weights $\alpha_p$ be positive is crucial for stability.

The resulting hyper-reduced model then computes the reduced force online by only visiting the $m$ selected quadrature points:
$$
g_i(q) \approx \sum_{p \in \mathcal{S}} \alpha_p g_{i,p}(q)
$$
Since $m$ is small, the online cost is decoupled from $N_q$ (and thus $N$). The accuracy of the ECM approximation depends on how well the online integrands are represented by the linear span of the training integrands. If an online integrand lies within this span, the error is zero. Otherwise, the error can be systematically reduced by enriching the training set [@problem_id:2566910, part E].

### Advanced Topic: Structure Preservation

For many physical systems, particularly in mechanics, the nonlinear operators possess special mathematical structure. For instance, in a conservative hyperelastic solid, the internal force is the gradient of a [scalar potential](@entry_id:276177) energy, $f_{\text{int}}(u) = \partial \Pi / \partial u$. This implies that the tangent stiffness matrix $K(u) = \partial f_{\text{int}} / \partial u$ is symmetric. This structure is physically meaningful (representing [path-independence](@entry_id:163750) of work) and computationally desirable (allowing the use of efficient symmetric solvers).

A critical issue in [hyper-reduction](@entry_id:163369) is whether this structure is preserved by the approximation.

-   **DEIM:** Since DEIM approximates the vector field $f_{\text{int}}$ directly, the resulting approximation $\hat{f}_{\text{int}}$ is generally *not* the gradient of any [scalar potential](@entry_id:276177). This is known as breaking the conservative structure. A major consequence is that the consistent Jacobian of the DEIM-reduced residual, $\widehat{J}(a) = V^T U (P^T U)^{-1} P^T K(Va) V$, is **non-symmetric** in general [@problem_id:2566984]. Using this correct but non-symmetric Jacobian restores quadratic convergence for Newton's method but requires a more expensive non-symmetric linear solver. Using a symmetrized but inconsistent Jacobian, such as $(V^T K(Va) V)$, destroys quadratic convergence.

-   **ECM and ECSW:** Quadrature-based methods like ECM and **Energy-Conserving Sampling and Weighting (ECSW)** offer a structural remedy [@problem_id:2566984, part E]. These methods can be formulated to approximate the [scalar potential](@entry_id:276177) energy $\Pi(u)$ itself with a hyper-reduced potential $\widehat{\Pi}(u)$, constructed from a weighted sum over sampled elements or quadrature points. The hyper-reduced force and stiffness are then *defined* as the derivatives of this approximate potential:
    $$
    \widehat{f}_{\text{int}}(u) := \frac{\partial \widehat{\Pi}(u)}{\partial u} \quad \text{and} \quad \widehat{K}(u) := \frac{\partial^2 \widehat{\Pi}(u)}{\partial u^2}
    $$
    By construction, $\widehat{f}_{\text{int}}$ is conservative with respect to $\widehat{\Pi}$, and $\widehat{K}$ is guaranteed to be symmetric. The resulting reduced [tangent stiffness matrix](@entry_id:170852) for the hyper-reduced model is therefore symmetric and consistent with the reduced residual, preserving the fundamental structure of the original system. ECSW, in particular, is formulated as an optimization problem to match the reduced [internal virtual work](@entry_id:172278) over a training set, subject to non-negative weights, explicitly designed to preserve the energetic properties of the system [@problem_id:2566965].

In summary, the choice of [hyper-reduction](@entry_id:163369) mechanism involves a trade-off. Interpolation-based methods like DEIM are powerful and general but may break inherent physical structures. Quadrature-based methods like ECM and ECSW are more intrusive to the FEM code but can be designed to preserve critical structures like [symmetry and conservation laws](@entry_id:160300), leading to more robust and physically faithful [reduced-order models](@entry_id:754172).