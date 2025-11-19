## Introduction
In the pursuit of predictive science, the goal of Computational Fluid Dynamics (CFD) is evolving beyond generating a single, deterministic answer. To achieve true predictive power, simulations must be accompanied by a quantitative statement of confidence, acknowledging the inherent uncertainties in physical processes, modeling assumptions, and numerical approximations. This shift addresses a critical knowledge gap: how can we systematically identify, manage, and quantify the impact of these various uncertainties to produce truly reliable and trustworthy results? Without a rigorous framework, the predictions from complex CFD models remain incomplete and potentially misleading.

This article provides a comprehensive guide to the theory and practice of Uncertainty Quantification (UQ) in CFD. Over the following chapters, you will develop a deep understanding of this essential discipline. The journey begins in the **Principles and Mechanisms** chapter, which deconstructs the different sources of uncertainty—aleatoric, epistemic, and numerical—and introduces the core mathematical techniques for modeling and propagating them. Next, the **Applications and Interdisciplinary Connections** chapter showcases the transformative power of UQ in real-world scenarios, from aerospace engineering to microfluidics, demonstrating how it enables robust design, [reliability analysis](@entry_id:192790), and data-driven model improvement. Finally, the **Hands-On Practices** chapter offers practical exercises to apply these concepts, solidifying your ability to move from theoretical knowledge to proficient application.

## Principles and Mechanisms

The ultimate goal of computational fluid dynamics (CFD) in a predictive science context is not merely to compute a single, deterministic answer, but to issue a prediction accompanied by a quantitative statement of confidence. This requires a rigorous framework for identifying, modeling, propagating, and analyzing the various uncertainties that influence the simulation result. This chapter lays the foundational principles and describes the core mechanisms for performing uncertainty quantification (UQ) in CFD.

### The Anatomy of Uncertainty in CFD

A crucial first step in any UQ endeavor is to categorize the different sources of uncertainty. In the context of [predictive modeling](@entry_id:166398), it is essential to distinguish between uncertainty that is inherent to the system being modeled, uncertainty that arises from our own lack of knowledge, and errors that are artifacts of our numerical approximation.

#### Aleatoric and Epistemic Uncertainty

Uncertainties related to the physical system and its mathematical representation are broadly classified into two categories: aleatoric and epistemic.

**Aleatoric uncertainty** refers to the inherent, irreducible variability or randomness within a system or its environment. The term derives from the Latin *alea*, meaning "die," reflecting an origin in chance. This type of uncertainty cannot be reduced by collecting more data or refining a model, although it can be better characterized. It is a feature of the system itself. In a mathematical framework, [aleatoric uncertainty](@entry_id:634772) is typically represented by a fixed, objective probability distribution, $p(\xi)$, derived from observed frequencies or physical principles.

**Epistemic uncertainty** stems from a lack of knowledge on the part of the modeler. The term originates from the Greek *episteme*, meaning "knowledge." This includes uncertainty about the appropriate values for model parameters, ignorance of the correct functional form of a model, or incomplete knowledge of the underlying physics. In principle, epistemic uncertainty is reducible. It can be diminished by acquiring more data (e.g., through experiments), improving the underlying theory, or developing higher-fidelity models. In a Bayesian context, epistemic uncertainty is often represented by a probability distribution, $\pi(\theta)$, that reflects a subjective [degree of belief](@entry_id:267904) and can be updated to a [posterior distribution](@entry_id:145605), $\pi(\theta \mid D)$, as new data $D$ becomes available.

Consider the simulation of turbulent, incompressible flow over a [backward-facing step](@entry_id:746640), a canonical problem in CFD. The mean flow is governed by the Reynolds-Averaged Navier–Stokes (RANS) equations. Suppose our quantity of interest (QoI) is the mean [reattachment length](@entry_id:754144), $L_r$. We can identify both aleatoric and epistemic uncertainties in this problem [@problem_id:3385624].

-   **Example of Aleatoric Uncertainty:** The inlet velocity profile, $u_{\text{in}}(y; \xi)$, may exhibit run-to-run variability in a wind tunnel experiment due to small, uncontrollable perturbations in operating conditions. This inherent randomness is aleatoric. Even with a perfect model of the fluid dynamics, we could not predict the exact [reattachment length](@entry_id:754144) for a *specific* future run, but we could predict the probability distribution of $L_r$ arising from this stochastic input.

-   **Example of Epistemic Uncertainty:** The RANS equations are not a first-principles description of turbulence; they require a closure model for the Reynolds stress tensor, $\boldsymbol{\tau}_R$. Our choice of turbulence model (e.g., $k$-$\epsilon$, $k$-$\omega$) and the values of its associated parameters, $\theta$, are a significant source of [epistemic uncertainty](@entry_id:149866). This reflects our incomplete knowledge of how to accurately represent the effects of turbulence on the mean flow. This uncertainty can be reduced through validation studies against experimental data or by using more sophisticated (and computationally expensive) models like Large Eddy Simulation (LES).

#### Numerical Error

Distinct from both [aleatoric and epistemic uncertainty](@entry_id:184798) is **numerical error**, which is an artifact of the computational process used to approximate the solution of the chosen mathematical model. Verification is the process of estimating and controlling these errors. Numerical error is not a physical property of the system but a feature of our simulation. The primary sources of numerical error in CFD are [@problem_id:3385672]:

-   **Discretization Error ($e_h^{\mathrm{disc}}$):** This is the error introduced by approximating the continuous [partial differential equations](@entry_id:143134) (PDEs) with a system of algebraic equations on a finite computational mesh of characteristic size $h$. For a consistent numerical method of order $p$, this error typically scales as $O(h^p)$. In UQ studies, discretization error is not random noise; for a given input, it is a deterministic, spatially correlated bias field that contaminates the solution.

-   **Iterative Solver Error ($e_h^{\mathrm{iter}}$):** The large algebraic systems in CFD are almost always solved using iterative methods. If the solver is terminated before converging to the exact discrete solution, an iterative error remains. This error is controllable by setting a sufficiently tight solver tolerance. In UQ, it is typically treated as a bounded, deterministic contribution that should be made negligible compared to other uncertainties.

-   **Floating-Point Round-off Error ($e^{\mathrm{fp}}$):** This error arises because computers represent real numbers with finite precision. While individual round-off errors are tiny, their accumulation over millions or billions of arithmetic operations can become significant, especially in [ill-conditioned problems](@entry_id:137067). In UQ, the aggregate effect can sometimes be modeled as a source of [aleatoric uncertainty](@entry_id:634772)—a mean-zero, weakly [correlated noise](@entry_id:137358) that establishes a floor on the achievable precision.

It is a critical error in reasoning to confuse [numerical error](@entry_id:147272) with physical uncertainty. Demonstrating that a simulation is "grid-converged" (i.e., that [discretization error](@entry_id:147889) is small) says nothing about whether the underlying physical model is correct.

#### The VVUQ Framework and a Unified View of Variance

The systematic management of these different facets of uncertainty and error is formalized in the **Verification, Validation, and Uncertainty Quantification (VVUQ)** framework, which is codified in standards such as ASME V&V 20 [@problem_id:3385653].

-   **Verification** is the process of assessing numerical error, asking the question: "Are we solving the equations right?" It involves activities like code verification (e.g., using the Method of Manufactured Solutions) and solution verification (estimating [discretization](@entry_id:145012) and iterative errors via [grid refinement](@entry_id:750066) studies).

-   **Validation** is the process of assessing [model-form error](@entry_id:274198) by comparing simulation predictions against experimental data, asking: "Are we solving the right equations?" A rigorous validation process must account for uncertainties in the simulation inputs, [numerical errors](@entry_id:635587), and the experimental measurements themselves. Its primary goal is to assess and reduce epistemic uncertainty.

-   **Uncertainty Quantification (UQ)** is the end-to-end process of propagating input uncertainties (both aleatoric and epistemic) through the model to determine the uncertainty in the final prediction.

These concepts can be unified through a formal decomposition of the total predictive variance. Let the total predicted quantity of interest be $Q = q(\boldsymbol{\theta}, \Delta) + \varepsilon_h$, where $q$ is the exact solution of a model with parameters $\boldsymbol{\theta}$ and model-form discrepancy $\Delta$, and $\varepsilon_h$ is the numerical error. Under the minimal assumption that the numerical error is conditionally unbiased, i.e., $\mathbb{E}[\varepsilon_h \mid \boldsymbol{\theta}, \Delta] = 0$, the total variance can be exactly decomposed using the law of total variance [@problem_id:3385638]:

$ \operatorname{Var}(Q) = \underbrace{\operatorname{Var}_{\boldsymbol{\theta}}\!\Big( \mathbb{E}_{\Delta \mid \boldsymbol{\theta}}\big[q(\boldsymbol{\theta},\Delta)\big] \Big)}_{\text{Parameter Uncertainty}} + \underbrace{\mathbb{E}_{\boldsymbol{\theta}}\!\Big( \operatorname{Var}_{\Delta \mid \boldsymbol{\theta}}\big(q(\boldsymbol{\theta},\Delta)\big) \Big)}_{\text{Model-Form Uncertainty}} + \underbrace{\mathbb{E}_{(\boldsymbol{\theta},\Delta)}\!\Big( \operatorname{Var}(\varepsilon_h \mid \boldsymbol{\theta},\Delta) \Big)}_{\text{Numerical Error Variance}} $

This powerful equation shows how the total predictive uncertainty is a sum of contributions from input [parameter uncertainty](@entry_id:753163), [model-form uncertainty](@entry_id:752061), and [numerical error](@entry_id:147272). It provides a mathematical roadmap for a comprehensive UQ analysis.

### Modeling and Representing Uncertainty

To perform UQ, we must first create mathematical representations of the uncertain inputs. These models form the foundation for all subsequent propagation and analysis.

#### Random Fields for Spatially Distributed Uncertainty

In many CFD problems, uncertainty is not confined to a few scalar parameters but is distributed in space. For example, inlet turbulence, boundary roughness, or material property variations are best described as **[random fields](@entry_id:177952)**. A random field $u(x, \omega)$ is a function of a spatial coordinate $x$ whose value at each point is a random variable.

For a second-order [random field](@entry_id:268702), its statistical structure can be characterized by its mean function and its [covariance function](@entry_id:265031) [@problem_id:3385621]:
-   **Mean Function:** $m(x) = \mathbb{E}[u(x, \omega)]$ describes the average value of the field at each point $x$.
-   **Covariance Function:** $C(x, x') = \mathbb{E}[(u(x, \omega) - m(x))(u(x', \omega) - m(x'))]$ describes the correlation between the field's values at two different points, $x$ and $x'$. The [covariance function](@entry_id:265031) must be symmetric ($C(x,x') = C(x',x)$) and positive semidefinite. The variance at a point $x$ is given by $C(x,x)$.

The **[correlation length](@entry_id:143364)**, $\ell$, is a key parameter of the [covariance function](@entry_id:265031) that quantifies the spatial distance over which the field's values are significantly correlated. A short correlation length implies a rapidly fluctuating field, while a long correlation length implies a smooth field.

A common and flexible family of covariance functions is the **Matérn class**, which includes the widely used **exponential covariance** as a special case. For a one-dimensional field, the exponential covariance is given by:
$ C(x, x') = \sigma^2 \exp(-|x-x'|/\ell) $
where $\sigma^2$ is the variance and $\ell$ is the [correlation length](@entry_id:143364).

A field is **[wide-sense stationary](@entry_id:144146)** if its mean is constant ($m(x) = m$) and its covariance depends only on the separation vector ($C(x,x') = C(x-x')$). It is **homogeneous** if its full finite-dimensional probability distributions are invariant under [spatial translation](@entry_id:195093). For a Gaussian [random field](@entry_id:268702) (where any collection of points has a multivariate Gaussian distribution), homogeneity and [wide-sense stationarity](@entry_id:173765) are equivalent.

To use a [random field](@entry_id:268702) in a computation, it must be discretized. The **Karhunen-Loève (KL) expansion** provides a spectrally optimal way to do this. It represents the [random field](@entry_id:268702) as a [series expansion](@entry_id:142878) with deterministic spatial modes and uncorrelated random coefficients:
$ u(x, \omega) = m(x) + \sum_{n=1}^{\infty} \sqrt{\lambda_n} \phi_n(x) \xi_n(\omega) $
where $(\lambda_n, \phi_n)$ are the eigenpairs of the covariance operator and $\xi_n$ are uncorrelated random variables with [zero mean](@entry_id:271600) and unit variance. The correlation length $\ell$ of the underlying [covariance kernel](@entry_id:266561) governs the rate of decay of the eigenvalues $\lambda_n$, determining how many terms are needed to accurately represent the field.

#### Physical Plausibility of Stochastic Models

When constructing a model for an uncertain input, especially a boundary condition in CFD, it is critical to ensure that the model respects the underlying physics of the governing equations for every possible realization. Failure to do so can lead to [ill-posed problems](@entry_id:182873) and non-physical results.

Consider modeling an uncertain inlet velocity profile for an incompressible channel flow [@problem_id:3385652]. A plausible stochastic model $u_{\text{in}}(x,t)$ should satisfy several constraints:
1.  **Mass Conservation:** The global [continuity equation](@entry_id:145242) requires that the net flux across the domain boundary is zero. If the outlet condition is not adjusted in response, this implies that the total volumetric inflow rate, $Q_{\text{in}} = \int_{\Gamma_{\text{in}}} u_{\text{in}} dS$, must be constant for every realization of the uncertainty, not just on average.
2.  **No Backflow:** For an inlet, it is typically required that the velocity be strictly positive everywhere, $u_{\text{in}}(x,t) > 0$. Violating this condition introduces recirculation at the inlet boundary, which is often non-physical and can cause severe [numerical instability](@entry_id:137058).
3.  **Finite Energy:** The kinetic energy flux through the boundary must be finite. This imposes regularity conditions on the [random field](@entry_id:268702) model. A model based on spatial [white noise](@entry_id:145248), for instance, would have [infinite variance](@entry_id:637427) at every point and introduce infinite energy, making it physically untenable.

One common approach is an additive model: $u_{\text{in}}(x) = \bar{u}(x) + \sigma \phi(x) \xi$, where $\bar{u}(x)$ is the mean profile and $\phi(x)\xi$ is a random perturbation. To satisfy [mass conservation](@entry_id:204015), the perturbation shape function $\phi(x)$ must have zero integral, $\int_{\Gamma_{\text{in}}} \phi(x) dS = 0$. To control the probability of backflow, the perturbation amplitude $\sigma$ must be sufficiently small relative to the minimum value of the mean profile $\bar{u}(x)$. For a Gaussian random variable $\xi \sim \mathcal{N}(0,1)$, choosing $\sigma \le \frac{\min \bar{u}(x)}{3 \|\phi\|_{L^{\infty}}}$ ensures that the probability of backflow is less than approximately $0.3\%$.

An alternative that elegantly satisfies both [mass conservation](@entry_id:204015) and positivity is a normalized multiplicative [log-normal model](@entry_id:270159) [@problem_id:3385652]. This construction ensures positivity by using an [exponential function](@entry_id:161417) and enforces the exact inflow rate for every realization through a random normalization factor.

### Propagating Uncertainty

Once mathematical models for the uncertain inputs are established, the next step is to propagate them through the CFD solver to determine the uncertainty in the quantity of interest. This involves solving the governing equations for a representative set of the inputs.

#### Monte Carlo Simulation

The most fundamental and robust method for [uncertainty propagation](@entry_id:146574) is **Monte Carlo (MC) simulation**. The concept is straightforward:
1.  Draw a large number $N$ of independent and identically distributed (IID) samples, $\{\mathbf{X}_i\}_{i=1}^N$, from the [joint probability distribution](@entry_id:264835) of the uncertain input parameters $\mathbf{X}$.
2.  For each sample $\mathbf{X}_i$, run the deterministic CFD solver to compute the corresponding output QoI, $Q(\mathbf{X}_i)$.
3.  Use the resulting collection of output samples, $\{Q(\mathbf{X}_i)\}_{i=1}^N$, to estimate the statistical properties of the output distribution.

The mean of the QoI, $\mu = \mathbb{E}[Q(\mathbf{X})]$, is estimated by the [sample mean](@entry_id:169249) [@problem_id:3385629]:
$ \hat{\mu} = \frac{1}{N} \sum_{i=1}^N Q(\mathbf{X}_i) $

This estimator has several important properties. It is **unbiased**, meaning $\mathbb{E}[\hat{\mu}] = \mu$. If the QoI has a [finite variance](@entry_id:269687) $\sigma^2 = \operatorname{Var}(Q(\mathbf{X}))$, the variance of the estimator is $\operatorname{Var}(\hat{\mu}) = \sigma^2/N$. The root-[mean-square error](@entry_id:194940) (RMSE) of the estimator is therefore $\sigma/\sqrt{N}$. This reveals the characteristic **convergence rate of Monte Carlo simulation, which is $O(N^{-1/2})$**. This rate is independent of the number of uncertain parameters $d$, which is a major advantage, but it is also quite slow; to reduce the error by a factor of 10, one must perform 100 times more simulations.

The **Central Limit Theorem (CLT)** states that for large $N$, the distribution of the sample mean $\hat{\mu}$ approaches a [normal distribution](@entry_id:137477). This allows us to construct a $(1-\alpha)$ confidence interval for the true mean $\mu$:
$ \mu \in \left[ \hat{\mu} - z_{1-\alpha/2} \frac{\hat{\sigma}}{\sqrt{N}}, \quad \hat{\mu} + z_{1-\alpha/2} \frac{\hat{\sigma}}{\sqrt{N}} \right] $
where $\hat{\sigma}$ is the sample standard deviation of the output samples and $z_{1-\alpha/2}$ is the corresponding quantile of the [standard normal distribution](@entry_id:184509).

#### Efficient Propagation Methods

The slow convergence of Monte Carlo and the high computational cost of each CFD simulation motivate the need for more efficient propagation methods, especially when the QoI is a smooth function of the inputs.

##### Stochastic Collocation and Sparse Grids

**Stochastic Collocation** methods approximate the high-dimensional integral for the expected value of the QoI using a quadrature rule. Instead of random sampling, they use a deterministic set of points (collocation nodes) and weights. A simple approach is to use a **tensor-product grid**, which combines one-dimensional [quadrature rules](@entry_id:753909) for each uncertain parameter. However, if a 1D rule requires $n$ points, the $d$-dimensional tensor-product rule requires $n^d$ points. This [exponential growth](@entry_id:141869) in cost with dimension is known as the **[curse of dimensionality](@entry_id:143920)**, rendering this approach infeasible for even a moderate number of uncertain inputs.

**Sparse grids** offer a powerful remedy. The **Smolyak sparse-grid construction** builds a high-dimensional quadrature rule by combining a specific set of smaller tensor-product rules in a way that prioritizes accuracy for functions that are smooth and dominated by low-order interactions between variables [@problem_id:3385696]. Based on a hierarchy of nested 1D [quadrature rules](@entry_id:753909), the Smolyak operator of level $q$ is defined as:
$ \mathcal{A}_q^d = \sum_{\boldsymbol{k} \in \mathbb{N}^d : \|\boldsymbol{k}\|_1 \le q} \bigotimes_{i=1}^d \Delta_i^{(k_i)} $
where $\boldsymbol{k}=(k_1, \dots, k_d)$ is a multi-index of levels, $\|\boldsymbol{k}\|_1 = \sum k_i$, and $\Delta_i^{(k_i)}$ is the hierarchical difference between level $k_i$ and level $k_i-1$ quadrature operators in dimension $i$.

The key advantage is computational cost. Whereas a tensor-product grid's size grows as $O(n^d)$, the number of points in a sparse grid grows much more slowly, often as $O(n (\log n)^{d-1})$. For moderately high dimensions ($d \approx 5-15$) and smooth problems, sparse grids can achieve accuracy comparable to Monte Carlo with orders of magnitude fewer CFD simulations.

##### Surrogate Modeling: Gaussian Processes

Another strategy to overcome high computational cost is to replace the expensive CFD model with a cheap-to-evaluate approximation, known as a **[surrogate model](@entry_id:146376)** or **metamodel**. The surrogate is first trained using a limited number of high-fidelity CFD runs and is then used for subsequent UQ tasks like propagation or sensitivity analysis.

**Gaussian Process (GP) regression** is a powerful, non-parametric Bayesian approach for building [surrogate models](@entry_id:145436) [@problem_id:3385632]. A GP defines a probability distribution over functions. It is fully specified by a mean function $m(\mathbf{x})$ and a [covariance function](@entry_id:265031) (or kernel) $k(\mathbf{x}, \mathbf{x}')$. The kernel encodes our prior beliefs about the function's properties, such as its smoothness and length scales. A common choice is the **squared-exponential kernel** with Automatic Relevance Determination (ARD), which assigns a different [correlation length](@entry_id:143364)-scale $\ell_j$ to each input dimension $x_j$:
$ k(\mathbf{x},\mathbf{x}') = \sigma_f^2 \exp\left(-\frac{1}{2}\sum_{j=1}^{d}\frac{(x_j-x'_j)^2}{\ell_j^2}\right) $
The hyperparameters $(\sigma_f, \ell_1, \dots, \ell_d)$ are typically learned by maximizing the [marginal likelihood](@entry_id:191889) of the training data.

Given a set of $n$ training points $(\mathbf{X}, \mathbf{y})$, the GP framework provides analytical formulas for the predictive distribution at a new, untested point $\mathbf{x}_*$. The posterior distribution of the QoI $Q(\mathbf{x}_*)$ is Gaussian with a predictive mean and variance given by:
$ \mathbb{E}[Q(\mathbf{x}_*) \mid \mathbf{y}] = m(\mathbf{x}_*) + \mathbf{k}_*^{\top}(\mathbf{K} + \sigma_n^2 \mathbf{I})^{-1}(\mathbf{y} - \mathbf{m}) $
$ \mathrm{Var}[Q(\mathbf{x}_*) \mid \mathbf{y}] = k(\mathbf{x}_*,\mathbf{x}_*) - \mathbf{k}_*^{\top}(\mathbf{K} + \sigma_n^2 \mathbf{I})^{-1}\mathbf{k}_* $
Here, $\mathbf{K}$ is the covariance matrix of the training inputs, $\mathbf{k}_*$ is the vector of covariances between the training inputs and the test point, $\mathbf{m}$ is the prior [mean vector](@entry_id:266544), and $\sigma_n^2$ is the variance of any observation noise.

A key strength of GPs is that they provide not only a point prediction (the predictive mean) but also a measure of the uncertainty in that prediction (the predictive variance). The predictive variance is naturally smaller near training data points and larger in regions of the input space that are sparsely sampled, making GPs ideal for applications like adaptive sampling and [optimization under uncertainty](@entry_id:637387).

### Analyzing Uncertainty: Sensitivity Analysis

After propagating uncertainty, a critical final step is to analyze the results to understand which input uncertainties have the most significant impact on the output uncertainty. This is the domain of **sensitivity analysis (SA)**.

A simple approach is **[local sensitivity analysis](@entry_id:163342)**, which examines the effect of small perturbations around a single nominal point in the input space. This is typically done by computing the partial derivatives of the output with respect to each input, $\partial Q / \partial X_i$. While easy to compute, local methods are often inadequate for UQ because they cannot capture the effects of large input variations or the non-linear interactions between inputs.

**Global Sensitivity Analysis (GSA)** addresses these limitations by examining the influence of each input across its entire range of uncertainty. The most widely used GSA method is variance-based, often called **Sobol' analysis**, which decomposes the output variance into contributions from each input or groups of inputs [@problem_id:3385633]. This method relies on the assumption that the input variables are independent.

The foundation of this method is the law of total variance. For an input $X_i$, the total variance of the output $Q(\mathbf{X})$ can be decomposed as:
$ \operatorname{Var}(Q) = \operatorname{Var}_{X_i}(\mathbb{E}[Q \mid X_i]) + \mathbb{E}_{X_i}[\operatorname{Var}(Q \mid X_i)] $
The term $\operatorname{Var}_{X_i}(\mathbb{E}[Q \mid X_i])$ represents the variance of the expected value of $Q$ when only $X_i$ is varied (and all other inputs are averaged out). This is the "main effect" of $X_i$ on the output variance.

This leads to the definition of the **first-order Sobol' index**, $S_i$, which is the fraction of the total variance caused by the main effect of $X_i$:
$ S_i = \frac{\operatorname{Var}_{X_i}(\mathbb{E}_{\mathbf{X}_{\sim i}}[Q(\mathbf{X}) \mid X_i])}{\operatorname{Var}(Q(\mathbf{X}))} $
where $\mathbf{X}_{\sim i}$ denotes all inputs except $X_i$. The sum of all first-order indices, $\sum_i S_i$, is less than or equal to 1. If the sum is less than 1, the remaining variance is due to non-linear interactions between the inputs.

To capture these interaction effects, we define the **total Sobol' index**, $S_{T_i}$. This index measures the total contribution of $X_i$ to the output variance, including its main effect and all its interactions with other inputs. It is defined as the fraction of variance that would *remain* if we could fix all inputs *except* $X_i$:
$ S_{T_i} = \frac{\mathbb{E}_{\mathbf{X}_{\sim i}}[\operatorname{Var}_{X_i}(Q(\mathbf{X}) \mid \mathbf{X}_{\sim i})]}{\operatorname{Var}(Q(\mathbf{X}))} $
The difference $S_{T_i} - S_i$ quantifies the contribution of all interaction effects involving $X_i$. If $S_{T_i}$ is close to zero, the input $X_i$ can be considered non-influential and potentially fixed at its nominal value, simplifying the model. If $S_{T_i}$ is large but $S_i$ is small, the input $X_i$ is influential primarily through its interactions with other parameters. Sobol' indices provide a powerful, quantitative ranking of input importance, guiding efforts for [model refinement](@entry_id:163834) and robust design.