## Introduction
In modern science and engineering, particularly in fields like [computational geophysics](@entry_id:747618), our understanding of complex systems is often refined by solving inverse problems. The Bayesian framework offers a powerful and principled approach to this task, combining prior knowledge with observed data to fully characterize the uncertainty of model parameters through the posterior probability distribution. However, for most realistic, non-linear problems, this posterior distribution is a high-dimensional and analytically intractable entity, rendering direct analysis impossible. This knowledge gap—the inability to explore and understand the very solution that Bayesian inference provides—is the central challenge we address.

This article provides a comprehensive guide to the computational methods designed to overcome this obstacle: Markov chain Monte Carlo (MCMC) and its powerful extension, [trans-dimensional sampling](@entry_id:756096). These algorithms transform the intractable problem of analyzing a distribution into the feasible task of generating samples from it, unlocking the full potential of Bayesian inference. Through the following chapters, you will gain a deep understanding of these state-of-the-art techniques. The journey begins with **Principles and Mechanisms**, where we will build the theoretical foundation, starting from Bayes' theorem and progressing through the mechanics of core MCMC algorithms, the innovative Reversible Jump MCMC for [model selection](@entry_id:155601), and methods for [model comparison](@entry_id:266577). Next, in **Applications and Interdisciplinary Connections**, we will explore how these methods are adapted and enhanced to solve challenging, [high-dimensional inverse problems](@entry_id:750278) in [geophysics](@entry_id:147342) and a variety of other scientific fields. Finally, the **Hands-On Practices** chapter provides concrete problems to solidify the theoretical concepts and prepare you for real-world implementation. We begin by exploring the core objective of any Bayesian analysis: characterizing the posterior distribution.

## Principles and Mechanisms

### The Bayesian Objective: Characterizing the Posterior Distribution

In [geophysical inversion](@entry_id:749866), our primary goal is to infer the properties of a physical system, represented by a model parameter vector $m$, from a set of observed data, $d$. The Bayesian framework accomplishes this by formulating the [posterior probability](@entry_id:153467) distribution, $p(m|d)$, which encapsulates all that is known about $m$ after observing $d$. According to Bayes' theorem, the posterior is the normalized product of the likelihood and the prior:

$p(m|d) = \frac{p(d|m) p(m)}{p(d)}$

Here, the **likelihood**, $p(d|m)$, quantifies the probability of observing the data $d$ for a given model $m$. The **prior**, $p(m)$, encodes our knowledge or assumptions about the model parameters before any data are considered. The denominator, $p(d) = \int p(d|m) p(m) dm$, is the **marginal likelihood** or **[model evidence](@entry_id:636856)**, which acts as a [normalizing constant](@entry_id:752675).

While this theorem provides a complete recipe for inference, the posterior distribution is often a complex, high-dimensional function for which direct analysis is intractable. To build intuition, it is instructive to consider a simplified case where an analytical solution exists. Consider a linear geophysical [forward model](@entry_id:148443), where the data are related to the model parameters by a matrix operator $G$:

$d = G m + e$

If we assume that both our prior knowledge about $m$ and the data noise $e$ can be described by Gaussian distributions, the problem becomes analytically tractable [@problem_id:3609510]. Specifically, let the prior be $m \sim \mathcal{N}(m_0, C_m)$ and the noise be $e \sim \mathcal{N}(0, C_e)$, where $m_0$ is the prior [mean vector](@entry_id:266544) and $C_m$ and $C_e$ are the prior and noise covariance matrices, respectively. The likelihood is then $p(d|m) \sim \mathcal{N}(Gm, C_e)$. In this special linear-Gaussian case, the resulting posterior distribution $p(m|d)$ is also a multivariate Gaussian, $\mathcal{N}(m_{\text{post}}, C_{\text{post}})$, with a [posterior mean](@entry_id:173826) and covariance given by:

$$C_{\text{post}} = \left(G^{\top} C_e^{-1} G + C_m^{-1}\right)^{-1}$$

$$m_{\text{post}} = C_{\text{post}}\left(G^{\top} C_e^{-1} d + C_m^{-1} m_0\right)$$

In this idealized scenario, our inferential goal is achieved. The [posterior mean](@entry_id:173826), $m_{\text{post}}$, represents the most probable model, a balanced combination of the data-predicted model and the prior model. The [posterior covariance](@entry_id:753630), $C_{\text{post}}$, completely characterizes the uncertainty in our estimate of $m$. Its diagonal elements give the variances of individual parameters, while its off-diagonal elements describe their correlations. The key insight is that for such problems, the posterior is known in [closed form](@entry_id:271343).

However, most real-world geophysical problems are not linear, and the associated probability distributions are not Gaussian. For these more complex scenarios, the [posterior distribution](@entry_id:145605) cannot be written down as a simple analytical function. We cannot directly compute its mean, covariance, or marginals. Instead, our objective shifts from finding a [closed-form solution](@entry_id:270799) to generating a representative set of samples from the posterior distribution. This collection of samples allows us to approximate any desired property of the posterior, such as its moments or [credible intervals](@entry_id:176433). **Markov chain Monte Carlo (MCMC)** methods are the primary class of algorithms designed to accomplish this sampling task.

### The Markov Chain Monte Carlo Paradigm

The core idea of MCMC is to construct a **Markov chain**, a sequence of random states $\{X_1, X_2, X_3, \dots\}$, where each state $X_{t+1}$ is drawn from a distribution that depends only on the previous state $X_t$. The algorithm is designed in such a way that, after an initial "[burn-in](@entry_id:198459)" period, the stationary distribution of this chain is precisely the target [posterior distribution](@entry_id:145605) $\pi(m) \equiv p(m|d)$. Thus, the states of the chain become samples from the posterior.

For this elegant correspondence to hold, the Markov chain's transition mechanism, defined by a **transition kernel** $K(x, A) = P(X_{t+1} \in A | X_t = x)$, must satisfy certain theoretical properties. These properties ensure that the chain not only converges to the correct distribution but also explores it thoroughly [@problem_id:3609570].

- **Stationarity (Invariance)**: A distribution $\pi$ is said to be stationary or invariant with respect to a transition kernel $K$ if, once the chain's state is distributed according to $\pi$, it remains so for all future steps. Formally, for any [measurable set](@entry_id:263324) of models $A$, $\int_{\mathcal{X}} \pi(dx) K(x, A) = \pi(A)$, where $\mathcal{X}$ is the state space. This means $\pi$ is a fixed point of the transition operator.

- **Detailed Balance (Reversibility)**: A sufficient, but not necessary, condition for stationarity is detailed balance. It is a stronger, microscopic condition stating that for a chain in its stationary state, the rate of transitions from any infinitesimal region $dx$ to another region $dy$ is equal to the rate of reverse transitions. Formally, this is an equality of measures: $\pi(dx) K(x, dy) = \pi(dy) K(y, dx)$. Most MCMC algorithms, including the ones discussed here, are constructed to satisfy detailed balance, as it provides a direct recipe for designing valid transition kernels.

- **Ergodicity**: For the chain to be guaranteed to converge to $\pi$ as its unique stationary distribution, regardless of its starting point, it must be ergodic. Ergodicity is comprised of two properties:
    - **Irreducibility**: The chain must be able to reach any "significant" region of the state space from any starting point, eventually. This ensures the sampler does not get permanently stuck in a subset of the parameter space and can, in principle, explore all regions with non-zero posterior probability.
    - **Aperiodicity**: The chain must not be trapped in deterministic cycles. For example, it should not be restricted to visiting a sequence of states $A \to B \to C \to A \to \dots$. Aperiodicity ensures the chain mixes properly and does not exhibit such periodic behavior.

A Markov chain that has a stationary distribution $\pi$ and is ergodic will, for any suitable function $f(m)$, produce sample averages that converge to the true posterior expectation:
$\lim_{N \to \infty} \frac{1}{N} \sum_{t=1}^N f(X_t) = \mathbb{E}_{\pi}[f(m)] = \int f(m) \pi(m) dm$

This [ergodic theorem](@entry_id:150672) is the cornerstone of MCMC, justifying the use of sample averages to estimate posterior properties.

### Foundational MCMC Algorithms

#### The Metropolis-Hastings Algorithm

The **Metropolis-Hastings (M-H) algorithm** is the archetypal MCMC method. It provides a general recipe for constructing a transition kernel that satisfies detailed balance with respect to a target distribution $\pi(m)$, even when $\pi(m)$ is only known up to a [normalizing constant](@entry_id:752675). The procedure at each step $t$ is:
1.  Given the current state $m^{(t)}$, propose a new candidate state $m'$ by drawing from a **[proposal distribution](@entry_id:144814)** $q(m'|m^{(t)})$.
2.  Calculate the **acceptance probability**, $\alpha(m^{(t)}, m')$.
3.  Draw a uniform random number $u \sim U(0,1)$. If $u  \alpha(m^{(t)}, m')$, accept the proposal and set $m^{(t+1)} = m'$. Otherwise, reject the proposal and set $m^{(t+1)} = m^{(t)}$.

The genius of the M-H algorithm lies in the form of the acceptance probability, which is derived directly from the detailed balance condition:
$\alpha(m, m') = \min\left(1, \frac{\pi(m') q(m|m')}{\pi(m) q(m'|m)}\right)$
Notice that the (often unknown) [normalizing constant](@entry_id:752675) of $\pi$ appears in both the numerator and denominator and thus cancels out. This makes the algorithm perfectly suited for Bayesian inference.

A simple variant is the **Independence Sampler**, where the proposal distribution is fixed and does not depend on the current state: $q(m'|m) = q(m')$. In this case, the acceptance probability simplifies to [@problem_id:3609527]:
$$\alpha(m, m') = \min\left(1, \frac{\pi(m')q(m)}{\pi(m)q(m')}\right) = \min\left(1, \frac{w(m')}{w(m)}\right)$$
where $w(m) = \pi(m)/q(m)$ are the [importance weights](@entry_id:182719). For this sampler to be efficient, the proposal density $q$ must be a good approximation of the target posterior $\pi$. An ideal choice for $q$ would minimize the distance to $\pi$, for instance by minimizing the **Kullback-Leibler (KL) divergence** $D_{\mathrm{KL}}(\pi \,\|\, q)$. However, constructing such a proposal requires detailed knowledge of $\pi$, which is precisely what we lack. This "chicken-and-egg" problem makes the design of a universally efficient [independence sampler](@entry_id:750605) practically infeasible for complex geophysical posteriors.

#### The Gibbs Sampler

The **Gibbs sampler** is another powerful MCMC algorithm, particularly effective for high-dimensional problems where the parameter vector $m$ can be broken down into blocks of components. For a two-component model $m=(\theta, \phi)$, a Gibbs sampling iteration consists of two steps [@problem_id:3609553]:
1.  Draw a new value $\theta^{(t+1)}$ from its **[full conditional distribution](@entry_id:266952)**: $\theta^{(t+1)} \sim p(\theta | \phi^{(t)}, d)$.
2.  Draw a new value $\phi^{(t+1)}$ from its [full conditional distribution](@entry_id:266952), conditioned on the newly drawn value of $\theta$: $\phi^{(t+1)} \sim p(\phi | \theta^{(t+1)}, d)$.

Each of these draws can be seen as a Metropolis-Hastings step with a specific proposal that is always accepted, thus making the algorithm computationally efficient. The sequence of pairs $\{(\theta^{(t)}, \phi^{(t)})\}$ forms a Markov chain whose [stationary distribution](@entry_id:142542) is the joint posterior $p(\theta, \phi | d)$.

The practical utility of Gibbs sampling hinges on our ability to sample from the full conditional distributions. This is often possible in hierarchical Bayesian models that employ **[conjugate priors](@entry_id:262304)**. A prior is conjugate to a likelihood if the resulting posterior belongs to the same family of distributions as the prior. For instance, in a linear-Gaussian model with an unknown precision parameter $\phi$, if we place a Gaussian prior on the model parameters $\theta$ (conditional on $\phi$) and a Gamma prior on $\phi$, the full conditional for $\theta$ will be Gaussian and the full conditional for $\phi$ will be Gamma. Since we can draw samples from Gaussian and Gamma distributions easily, Gibbs sampling is highly efficient in this conjugate setting [@problem_id:3609553].

Even without conjugacy, [exact sampling](@entry_id:749141) from a full conditional is possible if it is, for example, a univariate **log-concave** distribution. In such cases, methods like **Adaptive Rejection Sampling (ARS)** can generate exact samples without requiring knowledge of the [normalizing constant](@entry_id:752675). If a full conditional cannot be sampled directly, a Metropolis-Hastings step can be embedded within the Gibbs framework to sample that component, a strategy known as Metropolis-within-Gibbs.

### Trans-Dimensional Sampling: The Reversible Jump Algorithm

A central challenge in geophysical [model selection](@entry_id:155601) is that the model's complexity is often unknown. For example, when inverting for a 1-D layered Earth structure, the number of layers, $k$, is a parameter to be inferred from the data. The dimension of the parameter vector $m_k$ (containing layer depths and velocities) depends on $k$. The full state space is a union of subspaces of varying dimension: $\mathcal{X} = \bigcup_k \{k\} \times \mathbb{R}^{d_k}$.

Standard MCMC algorithms operate on a fixed-dimensional space. **Reversible Jump MCMC (RJMCMC)** extends the Metropolis-Hastings framework to handle these trans-dimensional problems. RJMCMC allows the Markov chain to "jump" between subspaces of different dimensionality while preserving detailed balance across the entire composite state space [@problem_id:3609576].

The key innovation is the design of moves between a model $m_k$ of dimension $d_k$ and a model $m_{k'}$ of dimension $d_{k'}$. To propose such a move, we first augment the current state $m_k$ with an [auxiliary random variable](@entry_id:270091) $u$, drawn from a [proposal distribution](@entry_id:144814) $g(u)$. Then, a deterministic and [invertible function](@entry_id:144295)—a **[bijection](@entry_id:138092)**—$T$ maps the augmented state $(m_k, u)$ to a new state $(m_{k'}, u')$. For this to be a valid [bijection](@entry_id:138092), the dimensions of the source and destination spaces must match. This is the **dimension matching condition**:

$$d_k + \dim(u) = d_{k'} + \dim(u')$$

The acceptance probability for this trans-dimensional move must account for the change in volume associated with the mapping. This is accomplished by including the absolute determinant of the **Jacobian matrix** of the transformation in the M-H ratio:

$$\alpha = \min\left(1, \frac{p(m_{k'}|d)}{p(m_k|d)} \frac{q(k \to k')}{q(k' \to k)} \frac{g_{k' \to k}(u')}{g_{k \to k}(u)} \left| \det\left(\frac{\partial(m_{k'}, u')}{\partial(m_k, u)}\right) \right| \right)$$

For a simple "birth" move that adds a new scalar parameter, we might propose $k' = k+1$. We draw a single auxiliary variable $u \sim g(u)$ (so $\dim(u)=1$) and define the new parameter vector by simple concatenation: $m_{k'} = (m_k, u)$. In this case, no auxiliary variable $u'$ is needed for the reverse move, so $\dim(u')=0$. The dimension matching condition $d_k + 1 = (d_k+1) + 0$ is satisfied. The [bijection](@entry_id:138092) is $T(m_k, u) = m_{k'}$, and its Jacobian determinant is simply 1, simplifying the acceptance ratio [@problem_id:3609576]. Designing effective bijections and proposal distributions is the primary challenge in implementing RJMCMC.

### Enhancing Sampler Performance

Geophysical posterior distributions are notoriously complex, often exhibiting multiple, well-separated modes (corresponding to distinct but data-consistent physical interpretations) and strong parameter correlations. Standard MCMC samplers can easily become trapped in a single mode, failing to explore the full posterior and producing biased results. **Parallel Tempering (PT)**, also known as Metropolis-Coupled MCMC, is an advanced technique designed to overcome this challenge.

The method involves running an ensemble of $N$ MCMC chains in parallel, each targeting a slightly different distribution. These distributions are constructed by "heating" the posterior using an inverse temperature parameter $\beta \in [0,1]$. A common formulation for this family of **[tempered distributions](@entry_id:193859)** is [@problem_id:3609567]:

$$p_\beta(m) \propto p(d|m)^\beta p(m)$$

The chain with $\beta=1$ is the "cold" chain and samples from the true target posterior. Chains with $\beta  1$ are "hotter". As $\beta \to 0$, the likelihood term is flattened ($p(d|m)^0=1$), and the distribution approaches the prior $p(m)$. In this high-temperature limit, the energy landscape is smooth, and the chain can easily traverse the [parameter space](@entry_id:178581), moving between modes that are separated by high energy barriers (low likelihood regions) for the cold chain.

To transfer this exploratory power to the cold chain, PT introduces a new type of move: a **swap** of the entire states between two adjacent chains, say chain $i$ at $\beta_i$ and chain $j$ at $\beta_j$. To maintain detailed balance for the entire ensemble, this swap is treated as a Metropolis-Hastings proposal and is accepted with probability:

$$a_{\text{swap}} = \min\left(1, \frac{p_{\beta_i}(m_j) p_{\beta_j}(m_i)}{p_{\beta_i}(m_i) p_{\beta_j}(m_j)}\right) = \min\left(1, [p(d|m_i)]^{\beta_j - \beta_i} [p(d|m_j)]^{\beta_i - \beta_j}\right)$$

By allowing well-fitting models found by hot chains to "cool down" and be passed to the target chain, [parallel tempering](@entry_id:142860) dramatically improves mixing and ensures a more complete exploration of multimodal and trans-dimensional posteriors.

### Post-Processing: Convergence and Efficiency Analysis

After running an MCMC simulation, two critical questions must be addressed: Has the chain converged to the stationary distribution? And how many [independent samples](@entry_id:177139) have we actually obtained?

#### Convergence Diagnostics

We can never prove that a finite-length chain has converged. We can, however, use diagnostics to detect a lack of convergence. The **Gelman-Rubin diagnostic**, or [potential scale reduction factor](@entry_id:753645) ($\hat{R}$), is a widely used method that requires running multiple chains ($m \ge 2$) from different, overdispersed starting points [@problem_id:3609590].

The core idea is to compare the variance *within* each chain to the variance *between* the chains. If all chains are sampling from the same stationary distribution, these two sources of variance should be comparable. If they have not converged, the between-chain variance will be significantly larger. For a scalar summary of the model, $Y=f(X)$, the procedure is:
1.  Compute the mean within-chain variance, $W = \frac{1}{m}\sum_i s_i^2$, where $s_i^2$ is the sample variance of chain $i$.
2.  Compute the between-chain variance, $B = \frac{n}{m-1}\sum_i (\bar{Y}_i - \bar{Y})^2$, where $n$ is the chain length, $\bar{Y}_i$ is the mean of chain $i$, and $\bar{Y}$ is the grand mean.
3.  Estimate the [pooled variance](@entry_id:173625) of the posterior, $\hat{V} = \frac{n-1}{n}W + \frac{1}{n}B$. This is a weighted average of $W$ and $B$.
4.  The [potential scale reduction factor](@entry_id:753645) is then $\hat{R} = \sqrt{\frac{\hat{V}}{W}}$.

As the chains converge, $B$ approaches $W$, and $\hat{R}$ approaches 1. A value of $\hat{R}$ substantially greater than 1 (e.g., > 1.1) is taken as evidence of non-convergence. This diagnostic is particularly useful in trans-dimensional problems, where it can be applied to any scalar quantity of interest that is well-defined across all model dimensions (e.g., Moho depth).

#### Sample Efficiency

MCMC samples are, by construction, correlated. A state $X_{t+1}$ is highly dependent on $X_t$. This correlation reduces the amount of independent information in the chain. The degree of correlation is measured by the **autocorrelation function**, $\rho_k = \operatorname{Corr}(f(X_t), f(X_{t+k}))$.

The **Integrated Autocorrelation Time (IAT)**, denoted $\tau_{\text{int}}$, quantifies the effective number of iterations required to produce one independent sample [@problem_id:3609522]. It is defined as:

$\tau_{\text{int}} = 1 + 2 \sum_{k=1}^{\infty} \rho_k$

A large $\tau_{\text{int}}$ indicates high correlation and an inefficient sampler. The variance of the sample mean $\overline{f}_N$ from a chain of $N$ samples is approximately $\frac{\operatorname{Var}_{\pi}(f)}{N/\tau_{\text{int}}}$. This leads to the definition of the **Effective Sample Size (ESS)**:

$\text{ESS} = \frac{N}{\tau_{\text{int}}}$

The ESS is the number of [independent samples](@entry_id:177139) that would yield the same statistical power as our $N$ correlated samples. It is the "true" number of samples we have for quantifying uncertainty. For example, for a chain of length $N=40000$ where the [autocorrelation](@entry_id:138991) decays like $\rho_k = 0.92^k$, the IAT is $\tau_{\text{int}} = \frac{1+0.92}{1-0.92} = 24$. The [effective sample size](@entry_id:271661) is only $\text{ESS} = 40000/24 \approx 1667$, a drastic reduction from the nominal chain length [@problem_id:3609522].

### Bayesian Model Selection via Evidence Estimation

Beyond [parameter inference](@entry_id:753157) within a single model, a key goal of Bayesian analysis is to compare competing models. For example, is a 3-layer Earth model more plausible than a 4-layer model, given the data? Bayesian model selection answers this question by comparing the models' **marginal likelihoods**, or **[model evidence](@entry_id:636856)**, $p(d)$. The evidence is the [normalizing constant](@entry_id:752675) of the posterior, obtained by integrating the likelihood times the prior over the entire parameter space:

$$p(d) = \int p(d|m) p(m) dm$$

This high-dimensional integral is extremely challenging to compute. Several advanced Monte Carlo methods have been developed for this purpose, many of which leverage the same path of [tempered distributions](@entry_id:193859) used in [parallel tempering](@entry_id:142860).

#### Thermodynamic Integration

**Thermodynamic Integration (TI)** recasts the evidence calculation as a one-dimensional integral over the inverse temperature $\beta$. By differentiating the logarithm of the tempered [normalizing constant](@entry_id:752675) $Z(\beta) = \int p(d|m)^\beta p(m) dm$ and integrating from $\beta=0$ to $\beta=1$, one arrives at the fundamental TI identity [@problem_id:3609574]:

$\log p(d) = \int_{0}^{1} \mathbb{E}_{p_{\beta}}[\log p(d|m)] d\beta$

This remarkable result transforms a difficult [multi-dimensional integration](@entry_id:142320) problem into a tractable one-dimensional one. In practice, we can run MCMC simulations at a series of discrete temperatures $\beta_i \in [0,1]$, estimate the expected [log-likelihood](@entry_id:273783) $\mathbb{E}_{p_{\beta_i}}[\log p(d|m)]$ from the samples at each temperature, and then use numerical quadrature (e.g., the trapezoidal or Simpson's rule) to approximate the integral. The accuracy of this method depends on having a sufficiently dense ladder of temperatures, especially in regions where the integrand $\mathbb{E}_{p_{\beta}}[\log p(d|m)]$ changes rapidly. Since the slope of the integrand is equal to the variance of the log-likelihood, $\text{Var}_{p_\beta}(\log p(d|m))$, the temperature ladder should be refined in regions of high variance to ensure both accurate quadrature and efficient mixing for the underlying [parallel tempering](@entry_id:142860) simulation [@problem_id:3609574].

#### Stepping-Stone and Bridge Sampling

**Stepping-stone (SS) sampling** and **[bridge sampling](@entry_id:746983) (BS)** are two powerful and related methods for evidence estimation [@problem_id:3609533].

Stepping-stone sampling expresses the evidence $p(d) = Z_1$ as a telescoping product of ratios of normalizing constants along the temperature path:

$$p(d) = Z_1 = \frac{Z_{\beta_K}}{Z_{\beta_{K-1}}} \frac{Z_{\beta_{K-1}}}{Z_{\beta_{K-2}}} \dots \frac{Z_{\beta_1}}{Z_{\beta_0}} Z_{\beta_0}$$

Since $Z_0=1$, the problem reduces to estimating each ratio $r_k = Z_{\beta_k}/Z_{\beta_{k-1}}$. Each such ratio can be written as an expectation with respect to the distribution at the preceding temperature, $p_{\beta_{k-1}}$, which is readily estimated from MCMC output. By breaking the large gap between the prior ($\beta=0$) and the posterior ($\beta=1$) into many small, overlapping "stones," the method provides a robust estimate, particularly for challenging posteriors where a direct bridge from prior to posterior would fail.

Bridge sampling provides a more general identity for the ratio of two normalizing constants, but often in practice it is used to bridge the prior and posterior directly. Its performance is critically dependent on the overlap between the two distributions.

The choice between these methods depends on the nature of the problem. For rugged, multi-modal geophysical posteriors with poor overlap between the prior and posterior, stepping-stone sampling with a dense ladder of temperatures is generally more robust and less biased than a single-stage bridge sampler. Conversely, for well-behaved, unimodal posteriors with good prior-posterior overlap (as might be found in a linearized inversion), a well-tuned [bridge sampling](@entry_id:746983) estimator can be more statistically efficient, achieving lower variance for a fixed computational cost [@problem_id:3609533]. Both methods are applicable to trans-dimensional problems, but their accuracy is contingent on the MCMC sampler's ability to effectively mix between different model dimensions.