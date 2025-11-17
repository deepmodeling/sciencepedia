## Introduction
The classical theory of electromagnetism, a pillar of 19th-century physics, provides a masterful description of macroscopic phenomena. However, its authority wanes at the atomic scale, where quantum effects dominate. A critical breakdown occurs with the phenomenon of spontaneous emission—the decay of an excited atom in a perfect vacuum—which classical and even semi-classical theories cannot explain. This gap highlights a fundamental necessity: the electromagnetic field itself must be a quantum-mechanical entity. This article provides a comprehensive introduction to the quantization of the free electromagnetic field, the foundational theory of quantum optics.

This journey into the [quantum nature of light](@entry_id:270825) unfolds across three chapters. In **Principles and Mechanisms**, we will perform the [canonical quantization](@entry_id:148501) of the classical field, transforming its normal modes into quantum harmonic oscillators and introducing the photon as the fundamental [quantum of light](@entry_id:173025). We will define the essential [field operators](@entry_id:140269) and the field Hamiltonian, confronting the profound concept of [zero-point energy](@entry_id:142176) and [vacuum fluctuations](@entry_id:154889). Next, in **Applications and Interdisciplinary Connections**, we will explore the rich physical consequences of this theory, from explaining the [quantum statistics](@entry_id:143815) of light and the Casimir effect to its role in van der Waals forces and the startling Unruh effect. Finally, **Hands-On Practices** will provide opportunities to apply these concepts to concrete physical problems, solidifying your understanding of the momentum, polarization, and energy of single-photon states.

## Principles and Mechanisms

The classical theory of electromagnetism, while remarkably successful, proves incomplete when describing interactions at the atomic scale. A semi-classical approach, which treats matter quantum mechanically but retains a classical description of the electromagnetic field, can account for phenomena like absorption and stimulated emission. However, it fundamentally fails to explain one of the most basic observations in [atomic physics](@entry_id:140823): **[spontaneous emission](@entry_id:140032)**. An excited atom in a perfect vacuum, devoid of any external classical field, will still decay to its ground state by emitting a photon. This process is inexplicable in a semi-classical model, where an excited state in the absence of an external field is a stationary state of the atomic Hamiltonian and should remain stable indefinitely [@problem_id:1393133]. The existence of spontaneous emission is compelling evidence that the electromagnetic field itself must be quantized. The mechanism for this decay arises from the interaction of the atom with the "[vacuum fluctuations](@entry_id:154889)" of the quantized field, a concept we will develop in this chapter.

### From Classical Modes to Quantum Oscillators

The quantization of the free electromagnetic field begins with its classical description. The total energy $H$ of the field in a vacuum is given by the integral of its energy density over all space:
$$
H = \frac{1}{2} \int d^3\mathbf{r} \left( \epsilon_0 \mathbf{E}^2(\mathbf{r}, t) + \frac{1}{\mu_0} \mathbf{B}^2(\mathbf{r}, t) \right)
$$
To make the structure more tractable, we work in the **Coulomb gauge**, where $\nabla \cdot \mathbf{A} = 0$. In this gauge, the [scalar potential](@entry_id:276177) is zero, and the electric and magnetic fields are derived solely from the [vector potential](@entry_id:153642) $\mathbf{A}(\mathbf{r}, t)$:
$$
\mathbf{E} = -\frac{\partial \mathbf{A}}{\partial t}, \quad \mathbf{B} = \nabla \times \mathbf{A}
$$
The classical field $\mathbf{A}(\mathbf{r}, t)$ can be decomposed into a superposition of normal modes. Within a quantization volume $V$, this is a Fourier series, which in the [continuum limit](@entry_id:162780) ($V \to \infty$) becomes a Fourier integral. For each wavevector $\mathbf{k}$, there are two mutually orthogonal polarization directions, indexed by $\lambda \in \{1, 2\}$, that are transverse to $\mathbf{k}$ (a consequence of the Coulomb [gauge condition](@entry_id:749729)). The [vector potential](@entry_id:153642) can be written as:
$$
\mathbf{A}(\mathbf{r}, t) = \sum_{\mathbf{k}, \lambda} \left( \mathbf{\epsilon}_{\mathbf{k}, \lambda} A_{\mathbf{k}, \lambda}(t) e^{i\mathbf{k} \cdot \mathbf{r}} + \mathbf{\epsilon}_{\mathbf{k}, \lambda}^* A_{\mathbf{k}, \lambda}^*(t) e^{-i\mathbf{k} \cdot \mathbf{r}} \right)
$$
where $\mathbf{\epsilon}_{\mathbf{k}, \lambda}$ are the (possibly complex) polarization vectors and $A_{\mathbf{k}, \lambda}(t)$ are time-dependent complex amplitudes. Substituting this into the Hamiltonian and performing the spatial integral reveals a remarkable result: the total energy of the field is a sum of energies of independent terms, one for each mode $(\mathbf{k}, \lambda)$. Each term has the mathematical form of a [classical harmonic oscillator](@entry_id:153404).

This analogy is the gateway to quantization. We perform **[canonical quantization](@entry_id:148501)** by promoting the classical amplitudes for each mode to quantum operators. We define the **[annihilation operator](@entry_id:149476)** $\hat{a}_{\mathbf{k}, \lambda}$ and **[creation operator](@entry_id:264870)** $\hat{a}_{\mathbf{k}, \lambda}^\dagger$, which replace the classical Fourier amplitudes. These operators are postulated to obey the [canonical commutation relations](@entry_id:185041) for bosons:
$$
[\hat{a}_{\mathbf{k}, \lambda}, \hat{a}_{\mathbf{k}', \lambda'}^\dagger] = \delta_{\mathbf{k}\mathbf{k}'} \delta_{\lambda\lambda'}
$$
$$
[\hat{a}_{\mathbf{k}, \lambda}, \hat{a}_{\mathbf{k}', \lambda'}] = [\hat{a}_{\mathbf{k}, \lambda}^\dagger, \hat{a}_{\mathbf{k}', \lambda'}^\dagger] = 0
$$
Here, we have used the discrete mode notation for simplicity; in the continuum, the Kronecker deltas $\delta_{\mathbf{k}\mathbf{k}'}$ are replaced by Dirac delta functions $\delta(\mathbf{k}-\mathbf{k}')$ with appropriate factors of $(2\pi)^3$ [@problem_id:711853].

### The Field Operators and the Photon

With this promotion, the fields themselves become operators. In the Schrödinger picture, the transverse [vector potential](@entry_id:153642) operator $\hat{\mathbf{A}}(\mathbf{r})$ is written as an expansion in these [creation and annihilation operators](@entry_id:147121). For a quantization volume $V$, a common form uses circularly polarized plane waves:
$$
\hat{\mathbf{A}}(\mathbf{r}) = \sum_{\mathbf{k}, \lambda} \sqrt{\frac{\hbar}{2 \epsilon_0 V \omega_k}} \left( \hat{a}_{\mathbf{k}, \lambda} \boldsymbol{\epsilon}_{\mathbf{k}, \lambda} e^{i\mathbf{k}\cdot\mathbf{r}} + \hat{a}^\dagger_{\mathbf{k}, \lambda} \boldsymbol{\epsilon}^*_{\mathbf{k}, \lambda} e^{-i\mathbf{k}\cdot\mathbf{r}} \right)
$$
where $\omega_k = c|\mathbf{k}|$ is the mode frequency. The operator $\hat{a}_{\mathbf{k}, \lambda}$ annihilates a quantum of excitation in the mode $(\mathbf{k}, \lambda)$, while $\hat{a}^\dagger_{\mathbf{k}, \lambda}$ creates one. This fundamental quantum of the electromagnetic field is what we call the **photon**.

The electric and magnetic [field operators](@entry_id:140269) are then derived from $\hat{\mathbf{A}}(\mathbf{r})$ and its [canonical momentum](@entry_id:155151). The electric field operator $\hat{\mathbf{E}}(\mathbf{r})$ is proportional to the canonical momentum, while the magnetic field operator is $\hat{\mathbf{B}}(\mathbf{r}) = \nabla \times \hat{\mathbf{A}}(\mathbf{r})$. Their expansions are:
$$
\hat{\mathbf{E}}(\mathbf{r}) = \sum_{\mathbf{k}, \lambda} i \sqrt{\frac{\hbar \omega_k}{2 \epsilon_0 V}} \left( \hat{a}_{\mathbf{k}, \lambda} \boldsymbol{\epsilon}_{\mathbf{k}, \lambda} e^{i \mathbf{k} \cdot \mathbf{r}} - \hat{a}_{\mathbf{k}, \lambda}^\dagger \boldsymbol{\epsilon}_{\mathbf{k}, \lambda}^* e^{-i \mathbf{k} \cdot \mathbf{r}} \right)
$$
$$
\hat{\mathbf{B}}(\mathbf{r}) = \sum_{\mathbf{k}, \lambda} i \sqrt{\frac{\hbar}{2 \epsilon_0 V \omega_k}} \left( (\mathbf{k} \times \boldsymbol{\epsilon}_{\mathbf{k}, \lambda}) \hat{a}_{\mathbf{k}, \lambda} e^{i\mathbf{k}\cdot\mathbf{r}} - (\mathbf{k} \times \boldsymbol{\epsilon}_{\mathbf{k}, \lambda}^*) \hat{a}_{\mathbf{k}, \lambda}^\dagger e^{-i\mathbf{k}\cdot\mathbf{r}} \right)
$$
These operator expressions are the foundation of quantum optics. They embody the [wave-particle duality](@entry_id:141736) of light: the wave nature is present in the plane-wave factors $e^{i\mathbf{k}\cdot\mathbf{r}}$ and mode structure, while the particle nature is captured by the discrete actions of the [creation and annihilation operators](@entry_id:147121). The ground state of the field, the **vacuum state** $|0\rangle$, is defined as the state containing no photons, i.e., it is annihilated by all [annihilation operators](@entry_id:180957): $\hat{a}_{\mathbf{k}, \lambda}|0\rangle = 0$ for all modes.

### The Field Hamiltonian and Zero-Point Energy

Substituting the [field operators](@entry_id:140269) into the classical energy expression yields the Hamiltonian operator for the quantum field. After a lengthy but straightforward calculation involving the commutation relations, one finds:
$$
\hat{H} = \sum_{\mathbf{k}, \lambda} \hbar \omega_k \left( \hat{a}_{\mathbf{k}, \lambda}^{\dagger} \hat{a}_{\mathbf{k}, \lambda} + \frac{1}{2} \right)
$$
This is a central result. It confirms that the total energy of the field is the sum of energies of independent quantum harmonic oscillators. The operator $\hat{N}_{\mathbf{k}, \lambda} = \hat{a}_{\mathbf{k}, \lambda}^{\dagger} \hat{a}_{\mathbf{k}, \lambda}$ is the **[number operator](@entry_id:153568)**; its eigenvalues are the integers $n = 0, 1, 2, ...$, representing the number of photons in mode $(\mathbf{k}, \lambda)$. The energy of a state with $n_{\mathbf{k}, \lambda}$ photons in each mode is thus $\sum_{\mathbf{k}, \lambda} \hbar \omega_k (n_{\mathbf{k}, \lambda} + \frac{1}{2})$.

The term $+\frac{1}{2}$ in the Hamiltonian leads to a profound and problematic consequence. The energy of the vacuum state $|0\rangle$ is not zero, but rather the **zero-point energy**:
$$
E_0 = \langle 0 | \hat{H} | 0 \rangle = \sum_{\mathbf{k}, \lambda} \frac{1}{2}\hbar\omega_k
$$
Since the sum is over all possible wavevectors, this sum diverges, yielding an infinite energy for empty space. This is the first of several infinities encountered in quantum field theory.

To work with this divergence, one can employ a **regularization** scheme. For instance, one can introduce a cutoff factor that suppresses high-frequency modes, such as $e^{-\omega_k / \Omega}$ where $\Omega$ is a cutoff frequency. The regularized [zero-point energy](@entry_id:142176) density can then be calculated, yielding a finite result that depends on the cutoff [@problem_id:756347].

For many applications, this infinite constant energy can be disregarded, as only energy differences are measurable. This is formalized by the procedure of **[normal ordering](@entry_id:145434)**. A normally ordered product, denoted by $:\hat{O}:$, is one in which all [creation operators](@entry_id:191512) are placed to the left of all [annihilation operators](@entry_id:180957). Applying this to the Hamiltonian, we define a new Hamiltonian where the [vacuum energy](@entry_id:155067) is zero by definition:
$$
\hat{H} = \frac{1}{2}\int d^3\mathbf{r} :\! \left( \epsilon_0 \hat{\mathbf{E}}^2(\mathbf{r}) + \frac{1}{\mu_0} \hat{\mathbf{B}}^2(\mathbf{r}) \right) \! : = \sum_{\mathbf{k}, \lambda} \hbar \omega_k \hat{a}_{\mathbf{k}, \lambda}^\dagger \hat{a}_{\mathbf{k}, \lambda}
$$
This redefinition sets the vacuum energy to zero and allows us to interpret $\hbar \omega_k$ as the energy of a single photon with [wavevector](@entry_id:178620) $\mathbf{k}$ [@problem_id:711806]. While this is a convenient formal step, it is crucial to remember that the [zero-point energy](@entry_id:142176) is physically real and has observable consequences, such as the Casimir effect and its role in [spontaneous emission](@entry_id:140032).

### Properties of the Quantized Fields and Photon States

The quantization of the fields leads to a rich set of physical properties that distinguish the quantum theory from its classical counterpart.

#### Field Commutators and Vacuum Fluctuations

A key feature of quantum fields is that field components at different spacetime points do not, in general, commute. A fundamental equal-time commutation relation (ETCR) is that between the electric and magnetic [field operators](@entry_id:140269). A direct calculation using the operator expansions yields:
$$
[\hat{E}_i(\mathbf{x}), \hat{B}_j(\mathbf{y})] = - \frac{i\hbar}{\epsilon_0} \epsilon_{ijk} \frac{\partial}{\partial x_k} \delta^{(3)}(\mathbf{x}-\mathbf{y})
$$
where $\epsilon_{ijk}$ is the Levi-Civita symbol. This [non-commutativity](@entry_id:153545) is a direct manifestation of the uncertainty principle applied to fields: one cannot simultaneously measure the electric and magnetic field components at a point with arbitrary precision. The presence of the derivative of a [delta function](@entry_id:273429) shows that the fields are highly singular and correlated at short distances [@problem_id:711853].

Even in the vacuum state $|0\rangle$, where the expectation values of the fields are zero, $\langle 0 | \hat{\mathbf{E}}(\mathbf{r}) | 0 \rangle = \langle 0 | \hat{\mathbf{B}}(\mathbf{r}) | 0 \rangle = 0$, their variances are not. For example, $\langle 0 | \hat{\mathbf{E}}^2(\mathbf{r}) | 0 \rangle \neq 0$. These are the **[vacuum fluctuations](@entry_id:154889)**, the spontaneous creation and annihilation of virtual photon pairs that permeate all of space. It is these fluctuations that an excited atom "feels" and interacts with, leading to its decay via [spontaneous emission](@entry_id:140032).

#### Photon States and Observables

Single-photon states are created by applying a [creation operator](@entry_id:264870) to the vacuum, $|1_{\mathbf{k}_0, \lambda_0}\rangle = \hat{a}^\dagger_{\mathbf{k}_0, \lambda_0} |0\rangle$. We can compute the expectation value of physical observables in such states. For example, the [magnetic energy density](@entry_id:193006) in a single-photon state, in excess of the vacuum energy, is found to be uniform throughout the quantization volume $V$ and equal to $\Delta \rho_B = \frac{\hbar \omega_{k_0}}{2V}$. The total excess energy (electric plus magnetic) in the volume is thus $\hbar \omega_{k_0}$, confirming our interpretation of the energy of a single photon [@problem_id:711870].

More complex states can be constructed, such as a two-photon state $| \psi \rangle = \hat{a}_{\mathbf{k}_0, R}^\dagger \hat{a}_{\mathbf{k}_0, L}^\dagger |0\rangle$. Probing such states involves measuring correlation functions. For instance, the normally ordered [two-point correlation function](@entry_id:185074) $\langle \psi | : \hat{E}_x(\mathbf{r}_1) \hat{E}_x(\mathbf{r}_2) : | \psi \rangle$ reveals the spatial coherence properties of the field. For two points separated by a distance $L$ along the propagation axis, this function exhibits a cosine-like spatial modulation, $\propto \cos(k_0 L)$, which is a signature of the underlying wave nature of the constituent photons [@problem_id:711717].

#### Photon Helicity

Photons, as spin-1 particles, possess angular momentum. For a massless particle, a particularly useful quantity is **[helicity](@entry_id:157633)**, the projection of the spin angular momentum $\mathbf{S}$ onto the direction of momentum $\hat{\mathbf{p}}$. The eigenvalues of the [helicity](@entry_id:157633) operator, $h = \mathbf{S} \cdot \hat{\mathbf{p}}$, are $\lambda = \pm 1$, corresponding to right- and left-circular polarization, respectively. The $\lambda=0$ state is absent for massless photons. Helicity is a Lorentz-invariant quantity for [massless particles](@entry_id:263424). It is instructive to see how it behaves under [discrete symmetries](@entry_id:158714) like parity. The [parity operator](@entry_id:148434) $\mathcal{P}$ inverts spatial coordinates, $\mathbf{x} \to -\mathbf{x}$. Under parity, a [true vector](@entry_id:190731) like momentum inverts ($\mathbf{P} \to -\mathbf{P}$), but an [axial vector](@entry_id:191829) like spin does not ($\mathbf{S} \to \mathbf{S}$). Consequently, the [helicity](@entry_id:157633) operator flips its sign: $\mathcal{P} h \mathcal{P}^{-1} = -h$. This implies that a [parity transformation](@entry_id:159187) on a photon state with [helicity](@entry_id:157633) $\lambda=+1$ results in a state with [helicity](@entry_id:157633) $\lambda'=-1$ [@problem_id:360387].

### Covariant Quantization: The Gupta-Bleuler Formalism

The Coulomb gauge quantization, while intuitive, is not manifestly Lorentz covariant because the condition $\nabla \cdot \mathbf{A} = 0$ is not preserved under a general Lorentz transformation. For relativistic theories, a covariant approach is preferable. The **Gupta-Bleuler formalism** provides such a framework by working in the Lorenz gauge, $\partial_\mu A^\mu = 0$.

This formalism introduces two "unphysical" types of photons: **scalar** (timelike, $\lambda=0$) and **longitudinal** (spacelike, along $\mathbf{k}$, $\lambda=3$), in addition to the two [transverse photons](@entry_id:197405). This is accomplished by quantizing the four-potential $A^\mu$. The crucial modification is the use of an indefinite metric in the state space, which manifests in the [commutation relation](@entry_id:150292):
$$
[a_{\mathbf{k},\lambda}, a^\dagger_{\mathbf{k}',\lambda'}] = - \eta_{\lambda\lambda'} \delta_{\mathbf{k}\mathbf{k}'}
$$
where $\eta = \text{diag}(1, -1, -1, -1)$ is the Minkowski metric. The unusual negative sign for the commutator of the scalar photon ($[a_0, a_0^\dagger] = -1$) implies that states created by $a_0^\dagger$ have negative norm, a bizarre but necessary feature of the mathematics.

This machinery leads to some elegant cancellations. For instance, when calculating the vacuum energy, the contribution from the scalar photon mode is negative, while the contribution from the longitudinal mode is positive. For any given [wavevector](@entry_id:178620) $\mathbf{k}$, these two contributions exactly cancel each other out: $E_{vac, S+L}(\mathbf{k}) = -\frac{\hbar\omega_k}{2} + \frac{\hbar\omega_k}{2} = 0$ [@problem_id:711825]. This leaves only the divergent vacuum energy from the two [transverse modes](@entry_id:163265), the same result as in the Coulomb gauge.

Physical states $|\psi\rangle_{\text{phys}}$ are defined by a weaker version of the Lorenz [gauge condition](@entry_id:749729). Instead of demanding $\partial_\mu \hat{A}^\mu = 0$ as an operator identity, we require that the annihilation part of the operator annihilates physical states: $(\partial_\mu \hat{A}^\mu)^{(+)} |\psi\rangle_{\text{phys}} = 0$. This ensures that the expectation value of the Lorenz condition operator is zero for any physical state, such as a state containing only [transverse photons](@entry_id:197405) [@problem_id:711783]. The unphysical scalar and longitudinal photons do not appear in initial or final states of physical processes. They exist only as virtual particles in intermediate states and combine in specific ways to ensure that physical observables are consistent. For example, specific linear combinations of scalar and longitudinal photon states can form zero-norm states, which are orthogonal to all physical states and have no impact on physical measurements [@problem_id:323944]. This intricate structure ensures the covariance of the theory while recovering the correct physical predictions of the simpler, non-covariant Coulomb gauge approach.