## Introduction
Emission and [absorption spectroscopy](@entry_id:164865) is the definitive, non-invasive language through which we interrogate the state of ionized matter. From the fiery atmospheres of distant stars to the controlled environments of fusion reactors and industrial processing chambers, the light a plasma emits or absorbs carries a detailed blueprint of its fundamental properties. However, this information is encoded in the subtle characteristics of the spectrum—the intensity, shape, and position of spectral lines. The central challenge for any plasma physicist or engineer is to accurately decode this spectral language to measure crucial parameters like temperature, density, composition, and internal fields. This article provides a comprehensive guide to mastering this process. The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork, journeying from the quantum origins of radiation to the macroscopic transport of light through a plasma. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these principles are transformed into powerful diagnostic tools across science and engineering. Finally, the **Hands-On Practices** section offers a chance to apply this knowledge to practical analysis problems. We begin by establishing the fundamental physics that governs the creation and transport of radiation within a plasma.

## Principles and Mechanisms

The emission and [absorption spectra](@entry_id:176058) of a plasma are encoded with a wealth of information about its physical state. To decode this information, we must first understand the fundamental principles governing the interaction of radiation with the constituent atoms and ions, the transport of this radiation through the medium, and the mechanisms that shape the observed spectral features. This chapter establishes the theoretical framework for this analysis, proceeding from the microscopic quantum processes to the [macroscopic observables](@entry_id:751601).

### The Microscopic Origin of Plasma Radiation

The foundation of [plasma spectroscopy](@entry_id:193988) lies in the quantum-mechanical transitions between discrete energy levels of atoms and ions. For simplicity, we begin by considering an idealized **[two-level atom](@entry_id:159911)**, with a lower energy level $l$ and an upper energy level $u$, having statistical weights $g_l$ and $g_u$ and populations (number densities) $N_l$ and $N_u$, respectively. The energy difference between these levels is $E_u - E_l = h\nu_0$, where $\nu_0$ is the characteristic frequency of the transition and $h$ is the Planck constant. These atoms interact with a [radiation field](@entry_id:164265) through three fundamental processes, first described by Einstein:

1.  **Spontaneous Emission:** An atom in the upper level $u$ can spontaneously decay to the lower level $l$, emitting a photon of energy $h\nu_0$. The rate of this process per unit volume is proportional to the population of the upper level, $N_u$. The constant of proportionality is the **Einstein A coefficient**, $A_{ul}$ (units of s$^{-1}$).

2.  **Stimulated Absorption:** An atom in the lower level $l$ can absorb a photon from the radiation field and be excited to the upper level $u$. The rate of this process per unit volume is proportional to the population of the lower level, $N_l$, and the energy density of the [radiation field](@entry_id:164265) at the transition frequency, $u_\nu$. The constant of proportionality is the **Einstein B coefficient for absorption**, $B_{lu}$.

3.  **Stimulated Emission:** An incident photon can stimulate an atom in the upper level $u$ to decay to the lower level $l$, emitting a second photon that is identical in frequency, direction, and phase to the incident photon. The rate of this process per unit volume is proportional to the upper-level population, $N_u$, and the radiation energy density, $u_\nu$. The constant of proportionality is the **Einstein B coefficient for [stimulated emission](@entry_id:150501)**, $B_{ul}$.

These three coefficients are not independent. Thermodynamic arguments show that they are linked by the following relations:
$$
g_l B_{lu} = g_u B_{ul}
$$
$$
A_{ul} = \frac{8\pi h \nu_0^3 n^3}{c^3} B_{ul}
$$
where $c$ is the speed of light in vacuum and $n$ is the refractive index of the plasma medium. These relations are fundamental, connecting the absorptive and emissive properties of matter.

### The Equation of Radiative Transfer

The macroscopic transport of radiation through a medium is described by the **Equation of Radiative Transfer (RTE)**. This equation acts as a bookkeeping ledger for the change in the **[spectral radiance](@entry_id:149918)** $I_\nu$ (or [specific intensity](@entry_id:158830), with units of W m$^{-2}$ sr$^{-1}$ Hz$^{-1}$) along a path $s$. The change in $I_\nu$ is the sum of gains (emission) and losses (absorption).

The gain term is the **spectral emission coefficient**, $j_\nu$, which describes the power emitted by the plasma per unit volume, per unit [solid angle](@entry_id:154756), per unit frequency. For [line radiation](@entry_id:751334), this is due to [spontaneous emission](@entry_id:140032). The total energy emitted per unit volume per second is $N_u A_{ul} h\nu_0$. This energy is distributed over a frequency range described by a normalized **line profile function**, $\phi(\nu)$, where $\int \phi(\nu) d\nu = 1$. Assuming isotropic emission over $4\pi$ steradians, the emission coefficient is:
$$
j_\nu = \frac{h\nu_0}{4\pi} N_u A_{ul} \phi(\nu)
$$

The loss term is more complex. While stimulated absorption removes energy from the beam of intensity $I_\nu$, stimulated emission adds energy to it. Because the stimulated photon is identical to the incident photon, this process effectively reduces the net absorption. The net rate of energy removal from the beam per unit volume is $h\nu_0 (N_l B_{lu} u_\nu - N_u B_{ul} u_\nu)$, distributed according to the profile $\phi(\nu)$. Relating the [spectral energy density](@entry_id:168013) $u_\nu$ to the [spectral radiance](@entry_id:149918) via $u_\nu = n I_\nu / c$, we can define an **effective [spectral absorption coefficient](@entry_id:148811)**, $\alpha'_\nu$, such that the loss of intensity is written as $\alpha'_\nu I_\nu$. This gives:
$$
\alpha'_\nu = \frac{h\nu_0 n}{c} (N_l B_{lu} - N_u B_{ul}) \phi(\nu)
$$
The term $N_u B_{ul}$ represents the "negative absorption" due to [stimulated emission](@entry_id:150501).

Combining these terms, the RTE takes its fundamental form:
$$
\frac{dI_\nu}{ds} = j_\nu - \alpha'_\nu I_\nu
$$
This equation states that the change in [radiance](@entry_id:174256) along a path is equal to what is emitted locally minus what is absorbed from the beam.

A [pivotal quantity](@entry_id:168397) in [radiative transfer](@entry_id:158448) is the **line [source function](@entry_id:161358)**, $S_\nu$, defined as the ratio of the emission to the effective [absorption coefficient](@entry_id:156541): $S_\nu = j_\nu / \alpha'_\nu$. Substituting the expressions for $j_\nu$ and $\alpha'_\nu$ allows for a profound simplification [@problem_id:255097].
$$
S_\nu = \frac{j_\nu}{\alpha'_\nu} = \frac{\frac{h\nu_0}{4\pi} N_u A_{ul} \phi(\nu)}{\frac{h\nu_0 n}{c} (N_l B_{lu} - N_u B_{ul}) \phi(\nu)} = \frac{c}{4\pi n} \frac{N_u A_{ul}}{N_l B_{lu} - N_u B_{ul}}
$$
Notice that the line profile function $\phi(\nu)$ has cancelled out. The [source function](@entry_id:161358) is independent of frequency across the [spectral line](@entry_id:193408). By substituting the Einstein relations, we arrive at an expression that depends only on the atomic level populations:
$$
S_\nu = \frac{c}{4\pi n} \frac{N_u \left(\frac{8\pi h \nu_0^3 n^3}{c^3} B_{ul}\right)}{N_l \left(\frac{g_u}{g_l} B_{ul}\right) - N_u B_{ul}} = \frac{2h\nu_0^3 n^2}{c^2} \frac{N_u g_l}{N_l g_u - N_u g_l} = \frac{2h\nu_0^3 n^2}{c^2} \left( \frac{g_u N_l}{g_l N_u} - 1 \right)^{-1}
$$
This result is central: the [source function](@entry_id:161358) $S_\nu$ is a direct measure of the local excitation state of the plasma, encapsulated in the population ratio $N_u/N_l$. The RTE can now be rewritten compactly as $\frac{dI_\nu}{ds} = \alpha'_\nu (S_\nu - I_\nu)$. This form reveals that where $I_\nu  S_\nu$, the intensity will grow; where $I_\nu > S_\nu$, it will diminish; and where $I_\nu = S_\nu$, the radiation and matter are in [local equilibrium](@entry_id:156295).

### The Source Function and Thermodynamic Equilibrium

The population ratio $N_u/N_l$, and thus the [source function](@entry_id:161358), is determined by the competition between all microscopic processes that populate and depopulate the energy levels. In a plasma, this balance is typically between radiative processes and [inelastic collisions](@entry_id:137360), primarily with free electrons. This is the condition of **statistical equilibrium**.

Let's consider the balance for our two-level atom, including [collisional excitation](@entry_id:159854) ([rate coefficient](@entry_id:183300) $C_{12}$) and de-excitation ([rate coefficient](@entry_id:183300) $C_{21}$) by an electron density $n_e$ [@problem_id:255072]. The statistical equilibrium equation for the upper level is:
$$
\text{Rate In} = \text{Rate Out}
$$
$$
N_l (B_{12} J_\nu + n_e C_{12}) = N_u (A_{21} + B_{21} J_\nu + n_e C_{21})
$$
where $J_\nu$ is the angle-averaged [spectral radiance](@entry_id:149918) (the mean intensity). Solving for the population ratio gives:
$$
\frac{N_u}{N_l} = \frac{B_{12} J_\nu + n_e C_{12}}{A_{21} + B_{21} J_\nu + n_e C_{21}}
$$
Substituting this into our expression for the [source function](@entry_id:161358) $S_\nu$ yields, after some algebra involving the Einstein relations and the principle of detailed balance for collisions ($g_1 C_{12} = g_2 C_{21} \exp(-h\nu/k_B T)$), a remarkably insightful form:
$$
S_\nu = \frac{J_\nu + \epsilon B_\nu(T)}{1 + \epsilon}
$$
Here, $B_\nu(T)$ is the **Planck function**, which describes [black-body radiation](@entry_id:136552) at the electron [kinetic temperature](@entry_id:751035) $T$, and $\epsilon = \frac{n_e C_{21}}{A_{21}}$ is a dimensionless parameter representing the ratio of collisional to radiative de-excitation rates.

This expression for $S_\nu$ elegantly describes the state of the plasma:
-   If collisions dominate ($\epsilon \gg 1$, typically in high-density plasmas), then $S_\nu \approx \epsilon B_\nu(T) / \epsilon = B_\nu(T)$. The level populations are forced into a Boltzmann distribution by the frequent collisions, and the plasma is said to be in **Local Thermodynamic Equilibrium (LTE)**. The emission is determined solely by the local temperature.
-   If radiative de-excitation dominates ($\epsilon \ll 1$, in low-density plasmas), then $S_\nu \approx J_\nu$. The atomic populations are determined by the radiation field they are bathed in, not the local [kinetic temperature](@entry_id:751035). This is a highly **non-Local Thermodynamic Equilibrium (non-LTE)** situation.
-   In the intermediate case, the [source function](@entry_id:161358) is a weighted average of the local [radiation field](@entry_id:164265) and the thermal Planck function. For instance, for the [source function](@entry_id:161358) to be the exact arithmetic mean of the mean intensity and the Planck function, $S_\nu = \frac{1}{2}(J_\nu + B_\nu(T))$, the collisional de-excitation parameter must be exactly $\epsilon = 1$ [@problem_id:255072].

### Interpreting Observed Spectra: Solving the RTE

With the [source function](@entry_id:161358) understood, we can solve the RTE to predict the radiation that emerges from a plasma and is observed by a spectrometer. It is convenient to introduce the **optical depth**, $\tau_\nu$, defined along the line of sight $s$ as $d\tau_\nu = \alpha'_\nu ds$. The [optical depth](@entry_id:159017) is a dimensionless measure of the [opacity](@entry_id:160442) of the path. An optical depth of $\tau_\nu=1$ means that radiation of frequency $\nu$ is attenuated by a factor of $e^{-1}$ along that path. The RTE becomes:
$$
\frac{dI_\nu}{d\tau_\nu} = I_\nu - S_\nu \quad (\text{for } \tau_\nu \text{ increasing away from the observer})
$$
The formal solution for the intensity $I_\nu(0)$ emerging from a plasma of total optical depth $\tau_{\nu,tot}$ is:
$$
I_\nu(0) = I_\nu(\tau_{\nu,tot}) e^{-\tau_{\nu,tot}} + \int_0^{\tau_{\nu,tot}} S_\nu(\tau_\nu) e^{-\tau_\nu} d\tau_\nu
$$
This shows that the emergent intensity is the sum of the background radiation (if any), attenuated by the entire plasma, plus the integrated emission from every point along the line of sight, with each contribution attenuated by the intervening plasma.

As a concrete example, consider a uniform, isothermal, plane-parallel plasma slab of total [optical thickness](@entry_id:150612) $\tau_{\nu,0}$ in LTE, so $S_\nu = B_\nu(T)$ is constant [@problem_id:255180]. Let's assume no radiation is incident on the far side ($\tau_\nu = 0$), but the near side ($\tau_\nu = \tau_{\nu,0}$) is a specular reflector with reflectivity $R$. An observer views the slab from the far side. The intensity emerging at an angle $\theta$ (where $\mu = \cos\theta$) is found by solving the RTE. The formal solution for the upward-propagating intensity at the top surface ($\tau_\nu=0$) is:
$$
I_\nu(0, \mu) = I_\nu(\tau_{\nu,0}, \mu) e^{-\tau_{\nu,0}/\mu} + B_\nu(T) (1 - e^{-\tau_{\nu,0}/\mu})
$$
The intensity at the bottom, $I_\nu(\tau_{\nu,0}, \mu)$, is due to the reflection of downward-propagating radiation. That downward radiation itself originated from emission within the slab. Solving for the full path gives the final emergent intensity:
$$
I_\nu(0, \mu) = B_\nu(T) (1 - e^{-\tau_{\nu,0}/\mu}) (1 + R e^{-\tau_{\nu,0}/\mu})
$$
This expression is highly instructive. The term $B_\nu(T)(1 - e^{-\tau_{\nu,0}/\mu})$ represents the direct emission from the slab, approaching the black-body limit $B_\nu(T)$ for optically thick lines ($\tau_{\nu,0}/\mu \gg 1$) and becoming $\approx B_\nu(T) \tau_{\nu,0}/\mu$ for optically thin lines. The term $(1 + R e^{-\tau_{\nu,0}/\mu})$ accounts for the reflected image of the slab's own emission, which is also attenuated on its way out.

### The Formation and Analysis of Spectral Line Shapes

The line profile function $\phi(\nu)$ contains detailed information about the plasma environment. The shape of a [spectral line](@entry_id:193408) is determined by various **[broadening mechanisms](@entry_id:158662)**, which can be broadly classified as Doppler broadening, related to emitter motion, and [pressure broadening](@entry_id:159590), related to interactions with other particles.

#### Doppler Broadening

Doppler broadening arises from the thermal motion of the emitting or absorbing atoms. An atom moving with a velocity component $v_z$ along the line of sight of an observer will have its emission frequency shifted from the rest-frame frequency $\nu_0$ to $\nu = \nu_0 (1 + v_z/c)$. The observed [spectral line shape](@entry_id:164367) is therefore a direct reflection of the distribution of line-of-sight velocities of the emitting atoms.

To illustrate this principle starkly, consider an idealized gas where all atoms have the same speed $v_0$ but move in isotropic directions [@problem_id:255257]. The line-of-sight velocity is $v_z = v_0 \cos\theta$, where $\theta$ is the angle between the velocity vector and the line of sight. For an isotropic distribution, the probability of finding a velocity vector at angle $\theta$ is proportional to the [solid angle](@entry_id:154756) element, meaning the probability distribution for $u = \cos\theta$ is uniform on the interval $[-1, 1]$. The frequency shift is $\Delta\nu = \nu - \nu_0 = (v_0\nu_0/c) u = \Delta\nu_D u$. Since the distribution of $u$ is rectangular, the resulting line shape $L(\nu)$ is also a rectangle:
$$
L(\nu) = \frac{1}{2\Delta\nu_D} \quad \text{for } |\nu - \nu_0| \le \Delta\nu_D, \text{ and } 0 \text{ otherwise.}
$$
This "boxcar" profile is a direct consequence of the underlying velocity distribution. In a realistic thermal plasma, the velocities follow a Maxwell-Boltzmann distribution. The corresponding line-of-sight velocity distribution is a Gaussian, and consequently, the Doppler-broadened line shape is a **Gaussian profile**:
$$
G(\nu) \propto \exp\left(-\frac{(\nu-\nu_0)^2}{2\sigma_D^2}\right)
$$
The width of this Gaussian is directly related to the [ion temperature](@entry_id:191275) $T_i$ and the emitter mass $M$. The Full Width at Half Maximum (FWHM) is given by $\Gamma_G = \nu_0 \sqrt{8 k_B T_i \ln 2 / (Mc^2)}$. Measurement of the Doppler width is one of the most common methods for determining [ion temperature](@entry_id:191275) in plasmas.

#### Pressure Broadening

Pressure broadening, also known as [collisional broadening](@entry_id:158173), results from perturbations to the emitting atom by neighboring particles (ions and electrons). These perturbations can be modeled in two main ways: the [impact approximation](@entry_id:161234) for fast collisions and the [quasi-static approximation](@entry_id:167818) for slow perturbations.

A simple and intuitive model for impact broadening treats the atom as a classical oscillator whose coherent oscillation is randomly interrupted by collisions [@problem_id:255249]. Each collision resets the phase of the oscillation. This loss of phase coherence shortens the [effective duration](@entry_id:140718) of the wave train, which, by the Fourier uncertainty principle, broadens its frequency spectrum. This process leads to a **Lorentzian profile**:
$$
L(\nu) \propto \frac{1}{(\nu-\nu_0)^2 + (\Gamma_L/2)^2}
$$
where $\Gamma_L$ is the FWHM of the line, which is proportional to the total collision frequency. Different types of collisions contribute to this width. For instance, if we consider hard, phase-randomizing collisions (frequency $\nu_h$) and weaker, glancing collisions that impart a small phase shift $\phi_0$ (frequency $\nu_g$), the total FWHM (in angular frequency units) can be shown to be the sum of the natural width $\gamma_n$ and the collisional contributions:
$$
\Delta\omega_L = \gamma_n + 2\nu_h + 2\nu_g(1-\cos\phi_0)
$$
Since collision frequencies are proportional to the density of perturbing particles, the Lorentzian width is a primary diagnostic for plasma density. Stark broadening, caused by the electric fields of nearby ions and electrons, is a particularly important form of [pressure broadening](@entry_id:159590) in plasmas.

#### The Voigt Profile and Advanced Line Shape Analysis

In many plasmas, both Doppler and [pressure broadening](@entry_id:159590) are significant. If the underlying processes are statistically independent, the resulting line shape is the **convolution** of the individual profiles. The convolution of a Gaussian (from Doppler broadening) and a Lorentzian (from [pressure broadening](@entry_id:159590)) is known as the **Voigt profile**.
$$
V(\nu) = (G \ast L)(\nu) = \int_{-\infty}^{\infty} G(\nu') L(\nu - \nu') d\nu'
$$
The Voigt profile does not have a simple [closed-form expression](@entry_id:267458), making its analysis complex. However, we can understand its properties. Near the line center, the profile is dominated by the Gaussian core. In the far wings, it is dominated by the Lorentzian, which decays more slowly as $(\Delta\nu)^{-2}$ compared to the [exponential decay](@entry_id:136762) of the Gaussian.

Approximations for the FWHM of the Voigt profile, $\Gamma_V$, are often used in practice. A simple but effective [quadratic approximation](@entry_id:270629) can be derived by finding a Gaussian profile that has the same peak height (or equivalent width) as the Lorentzian profile, and then adding the widths of this "equivalent" Gaussian and the original Doppler Gaussian in quadrature [@problem_id:255087]. This procedure yields an approximation of the form:
$$
\Gamma_V^2 \approx \Gamma_G^2 + \alpha \Gamma_L^2
$$
where $\alpha$ is a numerical constant (e.g., $\alpha = \pi\ln 2$ in the specific derivation). By fitting an observed line to a Voigt profile, one can deconvolve the Gaussian and Lorentzian contributions, simultaneously determining temperature and density.

The principle that the far wings of a convolved profile are dominated by the broadest constituent profile is general. Consider a line broadened by both the quasi-static Stark effect from ions (e.g., a Holtsmark profile $S(\Delta\omega) \propto |\Delta\omega|^{-5/2}$) and Doppler broadening (a Gaussian $G(\Delta\omega)$). The resulting profile is $L = S*G$. In the far wings ($\Delta\omega \gg \Delta\omega_D$), we can approximate the profile by expanding the dominant Stark term. This leads to an asymptotic form where the Gaussian provides a small correction [@problem_id:255253]:
$$
L(\Delta\omega) \approx S(\Delta\omega) \left(1 + \mathcal{C} \left(\frac{\Delta\omega_D}{\Delta\omega}\right)^2\right)
$$
where $\mathcal{C}$ is a numerical constant (e.g., $\mathcal{C}=35/16$ for this specific case). This shows how even in the wing-dominated region, information about the core-broadening mechanism can be extracted.

Finally, when spectral lines are broadened, they can overlap. A classic example is the Zeeman effect, where a single line splits into multiple components in a magnetic field. If the splitting is not much larger than the line width, the components merge. For a normal Zeeman triplet observed perpendicular to the field, the profile consists of two Lorentzian $\sigma$ components shifted by $\pm\Delta\nu_Z$. The observed intensity peaks will not be at $\pm\Delta\nu_Z$. One must analyze the shape of the total profile to recover the true splitting and, therefore, the magnetic field strength [@problem_id:255076]. This underscores a critical lesson in spectroscopy: the observed features are not always the true physical parameters, and a careful analysis of the line shape is required for accurate diagnostics.

### Integrated Absorption and the Curve of Growth

While emission line analysis is powerful, [absorption spectroscopy](@entry_id:164865) provides complementary information, particularly about the ground-state or lower-level populations. The key observable in absorption is the **equivalent width**, $W_\lambda$, defined as the integrated fractional absorption across the line:
$$
W_\lambda = \int_{-\infty}^{\infty} (1 - T_\lambda) d\lambda = \int_{-\infty}^{\infty} (1 - e^{-\tau_\lambda}) d\lambda
$$
where $T_\lambda$ is the [transmittance](@entry_id:168546) and $\tau_\lambda$ is the optical depth. The equivalent width represents the width of a hypothetical, perfectly absorbing rectangular line that removes the same total energy from the spectrum. It is a robust measure, insensitive to the resolution of the [spectrometer](@entry_id:193181).

The **[curve of growth](@entry_id:157552)** is a plot of the equivalent width $W_\lambda$ as a function of the column density of absorbing atoms (which is proportional to the [optical depth](@entry_id:159017) at the line center, $\tau_0$). This curve has a characteristic shape that reveals the [optical thickness](@entry_id:150612) of the plasma.

To understand this, we can analyze a simplified model with a triangular profile for the optical depth [@problem_id:255245]. By evaluating the integral for $W_\lambda$, we can identify two distinct asymptotic regimes:
1.  **Linear Regime ($\tau_0 \ll 1$):** When the line is optically thin, we can approximate $1 - e^{-\tau_\lambda} \approx \tau_\lambda$. The equivalent width becomes $W_\lambda \approx \int \tau_\lambda d\lambda$. Since the total area of the optical depth profile is proportional to $\tau_0$, we find that $W_\lambda \propto \tau_0$. In this regime, every atom contributes equally to the absorption, and $W_\lambda$ is a direct measure of the column density.

2.  **Saturated (or Plateau) Regime ($\tau_0 \gtrsim 1$):** When the line center becomes optically thick, the [transmittance](@entry_id:168546) there drops to nearly zero. Increasing the number of atoms does little to change the absorption at the line center; it is already "black". The equivalent width can now only grow by absorption in the less-opaque wings of the line. This causes the growth of $W_\lambda$ to slow dramatically. For a Doppler-broadened line, $W_\lambda$ grows very slowly, proportional to $\sqrt{\ln \tau_0}$.

The transition between these regimes can be characterized by finding the intersection of their respective asymptotes. For our triangular profile model, the linear asymptote is $W_\lambda = (\Delta\lambda_T) \tau_0$ and the saturated asymptote is $W_\lambda = 2\Delta\lambda_T$. Their intersection occurs at $\tau_0 = 2$ [@problem_id:255245]. By identifying where an observed line lies on the [curve of growth](@entry_id:157552), one can determine whether the plasma is optically thin or thick and extract the column density of absorbers. For very high column densities, if the line has Lorentzian wings (from [pressure broadening](@entry_id:159590)), a third regime emerges where the wings become optically thick, and the equivalent width again grows more rapidly, often as $W_\lambda \propto \sqrt{\tau_0}$. The [curve of growth](@entry_id:157552) is thus a powerful, comprehensive diagnostic tool in [absorption spectroscopy](@entry_id:164865).