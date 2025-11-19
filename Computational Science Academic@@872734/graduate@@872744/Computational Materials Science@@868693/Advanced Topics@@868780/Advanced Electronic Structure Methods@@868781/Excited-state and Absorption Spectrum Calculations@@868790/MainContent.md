## Introduction
Calculating the response of materials to light is a central challenge in computational materials science, unlocking our ability to design novel technologies from solar cells to advanced sensors. While ground-state theories like Density Functional Theory (DFT) have revolutionized our understanding of material properties, they are fundamentally insufficient for describing the electronic [excited states](@entry_id:273472) that govern [optical absorption](@entry_id:136597) and emission. This knowledge gap necessitates more advanced theoretical frameworks that can accurately capture the complex [many-body interactions](@entry_id:751663) involved in [electronic excitations](@entry_id:190531).

This article provides a graduate-level introduction to the state-of-the-art methods for computing excited-state properties and [absorption spectra](@entry_id:176058). Across the following sections, we will bridge the gap from fundamental theory to practical application. The first section, **Principles and Mechanisms**, delves into the core formalisms, distinguishing between charged and neutral excitations and detailing the GW approximation, Time-Dependent DFT, and the Bethe-Salpeter Equation. The second section, **Applications and Interdisciplinary Connections**, showcases how these powerful tools are used to interpret experimental data, model material behavior under external fields, and understand [collective phenomena](@entry_id:145962). Finally, **Hands-On Practices** provides a glimpse into applying these concepts to solve concrete computational problems. By navigating these topics, readers will gain a robust understanding of how to computationally predict and interpret the rich world of [optical spectroscopy](@entry_id:141940) in modern materials.

## Principles and Mechanisms

The theoretical description and computational modeling of [excited states](@entry_id:273472) are cornerstones of modern materials science, providing the foundation for understanding and predicting the optical and electronic properties of materials. This chapter delves into the fundamental principles and mechanisms governing [electronic excitations](@entry_id:190531), bridging the gap between quantum mechanical theory and the interpretation of experimental [absorption spectra](@entry_id:176058). We will explore the primary formalisms used to compute [excitation energies](@entry_id:190368) and spectral properties, including [many-body perturbation theory](@entry_id:168555) and [time-dependent density functional theory](@entry_id:164007).

### Distinguishing Charged and Neutral Excitations

Electronic excitations in materials can be broadly categorized into two types: **charged excitations** and **neutral excitations**.

A **charged excitation** involves the addition or removal of an electron from the system. These processes are probed experimentally by techniques such as [photoemission spectroscopy](@entry_id:139547) (PES) for electron removal and inverse [photoemission spectroscopy](@entry_id:139547) (IPES) for electron addition. The energies associated with these events correspond to the electron addition and removal energies, which define the material's [electronic band structure](@entry_id:136694). In a many-body context, the concept of an electron or hole is replaced by a **quasiparticle**: a single-particle-like entity whose properties (like energy and lifetime) are renormalized by its interactions with the surrounding cloud of electrons.

A **neutral excitation**, in contrast, involves the rearrangement of electrons within the system, leaving the total charge unchanged. The most common example is the promotion of an electron from an occupied state to an unoccupied state, creating an **electron-hole pair**. Because the electron and hole are oppositely charged, they attract each other via the Coulomb interaction. If this attraction is strong enough, they can form a [bound state](@entry_id:136872) known as an **[exciton](@entry_id:145621)**. Neutral excitations are typically probed by [optical absorption](@entry_id:136597) or [photoluminescence spectroscopy](@entry_id:140447), where a photon is absorbed to create the excitation or emitted upon its decay.

These two types of excitations are fundamentally different and require distinct theoretical treatments. The energy required to create a free electron and a free hole (the quasiparticle band gap) is generally larger than the energy required to create a bound [exciton](@entry_id:145621) (the optical gap). The difference between these two is the **[exciton binding energy](@entry_id:138355)**.

### Quasiparticle Excitations: The GW Approximation

The accurate calculation of charged [excitation energies](@entry_id:190368) is a central challenge in computational materials science. While Density Functional Theory (DFT) in the Kohn-Sham (KS) formalism provides a powerful framework for ground-state properties, the KS eigenvalues are, formally, not the true [quasiparticle energies](@entry_id:173936). The well-known "[band gap problem](@entry_id:143831)" of DFT, where standard approximations like the Local Density Approximation (LDA) or Generalized Gradient Approximations (GGA) systematically underestimate the fundamental band gap of semiconductors and insulators, is a direct manifestation of this limitation.

Many-Body Perturbation Theory (MBPT) provides a rigorous framework for calculating [quasiparticle energies](@entry_id:173936). The central quantity is the one-particle Green's function, whose poles correspond to the true electron addition and removal energies. The [quasiparticle energies](@entry_id:173936) $E_{n}^{\mathrm{QP}}$ are found by solving the quasiparticle equation:
$$
E_{n}^{\mathrm{QP}} = \varepsilon_{n}^{\mathrm{KS}} + \langle \phi_{n} | \Sigma(E_{n}^{\mathrm{QP}}) - v_{xc} | \phi_{n} \rangle
$$
where $\varepsilon_{n}^{\mathrm{KS}}$ and $|\phi_{n}\rangle$ are the Kohn-Sham eigenvalue and orbital for state $n$, $v_{xc}$ is the ground-state [exchange-correlation potential](@entry_id:180254), and $\Sigma(E_{n}^{\mathrm{QP}})$ is the electron **[self-energy](@entry_id:145608)**. The self-energy operator, $\Sigma$, is a non-local and energy-dependent operator that encapsulates all the many-body exchange and correlation effects beyond the mean-field description of the Hartree potential.

The **GW approximation** (GWA), pioneered by Lars Hedin, is the state-of-the-art method for computing the [self-energy](@entry_id:145608). In this approximation, the self-energy is given by the product of the one-particle Green's function ($G$) and the dynamically screened Coulomb interaction ($W$):
$$
\Sigma(E) \approx i \int \frac{d\omega'}{2\pi} G(E+\omega') W(\omega')
$$
Here, $W(\omega) = \varepsilon^{-1}(\omega)v$ is the Coulomb interaction $v$ screened by the [frequency-dependent dielectric function](@entry_id:139439) $\varepsilon(\omega)$, which is typically calculated within the Random Phase Approximation (RPA).

Solving the quasiparticle equation is complicated by the energy dependence of $\Sigma$. A common and effective simplification is to linearize the self-energy term around the Kohn-Sham energy $\varepsilon_{n}^{\mathrm{KS}}$. This first-order Taylor expansion leads to a direct expression for the quasiparticle energy:
$$
E_{n}^{\mathrm{QP}} \approx \varepsilon_{n}^{\mathrm{KS}} + \frac{\langle \phi_{n} | \mathrm{Re}\,\Sigma(\varepsilon_{n}^{\mathrm{KS}}) - v_{xc} | \phi_{n} \rangle}{1 - \left. \frac{\partial}{\partial \omega} \langle \phi_{n} | \mathrm{Re}\,\Sigma(\omega) | \phi_{n} \rangle \right|_{\omega=\varepsilon_{n}^{\mathrm{KS}}}}
$$
The term in the denominator involves the [energy derivative](@entry_id:268961) of the self-energy and leads to the **quasiparticle [renormalization](@entry_id:143501) factor** $Z_n = (1 - \Lambda_n)^{-1}$, where $\Lambda_n$ is the derivative term. This factor, typically between $0.7$ and $0.9$, reflects the reduction in [spectral weight](@entry_id:144751) of the bare particle due to its dressing by [many-body interactions](@entry_id:751663).

As a practical example, consider a hypothetical semiconductor where the KS band gap is $\varepsilon_{c}^{\mathrm{KS}} - \varepsilon_{v}^{\mathrm{KS}} = -5.00 - (-6.20) = 1.20\,\mathrm{eV}$. If a GW calculation provides the self-energy corrections and their derivatives, we can compute the corrected [quasiparticle energies](@entry_id:173936). For instance, with a correction $\Delta\Sigma_v(\varepsilon_v^{\mathrm{KS}}) = -1.00\,\mathrm{eV}$ and renormalization derivative $\Lambda_v = -0.20$ for the [valence band](@entry_id:158227) maximum, the quasiparticle energy becomes $E_{v}^{\mathrm{QP}} = -6.20 + \frac{-1.00}{1 - (-0.20)} \approx -7.03\,\mathrm{eV}$. Similarly, for the conduction band minimum with $\Delta\Sigma_c(\varepsilon_c^{\mathrm{KS}}) = +1.50\,\mathrm{eV}$ and $\Lambda_c = -0.30$, the energy is $E_{c}^{\mathrm{QP}} = -5.00 + \frac{1.50}{1 - (-0.30)} \approx -3.85\,\mathrm{eV}$. The resulting quasiparticle band gap is $E_{g}^{\mathrm{QP}} = E_{c}^{\mathrm{QP}} - E_{v}^{\mathrm{QP}} \approx 3.19\,\mathrm{eV}$, a significant correction from the initial KS gap, which is a characteristic success of the GW method.

### Neutral Excitations I: Time-Dependent DFT

For neutral excitations, Time-Dependent Density Functional Theory (TDDFT) is the most widely used first-principles method. It extends the ground-state DFT framework to time-dependent phenomena, based on the Runge-Gross theorem, which establishes a formal mapping between a time-dependent external potential and the time-dependent electron density.

#### The Real-Time Propagation Approach

One conceptually straightforward way to obtain an [absorption spectrum](@entry_id:144611) is through real-time (RT) TDDFT. The procedure mimics a physical pump-probe experiment computationally.
1.  The system is prepared in its ground state.
2.  At time $t=0$, a weak, impulsive electric field (a "delta-kick") is applied. This perturbation pushes the system into a coherent superposition of the ground state and all accessible [excited states](@entry_id:273472). The interaction is described by a potential $V_{ext}(x, t) = kx\delta(t)$, which imparts a momentum kick to the wavefunction: $\psi(x, 0^+) = \exp(-ikx)\psi_0(x)$.
3.  The time-dependent Kohn-Sham (TDKS) equations are then propagated forward in time, evolving the system under its unperturbed Hamiltonian.
4.  During the [time evolution](@entry_id:153943), the system's time-dependent dipole moment, $d(t) = \int x |\psi(x,t)|^2 dx$, is recorded. This signal contains oscillations at frequencies corresponding to the energy differences between the ground state and the [excited states](@entry_id:273472), i.e., the [excitation energies](@entry_id:190368) $\Omega_k$.
5.  The absorption spectrum, which measures the strength of absorption as a function of photon frequency $\omega$, is proportional to the imaginary part of the frequency-dependent polarizability, $\alpha(\omega)$. By the [fluctuation-dissipation theorem](@entry_id:137014), this is directly related to the Fourier transform of the time-dependent dipole moment:
    $$
    \mathrm{Im}\,\alpha(\omega) \propto \omega \int_{0}^{\infty} d(t) \sin(\omega t) dt
    $$
The resulting spectrum exhibits peaks at the system's neutral [excitation energies](@entry_id:190368). For a quantum harmonic oscillator with confining frequency $\omega_0$, for instance, the dipole selection rule allows transitions only to the first excited state, so the [absorption spectrum](@entry_id:144611) will show a single dominant peak at the frequency $\Omega = \omega_0$.

#### The Linear-Response (Casida) Approach

While RT-TDDFT is intuitive, a more common and often more efficient method for determining discrete [excitation energies](@entry_id:190368) is the linear-response formulation. This approach calculates how the ground-state density responds linearly to a small, oscillating external potential. The true [excitation energies](@entry_id:190368), $\Omega$, of the interacting system appear as poles in the calculated frequency-dependent density [response function](@entry_id:138845).

This leads to a [matrix eigenvalue problem](@entry_id:142446) known as **Casida's equations**. For singlet excitations, the equation takes the form of a non-Hermitian [eigenvalue problem](@entry_id:143898):
$$
\begin{pmatrix} \mathbf{A}  \mathbf{B} \\ \mathbf{B}^*  \mathbf{A}^* \end{pmatrix} \begin{pmatrix} \mathbf{X} \\ \mathbf{Y} \end{pmatrix} = \Omega \begin{pmatrix} \mathbf{1}  \mathbf{0} \\ \mathbf{0}  -\mathbf{1} \end{pmatrix} \begin{pmatrix} \mathbf{X} \\ \mathbf{Y} \end{pmatrix}
$$
The matrices $\mathbf{A}$ and $\mathbf{B}$ are indexed by electron-hole pairs, typically formed from occupied ($i, j$) and unoccupied ($a, b$) Kohn-Sham orbitals. Their elements are given by:
$$
A_{ia,jb} = \delta_{ij}\delta_{ab}(\varepsilon_a - \varepsilon_i) + K_{ia,jb}
$$
$$
B_{ia,jb} = K_{ia,jb}
$$
Here, $\varepsilon_a - \varepsilon_i$ are the Kohn-Sham [orbital energy](@entry_id:158481) differences. The crucial term is the coupling kernel, $K_{ia,jb}$, which incorporates the electron-hole interaction through the Hartree and exchange-correlation (xc) kernels: $K = v_H + f_{xc}$. The matrix $\mathbf{A}$ describes the promotion of an electron from state $i$ to $a$ (a particle-hole excitation), while the matrix $\mathbf{B}$ describes the creation of a pair from the vacuum, coupling excitations to de-excitations.

The full solution to this problem can be found by transforming it into a standard [symmetric eigenvalue problem](@entry_id:755714) for $\Omega^2$:
$$
(\mathbf{A}-\mathbf{B})^{1/2}(\mathbf{A}+\mathbf{B})(\mathbf{A}-\mathbf{B})^{1/2} \mathbf{Z} = \Omega^2 \mathbf{Z}
$$
This approach is often referred to as the Random Phase Approximation (RPA) within TDDFT. A common simplification is the **Tamm-Dancoff Approximation (TDA)**, which neglects the coupling to de-excitations by setting $\mathbf{B} = \mathbf{0}$. This reduces the problem to a standard Hermitian [eigenvalue problem](@entry_id:143898) for the matrix $\mathbf{A}$ alone: $\mathbf{A}\mathbf{X} = \Omega^{\mathrm{TDA}}\mathbf{X}$. The TDA is computationally cheaper and often yields results very close to the full solution, especially for localized, high-energy excitations. However, the TDA can fail significantly for certain systems, particularly for low-energy [charge-transfer excitations](@entry_id:174772) or when collective plasmonic effects are important, as the $\mathbf{B}$ matrix can become large and even lead to instabilities (imaginary frequencies) in the full solution.

For a simple system with uncoupled transitions, the matrices $\mathbf{A}$ and $\mathbf{B}$ are diagonal. The [eigenvalue problem](@entry_id:143898) for $\Omega^2$ becomes trivial, with solutions for each transition $q$:
$$
\Omega_q^2 = (\Delta\varepsilon_q)(\Delta\varepsilon_q + 2K_{qq})
$$
If a transition has a KS energy difference $\Delta\varepsilon_1 = 2.50\,\mathrm{eV}$ and a diagonal kernel element $K_{11} = 0.30\,\mathrm{eV}$, its corrected excitation energy under the full Casida formalism is $\Omega_1 = \sqrt{2.50 \times (2.50 + 2 \times 0.30)} \approx 2.784\,\mathrm{eV}$. This demonstrates how the electron-hole interaction kernel corrects the bare KS transition energies.

### Neutral Excitations II: The Bethe-Salpeter Equation

While TDDFT is a powerful tool, it can struggle to accurately describe [excitons](@entry_id:147299) with large binding energies, especially in solid-state systems. A more rigorous and generally more accurate approach for neutral excitations is to solve the **Bethe-Salpeter Equation (BSE)**, which is rooted in many-body Green's [function theory](@entry_id:195067).

The BSE can be formulated as an effective two-body eigenvalue problem for the [electron-hole pair](@entry_id:142506), resembling a Schrödinger equation for the exciton wavefunction:
$$
(E_c^{\mathrm{QP}} - E_v^{\mathrm{QP}})\mathbf{A}_{vc} + \sum_{v'c'} \langle vc | K^{eh} | v'c' \rangle \mathbf{A}_{v'c'} = \Omega \mathbf{A}_{vc}
$$
Here, $\mathbf{A}_{vc}$ are the coefficients of the [exciton](@entry_id:145621) wavefunction in a basis of electron-hole pairs $|v \to c\rangle$. The diagonal part consists of the quasiparticle transition energies, $E_c^{\mathrm{QP}} - E_v^{\mathrm{QP}}$, which should be obtained from a preceding GW calculation. This is a crucial difference from TDDFT, which starts from KS energies.

The BSE interaction kernel, $K^{eh}$, consists of two terms:
$$
K^{eh} = 2K_x - K_d^{\mathrm{screened}}
$$
-   $K_x$ is the **repulsive bare exchange** interaction between the electron and hole. This term is responsible for the splitting between singlet and triplet excitons.
-   $K_d^{\mathrm{screened}}$ is the **attractive screened direct** interaction, which describes the statically screened Coulomb attraction between the electron and hole, $K_d^{\mathrm{screened}} = \langle vc | W(\omega=0) | vc \rangle$. It is this term that binds the electron and hole together to form an exciton.

The screening of the Coulomb interaction is a critical element. In practice, the dynamically [screened interaction](@entry_id:136395) $W(\omega)$ from the GW calculation is approximated by its [static limit](@entry_id:262480) $W(\omega=0) = \varepsilon_0^{-1} v$, where $\varepsilon_0$ is the static [dielectric constant](@entry_id:146714). However, for a more accurate description, particularly when the exciton energy $\Omega$ is near other electronic resonances (like [plasmons](@entry_id:146184)) in the material, one must account for the frequency dependence of screening. This leads to a self-consistent BSE problem, where the [exciton](@entry_id:145621) energy $\Omega$ itself determines the screening in the kernel, $W(\Omega)$. One would solve the [eigenvalue problem](@entry_id:143898) iteratively: guess an energy $\Omega_k$, compute the kernel with $W(\Omega_k)$, find the lowest eigenvalue $\Omega_{k+1}$, and repeat until convergence, $\Omega_{k+1} = \Omega_k$. This [dynamic screening](@entry_id:267421) correctly captures the coupling between [excitons](@entry_id:147299) and other collective [electronic excitations](@entry_id:190531).

### From Excitons to Spectra: Observables and Corrections

Solving the BSE or Casida's equations provides a set of [excitation energies](@entry_id:190368) $\Omega_k$ and corresponding eigenvectors ([exciton](@entry_id:145621) wavefunctions) $\mathbf{A}_k$. To connect these theoretical quantities to an experimental absorption spectrum, several additional steps are required.

#### Oscillator Strength and Selection Rules

The intensity of an optical transition to an excitonic state $|X_k\rangle$ is determined by its **[oscillator strength](@entry_id:147221)**, $f_k$. This quantity is proportional to the square of the transition dipole moment, $\mathbf{M}_k = \langle X_k | e\mathbf{r} | 0 \rangle$, where $|0\rangle$ is the ground state and $e\mathbf{r}$ is the electric dipole operator. For a linearly polarized light field with polarization vector $\mathbf{e}$, the absorption intensity is proportional to $|\mathbf{e} \cdot \mathbf{M}_k|^2$.

The transition dipole moment $\mathbf{M}_k$ is computed using the exciton eigenvector $\mathbf{A}_k$ and the transition dipole moments of the underlying single-particle transitions, $\mathbf{d}_{vc} = \langle \phi_c | e\mathbf{r} | \phi_v \rangle$:
$$
\mathbf{M}_k = \sum_{vc} \mathbf{A}_{k,vc}^* \mathbf{d}_{vc}
$$
A fundamental principle of quantum mechanics, often expressed via the Heisenberg [equation of motion](@entry_id:264286), establishes a direct relationship between the [position operator](@entry_id:151496) $\hat{x}$ and the momentum operator $\hat{p}$ through the system's Hamiltonian $\hat{H}$: $[\hat{H}, \hat{x}] = -i\hbar\hat{p}/m$. This identity guarantees that oscillator strengths calculated using the "length gauge" (based on $\langle f | \hat{x} | i \rangle$) and the "velocity gauge" (based on $\langle f | \hat{p} | i \rangle$) are equivalent for an exact calculation. Numerical approximations, however, can violate this identity and break the [gauge invariance](@entry_id:137857), providing a useful diagnostic for the quality of a calculation.

Whether a transition is optically active ($f_k > 0$, a **bright exciton**) or forbidden ($f_k = 0$, a **dark [exciton](@entry_id:145621)**) is governed by **[selection rules](@entry_id:140784)**, which can be rigorously derived from group theory. A transition from the ground state (which is almost always totally symmetric, e.g., transforming as the $A_{1g}$ irreducible representation) to an excited state is dipole-allowed only if the excited state's [irreducible representation](@entry_id:142733) matches that of one of the components of the dipole operator $(x, y, z)$. For a centrosymmetric system (like one with $D_{4h}$ symmetry), the ground state has even (gerade, $g$) parity. The dipole operator has odd (ungerade, $u$) parity. Therefore, only transitions to [ungerade](@entry_id:147965) [excited states](@entry_id:273472) (e.g., $A_{2u}, E_u$) can be dipole-allowed. This [parity selection rule](@entry_id:155458) is a powerful tool for interpreting spectra.

#### Spectral Lineshapes and Broadening

The raw theoretical results are a series of discrete [excitation energies](@entry_id:190368) ("stick spectra"). In reality, these transitions are broadened into peaks with a finite width. This broadening arises from the finite lifetime of the excited state. The time-domain picture provides an intuitive link: if the coherence of an excited state decays exponentially with a [dephasing time](@entry_id:198745) $T_2$, its dipole correlation function behaves as $C(t) \propto \exp(-t/T_2)\cos(\Omega t)$. The Fourier transform of this decaying oscillation is a **Lorentzian function**:
$$
A(\omega) \propto \frac{\gamma}{(\omega - \Omega)^2 + \gamma^2}
$$
where $\Omega$ is the [resonance frequency](@entry_id:267512) and the linewidth (half-width at half-maximum) $\gamma$ is the dephasing rate, $\gamma = 1/T_2$. The peak height of this normalized lineshape is inversely proportional to the [linewidth](@entry_id:199028), $A(\Omega) \propto T_2$. This process of replacing each theoretical stick with a Lorentzian or Gaussian peak is how theoretical spectra are generated for comparison with experiment.

#### Advanced Corrections: Local Fields and Spin-Orbit Coupling

In an inhomogeneous material, the electric field experienced by an electron (the [local field](@entry_id:146504)) can be very different from the macroscopic external field. This is because the charge density fluctuations induced by the external field create their own microscopic fields. These **Local Field Effects (LFE)** are particularly important in [molecular solids](@entry_id:145019), [nanostructures](@entry_id:148157), and surfaces. They are naturally included in the BSE and TDDFT linear response formalisms through the off-diagonal elements ($G \neq G'$) of the [dielectric matrix](@entry_id:144203) $\epsilon_{GG'}(\omega)$ or the xc-kernel $f_{xc}(\mathbf{r}, \mathbf{r}', \omega)$. Neglecting LFE amounts to setting these off-diagonal elements to zero, which is equivalent to approximating the macroscopic [dielectric function](@entry_id:136859) as $\epsilon_M(\omega) \approx \epsilon_{00}(\omega)$. The correct approach requires a full [matrix inversion](@entry_id:636005), $\epsilon_M(\omega) = 1/\epsilon^{-1}_{00}(\omega)$, which mixes in the effects of all $G \neq 0$ components and can significantly shift peak positions and redistribute [oscillator strength](@entry_id:147221) in the spectrum.

Finally, for materials containing heavy elements, **Spin-Orbit Coupling (SOC)** can become important. SOC is a relativistic effect that couples an electron's spin to its orbital motion. In the context of excitations, SOC can mix states of different [spin multiplicity](@entry_id:263865). For example, it can couple a bright singlet [exciton](@entry_id:145621) ($S=0$) to a nearby dark triplet [exciton](@entry_id:145621) ($S=1$). This mixing can lend some oscillator strength to the triplet, making it "partially bright," and also modifies the energy splitting between the states. The SOC-mixed splitting between a singlet at energy $E_S$ and a triplet at $E_T$ with a coupling strength $\lambda$ is given by $\Delta_{\mathrm{ST}}^{\mathrm{SOC}} = \sqrt{(E_S - E_T)^2 + 4\lambda^2}$.

#### Validating Spectra with Sum Rules

A powerful check on the accuracy and completeness of a calculated [absorption spectrum](@entry_id:144611) is provided by **sum rules**. These are integral relations that the spectrum must satisfy, derived from fundamental principles like causality and [charge conservation](@entry_id:151839). The most famous is the longitudinal **[f-sum rule](@entry_id:147775)**, or Thomas-Reiche-Kuhn sum rule, which relates the integrated [optical conductivity](@entry_id:139437) $\sigma_1(\omega)$ to the total electron density $n$:
$$
\int_0^\infty \sigma_1(\omega) d\omega = \frac{\pi n e^2}{2m}
$$
In numerical calculations, the right-hand side of this equation is known exactly from the system's electron count. The left-hand side is computed by integrating the calculated spectrum. Failure to satisfy this sum rule points to deficiencies in the calculation, such as an incomplete basis set, insufficient [k-point sampling](@entry_id:177715) of the Brillouin zone, or a frequency range that is too small to capture all the [spectral weight](@entry_id:144751). Verifying sum rules is therefore a critical step in producing reliable and predictive [computational spectroscopy](@entry_id:201457).