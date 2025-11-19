## Introduction
In Bayesian statistics, the posterior distribution contains all our knowledge about a parameter after observing data. However, for reporting, decision-making, or practical application, we often need to distill this entire distribution into a single, representative number—a **[point estimate](@entry_id:176325)**. But how should we choose this single value? Is there a "best" summary? This article addresses this fundamental question by exploring the three most common Bayesian [point estimators](@entry_id:171246): the posterior mean, median, and mode. We will show that the choice is not arbitrary but is a principled decision rooted in both the shape of the posterior and the real-world consequences of estimation error.

This article will guide you through the theory and practice of these essential statistical summaries. In **Principles and Mechanisms**, we will define the [posterior mean](@entry_id:173826), median, and mode, explore their mathematical properties, and uncover their deep connection to Bayesian decision theory and [loss functions](@entry_id:634569). Following that, **Applications and Interdisciplinary Connections** will demonstrate how these estimators are used to solve tangible problems in fields ranging from engineering and physics to biology and finance. Finally, **Hands-On Practices** will offer a chance to apply these concepts to practical exercises, solidifying your understanding of how to calculate and interpret these crucial components of Bayesian analysis.

## Principles and Mechanisms

Following a Bayesian analysis, the complete inference about a parameter $\theta$ is encapsulated in its posterior distribution, $p(\theta | \text{data})$. This distribution represents our full state of updated knowledge. However, for communication, decision-making, or further calculation, it is often necessary to summarize this distribution with a single representative value, known as a **[point estimate](@entry_id:176325)**. The most common and principled [point estimates](@entry_id:753543) are derived from the [posterior distribution](@entry_id:145605)'s [measures of central tendency](@entry_id:168414): its **mean**, **median**, and **mode**. Each of these summaries has a distinct statistical interpretation and arises from different theoretical motivations, which we will explore in this chapter. The choice between them is not arbitrary; it is a principled decision that depends on the geometry of the [posterior distribution](@entry_id:145605) and the specific goals of the analysis.

### The Posterior Mode: The Most Probable Value

The **[posterior mode](@entry_id:174279)** is the value of the parameter $\theta$ that maximizes the [posterior probability](@entry_id:153467) density (or mass) function. It represents the single most probable value of the parameter, given the prior beliefs and the observed data. For this reason, it is also known as the **Maximum a Posteriori (MAP)** estimate.

For a continuous parameter $\theta$ with a differentiable posterior density $p(\theta | \text{data})$, the mode, $\theta_{\text{MAP}}$, can typically be found by solving the equation:
$$
\frac{d}{d\theta} p(\theta | \text{data}) = 0
$$
In practice, it is often mathematically simpler to work with the natural logarithm of the posterior, as the logarithm is a monotonically increasing function and will therefore have its maximum at the same value of $\theta$. This involves solving:
$$
\frac{d}{d\theta} \ln(p(\theta | \text{data})) = 0
$$

A classic application of this principle arises in the Beta-Binomial conjugate model. Suppose a quality control engineer is monitoring a semiconductor production line and wishes to estimate the defect rate, $\theta$ [@problem_id:1945461]. The number of defects, $k$, in a batch of size $n$ follows a Binomial likelihood, $L(\theta | k) \propto \theta^k (1-\theta)^{n-k}$. If the engineer's prior belief about $\theta$ is captured by a Beta distribution, $\theta \sim \text{Beta}(a, b)$, with density $p(\theta) \propto \theta^{a-1} (1-\theta)^{b-1}$, the resulting [posterior distribution](@entry_id:145605) is also a Beta distribution, $\theta | k, n \sim \text{Beta}(a+k, b+n-k)$. To find the [posterior mode](@entry_id:174279), we maximize the posterior density kernel, $\theta^{a+k-1}(1-\theta)^{b+n-k-1}$. Taking the logarithm gives $\ell(\theta) = (a+k-1)\ln(\theta) + (b+n-k-1)\ln(1-\theta)$. Differentiating with respect to $\theta$ and setting to zero yields:
$$
\frac{d\ell}{d\theta} = \frac{a+k-1}{\theta} - \frac{b+n-k-1}{1-\theta} = 0
$$
Solving for $\theta$ gives the [posterior mode](@entry_id:174279), provided the parameters are greater than 1:
$$
\theta_{\text{MAP}} = \frac{a+k-1}{a+b+n-2}
$$
This result provides the single most likely value for the defect rate based on the combined information from the prior and the experimental data.

This same principle of maximization applies to other parameters and models. For instance, when estimating the variance, $\sigma^2$, of a zero-mean Normal process using a conjugate Inverse-Gamma prior, $\sigma^2 \sim \text{IG}(\alpha, \beta)$, the posterior for $\sigma^2$ is also an Inverse-Gamma distribution [@problem_id:1945454]. The posterior parameters become $\alpha_{\text{post}} = \alpha + \frac{n}{2}$ and $\beta_{\text{post}} = \beta + \frac{1}{2}\sum x_i^2$. By maximizing the log of the posterior Inverse-Gamma density, we find the [posterior mode](@entry_id:174279) for the variance to be:
$$
\sigma^2_{\text{mode}} = \frac{\beta_{\text{post}}}{\alpha_{\text{post}} + 1} = \frac{\beta + \frac{1}{2}\sum_{i=1}^n x_i^2}{\alpha + \frac{n}{2} + 1}
$$
The [posterior mode](@entry_id:174279) is an intuitive and often easily calculated summary. However, it only reflects the peak of the distribution and can be a misleading summary if the distribution is highly skewed or multimodal.

### The Posterior Mean: The Center of Mass

The **posterior mean** is the expected value of the parameter with respect to the posterior distribution. It is calculated by integrating the parameter over its entire range, weighted by the [posterior probability](@entry_id:153467) density:
$$
E[\theta | \text{data}] = \int \theta \, p(\theta | \text{data}) \, d\theta
$$
Conceptually, the posterior mean represents the "center of mass" of the posterior distribution. It balances the probability density across its domain, and unlike the mode, it is sensitive to the entire shape of the distribution, including its tails.

For many standard conjugate models, the posterior mean has a simple analytical form. In the Beta-Binomial model, where the posterior is $\text{Beta}(a+k, b+n-k)$, the [posterior mean](@entry_id:173826) is:
$$
E[p | k, n] = \frac{a+k}{a+b+n}
$$
This formula has an elegant interpretation. It can be seen as a weighted average of the prior mean, $\frac{a}{a+b}$, and the [sample proportion](@entry_id:264484), $\frac{k}{n}$. The posterior mean for a proportion $p$ under a Jeffreys prior, $\text{Beta}(\frac{1}{2}, \frac{1}{2})$, after observing $k$ successes in $n$ trials, is a good example. The posterior is $\text{Beta}(k+\frac{1}{2}, n-k+\frac{1}{2})$, and its mean is $E[p|k,n] = \frac{k+1/2}{n+1}$ [@problem_id:1945470].

A powerful feature of the [posterior mean](@entry_id:173826) is its behavior as the amount of data increases. As the number of trials $n$ goes to infinity, the influence of the fixed prior parameters $(\alpha, \beta)$ diminishes relative to the data $(k, n)$. The posterior mean converges to the [sample proportion](@entry_id:264484) $\hat{p} = k/n$ [@problem_id:1945451]. Specifically:
$$
\lim_{n \to \infty} E[p | k, n] = \lim_{n \to \infty} \frac{\alpha+k}{\alpha+\beta+n} = \lim_{n \to \infty} \frac{\alpha/n + k/n}{\alpha/n + \beta/n + 1} = \hat{p}
$$
This property, often called Bayesian consistency, ensures that with enough data, the inference is driven by the evidence rather than the initial prior belief. A similar phenomenon occurs in the Normal-Normal model for a mean $\mu$. If we use a very diffuse or "non-informative" prior by letting its variance $\tau^2 \to \infty$, the [posterior mean](@entry_id:173826) converges to the [sample mean](@entry_id:169249) $\bar{x}$ [@problem_id:1945418]. This demonstrates that in the absence of strong [prior information](@entry_id:753750), Bayesian methods can produce results that align with classical frequentist estimators.

### The Posterior Median: The Central Partition

The **[posterior median](@entry_id:174652)** is the value $m$ that divides the posterior distribution into two regions of equal probability. It is the 50th percentile of the distribution, satisfying the condition:
$$
P(\theta \le m | \text{data}) = \int_{-\infty}^{m} p(\theta | \text{data}) \, d\theta = 0.5
$$
Unlike the mean, which can be heavily influenced by [outliers](@entry_id:172866) or long tails in a [skewed distribution](@entry_id:175811), the median is a more **robust** measure of central tendency. It is determined purely by the location where probability mass is centered, not by the values the parameter takes in the tails.

Calculating the median requires finding the posterior [cumulative distribution function](@entry_id:143135) (CDF), $F(\theta | \text{data})$, and solving the equation $F(m) = 0.5$. While this can be computationally intensive for complex posteriors, it is straightforward in some simple cases. Consider an engineer testing a biosensor with an unknown success probability $p$, assuming a uniform prior, $p \sim \text{Uniform}(0,1)$, which is equivalent to a $\text{Beta}(1,1)$ distribution [@problem_id:1945428]. After observing a single success, the likelihood is $L(p) = p$, and the posterior becomes $p | \text{success} \sim \text{Beta}(2,1)$. The posterior density is $p(p|\text{success}) = 2p$ for $p \in [0,1]$. The posterior CDF is $F(m) = \int_0^m 2t \, dt = m^2$. Setting this to 0.5 gives:
$$
m^2 = 0.5 \quad \implies \quad m = \frac{1}{\sqrt{2}}
$$
This is the value of $p$ for which we believe it is equally likely that the true value is higher or lower.

### A Principled Choice: Decision Theory and Loss Functions

The choice between the posterior mean, median, and mode is not merely a matter of preference. It can be formalized within the framework of **Bayesian decision theory**. This framework posits that for any given estimation problem, there is a **[loss function](@entry_id:136784)**, $L(\theta, \hat{\theta})$, that quantifies the penalty or "cost" of estimating the true parameter value $\theta$ with an estimate $\hat{\theta}$. The optimal Bayesian point estimator is the value $\hat{\theta}$ that minimizes the **posterior expected loss**, $E[L(\theta, \hat{\theta})|\text{data}]$. Different choices of [loss function](@entry_id:136784) lead directly to different [summary statistics](@entry_id:196779).

#### Squared Error Loss and the Posterior Mean
The most common [loss function](@entry_id:136784) is the **squared error loss**, $L(\theta, \hat{\theta}) = (\theta - \hat{\theta})^2$. This function penalizes errors quadratically, meaning that large errors are disproportionately more costly than small errors. To find the [optimal estimator](@entry_id:176428), we must find the value $a$ that minimizes the posterior expected loss:
$$
\rho(a) = E[(\theta - a)^2 | \text{data}] = \int (\theta - a)^2 p(\theta | \text{data}) \, d\theta
$$
By taking the derivative with respect to $a$ and setting it to zero, we find that this expression is minimized when $a = E[\theta | \text{data}]$ [@problem_id:1945465]. Therefore, **the [posterior mean](@entry_id:173826) is the optimal Bayes estimator under squared error loss**. Its use is implicitly motivated by a desire to avoid large estimation errors.

#### Absolute Error Loss and the Posterior Median
Another important loss function is the **[absolute error loss](@entry_id:170764)**, $L(\theta, \hat{\theta}) = |\theta - \hat{\theta}|$. This function's penalty is directly proportional to the magnitude of the error. It is appropriate when an overestimation of 1 unit is exactly as costly as an underestimation of 1 unit. Minimizing the posterior expected absolute loss:
$$
\rho(a) = E[|\theta - a| | \text{data}] = \int |\theta - a| p(\theta | \text{data}) \, d\theta
$$
leads to the conclusion that the [optimal estimator](@entry_id:176428) $a$ is the **[posterior median](@entry_id:174652)** [@problem_id:1945432]. The median is the estimator that minimizes the average absolute distance to the true parameter value, making it the preferred choice when the cost of error is linear and symmetric.

#### Asymmetric and Generalized Loss Functions
The decision-theoretic framework is highly flexible. Consider a situation where the costs of overestimation and underestimation are unequal. For example, a company might face a loss function where overestimating a parameter is twice as costly as underestimating it [@problem_id:1945421]. Such an asymmetric linear loss can be written as:
$$
L(\theta, \hat{\theta}) = \begin{cases} k(\theta - \hat{\theta})  &\text{if } \hat{\theta} < \theta \quad (\text{underestimation}) \\ 2k(\hat{\theta} - \theta)  &\text{if } \hat{\theta} \ge \theta \quad (\text{overestimation}) \end{cases}
$$
Minimizing the posterior expected loss for this function reveals that the [optimal estimator](@entry_id:176428) is the value $a$ such that $P(\theta \le a | \text{data}) = \frac{1}{3}$. In other words, the [optimal estimator](@entry_id:176428) is the **1/3-quantile (or 33.3rd percentile) of the [posterior distribution](@entry_id:145605)**. This powerful result shows that the [posterior median](@entry_id:174652) is just a special case of a posterior quantile that is optimal for a symmetric linear loss function. By carefully defining the [loss function](@entry_id:136784) to match the real-world consequences of estimation error, we can justify the choice of any quantile of the posterior distribution as the optimal [point estimate](@entry_id:176325).

### The Geometry of the Posterior: Symmetric vs. Skewed Distributions

The relationship between the mean, median, and mode is intimately tied to the geometric shape of the [posterior distribution](@entry_id:145605), particularly its symmetry.

For a **unimodal and symmetric** posterior distribution, the three [measures of central tendency](@entry_id:168414) coincide:
$$
\text{Posterior Mean} = \text{Posterior Median} = \text{Posterior Mode}
$$
The quintessential example is the Normal distribution. In a Normal-Normal conjugate model, where both the prior and the likelihood are Normal, the [posterior distribution](@entry_id:145605) is also Normal [@problem_id:1945435]. Since a Normal distribution is perfectly symmetric about its mean, its mean, median, and mode are all identical. In such cases, the choice between these three estimators is immaterial, as they all point to the same value.

The situation is different for **skewed** distributions. For a unimodal distribution with a **right (positive) skew**, the mass of the distribution is concentrated on the left, with a long tail to the right. The mode is at the peak, the median is pulled to the right of the mode to balance the probability mass, and the mean is pulled even further to the right by the influence of the high-valued tail. This leads to the well-known ordering:
$$
\text{Mode} < \text{Median} < \text{Mean} \quad (\text{for a right-skewed distribution})
$$
An example of this occurs in the Gamma-Poisson model. If the [posterior distribution](@entry_id:145605) for a [rate parameter](@entry_id:265473) $\lambda$ is a Gamma distribution, which is typically right-skewed, the posterior mean will be greater than the [posterior median](@entry_id:174652) [@problem_id:1945434]. For a Gamma($\alpha, \beta$) distribution, the mean is $\alpha/\beta$ while the mode is $(\alpha-1)/\beta$ (for $\alpha > 1$). The median lies between these two values. Conversely, for a left-[skewed distribution](@entry_id:175811), the ordering is reversed: $\text{Mean} < \text{Median} < \text{Mode}$.

In summary, while the full posterior distribution remains the gold standard of Bayesian inference, the mean, median, and mode provide invaluable, albeit incomplete, summaries. The [posterior mode](@entry_id:174279) identifies the most probable parameter value. The posterior mean and median, along with other [quantiles](@entry_id:178417), are best understood as optimal [point estimates](@entry_id:753543) under specific, well-defined [loss functions](@entry_id:634569). Their relationship to one another is a direct reflection of the symmetry, or lack thereof, in our final state of belief about the parameter.