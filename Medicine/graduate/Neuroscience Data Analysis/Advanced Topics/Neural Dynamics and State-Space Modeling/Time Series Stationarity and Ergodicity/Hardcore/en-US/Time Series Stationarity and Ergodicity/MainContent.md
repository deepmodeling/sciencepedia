## Introduction
Time series data, sequences of observations recorded over time, are ubiquitous across science and engineering, from tracking financial markets to monitoring seismic activity and analyzing neural signals. A fundamental challenge in analyzing such data is that their underlying statistical properties can change, potentially invalidating standard analytical methods. This article addresses this problem by providing a comprehensive overview of stationarity and [ergodicity](@entry_id:146461), two cornerstone concepts that define the conditions under which a finite time series can yield reliable and generalizable insights. By mastering these principles, researchers can ensure the validity of their statistical inferences and build more robust models of dynamic systems.

This guide is structured to build your understanding from theoretical foundations to practical applications.
The first chapter, **Principles and Mechanisms**, will formally define strict and [wide-sense stationarity](@entry_id:173765), explain the crucial concept of ergodicity, and show how these properties manifest in fundamental time series models like the ARMA family.
Next, **Applications and Interdisciplinary Connections** will ground these abstract ideas in real-world scenarios, exploring how stationarity assumptions are used and tested in the analysis of EEG, fMRI, and spike train data, and introducing advanced models for non-stationary phenomena.
Finally, **Hands-On Practices** will offer a set of targeted problems to solidify your command of the material, challenging you to apply these concepts in practical analytical contexts.

## Principles and Mechanisms

The analysis of neural time series, such as spike trains, Local Field Potentials (LFPs), or Electroencephalography (EEG) signals, fundamentally relies on characterizing their statistical properties. A critical challenge is that these properties may change over time, reflecting shifts in underlying brain states, cognitive processes, or experimental conditions. The concepts of stationarity and ergodicity provide the foundational mathematical framework for managing this complexity, defining the conditions under which statistical analysis of a single, finite recording can yield meaningful and generalizable insights.

### The Concept of Stationarity

At its core, stationarity is an assumption of [statistical equilibrium](@entry_id:186577). It posits that the statistical rules governing a process do not change over time. This assumption is powerful because it allows us to pool information across a long time series to learn about its underlying generative mechanism. Without it, each time point would be governed by a unique statistical law, making inference from a single realization nearly impossible. There are two primary forms of stationarity, differing in the strength of this invariance assumption.

#### Strict Stationarity

The most rigorous form is **[strict stationarity](@entry_id:260913)** (or strong-sense stationarity). A [stochastic process](@entry_id:159502) $\{X_t\}$ is strictly stationary if its complete probabilistic structure is invariant under shifts in time. Formally, for any finite integer $k \ge 1$, any selection of time indices $t_1, t_2, \dots, t_k$, and any time shift $h$, the [joint probability distribution](@entry_id:264835) of the vector $(X_{t_1}, X_{t_2}, \dots, X_{t_k})$ must be identical to that of the time-shifted vector $(X_{t_1+h}, X_{t_2+h}, \dots, X_{t_k+h})$ . This means that for any set of values $x_1, \dots, x_k$,
$$
P(X_{t_1} \le x_1, \dots, X_{t_k} \le x_k) = P(X_{t_1+h} \le x_1, \dots, X_{t_k+h} \le x_k)
$$
This is a very strong condition, as it requires all statistical properties—including all moments (mean, variance, [skewness](@entry_id:178163), etc.) and any other feature of the joint distributions—to be constant through time. While a powerful theoretical ideal, proving [strict stationarity](@entry_id:260913) from data is often intractable.

#### Wide-Sense Stationarity

For many practical applications in signal processing and neuroscience, a less restrictive condition known as **[wide-sense stationarity](@entry_id:173765)** (WSS), or covariance stationarity, is sufficient. This definition focuses only on the first two moments of the process, which are often the quantities of primary interest (e.g., mean firing rate, [signal power](@entry_id:273924)). A process $\{X_t\}$ with finite second moments is [wide-sense stationary](@entry_id:144146) if it satisfies three conditions :

1.  **Constant Mean:** The expected value of the process is constant for all time $t$. We denote this constant mean by $\mu$.
    $$ \mathbb{E}[X_t] = \mu \quad \text{for all } t $$

2.  **Constant Variance:** The variance of the process is finite and constant for all time $t$. This is implied by the third condition.

3.  **Time-Invariant Autocovariance:** The covariance between the process at two time points, $t_1$ and $t_2$, depends only on the time difference or **lag**, $\tau = t_2 - t_1$, and not on the absolute times.
    $$ \mathrm{Cov}(X_{t_1}, X_{t_2}) = \mathbb{E}[(X_{t_1}-\mu)(X_{t_2}-\mu)] = \gamma(\tau) $$
    The function $\gamma(\tau)$ is called the **autocovariance function**. The variance is simply the [autocovariance](@entry_id:270483) at lag zero, $\mathrm{Var}(X_t) = \gamma(0)$.

This weaker definition is more pragmatic because it is defined by properties that are more readily estimated from data. A strictly stationary process with finite second moments is always [wide-sense stationary](@entry_id:144146), but the converse is not true in general.

#### Stationarity in Vector Processes

In neuroscience, it is common to analyze multichannel recordings, such as signals from an array of electrodes. These are modeled as vector-valued stochastic processes, $X_t \in \mathbb{R}^p$, where $p$ is the number of channels. The concept of [wide-sense stationarity](@entry_id:173765) extends naturally to this multivariate case . A vector process $\{X_t\}$ is [wide-sense stationary](@entry_id:144146) if:

1.  Its [mean vector](@entry_id:266544) is constant: $\mathbb{E}[X_t] = \mu \in \mathbb{R}^p$ for all $t$.

2.  Its [autocovariance](@entry_id:270483) [matrix function](@entry_id:751754) depends only on the lag $\tau$. This is a $p \times p$ matrix defined as:
    $$ \Gamma(\tau) = \mathbb{E}[(X_t - \mu)(X_{t+\tau} - \mu)^\top] $$
    The diagonal elements $\Gamma_{ii}(\tau)$ are the [autocovariance](@entry_id:270483) functions of the individual channels, while the off-diagonal elements $\Gamma_{ij}(\tau)$ for $i \neq j$ are the **cross-covariance functions** between channels $i$ and $j$.

### The Relationship Between Stationarity Concepts

The distinction between strict and [wide-sense stationarity](@entry_id:173765) is subtle but important. While WSS only constrains the first two moments, SS constrains the entire distributional structure. A key question is: when does the more easily verified WSS imply the much stronger SS?

The answer lies in the nature of the process's probability distributions. The most significant special case in time series analysis involves **Gaussian processes**. A process is Gaussian if all its [finite-dimensional distributions](@entry_id:197042) are multivariate normal. A [multivariate normal distribution](@entry_id:267217) is completely specified by its [mean vector](@entry_id:266544) and its covariance matrix. If a Gaussian process is [wide-sense stationary](@entry_id:144146), its [mean vector](@entry_id:266544) and covariance matrix are invariant under time shifts. Because these two moments fully define the distributions, the distributions themselves must be invariant under time shifts. Therefore, for a Gaussian process, [wide-sense stationarity](@entry_id:173765) implies [strict stationarity](@entry_id:260913) . This property is immensely useful, as many models for neural signals assume an underlying Gaussian nature.

For non-Gaussian processes, however, this implication does not hold. It is possible to construct a process where the first two moments are time-invariant, but [higher-order moments](@entry_id:266936) or the shape of the distributions are not. Consider a simple process $\{X_t\}$ where the random variables are independent at each time point, but their distributions alternate depending on whether the time index $t$ is even or odd . For instance, let $X_t$ be drawn from a Uniform distribution for odd $t$ and a Laplace distribution for even $t$. By carefully choosing the parameters of these distributions, we can ensure they share the same mean (e.g., zero) and the same variance. In this case, the process has a constant mean of zero and a constant variance, and since the variables are independent, the [autocovariance](@entry_id:270483) is zero for all non-zero lags. This process is, by definition, [wide-sense stationary](@entry_id:144146). However, it is not strictly stationary because the [marginal distribution](@entry_id:264862) of $X_t$ is not the same for all $t$—it changes every time step.

### Stationarity in Parametric Time Series Models

The concept of stationarity becomes tangible when we examine specific time series models, such as the widely used Autoregressive Moving Average (ARMA) family. These models provide a parsimonious way to describe the dependence structure of a time series.

#### The Autoregressive Model of Order 1 (AR(1))

A foundational example is the AR(1) process, often used to model band-limited fluctuations in signals like EEG or LFP . It is defined by the [recursion](@entry_id:264696):
$$
X_t = \phi X_{t-1} + \epsilon_t
$$
where $\phi$ is the autoregressive coefficient and $\{\epsilon_t\}$ is a **white noise** process—a sequence of uncorrelated random variables with mean zero and constant variance $\sigma^2_\epsilon$.

For this process to be stationary, its dependence on the remote past must fade over time. By recursive substitution, we can express $X_t$ as a sum of past innovations:
$$
X_t = \phi^k X_{t-k} + \sum_{j=0}^{k-1} \phi^j \epsilon_{t-j}
$$
For a stationary solution to exist, the influence of the initial condition $X_{t-k}$ must vanish as we look infinitely far into the past ($k \to \infty$). This occurs if and only if $|\phi|  1$. Under this condition, the process has a well-defined representation as an infinite sum of past noise terms, $X_t = \sum_{j=0}^{\infty} \phi^j \epsilon_{t-j}$. This representation immediately shows that the statistical properties of $X_t$ are determined by the properties of the [white noise process](@entry_id:146877), which are time-invariant. Thus, $|\phi|  1$ is the necessary and [sufficient condition](@entry_id:276242) for the AR(1) process to be stationary.

Under this condition, we can derive its stationary properties :
-   **Mean:** Taking the expectation of the defining equation, $\mathbb{E}[X_t] = \phi \mathbb{E}[X_{t-1}] + \mathbb{E}[\epsilon_t]$. Under stationarity, $\mu = \phi \mu + 0$, which implies $\mu(1-\phi) = 0$. Since $|\phi|1$, we must have $\mu=0$.
-   **Autocovariance:** The variance, $\gamma(0)$, can be found by $\mathrm{Var}(X_t) = \phi^2 \mathrm{Var}(X_{t-1}) + \mathrm{Var}(\epsilon_t)$, which gives $\gamma(0) = \frac{\sigma^2_\epsilon}{1-\phi^2}$. For lags $\tau > 0$, multiplying the AR(1) equation by $X_{t-\tau}$ and taking expectations yields the **Yule-Walker equations**, which for an AR(1) process simplify to the recurrence $\gamma(\tau) = \phi \gamma(\tau-1)$. The solution is an exponentially decaying [autocovariance function](@entry_id:262114):
    $$
    \gamma(\tau) = \frac{\sigma^2_\epsilon}{1-\phi^2} \phi^{|\tau|}
    $$

#### General ARMA(p,q) Processes

This concept generalizes to more complex ARMA(p,q) models. The stationarity of an ARMA process depends exclusively on its autoregressive (AR) component. A causal ARMA(p,q) process is stationary if and only if all the roots of its characteristic AR polynomial, $\phi(z) = 1 - \phi_1 z - \phi_2 z^2 - \dots - \phi_p z^p$, lie strictly outside the unit circle in the complex plane . This mathematical condition ensures that the process can be expressed as a convergent sum of past innovations, making it independent of initial conditions in the remote past. For instance, to check if a given ARMA(2,1) model is stationary, one would find the roots of the quadratic polynomial $\phi(z) = 1 - \phi_1 z - \phi_2 z^2$ and verify that their magnitudes are all greater than 1.

### Ergodicity: The Bridge from Ensembles to Single Realizations

Stationarity is a property of the *ensemble*—the hypothetical collection of all possible realizations of a process. However, in any real experiment, we typically observe only *one* such realization over a finite period. This raises a fundamental question: how can we use a single time series to estimate ensemble properties like the mean $\mu$ or the autocovariance function $\gamma(\tau)$?

The property that provides this crucial link is **[ergodicity](@entry_id:146461)**. A process is ergodic if its time averages converge to its [ensemble averages](@entry_id:197763). More formally, a stationary process $\{X_t\}$ is said to be **[mean-ergodic](@entry_id:180206)** if its [time average](@entry_id:151381), $\bar{X}_n = \frac{1}{n}\sum_{t=1}^{n} X_t$, converges to the ensemble mean $\mu$ as $n \to \infty$.

The theoretical foundation for this is **Birkhoff's Pointwise Ergodic Theorem**, which states that for any strictly stationary and ergodic process $\{X_t\}$ with a finite mean ($\mathbb{E}[|X_t|]  \infty$), the time average converges [almost surely](@entry_id:262518) to the ensemble mean :
$$
\lim_{n \to \infty} \bar{X}_n = \mathbb{E}[X_t] = \mu \quad (\text{almost surely})
$$
This theorem is incredibly powerful because it applies to a vast range of dependent processes, not just independent ones. It is the formal justification for a common practice in neuroscience: calculating the mean firing rate or average LFP power from a single, long recording and treating it as an estimate of the true, underlying ensemble property.

It is critical to understand that stationarity and ergodicity are distinct concepts . Stationarity ensures that the ensemble statistics are time-invariant, making the target of our estimation (e.g., $\mu$) well-defined. Ergodicity ensures that a single, typical realization is representative enough of the entire ensemble that its long-run time average will match the [ensemble average](@entry_id:154225). Stationarity does not imply [ergodicity](@entry_id:146461).

A canonical example of a stationary but non-ergodic process is a mixture model . Imagine an LFP recording where, at the start of the session, the brain network settles into one of two possible latent states, $S=1$ or $S=2$, with some probability. This state then remains fixed. The observed signal is $X_t = \mu_S + W_t$, where $\mu_S$ is the mean signal level associated with the chosen state and $W_t$ is a zero-mean stationary and ergodic noise process.
-   **Stationarity:** As a mixture of two [stationary processes](@entry_id:196130), the overall process $\{X_t\}$ can be shown to be strictly stationary. Its ensemble mean is the weighted average $\mathbb{E}[X_t] = p\mu_1 + (1-p)\mu_2$.
-   **Non-Ergodicity:** However, for any single realization, the state $S$ is fixed. If the session is in state 1, the [time average](@entry_id:151381) will converge to $\mu_1$. If the session is in state 2, the [time average](@entry_id:151381) will converge to $\mu_2$. The time average converges not to the constant ensemble mean, but to a random variable that depends on the initial state. The process is not ergodic because a single realization does not "explore" all possible states; it is locked into one component of the mixture.

### Implications for Statistical Analysis of Neural Data

The principles of stationarity and ergodicity have profound consequences for how we analyze neural data and interpret the results.

#### Consistency and Distribution of Estimators

For a process that is both stationary and ergodic, key [sample statistics](@entry_id:203951) are **consistent estimators** of their ensemble counterparts. This means they converge to the true value as the sample size grows. For example, under [ergodicity](@entry_id:146461) and stationarity:
-   The sample mean $\bar{X}_n = \frac{1}{n}\sum_{t=1}^{n} X_t$ converges to the true mean $\mu$.
-   The [sample variance](@entry_id:164454) $s_n^2 = \frac{1}{n}\sum_{t=1}^{n} (X_t - \bar{X}_n)^2$ converges to the true variance $\gamma(0)$ .

To construct confidence intervals or perform hypothesis tests, we need to know the sampling distribution of our estimators. For [stationary processes](@entry_id:196130) with dependencies that decay sufficiently quickly (known as **mixing** conditions), a **Central Limit Theorem (CLT)** for dependent data applies. It states that the [sample mean](@entry_id:169249) $\bar{X}_n$ is asymptotically normally distributed :
$$
\sqrt{n}(\bar{X}_n - \mu) \xrightarrow{d} \mathcal{N}(0, \sigma^2_{LR})
$$
The [asymptotic variance](@entry_id:269933), $\sigma^2_{LR}$, is the **[long-run variance](@entry_id:751456)**, defined as the sum of all autocovariances:
$$
\sigma^2_{LR} = \sum_{k=-\infty}^{\infty} \gamma(k) = \gamma(0) + 2\sum_{k=1}^{\infty} \gamma(k)
$$
For a process with positive autocorrelation (common in neural signals), $\sigma^2_{LR} > \gamma(0)$, meaning that standard formulas assuming independence will severely underestimate the true uncertainty of the sample mean.

For a concrete example, consider the Gaussian AR(1) process. Its [long-run variance](@entry_id:751456) can be calculated in [closed form](@entry_id:271343) as $\sigma^2_{LR} = \sigma^2_\epsilon / (1-\phi)^2$ . Similar, though more complex, calculations can be performed for the [asymptotic variance](@entry_id:269933) of the [sample variance](@entry_id:164454), which for the Gaussian AR(1) case is $\frac{2\sigma_{\varepsilon}^{4}(1+\phi^{2})}{(1-\phi^{2})^{3}}$ . These results show explicitly how the degree of temporal dependence, captured by $\phi$, directly influences the uncertainty of our statistical estimates.

#### Practical Tools for Inference and Assessment

In practice, the true [autocovariance](@entry_id:270483) structure is unknown, so the [long-run variance](@entry_id:751456) cannot be calculated directly. This is where [resampling](@entry_id:142583) techniques like the **bootstrap** become invaluable. However, the standard i.i.d. bootstrap, which resamples individual data points, is invalid for time series data as it destroys the temporal dependence structure.

Instead, we use methods like the **[block bootstrap](@entry_id:136334)**. The **[moving block bootstrap](@entry_id:169926)** involves resampling overlapping blocks of consecutive observations of a fixed length $b$. By keeping the data within each block intact, the local dependence structure is preserved in the bootstrap replicates. An alternative is the **[stationary bootstrap](@entry_id:637036)**, which resamples blocks of random lengths drawn from a [geometric distribution](@entry_id:154371). For these methods to provide asymptotically valid confidence intervals, the block length $b$ must grow with the sample size $n$, but at a slower rate (i.e., $b \to \infty$ and $b/n \to 0$) .

Finally, since stationarity and [ergodicity](@entry_id:146461) are strong assumptions, it is good practice to perform empirical checks for their violation. While we can never prove these properties from a single finite time series, we can look for evidence of non-stationarity. A common heuristic is to divide a long recording into several non-overlapping segments and compute key statistics (e.g., mean, variance, autocorrelation function) for each segment. If the process is reasonably described as stationary and ergodic, these estimates should be statistically indistinguishable across segments, within [sampling variability](@entry_id:166518). Significant drift or abrupt changes in these statistics across time would be strong evidence against stationarity, warranting caution in the interpretation of analyses that rely on this assumption .