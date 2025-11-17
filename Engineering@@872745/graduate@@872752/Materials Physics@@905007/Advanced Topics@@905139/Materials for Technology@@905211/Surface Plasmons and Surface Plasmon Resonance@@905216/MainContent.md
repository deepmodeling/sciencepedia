## Introduction
Surface [plasmons](@entry_id:146184), the collective oscillations of electrons coupled to light at a metallic surface, represent a powerful paradigm for manipulating light at the nanoscale. Their ability to confine electromagnetic energy into sub-wavelength volumes, far beyond the [diffraction limit](@entry_id:193662), has unlocked a host of revolutionary applications. However, to effectively harness these phenomena, a deep understanding of the underlying physical principles is essential. This article addresses the knowledge gap between the concept of [plasmonics](@entry_id:142222) and its practical implementation by detailing the fundamental theory, mechanisms, and applications of both propagating and localized [surface plasmons](@entry_id:145851).

The following chapters will guide you through this fascinating subject. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, starting from the [optical response](@entry_id:138303) of metals described by the Drude model and moving to the derivation and characteristics of [surface plasmon polaritons](@entry_id:190932) (SPPs) and [localized surface plasmon](@entry_id:270427) resonances (LSPRs). The second chapter, "Applications and Interdisciplinary Connections," explores how these principles are applied in transformative technologies like real-time [biosensing](@entry_id:274809), enhanced spectroscopy, and [photocatalysis](@entry_id:155496). Finally, the "Hands-On Practices" section provides opportunities to apply these concepts to solve practical, research-relevant problems. We begin our journey by examining the fundamental [optical properties of metals](@entry_id:269719) that make [plasmonics](@entry_id:142222) possible.

## Principles and Mechanisms

### The Optical Response of Metals: The Drude-Sommerfeld Model

The defining characteristic of a plasmonic material is its [optical response](@entry_id:138303), which is dominated by the collective behavior of its [conduction electrons](@entry_id:145260). A simple yet powerful model for describing this behavior in metals is the Drude-Sommerfeld model. In this framework, the metal is pictured as a combination of a "gas" of free [conduction electrons](@entry_id:145260) moving against a static background of positive ion cores. The ion cores also contain bound electrons, which can contribute to the material's polarization.

To understand the [frequency-dependent permittivity](@entry_id:265694) $\epsilon_m(\omega)$, we consider the motion of an average conduction electron with effective mass $m^*$ and charge $-e$ under the influence of an external time-harmonic electric field $\mathbf{E}(t) = \mathrm{Re}\{\mathbf{E}_0 \exp(-i\omega t)\}$. The electron's motion is damped by various scattering events, such as collisions with phonons ([lattice vibrations](@entry_id:145169)), [crystal defects](@entry_id:144345), impurities, and other electrons. This damping is phenomenologically described by a [frictional force](@entry_id:202421) proportional to the electron's velocity $\mathbf{v}$, with a damping constant $\gamma$. The equation of motion is thus:

$$
m^* \frac{d\mathbf{v}}{dt} + m^*\gamma\mathbf{v} = -e\mathbf{E}(t)
$$

Assuming a harmonic solution for the velocity, $\mathbf{v}(t) = \mathbf{v}_0 \exp(-i\omega t)$, this differential equation simplifies to an algebraic one in the frequency domain:

$$
(-i\omega m^* + m^*\gamma)\mathbf{v}_0 = -e\mathbf{E}_0
$$

Solving for the [complex velocity](@entry_id:201810) amplitude $\mathbf{v}_0$ gives the mobility of the [electron gas](@entry_id:140692). From this, we can find the conduction current density $\mathbf{J}_{\text{free}} = -ne\mathbf{v}$, where $n$ is the conduction electron number density. The polarization of the [free electron gas](@entry_id:145649), $\mathbf{P}_{\text{free}}$, is related to the current by $\mathbf{J}_{\text{free}} = \partial\mathbf{P}_{\text{free}}/\partial t$, or $\mathbf{J}_{\text{free},0} = -i\omega\mathbf{P}_{\text{free},0}$ in the frequency domain. By defining the [electric susceptibility](@entry_id:144209) of the free electrons via $\mathbf{P}_{\text{free}} = \epsilon_0\chi_{\text{free}}\mathbf{E}$, we arrive at:

$$
\chi_{\text{free}}(\omega) = -\frac{ne^2}{\epsilon_0 m^* \omega(\omega + i\gamma)}
$$

It is conventional to define the **plasma frequency** $\omega_p$ as:

$$
\omega_p^2 = \frac{ne^2}{\epsilon_0 m^*}
$$

The [plasma frequency](@entry_id:137429) represents the natural resonance frequency for collective, longitudinal oscillations of the electron gas if displaced from equilibrium. With this definition, the free-electron susceptibility becomes $\chi_{\text{free}}(\omega) = -\frac{\omega_p^2}{\omega(\omega + i\gamma)}$.

The total relative permittivity of the metal, $\epsilon_m(\omega)$, must also account for the polarizability of the bound electrons in the ion cores. These electrons give rise to **[interband transitions](@entry_id:138793)**, typically at higher energies (ultraviolet frequencies). At frequencies below these transitions, their collective off-resonant response can be approximated by a constant, frequency-independent background polarizability, which contributes a term $\epsilon_\infty$ to the permittivity. Thus, the total permittivity is given by the Drude model:

$$
\epsilon_m(\omega) = \epsilon_\infty + \chi_{\text{free}}(\omega) = \epsilon_\infty - \frac{\omega_p^2}{\omega(\omega + i\gamma)}
$$

Separating this into its real and imaginary parts yields:

$$
\mathrm{Re}[\epsilon_m(\omega)] = \epsilon_m'(\omega) = \epsilon_\infty - \frac{\omega_p^2}{\omega^2 + \gamma^2}
$$

$$
\mathrm{Im}[\epsilon_m(\omega)] = \epsilon_m''(\omega) = \frac{\omega_p^2 \gamma}{\omega(\omega^2 + \gamma^2)}
$$

The physical significance of these parameters is paramount for understanding plasmonic phenomena [@problem_id:2864034]:
- The **plasma frequency** $\omega_p$ is determined by intrinsic material properties: the conduction electron density $n$ and their effective mass $m^*$. Metals with higher electron densities, like aluminum, have higher plasma frequencies than [noble metals](@entry_id:189233) like gold or silver.
- The **damping rate** $\gamma$ encapsulates all momentum-relaxing scattering processes. It is directly related to the metal's electrical resistivity and is the primary source of Ohmic loss for [plasmons](@entry_id:146184). Since [electron-phonon scattering](@entry_id:138098) is a major contributor, $\gamma$ typically increases with temperature.
- The **background [permittivity](@entry_id:268350)** $\epsilon_\infty$ represents the contribution of core electron polarization from off-resonant [interband transitions](@entry_id:138793). For real metals, $\epsilon_\infty > 1$. Its value significantly influences the real part of the [permittivity](@entry_id:268350), $\epsilon_m'(\omega)$, by shifting it to less negative values.

For a [surface plasmon](@entry_id:143470) to exist, the real part of the metal's [permittivity](@entry_id:268350) must be negative, $\epsilon_m'(\omega)  0$, which occurs for frequencies $\omega  \omega_p / \sqrt{\epsilon_\infty}$ in the lossless limit ($\gamma \to 0$).

### Surface Plasmon Polaritons at a Planar Interface

#### The Nature of the SPP: A Hybrid Mode

A **[surface plasmon polariton](@entry_id:138342) (SPP)** is an electromagnetic excitation that exists at the interface between a dielectric and a conductor. It is a hybrid mode, arising from the strong coupling between photons and the [collective oscillations](@entry_id:158973) of [conduction electrons](@entry_id:145260), known as [surface plasmons](@entry_id:145851). These modes are bound to the interface, with their fields decaying exponentially into both media.

An essential feature of an SPP is that it is a **transverse-magnetic (TM)** wave. This means the magnetic field vector is oriented parallel to the interface and perpendicular to the direction of propagation (e.g., $\mathbf{H}$ along $\hat{\mathbf{y}}$ for propagation along $\hat{\mathbf{x}}$), while the electric field vector lies in the sagittal plane (the $xz$-plane). The TM nature is intimately connected to the physical origin of the mode: an oscillating sheet of [surface charge density](@entry_id:272693).

From Maxwell's equations, the boundary conditions at a source-free interface require that the tangential component of the magnetic field ($\mathbf{H}$) and the normal component of the [electric displacement field](@entry_id:203286) ($\mathbf{D}$) be continuous. For a TM wave at a [metal-dielectric interface](@entry_id:261990) at $z=0$, this leads to a discontinuity in the normal component of the electric field, $E_z$. This discontinuity is directly related to the [induced surface charge density](@entry_id:276080), $\rho_s$, via Gauss's law [@problem_id:2864053]:

$$
\rho_s = \epsilon_0 \left( E_z^{(\mathrm{d})} - E_z^{(\mathrm{m})} \right)
$$

where $E_z^{(\mathrm{d})}$ and $E_z^{(\mathrm{m})}$ are the normal electric field components on the dielectric and metal sides of the interface, respectively. It is this dynamic accumulation of charge, oscillating in synchrony with the electromagnetic field, that constitutes the "plasmon" part of the polariton. The electromagnetic fields guide the charge oscillation, and the charge oscillation, in turn, sustains the fields, creating a self-consistent, propagating [bound state](@entry_id:136872).

#### Derivation of the SPP Dispersion Relation

To formalize the description of an SPP, we seek a solution to Maxwell's equations at the interface between a metal ($z0$, [permittivity](@entry_id:268350) $\epsilon_m$) and a dielectric ($z>0$, permittivity $\epsilon_d$). We assume a TM wave propagating along the $x$-direction with a wavevector $k_\parallel$ and decaying away from the interface at $z=0$. The magnetic field can be written as:

$$
\mathbf{H}(x, z, t) = \hat{\mathbf{y}} H_0 \exp(i k_{\parallel} x) \times 
\begin{cases}
\exp(-\kappa_d z) \exp(-i\omega t)  \text{for } z > 0 \\
\exp(+\kappa_m z) \exp(-i\omega t)  \text{for } z  0
\end{cases}
$$

Here, $\kappa_d$ and $\kappa_m$ are the transverse decay constants in the dielectric and metal, respectively. For the wave to be bound, their real parts must be positive. Substituting this ansatz into the Helmholtz wave equation, $\nabla^2 \mathbf{H} + \epsilon_j k_0^2 \mathbf{H} = 0$ (where $k_0 = \omega/c$), in each medium ($j=d, m$), we obtain relations linking the in-plane [wavevector](@entry_id:178620) to the decay constants [@problem_id:2864074]:

$$
k_{\parallel}^2 - \kappa_d^2 = \epsilon_d k_0^2
$$
$$
k_{\parallel}^2 - \kappa_m^2 = \epsilon_m k_0^2
$$

The final piece of the puzzle comes from the [electromagnetic boundary conditions](@entry_id:188865). Continuity of the tangential magnetic field component ($H_y$) at $z=0$ is already ensured by the ansatz. The crucial condition arises from the continuity of the tangential electric field component ($E_x$). Since $\mathbf{E} \propto (1/\epsilon) \nabla \times \mathbf{H}$, the continuity of $E_x$ requires:

$$
\frac{1}{\epsilon_d}\frac{\partial H_y}{\partial z}\bigg|_{z=0^+} = \frac{1}{\epsilon_m}\frac{\partial H_y}{\partial z}\bigg|_{z=0^-} \implies -\frac{\kappa_d}{\epsilon_d} = \frac{\kappa_m}{\epsilon_m}
$$

This elegantly simple equation, $\frac{\kappa_d}{\epsilon_d} + \frac{\kappa_m}{\epsilon_m} = 0$, is the quantization condition that selects the allowed surface modes [@problem_id:2864002] [@problem_id:2864074]. By combining this condition with the two relations from the wave equation, we can eliminate the decay constants and solve for the in-plane wavevector $k_\parallel$. The result is the celebrated **SPP dispersion relation**:

$$
k_{\parallel}(\omega) = k_0 \sqrt{\frac{\epsilon_m(\omega) \epsilon_d}{\epsilon_m(\omega) + \epsilon_d}}
$$

For a truly bound mode to exist, the fields must be evanescent in both media, meaning $\kappa_d$ and $\kappa_m$ must be real and positive (in the lossless limit). This requires that $\epsilon_m$ and $\epsilon_d$ have opposite signs, and that their sum is negative. For a typical interface with a passive dielectric ($\epsilon_d > 0$), the conditions for SPP existence are therefore [@problem_id:2864002]:

$$
\mathrm{Re}[\epsilon_m(\omega)]  0 \quad \text{and} \quad \mathrm{Re}[\epsilon_m(\omega)] + \epsilon_d  0
$$

#### Properties and Characteristics of SPPs

The [dispersion relation](@entry_id:138513) contains a wealth of information about the nature of SPPs.

**Propagation and Confinement**: A useful quantity for characterizing a guided wave is the **effective modal index**, $n_{\mathrm{eff}}$, defined as the ratio of the SPP [wavevector](@entry_id:178620) to the free-space [wavevector](@entry_id:178620):

$$
n_{\mathrm{eff}} = \frac{k_\parallel}{k_0} = \sqrt{\frac{\epsilon_m \epsilon_d}{\epsilon_m + \epsilon_d}}
$$

The effective index directly relates to the in-plane [phase velocity](@entry_id:154045) of the SPP, $v_{\mathrm{ph}} = \omega/k_\parallel = c/n_{\mathrm{eff}}$. Since $n_{\mathrm{eff}}$ is always greater than the refractive index of the dielectric, $\sqrt{\epsilon_d}$, the SPP [phase velocity](@entry_id:154045) is always less than the speed of light in the dielectric. The effective index also quantifies the degree of field confinement to the interface [@problem_id:2864044]. The decay constant into the dielectric, for instance, can be expressed as:

$$
\kappa_d = k_0 \sqrt{n_{\mathrm{eff}}^2 - \epsilon_d}
$$

A larger value of $n_{\mathrm{eff}}$ implies a larger $\kappa_d$, which corresponds to a faster field decay and thus stronger confinement of the SPP mode. As the frequency $\omega$ approaches the [surface plasmon resonance](@entry_id:137332) condition $\mathrm{Re}[\epsilon_m(\omega)] \to -\epsilon_d$, $n_{\mathrm{eff}}$ diverges, leading to extreme confinement and a near-zero group velocity.

Plotting the [dispersion relation](@entry_id:138513) $\omega(k_\parallel)$ reveals that the SPP mode always lies to the right of the "light line" of the dielectric, $\omega = c k_\parallel/\sqrt{\epsilon_d}$. This signifies that at any given frequency, the SPP has a larger momentum than a photon in the dielectric, a crucial fact for understanding SPP excitation. At high momentum ($k_\parallel \to \infty$), the [dispersion curve](@entry_id:748553) flattens and asymptotically approaches the [surface plasmon](@entry_id:143470) frequency $\omega_{SP}$, given by the condition $\mathrm{Re}[\epsilon_m(\omega_{SP})] = -\epsilon_d$ [@problem_id:2864069].

**Propagation Loss**: In a realistic scenario, the metal is lossy, so $\epsilon_m$ is complex. This makes the SPP wavevector $k_\parallel = k' + ik''$ complex as well. The imaginary part, $k'' = \mathrm{Im}[k_\parallel]$, causes the SPP's power, which is proportional to the field intensity squared, to decay exponentially along its propagation path as $\exp(-2k''x)$. The characteristic propagation length is $L_{SPP} = 1/(2k'')$.

The losses can be characterized by a **quality factor**, $Q$, defined as $\omega$ times the ratio of stored energy to power dissipated. For a propagating SPP, this can be related to the imaginary part of the [wavevector](@entry_id:178620). Starting from Poynting's theorem, we find that the power dissipated per unit length, $P_{\mathrm{loss}}$, is related to the total power flow $P$ by $P_{\mathrm{loss}}(x) = 2k''P(x)$. By defining the **energy velocity** $v_E$ as the ratio of power flow to stored energy per unit length, $v_E = P/U$, we arrive at a fundamental relation for the [quality factor](@entry_id:201005) [@problem_id:2863997]:

$$
Q = \omega \frac{U}{P_{\mathrm{loss}}} = \frac{\omega}{2 k'' v_E}
$$

This connects the spatial decay constant ($k''$) to the temporal energy decay rate ($\gamma_{\mathrm{sp}}$) via $v_E$, with $\gamma_{\mathrm{sp}} = v_E k''$.

### Excitation and Damping of Surface Plasmons

#### The Momentum Problem and Prism Coupling

The fact that the SPP [dispersion curve](@entry_id:748553) lies to the right of the dielectric's light line presents a fundamental challenge: at any given frequency, an SPP has more momentum than a photon freely propagating in the dielectric. Due to momentum conservation, it is therefore impossible to excite an SPP by simply shining light onto a smooth [metal-dielectric interface](@entry_id:261990).

To overcome this momentum mismatch, several techniques have been developed. The most common is **[attenuated total reflection](@entry_id:165072) (ATR)** in the **Kretschmann geometry**. This method employs a high-refractive-index prism ($n_p$) brought into close proximity with the plasmonic interface, separated by a thin metal film (typically a few tens of nanometers thick) [@problem_id:2864066].

Light is directed through the prism onto the film at an [angle of incidence](@entry_id:192705) $\theta$ that is greater than [the critical angle](@entry_id:169189) for [total internal reflection](@entry_id:267386) (TIR) at the prism-dielectric interface. In TIR, although no power propagates into the lower-index medium, an **[evanescent wave](@entry_id:147449)** is generated that penetrates a short distance into the medium, with its intensity decaying exponentially.

In the Kretschmann setup, this evanescent wave tunnels through the thin metal film. The in-plane component of the incident photon's wavevector in the prism is given by $k_x = k_0 n_p \sin\theta$. If the angle $\theta$ is adjusted such that this momentum matches the real part of the SPP [wavevector](@entry_id:178620) at the outer [metal-dielectric interface](@entry_id:261990), a resonance occurs:

$$
k_0 n_p \sin(\theta_{\mathrm{res}}) = \mathrm{Re}[k_\parallel]
$$

At this specific resonance angle, $\theta_{\mathrm{res}}$, energy from the incident light is efficiently transferred to the SPP mode. This [energy transfer](@entry_id:174809) manifests as a sharp dip in the intensity of the reflected light.

The thickness of the metal film is a critical parameter. If the film is too thick, the [evanescent field](@entry_id:165393) decays to negligible amplitude before reaching the outer interface, and no coupling occurs. If the film is too thin, the SPP mode is strongly coupled back to the prism, allowing it to easily re-radiate its energy back into the prism. This strong [radiative damping](@entry_id:270883) broadens the resonance dip, degrading its quality. An optimal thickness exists (e.g., ~50 nm for gold at 633 nm) that balances the coupling and intrinsic losses to achieve maximum energy transfer, ideally resulting in near-zero reflectivity at the resonance angle [@problem_id:2864066].

#### Damping Channels

The total damping or loss rate, $\Gamma_{\text{total}}$, of an SPP, which determines its propagation length and the width of its resonance peak, can be decomposed into several distinct channels, assuming they are weakly coupled [@problem_id:2864091]:

$$
\Gamma_{\text{total}} = \Gamma_{\text{Ohmic}} + \Gamma_{\text{rad}} + \Gamma_{\text{scat}}
$$

- **Intrinsic Ohmic Loss ($\Gamma_{\text{Ohmic}}$)**: This is the dominant loss mechanism for SPPs on smooth, thick films. It arises from the absorption of energy within the metal, corresponding to the imaginary part of the [permittivity](@entry_id:268350), $\epsilon_m''$. Microscopically, it is caused by the scattering of electrons with phonons, defects, and other electrons. This channel is inherently temperature-dependent.

- **Radiative Damping ($\Gamma_{\text{rad}}$)**: An ideal SPP on a perfectly smooth, infinite interface is a non-radiative mode. However, in practical configurations like the Kretschmann geometry, the proximity of the high-index prism allows the SPP to leak energy back into the prism, which is then detected as propagating light. This leakage constitutes [radiative damping](@entry_id:270883) and is highly dependent on the metal film thickness.

- **Scattering Loss ($\Gamma_{\text{scat}}$)**: Real metal surfaces are never perfectly smooth. Surface roughness features can act as antennas that scatter the SPP energy into other directions, including into freely propagating light in the dielectric or substrate. This loss mechanism depends on the statistical properties of the surface roughness, such as its root-mean-square height $\sigma$.

Experimentally, these contributions can be isolated. For example, by using an optically thick film, $\Gamma_{\text{rad}}$ can be eliminated, allowing one to study the temperature dependence of $\Gamma_{\text{Ohmic}}$. By varying the film thickness, $\Gamma_{\text{rad}}$ can be controlled and quantified. Finally, by systematically modifying the [surface roughness](@entry_id:171005) (e.g., with ion-beam smoothing) and measuring the resulting change in total damping, $\Gamma_{\text{scat}}$ can be determined [@problem_id:2864091].

### Localized Surface Plasmon Resonances (LSPRs)

#### Plasmons in Subwavelength Particles

When the collective [electron oscillation](@entry_id:173699) is confined to a metallic nanoparticle with dimensions much smaller than the wavelength of light, it is known as a **[localized surface plasmon resonance](@entry_id:157595) (LSPR)**. Unlike the propagating SPPs, LSPRs are non-propagating, [resonant modes](@entry_id:266261).

In the subwavelength regime, the interaction can be analyzed using the **electrostatic (or quasistatic) approximation**, where the phase of the external electric field is considered constant over the volume of the particle. For a general ellipsoidal particle embedded in a dielectric medium $\epsilon_d$ and placed in a uniform external field $\mathbf{E}_0$, the internal field $\mathbf{E}_{\mathrm{int}}$ becomes uniform but is reduced by a [depolarization field](@entry_id:187671). This effect is captured by a geometric **depolarization factor** $L$, which depends on the particle's aspect ratio along the direction of the field [@problem_id:2864026].

The [induced dipole moment](@entry_id:262417) of the particle is proportional to its polarizability, $\alpha$, which can be derived as:

$$
\alpha = V \frac{\epsilon(\omega) - \epsilon_d}{(1-L)\epsilon_d + L\epsilon(\omega)}
$$

where $V$ is the particle volume and $\epsilon(\omega)$ is the metal's [permittivity](@entry_id:268350). The LSPR occurs at the frequency where the polarizability is resonantly enhanced, corresponding to the denominator approaching a minimum. For a weakly-damped metal, this leads to the [resonance condition](@entry_id:754285):

$$
\mathrm{Re}[\epsilon(\omega_{\mathrm{LSPR}})] = -\epsilon_d \frac{1-L}{L}
$$

This powerful result shows that the LSPR frequency is directly tunable through the particle's geometry, which is encoded in $L$. For a sphere, the depolarization factor is $L=1/3$ in all directions, yielding the well-known Fröhlich condition $\mathrm{Re}[\epsilon(\omega)] = -2\epsilon_d$. For a [prolate spheroid](@entry_id:176438) (a nano-rod), the [depolarization](@entry_id:156483) factor for the long axis, $L_a$, decreases as the [aspect ratio](@entry_id:177707) increases. A decrease in $L_a$ requires $\mathrm{Re}[\epsilon(\omega)]$ to become more negative to satisfy the resonance condition. For a Drude-like metal, more negative $\mathrm{Re}[\epsilon]$ values occur at lower frequencies, meaning that **increasing the [aspect ratio](@entry_id:177707) of a nanorod red-shifts its longitudinal LSPR** [@problem_id:2864026]. This geometric tunability is a cornerstone of [nanoplasmonics](@entry_id:174122).

#### Propagating vs. Localized Plasmons: A Comparison

SPPs and LSPRs represent two distinct classes of plasmonic excitations, and their contrasting properties make them suitable for different applications. The key differences can be summarized as follows [@problem_id:2864069]:

- **Dispersion and Excitation**: SPPs are propagating modes with a continuous dispersion relation $\omega(k_\parallel)$. They possess momentum and require special techniques ([prisms](@entry_id:265758), gratings) for excitation. LSPRs are discrete, non-propagating resonances whose frequency is determined by geometry and material properties, not momentum. They can be excited directly by [far-field](@entry_id:269288) illumination.

- **Confinement and Mode Volume**: SPPs are confined to the interface in one dimension but are delocalized in the plane. Their fields typically extend hundreds of nanometers into the dielectric. LSPRs are confined in all three dimensions to a subwavelength volume around the nanoparticle. Their fields decay very rapidly, on the scale of tens of nanometers. Consequently, the effective [mode volume](@entry_id:191589) of an LSPR is many orders of magnitude smaller than that of an SPP.

- **Sensing Applications**: The different field profiles lead to different sensing capabilities. Due to their extended evanescent fields, SPPs are highly sensitive to changes in the bulk refractive index of the surrounding medium, making them ideal for **bulk sensing**. In contrast, the extreme field confinement of LSPRs at the nanoparticle surface makes them exceptionally sensitive to the binding of molecules in a very thin layer right at the surface. Therefore, LSPRs excel at **surface sensing** and can detect very small quantities of analyte [@problem_id:2864069].