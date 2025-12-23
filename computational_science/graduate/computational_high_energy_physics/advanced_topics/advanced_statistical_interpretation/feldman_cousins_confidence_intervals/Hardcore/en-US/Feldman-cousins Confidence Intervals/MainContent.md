## Introduction
Estimating parameters from experimental data is a fundamental task in science, with frequentist [confidence intervals](@entry_id:142297) serving as a cornerstone of statistical reporting, particularly in high-energy physics. However, traditional methods for constructing these intervals often fail when dealing with parameters that have physical boundaries, such as a signal strength that cannot be negative. This limitation can lead to unphysical results or the statistically unsound practice of "flip-flopping," where the analysis procedure is chosen after observing the data, compromising the crucial guarantee of [frequentist coverage](@entry_id:749592).

This article presents a comprehensive exploration of the Feldman-Cousins method, a unified approach that rigorously resolves these challenges. In the following chapters, you will gain a deep understanding of this powerful statistical tool. "Principles and Mechanisms" will dissect the theoretical foundations, starting from the Neyman construction and detailing the likelihood-ratio ordering principle that is the heart of the Feldman-Cousins technique. "Applications and Interdisciplinary Connections" will demonstrate the method's versatility by exploring its use in core physics analyses, its extension to models with [systematic uncertainties](@entry_id:755766), and its relevance to other scientific fields. Finally, "Hands-On Practices" will provide opportunities to solidify your knowledge by applying these concepts to practical problems. By the end, you will be equipped to construct and interpret Feldman-Cousins intervals, ensuring your statistical results are robust, meaningful, and rigorously correct.

## Principles and Mechanisms

This chapter delves into the principles and mechanisms that underpin the construction of frequentist confidence intervals, with a particular focus on the unified approach developed by Feldman and Cousins. We will begin by reviewing the foundational Neyman construction, articulate the challenges posed by physical parameter boundaries, and then systematically dissect the Feldman-Cousins likelihood-ratio ordering principle. We will explore how this principle provides a rigorous and unified solution, examining its theoretical properties and the practical steps for its implementation.

### The Neyman Construction and the Guarantee of Coverage

The primary objective of many statistical analyses in experimental physics is to report an interval estimate for an unknown parameter $\theta$ that is inferred from observed data $X$. In the frequentist paradigm, the definitive method for constructing such intervals is the **Neyman construction**. Its power lies in providing a strict guarantee about the long-run performance of the procedure.

This performance guarantee is known as **[frequentist coverage](@entry_id:749592)**. For a procedure that produces a confidence set $C(X)$ for a parameter $\theta$ at a [confidence level](@entry_id:168001) of $1-\alpha$, the coverage property is formally defined by the requirement that the probability of the set containing the true, fixed value of the parameter is at least $1-\alpha$. This must hold for every possible value of $\theta$ in the parameter space $\Theta$. Mathematically, this is expressed as:
$$
P_{\theta}(\theta \in C(X)) \ge 1-\alpha \quad \text{for all } \theta \in \Theta
$$
Here, $X$ is the random variable representing the outcome of the experiment, making the confidence set $C(X)$ a random entity. The probability $P_{\theta}$ is calculated using the probability distribution of $X$ given the true parameter value $\theta$ . The inequality ensures the procedure can be applied to [discrete distributions](@entry_id:193344), where exact equality may not be possible.

The Neyman construction achieves this coverage guarantee through a two-step process involving the concept of **acceptance regions** :

1.  **Construction of the Confidence Belt**: For *each* possible value of the parameter $\theta \in \Theta$, we define an **acceptance region** $A(\theta)$ in the space of possible data outcomes $\mathcal{X}$. This region is a pre-specified set of data outcomes that are considered "compatible" with the hypothesis that the true parameter value is $\theta$. The region is constructed such that the probability of the data falling within it, calculated under the assumption that $\theta$ is the true value, is at least $1-\alpha$:
    $$
    P_{\theta}(X \in A(\theta)) \ge 1-\alpha
    $$
    The collection of all such acceptance regions, $\{A(\theta) \mid \theta \in \Theta\}$, forms what is known as the **confidence belt**.

2.  **Inversion to obtain the Confidence Interval**: After performing the experiment and observing a specific outcome $x_{\text{obs}}$, the [confidence interval](@entry_id:138194) (or set) $C(x_{\text{obs}})$ is formed by collecting all parameter values $\theta$ for which the observed outcome $x_{\text{obs}}$ is contained within their respective acceptance regions.
    $$
    C(x_{\text{obs}}) = \{\theta \in \Theta \mid x_{\text{obs}} \in A(\theta)\}
    $$

The guarantee of coverage follows directly from this duality. The event "the true parameter $\theta$ is in the confidence set $C(X)$" is logically equivalent to the event "the observed data $X$ is in the acceptance region $A(\theta)$". Therefore, their probabilities are equal: $P_{\theta}(\theta \in C(X)) = P_{\theta}(X \in A(\theta))$. Since the acceptance regions were constructed to satisfy $P_{\theta}(X \in A(\theta)) \ge 1-\alpha$, the resulting confidence sets are guaranteed to have at least the nominal coverage $1-\alpha$. This connection between a family of hypothesis tests (defined by the acceptance regions) and the resulting confidence interval is a cornerstone of [frequentist inference](@entry_id:749593) .

A critical point of freedom in the Neyman construction is the choice of which data outcomes to include in the acceptance region $A(\theta)$. This choice is governed by an **ordering principle**, which ranks all possible outcomes for a given $\theta$. Different ordering principles lead to intervals with different properties, and a poor choice can lead to unhelpful or even misleading results.

### The Challenge of Physical Boundaries: Flip-Flopping and Undercoverage

In high-energy physics, many parameters of interest are physically constrained. A prominent example is the search for a new signal, where the signal strength parameter, let's call it $s$, cannot be negative ($s \ge 0$). Suppose an experiment counts events, $n$, which arise from both the signal $s$ and a known background source $b$. The total expected number of events is $\mu = s+b$, and the observation $n$ is modeled as a draw from a Poisson distribution, $n \sim \mathrm{Poisson}(s+b)$.

Traditional ordering principles, such as those used to construct **central intervals** where equal probabilities are excluded from the upper and lower tails of the distribution $P(n \mid s,b)$, encounter significant problems near the physical boundary $s=0$. If the observed count $n$ is less than the expected background $b$, a central interval for the total mean $\mu$ might be entirely above $n$. When one subtracts $b$ to get an interval for $s$, the result could be an [empty set](@entry_id:261946) or an interval that excludes the physically allowed value $s=0$. This is clearly an undesirable outcome.

This led to a common but problematic practice known as **"flip-flopping"** . Faced with an unphysical result from a central interval construction, an analyst might decide, *after* seeing the data, to switch procedures and instead report a one-sided upper limit on the signal. For example, the analyst might pre-plan to report a two-sided interval if the result is "significant" (e.g., $n$ is much larger than $b$), but switch to reporting an upper limit if the result is "not significant" ($n$ is close to or less than $b$).

This data-dependent choice of procedure violates the core tenet of the frequentist paradigm. The statistical procedure, including the complete specification of the confidence belt, must be defined *before* the data is observed. A procedure that involves a "flip-flop" is, in fact, a hybrid procedure whose coverage properties must be evaluated as a whole. When this is done, it is found that such procedures can severely under-cover for certain values of the true parameter $s$. That is, the actual probability of the interval containing the true value of $s$ can be significantly less than the nominal [confidence level](@entry_id:168001) $1-\alpha$. This is because the ad-hoc switch effectively removes certain outcomes from the acceptance region that should have been included, breaking the integrity of the Neyman construction. The Feldman-Cousins method was developed specifically to provide a **unified approach** that resolves this issue.

### The Feldman-Cousins Ordering Principle

The Feldman-Cousins (FC) construction is a specific implementation of the Neyman method that employs a powerful and principled ordering rule based on a **likelihood ratio**. This rule provides a unified framework that gracefully handles physical boundaries and automatically generates either upper limits or two-sided intervals as appropriate, without any ad-hoc decisions and while rigorously maintaining [frequentist coverage](@entry_id:749592)  .

For a given hypothesis for the parameter of interest, $\theta$, the FC method ranks every possible observable outcome $x$ according to the [likelihood ratio](@entry_id:170863) $R(x; \theta)$:
$$
R(x; \theta) \equiv \frac{\mathcal{L}(\theta \mid x)}{\mathcal{L}(\hat{\theta}(x) \mid x)}
$$
Let's dissect this crucial expression :

*   The numerator, $\mathcal{L}(\theta \mid x)$, is the likelihood function evaluated at the parameter value $\theta$ being tested. It quantifies how well the hypothesis $\theta$ explains the observed data $x$.

*   The denominator, $\mathcal{L}(\hat{\theta}(x) \mid x)$, is the [likelihood function](@entry_id:141927) evaluated at the parameter value $\hat{\theta}(x)$ that *best* explains the data $x$. This $\hat{\theta}(x)$ is the **Maximum Likelihood Estimate (MLE)** of $\theta$ for the given observation $x$. By definition of the MLE, this denominator is the maximum possible value of the [likelihood function](@entry_id:141927) for the observed data $x$.

A crucial element of the FC method is that the maximization is performed over the *physically allowed* [parameter space](@entry_id:178581). For our Poisson signal example where $s \ge 0$, the MLE for the signal strength $s$ given an observation $n$ is not simply $n-b$ (which could be negative), but the **constrained MLE** :
$$
\hat{s}(n) = \max(0, n-b)
$$
This direct incorporation of the physical boundary into the ordering principle is the key to the method's success.

The ratio $R(x; \theta)$, which must lie between $0$ and $1$, quantifies how plausible the hypothesis $\theta$ is relative to the most plausible explanation for the data $x$. Outcomes $x$ with a large value of $R(x; \theta)$ are those for which the hypothesis $\theta$ is "less surprising" or "more compatible", as it explains the data nearly as well as the best-fit hypothesis. The FC procedure builds the acceptance region $A(\theta)$ by including outcomes in descending order of $R(x; \theta)$ until the total probability meets or exceeds the [confidence level](@entry_id:168001) $1-\alpha$.

### The Mechanism of Unified Intervals

The brilliance of the likelihood-ratio ordering is how it automatically causes the resulting [confidence intervals](@entry_id:142297) to adapt their form. To see this mechanism clearly, consider a simplified model where an observation $x$ is drawn from a Gaussian distribution with unknown mean $\mu \ge 0$ and known standard deviation $\sigma$, i.e., $x \sim \mathcal{N}(\mu, \sigma^2)$ .

The constrained MLE for $\mu$ is $\hat{\mu}(x) = \max(0, x)$. The likelihood is $L(x \mid \mu) \propto \exp(-\frac{(x-\mu)^2}{2\sigma^2})$. The ordering statistic is therefore equivalent to ranking by $-2\ln R(x \mid \mu)$, which simplifies to:
$$
-2\ln R(x \mid \mu) = \frac{(x-\mu)^2 - (x-\hat{\mu}(x))^2}{\sigma^2}
$$
Let's analyze the construction of the acceptance region for the boundary hypothesis $\mu=0$. The ordering statistic becomes:
$$
-2\ln R(x \mid 0) = \frac{x^2 - (x-\max(0,x))^2}{\sigma^2} = \begin{cases} x^2/\sigma^2  \text{if } x \ge 0 \\ 0  \text{if } x \lt 0 \end{cases}
$$
To form the acceptance region $A(0)$, we must include outcomes with the smallest values of this statistic first. The absolute minimum value is $0$, which occurs for all $x \le 0$. Thus, all non-positive values of $x$ are ranked as most compatible with the hypothesis $\mu=0$ and are the first to be included in $A(0)$. To reach a total probability of $1-\alpha$, we must also include a range of positive $x$ values, starting from $x=0$ and moving outwards. The result is that the acceptance region $A(0)$ is a one-sided interval of the form $(-\infty, x_{\text{high}}]$.

Now, consider the inversion step. If we observe a value $x_{\text{obs}} \le 0$, it is guaranteed to be in the acceptance region $A(0)$. Therefore, by the definition of the Neyman construction, the value $\mu=0$ must be in the confidence interval for $x_{\text{obs}}$. Since the [parameter space](@entry_id:178581) is constrained to $\mu \ge 0$, the resulting interval must have a lower endpoint of $0$. It will be of the form $[0, \mu_{\text{upper}}]$—a one-sided upper limit.

As the observation $x_{\text{obs}}$ becomes large and positive, the best-fit parameter $\hat{\mu}(x_{\text{obs}}) = x_{\text{obs}}$ is far from the boundary. In this regime, the ordering principle behaves similarly to that of a central interval, and the resulting confidence interval for $\mu$ becomes two-sided, $[ \mu_{\text{lower}}, \mu_{\text{upper}} ]$ with $\mu_{\text{lower}} > 0$. The Feldman-Cousins procedure thus provides a single, unified prescription that smoothly transitions from upper limits to two-sided intervals, driven entirely by the data and the underlying [likelihood principle](@entry_id:162829) .

### Theoretical Properties and Practical Implementation

The Feldman-Cousins method possesses several important theoretical properties and practical features.

#### Duality with Hypothesis Testing and Optimality

As an implementation of the Neyman construction, the FC method has a direct duality with [hypothesis testing](@entry_id:142556) . The [confidence interval](@entry_id:138194) produced for an observation $x_{\text{obs}}$ is precisely the set of all parameter values $\mu_0$ for which the [null hypothesis](@entry_id:265441) $H_0: \mu = \mu_0$ is *not* rejected at [significance level](@entry_id:170793) $\alpha$. The test statistic used is the generalized likelihood ratio. The theory of [hypothesis testing](@entry_id:142556), originating with the Neyman-Pearson lemma, provides powerful arguments for the optimality of likelihood-ratio based tests. For the two-sided testing problem inherent in interval construction, where a Uniformly Most Powerful (UMP) test does not generally exist, the goal shifts to finding a Uniformly Most Powerful Unbiased (UMPU) test. For [exponential families](@entry_id:168704) like the Poisson distribution, the generalized [likelihood-ratio test](@entry_id:268070) is known to be closely related to the UMPU test, providing a strong theoretical justification for its optimality .

#### Conservative Coverage for Discrete Distributions

When dealing with discrete data, such as counts from a Poisson distribution, the total probability in an acceptance region, $\sum_{x \in A(\theta)} P(x|\theta)$, increases in discrete jumps as more outcomes are added. It is generally impossible to make this sum *exactly* equal to the nominal [confidence level](@entry_id:168001) $1-\alpha$. To satisfy the fundamental coverage guarantee of the Neyman construction, one must include outcomes until the cumulative probability first meets or *exceeds* $1-\alpha$. As a result, for most values of $\theta$, the true coverage probability will be strictly greater than $1-\alpha$. This phenomenon is known as **conservative coverage** or **over-coverage**, and it is an inherent and unavoidable feature of non-randomized interval constructions for [discrete distributions](@entry_id:193344)  .

#### Reparameterization Invariance

An elegant property of the FC method is its invariance under [reparameterization](@entry_id:270587) of the parameter of interest. The likelihood ratio $R(x; \theta)$ is invariant under any [one-to-one transformation](@entry_id:148028) of the parameter, $\theta' = g(\theta)$. This is because the MLE is equivariant, i.e., $\hat{\theta}'(x) = g(\hat{\theta}(x))$. This invariance of the ordering statistic means that the acceptance regions are consistently defined, and the resulting confidence intervals transform correctly. For example, constructing an interval for a parameter $\theta$ and then mapping that interval to the space of $\theta'$ yields the same result as directly constructing the interval for $\theta'$ from the outset .

#### Algorithmic Construction

In practice, the Feldman-Cousins confidence belt is constructed numerically. The procedure can be summarized by the following algorithm  :

1.  Define a sufficiently fine grid of points $\mu_i$ in the [parameter space](@entry_id:178581) of interest (e.g., for the signal $s \ge 0$).
2.  For each $\mu_i$, consider a sufficiently wide range of possible integer outcomes $n \in \{0, 1, \dots, n_{\max}\}$.
3.  For each outcome $n$, calculate the constrained MLE, $\hat{s}(n) = \max(0, n-b)$.
4.  For each pair $(\mu_i, n)$, compute the likelihood-ratio ordering statistic $R(n; \mu_i) = \frac{P(n \mid \mu_i+b)}{P(n \mid \hat{s}(n)+b)}$.
5.  For each $\mu_i$, sort the outcomes $n$ in descending order of $R(n; \mu_i)$.
6.  Construct the acceptance region $A(\mu_i)$ by adding the sorted outcomes $n$ and summing their probabilities $P(n \mid \mu_i+b)$ until the sum first meets or exceeds $1-\alpha$. Any ties in the rank-ordering are resolved by including all tied outcomes .
7.  Store the set of acceptance regions $\{A(\mu_i)\}$. This is the numerical confidence belt.
8.  Given an experimental observation $n_{\text{obs}}$, the confidence interval is found by identifying all $\mu_i$ for which $n_{\text{obs}} \in A(\mu_i)$. The endpoints of the interval can be found by interpolation between the grid points.

By adhering to this rigorous, pre-defined procedure, the Feldman-Cousins method provides a powerful and theoretically sound tool for physicists to report confidence intervals that are physically meaningful, statistically robust, and free from the ambiguities and undercoverage issues that plagued previous ad-hoc approaches.