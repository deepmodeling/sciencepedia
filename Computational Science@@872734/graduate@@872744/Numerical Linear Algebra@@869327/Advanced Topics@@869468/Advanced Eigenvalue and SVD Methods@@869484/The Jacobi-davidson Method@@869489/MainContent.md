## Introduction
Solving [large-scale eigenvalue problems](@entry_id:751145) is a cornerstone of modern computational science, enabling breakthroughs in fields from quantum mechanics to [structural engineering](@entry_id:152273). While many methods exist, finding specific eigenpairs—especially those hidden in the interior of the spectrum—poses a significant challenge for traditional algorithms. The Jacobi-Davidson (JD) method emerges as a sophisticated and powerful solution, uniquely designed to target desired eigenvalues with high efficiency through a tailored subspace expansion process. This article provides a comprehensive exploration of this advanced iterative technique. The journey begins in the "Principles and Mechanisms" chapter, where we will dissect the core of the method: the celebrated correction equation, its connection to Newton's method, and the role of the Rayleigh-Ritz procedure. From this foundation, the "Applications and Interdisciplinary Connections" chapter will showcase the method's remarkable versatility, demonstrating how it is adapted for generalized and nonlinear [eigenproblems](@entry_id:748835) and applied in diverse fields like nuclear physics and quantum chemistry. Finally, the "Hands-On Practices" section will bridge theory and application with guided challenges, allowing you to implement and test the key concepts discussed.

## Principles and Mechanisms

The Jacobi-Davidson (JD) method is a sophisticated and powerful iterative technique for computing a few eigenpairs of large, sparse matrices. It belongs to the family of subspace methods, which build a low-dimensional search subspace wherein approximations to the desired eigenpairs are sought. The defining characteristic of the Jacobi-Davidson method is its unique approach to expanding this subspace. Unlike Krylov subspace methods that rely on a fixed operator, Jacobi-Davidson computes a "correction" at each step that is tailored to the current [best approximation](@entry_id:268380). This chapter elucidates the core principles and mechanisms of this method, from its fundamental correction equation to advanced strategies for targeting [interior eigenvalues](@entry_id:750739) and ensuring robust convergence.

### The Correction Equation: The Heart of Jacobi-Davidson

At any given step of a subspace iteration, we have a search subspace $\mathcal{V}$ and a current [best approximation](@entry_id:268380) to an eigenpair, denoted as a **Ritz pair** $(\theta, u)$. The vector $u$ is a [unit vector](@entry_id:150575) within $\mathcal{V}$ ($u \in \mathcal{V}$, $\|u\|_2 = 1$), and the scalar $\theta$ is its corresponding **Ritz value**. The quality of this approximation is measured by the **[residual vector](@entry_id:165091)**, $r = A u - \theta u$. If $r = 0$, we have found an exact eigenpair. Otherwise, our goal is to find a correction vector $t$ such that $u+t$ is a better approximation to the true eigenvector. We then expand the search subspace to include this new information, $\mathcal{V}_{\text{new}} = \text{span}\{\mathcal{V}, t\}$.

The ideal correction $t$ would satisfy the eigenvalue equation exactly for some eigenvalue $\lambda$: $A(u+t) = \lambda(u+t)$. Rearranging this and substituting $Au = r + \theta u$ yields:
$$ (A - \lambda I)t = -r - (\lambda-\theta)u $$
This equation is nonlinear in the unknowns $t$ and $\lambda$. The core idea of Jacobi-Davidson is to derive a linear, solvable equation for an effective correction $t$. A key insight is that any correction to the unit vector $u$ should ideally be orthogonal to $u$ itself, $u^*t=0$, to represent a change in direction rather than a simple rescaling. This orthogonality constraint is fundamental to the method.

The Jacobi-Davidson method approximates the ideal equation by assuming $\lambda \approx \theta$ and projecting the equation onto the subspace orthogonal to $u$. This leads to the celebrated **Jacobi-Davidson correction equation**:
$$ (I - u u^{*})(A - \theta I)(I - u u^{*}) t = -r, \quad \text{subject to} \quad u^{*} t = 0 $$
Here, $P_u = (I - u u^{*})$ is the orthogonal projector onto the subspace $\{u\}^{\perp}$.

This equation has several profound properties:

1.  **Enforcement of Orthogonality**: The structure of the equation ensures that any solution $t$ is automatically orthogonal to $u$. The operator on the left, $P_u (A - \theta I) P_u$, maps any vector into the subspace $\{u\}^{\perp}$, and it takes as input a vector that is constrained to be in $\{u\}^{\perp}$ by the right-hand projector. This explicit enforcement of the [orthogonality condition](@entry_id:168905) $u^*t = 0$ is a key distinction from its predecessor, the Davidson method, and is crucial for preventing a form of convergence stagnation [@problem_id:3590373].

2.  **Connection to Newton's Method**: The correction equation is not an ad-hoc formulation; it can be rigorously derived as a stabilized, projected form of Newton's method applied to the constrained nonlinear system for an eigenpair $(v, \mu)$:
    $$ \begin{cases} Av - \mu v = 0 \\ u^*v - 1 = 0 \end{cases} $$
    The second equation, $u^*v - 1 = 0$, is a **[gauge condition](@entry_id:749729)** that fixes the phase and normalization of the eigenvector. Applying Newton's method to this system at the current approximation $(u, \theta)$ leads to a bordered linear system for the correction $(t, \delta\theta)$. By algebraically eliminating the eigenvalue update $\delta\theta$ and exploiting the orthogonality constraint $u^*t=0$, one arrives precisely at the Jacobi-Davidson correction equation. This reveals that the projection mechanism serves to regularize the Newton step, preventing the operator $A-\theta I$ from becoming singular as $\theta$ converges to an eigenvalue $\lambda$ [@problem_id:3590389].

3.  **Consistency**: For the equation to be consistent, the right-hand side, $-r$, must lie in the range of the operator on the left. Since the operator $P_u (A - \theta I) P_u$ maps vectors into $\{u\}^{\perp}$, the residual $r$ must be in $\{u\}^{\perp}$, i.e., $u^*r=0$. This condition is naturally satisfied if the pair $(\theta, u)$ is obtained from a **Rayleigh-Ritz procedure** in the subspace $\mathcal{V}$, where $\theta = u^*Au$ [@problem_id:2900279].

In practice, solving the correction equation exactly at every step is computationally prohibitive, often as difficult as the original problem. The power of JD comes from solving it **inexactly**, typically by applying a few iterations of a preconditioned [iterative method](@entry_id:147741) like GMRES or MINRES. This leads to the concept of an inner-outer iteration, where the "outer" iteration is the subspace expansion and the "inner" iteration is the approximate solve for the correction $t$ [@problem_id:3590401]. The [preconditioner](@entry_id:137537), $M$, is chosen to approximate $A - \sigma I$ for a fixed target shift $\sigma$, providing an approximate inverse that accelerates the inner iterations. A crucial advantage of JD is that the shift $\theta$ in the correction equation can be updated at every outer step to the current best Ritz value, while the more expensive preconditioner $M$ can be kept fixed for many steps [@problem_id:3590401].

### The Role of Ritz Extraction and Error Estimation

The Jacobi-Davidson method relies on a **[projection method](@entry_id:144836)** to extract approximate eigenpairs from the search subspace $\mathcal{V}$. The most common approach is the Rayleigh-Ritz procedure.

#### Rayleigh-Ritz Projection

Given an [orthonormal basis](@entry_id:147779) for the search subspace $\mathcal{V}$, stored in the columns of a matrix $V$, the Rayleigh-Ritz method consists of two steps:
1.  Form the small, dense projected matrix $H = V^{*} A V$.
2.  Solve the [standard eigenvalue problem](@entry_id:755346) for the $k \times k$ matrix $H$: $H y_i = \theta_i y_i$.

The eigenvalues $\theta_i$ of $H$ are the **Ritz values**, and the corresponding **Ritz vectors** are given by $u_i = V y_i$. For Hermitian matrices, the Ritz values serve as optimal approximations to the true eigenvalues given the constraints of the subspace $\mathcal{V}$. The accuracy of these approximations is directly related to how well the subspace $\mathcal{V}$ approximates the true [invariant subspace](@entry_id:137024) $\mathcal{S}$ associated with the desired eigenvalues. This relationship can be quantified. For a Hermitian matrix $A$, the error in the $i$-th Ritz value is bounded in terms of the [principal angles](@entry_id:201254) $\phi_i$ between $\mathcal{V}$ and the target invariant subspace $\mathcal{S}$. A classical result provides the bound:
$$ |\theta_{i} - \lambda_{i}| \le (\lambda_{n} - \lambda_{1}) \sin^{2} \phi_{i} $$
This shows that as the search subspace $\mathcal{V}$ aligns more closely with the true [invariant subspace](@entry_id:137024) $\mathcal{S}$ (i.e., as the [principal angles](@entry_id:201254) $\phi_i$ approach zero), the Ritz values converge to the true eigenvalues [@problem_id:3590390].

#### The Residual as an Error Indicator

The [residual norm](@entry_id:136782) $\|r\|_2 = \|Au - \theta u\|_2$ is the most important practical measure of the quality of a Ritz pair. A small [residual norm](@entry_id:136782) is a strong indicator of an accurate approximation, particularly when the target eigenvalue is well-separated from the rest of the spectrum. For a Hermitian matrix with a simple target eigenpair $(\lambda_*, x_*)$, the angle between the approximate eigenvector $v$ and the true eigenvector $x_*$ can be bounded by the [residual norm](@entry_id:136782) and the spectral separation:
$$ \sin(\angle(v, x_{*})) \le \frac{\|r\|_2}{\text{sep}(\theta)} $$
where $\text{sep}(\theta) = \min_{j \neq *} |\lambda_{j} - \theta|$ measures the separation of the approximate eigenvalue $\theta$ from all other true eigenvalues. This inequality, a variant of the Davis-Kahan theorem, shows that if the residual is small and the eigenvalue is not pathologically close to another, the Ritz vector must be closely aligned with the true eigenvector [@problem_id:3590357]. Furthermore, for any Ritz pair $(\theta, u)$, the residual $r$ is geometrically the component of the vector $Au$ that lies outside the search subspace $\mathcal{V}$ [@problem_id:3590357]. The goal of the subspace expansion is thus to introduce these missing components into $\mathcal{V}$ to improve the approximation.

### Advanced Extraction for Interior Eigenvalues

The standard Rayleigh-Ritz procedure is most effective at finding extremal eigenvalues (e.g., the largest or smallest). For **[interior eigenvalues](@entry_id:750739)**, which are common targets in many applications, a more specialized approach is needed.

#### Harmonic Ritz Extraction

To target eigenvalues near a specific shift $\sigma$, the Jacobi-Davidson method often employs **harmonic Ritz extraction**. This technique implicitly performs a [shift-and-invert](@entry_id:141092) operation without ever forming the [inverse of a matrix](@entry_id:154872). Instead of the standard Galerkin condition $r \perp \mathcal{V}$, it enforces a **Petrov-Galerkin condition** where the residual is made orthogonal to a different [test space](@entry_id:755876), namely $(A-\sigma I)\mathcal{V}$:
$$ ((A-\sigma I)V)^* (A u - \theta u) = 0, \quad \text{for } u \in \mathcal{V} $$
This seemingly complex condition is equivalent to performing a standard Rayleigh-Ritz extraction on the operator $T = (A-\sigma I)^{-1}$. The eigenvalues $\lambda$ of $A$ near the shift $\sigma$ correspond to eigenvalues $\mu = (\lambda - \sigma)^{-1}$ of $T$ that are large in magnitude. The harmonic Ritz procedure thus transforms the difficult problem of finding an interior eigenvalue of $A$ into the much easier problem of finding an extremal eigenvalue of $T$, which is precisely what the Rayleigh-Ritz process excels at [@problem_id:3590353].

#### Refined Ritz Extraction for Clustered Eigenvalues

When eigenvalues are tightly clustered, even the harmonic Ritz method can struggle to produce accurate individual Ritz *vectors*, although it may find the Ritz *values* accurately. The corresponding Ritz vectors can be poorly conditioned mixtures of the true eigenvectors spanning the cluster's invariant subspace. In such cases, a **refined Ritz extraction** is beneficial. For a given (and presumably accurate) harmonic Ritz value $\theta$, this procedure finds the vector $x$ within the current subspace $\mathcal{V}$ that minimizes the [residual norm](@entry_id:136782) $\|(A-\theta I)x\|_2$. This [least-squares problem](@entry_id:164198) often yields a more robust and accurate approximation to the specific eigenvector corresponding to $\theta$. For challenging problems with clustered interior spectra, a powerful strategy is to first compute harmonic Ritz values and then improve their corresponding vectors using a refined extraction [@problem_id:3590366].

### Algorithmic Implementation and Practical Considerations

A complete Jacobi-Davidson iteration integrates these components into a cycle of extraction, correction, and expansion.

#### Computational Cost

The cost of a single outer iteration of JD is the sum of its main components. Assuming a search subspace of dimension $k$, a matrix with $\zeta$ non-zero entries, and an inner solve for the correction equation requiring $k_c$ iterations with a [preconditioner](@entry_id:137537) application cost of $p(n)$, the leading-order cost per outer iteration is typically [@problem_id:3590350]:
$$ \text{Cost} \approx \underbrace{k_c (\zeta + p(n) + \mathcal{O}(n))}_{\text{Correction Eq. Solve}} + \underbrace{\zeta + \mathcal{O}(nk) + \mathcal{O}(k^3)}_{\text{Rayleigh-Ritz  Update}} + \underbrace{\mathcal{O}(nk)}_{\text{Orthonormalization}} $$
This highlights the main computational kernels: sparse matrix-vector products (SpMVs, cost $\zeta$), [preconditioner](@entry_id:137537) applications, dense vector operations (cost $\mathcal{O}(n)$ or $\mathcal{O}(nk)$), and the solution of a small, dense eigenproblem (cost $\mathcal{O}(k^3)$).

#### Restarting Strategies

To manage the memory and computational costs of a growing search subspace, the JD algorithm must be periodically restarted. When the subspace dimension reaches a maximum size $k_{\text{max}}$, it is pruned to a smaller dimension. A simple "thin" restart would retain only the $t$ best Ritz vectors. However, a more effective strategy known as **thick restarting** is commonly used. A thick restart constructs the new subspace not only from the $t$ best Ritz vectors but also from their corresponding residual vectors (or other vectors derived from the correction process).

By retaining the residuals, the algorithm preserves crucial information about the current error and the directions needed for improvement. This is particularly effective for accelerating convergence when computing [clustered eigenvalues](@entry_id:747399), as the discarded information would otherwise have to be slowly rediscovered. While a thick restart increases the memory footprint compared to a thin restart (requiring storage for up to $2t$ vectors instead of $t$), it is a vital technique for ensuring the robust and efficient convergence of the method on difficult problems. Of course, this process requires careful [orthogonalization](@entry_id:149208) of the retained vectors to ensure the new basis is numerically stable [@problem_id:3590381]. For any eigenpair that has already converged, its residual is zero, and the thick restart naturally reduces to a thin restart for that specific pair [@problem_id:3590381].