## Introduction
For centuries, planets in our own solar system have been resolved into detailed worlds, but exoplanets remain largely as single points of light. Eclipse mapping is a powerful remote sensing technique that overcomes this limitation, allowing us to transform the time-variable light from a transiting exoplanet system into a two-dimensional map of the planet's atmospheric brightness. However, this transformation is not straightforward. The core challenge lies in solving a mathematically complex "inverse problem": how to uniquely reconstruct a 2D spatial map from a 1D time-series of integrated light. This article provides a comprehensive guide to the theory and practice of this cutting-edge method.

This article is structured to build your expertise from the ground up. The first chapter, **Principles and Mechanisms**, will dissect the forward model, explain why the inversion is so challenging, and introduce the essential mathematical tools—from regularization to Bayesian inference—that make it solvable. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how these recovered maps are used to probe fundamental [atmospheric physics](@entry_id:158010), such as wind patterns and thermal structure, and reveal the surprising connections between eclipse mapping and other [inverse problems](@entry_id:143129) across science. Finally, the **Hands-On Practices** chapter will offer a series of computational exercises to solidify your understanding of the key theoretical concepts. We begin by constructing the foundational forward model, which describes how a planet's brightness map generates the light curve we observe.

## Principles and Mechanisms

This chapter delineates the fundamental principles and mechanisms that underpin eclipse mapping. We will begin by constructing the forward model, which translates a planet's brightness distribution into an observable light curve. We then explore the inherent challenges of inverting this model, focusing on the concepts of [ill-posedness](@entry_id:635673) and fundamental ambiguities. Finally, we will detail the mathematical and statistical frameworks, including discretization, regularization, and Bayesian inference, that enable the reconstruction of planetary maps from photometric data.

### The Forward Model: From Planetary Brightness to Observed Flux

The primary observable in eclipse mapping is the time-variable flux received from an unresolved star-planet system. The total observed spectral flux, $F(t)$, is the sum of the constant [stellar flux](@entry_id:1132378), $F_{\star}$, and the time-varying planetary flux, $F_p(t)$. Our goal is to mathematically describe how $F_p(t)$ relates to the planet's intrinsic brightness distribution.

The flux received from a distant, unresolved source is found by integrating the [specific intensity](@entry_id:158830), $I$, over the [solid angle](@entry_id:154756), $\Omega$, that the source subtends on the sky. For a surface element on the planet with physical area $dA$, its contribution to the observed flux, $dF_p$, depends on its specific intensity $I$, its projected area as seen by the observer, and the distance to the observer, $D$. The projected area introduces a geometric factor, $\mu = \cos(\zeta)$, where $\zeta$ is the emission angle between the local surface normal, $\mathbf{n}$, and the line of sight to the observer, $\hat{\mathbf{k}}$. A surface element viewed face-on ($\mu=1$) contributes more flux than one viewed at a glancing angle near the limb ($\mu \approx 0$).

Combining these elements, the flux from a small patch of the planet's surface with area $dA = R_p^2 d\Omega$ (where $R_p$ is the planetary radius and $d\Omega$ is the solid angle element on the unit sphere) is given by:

$$dF_p(t) = I(\boldsymbol{\theta}, t) \cdot \mu(\boldsymbol{\theta}, t) \cdot \frac{dA}{D^2} = \frac{R_p^2}{D^2} I(\boldsymbol{\theta}, t) \mu(\boldsymbol{\theta}, t) d\Omega$$

where $\boldsymbol{\theta}$ represents the coordinates (e.g., latitude and longitude) on the planetary surface. The projection factor can be written as $\mu(\boldsymbol{\theta}, t) = \max\{0, \mathbf{n}(\boldsymbol{\theta}, t) \cdot \hat{\mathbf{k}}\}$, which naturally ensures that only the hemisphere facing the observer ($\mu > 0$) can contribute to the flux.

During a [secondary eclipse](@entry_id:1131356), the star acts as an occulting screen. We can define a binary **occultation mask**, $O(\boldsymbol{\theta}, t)$, which is equal to 1 if the surface element at $\boldsymbol{\theta}$ is visible to the observer at time $t$, and 0 if it is blocked by the star. The total observed planetary flux is then the integral of these contributions over the entire planetary surface, $\mathbb{S}^2$ :

$$F_p(t) = \frac{R_p^2}{D^2} \int_{\mathbb{S}^2} I(\boldsymbol{\theta}, t) \, \mu(\boldsymbol{\theta}, t) \, O(\boldsymbol{\theta}, t) \, d\Omega$$

This [integral equation](@entry_id:165305) is the cornerstone of the forward model. It is often convenient to consolidate all geometric and time-dependent factors into a single function, the **eclipse kernel**, $K(\boldsymbol{\theta}, t)$:

$$K(\boldsymbol{\theta}, t) = \frac{R_p^2}{D^2} \mu(\boldsymbol{\theta}, t) \, O(\boldsymbol{\theta}, t)$$

With this definition, the forward problem assumes the elegant form of a linear [integral transform](@entry_id:195422), where the kernel maps the spatial brightness distribution $I(\boldsymbol{\theta})$ to the time-domain observable $F_p(t)$ :

$$F_p(t) = \int_{\mathbb{S}^2} I(\boldsymbol{\theta}) \, K(\boldsymbol{\theta}, t) \, d\Omega$$

Here, we have assumed the map $I(\boldsymbol{\theta})$ is stationary over the duration of the eclipse. In some practical applications, it is useful to work in a projected 2D sky-plane coordinate system $(x,y)$. In this case, the forward model can be expressed as a 2D integral over the projected planetary disk, where the occulting stellar limb is modeled as a moving boundary .

### The Inverse Problem: Ill-Posedness and Fundamental Ambiguities

Eclipse mapping seeks to perform the reverse operation: given a series of measurements of the flux $F(t)$, we want to solve the [integral equation](@entry_id:165305) to find the brightness map $I(\boldsymbol{\theta})$. This is a classic **inverse problem**, and it is fundamentally **ill-posed**. An ill-posed problem has one or more of the following characteristics: a solution may not exist, it may not be unique, or it may not depend continuously on the data (i.e., small amounts of noise in the data can lead to arbitrarily large errors in the solution).

To gain intuition about the non-uniqueness of the solution, we can analyze a simplified model where the star's limb is a straight "knife-edge" sweeping across the planetary disk in the $x$-direction. The time derivative of the flux light curve, $\frac{dF}{dt}$, is directly proportional to the brightness integrated along a chord perpendicular to the direction of motion :

$$\frac{dF(t)}{dt} \propto \int_{-\sqrt{R_p^2-x^2}}^{\sqrt{R_p^2-x^2}} I(x,y) \, dy$$

This reveals a profound limitation: the measurement is only sensitive to the one-dimensional, chord-integrated brightness profile. Any changes to the 2D brightness map $I(x,y)$ that do not alter these chord integrals will be completely invisible to the observation. The set of all such "invisible" map components constitutes the **null space** of the forward operator. A prime example is any brightness perturbation that is an [odd function](@entry_id:175940) in the coordinate perpendicular to the scan direction (e.g., $\delta I(x,y) = -\delta I(x, -y)$). The integral of such a perturbation over any symmetric chord is zero, making it unrecoverable from a single eclipse sweep. This north-south ambiguity is a fundamental degeneracy in standard eclipse mapping.

Furthermore, real-world observations have finite exposure times. This time-averaging acts as a convolution, blurring the instantaneous light curve. The effect in the spatial domain is a blurring of the reconstructed map along the scan direction, with an effective width proportional to the scan speed multiplied by the exposure time, $v \Delta t$. This sets a fundamental limit on the achievable spatial resolution .

### Discretization and Basis Representations

To solve the inverse problem on a computer, the continuous function $I(\boldsymbol{\theta})$ must be represented by a [finite set](@entry_id:152247) of numbers. This process, called **discretization**, transforms the integral equation into a matrix equation:

$$\mathbf{y} = \mathbf{A}\mathbf{x} + \boldsymbol{\epsilon}$$

Here, $\mathbf{y}$ is the vector of flux measurements, $\mathbf{x}$ is a vector of coefficients representing the map, $\mathbf{A}$ is the design matrix (the discretized version of the kernel $K$), and $\boldsymbol{\epsilon}$ is the measurement noise. The choice of how to represent the map—the choice of **basis**—is a critical modeling decision that embeds prior assumptions about the map's structure.

Two common choices are the pixel basis and the spherical harmonic basis :

1.  **Pixel Basis:** The planet is divided into a grid of discrete pixels, and the vector $\mathbf{x}$ contains the brightness value for each pixel. This is a [local basis](@entry_id:151573), where each basis function is non-zero only over a small patch of the sphere. It is well-suited for representing maps with sharp, localized features like hotspots. A compact hotspot can be represented sparsely, with only a few non-zero elements in $\mathbf{x}$.

2.  **Spherical Harmonic Basis ($Y_{\ell m}$):** The map is expanded as a sum of spherical [harmonic functions](@entry_id:139660), and $\mathbf{x}$ contains the coefficients of this expansion. Spherical harmonics are global, smooth functions. This basis is natural for spherical bodies and is efficient for representing large-scale, smooth brightness variations. However, it is inefficient for representing sharp edges. A localized hotspot requires a superposition of many spherical harmonics up to high degrees ($\ell$), resulting in a non-[sparse representation](@entry_id:755123) and potential for "ringing" (Gibbs phenomenon) artifacts near discontinuities.

The sharp edge of the occulting star introduces a discontinuity in the eclipse kernel $K(t)$. This means the kernel is not "band-limited" in the spherical harmonic domain; its coefficients decay slowly with $\ell$. This property, known as spectral leakage, couples different spherical harmonic modes in the data and contributes to the [ill-conditioning](@entry_id:138674) of the design matrix $\mathbf{A}$.

### Solving the Inverse Problem: Regularization

Due to the ill-posed nature of the problem and the [ill-conditioning](@entry_id:138674) of the matrix $\mathbf{A}$, a naive [least-squares](@entry_id:173916) inversion will catastrophically amplify noise. To obtain a physically meaningful solution, we must introduce additional information to stabilize the inversion. This process is known as **regularization**.

A widely used method is **Tikhonov regularization**, which seeks a solution $\mathbf{x}$ that minimizes a composite objective function:

$$J(\mathbf{x}) = \|\mathbf{y} - \mathbf{A}\mathbf{x}\|_2^2 + \lambda \|\mathbf{L}\mathbf{x}\|_2^2$$

The first term, $\|\mathbf{y} - \mathbf{A}\mathbf{x}\|_2^2$, is the data fidelity term (chi-squared), which ensures the solution fits the measurements. The second term, $\|\mathbf{L}\mathbf{x}\|_2^2$, is the regularization penalty, which enforces a desired property on the solution, such as smoothness. The hyperparameter $\lambda$ controls the trade-off between fitting the data and satisfying the penalty. The solution to this minimization problem has a [closed form](@entry_id:271343) :

$$\hat{\mathbf{x}} = (\mathbf{A}^{\mathsf{T}} \mathbf{A} + \lambda \mathbf{L}^{\mathsf{T}} \mathbf{L})^{-1} \mathbf{A}^{\mathsf{T}} \mathbf{y}$$

The choice of the regularization operator $\mathbf{L}$ encodes our [prior belief](@entry_id:264565) about the map's structure. Common choices include:
*   $\mathbf{L} = \mathbf{I}$ (Zeroth-order Tikhonov or "[ridge regression](@entry_id:140984)"): Penalizes the total power or brightness of the map.
*   $\mathbf{L} \approx \nabla_{\mathbb{S}^2}$ (First-order): Penalizes the squared magnitude of the map's gradient, promoting smoothness.
*   $\mathbf{L} \approx \Delta_{\mathbb{S}^2}$ (Second-order): Penalizes the map's curvature.

While Tikhonov regularization is effective at suppressing noise, its use of an $\ell_2$-norm penalty tends to produce overly [smooth maps](@entry_id:203730), blurring sharp features. For planetary maps expected to contain sharp boundaries, such as the edge of a hotspot, an alternative is needed. **Total Variation (TV) regularization** penalizes the $\ell_1$-norm of the map's gradient:

$$J(\mathbf{x}) = \|\mathbf{y} - \mathbf{A}\mathbf{x}\|_2^2 + \lambda \|\nabla_{\mathbb{S}^2} \mathbf{x}\|_1$$

The $\ell_1$-norm promotes **sparsity** in the map's gradient. This means it favors solutions that are piecewise-constant, allowing for sharp jumps (large gradients) at region boundaries while strongly smoothing flat areas. This makes TV regularization particularly well-suited for recovering sharp-edged features from noisy, incomplete data .

### A Probabilistic Perspective: Bayesian Inference

The principles of regularization can be placed on a more formal statistical footing using the framework of **Bayesian inference**. This approach interprets the inversion problem as a quest for the [posterior probability](@entry_id:153467) distribution of the map parameters, $p(\mathbf{x}|\mathbf{y})$, given the data. According to Bayes' theorem:

$$p(\mathbf{x}|\mathbf{y}) \propto p(\mathbf{y}|\mathbf{x}) \, p(\mathbf{x})$$

The posterior probability is proportional to the product of the **likelihood**, $p(\mathbf{y}|\mathbf{x})$, and the **prior**, $p(\mathbf{x})$.

*   **The Likelihood:** The likelihood function quantifies the probability of observing the data $\mathbf{y}$ for a given map $\mathbf{x}$. Assuming the measurement noise $\boldsymbol{\epsilon}$ is Gaussian, the likelihood takes the form:
    $$p(\mathbf{y}|\mathbf{x}) \propto \exp \left( -\frac{1}{2} (\mathbf{y} - \mathbf{A}\mathbf{x})^{\mathsf{T}} \mathbf{C}_n^{-1} (\mathbf{y} - \mathbf{A}\mathbf{x}) \right)$$
    where $\mathbf{C}_n$ is the [noise covariance](@entry_id:1128754) matrix. A realistic noise model is crucial. It typically includes a diagonal "white noise" component (from Poisson [photon statistics](@entry_id:175965) and detector [read noise](@entry_id:900001)) and a non-diagonal "[correlated noise](@entry_id:137358)" component (from instrumental [systematics](@entry_id:147126), often modeled as a Gaussian Process) .

*   **The Prior:** The prior distribution, $p(\mathbf{x})$, encodes our beliefs about the map's properties before observing the data. Regularization is mathematically equivalent to adopting a specific prior. A Tikhonov penalty corresponds to a Gaussian prior on the quantity $\mathbf{L}\mathbf{x}$, while a TV penalty corresponds to a Laplace (exponential) prior on the gradient of $\mathbf{x}$ .

The goal is often to find the **Maximum A Posteriori (MAP)** estimate, the map $\mathbf{x}$ that maximizes $p(\mathbf{x}|\mathbf{y})$. Maximizing the posterior is equivalent to minimizing its negative logarithm. This reveals that the Tikhonov and TV [objective functions](@entry_id:1129021) are simply the negative log-posterior under Gaussian and Laplace priors, respectively.

When both the likelihood and prior are Gaussian, the posterior distribution is also Gaussian. In this case, one can compute not only the most probable map (the [posterior mean](@entry_id:173826), which is the MAP estimate) but also the full [posterior covariance matrix](@entry_id:753631), which provides a rigorous quantification of the uncertainties on the map's features .

### Epistemology of Eclipse Mapping: A Critical Assessment

A comprehensive understanding of eclipse mapping requires a critical evaluation of its foundational assumptions. These can be classified into distinct epistemic categories :

*   **Indispensable Assumptions:** These form the bedrock of the method. Without them, the inverse problem is undefined or unsolvable. This category includes:
    *   **Known Geometry ($\mathsf{G}$):** The orbital parameters and system scales must be known to construct the eclipse kernel $\mathbf{A}$, which connects the time-domain data to the spatial map.
    *   **Linearity ($\mathsf{L}$):** The assumption that the observed flux is a linear superposition of contributions from different parts of the planet allows the use of linear inverse theory.

*   **Empirically Testable Assumptions:** These are hypotheses whose validity can be directly assessed from the data.
    *   **Map Stationarity ($\mathsf{S}$):** The assumption that the map doesn't change during the eclipse can be tested by comparing ingress and egress light curves or by analyzing multiple eclipse observations over time.
    *   **Baseline Stability ($\mathsf{B}$):** The assumption of a constant, known [stellar flux](@entry_id:1132378) can be tested by analyzing the out-of-eclipse [photometry](@entry_id:178667) for stellar variability or instrumental trends.

*   **Revisable Modeling Choices:** These are necessary assumptions to obtain a specific solution, but they can be altered or replaced with more complex alternatives within the same inferential framework. The choice among them is a matter of [model selection](@entry_id:155601).
    *   **Emission Model ($\mathsf{A}$):** The assumption of Lambertian (isotropic) emission is a simplification. It can be replaced by more sophisticated models that include [limb darkening](@entry_id:157740) or brightening, and the data can be used to compare the goodness-of-fit of these different models.
    *   **Regularizing Prior ($\mathsf{P}$):** The need for some form of regularization is indispensable, but the specific *choice* of prior (e.g., Tikhonov smoothness vs. TV sparsity) is a revisable modeling choice. Different priors are better suited to different map morphologies, and statistical tools like Bayesian evidence can be used to guide this choice.

By understanding this hierarchy of assumptions, researchers can better interpret the results of eclipse mapping, distinguishing between features robustly demanded by the data and those influenced by the adopted modeling conventions.