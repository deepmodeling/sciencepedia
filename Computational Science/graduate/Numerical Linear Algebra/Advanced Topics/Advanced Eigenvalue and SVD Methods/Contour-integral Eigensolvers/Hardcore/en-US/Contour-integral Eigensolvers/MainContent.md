## Introduction
Solving [large-scale eigenvalue problems](@entry_id:751145) is a fundamental task in computational science and engineering. While numerous methods exist for finding the extremal eigenvalues (the largest or smallest), many critical applications require computing [interior eigenvalues](@entry_id:750739)—those located within a specific range in the middle of the spectrum. Traditional algorithms are often inefficient for this task, as they may need to compute a vast number of unwanted eigenpairs to reach the region of interest. Contour-integral eigensolvers have emerged as a powerful and elegant paradigm to directly address this challenge, offering a way to "slice" the spectrum and isolate only the desired eigenvalues.

This article provides a thorough exploration of contour-integral methods, guiding you from their theoretical foundations to their practical application. The first chapter, **"Principles and Mechanisms,"** will unpack the core theory, showing how the abstract concept of a spectral projector from complex analysis is realized as a computable rational filter and embedded within the highly effective FEAST algorithm. Next, **"Applications and Interdisciplinary Connections"** will demonstrate the versatility of these solvers, showcasing their impact on diverse fields from [structural engineering](@entry_id:152273) and data science to [high-performance computing](@entry_id:169980) and materials science. Finally, **"Hands-On Practices"** will present targeted problems designed to solidify your understanding of the key design trade-offs and computational considerations. We begin by examining the elegant connection between complex analysis and numerical linear algebra that forms the heart of this method.

## Principles and Mechanisms

This chapter elucidates the core principles and mechanisms underpinning contour-integral eigensolvers. We will begin by establishing the fundamental connection between the abstract concept of a spectral projector, defined via a [contour integral](@entry_id:164714) in the complex plane, and its tangible realization as a rational [matrix function](@entry_id:751754) through numerical quadrature. We will then construct the framework for the Filtered Eigensolver (FEAST) algorithm, an [iterative method](@entry_id:147741) that harnesses this rational filter within a subspace iteration framework. The chapter will subsequently delve into a multi-faceted analysis of convergence, examining both the accuracy of the filter approximation and the convergence rate of the iterative solver itself. Finally, we will explore crucial practical extensions to generalized and non-Hermitian [eigenproblems](@entry_id:748835), alongside a discussion of [numerical stability](@entry_id:146550) in [finite-precision arithmetic](@entry_id:637673).

### From Spectral Projector to Rational Filter

The theoretical foundation of contour-integral methods is the **Riesz-Dunford [functional calculus](@entry_id:138358)**, which allows us to define [functions of a matrix](@entry_id:191388) through complex analysis. For a matrix $A \in \mathbb{C}^{n \times n}$, the **spectral projector** (or Riesz projector) $P_{\Gamma}$ onto the [invariant subspace](@entry_id:137024) associated with the eigenvalues of $A$ enclosed by a simple, closed, [positively oriented contour](@entry_id:166941) $\Gamma$ is given by the integral:

$$
P_{\Gamma} = \frac{1}{2\pi i} \oint_{\Gamma} (z I - A)^{-1} \, dz
$$

Here, $(z I - A)^{-1}$ is the **resolvent** of the matrix $A$. The contour $\Gamma$ must be chosen to lie within the [resolvent set](@entry_id:261708) of $A$, meaning it must not pass through any eigenvalues. By Cauchy's integral formula, this operator has the remarkable property that for any eigenvector $v_j$ with eigenvalue $\lambda_j$, we have $P_{\Gamma}v_j = v_j$ if $\lambda_j$ is inside $\Gamma$, and $P_{\Gamma}v_j = 0$ if $\lambda_j$ is outside $\Gamma$. The projector thus perfectly "filters" the vector space, isolating the desired invariant subspace.

While elegant, the continuous integral defining $P_{\Gamma}$ is not directly computable. The central mechanism of contour-integral eigensolvers is to approximate this integral using a numerical quadrature rule. An $m$-point quadrature rule with nodes $\{z_k\}_{k=1}^m$ on the contour $\Gamma$ and corresponding complex weights $\{\omega_k\}_{k=1}^m$ transforms the integral into a finite sum:

$$
\hat{P}_{\Gamma} = \sum_{k=1}^{m} \omega_k (z_k I - A)^{-1}
$$

This seemingly simple approximation has profound implications. If the matrix $A$ is diagonalizable, say $A = V \Lambda V^{-1}$, we can analyze the action of $\hat{P}_{\Gamma}$ on the eigenvalues. Defining a scalar [rational function](@entry_id:270841) $R(\lambda)$ as:

$$
R(\lambda) = \sum_{k=1}^{m} \frac{\omega_k}{z_k - \lambda}
$$

we find that the operator $\hat{P}_{\Gamma}$ is equivalent to applying this [rational function](@entry_id:270841) to the matrix $A$:

$$
\hat{P}_{\Gamma} = \sum_{k=1}^{m} \omega_k V(z_k I - \Lambda)^{-1}V^{-1} = V \left( \sum_{k=1}^{m} \omega_k (z_k I - \Lambda)^{-1} \right) V^{-1} = V \mathrm{diag}(R(\lambda_j)) V^{-1} = R(A)
$$

This demonstrates that the quadrature approximation of the spectral projector yields a **rational filter**, $R(A)$ . This filter acts on the spectrum of $A$, scaling each eigenvector $v_j$ by the factor $R(\lambda_j)$.

The quality of the eigensolver depends critically on how well $R(\lambda)$ mimics the ideal projector's behavior. Drawing an analogy from signal processing, we desire $R(\lambda)$ to be an ideal **[band-pass filter](@entry_id:271673)**: its value should be close to 1 for eigenvalues $\lambda$ inside $\Gamma$ (the "passband") and close to 0 for eigenvalues outside $\Gamma$ (the "stopband") . This translates to a set of **moment-matching conditions** on the quadrature rule. For $R(\lambda) \approx 1$ inside $\Gamma$ and $R(\lambda) \approx 0$ outside $\Gamma$, the quadrature rule $(z_k, \omega_k)$ must accurately approximate the integrals of powers of $z$, specifically requiring $\sum \omega_k z_k^{-1} \approx 1$ and $\sum \omega_k z_k^j \approx 0$ for other integer powers $j$ .

### A Concrete Example: The Trapezoidal Rule on a Circle

To make these ideas concrete, let us consider a common and particularly effective choice: a circular contour $\Gamma$ of radius $\rho$ centered at $c$, approximated by the $m$-point trapezoidal rule. The contour is parametrized by $z(\theta) = c + \rho \exp(i\theta)$. The remarkable properties of the trapezoidal rule for periodic [analytic functions](@entry_id:139584) lead to a simple and powerful [closed-form expression](@entry_id:267458) for the resulting rational filter. After a derivation involving geometric series and roots-of-unity identities, one finds that the scalar transfer function is  :

$$
R_m(\lambda) = \frac{1}{1 - \left(\frac{\lambda - c}{\rho}\right)^m}
$$

This explicit formula allows for a direct analysis of the filter's performance.
- If an eigenvalue $\lambda$ is inside the circle, then $|\lambda - c|  \rho$, which means the ratio $|\frac{\lambda-c}{\rho}|  1$. As the number of quadrature points $m$ increases, the term $((\lambda-c)/\rho)^m$ rapidly approaches zero, and thus $R_m(\lambda) \to 1$.
- If an eigenvalue $\lambda$ is outside the circle, then $|\lambda-c| > \rho$, and $|\frac{\lambda-c}{\rho}| > 1$. As $m$ increases, the magnitude of $((\lambda-c)/\rho)^m$ grows without bound, causing $R_m(\lambda)$ to rapidly approach 0.

This filter thus exhibits the desired behavior, becoming a near-perfect approximation of the [indicator function](@entry_id:154167) for the interior of the circle as $m$ becomes large.

### The FEAST Algorithm: Subspace Iteration with a Rational Filter

The rational filter $R(A)$ provides a mechanism for separating wanted from unwanted eigenvectors. The **FEAST algorithm** embeds this filter within a subspace iteration framework to efficiently compute the desired invariant subspace.

The algorithm proceeds iteratively. Starting with an initial search subspace spanned by the columns of a matrix $X_0 \in \mathbb{C}^{n \times p}$ (where $p$ is the desired subspace dimension), each iteration consists of two main steps:

1.  **Filtering Step:** Apply the rational filter to the current subspace to generate a new, "purified" subspace:
    $$
    Y_{k+1} = R(A) X_k
    $$
    Computationally, this is the most intensive step. It does not involve forming the matrix $R(A)$ explicitly. Instead, we use its definition as a sum of resolvents:
    $$
    Y_{k+1} = \left( \sum_{j=1}^{m} \omega_j (z_j I - A)^{-1} \right) X_k = \sum_{j=1}^{m} \omega_j \left( (z_j I - A)^{-1} X_k \right)
    $$
    To evaluate each term in the sum, we define an intermediate matrix $Q_j = (z_j I - A)^{-1} X_k$. This is computationally equivalent to solving a block linear system for $Q_j$:
    $$
    (z_j I - A) Q_j = X_k
    $$
    This block system consists of $p$ [linear systems](@entry_id:147850), each of size $n \times n$, sharing the same [coefficient matrix](@entry_id:151473) $(z_j I - A)$ but with different right-hand sides (the columns of $X_k$). After solving for each $Q_j$ corresponding to each quadrature node $z_j$, the filtered subspace is formed by the weighted sum $Y_{k+1} = \sum_{j=1}^m \omega_j Q_j$ .

    A critical feature of this step is its high degree of [parallelism](@entry_id:753103). The block linear systems for each quadrature node $z_j$ are completely independent of one another. Furthermore, for a given node $z_j$, the $p$ [linear systems](@entry_id:147850) corresponding to the columns of the right-hand side are also independent. This means the workload is **[embarrassingly parallel](@entry_id:146258)**, both across the $m$ quadrature nodes and across the $p$ columns of the search subspace. This structure allows contour-integral eigensolvers to leverage modern parallel computing architectures to a very high degree .

2.  **Subspace Extraction Step:** The filtered subspace $Y_{k+1}$ is now a much better approximation of the target invariant subspace. The next step is to extract the best possible estimates for the eigenpairs from this subspace. This is typically achieved via a **Rayleigh-Ritz projection**. First, an [orthonormal basis](@entry_id:147779) for the space spanned by $Y_{k+1}$ is computed, let's call it $X_{k+1}$. Then, the original matrix $A$ is projected onto this basis, forming a small $p \times p$ matrix $A_{\mathrm{proj}} = X_{k+1}^* A X_{k+1}$. The eigenpairs of this small projected matrix (the Ritz pairs) provide the updated approximations to the desired eigenpairs of the large matrix $A$. The Ritz vectors are then used to form the search subspace for the next iteration.

These two steps—filtering and projection—are repeated until a desired level of accuracy is reached.

### Convergence Analysis

The convergence of the FEAST algorithm is a two-level phenomenon. We must consider both the convergence of the rational filter $R(\lambda)$ to the ideal [indicator function](@entry_id:154167) as the number of quadrature points $m$ increases, and the convergence of the subspace iteration for a fixed filter $R(\lambda)$.

#### Convergence of the Quadrature Approximation

The use of the trapezoidal rule for approximating integrals of [periodic functions](@entry_id:139337) is known to yield **[exponential convergence](@entry_id:142080)**, provided the integrand is analytic in a strip around the real axis in the complex plane. For the integral defining our projector, the integrand, as a function of the contour parameter $\theta$, is $g(\theta) = (z(\theta)I-A)^{-1}z'(\theta)$. Assuming a smooth [parametrization](@entry_id:272587) $z(\theta)$, the only singularities of $g(\theta)$ occur at complex values of $\theta$ for which $z(\theta)$ coincides with an eigenvalue of $A$.

The rate of convergence of the [quadrature error](@entry_id:753905) $|R(\lambda) - \chi_{\Gamma}(\lambda)|$ is of the order $\mathcal{O}(e^{-\alpha m})$, where $m$ is the number of quadrature points and the rate constant $\alpha$ is determined by the width of the strip of [analyticity](@entry_id:140716), which is in turn dictated by the minimal imaginary part of the complex $\theta$ values that map to an eigenvalue. Essentially, the error depends on the "distance" from the contour $\Gamma$ to the nearest eigenvalue. If an eigenvalue is very close to $\Gamma$, the convergence of the quadrature will be slow. This provides a key insight for practical applications: one can improve the filter's performance (i.e., increase the convergence rate constant) by judiciously **shaping the contour** $\Gamma$. For instance, instead of a circle, one might use an ellipse to move the contour further away from known unwanted eigenvalues while still enclosing the target region, thereby improving the filter's attenuation in the stopband for the same number of quadrature points  .

#### Convergence of the Subspace Iteration

For a fixed filter $R(A)$ (i.e., for a fixed [quadrature rule](@entry_id:175061)), the FEAST algorithm is a form of subspace iteration with the iteration operator $R(A)$. The convergence of subspace iteration is governed by the separation of the eigenvalues of the iteration operator. The eigenvalues of $R(A)$ are simply $R(\lambda_j)$ for each eigenvalue $\lambda_j$ of $A$. The filter is designed such that $|R(\lambda_j)| \approx 1$ for eigenvalues inside the contour (the "wanted" eigenvalues) and $|R(\lambda_j)| \approx 0$ for eigenvalues outside (the "unwanted" eigenvalues).

The asymptotic [linear convergence](@entry_id:163614) factor of the subspace iteration is determined by the ratio of the largest magnitude of the filter on the unwanted spectrum to the smallest magnitude on the wanted spectrum. Let $\alpha_{\mathrm{in}} = \min_{\lambda \in \mathrm{int}(\Gamma)} |R(\lambda)|$ and $\alpha_{\mathrm{out}} = \max_{\lambda \notin \mathrm{int}(\Gamma)} |R(\lambda)|$. The convergence factor $\rho$ that governs the reduction of the unwanted components in the search subspace at each iteration is given by :

$$
\rho = \frac{\alpha_{\mathrm{out}}}{\alpha_{\mathrm{in}}}
$$

A smaller ratio $\rho$ implies faster convergence. This directly connects the quality of the rational filter to the speed of the iterative solver. Using our concrete example of the unit circle contour with the $N$-point trapezoidal rule to separate eigenvalues with $|\lambda| \le \rho_0  1$ from those with $|\lambda| \ge \eta > 1$, this convergence factor can be explicitly bounded by :

$$
\rho \le \frac{1 + \rho_0^N}{\eta^N - 1}
$$

This bound shows that convergence can be accelerated exponentially by increasing the number of quadrature points $N$ or by improving the separation between the wanted and unwanted eigenvalues (i.e., increasing $\eta$ and decreasing $\rho_0$).

#### Practical Stopping Criteria

Since FEAST is an iterative algorithm, a robust set of stopping criteria is essential. Terminating too early may yield incomplete or inaccurate results, while iterating too long is inefficient. A comprehensive criterion for convergence should simultaneously verify three conditions :
1.  **Accuracy of Ritz Pairs:** The residuals of the computed Ritz pairs, $\|A\hat{x}_i - \hat{\lambda}_i B \hat{x}_i\|$, must be below a specified tolerance. This ensures the computed pairs are indeed good approximations to true eigenpairs.
2.  **Stability of the Subspace:** The change in the search subspace between consecutive iterations must be small. This indicates that the iterative process has stabilized and is no longer discovering significant new directions.
3.  **Stability of the Spectrum:** The number of eigenvalues found within the target contour must be stable across several iterations. This helps to ensure that all eigenvalues in the region have been found and guards against spurious eigenvalues that may appear and disappear in early iterations.

### Extensions and Practical Considerations

The basic principles described above can be extended to a wider class of problems and must be considered in the context of [finite-precision arithmetic](@entry_id:637673).

#### Generalized Eigenproblems

The method is readily extended to the [generalized eigenvalue problem](@entry_id:151614) $Av = \lambda Bv$, where $A$ and $B$ are Hermitian and $B$ is positive definite. The spectral projector takes the form:

$$
P = \frac{1}{2\pi i} \oint_{\Gamma} (z B - A)^{-1} B \, dz
$$

Consequently, the rational filter becomes $R(A,B) = \sum_k \omega_k (z_k B - A)^{-1} B$, and the linear systems to be solved in the filtering step are $(z_k B - A) Y_k = B X$  . For real symmetric matrices $A$ and $B$, if the contour and quadrature rule are chosen to be symmetric with respect to the real axis (i.e., nodes and weights appear in conjugate pairs), the imaginary parts of the computation cancel out, ensuring that if the initial subspace is real, the filtered subspace remains real throughout the iteration .

#### Non-Hermitian Problems

For non-Hermitian matrices, the concepts of [left and right eigenvectors](@entry_id:173562) and [invariant subspaces](@entry_id:152829) become distinct. A **two-sided** or **bi-orthogonal** version of the FEAST algorithm is required. This involves simultaneously iterating on two subspaces: a right subspace $V_k$ for approximating the right [invariant subspace](@entry_id:137024), and a left subspace $W_k$ for the left [invariant subspace](@entry_id:137024). The right subspace is filtered using $R(A)$, while the left subspace is filtered using $R(A^*)$, which corresponds to a different quadrature rule. Instead of a Rayleigh-Ritz projection, a **Petrov-Galerkin projection** is used, and the bases are updated while maintaining a **[bi-orthogonality](@entry_id:175698)** condition, $W_{k+1}^* V_{k+1} = I$ .

#### Numerical Stability and Finite Precision

A crucial practical issue arises from the fact that the quadrature nodes $z_k$ on the contour $\Gamma$ may lie close to eigenvalues of $A$. When $z_k$ is close to an eigenvalue $\lambda_j$, the matrix $(z_k I - A)$ becomes nearly singular, and the corresponding linear system is ill-conditioned. In [finite-precision arithmetic](@entry_id:637673), solving such a system can lead to large forward errors in the computed solution.

The relative [forward error](@entry_id:168661) in the solution of $(z_k I - A)Y_k = Q$ is bounded by a term proportional to the condition number $\kappa(z_k I - A) = \|z_k I - A\|_2 \|(z_k I - A)^{-1}\|_2$. Since $A$ is Hermitian, $\|(z_k I - A)^{-1}\|_2 = 1/\mathrm{dist}(z_k, \Lambda(A))$. Thus, the error grows as the contour gets closer to the spectrum. By establishing a desired tolerance on the [forward error](@entry_id:168661), it is possible to work backward and derive a minimum "safe margin" $\delta_{\mathrm{safe}}$ that the contour must maintain from the spectrum to guarantee numerical stability. For a typical problem setup, this safe distance might be on the order of $10^{-5}$ or $10^{-4}$ . This analysis highlights the delicate balance in choosing a contour: it must be close enough to the target eigenvalues to achieve good separation from unwanted ones, but far enough to maintain numerical stability during the linear solves.