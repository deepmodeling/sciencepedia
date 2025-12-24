## Introduction
In the realistic description of quantum systems, interactions with an external environment are unavoidable. The evolution of such 'open' quantum systems is described not by unitary transformations, but by quantum dynamical maps. A fundamental question then arises: what are the minimal physical requirements that such a map must satisfy? While the preservation of state positivity seems like an obvious and [sufficient condition](@entry_id:276242), the uniquely quantum phenomenon of entanglement reveals a deeper, more stringent constraint. Relying on positivity alone can lead to unphysical predictions, such as negative probabilities, when the system of interest is entangled with an unobserved ancillary system.

This article provides a comprehensive exploration of this crucial distinction, guiding the reader from the intuitive notion of positivity to the physically necessary condition of complete positivity. We will establish the formal mathematical framework, demonstrating why complete positivity is essential and introducing powerful analytical tools like the Choi-Jamiołkowski isomorphism and the Kraus representation. Following this, we will showcase the far-reaching impact of these concepts, from modeling realistic noise in quantum devices to their surprising role in entanglement detection and the formulation of quantum thermodynamics. Finally, the hands-on practices will provide opportunities to apply these theoretical tools to concrete problems, cementing a robust understanding of how these mathematical properties govern the physical world.

## Principles and Mechanisms

In the study of [open quantum systems](@entry_id:138632), the evolution of a system of interest, which is coupled to a larger environment, is described by a quantum dynamical map. This chapter delineates the fundamental principles governing these maps, moving from the intuitive requirement of preserving positivity to the more subtle, yet physically essential, condition of complete positivity. We will establish the mathematical framework necessary to distinguish these properties and explore the profound physical consequences of this distinction.

### Positivity: A Necessary First Step

A quantum state is mathematically represented by a [density operator](@entry_id:138151) $\rho$, which must satisfy two conditions: it must have unit trace, $\operatorname{Tr}(\rho) = 1$, and it must be positive semidefinite, $\rho \ge 0$. The latter condition ensures that the probabilities of all possible measurement outcomes are non-negative. A [linear map](@entry_id:201112) $\Phi: \mathcal{B}(\mathcal{H}_S) \to \mathcal{B}(\mathcal{H}_S)$ describing the evolution of a system with Hilbert space $\mathcal{H}_S$ must, at a minimum, preserve these properties. A map is called **trace-preserving (TP)** if it conserves probability, i.e., $\operatorname{Tr}[\Phi(\rho)] = \operatorname{Tr}[\rho]$ for all operators $\rho$. More fundamentally, it must map valid states to valid states. This leads to the first crucial property: **positivity**.

A linear map $\Phi$ is defined as **positive** if it maps every positive semidefinite operator to a positive semidefinite operator. That is, if $\rho \ge 0$, then $\Phi(\rho) \ge 0$. This seems like a natural and [sufficient condition](@entry_id:276242); if a map transforms any valid initial density matrix into another positive semidefinite operator, it appears to be a physically reasonable evolution. However, this intuition is incomplete, as it neglects the uniquely quantum phenomenon of entanglement.

### The Role of Ancillary Systems and Entanglement

The critical flaw in relying on positivity alone becomes apparent when we consider that our system $S$ may be a part of a larger composite system. Imagine our system $S$ is initially entangled with an auxiliary system, or **ancilla**, $A$, which does not interact with the environment of $S$. The joint state of the system and ancilla, $\rho_{SA}$, is a positive semidefinite operator on the composite Hilbert space $\mathcal{H}_S \otimes \mathcal{H}_A$. If the dynamics $\Phi$ act locally on system $S$, the evolution of the joint state is described by the map $\Phi \otimes \mathbb{I}_A$, where $\mathbb{I}_A$ is the identity map on the ancilla's operator space.

Physical consistency demands that the final state $(\Phi \otimes \mathbb{I}_A)(\rho_{SA})$ must also be a valid, positive semidefinite density operator. A [positive map](@entry_id:1129978) $\Phi$ guarantees this outcome for any *separable* (classically correlated) state $\rho_{SA} = \sum_i p_i \rho_S^{(i)} \otimes \rho_A^{(i)}$, as the output is a convex sum of positive operators $\sum_i p_i \Phi(\rho_S^{(i)}) \otimes \rho_A^{(i)}$. However, for *entangled* states, this guarantee breaks down. It is precisely the presence of initial entanglement with an unobserved "spectator" system that reveals the insufficiency of simple positivity.

### Complete Positivity: The Correct Physical Requirement

This leads to a stronger, physically necessary condition. A dynamical map is physically admissible only if it preserves positivity *regardless of any ancillary systems with which the primary system might be entangled*. This is the principle of **complete positivity**.

Formally, a linear map $\Phi$ is **completely positive (CP)** if for any ancillary Hilbert space $\mathcal{H}_A$ of any finite dimension $n$, the extended map $\Phi \otimes \mathbb{I}_n$ is positive. That is, for every $n \in \mathbb{N}$ and every positive semidefinite operator $X$ on $\mathcal{H}_S \otimes \mathbb{C}^n$, the operator $(\Phi \otimes \mathbb{I}_n)(X)$ is also positive semidefinite.

A map that is both completely positive and trace-preserving is known as a **[quantum channel](@entry_id:141237)** or a **CPTP map**. These maps form the bedrock of the theory of open quantum systems, as they represent the most general physical processes that can occur on a quantum system, assuming the initial state of the system and environment are uncorrelated. The celebrated **Stinespring Dilation Theorem** makes this connection precise: a map is CPTP if and only if it can be realized by a [unitary evolution](@entry_id:145020) on a larger system (system plus environment) followed by a [partial trace](@entry_id:146482) over the environment. Mere positivity is not sufficient for such a physical realization.

A crucial result simplifies the verification of complete positivity. For a map acting on a $d$-dimensional system, it is not necessary to check ancillas of all dimensions. If the map $\Phi \otimes \mathbb{I}_d$ is positive (a property known as $d$-positivity), then the map is guaranteed to be completely positive.

### The Transpose Map: A Canonical Unphysical Process

The distinction between positivity and complete positivity is best illustrated by a canonical example: the **[transpose map](@entry_id:152972)**. Let $T$ be a map on $\mathcal{B}(\mathcal{H}_S)$ defined with respect to a fixed [orthonormal basis](@entry_id:147779) $\{|i\rangle\}$ as $T(X) = X^\top$.

The [transpose map](@entry_id:152972) is both positive and trace-preserving. Positivity holds because for any $\rho \ge 0$, the operator $\rho^\top$ is also positive semidefinite. Trace-preservation is manifest since $\operatorname{Tr}(X^\top) = \operatorname{Tr}(X)$. Despite these properties, the [transpose map](@entry_id:152972) is not completely positive for any system of dimension $d \ge 2$, and thus it does not represent a valid [quantum channel](@entry_id:141237).

To see this, consider a [two-qubit system](@entry_id:203437) ($d=2$) and let $T$ act on the first qubit while the identity $\mathbb{I}$ acts on the second. Let the initial state be the maximally entangled Bell state $|\Psi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$. The corresponding [density operator](@entry_id:138151) is $\rho_{12} = |\Psi^+\rangle\langle\Psi^+|$. Applying the map $T_1 \otimes \mathbb{I}_2$ yields:
$$
(T_1 \otimes \mathbb{I}_2)(\rho_{12}) = \frac{1}{2} \begin{pmatrix} 1  & 0  & 0  & 0 \\ 0  & 0  & 1  & 0 \\ 0  & 1  & 0  & 0 \\ 0  & 0  & 0  & 1 \end{pmatrix}
$$
This resulting operator, known as the [partial transpose](@entry_id:136776) of $\rho_{12}$, is not positive semidefinite. Its eigenvalues are $\{\frac{1}{2}, \frac{1}{2}, \frac{1}{2}, -\frac{1}{2}\}$. The presence of a negative eigenvalue means that the output is an unphysical state. This demonstrates that applying the "local" and seemingly innocuous [transpose map](@entry_id:152972) to one part of an entangled system can corrupt the global state into a non-physical entity. Consequently, the [transpose map](@entry_id:152972) is not completely positive and cannot arise from a unitary evolution on a larger system.

### The Choi-Jamiołkowski Isomorphism

A powerful tool for analyzing quantum maps is the **Choi-Jamiołkowski [isomorphism](@entry_id:137127)**. This establishes a one-to-one correspondence between a [linear map](@entry_id:201112) $\Phi: \mathcal{B}(\mathcal{H}_{\text{in}}) \to \mathcal{B}(\mathcal{H}_{\text{out}})$ and a linear operator $J(\Phi)$ on the composite space $\mathcal{H}_{\text{out}} \otimes \mathcal{H}_{\text{in}}$. This operator, known as the **Choi matrix** or **Choi operator**, is constructed by applying the map to one part of a maximally entangled state.

Let $\mathcal{H}_{\text{in}}$ be $d$-dimensional with basis $\{|i\rangle\}_{i=1}^d$. We define an unnormalized maximally entangled vector in $\mathcal{H}_{\text{in}} \otimes \mathcal{H}_{\text{in}}$ as $|\Omega\rangle = \sum_{i=1}^d |i\rangle \otimes |i\rangle$. The Choi matrix of a map $\Phi: \mathcal{B}(\mathcal{H}_{\text{in}}) \to \mathcal{B}(\mathcal{H}_{\text{out}})$ is then defined as:
$$
J(\Phi) = (\Phi \otimes \mathbb{I}_{\text{in}}) (|\Omega\rangle\langle\Omega|) = \sum_{i,j=1}^d \Phi(|i\rangle\langle j|) \otimes |i\rangle\langle j|
$$
The operator $J(\Phi)$ lives in $\mathcal{B}(\mathcal{H}_{\text{out}} \otimes \mathcal{H}_{\text{in}})$. This construction provides a direct way to convert questions about maps into questions about operators, which are often easier to analyze. The power of this isomorphism is captured by **Choi's Theorem**.

**Choi's Theorem**: A [linear map](@entry_id:201112) $\Phi$ is completely positive if and only if its Choi matrix $J(\Phi)$ is positive semidefinite.

This theorem provides an elegant and practical test for complete positivity: one only needs to construct a single matrix and check its eigenvalues. Furthermore, for a map $\Phi: \mathcal{B}(\mathcal{H}_S) \to \mathcal{B}(\mathcal{H}_S)$, the trace-preserving condition also has a simple form in terms of the Choi matrix: $\Phi$ is trace-preserving if and only if $\operatorname{Tr}_1(J(\Phi)) = I$, where $\operatorname{Tr}_1$ is the partial trace over the first tensor factor space (the output space in our construction).

### Structural Consequences of Complete Positivity

The property of complete positivity endows [quantum channels](@entry_id:145403) with a rich structure, elegantly captured by several key theorems.

#### The Kraus Representation

A direct consequence of Choi's theorem and the Stinespring dilation theorem is that any [completely positive map](@entry_id:146423) $\Phi$ admits an **[operator-sum representation](@entry_id:140073) (OSR)**, also known as a **Kraus representation**. This means the action of the map can be written as:
$$
\Phi(\rho) = \sum_k K_k \rho K_k^\dagger
$$
where the operators $\{K_k\}$, called Kraus operators, map the input Hilbert space to the output Hilbert space. Conversely, any map of this form is completely positive. If the map is also trace-preserving (i.e., it is a CPTP map), the Kraus operators must satisfy the condition $\sum_k K_k^\dagger K_k = I$. Maps that are positive but not CP, such as the [transpose map](@entry_id:152972), do not admit a Kraus representation.

#### Minimal Kraus Rank and the Choi Matrix

The Kraus representation is not unique. However, there is a minimum number of Kraus operators required to represent a given channel. This number, known as the **Kraus rank** of the channel, is deeply connected to the Choi matrix. The minimal number of Kraus operators required for any OSR of a channel $\Phi$ is equal to the rank of its Choi matrix, $J(\Phi)$.

To see why, note that the Choi matrix can be written in terms of the Kraus operators as $J(\Phi) = \sum_k |\psi_k\rangle\langle\psi_k|$, where each $|\psi_k\rangle$ is a vector in the composite space constructed from the operator $K_k$. This shows that the rank of $J(\Phi)$ is at most the number of Kraus operators. Conversely, from the [spectral decomposition](@entry_id:148809) of a positive semidefinite $J(\Phi)$, one can construct a set of Kraus operators whose number equals the rank of $J(\Phi)$. This provides a direct method to find the most efficient representation of a [quantum channel](@entry_id:141237). For instance, for a qubit channel given by Kraus operators $K_0 = \frac{\sqrt{3}}{2} I$, $K_1 = \frac{1}{2} |0\rangle\langle 1|$, and $K_2 = \frac{1}{2} |1\rangle\langle 0|$, one can construct the $4 \times 4$ Choi matrix and find its rank is 3, confirming that this three-operator representation is minimal.

### A Concrete Example: The Werner-Holevo Channel

To solidify the distinction between positive and [completely positive maps](@entry_id:139203), consider the family of qubit maps defined for $\lambda \in [0,1]$:
$$
\Phi_\lambda(\rho) = \lambda \rho^\top + (1-\lambda) \frac{\operatorname{Tr}(\rho)}{2} I
$$
This map is a convex combination of the [transpose map](@entry_id:152972) $T$ and the completely [depolarizing channel](@entry_id:139899). Since both $T$ and the [depolarizing channel](@entry_id:139899) are positive, their convex combination $\Phi_\lambda$ is also positive for all $\lambda \in [0,1]$.

To determine when $\Phi_\lambda$ is completely positive, we construct its Choi matrix $J(\Phi_\lambda)$ and find its eigenvalues. A direct calculation shows that the four eigenvalues of $J(\Phi_\lambda)$ are $\{\frac{1+\lambda}{2}, \frac{1+\lambda}{2}, \frac{1+\lambda}{2}, \frac{1-3\lambda}{2}\}$. For the Choi matrix to be positive semidefinite, all eigenvalues must be non-negative. For $\lambda \in [0,1]$, the eigenvalue $\frac{1+\lambda}{2}$ is always non-negative. The final eigenvalue requires $1-3\lambda \ge 0$, which implies $\lambda \le 1/3$.

Therefore, the map $\Phi_\lambda$ is completely positive if and only if $0 \le \lambda \le 1/3$. For any $\lambda$ in the range $(1/3, 1]$, the map is positive but not completely positive. At $\lambda=1$, we recover the [transpose map](@entry_id:152972), which is not CP. This example explicitly demonstrates that the set of CP maps is a strict subset of the set of positive maps.

### Geometric Perspective: Cones of Maps

The sets of positive and [completely positive maps](@entry_id:139203) on $\mathcal{B}(\mathcal{H})$ form convex cones. The Choi-Jamiołkowski [isomorphism](@entry_id:137127) provides a powerful geometric picture of these cones.
*   The cone of **[completely positive maps](@entry_id:139203)** is isomorphic to the cone of **positive semidefinite operators** on $\mathcal{H} \otimes \mathcal{H}$. This is a well-behaved, self-dual convex cone.
*   The cone of **positive maps** is isomorphic to a larger cone of operators known as **block-positive** or **separable** operators. An operator $W \in \mathcal{B}(\mathcal{H} \otimes \mathcal{H})$ is block-positive if $\langle x \otimes y | W | x \otimes y \rangle \ge 0$ for all product vectors $|x \otimes y\rangle$.

Every positive semidefinite operator is necessarily block-positive, but the converse is not true. This shows geometrically that the CP cone is a subset of the positive cone. The swap operator $F = \sum_{i,j} |i\rangle\langle j| \otimes |j\rangle\langle i|$, which is the Choi matrix of the [transpose map](@entry_id:152972), serves as the perfect example. It is block-positive, since $\langle x \otimes y | F | x \otimes y \rangle = |\langle x|y \rangle|^2 \ge 0$. However, it is not positive semidefinite, as it has an eigenvalue of $-1$ on the antisymmetric subspace (for $d \ge 2$). This demonstrates that the cone of CP maps is strictly contained within the cone of positive maps.

### Advanced Implications of Complete Positivity

The requirement of complete positivity is not a mere mathematical subtlety; it is deeply woven into the fabric of quantum theory and has profound physical consequences, particularly in quantum information dynamics and thermodynamics.

#### Quantum Markovianity and Information Backflow

In the study of non-Markovian [quantum dynamics](@entry_id:138183), the distinction between positive and [completely positive maps](@entry_id:139203) is crucial. A memoryless, or **Markovian**, quantum process is described by a family of CPTP maps $\{\Lambda_t\}$ that is **CP-divisible**. This means that the propagator from time $s$ to $t \ge s$, given by $\Lambda_{t,s} = \Lambda_t \Lambda_s^{-1}$, is itself a CPTP map. A key operational signature of CP-[divisibility](@entry_id:190902) is that the distinguishability between any two quantum states, as measured by the [trace distance](@entry_id:142668) $D(\rho, \sigma)$, can only decrease over time. This holds true even for states entangled with an ancilla: the function $t \mapsto D((\mathbb{I}_A \otimes \Lambda_t)\rho_{AS}, (\mathbb{I}_A \otimes \Lambda_t)\sigma_{AS})$ is non-increasing.

In contrast, a process can be **P-divisible**, meaning each propagator $\Lambda_{t,s}$ is positive but not necessarily completely positive. Such a process is non-Markovian. While the [distinguishability](@entry_id:269889) of states *on the system alone* will still decrease monotonically, there can be a temporary increase in [distinguishability](@entry_id:269889) for states entangled with an ancilla. This phenomenon, where $D((\mathbb{I}_A \otimes \Lambda_t)\rho_{AS}, (\mathbb{I}_A \otimes \Lambda_t)\sigma_{AS})$ increases over some time interval, is a clear signature of **information backflow** from the environment to the system. Thus, complete positivity is the mathematical condition that forbids such hidden memory effects. Similarly, entanglement between the system and an isolated ancilla can only decrease under CP-divisible dynamics.

#### Thermodynamic Consistency

Perhaps the most dramatic illustration of the physical necessity of complete positivity comes from [quantum thermodynamics](@entry_id:140152). The second law of thermodynamics, in the Kelvin-Planck statement, forbids the extraction of work from a single heat bath in a [cyclic process](@entry_id:146195). The consistency of microscopic quantum dynamics with this macroscopic law rests on the property of complete positivity.

The connection is made via the [quantum relative entropy](@entry_id:144397), $D(\rho||\sigma)$, which quantifies the [distinguishability](@entry_id:269889) of two states. For a system in contact with a heat bath at inverse temperature $\beta$, the relative entropy to the Gibbs state, $D(\rho || \pi_\beta)$, is proportional to the [non-equilibrium free energy](@entry_id:1128780). A cornerstone of consistent statistical mechanics is the **data-processing inequality**, which states that [relative entropy](@entry_id:263920) cannot increase under a physical process (a CPTP map). This inequality, in turn, guarantees that the free energy of a system in contact with a bath can only decrease, leading to the Clausius inequality $\Delta S - \beta Q \ge 0$.

However, the data-processing inequality for relative entropy holds only for [completely positive maps](@entry_id:139203). A map that is merely positive but not CP can violate this inequality. This implies that for such an "unphysical" thermalization map, it is possible for the free energy of the system to *increase* during contact with the bath. In a [cyclic process](@entry_id:146195), this increase in free energy could be converted into work, leading to a net extraction of work from a single heat bath—a direct violation of the second law. This demonstrates that complete positivity is not just a condition for preserving the positivity of states in the presence of entanglement, but is a fundamental requirement for ensuring the thermodynamic consistency of quantum dynamics.