## Introduction
Maximum Likelihood Estimation (MLE) stands as a cornerstone of modern [statistical inference](@entry_id:172747), offering a powerful and principled framework for estimating unknown parameters from data. In fields ranging from engineering to finance and across the natural sciences, researchers and practitioners constantly face the [inverse problem](@entry_id:634767): given a set of noisy observations, how can we infer the parameters of the underlying model that generated them? MLE addresses this challenge by reframing it as a question of probability, seeking the parameter values that make the observed data most likely. This approach provides not only a point estimate but also a comprehensive toolkit for quantifying uncertainty, testing hypotheses, and connecting with other estimation paradigms like Bayesian inference.

This article provides a graduate-level exploration of the theory and application of Maximum Likelihood Estimation. We begin in **Principles and Mechanisms** by dissecting the core concepts, from the definition of the [likelihood function](@entry_id:141927) to its optimization using numerical methods. This chapter also delves into the critical topic of [uncertainty quantification](@entry_id:138597) through the Fisher Information Matrix and establishes the deep connection between MLE and the familiar [method of least squares](@entry_id:137100). Following this theoretical foundation, **Applications and Interdisciplinary Connections** demonstrates the remarkable versatility of MLE through a survey of its use in solving real-world problems. We will see how it is applied to dynamical systems, [state-space models](@entry_id:137993), and complex observation scenarios across various scientific disciplines. Finally, **Hands-On Practices** presents a set of challenging problems designed to solidify your understanding and bridge the gap between theory and practical implementation in data assimilation and [inverse problems](@entry_id:143129).

## Principles and Mechanisms

The principle of Maximum Likelihood Estimation (MLE) provides a versatile and powerful framework for [parameter estimation](@entry_id:139349) in inverse problems. It recasts the task of finding unknown parameters as a question of probability: which set of parameters makes the observed data most likely? This chapter elucidates the core principles of MLE, the mechanisms for computing estimates and quantifying their uncertainty, and its deep connections to other estimation paradigms common in data assimilation.

### The Principle of Maximum Likelihood

The foundation of MLE is the **likelihood function**, denoted $L(\theta; y)$. It is numerically equivalent to the probability density function (or probability [mass function](@entry_id:158970)) of the observed data $y$, but it is interpreted as a function of the unknown parameter vector $\theta$. The **principle of maximum likelihood** posits that the most plausible value for $\theta$ is the one that maximizes this function. The resulting estimate, $\hat{\theta}_{\text{MLE}}$, is called the maximum likelihood estimate:

$$
\hat{\theta}_{\text{MLE}} = \underset{\theta}{\arg\max} \, L(\theta; y)
$$

In practice, it is almost always more convenient to work with the natural logarithm of the likelihood, known as the **[log-likelihood function](@entry_id:168593)**, $\ell(\theta; y) = \ln L(\theta; y)$. Since the logarithm is a monotonically increasing function, maximizing $\ell(\theta; y)$ is equivalent to maximizing $L(\theta; y)$. This transformation is advantageous as it converts products of probabilities (arising from independent observations) into sums, which are analytically and numerically easier to handle. The estimation problem then becomes:

$$
\hat{\theta}_{\text{MLE}} = \underset{\theta}{\arg\max} \, \ell(\theta; y)
$$

Equivalently, one can minimize the **[negative log-likelihood](@entry_id:637801)**, $J(\theta) = -\ell(\theta; y)$. This formulation is common in inverse problems and data assimilation, as it frames estimation as a minimization problem, analogous to minimizing a cost or [misfit function](@entry_id:752010).

#### Likelihood for Gaussian Noise Models

A prevalent assumption in inverse problems is that observational errors are additive, zero-mean, and follow a Gaussian distribution. Consider a general forward model $\mathcal{G}(\theta)$ that maps parameters $\theta \in \mathbb{R}^p$ to observations in $\mathbb{R}^m$. The data model is $y = \mathcal{G}(\theta) + \varepsilon$, where the noise $\varepsilon$ is drawn from a [multivariate normal distribution](@entry_id:267217), $\varepsilon \sim \mathcal{N}(0, \Sigma)$. Here, $\Sigma \in \mathbb{R}^{m \times m}$ is the [symmetric positive-definite](@entry_id:145886) covariance matrix of the noise.

The [likelihood function](@entry_id:141927) is the probability density of $y$ given $\theta$, which is $y \mid \theta \sim \mathcal{N}(\mathcal{G}(\theta), \Sigma)$. The PDF is:
$$
L(\theta; y) = \frac{1}{(2\pi)^{m/2} \det(\Sigma)^{1/2}} \exp\left(-\frac{1}{2} (y - \mathcal{G}(\theta))^\top \Sigma^{-1} (y - \mathcal{G}(\theta))\right)
$$
The corresponding log-likelihood is:
$$
\ell(\theta; y) = -\frac{m}{2}\ln(2\pi) - \frac{1}{2}\ln\det(\Sigma) - \frac{1}{2} (y - \mathcal{G}(\theta))^\top \Sigma^{-1} (y - \mathcal{G}(\theta))
$$
Minimizing the [negative log-likelihood](@entry_id:637801), and dropping the constant term $-\frac{m}{2}\ln(2\pi)$, is equivalent to minimizing the [objective function](@entry_id:267263):
$$
J(\theta) = \frac{1}{2} \ln\det(\Sigma) + \frac{1}{2} (y - \mathcal{G}(\theta))^\top \Sigma^{-1} (y - \mathcal{G}(\theta))
$$
This objective function is central to many [data assimilation methods](@entry_id:748186). The second term, involving the squared Mahalanobis distance between the data $y$ and the model prediction $\mathcal{G}(\theta)$, is a **[data misfit](@entry_id:748209)** or **weighted [least-squares](@entry_id:173916)** term. The first term, $\frac{1}{2}\ln\det(\Sigma)$, captures the volume of the noise distribution.

Two important cases arise :

1.  **Constant Covariance:** If the noise covariance $\Sigma$ is known and does not depend on the parameter $\theta$, the $\ln\det(\Sigma)$ term is a constant and can also be dropped. The MLE problem simplifies to a weighted least-squares problem:
    $$
    \hat{\theta}_{\text{MLE}} = \underset{\theta}{\arg\min} \, \frac{1}{2} (y - \mathcal{G}(\theta))^\top \Sigma^{-1} (y - \mathcal{G}(\theta))
    $$
    If the noise is also assumed to be uncorrelated and homoscedastic, i.e., $\Sigma = \sigma^2 I$, the problem reduces to standard [nonlinear least squares](@entry_id:178660).

2.  **Parameter-Dependent Covariance:** In more complex scenarios, the noise characteristics may depend on the state itself, so $\Sigma = \Sigma(\theta)$. In this case, the $\ln\det(\Sigma(\theta))$ term cannot be ignored, as it varies with $\theta$. Neglecting this term would lead to a generalized least-squares problem, but not the true MLE. It acts as a penalty term that discourages solutions where the model-predicted noise variance is unjustifiably large. If the variance, say $\Sigma(\theta) = \sigma^2 I_m$, is itself an unknown parameter to be estimated, MLE provides a principled way to find it. For a fixed $\theta$, the MLE of the variance $\sigma^2$ is the mean squared residual :
    $$
    \hat{\sigma}^2 = \frac{1}{m} \|y - \mathcal{G}(\theta)\|_2^2
    $$

#### Likelihood for Non-Gaussian Models: The Poisson Case

The MLE framework is not limited to Gaussian noise. Consider an application like [photon-limited imaging](@entry_id:753414), where observations are photon counts. Such data are often modeled by a **Poisson distribution**. Let $y_1, \dots, y_m$ be independent counts, where each $y_i \sim \mathrm{Poisson}(\lambda_i)$. The parameter of interest, $\theta$, is linked to the Poisson rates $\lambda_i$ via a known [forward model](@entry_id:148443), $\lambda_i = f_i(\theta) > 0$ .

The probability [mass function](@entry_id:158970) for a single count $y_i$ is $P(y_i \mid \theta) = \frac{(f_i(\theta))^{y_i} \exp(-f_i(\theta))}{y_i!}$. Due to independence, the joint [log-likelihood](@entry_id:273783) is the sum of the individual log-likelihoods:
$$
\ell(\theta \mid y_1, \dots, y_m) = \sum_{i=1}^{m} \left( y_i \ln(f_i(\theta)) - f_i(\theta) - \ln(y_i!) \right)
$$
Maximizing this function with respect to $\theta$ yields the MLE. This [objective function](@entry_id:267263) is clearly different from a least-squares criterion, reflecting the different statistical nature of the data.

### Computing the Maximum Likelihood Estimate

Finding the MLE requires solving an optimization problem. For differentiable [log-likelihood](@entry_id:273783) functions, a necessary condition for a candidate $\hat{\theta}$ to be a [local maximum](@entry_id:137813) is that the gradient of the [log-likelihood](@entry_id:273783), known as the **[score function](@entry_id:164520)**, vanishes at that point:
$$
S(\theta) = \nabla_\theta \ell(\theta; y) \quad \text{and we solve} \quad S(\hat{\theta}_{\text{MLE}}) = 0
$$
An important property of the [score function](@entry_id:164520) is that its expectation, taken with respect to the data distribution at the true parameter $\theta_0$, is zero: $\mathbb{E}[S(\theta_0)] = 0$.

For the Gaussian case with constant covariance $\Sigma$, the [score function](@entry_id:164520) is :
$$
S(\theta) = \nabla_\theta \left( -\frac{1}{2}(y - \mathcal{G}(\theta))^\top \Sigma^{-1} (y - \mathcal{G}(\theta)) \right) = (D\mathcal{G}(\theta))^\top \Sigma^{-1} (y - \mathcal{G}(\theta))
$$
where $D\mathcal{G}(\theta)$ is the Jacobian matrix (or sensitivity matrix) of the forward operator. Setting this to zero yields the [normal equations](@entry_id:142238) for the weighted [least-squares problem](@entry_id:164198). For the Poisson model, the [score function](@entry_id:164520) is :
$$
S(\theta) = \sum_{i=1}^{m} \left( \frac{y_i}{f_i(\theta)} - 1 \right) f_i'(\theta)
$$
where $f_i'(\theta)$ is the derivative of the rate function with respect to $\theta$.

#### Numerical Optimization: Newton and Gauss-Newton Methods

In most realistic [inverse problems](@entry_id:143129), the score equation $S(\theta) = 0$ is a [nonlinear system](@entry_id:162704) that cannot be solved analytically. This necessitates the use of iterative numerical [optimization algorithms](@entry_id:147840). **Newton's method** is a powerful second-order technique. Starting from an initial guess $\theta_k$, it computes the next iterate $\theta_{k+1}$ by modeling the objective function as a quadratic and jumping to its minimum. This leads to the update step:
$$
\theta_{k+1} = \theta_k - (H_\ell(\theta_k))^{-1} S(\theta_k)
$$
where $H_\ell(\theta) = \nabla_\theta^2 \ell(\theta; y)$ is the Hessian matrix of the [log-likelihood](@entry_id:273783).

For the common nonlinear [least-squares problem](@entry_id:164198) arising from Gaussian MLE, computing the full Hessian can be complex and computationally expensive. The Hessian of the [negative log-likelihood](@entry_id:637801) $\Phi(u) = \frac{1}{2} \|y - G(u)\|_{\Gamma^{-1}}^2$ is :
$$
H_\Phi(u) = \underbrace{G'(u)^\top \Gamma^{-1} G'(u)}_{\text{Gauss-Newton Hessian}} - \underbrace{\sum_{i=1}^m \left[ \nabla^2 G_i(u) \right] (\Gamma^{-1}(y-G(u)))_i}_{\text{Second-order term}}
$$
where $G'(u)$ is the Jacobian of $G$. The **Gauss-Newton method** approximates the full Hessian by dropping the second-order term, which involves second derivatives of the [forward model](@entry_id:148443) and is weighted by the residual $y-G(u)$. The Gauss-Newton approximate Hessian is $H_{GN}(u) = G'(u)^\top \Gamma^{-1} G'(u)$.

This approximation has several important properties :
*   **Computational Simplicity:** It only requires the first derivative (Jacobian) of the forward model, which is often available or easier to compute than the second derivative.
*   **Positive Semidefiniteness:** The matrix $H_{GN}(u)$ is always positive semidefinite (and positive definite if $G'(u)$ has full column rank), which ensures that the Gauss-Newton step is a descent direction for the minimization problem. The full Hessian, in contrast, can be indefinite, especially far from the minimum, which can complicate Newton's method.
*   **Accuracy:** The approximation is exact if the forward model $G(u)$ is linear or if the residual at the current iterate is zero. It is a good approximation in mildly nonlinear problems or near the solution where residuals are expected to be small. However, for highly nonlinear problems or in cases with large residuals (e.g., poor model fit or early in the optimization), the neglected term can be significant, and the Gauss-Newton step can differ substantially from the true Newton step.

### Uncertainty Quantification: Fisher Information and the Cramér-Rao Bound

A [point estimate](@entry_id:176325) $\hat{\theta}_{\text{MLE}}$ is of limited value without a measure of its uncertainty. The curvature of the log-likelihood surface at its peak provides this information. A sharply peaked likelihood implies that the data are highly informative, and the estimate is precise. A flat likelihood implies the data are less informative, and the estimate has high uncertainty.

The **Fisher Information Matrix (FIM)**, $I(\theta)$, mathematically formalizes this notion of curvature. It is defined as the expectation of the negative Hessian of the log-likelihood:
$$
I(\theta) = \mathbb{E}[- \nabla_\theta^2 \ell(\theta; y)] = \mathbb{E}[- H_\ell(\theta)]
$$
The expectation is taken over the distribution of the data $y$ for a fixed $\theta$. An alternative, often equivalent, definition is the covariance of the [score function](@entry_id:164520): $I(\theta) = \mathbb{E}[S(\theta)S(\theta)^\top]$.

For the Gaussian noise model, the Hessian of the [negative log-likelihood](@entry_id:637801) contains the Gauss-Newton term and the residual-weighted second-order term. Because the residual has [zero mean](@entry_id:271600), the expectation of the second-order term vanishes. Thus, the FIM is exactly the Gauss-Newton approximate Hessian :
$$
I(\theta) = G'(\theta)^\top \Gamma^{-1} G'(\theta)
$$
This provides a profound connection: the matrix used in the Gauss-Newton optimization step is also the measure of information about the parameters. For the Poisson model, a direct calculation shows that the FIM is :
$$
\mathcal{I}(\theta) = \sum_{i=1}^{m} \frac{(f_i'(\theta))^2}{f_i(\theta)}
$$

The FIM is crucial because it sets a fundamental limit on the precision of any unbiased estimator. The **Cramér-Rao Lower Bound (CRLB)** states that the covariance matrix of any [unbiased estimator](@entry_id:166722) $\hat{\theta}$ must satisfy:
$$
\text{Cov}(\hat{\theta}) \ge I(\theta)^{-1}
$$
This is a [matrix inequality](@entry_id:181828), meaning the difference of the two matrices is positive semidefinite. It implies that the variance of any single parameter estimate, $\hat{\theta}_j$, is bounded below by the corresponding diagonal element of the inverse FIM: $\text{Var}(\hat{\theta}_j) \ge (I(\theta)^{-1})_{jj}$.

An estimator that achieves this lower bound (at least asymptotically) is called **efficient**. The MLE is asymptotically efficient under suitable regularity conditions.

To see how this plays out in an [inverse problem](@entry_id:634767), consider a linear infinite-dimensional problem $y = Kx + \varepsilon$, where $K$ is a compact operator with a [singular system](@entry_id:140614) $\{(\sigma_i, u_i, f_i)\}$. The data can be decomposed into independent scalar equations $y_i = \sigma_i x_i + \varepsilon_i$, where $x_i = \langle x, u_i \rangle$ and $y_i = \langle y, f_i \rangle$. For Gaussian noise $\varepsilon_i \sim \mathcal{N}(0, \sigma^2)$, the FIM for the coefficients $\{x_i\}_{i=1}^m$ is a diagonal matrix with entries $\frac{\sigma_i^2}{\sigma^2}$. The CRLB for estimating a [linear combination](@entry_id:155091) $\theta_m(x) = \sum_{i=1}^m a_i x_i$ is then :
$$
\text{Var}(\hat{\theta}_m) \ge \sigma^2 \sum_{i=1}^m \frac{a_i^2}{\sigma_i^2}
$$
This result powerfully illustrates the nature of [ill-posedness](@entry_id:635673). The singular values $\sigma_i$ decay to zero. The bound on the variance is inflated by factors of $1/\sigma_i^2$. This means that components of $x$ corresponding to small singular values are associated with enormous uncertainty and are difficult to estimate from the data. The MLE for this problem, $\hat{x}_i = y_i / \sigma_i$, is unbiased and its variance can be shown to attain the CRLB, confirming its efficiency in this context .

### Advanced Principles and Practical Applications

#### Practical Identifiability

While theoretical identifiability asks if $\theta_1 \neq \theta_2$ implies $p(y | \theta_1) \neq p(y | \theta_2)$, **[practical identifiability](@entry_id:190721)** asks whether the effect of changing a parameter can be distinguished from noise in a finite-data setting. The FIM and CRLB provide the diagnostic tools.

A model is practically non-identifiable if certain parameters or combinations of parameters can be changed significantly without a statistically detectable change in the predicted data. This corresponds to directions in parameter space where the likelihood surface is very flat. In terms of the FIM, this means $I(\theta)$ has very small eigenvalues. The inverse FIM, $I(\theta)^{-1}$, will then have very large eigenvalues, and the CRLB predicts large variances for parameter combinations along the corresponding eigenvectors.

A crucial issue is that the eigenvalues of the FIM depend on parameter scaling. To diagnose [practical non-identifiability](@entry_id:270178), one should analyze a properly scaled FIM, e.g., $S I(\theta) S$, where $S$ is a [diagonal matrix](@entry_id:637782) of typical parameter scales. A large **condition number** of this scaled FIM, $\kappa(S I(\theta) S) = \lambda_{\max}/\lambda_{\min}$, signals extreme anisotropy in the likelihood surface. It indicates that while some parameter combinations are well-determined (sharp curvature), others are very poorly determined (flat curvature), which is the hallmark of [practical non-identifiability](@entry_id:270178) .

#### Connection to Bayesian Inference and Regularization

MLE is a frequentist approach, but it is deeply connected to the Bayesian framework. In **Bayesian inference**, one combines the likelihood $p(y|\theta)$ with a **prior distribution** $p(\theta)$ that encodes prior beliefs about the parameters. The result, via Bayes' rule, is the **[posterior distribution](@entry_id:145605)** $p(\theta|y) \propto p(y|\theta)p(\theta)$.

The **Maximum A Posteriori (MAP)** estimate is the mode of this [posterior distribution](@entry_id:145605):
$$
\hat{\theta}_{\text{MAP}} = \underset{\theta}{\arg\max} \, p(\theta|y) = \underset{\theta}{\arg\max} \, \left( \ell(\theta; y) + \ln p(\theta) \right)
$$
Thus, MAP estimation is equivalent to minimizing the [negative log-likelihood](@entry_id:637801) plus a penalty term, $-\ln p(\theta)$. This is known as **penalized maximum likelihood**.

This connection provides a probabilistic interpretation for many [regularization techniques](@entry_id:261393) used in [inverse problems](@entry_id:143129) :
*   **Gaussian Prior:** If we assume a Gaussian prior $\theta \sim \mathcal{N}(m, B)$, the penalty is $-\ln p(\theta) = \frac{1}{2}(\theta - m)^\top B^{-1}(\theta - m) + \text{const}$. This is a [quadratic penalty](@entry_id:637777). If $B = \tau^2 I$, this becomes the classic Tikhonov regularization penalty, $\frac{1}{2\tau^2}\|\theta - m\|_2^2$. The MAP objective combines the [data misfit](@entry_id:748209) from the likelihood with this quadratic departure from the prior mean.
*   **Laplace Prior:** If we assume a Laplace prior on the parameters, the penalty term is proportional to the $\ell_1$-norm, $\|\theta - m\|_1$. This form of regularization is known to promote [sparse solutions](@entry_id:187463).
*   **Flat Prior:** If one uses a "flat" or uninformative prior, $p(\theta) \propto \text{const}$, the MAP estimate coincides with the MLE.

For [ill-posed problems](@entry_id:182873) where the MLE is not unique (e.g., when the Hessian $G'^\top \Gamma^{-1} G'$ is singular), the inclusion of a proper prior (with a positive definite covariance $B$) makes the MAP objective strictly convex, guaranteeing a unique and stable solution . However, in the large-data limit, the likelihood term typically dominates the fixed prior term, and the MAP and MLE estimates converge. This is often summarized as "the data swamps the prior" .

#### Hypothesis Testing and Confidence Regions

Likelihood theory provides principled methods for hypothesis testing and constructing confidence regions. The **Likelihood Ratio (LR) test** is a powerful tool for comparing a full model with a nested, constrained sub-model.

Suppose we want to test a null hypothesis $H_0$ that restricts $\theta$ to a subspace $\Theta_0 \subset \mathbb{R}^p$, for example, through constraints $h(\theta)=0$. Let $\hat{\theta}$ be the unconstrained MLE and $\hat{\theta}_0$ be the constrained MLE. The LR [test statistic](@entry_id:167372) is:
$$
T_n = 2(\ell(\hat{\theta}) - \ell(\hat{\theta}_0))
$$
According to **Wilks' Theorem**, under suitable regularity conditions and if $H_0$ is true, $T_n$ asymptotically follows a [chi-square distribution](@entry_id:263145), $T_n \overset{d}{\to} \chi^2_r$. The degrees of freedom, $r$, is the number of independent constraints imposed by $H_0$ (i.e., the dimension of $h(\theta)$) . For example, if $\theta \in \mathbb{R}^5$ and the constraint is $K\theta = 0$ with a rank-3 matrix $K$, the degrees of freedom are $r=3$.

A $(1-\alpha)$ confidence region for $\theta$ can be constructed by inverting this test. It consists of all parameter values $\theta_0$ that would not be rejected by the test at [significance level](@entry_id:170793) $\alpha$:
$$
\mathcal{C}_{1-\alpha} = \{\theta_0 : 2(\ell(\hat{\theta}) - \ell(\theta_0)) \le \chi^2_{1-\alpha}(p) \}
$$
where $p$ is the dimension of $\theta$. This defines a region bounded by a contour of the log-likelihood surface.

A common challenge is the presence of **[nuisance parameters](@entry_id:171802)**. If $\theta = (\psi, \lambda)$, where $\psi$ is the parameter of interest and $\lambda$ is a [nuisance parameter](@entry_id:752755), we can use the **[profile likelihood](@entry_id:269700)**. The profile [log-likelihood](@entry_id:273783) for $\psi$ is defined by maximizing out the [nuisance parameter](@entry_id:752755) for each fixed value of $\psi$:
$$
\ell_p(\psi; y) = \max_\lambda \ell(\psi, \lambda; y)
$$
The likelihood ratio statistic based on the [profile likelihood](@entry_id:269700), $2(\ell_p(\hat{\psi}; y) - \ell_p(\psi_0; y))$, asymptotically follows a $\chi^2_{d_\psi}$ distribution, where $d_\psi$ is the dimension of $\psi$. Inverting this test gives a confidence region for $\psi$ without requiring any specification of a prior for $\lambda$ or performing Bayesian [marginalization](@entry_id:264637) .

#### Dealing with Model Misspecification

The properties of MLE, such as consistency and [asymptotic efficiency](@entry_id:168529), rely on the assumption that the chosen likelihood model is correct. When the model is misspecified, the estimator that maximizes the incorrect likelihood is called a **Quasi-Maximum Likelihood Estimator (QMLE)**.

The QMLE can still be consistent for some parameters if the working likelihood is chosen such that the [score function](@entry_id:164520) still has zero expectation at the true parameter value. For instance, in a linear model $y_i = s_i \theta + \varepsilon_i$ with true zero-mean errors, using a Gaussian likelihood yields an estimator that is equivalent to [ordinary least squares](@entry_id:137121), which is consistent for $\theta$ regardless of the true error distribution .

However, the FIM derived from the misspecified model is no longer valid for computing the estimator's variance. The correct [asymptotic variance](@entry_id:269933) is given by the **[sandwich covariance matrix](@entry_id:754502)**, which robustly accounts for the misspecification:
$$
V_{QMLE} = A(\theta_0)^{-1} B(\theta_0) A(\theta_0)^{-1}
$$
where $A(\theta) = \mathbb{E}_{\text{true}}[- \nabla_\theta^2 \ell_{\text{work}}(\theta)]$ is the expectation of the negative Hessian of the *working* log-likelihood, and $B(\theta) = \mathbb{E}_{\text{true}}[S_{\text{work}}(\theta)S_{\text{work}}(\theta)^\top]$ is the covariance of the *working* [score function](@entry_id:164520). Both expectations are taken under the *true* data-generating distribution. This sandwich form emerges because the [information matrix](@entry_id:750640) equality ($A=B$) no longer holds under misspecification.

This same sandwich structure, often involving the **Godambe [information matrix](@entry_id:750640)**, also arises when the full likelihood is intractable and is replaced by a **composite likelihood**. A composite likelihood is formed by multiplying lower-dimensional marginal or conditional likelihoods (e.g., all pairwise marginals). The resulting estimator is typically consistent but not fully efficient. Its [asymptotic variance](@entry_id:269933) is given by a sandwich formula, reflecting the fact that the composite score equation is an unbiased estimating equation but not the true score equation of the full data generating process . This provides a powerful, unified view on estimation under various forms of model imperfection.