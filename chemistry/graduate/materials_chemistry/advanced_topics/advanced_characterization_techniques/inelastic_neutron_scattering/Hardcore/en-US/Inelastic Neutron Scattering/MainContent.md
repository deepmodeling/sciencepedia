## Introduction
To truly understand a material's properties—from its thermal conductivity and magnetic behavior to its response under stress—we must look beyond its static atomic structure and investigate its dynamics. The ceaseless dance of atoms and spins, occurring on scales of picoseconds and angstroms, dictates the macroscopic world we observe. Inelastic Neutron Scattering (INS) stands as a uniquely powerful experimental method capable of providing a direct, quantitative view of these microscopic motions. Its ability to simultaneously resolve both the energy and momentum of elementary excitations makes it an indispensable tool in modern [condensed matter](@keyword=condensed_matter|lang=en-US|style=Feynman) physics, chemistry, and materials science.

This article provides a comprehensive exploration of Inelastic Neutron Scattering, addressing the fundamental question: How can we measure and interpret the rich spectrum of atomic and magnetic dynamics that underpin material properties? We will bridge the gap between abstract quantum theory and tangible experimental results, guiding you through the core concepts and their powerful applications.

The journey is structured into three distinct chapters. First, in **Principles and Mechanisms**, we will build the theoretical foundation, defining the core quantities of energy and momentum transfer and introducing the central concept of the [dynamic structure factor](@keyword=dynamic_structure_factor|lang=en-US|style=Feynman), $S(\mathbf{Q}, \omega)$. We will then dissect the origins and implications of coherent and [incoherent scattering](@keyword=incoherent_scattering|lang=en-US|style=Feynman). Following this, **Applications and Interdisciplinary Connections** will showcase the power of INS by exploring its use in mapping phonon and [magnon](@keyword=magnon|lang=en-US|style=Feynman) dispersions, unraveling the mysteries of [quantum magnetism](@keyword=quantum_magnetism|lang=en-US|style=Feynman), and characterizing the complex diffusive motions in soft and biological matter. Finally, **Hands-On Practices** will solidify your understanding by presenting practical problems that connect the physical principles of INS to the experimental realities of making a measurement.

## Principles and Mechanisms

This chapter delves into the fundamental principles and theoretical mechanisms that govern the inelastic scattering of neutrons from [condensed matter](@keyword=condensed_matter|lang=en-US|style=Feynman). We will establish the core theoretical constructs, beginning with the description of the scattering event itself and culminating in the formal relationship between the measured [scattering intensity](@keyword=scattering_intensity|lang=en-US|style=Feynman) and the microscopic dynamics of the sample.

### The Scattering Process: Energy and Momentum Transfer

At its most fundamental level, an inelastic neutron [scattering experiment](@keyword=scattering_experiment|lang=en-US|style=Feynman) measures the changes in a neutron's energy and momentum as it interacts with a sample. A neutron in an incident beam is characterized by its initial wavevector $\mathbf{k}_i$ and kinetic energy $E_i$. After scattering from the sample, it emerges with a final wavevector $\mathbf{k}_f$ and energy $E_f$. The fundamental quantities of interest are the [energy transfer](@keyword=energy_transfer|lang=en-US|style=Feynman), $\hbar\omega$, and the [momentum transfer](@keyword=momentum_transfer|lang=en-US|style=Feynman), $\hbar\mathbf{Q}$, exchanged between the neutron and the sample:

- **Energy Transfer:** $\hbar\omega = E_i - E_f$
- **Momentum Transfer:** $\hbar\mathbf{Q} = \hbar(\mathbf{k}_i - \mathbf{k}_f)$

By convention, a positive [energy transfer](@keyword=energy_transfer|lang=en-US|style=Feynman) ($\hbar\omega > 0$) signifies that the neutron has lost energy to the sample, typically by creating an excitation (such as a phonon or [magnon](@keyword=magnon|lang=en-US|style=Feynman)). This is known as a Stokes process. Conversely, a [negative energy](@keyword=negative_energy|lang=en-US|style=Feynman) transfer ($\hbar\omega  0$) means the neutron has gained energy from the sample by annihilating a pre-existing excitation, a process referred to as an anti-Stokes process.

The relationship between a neutron's energy and its wavevector (or wavelength $\lambda$) is given by the de Broglie relations. For non-relativistic neutrons, the kinetic energy is $E = \frac{p^2}{2m_n} = \frac{\hbar^2 k^2}{2m_n}$, where $p = \hbar k$ and $k=2\pi/\lambda$. These relations allow us to experimentally determine the [energy transfer](@keyword=energy_transfer|lang=en-US|style=Feynman) by measuring the neutron's initial and final wavelengths.

For example, consider a scenario where incident neutrons with a wavelength of $\lambda_i = 4.20$ Å scatter from a crystal and are detected with a final wavelength of $\lambda_f = 4.85$ Å. The neutron has clearly slowed down, indicating it lost energy. The energy of the excitation it created, in this case a single phonon, is precisely this energy loss [@problem_id:1783579]:
$$
\hbar\omega = E_i - E_f = \frac{\hbar^2}{2m_n} \left( k_i^2 - k_f^2 \right) = \frac{h^2}{2m_n} \left( \frac{1}{\lambda_i^2} - \frac{1}{\lambda_f^2} \right)
$$
Substituting the given values and physical constants ($h = 6.626 \times 10^{-34}$ J·s, $m_n = 1.675 \times 10^{-27}$ kg) yields a phonon frequency $\omega/(2\pi)$ of approximately $0.280$ THz. This simple calculation encapsulates the principle of [energy conservation](@keyword=energy_conservation|lang=en-US|style=Feynman) that underpins all inelastic scattering experiments.

The central quantity measured in an experiment is the **double-[differential scattering cross-section](@keyword=differential_scattering_cross_section|lang=en-US|style=Feynman)**, denoted $\frac{d^2\sigma}{d\Omega dE_f}$. This quantity represents the probability that an incident neutron will scatter into a specific solid angle $d\Omega$ with a final energy in the range $[E_f, E_f + dE_f]$. As we will see, this experimental observable is directly proportional to a theoretical function that contains all the information about the microscopic structure and dynamics of the scattering system.

### The Dynamic Structure Factor: S(Q,ω)

The theoretical description of neutron scattering is rooted in quantum mechanical [scattering theory](@keyword=scattering_theory|lang=en-US|style=Feynman), most commonly formulated within the first Born approximation. The interaction between a low-energy neutron and a nucleus is extremely short-ranged and can be effectively modeled by the **Fermi pseudo-potential**:
$$
V(\mathbf{r}) = \frac{2\pi\hbar^2}{m_n} b_j \delta(\mathbf{r} - \mathbf{R}_j)
$$
where $\mathbf{R}_j$ is the position of the $j$-th nucleus and $b_j$ is its **[nuclear scattering](@keyword=nuclear_scattering|lang=en-US|style=Feynman) length**, a phenomenological parameter that quantifies the strength of the interaction.

Within this framework, the double-[differential cross-section](@keyword=differential_cross_section|lang=en-US|style=Feynman) for a system of $N$ nuclei can be shown to be:
$$
\frac{d^2\sigma}{d\Omega dE_f} = N \frac{k_f}{k_i} \frac{\sigma_{\text{scatt}}}{4\pi} S(\mathbf{Q}, \omega)
$$
Here, $\frac{k_f}{k_i}$ is a kinematic factor accounting for the density of final states, and $\sigma_{\text{scatt}}$ is an average scattering cross-section per atom. The most important term is the **[dynamic structure factor](@keyword=dynamic_structure_factor|lang=en-US|style=Feynman)**, $S(\mathbf{Q}, \omega)$. This function is intrinsic to the sample and is independent of the properties of the neutron probe. It is formally defined as the space-time Fourier transform of the density-density correlation function, as first shown by Léon Van Hove:
$$
S(\mathbf{Q}, \omega) = \frac{1}{2\pi N} \int_{-\infty}^{\infty} dt \, e^{-i\omega t} \langle \rho_{-\mathbf{Q}}(0) \rho_{\mathbf{Q}}(t) \rangle
$$
where $\rho_{\mathbf{Q}}(t) = \sum_j e^{-i\mathbf{Q} \cdot \mathbf{R}_j(t)}$ is the Fourier component of the particle density operator at time $t$, and the angled brackets denote a thermal average over the states of the system. In essence, $S(\mathbf{Q}, \omega)$ measures the probability that a density fluctuation with [wavevector](@keyword=wavevector|lang=en-US|style=Feynman) $\mathbf{Q}$ can be excited in the system with an [energy transfer](@keyword=energy_transfer|lang=en-US|style=Feynman) of $\hbar\omega$.

### Coherent and Incoherent Scattering

The [scattering length](@entry_id:142881) $b_j$ is not necessarily the same for all nuclei in a sample, even if they belong to the same chemical element. This variation arises from two sources of randomness:
1.  **Isotopic Distribution:** Most elements have a natural mixture of stable isotopes, each with a different [nuclear scattering](@keyword=nuclear_scattering|lang=en-US|style=Feynman) length.
2.  **Nuclear Spin:** If a nucleus has a non-zero spin $I$, the [scattering length](@entry_id:142881) depends on the total spin of the neutron-nucleus system, which can be $I+1/2$ or $I-1/2$. The random orientation of nuclear spins in an unpolarized sample introduces further variation in $b_j$.

This randomness in the [scattering length](@entry_id:142881) is the physical origin of the fundamental division of [neutron scattering](@keyword=neutron_scattering|lang=en-US|style=Feynman) into **coherent** and **incoherent** components [@problem_id:2493194]. To see this, we must average the scattering cross-section over the random distribution of scattering lengths. The intensity depends on the average of the product $\langle b_j b_l \rangle$. If sites $j$ and $l$ are different, the scattering lengths are uncorrelated, and $\langle b_j b_l \rangle = \langle b \rangle^2$. If $j=l$, the average is simply $\langle b^2 \rangle$. This leads to a natural separation of the [scattering function](@keyword=scattering_function|lang=en-US|style=Feynman).

The scattering can be expressed in terms of two distinct parts, weighted by a coherent and an incoherent cross-section:
$$
\frac{d^2\sigma}{d\Omega dE_f} = \frac{k_f}{k_i} \left[ \sigma_{\text{coh}} S_{\text{coh}}(\mathbf{Q}, \omega) + \sigma_{\text{inc}} S_{\text{inc}}(\mathbf{Q}, \omega) \right]
$$
The coherent and incoherent cross sections are defined in terms of the average scattering length $\langle b \rangle$ and the average squared [scattering length](@entry_id:142881) $\langle b^2 \rangle$:
- **Coherent Cross Section:** $\sigma_{\text{coh}} = 4\pi \langle b \rangle^2$
- **Incoherent Cross Section:** $\sigma_{\text{inc}} = 4\pi (\langle b^2 \rangle - \langle b \rangle^2)$

The quantity $\langle b \rangle$ is the **bound [coherent scattering](@keyword=coherent_scattering|lang=en-US|style=Feynman) length**, $b_{\text{coh}}$, and the quantity $\sqrt{\langle b^2 \rangle - \langle b \rangle^2}$ is related to the **bound [incoherent scattering](@keyword=incoherent_scattering|lang=en-US|style=Feynman) length**, $b_{\text{inc}}$. Note that the incoherent [cross section](@keyword=cross_section|lang=en-US|style=Feynman) is proportional to the variance of the scattering length distribution. If a sample were composed of a single isotope with zero nuclear spin, all $b_j$ would be identical, the variance would be zero, and the scattering would be purely coherent [@problem_id:2493238].

The two dynamic structure factors, $S_{\text{coh}}(\mathbf{Q}, \omega)$ and $S_{\text{inc}}(\mathbf{Q}, \omega)$, probe fundamentally different aspects of the system's dynamics [@problem_id:2493238]:

-   **Coherent Dynamic Structure Factor, $S_{\text{coh}}(\mathbf{Q}, \omega)$:** This function describes the interference of waves scattered from all pairs of nuclei. It is determined by the Fourier transform of the total pair-[correlation function](@keyword=correlation_function|lang=en-US|style=Feynman), which measures the correlation between the position of a particle at the origin at time $t=0$ and another particle at position $\mathbf{r}$ at time $t$. Coherent scattering reveals collective phenomena. For example, in a crystal, the correlated motion of atoms in a lattice wave (a phonon) gives rise to sharp, dispersive features in $S_{\text{coh}}(\mathbf{Q}, \omega)$ that allow for the mapping of [phonon dispersion](@keyword=phonon_dispersion|lang=en-US|style=Feynman) curves, $\omega(\mathbf{q})$. The elastic part ($\omega=0$) of [coherent scattering](@keyword=coherent_scattering|lang=en-US|style=Feynman) gives rise to sharp Bragg peaks due to the static periodic order of the atoms.

-   **Incoherent Dynamic Structure Factor, $S_{\text{inc}}(\mathbf{Q}, \omega)$:** This function arises from the random deviations of scattering lengths from the mean. It describes the scattering from each nucleus independently, with no interference effects. It is determined by the Fourier transform of the self-correlation function, which measures the probability of finding the *same* particle at position $\mathbf{r}$ at time $t$ that was at the origin at time $t=0$. Incoherent scattering thus reveals single-particle dynamics. For example, the one-phonon incoherent inelastic signal from a crystal is related to the [phonon density of states](@keyword=phonon_density_of_states|lang=en-US|style=Feynman), $g(\omega)$, as it averages over all modes in which a single atom can participate. It does not produce Bragg peaks and does not show dispersive features.

### Scattering from Crystalline Solids

In a perfect crystal, the atomic positions $\mathbf{R}_j$ are not random but are arranged on a periodic Bravais lattice. This periodicity has profound consequences for [coherent scattering](@keyword=coherent_scattering|lang=en-US|style=Feynman).

#### The Nuclear Structure Factor and Bragg's Law

Let us first consider [elastic scattering](@keyword=elastic_scattering|lang=en-US|style=Feynman) ($\omega=0$). The total coherent [scattering amplitude](@keyword=scattering_amplitude|lang=en-US|style=Feynman) is a sum of phase factors from all nuclei in the crystal [@problem_id:2493231]. A nucleus in unit cell $\mathbf{R}$ at basis position $\mathbf{r}_j$ contributes a term $b_j e^{i\mathbf{Q}\cdot(\mathbf{R}+\mathbf{r}_j)}$. The total amplitude can be factored into two parts: a sum over all unit cells (the [lattice sum](@keyword=lattice_sum|lang=en-US|style=Feynman)) and a sum over the atoms within a single unit cell (the basis sum).
$$
\mathcal{A}(\mathbf{Q}) = \left( \sum_{\mathbf{R}} e^{i\mathbf{Q}\cdot\mathbf{R}} \right) \left( \sum_{j} b_j e^{i\mathbf{Q}\cdot\mathbf{r}_j} \right)
$$
The first term, the [lattice sum](@keyword=lattice_sum|lang=en-US|style=Feynman), is non-zero only when the [scattering vector](@keyword=scattering_vector|lang=en-US|style=Feynman) $\mathbf{Q}$ is equal to a **[reciprocal lattice vector](@keyword=reciprocal_lattice_vector|lang=en-US|style=Feynman)** $\mathbf{G}$. This is the famous Laue condition for diffraction, which gives rise to sharp **Bragg peaks** in the scattering pattern. The second term is the **nuclear structure factor**, $F_N(\mathbf{Q})$, which modulates the intensity of the Bragg peaks according to the arrangement of atoms within the unit cell. The measured intensity is proportional to $|\mathcal{A}(\mathbf{Q})|^2$. The cross terms in $|F_N(\mathbf{Q})|^2$ encode the interference between atoms within the basis.

#### Phonons and crystal momentum

When we consider inelastic scattering from collective excitations like phonons, the periodicity of the lattice introduces a modified conservation law [@problem_id:1783601]. While true momentum is conserved for the system of the neutron plus the entire crystal, it is not a useful concept because the recoil of the macroscopic crystal is immeasurable. Instead, interactions are governed by the conservation of **[crystal momentum](@keyword=crystal_momentum|lang=en-US|style=Feynman)**.

A phonon is a collective mode with a well-defined wavevector $\mathbf{q}$ (which is restricted to the first Brillouin zone) and energy $\hbar\omega(\mathbf{q})$. When a neutron scatters and creates or annihilates a phonon, the conservation laws are:
-   **Energy Conservation:** $E_f - E_i = \mp \hbar\omega(\mathbf{q})$
-   **Crystal Momentum Conservation:** $\mathbf{k}_f - \mathbf{k}_i = \mathbf{Q} = \mathbf{G} \pm \mathbf{q}$

The appearance of the reciprocal lattice vector $\mathbf{G}$ is crucial. It signifies that the crystal lattice as a whole can recoil, absorbing a discrete momentum "packet" of $\hbar\mathbf{G}$ without a significant change in its kinetic energy due to its enormous mass. This allows a scattering process to be observed in any Brillouin zone centered at a reciprocal lattice point $\mathbf{G}$. Processes with $\mathbf{G}=0$ are called *normal processes*, while those with $\mathbf{G} \neq 0$ are called *Umklapp processes*. This selection rule is the reason coherent inelastic [neutron scattering](@keyword=neutron_scattering|lang=en-US|style=Feynman) can be used to map out the full [phonon dispersion relation](@keyword=phonon_dispersion_relation|lang=en-US|style=Feynman) $\omega(\mathbf{q})$ throughout the reciprocal space.

#### The Debye-Waller Factor

At any finite temperature, atoms in a crystal are not static but vibrate about their equilibrium lattice positions $\mathbf{R}_j$. We can write the instantaneous position as $\mathbf{r}_j(t) = \mathbf{R}_j + \mathbf{u}_j(t)$, where $\mathbf{u}_j(t)$ is the thermal displacement. These [thermal fluctuations](@keyword=thermal_fluctuations|lang=en-US|style=Feynman) smear out the scattering potential and reduce the intensity of [coherent scattering](@keyword=coherent_scattering|lang=en-US|style=Feynman).

This effect is quantified by the **Debye-Waller factor**, $e^{-2W(\mathbf{Q})}$ [@problem_id:2493163]. For a harmonic crystal where displacements follow a Gaussian distribution, the Debye-Waller exponent $2W(\mathbf{Q})$ is the [mean-squared displacement](@keyword=mean_squared_displacement_2|lang=en-US|style=Feynman) of an atom projected onto the direction of the [scattering vector](@keyword=scattering_vector|lang=en-US|style=Feynman) $\mathbf{Q}$:
$$
2W(\mathbf{Q}) = \langle (\mathbf{Q} \cdot \mathbf{u})^2 \rangle
$$
In the multiphonon expansion of the [scattering function](@keyword=scattering_function|lang=en-US|style=Feynman), the term $e^{-2W(\mathbf{Q})}$ appears as a multiplicative pre-factor for *all* [coherent scattering](@keyword=coherent_scattering|lang=en-US|style=Feynman) processes, including elastic Bragg scattering and one-phonon inelastic scattering. For an isotropic (e.g., cubic) crystal, the exponent simplifies to $2W(\mathbf{Q}) = \frac{1}{3} Q^2 \langle u^2 \rangle$, where $\langle u^2 \rangle$ is the total [mean-squared displacement](@keyword=mean_squared_displacement_2|lang=en-US|style=Feynman).

The magnitude of $\langle u^2 \rangle$ increases with temperature $T$ (at high temperatures, $\langle u^2 \rangle \propto T$). Consequently, the Debye-Waller factor causes the intensity of [coherent scattering](@keyword=coherent_scattering|lang=en-US|style=Feynman) to decrease as either the temperature $T$ or the magnitude of the momentum transfer $Q$ increases. This suppression is exponential and often dominates the behavior of the [scattering intensity](@keyword=scattering_intensity|lang=en-US|style=Feynman) at high $Q$.

### Fundamental Principles and Sum Rules

The [dynamic structure factor](@keyword=dynamic_structure_factor|lang=en-US|style=Feynman) is not an arbitrary function but is subject to several exact constraints that arise from the fundamental principles of statistical mechanics and quantum mechanics.

#### Detailed Balance

For any system in thermal equilibrium at a temperature $T$, the rates of processes and their time-reversed counterparts are related. For scattering, this principle of **detailed balance** connects the probability of the neutron losing energy $\hbar\omega$ (Stokes) to the probability of it gaining the same amount of energy (anti-Stokes) [@problem_id:2493201]. This leads to a fundamental relation between the positive and [negative frequency](@keyword=negative_frequency|lang=en-US|style=Feynman) parts of the [dynamic structure factor](@keyword=dynamic_structure_factor|lang=en-US|style=Feynman):
$$
S(\mathbf{Q}, -\omega) = e^{-\hbar\omega / (k_B T)} S(\mathbf{Q}, \omega)
$$
This means the scattering spectrum is not symmetric about $\omega=0$. The anti-Stokes side ($S(\mathbf{Q}, -\omega)$) is always suppressed relative to the Stokes side ($S(\mathbf{Q}, \omega)$) by the Boltzmann factor $e^{-\hbar\omega / (k_B T)}$. This makes physical sense: to gain energy, the neutron must annihilate an excitation that was already thermally populated in the sample. The probability of this is lower than the probability of creating an excitation. This relation is a powerful tool for experimentalists to check the thermal equilibrium of their sample or to determine its [effective temperature](@keyword=effective_temperature|lang=en-US|style=Feynman) from the measured asymmetry.

#### The Fluctuation-Dissipation Theorem

One of the most profound results in [statistical physics](@keyword=statistical_physics|lang=en-US|style=Feynman) is the **[fluctuation-dissipation theorem](@keyword=fluctuation_dissipation_theorem|lang=en-US|style=Feynman)**. It establishes a rigorous and general link between the spectrum of microscopic fluctuations in a system at thermal equilibrium and the system's dissipative response to an external perturbation. In the context of neutron scattering, it relates the [dynamic structure factor](@keyword=dynamic_structure_factor|lang=en-US|style=Feynman) $S(\mathbf{Q}, \omega)$, which measures spontaneous density fluctuations, to the imaginary part of the generalized [dynamic susceptibility](@keyword=dynamic_susceptibility|lang=en-US|style=Feynman), $\chi''(\mathbf{Q}, \omega)$, which quantifies energy dissipation [@problem_id:2493166].

The theorem can be stated in several equivalent forms:
$$
\chi''(\mathbf{Q}, \omega) = \pi \left(1 - e^{-\beta\hbar\omega}\right) S(\mathbf{Q}, \omega)
$$
where $\beta = 1/(k_B T)$. Using the definition of the Bose-Einstein population factor, $n(\omega) = (e^{\beta\hbar\omega}-1)^{-1}$, this can be rewritten as:
$$
\chi''(\mathbf{Q}, \omega) = \pi \frac{S(\mathbf{Q}, \omega)}{n(\omega) + 1}
$$
Furthermore, by invoking the detailed balance relation, one can express the susceptibility in a way that is particularly useful in experimental analysis, as it removes the explicit dependence on the thermal factors:
$$
\chi''(\mathbf{Q}, \omega) = \pi \left[ S(\mathbf{Q}, \omega) - S(\mathbf{Q}, -\omega) \right]
$$
This theorem is immensely powerful because it connects a measured quantity, $S(\mathbf{Q}, \omega)$, to a theoretical quantity, $\chi(\mathbf{Q}, \omega)$, which is often more straightforward to calculate using theoretical formalisms like [linear response theory](@keyword=linear_response_theory|lang=en-US|style=Feynman).

#### Moment Sum Rules

The [dynamic structure factor](@keyword=dynamic_structure_factor|lang=en-US|style=Feynman) also obeys a set of **moment sum rules**, which are integral constraints on its shape. These rules relate the frequency moments of $S(\mathbf{Q}, \omega)$ to static properties of the system. The most important of these is the first moment, or **$f$-sum rule** [@problem_id:2493203]. For any monatomic [system of particles](@keyword=system_of_particles|lang=en-US|style=Feynman) of mass $m$, it states:
$$
\int_{-\infty}^{\infty} \omega S(\mathbf{Q}, \omega) d\omega = \frac{\hbar Q^2}{2m}
$$
This result is exact and remarkably general: it is independent of the temperature, the phase of matter (liquid, solid, or gas), and the details of the [interatomic potential](@keyword=interatomic_potential|lang=en-US|style=Feynman). It is a direct consequence of particle number conservation and the [commutation relations](@keyword=commutation_relations|lang=en-US|style=Feynman) between position and momentum. The sum rule provides a crucial check on the absolute normalization of experimental data and theoretical models, ensuring that the total [spectral weight](@keyword=spectral_weight|lang=en-US|style=Feynman) is correctly accounted for.

### From Theory to Reality: Instrumental Resolution

The theoretical framework described above deals with an ideal [dynamic structure factor](@keyword=dynamic_structure_factor|lang=en-US|style=Feynman), $S(\mathbf{Q}, \omega)$. In any real experiment, the measurement is smeared or blurred by the finite resolution of the instrument. This is due to factors such as the divergence of the neutron beam, the distribution of neutron velocities from the moderator, and the finite size and timing uncertainties of choppers and detectors.

This instrumental effect is described by a **resolution function**, $R(\Delta\mathbf{Q}, \Delta\omega)$, which can be thought of as the probability density that a scattering event with true transfers $(\mathbf{Q}', \omega')$ will be measured at the nominal instrument setting $(\mathbf{Q}, \omega)$ [@problem_id:2493177]. If the instrument response is linear and shift-invariant, the measured intensity, $I_{\text{meas}}(\mathbf{Q}, \omega)$, is a convolution of the true [dynamic structure factor](@keyword=dynamic_structure_factor|lang=en-US|style=Feynman) with the resolution function:
$$
I_{\text{meas}}(\mathbf{Q}, \omega) = \int d\mathbf{Q}' d\omega' \, R(\mathbf{Q}-\mathbf{Q}', \omega-\omega') S(\mathbf{Q}', \omega')
$$
In the limit of a perfect instrument, the resolution function becomes a Dirac delta function, $R(\Delta\mathbf{Q}, \Delta\omega) = \delta(\Delta\mathbf{Q})\delta(\Delta\omega)$, and the measured intensity is identical to the true $S(\mathbf{Q}, \omega)$. In practice, $R$ is a finite-width function, often approximated by a four-dimensional Gaussian, which broadens sharp features in the true spectrum. A [quantitative analysis](@keyword=quantitative_analysis|lang=en-US|style=Feynman) of inelastic [neutron scattering](@keyword=neutron_scattering|lang=en-US|style=Feynman) data requires a careful understanding and modeling of this resolution function to deconvolve its effects and extract the intrinsic properties of the sample.