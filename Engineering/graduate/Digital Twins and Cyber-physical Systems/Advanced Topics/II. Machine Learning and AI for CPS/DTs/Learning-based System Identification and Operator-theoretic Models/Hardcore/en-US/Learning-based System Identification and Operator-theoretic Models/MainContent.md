## Introduction
Modeling the complex, nonlinear behavior of modern cyber-physical systems is a central challenge in engineering and science, forming the bedrock for creating predictive digital twins. While traditional linear [system theory](@entry_id:165243) is well-developed, it falls short for many real-world applications, and purely nonlinear approaches can be analytically intractable. This article bridges that gap by exploring the powerful synthesis of learning-based system identification and [operator-theoretic models](@entry_id:1129150), which provide a pathway to analyze nonlinear dynamics using linear tools. Across three chapters, you will gain a comprehensive understanding of this cutting-edge field. The journey begins in "Principles and Mechanisms," where we will dissect the Koopman [operator theory](@entry_id:139990) that linearizes nonlinear dynamics and explore data-driven algorithms like EDMD and SINDy for approximating these operators. Next, "Applications and Interdisciplinary Connections" will demonstrate how these models are applied to control, [stochastic systems](@entry_id:187663), and even PDE-governed phenomena using advanced [neural operator](@entry_id:1128605) architectures. Finally, "Hands-On Practices" will solidify your knowledge through practical coding exercises that guide you from fundamental [least-squares](@entry_id:173916) estimation to full Dynamic Mode Decomposition pipelines. This structured approach will equip you with the theoretical and practical skills to build and deploy high-fidelity models of complex systems from data, starting with the core principles that make it all possible.

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms that underpin learning-based system identification through the lens of [operator theory](@entry_id:139990). We will move from the foundational concepts of how [linear operators](@entry_id:149003) can describe nonlinear dynamics to the practical algorithms used to approximate these operators from data. Furthermore, we will confront the critical real-world challenges of partial observations, noise, and experimental design, culminating in a discussion of model minimality.

### Linearizing Nonlinear Dynamics with Operators

The central challenge in modeling many complex systems, from fluid dynamics to cyber-physical systems, is their inherent nonlinearity. While [linear systems theory](@entry_id:172825) is mature and powerful, its direct application is limited. Operator-theoretic methods provide a remarkable bridge, allowing us to reframe the analysis of a nonlinear dynamical system in terms of an infinite-dimensional, yet perfectly linear, operator.

#### The Koopman Operator

Consider a [continuous-time dynamical system](@entry_id:261338) described by an ordinary differential equation (ODE) on a state space $X \subseteq \mathbb{R}^n$:
$$
\dot{x} = f(x)
$$
This equation governs the evolution of the state vector $x$. Instead of tracking the state itself, the Koopman operator framework focuses on the evolution of **observables**—scalar-valued functions $g: X \to \mathbb{C}$ that represent quantities one might measure or compute from the state. Let $\Phi^t(x)$ denote the flow of the dynamics, i.e., the state of the system at time $t$ starting from $x$. The value of the observable $g$ along this trajectory evolves as $g(\Phi^t(x))$.

The **Koopman operator**, $\mathcal{K}^t$, is defined by its action on an observable $g$. It advances the function $g$ forward in time along the system's trajectories. Formally, for each $t \ge 0$, the operator is given by composition with the flow :
$$
(\mathcal{K}^t g)(x) = g(\Phi^t(x))
$$
A key property of the Koopman operator is its linearity. For any two [observables](@entry_id:267133) $g_1, g_2$ and scalars $c_1, c_2$, we have $\mathcal{K}^t(c_1 g_1 + c_2 g_2) = c_1 \mathcal{K}^t g_1 + c_2 \mathcal{K}^t g_2$. This holds irrespective of whether the underlying dynamics $f(x)$ are nonlinear.

The dynamics of the Koopman operator are governed by its **[infinitesimal generator](@entry_id:270424)**, $\mathcal{L}$, defined by the limit:
$$
\mathcal{L}g = \lim_{t \to 0^+} \frac{\mathcal{K}^t g - g}{t}
$$
For sufficiently smooth observables, we can find a more explicit form for $\mathcal{L}$ by applying the [chain rule](@entry_id:147422) to the time derivative of $(\mathcal{K}^t g)(x)$ at $t=0$:
$$
\frac{d}{dt} g(\Phi^t(x))\bigg|_{t=0} = \nabla g(\Phi^0(x)) \cdot \frac{d}{dt}\Phi^t(x)\bigg|_{t=0} = \nabla g(x) \cdot f(x)
$$
Thus, the generator is the Lie derivative along the vector field $f$, $(\mathcal{L}g)(x) = f(x) \cdot \nabla g(x)$ . The evolution of any observable is then described by the linear partial differential equation $\frac{\partial}{\partial t}(\mathcal{K}^t g) = \mathcal{L}(\mathcal{K}^t g)$.

For [discrete-time systems](@entry_id:263935), $x_{k+1} = F(x_k)$, the concept is analogous and simpler. The discrete-time Koopman operator, which we denote by $\mathcal{K}$, advances an observable by one time step:
$$
(\mathcal{K} g)(x) = g(F(x))
$$

#### Spectral Decomposition of Nonlinear Dynamics

The true power of the Koopman framework lies in its spectral properties. If we can find [eigenfunctions](@entry_id:154705) of the Koopman operator, we can decompose the [nonlinear dynamics](@entry_id:140844) into a set of linearly evolving modes. An **[eigenfunction](@entry_id:149030)** $\varphi$ of $\mathcal{K}$ is a non-zero observable that transforms by simple scaling under the action of the operator:
$$
\mathcal{K}\varphi = \lambda \varphi
$$
where $\lambda \in \mathbb{C}$ is the corresponding **eigenvalue**.

The existence of these [eigenfunctions](@entry_id:154705) has profound consequences. Consider a discrete-time system $x_{k+1} = F(x_k)$ with a fixed point at the origin, $F(0)=0$. Let the system be linearized around this point by its Jacobian matrix $A = DF(0)$. Under certain non-resonance conditions on the eigenvalues of $A$, it can be shown that there exists a set of Koopman [eigenfunctions](@entry_id:154705) $\varphi_i(x)$ whose associated Koopman eigenvalues $\alpha_i$ are precisely the eigenvalues of the Jacobian $A$. These [eigenfunctions](@entry_id:154705) provide a local coordinate transformation $z_i = \varphi_i(x)$ that linearizes the [nonlinear dynamics](@entry_id:140844) . In this new coordinate system, the evolution is remarkably simple:
$$
z_{i, k+1} = \varphi_i(x_{k+1}) = \varphi_i(F(x_k)) = (\mathcal{K}\varphi_i)(x_k) = \alpha_i \varphi_i(x_k) = \alpha_i z_{i,k}
$$
This demonstrates that the Koopman operator's spectral properties can unravel the complex behavior of a nonlinear system into a collection of linear modes near a fixed point.

This concept extends to the evolution of any general observable $g(x)$. If the observable is analytic, it can be expanded in the basis of Koopman eigenfunctions (and their products, which are also [eigenfunctions](@entry_id:154705)). This leads to the **Koopman Mode Decomposition**. An observable $g(x)$ can be written as a linear combination of [eigenfunctions](@entry_id:154705) $\psi_\beta$:
$$
g(x) = \sum_{\beta} v_\beta \psi_\beta(x)
$$
where the $v_\beta$ are vector-valued coefficients called the **Koopman modes**. The [time evolution](@entry_id:153943) of the observable is then given by a linear superposition:
$$
g(x_k) = (\mathcal{K}^k g)(x_0) = \sum_{\beta} v_\beta (\mathcal{K}^k \psi_\beta)(x_0) = \sum_{\beta} v_\beta \lambda_\beta^k \psi_\beta(x_0)
$$
This powerful result shows that the complex, nonlinear evolution of an observable can be decomposed into a sum of modes, each evolving with a simple [exponential time](@entry_id:142418) dependence determined by a Koopman eigenvalue .

### From Theory to Data: Finite-Dimensional Approximations

The Koopman operator is an infinite-dimensional object, making its direct computation generally intractable. For practical, data-driven applications, we must find a finite-dimensional approximation. The most common family of methods for this task is Dynamic Mode Decomposition (DMD) and its extensions.

#### Extended Dynamic Mode Decomposition (EDMD)

**Extended Dynamic Mode Decomposition (EDMD)** is a general and powerful data-driven algorithm for approximating the action of the Koopman operator . The procedure consists of three main steps:

1.  **Choose a Dictionary of Observables:** First, we select a [finite set](@entry_id:152247) of $N$ basis functions, $\mathcal{D} = \{\psi_1, \psi_2, \dots, \psi_N\}$, called a **dictionary**. These functions should be chosen to span a subspace of observables that is relevant to the dynamics we wish to capture. Examples range from simple polynomials and [trigonometric functions](@entry_id:178918) to radial basis functions or even deep neural networks.

2.  **Lift Data into Observable Space:** Given a set of $M$ snapshot pairs from the system's trajectory, $\{(x_k, x_{k+1})\}_{k=0}^{M-1}$, we "lift" the data from the original state space into the higher-dimensional space spanned by our dictionary. This is done by evaluating the dictionary at each snapshot, creating two data matrices:
    $$
    \mathbf{X}_\psi = \begin{pmatrix} |  |   | \\ \boldsymbol{\psi}(x_0)  \boldsymbol{\psi}(x_1)  \cdots  \boldsymbol{\psi}(x_{M-1}) \\ |  |   | \end{pmatrix}, \quad
    \mathbf{Y}_\psi = \begin{pmatrix} |  |   | \\ \boldsymbol{\psi}(x_1)  \boldsymbol{\psi}(x_2)  \cdots  \boldsymbol{\psi}(x_M) \\ |  |   | \end{pmatrix}
    $$
    where $\boldsymbol{\psi}(x) = [\psi_1(x), \dots, \psi_N(x)]^T$.

3.  **Find the Best-Fit Linear Operator:** We then seek a matrix $K \in \mathbb{C}^{N \times N}$ that best approximates the linear evolution in the lifted space, i.e., $\boldsymbol{\psi}(x_{k+1}) \approx K \boldsymbol{\psi}(x_k)$. This is formulated as a linear [least-squares regression](@entry_id:262382) problem:
    $$
    \min_{K} \|\mathbf{Y}_\psi - K \mathbf{X}_\psi\|_F^2
    $$
    where $\|\cdot\|_F$ is the Frobenius norm. The solution is given by $K_{EDMD} = \mathbf{Y}_\psi \mathbf{X}_\psi^+$, where $\mathbf{X}_\psi^+$ is the Moore-Penrose [pseudoinverse](@entry_id:140762) of $\mathbf{X}_\psi$.

The matrix $K_{EDMD}$ is our finite-dimensional approximation of the Koopman operator, projected onto the subspace spanned by the dictionary $\mathcal{D}$. Its eigenvalues and eigenvectors approximate the Koopman eigenvalues and modes, respectively.

#### Dynamic Mode Decomposition (DMD)

**Dynamic Mode Decomposition (DMD)** can be understood as a special case of EDMD where the dictionary of [observables](@entry_id:267133) is simply the [identity function](@entry_id:152136) on the [state variables](@entry_id:138790): $\psi_i(x) = x_i$ . In this case, the regression seeks the best-fit linear model $x_{k+1} \approx A x_k$ directly from the state snapshot data. While computationally simple, DMD provides a good approximation of the Koopman operator only when the dynamics are already linear or when the chosen [observables](@entry_id:267133) (the state variables) happen to span a Koopman-[invariant subspace](@entry_id:137024). For general [nonlinear systems](@entry_id:168347), a richer dictionary via EDMD is necessary to achieve accurate models.

#### Theoretical Guarantees for EDMD

The convergence of the EDMD algorithm depends on both the quality of the dictionary and the richness of the data. As the number of data samples $M \to \infty$, we expect the empirical matrix $K_{EDMD}$ to converge to a deterministic limit. This limit is the [matrix representation](@entry_id:143451) of the Koopman operator $\mathcal{K}$ orthogonally projected onto the subspace spanned by the dictionary observables, $\mathrm{span}\{\psi_1, \dots, \psi_N\}$, with respect to an underlying [invariant measure](@entry_id:158370) $\mu$ of the dynamics.

For this convergence to be well-defined and meaningful, several conditions must be met :

1.  **Data Richness:** The data must be "rich" enough to accurately estimate the required statistical moments. This is satisfied if the data points are sampled independently and identically distributed (i.i.d.) from the [invariant measure](@entry_id:158370) $\mu$, or if they are generated from a single, sufficiently long trajectory of an ergodic system. In these cases, the law of large numbers or [the ergodic theorem](@entry_id:261967) guarantees that empirical averages converge to their true expected values.

2.  **Dictionary Linear Independence:** The dictionary functions $\{\psi_j\}_{j=1}^N$ must be [linearly independent](@entry_id:148207) in the function space $L^2(\mu)$. This ensures that the Gram matrix $G$, with entries $G_{ij} = \mathbb{E}_\mu[\psi_i(x) \overline{\psi_j(x)}]$, is positive-definite and invertible. If this condition is not met, the [least-squares problem](@entry_id:164198) becomes ill-posed, and the projected operator is not uniquely defined.

It is crucial to note that convergence of EDMD to the projected operator does *not* require the dictionary span to be a Koopman-[invariant subspace](@entry_id:137024). This property is only required if one wishes for the approximation to be exact on that subspace.

### Parsimony and Sparsity in Model Discovery

A key challenge in applying EDMD is the choice of dictionary. A small dictionary may not be expressive enough to capture the dynamics, while a large one can lead to overfitting and computationally expensive models. An alternative approach is to begin with a very large, comprehensive library of candidate functions and enforce that the resulting model should be **sparse**—meaning that most of the candidate functions are not used.

#### Sparse Identification of Nonlinear Dynamics (SINDy)

The **Sparse Identification of Nonlinear Dynamics (SINDy)** algorithm operationalizes this [principle of parsimony](@entry_id:142853) . For a continuous-time system $\dot{x} = f(x)$, SINDy assumes that each component of the vector field $f_i(x)$ can be represented as a sparse linear combination of functions from a large candidate library.

The procedure is as follows:
1.  **Generate Data:** Collect time-series data of the state $x(t)$ and numerically estimate its derivative, $\dot{x}(t)$. This forms two large matrices, $\mathbf{X}$ and $\mathbf{X}'$, stacking the state and derivative measurements over time.

2.  **Construct Library Matrix:** Define a library of candidate functions, $\Theta(x) = [\theta_1(x), \theta_2(x), \dots, \theta_m(x)]$, which might include polynomials, [trigonometric functions](@entry_id:178918), or other terms suspected to be relevant. Evaluate this library on the state data to form the feature matrix $\mathbf{\Theta}(\mathbf{X})$.

3.  **Perform Sparse Regression:** The problem is now to solve the linear system $\mathbf{X}' \approx \mathbf{\Theta}(\mathbf{X}) \Xi$ for the [coefficient matrix](@entry_id:151473) $\Xi$, with the critical constraint that $\Xi$ must be sparse. Ordinary [least squares](@entry_id:154899) would yield a dense, uninterpretable solution. SINDy instead solves a regularized regression problem, typically using an $\ell_1$-norm penalty (LASSO):
    $$
    \min_{\Xi} \frac{1}{2} \|\mathbf{X}' - \mathbf{\Theta}(\mathbf{X}) \Xi\|_F^2 + \lambda \|\Xi\|_1
    $$
    The term $\lambda \|\Xi\|_1$ penalizes the sum of the [absolute values](@entry_id:197463) of the coefficients, which is a [convex relaxation](@entry_id:168116) of the non-convex $\ell_0$ "norm" (which counts non-zero elements) and effectively drives many coefficients to exactly zero. The parameter $\lambda$ controls the trade-off between data fidelity and model sparsity.

For this process to be effective, it is often essential to normalize the columns of the library matrix $\mathbf{\Theta}(\mathbf{X})$ to ensure the penalty is applied fairly to functions of different scales. The final sparse model is often refined using techniques like Sequentially Thresholded Least Squares (STLS) to debias the non-zero coefficient estimates.

### Practical Challenges in System Identification

Translating these elegant theoretical frameworks into practical tools for building digital twins requires confronting several real-world challenges. We address three of the most important: partial [observability](@entry_id:152062), noise, and [experiment design](@entry_id:166380).

#### The Problem of Partial Observations and Time-Delay Embedding

In many applications, we cannot measure the full state vector $x_k$ of a system. Instead, we have access only to a limited set of scalar measurements, $y_k = h(x_k)$. Attempting to build a predictive model of the form $y_{k+1} = G(y_k)$ will generally fail, as the evolution of $y_k$ depends on the entire hidden state $x_k$, making the process non-Markovian.

A powerful solution to this problem is **[time-delay embedding](@entry_id:149723)**. The core idea is to reconstruct a state space from the history of the scalar measurement. We form a delay vector:
$$
z_t = [y_t, y_{t-\tau}, y_{t-2\tau}, \dots, y_{t-(m-1)\tau}]^T \in \mathbb{R}^m
$$
where $m$ is the [embedding dimension](@entry_id:268956) and $\tau$ is the time delay. **Takens' Embedding Theorem** provides the theoretical justification for this reconstruction  . The theorem states that for a generic smooth dynamical system evolving on a $d$-dimensional attractor, the map from the original state $x_t$ to the delay vector $z_t$ is an **embedding** (a one-to-one, smooth transformation) provided the [embedding dimension](@entry_id:268956) is sufficiently large, specifically $m \ge 2d+1$.

The justification for this dimension requirement comes from dimension-counting arguments in [differential topology](@entry_id:157662). To ensure the map is injective (no two distinct states $x$ and $y$ map to the same delay vector), the dimension of the [target space](@entry_id:143180) ($m$) must be generically larger than the dimension of the space of pairs of points ($2d$). To ensure the map is an immersion (the derivative is full rank), the dimension $m$ must be at least $2d$. The stricter [injectivity](@entry_id:147722) requirement leads to the famous $m \ge 2d+1$ bound .

The profound implication of Takens' theorem is that the reconstructed delay vector $z_t$ serves as a [faithful representation](@entry_id:144577) of the true state. The dynamics in this reconstructed space become deterministic and Markovian: there exists a [smooth map](@entry_id:160364) $G$ such that $z_{t+1} = G(z_t)$. This reconstructed state $z_t$ can then be used as the input to identification algorithms like EDMD or SINDy, enabling the modeling of systems from partial observations .

#### The Role of Noise and Uncertainty

Real-world measurements are invariably corrupted by noise. It is crucial to distinguish between two types :
-   **Process Noise ($w_k$):** Random disturbances that act directly on the system's state dynamics, e.g., $x_{k+1} = f(x_k, u_k) + w_k$. This represents unmodeled forces or intrinsic stochasticity.
-   **Measurement Noise ($v_k$):** Errors introduced by the sensor during the measurement process, e.g., $y_k = h(x_k) + v_k$.

The presence of noise, particularly measurement noise, poses a significant challenge for regression-based identification methods. When we construct regressors from noisy measurements (e.g., using past outputs $y_{k-1}$ in an autoregressive model), we create a correlation between the regressors and the noise in the data. This is known as an **[errors-in-variables](@entry_id:635892)** problem. This correlation violates a fundamental assumption of [ordinary least squares](@entry_id:137121), leading to **biased and inconsistent** parameter estimates, even if the measurement noise itself is simple Additive White Gaussian Noise (AWGN). For reliable estimation in such cases, more advanced techniques like Instrumental Variables (IV) methods or subspace identification are required.

The statistical properties of the noise also matter. If [process noise](@entry_id:270644) is **colored** (i.e., its power spectrum is not flat), one standard technique is to model the noise process itself with a [linear filter](@entry_id:1127279) and **augment the system state** with the internal states of this filter. This transforms the problem into an equivalent one with white process noise, allowing standard tools to be applied . If disturbances are **non-Gaussian** with heavy tails, estimators based on minimizing squared error become highly sensitive to outliers. In these cases, robust statistical methods that temper the influence of large errors are necessary.

#### The Importance of Experiment Design and Persistent Excitation

The quality of a data-driven model is fundamentally limited by the quality of the data used to build it. A critical concept in this regard is **[persistency of excitation](@entry_id:189029)** . The input signal applied to the system during the identification experiment must be sufficiently "rich" to excite all the relevant dynamical modes.

If the input is not persistently exciting, the regression problem at the heart of methods like EDMD and SINDy can become ill-conditioned or even singular. For instance, if a nonlinear system is excited with only a single-frequency sinusoid, $u_k = \alpha \sin(\omega k)$, the system's state may settle into a simple [periodic orbit](@entry_id:273755). When this data is lifted into a high-dimensional feature space containing terms like $u_k$, $u_k^2$, and cross-products like $x_k u_k$, many of the columns of the feature matrix $\mathbf{\Phi}$ will become nearly linearly dependent. This multicollinearity results in an [information matrix](@entry_id:750640) $\mathbf{\Phi}^T \mathbf{\Phi}$ that is ill-conditioned (has a very large condition number), which in turn inflates the variance of the estimated parameters, making the model unreliable.

The remedy is not simply to collect more data with the same poor input, nor is it to rely solely on regularization. The correct solution is a proper **experiment redesign**. A persistently exciting input should be used, such as:
-   A **pseudo-random binary sequence (PRBS)**, which has a broad power spectrum.
-   A **random-phase multisine signal**, which is a sum of sinusoids at different frequencies with randomized phases.

Such inputs ensure that the system is explored more thoroughly, breaking the correlations between features and yielding a well-conditioned regression problem, which is essential for identifying a reliable and accurate model .

#### Realization Theory and Model Minimality

After identifying a state-space model, whether through EDMD or other methods, a natural question arises: is this the simplest possible model that describes the input-output behavior? This is the central question of **realization theory** .

For a linear time-invariant (LTI) system specified by matrices $(A,B,C,D)$, a realization is said to be **minimal** if its state dimension is the smallest possible among all realizations that produce the same input-output map. A fundamental theorem of [system theory](@entry_id:165243) states that a realization is minimal if and only if it is both:
-   **Reachable (or Controllable):** Any state can be reached from the zero state in a finite time by applying some input sequence. This means no part of the state space is inaccessible to the controls.
-   **Observable:** Any initial state can be uniquely determined by observing the output sequence over a finite time (for zero input). This means there are no distinct internal states that produce the exact same output, making them indistinguishable.

The dimension of a [minimal realization](@entry_id:176932) is a unique property of the system, known as its **McMillan degree**. This degree is equal to the rank of the (infinite block) **Hankel matrix** constructed from the system's impulse response coefficients (Markov parameters). All minimal realizations of a given system are related to each other by an invertible state-space transformation (a similarity transform).

These concepts are crucial because learning-based methods, particularly those with large, generic dictionaries, can easily produce over-parameterized, non-[minimal models](@entry_id:142622). The principles of realization theory provide the theoretical foundation for post-processing and [model reduction](@entry_id:171175) techniques (such as [balanced truncation](@entry_id:172737)) that aim to extract a minimal, and thus more efficient and interpretable, model from an initial, high-dimensional identification result. It is important to note that minimality is a structural property, independent of the system's stability .