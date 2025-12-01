## Introduction
Estimating the true proportion of a characteristic within a population—be it the prevalence of a disease, the success rate of a treatment, or the frequency of a genetic marker—is a fundamental task in biostatistics and many other empirical sciences. While the [sample proportion](@entry_id:264484) provides a single best guess, it offers no insight into the uncertainty of the estimate. This knowledge gap is critical, as decisions in public health, engineering, and policy often depend on understanding the range of plausible values for the true parameter.

This article addresses the challenge of quantifying this uncertainty by providing a thorough guide to confidence intervals for a population proportion. You will learn not only how to construct these intervals but also how to interpret them correctly and, crucially, how to avoid common pitfalls associated with standard methods.

The article is structured to build your expertise progressively. In "Principles and Mechanisms," we will derive the common Wald interval from first principles, explore its significant flaws, and introduce the more robust Wilson (Score) and Agresti-Coull intervals that are preferred in modern practice. Next, "Applications and Interdisciplinary Connections" will demonstrate how these statistical tools are applied in diverse fields like epidemiology and quality control, and how they are adapted for the complexities of real-world data, including complex survey designs and measurement error. Finally, "Hands-On Practices" will give you the opportunity to apply these concepts through targeted exercises, solidifying your ability to calculate, compare, and plan studies using these essential methods. We begin by exploring the core statistical principles that form the foundation of this topic.

## Principles and Mechanisms

This chapter delves into the fundamental principles and statistical mechanisms that underpin the construction and interpretation of confidence intervals for a population proportion. We will begin by formalizing the estimation problem, proceed to derive the most common type of confidence interval, analyze its significant limitations, and finally, introduce more robust and theoretically sound alternatives that are preferred in modern biostatistical practice.

### The Estimation Framework: Proportions and Their Estimators

In many biostatistical applications, we are interested in a [binary outcome](@entry_id:191030) within a population: a patient has a disease or does not, a new drug is effective or is not, an individual possesses a specific genetic marker or does not. The parameter of central interest is the **population proportion**, denoted by $p$, which represents the true fraction of individuals in the entire population who exhibit the characteristic of interest.

To estimate $p$, we draw a sample of size $n$ from the population. For each individual $i$ in the sample, we record a binary outcome, which can be represented by an [indicator variable](@entry_id:204387) $X_i$. We set $X_i=1$ if the characteristic is present (a "success") and $X_i=0$ if it is absent (a "failure"). If the sample is drawn randomly from a large population, we can model each $X_i$ as an independent random variable following a Bernoulli distribution with parameter $p$. This means that for any individual, the probability of having the characteristic is $p$, or $\mathbb{P}(X_i=1) = p$, and the probability of not having it is $\mathbb{P}(X_i=0) = 1-p$. The expected value of a single observation is therefore $\mathbb{E}[X_i] = 1 \cdot p + 0 \cdot (1-p) = p$. [@problem_id:4902727]

The natural estimator for the population proportion $p$ is the **[sample proportion](@entry_id:264484)**, denoted by $\hat{p}$. It is calculated as the fraction of successes observed in the sample:

$$
\hat{p} = \frac{\sum_{i=1}^{n} X_i}{n}
$$

This estimator is not only intuitive but also possesses the desirable property of being **unbiased**. This means that, on average, the [sample proportion](@entry_id:264484) will equal the true population proportion. We can demonstrate this by taking the expectation of $\hat{p}$ over all possible random samples:

$$
\mathbb{E}[\hat{p}] = \mathbb{E}\left[\frac{1}{n}\sum_{i=1}^{n} X_i\right] = \frac{1}{n}\sum_{i=1}^{n}\mathbb{E}[X_i] = \frac{1}{n}\sum_{i=1}^{n}p = \frac{np}{n} = p
$$

The sum of these independent and identically distributed (i.i.d.) Bernoulli trials, $X = \sum_{i=1}^{n} X_i$, which represents the total count of successes in the sample, follows a **Binomial distribution**, denoted $X \sim \mathrm{Bin}(n,p)$. This model is justified under several key assumptions: the number of trials ($n$) is fixed, each trial is binary, the probability of success ($p$) is constant for all trials, and the trials are independent. In practice, when we perform [simple random sampling](@entry_id:754862) *without* replacement from a large finite population, the trials are not perfectly independent. However, as long as the sample size $n$ is a small fraction of the total population size (e.g., less than 5%), the dependence is negligible, and the binomial model serves as an excellent and standard approximation. [@problem_id:4902771]

### The Frequentist Interpretation of a Confidence Interval

While $\hat{p}$ is our best point estimate for $p$, it is almost certain to not be exactly equal to the true value. A single [point estimate](@entry_id:176325) provides no information about the uncertainty associated with it. A **confidence interval (CI)** addresses this by providing a range of plausible values for the unknown parameter $p$.

Formally, a $100(1-\alpha)\%$ confidence interval is the output of a procedure, let's call it $C$, which takes the random data (represented by $X$) and produces a random interval, $C(X)$. The defining property of this procedure is its **coverage probability**: the probability that the random interval it produces will contain the true, fixed parameter $p$. In the frequentist paradigm, a procedure is considered valid if its coverage probability is at least the nominal level $1-\alpha$ for *every possible value* of the parameter $p$. This is a stringent requirement, expressed mathematically as:

$$
\inf_{p \in (0,1)} \mathbb{P}_{p}\{ p \in C(X) \} \ge 1-\alpha
$$

Here, $\mathbb{P}_{p}$ denotes that the probability is calculated assuming the true parameter value is $p$, and the [infimum](@entry_id:140118) signifies that we consider the worst-case performance across the entire parameter space. [@problem_id:4902742]

This formal definition leads to a very specific interpretation. A confidence level of, say, 95% does **not** mean there is a 95% probability that the true parameter $p$ lies within a *particular, calculated interval*, such as $(0.55, 0.65)$. Once an interval is calculated from data, both the interval and the true parameter $p$ are fixed; $p$ is either in the interval or it is not. The probability is 0 or 1. [@problem_id:1907079]

The correct **[frequentist interpretation](@entry_id:173710)** is a statement about the long-run performance of the procedure itself: If we were to repeat our study many times, drawing a new random sample of the same size each time and calculating a new 95% confidence interval from each sample, we would expect approximately 95% of these calculated intervals to capture the true, fixed population proportion $p$. The confidence is in the reliability of the method over many hypothetical repetitions, not in any single outcome. [@problem_id:1907052]

### The Wald Interval: A First-Principles Construction

The most common method for constructing a confidence interval for a proportion relies on the **Central Limit Theorem (CLT)**. The CLT states that for a sufficiently large sample size $n$, the sampling distribution of the sample proportion $\hat{p}$ is approximately normal. The mean of this distribution is $p$, and its variance is:

$$
\mathrm{Var}(\hat{p}) = \mathrm{Var}\left(\frac{1}{n}\sum_{i=1}^{n} X_i\right) = \frac{1}{n^2}\sum_{i=1}^{n}\mathrm{Var}(X_i) = \frac{n p(1-p)}{n^2} = \frac{p(1-p)}{n}
$$

The standard deviation of an estimator's sampling distribution is called its **[standard error](@entry_id:140125) (SE)**. Therefore, the true standard error of $\hat{p}$ is:

$$
\mathrm{SE}(\hat{p}) = \sqrt{\frac{p(1-p)}{n}}
$$

This expression shows that the statistical uncertainty in our estimator $\hat{p}$ decreases as the sample size $n$ increases, specifically scaling with $n^{-1/2}$. This implies that the width of a confidence interval will also be proportional to $n^{-1/2}$. To cut the interval width in half, one must quadruple the sample size—a crucial consideration in study design. [@problem_id:4902749]

The [standard error](@entry_id:140125) formula depends on the unknown parameter $p$, presenting a challenge. The standard approach, known as the **Wald method**, is to substitute the [sample proportion](@entry_id:264484) $\hat{p}$ for the unknown $p$ in the [standard error](@entry_id:140125) formula. This yields the **estimated [standard error](@entry_id:140125)**:

$$
\widehat{\mathrm{SE}}(\hat{p}) = \sqrt{\frac{\hat{p}(1-\hat{p})}{n}}
$$

This "plug-in" substitution is justified by [asymptotic theory](@entry_id:162631). By the Law of Large Numbers, $\hat{p}$ is a [consistent estimator](@entry_id:266642) for $p$ (it converges in probability to $p$ as $n \to \infty$). Slutsky's Theorem then allows us to replace the true standard error with this consistent estimate in the standardized statistic without changing its [limiting distribution](@entry_id:174797). [@problem_id:4902704]

We can now construct the interval. We form an approximate [pivotal quantity](@entry_id:168397) that follows a [standard normal distribution](@entry_id:184509):

$$
\frac{\hat{p} - p}{\widehat{\mathrm{SE}}(\hat{p})} = \frac{\hat{p} - p}{\sqrt{\hat{p}(1-\hat{p})/n}} \approx \mathcal{N}(0,1)
$$

For a $100(1-\alpha)\%$ confidence interval, we find the critical value $z_{\alpha/2}$ from the standard normal distribution (e.g., $z_{0.025} \approx 1.96$ for a 95% CI). The interval is formed by taking all values of $p$ that are not rejected by a two-sided test at level $\alpha$:

$$
\hat{p} \pm z_{\alpha/2} \times \widehat{\mathrm{SE}}(\hat{p})
$$

This gives the well-known formula for the **Wald confidence interval**:

$$
\left( \hat{p} - z_{\alpha/2} \sqrt{\frac{\hat{p}(1-\hat{p})}{n}}, \quad \hat{p} + z_{\alpha/2} \sqrt{\frac{\hat{p}(1-\hat{p})}{n}} \right)
$$

### Pathologies of the Wald Interval

Despite its widespread use due to its simplicity, the Wald interval suffers from severe theoretical and practical deficiencies, particularly with small to moderate sample sizes or when the true proportion $p$ is near 0 or 1.

The primary reason for its failure is that the [normal approximation](@entry_id:261668) to the [binomial distribution](@entry_id:141181) is poor when the distribution is not symmetric. The [binomial distribution](@entry_id:141181) is symmetric only when $p=0.5$; as $p$ approaches the boundaries of 0 or 1, the distribution becomes highly **skewed**. A symmetric normal curve is then a very poor fit. The skewness of the standardized binomial count can be shown to be $\frac{1-2p}{\sqrt{np(1-p)}}$. For the [normal approximation](@entry_id:261668) to be reliable, this [skewness](@entry_id:178163) must be small, which requires the denominator term $np(1-p)$ to be sufficiently large. This leads to common **rules of thumb**, such as requiring the expected number of successes and failures to be at least 10 (i.e., $n\hat{p} \ge 10$ and $n(1-\hat{p}) \ge 10$). [@problem_id:4902702]

The practical consequences of these failures are stark. Most notably, the Wald interval can produce endpoints that are outside the valid parameter space of $[0, 1]$. For instance, in a study with $n=20$ subjects, observing just one success ($x=1$) gives $\hat{p}=0.05$. A 95% Wald CI would be $0.05 \pm 1.96 \sqrt{0.05(0.95)/20}$, which calculates to $(-0.046, 0.146)$. A negative proportion is nonsensical. Similarly, observing 19 successes gives a CI of $(0.854, 1.046)$, with an upper bound exceeding 1. [@problem_id:4902731]

A common but misguided "fix" is to simply truncate the interval, for example, reporting $[0, 0.146]$ in the first case. However, this is a purely cosmetic change. The coverage probability of an interval is determined by the set of sample outcomes for which the calculated interval contains the true parameter $p$. Since the true $p$ must be in $[0,1]$, the condition that $p$ is in the original Wald interval is logically equivalent to the condition that $p$ is in the truncated interval. Therefore, **truncation does not change the coverage probability at all**. It does not fix the underlying poor performance of the procedure. [@problem_id:4902731] Another critical failure occurs when we observe 0 or $n$ successes. In this case, $\hat{p}(1-\hat{p})=0$, and the Wald interval collapses to a zero-width interval $[\hat{p}, \hat{p}]$. This absurdly implies perfect certainty and guarantees non-coverage if the true $p$ is merely close to, but not exactly, 0 or 1.

### A Principled Alternative: The Wilson (Score) Interval

The core flaw of the Wald interval stems from the "plug-in" estimation of the standard error. A more principled approach avoids this by returning to the [pivotal quantity](@entry_id:168397) *before* the substitution:

$$
Z = \frac{\hat{p} - p}{\sqrt{p(1-p)/n}}
$$

This is known as the **score pivot**, as it is derived from Rao's [score test](@entry_id:171353). The **Wilson score interval** is constructed by finding all values of $p$ for which this statistic is within the critical values $\pm z_{\alpha/2}$:

$$
\left| \frac{\hat{p} - p}{\sqrt{p(1-p)/n}} \right| \le z_{\alpha/2}
$$

Solving this inequality for $p$ requires solving a quadratic equation. While algebraically more complex, the resulting interval has vastly superior statistical properties. It is always contained within $(0,1)$ and does not produce zero-width intervals at the boundaries.

The theoretical superiority of the score interval can be shown more formally. A Taylor series expansion reveals that the Wald pivot ($T_W$) is systematically distorted relative to the score pivot ($Z$):

$$
T_W \approx Z - \left( \frac{1-2p}{2\sqrt{p(1-p)}} \right) \frac{Z^2}{\sqrt{n}}
$$

The Wald pivot contains an additional error term of order $n^{-1/2}$ that is not present in the score pivot. The coefficient of this error term explodes as $p$ approaches 0 or 1, explaining why the Wald interval's performance degrades so dramatically at the boundaries. By using the true parameter $p$ in the [standard error](@entry_id:140125), the score interval avoids this source of distortion, leading to coverage probabilities that are much closer to the nominal $1-\alpha$ level and far more uniform across the entire range of $p$. [@problem_id:4902762]

### A Practical and Accurate Alternative: The Agresti-Coull Interval

While the Wilson score interval is theoretically excellent, the need to solve a quadratic equation makes it less convenient for quick calculations. Fortunately, a simple adjustment to the Wald formula yields an interval with performance nearly as good as the Wilson interval. This is the **Agresti-Coull interval**.

The procedure for a 95% CI is remarkably simple: one "adds two successes and two failures" to the data before computing a Wald-style interval. Specifically, we define an adjusted [sample proportion](@entry_id:264484) $\tilde{p}$ and an adjusted sample size $\tilde{n}$:

$$
\tilde{p} = \frac{x+2}{n+4}, \quad \tilde{n} = n+4
$$

The Agresti-Coull interval is then given by the simple Wald formula using these adjusted values:

$$
\tilde{p} \pm z_{0.025} \sqrt{\frac{\tilde{p}(1-\tilde{p})}{\tilde{n}}}
$$

This procedure may seem arbitrary, but it has a deep justification. The center of the Wilson interval can be shown to be $\frac{x + z_{\alpha/2}^2/2}{n + z_{\alpha/2}^2}$. This is a "shrinkage" estimator that pulls the raw sample proportion $\hat{p}$ towards the center value of $0.5$. The Agresti-Coull method, by adding a number of pseudo-observations (for a 95% CI, $z_{0.025}^2 \approx 4$, so we add $z_{0.025}^2/2=2$ successes and 2 failures), creates an adjusted proportion $\tilde{p}$ that is an excellent approximation of the Wilson interval's center. Because its center is purposefully designed to mimic the theoretically superior Wilson interval, the Agresti-Coull interval inherits its excellent coverage properties while retaining the computational simplicity of the Wald formula. It is for this reason that it is widely recommended for general use. [@problem_id:4902765]