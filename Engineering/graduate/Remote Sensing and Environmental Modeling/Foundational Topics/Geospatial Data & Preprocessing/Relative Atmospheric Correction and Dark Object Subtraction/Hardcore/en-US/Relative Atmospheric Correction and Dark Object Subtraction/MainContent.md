## Introduction
The conversion of raw satellite signals into physically meaningful surface reflectance is a fundamental step for quantitative environmental analysis. However, the Earth's atmosphere introduces significant distortions, scattering and absorbing light in ways that obscure the true signal from the surface. This article addresses the challenge of correcting for these atmospheric effects by focusing on two widely-used, image-based techniques: Dark Object Subtraction and [relative atmospheric correction](@entry_id:1130818). In the following chapters, you will first explore the foundational **Principles and Mechanisms** of radiative transfer that underpin these methods. Next, you will discover their **Applications and Interdisciplinary Connections**, learning how they enable critical analyses in fields from ecology to [climatology](@entry_id:1122484) and understanding their limitations. Finally, you will put theory into practice with a series of **Hands-On Practices** designed to solidify your understanding of the correction workflow. This journey will equip you with the essential knowledge to transform raw remote sensing data into reliable, analysis-ready information.

## Principles and Mechanisms

The process of converting raw [digital signals](@entry_id:188520) from a remote sensing instrument into physically meaningful surface reflectance values is a critical step in quantitative environmental analysis. This transformation, known as atmospheric correction, seeks to remove the confounding effects of the atmosphere, which both attenuates the signal from the Earth's surface and adds its own signal through scattering. This chapter delves into the principles and mechanisms of two foundational approaches: image-based correction using the Dark Object Subtraction method and relative normalization using stable surface features.

### The Radiative Transfer Model: Decomposing the At-Sensor Signal

The radiance measured by a satellite sensor, termed the **[at-sensor spectral radiance](@entry_id:1121172)** $L_{sensor}(\lambda)$, is a composite signal. For a sensor viewing the Earth's surface at a specific wavelength $\lambda$ in the solar-reflective spectrum, this signal can be decomposed into its primary constituents. A simplified, yet powerful, model represents the [at-sensor radiance](@entry_id:1121171) as the sum of radiance originating from the surface and radiance originating from the atmosphere itself .

The fundamental decomposition is expressed as:

$L_{sensor}(\lambda) = L_p(\lambda) + T_v(\lambda) L_s(\lambda)$

Here, the terms represent distinct physical processes:

1.  **Path Radiance**, $L_p(\lambda)$: This is an additive component representing photons from the sun that are scattered by atmospheric molecules and aerosols directly into the sensor's field of view without ever interacting with the target surface. This term is the primary source of atmospheric "haze" and is a function of the atmospheric composition, solar illumination geometry, and viewing angle .

2.  **Surface-Leaving Radiance**, $L_s(\lambda)$: This is the radiance that is reflected or emitted by the surface itself in the direction of the sensor. For a perfectly diffuse, or **Lambertian**, surface with a given **surface reflectance** $\rho(\lambda)$, this radiance is related to the total hemispherical [irradiance](@entry_id:176465) reaching the surface, $E_d(\lambda)$, by the relation $L_s(\lambda) = \rho(\lambda) E_d(\lambda) / \pi$.

3.  **Atmospheric Transmittance**, $T_v(\lambda)$: This is a multiplicative, dimensionless factor (between $0$ and $1$) that describes the attenuation of the surface-leaving radiance as it travels upward through the atmosphere to the sensor. This attenuation is caused by both absorption and scattering of photons out of the line of sight.

The path radiance $L_p(\lambda)$ and transmittance $T_v(\lambda)$ are distinct consequences of the same physical processes: scattering and absorption. Transmittance quantifies the loss of signal from a beam of light due to photons being either absorbed or scattered away (**out-scattering**). Path radiance, in contrast, is a gain of signal due to photons from the ambient light field being scattered into the sensor's line of sight (**in-scattering**). Formally, $L_p(\lambda)$ is the [line-of-sight integral](@entry_id:751289) of the in-scattering source term, with each contribution being attenuated on its remaining path to the sensor. Both transmittance and path radiance are profoundly influenced by the atmospheric composition, particularly the concentration and properties of aerosols .

### From Radiance to Reflectance

While sensor measurements are in units of radiance, the intrinsic property of the surface that is most often desired for environmental analysis is its reflectance, $\rho(\lambda)$. Reflectance is a dimensionless quantity that describes the fraction of incident light a surface reflects. To retrieve it, we must first convert the raw Digital Number ($DN$) recorded by the sensor into at-sensor radiance $L_{sensor}(\lambda)$ using sensor-specific calibration coefficients for gain ($G$) and offset ($O$):

$L_{sensor}(\lambda) = G \cdot DN + O$

Next, we must account for the illumination source. The [at-sensor radiance](@entry_id:1121171) is converted to a quantity called **Top-of-Atmosphere (TOA) reflectance**, $\rho_{TOA}$, which normalizes the measured radiance by the incoming solar irradiance. This accounts for the [solar zenith angle](@entry_id:1131912) ($\theta_s$) and the variation in the Earth-Sun distance ($d$, in astronomical units) throughout the year. For a Lambertian surface, the formula is :

$\rho_{TOA}(\lambda) = \frac{\pi L_{sensor}(\lambda) d^2}{E_{sun}(\lambda) \cos(\theta_s)}$

where $E_{sun}(\lambda)$ is the mean exoatmospheric solar irradiance at wavelength $\lambda$.

It is crucial to understand that TOA reflectance is not the same as surface reflectance. As derived from $L_{sensor}(\lambda)$, $\rho_{TOA}$ is still "contaminated" by the atmosphere. It contains an additive contribution from path radiance and is multiplicatively affected by atmospheric attenuation. Furthermore, for non-Lambertian surfaces, it is subject to angular anisotropy, or **bidirectional effects**, from both the surface's Bidirectional Reflectance Distribution Function (BRDF) and the atmosphere itself. True atmospheric correction aims to solve for the surface reflectance, $\rho_s(\lambda)$, by inverting the radiative transfer model to remove these atmospheric effects from $\rho_{TOA}$ or $L_{sensor}$ .

### Dark Object Subtraction (DOS)

The **Dark Object Subtraction (DOS)** method is a widely used, image-based technique that provides a [first-order correction](@entry_id:155896) for the additive effects of atmospheric path radiance. It operates on a simple yet effective premise.

The formal definition of DOS is that it estimates the additive atmospheric path radiance in a given spectral band by identifying the minimum [at-sensor radiance](@entry_id:1121171) value, $L_{min}(\lambda)$, observed across the entire scene (after correcting for any instrumental offset). This minimum value is then assumed to be a reasonable estimate of the path radiance, $L_p(\lambda)$, and is subtracted from every pixel in that band .

$L_{corrected}(\lambda) = L_{sensor}(\lambda) - L_{min}(\lambda)$

This simple procedure rests on a series of critical implicit assumptions:

1.  **Existence of a Dark Object**: The scene must contain at least one pixel (or a small population of pixels) whose true surface reflectance in that band is approximately zero. For this "dark object," the surface-leaving radiance term $T_v(\lambda) L_s(\lambda)$ vanishes, and the measured at-sensor radiance consists almost entirely of path radiance: $L_{sensor, dark}(\lambda) \approx L_p(\lambda)$.

2.  **Spatially Uniform Path Radiance**: The method assumes that the path radiance is constant across the entire image. This allows the single value estimated from the dark object's location to be applied globally. This assumption is generally valid for small scenes acquired under horizontally homogeneous atmospheric conditions but breaks down in the presence of, for example, spatially variable aerosol loading .

3.  **Negligible Adjacency Effects**: It is assumed that the radiance of the dark pixel is not contaminated by light scattered from its brighter neighbors. This "adjacency effect," discussed later, can lead to an overestimation of path radiance.

A complete DOS workflow to retrieve apparent surface reflectance involves several steps, as illustrated by the following example . Consider a sensor with gain $G=0.05$ and offset $O=10$ (in relevant units) observes a target pixel with $DN_{target}=2500$ and a dark object with $DN_{dark}=100$. The exoatmospheric [irradiance](@entry_id:176465) is $E_{sun}=1928$, the [solar zenith angle](@entry_id:1131912) is $\theta_s=30^\circ$, and the Earth-Sun distance ratio is $d=0.991$.

-   **Step 1: Convert DN to Radiance.**
    $L_{target} = (0.05)(2500) + 10 = 135$
    $L_{dark} = (0.05)(100) + 10 = 15$

-   **Step 2: Estimate and Subtract Path Radiance.**
    The path radiance is estimated as $L_p \approx L_{dark} = 15$. The corrected radiance for the target pixel is:
    $L' = L_{target} - L_p = 135 - 15 = 120$

-   **Step 3: Convert Corrected Radiance to Apparent Reflectance.**
    Using the TOA reflectance formula with the corrected radiance $L'$:
    $\rho = \frac{\pi L' d^2}{E_{sun}(\lambda) \cos(\theta_s)} = \frac{\pi (120) (0.991)^2}{(1928) \cos(30^\circ)} \approx 0.222$

### The Spectral Nature of Path Radiance

A critical aspect of atmospheric correction is the strong dependence of path radiance on wavelength. This spectral behavior is driven by the physics of atmospheric scattering. The two dominant scattering mechanisms are:

-   **Rayleigh Scattering**: Scattering by air molecules, which are much smaller than the wavelength of light. Its efficiency scales as $\lambda^{-4}$, meaning it is much stronger for shorter (blue) wavelengths than for longer (red) wavelengths. This is why a clear sky appears blue.
-   **Mie Scattering**: Scattering by larger particles such as aerosols (dust, smoke, pollutants). Its spectral dependence is generally weaker and is often modeled as $\lambda^{-\alpha}$, where $\alpha$ is the **Ångström exponent**. The value of $\alpha$ depends on the size distribution of the aerosol particles; it is larger for fine-mode aerosols and decreases towards zero for coarse-mode particles (e.g., dust or sea salt), making the scattering more spectrally neutral or "gray" .

The total path radiance is a mixture of these two components. Consequently, $L_p(\lambda)$ is not constant with wavelength. For example, measured minimum TOA radiances over deep water might be $30$, $20$, $13$, and $6$ (in $\mathrm{W\,m^{-2}\,sr^{-1}\,\mu m^{-1}}$) for blue, green, red, and near-infrared bands, respectively. This strong decrease with wavelength demonstrates that a DOS correction must be performed **independently for each spectral band**. Applying a single path radiance value (e.g., the one derived from the near-infrared band) to all bands would severely under-correct the shorter wavelengths, leaving a significant residual blue-green haze in the corrected image .

### Variants of the DOS Method

The basic DOS procedure has been refined into a hierarchy of models that progressively incorporate more physical realism. These are commonly referred to as DOS1, DOS2, and DOS3 .

-   **DOS1**: This is the simplest model, as described in the numerical example above. It assumes the atmospheric transmittance is unity ($T_v(\lambda) = 1$) and that all surface illumination comes from the direct solar beam (i.e., diffuse skylight is ignored). It is a pure haze subtraction.

-   **DOS2**: This model improves upon DOS1 by accounting for the atmospheric attenuation of the signal from the surface, using an estimated transmittance value $T_v(\lambda) \lt 1$. It still, however, typically neglects the contribution of diffuse skylight to surface illumination.

-   **DOS3**: This model provides a more physically complete correction by accounting for path radiance, atmospheric transmittance, direct solar [irradiance](@entry_id:176465), and diffuse skylight irradiance ($E_{diff, \lambda} > 0$). The diffuse [irradiance](@entry_id:176465) is often modeled as a function of the path radiance itself, leveraging the fact that both are driven by atmospheric scattering.

### Limitations: The Adjacency Effect

A significant limitation of simple DOS models is their neglect of the **[adjacency effect](@entry_id:1120809)**. This phenomenon occurs when photons reflected from bright surfaces are scattered by the atmosphere into the [field of view](@entry_id:175690) of a sensor observing an adjacent, darker target. This effect acts as a low-pass spatial filter, blurring the scene and adding radiance to dark pixels that is not their own.

Mathematically, the adjacency radiance $L_{adj}(x, \lambda)$ at a pixel location $x$ can be modeled as a spatial convolution of the surrounding surface-leaving radiance field $L_{surf}$ with an atmospheric [point spread function](@entry_id:160182) (PSF), $h_\lambda$ :

$L_{adj}(x, \lambda) = \int_{\mathbb{R}^2} h_\lambda(r) L_{surf}(x + r, \lambda) \mathrm{d}^2 r$

The implication for DOS is significant. When a dark object is located near brighter surfaces, its measured radiance $L_{sensor, dark}$ is not just the true path radiance $L_p$, but rather $L_p + L_{adj}$. Since $L_{adj}$ is always positive, the DOS method will overestimate the path radiance, leading to over-correction (subtracting too much) in other parts of the scene .

### Relative Atmospheric Correction with Pseudo-Invariant Features

An alternative to the absolute correction attempted by DOS is **[relative atmospheric correction](@entry_id:1130818)**. This approach does not aim to retrieve the true surface reflectance but instead normalizes a target image to match the radiometric conditions of a reference image, which is assumed to be well-corrected or is used as a baseline. This is particularly useful for change detection studies, where consistency between images is more important than absolute accuracy.

This method relies on identifying **Pseudo-Invariant Features (PIFs)**: objects whose surface reflectance is assumed to be stable over time. Examples include deep water bodies, bare soil, asphalt parking lots, and specific rooftops .

PIFs are selected using rigorous statistical criteria to ensure their temporal stability. For a set of multi-date images, candidate PIFs are identified by requiring :
-   **Low Temporal Variability**: The [coefficient of variation](@entry_id:272423) ($CV = \sigma / \mu$) of the pixel's reflectance or radiance over time should be very low.
-   **Low Spectral Shape Change**: The spectral angle between the pixel's reflectance vectors on different dates should be minimal, indicating the material composition has not changed.
-   **Exclusion of Unstable Areas**: Pixels affected by shadow, saturation, or [land cover change](@entry_id:1127048) (e.g., identified by a change in NDVI) must be excluded.

Once a robust set of PIFs is identified across a reference image (day R) and a target image (day T), their at-sensor radiances ($L_r$ and $L_t$) are extracted. Under the assumption of a linear relationship between surface reflectance and at-sensor radiance, the radiances of the PIFs on the two dates will be linearly related:

$L_t = \alpha L_r + \beta$

The gain ($\alpha$) and offset ($\beta$) parameters can be determined by performing a [linear regression](@entry_id:142318) on the PIF radiance pairs. The target image is then normalized to the reference image's radiometric scale by applying the inverse of this transformation to every pixel in the target image :

$L_{norm} = \frac{L_t - \beta}{\alpha}$

This PIF-based approach provides a robust and physically-grounded method for achieving relative radiometric consistency between images, effectively compensating for differences in atmospheric conditions and illumination geometry without requiring a full radiative transfer inversion.