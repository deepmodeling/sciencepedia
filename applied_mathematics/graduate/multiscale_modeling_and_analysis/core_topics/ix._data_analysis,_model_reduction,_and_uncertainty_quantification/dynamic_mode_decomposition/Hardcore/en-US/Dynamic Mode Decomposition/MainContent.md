## Introduction
In the age of big data, extracting meaningful, dynamic insights from complex, high-dimensional time-series remains a central challenge across science and engineering. Traditional methods often struggle with the inherent nonlinearity and scale of modern datasets, from fluid flow simulations to epidemiological records. Dynamic Mode Decomposition (DMD) emerges as a powerful, data-driven framework designed to tackle this challenge by identifying coherent spatio-temporal patterns and their underlying temporal evolution.

This article addresses the need for a comprehensive understanding of DMD by bridging its theoretical foundations with its practical applications. We will unravel how DMD provides an interpretable, linear perspective on even highly nonlinear systems.

To achieve this, we will first delve into the **Principles and Mechanisms** of DMD, exploring its deep connection to the Koopman operator and detailing the core algorithm for its computation. Next, in **Applications and Interdisciplinary Connections**, we will showcase the method's versatility across diverse fields and introduce a family of advanced DMD variants that extend its capabilities. Finally, a series of **Hands-On Practices** will ground these concepts in practical exercises. This structured journey will equip you with the knowledge to leverage DMD for analysis, prediction, and modeling of complex dynamical systems.

## Principles and Mechanisms

The capacity of Dynamic Mode Decomposition (DMD) to extract coherent [spatiotemporal patterns](@entry_id:203673) from complex data streams rests upon a deep theoretical foundation and a robust set of algorithmic procedures. This chapter elucidates these core principles and mechanisms, beginning with the operator-theoretic viewpoint that provides a linear framework for analyzing nonlinear systems, and proceeding to the practical, data-driven algorithms that approximate this framework. We will explore the construction of the DMD operator, the interpretation of its spectral properties, and the practical considerations for its application and evaluation.

### The Koopman Operator: A Linear Perspective on Nonlinear Dynamics

The analysis of [nonlinear dynamical systems](@entry_id:267921) is notoriously challenging due to the complex interactions between state variables. A powerful alternative to studying the dynamics in the state space is to shift perspective and analyze the evolution of functions of the state, known as **observables**. This is the central idea behind the Koopman operator framework.

Consider a [discrete-time dynamical system](@entry_id:276520) governed by the (possibly nonlinear) state-evolution map $f$:
$$
x_{k+1} = f(x_k)
$$
where $x_k \in \mathcal{X}$ is the state of the system in a state space $\mathcal{X} \subseteq \mathbb{C}^n$ at time step $k$. Instead of tracking the state vector $x_k$ itself, let us consider an observable, which is a scalar-valued function $g: \mathcal{X} \to \mathbb{C}$ that reports some quantity of interest about the state. The value of this observable at time step $k+1$ is $g(x_{k+1})$, which can be written in terms of the state at time $k$ as $g(f(x_k))$.

The **Koopman operator**, denoted $\mathcal{K}$, is defined as the operator that advances any observable function $g$ forward by one time step according to the system's dynamics. Its action is defined by composition with the state-evolution map $f$ :
$$
(\mathcal{K}g)(x) = g(f(x))
$$
The Koopman operator acts on a [function space](@entry_id:136890) $\mathcal{G}$ of [observables](@entry_id:267133), mapping it to itself, i.e., $\mathcal{K}: \mathcal{G} \to \mathcal{G}$. The most remarkable property of the Koopman operator is that it is **always linear**, regardless of whether the underlying state-evolution map $f$ is linear or nonlinear. This can be verified by its action on a [linear combination](@entry_id:155091) of two [observables](@entry_id:267133), $g_1$ and $g_2$, with scalar coefficients $\alpha$ and $\beta$:
$$
\mathcal{K}(\alpha g_1 + \beta g_2)(x) = (\alpha g_1 + \beta g_2)(f(x)) = \alpha g_1(f(x)) + \beta g_2(f(x)) = \alpha (\mathcal{K}g_1)(x) + \beta (\mathcal{K}g_2)(x)
$$
This inherent linearity allows the powerful tools of [linear systems theory](@entry_id:172825) and spectral analysis to be applied to nonlinear dynamics. The Koopman operator effectively "lifts" the finite-dimensional, [nonlinear dynamics](@entry_id:140844) of the state into an infinite-dimensional, linear evolution of [observables](@entry_id:267133).

The spectrum of the Koopman operator holds the key to understanding the system's temporal behavior. The **[eigenfunctions](@entry_id:154705)** $\phi_j$ and **eigenvalues** $\lambda_j$ of $\mathcal{K}$ are defined by the relation:
$$
\mathcal{K}\phi_j = \lambda_j \phi_j
$$
An [eigenfunction](@entry_id:149030) of the Koopman operator is a special observable whose spatial structure is preserved under the dynamics, changing only by a multiplicative factor $\lambda_j$ at each time step. If we evaluate an [eigenfunction](@entry_id:149030) along a trajectory of the system, its dynamics are perfectly linear:
$$
\phi_j(x_{k+1}) = \phi_j(f(x_k)) = (\mathcal{K}\phi_j)(x_k) = \lambda_j \phi_j(x_k)
$$
The Koopman eigenvalues $\lambda_j$ encode the characteristic frequencies and growth/decay rates of the system. Finding these spectral components is the primary goal of Koopman analysis.

### DMD as a Finite-Dimensional Approximation of the Koopman Operator

While the Koopman operator provides a profound theoretical framework, it is an infinite-dimensional operator and generally cannot be constructed explicitly. Dynamic Mode Decomposition provides a practical, data-driven method to compute a finite-dimensional approximation of the Koopman operator and its spectrum.

The fundamental premise of DMD is to approximate the action of the nonlinear flow map with a single, best-fit [linear operator](@entry_id:136520). Suppose we have collected a time series of data snapshots, $x_1, x_2, \dots, x_m$, sampled at a uniform time interval $\Delta t$. For an [autonomous system](@entry_id:175329), the true relationship between consecutive snapshots is given by the flow map, $x_{k+1} = \Phi^{\Delta t}(x_k)$. DMD postulates a [linear approximation](@entry_id:146101) to this relationship :
$$
x_{k+1} \approx A x_k
$$
where $A \in \mathbb{R}^{n \times n}$ is a time-invariant matrix. This matrix $A$ can be seen as a finite-dimensional approximation of the Koopman operator, specifically for the case where the [observables](@entry_id:267133) are the identity functions on each state variable.

To find the "best" such matrix $A$ from data, we assemble two snapshot matrices:
$$
X = [x_1, x_2, \dots, x_{m-1}] \in \mathbb{R}^{n \times (m-1)}
$$
$$
Y = [x_2, x_3, \dots, x_m] \in \mathbb{R}^{n \times (m-1)}
$$
The set of approximate relationships can then be written in matrix form as $Y \approx AX$. The DMD operator $A$ is found by solving the following optimization problem, which minimizes the [sum of squared residuals](@entry_id:174395) over all snapshot pairs:
$$
A^\star = \arg\min_{A \in \mathbb{R}^{n \times n}} \|Y - A X\|_F
$$
where $\|\cdot\|_F$ denotes the Frobenius norm. This is a standard linear [least-squares problem](@entry_id:164198), and its solution is given by:
$$
A^\star = Y X^\dagger
$$
where $X^\dagger$ is the Moore-Penrose [pseudoinverse](@entry_id:140762) of $X$. The spectral properties of this matrix $A^\star$—its [eigenvalues and eigenvectors](@entry_id:138808)—are the DMD eigenvalues and modes. They serve as finite-dimensional approximations to the true Koopman [eigenvalues and eigenfunctions](@entry_id:167697). This formulation can be extended beyond [state-space](@entry_id:177074) measurements to any chosen vector of observables $g(x)$, in which case the columns of $X$ and $Y$ would be the observable vectors $g(x_k)$ and $g(x_{k+1})$, respectively .

### The DMD Algorithm and Mode Construction

In many applications, the state dimension $n$ is very large (e.g., millions of grid points in a fluid simulation), making the explicit computation of the $n \times n$ operator $A^\star$ intractable. The standard DMD algorithm cleverly circumvents this by projecting the dynamics onto a low-dimensional subspace that captures the essential features of the data.

The algorithm typically proceeds as follows, starting with the snapshot matrices $X$ and $Y$  :

1.  **Singular Value Decomposition (SVD):** Compute the "thin" SVD of the data matrix $X$:
    $$
    X = U \Sigma V^*
    $$
    The columns of $U$ are [orthonormal vectors](@entry_id:152061) that form an [optimal basis](@entry_id:752971) for the data in an energy sense (they are the Proper Orthogonal Decomposition, or POD, modes). The [diagonal matrix](@entry_id:637782) $\Sigma$ contains the singular values, which quantify the energy content of each mode.

2.  **Rank Truncation:** For noisy or [high-dimensional systems](@entry_id:750282), the singular values typically decay rapidly. This suggests that the dynamics are largely confined to a low-dimensional subspace. We truncate the SVD to a rank $r \lt \min(n, m-1)$, where $r$ is a carefully chosen rank (a topic we return to later):
    $$
    X \approx U_r \Sigma_r V_r^*
    $$
    The columns of $U_r \in \mathbb{R}^{n \times r}$ form an orthonormal basis for this approximately [invariant subspace](@entry_id:137024).

3.  **Projection:** Instead of computing the full $n \times n$ operator $A^\star$, we compute its projection onto the low-dimensional subspace spanned by $U_r$. This yields a small, $r \times r$ **reduced-order operator**, $\tilde{A}$:
    $$
    \tilde{A} = U_r^* A^\star U_r = U_r^* (Y X^\dagger) U_r
    $$
    Using the truncated SVD to represent the [pseudoinverse](@entry_id:140762) ($X^\dagger \approx V_r \Sigma_r^{-1} U_r^*$), this simplifies to:
    $$
    \tilde{A} = U_r^* Y V_r \Sigma_r^{-1}
    $$
    This reduced operator $\tilde{A}$ captures the dynamics within the coordinate system defined by the POD basis $U_r$.

4.  **Eigendecomposition:** Compute the eigenvalues $\lambda_j$ and eigenvectors $w_j$ of the small matrix $\tilde{A}$:
    $$
    \tilde{A} w_j = \lambda_j w_j
    $$
    The eigenvalues $\lambda_j$ are the **DMD eigenvalues**, approximating the dominant Koopman eigenvalues. The vectors $w_j$ represent the DMD modes in the reduced-order coordinates.

5.  **Mode Reconstruction:** The final step is to reconstruct the **DMD modes** in the high-dimensional state space. There are two common variants for this step :
    *   **Standard (Projected) DMD:** The reduced-space eigenvectors $w_j$ are lifted back to the full space by taking a [linear combination](@entry_id:155091) of the POD basis vectors. The resulting mode is $\Phi_j = U_r w_j$. By construction, these modes lie within the subspace spanned by the input data, $\mathrm{range}(X)$.
    *   **Exact DMD:** This variant defines the modes as the image of the projected modes under the action of the full operator $A^\star$. The resulting expression is $\Phi_j = Y V_r \Sigma_r^{-1} w_j$. These modes lie within the subspace spanned by the output data, $\mathrm{range}(Y)$. If the subspace $\mathrm{range}(U_r)$ is not perfectly invariant under the dynamics (i.e., if $A^\star U_r$ has components outside of $\mathrm{range}(U_r)$), the exact DMD modes can provide a more accurate representation of the dynamic structures, leading to a smaller reconstruction error.

### Interpreting the DMD Output

The output of the DMD algorithm—a set of modes $\Phi_j$ and corresponding eigenvalues $\lambda_j$—provides a powerful decomposition of the dynamics into simpler, linearly evolving components.

The state of the system at any time step can be approximated by a linear superposition of the DMD modes, where each mode's amplitude evolves according to its eigenvalue :
$$
\hat{x}_k = \sum_{j=1}^r \Phi_j b_j \lambda_j^{k-1}
$$
Here, the coefficients $b_j$ are the initial amplitudes of each mode, determined by projecting the initial state $x_1$ onto the DMD modes (typically via a least-squares fit, $b = \Phi^\dagger x_1$, where $\Phi = [\Phi_1, \dots, \Phi_r]$).

The eigenvalues $\lambda_j$ are complex numbers that encode the temporal behavior of their associated modes. An eigenvalue can be written in [polar form](@entry_id:168412) as $\lambda_j = |\lambda_j| \exp(i\arg(\lambda_j))$.
*   The **magnitude** $|\lambda_j|$ governs the mode's growth or decay. If $|\lambda_j| \gt 1$, the mode is unstable and grows exponentially. If $|\lambda_j| \lt 1$, the mode is stable and decays. If $|\lambda_j| = 1$, the mode has a constant amplitude, representing a purely oscillatory or stationary state.
*   The **angle** $\arg(\lambda_j)$ determines the mode's [oscillation frequency](@entry_id:269468).

Since physical data (like temperature or velocity fields) are real-valued, the DMD operator $A^\star$ is a real matrix. A fundamental property of real matrices is that their non-real eigenvalues must occur in **complex-conjugate pairs**. If $\lambda$ is an eigenvalue with mode $\Phi$, then its conjugate $\bar{\lambda}$ is also an eigenvalue with mode $\bar{\Phi}$. A real-valued oscillation is constructed not by a single complex mode, but by the superposition of such a conjugate pair. This combination forms a real-valued pattern that oscillates with a specific frequency and is modulated by an [exponential growth](@entry_id:141869) or decay .

For systems originating from continuous-time processes sampled at an interval $\Delta t$, it is more natural to work with continuous-time eigenvalues, $\omega_j$. These are related to the discrete-time DMD eigenvalues by $\lambda_j = \exp(\omega_j \Delta t)$, which implies:
$$
\omega_j = \frac{\ln(\lambda_j)}{\Delta t}
$$
The real and imaginary parts of $\omega_j = \sigma_j + i f_j$ have direct physical interpretations:
*   $\sigma_j = \Re(\omega_j)$ is the continuous **growth/decay rate** (in units of inverse time).
*   $f_j = \Im(\omega_j)$ is the continuous **[angular frequency](@entry_id:274516)** (in radians per unit time).

For instance, in the analysis of a thermal conduction problem governed by the heat equation $\frac{\partial T}{\partial t} = \alpha \frac{\partial^2 T}{\partial x^2}$, the eigenvalues of the governing operator are real and negative. A DMD analysis of this system would yield real DMD eigenvalues $\lambda_j \lt 1$, corresponding to continuous-time eigenvalues $\omega_j$ that are purely real and negative. The value $\omega_j$ would directly approximate the physical decay rate $-\alpha k^2$ of a thermal mode with spatial wavenumber $k$ [@problem_id:3949672, @problem_id:3949590].

In more complex scenarios, such as a heated cylinder in a crossflow shedding periodic vortices, the dynamics involve both advection and diffusion. A DMD mode capturing an advected [thermal wave](@entry_id:152862) packet would exhibit an eigenvalue pair reflecting both phenomena. The frequency $\Im(\omega)$ would be related to the advection speed, while the decay rate $\Re(\omega)$ would be determined by the rate of thermal diffusion, which acts to damp the structure as it propagates .

### Practical Considerations and Advanced Topics

#### Dynamic vs. Energy Optimality: DMD vs. POD

It is crucial to distinguish DMD from Proper Orthogonal Decomposition (POD), as they serve different purposes .
*   **POD** (which is equivalent to the SVD of the data matrix) provides a set of [orthonormal basis](@entry_id:147779) modes that are **energy-optimal**. For any given rank $r$, the POD basis captures the maximum possible variance (energy) of the data ensemble. However, the temporal evolution of a POD mode's coefficient is generally complex, as a single POD mode may contain a mixture of different frequencies and growth rates.
*   **DMD** provides a set of modes that are **dynamically optimal**. Each DMD mode is associated with a single frequency and growth/decay rate. This makes the modes highly interpretable from a dynamical systems perspective. However, DMD modes are generally not orthogonal and do not form an energy-[optimal basis](@entry_id:752971).

In a heat transfer problem featuring a coherent oscillation (like periodic plume shedding), DMD is well-suited to isolate this oscillation into a single mode-eigenvalue pair, directly providing its frequency and decay rate. POD, by contrast, might spread this oscillation across several modes if its energy is not dominant, complicating the analysis of its dynamics. Conversely, for a system dominated by a single, stationary high-energy structure, POD would be highly efficient at representing it, while DMD's focus would be on the dynamics evolving on top of it.

#### Choosing the Truncation Rank

The choice of the truncation rank $r$ is one of the most critical and subtle steps in applying DMD to real-world data, which is often contaminated by noise and exhibits multiscale behavior . A rank that is too low may result in an impoverished model that misses important dynamics ([underfitting](@entry_id:634904)). A rank that is too high may lead to a model that fits the noise in the data, resulting in poor predictive performance (overfitting).

A principled approach to selecting $r$ involves several steps:
1.  **Heuristic Analysis:** Examine the [singular value](@entry_id:171660) spectrum of the data matrix $X$. A sharp "knee" or a large gap in the singular values (i.e., a large ratio $\sigma_r / \sigma_{r+1}$) often indicates a separation between the signal-dominated subspace and the noise-dominated subspace. Additionally, one might consider the rank needed to capture a certain percentage (e.g., $0.99$) of the total energy. These [heuristics](@entry_id:261307) can provide a set of candidate ranks.
2.  **Cross-Validation:** The ultimate test of a model is its ability to generalize to new data. For time series, this must be assessed using a method that respects temporal causality, such as **rolling-origin [cross-validation](@entry_id:164650)** or [blocked cross-validation](@entry_id:1121714), where the training set always precedes the [validation set](@entry_id:636445).
3.  **Multi-Horizon Error:** To ensure the model captures both [fast and slow dynamics](@entry_id:265915), the out-of-sample prediction error should be evaluated over multiple forecast horizons.
4.  **Parsimony:** Among models with similar cross-validated predictive performance, the simplest model (smallest $r$) is generally preferred. A common heuristic is the "one [standard error](@entry_id:140125) rule," which selects the most parsimonious model whose performance is statistically indistinguishable from the best-performing model.

#### Model Evaluation

Once a DMD model is constructed, its quality must be rigorously assessed. Key metrics include :
*   **In-Sample Reconstruction Error:** This measures how well the DMD model can reproduce the training data. A common metric is the relative Frobenius norm of the error:
    $$
    E_{\mathrm{recon}} = \frac{\|X - \hat{X}\|_F}{\|X\|_F}
    $$
    where $\hat{X}$ is the matrix of reconstructed snapshots.
*   **Out-of-Sample Prediction Error:** This is the most important metric for assessing a model's utility. It is computed on a held-out test dataset not used during training. For a test trajectory $\{y_i\}$, one can use the model to predict $h$ steps ahead from an initial condition $y_i$ and compare the prediction $\hat{y}_{i+h}$ to the true state $y_{i+h}$. Averaging the relative error over many such predictions provides a robust measure of the model's forecasting capability.

By combining the elegant linearity of the Koopman framework with robust, data-driven algorithms, Dynamic Mode Decomposition provides a versatile and powerful tool for the analysis, prediction, and control of complex dynamical systems across scientific and engineering disciplines.