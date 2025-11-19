## Introduction
The simple act of counting objects across the cosmos, from stars to distant galaxies, holds the key to unlocking the deepest secrets of our Universe. This fundamental technique, known as number count analysis, provides a surprisingly powerful method for mapping cosmic history, measuring the geometry of spacetime, and testing the laws of physics on the largest scales. But how do we transform a raw catalog of sources into a precision cosmological probe? How do we account for the evolution of galaxies and the distorting effects of gravity that lie between us and the objects we observe? This article addresses these questions, providing a graduate-level guide to the science of cosmological [number counts](@entry_id:160205).

The journey begins in the **Principles and Mechanisms** chapter, where we will derive the fundamental equations that govern the expected number of sources as a function of [redshift](@entry_id:159945). We will explore how these counts depend on key [cosmological parameters](@entry_id:161338) and dissect the subtle observational effects, like gravitational lensing and [redshift-space distortions](@entry_id:157636), that are crucial for modern analysis. Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate the remarkable versatility of this method, showing how it is used to constrain the nature of [dark energy](@entry_id:161123), test General Relativity, probe the [epoch of reionization](@entry_id:161482), and even investigate the properties of dark matter. Finally, the **Hands-On Practices** section bridges theory and practice, presenting a curated set of problems that allow you to apply these concepts to calculate key observables, from the total background light to the [redshift distribution](@entry_id:157730) of sources in a realistic survey.

## Principles and Mechanisms

The previous chapter introduced the foundational idea that counting sources across the cosmos provides a powerful method for understanding the Universe's history and composition. Here, we develop the quantitative framework for this technique. We will derive the fundamental equations governing source [number counts](@entry_id:160205), explore their dependence on [cosmological parameters](@entry_id:161338) and source evolution, and investigate the subtle observational effects that are now at the forefront of modern cosmological research.

### The Fundamental Relation of Number Counts

The simplest cosmological observable is the number of sources of a certain type on the sky. To turn this into a precise scientific tool, we must predict the number of sources we expect to see in a given patch of sky and within a specific range of distances. In an expanding universe, distance is most conveniently measured by [cosmological redshift](@entry_id:152343), $z$.

Let us consider the number of sources, $dN$, observed within a small solid angle on the sky, $d\Omega$, and a small [redshift](@entry_id:159945) interval, $dz$. This number is simply the comoving number density of the sources, $n_c(z)$, multiplied by the corresponding comoving volume element, $dV_c$.

$dN = n_c(z) dV_c$

The **comoving [number density](@entry_id:268986)**, $n_c(z)$, represents the number of sources per unit comoving volume at the epoch corresponding to [redshift](@entry_id:159945) $z$. A key point is that if sources are conserved (i.e., they are neither created nor destroyed), their comoving [number density](@entry_id:268986) is constant, $n_c(z) = n_c(0)$. However, real astrophysical populations like galaxies and [quasars](@entry_id:159221) evolve through processes like mergers, [star formation](@entry_id:160356), and active galactic nucleus feedback, so $n_c(z)$ is generally a function of [redshift](@entry_id:159945).

The comoving [volume element](@entry_id:267802), $dV_c$, for a survey that covers a [solid angle](@entry_id:154756) $d\Omega$ and a redshift slice $dz$ is given by the area of the spherical shell at that distance, multiplied by its thickness. In a Friedmann-Lemaître-Robertson-Walker (FLRW) universe, the proper area of a sphere at [comoving distance](@entry_id:158059) $D_C(z)$ is $4\pi D_M(z)^2$, where $D_M(z)$ is the transverse [comoving distance](@entry_id:158059). For a spatially [flat universe](@entry_id:183782) ($\Omega_k = 0$), which is strongly supported by observations, the transverse [comoving distance](@entry_id:158059) is equal to the line-of-sight [comoving distance](@entry_id:158059), $D_C(z)$. The proper thickness of the shell corresponding to a [redshift](@entry_id:159945) interval $dz$ is related to the Hubble parameter $H(z)$, which describes the expansion rate of the universe at that epoch: $dr = c \, dz / H(z)$. Combining these geometric factors, the comoving volume element is:

$dV_c = D_C(z)^2 \frac{c \, dz}{H(z)} d\Omega$

Putting these pieces together, we arrive at the fundamental equation for the differential [number counts](@entry_id:160205) per unit [redshift](@entry_id:159945) and unit [solid angle](@entry_id:154756):

$\frac{dN}{dz \, d\Omega} = n_c(z) D_C(z)^2 \frac{c}{H(z)}$

This equation is the cornerstone of number count cosmology. It beautifully encapsulates how counting sources is a function of both astrophysics (through the evolution of $n_c(z)$) and cosmology (through the geometric factors $D_C(z)$ and the expansion history $H(z)$).

### Probing Cosmology with Number Counts

The cosmological utility of the number count equation stems from the dependence of the Hubble parameter, $H(z)$, and the [comoving distance](@entry_id:158059), $D_C(z)$, on the energy content of the universe. The Hubble parameter's evolution is governed by the Friedmann equation:

$H(z) = H_0 \sqrt{\Omega_{m,0}(1+z)^3 + \Omega_{r,0}(1+z)^4 + \Omega_{k,0}(1+z)^2 + \Omega_{de,0} \exp\left(3 \int_0^z \frac{1+w(z')}{1+z'} dz'\right)}$

Here, $H_0$ is the Hubble constant (the expansion rate today), and $\Omega_{i,0}$ are the present-day density parameters for matter ($m$), radiation ($r$), curvature ($k$), and dark energy ($de$). The function $w(z)$ is the [equation of state parameter](@entry_id:159133) for dark energy.

The line-of-sight [comoving distance](@entry_id:158059) is then found by integrating the inverse of the Hubble parameter:

$D_C(z) = c \int_0^z \frac{dz'}{H(z')}$

By measuring $dN/dz$ and comparing it to predictions, we can constrain the values of these [cosmological parameters](@entry_id:161338).

#### Case Study 1: The Einstein-de Sitter Universe

To build intuition, let's consider the simplest cosmological model: a spatially flat, matter-only universe known as the **Einstein-de Sitter (EdS) model**. In this model, $\Omega_{m,0}=1$ and all other density parameters are zero. The Hubble parameter and [comoving distance](@entry_id:158059) simplify considerably:

$H(z) = H_0 (1+z)^{3/2}$

$D_C(z) = c \int_0^z \frac{dz'}{H_0(1+z')^{3/2}} = \frac{2c}{H_0} \left[1 - \frac{1}{\sqrt{1+z}}\right]$

Let's also assume a simple model for source evolution, where the comoving [number density](@entry_id:268986) follows a power law: $n_c(z) = n_0(1+z)^\beta$. Here, $n_0$ is the local number density, and the **evolution parameter** $\beta$ describes how the population changes. $\beta > 0$ implies there were more sources in the past (e.g., due to mergers), while $\beta  0$ implies sources were less numerous (e.g., if we are observing a population that forms late).

Substituting these expressions into our fundamental equation gives the predicted [number counts](@entry_id:160205) for this specific scenario [@problem_id:1040307]:

$\frac{dN}{dz \, d\Omega} = \left(n_0(1+z)^\beta\right) \left(\frac{2c}{H_0}\left[1 - \frac{1}{\sqrt{1+z}}\right]\right)^2 \frac{c}{H_0(1+z)^{3/2}}$

$\frac{dN}{dz \, d\Omega} = \frac{4 c^3 n_0}{H_0^3} (1+z)^{\beta - 3/2} \left[1 - \frac{1}{\sqrt{1+z}}\right]^2$

If we were to conduct an all-sky survey, the counts per unit [redshift](@entry_id:159945) would simply be this expression integrated over the full $4\pi$ steradians of the [celestial sphere](@entry_id:158268) [@problem_id:830323].

#### Case Study 2: A General Perfect Fluid Universe

The EdS model is a useful toy model, but modern cosmology aims to test more general theories, particularly concerning [dark energy](@entry_id:161123). We can generalize our framework to a [flat universe](@entry_id:183782) dominated by a **perfect fluid** with a constant [equation of state parameter](@entry_id:159133) $w_1 = p_1/\rho_1$. For such a universe, $H(z) = H_0(1+z)^{3(1+w_1)/2}$. A [matter-dominated universe](@entry_id:158254) corresponds to $w_1=0$, and a radiation-dominated one to $w_1=1/3$.

Furthermore, we can adopt a more physically motivated model for source evolution. For instance, the formation of certain sources might be tied to the background density of a specific component of the universe. Let's imagine our sources have a number density proportional to the energy density of a second, subdominant perfect fluid with equation of state $w_2$. In this case, $n(z) \propto \rho_2(z) \propto (1+z)^{3(1+w_2)}$.

Following the same procedure as before—calculating $D_C(z)$ and substituting into the main equation—we can derive a general expression for the [number counts](@entry_id:160205) [@problem_id:859032]. For $w_1 \neq -1/3$, the result is:

$\frac{dN}{dz d\Omega} = \frac{4c^{3}n_{0}}{H_{0}^{3}(1+3w_{1})^{2}} (1+z)^{\frac{3(1+2w_{2}-w_{1})}{2}} \left[1-(1+z)^{-\frac{1+3w_{1}}{2}}\right]^{2}$

This powerful result demonstrates how the observed distribution of sources over redshift, $\frac{dN}{dz}$, is sensitively dependent on the equation of state of the dominant energy component ($w_1$). This is one of the classic methods used to probe the nature of dark energy, for which $w_1 \approx -1$.

### The Interplay of Volume and Evolution

A naive expectation might be that we should see progressively fewer sources as we look to higher redshifts, simply because they are farther away. However, the number count relation tells a more complex story. The function $\frac{dN}{dz}$ is a product of three redshift-dependent terms: the source evolution $n_c(z)$, the area factor $D_C(z)^2$, and the volume-depth factor $1/H(z)$.

The comoving volume element per unit [redshift](@entry_id:159945), $dV_c/dz$, typically increases from $z=0$, reaches a maximum, and then decreases at very high redshift. The source density $n_c(z)$ can either increase or decrease with [redshift](@entry_id:159945), depending on the population. The competition between these effects often produces a peak in the [number counts](@entry_id:160205) at a specific [redshift](@entry_id:159945), $z_{peak}$.

We can find this peak by differentiating the number count expression with respect to $z$ and setting the result to zero. For our EdS model with power-law evolution, this maximization yields a simple and elegant result for the peak [redshift](@entry_id:159945) [@problem_id:816605]:

$z_{peak} = \left(\frac{5/2 - \beta}{3/2 - \beta}\right)^2 - 1$

This shows a direct link between a macroscopic feature of the survey data ($z_{peak}$) and a microscopic property of the source population (the evolution parameter $\beta$). For example, if we observe a population of galaxies with $\beta=1$ (a declining comoving density towards the present), the peak of their distribution would be expected at $z_{peak} = (1.5/0.5)^2 - 1 = 8$.

### The Anatomy of Observed Number Count Fluctuations

While the mean [number counts](@entry_id:160205), $\bar{N}(z)$, are a powerful cosmological probe, even more information is encoded in their fluctuations across the sky. We define the observed number count fluctuation as $\delta_N^{\text{obs}}(\hat{\mathbf{n}}, z) = (N(\hat{\mathbf{n}}, z) - \bar{N}(z)) / \bar{N}(z)$, where $\hat{\mathbf{n}}$ is a direction on the sky.

These observed fluctuations are not solely due to the intrinsic clustering of sources, $\delta_g$. As light propagates from a distant source to us, its path is perturbed by the gravitational landscape of the intervening large-scale structure. This imprints a series of projection effects on the observed number and distribution of sources. The full expression for the observed fluctuation is a sum of many terms:

$\delta_N^{\text{obs}} = \delta_g + \delta_{\text{RSD}} + \delta_{\text{lens}} + \delta_{\text{SW}} + \dots$

Let's examine some of the most significant contributions.

#### Gravitational Lensing and Magnification Bias

The gravitational field of foreground structures acts like a lens, bending the paths of light rays from background sources. This **gravitational lensing** has two effects on a flux-limited survey (which catalogs all sources brighter than a flux limit $F_{\text{lim}}$):

1.  **Flux Magnification**: The flux of a background source is magnified by a factor $\mu$. This means some sources that were intrinsically too faint to be included in the survey ($F_{\text{int}}  F_{\text{lim}}$) are magnified above the threshold ($\mu F_{\text{int}} > F_{\text{lim}}$), increasing the number of observed sources.
2.  **Solid Angle Dilution**: The same patch of sky is stretched by the lensing, so its apparent [solid angle](@entry_id:154756) increases by the same factor $\mu$. This dilutes the number of sources per unit [solid angle](@entry_id:154756), decreasing the observed count.

These two effects compete. The net result depends on the faint-end slope of the source [number counts](@entry_id:160205), typically modeled as a power law $\bar{N}(>F) \propto F^{-s}$. A steeper slope (larger $s$) means there are many more faint sources than bright ones, so the flux [magnification](@entry_id:140628) effect, which brings faint sources into the sample, will dominate.

In the [weak lensing](@entry_id:158468) regime, the magnification is related to the **lensing convergence** $\kappa$ by $\mu \approx 1 + 2\kappa$. The convergence is a weighted [line-of-sight integral](@entry_id:751289) of the matter density. A careful calculation shows that the fluctuation in the [number counts](@entry_id:160205) due to lensing, known as **[magnification](@entry_id:140628) bias**, is [@problem_id:856064]:

$\delta_{g, \text{lens}} = 2(s-1)\kappa$

This remarkable relation shows that an overdensity of foreground matter (positive $\kappa$) leads to an increase in the observed number of background galaxies (positive $\delta_{g, \text{lens}}$), provided $s > 1$. By measuring this effect, we can map the foreground mass distribution using the background galaxies as tracers.

#### Peculiar Velocities and Redshift-Space Distortions

The observed [redshift](@entry_id:159945) of a galaxy has two components: the [cosmological redshift](@entry_id:152343) due to the Hubble expansion, and a Doppler shift from the galaxy's [peculiar velocity](@entry_id:157964) relative to the observer. This means the observed redshift is not a perfect indicator of distance. This effect, known as **[redshift-space distortions](@entry_id:157636) (RSD)**, causes galaxies to appear squashed along the line of sight in overdense regions (the "Fingers of God" effect) and flattened in underdense regions. In Fourier space, the RSD contribution to the galaxy overdensity is anisotropic, depending on the angle between the [wavevector](@entry_id:178620) $\vec{k}$ and the line of sight $\hat{\mathbf{n}}$: $\Delta_g^{\text{RSD}}(\vec{k}) \propto (\hat{\mathbf{n}}\cdot\hat{\mathbf{k}})^2 \delta_m(\vec{k})$ [@problem_id:885217]. This anisotropy allows us to measure the rate of [growth of cosmic structure](@entry_id:750080), a key test of General Relativity on cosmological scales.

#### Other Relativistic and Local Effects

The full relativistic picture includes a host of other effects, such as the Sachs-Wolfe effect ([gravitational redshift](@entry_id:158697) from the potential at the source), the integrated Sachs-Wolfe effect, and Doppler terms. Even our local environment can induce anisotropies. For example, an observer situated in a large-scale gravitational tidal field, described by a [tidal tensor](@entry_id:755970) $T_{ij}$, will observe a quadrupole anisotropy in the [number counts](@entry_id:160205) of distant sources. This anisotropy is a combination of local RSD, gravitational redshift, and lensing effects. At low [redshift](@entry_id:159945) in a [matter-dominated universe](@entry_id:158254), the amplitude of this quadrupole fluctuation, $\delta_N(\hat{\mathbf{n}}, z) = C(z) T_{ij}\hat{n}^i\hat{n}^j$, can be explicitly calculated [@problem_id:836754]:

$C(z) = \frac{1}{H_0^2}\left[-\frac{2}{3}(\alpha+1)+\frac{\alpha+2}{2}z+z^2\right]$

where $\alpha$ is the power-law index of the background counts. This demonstrates how even our local [cosmic web](@entry_id:162042) influences our view of the large-scale Universe.

### Statistical Analysis of Number Count Fluctuations

To extract cosmological information from these fluctuations, we use statistical tools, chief among them the **[angular power spectrum](@entry_id:161125)**, $C_\ell$. This quantity measures the variance of the fluctuation field as a function of angular scale on the sky (where large scales correspond to small [multipole moments](@entry_id:191120) $\ell$, and small scales to large $\ell$).

#### Example 1: The Power Spectrum of Magnification Bias

The simple relationship $\delta_{g, \text{lens}} = 2(s-1)\kappa$ translates directly to the power spectra: $C_\ell^{\mu\mu} = 4(s-1)^2 C_\ell^{\kappa\kappa}$. The [magnification](@entry_id:140628) bias power spectrum is simply proportional to the lensing convergence [power spectrum](@entry_id:159996). Using the **Limber approximation**, a tool for calculating power spectra of projected quantities, we can compute $C_\ell^{\kappa\kappa}$.

For an EdS universe, with all sources at a [comoving distance](@entry_id:158059) $\chi_s$ and a [matter power spectrum](@entry_id:161407) $P_\delta(k) = A k^{-2}$, the [magnification](@entry_id:140628) bias [power spectrum](@entry_id:159996) is found to be [@problem_id:836784]:

$C_\ell^{\mu\mu} = \frac{3(s-1)^2 A H_0^4 \chi_s^5}{35 c^4 \ell^2}$

This result shows how a measurement of the angular clustering of galaxies ($C_\ell^{\mu\mu}$) can be used to constrain a combination of the source properties ($s, \chi_s$), the amplitude of matter fluctuations ($A$), and the expansion history ($H_0$).

#### Example 2: Cross-Correlations

The true power of [modern cosmology](@entry_id:752086) often comes from cross-correlating different observational probes. For instance, we can cross-correlate the lensing of the Cosmic Microwave Background (CMB) with the distribution of galaxies. The CMB lensing convergence, $\kappa_{\text{CMB}}$, probes the entire matter distribution out to the [last scattering surface](@entry_id:157701), while the galaxy distribution traces the matter at a lower redshift.

Let's consider the cross-[power spectrum](@entry_id:159996) between the CMB lensing convergence $\kappa$ and the RSD contribution to galaxy [number counts](@entry_id:160205), $C_\ell^{\kappa, \text{RSD}}$. Both fields are sourced by the same underlying matter distribution, so they are expected to be correlated. Using the Limber approximation and a model where galaxies are in a thin shell at distance $\chi_g$, we can calculate this cross-spectrum. The calculation reveals a non-[zero correlation](@entry_id:270141) that depends on the properties of the intervening [gravitational potential](@entry_id:160378) and the [growth of structure](@entry_id:158527) [@problem_id:885217]. For a specific EdS model, the result is:

$C_\ell^{\kappa, \text{RSD}} = \frac{2A (1-\chi_g/\eta_0)^2 (\chi_s-\chi_g)}{3 \ell \chi_s \chi_g^2}$

where $\chi_s$ is the distance to the CMB, and $\eta_0$ is the horizon distance. Measuring such a cross-spectrum provides a powerful consistency check of the entire cosmological model and can help break degeneracies between parameters.

### The Impact of Observational Realities

Finally, it is crucial to recognize that real-world observations are never perfect. Instrumental noise, [photon statistics](@entry_id:175965), and intrinsic variability can introduce errors in measurements, such as the flux of a source. These errors can potentially bias our cosmological inferences.

Consider a population of sources whose true integral [number counts](@entry_id:160205) follow a perfect power law, $N_{\text{true}}(S) \propto S^{-\alpha_0}$. If our observed flux measurements are subject to a log-normal random error (i.e., the error in $\ln S$ is Gaussian with variance $\sigma^2$), one might expect this smearing to change the effective slope of the counts. A detailed calculation, however, reveals a subtle and important result: the convolution of a [power-law distribution](@entry_id:262105) with a Gaussian in [logarithmic space](@entry_id:270258) results in another power law with the *exact same slope* [@problem_id:836856].

The observed logarithmic slope $\alpha_{\text{obs}}$ remains equal to the true slope $\alpha_0$. The observational error only changes the overall normalization of the counts. While this is a specific result for a [power-law distribution](@entry_id:262105), it serves as a critical lesson: the impact of systematic errors must be carefully and quantitatively modeled, as our intuition can sometimes be misleading. Understanding these details is essential for extracting robust cosmological constraints from galaxy surveys.