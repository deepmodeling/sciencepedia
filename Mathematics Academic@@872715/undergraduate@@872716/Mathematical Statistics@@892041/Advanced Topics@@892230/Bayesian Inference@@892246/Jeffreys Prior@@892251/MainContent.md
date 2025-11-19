## Introduction
In the framework of Bayesian statistics, the choice of a prior distribution is a fundamental and often debated step. This prior represents our state of knowledge about a parameter before observing any data. While expert knowledge can inform this choice, analysts often seek an "objective" prior that is constructed by a formal rule, allowing the data to drive the inference as much as possible. Simple choices, like a [uniform distribution](@entry_id:261734), fail to be truly objective because they are not consistent under changes of [parameterization](@entry_id:265163). The Jeffreys prior, developed by Sir Harold Jeffreys, offers a principled and systematic solution to this problem, creating a prior based on the mathematical structure of the statistical model itself.

This article provides a comprehensive exploration of the Jeffreys prior, guiding you from its theoretical underpinnings to its practical applications. The first chapter, **"Principles and Mechanisms"**, delves into the core theory, defining the prior using Fisher information and demonstrating its hallmark property of [reparameterization invariance](@entry_id:267417). The second chapter, **"Applications and Interdisciplinary Connections"**, showcases the prior's utility across various scientific fields, from estimating simple proportions to characterizing complex systems in astrophysics and engineering. Finally, the **"Hands-On Practices"** section offers a set of targeted problems to help you develop the skills needed to derive and apply Jeffreys priors in your own work.

## Principles and Mechanisms

In the landscape of Bayesian inference, the selection of a prior distribution is a foundational step, embodying our state of knowledge before observing data. While informative priors are powerful when expert knowledge is available, there is often a need for an "objective" or "non-informative" prior—one that is constructed by a formal rule and is intended to let the data speak for itself as much as possible. A naive choice, such as a [uniform distribution](@entry_id:261734), proves inadequate as it is not invariant to [reparameterization](@entry_id:270587); a uniform prior on a parameter $\theta$ does not correspond to a uniform prior on, say, $\theta^2$. The Jeffreys prior, proposed by Sir Harold Jeffreys, provides a systematic solution to this challenge by deriving the prior directly from the structure of the [likelihood function](@entry_id:141927) itself.

### The Fisher Information and the Definition of Jeffreys Prior

The Jeffreys prior is fundamentally linked to the concept of **Fisher information**, a cornerstone of statistical theory that quantifies the amount of information a random variable carries about an unknown parameter. For a statistical model defined by a probability density or [mass function](@entry_id:158970) $p(x|\theta)$ with a single parameter $\theta$, the Fisher information, denoted $I(\theta)$, is defined as the negative expectation of the second derivative of the [log-likelihood function](@entry_id:168593):

$$
I(\theta) = -E\left[\frac{\partial^2}{\partial\theta^2} \ln p(X|\theta)\right]
$$

The expectation $E[\cdot]$ is taken with respect to the data distribution $p(x|\theta)$. Intuitively, $I(\theta)$ measures the curvature of the [log-likelihood function](@entry_id:168593). A high curvature (a sharply peaked likelihood) implies that the data provide substantial information for pinpointing the value of $\theta$, whereas a low curvature (a flat likelihood) suggests the data are less informative.

Jeffreys' rule defines the [prior distribution](@entry_id:141376) for $\theta$, $\pi_J(\theta)$, as being proportional to the square root of the Fisher information:

$$
\pi_J(\theta) \propto \sqrt{I(\theta)}
$$

This construction ensures that the prior assigns more density to regions of the [parameter space](@entry_id:178581) where the model is more "sensitive" to changes in the parameter, as measured by the Fisher information.

### Calculation of Jeffreys Priors for Common Models

Let us derive the Jeffreys prior for several standard statistical models to understand its form and behavior. The process in each case involves calculating the [log-likelihood](@entry_id:273783), its second derivative, the Fisher information, and finally the square root of the information.

#### Bernoulli Distribution

Consider a single Bernoulli trial with success probability $p \in (0, 1)$. The probability [mass function](@entry_id:158970) is $p(x|p) = p^x (1-p)^{1-x}$ for $x \in \{0, 1\}$. The [log-likelihood](@entry_id:273783) is $\ln p(x|p) = x \ln p + (1-x) \ln(1-p)$. The derivatives with respect to $p$ are:

$$
\frac{\partial}{\partial p} \ln p(x|p) = \frac{x}{p} - \frac{1-x}{1-p}
$$

$$
\frac{\partial^2}{\partial p^2} \ln p(x|p) = -\frac{x}{p^2} - \frac{1-x}{(1-p)^2}
$$

To find the Fisher information, we take the negative expectation, noting that $E[X] = p$:

$$
I(p) = -E\left[-\frac{X}{p^2} - \frac{1-X}{(1-p)^2}\right] = \frac{E[X]}{p^2} + \frac{1-E[X]}{(1-p)^2} = \frac{p}{p^2} + \frac{1-p}{(1-p)^2} = \frac{1}{p} + \frac{1}{1-p} = \frac{1}{p(1-p)}
$$

The Jeffreys prior for $p$ is therefore:

$$
\pi_J(p) \propto \sqrt{I(p)} = \frac{1}{\sqrt{p(1-p)}} = p^{-1/2}(1-p)^{-1/2}
$$

This functional form is that of a Beta distribution, specifically $\text{Beta}(\frac{1}{2}, \frac{1}{2})$. This prior, also known as the arcsine distribution, is notably different from a uniform $\text{Beta}(1, 1)$ prior. It places more prior mass near the boundaries (0 and 1), reflecting a belief that the event is either very rare or very common [@problem_id:1379701].

#### Poisson Distribution

For a single observation $k$ from a Poisson distribution with rate parameter $\lambda > 0$, the probability [mass function](@entry_id:158970) is $P(k;\lambda) = \frac{\lambda^k e^{-\lambda}}{k!}$. The log-likelihood is $\ln P(k;\lambda) = k \ln \lambda - \lambda - \ln k!$. The derivatives are:

$$
\frac{\partial}{\partial\lambda} \ln P(k;\lambda) = \frac{k}{\lambda} - 1
$$

$$
\frac{\partial^2}{\partial\lambda^2} \ln P(k;\lambda) = -\frac{k}{\lambda^2}
$$

Taking the negative expectation, with $E[k] = \lambda$, gives the Fisher information:

$$
I(\lambda) = -E\left[-\frac{k}{\lambda^2}\right] = \frac{E[k]}{\lambda^2} = \frac{\lambda}{\lambda^2} = \frac{1}{\lambda}
$$

The resulting Jeffreys prior for the Poisson rate is:

$$
\pi_J(\lambda) \propto \sqrt{I(\lambda)} = \sqrt{\frac{1}{\lambda}} = \lambda^{-1/2}
$$

This is an improper prior, a concept we will return to later [@problem_id:815072].

### The Hallmark Property: Reparameterization Invariance

The primary motivation for the Jeffreys prior is its **invariance under [reparameterization](@entry_id:270587)**. This means that the [statistical inference](@entry_id:172747) drawn from a Bayesian analysis should not depend on the specific mathematical form chosen for the parameter. For example, modeling a physical process using a [rate parameter](@entry_id:265473) $\lambda$ or its inverse, the [mean lifetime](@entry_id:273413) $\tau = 1/\lambda$, should lead to equivalent conclusions.

Let $\phi = g(\theta)$ be a one-to-one [reparameterization](@entry_id:270587). The standard rule for transforming a probability density function states that $\pi(\phi) = \pi(\theta(\phi)) \left|\frac{d\theta}{d\phi}\right|$. Jeffreys' construction is designed to obey this transformation rule automatically. The Fisher information itself transforms as $I(\phi) = I(\theta) \left(\frac{d\theta}{d\phi}\right)^2$. Consequently, the Jeffreys prior for $\phi$ is:

$$
\pi_J(\phi) \propto \sqrt{I(\phi)} = \sqrt{I(\theta) \left(\frac{d\theta}{d\phi}\right)^2} = \sqrt{I(\theta)} \left|\frac{d\theta}{d\phi}\right| \propto \pi_J(\theta) \left|\frac{d\theta}{d\phi}\right|
$$

This demonstrates that the prior derived for $\phi$ is precisely the prior for $\theta$ transformed to the $\phi$ scale.

Let's illustrate this with the [exponential distribution](@entry_id:273894), which models phenomena like [radioactive decay](@entry_id:142155) or component failure times [@problem_id:1925889]. The PDF can be parameterized by the rate $\lambda$ or the mean lifetime $\tau = 1/\lambda$.

1.  **Parameterization by Rate $\lambda$:** The PDF is $f(t;\lambda) = \lambda e^{-\lambda t}$. Following a similar calculation as for the Poisson distribution, the Fisher information is $I(\lambda) = 1/\lambda^2$. Thus, the Jeffreys prior is $\pi_J(\lambda) \propto \sqrt{1/\lambda^2} = 1/\lambda$ [@problem_id:1624948].

2.  **Parameterization by Mean $\tau$:** The PDF is $f(t;\tau) = \frac{1}{\tau} e^{-t/\tau}$. The log-likelihood is $\ln f(t;\tau) = -\ln\tau - t/\tau$. The second derivative is $\frac{\partial^2}{\partial\tau^2} \ln f(t;\tau) = \frac{1}{\tau^2} - \frac{2t}{\tau^3}$. Taking the negative expectation with $E[t] = \tau$ gives the Fisher information:
    $$
    I(\tau) = -E\left[\frac{1}{\tau^2} - \frac{2t}{\tau^3}\right] = -\left(\frac{1}{\tau^2} - \frac{2\tau}{\tau^3}\right) = \frac{1}{\tau^2}
    $$
    The Jeffreys prior is therefore $\pi_J(\tau) \propto \sqrt{1/\tau^2} = 1/\tau$ [@problem_id:1925871].

The two results, $\pi_J(\lambda) \propto 1/\lambda$ and $\pi_J(\tau) \propto 1/\tau$, are perfectly consistent under the transformation $\tau = 1/\lambda$, confirming the [reparameterization invariance](@entry_id:267417).

### Generalizations for Location and Scale Families

The behavior of Jeffreys prior can be generalized for entire families of distributions.

#### Location Parameters

A **location family** has a PDF of the form $p(x|\theta) = f(x-\theta)$, where $\theta$ shifts the distribution along the real axis without changing its shape. A canonical example is the mean $\mu$ of a normal distribution with known variance $\sigma^2$ [@problem_id:1925902]. It can be shown that for any such family, the Fisher information $I(\theta)$ is a constant that does not depend on $\theta$ [@problem_id:1925905].
As a result, the Jeffreys prior for a pure [location parameter](@entry_id:176482) is always uniform:

$$
\pi_J(\theta) \propto \sqrt{I(\theta)} \propto 1
$$

For the normal mean $\mu$ with known variance $\sigma^2$, the Fisher information is $I(\mu) = 1/\sigma^2$, which is constant with respect to $\mu$. The Jeffreys prior is thus $\pi_J(\mu) \propto \sqrt{1/\sigma^2} = 1/\sigma \propto 1$ [@problem_id:1925902]. This flat prior formalizes the notion of being "ignorant" about the location of the parameter.

#### Scale Parameters

A **scale family** has a PDF of the form $p(x|\sigma) = \frac{1}{\sigma}f(x/\sigma)$ for $\sigma > 0$, where $\sigma$ stretches or compresses the distribution. For any such family, the Fisher information can be shown to be $I(\sigma) \propto 1/\sigma^2$ [@problem_id:1925891].
The Jeffreys prior for a pure [scale parameter](@entry_id:268705) is therefore:

$$
\pi_J(\sigma) \propto \sqrt{I(\sigma)} \propto \frac{1}{\sigma}
$$

This is often called the log-uniform prior, as it corresponds to a uniform prior on $\ln(\sigma)$. This prior expresses ignorance about the magnitude (order of magnitude) of the scale. The exponential mean $\tau$ is an example of a scale parameter, and its prior $\pi_J(\tau) \propto 1/\tau$ fits this rule [@problem_id:1925891]. Similarly, for a [normal distribution](@entry_id:137477) with known mean $\mu$, the variance $\theta = \sigma^2$ acts as a scale-related parameter. Its Jeffreys prior is $\pi_J(\sigma^2) \propto 1/\sigma^2$ [@problem_id:1925894].

### Practical Considerations and Advanced Topics

While elegant, the application of Jeffreys prior involves important subtleties.

#### Improper Priors and Proper Posteriors

Many Jeffreys priors, such as the uniform prior for a [location parameter](@entry_id:176482) ($\pi(\mu) \propto 1$) or the scale prior ($\pi(\sigma) \propto 1/\sigma$), are **improper**. This means they do not integrate to a finite value over their domain and are not, strictly speaking, probability distributions. For instance, $\int_{-\infty}^{\infty} 1 \, d\mu = \infty$.

While this may seem problematic, such priors can often be used in Bayes' theorem without issue. If the data are sufficiently informative, the resulting posterior distribution can be **proper**, meaning it integrates to one and is a valid probability distribution. For example, combining the improper prior $\pi(\mu) \propto 1$ with a single observation $x$ from a normal likelihood $N(x|\mu, \sigma^2)$ results in a [posterior distribution](@entry_id:145605) for $\mu$ that is a proper [normal distribution](@entry_id:137477), $N(\mu|x, \sigma^2)$ [@problem_id:1925868]. The condition for a proper posterior is that the marginal likelihood, $\int p(x|\theta)\pi(\theta)d\theta$, must be finite.

#### Multiparameter Models and the Jeffreys-Lindley Paradox

The Jeffreys rule has generalizations to multiparameter models, but its application is not always straightforward and can lead to priors with undesirable properties. For a model with parameters $(\mu, \sigma)$, the multivariate Jeffreys prior is $\pi_J(\mu, \sigma) \propto \sqrt{\det I(\mu, \sigma)}$, where $I(\mu, \sigma)$ is the Fisher [information matrix](@entry_id:750640). For the normal distribution, this yields $\pi_J(\mu, \sigma) \propto 1/\sigma^2$. However, the commonly used "[reference prior](@entry_id:171432)" for this problem, derived from a more sophisticated algorithm, is $\pi_R(\mu, \sigma) \propto 1/\sigma$ [@problem_id:1925853]. This latter prior is often preferred as it leads to better frequentist properties of the resulting Bayesian procedures. This discrepancy highlights that Jeffreys' original rule can be problematic in multiparameter settings, motivating the development of modern [objective priors](@entry_id:167984) like reference priors.

Furthermore, [improper priors](@entry_id:166066) like Jeffreys priors are particularly problematic for Bayesian hypothesis testing, especially when testing a point [null hypothesis](@entry_id:265441) (e.g., $H_0: \theta = \theta_0$) against a composite alternative ($H_1: \theta \neq \theta_0$). This issue is famously known as the **Jeffreys-Lindley paradox**. The paradox demonstrates that for a fixed level of "marginal" frequentist significance (e.g., a [z-score](@entry_id:261705) of 2), as the sample size $n$ grows, the Bayes factor can provide overwhelming evidence in favor of the null hypothesis. This occurs because the improper prior for $\theta$ under $H_1$ spreads its mass over an infinitely large space, penalizing $H_1$ so severely that even strong evidence in the data cannot overcome it. In a typical scenario comparing $H_0: \mu = 0$ vs $H_1: \mu \neq 0$ for a normal mean, the Bayes factor in favor of $H_0$ can be shown to grow proportionally to $\sqrt{n}$ for a fixed, significant [z-score](@entry_id:261705), leading to the counterintuitive conclusion that more data leads to more support for the null [@problem_id:1925849]. This paradox serves as a critical warning: Jeffreys priors are generally suitable for [parameter estimation](@entry_id:139349) but should not be naively used for comparing models or testing sharp null hypotheses.