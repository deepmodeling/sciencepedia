## Introduction
Correlations are the connective tissue of the quantum world, dictating everything from the flow of information to the emergence of classical reality. In disciplines ranging from quantum computing to thermodynamics, understanding the nature and strength of these connections is paramount. However, simply acknowledging their existence is insufficient. A central challenge lies in rigorously quantifying these correlations and, crucially, distinguishing between those that are classical in nature and those that are uniquely quantum, like entanglement.

This article provides a comprehensive guide to the primary tool for this task: [quantum mutual information](@entry_id:144024). We will build a foundational understanding of this measure and its derivatives, then explore its profound physical implications across diverse fields. The first chapter, **Principles and Mechanisms**, introduces the formal definition of [quantum mutual information](@entry_id:144024), dissects it into classical and quantum components like [quantum discord](@entry_id:145504), and extends the concept to multipartite systems. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the operational power of these ideas, showing how [mutual information](@entry_id:138718) quantifies [thermodynamic work](@entry_id:137272), defines [communication channel](@entry_id:272474) capacities, governs open [system dynamics](@entry_id:136288), and characterizes [phases of matter](@entry_id:196677). Finally, the **Hands-On Practices** section provides opportunities to apply these concepts to concrete physical problems. By navigating these sections, you will gain the theoretical and practical knowledge to wield [quantum information theory](@entry_id:141608) as a powerful lens for analyzing the correlated quantum universe.

## Principles and Mechanisms

In the study of [quantum thermodynamics](@entry_id:140152) and open quantum systems, understanding the nature and extent of correlations between a system and its environment, or between different parts of a composite system, is of paramount importance. These correlations govern the flow of information, the process of decoherence, and the thermodynamic resources available within a quantum state. This chapter lays down the fundamental principles for quantifying and classifying these correlations, moving from the total correlation content of a state to its decomposition into classical and quantum components, and finally to the nuances of multipartite systems.

### Defining and Quantifying Total Correlation: Quantum Mutual Information

The most fundamental measure of the total correlation—both classical and quantum—between two quantum systems, $A$ and $B$, is the **[quantum mutual information](@entry_id:144024)**, denoted $I(A:B)$. Its definition is rooted in the concept of distinguishability. Specifically, it quantifies how distinguishable the actual state of the composite system, $\rho_{AB}$, is from a hypothetical uncorrelated state formed by the [tensor product](@entry_id:140694) of its own marginals, $\rho_A \otimes \rho_B$, where $\rho_A = \operatorname{Tr}_B(\rho_{AB})$ and $\rho_B = \operatorname{Tr}_A(\rho_{AB})$.

This distinguishability is measured by the **[quantum relative entropy](@entry_id:144397)**, $D(\rho \| \sigma) = \operatorname{Tr}[\rho (\log \rho - \log \sigma)]$, which is a quantum generalization of the Kullback–Leibler divergence. The [quantum mutual information](@entry_id:144024) is thus formally defined as:

$I(A:B)_{\rho} \equiv D(\rho_{AB} \| \rho_A \otimes \rho_B)$

This definition makes it clear that $I(A:B)$ is always non-negative, and it is zero if and only if $\rho_{AB} = \rho_A \otimes \rho_B$, which is the very definition of an uncorrelated state. A more convenient computational formula can be derived by expanding the definition of [relative entropy](@entry_id:263920). Using the von Neumann entropy, $S(\rho) = -\operatorname{Tr}(\rho \log \rho)$, we arrive at the widely used expression:

$I(A:B)_{\rho} = S(\rho_A) + S(\rho_B) - S(\rho_{AB})$

Let us examine this quantity for two elementary cases, using base-2 logarithms for entropies (measuring information in bits).

First, consider any **product state**, $\rho_{AB} = \rho_A \otimes \rho_B$. The entropy of a [tensor product](@entry_id:140694) state is the sum of the entropies of its constituents, so $S(\rho_{AB}) = S(\rho_A) + S(\rho_B)$. Substituting this into the formula for [mutual information](@entry_id:138718) yields $I(A:B)_{\rho} = S(\rho_A) + S(\rho_B) - (S(\rho_A) + S(\rho_B)) = 0$. This confirms that product states, which by definition lack inter-system correlations, have zero mutual information.

Second, consider a maximally entangled state of two qubits, the Bell state $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$. The joint state $\rho_{AB} = |\Phi^+\rangle\langle\Phi^+|$ is pure, so its entropy $S(\rho_{AB}) = 0$. The reduced states $\rho_A$ and $\rho_B$ are found by tracing out the other subsystem. For this state, both reduced states are maximally mixed: $\rho_A = \rho_B = \frac{1}{2}\mathbb{I}$. The entropy of a maximally mixed qubit is $S(\frac{1}{2}\mathbb{I}) = -\operatorname{Tr}(\frac{1}{2}\mathbb{I} \log_2(\frac{1}{2}\mathbb{I})) = -2 \times (\frac{1}{2} \log_2 \frac{1}{2}) = 1$ bit. Therefore, the mutual information is $I(A:B) = S(\rho_A) + S(\rho_B) - S(\rho_{AB}) = 1 + 1 - 0 = 2$ bits. This is the maximum possible [mutual information](@entry_id:138718) for a [two-qubit system](@entry_id:203437), reflecting the maximal correlations present in a Bell state. 

A crucial property of any valid correlation measure is that correlations cannot be created by local actions. The [quantum mutual information](@entry_id:144024) satisfies this requirement, as it is non-increasing under any local quantum operations, such as local Completely Positive Trace-Preserving (CPTP) maps. This property is known as the **[data processing inequality](@entry_id:142686)**. 

### The Nature of Correlations: Dissecting Quantum Mutual Information

While [quantum mutual information](@entry_id:144024) quantifies the *total* amount of correlation, it does not, by itself, distinguish between correlations of a classical nature and those of a purely quantum origin, such as entanglement.

For **pure bipartite states**, the distinction is simple. If the global state $\rho_{AB} = |\Psi\rangle\langle\Psi|$ is pure, then $S(\rho_{AB})=0$. The **Schmidt decomposition theorem** guarantees that the reduced states $\rho_A$ and $\rho_B$ have the same spectrum of non-zero eigenvalues, and therefore $S(\rho_A) = S(\rho_B)$. This quantity, $S(\rho_A)$, is the **[entanglement entropy](@entry_id:140818)**, the standard measure of entanglement for [pure states](@entry_id:141688). The mutual information thus becomes:

$I(A:B) = S(\rho_A) + S(\rho_B) - S(\rho_{AB}) = S(\rho_A) + S(\rho_A) - 0 = 2S(\rho_A)$

This profound result shows that for [pure states](@entry_id:141688), the total correlation is precisely twice the entanglement. In this context, all correlations are inherently quantum. 

For **[mixed states](@entry_id:141568)**, the picture is more intricate. Consider a classically correlated state, such as $\rho_{AB} = \frac{1}{2}(|00\rangle\langle00| + |11\rangle\langle11|)$. This state is **separable**, meaning it can be written as a convex combination of product states and thus contains no entanglement. However, it is clearly correlated. Its [mutual information](@entry_id:138718) is $I(A:B) = \log_2 2 = 1$ bit. This demonstrates that mutual information captures not just entanglement but also [classical correlations](@entry_id:136367). 

Furthermore, [quantum mutual information](@entry_id:144024) captures complex statistical dependencies that may be invisible to simpler measures. For example, consider a system where a simple two-point correlator, like the covariance of two [observables](@entry_id:267133), vanishes. This does not imply the absence of correlations. We can construct a state where such a simple correlator is zero due to symmetry, yet the [mutual information](@entry_id:138718) is demonstrably positive.

To see this, imagine a [qutrit](@entry_id:146257)-qubit system prepared in the state $\rho_{AB} = \frac{r}{2}|-1,1\rangle\langle-1,1| + (1-r)|0,0\rangle\langle 0,0| + \frac{r}{2}|+1,1\rangle\langle+1,1|$, where the states of the [qutrit](@entry_id:146257) correspond to [energy eigenvalues](@entry_id:144381) $-\epsilon, 0, +\epsilon$ and the qubit to $0, \epsilon$. The connected two-point energy correlator $C_{AB} = \langle H_A H_B \rangle - \langle H_A \rangle \langle H_B \rangle$ can be shown to be exactly zero for all $r \in [0,1]$ due to the symmetric weighting of the states with opposite [energy eigenvalues](@entry_id:144381) for system $A$. However, a direct calculation of the [quantum mutual information](@entry_id:144024) reveals that $I(A:B) = -r \ln(r) - (1-r) \ln(1-r)$ (the [binary entropy](@entry_id:140897)), which is strictly positive for any $r \in (0,1)$. The state is correlated, as the state of one system provides information about the other (e.g., if system B is in state $|0\rangle$, system A must be in state $|0\rangle$). The mutual information correctly captures this, while the two-point energy correlator fails to do so. This highlights the generality of $I(A:B)$ as a measure of [statistical dependence](@entry_id:267552). 

### Quantum Correlations Beyond Entanglement: Quantum Discord

The existence of [separable states](@entry_id:142281) with non-zero mutual information motivates a finer-grained decomposition of total correlations. The key insight is that some quantum states, even without entanglement, possess a "quantumness" that is fragile to local measurements. This leads to the concept of **[quantum discord](@entry_id:145504)**.

The total correlation, $I(A:B)$, can be partitioned into a classical part and a quantum part. The **classical correlation**, $J^{\rightarrow}(A:B)$, is defined as the maximum amount of information one can learn about system $B$ by performing a local measurement on system $A$. A generalized measurement (POVM) on $A$, described by elements $\{\Pi_x\}$, yields outcome $x$ with probability $p_x$, leaving system $B$ in the conditional state $\rho_{B|x}$. The classical information gained is $I(X:B) = S(\rho_B) - \sum_x p_x S(\rho_{B|x})$. Maximizing this over all possible measurements on $A$ gives the classical correlation:

$J^{\rightarrow}(A:B) = \max_{\{\Pi_x\}} \left( S(\rho_B) - \sum_x p_x S(\rho_{B|x}) \right)$

The [quantum discord](@entry_id:145504), $\delta^{\rightarrow}(A:B)$, is then defined as the part of the total correlation that is not captured by this process; it is the "missing information" that cannot be accessed via local measurements on $A$:

$\delta^{\rightarrow}(A:B) = I(A:B) - J^{\rightarrow}(A:B)$

Non-zero discord is a signature of [quantum correlations](@entry_id:136327). All [entangled states](@entry_id:152310) have non-zero discord, but critically, some [separable states](@entry_id:142281) do as well. These are states that possess [quantum correlations](@entry_id:136327) without being entangled.

A prime example is the family of **Werner states**, $\rho_W(p) = p|\Psi^-\rangle\langle\Psi^-| + (1-p)\frac{\mathbb{I}_4}{4}$. These states are known to be separable for $p \le 1/3$. In this regime, the [entanglement of formation](@entry_id:139137) is zero. However, the mutual information is generally non-zero. The maximum [mutual information](@entry_id:138718) that can be achieved in this separable region occurs at the boundary $p=1/3$, where $I(A:B) = \ln(2) - \frac{1}{2}\ln(3) \approx 0.14$ nats. This non-[zero correlation](@entry_id:270141) in an unentangled state is entirely due to [quantum discord](@entry_id:145504).  

The calculation of discord often involves a challenging optimization over all possible measurements. Consider the two-qubit state $\rho_{AB} = \frac{1}{2}|0\rangle\langle 0|_A \otimes |0\rangle\langle 0|_B + \frac{1}{2}|+\rangle\langle +|_A \otimes |1\rangle\langle 1|_B$, where $|+\rangle = (|0\rangle+|1\rangle)/\sqrt{2}$. This state is separable. If one were to measure system $B$ in the computational basis, they would prepare an ensemble of non-orthogonal states ($|0\rangle$ and $|+\rangle$) on system $A$. The impossibility of perfectly distinguishing these non-orthogonal states is the source of [quantum discord](@entry_id:145504). A full calculation shows that for this state, the [quantum mutual information](@entry_id:144024) is $I(A:B) = S(\rho_A)$ and the classical correlation is $J^{\rightarrow}(A:B) = \ln 2 - S(\rho_A)$, leading to a non-zero discord of $\delta^{\rightarrow}(A:B) = 2S(\rho_A) - \ln 2$. This confirms the presence of [quantum correlations](@entry_id:136327) that are destroyed upon measurement. 

### Correlations in a Larger Context: Conditional and Multipartite Systems

The concepts of correlation can be extended to scenarios involving more than two systems, which is essential for understanding open quantum systems where a system interacts with a multi-component environment.

#### Conditional Mutual Information and Quantum Markov Chains

The **quantum [conditional mutual information](@entry_id:139456)** (CMI), $I(A:C|B)$, quantifies the correlation between systems $A$ and $C$ given knowledge of a third system, $B$. It is defined as:

$I(A:C|B) = S(\rho_{AB}) + S(\rho_{BC}) - S(\rho_B) - S(\rho_{ABC})$

A fundamental result in [quantum information theory](@entry_id:141608), the property of **[strong subadditivity](@entry_id:147619)** of von Neumann entropy, is equivalent to the statement that CMI is always non-negative: $I(A:C|B) \ge 0$.

A special case of great importance is when the CMI vanishes. A tripartite state for which $I(A:C|B) = 0$ is called a **quantum Markov chain**, often denoted $A-B-C$. This condition implies that any correlation between $A$ and $C$ is mediated entirely through $B$; once $B$ is known, $A$ and $C$ are effectively independent. This concept is central to the theory of [open quantum systems](@entry_id:138632), where it is often assumed that the successive actions of an environment on a system are uncorrelated, forming a Markovian evolution.

For continuous-variable Gaussian systems, these concepts have direct analogues. A state with a chain-like correlation structure, such as one with a covariance matrix of the form $\boldsymbol{\Gamma} = \begin{pmatrix} \boldsymbol{A}  \boldsymbol{X}  \boldsymbol{0} \\ \boldsymbol{X}^{\top}  \boldsymbol{B}  \boldsymbol{Y} \\ \boldsymbol{0}  \boldsymbol{Y}^{\top}  \boldsymbol{C} \end{pmatrix}$, represents a physical arrangement where $A$ interacts with $B$ and $B$ interacts with $C$, but $A$ and $C$ do not interact directly. One might expect this to form a quantum Markov chain. However, calculation of the CMI (or its Rényi-2 analogue) often reveals a small but non-zero value, indicating that conditioning on $B$ can induce a correlation between $A$ and $C$. This is directly related to the non-vanishing of the conditional cross-covariance between $A$ and $C$ given $B$, which can be computed via the Schur complement of the covariance matrix. The failure of the Markov condition signifies the presence of non-local memory effects in the system's dynamics. 

#### Multipartite Correlations

Generalizing correlation measures to $n$ parties, $A_1, \dots, A_n$, reveals new structural complexities.

A straightforward generalization of mutual information is the **total correlation** or **multi-information**, defined as the difference between the sum of the local entropies and the entropy of the global state:

$T(A_1:\cdots:A_n) = \sum_{i=1}^{n} S(\rho_{A_i}) - S(\rho_{A_1\cdots A_n})$

For any pure $n$-partite state, $S(\rho_{A_1\cdots A_n}) = 0$, so the total correlation is simply the sum of the marginal entropies, $\sum S(\rho_{A_i})$. Let us consider two starkly different $n$-qubit [pure states](@entry_id:141688). The first is the GHZ state, $|\mathrm{GHZ}_n\rangle = \frac{1}{\sqrt{2}}(|0\rangle^{\otimes n} + |1\rangle^{\otimes n})$, which possesses genuine $n$-partite entanglement. The second is a state composed of a product of $n/2$ Bell pairs, e.g., $|\Phi^+\rangle_{12} \otimes |\Phi^+\rangle_{34} \otimes \dots$, which only has pairwise entanglement. In both cases, the reduced state of every single qubit is maximally mixed, with entropy $\ln 2$. Consequently, for both states, the total correlation is $T = n \ln 2$. This illustrates a key limitation of total correlation: it measures the overall amount of information shared among the parties but is completely insensitive to the *structure* of that sharing. It cannot distinguish between genuine multipartite correlations and a collection of bipartite ones. 

To probe this structure, one can define the **interaction information**, which for three parties takes the symmetric form:

$I_3(A:B:C) = S_A + S_B + S_C - S_{AB} - S_{AC} - S_{BC} + S_{ABC}$

This can also be expressed as $I_3(A:B:C) = I(A:B) - I(A:B|C)$. Unlike two-party mutual information, interaction information can be negative.
- **Positive $I_3$** signifies **redundancy**: the correlation between $A$ and $B$ is partially redundant with the information in $C$. Knowing $C$ reduces the correlation between $A$ and $B$, i.e., $I(A:B|C)  I(A:B)$.
- **Negative $I_3$** signifies **synergy**: the correlation between $A$ and $B$ is enhanced by knowledge of $C$, i.e., $I(A:B|C)  I(A:B)$.

For the classical probability distributions resulting from measuring GHZ and W states in the computational basis, the GHZ state exhibits redundancy ($I_3  0$), while the W state exhibits synergy ($I_3  0$). Interestingly, for any pure tripartite quantum state, the quantum interaction information is identically zero, $I_3(A:B:C) \equiv 0$, a direct consequence of the entropy relations for [pure states](@entry_id:141688). 

### A Deeper Link: Mutual Information and Entanglement Measures

While mutual information and entanglement are distinct concepts for [mixed states](@entry_id:141568), the information-theoretic toolkit is foundational for constructing robust measures of entanglement itself.

One of the most important such measures is **[squashed entanglement](@entry_id:141782)**, $E_{\text{sq}}$. It is defined by considering all possible ways the state $\rho_{AB}$ could have arisen from a larger system including an environment $E$. For every such extension $\rho_{ABE}$ where $\operatorname{Tr}_E(\rho_{ABE}) = \rho_{AB}$, one calculates the [conditional mutual information](@entry_id:139456) $I(A:B|E)$. Squashed entanglement is half the [infimum](@entry_id:140118) of this quantity over all possible extensions:

$E_{\text{sq}}(A:B) = \frac{1}{2} \inf_{\rho_{ABE}} I(A:B|E)$

The intuition is that the environment $E$ can "explain away" [classical correlations](@entry_id:136367) between $A$ and $B$, leaving behind only the ineliminable quantum part. This quantity has all the desirable properties of a good entanglement measure (it is an [entanglement monotone](@entry_id:136743)).

A beautiful and reassuring result is that for any **pure state** $\rho_{AB}$, this sophisticated definition reduces to a familiar quantity. For a pure $\rho_{AB}$, any extension must have the form $\rho_{ABE} = \rho_{AB} \otimes \rho_E$. For such a state, the [conditional mutual information](@entry_id:139456) becomes $I(A:B|E) = S(\rho_A) + S(\rho_B) = 2S(\rho_A)$. Since this value is independent of the extension, the [infimum](@entry_id:140118) is trivial, and we find:

$E_{\text{sq}}(A:B) = \frac{1}{2} [2S(\rho_A)] = S(\rho_A)$

For [pure states](@entry_id:141688), [squashed entanglement](@entry_id:141782) equals the [entanglement entropy](@entry_id:140818). Applying this to a Bell state, for which $S(\rho_A)=1$ bit, we find $E_{\text{sq}}(|\Phi^+\rangle) = 1$ bit, as expected for a single ebit of entanglement. This result provides a powerful connection, demonstrating how the fundamental building blocks of [quantum information theory](@entry_id:141608) can be assembled to construct a measure that isolates the purely quantum aspect of correlations. 