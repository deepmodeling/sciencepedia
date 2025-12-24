## Introduction
Quantum systems are rarely perfectly isolated; they inevitably interact with their surroundings, leading to phenomena like decoherence and [energy relaxation](@entry_id:136820). Describing the dynamics of these "open" quantum systems presents a fundamental challenge, as their evolution is no longer unitary. The operator-sum representation (OSR), also known as the Kraus representation, provides a powerful and universally applicable mathematical framework to meet this challenge. It allows us to characterize the evolution of a system's state without needing to track the complex details of its environment. This article provides a graduate-level exploration of this essential formalism.

This article will guide you through the theoretical underpinnings and practical applications of the OSR across three chapters. In "Principles and Mechanisms," we will derive the operator-sum representation from the first principles of a [system-environment interaction](@entry_id:145659) and establish its crucial connection to the axiomatic properties of completely positive and trace-preserving (CPTP) maps. In "Applications and Interdisciplinary Connections," we will explore how the OSR is used to model physical noise processes, design [quantum error correction](@entry_id:139596) protocols, and provide insights into [quantum thermodynamics](@entry_id:140152). Finally, the "Hands-On Practices" section will offer a set of problems designed to solidify your understanding and build your calculational skills with this indispensable tool.

## Principles and Mechanisms

Having established the conceptual foundation of [open quantum systems](@entry_id:138632), this chapter delves into the primary mathematical framework used to describe their dynamics: the operator-sum representation. We will derive this representation from the physical picture of a system interacting with an environment, elucidate its fundamental properties, and explore its applications in calculating physical quantities and characterizing the nature of quantum processes.

### The Microscopic Origin of Quantum Channels

The evolution of any closed quantum system, including a composite system and its environment, is unitary. The dynamics of an [open system](@entry_id:140185) are a direct consequence of this principle. Consider a system $S$ with Hilbert space $\mathcal{H}_S$ and an environment $E$ with Hilbert space $\mathcal{H}_E$. The total system $S+E$ resides in the [tensor product](@entry_id:140694) space $\mathcal{H}_S \otimes \mathcal{H}_E$. Its evolution over a given time interval is described by a [unitary operator](@entry_id:155165) $U$ acting on this composite space.

Typically, we assume the system and environment are initially uncorrelated, such that the initial state of the composite system is a product state, $\rho_{SE}(0) = \rho_S \otimes \sigma_E$. Here, $\rho_S$ is the initial state of the system, and $\sigma_E$ is the fixed initial state of the environment, which is a [density operator](@entry_id:138151) on $\mathcal{H}_E$. After the interaction, the state of the composite system becomes $U(\rho_S \otimes \sigma_E)U^\dagger$. Since we are only interested in the properties of the system $S$, we discard the environmental degrees of freedom by performing a **[partial trace](@entry_id:146482)** over $\mathcal{H}_E$, denoted $\mathrm{Tr}_E$.

This procedure defines a linear map $\Phi$, known as a **[quantum channel](@entry_id:141237)** or **quantum operation**, which maps the initial system state $\rho_S$ to its final state $\Phi(\rho_S)$:

$$
\Phi(\rho_S) = \mathrm{Tr}_E \left[ U (\rho_S \otimes \sigma_E) U^\dagger \right]
$$

This construction, which begins with a system-environment model and ends with a map on the system alone, is the physical basis for all valid quantum dynamics. The map $\Phi$ inherits crucial properties from this microscopic origin, ensuring that its predictions are physically consistent.

### The Operator-Sum Representation

The expression for $\Phi$ can be cast into a more convenient and powerful form known as the **operator-sum representation (OSR)**, or **Kraus representation**. This form makes the action of the channel on the system explicit without direct reference to the environment's structure.

To derive the OSR, we begin by expressing the environment's initial state $\sigma_E$ in a basis where it is diagonal. Since $\sigma_E$ is a [density operator](@entry_id:138151), it is positive semidefinite and can be written as $\sigma_E = \sum_j p_j |\epsilon_j\rangle\langle \epsilon_j|$, where $\{|\epsilon_j\rangle\}$ is an [orthonormal basis of eigenvectors](@entry_id:180262) for $\sigma_E$ and $p_j \ge 0$ are the corresponding eigenvalues, with $\sum_j p_j = 1$. Let us first consider the simpler, yet illustrative, case where the environment starts in a [pure state](@entry_id:138657), say $|0\rangle_E$, so $\sigma_E = |0\rangle_E \langle 0|_E$.

The channel is then $\Phi(\rho_S) = \mathrm{Tr}_E \left[ U (\rho_S \otimes |0\rangle_E \langle 0|_E) U^\dagger \right]$. To evaluate the partial trace, we can insert a [resolution of the identity](@entry_id:150115) for the environment, $I_E = \sum_i |i\rangle_E \langle i|_E$, where $\{|i\rangle_E\}$ is any orthonormal basis for $\mathcal{H}_E$.

$$
\begin{align}
\Phi(\rho_S)  = \sum_i \langle i|_E \left[ U (\rho_S \otimes |0\rangle_E \langle 0|_E) U^\dagger \right] |i\rangle_E \\
 = \sum_i \left( \langle i|_E U (I_S \otimes |0\rangle_E) \right) \rho_S \left( (I_S \otimes \langle 0|_E) U^\dagger |i\rangle_E \right)
\end{align}
$$

We now define a set of operators $\{K_i\}$ that act only on the system's Hilbert space $\mathcal{H}_S$:

$$
K_i \equiv \langle i|_E U (I_S \otimes |0\rangle_E)
$$

These are the **Kraus operators**. Each $K_i$ can be interpreted as an effective evolution on the system, conditioned on the environment undergoing a specific transition from its initial state $|0\rangle_E$ to a final basis state $|i\rangle_E$. The adjoint is $K_i^\dagger = (I_S \otimes \langle 0|_E) U^\dagger |i\rangle_E$. Substituting these definitions into the expression for $\Phi(\rho_S)$ yields the operator-sum representation:

$$
\Phi(\rho_S) = \sum_i K_i \rho_S K_i^\dagger
$$

If the environment starts in a [mixed state](@entry_id:147011) $\sigma_E = \sum_j p_j |\epsilon_j\rangle\langle \epsilon_j|$, the derivation is a straightforward extension. The resulting Kraus operators become $K_{ij} = \sqrt{p_j} \langle i|_E U (I_S \otimes |\epsilon_j\rangle_E)$, and the map is a sum over both indices, $\Phi(\rho_S) = \sum_{i,j} K_{ij} \rho_S K_{ij}^\dagger$. By relabeling the pair of indices $(i, j)$ with a single index, we recover the standard form $\sum_k K_k \rho_S K_k^\dagger$. 

**Example: Derivation for the Amplitude Damping Channel**
Let's make this concrete. Consider a qubit system $S$ interacting with a three-level environment $E$ initially in the state $|0\rangle_E$. The joint unitary evolution is defined on the relevant subspace by:
$$
\begin{align}
U\big(|0\rangle_{S}\otimes|0\rangle_{E}\big)  &= |0\rangle_{S}\otimes|0\rangle_{E} \\
U\big(|1\rangle_{S}\otimes|0\rangle_{E}\big)  &= \sqrt{1-\gamma}\,|1\rangle_{S}\otimes|0\rangle_{E}+\sqrt{\gamma}\,|0\rangle_{S}\otimes|1\rangle_{E}
\end{align}
$$
(Here, we simplify the model from  by assuming the environment has only two relevant levels, $|0\rangle_E, |1\rangle_E$). This unitary describes a process where the system's excited state $|1\rangle_S$ can decay to the ground state $|0\rangle_S$ with probability $\gamma$ by creating an excitation in the environment (state $|1\rangle_E$).

We choose the environment basis $\{|0\rangle_E, |1\rangle_E\}$ to define our Kraus operators, $K_i = \langle i|_E U (I_S \otimes |0\rangle_E)$.
For $i=0$:
$K_0 |a\rangle_S = \langle 0|_E U (|a\rangle_S \otimes |0\rangle_E)$ for $a \in \{0, 1\}$.
$K_0|0\rangle_S = \langle 0|_E (|0\rangle_S \otimes |0\rangle_E) = |0\rangle_S$.
$K_0|1\rangle_S = \langle 0|_E (\sqrt{1-\gamma}|1\rangle_S \otimes |0\rangle_E + \dots) = \sqrt{1-\gamma}|1\rangle_S$.
Thus, $K_0 = |0\rangle\langle 0| + \sqrt{1-\gamma}|1\rangle\langle 1|$.

For $i=1$:
$K_1 |a\rangle_S = \langle 1|_E U (|a\rangle_S \otimes |0\rangle_E)$.
$K_1|0\rangle_S = \langle 1|_E (|0\rangle_S \otimes |0\rangle_E) = 0$.
$K_1|1\rangle_S = \langle 1|_E (\dots + \sqrt{\gamma}|0\rangle_S \otimes |1\rangle_E) = \sqrt{\gamma}|0\rangle_S$.
Thus, $K_1 = \sqrt{\gamma}|0\rangle\langle 1|$.

The resulting channel, known as the **[amplitude damping channel](@entry_id:141880)**, is described by $\Phi(\rho_S) = K_0 \rho_S K_0^\dagger + K_1 \rho_S K_1^\dagger$. This simple example beautifully illustrates how the abstract formalism of the OSR directly connects to a specific physical process of [energy relaxation](@entry_id:136820).

### The Axiomatic Properties of Quantum Channels

Any physically realizable [quantum evolution](@entry_id:198246) must satisfy certain mathematical properties. The OSR provides a powerful way to check these properties and understand their implications. A map $\Phi$ is a valid [quantum channel](@entry_id:141237) if and only if it is **Completely Positive** and **Trace-Preserving** (CPTP).

#### Complete Positivity and the Physicality Constraint

A map $\Phi$ is **positive** if it maps positive semidefinite operators to positive semidefinite operators; i.e., if $\rho \ge 0$, then $\Phi(\rho) \ge 0$. This ensures that density matrices (which are positive) evolve into valid density matrices.

However, positivity alone is not a [sufficient condition](@entry_id:276242) for a map to be physically realizable. The correct, stronger condition is **complete positivity (CP)**. A map $\Phi$ is completely positive if, for any auxiliary system (or "ancilla") $R$ of any dimension $d$, the extended map $\Phi \otimes I_R$ is positive. Here, $I_R$ is the identity map on the [ancilla system](@entry_id:142219). This condition ensures that if we apply the dynamics $\Phi$ to a part of an entangled system, the overall state remains positive, which is a fundamental physical requirement.

The classic example that illustrates the distinction is the **[transpose map](@entry_id:152972)** $\mathcal{T}$, defined by $\mathcal{T}(\rho) = \rho^T$.
The [transpose map](@entry_id:152972) is positive. For any density operator $\rho \ge 0$ and any state $|\psi\rangle$, one can show that $\langle\psi|\mathcal{T}(\rho)|\psi\rangle = \langle\psi^*|\rho|\psi^*\rangle \ge 0$, where $|\psi^*\rangle$ is the vector obtained by taking the complex conjugate of the components of $|\psi\rangle$ in the computational basis. Thus, $\mathcal{T}(\rho)$ is a [positive operator](@entry_id:263696).

However, the [transpose map](@entry_id:152972) is **not completely positive**. To see this, we test the extended map $\mathrm{id}_2 \otimes \mathcal{T}$ on a maximally entangled two-qubit state, $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$. The corresponding [density operator](@entry_id:138151) is $\rho_{\Phi^+} = |\Phi^+\rangle\langle\Phi^+|$. Applying the [partial transpose](@entry_id:136776) on the second qubit gives:
$$
(\mathrm{id}_2 \otimes \mathcal{T})(\rho_{\Phi^+}) = \frac{1}{2} \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}
$$
This resulting operator has eigenvalues $\{1/2, 1/2, 1/2, -1/2\}$. The presence of a negative eigenvalue means the operator is not positive semidefinite. Since $\mathrm{id}_2 \otimes \mathcal{T}$ mapped a valid positive state to an unphysical non-[positive operator](@entry_id:263696), the original map $\mathcal{T}$ is not completely positive. 

This failure has a profound consequence: a map that is not completely positive cannot be derived from a [unitary evolution](@entry_id:145020) on a larger system and therefore does not represent a physical process. The connection to the OSR is provided by **Choi's theorem on [completely positive maps](@entry_id:139203)**: A linear map $\Phi$ is completely positive if and only if it admits an operator-sum representation. Because the [transpose map](@entry_id:152972) is not CP, it cannot be written in the form $\sum_k K_k \rho K_k^\dagger$.  

#### Trace Preservation and the Completeness Relation

For $\Phi(\rho)$ to be a valid density operator, its trace must be unity, assuming the input $\rho$ is normalized. This is the **trace-preserving (TP)** property: $\mathrm{Tr}[\Phi(\rho)] = \mathrm{Tr}[\rho]$ for all input states $\rho$. Using the OSR and the cyclic property of the trace:
$$
\begin{align}
\mathrm{Tr}[\Phi(\rho)]  &= \mathrm{Tr}\left[\sum_i K_i \rho K_i^\dagger\right] \\
 &= \sum_i \mathrm{Tr}[K_i \rho K_i^\dagger] \\
 &= \sum_i \mathrm{Tr}[K_i^\dagger K_i \rho] \\
 &= \mathrm{Tr}\left[\left(\sum_i K_i^\dagger K_i\right) \rho\right]
\end{align}
$$
For this to equal $\mathrm{Tr}[\rho]$ for any arbitrary $\rho$, the operator multiplying $\rho$ inside the trace must be the [identity operator](@entry_id:204623). This gives the **[completeness relation](@entry_id:139077)** for the Kraus operators:

$$
\sum_i K_i^\dagger K_i = I_S
$$

This algebraic condition on the Kraus operators is equivalent to the physical requirement that probability is conserved.  It can be directly verified for our [amplitude damping](@entry_id:146861) example:
$$
K_0^\dagger K_0 + K_1^\dagger K_1 = \left(|0\rangle\langle 0| + (1-\gamma)|1\rangle\langle 1|\right) + \gamma|1\rangle\langle 1| = |0\rangle\langle 0| + |1\rangle\langle 1| = I_S
$$
Any map that is both completely positive and trace-preserving is called a **CPTP map** and constitutes a valid [quantum channel](@entry_id:141237).

#### Unital Channels and Steady States

A related property is **unitality**. A channel $\Phi$ is unital if it leaves the maximally [mixed state](@entry_id:147011) invariant, i.e., $\Phi(I/d) = I/d$, which is equivalent to $\Phi(I)=I$. Applying the OSR to the [identity operator](@entry_id:204623), we find the condition for a unital channel:

$$
\sum_i K_i K_i^\dagger = I_S
$$

Note the difference in the order of operators compared to the trace-preserving condition. A channel can be trace-preserving without being unital, and vice versa. For example, the [amplitude damping channel](@entry_id:141880) is trace-preserving but not unital for $\gamma > 0$, since $\sum_i K_i K_i^\dagger = (1+\gamma)|0\rangle\langle 0| + (1-\gamma)|1\rangle\langle 1| \neq I_S$.  The physical meaning of this is that the channel has a preferential steady state. Repeated application of the [amplitude damping channel](@entry_id:141880) will drive any initial state towards the ground state $|0\rangle\langle 0|$, not the maximally mixed state. Unital channels, in contrast, describe dynamics that tend to randomize the system towards a uniform mixture.

### Structure and Freedom of the Representation

The OSR is a powerful tool, but it is important to understand its structure and inherent ambiguities.

#### Non-Uniqueness of Kraus Operators

The set of Kraus operators $\{K_i\}$ for a given channel $\Phi$ is not unique. If $\{K_i\}_{i=1}^N$ is a set of Kraus operators for $\Phi$, then any other set $\{K'_j\}_{j=1}^N$ related by a [unitary matrix](@entry_id:138978) $U$ of size $N \times N$,

$$
K'_j = \sum_{i=1}^N U_{ji} K_i
$$

will generate the exact same [quantum channel](@entry_id:141237). To see this, we compute the action of the channel using the new set:
$$
\begin{align}
\Phi'(\rho)  &= \sum_j K'_j \rho (K'_j)^\dagger \\
 &= \sum_j \left(\sum_i U_{ji} K_i\right) \rho \left(\sum_l U_{jl} K_l\right)^\dagger \\
 &= \sum_{i,l} \left(\sum_j U_{ji} U_{jl}^*\right) K_i \rho K_l^\dagger
\end{align}
$$
Since $U$ is unitary, its [matrix elements](@entry_id:186505) satisfy $\sum_j U_{ji} U_{jl}^* = \sum_j U_{ji} (U^\dagger)_{lj} = (UU^\dagger)_{il} = \delta_{il}$. The expression simplifies to:
$$
\Phi'(\rho) = \sum_{i,l} \delta_{il} K_i \rho K_l^\dagger = \sum_i K_i \rho K_i^\dagger = \Phi(\rho)
$$
This demonstrates that the two representations are physically equivalent.  This unitary freedom means that the individual Kraus operators do not have a direct, unique physical meaning; only the space spanned by them is uniquely determined by the channel.

#### The Kraus Rank and Minimal Environment Dimension

While a channel can have many different OSRs, the minimum number of Kraus operators required to represent it is a unique property of the channel, known as the **Kraus rank** or **Choi rank**. This rank is equal to the rank of the channel's Choi matrix.

This has a deep physical interpretation rooted in the **Stinespring dilation theorem**. The theorem guarantees that for any CP map $\Phi$, there exists a Hilbert space $\mathcal{H}_E$ and an [isometry](@entry_id:150881) $V: \mathcal{H}_S \to \mathcal{H}_S \otimes \mathcal{H}_E$ such that $\Phi(\rho) = \mathrm{Tr}_E[V\rho V^\dagger]$. The Kraus rank of the channel is precisely the minimal dimension required for the environment's Hilbert space $\mathcal{H}_E$ in such a physical realization.

For instance, for the **generalized [amplitude damping channel](@entry_id:141880)**, which models interaction with a thermal bath, a standard representation uses four Kraus operators. In the non-degenerate regime where both emission and absorption are possible ($0  \gamma  1$ and $0  p  1$, where $p$ is the thermal population of the environment), one can show that the Choi matrix of this channel has rank 4. This implies that the Kraus rank is 4, and any physical realization of this channel requires an environment with at least four dimensions. 

### Applications and Advanced Topics

#### The Heisenberg Picture and Expectation Values

The OSR describes the evolution of states in the Schrödinger picture, where states evolve and operators ([observables](@entry_id:267133)) are fixed. We can also formulate the dynamics in the **Heisenberg picture**, where the state is fixed and observables evolve. The evolution of an observable $X$ is described by the **[adjoint map](@entry_id:191705)** $\Phi^\dagger$, defined by the relation $\mathrm{Tr}[X^\dagger \Phi(\rho)] = \mathrm{Tr}[(\Phi^\dagger(X))^\dagger \rho]$ for all $\rho$ and $X$.

Using the OSR for $\Phi$, we can find the OSR for $\Phi^\dagger$:
$$
\begin{align}
\mathrm{Tr}[X^\dagger \Phi(\rho)]  = \mathrm{Tr}\left[X^\dagger \sum_i K_i \rho K_i^\dagger\right] \\
 = \sum_i \mathrm{Tr}[X^\dagger K_i \rho K_i^\dagger] \\
 = \sum_i \mathrm{Tr}[K_i^\dagger X^\dagger K_i \rho] \\
 = \mathrm{Tr}\left[\left(\sum_i K_i^\dagger X K_i\right)^\dagger \rho\right]
\end{align}
$$
By comparison with the definition of the adjoint, we identify the action of the Heisenberg-picture map:
$$
\Phi^\dagger(X) = \sum_i K_i^\dagger X K_i
$$
The equivalence of the two pictures is expressed by the important identity for [expectation values](@entry_id:153208):
$$
\langle X \rangle_{\text{final}} = \mathrm{Tr}[\Phi(\rho) X] = \mathrm{Tr}[\rho \Phi^\dagger(X)]
$$
This identity is often computationally advantageous. For example, to calculate the change in the average energy of a system, $\Delta E = \mathrm{Tr}[\Phi(\rho) H] - \mathrm{Tr}[\rho H]$, we can use the Heisenberg picture to write it as $\Delta E = \mathrm{Tr}[\rho (\Phi^\dagger(H) - H)]$. This requires evolving a single operator, the Hamiltonian $H$, rather than every possible input state $\rho$. This approach is particularly useful in [quantum thermodynamics](@entry_id:140152) for calculating quantities like heat and work. 

#### Operator-Sum Representation for Non-Markovian Dynamics

The standard OSR describes the evolution over a fixed time interval. For time-[continuous dynamics](@entry_id:268176), we have a family of maps $\Lambda(t)$. A process is called **Markovian** if the evolution from time $t_1$ to $t_2$ depends only on the state at $t_1$, not on the history before $t_1$. A precise mathematical formulation of this is **CP-[divisibility](@entry_id:190902)**: the process $\Lambda(t)$ is CP-divisible if for any $t_2 \ge t_1 \ge 0$, the intermediate map $V(t_2, t_1)$ defined by $\Lambda(t_2) = V(t_2, t_1) \circ \Lambda(t_1)$ is itself a CPTP map.

If a process is not CP-divisible, it is **non-Markovian**. This occurs when the environment has memory, leading to information flowing back from the environment to the system. In this case, for some interval $[t_1, t_2]$, the map $V(t_2, t_1)$ will not be completely positive. This means it does not admit a standard Kraus representation. The failure to find a valid OSR for the intermediate dynamics is a direct signature of non-Markovianity. 

#### Extension to Infinite-Dimensional Systems

Many physically relevant environments, such as the electromagnetic field (a bosonic bath), are described by infinite-dimensional Hilbert spaces. The formalism of the OSR can be extended to this case. If the environment's Hilbert space is separable (i.e., has a countable [orthonormal basis](@entry_id:147779)), the Stinespring construction still yields a [countable set](@entry_id:140218) of Kraus operators, $\Phi(\rho) = \sum_{i=1}^\infty K_i \rho K_i^\dagger$. If the environment has a [continuous spectrum](@entry_id:153573), the representation may take the form of an integral over a continuous variable $x$: $\Phi(\rho) = \int K(x) \rho K(x)^\dagger d\mu(x)$.

In these infinite-dimensional cases, one must be careful about the convergence of the sum or integral. For a normal, CPTP map on a separable Hilbert space, the [completeness relation](@entry_id:139077) $\sum_i K_i^\dagger K_i = I$ (converging in the [strong operator topology](@entry_id:272264)) is a [sufficient condition](@entry_id:276242) to guarantee that the OSR series converges in the trace norm for any trace-class input state $\rho$. This ensures that the framework remains well-behaved and physically meaningful even when dealing with the complexities of infinite-dimensional environments. 