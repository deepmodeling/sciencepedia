## Introduction
The estimation of normalizing constants—also known as partition functions—is a fundamental yet notoriously challenging task in many computational disciplines, including [statistical physics](@entry_id:142945), Bayesian statistics, and machine learning. These constants are essential for comparing models, calculating marginal likelihoods, and understanding the absolute scale of probability distributions. However, their computation involves [high-dimensional integrals](@entry_id:137552) that are analytically and numerically intractable. Standard Monte Carlo methods like importance sampling often fail dramatically in these settings, suffering from catastrophically high variance that renders their estimates useless.

This article introduces Annealed Importance Sampling (AIS), a powerful and versatile algorithm designed to overcome these limitations. AIS provides a robust framework for estimating ratios of normalizing constants by transforming a single, difficult estimation problem into a sequence of more manageable steps. By bridging a simple distribution to a complex one through a path of intermediate distributions, AIS controls variance and delivers reliable results.

Across the following sections, you will gain a comprehensive understanding of this technique. The **"Principles and Mechanisms"** section will lay the theoretical groundwork, deriving the AIS algorithm and proving its key property of unbiasedness. Next, **"Applications and Interdisciplinary Connections"** will showcase the practical utility of AIS, exploring its role in Bayesian [model selection](@entry_id:155601), [statistical physics](@entry_id:142945), and state-of-the-art [generative modeling](@entry_id:165487). Finally, the **"Hands-On Practices"** section offers a series of guided exercises to build your intuition and practical skills in implementing and analyzing the method.

## Principles and Mechanisms

The estimation of normalizing constants, or partition functions, is a central and notoriously difficult problem in [statistical physics](@entry_id:142945), Bayesian statistics, and machine learning. As outlined in the introduction, these constants are essential for [model comparison](@entry_id:266577), computing marginal likelihoods, and understanding the absolute scale of probability distributions. Annealed Importance Sampling (AIS) provides a powerful and versatile framework for this task. This chapter delves into the fundamental principles of AIS, deriving its mechanics from foundational concepts and exploring the theoretical and practical considerations that govern its performance.

### The Challenge of Normalizing Constants and the Limits of Basic Importance Sampling

Let us consider two distributions defined on a space $\mathcal{X} \subseteq \mathbb{R}^d$, represented by unnormalized densities $f_0(x)$ and $f_T(x)$. Their respective normalizing constants are $Z_0 = \int f_0(x) \,dx$ and $Z_T = \int f_T(x) \,dx$. Our objective is to compute the ratio $R = Z_T/Z_0$. Assume we can easily draw samples from the normalized base distribution, $p_0(x) = f_0(x)/Z_0$, and that the support of $p_T(x) = f_T(x)/Z_T$ is contained within the support of $p_0(x)$.

The principles of importance sampling provide a direct approach to estimating this ratio. The ratio $Z_T/Z_0$ can be expressed as an expectation under the base distribution $p_0(x)$:

$$
\frac{Z_T}{Z_0} = \frac{\int f_T(x) \,dx}{Z_0} = \int \frac{f_T(x)}{f_0(x)} \frac{f_0(x)}{Z_0} \,dx = \int \frac{f_T(x)}{f_0(x)} p_0(x) \,dx = \mathbb{E}_{p_0}\left[ \frac{f_T(X)}{f_0(X)} \right]
$$

This identity suggests a straightforward Monte Carlo estimator. By drawing $N$ [independent and identically distributed](@entry_id:169067) samples $X_1, \dots, X_N$ from $p_0(x)$, we can form the unbiased [importance sampling](@entry_id:145704) estimator:

$$
\widehat{R}_{\text{IS}} = \frac{1}{N} \sum_{i=1}^N \frac{f_T(X_i)}{f_0(X_i)}
$$

While elegant in theory, this estimator often proves deeply problematic in practice, particularly in high-dimensional settings. The variance of the estimator, which dictates its reliability, can be catastrophically large or even infinite. This high variance stems from two primary sources.

First, **mismatched tail behavior** can render the variance infinite [@problem_id:3288049]. For the variance of the estimator to be finite, the second moment of the importance weight $w(x) = f_T(x)/f_0(x)$ must be finite. That is, we require $\mathbb{E}_{p_0}[w(X)^2]  \infty$. Let's examine this condition:

$$
\mathbb{E}_{p_0}[w(X)^2] = \int \left(\frac{f_T(x)}{f_0(x)}\right)^2 p_0(x) \,dx = \frac{1}{Z_0} \int \frac{f_T(x)^2}{f_0(x)} \,dx
$$

If the [proposal distribution](@entry_id:144814) $p_0$ has lighter tails than the [target distribution](@entry_id:634522) $p_T$, the ratio $f_T(x)/f_0(x)$ will grow rapidly in the tails. The integral for the second moment may diverge. For instance, attempting to use a [standard normal distribution](@entry_id:184509) as a proposal for a Student-$t$ distribution (which has heavier, polynomial tails) results in an infinite-variance estimator [@problem_id:3288049].

Second, even when the variance is finite, it can grow exponentially with the dimension $d$, a manifestation of the **curse of dimensionality** [@problem_id:3288047]. If the densities have a product structure, $f_0(x) = \prod_{j=1}^d f_0^{(j)}(x_j)$ and $f_T(x) = \prod_{j=1}^d f_T^{(j)}(x_j)$, the overall importance weight is a product of per-dimension weights: $W = \prod_j w_j(X_j)$. The second moment of the total weight is the product of the second moments of the individual weights: $\mathbb{E}[W^2] = \prod_j \mathbb{E}[w_j^2]$. If there is even a modest mismatch between $f_0^{(j)}$ and $f_T^{(j)}$ such that $\mathbb{E}[w_j^2] > 1$ for many dimensions, the overall second moment $\mathbb{E}[W^2]$ will grow exponentially with $d$. This leads to a phenomenon called **[weight degeneracy](@entry_id:756689)**: the vast majority of samples will have weights close to zero, while a tiny fraction of samples will have enormous weights that dominate the sum. The resulting estimator is highly unstable and unreliable.

### Annealing as a Bridge Between Distributions

Annealed Importance Sampling (AIS) is designed to circumvent these issues by transforming a single, large, high-variance jump from $p_0$ to $p_T$ into a sequence of many small, low-variance steps. The core idea is to construct a **path** of intermediate distributions that smoothly interpolates between the base and the target.

Let us define a sequence of $K+1$ unnormalized densities, $\{f_k\}_{k=0}^K$, indexed by a parameter that we will call **inverse temperature**, following the convention in statistical physics. This sequence is constructed such that $f_0$ is our simple base density and $f_K$ is our complex target density. A widely used method for constructing such a path is the **geometric path**. Given a schedule of inverse temperatures $0 = \beta_0  \beta_1  \dots  \beta_K = 1$, we define the intermediate densities as a geometric mixture:

$$
f_{\beta_k}(x) = f_0(x)^{1-\beta_k} f_T(x)^{\beta_k}
$$

This construction ensures a smooth transition: when $\beta_k = 0$, we have $f_{\beta_0}(x) = f_0(x)$, and when $\beta_k = 1$, we have $f_{\beta_K}(x) = f_T(x)$. The ratio of normalizing constants can now be expressed as a telescoping product:

$$
\frac{Z_T}{Z_0} = \frac{Z_K}{Z_{K-1}} \frac{Z_{K-1}}{Z_{K-2}} \cdots \frac{Z_1}{Z_0} = \prod_{k=1}^{K} \frac{Z_k}{Z_{k-1}}
$$

where $Z_k$ is the [normalizing constant](@entry_id:752675) for $f_k \equiv f_{\beta_k}$. Each ratio in this product, $Z_k/Z_{k-1}$, can itself be estimated via importance sampling. If we can make each step sufficiently "small" by choosing a fine enough temperature schedule, the variance of each incremental estimation can be controlled. AIS operationalizes this concept in an elegant and powerful way.

### The Annealed Importance Sampling Algorithm

AIS can be understood as a form of [importance sampling](@entry_id:145704) on an extended path space. The algorithm generates a trajectory of states $(x_0, x_1, \dots, x_K)$ and computes a single importance weight for this entire path.

#### Path Generation and the AIS Weight

The AIS algorithm proceeds as follows [@problem_id:3288068] [@problem_id:3288069]:

1.  **Initialization**: Draw an initial state $x_0$ from the base distribution, $x_0 \sim \pi_0(x) = f_0(x)/Z_0$.

2.  **Annealing Schedule**: For $k = 1, \dots, K$:
    a.  Apply a Markov Chain Monte Carlo (MCMC) transition to the previous state. Let $T_k(\cdot | x_{k-1})$ be a Markov transition kernel that is constructed to leave the intermediate distribution $\pi_k(x) = f_k(x)/Z_k$ **invariant**.
    b.  The next state in the path, $x_k$, is a sample from this transition: $x_k \sim T_k(\cdot | x_{k-1})$.

Note a crucial subtlety in the standard AIS formulation: the kernel $T_k$ is applied to state $x_{k-1}$ to produce $x_k$. This means the state is "moved" *before* the importance weight for that step is calculated. The standard AIS importance weight for a single path is given by the product of incremental density ratios:

$$
W = \frac{f_1(x_0)}{f_0(x_0)} \cdot \frac{f_2(x_1)}{f_1(x_1)} \cdots \frac{f_K(x_{K-1})}{f_{K-1}(x_{K-1})} = \prod_{k=1}^{K} \frac{f_k(x_{k-1})}{f_{k-1}(x_{k-1})}
$$

The key insight is that the ratio for bridging from distribution $k-1$ to $k$ is evaluated at state $x_{k-1}$, the state generated from the *previous* stage of the [annealing](@entry_id:159359) run. Let's consider a concrete example using the geometric path [@problem_id:3288031]. The incremental weight ratio is:

$$
\frac{f_{\beta_k}(x_{k-1})}{f_{\beta_{k-1}}(x_{k-1})} = \frac{f_0(x_{k-1})^{1-\beta_k} f_T(x_{k-1})^{\beta_k}}{f_0(x_{k-1})^{1-\beta_{k-1}} f_T(x_{k-1})^{\beta_{k-1}}} = \left(\frac{f_T(x_{k-1})}{f_0(x_{k-1})}\right)^{\beta_k - \beta_{k-1}}
$$

The total weight is then $W = \prod_{k=1}^K \left(\frac{f_T(x_{k-1})}{f_0(x_{k-1})}\right)^{\Delta\beta_k}$, where $\Delta\beta_k = \beta_k - \beta_{k-1}$. Summing the exponents, which depend on the path $x_0, \dots, x_{K-1}$, we get $W = \exp\left( \sum_{k=1}^K \Delta\beta_k \log\left(\frac{f_T(x_{k-1})}{f_0(x_{k-1})}\right) \right)$.

For instance, if $f_0(x) = \exp(-x^2/2)$ and $f_T(x) = \exp(-(x-2)^2)$, with a schedule $\beta_0=0, \beta_1=0.3, \beta_2=0.6, \beta_3=1$ and a realized path $x_0=0.5, x_1=1.2, x_2=1.8$, the weight would be calculated as:
$W = \left(\frac{f_T(x_0)}{f_0(x_0)}\right)^{0.3} \left(\frac{f_T(x_1)}{f_0(x_1)}\right)^{0.3} \left(\frac{f_T(x_2)}{f_0(x_2)}\right)^{0.4} \approx 1.019$ [@problem_id:3288031].

#### The Unbiasedness Property

The most remarkable property of the AIS estimator is that, under the right conditions, it is **unbiased**. That is, the expectation of the weight $W$, taken over the distribution of generated paths, is exactly the desired ratio:

$$
\mathbb{E}[W] = \frac{Z_K}{Z_0}
$$

The proof of this property reveals the elegance of the algorithm's construction [@problem_id:3288132] [@problem_id:3288069]. The key ingredient is the **invariance** of the Markov kernels. The condition is that for each $k \in \{1, \dots, K\}$, the kernel $T_k$ must leave the distribution $\pi_k$ invariant: $\int \pi_k(x) T_k(x'|x) dx = \pi_k(x')$. This is a weaker condition than reversibility (detailed balance), which is often used to construct such kernels but is not strictly necessary for unbiasedness.

The expectation of $W$ is an integral over the entire path space. By integrating out the states sequentially ($x_0, x_1, \dots$), a telescoping cancellation occurs. The integral over $x_{k-1}$ involves the term $\int f_k(x_{k-1}) T_k(x_k | x_{k-1}) \, dx_{k-1}$. Due to the $\pi_k$-invariance of $T_k$, this integral simplifies to $f_k(x_k)$, which then cancels with the denominator of the next weight term in the product. This recursive cancellation continues until only $\frac{1}{Z_0} \int f_K(x_{K-1}) dx_{K-1} = Z_K/Z_0$ remains.

Crucially, this proof of unbiasedness does not depend on how many steps of the MCMC kernel $T_k$ are run, nor on how well it mixes. Even a single application of an invariant kernel is sufficient for the expectation to be correct [@problem_id:3288132] [@problem_id:3288122]. Poor mixing will dramatically increase the variance of the estimator, but it does not introduce bias.

From a more abstract perspective, AIS can be viewed as a special case of Sequential Monte Carlo (SMC) without a resampling step, using a specific choice of backward kernels [@problem_id:3288042]. This connection provides a deeper theoretical grounding and relates AIS to the broader family of [particle filtering](@entry_id:140084) methods.

### Practical Implementation and Performance Diagnostics

While theoretically sound, the practical success of AIS hinges on careful implementation and monitoring. Two key challenges are numerical stability and [weight degeneracy](@entry_id:756689).

#### Numerical Stability and Log-Domain Computation

The AIS weight is a product of many terms. If the incremental ratios are consistently small, this product can quickly [underflow](@entry_id:635171) to zero in [finite-precision arithmetic](@entry_id:637673). For example, in standard double-precision [floating-point arithmetic](@entry_id:146236), any value smaller than roughly $10^{-324}$ becomes exactly zero. If the cumulative log-weight $\sum_k \log r_k$ drops below approximately $-744$, the resulting weight will underflow [@problem_id:3288076].

To avoid this, all computations should be performed in the log domain. Instead of multiplying ratios $r_k$, one accumulates the sum of log-ratios, $\ell_k = \log r_k$:
$$
S_K = \sum_{k=1}^K \ell_k
$$
This sum is far less susceptible to [underflow](@entry_id:635171) or overflow. After running $N$ independent AIS simulations to obtain $N$ log-weights $\{S_K^{(i)}\}_{i=1}^N$, we need to compute the [sample mean](@entry_id:169249) of the original weights, $\widehat{R} = \frac{1}{N} \sum_{i=1}^N \exp(S_K^{(i)})$. A naive computation of this sum can still suffer from numerical issues if the $S_K^{(i)}$ values are very large or small. The standard and stable solution is the **log-sum-exp** trick:
$$
\log \widehat{R} = a + \log\left( \frac{1}{N} \sum_{i=1}^N \exp(S_K^{(i)} - a) \right)
$$
where $a = \max_i S_K^{(i)}$. This transformation ensures that the arguments of the [exponential function](@entry_id:161417) are less than or equal to zero, preventing overflow and reducing the chance of underflow, thereby yielding a stable estimate of the mean [@problem_id:3288076]. It is critical to note that one must compute the [arithmetic mean](@entry_id:165355) of the weights, not the geometric mean. Using $\exp(\frac{1}{N} \sum S_K^{(i)})$ would estimate the geometric mean, which is a biased and inconsistent estimator for $Z_T/Z_0$.

#### Weight Degeneracy and Effective Sample Size

The primary diagnostic for the quality of an AIS run is the variability of the weights obtained from multiple independent simulations. As in basic [importance sampling](@entry_id:145704), if a few weights are much larger than the rest, the estimate is unreliable. This is [weight degeneracy](@entry_id:756689). To quantify this, we use the **Effective Sample Size (ESS)** [@problem_id:3288041]. Given $N$ weights $\{w_i\}_{i=1}^N$, the ESS is defined as:

$$
\mathrm{ESS} = \frac{\left(\sum_{i=1}^N w_i\right)^2}{\sum_{i=1}^N w_i^2}
$$

This quantity can be interpreted as the number of "effective" particles that contribute to the estimate. The ESS is bounded by $1 \le \mathrm{ESS} \le N$.
-   $\mathrm{ESS} = N$ occurs only if all weights are identical ($w_1 = w_2 = \dots = w_N$), representing a perfect, zero-variance scenario.
-   $\mathrm{ESS} \approx 1$ occurs if one weight is vastly larger than all others, representing extreme degeneracy.

The ESS can be expressed in terms of the squared [coefficient of variation](@entry_id:272423) ($\mathrm{CV}^2$) of the weights as $\mathrm{ESS} = N/(1 + \mathrm{CV}^2)$, explicitly showing that higher weight variability leads to a lower ESS. In practice, a low ESS (e.g., $\mathrm{ESS} \ll N$) is a red flag indicating that the variance of the AIS estimator is high and the estimate is likely poor. This often motivates practitioners to refine the annealing schedule or improve the MCMC kernels.

### Challenges and Advanced Strategies

The performance of AIS depends critically on the interplay between the [annealing](@entry_id:159359) schedule and the efficiency of the MCMC transition kernels. This is particularly evident when dealing with complex, multimodal distributions.

#### Comparison with Thermodynamic Integration

Another classic method for estimating log-normalizing constants is **Thermodynamic Integration (TI)**. TI uses the [thermodynamic identity](@entry_id:142524):
$$
\log\left(\frac{Z_T}{Z_0}\right) = \int_0^T \mathbb{E}_{\pi_\beta}\left[ \frac{\partial}{\partial\beta} \log f_\beta(X) \right] \,d\beta
$$
TI estimates this integral by using numerical quadrature (e.g., the [trapezoidal rule](@entry_id:145375)) over a grid of $\beta$ values, where each required expectation is estimated via a separate, long MCMC run.

AIS and TI present a fundamental trade-off in bias and variance [@problem_id:3288028].
-   **Bias**: The AIS estimator for $Z_T/Z_0$ is unbiased. However, the estimator for the logarithm, $\log(\frac{1}{N}\sum w_i)$, is negatively biased due to Jensen's inequality. This bias decreases as $1/N$. The TI estimator is biased due to the deterministic error of numerical quadrature.
-   **Variance**: The variance of the AIS estimator accumulates multiplicatively and can be very high if the annealing schedule is too coarse. The variance of the TI estimator accumulates additively from the independent MCMC runs at each temperature.

In "smooth" problems where the integrand of the TI formula is a well-behaved function of $\beta$, TI can be very effective, as its quadrature bias can be made small with a reasonable number of grid points. In contrast, if an AIS schedule is not chosen carefully, its variance can be large. However, if the [annealing](@entry_id:159359) schedule for AIS can be designed such that the "distance" (e.g., KL divergence) between successive distributions is kept small, the variance of the AIS weights can be well-controlled. In such regimes, AIS can be highly competitive, as its own bias can be reduced simply by increasing the number of independent runs, $N$ [@problem_id:3288028].

#### The Challenge of Multimodality

A significant challenge for AIS arises when the [target distribution](@entry_id:634522) is multimodal. For example, consider [annealing](@entry_id:159359) from a single Gaussian to a well-separated two-component Gaussian mixture. As the inverse temperature $\beta$ increases, the intermediate distribution $f_\beta$ can undergo a phase transition, changing from unimodal to bimodal [@problem_id:3288122].

When this happens, standard local-move MCMC kernels (like random-walk Metropolis) become ineffective. Once a particle enters one mode, the probability of proposing a move that jumps to the other mode becomes vanishingly small. The MCMC chain becomes "trapped". This poor mixing has severe consequences for AIS: an individual AIS path will typically explore only one of the target's modes. This path is not representative of the full distribution, leading to extremely high variance in the final [importance weights](@entry_id:182719). Different runs get trapped in different modes, yielding wildly different weights and a highly unstable final estimate [@problem_id:3288122].

To combat this, two primary strategies are employed:
1.  **Adaptive Annealing Schedules**: Since the change from unimodal to bimodal happens in a specific region of $\beta$, the [annealing](@entry_id:159359) schedule should be made much denser in that region. This makes the steps smaller precisely where the landscape is changing most dramatically, helping to control the variance of the incremental weights [@problem_id:3288122].
2.  **Advanced MCMC Kernels**: To overcome mode-trapping, more sophisticated, non-local MCMC kernels can be used for the transitions $T_k$. One such technique is using **tempered transitions**. At a given temperature $\beta_k$, this involves running an auxiliary MCMC chain on a ladder of even higher temperatures (lower $\beta$'s), where energy barriers are lower and mode-jumping is easier. A proposed move from this auxiliary chain is then accepted or rejected for the main chain via a Metropolis-Hastings step that preserves the $\pi_{\beta_k}$ distribution. By embedding such powerful kernels within the AIS framework, one can improve mixing and drastically reduce variance without introducing any bias [@problem_id:3288122].

In summary, Annealed Importance Sampling is a fundamentally unbiased and broadly applicable method for estimating ratios of normalizing constants. Its practical success requires a careful understanding of its numerical properties, the use of diagnostics like ESS, and the intelligent design of annealing schedules and transition kernels to match the complexity of the problem at hand.