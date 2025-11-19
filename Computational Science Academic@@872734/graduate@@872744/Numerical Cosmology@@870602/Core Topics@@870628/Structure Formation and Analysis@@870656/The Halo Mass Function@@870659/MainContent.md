## Introduction
The [halo mass function](@entry_id:158011) is a cornerstone of modern cosmology, providing a critical link between the smooth, initial conditions of the universe and the rich, clustered structures we observe today. It addresses the fundamental problem of how to predict the number density of gravitationally collapsed dark matter halos, which host the galaxies and clusters that trace the cosmic web. This article offers a comprehensive exploration of this vital tool. The first chapter, **Principles and Mechanisms**, will delve into the theoretical underpinnings, from the seminal Press-Schechter formalism to the refined models that match high-precision simulations. Next, **Applications and Interdisciplinary Connections** will showcase how the [halo mass function](@entry_id:158011) is used to constrain [cosmological parameters](@entry_id:161338), probe new physics, and serve as the foundation for models of galaxy formation. Finally, **Hands-On Practices** will provide practical exercises to solidify understanding of key concepts, connecting theory to numerical application.

## Principles and Mechanisms

The [halo mass function](@entry_id:158011) is a cornerstone of [modern cosmology](@entry_id:752086), providing a quantitative prediction for the abundance of [dark matter halos](@entry_id:147523) as a function of their mass $M$ and redshift $z$. It serves as a critical bridge between the linear theory of [cosmic structure formation](@entry_id:137761), which describes the evolution of small initial density fluctuations, and the highly non-linear, collapsed objects that host galaxies and galaxy clusters. This chapter elucidates the theoretical principles and mechanisms that underpin our understanding of the [halo mass function](@entry_id:158011), from its fundamental definition to sophisticated models that accurately describe the results of large-scale numerical simulations.

### Defining the Halo Mass Function

The primary quantity of interest is the **differential [halo mass function](@entry_id:158011)**, denoted $n(M,z)$, which is defined as the number of [dark matter halos](@entry_id:147523) per unit comoving volume per unit mass interval. If we consider a comoving volume $V$ and count the number of halos $N$ whose masses fall within a narrow range $[M, M+\mathrm{d}M]$, the [mass function](@entry_id:158970) is given by:

$$
n(M,z) \equiv \frac{\mathrm{d}N}{\mathrm{d}V \mathrm{d}M}
$$

The use of **comoving volume** is crucial. As the universe expands, the physical number density of any conserved population of objects decreases. By using [comoving coordinates](@entry_id:271238)—a coordinate system that expands with the universe—we factor out this trivial dilution, allowing for a meaningful comparison of structure abundance at different cosmic epochs. From its definition, the physical units of $n(M,z)$ are inverse volume times inverse mass, typically expressed in cosmology as $\mathrm{Mpc}^{-3} M_{\odot}^{-1}$.

Due to the vast range of halo masses, spanning many orders of magnitude from dwarf galaxy halos to massive clusters, it is often more convenient to consider the [mass function](@entry_id:158970) per logarithmic mass interval. This form is related to $n(M,z)$ by a simple change of variables. Since $\mathrm{d}(\ln M) = \mathrm{d}M/M$, the number of halos per unit comoving volume in a logarithmic mass bin $\mathrm{d}(\ln M)$ is:

$$
\frac{\mathrm{d}n}{\mathrm{d}\ln M} \mathrm{d}(\ln M) = n(M,z) \mathrm{d}M
$$

Substituting $\mathrm{d}M = M \mathrm{d}(\ln M)$, we find the direct relationship:

$$
\frac{\mathrm{d}n}{\mathrm{d}\ln M} = M n(M,z) = M \frac{\mathrm{d}N}{\mathrm{d}V \mathrm{d}M}
$$

This quantity has units of comoving number density, e.g., $\mathrm{Mpc}^{-3}$, and is often plotted as it gives a clearer visual representation of halo abundances across different mass scales.

### The Press-Schechter Formalism: A First-Principles Model

The first successful theoretical model for the [halo mass function](@entry_id:158011) was developed by William H. Press and Paul Schechter in 1974. The **Press-Schechter (PS) formalism** connects the abundance of collapsed objects at a given epoch to the statistical properties of the initial [density fluctuations](@entry_id:143540) in the early universe. The derivation rests on three fundamental pillars.

First, the initial matter [density fluctuations](@entry_id:143540) are assumed to be a **Gaussian [random field](@entry_id:268702)**. This is a key prediction from the theory of cosmic inflation. Such a field is fully characterized by its [two-point correlation function](@entry_id:185074), or its Fourier transform, the **[power spectrum](@entry_id:159996)** $P(k)$. To study objects of a characteristic mass $M$, we smooth the linear [density contrast](@entry_id:157948) field, $\delta(\mathbf{x})$, with a filter function $W(kR)$ of characteristic radius $R$. The mass scale is related to the smoothing radius by $M = \frac{4\pi}{3} \bar{\rho}_{\mathrm{m}} R^3$, where $\bar{\rho}_{\mathrm{m}}$ is the mean comoving [matter density](@entry_id:263043). The variance of the smoothed field, $\sigma^2(M)$, is then given by an integral over the [power spectrum](@entry_id:159996):

$$
\sigma^2(M) = \int_0^\infty \frac{k^2 \mathrm{d}k}{2\pi^2} P(k) |W(kR)|^2
$$

The variance $\sigma^2(M)$ is a crucial quantity: it represents the typical amplitude of [density fluctuations](@entry_id:143540) on the mass scale $M$. Since the power spectrum of cold dark matter has more power on small scales, $\sigma(M)$ is a monotonically decreasing function of $M$.

Second, the model adopts the **[spherical collapse](@entry_id:161208)** condition. This idealized model shows that a spherical overdense region will stop expanding, turn around, and collapse to form a gravitationally bound object if its initial, linearly extrapolated overdensity exceeds a critical threshold, $\delta_{\mathrm{c}}$. For a flat, matter-dominated (Einstein-de Sitter) universe, this threshold is a constant, $\delta_{\mathrm{c}} \approx 1.686$. In more general cosmologies, it has a very weak dependence on redshift and [cosmological parameters](@entry_id:161338).

Third, the original PS formalism makes the key [ansatz](@entry_id:184384) that the fraction of all mass in the universe contained within collapsed halos of mass greater than $M$ is equal to the probability that the smoothed linear overdensity $\delta_M$ exceeds the critical threshold $\delta_{\mathrm{c}}$. Since $\delta_M$ is a Gaussian random variable with [zero mean](@entry_id:271600) and variance $\sigma^2(M)$, this probability is:

$$
P(\delta_M > \delta_{\mathrm{c}}) = \int_{\delta_{\mathrm{c}}}^\infty \frac{1}{\sqrt{2\pi}\sigma(M)} \exp\left(-\frac{\delta^2}{2\sigma^2(M)}\right) \mathrm{d}\delta = \frac{1}{2} \mathrm{erfc}\left(\frac{\delta_{\mathrm{c}}}{\sqrt{2}\sigma(M)}\right)
$$

This simple calculation, however, leads to a normalization issue known as the **cloud-in-cloud problem**: as $M \to 0$, it predicts that only half the mass of the universe ends up in collapsed objects. The PS formalism resolved this by inserting a fudge factor of 2, arguing that underdense regions are destined to be accreted by overdense ones.

A more rigorous justification for this factor comes from the **Excursion Set Theory**. This powerful framework recasts the problem by considering the trajectory of the smoothed overdensity $\delta(S)$ as a function of variance $S \equiv \sigma^2(M)$. As one decreases the smoothing scale (increasing [mass resolution](@entry_id:197946)), $S$ increases, and $\delta(S)$ performs a random walk. A mass element is said to belong to a halo of mass $M$ if the variance $S(M)$ is the *first* scale at which its trajectory crosses the barrier $\delta_{\mathrm{c}}$. This "first-passage" problem for a random walk with an absorbing barrier naturally yields a solution that is exactly twice the naive estimate, thereby ensuring [mass conservation](@entry_id:204015) and resolving the cloud-in-cloud problem from first principles.

Following this corrected approach, the fraction of mass in halos more massive than $M$, $F(>M)$, is $F(>M) = \mathrm{erfc}(\delta_{\mathrm{c}} / (\sqrt{2}\sigma(M)))$. The [mass fraction](@entry_id:161575) in the interval $[M, M+\mathrm{d}M]$ is then related to the [number density](@entry_id:268986) $n(M)$ by [mass conservation](@entry_id:204015): $\frac{M}{\bar{\rho}_{\mathrm{m}}} n(M) \mathrm{d}M = -\frac{\mathrm{d}F}{\mathrm{d}M} \mathrm{d}M$. Differentiating $F(>M)$ with respect to $M$ and rearranging yields the Press-Schechter [mass function](@entry_id:158970):

$$
\frac{\mathrm{d}n}{\mathrm{d}M} = \sqrt{\frac{2}{\pi}} \frac{\bar{\rho}_{\mathrm{m}}}{M^2} \frac{\delta_{\mathrm{c}}}{\sigma(M)} \exp\left(-\frac{\delta_{\mathrm{c}}^2}{2\sigma^2(M)}\right) \left(-\frac{M}{\sigma(M)}\frac{\mathrm{d}\sigma(M)}{\mathrm{d}M}\right)
$$
This expression remarkably predicts the abundance of halos based only on the initial power spectrum and the theory of gravity.

### Universality and the Multiplicity Function

The PS formula reveals a deep concept in structure formation: **universality**. The abundance of halos depends on mass, redshift, and cosmology, but these dependencies can be packaged into a single, dimensionless variable. This is the **peak height**, $\nu$, defined as:

$$
\nu \equiv \frac{\delta_{\mathrm{c}}(z)}{\sigma(M,z)}
$$

Here, we have made the redshift dependence explicit. The variance evolves as $\sigma(M,z) = D(z)\sigma(M,0)$, where $D(z)$ is the [linear growth](@entry_id:157553) factor. The peak height $\nu$ measures the "rareness" of the fluctuation that gave rise to a halo: a halo with $\nu=1$ formed from a typical "1-$\sigma$" fluctuation on that mass scale, while a halo with $\nu=3$ formed from a much rarer "3-$\sigma$" peak. By construction, $\nu$ incorporates the primary dependencies on mass (via $\sigma(M,0)$), [redshift](@entry_id:159945) (via $D(z)$), and cosmology (via $P(k)$, $D(z)$, and $\delta_{\mathrm{c}}$). The hypothesis is that the abundance of halos, when expressed as a function of $\nu$, should be approximately universal across different masses, redshifts, and even [cosmological models](@entry_id:161416).

This leads to the definition of the **multiplicity function**, $f(\nu)$, which represents the fraction of total cosmic mass contained in halos per unit logarithmic interval of $\nu$. By enforcing [mass conservation](@entry_id:204015), one can derive the fundamental relationship that connects the theoretical multiplicity function to the observable [number density](@entry_id:268986):

$$
n(M,z) = \frac{\bar{\rho}_{\mathrm{m}}}{M} f(\nu) \left|\frac{\mathrm{d}\ln\nu}{\mathrm{d}M}\right|
$$

Using this formalism, the Press-Schechter [mass function](@entry_id:158970) can be expressed in the beautifully simple universal form:

$$
f_{\mathrm{PS}}(\nu) = \sqrt{\frac{2}{\pi}} \nu \exp\left(-\frac{\nu^2}{2}\right)
$$

This function depends only on the peak height $\nu$, embodying the principle of universality.

### Beyond Spherical Collapse: Ellipsoidal Models and Halo Bias

While the Press-Schechter model was a monumental success, it has known inaccuracies. N-body simulations show that it underpredicts the abundance of the most massive halos and overpredicts the number of intermediate-mass halos. The primary physical reason for this discrepancy is the simplifying assumption of [spherical collapse](@entry_id:161208). In reality, [gravitational collapse](@entry_id:161275) is anisotropic; proto-halos are generally triaxial and are subject to external tidal forces from the surrounding large-scale structure.

This more realistic picture of **[ellipsoidal collapse](@entry_id:159908)** can be incorporated into the [excursion set formalism](@entry_id:161517) by replacing the constant collapse barrier $\delta_{\mathrm{c}}$ with a **moving barrier** $B(S)$ that depends on the variance $S=\sigma^2(M)$. The physical motivation is that smaller-mass halos (larger $S$) require a higher initial overdensity to collapse because they must overcome the shearing [tidal forces](@entry_id:159188) of the larger environment. Motivated by this, Sheth and Tormen proposed a modification to the PS function based on an excursion set model with a moving barrier. The resulting **Sheth-Tormen (ST) [multiplicity](@entry_id:136466) function** provides a much better fit to simulation results and has the form:

$$
f_{\mathrm{ST}}(\nu) = A \sqrt{\frac{2a}{\pi}} \nu \left[1 + (a\nu^2)^{-p}\right] \exp\left(-\frac{a\nu^2}{2}\right)
$$

Here, $a \approx 0.707$ and $p \approx 0.3$ are parameters fit to simulations, and $A$ is a [normalization constant](@entry_id:190182) ensuring $\int f(\nu) \mathrm{d}\ln\nu = 1$. The term $(a\nu^2)^{-p}$ enhances the abundance of rare, high-$\nu$ halos, correcting the main deficiency of the PS model. More advanced models, starting from first principles with a linear barrier in variance $B(S) = \delta_c + \beta S$, can also be solved within the excursion set framework, yielding multiplicity functions that capture the essential modifications introduced by scale-dependent collapse thresholds.

The [halo mass function](@entry_id:158011) is also intimately linked to **[halo bias](@entry_id:161548)**, which describes the fact that halos are not uniformly distributed but are biased tracers of the underlying matter distribution. The **[peak-background split](@entry_id:753301) (PBS)** formalism provides a powerful method to compute this bias. The core idea is to consider the effect of a long-wavelength density fluctuation $\delta_{\ell}$ on the abundance of smaller-mass halos. This background fluctuation effectively modulates the collapse threshold, $\delta_{\mathrm{c}} \to \delta_{\mathrm{c}} - \delta_{\ell}$, making it easier for halos to form in large-scale overdensities and harder in underdensities. The linear [halo bias](@entry_id:161548) $b_1$ is defined as the first-order response of the halo number density to this [modulation](@entry_id:260640). Applying this to the ST [mass function](@entry_id:158970) allows for a direct derivation of the bias as a function of peak height:

$$
b_{1}^{\mathrm{E}}(\nu) = 1 + \frac{1}{\delta_{\mathrm{c}}}\left(a\nu^{2} - 1 + \frac{2p}{1+(a\nu^{2})^{p}}\right)
$$

This expression correctly predicts that more massive, rarer halos (higher $\nu$) are more strongly biased tracers of the [cosmic web](@entry_id:162042).

### From Theory to Practice: Halo Finding and Mass Definitions

The theoretical concept of a halo must be translated into a practical algorithm for identifying them in N-body simulations. The choice of algorithm and mass definition has a significant, systematic impact on the measured [halo mass function](@entry_id:158011). The two most common methods are **Friends-of-Friends (FOF)** and **Spherical Overdensity (SO)**.

The FOF algorithm is a percolation method. It links together any two simulation particles separated by less than a specified **linking length**, $b$, which is a fraction of the mean inter-particle separation. All particles connected by a chain of such links form a single FOF group, or halo. The canonical value used in cosmology is $b=0.2$.

The SO method, in contrast, is centered on density peaks. It defines a halo as the mass enclosed within a spherical region whose mean internal density reaches a certain threshold, $\Delta$, relative to a reference density. Common choices are $M_{200\mathrm{c}}$, where the mean density is 200 times the [critical density](@entry_id:162027) of the universe, $\rho_{\mathrm{c}}$, or $M_{180\mathrm{b}}$, where the mean density is 180 times the mean background matter density, $\bar{\rho}_{\mathrm{m}}$.

These two definitions are not equivalent. Using simple physical arguments, one can show that for the standard linking length of $b=0.2$, the FOF algorithm approximately groups particles out to a boundary iso-density contour of $\rho \approx 60 \bar{\rho}_{\mathrm{m}}$. For a typical halo density profile, this corresponds to a mean enclosed overdensity of $\Delta \approx 180$ relative to the mean [matter density](@entry_id:263043). Thus, FOF masses with $b=0.2$ are most closely related to the $M_{180\mathrm{b}}$ definition.

This difference has profound consequences. At [redshift](@entry_id:159945) $z=0$ in a $\Lambda$CDM cosmology with $\Omega_{\mathrm{m},0} \approx 0.3$, the $M_{180\mathrm{b}}$ mass definition corresponds to a mean density of $180 \bar{\rho}_{\mathrm{m}} = 180 (\Omega_{\mathrm{m},0} \rho_{\mathrm{c}}) \approx 54\rho_{\mathrm{c}}$. Since this density threshold is much lower than the $200\rho_{\mathrm{c}}$ used for $M_{200\mathrm{c}}$, the radius of an FOF/$M_{180\mathrm{b}}$ halo is significantly larger than its $M_{200\mathrm{c}}$ radius. Consequently, for a given object, $M_{\mathrm{FOF}} > M_{200\mathrm{c}}$. Because the [halo mass function](@entry_id:158011) falls steeply at high masses, this systematic shift in the [mass assignment](@entry_id:751704) leads to a significantly higher amplitude for the FOF [mass function](@entry_id:158970) compared to the $M_{200\mathrm{c}}$ [mass function](@entry_id:158970) at a fixed mass. It is also important to note that FOF algorithms are susceptible to numerical artifacts, such as forming spurious "bridges" between physically distinct halos that are close to each other, an effect that can artificially inflate halo masses, particularly for objects resolved with few particles. Understanding these subtleties is paramount when comparing theoretical predictions to measurements from simulations or observational surveys.