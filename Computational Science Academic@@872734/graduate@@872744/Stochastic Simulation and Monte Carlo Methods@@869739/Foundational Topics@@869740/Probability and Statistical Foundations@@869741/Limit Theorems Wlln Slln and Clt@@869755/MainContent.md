## Introduction
The Monte Carlo method is a cornerstone of modern computational science, enabling the estimation of complex quantities through [random sampling](@entry_id:175193). While its practical application is widespread, a deep understanding of its reliability and precision rests on a rigorous theoretical foundation: the [limit theorems](@entry_id:188579) of probability. These theorems—principally the Law of Large Numbers (LLN) and the Central Limit Theorem (CLT)—explain why and how simulation-based estimators converge to the correct values. This article bridges the gap between the practitioner's use of Monte Carlo methods and the theorist's understanding of their asymptotic behavior.

Over the next three chapters, you will embark on a comprehensive journey through this foundational theory. We will begin in "Principles and Mechanisms" by dissecting the theorems themselves, exploring different [modes of convergence](@entry_id:189917) and examining powerful generalizations for the non-i.i.d. and dependent data ubiquitous in advanced simulations like MCMC. Next, in "Applications and Interdisciplinary Connections," we will see these theorems in action, learning how they are used to analyze Monte Carlo error, optimize [variance reduction techniques](@entry_id:141433), and understand the behavior of complex statistical estimators. Finally, "Hands-On Practices" will provide an opportunity to solidify these concepts by applying them to solve practical problems in simulation design and analysis. By the end, you will have a robust framework for not only using [stochastic simulation](@entry_id:168869) methods but also for analyzing, critiquing, and extending them.

## Principles and Mechanisms

The reliability and utility of Monte Carlo methods are not matters of conjecture; they are underwritten by a rigorous body of mathematical results known as [limit theorems](@entry_id:188579). These theorems describe the behavior of sums and averages of random variables as the number of terms grows to infinity. Having introduced the broad context of [stochastic simulation](@entry_id:168869), this chapter delves into the core principles and mechanisms of these [limit theorems](@entry_id:188579). We will explore not only what these theorems state but also the conditions under which they hold and the profound implications they have for the practice of computational science. We will begin by establishing a precise vocabulary for convergence, then examine the foundational Laws of Large Numbers and Central Limit Theorems, and finally explore their powerful generalizations to the dependent and non-identically distributed scenarios that are ubiquitous in modern applications.

### Modes of Convergence: A Foundational Lexicon

To discuss the [asymptotic behavior](@entry_id:160836) of estimators, we must first be precise about what it means for a sequence of random variables to "converge". There is not one single definition, but rather a hierarchy of different **[modes of convergence](@entry_id:189917)**, each capturing a different probabilistic sense of approaching a limit. Understanding these distinctions is crucial, as different [limit theorems](@entry_id:188579) provide guarantees in different modes. Let $\{X_n\}_{n\geq 1}$ be a sequence of random variables and let $X$ be another random variable, all defined on the same probability space.

**Almost Sure Convergence (Convergence with Probability 1)**: This is the strongest mode of convergence. A sequence $X_n$ converges **[almost surely](@entry_id:262518)** to $X$, denoted $X_n \xrightarrow{a.s.} X$, if the set of outcomes $\omega$ in the [sample space](@entry_id:270284) for which the [sequence of real numbers](@entry_id:141090) $X_n(\omega)$ converges to $X(\omega)$ has probability 1. Formally:
$$
\mathbb{P}\left(\left\{\omega : \lim_{n\to\infty} X_n(\omega) = X(\omega) \right\}\right) = 1
$$
This is a very strong, pathwise notion of convergence. For almost every realization of the underlying random process, the sequence of values converges in the classical sense of a sequence of numbers.

**Convergence in $L^p$ (Convergence in the $p$-th Mean)**: For any real number $p \geq 1$, a sequence $X_n$ converges to $X$ in **$L^p$** if the expected value of the $p$-th power of the absolute difference between $X_n$ and $X$ tends to zero. Formally:
$$
\lim_{n\to\infty} \mathbb{E}\left[|X_n - X|^p\right] = 0
$$
When $p=2$, this is known as **[mean-square convergence](@entry_id:137545)**. This mode is particularly important in [estimation theory](@entry_id:268624), as $\mathbb{E}[(X_n-X)^2]$ represents the [mean squared error](@entry_id:276542) of an estimator $X_n$ for a quantity $X$.

**Convergence in Probability**: A sequence $X_n$ converges **in probability** to $X$, denoted $X_n \xrightarrow{p} X$, if for any arbitrarily small tolerance $\varepsilon > 0$, the probability that $X_n$ and $X$ differ by more than $\varepsilon$ vanishes as $n$ goes to infinity. Formally, for every $\varepsilon > 0$:
$$
\lim_{n\to\infty} \mathbb{P}(|X_n - X| > \varepsilon) = 0
$$
Unlike [almost sure convergence](@entry_id:265812), this mode does not guarantee that any particular sequence $X_n(\omega)$ will converge. It only implies that large deviations from the limit become increasingly rare.

**Convergence in Distribution (Weak Convergence)**: This is the weakest mode of convergence. A sequence $X_n$ converges **in distribution** to $X$, denoted $X_n \xrightarrow{d} X$ or $X_n \Rightarrow X$, if the cumulative distribution function (CDF) of $X_n$, say $F_n(x)$, converges to the CDF of $X$, say $F(x)$, at every point $x$ where $F(x)$ is continuous. Formally:
$$
\lim_{n\to\infty} F_n(x) = F(x) \quad \text{for all } x \text{ where } F \text{ is continuous}
$$
This mode only concerns the "shape" of the distributions. It does not require the random variables to be defined on the same probability space and says nothing about the relationship between the values of $X_n$ and $X$.

These modes are related by a clear hierarchy of implications [@problem_id:3317776]. Both [almost sure convergence](@entry_id:265812) and $L^p$ convergence are stronger than [convergence in probability](@entry_id:145927). Convergence in probability, in turn, is stronger than [convergence in distribution](@entry_id:275544).
$$
\begin{align*}
(X_n \xrightarrow{a.s.} X)  \implies (X_n \xrightarrow{p} X) \\
(X_n \xrightarrow{L^p} X)  \implies (X_n \xrightarrow{p} X) \quad (\text{for } p \ge 1) \\
(X_n \xrightarrow{p} X)  \implies (X_n \xrightarrow{d} X)
\end{align*}
$$

It is essential to recognize that none of these implications are reversible in general. Consider the following illustrative [thought experiments](@entry_id:264574) [@problem_id:3317776]:
*   **Probability $\nRightarrow$ Almost Sure**: Imagine a sequence of [independent events](@entry_id:275822) $A_n$ with $\mathbb{P}(A_n) = 1/n$. Let $X_n$ be the [indicator variable](@entry_id:204387) for $A_n$. Then $\mathbb{P}(|X_n - 0| > \varepsilon) = \mathbb{P}(X_n=1) = 1/n \to 0$, so $X_n \xrightarrow{p} 0$. However, since $\sum \mathbb{P}(A_n)$ diverges, the second Borel-Cantelli lemma implies that with probability 1, infinitely many of the events $A_n$ occur. This means the sequence of values $X_n(\omega)$ will be a sequence of 0s and 1s, with 1s appearing infinitely often, so it does not converge to 0. Thus, $X_n$ does not converge [almost surely](@entry_id:262518).
*   **Probability $\nRightarrow L^p$**: Let $X_n = n^{1/p} \mathbf{1}_{A_n}$ where $A_n$ are independent events with $\mathbb{P}(A_n) = 1/n$. The probability of a large deviation is again $\mathbb{P}(X_n > \varepsilon) = 1/n \to 0$, so $X_n \xrightarrow{p} 0$. However, the $L^p$ error is $\mathbb{E}[|X_n|^p] = \mathbb{E}[(n^{1/p})^p \mathbf{1}_{A_n}] = n \cdot \mathbb{P}(A_n) = n(1/n) = 1$. Since the expected error does not go to zero, $X_n$ does not converge in $L^p$. This models a scenario of estimators that are usually accurate but have a small chance of a catastrophically large error.
*   **Distribution $\nRightarrow$ Probability**: Let $X$ be a Bernoulli(1/2) random variable, and let $X_n$ be an independent copy of $X$ for each $n$. Since all variables are identically distributed, $X_n \xrightarrow{d} X$ trivially. However, the probability that they differ is $\mathbb{P}(|X_n - X| > 0) = \mathbb{P}(X_n \neq X) = 1/2$, which does not converge to 0. Hence, $X_n$ does not converge in probability to $X$.

### The Laws of Large Numbers: Justifying Estimation

The Laws of Large Numbers (LLNs) are the bedrock of Monte Carlo methods. They provide the fundamental guarantee that the average of a large number of random samples converges to its expected value. This justifies using empirical averages to estimate population means or integrals. The LLNs come in two flavors, corresponding to two of the [modes of convergence](@entry_id:189917) we have discussed.

The **Weak Law of Large Numbers (WLLN)** states that the sample mean converges *in probability* to the true mean. The **Strong Law of Large Numbers (SLLN)** makes the more powerful claim that the [sample mean](@entry_id:169249) converges *[almost surely](@entry_id:262518)*. For a practitioner, the SLLN is particularly reassuring: it implies that for any single, long-enough simulation run, the computed average is virtually guaranteed to be close to the true value.

While the most basic LLNs apply to [independent and identically distributed](@entry_id:169067) (i.i.d.) random variables, many practical scenarios in [stochastic simulation](@entry_id:168869) involve more complex [data structures](@entry_id:262134).

#### Kolmogorov's SLLN for Independent Variables

A significant generalization handles sequences of [independent random variables](@entry_id:273896) that are not necessarily identically distributed. This is relevant, for instance, in [importance sampling](@entry_id:145704) with varying proposal distributions. **Kolmogorov's Strong Law of Large Numbers** provides a powerful result in this setting [@problem_id:3317817]. It states that if $\{X_i\}$ is a sequence of [independent random variables](@entry_id:273896) with $\mathbb{E}[X_i] = 0$ and finite variances $\sigma_i^2 = \text{Var}(X_i)$, then the sample mean $\frac{1}{n} \sum_{i=1}^n X_i$ converges almost surely to 0, provided that the variances do not grow too quickly. The precise condition is:
$$
\sum_{i=1}^\infty \frac{\sigma_i^2}{i^2}  \infty
$$
This condition is remarkably weak; for instance, it is satisfied if the variances are uniformly bounded. The proof of this theorem elegantly combines a probabilistic result with a deterministic one. First, one applies **Kolmogorov's convergence criterion** to the transformed sequence $Y_i = X_i/i$. The criterion states that a sum of independent mean-zero variables converges [almost surely](@entry_id:262518) if the sum of their variances is finite. Here, $\sum \text{Var}(Y_i) = \sum \sigma_i^2/i^2$, which is finite by assumption. Thus, the series $\sum_{i=1}^\infty X_i/i$ converges almost surely. Second, one invokes a purely analytical result, **Kronecker's lemma**. This lemma states that if a series $\sum a_k/b_k$ converges for an increasing sequence $b_k \to \infty$, then the average $(1/b_n)\sum a_k$ must go to zero. Applying this to the convergent [sample path](@entry_id:262599) of $\sum X_i(\omega)/i$ (with $a_i=X_i(\omega)$ and $b_i=i$) directly yields that $\frac{1}{n}\sum_{i=1}^n X_i(\omega) \to 0$. Since this holds for almost every path $\omega$, the SLLN is established.

#### The Ergodic Theorem for Markov Chains

Perhaps the most critical extension of the SLLN for modern [computational statistics](@entry_id:144702) is to dependent sequences. Markov Chain Monte Carlo (MCMC) methods, by their very nature, generate a correlated sequence of samples from a target distribution. The theorem that guarantees the consistency of MCMC estimators is the **Ergodic Theorem for Markov Chains** [@problem_id:3317793].

This theorem provides an SLLN for averages computed along the path of a Markov chain. Let $\{X_i\}$ be a Markov chain with a stationary probability distribution $\pi$, and let $f$ be a function whose expectation $\pi(f) = \int f(x) \pi(dx)$ we wish to compute. The key condition for the SLLN to hold is that the chain must be **Harris ergodic**. This is a technical condition ensuring that the chain explores the entire state space sufficiently well and does not get stuck in cycles. If the chain is Harris ergodic and the function $f$ is integrable with respect to the stationary measure (i.e., $f \in L^1(\pi)$, meaning $\int |f(x)|\pi(dx)  \infty$), then for any initial distribution of the chain, the empirical average converges [almost surely](@entry_id:262518) to the true expectation:
$$
\frac{1}{n}\sum_{i=1}^n f(X_i) \xrightarrow{a.s.} \pi(f) \quad \text{as } n \to \infty
$$
This powerful result is the theoretical justification for MCMC. It assures us that, regardless of where the chain starts, a long-enough simulation will produce an estimate that is arbitrarily close to the true value we seek. The proof often relies on a regenerative construction, where the chain's path is cut into i.i.d. "tours", allowing the classical SLLN to be applied to the properties of these tours.

### The Central Limit Theorem: Quantifying Uncertainty

The Laws of Large Numbers tell us that our estimators converge, but they do not tell us at what rate or what the nature of the error is for a finite sample size. This is the role of the **Central Limit Theorem (CLT)**. The CLT describes the distribution of the fluctuations of the sample mean around the true mean. It states that, under suitable conditions, this distribution is approximately Gaussian (Normal). This is an extraordinary and universal result that allows us to construct [confidence intervals](@entry_id:142297) and perform hypothesis tests on the outputs of our simulations.

The canonical CLT states that for a sequence of [i.i.d. random variables](@entry_id:263216) $X_i$ with mean $\mu$ and [finite variance](@entry_id:269687) $\sigma^2 > 0$, the normalized sum converges in distribution to a [standard normal distribution](@entry_id:184509):
$$
\frac{\sum_{i=1}^n X_i - n\mu}{\sigma\sqrt{n}} = \sqrt{n}\left(\frac{\bar{X}_n - \mu}{\sigma}\right) \xrightarrow{d} \mathcal{N}(0,1)
$$
The crucial insight is the $\sqrt{n}$ scaling factor. This tells us that the standard deviation of the error in the sample mean, $\bar{X}_n - \mu$, shrinks at a rate proportional to $1/\sqrt{n}$.

#### The Rate of Convergence: Berry-Esseen Theorem

The CLT is an asymptotic result. For any finite $n$, the [normal approximation](@entry_id:261668) is not exact. The **Berry-Esseen theorem** provides a quantitative, non-[asymptotic bound](@entry_id:267221) on the error in the CLT approximation [@problem_id:3317783]. Under the same i.i.d. assumptions as the classical CLT, plus the condition of a finite third absolute moment $\rho = \mathbb{E}[|X_1 - \mu|^3]  \infty$, the theorem states that there exists an absolute constant $C$ such that:
$$
\sup_{x \in \mathbb{R}} \left| \mathbb{P}\left( \frac{\sqrt{n}(\bar{X}_n - \mu)}{\sigma} \le x \right) - \Phi(x) \right| \le C \frac{\rho}{\sigma^3 \sqrt{n}}
$$
where $\Phi(x)$ is the standard normal CDF. This bound is highly informative. It confirms the $1/\sqrt{n}$ [rate of convergence](@entry_id:146534). The term $\rho/\sigma^3$ is a dimensionless measure of the underlying distribution's asymmetry and tail weight (related to [skewness and kurtosis](@entry_id:754936)). The larger this term, the slower the convergence to the [normal distribution](@entry_id:137477) will be. It is important that the bound depends on the third *absolute* moment $\rho$, not the third central moment $\mathbb{E}[(X_1-\mu)^3]$, because a symmetric distribution (with zero third central moment) is not necessarily normal, and its sum will still have a non-zero approximation error.

#### Generalizations for Independent Variables: The Lindeberg-Feller CLT

Just as with the SLLN, a major goal is to extend the CLT beyond the i.i.d. setting. The **Lindeberg-Feller Central Limit Theorem** is a monumental result that provides [necessary and sufficient conditions](@entry_id:635428) for the CLT to hold for a sum of independent, but not necessarily identically distributed, random variables [@problem_id:3317811].

This theorem is best stated in the language of **triangular arrays**. A triangular array is a collection of random variables $\{X_{n,i}: 1 \le i \le n, n \ge 1\}$, where variables in the same row $n$ are summed up. Let $X_{n,i}$ be independent with $\mathbb{E}[X_{n,i}]=0$ and variance $\sigma_{n,i}^2$. Let $s_n^2 = \sum_{i=1}^n \sigma_{n,i}^2$ be the total variance of the $n$-th row sum $S_n = \sum_{i=1}^n X_{n,i}$. The theorem states that $S_n/s_n \Rightarrow \mathcal{N}(0,1)$ if and only if the **Lindeberg condition** holds: for every $\varepsilon > 0$,
$$
\lim_{n\to\infty} \frac{1}{s_n^2} \sum_{i=1}^n \mathbb{E}\left[X_{n,i}^2 \mathbf{1}\{|X_{n,i}| > \varepsilon s_n\}\right] = 0
$$
The Lindeberg condition has a clear intuition: it requires that the contribution to the total variance from individual variables that are unusually large (specifically, larger than a fraction $\varepsilon$ of the total standard deviation $s_n$) must become negligible as $n \to \infty$. In essence, it ensures that the sum is the result of many small, uniformly behaved contributions, and no single variable dominates the sum. This condition implies a simpler (but not sufficient) condition known as the **Feller condition**, $\max_{i} (\sigma_{n,i}^2 / s_n^2) \to 0$, which states that the largest individual variance must be negligible compared to the total variance.

#### Generalizations for Dependent Data: CLTs for Martingales and Markov Chains

For [stochastic simulation](@entry_id:168869), CLTs for dependent data are paramount. Two of the most important classes are for martingales and Markov chains.

A **[martingale](@entry_id:146036) difference sequence** $\{D_i\}$ with respect to a [filtration](@entry_id:162013) $\{\mathcal{F}_{i-1}\}$ is a sequence where $\mathbb{E}[D_i | \mathcal{F}_{i-1}] = 0$. This models the "innovations" or "surprises" in a time series. The **Martingale Central Limit Theorem** [@problem_id:3317797] states that the sum of a martingale [difference array](@entry_id:636191), $S_n = \sum_i D_{n,i}$, converges to a [normal distribution](@entry_id:137477), provided two key conditions hold. First, the sum of the conditional variances must converge in probability to a constant (say, 1):
$$
\sum_{i=1}^{k_n} \mathbb{E}[D_{n,i}^2 | \mathcal{F}_{n,i-1}] \xrightarrow{p} 1
$$
This is the analog of the variance stabilization in the independent case. Second, a **conditional Lindeberg condition** must hold, ensuring that the [conditional expectation](@entry_id:159140) of large jumps is negligible. This theorem is the foundation for proving the [asymptotic normality](@entry_id:168464) of estimators in many adaptive and time-series models.

For MCMC, the relevant result is the **CLT for Markov Chains** [@problem_id:3317821]. Building upon the SLLN, this theorem specifies the distribution of the error in the MCMC estimator $\bar{f}_n$. Under stronger conditions than the SLLN—typically, **[geometric ergodicity](@entry_id:191361)** (a rapid rate of forgetting the initial state) and square-integrability of the function, $f \in L^2(\pi)$—the CLT holds:
$$
\sqrt{n}(\bar{f}_n - \pi(f)) \xrightarrow{d} \mathcal{N}(0, \sigma_{\text{as}}^2)
$$
A critical feature of this theorem is the form of the **[asymptotic variance](@entry_id:269933)**, $\sigma_{\text{as}}^2$. Unlike the i.i.d. case where the variance is simply $\text{Var}(f(X_1))$, for a Markov chain the [asymptotic variance](@entry_id:269933) includes covariance terms that account for the correlation in the sample:
$$
\sigma_{\text{as}}^2 = \text{Var}_\pi(f(X_0)) + 2 \sum_{k=1}^\infty \text{Cov}_\pi(f(X_0), f(X_k))
$$
This sum, which must be absolutely summable for the theorem to hold, captures the total correlation structure of the process. If the samples are positively correlated (which is common), $\sigma_{\text{as}}^2$ will be larger than the naive variance, meaning the estimator is less precise than an i.i.d. estimator of the same size. Estimating $\sigma_{\text{as}}^2$ is a key challenge in analyzing MCMC output.

### The Analyst's Toolkit: Slutsky's Theorem and the Continuous Mapping Theorem

To apply [limit theorems](@entry_id:188579) in practice, we often need to analyze functions or combinations of convergent sequences. Two indispensable tools for this are the Continuous Mapping Theorem and Slutsky's Theorem [@problem_id:3317781].

The **Continuous Mapping Theorem (CMT)** states that if a sequence of random variables converges in distribution ($X_n \Rightarrow X$), then applying a continuous function $g$ preserves the convergence: $g(X_n) \Rightarrow g(X)$. (More generally, this holds if the set of discontinuity points of $g$ has probability zero under the [limiting distribution](@entry_id:174797) of $X$). For example, if we have a CLT for an estimator $\hat{\theta}_n$ such that $\sqrt{n}(\hat{\theta}_n - \theta) \Rightarrow \mathcal{N}(0, \sigma^2)$, we can use the CMT with the function $g(x) = x^2$ to find the [limiting distribution](@entry_id:174797) of the squared error.

**Slutsky's Theorem** is a powerful result for combining sequences that converge in different modes. It states that if $X_n \Rightarrow X$ ([convergence in distribution](@entry_id:275544)) and $Y_n \xrightarrow{p} c$ ([convergence in probability](@entry_id:145927) to a *constant* $c$), then:
$$
X_n + Y_n \Rightarrow X + c, \quad X_n Y_n \Rightarrow cX, \quad \frac{X_n}{Y_n} \Rightarrow \frac{X}{c} \text{ (if } c \neq 0)
$$
A classic application is the justification of the [t-statistic](@entry_id:177481). The CLT gives $\sqrt{n}(\bar{X}_n - \mu) / \sigma \Rightarrow \mathcal{N}(0,1)$. The sample standard deviation $S_n$ converges in probability to the true standard deviation $\sigma$ by the LLN and CMT. Slutsky's theorem allows us to replace the unknown true $\sigma$ with the estimator $S_n$ in the denominator, concluding that the [t-statistic](@entry_id:177481) $\sqrt{n}(\bar{X}_n - \mu) / S_n$ also converges in distribution to $\mathcal{N}(0,1)$. Slutsky's theorem is potent because it does not require joint convergence of the pair $(X_n, Y_n)$, only marginal convergence.

### A Deeper View: Tightness and Characteristic Functions

The proofs of these powerful [limit theorems](@entry_id:188579) often rely on a more abstract, measure-theoretic framework. The core concepts are **tightness** and **[characteristic functions](@entry_id:261577)** [@problem_id:3317801].

A sequence of probability distributions is **tight** if it does not "escape to infinity". Formally, for any $\varepsilon > 0$, there exists a [compact set](@entry_id:136957) (a bounded, [closed set](@entry_id:136446) in $\mathbb{R}^d$) that contains at least $1-\varepsilon$ of the probability mass for *all* distributions in the sequence. Tightness prevents probability from leaking away.

**Prokhorov's Theorem** provides the crucial link: on a "nice" space like $\mathbb{R}^d$, a sequence of probability measures is tight if and only if every subsequence has a further subsequence that converges weakly (in distribution). Tightness guarantees the existence of convergent subsequences.

**Lévy's Continuity Theorem** connects this to characteristic functions (the Fourier transforms of probability distributions). It states that a sequence of distributions converges weakly if and only if their corresponding characteristic functions converge pointwise to a function that is continuous at the origin.

The general strategy to prove a CLT, then, is a two-step process:
1.  Prove that the sequence of distributions of the normalized sums is tight.
2.  Prove that the sequence of characteristic functions converges pointwise to the [characteristic function](@entry_id:141714) of a normal distribution, $\exp(-t^2\sigma^2/2)$.

Prokhorov's theorem ensures that at least one subsequential limit exists. The uniqueness of the [characteristic function](@entry_id:141714) ensures all subsequential limits must be the same (the normal distribution), which in turn implies that the entire sequence converges.

### A Cautionary Tale: Long-Range Dependence

Finally, it is vital to recognize that the classical CLT scaling is not universal. The behavior of sums can change dramatically if the dependence between observations is very strong. A canonical example is **fractional Gaussian noise**, the increment process of fractional Brownian motion with Hurst parameter $H \in (1/2, 1)$ [@problem_id:3317825]. This process exhibits **[long-range dependence](@entry_id:263964)**, meaning the auto-covariances decay so slowly that their sum diverges.

For such a process, the SLLN may still hold due to ergodicity, ensuring that the sample mean $\bar{X}_n$ converges to the true mean. However, the CLT takes on a non-standard form. By exploiting the [self-similarity](@entry_id:144952) of the underlying fractional Brownian motion, one can show that the sum $\sum_{k=1}^n X_k$ is equal in distribution to $n^H B_H(1)$. This leads to a CLT with a different normalization:
$$
n^{1-H} \bar{X}_n \xrightarrow{d} \mathcal{N}(0, \sigma_H^2)
$$
Since $H > 1/2$, the exponent $\beta = 1-H$ is less than the classical $1/2$. This implies that the standard deviation of the sample mean decays as $n^{H-1}$, which is much slower than the classical $n^{-1/2}$ rate. For example, if $H=0.75$, the error scales as $n^{-0.25}$. This means that to reduce the error by a factor of 10, one needs to increase the sample size by a factor of $10^4 = 10,000$, as opposed to $10^2 = 100$ in the classical case. This illustrates a profound practical lesson: blind application of standard error formulas without considering the dependence structure of the data can lead to a drastic overestimation of an estimator's precision.

In summary, the [limit theorems](@entry_id:188579) of probability provide a complete and rigorous framework for understanding the behavior of stochastic simulations. They not only justify the methods but also provide the tools to quantify their uncertainty and reveal the subtle ways in which the structure of the data—be it non-identical distributions or complex dependence—governs the convergence of our estimators to the truth.