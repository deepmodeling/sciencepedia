## Introduction
The detection of Earth-mass exoplanets using the radial velocity (RV) method represents one of the foremost challenges in modern astrophysics. This sensitive technique, which measures the gravitational wobble a planet induces on its host star, is fundamentally limited not by our instruments, but by the intrinsic variability of the stars themselves. This "stellar activity noise"—apparent velocity shifts caused by phenomena like starspots and convection—can obscure the tiny signals of low-mass planets or even create [false positives](@entry_id:197064), presenting a critical knowledge gap that must be bridged. This article provides a comprehensive overview of this problem, guiding the reader from first principles to state-of-the-art solutions. The following chapters will first deconstruct the physical **Principles and Mechanisms** that generate stellar RV noise. Next, we will explore the **Applications and Interdisciplinary Connections**, demonstrating how astronomers use diagnostic indicators and advanced statistical models to mitigate these effects in real-world exoplanet searches. Finally, a series of **Hands-On Practices** will allow you to apply these concepts and develop practical skills in analyzing and interpreting RV data contaminated by stellar activity.

## Principles and Mechanisms

The detection of exoplanets via the [radial velocity](@entry_id:159824) (RV) method hinges on measuring minute, periodic Doppler shifts in a star's spectrum, induced by the gravitational pull of an orbiting companion. The true center-of-mass velocity of the star, however, is just one of several components that contribute to the total measured velocity. A raw RV measurement, as obtained from a spectrograph, is a composite signal that must be carefully deconstructed to isolate the planetary signal of interest. The remaining, non-planetary stellar variations constitute what is known as "stellar activity noise," a primary limiting factor in the detection of low-mass, long-period planets. This chapter dissects the physical principles and mechanisms that generate this astrophysical noise.

### Deconstructing the Measured Radial Velocity

A raw [radial velocity](@entry_id:159824) measurement, denoted as $v_{\mathrm{raw}}(t)$, derived from the centroid of a [spectral line](@entry_id:193408) or a [cross-correlation function](@entry_id:147301) at time $t$, is the sum of several distinct velocity components. To a first-order approximation for non-relativistic speeds, these components add linearly:

$v_{\mathrm{raw}}(t) = v_{\star}(t) + v_{B}(t) + v_{\mathrm{inst}}(t) + v_{\mathrm{act}}(t)$

Here, $v_{\star}(t)$ represents the **true barycentric velocity of the star**, the component that contains the Keplerian signal from any orbiting planets. This is the signal we seek to isolate. The other terms are contaminants that must be removed or modeled.

The term $v_{B}(t)$ is the **barycentric correction**, which accounts for the motion of the observatory itself. As the Earth orbits the Sun and rotates on its axis, the observatory moves with a significant and time-varying velocity relative to the Solar System's barycenter. This motion, projected onto the line of sight to the target star, introduces a large, predictable Doppler shift. This component is precisely calculated using orbital ephemerides and subtracted from the raw data.

The term $v_{\mathrm{inst}}(t)$ represents **instrumental drift**. This is an apparent velocity shift caused by subtle changes in the spectrograph's internal environment, such as variations in temperature or pressure, which can alter the optical path and the effective [dispersion of light](@entry_id:171169). To track and remove this drift, modern high-precision spectrographs simultaneously observe a stable calibration source, such as a Laser Frequency Comb (LFC). Since the LFC is internal to the instrument, it is affected by $v_{\mathrm{inst}}(t)$ but not by $v_{\star}(t)$, $v_{B}(t)$, or [stellar astrophysics](@entry_id:160229). By measuring the apparent shift of the LFC's known [spectral lines](@entry_id:157575), $v_{\mathrm{inst}}(t)$ can be determined and subtracted from the stellar measurement.

After removing the barycentric and instrumental effects, we are left with $v_{\star}(t) + v_{\mathrm{act}}(t)$. The term $v_{\mathrm{act}}(t)$ is the **astrophysical noise** arising from stellar activity. It is not a true center-of-mass velocity but an apparent velocity shift caused by physical processes on the stellar surface that distort the shapes of [spectral lines](@entry_id:157575). Since these processes are intrinsic to the star, they cannot be removed by simple kinematic corrections or instrumental calibration . Understanding the origins of $v_{\mathrm{act}}(t)$ is therefore paramount to mitigating its impact.

### The Cross-Correlation Function and its Diagnostics

The radial velocity of a star is typically measured not from a single [spectral line](@entry_id:193408), but from thousands of lines simultaneously. This is accomplished using the **[cross-correlation function](@entry_id:147301) (CCF)**. The observed stellar spectrum, $S(\lambda)$, is correlated with a numerical template or mask, $M(\lambda)$, which represents the positions and relative strengths of many stellar absorption lines. The CCF, $C(v)$, is computed as a function of a trial Doppler velocity $v$:

$C(v) = \sum_{j} w_{j}\,S(\lambda_{j}(1+v/c))$

where the sum is over the lines in the mask at rest wavelengths $\lambda_j$ with weights $w_j$. The resulting CCF is effectively an average, high signal-to-noise representation of the stellar line profile.

For a quiet, non-rotating star, the CCF would be a symmetric dip, and its [centroid](@entry_id:265015) would accurately reflect the star's systemic velocity. The RV is typically extracted by fitting a symmetric profile, such as a Gaussian, to the CCF dip and adopting the fitted mean as the [centroid](@entry_id:265015) . However, stellar activity introduces asymmetries into the spectral lines. Because the [centroid](@entry_id:265015) calculation is sensitive to the full shape of the CCF dip, any asymmetry will bias the measurement, creating an apparent velocity shift, $\delta v$, even if the star's true center-of-mass velocity is constant. This can be understood by considering the first moment of the CCF dip profile, $D(v)$. If an activity-driven perturbation adds a small, asymmetric component $\epsilon \Delta D(v)$ to a symmetric base profile $D_0(v)$, the [centroid](@entry_id:265015) will shift by an amount proportional to the first moment of the asymmetric part, demonstrating that line-shape changes directly translate to apparent RV changes .

This physical connection between line shape and apparent RV gives rise to powerful diagnostics. By measuring not only the position but also the shape of the CCF, we can track [stellar activity](@entry_id:1132375). The most common shape indicators are:

*   **Full Width at Half Maximum (FWHM):** The width of the CCF profile, which is sensitive to [stellar rotation](@entry_id:161595) and magnetic broadening (Zeeman effect).
*   **Contrast (or Depth):** The depth of the CCF dip, which can be affected by the temperature of active regions.
*   **Bisector Inverse Span (BIS):** A direct measure of line asymmetry. The bisector is the [locus of midpoints](@entry_id:164215) of horizontal segments across the CCF profile. For a symmetric line, the bisector is a vertical line. For an asymmetric line, it is curved. The BIS is defined as the difference in velocity between the top and bottom sections of the bisector, $\mathrm{BIS}=\langle v_{\mathrm{bis}}\rangle_{\mathrm{top}}-\langle v_{\mathrm{bis}}\rangle_{\mathrm{bottom}}$.

A true Keplerian signal from a planet should cause a rigid shift of the CCF without altering its shape. Therefore, a planetary signal should manifest as a periodic variation in RV with no corresponding variations in the FWHM, contrast, or BIS. In contrast, stellar activity causes variations in all of these parameters that are often correlated with the apparent RV changes . This provides a crucial method for distinguishing planetary signals from activity-induced noise.

### Mechanisms of Rotational Modulation

The most prominent sources of stellar RV variability for Sun-like stars are tied to the star's rotation, which carries magnetic features across the visible disk. These features perturb the disk-integrated light in two primary ways: by modulating the surface brightness and by altering the local convective velocity field.

#### Flux Blocking by Starspots

Starspots are cool, dark regions that emerge on the photosphere due to strong magnetic fields. As a spot rotates across the stellar disk, it blocks light from the portion of the rotating surface it covers. When the spot is on the approaching (blueshifted) limb, it selectively removes blueshifted light from the disk-integrated spectrum. This causes the net [spectral line profile](@entry_id:187553) to become slightly redshifted, resulting in a positive RV perturbation. Conversely, when the spot is on the receding (redshifted) limb, it blocks redshifted light, causing a net [blueshift](@entry_id:274414) and a negative RV perturbation .

In a simplified model neglecting [limb darkening](@entry_id:157740), the RV perturbation, $\Delta v(t)$, caused by a single small spot is approximately:

$\Delta v(t) \approx a (1-\beta) v_{\mathrm{eq}} \sin i \cos \lambda \sin(\Omega t)$

Here, $a$ is the fractional area of the spot, $\beta \approx (T_{\mathrm{spot}}/T_{\mathrm{phot}})^4$ is its intensity contrast relative to the quiet photosphere, $v_{\mathrm{eq}}$ is the equatorial rotation speed, $i$ is the stellar inclination, $\lambda$ is the spot's latitude, and $\Omega$ is the angular rotation speed. This model shows that the spot-induced RV signal is **antisymmetric** about the central meridian, crossing from positive to negative as the spot transits the visible disk. Its amplitude scales with the spot's area, contrast, and the projected rotational velocity  . A similar, but opposite-signed, effect is produced by bright regions ([faculae](@entry_id:1124815)), which add light instead of blocking it.

#### Convective Blueshift and its Suppression

The surface of a Sun-like star is a roiling sea of convective cells called granules. Hot, bright plasma rises in the center of these granules and sinks in the cooler, darker intergranular lanes. Because the upflows are both brighter and cover a larger surface area than the downflows, the disk-integrated spectrum exhibits a net [blueshift](@entry_id:274414), known as the **convective blueshift**.

We can quantify this using a simple two-component model. Let upflows have fractional area $f_u$, intensity $I_u$, and velocity $v_u$ (negative), and downflows have $f_d$, $I_d$, and $v_d$ (positive). The net RV is the flux-weighted average velocity:

$v_{\mathrm{cen}} = \frac{f_u I_u v_u + f_d I_d v_d}{f_u I_u + f_d I_d}$

Using typical solar values (e.g., $f_u = 0.6$, $I_u = 1.1$, $v_u = -1.0\,\mathrm{km\,s^{-1}}$ and $f_d = 0.4$, $I_d = 0.9$, $v_d = +0.5\,\mathrm{km\,s^{-1}}$), we find a net [blueshift](@entry_id:274414) of several hundred meters per second ($v_{\mathrm{cen}} \approx -471\,\mathrm{m\,s^{-1}}$). This large, constant blueshift is a fundamental property of the stellar spectrum .

RV *variability* arises when this [blueshift](@entry_id:274414) is locally altered. Magnetic fields in active regions, particularly in bright [faculae](@entry_id:1124815) and plage, inhibit convection. This **suppression of convective blueshift** means that the local gas has a velocity that is redshifted relative to the quiet photosphere. As a facula rotates across the disk, it introduces a region with an intrinsic positive velocity shift, $\Delta v_{\mathrm{cb}} > 0$. The resulting RV perturbation is dominated by this effect. Unlike the flux-blocking signal of a spot, this convective signal is **symmetric** and produces a net redshift that peaks when the facula is near disk center, as the line-of-sight projection of the vertical convective motions is greatest there. The facular RV signature is thus predominantly a symmetric redshift, in stark contrast to the antisymmetric signature of a spot .

### Stochastic and Evolutionary Effects

Beyond the regular modulation from stable rotating features, [stellar activity](@entry_id:1132375) also introduces RV variations that are stochastic or evolve over time, leading to quasi-periodic behavior.

#### Granulation Jitter

The convective granulation pattern itself is not static; individual granules evolve on timescales of minutes. Because we observe a finite number of granules on the stellar disk, their statistical fluctuations do not average out perfectly. This incomplete averaging of the velocity and brightness patterns of millions of granules produces a stochastic RV signal, often called "jitter."

The standard deviation of this jitter, $\sigma_{\mathrm{RV,g}}$, can be estimated by noting that the variance of an average of $N_{\mathrm{eff}}$ independent elements scales as $1/N_{\mathrm{eff}}$. The RV jitter is thus:

$\sigma_{\mathrm{RV,g}} \approx \frac{\sigma_{\mathrm{patch}}}{\sqrt{N_{\mathrm{eff,g}}}}$

where $\sigma_{\mathrm{patch}}$ is the characteristic RV contribution of a single convective patch (related to its velocity and brightness contrast) and $N_{\mathrm{eff,g}}$ is the number of effective, independent granulation patches on the visible disk. For a Sun-like star, $N_{\mathrm{eff,g}}$ is on the order of $10^5$, which reduces a local velocity signature of $\sim 1\,\mathrm{km\,s^{-1}}$ to a disk-integrated jitter of $\sim 0.3 - 0.6\,\mathrm{m\,s^{-1}}$ on timescales of minutes. The power spectrum of this noise is that of a correlated stochastic process, with power concentrated at frequencies corresponding to the granulation timescale ($\sim 8$ minutes) . Larger scale flows, such as supergranulation, contribute similarly on longer timescales (hours to days).

#### Differential Rotation and Quasi-periodicity

Solar-type stars do not rotate as solid bodies. Their rotation rate is latitude-dependent, a phenomenon known as **differential rotation**. A common empirical law describes the angular velocity $\Omega$ as a function of latitude $\theta$:

$\Omega(\theta) = \Omega_{\mathrm{eq}}(1 - \alpha \sin^2\theta)$

where $\Omega_{\mathrm{eq}}$ is the equatorial angular velocity and $\alpha$ is the shear parameter. This means that starspots at different latitudes will orbit the star with different periods, $P(\theta) = 2\pi/\Omega(\theta)$. A star with active regions at multiple latitudes will thus exhibit multiple, closely spaced periodicities in its RV data, corresponding to the various rotation periods present .

Furthermore, active regions are not permanent. They emerge, evolve, and decay over a characteristic **spot evolution timescale**, $\tau_{\mathrm{spot}}$. The combination of these two effects—[differential rotation](@entry_id:161059) (a spread of frequencies, $\Delta\omega$) and finite spot lifetimes (amplitude and [phase modulation](@entry_id:262420) on timescale $\tau_{\mathrm{spot}}$)—destroys the strict periodicity of the activity signal. The RV signal becomes **quasi-periodic**: it oscillates near the rotation period, but its amplitude and phase decorrelate over time. The signal loses its "memory."

This loss of coherence is a critical concept for modern [time-series analysis](@entry_id:178930), particularly in Gaussian Process (GP) regression. The **[coherence time](@entry_id:176187)** of a quasi-periodic signal is the timescale over which its autocorrelation envelope decays. This timescale is set by the physical processes that destroy phase coherence. It is determined by the shorter of the spot evolution timescale, $\tau_{\mathrm{spot}}$, and the de-phasing time due to differential rotation, $\sim 1/\Delta\omega$. The rotation period, $P_{\mathrm{rot}}$, sets the timescale of the oscillation, but the [coherence time](@entry_id:176187), which governs the long-term predictability, is set by these evolutionary and dispersive effects .

### The Chromatic Signature of Stellar Activity

A powerful, unifying characteristic of [stellar activity](@entry_id:1132375) noise is its **chromaticity**—its wavelength dependence. This provides a key avenue for distinguishing it from a planetary signal.

A true Doppler shift from a planet's gravitational pull is **achromatic**. According to the Doppler relation, $\Delta\lambda / \lambda = v/c$, the fractional wavelength shift is constant across the entire spectrum. An RV measurement should therefore yield the same velocity regardless of the wavelength range (or spectral order) used for the measurement.

In contrast, RV signals induced by stellar activity are fundamentally chromatic for two main reasons:

1.  **Line-dependent Convective Blueshift:** As discussed, the magnitude of convective blueshift depends on the detailed physics of line formation. Lines with different opacities and excitation potentials form at different average depths in the [stellar atmosphere](@entry_id:158094), where the convective velocity fields and thermodynamic properties are different. Consequently, the magnitude of the convective blueshift, and its suppression in magnetic regions, varies from line to line. An RV measurement, which is an average over many lines, will therefore depend on the specific set of lines used, which varies by wavelength region .

2.  **Zeeman Effect:** The magnetic fields responsible for spots and [faculae](@entry_id:1124815) also directly affect the spectral lines through the Zeeman effect, which splits [atomic energy levels](@entry_id:148255). This splitting results in a characteristic wavelength separation $\Delta\lambda_Z \propto \lambda^2 g B$, where $g$ is the line's Landé factor. When converted to velocity units, the scale of this magnetic perturbation becomes $\Delta v_Z = c(\Delta\lambda_Z/\lambda) \propto \lambda g B$. The apparent RV shift induced by Zeeman-distorted line profiles is thus wavelength-dependent, becoming more pronounced in redder spectral orders.

Because both major sources of activity-induced RV—convective effects and magnetic effects—are inherently wavelength-dependent, the total signal $v_{\mathrm{act}}(t)$ is chromatic. Measuring the RV simultaneously in different color bands and looking for differences is a potent technique for diagnosing and disentangling stellar activity from the achromatic signature of a true planetary companion .