## Introduction
Simultaneously estimating the evolving state of a dynamical system and its unknown, underlying parameters is a fundamental challenge across science and engineering. From forecasting weather with complex atmospheric models to enabling [autonomous navigation](@entry_id:274071), the ability to learn from data to refine both a system's state and its governing equations is paramount. This dual objective, however, presents a significant hurdle: how can we efficiently and accurately disentangle the effects of the state from those of the parameters using a finite stream of noisy observations? The choice of estimation strategy is not merely a technical detail but a critical decision that impacts accuracy, stability, and computational feasibility.

This article provides a comprehensive exploration of the two principal methodologies developed to solve this problem: joint and dual estimation. We will dissect their theoretical foundations, algorithmic implementations, and practical trade-offs, offering a clear guide to navigating this complex topic. In the first chapter, "Principles and Mechanisms," we will establish the core Bayesian framework for the problem, define the critical concepts of identifiability and observability, and contrast the joint (augmented-state) and dual (decoupled) strategies as they are implemented in sequential filters and variational smoothers. The second chapter, "Applications and Interdisciplinary Connections," will showcase how these methods are deployed in large-scale [geophysics](@entry_id:147342), robotics, and [statistical modeling](@entry_id:272466), highlighting the practical challenges and advanced solutions that arise in [high-dimensional systems](@entry_id:750282). Finally, "Hands-On Practices" will provide a set of targeted problems to solidify your understanding of the theoretical concepts and their numerical application. We begin by delving into the foundational principles that govern [state-parameter estimation](@entry_id:755361).

## Principles and Mechanisms

The estimation of unknown parameters within a dynamical system, concurrent with the estimation of the system's state, represents a cornerstone of modern data assimilation and [inverse problem theory](@entry_id:750807). This chapter delineates the fundamental principles and mechanisms governing this task. We will first establish the foundational Bayesian framework for joint [state-parameter estimation](@entry_id:755361), then explore the critical concepts of identifiability and [observability](@entry_id:152062) that determine whether such estimation is feasible. Subsequently, we will contrast the two principal methodological strategies—joint and dual estimation—and detail their implementation within both sequential (filtering) and variational (smoothing) contexts. Finally, we will address advanced practical considerations, including the rationale for choosing one strategy over the other, the role of regularization, and specialized techniques for ensemble-based methods.

### The Bayesian Formulation of Joint Estimation

The canonical problem involves a [discrete-time state-space](@entry_id:261361) model, which consists of a **process model** describing the system's evolution and an **observation model** linking the state to available measurements.

The process model is given by:
$$x_{k+1} = M(x_k, \theta) + \eta_k$$

Here, $x_k \in \mathbb{R}^{n_x}$ is the [state vector](@entry_id:154607) at time $k$, $\theta \in \mathbb{R}^{n_\theta}$ is a vector of unknown parameters that influence the dynamics, and $M$ is the model operator, which is often nonlinear. The term $\eta_k$ represents the model or process error, typically modeled as a random variable with a known probability distribution, such as a zero-mean Gaussian with covariance $Q$. This equation's structure implies a first-order Markov property: the state at time $k+1$ depends only on the state and parameters at time $k$.

The observation model is:
$$y_k = H(x_k) + \epsilon_k$$

In this equation, $y_k \in \mathbb{R}^{n_y}$ is the vector of observations at time $k$, $H$ is the [observation operator](@entry_id:752875) that maps the state space to the observation space, and $\epsilon_k$ is the [observation error](@entry_id:752871), also typically modeled as a zero-mean Gaussian random variable with covariance $R$. Crucially, observations are conditionally independent given the true state; $y_k$ depends only on $x_k$.

The objective of [state-parameter estimation](@entry_id:755361) is to infer the unknown states $x_{0:K} = \{x_0, \dots, x_K\}$ and parameters $\theta$ from a sequence of observations $y_{0:K} = \{y_0, \dots, y_K\}$. Within a Bayesian framework, this translates to determining the joint posterior probability distribution $p(x_{0:K}, \theta \mid y_{0:K})$. According to Bayes' rule, this posterior is proportional to the product of the likelihood and the prior:

$$p(x_{0:K}, \theta \mid y_{0:K}) \propto p(y_{0:K} \mid x_{0:K}, \theta) \, p(x_{0:K}, \theta)$$

By leveraging the [conditional independence](@entry_id:262650) structure of the [state-space model](@entry_id:273798), we can factorize these terms. The likelihood $p(y_{0:K} \mid x_{0:K}, \theta)$ decomposes into a product of individual observation likelihoods, $p(y_k \mid x_k)$. The joint prior $p(x_{0:K}, \theta)$ decomposes via the [chain rule](@entry_id:147422) and the Markov property into the product of a prior on the initial state and parameters, $p(x_0, \theta)$, and the sequence of state transitions, $p(x_{k+1} \mid x_k, \theta)$.

This leads to two principal formulations depending on the nature of the parameter $\theta$ [@problem_id:3421540].

**Static Parameter Estimation:** If the parameter vector $\theta$ is assumed to be unknown but constant over time, the posterior distribution takes the form:
$$p(x_{0:K}, \theta \mid y_{0:K}) \propto p(x_0, \theta) \left( \prod_{k=0}^{K-1} p(x_{k+1} \mid x_k, \theta) \right) \left( \prod_{k=0}^{K} p(y_k \mid x_k) \right)$$
Expressing this in terms of the error distributions (e.g., PDFs $q_\eta$ and $q_\epsilon$), we have:
$$p(x_{0:K}, \theta \mid y_{0:K}) \propto p(x_0, \theta) \left( \prod_{k=0}^{K-1} q_\eta(x_{k+1} - M(x_k, \theta)) \right) \left( \prod_{k=0}^{K} q_\epsilon(y_k - H(x_k)) \right)$$

**Dynamic Parameter Estimation:** In many cases, parameters may also evolve over time, or it may be advantageous for the estimation algorithm to model them as such. We introduce a time-dependent parameter $\theta_k$ with its own evolution model, for example, a random walk: $\theta_{k+1} = G(\theta_k) + \nu_k$, where $\nu_k$ is a noise term with PDF $q_\nu$. The set of unknowns now includes the entire parameter trajectory $\theta_{0:K}$. The joint posterior becomes:
$$p(x_{0:K}, \theta_{0:K} \mid y_{0:K}) \propto p(x_0, \theta_0) \left( \prod_{k=0}^{K-1} p(x_{k+1} \mid x_k, \theta_k) p(\theta_{k+1} \mid \theta_k) \right) \left( \prod_{k=0}^{K} p(y_k \mid x_k) \right)$$
In terms of error distributions:
$$p(x_{0:K}, \theta_{0:K} \mid y_{0:K}) \propto p(x_0, \theta_0) \left( \prod_{k=0}^{K-1} q_\eta(x_{k+1} - M(x_k, \theta_k)) q_\nu(\theta_{k+1} - G(\theta_k)) \right) \left( \prod_{k=0}^{K} q_\epsilon(y_k - H(x_k)) \right)$$
This dynamic formulation is mathematically equivalent to [state estimation](@entry_id:169668) for an **augmented state vector** $z_k = [x_k^T, \theta_k^T]^T$.

### Fundamental Concepts: Identifiability and Observability

Before attempting to solve for the [posterior distribution](@entry_id:145605), one must ask a more fundamental question: is it even possible to uniquely determine the unknown parameters and states from the available data? This question relates to the system-theoretic concepts of identifiability and [observability](@entry_id:152062). These are intrinsic properties of the model structure, independent of the estimation algorithm used [@problem_id:3421606].

**State Observability** concerns the ability to determine the state of the system. A system is said to be observable if, for a known parameter vector $\theta$, the initial state $x_0$ can be uniquely determined from the sequence of outputs $y_{0:\infty}$. This is a question of the injectivity of the map from the initial state to the output sequence.

**Structural Parameter Identifiability** concerns the ability to determine the parameters. A parameter $\theta$ is structurally identifiable if, for a generic initial state $x_0$, any two distinct parameter values $\theta_1 \neq \theta_2$ produce distinct output sequences. If different parameters can produce identical outputs, the parameters are structurally unidentifiable [@problem_id:3421606].

The two concepts are intimately linked through the augmented-state viewpoint. The joint estimation problem is equivalent to a state [observability](@entry_id:152062) problem for the augmented state $z_k = [x_k^T, \theta^T]^T$. If this augmented system is observable, it implies that the pair $(x_0, \theta)$ can be uniquely determined, which in turn means that the original state is observable and the parameter is identifiable [@problem_id:3421606].

A major challenge to [identifiability](@entry_id:194150) is the **[confounding](@entry_id:260626) of variables**, where the effect of one unknown can be mimicked by another. For example, consider a simple linear model where the true dynamics are $x_{k+1} = \theta x_k$, but we attempt to estimate both $\theta$ and a constant [model bias](@entry_id:184783) $b$, such that our estimation model is $x_{k+1} = \theta x_k + b$. If the system trajectory happens to be constant, $x_k = c$, the governing equation becomes $c = \theta c + b$. This single linear equation for two unknowns $(\theta, b)$ has a line of solutions, making the parameters unidentifiable. Only if the trajectory is not constant can the effects of $\theta$ and $b$ be disentangled [@problem_id:3421547]. More generally, if the effect of a parameter perturbation $\delta\theta$ on the dynamics can be perfectly absorbed by a change in the [model error](@entry_id:175815) term, the parameter is unidentifiable from the bias [@problem_id:3421547].

### Principal Strategies: Joint vs. Dual Estimation

Assuming the problem is well-posed (i.e., the unknowns are identifiable), there are two main strategies for tackling the estimation [@problem_id:3421545].

1.  **Joint Estimation:** This strategy, also known as the augmented-state approach, treats the parameters as additional state variables. The [state vector](@entry_id:154607) is augmented to $z_k = [x_k^T, \theta_k^T]^T$, and a single, unified estimation algorithm is applied to this larger system. The primary advantage of this approach is its theoretical rigor. By estimating states and parameters simultaneously, it can fully account for the evolving statistical cross-correlations between them, which are essential for optimal information propagation.

2.  **Dual Estimation:** This strategy decouples the problem into two or more smaller estimation tasks that are solved iteratively or sequentially. A common implementation involves alternating between a [state estimation](@entry_id:169668) step (where parameters are held fixed at their current best estimate) and a [parameter estimation](@entry_id:139349) step (where the state trajectory is held fixed or informed by the recent state analysis). This approach is often suboptimal because it simplifies or ignores the state-parameter cross-correlations during the update. However, as we will see, it possesses significant practical advantages in certain scenarios.

### Mechanisms and Implementations

We now explore how these strategies are put into practice within the two dominant paradigms of data assimilation: sequential filtering and variational smoothing.

#### Sequential Methods: The Augmented-State Ensemble Kalman Filter (EnKF)

In sequential [data assimilation](@entry_id:153547), estimates are updated recursively as each new observation becomes available. The Ensemble Kalman Filter (EnKF) is a prominent Monte Carlo method for doing so, particularly in high-dimensional [nonlinear systems](@entry_id:168347). The joint estimation strategy is naturally implemented in the EnKF through [state augmentation](@entry_id:140869) [@problem_id:3421602].

Let us consider the augmented state $z_k = [x_k^T, \theta_k^T]^T$. The EnKF represents the probability distribution of $z_k$ using an ensemble of $N$ forecast members, collected in an ensemble matrix $Z_f = [X_f^T, \Theta_f^T]^T$. The sample covariance of this ensemble, $P^z_f$, is a [block matrix](@entry_id:148435):
$$P^z_f = \begin{pmatrix} P_{xx}  P_{x\theta} \\ P_{\theta x}  P_{\theta\theta} \end{pmatrix}$$

The analysis step updates the [forecast ensemble](@entry_id:749510) to an analysis ensemble using the observation $y_k$. The update for each ensemble member is proportional to the innovation (the difference between the observation and the model's prediction) weighted by a Kalman gain matrix $K_z$. For the augmented system, the gain matrix $K_z$ also has a block structure, $K_z = [K_x^T, K_\theta^T]^T$. The update equations are:
$$X_a = X_f + K_x (Y^o - H X_f)$$
$$\Theta_a = \Theta_f + K_\theta (Y^o - H X_f)$$
where $Y^o$ is a matrix of perturbed observations used in stochastic EnKF formulations.

The crucial insight lies in the expression for the parameter gain, $K_\theta$. It can be shown that [@problem_id:3421602]:
$$K_\theta = P_{\theta x} H^T S^{-1}$$
where $S = H P_{xx} H^T + R$ is the innovation covariance. This equation reveals the central mechanism of joint estimation in a Kalman filter context: **the parameter $\theta$ is updated based on the observation of the state $x$ through the forecast cross-covariance $P_{\theta x}$**. If the ensemble indicates a [statistical correlation](@entry_id:200201) between the parameter and the state ($P_{\theta x} \neq 0$), an innovation in the state will lead to a correction in the parameter [@problem_id:3421545].

A critical aspect of implementing this approach is the model for the parameter evolution itself. If we model the parameter as static ($\theta_{k+1}=\theta_k$), the filter's estimate of the parameter variance, $P_{\theta\theta}$, will tend to shrink with every update. This can lead to **covariance collapse**, where the parameter variance becomes so small that the filter effectively stops learning, a phenomenon sometimes called "filter sleep". If the true parameter drifts, the filter will fail to track it, leading to bias and potential divergence. To counteract this, a common technique is to model the parameter with artificial dynamics, such as a random walk: $\theta_{k+1} = \theta_k + \xi_k$, where $\xi_k \sim \mathcal{N}(0, Q_\theta)$. The parameter process noise variance, $Q_\theta$, acts as an **inflation factor** that prevents the parameter variance from collapsing, thereby maintaining the filter's responsiveness. Choosing $Q_\theta$ involves a delicate trade-off: a value that is too small leads back to filter sleep, while one that is too large can cause the parameter estimate to wander erratically in response to noise, degrading the overall state estimate [@problem_id:3421598].

#### Variational Methods: Joint 4D-Var

Variational methods approach estimation as an optimization problem. Strong-constraint 4D-Var seeks the initial state $x_0$ and parameters $\theta$ that minimize a [cost function](@entry_id:138681) measuring the mismatch between the model trajectory and the observations over a time window, while respecting the model dynamics as a perfect constraint.

For joint [state-parameter estimation](@entry_id:755361), the control vector is the pair $(x_0, \theta)$, and the cost function is [@problem_id:3421556]:
$$J(x_0, \theta) = \frac{1}{2}\|x_0 - x_b\|_{B^{-1}}^2 + \frac{1}{2} \sum_{k=1}^{K} \|y_k - H(x_k(x_0, \theta))\|_{R^{-1}}^2$$
The first term penalizes deviations of the initial state from a prior (background) estimate $x_b$ with covariance $B$, and the second term penalizes the sum of squared observation-minus-forecast residuals along the trajectory. The notation $x_k(x_0, \theta)$ emphasizes that the state trajectory is uniquely determined by the control variables.

The minimum of this cost function is found using iterative, [gradient-based optimization](@entry_id:169228) methods. The primary challenge is the efficient computation of the gradient of $J$ with respect to the high-dimensional control vector $(x_0, \theta)$. This is achieved using the **[adjoint method](@entry_id:163047)**. By introducing Lagrange multipliers $\lambda_k$ (the adjoint variables) to enforce the model constraints $x_{k+1} - M_k(x_k, \theta) = 0$, one can derive a set of backward-propagating adjoint equations. The solution of these adjoint equations provides the sensitivities needed to compute the gradient.

The resulting gradients have the form [@problem_id:3421556]:
$$\nabla_{x_0} J = B^{-1}(x_0 - x_b) - M_{0,x}(x_0, \theta)^{\top} \lambda_1$$
$$\nabla_{\theta} J = - \sum_{k=0}^{K-1} M_{k,\theta}(x_k, \theta)^{\top} \lambda_{k+1}$$
where $M_{k,x}$ and $M_{k,\theta}$ are the Jacobians of the model operator with respect to the state and parameters, respectively. The adjoint variable $\lambda_{k+1}$ effectively accumulates the sensitivity of the cost function to a perturbation at state $x_{k+1}$. The gradient with respect to $\theta$ sums these sensitivities, weighted by the direct sensitivity of the model to $\theta$, across the entire assimilation window.

In this variational context, local identifiability is related to the curvature of the cost function at its minimum, which is described by the **Hessian matrix**, $\mathcal{H}$. The [posterior covariance](@entry_id:753630) of the estimate is approximated by the inverse of the Hessian. A singular or ill-conditioned Hessian indicates poor identifiability. For the joint problem, the Hessian is a [block matrix](@entry_id:148435). The marginal uncertainty of the parameter $\theta$ is given by the inverse of the **Schur complement** of the state block in the Hessian. This matrix represents the effective information content for the parameters after accounting for the uncertainty in the initial state, and its conditioning governs the quality of the parameter estimate [@problem_id:3421560].

### Practical Considerations and Advanced Topics

While the joint strategy is often theoretically optimal, practical constraints can render the dual strategy preferable. The choice depends on a careful analysis of the problem's characteristics.

#### When to Prefer Dual Estimation

Dual estimation can be advantageous under several conditions [@problem_id:3421565]:

*   **Numerical Ill-Conditioning:** When there is a large [separation of scales](@entry_id:270204)—for instance, if the [state variables](@entry_id:138790) evolve much faster than the parameters, or if the observations are far more sensitive to the state than to the parameters—the joint Hessian matrix can become severely ill-conditioned. This makes its inversion numerically unstable. Dual methods, by solving separate, smaller problems for the state and parameters, can circumvent this by working with better-conditioned sub-problems.
*   **Computational Cost:** The computational cost of solving the joint estimation problem scales with the size of the augmented state, $(n_x + n_\theta)$. For [high-dimensional systems](@entry_id:750282), this can be prohibitive. Dual strategies break the problem into smaller, more manageable pieces (e.g., of size $n_x$ and $n_\theta$), which can lead to substantial computational savings.
*   **The Small Ensemble Problem:** In [high-dimensional systems](@entry_id:750282) where the EnKF is used, the ensemble size $N$ is often much smaller than the state dimension ($N \ll n_x$), let alone the augmented dimension ($N \ll n_x + n_\theta$). In such cases, the [sample covariance matrix](@entry_id:163959) for the joint system is rank-deficient and riddled with spurious long-range correlations. These [spurious correlations](@entry_id:755254) can catastrophically corrupt the update, especially the delicate state-parameter cross-covariance. A dual approach can mitigate this by, for example, running an EnKF on the state alone (where the rank-deficiency problem may be less severe) and using a separate method for the parameters, thus preventing contamination from spurious state-parameter correlations.

#### Regularization and Error Attribution

When a model is structurally unidentifiable or poorly identifiable, the corresponding estimation problem is ill-posed. This manifests as a singular or ill-conditioned Hessian in [variational methods](@entry_id:163656). A standard remedy is **regularization**. By adding a penalty term to the cost function, we incorporate additional information that makes the problem well-posed. A common choice is **Tikhonov regularization**, which adds a penalty of the form $\frac{1}{2}\lambda\|\theta\|^2$. This adds a term $\lambda I$ to the parameter block of the Hessian, improving its condition number and ensuring invertibility. This introduces a small bias into the solution in exchange for a large reduction in variance, a classic bias-variance trade-off [@problem_id:3421560].

In a [stochastic filtering](@entry_id:191965) context, the relative magnitudes of [process noise](@entry_id:270644) variances act as an implicit regularizer. If a model exhibits [confounding](@entry_id:260626) between a parameter $\theta$ and a [model bias](@entry_id:184783) $b$, the filter must decide how to attribute any forecast error. If the process noise for the bias, $q_b$, is set much larger than that for the parameter, $q_\theta$, the filter is being told that the bias is more likely to vary than the parameter. Consequently, it will preferentially adjust its estimate of the bias to explain innovations, effectively allowing the bias term to absorb any apparent parameter misspecification [@problem_id:3421547].

#### Covariance Localization for Augmented-State EnKF

A key technique for mitigating the effects of small ensemble sizes in the EnKF is **[covariance localization](@entry_id:164747)**. This involves element-wise multiplication (a Schur product) of the [sample covariance matrix](@entry_id:163959) $P_f$ with a tapering matrix $L$ whose elements decay to zero with increasing distance between variables. To ensure the resulting localized covariance $L \circ P_f$ remains a valid (symmetric [positive semi-definite](@entry_id:262808)) covariance matrix, the taper matrix $L$ must also be SPSD.

When applying localization to an augmented state-parameter system, special care must be taken with the parameter type [@problem_id:3421611].
*   For **local parameters**, which have a spatially confined influence, it is appropriate to assign them a pseudo-location and apply a taper with a radius of influence commensurate with their physical scale. This correctly [damps](@entry_id:143944) [spurious correlations](@entry_id:755254) between the parameter and distant [state variables](@entry_id:138790).
*   For **global parameters**, which influence the entire model domain, the true physical correlations are long-ranged. Applying a distance-based taper with a finite radius would erroneously suppress these essential correlations, crippling the filter's ability to update the parameter using information from across the domain. Therefore, for global parameters, the taper radius in the corresponding blocks of the localization matrix ($L_{x\theta}$ and $L_{\theta\theta}$) must be set to be very large (effectively infinite), meaning their correlations are not localized. This preserves the global information flow necessary for their estimation.