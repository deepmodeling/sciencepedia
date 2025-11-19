## Introduction
For decades, the Kalman filter has been the gold standard for [state estimation](@entry_id:169668) in [linear dynamical systems](@entry_id:150282), offering an elegant and [optimal solution](@entry_id:171456) for tracking states amidst uncertainty. However, the vast majority of real-world systems—from a robot navigating a room to the complex interactions in an ecosystem—are inherently nonlinear. In these domains, the mathematical assumptions that guarantee the Kalman filter's optimality break down, creating a significant knowledge gap: how can we reliably estimate the state of a system when its dynamics defy simple linear descriptions?

This article addresses this fundamental challenge by exploring two of the most powerful and widely used extensions for [nonlinear state estimation](@entry_id:269877): the Extended Kalman Filter (EKF) and the Unscented Kalman Filter (UKF). By working through this material, you will gain a deep, practical understanding of how to move beyond [linear models](@entry_id:178302) and tackle the complexities of [nonlinear filtering](@entry_id:201008).

First, in **Principles and Mechanisms**, we will dissect the core theory, beginning with why nonlinearity breaks the elegant "Gaussian closure" of the standard Kalman filter. We will then detail the EKF's approach of approximation by linearization and its inherent pitfalls, before contrasting it with the UKF's sophisticated and derivative-free method of approximation by deterministic sampling.

Next, the chapter on **Applications and Interdisciplinary Connections** will demonstrate the remarkable versatility of these filters. We will journey from their classic uses in robotics and navigation to their roles in advanced algorithmic hybrids and their application in diverse scientific fields like ecology, [biophysics](@entry_id:154938), and chemistry, illustrating how these tools solve real-world problems.

Finally, you will have the opportunity to solidify your knowledge through a series of **Hands-On Practices**. These guided problems will challenge you to prove the properties of the Unscented Transform, discretize continuous-time models for [filter implementation](@entry_id:193316), and handle complex non-[additive noise](@entry_id:194447) models in code.

## Principles and Mechanisms

The previous chapter introduced the [state-space](@entry_id:177074) formulation and the celebrated Kalman filter, which provides the [optimal solution](@entry_id:171456) for [state estimation](@entry_id:169668) in [linear systems](@entry_id:147850) subject to Gaussian noise. Its optimality, however, is critically dependent on a powerful mathematical property: **Gaussian closure**. When a Gaussian random variable is subjected to a [linear transformation](@entry_id:143080), the result is another Gaussian. When two Gaussian probability densities are multiplied (as in the Bayesian update step), the result is proportional to another Gaussian density. Consequently, if the initial state and all noises are Gaussian, the [posterior distribution](@entry_id:145605) of the state remains perfectly Gaussian at every time step. A Gaussian distribution is fully characterized by its first two moments—its mean and covariance. The Kalman filter elegantly propagates these two moments, providing an exact, finite-dimensional, and recursive solution to an otherwise intractable problem.

This chapter delves into the more general and challenging domain of nonlinear systems. We will see that as soon as the system dynamics or the measurement model become nonlinear, the elegant simplicity of Gaussian closure is lost. The posterior distribution of the state will no longer remain Gaussian, and its mean and covariance are no longer [sufficient statistics](@entry_id:164717) to describe it. This necessitates a move from optimal filtering to approximate filtering. We will explore the principles and mechanisms of two of the most influential approximate nonlinear filters: the Extended Kalman Filter (EKF) and the Unscented Kalman Filter (UKF).

### The Breakdown of Gaussian Closure in Nonlinear Systems

Let us consider the general discrete-time nonlinear [state-space model](@entry_id:273798):
$$x_k = f(x_{k-1}, u_{k-1}) + w_{k-1}$$
$$y_k = h(x_k) + v_k$$
Here, $x_k$ is the state vector, $u_k$ is a known control input, and $y_k$ is the measurement. The functions $f(\cdot)$ and $h(\cdot)$ represent the nonlinear process and measurement models, respectively. The terms $w_{k-1}$ and $v_k$ are typically assumed to be zero-mean, white, mutually independent Gaussian noise processes with known covariances $Q$ and $R$.

The foundation of Bayesian filtering rests on a two-step recursive procedure involving prediction and update.

1.  **Prediction:** The predictive density $p(x_k | y_{1:k-1})$ is obtained by marginalizing the previous state's posterior $p(x_{k-1} | y_{1:k-1})$ through the process model:
    $$p(x_k | y_{1:k-1}) = \int p(x_k | x_{k-1}) \, p(x_{k-1} | y_{1:k-1}) \, dx_{k-1}$$

2.  **Update:** The new posterior density $p(x_k | y_{1:k})$ is computed by applying Bayes' rule to the predictive density using the new measurement $y_k$:
    $$p(x_k | y_{1:k}) \propto p(y_k | x_k) \, p(x_k | y_{1:k-1})$$

In the linear-Gaussian case, if $p(x_{k-1} | y_{1:k-1})$ is Gaussian, the prediction integral (a convolution of two Gaussians) yields a Gaussian $p(x_k | y_{1:k-1})$. The update step then multiplies this predictive Gaussian by the Gaussian likelihood $p(y_k | x_k)$, resulting in a new posterior $p(x_k | y_{1:k})$ that is also Gaussian. The cycle continues, and the distributions remain within the Gaussian family.

However, if either $f$ or $h$ is nonlinear, this [closure property](@entry_id:136899) is broken [@problem_id:2886785]. When a Gaussian distribution $p(x_{k-1} | y_{1:k-1})$ is propagated through the nonlinear function $f$, the resulting distribution of $f(x_{k-1})$ is generally non-Gaussian. Convolving this with the Gaussian [process noise](@entry_id:270644) $w_{k-1}$ does not, in general, recover a Gaussian shape. Similarly, even if the predictive density $p(x_k | y_{1:k-1})$ were somehow Gaussian, multiplying it by the likelihood $p(y_k | x_k)$, which is a function of $x_k$ through the nonlinear $h(x_k)$, will typically yield a non-Gaussian posterior.

Since the true posterior is no longer Gaussian, its mean and covariance are no longer a complete description of the state's uncertainty. The exact Bayesian recursion would require propagating an entire probability density function, which is computationally intractable in most cases. This is the fundamental challenge of [nonlinear filtering](@entry_id:201008).

To make the problem tractable, both the EKF and UKF adopt a **Gaussian moment-closure** approximation [@problem_id:2886814]. They operate under the simplifying assumption that the posterior distribution can be adequately approximated by a Gaussian at each time step. The core of the filter then becomes a mechanism for propagating the mean and covariance of this approximating Gaussian through the nonlinear system dynamics. The EKF and UKF differ profoundly in how they perform this propagation.

### The Extended Kalman Filter: Approximation by Linearization

The Extended Kalman Filter (EKF) is the most direct and historically significant extension of the standard Kalman filter to nonlinear systems. The core principle of the EKF is to confront nonlinearity by approximating it with linearity. At each time step, the EKF linearizes the nonlinear process and measurement models around the current best estimate of the state using a first-order Taylor [series expansion](@entry_id:142878). Once the system is locally approximated as a linear one, the standard Kalman filter equations can be applied to propagate the mean and covariance.

#### The EKF Algorithm

Let the posterior at time $k-1$ be approximated by a Gaussian distribution with mean $\hat{x}_{k-1}^{+}$ and covariance $P_{k-1}^{+}$. The EKF proceeds in two steps [@problem_id:2886807]:

**1. Prediction Step:**
The goal is to compute the predictive mean $\hat{x}_k^{-}$ and covariance $P_k^{-}$.
The state is predicted by propagating the previous [posterior mean](@entry_id:173826) through the true [nonlinear dynamics](@entry_id:140844) function:
$$\hat{x}_k^{-} = f(\hat{x}_{k-1}^{+}, u_{k-1})$$
The covariance is predicted by propagating the previous [posterior covariance](@entry_id:753630) through a linearized version of the dynamics. The function $f$ is linearized around $\hat{x}_{k-1}^{+}$:
$$f(x_{k-1}, u_{k-1}) \approx f(\hat{x}_{k-1}^{+}, u_{k-1}) + F_{k-1}(x_{k-1} - \hat{x}_{k-1}^{+})$$
where $F_{k-1}$ is the **Jacobian** of $f$ with respect to the state, evaluated at the previous [posterior mean](@entry_id:173826):
$$F_{k-1} = \left. \frac{\partial f}{\partial x} \right|_{x=\hat{x}_{k-1}^{+}, u=u_{k-1}}$$
The predicted covariance is then computed as in the linear Kalman filter, using this Jacobian as the [state transition matrix](@entry_id:267928):
$$P_k^{-} = F_{k-1} P_{k-1}^{+} F_{k-1}^{\top} + Q_{k-1}$$
where $Q_{k-1}$ is the [process noise covariance](@entry_id:186358).

**2. Update Step:**
The goal is to use the measurement $y_k$ to update the predictive estimates into the new [posterior mean](@entry_id:173826) $\hat{x}_k^{+}$ and covariance $P_k^{+}$.
First, the measurement model $h$ is linearized around the current predictive mean $\hat{x}_k^{-}$:
$$h(x_k) \approx h(\hat{x}_k^{-}) + H_k(x_k - \hat{x}_k^{-})$$
where $H_k$ is the Jacobian of $h$ with respect to the state, evaluated at the predictive mean:
$$H_k = \left. \frac{\partial h}{\partial x} \right|_{x=\hat{x}_k^{-}}$$
The subsequent update equations are identical in form to the linear Kalman filter:
-   **Innovation (Residual):** $\tilde{y}_k = y_k - h(\hat{x}_k^{-})$
-   **Innovation Covariance:** $S_k = H_k P_k^{-} H_k^{\top} + R_k$
-   **Kalman Gain:** $K_k = P_k^{-} H_k^{\top} S_k^{-1}$
-   **Posterior Mean Update:** $\hat{x}_k^{+} = \hat{x}_k^{-} + K_k \tilde{y}_k$
-   **Posterior Covariance Update:** $P_k^{+} = (I - K_k H_k) P_k^{-}$

An alternative, more numerically stable form for the covariance update, known as the **Joseph form**, is also commonly used:
$$P_k^{+} = (I - K_k H_k) P_k^{-} (I - K_k H_k)^{\top} + K_k R_k K_k^{\top}$$

#### Limitations and Pitfalls of Linearization

For the EKF to be applicable, the functions $f$ and $h$ must be continuously differentiable. Furthermore, the standard probabilistic assumptions must hold: the initial state and noise processes must be zero-mean, white, Gaussian, and mutually independent [@problem_id:2886825]. However, even when these conditions are met, the EKF's performance is fundamentally limited by the quality of its [linear approximation](@entry_id:146101).

**Linearization Error and Bias:** A careful analysis shows that the EKF's prediction of the mean is generally biased. For a generic nonlinear function $g(x)$, the true expected value is approximately $\mathbb{E}[g(x)] \approx g(\mu) + \frac{1}{2}g''(\mu)P$, where $x \sim \mathcal{N}(\mu, P)$. The EKF prediction is simply $g(\mu)$. This results in a bias of approximately $\frac{1}{2}g''(\mu)P$, which is first-order in the variance $P$ [@problem_id:2886769]. For highly [nonlinear systems](@entry_id:168347) or large state uncertainties (large $P$), this bias can become significant and degrade filter performance.

**Observability and Overconfidence:** Linearization can create a misleading picture of the system's [observability](@entry_id:152062). Consider a scalar system where a particle's position is static, $x_{k+1}=x_k$, and the measurement is its squared position, $y_k = x_k^2 + v_k$. The true system is globally unobservable, as a measurement $y_k$ cannot distinguish between a state $x$ and its negative $-x$. However, the EKF linearizes the measurement model $h(x)=x^2$ to get the Jacobian $H = 2x$. When evaluated at a prior mean estimate $\hat{x}_k^{-} = m \neq 0$, the Jacobian is non-zero, $H=2m$. This suggests the system is locally observable. The EKF, blind to the global ambiguity, may become overconfident in an estimate that has the wrong sign and diverge from the true state. This overconfidence manifests as an underestimation of the innovation variance. The true variance of the measurement involves [higher-order moments](@entry_id:266936) of the state distribution, which the EKF's linear model ignores [@problem_id:2886784].

**Breakdown in Highly Nonlinear Regions:** The validity of the first-order approximation is contingent on the state uncertainty being confined to a region where the function is "mostly linear." For functions with high curvature, this region can be very small. Consider a bearing-only sensor measuring the angle to a target, $h(x) = \operatorname{atan2}(x_2, x_1)$ [@problem_id:2886760]. The Jacobian of this function is $H(x) = \frac{1}{x_1^2+x_2^2} \begin{pmatrix} -x_2  x_1 \end{pmatrix}$. As the target approaches the origin ($x_1, x_2 \to 0$), the Jacobian's magnitude grows without bound, indicating a severe nonlinearity where the [linear approximation](@entry_id:146101) is poor. Furthermore, if the uncertainty in the target's position is large, particularly in the direction tangential to the sensor (a high "elongation ratio" of the uncertainty ellipse), the second-order terms in the Taylor expansion, which the EKF ignores, can become dominant. This can lead to a complete breakdown of the EKF's validity, where the calculated variance is a poor reflection of the true uncertainty [@problem_id:2886757].

### The Unscented Kalman Filter: Approximation by Deterministic Sampling

The Unscented Kalman Filter (UKF) offers a fundamentally different approach to the Gaussian moment-[closure problem](@entry_id:160656). Instead of approximating the nonlinear functions, the UKF provides a superior approximation of the probability distribution's propagation. The core mechanism is the **Unscented Transform (UT)**, a deterministic sampling technique that captures the mean and covariance of a random variable with a minimal set of carefully chosen sample points, called **[sigma points](@entry_id:171701)**.

#### The Unscented Transform (UT)

The principle of the UT is as follows: *It is easier to approximate a probability distribution than it is to approximate an arbitrary nonlinear function*.

For an $n$-dimensional Gaussian random variable $x \sim \mathcal{N}(\hat{x}, P)$, the scaled Unscented Transform generates a set of $2n+1$ [sigma points](@entry_id:171701) and corresponding weights. These points and weights are constructed to perfectly match the mean and covariance of the original Gaussian distribution [@problem_id:2886801].

1.  **Parameter and Sigma Point Selection:** The transform is parameterized by scaling parameters $\alpha$, $\beta$, and $\kappa$. These are combined into a composite parameter $\lambda = \alpha^2(n+\kappa)-n$. The [sigma points](@entry_id:171701) $\chi_i$ are then generated:
    $$\begin{align*}
    \chi_0 = \hat{x} \\
    \chi_i = \hat{x} + \left(\sqrt{(n+\lambda)P}\right)_i  \text{for } i=1,\dots,n \\
    \chi_{i+n} = \hat{x} - \left(\sqrt{(n+\lambda)P}\right)_{i-n}  \text{for } i=n+1,\dots,2n
    \end{align*}$$
    where $\left(\sqrt{(n+\lambda)P}\right)_i$ denotes the $i$-th column of the [matrix square root](@entry_id:158930) (e.g., from Cholesky factorization) of the scaled covariance matrix $(n+\lambda)P$.

2.  **Weight Selection:** Two sets of weights are defined, one for calculating the mean ($W_i^{(m)}$) and one for the covariance ($W_i^{(c)}$):
    $$\begin{align*}
    W_0^{(m)} = \frac{\lambda}{n+\lambda} \\
    W_0^{(c)} = \frac{\lambda}{n+\lambda} + (1-\alpha^2+\beta) \\
    W_i^{(m)} = W_i^{(c)} = \frac{1}{2(n+\lambda)}  \text{for } i=1,\dots,2n
    \end{align*}$$
    The parameter $\beta$ is often set to $2$ for Gaussian distributions, which is optimal in a certain sense.

3.  **Propagation and Recombination:** Each sigma point $\chi_i$ is propagated through the true nonlinear function $g(\cdot)$ to yield a set of transformed points $\mathcal{Y}_i = g(\chi_i)$. The mean and covariance of the transformed variable are then estimated as the weighted sample mean and covariance of these transformed points:
    $$\hat{y} \approx \sum_{i=0}^{2n} W_i^{(m)} \mathcal{Y}_i$$
    $$P_{yy} \approx \sum_{i=0}^{2n} W_i^{(c)} (\mathcal{Y}_i - \hat{y})(\mathcal{Y}_i - \hat{y})^\top$$

#### The UKF Algorithm

The UKF algorithm embeds the Unscented Transform into the Bayesian prediction-update cycle. Like the EKF, it assumes the posterior is Gaussian and requires the same probabilistic assumptions on the noise and initial state, but it does not require the system functions to be differentiable [@problem_id:2886825].

**1. Prediction Step:**
-   Generate [sigma points](@entry_id:171701) from the posterior distribution $\mathcal{N}(\hat{x}_{k-1}^{+}, P_{k-1}^{+})$.
-   Propagate each sigma point through the nonlinear process model: $\chi_{i,k|k-1} = f(\chi_{i,k-1}, u_{k-1})$.
-   Compute the predicted mean $\hat{x}_k^{-}$ by taking the weighted average of the propagated [sigma points](@entry_id:171701) using weights $W_i^{(m)}$.
-   Compute the predicted covariance $P_k^{-}$ by taking the weighted sample covariance of the propagated points using weights $W_i^{(c)}$, and add the [process noise covariance](@entry_id:186358): $P_k^{-} = \sum_i W_i^{(c)} (\chi_{i,k|k-1} - \hat{x}_k^{-})(\dots)^\top + Q_{k-1}$.

**2. Update Step:**
-   Propagate the predictive [sigma points](@entry_id:171701) $\chi_{i,k|k-1}$ through the nonlinear measurement model: $\mathcal{Y}_{i,k} = h(\chi_{i,k|k-1})$.
-   Compute the predicted measurement mean $\hat{y}_k$ as the weighted average of the transformed points $\mathcal{Y}_{i,k}$.
-   Compute the innovation covariance $S_k$ as the weighted sample covariance of $\mathcal{Y}_{i,k}$, and add the [measurement noise](@entry_id:275238) covariance $R_k$.
-   Compute the cross-covariance $P_{xy}$ between the state [sigma points](@entry_id:171701) and measurement [sigma points](@entry_id:171701).
-   The Kalman gain, [posterior mean](@entry_id:173826), and [posterior covariance](@entry_id:753630) are then calculated using formulas analogous to the linear case, but using these UT-approximated covariances:
    -   $K_k = P_{xy} S_k^{-1}$
    -   $\hat{x}_k^{+} = \hat{x}_k^{-} + K_k (y_k - \hat{y}_k)$
    -   $P_k^{+} = P_k^{-} - K_k S_k K_k^{\top}$

#### Advantages of the Unscented Approach

The UKF offers several significant advantages over the EKF, stemming directly from the power of the Unscented Transform.

**Higher-Order Accuracy:** The UT is constructed to match moments more accurately than a first-order linearization. For a Gaussian input, the UT-estimated mean and covariance are accurate to the second order in the Taylor [series expansion](@entry_id:142878). A more detailed analysis reveals that the bias in the UKF's predicted mean is of order $O(P^2)$, a significant improvement over the EKF's $O(P)$ bias [@problem_id:2886769]. For quadratic nonlinearities, such as the $h(x)=x^2$ example, the UT provides the exact mean and variance of the transformed distribution, yielding a bias of zero.

**Derivative-Free:** The UKF does not require the computation of Jacobians. This is a major practical advantage. It makes the UKF applicable to systems where the dynamics are non-differentiable or are available only as a "black-box" simulation. It also eliminates a common source of implementation errors associated with deriving and coding complex analytical Jacobians.

**Improved Robustness:** By capturing more of the true distribution's geometry, the UKF often demonstrates better robustness and accuracy, especially for highly [nonlinear systems](@entry_id:168347). In the unobservable $h(x)=x^2$ case, the UKF correctly computes the innovation variance, leading to a more appropriate (less aggressive) Kalman gain and avoiding the EKF's tendency for overconfidence and divergence [@problem_id:2886784]. In the bearing-only sensor example, the UKF naturally handles the angular nature of the problem. Propagated [sigma points](@entry_id:171701) can be averaged using circular statistics to correctly compute a mean angle, even when the uncertainty spans across the $\pm\pi$ boundary—a feat the EKF's local linear model cannot perform [@problem_id:2886760].

### Practical Considerations: Additive vs. Non-Additive Noise

A crucial distinction in implementing nonlinear filters is whether the noise enters the system in an **additive** or **non-additive** manner [@problem_id:2886782].

An **[additive noise](@entry_id:194447)** model takes the form:
$$x_{k+1} = f(x_k, u_k) + w_k$$
$$y_k = h(x_k) + v_k$$
Here, the noise is added *after* the state has passed through the nonlinearity. Because the noise is independent of the state, the covariance of the result is simply the sum of the covariances. This allows for a more efficient UKF implementation. Instead of augmenting the state with the noise variables, one can propagate the state-only [sigma points](@entry_id:171701) through the deterministic function (e.g., $f(x_k, u_k)$) and then simply add the noise covariance matrix ($Q_k$) to the resulting state covariance. This is mathematically equivalent to the more computationally expensive augmented approach and is the standard method for additive-noise UKFs.

A **non-[additive noise](@entry_id:194447)** model is more general:
$$x_{k+1} = f(x_k, u_k, w_k)$$
$$y_k = h(x_k, v_k)$$
In this case, the state and noise are coupled inside the nonlinearity. The principle of superposition fails. To correctly capture the statistics of the output, the filter must account for the joint distribution of the inputs.
-   For the EKF, this means computing Jacobians with respect to both the state and the noise variables.
-   For the UKF, this requires creating an **augmented [state vector](@entry_id:154607)** that concatenates the state and the noise, e.g., $x_a = [x^\top, w^\top]^\top$. The Unscented Transform is then applied to this larger vector. While this increases the number of [sigma points](@entry_id:171701) and thus the computational cost, it is the correct way to handle the nonlinear interactions between the state and the noise.

In summary, the choice between the EKF and UKF represents a trade-off. The EKF is computationally simpler and easier to understand as a direct extension of the Kalman filter. However, its reliance on linearization makes it prone to significant errors and instability in the face of strong nonlinearities. The UKF, while more complex to formulate, offers a derivative-free approach that provides superior accuracy and robustness by capturing higher-order moment information, making it the preferred choice for many challenging [nonlinear estimation](@entry_id:174320) problems.