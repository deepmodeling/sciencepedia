## Introduction
The Cosmic Microwave Background (CMB) provides an unparalleled snapshot of the universe in its infancy. However, this primordial light has not traveled to us undisturbed. On its journey across billions of light-years, it has been subtly deflected by the gravitational pull of all the intervening matter, a phenomenon known as [gravitational lensing](@entry_id:159000). This effect encodes a wealth of information about the large-scale structure of the cosmos. The central challenge, which this article addresses, is how to extract this faint lensing signal from the CMB maps themselves. The primary statistical tool developed for this task is the [quadratic estimator](@entry_id:753901).

This article provides a graduate-level overview of CMB lensing reconstruction, guiding you from fundamental theory to cutting-edge application. We will navigate through three distinct stages of learning:

First, the **Principles and Mechanisms** chapter will lay the theoretical groundwork. We will explore how lensing imprints a specific non-Gaussian signature—a breaking of statistical [isotropy](@entry_id:159159)—onto the CMB. You will learn how the [quadratic estimator](@entry_id:753901) is mathematically constructed to isolate and measure this signature, and how its performance is optimized by carefully filtering the CMB data to minimize noise.

Next, the **Applications and Interdisciplinary Connections** chapter will shift focus to the scientific impact of this technique. We will see how reconstructed lensing maps are used to measure the [lensing power spectrum](@entry_id:751242), placing tight constraints on [cosmological parameters](@entry_id:161338) like the [matter density](@entry_id:263043) and [neutrino mass](@entry_id:149593). We will also examine its crucial role in modern astrophysics, from cross-correlating with galaxy surveys to "[delensing](@entry_id:748292)" the CMB in the monumental search for [primordial gravitational waves](@entry_id:161080).

Finally, the **Hands-On Practices** section will bridge the gap between theory and practical implementation. It outlines key computational projects that form the backbone of a real-world lensing analysis, from building an end-to-end simulation pipeline to handling the complexities of masked sky observations.

## Principles and Mechanisms

The reconstruction of the Cosmic Microwave Background (CMB) [lensing potential](@entry_id:161831) is a cornerstone of [modern cosmology](@entry_id:752086), transforming the CMB from a simple two-dimensional surface into a three-dimensional probe of the universe's intervening [large-scale structure](@entry_id:158990). This chapter elucidates the fundamental principles and mechanisms that underpin this technique, focusing on the widely used [quadratic estimator](@entry_id:753901) formalism. We will begin by describing how [gravitational lensing](@entry_id:159000) alters the observed CMB, proceed to explain how this alteration is exploited statistically to construct an estimator for the lensing field, and conclude with a discussion of the practical challenges and systematic effects encountered in real-world data analysis.

### The Lensing Effect as a Coordinate Remapping

The [gravitational lensing](@entry_id:159000) of the CMB is the deflection of microwave photons by the gravitational potentials of matter structures situated between the observer and the [last-scattering surface](@entry_id:159753). In a [standard cosmological model](@entry_id:159833), specifically a spatially flat Friedmann-Lemaître-Robertson–Walker (FLRW) universe with small scalar [metric perturbations](@entry_id:160321), photon paths are [null geodesics](@entry_id:158803) of the perturbed spacetime.

Under the [weak lensing](@entry_id:158468) regime, where deflections are small, the effect can be modeled as a simple remapping of the CMB sky. The observed (lensed) temperature or [polarization field](@entry_id:197617), which we denote as $\tilde{X}(\hat{n})$, at a given line-of-sight direction $\hat{n}$ is simply the unlensed field $X$ evaluated at a slightly different source direction $\hat{n}_s$:

$\tilde{X}(\hat{n}) = X(\hat{n}_s)$

The displacement between the observed and source directions is caused by the integrated [gravitational potential](@entry_id:160378) along the line of sight. This displacement can be expressed as the [gradient of a scalar field](@entry_id:270765) on the sky, the **[lensing potential](@entry_id:161831)** $\phi(\hat{n})$. In a widely used convention, the relationship is defined via a deflection field $\boldsymbol{d}(\hat{n})$:

$\boldsymbol{d}(\hat{n}) = \boldsymbol{\nabla}_{\hat{n}}\phi(\hat{n})$

where $\boldsymbol{\nabla}_{\hat{n}}$ is the covariant angular derivative on the [celestial sphere](@entry_id:158268). The deflection field relates the observed and source positions by $\hat{n}_s = \hat{n} + \boldsymbol{d}(\hat{n})$. The remapping equation is therefore:

$\tilde{X}(\hat{n}) = X\big(\hat{n} + \boldsymbol{d}(\hat{n})\big) = X\big(\hat{n} + \boldsymbol{\nabla}_{\hat{n}}\phi(\hat{n})\big)$

The [lensing potential](@entry_id:161831) itself is a projection of the three-dimensional [gravitational potential](@entry_id:160378), $\Psi$, along the line of sight. Within the **Born approximation**, where the integration is performed along the unperturbed path, and assuming a single source plane at [comoving distance](@entry_id:158059) $\chi_*$ (the [last-scattering surface](@entry_id:159753)), the [lensing potential](@entry_id:161831) is given by [@problem_id:3467510]:

$$\phi(\hat{n}) = -2 \int_{0}^{\chi_*} d\chi\,\frac{\chi_* - \chi}{\chi_* \chi}\,\Psi\big(\chi\hat{n}, \eta_0 - \chi\big)$$

Here, $\chi$ is the [comoving distance](@entry_id:158059), and $\eta_0 - \chi$ is the [conformal time](@entry_id:263727) at that distance. This formalism relies on several key assumptions: the validity of [geometric optics](@entry_id:175028), a spatially flat background metric, and the absence of significant [anisotropic stress](@entry_id:161403), which allows the two scalar potentials of the perturbed metric to be considered equal. Higher-order effects, such as post-Born corrections and lens-lens couplings, are neglected in this leading-order description.

Another important quantity related to the [lensing potential](@entry_id:161831) is the **lensing convergence**, $\kappa$. It describes the local [magnification](@entry_id:140628) of the CMB field and is defined as $\kappa = -\frac{1}{2} \nabla \cdot \boldsymbol{d}$. In harmonic space, this relationship simplifies to a direct scaling [@problem_id:3467589]:

$\kappa(\boldsymbol{L}) = \frac{L^2}{2} \phi(\boldsymbol{L})$

where $\boldsymbol{L}$ is the two-dimensional [wavevector](@entry_id:178620) (multipole) and $L = |\boldsymbol{L}|$.

### Breaking Statistical Isotropy: The Origin of the Lensing Signal

The primordial CMB anisotropies are believed to be a realization of a statistically isotropic and homogeneous Gaussian [random field](@entry_id:268702). A key consequence of statistical isotropy is that the harmonic modes of the unlensed field, $X_{\boldsymbol{\ell}}$, are uncorrelated for different wavevectors. Their [two-point correlation function](@entry_id:185074) (or [power spectrum](@entry_id:159996)) is diagonal:

$\langle X_{\boldsymbol{\ell}} Y_{\boldsymbol{\ell}'} \rangle = (2\pi)^2 \delta^{(2)}(\boldsymbol{\ell} + \boldsymbol{\ell}') C_{\ell}^{XY}$

where $C_{\ell}^{XY}$ is the cross-power spectrum, which depends only on the magnitude $\ell = |\boldsymbol{\ell}|$, and $\delta^{(2)}$ is the two-dimensional Dirac delta function.

Gravitational lensing fundamentally alters this statistical property. A specific realization of the large-scale structure, and thus a specific [lensing potential](@entry_id:161831) $\phi(\hat{n})$, is not itself statistically isotropic. By remapping the CMB fields, this anisotropic potential imprints its structure onto the observed CMB, breaking its statistical isotropy.

To see this explicitly, we can perform a first-order Taylor expansion of the remapping equation for small deflections, $\boldsymbol{d}(\hat{n})$:

$\tilde{X}(\hat{n}) \approx X(\hat{n}) + \boldsymbol{d}(\hat{n}) \cdot \boldsymbol{\nabla}X(\hat{n}) = X(\hat{n}) + (\boldsymbol{\nabla}\phi(\hat{n})) \cdot (\boldsymbol{\nabla}X(\hat{n}))$

When we compute the [two-point correlation function](@entry_id:185074) of the lensed fields $\tilde{X}$ and $\tilde{Y}$, a new term emerges at first order in $\phi$. This term creates correlations between modes $\boldsymbol{\ell}$ and $\boldsymbol{\ell}'$ where $\boldsymbol{\ell}+\boldsymbol{\ell}' \neq \boldsymbol{0}$. For a fixed realization of the [lensing potential](@entry_id:161831) $\phi$, the lensed CMB covariance becomes [@problem_id:3467538]:

$\langle \tilde{X}_{\boldsymbol{\ell}} \tilde{Y}_{\boldsymbol{\ell}'} \rangle_{\text{CMB}|\phi} = (2\pi)^2 \delta^{(2)}(\boldsymbol{\ell}+\boldsymbol{\ell}') C_{\ell}^{XY} + \phi_{\boldsymbol{\ell}+\boldsymbol{\ell}'} \left[ (\boldsymbol{\ell}+\boldsymbol{\ell}') \cdot \boldsymbol{\ell}\, C_{\ell}^{XY} + (\boldsymbol{\ell}+\boldsymbol{\ell}') \cdot \boldsymbol{\ell}'\, C_{\ell'}^{XY} \right]$

This expression reveals the central principle of lensing reconstruction. The [lensing potential](@entry_id:161831) mode $\phi_{\boldsymbol{L}}$ (where $\boldsymbol{L} = \boldsymbol{\ell}+\boldsymbol{\ell}'$) induces a specific, non-diagonal correlation between pairs of small-scale CMB modes $\boldsymbol{\ell}$ and $\boldsymbol{\ell}'$. The amplitude of this correlation is proportional to $\phi_{\boldsymbol{L}}$. This phenomenon is often described as **mode-coupling**. A large-scale lensing mode couples pairs of small-scale CMB modes. By measuring this pattern of off-diagonal covariance in the observed CMB data, we can infer, or estimate, the [lensing potential](@entry_id:161831) itself.

### The Quadratic Estimator Framework

An estimator designed to measure a quantity proportional to the product of two fields is known as a **[quadratic estimator](@entry_id:753901)**. Given that the lensing-induced covariance is proportional to the product of two CMB fields and the [lensing potential](@entry_id:161831), it is natural to construct an estimator for $\phi$ that is quadratic in the observed CMB map.

The general form of a [quadratic estimator](@entry_id:753901) for the [lensing potential](@entry_id:161831) mode $\phi(\boldsymbol{L})$ is an integral over all pairs of observed CMB modes, $T^{\text{tot}}(\boldsymbol{\ell})$ and $T^{\text{tot}}(\boldsymbol{L}-\boldsymbol{\ell})$, that could be coupled by the lensing mode $\boldsymbol{L}$ [@problem_id:3467514]:

$$\hat{\phi}(\boldsymbol{L}) \equiv A_{L} \int \frac{d^{2}\boldsymbol{\ell}}{(2\pi)^{2}}\, g(\boldsymbol{\ell}, \boldsymbol{L}-\boldsymbol{\ell})\, T^{\text{tot}}(\boldsymbol{\ell})\, T^{\text{tot}}(\boldsymbol{L}-\boldsymbol{\ell})$$

Here, $T^{\text{tot}}$ represents the total observed temperature map, which includes the lensed CMB, astrophysical foregrounds, and instrumental noise. The function $g(\boldsymbol{\ell}, \boldsymbol{\ell}')$ is a carefully chosen **weight function**, and $A_L$ is a **normalization factor**. The goal of the formalism is to determine the weights and normalization such that the [expectation value](@entry_id:150961) of the estimator, $\langle \hat{\phi}(\boldsymbol{L}) \rangle$, is equal to the true [lensing potential](@entry_id:161831) mode $\phi(\boldsymbol{L})$, and that the variance of the estimator is minimized.

While typically formulated in harmonic space, this estimation can also be conceived in real space. For instance, an estimator for the convergence $\kappa(\hat{n})$ can be constructed from local products of filtered temperature maps, such as $\nabla \cdot (T_a(\hat{n}) \nabla T_b(\hat{n}))$, where $T_a$ and $T_b$ are versions of the observed map convolved with specific kernels [@problem_id:3467584]. This [real-space](@entry_id:754128) picture reinforces the intuition that lensing reconstruction measures correlations between the CMB field and its own gradient.

### Optimizing Estimator Performance

The efficacy of a [quadratic estimator](@entry_id:753901) is determined by its [signal-to-noise ratio](@entry_id:271196). Constructing an [optimal estimator](@entry_id:176428) involves maximizing the response to the lensing signal while minimizing the statistical uncertainty, or reconstruction noise.

#### The Lensing Signal and Power Spectrum Gradients

The "signal" for the [quadratic estimator](@entry_id:753901) originates from the coupling term in the lensed covariance, which involves factors like $(\boldsymbol{\ell}+\boldsymbol{\ell}') \cdot \boldsymbol{\ell}\, C_{\ell}^{XY}$. This can be intuitively understood as being proportional to the gradient of the unlensed power spectrum, $\nabla_{\boldsymbol{\ell}} C_\ell$. A [power spectrum](@entry_id:159996) with sharp features and steep gradients provides a much stronger lensing signal than a smooth, featureless one [@problem_id:3467516].

This principle has profound consequences for choosing which CMB fields to use for reconstruction. At high multipoles ($\ell \gtrsim 1500$), the temperature [power spectrum](@entry_id:159996), $C_\ell^{TT}$, is in its **Silk damping tail**—a region of smooth, exponential decay where the gradient is very small. In contrast, the $E$-mode polarization [power spectrum](@entry_id:159996), $C_\ell^{EE}$, retains significant acoustic peak structure at these scales. The sharp gradients on the sides of these polarization peaks provide a much larger lensing response. Consequently, for reconstructing small-scale lensing modes (large $L$), polarization-based estimators (like the $EE$ estimator) can significantly outperform the temperature-only ($TT$) estimator, provided the instrumental noise in polarization is sufficiently low [@problem_id:3467516].

#### Optimal Filtering and Reconstruction Noise

The primary source of uncertainty in the reconstruction is **reconstruction noise**. This noise arises from the chance correlations present in the unlensed CMB and instrumental noise, which mimic the signature of lensing. For a Gaussian field, these chance correlations are described by the disconnected part of the four-point function. The resulting noise [power spectrum](@entry_id:159996) is often denoted $N_L^{(0)}$.

To minimize this reconstruction noise, the input CMB maps must be optimally filtered. The task is to design a filter, $F_\ell$, applied to the observed map $T^{\text{tot}}_\ell$, that maximizes sensitivity. Using the Cauchy-Schwarz inequality, one can show that the filter that minimizes the [estimator variance](@entry_id:263211) for a fixed signal response is [@problem_id:3467521]:

$F_\ell \propto \frac{S_\ell}{C_\ell^{\text{tot}}}$

where $C_\ell^{\text{tot}} = C_\ell^{\text{CMB}} + N_\ell^{\text{noise}}$ is the total power spectrum of the observed map, and $S_\ell$ is a response kernel that models the signal template. If one uses prior knowledge that the lensing signal is sourced by the CMB itself, a natural choice is $S_\ell = C_\ell^{\text{CMB}}$. This leads to the well-known **Wiener filter**:

$F_\ell^{\text{Wiener}} \propto \frac{C_\ell^{\text{CMB}}}{C_\ell^{\text{CMB}} + N_\ell^{\text{noise}}}$

This filter provides an optimal trade-off: it up-weights modes where the signal-to-noise ratio is high (i.e., where $C_\ell^{\text{CMB}} \gg N_\ell^{\text{noise}}$) and down-weights modes dominated by instrumental noise.

#### Combining Estimators

Quadratic estimators can be constructed from various pairs of CMB fields: temperature (TT), E-mode polarization (EE), B-mode polarization (BB), and their cross-correlations (TE, EB, TB). Each of these estimators has a different signal response and is affected differently by noise. For example, the **EB estimator** is particularly powerful because unlensed B-modes are expected to be nearly zero. Therefore, any measured correlation between E-modes and B-modes is a very clean tracer of lensing, which converts E-modes into B-modes.

To achieve the best possible measurement, these individual estimators are combined into a single **minimum-variance (MV) estimator**. This is achieved by weighting each individual estimator by its inverse reconstruction noise variance. The relative importance of different channels, such as EB versus TT, depends on the lensing scale $L$ as well as the instrumental noise properties and beam size [@problem_id:3467552]. For a given experiment, polarization channels often dominate the reconstruction on small angular scales, while the temperature channel dominates on large scales.

Finally, we note that the reconstruction noise [power spectrum](@entry_id:159996) for the convergence, $N_L^\kappa$, is simply related to that of the potential, $N_L^\phi$, through their harmonic-space definition. A direct application of linear [error propagation](@entry_id:136644) shows [@problem_id:3467589]:

$N_L^\kappa = \frac{L^4}{4} N_L^\phi$

This implies that the signal-to-noise ratio for convergence reconstruction falls off rapidly at low $L$ compared to the potential reconstruction.

### Systematic Effects and Practical Considerations in Lensing Reconstruction

Applying the [quadratic estimator](@entry_id:753901) formalism to real data introduces several practical challenges and potential systematic biases that are absent in an idealized full-sky, noise-free, and foreground-free scenario.

#### Foreground-Induced Bias

Astrophysical foregrounds, such as the thermal Sunyaev-Zel'dovich (tSZ) effect and the Cosmic Infrared Background (CIB), are significant contaminants in CMB temperature maps. These foregrounds are inherently non-Gaussian, as they arise from discrete, clustered sources. This non-Gaussianity means they possess a non-zero intrinsic connected four-point function, or **[trispectrum](@entry_id:158605)**.

When a [quadratic estimator](@entry_id:753901) is applied to a map containing these foregrounds, the foreground [trispectrum](@entry_id:158605) contributes to the estimator's four-point function in the same way as the lensing signal does. This creates an additive bias in the reconstructed [lensing power spectrum](@entry_id:751242), $\Delta C_L^{\phi\phi}$. For a simplified "white [trispectrum](@entry_id:158605)" model where the foreground [trispectrum](@entry_id:158605) is assumed to be constant, $T_0$, this bias is given by [@problem_id:3467514]:

$$\Delta C_L^{\phi\phi} = A_L^2 T_0 \left[ \int \frac{d^2\boldsymbol{\ell}}{(2\pi)^2} g(\boldsymbol{\ell}, \boldsymbol{L}-\boldsymbol{\ell}) \right]^2$$

This foreground bias is a major systematic for lensing reconstruction using temperature data and must be modeled and subtracted, or mitigated by using multi-frequency data to clean the foregrounds from the CMB map before estimation.

#### Masking and Boundary Effects

Real CMB maps have incomplete sky coverage due to galactic contamination and point source masking. This masking procedure, equivalent to multiplying the true sky by a [window function](@entry_id:158702) or mask $W(\boldsymbol{x})$, breaks the statistical isotropy of the data. This has two primary consequences for quadratic estimators.

First, it generates a **mean-field bias**. Even in the absence of lensing, the mask induces mode-couplings that give the [quadratic estimator](@entry_id:753901) a non-zero expectation value, $\langle \hat{\phi} \rangle \neq 0$. This spurious signal is often largest near the mask boundaries and its amplitude is related to the gradient of the [window function](@entry_id:158702). To mitigate this, masks are typically smoothed or **apodized**. A classic approach is to find a [window function](@entry_id:158702) that minimizes the bias source term (related to the Dirichlet energy, $\int |\nabla W|^2 d^2x$) while preserving the overall normalization of the estimator. For a square patch, this leads to an optimal window of the form $W(x, y) = 2 \sin(\frac{\pi x}{L}) \sin(\frac{\pi y}{L})$ [@problem_id:3467536].

Second, even with [apodization](@entry_id:147798), complex masks and inhomogeneous instrumental noise will generate a residual mean-field that must be subtracted. This is typically done using simulations. A large number of simulated unlensed CMB maps are passed through the full analysis pipeline (including masking and noise addition) to compute the average response of the estimator, which serves as an estimate of the mean-field. The statistical uncertainty of this simulation-based correction decreases with the number of simulations, $N_{\text{sim}}$, as $N_{\text{sim}}^{-1/2}$. To ensure the residual bias is a small fraction $r$ of the statistical error on the estimator itself, the number of simulations must satisfy $N_{\text{sim}} \ge 1/r^2$ [@problem_id:3467586]. This can necessitate hundreds or thousands of simulations for a high-precision analysis.

In summary, CMB lensing reconstruction is a powerful technique built on a solid theoretical foundation. Its successful application requires not only an understanding of the fundamental lensing effect and the statistical principles of the [quadratic estimator](@entry_id:753901) but also careful control and mitigation of a host of systematic effects inherent to real-world cosmological data analysis.