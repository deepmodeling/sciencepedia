## Introduction
Understanding and controlling the behavior of a multi-million-degree fusion plasma requires precise, non-invasive measurements of its most fundamental properties. Key among these are the [ion temperature](@entry_id:191275), which dictates the [fusion reaction](@entry_id:159555) rate, and the concentration of impurity species, which can cool the plasma and dilute the fuel. Photon spectroscopy emerges as the premier diagnostic tool, capable of peering into the heart of the plasma and deciphering the information encoded in the light emitted by impurity ions.

However, extracting quantitative data from this light is a complex challenge. Each observed photon is the result of intricate atomic processes influenced by the local temperature, density, magnetic fields, and plasma flows. This article bridges the gap between raw spectral data and meaningful physical insight, providing a comprehensive guide to using photon spectroscopy as a quantitative diagnostic for fusion research.

You will begin by exploring the foundational **Principles and Mechanisms**, learning how the position, width, and shape of a single [spectral line](@entry_id:193408) are determined by the plasma environment. The journey then continues into **Applications and Interdisciplinary Connections**, where these principles are applied to real-world scenarios, from measuring core [plasma rotation](@entry_id:753506) with Charge Exchange Recombination Spectroscopy (CXRS) to studying impurity sources at the plasma edge. Finally, the **Hands-On Practices** section offers the opportunity to solidify your understanding by tackling practical problems in [line shape analysis](@entry_id:172739) and spectral identification.

## Principles and Mechanisms

The light emitted by impurity ions embedded within a high-temperature plasma is a rich source of information. Each photon carries with it quantitative details about the local conditions at the point of its creation—the temperature, density, velocity, and electromagnetic fields of the surrounding plasma. Extracting this information requires a deep understanding of the atomic physics governing the emission process and the spectroscopic principles used to interpret the resulting spectrum. This chapter systematically lays out these core principles and mechanisms, progressing from the information encoded in a single spectral line to the interpretation of complex spectra and the practicalities of measurement.

### The Anatomy of a Spectral Line: Position, Width, and Shape

A spectral line, observed with a spectrometer, is not an infinitely sharp feature at a single wavelength. It is a profile characterized by a central position, a finite width, and a specific shape. Each of these attributes is a direct consequence of the physical environment of the emitting ions.

#### Line Center and Doppler Shift: Measuring Plasma Flow

An ion at rest emits a photon at a specific, characteristic rest wavelength, $\lambda_0$, determined by the [quantized energy](@entry_id:274980) difference between its initial and final states. If, however, the ion is moving with a velocity component $v_{\parallel}$ along the line of sight toward or away from the observer, the observed wavelength $\lambda$ will be shifted according to the non-relativistic Doppler effect:

$$ \frac{\lambda - \lambda_0}{\lambda_0} = \frac{v_{\parallel}}{c} $$

where $c$ is the speed of light.

In a fusion plasma, ions rarely act in isolation. They are part of a fluid that may exhibit large-scale, collective motion, such as toroidal or poloidal rotation. This [bulk flow](@entry_id:149773) imparts a common velocity component $v_{\parallel}$ to all impurity ions in a given region. Consequently, the center of the observed [spectral line profile](@entry_id:187553) will be shifted away from its rest wavelength by an amount $\Delta\lambda_{\text{shift}}$:

$$ \Delta\lambda_{\text{shift}} = \lambda_c - \lambda_0 = \frac{\lambda_0 v_{\parallel}}{c} $$

Here, $\lambda_c$ is the central wavelength of the observed line profile. By precisely measuring this shift relative to a known rest wavelength, we can determine the line-of-sight component of the bulk ion flow velocity. This is the fundamental principle behind spectroscopic measurements of [plasma rotation](@entry_id:753506) .

#### Line Broadening Mechanisms: Probing the Plasma Environment

The finite width and characteristic shape of a spectral line arise because not all ions emit at the same wavelength. Several physical mechanisms contribute to this broadening, each providing a unique diagnostic window into the plasma.

**Thermal Doppler Broadening: The Ion Temperature Thermometer**

In addition to any [bulk flow](@entry_id:149773), ions in a plasma possess random thermal motion, described by a [velocity distribution function](@entry_id:201683). For a plasma in thermal equilibrium, this is a Maxwell-Boltzmann distribution characterized by the **[ion temperature](@entry_id:191275)**, $T_i$. The velocity components of the ions along the line of sight therefore form a Gaussian distribution.

Each ion's velocity contributes a different Doppler shift, and the collective effect is a broadening of the [spectral line](@entry_id:193408) into a Gaussian profile. The intensity of the line at a wavelength $\lambda$, $I(\lambda)$, centered at $\lambda_c = \lambda_0(1 + v_{\parallel}/c)$, is given by:

$$ I(\lambda) \propto \exp\left(-\frac{mc^2}{2k_B T_i \lambda_0^2}(\lambda - \lambda_c)^2\right) $$

where $m$ is the mass of the impurity ion and $k_B$ is the Boltzmann constant. The width of this Gaussian profile is a direct measure of the [ion temperature](@entry_id:191275). A common metric for this width is the half width at $1/e$ of the maximum intensity, denoted $\Delta\lambda_D$. This is found by setting the argument of the exponential to $-1$, which yields:

$$ \Delta\lambda_D = \frac{\lambda_0}{c}\sqrt{\frac{2k_B T_i}{m}} $$

By measuring the Doppler broadening of an impurity line, we can thus determine the local [ion temperature](@entry_id:191275), a critical parameter for fusion performance. It is crucial to note that this broadening is governed by the temperature of the emitting ions ($T_i$), not the electrons ($T_e$) .

**Zeeman Splitting: Mapping the Magnetic Field**

Magnetically confined plasmas possess strong magnetic fields, which also influence [atomic energy levels](@entry_id:148255). An external magnetic field $\vec{B}$ lifts the degeneracy of levels with respect to the [magnetic quantum number](@entry_id:145584) $m_J$. In the linear (or weak-field) Zeeman regime, the energy shift $\Delta E$ of a sublevel is proportional to the field strength $B$:

$$ \Delta E = g_J \mu_B B m_J $$

Here, $\mu_B$ is the Bohr magneton and $g_J$ is the Landé [g-factor](@entry_id:153442), which depends on the orbital ($L$), spin ($S$), and total ($J$) angular momentum [quantum numbers](@entry_id:145558) of the level. For transitions between two such split levels, the emitted line is split into multiple polarized components, governed by the [selection rules](@entry_id:140784) $\Delta m_J = 0$ (for $\pi$ components) and $\Delta m_J = \pm 1$ (for $\sigma^{\pm}$ components).

The resulting spectral pattern depends on the g-factors of the upper and lower levels .
-   **Normal Zeeman Effect**: For transitions between singlet states (where $S=0$), the [g-factor](@entry_id:153442) for both levels is $g_J=1$. This results in a simple, universal triplet pattern: an unshifted $\pi$ component and two symmetrically shifted $\sigma^{\pm}$ components.
-   **Anomalous Zeeman Effect**: For transitions involving at least one state with non-zero spin ($S \neq 0$), the g-factors of the upper and lower levels are generally different and not equal to 1. This leads to a complex, multi-line pattern unique to the specific transition. For example, the triplet transition ${}^{3}P_{2} \rightarrow {}^{3}S_{1}$ in an Ar II ion results in nine distinct spectral components with relative frequency offsets of $\{ -2, -1.5, -1, -0.5, 0, +0.5, +1, +1.5, +2 \}$ in units of the Larmor frequency.

While often a complication that must be accounted for in [line-shape analysis](@entry_id:751290) for $T_i$, the Zeeman effect can also be used as a powerful diagnostic to measure the magnitude of the local magnetic field.

**Stark Broadening: Sensing Electric Microfields**

The dense environment of a plasma means that every emitting ion is subject to fluctuating electric fields from nearby electrons and ions. These **electric microfields** cause a shifting and splitting of energy levels known as the Stark effect, which leads to [line broadening](@entry_id:174831). The nature of the Stark effect depends critically on the atomic structure of the emitter .

-   **Linear Stark Effect**: For **[hydrogenic ions](@entry_id:174450)** (e.g., H, He$^{+}$, C$^{5+}$), energy levels with the same principal quantum number $n$ but different [orbital angular momentum](@entry_id:191303) $l$ are degenerate. This degeneracy allows for a first-order, linear shift in energy with the electric field strength, $\Delta E \propto E$. This results in significant broadening, particularly for lines from high-$n$ states.

-   **Quadratic Stark Effect**: For most **non-[hydrogenic ions](@entry_id:174450)**, the electronic core lifts the $l$-degeneracy. The relevant energy levels are non-degenerate and possess definite parity. Due to [parity selection rules](@entry_id:203598), the first-order energy shift vanishes. The leading contribution is a second-order effect, where the energy shift is proportional to the square of the field strength, $\Delta E \propto E^2$. This effect is generally much weaker than the linear Stark effect.

In fusion plasmas, Doppler broadening is often the dominant mechanism for impurity lines in the visible spectrum, but Stark broadening can become significant for certain lines (e.g., hydrogenic lines from high-$n$ states) and in regions of very high density, such as near a [divertor](@entry_id:748611) plate.

### Decoding Multi-Line Spectra

While a single line provides information on temperature and flows, observing multiple lines from the same or different ions unlocks a wealth of additional information about the plasma's composition and [thermodynamic state](@entry_id:200783).

#### Spectroscopic Identification

The first step in any analysis is to identify the origin of the observed spectral features. This is achieved by comparing the measured spectrum to extensive atomic databases. The process relies on matching a unique "fingerprint" of an atomic transition or multiplet . The key features for identification are:
1.  **Wavelength Positions**: The absolute wavelengths of the lines, corrected for the expected Doppler shift due to [plasma rotation](@entry_id:753506).
2.  **Multiplet Structure**: For transitions involving [fine structure](@entry_id:140861), a single transition can appear as a multiplet of closely spaced lines. The *separations* between these lines are invariant under a uniform Doppler shift and serve as a robust identifier.
3.  **Relative Intensities**: In an optically thin plasma, the relative intensities of lines within a multiplet are determined by atomic transition probabilities and statistical weights. This intensity pattern is a powerful constraint for identification.

For instance, an observed feature consisting of three lines at approximately $464.74\,\mathrm{nm}$, $465.03\,\mathrm{nm}$, and $465.16\,\mathrm{nm}$ with relative intensities of roughly $0.6:1.0:0.5$ can be confidently identified as the $3p\,^{3}P_J \rightarrow 3d\,^{3}D_{J'}$ multiplet of doubly-ionized carbon (C$^{2+}$) by matching these observed separations and intensity ratios to database values, while rejecting other candidate species like O$^{+}$ or N$^{+}$ whose patterns are inconsistent.

#### Line Intensity and Collisional-Radiative Modeling

The absolute intensity, or more fundamentally, the **photon [emissivity](@entry_id:143288)** $\varepsilon$ (photons emitted per unit volume per unit time) of a [spectral line](@entry_id:193408), depends on the population density of the upper atomic level of the transition. Understanding and predicting these populations is the central goal of **Collisional-Radiative (CR) modeling**.

In a plasma, an ion's excited level populations are determined by a dynamic balance of numerous atomic processes. The emissivity of a line from an impurity in charge state $z$ is primarily driven by two pathways :
1.  **Electron-Impact Excitation**: A plasma electron collides with an ion in charge state $z$, exciting it from a lower level to the upper level of the transition. The rate of this process scales with the electron density $n_e$ and the density of the parent ion, $n_z$.
2.  **Recombination**: An electron recombines with an ion from the next higher charge state, $z+1$, producing an ion in charge state $z$ in a highly excited state, which then cascades down to the level of interest. This process scales with the electron density $n_e$ and the density of the recombining ion, $n_{z+1}$.

This dual-pathway nature allows us to express the total line [emissivity](@entry_id:143288) $\varepsilon_{u\ell}$ for a transition $u \rightarrow \ell$ as the sum of these two contributions:
$$ \varepsilon_{u\ell} = n_{e}\, n_{z}\, \mathrm{PEC}^{\mathrm{ex}}_{u\ell}(T_{e}, n_{e}) \;+\; n_{e}\, n_{z+1}\, \mathrm{PEC}^{\mathrm{rec}}_{u\ell}(T_{e}, n_{e}) $$
Here, $\mathrm{PEC}^{\mathrm{ex}}$ and $\mathrm{PEC}^{\mathrm{rec}}$ are the **Photon Emissivity Coefficients** for the excitation and recombination channels, respectively. These coefficients, pre-calculated using a detailed CR model, encapsulate all the complex [atomic physics](@entry_id:140823) (cross-sections, branching ratios, cascade effects) and depend on the [electron temperature](@entry_id:180280) $T_e$ and density $n_e$.

The general CR model has important limiting cases that depend on the [plasma density](@entry_id:202836) :
-   **Coronal Equilibrium (CE)**: At low electron densities typical of the core of many fusion plasmas, collisional de-excitation is negligible compared to spontaneous [radiative decay](@entry_id:159878). An excited state is populated by electron-impact excitation and depopulated almost exclusively by radiation. Line emissivities scale linearly with $n_e$.
-   **Local Thermodynamic Equilibrium (LTE)**: At extremely high electron densities, collisions dominate all other processes. Collisional excitation and de-excitation rates far exceed [radiative decay](@entry_id:159878) rates, forcing the level populations into a Boltzmann distribution characterized by the [electron temperature](@entry_id:180280) $T_e$.
-   **Collisional-Radiative (CR) Regime**: In the intermediate density range, common in plasma edge and [divertor](@entry_id:748611) regions, both collisional and radiative processes are important. This is the most complex regime, but it also offers the richest diagnostic possibilities.

#### Line Ratio Diagnostics

A powerful diagnostic technique involves measuring the ratio of intensities of two different spectral lines. Taking a ratio has the significant advantage of eliminating the dependence on the absolute impurity density, which is often difficult to measure. The behavior of these ratios, as predicted by CR models, can be highly sensitive to local plasma parameters.

A classic example is the spectroscopy of helium-like ions (e.g., C$^{4+}$, O$^{6+}$), which emit a characteristic set of four lines from the $n=2$ levels, often called the `w`, `x`, `y`, and `z` lines . Ratios of these lines serve as benchmark diagnostics:
-   **The R-ratio, $R \equiv z/(x+y)$**, is primarily sensitive to **electron density $n_e$**. The `z` line originates from a long-lived (metastable) level. As $n_e$ increases, electrons can collisionally excite the ion out of this [metastable state](@entry_id:139977) before it has a chance to radiate, thus decreasing the intensity of the `z` line relative to the others.
-   **The G-ratio, $G \equiv (z+x+y)/w$**, is primarily sensitive to **[electron temperature](@entry_id:180280) $T_e$**. This ratio compares the triplet lines (`x`,`y`,`z`) to the singlet resonance line (`w`). The triplet levels are populated efficiently by recombination from the next higher charge state (H-like), a process that dominates at lower $T_e$. The singlet level is populated mainly by direct excitation, which has a strong, exponential dependence on $T_e$. The ratio is therefore a sensitive [thermometer](@entry_id:187929).

Ratios of lines from adjacent charge states, such as the H-like Ly-$\alpha$ line to the He-like `w` line of the same element, are direct probes of the [ionization balance](@entry_id:162056), providing another avenue to constrain $T_e$ and $n_e$.

### Probing the Plasma: Passive vs. Active Spectroscopy

The methods described so far rely on **passive spectroscopy**—observing the photons that the plasma naturally emits. A more powerful technique, **active spectroscopy**, involves injecting a probe into the plasma to stimulate a specific emission process at a precise location.

The premier active spectroscopic diagnostic for measuring local [ion temperature](@entry_id:191275) and rotation is **Charge Exchange Recombination Spectroscopy (CXRS)** . The process is as follows:
1.  A high-energy beam of neutral atoms (typically hydrogen or deuterium) is injected into the plasma.
2.  A [neutral beam](@entry_id:752451) atom collides with a fully stripped impurity ion (e.g., C$^{6+}$). In this charge-exchange reaction, the neutral donates its electron to the ion.
3.  The impurity ion, now with one electron (e.g., C$^{5+}$), is left in a highly excited state. Momentum transfer during this rapid electron exchange is negligible, so the newly formed ion retains the exact velocity of its parent impurity ion.
4.  This excited ion then radiatively decays, emitting a characteristic photon.

The power of CXRS lies in its localization and its direct link to the ion properties. The emission only occurs where the [neutral beam](@entry_id:752451) and the spectrometer's line-of-sight intersect, providing excellent spatial resolution. Because the emitting ion's velocity is identical to the local impurity ion velocity, the Doppler broadening of the resulting spectral line directly yields the local $T_i$, and the Doppler shift gives the local rotation velocity.

### From Plasma to Detector: The Realities of Measurement

The journey from a photon emitted in the plasma to a signal recorded by a detector involves two final, crucial steps that must be accounted for to accurately interpret the data.

#### Line-of-Sight Integration and Abel Inversion

A spectrometer does not measure the emission from a single point. It collects all the light along its collimated **line-of-sight (LOS)**, or chord, through the plasma. The measured quantity is the chord-integrated **brightness** $I(b)$, where $b$ is the chord's impact parameter (its minimum distance to the plasma center).

For an axisymmetric plasma (like an idealized tokamak) where the local emissivity $\epsilon$ is only a function of the minor radius $r$, the brightness is related to the [emissivity](@entry_id:143288) profile $\epsilon(r)$ via the **Abel transform** :

$$ I(b) = 2 \int_{b}^{a} \epsilon(r) \frac{r}{\sqrt{r^{2}-b^{2}}} dr $$

where $a$ is the plasma radius. To recover the physically important local [emissivity](@entry_id:143288) profile $\epsilon(r)$ from a set of brightness measurements $I(b)$ taken at different impact parameters, one must perform the inverse operation, known as the **Abel inversion**:

$$ \epsilon(r) = -\frac{1}{\pi} \int_{r}^{a} \frac{dI/db}{\sqrt{b^2-r^2}} db $$

This mathematical [deconvolution](@entry_id:141233) is fundamental to moving from line-integrated data to local plasma parameters. It is critical to recognize that this procedure is only valid under the assumption of axisymmetry; for plasmas with significant poloidal or toroidal asymmetries, more complex tomographic techniques are required.

#### The Instrument Function and Convolution

No real spectrometer has perfect resolution. The optics and finite slit width cause even a perfectly monochromatic input (a delta function in wavelength) to be recorded as a profile with a finite width. This profile is called the **instrument line shape** or instrument function, and it represents the spectrometer's impulse response .

The spectrum that physically arrives at the detector plane, $I_{\text{obs}}(\lambda)$, is the **convolution** of the true spectrum emitted by the plasma, $I_{\text{true}}(\lambda)$, with the instrument line shape, $I_{\text{inst}}(\lambda)$:

$$ I_{\text{obs}}(\lambda) = (I_{\text{true}} * I_{\text{inst}})(\lambda) $$

This convolution process invariably broadens the observed line. For instance, if the true Doppler-broadened line is a Gaussian and the instrument function is also well-approximated by a Gaussian, the observed line will be a wider Gaussian whose variance is the sum of the true line's variance and the instrumental variance.

Finally, this [continuous spectrum](@entry_id:153573) is sampled by a detector with pixels of finite size. It is important to distinguish **[spectral resolution](@entry_id:263022)**, which is the intrinsic width of the instrument function ($W_{\text{inst}}$) set by the optics and slit, from **spectral sampling**, which is the wavelength range covered by a single pixel ($D$). A well-designed experiment ensures that the spectral features of interest are oversampled (i.e., covered by more than two pixels across their width) so that the measurement is limited by the physical broadening and instrumental resolution, not by the pixel size. For example, a CXRS measurement of a C$^{5+}$ line at $T_i = 2.0\,\mathrm{keV}$ might produce a true Doppler width of $\sim0.53\,\mathrm{nm}$. When observed with an instrument having a resolution of $W_{\text{inst}} = 0.15\,\mathrm{nm}$, the resulting observed line has a width of $W_{\text{obs}} = \sqrt{(0.53)^2 + (0.15)^2} \approx 0.55\,\mathrm{nm}$. If this is sampled by a detector with $D = 0.020\,\mathrm{nm/pixel}$, the line profile will span approximately 27 pixels, indicating a well-resolved, oversampled measurement where the instrument's characteristics can be reliably deconvolved from the data to extract the true plasma parameters.