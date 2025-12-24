## Introduction
Observing the light from a planet orbiting a distant star is a monumental challenge in modern astronomy. Yet, within that faint signal lies a wealth of information about an alien world's atmosphere—its temperature, chemical makeup, and even its weather patterns. The primary tools for decoding this information are [emission spectroscopy](@entry_id:186353) and the analysis of [thermal phase curves](@entry_id:1133014), which measure the heat radiated by the planet itself. The core problem this article addresses is how to translate the observed flux from an exoplanet into a detailed portrait of its atmospheric structure and dynamics. This requires a deep and quantitative physical framework that connects the microscopic processes within the gas to the integrated light we capture with our telescopes.

To build this understanding, we will progress through three distinct chapters. The first, **Principles and Mechanisms**, lays the theoretical groundwork, starting from the fundamental physics of thermal radiation (the Planck function) and its journey through a gaseous medium as described by the [radiative transfer equation](@entry_id:155344). We will explore how the local state of the gas, under the crucial assumption of Local Thermodynamic Equilibrium (LTE), determines its opacity and emission, and how these local properties scale up to create global phenomena like hotspot displacement. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how this theoretical toolkit is used in practice to probe atmospheric structure, disentangle competing physical processes, and connect atmospheric properties to broader climate regimes. Finally, **Hands-On Practices** provides a series of computational problems designed to solidify these concepts, guiding you through building models for energy balance, radiative transfer, and understanding the systematic biases inherent in data interpretation.

## Principles and Mechanisms

The interpretation of thermal emission from an exoplanet requires a robust physical framework that connects the microscopic processes of absorption and emission within its atmosphere to the macroscopic, observable quantities of [spectral radiance](@entry_id:149918) and its variation with orbital phase. This chapter establishes the foundational principles and mechanisms that govern this connection. We begin with the fundamental law of thermal radiation, proceed through the theory of how this radiation is transferred through a gaseous medium, explore the microscopic physics that determines the [atmospheric opacity](@entry_id:1121203), and conclude by linking these concepts to the global energy balance and atmospheric dynamics that shape the observable [thermal phase curves](@entry_id:1133014).

### The Spectrum of Thermal Emission: The Planck Function

All matter at a finite temperature emits [electromagnetic radiation](@entry_id:152916). For an idealized object known as a **blackbody**—one that perfectly absorbs all incident radiation—the [spectral distribution](@entry_id:158779) of this emitted energy is described by a universal function of temperature. This function, derived by Max Planck from the principles of quantized oscillators and statistical mechanics, is known as the **Planck function**. It is the cornerstone for understanding thermal emission from astronomical objects, including stars and planets. The Planck function can be expressed in two forms: per unit frequency, $B_{\nu}(T)$, or per unit wavelength, $B_{\lambda}(T)$.

The spectral radiance per unit frequency, $B_{\nu}(T)$, represents the energy emitted per unit time, per unit projected area, per unit [solid angle](@entry_id:154756), and per unit frequency interval. Its form is:

$B_{\nu}(T) = \dfrac{2 h \nu^{3}}{c^{2}} \left[\exp\left(\dfrac{h \nu}{k_B T}\right) - 1\right]^{-1}$

where $h$ is the Planck constant, $\nu$ is the frequency, $c$ is the speed of light, $k_B$ is the Boltzmann constant, and $T$ is the absolute temperature. The units of $B_{\nu}(T)$ are typically $\mathrm{W\,m^{-2}\,sr^{-1}\,Hz^{-1}}$.

Similarly, the spectral radiance per unit wavelength, $B_{\lambda}(T)$, is given by:

$B_{\lambda}(T) = \dfrac{2 h c^{2}}{\lambda^{5}} \left[\exp\left(\dfrac{h c}{\lambda k_B T}\right) - 1\right]^{-1}$

where $\lambda$ is the wavelength. The units of $B_{\lambda}(T)$ are typically $\mathrm{W\,m^{-2}\,sr^{-1}\,m^{-1}}$.

It is crucial to understand that one form cannot be obtained from the other by a simple substitution of $\nu = c/\lambda$. The two functions represent densities over different variables, and their relationship must preserve the energy radiated in an infinitesimal spectral interval. That is, the energy element must be conserved: $B_{\lambda}(T) |d\lambda| = B_{\nu}(T) |d\nu|$. This implies a transformation rule involving the Jacobian of the change of variables:

$B_{\lambda}(T) = B_{\nu}(T)\big|_{\nu = c/\lambda} \left| \dfrac{d\nu}{d\lambda} \right|$

Since $\nu = c/\lambda$, the Jacobian is $\dfrac{d\nu}{d\lambda} = -\dfrac{c}{\lambda^2}$. The absolute value is essential because radiance must be a positive quantity. Therefore, $\left| \dfrac{d\nu}{d\lambda} \right| = \dfrac{c}{\lambda^{2}}$. Applying this transformation correctly yields the expression for $B_{\lambda}(T)$ from $B_{\nu}(T)$. 

In certain physical regimes, the Planck function can be simplified into useful approximations. These limits are determined by the ratio of the [photon energy](@entry_id:139314), $h\nu$, to the characteristic thermal energy of the gas, $k_B T$.

-   The **Rayleigh–Jeans approximation** is valid at low frequencies or long wavelengths, where $h \nu \ll k_B T$. In this limit, the exponential in the denominator of the Planck function can be approximated by $\exp(x) \approx 1 + x$, leading to $B_{\nu}(T) \approx \frac{2 \nu^2 k_B T}{c^2}$. This approximation, which famously failed at high frequencies (the "[ultraviolet catastrophe](@entry_id:145753)") in classical physics, shows that thermal emission is directly proportional to temperature in the long-wavelength limit.

-   The **Wien approximation** is valid at high frequencies or short wavelengths, where $h \nu \gg k_B T$. Here, the exponential term is much larger than one, so $\exp(h\nu/k_B T) - 1 \approx \exp(h\nu/k_B T)$. This yields $B_{\nu}(T) \approx \frac{2 h \nu^3}{c^2} \exp(-h\nu/k_B T)$. The emission drops off exponentially at photon energies far exceeding the thermal energy of the medium. 

### Radiative Transfer Through an Atmosphere

An exoplanet's atmosphere is not a simple blackbody. It is a gaseous medium that absorbs, emits, and scatters radiation. To understand the emergent spectrum, we must describe how radiation propagates through this medium. This is the domain of **[radiative transfer theory](@entry_id:1130514)**.

#### Fundamental Quantities

Three fundamental quantities describe the radiation field and its interaction with matter in a plane-parallel atmosphere, where properties are assumed to vary only with vertical depth.

1.  **Specific Intensity ($I_{\nu}$)**: Also known as radiance, the specific intensity is the most fundamental quantity. It is defined as the energy flowing per unit time, per unit frequency, per unit [solid angle](@entry_id:154756), through an infinitesimal area oriented perpendicular to the direction of flow. Its SI units are $\mathrm{W\,m^{-2}\,Hz^{-1}\,sr^{-1}}$. A key property of specific intensity is that, in the absence of any interaction with matter (emission, absorption, or scattering), its value is constant along any given ray. In an atmosphere, its value depends on both location (e.g., optical depth $\tau_\nu$) and direction (e.g., the cosine of the viewing angle, $\mu = \cos\theta$).

2.  **Monochromatic Flux ($F_{\nu}$)**: The flux represents the net energy passing through a fixed surface per unit time, per unit frequency, per unit area. In a plane-parallel atmosphere, this surface is typically a horizontal plane. To calculate the flux from the specific intensity, one must account for the projection of this horizontal surface onto the direction of each ray. This introduces a weighting factor of $\mu = \cos\theta$. The flux is therefore the $\mu$-weighted integral of the [specific intensity](@entry_id:158830) over all solid angles of a hemisphere. For upward flux, this is $F_{\nu} = \int_{0}^{2\pi} d\phi \int_{0}^{1} I_{\nu}(\mu, \phi) \mu d\mu$. The units of flux are $\mathrm{W\,m^{-2}\,Hz^{-1}}$.

3.  **Source Function ($S_{\nu}$)**: The source function describes the creation of new radiation at a point in the atmosphere. It is formally defined as the ratio of the **emission coefficient** ($j_{\nu}$, power emitted per unit volume per [solid angle](@entry_id:154756)) to the **extinction coefficient** ($\alpha_{\nu}$, the inverse of the mean free path of a photon). Thus, $S_{\nu} \equiv j_{\nu} / \alpha_{\nu}$. The units of the source function are identical to those of [specific intensity](@entry_id:158830), $\mathrm{W\,m^{-2}\,Hz^{-1}\,sr^{-1}}$. This is dimensionally necessary for the [radiative transfer equation](@entry_id:155344). For emission and absorption processes that are isotropic (independent of direction), the [source function](@entry_id:161358) is also isotropic and does not depend on the viewing angle $\mu$. It is a local property of the gas, determined by its temperature, pressure, and composition. 

#### The Formal Solution and the Contribution Function

The journey of radiation through an atmosphere is described by the **[radiative transfer equation](@entry_id:155344) (RTE)**. In a plane-parallel geometry, for a non-scattering medium, the equation takes the form:

$\mu \frac{dI_{\nu}(\tau_{\nu}, \mu)}{d\tau_{\nu}} = I_{\nu}(\tau_{\nu}, \mu) - S_{\nu}(\tau_{\nu})$

Here, $\tau_{\nu}$ is the **vertical optical depth**, a dimensionless quantity that measures the opacity of the atmosphere integrated from the top down. An [optical depth](@entry_id:159017) of unity ($\tau_{\nu}=1$) corresponds to the layer from which a photon has a probability of $1/e$ of escaping without further interaction.

For a semi-infinite atmosphere (one that is optically thick at all depths), this differential equation can be formally solved for the emergent intensity at the top of the atmosphere ($\tau_{\nu}=0$) along a direction $\mu$. The solution is an integral that sums the contributions from all layers below:

$I_{\nu}(0, \mu) = \int_{0}^{\infty} S_{\nu}(\tau'_{\nu}) e^{-\tau'_{\nu}/\mu} \frac{d\tau'_{\nu}}{\mu}$

This is the **formal solution** of the RTE. It shows that the emergent intensity is a weighted average of the [source function](@entry_id:161358) over all depths. The weighting function, often written as part of the **contribution function**, is composed of two parts: the [source function](@entry_id:161358) $S_{\nu}(\tau'_{\nu})$ itself, and the attenuation term $e^{-\tau'_{\nu}/\mu}$, which represents the probability that a photon emitted at depth $\tau'_{\nu}$ will escape to the top of theatmosphere along the direction $\mu$. 

The integrand of this formal solution, $C(\tau_\nu; \mu) = S_{\nu}(\tau'_{\nu}) e^{-\tau'_{\nu}/\mu}$, represents the contribution of each layer at [optical depth](@entry_id:159017) $\tau'_\nu$ to the final emergent intensity. In a typical atmosphere where temperature (and thus the source function) increases with depth, this contribution function is the product of a decreasing exponential and an increasing source function. Consequently, it has a peak. A very useful rule of thumb is that the peak of the contribution function occurs at a vertical [optical depth](@entry_id:159017) of approximately $\tau_{\nu} \approx \mu$. This means that observations at different viewing angles probe different vertical layers of the atmosphere: nadir observations ($\mu=1$) probe deepest (to $\tau_\nu \approx 1$), while limb observations ($\mu \to 0$) probe highest in the atmosphere (to $\tau_\nu \approx 0$). This is the physical basis for [limb darkening](@entry_id:157740) in stars and planets, where the cooler upper layers seen at the limb appear dimmer than the hotter deeper layers seen at the disk center.  

#### Interpreting Spectra: Brightness Temperature

The emergent intensity $I_\nu$ is a powerful diagnostic, but it is often convenient to express it in terms of a temperature. The **brightness temperature**, $T_b(\nu, \mu)$, is defined as the temperature of a blackbody that would produce the same specific intensity at that frequency. It is defined implicitly by the equation:

$I_{\nu}(\mu) = B_{\nu}(T_b(\nu, \mu))$

Using the formal solution of the RTE, this definition becomes:

$B_{\nu}(T_b(\nu, \mu)) = \int_{0}^{\infty} S_{\nu}(\tau_{\nu}) e^{-\tau_{\nu}/\mu} \frac{d\tau_{\nu}}{\mu}$

This equation reveals that the brightness temperature is *not*, in general, equal to the [kinetic temperature](@entry_id:751035) at any single point in the atmosphere. Instead, it is a complex, weighted average. However, some important relationships and approximations exist:

-   **Isothermal Atmosphere:** In the simple case of an [isothermal atmosphere](@entry_id:203207) where $T(\tau_\nu)$ is constant, the [source function](@entry_id:161358) $S_\nu = B_\nu(T)$ is also constant. It can be pulled out of the integral, which normalizes to one. This yields $I_\nu(\mu) = B_\nu(T)$, and therefore $T_b(\nu, \mu) = T$. An [isothermal atmosphere](@entry_id:203207) in LTE radiates as a perfect blackbody at its own temperature. 

-   **The Eddington-Barbier Approximation:** In a non-[isothermal atmosphere](@entry_id:203207), a powerful approximation relates the emergent intensity to the source function at the depth where the [optical depth](@entry_id:159017) along the ray is unity. This depth corresponds to a vertical optical depth of $\tau_\nu = \mu$. The approximation states $I_\nu(\mu) \approx S_\nu(\tau_\nu = \mu)$, which implies $T_b(\nu, \mu) \approx T(\tau_\nu = \mu)$. This approximation is exact if the [source function](@entry_id:161358) is a linear function of [optical depth](@entry_id:159017) but serves as a useful guide in general.

-   **Non-linearity of the Planck Function:** The accuracy of the Eddington-Barbier relation is affected by the [non-linearity](@entry_id:637147) of the Planck function.
    - In the **Rayleigh-Jeans limit** ($h\nu \ll k_B T$), $B_\nu(T) \propto T$. In this case, the brightness temperature becomes a true, linearly weighted average of the [kinetic temperature](@entry_id:751035) profile: $T_b(\nu, \mu) = \int_0^\infty T(\tau_\nu) e^{-\tau_\nu/\mu} d\tau_\nu/\mu$. 
    - In the **Wien limit** ($h\nu \gg k_B T$), $B_\nu(T)$ is exponentially sensitive to temperature. This means that hotter regions contribute disproportionately to the integral. Consequently, the measured brightness temperature is biased towards the hottest temperatures within the region of the contribution function's peak, and can be significantly higher than the kinetic temperature at the mean formation depth, $T(\tau_\nu \approx \mu)$. 

-   **Thermal Inversions and Emission Lines:** If an atmosphere possesses a thermal inversion, where temperature increases with altitude (decreasing optical depth), this structure leaves a distinct signature in the spectrum. The opacity is much higher in the core of a spectral line than in the surrounding continuum. This means the line core probes higher altitudes than the continuum. In an inversion, these higher altitudes are hotter. Therefore, the brightness temperature in the line core will be greater than in the continuum, producing an **emission line** in the thermal spectrum. 

### The State of the Gas: Opacity and Equilibrium

To solve the radiative transfer equation, we need to know the source function $S_\nu$ and the [optical depth](@entry_id:159017) $\tau_\nu$. These quantities are determined by the microscopic physical state of the gas—its temperature, density, composition, and the interaction [cross-sections](@entry_id:168295) of its constituent atoms and molecules.

#### Local Thermodynamic Equilibrium (LTE)

A foundational concept in atmospheric modeling is **Local Thermodynamic Equilibrium (LTE)**. LTE is a state where, on a local scale, matter is in thermal equilibrium with itself, but not necessarily with the radiation field passing through it. This means that while the [radiation field](@entry_id:164265) can be highly non-local and non-Planckian, the statistical properties of the gas particles (atoms, molecules, electrons) are described by a single, local [kinetic temperature](@entry_id:751035), $T$. Specifically, in LTE:
1.  The velocity distribution of particles is Maxwellian.
2.  The population of internal energy levels (e.g., rotational, vibrational, electronic states) follows the **Boltzmann distribution**.
3.  The ionization and dissociation states follow the **Saha and chemical [equilibrium equations](@entry_id:172166)**, respectively.

The condition for LTE to hold is that **collisional processes must dominate over radiative processes** in setting the populations of energy levels. Collisions thermalize the gas, forcing level populations to conform to the local [kinetic temperature](@entry_id:751035). Radiative processes, particularly [spontaneous emission](@entry_id:140032), can cause populations to deviate from this equilibrium. A robust criterion for LTE is that the collisional de-excitation rate, $C_{ul} = n_c k_{ul}$ (where $n_c$ is the number density of collision partners and $k_{ul}$ is the rate coefficient), must be much greater than the spontaneous radiative de-excitation rate, $A_{ul}$.

$C_{ul} \gg A_{ul}$

This condition implies that there is a **[critical density](@entry_id:162027)**, $n_{crit} = A_{ul}/k_{ul}$, above which LTE is a good assumption. For typical infrared ro-[vibrational transitions](@entry_id:167069) in hot Jupiter atmospheres ($A_{ul} \sim 1-100 \text{ s}^{-1}$, $k_{ul} \sim 10^{-12} \text{ cm}^3\text{s}^{-1}$), the [critical density](@entry_id:162027) is around $10^{13} - 10^{14} \text{ cm}^{-3}$. This corresponds to pressures of roughly $10^{-6} - 10^{-5}$ bar. Since the infrared photosphere of a hot Jupiter is typically located at much higher pressures ($10^{-3} - 10^{-1}$ bar), the assumption of LTE is generally well-justified for interpreting their thermal emission spectra. In the much more tenuous upper atmosphere, however, this condition breaks down, and non-LTE (NLTE) effects become important. 

When LTE holds, a profound simplification occurs. According to **Kirchhoff's Law of thermal radiation**, the ratio of the emission coefficient to the [absorption coefficient](@entry_id:156541) for a material in [thermodynamic equilibrium](@entry_id:141660) is equal to the Planck function. Extending this principle to a gas in LTE, we find that the source function becomes equal to the Planck function at the local kinetic temperature:

$S_{\nu} = B_{\nu}(T)$

This is a pivotal result, as it directly links the source function in the RTE to a local thermodynamic property, the temperature, allowing us to interpret thermal emission spectra as a probe of the atmospheric temperature structure. 

#### Monochromatic Absorption Coefficient

The optical depth is the integral of the extinction coefficient, $\alpha_\nu$. For a [spectral line](@entry_id:193408) arising from a bound-bound transition, this is often called the **monochromatic [absorption coefficient](@entry_id:156541)**, $\kappa_\nu$. It can be factorized into two components: the total strength of the line and its frequency profile.

$\kappa_{\nu} = S(T) \phi(\nu)$

Here, $\phi(\nu)$ is the normalized **line profile** function (e.g., a Voigt profile, which combines thermal and [pressure broadening](@entry_id:159590)), and $S(T)$ is the **[line strength](@entry_id:182782)**. The [line strength](@entry_id:182782) represents the total integrated absorption cross-section of the line and depends strongly on the thermodynamic state of the gas. For a transition from a lower level $l$ to an upper level $u$, its temperature dependence arises from three factors:

1.  **Lower State Population:** The strength of the absorption is proportional to the number density of absorbers in the lower state, $n_l$. In LTE, this is given by the Boltzmann distribution: $n_l = n \frac{g_l \exp(-E_l/k_B T)}{Q(T)}$, where $n$ is the total [number density](@entry_id:268986) of the species, $g_l$ and $E_l$ are the degeneracy and energy of the lower level, and $Q(T)$ is the **partition function**. The partition function, $Q(T) = \sum_i g_i \exp(-E_i/k_B T)$, sums over all energy states and normalizes the distribution. As temperature increases, $Q(T)$ increases, spreading the population over more states and generally reducing the fractional population in any single state.

2.  **Boltzmann Factor:** The term $\exp(-E_l/k_B T)$ in the numerator describes how the population of the specific lower level $l$ changes with temperature. For low-lying states, this factor changes slowly, while for highly [excited states](@entry_id:273472), it can cause the [line strength](@entry_id:182782) to increase rapidly with temperature.

3.  **Stimulated Emission Correction:** The net absorption must account for photons that stimulate an excited absorber to emit a photon of the same frequency and direction. This process effectively cancels an absorption event. The correction factor, derived from the [principle of detailed balance](@entry_id:200508) and the Einstein relations, is $[1 - \exp(-h\nu_0/k_B T)]$, where $\nu_0$ is the line-center frequency. This factor approaches 1 at low temperatures (where [stimulated emission](@entry_id:150501) is negligible) and approaches 0 at very high temperatures (where [stimulated emission](@entry_id:150501) becomes nearly as frequent as absorption).

Combining these factors, the temperature dependence of the [line strength](@entry_id:182782) is complex but well-defined under LTE:

$S(T) \propto \frac{n \, g_l \, e^{-E_l/k_B T}}{Q(T)} \left[ 1 - e^{-h \nu_0 / k_B T} \right]$

Understanding this dependence is critical for accurately modeling how an exoplanet's spectrum changes with temperature. 

#### Departures from LTE (NLTE)

When collisions are not frequent enough to dominate radiative processes ($\epsilon_\nu \ll 1$), the LTE assumption breaks down. A common cause of NLTE effects is scattering, where a photon is absorbed and re-emitted without being thermalized. In this case, the [source function](@entry_id:161358) is no longer equal to the Planck function. For isotropic, [coherent scattering](@entry_id:267724), it takes the form:

$S_{\nu} = \epsilon_{\nu} B_{\nu}(T) + (1-\epsilon_{\nu})J_{\nu}$

where $\epsilon_\nu$ is the **photon destruction probability** (the fraction of interactions that are thermalizing collisions) and $J_\nu$ is the angle-averaged mean intensity of the radiation field. The [source function](@entry_id:161358) now has two components: a thermal part tied to the local temperature, and a scattering part tied to the ambient radiation field. This coupling to the non-local [radiation field](@entry_id:164265) can cause the source function to decouple significantly from the local temperature, altering the emergent spectrum. 

### Global Energetics and Phase Curves

While [emission spectroscopy](@entry_id:186353) probes the vertical structure of an atmosphere, **[thermal phase curves](@entry_id:1133014)**—measurements of a planet's total thermal brightness as a function of its orbital phase—reveal its longitudinal (day-night) structure.

#### Global Energy Balance and the Redistribution Factor

The overall temperature of a planet is set by the global energy balance between absorbed [stellar radiation](@entry_id:1132380) and emitted thermal radiation. The total power absorbed by a planet of radius $R_p$ is $P_{abs} = F_\star \pi R_p^2 (1 - A)$, where $F_\star$ is the incident [stellar flux](@entry_id:1132378) and $A$ is the planet's **Bond albedo** (the fraction of total incident power reflected). The total power emitted is the integral of $\sigma T^4$ over the planet's surface area.

To characterize the planet's temperature with a single value, we define an **equilibrium temperature**, $T_{eq}$. However, its precise definition depends on how efficiently atmospheric winds transport heat from the irradiated dayside to the unlit nightside. This is parameterized by a **redistribution factor**, $f$, in the standard definition:

$T_{eq}^4 = f \frac{(1-A)F_\star}{\sigma}$

The value of $f$ corresponds to different physical scenarios:
-   $f = 1/4$: This corresponds to a planet with extremely efficient heat redistribution, resulting in a uniform temperature over the entire surface ($4\pi$ steradians). The absorbed energy is spread evenly before being re-radiated.
-   $f = 1/2$: This represents the case of zero heat redistribution, where energy is radiated only from the dayside hemisphere ($2\pi$ steradians), which is assumed to have a uniform temperature.
-   $f = 2/3$: This value does not represent a physical temperature but corresponds to the disc-averaged brightness temperature of the dayside hemisphere as seen by a distant observer at secondary eclipse, assuming no redistribution and Lambertian (isotropic) emission.

The redistribution factor is a powerful, albeit simplified, way to connect the global energy budget to the efficiency of [atmospheric dynamics](@entry_id:746558). 

#### Hotspot Displacement and Phase Offset

For tidally locked planets, the permanent dayside is intensely heated, while the nightside is cold. Strong eastward (prograde) winds, or "super-rotation," are expected to advect this heat downstream. This dynamic process results in the planet's hottest point—the **thermal hotspot**—being displaced eastward from the substellar point (the point directly facing the star).

This phenomenon can be understood with a simple model that balances zonal (east-west) advection by a wind of speed $U$ with radiative cooling over a timescale $t_{rad}$. The key parameter governing the displacement is the ratio of the radiative timescale to the advective timescale ($t_{adv} = R_p / U$): $\xi = t_{rad} / t_{adv}$. When forced with a sinusoidal heating pattern peaked at the substellar point, the resulting longitudinal temperature profile is also a [sinusoid](@entry_id:274998), but its peak is shifted eastward by a [phase angle](@entry_id:274491) $\delta$. The solution to the linearized [energy balance equation](@entry_id:191484) yields a simple, elegant result for this displacement:

$\delta = \arctan(\xi)$

This eastward hotspot displacement is directly observable in the [thermal phase curve](@entry_id:1133013). The peak of the planet's integrated thermal flux will not occur at secondary eclipse (when the dayside is fully visible) but will be delayed, occurring at an orbital phase offset $\phi_1$. For a simple cosine temperature map, the disk-integrated phase offset is identical to the hotspot displacement on the map: $\phi_1 = \delta$.

The limiting cases are intuitive:
-   If radiation is very efficient compared to advection ($\xi \to 0$), the atmosphere cools before the wind can move the heat far. The hotspot remains at the substellar point ($\delta \to 0$), and the phase offset is zero.
-   If advection is very efficient compared to radiation ($\xi \to \infty$), the heat is carried far downstream before it can be radiated away. The hotspot is shifted by a full quarter of the planet's circumference, and the phase offset approaches its maximum value of $90^\circ$ ($\pi/2$ radians). 

The amplitude of the phase curve is also affected by dynamics and radiative transfer. For instance, non-LTE scattering can alter the day-night heat exchange. In a simple two-hemisphere model, scattering acts to "short-circuit" the temperature gradient, as photons from the hot dayside can scatter into the nightside hemisphere and vice-versa. This homogenizes the planet's brightness, suppressing the day-night flux contrast and thus reducing the amplitude of the [thermal phase curve](@entry_id:1133013) by a factor related to the scattering probability. 

### Model Assumptions and Limitations

The theoretical framework described above relies on a key idealization: the **plane-parallel, one-dimensional (1D) slab approximation**. This model assumes the atmosphere is a flat, horizontally infinite slab where all properties (temperature, composition, etc.) vary only with the vertical coordinate. This is a reasonable approximation when the [atmospheric scale height](@entry_id:203508) $H$ is much smaller than the planetary radius $R_p$, and for viewing angles not too close to the limb.

However, this approximation has significant limitations, especially when interpreting phase curves that inherently map a 3D object:
-   **Curvature at the Limb/Terminator:** At grazing viewing angles, such as those probing the planet's limb or terminator, the plane-parallel assumption breaks down. The true, curved line-of-sight path length through the spherical atmospheric shells is significantly different from the $ds = dz/\mu$ relation, altering the contribution function and the resulting spectrum.
-   **Horizontal Inhomogeneity:** The 1D model, by definition, cannot account for horizontal variations in temperature or composition. This makes it fundamentally incapable of self-consistently modeling phenomena like hotspot displacement. While one can create a "patchwork" of 1D models to represent different longitudes, this fails to capture the physical advection of heat between them. Fitting a phase curve with a 1D model can therefore lead to significant biases in the inferred vertical temperature structure.
-   **3D Effects:** A full interpretation of [thermal phase curves](@entry_id:1133014) requires 3D models that couple fluid dynamics (to predict winds and heat transport) with 3D radiative transfer on a spherical grid. These models can properly account for the geometry of the limb and the strong horizontal gradients in temperature and composition across the day-night terminator, providing a much more physically realistic picture of the planet's climate. 