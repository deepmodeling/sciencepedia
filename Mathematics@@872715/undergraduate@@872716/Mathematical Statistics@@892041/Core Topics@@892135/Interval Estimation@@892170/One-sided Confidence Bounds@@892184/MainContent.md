## Introduction
In statistical inference, estimating unknown population parameters is a core task. While [point estimates](@entry_id:753543) offer a single best guess, they fail to convey the inherent uncertainty in estimation. Two-sided confidence intervals provide a range of plausible values, but many real-world problems demand a different kind of answer. Often, the critical question is not about bracketing a parameter, but about ensuring it meets a minimum standard or does not exceed a maximum threshold. This is the gap filled by one-sided confidence bounds, which provide a statistical guarantee in one direction.

This article serves as a comprehensive guide to understanding and implementing these essential tools. The first chapter, "Principles and Mechanisms," will lay the theoretical groundwork, explaining how to construct one-sided bounds for means, variances, and proportions using methods like [pivotal quantities](@entry_id:174762) and large-sample approximations. Following this, "Applications and Interdisciplinary Connections" will demonstrate their practical power in fields ranging from quality control and engineering to [clinical trials](@entry_id:174912), showing how they drive decision-making. Finally, "Hands-On Practices" will allow you to solidify your understanding by working through applied problems. We will begin by exploring the fundamental principles and mechanisms that underpin one-sided confidence bounds.

## Principles and Mechanisms

In statistical inference, a primary objective is to estimate unknown population parameters using sample data. While a point estimate provides a single best guess, it conveys no information about the uncertainty of that guess. A two-sided confidence interval addresses this by providing a range of plausible values for the parameter. However, in many scientific, engineering, and policy contexts, the interest is not in bracketing a parameter on both sides, but rather in establishing a boundary on one side only. This leads to the concept of **one-sided confidence bounds**.

### The Rationale for One-Sided Bounds

The motivation for one-sided bounds arises when the practical implications of an estimation error are asymmetric. We are often concerned with ensuring a parameter is *at least* a certain value (a minimum guarantee) or *at most* a certain value (a maximum limit).

For instance, consider a robotics company assessing a new high-endurance battery. The primary concern for marketing and reliability is to provide a conservative guarantee on its performance. The question of interest is not "what is the range of the average battery lifetime?" but rather "what is the minimum [average lifetime](@entry_id:195236) we can confidently claim?" This calls for a **[lower confidence bound](@entry_id:172707)** [@problem_id:1941745]. Conversely, a food quality agency investigating a "low-calorie" snack is primarily concerned that the true average calorie content might be unacceptably high. The goal is to determine a value $C$ such that they can be highly confident the true mean calorie content is *less than* $C$. This requires an **[upper confidence bound](@entry_id:178122)** [@problem_id:1941726].

Formally, for a parameter $\theta$, a **$100(1-\alpha)\%$ one-sided [upper confidence bound](@entry_id:178122)** is a statistic $U$ calculated from the sample data such that:
$$ P(\theta \le U) = 1-\alpha $$
This means that in the long run, $100(1-\alpha)\%$ of the [upper bounds](@entry_id:274738) calculated from repeated samples will be greater than or equal to the true parameter value $\theta$. Similarly, a **$100(1-\alpha)\%$ one-sided [lower confidence bound](@entry_id:172707)** is a statistic $L$ such that:
$$ P(\theta \ge L) = 1-\alpha $$

### Constructing Bounds via Pivotal Quantities

The most common method for deriving exact confidence bounds is the **[pivotal quantity](@entry_id:168397) method**. A [pivotal quantity](@entry_id:168397), or **pivot**, is a function of the sample data and the parameter of interest whose probability distribution is known and does not depend on any unknown parameters.

#### Bounds for the Mean of a Normal Distribution

A foundational example is making inferences about the mean $\mu$ of a normally distributed population. When the population variance $\sigma^2$ is unknown, we use the [sample mean](@entry_id:169249) $\bar{X}$ and sample standard deviation $S$. The [pivotal quantity](@entry_id:168397) is the [t-statistic](@entry_id:177481):
$$ T = \frac{\bar{X} - \mu}{S / \sqrt{n}} $$
This quantity follows a Student's [t-distribution](@entry_id:267063) with $\nu = n-1$ degrees of freedom, a distribution that depends only on the sample size $n$.

To derive an [upper confidence bound](@entry_id:178122), we start with a probability statement about the pivot $T$. Let $t_{\alpha, \nu}$ be the critical value of the t-distribution with $\nu$ degrees of freedom such that the area in the upper tail is $\alpha$, i.e., $P(T > t_{\alpha, \nu}) = \alpha$. This implies $P(T \le t_{\alpha, \nu}) = 1-\alpha$. We can then manipulate the inequality algebraically to isolate $\mu$:
$$ P\left(\frac{\bar{X} - \mu}{S / \sqrt{n}} \le t_{\alpha, n-1}\right) = 1-\alpha $$
$$ P\left(\bar{X} - \mu \le t_{\alpha, n-1} \frac{S}{\sqrt{n}}\right) = 1-\alpha $$
$$ P\left(-\mu \le -\bar{X} + t_{\alpha, n-1} \frac{S}{\sqrt{n}}\right) = 1-\alpha $$
$$ P\left(\mu \ge \bar{X} - t_{\alpha, n-1} \frac{S}{\sqrt{n}}\right) = 1-\alpha $$
This derivation yields the formula for a [lower confidence bound](@entry_id:172707). A similar argument, starting with $P(T \ge -t_{\alpha, n-1}) = 1-\alpha$, gives the $100(1-\alpha)\%$ [upper confidence bound](@entry_id:178122) for $\mu$:
$$ U = \bar{X} + t_{\alpha, n-1} \frac{S}{\sqrt{n}} $$
And the $100(1-\alpha)\%$ [lower confidence bound](@entry_id:172707) for $\mu$ is:
$$ L = \bar{X} - t_{\alpha, n-1} \frac{S}{\sqrt{n}} $$

**Example:** A food agency samples $n=16$ snack bars and finds a [sample mean](@entry_id:169249) $\bar{x} = 104.5$ kcal and sample standard deviation $s=8.0$ kcal. To find a 95% upper bound for the true mean $\mu$ ($\alpha=0.05$), they use the t-distribution with $df=15$. The critical value is $t_{0.05, 15} \approx 1.753$. The upper bound is calculated as:
$$ U = 104.5 + 1.753 \times \frac{8.0}{\sqrt{16}} = 104.5 + 3.506 = 108.006 $$
The agency can be 95% confident that the true average calorie content is no more than 108.0 kcal [@problem_id:1941726].

**Example:** A robotics company tests $n=10$ batteries and calculates a sample [mean lifetime](@entry_id:273413) of $\bar{x} = 50.2$ hours and sample standard deviation of $s \approx 2.28$ hours. To find a 99% [lower confidence bound](@entry_id:172707) for the true [mean lifetime](@entry_id:273413) $\mu$ ($\alpha=0.01$), they use the t-distribution with $df=9$. The critical value is $t_{0.01, 9} \approx 2.821$. The lower bound is:
$$ L = 50.2 - 2.821 \times \frac{2.28}{\sqrt{10}} \approx 50.2 - 2.03 \approx 48.2 $$
The company can be 99% confident that the true mean battery lifetime is at least 48.2 hours [@problem_id:1941745].

#### Bounds for the Variance of a Normal Distribution

The pivotal method can also be used for the population variance, $\sigma^2$. For a random sample from a [normal distribution](@entry_id:137477), the following quantity is a pivot:
$$ \frac{(n-1)S^2}{\sigma^2} \sim \chi^2_{n-1} $$
This statistic follows a [chi-squared distribution](@entry_id:165213) with $\nu = n-1$ degrees of freedom.

To find an upper bound on variance—a common goal in quality control to limit inconsistency—we want to find $U$ such that $P(\sigma^2 \le U) = 1-\alpha$. This requires us to find a value that $\sigma^2$ is unlikely to exceed. Let $\chi^2_{\alpha, n-1}$ denote the critical value such that the area to its left is $\alpha$. The relevant probability statement is:
$$ P\left(\frac{(n-1)S^2}{\sigma^2} \ge \chi^2_{\alpha, n-1}\right) = 1-\alpha $$
Rearranging the inequality to isolate $\sigma^2$ yields the upper bound:
$$ \sigma^2 \le \frac{(n-1)S^2}{\chi^2_{\alpha, n-1}} $$
Note that to get an *upper* bound for $\sigma^2$, we use the *lower-tail* quantile of the [chi-squared distribution](@entry_id:165213).

**Example:** A quality control engineer samples $n=20$ cereal boxes and finds a sample standard deviation of $s=8.5$ grams. To find a 95% upper bound for the true variance $\sigma^2$, we have $\alpha=0.05$ and $\nu=19$. The lower 0.05 quantile of a $\chi^2_{19}$ distribution is approximately $10.117$. The upper bound is:
$$ U = \frac{(20-1) \times (8.5)^2}{10.117} = \frac{19 \times 72.25}{10.117} \approx 136 \text{ g}^2 $$
The engineer can be 95% confident that the true variance of the filling process does not exceed 136 g$^2$ [@problem_id:1941728].

### Large-Sample Approximate Bounds

When an exact [pivotal quantity](@entry_id:168397) is unavailable, or if the underlying distribution is unknown, we can often rely on the **Central Limit Theorem (CLT)** to construct approximate bounds for large sample sizes.

#### Bounds for a Population Proportion

A common application is finding a bound for a population proportion, $p$. For a large sample size $n$, the [sample proportion](@entry_id:264484) $\hat{p} = X/n$ is approximately normally distributed. The standardized quantity
$$ Z = \frac{\hat{p} - p}{\sqrt{p(1-p)/n}} $$
is approximately a standard normal random variable. For practical use, the unknown $p$ in the standard error term is replaced with its estimate $\hat{p}$. This gives the approximate [pivotal quantity](@entry_id:168397):
$$ Z \approx \frac{\hat{p} - p}{\sqrt{\hat{p}(1-\hat{p})/n}} $$
Let $z_\alpha$ be the upper $\alpha$-quantile of the [standard normal distribution](@entry_id:184509). By following the same logic as in the t-distribution case, we can derive the approximate $100(1-\alpha)\%$ one-sided bounds for $p$:
$$ \text{Upper Bound: } U = \hat{p} + z_{\alpha} \sqrt{\frac{\hat{p}(1-\hat{p})}{n}} $$
$$ \text{Lower Bound: } L = \hat{p} - z_{\alpha} \sqrt{\frac{\hat{p}(1-\hat{p})}{n}} $$
These formulas are considered reliable when the sample is large enough, typically when both $n\hat{p} \ge 10$ and $n(1-\hat{p}) \ge 10$.

**Example:** A poll of $n=500$ voters finds that $x=220$ support a policy, giving $\hat{p} = 220/500 = 0.44$. To find a 95% lower bound for the true proportion $p$ of supporters, we use $\alpha=0.05$ and the critical value $z_{0.05} = 1.645$. The lower bound is:
$$ L = 0.44 - 1.645 \sqrt{\frac{0.44(1-0.44)}{500}} \approx 0.44 - 1.645 \times 0.0222 \approx 0.4035 $$
The firm can be 95% confident that the true support for the policy is at least 40.35% [@problem_id:1941753].

### The Duality with One-Sided Hypothesis Testing

One of the most important theoretical aspects of [confidence intervals](@entry_id:142297) is their duality with hypothesis tests. This relationship provides a unified framework for inference. For any parameter $\theta$, a $100(1-\alpha)\%$ confidence interval can be viewed as the set of all plausible values for $\theta_0$ that would *not* be rejected in a [hypothesis test](@entry_id:635299) of $H_0: \theta = \theta_0$ at the $\alpha$ [significance level](@entry_id:170793).

This duality extends elegantly to one-sided scenarios. Consider testing a hypothesis about a minimum requirement, such as $H_0: p \le p_0$ versus $H_1: p > p_0$. This test asks: "Is there significant evidence that the true proportion $p$ is greater than some threshold $p_0$?" The conclusion of this test is directly linked to a one-sided [lower confidence bound](@entry_id:172707) for $p$.

The decision rule is as follows: we reject the [null hypothesis](@entry_id:265441) $H_0: p \le p_0$ in favor of the alternative $H_1: p > p_0$ at [significance level](@entry_id:170793) $\alpha$ if and only if the $100(1-\alpha)\%$ [lower confidence bound](@entry_id:172707) for $p$ lies entirely above $p_0$. That is, we reject $H_0$ if $L > p_0$. The logic is that if our entire range of plausible values for $p$ (i.e., $[L, 1]$) excludes $p_0$, we have statistically significant evidence that the true value of $p$ is indeed greater than $p_0$.

**Example:** A company wants to determine if a new biodegradable plastic is superior to an old one, which has a biodegradability proportion of $p_0 = 0.60$. They test the hypotheses $H_0: p \le 0.60$ versus $H_1: p > 0.60$ at $\alpha = 0.05$. In a sample of $n=200$, they observe $x=135$ biodegraded pieces, so $\hat{p} = 0.675$. The corresponding 95% [lower confidence bound](@entry_id:172707) for $p$ is calculated as approximately $L = 0.621$. Since $0.621 > 0.60$, the null value $p_0=0.60$ is not contained within the 95% confidence region $[0.621, 1]$. Therefore, the team can reject the null hypothesis and conclude that the new plastic has a significantly higher biodegradability proportion [@problem_id:1941727].

### Advanced and Specialized Bounds

While the methods above cover many common scenarios, statistical practice often requires more specialized techniques for constructing one-sided bounds.

#### Bounds from First Principles: The Exponential Distribution

Consider a random sample $X_1, \dots, X_n$ from an [exponential distribution](@entry_id:273894) with rate parameter $\lambda$, often used to model lifetimes or failure rates. A higher $\lambda$ implies a shorter [average lifetime](@entry_id:195236). To find an upper bound for this undesirable rate, we can again use the pivotal method. A key statistical fact is that the sum of these observations, $T = \sum_{i=1}^n X_i$, follows a Gamma distribution, and the scaled sum, $2\lambda T$, follows a chi-squared distribution with $2n$ degrees of freedom. Thus, $2\lambda T \sim \chi^2_{2n}$ is a pivot. To find an upper bound for $\lambda$, we write:
$$ P(2\lambda T \le \chi^2_{1-\alpha, 2n}) = 1-\alpha $$
Solving for $\lambda$ gives the $100(1-\alpha)\%$ [upper confidence bound](@entry_id:178122):
$$ U = \frac{\chi^2_{1-\alpha, 2n}}{2T} $$
This derivation demonstrates how the pivotal method extends to non-normal distributions, provided a suitable [pivotal quantity](@entry_id:168397) can be identified [@problem_id:1941762].

#### Exact Bounds by Test Inversion: The Negative Binomial

In some cases, a bound is most elegantly derived by directly inverting the acceptance region of a hypothesis test. Consider an experiment where trials are repeated until $r$ successes are observed, and we count the number of failures, $X$. This follows a [negative binomial distribution](@entry_id:262151) with success probability $p$. To find a lower bound for $p$, we can use the **Clopper-Pearson method**, which defines the bound $p_L$ as the value of $p$ for which the observed outcome $x$ would be just barely significant. For a lower bound, we consider the test $H_0: p \le p_0$ vs $H_1: p > p_0$. Small values of $X$ (failures) are evidence for large $p$. The [p-value](@entry_id:136498) for an observed $x$ is $P_p(X \le x)$. The lower bound $p_L$ is the value of $p$ that satisfies:
$$ P_{p_L}(X \le x) = \alpha $$
A fundamental identity connects the cumulative distribution function (CDF) of the [negative binomial distribution](@entry_id:262151) to the CDF of the Beta distribution: $P_p(X \le x) = I_p(r, x+1)$, where $I_p$ is the [regularized incomplete beta function](@entry_id:181457). Thus, the lower bound is the solution to $F_{\text{Beta}(r, x+1)}(p_L) = \alpha$, which is simply the $\alpha$-quantile of a Beta distribution:
$$ p_L = F_{\text{Beta}(r, x+1)}^{-1}(\alpha) $$
This provides an exact, non-trivial confidence bound derived from foundational principles [@problem_id:1941735].

#### Distribution-Free Bounds for Quantiles

A powerful class of methods, known as **non-parametric** or **distribution-free** methods, do not require assumptions about the underlying distribution family. A classic example is finding a confidence bound for a population quantile, $\eta_p$, using [order statistics](@entry_id:266649). Let $X_{(1)} \le X_{(2)} \le \dots \le X_{(n)}$ be the ordered sample from any continuous distribution. Consider using the sample maximum, $X_{(n)}$, to form an [upper confidence bound](@entry_id:178122) $(-\infty, X_{(n)}]$ for the $p$-th quantile $\eta_p$. The [confidence level](@entry_id:168001) of this interval is the probability $P(\eta_p \le X_{(n)})$. The only way this statement can be false is if all $n$ observations fall below $\eta_p$. The probability of this event is:
$$ P(X_{(n)}  \eta_p) = P(X_1  \eta_p, \dots, X_n  \eta_p) = [P(X  \eta_p)]^n = p^n $$
Therefore, the [confidence level](@entry_id:168001) is exactly $1 - p^n$. This simple formula allows us to determine the sample size needed to achieve a desired [confidence level](@entry_id:168001) without knowing anything about the population's distribution shape [@problem_id:1941734]. For example, to be at least 99.9% confident that the 90th percentile, $\eta_{0.90}$, is less than the sample maximum, we need to solve $1 - (0.90)^n \ge 0.999$, which yields a minimum sample size of $n=66$.

#### Advanced Asymptotic Bounds

For complex parameters that are functions of simpler parameters, the **Delta method** combined with transformations can yield approximate bounds. For example, if the number of defects in a sample follows a Poisson distribution with mean $\lambda$, the probability of a sample being imperfect is $\theta = 1 - \exp(-\lambda)$. A bound on $\theta$ can be derived from a bound on $\lambda$. A more statistically robust approach first applies a **[variance-stabilizing transformation](@entry_id:273381)**. For a Poisson mean, the transformation $h(\lambda) = \sqrt{\lambda}$ is variance-stabilizing. Using the CLT, one can construct a bound for $\sqrt{\lambda}$, which can then be transformed back to obtain a bound for $\lambda$, and finally, by applying the function $g(\lambda) = 1-\exp(-\lambda)$, one can obtain an upper bound for the imperfection probability $\theta$ [@problem_id:1941749].

Finally, for certain problems, such as placing a lower bound on the reliability probability $p = P(X > c)$ where $X \sim N(\mu, \sigma^2)$, highly specialized tools are required. The key is to recognize that $p$ is a function of the standardized mean difference $\delta = (\mu-c)/\sigma$. Inferences about $\delta$ can be made using the **non-central t-distribution**, which governs the statistic $T = \sqrt{n}(\bar{X}-c)/S$. By finding a [lower confidence bound](@entry_id:172707) for the non-centrality parameter $\lambda = \sqrt{n}\delta$, one can derive a lower bound for $\delta$, and in turn, a lower bound for the probability $p = \Phi(\delta)$, where $\Phi$ is the standard normal CDF [@problem_id:1941725]. These advanced techniques showcase the breadth and depth of methods available for constructing one-sided confidence bounds in diverse statistical problems.