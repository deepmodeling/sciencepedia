## Introduction
In medical imaging, noise is more than just a reduction in image clarity; it possesses a structure and texture that can obscure diagnostic information and confound quantitative analysis. While simple metrics like noise variance provide a single number to quantify noise magnitude, they fail to capture its spatial character—the very quality that determines whether noise appears as fine-grained salt-and-pepper static or as large, blotchy artifacts. To address this gap, we turn to a more sophisticated tool: the **Noise Power Spectrum (NPS)**. The NPS provides a comprehensive, frequency-based description of noise, allowing physicists and engineers to understand, predict, and control its impact on image quality.

This article offers a complete exploration of the Noise Power Spectrum, structured to build from foundational theory to practical application. The first chapter, **Principles and Mechanisms**, establishes the formal mathematical definition of the NPS, connecting it to the concepts of [stationarity](@entry_id:143776) and [autocovariance](@entry_id:270483), and explains how to interpret its shape to understand noise correlation and directionality. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how the NPS is shaped by the entire imaging chain—from [detector physics](@entry_id:748337) to reconstruction algorithms like FBP and Iterative Reconstruction—and its crucial role in task-based image quality assessment and the burgeoning field of radiomics. Finally, **Hands-On Practices** will provide opportunities to apply these concepts to practical problems in imaging [system analysis](@entry_id:263805).

## Principles and Mechanisms

In the analysis of medical images, noise is not merely a scalar value but a complex, spatially distributed phenomenon. To characterize its structure, we move beyond simple metrics like variance and employ the **Noise Power Spectrum (NPS)**. The NPS provides a powerful framework for understanding how noise power is distributed across different spatial frequencies, revealing crucial information about the texture, correlation, and directional properties of noise that ultimately impact diagnostic image quality. This chapter elucidates the fundamental principles defining the NPS and the mechanisms by which it is interpreted and estimated.

### The Formal Definition of the Noise Power Spectrum

We begin by modeling image noise as a two-dimensional **random field**, denoted by $n(\mathbf{x})$, where $\mathbf{x} \in \mathbb{R}^2$ is the continuous spatial coordinate. A foundational assumption in the analysis of many imaging systems is that the noise process is **[wide-sense stationary](@entry_id:144146) (WSS)**. A [random field](@entry_id:268702) is considered WSS if its statistical properties are invariant to spatial shifts, which formally requires two conditions to be met [@problem_id:4934400]:
1.  The mean of the [random field](@entry_id:268702) is constant for all spatial positions: $\mathbb{E}[n(\mathbf{x})] = \mu_n = \text{constant}$. For simplicity and without loss of generality, we often analyze the zero-mean version of the noise, $n_0(\mathbf{x}) = n(\mathbf{x}) - \mu_n$.
2.  The correlation between the noise values at two points depends only on the vector difference (or **lag**) between them, $\boldsymbol{\tau}$, and not on their absolute position.

This second condition is captured by the **[autocovariance function](@entry_id:262114)**. For a zero-mean, real-valued noise field, the [autocovariance](@entry_id:270483) $C_n(\boldsymbol{\tau})$ is defined as the [ensemble average](@entry_id:154225) of the product of noise values at two points separated by the lag vector $\boldsymbol{\tau}$:

$C_n(\boldsymbol{\tau}) = \mathbb{E}\{[n(\mathbf{x}) - \mu_n][n(\mathbf{x} + \boldsymbol{\tau}) - \mu_n]\}$

For a zero-mean process where $\mu_n=0$, this simplifies to the [autocorrelation function](@entry_id:138327), $C_n(\boldsymbol{\tau}) = \mathbb{E}\{n(\mathbf{x}) n(\mathbf{x} + \boldsymbol{\tau})\}$. It is crucial to recognize that the expectation operator $\mathbb{E}\{\cdot\}$ signifies an average over an ensemble of all possible realizations of the noise field, a theoretical concept that distinguishes the analysis of [random processes](@entry_id:268487) from that of [deterministic signals](@entry_id:272873) [@problem_id:4934478].

With the [autocovariance function](@entry_id:262114) established as the fundamental descriptor of the noise's second-order [spatial statistics](@entry_id:199807), we can now formally define the Noise Power Spectrum. The **Wiener-Khinchin theorem** states that for a WSS process, the NPS, denoted $S_n(\mathbf{f})$, is the two-dimensional Fourier transform of the [autocovariance function](@entry_id:262114) $C_n(\boldsymbol{\tau})$:

$S_n(\mathbf{f}) = \int_{\mathbb{R}^2} C_n(\boldsymbol{\tau}) e^{-i 2\pi \mathbf{f} \cdot \boldsymbol{\tau}} \, d\boldsymbol{\tau}$

Here, $\mathbf{f}$ is the spatial frequency vector. This definition provides the direct mathematical link between the [spatial correlation](@entry_id:203497) structure of the noise (encoded in $C_n(\boldsymbol{\tau})$) and its representation in the frequency domain. For this Fourier transform relationship to hold in the ordinary sense (i.e., for $S_n(\mathbf{f})$ to be a bounded function), the [autocovariance function](@entry_id:262114) must be absolutely integrable, meaning $\int_{\mathbb{R}^2} |C_n(\boldsymbol{\tau})| \, d\boldsymbol{\tau} \lt \infty$ [@problem_id:4934424].

### Interpreting the Noise Power Spectrum

The NPS is more than a mathematical transform; it is a rich descriptor of the noise's character. Its value at a given frequency $\mathbf{f}$ quantifies the contribution of that [spatial frequency](@entry_id:270500) component to the total noise variance.

#### Total Noise Variance

A fundamental property connects the NPS to the total variance of the noise field, $\sigma_n^2$. The variance is, by definition, the [autocovariance](@entry_id:270483) at zero lag: $\sigma_n^2 = C_n(\mathbf{0})$. Using the inverse Fourier transform relationship, we can express the [autocovariance](@entry_id:270483) in terms of the NPS:

$C_n(\boldsymbol{\tau}) = \int_{\mathbb{R}^2} S_n(\mathbf{f}) e^{i 2\pi \mathbf{f} \cdot \boldsymbol{\tau}} \, d\mathbf{f}$

Evaluating this expression at $\boldsymbol{\tau} = \mathbf{0}$ yields a profound result [@problem_id:4934398]:

$\sigma_n^2 = C_n(\mathbf{0}) = \int_{\mathbb{R}^2} S_n(\mathbf{f}) e^{0} \, d\mathbf{f} = \int_{\mathbb{R}^2} S_n(\mathbf{f}) \, d\mathbf{f}$

This equation demonstrates that the **total noise variance is the integral of the NPS over all spatial frequencies**. The NPS thus describes how the total "power" (variance) of the noise is distributed across the frequency domain.

For instance, consider a hypothetical imaging system with an anisotropic Gaussian NPS given by $S_n(f_x, f_y) = S_0 \exp(-f_x^2/\alpha^2 - f_y^2/\beta^2)$. To find the total noise variance, we integrate this function over the entire 2D frequency plane. This separable integral evaluates to $\sigma_n^2 = S_0 \pi \alpha \beta$ [@problem_id:4934398]. This example shows how the parameters defining the NPS shape ($S_0, \alpha, \beta$) directly determine the overall variance.

#### Frequency Content and Spatial Correlation

The shape of the NPS is a direct reflection of the correlation structure of the noise in the spatial domain [@problem_id:4934465]. This relationship is governed by the properties of the Fourier transform.

*   **Uncorrelated (White) Noise**: If the noise values at any two distinct points are uncorrelated, the [autocovariance function](@entry_id:262114) is a Dirac delta function: $C_n(\boldsymbol{\tau}) = \sigma_n^2 \delta(\boldsymbol{\tau})$. The Fourier transform of a delta function is a constant. Therefore, the NPS of uncorrelated noise is flat: $S_n(\mathbf{f}) = \sigma_n^2$. This is known as **[white noise](@entry_id:145248)**, signifying that noise power is distributed equally across all spatial frequencies.

*   **Correlated Noise**: In most real imaging systems, noise is correlated. This means $C_n(\boldsymbol{\tau})$ is non-zero for $\boldsymbol{\tau} \neq \mathbf{0}$. The shape of $C_n(\boldsymbol{\tau})$ dictates the shape of $S_n(\mathbf{f})$:
    *   If neighboring pixels are **positively correlated**, the noise exhibits a smooth, slowly varying appearance. This corresponds to an [autocovariance function](@entry_id:262114) that is broad and positive near the origin. Due to the uncertainty principle of Fourier transforms, a broad function in the spatial domain transforms to a narrow function in the frequency domain. Thus, the NPS will be concentrated at low spatial frequencies, appearing as a peak at or near $\mathbf{f} = \mathbf{0}$.
    *   If the noise has **negative correlations**, for example, if a bright noise pixel tends to be surrounded by darker ones, the [autocovariance function](@entry_id:262114) will oscillate. These high-frequency variations in the spatial domain translate to more power at high spatial frequencies in the NPS.

#### Directional Properties: Isotropy and Anisotropy

The NPS can also describe whether noise characteristics are uniform in all directions.

*   **Isotropic Noise**: Noise is **isotropic** if its statistical properties are rotationally invariant. This means the [autocovariance](@entry_id:270483) $C_n(\boldsymbol{\tau})$ depends only on the distance (magnitude) of the lag, $r = |\boldsymbol{\tau}|$, and not its direction. A fundamental property of the Fourier transform is that a rotationally invariant function transforms into another rotationally invariant function. Consequently, the NPS, $S_n(\mathbf{f})$, of isotropic noise will also be rotationally invariant, depending only on the radial frequency, $f = |\mathbf{f}|$. The **level sets** of an isotropic NPS—the curves in the frequency plane where $S_n(\mathbf{f})$ is constant—are concentric circles centered at the origin [@problem_id:4934425].

*   **Anisotropic Noise**: Noise is **anisotropic** when its correlation structure depends on direction. For example, if reconstruction algorithms or detector scanning patterns introduce different smoothing properties along the horizontal and vertical axes, the noise will be anisotropic. Consider a noise field with a separable Gaussian [autocovariance](@entry_id:270483), $C_n(\Delta x, \Delta y) \propto \exp(-(\Delta x^2/L_x^2 + \Delta y^2/L_y^2))$, where $L_x$ and $L_y$ are the correlation lengths along the $x$ and $y$ axes. If $L_x \neq L_y$, the noise is anisotropic. The resulting NPS is also a separable Gaussian, $S_n(f_x, f_y) \propto \exp(-\pi^2(f_x^2 L_x^2 + f_y^2 L_y^2))$. The level sets of this NPS are ellipses. Notably, the axes of the ellipses are inversely related to the correlation lengths: a shorter correlation length in space (e.g., small $L_x$) corresponds to a wider spread of power in frequency, resulting in a longer axis of the ellipse in that frequency direction (the $f_x$ axis) [@problem_id:4934425].

### Estimation of the Noise Power Spectrum

The theoretical definition of the NPS relies on the ensemble average, which requires an infinite number of noise realizations. In practice, we must estimate the NPS from a finite number of experimental images.

#### The Role of Ergodicity

The bridge between the theoretical [ensemble average](@entry_id:154225) and a practical spatial average is the assumption of **ergodicity**. A WSS process is said to be ergodic if its [ensemble averages](@entry_id:197763) are equivalent to spatial averages calculated over a single, sufficiently large realization [@problem_id:4934400]. For instance, for an ergodic process, the ensemble mean $\mu_n$ can be found by averaging a single noise image over its entire spatial extent. Similarly, the [autocovariance function](@entry_id:262114) can be estimated by calculating spatially averaged lagged products from a single image. This property provides the theoretical justification for estimating the NPS from a limited set of acquired data.

#### The Periodogram Estimator

The most common method for estimating the NPS is based on the **[periodogram](@entry_id:194101)**. For a discrete $M \times N$ region of interest (ROI) from a noise image $n[m,n]$, the [periodogram](@entry_id:194101) estimator, $\hat{S}(\mathbf{f})$, is proportional to the squared magnitude of its discrete Fourier transform. Proper normalization is critical to ensure the estimator has the correct physical units and scale. A correctly scaled 2D [periodogram](@entry_id:194101) estimator is:

$\hat{S}(\mathbf{f}) = \frac{\Delta x \Delta y}{MN} \left| \sum_{m=0}^{M-1}\sum_{n=0}^{N-1} n[m,n] e^{-i 2\pi (f_x m \Delta x + f_y n \Delta y)} \right|^2$

where $\Delta x$ and $\Delta y$ are the pixel spacings [@problem_id:4934458]. In practice, this single-ROI [periodogram](@entry_id:194101) is a very noisy estimate. To obtain a stable, low-variance estimate, one typically averages the periodograms calculated from multiple, independent ROIs or from multiple independent image acquisitions [@problem_id:4934478].

#### Statistical Properties and Practical Challenges

The [periodogram](@entry_id:194101) estimator has inherent statistical properties and is susceptible to practical artifacts that must be understood for accurate interpretation.

*   **Bias and Spectral Leakage**: The [periodogram](@entry_id:194101) is a **biased** estimator. Because it is computed from a finite-sized ROI, the underlying continuous noise field is implicitly multiplied by a [window function](@entry_id:158702) (e.g., a rectangle). In the frequency domain, this corresponds to the convolution of the true NPS with the power spectrum of the [window function](@entry_id:158702). This convolution causes spectral smoothing, blurring sharp features in the true NPS and limiting the [frequency resolution](@entry_id:143240) to be on the order of the inverse of the ROI size. It also causes **[spectral leakage](@entry_id:140524)**, where power from strong frequency components leaks into adjacent frequency bins [@problem_id:4934458] [@problem_id:4934455].

*   **Variance**: A [periodogram](@entry_id:194101) from a single ROI is an **inconsistent** estimator; its variance does not decrease as the ROI size increases. In fact, for Gaussian noise, the standard deviation of the estimate at a given frequency is approximately equal to its expected value [@problem_id:4934458]. This high variance makes a single [periodogram](@entry_id:194101) unreliable. As mentioned, averaging $K$ independent periodograms is the standard method to reduce the variance by a factor of $K$.

*   **Non-Zero Mean and Trends**: A common practical problem is the presence of a non-zero mean or a slowly varying background trend in the noise data, often due to detector gain non-uniformities or [vignetting](@entry_id:174163) effects.
    *   If the noise has a non-zero mean $\mu_n$, its true NPS contains a Dirac delta function term, $\mu_n^2 \delta(\mathbf{f})$, which appears as a large spike at the DC component ($\mathbf{f}=\mathbf{0}$) of the estimated NPS, potentially contaminating nearby low frequencies [@problem_id:4934478].
    *   If the image contains a slowly varying deterministic trend $m(\mathbf{x})$ in addition to the noise $n(\mathbf{x})$, the expected value of the estimated NPS becomes the sum of the true noise NPS and the power spectrum of the trend, $|M(\mathbf{f})|^2$. Since a slow trend has most of its power at low frequencies, this results in a characteristic artificial "upturn" in the estimated NPS at low frequencies. Simply subtracting the global image mean is insufficient to remove this artifact. **Detrending**—estimating and subtracting the smoothly varying background from the data *before* calculating the NPS—is essential for accurate low-frequency noise characterization [@problem_id:4934479].

*   **Non-Stationary Noise**: In some imaging modalities, noise statistics are not constant across the image (i.e., the noise is non-stationary). In such cases, a global NPS is not meaningful. The concept can be adapted by defining a **local NPS**, estimated from a small window centered at a specific location $\mathbf{r}_0$ [@problem_id:4934455]. This introduces a fundamental trade-off: a smaller window provides better spatial localization of the noise properties but suffers from poorer [frequency resolution](@entry_id:143240) and higher estimate variance. To improve statistics, one can average periodograms from overlapping windows, but this comes at the cost of reduced statistical independence between the estimates, yielding a smaller [variance reduction](@entry_id:145496) than with fully independent windows.