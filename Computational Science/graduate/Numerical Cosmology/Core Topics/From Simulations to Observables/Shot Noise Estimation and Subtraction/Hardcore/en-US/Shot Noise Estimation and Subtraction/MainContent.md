## Introduction
In modern cosmology, the distribution of galaxies and [dark matter halos](@entry_id:147523) acts as a discrete set of tracers for the underlying continuous matter density field. The process of sampling this field with a finite number of points inevitably introduces a fundamental statistical uncertainty known as **[shot noise](@entry_id:140025)**. This noise floor presents a primary challenge to precision measurements of cosmic structure, particularly on small scales where the cosmological signal is weak. While a simple correction exists for an idealized Poisson distribution of tracers, its application is fraught with complications in real-world scenarios. Addressing the gap between this simple model and the demands of professional analysis requires a deeper understanding of how shot noise interacts with numerical methods, complex survey properties, and the intricate physics of galaxy formation.

This article provides a systematic guide to estimating and subtracting [shot noise](@entry_id:140025) in [large-scale structure](@entry_id:158990) analysis. The journey begins in the "Principles and Mechanisms" chapter, which builds the concept from its statistical origins in Poisson point processes, explores the impact of numerical estimation techniques like [mass assignment](@entry_id:751704), and culminates in the modern Effective Field Theory (EFTofLSS) perspective that reframes shot noise as a fundamental parameter of the model. Following this, the "Applications and Interdisciplinary Connections" chapter demonstrates how shot noise influences advanced cosmological analyses, revealing its complex interplay with Redshift-Space Distortions, BAO reconstruction, and tomographic measurements. Finally, the "Hands-On Practices" section offers concrete exercises to diagnose and manage [shot noise](@entry_id:140025) contributions, preparing the reader to tackle these challenges in practical research settings.

## Principles and Mechanisms

In the study of large-scale structure, our primary tracers—galaxies, [quasars](@entry_id:159221), and dark matter halos in simulations—are discrete entities. However, the theoretical framework of cosmology is built upon continuous fields, such as the matter [density contrast](@entry_id:157948) $\delta(\mathbf{x})$. The act of using a finite number of discrete points to probe an underlying continuous field inevitably introduces a specific form of sampling uncertainty known as **[shot noise](@entry_id:140025)**. This chapter elucidates the principles governing shot noise, from its idealized statistical origin to the complex interplay with numerical methods and the physical nuances of galaxy formation, culminating in the modern [effective field theory](@entry_id:145328) perspective that reframes it as a parameter of fundamental theoretical importance.

### The Idealized Model: Poisson Shot Noise

The simplest and most fundamental model for the distribution of cosmic tracers is to assume they form a **Poisson point process**. In this picture, the probability of finding a tracer in an infinitesimal volume $dV$ is independent of the presence of tracers in any other disjoint volume. If the underlying continuous field from which these tracers are drawn is homogeneous with a mean [number density](@entry_id:268986) $\bar{n}$, the resulting discrete density field can be described as a set of Dirac delta functions located at the tracer positions $\mathbf{x}_i$:

$n(\mathbf{x}) = \sum_i \delta_D(\mathbf{x} - \mathbf{x}_i)$

The overdensity field of these tracers, $\delta_g(\mathbf{x})$, is defined relative to the mean density: $\delta_g(\mathbf{x}) = n(\mathbf{x}) / \bar{n} - 1$. The [power spectrum](@entry_id:159996) of this tracer field, $P_{gg}(k)$, is the Fourier transform of its [two-point correlation function](@entry_id:185074). A first-principles derivation reveals that the measured power spectrum is the sum of two distinct components:

$P_{gg}(k) = P_{\text{clust}}(k) + P_{\text{shot}}$

Here, $P_{\text{clust}}(k)$ is the true [power spectrum](@entry_id:159996) of the underlying continuous field that we wish to measure, reflecting the intrinsic clustering of matter. The second term, $P_{\text{shot}}$, is the shot noise contribution. For an ideal Poisson process, this term is a constant, or "[white noise](@entry_id:145248)," spectrum given by the inverse of the mean [number density](@entry_id:268986) ():

$$P_{\text{shot}} = \frac{1}{\bar{n}}$$

This relation is a cornerstone of [large-scale structure](@entry_id:158990) analysis. It originates from the self-correlation of each individual tracer, which contributes a constant power across all Fourier modes. The physical implication is that [shot noise](@entry_id:140025) is scale-independent, while the clustering signal, $P_{\text{clust}}(k)$, typically decreases with increasing [wavenumber](@entry_id:172452) $k$. Consequently, there will always be a scale at which the shot noise equals or exceeds the clustering signal. For instance, given a tracer sample with $\bar{n} = 5 \times 10^{-4} \, h^3\mathrm{Mpc}^{-3}$ and a clustering spectrum approximated by $P(k) = 10^4 (k / (0.1 \, h\,\mathrm{Mpc}^{-1}))^{-1.5} \, h^{-3}\mathrm{Mpc}^3$, the shot noise level is $P_{\text{shot}} = 1/\bar{n} = 2000 \, h^{-3}\mathrm{Mpc}^3$. Equating this to $P(k)$ allows us to find the wavenumber $k \approx 0.292 \, h\,\mathrm{Mpc}^{-1}$ where the signal-to-noise ratio becomes unity (). Beyond this [wavenumber](@entry_id:172452), the measurement is dominated by [shot noise](@entry_id:140025), fundamentally limiting the precision of clustering measurements on small scales.

### A Model-Independent Approach: The Split-Sample Cross-Spectrum

The canonical [shot noise subtraction](@entry_id:754804), $P_{\text{clust}}(k) = P_{gg}(k) - 1/\bar{n}$, relies on the assumption of Poisson sampling. A powerful technique exists to measure the clustering power spectrum without making any assumptions about the nature of the shot noise: the **split-sample cross-spectrum** method ().

The procedure involves randomly dividing the full tracer catalog into two disjoint sub-samples, let's call them A and B. The overdensity fields for each sub-sample, $\delta_A(\mathbf{k})$ and $\delta_B(\mathbf{k})$, are then computed. Instead of calculating the auto-power spectrum of either sub-sample (which would contain its own [shot noise](@entry_id:140025)), one computes their **cross-[power spectrum](@entry_id:159996)**:

$$P_{\times}(k) = \langle \Re\{\delta_A(\mathbf{k}) \delta_B^*(\mathbf{k})\} \rangle_k$$

where the angle brackets denote an average over modes in a spherical shell of radius $k$. The remarkable property of the cross-spectrum is that its expectation value is exactly the true clustering power spectrum, $\mathbb{E}[P_{\times}(k)] = P_{\text{clust}}(k)$. This is because the [shot noise](@entry_id:140025) term arises from the correlation of each particle with itself (a "self-pair"). In a [cross-correlation](@entry_id:143353) between two [disjoint sets](@entry_id:154341) of particles, there are by definition no self-pairs. The random splitting process ensures that the correlation between a particle in sample A and a particle in sample B is purely due to the underlying physical clustering, not statistical self-counting.

This technique serves two critical purposes. First, it provides a direct, shot-noise-free measurement of the clustering signal, which is invaluable because it is robust even if the true [shot noise](@entry_id:140025) is non-Poissonian—a common occurrence we will explore later. Second, it offers a stringent validation of the standard auto-[spectrum analysis](@entry_id:275514). By constructing an empirical [shot noise](@entry_id:140025) estimator from the auto- and cross-spectra of the sub-samples, one can verify that the standard subtraction on the full catalog, $P_{gg}(k) - 1/\bar{n}$, is consistent with the direct measurement from $P_{\times}(k)$ (). Any significant discrepancy would signal a failure of the Poisson assumption or an error in the analysis pipeline.

### Shot Noise in the Context of Numerical Estimation

While the theoretical principles are elegant, estimating the [power spectrum](@entry_id:159996) from a simulation or survey introduces numerical artifacts that interact with shot noise in non-trivial ways.

#### Mass Assignment Schemes and Deconvolution Noise Amplification

To compute a [power spectrum](@entry_id:159996) using the Fast Fourier Transform (FFT), the discrete particle distribution must first be assigned to a regular Cartesian grid. This is accomplished using a **Mass Assignment Scheme (MAS)**, such as Cloud-in-Cell (CIC) or Triangular-Shaped-Cloud (TSC). This procedure is a convolution in real space, which corresponds to a multiplication by a window function $W(\mathbf{k})$ in Fourier space. Consequently, the power spectrum measured from the gridded field, $P_{\text{grid}}(k)$, is suppressed relative to the true [discrete spectrum](@entry_id:150970):

$$P_{\text{grid}}(k) \approx \left( P_{\text{clust}}(k) + P_{\text{shot}} \right) |W(k)|^2$$

To recover an estimate of the true spectrum, one must perform **[deconvolution](@entry_id:141233)** by dividing the gridded spectrum by $|W(k)|^2$. This, however, introduces a significant problem (). The MAS [window functions](@entry_id:201148) are designed to be smooth and are thus low-pass filters; their magnitude $|W(k)|$ decreases with increasing $k$, approaching zero near the **Nyquist [wavenumber](@entry_id:172452)** of the grid, $k_{\text{Ny}} = \pi/d$, where $d$ is the grid [cell size](@entry_id:139079).

The deconvolution factor, $1/|W(k)|^2$, therefore, becomes extremely large at high $k$. When this large factor multiplies the measured grid power, it dramatically amplifies any errors, including the statistical fluctuations of the shot noise contribution. While the expected value of the deconvolved [shot noise](@entry_id:140025) is simply $1/\bar{n}$ (before considering aliasing), its variance becomes highly amplified. This amplification renders the measurement numerically unstable at wavenumbers approaching the grid scale. A practical analysis must therefore define a maximum wavenumber, $k_{\text{max}}$, beyond which the deconvolution amplification factor exceeds a chosen tolerance, ensuring that the results remain robust ().

#### Aliasing of Shot Noise

A second, more subtle numerical artifact is **[aliasing](@entry_id:146322)**. When a continuous signal is sampled on a discrete grid, power from frequencies above the Nyquist frequency is "folded" or aliased back into the measurable frequency range ($|k_i| \le k_{\text{Ny}}$). The true power spectrum of a discrete Poisson process extends as a flat constant, $1/\bar{n}$, to arbitrarily high wavenumbers. The process of gridding this field causes this infinite reservoir of high-$k$ power to be aliased into the fundamental Brillouin zone ().

While the MAS window suppresses power at high $k$, it does not eliminate it. The result is that the measured, deconvolved [power spectrum](@entry_id:159996) of a pure shot noise field is no longer constant. It acquires a $k$-dependent contamination from its high-frequency images:

$$P_{\text{meas, shot}}(k) = \frac{1}{\bar{n}} \mathcal{A}(k)$$

where the aliasing factor $\mathcal{A}(k) = \sum_{\mathbf{m} \in \mathbb{Z}^3} |W(\mathbf{k} + 2k_{\text{Ny}}\mathbf{m})|^2 / |W(\mathbf{k})|^2$ is greater than 1 and increases with $k$. A naive subtraction of the constant $1/\bar{n}$ would therefore systematically under-subtract the [shot noise](@entry_id:140025), leaving a positive residual bias.

This effect can be mitigated in several ways. Using higher-order assignment schemes (e.g., TSC, $p=3$) which have more rapidly decaying [window functions](@entry_id:201148) reduces the magnitude of $\mathcal{A}(k)$. A particularly effective technique is **interlacing**, where the power spectrum is computed as the average of two grids, one of which is shifted by half a grid cell. This procedure exactly cancels the contributions from [aliasing](@entry_id:146322) images with [odd parity](@entry_id:175830), significantly reducing the overall bias (). For the highest precision, one can explicitly compute the [aliasing](@entry_id:146322) factor $\mathcal{A}(k)$ and subtract the corrected, $k$-dependent shot noise term.

### Physical Origins of Non-Poissonian Noise

Beyond numerical effects, the assumption of Poisson sampling itself often breaks down due to the complex physics of galaxy formation and clustering.

#### Counts-in-Cells and Excess Variance

A clear illustration of non-Poissonian behavior can be seen through the **counts-in-cells** statistic. Imagine partitioning the cosmic volume into cells and counting the number of tracers, $N_i$, in each cell. If the tracers were a simple Poisson sample of a uniform field with mean count $\bar{N}$, the variance of the counts would equal the mean: $\mathrm{Var}(N_i) = \bar{N}$.

However, the tracers are sampled from a density field that is itself fluctuating. Using the law of total variance, we can account for this. The variance of the counts becomes the sum of two terms: the average Poisson variance and the variance of the underlying field itself ():

$$\mathrm{Var}(N_i) = \mathbb{E}[\mathrm{Var}(N_i|\lambda_i)] + \mathrm{Var}(\mathbb{E}[N_i|\lambda_i]) = \bar{N} + \bar{N}^2 \sigma_{\text{cell}}^2$$

where $\lambda_i$ is the local Poisson rate, $\bar{N}$ is the mean count, and $\sigma_{\text{cell}}^2$ is the variance of the underlying density field coarse-grained on the cell scale. The total variance is the sum of the standard Poisson [shot noise](@entry_id:140025) ($\bar{N}$) and an **excess variance** term that arises from cosmic structure. The presence of clusters and voids naturally makes the distribution of counts broader than Poisson. The **[variance-to-mean ratio](@entry_id:262869)**, $\mathrm{Var}(N_i)/\mathbb{E}[N_i]$, is therefore greater than 1, and its excess, $D = \mathrm{Var}(N)/\mathbb{E}[N] - 1$, serves as a direct, dimensionless measure of the departure from Poisson statistics.

#### The Integral Constraint

A different effect arises in configuration space from the [finite volume](@entry_id:749401) of any survey. To compute the [two-point correlation function](@entry_id:185074) (2PCF), $\xi(r)$, one must estimate the mean tracer density from the survey itself. This normalization imposes an **integral constraint**: the volume-averaged measured correlation function, $\hat{\xi}(r)$, must be zero. This forces a negative bias on the measurement, which can be approximated as a constant offset $C$ ():

$$\hat{\xi}(r) \approx \xi(r) - C$$

where $C$ is the true 2PCF averaged over the survey volume. Shot noise, in configuration space, manifests as a contribution behaving like a Dirac [delta function](@entry_id:273429) at zero separation, $\delta_D(\mathbf{r})$. When binned radially, this creates a large positive contribution in the first radial bin (e.g., $[0, \Delta r]$). An observer measuring the 2PCF in this first bin sees the sum of the true binned clustering, the positive [shot noise](@entry_id:140025) contribution, and the negative integral constraint offset. These two constant-like offsets are degenerate, making it difficult to disentangle them from the measurement in the first bin alone.

### The Modern Synthesis: Shot Noise in Effective Field Theory

The various complexities—numerical artifacts, halo exclusion, and non-linear clustering—motivate a more sophisticated and systematic framework. The **Effective Field Theory of Large-Scale Structure (EFTofLSS)** provides this synthesis by treating "[shot noise](@entry_id:140025)" not as a simple statistical artifact to be removed, but as a component of a physical model to be measured and marginalized over.

In this framework, the galaxy density field is modeled as a bias expansion of the matter field plus a stochastic component, $\epsilon(\mathbf{x})$, which parameterizes our ignorance of the unresolved small-scale physics of galaxy formation. The auto-[power spectrum](@entry_id:159996) of this stochastic field, $P_{\epsilon\epsilon}(k)$, encapsulates what we traditionally call shot noise ().

A core principle of EFT is that since the small-scale physics has a finite correlation length (e.g., the size of a [dark matter halo](@entry_id:157684)), its impact on large-scale observables must be local. This implies that the Fourier transform of the stochastic [correlation function](@entry_id:137198), $P_{\epsilon\epsilon}(k)$, must be an [analytic function](@entry_id:143459) of $k$ at low $k$. Due to statistical [isotropy](@entry_id:159159), it can be Taylor expanded in even powers of $k$:

$$P_{\epsilon\epsilon}(k) = P_{\text{SN}} + c_2 k^2 + c_4 k^4 + \dots$$

The leading term, $P_{\text{SN}}$, is the **renormalized shot noise parameter**. It is a free parameter of the theory and is fundamentally not equal to $1/\bar{n}$. Instead, it absorbs all UV-sensitive, scale-independent contributions to the [power spectrum](@entry_id:159996). This includes the simple $1/\bar{n}$ term from discreteness, but also physical contributions from halo exclusion, [stochasticity](@entry_id:202258) in the galaxy-halo connection, and other non-linear effects.

A robust analysis within the EFTofLSS models the measured galaxy [power spectrum](@entry_id:159996) as:

$$P_{gg}^{\text{model}}(k) = P_{\text{clust}}(k; \theta_{\text{cosmo}}, \theta_{\text{bias}}) + P_{\text{SN}} + c_2 k^2 + \dots$$

The [cosmological parameters](@entry_id:161338) ($\theta_{\text{cosmo}}$), bias parameters ($\theta_{\text{bias}}$), and the stochastic [nuisance parameters](@entry_id:171802) ($P_{\text{SN}}, c_2, \dots$) are then jointly fit to the observational data. By marginalizing over the [nuisance parameters](@entry_id:171802), one obtains robust constraints on the [cosmological parameters](@entry_id:161338) of interest, with uncertainties that properly account for our ignorance of small-scale physics.

To guide these fits, one must have a reasonable **prior** on the [nuisance parameters](@entry_id:171802). This is where simulations become crucial (). The EFT procedure can be applied to [mock galaxy catalogs](@entry_id:752051) generated from simulations that span a range of galaxy formation physics (e.g., through variations in Halo Occupation Distribution models). A powerful method for calibrating $P_{\text{SN}}$ involves leveraging the galaxy-matter cross-spectrum, $P_{gm}(k)$. At leading order, $P_{gm}(k) = b_1 P_{mm}(k)$, which is clean of stochastic terms. This allows for an independent measurement of the linear bias $b_1$. With $b_1$ fixed, $P_{\text{SN}}$ can be isolated from the auto-spectrum, $P_{gg}(k) \approx b_1^2 P_{mm}(k) + P_{\text{SN}}$. Repeating this across an ensemble of mocks provides the distribution of expected $P_{\text{SN}}$ values, forming the basis for an informed prior in the analysis of real data. This modern approach transforms shot noise from a mere contaminant to be subtracted into a set of well-defined physical parameters that characterize the complex relationship between galaxies and the underlying [cosmic web](@entry_id:162042).