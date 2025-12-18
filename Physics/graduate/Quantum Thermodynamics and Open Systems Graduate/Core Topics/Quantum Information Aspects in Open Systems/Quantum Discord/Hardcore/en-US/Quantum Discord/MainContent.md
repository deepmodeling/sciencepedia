## Introduction
In the quest to understand the quantum world, correlations between systems play a central role. For decades, entanglement was considered the definitive signature of "quantumness," but this view is incomplete. A significant knowledge gap emerged with the discovery that some quantum states, while not entangled, still harbor correlations that defy classical explanation. This article delves into **Quantum Discord**, the measure developed to quantify these more general, non-[classical correlations](@entry_id:136367). We will embark on a comprehensive exploration, beginning with the foundational **Principles and Mechanisms**, where we will define discord and contrast it with entanglement. Following this, the chapter on **Applications and Interdisciplinary Connections** will reveal discord's surprising relevance in fields from [condensed matter](@entry_id:747660) physics to cosmology. Finally, a **Hands-On Practices** section will solidify your understanding by guiding you through concrete calculations for key quantum states. This journey will illuminate why discord is a crucial concept for a modern understanding of quantum information and its physical manifestations.

## Principles and Mechanisms

In the study of [composite quantum systems](@entry_id:193313), understanding the nature and extent of correlations between subsystems is of paramount importance. While entanglement has historically been considered the hallmark of [quantum correlations](@entry_id:136327), it has become clear that it does not capture the full spectrum of non-[classical correlations](@entry_id:136367). There exist [mixed quantum states](@entry_id:262127) that are separable (and thus not entangled) but whose correlations still exhibit distinctly quantum features. Quantum discord is a measure designed to quantify these more general [quantum correlations](@entry_id:136327), capturing the "quantumness" that persists even in the absence of entanglement. This chapter elucidates the fundamental principles defining quantum discord, explores its key properties and operational meanings, and discusses important generalizations.

### Total Correlations and Quantum Mutual Information

The natural starting point for quantifying correlations in any system, classical or quantum, is mutual information. For a bipartite quantum system $AB$ described by a density operator $\rho_{AB}$, the **[quantum mutual information](@entry_id:144024)** serves as the measure of total correlation between subsystems $A$ and $B$. It is defined in direct analogy to the classical Shannon mutual information, but with the Shannon entropy replaced by the **von Neumann entropy**, $S(\rho) = -\mathrm{Tr}(\rho \ln \rho)$.

The [quantum mutual information](@entry_id:144024) is given by:
$I(A:B) = S(\rho_A) + S(\rho_B) - S(\rho_{AB})$
where $\rho_A = \mathrm{Tr}_B(\rho_{AB})$ and $\rho_B = \mathrm{Tr}_A(\rho_{AB})$ are the reduced density operators of the subsystems.

This quantity has a profound information-theoretic interpretation as a measure of distance. The [quantum mutual information](@entry_id:144024) is equal to the **[quantum relative entropy](@entry_id:144397)** between the actual state $\rho_{AB}$ and the uncorrelated product state of its marginals, $\rho_A \otimes \rho_B$ :
$I(A:B) = D(\rho_{AB} \Vert \rho_A \otimes \rho_B) = \mathrm{Tr}[\rho_{AB}(\ln \rho_{AB} - \ln(\rho_A \otimes \rho_B))]$
Since relative entropy is a measure of distinguishability between two states, $I(A:B)$ quantifies how distinguishable the actual correlated state $\rho_{AB}$ is from the "un-correlated" state $\rho_A \otimes \rho_B$. It is zero if and only if $\rho_{AB} = \rho_A \otimes \rho_B$.

The behavior of [quantum mutual information](@entry_id:144024) highlights its role as a measure of total correlation. For a pure bipartite state $|\psi\rangle_{AB}$, the global entropy $S(\rho_{AB})$ is zero, and the local entropies are equal, $S(\rho_A) = S(\rho_B) = E(|\psi\rangle)$, where $E$ is the entropy of entanglement. In this case, the [mutual information](@entry_id:138718) becomes $I(A:B) = 2S(\rho_A)$, twice the [entanglement entropy](@entry_id:140818) . This signifies that for [pure states](@entry_id:141688), all correlations are quantum and are captured by entanglement. Conversely, for a "classical-classical" state, which is diagonal in a product basis, $\rho_{AB} = \sum_{i,j} p_{ij} |i\rangle\langle i|_A \otimes |j\rangle\langle j|_B$, the [quantum mutual information](@entry_id:144024) exactly equals the Shannon [mutual information](@entry_id:138718) of the classical probability distribution $\{p_{ij}\}$ .

### Classical Correlations and The Asymmetry of Measurement

While $I(A:B)$ quantifies the total correlations, a central insight in the development of quantum discord is that these correlations can be divided into classical and quantum parts. This division hinges on the role of local measurement.

In [classical information theory](@entry_id:142021), [mutual information](@entry_id:138718) can also be expressed as the reduction in uncertainty about one variable given knowledge of the other: $I(X:Y) = H(Y) - H(Y|X)$. The quantum analogue of this involves performing a local measurement on one subsystem, say $A$, to gain information about the other, $B$. A general measurement on $A$ is described by a Positive Operator-Valued Measure (POVM), a set of operators $\{\Pi_k^A\}$ on $\mathcal{H}_A$ such that $\Pi_k^A \ge 0$ and $\sum_k \Pi_k^A = \mathbb{I}_A$. When outcome $k$ is obtained with probability $p_k = \mathrm{Tr}[(\Pi_k^A \otimes \mathbb{I}_B)\rho_{AB}]$, the state of system $B$ is updated to $\rho_{B|k}$. The average uncertainty about $B$ that remains after the measurement on $A$ is given by the average [conditional entropy](@entry_id:136761), $\sum_k p_k S(\rho_{B|k})$.

The information gained about $B$ by this specific measurement on $A$ is thus $S(\rho_B) - \sum_k p_k S(\rho_{B|k})$. To find the total amount of classical correlation, one must find the measurement on $A$ that maximizes this information gain. This leads to the definition of **classical correlation** :
$J_{B|A}(\rho_{AB}) = \max_{\{\Pi_k^A\}} \left[ S(\rho_B) - \sum_k p_k S(\rho_{B|k}) \right]$
The quantity $J_{B|A}$ represents the maximum classical information about $B$ that can be extracted by performing a local measurement on $A$.

### Defining Quantum Discord

The two expressions for [mutual information](@entry_id:138718) that are equivalent in classical theory are generally not equivalent in quantum theory. Quantum discord is defined as the difference between them. The **quantum discord**, measuring correlations from $A$ to $B$, is defined as the total correlation minus the accessible classical correlation  :
$\mathcal{D}_{B|A}(\rho_{AB}) = I(A:B) - J_{B|A}$

This quantity represents the portion of the total correlation that is "lost" or made inaccessible by the act of local measurement. It is the minimal amount of correlation that is destroyed by even the most careful, optimal local measurement on subsystem $A$. It therefore quantifies the inherently quantum nature of the correlations—the part that cannot be accessed without disturbing the system in a way that prevents full retrieval of the information. This gives discord its interpretation as **locally inaccessible information** .

A crucial feature of quantum discord is its **asymmetry**. The definition of classical correlation $J_{B|A}$ involves a maximization over measurements on subsystem $A$. One can analogously define $J_{A|B}$ by maximizing over measurements on subsystem $B$. Since these are different optimization problems, in general $J_{B|A} \neq J_{A|B}$. As the total [mutual information](@entry_id:138718) $I(A:B)$ is symmetric, the discord is inherently asymmetric:
$\mathcal{D}_{B|A} \neq \mathcal{D}_{A|B}$
This asymmetry reflects the directional nature of measurement in probing correlations.

A state has zero discord, $\mathcal{D}_{B|A}(\rho_{AB}) = 0$, if and only if it is a **classical-quantum state** with respect to system A, meaning it can be written in the form :
$\rho_{AB} = \sum_k p_k |k\rangle\langle k|_A \otimes \rho_B^k$
where $\{|k\rangle_A\}$ is an [orthonormal basis](@entry_id:147779) for $A$. For such states, there exists a [projective measurement](@entry_id:151383) on $A$ (in the basis $\{|k\rangle_A\}$) that reveals which state $\rho_B^k$ system $B$ is in without disturbing the correlations. Conversely, if a state is not of this form, no local measurement on $A$ can perfectly reveal information about $B$ without introducing some disturbance, resulting in non-zero discord. An explicit example can be constructed using such a classical-quantum state, for which measuring the "classical" subsystem A yields zero discord ($\mathcal{D}_{B|A}=0$), while measuring the "quantum" subsystem B (whose states may be non-orthogonal) yields a non-zero discord ($\mathcal{D}_{A|B}>0$) .

### Quantum Discord versus Entanglement

A central motivation for studying quantum discord is that it captures [quantum correlations](@entry_id:136327) beyond entanglement. While all [entangled states](@entry_id:152310) have non-zero discord, the converse is not true: there exist [separable states](@entry_id:142281) that possess non-zero quantum discord.

For [pure states](@entry_id:141688), discord is equivalent to entanglement. A pure bipartite state $|\psi\rangle_{AB}$ has a discord (measured on either side) equal to its entropy of entanglement: $\mathcal{D}_{B|A} = \mathcal{D}_{A|B} = S(\rho_A)$ . However, for [mixed states](@entry_id:141568), the picture is richer.

The canonical example is the family of two-qubit **Werner states**, which can be conceptualized as a mixture of a maximally entangled [singlet state](@entry_id:154728) $|\Psi^-\rangle = (|01\rangle - |10\rangle)/\sqrt{2}$ and a maximally [mixed state](@entry_id:147011) $\mathbb{I}_4/4$:
$\rho_{AB}(p) = (1-p) \frac{\mathbb{I}_4}{4} + p |\Psi^-\rangle\langle\Psi^-|$
It is known that this state is entangled for $p > 1/3$ and separable for $p \le 1/3$. Let us consider the boundary case $p=1/3$, where the state is separable. A detailed calculation  reveals the following quantities (using natural logarithms):
-   Total Mutual Information: $I(\rho_{AB}) = \ln(2) - \frac{1}{2}\ln(3)$
-   Classical Correlation: $J_{B|A}(\rho_{AB}) = \frac{5}{3}\ln(2) - \ln(3)$
-   Quantum Discord: $\mathcal{D}_{B|A}(\rho_{AB}) = I(\rho_{AB}) - J_{B|A}(\rho_{AB}) = \frac{1}{2}\ln(3) - \frac{2}{3}\ln(2) > 0$

This result is profound. The state at $p=1/3$ contains no entanglement, yet it possesses non-zero quantum discord. This demonstrates unequivocally that discord is a more general indicator of [quantum correlations](@entry_id:136327). These are correlations that are non-classical (as evidenced by $\mathcal{D}>0$) but not strong enough to constitute entanglement. The existence of such states refutes the naive assumption that all [quantum correlations](@entry_id:136327) are synonymous with entanglement, or that [separable states](@entry_id:142281) are "classical" in all respects .

### The Operational Significance of Discord

The utility of quantum discord is not merely classificatory; it has tangible operational consequences in both thermodynamics and computation.

#### A Thermodynamic Resource

In the framework of quantum thermodynamics, correlations represent a resource from which work can be extracted. Consider a "quantum Maxwell's demon" or Szilard engine that attempts to extract work from a bipartite state $\rho_{AB}$ coupled to a [heat bath](@entry_id:137040) at temperature $T$. The total correlation, quantified by $k_B T I(A:B)$, represents the total information-theoretic resource available. The portion of this resource that can be converted into useful work through local operations on one subsystem and classical communication is limited by the accessible classical correlation, $W_{\text{ext,max}} = k_B T J_{B|A}$.

The remaining part of the correlation, the quantum discord, cannot be converted into work. Instead, the very act of measurement required to access the classical information causes an unavoidable disturbance or "back-action" on the system. This disturbance leads to irreversible [entropy production](@entry_id:141771). The minimal heat dissipated to the environment during an optimal cycle of measurement, feedback, and memory erasure is directly proportional to the quantum discord :
$Q_{\min} = k_B T \mathcal{D}_{B|A}(\rho_{AB})$

Thus, discord acquires a clear physical meaning: it is the thermodynamic cost of accessing classical information from a quantum system. It quantifies the fundamental [irreversibility](@entry_id:140985) inherent in [quantum measurement](@entry_id:138328). This can also be viewed as a **work deficit**: the difference between the [maximum work](@entry_id:143924) extractable under global [quantum control](@entry_id:136347) and that extractable under local measurement is determined by discord .

#### A Computational Resource

Quantum discord also emerges as a key resource in certain models of [quantum computation](@entry_id:142712) that exhibit a [quantum advantage](@entry_id:137414) without significant entanglement. The paradigmatic example is **Deterministic Quantum Computation with One Qubit (DQC1)** .

The DQC1 model uses a single pure control qubit ($A$) and a register of $n$ qubits in a maximally mixed state ($B$) to efficiently estimate the normalized trace of a large $2^n \times 2^n$ [unitary matrix](@entry_id:138978) $U$. The algorithm involves preparing an input state, applying a controlled-$U$ operation, and then measuring only the control qubit. The [expectation values](@entry_id:153208) of the control qubit's [observables](@entry_id:267133) reveal the real and imaginary parts of $\mathrm{Tr}(U)/2^n$. This task is believed to be hard for classical computers, yet the [quantum algorithm](@entry_id:140638) requires resources that scale only polynomially in $n$.

Analysis of the final state $\rho_{AB}$ in the DQC1 protocol reveals that for large $n$, the entanglement between the control qubit and the mixed register is negligible. However, the quantum discord $\mathcal{D}_{B|A}$ is generally non-zero and is directly related to the magnitude of the trace being estimated. It is this non-zero discord that facilitates the information flow from the global properties of the unitary $U$ (acting on $B$) to the local [observables](@entry_id:267133) of the control qubit $A$. It has been shown that any quantum circuit that generates zero discord at every step is efficiently simulable by a classical computer. Therefore, the generation of non-zero discord is a necessary condition for the [quantum speedup](@entry_id:140526) observed in this model, establishing discord as a genuine computational resource.

### Advanced Topics: Alternative and Generalized Discord Measures

The original definition of discord, based on von Neumann entropy, is not the only way to formalize the concept. Research has explored various alternative definitions, each with its own strengths and weaknesses.

#### Geometric Discord

An intuitive alternative is to define discord geometrically as the minimal distance from the given state $\rho_{AB}$ to the set of classical-quantum (zero-discord) states.
$D_d(\rho_{AB}) = \min_{\chi \in \Omega_0} d(\rho_{AB}, \chi)$
where $d$ is some distance measure and $\Omega_0$ is the set of states with zero discord. A common choice for the distance measure is the squared **Hilbert-Schmidt distance**, $d_{\mathrm{HS}}(\rho, \sigma) = \|\rho - \sigma\|_2^2 = \mathrm{Tr}[(\rho - \sigma)^2]$.

The Hilbert-Schmidt geometric discord, $D_{\mathrm{HS}}$, is computationally accessible for certain classes of states. For instance, for two-qubit Bell-diagonal states, it is given by the sum of the squares of the two smaller correlation coefficients . However, $D_{\mathrm{HS}}$ suffers from a serious deficiency: it is not a **monotonic** measure under local operations on the unmeasured subsystem. That is, there exist local CPTP maps $\Lambda_B$ such that $D_{\mathrm{HS}}((\mathrm{id}_A \otimes \Lambda_B)(\rho_{AB})) > D_{\mathrm{HS}}(\rho_{AB})$ . This is a pathological property for any quantity intended to be a quantum resource, as local actions by one party should not be able to create the resource out of thin air.

This issue stems from the fact that the Hilbert-Schmidt distance itself is not contractive under all CPTP maps. A well-behaved alternative is to use a distance that is contractive, such as the **Bures distance**, which is derived from the Uhlmann fidelity. A geometric discord based on the Bures distance, $D_{\mathrm{B}}$, can be proven to be a proper monotone, resolving the key issue with the Hilbert-Schmidt version .

#### Rényi-α Generalizations

Another important direction is the generalization of discord using the family of **Rényi-$\alpha$ entropies**, $S_\alpha(\rho) = \frac{1}{1-\alpha} \ln \mathrm{Tr}[\rho^\alpha]$, which reduce to the von Neumann entropy as $\alpha \to 1$.

A straightforward generalization, $D_\alpha^{(E)}$, can be defined by replacing all von Neumann entropies in the original definition with Rényi-$\alpha$ entropies. While this entropic Rényi discord correctly reduces to the standard discord for $\alpha=1$ and to the Rényi entropy of entanglement for [pure states](@entry_id:141688), it inherits the problematic properties of the Rényi entropy itself . Specifically, for $\alpha \neq 1$, it is not guaranteed to be non-negative or monotonic under local operations on the unmeasured party, limiting its utility as a resource [quantifier](@entry_id:151296).

A more robust generalization is constructed using the **sandwiched Rényi divergence**, $\tilde{D}_\alpha(\rho \| \sigma)$, a quantity that satisfies the crucial data-processing inequality (i.e., it is monotonic under CPTP maps) for $\alpha \in [1/2, \infty)$. Defining a Rényi mutual information as $\tilde{I}_\alpha(\rho_{AB}) = \tilde{D}_\alpha(\rho_{AB} \| \rho_A \otimes \rho_B)$ leads to a discord measure, $\tilde{D}_\alpha^{(\text{disc})}$, that is guaranteed to be non-negative and monotonic under local operations on the unmeasured party .

This family of discords finds a compelling operational interpretation in the context of **single-shot [quantum thermodynamics](@entry_id:140152)**. Generalized free energies based on the sandwiched Rényi divergence quantify the work extractable from a system in a single experimental run, with the parameter $\alpha$ tuning the nature of the guarantee from typical-case to worst-case scenarios. This provides a clear thermodynamic meaning to this class of well-behaved Rényi discords, a feature the simpler entropic version lacks . These advanced formulations underscore that while the core concept of discord is simple, its rigorous and operationally meaningful quantification is a subtle and active area of research.