## Introduction
In modern cosmology, confronting theoretical models with high-precision observational data often requires running computationally intensive simulations, a process that can take thousands of CPU hours for a single point in parameter space. This computational bottleneck severely limits our ability to perform comprehensive statistical inference, such as exploring vast parameter spaces with MCMC methods. Machine learning emulators offer a powerful solution to this challenge by learning a fast and accurate [surrogate model](@entry_id:146376) that approximates the output of these expensive simulations.

This article provides a systematic guide to the principles, applications, and hands-on practices of building and using machine learning emulators in a cosmological context. It addresses the crucial knowledge gap between understanding the theoretical potential of emulators and mastering the practical details required for their successful implementation. By working through this material, you will gain a deep understanding of how to construct robust, physically-informed, and statistically-principled emulators.

The journey begins in **Principles and Mechanisms**, where we will dissect the core components of an emulation pipeline, from defining the learning target and reducing its dimensionality to choosing between architectures like Neural Networks and Gaussian Processes. Next, **Applications and Interdisciplinary Connections** will demonstrate how these tools are applied to complex, high-dimensional [cosmological observables](@entry_id:747921), used to manage [systematic uncertainties](@entry_id:755766), and integrated into advanced inference engines. Finally, **Hands-On Practices** will provide concrete exercises to solidify your understanding of model selection, validation, and multi-fidelity emulation, equipping you with the practical skills needed to deploy these techniques in your own research.

## Principles and Mechanisms

Having established the foundational role of emulators in modern cosmology, this chapter delves into the principles and mechanisms that govern their design, training, and application. We will dissect the core components of an emulation pipeline, from defining the precise nature of the learning task to selecting an appropriate surrogate model and rigorously accounting for its inherent uncertainties. Our focus will be on building a systematic understanding of the choices an analyst must make and the trade-offs they entail.

### Defining the Emulation Target: From Observables to Learnable Representations

The first critical step in constructing an emulator is to define precisely what is being learned. The primary goal is to create a fast surrogate for the mapping from a vector of [cosmological parameters](@entry_id:161338), $\boldsymbol{\theta} \in \mathbb{R}^k$, to a predicted cosmological observable, such as the [matter power spectrum](@entry_id:161407) $P(k,z)$ or an [angular power spectrum](@entry_id:161125) $C_\ell$. These observables are often high-dimensional objects, represented as vectors evaluated at numerous points in [wavenumber](@entry_id:172452) $k$ or multipole space $\ell$. The choice of how to represent this target function has profound implications for the entire emulation workflow.

#### Logarithmic vs. Linear Scale for Power Spectra

Cosmological power spectra, being [ensemble averages](@entry_id:197763) of squared amplitudes (e.g., $C_\ell \propto \sum_m \langle |a_{\ell m}|^2 \rangle$), are by definition non-negative quantities. This physical constraint of **positivity** must be respected by the emulator. A naive emulator architecture that directly predicts the value of $P(k)$ or $C_\ell$ can easily produce unphysical negative values, which would require ad-hoc post-processing like clipping. A far more elegant and principled solution is to change the target of emulation from the observable $y$ to its logarithm, $\log y$. An emulator trained to predict $\log y$ can output any real number; the physical prediction is then recovered by exponentiation, $\hat{y} = \exp(\widehat{\log y})$, which automatically guarantees positivity [@problem_id:3478322].

Furthermore, cosmological power spectra often span several orders of magnitude. A training objective based on the absolute error, such as the Mean Squared Error (MSE) on $y$, would be overwhelmingly dominated by the high-amplitude regions of the spectrum (typically at large scales or low $k$/$\ell$), while being insensitive to the fitting accuracy in low-amplitude regions. However, from a scientific perspective, a $1\%$ error is often considered equally important regardless of the absolute scale. By emulating $\log y$, a standard MSE loss, $(\log \hat{y} - \log y)^2$, becomes approximately equivalent to minimizing the squared *fractional* error, $((\hat{y}-y)/y)^2$, for small errors. This re-weighting aligns the training objective with the scientific goal of achieving uniform relative accuracy across the entire spectrum [@problem_id:3478322].

Finally, the statistical properties of the target can be simplified by a logarithmic transform. For a Gaussian random field, the sample variance of an estimated power spectrum, known as **[cosmic variance](@entry_id:159935)**, is proportional to the square of the true spectrum: $\mathrm{Var}(\hat{C}_\ell) \approx \frac{2}{2\ell+1} C_\ell^2$. By applying a logarithmic transform, the variance becomes approximately constant: $\mathrm{Var}(\log \hat{C}_\ell) \approx \frac{2}{2\ell+1}$. This variance stabilization, or **homoscedasticity**, makes the logarithm a more natural quantity for statistical modeling and can simplify the structure of the likelihood and the training [loss function](@entry_id:136784) [@problem_id:3478322]. When the emulator's own uncertainty is modeled as Gaussian in log-space, this implies a [log-normal distribution](@entry_id:139089) for the observable itself, corresponding to multiplicative rather than additive errors—a more realistic model for many physical quantities.

#### Encoding Structural Priors: Smoothness and Positivity

Beyond simple positivity, physical observables often possess additional structural properties. For example, angular power spectra $C_\ell$ are known to be not only non-negative but also [smooth functions](@entry_id:138942) of the multipole $\ell$. These structural priors can and should be encoded directly into the emulator's architecture to improve its efficiency and physical realism.

Several strategies can enforce these constraints [@problem_id:3478338]:
1.  **Output Transformation:** As discussed, using an exponential output, $C_\ell = \exp(g(\ell, \boldsymbol{\theta}))$, enforces positivity. If the latent function $g(\ell, \boldsymbol{\theta})$ is modeled by a smooth architecture (e.g., a network with smooth activations or a GP with a smooth kernel), then $C_\ell$ will also be smooth. A similar approach is to model the output as the square of a latent function, $C_\ell = f(\ell, \boldsymbol{\theta})^2$, which also guarantees positivity and preserves smoothness.
2.  **Basis Function Expansion:** The observable can be represented as a linear combination of pre-defined basis functions that already possess the desired properties. For instance, we can model $C_\ell = \sum_i \alpha_i(\boldsymbol{\theta}) \phi_i(\ell)$, where the basis functions $\phi_i(\ell)$ are themselves smooth and positive (e.g., Gaussian bumps). Positivity of the full spectrum is then guaranteed by constraining the coefficients to be non-negative, $\alpha_i \ge 0$, which can be achieved by parameterizing them with a softplus function, $\alpha_i = \log(1+\exp(\beta_i))$, and having the emulator learn the unconstrained values $\beta_i$.
3.  **Regularization:** Smoothness can also be encouraged by adding a penalty term to the training loss that penalizes roughness, such as the integrated squared second derivative of the function, $\int (\partial_\ell^2 C_\ell)^2 d\ell$.

These techniques move beyond treating the emulator as a black box and instead infuse it with physical knowledge, leading to more data-efficient and robust models.

### Basis Representations and Dimensionality Reduction

Even after transformation, a cosmological spectrum may be defined on hundreds or thousands of bins, making the [effective dimension](@entry_id:146824) of the emulation target very high. Emulating each bin independently is inefficient as it ignores the strong correlations between adjacent bins. It is often advantageous to first find a low-dimensional representation of the spectral variations.

#### Principal Component Analysis (PCA)

Given a training set of $n$ spectra, $\lbrace \mathbf{y}^{(j)} \rbrace_{j=1}^n$, each being a vector in $\mathbb{R}^p$, PCA provides a systematic way to find the most compact [linear representation](@entry_id:139970). It constructs an [orthonormal basis](@entry_id:147779) for the space of spectra, ordered by the amount of variance they capture in the [training set](@entry_id:636396). The basis vectors, or **principal components** (PCs), are the eigenvectors of the data's empirical covariance matrix, $S = \mathbb{E}[(\mathbf{y}-\bar{\mathbf{y}})(\mathbf{y}-\bar{\mathbf{y}})^T]$.

Any spectrum can then be approximated by projecting it onto the first $m$ principal components, where $m \ll p$:
$$
\mathbf{y} \approx \hat{\mathbf{y}}_m = \bar{\mathbf{y}} + W_m \mathbf{c}_m
$$
where $\bar{\mathbf{y}}$ is the mean spectrum, $W_m$ is the matrix whose columns are the first $m$ eigenvectors of $S$, and $\mathbf{c}_m = W_m^T (\mathbf{y} - \bar{\mathbf{y}})$ are the PCA coefficients. This projection is optimal in the sense that it minimizes the mean squared reconstruction error for any choice of $m$-dimensional linear basis [@problem_id:3478388]. The fraction of total variance unexplained by the first $m$ components is given by the ratio of the sum of the discarded eigenvalues to the sum of all eigenvalues:
$$
\varepsilon_m = \frac{\sum_{j=m+1}^{p} \lambda_j}{\sum_{j=1}^{p} \lambda_j}
$$
where $\lambda_j$ are the eigenvalues of $S$ in descending order. For many [cosmological observables](@entry_id:747921), a handful of PCs ($m \sim 5-10$) can capture over $99.9\%$ of the variance, meaning the emulation task can be reduced from predicting a $p$-dimensional vector $\mathbf{y}$ to predicting an $m$-dimensional vector of coefficients $\mathbf{c}_m$, a significantly simpler problem [@problem_id:3478388].

#### Polynomial Chaos Expansion (PCE)

An alternative approach is to construct a basis in the input [parameter space](@entry_id:178581) rather than the output space. If the input parameters $\boldsymbol{\theta}$ can be transformed into a set of [independent random variables](@entry_id:273896) with a known probability measure (e.g., standard Gaussians), then any square-integrable function of these parameters, such as $P(k,z; \boldsymbol{\theta})$, can be expanded in a basis of orthonormal polynomials. This is known as **Polynomial Chaos Expansion**.

For instance, if the parameters are standard Gaussian variables $\xi_1, \dots, \xi_k$, the appropriate basis is formed by products of Hermite polynomials. A truncated expansion of the observable $y(\boldsymbol{\theta})$ up to a total polynomial degree $P$ takes the form:
$$
y(\boldsymbol{\theta}) \approx \sum_{|\boldsymbol{\alpha}| \le P} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\theta})
$$
where $\Psi_{\boldsymbol{\alpha}}$ are multivariate Hermite polynomials and $c_{\boldsymbol{\alpha}}$ are coefficients to be determined. Because the basis is orthonormal with respect to the input parameter measure, the coefficients can be found via projection: $c_{\boldsymbol{\alpha}} = \mathbb{E}[y(\boldsymbol{\theta}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\theta})]$. In practice, these coefficients are often determined via [least-squares regression](@entry_id:262382) using a set of training points. Once determined, this expansion provides a global [polynomial approximation](@entry_id:137391) of the simulator over the entire parameter space [@problem_id:3478356].

### Core Emulator Architectures and Their Properties

With a well-defined learning target, we now turn to the choice of the "machine" for the emulator. Two architectures dominate the landscape: Neural Networks and Gaussian Processes.

#### Neural Networks (NNs)

Feedforward neural networks are universal function approximators. The **Universal Approximation Theorem (UAT)** states that a shallow network with a single hidden layer of sufficient width and a suitable non-polynomial activation function can approximate any continuous function on a [compact domain](@entry_id:139725) to arbitrary accuracy [@problem_id:3478363].

However, the UAT is an [existence theorem](@entry_id:158097); it does not guarantee that such a network is learnable or efficient. In practice, several challenges arise:
- **Curse of Dimensionality:** While the UAT guarantees existence, the number of neurons (width) or training samples required to achieve a given accuracy for an arbitrary function can grow exponentially with the input dimension $d_\theta$. For a general function with Lipschitz constant $L$, covering the parameter space to ensure an error no greater than $\varepsilon$ requires a number of samples scaling as $(L/\varepsilon)^{d_\theta}$ [@problem_id:3478363].
- **Depth vs. Width:** Modern deep learning has shown that for certain classes of functions, particularly those with a compositional structure, deep networks can be exponentially more efficient than shallow ones. Increasing depth can mitigate the curse of dimensionality, a benefit not captured by the classic UAT.
- **Trainability:** The UAT says nothing about our ability to find the optimal network weights. Training involves navigating a high-dimensional, non-convex [loss landscape](@entry_id:140292), where optimization algorithms like [stochastic gradient descent](@entry_id:139134) may only find a [local minimum](@entry_id:143537).

Despite these caveats, NNs are powerful and flexible emulators, capable of learning highly complex relationships in cosmological data.

#### Gaussian Processes (GPs)

A Gaussian Process offers a non-parametric, probabilistic approach to regression. A GP defines a [prior distribution](@entry_id:141376) over functions. It is fully specified by a mean function (often taken to be zero) and a **[covariance function](@entry_id:265031)**, or **kernel**, $k(\mathbf{x}, \mathbf{x}')$, which defines the covariance between the function's values at any two points $\mathbf{x}$ and $\mathbf{x}'$. A key assumption is that any finite collection of function values follows a multivariate Gaussian distribution.

The choice of kernel is critical as it encodes prior beliefs about the function's properties, most notably its smoothness.
- **Squared Exponential (SE) Kernel:** $k(\tau) = \sigma^2 \exp(-\tau^2 / (2\ell^2))$, where $\tau=|\mathbf{x}-\mathbf{x}'|$. This kernel is infinitely differentiable, meaning [sample paths](@entry_id:184367) from a GP with an SE kernel are also infinitely differentiable (in mean-square) and analytic. This imposes a very strong smoothness assumption, which can be inappropriate for physical functions that are smooth but not analytic, potentially leading to **oversmoothing** of important features [@problem_id:3478385].
- **Matérn Kernel Family:** This family, parameterized by a smoothness parameter $\nu$, provides more flexibility. Sample paths from a GP with a Matérn kernel are $p$ times mean-square differentiable, where $p \approx \nu$. For instance, the Matérn-$\frac{3}{2}$ kernel yields once-differentiable functions, and the Matérn-$\frac{5}{2}$ kernel yields twice-differentiable functions. These are often a more realistic choice for physical observables like the [matter power spectrum](@entry_id:161407), which contains features like Baryon Acoustic Oscillations (BAO) and non-linear enhancements that make it smooth but not infinitely so. The Matérn kernel allows for "controlled [differentiability](@entry_id:140863)," matching the prior to the known physics of the problem [@problem_id:3478385].

The main drawback of exact GPs is their [computational complexity](@entry_id:147058). Training an exact GP on $N$ data points requires inverting an $N \times N$ covariance matrix, a task with $O(N^3)$ [time complexity](@entry_id:145062) and $O(N^2)$ memory complexity. Prediction for a single test point costs $O(N^2)$. This scaling makes exact GPs intractable for datasets with more than a few thousand points. To overcome this, **sparse GP approximations** are used. These methods, such as those based on a set of $M \ll N$ **inducing points**, construct a [low-rank approximation](@entry_id:142998) to the full covariance matrix. This reduces the training complexity to roughly $O(NM^2)$ and prediction complexity to $O(M^2)$, making GPs applicable to much larger datasets [@problem_id:3478340].

### Advanced Emulation Strategies for Cosmological Inference

Building a high-quality emulator is often just the first step. Integrating it into a full cosmological analysis requires further sophistication.

#### Forward Model Emulation vs. Likelihood Emulation

When the ultimate goal is Bayesian inference—finding the posterior $p(\boldsymbol{\theta}|d)$ for data $d$—there are two main ways to use an emulator [@problem_id:3478382]:

1.  **Emulate the Forward Model:** Here, the emulator learns the mapping from parameters $\boldsymbol{\theta}$ to the expected value of a summary statistic, $\mathbf{y}(\boldsymbol{\theta}) = \mathbb{E}[\mathbf{s}(d)|\boldsymbol{\theta}]$. The likelihood is then constructed using an analytic approximation, typically a multivariate Gaussian: $p(\mathbf{s}|\boldsymbol{\theta}) \approx \mathcal{N}(\mathbf{s} | \mathbf{y}_{\text{emu}}(\boldsymbol{\theta}), C(\boldsymbol{\theta}))$. This approach is efficient and preferred when the summary statistic $\mathbf{s}(d)$ is nearly **sufficient** (captures all information about $\boldsymbol{\theta}$) and its [sampling distribution](@entry_id:276447) is well-approximated by a Gaussian with a simple or easily modeled covariance matrix $C(\boldsymbol{\theta})$.

2.  **Emulate the Likelihood:** In this more powerful but challenging approach, the emulator learns the entire [likelihood function](@entry_id:141927) $p(\mathbf{s}|\boldsymbol{\theta})$ or even $p(d|\boldsymbol{\theta})$ directly. This is a [density estimation](@entry_id:634063) problem, often tackled with models like [normalizing flows](@entry_id:272573). This strategy is necessary when [summary statistics](@entry_id:196779) are insufficient (e.g., they discard non-Gaussian information) or when the data distribution is highly non-Gaussian with a complex, parameter-dependent covariance that cannot be easily modeled analytically. This approach makes fewer assumptions but requires a more flexible model and typically a larger [training set](@entry_id:636396).

#### Multi-Fidelity Emulation and Transfer Learning

High-fidelity [cosmological simulations](@entry_id:747925) are computationally expensive, limiting the size of training sets. Often, however, cheaper, lower-fidelity (approximate) simulations are available in abundance. **Transfer learning** provides a framework for leveraging this multi-fidelity information. The strategy is to first pretrain an emulator on a large dataset of low-fidelity simulations, and then fine-tune it on the small, precious set of high-fidelity simulations.

A successful pretraining strategy often involves incorporating known physics. For instance, the pretraining loss can include a term that penalizes deviations from linear theory at large scales, anchoring the emulator in a physically correct regime [@problem_id:3478321]. After pretraining, the model is fine-tuned on the high-fidelity data using the statistically optimal loss function (e.g., a Gaussian [log-likelihood](@entry_id:273783) that accounts for [error covariance](@entry_id:194780)).

A key risk in this process is **[negative transfer](@entry_id:634593)**, where pretraining on the low-fidelity data actually harms the final performance on the high-fidelity task. To diagnose this robustly, especially with a small high-fidelity dataset, one must rely on rigorous statistical validation, not simple [heuristics](@entry_id:261307). The gold standard is $K$-fold [cross-validation](@entry_id:164650) on the high-fidelity set, where in each fold, a model trained from scratch is compared against a fine-tuned pretrained model. A paired statistical test on the held-out validation scores can then determine with confidence whether pretraining provided a significant benefit or detriment [@problem_id:3478321].

#### Accounting for Emulator Uncertainty

An emulator is an approximation, and its predictions are not perfect. A rigorous analysis must propagate the emulator's own uncertainty into the final cosmological parameter constraints. Ignoring this **emulator uncertainty** can lead to artificially tight and overconfident posterior distributions.

One powerful method for handling this is to model the emulator's residual error, $r(k,z; \boldsymbol{\theta}) = p_{\text{true}}(k,z; \boldsymbol{\theta}) - p_{\text{em}}(k,z; \boldsymbol{\theta})$, as a stochastic process. A common and flexible choice is to model the residuals as a correlated Gaussian Process over the observable's domain (e.g., $(k,z)$ space). This GP model for the residual, with its own covariance structure, can be incorporated directly into the total covariance of the data likelihood. The total [data covariance](@entry_id:748192) matrix then becomes $\boldsymbol{\Sigma}_{\text{tot}} = \boldsymbol{\Sigma}_n + \boldsymbol{\Sigma}_r$, where $\boldsymbol{\Sigma}_n$ is the observational noise covariance and $\boldsymbol{\Sigma}_r$ is the emulator residual covariance [@problem_id:3478394].

Adding this residual covariance term correctly accounts for the fact that emulator errors can be correlated across different $k$ or $\ell$ bins. This effectively down-weights the information from the data, leading to a more conservative and honest estimation of the posterior [credible intervals](@entry_id:176433) for the [cosmological parameters](@entry_id:161338). The magnitude and correlation structure of the residual model directly control the degree to which the final parameter constraints are inflated to account for the emulator's imperfection.