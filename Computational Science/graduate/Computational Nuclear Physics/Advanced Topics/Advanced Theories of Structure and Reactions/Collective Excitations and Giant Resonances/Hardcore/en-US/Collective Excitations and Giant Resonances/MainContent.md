## Introduction
Collective excitations, such as [giant resonances](@entry_id:159268), represent one of the most fascinating phenomena in [nuclear physics](@entry_id:136661). They reveal that an atomic nucleus, a complex system of strongly interacting protons and neutrons, can behave not just as a collection of individual particles, but as a coherent quantum fluid capable of large-scale, coordinated motion. Understanding how this collective behavior emerges from the underlying microscopic interactions is a central challenge in [nuclear many-body theory](@entry_id:752716). This article addresses this challenge by providing a comprehensive theoretical framework for describing collective excitations, from first principles to practical applications.

This article first builds the theoretical toolkit required to understand these phenomena, starting with the general framework of [linear response theory](@entry_id:140367), exploring the power of model-independent sum rules, and constructing a microscopic description using the Random Phase Approximation (RPA). We then demonstrate how these theories are applied, showing how [giant resonances](@entry_id:159268) serve as a unique laboratory to probe the shape of nuclei, constrain the [equation of state](@entry_id:141675) relevant for [neutron stars](@entry_id:139683), and test the limits of our microscopic models. Finally, hands-on practices provide opportunities to apply these concepts through guided computational problems, bridging the gap between theory and implementation.

## Principles and Mechanisms

Collective excitations, particularly [giant resonances](@entry_id:159268), represent a fundamental mode of response in atomic nuclei, where a significant fraction of nucleons move in a coherent manner. While the preceding chapter introduced the phenomenology of these states, this chapter delves into the theoretical principles and microscopic mechanisms that govern their existence, properties, and decay. We will build a theoretical framework from the ground up, starting with the general theory of [linear response](@entry_id:146180), exploring the power of model-independent sum rules, and then constructing a microscopic description using the Random Phase Approximation (RPA). Finally, we will address the crucial topic of damping, which gives [giant resonances](@entry_id:159268) their characteristic finite widths.

### Linear Response Theory and the Strength Function

The primary theoretical tool for studying the response of a quantum system to a weak external probe is **[linear response theory](@entry_id:140367)**. Imagine a nucleus in its ground state $|0\rangle$, described by a time-independent Hamiltonian $H_0$. At time $t=0$, we apply a weak, time-dependent external field that couples to the nucleus via a one-body operator $F$. The perturbation to the Hamiltonian is thus $H'(t) = -f(t)F$, where $f(t)$ is a scalar function representing the time-dependence of the external field.

The external field induces a change in the [expectation value](@entry_id:150961) of any observable. We are particularly interested in the induced change in the expectation value of the same operator $F$, denoted $\delta \langle F \rangle (t)$. In the linear regime, where the perturbation is sufficiently weak, this response is linearly proportional to the perturbing field. This relationship is formalized by the **retarded [response function](@entry_id:138845)**, $R(t-t')$, which connects the field at time $t'$ to the response at a later time $t$. Causality dictates that the response cannot precede the stimulus, so $R(t-t') = 0$ for $t \lt t'$. Using the Kubo formalism, the response function can be expressed in terms of the commutator of the operator $F$ in the Heisenberg picture:
$$
R(t) = -\frac{i}{\hbar} \Theta(t) \langle 0 | [F(t), F(0)] | 0 \rangle
$$
where $\Theta(t)$ is the Heaviside step function ensuring causality, and $F(t) = e^{iH_0 t/\hbar} F e^{-iH_0 t/\hbar}$ is the operator in the Heisenberg picture.

For experimental and theoretical analysis, it is more convenient to work in the frequency (or energy) domain. The frequency-domain [response function](@entry_id:138845), $R(\omega)$, is the Fourier transform of $R(t)$. To ensure convergence of the integral and enforce causality, we introduce an infinitesimal positive parameter $\eta$, which corresponds to giving the frequency $\omega$ a small positive imaginary part. The result is the fundamental expression for the retarded response function :
$$
R(\omega) = \int_{-\infty}^{\infty} e^{i\omega t} R(t) dt = -\frac{i}{\hbar} \int_{0}^{\infty} e^{i(\omega + i\eta)t} \langle 0 | [F(t), F(0)] | 0 \rangle dt
$$

The physical quantity of interest is the **[strength function](@entry_id:755507)**, $S_F(\omega)$, which describes how the transition strength associated with the operator $F$ is distributed as a function of excitation energy $E = \hbar\omega$. It is formally defined as:
$$
S_F(E) = \sum_{n \neq 0} |\langle n | F | 0 \rangle|^2 \delta(E - (E_n - E_0))
$$
where $|n\rangle$ are the excited states of $H_0$ with energies $E_n$. A crucial result, often considered a manifestation of the [fluctuation-dissipation theorem](@entry_id:137014), connects the [strength function](@entry_id:755507) directly to the imaginary part of the [response function](@entry_id:138845):
$$
S_F(\hbar\omega) = -\frac{1}{\pi} \mathrm{Im}[R(\omega)]
$$
This relationship is central: peaks in the [strength function](@entry_id:755507), which correspond to resonances, manifest as regions where the imaginary part of the response function is large. The [response function](@entry_id:138845) thus provides a complete and powerful framework for describing the [excitation spectrum](@entry_id:139562) of the nucleus.

### Sum Rules: Model-Independent Constraints

While calculating the full [strength function](@entry_id:755507) requires solving the complete [nuclear many-body problem](@entry_id:161400), significant physical insight can be gained from its energy-weighted moments, known as **sum rules**. The $k$-th moment of the strength distribution is defined as:
$$
m_k(F) = \int_{0}^{\infty} E^k S_F(E) dE = \sum_{n \neq 0} (E_n - E_0)^k |\langle n | F | 0 \rangle|^2
$$

Among the most important is the **energy-weighted sum rule (EWSR)**, $m_1$. A remarkable property of $m_1$ is that it can be calculated without knowing the [excited states](@entry_id:273472) $|n\rangle$. Through a short derivation involving the completeness of the eigenstates, $m_1$ can be expressed as the ground-state [expectation value](@entry_id:150961) of a double commutator  :
$$
m_1(F) = \frac{1}{2} \langle 0 | [F, [H, F]] | 0 \rangle
$$
This powerful result allows us to evaluate the total energy-weighted strength by simply calculating a commutator and a ground-state expectation value.

A classic application is the **Thomas-Reiche-Kuhn (TRK) sum rule** for the isovector [electric dipole](@entry_id:263258) operator. For a Hamiltonian containing only a standard kinetic energy term $T = \sum_i \mathbf{p}_i^2 / (2m)$ and a local, velocity-independent potential $V(\{\mathbf{r}_i\})$, the potential commutes with the dipole operator $F$ (which depends only on coordinates). The double commutator thus depends only on the kinetic term and the [canonical commutation relation](@entry_id:150454) $[r_j, p_k] = i\hbar\delta_{jk}$. The calculation yields a model-independent result that depends only on the number of protons ($Z$) and neutrons ($N$) :
$$
m_1(\text{dipole}) = \frac{\hbar^2 e^2}{2m} \frac{NZ}{A}
$$
This classical sum rule provides a benchmark for the total integrated strength of the Giant Dipole Resonance (GDR).

However, realistic nuclear interactions are more complex. They contain momentum-dependent (non-local) and tensor components. These terms do not commute with the dipole operator, and their presence modifies the double commutator, leading to an "enhancement" of the EWSR. For a local Energy Density Functional (EDF), these modifications can be parameterized. For instance, a momentum-dependent mean field can be approximated by introducing an **effective mass** $m^*$. If the kinetic energy term in the Hamiltonian is effectively replaced by $T = \sum_i \mathbf{p}_i^2 / (2m^*)$, the TRK sum rule is enhanced by a factor of $m/m^*$ . More generally, contributions from central velocity-dependent and tensor forces can be included, leading to a total enhancement factor $\kappa$ :
$$
m_1 = m_1^{\mathrm{TRK}} (1 + \kappa)
$$
The value of $\kappa$, which can be measured experimentally, provides a crucial constraint on the nature of the nuclear interaction.

Other moments are also highly valuable. The inverse-energy-weighted sum rule, $m_{-1}$, is related to the static polarizability of the nucleus. The ratio of moments can be used to estimate the average energy of a collective state. For the isoscalar monopole resonance (the "[breathing mode](@entry_id:158261)"), the collective energy $E_c$ can be precisely determined in a [harmonic oscillator model](@entry_id:178080) by $E_c = \sqrt{m_1/m_{-1}}$. This analysis yields the elegant result that the [breathing mode](@entry_id:158261) occurs at exactly twice the oscillator frequency, $E_c = 2\hbar\omega$, perfectly illustrating its collective nature .

### The Random Phase Approximation (RPA)

To obtain a microscopic description of the [strength function](@entry_id:755507), we need a theory that can predict the energies $E_n$ and transition strengths $|\langle n | F | 0 \rangle|^2$. The **Random Phase Approximation (RPA)** is the workhorse for this task. RPA can be derived as the small-amplitude limit of the Time-Dependent Hartree-Fock (TDHF) equations, and it describes nuclear excited states as coherent superpositions of one-particle–one-hole (1p1h) configurations relative to the mean-field ground state.

The core of RPA is the following generalized eigenvalue problem  :
$$
\begin{pmatrix} A  B \\ -B^*  -A^* \end{pmatrix} \begin{pmatrix} X^{(\nu)} \\ Y^{(\nu)} \end{pmatrix} = \Omega_\nu \begin{pmatrix} X^{(\nu)} \\ Y^{(\nu)} \end{pmatrix}
$$
Here, $\Omega_\nu$ is the excitation energy of the $\nu$-th RPA state. $X^{(\nu)}$ and $Y^{(\nu)}$ are vectors containing the forward-going and backward-going amplitudes, respectively, which describe the probability of creating or annihilating a 1p1h pair in the excited state. The matrices $A$ and $B$ are defined in the space of 1p1h configurations.
*   The matrix $A$ contains the unperturbed 1p1h energies $(\epsilon_p - \epsilon_h)$ on its diagonal and the particle-hole [matrix elements](@entry_id:186505) of the [residual interaction](@entry_id:159129) on its off-diagonal.
*   The matrix $B$ contains the matrix elements of the [residual interaction](@entry_id:159129) that create or annihilate two 1p1h pairs, coupling the ground state to 2p2h configurations.

The [residual interaction](@entry_id:159129), contained in $A$ and $B$, is responsible for **collectivity**. To understand this, consider a schematic model with two degenerate 1p1h states with energy $\epsilon_0$. In the absence of an interaction, there are two [excited states](@entry_id:273472) at energy $\epsilon_0$. When the [residual interaction](@entry_id:159129) is turned on, the RPA equations show that these states mix. One resulting state is a coherent, symmetric superposition whose energy is significantly shifted from $\epsilon_0$ and which carries most of the transition strength. The other, antisymmetric state is largely unaffected in energy and carries little strength . This is the essence of a collective state: the [residual interaction](@entry_id:159129) causes many 1p1h configurations to contribute constructively, creating a state with enhanced transition strength and a shifted energy.

The RPA formalism connects directly back to [linear response theory](@entry_id:140367). The [spectral representation](@entry_id:153219) of the response function, derived by inserting the complete set of RPA states into the commutator, takes the form :
$$
R(\omega) = \sum_{\nu} \left( \frac{|\langle 0 | F | \nu \rangle|^2}{\omega - \Omega_\nu + i\eta} - \frac{|\langle 0 | F | \nu \rangle|^2}{\omega + \Omega_\nu + i\eta} \right)
$$
where $|\langle 0 | F | \nu \rangle|^2$ is the transition strength to the RPA state $|\nu\rangle$. This expression transparently shows that the RPA [excitation energies](@entry_id:190368) $\Omega_\nu$ appear as poles in the response function. A collective state with a large transition strength produces a pole with a large residue, leading to a strong peak in the [strength function](@entry_id:755507) $S_F(\omega)$.

### Self-Consistency and Spurious Modes

A critical technical aspect of RPA calculations is **self-consistency**. If the underlying Hartree-Fock mean field is derived from a Hamiltonian $H$, the RPA calculation is fully self-consistent only if the [residual interaction](@entry_id:159129) used in the $A$ and $B$ matrices is the same second derivative of the energy functional that defines the mean field.

Failure to ensure [self-consistency](@entry_id:160889) leads to the appearance of **spurious modes**. These are [unphysical states](@entry_id:153570) that mix with the true physical excitations. For example, the total [momentum operator](@entry_id:151743) $\mathbf{P}$ is the generator of translations. Since any realistic nuclear Hamiltonian is translationally invariant, $[\mathbf{P}, H] = 0$. In a self-consistent RPA calculation, this symmetry ensures that the collective state corresponding to the [center-of-mass motion](@entry_id:747201) (a spurious excitation of the nucleus as a whole) appears at exactly zero excitation energy, where it is harmlessly decoupled from the physical spectrum of internal excitations. If [self-consistency](@entry_id:160889) is broken—for instance, by using a truncated 1p1h space or an inconsistent [residual interaction](@entry_id:159129)—this spurious mode is shifted to a non-zero energy and can contaminate the calculated physical spectrum . Verifying that spurious modes appear at or near zero energy is a crucial diagnostic test for the quality and consistency of an RPA calculation.

### Damping Mechanisms and Resonance Widths

The RPA model described so far predicts a spectrum of discrete, sharp [excited states](@entry_id:273472). However, experimentally observed [giant resonances](@entry_id:159268) are not sharp lines but broad structures with widths of several MeV. This broadening, or **damping**, arises from decay mechanisms that are not included in the standard RPA framework. The simple 1p1h collective state predicted by RPA is not a true eigenstate of the full Hamiltonian; it is a **doorway state** that can decay into more complex configurations. The total width $\Gamma$ of a [giant resonance](@entry_id:749900) is the sum of partial widths corresponding to different decay channels.

Two primary damping mechanisms contribute to the total width  :

1.  **Escape Width ($\Gamma^\uparrow$) or Landau Damping**: This is a one-body damping mechanism where a nucleon in the collective state is directly emitted into the continuum. This process is also known as **Landau damping**, representing the decay of the coherent collective mode into incoherent 1p1h states where the particle is unbound. This mechanism can be included in extensions of RPA such as Continuum-RPA. The escape width is zero below the particle emission threshold and generally increases with energy above it.

2.  **Spreading Width ($\Gamma^\downarrow$) or Collisional Damping**: This is a two-body (or higher-order) process where the initial 1p1h doorway state dissolves into more complex configurations, such as 2p2h, 3p3h, and so on. This mixing is driven by the parts of the [nucleon-nucleon interaction](@entry_id:162177) that go beyond the [mean-field approximation](@entry_id:144121). This process is also referred to as **[collisional damping](@entry_id:202128)**, as it can be thought of as arising from collisions between nucleons that are not captured by the smooth mean field. The density of available 2p2h states increases rapidly with excitation energy, causing the spreading width to be a strong function of energy.

The total width $\Gamma(E)$ is the energy-dependent sum of these contributions (and other smaller ones, like [radiative decay](@entry_id:159878) $\Gamma_\gamma$). The [strength function](@entry_id:755507) is no longer a series of delta peaks but is described by a distribution, such as a Breit-Wigner-like form with an energy-dependent width :
$$
S(E) \propto \frac{\Gamma(E)}{(E - E_0)^2 + [\Gamma(E)/2]^2}
$$
where $E_0$ is the bare energy of the doorway state. The energy dependence of $\Gamma(E)$ explains the often-asymmetric shapes of [giant resonances](@entry_id:159268).

From a more formal perspective, damping is encoded in the complex **[self-energy](@entry_id:145608)**, $\Sigma(\omega)$, of the collective state's propagator. The total width is given by the imaginary part of the on-shell [self-energy](@entry_id:145608), $\Gamma = -2 \, \mathrm{Im}[\Sigma(E_0)]$. Within this picture, Landau damping arises from the coupling of the collective mode to the continuum of 1p1h states, while [collisional damping](@entry_id:202128) can be modeled phenomenologically via a [relaxation-time approximation](@entry_id:138429), introducing a finite lifetime for quasiparticles due to two-body collisions . Decomposing the total observed width of a [giant resonance](@entry_id:749900) into these microscopic contributions is a key goal of modern [nuclear theory](@entry_id:752748), as it provides deep insights into the dynamics of [nuclear structure](@entry_id:161466) and the nature of the nuclear force.