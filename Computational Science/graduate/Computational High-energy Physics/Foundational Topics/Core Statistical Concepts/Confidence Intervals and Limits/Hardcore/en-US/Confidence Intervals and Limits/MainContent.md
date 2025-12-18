## Introduction
Confidence intervals and limits are the cornerstone of [statistical inference](@entry_id:172747) in experimental science, providing the essential language for quantifying uncertainty and communicating the results of measurements. In [high-energy physics](@entry_id:181260), where experiments push the frontiers of knowledge by searching for subtle signals amidst vast backgrounds, the correct construction and interpretation of these statistical statements are paramount. However, the path from raw data to a final [confidence interval](@entry_id:138194) is complex, filled with challenges such as the proper handling of [systematic uncertainties](@entry_id:755766), the presence of physical boundaries on parameters, and the risk of misinterpreting statistical fluctuations. This article provides a graduate-level guide to navigating these challenges within the frequentist framework.

Over the next three chapters, you will build a robust understanding of these critical statistical tools. The journey begins in **Principles and Mechanisms**, where we will dissect the core concepts of [frequentist statistics](@entry_id:175639), from the foundational Neyman construction to the powerful but nuanced application of likelihood-based [asymptotic methods](@entry_id:177759). Next, in **Applications and Interdisciplinary Connections**, we will see these principles in action, exploring their use in designing and optimizing physics analyses, combining results, and drawing connections to similar statistical problems in cosmology, genetics, and finance. Finally, **Hands-On Practices** will provide you with the opportunity to implement these methods yourself, solidifying your theoretical knowledge through practical, computational exercises that mirror the work of a professional physicist.

## Principles and Mechanisms

This chapter delves into the fundamental principles and operational mechanisms underlying the construction and interpretation of confidence intervals and limits, a cornerstone of [statistical inference](@entry_id:172747) in high-energy physics. We will begin by establishing the core tenets of the frequentist framework, explore exact and approximate methods for interval construction, and address the sophisticated challenges posed by [nuisance parameters](@entry_id:171802), physical boundaries, and [multiple hypothesis testing](@entry_id:171420).

### Core Principles of Frequentist Intervals

At the heart of [frequentist statistics](@entry_id:175639) is the idea that probability describes the long-run frequency of outcomes in hypothetical repetitions of an experiment. Parameters of a model are considered fixed, unknown constants, while the data, and any quantity derived from it, are random variables.

#### The Concept of Coverage

The defining characteristic of a frequentist confidence interval procedure is its **coverage**. For a given procedure that produces an interval $C(X)$ from data $X$ for a parameter $\theta$, the coverage probability at a fixed true value $\theta_0$ is the probability that the random interval will contain $\theta_0$. This probability is computed under the [sampling distribution](@entry_id:276447) of the data assuming $\theta = \theta_0$, and is denoted $P_{\theta_0}(\theta_0 \in C(X))$ .

A procedure is said to have a [confidence level](@entry_id:168001) (CL) of $1-\alpha$ if its coverage probability is at least $1-\alpha$ for all possible values of $\theta$. Formally, this is the condition $\inf_{\theta} P_{\theta}(\theta \in C(X)) \ge 1-\alpha$. This guarantees a minimum success rate for the procedure.

It is critical to interpret the [confidence level](@entry_id:168001) correctly. A statement such as "a $95\%$ [confidence interval](@entry_id:138194)" does not mean there is a $0.95$ probability that the true parameter lies within a specific, already-computed interval. Once the data are observed and an interval is calculated (e.g., $[1.2, 3.4]$), the true parameter is either in it or not. The probability statement applies to the *procedure* itself, not to a single outcome. The operational meaning of a $95\%$ [confidence level](@entry_id:168001) is that if one were to repeat the experiment a large number of times, approximately $95\%$ of the computed intervals would contain the true, fixed value of the parameter . Confusing this with a Bayesian [credible interval](@entry_id:175131), which does make a probabilistic statement about the parameter given the data, is a common but fundamental error.

The coverage of a proposed interval construction method is not just a theoretical claim; it can and should be empirically verified. In computational physics, this is done using **Monte Carlo pseudo-experiments**. One fixes a true value for the parameter(s) of interest, $\theta^{\star}$, and any [nuisance parameters](@entry_id:171802), $\eta^{\star}$. A large number of synthetic datasets are then generated from the model $f(x; \theta^{\star}, \eta^{\star})$. The full interval construction procedure is applied to each synthetic dataset, and the coverage is estimated as the fraction of the resulting intervals that contain $\theta^{\star}$ .

#### The Neyman Construction: A General Framework

The foundational method for constructing confidence intervals with guaranteed coverage is the **Neyman construction** . This elegant procedure consists of two conceptual steps:

1.  **Constructing the Acceptance Belt**: For *each* possible value of the parameter $\theta$, an **acceptance region** $A_{\theta}$ is defined in the space of possible data outcomes. This region is a set of data outcomes that are considered "compatible" with the given $\theta$. The region must be chosen such that the probability of observing data within it, given that $\theta$ is the true value, is at least the desired [confidence level](@entry_id:168001): $P(X \in A_{\theta} | \theta) \ge 1-\alpha$. The collection of all such acceptance regions, visualized as a band or "belt" in the space of $(\theta, X)$, is the confidence belt.

2.  **Inverting the Belt**: After performing the experiment and observing a specific data outcome $x_{\text{obs}}$, the [confidence interval](@entry_id:138194) $C(x_{\text{obs}})$ is found by "inverting" the belt. The interval consists of all values of $\theta$ for which the observed data $x_{\text{obs}}$ falls into their corresponding acceptance region: $C(x_{\text{obs}}) = \{ \theta \mid x_{\text{obs}} \in A_{\theta} \}$.

The guarantee of coverage is inherent in this construction. The statement "the true parameter value $\theta_{\text{true}}$ is contained in the [confidence interval](@entry_id:138194) $C(X)$" is logically equivalent to the statement "the observed data $X$ fell within the acceptance region $A_{\theta_{\text{true}}}$ for that true parameter." By construction, the probability of the latter is $\ge 1-\alpha$. Therefore, $P(\theta_{\text{true}} \in C(X)) \ge 1-\alpha$ for all $\theta_{\text{true}}$.

In models with discrete data, such as a Poisson counting experiment, it is often impossible to define acceptance regions whose total probability is *exactly* $1-\alpha$. To satisfy the Neyman condition, one must include discrete outcomes until the cumulative probability is *at least* $1-\alpha$. This frequently results in the actual coverage probability being strictly greater than the nominal level for some values of $\theta$. This phenomenon is known as **over-coverage** and is an unavoidable consequence of the discreteness of the sample space .

### Constructing Intervals in Practice

While the Neyman construction provides a universal blueprint, its implementation requires choosing the acceptance regions. This choice, known as an **ordering rule**, determines the properties of the resulting intervals, such as their length and whether they are one-sided or two-sided.

#### Exact Intervals from Pivotal Quantities and CDF Inversion

In some fortunate cases, exact intervals with nominal coverage (i.e., coverage is exactly $1-\alpha$, not just $\ge 1-\alpha$) can be constructed. This is often possible when a **[pivotal quantity](@entry_id:168397)** can be found—a function of the data and the parameter whose [sampling distribution](@entry_id:276447) is independent of the parameter.

A canonical example is the mean $\mu$ of a Gaussian distribution with known variance $\sigma^2$. Given $n$ measurements, the [sample mean](@entry_id:169249) $\bar{X}$ is a [sufficient statistic](@entry_id:173645), and the quantity $Z = \sqrt{n}(\bar{X}-\mu)/\sigma$ is a pivot, as it follows a [standard normal distribution](@entry_id:184509) $\mathcal{N}(0,1)$ regardless of the true value of $\mu$. By finding the values $[-z_{1-\alpha/2}, z_{1-\alpha/2}]$ that contain $1-\alpha$ of the probability for $Z$, we can invert the inequality to obtain the exact $1-\alpha$ [confidence interval](@entry_id:138194) for $\mu$: $[\bar{X} - z_{1-\alpha/2}\frac{\sigma}{\sqrt{n}}, \bar{X} + z_{1-\alpha/2}\frac{\sigma}{\sqrt{n}}]$. In this idealized scenario, the coverage is exactly nominal . However, this ideal is rarely met in high-energy physics, where model uncertainties prevent the construction of perfect pivots.

For [discrete distributions](@entry_id:193344), direct inversion of the [cumulative distribution function](@entry_id:143135) (CDF) provides another path to exact intervals. Consider a Poisson counting experiment observing $n$ events, with unknown mean $\lambda$. The so-called **Garwood interval**, an equal-tailed $1-\alpha$ interval, is constructed by finding the endpoints $[\lambda_L, \lambda_U]$ that satisfy:
$$
P(N \ge n \mid \lambda_L) = \frac{\alpha}{2} \quad \text{and} \quad P(N \le n \mid \lambda_U) = \frac{\alpha}{2}
$$
The first condition defines $\lambda_L$ as the value for which observing $n$ or more events is unlikely (an upward fluctuation), and the second defines $\lambda_U$ as the value for which observing $n$ or fewer is unlikely (a downward fluctuation). These equations can be solved numerically. A crucial identity relates the Poisson sum to the [gamma distribution](@entry_id:138695), allowing the endpoints to be expressed in terms of [quantiles](@entry_id:178417) of the $\chi^2$ distribution :
$$
\lambda_L(n) = \frac{1}{2} F_{\chi^2_{2n}}^{-1}\left(\frac{\alpha}{2}\right) \quad \text{for } n > 0, \quad \text{and} \quad \lambda_L(0) = 0
$$
$$
\lambda_U(n) = \frac{1}{2} F_{\chi^2_{2(n+1)}}^{-1}\left(1 - \frac{\alpha}{2}\right) \quad \text{for } n \ge 0
$$
where $F_{\chi^2_{\nu}}^{-1}(p)$ is the [quantile function](@entry_id:271351) (inverse CDF) of the [chi-square distribution](@entry_id:263145) with $\nu$ degrees of freedom. For instance, for a $90\%$ [confidence level](@entry_id:168001) ($\alpha=0.1$) and observed counts of $n=0, 1,$ and $5$, the intervals $[\lambda_L, \lambda_U]$ are $[0, 2.996]$, $[0.051, 4.744]$, and $[1.970, 10.51]$, respectively .

#### The Challenge of Physical Boundaries and the Unified Approach

A recurring challenge in physics is the presence of physical boundaries, such as a signal strength $\mu$ being non-negative ($\mu \ge 0$). A naive application of central intervals can produce unphysical results (e.g., an interval entirely in the negative region) or lead to the problematic practice of **flip-flopping**: deciding whether to report a two-sided interval or a one-sided upper limit *after* observing the data. For example, an analyst might decide to report an upper limit if the result is a small, non-significant excess, but a two-sided interval if a large excess is seen. This data-dependent choice of procedure violates the premises of the Neyman construction and can lead to under-coverage for certain true values of $\mu$ .

The **Feldman-Cousins unified approach** was developed to solve this problem  . It is a specific implementation of the Neyman construction that uses a single, pre-defined ordering rule based on the [likelihood ratio](@entry_id:170863):
$$
R(n; \mu) = \frac{L(n \mid \mu)}{L(n \mid \hat{\mu}(n))}
$$
Here, $L(n \mid \mu)$ is the likelihood for a hypothesized signal $\mu$, and $L(n \mid \hat{\mu}(n))$ is the likelihood at the best-fit physical signal $\hat{\mu}(n)$ for the given observation $n$. For a Poisson process with mean $\mu+b$, the maximum likelihood estimate is $\hat{\mu}(n) = \max(0, n-b)$. For each $\mu$, the acceptance region $A_\mu$ is built by including outcomes $n$ in decreasing order of $R(n; \mu)$ until the total probability is $\ge 1-\alpha$.

The power of this ordering is that it automatically handles the boundary. When the observation $n$ is large compared to the background $b$, $\hat{\mu}(n)$ is positive, and the ordering rule produces two-sided intervals. When $n$ is small (e.g., $n \le b$), $\hat{\mu}(n)$ saturates at $0$, and the ordering rule naturally produces an acceptance region that, upon inversion, yields a one-sided upper limit. Because the rule is fixed beforehand, the procedure is "unified"—it avoids flip-flopping and guarantees correct coverage across the entire [parameter space](@entry_id:178581), including at the boundary  .

### Asymptotic Methods and Likelihood-Based Intervals

For complex, multi-parameter models, constructing exact intervals is often intractable. In such cases, physicists typically rely on methods based on the asymptotic (large-sample) properties of the [likelihood function](@entry_id:141927).

#### The Profile Likelihood Ratio and Wilks' Theorem

In most realistic analyses, the model depends not only on the parameter of interest $\theta$ but also on a set of **[nuisance parameters](@entry_id:171802)** $\eta$. These are parameters that are necessary to define the model but are not the primary target of inference, such as uncertainties on background rates, luminosity, or detector response .

The standard frequentist technique to handle [nuisance parameters](@entry_id:171802) is **profiling**. For each fixed value of the parameter of interest $\theta$, the likelihood is maximized with respect to all [nuisance parameters](@entry_id:171802). This defines the **[profile likelihood](@entry_id:269700)** function, $L_p(\theta) = \max_{\eta} L(\theta, \eta)$. We then form the **[profile likelihood ratio](@entry_id:753793)**:
$$
\lambda(\theta) = \frac{L(\theta, \hat{\hat{\eta}}(\theta))}{L(\hat{\theta}, \hat{\eta})}
$$
where $(\hat{\theta}, \hat{\eta})$ are the [global maximum](@entry_id:174153) likelihood estimators, and $\hat{\hat{\eta}}(\theta)$ is the value of $\eta$ that maximizes the likelihood for a fixed $\theta$.

The utility of this statistic stems from **Wilks' Theorem**, which states that under certain regularity conditions, the distribution of the test statistic $q_\theta = -2 \ln \lambda(\theta)$ converges to a chi-square ($\chi^2$) distribution as the sample size grows. The number of degrees of freedom is equal to the number of constrained parameters in $\theta$ (for a single scalar parameter, it is $\chi^2_1$) . This powerful theorem holds even in the presence of profiled [nuisance parameters](@entry_id:171802).

This allows for the construction of approximate [confidence intervals](@entry_id:142297). The $1-\alpha$ confidence interval is the set of all $\theta$ values for which $q_\theta$ is less than or equal to the critical value $c$ from the appropriate $\chi^2$ distribution (e.g., for a $90\%$ interval for one parameter, $c$ is the 90th percentile of the $\chi^2_1$ distribution).

A further simplification is the **Wald approximation**, where the log-likelihood is approximated as a parabola around the MLE, $\hat{\theta}$. In this limit, the [test statistic](@entry_id:167372) becomes $q_\theta \approx (\theta - \hat{\theta})^2 / \sigma_{\hat{\theta}}^2$, where $\sigma_{\hat{\theta}}^2$ is the variance of the MLE, obtained from the inverse of the Fisher [information matrix](@entry_id:750640). This provides a simple recipe for an interval: $\hat{\theta} \pm z_{1-\alpha/2} \sigma_{\hat{\theta}}$ .

#### A Critical Failure of Asymptotics: Parameters on a Boundary

The convenience of Wilks' theorem comes with a crucial caveat. The regularity conditions include the requirement that the true parameter value being tested lies in the *interior* of the allowed parameter space. This condition is frequently violated in high-energy physics, particularly when testing for the existence of a new signal. The [null hypothesis](@entry_id:265441) in this case is $\mu=0$, which lies on the boundary of the [physical region](@entry_id:160106) $\mu \ge 0$ .

In this situation, Wilks' theorem does not apply in its standard form. To understand why, consider a simple model where an estimator $x$ follows $\mathcal{N}(\mu, \sigma^2)$, with $\mu \ge 0$. We test the hypothesis $\mu=0$. The [test statistic](@entry_id:167372) is $q_0 = -2 \ln (L(0)/L(\hat{\mu}))$. If the observed $x$ is negative, the best physical fit is $\hat{\mu}=0$, making $q_0=0$. This happens $50\%$ of the time under the [null hypothesis](@entry_id:265441). If $x$ is positive, $\hat{\mu}=x$, and $q_0 = (x/\sigma)^2$, which follows a $\chi^2_1$ distribution. Therefore, the [asymptotic distribution](@entry_id:272575) of $q_0$ is not a pure $\chi^2_1$ but a 50/50 mixture: $\frac{1}{2}\chi^2_0 + \frac{1}{2}\chi^2_1$, where $\chi^2_0$ is a point mass at zero .

This has profound implications. Using the standard $\chi^2_1$ critical value to set an exclusion limit (e.g., requiring $q_0 > c$) would lead to a test with the wrong error rate. For a one-sided $95\%$ limit, the Type I error rate $\alpha$ should be $0.05$. If we used the [mixture distribution](@entry_id:172890), we would need to find $c$ such that $P(q_0 > c) = 0.5 \times P(\chi^2_1 > c) = 0.05$, which implies $P(\chi^2_1 > c) = 0.10$. The correct critical value is therefore the 90th percentile of the $\chi^2_1$ distribution ($c \approx 2.71$), not the 95th percentile ($c \approx 3.84$) . Naively applying Wilks' theorem at a boundary leads to conservative limits that over-cover.

### Advanced Topics in Hypothesis Testing and Limits

#### The $CL_s$ Method for Robust Exclusions

When setting exclusion limits, a standard frequentist test might exclude a [signal hypothesis](@entry_id:137388) simply because the experiment observed a downward fluctuation of the background, even if the experiment had very little sensitivity to the signal in the first place. This is considered an undesirable feature.

The **$CL_s$ method** was introduced to address this issue by modifying the exclusion criterion to be more conservative in regions of low sensitivity . Let $CL_{s+b}$ be the [p-value](@entry_id:136498) for the [signal-plus-background](@entry_id:754818) hypothesis and $CL_b$ be the cumulative probability for the background-only hypothesis, both calculated for the observed data. The $CL_s$ statistic is defined as their ratio:
$$
CL_s = \frac{CL_{s+b}}{CL_b}
$$
A signal is excluded at [confidence level](@entry_id:168001) $1-\alpha$ if $CL_s \le \alpha$.

The intuition is that $CL_b = P(\text{data as or less signal-like than observed} \mid b)$ acts as a guard. If the experiment observes a downward fluctuation (e.g., fewer events than expected from background), $CL_b$ will be small. This inflates $CL_s$, making it harder to satisfy the exclusion criterion. For example, observing $n=1$ event when $b=5$ is expected is a significant downward fluctuation. This yields a small $CL_{s+b}$ but also a small $CL_b$, and the resulting $CL_s$ can be large enough to prevent exclusion . In contrast, if the experiment has good sensitivity and the observation is consistent with the background-only hypothesis, $CL_b$ will be close to 1, and the test effectively reduces to the standard $CL_{s+b} \le \alpha$ criterion . The $CL_s$ method is explicitly conservative (it over-covers), sacrificing some statistical power to ensure the robustness of its exclusions.

#### Multiple Testing and the Look-Elsewhere Effect

Many searches in high-energy physics are not targeted at a single, pre-defined [signal hypothesis](@entry_id:137388) but involve scanning over a continuous parameter, such as the mass of a hypothetical particle. This practice of performing many hypothesis tests simultaneously gives rise to the **[look-elsewhere effect](@entry_id:751461) (LEE)** .

The LEE is a manifestation of the [multiple testing problem](@entry_id:165508): if you look in enough places, you are bound to find a statistical fluctuation. The significance of an excess observed at some point in a scan cannot be judged by its **[local p-value](@entry_id:751406)** (the p-value it would have if that point had been the only one tested). One must instead calculate the **[global p-value](@entry_id:749928)**: the probability that at least one point in the entire search range would show a fluctuation as large or larger than the one observed, under the global background-only hypothesis.

For $N_{\text{eff}}$ independent tests, the relationship is $p_{\text{glob}} = 1 - (1-p_{\text{loc}})^{N_{\text{eff}}}$. A [local p-value](@entry_id:751406) that seems very small can correspond to a large, non-significant [global p-value](@entry_id:749928). For example, a local significance of $Z=3.0$ ($p_{\text{loc}} \approx 1.35 \times 10^{-3}$) can become a [global p-value](@entry_id:749928) of $p_{\text{glob}} \approx 0.18$ when scanning over $N_{\text{eff}}=150$ effective independent positions, rendering the excess statistically insignificant .

Similarly, when setting exclusion limits across a mass range, one must correct the significance threshold to control the **[family-wise error rate](@entry_id:175741) (FWER)**—the probability of making at least one false exclusion anywhere in the range. To maintain a global FWER of $\alpha$, the [local p-value](@entry_id:751406) threshold for exclusion, $p_{\text{loc}}^\ast$, must be made more stringent. A common approach is the Bonferroni correction, $p_{\text{loc}}^\ast \le \alpha / N_{\text{eff}}$, or the slightly less conservative Šidák correction, $p_{\text{loc}}^\ast \le 1 - (1-\alpha)^{1/N_{\text{eff}}}$ .

### Handling Nuisance Parameters: A Philosophical Divide

The treatment of [nuisance parameters](@entry_id:171802) exposes a deep philosophical division between frequentist and Bayesian statistics.

The frequentist approach, as we have seen, is **profiling**. Nuisance parameters are treated as unknown constants. Their values are optimized away for each hypothesis test on the parameter of interest. The resulting confidence intervals have guaranteed (or asymptotically guaranteed) [frequentist coverage](@entry_id:749592), but their construction can be complex, and asymptotic approximations may fail, particularly at boundaries .

The Bayesian approach is **[marginalization](@entry_id:264637)**. Nuisance parameters are treated as random variables, assigned a [prior probability](@entry_id:275634) distribution $\pi(\eta)$, and integrated out of the joint [posterior distribution](@entry_id:145605) to yield a marginal posterior for the parameter of interest, $p(\theta | \text{data}) = \int p(\theta, \eta | \text{data}) d\eta$. From this, one can derive a credible interval.

While computationally elegant, it is crucial to recognize that a Bayesian credible interval comes with no general guarantee of [frequentist coverage](@entry_id:749592) . The resulting interval and its coverage properties are contingent on the choice of prior. If a chosen prior for a [nuisance parameter](@entry_id:752755) is overly restrictive and centered far from the true value, it can bias the inference on the parameter of interest and lead to severe under-coverage, even if the underlying physics model is correct . The choice between these two paradigms involves a trade-off between the philosophical guarantees of coverage and the practicalities of implementation and prior specification.