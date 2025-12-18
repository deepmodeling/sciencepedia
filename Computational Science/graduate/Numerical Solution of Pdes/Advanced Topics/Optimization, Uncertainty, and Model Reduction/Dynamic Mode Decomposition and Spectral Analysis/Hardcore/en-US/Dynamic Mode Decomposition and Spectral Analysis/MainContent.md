## Introduction
The study of dynamical systems, from the turbulent flow of fluids to the spread of diseases, is often challenged by high-dimensionality and inherent nonlinearity. While first-principles models described by [partial differential equations](@entry_id:143134) (PDEs) provide fundamental understanding, extracting comprehensible dynamic features from the vast datasets they produce—or from experimental measurements—remains a significant hurdle. How can we distill complex, evolving spatio-temporal data into a simple, linear model of its core dynamic components? Dynamic Mode Decomposition (DMD) has emerged as a powerful, data-driven answer to this question, providing a systematic framework for identifying [coherent structures](@entry_id:182915) that evolve with a fixed frequency and growth/decay rate.

This article provides a graduate-level exploration of DMD and its role in modern [spectral analysis](@entry_id:143718). We will bridge the gap between abstract [dynamical systems theory](@entry_id:202707) and practical data analysis. The first chapter, **Principles and Mechanisms**, delves into the theoretical heart of DMD, introducing the Koopman operator that linearizes nonlinear dynamics and detailing the standard DMD algorithm. We then transition to practice in the second chapter, **Applications and Interdisciplinary Connections**, showcasing how DMD is applied to analyze fluid flows, classify system behaviors, and reveal patterns in fields as diverse as [epidemiology](@entry_id:141409) and network science. Finally, the **Hands-On Practices** chapter provides a series of focused problems designed to solidify your understanding of the method's strengths and sensitivities in real-world scenarios. By the end, you will have a comprehensive grasp of DMD as both a powerful analytical tool and a practical method for data interrogation.

## Principles and Mechanisms

### The Koopman Operator: A Linear Perspective on Nonlinear Dynamics

The theoretical foundation of Dynamic Mode Decomposition (DMD) lies in the [spectral theory](@entry_id:275351) of dynamical systems, specifically through the lens of the **Koopman operator**. While many dynamical systems, particularly those described by partial differential equations (PDEs), are nonlinear in their state space, the Koopman operator provides a powerful framework for recasting these [nonlinear dynamics](@entry_id:140844) into a linear evolution.

Consider a dynamical system whose state $u$ evolves in a state space $E$ according to a [flow map](@entry_id:276199) $\Phi_t$, such that a state $u_0$ at time $t=0$ evolves to $u(t) = \Phi_t(u_0)$ at time $t$. The [flow map](@entry_id:276199) $\Phi_t$ is typically a nonlinear operator. The key idea, introduced by Bernard Koopman in the context of Hamiltonian mechanics, is to shift focus from the evolution of states to the evolution of **observables**. An observable is simply a function $g: E \to \mathbb{C}$ that extracts a certain quantity of interest from the state. For example, an observable could be the temperature at a specific point in a fluid, the total kinetic energy of a system, or the value of a Fourier coefficient.

The continuous-time **Koopman operator family**, denoted $\{K^t\}_{t \ge 0}$, describes how the values of these [observables](@entry_id:267133) change as the system state evolves. The action of the operator $K^t$ on an observable $g$ is defined by composition with the [flow map](@entry_id:276199):
$$
(K^t g)(u) = g(\Phi_t(u))
$$
This definition states that the value of the new observable $K^t g$ at state $u$ is found by first evolving the state $u$ for a time $t$ to $\Phi_t(u)$, and then evaluating the original observable $g$ at this new state. While the flow $\Phi_t$ acts nonlinearly on states $u$, the Koopman operator $K^t$ acts linearly on the space of observables. That is, for any two [observables](@entry_id:267133) $g_1, g_2$ and scalars $c_1, c_2$, we have $K^t(c_1 g_1 + c_2 g_2) = c_1 K^t g_1 + c_2 K^t g_2$. This "lifting" of nonlinear dynamics into a linear context is the central theoretical contribution of the Koopman framework.

For this framework to be mathematically useful, the family $\{K^t\}$ must possess certain properties. Specifically, we are interested in cases where it forms a **[strongly continuous semigroup](@entry_id:274059)** (or $C_0$-[semigroup](@entry_id:153860)) on a suitable Banach space of [observables](@entry_id:267133) $X$. This requires that for every observable $g \in X$, the map $t \mapsto K^t g$ is continuous. A set of [sufficient conditions](@entry_id:269617) for this property can be established as follows . If we consider a compact, positively [invariant set](@entry_id:276733) $M \subset E$ (meaning $\Phi_t(M) \subseteq M$ for all $t \ge 0$) and assume the [flow map](@entry_id:276199) $(t,u) \mapsto \Phi_t(u)$ is jointly continuous, then $\{K^t\}$ forms a [strongly continuous semigroup](@entry_id:274059) on the Banach space $X=C(M)$ of continuous functions on $M$. The compactness of $M$ is crucial, as it ensures that continuous observables are also uniformly continuous, a property needed to prove the strong continuity condition $\lim_{t \to 0^+} \|K^t g - g\|_\infty = 0$.

The power of this [linear representation](@entry_id:139970) is fully realized through its spectral decomposition. We seek special observables, known as **Koopman eigenfunctions** $g_\omega$, that transform multiplicatively under the action of the Koopman operator. For the infinitesimal generator of the [semigroup](@entry_id:153860), $\mathcal{K}$, these eigenfunctions satisfy an [eigenvalue equation](@entry_id:272921):
$$
\mathcal{K} g_\omega = \omega g_\omega
$$
where $\omega \in \mathbb{C}$ is the corresponding **continuous-time Koopman eigenvalue**. Such an eigenfunction evolves simply in time: $(K^t g_\omega)(u_0) = g_\omega(\Phi_t(u_0)) = g_\omega(u_0) \exp(\omega t)$. The real part of $\omega$ gives the growth or decay rate of the observable's magnitude, and the imaginary part gives its frequency of oscillation. The goal of DMD is to find a data-driven approximation of these key spectral components—the Koopman eigenvalues and their associated **Koopman modes**, which represent the spatial structure of the corresponding eigenfunctions.

### The Connection to Linear PDEs and the Genesis of DMD

To make the abstract Koopman theory concrete, consider a linear PDE, such as the [advection-diffusion equation](@entry_id:144002) on a periodic domain, governed by an operator $L$:
$$
\partial_t u = Lu = (\nu \partial_{xx} - c \partial_x)u
$$
The eigenfunctions of the operator $L$ on the periodic domain $[0, 2\pi]$ are the Fourier basis functions $\varphi_m(x) = \exp(imx)$, and the corresponding eigenvalues are $\lambda_m = -\nu m^2 - icm$. Any solution $u(x,t)$ can be expanded in this basis, with each Fourier coefficient evolving independently as $\hat{u}_m(t) = \hat{u}_m(0)\exp(\lambda_m t)$.

Now, let us connect this to the Koopman framework . Consider the linear [observables](@entry_id:267133) $g_m$ that extract the $m$-th Fourier coefficient from a state $u$:
$$
g_m(u) = \frac{1}{2\pi} \int_0^{2\pi} u(x) \exp(-imx) dx = \hat{u}_m
$$
Let's see how this observable evolves under the Koopman operator $K^t$. We apply $K^t$ to $g_m$ and evaluate at an initial state $u_0$:
$$
(K^t g_m)(u_0) = g_m(u(\cdot, t)) = \hat{u}_m(t) = \hat{u}_m(0) \exp(\lambda_m t) = g_m(u_0) \exp(\lambda_m t)
$$
This holds for any initial state $u_0$. We see that $K^t g_m = \exp(\lambda_m t) g_m$. This is a Koopman [eigenvalue equation](@entry_id:272921). The Fourier coefficient extractors $g_m$ are the Koopman eigenfunctions, and the continuous-time Koopman eigenvalues are precisely the eigenvalues $\lambda_m$ of the underlying PDE operator $L$.

This remarkable result for linear systems provides the fundamental motivation for DMD. DMD is a data-driven numerical method designed to approximate the spectral components of the Koopman operator from a sequence of system snapshots. For a linear system like the one above, DMD aims to recover the eigenvalues $\lambda_m$ and the associated spatial structures (the Koopman modes), which in this case correspond to the Fourier basis functions $\varphi_m(x)$.

### The Standard DMD Algorithm

Let us now formalize the DMD algorithm. Suppose we have a sequence of $n+1$ snapshots of the system state, represented as column vectors $\{x_0, x_1, \dots, x_n\}$, sampled at a uniform time interval $\Delta t$. We arrange these snapshots into two matrices:
$$
X = \begin{pmatrix} |  |   | \\ x_0  x_1  \dots  x_{n-1} \\ |  |   | \end{pmatrix}, \quad X' = \begin{pmatrix} |  |   | \\ x_1  x_2  \dots  x_n \\ |  |   | \end{pmatrix}
$$
The core assumption of DMD is that there exists a linear operator $A$ that approximately advances the state from one time step to the next: $x_{k+1} \approx A x_k$. This implies the matrix relationship $X' \approx AX$. The goal is to find the best-fit [linear operator](@entry_id:136520) $A$. This is typically formulated as a [least-squares problem](@entry_id:164198):
$$
\min_A \|X' - AX\|_F
$$
where $\|\cdot\|_F$ is the Frobenius norm. The solution to this problem is given by $A = X' X^\dagger$, where $X^\dagger$ is the Moore-Penrose pseudoinverse of $X$. The eigenvectors of this matrix $A$ are the **DMD modes**, and its eigenvalues are the **discrete-time DMD eigenvalues**, which we denote by $\lambda_j$.

In practice, the state dimension can be very large, making the computation and [eigendecomposition](@entry_id:181333) of the full matrix $A$ prohibitively expensive. A more efficient, reduced-order version of the algorithm is standard. This procedure relies on the Singular Value Decomposition (SVD) of the snapshot matrix $X = U \Sigma V^*$, where $U$ and $V$ are [unitary matrices](@entry_id:200377) and $\Sigma$ is a [diagonal matrix](@entry_id:637782) of singular values. The algorithm proceeds as follows :

1.  **Compute the SVD** of the input data matrix: $X = U \Sigma V^*$. The SVD may be truncated to a lower rank $r$ to filter noise and reduce computational cost.
2.  **Construct the reduced operator** $\tilde{A}$. Instead of computing the full operator $A$, we compute its projection onto the subspace spanned by the columns of $U$. This low-dimensional operator is given by:
    $$
    \tilde{A} = U^* A U = U^* (X' X^\dagger) U = U^* X' (V \Sigma^{-1} U^*) U = U^* X' V \Sigma^{-1}
    $$
    The matrix $\tilde{A}$ is small (typically $r \times r$) and shares the same non-zero eigenvalues as the full operator $A$.
3.  **Compute the [eigendecomposition](@entry_id:181333)** of the reduced operator: $\tilde{A}W = W\Lambda$, where the columns of $W$ are the eigenvectors of $\tilde{A}$ and $\Lambda$ is a [diagonal matrix](@entry_id:637782) containing the discrete-time DMD eigenvalues $\lambda_j$.
4.  **Reconstruct the high-dimensional DMD modes**. The eigenvectors of the full operator $A$, which are the DMD modes $\phi_j$, can be reconstructed from the eigenvectors $W$ of the reduced operator. From the relationship $\tilde{A}w_j = \lambda_j w_j$, we can show that the corresponding eigenvector of $A$ is $\phi_j = U w_j$ (when $A$ is projected onto the column space of $X$). A more general reconstruction is $\phi_j = X'V\Sigma^{-1}w_j$ . The collection of DMD modes forms the columns of the matrix $\Phi$.

Once the discrete-time eigenvalues $\lambda_j$ are found, the continuous-time eigenvalues $\omega_j$ are recovered using the relationship $\lambda_j = \exp(\omega_j \Delta t)$, which gives:
$$
\omega_j = \frac{\ln(\lambda_j)}{\Delta t}
$$
The real part of $\omega_j$ represents the growth/decay rate of the mode, and the imaginary part represents its angular frequency.

### Interpreting DMD Modes and a Comparison with POD

With the DMD modes $\phi_j$ and eigenvalues $\lambda_j$ computed, the original snapshots can be reconstructed as a [linear combination](@entry_id:155091) of these modes evolving in time. The evolution of the system is approximated as:
$$
x_k \approx \sum_{j=1}^r b_j \phi_j (\lambda_j)^k
$$
where the amplitudes $b_j$ are the coordinates of the initial state $x_0$ in the basis of DMD modes.

A crucial point is the interpretation of DMD modes in contrast to another widely used decomposition technique, **Proper Orthogonal Decomposition (POD)**. POD, also known as Principal Component Analysis (PCA), identifies a set of [orthonormal basis](@entry_id:147779) vectors (POD modes) that are optimal for representing the system's energy or variance. The POD modes are the eigenvectors of the snapshot covariance matrix $C = \frac{1}{n}XX^*$.

The fundamental difference can be summarized as follows :
- **POD** is designed for optimal **[data representation](@entry_id:636977)**. The POD modes form an orthonormal basis that, for any given rank $r$, captures the maximum possible energy (variance) in the data. However, POD modes are static; they do not have a simple temporal evolution associated with them. A single POD mode will generally evolve into a complex combination of all other POD modes.
- **DMD** is designed for optimal **dynamic representation**. Each DMD mode evolves with a single, well-defined frequency and growth/decay rate. This makes DMD modes ideal for understanding the underlying dynamics. However, DMD modes are generally not orthogonal, and they are not optimized for energy capture.

In the special case where the data consists of a single spatial structure evolving as a pure exponential in time (i.e., a single Koopman mode), the POD and DMD analyses coincide, yielding the same mode and eigenvalue .

A practical consideration in using DMD modes is their scaling. There is an inherent ambiguity, as one can scale a mode $\phi_j$ by a constant and the corresponding amplitude $b_j$ by its inverse without changing the reconstruction. A physically meaningful convention is to normalize each DMD mode to have unit Euclidean norm, i.e., $\|\phi_j\|_2 = 1$. If the snapshot [vector norm](@entry_id:143228) approximates the physical energy of the system (e.g., the $L^2$ norm), this normalization ensures that the mode $\phi_j$ represents a fundamental spatial pattern of unit energy. The magnitude of the amplitude $|b_j|$ can then be directly interpreted as the contribution of that mode to the total energy of the initial state .

### Advanced Topics and Practical Considerations

Applying DMD to real or numerical data requires an awareness of several practical and theoretical challenges that can affect the accuracy and interpretation of the results.

#### Non-Normal Dynamics and the Pseudospectrum

Many physical systems, especially those involving fluid flows with strong convection, are described by **non-normal** operators. A matrix $A$ is non-normal if it does not commute with its conjugate transpose ($AA^* \neq A^*A$). Unlike [normal matrices](@entry_id:195370), the eigenvectors of [non-normal matrices](@entry_id:137153) are not orthogonal. This has profound consequences for the system's dynamics and its spectral analysis.

A key feature of [non-normal systems](@entry_id:270295) is the possibility of **transient growth**. Even if all eigenvalues of $A$ are inside the unit circle (i.e., the [spectral radius](@entry_id:138984) $\rho(A)  1$), guaranteeing long-term decay, the norm of the state $\|A^k x_0\|$ can grow substantially for a period of time before it eventually decays.

The spectrum (the set of eigenvalues) of a [non-normal matrix](@entry_id:175080) can be a poor predictor of its short-term behavior. A more informative tool is the **$\epsilon$-[pseudospectrum](@entry_id:138878)**, $\Lambda_\epsilon(A)$, defined as the set of complex numbers $z$ that are "almost" eigenvalues :
$$
\Lambda_\epsilon(A) = \{ z \in \mathbb{C} : \|(A-zI)^{-1}\| > 1/\epsilon \}
$$
where $\|\cdot\|$ is the matrix [2-norm](@entry_id:636114). This definition is equivalent to saying that $z$ is in $\Lambda_\epsilon(A)$ if the smallest [singular value](@entry_id:171660) of $(A-zI)$ is less than $\epsilon$. The [pseudospectrum](@entry_id:138878) can be interpreted as the set of points that become eigenvalues of $A$ under some small perturbation of norm less than $\epsilon$. For [non-normal matrices](@entry_id:137153), the pseudospectrum can extend far beyond the actual spectrum.

The connection to transient growth is direct: large resolvent norms $\|(A-zI)^{-1}\|$ near the unit circle are a signature of potential transient growth, a fact formalized by the Kreiss Matrix Theorem. This can be seen from the Cauchy integral formula for [matrix powers](@entry_id:264766), which bounds $\|A^k\|$ in terms of the [resolvent norm](@entry_id:754284) on a contour enclosing the spectrum . When DMD is applied to data from a non-normal system, the computed DMD eigenvalues (which are Ritz values of the underlying operator) can be "spurious", lying within the pseudospectrum but far from any true eigenvalue. This is not an algorithmic failure but a manifestation of the inherent sensitivity of the non-[normal operator](@entry_id:270585).

#### Effects of Numerical Integration

When analyzing data from a [numerical simulation](@entry_id:137087), the snapshots are not generated by the true continuous-time flow, but by a [discrete time](@entry_id:637509)-stepping method. DMD will therefore identify the spectral properties of the *numerical* one-[step operator](@entry_id:199991), not the underlying continuous system.

Consider a system governed by $\dot{u} = Au$, where the eigenvalues of $A$ are $\lambda$. If a numerical integrator like the classical fourth-order Runge-Kutta (RK4) method is used with a time step $\Delta t$, the numerical update is of the form $u_{k+1} = R(A\Delta t) u_k$, where $R(z)$ is the method's **stability function**. For RK4, this function is the fourth-order Taylor expansion of the exponential, $R(z) = 1 + z + z^2/2 + z^3/6 + z^4/24$. The eigenvalues $\mu$ captured by DMD will be the eigenvalues of the numerical [propagator](@entry_id:139558), which, by the [spectral mapping theorem](@entry_id:264489), are given by $\mu = R(\lambda \Delta t)$ . This shows that the numerical scheme can significantly distort the spectrum, and this effect must be considered when interpreting DMD results from simulation data.

#### Sampling Rate and Aliasing

The choice of sampling interval $\Delta t$ is critical. According to the **Nyquist-Shannon sampling theorem**, to uniquely identify a temporal frequency $\omega$, the sampling rate must be sufficiently high. Specifically, the magnitude of the frequency must not exceed the **Nyquist frequency**, $\omega_{Nyquist} = \pi/\Delta t$ .

If a signal contains a frequency $|\omega| > \pi/\Delta t$, it will be **aliased**: the sampled data will be indistinguishable from that of a lower-frequency signal within the principal frequency range $(-\pi/\Delta t, \pi/\Delta t]$. DMD, which reconstructs frequency from the argument of the discrete eigenvalue $\lambda = \exp(i\omega\Delta t)$, will report an aliased frequency $\omega_{DMD}$ that is related to the true frequency by
$$
\omega_{DMD} = \omega + m \frac{2\pi}{\Delta t}
$$
where the integer $m$ is chosen to "fold" the frequency into the principal range. For example, if a true frequency of $\omega=80$ rad/s is sampled with $\Delta t = 0.05$ s, the Nyquist frequency is $20\pi \approx 62.8$ rad/s. The system is undersampled, and DMD will report an aliased frequency of $\omega_{DMD} = 80 - 40\pi \approx -45.7$ rad/s . This highlights the importance of ensuring a sufficiently high sampling rate to avoid misinterpretation of dynamic frequencies.

#### Sensitivity to Noise and Robust Formulations

The standard DMD algorithm, based on a [least-squares solution](@entry_id:152054), is known to be sensitive to [measurement noise](@entry_id:275238). Consider the case where the snapshot matrix $X$ is corrupted by additive i.i.d. Gaussian noise, yielding a measured matrix $\tilde{X} = X+E$. The DMD operator is then estimated as $\tilde{A} = X' \tilde{X}^\dagger$. In the limit of a large number of snapshots, this estimator is biased. This is a classic "[errors-in-variables](@entry_id:635892)" problem in regression. The asymptotic bias is given by $B \approx -\sigma^2 A \Sigma_{xx}^{-1}$, where $\sigma^2$ is the noise variance and $\Sigma_{xx}$ is the [state covariance matrix](@entry_id:200417) . This **[attenuation bias](@entry_id:746571)** systematically shifts the estimated eigenvalues towards the origin, underestimating growth rates.

To address this sensitivity, more robust formulations of DMD have been developed. A prominent example is **Total Least Squares (TLS) DMD**. The TLS formulation acknowledges that noise may be present in both the input data $X$ and the output data $X'$. It seeks to find perturbations $\Delta X$ and $\Delta X'$ and an operator $A$ that minimize the size of the perturbations while satisfying the dynamic constraint exactly:
$$
\min_{A, \Delta X, \Delta X'} \|\begin{bmatrix} \Delta X \\ \Delta X' \end{bmatrix}\|_F \quad \text{subject to} \quad (X'+\Delta X') = A(X+\Delta X)
$$
This problem can be solved elegantly using the SVD of the augmented data matrix $Z = \begin{bmatrix} X \\ X' \end{bmatrix}$ . The SVD provides an [orthonormal basis](@entry_id:147779) for the data, and by truncating the singular values that are primarily associated with noise, a "cleaned" data set can be constructed. The DMD operator is then computed on this denoised data. Specifically, if the SVD of $Z$ is $U \Sigma V^*$, we can approximate the system dynamics from the truncated left [singular matrix](@entry_id:148101) $U_r$ (corresponding to the $r$ largest singular values). By partitioning this matrix into $U_r = \begin{bmatrix} U_X \\ U_{X'} \end{bmatrix}$, the TLS approximation of the system operator $A$ can be shown to be related to these subspaces, yielding eigenvalues that are less biased by noise. This approach provides a more robust estimate of the system dynamics in the presence of noise.