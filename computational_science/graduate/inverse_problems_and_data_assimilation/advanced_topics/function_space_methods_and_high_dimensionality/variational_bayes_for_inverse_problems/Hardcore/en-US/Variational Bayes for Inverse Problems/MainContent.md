## Introduction
In the realm of inverse problems, the Bayesian framework offers a complete and principled approach to inference, characterizing the solution as a posterior probability distribution. However, for many scientifically significant problems involving high dimensionality or nonlinearity, this posterior is computationally intractable, rendering exact inference impossible. This creates a critical knowledge gap: how can we harness the power of Bayesian reasoning when direct computation is off the table? This article introduces **Variational Bayes (VB)**, a powerful class of methods that bridges this gap by transforming the intractable inference problem into a tractable optimization problem.

Over the next three chapters, you will gain a deep understanding of the variational framework. We will begin in **Principles and Mechanisms** by deriving the core theory, from the Kullback-Leibler divergence to the pivotal Evidence Lower Bound (ELBO), and exploring the crucial design choices that govern the approximation's behavior. Next, in **Applications and Interdisciplinary Connections**, we will showcase the remarkable versatility of VB, demonstrating how it is adapted to solve complex problems in fields ranging from [medical imaging](@entry_id:269649) to control theory. Finally, in **Hands-On Practices**, you will have the opportunity to implement these concepts, solidifying your theoretical knowledge through practical application. We begin by laying the groundwork for this powerful methodology.

## Principles and Mechanisms

In the preceding chapter, we introduced the Bayesian formulation of [inverse problems](@entry_id:143129), culminating in the posterior probability distribution $p(x \mid y)$. This distribution represents the complete solution to the inverse problem, encoding all that is known about the parameters $x$ after observing the data $y$. However, for a majority of scientifically relevant problems—particularly those involving high-dimensional parameter spaces or nonlinear forward operators—the [posterior distribution](@entry_id:145605) is computationally intractable. We can neither evaluate its [normalization constant](@entry_id:190182) nor draw [independent samples](@entry_id:177139) from it efficiently. This chapter delves into a powerful framework for overcoming this challenge: **Variational Bayes (VB)**, also known as Variational Inference (VI). VB reframes the problem of inference as a problem of optimization, seeking a tractable approximation to the true, intractable posterior.

### The Variational Principle: Approximating Posteriors through Optimization

The central tenet of variational Bayes is to posit a family of tractable probability distributions, denoted $\mathcal{Q}$, and then to find the member of this family, $q(x) \in \mathcal{Q}$, that is "closest" to the true posterior $p(x \mid y)$. The "closeness" between two distributions is measured using a divergence, most commonly the **Kullback-Leibler (KL) divergence**. The KL divergence from an approximating distribution $q(x)$ to a true distribution $p(x \mid y)$ is defined as:

$$
\mathrm{KL}(q \,\|\, p(\cdot \mid y)) = \int q(x) \log \frac{q(x)}{p(x \mid y)} dx = \mathbb{E}_{x \sim q(x)} \left[ \log q(x) - \log p(x \mid y) \right]
$$

The KL divergence is always non-negative, $\mathrm{KL}(q \,\|\, p) \ge 0$, and equals zero if and only if $q(x) = p(x \mid y)$ [almost everywhere](@entry_id:146631). The goal of [variational inference](@entry_id:634275) is therefore to solve the following optimization problem:

$$
q^*(x) = \arg\min_{q \in \mathcal{Q}} \mathrm{KL}(q \,\|\, p(\cdot \mid y))
$$

While this objective seems straightforward, it directly involves the intractable posterior $p(x \mid y)$. A crucial insight of VB is that this minimization can be made equivalent to the maximization of a more convenient objective function.

### The Evidence Lower Bound (ELBO)

Let us expand the definition of the KL divergence using Bayes' rule, $p(x \mid y) = p(x, y) / p(y)$, where $p(x, y) = p(y \mid x)p(x)$ is the joint distribution and $p(y)$ is the [marginal likelihood](@entry_id:191889), or **evidence**.

$$
\begin{align}
\mathrm{KL}(q \,\|\, p(\cdot \mid y))  = \mathbb{E}_{q} \left[ \log q(x) - \log p(x, y) + \log p(y) \right] \\
 = \mathbb{E}_{q} [\log q(x) - \log p(x, y)] + \mathbb{E}_{q} [\log p(y)] \\
 = \mathbb{E}_{q} [\log q(x) - \log p(x, y)] + \log p(y)
\end{align}
$$

Rearranging this equation yields a fundamental identity in [variational inference](@entry_id:634275)  :

$$
\log p(y) = \mathbb{E}_{q} [\log p(x, y) - \log q(x)] + \mathrm{KL}(q \,\|\, p(\cdot \mid y))
$$

The first term on the right-hand side is known as the **Evidence Lower Bound (ELBO)**, denoted $\mathcal{L}(q)$:

$$
\mathcal{L}(q) = \mathbb{E}_{q} [\log p(x, y) - \log q(x)]
$$

The identity can thus be written as $\log p(y) = \mathcal{L}(q) + \mathrm{KL}(q \,\|\, p(\cdot \mid y))$. Since the KL divergence term is always non-negative, it immediately follows that $\mathcal{L}(q) \leq \log p(y)$. As its name suggests, the ELBO is a lower bound on the log [marginal likelihood](@entry_id:191889) of the data.

Crucially, because $\log p(y)$ is a constant with respect to $q(x)$, maximizing the ELBO is mathematically equivalent to minimizing the KL divergence to the posterior. Unlike the KL divergence, the ELBO is often computable without knowledge of the posterior's normalization constant $p(y)$. It depends only on the [joint distribution](@entry_id:204390) $p(x, y)$ and the variational approximation $q(x)$, both of which are typically available in analytic form or can be sampled from.

#### Interpretations of the ELBO

The ELBO can be rearranged into several forms, each providing a different intuition.

1.  **Data Fit vs. Prior Regularization:** By expanding the joint probability $p(x,y) = p(y|x)p(x)$, the ELBO can be written as :
    $$
    \mathcal{L}(q) = \mathbb{E}_{q}[\log p(y \mid x)] - \mathbb{E}_{q}[\log q(x) - \log p(x)] = \mathbb{E}_{q}[\log p(y \mid x)] - \mathrm{KL}(q \,\|\, p(x))
    $$
    In this form, maximizing the ELBO is a trade-off. The first term, the **expected [log-likelihood](@entry_id:273783)**, encourages the approximation $q(x)$ to place its mass on parameter values $x$ that are effective at explaining the observed data $y$. The second term, the negative KL divergence from the approximation to the prior $p(x)$, acts as a regularizer, penalizing $q(x)$ for deviating too far from our prior beliefs.

2.  **The Free Energy Analogy:** An alternative decomposition provides a deep connection to [statistical physics](@entry_id:142945) . We can write:
    $$
    \mathcal{L}(q) = \mathbb{E}_{q}[\log p(x, y)] + \left( - \mathbb{E}_{q}[\log q(x)] \right)
    $$
    The second term, $-\mathbb{E}_{q}[\log q(x)]$, is the **Shannon entropy** of the distribution $q(x)$, denoted $H(q)$. If we define an "energy" function $E(x,y) = -\log p(x,y)$, the ELBO becomes:
    $$
    \mathcal{L}(q) = -\mathbb{E}_{q}[E(x,y)] + H(q)
    $$
    This is analogous to the negative Helmholtz free energy, $F = U - TS$, at unit temperature ($T=1$), where $\mathbb{E}_{q}[E(x,y)]$ is the expected internal energy and $H(q)$ is the entropy. Maximizing the ELBO corresponds to finding a distribution $q(x)$ that minimizes the free energy. This involves a balance: finding low-energy states (regions of high [joint probability](@entry_id:266356)) while also maximizing the entropy, which favors distributions that are broad and represent higher **[epistemic uncertainty](@entry_id:149866)**. The entropy term prevents the approximation from collapsing to a single point estimate, ensuring that VB provides a measure of posterior uncertainty.

### The Choice of Divergence and its Consequences

The use of the "reverse" KL divergence, $\mathrm{KL}(q \,\|\, p)$, as opposed to the "forward" KL divergence, $\mathrm{KL}(p \,\|\, q)$, is a deliberate and consequential choice. While the forward KL also measures the dissimilarity between distributions, its optimization leads to vastly different behavior and computational challenges.

The reverse KL, $\mathrm{KL}(q \,\|\, p) = \int q(x) \log \frac{q(x)}{p(x)} dx$, includes the term $\log p(x)$. If the approximation $q(x)$ places significant probability mass in a region where the target $p(x)$ is near zero, the logarithm will be a large negative number, causing the KL divergence to become very large. To minimize this divergence, the approximation $q(x)$ is forced to be small wherever $p(x)$ is small. This is known as **zero-forcing** or **[mode-seeking](@entry_id:634010)** behavior.

Consider a nonlinear [inverse problem](@entry_id:634767) where the posterior is multimodal, possessing multiple, well-separated regions of high probability. A classic pedagogical example is a scalar problem with a quadratic forward map $f(\theta) = \theta^2$, an observation $y=9$, and low observation noise (e.g., $\sigma^2=0.04$). The likelihood function will have peaks at $\theta \approx 3$ and $\theta \approx -3$. If the prior is broad, the posterior $p(\theta \mid y)$ will be strongly bimodal . If we attempt to approximate this bimodal posterior with a unimodal Gaussian distribution $q(\theta)$, the [mode-seeking](@entry_id:634010) property of reverse-KL VB becomes apparent. A wide Gaussian $q(\theta)$ centered at zero would have to place significant mass in the "valley" between the two modes, where $p(\theta \mid y)$ is nearly zero, incurring a massive KL penalty. Consequently, the optimization will favor a solution where the unimodal $q(\theta)$ fits tightly around one of the posterior modes, completely ignoring the other .

This has profound consequences for [uncertainty quantification](@entry_id:138597). By selecting a single mode, VB can severely underestimate the true posterior uncertainty, providing a deceptively confident result that entirely misses other plausible solution branches.

In contrast, the forward KL, $\mathrm{KL}(p \,\|\, q) = \int p(x) \log \frac{p(x)}{q(x)} dx$, exhibits **mass-covering** behavior. It penalizes the approximation $q(x)$ for being small where the target $p(x)$ is large. Faced with a [multimodal posterior](@entry_id:752296), it would result in a single, wide approximation that attempts to cover all modes, often overestimating the variance.

The primary reason for the conventional use of the reverse KL, however, is computational. As shown previously, minimizing $\mathrm{KL}(q \,\|\, p)$ is equivalent to maximizing the ELBO, which only requires computing expectations with respect to the (by design, tractable) distribution $q(x)$. Minimizing the forward KL would require computing expectations with respect to the intractable posterior $p(x \mid y)$, defeating the purpose of [variational methods](@entry_id:163656) as an alternative to expensive sampling algorithms like MCMC .

### Variational Families: The Structure of the Approximation

The choice of the variational family $\mathcal{Q}$ is the most critical design decision in VB. It determines the trade-off between the flexibility of the approximation and the tractability of the optimization.

#### The Linear-Gaussian Model: An Exact Solution

As a foundational benchmark, consider an inverse problem with a linear forward operator $G(x) = Gx$ and both Gaussian prior $p(x) = \mathcal{N}(m_0, C_0)$ and Gaussian noise $\varepsilon \sim \mathcal{N}(0, \Gamma)$. In this conjugate setting, the [posterior distribution](@entry_id:145605) $p(x \mid y)$ is also Gaussian . If we choose our variational family $\mathcal{Q}$ to be the set of all possible Gaussian distributions, then the true posterior is a member of this family. Since the KL divergence is minimized at zero only when $q(x)=p(x \mid y)$, the VB optimization will recover the exact posterior mean and covariance. This demonstrates that when the variational family is sufficiently expressive to contain the true posterior, VB yields the exact solution.

#### Mean-Field Variational Bayes

For general, non-conjugate problems, the posterior is not in a simple [parametric form](@entry_id:176887). The most common and simplest variational family is the **mean-field** family, which assumes the posterior factorizes into independent blocks:

$$
q(x) = \prod_{j=1}^{n} q_j(x_j)
$$

This assumption posits that the components of the parameter vector $x$ are independent in the posterior. This drastically simplifies the optimization, but at the cost of introducing a strong [structural bias](@entry_id:634128). For a posterior that is in reality highly correlated, the mean-field approximation has two [main effects](@entry_id:169824) :
1.  **Zeroed Correlations:** By construction, the covariance matrix of the approximation $q(x)$ is diagonal, forcing all posterior correlations between the components $x_j$ to be zero.
2.  **Underestimated Variance:** The [mode-seeking](@entry_id:634010) nature of the KL divergence, combined with the inflexibility of the factorized form, forces the approximation to fit compactly within the true posterior. This results in a systematic underestimation of the marginal posterior variances. For a Gaussian posterior with [precision matrix](@entry_id:264481) $\Lambda$, the true marginal variance of component $x_j$ is $(\Lambda^{-1})_{jj}$, while the [mean-field approximation](@entry_id:144121) yields a variance of $(\Lambda_{jj})^{-1}$. It is a matrix identity that $(\Lambda^{-1})_{jj} \ge (\Lambda_{jj})^{-1}$, with equality holding if and only if the true posterior is already diagonal.

This underestimation of uncertainty is a hallmark of mean-field VB and a critical limitation to be aware of when interpreting its results. The approximation will be exact only in the trivial case where the true posterior already factorizes in the chosen basis .

#### Structured Variational Approximations

To mitigate the limitations of the mean-field assumption while retaining computational tractability, researchers have developed **structured variational families**. A powerful approach for [high-dimensional inverse problems](@entry_id:750278) is to use a full-covariance Gaussian approximation $q(x) = \mathcal{N}(\mu, \Sigma)$, but with a specific structure imposed on the covariance matrix $\Sigma$.

A common and effective choice is a **low-rank plus diagonal** structure :

$$
\Sigma = D + UU^{\top}
$$

Here, $D$ is a diagonal matrix, and $U$ is a tall, thin $n \times r$ matrix, with $r \ll n$. This [parameterization](@entry_id:265163) is motivated by the observation that in many high-dimensional problems, the data are only informative about a low-dimensional subspace of the [parameter space](@entry_id:178581). The low-rank term $UU^{\top}$ is designed to capture the strong correlations and variance changes within this data-informed subspace, while the diagonal term $D$ models the residual, largely uncorrelated variance in the complementary subspace. A principled choice for the columns of $U$ is to align them with the dominant directions of posterior update, which can be identified via an [eigendecomposition](@entry_id:181333) involving the prior covariance and the data Hessian .

This structured approach offers significant advantages. Statistically, it is far more expressive than the mean-field model and can capture the most important posterior dependencies. Computationally, it avoids the prohibitive $\mathcal{O}(n^2)$ storage and $\mathcal{O}(n^3)$ cost of [dense matrix](@entry_id:174457) operations. Key quantities like the inverse $\Sigma^{-1}$ and the determinant $\det(\Sigma)$, which are needed to evaluate the ELBO, can be computed efficiently in $\mathcal{O}(nr^2)$ or $\mathcal{O}(nr)$ time using the Sherman-Morrison-Woodbury formula and the [matrix determinant lemma](@entry_id:186722), respectively .

### Optimization and Practical Considerations

Once a variational family is chosen, the parameters of $q(x)$ are found by maximizing the ELBO. For the mean-field family, the standard algorithm is **Coordinate Ascent Variational Inference (CAVI)**. CAVI iteratively optimizes the ELBO with respect to each factor $q_j(x_j)$ while holding all other factors $\{q_k\}_{k \neq j}$ fixed. Each step is guaranteed to not decrease the ELBO, so the algorithm's objective value is monotonically non-decreasing .

Under standard regularity conditions, CAVI is guaranteed to converge to a [stationary point](@entry_id:164360) of the ELBO, which is a local maximum. However, the ELBO is generally a non-[concave function](@entry_id:144403) of the variational parameters, even for simple models like the linear-Gaussian case (unless the posterior is diagonal) . This non-[concavity](@entry_id:139843) means that multiple local optima can exist.

The existence of local optima is especially problematic when the true posterior is multimodal. As discussed, the [mean-field approximation](@entry_id:144121) will typically fit a single mode. The specific mode it converges to is determined by the **initialization** of the algorithm. Different starting points can lead CAVI into different basins of attraction, resulting in convergence to different local maxima of the ELBO, each corresponding to an approximation of a different [posterior mode](@entry_id:174279) . It is therefore standard practice to run the optimization from multiple random initializations and select the solution that yields the highest final ELBO.

### Applications in Inference and Model Selection

Variational Bayes provides not just an approximation to the posterior but also a principled framework for uncertainty quantification and [model evaluation](@entry_id:164873).

#### From Point Estimates to Full Distributions

Simple approaches to [inverse problems](@entry_id:143129) often yield only a point estimate, such as the **Maximum A Posteriori (MAP)** estimate. The MAP estimate corresponds to the mode of the posterior and is found by maximizing $p(x \mid y)$, which is equivalent to minimizing a regularized cost function . While useful, a point estimate provides no information about the uncertainty surrounding the solution. In contrast, the variational approximation $q(x)$ is a full probability distribution, providing not only a central estimate (its mean) but also a characterization of the uncertainty (its covariance). In the linear-Gaussian case, the MAP estimate coincides with the posterior mean, but using MAP alone discards the crucial covariance information that VB seeks to approximate . This uncertainty is essential for tasks like computing [credible intervals](@entry_id:176433) or propagating uncertainty to predictions of new data .

#### Assessing Approximation Quality

A key question is how good the variational approximation is. The fundamental identity $\log p(y) = \mathcal{L}(q) + \mathrm{KL}(q \,\|\, p(\cdot \mid y))$ tells us that the "gap" between the log evidence and the ELBO is precisely the KL divergence we sought to minimize. While this gap is not directly computable, it can be estimated. One common method uses **[importance sampling](@entry_id:145704)** with the variational distribution $q(x)$ as the proposal distribution to produce an unbiased estimate of the evidence $p(y)$. While taking the logarithm introduces bias, this and more advanced techniques like Annealed Importance Sampling (AIS) provide practical diagnostics for assessing the quality of the variational approximation .

#### Bayesian Model Comparison

Perhaps one of the most powerful applications of the ELBO is for **Bayesian [model comparison](@entry_id:266577)**. Suppose we have a set of competing models, such as different forward operators $\{G^{(1)}, G^{(2)}, \dots, G^{(K)}\}$, that could explain the data. The principled Bayesian approach is to compare them based on their marginal likelihood, or evidence, $p(y \mid G^{(m)})$. The evidence naturally penalizes overly complex models (a manifestation of Ockham's razor) and rewards models that provide a good fit to the data.

Since the evidence is intractable, we can use the optimized ELBO, $\mathcal{L}(q^*)$, as a proxy. For each model $G^{(m)}$, we run [variational inference](@entry_id:634275) to find the best approximation $q^{(m)}$ and its corresponding maximized ELBO value. We then select the model with the highest ELBO . The difference between the ELBOs of two models serves as an approximation to their log-Bayes factor, providing a quantitative basis for [model selection](@entry_id:155601).