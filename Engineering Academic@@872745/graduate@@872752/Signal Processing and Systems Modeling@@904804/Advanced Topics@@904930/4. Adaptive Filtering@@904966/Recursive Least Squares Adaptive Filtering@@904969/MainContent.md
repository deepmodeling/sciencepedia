## Introduction
Adaptive filtering is a cornerstone of modern signal processing and control systems, enabling algorithms to learn and track the dynamics of a system in real time. While simple algorithms like the Least Mean Squares (LMS) method are valued for their low computational cost, their slow convergence in many practical scenarios creates a demand for more powerful techniques. The Recursive Least Squares (RLS) algorithm emerges as a solution to this challenge, offering significantly faster convergence by leveraging a more sophisticated statistical foundation.

This article addresses the need for an efficient and rapidly converging online [parameter estimation](@entry_id:139349) method, moving beyond the computational burden of batch least squares processing. We will dissect the RLS algorithm, providing a deep understanding of its operation, performance, and practical application. Across three comprehensive chapters, you will gain a thorough mastery of this essential [adaptive filtering](@entry_id:185698) tool.

The journey begins in **Principles and Mechanisms**, where we derive the RLS algorithm from its deterministic roots in [weighted least squares](@entry_id:177517). We will explore its recursive structure, analyze its convergence properties and failure modes like covariance blow-up, and uncover its elegant connection to Bayesian estimation through the Kalman filter. Next, in **Applications and Interdisciplinary Connections**, we situate RLS in a broader context, examining its use in [system identification](@entry_id:201290), [adaptive control](@entry_id:262887), and signal processing, and comparing its performance trade-offs against other popular methods. Finally, **Hands-On Practices** will guide you through implementing the algorithm, from a single update step to building numerically robust square-root filters, cementing your theoretical knowledge with practical skill.

## Principles and Mechanisms

The Recursive Least Squares (RLS) algorithm represents a powerful and fundamental tool in [adaptive filtering](@entry_id:185698), providing a method for sequentially estimating the parameters of a linear model. Unlike stochastic gradient methods such as the Least Mean Squares (LMS) algorithm, RLS is rooted in deterministic optimization, specifically the method of least squares. This chapter elucidates the principles and mechanisms of the RLS algorithm, beginning with its foundation in [weighted least squares](@entry_id:177517), deriving its recursive structure, analyzing its convergence and tracking properties, and exploring its deep connection to Bayesian estimation via the Kalman filter. We will conclude with a discussion of critical practical challenges, including estimator bias and numerical stability.

### From Batch to Recursive Estimation: The Weighted Least Squares Foundation

The journey to understanding RLS begins with the classical batch [least squares problem](@entry_id:194621). Consider a linear model where a sequence of scalar outputs, $y_k$, is related to a sequence of $p$-dimensional regressor vectors, $x_k$, through an unknown, constant parameter vector $\theta^{\star} \in \mathbb{R}^p$. Over a block of $N$ observations, we can express this relationship in matrix form as $y = X\theta^{\star} + v$, where $y \in \mathbb{R}^N$ is the vector of outputs, $X \in \mathbb{R}^{N \times p}$ is the matrix whose rows are $x_k^\top$, and $v \in \mathbb{R}^N$ represents measurement noise or modeling errors.

The goal is to find an estimate, $\hat{\theta}$, that best fits the data. The **Weighted Least Squares (WLS)** criterion provides a flexible framework for this, minimizing a weighted [sum of squared residuals](@entry_id:174395):

$J(\theta) = \sum_{k=1}^{N} w_k (y_k - x_k^\top \theta)^2 = (y - X\theta)^\top W (y - X\theta)$

Here, $W = \mathrm{diag}(w_1, w_2, \dots, w_N)$ is a [diagonal matrix](@entry_id:637782) of positive weights. To find the minimizer, we set the gradient of the cost function with respect to $\theta$ to zero. The cost function is a [quadratic form](@entry_id:153497) in $\theta$:

$J(\theta) = y^\top W y - 2\theta^\top X^\top W y + \theta^\top (X^\top W X) \theta$

The gradient is $\nabla_{\theta} J(\theta) = -2X^\top W y + 2(X^\top W X)\theta$. Setting this to zero yields the celebrated **normal equations** for the [weighted least squares](@entry_id:177517) problem [@problem_id:2899730]:

$(X^\top W X) \hat{\theta}_{WLS} = X^\top W y$

Provided the matrix $X^\top W X$ is invertible, a unique solution exists.

In [adaptive filtering](@entry_id:185698), we are often interested in tracking systems whose parameters may change over time. This motivates giving more importance to recent data than to older data. A mathematically convenient and effective way to achieve this is through **exponential forgetting**. We define the weights to decay exponentially into the past from the current time $N$. Specifically, the weight for the data at time $k$ is set to $w_k = \lambda^{N-k}$, where $\lambda \in (0, 1]$ is the **[forgetting factor](@entry_id:175644)**.

With this choice, the batch WLS solution at time $N$ becomes [@problem_id:2899730]:

$\hat{\theta}_N = \left( \sum_{k=1}^{N} \lambda^{N-k} x_k x_k^\top \right)^{-1} \left( \sum_{k=1}^{N} \lambda^{N-k} y_k x_k \right)$

The [forgetting factor](@entry_id:175644) $\lambda$ governs the algorithm's memory and behavior.
- If $\lambda = 1$, all past data are weighted equally. This corresponds to the standard, unweighted [least squares problem](@entry_id:194621), which has an effectively infinite memory. It is suitable for identifying constant parameters in a stationary environment.
- If $0  \lambda  1$, the algorithm discounts older data. The influence of a data point decays exponentially as new data arrives, allowing the filter to track time-varying parameters. This introduces a fundamental trade-off: A smaller $\lambda$ (e.g., closer to 0) leads to a shorter memory, enabling faster tracking of system changes, but makes the estimate more sensitive to [measurement noise](@entry_id:275238), resulting in higher variance. Conversely, a larger $\lambda$ (closer to 1) provides a longer memory, averaging over more data to produce a smoother, lower-variance estimate, but at the cost of slower adaptation to changes [@problem_id:2899670].

A useful rule of thumb is that the **effective memory length** of the filter, or the number of samples it effectively "remembers," is approximately $N_{\text{eff}} \approx \frac{1}{1-\lambda}$. For instance, a [forgetting factor](@entry_id:175644) of $\lambda = 0.99$ corresponds to an effective memory of about 100 samples.

### The Recursive Least Squares (RLS) Algorithm

While the batch formula provides an optimal estimate at time $N$, recalculating the large matrix sums and inverting the resulting matrix at every new time step is computationally prohibitive. The genius of the RLS algorithm is that it provides a way to update the estimate $\hat{\theta}_{k-1}$ to $\hat{\theta}_k$ with a fixed computational cost, without re-processing all past data.

Let us define the **[information matrix](@entry_id:750640)** (or weighted [normal matrix](@entry_id:185943)) at time $k$ as $R_k$ and the corresponding [cross-correlation](@entry_id:143353) vector as $r_k$:

$R_k \triangleq \sum_{i=1}^{k} \lambda^{k-i} \phi_i \phi_i^\top$
$r_k \triangleq \sum_{i=1}^{k} \lambda^{k-i} \phi_i y_i$

(Here we adopt the notation $\phi_k$ for the regressor, common in [adaptive filtering](@entry_id:185698) literature). These quantities can be updated recursively:

$R_k = \lambda R_{k-1} + \phi_k \phi_k^\top$
$r_k = \lambda r_{k-1} + \phi_k y_k$

A "direct" recursive method could update $R_k$ and $r_k$ and then solve the [normal equations](@entry_id:142238) $R_k \hat{\theta}_k = r_k$ at each step. However, this requires a [matrix inversion](@entry_id:636005), an operation with [computational complexity](@entry_id:147058) of $\mathcal{O}(n^3)$, where $n$ is the dimension of $\theta$. This is computationally expensive and numerically problematic [@problem_id:2899718].

The standard RLS algorithm cleverly circumvents this repeated inversion by directly updating the inverse of the [information matrix](@entry_id:750640), $P_k \triangleq R_k^{-1}$, often called the **covariance matrix**. The update is derived by applying the **[matrix inversion](@entry_id:636005) lemma** (also known as the Woodbury identity) to the recursion for $R_k$. For the [rank-1 update](@entry_id:754058) $R_k = \lambda R_{k-1} + \phi_k \phi_k^\top$, we map $\boldsymbol{A} = \lambda R_{k-1}$, $\boldsymbol{U} = \phi_k$, $\boldsymbol{C} = 1$, and $\boldsymbol{V} = \phi_k^\top$ into the lemma [@problem_id:2899694]. This yields a direct recursive update for $P_k$:

$P_k = \frac{1}{\lambda} \left( P_{k-1} - \frac{P_{k-1} \phi_k \phi_k^\top P_{k-1}}{\lambda + \phi_k^\top P_{k-1} \phi_k} \right)$

This update, along with the update for the parameter estimate, forms the complete RLS algorithm. The standard steps are:
1.  Compute the **gain vector**: $K_k = \frac{P_{k-1} \phi_k}{\lambda + \phi_k^\top P_{k-1} \phi_k}$
2.  Compute the a priori error (**innovation**): $e_k = y_k - \phi_k^\top \hat{\theta}_{k-1}$
3.  Update the parameter estimate: $\hat{\theta}_k = \hat{\theta}_{k-1} + K_k e_k$
4.  Update the [inverse covariance matrix](@entry_id:138450): $P_k = \frac{1}{\lambda} (I - K_k \phi_k^\top) P_{k-1}$

This set of equations constitutes the RLS algorithm. The [computational complexity](@entry_id:147058) of each step is dominated by matrix-vector and matrix-matrix multiplications, resulting in a total complexity of $\mathcal{O}(n^2)$ per time step. This is a significant improvement over the $\mathcal{O}(n^3)$ direct inversion method and provides better numerical properties by avoiding the explicit formation and inversion of the potentially ill-conditioned [information matrix](@entry_id:750640) $R_k$ [@problem_id:2899718] [@problem_id:2899705].

### Convergence, Tracking, and Identifiability

The [existence and uniqueness](@entry_id:263101) of a least-squares estimate depend on the invertibility of the [information matrix](@entry_id:750640) $R_k$. In the batch case, this is equivalent to the matrix $X^\top W X$ being invertible, which holds if and only if the data matrix $X$ has full column rank. This means its columns must be [linearly independent](@entry_id:148207). If the columns are linearly dependent, different parameter vectors can produce the same output, and the parameters are not **identifiable** from the data [@problem_id:2899742].

In the recursive setting, especially with $\lambda  1$, the condition for convergence and good tracking is more stringent. It is not enough for the regressors to be [linearly independent](@entry_id:148207) over all time; they must be sufficiently rich in information within any finite time window. This property is known as **Persistent Excitation (PE)**. A regressor sequence $\{\phi_k\}$ is persistently exciting if the [information matrix](@entry_id:750640) formed over any sufficiently long window of time remains uniformly [positive definite](@entry_id:149459). This ensures that the algorithm continually receives new information in all directions of the [parameter space](@entry_id:178581), preventing the [information matrix](@entry_id:750640) $R_k$ from becoming singular. PE is the fundamental requirement for the convergence of RLS parameter estimates to their true values [@problem_id:2899742].

What happens if the PE condition is violated while using a [forgetting factor](@entry_id:175644) $\lambda  1$? This can lead to a catastrophic failure known as **covariance blow-up**. If the regressor $\phi_k$ is zero or very small for an extended period, the [information matrix](@entry_id:750640) recursion becomes $R_k \approx \lambda R_{k-1}$. Correspondingly, the inverse covariance [recursion](@entry_id:264696) becomes $P_k \approx \lambda^{-1} P_{k-1}$. Since $\lambda^{-1} > 1$, the matrix $P_k$ grows exponentially during this period of no excitation. When a small but non-zero regressor eventually appears, the gain vector $K_k$, which is proportional to $P_{k-1}$, will be enormous. This massive gain will cause the update term $K_k e_k$ to be dominated by the amplified [measurement noise](@entry_id:275238), effectively "kicking" the parameter estimate far away from its true value. This can lead to the divergence of the estimate, a phenomenon where the variance of the estimate grows without bound [@problem_id:2899724].

### A Bayesian Perspective: RLS as a Kalman Filter

The RLS algorithm, derived from a deterministic least-squares criterion, has a profound and elegant interpretation within the framework of Bayesian estimation. It can be shown that the RLS algorithm is mathematically equivalent to the **Kalman filter** for a specific [state-space model](@entry_id:273798).

To see this connection, let us consider the parameter vector $\theta_k$ as the "state" of a dynamic system we wish to estimate. We can model the system with the following [state-space equations](@entry_id:266994):

$\theta_k = \theta_{k-1} + w_{k-1} \quad \text{(State Equation)}$
$y_k = \phi_k^\top \theta_k + v_k \quad \text{(Measurement Equation)}$

The measurement equation is our standard linear regression model. The state equation models the [time evolution](@entry_id:153943) of the "true" parameters. A key insight is how to model the [process noise](@entry_id:270644) $w_{k-1}$ to reproduce the RLS algorithm. The equivalence holds if we assume the parameters follow a random walk, where the process noise $w_{k-1}$ is zero-mean Gaussian noise with a very specific, time-varying covariance matrix [@problem_id:2899731]:

$Q_{k-1} = \mathrm{Cov}(w_{k-1}) = \left(\frac{1}{\lambda} - 1\right) P_{k-1|k-1}$

Here, $P_{k-1|k-1}$ is the Kalman filter's posterior [error covariance](@entry_id:194780) of the state estimate at time $k-1$. This choice of $Q_{k-1}$ leads to a time-update step for the [error covariance](@entry_id:194780) $P_{k|k-1} = P_{k-1|k-1} + Q_{k-1} = \frac{1}{\lambda} P_{k-1|k-1}$. This mechanism, known as **[covariance inflation](@entry_id:635604)**, is precisely how the [forgetting factor](@entry_id:175644) operates in RLS.

Under this mapping, the RLS variables correspond directly to the Kalman filter variables:
- The RLS estimate $\hat{\theta}_k$ is the Kalman filter's posterior state estimate $\hat{\theta}_{k|k}$.
- The RLS matrix $P_k$ is precisely the posterior [mean-square [erro](@entry_id:194940)r covariance](@entry_id:194780) of the state estimate, $P_{k|k} = \mathbb{E}[(\theta_k - \hat{\theta}_{k|k})(\theta_k - \hat{\theta}_{k|k})^\top | y_{1:k}]$.
- The RLS gain vector $K_k$ is the Kalman gain.

This Bayesian interpretation is powerful. It reveals that the [forgetting factor](@entry_id:175644) is not merely an ad-hoc mechanism but is equivalent to assuming that the true parameters are not constant but are drifting randomly over time. The amount of drift we assume is proportional to our current uncertainty in the parameters. This allows the filter to downweigh old information and remain responsive to new data, providing a rigorous statistical justification for the algorithm's tracking capability [@problem_id:2899699] [@problem_id:2899731].

### Practical Considerations and Advanced Topics

While the RLS algorithm is powerful, its practical application requires careful consideration of potential pitfalls, including biased estimation and numerical instability.

#### Biased Estimation in Errors-in-Variables Models

A fundamental requirement for any least-squares estimator to be consistent (i.e., converge to the true parameters) is that the regressor vector must be uncorrelated with the true equation error. In many practical scenarios, this condition is violated. A classic example is the identification of an autoregressive (AR) model from noisy measurements, a so-called **[errors-in-variables](@entry_id:635892)** problem.

Suppose the true system is $y_k = -\sum a_i y_{k-i} + e_k$, but we can only observe $d_k = y_k + v_k$. If we form the regressor vector from past noisy measurements, $\phi_k = -[d_{k-1}, \dots, d_{k-p}]^\top$, a problem arises. The regressor $\phi_k$ contains past noise terms ($v_{k-1}, \dots, v_{k-p}$), and the equation error for the measured system also contains these same noise terms. This induces a correlation between the regressors and the error, violating the [orthogonality condition](@entry_id:168905). As a result, the standard RLS algorithm will converge to a biased estimate [@problem_id:2899692].

A solution to this problem is the **Instrumental Variable (IV)** method. The IV method replaces the regressor in the [normal equations](@entry_id:142238)' [orthogonality condition](@entry_id:168905) with an "instrumental" vector $z_k$ that satisfies two properties: (1) it is uncorrelated with the equation error, and (2) it is strongly correlated with the true regressor. This leads to the **Recursive Instrumental Variable (RIV)** algorithm, a modification of RLS that uses the instrument $z_k$ in the gain calculation to restore consistency and obtain unbiased estimates in the limit [@problem_id:2899692].

#### Numerical Stability and Square-Root Filtering

A second major practical issue is the numerical stability of the RLS covariance update. The standard update equation for $P_k$ involves a subtraction:

$P_k = \frac{1}{\lambda} \left( P_{k-1} - \text{a positive semidefinite matrix} \right)$

In finite-precision [floating-point arithmetic](@entry_id:146236), this subtraction can be numerically hazardous, a phenomenon known as **[catastrophic cancellation](@entry_id:137443)**. When the [information matrix](@entry_id:750640) $R_k$ is ill-conditioned (which happens with nearly collinear regressors), the matrices involved in the subtraction are nearly equal in a certain sense. Rounding errors can lead to a computed $P_k$ that is no longer symmetric or, worse, no longer positive definite, even though it must be so in exact arithmetic. A non-[positive definite](@entry_id:149459) $P_k$ can cause the entire algorithm to become unstable and diverge [@problem_id:2899705].

To overcome this numerical fragility, a class of algorithms known as **square-root filters** was developed. Instead of propagating the covariance matrix $P_k$ itself, these methods propagate a [matrix square root](@entry_id:158930) (e.g., the Cholesky factor). For example, a **square-root [information filter](@entry_id:750637) (SRIF)** propagates an [upper-triangular matrix](@entry_id:150931) $S_k^{1/2}$ such that the [information matrix](@entry_id:750640) is $R_k = (S_k^{1/2})^\top S_k^{1/2}$. The update is performed using numerically stable orthogonal transformations (like Givens rotations or Householder reflections), which do not involve subtractions. By always maintaining a valid Cholesky factor, the symmetry and [positive definiteness](@entry_id:178536) of the underlying [information matrix](@entry_id:750640) are preserved by construction, yielding a much more robust algorithm. These methods have a significantly better [numerical conditioning](@entry_id:136760), making them the preferred choice for high-precision or safety-critical applications [@problem_id:2899705].