## Introduction
In modern engineering and scientific research, the ability to rapidly simulate complex physical systems is paramount for design optimization, uncertainty quantification, and control. While [model order reduction](@entry_id:167302) (MOR) techniques offer a powerful way to accelerate these simulations by projecting governing equations onto a low-dimensional subspace, they often encounter a critical roadblock: the "nonlinear bottleneck." This issue arises because evaluating nonlinear functions within the model still requires computations that scale with the original, high-dimensional system size, negating the potential [speedup](@entry_id:636881).

This article introduces a pivotal solution to this challenge: the **Discrete Empirical Interpolation Method (DEIM)**, a [hyper-reduction](@entry_id:163369) technique that efficiently approximates nonlinear terms to achieve true computational acceleration. Across the following chapters, we will provide a comprehensive guide to understanding and applying DEIM. The journey begins with **Principles and Mechanisms**, where we will dissect the core algorithm, from constructing the necessary basis via Proper Orthogonal Decomposition (POD) to selecting the crucial interpolation points. Next, in **Applications and Interdisciplinary Connections**, we will explore the real-world impact of DEIM in fields ranging from lithium-ion battery design to computational fluid dynamics, highlighting its role as an enabling technology. Finally, the **Hands-On Practices** section will offer a chance to solidify this knowledge by implementing the POD-DEIM methodology on a representative nonlinear problem, bridging the gap between theory and practical application.

## Principles and Mechanisms

In the preceding chapter, we introduced the concept of [model order reduction](@entry_id:167302) as a powerful strategy for accelerating complex simulations, particularly in automated design workflows for systems like lithium-ion batteries. We established that projecting the governing equations onto a low-dimensional subspace, often derived from Proper Orthogonal Decomposition (POD), can dramatically reduce the size of the [state-space](@entry_id:177074). However, when the underlying physical model contains nonlinearities—as is nearly always the case in realistic electrochemical systems—this projection alone is insufficient to guarantee computational efficiency. This chapter delves into the principles and mechanisms of a crucial [hyper-reduction](@entry_id:163369) technique, the **Discrete Empirical Interpolation Method (DEIM)**, designed specifically to overcome this "nonlinear bottleneck."

### The Nonlinear Bottleneck in Projection-Based Model Reduction

Let us consider a general semi-discretized system of ordinary differential equations (ODEs) arising from the spatial discretization of a set of partial differential equations (PDEs), such as the Doyle-Fuller-Newman (DFN) model for a lithium-ion battery. Such a system can often be written in the form:

$$
\mathbf{M}\dot{x}(t) = \mathbf{A}x(t) + f(x(t))
$$

Here, $x(t) \in \mathbb{R}^n$ is the **full-order state vector**, whose components might represent local concentrations and potentials at $n$ discrete points in the model geometry. The dimension $n$ can be very large, on the order of thousands or millions, to resolve fine physical details. $\mathbf{M} \in \mathbb{R}^{n \times n}$ is the mass matrix, $\mathbf{A} \in \mathbb{R}^{n \times n}$ is a matrix representing linear [transport phenomena](@entry_id:147655) like diffusion and migration, and $f: \mathbb{R}^n \to \mathbb{R}^n$ is the **nonlinear function**. In battery models, this function typically encapsulates the highly nonlinear Butler-Volmer kinetics that govern electrochemical reactions at the electrode-electrolyte interfaces .

As discussed previously, a projection-based reduced-order model (ROM) seeks an approximation of the state in a low-dimensional subspace. This is expressed as $x(t) \approx V a(t)$, where $V \in \mathbb{R}^{n \times r}$ is a [basis matrix](@entry_id:637164) with $r \ll n$ orthonormal columns (the POD modes), and $a(t) \in \mathbb{R}^r$ is the **reduced-state vector**. A Galerkin projection, which enforces that the residual of the approximation is orthogonal to the subspace spanned by $V$, yields the following ROM:

$$
V^T \mathbf{M} V \dot{a}(t) = V^T \mathbf{A} V a(t) + V^T f(V a(t))
$$

Let us define the reduced matrices $\mathbf{M}_r = V^T \mathbf{M} V$ and $\mathbf{A}_r = V^T \mathbf{A} V$. These are small $r \times r$ matrices that can be computed once in an offline stage. The ROM then becomes:

$$
\mathbf{M}_r \dot{a}(t) = \mathbf{A}_r a(t) + V^T f(V a(t))
$$

While the linear part of this system, $\mathbf{A}_r a(t)$, is computationally inexpensive to evaluate (an $\mathcal{O}(r^2)$ operation), the nonlinear term $V^T f(V a(t))$ presents a significant challenge. To evaluate this term at each time step of a simulation, one must perform a sequence of operations that depends on the full-order dimension $n$ :

1.  **Lifting/Reconstruction**: The reduced state $a(t) \in \mathbb{R}^r$ must be "lifted" back to the full-order space to obtain an approximate full state: $x_{approx} = V a(t)$. This [matrix-vector product](@entry_id:151002) has a computational cost of $\mathcal{O}(nr)$.

2.  **Nonlinear Function Evaluation**: The nonlinear function $f$ must be evaluated on this reconstructed state, $f(x_{approx})$. Since $f$ is defined on $\mathbb{R}^n$ and typically involves evaluating local physics at each of the $n$ spatial locations, its evaluation has a cost that scales with $n$, i.e., $\mathcal{O}(n)$.

3.  **Projection**: The resulting full-order vector $f(x_{approx}) \in \mathbb{R}^n$ must be projected back onto the reduced subspace via multiplication with $V^T$. This [matrix-vector product](@entry_id:151002) has a cost of $\mathcal{O}(nr)$.

The total cost to evaluate the nonlinear term is therefore $\mathcal{O}(nr) + \mathcal{O}(n)$, which simplifies to $\mathcal{O}(nr)$ since $r \ge 1$. Because this cost scales linearly with the original, large dimension $n$, the ROM fails to achieve the desired computational [speedup](@entry_id:636881). This problem is known as the **nonlinear bottleneck**. To create a truly fast ROM, we must find a way to approximate the nonlinear term without ever constructing the full $n$-dimensional vectors, a process known as **[hyper-reduction](@entry_id:163369)**. DEIM is a premier technique for achieving this.

### The Empirical Interpolation Method: From Continuous Functions to Discrete Vectors

At its heart, DEIM is an interpolation method. The fundamental idea is to approximate a complex function by a simpler function (a linear combination of basis functions) that is constrained to match the original function at a small number of cleverly chosen points.

#### The Continuous Case: Empirical Interpolation Method (EIM)

To build intuition, let's first consider the continuous version of the method, known as the **Empirical Interpolation Method (EIM)**. Suppose we want to approximate a nonlinear function $f(y; \mathbf{p}): \Omega \to \mathbb{R}$ where $y$ is a spatial coordinate in domain $\Omega$ and $\mathbf{p}$ are parameters. Assume we have a set of $m$ basis functions $\{\phi_i(y)\}_{i=1}^m$ that are known to capture the dominant features of $f$. We can write an approximation $f_m$ as a [linear combination](@entry_id:155091) of these basis functions:

$$
f(y; \mathbf{p}) \approx f_m(y; \mathbf{p}) = \sum_{i=1}^{m} c_i(\mathbf{p}) \phi_i(y)
$$

The challenge is to find the coefficients $c_i$ efficiently. EIM does this by selecting $m$ interpolation points $\{y_1, y_2, \dots, y_m\} \subset \Omega$ and enforcing that the approximation exactly matches the true function at these points:

$$
f_m(y_j; \mathbf{p}) = f(y_j; \mathbf{p}) \quad \text{for } j=1, \dots, m
$$

This leads to a square $m \times m$ linear system for the unknown coefficients $c = [c_1, \dots, c_m]^T$:

$$
\mathbf{B}c = \mathbf{f}_p
$$

where the matrix $\mathbf{B}$ has entries $B_{ji} = \phi_i(y_j)$, and the vector $\mathbf{f}_p$ has entries $(\mathbf{f}_p)_j = f(y_j; \mathbf{p})$. If the basis functions and interpolation points are chosen such that $\mathbf{B}$ is invertible, we can uniquely solve for the coefficients. The key is that we only need to evaluate the expensive function $f$ at $m$ points, rather than across the entire domain .

#### The Discrete Case: Discrete Empirical Interpolation Method (DEIM)

DEIM is the direct application of this concept to the discrete [vector-valued functions](@entry_id:261164) encountered in semi-discretized models. Let our nonlinear function be $f(x) \in \mathbb{R}^n$, and assume we have an [orthonormal basis](@entry_id:147779) matrix $U \in \mathbb{R}^{n \times m}$ whose columns span the space where the outputs of $f$ predominantly lie. The DEIM approximation, $\hat{f}$, is sought within the span of this basis:

$$
\hat{f} = U c
$$

where $c \in \mathbb{R}^m$ is the vector of unknown coefficients.

Analogous to EIM, we select $m$ interpolation indices (or "magic points") $\{p_1, p_2, \dots, p_m\} \subset \{1, \dots, n\}$ and enforce that the approximation matches the [true vector](@entry_id:190731) at these components. This can be expressed elegantly using a **selection matrix** $P \in \mathbb{R}^{n \times m}$, constructed as $P = [e_{p_1}, e_{p_2}, \dots, e_{p_m}]$, where $e_{p_j}$ is the $p_j$-th standard [basis vector](@entry_id:199546) of $\mathbb{R}^n$. Pre-multiplying a vector by $P^T$ extracts its components at the chosen indices. The interpolation condition is thus:

$$
P^T \hat{f} = P^T f
$$

Substituting $\hat{f} = U c$, we obtain a small $m \times m$ linear system for the coefficients $c$:

$$
(P^T U) c = P^T f
$$

Assuming the matrix $(P^T U)$ is invertible, we can solve for $c$:

$$
c = (P^T U)^{-1} P^T f
$$

Finally, substituting this back into the expression for $\hat{f}$ yields the explicit DEIM approximation formula:

$$
\hat{f} = U (P^T U)^{-1} P^T f
$$

This expression defines an **[oblique projection](@entry_id:752867)** of $f$ onto the subspace spanned by $U$. The crucial computational advantage is now clear: to compute the coefficients $c$, the only part that depends on the full vector $f$ is the term $P^T f$. This operation only requires evaluating the $m$ components of $f$ corresponding to the interpolation indices. The cost of the nonlinear evaluation is thus reduced from $\mathcal{O}(n)$ to $\mathcal{O}(m)$, successfully breaking the bottleneck . If the [true vector](@entry_id:190731) $f$ happens to lie exactly in the span of $U$, i.e., $f = U c_{true}$, then the DEIM approximation becomes exact: $\hat{f} = U(P^T U)^{-1} P^T(U c_{true}) = U c_{true} = f$ .

### The DEIM Algorithm in Practice: Offline Training and Online Application

The application of DEIM, like most model reduction techniques, is divided into a computationally intensive offline "training" phase and a rapid online "application" phase.

#### Offline Phase: Basis Construction and Index Selection

The goal of the offline phase is to compute the basis $U$ and the selection matrix $P$, which together define the DEIM approximation.

**Step 1: Collect Nonlinear Snapshots**
To construct a basis that can effectively represent the nonlinear term $f(x)$, we must first sample its behavior over a range of relevant conditions. This is done by running the [full-order model](@entry_id:171001) for various input parameters $\mu$ and operating conditions (e.g., different C-rates for a battery), and collecting "snapshots" of the nonlinear function's output vector at different points in time. This results in a set of vectors $\{f(x(t_j; \mu_\ell))\}$. These vectors are then assembled as columns into a **[snapshot matrix](@entry_id:1131792)** $S \in \mathbb{R}^{n \times N_s}$, where $N_s$ is the total number of snapshots collected .

$$
S = [f_1, f_2, \dots, f_{N_s}]
$$

It is critical to use snapshots of the nonlinear term $f(x)$ itself, not the state $x$, as the basis $U$ must approximate the range of $f$.

**Step 2: Compute the Nonlinear Basis ($U$)**
The next step is to find a low-dimensional basis that optimally captures the information in the [snapshot matrix](@entry_id:1131792) $S$. This is the role of **Proper Orthogonal Decomposition (POD)**. The POD basis that minimizes the squared reconstruction error of the snapshots is given by the leading [left singular vectors](@entry_id:751233) of $S$. We compute the thin Singular Value Decomposition (SVD) of the [snapshot matrix](@entry_id:1131792):

$$
S = Q \Sigma Z^T
$$

The POD basis of rank $m$ is then formed by taking the first $m$ columns of the matrix $Q$ of [left singular vectors](@entry_id:751233):

$$
U = Q_{:, 1:m}
$$

The columns of $U$ are orthonormal by construction and are ordered by their importance in representing the snapshot data . The rank $m$ is typically chosen to capture a desired amount of "energy" (e.g., 99.99%), which is related to the sum of the squared singular values.

**Step 3: Select Interpolation Indices ($P$)**
With the basis $U$ in hand, we must select the $m$ interpolation indices $\{p_1, \dots, p_m\}$ that define the matrix $P$. A poor choice of indices could lead to a singular or [ill-conditioned matrix](@entry_id:147408) $P^T U$, making the DEIM approximation unusable. The standard method for selecting these indices is a **greedy algorithm** .

The algorithm proceeds iteratively:

1.  **For $j=1$**: Find the index of the largest-magnitude entry in the first [basis vector](@entry_id:199546) $u_1$. This index is $p_1$.
    $$p_1 = \arg\max_{i=1,\dots,n} |(u_1)_i|$$

2.  **For $j=2, \dots, m$**:
    a. Find the approximation of the current [basis vector](@entry_id:199546) $u_j$ using the previously found basis vectors $\{u_1, \dots, u_{j-1}\}$ and interpolation points $\{p_1, \dots, p_{j-1}\}$. This involves solving a small $(j-1) \times (j-1)$ system for coefficients.
    b. Compute the [residual vector](@entry_id:165091) $r_j = u_j - \sum_{k=1}^{j-1} c_k u_k$. This vector represents the part of $u_j$ that cannot be represented by the previous basis vectors when constrained by interpolation.
    c. Select the next index $p_j$ as the location of the largest-magnitude entry in the [residual vector](@entry_id:165091) $r_j$.
    $$p_j = \arg\max_{i=1,\dots,n} |(r_j)_i|$$

This greedy procedure can be shown to be equivalent to performing an LU decomposition with [partial pivoting](@entry_id:138396) on $U^T$, and it guarantees (in exact arithmetic) that the resulting matrix $P^T U$ is non-singular, provided the columns of $U$ are [linearly independent](@entry_id:148207) .

#### Online Phase: Hyper-Reduced Model Simulation

Once the matrices $U$ and $P$ (and thus the pre-computable matrix products $V^T U$ and $(P^T U)^{-1}$) have been determined offline, the online simulation of the hyper-reduced model is extremely fast. The reduced system to be solved is:

$$
\mathbf{M}_r \dot{a}(t) = \mathbf{A}_r a(t) + \left( V^T U (P^T U)^{-1} \right) \left( P^T f(V a(t)) \right)
$$

At each time step, given the current reduced state $a(t)$:
1.  The full state $x_{approx} = Va$ is formed.
2.  Crucially, only the $m$ components of $f(x_{approx})$ corresponding to the indices in $P$ are evaluated to form the small vector $P^T f(V a(t)) \in \mathbb{R}^m$.
3.  This small vector is then multiplied by the pre-computed constant matrix $V^T U (P^T U)^{-1} \in \mathbb{R}^{r \times m}$ to obtain the final reduced nonlinear term.

The entire evaluation of the nonlinear term now has a cost that scales with the small dimensions $r$ and $m$, completely independent of the original dimension $n$. Furthermore, for [implicit time integration](@entry_id:171761) methods that require a Newton solver, the Jacobian of the DEIM-approximated residual can also be computed efficiently, as it too only depends on the $m$ selected rows of the full Jacobian .

### Advanced Considerations and Practical Challenges

While DEIM is a powerful and elegant method, its practical application requires attention to certain numerical subtleties.

#### Well-Posedness and Conditioning

The invertibility of the $m \times m$ matrix $P^T U$ is fundamental to the entire method. As noted, the greedy [selection algorithm](@entry_id:637237) is designed to ensure this. It is important to recognize that simply choosing $m$ distinct indices is a necessary but not [sufficient condition](@entry_id:276242) for invertibility; the greedy procedure provides a constructive algorithm to ensure it .

However, even if $P^T U$ is invertible, it may be **ill-conditioned**, meaning its singular values span many orders of magnitude. This makes the solution for the coefficients $c$ highly sensitive to small perturbations or numerical errors in the right-hand side $P^T f$. Such [ill-conditioning](@entry_id:138674) often arises when the underlying physics is highly localized, for example, at the thin interfaces between the electrode and separator in a battery. In such cases, the POD basis vectors in $U$ will also be localized, having significant magnitude in only a few rows. This property is quantified by a high **coherence** of the [basis matrix](@entry_id:637164). The greedy algorithm, by seeking large-magnitude entries, will tend to select interpolation indices that are clustered together in these "hotspots." This can result in the selected rows of $U$ being nearly linearly dependent, leading to the [ill-conditioning](@entry_id:138674) of $P^T U$ .

Several strategies exist to mitigate this problem:
*   **Oversampling**: Instead of selecting $m$ indices, we can select $k > m$ indices to form an [overdetermined system](@entry_id:150489) $(P_k^T U)c = P_k^T f$. This rectangular system is then solved in a least-squares sense, i.e., $\min_c \|(P_k^T U)c - P_k^T f\|_2^2$. This approach tends to average out errors and produce a better-conditioned problem.
*   **Regularization**: To further stabilize the solution, especially in the presence of noise, Tikhonov regularization can be added to the [least-squares problem](@entry_id:164198): $\min_c \{\|(P_k^T U)c - P_k^T f\|_2^2 + \lambda^2 \|c\|_2^2\}$, where $\lambda > 0$ is a small [regularization parameter](@entry_id:162917).
*   **Alternative Selection Algorithms**: More robust index selection algorithms, such as those based on QR factorization with [column pivoting](@entry_id:636812) (often called Q-DEIM), can be used instead of the standard greedy approach. These methods are designed to select a set of "more orthogonal" rows, directly improving the conditioning of the resulting system .

By understanding these principles and practical considerations, DEIM can be robustly applied to create highly efficient and accurate reduced-order models for complex [nonlinear systems](@entry_id:168347), enabling the rapid simulation and automated design exploration that is essential in modern engineering.