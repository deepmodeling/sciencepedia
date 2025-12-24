## Introduction

In an era defined by intelligent systems, from autonomous vehicles to digital twins, the ability to build a reliable understanding of the world from sensor data is critical. Sensor fusion is the discipline that provides the framework for this task, enabling systems to intelligently combine information from multiple, often noisy and incomplete, sources. By integrating data, a system can achieve a state estimate that is more accurate, robust, and comprehensive than what any single sensor could provide. The fundamental challenge addressed by [sensor fusion](@entry_id:263414) is how to mathematically merge these disparate data streams, each with unique error characteristics, to produce a single, coherent estimate while rigorously quantifying the uncertainty of that result.

This article serves as a foundational guide to the theory and practice of sensor fusion. We will journey from the mathematical bedrock of probabilistic estimation to the powerful algorithms that are staples of modern engineering and science. You will gain insight into not just the mechanics of these methods, but also the principles that govern their application. This exploration is structured across three key sections. First, in **"Principles and Mechanisms,"** we will dissect the core theory of probabilistic [state representation](@entry_id:141201), [state-space modeling](@entry_id:180240), and the recursive Bayesian filtering paradigm, culminating in the mechanics of the Kalman Filter and its nonlinear extensions. Next, **"Applications and Interdisciplinary Connections"** will showcase these concepts in action, highlighting their impact on robotics, healthcare, and [environmental monitoring](@entry_id:196500). Finally, the **"Hands-On Practices"** section offers a chance to apply this knowledge to concrete problems. We will now begin our detailed study of the foundational **Principles and Mechanisms** that underpin all of [sensor fusion](@entry_id:263414).

## Principles and Mechanisms

In the preceding section, we introduced the conceptual framework of sensor fusion within cyber-physical systems and their digital twins. We established that the core task is to estimate a system's latent state by integrating information from multiple, often imperfect, sources. This section delves into the fundamental principles and mathematical mechanisms that make this possible. We will begin by formalizing how to represent and quantify uncertainty, proceed to construct the standard models for [system dynamics](@entry_id:136288) and measurements, and then explore the computational engines—filters—that recursively refine our knowledge of the state in light of new evidence.

### Foundations of Probabilistic State Representation

A central tenet of modern sensor fusion is that the state of a system is never known with absolute certainty. Consequently, we do not represent the state $x$ as a single point value, but rather as a probability distribution that reflects our belief about its possible values. While many forms of distributions exist, the most prevalent and computationally tractable representation, especially within the Kalman filtering family, is defined by its first two moments: the **mean** and the **covariance**.

The mean, or expected value $\mu = \mathbb{E}[x]$, represents our best guess for the state, corresponding to the center of mass of the probability distribution. The covariance, however, is what quantifies the uncertainty surrounding this guess.

#### The Covariance Matrix: Quantifying Uncertainty

For an $n$-dimensional state vector $x$, the **covariance matrix** $\Sigma$ is a crucial $n \times n$ matrix that summarizes the dispersion and correlation of the [state variables](@entry_id:138790). It is formally defined as the expected value of the [outer product](@entry_id:201262) of the state's deviation from its mean with itself:

$$
\Sigma = \mathbb{E}[(x - \mu)(x - \mu)^\top]
$$

Each element $\Sigma_{ij}$ of this matrix represents the covariance between the $i$-th and $j$-th components of the state vector, $\Sigma_{ij} = \operatorname{Cov}(x_i, x_j)$. The diagonal elements $\Sigma_{ii}$ are the variances of individual components, $\operatorname{Var}(x_i)$, quantifying the uncertainty in each state variable independently. The off-diagonal elements describe how the uncertainties in different state variables are related; a non-zero $\Sigma_{ij}$ indicates that if $x_i$ deviates from its mean, $x_j$ is also likely to deviate in a correlated manner.

A valid covariance matrix must possess two fundamental properties: it must be **symmetric** and **positive semidefinite** .

1.  **Symmetry**: A matrix $\Sigma$ is symmetric if $\Sigma = \Sigma^\top$. The symmetry of the covariance matrix is a direct consequence of its definition. The [outer product](@entry_id:201262) $(x - \mu)(x - \mu)^\top$ is itself a [symmetric matrix](@entry_id:143130) for any realization of the random vector $x$. Since the expectation operator is a linear, element-wise operation, the expectation of a symmetric random matrix is also symmetric. Thus, $\Sigma^\top = \mathbb{E}[((x - \mu)(x - \mu)^\top)^\top] = \mathbb{E}[(x - \mu)(x - \mu)^\top] = \Sigma$.

2.  **Positive Semidefiniteness (PSD)**: A symmetric matrix $\Sigma$ is positive semidefinite if for any non-zero vector $v \in \mathbb{R}^n$, the quadratic form $v^\top \Sigma v \ge 0$. To see why this must hold, we can substitute the definition of $\Sigma$:
    $$
    v^\top \Sigma v = v^\top \mathbb{E}[(x - \mu)(x - \mu)^\top] v
    $$
    By the [linearity of expectation](@entry_id:273513), we can move the constant vector $v$ inside:
    $$
    v^\top \Sigma v = \mathbb{E}[v^\top (x - \mu)(x - \mu)^\top v]
    $$
    The expression inside the expectation can be rewritten by recognizing that $v^\top(x-\mu)$ is a scalar. Let $s = v^\top(x-\mu)$. Then the expression is $\mathbb{E}[s \cdot s^\top] = \mathbb{E}[s^2]$. Therefore:
    $$
    v^\top \Sigma v = \mathbb{E}[(v^\top(x - \mu))^2]
    $$
    Since the square of any real number is non-negative, the quantity $(v^\top(x - \mu))^2$ is always greater than or equal to zero. The expectation of a non-negative random variable must also be non-negative. This proves that $\Sigma$ is positive semidefinite.

Geometrically, the covariance matrix defines an **uncertainty ellipsoid** in the state space centered at the mean $\mu$. This [ellipsoid](@entry_id:165811) is the set of points $y$ satisfying $(y-\mu)^\top \Sigma^{-1} (y-\mu) \le c^2$ for some constant $c$. The principal axes of the [ellipsoid](@entry_id:165811) are aligned with the eigenvectors of $\Sigma$, and the length of these axes are proportional to the square roots of the corresponding eigenvalues.

If $\Sigma$ is **positive definite (SPD)**, meaning $v^\top \Sigma v > 0$ for all non-zero $v$, then all its eigenvalues are strictly positive. In this case, $\Sigma$ is invertible, and the uncertainty ellipsoid is non-degenerate, having volume in $\mathbb{R}^n$. This signifies that there is uncertainty in every direction of the state space. If, however, $\Sigma$ is PSD but not SPD (i.e., it is singular), it has at least one zero eigenvalue. This implies that there is zero uncertainty along the direction of the corresponding eigenvector—the state is known to lie on a lower-dimensional subspace. The resulting uncertainty [ellipsoid](@entry_id:165811) is degenerate, or "flat" .

### Modeling the System: The State-Space Representation

To perform sensor fusion, we must first construct a mathematical model of the system we are observing. In discrete-time filtering, this is typically done using a **[state-space representation](@entry_id:147149)**, which consists of two core equations: a process model and a measurement model.

#### The Process Model: How the State Evolves

The **process model** (or dynamics model) describes how the system's state $x_k$ at time step $k$ evolves into the state $x_{k+1}$ at the next time step. A general form is:
$$
x_{k+1} = f(x_k, u_k) + w_k
$$
Here, $f(\cdot)$ is a function, which can be linear or nonlinear, that describes the deterministic physics or kinematics of the system. The vector $u_k$ represents any known control inputs applied to the system (e.g., motor commands). The term $w_k$ is the **process noise**. This crucial component represents the uncertainty in the system's evolution. It accounts for all factors not captured by the deterministic model $f(\cdot)$, such as unmodeled forces (e.g., wind gusts on a drone), actuator inaccuracies, or simplifications made in the formulation of $f(\cdot)$.

#### The Measurement Model: How the State is Observed

The **measurement model** describes the relationship between the latent state $x_k$ and the actual measurement $z_k$ obtained from a sensor at time $k$:
$$
z_k = h(x_k) + v_k
$$
The function $h(\cdot)$, which can also be linear or nonlinear, maps the state vector into the measurement space. For instance, it might describe the geometric projection that relates a robot's 3D position (the state) to the 2D pixel coordinates of a landmark in an image (the measurement). The term $v_k$ is the **measurement noise**, which accounts for inaccuracies and stochastic errors inherent in the sensing process itself.

As a concrete example, consider a robot navigating a plane, whose state includes its position $(p_x, p_y)$ and heading $\psi$. A camera on the robot measures the bearing to a known static landmark at $(L_x, L_y)$. The ideal, noise-free measurement is a geometric quantity. The bearing of the landmark in the world frame is $\alpha = \mathrm{atan2}(L_y - p_y, L_x - p_x)$. The bearing relative to the robot's body frame is this world-frame angle minus the robot's own heading. Thus, the measurement function $h(\cdot)$ is:
$$
h(x_k) = \mathrm{atan2}(L_y - p_y, L_x - p_x) - \psi
$$
where the state is $x_k = [p_x, p_y, \psi]^\top$. The actual sensor reading $z_k$ would be this ideal value plus some noise $v_k$ .

#### Characterizing the Noise

The process noise $w_k$ and measurement noise $v_k$ are fundamentally different in their physical origin. Process noise arises from the system's interaction with its environment and its own internal imperfections, affecting the *actual* [state evolution](@entry_id:755365). Measurement noise arises from the sensor's hardware and signal processing, affecting the *observation* of the state .

In many filtering applications, a simplifying set of assumptions known as the **Additive White Gaussian Noise (AWGN)** model is used. This model is justified under a specific set of physical and statistical conditions :

*   **Additive**: The noise is assumed to be simply added to the ideal model output. This is a good approximation if the physical noise sources are small, allowing for a first-order Taylor expansion of a more complex true noise model. It breaks down in cases of sensor saturation or large, nonlinear distortions.
*   **Gaussian**: The noise is assumed to follow a Gaussian (Normal) distribution. The primary justification for this is the **Central Limit Theorem**, which states that the sum of many small, independent random disturbances will tend toward a Gaussian distribution, even if the individual sources are not Gaussian. For a camera, these sources might include thermal noise, shot noise, and quantization errors.
*   **Zero-Mean**: The noise is assumed to have an expected value of zero, $\mathbb{E}[v_k] = 0$. This implies the absence of [systematic errors](@entry_id:755765) or **biases**. For this to hold, the sensor must be well-calibrated. Any uncorrected systematic effect would manifest as a non-zero mean.
*   **White**: The noise is assumed to be "white" in time, meaning the noise at one time step is statistically uncorrelated with the noise at any other time step ($\mathbb{E}[v_k v_j^\top] = 0$ for $k \neq j$). This approximation is valid if the sensor's sampling interval is much longer than the [correlation time](@entry_id:176698) of the underlying physical noise phenomena (e.g., [electronic noise](@entry_id:894877) is very fast). It is violated by slow-drifting errors, such as thermal bias in a [gyroscope](@entry_id:172950).

Furthermore, a critical assumption in standard [filter design](@entry_id:266363) is that the [process noise](@entry_id:270644) sequence $\{w_k\}$ and the measurement noise sequence $\{v_k\}$ are **mutually independent**. This means $\mathbb{E}[w_k v_j^\top] = 0$ for all time indices $k$ and $j$. This is physically plausible as they arise from distinct phenomena. This independence simplifies the filter mathematics considerably.

Finally, we must consider the relationship between the noise and the state itself. A system is non-anticipative, meaning future noise cannot affect the present state. Therefore, the process noise $w_k$ is independent of the state $x_j$ and measurement $z_j$ for all past and present times $j \le k$. This implies that the [cross-correlation](@entry_id:143353) $\mathbb{E}[w_k z_j^\top] = 0$ for $j \le k$. However, for a future time $j > k$, the state $x_j$ will depend on $w_k$ through the [system dynamics](@entry_id:136288). Consequently, the measurement $z_j$ will also depend on $w_k$, and their correlation $\mathbb{E}[w_k z_j^\top]$ will generally be non-zero .

### The Bayesian Filtering Paradigm

With the state-space model established, we can now address the core estimation problem. The **Bayesian filtering** framework provides a recursive two-step procedure for updating our belief about the state as new measurements become available. The two steps are **Prediction** and **Update**.

1.  **Prediction**: Given the state distribution at time $k-1$, $p(x_{k-1} | z_{1:k-1})$, the prediction step uses the process model to compute the *prior* distribution for the state at time $k$, before the new measurement is incorporated: $p(x_k | z_{1:k-1})$.

2.  **Update**: Once the measurement $z_k$ is received, the update step uses the measurement model to correct the prior distribution, yielding the refined *posterior* distribution for the state at time $k$: $p(x_k | z_{1:k})$.

This cycle then repeats, with the new posterior serving as the basis for the next prediction.

#### Bayes' Theorem: The Engine of the Update

The mathematical engine driving the update step is **Bayes' Theorem**. In the context of filtering, it is written as:
$$
p(x_k | z_k) \propto p(z_k | x_k) \, p(x_k)
$$
Here, $p(x_k)$ is the [prior distribution](@entry_id:141376) from the prediction step. The term $p(z_k | x_k)$ is the **likelihood**, which is specified by the measurement model and quantifies how probable the observed measurement $z_k$ is for a given hypothesized state $x_k$. The result, $p(x_k | z_k)$, is the posterior distribution, representing our updated belief after considering the measurement.

The **prior** distribution, which for the very first step is $p(x_0)$, plays a crucial role in initializing the filter. The choice of the initial prior mean $m_0$ and covariance $P_0$ represents all knowledge about the system before any measurements are taken. The confidence in this prior knowledge, encoded in the magnitude of $P_0$, significantly impacts the filter's initial behavior .

Consider a simple static estimation problem where we estimate a scalar value $x$ from a measurement $z = x+v$. If our prior belief is $x \sim \mathcal{N}(m_0, P_0)$ and the noise is $v \sim \mathcal{N}(0, R)$, the posterior variance will be $P_1 = (P_0^{-1} + R^{-1})^{-1}$. If we choose a very small prior variance $P_0$, we are stating that we are highly confident in our initial guess $m_0$. Consequently, the posterior variance $P_1$ will be dominated by $P_0$, and the updated mean will barely move from $m_0$. The filter will appear "stubborn" and less sensitive to the new data.

Conversely, if we are very uncertain about the initial state, we would choose a large $P_0$. In the long run, however, as more and more measurements are fused, the influence of the initial prior diminishes. For a correctly specified model, the [posterior mean](@entry_id:173826) will converge towards the true state, and the posterior distribution will become dominated by the accumulated information from the data (the likelihood). The initial bias introduced by a poorly chosen $m_0$ will decay, typically at a rate proportional to $1/n$ where $n$ is the number of measurements .

### Mechanisms of Linear Filtering: The Kalman Filter

The general Bayesian filtering paradigm is elegant but often computationally intractable. However, for the special case of a **linear-Gaussian system**, there exists a closed-form, [optimal solution](@entry_id:171456): the **Kalman Filter**. The system must adhere to the form:
$$
x_{k+1} = Fx_k + Bu_k + w_k, \quad w_k \sim \mathcal{N}(0, Q)
$$
$$
z_k = Hx_k + v_k, \quad v_k \sim \mathcal{N}(0, R)
$$
where $F, B, H$ are matrices. In this case, if the initial state is Gaussian, the state distribution remains Gaussian at every subsequent step. The filter's task simplifies to propagating the mean and covariance of this distribution through the prediction and update steps.

#### Mechanism 1: The Prediction Step

The prediction step projects the state estimate forward in time. Given the [posterior mean](@entry_id:173826) $\hat{x}_{k-1|k-1}$ and covariance $P_{k-1|k-1}$ from the previous step, we can derive the predicted (prior) mean $\hat{x}_{k|k-1}$ and covariance $P_{k|k-1}$ for the current step .

The predicted mean is found by taking the expectation of the process model:
$$
\hat{x}_{k|k-1} = E[Fx_{k-1} + Bu_{k-1} + w_{k-1}] = F E[x_{k-1}] + B u_{k-1} + E[w_{k-1}] = F \hat{x}_{k-1|k-1} + B u_{k-1}
$$
The mean simply propagates through the deterministic part of the system dynamics.

The predicted covariance captures the growth of uncertainty. It is derived from the error dynamics and the independence of the state estimate error and process noise:
$$
P_{k|k-1} = F P_{k-1|k-1} F^\top + Q
$$
This equation shows that uncertainty increases for two reasons: the existing uncertainty, $P_{k-1|k-1}$, is transformed by the system dynamics ($F(\cdot)F^\top$), and new uncertainty from the process noise, $Q$, is added.

For example, consider a 1D constant-velocity model with state $x = [p, v]^\top$, dynamics matrix $F = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$ (for a 1s time step), and process noise $Q = \begin{pmatrix} 1 & 0 \\ 0 & 2 \end{pmatrix}$. If the [posterior covariance](@entry_id:753630) at the previous step was $P_{k-1|k-1} = \begin{pmatrix} 2 & 1 \\ 1 & 3 \end{pmatrix}$, the predicted covariance would be:
$$
P_{k|k-1} = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} 2 & 1 \\ 1 & 3 \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 1 & 1 \end{pmatrix} + \begin{pmatrix} 1 & 0 \\ 0 & 2 \end{pmatrix} = \begin{pmatrix} 7 & 4 \\ 4 & 3 \end{pmatrix} + \begin{pmatrix} 1 & 0 \\ 0 & 2 \end{pmatrix} = \begin{pmatrix} 8 & 4 \\ 4 & 5 \end{pmatrix}
$$
The trace of the covariance, a measure of total uncertainty, increases from $2+3=5$ to $8+5=13$ .

#### Mechanism 2: The Update Step

The update step corrects the predicted estimate using the new measurement. For the scalar case $z = x+v$ with prior $x \sim \mathcal{N}(\mu_0, P_0)$ and noise $v \sim \mathcal{N}(0, R)$, the [posterior mean](@entry_id:173826) and variance are :
$$
\hat{x} = \frac{\mu_0 R + z P_0}{P_0 + R}, \quad P = \frac{P_0 R}{P_0 + R}
$$
This update can be expressed in the insightful **innovations form**:
$$
\hat{x} = \mu_0 + K(z - \mu_0), \quad \text{where the Kalman Gain } K = \frac{P_0}{P_0 + R}
$$
The term $(z - \mu_0)$ is the **innovation** or prediction error—the difference between the actual measurement and the predicted measurement. The updated estimate is the predicted estimate plus a correction proportional to this innovation. The **Kalman Gain** $K$ acts as the proportionality constant, balancing the confidence in the prediction (encoded in $P_0$) versus the confidence in the measurement (encoded in $R$).

This logic extends to the multidimensional case, yielding the canonical Kalman filter update equations:
-   Innovation: $\tilde{y}_k = z_k - H\hat{x}_{k|k-1}$
-   Innovation Covariance: $S_k = HP_{k|k-1}H^\top + R$
-   Kalman Gain: $K_k = P_{k|k-1}H^\top S_k^{-1}$
-   Updated Mean: $\hat{x}_{k|k} = \hat{x}_{k|k-1} + K_k\tilde{y}_k$
-   Updated Covariance: $P_{k|k} = (I - K_k H)P_{k|k-1}$

#### Observability: A Condition for Estimation

A Kalman filter can only estimate states that are, in principle, "visible" through the measurements. This property is known as **observability**. For an LTI system, a state is observable if an initial non-zero value for that state will eventually produce a non-zero effect on the measurement output.

Observability is formally tested using the **[observability matrix](@entry_id:165052)**:
$$
\mathcal{O} = \begin{pmatrix} H \\ HF \\ HF^2 \\ \vdots \\ HF^{n-1} \end{pmatrix}
$$
The system pair $(F, H)$ is observable if and only if this matrix has full column rank, i.e., $\operatorname{rank}(\mathcal{O}) = n$.

If a system is not observable, there exists an **[unobservable subspace](@entry_id:176289)**. Any state component within this subspace is invisible to the sensor configuration. For example, consider a system with two decoupled parts: a position-velocity block and a rotation block. If the sensor only measures position, the rotation states are completely uncoupled from the measurement . The [observability matrix](@entry_id:165052) will be rank-deficient, and its [null space](@entry_id:151476) will correspond exactly to the unobservable rotation states.

For the Kalman filter, unobservability means that it cannot reduce the uncertainty of the states in the [unobservable subspace](@entry_id:176289). The Kalman gain components corresponding to these states will be zero. The error covariance for these states will not decrease during the update step and may even grow indefinitely due to process noise. This is a fundamental limitation, not merely a question of convergence rate. However, if the system is observable (and another condition, [stabilizability](@entry_id:178956), holds), the Kalman filter [error covariance](@entry_id:194780) will converge to a unique steady-state value that is independent of the initial [prior covariance](@entry_id:1130174) $P_0$ . Observability can often be achieved by adding more or different sensors to the system .

### Mechanisms of Nonlinear Filtering

Most real-world systems are nonlinear. While the optimal solution is no longer a simple Kalman filter, several powerful approximation techniques exist.

#### The Extended Kalman Filter (EKF): Linearization

The most common approach is the **Extended Kalman Filter (EKF)**. Its core idea is to handle nonlinearity by performing a [local linearization](@entry_id:169489) of the nonlinear process and measurement functions around the current best state estimate. The standard Kalman filter equations are then applied to this approximated linear system.

For the measurement update, the nonlinear function $h(x)$ is approximated using a first-order Taylor [series expansion](@entry_id:142878) around the predicted mean $\bar{x} = \hat{x}_{k|k-1}$:
$$
h(x) \approx h(\bar{x}) + H(\bar{x})(x - \bar{x})
$$
The matrix $H(\bar{x})$ is the **Jacobian matrix** of $h$ evaluated at $\bar{x}$. It is the matrix of all first-order partial derivatives of the function's components with respect to the state variables:
$$
H_{ij}(\bar{x}) = \frac{\partial h_i}{\partial x_j} \bigg|_{x=\bar{x}}
$$
For example, if the state contains 2D position $(p_x, p_y)$ and a sensor measures the range to the origin, $h(x) = \sqrt{p_x^2 + p_y^2}$, the Jacobian is a row vector whose components are $\frac{\partial h}{\partial p_x} = \frac{p_x}{\sqrt{p_x^2+p_y^2}}$ and $\frac{\partial h}{\partial p_y} = \frac{p_y}{\sqrt{p_x^2+p_y^2}}$ . The EKF uses this Jacobian matrix in place of the static $H$ matrix in the Kalman filter update equations.

#### The Unscented Kalman Filter (UKF): Statistical Approximation

A more sophisticated approach is the **Unscented Kalman Filter (UKF)**, which is based on the **Unscented Transform (UT)**. The UT operates on the principle that it is easier to approximate a probability distribution than it is to approximate a nonlinear function.

Instead of linearizing the function, the UT deterministically selects a small set of points, called **[sigma points](@entry_id:171701)**, from the state distribution. These points are chosen and weighted so that their [sample mean](@entry_id:169249) and covariance exactly match the mean $\mu$ and covariance $\Sigma$ of the original Gaussian distribution. A standard scheme for a state of dimension $n$ uses $2n+1$ [sigma points](@entry_id:171701) .

These [sigma points](@entry_id:171701) are then propagated individually through the true nonlinear function, $y_i = g(\chi_i)$. The mean and covariance of the transformed variable are then estimated by computing the weighted sample mean and covariance of the resulting transformed points:
$$
\hat{y} \approx \sum_i W_i^{(m)} y_i, \quad P_y \approx \sum_i W_i^{(c)} (y_i - \hat{y})(y_i - \hat{y})^\top
$$
The key advantage of the UT is its accuracy. By matching the first two moments of the Gaussian distribution, the UT's estimate of the mean is accurate to the *second* order of the function's Taylor expansion. In contrast, the EKF's linearization discards these second-order terms. This allows the UKF to handle strong nonlinearities much more effectively than the EKF, without requiring the analytical derivation of Jacobians.

### Advanced Topic: Fusing Data from Multiple Sensors

When a digital twin receives data from multiple sensors simultaneously, a key question is how to combine their likelihoods.

#### Conditional Independence

The simplest case occurs when the sensor measurements are **conditionally independent** given the state. This means that, if the true state $x$ were known, knowing the measurement from one sensor would provide no additional information about the measurement from another. In this case, the [joint likelihood](@entry_id:750952) is simply the product of the individual likelihoods:
$$
p(y_L, y_C, y_I | x) = p(y_L | x) \, p(y_C | x) \, p(y_I | x)
$$
This allows for a very simple fusion process, where measurements can be processed sequentially.

#### Correlated Measurements

In more complex scenarios, this independence may not hold. A common reason is the presence of an unobserved **nuisance variable** that affects multiple sensors. For example, a sudden change in ambient illumination might affect both a LiDAR and a camera, while also being influenced by sensor-specific biases .

In such cases, simply multiplying the individual likelihoods is incorrect because it ignores the correlation induced by the common disturbance. The rigorous approach is to model the nuisance variables explicitly and then **marginalize** them out using the law of total probability. If $w$ is the common disturbance and $b_L, b_C, b_I$ are independent biases, the correct [joint likelihood](@entry_id:750952) requires integrating over all possible values of these unobserved variables:
$$
p(y_L, y_C, y_I | x, m) = \int p(w) \left( \int p(y_L | \dots, w, b_L)p(b_L)db_L \right) \left( \int p(y_C | \dots, w, b_C)p(b_C)db_C \right) \left( \dots \right) dw
$$
The outer integral over the common disturbance $w$ is what correctly couples the likelihoods of the affected sensors. This principled approach ensures that dependencies between sensors are properly accounted for, leading to a consistent and accurate fused estimate.