## Introduction
The method of maximum likelihood represents a cornerstone of modern data analysis, providing a powerful and versatile framework for extracting scientific insights from experimental data. In high-energy physics (HEP), where statistical precision is paramount and models are often complex, this method is the primary tool for [parameter estimation](@entry_id:139349), hypothesis testing, and [uncertainty quantification](@entry_id:138597). However, applying these techniques to real-world data presents significant challenges, from handling imperfections in detector response to accounting for numerous sources of [systematic uncertainty](@entry_id:263952). This article addresses the need for a coherent statistical framework that can rigorously manage these complexities.

Over the next three sections, you will build a comprehensive understanding of maximum likelihood fits. The journey begins in **Principles and Mechanisms**, where we will construct the unbinned and [binned likelihood](@entry_id:746807) functions from first principles, explore the mathematics of their optimization, and establish the methods for estimating parameter uncertainties. Next, in **Applications and Interdisciplinary Connections**, we will transition from theory to practice, demonstrating how the likelihood is adapted to solve real-world HEP problems, such as correcting for detector effects and incorporating [systematic uncertainties](@entry_id:755766) via [nuisance parameters](@entry_id:171802). Finally, **Hands-On Practices** will provide opportunities to solidify these concepts through targeted computational exercises. By the end, you will have a deep appreciation for the theoretical elegance and practical power of maximum likelihood methods in scientific discovery.

## Principles and Mechanisms

The method of maximum likelihood is a cornerstone of [statistical inference](@entry_id:172747) in [high-energy physics](@entry_id:181260), providing a robust and versatile framework for [parameter estimation](@entry_id:139349), [hypothesis testing](@entry_id:142556), and uncertainty quantification. This chapter delves into the fundamental principles and mechanisms underlying maximum likelihood fits, focusing on two primary modalities: unbinned and binned analyses. We will construct the [likelihood function](@entry_id:141927) from first principles, explore extensions to realistic multi-component models, discuss the mechanics of its numerical maximization, and detail the methods for estimating parameter uncertainties and incorporating systematic effects.

### The Unbinned Likelihood Function

The most direct application of the maximum [likelihood principle](@entry_id:162829) is to an **unbinned** dataset, where the precise value of each measurement is retained. Consider a set of $N$ events, each characterized by an observable $x$, for which we have measurements $\{x_1, x_2, \dots, x_N\}$. If these events are [independent and identically distributed](@entry_id:169067) (i.i.d.), each drawn from a probability density function (PDF) $f(x \mid \boldsymbol{\theta})$ that depends on a vector of parameters $\boldsymbol{\theta}$, the [joint probability](@entry_id:266356) density for observing this specific dataset is the product of the individual densities:
$$
p(\{x_i\} \mid \boldsymbol{\theta}) = \prod_{i=1}^{N} f(x_i \mid \boldsymbol{\theta})
$$
The **[likelihood function](@entry_id:141927)**, denoted $L(\boldsymbol{\theta})$, is this joint probability density re-interpreted as a function of the parameters $\boldsymbol{\theta}$ for the fixed, observed data.
$$
L(\boldsymbol{\theta}) = \prod_{i=1}^{N} f(x_i \mid \boldsymbol{\theta})
$$
The central tenet of the method of maximum likelihood is to estimate the true parameters $\boldsymbol{\theta}$ with the values, $\hat{\boldsymbol{\theta}}$, that maximize this function. The intuition is that the best-fit parameters are those that make the observed data most probable.

For this construction to be statistically valid, the model $f(x \mid \boldsymbol{\theta})$ must be a proper PDF for every value of $\boldsymbol{\theta}$ in the parameter space. This imposes three essential mathematical conditions:
1.  **Non-negativity**: $f(x \mid \boldsymbol{\theta}) \ge 0$ for all $x$. Probabilities cannot be negative.
2.  **Normalization**: $\int f(x \mid \boldsymbol{\theta}) \, dx = 1$. The total probability over the entire observable space must be unity.
3.  **Measurability**: The function must be measurable, a technical condition that ensures its integral is well-defined.

Notably, for the [likelihood function](@entry_id:141927) to simply exist, no further conditions such as differentiability with respect to $\boldsymbol{\theta}$ are strictly necessary. However, such "regularity conditions" are required to establish the desirable asymptotic properties of the resulting estimators and to employ [gradient-based optimization](@entry_id:169228) methods .

In practice, it is almost always more convenient to work with the natural logarithm of the likelihood, known as the **[log-likelihood function](@entry_id:168593)**, $\ell(\boldsymbol{\theta}) = \ln L(\boldsymbol{\theta})$.
$$
\ell(\boldsymbol{\theta}) = \ln \left( \prod_{i=1}^{N} f(x_i \mid \boldsymbol{\theta}) \right) = \sum_{i=1}^{N} \ln f(x_i \mid \boldsymbol{\theta})
$$
Since the logarithm is a strictly [monotonic function](@entry_id:140815), maximizing $\ell(\boldsymbol{\theta})$ is equivalent to maximizing $L(\boldsymbol{\theta})$. The log-likelihood's primary advantages are computational: it converts products into sums, which are numerically more stable and analytically more tractable, and it often has a more favorable landscape for numerical optimization.

### Extended Maximum Likelihood

In many physics analyses, the total number of observed events $N$ is not fixed in advance but is itself an outcome of the experiment. The **extended maximum likelihood** method incorporates this information by treating $N$ as a Poisson random variable with a mean expected yield $\nu(\boldsymbol{\theta})$ that may also depend on the model parameters.

The full probability of observing a specific dataset is now the product of the probability of observing exactly $N$ events and the probability of those $N$ events having the specific values $\{x_i\}$. This gives rise to the extended likelihood function:
$$
L(\boldsymbol{\theta}) = \frac{\nu(\boldsymbol{\theta})^N \exp(-\nu(\boldsymbol{\theta}))}{N!} \prod_{i=1}^{N} f(x_i \mid \boldsymbol{\theta})
$$
The corresponding extended [log-likelihood](@entry_id:273783) is:
$$
\ell(\boldsymbol{\theta}) = N \ln \nu(\boldsymbol{\theta}) - \nu(\boldsymbol{\theta}) - \ln(N!) + \sum_{i=1}^{N} \ln f(x_i \mid \boldsymbol{\theta})
$$
A remarkable property of this formulation is that if the overall yield $\nu$ is a free parameter independent of the [shape parameters](@entry_id:270600) in $f(x \mid \boldsymbol{\theta})$, its maximum likelihood estimate (MLE) is simply the observed number of events, $\hat{\nu} = N$ .

This framework becomes particularly powerful for models comprising multiple components, such as a signal and one or more backgrounds. Consider a two-component model with expected signal yield $\mu_s$ and background yield $\mu_b$. The total expected yield is $\nu = \mu_s + \mu_b$. The PDF for any single event is a mixture model:
$$
f(x) = \frac{\mu_s s(x) + \mu_b b(x)}{\mu_s + \mu_b}
$$
where $s(x)$ and $b(x)$ are the unit-normalized PDFs for the signal and background components, respectively. Naively inserting this into the standard likelihood would be cumbersome. However, a significant simplification occurs in the extended likelihood formalism. Starting from the standard mixture model likelihood and multiplying by the Poisson term for the total yield $N$ gives:
$$
L(\mu_s, \mu_b) = \frac{(\mu_s + \mu_b)^N \exp(-(\mu_s + \mu_b))}{N!} \prod_{i=1}^{N} \left( \frac{\mu_s s(x_i) + \mu_b b(x_i)}{\mu_s + \mu_b} \right)
$$
The term $(\mu_s + \mu_b)^N$ in the denominator of the product cancels with the identical term in the numerator of the Poisson factor, leading to the elegant and widely used form of the extended [unbinned likelihood](@entry_id:756294) for a multi-component model :
$$
L(\mu_s, \mu_b) = \frac{\exp(-(\mu_s + \mu_b))}{N!} \prod_{i=1}^{N} (\mu_s s(x_i) + \mu_b b(x_i))
$$
The [log-likelihood](@entry_id:273783) becomes:
$$
\ell(\mu_s, \mu_b) = -(\mu_s + \mu_b) + \sum_{i=1}^{N} \ln(\mu_s s(x_i) + \mu_b b(x_i))
$$
(dropping the constant term $\ln(N!)$). This formulation simultaneously estimates the component yields and any [shape parameters](@entry_id:270600) embedded within $s(x)$ and $b(x)$.

### Binned Likelihood Fits and Goodness-of-Fit

While unbinned fits utilize the maximal information from the data, **[binned likelihood](@entry_id:746807) fits** are often preferred for their computational speed, simpler handling of certain [systematic uncertainties](@entry_id:755766), and the ability to perform straightforward [goodness-of-fit](@entry_id:176037) tests. In this approach, the range of the observable $x$ is divided into $K$ disjoint bins, and the data are reduced to a set of observed counts $\{n_1, n_2, \dots, n_K\}$.

The model predicts the expected count $\mu_k(\boldsymbol{\theta})$ for each bin $k$. The observed count $n_k$ is modeled as an independent Poisson random variable with mean $\mu_k(\boldsymbol{\theta})$. The [binned likelihood](@entry_id:746807) is the product of these Poisson probabilities:
$$
L(\boldsymbol{\theta}) = \prod_{k=1}^{K} \frac{\mu_k(\boldsymbol{\theta})^{n_k} \exp(-\mu_k(\boldsymbol{\theta}))}{n_k!}
$$
The binned [log-likelihood](@entry_id:273783), dropping parameter-independent constants, is:
$$
\ell(\boldsymbol{\theta}) = \sum_{k=1}^{K} \left( n_k \ln \mu_k(\boldsymbol{\theta}) - \mu_k(\boldsymbol{\theta}) \right)
$$
A key advantage of [binning](@entry_id:264748) is the ability to assess how well the fitted model describes the observed data distribution. This is achieved by comparing the likelihood of the fitted model, $L(\hat{\boldsymbol{\theta}})$, to that of a **saturated model**. The saturated model is a "perfect" model with one parameter per bin, such that its predictions exactly match the data: $\hat{\mu}_k^{\text{sat}} = n_k$. The likelihood of the saturated model represents the best possible fit to the binned data.

The **[deviance](@entry_id:176070)**, $D$, is defined as twice the difference in log-likelihood between the saturated and the fitted models :
$$
D = 2(\ln L_{\text{sat}} - \ln L(\hat{\boldsymbol{\theta}})) = 2 \sum_{k=1}^{K} \left[ \hat{\mu}_k - n_k + n_k \ln\left(\frac{n_k}{\hat{\mu}_k}\right) \right]
$$
This quantity serves as a powerful [goodness-of-fit](@entry_id:176037) statistic. According to **Wilks's theorem**, if the fitted model is correct, the [deviance](@entry_id:176070) $D$ asymptotically follows a chi-square ($\chi^2$) distribution with a number of degrees of freedom equal to the number of bins minus the number of fitted parameters ($v = K - P$). A large value of $D$ (and a correspondingly small $p$-value from the $\chi^2$ distribution) indicates that the model provides a poor description of the data. However, this [asymptotic approximation](@entry_id:275870) is only reliable when the [expected counts](@entry_id:162854) in all bins are sufficiently large (e.g., $\mu_k \gtrsim 5$). In the common high-energy physics scenario of low-count bins, the $\chi^2$ approximation can fail, and the distribution of $D$ should be calibrated using Monte Carlo simulations .

### Maximizing the Likelihood

Finding the MLE $\hat{\boldsymbol{\theta}}$ requires solving the system of **score equations**, $\nabla \ell(\boldsymbol{\theta}) = 0$. The score is the gradient of the log-likelihood. For the [signal-plus-background](@entry_id:754818) extended model, the score equations for the yields are :
$$
\frac{\partial \ell}{\partial \mu_s} = -1 + \sum_{i=1}^{N} \frac{s(x_i)}{\mu_s s(x_i) + \mu_b b(x_i)} = 0
$$
$$
\frac{\partial \ell}{\partial \mu_b} = -1 + \sum_{i=1}^{N} \frac{b(x_i)}{\mu_s s(x_i) + \mu_b b(x_i)} = 0
$$
In some cases, the model PDF itself has a parameter-dependent normalization factor, or **partition function**, $Z(\boldsymbol{\theta})$, such that $f(x \mid \boldsymbol{\theta}) = h(x \mid \boldsymbol{\theta}) / Z(\boldsymbol{\theta})$. This introduces an additional term into the score. The derivative of the log-likelihood becomes :
$$
\frac{\partial \ell(\boldsymbol{\theta})}{\partial \theta_j} = \sum_{i=1}^{N} \left( \frac{\partial \ln h(x_i, \boldsymbol{\theta})}{\partial \theta_j} - E_{f(x|\boldsymbol{\theta})}\left[ \frac{\partial \ln h(x, \boldsymbol{\theta})}{\partial \theta_j} \right] \right)
$$
This reveals that the score contribution from each event is its individual score term minus the expectation value of that term over the model—a structure of "observed minus expected".

Except in the simplest cases, the score equations cannot be solved analytically. Instead, iterative numerical optimization algorithms are used. A fundamental and powerful method is the **Newton-Raphson algorithm**. It approximates the [log-likelihood function](@entry_id:168593) as a quadratic surface around the current iterate $\boldsymbol{\theta}_k$ and then jumps to the maximum of that approximation. This leads to the update rule :
$$
\boldsymbol{\theta}_{k+1} = \boldsymbol{\theta}_k - H(\boldsymbol{\theta}_k)^{-1} g(\boldsymbol{\theta}_k)
$$
where $g(\boldsymbol{\theta}_k) = \nabla \ell(\boldsymbol{\theta}_k)$ is the gradient (score) and $H(\boldsymbol{\theta}_k) = \nabla^2 \ell(\boldsymbol{\theta}_k)$ is the Hessian matrix of second derivatives.

While Newton's method offers fast [quadratic convergence](@entry_id:142552) near the maximum, it has practical limitations. The [log-likelihood](@entry_id:273783) functions encountered in physics, such as those for mixture models, are often not globally concave. If the Hessian $H(\boldsymbol{\theta}_k)$ is not [negative definite](@entry_id:154306) (a condition for a [local maximum](@entry_id:137813)), the pure Newton step may not be an ascent direction. Furthermore, even in a concave region, a full step can "overshoot" the maximum or violate physical parameter boundaries (e.g., proposing a negative yield). To ensure robust convergence, these algorithms are augmented with **globalization strategies**. A **line search** algorithm, for instance, scales the Newton step by a factor $\alpha$ chosen to satisfy a sufficient increase condition (like the Armijo condition). This prevents overshooting and ensures progress toward the maximum at each step .

### Estimating Parameter Uncertainties

Once the MLE $\hat{\boldsymbol{\theta}}$ has been found, the next crucial task is to determine its statistical uncertainty. This is quantified by the variance-covariance matrix of the estimator, $\text{Cov}(\hat{\boldsymbol{\theta}})$. In the large-sample limit, the covariance is intimately related to the curvature of the [log-likelihood function](@entry_id:168593) at its maximum.

The curvature is described by the **[information matrix](@entry_id:750640)**. We define two related quantities:
1.  The **[observed information](@entry_id:165764) matrix**, $J(\boldsymbol{\theta}) = -\nabla^2 \ell(\boldsymbol{\theta}) = -H(\boldsymbol{\theta})$, which is the negative of the Hessian of the [log-likelihood](@entry_id:273783). It depends on the specific data observed.
2.  The **expected Fisher [information matrix](@entry_id:750640)**, $I(\boldsymbol{\theta}) = E[J(\boldsymbol{\theta})]$, which is the [expectation value](@entry_id:150961) of the [observed information](@entry_id:165764), averaged over all possible datasets that could be generated by the model.

A cornerstone result of likelihood theory, derivable from a Taylor expansion of the [score function](@entry_id:164520), states that in the large-sample limit, the distribution of the MLE $\hat{\boldsymbol{\theta}}$ approaches a multivariate Gaussian centered on the true value $\boldsymbol{\theta}_0$ with a covariance matrix given by the inverse of the Fisher [information matrix](@entry_id:750640): $\text{Cov}(\hat{\boldsymbol{\theta}}) \approx I(\boldsymbol{\theta}_0)^{-1}$ . This provides the theoretical basis for the **Cramér-Rao lower bound**, which states that the variance of any [unbiased estimator](@entry_id:166722) for a parameter $\theta$ cannot be smaller than $1/I(\theta)$.

In practice, since $\boldsymbol{\theta}_0$ is unknown, we estimate the covariance by inverting the [information matrix](@entry_id:750640) evaluated at the MLE, $\hat{\boldsymbol{\theta}}$. A common choice is to use the inverse of the [observed information](@entry_id:165764) matrix :
$$
\widehat{\text{Cov}}(\hat{\boldsymbol{\theta}}) = J(\hat{\boldsymbol{\theta}})^{-1} = \left( -\nabla^2 \ell(\boldsymbol{\theta}) |_{\boldsymbol{\theta}=\hat{\boldsymbol{\theta}}} \right)^{-1}
$$
This estimator uses the actual curvature of the likelihood at the discovered maximum. Alternatively, one can use the inverse of the expected Fisher information, $I(\hat{\boldsymbol{\theta}})^{-1}$. The latter can be advantageous as it averages out statistical fluctuations present in a single dataset, often yielding more stable uncertainty estimates, especially in small samples or binned fits with noisy bin counts .

As a concrete example, for a simple [exponential decay model](@entry_id:634765) with lifetime $\tau$, the CRLB for $N$ events is $\tau^2/N$. The variance estimated from the [observed information](@entry_id:165764) for a specific dataset is $\hat{\tau}^2/N$, where $\hat{\tau}$ is the MLE from that dataset. The ratio of these two quantities, $(\hat{\tau}/\tau)^2$, reflects how the statistical fluctuation in the specific dataset (manifesting in $\hat{\tau}$) leads to an estimated uncertainty that differs from the theoretical average .

### Incorporating Systematic Uncertainties

Real-world analyses are affected by [systematic uncertainties](@entry_id:755766), such as detector calibration, luminosity, or theoretical modeling imperfections. These are incorporated into the likelihood framework using **[nuisance parameters](@entry_id:171802)**, $\boldsymbol{\eta}$. The likelihood becomes a function of both the parameters of interest, $\boldsymbol{\theta}$, and the [nuisance parameters](@entry_id:171802): $L(\boldsymbol{\theta}, \boldsymbol{\eta})$.

To prevent [nuisance parameters](@entry_id:171802) from being unconstrained by the main measurement, they are "penalized" by including additional terms in the likelihood that represent external knowledge, for instance from calibration studies. In a frequentist analysis, this is rigorously interpreted as extending the likelihood to include auxiliary measurements that constrain $\boldsymbol{\eta}$. For example, if an auxiliary measurement estimates a [nuisance parameter](@entry_id:752755) $\eta_j$ to be $\eta_{0j}$ with uncertainty $\sigma_j$, this is modeled as an auxiliary dataset whose likelihood is a Gaussian function :
$$
L_{\text{aux}}(\eta_j) \propto \exp\left( -\frac{(\eta_j - \eta_{0j})^2}{2\sigma_j^2} \right)
$$
The total likelihood is the product of the main likelihood and all such auxiliary likelihood terms: $L_{\text{total}} = L_{\text{main}}(\boldsymbol{\theta}, \boldsymbol{\eta}) \times \prod_j L_{\text{aux}, j}(\eta_j)$. The parameters $\boldsymbol{\theta}$ and $\boldsymbol{\eta}$ are then estimated by maximizing this combined likelihood. Inference on $\boldsymbol{\theta}$ is typically done using the [profile likelihood](@entry_id:269700), where $\boldsymbol{\eta}$ is re-maximized for each tested value of $\boldsymbol{\theta}$. This construction ensures that the resulting confidence intervals for $\boldsymbol{\theta}$ have the correct [frequentist coverage](@entry_id:749592) properties. It is conceptually distinct from a Bayesian approach where the constraint term would be interpreted as a [prior probability](@entry_id:275634) distribution for $\boldsymbol{\eta}$ .

Different types of [nuisance parameters](@entry_id:171802) call for different constraint forms.
- A parameter $\delta$ representing an additive shape variation that can be positive or negative is naturally constrained by a symmetric **Gaussian** term.
- A parameter $\eta$ representing a multiplicative normalization factor, which must be positive ($\eta > 0$), is more appropriately constrained by an asymmetric **log-normal** distribution. A log-normal constraint arises when the logarithm of the parameter is assumed to be Gaussian, e.g., $\ln \eta \sim \mathcal{N}(0, \sigma_\eta^2)$. This implies a PDF for $\eta$ of the form $p(\eta) \propto \frac{1}{\eta}\exp(-(\ln \eta)^2 / (2\sigma_\eta^2))$ .

A full likelihood for a binned fit with signal strength $\mu$, a log-normal normalization nuisance $\eta$, and a Gaussian shape nuisance $\delta$ would take the form :
$$
L(\mu, \eta, \delta) \propto \left( \prod_i (\lambda_i)^{n_i} \exp(-\lambda_i) \right) \times \frac{1}{\eta} \exp\left(-\frac{(\ln\eta)^2}{2\sigma_\eta^2}\right) \times \exp\left(-\frac{\delta^2}{2\sigma_\delta^2}\right)
$$
where $\lambda_i = \lambda_i(\mu, \eta, \delta)$ is the model prediction for bin $i$. The asymmetry of the log-normal constraint is a key feature, correctly modeling quantities where relative (percentage) uncertainties are symmetric, leading to an asymmetric PDF for the parameter itself.