## Introduction
Likelihood-based inference and Maximum Likelihood Estimation (MLE) represent a cornerstone of modern statistics, providing a powerful and versatile framework for modeling data across scientific disciplines. In data-intensive fields like bioinformatics and medical data analytics, these principles are not just theoretical constructs but the engines driving discovery, from calling genetic variants to modeling disease progression. The core idea is elegantly simple: to select model parameters that make our observed data the most probable. However, applying this principle to real-world biological and medical data introduces significant challenges, including incomplete observations, unobserved latent structures, and the "curse of dimensionality" where predictors outnumber samples.

This article provides a comprehensive exploration of the likelihood framework, designed to bridge theory and practice. We will begin by establishing the mathematical foundations, then demonstrate how these concepts are applied and extended to solve complex analytical problems. The section on **"Principles and Mechanisms,"** will dissect the [likelihood function](@entry_id:141927), the mechanics of MLE, and the key theoretical results that guarantee its desirable properties. The section on **"Applications and Interdisciplinary Connections,"** will illustrate the framework's power in diverse contexts, including genomics, survival analysis, and its crucial interfaces with Bayesian and causal inference. Finally, the **"Hands-On Practices"** section will offer opportunities to implement these methods, cementing a practical understanding of the theory. We begin our journey by defining the likelihood function and exploring its fundamental properties.

## Principles and Mechanisms

### The Likelihood Function: Definition and Core Principles

At the heart of likelihood-based inference lies the **[likelihood function](@entry_id:141927)**, a concept that, while derived from the [joint probability distribution](@entry_id:264835) of the data, serves a fundamentally different purpose. Given a set of independent and identically distributed (i.i.d.) observations $x_{1:n} = (x_1, \dots, x_n)$ drawn from a parametric probability distribution with density or mass function $f(x; \theta)$, the [joint probability](@entry_id:266356) of observing this specific dataset is given by the product of the individual probabilities:

$$ p(x_{1:n} \mid \theta) = \prod_{i=1}^{n} f(x_i; \theta) $$

This joint density is a function of the data $x_{1:n}$ for a fixed value of the parameter $\theta$. It describes the probability of various data outcomes given a known data-generating process.

The likelihood function, denoted $L(\theta \mid x_{1:n})$, flips this perspective. Once the data have been observed and are now fixed, the likelihood function is the same mathematical expression but viewed as a function of the parameter $\theta$.

$$ L(\theta \mid x_{1:n}) = \prod_{i=1}^{n} f(x_i; \theta) $$

Thus, the crucial distinction lies in what is held fixed and what varies: the joint density is a function on the [sample space](@entry_id:270284), $x_{1:n} \mapsto p(x_{1:n} \mid \theta)$, while the likelihood is a function on the parameter space, $\theta \mapsto L(\theta \mid x_{1:n})$ [@problem_id:4578125]. This function quantifies the plausibility of different parameter values in light of the observed data.

It is critical to understand that the likelihood function is **not a probability distribution for the parameter $\theta$**. In the frequentist paradigm, the parameter $\theta$ is considered a fixed, unknown constant, not a random variable. Therefore, it cannot have a probability distribution. A formal reason the likelihood is not a probability density is that it does not, in general, integrate to one over the parameter space $\Theta$.

Consider a simple but illustrative example from medical genomics: assaying for a single nucleotide variant (SNV) across $n$ independent reads, where each read is a Bernoulli trial with success probability $p$ [@problem_id:4578016]. The probability [mass function](@entry_id:158970) for a single observation $x_i \in \{0, 1\}$ is $f(x_i; p) = p^{x_i}(1-p)^{1-x_i}$. For an observed sequence of $n$ reads, the [likelihood function](@entry_id:141927) is:

$$ L(p \mid x_{1:n}) = \prod_{i=1}^{n} p^{x_i}(1-p)^{1-x_i} = p^k (1-p)^{n-k} $$

where $k = \sum x_i$ is the total number of reads supporting the variant. If we were to integrate this function over the parameter space $p \in [0, 1]$, we would obtain:

$$ \int_0^1 p^k (1-p)^{n-k} \,dp = B(k+1, n-k+1) = \frac{k!(n-k)!}{(n+1)!} $$

where $B(\cdot, \cdot)$ is the Beta function. This value is clearly not equal to 1 in general (unless $n=0$), demonstrating that $L(p)$ is not a valid probability density function for $p$. Normalization of the underlying probability model occurs over the data space ($\sum_{x \in \{0,1\}^n} p(x \mid p) = 1$), not the parameter space [@problem_id:4578016].

A central tenet of likelihood-based inference is the **principle of proportionality**. The likelihood function is defined only up to a strictly positive multiplicative constant. This means that for [parameter estimation](@entry_id:139349) *within a single model*, any factors in the likelihood expression that do not depend on the parameter $\theta$ can be dropped without affecting the inference. This is because the value of $\theta$ that maximizes $L(\theta)$ will also maximize $c(x) \cdot L(\theta)$ for any $c(x) > 0$.

For instance, in a bioinformatics model where read counts $X_i$ follow a Poisson distribution with rate $s_i \lambda$, with known library-size offsets $s_i$, the [joint probability mass function](@entry_id:184238) is $\prod_{i=1}^n \frac{(s_i \lambda)^{x_i} \exp(-s_i \lambda)}{x_i!}$. We can rewrite this as:

$$ L(\lambda \mid x_{1:n}) = \left( \prod_{i=1}^n \frac{s_i^{x_i}}{x_i!} \right) \left( \lambda^{\sum x_i} \exp(-\lambda \sum s_i) \right) $$

For the purpose of finding the $\lambda$ that maximizes this function, the entire first term, $\prod_{i=1}^n \frac{s_i^{x_i}}{x_i!}$, can be discarded as it does not depend on $\lambda$ [@problem_id:4578125]. We can work with a simpler, proportional likelihood $L_{prop}(\lambda) \propto \lambda^{\sum x_i} \exp(-\lambda \sum s_i)$.

However, this convenience does not extend to **[model comparison](@entry_id:266577)**. When comparing different statistical models using criteria like the Akaike Information Criterion (AIC) or [likelihood ratio](@entry_id:170863) tests, the absolute value of the maximized likelihood $\hat{L}$ is crucial. Dropping model-dependent constants can lead to erroneous conclusions [@problem_id:4578125].

Another key property is the **invariance of likelihood to [reparameterization](@entry_id:270587)**. If we define a new parameter $\phi = g(\theta)$ through a [one-to-one transformation](@entry_id:148028), the likelihood function in terms of $\phi$ is simply $L_{\phi}(\phi) = L_{\theta}(g^{-1}(\phi))$. Unlike probability density functions, no Jacobian determinant is required for this transformation. This is a profound and useful property, as it ensures that the maximum likelihood estimate (MLE) is also invariant: $\hat{\phi} = g(\hat{\theta})$ [@problem_id:4578125].

Finally, special care must be taken when the **support of the distribution depends on the parameter**. In such cases, the [indicator functions](@entry_id:186820) that define the support cannot be dropped. For example, if data are drawn from a Uniform$[0, \theta]$ distribution, the joint density is $\theta^{-n} \prod_{i=1}^n \mathbf{1}\{0 \le x_i \le \theta\}$. This can be written as $L(\theta) = \theta^{-n} \mathbf{1}\{\theta \ge x_{(n)}\}$, where $x_{(n)}$ is the maximum observed data point. The indicator term $\mathbf{1}\{\theta \ge x_{(n)}\}$ is a function of $\theta$ and is essential for correct inference; dropping it would lead to the nonsensical conclusion that the likelihood is maximized at $\theta \to 0$ [@problem_id:4578125].

### Identifiability: A Precondition for Meaningful Inference

Before proceeding with estimation, a fundamental property of the parametric model must be verified: **identifiability**. A model is identifiable if distinct parameter values correspond to distinct probability distributions. Formally, the mapping $\theta \mapsto P_{\theta}$ must be injective, meaning that if $P_{\theta_1} = P_{\theta_2}$, then it must be that $\theta_1 = \theta_2$ [@problem_id:4578019].

If a model is not identifiable, then there exist at least two different parameter values, $\theta_1 \neq \theta_2$, that generate the exact same probability distribution for the data. Consequently, for any dataset, the likelihood function will have the same value at these two points: $L(\theta_1 \mid x_{1:n}) = L(\theta_2 \mid x_{1:n})$. This creates an ambiguity that makes it impossible to uniquely determine the parameter from the data, as the likelihood surface will possess multiple, equivalent maxima.

A classic example of non-[identifiability](@entry_id:194150) in bioinformatics arises in mixture models, such as the deconvolution of cell-free DNA fragment lengths. A two-component Gaussian mixture model has the density:

$$ f(x \mid \theta) = \pi \cdot \mathcal{N}(x \mid \mu_1, \sigma_1^2) + (1-\pi) \cdot \mathcal{N}(x \mid \mu_2, \sigma_2^2) $$

Here, the parameter vector is $\theta = (\pi, \mu_1, \sigma_1, \mu_2, \sigma_2)$. Consider a second parameter vector $\theta' = (1-\pi, \mu_2, \sigma_2, \mu_1, \sigma_1)$, which corresponds to swapping the labels of the two components. Because addition is commutative, the density function remains unchanged: $f(x \mid \theta) = f(x \mid \theta')$. The model is therefore not identifiable. For any dataset, the likelihood function will be perfectly symmetric with respect to this label-swapping, and any maximum likelihood estimate $\hat{\theta}$ will be accompanied by an equally valid estimate $\hat{\theta}'$ [@problem_id:4578019].

There are two primary strategies to address non-[identifiability](@entry_id:194150):
1.  **Imposing Constraints**: We can restrict the parameter space to ensure a unique representation. For the mixture model, imposing an ordering constraint such as $\mu_1  \mu_2$ breaks the label symmetry and makes the parameterization identifiable on the constrained space.
2.  **Augmenting the Model**: If additional data are available that are informative about component membership, identifiability can be restored. For instance, if each DNA fragment carried a methylation tag with a different distribution for apoptotic versus necrotic origins, the [joint likelihood](@entry_id:750952) for fragment length and tag status could distinguish the components, breaking the symmetry [@problem_id:4578019].

### Maximum Likelihood Estimation (MLE)

The **principle of maximum likelihood** proposes a simple and intuitive method for estimating a parameter $\theta$: we select the parameter value that makes the observed data most probable, or "most likely." The **maximum likelihood estimate (MLE)**, denoted $\hat{\theta}$, is the value of $\theta$ that maximizes the likelihood function $L(\theta \mid x_{1:n})$.

$$ \hat{\theta} = \arg\max_{\theta \in \Theta} L(\theta \mid x_{1:n}) $$

In practice, it is almost always more convenient to work with the natural logarithm of the likelihood, known as the **[log-likelihood function](@entry_id:168593)**, $\ell(\theta) = \ln L(\theta \mid x_{1:n})$. Since the logarithm is a strictly [monotonic function](@entry_id:140815), maximizing $\ell(\theta)$ is equivalent to maximizing $L(\theta)$.

$$ \hat{\theta} = \arg\max_{\theta \in \Theta} \ell(\theta \mid x_{1:n}) $$

Working with the [log-likelihood](@entry_id:273783) offers two significant advantages. First, it converts the product of probabilities into a sum of log-probabilities, which is often analytically and computationally simpler.
$$ \ell(\theta) = \ln \left( \prod_{i=1}^{n} f(x_i; \theta) \right) = \sum_{i=1}^{n} \ln f(x_i; \theta) $$

Second, and more critically in modern data analytics, it provides profound numerical stability. The likelihood, being a product of many small probabilities, can easily **[underflow](@entry_id:635171)** in standard [floating-point arithmetic](@entry_id:146236), evaluating to zero even when it is not. This is a common problem in bioinformatics applications with large datasets. For example, in a study with $n=10^4$ patients, if the probability of an observed outcome for each patient is $0.5$, the total likelihood is $(0.5)^{10000} \approx 10^{-3010}$. This number is vastly smaller than the smallest positive number representable in standard double-precision arithmetic (approx. $10^{-324}$), causing a catastrophic [underflow](@entry_id:635171) to zero. The [log-likelihood](@entry_id:273783), however, remains a well-behaved, representable number: $\ell(\theta) = 10000 \times \ln(0.5) \approx -6931.47$. Computations and comparisons can proceed on the log scale without loss of precision [@problem_id:4578098].

To find the MLE, we typically use calculus, finding the point where the derivative of the log-likelihood function is zero. The first derivative of the [log-likelihood](@entry_id:273783) is a fundamentally important quantity known as the **[score function](@entry_id:164520)**, $U(\theta) = \frac{d}{d\theta} \ell(\theta)$. The MLE $\hat{\theta}$ is found by solving the **score equation**: $U(\hat{\theta}) = 0$. For a simple model like i.i.d. Poisson($\lambda$) observations, the log-likelihood is $\ell(\lambda) = (\sum x_i)\ln(\lambda) - n\lambda - \sum\ln(x_i!)$. The [score function](@entry_id:164520) is $U(\lambda) = \frac{\sum x_i}{\lambda} - n$. Setting this to zero immediately yields the familiar MLE: $\hat{\lambda} = \frac{1}{n}\sum x_i = \bar{x}$ [@problem_id:4578074].

### The Curvature of the Likelihood: Fisher Information

The MLE tells us the most plausible value of the parameter. However, it does not, by itself, tell us about the uncertainty of this estimate. This information is encoded in the *shape* of the [log-likelihood function](@entry_id:168593) around its maximum. A sharply peaked [log-likelihood](@entry_id:273783) indicates that the data are highly informative, and small deviations from $\hat{\theta}$ cause a large drop in likelihood. Conversely, a flat log-likelihood suggests that the data are not very informative, and a wide range of parameter values are nearly as plausible as the MLE.

The curvature of the log-likelihood function is formally quantified by the **Fisher information**. For a single parameter $\theta$, the Fisher information $I(\theta)$ can be defined in two equivalent ways, assuming certain regularity conditions:
1.  As the variance of the [score function](@entry_id:164520): $I(\theta) = \mathbb{E}[ (U(\theta))^2 ]$.
2.  As the negative expected value of the second derivative (Hessian) of the [log-likelihood](@entry_id:273783): $I(\theta) = -\mathbb{E}[ \frac{d^2}{d\theta^2} \ell(\theta) ]$.

For a sample of $n$ i.i.d. observations, the total Fisher information is simply $n$ times the information for a single observation.

Let's derive these quantities for the i.i.d. Poisson($\theta$) model, which is foundational for count-based data in genomics [@problem_id:4578085]. The [log-likelihood](@entry_id:273783) for a sample of size $n$ is $\ell(\theta) = (\sum x_i)\ln(\theta) - n\theta - \text{const}$.
The score function is $U(\theta) = \frac{\sum x_i}{\theta} - n$.
The second derivative is $\frac{d^2\ell}{d\theta^2} = -\frac{\sum x_i}{\theta^2}$.

The Fisher information for the sample of size $n$ is:
$$ I_n(\theta) = -\mathbb{E}\left[ \frac{d^2\ell}{d\theta^2} \right] = -\mathbb{E}\left[ -\frac{\sum X_i}{\theta^2} \right] = \frac{1}{\theta^2} \mathbb{E}\left[\sum X_i\right] $$
Since $\mathbb{E}[X_i] = \theta$ for each observation, $\mathbb{E}[\sum X_i] = n\theta$. Therefore,
$$ I_n(\theta) = \frac{n\theta}{\theta^2} = \frac{n}{\theta} $$
To verify the alternative definition, we compute the variance of the score:
$$ \operatorname{Var}(U(\theta)) = \operatorname{Var}\left(\frac{\sum X_i}{\theta} - n\right) = \frac{1}{\theta^2} \operatorname{Var}\left(\sum X_i\right) $$
Since the observations are independent, $\operatorname{Var}(\sum X_i) = \sum \operatorname{Var}(X_i)$. For a Poisson distribution, $\operatorname{Var}(X_i) = \theta$. Thus, $\operatorname{Var}(\sum X_i) = n\theta$.
$$ \operatorname{Var}(U(\theta)) = \frac{n\theta}{\theta^2} = \frac{n}{\theta} $$
The two definitions agree, confirming that $I_n(\theta) = n/\theta$. The information is inversely proportional to the rate $\theta$, indicating that we have more precision (higher information) for estimating smaller rates.

### Finding the Maximum: Numerical Optimization

For many realistic models in bioinformatics, especially those with multiple parameters, the score equation $U(\theta) = 0$ cannot be solved analytically. In these cases, we must resort to numerical [optimization algorithms](@entry_id:147840) to find the MLE.

A powerful and widely used second-order method is the **Newton-Raphson algorithm**. The core idea is to iteratively approximate the log-likelihood function with a quadratic function and jump to the maximum of that approximation. The update rule can be derived by taking a Taylor expansion of the [score function](@entry_id:164520) $S(\theta)$ (using scalar notation for simplicity) around the current estimate $\theta^{(t)}$:
$$ S(\theta) \approx S(\theta^{(t)}) + S'(\theta^{(t)})(\theta - \theta^{(t)}) $$
We want to find the next iterate $\theta^{(t+1)}$ where the score is zero. Setting $S(\theta^{(t+1)})=0$:
$$ 0 \approx S(\theta^{(t)}) + H(\theta^{(t)})(\theta^{(t+1)} - \theta^{(t)}) $$
where $H(\theta) = S'(\theta) = \ell''(\theta)$ is the Hessian (second derivative) of the log-likelihood. Solving for $\theta^{(t+1)}$ gives the update rule:
$$ \theta^{(t+1)} = \theta^{(t)} - [H(\theta^{(t)})]^{-1} S(\theta^{(t)}) $$
This method typically exhibits fast **quadratic convergence** near the maximum, provided the log-likelihood is sufficiently smooth and the Hessian is non-singular [@problem_id:4578102].

In some contexts, a closely related method called **Fisher scoring** is used. It replaces the (potentially noisy) observed Hessian $H(\theta^{(t)})$ with its stable expectation, the negative Fisher information $-I(\theta^{(t)})$. The update becomes:
$$ \theta^{(t+1)} = \theta^{(t)} + [I(\theta^{(t)})]^{-1} S(\theta^{(t)}) $$

These methods are particularly powerful in the context of **[generalized linear models](@entry_id:171019) (GLMs)**, which are ubiquitous in medical data analysis. For example, to model a binomial outcome like variant allele fraction, one might use a logit link function $p = \sigma(\eta) = 1/(1+\exp(-\eta))$ to map the unconstrained parameter $\eta \in \mathbb{R}$ to the probability $p \in (0,1)$. The Newton-Raphson update can be explicitly derived for $\eta$, providing a [robust optimization](@entry_id:163807) procedure [@problem_id:4578102].

### Properties of Maximum Likelihood Estimators

The widespread use of MLE is due to its excellent asymptotic properties, which hold under a set of "regularity conditions." These conditions essentially ensure the model is smooth and well-behaved.

1.  **Consistency**: As the sample size $n$ grows, the MLE $\hat{\theta}_n$ converges in probability to the true parameter value $\theta_0$. Intuitively, this means that with enough data, the MLE will be arbitrarily close to the true value. The proof of consistency relies on showing that the normalized log-likelihood $\frac{1}{n}\ell(\theta)$ converges to its expectation $\mathbb{E}_{\theta_0}[\ell(\theta;X)]$, and that this expected [log-likelihood](@entry_id:273783) is uniquely maximized at the true parameter $\theta_0$ [@problem_id:4578074].

2.  **Asymptotic Normality**: For large $n$, the distribution of the MLE is approximately normal, centered at the true value $\theta_0$, with a variance determined by the inverse of the Fisher information. Formally:
    $$ \sqrt{n}(\hat{\theta}_n - \theta_0) \xrightarrow{d} \mathcal{N}(0, I(\theta_0)^{-1}) $$
    where $I(\theta_0)$ is the Fisher information for a single observation. This powerful result connects the theoretical quantity of Fisher information directly to the practical precision of our estimator. A higher information content leads to a lower variance and thus a more precise estimate.

3.  **Asymptotic Efficiency**: The MLE is asymptotically efficient, meaning that it achieves the **Cramér-Rao lower bound**. This bound specifies the lowest possible variance for any [unbiased estimator](@entry_id:166722). In large samples, no other [unbiased estimator](@entry_id:166722) is more precise than the MLE.

A crucial tool for leveraging [asymptotic normality](@entry_id:168464) is the **Delta Method**. It allows us to find the [asymptotic distribution](@entry_id:272575) of a smooth function $g(\hat{\theta})$ of the MLE. If $\sqrt{n}(\hat{\theta} - \theta) \xrightarrow{d} \mathcal{N}(0, \sigma^2)$, then:
$$ \sqrt{n}(g(\hat{\theta}) - g(\theta)) \xrightarrow{d} \mathcal{N}(0, [g'(\theta)]^2 \sigma^2) $$
This is extremely useful. For example, in [single-cell transcriptomics](@entry_id:274799), we might model UMI counts with a Poisson($\lambda$) distribution. The MLE is $\hat{\lambda}=\bar{X}$, and its [asymptotic variance](@entry_id:269933) is $I(\lambda)^{-1} = \lambda$. If we are interested in the log-transformed rate, $g(\lambda) = \ln(\lambda)$, which is often used for variance stabilization, the [delta method](@entry_id:276272) tells us its [asymptotic variance](@entry_id:269933). With $g'(\lambda) = 1/\lambda$, the [asymptotic variance](@entry_id:269933) of $\ln(\hat{\lambda})$ is $[g'(\lambda)]^2 \cdot \lambda = (1/\lambda)^2 \cdot \lambda = 1/\lambda$ [@problem_id:4578136].

### Likelihood-Based Inference in Practice

The principles of likelihood can be directly applied to the core tasks of [statistical inference](@entry_id:172747): hypothesis testing and [interval estimation](@entry_id:177880).

#### Handling Nuisance Parameters: The Profile Likelihood

In many realistic models, the parameter vector $\theta$ contains both parameters of scientific interest, $\psi$, and **[nuisance parameters](@entry_id:171802)**, $\lambda$, which are necessary for a realistic model but are not of direct interest. A powerful strategy for inference on $\psi$ in the presence of $\lambda$ is the **[profile likelihood](@entry_id:269700)**.

The [profile likelihood](@entry_id:269700) for $\psi$, denoted $L_p(\psi)$, is obtained by maximizing the full [likelihood function](@entry_id:141927) over the nuisance parameters $\lambda$ for each fixed value of $\psi$.
$$ L_p(\psi) = \max_{\lambda} L(\psi, \lambda) = L(\psi, \hat{\lambda}(\psi)) $$
where $\hat{\lambda}(\psi)$ is the MLE of $\lambda$ given a fixed $\psi$. The resulting function $L_p(\psi)$ depends only on the parameter of interest $\psi$ and can be treated much like an ordinary [likelihood function](@entry_id:141927) for inferential purposes. For instance, in a model of log-transformed gene expression as $\mathcal{N}(\mu, \sigma^2)$, if our interest is in the mean expression level $\mu$, then $\sigma^2$ is a [nuisance parameter](@entry_id:752755). The [profile likelihood](@entry_id:269700) for $\mu$ can be derived by maximizing the normal likelihood over $\sigma^2$ for each fixed $\mu$, which yields $\hat{\sigma}^2(\mu) = \frac{1}{n}\sum(x_i-\mu)^2$. Plugging this back into the likelihood gives a function purely of $\mu$ [@problem_id:4578070].

#### Likelihood Ratio Tests and Confidence Intervals

A general method for hypothesis testing is the **likelihood ratio (LR) test**. To test a null hypothesis $H_0: \theta \in \Theta_0$ against an alternative $H_A: \theta \in \Theta$, we compare the maximized likelihood under the null hypothesis, $L(\hat{\theta}_0)$, with the globally maximized likelihood, $L(\hat{\theta})$. The LR statistic is:
$$ W = -2 \ln \left( \frac{L(\hat{\theta}_0)}{L(\hat{\theta})} \right) = 2(\ell(\hat{\theta}) - \ell(\hat{\theta}_0)) $$
A cornerstone of likelihood theory is **Wilks' Theorem**, which states that under the null hypothesis, the distribution of the LR statistic $W$ is asymptotically a chi-square ($\chi^2$) distribution. The degrees of freedom are equal to the difference in the number of free parameters between the full and null models.

This theorem provides a direct path to constructing [confidence intervals](@entry_id:142297). A $(1-\alpha)$ confidence interval for a single parameter $\theta$ can be formed by "inverting" the LR test. The interval is the set of all parameter values $\theta_0$ for which the null hypothesis $H_0: \theta = \theta_0$ would *not* be rejected at significance level $\alpha$. This corresponds to the set of $\theta$ values whose log-likelihood is "close" to the maximum:
$$ \{ \theta : 2(\ell(\hat{\theta}) - \ell(\theta)) \le \chi^2_{1, 1-\alpha} \} $$
where $\chi^2_{1, 1-\alpha}$ is the $(1-\alpha)$ quantile of the $\chi^2$ distribution with one degree of freedom (approximately 3.84 for a 95% interval). The endpoints of the interval are the two solutions to the equation $2(\ell(\hat{\theta}) - \ell(\theta)) = \chi^2_{1, 1-\alpha}$. This method is broadly applicable, for instance, in finding an interval for a binomial proportion from sequencing data, and it relies only on the shape of the likelihood function itself [@problem_id:4578130]. This powerful approach can be extended to multiparameter models by using the profile log-likelihood in place of the ordinary log-likelihood [@problem_id:4578070].