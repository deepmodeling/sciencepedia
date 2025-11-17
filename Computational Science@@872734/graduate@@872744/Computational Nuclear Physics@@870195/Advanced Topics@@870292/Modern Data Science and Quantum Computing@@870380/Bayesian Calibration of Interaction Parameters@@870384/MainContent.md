## Introduction
The predictive power of modern [computational nuclear physics](@entry_id:747629) hinges on theoretical models of nuclear interactions and structure. These models, from fundamental Effective Field Theories (EFTs) to phenomenological Energy Density Functionals (EDFs), contain parameters that are not known from first principles and must be determined by confronting theory with experimental data. This process of [parameter estimation](@entry_id:139349), or calibration, is far from trivial; it demands a rigorous framework that can not only find the best-fit parameters but also coherently quantify all sources of uncertainty—from experimental noise to the inherent limitations of the theoretical models themselves. Bayesian inference provides this comprehensive and principled approach, transforming calibration from a simple curve-fitting exercise into a systematic method for [scientific reasoning](@entry_id:754574) under uncertainty.

This article provides a graduate-level guide to Bayesian calibration in nuclear physics. We begin in the **Principles and Mechanisms** chapter by laying out the mathematical and conceptual foundations of the Bayesian framework, from constructing likelihoods and priors to quantifying [model discrepancy](@entry_id:198101). Next, in **Applications and Interdisciplinary Connections**, we explore how these principles are applied to real-world problems, such as constraining nuclear forces, fusing data from multiple experiments, and even guiding future research. Finally, the **Hands-On Practices** section offers practical exercises to reinforce these concepts and build the skills necessary to apply Bayesian methods in your own work. By the end, you will have a thorough understanding of how to use Bayesian inference to convert data and physical principles into robust, quantitative knowledge about nuclear interactions.

## Principles and Mechanisms

The process of calibrating nuclear [interaction parameters](@entry_id:750714) is fundamentally a problem of [statistical inference](@entry_id:172747): using experimental data to constrain the unknown parameters of a theoretical model and to quantify the remaining uncertainty. Bayesian inference provides a comprehensive and principled framework for this task, allowing for the coherent integration of experimental measurements, theoretical constraints, and uncertainties arising from multiple sources. This chapter delineates the core principles and mechanisms of Bayesian calibration as applied to [computational nuclear physics](@entry_id:747629).

### The Bayesian Framework: Core Components

At the heart of Bayesian calibration lies Bayes' theorem, which describes how our state of knowledge about a set of parameters, $\boldsymbol{\theta}$, is updated in light of observed data, $\boldsymbol{d}$. The theorem provides a rule for constructing the **[posterior probability](@entry_id:153467) distribution** $p(\boldsymbol{\theta} | \boldsymbol{d})$, which represents our updated beliefs about the parameters after observing the data. It is expressed as:

$p(\boldsymbol{\theta} | \boldsymbol{d}) = \frac{p(\boldsymbol{d} | \boldsymbol{\theta}) p(\boldsymbol{\theta})}{p(\boldsymbol{d})}$

Each term in this equation has a distinct and crucial epistemic role [@problem_id:3544180]:

*   The **[prior probability](@entry_id:275634) distribution**, $p(\boldsymbol{\theta})$, encodes our knowledge or beliefs about the parameters *before* considering the experimental data being used for calibration. This is where we incorporate theoretical constraints, such as the "naturalness" of [low-energy constants](@entry_id:751501) (LECs) in an Effective Field Theory (EFT) or stability conditions in an Energy Density Functional (EDF).

*   The **likelihood function**, $p(\boldsymbol{d} | \boldsymbol{\theta})$, is the probability of observing the data $\boldsymbol{d}$ for a fixed set of parameter values $\boldsymbol{\theta}$. It is derived from the "[forward model](@entry_id:148443)"—the combination of the theoretical model predicting [observables](@entry_id:267133) and a statistical model of the discrepancies between prediction and observation. The likelihood function is the component that directly connects the data to the parameters.

*   The **[posterior probability](@entry_id:153467) distribution**, $p(\boldsymbol{\theta} | \boldsymbol{d})$, is the result of the inference. It represents our updated, post-data state of knowledge about $\boldsymbol{\theta}$, combining the information from the prior with that supplied by the data through the likelihood. The posterior is the primary object of interest, as it provides not only [point estimates](@entry_id:753543) for parameters (such as its mean or mode) but also a complete quantification of their uncertainties and correlations.

*   The **marginal likelihood** or **evidence**, $p(\boldsymbol{d})$, is the probability of the data integrated over all possible parameter values: $p(\boldsymbol{d}) = \int p(\boldsymbol{d} | \boldsymbol{\theta}) p(\boldsymbol{\theta}) \mathrm{d}\boldsymbol{\theta}$. While it serves as the normalization constant ensuring that the posterior integrates to one, it also plays a vital role in **Bayesian model selection**. By comparing the evidence for different models (e.g., competing nuclear interactions or different assumptions about error structures), one can quantify their relative plausibility given the data.

### Constructing the Likelihood: From Residuals to Probabilities

The [likelihood function](@entry_id:141927) quantifies the mismatch between model predictions and experimental data. Let the forward model, which maps a parameter vector $\boldsymbol{\theta}$ to a set of $n$ predicted [observables](@entry_id:267133), be denoted by $\boldsymbol{f}(\boldsymbol{\theta})$. The discrepancy between these predictions and the experimental data vector $\boldsymbol{d}$ is the residual vector $\boldsymbol{r} = \boldsymbol{d} - \boldsymbol{f}(\boldsymbol{\theta})$.

A ubiquitous and powerful assumption is that the total discrepancy, arising from all sources of error, can be modeled by a [multivariate normal distribution](@entry_id:267217) with a mean of zero and a total covariance matrix $\boldsymbol{C}$. The [likelihood function](@entry_id:141927) is then the probability density of this distribution evaluated at the observed residual:

$p(\boldsymbol{d} | \boldsymbol{\theta}) = \frac{1}{\sqrt{(2\pi)^n \det(\boldsymbol{C})}} \exp\left( -\frac{1}{2} (\boldsymbol{d} - \boldsymbol{f}(\boldsymbol{\theta}))^{\top} \boldsymbol{C}^{-1} (\boldsymbol{d} - \boldsymbol{f}(\boldsymbol{\theta})) \right)$

For computational purposes, particularly within sampling algorithms like Markov Chain Monte Carlo (MCMC), it is more convenient and numerically stable to work with the [log-likelihood](@entry_id:273783):

$\log p(\boldsymbol{d} | \boldsymbol{\theta}) = -\frac{1}{2} \left[ \boldsymbol{r}^{\top} \boldsymbol{C}^{-1} \boldsymbol{r} + \log|\boldsymbol{C}| + n\log(2\pi) \right]$

Evaluating this expression efficiently and stably is critical. If the covariance matrix $\boldsymbol{C}$ is dense, as is common when data points have [correlated errors](@entry_id:268558), explicitly calculating its inverse $\boldsymbol{C}^{-1}$ and determinant $|\boldsymbol{C}|$ is computationally expensive ($\mathcal{O}(n^3)$) and can be numerically unstable. A superior approach is to use the **Cholesky factorization** [@problem_id:3544114]. Since $\boldsymbol{C}$ is symmetric and positive-definite, it can be uniquely decomposed as $\boldsymbol{C} = \boldsymbol{L}\boldsymbol{L}^{\top}$, where $\boldsymbol{L}$ is a [lower-triangular matrix](@entry_id:634254). This factorization costs $\mathcal{O}(n^3)$ but needs to be performed only once if $\boldsymbol{C}$ is independent of $\boldsymbol{\theta}$. The terms in the log-likelihood can then be computed efficiently:
*   The [log-determinant](@entry_id:751430) is $\log|\boldsymbol{C}| = 2 \sum_{i=1}^{n} \log(L_{ii})$.
*   The quadratic form $\boldsymbol{r}^{\top} \boldsymbol{C}^{-1} \boldsymbol{r}$ is computed by first solving the triangular system $\boldsymbol{L}\boldsymbol{z} = \boldsymbol{r}$ for $\boldsymbol{z}$ ([forward substitution](@entry_id:139277), $\mathcal{O}(n^2)$), and then calculating the squared norm $\boldsymbol{z}^{\top}\boldsymbol{z}$. This avoids forming the inverse entirely.

#### Decomposing Uncertainty: Experimental Noise and Model Discrepancy

A principled construction of the likelihood requires a careful accounting of all sources of uncertainty that contribute to the total covariance $\boldsymbol{C}$. The residual is not simply [experimental error](@entry_id:143154). A more complete generative model for the observed data is [@problem_id:3544193]:

$\boldsymbol{d} = \boldsymbol{f}(\boldsymbol{\theta}) + \boldsymbol{\delta} + \boldsymbol{\epsilon}$

Here, the total error is additively decomposed into two physically distinct components:

1.  **Experimental Noise ($\boldsymbol{\epsilon}$):** This is **aleatoric** (statistical) uncertainty arising from the measurement process itself, such as detector resolution and counting statistics. It is typically modeled as a zero-mean random variable with a covariance matrix $\boldsymbol{\Sigma}_{\text{exp}}$ that is often diagonal or block-diagonal, reflecting known experimental conditions.

2.  **Model Discrepancy ($\boldsymbol{\delta}$):** This is **epistemic** (systematic) uncertainty arising from the known inadequacies of the theoretical model $\boldsymbol{f}(\boldsymbol{\theta})$. Even with the "true" parameters, the model is only an approximation of reality. Sources of discrepancy in nuclear physics include the truncation of the chiral Effective Field Theory (EFT) expansion, approximations in the many-body solver, and neglected physical effects. This discrepancy is not a property of the parameters but of the model's structure. It should be modeled as a random quantity to represent our uncertainty about its form and magnitude, often with a covariance matrix $\boldsymbol{\Sigma}_{\text{disc}}$.

Assuming these two sources of error are independent, a fundamental property of variances dictates that the total covariance matrix is the sum of the individual covariance matrices:

$\boldsymbol{C} = \boldsymbol{\Sigma}_{\text{exp}} + \boldsymbol{\Sigma}_{\text{disc}}$

This separation is crucial: conflating [model discrepancy](@entry_id:198101) with [experimental error](@entry_id:143154) or attempting to absorb it into the prior on $\boldsymbol{\theta}$ is an unprincipled approach that can lead to biased parameter estimates and overconfident (i.e., unreliable) uncertainty predictions.

#### Quantifying Model Discrepancy: EFT Truncation Error

In the context of chiral EFT, the concept of [model discrepancy](@entry_id:198101) can be made concrete. EFT provides a systematic expansion of nuclear [observables](@entry_id:267133) in powers of a small parameter $Q = p/\Lambda_b$, where $p$ is a typical momentum and $\Lambda_b$ is the "breakdown scale" of the theory. An observable $y$ is given by an infinite series:

$y = \sum_{k=0}^{\infty} c_k Q^k$

When we use a theoretical model truncated at a finite order $n$, our prediction is $y^{(n)} = \sum_{k=0}^{n} c_k Q^k$. The [model discrepancy](@entry_id:198101) is precisely the omitted tail of this series [@problem_id:3544164]:

$\delta_n = \sum_{k=n+1}^{\infty} c_k Q^k$

The coefficients $c_k$ for $k > n$ are unknown. We can represent our [epistemic uncertainty](@entry_id:149866) about them by modeling them as random variables. A standard assumption, motivated by naturalness, is that they are [independent and identically distributed](@entry_id:169067) draws from a zero-mean distribution, e.g., $c_k \sim \mathcal{N}(0, \bar{c}^2)$, where $\bar{c}$ is a scale factor of order unity.

Under this assumption, the variance of the truncation error, which defines the discrepancy variance $\sigma^2_{\text{disc}} \equiv \sigma^2_{\text{trunc}}$, can be derived from first principles [@problem_id:3544128]. Since the $c_k$ are independent and have [zero mean](@entry_id:271600), the variance of the sum is the sum of the variances:

$\sigma^2_{\text{trunc}} = \text{Var}(\delta_n) = \sum_{k=n+1}^{\infty} \text{Var}(c_k Q^k) = \sum_{k=n+1}^{\infty} Q^{2k} \text{Var}(c_k) = \bar{c}^2 \sum_{k=n+1}^{\infty} (Q^2)^k$

This is a geometric series, which sums to a [closed-form expression](@entry_id:267458) for $|Q| < 1$:

$\sigma^2_{\text{trunc}} = \bar{c}^2 \frac{Q^{2(n+1)}}{1 - Q^2}$

This formula provides a concrete, theory-driven prescription for estimating the [model discrepancy](@entry_id:198101) variance $\boldsymbol{\Sigma}_{\text{disc}}$ associated with EFT truncation. For example, in a calibration problem with $Q = 1/6$, truncation order $k=2$, [experimental error](@entry_id:143154) $\sigma_{\epsilon} = 0.05$, and $\bar{c}=1$, the truncation error variance would be $\sigma^2_{\text{trunc}} \approx 2.2 \times 10^{-5}$. While much smaller than the experimental variance $\sigma^2_{\epsilon} = 2.5 \times 10^{-3}$, it is a non-negligible, principled correction to the total likelihood variance, leading to a slightly larger and more honest posterior uncertainty in the calibrated parameters [@problem_id:3544164].

### Encoding Physical Knowledge in the Prior

The [prior distribution](@entry_id:141376), $p(\boldsymbol{\theta})$, is the mathematical tool for injecting existing theoretical knowledge into the inference, thereby regularizing the problem and ensuring that the results are physically sensible.

#### Priors from EFT Naturalness

In EFT, the principle of **naturalness** (or [power counting](@entry_id:158814)) posits that after non-dimensionalizing the theory using the appropriate physical scales (like the breakdown scale $\Lambda_b$), the resulting dimensionless [low-energy constants](@entry_id:751501) (LECs) should be of "order unity". Placing a prior directly on dimensionful parameters is ill-advised, as its physical meaning would change with arbitrary choices of units or scales. Instead, we encode naturalness by assigning priors to the dimensionless LECs, denoted $c_n$. A standard choice is a Gaussian prior centered at zero with a standard deviation of order one, e.g., $p(c_n) = \mathcal{N}(0, 1^2)$. This expresses the belief that very large coefficients are unlikely, without favoring a positive or negative sign [@problem_id:3544191].

This approach can be made more sophisticated using a **hierarchical prior**. Instead of fixing the variance, we can treat it as an unknown hyperparameter, $s^2$, and assign a prior to it (a hyperprior). For instance, we could model $p(c_n | s) = \mathcal{N}(0, s^2)$ and place a weakly informative prior on $s$ that favors values around one, such as a half-Cauchy distribution. This allows the data itself to inform the plausible range of the LECs, providing a data-driven check on the naturalness assumption [@problem_id:3544191].

#### Priors from Theoretical Constraints

Many physical theories impose hard constraints on parameters. For instance, the stability of nuclear matter requires certain combinations of couplings in an Energy Density Functional to be positive. Such constraints are implemented in a Bayesian framework by restricting the support of the prior distribution [@problem_id:3544144]. If an unconstrained baseline prior is $p_0(c)$, and theory requires $c \in \mathcal{D}$ (e.g., $c > 0$), the constrained prior becomes a truncated distribution:

$p(c) = \frac{p_0(c) \mathbb{I}\{c \in \mathcal{D}\}}{\int_{\mathcal{D}} p_0(c') \mathrm{d}c'}$

where $\mathbb{I}\{\cdot\}$ is the [indicator function](@entry_id:154167). This is equivalent to assigning zero prior probability to the forbidden region. Consequently, the posterior distribution will also have zero density outside $\mathcal{D}$. This hard truncation acts as an infinite penalty in the log-posterior, which can pose challenges for MCMC samplers, often requiring specialized proposal mechanisms to efficiently explore near the boundary.

This formalism also illuminates the behavior under **[model misspecification](@entry_id:170325)**. If the data strongly favor a parameter value $c^{\star}$ that is forbidden by the prior (i.e., $c^{\star} \notin \mathcal{D}$), the Bayesian framework provides a coherent response. The posterior will not concentrate at the true value $c^{\star}$ (it is "inconsistent"). Instead, as more data accumulate, the posterior will concentrate on the point within the allowed domain $\mathcal{D}$ that is "closest" to the forbidden truth—that is, the point in $\mathcal{D}$ that maximizes the [likelihood function](@entry_id:141927) [@problem_id:3544144]. For a positivity constraint $c>0$ and data favoring a negative $c^{\star}$, the posterior will pile up against the boundary at $c=0$.

### The Mechanics and Challenges of Inference

#### Sequential Updating

A powerful feature of Bayesian inference is its natural capacity for sequential learning. If we have two conditionally independent datasets, $D_1$ and $D_2$, we can update our knowledge in stages. First, we compute the posterior using the first dataset: $p(\boldsymbol{\theta} | D_1) \propto p(D_1 | \boldsymbol{\theta}) p(\boldsymbol{\theta})$. Then, we use this posterior as the prior for an update with the second dataset: $p(\boldsymbol{\theta} | D_1, D_2) \propto p(D_2 | \boldsymbol{\theta}) p(\boldsymbol{\theta} | D_1)$. A simple algebraic substitution reveals that this is equivalent to performing a single, combined update with the product of the likelihoods: $p(\boldsymbol{\theta} | D_1, D_2) \propto p(D_1 | \boldsymbol{\theta}) p(D_2 | \boldsymbol{\theta}) p(\boldsymbol{\theta})$. This equivalence is a direct consequence of the laws of probability and holds regardless of whether the priors are conjugate; it relies only on the [conditional independence](@entry_id:262650) of the data [@problem_id:3544155]. This allows complex calibration problems to be broken down, incorporating data from disparate experiments (e.g., scattering [cross-sections](@entry_id:168295) and nuclear binding energies) in a modular fashion.

#### Emulation for Expensive Models

In many areas of [nuclear theory](@entry_id:752748), the forward model $\boldsymbol{f}(\boldsymbol{\theta})$ is a complex simulation that is too computationally expensive to run thousands of times inside an MCMC loop. In such cases, a **surrogate model**, or **emulator**, can be built to approximate the true model output [@problem_id:3544201]. A Gaussian Process (GP) is a particularly powerful choice for an emulator. A GP is a statistical model that defines a prior distribution over functions. Building a GP emulator involves:
1.  Running the expensive [forward model](@entry_id:148443) at a limited number of training points in the [parameter space](@entry_id:178581).
2.  Fitting a GP to these training data. The choice of the GP's [covariance function](@entry_id:265031) (or "kernel") encodes prior beliefs about the smoothness and behavior of the true model function. For example, a stationary kernel assumes the function's characteristics (like variability and [correlation length](@entry_id:143364)) are the same everywhere, an assumption that is only justified if the underlying physics has no thresholds or sharp regime changes.
3.  Using the trained GP, which can be evaluated very quickly, in place of the expensive model inside the calibration workflow.

Critically, a GP provides not only a mean prediction but also a predictive variance that quantifies the emulator's own [epistemic uncertainty](@entry_id:149866). This emulator uncertainty is input-dependent—it is small near the training points and grows in unexplored regions. A complete Bayesian analysis must propagate this emulator uncertainty into the final posterior for $\boldsymbol{\theta}$. It is essential to distinguish this emulator uncertainty (the error in approximating the code) from the physical [model discrepancy](@entry_id:198101) (the error of the code in approximating reality). An emulator learns the model, flaws and all; it does not correct them [@problem_id:3544201].

#### Identifiability and Sloppiness in Many-Parameter Models

As nuclear models become more complex and involve tens of parameters, we face the challenge of **identifiability** [@problem_id:3544190].

*   **Structural Identifiability** is a property of the model itself. It asks: if we had perfect, noise-free data, could we uniquely determine the parameters? A lack of [structural identifiability](@entry_id:182904) means there are different parameter combinations that produce the exact same observable predictions.

*   **Practical Identifiability** is a property of the model-data combination. It asks: given our actual, finite, and noisy data, can we effectively constrain the parameters? A model may be structurally identifiable, but if the available data are not sensitive to a particular parameter or combination of parameters, it will be practically non-identifiable. The [posterior distribution](@entry_id:145605) for that parameter will be very broad, reflecting our lack of knowledge.

In many-parameter physics models, [practical non-identifiability](@entry_id:270178) often manifests as **sloppiness**. A sloppy model is characterized by a highly anisotropic [information geometry](@entry_id:141183): its predictions are extremely sensitive to a few "stiff" combinations of parameters but remarkably insensitive to many other "sloppy" combinations. This is revealed by the eigenvalues of the Fisher Information Matrix (FIM), which may span many orders of magnitude. The stiff directions (large FIM eigenvalues) correspond to well-constrained parameter combinations with small posterior variance. The sloppy directions (tiny FIM eigenvalues) are poorly constrained and have very large posterior variance. Understanding [sloppiness](@entry_id:195822) is key to interpreting the results of a calibration and designing new experiments that can better constrain the sloppy directions of our theoretical models.