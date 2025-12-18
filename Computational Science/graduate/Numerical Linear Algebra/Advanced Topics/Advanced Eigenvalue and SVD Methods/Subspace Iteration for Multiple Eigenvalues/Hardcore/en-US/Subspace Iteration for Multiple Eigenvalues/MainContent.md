## Introduction
The [eigenvalue problem](@entry_id:143898) is a cornerstone of computational science and engineering, essential for understanding phenomena from [structural vibrations](@entry_id:174415) to the principal components of data. While simple methods suffice for small matrices, the [large-scale systems](@entry_id:166848) encountered in modern applications demand sophisticated iterative techniques. A primary challenge is the need to compute not just one, but multiple eigenpairs simultaneously, often corresponding to a cluster of eigenvalues. Subspace iteration, also known as simultaneous iteration, provides a fundamental and powerful framework for addressing this very problem.

This article offers a graduate-level exploration of subspace iteration, bridging foundational theory with modern applications. Over the course of three chapters, you will gain a deep understanding of this essential algorithm. We will begin by deconstructing its core mechanics and analyzing its convergence properties. We will then broaden our perspective to see how the method is enhanced and applied across diverse fields, from data science to [high-performance computing](@entry_id:169980). Finally, you will have the opportunity to solidify your knowledge through hands-on practice problems that highlight key implementation challenges. We begin by examining the core principles that make the algorithm work.

## Principles and Mechanisms

The preceding chapter introduced the [eigenvalue problem](@entry_id:143898) and the motivation for iterative methods capable of handling [large-scale systems](@entry_id:166848) and computing multiple eigenpairs simultaneously. We now delve into the principles and mechanisms of one of the most fundamental such methods: **subspace iteration**, also known as simultaneous iteration. This chapter will deconstruct the algorithm, analyze its convergence properties, and explore the practical considerations essential for its effective implementation.

### The Rayleigh-Ritz Procedure: Extracting Optimal Approximations

Subspace iteration, in its most basic form, can be viewed as a block version of the [power method](@entry_id:148021). Starting with a set of $p$ linearly independent vectors that form the columns of a matrix $Y_0 \in \mathbb{C}^{n \times p}$, one repeatedly applies the matrix $A$: $Y_{k+1} = A Y_k$. To prevent all columns from converging to the [dominant eigenvector](@entry_id:148010) and to maintain numerical stability, an [orthonormalization](@entry_id:140791) step is introduced at each iteration, typically via a QR factorization:

$Z_{k+1} = A Q_k$
$Z_{k+1} = Q_{k+1} R_{k+1}$

Here, $Q_k$ is an $n \times p$ matrix with orthonormal columns spanning the subspace of interest at iteration $k$. While the subspace $\mathcal{Q}_{k+1} = \operatorname{range}(Q_{k+1})$ converges to the dominant $p$-dimensional invariant subspace of $A$, the columns of $Q_{k+1}$ themselves are not necessarily the best approximations to the eigenvectors within that subspace. To extract the optimal approximations, we employ the **Rayleigh-Ritz procedure**.

The core idea is to project the large eigenvalue problem $Ax = \lambda x$ onto the much smaller trial subspace $\mathcal{Q}_k$. We seek an approximate eigenpair $(\theta, u)$ where the vector $u$ is constrained to lie in $\mathcal{Q}_k$. The quality of this approximation is enforced by a **Petrov-Galerkin condition**, which demands that the [residual vector](@entry_id:165091), $r = Au - \theta u$, be orthogonal to a chosen *test subspace*. In the Rayleigh-Ritz procedure, the test subspace is chosen to be the same as the trial subspace, $\mathcal{Q}_k$. This specific choice is also known as a **Galerkin condition**. 

Mathematically, the condition is $s^*r = 0$ for all $s \in \mathcal{Q}_k$. Since the columns of $Q_k$ form an orthonormal basis for $\mathcal{Q}_k$, this is equivalent to requiring $Q_k^* r = 0$. Substituting the definitions of $r$ and $u = Q_k y$ (where $y \in \mathbb{C}^p$ is the [coordinate vector](@entry_id:153319) of $u$ in the basis $Q_k$), we derive the projected problem:

$Q_k^* (A (Q_k y) - \theta (Q_k y)) = 0$

$(Q_k^* A Q_k) y - \theta (Q_k^* Q_k) y = 0$

Letting $T_k = Q_k^* A Q_k$ be the $p \times p$ projected matrix and using the [orthonormality](@entry_id:267887) $Q_k^* Q_k = I_p$, we arrive at a standard, small-scale [eigenvalue problem](@entry_id:143898):

$T_k y = \theta y$

The eigenpairs of this $p \times p$ matrix $T_k$ provide our desired approximations. The eigenvalues $\theta_j$ of $T_k$ are called **Ritz values**, and the corresponding vectors $u_j = Q_k y_j$ are the **Ritz vectors**. These pairs, $(\theta_j, u_j)$, represent the best approximations to the eigenpairs of $A$ that can be formed from the subspace $\mathcal{Q}_k$, in the sense that their residuals are orthogonal to $\mathcal{Q}_k$. 

### Quantifying Convergence: Principal Angles and Subspace Distance

To analyze the convergence of the subspace $\mathcal{Q}_k$ to the true [invariant subspace](@entry_id:137024) $\mathcal{U}$, we need a way to measure the "distance" or "angle" between them. The most natural and rigorous way to do this is through the concept of **[principal angles](@entry_id:201254)**.

Let $\mathcal{S}$ and $\mathcal{T}$ be two $p$-dimensional subspaces of $\mathbb{C}^n$, with [orthonormal bases](@entry_id:753010) given by the columns of matrices $Q_{\mathcal{S}}$ and $Q_{\mathcal{T}}$. The relationship between these subspaces is captured by the $p \times p$ matrix $Q_{\mathcal{S}}^* Q_{\mathcal{T}}$. Let the Singular Value Decomposition (SVD) of this matrix be $Q_{\mathcal{S}}^* Q_{\mathcal{T}} = U \Sigma V^*$, where $\Sigma = \operatorname{diag}(\sigma_1, \dots, \sigma_p)$ and $1 \ge \sigma_1 \ge \dots \ge \sigma_p \ge 0$. The **[principal angles](@entry_id:201254)** $\theta_i \in [0, \pi/2]$ are defined by:

$\cos \theta_i = \sigma_i \quad \text{for } i = 1, \dots, p$

This definition implies an ordering $0 \le \theta_1 \le \theta_2 \le \dots \le \theta_p \le \pi/2$. Critically, these angles are an intrinsic property of the subspaces themselves and do not depend on the specific choice of [orthonormal bases](@entry_id:753010) used to represent them.  A different choice of bases would only change the unitary matrices $U$ and $V$ in the SVD, leaving the singular values $\sigma_i$—and thus the [principal angles](@entry_id:201254) $\theta_i$—invariant.

The largest principal angle, $\theta_{\max} = \theta_p$, serves as a powerful measure of the distance between the subspaces. For example, it can be shown that the [operator norm](@entry_id:146227) of the projection of one subspace onto the orthogonal complement of the other is given by $\sin \theta_{\max}$:

$\| (I - P_{\mathcal{S}}) Q_{\mathcal{T}} \|_2 = \| P_{\mathcal{S}}^{\perp} P_{\mathcal{T}} \|_2 = \sin \theta_{\max}$

where $P_{\mathcal{S}}$ and $P_{\mathcal{T}}$ are the orthogonal projectors onto $\mathcal{S}$ and $\mathcal{T}$. This error measure is zero if and only if $\theta_{\max}=0$, which occurs precisely when $\mathcal{S} = \mathcal{T}$.  Convergence of subspace iteration can thus be rigorously defined as the process by which all [principal angles](@entry_id:201254) between the iterated subspace $\mathcal{Q}_k$ and the target [invariant subspace](@entry_id:137024) $\mathcal{U}$ tend to zero.

### Analysis of Convergence

The rate at which the [principal angles](@entry_id:201254) decay depends fundamentally on the properties of the matrix $A$.

#### The Ideal Case: Hermitian Matrices

For a Hermitian matrix ($A=A^*$), the eigenvectors form an orthonormal basis. This orthogonal structure leads to a clean and predictable convergence behavior. Let's assume we are targeting the $m$-dimensional [invariant subspace](@entry_id:137024) $\mathcal{U}$ associated with the $m$ largest-magnitude eigenvalues, and we are using a block size $p \ge m$. The convergence of the iterated subspace $\mathcal{Q}_k$ to $\mathcal{U}$ can be precisely characterized.

A detailed derivation shows that the tangent of the largest principal angle between the $k$-th iterate and the target subspace contracts at each step. If we assume a spectral gap exists such that $|\lambda_m| > |\lambda_{m+1}|$, and we use a block of size $p=m$, the convergence rate is governed by the ratio of the first unwanted eigenvalue to the last wanted one. For a [normal matrix](@entry_id:185943) (which includes the Hermitian case), this is captured by the inequality :

$\tan \theta_{\max}^{(k+1)} \le \frac{|\lambda_{m+1}|}{|\lambda_m|} \tan \theta_{\max}^{(k)}$

This shows that the convergence is geometric, and the rate is determined by the spectral gap. If the eigenvalues are well-separated, convergence is rapid. If they are clustered near the cutoff, convergence will be slow.

When $A$ is Hermitian, the matrix of eigenvectors $V$ is unitary, meaning its condition number $\kappa_2(V) = \|V\|_2 \|V^{-1}\|_2 = 1$. The convergence bound for the tangent of the matrix of [principal angles](@entry_id:201254), $\Theta_k$, simplifies to :

$\|\tan \Theta_k\|_2 \le \left( \frac{|\lambda_{m+1}|}{|\lambda_m|} \right)^k \|\tan \Theta_0\|_2$

This direct relationship between the [spectral gap](@entry_id:144877) and convergence makes subspace iteration particularly reliable for Hermitian problems.

#### An Abstract View: Convergence via Exterior Algebra

The reason subspace iteration converges to an entire subspace, rather than just a single eigenvector, can be elegantly understood through the lens of **[exterior algebra](@entry_id:201164)**. An $m$-dimensional subspace spanned by vectors $\{q_1, \dots, q_m\}$ can be uniquely represented (up to a scalar) by a mathematical object called a [wedge product](@entry_id:147029), $q_1 \wedge \dots \wedge q_m$, which is an element of a higher-dimensional space $\Lambda^m(\mathbb{C}^n)$.

The action of $A$ on the subspace, $S_k \to A(S_k)$, induces a [linear map](@entry_id:201112) $\mathcal{A}$ on the [exterior algebra](@entry_id:201164) space. The subspace iteration algorithm can then be interpreted as a simple power method applied to this [induced map](@entry_id:271712) $\mathcal{A}$. The eigenvectors of $\mathcal{A}$ are wedge products of the eigenvectors of $A$, and its eigenvalues are products of the eigenvalues of $A$.

The [dominant eigenvector](@entry_id:148010) of $\mathcal{A}$ is $v_1 \wedge \dots \wedge v_m$, corresponding to the dominant invariant subspace of $A$. The associated eigenvalue is $\prod_{i=1}^m \lambda_i$. The second-largest eigenvalue of $\mathcal{A}$ (in magnitude) corresponds to the [wedge product](@entry_id:147029) $v_1 \wedge \dots \wedge v_{m-1} \wedge v_{m+1}$, with eigenvalue $\lambda_1 \cdots \lambda_{m-1} \lambda_{m+1}$. The convergence rate of the [power method](@entry_id:148021) is the ratio of the magnitudes of the second-dominant to the dominant eigenvalue, which is precisely:

$\rho = \frac{|\lambda_1 \cdots \lambda_{m-1} \lambda_{m+1}|}{|\lambda_1 \cdots \lambda_m|} = \frac{|\lambda_{m+1}|}{|\lambda_m|}$

This abstract perspective provides a profound justification for why the method works as it does, confirming that the convergence of the entire subspace is governed by the separation of eigenvalues at the boundary of the desired set. 

#### The Complicated Case: Non-Normal Matrices

When $A$ is non-Hermitian, and particularly when it is **non-normal** ($A A^* \neq A^* A$), the situation becomes far more complex. The eigenvectors of a [non-normal matrix](@entry_id:175080) may not be orthogonal and can be nearly linearly dependent. This has profound consequences for [iterative methods](@entry_id:139472).

For a diagonalizable [non-normal matrix](@entry_id:175080), a convergence bound similar to the Hermitian case can be derived, but it includes a crucial, often large, factor related to the conditioning of the [eigenvector basis](@entry_id:163721) $V$ :

$\|\tan \Theta_k\|_2 \le \kappa_2(V)^2 \left( \frac{|\lambda_{m+1}|}{|\lambda_m|} \right)^k \|\tan \Theta_0\|_2$

The term $\kappa_2(V)^2$ can be very large if the eigenvectors are nearly parallel. While the *asymptotic* rate is still governed by the eigenvalue ratio, this pre-factor can delay the onset of convergence significantly.

This delay is a symptom of a broader phenomenon related to the **[pseudospectrum](@entry_id:138878)** of [non-normal matrices](@entry_id:137153). The pseudospectrum, $\Lambda_\varepsilon(A)$, is the set of complex numbers $z$ for which the [resolvent norm](@entry_id:754284) $\|(zI-A)^{-1}\|_2$ is large. A large [pseudospectrum](@entry_id:138878) indicates that small perturbations to $A$ can cause large shifts in its eigenvalues. It is also associated with **transient amplification**, where $\|A^k\|$ can grow substantially before it begins to decay according to the [spectral radius](@entry_id:138984). In subspace iteration, this transient behavior can cause the [principal angles](@entry_id:201254) between the iterated and true subspaces to increase or stagnate for many iterations, even when the eigenvalues themselves are well-separated. This makes convergence non-monotonic and unpredictable. 

For non-Hermitian problems, the standard Rayleigh-Ritz procedure is often inadequate. Left and right eigenvectors are distinct, and a more robust approach is to use a **two-sided projection** method. This is a Petrov-Galerkin method where the trial subspace $\mathcal{Q}_k$ approximates the right [invariant subspace](@entry_id:137024) (of $A$) and a separate test subspace $\mathcal{P}_k$ approximates the left [invariant subspace](@entry_id:137024) (of $A^*$). This leads to the approximation of **bi-orthogonal Ritz pairs**, which better capture the underlying non-orthogonal eigenstructure and can stabilize convergence. 

### Practical Considerations and Refinements

#### Handling Eigenvalue Clusters and Choosing the Block Size

One of the most critical parameters in subspace iteration is the **block size**, $p$. A fundamental rule is that to find an $m$-dimensional invariant subspace, the block size must be at least $m$ ($p \ge m$). If $p  m$, the method can at best find the dominant $p$-dimensional subspace, and it will fail to capture the full target space. 

The choice of $p$ is intimately linked to the distribution of eigenvalues. As we have seen, the convergence rate depends on the spectral gap at the boundary of the block, $|\lambda_{p+1}/\lambda_p|$. If the eigenvalues we wish to compute form a tight **cluster**, for instance $\lambda_m \approx \lambda_{m+1}$, then choosing $p=m$ would result in a ratio close to $1$, leading to stagnation. To overcome this, one must "oversample" by choosing a block size $p$ that is larger than the cluster size, such that a significant spectral gap exists between $\lambda_p$ and $\lambda_{p+1}$. This ensures that the entire clustered invariant subspace is captured effectively before being separated from the rest of the spectrum. 

This principle extends to cases where eigenvalues have multiplicities or the matrix is **defective** (i.e., does not have a full set of [linearly independent](@entry_id:148207) eigenvectors). Subspace iteration does not inherently distinguish individual eigenvectors within a cluster. Instead, it converges to the entire **[invariant subspace](@entry_id:137024)** associated with the cluster. For a [defective matrix](@entry_id:153580), the target is the **generalized [eigenspace](@entry_id:150590)**, which includes Jordan chains, and its dimension is the sum of the *algebraic* multiplicities of the eigenvalues in the cluster. Subspace iteration, when properly configured with a sufficiently large block size, is capable of converging to this generalized [invariant subspace](@entry_id:137024). 

#### Computational Cost and Trade-offs

The choice of block size $p$ involves a critical trade-off between convergence speed and computational cost per iteration. The primary costs in a [typical subspace](@entry_id:138088) iteration with Rayleigh-Ritz extraction are :
1.  **Matrix-vector products:** Computing $Z_{k+1} = A Q_k$ requires $p$ matrix-vector products. For a sparse matrix $A$ with $z$ non-zero entries, this costs $O(zp)$.
2.  **Orthonormalization:** Computing the QR factorization of the $n \times p$ matrix $Z_{k+1}$ costs approximately $O(np^2)$ using methods like Modified Gram-Schmidt.
3.  **Rayleigh-Ritz step:** Forming the $p \times p$ matrix $T_k = Q_k^* A Q_k$ and solving its eigenproblem costs $O(np^2 + p^3)$.

The total cost per iteration is dominated by the [orthonormalization](@entry_id:140791) and projection steps, scaling roughly as $O(np^2)$. Increasing $p$ improves the convergence factor, thereby reducing the number of iterations required. However, the cost of each iteration grows quadratically with $p$. The optimal strategy involves choosing a block size $p$ that is just large enough to clear any significant eigenvalue clusters, balancing the benefit of faster convergence against the rapidly increasing per-iteration workload. 

#### Stopping Criteria

An iterative method is only practical if we know when to stop. A robust stopping criterion should be based on a computable quantity that reliably indicates the accuracy of the current solution. The **residual** of a Ritz pair, $r_j = A u_j - \theta_j u_j$, is such a quantity. A small [residual norm](@entry_id:136782) $\|r_j\|_2$ indicates that $(\theta_j, u_j)$ is close to being an exact eigenpair.

For subspace accuracy, we are interested in the error of the entire subspace $\mathcal{Q}_k = \operatorname{range}(U)$, measured by the [principal angles](@entry_id:201254). The theoretical link between the residuals and the subspace error is provided by the **Davis-Kahan $\sin\Theta$ theorem**. For a Hermitian matrix with a [spectral gap](@entry_id:144877) $\delta$ separating the target eigenvalues from the rest, this theorem provides a bound of the form:

$\|\sin\Theta(\mathcal{Q}_k, \mathcal{U})\|_F \le \frac{\|R\|_F}{\delta}$

where $\Theta$ is the matrix of [principal angles](@entry_id:201254), $R = AU - U\Theta$ is the matrix whose columns are the residuals $r_j$, and $\|\cdot\|_F$ denotes the Frobenius norm. 

This powerful result gives us a practical stopping criterion. If we desire an accuracy where the sine of the largest principal angle is no more than a tolerance $\tau$, we can enforce the more stringent condition on the computable upper bound:

$\frac{\|R\|_F}{\delta} \le \tau \implies \|R\|_F \le \tau \delta$

The iteration can be terminated once the Frobenius norm of the residual matrix falls below this threshold. For example, if a target cluster in $[9.5, 10.4]$ is separated from the rest of the spectrum in $[0, 8.2]$ by a gap of $\delta = 1.3$, and the required accuracy tolerance is $\tau = 7.5 \times 10^{-4}$, the iteration can stop when $\|R\|_F \le 1.3 \times (7.5 \times 10^{-4}) = 9.75 \times 10^{-4}$.  For certain structured problems, it is even possible to derive an exact analytical relationship between the [residual norms](@entry_id:754273) and the [principal angles](@entry_id:201254), further solidifying this connection. 