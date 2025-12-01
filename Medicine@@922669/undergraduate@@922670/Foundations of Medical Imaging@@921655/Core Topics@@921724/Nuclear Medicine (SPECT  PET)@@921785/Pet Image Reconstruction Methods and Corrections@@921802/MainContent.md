## Introduction
Positron Emission Tomography (PET) is a cornerstone of modern [molecular imaging](@entry_id:175713), providing unique insights into physiological processes within the body. However, the raw data acquired by a PET scanner is not a direct picture; it is an indirect, noisy, and physically distorted set of measurements. The fundamental challenge, and the focus of this article, is the process of [image reconstruction](@entry_id:166790): the sophisticated computational task of transforming this raw data into a quantitatively accurate and diagnostically useful image. This involves solving a complex inverse problem, navigating statistical noise, and correcting for a host of physical phenomena that degrade the signal.

This article provides a comprehensive overview of the principles, methods, and corrections that underpin modern PET image reconstruction. In the "Principles and Mechanisms" chapter, we will build the mathematical [forward model](@entry_id:148443) from the ground up, explore the classic analytic approach of Filtered Backprojection, and delve into the powerful statistical [iterative algorithms](@entry_id:160288) like ML-EM and OSEM that define the current state of the art. We will also detail the essential corrections for attenuation, scatter, and other effects that are vital for accuracy. The "Applications and Interdisciplinary Connections" chapter will demonstrate how these rigorous methods enable quantitative applications, such as the calculation of Standardized Uptake Value (SUV), and create unique challenges and opportunities in hybrid PET/CT and PET/MRI systems. Finally, the "Hands-On Practices" section will provide practical problems to solidify your understanding of these core concepts, bridging theory with application.

## Principles and Mechanisms

The process of forming a diagnostic image from the raw data acquired by a Positron Emission Tomography (PET) scanner is a sophisticated task in computational science, bridging physics, statistics, and [numerical optimization](@entry_id:138060). This chapter elucidates the fundamental principles and mechanisms that govern PET [image reconstruction](@entry_id:166790). We will begin by constructing the mathematical "[forward model](@entry_id:148443)" that describes the [data acquisition](@entry_id:273490) process, then explore the major families of reconstruction algorithms—analytic and iterative—and finally delve into the critical corrections and advanced modeling techniques required for quantitative accuracy.

### The Forward Model: From Physics to Mathematics

At its core, image reconstruction seeks to solve an inverse problem: given a set of measured projection data, what is the underlying [spatial distribution](@entry_id:188271) of radiotracer that produced it? To solve this, we must first have a precise "[forward model](@entry_id:148443)" that describes how a given tracer distribution generates the data we measure.

#### Idealized Projections and the Radon Transform

In an idealized scenario, stripped of all physical complexities like photon attenuation, scatter, and statistical noise, a PET scanner measures the total radioactivity along straight lines passing through the object. A pair of back-to-back annihilation photons defines a **Line of Response (LOR)**. The collection of all LOR measurements constitutes the projection data.

Mathematically, this idealized measurement process is described by the **Radon Transform**. For a two-dimensional activity distribution $f(\mathbf{x})$, where $\mathbf{x}=(x,y)$, the Radon transform $p(s, \theta)$ gives the integral of $f(\mathbf{x})$ along a line defined by its angle $\theta$ and its [perpendicular distance](@entry_id:176279) $s$ from the origin:

$p(s, \theta) = \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} f(x, y) \delta(x\cos\theta + y\sin\theta - s) \,dx\,dy$

Here, $\delta(\cdot)$ is the Dirac delta function, which constrains the integration to the specified line. The set of all such line integrals for $\theta \in [0, \pi)$ and all relevant $s$ values forms a sinogram, which represents the ideal, noise-free data. While the Radon transform provides a powerful theoretical foundation, it is an incomplete description of any real PET acquisition [@problem_id:4908124].

#### A Practical, Discrete Statistical Model

Real-world PET data deviates from the ideal Radon transform in several crucial ways: the measurements are discrete, corrupted by statistical noise, and affected by numerous physical phenomena. A practical forward model must account for these realities.

First, both the image we wish to reconstruct and the data we measure are discrete. The image is represented by a vector $\mathbf{x}$ of size $J$, where each element $x_j$ is the average activity in a small volume element, or **voxel**. The measurement is a vector $\mathbf{y}$ of size $I$, where each element $y_i$ is the number of coincidence events detected in a specific LOR, or sinogram bin, over the acquisition time.

The relationship between the expected activity in the voxels and the expected counts in the LORs is encapsulated by the **system matrix**, $A$. The element $A_{ij}$ of this matrix represents the probability that an [annihilation](@entry_id:159364) event occurring in voxel $j$ is detected as a coincidence in LOR $i$, *excluding the effect of attenuation by the patient*. This matrix is far more than a simple geometric projector; it is a complex physical model that incorporates:

1.  **Geometric Sensitivity**: The [solid angle](@entry_id:154756) subtended by the detector pair for LOR $i$ from the location of voxel $j$. This accounts for the finite size of detector elements and the fact that LORs are better described as "tubes of response" rather than infinitely thin lines [@problem_id:4908124].

2.  **Detector Efficiency and Normalization**: The intrinsic probability of detection for each crystal pair, accounting for variations in crystal properties and other geometric factors.

The expected number of "true" coincidences (those from unscattered photon pairs) in LOR $i$ must also account for **Photon Attenuation**: the probability that both photons from an annihilation travel from the source to their respective detectors without being absorbed or scattered by the patient's body. This is captured by an attenuation factor $a_i$ for each LOR, which can be determined from a separate CT scan. The expected number of true coincidences is the product of this factor and the sum of contributions from all voxels: $a_i \sum_{j=1}^{J} A_{ij} x_j$, or $a_i (A\mathbf{x})_i$ in matrix notation.

However, true coincidences are not the only events recorded. We must also account for background events that do not originate from the correct LOR. The two primary sources are:

-   **Scattered Coincidences ($s$)**: Events where at least one of the two photons undergoes Compton scattering within the patient, changing its direction and causing it to be assigned to an incorrect LOR. The expected number of scattered events in LOR $i$ is denoted by the term $s_i$.

-   **Random Coincidences ($r$)**: Events arising from the near-simultaneous detection of two unrelated photons from different [annihilation](@entry_id:159364) events. The expected number of these events in LOR $i$ is denoted by $r_i$.

These background events are additive. Therefore, the total expected count in LOR $i$, which we denote $\bar{y}_i$, is the sum of the attenuated true, scattered, and random components:

$\bar{y}_i = a_i (A\mathbf{x})_i + s_i + r_i$

Finally, we must model the statistical nature of the measurement. Radioactive decay and photon detection are stochastic quantum processes. The number of events counted in a fixed time interval is well-described by a **Poisson distribution**. Since the true, scattered, and random event streams are independent, their sum is also a Poisson process. Thus, the measured count $y_i$ in each LOR is a random variable drawn from a Poisson distribution with a mean equal to the total expected count $\bar{y}_i$:

$y_i \sim \text{Poisson}(\bar{y}_i)$

This complete statistical [forward model](@entry_id:148443), $y_i \sim \text{Poisson}(a_i(A\mathbf{x})_i + s_i + r_i)$, forms the foundation of modern PET [image reconstruction](@entry_id:166790) [@problem_id:4907976].

### Analytic Reconstruction: Filtered Backprojection

The historically dominant method for [tomographic reconstruction](@entry_id:199351) is **Filtered Backprojection (FBP)**. It provides a direct, non-iterative solution to the inverse problem based on the idealized Radon transform. Understanding FBP reveals key insights into the nature of projection data.

The core of FBP relies on a powerful mathematical result called the **Projection-Slice Theorem**. This theorem states that the one-dimensional Fourier transform of a projection $p(s, \theta)$ at a given angle $\theta$ is identical to a "slice" through the two-dimensional Fourier transform of the original image $f(\mathbf{x})$, taken at the same angle $\theta$ [@problem_id:4908147]. By acquiring projections at all angles from $0$ to $\pi$, one can, in principle, fill the entire 2D Fourier space of the image and then recover the image via a 2D inverse Fourier transform.

A more intuitive, but flawed, approach to reconstruction is simple **[backprojection](@entry_id:746638)**. This operation takes each projection profile and "smears" it back across the image plane along the direction from which it was acquired. Summing the backprojected profiles from all angles produces an image. While this process concentrates intensity at the correct locations, the resulting image, $b(\mathbf{x})$, is severely blurred. This blurring can be shown to be equivalent to convolving the true image $f(\mathbf{x})$ with a [point spread function](@entry_id:160182) (PSF) proportional to $1/r$, where $r$ is the radial distance. This is the characteristic **$1/r$ blur** of unfiltered [backprojection](@entry_id:746638) [@problem_id:4908147].

The Projection-Slice Theorem explains the origin of this blur. The process of [backprojection](@entry_id:746638), when viewed in the frequency domain, acts as a filter that weights the image's Fourier components by $1/\|\mathbf{k}\|$, where $\|\mathbf{k}\|$ is the [spatial frequency](@entry_id:270500) magnitude. This disproportionately amplifies low frequencies and suppresses high frequencies, causing the blur.

To correct this, FBP applies a "filter" to the projection data before backprojecting. To counteract the $1/\|\mathbf{k}\|$ weighting of [backprojection](@entry_id:746638), we must apply a filter that multiplies the data by $\|\mathbf{k}\|$. In the 1D Fourier domain of each projection, where frequency is denoted by $\omega$, this corresponds to a filter with a frequency response of $|\omega|$. This is known as the **[ramp filter](@entry_id:754034)**.

The FBP algorithm is thus:
1.  For each projection angle $\theta$, compute the 1D Fourier transform of the projection data $p(s, \theta)$.
2.  Multiply the result by the [ramp filter](@entry_id:754034), $|\omega|$.
3.  Compute the inverse 1D Fourier transform to obtain the "filtered" projection.
4.  Backproject the filtered projections from all angles to form the final image.

FBP is computationally fast and efficient. However, it is derived from the ideal Radon transform and struggles to accurately incorporate the complex statistics (Poisson noise) and physical effects (scatter, randoms, detector response) that are naturally handled by [iterative methods](@entry_id:139472).

### Iterative Reconstruction: Statistical Approaches

Modern PET reconstruction is dominated by [iterative algorithms](@entry_id:160288) that directly leverage the statistical [forward model](@entry_id:148443), $y_i \sim \text{Poisson}(a_i(A\mathbf{x})_i + s_i + r_i)$. These methods begin with an initial guess for the image $\mathbf{x}^{(0)}$ (e.g., a uniform image) and iteratively refine it to find an image that is most consistent with the measured data $\mathbf{y}$.

#### Maximum Likelihood Expectation-Maximization (ML-EM)

The most fundamental statistical approach is **Maximum Likelihood (ML)** reconstruction. Its goal is to find the image $\mathbf{x}$ that maximizes the likelihood of having observed the measured data $\mathbf{y}$. For Poisson-distributed data, this means maximizing the log-likelihood function:

$L(\mathbf{x}) = \sum_{i=1}^{I} \left( y_i \log(\bar{y}_i) - \bar{y}_i \right)$

where $\bar{y}_i = a_i(A\mathbf{x})_i + s_i + r_i$. Due to the complexity of this function and the non-negativity constraint on $\mathbf{x}$, a direct solution is intractable. The **Expectation-Maximization (EM)** algorithm provides an elegant iterative procedure to find the ML solution. The **ML-EM** update rule for each voxel $j$ from iteration $k$ to $k+1$ is:

$x_j^{(k+1)} = \frac{x_j^{(k)}}{\sum_{i=1}^{I} a_i A_{ij}} \sum_{i=1}^{I} a_i A_{ij} \frac{y_i}{a_i(A\mathbf{x}^{(k)})_i + s_i + r_i}$

This update has a beautiful intuitive interpretation. The term $\frac{y_i}{a_i(A\mathbf{x}^{(k)})_i + s_i + r_i}$ is a correction factor, representing the ratio of measured counts to expected counts for LOR $i$. The inner sum computes a weighted average of these correction factors for all LORs that voxel $j$ contributes to. This average correction factor then multiplicatively updates the current estimate for voxel $j$. ML-EM has the desirable properties of guaranteed non-decreasing likelihood at each iteration and preservation of image non-negativity. However, it converges very slowly.

#### Ordered Subsets Expectation-Maximization (OSEM)

To address the slow convergence of ML-EM, the **Ordered Subsets Expectation-Maximization (OSEM)** algorithm was developed. OSEM accelerates the process by partitioning the projection data (the LORs) into an ordered sequence of $M$ subsets, $S_1, S_2, \ldots, S_M$. Instead of using all the data for one large update, OSEM performs an ML-EM-like update for each subset in sequence, using the result of one update as the starting point for the next [@problem_id:4908010].

The update for the $m$-th subset is:
$x_j^{\text{new}} = \frac{x_j^{\text{old}}}{\sum_{i \in S_m} a_i A_{ij}} \sum_{i \in S_m} a_i A_{ij} \frac{y_i}{a_i(A\mathbf{x}^{\text{old}})_i + s_i + r_i}$

A full pass through all $M$ subsets constitutes one "iteration" of OSEM. By updating the image more frequently, OSEM achieves a dramatic acceleration in early iterations, often providing a visually converged image in a fraction of the time required by ML-EM.

This speed comes at a theoretical cost. Because each subset update pulls the image towards the optimum for only a fraction of the data, the algorithm does not converge to the true ML solution. Instead, it converges to a **limit cycle**, where the image estimate cycles through a set of points near the ML solution. The amplitude of this limit cycle generally increases with the number of subsets $M$ and with the imbalance or correlation between subsets. However, for many clinical applications, the acceleration is so significant that the small sub-optimality is an acceptable trade-off. For research applications requiring convergence, modifications like using a diminishing [relaxation parameter](@entry_id:139937) can restore convergence to the ML solution [@problem_id:4908010].

### Essential Data Corrections

Quantitative PET imaging, where voxel values represent a true measure of tracer concentration, is only possible if the raw data are accurately corrected for various physical degrading effects. Iterative methods are particularly well-suited for incorporating these corrections.

#### Attenuation Correction

Photons traveling through the body can be absorbed or scattered, reducing the number of detected coincidences. This **attenuation** is not uniform; it depends on the length and composition of the tissue traversed by the LOR. Without correction, areas deep within the body or surrounded by dense structures (like bone) will appear artificially "cold".

Modern PET/CT scanners perform attenuation correction using the co-registered CT image. The CT image provides a map of tissue density in **Hounsfield Units (HU)**. To be useful for PET, this HU map must be converted into a map of linear attenuation coefficients at the PET photon energy of 511 keV, denoted $\mu_{511}$. This is achieved using a physically motivated piecewise linear transformation [@problem_id:4907986].

The need for a piecewise function stems from the different ways photons interact with tissue at CT energies (e.g., ~70 keV) versus PET energies (511 keV).
-   At 511 keV, attenuation is dominated by **Compton scattering**, which depends primarily on the electron density of the material.
-   At lower CT energies, the **photoelectric effect** becomes significant, especially in materials with high atomic numbers ($Z$), like the calcium in bone. The [photoelectric effect](@entry_id:138010) has a strong $Z^3$ dependence.

This means that the high HU value of bone is disproportionately "boosted" at CT energies due to the photoelectric effect. A simple [linear scaling](@entry_id:197235) from HU to $\mu_{511}$ would overestimate the attenuation of bone at 511 keV. The [standard solution](@entry_id:183092) is a [bilinear map](@entry_id:150924) with a break-point at the HU value of water (HU=0):
-   For water-like tissues (HU $\le 0$), where the effective atomic number is low, a single slope relates HU to $\mu_{511}$.
-   For denser, bone-like tissues (HU $> 0$), a different, shallower slope is used to account for the energy-dependent behavior.

This derived $\mu_{511}$ map is then used to calculate the attenuation factor $a_i = \exp(-\int_{\text{LOR } i} \mu_{511}(\mathbf{l}) d\mathbf{l})$ for each LOR, which is incorporated into the iterative reconstruction model.

#### Scatter Correction

When a photon scatters in the patient, it changes direction. If the scattered photon is still detected, the event is assigned to an incorrect LOR, adding a low-frequency haze to the projection data that reduces image contrast and quantitative accuracy.

One common method for scatter correction is **convolution-subtraction**. This method models the scatter distribution by convolving an initial estimate of the true, unscattered [sinogram](@entry_id:754926), $t(r)$, with a **scatter kernel**, $k(r)$. This kernel represents the probability distribution of mispositioning due to scatter [@problem_id:4908088].

The shape of the scatter kernel is physically motivated. Single Compton scattering at 511 keV is forward-peaked, leading to a mispositioning distribution that can be approximated by a decaying function, often an exponential. This intrinsic object scatter distribution is further blurred by the finite spatial resolution of the detector system (detector response). Thus, a robust scatter kernel $k(r)$ is modeled as the convolution of an object scatter function (e.g., exponential) and the detector's [point spread function](@entry_id:160182) (e.g., Gaussian).

The scatter estimate is then $s_{\text{est}}(r) = \alpha (k * t)(r)$, where $\alpha$ is a scaling factor. This factor is determined by fitting the estimated scatter profile to the measured projection data in the regions outside the patient (the "tails" of the [sinogram](@entry_id:754926)), where the signal is known to be composed almost entirely of scatter and randoms. By minimizing the difference between $s_{\text{est}}(r)$ and the measured data in these tails, the correct scatter fraction $\alpha$ can be found. The final estimated scatter [sinogram](@entry_id:754926) is then subtracted from the measured data or, more appropriately, included as the term $s_i$ in an iterative reconstruction model.

#### Randoms Correction

Random coincidences occur when two photons from separate annihilations happen to strike detectors within the same short coincidence timing window (e.g., a few nanoseconds). The rate of randoms increases with the overall activity in the [field of view](@entry_id:175690) and degrades the [signal-to-noise ratio](@entry_id:271196).

A robust method for measuring the randoms contribution is the **delayed-[window method](@entry_id:270057)**. In addition to the standard "prompt" coincidence window, the scanner hardware implements a second, "delayed" window. One detector's signal is electronically delayed by a time much longer than the timing window width. Any coincidences registered in this delayed stream cannot be from the same annihilation event and are therefore purely random.

This provides a direct, LOR-by-LOR measurement of the randoms distribution, $D$. The simplest way to correct for randoms is to subtract this measurement from the prompt measurement, $P$, to get an estimate of the true counts: $\hat{T} = P - D$.

While this subtraction yields an unbiased estimate of the true counts, it comes at a statistical cost. Both $P$ and $D$ are independent Poisson measurements. The variance of a sum or difference of [independent random variables](@entry_id:273896) is the sum of their variances. Let the mean true rate be $\lambda_T$ and the mean randoms rate be $\lambda_R$.
-   Variance of the prompt measurement: $\text{Var}(P) = \lambda_T + \lambda_R$
-   Variance of the delayed measurement: $\text{Var}(D) = \lambda_R$
-   Variance of the corrected estimate: $\text{Var}(\hat{T}) = \text{Var}(P) + \text{Var}(D) = (\lambda_T + \lambda_R) + \lambda_R = \lambda_T + 2\lambda_R$

The act of subtracting the noisy randoms measurement increases the total variance of the data, a phenomenon known as **[noise propagation](@entry_id:266175)**. This highlights a key principle: every correction step based on a noisy measurement adds noise to the final result [@problem_id:4908156].

### Advanced Reconstruction Models

For the highest quantitative accuracy, reconstruction algorithms can be enhanced with even more sophisticated physical models.

#### Modeling the Shift-Variant System Response

The system matrix $A$ implicitly contains the scanner's **Point Spread Function (PSF)**, which describes the blurring inherent in the detection process. In a simple model, this PSF is assumed to be the same everywhere in the image (shift-invariant). In reality, the PET PSF is significantly **shift-variant**, meaning its shape and size change depending on the position in the [field of view](@entry_id:175690).

A major cause of this shift-variance is **parallax error**, which arises from the unknown **Depth-of-Interaction (DOI)** of the photon within the detector crystal [@problem_id:4908077]. For an [annihilation](@entry_id:159364) at the scanner's center, photons strike the detectors at a normal angle, and the unknown DOI does not displace the LOR. For an off-center [annihilation](@entry_id:159364), however, photons strike the detectors at an oblique angle. An interaction deep within the crystal will be assigned to the LOR of the crystal face, introducing a positioning error. The magnitude of this error depends on the [angle of incidence](@entry_id:192705), which increases with the source's radial distance from the center.

By modeling the geometry of the scanner ring (radius $R$, crystal thickness $T$) and the trigonometry of the incidence angle, one can derive an expression for the DOI-induced blur, $\sigma_{DOI}(r)$, as a function of radial position $r$. A common result shows that this blur is proportional to $\frac{r}{\sqrt{R^2 - r^2}}$. The total PSF width $\sigma(r)$ is then the combination of this position-dependent blur and a baseline, position-independent blur $\sigma_0$ (from factors like positron range and non-[collinearity](@entry_id:163574)), typically added in quadrature:

$\sigma(r) = \sqrt{\sigma_0^2 + \sigma_{DOI}^2(r)}$

Incorporating this shift-variant PSF model into the system matrix $A$ during iterative reconstruction can significantly improve spatial resolution, especially towards the edges of the [field of view](@entry_id:175690).

#### Regularization: Maximum a Posteriori (MAP) Reconstruction

A key challenge with ML-EM reconstruction is that as the algorithm iterates to fit the data more closely, it also amplifies the Poisson noise present in the measurements. The resulting images can become unacceptably noisy. **Maximum a Posteriori (MAP)** reconstruction addresses this by incorporating a **prior** belief about the nature of the true image.

MAP modifies the objective function by adding a regularization term (or penalty term) that penalizes images with undesirable characteristics, such as excessive roughness. The new objective is:

$Q(\mathbf{x}) = L(\mathbf{x}) - \beta U(\mathbf{x})$

where $L(\mathbf{x})$ is the log-likelihood, $U(\mathbf{x})$ is the [penalty function](@entry_id:638029), and $\beta$ is a [regularization parameter](@entry_id:162917) that controls the trade-off between fitting the data and adhering to the prior.

A common choice for the [penalty function](@entry_id:638029) is to penalize the differences between neighboring voxels. The choice of the specific [penalty function](@entry_id:638029) $\rho(t)$ on a difference $t = |x_p - x_q|$ has a profound impact on the final image properties [@problem_id:4907987]. We can analyze this by examining the derivative of the penalty, $\psi(t) = \rho'(t)$, which acts as an "influence function" determining the strength of the penalty for a given difference.

-   **Quadratic Penalty**: $\rho(t) \propto t^2$. The influence function is $\psi(t) \propto t$. This penalty grows without bound for large differences. While effective at smoothing small noise-induced oscillations, it also heavily penalizes the large differences that constitute anatomical edges, leading to blurred images.

-   **Total Variation (TV) Penalty**: $\rho(t) \propto |t|$. The [influence function](@entry_id:168646) is $\psi(t) \propto \text{sign}(t)$, a constant magnitude. Because the penalty's influence saturates, it allows large intensity jumps to exist, thereby preserving sharp edges. However, its constant influence even for small differences can be overly aggressive, sometimes creating "blocky" or "staircase" artifacts.

-   **Huber Penalty**: This is a hybrid that is quadratic for small differences ($|t| \le \delta$) and linear for large differences ($|t| > \delta$). Its [influence function](@entry_id:168646) $\psi(t)$ grows linearly up to a threshold $\delta$ and then becomes constant. It thus combines the nice noise-smoothing properties of the [quadratic penalty](@entry_id:637777) for small variations with the edge-preserving property of the TV penalty for large variations, offering a powerful compromise.

By selecting an appropriate [penalty function](@entry_id:638029) and tuning the parameter $\beta$, MAP reconstruction can produce images with substantially lower noise than ML-EM while preserving important structural details.

### Integrating Corrections: A Unified View

We have discussed a series of corrections for attenuation, scatter, and randoms. A fundamental question in reconstruction design is *how* to apply these corrections. Two philosophies exist:

1.  **Pre-correction**: The raw data $y_i$ is "corrected" before reconstruction. For example, one could compute $y_i'' = (y_i - r_i - s_i) / a_i$ and then reconstruct an image from this corrected data $y_i''$ using a simpler forward model.

2.  **In-reconstruction Modeling**: The full physical model, including the terms for attenuation, scatter, and randoms, is incorporated directly into the forward model $\bar{y}_i = a_i(A\mathbf{x})_i + s_i + r_i$ used within an iterative algorithm like OSEM.

While pre-correction is simpler to implement, it is statistically suboptimal. The reason can be understood by examining the noise properties. When we perform operations like subtraction and division on the noisy data $y_i$, we alter its variance. For the two approaches to be equivalent, the statistical weights used in the reconstruction algorithm must be correctly adjusted to reflect the new variance of the pre-corrected data [@problem_id:4907916].

For example, in a Weighted Least Squares (WLS) framework, if we transform the data $y_i$ to $y_i'' = (y_i - r_i - s_i) / a_i$, the variance transforms as $\text{Var}(y_i'') \approx \text{Var}(y_i) / a_i^2$ (assuming $r_i$ and $s_i$ are noiseless constants). Therefore, the weighting for the pre-corrected data, $w_i''$, must be related to the original weighting $w_i$ by $w_i'' = w_i a_i^2$. If this re-weighting is not performed, the algorithm will be statistically inefficient. More importantly, if the correction terms $r_i$ and $s_i$ are themselves noisy estimates (which they always are in practice), the pre-subtraction introduces additional noise that is very difficult to model correctly.

For these reasons, the modern and most accurate approach is to incorporate all physical effects and corrections directly into the [forward model](@entry_id:148443) of a statistical iterative reconstruction algorithm. This allows the algorithm to correctly account for the Poisson nature of the raw data and provides a unified, principled framework for producing the most quantitatively accurate images possible from PET data.