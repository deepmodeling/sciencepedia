## Introduction
In the world of statistical inference, the method of maximum likelihood estimation (MLE) offers a powerful framework for estimating unknown parameters from data. While we can find the MLE for a distribution's primary parameter, such as the mean (λ) of a Poisson distribution or the success probability (p) of a Bernoulli trial, our scientific questions often concern derived quantities—like the odds of success, the median lifetime of a component, or the variance of a process. Deriving a new likelihood function for each of these transformed parameters would be a repetitive and often difficult task. This is the gap filled by the **invariance property of MLEs**, a fundamental principle that provides a direct and elegant "plug-in" solution. This article explores this crucial property in depth. The first chapter, **"Principles and Mechanisms,"** formally defines the [invariance principle](@entry_id:170175) and demonstrates its mechanics with core examples. The second chapter, **"Applications and Interdisciplinary Connections,"** showcases its vast utility across diverse fields like engineering, economics, and genetics. Finally, **"Hands-On Practices"** provides targeted problems to reinforce the concepts, making this property a tangible tool in your statistical toolkit.

## Principles and Mechanisms

In statistical inference, our primary goal is often to estimate the unknown parameters of a probability distribution based on observed data. The method of maximum likelihood provides a systematic approach to this problem, identifying the parameter values that render the observed data most probable. However, the parameter that directly governs the data-generating process may not always be the quantity of ultimate scientific or practical interest. We might be more concerned with a function of this parameter—such as a standard deviation, a probability of a specific event, a median lifetime, or an [odds ratio](@entry_id:173151). The **invariance property of maximum likelihood estimators (MLEs)** is a cornerstone principle that provides a direct and elegant method for finding the MLE of such transformed parameters.

### The Invariance Principle Stated

The invariance property, sometimes called the equivariance property, can be stated as follows:

If $\hat{\theta}$ is the maximum likelihood estimator of a parameter $\theta$, and if $g(\theta)$ is a function of $\theta$, then the maximum likelihood estimator of $g(\theta)$ is $g(\hat{\theta})$.

In essence, to find the MLE for a function of a parameter, one simply applies the function to the MLE of the original parameter. This property is remarkably powerful because it frees us from the often-laborious task of re-deriving the entire [likelihood function](@entry_id:141927) for the new parameter of interest. Once we have the MLE for the base parameter $\theta$, we can immediately obtain the MLE for an infinite number of related quantities, such as $\theta^2$, $1/\theta$, $\exp(\theta)$, or more complex functions.

The intuition behind this principle rests on the very definition of the likelihood function, $L(\theta | \text{data})$, which acts as a measure of plausibility for each possible value of $\theta$. The MLE, $\hat{\theta}$, is the value that maximizes this function, representing the most plausible value for the parameter given the data. If we are interested in a transformed parameter $\eta = g(\theta)$, it is natural to believe that the most plausible value for $\eta$ should correspond to the most plausible value of $\theta$.

If the function $g$ is a one-to-one (injective) transformation, the argument is straightforward. The likelihood function for $\eta$ can be expressed as $L^*(\eta | \text{data}) = L(g^{-1}(\eta) | \text{data})$. Since maximizing $L^*$ with respect to $\eta$ is equivalent to maximizing $L$ with respect to $\theta$, the maximum must occur at $\hat{\eta} = g(\hat{\theta})$. More formally, the property holds even when the function $g$ is not one-to-one. In such cases, the likelihood of a value $\eta_0$ is defined as the maximum likelihood over all $\theta$ that map to $\eta_0$. This is known as the **[profile likelihood](@entry_id:269700)**. The [invariance principle](@entry_id:170175) guarantees that applying the function $g$ to the global MLE $\hat{\theta}$ yields the MLE of $\eta$, a result rigorously established by Zehna in 1966.

### Applications with Common Transformations

Let's explore the application of this principle through a series of foundational examples, starting with simple algebraic transformations of parameters from [discrete distributions](@entry_id:193344).

Consider a scenario from a clinical trial where the outcome for $n$ patients is either "improvement" (success) or "no improvement" (failure). This can be modeled as a series of $n$ independent Bernoulli trials with an unknown probability of success, $p$. If we observe $k$ successes, the [likelihood function](@entry_id:141927) is $L(p) \propto p^k(1-p)^{n-k}$. By maximizing the [log-likelihood](@entry_id:273783), we find the familiar MLE for the success probability:
$$
\hat{p} = \frac{k}{n}
$$

Now, suppose we are interested in different quantities derived from $p$.

First, a quantum scientist might need to estimate the probability that two independent, identical qubits both collapse to the "success" state. This [joint probability](@entry_id:266356) is $\eta_1 = p^2$. Using the invariance property, the MLE for this quantity is simply the square of the MLE for $p$ [@problem_id:1925594]:
$$
\hat{\eta}_1 = (\hat{p})^2 = \left(\frac{k}{n}\right)^2
$$

In epidemiology and fields utilizing [logistic regression](@entry_id:136386), a more common metric is the **odds** of success, defined as $\eta_2 = \frac{p}{1-p}$. Instead of constructing a new [likelihood function](@entry_id:141927) in terms of $\eta_2$, we can apply the [invariance principle](@entry_id:170175) directly to $\hat{p}$ [@problem_id:1925557]:
$$
\hat{\eta}_2 = \frac{\hat{p}}{1-\hat{p}} = \frac{k/n}{1 - k/n} = \frac{k}{n-k}
$$

This result gives us the most likely value for the odds of a patient showing improvement, based on the trial data. Often, for [statistical modeling](@entry_id:272466), it is advantageous to work on an unrestricted scale. The **[log-odds](@entry_id:141427)**, or logit transformation, $\eta_3 = \ln\left(\frac{p}{1-p}\right)$, achieves this. Its MLE follows immediately [@problem_id:1925584]:
$$
\hat{\eta}_3 = \ln\left(\frac{\hat{p}}{1-\hat{p}}\right) = \ln\left(\frac{k}{n-k}\right)
$$
These examples illustrate how, from a single MLE $\hat{p}$, we can effortlessly estimate a whole family of related parameters that are central to different scientific disciplines.

### Invariance in Poisson and Exponential Models

The principle extends seamlessly to continuous and other [discrete distributions](@entry_id:193344). Consider a process modeled by a Poisson distribution, such as the number of alpha particles detected by a Geiger counter in a fixed time interval, or the number of non-coding mutations in a gene sequence. If we have $n$ observations $X_1, X_2, \ldots, X_n$ from a $\text{Poisson}(\lambda)$ distribution, the MLE for the mean rate $\lambda$ is the [sample mean](@entry_id:169249):
$$
\hat{\lambda} = \frac{1}{n}\sum_{i=1}^n X_i = \bar{X}
$$

A physicist might be interested in the probability of detecting exactly one particle in an interval, a quantity given by the function $g(\lambda) = \lambda e^{-\lambda}$. The invariance property allows for immediate estimation [@problem_id:1925579]:
$$
\widehat{g(\lambda)} = \hat{\lambda} e^{-\hat{\lambda}} = \bar{X} \exp(-\bar{X})
$$

Similarly, a biologist might want to estimate the probability that a [gene sequence](@entry_id:191077) has fewer than two mutations, i.e., $P(X < 2)$. For a Poisson variable, this probability is $\theta(\lambda) = P(X=0) + P(X=1) = e^{-\lambda} + \lambda e^{-\lambda} = (1+\lambda)e^{-\lambda}$. The MLE for this probability is found by substituting $\hat{\lambda}$ [@problem_id:1925606]:
$$
\hat{\theta} = (1+\hat{\lambda})e^{-\hat{\lambda}} = \left(1 + \bar{X}\right)\exp(-\bar{X})
$$

The same logic applies to [continuous distributions](@entry_id:264735). For instance, the lifetime of electronic components like solid-state drives is often modeled by an exponential distribution with rate parameter $\lambda$, having a PDF $f(x; \lambda) = \lambda \exp(-\lambda x)$. For a random sample $X_1, \ldots, X_n$, the MLE for the rate $\lambda$ is the reciprocal of the sample mean:
$$
\hat{\lambda} = \frac{1}{\bar{X}}
$$

For an [exponential distribution](@entry_id:273894), the mean is $1/\lambda$ and the standard deviation is also $1/\lambda$. Let's find the MLE for the standard deviation, $\sigma = 1/\lambda$. Applying the [invariance principle](@entry_id:170175) [@problem_id:1925596]:
$$
\hat{\sigma} = \frac{1}{\hat{\lambda}} = \frac{1}{1/\bar{X}} = \bar{X}
$$
This is a remarkable result: for an exponentially distributed sample, the maximum likelihood estimator for the standard deviation is the sample mean.

We can extend this to any characteristic of the distribution that can be expressed as a function of $\lambda$. For example, the median lifetime, $m$, is the time by which half of the components are expected to have failed. It is found by solving $1 - \exp(-\lambda m) = 0.5$, which yields $m = (\ln 2)/\lambda$. The MLE for the median is therefore [@problem_id:1925563]:
$$
\hat{m} = \frac{\ln 2}{\hat{\lambda}} = (\ln 2)\bar{X}
$$
Likewise, if a manufacturer wants to set a warranty based on the 95th percentile, $\theta_{0.95}$, we first solve $1 - \exp(-\lambda \theta_{0.95}) = 0.95$ to find $\theta_{0.95} = \ln(20)/\lambda$. The MLE is then [@problem_id:1925587]:
$$
\hat{\theta}_{0.95} = \frac{\ln 20}{\hat{\lambda}} = (\ln 20)\bar{X}
$$

### Generality of the Principle

The invariance property is not limited to parameters of single-parameter distributions or cases where the MLE is found via differentiation. Its generality is one of its most compelling features.

Consider experimental measurements $X_1, \ldots, X_n$ from a [normal distribution](@entry_id:137477) $N(\mu_0, \sigma^2)$ where the mean $\mu_0$ is a known constant but the variance $\sigma^2$ is unknown. The parameter of interest is $\sigma^2$. The MLE for the variance is $\hat{\sigma}^2 = \frac{1}{n}\sum_{i=1}^n (X_i - \mu_0)^2$. In many scientific contexts, the quality of an experiment is measured by its **precision**, defined as the reciprocal of the variance, $\tau = 1/\sigma^2$. By the invariance property, the MLE for the precision is immediately found [@problem_id:1925595]:
$$
\hat{\tau} = \frac{1}{\hat{\sigma}^2} = \frac{n}{\sum_{i=1}^n (X_i - \mu_0)^2}
$$

Furthermore, the principle holds even when the MLEs are not found by calculus. Let's analyze voltage signals from a process that are uniformly distributed on an unknown interval $[\theta_1, \theta_2]$. The [likelihood function](@entry_id:141927) is $L(\theta_1, \theta_2) = (\theta_2-\theta_1)^{-n}$ for $\theta_1 \le \min(X_i)$ and $\theta_2 \ge \max(X_i)$. To maximize this likelihood, we must make the interval length $\theta_2 - \theta_1$ as small as possible. This occurs when $\hat{\theta}_1 = X_{(1)}$ and $\hat{\theta}_2 = X_{(n)}$, where $X_{(1)}$ and $X_{(n)}$ are the sample minimum and maximum, respectively. Now, suppose we wish to estimate the central voltage, or midpoint of the interval, $\mu = (\theta_1 + \theta_2)/2$. The invariance property applies directly to this multi-parameter function [@problem_id:1925544]:
$$
\hat{\mu} = \frac{\hat{\theta}_1 + \hat{\theta}_2}{2} = \frac{X_{(1)} + X_{(n)}}{2}
$$

Finally, the property remains valid even for transformations that are not one-to-one. Consider a sample from a uniform distribution $U(0, \theta)$, where the [parameter space](@entry_id:178581) for $\theta$ is $(0, 4\pi]$. The MLE for $\theta$ is $\hat{\theta} = X_{(n)}$. Suppose we want to find the MLE for $\eta = \cos(\theta)$. The function $g(\theta) = \cos(\theta)$ is not invertible on the interval $(0, 4\pi]$. Nonetheless, the [invariance principle](@entry_id:170175) holds, and the MLE is found by substituting $\hat{\theta}$ into the function [@problem_id:1925577]:
$$
\hat{\eta} = \cos(\hat{\theta}) = \cos(X_{(n)})
$$
The value $\hat{\theta} = X_{(n)}$ represents the single most plausible value for the parameter $\theta$. The most plausible value for the transformed parameter $\eta$ is therefore the transformation of this most plausible $\theta$. Any other value of $\theta$ that yields the same cosine value must be larger than $X_{(n)}$ and would thus have a lower likelihood, confirming that $\cos(X_{(n)})$ maximizes the [profile likelihood](@entry_id:269700) for $\eta$. This demonstrates the profound robustness of the [invariance principle](@entry_id:170175).

In summary, the invariance property of maximum likelihood estimators is an indispensable tool in statistical practice. It provides a simple, yet powerful, mechanism for extending estimation from the natural parameters of a distribution to a vast array of other scientifically meaningful quantities, regardless of the complexity of the transformation or the method used to find the original MLE.