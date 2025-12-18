## Introduction
Estimating the hidden states of physiological systems—from drug concentrations in tissue to the underlying drivers of heart rate—is a fundamental challenge in [biomedical engineering](@entry_id:268134). We often rely on indirect and noisy measurements, making it difficult to track how these systems evolve over time. This article provides a rigorous guide to Kalman filtering and its advanced variants, a powerful suite of statistical tools designed to solve exactly these kinds of problems by optimally fusing model-based predictions with sensor data.

This comprehensive overview is structured to build your expertise from the ground up. The first chapter, **Principles and Mechanisms**, delves into the mathematical foundations, starting with the classic linear Kalman filter and its optimality, then progressing to the nonlinear Extended Kalman Filter (EKF) and Unscented Kalman Filter (UKF) essential for real-world biological complexity. Next, the **Applications and Interdisciplinary Connections** chapter bridges theory and practice, demonstrating how to model complex physiological phenomena like [pharmacokinetics](@entry_id:136480) and glucose dynamics, handle real-world data imperfections, and perform advanced tasks like joint parameter estimation. Finally, the **Hands-On Practices** section provides targeted exercises to solidify your understanding of key concepts, from discretizing continuous-time models to calculating the filter's steady-state performance. By progressing through these chapters, you will gain the theoretical knowledge and practical insight needed to apply these powerful estimation techniques to your own biomedical modeling challenges.

## Principles and Mechanisms

The estimation of unobserved physiological states from noisy and indirect measurements is a central challenge in [biomedical systems modeling](@entry_id:1121641). This chapter delves into the principles and mechanisms of Kalman filtering and its powerful extensions, which provide a rigorous framework for solving such estimation problems. We will begin with the foundational linear-Gaussian model, establish the theoretical basis for the Kalman filter's optimality, and then progress to the nonlinear variants—the Extended and Unscented Kalman Filters—that are essential for modeling the complex dynamics inherent in biological systems. Finally, we will explore how these estimates can be further refined using information from the entire time-series through optimal smoothing.

### The Linear-Gaussian State-Space Model

The bedrock of Kalman filtering is the **[state-space representation](@entry_id:147149)**, a mathematical model that describes a system's evolution over time. For a wide range of biomedical applications, from tracking metabolite concentrations to modeling cardiovascular dynamics, a discrete-time linear-Gaussian model provides a powerful and tractable starting point. This model is defined by two core equations:

1.  The **State Equation**, which describes how the system's internal state evolves from one time step to the next:
    $x_{k+1} = A x_k + B u_k + w_k$

2.  The **Measurement Equation**, which relates the internal state to the observable sensor measurements:
    $y_k = C x_k + v_k$

Let us deconstruct each component of this model:

-   The **state vector** $x_k \in \mathbb{R}^n$ represents the collection of unobserved, or latent, physiological variables at a [discrete time](@entry_id:637509) step $k$. These could be, for example, the concentration of glucose in different body compartments, latent variables describing autonomic nervous system tone, or compartmental flows in a hormone-regulation model.

-   The **[state transition matrix](@entry_id:267928)** $A$ governs the autonomous dynamics of the system. It models how the physiological state at time $k$ would evolve to time $k+1$ in the absence of external inputs or random disturbances. For instance, it might encode the natural rates of clearance or metabolic conversion of a substance.

-   The **input vector** $u_k \in \mathbb{R}^p$ represents known external stimuli or interventions, such as an administered drug dose, a controlled pacing signal in a cardiac experiment, or a defined meal intake in a glucose model. The **input matrix** $B$ maps these inputs to their effect on the state dynamics.

-   The **measurement vector** $y_k \in \mathbb{R}^m$ is the output from our sensors, such as a blood glucose reading from a continuous glucose monitor (CGM) or an oxygen saturation level derived from [photoplethysmography](@entry_id:898778). The **observation matrix** $C$ maps the unobserved state vector $x_k$ to the expected measurement $y_k$. 

A crucial aspect of this model is the explicit accounting for uncertainty, represented by the noise terms $w_k$ and $v_k$.

-   The **process noise** $w_k$ represents the uncertainty in the state dynamics. It accounts for unmodeled physiological variability, random fluctuations, and simplifications made in the model $A x_k + B u_k$. For example, in a model of cardiac dynamics, $w_k$ might represent unpredictable variations in [autonomic tone](@entry_id:151146) that are not captured by the deterministic part of the model.

-   The **measurement noise** $v_k$ represents the uncertainty in the sensor readings. It accounts for sensor inaccuracies, electronic noise, and other random measurement errors.

In the standard Kalman filter framework, we make several key assumptions about these noise processes. We assume they are **zero-mean Gaussian** processes, meaning they have no [systematic bias](@entry_id:167872) and their amplitudes follow a normal distribution. We also assume they are **temporally white**, meaning the noise at one time step is uncorrelated with the noise at any other time step. Formally, for $j \neq k$:
$$
\mathbb{E}[w_k] = 0, \quad \mathbb{E}[v_k] = 0, \quad \mathbb{E}[w_k w_j^\top] = 0, \quad \mathbb{E}[v_k v_j^\top] = 0
$$
Furthermore, we assume the process and measurement noises are mutually independent. The magnitudes of these noises are characterized by their covariance matrices:
$$
Q = \mathbb{E}[w_k w_k^\top], \quad R = \mathbb{E}[v_k v_k^\top]
$$
The **[process noise covariance](@entry_id:186358)** $Q$ quantifies the uncertainty we have in our dynamic model, while the **measurement noise covariance** $R$ quantifies the unreliability of our sensors. These assumptions of [linear dynamics](@entry_id:177848) and additive, white, Gaussian noise (the "linear-Gaussian" model) are critical because they lead to a computationally tractable and [optimal estimation](@entry_id:165466) solution. 

### The Kalman Filter: Optimal Estimation for Linear Systems

Given the linear-Gaussian model, our goal is to compute the best possible estimate of the latent state $x_k$ using the history of measurements $y_{1:k} = \{y_1, \dots, y_k\}$. But what does "best" mean?

#### The Principle of Minimum Mean-Square Error

In estimation theory, a standard criterion for optimality is the minimization of the **[mean-square error](@entry_id:194940) (MSE)**. The MSE is the expected value of the squared distance between the true state $x_k$ and our estimate $\hat{x}_k$. The estimator that achieves this minimum is called the **Minimum Mean-Square Error (MMSE)** estimator. It is a fundamental result of Bayesian [estimation theory](@entry_id:268624) that the MMSE estimator is the **conditional mean** of the state given the observation history:
$$
\hat{x}_{k, \text{MMSE}} = \mathbb{E}[x_k \mid y_{1:k}]
$$
This estimator averages all possible values of $x_k$, weighted by their posterior probability after observing the data $y_{1:k}$.

A remarkable property of the linear-Gaussian state-space model is that it makes the computation of this conditional mean tractable. Because the initial state $x_0$ is assumed to be Gaussian and all subsequent states and measurements are formed through [linear transformations](@entry_id:149133) of Gaussian variables ($x_{k-1}, w_{k-1}, v_k$), the [joint distribution](@entry_id:204390) of the state $x_k$ and the entire measurement history $y_{1:k}$ is also Gaussian. A key property of jointly Gaussian distributions is that the conditional mean of one variable given another is an affine (linear plus a constant) function. This means that the optimal MMSE estimator $\mathbb{E}[x_k \mid y_{1:k}]$ is an [affine function](@entry_id:635019) of the measurements $y_{1:k}$, and the Kalman filter provides the exact [recursive algorithm](@entry_id:633952) to compute it. 

#### The Bayesian Recursive Framework

The Kalman filter can be elegantly understood as an algorithm for **recursive Bayesian inference**. At each time step, it computes the posterior probability distribution of the state, $p(x_k | y_{1:k})$, which represents our complete knowledge of $x_k$ given the data so far. Because we are in a linear-Gaussian world, this distribution is always Gaussian and can be completely described by its mean $\hat{x}_{k|k}$ and its covariance $P_{k|k}$.

The [recursion](@entry_id:264696) unfolds in a two-step cycle: **prediction** and **update**.

1.  **Prediction (Time Update):** Starting with the posterior from the previous step, $p(x_{k-1} | y_{1:k-1}) = \mathcal{N}(\hat{x}_{k-1|k-1}, P_{k-1|k-1})$, we use the state equation to predict the distribution of the state at the current time $k$, before seeing the new measurement $y_k$. This gives us the **[prior distribution](@entry_id:141376)** for time $k$:
    $$
    p(x_k | y_{1:k-1}) = \mathcal{N}(\hat{x}_{k|k-1}, P_{k|k-1})
    $$

2.  **Update (Measurement Update):** When the new measurement $y_k$ arrives, it provides new information. The relationship between $y_k$ and $x_k$ is defined by the measurement equation, which gives us the **likelihood** $p(y_k | x_k)$. We then use Bayes' theorem to combine our prior with this likelihood to obtain the updated **posterior distribution**:
    $$
    p(x_k | y_{1:k}) \propto \underbrace{p(y_k | x_k)}_{\text{Likelihood}} \underbrace{p(x_k | y_{1:k-1})}_{\text{Prior}}
    $$
A key property of Gaussian distributions is **[conjugacy](@entry_id:151754)** under a linear-Gaussian model: when a Gaussian prior is multiplied by a Gaussian likelihood, the resulting posterior is also Gaussian. The Kalman filter update equations are precisely the mathematical formulas for the mean and covariance of this new posterior Gaussian distribution. 

#### The Kalman Filter Algorithm

Let's now present the concrete equations for the [predict-update cycle](@entry_id:269441), assuming we have the [posterior mean](@entry_id:173826) $\hat{x}_{k-1|k-1}$ and covariance $P_{k-1|k-1}$ from the previous step. 

**Time Update (Prediction):**
The state mean is propagated forward using the deterministic part of the system model. The covariance is also propagated forward and increased by the [process noise covariance](@entry_id:186358) $Q$, reflecting the added uncertainty from the model dynamics.
$$
\hat{x}_{k|k-1} = A \hat{x}_{k-1|k-1} + B u_{k-1}
$$
$$
P_{k|k-1} = A P_{k-1|k-1} A^{\top} + Q
$$
Here, $\hat{x}_{k|k-1}$ is our best guess of the state at time $k$ based on information up to $k-1$, and $P_{k|k-1}$ is the uncertainty (covariance) of that guess.

**Measurement Update (Correction):**
This step corrects our prediction using the new measurement $y_k$.
1.  First, we calculate the **innovation** or measurement residual, which is the difference between the actual measurement $y_k$ and the predicted measurement $C\hat{x}_{k|k-1}$:
    $$
    \tilde{y}_k = y_k - C \hat{x}_{k|k-1}
    $$
2.  Next, we compute the covariance of this innovation, $S_k$, which combines the projected state uncertainty with the measurement noise:
    $$
    S_k = C P_{k|k-1} C^{\top} + R
    $$
3.  The **Kalman gain** $K_k$ is then computed. This crucial matrix determines how much we correct our predicted state based on the innovation:
    $$
    K_k = P_{k|k-1} C^{\top} S_k^{-1}
    $$
4.  Finally, we update the state mean and covariance to obtain the posterior for time $k$:
    $$
    \hat{x}_{k|k} = \hat{x}_{k|k-1} + K_k \tilde{y}_k
    $$
    $$
    P_{k|k} = (I - K_k C) P_{k|k-1}
    $$
The updated state $\hat{x}_{k|k}$ is our new best estimate, and $P_{k|k}$ represents its (reduced) uncertainty. This cycle then repeats for the next time step. It is important to note that there are several algebraically equivalent forms for the covariance update, such as the more numerically stable Joseph form, $P_{k|k} = (I - K_k C) P_{k|k-1} (I - K_k C)^\top + K_k R K_k^\top$, which is often preferred in practical implementations. 

#### The Intuitive Role of the Kalman Gain

The Kalman gain $K_k$ acts as a "blending factor" that optimally balances the trust we place in our model's prediction versus the new measurement. Its magnitude is directly influenced by the relative uncertainties $Q$ and $R$. 

-   If the **[process noise covariance](@entry_id:186358) $Q$ is large**, it means our dynamic model is uncertain. This leads to a larger predicted covariance $P_{k|k-1}$, which in turn **increases the Kalman gain $K_k$**. A larger gain means we put more trust in the new measurement $y_k$ to correct our uncertain prediction.

-   If the **measurement noise covariance $R$ is large**, it means our sensor is unreliable. This increases the innovation covariance $S_k$, which **decreases the Kalman gain $K_k$**. A smaller gain means we discount the noisy measurement and put more trust in our model's prediction $\hat{x}_{k|k-1}$.

This intuitive behavior is at the heart of the filter's optimality: it dynamically adjusts how it fuses information based on the uncertainties inherent in the system. In both cases (increasing $Q$ or increasing $R$), the overall uncertainty in our final estimate, reflected by the [posterior covariance](@entry_id:753630) $P_{k|k}$, will increase, as we are dealing with a more uncertain system.

### Estimation for Nonlinear Systems

While the linear Kalman filter is powerful, most biological processes are inherently nonlinear. For example, [enzyme kinetics](@entry_id:145769) saturate, and physiological regulatory mechanisms often involve nonlinear feedback. To handle such systems, we use a more general nonlinear [state-space model](@entry_id:273798):
$$
x_{k+1} = f(x_k, u_k) + w_k
$$
$$
y_k = h(x_k) + v_k
$$
Here, $f(\cdot)$ and $h(\cdot)$ are nonlinear functions. When a Gaussian distribution is propagated through a nonlinear function, the result is generally non-Gaussian. This breaks the assumptions of the standard Kalman filter, and an exact, finite-dimensional solution for the posterior distribution is no longer possible. We must therefore resort to approximations. The two most common approaches are the Extended Kalman Filter (EKF) and the Unscented Kalman Filter (UKF).

#### The Extended Kalman Filter (EKF): Approximation by Linearization

The EKF tackles nonlinearity by making a direct approximation: it linearizes the nonlinear functions $f$ and $h$ at each time step using a first-order Taylor [series expansion](@entry_id:142878). The standard Kalman filter equations are then applied to this locally linearized model.

The core of the EKF is the replacement of the static matrices $A$ and $C$ with time-varying **Jacobian matrices**, which are matrices of first-order partial derivatives.

-   $F_{k-1} = \left.\frac{\partial f}{\partial x}\right|_{x=\hat{x}_{k-1|k-1},\,u=u_{k-1}}$
-   $H_k = \left.\frac{\partial h}{\partial x}\right|_{x=\hat{x}_{k|k-1}}$

Notice the points of evaluation: the process model $f$ is linearized around the previous updated state $\hat{x}_{k-1|k-1}$, while the measurement model $h$ is linearized around the current predicted state $\hat{x}_{k|k-1}$.

The EKF algorithm proceeds as follows: 

**Time Update (Prediction):**
The state mean is propagated through the true nonlinear function $f$. The covariance is propagated using the linearized dynamics, represented by the Jacobian $F_{k-1}$.
$$
\hat{x}_{k|k-1} = f(\hat{x}_{k-1|k-1}, u_{k-1})
$$
$$
P_{k|k-1} = F_{k-1} P_{k-1|k-1} F_{k-1}^\top + Q_{k-1}
$$

**Measurement Update (Correction):**
The measurement update also uses the true nonlinear function $h$ for predicting the measurement, but the Jacobian $H_k$ is used for calculating the innovation covariance and Kalman gain.
$$
\tilde{y}_k = y_k - h(\hat{x}_{k|k-1})
$$
$$
S_k = H_k P_{k|k-1} H_k^\top + R_k
$$
$$
K_k = P_{k|k-1} H_k^\top S_k^{-1}
$$
$$
\hat{x}_{k|k} = \hat{x}_{k|k-1} + K_k \tilde{y}_k
$$
$$
P_{k|k} = (I - K_k H_k) P_{k|k-1}
$$

The EKF is a widely used tool, but its performance depends heavily on how well the [local linearization](@entry_id:169489) approximates the true nonlinearity. If the system is highly nonlinear or the state uncertainty is large, this first-order approximation can be inaccurate, leading to poor performance or even divergence of the filter.

#### The Unscented Kalman Filter (UKF): Approximation by Deterministic Sampling

The Unscented Kalman Filter (UKF) offers a different philosophy: instead of approximating the nonlinear functions, it aims to provide a better approximation of the state's probability distribution. The core mechanism is the **Unscented Transform (UT)**, a method for propagating a probability distribution through a nonlinear function using a minimal set of deterministically chosen sample points, called **[sigma points](@entry_id:171701)**.

**The Unscented Transform (UT):**
The UT operates on the principle that it is easier to approximate a Gaussian distribution than it is to approximate an arbitrary nonlinear function. For an $n$-dimensional Gaussian distribution $\mathcal{N}(\mu, P)$, the UT generates a small set of $2n+1$ weighted [sigma points](@entry_id:171701) that completely capture its mean and covariance.

The standard procedure for generating these points is as follows: 
1.  **Choose scaling parameters:** $\alpha, \beta, \kappa$. These parameters control the spread of the [sigma points](@entry_id:171701). Common choices are $\alpha=1$, $\beta=2$ (optimal for Gaussians), and $\kappa=0$.
2.  **Calculate a composite scaling parameter:** $\lambda = \alpha^2(n+\kappa) - n$.
3.  **Generate [sigma points](@entry_id:171701):** Let $S$ be a [matrix square root](@entry_id:158930) of the covariance $P$ (e.g., from Cholesky decomposition, $P=SS^\top$). The $2n+1$ [sigma points](@entry_id:171701) $\mathcal{X}^{(i)}$ are:
    $$
    \begin{align*}
    \mathcal{X}^{(0)} = \mu \\
    \mathcal{X}^{(i)} = \mu + \sqrt{n+\lambda} \, s_i, \quad \text{for } i=1, \dots, n \\
    \mathcal{X}^{(i+n)} = \mu - \sqrt{n+\lambda} \, s_i, \quad \text{for } i=1, \dots, n
    \end{align*}
    $$
    where $s_i$ is the $i$-th column of $S$.
4.  **Define weights:** Two sets of weights are used to recombine the [sigma points](@entry_id:171701) after they are passed through a nonlinear function.
    -   Weights for the mean, $W_m^{(i)}$:
        $$
        W_m^{(0)} = \frac{\lambda}{n+\lambda}, \quad W_m^{(i)} = \frac{1}{2(n+\lambda)} \text{ for } i=1, \dots, 2n
        $$
    -   Weights for the covariance, $W_c^{(i)}$:
        $$
        W_c^{(0)} = \frac{\lambda}{n+\lambda} + (1-\alpha^2+\beta), \quad W_c^{(i)} = \frac{1}{2(n+\lambda)} \text{ for } i=1, \dots, 2n
        $$

To propagate the mean and covariance through a function $h(\cdot)$, we simply pass each sigma point $\mathcal{X}^{(i)}$ through the function to get transformed points $\mathcal{Y}^{(i)} = h(\mathcal{X}^{(i)})$. The mean and covariance of the output are then estimated as the weighted average and weighted sample covariance of these transformed points.

**The UKF Algorithm:**
The UKF replaces the linearization steps of the EKF with the Unscented Transform. A key advantage is that it is **derivative-free**, only requiring evaluations of the functions $f$ and $h$. The algorithm proceeds as follows: 

1.  **Sigma Point Generation:** Generate $2n+1$ [sigma points](@entry_id:171701) $\mathcal{X}_{k-1|k-1}^{(i)}$ from the posterior distribution at the previous step, $\mathcal{N}(\hat{x}_{k-1|k-1}, P_{k-1|k-1})$.

2.  **Time Update (Prediction):**
    -   Propagate each sigma point through the [nonlinear dynamics](@entry_id:140844): $\mathcal{X}_{k|k-1}^{(i)} = f(\mathcal{X}_{k-1|k-1}^{(i)}, u_{k-1})$.
    -   Compute the predicted mean and covariance by recombining the propagated points:
        $$
        \hat{x}_{k|k-1} = \sum_{i=0}^{2n} W_m^{(i)} \mathcal{X}_{k|k-1}^{(i)}
        $$
        $$
        P_{k|k-1} = \sum_{i=0}^{2n} W_c^{(i)} (\mathcal{X}_{k|k-1}^{(i)} - \hat{x}_{k|k-1})(\mathcal{X}_{k|k-1}^{(i)} - \hat{x}_{k|k-1})^\top + Q
        $$

3.  **Measurement Update (Correction):**
    -   Propagate the *predicted* [sigma points](@entry_id:171701) $\mathcal{X}_{k|k-1}^{(i)}$ through the nonlinear measurement function: $\mathcal{Z}^{(i)} = h(\mathcal{X}_{k|k-1}^{(i)})$.
    -   Compute the predicted measurement mean, innovation covariance, and the crucial **state-measurement cross-covariance** $P_{xz}$:
        $$
        \hat{y}_{k|k-1} = \sum_{i=0}^{2n} W_m^{(i)} \mathcal{Z}^{(i)}
        $$
        $$
        S_k = \sum_{i=0}^{2n} W_c^{(i)} (\mathcal{Z}^{(i)} - \hat{y}_{k|k-1})(\mathcal{Z}^{(i)} - \hat{y}_{k|k-1})^\top + R
        $$
        $$
        P_{xz} = \sum_{i=0}^{2n} W_c^{(i)} (\mathcal{X}_{k|k-1}^{(i)} - \hat{x}_{k|k-1})(\mathcal{Z}^{(i)} - \hat{y}_{k|k-1})^\top
        $$
    -   Compute the Kalman gain and perform the final update:
        $$
        K_k = P_{xz} S_k^{-1}
        $$
        $$
        \hat{x}_{k|k} = \hat{x}_{k|k-1} + K_k (y_k - \hat{y}_{k|k-1})
        $$
        $$
        P_{k|k} = P_{k|k-1} - K_k S_k K_k^\top
        $$

#### EKF vs. UKF: A Practical Comparison

The choice between EKF and UKF depends on the specific problem. A primary advantage of the UKF is its derivative-free nature, making it easy to implement even for complex models where deriving Jacobians is difficult or error-prone. More fundamentally, the UKF often yields superior accuracy.

Consider a biomedical sensor with a saturating Michaelis-Menten characteristic, common in enzyme-based glucose monitors. The measurement function $h(x) = I_{\max}\frac{x}{K_M + x}$ is concave for positive glucose concentrations $x$. 

-   The **EKF**, by linearizing at the mean $\mu$, effectively ignores the curvature of the function. For a [concave function](@entry_id:144403), **Jensen's inequality** tells us that $\mathbb{E}[h(x)] \le h(\mathbb{E}[x])$. The EKF approximates the predicted mean as $h(\mu)$, which is an overestimate of the true mean. Furthermore, by ignoring higher-order terms, the EKF tends to underestimate the predicted variance.

-   The **UKF**, by contrast, propagates [sigma points](@entry_id:171701) that are spread out on both sides of the mean. When these points are passed through the true nonlinear function *before* being averaged, the filter captures the effect of the function's curvature. This results in a more accurate estimate of both the predicted mean and covariance, typically accurate to the second order of the Taylor expansion (whereas EKF is accurate only to the first).

The UKF's advantage is most pronounced when the state uncertainty (covariance $P$) is large or when the nonlinearity is strong (e.g., near the saturation point of the sensor). In these regimes, the linear approximation of the EKF breaks down, while the UKF's sampling approach remains robust.

### Optimal Smoothing: Refining Estimates with Future Data

Kalman filtering is a *causal* process; the estimate of the state at time $k$, $\hat{x}_{k|k}$, uses measurements only up to time $k$. In many biomedical applications, such as analyzing data from a clinical trial or a long-term monitoring session, the entire dataset is available for offline analysis. In this case, we can do better. **Optimal smoothing** refers to the process of computing state estimates using the full history of measurements, both past and future, $y_{1:N}$.

The **Rauch-Tung-Striebel (RTS) smoother** is a classic and efficient algorithm for [fixed-interval smoothing](@entry_id:201439). It provides the MMSE estimate $\hat{x}_{k|N} = \mathbb{E}[x_k | y_{1:N}]$ and its corresponding covariance $P_{k|N}$. The RTS smoother operates in two passes:

1.  A **[forward pass](@entry_id:193086)**, which is simply the standard Kalman filter (or EKF/UKF for [nonlinear systems](@entry_id:168347)) run from $k=1$ to $N$. This pass computes and stores all the filtered estimates $(\hat{x}_{k|k}, P_{k|k})$ and predicted estimates $(\hat{x}_{k+1|k}, P_{k+1|k})$.

2.  A **backward pass**, which starts from the final filtered estimate at time $N$ ($\hat{x}_{N|N}, P_{N|N}$) and moves backward to $k=0$. At each step, it refines the filtered estimate using information propagated back from the future.

The RTS [backward recursion](@entry_id:637281) is given by the following equations for $k = N-1, \dots, 0$: 
-   First, compute the **smoother gain** $C_k$, which relates the state at time $k$ to the state at time $k+1$:
    $$
    C_k = P_{k|k} F_k^\top P_{k+1|k}^{-1}
    $$
-   Then, update the state mean and covariance with the "smoothing innovation" $(\hat{x}_{k+1|N} - \hat{x}_{k+1|k})$, which is the difference between the smoothed and predicted estimates at the next time step:
    $$
    \hat{x}_{k|N} = \hat{x}_{k|k} + C_k (\hat{x}_{k+1|N} - \hat{x}_{k+1|k})
    $$
    $$
    P_{k|N} = P_{k|k} + C_k (P_{k+1|N} - P_{k+1|k}) C_k^\top
    $$
The resulting smoothed trajectory $\hat{x}_{0:N|N}$ is the most accurate possible estimate of the [state evolution](@entry_id:755365) given the model and the entire dataset. The smoothed covariance $P_{k|N}$ will be smaller than or equal to the filtered covariance $P_{k|k}$, reflecting the increased certainty gained from using future information. This makes smoothing an invaluable tool for retrospective analysis of physiological data.