## Introduction
The postulates of quantum mechanics form the bedrock of modern physics, providing the fundamental rules that govern the behavior of matter and energy at the atomic and subatomic scales. While many are introduced to quantum concepts, a rigorous, formal understanding of its axiomatic structure is essential for tackling advanced topics in quantum thermodynamics, open systems, and quantum information. This article bridges that gap by providing a systematic exploration of the quantum mechanical framework. It begins by establishing the core principles, from the mathematical description of states and observables to the rules of measurement and [time evolution](@entry_id:153943). It then demonstrates how this abstract formalism finds powerful application in explaining real-world phenomena across chemistry, computation, and [solid-state physics](@entry_id:142261). Finally, it provides opportunities for hands-on practice to deepen comprehension. The journey begins with the foundational "Principles and Mechanisms," moves to "Applications and Interdisciplinary Connections," and concludes with "Hands-On Practices," offering a complete and coherent guide to the operational heart of quantum theory.

## Principles and Mechanisms

The theoretical framework of quantum mechanics is built upon a set of fundamental postulates that establish the mathematical representation of physical systems, [observables](@entry_id:267133), measurements, and their temporal evolution. These postulates provide the rules for connecting the abstract formalism of Hilbert spaces and operators to experimentally verifiable predictions. This chapter systematically elucidates these principles, beginning with the description of a quantum state and proceeding through the concepts of measurement, dynamics, composite systems, and fundamental constraints such as [superselection rules](@entry_id:203866).

### The State of a Quantum System

At the heart of quantum theory is the description of the state of a physical system. This is achieved through a hierarchy of concepts, from the idealized pure state to the more general mixed state, which is indispensable in the study of open quantum systems and quantum thermodynamics.

#### Postulate 1: The State Space and Pure States

The first postulate asserts that to every isolated quantum system, there is an associated complex separable **Hilbert space** $\mathcal{H}$, known as the state space. A complete description of the system, when it is in a **[pure state](@entry_id:138657)**, is given by a vector $|\psi\rangle$ in this Hilbert space.

However, a physical state is not represented by a single vector but by an entire [equivalence class](@entry_id:140585) of vectors. All physical predictions derived from a state vector, such as [expectation values](@entry_id:153208) and probabilities, are invariant under the scaling of the vector by any non-zero complex number $c$. Consider the [expectation value](@entry_id:150961) of an observable $A$ for a system in a state represented by $|\psi\rangle$. It is given by $\langle A \rangle = \frac{\langle\psi|A|\psi\rangle}{\langle\psi|\psi\rangle}$. If we represent the same state with a different vector $|\phi\rangle = c|\psi\rangle$ where $c \in \mathbb{C} \setminus \{0\}$, the [expectation value](@entry_id:150961) remains unchanged:

$$
\langle A \rangle_\phi = \frac{\langle c\psi|A|c\psi\rangle}{\langle c\psi|c\psi\rangle} = \frac{c^*c\langle\psi|A|\psi\rangle}{c^*c\langle\psi|\psi\rangle} = \frac{|c|^2\langle\psi|A|\psi\rangle}{|c|^2\langle\psi|\psi\rangle} = \langle A \rangle_\psi
$$

This invariance means that a pure physical state corresponds to a **ray** in the Hilbert space, which is the set of all non-zero scalar multiples of a given non-zero vector: $[\psi] = \{c|\psi\rangle : c \in \mathbb{C} \setminus \{0\}\}$. By convention, we typically work with state vectors that are normalized to unity, i.e., $\langle\psi|\psi\rangle = 1$. Under this convention, any two vectors $|\psi\rangle$ and $|\phi\rangle$ represent the same state if and only if they differ by a **[global phase](@entry_id:147947) factor**, $|\phi\rangle = e^{i\theta}|\psi\rangle$ for some real $\theta$ .

This physical irrelevance of the [global phase](@entry_id:147947) is most transparent in the density [operator formalism](@entry_id:180896). A pure state $|\psi\rangle$ (assumed normalized) can be represented by a rank-one [projection operator](@entry_id:143175) $\rho = |\psi\rangle\langle\psi|$. A change in [global phase](@entry_id:147947) $|\psi'\rangle = e^{i\theta}|\psi\rangle$ leaves this operator invariant:

$$
\rho' = |\psi'\rangle\langle\psi'| = (e^{i\theta}|\psi\rangle)(\langle\psi|e^{-i\theta}) = |\psi\rangle\langle\psi| = \rho
$$

Since all physical predictions can be calculated from $\rho$, the unobservability of the [global phase](@entry_id:147947) is manifest .

#### The Superposition Principle and Statistical Mixtures

The linear vector space structure of the Hilbert space gives rise to one of the most distinctive features of quantum mechanics: the **[superposition principle](@entry_id:144649)**. If $|0\rangle$ and $|1\rangle$ are two possible states of a system, then any normalized [linear combination](@entry_id:155091) $|\psi\rangle = c_0|0\rangle + c_1|1\rangle$ (where $|c_0|^2 + |c_1|^2 = 1$) is also a valid physical state. This is a *[coherent superposition](@entry_id:170209)*.

It is crucial to distinguish a [coherent superposition](@entry_id:170209) from a **statistical mixture**, where the system is in one of a set of states $\{|\psi_k\rangle\}$ with classical probabilities $\{p_k\}$. A mixture cannot be described by a single state vector but requires a more general object: the density operator.

Consider a two-level system (a qubit) and two preparation procedures :
1.  **Pure Superposition:** The system is prepared in the state $|\psi\rangle = \cos\theta|0\rangle + e^{i\phi}\sin\theta|1\rangle$.
2.  **Statistical Mixture:** The system is prepared in the state $|0\rangle$ with probability $\cos^2\theta$ or in the state $|1\rangle$ with probability $\sin^2\theta$.

The physical difference becomes apparent when measuring an observable that can probe the "coherence" between the $|0\rangle$ and $|1\rangle$ states. Let the observable be $A = \sigma_x \cos\alpha + \sigma_y \sin\alpha$.
For the pure state, the expectation value is:
$$
\langle A \rangle_{\text{pure}} = \langle\psi|A|\psi\rangle = \sin(2\theta)\cos(\phi-\alpha)
$$
This result depends on the [relative phase](@entry_id:148120) $\phi$ between the $|0\rangle$ and $|1\rangle$ components, a hallmark of quantum interference.

For the statistical mixture, the situation is different. The system is described by the [density operator](@entry_id:138151) $\rho_{\text{mix}} = \cos^2\theta|0\rangle\langle0| + \sin^2\theta|1\rangle\langle1|$. The [expectation value](@entry_id:150961) is calculated as a weighted average:
$$
\langle A \rangle_{\text{mix}} = \mathrm{Tr}(\rho_{\text{mix}}A) = \cos^2\theta\langle0|A|0\rangle + \sin^2\theta\langle1|A|1\rangle = 0
$$
The interference term is absent because there is no definite phase relation between the components of the statistical ensemble. This operational distinction underscores the fundamental difference between [coherent superposition](@entry_id:170209) and classical uncertainty.

#### General States: The Density Operator

The concept of the statistical mixture leads to the general definition of a quantum state. The most general state of a quantum system is described by a **density operator** (or density matrix) $\rho$, which must satisfy three properties :
1.  **Hermiticity:** $\rho = \rho^\dagger$.
2.  **Positive Semidefiniteness:** $\langle\phi|\rho|\phi\rangle \ge 0$ for all vectors $|\phi\rangle \in \mathcal{H}$.
3.  **Unit Trace:** $\mathrm{Tr}(\rho) = 1$.

The set of all density operators for a given system forms a [convex set](@entry_id:268368). The [pure states](@entry_id:141688), corresponding to rank-one projectors $\rho=|\psi\rangle\langle\psi|$, are the extremal points of this set. Any mixed state can be written as a non-trivial convex combination of [pure states](@entry_id:141688), e.g., $\rho = \sum_k p_k |\psi_k\rangle\langle\psi_k|$ with $p_k > 0$ and $\sum_k p_k = 1$.

A useful measure to distinguish pure from [mixed states](@entry_id:141568) is the **purity**, defined as $\mathrm{Tr}(\rho^2)$. For any state, the purity is bounded: $\frac{1}{d} \le \mathrm{Tr}(\rho^2) \le 1$, where $d$ is the dimension of the Hilbert space.
-   $\mathrm{Tr}(\rho^2) = 1$ if and only if the state is pure (rank 1).
-   $\mathrm{Tr}(\rho^2) = 1/d$ if and only if the state is maximally mixed, $\rho = I/d$, representing complete ignorance about the system's state.

For example, a thermal Gibbs state $\rho_\beta = \exp(-\beta H)/Z$ at a finite inverse temperature $\beta > 0$ for a system with a non-degenerate Hamiltonian $H$ is always a mixed state ($\mathrm{Tr}(\rho_\beta^2)  1$). However, in the zero-temperature limit ($\beta \to \infty$), it purifies to the ground state projector, and its purity approaches 1 .

### Observables and Measurement

The second set of postulates connects the abstract state description to physical measurements. It specifies what can be measured and what the outcomes will be.

#### Postulate 2: Observables as Self-Adjoint Operators

Every measurable physical quantity, or **observable**, is associated with a **[self-adjoint operator](@entry_id:149601)** $A$ acting on the Hilbert space $\mathcal{H}$. The distinction between a [self-adjoint operator](@entry_id:149601) and a merely Hermitian (or symmetric) one is subtle but crucial, particularly for [infinite-dimensional systems](@entry_id:170904) where [unbounded operators](@entry_id:144655) like position and momentum are common .

A [symmetric operator](@entry_id:275833) $A$ is one for which $\langle\psi|A\phi\rangle = \langle A\psi|\phi\rangle$ for all vectors $|\psi\rangle, |\phi\rangle$ in its domain $\mathcal{D}(A)$. An operator is self-adjoint if it is symmetric and its domain is equal to the domain of its adjoint, $\mathcal{D}(A) = \mathcal{D}(A^\dagger)$. While symmetry is sufficient to guarantee real [expectation values](@entry_id:153208) ($\langle\psi|A|\psi\rangle \in \mathbb{R}$), it is not sufficient to guarantee a real spectrum or the existence of a complete set of eigenvectors. Only self-adjointness guarantees, via the **Spectral Theorem**, the existence of a unique [projection-valued measure](@entry_id:274834) (PVM) on the real line. This PVM is essential for defining the probabilities of all possible measurement outcomes, thereby providing a complete statistical model for the observable .

#### The Spectral Theorem and Measurement Outcomes

The **Spectral Theorem** is the mathematical cornerstone of the measurement postulate. It states that for any [self-adjoint operator](@entry_id:149601) $A$, there exists a unique **Projection-Valued Measure (PVM)**, denoted $\{E_A(\Delta)\}$, which assigns a [projection operator](@entry_id:143175) $E_A(\Delta)$ to every suitable subset $\Delta$ of the real line $\mathbb{R}$. The operator $A$ can be reconstructed from its PVM via the spectral integral:

$$
A = \int_{-\infty}^{\infty} a \, dE_A(a)
$$

The physical interpretation is that the possible outcomes of a measurement of the observable $A$ are the values in the **spectrum** of the operator $A$. The operator $E_A(\Delta)$ projects onto the subspace of states for which a measurement of $A$ is certain to yield a result within the set $\Delta$ .

#### Postulate 3: The Born Rule and Probabilities

Given the state of the system $\rho$ and an observable $A$ with its PVM $\{E_A(\Delta)\}$, the probability of obtaining a measurement outcome in the set $\Delta \subset \mathbb{R}$ is given by the **Born rule**:

$$
\mathbb{P}_A(\Delta) = \mathrm{Tr}(\rho E_A(\Delta))
$$

If the observable has a [discrete spectrum](@entry_id:150970) with eigenvalues $\{a_i\}$ and corresponding projectors $\{\Pi_i\}$, this simplifies to the probability of obtaining outcome $a_i$: $p(a_i) = \mathrm{Tr}(\rho \Pi_i)$ . The [expectation value](@entry_id:150961) of the observable is then $\langle A \rangle = \mathrm{Tr}(\rho A) = \sum_i a_i p(a_i)$.

#### Generalized Measurements: Positive Operator-Valued Measures (POVMs)

The formalism of PVMs describes ideal, sharp measurements. However, the most general type of measurement allowed by quantum mechanics is described by a **Positive Operator-Valued Measure (POVM)**. A POVM is a set of operators $\{M_i\}$ where each $M_i$ is [positive semi-definite](@entry_id:262808) ($M_i \ge 0$) and the set satisfies the [completeness relation](@entry_id:139077) $\sum_i M_i = I$. The operators $M_i$ are not required to be projectors.

The probability of obtaining outcome $i$ for a measurement described by the POVM $\{M_i\}$ on a system in state $\rho$ is:

$$
p_i = \mathrm{Tr}(\rho M_i)
$$

This generalized framework is not an ad-hoc extension but arises naturally from considering realistic measurement schemes. Any generalized measurement on a system $S$ can be modeled as a unitary interaction $U$ with an ancillary system (or environment) $E$ prepared in a known state $|e_0\rangle$, followed by a standard [projective measurement](@entry_id:151383) on the environment, described by projectors $\{\Pi_i^E\}$ . The probability of obtaining outcome $i$ on the environment induces an effective measurement on the system, whose elements are given by:

$$
M_i = \mathrm{Tr}_E \left[ (I_S \otimes |e_0\rangle\langle e_0|) U^\dagger (I_S \otimes \Pi_i^E) U \right] = \langle e_0| U^\dagger (I_S \otimes \Pi_i^E) U |e_0 \rangle
$$

This construction, known as **Naimark's dilation theorem**, shows that POVMs are the necessary and sufficient description for all physically realizable quantum measurements. Any process of an open quantum system, such as pre-measurement noise, will generally transform an ideal [projective measurement](@entry_id:151383) into a generalized POVM measurement from the perspective of an observer measuring the system .

#### Postulate 4: The State Update Rule

The final piece of the measurement puzzle concerns the state of the system *after* a measurement has occurred. If a measurement of observable $A$ on a system in state $\rho$ yields the outcome $a$ (corresponding to a non-degenerate projector $\Pi_a$), the state of the system immediately after the measurement is updated according to **Lüders' rule**:

$$
\rho \mapsto \rho'_a = \frac{\Pi_a \rho \Pi_a}{\mathrm{Tr}(\rho \Pi_a)}
$$

This rule ensures that an immediate repetition of the measurement will yield the same outcome $a$ with probability 1. Lüders' rule can be derived from a principle of **minimal disturbance** . It is the unique update rule that, upon obtaining outcome $a$, correctly predicts the post-measurement statistics for any other observable $B$ that is compatible with the measurement (i.e., $[B, \Pi_a] = 0$) by preserving all pre-existing information about $B$. In cases of degeneracy, this rule is less disruptive than the older von Neumann [projection postulate](@entry_id:145685), as it preserves coherences within the measured [eigenspace](@entry_id:150590).

### Dynamics of Quantum Systems

Having established the static description of states and measurements, we now turn to the postulates governing their evolution in time.

#### Postulate 5: Time Evolution of Closed Systems

The dynamics of a closed quantum system (one that does not interact with any external environment) is described by a [unitary transformation](@entry_id:152599). This is formalized in the fifth postulate: The evolution of a closed system is described by a **strongly continuous one-parameter [unitary group](@entry_id:138602)** $\{U(t)\}_{t \in \mathbb{R}}$. This means that if the state of the system at time $t_0$ is $|\psi(t_0)\rangle$, the state at time $t$ is $|\psi(t)\rangle = U(t-t_0)|\psi(t_0)\rangle$. The unitary nature of $U(t)$ ensures that probabilities are conserved (i.e., the norm of the state vector is preserved), and the group property $U(t+s) = U(t)U(s)$ reflects time-translation homogeneity.

**Stone's Theorem on [one-parameter unitary groups](@entry_id:270459)** provides the crucial link between this kinematic description and the system's energy. The theorem states that for any such group, there exists a unique [self-adjoint operator](@entry_id:149601) $H$, the **Hamiltonian**, which serves as its [infinitesimal generator](@entry_id:270424) :

$$
U(t) = e^{-iHt/\hbar}
$$

The differential form of this evolution is the celebrated **time-dependent Schrödinger equation**:
$$
i\hbar \frac{d}{dt}|\psi(t)\rangle = H|\psi(t)\rangle
$$
The requirement that the Hamiltonian be self-adjoint is paramount, as it guarantees a unique, probability-preserving evolution for all time. For physical systems of interest, such as molecules described by kinetic and Coulomb potential terms, powerful mathematical results like the **Kato-Rellich theorem** are used to prove that the corresponding Hamiltonians are indeed self-adjoint, thus ensuring the physical relevance of this postulate .

#### Dynamics of Open Systems: The Markovian Postulate

Real-world systems are rarely truly closed; they interact with their environment. The study of such **[open quantum systems](@entry_id:138632)** is central to [quantum thermodynamics](@entry_id:140152) and understanding phenomena like decoherence. While the total system-plus-environment complex evolves unitarily, the dynamics of the system alone is generally non-unitary.

In the important case where the environment is large and its memory of the system is short-lived (the **Markovian approximation**), the system's evolution is described by a **[quantum dynamical semigroup](@entry_id:1130394)**. This is a strongly continuous one-parameter [semigroup](@entry_id:153860) of Completely Positive and Trace-Preserving (CPTP) maps $\{\mathcal{T}_t\}_{t \ge 0}$ . The evolution of the density operator is given by $\rho(t) = \mathcal{T}_t(\rho(0))$. In [differential form](@entry_id:174025), this is the master equation $\frac{d\rho}{dt} = \mathcal{L}(\rho)$, where $\mathcal{L}$ is the generator of the [semigroup](@entry_id:153860).

The **Gorini-Kossakowski-Sudarshan-Lindblad (GKSL) theorem** gives the general form that any such generator $\mathcal{L}$ must take to ensure the dynamics is CPTP:
$$
\mathcal{L}(\rho) = -i[H, \rho] + \sum_k \gamma_k \left( L_k \rho L_k^\dagger - \frac{1}{2}\{L_k^\dagger L_k, \rho\} \right)
$$
Here, $H$ is a Hermitian operator representing the unitary part of the dynamics, the $L_k$ are arbitrary system operators known as **Lindblad operators** or jump operators that model dissipative processes, and the $\gamma_k \ge 0$ are rates for these processes. This equation, known as the Lindblad or GKSL master equation, is a fundamental tool for describing decoherence, [thermalization](@entry_id:142388), and other non-unitary phenomena in a manner consistent with the postulates of quantum mechanics.

### Composite and Many-Body Systems

The postulates must also account for systems composed of multiple parts and collections of [identical particles](@entry_id:153194).

#### Postulate 6: Composite Systems and Entanglement

When two or more systems are considered together as a single composite system, the state space of the composite system is the **[tensor product](@entry_id:140694)** of the state spaces of the individual subsystems. For two systems $A$ and $B$ with Hilbert spaces $\mathcal{H}_A$ and $\mathcal{H}_B$, the composite system's space is $\mathcal{H}_{AB} = \mathcal{H}_A \otimes \mathcal{H}_B$ .

A [pure state](@entry_id:138657) of the composite system is called a **product state** if it can be written as $|\psi\rangle = |\phi\rangle_A \otimes |\chi\rangle_B$, where $|\phi\rangle_A \in \mathcal{H}_A$ and $|\chi\rangle_B \in \mathcal{H}_B$. States that cannot be written in this form are called **[entangled states](@entry_id:152310)**. Entanglement represents correlations between quantum systems that have no classical analogue.

The **Schmidt decomposition** provides a canonical way to represent any [pure state](@entry_id:138657) $|\psi\rangle$ of a bipartite system:
$$
|\psi\rangle = \sum_{k=1}^r \sqrt{\lambda_k} |u_k\rangle_A \otimes |v_k\rangle_B
$$
Here, $\{|u_k\rangle_A\}$ and $\{|v_k\rangle_B\}$ are [orthonormal sets](@entry_id:155086) of vectors in $\mathcal{H}_A$ and $\mathcal{H}_B$ respectively, and the Schmidt coefficients $\lambda_k$ are positive real numbers summing to 1.
- The number of terms, $r$, is the **Schmidt rank**. A state is a product state if and only if $r=1$; it is entangled if $r1$.
- The Schmidt coefficients $\{\lambda_k\}$ are the eigenvalues of the reduced density operators $\rho_A = \mathrm{Tr}_B(|\psi\rangle\langle\psi|)$ and $\rho_B = \mathrm{Tr}_A(|\psi\rangle\langle\psi|)$. A pure bipartite state is a product state if and only if its reduced states are pure .
- The amount of entanglement can be quantified by the **entropy of entanglement**, $S(\rho_A) = S(\rho_B) = -\sum_k \lambda_k \ln \lambda_k$, which is zero for product states and positive for [entangled states](@entry_id:152310).
- Entanglement is a non-local property: it is invariant under [local unitary operations](@entry_id:198146) $U_A \otimes V_B$. An [entangled state](@entry_id:142916) cannot be created from or transformed into a product state by local operations alone .
A key property relating the global state to its parts is that if a subsystem's state is pure (e.g., $\rho_A = |\phi\rangle\langle\phi|$), then the global state must be a product state of the form $\rho_{AB} = \rho_A \otimes \rho_B$ .

#### Postulate 7: Identical Particles

The final postulate concerns systems containing multiple [identical particles](@entry_id:153194), such as electrons in a molecule. The **[symmetrization postulate](@entry_id:148962)** states that if a system contains [identical particles](@entry_id:153194), the state vector must transform in a specific way under the exchange of any two particles.
- For identical **bosons** (particles with integer spin), the state vector must be symmetric: $\hat{P}_{ij}|\psi\rangle = +|\psi\rangle$.
- For identical **fermions** (particles with [half-integer spin](@entry_id:148826)), the state vector must be antisymmetric: $\hat{P}_{ij}|\psi\rangle = -|\psi\rangle$.

Electrons are fermions. Therefore, any valid [multi-electron wavefunction](@entry_id:156344) must be antisymmetric with respect to the exchange of any two electrons' labels (both space and spin coordinates) . This requirement, often called the **Pauli exclusion principle**, has profound consequences. For a two-electron system, a valid state $\Psi(\mathbf{x}_1, \mathbf{x}_2)$ must be constructed from a product of a spatial part and a spin part such that the overall symmetry is antisymmetric. This leaves two possibilities:
1.  **Antisymmetric Spatial Part $\times$ Symmetric Spin Part (Triplet State)**: e.g., $\frac{1}{\sqrt{2}}[\phi_a(\mathbf{r}_1)\phi_b(\mathbf{r}_2) - \phi_b(\mathbf{r}_1)\phi_a(\mathbf{r}_2)] \times [\alpha(1)\alpha(2)]$.
2.  **Symmetric Spatial Part $\times$ Antisymmetric Spin Part (Singlet State)**: e.g., $\frac{1}{\sqrt{2}}[\phi_a(\mathbf{r}_1)\phi_b(\mathbf{r}_2) + \phi_b(\mathbf{r}_1)\phi_a(\mathbf{r}_2)] \times \frac{1}{\sqrt{2}}[\alpha(1)\beta(2) - \beta(1)\alpha(2)]$.

Notably, if two electrons occupy the same spatial orbital ($\phi_a = \phi_b$), the spatial part $\phi_a(\mathbf{r}_1)\phi_a(\mathbf{r}_2)$ is necessarily symmetric. To satisfy the [antisymmetry principle](@entry_id:137331), the spin part must be antisymmetric (the [singlet state](@entry_id:154728)). It is impossible to form a valid state where two electrons have both the same spatial orbital and the same spin state, as this would result in an overall [symmetric wavefunction](@entry_id:153601) .

### Constraints on the Framework: Superselection Rules

While the [superposition principle](@entry_id:144649) is a cornerstone of quantum mechanics, its application is not without limits. The existence of **[superselection rules](@entry_id:203866)** constrains the set of physically realizable states and measurable observables .

A [superselection rule](@entry_id:152289) arises when there exists a [self-adjoint operator](@entry_id:149601) $\hat{Q}$ (often representing a fundamental charge like electric charge or [baryon number](@entry_id:157941)) that commutes with *all* [physical observables](@entry_id:154692) $\hat{A}$ in the theory: $[\hat{A}, \hat{Q}] = 0$ for all $\hat{A}$.

This has a critical consequence: the Hilbert space decomposes into a [direct sum](@entry_id:156782) of [eigenspaces](@entry_id:147356) of $\hat{Q}$, $\mathcal{H} = \bigoplus_q \mathcal{H}_q$, called **superselection sectors**. Because every observable commutes with $\hat{Q}$, they also commute with the projectors $\hat{P}_q$ onto these sectors. This means no physical observable can cause a transition between different sectors; they are [invariant subspaces](@entry_id:152829) under the action of all [observables](@entry_id:267133).

The operational consequence is that no measurement can distinguish a coherent [superposition of states](@entry_id:273993) from different sectors, $|\psi\rangle = \sum_q c_q |\psi_q\rangle$ (with $|\psi_q\rangle \in \mathcal{H}_q$), from a classical statistical mixture represented by the density operator $\rho_{\text{mix}} = \sum_q |c_q|^2 |\psi_q\rangle\langle\psi_q|$. The [expectation value](@entry_id:150961) of any observable $\hat{A}$ depends only on the squared moduli $|c_q|^2$ and not on the relative phases between the components from different sectors.
$$
\langle\psi|\hat{A}|\psi\rangle = \sum_q |c_q|^2 \langle\psi_q|\hat{A}|\psi_q\rangle = \mathrm{Tr}(\rho_{\text{mix}}\hat{A})
$$
These relative phases are unobservable, rendering coherent superpositions across different sectors physically meaningless. In this context, the [superposition principle](@entry_id:144649) is restricted: only superpositions of states *within* a single superselection sector are physically distinct from mixtures. This phenomenon is distinct from the unobservability of an overall [global phase](@entry_id:147947), which is a universal feature of the [quantum state postulate](@entry_id:150109) itself .