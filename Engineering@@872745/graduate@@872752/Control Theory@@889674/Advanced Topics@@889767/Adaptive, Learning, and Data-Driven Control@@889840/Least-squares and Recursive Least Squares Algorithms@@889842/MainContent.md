## Introduction
The ability to construct mathematical models from observed data is a cornerstone of modern science and engineering, enabling prediction, analysis, and control of complex systems. Among the most fundamental and powerful tools for this task is the [principle of least squares](@entry_id:164326) (LS). While the classical batch formulation of least squares provides a powerful offline solution, many modern challenges—from adaptive flight control to real-time signal processing—demand estimators that can learn and adapt sequentially as new data arrives. This creates a knowledge gap between static modeling and the need for dynamic, online estimation.

This article bridges that gap by providing a thorough treatment of both batch Least-Squares and the more dynamic Recursive Least-Squares (RLS) algorithm. The following chapters will guide you through this powerful framework. The first chapter, **Principles and Mechanisms**, lays the groundwork by exploring the core mathematics of batch [least squares](@entry_id:154899), its statistical properties, and its practical challenges, leading to the derivation of the efficient RLS algorithm. Next, **Applications and Interdisciplinary Connections** demonstrates the versatility of these methods in fields like [adaptive control](@entry_id:262887) and materials science, while also addressing practical challenges such as noise, ill-conditioning, and the incorporation of prior knowledge. Finally, the **Hands-On Practices** section provides an opportunity to solidify your understanding through guided exercises in algorithm derivation and robust implementation.

## Principles and Mechanisms

This chapter delves into the fundamental principles of least-squares estimation, beginning with the classical batch formulation and its properties. We will explore the algebraic and geometric underpinnings of the solution, its statistical interpretation, and its performance characteristics. This foundation will illuminate the practical challenges of bias and numerical sensitivity, which in turn motivate the transition to the computationally efficient and adaptive Recursive Least-Squares (RLS) algorithm. We conclude by examining the mechanisms of RLS, including its ability to track [time-varying systems](@entry_id:175653) and the numerical considerations crucial for robust implementation.

### The Principle of Batch Least Squares

The method of least squares provides a standard approach for fitting a mathematical model to a set of observed data. In the context of system identification and control, we are often concerned with linear regression models.

#### The Linear Regression Problem and the Normal Equations

Consider a system whose output can be modeled as a linear combination of known variables. We collect $N$ data points, where for each observation $k \in \{1, \dots, N\}$, the output $y_k \in \mathbb{R}$ is related to a vector of known regressors $\phi_k \in \mathbb{R}^p$ by the model:

$y_k = \phi_k^{\top}\theta + v_k$

Here, $\theta \in \mathbb{R}^p$ is a vector of unknown parameters that we wish to estimate, and $v_k$ represents [unmodeled dynamics](@entry_id:264781), measurement noise, or other disturbances. We can write the entire set of $N$ observations in matrix form:

$y = \Phi \theta + v$

where $y = [y_1, \dots, y_N]^{\top}$ is the vector of outputs, $v = [v_1, \dots, v_N]^{\top}$ is the vector of disturbances, and $\Phi \in \mathbb{R}^{N \times p}$ is the data or regressor matrix, whose $k$-th row is $\phi_k^{\top}$.

The **[principle of least squares](@entry_id:164326)** posits that the best estimate of $\theta$, denoted $\hat{\theta}$, is the one that minimizes the sum of the squared differences between the observed outputs $y_k$ and the model's predicted outputs $\phi_k^{\top}\theta$. This [sum of squared residuals](@entry_id:174395) defines the least-squares cost function:

$J(\theta) = \sum_{k=1}^{N} (y_k - \phi_k^{\top}\theta)^2 = \|y - \Phi\theta\|_2^2$

To find the parameter vector $\hat{\theta}$ that minimizes this quadratic cost function, we can use calculus. The minimum must occur at a point where the gradient of $J(\theta)$ with respect to $\theta$ is the [zero vector](@entry_id:156189). Expanding the [cost function](@entry_id:138681), we have:

$J(\theta) = (y - \Phi\theta)^{\top}(y - \Phi\theta) = y^{\top}y - 2y^{\top}\Phi\theta + \theta^{\top}\Phi^{\top}\Phi\theta$

The gradient is:

$\nabla_{\theta} J(\theta) = -2\Phi^{\top}y + 2\Phi^{\top}\Phi\theta$

Setting the gradient to zero, $\nabla_{\theta} J(\hat{\theta}) = 0$, yields the celebrated **normal equations**:

$(\Phi^{\top}\Phi)\hat{\theta} = \Phi^{\top}y$

Any solution $\hat{\theta}$ to this system of linear equations is a least-squares estimate.

#### Identifiability and Uniqueness of the Solution

The [normal equations](@entry_id:142238) provide a potential solution, but a critical question remains: does a unique solution for $\hat{\theta}$ exist? The answer lies in the properties of the matrix $\Phi^{\top}\Phi$. This $p \times p$ matrix, often called the **[information matrix](@entry_id:750640)** or **Gram matrix**, encapsulates all the information the regressor data provides about the parameters. Let us denote it by $S_N = \Phi^{\top}\Phi = \sum_{k=1}^{N} \phi_k \phi_k^{\top}$.

The [normal equations](@entry_id:142238) form a linear system $S_N \hat{\theta} = \Phi^{\top}y$. From linear algebra, this system has a unique solution for any right-hand side if and only if the matrix $S_N$ is invertible, or nonsingular. A square matrix is nonsingular if and only if it has full rank, which for $S_N \in \mathbb{R}^{p \times p}$ means $\mathrm{rank}(S_N) = p$. Furthermore, since $S_N$ is symmetric and positive semidefinite (since $x^\top S_N x = x^\top \Phi^\top \Phi x = \|\Phi x\|_2^2 \ge 0$), this condition is equivalent to $S_N$ being **[positive definite](@entry_id:149459)**.

This mathematical condition has a deep connection to the concept of **[identifiability](@entry_id:194150)**. A parameter vector $\theta$ is said to be identifiable from the data if distinct parameter vectors lead to distinct noise-free model predictions. That is, for any two different parameter vectors $\theta_1 \neq \theta_2$, their corresponding noise-free output sequences must not be identical. In matrix form, this means $\Phi\theta_1 \neq \Phi\theta_2$. This is equivalent to requiring that the mapping from parameters to outputs, represented by the matrix $\Phi$, is injective. This, in turn, is true if and only if the [null space](@entry_id:151476) of $\Phi$ contains only the zero vector, $\mathrm{null}(\Phi)=\{0\}$, which means the columns of $\Phi$ are [linearly independent](@entry_id:148207).

The link to the [information matrix](@entry_id:750640) is direct: the [null space](@entry_id:151476) of $\Phi$ is identical to the [null space](@entry_id:151476) of $\Phi^{\top}\Phi = S_N$. Therefore, the parameter vector $\theta$ is identifiable if and only if $\mathrm{null}(S_N)=\{0\}$, which is equivalent to $\mathrm{rank}(S_N)=p$ [@problem_id:2718876]. If this condition holds, the regressors are said to be **persistently exciting**, as they contain enough "richness" to distinguish the effects of each parameter. Consequently, the [least-squares](@entry_id:173916) cost function $J(\theta)$ is strictly convex and possesses a unique minimizer given by:

$\hat{\theta} = (\Phi^{\top}\Phi)^{-1}\Phi^{\top}y$

Conversely, if $S_N$ is singular ($\mathrm{rank}(S_N)  p$), then its [null space](@entry_id:151476) is non-trivial. This implies there exists a nonzero vector $\Delta\theta$ such that $S_N \Delta\theta = 0$, and thus $\Phi\Delta\theta = 0$. In this case, for any parameter vector $\theta_1$, the distinct vector $\theta_2 = \theta_1 + \Delta\theta$ produces the exact same noise-free output, $\Phi\theta_1 = \Phi\theta_2$. The parameters are unidentifiable from the data, and the least-squares problem has infinitely many solutions [@problem_id:2718876] [@problem_id:2718860].

#### The Minimum-Norm Solution for Rank-Deficient Problems

When the regressor matrix $\Phi$ does not have full column rank, the [least-squares solution](@entry_id:152054) is not unique. The set of all solutions forms an affine subspace: if $\hat{\theta}_p$ is any [particular solution](@entry_id:149080), the complete [solution set](@entry_id:154326) is $\{\hat{\theta}_p + v \mid v \in \mathrm{null}(\Phi)\}$. In such scenarios, a common and sensible approach is to select the solution that has the smallest Euclidean norm. This is known as the **minimum-norm [least-squares solution](@entry_id:152054)**.

This unique [minimum-norm solution](@entry_id:751996) can be found by considering the [orthogonal decomposition](@entry_id:148020) of the parameter space $\mathbb{R}^p$ into the row space of $\Phi$, $\mathcal{R}(\Phi^\top)$, and its [orthogonal complement](@entry_id:151540), the [null space](@entry_id:151476) of $\Phi$, $\mathcal{N}(\Phi)$. Any [least-squares solution](@entry_id:152054) $\hat{\theta}$ can be uniquely written as $\hat{\theta} = \hat{\theta}_R + \hat{\theta}_N$, where $\hat{\theta}_R \in \mathcal{R}(\Phi^\top)$ and $\hat{\theta}_N \in \mathcal{N}(\Phi)$. By the Pythagorean theorem, its squared norm is $\|\hat{\theta}\|_2^2 = \|\hat{\theta}_R\|_2^2 + \|\hat{\theta}_N\|_2^2$. To minimize the norm, we must choose the solution for which the component in the null space is zero. Thus, the unique [minimum-norm solution](@entry_id:751996) is the one that lies entirely in the row space of $\Phi$.

This special solution is given by the action of the **Moore-Penrose [pseudoinverse](@entry_id:140762)** of $\Phi$, denoted $\Phi^+$, on the output vector $y$:

$\hat{\theta}_{\mathrm{min-norm}} = \Phi^{+}y$

The pseudoinverse $\Phi^+$ provides the unique solution to the normal equations that also has the minimum norm. For instance, consider the [underdetermined system](@entry_id:148553) with $\Phi = \begin{pmatrix} 1  0  1 \\ 0  1  0 \end{pmatrix}$ and $y = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$. The normal equations $x_1+x_3=1$ and $x_2=2$ admit an infinite family of solutions parameterized by $\alpha$: $x(\alpha) = [1-\alpha, 2, \alpha]^\top$. Minimizing the squared norm $\|x(\alpha)\|_2^2 = (1-\alpha)^2 + 2^2 + \alpha^2$ yields $\alpha = 1/2$. The unique [minimum-norm solution](@entry_id:751996) is therefore $x^\star = [1/2, 2, 1/2]^\top$ [@problem_id:2718860].

### Properties and Interpretations of the Least-Squares Estimator

Beyond its algebraic definition, the least-squares estimator possesses rich geometric and statistical interpretations that are crucial for its application and analysis.

#### Geometric Interpretation: Orthogonal Projection

The [least-squares solution](@entry_id:152054) has an elegant geometric interpretation. The vector of predicted outputs, $\hat{y} = \Phi\hat{\theta}$, represents a vector in the **[column space](@entry_id:150809)** of $\Phi$, denoted $\mathrm{col}(\Phi)$, which is the subspace of $\mathbb{R}^N$ spanned by the columns of $\Phi$. The [least-squares problem](@entry_id:164198) is equivalent to finding the vector $\hat{y}$ in this subspace that is closest to the observed data vector $y$. Geometrically, this closest point is the **orthogonal projection** of $y$ onto $\mathrm{col}(\Phi)$.

The [normal equations](@entry_id:142238) $(\Phi^{\top}\Phi)\hat{\theta} = \Phi^{\top}y$ can be rewritten as $\Phi^{\top}(y - \Phi\hat{\theta}) = 0$. This states that the residual vector, $e = y - \hat{y}$, is orthogonal to every column of $\Phi$, and therefore orthogonal to the entire column space $\mathrm{col}(\Phi)$.

This projection can be represented by an **[orthogonal projection](@entry_id:144168) matrix**, $P_\Phi = \Phi(\Phi^{\top}\Phi)^{-1}\Phi^{\top}$. The predicted output is $\hat{y} = P_\Phi y$, and the residual is $e = (I - P_\Phi)y = M_\Phi y$, where $M_\Phi = I - P_\Phi$ is the projector onto the space orthogonal to $\mathrm{col}(\Phi)$.

This geometric view is powerful for analyzing model structure. For example, to test whether a set of new regressors, $X_2$, provides additional explanatory power beyond an existing set, $X_1$, we can compare the reduction in the [residual sum of squares](@entry_id:637159) (RSS). The RSS for a model with regressors $X$ is $\|M_X y\|_2^2$. The incremental reduction in RSS from adding $X_2$ to a model with $X_1$ is $\Delta = \|M_{X_1} y\|_2^2 - \|M_{[X_1, X_2]} y\|_2^2 = y^\top(P_{[X_1, X_2]} - P_{X_1})y$. This reduction is precisely the squared norm of the projection of $y$ onto the part of $\mathrm{col}(X_2)$ that is orthogonal to $\mathrm{col}(X_1)$. Under standard statistical assumptions, a normalized version of $\Delta$ can be used to construct an F-test to determine if the contribution of $X_2$ is statistically significant [@problem_id:2718795].

#### Statistical Interpretation: The Maximum Likelihood Connection

The [principle of least squares](@entry_id:164326) is often motivated by its computational and geometric simplicity, without any probabilistic assumptions. However, it gains profound statistical justification under a specific noise model. If we assume that the disturbance terms $v_k$ are independent and identically distributed (i.i.d.) random variables from a zero-mean Gaussian distribution with variance $\sigma^2$, i.e., $v \sim \mathcal{N}(0, \sigma^2 I)$, then the vector of measurements $y$ follows the distribution $y \sim \mathcal{N}(\Phi\theta, \sigma^2 I)$.

The **Maximum Likelihood Estimator (MLE)** is the parameter value that maximizes the probability (or likelihood) of observing the given data $y$. The [log-likelihood function](@entry_id:168593) for this model is:

$\ln L(\theta, \sigma^2 | y) = -\frac{N}{2} \ln(2\pi\sigma^2) - \frac{1}{2\sigma^2} \|y - \Phi\theta\|_2^2$

To find the MLE for $\theta$, we must maximize this expression. Maximizing the [log-likelihood](@entry_id:273783) with respect to $\theta$ is equivalent to minimizing the term $\|y - \Phi\theta\|_2^2$. This is precisely the [least-squares](@entry_id:173916) cost function. Therefore, under the assumption of i.i.d. Gaussian noise, **the least-squares estimator is identical to the maximum likelihood estimator** [@problem_id:2718817]. This equivalence holds whether the noise variance $\sigma^2$ is known or not, and it provides a strong statistical rationale for using least squares.

It is important to note that this equivalence breaks down if the noise is not i.i.d. Gaussian. For instance, if the noise is still Gaussian but correlated, $v \sim \mathcal{N}(0, R)$ with $R \neq \sigma^2 I$, the MLE corresponds to the Generalized Least Squares (GLS) estimator. If the noise is non-Gaussian (e.g., Laplace distributed), the MLE will be different from the LS estimator (e.g., the [least absolute deviations](@entry_id:175855) estimator) [@problem_id:2718817].

#### Asymptotic Properties and Performance

In many control applications, data arrives sequentially, and we are interested in the behavior of the estimator as the number of data points $N$ becomes large. Under certain stationarity and [ergodicity](@entry_id:146461) assumptions on the regressor and noise processes, we can characterize the **asymptotic properties** of the LS estimator.

A key condition for the estimator to converge to the true parameter value $\theta_\star$ (i.e., for the estimator to be **consistent**) is that the regressor sequence must be **persistently exciting**. This is a dynamic version of the full-rank condition on $\Phi$. It requires the regressor covariance matrix, $R_\varphi = \mathbb{E}[\phi_k \phi_k^\top]$, to be positive definite.

Under these conditions, we can use the Law of Large Numbers and the Central Limit Theorem to analyze the estimation error $\tilde{\theta}_N = \hat{\theta}_N - \theta_\star$. It can be shown that the scaled error $\sqrt{N}\tilde{\theta}_N$ converges in distribution to a zero-mean Gaussian random vector. The covariance of this [limiting distribution](@entry_id:174797), which characterizes the uncertainty of the estimate for large $N$, is given by:

$\lim_{N\to\infty} N \cdot \mathrm{Cov}(\hat{\theta}_N) = \sigma_w^2 R_\varphi^{-1}$

where $\sigma_w^2$ is the variance of the noise process [@problem_id:2718804]. This fundamental result reveals that the [asymptotic variance](@entry_id:269933) of the estimator is directly proportional to the noise power $\sigma_w^2$ and inversely proportional to the regressor covariance matrix $R_\varphi$. A "stronger" or more exciting input signal leads to a larger $R_\varphi$ and thus a smaller [estimation error](@entry_id:263890) variance.

#### Practical Challenges: Bias and Sensitivity

While powerful, the LS estimator is not without its pitfalls. Two critical practical issues are estimator bias and numerical sensitivity.

##### Bias in Errors-in-Variables Models

A fundamental requirement for the LS estimator to be consistent is that the regressors must be uncorrelated with the noise term. In many [system identification](@entry_id:201290) problems, this assumption is violated. A canonical example is the identification of an [autoregressive model](@entry_id:270481) with exogenous input (ARX) from noisy output measurements. Consider the true system $y_t = a_0 y_{t-1} + b_0 u_{t-1} + w_t$, where the measured output is $y_t^m = y_t + v_t$. If we naively formulate an LS problem using the measured regressor $\phi_t = [y_{t-1}^m, u_{t-1}]^\top$, the regressor component $y_{t-1}^m$ contains the noise term $v_{t-1}$. The corresponding "equation error" in the regression model also contains $v_{t-1}$, creating a correlation between the regressor and the error. This situation is known as an **[errors-in-variables](@entry_id:635892)** problem.

This correlation violates the conditions for consistency, and the ordinary least-squares estimator will converge to a biased value, even with infinite data. The asymptotic bias for the parameter $a_0$ can be explicitly derived and is a function of the true parameter, the noise variances, and the input variance. For instance, in a simple ARX(1,1) model, the asymptotic estimate for the autoregressive parameter is always smaller in magnitude than the true value, a phenomenon known as [attenuation bias](@entry_id:746571) [@problem_id:2718808]. This highlights the need for more sophisticated methods, like Instrumental Variable (IV) estimation, when regressors are correlated with noise.

##### Numerical Sensitivity and Ill-Conditioning

The quality of the LS solution is also highly dependent on the numerical properties of the data matrix $\Phi$. The [estimation error](@entry_id:263890) $\hat{\theta} - \theta^\star$ is given by $\Phi^+ e$, where $e$ is the disturbance vector. Using the Singular Value Decomposition (SVD) of $\Phi = U\Sigma V^\top$, we can see that the error is amplified by the inverse of the singular values $\sigma_i$. A small [singular value](@entry_id:171660) $\sigma_i$ means that noise components in the data aligned with the corresponding left [singular vector](@entry_id:180970) $u_i$ are greatly magnified in the parameter error along the direction of the right [singular vector](@entry_id:180970) $v_i$ [@problem_id:28664].

This sensitivity can be quantified by the **condition number** of $\Phi$, defined as $\kappa(\Phi) = \sigma_{\max}/\sigma_{\min}$. A large condition number indicates that the problem is **ill-conditioned**, meaning small perturbations in the data can lead to large changes in the solution. The relative error in the parameter estimate can be bounded as follows:

$\frac{\|\hat{\theta} - \theta^{\star}\|_2}{\|\theta^{\star}\|_2} \le \kappa(\Phi) \frac{\|e\|_2}{\|\Phi \theta^{\star}\|_2}$

This inequality shows that the relative parameter error is bounded by the product of the condition number and the noise-to-signal ratio. For an [ill-conditioned matrix](@entry_id:147408), even a small amount of noise can lead to a very large [relative error](@entry_id:147538) in the estimated parameters. For example, if a data matrix has a condition number of 200 and the noise norm is a fraction of the signal norm, the [relative error](@entry_id:147538) bound on the parameters can still be significant [@problem_id:2718864].

### The Recursive Least-Squares (RLS) Algorithm

The batch [least-squares method](@entry_id:149056) requires all data to be available at once and involves computations whose complexity grows with the size of the dataset. In online applications such as [adaptive control](@entry_id:262887), data arrives sequentially, and a new estimate is desired at each time step.

#### Motivation: The Cost of Batch Recomputation

If we were to recompute the batch LS solution from scratch every time a new sample $(\phi_k, y_k)$ arrives, the computational burden would be prohibitive. At step $k$, we would form the data matrix $\Phi_k \in \mathbb{R}^{k \times p}$ and solve the normal equations. Forming the [information matrix](@entry_id:750640) $\Phi_k^\top\Phi_k$ costs $O(k p^2)$ operations, and solving the resulting $p \times p$ system costs $O(p^3)$ operations. The memory required to store the entire data history is $O(kp)$. As $k$ grows, these costs become unsustainable for real-time applications [@problem_id:2718833]. This motivates the need for a [recursive algorithm](@entry_id:633952) that can update the estimate efficiently.

#### Derivation and Mechanics of RLS

The **Recursive Least-Squares (RLS)** algorithm provides an efficient method for updating the LS estimate without re-processing all past data. The core idea is to find a recursion for the estimate $\hat{\theta}_k$ based on the previous estimate $\hat{\theta}_{k-1}$ and the new data pair $(\phi_k, y_k)$. This is achieved by applying the [matrix inversion](@entry_id:636005) lemma (specifically, the Sherman-Morrison formula) to the update of the [information matrix](@entry_id:750640) $S_k = S_{k-1} + \phi_k \phi_k^\top$.

Let $P_k = S_k^{-1} = (\sum_{i=1}^k \phi_i \phi_i^\top)^{-1}$ be the inverse of the [information matrix](@entry_id:750640), often called the **covariance matrix**. The RLS algorithm consists of the following steps at each time instant $k$:

1.  Compute the **gain vector**: $K_k = \frac{P_{k-1}\phi_k}{1 + \phi_k^\top P_{k-1} \phi_k}$
2.  Compute the **[prediction error](@entry_id:753692)**: $e_k = y_k - \phi_k^\top \hat{\theta}_{k-1}$
3.  Update the **parameter estimate**: $\hat{\theta}_k = \hat{\theta}_{k-1} + K_k e_k$
4.  Update the **covariance matrix**: $P_k = (I - K_k \phi_k^\top)P_{k-1}$

This elegant algorithm has a fixed [computational complexity](@entry_id:147058) of $O(p^2)$ per time step, dominated by the matrix-vector and [outer product](@entry_id:201262) operations. It also requires a fixed memory of $O(p^2)$ to store the $P$ matrix. This makes RLS vastly more efficient than batch recomputation for online estimation [@problem_id:2718833].

#### Tracking Time-Varying Parameters: The Forgetting Factor

The standard RLS algorithm gives equal weight to all past data. This is appropriate for estimating a constant parameter vector but is unsuitable if the system parameters are expected to change over time. To enable the estimator to track such variations, we must discount older data. This is accomplished by introducing an exponentially weighted [cost function](@entry_id:138681):

$J_k(\theta) = \sum_{i=1}^{k} \lambda^{k-i} (y_i - \phi_i^{\top}\theta)^2$

The **[forgetting factor](@entry_id:175644)**, $\lambda \in (0, 1]$, determines the rate at which past information is down-weighted. A value of $\lambda=1$ corresponds to the standard, equally weighted case. A value of $\lambda  1$ gives more weight to recent data, allowing the estimator to adapt to changes.

This modification leads to a simple change in the RLS recursions. The [information matrix](@entry_id:750640) update becomes $R_k = \lambda R_{k-1} + \phi_k \phi_k^\top$, and the covariance matrix update in the final RLS algorithm becomes:

$P_k = \frac{1}{\lambda}(I - K_k \phi_k^\top)P_{k-1}$

The choice of $\lambda$ represents a fundamental trade-off. A value close to 1 provides good [noise immunity](@entry_id:262876) but slow adaptation to parameter changes. A smaller value of $\lambda$ provides faster tracking but makes the estimate more sensitive to noise. The effective memory of the algorithm can be quantified by an **effective window length**, defined as the size of a [rectangular window](@entry_id:262826) with the same total weight as the infinite exponential window. This length is given by $N_{\mathrm{eff}} = \sum_{j=0}^{\infty} \lambda^j = \frac{1}{1-\lambda}$ [@problem_id:2718840]. For example, a [forgetting factor](@entry_id:175644) of $\lambda=0.99$ corresponds to an effective memory of 100 samples.

#### Numerical Stability of RLS Implementations

While algorithmically elegant, the conventional "covariance form" of RLS presented above is known to be numerically fragile in [finite-precision arithmetic](@entry_id:637673). After many iterations, rounding errors can accumulate, causing the computed covariance matrix $P_k$ to lose its essential properties of symmetry and [positive definiteness](@entry_id:178536).

The primary source of this instability is the subtraction in the covariance update step, $P_k = (I - K_k\phi_k^\top)P_{k-1}$. When the incoming data is not very informative, the gain $K_k$ is small, and this step becomes a subtraction of two nearly equal matrices. This can lead to **catastrophic cancellation**, where the result is dominated by rounding errors, potentially introducing asymmetry or even small negative eigenvalues into the computed $P_k$. A non-[positive definite](@entry_id:149459) covariance matrix can cause the estimator gains to grow uncontrollably, destabilizing the entire estimation loop [@problem_id:2718866].

To overcome this numerical weakness, more robust formulations have been developed:

*   **Joseph-Form RLS**: This formulation rewrites the covariance update as a sum of symmetric positive semidefinite terms, such as $P_k = (I - K_k\phi_k^\top) P_{k-1} (I - K_k\phi_k^\top)^\top + K_k R_v K_k^\top$ (where $R_v$ is related to noise covariance). By avoiding the critical subtraction, this form is inherently more stable against round-off errors, though it comes at a higher computational cost [@problem_id:2718866].

*   **Square-Root RLS (SR-RLS)**: A more effective and widely used approach is to propagate a square root of the covariance matrix, such as its Cholesky factor $S_k$ where $P_k = S_k S_k^\top$. The updates are performed directly on $S_k$ using numerically stable orthogonal transformations (e.g., Givens rotations or Householder reflectors). Since the updated covariance, if recomputed, is always of the form $S_k S_k^\top$, symmetry and [positive definiteness](@entry_id:178536) are guaranteed by construction. Furthermore, these algorithms effectively work with quantities whose condition numbers are the square root of the condition number of $P_k$, leading to significantly improved numerical behavior [@problem_id:2718866]. For applications requiring high reliability and long run-times, square-root implementations are strongly preferred.