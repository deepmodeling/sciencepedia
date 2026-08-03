## Introduction
How do we determine the composition of an atmosphere hundreds of light-years away? How can we measure the temperature profile of our own planet's air from space? The answer to these profound questions lies in the sophisticated science of [atmospheric retrieval](@entry_id:1121206). This field provides the tools to translate the light we observe from a planet—whether it's the starlight filtered through an exoplanet's limb or the thermal glow of Earth—into a detailed understanding of its physical and chemical properties. However, this translation is a complex inverse problem, fraught with ambiguity and statistical challenges. This article provides a graduate-level introduction to the core concepts that form the bedrock of modern [atmospheric retrieval](@entry_id:1121206).

The following chapters will guide you from first principles to advanced applications. In **Principles and Mechanisms**, we will deconstruct the problem, starting with the physics of the forward model—how an atmosphere generates a spectrum—before establishing Bayesian inference as the primary framework for solving the inverse problem. Next, in **Applications and Interdisciplinary Connections**, we will see these principles in action, exploring how they are used to characterize distant exoplanets, monitor Earth's climate system, and navigate the complexities of real-world data. Finally, the **Hands-On Practices** section will offer an opportunity to engage directly with some of the practical and computational challenges inherent in the retrieval process. By the end, you will have a comprehensive conceptual toolkit for understanding and critically evaluating [atmospheric retrieval](@entry_id:1121206) studies across planetary science and astrophysics.

## Principles and Mechanisms

### The Physical Forward Model: From Atmosphere to Spectrum

Atmospheric retrieval is fundamentally an inverse problem: we seek to infer the physical and chemical properties of an atmosphere from the light we observe. To do this, we must first master the [forward problem](@entry_id:749531): predicting the spectrum that a given atmosphere would produce. This predictive model, known as the **forward model**, is rooted in the principles of radiative transfer.

#### The Radiative Transfer Equation

The journey of light through a planetary atmosphere is described by the **Radiative Transfer Equation (RTE)**. In its common plane-[parallel form](@entry_id:271259), which approximates a curved atmosphere as a series of flat layers, the RTE describes the change in specific intensity $I_{\lambda}$ (the energy per unit time, area, frequency, and [solid angle](@entry_id:154756)) with respect to optical depth $\tau_{\lambda}$ along a direction specified by the cosine of the zenith angle, $\mu = \cos\theta$:

$$
\mu \frac{dI_{\lambda}}{d\tau_{\lambda}} = I_{\lambda} - S_{\lambda}
$$

Here, the **[optical depth](@entry_id:159017)** $\tau_{\lambda}$ is a dimensionless measure of opacity, defined such that $\tau_{\lambda} = 0$ is at the top of the atmosphere (space-facing) and increases downwards. The term $I_{\lambda}$ represents the attenuation of light due to absorption and scattering out of the line of sight. The **[source function](@entry_id:161358)**, $S_{\lambda}$, represents light added into the line of sight, either through thermal emission from the gas itself or by light scattered from other directions.

Under the common assumption of Local Thermodynamic Equilibrium (LTE), the thermal emission is described by the Planck function, $B_{\lambda}(T)$. The scattering is characterized by the **single-scattering albedo**, $\omega$, which is the fraction of extinction due to scattering ($0 \le \omega \le 1$). The [source function](@entry_id:161358) can thus be written as:

$$
S_{\lambda} = (1-\omega) B_{\lambda}(T) + \omega J_{\lambda}
$$

where $J_{\lambda}$ is the mean intensity, an integral of $I_{\lambda}$ over all solid angles, representing the contribution from scattered light.

To illustrate, consider a simplified exoplanet atmosphere observed in emission, modeled as a plane-parallel, isothermal slab at temperature $T$. This atmosphere is illuminated from above by its star, providing a collimated beam of intensity $I_{0,\lambda}$ at an angle $\mu_0$. If we consider only thermal emission and first-order scattering of the stellar light (isotropic scattering), the emergent intensity at the top of the atmosphere ($\tau_{\lambda}=0$) in the observer's direction $\mu$ can be found by solving the RTE . The total intensity is the sum of two distinct components:

1.  **Thermal Emission**: This is the planet's own glow, attenuated by the overlying atmosphere. For a total optical depth of $\tau_{t}$, the thermal contribution is $I_{\text{thermal}} = (1-\omega) B_{\lambda}(T) (1 - \exp(-\tau_{t}/\mu))$.
2.  **Scattered Stellar Light**: This is starlight that is scattered once into the observer's line of sight. Its contribution is $I_{\text{scattered}} = \frac{\omega I_{0,\lambda} \mu_{0}}{4\pi(\mu + \mu_{0})} (1 - \exp(-\tau_{t}(\frac{1}{\mu} + \frac{1}{\mu_{0}})))$.

The total emergent intensity is the sum of these two terms, $I_{\lambda}(0,\mu) = I_{\text{thermal}} + I_{\text{scattered}}$. This example demonstrates how the observed spectrum is a composite of physical processes—thermal structure, absorption, and scattering—each encoded in the light we receive.

#### Transmission Spectroscopy: A Geometric View

While [emission spectroscopy](@entry_id:186353) probes the thermal structure of an atmosphere, **[transmission spectroscopy](@entry_id:1133375)** probes its composition and scale by measuring starlight filtered through the planet's limb during a transit. The fundamental quantity we derive is the wavelength-dependent transit depth, which translates to an effective transit radius, $R(\lambda)$.

The size of this radius is determined by the altitude at which the atmosphere becomes opaque to a ray of starlight grazing the planet. This opacity is a function of the gas density and the absorption [cross-sections](@entry_id:168295) of its constituent molecules. To model this, we begin with the principle of **[hydrostatic equilibrium](@entry_id:146746)**, which balances the pressure [gradient force](@entry_id:166847) with gravity:

$$
\frac{dP}{dz} = -\rho g
$$

where $P$ is pressure, $z$ is altitude, $\rho$ is density, and $g$ is the [acceleration due to gravity](@entry_id:173411). Combining this with the Ideal Gas Law, $P = \frac{\rho k_B T}{\bar{m}}$, where $k_B$ is the Boltzmann constant, $T$ is temperature, and $\bar{m}$ is the mean [molecular mass](@entry_id:152926), we arrive at an expression for the pressure profile. For an [isothermal atmosphere](@entry_id:203207), this integrates to $P(z) = P_0 \exp(-z/H)$, where the **[atmospheric scale height](@entry_id:203508)**, $H$, is defined as:

$$
H = \frac{k_B T}{\bar{m} g}
$$

The scale height represents the characteristic distance over which the atmospheric pressure or density decreases by a factor of $e$, and it is a crucial parameter in [atmospheric retrieval](@entry_id:1121206).

The monochromatic optical depth along a slant path through the limb, with tangent radius ([impact parameter](@entry_id:165532)) $r_t$, is given by the Beer-Lambert law integrated along the line of sight, $s$:

$$
\tau_{\lambda}(r_t) = \int_{-\infty}^{\infty} n(r(s)) \sigma_{\lambda} ds
$$

where $n(r(s))$ is the [number density](@entry_id:268986) of the absorbing gas at radius $r(s) = \sqrt{r_t^2 + s^2}$ and $\sigma_{\lambda}$ is the molecular absorption cross-section. Under the local approximation of an [isothermal atmosphere](@entry_id:203207) with constant gravity, the number [density profile](@entry_id:194142) is $n(r) = n_t \exp(-(r-r_t)/H)$, where $n_t$ is the density at the tangent point. The exact evaluation of this integral yields a [closed-form solution](@entry_id:270799) involving a special function :

$$
\tau_{\lambda}(r_t) = 2 \sigma_{\lambda} n_t r_t \exp\left(\frac{r_t}{H}\right) K_1\left(\frac{r_t}{H}\right)
$$

where $K_1$ is the modified Bessel function of the second kind of order one. While this [exact form](@entry_id:273346) is important for high-fidelity models, a powerful intuition can be gained from a simpler approximation. The transit radius $R(\lambda)$ is the altitude where $\tau_{\lambda}$ is approximately constant (of order unity). This leads to a widely used approximate relationship for the transit radius:

$$
R(\lambda) \approx R_0 + H \ln(\kappa_{\lambda} \chi) + C
$$

Here, $R_0$ is a reference radius (e.g., at the cloud-top deck), $\kappa_{\lambda}$ is the wavelength-dependent opacity, $\chi$ is the absorber's [mixing ratio](@entry_id:1127970), and $C$ is a constant containing other parameters. This equation reveals that the amplitude of spectral features in a transmission spectrum is primarily proportional to the scale height $H$. A "puffier" atmosphere (larger $H$) will produce more prominent absorption features.

### The Inverse Problem: Core Principles of Atmospheric Retrieval

With a forward model $\mathbf{F}$ that predicts a spectrum $\mathbf{y}$ from a set of atmospheric parameters $\mathbf{x}$, i.e., $\mathbf{y} = \mathbf{F}(\mathbf{x})$, retrieval is the process of inverting this relationship to find the most plausible parameters $\mathbf{x}$ that explain an observed spectrum $\mathbf{y}_{\text{obs}}$.

#### Bayesian Inference as the Foundational Framework

The most rigorous framework for solving [inverse problems](@entry_id:143129) is **Bayesian inference**. Bayes' theorem provides a probabilistic rule for updating our knowledge about the parameters $\mathbf{x}$ in light of new data $\mathbf{y}$:

$$
P(\mathbf{x} | \mathbf{y}) = \frac{P(\mathbf{y} | \mathbf{x}) P(\mathbf{x})}{P(\mathbf{y})}
$$

Let's dissect this fundamental equation:

-   $P(\mathbf{x} | \mathbf{y})$ is the **[posterior probability](@entry_id:153467) distribution**, representing our updated state of knowledge about the parameters $\mathbf{x}$ after observing the data $\mathbf{y}$. This is the primary output of a retrieval.
-   $P(\mathbf{y} | \mathbf{x})$ is the **likelihood**, which quantifies the probability of observing the data $\mathbf{y}$ if the true parameters were $\mathbf{x}$. It is where the forward model and a statistical model of the measurement noise come together. Assuming independent Gaussian measurement errors with covariance $\mathbf{S}_{\epsilon}$, the likelihood is given by:
    $$
    P(\mathbf{y} | \mathbf{x}) \propto \exp\left(-\frac{1}{2} (\mathbf{y} - \mathbf{F}(\mathbf{x}))^{\mathsf{T}} \mathbf{S}_{\epsilon}^{-1} (\mathbf{y} - \mathbf{F}(\mathbf{x}))\right)
    $$
-   $P(\mathbf{x})$ is the **[prior probability](@entry_id:275634) distribution**, which encodes our knowledge about the parameters *before* considering the new data. This can come from physical constraints, theoretical models (e.g., [thermochemistry](@entry_id:137688)), or previous observations.
-   $P(\mathbf{y})$ is the **Bayesian evidence** or marginal likelihood. It acts as a [normalization constant](@entry_id:190182), ensuring the posterior integrates to one. While often ignored for [parameter estimation](@entry_id:139349), it is crucial for [model comparison](@entry_id:266577), as we will see later.

The full posterior distribution $P(\mathbf{x} | \mathbf{y})$ is the most complete description of the retrieval result, but it is often convenient to summarize it with a single [point estimate](@entry_id:176325).

#### Estimation Methods: Maximizing the Posterior

A common summary of the posterior is the **Maximum A Posteriori (MAP)** estimate, $\mathbf{x}_{\text{MAP}}$, which is the parameter vector that maximizes the [posterior probability](@entry_id:153467). Maximizing $P(\mathbf{x} | \mathbf{y})$ is equivalent to minimizing its negative logarithm. For a Gaussian likelihood and Gaussian prior, this leads to minimizing a cost function $J(\mathbf{x})$:

$$
J(\mathbf{x}) = (\mathbf{y} - \mathbf{F}(\mathbf{x}))^{\mathsf{T}} \mathbf{S}_{\epsilon}^{-1} (\mathbf{y} - \mathbf{F}(\mathbf{x})) + (\mathbf{x} - \mathbf{x}_a)^{\mathsf{T}} \mathbf{S}_a^{-1} (\mathbf{x} - \mathbf{x}_a)
$$

where $\mathbf{x}_a$ and $\mathbf{S}_a$ are the mean and covariance of the Gaussian prior, respectively. The first term is the familiar chi-squared ($\chi^2$) misfit to the data, while the second term penalizes solutions that deviate from the prior.

For many problems, the forward model can be approximated as linear around a [reference state](@entry_id:151465), $\mathbf{F}(\mathbf{x}) \approx \mathbf{y}_a + \mathbf{K}(\mathbf{x} - \mathbf{x}_a)$, where $\mathbf{K}$ is the Jacobian matrix of [partial derivatives](@entry_id:146280) $\frac{\partial \mathbf{F}}{\partial \mathbf{x}}$. In this linear-Gaussian case, the posterior is also a Gaussian, and the MAP estimate has a closed-form analytical solution.

As a simple example, consider retrieving a single parameter, $u = \log_{10}(q_X)$ (the log [mixing ratio](@entry_id:1127970) of a gas), from a set of four spectral measurements $r_i$ where the forward model is linear: $r_i = a_i u + b_i$. With Gaussian measurement errors and a Gaussian prior for $u$, $u \sim \mathcal{N}(\mu_0, s_0^2)$, the MAP estimate is a precision-weighted average of the information from the data and the prior :

$$
\hat{u}_{\text{MAP}} = \frac{\sum_{i=1}^{4} \frac{a_i(r_i - b_i)}{\sigma_i^2} + \frac{\mu_0}{s_0^2}}{\sum_{i=1}^{4} \frac{a_i^2}{\sigma_i^2} + \frac{1}{s_0^2}}
$$

Generalizing to the multivariate case, the MAP solution for the linear model $\mathbf{y} = \mathbf{Kx} + \boldsymbol{\epsilon}$ is found by solving the linear system that results from setting the gradient of $J(\mathbf{x})$ to zero, yielding the solution known as the **Optimal Estimation** or **Gauss-Markov** estimator :

$$
\mathbf{x}_{\text{MAP}} = (\mathbf{K}^{\mathsf{T}} \mathbf{S}_{\epsilon}^{-1} \mathbf{K} + \mathbf{S}_a^{-1})^{-1} (\mathbf{K}^{\mathsf{T}} \mathbf{S}_{\epsilon}^{-1} \mathbf{y} + \mathbf{S}_a^{-1} \mathbf{x}_a)
$$

This equation lies at the heart of many modern retrieval codes. The matrix $(\mathbf{K}^{\mathsf{T}} \mathbf{S}_{\epsilon}^{-1} \mathbf{K} + \mathbf{S}_a^{-1})$ is the inverse of the [posterior covariance matrix](@entry_id:753631), $\mathbf{S}_{\text{post}}$.

### Challenges and Diagnostics in Retrieval

The solution to an inverse problem is rarely unique or perfectly constrained. Understanding the limitations, degeneracies, and actual information gain of a retrieval is as important as finding the best-fit parameters.

#### Parameter Degeneracy and Correlation

A **degeneracy** occurs when different combinations of physical parameters produce nearly identical observable spectra. This leads to strong correlations in the posterior distribution, meaning that the uncertainty in one parameter is linked to the uncertainty in another.

A classic example in transmission spectroscopy is the degeneracy between the reference radius $R_0$ and the volume [mixing ratio](@entry_id:1127970) $\chi$ of an absorbing gas . In the simplified model $R(\lambda) \approx R_0 + H \ln(\chi) + H\ln(\kappa_\lambda)$, the absolute vertical level of the spectrum depends on the combination $R_0 + H\ln(\chi)$. An increase in the assumed cloud-top radius $R_0$ can be almost perfectly compensated by a corresponding decrease in the [mixing ratio](@entry_id:1127970) $\chi$ to produce the same spectrum. This results in a strong negative correlation between $R_0$ and $\ln(\chi)$ in the retrieved posterior, making it difficult to constrain either parameter independently without strong [prior information](@entry_id:753750) or data spanning a very wide wavelength range.

Correlations can also be induced by the underlying physics. Consider the scale height, $H = k_B T / (\bar{m} g)$. A measurement of $H$ constrains the combination of $T$, $\bar{m}$, and $g$. If these parameters are uncertain, they will become correlated in the posterior. For instance, gravity itself is not a fundamental parameter but is derived from mass $M$ and radius $R$ via $g = GM/R^2$. Priors on $M$ and $R$ induce a prior on $g$. A measurement of $H$ introduces the constraint $\ln g \approx \ln(k_B T / \bar{m}) - \ln H$. Because $\ln g$ and $\ln \bar{m}$ appear with the same sign in this constraint, a precise measurement of $H$ will induce a strong negative correlation between them in the posterior distribution . A higher gravity can be mimicked by a higher mean molecular weight, and the data may not be able to tell the difference.

#### Information Content and Identifiability

Given these degeneracies, a critical question is: how much information about the atmosphere did the measurement actually provide? Several diagnostic tools help answer this.

The **Averaging Kernel Matrix**, $\mathbf{A}$, provides a powerful linear-algebraic perspective. For a linear retrieval, it relates the expected value of the retrieved state, $\langle \mathbf{x}_{\text{retrieved}} \rangle$, to the true state, $\mathbf{x}_{\text{true}}$:

$$
\langle \mathbf{x}_{\text{retrieved}} \rangle = \mathbf{A} \mathbf{x}_{\text{true}} + (\mathbf{I}-\mathbf{A})\mathbf{x}_a
$$

The [averaging kernel](@entry_id:746606) is given by $\mathbf{A} = (\mathbf{K}^{\mathsf{T}} \mathbf{S}_{\epsilon}^{-1} \mathbf{K} + \mathbf{S}_a^{-1})^{-1} \mathbf{K}^{\mathsf{T}} \mathbf{S}_{\epsilon}^{-1} \mathbf{K}$ . An ideal retrieval would have $\mathbf{A}=\mathbf{I}$, the identity matrix, meaning the retrieved state perfectly matches the true state. In reality, the rows of $\mathbf{A}$ are peaked functions, indicating that the retrieved value for a parameter is a weighted average of the true values of several parameters. The width of these peaks indicates the resolution of the retrieval.

The trace of the [averaging kernel](@entry_id:746606), $\text{Tr}(\mathbf{A})$, is called the **[degrees of freedom for signal](@entry_id:748284)** ($d_s$). It represents the effective number of independent parameters that are constrained by the measurement, rather than by the prior. Using a Singular Value Decomposition (SVD) of a "pre-whitened" Jacobian, $K' = S_e^{-1/2} K S_a^{1/2}$, with singular values $\lambda_i$, the degrees of freedom can be expressed elegantly :

$$
d_s = \sum_i \frac{\lambda_i^2}{\lambda_i^2 + 1}
$$

Each term represents the information gained for one "mode" of the parameter space, ranging from 0 (no information, prior-dominated) to 1 (perfectly constrained by data). For a [well-posed problem](@entry_id:268832) with two parameters and good data, one might find $d_s \approx 1.956$, indicating that the measurement successfully constrains nearly two independent pieces of information.

An alternative, information-theoretic perspective is to quantify the **Shannon [information content](@entry_id:272315)** of the measurement. This is defined as the reduction in [differential entropy](@entry_id:264893) from the prior distribution to the posterior distribution, measured in "nats" (if using natural logarithm) or bits. For a multivariate Gaussian system, the information gain $I_g$ is :

$$
I_g = h(\text{prior}) - h(\text{posterior}) = \frac{1}{2} \ln\left(\frac{\det(\mathbf{S}_a)}{\det(\mathbf{S}_{\text{post}})}\right)
$$

This metric provides a single scalar value that quantifies how much the measurement reduced the volume of uncertainty in the parameter space.

Finally, for forecasting the potential of future instruments, the **Fisher Information Matrix (FIM)** is often used. For a linear-Gaussian model, the FIM is $\mathbf{F} = \mathbf{K}^{\mathsf{T}} \mathbf{S}_{\epsilon}^{-1} \mathbf{K}$. Its inverse, $\mathbf{F}^{-1}$, provides the Cramér-Rao lower bound on the covariance of an [unbiased estimator](@entry_id:166722). The information on a parameter like [scale height](@entry_id:263754) $H$ scales with the spread of opacity values sampled by the instrument , emphasizing the need for broad wavelength coverage to achieve high precision.

### Advanced Topics and Practical Considerations

Real-world retrievals involve additional layers of complexity, from ill-posedness and instrument [systematics](@entry_id:147126) to the fundamental choice of the model itself.

#### Regularization: The Role of the Prior

In many realistic scenarios, particularly when retrieving atmospheric profiles (e.g., temperature vs. pressure), the problem is ill-posed or underdetermined. There are more parameters to solve for than independent data points. In such cases, the retrieval is only possible with the inclusion of a prior, which acts to **regularize** the solution by imposing constraints. The MAP cost function naturally incorporates this.

The choice of [prior covariance](@entry_id:1130174) matrix, $\mathbf{S}_a$, defines the type of regularization :

1.  **Diagonal Prior (Tikhonov Regularization)**: If $\mathbf{S}_a^{-1}$ is a [diagonal matrix](@entry_id:637782), the prior term becomes $\sum_i \gamma_i (x_i - x_{a,i})^2$. This independently penalizes each parameter for deviating from its prior mean $x_{a,i}$. If the prior is very strong (large $\gamma_i$), the solution will be heavily biased toward the prior mean, potentially washing out information from the data.
2.  **Smoothness Prior**: To retrieve a profile that is expected to be physically smooth, we can penalize "roughness" instead of deviation from a fixed profile. This is done by constructing $\mathbf{S}_a^{-1} = \lambda \mathbf{L}^{\mathsf{T}}\mathbf{L}$, where $\mathbf{L}$ is a [finite difference](@entry_id:142363) operator (e.g., $(Lx)_i = x_{i+1} - x_i$). The prior term becomes $\lambda \sum_i (x_{i+1} - x_i)^2$, which enforces similarity between adjacent layers of the atmosphere. The strength of this smoothness constraint is controlled by the hyperparameter $\lambda$.

#### Modeling Instrument Systematics and Correlated Noise

Raw data from telescopes is never perfect. It contains instrumental artifacts, or **[systematics](@entry_id:147126)**, which can mimic or mask astrophysical signals. A robust retrieval must model and marginalize these [systematics](@entry_id:147126). Often, these are known to correlate with observable instrument parameters like detector temperature or spacecraft position. A common approach is to include them as a linear component in the forward model :

$$
\mathbf{y} = \theta\mathbf{s} + \mathbf{Bw} + \boldsymbol{\epsilon}
$$

Here, $\theta\mathbf{s}$ is the astrophysical signal, and $\mathbf{Bw}$ is the [systematics](@entry_id:147126) model, where $\mathbf{B}$ is a design matrix of [systematics](@entry_id:147126) basis vectors and $\mathbf{w}$ are their unknown coefficients. The [nuisance parameters](@entry_id:171802) $\mathbf{w}$ are estimated jointly with the science parameter $\theta$.

Furthermore, measurement noise is not always independent. Noise can be correlated in time or across wavelength channels. A simple but effective model for [time-series data](@entry_id:262935) is a combination of independent white noise ($\sigma^2$) and a common-mode "breathing" noise ($\rho^2$) that affects all data points together. The [noise covariance](@entry_id:1128754) matrix becomes $\mathbf{C} = \sigma^2 \mathbf{I} + \rho^2 \mathbf{1}\mathbf{1}^{\mathsf{T}}$, where $\mathbf{1}$ is a vector of ones. When the [noise covariance](@entry_id:1128754) $\mathbf{C}$ is not diagonal, the standard [least-squares method](@entry_id:149056) is insufficient, and one must use **Generalized Least Squares (GLS)**, which properly weights the data using the [inverse covariance matrix](@entry_id:138450) $\mathbf{C}^{-1}$.

#### Bayesian Model Selection

Perhaps the most fundamental question in retrieval is: "Which model should I be using?" Should we include another gas in our model? Is a complex temperature profile justified? Is the [systematics](@entry_id:147126) model necessary? This is the domain of **Bayesian model selection**.

The key quantity for comparing two models, $\mathcal{M}_0$ and $\mathcal{M}_1$, is the **Bayesian evidence**, $Z = P(\mathbf{y} | \mathcal{M})$. The evidence is the integral of the likelihood over the entire prior parameter space:

$$
Z = \int P(\mathbf{y} | \mathbf{x}, \mathcal{M}) P(\mathbf{x} | \mathcal{M}) d\mathbf{x}
$$

The evidence represents the average likelihood of the model, weighted by the prior. It automatically embodies **Occam's razor**: a more complex model (with a larger prior volume) will be penalized unless it provides a significantly better fit to the data. For a linear-Gaussian model, the evidence has an elegant analytical form : it is simply the probability of the data under a Gaussian distribution with zero mean and a total covariance of $\boldsymbol{\Sigma}_{\text{data}} = \mathbf{K} \mathbf{S}_a \mathbf{K}^{\mathsf{T}} + \mathbf{S}_{\epsilon}$.

The ratio of evidences for two models is the **Bayes factor**, $K = Z_1 / Z_0$. A large Bayes factor ($K \gg 1$) provides strong support for model $\mathcal{M}_1$ over $\mathcal{M}_0$.

Calculating the evidence integral can be computationally prohibitive for non-[linear models](@entry_id:178302). A common, cheaper alternative is an [information criterion](@entry_id:636495) like the **Bayesian Information Criterion (BIC)** :

$$
\text{BIC} = k \ln N - 2\ln \mathcal{L}_{\text{max}}
$$

where $k$ is the number of free parameters, $N$ is the number of data points, and $\mathcal{L}_{\text{max}}$ is the maximum likelihood value. The model with the lower BIC is preferred. While an approximation, the BIC provides a valuable and computationally tractable tool for balancing [model complexity](@entry_id:145563) against goodness-of-fit in the practical world of [atmospheric retrieval](@entry_id:1121206).