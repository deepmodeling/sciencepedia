## Introduction
Quantum mechanics provides the fundamental laws governing matter at the atomic and subatomic levels, making it the bedrock of modern physics, chemistry, and materials science. While its principles are often introduced in abstract terms, the true power of quantum theory is unlocked through practical methods that can model and predict the behavior of complex, real-world systems. This article bridges the gap between abstract quantum theory and its computational application, particularly for graduate students entering the field of multiscale modeling. It provides a comprehensive introduction to the essential toolkit of quantum mechanical methods required to simulate molecules, materials, and their interactions.

The journey begins in the first chapter, **Principles and Mechanisms**, where we will formalize the mathematical structure of quantum mechanics, covering state vectors, operators, quantum dynamics, and the cornerstone approximation methods for [stationary states](@entry_id:137260) like the variational principle, perturbation theory, and Density Functional Theory (DFT). The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the utility of these methods by exploring their application in [computational chemistry](@entry_id:143039) and materials science. We will see how forces are calculated, how molecular dynamics are simulated, and how quantum principles explain the properties of solids. Finally, the third chapter, **Hands-On Practices**, provides a set of targeted problems designed to solidify your understanding of key concepts like [coherent states](@entry_id:154533), density matrices, and level crossings, preparing you to apply these theories in your own research.

## Principles and Mechanisms

In this chapter, we transition from the conceptual introduction of quantum mechanics to its formal mathematical structure. We will establish the core principles governing the description of quantum states, the nature of [physical observables](@entry_id:154692), the mechanisms of time evolution, and the powerful approximation methods that enable the application of quantum theory to complex systems encountered in multiscale modeling.

### The Description of Quantum States

At the heart of quantum mechanics lies the concept of the **state**, which encapsulates all possible information about a physical system at a given instant. Unlike classical mechanics, where a state is a point in phase space (defined by positions and momenta), a quantum state is a more abstract mathematical object.

#### Pure States: Hilbert Space and State Vectors

The first postulate of quantum mechanics asserts that a pure quantum state is represented by a vector in a complex **Hilbert space**, denoted $\mathcal{H}$. For a single non-relativistic particle moving in three dimensions, this space is typically the set of all square-integrable, complex-valued functions on $\mathbb{R}^3$, denoted $L^2(\mathbb{R}^3)$. A "vector" in this context is a function $\psi(\mathbf{r})$, often called the **[wave function](@entry_id:148272)** or **state vector**.

The requirement that $\psi(\mathbf{r})$ be an element of $L^2(\mathbb{R}^3)$ means that the integral of its squared modulus over all space must be finite:
$$
\int_{\mathbb{R}^3} |\psi(\mathbf{r})|^2 \, d^3\mathbf{r} \lt \infty
$$
This square-[integrability](@entry_id:142415) is not merely a mathematical convenience; it is essential for the probabilistic interpretation of the theory. According to the **Born rule**, the quantity $|\psi(\mathbf{r})|^2$ represents the probability density of finding the particle at position $\mathbf{r}$. For this interpretation to be consistent, the total probability of finding the particle somewhere in the universe must be unity. This leads to the [normalization condition](@entry_id:156486):
$$
\int_{\mathbb{R}^3} |\psi(\mathbf{r})|^2 \, d^3\mathbf{r} = 1
$$
A state vector that satisfies this condition is said to be **normalized**. This probabilistic interpretation is a cornerstone of quantum mechanics, providing the direct link between the mathematical formalism and experimental measurement .

While the $L^2(\mathbb{R}^3)$ framework is essential for describing localized particles (so-called **[bound states](@entry_id:136502)**), it is important to acknowledge that certain idealized states used in theoretical physics, such as the plane waves $\psi(\mathbf{r}) \propto \exp(i\mathbf{k}\cdot\mathbf{r})$ that describe particles with definite momentum in [scattering theory](@entry_id:143476), are not themselves square-integrable. These are not strictly elements of the Hilbert space but are indispensable theoretical tools that can be handled rigorously within a more advanced mathematical framework known as a rigged Hilbert space.

#### The Physical State as a Ray

A crucial subtlety in the state vector formalism is that all physically measurable quantities, such as probabilities and [expectation values](@entry_id:153208) of observables, are invariant under the multiplication of the state vector by a [global phase](@entry_id:147947) factor, $e^{i\phi}$, where $\phi$ is any real number. If we consider two state vectors $\psi$ and $\psi' = e^{i\phi}\psi$, the probability density remains unchanged:
$$
|\psi'(\mathbf{r})|^2 = |e^{i\phi}\psi(\mathbf{r})|^2 = |e^{i\phi}|^2 |\psi(\mathbf{r})|^2 = 1 \cdot |\psi(\mathbf{r})|^2 = |\psi(\mathbf{r})|^2
$$
Similarly, as we will see, the expectation value of any observable also remains unchanged. Because all physical predictions are identical for any vector in the set $\{e^{i\phi}\psi : \phi \in \mathbb{R}\}$, these vectors are considered physically equivalent. This [equivalence class](@entry_id:140585) is known as a **ray** in the Hilbert space. Therefore, a pure quantum state is more precisely represented by a ray rather than a single vector. For example, the state vectors $\psi$ and $-\psi$ (which corresponds to a phase shift of $\phi=\pi$) represent the same physical state .

This invariance applies only to a **[global phase](@entry_id:147947)**. In a **superposition** of states, such as $|\Psi\rangle = c_1 |\psi_1\rangle + c_2 |\psi_2\rangle$, the **[relative phase](@entry_id:148120)** between the complex coefficients $c_1$ and $c_2$ is physically significant. A change in the [relative phase](@entry_id:148120) fundamentally alters the resulting state, leading to a different ray in the Hilbert space and observable consequences due to changes in interference terms. For example, the states $|\psi_1\rangle + |\psi_2\rangle$ and $|\psi_1\rangle - |\psi_2\rangle$ are physically distinct .

#### Mixed States and the Density Operator

The state vector formalism is sufficient for describing **[pure states](@entry_id:141688)**, where the system's state is known with maximum possible certainty. However, in many realistic scenarios, particularly in multiscale modeling where a quantum subsystem is coupled to a large environment or when preparation protocols are imperfect, the system may be in a [statistical ensemble](@entry_id:145292) of different [pure states](@entry_id:141688). Such a state is called a **[mixed state](@entry_id:147011)**.

A [mixed state](@entry_id:147011) cannot be described by a single state vector. Instead, we use the **[density operator](@entry_id:138151)** (or density matrix), denoted by $\rho$. For an ensemble where the system is in the pure state $|\psi_i\rangle$ with probability $p_i$, the [density operator](@entry_id:138151) is defined as the weighted sum of the [projection operators](@entry_id:154142) for each state:
$$
\rho = \sum_{i} p_i |\psi_i\rangle\langle\psi_i|
$$
The density [operator formalism](@entry_id:180896) generalizes the state vector description and has several fundamental properties :
1.  **Hermiticity**: $\rho = \rho^{\dagger}$. This ensures that physical predictions are real.
2.  **Unit Trace**: $\operatorname{Tr}(\rho) = 1$. This is the generalization of the [normalization condition](@entry_id:156486) for state vectors.
3.  **Positive Semidefiniteness**: $\rho \ge 0$. This means all its eigenvalues are non-negative, consistent with their interpretation as probabilities.

The power of the [density operator](@entry_id:138151) is that it provides a unified framework for both pure and [mixed states](@entry_id:141568). A pure state $|\psi\rangle$ can be represented by the density operator $\rho = |\psi\rangle\langle\psi|$, which is simply a projector onto that state.

A simple, powerful tool for distinguishing between pure and [mixed states](@entry_id:141568) is the **purity**, defined as $\gamma = \operatorname{Tr}(\rho^2)$. By diagonalizing the [density operator](@entry_id:138151), one can show that a state is pure if and only if its purity is exactly 1. For any mixed state, the purity is strictly less than 1 ($\gamma \lt 1$). For a system in a $d$-dimensional Hilbert space, the purity is bounded by $\frac{1}{d} \le \gamma \le 1$. A value of $\gamma = 1/d$ corresponds to a maximally mixed state, where the system has an equal probability of being in any of the [basis states](@entry_id:152463) .

### Observables, Measurement, and Uncertainty

Having established the representation of quantum states, we now turn to the question of how physical properties are represented and extracted from the state.

#### Observables and the Spectral Theorem

The second postulate of quantum mechanics states that every physically measurable quantity (an **observable**) is associated with a **self-adjoint** (Hermitian) operator acting on the Hilbert space of the system. For example, the position of a particle is associated with the operator $\hat{x}$, and its momentum with the operator $\hat{p}$.

The connection between these operators and experimental outcomes is provided by the **[spectral theorem](@entry_id:136620)**, a cornerstone of [functional analysis](@entry_id:146220) and quantum theory. For any [self-adjoint operator](@entry_id:149601) $A$, the theorem guarantees the existence of a unique **[projection-valued measure](@entry_id:274834) (PVM)**, denoted $E$, defined on the real line. This PVM assigns an [orthogonal projection](@entry_id:144168) operator $E(\Delta)$ to each (Borel) subset $\Delta \subset \mathbb{R}$. The [spectral theorem](@entry_id:136620) allows us to express the operator $A$ as an integral over its eigenvalues weighted by these projectors :
$$
A = \int_{-\infty}^{\infty} \lambda \, dE_{\lambda}
$$
Here, $\lambda$ represents the possible values the observable $A$ can take. The set of all such values forms the **spectrum** of the operator.

The profound physical meaning of the [spectral theorem](@entry_id:136620) is revealed in the context of measurement:
1.  **Possible Measurement Outcomes**: The only possible results of a measurement of the observable $A$ are the values $\lambda$ in the spectrum of the operator $\hat{A}$.
2.  **Probabilities of Outcomes**: If the system is in a normalized state $|\psi\rangle$, the probability that a measurement of $A$ yields a result within the range $\Delta$ is given by the [expectation value](@entry_id:150961) of the corresponding [projection operator](@entry_id:143175):
    $$
    \operatorname{Prob}(A \in \Delta) = \langle \psi | E(\Delta) | \psi \rangle = \| E(\Delta) |\psi\rangle \|^2
    $$
3.  **State Collapse**: Immediately after a measurement of $A$ yields a result $\lambda$, the system's state is projected into the [eigenspace](@entry_id:150590) associated with that eigenvalue.

For a mixed state described by the [density operator](@entry_id:138151) $\rho$, the probability rule generalizes to $\operatorname{Prob}(A \in \Delta) = \operatorname{Tr}(\rho E(\Delta))$. The **[expectation value](@entry_id:150961)** (or average value) of an observable $A$ in a state $\rho$ is given by:
$$
\langle A \rangle = \operatorname{Tr}(\rho A)
$$
For a [pure state](@entry_id:138657) $|\psi\rangle$, this simplifies to the familiar expression $\langle A \rangle = \langle \psi | A | \psi \rangle$.

#### Example: Spin-1/2 and the Bloch Sphere

The formalism of states and [observables](@entry_id:267133) can be beautifully illustrated with the simplest non-trivial quantum system: a **[two-level system](@entry_id:138452)**, such as the spin of an electron, also known as a **qubit**. The Hilbert space is two-dimensional, spanned by the [basis states](@entry_id:152463) $|0\rangle$ (spin-up) and $|1\rangle$ (spin-down).

A general [pure state](@entry_id:138657) can be written as a superposition $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$, with $|\alpha|^2 + |\beta|^2 = 1$. It is conventional to parameterize this state using two angles, $\theta$ and $\phi$:
$$
|\psi\rangle = \cos\left(\frac{\theta}{2}\right)|0\rangle + e^{i\phi}\sin\left(\frac{\theta}{2}\right)|1\rangle
$$
The observables corresponding to the spin components along the $x, y,$ and $z$ axes are given by the **Pauli operators** (up to a factor of $\hbar/2$), which in the $\{|0\rangle, |1\rangle\}$ basis are represented by the Pauli matrices:
$$
\sigma_x = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}, \quad \sigma_y = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix}, \quad \sigma_z = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}
$$
By calculating the [expectation values](@entry_id:153208) of these operators for the general state $|\psi\rangle$, we obtain the components of the **Bloch vector**, a real three-dimensional vector that provides a geometric representation of the pure state :
$$
\langle\sigma_x\rangle = \langle\psi|\sigma_x|\psi\rangle = \sin(\theta)\cos(\phi)
$$
$$
\langle\sigma_y\rangle = \langle\psi|\sigma_y|\psi\rangle = \sin(\theta)\sin(\phi)
$$
$$
\langle\sigma_z\rangle = \langle\psi|\sigma_z|\psi\rangle = \cos(\theta)
$$
This vector $(\langle\sigma_x\rangle, \langle\sigma_y\rangle, \langle\sigma_z\rangle)$ is a point on the surface of a unit sphere known as the **Bloch sphere**. This visualization provides a powerful one-to-one correspondence between every [pure state](@entry_id:138657) of a qubit and a point on the sphere's surface. Mixed states, in this picture, correspond to points inside the sphere.

#### Incompatible Observables and the Uncertainty Principle

A revolutionary departure from classical physics is the existence of **[incompatible observables](@entry_id:156311)**: pairs of properties that cannot be simultaneously known with arbitrary precision. The compatibility of two [observables](@entry_id:267133), $A$ and $B$, is determined by their **commutator**, defined as $[\hat{A}, \hat{B}] = \hat{A}\hat{B} - \hat{B}\hat{A}$. Two [observables](@entry_id:267133) are compatible if and only if their operators commute, i.e., $[\hat{A}, \hat{B}] = 0$.

If two operators do not commute, $[\hat{A}, \hat{B}] \neq 0$, it is impossible to find a complete set of states that are simultaneously [eigenstates](@entry_id:149904) of both. This implies that a measurement of one observable will necessarily disturb the value of the other.

A classic example is provided by the spin components. An explicit calculation of the commutator for the [spin operators](@entry_id:155419) $S_j = (\hbar/2)\sigma_j$ yields the fundamental [angular momentum commutation relations](@entry_id:150953) :
$$
[S_x, S_y] = i\hbar S_z
$$
(and cyclic [permutations](@entry_id:147130) thereof). Since $[S_x, S_y] \neq 0$, the $x$- and $y$-components of spin are [incompatible observables](@entry_id:156311). If a particle is prepared in an eigenstate of $S_x$ (i.e., its spin along $x$ is definite), it is not in an eigenstate of $S_y$. A subsequent measurement of $S_y$ will yield a probabilistic outcome and will alter the state, destroying the definite value of $S_x$.

This trade-off in precision is quantified by the **Heisenberg-Robertson uncertainty relation**:
$$
(\Delta A)^2 (\Delta B)^2 \ge \frac{1}{4} |\langle[\hat{A}, \hat{B}]\rangle|^2
$$
where $(\Delta A)^2 = \langle(\hat{A} - \langle\hat{A}\rangle)^2\rangle$ is the variance of the observable $A$. For position and momentum, with the [canonical commutation relation](@entry_id:150454) $[\hat{x}, \hat{p}] = i\hbar$, this becomes the famous **Heisenberg uncertainty principle**:
$$
\Delta x \Delta p \ge \frac{\hbar}{2}
$$
It is possible to construct states that saturate this inequality, known as **minimum uncertainty states**. For the position-momentum pair, these states are described by Gaussian [wave packets](@entry_id:154698). A Gaussian wave packet with mean position $x_0$, mean momentum $p_0$, and spatial width $\sigma$ takes the form :
$$
\psi(x) \propto \exp\left( -\frac{(x-x_0)^2}{4\sigma^2} + \frac{ip_0x}{\hbar} \right)
$$
For this state, the position uncertainty is $\Delta x = \sigma$ and the momentum uncertainty is $\Delta p = \hbar/(2\sigma)$, exactly satisfying the bound $\Delta x \Delta p = \hbar/2$. These states represent the most "classical-like" quantum states, having simultaneously localized position and momentum to the maximum degree allowed by nature.

### Quantum Dynamics

The principles discussed so far describe the static properties of a quantum system. The evolution of these states in time is governed by the **time-dependent Schrödinger equation (TDSE)**:
$$
i\hbar \frac{\partial}{\partial t} |\psi(t)\rangle = \hat{H} |\psi(t)\rangle
$$
Here, $\hat{H}$ is the Hamiltonian operator of the system, which corresponds to its total energy. The TDSE dictates that the Hamiltonian is the **generator of time translations**.

For a system with a time-independent Hamiltonian, the TDSE can be formally solved. The state at time $t$ is related to the initial state $|\psi(0)\rangle$ by a linear operator known as the **[time-evolution operator](@entry_id:186274)**, $U(t)$:
$$
|\psi(t)\rangle = U(t) |\psi(0)\rangle
$$
By substituting this into the TDSE, we find that $U(t)$ must satisfy the operator differential equation $i\hbar \frac{d}{dt}U(t) = \hat{H}U(t)$ with the initial condition $U(0) = I$ (the [identity operator](@entry_id:204623)). The solution is the [operator exponential](@entry_id:198199):
$$
U(t) = \exp\left(-\frac{i\hat{H}t}{\hbar}\right)
$$
The [time-evolution operator](@entry_id:186274) has two crucial properties :
1.  **Unitarity**: $U(t)$ is a [unitary operator](@entry_id:155165), meaning $U(t)^{\dagger}U(t) = U(t)U(t)^{\dagger} = I$. This can be seen from $U(t)^{\dagger} = \exp(i\hat{H}^{\dagger}t/\hbar) = \exp(i\hat{H}t/\hbar) = U(-t)$. Unitarity ensures that the norm of the state vector is conserved over time, so that a normalized state remains normalized. Physically, this means total probability is conserved.
2.  **Group Property**: $U(t_1)U(t_2) = U(t_1+t_2)$. This means that evolving the system for a time $t_2$ and then for a time $t_1$ is equivalent to evolving it for the total time $t_1+t_2$.

If the [eigenstates](@entry_id:149904) $|n\rangle$ and eigenvalues $E_n$ of the Hamiltonian are known (i.e., $\hat{H}|n\rangle = E_n|n\rangle$), the action of $U(t)$ can be computed explicitly using the [spectral theorem](@entry_id:136620). For any function $f(\hat{H})$, its action is defined by $f(\hat{H}) = \sum_n f(E_n) |n\rangle\langle n|$. Applying this to the [operator exponential](@entry_id:198199), we get:
$$
U(t) = \sum_{n} \exp\left(-\frac{iE_n t}{\hbar}\right) |n\rangle\langle n|
$$
This expression beautifully shows how a state evolves: an arbitrary initial state $|\psi(0)\rangle = \sum_n c_n |n\rangle$ evolves into $|\psi(t)\rangle = \sum_n c_n e^{-iE_n t/\hbar} |n\rangle$. Each energy [eigenstate](@entry_id:202009) component simply acquires a phase factor that oscillates at a frequency proportional to its energy .

### Methods for Stationary States

For many applications in chemistry, materials science, and multiscale modeling, the primary goal is to find the [stationary states](@entry_id:137260) of a system—the [eigenstates](@entry_id:149904) of the Hamiltonian, particularly the **ground state** (the state of lowest energy). This is governed by the **time-independent Schrödinger equation (TISE)**, $\hat{H}|\psi\rangle = E|\psi\rangle$. Except for the simplest model systems, the TISE is intractable to solve exactly. Therefore, a significant part of applied quantum mechanics is dedicated to developing and using robust approximation methods.

#### The Variational Principle

The **variational principle** provides a powerful and versatile method for estimating the [ground-state energy](@entry_id:263704) of a system. It states that for any normalized trial [wave function](@entry_id:148272) $|\psi\rangle$ that is a candidate for the ground state, the [expectation value](@entry_id:150961) of the energy is an upper bound to the true ground-state energy, $E_0$:
$$
E_0 \le \langle \psi | \hat{H} | \psi \rangle
$$
The proof follows directly from expanding the trial state $|\psi\rangle$ in the true energy [eigenbasis](@entry_id:151409) $|\psi_n\rangle$ of $\hat{H}$. The equality holds if and only if the trial state $|\psi\rangle$ is identical to the true ground state $|\psi_0\rangle$ (assuming the ground state is non-degenerate) .

In practice, one chooses a physically motivated family of trial [wave functions](@entry_id:201714), $|\psi(\alpha)\rangle$, that depends on one or more parameters $\alpha$. One then calculates the variational energy $E(\alpha) = \langle \psi(\alpha) | \hat{H} | \psi(\alpha) \rangle$ and minimizes this function with respect to the parameters. The resulting minimum energy, $E_{min}$, provides the best possible estimate for $E_0$ within that family of [trial functions](@entry_id:756165). For example, one could use a Gaussian function to estimate the [ground state energy](@entry_id:146823) of the hydrogen atom. While the true ground state is an [exponential function](@entry_id:161417), the [variational method](@entry_id:140454) with a Gaussian [trial function](@entry_id:173682) still provides a surprisingly reasonable (though not exact) upper bound on the energy .

#### Perturbation Theory

When the Hamiltonian of interest, $\hat{H}$, can be expressed as a sum of a solvable Hamiltonian, $\hat{H}_0$, and a small perturbation, $\hat{V}$ (i.e., $\hat{H} = \hat{H}_0 + \lambda\hat{V}$, where $\lambda$ is a small parameter), **[perturbation theory](@entry_id:138766)** can be used to systematically approximate the [eigenvalues and eigenstates](@entry_id:149417) of $\hat{H}$.

A particularly important and common case is when the energy level $E^{(0)}$ of the unperturbed system is **degenerate**, meaning multiple [linearly independent](@entry_id:148207) [eigenstates](@entry_id:149904) share the same energy. In this scenario, standard [non-degenerate perturbation theory](@entry_id:153724) fails. **Degenerate [perturbation theory](@entry_id:138766)** provides the correct procedure. The key insight is that the perturbation "lifts" the degeneracy by selecting specific [linear combinations](@entry_id:154743) of the unperturbed states as the correct zeroth-order approximations to the new [eigenstates](@entry_id:149904).

The first-order corrections to the energy, $E^{(1)}$, are found by solving an [eigenvalue problem](@entry_id:143898) restricted to the degenerate subspace. One must construct the matrix of the perturbation operator, $\mathbf{V}$, with elements $V_{ab} = \langle \phi_a | \hat{V} | \phi_b \rangle$, where $\{|\phi_a\rangle\}$ is an [orthonormal basis](@entry_id:147779) for the degenerate subspace. The eigenvalues of this matrix are the first-order energy corrections .

A classic application of this method is the **linear Stark effect**, which describes the splitting of [atomic energy levels](@entry_id:148255) in a [uniform electric field](@entry_id:264305). For the hydrogen atom, the $n=2$ level is four-fold degenerate (composed of the $|2s\rangle$, $|2p_0\rangle$, $|2p_{+1}\rangle$, and $|2p_{-1}\rangle$ states). Applying an electric field $\mathcal{E}$ along the $z$-axis introduces a perturbation $\hat{V} = e\mathcal{E}z$. Diagonalizing this perturbation in the $n=2$ subspace reveals that the degeneracy is partially lifted, splitting the level into three distinct energies, providing a clear experimental signature .

#### Density Functional Theory

For systems with many interacting electrons, such as atoms, molecules, and solids, the dimensionality of the [wave function](@entry_id:148272) grows exponentially, making [wave function](@entry_id:148272)-based methods computationally prohibitive. **Density Functional Theory (DFT)** offers a revolutionary alternative.

The foundation of DFT lies in the **Hohenberg-Kohn theorems**, which prove that the ground-state electron density, $n(\mathbf{r})$, a function of only three spatial coordinates, uniquely determines the external potential and therefore all properties of the system, including the total energy. This establishes the energy as a functional of the density, $E[n]$.

The practical implementation of DFT is achieved through the **Kohn-Sham construction**. This ingenious approach replaces the problem of interacting electrons with a fictitious problem of non-interacting electrons moving in an effective potential, $V_{\text{eff}}[n](\mathbf{r})$, designed such that the ground-state density of this auxiliary system is identical to that of the real, interacting system. The total [energy functional](@entry_id:170311) is written as:
$$
E[n] = T_s[n] + \int v_{\text{ext}}(\mathbf{r}) n(\mathbf{r}) \, d\mathbf{r} + E_H[n] + E_{xc}[n]
$$
Here, $T_s[n]$ is the kinetic energy of the non-interacting reference system, $E_H[n]$ is the classical electrostatic (Hartree) energy of the electron cloud repelling itself, and $E_{xc}[n]$ is the **exchange-correlation functional**, which contains all the complex many-body quantum effects.

Applying the [variational principle](@entry_id:145218) to this [energy functional](@entry_id:170311) with respect to the single-particle orbitals $\{\phi_i\}$ that constitute the density ($n(\mathbf{r}) = \sum_i f_i |\phi_i(\mathbf{r})|^2$) leads to a set of single-particle [eigenvalue equations](@entry_id:192306) known as the **Kohn-Sham equations** :
$$
\left[ -\frac{1}{2}\nabla^2 + V_{\text{eff}}[n](\mathbf{r}) \right] \phi_i(\mathbf{r}) = \varepsilon_i \phi_i(\mathbf{r})
$$
The [effective potential](@entry_id:142581) is given by:
$$
V_{\text{eff}}[n](\mathbf{r}) = v_{\text{ext}}(\mathbf{r}) + \int \frac{n(\mathbf{r}')}{|\mathbf{r}-\mathbf{r}'|} \, d\mathbf{r}' + \frac{\delta E_{xc}[n]}{\delta n(\mathbf{r})}
$$
Since the effective potential depends on the density, which in turn depends on the orbitals that are the solutions to the equations, they must be solved iteratively. This process is called the **Self-Consistent Field (SCF) method**:
1.  Guess an initial electron density, $n^{(0)}(\mathbf{r})$.
2.  Construct the effective potential $V_{\text{eff}}[n^{(0)}](\mathbf{r})$.
3.  Solve the Kohn-Sham equations to obtain a new set of orbitals $\{\phi_i^{(0)}\}$.
4.  Construct a new density $n^{(1)}(\mathbf{r})$ from these orbitals.
5.  Compare $n^{(1)}$ to $n^{(0)}$. If they are sufficiently close (converged), the calculation is complete. Otherwise, mix the old and new densities to produce a better guess for the next iteration and repeat from step 2.

The exact form of the [exchange-correlation functional](@entry_id:142042) $E_{xc}[n]$ is unknown and must be approximated. The development of increasingly accurate approximations for $E_{xc}[n]$ is a central focus of modern DFT research, and has transformed the theory into the most widely used quantum mechanical method in [computational chemistry](@entry_id:143039) and condensed matter physics.