## Introduction
Computational models are indispensable tools in modern [combustion science](@entry_id:187056), enabling the design of cleaner, more efficient engines and the assessment of complex safety scenarios. However, a single, [deterministic simulation](@entry_id:261189) provides an incomplete picture. To make reliable, high-consequence decisions, we must not only predict an outcome but also quantify the confidence in that prediction. This is the domain of Uncertainty Quantification (UQ), a rigorous discipline that transforms computational models from deterministic calculators into powerful tools for predictive science.

This article addresses the critical gap between producing a simulation and establishing its credibility. It provides a systematic guide to understanding, characterizing, and propagating uncertainties inherent in complex combustion models. You will learn how to move beyond single-[point estimates](@entry_id:753543) to probabilistic forecasts that support robust design and informed decision-making.

The journey begins in the **Principles and Mechanisms** chapter, which lays the groundwork by defining the core tenets of Verification, Validation, and Uncertainty Quantification (V&V/UQ) and introducing the mathematical machinery used to model and propagate uncertainty. Next, the **Applications and Interdisciplinary Connections** chapter demonstrates how these methods are applied to solve practical problems, from analyzing turbulent flames and detonations to performing [quantitative risk assessment](@entry_id:198447) in engineering systems. Finally, the **Hands-On Practices** section offers a chance to apply these concepts through guided exercises, solidifying your understanding of how to analyze and quantify uncertainty in real-world combustion phenomena.

## Principles and Mechanisms

The development and application of predictive [computational combustion](@entry_id:1122776) models require a rigorous framework for assessing their credibility. This chapter delineates the core principles and mechanisms that constitute modern Uncertainty Quantification (UQ). We move from foundational definitions that distinguish between code correctness, model fidelity, and quantified confidence, to a systematic classification of uncertainties. Subsequently, we explore the mathematical machinery used to represent, propagate, and analyze these uncertainties, with a particular focus on the challenges inherent to the complex, high-dimensional models used in combustion science.

### The Foundation: Verification, Validation, and Uncertainty Quantification

To establish the credibility of a computational simulation, we must address three distinct but complementary activities: **Verification**, **Validation**, and **Uncertainty Quantification (V/UQ)**. A clear understanding of their respective roles is paramount. Consider a Large Eddy Simulation (LES) of a turbulent premixed flame, where we aim to predict quantities of interest (QoIs) like the [laminar flame speed](@entry_id:202145), $S_L$, or NOx emissions, $J_{\mathrm{NO_x}}$. The total deviation between a numerical prediction and physical reality can be formally decomposed .

Let $Q_{\mathrm{phys}}$ be the true physical quantity, measured in a well-[controlled experiment](@entry_id:144738). Let the mathematical model, comprising the governing partial differential equations (e.g., Navier-Stokes) and associated [closures](@entry_id:747387) (e.g., chemical kinetics, transport models), be defined by a set of input parameters $\boldsymbol{\theta}$. The exact, continuous solution to this model is denoted $Q_{\mathrm{model}}(\boldsymbol{\theta})$. The numerical simulation, however, yields an approximate solution, $\hat{Q}(h, \boldsymbol{\theta})$, on a computational grid with characteristic size $h$. The total deviation is thus:

$$
\hat{Q}(h, \boldsymbol{\theta}) - Q_{\mathrm{phys}} = \underbrace{\left(\hat{Q}(h, \boldsymbol{\theta}) - Q_{\mathrm{model}}(\boldsymbol{\theta})\right)}_{\text{Numerical Error}} + \underbrace{\left(Q_{\mathrm{model}}(\boldsymbol{\theta}) - Q_{\mathrm{phys}}\right)}_{\text{Model Discrepancy}}
$$

This decomposition provides the basis for defining V/UQ:

- **Verification** is the process of assessing the **numerical error**. The central question it answers is: "Are we solving the equations correctly?" Verification activities focus on ensuring the computational code faithfully implements the mathematical model and that the numerical solution is sufficiently accurate. **Code verification** often employs techniques like the Method of Manufactured Solutions (MMS) to check for programming errors. **Solution verification** estimates the numerical error in a specific simulation, typically through systematic refinement studies (e.g., [grid refinement](@entry_id:750066)) to demonstrate convergence of $\hat{Q}(h, \boldsymbol{\theta})$ toward $Q_{\mathrm{model}}(\boldsymbol{\theta})$ as $h \to 0$. A verified code is the non-negotiable foundation of any credible simulation.

- **Validation** is the process of assessing the **[model discrepancy](@entry_id:198101)**. Its central question is: "Are we solving the correct equations?" Validation activities evaluate the degree to which the mathematical model, $Q_{\mathrm{model}}(\boldsymbol{\theta})$, is an accurate representation of the physical reality, $Q_{\mathrm{phys}}$. This is achieved by comparing numerically converged predictions against high-quality experimental data. A scientifically rigorous validation requires that the numerical error is negligible compared to the expected model discrepancy and that all sources of uncertainty—in both the simulation inputs $\boldsymbol{\theta}$ and the experimental measurements—are quantified.

- **Uncertainty Quantification (UQ)** is the end-to-end process of characterizing all known sources of uncertainty and propagating their effects through the model to the final prediction. UQ provides a probabilistic description of the QoI, such as a probability density function (PDF) or a confidence interval, rather than a single deterministic value. This quantifies the confidence in the prediction and is essential for making informed decisions under uncertainty. UQ is inextricably linked with validation; a meaningful comparison between a model and data is only possible when the uncertainties in both are accounted for.

In summary, credibility is not achieved by any single activity. It requires verified numerics to ensure errors are not of our own making, validated models to establish a connection to physical reality, and a full UQ analysis to express the limits of our predictive confidence .

### A Taxonomy of Uncertainty

To systematically manage uncertainty, we must first classify its various forms. Uncertainties are typically categorized along two axes: their fundamental nature (epistemic vs. aleatoric) and their location within the modeling process (parametric, structural, etc.) .

**Aleatoric vs. Epistemic Uncertainty**

This is the most fundamental distinction.
- **Aleatoric uncertainty** stems from inherent randomness or variability in a system or its environment. It is considered irreducible, as no amount of additional knowledge can eliminate the [stochasticity](@entry_id:202258). Examples in [combustion modeling](@entry_id:201851) include random turbulent fluctuations or stochastic variability in experimental boundary conditions, such as noisy measurements of inlet temperature $T_0$ or [equivalence ratio](@entry_id:1124617) $\phi$. This type of uncertainty is typically modeled by introducing random variables with specified probability distributions into the model.

- **Epistemic uncertainty** arises from a lack of knowledge. It is, in principle, reducible by collecting more data or developing better models. This is the dominant form of uncertainty in most physics-based models. It encompasses our ignorance about the correct values of model parameters or even the correct form of the model itself. For instance, uncertainty in an activation energy value is epistemic; so is the choice between a mixture-averaged and a more detailed multicomponent diffusion model in a flame simulation.

**Practical Categories of Modeling Uncertainty**

Within the realm of epistemic uncertainty, it is useful to identify more specific categories:

- **Parametric uncertainty** refers to uncertainty in the values of parameters that appear within a fixed model structure. In combustion models, this is a primary concern. The parameters of the Arrhenius law for reaction rates, $k(T) = A T^n \exp(-E_a / (RT))$, or the coefficients in transport property models are classic examples. This uncertainty arises because these parameters are estimated from finite, noisy experimental or theoretical data.

- **Structural uncertainty**, also known as [model-form uncertainty](@entry_id:752061), results from inadequacies in the mathematical model itself. It represents the choice of which physical phenomena to include and how to represent them. Examples in a laminar flame simulation include the choice of a specific detailed [chemical kinetic mechanism](@entry_id:1122345) from several published versions, the decision to neglect or include thermal diffusion (the Soret effect), or the selection of a particular radiation model. This uncertainty cannot be removed by simply tuning parameters within the existing model.

- **Numerical uncertainty** is the error introduced by the discretization and numerical solution of the governing mathematical equations. As discussed under Verification, sources include grid spacing $\Delta x$, time step $\Delta t$, and solver tolerances. This uncertainty can be controlled and estimated through convergence studies.

It is crucial to recognize that these categories are not always cleanly separable, but they provide an essential conceptual framework for diagnosing and quantifying the sources of predictive uncertainty .

### Characterizing and Modeling Input Uncertainties

A cornerstone of UQ is the development of probabilistic models for all uncertain inputs. This involves specifying [marginal probability](@entry_id:201078) distributions for each parameter and a dependence structure (correlation) among them.

#### Uncertainty in Chemical Kinetic Parameters

The Arrhenius expression, $k(T) = A T^n \exp(-E_a / (RT))$, is central to combustion modeling, and its parameters—the [pre-exponential factor](@entry_id:145277) $A$, temperature exponent $n$, and activation energy $E_a$—are significant sources of uncertainty.

A standard approach for assigning prior distributions to these parameters in a Bayesian context involves encoding physical knowledge . Since $A$ must be positive, a **[log-normal distribution](@entry_id:139089)** is a natural choice (equivalent to a [normal distribution](@entry_id:137477) for $\ln A$). Since activation energies $E_a$ must be non-negative and are often informed by quantum chemistry calculations with near-additive errors, a **truncated [normal distribution](@entry_id:137477)** over $E \ge 0$ is appropriate. The temperature exponent $n$ is often known to be small, which can be encoded with a **normal distribution** centered at or near zero.

A critical, and often overlooked, aspect of kinetic [parameter uncertainty](@entry_id:753163) is the strong [statistical correlation](@entry_id:200201) induced during the fitting process. Consider the linearized form, $\ln k(T) = \ln A + n \ln T - E_a/(RT)$. When fitting this model to experimental data of $\ln k$ versus $1/T$ over a finite temperature range, a [strong coupling](@entry_id:136791) emerges between the estimates of $\ln A$ and $E_a$. To maintain a good fit at a representative temperature, a statistical increase in the estimated $E_a$ must be compensated by an increase in the estimated $\ln A$. This results in a **strong positive correlation** between $\ln A$ and $E_a$ , . A faithful uncertainty model must capture this **Arrhenius compensation effect**, typically through a [multivariate normal distribution](@entry_id:267217) for $(\ln A, E_a, n)$ with a non-zero covariance term, or by using a copula to model the dependence.

For large mechanisms with many reactions, it is often beneficial to group reactions into classes (e.g., H-atom abstractions by OH). A **hierarchical prior** can then be used, where the parameters for each reaction in a class are assumed to be drawn from a shared, class-level distribution. This allows "borrowing of statistical strength" across reactions and helps prevent overfitting, especially for reactions with sparse data .

#### Uncertainty in Transport Properties

Similar principles apply to modeling uncertainties in transport properties like viscosity $\mu$, thermal conductivity $\kappa$, and binary diffusion coefficients $D_{AB}$. These properties are positive definite, making a log-space formulation natural. According to kinetic theory, these coefficients are all functions of the same underlying [intermolecular potential](@entry_id:146849) parameters (e.g., Lennard-Jones parameters $\sigma$ and $\epsilon$). Consequently, even if the fundamental parameters $\sigma$ and $\epsilon$ are considered independent, the transport coefficients $\mu$, $\kappa$, and $D_{AB}$ will be **correlated**. For instance, the near-constancy of the Prandtl number, $\mathrm{Pr} = \mu c_p / \kappa$, for monatomic gases implies a strong positive correlation between $\mu$ and $\kappa$. A robust UQ model must capture these physics-induced correlations, typically by constructing a joint probability distribution in log-space, e.g., a [multivariate normal distribution](@entry_id:267217) for $(\ln \mu, \ln \kappa, \ln D_{AB})$ .

#### The Role of Bayesian Inference

Bayesian inference provides a formal framework for updating our knowledge about uncertain parameters $\boldsymbol{\theta}$ in light of experimental data $y$. According to Bayes' theorem, the **posterior distribution** $p(\boldsymbol{\theta} | y)$ is proportional to the product of the **likelihood** $p(y | \boldsymbol{\theta})$ and the **prior distribution** $p(\boldsymbol{\theta})$:

$$
p(\boldsymbol{\theta} | y) \propto p(y | \boldsymbol{\theta}) p(\boldsymbol{\theta})
$$

Here, the prior $p(\boldsymbol{\theta})$ mathematically encodes our epistemic uncertainty about the parameters before seeing the data. The likelihood $p(y | \boldsymbol{\theta})$ connects the parameters to the data; it is the probability of observing the data $y$ for a given set of parameters $\boldsymbol{\theta}$. The form of the likelihood is determined by the statistical model for the measurement noise, which represents [aleatoric uncertainty](@entry_id:634772). For example, if we model the logarithm of an ignition delay measurement $y_i$ as the log of the model prediction $\tau(\boldsymbol{\theta}; \mathbf{x}_i)$ plus an independent Gaussian error term, $\log y_i = \log \tau(\boldsymbol{\theta}; \mathbf{x}_i) + \varepsilon_i$ with $\varepsilon_i \sim \mathcal{N}(0, \sigma^2)$, the likelihood for a set of independent measurements is the product of individual normal PDFs. The posterior then combines the prior knowledge with the information from the data to yield an updated state of knowledge about the parameters .

### Propagating and Analyzing Uncertainty

Once input uncertainties are characterized, the next step is to propagate them through the computational model to determine the resulting uncertainty in the QoI.

#### Local Sensitivity Analysis

The simplest method for analyzing parameter influence is **[local sensitivity analysis](@entry_id:163342)**. The local [sensitivity coefficient](@entry_id:273552) of a QoI $Q$ with respect to a parameter $\theta_i$ is defined as the partial derivative evaluated at a nominal parameter point $\boldsymbol{\theta}^\star$:

$$
S_i = \left. \frac{\partial Q}{\partial \theta_i} \right|_{\boldsymbol{\theta}^\star}
$$

This coefficient quantifies the first-order change in $Q$ for a small perturbation in $\theta_i$. Its sign indicates whether the parameter is promoting ($S_i > 0$) or inhibiting ($S_i  0$) the QoI, while its magnitude indicates the strength of the influence. For a flame-promoting reaction, increasing the [pre-exponential factor](@entry_id:145277) $A$ increases the reaction rate, leading to a higher flame speed ($S_A > 0$). Conversely, increasing the activation energy $E_a$ slows the reaction, reducing the flame speed ($S_{E_a}  0$) . These coefficients are the building blocks for first-order error propagation and provide invaluable physical insight into a model's behavior.

#### Polynomial Chaos Expansions

For propagating the full distribution of uncertainty, particularly for nonlinear models, more advanced techniques are needed. **Polynomial Chaos Expansion (PCE)** is a powerful non-intrusive method. It represents the model output $Q$ as a spectral expansion in terms of polynomials that are orthogonal with respect to the probability measure of the uncertain inputs $\boldsymbol{\xi}$. For an input vector $\boldsymbol{\xi}$ of independent standard random variables, the expansion takes the form:

$$
Q(\boldsymbol{\xi}) \approx \sum_{k=0}^{P} a_k \Psi_k(\boldsymbol{\xi})
$$

Here, $\{a_k\}$ are the deterministic PCE coefficients and $\{\Psi_k\}$ are the [orthogonal basis](@entry_id:264024) polynomials. The crucial property of **orthogonality** is defined with respect to the inner product weighted by the input PDF, $\langle \Psi_i, \Psi_j \rangle = \mathbb{E}[\Psi_i(\boldsymbol{\xi}) \Psi_j(\boldsymbol{\xi})] = 0$ for $i \neq j$ . The specific choice of polynomial family depends on the input distribution (e.g., Hermite polynomials for Gaussian inputs, Legendre polynomials for uniform inputs), a system known as the Wiener-Askey scheme.

Once the coefficients $a_k$ are computed (e.g., via [spectral projection](@entry_id:265201)), the PCE acts as a computationally inexpensive surrogate model. A key advantage is that the statistical moments of the output can be calculated analytically from the coefficients. If the basis is orthonormal and $\Psi_0=1$, the mean and variance are simply:

$$
\mathbb{E}[Q] = a_0, \quad \mathrm{Var}[Q] = \sum_{k=1}^{P} a_k^2
$$

This avoids the need for expensive Monte Carlo sampling of the original high-fidelity model to estimate output statistics .

### Advanced Topics in Model Credibility

As UQ matures, the focus shifts to more subtle but critically important aspects of model credibility.

#### Model Discrepancy and Structural Uncertainty

As introduced earlier, the model discrepancy term, $\delta(\phi)$, represents the systematic error of a model. In Bayesian calibration, ignoring this term and assuming that all mismatch between model and data is measurement noise (i.e., using a likelihood $d_i = S_M(\phi_i, \boldsymbol{\theta}) + \epsilon_i$ when the truth is $d_i = S_M(\phi_i, \boldsymbol{\theta}^\star) + \delta(\phi_i) + \epsilon_i$) has severe consequences. The inference procedure will attempt to force the parameters $\boldsymbol{\theta}$ to absorb the systematic error $\delta(\phi)$, leading to **biased parameter posteriors**. Furthermore, because the model lacks a mechanism to account for this systematic error, its predictions will be **overconfident**, resulting in predictive intervals that are too narrow and exhibit poor coverage (e.g., a nominal 95% interval may contain the true value far less than 95% of the time). Explicitly modeling the discrepancy term $\delta(\phi)$, for example as a Gaussian Process, is therefore essential for obtaining calibrated predictions and preventing the "contamination" of physical parameter estimates with [model inadequacy](@entry_id:170436) .

#### Parameter Identifiability and "Sloppy" Models

In high-dimensional models like chemical kinetic mechanisms, a common and vexing challenge is **practical identifiability**. While a model may be **structurally identifiable** (i.e., its parameters are unique in a noise-free world), the finite amount and noise level of real data may make it impossible to precisely constrain all parameters. This phenomenon is often diagnosed using the **Fisher Information Matrix (FIM)**, which quantifies the amount of information the experimental data provides about the parameters.

Many complex models are found to be **"sloppy"**: the eigenvalues of their FIM span many orders of magnitude. This implies that the data provide strong constraints on a few combinations of parameters (the "stiff" directions, corresponding to large eigenvalues), but leave many other combinations very poorly constrained (the "sloppy" directions, corresponding to small eigenvalues). In a Bayesian context, this manifests as a highly anisotropic posterior distribution—extremely narrow in stiff directions and extremely wide in sloppy ones. It is not that individual parameters are unidentifiable, but rather that certain collective modes of variation are difficult to resolve.

This is not a fundamental roadblock but a challenge to be met with smarter inquiry. The solution lies in **[optimal experimental design](@entry_id:165340)**, which aims to devise new experiments that are maximally sensitive to the currently sloppy parameter directions. By targeting measurements that align with these poorly constrained modes, we can increase the smallest eigenvalues of the FIM, making it better-conditioned and systematically improving the practical identifiability of the model parameters .