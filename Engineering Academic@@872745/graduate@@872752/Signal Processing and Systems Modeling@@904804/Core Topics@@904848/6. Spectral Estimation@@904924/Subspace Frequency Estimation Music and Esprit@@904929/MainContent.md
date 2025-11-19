## Introduction
Subspace-based methods represent a significant leap forward in frequency and direction-of-arrival estimation, offering "high-resolution" capabilities that can surpass the fundamental limits of classical techniques like the Fourier transform. While traditional methods analyze the signal's spectrum directly, subspace algorithms leverage the underlying algebraic structure of the signal model, providing a more refined and powerful approach to [parameter estimation](@entry_id:139349). This article addresses the knowledge gap between basic [spectral analysis](@entry_id:143718) and these advanced techniques, guiding the reader from foundational theory to state-of-the-art applications. It provides a structured journey into the world of high-resolution estimation, revealing how geometric insights can solve complex signal processing problems.

The following chapters are designed to build this expertise systematically. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, establishing the core signal model and deriving the two cornerstone algorithms: MUSIC and ESPRIT. It explains how [eigendecomposition](@entry_id:181333) partitions data into [signal and noise](@entry_id:635372) subspaces and how each algorithm uniquely exploits this structure. The second chapter, "Applications and Interdisciplinary Connections," moves from theory to practice, exploring how these methods are adapted to handle real-world complexities such as coherent multipath, wideband signals, and sensor array errors, while also touching on modern extensions like sparse recovery and Bayesian frameworks. Finally, "Hands-On Practices" offers a set of curated problems to solidify understanding and build practical skills in applying and analyzing these powerful estimation tools.

## Principles and Mechanisms

Subspace-based methods for frequency estimation represent a paradigm shift from classical Fourier-based techniques. Instead of relying on spectral analysis of the data directly, these high-resolution methods leverage the underlying algebraic structure of the signal model, as captured by the second-[order statistics](@entry_id:266649) of the data. By performing an [eigendecomposition](@entry_id:181333) of the [data covariance](@entry_id:748192) matrix, we can separate the observation space into two orthogonal subspaces: one containing the signals of interest and another containing only noise. The geometric properties of these subspaces are then exploited to estimate the signal parameters with a precision that can far exceed the limits of classical [spectral analysis](@entry_id:143718). This chapter delineates the fundamental principles and mechanisms underpinning these powerful techniques, focusing on two canonical algorithms: MUSIC (Multiple Signal Classification) and ESPRIT (Estimation of Signal Parameters via Rotational Invariance Techniques).

### The Fundamental Signal Model

The efficacy of subspace methods is predicated on a well-defined mathematical model of the observed data. We begin by establishing this model, which serves as the foundation for all subsequent developments.

#### The General Model for Array Processing

Consider an array of $M$ sensors receiving signals from $K$ [far-field](@entry_id:269288), narrowband sources. The vector of signals received by the array at a discrete time instant $n$, known as a **snapshot**, can be modeled as a linear superposition of the source signals corrupted by [additive noise](@entry_id:194447). This is expressed as:

$x[n] = A(\boldsymbol{\theta})s[n] + w[n]$

Here, $x[n] \in \mathbb{C}^{M}$ is the snapshot vector, where each element represents the complex baseband signal at a sensor. The vector $s[n] \in \mathbb{C}^{K}$ contains the complex baseband waveforms of the $K$ sources at time $n$. The matrix $A(\boldsymbol{\theta}) \in \mathbb{C}^{M \times K}$ is the **array manifold matrix** (or steering matrix), which encapsulates the geometric and propagation characteristics of the array-source system. Its columns are the **steering vectors** $a(\theta_k)$ corresponding to each source's direction of arrival (DOA) $\theta_k$. Finally, $w[n] \in \mathbb{C}^{M}$ is the [additive noise](@entry_id:194447) vector.

For subspace separation to be possible, we rely on a set of standard statistical assumptions [@problem_id:2908498]:
1.  The source signals $s[n]$ are modeled as zero-mean, [wide-sense stationary](@entry_id:144146) (WSS) [random processes](@entry_id:268487). They are assumed to be **mutually uncorrelated**, meaning the source covariance matrix $R_s = \mathbb{E}\{s[n]s[n]^H\}$ is diagonal with positive entries representing the power of each source.
2.  The noise $w[n]$ is modeled as a zero-mean, WSS random process. It is assumed to be **spatially white**, implying its covariance is $R_w = \mathbb{E}\{w[n]w[n]^H\} = \sigma^2 I_M$, where $\sigma^2$ is the noise power at each sensor and $I_M$ is the $M \times M$ identity matrix. The noise is also typically assumed to be temporally white.
3.  The source signals and noise are uncorrelated, i.e., $\mathbb{E}\{s[n]w[m]^H\} = \mathbf{0}$ for all $n, m$.

#### The ULA Manifold and Spatial Frequency

A common and illustrative example is the **Uniform Linear Array (ULA)**, where sensors are placed at regular intervals along a line. Let the inter-element spacing be $d$. For a narrowband plane wave of wavelength $\lambda$ arriving from a direction $\theta$ (measured from broadside, i.e., perpendicular to the array axis), the signal arrives at each sensor with a progressive phase shift. If we use the first sensor as the phase reference, the [phase delay](@entry_id:186355) at the $m$-th sensor (for $m=1, \dots, M$) relative to the first is due to the [path difference](@entry_id:201533) $(m-1)d \sin\theta$. This results in a phase shift of $-2\pi (m-1)d \sin\theta / \lambda$.

The steering vector $a(\theta) \in \mathbb{C}^{M}$ for a ULA is thus given by [@problem_id:2908498]:
$a(\theta) = \begin{pmatrix} 1 \\ \exp(-j \frac{2\pi d}{\lambda} \sin\theta) \\ \vdots \\ \exp(-j (M-1) \frac{2\pi d}{\lambda} \sin\theta) \end{pmatrix}$

This structure can be simplified by introducing the concept of **[spatial frequency](@entry_id:270500)**. The spatial frequency, often denoted $u$, is defined as the phase progression per unit of sensor index, normalized by the inter-element phase shift:

$u = \frac{2\pi d}{\lambda} \sin\theta$

Using this definition, the $m$-th element of the steering vector becomes simply $\exp(-j(m-1)u)$, and the steering vector is $a(u) = [1, e^{-ju}, \dots, e^{-j(M-1)u}]^T$. This reveals a crucial insight: the steering vector of a ULA has a **Vandermonde structure**. This structure is not unique to [array processing](@entry_id:200868); it arises identically in the problem of estimating the frequencies of superimposed complex exponentials in a time series [@problem_id:2908553]. An $M$-point snapshot of a time signal $x(t) = \sum_{k=1}^K \alpha_k \exp(j\omega_k t)$ has a signal component that lies in the span of Vandermonde vectors with nodes $e^{j\omega_k}$. This deep analogy allows concepts to be transferred between the spatial (DOA) and temporal (frequency) domains.

A critical aspect of the mapping from physical angle $\theta$ to [spatial frequency](@entry_id:270500) $u$ is uniqueness. The range of physical angles is $\theta \in [-\pi/2, \pi/2]$, which corresponds to $\sin\theta \in [-1, 1]$. The visible range of spatial frequencies is therefore $u \in [-2\pi d/\lambda, 2\pi d/\lambda]$. Since the [complex exponential function](@entry_id:169796) $e^{-ju}$ is periodic with period $2\pi$, if the width of this visible range ($4\pi d/\lambda$) exceeds $2\pi$, distinct physical angles can map to indistinguishable steering vectors. This phenomenon is called **[spatial aliasing](@entry_id:275674)**. To avoid it, we must satisfy the condition $2d/\lambda \le 1$, or $d \le \lambda/2$. For the critical spacing $d = \lambda/2$, the spatial frequency simplifies to $u = \pi \sin\theta$, and the physical range $\theta \in [-\pi/2, \pi/2]$ maps uniquely to the [spatial frequency](@entry_id:270500) range $u \in [-\pi, \pi]$. The inverse mapping is then simply $\theta(u) = \arcsin(u/\pi)$ [@problem_id:2908543].

### The Covariance Matrix and Its Subspace Structure

The foundation of subspace methods lies not in the signal snapshots themselves, but in their second-[order statistics](@entry_id:266649), encapsulated by the [data covariance](@entry_id:748192) matrix.

#### The Ensemble Covariance Matrix

The **ensemble covariance matrix** is the expectation of the outer product of the snapshot vector with its conjugate transpose:

$R_x = \mathbb{E}\{x[n]x[n]^H\}$

Substituting the signal model $x[n] = A s[n] + w[n]$ and using the statistical assumptions of uncorrelated signals and noise, we get:

$R_x = \mathbb{E}\{(A s[n] + w[n])(A s[n] + w[n])^H\} = A \mathbb{E}\{s[n]s[n]^H\} A^H + \mathbb{E}\{w[n]w[n]^H\}$
$R_x = A R_s A^H + \sigma^2 I_M$

This equation is central to all subspace methods [@problem_id:2908474]. It decomposes the [data covariance](@entry_id:748192) into two components: a **signal covariance matrix**, $R_{sig} = A R_s A^H$, and a **noise covariance matrix**, $R_w = \sigma^2 I_M$.

#### Eigendecomposition and Subspace Separation

The structure of $R_x$ becomes clear through its [eigendecomposition](@entry_id:181333). Assuming there are $K$ uncorrelated sources, the source covariance $R_s$ has rank $K$. Since the array manifold $A$ for distinct DOAs has full column rank (assuming $K  M$ and no aliasing), the signal covariance matrix $R_{sig} = A R_s A^H$ also has rank $K$. This means $R_{sig}$ has $K$ positive eigenvalues and $M-K$ zero eigenvalues.

The eigenvalues of the full [data covariance](@entry_id:748192) $R_x$ are the eigenvalues of $R_{sig}$ shifted by the noise power $\sigma^2$. Therefore, $R_x$ has:
- $K$ **signal eigenvalues** $\lambda_1 \ge \lambda_2 \ge \dots \ge \lambda_K  \sigma^2$. The corresponding eigenvectors span a $K$-dimensional subspace called the **[signal subspace](@entry_id:185227)**.
- $M-K$ **noise eigenvalues** $\lambda_{K+1} = \dots = \lambda_M = \sigma^2$. The corresponding eigenvectors span an $(M-K)$-dimensional subspace called the **noise subspace**.

The column space of the signal covariance matrix $R_{sig}$ is, by construction, the space spanned by the columns of $A$, i.e., the true steering vectors. This means the [signal subspace](@entry_id:185227) is precisely the span of the true steering vectors: $\text{span}\{a(\theta_1), \dots, a(\theta_K)\}$.

A fundamental property of Hermitian matrices is that eigenvectors corresponding to distinct eigenvalues are orthogonal. Here, all signal eigenvectors are orthogonal to all noise eigenvectors. This partitions the entire $M$-dimensional observation space $\mathbb{C}^M$ into two orthogonal subspaces: the [signal subspace](@entry_id:185227) and the noise subspace.

For this elegant separation to be possible, the dimension of the noise subspace must be at least one. This requires $M-K \ge 1$, which leads to the fundamental [identifiability](@entry_id:194150) condition for subspace methods: the number of sources $K$ must be strictly less than the number of sensors $M$ [@problem_id:2908550].

### The MUSIC Algorithm: Exploiting Orthogonality

The MUSIC algorithm was one of the first and is arguably the most famous subspace method. Its operation is based on a direct exploitation of the orthogonality between the [signal and noise](@entry_id:635372) subspaces.

#### The Orthogonality Principle

Since the [signal subspace](@entry_id:185227) is the span of the true steering vectors and is orthogonal to the noise subspace, it follows that every true steering vector must be orthogonal to every vector in the noise subspace [@problem_id:2908474]. Let $E_n$ be an $M \times (M-K)$ matrix whose columns form an orthonormal basis for the noise subspace. The [orthogonality principle](@entry_id:195179) can be stated mathematically as:

$E_n^H a(\theta_k) = \mathbf{0} \quad \text{for } k=1, \dots, K$

This means the true steering vectors lie in the [null space](@entry_id:151476) of the operator $E_n^H$. The MUSIC algorithm's goal is to find which candidate steering vectors $a(\theta)$ satisfy this condition.

#### The MUSIC Pseudospectrum

To find the directions that satisfy the [orthogonality condition](@entry_id:168905), MUSIC evaluates the squared norm of the projection of a candidate steering vector $a(\theta)$ onto the noise subspace. This projection is given by $P_n a(\theta) = E_n E_n^H a(\theta)$. Its squared norm is $\|E_n E_n^H a(\theta)\|_2^2 = a(\theta)^H E_n E_n^H a(\theta)$. This quantity will be zero for a true DOA and non-zero otherwise.

To visualize the results as peaks, the **MUSIC pseudospectrum** is defined as the reciprocal of this projection norm [@problem_id:2908474]:

$P_{\text{MUSIC}}(\theta) = \frac{1}{a(\theta)^H E_n E_n^H a(\theta)}$

By scanning $\theta$ over the entire range of possible angles and plotting $P_{\text{MUSIC}}(\theta)$, we obtain a spectrum that, in the ideal noise-free case, exhibits infinitely sharp peaks at the true DOAs. In practice, with estimated subspaces, the peaks are finite but sharp, and their locations provide the DOA estimates.

#### Theoretical Insight: Root-MUSIC

A deeper analysis reveals an elegant connection between MUSIC and polynomial rooting [@problem_id:2908506]. The denominator of the MUSIC pseudospectrum, $p(\theta) = a(\theta)^H E_n E_n^H a(\theta)$, is a non-negative [trigonometric polynomial](@entry_id:633985). By the Fejér-Riesz theorem, any such polynomial can be factored as the squared magnitude of another polynomial, i.e., $p(\theta) = |B(e^{j\theta})|^2$.

The zeros of $p(\theta)$ occur at the true DOAs. This means the polynomial $B(z)$ must have roots on the unit circle at locations corresponding to the true spatial frequencies, $\{e^{j u_k}\}$. Furthermore, the coefficients of this "annihilating filter" polynomial $B(z)$ form a vector that is orthogonal to all the true signal steering vectors, meaning this coefficient vector must lie in the noise subspace.

This insight gives rise to **Root-MUSIC**, an alternative to the peak-searching procedure. Instead of forming the pseudospectrum, one constructs a polynomial whose roots correspond to the signal frequencies. This avoids the [grid search](@entry_id:636526) of spectral MUSIC and can offer higher accuracy.

### The ESPRIT Algorithm: Exploiting Rotational Invariance

ESPRIT offers a different approach that avoids the computationally intensive spectral search of MUSIC. It requires an array with a specific displacement invariance, a property naturally possessed by a ULA.

#### The Principle of Rotational Invariance

ESPRIT works by dividing the main array of $M$ sensors into two identical, overlapping subarrays of size $m  M$. For a ULA, a simple choice is to have the first subarray consist of sensors $1$ to $M-1$ and the second consist of sensors $2$ to $M$. The second subarray is simply a shifted version of the first, with a displacement of $d$.

The signal received by the second subarray is identical to that received by the first, but with an additional phase shift applied to each source component. For the $k$-th source, this phase shift is $\phi_k = \exp(-j u_k)$. This relationship is captured by a diagonal matrix of phase shifts, $\Phi = \text{diag}(e^{-ju_1}, \dots, e^{-ju_K})$.

#### The ESPRIT Formulation

Let $V$ be the $M \times K$ steering matrix whose columns are the true steering vectors. Let $J_1$ and $J_2$ be selection matrices that select the rows corresponding to the first and second subarrays, respectively. The steering matrices for the two subarrays are $V_1 = J_1 V$ and $V_2 = J_2 V$. The shift relationship implies:

$V_2 = V_1 \Phi$

This is the core **[rotational invariance](@entry_id:137644)** equation [@problem_id:2908553]. The same relationship holds for any basis of the [signal subspace](@entry_id:185227). Let $E_s$ be a matrix whose columns are an orthonormal basis for the [signal subspace](@entry_id:185227). Then we can write $E_s = V T$ for some invertible $K \times K$ matrix $T$. The corresponding subarray matrices are $E_{s1} = J_1 E_s$ and $E_{s2} = J_2 E_s$. Substituting, we find:

$E_{s2} = J_2 V T = (J_1 V \Phi) T = (J_1 V T) T^{-1} \Phi T = E_{s1} (T^{-1} \Phi T)$

This shows that there exists a unique $K \times K$ matrix $\Psi = T^{-1} \Phi T$ such that $E_{s2} = E_{s1} \Psi$. The matrix $\Psi$ has the same eigenvalues as $\Phi$, which are the diagonal elements $\{e^{-ju_k}\}$.

The ESPRIT algorithm proceeds by first estimating the [signal subspace](@entry_id:185227) basis $\hat{E}_s$ from the data. It then forms $\hat{E}_{s1}$ and $\hat{E}_{s2}$ and solves the [overdetermined system](@entry_id:150489) of equations $\hat{E}_{s2} \approx \hat{E}_{s1} \Psi$ for the matrix $\Psi$ (e.g., using Total Least Squares). Finally, the eigenvalues of the estimated $\hat{\Psi}$ are computed. The arguments of these eigenvalues directly yield the estimated spatial frequencies $\{\hat{u}_k\}$, from which the DOAs are found.

### Practical Considerations and Extensions

The principles described above apply to an idealized model. In practice, we must confront several challenges, including finite data, correlated sources, and non-ideal noise environments.

#### Sample Covariance and Subspace Leakage

In any real application, the ensemble covariance matrix $R_x$ is unknown and must be estimated from a finite number of snapshots, $N$. The standard estimator is the **[sample covariance matrix](@entry_id:163959)**:

$\hat{R}_x = \frac{1}{N} \sum_{n=1}^{N} x[n]x[n]^H$

For ergodic processes, $\hat{R}_x$ is an unbiased and [consistent estimator](@entry_id:266642) of $R_x$ [@problem_id:2908541]. However, for any finite $N$, $\hat{R}_x$ is a random matrix that can be viewed as a perturbation of the true $R_x$. This perturbation has profound consequences. The [eigendecomposition](@entry_id:181333) of $\hat{R}_x$ yields estimated subspaces, $\hat{E}_s$ and $\hat{E}_n$, which are "rotated" versions of the true subspaces.

This rotation means the estimated noise subspace $\hat{E}_n$ is no longer perfectly orthogonal to the true [signal subspace](@entry_id:185227). A true steering vector $a(\theta_k)$ will now have a small, non-zero projection onto $\hat{E}_n$. This phenomenon is called **subspace leakage** [@problem_id:2908500].

The immediate impact of leakage is that the nulls in the MUSIC spectrum become finite minima, and the peaks become finite maxima. The locations of these peaks become random variables, introducing **variance** to the estimates. Furthermore, the expected peak location may be slightly shifted, causing a **finite-sample bias**. The severity of this leakage, and thus the degradation in performance, is governed by two factors:
1.  **Number of Snapshots ($N$)**: As $N \to \infty$, the perturbation vanishes, leakage disappears, and the estimators become unbiased and have zero variance.
2.  **Eigenvalue Separation**: Matrix [perturbation theory](@entry_id:138766) shows that the amount of subspace rotation is inversely proportional to the gap between the [signal and noise](@entry_id:635372) eigenvalues. This gap is small at low signal-to-noise ratios (SNR) or when sources are very closely spaced in angle, leading to amplified leakage and poorer performance [@problem_id:2908500].

#### The Challenge of Coherent Sources

A critical assumption for the standard subspace model is that the source covariance matrix $R_s$ is full rank, implying uncorrelated sources. In many real-world scenarios, such as multipath propagation, signals arriving from different directions can be fully correlated, or **coherent**. In this case, $R_s$ becomes rank-deficient. If the rank of $R_s$ drops from $K$ to $r  K$, the rank of the signal covariance matrix $A R_s A^H$ also drops to $r$.

This **rank collapse** of the [signal subspace](@entry_id:185227) is catastrophic for standard MUSIC and ESPRIT, as they will identify only $r$ "sources" instead of the true $K$ [@problem_id:2908473].

A powerful remedy for ULAs is **[spatial smoothing](@entry_id:202768)**. This technique involves partitioning the full array of size $M$ into $L = M - m + 1$ overlapping subarrays of a smaller size $m$. A new, "smoothed" covariance matrix is formed by averaging the covariance matrices of these subarrays. This averaging process effectively decorrelates the coherent signals. For **forward-only [spatial smoothing](@entry_id:202768)**, the rank of the smoothed signal covariance matrix is restored to $\min(K, L)$. Thus, to resolve $K$ coherent sources, we need to choose a subarray size $m$ such that the number of subarrays $L = M - m + 1$ is at least $K$, and we must also have $m > K$ to ensure a noise subspace exists in the smoothed $m \times m$ matrix.

**Forward-backward [spatial smoothing](@entry_id:202768)** further enhances this process by also averaging in the contributions from "backward" subarrays. This exploits the [conjugate symmetry](@entry_id:144131) of the ULA manifold and is equivalent to synthesizing a larger virtual array. The rank of the resulting signal covariance becomes $\min(K, 2L-1)$, allowing for the resolution of more coherent sources with the same physical array compared to forward-only smoothing [@problem_id:2908473].

#### The Challenge of Colored Noise

The assumption of spatially [white noise](@entry_id:145248) ($R_w = \sigma^2 I$) is often violated in practice due to directional interference or non-uniform [thermal noise](@entry_id:139193) across sensors. When the noise is **spatially colored**, so $R_w \ne \sigma^2 I$, the simple structure of the [data covariance](@entry_id:748192) is lost: $R_x = A R_s A^H + R_w$. The eigenvectors of $R_x$ no longer neatly partition into [signal and noise](@entry_id:635372) subspaces with the desired properties.

The [standard solution](@entry_id:183092) is **[pre-whitening](@entry_id:185911)** the data. If the noise covariance $R_w$ is known or can be estimated (e.g., from noise-only measurements), we can find a "whitening" matrix $L$ such that $L R_w L^H = I$. A common choice is $L = R_w^{-1/2}$. We then transform the received data as $y[n] = L x[n]$. The covariance of the transformed data becomes:

$R_y = \mathbb{E}\{y[n]y[n]^H\} = L(A R_s A^H + R_w)L^H = (LA)R_s(LA)^H + I$

This transformed problem is once again in the standard form for white noise, but with a new, modified array manifold $A' = LA$.
-   For **MUSIC**, this means the algorithm can proceed, but the search must be performed over the whitened steering vectors $a'(\theta) = L a(\theta)$ [@problem_id:2908490].
-   For **ESPRIT**, the situation is more complex. A general whitening matrix $L$ will destroy the precise [shift-invariance](@entry_id:754776) of the ULA manifold, rendering ESPRIT inapplicable. However, if the noise field is itself spatially stationary (e.g., generated by a process that is WSS across the array), its covariance $R_w$ will be Toeplitz. In this special case, it is possible to use a Toeplitz whitener which preserves the shift structure, allowing ESPRIT to function correctly [@problem_id:2908490].

An alternative to explicit [pre-whitening](@entry_id:185911) is to solve the **generalized eigenvalue problem** for the matrix pair $(R_x, R_w)$. This single step implicitly performs the whitening and subspace separation, and is mathematically equivalent to the two-step process [@problem_id:2908490].

### A Comparative Analysis: MUSIC vs. ESPRIT

While both MUSIC and ESPRIT are canonical subspace methods, they offer a distinct set of trade-offs, making one more suitable than the other depending on the application context [@problem_id:2908475].

-   **Generality and Applicability**: MUSIC is highly flexible and can be applied to any array geometry, as long as its manifold $a(\theta)$ is known. ESPRIT is restricted to arrays with a specific [translational invariance](@entry_id:195885) structure, such as ULAs or pairs of matched arrays.

-   **Computational Cost**: The primary computational burden of MUSIC is its [grid search](@entry_id:636526). For a $d$-dimensional [parameter estimation](@entry_id:139349) problem (e.g., 2D DOA), the search space grows exponentially as $G^d$, where $G$ is the grid size per dimension. This makes MUSIC computationally prohibitive for $d \ge 3$. ESPRIT, being an algebraic method, avoids this search. Its cost is dominated by the initial [eigendecomposition](@entry_id:181333) and solving a small system of equations, which scales polynomially and is far more efficient for multidimensional problems.

-   **Accuracy and Bias**: In its standard implementation, MUSIC is subject to a grid bias if the true DOA lies between grid points. ESPRIT is free from this particular bias. In the asymptotic limit of many snapshots, both methods (specifically, TLS-ESPRIT and ideal-search MUSIC) are statistically efficient, meaning they can achieve the Cramér-Rao Lower Bound on [estimator variance](@entry_id:263211).

-   **Robustness**: ESPRIT's algebraic elegance comes at a cost. Its reliance on a perfect, rigid geometric structure makes it more sensitive to array calibration errors (e.g., sensor position errors), which can break the [rotational invariance](@entry_id:137644) and lead to large biases. MUSIC's spectral search can be more robust, with small calibration errors often leading to graceful degradation (slight peak shifting and broadening) rather than catastrophic failure. In low-snapshot or low-SNR regimes, MUSIC's averaging nature in forming the pseudospectrum can sometimes make it less prone to the variance amplification that can affect ESPRIT's [least-squares](@entry_id:173916) step.

In summary, the choice between MUSIC and ESPRIT depends on a balance of computational budget, required accuracy, array geometry, and the expected quality of array calibration.