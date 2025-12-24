## Introduction
The relentless pursuit of accuracy in scientific and engineering simulation often leads to high-fidelity models that are computationally prohibitive for many practical tasks. Applications such as design optimization, real-time control, and [uncertainty quantification](@entry_id:138597) demand thousands or even millions of model evaluations, a requirement that traditional complex simulations cannot meet. Reduced-order and surrogate modeling provides a powerful solution to this challenge by creating efficient, accurate approximations that can be queried rapidly. This article offers a comprehensive exploration of this vital field. The first chapter, **Principles and Mechanisms**, delves into the mathematical foundations, explaining how methods like projection and data-driven learning work. The second chapter, **Applications and Interdisciplinary Connections**, showcases the real-world impact of these techniques across diverse domains, from nuclear engineering to astrophysics. Finally, the **Hands-On Practices** section provides an opportunity to apply these concepts, solidifying the reader's understanding and bridging the gap between theory and practice.

## Principles and Mechanisms

Reduced-order and surrogate models are powerful tools designed to replace computationally expensive high-fidelity simulations with efficient, accurate approximations. The primary motivation for their development and use is the creation of models that are fast enough for applications requiring many queries, such as design optimization, real-time control, and [uncertainty quantification](@entry_id:138597), without sacrificing essential physical fidelity. This is achieved through a variety of mathematical techniques that can be broadly categorized into projection-based methods, which simplify the governing equations, and non-intrusive methods, which learn the input-output relationship directly from data. This chapter elucidates the fundamental principles and core mechanisms underpinning these approaches.

### The Foundation of Projection-Based Model Reduction

Projection-based Reduced-Order Models (ROMs) operate on a compelling principle: although the state of a complex physical system (like the neutron flux in a reactor) may be described by a very large number of degrees of freedom, the actual solutions under various operating conditions often lie on or very near a much lower-dimensional manifold within the high-dimensional state space. The goal of projection-based ROM is to identify this low-dimensional subspace and project the governing equations onto it, yielding a small system of equations that is computationally inexpensive to solve.

#### The Offline-Online Computational Strategy

The power of projection-based ROMs lies in their ability to separate the computational workload into two distinct stages: a computationally intensive **offline stage** and a rapid **online stage**. This decomposition is the cornerstone of the method's efficiency .

The **offline stage** is performed once as a pre-computation. It involves generating the low-dimensional subspace and pre-calculating all parameter-independent components of the reduced system. This stage includes:
1.  Running the high-fidelity model for a few well-chosen parameter values to generate "snapshots" of the system's behavior.
2.  Constructing a low-dimensional basis from these snapshots that optimally represents the solution manifold.
3.  Projecting the parameter-independent operators of the high-fidelity model onto this reduced basis to form small, constant matrices.

The **online stage** is performed every time a new solution is desired for a new parameter value. This stage is designed to be extremely fast and involves only a few simple operations:
1.  Evaluating the parameter-dependent scalar coefficients of the model.
2.  Assembling the small, reduced system matrices from the pre-computed offline components.
3.  Solving the small system of equations for the reduced coordinates.

Consider, for example, a discretized system of equations that depends on a parameter vector $\mu$ and has an affine structure, such as the [generalized eigenvalue problem](@entry_id:151614) $\mathbf{A}(\mu) \boldsymbol{\phi}(\mu) = \frac{1}{k(\mu)} \mathbf{F}(\mu) \boldsymbol{\phi}(\mu)$ from neutron diffusion . If the operators can be expressed as $\mathbf{A}(\mu) = \sum_{q=1}^{Q} \theta_q(\mu) \mathbf{A}_q$ and $\mathbf{F}(\mu) = \sum_{q=1}^{Q} \vartheta_q(\mu) \mathbf{F}_q$, the online computational cost for solving the reduced problem of size $r$ is dominated by two terms. First, assembling the reduced matrices, which involves $Q$ scalar-matrix multiplications and additions for matrices of size $r \times r$, scales as $O(Q r^2)$. Second, solving the resulting dense [generalized eigenvalue problem](@entry_id:151614) of size $r \times r$ with a direct solver scales as $O(r^3)$. The total online complexity is therefore $O(Q r^2 + r^3)$. Since both $Q$ and $r$ are typically small, this cost is orders of magnitude lower than solving the original system of size $N$.

#### Projection Methods: Galerkin and Petrov-Galerkin

The mathematical mechanism for reducing the governing equations is projection. Given a high-dimensional state vector $\phi \in \mathbb{R}^N$, we seek an approximation $\phi_r$ in a low-dimensional **trial subspace** spanned by the columns of a [basis matrix](@entry_id:637164) $V \in \mathbb{R}^{N \times r}$, where $r \ll N$. The approximation takes the form $\phi_r = V a$, where $a \in \mathbb{R}^r$ is the vector of reduced coordinates.

Substituting this approximation into a linear system $A\phi = q$ yields a residual, $R = A(Va) - q$, which is generally non-zero. The [projection method](@entry_id:144836) determines the unknown coefficients $a$ by enforcing that this residual be orthogonal to a chosen **test subspace**, spanned by the columns of a [basis matrix](@entry_id:637164) $W \in \mathbb{R}^{N \times r}$. This [orthogonality condition](@entry_id:168905) is expressed as $W^T R = 0$, which leads to the reduced system:
$$ (W^T A V) a = W^T q $$
This is a small linear system of size $r \times r$ for the unknown vector $a$. The choice of the test basis $W$ defines the type of projection .

The most common choice is the **Galerkin projection**, where the test subspace is identical to the trial subspace, i.e., $W = V$. The reduced system becomes:
$$ A_r a = q_r \quad \text{where} \quad A_r = V^T A V \quad \text{and} \quad q_r = V^T q $$
A key property of the Galerkin projection is that it preserves the symmetry of the original operator. If the full-order operator $A$ is symmetric ($A^T = A$), then the reduced operator $A_r$ is also symmetric, since $A_r^T = (V^T A V)^T = V^T A^T V = V^T A V = A_r$.

In a **Petrov-Galerkin projection**, the test subspace is chosen to be different from the trial subspace, $W \neq V$. This added flexibility can be exploited to enforce specific desired properties in the reduced model. For instance, if the full-order operator $A$ is not symmetric in the standard sense but is self-adjoint with respect to a [weighted inner product](@entry_id:163877) defined by a [symmetric positive definite matrix](@entry_id:142181) $G$ (i.e., $A^T G = G A$), a standard Galerkin projection will not yield a symmetric reduced operator. However, by choosing a Petrov-Galerkin projection with the test basis $W = G V$, the resulting reduced operator $A_r = (G V)^T A V = V^T G A V$ becomes symmetric. This is a powerful technique for ensuring the stability and physical consistency of the ROM .

#### Constructing the Basis: Proper Orthogonal Decomposition (POD)

The quality of a projection-based ROM depends critically on the choice of the reduced basis $V$. An effective basis must be able to represent the system's behavior accurately with very few basis vectors. **Proper Orthogonal Decomposition (POD)**, also known as Principal Component Analysis (PCA), is a systematic method for extracting an [optimal basis](@entry_id:752971) from a set of data.

The process begins by collecting a series of solution snapshots, which are solutions of the high-fidelity model at different times or for different parameter values. These $m$ snapshot vectors, each of dimension $N$, are arranged as the columns of a **[snapshot matrix](@entry_id:1131792)** $X \in \mathbb{R}^{N \times m}$ . For example, in a [multigroup diffusion](@entry_id:1128303) problem, each state vector $x^{(j)}$ would be formed by stacking the group-wise flux vectors for a given operating condition $j$.

POD seeks an orthonormal basis that is optimal in the sense that it captures the most "energy" (variance) of the snapshot data, on average, for any given basis size $r$. The solution to this optimization problem is given by the **Singular Value Decomposition (SVD)** of the [snapshot matrix](@entry_id:1131792):
$$ X = U \Sigma V^T $$
Here, $U \in \mathbb{R}^{N \times N}$ is an [orthogonal matrix](@entry_id:137889) whose columns are the [left singular vectors](@entry_id:751233), $\Sigma \in \mathbb{R}^{N \times m}$ is a rectangular [diagonal matrix](@entry_id:637782) of non-negative singular values $\sigma_i$ (ordered by magnitude), and $V \in \mathbb{R}^{m \times m}$ is an [orthogonal matrix](@entry_id:137889) whose columns are the [right singular vectors](@entry_id:754365).

The optimal rank-$r$ POD basis is simply the set of the first $r$ columns of $U$. These vectors, called the **POD modes**, form the [basis matrix](@entry_id:637164) $V$ for our ROM. The singular values quantify the importance of each mode. The squared Frobenius norm of the [snapshot matrix](@entry_id:1131792), $\|X\|_F^2 = \sum_{i=1}^{\min(N,m)} \sigma_i^2$, is proportional to the total energy of the snapshots. The fraction of energy captured by a rank-$r$ basis is given by:
$$ \mathcal{E}(r) = \frac{\sum_{i=1}^r \sigma_i^2}{\sum_{i=1}^{\min(N,m)} \sigma_i^2} $$
A common heuristic for choosing the reduced dimension $r$ is to select the smallest value such that this captured energy exceeds a certain threshold, for example, $\mathcal{E}(r) \ge 0.9999$ .

For problems where the state dimension $N$ is much larger than the number of snapshots $m$, computing the full SVD of $X$ can be prohibitive. The **[method of snapshots](@entry_id:168045)** provides a computationally cheaper alternative by solving the small $m \times m$ eigenvalue problem on the [correlation matrix](@entry_id:262631) $X^T X$. The POD modes can then be recovered from the eigenvectors of this smaller problem, yielding the same basis .

### Advanced Mechanisms for Practical ROMs

While the foundational principles of projection and POD provide a powerful framework, building practical ROMs for complex, nonlinear, and time-dependent systems requires additional machinery.

#### Hyper-reduction for Nonlinear Systems: DEIM

A major challenge in reducing nonlinear models is that even after projection, the nonlinear terms may still depend on the full-dimensional state, destroying the computational advantage of the ROM. For example, in a system with a nonlinear term $f(\phi)$, the reduced system may contain terms like $V^T f(Va)$. Evaluating $f(Va)$ still requires reconstructing the full state vector $Va \in \mathbb{R}^N$ and then evaluating the function $f$, which can be an $O(N)$ operation.

**Hyper-reduction** techniques are designed to overcome this bottleneck. The **Discrete Empirical Interpolation Method (DEIM)** is a prominent [hyper-reduction](@entry_id:163369) method that approximates the nonlinear term by evaluating it at only a small, judiciously chosen set of points . DEIM assumes that the nonlinear outputs $\{f(\phi)\}$ also lie on a [low-dimensional manifold](@entry_id:1127469). It proceeds in two steps:
1.  A POD basis $U \in \mathbb{R}^{N \times m}$ is constructed for the nonlinear term itself from snapshots of $f(\phi)$. The approximation is then sought in the form $f(\phi) \approx U c$.
2.  Instead of a costly Galerkin projection, the coefficients $c \in \mathbb{R}^m$ are found by enforcing interpolation: the approximation must match the true function at $m$ specific "interpolation points."

This leads to the DEIM approximant:
$$ f(\phi) \approx U (P^T U)^{-1} P^T f(\phi) $$
Here, $P \in \mathbb{R}^{N \times m}$ is a sampling matrix that extracts the entries corresponding to the $m$ interpolation points. The matrix $U (P^T U)^{-1}$ is pre-computed offline. During the online stage, one only needs to compute the $m$ entries of the nonlinear term specified by $P^T f(\phi)$, an $O(m)$ operation, instead of the full $N$ entries. For coupled neutronics-thermal-hydraulics problems, this means one might only need to compute temperatures and update cross sections at a few key spatial locations to approximate the feedback effect across the entire core .

#### Rigorous Error Control: A Posteriori Error Estimation

A critical question for any approximation is: how accurate is it? For ROMs to be used in high-consequence applications like [reactor safety analysis](@entry_id:1130678), we need rigorous and computable bounds on the [approximation error](@entry_id:138265). **A posteriori [error estimation](@entry_id:141578)** provides a way to quantify the error of a ROM solution without knowing the true solution.

For [elliptic problems](@entry_id:146817) like the fixed-source neutron diffusion equation, the error of the ROM solution can be bounded by a quantity that depends on the **residual** of the ROM solution. The residual measures how well the approximate solution satisfies the original high-fidelity governing equation. The standard residual-based [error bound](@entry_id:161921) takes the form :
$$ \|u(\mu) - u_N(\mu)\|_V \leq \frac{\|r_\mu\|_{V^*}}{\beta(\mu)} $$
Here, $\|u(\mu) - u_N(\mu)\|_V$ is the error in the appropriate [function space](@entry_id:136890) norm (e.g., the [energy norm](@entry_id:274966)). The two key components of the estimator are:
-   $\|r_\mu\|_{V^*}$: The [dual norm](@entry_id:263611) of the residual functional. This term is computable online and quantifies the magnitude of the error source.
-   $\beta(\mu)$: The **stability constant** (or [coercivity constant](@entry_id:747450)) of the governing operator. This constant is a measure of the operator's well-posedness and is independent of any [particular solution](@entry_id:149080). A larger stability constant implies that a given residual source produces a smaller error, indicating a more stable physical system.

For the [error bound](@entry_id:161921) to be rigorous, one must be able to compute the [residual norm](@entry_id:136782) and a certified lower bound for the stability constant $\beta(\mu)$ efficiently in the online stage. This provides a "certificate" of accuracy for every ROM computation, making the ROM a reliable predictive tool.

### Data-Driven Surrogates for Dynamics and Uncertainty

While projection-based ROMs reduce the complexity of the governing equations, an alternative paradigm, often termed **surrogate modeling**, aims to learn the input-to-output mapping of a system directly from data, often without direct reference to the governing equations. These methods are typically "non-intrusive" as they treat the high-fidelity solver as a black box.

#### Modeling Transient Phenomena: Dynamic Mode Decomposition (DMD)

For time-dependent problems, **Dynamic Mode Decomposition (DMD)** is a powerful data-driven technique for extracting dominant [spatiotemporal patterns](@entry_id:203673) from a sequence of snapshots . Given a time series of state vectors $\{\phi_0, \phi_1, \dots, \phi_m\}$, DMD assumes the underlying dynamics are approximately linear, i.e., $\phi_{t+1} \approx A \phi_t$ for some constant matrix $A$.

The core of the DMD algorithm is to find the best-fit linear operator $A$ that advances the snapshots in time. This is achieved by forming two data matrices, $X_1 = [\phi_0, \dots, \phi_{m-1}]$ and $X_2 = [\phi_1, \dots, \phi_m]$, and solving the [least-squares problem](@entry_id:164198) to minimize $\|X_2 - A X_1\|_F$. The solution is given by $A = X_2 X_1^\dagger$, where $X_1^\dagger$ is the Moore-Penrose [pseudoinverse](@entry_id:140762) of $X_1$.

In practice, to handle [high-dimensional data](@entry_id:138874) and reduce noise, this is done in a reduced-dimensional space. The snapshots in $X_1$ are projected onto their first $r$ POD modes (the columns of $U_r$). The dynamics are then approximated on the low-dimensional coefficients, yielding a small $r \times r$ reduced operator $\tilde{A} = U_r^T X_2 V_r \Sigma_r^{-1}$, where $U_r, \Sigma_r, V_r$ come from the SVD of $X_1$.

The [eigendecomposition](@entry_id:181333) of this small matrix $\tilde{A}$ reveals the core characteristics of the dynamics. The eigenvalues of $\tilde{A}$ approximate the eigenvalues of the full system operator $A$ and indicate the growth/decay rates and frequencies of the dynamic patterns. The eigenvectors of $\tilde{A}$ can be used to construct the corresponding **DMD modes**, which represent the coherent spatial structures that evolve with these specific rates and frequencies .

The remarkable success of DMD, even for highly nonlinear systems, is explained by its connection to **Koopman [operator theory](@entry_id:139990)** . The Koopman operator, $\mathcal{K}$, is an infinite-dimensional [linear operator](@entry_id:136520) that describes the evolution of observable functions of the state. While the [state evolution](@entry_id:755365) $x_{k+1}=F(x_k)$ might be nonlinear, the evolution of [observables](@entry_id:267133) $g$ is linear: $(\mathcal{K}g)(x) = g(F(x))$. DMD can be interpreted as a numerical algorithm for finding a finite-dimensional approximation of the Koopman operator on a subspace spanned by a set of observable functions. The DMD modes and eigenvalues are thus approximations of the Koopman [eigenfunctions and eigenvalues](@entry_id:169656), which provide a global linearization of the nonlinear dynamics.

#### Non-Intrusive Surrogates for Parametric Studies

For problems where the goal is to map a set of input parameters $\mu$ to a scalar output $y(\mu)$ (e.g., $k_{\text{eff}}$ or a reaction rate), several non-intrusive surrogate modeling techniques are available.

**Polynomial Chaos Expansion (PCE)** is a spectral method that represents the output as an expansion in a [basis of polynomials](@entry_id:148579) that are orthogonal with respect to the probability distribution of the uncertain inputs . Assuming the input is a random vector $\xi$ with probability density $\rho(\xi)$, the expansion takes the form:
$$ y(\xi) \approx \sum_{|\alpha| \le p} c_\alpha \Psi_\alpha(\xi) $$
Here, $\{\Psi_\alpha\}$ are multivariate polynomials orthogonal in the Hilbert space $L^2(\Xi, \rho)$, and the coefficients $c_\alpha$ are computed via [orthogonal projection](@entry_id:144168): $c_\alpha = \langle y(\xi), \Psi_\alpha \rangle_\rho$. This method is highly efficient when the mapping from inputs to outputs is smooth and the number of uncertain parameters is small.

**Gaussian Process (GP) Regression** offers a non-parametric, Bayesian alternative . A GP defines a probability distribution over functions. It is specified by a prior mean function $m(\mu)$ and a covariance function, or kernel, $k(\mu, \mu')$, which encodes prior beliefs about the function's smoothness and correlation structure.

Given a set of training data points $\{(\mu_i, y_i)\}$, Bayesian inference is used to update the prior distribution to a **posterior predictive distribution** at a new test point $\mu_*$. For a Gaussian likelihood, this posterior is also a Gaussian distribution, defined by a [posterior mean](@entry_id:173826) and a posterior variance.
-   The **[posterior mean](@entry_id:173826)** provides the best estimate for the function's value. It is an interpolation of the training data, weighted by the kernel.
-   The **posterior variance** provides a measure of the uncertainty in this prediction. The variance is low near training data points and grows in regions of the input space far from any data.

This built-in [uncertainty quantification](@entry_id:138597) is a major strength of GP models, allowing them to not only predict an outcome but also express their confidence in that prediction .

### Ensuring Model Reliability: Verification and Validation (V&V)

The development of any computational model, especially a reduced-order one, must be accompanied by a rigorous **Verification and Validation (V&V)** process to build confidence in its predictions . These two activities are distinct and essential.

**Verification** answers the question: "Are we solving the mathematical model correctly?" It is a purely mathematical exercise focused on assessing the numerical accuracy of the code and solution. For a ROM or surrogate, verification activities involve comparing its predictions to those of the high-fidelity model it is meant to emulate. Key tasks include:
-   Performing convergence studies to show that the ROM error decreases as the basis dimension $r$ is increased.
-   Using techniques like the Method of Manufactured Solutions (MMS) to confirm the code's order of accuracy.
-   For data-driven surrogates, using techniques like $K$-fold [cross-validation](@entry_id:164650) to assess the model's [generalization error](@entry_id:637724) on held-out data.
-   Quantifying the error using appropriate metrics, such as the relative $L^2$-norm for fields and the relative error for integral quantities like reaction rates or $k_{\text{eff}}$.

**Validation** answers the question: "Are we solving the right model?" It is a physics and engineering exercise that assesses how well the mathematical model represents physical reality. This requires comparing model predictions against experimental data. Key tasks include:
-   Identifying relevant experimental benchmarks (e.g., from the International Criticality Safety Benchmark Evaluation Project, ICSBEP).
-   Performing [uncertainty quantification](@entry_id:138597) (UQ) to propagate uncertainties in model inputs (like nuclear data) and parameters through the model, yielding a prediction with a [confidence interval](@entry_id:138194).
-   Comparing the model's predictive interval to the experimental measurement and its uncertainty. The agreement is often quantified using a standardized residual.

A model is considered validated only when it is shown to be consistent with experimental data, considering all known sources of uncertainty. A comprehensive V&V plan is indispensable for the responsible development and deployment of reduced-order and [surrogate models](@entry_id:145436) in nuclear engineering.