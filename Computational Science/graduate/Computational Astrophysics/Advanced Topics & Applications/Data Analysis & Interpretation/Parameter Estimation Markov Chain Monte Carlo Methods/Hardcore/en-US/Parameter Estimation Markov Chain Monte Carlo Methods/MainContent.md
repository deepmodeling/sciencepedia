## Introduction
Parameter estimation is a fundamental task in the quantitative sciences, allowing us to constrain the theories that describe our universe by confronting them with data. However, a single best-fit value is rarely sufficient; a rigorous scientific conclusion requires a complete characterization of the uncertainty associated with those parameters. The Bayesian framework provides a principled way to achieve this by framing the problem as one of inferring the posterior probability distribution. For any realistically complex model, this posterior is a high-dimensional, non-analytic function that defies direct computation. This intractability presents a significant knowledge gap between the theoretical elegance of Bayesian inference and its practical application.

This article bridges that gap by providing a deep dive into Markov Chain Monte Carlo (MCMC) methods, the computational engine that has revolutionized modern statistical inference. You will learn how these algorithms enable us to explore and characterize complex posterior distributions, turning an intractable analytical problem into a feasible computational one. The following chapters are structured to build your expertise from the ground up. The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork, explaining the goals of Bayesian inference and detailing the inner workings of foundational MCMC algorithms like Metropolis-Hastings, Gibbs Sampling, and Hamiltonian Monte Carlo. Next, **Applications and Interdisciplinary Connections** demonstrates the versatility of this framework, showing how MCMC is adapted to solve challenging real-world problems, from building [hierarchical models](@entry_id:274952) of celestial populations to navigating the complex posterior landscapes of [biological networks](@entry_id:267733). Finally, **Hands-On Practices** will offer the opportunity to solidify your conceptual understanding through targeted problems designed to build practical intuition.

## Principles and Mechanisms

### The Goal: Characterizing the Posterior Distribution

In Bayesian [parameter estimation](@entry_id:139349), our objective extends beyond finding a single "best-fit" value for a set of model parameters, $\theta$. Instead, we aim to characterize the entire **[posterior probability](@entry_id:153467) distribution**, $p(\theta \mid D, M)$, which represents our complete state of knowledge about the parameters $\theta$ after observing the data $D$, given a model $M$. This distribution is furnished by Bayes' theorem:

$$
p(\theta \mid D, M) = \frac{p(D \mid \theta, M) p(\theta)}{p(D \mid M)}
$$

This fundamental equation combines two key sources of information. The first is the **likelihood**, $p(D \mid \theta, M)$, which quantifies the probability of observing the data $D$ if the true parameters were $\theta$. It encapsulates our understanding of the data-generation process, including the physical model and the statistical properties of the measurement noise. For instance, if we measure spectrophotometric fluxes of a galaxy, the likelihood function would describe how the observed fluxes are expected to be distributed around the theoretical fluxes predicted by a galaxy model with parameters $\theta$ .

The second component is the **prior distribution**, $p(\theta)$, which encodes our knowledge about the parameters *before* considering the new data. This prior knowledge can stem from established physical laws, results from previous experiments, or constraints on plausibility. The [posterior distribution](@entry_id:145605) is thus a principled synthesis of prior knowledge and new evidence. Since the denominator, $p(D \mid M)$, known as the **marginal likelihood** or **evidence**, is a constant with respect to $\theta$, we often work with the unnormalized posterior:

$$
p(\theta \mid D, M) \propto p(D \mid \theta, M) p(\theta)
$$

The evidence term $p(D \mid M) = \int p(D \mid \theta, M) p(\theta) \, d\theta$ involves an integration over the entire [parameter space](@entry_id:178581). In models with more than a few parameters, this integral is almost always computationally intractable. This intractability is a primary motivation for turning to [sampling methods](@entry_id:141232), which allow us to characterize the posterior distribution without ever needing to compute its normalization constant.

### The Role of Priors: Guiding and Grounding Inference

The choice of a prior distribution is a defining feature of Bayesian modeling. Priors can be broadly categorized by the degree of information they incorporate.

An **informative prior** injects substantial, specific information into the analysis. For example, if we are estimating a flux normalization parameter $A$ and a previous, highly precise experiment determined it to be near a value $A_0$ with a small uncertainty $\tau$, we could encapsulate this with an informative Gaussian prior, such as $A \sim \mathcal{N}(A_0, \tau^2)$ . When combined with a Gaussian likelihood, such a prior leads to a Gaussian posterior whose mean is a precision-weighted average of the prior mean and the maximum likelihood estimate, elegantly blending old and new information.

Often, however, we wish for the data to dominate the inference. In such cases, we might opt for a **weakly informative** or **uninformative prior**. A common choice is a [uniform distribution](@entry_id:261734) over a wide range of plausible values. Sometimes, this range is taken to be infinite, resulting in an **improper prior**—one that does not integrate to a finite value. While often useful, [improper priors](@entry_id:166066) must be handled with care. The product of a likelihood and an improper prior may not result in a **proper posterior**; that is, the posterior itself may not be normalizable to a valid probability distribution.

Consider estimating a Poisson count rate $\lambda$ from a set of photon counts . A common improper prior for a [rate parameter](@entry_id:265473) is the Jeffreys prior $\pi(\lambda) \propto \lambda^{-1/2}$ (for the Poisson case) or sometimes $\pi(\lambda) \propto \lambda^{-1}$. If we adopt the latter and observe a total of zero counts ($N=0$), the unnormalized posterior becomes $p(\lambda \mid N=0, T) \propto \lambda^{-1} \exp(-\lambda T)$. This function is not integrable over $\lambda \in (0, \infty)$ because it diverges as $\ln(\lambda)$ near $\lambda=0$. The posterior is improper, and no valid probabilistic inference can be drawn. This demonstrates a critical check in any Bayesian analysis: one must ensure the posterior is proper, which means its integral over the parameter space converges. This is typically achieved if the data are sufficiently informative or if the prior is chosen to guarantee [integrability](@entry_id:142415), such as a Gamma prior, $\pi(\lambda) \propto \lambda^{\alpha-1}\exp(-\beta \lambda)$, which for $\alpha > 0$ and $\beta \ge 0$ ensures a proper posterior for any non-negative [count data](@entry_id:270889) .

A special class of [uninformative priors](@entry_id:172418) are **Jeffreys priors**, defined by $p(\theta) \propto \sqrt{I(\theta)}$, where $I(\theta)$ is the **Fisher information** matrix. The Fisher information measures how much information the data are expected to provide about the parameter $\theta$. The principal virtue of the Jeffreys prior is its **invariance under [reparameterization](@entry_id:270587)**. This means that the substantive results of an inference do not depend on an arbitrary choice of how the parameters are defined. For instance, if one derives the Jeffreys prior for a parameter $A$ and then transforms it to a new parameter $B = g(A)$, the result is the same as deriving the Jeffreys prior for $B$ directly . This is not true for a simple uniform prior; a uniform prior on $A$ implies a non-uniform prior on $B = \ln(A)$, and vice versa. This invariance property makes the Jeffreys prior a principled choice for an objective [reference prior](@entry_id:171432).

### The Challenge of Nuisance Parameters

Astrophysical models rarely contain only the parameters we are directly interested in. They often include **[nuisance parameters](@entry_id:171802)**, which are necessary for a correct description of the data but are not the primary object of inquiry. A common example is an uncertain instrument calibration factor, $\gamma$, that affects all measurements .

A key strength of the Bayesian framework is its systematic approach to handling such parameters. Uncertainty about a [nuisance parameter](@entry_id:752755) is propagated into the final uncertainty of the parameters of interest through the process of **[marginalization](@entry_id:264637)**. If our full parameter space is $(\theta, \gamma)$, we find the posterior for our parameters of interest, $\theta$, by integrating the joint posterior over all possible values of the [nuisance parameter](@entry_id:752755) $\gamma$:

$$
p(\theta \mid D, M) = \int p(\theta, \gamma \mid D, M) \, d\gamma = \int p(\theta \mid \gamma, D, M) p(\gamma \mid D, M) \, d\gamma
$$

This integral averages the conditional posterior for $\theta$ over the [posterior distribution](@entry_id:145605) of $\gamma$, effectively weighting each possible value of the [nuisance parameter](@entry_id:752755) by its plausibility in light of the data and prior. This ensures that our final uncertainty on $\theta$ fully accounts for our uncertainty in $\gamma$. This contrasts with some frequentist methods where [nuisance parameters](@entry_id:171802) might be fixed at a best-fit value (a "plug-in" estimate) or profiled out, approaches which can lead to an underestimate of the true uncertainty.

### Introduction to Markov Chain Monte Carlo (MCMC)

The combination of high-dimensional parameter spaces, complex likelihoods, and the need for [marginalization](@entry_id:264637) means that analytical solutions for the posterior distribution are available only in the simplest of cases. This is where computational methods, and specifically Markov Chain Monte Carlo (MCMC), become indispensable.

MCMC is a class of algorithms designed to draw samples from a probability distribution, even when that distribution is known only up to a normalization constant. This is perfectly suited to our problem, where the posterior $p(\theta \mid D) \propto p(D \mid \theta) p(\theta)$ is easy to evaluate pointwise, but the normalizing evidence $p(D)$ is not. The core idea of MCMC is to construct a "random walk," or a **Markov chain**, in the [parameter space](@entry_id:178581). This walk is designed to have the target [posterior distribution](@entry_id:145605) as its unique stationary distribution. After an initial "burn-in" period, the points visited by the chain, $\{\theta_1, \theta_2, \dots, \theta_N\}$, can be treated as a set of (correlated) samples drawn from the posterior. This collection of samples provides a rich, empirical representation of the full posterior distribution, from which we can compute [summary statistics](@entry_id:196779), visualize marginal distributions, and quantify uncertainties.

### Theoretical Foundations of MCMC

For MCMC results to be reliable, the underlying Markov chain must possess certain theoretical properties that guarantee its convergence to the target posterior distribution, $\pi(\theta) = p(\theta \mid D)$, from any starting point. These properties are formally defined in [measure theory](@entry_id:139744) .

A **Markov chain** is a stochastic process where the next state depends only on the current state, not on the sequence of states that preceded it. For a [continuous state space](@entry_id:276130), its evolution is described by a **transition kernel**, $P(x, A)$, which gives the probability of moving from state $x$ to a set $A$. For an MCMC sampler to be valid, we construct a kernel $P$ that leaves our target posterior $\pi$ invariant, meaning $\int P(x,A) \pi(dx) = \pi(A)$. Furthermore, to ensure the chain converges to $\pi$ as its unique [stationary distribution](@entry_id:142542) from any starting point, it must satisfy three key conditions:

1.  **Irreducibility**: The chain must be able to reach any region of the [parameter space](@entry_id:178581) that has a non-zero [posterior probability](@entry_id:153467). More formally, for a reference measure $\psi$ (typically $\pi$ itself), a chain is $\psi$-irreducible if from any starting point $x$, it has a non-zero probability of eventually entering any set $A$ where $\psi(A) > 0$. This ensures the sampler can explore the entire posterior support and will not get permanently trapped in a local region.

2.  **Aperiodicity**: The chain must not be trapped in deterministic cycles. If a chain could only visit a certain region at steps $2, 4, 6, \dots$, its distribution could never converge to a single stationary state. Aperiodicity forbids such periodic behavior.

3.  **Harris Recurrence**: A $\psi$-[irreducible chain](@entry_id:267961) is Harris recurrent if it is guaranteed to return to any set $A$ with $\psi(A) > 0$ with probability one, regardless of its starting point. This is a stronger condition than simple recurrence and ensures that the chain does not just pass through a region once but explores it thoroughly over time.

A chain that is $\pi$-invariant, irreducible, aperiodic, and Harris recurrent is said to be **ergodic**. The **Ergodic Theorem** for Markov chains is the cornerstone of MCMC. It guarantees that, for a sufficiently long chain, the average of a function $f(\theta)$ over the samples will converge to the expectation of that function under the [posterior distribution](@entry_id:145605):

$$
\lim_{N \to \infty} \frac{1}{N} \sum_{i=1}^{N} f(\theta_i) = \mathbb{E}_{\pi}[f(\theta)] = \int f(\theta) \pi(\theta) \, d\theta
$$

This powerful result allows us to approximate any desired posterior expectation—such as the mean, variance, or [credible intervals](@entry_id:176433) of our parameters—by simply computing averages over our MCMC samples.

### Mechanisms of MCMC: Core Algorithms

All MCMC algorithms provide a recipe for constructing a transition kernel that satisfies the conditions for ergodicity. We will explore three of the most important families of algorithms.

#### The Metropolis-Hastings Algorithm

The Metropolis-Hastings (M-H) algorithm is the foundational MCMC method. It provides a general framework for constructing a valid sampler given the ability to evaluate the (unnormalized) target density $\pi(\theta)$. The M-H step proceeds as follows:

1.  Given the current state $\theta$, draw a candidate state $\theta'$ from a **[proposal distribution](@entry_id:144814)** $q(\theta' \mid \theta)$.
2.  Calculate the **acceptance ratio**:
    $$
    r(\theta \to \theta') = \frac{\pi(\theta') q(\theta \mid \theta')}{\pi(\theta) q(\theta' \mid \theta)}
    $$
3.  Generate a uniform random number $u \sim U(0,1)$. If $u  r$, the proposal is accepted, and the next state is $\theta'$. Otherwise, the proposal is rejected, and the chain remains at $\theta$.

The acceptance ratio is a product of three terms: the ratio of posterior densities at the proposed and current points, and the ratio of proposal densities. The latter term corrects for any asymmetry in the proposal distribution. A common and simple choice is a [symmetric proposal](@entry_id:755726), such as a Gaussian random walk where $q(\theta' \mid \theta) = \mathcal{N}(\theta'; \theta, \Sigma)$. In this case, $q(\theta \mid \theta') = q(\theta' \mid \theta)$, the proposal ratio cancels, and the acceptance ratio simplifies to just the ratio of posterior densities, $r = \pi(\theta') / \pi(\theta)$.

Let's see this in action with a concrete astrophysical example: inferring the log-amplitude $\theta$ of a source from Poisson photon counts . The posterior is $\pi(\theta) \propto p(\mathbf{n} \mid \theta) p(\theta)$, where $p(\mathbf{n} \mid \theta)$ is a product of Poisson likelihoods and $p(\theta)$ is a Gaussian prior. The acceptance ratio for a [symmetric proposal](@entry_id:755726) is:

$$
r = \frac{p(\mathbf{n} \mid \theta') p(\theta')}{p(\mathbf{n} \mid \theta) p(\theta)} = \left[ \frac{p(\mathbf{n} \mid \theta')}{p(\mathbf{n} \mid \theta)} \right] \left[ \frac{p(\theta')}{p(\theta)} \right]
$$

The likelihood ratio and prior ratio can be computed separately. For the Poisson likelihood $p(\mathbf{n} \mid \theta) = \prod_i \frac{\mu_i(\theta)^{n_i} \exp(-\mu_i(\theta))}{n_i!}$, the ratio simplifies to a form involving products and sums over the energy bins. For the Gaussian prior $p(\theta) \propto \exp(-(\theta-\mu_0)^2 / 2\tau^2)$, the ratio is an exponential of the difference of squares. Combining these yields the full acceptance ratio, which can be computed at each step to decide whether to move to the proposed point. This mechanism ensures that moves to regions of higher posterior density are always accepted, while moves to regions of lower density are accepted probabilistically, allowing the chain to explore the full distribution.

#### Gibbs Sampling

Gibbs sampling is a special case of the Metropolis-Hastings algorithm that is particularly efficient when the parameter vector $\boldsymbol{\theta}$ can be broken down into blocks or individual components for which the **full conditional distributions** are easy to sample from . The full conditional for a parameter $\theta_i$ is its distribution given the data and all other parameters, $p(\theta_i \mid \boldsymbol{\theta}_{-i}, D)$, where $\boldsymbol{\theta}_{-i}$ denotes all components of $\boldsymbol{\theta}$ except for $\theta_i$.

The Gibbs sampling algorithm proceeds by cycling through the parameters. At each step $i$, it draws a new value for $\theta_i$ directly from its full conditional:

$$
\theta_i^{(t+1)} \sim p(\theta_i \mid \theta_1^{(t+1)}, \dots, \theta_{i-1}^{(t+1)}, \theta_{i+1}^{(t)}, \dots, \theta_d^{(t)}, D)
$$

Because the [proposal distribution](@entry_id:144814) is the true [conditional distribution](@entry_id:138367), the [acceptance probability](@entry_id:138494) in the M-H framework is always 1. This makes the algorithm highly efficient, provided the full conditionals are known and samplable. To find the functional form of a full conditional, one simply inspects the joint posterior $p(\boldsymbol{\theta} \mid D)$ and treats all factors not involving $\theta_i$ as part of the normalization constant.

This process is especially powerful in models exhibiting **conjugacy**. A prior is conjugate to a likelihood if the resulting posterior is in the same family of distributions as the prior. For example, in a hierarchical Gaussian model for stellar velocities, if the variance $\sigma^2$ has an Inverse-Gamma prior and the mean $\mu$ has a Normal prior, the full conditionals $p(\mu \mid \sigma^2, D)$ and $p(\sigma^2 \mid \mu, D)$ are also Normal and Inverse-Gamma, respectively . This allows for direct, efficient Gibbs updates.

Even when a model is not fully conjugate, **[data augmentation](@entry_id:266029)** can sometimes restore conditional [conjugacy](@entry_id:151754). This technique introduces latent (unobserved) variables into the model to simplify the conditional dependencies. For example, in an X-ray counting model where the observed counts are a sum of source and background events, $y_n \sim \mathrm{Poisson}(e_n s + e_n b)$, the full conditionals for the source rate $s$ and background rate $b$ are not simple Gamma distributions. However, by introducing [latent variables](@entry_id:143771) $y_n^{(s)}$ representing the (unknown) number of source counts in each observation $y_n$, we can break the sum. The model becomes a Gibbs sampler that iterates through sampling $s$, $b$, and the latent allocations. The resulting full conditionals for $s$ and $b$ become standard Gamma distributions, which are trivial to sample from .

#### Hamiltonian Monte Carlo (HMC)

While powerful, simple M-H samplers with random-walk proposals can be inefficient in high dimensions, and Gibbs sampling requires knowledge of the full conditionals. **Hamiltonian Monte Carlo (HMC)** is a more sophisticated method that uses gradient information from the posterior to propose distant, high-acceptance-probability moves, dramatically improving [sampling efficiency](@entry_id:754496).

HMC frames the sampling problem in the language of classical mechanics . The parameter vector $\theta$ is treated as the "position" of a particle, and we introduce an auxiliary "momentum" vector $p$. The system's dynamics are governed by a Hamiltonian $H(\theta, p) = U(\theta) + K(p)$, where the potential energy $U(\theta)$ is defined as the negative log-posterior, $U(\theta) = -\log \pi(\theta)$, and the kinetic energy is $K(p) = \frac{1}{2} p^\top M^{-1} p$ for some "mass matrix" $M$.

An HMC step involves:
1.  Drawing a random momentum $p$ from a Gaussian distribution, typically $\mathcal{N}(0, M)$.
2.  Simulating the evolution of $(\theta, p)$ for a finite time $T$ by integrating Hamilton's [equations of motion](@entry_id:170720). This is done numerically using a **[symplectic integrator](@entry_id:143009)**, such as the [leapfrog algorithm](@entry_id:273647), which takes $L$ steps of size $\epsilon$.
3.  The final state $(\theta', p')$ is used as a proposal. A Metropolis acceptance step is performed to correct for [numerical errors](@entry_id:635587) from the integration. Because the integrator is time-reversible and volume-preserving, the acceptance probability simplifies to $\min(1, \exp(-\Delta H))$, where $\Delta H = H(\theta', p') - H(\theta, p)$.

The efficiency of HMC depends on two key tuning parameters: the step size $\epsilon$ and the number of steps $L$.
- The **step size $\epsilon$** controls the accuracy of the numerical integration. Smaller $\epsilon$ leads to a smaller energy error $\Delta H$ and thus a higher acceptance rate, but requires more computation for a given trajectory length. Theoretical analysis shows that to maintain a constant acceptance rate in high dimensions ($d$), the step size must scale as $\epsilon \propto d^{-1/4}$ .
- The **trajectory length**, determined by $L$ (or total time $T = L\epsilon$), dictates how far the proposal is from the starting point. If $L$ is too small, HMC mimics a random walk. If $L$ is too large, the trajectory can curve back on itself and return near its starting point, an inefficient "U-turn" .

The difficulty of manually tuning $L$ for complex, anisotropic posteriors (common in cosmology, for example) motivated the development of the **No-U-Turn Sampler (NUTS)** . NUTS is an extension of HMC that automates the choice of trajectory length. It does this by building a trajectory and adaptively doubling its length, while constantly checking for a geometric U-turn. A U-turn is detected when the vector from the start of the trajectory to its end, $(q_t - q_0)$, points opposite to the current momentum, $p_t$. Formally, the condition is $(q_t - q_0)^\top M^{-1} p_t  0$. By stopping the trajectory just before it turns back, NUTS automatically finds an appropriate trajectory length that varies at each step, allowing for long, efficient moves in wide, flat regions of the posterior and shorter, careful steps in narrow, highly curved regions. This makes HMC a far more robust and automated tool for practical inference.

### Assessing Performance: Did the Sampler Work?

After running an MCMC sampler, we are left with a chain of samples $\{\theta_t\}_{t=1}^N$. A critical task is to diagnose whether this chain has converged to the posterior and is exploring it efficiently. Because of the way they are generated, successive samples in an MCMC chain are correlated. High correlation indicates that the chain is moving slowly and exploring the parameter space inefficiently, a phenomenon known as **slow mixing**.

We quantify this correlation using the **autocorrelation function**, $\rho_f(t)$, for a scalar quantity of interest $f(\theta)$. This function measures the correlation between samples that are $t$ steps apart in the chain. The overall effect of this correlation on the [statistical power](@entry_id:197129) of our sample is summarized by the **[integrated autocorrelation time](@entry_id:637326)**, $\tau_{\mathrm{int}}$ :

$$
\tau_{\mathrm{int}} = 1 + 2\sum_{t=1}^{\infty} \rho_f(t)
$$

The variance of the mean estimate $\bar{f}_N$ from our $N$ correlated samples is approximately $\mathrm{Var}(\bar{f}_N) \approx \frac{\sigma_f^2}{N} \tau_{\mathrm{int}}$, where $\sigma_f^2$ is the true posterior variance of $f$. This means the correlation inflates the variance of our estimates by a factor of $\tau_{\mathrm{int}}$. An [ideal chain](@entry_id:196640) of [independent samples](@entry_id:177139) would have $\tau_{\mathrm{int}} = 1$. A poorly mixing chain might have $\tau_{\mathrm{int}} \gg 1$.

This leads to the concept of the **Effective Sample Size (ESS)**:

$$
\mathrm{ESS} = \frac{N}{\tau_{\mathrm{int}}}
$$

The ESS represents the number of [independent samples](@entry_id:177139) that would provide the same statistical precision as our $N$ correlated samples. A low ESS (relative to $N$) is a clear sign of poor mixing and high [autocorrelation](@entry_id:138991), indicating that a longer chain is needed to achieve the desired precision. Monitoring $\tau_{\mathrm{int}}$ and ESS is therefore essential for any practical application of MCMC.

### Interpreting the Output: From Samples to Science

Once we are confident in our MCMC samples, we can use them to summarize the posterior distribution and report our scientific findings. A common way to summarize uncertainty is with a **[credible interval](@entry_id:175131)** (or credible region in higher dimensions) .

A $(1-\alpha)$ [credible interval](@entry_id:175131) is any interval $C$ that contains $(1-\alpha)$ of the posterior probability mass, i.e., $\int_C p(\theta \mid D) \,d\theta = 1-\alpha$. This definition is not unique. The simplest choice is the **[equal-tailed interval](@entry_id:164843)**, which is constructed from the $\alpha/2$ and $1-\alpha/2$ [quantiles](@entry_id:178417) of the posterior samples.

A more principled and often more informative choice is the **Highest Posterior Density (HPD)** interval. The HPD interval at level $(1-\alpha)$ is defined as the set of parameter values for which the posterior density exceeds some threshold $t$, where $t$ is chosen such that the region contains $(1-\alpha)$ of the total probability. By construction, any point inside an HPD interval has a higher posterior density than any point outside it. For a unimodal posterior, this means the HPD interval is the *shortest possible* credible interval at a given level.

For symmetric, unimodal posteriors, the equal-tailed and HPD intervals are identical. However, for the skewed posteriors common in astrophysical inference, they differ . The HPD interval will be asymmetric, adapting its bounds to cover the most probable region of the [parameter space](@entry_id:178581). It can be computed from MCMC samples either by finding the shortest interval containing $(1-\alpha)N$ of the samples, or by using stored log-posterior values to identify the $(1-\alpha)N$ samples with the highest posterior density. Importantly, this procedure does not require the (unknown) [normalization constant](@entry_id:190182) of the posterior . A further advantage of the HPD concept is its generalization to multimodal posteriors, where it can correctly identify a credible region as a union of disjoint intervals around multiple modes, a feature that quantile-based intervals would entirely miss.