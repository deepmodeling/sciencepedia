## Introduction
In the field of inverse problems, successfully reconstructing a signal or image from incomplete and noisy data hinges on the use of effective [prior information](@entry_id:753750). While traditional priors excel at modeling smooth phenomena, they often fail when the underlying truth contains sharp edges, localized events, or other sparse features, leading to oversmoothed and inaccurate results. This introduces a critical knowledge gap: how can we regularize [ill-posed problems](@entry_id:182873) in a way that respects and preserves these essential non-smooth characteristics?

This article introduces Besov space priors as a powerful solution to this challenge. By moving beyond classical smoothness assumptions, these priors provide a sophisticated mathematical framework for promoting sparsity in a transformed domain, typically using wavelets. This approach allows for the [robust recovery](@entry_id:754396) of complex structures that are ubiquitous in science and engineering. Across three chapters, this article will guide you from fundamental theory to practical application.

The first chapter, **Principles and Mechanisms**, will lay the groundwork by defining Besov spaces, explaining their characterization through [wavelet coefficients](@entry_id:756640), and detailing the precise mechanism by which they enforce sparsity. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how these principles are applied to solve real-world problems like edge-preserving [image reconstruction](@entry_id:166790) and four-dimensional [data assimilation](@entry_id:153547), highlighting connections to various scientific disciplines. Finally, the third chapter, **Hands-On Practices**, will provide a series of guided exercises to solidify your understanding and build practical skills in implementing and analyzing Besov-based models.

## Principles and Mechanisms

In the context of [inverse problems](@entry_id:143129), [prior information](@entry_id:753750) is essential for regularizing [ill-posed problems](@entry_id:182873) and guiding the solution towards a physically plausible or desirable state. When dealing with signals or images that are known to possess sharp edges, localized features, or other non-uniform characteristics, traditional smoothness priors, such as those based on Sobolev spaces, can be overly restrictive, tending to blur or oversmooth these important details. Besov space priors have emerged as a powerful alternative, providing a flexible framework for promoting **sparsity** in a transformed domain—typically a [wavelet basis](@entry_id:265197)—which corresponds to preserving sharp features in the original signal. This chapter elucidates the fundamental principles and mechanisms underlying Besov space priors, from their mathematical definition to their practical implementation and theoretical justification.

### Defining Smoothness and Sparsity: From Sobolev to Besov Spaces

The concept of smoothness is mathematically formalized through function spaces. A common choice is the **Sobolev space** $W^{s,p}$, which contains functions whose derivatives up to a certain order $s$ are integrable in the $L^p$ sense. While effective for modeling globally [smooth functions](@entry_id:138942), Sobolev spaces are less adept at representing functions with spatially varying smoothness.

**Besov spaces**, denoted $B_{p,q}^s$, offer a finer and more flexible characterization of [function smoothness](@entry_id:144288). One way to define these spaces is through the behavior of finite differences. For a function $f$ defined on a domain such as the $d$-dimensional torus $\mathbb{T}^d$, we can define its $r$-th order [modulus of smoothness](@entry_id:752104) in $L^p$ as:
$$
\omega_{r}(f,t)_{p} = \sup_{|h|\le t} \left\| \sum_{k=0}^{r} (-1)^{r-k} \binom{r}{k} f(\cdot + k h) \right\|_{L^{p}(\mathbb{T}^{d})}, \quad t > 0
$$
This quantity measures the average variation of the function at a scale $t$. A function is considered smooth if this variation decays quickly as $t \to 0$. The Besov space norm formalizes this by integrating these scale-dependent variations. Specifically, for a smoothness index $s > 0$, we choose an integer $r > s$, and the Besov (quasi-)norm $\|f\|_{B_{p,q}^s(\mathbb{T}^d)}$ is equivalent to:
$$
\| f \|_{L^{p}(\mathbb{T}^{d})} + \left( \int_{0}^{1} \big( t^{-s} \omega_{r}(f,t)_{p} \big)^{q} \frac{dt}{t} \right)^{1/q}
$$
(with the integral replaced by a supremum if $q=\infty$). The parameters $s$, $p$, and $q$ each play a distinct role :
- The **smoothness index** $s$ governs the overall differentiability of the function, controlling the rate of decay of the [modulus of smoothness](@entry_id:752104).
- The **integrability index** $p$ is a spatial parameter, measuring how variations are aggregated within a given scale $t$. Smaller values of $p$ (e.g., $p=1$) are more sensitive to localized, sparse variations, while larger values (e.g., $p=2$) measure average-case, or energy-based, smoothness.
- The **summability index** $q$ aggregates contributions across different scales. A smaller $q$ value encourages the function's "roughness" to be concentrated in a few scales, promoting a form of *across-scale sparsity*.

The key innovation of Besov spaces over Sobolev spaces lies in the [decoupling](@entry_id:160890) of spatial ($p$) and across-scale ($q$) aggregation. For non-integer $s$ and $1  p  \infty$, the Sobolev space is a special case: $W^{s,p} = B_{p,p}^s$. By allowing $q \neq p$, Besov spaces provide a richer class of models. In particular, choosing $p$ and $q$ to be small (typically $p, q \le 1$) is the primary mechanism for inducing sparsity.

### Wavelet Characterization and Probabilistic Construction

While the modulus-of-smoothness definition is theoretically insightful, the most practical and widely used definition of Besov spaces comes from their characterization using **[wavelet](@entry_id:204342) bases**. An orthonormal [wavelet basis](@entry_id:265197) $\{\psi_{j,k}\}$ decomposes a function $f$ into components localized in both scale (indexed by $j$) and space (indexed by $k$). The Besov norm can then be shown to be equivalent to a sequence-space norm on the [wavelet coefficients](@entry_id:756640) $\theta_{j,k} = \langle f, \psi_{j,k} \rangle$.

For a function $f$ with [wavelet coefficients](@entry_id:756640) $\theta_{j,k}$, its Besov norm $\|f\|_{B^s_{p,q}}$ is equivalent to a weighted combination of these coefficients. For an $L^2$-normalized [wavelet basis](@entry_id:265197), this equivalence takes the form:
$$
\|f\|_{B_{p,q}^s} \asymp \left( \sum_{j=j_0}^{\infty} \left( 2^{j\left(s + \frac{d}{2} - \frac{d}{p}\right)} \left( \sum_{k} |\theta_{j,k}|^p \right)^{1/p} \right)^q \right)^{1/q}
$$
Here, the term $\left(\sum_k |\theta_{j,k}|^p\right)^{1/p}$ is the $\ell_p$ norm of the coefficients within the scale $j$, corresponding to the role of the index $p$. The outer summation, an $\ell_q$ norm across scales $j$, corresponds to the index $q$. The weight factor $2^{j(s + d/2 - d/p)}$ precisely calibrates the contribution of each scale according to the desired smoothness $s$. The exponent reflects the intrinsic scaling properties of Besov functions; under a dilation $f_\lambda(x) = f(\lambda x)$, the Besov norm scales principally as $\lambda^{s - d/p}$ .

This [wavelet](@entry_id:204342) characterization provides a direct pathway to constructing a **Besov space prior** in a Bayesian setting. We can define a prior distribution directly on the [wavelet coefficients](@entry_id:756640). A common construction is to model the coefficients as [independent random variables](@entry_id:273896) whose distributions are chosen to match the Besov norm structure . For instance, a prior corresponding to the space $B^s_{p,p}$ can be constructed by assigning each coefficient $\theta_{j,k}$ a probability density proportional to $\exp(-c_j |\theta_{j,k}|^p)$, where the scale-dependent weights $c_j$ are derived from the [wavelet](@entry_id:204342) characterization.

A powerful and general method is to define the [wavelet coefficients](@entry_id:756640) $\theta_{j,k}$ via a scaling of [i.i.d. random variables](@entry_id:263216) $\xi_{j,k}$:
$$
\theta_{j,k} = \lambda_j \xi_{j,k}
$$
where the base variables $\xi_{j,k}$ are drawn from a fixed density, e.g., $\rho_p(x) \propto \exp(-|x|^p)$, and the [scale factors](@entry_id:266678) $\lambda_j$ encode the Besov smoothness:
$$
\lambda_j = \tau 2^{-j\left(s + d\left(\frac{1}{2} - \frac{1}{p}\right)\right)}
$$
The joint prior density for a finite set of coefficients up to level $J$, denoted $\boldsymbol{\theta}^{(J)}$, is then the product of the individual densities due to independence. A [change of variables](@entry_id:141386) from $\xi_{j,k}$ to $\theta_{j,k}$ reveals the structure:
$$
p_J(\boldsymbol{\theta}^{(J)}) = \prod_{j=0}^{J} \prod_{k \in \mathcal{K}_j} \frac{1}{\lambda_j} \rho_p\left(\frac{\theta_{j,k}}{\lambda_j}\right) \propto \exp\left( -\sum_{j=0}^{J} \sum_{k \in \mathcal{K}_j} \left|\frac{\theta_{j,k}}{\lambda_j}\right|^p \right)
$$
This construction provides a concrete, computationally tractable [prior distribution](@entry_id:141376) that formally places high probability on functions belonging to a specific Besov space.

### The Mechanism of Sparsity Promotion

The central motivation for using Besov priors is their ability to promote sparsity. This property is most pronounced when the integrability index $p$ is small, particularly for $p=1$. To understand the mechanism, we can compare a Besov prior for $p=1$ (which induces a **Laplace distribution** on coefficients) with a prior for $p=2$ (which induces a **Gaussian distribution** and corresponds to a Sobolev-type space) .

Consider the prior density on a single coefficient $\theta$:
- **Gaussian Prior ($p=2$):** $p(\theta) \propto \exp(-\gamma \theta^2)$
- **Laplace Prior ($p=1$):** $p(\theta) \propto \exp(-\gamma |\theta|)$

The key differences are in the tail behavior and the shape at the origin.
1.  **Tail Behavior:** The Laplace distribution has **heavier tails** than the Gaussian distribution. This means that for large values of $|\theta|$, the Laplace density decays exponentially ($e^{-|\theta|}$), whereas the Gaussian density decays much faster ($e^{-\theta^2}$). Counter-intuitively, this means the Laplace prior penalizes large coefficients *less* severely than a Gaussian prior. This allows the model to retain large, significant coefficients, which often correspond to important features like edges in an image.
2.  **Behavior at Zero:** The Laplace density has a sharp **cusp** at $\theta=0$, while the Gaussian density is flat. This cusp indicates a much stronger [prior belief](@entry_id:264565) that coefficients are exactly, or very close to, zero.

This dual behavior—tolerance of large coefficients and a strong preference for zero—is the essence of a sparsity-promoting prior. The practical consequence of this becomes evident when we consider the **Maximum A Posteriori (MAP)** estimator. In a simple denoising problem where we observe $y = f + \eta$ with Gaussian noise $\eta$, the MAP estimate for the [wavelet coefficients](@entry_id:756640) of $f$ is found by minimizing:
$$
\hat{\boldsymbol{\theta}}_{\text{MAP}} = \arg \min_{\boldsymbol{\theta}} \left( \frac{1}{2\sigma^2} \sum_{j,k} (y_{j,k} - \theta_{j,k})^2 - \log p(\boldsymbol{\theta}) \right)
$$
where $y_{j,k}$ are the [wavelet coefficients](@entry_id:756640) of the noisy data $y$.
- With the **Gaussian prior**, $-\log p(\boldsymbol{\theta}) \propto \sum_{j,k} \gamma_j \theta_{j,k}^2$. The MAP estimator is a linear shrinkage rule: $\hat{\theta}_{j,k} = c \cdot y_{j,k}$ for some constant $c  1$. The estimate is never exactly zero unless the data is zero.
- With the **Laplace prior**, $-\log p(\boldsymbol{\theta}) \propto \sum_{j,k} \gamma_j |\theta_{j,k}|$. The non-differentiability of the absolute value at the origin leads to a non-linear **soft-thresholding** rule:
  $$
  \hat{\theta}_{j,k} = \text{sign}(y_{j,k}) \max(0, |y_{j,k}| - T_j)
  $$
  where $T_j$ is a threshold proportional to $\gamma_j$. This rule explicitly sets any coefficient whose corresponding data $|y_{j,k}|$ falls below the threshold to **exactly zero**. This is the mechanism by which the prior actively enforces a sparse solution.

### From Bayesian MAP to Variational Regularization

The connection between MAP estimation and regularization is a cornerstone of modern inverse problems. For a general linear inverse problem $y = A f + \eta$ with Gaussian noise, the MAP [objective function](@entry_id:267263) under a Besov prior on $f$ takes the form of a Tikhonov-style variational problem. If we represent $f$ by its [wavelet coefficients](@entry_id:756640) $\boldsymbol{\theta}$, the objective is to minimize:
$$
J(\boldsymbol{\theta}) = \frac{1}{2\sigma^2} \| A W^* \boldsymbol{\theta} - y \|_2^2 - \log p(\boldsymbol{\theta})
$$
where $W^*$ is the wavelet synthesis operator.

If we adopt a prior corresponding to the space $B_{1,1}^s$, the negative log-prior becomes a weighted $\ell_1$-norm of the coefficients . Specifically, for an $L^2$-normalized [wavelet basis](@entry_id:265197) in $d$ dimensions, the prior penalty term is proportional to the Besov [seminorm](@entry_id:264573):
$$
-\log p(\boldsymbol{\theta}) \propto \sum_{j,k} 2^{j(s - d/2)} |\theta_{j,k}|
$$
The MAP estimation problem is therefore equivalent to solving the following optimization problem, widely known as the **Lasso** (Least Absolute Shrinkage and Selection Operator) in the wavelet domain:
$$
\hat{\boldsymbol{\theta}} = \arg \min_{\boldsymbol{\theta}} \left( \frac{1}{2} \| A W^* \boldsymbol{\theta} - y \|_2^2 + \lambda \sum_{j,k} w_j |\theta_{j,k}| \right)
$$
where the regularization parameters $w_j = 2^{j(s - d/2)}$ are determined by the smoothness $s$, dimension $d$, and scale $j$. This formulation bridges the probabilistic Bayesian perspective with the deterministic optimization framework of [variational regularization](@entry_id:756446).

### Advanced Priors: Scale-Mixture Models

While Laplace priors are effective, they are part of a broader class of heavy-tailed, sparsity-inducing distributions. A flexible and computationally convenient way to generate such priors is through **Gaussian scale-mixtures**. In this hierarchical approach, each [wavelet](@entry_id:204342) coefficient $\theta_{j,k}$ is modeled as a draw from a Gaussian distribution, but with its own unique, random variance $\tau_{j,k}$:
$$
\theta_{j,k} \mid \tau_{j,k} \sim \mathcal{N}(0, \tau_{j,k})
$$
Sparsity is induced by placing a hyperprior on the variances $\tau_{j,k}$ that favors small values but allows for occasional large ones.

A standard choice is the **Inverse-Gamma distribution** for the variances: $\tau_{j,k} \sim \text{Inverse-Gamma}(a_j, b_j)$. Integrating out the random variance $\tau_{j,k}$ yields the marginal prior for $\theta_{j,k}$, which can be shown to be a **Student-t distribution** with $\nu_j = 2a_j$ degrees of freedom .
$$
p(\theta_{j,k}) \propto \left(1 + \frac{\theta_{j,k}^2}{\nu_j s_j^2}\right)^{-\frac{\nu_j+1}{2}}, \quad \text{where } s_j^2=b_j/a_j
$$
The tails of this distribution decay polynomially ($\propto |\theta_{j,k}|^{-(\nu_j+1)}$), which is heavier than the [exponential decay](@entry_id:136762) of the Laplace distribution. This provides an even weaker penalty for large coefficients. The degrees of freedom $\nu_j=2a_j$ control the heaviness of the tails; as $a_j \to \infty$, the Student-t distribution approaches a Gaussian, and as $a_j \to 0$, the tails become extremely heavy.

Other [hyperpriors](@entry_id:750480) on the local scale lead to different sparsity-promoting distributions. A prominent example is the **[horseshoe prior](@entry_id:750379)**, which results from placing a half-Cauchy hyperprior on the standard deviations $\sqrt{\tau_{j,k}}$. Compared to the Student-t prior, the [horseshoe prior](@entry_id:750379) exhibits even stronger sparsity promotion, featuring both extremely heavy tails and an unbounded spike in its density at the origin. This allows it to shrink small, noisy coefficients more aggressively towards zero while applying even less shrinkage to large, true signals .

### Theoretical Guarantees: Optimal Contraction Rates

The practical success of sparsity-promoting Besov priors is underpinned by strong theoretical results. In the framework of Bayesian nonparametrics, a key measure of performance is the **posterior contraction rate**. This rate, $r_n$, describes how quickly the [posterior distribution](@entry_id:145605) concentrates around the true underlying function $f^\dagger$ as the amount of data (or [signal-to-noise ratio](@entry_id:271196), indexed by $n$) increases. A faster rate (smaller $r_n$) means a more accurate and efficient statistical procedure.

Consider a denoising problem where we observe $N_n$ [wavelet coefficients](@entry_id:756640) contaminated by Gaussian noise with variance $\delta_n^2$. Suppose the true signal $f^\dagger$ is **sparse**, meaning only $m_n \ll N_n$ of its [wavelet coefficients](@entry_id:756640) are non-zero. We can compare the performance of a non-adaptive Gaussian prior with an adaptive Laplace-type Besov prior .

1.  **Gaussian Prior ($B^s_{2,2}$):** Because the Gaussian prior is non-adaptive and applies shrinkage to all coefficients, it cannot distinguish signal from noise based on sparsity. The uncertainty from all $N_n$ noisy dimensions accumulates. The resulting posterior contraction rate for the squared $\ell^2$ error is suboptimal:
    $$
    r_n^{(G)} \asymp \delta_n \sqrt{N_n}
    $$

2.  **Laplace-Besov Prior ($B^s_{1,1}$):** The Laplace prior, through the thresholding mechanism, effectively "discovers" the sparse structure. It aggressively shrinks the $N_n - m_n$ noise-only coefficients to zero, focusing the model's capacity on estimating the $m_n$ significant coefficients. This adaptation to sparsity results in a much faster, near-optimal contraction rate:
    $$
    r_n^{(L)} \asymp \delta_n \sqrt{m_n \log N_n}
    $$
    The term $\log N_n$ is the statistical "price" for not knowing the locations of the non-zero coefficients in advance.

The Laplace-Besov prior provides a strict improvement whenever $m_n \log N_n = o(N_n)$, a condition that holds for any truly sparse signal. This result provides a profound theoretical justification for using Besov space priors: they automatically adapt to the unknown sparsity of the ground truth, leading to statistically optimal rates of recovery in settings where classical smoothness priors fail.