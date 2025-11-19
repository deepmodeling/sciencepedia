## Introduction
Electronic excited states are at the heart of light-matter interactions, governing a vast range of phenomena from vision and photosynthesis to the optical properties of advanced materials. To understand and engineer these processes, we require a robust theoretical framework that can accurately predict the energies, properties, and dynamics of molecules and materials in the excited state. This article provides a comprehensive exploration of the modern computational methods designed for this purpose, addressing the gap between fundamental quantum mechanics and practical application. We will begin in the first chapter, "Principles and Mechanisms," by establishing the rigorous mathematical foundation of response theory and examining its implementation in cornerstone methods like Time-Dependent Density Functional Theory (TDDFT), correlated wavefunction theories, and the GW-BSE approach. The second chapter, "Applications and Interdisciplinary Connections," will showcase how these tools are used to interpret complex spectra, map [photochemical reaction](@entry_id:195254) pathways, and provide insight into systems from solvated molecules to solid-state [excitons](@entry_id:147299). Finally, "Hands-On Practices" will provide concrete exercises to reinforce the theoretical concepts and address common computational challenges. Our exploration begins with the fundamental principles and mechanisms that form the bedrock of excited-state quantum chemistry.

## Principles and Mechanisms

The theoretical and computational exploration of electronic excited states is a cornerstone of modern chemistry and physics, providing the fundamental language for describing spectroscopy, [photochemistry](@entry_id:140933), and a vast array of light-matter interactions. Building upon the introductory concepts, this chapter delves into the core principles and mechanisms that underpin contemporary [excited-state methods](@entry_id:190102). We will begin with the universal formalism of response theory, which provides a rigorous mathematical foundation for understanding how quantum systems react to external perturbations. We will then examine how this theory is realized in practical computational frameworks, most notably Time-Dependent Density Functional Theory (TDDFT), and explore a diverse landscape of methods designed to address specific challenges, from [strong electron correlation](@entry_id:183841) to the accurate prediction of solid-state optical properties. Finally, we will touch upon the numerical machinery required to implement these methods and the crucial link between electronic structure and nuclear dynamics.

### The Formalism of Response Theory

At its heart, the calculation of excited-state properties is a problem of **response theory**. We wish to understand how a system, initially in its ground state, responds to an external, time-dependent perturbation, such as the oscillating electric field of a light wave. This response is captured by mathematical objects known as [propagators](@entry_id:153170) or Green's functions.

#### Linear Response and the Polarization Propagator

For a weak perturbation, the system's response is linear. The central quantity describing this linear response is the **[polarization propagator](@entry_id:201288)**, also known as the retarded two-time Green's function. Let us consider two Hermitian operators, $\hat{A}$ and $\hat{B}$, which could represent, for example, components of the electric dipole moment operator. The retarded [polarization propagator](@entry_id:201288), denoted $\Pi_{AB}(\omega)$ or $\langle\langle \hat{A}; \hat{B} \rangle\rangle_{\omega}$, quantifies how a perturbation coupled to operator $\hat{B}$ at one time affects the expectation value of operator $\hat{A}$ at a later time.

Causality—the principle that an effect cannot precede its cause—is a paramount physical constraint. This is formally imposed in the time-domain definition of the [propagator](@entry_id:139558) through the Heaviside step function, $\theta(t)$. For a time-translationally invariant system, the [propagator](@entry_id:139558) depends only on the time difference $\tau = t-t'$ and is defined as:

$$
\Pi_{AB}^R(t) = -i \theta(t) \langle 0 \lvert [\hat{A}_H(t), \hat{B}_H(0)] \rvert 0 \rangle
$$

Here, $\lvert 0 \rangle$ is the exact ground state of the unperturbed Hamiltonian $\hat{H}$, and operators are expressed in the Heisenberg picture, e.g., $\hat{A}_H(t) = e^{i \hat{H} t} \hat{A} e^{-i \hat{H} t}$ (with $\hbar=1$). The commutator $[\hat{A}_H(t), \hat{B}_H(0)]$ measures the quantum mechanical influence of the perturbation.

Spectroscopy, however, operates in the frequency domain. The frequency-domain propagator is obtained via a Fourier transform. The presence of the Heaviside function restricts the integral to positive times and, to ensure convergence, an infinitesimal positive parameter $\eta$ is introduced. This leads to the integral representation:

$$
\Pi_{AB}(\omega) = -i \int_{0}^{\infty} dt \, e^{i \omega t} \, \langle 0 \lvert [\hat{A}_H(t), \hat{B}_H(0)] \rvert 0 \rangle
$$

where the transform is understood with a convergence factor $e^{-\eta t}$, which is equivalent to replacing $\omega$ with $\omega + i\eta$ in the exponential. The true power of this formalism is revealed through the **Lehmann representation**, which is derived by inserting a complete set of the exact eigenstates of the Hamiltonian, $\sum_n \lvert n \rangle \langle n \lvert = \mathbb{1}$, into the expression. After performing the Fourier transform, one arrives at a spectral decomposition of the [propagator](@entry_id:139558) [@problem_id:2890541]:

$$
\Pi_{AB}(\omega) = \sum_{n \ge 1} \left[ \frac{\langle 0 \lvert \hat{A} \rvert n \rangle \langle n \lvert \hat{B} \rvert 0 \rangle}{\omega - \omega_{n0} + i \eta} - \frac{\langle 0 \lvert \hat{B} \rvert n \rangle \langle n \lvert \hat{A} \rvert 0 \rangle}{\omega + \omega_{n0} + i \eta} \right]
$$

This remarkable equation forms a bridge between the abstract response function and concrete spectroscopic observables. It shows that the [polarization propagator](@entry_id:201288) has poles in the [complex frequency plane](@entry_id:190333) located at $\omega = \pm \omega_{n0} - i\eta$, where $\omega_{n0} = E_n - E_0$ are the exact transition energies from the ground state $\lvert 0 \rangle$ to the [excited states](@entry_id:273472) $\lvert n \rangle$. The residues at these poles are products of transition [matrix elements](@entry_id:186505), such as $\langle 0 \lvert \hat{A} \rvert n \rangle \langle n \lvert \hat{B} \rvert 0 \rangle$. For the polarizability, where $\hat{A}$ and $\hat{B}$ are dipole operators, the residues are directly related to the [transition probabilities](@entry_id:158294), or oscillator strengths. All poles of this retarded function lie in the lower half of the complex plane, a direct mathematical consequence of causality.

#### Nonlinear Response and Hyperpolarizability

When perturbations become stronger, the linear response approximation breaks down, and nonlinear effects become significant. These are described by higher-order response functions. The next term in the expansion is the **quadratic [response function](@entry_id:138845)**, $\langle\langle A; B, C \rangle\rangle_{\omega_b,\omega_c}$, which describes the response of observable $\hat{A}$ at a sum frequency $\omega_\sigma = \omega_b + \omega_c$ to perturbations coupled to operators $\hat{B}$ and $\hat{C}$ at frequencies $\omega_b$ and $\omega_c$, respectively.

A key physical manifestation of quadratic response is the **first [hyperpolarizability](@entry_id:202797)**, $\beta_{ijk}$, which governs phenomena like [second-harmonic generation](@entry_id:145639). This tensor relates the second-order induced polarization $P_i^{(2)}$ to the applied electric field components $E_j$ and $E_k$. The connection to the formal response theory is given by [@problem_id:2890575]:

$$
\beta_{ijk}(-\omega_\sigma; \omega_b, \omega_c) = - \langle\langle \mu_i; \mu_j, \mu_k \rangle\rangle_{\omega_b,\omega_c}
$$

where $\mu_i$ are components of the [electric dipole](@entry_id:263258) operator. Similar to [linear response](@entry_id:146180), the quadratic [response function](@entry_id:138845) possesses a fundamental symmetry: it is invariant under the simultaneous exchange of the perturbation-operator pairs, i.e., $\langle\langle A; B, C \rangle\rangle_{\omega_b,\omega_c} = \langle\langle A; C, B \rangle\rangle_{\omega_c,\omega_b}$ [@problem_id:2890575].

In the [static limit](@entry_id:262480) ($\omega_b = \omega_c = 0$), response functions can be related to derivatives of the ground-state energy with respect to static field strengths. While the linear polarizability $\alpha_{ij}$ is a second derivative of the energy, the static [hyperpolarizability](@entry_id:202797) $\beta_{ijk}$ is related to the third derivative. This also provides an alternative definition: $\beta_{ijk}$ can be viewed as the change in the linear polarizability $\alpha_{ij}$ with respect to a third static field $F_k$ [@problem_id:2890575]:

$$
\beta_{ijk}(0; 0, 0) = - \frac{\partial^3 E_0}{\partial F_i \partial F_j \partial F_k}\bigg|_{F=0} = \frac{\partial \alpha_{ij}}{\partial F_k}\bigg|_{F=0}
$$

### Realization in Time-Dependent Density Functional Theory

The exact Lehmann representation is a formal expression, as the exact many-body [eigenstates](@entry_id:149904) are unknown. Practical methods aim to approximate it. **Time-Dependent Density Functional Theory (TDDFT)** is arguably the most widely used framework for this purpose. It recasts the problem of the interacting many-electron system into one involving a fictitious non-interacting **Kohn-Sham (KS)** system that, by design, has the same time-dependent electron density as the real system.

#### The Adiabatic Approximation and its Consequences

The core of TDDFT lies in the **Dyson-like equation** that relates the interacting density-density [response function](@entry_id:138845) of the real system, $\chi(\omega)$, to that of the non-interacting KS system, $\chi_0(\omega)$:

$$
\chi(\omega) = \chi_0(\omega) + \chi_0(\omega) f_{Hxc}(\omega) \chi(\omega)
$$

The kernel $f_{Hxc}$ accounts for the [electron-electron interaction](@entry_id:189236), comprising the classical Coulomb (Hartree) part and the quantum mechanical exchange-correlation (XC) part, $f_{xc}$. In the most general case, the XC potential at a given time $t$ depends on the entire history of the density at times $t' \le t$. This "memory" is encoded in a frequency-dependent XC kernel, $f_{xc}(\omega)$.

However, the vast majority of TDDFT calculations employ the **[adiabatic approximation](@entry_id:143074)**. This assumes that the XC potential is local in time, depending only on the instantaneous density. This simplification has a profound consequence for the XC kernel [@problem_id:2890543]. The time-domain kernel becomes proportional to a Dirac delta function in time, $f_{xc}^{\text{adia}}(t, t') \propto \delta(t-t')$. Its Fourier transform is therefore independent of frequency, $\omega$. The adiabatic kernel is simply the second functional derivative of a ground-state XC [energy functional](@entry_id:170311), $E_{xc}$:

$$
f_{xc}^{\text{adia}, \sigma\sigma'}(\mathbf{r},\mathbf{r}') = \frac{\delta^2 E_{xc}[n_{\uparrow},n_{\downarrow}]}{\delta n_{\sigma}(\mathbf{r})\,\delta n_{\sigma'}(\mathbf{r}')}
$$

This loss of frequency dependence is the mathematical root of one of TDDFT's most famous limitations: the inability to describe states with significant **double-excitation character**. The non-interacting response function, $\chi_0(\omega)$, has poles only at KS single-particle (electron-hole) transition energies. The algebraic structure of the Dyson equation with a static (frequency-independent) kernel can only mix these single-excitation configurations. The resulting [excited states](@entry_id:273472) are "dressed" single excitations. States that are predominantly of double-excitation character (two electrons excited simultaneously) lie outside this single-particle-hole manifold and cannot be generated. A frequency-dependent kernel, $f_{xc}(\omega)$, is required to introduce the necessary "dynamical" coupling to these higher-order configurations and generate new poles in $\chi(\omega)$ at double-[excitation energies](@entry_id:190368) [@problem_id:2890587].

### A Survey of Modern Computational Methods

Beyond the foundational principles, a variety of distinct computational strategies have been developed to approximate the excited-state problem.

#### Real-Time Propagation in TDDFT

While the Dyson equation is typically solved in the frequency domain (leading to matrix [eigenvalue problems](@entry_id:142153) like Casida's equations), an alternative and powerful approach is to work directly in the time domain. In **Real-Time TDDFT (RT-TDDFT)**, one numerically propagates the Time-Dependent Kohn-Sham (TDKS) equations forward in time under the influence of an external field.

A particularly elegant technique for obtaining the full linear optical spectrum is the **delta-kick** method. At time $t=0$, the system is perturbed by an impulsive, broadband electric field, mathematically represented by a Dirac delta function, $E_j(t) = \kappa \delta(t)$, where $\kappa$ is a small kick strength. In the length gauge, this is implemented by instantaneously multiplying each occupied KS orbital by a phase factor $\exp(i\kappa r_j)$. The system then evolves field-free for $t>0$. The time-dependent [induced dipole moment](@entry_id:262417), $\Delta\mu_i(t)$, is recorded. According to the principles of [linear response](@entry_id:146180), the frequency-dependent [polarizability tensor](@entry_id:191938), $\alpha_{ij}(\omega)$, is simply proportional to the Fourier transform of this signal [@problem_id:2890571]:

$$
\alpha_{ij}(\omega) = \frac{1}{\kappa} \int_0^\infty \Delta\mu_i(t) e^{i\omega t} dt
$$

This powerful approach yields the entire [absorption spectrum](@entry_id:144611) from a single simulation. Because the underlying TDKS equations describe a causal time evolution, the resulting polarizability correctly obeys the **Kramers-Kronig relations** that connect its real and imaginary parts, a fundamental consequence of causality in any physical response function [@problem_id:2890571].

#### Wavefunction-Based Correlated Methods

While TDDFT is a workhorse, wavefunction-based theories offer a systematic path towards higher accuracy and a more controlled treatment of electron correlation.

The **Algebraic Diagrammatic Construction (ADC)** scheme is a family of methods derived directly from the [polarization propagator](@entry_id:201288) formalism. It provides a hierarchy of approximations (ADC(1), ADC(2), ADC(3), ...) that are size-consistent and yield a Hermitian eigenvalue problem in a truncated basis of excited configurations (e.g., single, double, ... [particle-hole excitations](@entry_id:137289)), known as the Intermediate State Representation (ISR). Because the effective Hamiltonian is Hermitian, the resulting oscillator strengths are guaranteed to be non-negative. However, a key consequence of working in a truncated configuration space is that properties relying on the completeness of the exact [eigenstates](@entry_id:149904), such as the **Thomas-Reiche-Kuhn (TRK) sum rule** ($\sum_n f_{0n} = N_{\text{electrons}}$), are not exactly satisfied. As one moves up the ADC hierarchy, the ISR becomes more complete, and the sum rule is fulfilled more accurately, but exact satisfaction requires the full, infinite Hilbert space [@problem_id:2890595].

Another premier family of methods is based on the **Equation-of-Motion Coupled-Cluster (EOM-CC)** ansatz. A major challenge for standard single-reference methods like CCSD is systems with strong **[static correlation](@entry_id:195411)**, where the ground state is poorly described by a single determinant. This occurs in bond-breaking, [diradicals](@entry_id:165761), and certain [transition metal complexes](@entry_id:144856). **Spin-Flip EOM-CCSD** is an ingenious solution to this problem. Instead of starting from the poorly-described low-spin ground state, the calculation begins with a well-behaved high-spin single-determinant reference (e.g., the $M_S=1$ triplet state of a diradical). The EOM operators, $\hat{R}_k$, are then designed to not only excite electrons but also to flip the spin of one electron (e.g., $\alpha \to \beta$), thereby reducing the total [spin projection](@entry_id:184359) by one unit ($\Delta M_S = -1$). The EOM diagonalization then finds the correct linear combinations of these spin-flipped configurations to describe the low-spin target states (e.g., the $M_S=0$ singlet and triplet). In this way, the [multireference character](@entry_id:180987) of the target state is captured by the [linear expansion](@entry_id:143725) of the EOM operator, while the [reference state](@entry_id:151465) remains simple and single-configurational [@problem_id:2890597]. While highly effective, this approach can suffer from spin contamination, an issue addressed by more advanced spin-adapted formulations [@problem_id:2890597].

#### Many-Body Green's Function Theory: The GW-BSE Approach

For condensed matter systems and large molecules, the **GW-BSE** approach has become the gold standard. This two-step method carefully distinguishes between two types of excitations.

First, the **GW approximation** is used to calculate **[quasiparticle energies](@entry_id:173936)**, which correspond to **charged excitations**: the energies required to add or remove an electron ([ionization](@entry_id:136315) potentials and electron affinities). This is accomplished by calculating the electron **[self-energy](@entry_id:145608)**, $\Sigma$, which corrects the mean-field (e.g., DFT) eigenvalues. The self-energy is approximated as the product of the one-particle Green's function $G$ and the dynamically screened Coulomb interaction $W$, hence the name $\Sigma \approx iGW$. The [quasiparticle energies](@entry_id:173936) $E_n^{\text{QP}}$ are then found by solving a Dyson-like equation, often linearized for practicality [@problem_id:2890572]:

$$
E_n^{\text{QP}} \approx \epsilon_n + Z_n \langle \phi_n \lvert \Sigma(\epsilon_n) - v_{\text{xc}} \rvert \phi_n \rangle
$$

where $Z_n$ is a [renormalization](@entry_id:143501) factor. The $GW$ correction typically opens up the fundamental gap between occupied and [virtual states](@entry_id:151513) compared to standard DFT.

Second, to describe **neutral excitations** (as seen in [optical absorption](@entry_id:136597)), where an electron is promoted but remains in the system, one must account for the attractive interaction between the excited electron and the hole it left behind. This is the role of the **Bethe-Salpeter Equation (BSE)**. The BSE is an effective two-particle eigenvalue problem whose diagonal elements are the differences in the [quasiparticle energies](@entry_id:173936) ($E_{c}^{\text{QP}} - E_{v}^{\text{QP}}$) obtained from the prior $GW$ step. The BSE kernel, representing the electron-hole interaction, is then diagonalized in this basis. The BSE eigenvalues are the neutral [excitation energies](@entry_id:190368). This electron-hole attraction lowers the optical excitation energy relative to the fundamental quasiparticle gap. The difference is known as the **[exciton binding energy](@entry_id:138355)**, $E_b$:

$$
E_{\text{optical}} = (E_{c}^{\text{QP}} - E_{v}^{\text{QP}}) - E_b
$$

This two-step procedure is crucial: using uncorrected DFT energies in the BSE would lead to inaccurate optical gaps, as it starts from an incorrect fundamental gap [@problem_id:2890572].

### Numerical Implementation and Connection to Dynamics

The theoretical frameworks described above invariably lead to the problem of finding a few [eigenvalues and eigenvectors](@entry_id:138808) of very large matrices.

#### The Davidson Algorithm for Non-Hermitian Problems

Methods like EOM-CC and TDDFT beyond the Tamm-Dancoff approximation result in **non-Hermitian** eigenvalue problems. Solving these by direct diagonalization is computationally prohibitive. The **Davidson algorithm** is the iterative method of choice. For non-Hermitian matrices, a **two-sided** or **bi-orthogonal** variant is required. This involves building separate right ($\operatorname{span}(V)$) and left ($\operatorname{span}(W)$) trial subspaces that are kept bi-orthonormal ($W^\dagger V = I$).

In each iteration, the large matrix $A$ is projected onto this small subspace ($T = W^\dagger A V$), the small projected problem is solved for a Ritz eigenpair $(\theta, v)$, and the corresponding residual $r = Av - \theta v$ is calculated. The central feature of the Davidson method is the generation of a correction vector, $t$, to expand the subspace, not by using the residual directly, but by solving the approximate correction equation:

$$
(\operatorname{diag}(A) - \theta I) t \approx -r \quad \implies \quad t_i = \frac{-r_i}{A_{ii} - \theta}
$$

This **[preconditioning](@entry_id:141204)** step, using a readily invertible [diagonal approximation](@entry_id:270948) of $(A-\theta I)$, preferentially selects components of the residual corresponding to small diagonal elements, dramatically accelerating convergence towards the desired eigenvectors [@problem_id:2890573]. The diagonal elements of the Jacobian, $A_{ii}$, often have a clear physical meaning, such as [orbital energy](@entry_id:158481) differences, making this a physically motivated and highly effective [preconditioner](@entry_id:137537) [@problem_id:2890573].

#### Coupling to Nuclear Motion: Nonadiabatic Couplings

Calculating the electronic [excited states](@entry_id:273472) is often just the beginning. Understanding subsequent photochemistry requires coupling this electronic information to the motion of the nuclei, going beyond the simple Born-Oppenheimer (BO) approximation where nuclei are fixed. The terms that mediate transitions between different BO electronic potential energy surfaces are the **nonadiabatic [derivative coupling](@entry_id:202003) vectors**:

$$
\mathbf{d}_{IJ}(\mathbf{R}) \equiv \langle \Psi_I(\mathbf{R}) \vert \nabla_{\mathbf{R}} \Psi_J(\mathbf{R}) \rangle
$$

These couplings depend on the nuclear coordinates $\mathbf{R}$ and have a crucial but subtle property: they are **gauge-dependent**. The phase of the electronic wavefunctions $\lvert \Psi_I \rangle$ is arbitrary. A change of phase, $\lvert \Psi_I' \rangle = e^{i\theta_I(\mathbf{R})} \lvert \Psi_I \rangle$, which leaves all physical observables unchanged, alters the couplings. The diagonal ($I=J$) and off-diagonal ($I \neq J$) elements transform differently [@problem_id:2890577]:

$$
\mathbf{d}_{II}'(\mathbf{R}) = \mathbf{d}_{II}(\mathbf{R}) + i \nabla_{\mathbf{R}} \theta_I(\mathbf{R})
$$
$$
\mathbf{d}_{IJ}'(\mathbf{R}) = e^{i(\theta_J(\mathbf{R}) - \theta_I(\mathbf{R}))} \mathbf{d}_{IJ}(\mathbf{R}) \quad (I \neq J)
$$

The diagonal coupling $\mathbf{d}_{II}$ acts like a vector potential and is not gauge-invariant. However, its curl, $\nabla_{\mathbf{R}} \times \mathbf{d}_{II}(\mathbf{R})$, is gauge-invariant and is related to the **[geometric phase](@entry_id:138449)** (or Berry phase), a deeply important concept for systems with [conical intersections](@entry_id:191929). In contrast, for the off-diagonal couplings that directly drive [population transfer](@entry_id:170564), it is their magnitude, $|\mathbf{d}_{IJ}(\mathbf{R})|$, that is gauge-invariant and thus physically meaningful [@problem_id:2890577]. Understanding these properties is essential for the correct formulation of nonadiabatic [molecular dynamics simulations](@entry_id:160737).