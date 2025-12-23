## Introduction
The atomic nucleus, a complex system of strongly interacting protons and neutrons, presents one of the most formidable challenges in computational science. For decades, classical computers have struggled against the exponential scaling of the [nuclear many-body problem](@entry_id:161400), forcing physicists to rely on approximations that limit predictive power. The advent of quantum computing offers a new paradigm, promising to solve the Schrödinger equation for nuclei with unprecedented accuracy by harnessing the principles of quantum mechanics itself. This approach could revolutionize our understanding of nuclear structure, reactions, and the fundamental forces that govern matter.

This article provides a comprehensive guide to the principles, methods, and applications of quantum computing in nuclear physics. It addresses the critical knowledge gap between abstract quantum algorithms and their concrete implementation for solving nuclear problems. Across three chapters, you will gain a deep understanding of this rapidly advancing field. We begin by laying the groundwork in **Principles and Mechanisms**, where we detail how to translate the nuclear Hamiltonian into the language of qubits and explore the foundational [quantum algorithms](@entry_id:147346) used to solve for its properties. Next, in **Applications and Interdisciplinary Connections**, we showcase how these tools are applied to tangible problems, from calculating the spectra of [light nuclei](@entry_id:751275) to simulating complex nuclear reactions, and highlight the rich cross-pollination of ideas with fields like machine learning and [quantum information science](@entry_id:150091). Finally, the **Hands-On Practices** section provides an opportunity to solidify these concepts by working through practical exercises in Hamiltonian mapping, reference state calculations, and [error mitigation](@entry_id:749087).

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that underpin the application of quantum computing to nuclear physics. We transition from the abstract formulation of the [nuclear many-body problem](@entry_id:161400) to the concrete steps required for its representation and solution on quantum hardware. Our exploration will cover three main areas: first, how the nuclear Hamiltonian is formulated and mapped onto a system of qubits; second, the primary quantum algorithms employed to solve for its properties; and third, the intrinsic theoretical and practical challenges that define the frontiers of this research area.

### The Nuclear Hamiltonian in Second Quantization

The starting point for any *ab initio* nuclear structure or reaction calculation is the Hamiltonian, which governs the dynamics of the constituent nucleons (protons and neutrons). In a non-relativistic framework, this Hamiltonian, $H$, is typically expressed as a sum of one-body kinetic energy terms and two-body interactions, with three-body (and higher) interactions included for high-accuracy calculations.

When working within a finite single-particle basis, such as the eigenstates of a [harmonic oscillator](@entry_id:155622) or a Hartree-Fock mean field, it is most convenient to express the Hamiltonian in the language of **[second quantization](@entry_id:137766)**. Let $a_p^\dagger$ and $a_p$ be the [creation and annihilation operators](@entry_id:147121), respectively, for a nucleon in a single-particle state labeled by the [quantum numbers](@entry_id:145558) $p$. These operators obey the canonical fermionic [anticommutation](@entry_id:182725) relations:
$$
\{a_p, a_q^\dagger\} = a_p a_q^\dagger + a_q^\dagger a_p = \delta_{pq}, \quad \{a_p, a_q\} = \{a_p^\dagger, a_q^\dagger\} = 0
$$
where $\delta_{pq}$ is the Kronecker delta. These relations mathematically enforce the Pauli exclusion principle, which is fundamental to the behavior of fermions like nucleons.

A general nuclear Hamiltonian including up to [three-body forces](@entry_id:159489) can be written in this formalism as:
$$
H = \sum_{pq} t_{pq} a_p^\dagger a_q + \frac{1}{4}\sum_{pqrs} v_{pqrs} a_p^\dagger a_q^\dagger a_s a_r + \frac{1}{36}\sum_{pqrstu} w_{pqrstu} a_p^\dagger a_q^\dagger a_r^\dagger a_u a_t a_s
$$
Here, the coefficients are [matrix elements](@entry_id:186505) of the interaction operators calculated in the chosen single-particle basis. The term $t_{pq}$ represents the one-body part (e.g., kinetic energy and external potential). The terms $v_{pqrs}$ and $w_{pqrstu}$ represent the two- and three-body interactions, respectively. 

A crucial feature of this representation is the specific prefactors and the symmetry properties of the [matrix elements](@entry_id:186505), which directly follow from the fermionic nature of the operators. For the two-body term, the antisymmetrized [matrix element](@entry_id:136260) $v_{pqrs}$ is used, which has the property $v_{pqrs} = -v_{qprs} = -v_{pqsr}$. This antisymmetry reflects the indistinguishability of the two particles being created (in states $p,q$) and the two being annihilated (in states $r,s$). When summing over all indices without restriction, this leads to the prefactor of $\frac{1}{4} = \frac{1}{(2!)^2}$. Similarly, for the three-body term, a fully antisymmetrized matrix element $w_{pqrstu}$ is used (antisymmetric in the first three and last three indices separately), which gives rise to the prefactor of $\frac{1}{36} = \frac{1}{(3!)^2}$. The Hermiticity of the Hamiltonian imposes further constraints, namely $t_{pq} = t_{qp}^*$, $v_{pqrs} = v_{rspq}^*$, and $w_{pqrstu} = w_{stupqr}^*$. This second-quantized form is the standard representation of the nuclear problem that must be translated for a quantum computer.

### Mapping Fermions to Qubits

Quantum computers operate on qubits, which are two-level quantum systems described by Pauli algebra, not [fermionic operators](@entry_id:149120). Therefore, a critical step is to establish a mapping between the fermionic Hilbert space and the qubit Hilbert space that faithfully preserves the algebraic structure of the problem. This mapping must transform the fermionic [creation and annihilation operators](@entry_id:147121) into operators acting on qubits, while ensuring that the [canonical anticommutation relations](@entry_id:146961) are satisfied.

#### The Jordan-Wigner Transformation

The most direct of these mappings is the **Jordan-Wigner (JW) transformation**.  It associates each of the $N$ single-particle fermionic modes with one of $N$ qubits. The occupancy of a fermionic mode (either 0 or 1) is encoded in the state of the corresponding qubit, typically with $|1\rangle$ representing an occupied mode and $|0\rangle$ an empty one. The [number operator](@entry_id:153568) $n_p = a_p^\dagger a_p$ is then naturally related to the Pauli-$Z$ operator on qubit $p$: $n_p \mapsto \frac{1}{2}(I - Z_p)$.

To construct the [creation and annihilation operators](@entry_id:147121), the JW transformation uses local ladder operators on each qubit, $\sigma_p^+ = \frac{1}{2}(X_p + iY_p)$ and $\sigma_p^- = \frac{1}{2}(X_p - iY_p)$, and combines them with non-local strings of Pauli-$Z$ operators. The [annihilation operator](@entry_id:149476) $a_p$ maps to the qubit-state lowering operator $\sigma_p^+$, while the [creation operator](@entry_id:264870) $a_p^\dagger$ maps to the qubit-state raising operator $\sigma_p^-$. The full transformation is given by:
$$
a_p \mapsto \left(\prod_{j=0}^{p-1} Z_j\right) \sigma_p^+ = \frac{1}{2}\left(\prod_{j=0}^{p-1} Z_j\right)(X_p + iY_p)
$$
$$
a_p^\dagger \mapsto \left(\prod_{j=0}^{p-1} Z_j\right) \sigma_p^- = \frac{1}{2}\left(\prod_{j=0}^{p-1} Z_j\right)(X_p - iY_p)
$$
The string of $Z$ operators, often called the **parity string** or Jordan-Wigner string, runs over all qubits with an index less than $p$. Its function is to enforce the correct [anticommutation](@entry_id:182725) relations for operators on different fermionic modes. While operators on different qubits commute (e.g., $[X_p, Z_q]=0$ for $p \neq q$), [fermionic operators](@entry_id:149120) must anticommute. The Z-string provides the necessary minus sign. For instance, consider two operators $a_p$ and $a_q$ with $p  q$. When forming the product $a_p a_q$, the local part of $a_q$ (at site $q$) commutes with the local part of $a_p$ (at site $p$). However, in the product $a_q a_p$, the local operator at site $p$ must pass through the Z-string of the operator at site $q$, which contains a $Z_p$ factor. Since Pauli operators $X_p$ and $Y_p$ anticommute with $Z_p$, this generates a minus sign, leading to $a_q a_p = - a_p a_q$ and thus ensuring $\{a_p, a_q\}=0$. A similar mechanism ensures that $\{a_p, a_q^\dagger\}=0$ for $p \neq q$.

#### Alternative Mappings: Bravyi-Kitaev and Parity

While the JW transformation is conceptually straightforward, the non-local nature of its Z-strings can be a disadvantage. An operator acting on a high-index fermionic mode $p$ becomes a Pauli string acting on up to $p$ qubits. This can increase the resources needed for simulation.

To address this, alternative mappings have been developed. The **Bravyi-Kitaev (BK) transformation** uses a more sophisticated data structure, akin to a Fenwick tree, to store parity information.  In the BK mapping, the occupation of a fermionic mode $p$ is stored non-locally across a set of qubits of size $O(\log N)$, and conversely, the state of a single qubit affects the parity of an $O(\log N)$ set of modes. The key advantage is that any single fermionic operator $a_p$ or $a_p^\dagger$ maps to a Pauli string with a weight of only $O(\log N)$. This logarithmic scaling makes the BK transformation significantly more efficient for systems with [long-range interactions](@entry_id:140725), as we will see later. Other encodings, such as the **Parity mapping**, also exist and offer different trade-offs between locality and complexity.

### Quantum Algorithms for Nuclear Physics

Once the nuclear Hamiltonian is expressed as a sum of Pauli strings, $H = \sum_j h_j P_j$, we can employ quantum algorithms to find its [eigenvalues and eigenstates](@entry_id:149417). The two dominant paradigms are [variational methods](@entry_id:163656) and time-evolution-based methods.

#### Variational Quantum Eigensolver (VQE)

The VQE algorithm is a [hybrid quantum-classical](@entry_id:750433) approach that leverages the **[variational principle](@entry_id:145218)** of quantum mechanics. This principle states that for any trial quantum state $|\psi(\boldsymbol{\theta})\rangle$, the [expectation value](@entry_id:150961) of the Hamiltonian is an upper bound to the true [ground-state energy](@entry_id:263704) $E_0$:
$$
E(\boldsymbol{\theta}) = \langle \psi(\boldsymbol{\theta}) | H | \psi(\boldsymbol{\theta}) \rangle \ge E_0
$$
VQE works by preparing a parameterized trial state $|\psi(\boldsymbol{\theta})\rangle = U(\boldsymbol{\theta})|\phi_0\rangle$ on a quantum computer, where $U(\boldsymbol{\theta})$ is a parameterized quantum circuit and $|\phi_0\rangle$ is an easily prepared reference state. The quantum computer is used to estimate the energy $E(\boldsymbol{\theta})$ by measuring the expectation values of the individual Pauli strings $P_j$ in the Hamiltonian and summing them classically: $E(\boldsymbol{\theta}) = \sum_j h_j \langle P_j \rangle$. A classical optimizer then updates the parameters $\boldsymbol{\theta}$ to minimize $E(\boldsymbol{\theta})$, iteratively approaching the ground-state energy.

##### The Unitary Coupled-Cluster Ansatz

The choice of the parameterized unitary $U(\boldsymbol{\theta})$ is critical to the success of VQE. A powerful, physically-motivated choice for molecular and nuclear systems is the **Unitary Coupled-Cluster (UCC)** [ansatz](@entry_id:184384).  This [ansatz](@entry_id:184384) is inspired by classical [coupled-cluster theory](@entry_id:141746), a gold standard in computational chemistry.

The UCC trial state is generated from a reference state, typically the Hartree-Fock Slater determinant $| \Phi_0 \rangle$, by applying a unitary operator $U(\boldsymbol{\theta}) = \exp(T(\boldsymbol{\theta}) - T^\dagger(\boldsymbol{\theta}))$. The operator $T(\boldsymbol{\theta})$ is the **cluster operator**, which is a sum of particle-hole excitation operators. Truncated to single and double excitations (UCCSD), it takes the form $T(\boldsymbol{\theta}) = T_1(\boldsymbol{\theta}) + T_2(\boldsymbol{\theta})$, where:
$$
T_1(\boldsymbol{\theta}) = \sum_{i \in \mathcal{H}, a \in \mathcal{P}} \theta_i^a a_a^\dagger a_i
$$
$$
T_2(\boldsymbol{\theta}) = \frac{1}{4} \sum_{i,j \in \mathcal{H}, a,b \in \mathcal{P}} \theta_{ij}^{ab} a_a^\dagger a_b^\dagger a_j a_i
$$
Here, $\mathcal{H}$ denotes the set of occupied (hole) orbitals in the [reference state](@entry_id:151465), and $\mathcal{P}$ denotes the unoccupied (particle) orbitals. The operators $a_a^\dagger a_i$ and $a_a^\dagger a_b^\dagger a_j a_i$ represent single and double excitations, respectively. The parameters $\boldsymbol{\theta} = \{\theta_i^a, \theta_{ij}^{ab}\}$ are real amplitudes to be determined by the variational procedure. The generator of the unitary, $T - T^\dagger$, is anti-Hermitian, ensuring that $U(\boldsymbol{\theta})$ is unitary. The UCC ansatz is systematically improvable and, by its construction, preserves symmetries like particle number.

##### Measurement and Optimization

A key practical aspect of VQE is the measurement process. Since the quantum computer provides measurement outcomes with statistical uncertainty, the total number of measurements, or **shots**, must be carefully allocated to achieve the desired precision. The variance of the total energy estimator is given by $\sigma^2 = \sum_i w_i^2 \mathrm{Var}(\widehat{\langle P_i \rangle})$, where $w_i$ are the Hamiltonian coefficients and $\mathrm{Var}(\widehat{\langle P_i \rangle}) = \mathrm{Var}(P_i)/n_i$ is the variance of the estimator for a single Pauli group measured with $n_i$ shots.

To minimize the total variance $\sigma^2$ subject to a fixed total shot budget $N = \sum_i n_i$, we can use the method of Lagrange multipliers. This yields the [optimal allocation](@entry_id:635142) rule: 
$$
n_i^\star = N \frac{|w_i| \sqrt{\mathrm{Var}(P_i)}}{\sum_j |w_j| \sqrt{\mathrm{Var}(P_j)}}
$$
This result shows that more shots should be allocated to terms with larger weights $|w_i|$ and larger intrinsic variance $\mathrm{Var}(P_i) = 1 - \langle P_i \rangle^2$. This [optimal allocation](@entry_id:635142) leads to a minimal total variance of:
$$
\sigma^2_{\min} = \frac{1}{N} \left( \sum_i |w_i| \sqrt{\mathrm{Var}(P_i)} \right)^2
$$
This illustrates how measurement resources can be intelligently managed to maximize the efficiency of VQE experiments.

#### Hamiltonian Simulation and Phase Estimation

An alternative to [variational methods](@entry_id:163656) is to directly simulate the [time-evolution operator](@entry_id:186274) $U(t) = e^{-iHt}$ and use it within algorithms like **Quantum Phase Estimation (QPE)** to extract eigenvalues. Since the terms $H_k$ in the Hamiltonian $H = \sum_k H_k$ generally do not commute, the exponential cannot be split into a simple product: $e^{-iHt} \neq \prod_k e^{-iH_k t}$.

##### Trotter-Suzuki Product Formulas

A common way to approximate the [time-evolution operator](@entry_id:186274) is with **Trotter-Suzuki product formulas**.  These formulas approximate the evolution over a small time step $\lambda$ by a sequence of evolutions under the individual terms $H_k$. The total evolution for time $t$ is then built from $r=t/\lambda$ repetitions of this small step.

The simplest is the first-order Lie-Trotter formula:
$$
S_1(\lambda) = \prod_{k=1}^m e^{-i\lambda H_k} \approx e^{-i\lambda H}
$$
The error in this approximation for a single step is $O(\lambda^2)$. After $r$ steps, the total accumulated error scales as $O(t^2/r)$, with the error constant proportional to the norm of [commutators](@entry_id:158878) $[H_j, H_k]$.

Higher-order formulas offer better accuracy. The second-order, or symmetric, Trotter formula is widely used:
$$
S_2(\lambda) = \left(\prod_{k=1}^m e^{-i(\lambda/2)H_k}\right) \left(\prod_{k=m}^1 e^{-i(\lambda/2)H_k}\right) \approx e^{-i\lambda H}
$$
By constructing a symmetric sequence, the $O(\lambda^2)$ error term is canceled, leaving a [local error](@entry_id:635842) of $O(\lambda^3)$. This results in a much smaller [global error](@entry_id:147874) that scales as $O(t^3/r^2)$, with the error constant now depending on nested [commutators](@entry_id:158878) like $[H_i, [H_j, H_k]]$.

##### Block Encoding and Advanced Methods

More advanced algorithms often rely on a technique called **block encoding**.  Instead of approximating $e^{-iHt}$, block encoding embeds the Hamiltonian $H$ as a sub-block of a larger [unitary matrix](@entry_id:138978) $\mathcal{U}$ that can be implemented exactly. This is typically achieved through the **Linear Combination of Unitaries (LCU)** framework.

Given the Hamiltonian $H = \sum_{j=0}^{N-1} c_j S_j$, where $S_j$ are Pauli strings (which are unitary), we introduce an ancilla register to index the terms. A `PREPARE` unitary $\mathcal{P}$ creates a superposition over the ancilla indices weighted by the coefficients, and a `SELECT` unitary $\mathcal{S}$ applies the corresponding Pauli string $S_j$ conditioned on the ancilla being in state $|j\rangle$. The full unitary $\mathcal{U} = \mathcal{P}^\dagger \mathcal{S} \mathcal{P}$ then has the property that its top-left block, projected onto the ancilla state $|0\rangle$, is precisely the Hamiltonian scaled by a normalization factor $\alpha$:
$$
\langle 0 | \mathcal{U} | 0 \rangle = \frac{H}{\alpha}
$$
For this to hold, $\mathcal{P}$ must prepare a normalized state, which requires that $\alpha = \sum_{j=0}^{N-1} |c_j|$, the [1-norm](@entry_id:635854) of the coefficients. The number of ancilla qubits $m$ needed to index the $N$ terms is $m = \lceil \log_2 N \rceil$. Block encoding is a powerful primitive that serves as the input to modern algorithms like Qubitization and Quantum Signal Processing, which can offer significantly better scaling with respect to simulation error than Trotter-based methods.

### Challenges and Limitations

Despite the power of these [quantum algorithms](@entry_id:147346), their application to nuclear physics faces significant challenges, both in theoretical complexity and practical implementation.

#### Algorithmic Scaling and Resource Requirements

The practical cost of a quantum simulation is determined by the number of qubits and, crucially, the number of quantum gates required. This cost depends heavily on the structure of the Hamiltonian and the chosen [fermion-to-qubit mapping](@entry_id:201306). 

Consider simulating a dense nuclear shell-model interaction on $M$ orbitals using a first-order Trotter formula. The number of distinct two-body terms in the Hamiltonian scales as $\Theta(M^4)$. The total gate count for one Trotter step is this number of terms multiplied by the average cost to simulate each term. This cost is proportional to the Pauli weight of the mapped operators.
-   For the **Jordan-Wigner** or **Parity** mappings, the non-local strings lead to Pauli operators with weight $\Theta(M)$. The total gate count scales as $\Theta(M^4) \times \Theta(M) = \Theta(M^5)$.
-   For the **Bravyi-Kitaev** mapping, the logarithmic locality ensures the Pauli weight of any number-conserving term is $\Theta(\log M)$. This leads to a much more favorable gate count scaling of $\Theta(M^4) \times \Theta(\log M) = \Theta(M^4 \log M)$.
This polynomial difference highlights the critical importance of choosing an efficient encoding and illustrates that even for quantum computers, resource requirements can be formidable.

#### Computational Complexity and the Sign Problem

A more fundamental question is whether finding the [ground-state energy](@entry_id:263704) of a nuclear Hamiltonian is an "easy" (in BQP) or "hard" (QMA-hard) problem for a quantum computer. **BQP** (Bounded-Error Quantum Polynomial Time) is the class of problems solvable efficiently by a quantum computer. **QMA** (Quantum Merlin-Arthur) is the quantum analogue of NP, representing problems for which a proposed quantum solution ("proof") can be efficiently verified on a quantum computer.

The problem of finding the [ground-state energy](@entry_id:263704) of a general local Hamiltonian is the canonical **QMA-complete** problem.  Nuclear shell-model Hamiltonians, despite their physical origins, generally fall into this category. The source of this hardness is often related to the **[fermion sign problem](@entry_id:139821)** that plagues classical Monte Carlo methods. In the quantum complexity context, this manifests as a **non-stoquastic** Hamiltonian, meaning it has positive off-diagonal matrix elements in the standard occupation-number basis, which prevents certain classical and [quantum algorithms](@entry_id:147346) from working efficiently.

While phase estimation can, in principle, find eigenvalues with high precision, it requires an initial state with significant overlap with the true ground state. For a general QMA-hard Hamiltonian, preparing such a state is itself believed to be an intractable problem. Therefore, simply having a quantum computer does not guarantee an efficient solution for the general [nuclear many-body problem](@entry_id:161400).

The problem becomes tractable (in BQP) only under special, physically restrictive conditions. For instance, if the Hamiltonian is non-interacting (quadratic in the [fermionic operators](@entry_id:149120)), or if it is stoquastic and has a known gapped path from a simple, preparable ground state (enabling adiabatic [state preparation](@entry_id:152204)), then an efficient quantum solution exists. For the general, realistic nuclear case, however, the problem remains fundamentally hard.

#### The Impact of Noise

Near-term quantum processors are subject to noise, which can corrupt the computation and lead to incorrect results. Understanding and mitigating the effects of noise is paramount.

##### Barren Plateaus

In variational algorithms like VQE, a particularly insidious noise-like phenomenon is the **[barren plateau](@entry_id:183282)**.  This refers to a region in the parameter landscape where the gradient of the cost function becomes exponentially small with the number of qubits, i.e., $\mathrm{Var}[\partial C/\partial \theta_j] \sim \mathcal{O}(\alpha^{-n})$. With exponentially small gradients, optimization becomes practically impossible, as an exponential number of measurements would be needed to find a descent direction.

Barren plateaus arise from two main sources. One is the use of a **global [cost function](@entry_id:138681)** (where the Hamiltonian acts on many or all qubits) combined with a **deep, randomly initialized ansatz**. Such circuits tend to scramble information and approximate a mathematical structure known as a unitary 2-design, which maps most initial states to states that look random. The expectation value of any global operator on such a state will be close to zero, leading to flat energy landscapes.

Several strategies can mitigate [barren plateaus](@entry_id:142779):
-   **Problem-Aware Ansatz:** Using physically motivated ansatzes like UCCSD, which restrict the search to a relevant physical subspace, avoids exploring the vast, unphysical regions of Hilbert space where random states lie.
-   **Shallow/Near-Identity Initialization:** Starting with shallow circuits or initializing parameters near zero ensures the initial trial state is close to the reference state, where gradients are typically well-behaved.
-   **Layerwise Training:** Building the [circuit depth](@entry_id:266132) layer by layer, training each new layer from a near-identity starting point, can prevent the optimizer from getting lost on a deep-circuit plateau.
-   **Local Cost Functions:** Decomposing the global Hamiltonian into local pieces and optimizing with respect to these local costs can avoid the global [barren plateau](@entry_id:183282) phenomenon, as the gradient variance of a local observable does not decay exponentially with system size.

##### Incoherent Noise and Error Mitigation

Incoherent noise processes, such as decoherence [and gate](@entry_id:166291) errors, also degrade performance. Their effect can be analyzed in the Heisenberg picture, where the noise channel $\mathcal{E}$ acts on the observable $P$ rather than the state $\rho$: $\langle P \rangle_{\text{noisy}} = \mathrm{Tr}[\mathcal{E}(\rho)P] = \mathrm{Tr}[\rho \mathcal{E}^\dagger(P)]$. 

The nature of the error depends on whether the noise channel is unital (maps the [identity operator](@entry_id:204623) to itself) or non-unital.
-   **Unital Channels:** Depolarizing and dephasing channels are unital. They cause a purely multiplicative decay of the [expectation value](@entry_id:150961). For example, under single-qubit depolarizing noise with probability $p$, an $n$-qubit Pauli string $P$ with weight $w(P)$ is transformed as $\langle P \rangle \mapsto (1-p)^{w(P)} \langle P \rangle$.
-   **Non-Unital Channels:** Amplitude damping, which models [energy relaxation](@entry_id:136820), is non-unital. It causes both multiplicative decay and an **additive bias**. For instance, $\mathcal{A}_\gamma^\dagger(Z) = (1-\gamma)Z + \gamma I$. This means the measured [expectation value](@entry_id:150961) becomes a mix of the true [expectation value](@entry_id:150961) and the expectation value of other operators (including the identity, which creates the bias).

This distinction is critical for [error mitigation](@entry_id:749087). The effects of unital channels can, in principle, be corrected by simple rescaling (e.g., Zero-Noise Extrapolation). However, the additive bias from non-unital channels cannot be removed by a single rescaling factor, requiring more sophisticated [error mitigation](@entry_id:749087) techniques. The presence of non-unital noise thus presents a more fundamental challenge to accurately estimating Hamiltonian [expectation values](@entry_id:153208) on near-term devices.