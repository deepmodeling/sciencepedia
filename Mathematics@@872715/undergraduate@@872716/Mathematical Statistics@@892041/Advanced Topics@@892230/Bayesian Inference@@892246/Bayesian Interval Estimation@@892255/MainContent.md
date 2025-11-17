## Introduction
In the landscape of statistical inference, quantifying uncertainty is as crucial as estimating a parameter's value. Bayesian [interval estimation](@entry_id:177880) offers a powerful and intuitive framework for this task. By leveraging the [posterior distribution](@entry_id:145605)—the result of updating prior beliefs with observed data—Bayesian methods produce [credible intervals](@entry_id:176433), which provide a direct probabilistic summary of where a parameter is likely to lie. This approach addresses the common scientific question, "What is the range of plausible values for the parameter of interest?", with a clarity and directness that is highly appealing. This article serves as a guide to understanding and applying this fundamental tool of Bayesian statistics.

The following chapters will systematically build your expertise in Bayesian [interval estimation](@entry_id:177880). First, in **Principles and Mechanisms**, we will delve into the core concepts, defining the credible interval and contrasting its straightforward interpretation with the frequentist confidence interval. We will explore the primary methods of construction—the equal-tailed and Highest Posterior Density (HPD) intervals—and examine how they behave in foundational statistical models. Next, in **Applications and Interdisciplinary Connections**, we will witness the versatility of Bayesian intervals through a survey of their use in diverse fields, from quality control in engineering to [molecular dating](@entry_id:147513) in biology, highlighting their ability to solve complex, real-world problems. Finally, the **Hands-On Practices** section provides an opportunity to apply these concepts, guiding you through the construction of [credible intervals](@entry_id:176433) in practical scenarios, from basic probability estimation to modern [simulation-based inference](@entry_id:754873).

## Principles and Mechanisms

Following our introduction to the philosophical foundations of Bayesian inference, we now turn to one of its most practical and widely used outputs: the summarization of posterior knowledge. Once we have derived the posterior distribution $p(\theta | y)$, which encapsulates all that is known about a parameter $\theta$ after observing data $y$, a common task is to report a range of plausible values for $\theta$. This is the role of the Bayesian [credible interval](@entry_id:175131). In this chapter, we will explore the principles governing the definition and interpretation of [credible intervals](@entry_id:176433), the mechanisms for their construction, and their behavior in various common statistical models.

### The Credible Interval: A Direct Statement of Posterior Probability

The core output of a Bayesian analysis is the [posterior distribution](@entry_id:145605). A **credible interval** is a summary of this distribution, providing a range of values for the parameter that is plausible given the data and our prior beliefs. Formally, for a given probability level $1-\alpha$, a $100(1-\alpha)\%$ credible interval for a parameter $\theta$ is a subset $C$ of the parameter space such that:

$$
\Pr(\theta \in C \mid y) = \int_{C} p(\theta \mid y) \,d\theta = 1-\alpha
$$

The most profound and practical feature of the [credible interval](@entry_id:175131) lies in its direct interpretation. If a Bayesian analysis yields a 95% [credible interval](@entry_id:175131) for a parameter $\theta$ of $[0.72, 0.89]$, the interpretation is straightforward: given the observed data and the assumptions of the model, there is a 95% probability that the true value of $\theta$ lies within the interval $[0.72, 0.89]$ [@problem_id:1899400]. This is a direct probabilistic statement about the parameter itself.

This interpretation stands in stark contrast to that of the frequentist **[confidence interval](@entry_id:138194)**. A 95% [confidence interval](@entry_id:138194) is the result of a procedure that, if repeated across many independent experiments, would produce intervals containing the true, fixed parameter value in 95% of instances. However, for any single interval calculated from a specific dataset, frequentist theory does not permit us to say there is a 95% probability that the true parameter lies within it. The parameter is considered a fixed constant, not a random variable, so it is either in the interval or it is not. The probability statement refers to the long-run performance of the interval-generating procedure, not to the specific interval at hand.

The Bayesian [credible interval](@entry_id:175131), by treating $\theta$ as a random variable whose uncertainty is described by the posterior distribution, provides an answer that aligns more closely with the intuitive question researchers often ask: "How likely is it that the true value of the parameter is in this range?" [@problem_id:1899402].

### Constructing Credible Intervals

While the definition of a [credible interval](@entry_id:175131) is a region containing a specified [posterior probability](@entry_id:153467) mass, it does not uniquely define the interval. For any given posterior distribution, there are infinitely many intervals that could satisfy the condition. Therefore, we require additional criteria to select a specific interval. The two most common types of [credible intervals](@entry_id:176433) are the [equal-tailed interval](@entry_id:164843) and the highest posterior density (HPD) interval.

#### Equal-Tailed Intervals

The **[equal-tailed interval](@entry_id:164843)** is the most widely used type of credible interval due to its simplicity of construction. A $100(1-\alpha)\%$ [equal-tailed interval](@entry_id:164843) is defined by the $\alpha/2$ and $1-\alpha/2$ [quantiles](@entry_id:178417) of the posterior distribution. Let $F(\theta | y)$ be the cumulative distribution function (CDF) of the posterior for $\theta$. The lower bound $L$ and upper bound $U$ of the interval are found such that:

$$
F(L \mid y) = \frac{\alpha}{2} \quad \text{and} \quad F(U \mid y) = 1 - \frac{\alpha}{2}
$$

This construction ensures that the probability of $\theta$ being below the interval is equal to the probability of it being above the interval, with each tail containing $\alpha/2$ of the [posterior probability](@entry_id:153467) mass.

For example, consider an analysis of a [biosensor](@entry_id:275932)'s detection probability, $\theta$. Suppose that after combining a $\text{Beta}(2, 2)$ prior with experimental data of 14 successes in 18 trials, the [posterior distribution](@entry_id:145605) is found to be $\theta | \text{data} \sim \text{Beta}(16, 6)$. To find the 90% equal-tailed [credible interval](@entry_id:175131) ($\alpha = 0.10$), we need to find the values $L$ and $U$ such that $P(\theta  L | \text{data}) = 0.05$ and $P(\theta > U | \text{data}) = 0.05$. The latter condition is equivalent to $P(\theta \le U | \text{data}) = 0.95$. If the 0.05 quantile of the $\text{Beta}(16, 6)$ distribution is 0.559 and the 0.95 quantile is 0.875, then the 90% equal-tailed credible interval is $[0.559, 0.875]$ [@problem_id:1899393].

#### Highest Posterior Density (HPD) Intervals

An alternative and conceptually appealing choice is the **Highest Posterior Density (HPD) interval**. For a given probability level $1-\alpha$, the HPD interval is the set of values for $\theta$ such that:
1.  The total probability of the set is $1-\alpha$.
2.  For every value $\theta_1$ inside the interval and every value $\theta_2$ outside the interval, the posterior density at $\theta_1$ is greater than or equal to the posterior density at $\theta_2$, i.e., $p(\theta_1 | y) \ge p(\theta_2 | y)$.

This second condition means that the HPD interval includes the "most plausible" values of the parameter. A key property of the HPD interval is that for a given probability level $1-\alpha$, it is the shortest possible credible interval.

For unimodal and symmetric posterior distributions, such as the Normal distribution, the [equal-tailed interval](@entry_id:164843) and the HPD interval are identical. However, for skewed or multimodal distributions, they can differ. The HPD interval is particularly insightful for multimodal posteriors. Consider a scenario where the [posterior distribution](@entry_id:145605) for a parameter $\theta$ is a mixture of two well-separated normal distributions: $p(\theta|\text{data}) = 0.5 \cdot N(\theta; 10, 1) + 0.5 \cdot N(\theta; 20, 1)$. This distribution has two modes, one at $\theta=10$ and one at $\theta=20$, with a region of very low density in between. An [equal-tailed interval](@entry_id:164843) would be forced to include this low-density region to connect the two modes into a single interval. In contrast, the 90% HPD interval would consist of two disjoint intervals, one centered around each mode, for instance, $[8.355, 11.645] \cup [18.355, 21.645]$. This provides a more faithful summary of our posterior belief: $\theta$ is likely to be near 10 or near 20, but very unlikely to be in the region between them [@problem_id:1899419].

### Credible Intervals for Common Models

Let's examine how [credible intervals](@entry_id:176433) are derived and how they behave in some standard modeling scenarios.

#### Normal Model with Known Variance

A foundational example is estimating the mean $\mu$ of a normal distribution with known variance $\sigma^2$. If we adopt a normal prior for the mean, $\mu \sim \mathcal{N}(\mu_0, \sigma_0^2)$, and our data consists of $n$ observations with [sample mean](@entry_id:169249) $\bar{x}$, the [posterior distribution](@entry_id:145605) for $\mu$ is also normal, $\mu \mid y \sim \mathcal{N}(\mu_n, \sigma_n^2)$. The posterior mean $\mu_n$ and variance $\sigma_n^2$ are given by:

$$
\mu_n = \frac{\frac{1}{\sigma_0^2}\mu_0 + \frac{n}{\sigma^2}\bar{x}}{\frac{1}{\sigma_0^2} + \frac{n}{\sigma^2}} \quad \text{and} \quad \sigma_n^2 = \left(\frac{1}{\sigma_0^2} + \frac{n}{\sigma^2}\right)^{-1}
$$

The posterior mean is a **precision-weighted average** of the prior mean $\mu_0$ and the sample mean $\bar{x}$, where precision is the reciprocal of variance. The posterior represents a compromise between [prior belief](@entry_id:264565) and observed data. If the prior is very precise (small $\sigma_0^2$), the [posterior mean](@entry_id:173826) will be close to $\mu_0$. If the data is very informative (large $n$), the [posterior mean](@entry_id:173826) will be pulled towards $\bar{x}$ [@problem_id:1899399].

Since the posterior is normal, the 95% symmetric [credible interval](@entry_id:175131) (which is both equal-tailed and HPD) is simply:
$$
[\mu_n - 1.96 \cdot \sigma_n, \mu_n + 1.96 \cdot \sigma_n]
$$

#### The Role of Data and Priors

The resulting [credible interval](@entry_id:175131) is a function of both the [prior information](@entry_id:753750) and the data. Two aspects are particularly important: the amount of data and the choice of prior.

**The Influence of Sample Size:** As the amount of data increases, the posterior distribution becomes more concentrated, and consequently, the [credible interval](@entry_id:175131) becomes narrower. This reflects our increasing certainty about the parameter's value. For instance, in an A/B test analyzing a click-through rate $p$, if two experiments yield the same [sample proportion](@entry_id:264484) of clicks (e.g., 0.15), but one has a sample size of $n=1000$ and the other has $n=100$, the [credible interval](@entry_id:175131) from the larger experiment will be significantly narrower. The larger dataset provides more information, leading to a more precise posterior belief [@problem_id:1899380]. In the limit as $n \to \infty$, the influence of any reasonable prior vanishes, and the posterior becomes entirely dominated by the data.

**The Influence of the Prior:**
- **Non-informative Priors:** In some cases, we wish to express maximal uncertainty in our prior. For a normal mean $\mu$, a common **[non-informative prior](@entry_id:163915)** is an improper uniform distribution, $p(\mu) \propto 1$. When combined with a normal likelihood, this leads to a [posterior distribution](@entry_id:145605) for the mean that is normal, centered at the [sample mean](@entry_id:169249) $\bar{x}$, with variance $\sigma^2/n$: $\mu \mid y \sim \mathcal{N}(\bar{x}, \sigma^2/n)$. The resulting 95% [credible interval](@entry_id:175131), $\bar{x} \pm 1.96 \frac{\sigma}{\sqrt{n}}$, is numerically identical to the frequentist 95% [confidence interval](@entry_id:138194) for $\mu$ [@problem_id:1899396]. This correspondence is a recurring theme when using [non-informative priors](@entry_id:176964) and serves as a useful bridge between Bayesian and frequentist results.

- **Robust Priors:** The choice of prior can also be used to make an analysis more robust to surprising data, such as [outliers](@entry_id:172866). If our prior for a mean $\mu$ is Normal, $N(\mu_0, \tau_0^2)$, an outlier in the data can exert a strong pull on the posterior, dragging it away from the prior mean. An alternative is to use a **heavy-tailed prior**, such as a Student's t-distribution. The heavier tails of the [t-distribution](@entry_id:267063) assign more prior probability to values of $\mu$ far from the prior mean $\mu_0$. This makes the model more accommodating of data that is inconsistent with the prior beliefs. When an outlier is observed, a t-prior allows the posterior mean to be less influenced by the outlier compared to a normal prior, resulting in a more robust inference [@problem_id:1899369].

### Advanced Cases and Computational Solutions

While the examples above are illustrative, real-world analyses often involve more complex models.

#### Nuisance Parameters

Often, a model contains multiple unknown parameters, but we are only interested in making inferences about one of them. The other parameters are called **[nuisance parameters](@entry_id:171802)**. The standard Bayesian procedure is to obtain the marginal posterior distribution for the parameter of interest by integrating the joint [posterior distribution](@entry_id:145605) over all [nuisance parameters](@entry_id:171802).

A classic example is the normal model where both the mean $\mu$ and the variance $\sigma^2$ are unknown. Using a standard [non-informative prior](@entry_id:163915) $p(\mu, \sigma^2) \propto 1/\sigma^2$, one can derive the joint posterior $p(\mu, \sigma^2 | y)$. To get a [credible interval](@entry_id:175131) for $\mu$, we must integrate out the [nuisance parameter](@entry_id:752755) $\sigma^2$:

$$
p(\mu \mid y) = \int_0^\infty p(\mu, \sigma^2 \mid y) \,d\sigma^2
$$

Performing this integration reveals that the marginal [posterior distribution](@entry_id:145605) for $\mu$ is not normal, but rather a scaled and shifted Student's [t-distribution](@entry_id:267063) centered at the sample mean $\bar{x}$ with $n-1$ degrees of freedom. The credible interval for $\mu$ is then constructed using [quantiles](@entry_id:178417) from this [t-distribution](@entry_id:267063): $\bar{x} \pm t_{n-1, 1-\alpha/2} \frac{s}{\sqrt{n}}$, where $s$ is the sample standard deviation [@problem_id:1899387]. The use of the [t-distribution](@entry_id:267063) appropriately accounts for the additional uncertainty introduced by not knowing $\sigma^2$.

#### Credible Intervals from Posterior Samples

For many complex, modern statistical models, the posterior distribution is analytically intractable; it cannot be written down in a closed form, and integration is not feasible. In these situations, Bayesian inference relies on computational algorithms, most notably **Markov Chain Monte Carlo (MCMC)** methods, to generate a large number of samples from the [posterior distribution](@entry_id:145605).

Once we have a large collection of, say, 10,000 samples $\{\theta^{(1)}, \theta^{(2)}, \dots, \theta^{(10000)}\}$ drawn from $p(\theta | y)$, constructing a credible interval becomes remarkably simple. To find a $100(1-\alpha)\%$ equal-tailed credible interval, we can use the empirical [quantiles](@entry_id:178417) of the samples. The procedure is as follows:
1.  Sort the MCMC samples in ascending order.
2.  The lower bound of the interval is the sample at rank $(\alpha/2) \times N$.
3.  The upper bound of the interval is the sample at rank $(1 - \alpha/2) \times N$.

For a 95% interval from 40 samples, we would find the lower and upper bounds by taking the 2nd and 39th values in the sorted list, as these approximate the 2.5% and 97.5% [quantiles](@entry_id:178417) of the [posterior distribution](@entry_id:145605) [@problem_id:1899403]. This simulation-based approach is powerful and general, allowing for the construction of [credible intervals](@entry_id:176433) for any parameter in any model for which posterior samples can be generated.