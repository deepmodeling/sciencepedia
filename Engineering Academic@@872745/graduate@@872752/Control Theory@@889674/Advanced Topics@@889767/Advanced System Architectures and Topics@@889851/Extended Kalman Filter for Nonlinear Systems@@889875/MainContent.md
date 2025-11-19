## Introduction
Estimating the internal state of a dynamic system from noisy, indirect measurements is a fundamental challenge in virtually every field of science and engineering. While the celebrated Kalman filter provides an [optimal solution](@entry_id:171456) for linear systems, the vast majority of real-world phenomena—from a robot navigating a room to the [global carbon cycle](@entry_id:180165)—are inherently nonlinear. This presents a significant knowledge gap: how can we recursively estimate the state of a system when its dynamics or measurements cannot be described by simple [linear equations](@entry_id:151487)?

The Extended Kalman Filter (EKF) emerges as a powerful and widely adopted answer to this question. It serves as the workhorse for [nonlinear state estimation](@entry_id:269877) by ingeniously applying the principles of the linear Kalman filter to a localized, linear approximation of the nonlinear system. However, this approximation is both the EKF's greatest strength and its most significant vulnerability, introducing errors that can lead to poor performance or even [filter divergence](@entry_id:749356) if not properly understood.

This article provides a graduate-level exploration of the Extended Kalman Filter, moving from foundational theory to practical application.
- First, in **Principles and Mechanisms**, we will dissect the EKF from its probabilistic roots in Bayesian filtering. We will derive its famous predict-update equations, investigate the critical impact of [linearization error](@entry_id:751298), and discuss methods for ensuring stability and [numerical robustness](@entry_id:188030).
- Next, in **Applications and Interdisciplinary Connections**, we will witness the EKF's versatility as it is applied to a diverse array of problems in robotics, engineering, ecology, and synthetic biology, showcasing advanced techniques like [state augmentation](@entry_id:140869) and the error-state EKF.
- Finally, the **Hands-On Practices** section will provide opportunities to solidify this knowledge by tackling core implementation challenges, from model [discretization](@entry_id:145012) to filter tuning.

## Principles and Mechanisms

### The Probabilistic Foundation of Recursive Estimation

At its core, [state estimation](@entry_id:169668) is a problem of inferring the unobservable internal state of a dynamic system from a sequence of noisy measurements. The mathematical framework for this problem is rooted in probability theory. We consider a discrete-time nonlinear [stochastic system](@entry_id:177599) described by a state transition model and a measurement model:
$$
x_{k+1} = f(x_k, u_k) + w_k
$$
$$
y_k = h(x_k, u_k) + v_k
$$
Here, $x_k \in \mathbb{R}^n$ represents the state vector at time $k$, $u_k \in \mathbb{R}^m$ is a known control input, and $y_k \in \mathbb{R}^p$ is the measurement. The terms $w_k$ and $v_k$ represent [unmodeled dynamics](@entry_id:264781) and sensor noise, respectively, and are treated as random variables.

The goal of filtering is to compute the posterior probability density function (PDF) of the current state, $p(x_k | y_{1:k})$, where $y_{1:k} = \{y_1, y_2, \ldots, y_k\}$ is the history of all measurements up to time $k$. This posterior PDF encapsulates all available information about the state.

The possibility of a recursive solution—one that updates the estimate at time $k-1$ to an estimate at time $k$ without reprocessing the entire history of measurements—hinges on a crucial set of [conditional independence](@entry_id:262650) assumptions. These assumptions define the system as a **Hidden Markov Model (HMM)**. Specifically, we assume:

1.  **The Markov Property**: The state at time $k+1$ is conditionally independent of all past states and measurements, given the state at time $k$. The state $x_k$ is a complete summary of the past. Mathematically, $p(x_{k+1} | x_{0:k}, y_{1:k}, u_{0:k}) = p(x_{k+1} | x_k, u_k)$. This arises naturally from our state transition model, where $x_{k+1}$ depends only on $x_k$, $u_k$, and the independent noise term $w_k$.

2.  **Conditional Independence of Measurements**: The measurement at time $k$ is conditionally independent of all other states and measurements, given the current state $x_k$. The measurement $y_k$ depends only on the current state and not on how the system arrived there. Mathematically, $p(y_k | x_{0:k}, y_{1:k-1}, u_{0:k}) = p(y_k | x_k, u_k)$.

Under these assumptions, the [joint probability](@entry_id:266356) density of the state and measurement history factorizes into a product of local conditional densities [@problem_id:2705994]:
$$
p(x_{0:k},y_{1:k} | u_{0:k}) = p(x_0) \prod_{i=0}^{k-1} p(x_{i+1} | x_i, u_i) \prod_{i=1}^{k} p(y_i | x_i, u_i)
$$
This factorization enables a two-step recursive process for propagating the posterior density, known as the general **Bayesian Filter**. Starting with the posterior from the previous step, $p(x_{k-1} | y_{1:k-1})$, the recursion proceeds as follows:

1.  **Prediction (Time Update)**: The prior density for the state at time $k$ is computed by marginalizing over the previous state, using the state transition model. This is an application of the Chapman-Kolmogorov equation.
    $$
    p(x_k | y_{1:k-1}) = \int p(x_k | x_{k-1}, u_{k-1}) p(x_{k-1} | y_{1:k-1}) \, dx_{k-1}
    $$

2.  **Update (Measurement Update)**: The new measurement $y_k$ is incorporated using Bayes' rule to convert the prior density into the posterior density.
    $$
    p(x_k | y_{1:k}) = \frac{p(y_k | x_k, u_k) p(x_k | y_{1:k-1})}{p(y_k | y_{1:k-1})} \propto p(y_k | x_k, u_k) p(x_k | y_{1:k-1})
    $$
This [predict-update cycle](@entry_id:269441) is the theoretical bedrock of all Kalman filtering variants. For general nonlinear functions $f$ and $h$ and arbitrary noise distributions, these integrals are intractable. The Extended Kalman Filter provides a tractable, albeit approximate, solution by assuming all distributions are Gaussian and linearizing the [system dynamics](@entry_id:136288).

### The Extended Kalman Filter as a Gaussian Approximation

The central premise of the Kalman filter family, including the EKF, is to represent the state's probability distribution by its first two moments: the **mean** (the state estimate, $\hat{x}$) and the **covariance** (the uncertainty of the estimate, $P$). For a linear system with Gaussian noise, an initially Gaussian state distribution remains Gaussian after every prediction and update step. The standard Kalman filter provides the exact equations for propagating this mean and covariance.

However, when a Gaussian random variable is passed through a nonlinear function, the resulting distribution is generally non-Gaussian. The EKF confronts this challenge by making a crucial approximation: at each step, it approximates the nonlinear function with a linear one using a first-order Taylor series expansion around the current state estimate. This [local linearization](@entry_id:169489) allows the filter to operate within the Gaussian world, using the familiar linear Kalman filter equations on the approximated system.

If the system dynamics and measurement models are truly linear, i.e., $f(x,u) = A_k x + B_k u$ and $h(x,u) = C_k x + D_k u$, then the Jacobians computed by the EKF become constant matrices ($F_k = A_k, H_k = C_k$). The Taylor expansion becomes exact, and the EKF algorithm reduces precisely to the standard linear Kalman filter [@problem_id:2706004]. Thus, the EKF can be understood as a local application of the linear Kalman filter at each time step.

### The EKF Algorithm: A Step-by-Step Derivation

Let us assume that at the end of step $k-1$, we have a posterior state estimate $\hat{x}_{k-1|k-1}$ and its [error covariance](@entry_id:194780) $P_{k-1|k-1}$. The [estimation error](@entry_id:263890) is defined as $\tilde{x}_{k-1|k-1} = x_{k-1} - \hat{x}_{k-1|k-1}$, and its covariance is $P_{k-1|k-1} = \mathbb{E}[\tilde{x}_{k-1|k-1} \tilde{x}_{k-1|k-1}^\top]$. The EKF algorithm proceeds in two stages.

#### The Prediction Step (Time Update)

The goal of the prediction step is to project the state estimate and its covariance forward in time, from step $k-1$ to step $k$, using the system's dynamic model.

**State Prediction**: The most straightforward guess for the state at time $k$ is to propagate the previous best estimate through the nonlinear dynamics function, ignoring the noise term (whose mean is assumed to be zero). This yields the *a priori* state estimate:
$$
\hat{x}_{k|k-1} = f(\hat{x}_{k-1|k-1}, u_{k-1})
$$

**Covariance Prediction**: To propagate the covariance, we must analyze the propagation of the estimation error. The *a priori* error is $\tilde{x}_{k|k-1} = x_k - \hat{x}_{k|k-1}$.
$$
\tilde{x}_{k|k-1} = (f(x_{k-1}, u_{k-1}) + w_{k-1}) - f(\hat{x}_{k-1|k-1}, u_{k-1})
$$
Here we linearize the function $f$ around the posterior estimate from the previous step, $\hat{x}_{k-1|k-1}$:
$$
f(x_{k-1}, u_{k-1}) \approx f(\hat{x}_{k-1|k-1}, u_{k-1}) + F_k (x_{k-1} - \hat{x}_{k-1|k-1})
$$
where $F_k$ is the **state-transition Jacobian**, defined as:
$$
F_k = \left. \frac{\partial f}{\partial x} \right|_{(\hat{x}_{k-1|k-1}, u_{k-1})}
$$
Substituting the [linearization](@entry_id:267670) into the error equation gives:
$$
\tilde{x}_{k|k-1} \approx F_k \tilde{x}_{k-1|k-1} + w_{k-1}
$$
The *a priori* covariance $P_{k|k-1}$ is the expected value of the outer product of this error:
$$
P_{k|k-1} = \mathbb{E}[\tilde{x}_{k|k-1} \tilde{x}_{k|k-1}^\top] \approx \mathbb{E}[(F_k \tilde{x}_{k-1|k-1} + w_{k-1})(F_k \tilde{x}_{k-1|k-1} + w_{k-1})^\top]
$$
Expanding this expression yields four terms. The cross-terms, such as $\mathbb{E}[F_k \tilde{x}_{k-1|k-1} w_{k-1}^\top]$, vanish due to the fundamental noise assumptions [@problem_id:2705963]. Specifically, we assume the [process noise](@entry_id:270644) $w_k$ is **zero-mean** ($\mathbb{E}[w_k]=0$) and **temporally white** (uncorrelated with past states and noises). Since the error $\tilde{x}_{k-1|k-1}$ is a function of the noise history up to time $k-1$, it is uncorrelated with the new noise $w_{k-1}$. This simplifies the expression to:
$$
P_{k|k-1} \approx F_k \mathbb{E}[\tilde{x}_{k-1|k-1} \tilde{x}_{k-1|k-1}^\top] F_k^\top + \mathbb{E}[w_{k-1} w_{k-1}^\top]
$$
This gives us the final covariance prediction equation:
$$
P_{k|k-1} = F_k P_{k-1|k-1} F_k^\top + Q_{k-1}
$$
where $Q_{k-1}$ is the covariance of the [process noise](@entry_id:270644) $w_{k-1}$. The Jacobian $F_k$ acts to transform the prior uncertainty through the linearized dynamics, while $Q_{k-1}$ adds uncertainty due to the unpredictable nature of the process.

#### The Update Step (Measurement Update)

The update step corrects the *a priori* estimate using the information contained in the new measurement $y_k$.

**Innovation**: The first step is to compute the **innovation** or **measurement residual**, which is the difference between the actual measurement $y_k$ and the measurement predicted from the *a priori* state estimate:
$$
\tilde{y}_k = y_k - h(\hat{x}_{k|k-1}, u_k)
$$
The innovation represents the new information provided by the measurement that was not anticipated by the model.

**Innovation Covariance**: To properly weight this new information, we must compute the uncertainty of the innovation, $S_k = \mathbb{E}[\tilde{y}_k \tilde{y}_k^\top]$. The innovation can be expressed in terms of the *a priori* estimation error by linearizing the measurement function $h$ around the *a priori* estimate $\hat{x}_{k|k-1}$:
$$
\tilde{y}_k = (h(x_k, u_k) + v_k) - h(\hat{x}_{k|k-1}, u_k) \approx H_k \tilde{x}_{k|k-1} + v_k
$$
Here, $H_k$ is the **measurement Jacobian**:
$$
H_k = \left. \frac{\partial h}{\partial x} \right|_{(\hat{x}_{k|k-1}, u_k)}
$$
Note the critical difference in the [linearization](@entry_id:267670) point: for prediction, we linearize around the *last known best estimate* ($\hat{x}_{k-1|k-1}$), while for the update, we linearize around the *current predicted estimate* ($\hat{x}_{k|k-1}$). The calculation of $H_k$ requires the predicted state, as it defines the [operating point](@entry_id:173374) at which the measurement is taken.

The covariance of the linearized innovation is then:
$$
S_k = \mathbb{E}[(H_k \tilde{x}_{k|k-1} + v_k)(H_k \tilde{x}_{k|k-1} + v_k)^\top]
$$
Similar to the prediction step, the cross-term $\mathbb{E}[H_k \tilde{x}_{k|k-1} v_k^\top]$ vanishes. This relies on the assumption that the [measurement noise](@entry_id:275238) $v_k$ is **zero-mean** and **uncorrelated** with the process noise history and initial state, which means it is uncorrelated with the *a priori* error $\tilde{x}_{k|k-1}$. This leaves:
$$
S_k = H_k P_{k|k-1} H_k^\top + R_k
$$
where $R_k$ is the covariance of the [measurement noise](@entry_id:275238) $v_k$. It is important to note that this derivation for $S_k$ only depends on the mean and covariance of the noises, not on their full probability distributions. The Gaussian assumption is not strictly necessary for the [covariance propagation](@entry_id:747989) formulas themselves [@problem_id:2705963].

**Kalman Gain and State Update**: The **Kalman gain**, $K_k$, is computed to provide the optimal blending of the predicted state and the new measurement information. It balances the uncertainty of the prediction ($P_{k|k-1}$) against the uncertainty of the measurement ($R_k$).
$$
K_k = P_{k|k-1} H_k^\top S_k^{-1}
$$
The *a posteriori* state estimate is then formed by correcting the *a priori* estimate with the innovation, scaled by the Kalman gain:
$$
\hat{x}_{k|k} = \hat{x}_{k|k-1} + K_k \tilde{y}_k
$$

**Covariance Update**: Finally, the *a priori* [error covariance](@entry_id:194780) is updated to reflect the reduction in uncertainty resulting from the measurement. The standard update formula is:
$$
P_{k|k} = (I - K_k H_k) P_{k|k-1}
$$
This updated covariance $P_{k|k}$ then serves as the input for the prediction step at the next time instant, completing the recursive cycle.

***
**Example: Jacobians for a Pendulum Model** [@problem_id:2706002]

Consider a simple pendulum model where the state is $x_k = [\theta_k, \omega_k]^\top$, representing angle and angular velocity. The discrete-time dynamics might be:
$$
\begin{aligned}
\theta_k = \theta_{k-1} + \omega_{k-1} \Delta t \\
\omega_k = \omega_{k-1} + \left(-\lambda \sin \theta_{k-1} + \frac{1}{I}u_{k-1}\right) \Delta t
\end{aligned}
$$
And suppose we measure the horizontal position, so the measurement model is $z_k = \sin \theta_k$. The corresponding functions are $f(x, u)$ and $h(x)$.

The state-transition Jacobian $F_k = \frac{\partial f}{\partial x}$ is found by taking [partial derivatives](@entry_id:146280) of the dynamics with respect to $\theta$ and $\omega$:
$$
F_k = \begin{bmatrix}
1 & \Delta t \\
-\lambda(\cos \theta_{k-1}) \Delta t & 1
\end{bmatrix}
$$
This matrix is evaluated at the latest posterior estimate, e.g., $\hat{x}_{k-1|k-1} = [\hat{\theta}_{k-1|k-1}, \hat{\omega}_{k-1|k-1}]^\top$.

The measurement Jacobian $H_k = \frac{\partial h}{\partial x}$ is found by taking [partial derivatives](@entry_id:146280) of the measurement function:
$$
H_k = \begin{bmatrix} \cos \theta_k & 0 \end{bmatrix}
$$
Crucially, this Jacobian must be evaluated at the *a priori* state estimate for the current step, $\hat{x}_{k|k-1} = [\hat{\theta}_{k|k-1}, \hat{\omega}_{k|k-1}]^\top$. This distinction highlights the flow of information in the filter: we predict where we think the state will be, and then we evaluate the local geometry of the measurement space at that predicted point. Conceptually, $F_k$ maps prior uncertainty into predicted uncertainty, while $H_k$ relates state perturbations to measurement perturbations, informing how the innovation corrects the state estimate.
***

### The Achilles' Heel: Linearization Error

The elegance of the EKF comes at a price. By approximating nonlinear functions with linear ones, the filter introduces **[linearization error](@entry_id:751298)**. This error is the primary reason for the EKF's potential sub-optimality and divergence.

#### The Nature and Magnitude of Linearization Error

The error in a first-order Taylor approximation is captured by the higher-order terms in the series. For a twice-[differentiable function](@entry_id:144590) $f$, the [remainder term](@entry_id:159839) can be bounded. A rigorous analysis shows that the norm of the [linearization error](@entry_id:751298), $\|f(x) - f(\mu) - J_f(\mu)(x-\mu)\|$, is bounded by a term proportional to $\|x-\mu\|^2$ [@problem_id:2705990]. The constant of proportionality is related to the curvature of the function, which is captured by its second derivatives (the Hessian matrix).

More formally, if the Jacobian of $f$ is Lipschitz continuous with constant $L_f$ in a ball of radius $\delta$ around the linearization point $\mu$, the [linearization error](@entry_id:751298) is bounded by $\frac{L_f}{2}\delta^2$. This provides a quantitative way to understand the "region of validity" for the EKF's approximation. The linearization is only accurate if the state uncertainty (represented by the covariance matrix $P$) is small enough that the state stays within a region where the function is nearly linear.

#### Consequences of Linearization Error

When the nonlinearity is significant across the span of the state uncertainty (e.g., when the covariance $P$ is large, or when the function has high curvature), the [first-order approximation](@entry_id:147559) becomes poor. This has two detrimental effects [@problem_id:2706001]:

1.  **Biased Innovation**: The EKF assumes the innovation is zero-mean. However, the unmodeled second-order terms in the Taylor expansion of $h(x)$ can introduce a [systematic bias](@entry_id:167872) into the true innovation. For example, for a [convex function](@entry_id:143191), the mean of the transformed variable will be higher than the transformation of the mean, a discrepancy the EKF misses.

2.  **Incorrect Innovation Covariance**: The EKF's calculated innovation covariance, $S_k = H_k P_{k|k-1} H_k^\top + R_k$, only accounts for the uncertainty propagated through the linearized model. The true innovation covariance is larger due to the unmodeled variance introduced by the higher-order terms.

The combination of a biased innovation and an underestimated innovation covariance is a recipe for divergence. The filter becomes **overconfident**: it trusts its flawed model too much, calculates an overly optimistic (small) [posterior covariance](@entry_id:753630) $P_{k|k}$, and assigns too much weight to the biased innovation, leading to inaccurate state updates.

#### Consistency and Diagnostics

A filter is said to be **consistent** if its estimates are unbiased and its reported covariance matrix accurately reflects the true covariance of the estimation error. For a consistent EKF, the calculated covariance $P_{k|k}$ serves as a meaningful statistical quantity, representing a first-order approximation of the true [error covariance](@entry_id:194780) $\mathbb{E}[\tilde{x}_{k|k} \tilde{x}_{k|k}^\top]$ [@problem_id:2705968].

Detecting inconsistency is crucial for practical applications. Since the true state is unknown, we cannot directly check the estimation error. Instead, we perform statistical tests on the [innovation sequence](@entry_id:181232), which is computable from the filter's outputs.

The primary tool for this is the **Normalized Innovation Squared (NIS)** test. The NIS for step $k$ is defined as:
$$
\eta_k = \tilde{y}_k^\top S_k^{-1} \tilde{y}_k
$$
If the filter is consistent and its underlying assumptions hold (including negligible [linearization error](@entry_id:751298)), the innovation $\tilde{y}_k$ is approximately a zero-mean Gaussian with covariance $S_k$. Consequently, the NIS statistic $\eta_k$ follows a **chi-square ($\chi^2$) distribution** with $p$ degrees of freedom, where $p$ is the dimension of the measurement vector.

By monitoring the time series of $\eta_k$, we can check for [statistical consistency](@entry_id:162814). If the filter is overconfident due to [linearization](@entry_id:267670) errors, the true innovation will be stochastically larger than what the filter's $S_k$ predicts. This will cause the NIS values to be systematically larger than expected, persistently exceeding the upper confidence bounds of the $\chi^2_p$ distribution (e.g., the 95% quantile). This provides a powerful online diagnostic for [filter divergence](@entry_id:749356) [@problem_id:2706001] [@problem_id:2705968]. For offline analysis where the true state trajectory is known (e.g., in simulation), a similar metric called the **Normalized Estimation Error Squared (NEES)**, $\epsilon_k = \tilde{x}_{k|k}^\top P_{k|k}^{-1} \tilde{x}_{k|k}$, can be used. It should follow a $\chi^2_n$ distribution.

### Advanced Topics in EKF Theory and Practice

#### Stability and Convergence

A natural question arises: under what conditions can we guarantee that the EKF will work? While [global convergence](@entry_id:635436) guarantees are rare for [nonlinear systems](@entry_id:168347), a rich body of theory provides conditions for [local stability](@entry_id:751408). For the estimation error $e(t) = x(t) - \hat{x}(t)$ to converge to zero, the error dynamics must be stable. The key components for ensuring this are [observability](@entry_id:152062) and bounded [model uncertainty](@entry_id:265539) [@problem_id:2705980].

A sufficient set of conditions for local [exponential convergence](@entry_id:142080) of the EKF error includes:
1.  **Boundedness and Smoothness**: The system's true trajectory lies within a region where the nonlinear functions $f$ and $h$ are sufficiently smooth (e.g., twice continuously differentiable), ensuring that [linearization](@entry_id:267670) errors are quadratically bounded by the [estimation error](@entry_id:263890).
2.  **Uniform Complete Observability (UCO)**: The linearized system, defined by the pair of Jacobians $(F_k, H_k)$ evaluated along the trajectory, must be uniformly completely observable. Intuitively, this means that over any finite time window, the measurements provide enough information to unambiguously distinguish any two distinct initial states. Observability ensures that the filter gain does not vanish and that all modes of the [estimation error](@entry_id:263890) can be corrected by measurements.
3.  **Sufficient Excitation**: The design [process noise covariance](@entry_id:186358) $Q_k$ must be uniformly positive definite. This prevents the filter from becoming overconfident in its dynamic model and ensures that the [error covariance](@entry_id:194780) $P_k$ remains bounded away from zero, keeping the filter "open" to new information.

Under these conditions, the solution to the filter's Riccati equation for the covariance remains bounded, which in turn guarantees that the linear part of the error dynamics is exponentially stable. For a sufficiently small initial estimation error, this stable linear part will dominate the quadratic [linearization](@entry_id:267670) errors, driving the estimation error to zero.

#### Numerical Implementation and Stability

Beyond theoretical convergence, practical implementation on finite-precision computers introduces numerical challenges. The covariance matrix $P_k$ must, by definition, be symmetric and positive semidefinite. However, the standard covariance update formula, $P_{k|k} = P_{k|k-1} - K_k H_k P_{k|k-1}$, is prone to [numerical instability](@entry_id:137058) [@problem_id:2705984].

When a measurement is very precise, the term being subtracted ($K_k H_k P_{k|k-1}$) can be very close in magnitude to the term it is subtracted from ($P_{k|k-1}$). This can lead to **[catastrophic cancellation](@entry_id:137443)**, where rounding errors result in a computed $P_{k|k}$ that is no longer symmetric or, worse, loses [positive semidefiniteness](@entry_id:147720) (i.e., develops negative eigenvalues). Simply enforcing symmetry by averaging with the transpose, e.g., $P \leftarrow (P+P^\top)/2$, is not sufficient to restore [positive semidefiniteness](@entry_id:147720).

To mitigate this, numerically stable formulations of the covariance update are used:

1.  **Joseph Form**: An algebraically equivalent but numerically superior version of the update is the Joseph form:
    $$
    P_{k|k} = (I - K_k H_k) P_{k|k-1} (I - K_k H_k)^\top + K_k R_k K_k^\top
    $$
    This form computes the [posterior covariance](@entry_id:753630) as the sum of two [positive semidefinite matrices](@entry_id:202354), which is mathematically guaranteed to be positive semidefinite. It avoids the [subtractive cancellation](@entry_id:172005) and is thus far more robust to rounding errors.

2.  **Square-Root Filtering**: For maximum numerical stability, **square-root filters** are employed. Instead of propagating the covariance matrix $P$ itself, these methods propagate a [matrix square root](@entry_id:158930) $S$ such that $P = S S^\top$ (e.g., the Cholesky factor). The predict and update steps are reformulated to operate directly on $S$. These updates often use numerically stable orthogonal transformations (e.g., via QR factorization), which avoids the explicit formation and inversion of the innovation covariance matrix $S_k$ and guarantees that the resulting covariance remains positive semidefinite by construction. This also improves the [numerical conditioning](@entry_id:136760) of the problem, as the condition number of $S$ is the square root of the condition number of $P$.

### Beyond First-Order: A Glimpse at Higher-Order Filters

The Extended Kalman Filter's reliance on first-order linearization is both its strength (simplicity) and its weakness. When nonlinearities are significant, its performance can be poor. To illustrate, consider a simple scalar state $x \sim \mathcal{N}(0, P)$ and a quadratic measurement $y=x^2$ [@problem_id:2705954].

-   The **true** expected value of the measurement is $\mathbb{E}[y] = \mathbb{E}[x^2] = P$.
-   The **EKF**, linearizing at the mean $\mu=0$, predicts $\hat{y} = 0^2 = 0$.

The EKF introduces a significant bias by completely ignoring the function's curvature. This motivates the development of filters that can better handle nonlinearity:

-   **Second-Order EKF (SOEKF)**: This filter includes the second-order term from the Taylor expansion to correct the mean prediction. For the example above, it adds a correction term proportional to the Hessian, correctly predicting $\mathbb{E}[y] = P$. However, it requires computing and manipulating Hessian matrices, which can be computationally burdensome.

-   **Unscented Kalman Filter (UKF)**: The UKF takes a different approach. Instead of linearizing the function, it approximates the probability distribution itself. It uses a small set of deterministically chosen "[sigma points](@entry_id:171701)" that capture the mean and covariance of the state distribution. These points are propagated individually through the true nonlinear function, and the mean and covariance of the transformed points are then calculated. For the $y=x^2$ example, a standard UKF correctly computes the mean $\mathbb{E}[y] = P$ and can also exactly capture the true variance of $y$.

The UKF and other related sigma-point filters generally provide superior accuracy to the EKF for highly nonlinear systems, often at a comparable computational cost, without requiring the analytical derivation of Jacobians. They represent the next step in advancing beyond the fundamental, yet limited, principles of the Extended Kalman Filter.