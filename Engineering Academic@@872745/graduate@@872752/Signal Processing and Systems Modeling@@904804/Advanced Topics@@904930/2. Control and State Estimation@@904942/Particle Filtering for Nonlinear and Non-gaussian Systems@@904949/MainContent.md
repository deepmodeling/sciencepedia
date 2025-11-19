## Introduction
Estimating the hidden states of dynamic systems from noisy observations is a fundamental problem across science and engineering. While methods like the Kalman filter provide an [optimal solution](@entry_id:171456) for [linear systems](@entry_id:147850) with Gaussian noise, a vast number of real-world problems—from tracking [financial volatility](@entry_id:143810) to modeling cellular processes—are inherently nonlinear and subject to complex, non-Gaussian uncertainties. In these scenarios, analytical solutions become intractable, creating a critical need for robust and flexible numerical methods.

This article introduces [particle filtering](@entry_id:140084), also known as Sequential Monte Carlo (SMC), a powerful simulation-based framework designed to solve precisely these challenging estimation problems. By representing probability distributions with a cloud of weighted samples, or "particles," these methods can approximate the true posterior distribution of the system's state without restrictive assumptions about linearity or noise characteristics. This article provides a comprehensive exploration of [particle filtering](@entry_id:140084), structured to build your expertise from the ground up.

First, in **Principles and Mechanisms**, we will construct the [particle filter](@entry_id:204067) from first principles, starting with the general Bayesian filtering problem and the Monte Carlo concept. We will then delve into the core mechanics of importance sampling and resampling, and analyze the theoretical guarantees and inherent limitations of these techniques. Next, **Applications and Interdisciplinary Connections** will broaden our perspective, showcasing how [particle filters](@entry_id:181468) are adapted for advanced tasks like [parameter estimation](@entry_id:139349) and smoothing, and how they have become indispensable tools in fields ranging from econometrics to [systems biology](@entry_id:148549). Finally, **Hands-On Practices** will allow you to solidify your understanding by implementing and analyzing key components of the [particle filtering](@entry_id:140084) algorithm.

## Principles and Mechanisms

This chapter delineates the foundational principles and core mechanisms that underpin [particle filtering](@entry_id:140084). We begin by formulating the general Bayesian filtering problem for nonlinear and non-Gaussian systems, highlighting the analytical intractability that motivates numerical solutions. We then introduce the Monte Carlo principle and importance sampling as the conceptual cornerstones of [particle methods](@entry_id:137936). Building upon this, we construct the bootstrap [particle filter algorithm](@entry_id:202446) step-by-step, addressing the critical issues of [weight degeneracy](@entry_id:756689) and resampling. The chapter concludes by examining the theoretical guarantees and inherent limitations of these methods, including path degeneracy and the [curse of dimensionality](@entry_id:143920).

### The General Bayesian Filtering Problem

In the context of [discrete-time state-space](@entry_id:261361) models, we are concerned with inferring a sequence of hidden states, $\{x_t \in \mathbb{R}^{d_x}\}_{t \ge 0}$, given a corresponding sequence of observations, $\{y_t \in \mathbb{R}^{d_y}\}_{t \ge 1}$. The behavior of the system is characterized by two fundamental components:

1.  A **state transition model**, which defines the evolution of the state over time. It is specified by the transition probability density $p(x_t | x_{t-1})$. The state process is assumed to be a first-order Markov process, meaning the current state $x_t$ depends only on the immediately preceding state $x_{t-1}$.

2.  An **observation model**, which defines the probabilistic relationship between the current state and the current observation. It is specified by the observation probability density, or likelihood, $p(y_t | x_t)$. Observations are assumed to be conditionally independent given the current state.

A general state-space model can therefore be expressed as:
$x_t = f(x_{t-1}, v_{t-1})$
$y_t = h(x_t, e_t)$
where $f$ and $h$ are potentially nonlinear functions, and $v_t$ and $e_t$ are sequences of independent random variables representing [process and measurement noise](@entry_id:165587), respectively. These noise terms may follow arbitrary, non-Gaussian distributions. For example, a system might exhibit nonlinear dynamics and be subject to heavy-tailed noise, such as that described by a Laplace distribution [@problem_id:2890402].

The central objective of filtering is to recursively compute the posterior probability distribution of the current state $x_t$ given all observations up to time $t$, denoted by the history $y_{1:t} = (y_1, \dots, y_t)$. This posterior, $p(x_t | y_{1:t})$, is known as the **filtering distribution**. It encapsulates all available information about the state at time $t$. The [recursive estimation](@entry_id:169954) of this distribution proceeds in two stages:

**1. Prediction (Time Update):** This step involves using the state transition model to predict the state distribution at time $t$, based on all information available at time $t-1$. Starting with the filtering distribution from the previous step, $p(x_{t-1} | y_{1:t-1})$, the predictive distribution $p(x_t | y_{1:t-1})$ is computed via the Chapman-Kolmogorov equation:
$$
p(x_t | y_{1:t-1}) = \int p(x_t | x_{t-1}) p(x_{t-1} | y_{1:t-1}) \, \mathrm{d}x_{t-1}
$$
This integral propagates the uncertainty from the previous state through the [system dynamics](@entry_id:136288).

**2. Update (Measurement Update):** This step incorporates the new observation $y_t$ to refine the predictive distribution into the new filtering distribution. Using Bayes' rule, the update is performed as follows:
$$
p(x_t | y_{1:t}) = \frac{p(y_t | x_t) p(x_t | y_{1:t-1})}{p(y_t | y_{1:t-1})}
$$
The denominator, $p(y_t | y_{1:t-1}) = \int p(y_t | x_t) p(x_t | y_{1:t-1}) \, \mathrm{d}x_t$, is the marginal likelihood of the new observation, often called the evidence. It serves as a [normalizing constant](@entry_id:752675), ensuring the posterior integrates to one [@problem_id:2890402].

For general nonlinear functions $f$ and $h$ or non-Gaussian noise distributions, the integrals in the prediction and update steps do not have closed-form analytical solutions. The distributions $p(x_t | y_{1:t-1})$ and $p(x_t | y_{1:t})$ cannot be represented by a [finite set](@entry_id:152247) of parameters, and the recursive computation becomes intractable. This necessitates the use of [numerical approximation methods](@entry_id:169303), among which [particle filtering](@entry_id:140084) is a prominent and powerful approach.

### The Limitations of Analytical Solutions: Why the Kalman Filter Fails

To appreciate the need for [particle filters](@entry_id:181468), it is instructive to consider the specific case where the Bayesian filtering [recursion](@entry_id:264696) *is* analytically tractable: the linear-Gaussian model, for which the Kalman filter provides an exact solution. The Kalman filter's success hinges on a crucial property of the Gaussian distribution: its closure under affine transformations and products.

Let us assume the filtering distribution at time $t-1$, $p(x_{t-1} | y_{1:t-1})$, is Gaussian.
*   In the **prediction step**, a linear-Gaussian model assumes $x_t = F_t x_{t-1} + w_t$, where $w_t$ is zero-mean Gaussian noise. The predictive distribution $p(x_t | y_{1:t-1})$ is obtained by convolving the Gaussian distribution of $F_t x_{t-1}$ (which is Gaussian because $x_{t-1}$ is) with the Gaussian distribution of $w_t$. The result is another Gaussian distribution.
*   In the **update step**, the model assumes $y_t = H_t x_t + v_t$, with $v_t$ being zero-mean Gaussian noise. The likelihood $p(y_t | x_t)$ is a Gaussian function of $x_t$. The posterior $p(x_t | y_{1:t})$ is proportional to the product of this Gaussian likelihood and the Gaussian predictive prior. The product of two Gaussian functions is another (unnormalized) Gaussian function.

Thus, if the initial state is Gaussian, the filtering distribution remains Gaussian at every subsequent step. The Kalman filter elegantly propagates the mean and covariance of this Gaussian through the prediction and update equations.

This analytical tractability breaks down immediately if either the [system dynamics](@entry_id:136288) or the noise distributions deviate from the linear-Gaussian assumption [@problem_id:2890466].
*   **Nonlinearity:** If the state transition $f(x_{t-1})$ or observation function $h(x_t)$ is nonlinear, the Gaussian property is lost. A nonlinear transformation of a Gaussian variable does not, in general, yield a Gaussian variable. In the update step, a nonlinear $h(x_t)$ results in a non-Gaussian likelihood function, and its product with a Gaussian prior is no longer Gaussian.
*   **Non-Gaussian Noise:** Even if the functions $f$ and $h$ are linear, if the [process noise](@entry_id:270644) $v_t$ or measurement noise $e_t$ is non-Gaussian (e.g., from a Laplace or a [mixture distribution](@entry_id:172890)), the [closure property](@entry_id:136899) fails. The convolution in the prediction step or the product in the update step will involve a non-Gaussian density, yielding a non-Gaussian result.

In these widespread and practical scenarios, the filtering distribution can become multimodal, skewed, or otherwise complex. Any algorithm, like the Kalman filter, that restricts its representation of the posterior to a Gaussian form will be, at best, an approximation and may fail to capture the true nature of the state uncertainty. This is the fundamental motivation for [particle filters](@entry_id:181468), which are designed to represent and propagate arbitrary probability distributions.

### The Monte Carlo Principle

Since we cannot compute the filtering recursion analytically, we turn to [numerical approximation](@entry_id:161970). The core idea behind [particle filtering](@entry_id:140084) is the **Monte Carlo method**. Many quantities of interest in filtering are expectations of some function $\varphi(x_t)$ with respect to the filtering distribution, such as the state mean ($\varphi(x_t) = x_t$) or variance ($\varphi(x_t) = (x_t - \mathbb{E}[x_t])^2$). By definition, this expectation is an integral:
$$
\mathbb{E}[\varphi(x_t) | y_{1:t}] = \int \varphi(x_t) p(x_t | y_{1:t}) \, \mathrm{d}x_t
$$
The Monte Carlo principle states that we can approximate this integral by drawing a large number, $N$, of samples (or "particles") from the distribution and computing an empirical average. If we could somehow generate $N$ independent and identically distributed (i.i.d.) samples $x_t^{(1)}, \dots, x_t^{(N)}$ directly from the target filtering distribution $p(x_t | y_{1:t})$, then by the Law of Large Numbers, the [sample mean](@entry_id:169249) provides a [consistent estimator](@entry_id:266642) of the true expectation [@problem_id:2890451]:
$$
\mathbb{E}[\varphi(x_t) | y_{1:t}] \approx \frac{1}{N} \sum_{i=1}^{N} \varphi(x_t^{(i)})
$$
This [empirical distribution](@entry_id:267085), $\hat{p}(x_t | y_{1:t}) = \frac{1}{N} \sum_{i=1}^{N} \delta(x_t - x_t^{(i)})$, where $\delta(\cdot)$ is the Dirac [delta function](@entry_id:273429), can be seen as a discrete approximation of the true continuous posterior.

The critical challenge, however, is that sampling directly from the complex and recursively-defined filtering distribution $p(x_t | y_{1:t})$ is typically just as intractable as solving the integral itself. This leads us to a more sophisticated technique: [importance sampling](@entry_id:145704).

### Importance Sampling: The Foundation of Particle Filtering

**Importance Sampling (IS)** is a Monte Carlo technique that allows us to approximate expectations with respect to a [target distribution](@entry_id:634522) $p(x)$ by using samples drawn from a different, simpler distribution $q(x)$, known as the **[proposal distribution](@entry_id:144814)** or **importance distribution**. The only major requirement is that the support of the proposal must cover the support of the target, i.e., if $p(x) > 0$, then $q(x) > 0$.

The method is based on a simple identity. We rewrite the integral of interest as:
$$
I = \int \varphi(x) p(x) \, \mathrm{d}x = \int \varphi(x) \frac{p(x)}{q(x)} q(x) \, \mathrm{d}x = \mathbb{E}_{q}\left[ \varphi(X) w(X) \right]
$$
where $w(x) \equiv \frac{p(x)}{q(x)}$ is the **importance weight**. This re-expresses the original expectation under $p$ as an expectation under $q$ of the modified function $\varphi(x)w(x)$. We can now approximate this new expectation by drawing samples $x^{(i)} \sim q(x)$ and forming the Monte Carlo average:
$$
I \approx \frac{1}{N} \sum_{i=1}^{N} \varphi(x^{(i)}) w(x^{(i)})
$$
The weights $w(x^{(i)})$ correct for the mismatch between the proposal distribution $q(x)$ from which we sampled and the [target distribution](@entry_id:634522) $p(x)$ that we are interested in.

In Bayesian filtering, the target density $p(x_t | y_{1:t})$ is often known only up to a [normalizing constant](@entry_id:752675). That is, $p(x) = \gamma(x)/Z$, where $\gamma(x)$ is computable (e.g., likelihood $\times$ prior) but the evidence $Z$ is not. In this case, the importance weight $w(x) = \gamma(x) / (Z q(x))$ still contains the unknown constant $Z$. We can circumvent this by using **[self-normalized importance sampling](@entry_id:186000)**. We compute unnormalized weights $\tilde{w}(x) = \gamma(x) / q(x)$ and then normalize them:
$$
w^{(i)} = \frac{\tilde{w}^{(i)}}{\sum_{j=1}^{N} \tilde{w}^{(j)}}
$$
The unknown constant $Z$ appears in both the numerator and denominator and thus cancels out [@problem_id:2890408]. The final estimator for the expectation is a weighted average:
$$
\mathbb{E}[\varphi(x_t) | y_{1:t}] \approx \sum_{i=1}^{N} w^{(i)} \varphi(x^{(i)})
$$
This self-normalized estimator is consistent, converging to the true expectation as $N \to \infty$, but it is generally biased for any finite sample size $N$ [@problem_id:2890451].

### Sequential Importance Sampling and the Bootstrap Filter

The idea of importance sampling can be extended to the sequential nature of the filtering problem, leading to the **Sequential Importance Sampling (SIS)** algorithm. The goal is to approximate the sequence of filtering distributions $p(x_t|y_{1:t})$ for $t=1, 2, \dots$. The SIS framework applies importance sampling recursively.

At each step $t$, we draw new particles $x_t^{(i)}$ from a proposal distribution $q(x_t | x_{t-1}^{(i)}, y_t)$ and update their [importance weights](@entry_id:182719). The weight for the entire path of a particle $x_{0:t}^{(i)}$ is updated recursively: $W_t^{(i)} \propto W_{t-1}^{(i)} \times \alpha_t^{(i)}$, where $\alpha_t^{(i)}$ is the incremental weight.

A particularly simple and widely used variant is the **bootstrap [particle filter](@entry_id:204067)**. In this algorithm, the proposal distribution is chosen to be the state transition prior:
$$
q(x_t | x_{t-1}^{(i)}, y_t) = p(x_t | x_{t-1}^{(i)})
$$
This is a convenient choice because it is readily available from the model definition and does not depend on the current observation $y_t$. With this proposal, the incremental weight factor simplifies dramatically. The unnormalized weight for particle $i$ at time $t$ becomes:
$$
\tilde{w}_t^{(i)} \propto \tilde{w}_{t-1}^{(i)} \frac{p(y_t | x_t^{(i)}) p(x_t^{(i)} | x_{t-1}^{(i)})}{p(x_t^{(i)} | x_{t-1}^{(i)})} = \tilde{w}_{t-1}^{(i)} p(y_t | x_t^{(i)})
$$
Thus, to update the weights, we simply multiply the previous weight by the likelihood of the new observation given the new particle state [@problem_id:2890451].

### The Problem of Degeneracy and the Necessity of Resampling

A naive implementation of the SIS algorithm suffers from a severe practical issue known as **[weight degeneracy](@entry_id:756689)**. As the algorithm iterates over time, the variance of the unnormalized [importance weights](@entry_id:182719) tends to increase. After a few steps, a situation arises where one or a very small number of particles have weights close to one, while all other particles have weights that are nearly zero. This means that a large amount of computational effort is wasted on updating particles that contribute negligibly to the approximation of the [posterior distribution](@entry_id:145605).

To monitor this problem, a quantitative measure is needed. The most common metric is the **Effective Sample Size (ESS)**, which provides an estimate of the number of "useful" particles. For a set of normalized weights $\{w_t^{(i)}\}_{i=1}^N$, the ESS is estimated as:
$$
N_{\text{eff}} = \frac{1}{\sum_{i=1}^{N} (w_t^{(i)})^2}
$$
This quantity ranges from $1$ (complete degeneracy, one particle has all the weight) to $N$ (no degeneracy, all weights are uniform, $w_t^{(i)} = 1/N$). If one is working with unnormalized weights $\{\tilde{w}_t^{(i)}\}$, the formula is $N_{\text{eff}} = (\sum \tilde{w}_t^{(i)})^2 / (\sum (\tilde{w}_t^{(i)})^2)$ [@problem_id:2890369].

A common practice is to perform a resampling step whenever the ESS drops below a certain threshold, for example, $N_{\text{eff}} \le N/2$. Consider a system with $N=6$ particles with normalized weights $(0.40, 0.25, 0.20, 0.10, 0.03, 0.02)$. The sum of squared weights is $0.4^2 + 0.25^2 + \dots + 0.02^2 = 0.2738$, yielding an ESS of $1/0.2738 \approx 3.65$. With a threshold of $N/2=3$, resampling would not yet be triggered. However, the weights are clearly uneven, illustrating the onset of degeneracy [@problem_id:2890369].

### The Resampling Step: Mechanism and Consequences

To counteract [weight degeneracy](@entry_id:756689), a **[resampling](@entry_id:142583)** step is introduced into the SIS algorithm, leading to the full **Sequential Importance Resampling (SIR)** algorithm, of which the [bootstrap filter](@entry_id:746921) is the most common example. Resampling is a procedure that aims to eliminate particles with low weights and replicate particles with high weights.

The full cycle of the [bootstrap filter](@entry_id:746921) (a resample-propagate algorithm) proceeds as follows [@problem_id:2890365]:

1.  **Resampling:** Given the weighted particles from the previous step, $\{(x_{t-1}^{(i)}, w_{t-1}^{(i)})\}_{i=1}^N$, we generate an intermediate set of $N$ particles by drawing with replacement from the set $\{x_{t-1}^{(i)}\}$ according to their weights. That is, the probability of drawing $x_{t-1}^{(j)}$ is $w_{t-1}^{(j)}$. Let the resampled particles (which may have duplicates) be denoted $\{\tilde{x}_{t-1}^{(i)}\}_{i=1}^N$.

2.  **Propagation:** Each new particle $x_t^{(i)}$ is generated by sampling from the state transition model, using one of the resampled particles from the previous step as its "parent":
    $$
    x_t^{(i)} \sim p(x_t | \tilde{x}_{t-1}^{(i)})
    $$

3.  **Weighting:** The new unnormalized weights are set equal to the likelihood of the observation $y_t$ given the new particle state. Crucially, after [resampling](@entry_id:142583), all "parent" particles are effectively given equal weight, so the previous weights $w_{t-1}^{(i)}$ are not carried over.
    $$
    \tilde{w}_t^{(i)} = p(y_t | x_t^{(i)})
    $$
    These weights are then normalized to sum to one: $w_t^{(i)} = \tilde{w}_t^{(i)} / \sum_j \tilde{w}_t^{(j)}$.

After the [resampling](@entry_id:142583) step, the particle set consists of $N$ equally weighted particles representing the posterior at time $t-1$. This resets the ESS to its maximum value, $N$, effectively combating [weight degeneracy](@entry_id:756689) [@problem_id:2890369].

An important byproduct of this process is an [unbiased estimator](@entry_id:166722) for the incremental [marginal likelihood](@entry_id:191889), or evidence, $p(y_t | y_{1:t-1})$. This can be estimated by the average of the unnormalized weights before normalization:
$$
\hat{p}(y_t | y_{1:t-1}) = \frac{1}{N} \sum_{i=1}^N \tilde{w}_t^{(i)} = \frac{1}{N} \sum_{i=1}^N p(y_t | x_t^{(i)})
$$
By multiplying these estimates over time, one can obtain an estimate of the total marginal likelihood $p(y_{1:t})$, which is useful for [model comparison](@entry_id:266577) [@problem_id:2890365].

### A Deeper Look at Resampling Schemes

The term "resampling" encompasses several specific algorithms, each with different statistical properties. The choice of scheme can impact the performance of the particle filter by affecting the variance of the resulting estimates. All valid schemes are unbiased in the sense that the expected number of offspring for a particle $i$ is $N w_i$. They primarily differ in the variance of the offspring counts [@problem_id:2890427].

*   **Multinomial Resampling:** This is the most conceptually simple scheme. It consists of drawing $N$ [independent samples](@entry_id:177139) from the categorical distribution defined by the weights $\{w_i\}$. It is equivalent to [sampling with replacement](@entry_id:274194). While simple, it introduces significant [stochasticity](@entry_id:202258), as the number of offspring for a given particle can vary widely.

*   **Stratified Resampling:** This scheme reduces the variance of the resampling process. It divides the interval $[0, 1)$ into $N$ contiguous strata of equal size $1/N$. One uniform random number is drawn independently from each stratum. These $N$ numbers are then used to select particles via the inverse CDF method. This ensures that the selection of samples is more evenly spread, and it can be shown that the variance of the resulting estimator is lower than or equal to that of [multinomial resampling](@entry_id:752299).

*   **Systematic Resampling:** This is a popular and efficient low-variance scheme. A single random number $u$ is drawn from $\text{Unif}[0, 1/N)$. This defines a grid of $N$ points: $u, u+1/N, u+2/N, \dots, u+(N-1)/N$. These points are then used to select particles. This introduces negative correlation between the selections, which further reduces sampling variance. For many problems, its variance is lower than stratified resampling, although no universal ordering exists.

*   **Residual Resampling:** This method combines deterministic and random components. For each particle $i$, a deterministic number of offspring, $\lfloor N w_i \rfloor$, is created. The remaining $R = N - \sum_i \lfloor N w_i \rfloor$ offspring are then chosen by applying a simpler resampling scheme (like multinomial) to the "residual" weights. This scheme guarantees that particles with large weights get at least a certain number of copies, significantly reducing the sampling variance.

### Theoretical Guarantees and Inherent Limitations

While [particle filters](@entry_id:181468) provide a powerful and flexible tool, it is crucial to understand their theoretical properties and limitations.

#### Consistency

Under relatively mild conditions, the bootstrap particle filter is **consistent**. This means that for any fixed time horizon $t$, as the number of particles $N$ approaches infinity, the empirical approximation converges to the true filtering distribution. More formally, for any bounded [test function](@entry_id:178872) $\varphi$, the estimator $\hat{\pi}_t^N(\varphi) = \sum_i W_t^{(i)} \varphi(X_t^{(i)})$ converges to the true expectation $\pi_t(\varphi) = \mathbb{E}[\varphi(X_t) | Y_{0:t}]$. The proof of this fundamental result proceeds by induction on time. At each step, the consistency is a consequence of the Law of Large Numbers applied to the (self-normalized) [importance sampling](@entry_id:145704) and [resampling](@entry_id:142583) stages, which are conditionally unbiased [@problem_id:2890470]. This guarantee provides the essential theoretical justification for using [particle filters](@entry_id:181468).

#### Path Degeneracy

While resampling solves the problem of [weight degeneracy](@entry_id:756689), it introduces a new, more subtle issue: **path degeneracy**. Because [resampling](@entry_id:142583) involves duplicating particles, the diversity of the particle *trajectories* (or paths) is reduced. If we trace the ancestry of the particles at time $t$ backward, they descend from an ever-smaller set of ancestors at previous times. After a sufficient number of resampling steps, it is likely that all $N$ particles at time $t$ share a single common ancestor from a much earlier time, say $t-s$. This phenomenon is called **coalescence** of the ancestry tree. The result is that while the particles $\{x_t^{(i)}\}$ may provide a good approximation of the *marginal* filtering distribution $p(x_t|y_{1:t})$, the set of paths $\{x_{0:t}^{(i)}\}$ provides a very poor approximation of the *joint* smoothing distribution $p(x_{0:t}|y_{1:t})$. The time scale for this coalescence to occur is on the order of $O(N)$ [@problem_id:2890415]. This makes standard [particle filters](@entry_id:181468) poorly suited for many smoothing applications.

#### The Curse of Dimensionality

Perhaps the most significant limitation of the basic [particle filter](@entry_id:204067) is the **curse of dimensionality**. The performance of the filter degrades rapidly as the dimension $d_x$ of the state space increases. The underlying reason is that in a high-dimensional space, it becomes exceedingly difficult for a "blind" proposal distribution, such as the transition prior $p(x_t|x_{t-1})$, to generate particles that land in regions of high likelihood $p(y_t|x_t)$.

This can be quantified by analyzing the variance of the [importance weights](@entry_id:182719). For a simple linear-Gaussian model, it can be shown that the variance of the log-weights grows linearly with the dimension $d_x$. Using a log-[normal approximation](@entry_id:261668) for the distribution of the weights, this [linear growth](@entry_id:157553) in the log-weight variance implies that the Effective Sample Size (ESS) decays *exponentially* with the dimension [@problem_id:2890433]:
$$
\text{ESS} \propto N \exp(-c \cdot d_x)
$$
where $c$ is a constant depending on model parameters. To counteract this exponential decay and maintain a constant ESS, the number of particles $N$ would need to grow exponentially with the dimension $d_x$. This makes the basic [particle filter](@entry_id:204067) computationally infeasible for all but low-dimensional problems. This critical limitation has motivated a vast field of research into more advanced [particle filtering](@entry_id:140084) techniques designed to operate in higher dimensions.