## Introduction
The temperature of the Earth's surface is a fundamental variable that drives weather, climate, and ecosystem processes. Satellites equipped with thermal infrared sensors provide a unique capability to monitor Land Surface Temperature (LST) and Sea Surface Temperature (SST) globally and continuously. However, the radiance measured by a satellite is not a direct reflection of surface temperature. As thermal radiation journeys from the surface to the sensor, it is absorbed, emitted, and scattered by the atmosphere, creating a significant discrepancy between the satellite measurement and the true surface condition. This article addresses this critical knowledge gap by providing a comprehensive guide to atmospheric correction, the process of removing these atmospheric effects to retrieve accurate surface temperature.

This article is structured to build your expertise from the ground up. In the "Principles and Mechanisms" chapter, you will explore the fundamental physics of radiative transfer, including Planck's Law, Kirchhoff's Law, and the formulation of the Radiative Transfer Equation. We will dissect the key challenges, such as the Temperature-Emissivity Separation problem and the influence of clouds. Following this, the "Applications and Interdisciplinary Connections" chapter demonstrates how these principles are put into practice. You will learn about operational retrieval algorithms like the split-window technique and see how the resulting temperature data fuel advancements in hydrology, geology, [urban planning](@entry_id:924098), and public health. Finally, the "Hands-On Practices" section will challenge you to apply your knowledge by implementing core algorithms, bridging the gap between theory and operational data processing.

## Principles and Mechanisms

The retrieval of [land surface temperature](@entry_id:1127055) and emissivity from satellite-based thermal infrared (TIR) measurements is a cornerstone of modern [environmental remote sensing](@entry_id:1124564). The process is fundamentally one of inversion, where the radiance measured by a sensor at the top of the atmosphere (TOA) is used to infer properties of the Earth's surface. However, the radiation emitted by the surface is significantly modified as it traverses the atmosphere. The atmosphere absorbs, emits, and scatters radiation, confounding the direct interpretation of the TOA signal. Atmospheric correction is the critical process of modeling and removing these atmospheric effects to isolate the true surface-leaving radiance. This chapter delineates the fundamental physical principles and mechanisms that govern this process.

### The Radiative Transfer Equation for the Thermal Infrared

The journey of thermal radiation from the Earth's surface to a satellite sensor is described by the Radiative Transfer Equation (RTE). In the thermal infrared portion of the spectrum (typically $3–15\,\mu\mathrm{m}$), scattering by atmospheric gas molecules is negligible, and for clear-sky conditions, scattering by aerosols is often treated as a secondary effect compared to molecular absorption and emission. Under these conditions, and assuming a plane-parallel atmosphere in Local Thermodynamic Equilibrium (LTE), the RTE simplifies considerably.

The total [spectral radiance](@entry_id:149918) measured by a sensor at the top of the atmosphere, $L_{\lambda}^{\mathrm{toa}}$, is the sum of radiance originating from the surface that is transmitted through the atmosphere, and the radiance emitted by the atmospheric path itself toward the sensor. This can be conceptually written as:

$L_{\lambda}^{\mathrm{toa}} = (\text{Surface Radiance Transmitted to Space}) + (\text{Atmospheric Path Radiance})$

To understand this equation fully, we must dissect each term based on its physical origin .

#### Surface-Leaving Radiance

The radiance leaving the surface, $L_{\lambda}^{\mathrm{sfc}}$, is itself a composite of two processes: thermal emission from the surface and the reflection of downwelling atmospheric radiation by the surface.

1.  **Thermal Emission**: All objects with a temperature above absolute zero emit thermal radiation. The theoretical upper limit of this emission is described by **Planck's Law**, which gives the spectral radiance $B_{\lambda}(T)$ of a perfect emitter, known as a **blackbody**, at a given [absolute temperature](@entry_id:144687) $T$ and wavelength $\lambda$ :
    $$
    B_{\lambda}(T) = \frac{2 h c^2}{\lambda^5} \frac{1}{\exp\left(\frac{h c}{\lambda k_B T}\right) - 1}
    $$
    Here, $h$ is Planck's constant, $c$ is the speed of light in vacuum, and $k_B$ is Boltzmann's constant. Real-world surfaces, however, are not perfect emitters. Their ability to emit radiation is quantified by the **spectral emissivity**, $\epsilon_{\lambda}$, defined as the ratio of the radiance emitted by the surface to the radiance that would be emitted by a blackbody at the same temperature. Thus, the emitted component of the surface-leaving radiance is $\epsilon_{\lambda} B_{\lambda}(T_s)$, where $T_s$ is the true kinetic temperature of the surface.

2.  **Reflected Downwelling Radiance**: The atmosphere itself radiates energy downwards, creating a field of downwelling [spectral radiance](@entry_id:149918), $L_{\lambda}^{\mathrm{down}}$, that illuminates the surface. A portion of this incident radiation is reflected upwards. The fraction of incident radiation reflected is given by the **spectral reflectivity**, $\rho_{\lambda}$. For an **opaque** surface, which by definition does not transmit radiation, the principles of energy conservation and thermal equilibrium lead to a simple and powerful relationship. At any given wavelength, the fraction of energy absorbed ($\alpha_{\lambda}$) plus the fraction reflected must equal one: $\alpha_{\lambda} + \rho_{\lambda} = 1$. **Kirchhoff's Law of Thermal Radiation** states that for a body in LTE, its absorptivity is equal to its emissivity: $\alpha_{\lambda} = \epsilon_{\lambda}$. Combining these principles for an opaque surface yields the fundamental relation :
    $$
    \epsilon_{\lambda} + \rho_{\lambda} = 1
    $$
    This implies that a good emitter is a poor reflector, and vice versa. The reflected component of the surface-leaving radiance is therefore $\rho_{\lambda} L_{\lambda}^{\mathrm{down}} = (1 - \epsilon_{\lambda}) L_{\lambda}^{\mathrm{down}}$. The precise formulation of this term depends on the angular properties of the surface reflection and the downwelling [radiation field](@entry_id:164265). For a surface that reflects isotropically (a **Lambertian** surface) illuminated by an isotropic downwelling field, the reflected radiance is indeed $(1 - \epsilon_{\lambda}) L_{\lambda}^{\mathrm{down}}$ .

Combining the emitted and reflected components, the total upwelling spectral radiance just above the surface is:
$$
L_{\lambda}^{\mathrm{sfc}} = \epsilon_{\lambda} B_{\lambda}(T_s) + (1 - \epsilon_{\lambda}) L_{\lambda}^{\mathrm{down}}
$$

#### Atmospheric Transmission and Path Radiance

As the surface-leaving radiance travels upward to the sensor, it is attenuated by the atmosphere. This process is governed by the **Beer-Lambert Law**. The **spectral transmittance**, $\tau_{\lambda}$, is the fraction of radiation at a specific wavelength that passes through the atmosphere without being absorbed. It is an [exponential function](@entry_id:161417) of the [optical depth](@entry_id:159017) of the path. For a nadir-viewing sensor, the transmittance from the surface to space is given by integrating the absorption properties of the constituent gases through the atmospheric column :
$$
\tau_{\lambda} = \exp\left( -\int_{0}^{H} \sum_{i} \kappa_{i,\lambda}(z) \rho_i(z) \, \mathrm{d}z \right)
$$
where $H$ is the top of the atmosphere, $\kappa_{i,\lambda}(z)$ is the mass [absorption coefficient](@entry_id:156541) of gas species $i$ at altitude $z$, and $\rho_i(z)$ is its density. For an off-nadir view with zenith angle $\theta$, the path length through each atmospheric layer increases by a factor of approximately $\sec\theta$, increasing the [optical depth](@entry_id:159017) and decreasing the transmittance.

Simultaneously, the atmosphere emits its own thermal radiation in all directions. The portion emitted upward along the sensor's line of sight is known as the **upwelling path radiance**, $L_{\lambda}^{\mathrm{up}}$. This radiance is the integrated contribution of emission from all atmospheric layers between the surface and the sensor, with each layer's contribution being attenuated by the part of the atmosphere above it. The downwelling radiance, $L_{\lambda}^{\mathrm{down}}$, is formed by a similar process of downward emission.

#### The Full Radiative Transfer Equation

Assembling all the components, we arrive at the full [radiative transfer equation](@entry_id:155344) for the TOA spectral radiance measured by a satellite sensor  :
$$
L_{\lambda}^{\mathrm{toa}} = \tau_{\lambda} \Big[ \epsilon_{\lambda} B_{\lambda}(T_s) + (1 - \epsilon_{\lambda}) L_{\lambda}^{\mathrm{down}} \Big] + L_{\lambda}^{\mathrm{up}}
$$
This equation is the fundamental forward model in [thermal remote sensing](@entry_id:1133019). It describes how the surface properties ($T_s$, $\epsilon_{\lambda}$) and atmospheric properties ($\tau_{\lambda}$, $L_{\lambda}^{\mathrm{up}}$, $L_{\lambda}^{\mathrm{down}}$) combine to produce the signal measured by the satellite.

### The Goal of Atmospheric Correction

A sensor measures $L_{\lambda}^{\mathrm{toa}}$. From this measurement, a **brightness temperature**, $T_b$, can be calculated. It is defined as the temperature a perfect blackbody would need to have to produce the same radiance level, i.e., $B_{\lambda}(T_b) = L_{\lambda}^{\mathrm{toa}}$ .

It is a common misconception to equate this brightness temperature with the true surface temperature, $T_s$. The presence of the atmosphere and the fact that most surfaces are not blackbodies ($\epsilon_{\lambda}  1$) cause a significant discrepancy. Typically, for a surface warmer than the atmosphere, both [atmospheric absorption](@entry_id:1121179) (since $\tau_{\lambda}  1$) and non-unity emissivity reduce the signal reaching the sensor. While the atmospheric path radiance $L_{\lambda}^{\mathrm{up}}$ adds to the signal, this contribution is generally from the colder atmosphere. The net effect is that the measured TOA radiance is less than the radiance that would be emitted by a blackbody at the surface temperature, $B_{\lambda}(T_s)$. Consequently, the uncorrected brightness temperature is usually lower than the true surface temperature: $T_b  T_s$.

The goal of atmospheric correction is to "invert" the RTE. By estimating the atmospheric parameters ($\tau_{\lambda}$, $L_{\lambda}^{\mathrm{up}}$, $L_{\lambda}^{\mathrm{down}}$) using atmospheric models or ancillary data, we can rearrange the RTE to solve for the radiance term originating purely from surface emission, $\epsilon_{\lambda} B_{\lambda}(T_s)$, or more fundamentally, for the blackbody radiance corresponding to the true surface temperature, $B_{\lambda}(T_s)$ :
$$
B_{\lambda}(T_s) = \frac{1}{\tau_{\lambda} \epsilon_{\lambda}} \left( L_{\lambda}^{\mathrm{toa}} - L_{\lambda}^{\mathrm{up}} \right) - \frac{1 - \epsilon_{\lambda}}{\epsilon_{\lambda}} L_{\lambda}^{\mathrm{down}}
$$
Once $B_{\lambda}(T_s)$ is determined, the Planck function can be inverted to find $T_s$. This equation makes it clear that accurate retrieval of $T_s$ depends critically on knowing not only the atmospheric state but also the surface emissivity, $\epsilon_{\lambda}$.

### Atmospheric Windows and Key Spectral Regimes

The feasibility of [thermal remote sensing](@entry_id:1133019) of the surface relies on the existence of **[atmospheric windows](@entry_id:1121214)**—spectral regions where [atmospheric absorption](@entry_id:1121179) is relatively weak, meaning transmittance $\tau_{\lambda}$ is high. In these windows, a larger fraction of the surface signal reaches the sensor, making the retrieval less sensitive to uncertainties in the atmospheric correction parameters .

The primary [thermal infrared window](@entry_id:1133005) for Earth observation lies between approximately $8\,\mu\mathrm{m}$ and $14\,\mu\mathrm{m}$. This region is known as the **Long-Wave Infrared (LWIR)**. Even within this window, the atmosphere is not perfectly transparent. The dominant absorbing and emitting gas is **water vapor**, whose concentration is highly variable in space and time. The absorption is due to the far wings of strong absorption lines located elsewhere and a poorly understood "continuum" absorption. The **total column water vapor** ($W$), defined as the vertically integrated mass of water vapor per unit area, $W = \int_{0}^{\infty}\rho_v(z)\,\mathrm{d}z$, is the primary determinant of $\tau_{\lambda}$ and $L_{\lambda}^{\mathrm{up}}$ in this window. Higher water vapor content leads to lower transmittance and higher path radiance . Modern techniques, such as the **split-window approach**, use measurements at two or more nearby wavelengths within the $10–12\,\mu\mathrm{m}$ region where water vapor absorption differs slightly. This differential absorption allows for an estimation and correction of the water vapor effect .

Another important window lies in the **Mid-Wave Infrared (MWIR)**, from about $3\,\mu\mathrm{m}$ to $5\,\mu\mathrm{m}$. Comparing the LWIR and MWIR reveals critical differences for atmospheric correction, particularly for daytime observations . For a typical Earth surface temperature of $300\,\mathrm{K}$, the peak of thermal emission occurs around $9.7\,\mu\mathrm{m}$ (in the LWIR). The emitted radiance in the MWIR (e.g., at $4\,\mu\mathrm{m}$) is more than an order of magnitude lower. In contrast, the incoming solar spectrum, characteristic of a $\sim 5778\,\mathrm{K}$ blackbody, is still significantly strong in the MWIR but has fallen to negligible levels in the LWIR.

During the day, this leads to a critical complication in the MWIR: the measured radiance contains not only thermal emission from the surface and atmosphere but also a significant component of reflected solar radiation. The combination of a weak thermal signal and a strong contaminating solar signal makes daytime MWIR measurements highly susceptible to errors if the solar reflection is not meticulously corrected. In the LWIR, the solar component is so small that it can almost always be ignored. Furthermore, scattering by aerosols, which is more efficient at shorter wavelengths, can be a relevant contributor to path radiance in the MWIR during daytime but is typically negligible in the LWIR .

### Advanced Challenges in Atmospheric Correction

While the principles outlined above form the basis of atmospheric correction, several advanced challenges complicate the practical application.

#### The Temperature-Emissivity Separation (TES) Problem

The inverted RTE shows that to find $T_s$, we must know $\epsilon_{\lambda}$. However, emissivity is also an unknown property of the surface that often varies with wavelength. This leads to a fundamental ambiguity known as the **Temperature-Emissivity Separation (TES) problem** .

Consider a multispectral sensor measuring radiance in $N$ thermal bands. After atmospheric correction, we are left with a system of $N$ equations, one for each band's surface-leaving radiance:
$L_i = \epsilon_i B_i(T_s) + (1 - \epsilon_i) L_{i}^{\mathrm{down}}$, for $i=1, ..., N$.

In this system, we have $N$ measurements ($L_i$), but we have $N+1$ unknowns: the single surface temperature $T_s$ and the $N$ emissivity values ($\epsilon_1, ..., \epsilon_N$). With more unknowns than equations, the system is mathematically **underdetermined** or **ill-posed**. An infinite number of combinations of $T_s$ and $\{\epsilon_i\}$ can produce the same measured radiances. For example, a lower temperature can be compensated for by a higher emissivity, and vice versa. To solve the TES problem, additional constraints or assumptions must be introduced, such as assuming a known emissivity in one channel, assuming a particular spectral shape for the emissivity, or using multi-angle or multi-temporal observations.

#### Sensor Spectral Response and Band-Averaged Quantities

The RTE is defined for monochromatic (single-wavelength) radiation. Real sensors, however, measure radiance over a finite spectral band, characterized by a **spectral response function**, $R(\lambda)$. To bridge this gap, the spectral quantities in the RTE must be properly convolved to produce physically consistent band-averaged values .

The band-averaged radiance, $L_{\text{band}}$, measured by a sensor is the $R(\lambda)$-weighted average of the [spectral radiance](@entry_id:149918):
$$
L_{\text{band}} = \frac{\int R(\lambda) L(\lambda) \, \mathrm{d}\lambda}{\int R(\lambda) \, \mathrm{d}\lambda}
$$
A more complex issue arises when defining an effective band transmittance, $\tau_{\text{band}}$. It is tempting to define it as a simple weighted average of $\tau(\lambda)$. However, to preserve the multiplicative structure of the RTE ($L_{\text{transmitted}} = \tau S_{\text{source}}$), the effective band transmittance must be weighted by the source spectrum itself. For a source spectrum $S(\lambda)$, the correct definition is:
$$
\tau_{\text{band}} = \frac{\int R(\lambda) \tau(\lambda) S(\lambda) \, \mathrm{d}\lambda}{\int R(\lambda) S(\lambda) \, \mathrm{d}\lambda}
$$
This crucial result shows that **effective band transmittance is not a property of the atmosphere alone but also depends on the spectrum of the radiation being transmitted**. For example, the effective transmittance for the surface emission term (where $S(\lambda) \approx B(\lambda, T_s)$) will be different from the effective transmittance for the reflected solar term. This detail must be handled carefully in high-accuracy retrieval algorithms.

#### The Influence of Clouds

The presence of clouds dramatically alters the radiative transfer problem. Opaque clouds completely obscure the surface, and the measured radiance relates to the cloud-top temperature. More complex are **semitransparent clouds**, such as thin cirrus, which are common and can be difficult to detect.

A semitransparent cloud acts as an additional layer in the atmosphere. It attenuates the radiation from below while adding its own thermal emission. We can model a simple case of a uniform, isothermal cirrus layer at temperature $T_c$ with transmittance $\tau_c$ located below a clear atmospheric layer with transmittance $\tau_a$ and path radiance $L_a^{\uparrow}$. Assuming a blackbody surface ($\epsilon_s=1$) at temperature $T_s$, the radiance reaching the top of the cirrus cloud is a sum of the transmitted surface radiance and the cloud's own emission. The cloud's emissivity, by Kirchhoff's Law, is $\epsilon_c = 1-\tau_c$. The TOA radiance is then given by :
$$
L_{\mathrm{TOA}} = \tau_a \left[ \tau_c B(T_s) + (1 - \tau_c) B(T_c) \right] + L_a^{\uparrow}
$$
This two-layer model demonstrates how the presence of a semitransparent cloud significantly cools the apparent brightness temperature, as the cold cloud both obscures the warmer surface signal and emits at its own colder temperature. Failure to detect and correct for such clouds is a major source of error in surface temperature retrieval.