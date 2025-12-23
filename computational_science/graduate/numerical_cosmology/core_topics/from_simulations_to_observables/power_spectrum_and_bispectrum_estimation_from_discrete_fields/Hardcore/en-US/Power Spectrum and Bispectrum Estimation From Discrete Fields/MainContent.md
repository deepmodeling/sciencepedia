## Introduction
The [power spectrum](@entry_id:159996) and [bispectrum](@entry_id:158545) are cornerstone statistics in cosmology, providing a quantitative description of the cosmic web and a vital link between theory and observation. While their theoretical definitions in a continuous, infinite universe are elegant, their practical application requires confronting the realities of data: discrete tracers sampled within a finite volume. This transition from abstract theory to numerical practice introduces a host of systematic effects and computational challenges that must be meticulously understood and addressed to extract reliable cosmological information. This article bridges this critical gap, providing a detailed framework for estimating the power spectrum and bispectrum from discrete fields.

This guide is structured to lead you from foundational concepts to advanced applications. The first chapter, **Principles and Mechanisms**, establishes the mathematical formalism of discrete Fourier analysis and derives the estimators for the [power spectrum](@entry_id:159996) and [bispectrum](@entry_id:158545). It carefully dissects the origin and impact of systematic effects like [mass assignment](@entry_id:751704), [shot noise](@entry_id:140025), and aliasing. Following this, the **Applications and Interdisciplinary Connections** chapter demonstrates how these statistical tools are used to probe cosmic structure, measure [redshift-space distortions](@entry_id:157636), test advanced gravitational theories, and disentangle complex baryonic physics, while also touching on connections to signal processing and computer science. Finally, the **Hands-On Practices** section offers practical exercises designed to solidify your understanding of the core concepts, from counting Fourier modes to implementing estimators for anisotropic signals. By the end, you will have a robust understanding of how to turn raw simulation or survey data into precise cosmological measurements.

## Principles and Mechanisms

In the study of large-scale structure, the power spectrum and bispectrum are indispensable statistical tools. They quantify the two- and three-point correlation properties of cosmological density fields in Fourier space, providing a powerful link between theoretical models and observational or simulation data. However, moving from the continuous, infinite-volume definitions of theory to practical estimation from discrete fields within a [finite volume](@entry_id:749401) introduces a number of critical subtleties. This chapter elucidates the fundamental principles governing these statistics and the mechanisms of their estimation, bridging the gap between abstract theory and numerical application.

### From Continuous Fields to Discrete Fourier Modes

Cosmological fields, such as the matter [density contrast](@entry_id:157948) $\delta(\boldsymbol{x})$, are continuous functions of position. However, both N-body simulations and galaxy surveys provide information at discrete locations within a finite volume. To analyze such data, we must first establish a consistent mathematical framework for discrete Fourier analysis.

Consider a continuous, real-valued field $\delta(\boldsymbol{x})$ within a periodic cubic box of side length $L$ and volume $V = L^3$. The assumption of [periodicity](@entry_id:152486) is a crucial simplification that discretizes the allowed Fourier wavevectors. Any periodic function can be represented by a Fourier series, not a Fourier transform. The allowed wavevectors are those that are commensurate with the box size, forming a discrete lattice in Fourier space:
$$
\boldsymbol{k}_{\boldsymbol{m}} = \frac{2\pi}{L} \boldsymbol{m}
$$
where $\boldsymbol{m} = (m_x, m_y, m_z)$ is a triplet of integers.

The Fourier [series representation](@entry_id:175860) of the field is given by the pair:
$$
\tilde{\delta}(\boldsymbol{k}_{\boldsymbol{m}}) = \int_V d^3x \, \delta(\boldsymbol{x}) e^{-i \boldsymbol{k}_{\boldsymbol{m}} \cdot \boldsymbol{x}}
$$
$$
\delta(\boldsymbol{x}) = \frac{1}{V} \sum_{\boldsymbol{m}} \tilde{\delta}(\boldsymbol{k}_{\boldsymbol{m}}) e^{i \boldsymbol{k}_{\boldsymbol{m}} \cdot \boldsymbol{x}}
$$
This convention must be carefully distinguished from the infinite-volume Fourier transform pair, which involves an integral over all $\boldsymbol{k}$-space with a factor of $(2\pi)^{-3}$ and relies on the Dirac delta function, $\delta_{\mathrm{D}}^{(3)}(\boldsymbol{k})$, for orthogonality. In our finite periodic volume, orthogonality is governed by the Kronecker delta, $\delta^K_{\boldsymbol{m}\boldsymbol{n}}$:
$$
\int_V d^3x \, e^{i (\boldsymbol{k}_{\boldsymbol{m}} - \boldsymbol{k}_{\boldsymbol{n}}) \cdot \boldsymbol{x}} = V \delta^K_{\boldsymbol{m}\boldsymbol{n}}
$$

In practice, the field is often sampled on a regular Cartesian grid with $N^3$ points and a grid spacing $a = L/N$. The [density contrast](@entry_id:157948) at a grid point $\boldsymbol{x}_{\boldsymbol{j}} = a\boldsymbol{j}$ is denoted $\delta_{\boldsymbol{j}}$. The integral in the forward Fourier transform is then approximated by a Riemann sum over the grid cells, each of volume $a^3$:
$$
\tilde{\delta}(\boldsymbol{k}_{\boldsymbol{m}}) \approx \sum_{\boldsymbol{j}} \delta_{\boldsymbol{j}} e^{-i \boldsymbol{k}_{\boldsymbol{m}} \cdot \boldsymbol{x}_{\boldsymbol{j}}} (a^3)
$$
This leads to the standard Discrete Fourier Transform (DFT) pair used in [numerical cosmology](@entry_id:752779) . The forward transform (often computed via a Fast Fourier Transform, or FFT, algorithm) relates the [real-space](@entry_id:754128) grid values $\delta_{\boldsymbol{j}}$ to the Fourier-space coefficients $\tilde{\delta}_{\boldsymbol{m}}$:
$$
\tilde{\delta}_{\boldsymbol{m}} = a^3 \sum_{\boldsymbol{j}} \delta_{\boldsymbol{j}} e^{-i \boldsymbol{k}_{\boldsymbol{m}} \cdot \boldsymbol{x}_{\boldsymbol{j}}}
$$
$$
\delta_{\boldsymbol{j}} = \frac{1}{V} \sum_{\boldsymbol{m}} \tilde{\delta}_{\boldsymbol{m}} e^{i \boldsymbol{k}_{\boldsymbol{m}} \cdot \boldsymbol{x}_{\boldsymbol{j}}}
$$
The sum over $\boldsymbol{m}$ is typically performed over the $N^3$ wavevectors in the fundamental Brillouin zone. The [density contrast](@entry_id:157948) is defined as $\delta_{\boldsymbol{j}} = \rho_{\boldsymbol{j}}/\bar{\rho} - 1$, where $\rho_{\boldsymbol{j}}$ is the density at grid cell $\boldsymbol{j}$ and $\bar{\rho}$ is the mean density in the entire box. By this definition, the field has a [zero mean](@entry_id:271600) over the box, which implies that the [zero-frequency mode](@entry_id:166697) (the "DC component") must vanish: $\tilde{\delta}_{\boldsymbol{m}=\boldsymbol{0}} = a^3 \sum_{\boldsymbol{j}} \delta_{\boldsymbol{j}} = 0$.

### The Power Spectrum: Definition and Properties

The power spectrum, $P(\boldsymbol{k})$, is the fundamental descriptor of two-point clustering. It is formally defined as the Fourier transform of the [two-point correlation function](@entry_id:185074), $\xi(\boldsymbol{r}) = \langle \delta(\boldsymbol{x})\delta(\boldsymbol{x}+\boldsymbol{r}) \rangle$. For a statistically homogeneous field, the correlations depend only on the separation vector $\boldsymbol{r}$, not on the absolute position $\boldsymbol{x}$. This property has a profound consequence in Fourier space.

Let us compute the two-point correlator of the Fourier modes in our periodic box. Using the definitions above and the property of [statistical homogeneity](@entry_id:136481):
$$
\langle \tilde{\delta}(\boldsymbol{k}) \tilde{\delta}^*(\boldsymbol{k}') \rangle = \int_V d^3x \int_V d^3x' \, e^{-i\boldsymbol{k}\cdot\boldsymbol{x} + i\boldsymbol{k}'\cdot\boldsymbol{x}'} \langle \delta(\boldsymbol{x})\delta(\boldsymbol{x}') \rangle
$$
$$
= \int_V d^3x \int_V d^3x' \, e^{-i\boldsymbol{k}\cdot\boldsymbol{x} + i\boldsymbol{k}'\cdot\boldsymbol{x}'} \xi(\boldsymbol{x}'-\boldsymbol{x})
$$
By changing variables to $\boldsymbol{r} = \boldsymbol{x}' - \boldsymbol{x}$, the expression separates into two integrals:
$$
= \left( \int_V d^3x \, e^{i(\boldsymbol{k}'-\boldsymbol{k})\cdot\boldsymbol{x}} \right) \left( \int_V d^3r \, e^{i\boldsymbol{k}'\cdot\boldsymbol{r}} \xi(\boldsymbol{r}) \right)
$$
The [first integral](@entry_id:274642) enforces orthogonality, yielding $V \delta^K_{\boldsymbol{k}\boldsymbol{k}'}$. The second integral, assuming the [correlation length](@entry_id:143364) is much smaller than the box size $L$, approximates the Fourier transform of $\xi(\boldsymbol{r})$, which is the [power spectrum](@entry_id:159996) $P(\boldsymbol{k}')$. This leads to the central relation for the power spectrum in a periodic volume  :
$$
\langle \tilde{\delta}(\boldsymbol{k}) \tilde{\delta}^*(\boldsymbol{k}') \rangle = V P(\boldsymbol{k}) \delta^K_{\boldsymbol{k}\boldsymbol{k}'}
$$
This equation reveals that **[statistical homogeneity](@entry_id:136481)** implies that different Fourier modes are uncorrelated. The entire two-point statistical content of the field is contained in the variance of each mode, which is proportional to the power spectrum $P(\boldsymbol{k})$.

If the field is also **statistically isotropic**, the statistics are invariant under rotations. This means the correlation function depends only on the distance $r=|\boldsymbol{r}|$, and consequently, the power spectrum depends only on the wavenumber $k=|\boldsymbol{k}|$ . The power spectrum simplifies from a function of a vector, $P(\boldsymbol{k})$, to a function of a scalar, $P(k)$.

From the relation above, the units of the power spectrum can be deduced. With our Fourier convention, $\tilde{\delta}(\boldsymbol{k})$ has units of [$\delta$] $\times$ Volume. Since $\delta$ is dimensionless, $[\tilde{\delta}] = L^3$. Therefore, the [power spectrum](@entry_id:159996) $P(k)$ must have units of Volume to make the equation dimensionally consistent:
$$
[L^3]^2 = [L^3] [P(k)] \implies [P(k)] = L^3
$$
This is a critical consistency check for any [power spectrum](@entry_id:159996) estimator .

The concept can be extended to two different fields, $\delta_a$ and $\delta_b$, to define the **cross-[power spectrum](@entry_id:159996)** $P_{ab}(k)$. The governing relation is analogous:
$$
\langle \tilde{\delta}_a(\boldsymbol{k}) \tilde{\delta}_b^*(\boldsymbol{k}') \rangle = V P_{ab}(\boldsymbol{k}) \delta^K_{\boldsymbol{k}\boldsymbol{k}'}
$$
In general, the cross-power spectrum can be complex, and it obeys the symmetry relation $P_{ba}(\boldsymbol{k}) = P_{ab}^*(\boldsymbol{k})$. If the underlying statistics are parity-invariant and both fields are scalars (or both are pseudoscalars), then $P_{ab}(\boldsymbol{k})$ will be a real-valued function, in which case $P_{ab}(\boldsymbol{k}) = P_{ba}(\boldsymbol{k})$ .

### The Bispectrum: Probing Non-Gaussianity

While the power spectrum provides a complete statistical description of a Gaussian [random field](@entry_id:268702), cosmological density fields develop non-Gaussian features under gravitational evolution. These are captured by [higher-order statistics](@entry_id:193349), the simplest of which is the bispectrum.

The [bispectrum](@entry_id:158545), $B(\boldsymbol{k}_1, \boldsymbol{k}_2, \boldsymbol{k}_3)$, is the Fourier transform of the three-point [correlation function](@entry_id:137198), $\zeta(\boldsymbol{r}_1, \boldsymbol{r}_2) = \langle \delta(\boldsymbol{x})\delta(\boldsymbol{x}+\boldsymbol{r}_1)\delta(\boldsymbol{x}+\boldsymbol{r}_2) \rangle$. Following a derivation analogous to that for the [power spectrum](@entry_id:159996), we can find the three-point correlator of Fourier modes :
$$
\langle \tilde{\delta}(\boldsymbol{k}_1) \tilde{\delta}(\boldsymbol{k}_2) \tilde{\delta}(\boldsymbol{k}_3) \rangle = \int_V \!d^3x_1 \! \int_V \!d^3x_2 \! \int_V \!d^3x_3 \, e^{-i(\boldsymbol{k}_1\cdot\boldsymbol{x}_1+\boldsymbol{k}_2\cdot\boldsymbol{x}_2+\boldsymbol{k}_3\cdot\boldsymbol{x}_3)} \langle \delta(\boldsymbol{x}_1)\delta(\boldsymbol{x}_2)\delta(\boldsymbol{x}_3) \rangle
$$
Statistical homogeneity allows us to express the correlation in terms of separation vectors, which causes the integral to factorize:
$$
= \left( \int_V d^3x \, e^{-i(\boldsymbol{k}_1+\boldsymbol{k}_2+\boldsymbol{k}_3)\cdot\boldsymbol{x}} \right) \left( \dots \right)
$$
The [first integral](@entry_id:274642) yields $V \delta^K_{\boldsymbol{k}_1+\boldsymbol{k}_2+\boldsymbol{k}_3, \boldsymbol{0}}$, while the remaining terms define the bispectrum. This gives the fundamental relation for the bispectrum:
$$
\langle \tilde{\delta}(\boldsymbol{k}_1) \tilde{\delta}(\boldsymbol{k}_2) \tilde{\delta}(\boldsymbol{k}_3) \rangle = V B(\boldsymbol{k}_1, \boldsymbol{k}_2, \boldsymbol{k}_3) \delta^K_{\boldsymbol{k}_1+\boldsymbol{k}_2+\boldsymbol{k}_3, \boldsymbol{0}}
$$
This shows that the three-point correlator of Fourier modes is non-zero only for triplets of wavevectors that form a closed triangle, $\boldsymbol{k}_1+\boldsymbol{k}_2+\boldsymbol{k}_3 = \boldsymbol{0}$. This **triangle closure condition** is a direct and powerful consequence of [statistical homogeneity](@entry_id:136481). The [bispectrum](@entry_id:158545) $B$ contains the amplitude and shape information for these correlated triangles, providing a rich probe of non-Gaussianity. Following our unit conventions, the [bispectrum](@entry_id:158545) has units of $(\text{Volume})^2$, or $L^6$ .

### Practical Estimation from Discrete Data

The theoretical relations above form the foundation for practical estimation. However, turning discrete, finite data into a reliable estimate of the [power spectrum](@entry_id:159996) or [bispectrum](@entry_id:158545) requires accounting for several systematic effects introduced by the measurement process itself.

#### Mass Assignment and Window Functions

In simulations or surveys, the density field is initially represented by a collection of discrete objects (particles or galaxies). To compute a DFT, this distribution must be interpolated onto a regular grid. This process is known as **[mass assignment](@entry_id:751704)**. Common schemes include:
*   **Nearest Grid Point (NGP):** All the mass of a particle is assigned to the single nearest grid cell.
*   **Cloud-in-Cell (CIC):** A particle's mass is distributed bilinearly among the 4 (in 2D) or 8 (in 3D) surrounding grid cells.
*   **Triangular-Shaped Cloud (TSC):** A particle's mass is distributed via a higher-order quadratic scheme to the 9 (in 2D) or 27 (in 3D) surrounding cells.

Mathematically, these schemes are equivalent to convolving the underlying true density field with a kernel function before sampling on the grid. By the convolution theorem, this corresponds to multiplying the Fourier modes of the field by the Fourier transform of the kernel, known as the **[mass assignment](@entry_id:751704) [window function](@entry_id:158702)**, $W(\boldsymbol{k})$. For the standard schemes, which are separable along the Cartesian axes, the 3D window is a product of 1D windows: $W(\boldsymbol{k}) = W(k_x)W(k_y)W(k_z)$. These 1D [window functions](@entry_id:201148) can be derived by recognizing that CIC is a self-convolution of the NGP kernel (a top-hat), and TSC is a convolution of the CIC kernel with an NGP kernel . This leads to:
$$
W_{\text{NGP}}(k) = \operatorname{sinc}(k a/2)
$$
$$
W_{\text{CIC}}(k) = \operatorname{sinc}^2(k a/2)
$$
$$
W_{\text{TSC}}(k) = \operatorname{sinc}^3(k a/2)
$$
where $a$ is the grid spacing and $\operatorname{sinc}(x) \equiv \sin(x)/x$. This window function suppresses power, especially at high $k$. The measured power spectrum is proportional to $|W(\boldsymbol{k})|^2 P(k)$, so any accurate estimate must correct for this effect by dividing the raw measured power by $|W(\boldsymbol{k})|^2$.

#### Shot Noise from Discrete Tracers

Representing a continuous density field with a finite number of discrete tracers introduces a stochastic uncertainty known as **shot noise**. This is a fundamental consequence of sampling. For a set of tracers that form a Poisson point process with mean [number density](@entry_id:268986) $\bar{n}$, the measured [power spectrum](@entry_id:159996) acquires an additive, scale-independent bias . This can be seen by calculating the [expectation value](@entry_id:150961) of the squared Fourier modes, which splits into a "self-correlation" part (from each particle correlating with itself) and a "[cross-correlation](@entry_id:143353)" part (from distinct particles). The self-correlation term is responsible for the [shot noise](@entry_id:140025). The result is:
$$
P_{\text{measured}}(k) = P_{\text{true}}(k) + \frac{1}{\bar{n}}
$$
This constant term, $P_{\text{shot}} = 1/\bar{n}$, must be subtracted from the measured [power spectrum](@entry_id:159996) to obtain an unbiased estimate of the underlying clustering signal.

#### Aliasing from Grid Sampling

The act of sampling a continuous field only at discrete grid points with spacing $a$ fundamentally limits the information that can be recovered. Any wave present in the continuous field with a frequency higher than the **Nyquist frequency**, $k_{\text{Ny}} = \pi/a$, cannot be properly resolved. Instead, its power is "folded" or "aliased" into the range of resolvable frequencies, $|k| \le k_{\text{Ny}}$.

This phenomenon can be understood by modeling the sampling process as multiplying the continuous field by a Dirac comb in real space. In Fourier space, this corresponds to convolving the true spectrum with another Dirac comb, creating infinite periodic replicas of the true spectrum spaced by $2 k_{\text{Ny}}$. The DFT only measures power within the [fundamental domain](@entry_id:201756) (the first Brillouin zone). The power it measures at a given $\boldsymbol{k}$ is thus the sum of the true power at $\boldsymbol{k}$ plus the power from all its aliases at $\boldsymbol{k} \pm 2n \boldsymbol{k}_{\text{Ny}}$. Aliasing is therefore a form of contamination from unresolved small-scale power, and its magnitude is controlled by the grid spacing $a$ .

#### Finite-Volume Effects and the Integral Constraint

In addition to effects from discreteness, the finite size of the simulation or survey volume introduces its own systematic effects. Observing a field only within a volume $V$ is equivalent to multiplying the true, infinite-universe field by a [window function](@entry_id:158702). This windowing in real space corresponds to a convolution in Fourier space, which mixes power between adjacent modes and discretizes the observable wavenumbers (with [fundamental mode](@entry_id:165201) $k_f = 2\pi/L$). This effect, often called [cosmic variance](@entry_id:159935) on large scales, is distinct from aliasing .

A more subtle finite-volume effect is the **integral constraint** . While the true cosmic mean overdensity is zero by definition, the mean overdensity within any finite survey volume, $\bar{\delta}_W$, will fluctuate and generally be non-zero. Since the true mean is unknown, a standard practice is to subtract this sample mean from the data before analysis, enforcing that the mean within the survey is zero. This subtraction preferentially removes power from long-wavelength modes (with $k \lesssim 1/L$) that contribute most to the sample mean. The result is a systematic suppression, or negative bias, in the estimated [power spectrum](@entry_id:159996) at the largest observable scales.

### A Unified Estimator

Combining these principles, we can construct a unified practical estimator for the [power spectrum](@entry_id:159996) from a gridded [density contrast](@entry_id:157948) field, $\delta_{\boldsymbol{j}}$, derived from a set of discrete tracers.

1.  **Compute Fourier Modes:** Calculate the raw DFT coefficients, often using an FFT algorithm. Let's call the output $C(\boldsymbol{k}_{\boldsymbol{m}})$.

2.  **Normalize:** Convert the raw DFT output to continuum-normalized Fourier modes, $\tilde{\delta}(\boldsymbol{k}_{\boldsymbol{m}})$, by multiplying by the grid cell volume: $\tilde{\delta}(\boldsymbol{k}_{\boldsymbol{m}}) = a^3 C(\boldsymbol{k}_{\boldsymbol{m}})$.

3.  **Calculate Raw Power:** Compute the raw power for each mode, $P_{\text{raw}}(\boldsymbol{k}_{\boldsymbol{m}}) = \frac{1}{V} |\tilde{\delta}(\boldsymbol{k}_{\boldsymbol{m}})|^2$.

4.  **Shell Average:** Average the raw power over all modes within thin spherical shells in $k$-space to obtain an isotropic estimate, $\hat{P}_{\text{raw}}(k)$.

5.  **Apply Corrections:** Apply the necessary corrections for windowing and [shot noise](@entry_id:140025) to obtain the final, [unbiased estimator](@entry_id:166722) :
    $$
    \hat{P}(k) = \frac{\hat{P}_{\text{raw}}(k)}{|W(k)|^2} - \frac{1}{\bar{n}}
    $$
    Here, $|W(k)|^2$ is the angle-averaged [mass assignment](@entry_id:751704) window function for the chosen scheme, and $1/\bar{n}$ is the Poisson [shot noise](@entry_id:140025) term. This final estimator, while still subject to aliasing and [finite-volume effects](@entry_id:749371), accounts for the most direct biases introduced by the measurement process.