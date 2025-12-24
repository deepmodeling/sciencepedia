## Introduction
Global Navigation Satellite System Reflectometry (GNSS-R) has emerged as a powerful and innovative remote sensing technique, transforming the ubiquitous signals from navigation satellites into valuable tools for Earth observation. By treating the Earth's surface as a mirror, GNSS-R provides a unique, low-cost method for monitoring [critical properties](@entry_id:260687) of our planet's land and water systems. This article addresses the need for a comprehensive understanding of this method, bridging the gap from fundamental physics to practical application. It provides a detailed exploration of how the faint, reflected GNSS signals can be harnessed to retrieve quantitative information about the environment.

The following chapters are structured to guide you from theoretical foundations to real-world use cases. In **"Principles and Mechanisms"**, we will dissect the core physics of GNSS-R, examining it as a [bistatic radar](@entry_id:1121676) system, exploring the signal interactions with different surfaces, and detailing the signal processing chain that produces the fundamental Delay-Doppler Map (DDM) observable. Following this, **"Applications and Interdisciplinary Connections"** will demonstrate the technique's versatility by exploring its role in retrieving key geophysical parameters such as ocean wind speed, land soil moisture, and surface height, while also addressing the complex environmental factors that influence measurements. Finally, **"Hands-On Practices"** will offer a series of guided problems to solidify your understanding of key concepts, from calculating atmospheric delays to modeling the effects of surface motion on the received signal.

## Principles and Mechanisms

The capacity of Global Navigation Satellite System Reflectometry (GNSS-R) to retrieve geophysical parameters of the Earth's surface rests upon a combination of [bistatic radar](@entry_id:1121676) principles, [electromagnetic scattering](@entry_id:182193) theory, and sophisticated signal processing techniques. This chapter elucidates these foundational principles and mechanisms, beginning with the fundamental geometry of the measurement, progressing to the physical interaction between the signal and the surface, and concluding with an examination of the signal processing chain that produces the core [observables](@entry_id:267133).

### GNSS-R as a Bistatic Radar System

At its core, GNSS-R is a form of **[bistatic radar](@entry_id:1121676)**. A radar system is defined as bistatic when its transmitter and receiver are located at significantly different positions. In the context of GNSS-R, the transmitters are the satellites of GNSS constellations (e.g., GPS, Galileo, GLONASS), which continuously illuminate the Earth with signals of opportunity. The receiver, typically airborne or spaceborne, is a separate, passive instrument that measures the energy scattered from the surface. This configuration contrasts sharply with two other common remote sensing modalities: monostatic radar and passive [radiometry](@entry_id:174998) .

A **monostatic radar**, such as a conventional radar [altimeter](@entry_id:264883) or a [synthetic aperture radar](@entry_id:755751) (SAR), employs a co-located transmitter and receiver. It actively illuminates a target and measures the energy scattered directly back toward the source, a quantity known as **backscatter**. The measurement is characterized by the normalized [backscattering](@entry_id:142561) coefficient, $\sigma^0$.

In contrast, a **passive radiometer** is not a radar at all; it is a passive system that measures the natural thermal [electromagnetic radiation](@entry_id:152916) emitted by the surface. The primary observable is the **brightness temperature**, $T_B$, which, according to the Rayleigh-Jeans approximation and Kirchhoff's law of thermal radiation, is proportional to the product of the surface's physical temperature and its emissivity, $\epsilon$.

GNSS-R occupies a unique space between these modalities. Like a radar, it measures scattered energy from an external source, not thermal emission. However, because the transmitter (the GNSS satellite) and the receiver are spatially separated, the geometry is bistatic, and the measurement is sensitive to **forward scatter** around the specular reflection point. The scattering is characterized by a **bistatic [radar cross-section](@entry_id:754000)**, $\sigma_b$. The use of signals that were not intended for this purpose classifies GNSS-R as a "signal of opportunity" remote sensing technique .

### The Direct and Reflected Signal Path

The measurement principle of GNSS-R relies on comparing the signal received directly from the satellite with the signal that has reflected off the Earth's surface. These two signal paths impart distinct and informative transformations upon the signal, which are fundamental to the retrieval process .

A GNSS-R receiver typically utilizes two antennas: an upward-looking antenna to receive the direct, line-of-sight signal, and a downward-looking antenna to capture the reflected signal. The GNSS satellites transmit Right-Hand Circularly Polarized (RHCP) signals in the L-band.

*   **Polarization:** Upon quasi-[specular reflection](@entry_id:270785) from a dielectric interface like a calm water body, fundamental [electromagnetic boundary conditions](@entry_id:188865) cause a reversal in the signal's polarization handedness. The incident RHCP signal becomes predominantly Left-Hand Circularly Polarized (LHCP) after reflection. For this reason, the downward-looking antenna on a GNSS-R instrument is typically designed to be sensitive to LHCP signals to maximize the reception of the reflected energy. For very rough surfaces, the scattering becomes more diffuse, and the reflected signal becomes more depolarized, containing a mix of both RHCP and LHCP components.

*   **Path Delay:** The path taken by the reflected signal, from the satellite to the surface and then to the receiver ($R_{ts} + R_{sr}$), is geometrically longer than the direct path from the satellite to the receiver ($R_d$). Consequently, the reflected signal arrives at the receiver with an **excess path delay**, $\Delta \tau = (R_{ts} + R_{sr} - R_d)/c$, where $c$ is the speed of light. This delay is a primary observable used to geolocate the reflection point and, in some applications, to measure the height of the receiver above the surface.

*   **Doppler Shift:** Both the direct and reflected signals experience a Doppler shift due to the relative motion between the satellite and the receiver. The Doppler shift is defined as $f_D = -(1/\lambda) dR/dt$, where $\lambda$ is the wavelength and $R$ is the path length. Because the geometric paths $R_d$ and $R_b = R_{ts} + R_{sr}$ are different and their time derivatives are generally not equal, the direct and reflected signals will have different Doppler shifts. The Doppler of the reflected signal is determined by the rate of change of the entire bistatic path, which depends on the velocities of the satellite, the receiver, and the motion of the specular point on the surface.

*   **Coherence:** Coherence refers to the stability of the signal's phase over time. The direct signal from the satellite is highly coherent. The coherence of the reflected signal, however, is a strong function of the surface state. For a very smooth surface like calm water, the reflection is specular and highly coherent. As the surface roughness increases, the signal scatters from many different points, each imparting a random phase shift. This leads to rapid decorrelation and a loss of coherence.

### The Bistatic Radar Equation: A Quantitative Framework

The power of the reflected signal captured by the receiver can be quantitatively described by the **[bistatic radar](@entry_id:1121676) equation**. This equation provides the crucial link between the properties of the transmitter, the surface, the receiver, and the geometry of the observation. The derivation proceeds from first principles of wave propagation and antenna theory .

1.  The GNSS satellite transmits with an **Effective Isotropic Radiated Power**, denoted as $\mathrm{EIRP}$. This is the power that would be needed for an [isotropic antenna](@entry_id:263217) to produce the same power density in the direction of the target. At a distance $R_t$ (transmitter-to-target range), the power density incident on the surface is given by the [inverse-square law](@entry_id:170450): $S_t = \frac{\mathrm{EIRP}}{4\pi R_t^2}$.

2.  The surface intercepts this power and scatters it. The **bistatic [radar cross section](@entry_id:754002)**, $\sigma_b$, defines the [effective area](@entry_id:197911) of the surface that scatters power towards the receiver. The power scattered in the direction of the receiver, as if it were radiated isotropically, is $P_{scat} = S_t \cdot \sigma_b$.

3.  This scattered power propagates over the target-to-receiver range, $R_r$. The power density at the receiver is again subject to inverse-square law spreading: $S_r = \frac{P_{scat}}{4\pi R_r^2} = \frac{\mathrm{EIRP} \cdot \sigma_b}{(4\pi)^2 R_t^2 R_r^2}$.

4.  The receiver's antenna, with gain $G_r$, captures this power over its [effective area](@entry_id:197911), $A_e = \frac{G_r \lambda^2}{4\pi}$. The captured power is $P_r = S_r \cdot A_e$.

Combining these steps and including a term $L \ge 1$ to account for miscellaneous system and atmospheric losses, we arrive at the [bistatic radar](@entry_id:1121676) equation for GNSS-R:

$$P_r = \frac{\mathrm{EIRP}\; G_r\; \lambda^2\; \sigma_b}{(4\pi)^3\; R_t^2\; R_r^2\; L}$$

This equation demonstrates that the received power is directly proportional to the surface's bistatic [radar cross section](@entry_id:754002) $\sigma_b$. Since $\sigma_b$ is determined by the surface's roughness and dielectric properties, this equation forms the basis for inverting the measured power to retrieve geophysical parameters.

### Surface Scattering Mechanisms and Sensitivities

The ability of GNSS-R to sense properties like soil moisture and ocean roughness is rooted in how the L-band signals interact with the surface materials and geometry.

#### The Advantage of L-Band Signals

The use of L-band frequencies (around $1.2-1.6$ GHz, $\lambda \approx 19-24$ cm) is a key enabling factor for many GNSS-R applications, particularly when compared to higher-frequency microwave sensors .

*   **Penetration Depth:** Electromagnetic waves are attenuated as they propagate through [lossy media](@entry_id:1127459) like soil and water. The attenuation constant, $\alpha$, generally increases with frequency. For conducting media like seawater, the skin depth $\delta = 1/\alpha$ scales as $\delta \propto 1/\sqrt{\omega}$, where $\omega$ is the angular frequency. Consequently, lower-frequency L-band signals penetrate deeper into the subsurface than higher-frequency signals (e.g., X-band or Ku-band). This allows GNSS-R to sense root-zone soil moisture rather than just the immediate surface, and makes it less susceptible to confounding effects from very thin surface layers on the ocean, such as foam.

*   **Sensitivity to Water Content:** The sensitivity to soil moisture is driven by the large dielectric contrast between dry soil and water. The dielectric constant of liquid water exhibits a strong frequency dependence known as **Debye dispersion**. At L-band frequencies, the real part of water's relative permittivity, $\epsilon'$, is near its maximum static value of approximately $80$. At higher microwave frequencies (e.g., X-band, $\sim 10$ GHz), $\epsilon'$ is significantly lower. This means that for a given amount of water added to soil, the change in the bulk dielectric constant of the soil-water mixture is much larger at L-band. According to the Fresnel reflection equations, this larger dielectric contrast translates into a much larger change in surface reflectivity, granting L-band measurements superior sensitivity to variations in soil moisture .

#### Coherent and Incoherent Scattering

The nature of the scattering process is governed by the vertical scale of the surface roughness, quantified by the root-mean-square (RMS) height $\sigma$, relative to the wavelength $\lambda$ and the incidence angle $\theta$.

When a coherent wave reflects from a rough surface, the path length for each point on the surface differs, inducing a random phase shift in the reflected field. For a surface with a Gaussian height distribution, the statistical averaging of these [phase shifts](@entry_id:136717) leads to an attenuation of the coherent (specular) component of the reflected power. This [attenuation factor](@entry_id:1121239), which multiplies the power that would be reflected from a perfectly smooth surface, is given by:

$$ \mathcal{R}_{\text{spec}} = \exp(-4k^2\sigma^2\cos^2\theta) $$

where $k = 2\pi/\lambda$ is the wavenumber . This exponential term is a cornerstone of rough surface scattering models.

This expression leads to the **Rayleigh criterion for roughness**. The scattering is considered predominantly **coherent** (smooth) when the argument of the exponential is much less than one, and predominantly **incoherent** (rough) when it is much greater than one. A useful threshold is the **vertical [coherence length](@entry_id:140689)**, $\ell_c$, defined as the RMS height $\sigma$ for which the coherent power is attenuated by a factor of $1/e$. This occurs when the exponent's magnitude is one:

$$ 4k^2 \ell_c^2 \cos^2\theta = 1 \implies \ell_c = \frac{1}{2k\cos\theta} = \frac{\lambda}{4\pi\cos\theta} $$

Thus, the scattering regime can be classified by comparing the [surface roughness](@entry_id:171005) $\sigma$ to this characteristic length $\ell_c(\theta, \lambda)$. If $\sigma \ll \ell_c$, the surface acts as a specular reflector. If $\sigma \gg \ell_c$, the specular component is negligible, and the scattering is diffuse or incoherent .

#### Theoretical Scattering Models

To build a quantitative forward model that relates surface properties to the bistatic cross section $\sigma_b$, physicists employ analytical scattering theories. The choice of model depends on the values of the dimensionless parameters $k\sigma$ and $kL$, where $L$ is the horizontal [correlation length](@entry_id:143364) of the roughness .

*   The **Kirchhoff Approximation (KA)**, also known as the [physical optics](@entry_id:178058) model, is valid for surfaces that are locally flat, meaning their radius of curvature is large compared to the wavelength. This condition is met when $kL \gg 1$. The KA does not require the [surface roughness](@entry_id:171005) height to be small, so it can be valid even when $k\sigma \ge 1$. This model is highly appropriate for describing the quasi-specular scattering from gently undulating surfaces like the ocean, where the return signal is concentrated in a "glistening zone" around the specular point.

*   The **Small Perturbation Method (SPM)** is based on a [perturbative expansion](@entry_id:159275) of the scattered field in powers of the surface height. Its validity requires the [surface roughness](@entry_id:171005) to be much smaller than the wavelength, i.e., $k\sigma \ll 1$. It does not, however, require the surface to be locally flat ($kL$ can be of order unity or smaller). SPM is more suitable for describing scattering from surfaces with small-amplitude, possibly high-frequency roughness.

For many GNSS-R applications over the ocean, where at L-band $k\sigma$ can be greater than $1$ and $kL$ is much greater than $1$, the Kirchhoff approximation is the more applicable physical model .

### Signal Processing and Observables

The raw signal captured by the receiver antenna must undergo significant processing to yield the fundamental GNSS-R observable. This processing is designed to isolate the very weak reflected signal from background noise and to map its distribution in terms of delay and Doppler.

#### The Delay-Doppler Map (DDM)

The cornerstone of GNSS-R signal processing is correlation. The incoming signal from the downward-looking antenna, $r(t)$, is correlated with a clean, locally generated replica of the satellite's pseudorandom noise (PRN) code, $s(t)$. This is performed over a grid of trial delays, $\tau$, and trial Doppler shifts, $f$, to search for the reflected signal. The result of this two-dimensional correlation process is the **Delay-Doppler Map (DDM)**.

Mathematically, the DDM is the power of the complex cross-[ambiguity function](@entry_id:199061) between the received signal and the code replica, computed over a coherent integration time $T_c$:

$$ \mathrm{DDM}(\tau,f) = \left| \int_{0}^{T_c} r(t) s^{*}(t-\tau) e^{-j2\pi f t} dt \right|^2 $$

The DDM represents the distribution of scattered power as a function of delay and Doppler. The shape, peak power, and extent of the DDM are directly related to the surface's bistatic cross section and roughness .

#### The Woodward Ambiguity Function and Resolution

The DDM is effectively a "smeared" version of the true surface [scattering function](@entry_id:190527). The "smearing" function is the instrument's own response to an ideal point scatterer, known as the **Woodward Ambiguity Function (WAF)**. The WAF is the auto-[ambiguity function](@entry_id:199061) of the transmitted waveform itself (approximated by the local code replica $c(t)$ over the integration interval):

$$ \mathrm{WAF}(\tau,f) = \left| \int_{0}^{T_c} c(t) c^{*}(t-\tau) e^{-j2\pi f t} dt \right|^2 $$

The shape of the WAF determines the intrinsic resolution of the measurement . For PRN codes used in GNSS, the WAF is sharply peaked in delay, with a width determined by the code's chip duration. The **delay resolution** is thus set by the chip rate of the PRN code. In the Doppler dimension, the WAF's shape is determined by the Fourier transform of the time-window of the coherent integration. For a [rectangular window](@entry_id:262826) of duration $T_c$, this response is a [sinc function](@entry_id:274746) with a [main lobe width](@entry_id:274761) proportional to $1/T_c$. Thus, the **Doppler resolution** is inversely proportional to the coherent integration time.

#### Limits on Coherent Integration

While a longer coherent integration time $T_c$ improves Doppler resolution and increases the signal-to-noise ratio against thermal noise, there are fundamental limits to how long one can integrate coherently.

*   **Surface Dynamics:** If the scattering surface itself is changing rapidly (e.g., due to ocean waves), the phase of the reflected signal will decorrelate over a characteristic **[coherence time](@entry_id:176187)**. Integrating for a duration $T_c$ significantly longer than this surface [coherence time](@entry_id:176187) will average out the signal, smearing the DDM and reducing its peak power .

*   **Ionospheric Scintillation:** A major external error source is the fluctuation in the signal's phase caused by propagation through irregularities in the [ionosphere](@entry_id:262069). This phenomenon, known as **ionospheric scintillation**, introduces a random phase wander, $\phi_i(t)$. The power spectral density of these fluctuations typically follows a power law, $S_{\phi}(f) \propto f^{-p}$, with $p$ often between $2$ and $3$. For this type of colored noise, where power is concentrated at low frequencies, the variance of the phase averaged over an interval $T_c$ *increases* with the integration time, scaling as $\sigma_{\phi,T_c}^{2} \propto T_c^{p-1}$. This growing phase variance causes a loss of coherence, $\exp(-\frac{1}{2}\sigma_{\phi,T_c}^2)$, which again limits the useful duration of $T_c$. To mitigate this degradation, advanced signal processing is required. Robust strategies involve **[polynomial detrending](@entry_id:1129923)** of the measured phase to remove the low-frequency wander, and the application of tapered **[windowing functions](@entry_id:139733)** (e.g., a Hann window) during correlation. Tapered windows have lower spectral sidelobes than a simple [rectangular window](@entry_id:262826), which significantly reduces the leakage of the strong [low-frequency noise](@entry_id:1127472) into the measurement bandwidth, thereby maximizing the achievable coherence .