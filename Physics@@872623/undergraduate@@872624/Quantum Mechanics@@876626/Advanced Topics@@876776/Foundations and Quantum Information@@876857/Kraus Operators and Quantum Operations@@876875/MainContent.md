## Introduction
While the Schrödinger equation masterfully describes the evolution of perfectly isolated quantum systems, reality is rarely so clean. All realistic quantum systems are "open," meaning they inevitably interact with their environment. These interactions lead to complex processes like decoherence and [energy dissipation](@entry_id:147406) that cannot be captured by simple [unitary evolution](@entry_id:145020). To understand and control quantum systems in the real world, we need a more general mathematical framework.

This article addresses this gap by introducing the theory of **quantum operations** and their most common description, the **Kraus [operator-sum representation](@entry_id:140073)**. This powerful formalism provides the language to describe any physically possible transformation of a quantum state. We will demystify this essential topic by breaking it down into its core components and practical applications.

The journey begins in **Principles and Mechanisms**, where we will lay the mathematical groundwork for the [operator-sum representation](@entry_id:140073), explore the crucial physical constraints of complete positivity and trace preservation, and uncover the elegant physical picture provided by the Stinespring Dilation Theorem. Next, in **Applications and Interdisciplinary Connections**, we will see the theory in action, applying it to model critical physical processes like noise, decoherence, measurement, and imperfect quantum gates, and exploring its connections to quantum error correction and other areas of quantum science. Finally, **Hands-On Practices** will offer a chance to solidify your understanding by working through concrete calculations involving common noise channels.

## Principles and Mechanisms

The Schrödinger equation provides a complete description for the time evolution of a closed quantum system, one that is perfectly isolated from its surroundings. This evolution is always unitary. However, any realistic quantum system is inevitably an **[open quantum system](@entry_id:141912)**, subject to interactions with its environment. These interactions lead to processes such as decoherence, dissipation, and measurement, which cannot be described by [unitary evolution](@entry_id:145020) alone. To account for the full range of physical transformations a quantum state can undergo, we must generalize our framework from unitary transformations to the broader class of **quantum operations**, also known as [quantum channels](@entry_id:145403).

### The Operator-Sum Representation

The most general transformation of a quantum state, described by a [density matrix](@entry_id:139892) $\rho$, can be expressed through the **[operator-sum representation](@entry_id:140073) (OSR)**. A quantum operation $\mathcal{E}$ maps an initial density matrix $\rho$ to a final [density matrix](@entry_id:139892) $\rho'$ according to the formula:

$$ \rho' = \mathcal{E}(\rho) = \sum_{k} E_k \rho E_k^\dagger $$

The operators $\{E_k\}$ are known as the **Kraus operators** of the channel. They act on the Hilbert space of the system and encapsulate the dynamics of the transformation. The index $k$ can be thought of as labeling the different possible "outcomes" of the [system-environment interaction](@entry_id:145659), which are then summed over incoherently.

It is instructive to see how the familiar case of [unitary evolution](@entry_id:145020) fits into this more general framework. The evolution of a [closed system](@entry_id:139565) for a time $t$ under a time-independent Hamiltonian $H$ is described by a unitary operator $U = \exp(-iHt/\hbar)$. The density matrix transforms as $\rho' = U \rho U^\dagger$. This is an [operator-sum representation](@entry_id:140073) with a single Kraus operator, $E_0 = U$. For instance, the evolution of a qubit under the Hamiltonian $H = \frac{\hbar \omega}{2} \sigma_z$ results in the unitary operator $U(t) = \exp(-i\frac{\omega t}{2}\sigma_z)$, which itself serves as the sole Kraus operator for this ideal, noise-free process [@problem_id:2099498]. The existence of multiple, non-proportional Kraus operators is the hallmark of non-[unitary evolution](@entry_id:145020), characteristic of noise, decoherence, or measurement.

### Physical Constraints I: Trace Preservation and the Completeness Relation

For a quantum operation to represent a valid physical process that does not involve post-selection (i.e., discarding certain outcomes), it must conserve probability. Since the trace of a density matrix, $\text{Tr}(\rho)$, is equal to 1, this physical requirement translates into the mathematical condition that the map must be **trace-preserving**:

$$ \text{Tr}(\mathcal{E}(\rho)) = \text{Tr}(\rho) $$

for any input state $\rho$. Let us apply this condition to the [operator-sum representation](@entry_id:140073):

$$ \text{Tr}(\mathcal{E}(\rho)) = \text{Tr}\left(\sum_k E_k \rho E_k^\dagger\right) = \sum_k \text{Tr}(E_k \rho E_k^\dagger) $$

Using the cyclic property of the trace, $\text{Tr}(ABC) = \text{Tr}(CAB)$, we can rearrange the terms inside the sum:

$$ \sum_k \text{Tr}(E_k^\dagger E_k \rho) = \text{Tr}\left(\left(\sum_k E_k^\dagger E_k\right) \rho\right) $$

For this to equal $\text{Tr}(\rho)$ for any arbitrary state $\rho$, the expression in the parenthesis must be the identity operator $I$. This gives us the fundamental **[completeness relation](@entry_id:139077)** that the Kraus operators for any trace-preserving quantum operation must satisfy:

$$ \sum_k E_k^\dagger E_k = I $$

This condition is not merely a mathematical formality; it is a powerful constraint that dictates the allowed form of physical processes. For example, if a decoherence model is proposed with a set of Kraus operators containing unknown parameters, the [completeness relation](@entry_id:139077) can be used to determine their values [@problem_id:2099473]. Similarly, this relation connects the abstract parameters of a channel model to physically measurable quantities. If a qubit prepared in state $|0\rangle$ is passed through a channel with Kraus operators $E_1 = \alpha \sigma_y$ and $E_2 = \beta \sigma_z$, the [completeness relation](@entry_id:139077) immediately tells us that $\alpha^2 + \beta^2 = 1$. If an experiment then reveals the probability of measuring the output in state $|0\rangle$, this provides a second equation allowing for the determination of the specific values of $\alpha$ and $\beta$ [@problem_id:2099470].

### Physical Constraints II: Complete Positivity

A second, more subtle, condition for a map to be physical is that it must be **completely positive (CP)**. A map $\mathcal{E}$ is called **positive** if it maps any positive semidefinite operator (like a density matrix) to another positive semidefinite operator. This ensures that probabilities calculated from the output state are non-negative.

However, positivity alone is not sufficient. Consider a situation where the map $\mathcal{E}$ acts only on a subsystem $A$ of a larger composite system $AB$, which may be in an [entangled state](@entry_id:142916). The total map is $\mathcal{E}_A \otimes \mathcal{I}_B$, where $\mathcal{I}_B$ is the identity map on subsystem $B$. For $\mathcal{E}_A$ to represent a physical process, the combined map $\mathcal{E}_A \otimes \mathcal{I}_B$ must also transform valid density matrices of the composite system into valid density matrices. A map $\mathcal{E}_A$ that satisfies this requirement for any dimension of system $B$ and any state on $AB$ is called **completely positive**.

A canonical example demonstrating the necessity of this stronger condition is the [matrix transpose](@entry_id:155858) map, $\mathcal{T}(\rho) = \rho^T$. This map is positive on a single qubit; the transpose of a positive semidefinite $2 \times 2$ matrix is also positive semidefinite. However, it is not *completely* positive. To see this, consider applying the [transpose map](@entry_id:152972) to just one qubit (say, qubit B) of a [two-qubit system](@entry_id:203437) prepared in the maximally [entangled state](@entry_id:142916) $|\psi\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$. The resulting operator, $(\mathcal{I} \otimes \mathcal{T})(\rho)$, where $\rho = |\psi\rangle\langle\psi|$, is known as the [partial transpose](@entry_id:136776) of $\rho$. A direct calculation shows that this resulting $4 \times 4$ matrix has an eigenvalue of $-\frac{1}{2}$ [@problem_id:2099474]. Since a [density matrix](@entry_id:139892) cannot have negative eigenvalues, the [transpose map](@entry_id:152972) cannot correspond to a physical evolution.

It is a cornerstone result of quantum information theory, known as **Choi's theorem on [completely positive maps](@entry_id:139203)**, that a map $\mathcal{E}$ is completely positive if and only if it admits an [operator-sum representation](@entry_id:140073). This is precisely why the Kraus representation is so central: it automatically guarantees that the map is not only positive but completely positive, and is therefore physically realizable. A completely positive, [trace-preserving map](@entry_id:146926) is often abbreviated as a **CPTP map**.

### The Physical Interpretation: Stinespring Dilation

The [operator-sum representation](@entry_id:140073) is a powerful mathematical tool, but it begs a physical question: what is the underlying process that gives rise to this structure? The **Stinespring Dilation Theorem** provides a profound and intuitive answer: any quantum operation on a system $S$ can be realized as a [unitary evolution](@entry_id:145020) on a larger composite system comprising $S$ and an auxiliary system $A$, called an **ancilla** or **environment**, followed by discarding the ancilla.

More formally, for any CPTP map $\mathcal{E}(\rho) = \sum_k E_k \rho E_k^\dagger$, there exists an [ancilla system](@entry_id:142219), initially in a [pure state](@entry_id:138657) $|0\rangle_A$, and a unitary operator $U$ acting on the composite system Hilbert space $\mathcal{H}_S \otimes \mathcal{H}_A$, such that:

$$ \mathcal{E}(\rho) = \text{Tr}_A \left( U (\rho \otimes |0\rangle_A\langle 0|_A) U^\dagger \right) $$

Here, $\text{Tr}_A$ denotes the [partial trace](@entry_id:146482) over the [ancilla system](@entry_id:142219). This theorem tells us that decoherence and non-unitary dynamics can be understood as arising from the system becoming entangled with an environment, whose degrees of freedom are then ignored or become inaccessible to the observer.

The Kraus operators are directly related to the action of the unitary $U$. The dimension of the [ancilla system](@entry_id:142219) required for this construction is related to the number of Kraus operators. If a channel is described by $m$ Kraus operators, $\{E_1, \dots, E_m\}$, an ancilla of dimension $m$ is sufficient. However, the Kraus representation for a channel is not unique. The minimum number of Kraus operators required to represent a channel is called the **Kraus rank** of the channel, and this rank determines the minimal dimension of the ancilla needed for a Stinespring dilation [@problem_id:2099509]. For example, a channel given by two Kraus operators will generally require a two-dimensional ancilla. However, if those two operators happen to be linearly dependent, the channel can be simplified to a representation with a single Kraus operator, which must be unitary. In this special case, the minimal ancilla dimension is one (i.e., no ancilla is needed).

### Alternative Representations and Equivalence

#### The Choi-Jamiołkowski Isomorphism

While the OSR is fundamental, it is often convenient to represent a channel in a different way. The **Choi-Jamiołkowski isomorphism** provides a powerful mapping between [quantum channels](@entry_id:145403) (which are superoperators, i.e., operators acting on operators) and standard quantum states (which are operators acting on vectors). This is achieved by defining the **Choi matrix** of a channel $\mathcal{E}$, denoted $J(\mathcal{E})$, as the result of applying the channel to one half of a maximally [entangled state](@entry_id:142916) shared between the system and an identical reference system. For a system with basis $\{|i\rangle\}$, the Choi matrix is:

$$ J(\mathcal{E}) = (\mathcal{I} \otimes \mathcal{E})(|\Phi^+\rangle\langle\Phi^+|) $$

where $|\Phi^+\rangle = \frac{1}{\sqrt{d}} \sum_{i=0}^{d-1} |i\rangle \otimes |i\rangle$ is a maximally entangled state on a $d \times d$ system.

The Choi matrix contains all the information about the channel. The condition of complete positivity for $\mathcal{E}$ is elegantly captured by the statement that the Choi matrix $J(\mathcal{E})$ must be positive semidefinite. Calculating the eigenvalues of $J(\mathcal{E})$ for a given channel thus serves as a direct test of its physical validity [@problem_id:2099471].

This [isomorphism](@entry_id:137127) is a two-way street. Not only can we compute the Choi matrix from the Kraus operators, but we can also extract a set of Kraus operators from a given Choi matrix. If one performs a [spectral decomposition](@entry_id:148809) of $J(\mathcal{E}) = \sum_j \lambda_j |v_j\rangle\langle v_j|$, then each eigenvector $|v_j\rangle$ can be "reshaped" into a matrix $E_j = \sqrt{\lambda_j} \text{unvec}(|v_j\rangle)$ that serves as a Kraus operator. This procedure provides a systematic way to find an OSR for a channel if its Choi matrix is known, for instance, through experimental quantum process [tomography](@entry_id:756051) [@problem_id:2099458].

#### Freedom in the Kraus Representation

As mentioned earlier, the set of Kraus operators describing a given [quantum channel](@entry_id:141237) is not unique. If $\{E_k\}$ is a set of Kraus operators for a channel $\mathcal{E}$, then any other set $\{F_j\}$ of the form

$$ F_j = \sum_k u_{jk} E_k $$

where $U = (u_{jk})$ is an arbitrary [unitary matrix](@entry_id:138978), will describe the exact same channel. One can verify that $\sum_j F_j \rho F_j^\dagger = \sum_k E_k \rho E_k^\dagger$. This freedom is analogous to the freedom of choosing a basis in a vector space. For example, the standard Kraus operators for the [amplitude damping channel](@entry_id:141880) can be transformed using a simple Hadamard-like unitary matrix to produce a new, physically equivalent set of Kraus operators that look quite different but produce identical dynamics [@problem_id:2099496]. This unitary freedom is intimately linked to the choice of basis for the environment in the Stinespring dilation picture.

### Important Classes of Quantum Channels

Quantum channels can be categorized based on their properties. One of the most important classifications is based on their action on the maximally mixed state.

#### Unital Channels

A [quantum channel](@entry_id:141237) $\mathcal{E}$ is said to be **unital** if it preserves the [identity operator](@entry_id:204623):

$$ \mathcal{E}(I) = I $$

For a $d$-dimensional system, this is equivalent to preserving the maximally [mixed state](@entry_id:147011), $\mathcal{E}(I/d) = I/d$. Physically, a unital channel does not have a "preferred" state; it does not systematically bias the system towards a particular state or direction in the state space. Many common noise models are unital. For example, the **phase-flip channel**, which applies a $\sigma_z$ operator with probability $p$ and does nothing with probability $1-p$, is unital for all values of $p$ [@problem_id:2099461]. The bit-flip channel and the [depolarizing channel](@entry_id:139899) are other canonical examples of unital channels.

#### Non-Unital Channels

In contrast, a **non-unital** channel is one that does not preserve the maximally mixed state. These channels typically model processes involving energy exchange with an environment that has a thermal bias. The most prominent example is the **[amplitude damping channel](@entry_id:141880)**, which models [spontaneous emission](@entry_id:140032). An excited state $|1\rangle$ can decay to the ground state $|0\rangle$, but the reverse process does not happen. This asymmetry introduces a bias towards the ground state, and the channel is therefore not unital.

One can construct other physical examples of non-unital channels. Consider a "Thermal Excitation Channel" where a qubit in the ground state $|0\rangle$ can be excited to $|1\rangle$ with probability $p$ by a high-temperature reservoir, while the excited state $|1\rangle$ is unaffected. The Kraus operators can be constructed to model this process, and they will satisfy the trace-preserving condition. However, applying this channel to the maximally [mixed state](@entry_id:147011) $\frac{1}{2}I$ results in an output state that is biased towards the $|1\rangle$ state, demonstrating that the channel is not unital [@problem_id:2099501]. Understanding whether a channel is unital or non-unital is crucial for analyzing its long-term behavior and its effect on quantum information.