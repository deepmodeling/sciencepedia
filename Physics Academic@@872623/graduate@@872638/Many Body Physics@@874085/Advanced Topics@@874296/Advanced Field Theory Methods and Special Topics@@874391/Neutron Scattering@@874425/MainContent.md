## Introduction
Neutron scattering stands as one of the most powerful and versatile techniques in the arsenal of [condensed matter](@entry_id:747660) science, offering a unique window into the microscopic world of materials. Its ability to simultaneously reveal where atoms are and how they move makes it indispensable for understanding the fundamental properties of solids, liquids, and [complex fluids](@entry_id:198415). However, translating the raw data of a scattering experiment—counts in a detector—into a rich picture of atomic-scale structure and dynamics requires a deep understanding of the underlying physical principles. This article aims to bridge that gap, providing a comprehensive guide to the theory and practice of neutron scattering.

The journey begins in **Principles and Mechanisms**, which lays the theoretical groundwork. We will explore the [kinematics](@entry_id:173318) of the scattering process, define the crucial concepts of momentum and energy transfer, and establish the formal connection between the measured cross-section and the microscopic Van Hove correlation functions. You will learn how scattering is separated into coherent and incoherent components, which respectively probe collective and single-particle behavior, and discover how the neutron's magnetic moment makes it an exquisite probe of magnetism.

Building on this foundation, **Applications and Interdisciplinary Connections** showcases the immense practical power of neutron scattering. We will traverse diverse scientific fields—from physics and materials science to chemistry and biology—demonstrating how techniques like diffraction, [small-angle scattering](@entry_id:754965), and inelastic spectroscopy are used to solve real-world problems. You will see how neutrons locate light atoms in complex structures, map out polymer conformations, determine intricate magnetic orders, and measure the dispersion of elementary excitations like phonons and magnons.

Finally, to solidify this knowledge, **Hands-On Practices** presents targeted problems that connect theory to experimental reality, from designing beam filters to modeling diffusion signals. This comprehensive exploration will equip you with the knowledge to interpret neutron scattering data and appreciate its profound impact on modern science. We begin by delving into the core principles that govern how a neutron interacts with matter.

## Principles and Mechanisms

Neutron scattering is a uniquely powerful technique for probing the structure and dynamics of condensed matter. The interaction of a thermal neutron with a material provides simultaneous information about the spatial arrangement of atoms and their motions. This chapter delineates the fundamental principles governing the neutron scattering process, from the [kinematics](@entry_id:173318) of a single scattering event to the statistical mechanics of collective phenomena. We will explore how the measured [scattering cross-section](@entry_id:140322) is formally related to the microscopic [correlation functions](@entry_id:146839) of the system, and how this relationship allows us to decipher atomic-scale structure, [lattice vibrations](@entry_id:145169), diffusive motion, and magnetic order.

### The Kinematics of Scattering

At its core, a neutron scattering experiment measures the change in a neutron's momentum and energy as it interacts with a sample. A neutron is characterized by its wavevector $\vec{k}$ and its kinetic energy $E$. For non-relativistic [thermal neutrons](@entry_id:270226), these quantities are related by:

$E = \frac{\hbar^2 |\vec{k}|^2}{2 m_n}$

where $m_n$ is the neutron mass and $\hbar$ is the reduced Planck constant. The magnitude of the wavevector is related to the neutron's de Broglie wavelength $\lambda$ by $|\vec{k}| = 2\pi / \lambda$.

In a scattering experiment, a neutron from a well-defined incident beam (with initial wavevector $\vec{k}_i$ and energy $E_i$) strikes the sample and is scattered into a final state (with wavevector $\vec{k}_f$ and energy $E_f$), which is registered by a detector. The two key quantities that characterize this interaction are the **[momentum transfer vector](@entry_id:153928)** $\vec{Q}$ and the **energy transfer** $\hbar\omega$, defined by the conservation laws:

$\vec{Q} = \vec{k}_i - \vec{k}_f$

$\hbar\omega = E_i - E_f = \frac{\hbar^2}{2 m_n} (|\vec{k}_i|^2 - |\vec{k}_f|^2)$

The [momentum transfer](@entry_id:147714) $\vec{Q}$ represents the momentum exchanged between the neutron and the sample, and it acts as the inverse length scale of the probe. The [energy transfer](@entry_id:174809) $\hbar\omega$ is the energy lost by the neutron to the sample. If $\hbar\omega > 0$, the neutron has lost energy by creating an excitation in the sample (a Stokes process). If $\hbar\omega  0$, the neutron has gained energy by annihilating a pre-existing excitation (an anti-Stokes process). If $\hbar\omega = 0$, the scattering is **elastic**, probing static structure. If $\hbar\omega \neq 0$, the scattering is **inelastic**, probing dynamics.

The magnitude of the [momentum transfer vector](@entry_id:153928), $Q = |\vec{Q}|$, is determined by the magnitudes of the initial and final wavevectors and the scattering angle $\theta$ between them, according to the law of cosines:

$Q^2 = |\vec{k}_i|^2 + |\vec{k}_f|^2 - 2 |\vec{k}_i| |\vec{k}_f| \cos\theta$

As a practical example, consider an [inelastic neutron scattering](@entry_id:140691) experiment where incident neutrons of wavelength $\lambda_i = 4.00$ Å scatter from a crystal and are detected at an angle of $\theta = 60.0^\circ$ with a final wavelength of $\lambda_f = 4.50$ Å. The [wavevector](@entry_id:178620) magnitudes are $k_i = 2\pi/\lambda_i \approx 1.571$ Å⁻¹ and $k_f = 2\pi/\lambda_f \approx 1.396$ Å⁻¹. Applying the law of cosines yields a [momentum transfer](@entry_id:147714) magnitude of $Q \approx 1.49$ Å⁻¹. The energy transfer is calculated from the change in kinetic energy, yielding $\hbar\omega \approx 1.07$ meV. These two values, $(Q, \hbar\omega)$, pinpoint a specific excitation in the material's dynamic response [@problem_id:1999729].

### The Scattering Cross-Section and Correlation Functions

The probability of a scattering event is quantified by the **double-[differential scattering cross-section](@entry_id:172304)**, $\frac{d^2\sigma}{d\Omega dE_f}$, which measures the fraction of neutrons scattered into a [solid angle](@entry_id:154756) element $d\Omega$ with a final energy in a range $dE_f$. In the first Born approximation, this cross-section is directly proportional to a quantity that contains all the physics of the sample: the **[dynamic structure factor](@entry_id:143433)**, $S(\vec{Q}, \omega)$.

#### Coherent and Incoherent Scattering

The fundamental interaction for [nuclear scattering](@entry_id:172564) is described by a single parameter for each nucleus, the **scattering length** $b$. However, the scattering from an assembly of atoms is complicated by the fact that a given chemical element may consist of multiple isotopes, each with a different [scattering length](@entry_id:142881). Furthermore, if a nucleus has a non-zero spin $I$, the [scattering length](@entry_id:142881) depends on the relative orientation of the neutron and nuclear spins.

This randomness in the [scattering length](@entry_id:142881) across the sample gives rise to a crucial division of the scattering into two components: coherent and incoherent. Let us consider a sample of a single element with various isotopes $i$ of fractional abundance $f_i$, where each isotope has a set of possible scattering lengths $b_{i,s}$ depending on the nuclear spin state $s$, which occurs with probability $p_{s}$. The average [scattering length](@entry_id:142881) of the element is:

$b_{coh} = \langle b \rangle = \sum_i f_i \sum_s p_{s} b_{i,s}$

The average of the square of the scattering length is:

$\langle b^2 \rangle = \sum_i f_i \sum_s p_{s} b_{i,s}^2$

Scattering that arises from the average [scattering length](@entry_id:142881), $\langle b \rangle$, is called **[coherent scattering](@entry_id:267724)**. It is sensitive to the interference of waves scattered from different nuclei and thus reveals information about the correlation between pairs of atoms. The **coherent cross-section** is defined as $\sigma_{coh} = 4\pi \langle b \rangle^2 = 4\pi b_{coh}^2$.

Scattering that arises from the random deviations of individual scattering lengths from the average is called **[incoherent scattering](@entry_id:190180)**. It carries no phase relation between waves scattered from different sites and thus contains no interference information. It probes the correlation of a single atom with itself over time. The **incoherent cross-section** is proportional to the variance of the scattering length distribution:

$\sigma_{inc} = 4\pi (\langle b^2 \rangle - \langle b \rangle^2)$

This allows us to define a bound [incoherent scattering](@entry_id:190180) length $b_{inc}$ via $\sigma_{inc} = 4\pi b_{inc}^2$. For a hypothetical material like "Fictitium" with two isotopes ($c_A=0.60, b_A=5.0$ fm; $c_B=0.40, b_B=-2.0$ fm), the [total scattering cross-section](@entry_id:168963) per atom is the abundance-weighted average of the individual total cross-sections, $\sigma_{tot} = 4\pi(c_A b_A^2 + c_B b_B^2)$, which is approximately $2.09$ barns [@problem_id:1999707]. It's important to recognize that this [total cross-section](@entry_id:151809) is the sum of the coherent and incoherent parts, $\sigma_{tot} = \sigma_{coh} + \sigma_{inc}$.

In complex materials like alloys, this principle extends. For a random [binary alloy](@entry_id:160005) of Vanadium (V) and Nickel (Ni) with concentration $c_V$, the total incoherent cross-section has contributions from the intrinsic incoherence of V and Ni, plus a term from the chemical disorder itself. This **disorder scattering** arises from the random distribution of two different average scattering lengths, $b_V$ and $b_{Ni}$, on the lattice. The total incoherent cross-section per atom becomes [@problem_id:1174176]:

$\sigma_{inc, alloy} = c_V \sigma_{inc,V} + (1-c_V) \sigma_{inc,Ni} + 4\pi c_V(1-c_V)(b_V - b_{Ni})^2$

#### The Van Hove Correlation Function and Dynamic Structure Factors

The rigorous connection between the macroscopic cross-section and the microscopic atomic correlations was established by Léon Van Hove. He introduced the **space-[time correlation function](@entry_id:149211)** $G(\vec{r}, t)$, which describes the probability of finding a particle at position $\vec{r}$ at time $t$ if there was a particle at the origin at time $t=0$. This function naturally separates into two parts [@problem_id:1999735]:

1.  The **self-[correlation function](@entry_id:137198)**, $G_s(\vec{r}, t)$: This gives the probability that the *same* particle that was at the origin at $t=0$ has moved to position $\vec{r}$ at time $t$. It describes single-particle motion.
2.  The **distinct-correlation function**, $G_d(\vec{r}, t)$: This gives the probability of finding a *different* particle at position $\vec{r}$ at time $t$, given there was a particle at the origin at $t=0$. It describes the structure and dynamics of the surrounding particles.

The power of this formalism is that the coherent and [incoherent scattering](@entry_id:190180) components are direct probes of these two functions. The double-[differential cross-section](@entry_id:137333) per atom can be expressed as:

$\frac{d^2\sigma}{d\Omega dE_f} = \frac{k_f}{k_i} \left[ b_{coh}^2 S_{coh}(\vec{Q}, \omega) + b_{inc}^2 S_{inc}(\vec{Q}, \omega) \right]$

where $S_{coh}(\vec{Q}, \omega)$ and $S_{inc}(\vec{Q}, \omega)$ are the coherent and incoherent dynamic structure factors, respectively. They are the full space-time Fourier transforms of the total and self-[correlation functions](@entry_id:146839):

$S(\vec{Q}, \omega) = S_{coh}(\vec{Q}, \omega) + S_{inc}(\vec{Q}, \omega) = \frac{1}{2\pi\hbar} \iint G(\vec{r},t) e^{i(\vec{Q}\cdot\vec{r} - \omega t)} d^3r dt$

$S_{inc}(\vec{Q}, \omega) = \frac{1}{2\pi\hbar} \iint G_s(\vec{r},t) e^{i(\vec{Q}\cdot\vec{r} - \omega t)} d^3r dt$

This provides a direct link between the measured [scattering intensity](@entry_id:202196) and the microscopic correlations in space and time [@problem_id:2493194].

### Probing Structure and Dynamics with Coherent and Incoherent Scattering

The separation into coherent and incoherent components allows us to selectively study collective phenomena or single-particle dynamics.

**Coherent scattering** arises from interference and thus probes correlated structure and dynamics.
*   **Elastic Coherent Scattering ($\omega=0$)**: The time-averaged positions of atoms in a crystal form a [regular lattice](@entry_id:637446). Constructive interference occurs only when the [momentum transfer](@entry_id:147714) $\vec{Q}$ is equal to a [reciprocal lattice vector](@entry_id:276906) $\vec{G}$, leading to sharp **Bragg peaks**. The positions and intensities of these peaks reveal the crystal's unit cell and atomic arrangement.
*   **Inelastic Coherent Scattering ($\omega \neq 0$)**: Correlated motions of atoms, such as lattice vibrations (**phonons**), also produce interference. This gives rise to sharp, dispersive features in $(\vec{Q}, \omega)$ space that map the [phonon dispersion relations](@entry_id:182841), $\omega(\vec{q})$, where $\vec{q}$ is the phonon [wavevector](@entry_id:178620) relative to a [reciprocal lattice](@entry_id:136718) point.

**Incoherent scattering** arises from random deviations and probes single-particle motion, devoid of interference effects.
*   A key feature of [incoherent scattering](@entry_id:190180) is the absence of Bragg peaks.
*   In a crystal, incoherent inelastic scattering is sensitive to the vibrations of individual atoms. By averaging over all modes, it provides a measure of the **vibrational density of states**, $g(\omega)$.
*   In a liquid, the self-[correlation function](@entry_id:137198) $G_s(\vec{r},t)$ for a particle undergoing [simple diffusion](@entry_id:145715) can be modeled by Fick's law. The Fourier transform of this function shows that the incoherent [dynamic structure factor](@entry_id:143433) $S_{inc}(\vec{Q}, \omega)$ takes the form of a Lorentzian function centered at $\omega=0$ [@problem_id:1999740, @problem_id:1999775]:

$S_{inc}(\vec{Q}, \omega) \propto \frac{D Q^2}{\omega^2 + (D Q^2)^2}$

This peak is known as the **quasi-elastic** peak. Its width is directly proportional to the [self-diffusion coefficient](@entry_id:754666) $D$ of the atoms. By measuring the broadening of the elastic line in an [incoherent scattering](@entry_id:190180) experiment, one can directly measure [atomic diffusion](@entry_id:159939) [@problem_id:1999772]. For example, in liquid argon, a measured quasi-elastic broadening of $\Gamma = 0.120$ meV at $E_i = 15.0$ meV and $\theta=60^\circ$ allows for the determination of the [self-diffusion coefficient](@entry_id:754666) $D \approx 0.126 \times 10^{-9} \text{ m}^2/\text{s}$. This powerful capability distinguishes neutron scattering from techniques like X-ray scattering, which are almost purely coherent.

A purely coherent scatterer (a hypothetical monoisotopic, zero-spin element) would show only Bragg peaks and dispersive phonons. A purely incoherent scatterer (like Vanadium, which has a negative scattering length for one spin state, making $\langle b \rangle \approx 0$) would show no Bragg peaks and its inelastic spectrum would reflect the single-particle density of states [@problem_id:2493238].

#### The Debye-Waller Factor

At any finite temperature, atoms are not fixed at their lattice sites but vibrate thermally. The intensity of [coherent scattering](@entry_id:267724), both elastic and inelastic, is reduced by these vibrations. This reduction is quantified by the **Debye-Waller factor**, $\exp(-2W)$. The exponent, often called the Debye-Waller exponent, is given by the thermal average of the atomic displacement squared, projected along the [scattering vector](@entry_id:262662) $\vec{Q}$:

$2W(\vec{Q}) = \langle (\vec{Q} \cdot \vec{u})^2 \rangle$

where $\vec{u}$ is the displacement of an atom from its [equilibrium position](@entry_id:272392). This factor arises because the interference condition for scattering from a periodic array is smeared out by thermal motion. A larger vibrational amplitude (larger $\langle u^2 \rangle$) leads to a stronger suppression of coherent intensity.

The mean square displacement $\langle u^2 \rangle$ increases with temperature. In a simple classical model of harmonic oscillators, equipartition dictates that $\langle u^2 \rangle \propto T$ [@problem_id:1999755]. Therefore, as temperature increases, Bragg peaks and coherent phonon signals become weaker. The Debye-Waller factor also depends on the magnitude of the momentum transfer, with $2W \propto Q^2$. This means that [coherent scattering](@entry_id:267724) is more strongly suppressed at high $Q$. This exponential suppression with $Q^2$ and temperature is a universal feature of scattering from crystalline solids and applies to both elastic and inelastic (one-phonon, multi-phonon) scattering channels [@problem_id:2493163].

### Magnetic Neutron Scattering

The neutron possesses a magnetic dipole moment, despite being electrically neutral. This property makes it an ideal probe for magnetism. The neutron's magnetic moment operator $\boldsymbol{\mu}_n$ is proportional to its [spin operator](@entry_id:149715) $\mathbf{S} = \frac{\hbar}{2}\boldsymbol{\sigma}$ (where $\boldsymbol{\sigma}$ are the Pauli matrices), but with a negative [gyromagnetic ratio](@entry_id:149290) $\gamma_n  0$. This means the magnetic moment vector is directed **antiparallel** to the spin vector [@problem_id:3007083].

The interaction potential for [magnetic scattering](@entry_id:147236) is given by the Zeeman energy of the neutron in the magnetic field $\mathbf{B}(\mathbf{r})$ produced by the electrons in the sample:

$V_M(\mathbf{r}) = -\boldsymbol{\mu}_n \cdot \mathbf{B}(\mathbf{r})$

This interaction is fundamentally different from the scalar nuclear interaction. The scattering amplitude for the magnetic interaction is a vector operator in the neutron's spin space. A detailed derivation shows that the scattering amplitude is proportional to the component of the Fourier-transformed magnetization, $\mathbf{M}(\mathbf{Q})$, that is **perpendicular** to the [scattering vector](@entry_id:262662) $\mathbf{Q}$. This is a crucial selection rule for magnetic neutron scattering.

The scattering cross-section is proportional to the square of the **[magnetic structure](@entry_id:201216) factor**, $\mathbf{F}_M(\mathbf{Q})$, which is a vector quantity defined as:

$\mathbf{F}_M(\mathbf{Q}) = \sum_j \mathbf{m}_j f_j(Q) e^{i\mathbf{Q}\cdot\mathbf{r}_j} e^{-W_j}$

Here, the sum is over all magnetic atoms $j$ in the unit cell at positions $\mathbf{r}_j$, $\mathbf{m}_j$ is the vector magnetic moment of atom $j$, $f_j(Q)$ is the [magnetic form factor](@entry_id:136670) (the Fourier transform of the unpaired electron density), and $e^{-W_j}$ is the Debye-Waller factor.

Due to the selection rule, the measured intensity of a magnetic Bragg peak is not proportional to $|\mathbf{F}_M(\mathbf{Q})|^2$, but rather to the square of its component perpendicular to $\mathbf{Q}$, denoted $\mathbf{F}_{M\perp}(\mathbf{Q})$ [@problem_id:3007099]:

$I_{mag}(\mathbf{Q}) \propto |\mathbf{F}_{M\perp}(\mathbf{Q})|^2 = |\mathbf{F}_M(\mathbf{Q}) - \hat{\mathbf{Q}}(\hat{\mathbf{Q}} \cdot \mathbf{F}_M(\mathbf{Q}))|^2$

where $\hat{\mathbf{Q}} = \mathbf{Q}/|\mathbf{Q}|$. The term $(\delta_{\alpha\beta} - \hat{Q}_\alpha \hat{Q}_\beta)$ is the **magnetic polarization factor** that projects out the components of magnetization parallel to $\mathbf{Q}$ [@problem_id:3007130]. This factor leads to characteristic variations in magnetic [scattering intensity](@entry_id:202196) depending on the orientation of the magnetic moments relative to $\mathbf{Q}$. For example, in a uniaxial antiferromagnet with moments aligned along the $\hat{z}$ axis, the inelastic scattering intensity from transverse spin waves ([magnons](@entry_id:139809)) varies with the angle $\theta$ between $\mathbf{Q}$ and $\hat{z}$ as $I(\theta) \propto 1 + \cos^2\theta$ [@problem_id:2493173]. This orientational dependence is a powerful tool for determining magnetic structures.

### Fundamental Theorems and Practical Aspects

The [dynamic structure factor](@entry_id:143433) is not just an empirical quantity; it is deeply rooted in statistical mechanics, obeying several fundamental theorems.

#### Detailed Balance and the Fluctuation-Dissipation Theorem

For a system in thermal equilibrium at temperature $T$, the processes of creating an excitation (energy loss, $\omega0$) and annihilating an excitation (energy gain, $\omega0$) are not equally likely. The probability of finding the system in a state from which it can give up energy $\hbar\omega$ is suppressed by a Boltzmann factor compared to finding it in a state that can absorb that energy. This leads to the principle of **detailed balance**:

$\frac{S(\vec{Q}, \omega)}{S(\vec{Q}, -\omega)} = \exp\left(\frac{\hbar\omega}{k_B T}\right)$

This relation reflects the thermal population of excited states. The ratio of Stokes to anti-Stokes scattering is a direct measure of the sample temperature [@problem_id:1999746]. For example, by analyzing the ratio of intensities at positive and [negative energy](@entry_id:161542) transfers for a series of data points, one can extract the effective temperature of the sample [@problem_id:2493201].

An even deeper result is the **fluctuation-dissipation theorem**. It states that the [dynamic structure factor](@entry_id:143433) $S(\vec{Q}, \omega)$, which describes spontaneous [thermal fluctuations](@entry_id:143642) in the system, is directly proportional to the imaginary part of the generalized [dynamic susceptibility](@entry_id:139739), $\chi''(\vec{Q}, \omega)$, which describes how the system dissipates energy when driven by an external field. The relation is:

$\chi''(\vec{Q}, \omega) = \pi (1 - e^{-\hbar\omega/k_B T}) S(\vec{Q}, \omega)$

This theorem is profound because it connects a quantity measured in thermal equilibrium ($S$) to a non-equilibrium response property ($\chi''$). There are several equivalent ways to write this relation, for instance, using the Bose-Einstein function $n(\omega) = 1/(\exp(\hbar\omega/k_B T)-1)$, or by taking the difference between the positive and negative energy transfer signals: $\chi''(\vec{Q}, \omega) = \pi [S(\vec{Q}, \omega) - S(\vec{Q}, -\omega)]$ [@problem_id:2493166].

#### Sum Rules

Integrating the [dynamic structure factor](@entry_id:143433) over frequency yields sum rules that relate dynamic properties to static ones.
*   The **zeroth moment**, $\int S(\vec{Q}, \omega) d\omega$, is proportional to the [static structure factor](@entry_id:141682) $S(\vec{Q})$. In the [low-temperature limit](@entry_id:267361) for a simple excitation model, the energy-integrated intensity is proportional to the static susceptibility $\chi(\vec{Q}, \omega=0)$ [@problem_id:129578].
*   The **first moment sum rule** (or [f-sum rule](@entry_id:147775)) is a particularly powerful result:
    $\int_{-\infty}^{\infty} \omega S_{coh}(\vec{Q}, \omega) d\omega = \frac{\hbar Q^2}{2m}$
    This states that the average [energy transfer](@entry_id:174809) in [coherent scattering](@entry_id:267724) is exactly the recoil energy of a single, free particle of mass $m$. Remarkably, this result is independent of the temperature and the details of the [interatomic potential](@entry_id:155887), providing a rigorous constraint on experimental data [@problem_id:1999766].

#### Experimental Realities

The measured intensity is never a perfect representation of the true $S(\vec{Q}, \omega)$.
*   **Instrument Resolution**: Any real instrument has a finite resolution in both momentum and energy. The measured intensity $I_{meas}(\vec{Q}, \omega)$ is a convolution of the true [dynamic structure factor](@entry_id:143433) with the instrument's **resolution function** $R(\Delta \vec{Q}, \Delta \omega)$:
    $I_{meas}(\vec{Q}, \omega) = \iint R(\vec{Q}-\vec{Q}', \omega-\omega') S(\vec{Q}', \omega') d^3Q' d\omega'$
    Understanding and modeling this convolution is essential for quantitative data analysis [@problem_id:2493177].
*   **Multiple Scattering**: The theoretical framework presented assumes that each neutron scatters only once in the sample. In reality, especially in thick or strongly scattering samples (e.g., those containing hydrogen), **multiple scattering** can occur. The probability of a neutron interacting at least once can be estimated as $1-\exp(-\Sigma t)$, where $\Sigma$ is the total macroscopic [cross section](@entry_id:143872) and $t$ is the sample thickness. If this value is large (e.g., for a 5 mm thick sample with $\Sigma=10 \text{ cm}^{-1}$, the probability is over 99%), multiple scattering will severely distort the measured signal. Mitigation strategies include using thinner samples or [isotopic substitution](@entry_id:174631) (e.g., replacing hydrogen with deuterium, which has a much smaller cross-section) [@problem_id:2493205].

By carefully accounting for these principles and practicalities, neutron scattering provides an unparalleled window into the atomic-scale world of materials.