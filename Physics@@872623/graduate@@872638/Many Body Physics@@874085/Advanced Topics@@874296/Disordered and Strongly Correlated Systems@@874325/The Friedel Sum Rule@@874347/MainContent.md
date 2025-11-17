## Introduction
How does a sea of electrons respond to the introduction of a single impurity? The answer is not just a local shuffle but a global rearrangement governed by a profound principle: the Friedel sum rule. This exact, non-perturbative result forms a cornerstone of condensed matter physics, establishing a direct link between the microscopic quantum [scattering phase shifts](@entry_id:138129) and the macroscopic electronic charge displaced to screen the impurity. It addresses the fundamental problem of impurity screening by providing a powerful counting tool that remains valid even in complex, strongly interacting scenarios. This article provides a comprehensive exploration of this pivotal rule. The first chapter, "Principles and Mechanisms," will lay the groundwork, deriving the rule from fundamental state-counting arguments and exploring its connection to [scattering theory](@entry_id:143476) and Levinson's theorem. The second chapter, "Applications and Interdisciplinary Connections," will showcase the rule's immense utility, demonstrating how it provides crucial insights into [quantum transport](@entry_id:138932), the Kondo effect, spectroscopic signatures, and impurity physics in novel materials. Finally, the "Hands-On Practices" section will allow you to apply these concepts to concrete problems in metals, superconductors, and topological systems.

## Principles and Mechanisms

The introduction of a localized impurity into an otherwise homogeneous sea of electrons fundamentally alters the electronic structure of the host material. The electrons, being mobile charges, redistribute themselves to screen the potential of the impurity. This screening phenomenon is not merely a local rearrangement but a global one, governed by a profound and exact result known as the **Friedel sum rule**. This rule establishes a direct connection between a microscopic quantity—the quantum mechanical [scattering phase shifts](@entry_id:138129) an electron acquires when interacting with the impurity—and a macroscopic quantity: the total electronic charge displaced by the impurity. This chapter elucidates the principles and mechanisms underlying this rule, from its intuitive physical origins to its formal derivations and broad generalizations in many-body physics.

### Charge Displacement and the Density of States

At its core, the Friedel sum rule is a statement about state counting. When an impurity potential $V(\mathbf{r})$ is introduced into a system of non-interacting electrons at zero temperature, the [single-particle energy](@entry_id:160812) levels of the Hamiltonian are shifted. Some states are pushed up in energy, others are pushed down, and new bound states may be formed below the original continuum of energies. The **total displaced charge**, often denoted $Z$ or $\Delta N$ (in units of the [elementary charge](@entry_id:272261) $e$), is the total number of electrons that accumulate or are depleted in the vicinity of the impurity. At zero temperature, where all states up to the Fermi energy $E_F$ are occupied, this is equivalent to the net change in the number of states with energy less than or equal to $E_F$.

This change in the total number of states can be expressed as an integral of the change in the **[density of states](@entry_id:147894) (DOS)**, $\Delta\rho(E)$, induced by the impurity:
$$
\Delta N = \int_0^{E_F} \Delta\rho(E) \, dE
$$
The quantity $\Delta\rho(E)$ represents the difference between the density of states in the system with the impurity and that of the [free electron gas](@entry_id:145649). A central result from scattering theory, known as the Krein-Friedel-Lloyd formula, relates this change in the DOS directly to the [energy derivative](@entry_id:268961) of the [scattering phase shifts](@entry_id:138129). For a spherically [symmetric potential](@entry_id:148561) in three dimensions, the scattering process can be decomposed into independent **partial waves**, each labeled by an [angular momentum quantum number](@entry_id:172069) $l$. The change in the DOS is the sum of contributions from each channel, weighted by its degeneracy ($g_s$ for spin and $2l+1$ for orbital angular momentum):
$$
\Delta\rho(E) = \frac{g_s}{\pi} \sum_{l=0}^{\infty} (2l+1) \frac{d\delta_l(E)}{dE}
$$
Here, $\delta_l(E)$ is the [scattering phase shift](@entry_id:146584) for the $l$-th partial wave at energy $E$.

Substituting this into the integral for $\Delta N$ and performing the integration, we obtain a preliminary version of the sum rule:
$$
\Delta N = \int_0^{E_F} \left( \frac{g_s}{\pi} \sum_{l=0}^{\infty} (2l+1) \frac{d\delta_l(E)}{dE} \right) dE = \frac{g_s}{\pi} \sum_{l=0}^{\infty} (2l+1) \left[ \delta_l(E_F) - \delta_l(0) \right]
$$
This expression forms the basis of the Friedel sum rule. It demonstrates that the total accumulated charge is determined not by the [phase shifts](@entry_id:136717) themselves, but by their change from the bottom of the band ($E=0$) to the Fermi level ($E=E_F$). The physical interpretation of this result and the significance of the term $\delta_l(0)$ will be explored in subsequent sections.

### A Physical Picture: How Phase Shifts Count States

The mathematical connection between displaced charge and [phase shifts](@entry_id:136717) can be understood through more intuitive physical arguments.

#### The One-Dimensional Case: A WKB Perspective

Consider a simple one-dimensional [system of particles](@entry_id:176808) confined to a large box of length $L$. Within the semi-classical WKB approximation, the number of states $N(E)$ with energy up to $E$ is related to the classically allowed phase space. The introduction of a localized potential $V(x)$ modifies this count. The change in the integrated number of states, $\Delta N(E) = N(E) - N_0(E)$, can be calculated directly. Using the WKB formulas for the integrated density of states and the [scattering phase shift](@entry_id:146584), one finds a remarkably simple and exact relationship in one dimension:
$$
\Delta N(E) = \frac{\delta(E)}{\pi}
$$
Here, we have considered a single [scattering channel](@entry_id:152994) (e.g., the even-parity channel for a [symmetric potential](@entry_id:148561)). This result, the 1D Friedel sum rule, provides a clear picture: for every $\pi$ of phase shift induced by the scatterer at a given energy, exactly one state has been added to (or removed from) the system below that energy.

#### The Three-Dimensional Case: Particle in a Spherical Box

This physical picture extends to three dimensions. Imagine the [electron gas](@entry_id:140692) is confined within a large, impenetrable sphere of radius $R$. In the absence of an impurity, the [radial wavefunctions](@entry_id:266233) must vanish at the boundary, leading to a quantization condition on the allowed wavevectors $k$. For the $l$-th partial wave, this condition is approximately $kR - l\pi/2 = n\pi$, where $n$ is an integer.

When a short-range, spherically symmetric impurity is placed at the center, the [radial wavefunction](@entry_id:151047) outside the potential range acquires a phase shift $\delta_l(k)$. The asymptotic form becomes proportional to $\sin(kr - l\pi/2 + \delta_l(k))$. The boundary condition at $R$ now quantizes the wavevectors according to a modified rule: $kR - l\pi/2 + \delta_l(k) = n\pi$.

For a fixed integer $n$, the change in the allowed wavevector is $\Delta k \approx -\delta_l(k)/R$. A positive phase shift "pushes" the allowed $k$ values to be smaller, effectively squeezing more states into a given energy interval. By counting the number of states up to the Fermi wavevector $k_F$, one can find the total number of states added by the impurity. Summing over all partial waves $l$ and including the spin and orbital degeneracies, this argument precisely reproduces the Friedel sum rule. This demonstrates how phase shifts act as a bookkeeping device for the number of states added or removed from the spectrum.

### The Friedel Sum Rule: Formal Statement and Assumptions

For a gas of spin-$1/2$ electrons ($g_s=2$) at zero temperature scattering elastically off a static, spherically symmetric impurity, the Friedel sum rule states that the total displaced charge $Z$ is given by:
$$
Z = \frac{2}{\pi} \sum_{l=0}^{\infty} (2l+1) \delta_l(E_F)
$$
This celebrated formula is an exact, non-perturbative result. However, its validity rests on a set of crucial assumptions that define the physical context:

1.  **Zero Temperature ($T=0$):** The derivation relies on a sharply defined Fermi energy, below which all states are occupied and above which all are empty. At finite temperatures, the Fermi-Dirac distribution smears this cutoff, and the sum rule holds only approximately.

2.  **Static, Elastic Scattering:** The impurity potential is assumed to be time-independent, and the scattering process must be elastic (energy-conserving). This allows for the definition of energy-dependent [phase shifts](@entry_id:136717).

3.  **Adiabatic Switching:** Conceptually, the sum rule is derived by imagining that the impurity potential is switched on infinitely slowly. This ensures a [one-to-one correspondence](@entry_id:143935) between the states of the free system and the interacting system, allowing for a meaningful counting of displaced states. Any [bound states](@entry_id:136502) that form are considered to be "pulled down" from the continuum.

4.  **Short-Range Potential:** The standard [partial wave analysis](@entry_id:136738) requires a potential that falls off sufficiently fast at large distances (faster than $1/r^2$). This is naturally satisfied in metals, where the long-range Coulomb potential of an impurity is screened by the [electron gas](@entry_id:140692) itself.

5.  **Spherical Symmetry:** The decomposition into partial waves labeled by $l$ with degeneracy $(2l+1)$ is a direct consequence of [rotational invariance](@entry_id:137644). For anisotropic impurities, this specific form must be modified.

### Bound States and Levinson's Theorem

The formula $Z = \frac{2}{\pi}\sum(2l+1)\delta_l(E_F)$ contains a remarkable subtlety related to the phase shift at zero energy, $\delta_l(0)$. As derived earlier, the integrated change in the continuum density of states is $\frac{2}{\pi}\sum(2l+1)[\delta_l(E_F)-\delta_l(0)]$. The total displaced charge must also include any bound states formed by the potential, $N_B$.

The connection is provided by **Levinson's theorem**, which states that for a short-range potential in three dimensions, the zero-energy phase shift is related to the number of bound states, $n_b(l)$, in that partial wave channel:
$$
\delta_l(0) = n_b(l) \pi
$$
Each bound state contributes exactly $\pi$ to the phase shift at the bottom of the band. The total number of electrons in [bound states](@entry_id:136502) is $N_B = \sum_l (2l+1) n_b(l)$ (for spinless fermions).

The total displaced charge is the sum of electrons in newly formed [bound states](@entry_id:136502) and the change in the number of electrons in scattering (continuum) states:
$$
Z = N_B + \int_0^{E_F} \Delta \rho(E) dE = \sum_l (2l+1) n_b(l) + \frac{1}{\pi} \sum_l (2l+1)[\delta_l(E_F) - \delta_l(0)]
$$
(Here we use the spinless case for simplicity). Substituting Levinson's theorem, $\delta_l(0) = n_b(l) \pi$:
$$
Z = \sum_l (2l+1) n_b(l) + \frac{1}{\pi} \sum_l (2l+1)[\delta_l(E_F) - n_b(l) \pi] = \frac{1}{\pi} \sum_{l=0}^{\infty} (2l+1) \delta_l(E_F)
$$
This demonstrates that the concise form of the Friedel sum rule is powerful because the phase shift at the Fermi energy, $\delta_l(E_F)$, automatically accounts for both the redistribution of [continuum states](@entry_id:197473) *and* the formation of bound states.

A failure to correctly account for the phase at the bottom of the energy band can lead to incorrect conclusions. For instance, in the Anderson impurity model, a naive application of the formula $Z = \frac{2}{\pi}\delta(E_F)$ can be misleading. The correct calculation involves integrating the change in DOS from the bottom of the band, properly accounting for the phase shift at $-\infty$, which reveals that the naive formula is only correct at resonance ($E_F = \epsilon_d$), where $\delta(E_F) = \pi/2$. Similarly, for an attractive [delta-function potential](@entry_id:189699) in a finite 1D box, a special tuning of parameters can place a [bound state](@entry_id:136872) exactly at zero energy, leading to a fractional contribution to the state count and a total displaced charge of $1/2$ in the high-energy limit.

### Applications and Illustrative Calculations

The Friedel sum rule is not just a theoretical curiosity; it is a practical tool for calculating the screening charge around impurities.

#### Weak and Strong Scattering

For a weak potential, the phase shifts can be calculated using the **first Born approximation**. For example, for a delta-shell potential $V(r) = \alpha \delta(r-a)$, the phase shifts are approximately $\delta_l(k_F) \approx - \frac{2m k_F \alpha a^2}{\hbar^2} [j_l(k_F a)]^2$. Substituting this into the sum rule and using the identity $\sum_{l=0}^{\infty}(2l+1)[j_l(x)]^2 = 1$, one finds the total displaced charge to be $\Delta N = - \frac{g_s m k_F \alpha a^2}{\pi \hbar^2}$.

The rule is, however, non-perturbative and works equally well for strong potentials. Consider an attractive spherical well potential $V(r)=-V_0$ for $r \le a$. Even if the potential is strong, if the energy is low ($k_F a \ll 1$), scattering is dominated by the s-wave ($l=0$) channel. By solving the Schrödinger equation for the [s-wave](@entry_id:754474) phase shift $\delta_0(k_F)$ and applying the simplified sum rule $Z \approx \frac{2}{\pi}\delta_0(k_F)$, one can calculate the displaced charge exactly, beyond any approximation in the potential strength.

#### Lattice Models

The Friedel sum rule is not restricted to [continuum models](@entry_id:190374). In a one-dimensional [tight-binding](@entry_id:142573) chain with a single on-site impurity $V_0 |0\rangle\langle 0|$, the accumulated charge is related to the phase shift via $\Delta N = -\frac{1}{\pi}\delta(E_F)$. (The sign convention can vary). The phase shift can be found from the impurity Green's function, $\delta(E) = \text{Arg}[1 - V_0 G_{00}(E)]$. By calculating the local Green's function $G_{00}(E)$, one can determine the accumulated charge for any band filling. For example, at half-filling ($E_F=0$), an accumulated charge of $\Delta N = 1/4$ is achieved for a specific attractive potential strength of $V_0/t = -2$.

### Advanced Perspectives and Generalizations

The Friedel sum rule's significance is amplified by its deep connections to other areas of [many-body theory](@entry_id:169452) and its applicability to complex interacting systems.

#### Connection to Screening and Linear Response

The sum rule can be understood as a statement of **[perfect screening](@entry_id:146940)**. If an impurity has a valence charge of $Ze$ relative to the host atoms, the electron gas must rearrange to accumulate a total charge of $-Ze$ (i.e., $\Delta N = Z$ electrons) to neutralize the impurity at large distances. This ensures that the impurity's influence is localized. This can be verified explicitly using [linear response theory](@entry_id:140367). For a [point charge](@entry_id:274116) impurity $Ze$, the total induced charge calculated using the Random Phase Approximation (RPA) dielectric function is found to be exactly $Z$ in the long-wavelength limit, in perfect agreement with the sum rule.

#### Connection to Green's Functions and Luttinger's Theorem

A more formal and powerful derivation of the sum rule uses the Green's function formalism. The change in the number of states can be expressed in terms of the determinant of the operator $1 - G_0 V$, where $G_0$ is the free Green's function. By relating this to the determinant of the [scattering matrix](@entry_id:137017) $S$, whose eigenvalues are given by the phase shifts ($S_l = \exp(2i\delta_l)$), the sum rule can be re-derived.

This perspective reveals the FSR as a special case of **Luttinger's theorem**. Luttinger's theorem states that for an interacting Fermi liquid, the volume of the Fermi surface is conserved, provided the particle number is held fixed. The Friedel sum rule can be viewed as applying this principle to a system where the particle number is allowed to change at a fixed chemical potential in the presence of a single impurity.

#### Generalizations to Complex Systems

The fundamental principle of state counting extends far beyond non-interacting fermions scattering from a simple potential.

*   **Magnetic Impurities:** For an impurity with a magnetic moment (spin), the scattering becomes spin-dependent. The scattering channels must be classified according to the total spin of the electron-impurity system. For an [s-wave scattering](@entry_id:155985) off a spin-1/2 impurity, the channels are singlet ($S_{tot}=0$) and triplet ($S_{tot}=1$). The Friedel sum rule applies to each channel separately, with [phase shifts](@entry_id:136717) $\delta_s$ and $\delta_t$. The total displaced charge for spin-up electrons, for instance, is a weighted average over these fundamental channels: $\Delta N_\uparrow = \frac{1}{2\pi}(\delta_s + 3\delta_t)$. This generalization is a cornerstone in the theory of the Kondo effect.

*   **Interacting Systems (Luttinger Liquids):** In one-dimensional interacting systems, known as Luttinger liquids, the concept still holds, albeit in a modified form. Using the technique of [bosonization](@entry_id:139728), the accumulated charge $\Delta Q$ around a weak [potential barrier](@entry_id:147595) can be related to the backscattering amplitude $V_{BS}$ and the Luttinger parameter $K$, which encodes the [interaction strength](@entry_id:192243): $\Delta Q = -e K V_{BS} / (\pi \hbar v)$. For non-interacting electrons, $K=1$, and this result connects to the 1D FSR.

*   **Fractional Quantum Hall Systems:** The principle even applies to the exotic [edge states](@entry_id:142513) of Fractional Quantum Hall (FQH) systems. These edges form a chiral Luttinger liquid where the [elementary excitations](@entry_id:140859) carry [fractional charge](@entry_id:142896). The total charge accumulated by a weak potential constriction is proportional to the FQH filling fraction $\nu$, a direct manifestation of the fractionalization of charge.

#### Dynamic vs. Static Response

It is critical to remember the assumption of adiabaticity. If an impurity potential is switched on *suddenly*, the system is thrown into a non-equilibrium state. The number of electrons that eventually become trapped in a [bound state](@entry_id:136872) of the potential is not given by the static sum rule. It is determined by the projection of the initial Fermi sea onto the final eigenstates. This dynamically determined trapped charge can be different from the total displaced charge predicted by the FSR, highlighting the distinction between the system's dynamic response and its final equilibrium (or steady-state) properties.

In summary, the Friedel sum rule provides a remarkably robust and versatile bridge between the microscopic world of quantum scattering and the macroscopic phenomenon of [charge screening](@entry_id:139450). Its principles, rooted in the fundamentals of quantum state counting, extend from simple metals to the frontiers of strongly correlated matter, cementing its status as a central concept in condensed matter physics.