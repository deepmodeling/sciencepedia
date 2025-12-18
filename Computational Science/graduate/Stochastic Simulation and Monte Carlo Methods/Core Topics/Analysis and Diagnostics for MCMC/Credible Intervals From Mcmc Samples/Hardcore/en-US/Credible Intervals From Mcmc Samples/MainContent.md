## Introduction
In Bayesian statistics, the posterior distribution represents the totality of our knowledge about a parameter after observing data. While powerful, this full distribution often needs to be summarized into a more digestible form, like an interval, to facilitate interpretation and decision-making. When using Markov chain Monte Carlo (MCMC) methods, we are left with a large, but finite and often autocorrelated, sample from this posterior. This raises a critical question: how do we reliably construct an interval that captures the parameter's plausible values from this MCMC output? This article provides a graduate-level exploration of the theory and practice of creating and validating these Bayesian summaries, known as [credible intervals](@entry_id:176433).

This article systematically builds your expertise across three core areas. The first section, **"Principles and Mechanisms,"** establishes the foundational concepts, contrasting the Bayesian [credible interval](@entry_id:175131) with the frequentist [confidence interval](@entry_id:138194). It details the construction and properties of the two most common types of [credible intervals](@entry_id:176433)—the [equal-tailed interval](@entry_id:164843) (ETI) and the highest posterior density (HPD) set—and introduces the essential tools for quantifying the Monte Carlo error of these estimates. The **"Applications and Interdisciplinary Connections"** section moves from theory to practice, showcasing how these methods are applied in complex, real-world scenarios, from high-dimensional [covariance estimation](@entry_id:145514) to latent structure models, and addresses subtle issues like distinguishing parameter and predictive uncertainty. Finally, the **"Hands-On Practices"** appendix presents targeted exercises to solidify your understanding of advanced topics, such as the true effect of thinning MCMC chains and the formal trade-offs involved in selecting a [burn-in period](@entry_id:747019).

## Principles and Mechanisms

In Bayesian inference, the posterior distribution $p(\theta \mid y)$ encapsulates our complete knowledge about a parameter $\theta$ after observing data $y$. While the full distribution is the most comprehensive summary, it is often necessary to distill this information into a concise numerical summary, such as an interval that contains the parameter with high probability. This chapter details the principles and mechanisms for constructing such intervals, known as **[credible intervals](@entry_id:176433)**, from the output of Markov chain Monte Carlo (MCMC) simulations.

### The Credible Set: A Bayesian Conception of an Interval

A **credible set** is a region in the [parameter space](@entry_id:178581) that is believed to contain the true parameter value with a specified probability. A $100(1-\alpha)\%$ credible set for a scalar parameter $\theta$ is any subset $C$ of the [parameter space](@entry_id:178581) such that the [posterior probability](@entry_id:153467) of $\theta$ lying within $C$ is $1-\alpha$:

$$ P(\theta \in C \mid y) = \int_C p(\theta \mid y) \, d\theta = 1-\alpha $$

This definition embodies a fundamentally Bayesian perspective. The parameter $\theta$ is treated as a random variable, and the probability statement is a direct measure of our belief about its location, conditional on the data we have observed. This contrasts sharply with the frequentist **confidence interval**. A frequentist $95\%$ [confidence interval](@entry_id:138194) is the result of a procedure that, if repeated across many hypothetical datasets drawn from the true data-generating process, would produce intervals containing the fixed, true parameter value in $95\%$ of cases. The probability statement in the frequentist paradigm applies to the procedure, not to any single computed interval containing the parameter  .

An immediate consequence of the definition is that for any given posterior distribution and probability level $1-\alpha$, there are infinitely many possible credible sets. To choose a specific interval, we need additional criteria. The two most common criteria lead to the [equal-tailed interval](@entry_id:164843) and the highest posterior density credible set. MCMC methods provide the computational foundation for estimating these sets by generating a large sample of draws, $\{\theta^{(s)}\}_{s=1}^S$, that can be treated as an empirical approximation of the [posterior distribution](@entry_id:145605) $p(\theta \mid y)$. The consistency of these approximations relies on the ergodicity of the Markov chain, which ensures that averages over the samples converge to true posterior expectations as the number of samples $S \to \infty$ .

### The Equal-Tailed Credible Interval

The **equal-tailed [credible interval](@entry_id:175131) (ETI)** is defined by having equal probability mass in the two tails of the posterior distribution outside the interval. A $100(1-\alpha)\%$ ETI is given by the interval $[q_{\alpha/2}, q_{1-\alpha/2}]$, where $q_p$ is the $p$-th quantile of the posterior distribution of $\theta$.

#### Construction from MCMC Samples

Constructing an ETI from a set of $S$ MCMC draws is straightforward. One simply computes the empirical [quantiles](@entry_id:178417) of the sample. This is typically done by sorting the draws, $\theta_{(1)} \le \theta_{(2)} \le \dots \le \theta_{(S)}$, and identifying the values corresponding to the desired quantile positions. For example, to construct a $95\%$ ETI ($\alpha=0.05$) from $S=20000$ draws, we would find the empirical $0.025$ and $0.975$ [quantiles](@entry_id:178417). These might correspond to the values of the $500$-th and $19500$-th sorted draws, yielding an interval like $[1.18, 3.82]$ . As long as the MCMC chain is ergodic, this empirical interval is a [consistent estimator](@entry_id:266642) of the true posterior ETI, meaning it converges to the true interval as $S \to \infty$. This holds even if the chain is autocorrelated  .

#### A Key Property: Invariance to Transformation

A principal advantage of the ETI is its **equivariance under monotone transformations**. If we have a $95\%$ ETI for a parameter $\theta$ and are interested in a transformed parameter $\phi = g(\theta)$, where $g$ is a strictly [monotone function](@entry_id:637414), the $95\%$ ETI for $\phi$ is simply the result of applying the function $g$ to the endpoints of the interval for $\theta$. This is because [quantiles](@entry_id:178417) themselves transform predictably: the $p$-th quantile of $\phi$ is $g$ applied to the $p$-th quantile of $\theta$ (or $g$ applied to the $(1-p)$-th quantile if $g$ is decreasing). This property holds regardless of the shape of the posterior distribution, including for multimodal posteriors, and is a direct consequence of the definition of [quantiles](@entry_id:178417)  . This invariance is a powerful feature, ensuring consistency of inference across different parameterizations.

### The Highest Posterior Density (HPD) Credible Set

The **highest posterior density (HPD)** credible set is constructed to include the "most plausible" values of the parameter. For a given credibility level $1-\alpha$, the HPD set is the region of the parameter space that contains $100(1-\alpha)\%$ of the [posterior probability](@entry_id:153467) while having the smallest possible volume (or length in one dimension). This is achieved by selecting all points $\theta$ where the posterior density $p(\theta \mid y)$ is above some threshold $c$:

$$ C_{1-\alpha} = \{\theta : p(\theta \mid y) \ge c\} $$

The threshold $c$ is chosen to be the largest value such that the total probability of the set is $1-\alpha$. This construction ensures that any point inside the HPD set has a posterior density greater than or equal to any point outside of it.

#### Structure and Construction

The structure of the HPD set depends critically on the shape of the [posterior distribution](@entry_id:145605).

-   **Unimodal Posteriors:** If the posterior is unimodal, the HPD set will be a single, connected interval. For a continuous density, a necessary condition for this interval $[a,b]$ to be HPD is that the density at its endpoints must be equal: $p(a \mid y) = p(b \mid y)$. This interval is guaranteed to be the shortest of all possible $95\%$ [credible intervals](@entry_id:176433) . To estimate this from MCMC samples, one can search among all intervals containing $(1-\alpha)S$ consecutive sorted draws for the one with the minimum width .

-   **Multimodal Posteriors:** A key strength of the HPD criterion is its handling of multimodal posteriors. If a posterior has multiple modes separated by regions of low density, the HPD set will naturally be a **disjoint union of intervals**, with each interval surrounding a mode. The ETI, by contrast, is always a single interval and may misleadingly include the low-density "valley" between modes, suggesting these values are plausible when they are not .

Consider a hypothetical bimodal posterior for which we have obtained $20$ MCMC draws along with their unnormalized posterior density values. To find the $90\%$ HPD set, we must select the $18$ draws (i.e., $90\%$ of $20$) with the highest posterior density. This is achieved by identifying and discarding the two draws with the lowest density values. If these draws are at the extreme ends of the distribution, the resulting set of $18$ points might span two disconnected regions, for instance, $[-1.5, -0.4]$ and $[2.0, 3.0]$. The total length of this disjoint set would be shorter than any single connected interval containing $18$ draws . This illustrates how the HPD set correctly identifies the distinct high-probability regions.

#### A Key Drawback: Non-Invariance to Transformation

Despite its optimality in terms of length, the HPD set suffers from a significant drawback: it is **not invariant under non-linear reparameterizations**. The reason lies in the change-of-variables formula for probability densities. If $\phi = g(\theta)$, the density of $\phi$ is $p_{\phi}(\phi) = p_{\theta}(g^{-1}(\phi)) |(g^{-1})'(\phi)|$. The Jacobian term $|(g^{-1})'(\phi)|$ re-weights the density. Unless this term is constant—which occurs only if $g$ is an affine transformation ($g(\theta) = a\theta + b$)—the density ordering of points is not preserved  .

A powerful illustration of this is the log-normal distribution . Suppose the posterior for $\phi = \log(\theta)$ is a symmetric normal distribution, $\phi \mid y \sim \mathcal{N}(\mu, \sigma^2)$. The HPD interval for $\phi$ is symmetric around its mean, $[\mu - z\sigma, \mu + z\sigma]$. The posterior for $\theta = \exp(\phi)$ is a skewed [log-normal distribution](@entry_id:139089). One might naively assume that exponentiating the HPD interval for $\phi$ would yield the HPD interval for $\theta$. However, a rigorous derivation shows that the HPD interval for $\theta$, when transformed back to the [log scale](@entry_id:261754), is centered not at $\mu$, but at $\mu - \sigma^2$. This shift demonstrates that the region of highest density for $\theta$ does not correspond to the region of highest density for $\phi$. This non-invariance can lead to different inferential conclusions depending on the parameterization chosen for the analysis.

### Quantifying Monte Carlo Uncertainty

Credible intervals computed from MCMC samples are estimates and are subject to **Monte Carlo error**. A reliable analysis requires quantifying the uncertainty of the interval endpoints themselves.

#### Monte Carlo Standard Error (MCSE) for Quantiles

The primary tool for this is the **Monte Carlo Standard Error (MCSE)**. The MCSE of an estimated quantile $\hat{q}_p$ measures the standard deviation of this estimate across hypothetical repetitions of the MCMC simulation. For an ergodic MCMC chain, the [asymptotic variance](@entry_id:269933) of $\hat{q}_p$ is given by:

$$ \text{Var}(\hat{q}_p) \approx \frac{p(1-p)}{n_{\text{eff}} [f(q_p)]^2} $$

where $f(q_p)$ is the true posterior density at the quantile $q_p$, and $n_{\text{eff}}$ is the **[effective sample size](@entry_id:271661)**. The MCSE is the square root of this variance. The formula reveals that the precision of a quantile estimate depends on three factors:
1.  The quantile level $p$: uncertainty is highest for extreme [quantiles](@entry_id:178417) (as $p \to 0$ or $p \to 1$).
2.  The posterior density at the quantile $f(q_p)$: where the density is low, [quantiles](@entry_id:178417) are harder to estimate precisely (higher MCSE).
3.  The [effective sample size](@entry_id:271661) $n_{\text{eff}}$: a larger [effective sample size](@entry_id:271661) reduces error.

#### The Role of Autocorrelation and Effective Sample Size (ESS)

MCMC draws are typically autocorrelated, meaning that adjacent samples are not independent. This reduces the amount of information in the sample compared to an independent sample of the same size. The **[integrated autocorrelation time](@entry_id:637326) (IAT)**, denoted $\tau$, quantifies this effect. It is defined as $\tau = 1 + 2\sum_{k=1}^{\infty} \rho_k$, where $\rho_k$ is the [autocorrelation](@entry_id:138991) at lag $k$. The **[effective sample size](@entry_id:271661) (ESS)** is then $n_{\text{eff}} = N/\tau$, where $N$ is the total number of MCMC draws. A higher IAT implies a lower ESS and thus higher Monte Carlo error.

For instance, consider estimating a $95\%$ ETI from a chain of $N=20000$ draws with an IAT of $\tau_{\text{int}}=20$. The [effective sample size](@entry_id:271661) is $n_{\text{eff}} = 20000 / 20 = 1000$. If the posterior density is estimated to be $f(\hat{q}_{0.975}) \approx 0.25$ at the upper quantile, the MCSE for that endpoint can be calculated as :

$$ \text{MCSE}(\hat{q}_{0.975}) \approx \sqrt{\frac{0.975(1-0.975)}{1000 \cdot (0.25)^2}} \approx \sqrt{\frac{0.024375}{62.5}} \approx 0.0198 $$

This MCSE can be used to construct a [confidence interval](@entry_id:138194) for the true quantile. For example, a $90\%$ [confidence interval](@entry_id:138194) for the true value of $q_{0.975}$ is approximately $\hat{q}_{0.975} \pm 1.645 \times \text{MCSE}(\hat{q}_{0.975})$ .

#### Diagnostics for Interval Reliability

It is a common pitfall to assume that an MCMC sampler that has converged for estimating the [posterior mean](@entry_id:173826) has also converged for estimating tail [quantiles](@entry_id:178417). Samplers often mix more slowly in the low-density tails of a distribution. Therefore, diagnostics for the reliability of [credible intervals](@entry_id:176433) must be specific to the tails .

- **Tail-ESS vs. Bulk-ESS:** Modern diagnostic packages distinguish between **bulk-ESS**, which pertains to estimating central tendencies like the mean, and **tail-ESS**, which measures the [effective sample size](@entry_id:271661) for estimating [quantiles](@entry_id:178417). It is common to see a large bulk-ESS but much smaller tail-ESS values. The MCSE for interval endpoints should always be calculated using the appropriate tail-ESS.
- **Gelman-Rubin Diagnostic ($\hat{R}$):** While an $\hat{R}$ value close to 1.0 is a necessary check for non-convergence, it is not sufficient to guarantee the reliability of a credible interval. A chain could pass this test but still have a very low tail-ESS, leading to highly uncertain quantile estimates.
- **Thinning:** A common misconception is that thinning an MCMC chain (keeping only every $k$-th draw) improves estimator precision. Thinning discards information and thus can never increase the [effective sample size](@entry_id:271661) or reduce the MCSE  . The correct approach is to use the full chain and account for autocorrelation via the IAT and ESS.

### Summary and Recommendations

The choice between an [equal-tailed interval](@entry_id:164843) and a highest posterior density set involves a trade-off.

-   The **Equal-Tailed Interval (ETI)** is simple to compute and is invariant under parameter transformations, making it a robust and popular choice.
-   The **Highest Posterior Density (HPD) Set** has the appealing property of being the shortest possible credible set and providing a more intuitive summary for skewed or multimodal distributions. However, its lack of invariance to [reparameterization](@entry_id:270587) is a serious theoretical drawback.

In practice, for unimodal and roughly symmetric posteriors, the two intervals will be very similar. For skewed posteriors, the HPD interval will be shorter. For multimodal posteriors, the HPD set is strongly preferred as it correctly identifies disjoint regions of high probability.

Regardless of the method chosen, it is imperative to assess the reliability of the result. The endpoints of any MCMC-derived [credible interval](@entry_id:175131) are estimates subject to Monte Carlo error. Reporting the interval should always be accompanied by a measure of this uncertainty, such as the **Monte Carlo Standard Error (MCSE)** for each endpoint, calculated using an appropriate **tail-specific [effective sample size](@entry_id:271661)**. This practice ensures a transparent and scientifically rigorous communication of posterior uncertainty.