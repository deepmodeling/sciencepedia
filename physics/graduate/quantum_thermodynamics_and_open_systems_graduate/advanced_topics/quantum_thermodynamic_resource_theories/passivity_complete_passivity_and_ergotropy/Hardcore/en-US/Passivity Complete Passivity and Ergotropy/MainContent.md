## Introduction
The quest to understand and harness energy at the quantum scale is a central pillar of modern physics, driving advancements from quantum computing to [nanoscale engineering](@entry_id:268878). A fundamental question in this domain is: how much useful work can be extracted from a given quantum system? The answer is not always straightforward and requires a precise framework for quantifying non-equilibrium energy and identifying the properties of states that are thermodynamically inert. This article addresses this knowledge gap by introducing the core concepts of [ergotropy](@entry_id:1124640), passivity, and complete passivity, which together form the bedrock for analyzing [work extraction](@entry_id:1134128) in [quantum thermodynamics](@entry_id:140152).

The following chapters will guide you through this essential landscape. First, **Principles and Mechanisms** will lay the theoretical groundwork, rigorously defining [ergotropy](@entry_id:1124640) as the maximum extractable work and distinguishing between passive states (from which no work can be extracted) and completely passive states (which are stable even when multiple copies are available). Next, **Applications and Interdisciplinary Connections** will demonstrate the power of these concepts by applying them to canonical quantum systems, exploring the thermodynamic value of coherence and correlations, and establishing connections to open system dynamics and [resource theories](@entry_id:142789). Finally, **Hands-On Practices** will provide a series of guided problems to solidify your understanding and build practical skills in calculating and interpreting these fundamental thermodynamic quantities.

## Principles and Mechanisms

In the study of quantum thermodynamics, a central question concerns the amount of work that can be extracted from a quantum system. This chapter delves into the fundamental principles governing [work extraction](@entry_id:1134128) from isolated quantum systems under cyclic unitary control. We will define and explore the concepts of **ergotropy**, which quantifies the maximum extractable work, and **passivity**, which characterizes states from which no work can be extracted. This will lead us to the crucial and more subtle distinction between simple passivity and **complete passivity**, ultimately connecting the latter to the familiar notion of thermal equilibrium.

### Ergotropy: The Maximum Extractable Work

Consider a quantum system described by a state $\rho$ and a time-independent Hamiltonian $H$. We wish to extract work by applying an external control, which we model as a unitary evolution $U$ acting on the state. If the process is **cyclic**, meaning the system's Hamiltonian is the same at the beginning and the end of the process, the work $W$ performed on the system is defined as the change in its average energy: $W = \operatorname{Tr}(U\rho U^\dagger H) - \operatorname{Tr}(\rho H)$. The work *extracted from* the system is the negative of this quantity, representing the energy decrease of the system.

The maximum possible work one can extract from the state $\rho$ via any cyclic unitary process is known as the **ergotropy**, denoted $\mathcal{W}(\rho, H)$. It is formally defined as:

$$
\mathcal{W}(\rho,H) \equiv \sup_{U} \left\{ \operatorname{Tr}(\rho H) - \operatorname{Tr}(U\rho U^{\dagger} H) \right\} = \operatorname{Tr}(\rho H) - \inf_{U} \operatorname{Tr}(U\rho U^{\dagger} H)
$$

where the [supremum and infimum](@entry_id:146074) are taken over all possible [unitary operators](@entry_id:151194) $U$ acting on the system's Hilbert space.

To understand how to calculate the [ergotropy](@entry_id:1124640), we must analyze the minimization term $\inf_{U} \operatorname{Tr}(U\rho U^{\dagger} H)$. A key principle of quantum mechanics is that a [unitary transformation](@entry_id:152599) $U\rho U^\dagger$ preserves the spectrum (the set of eigenvalues) of the density operator $\rho$. Therefore, the minimization is performed over all states that are unitarily equivalent to $\rho$, which is known as the **unitary orbit** of $\rho$.

Let the Hamiltonian $H$ have an ordered, non-degenerate spectrum of eigenvalues $E_0  E_1  \dots  E_{d-1}$. Let the state $\rho$ have eigenvalues $r_0 \ge r_1 \ge \dots \ge r_{d-1}$. According to the **rearrangement inequality** from classical mathematics, which has a powerful analogue in [matrix theory](@entry_id:184978), the sum $\sum_i a_i b_i$ is minimized when one sequence is sorted in ascending order and the other in descending order. Applying this to our problem, the [expectation value of energy](@entry_id:174035), $\operatorname{Tr}(\sigma H)$, for a state $\sigma$ with eigenvalues $\{r_k\}$, is minimized when the largest eigenvalue of the state is paired with the [smallest eigenvalue](@entry_id:177333) of the Hamiltonian, and so on.

This minimum-energy state, which we will call the **associated passive state** $\pi_\rho$, is therefore diagonal in the energy [eigenbasis](@entry_id:151409) and has the form:

$$
\pi_\rho = \sum_{k=0}^{d-1} r_k |E_k\rangle\langle E_k|
$$

where $\{r_k\}$ are the eigenvalues of $\rho$ sorted in non-increasing order. The minimum achievable energy is thus $\operatorname{Tr}(\pi_\rho H)$. The ergotropy can therefore be expressed as the difference between the initial energy and the energy of this associated passive state :

$$
\mathcal{W}(\rho,H) = \operatorname{Tr}(\rho H) - \operatorname{Tr}(\pi_\rho H)
$$

This provides a direct algorithm for computing the maximum extractable work: (1) calculate the initial energy $\operatorname{Tr}(\rho H)$; (2) find the eigenvalues of $\rho$; (3) construct the associated passive state $\pi_\rho$ by assigning these eigenvalues, sorted descendingly, as populations to the [energy eigenstates](@entry_id:152154), sorted ascendingly by energy; (4) calculate the energy of this passive state, $\operatorname{Tr}(\pi_\rho H)$; (5) the [ergotropy](@entry_id:1124640) is the difference between these two energies.

For instance, consider a [three-level system](@entry_id:147049) with [energy eigenvalues](@entry_id:144381) $\{0, \epsilon, 3\epsilon\}$ for $\epsilon > 0$. Suppose a state $\rho$ has eigenvalues $\{\frac{1}{2}, \frac{1}{3}, \frac{1}{6}\}$ and its initial populations in the energy basis are $\{0.2, 0.5, 0.3\}$. The initial energy is $\operatorname{Tr}(\rho H) = 0.2 \cdot 0 + 0.5 \cdot \epsilon + 0.3 \cdot 3\epsilon = 1.4\epsilon$. The eigenvalues of $\rho$, sorted descendingly, are $r_0=\frac{1}{2}, r_1=\frac{1}{3}, r_2=\frac{1}{6}$. The minimal energy is achieved by pairing these with the sorted energies $E_0=0, E_1=\epsilon, E_2=3\epsilon$: $\operatorname{Tr}(\pi_\rho H) = \frac{1}{2} \cdot 0 + \frac{1}{3} \cdot \epsilon + \frac{1}{6} \cdot 3\epsilon = (\frac{1}{3} + \frac{1}{2})\epsilon = \frac{5}{6}\epsilon$. The ergotropy is therefore $\mathcal{W}(\rho, H) = 1.4\epsilon - \frac{5}{6}\epsilon = (\frac{7}{5} - \frac{5}{6})\epsilon = \frac{17}{30}\epsilon$ .

### Passive States: The Limits of Work Extraction

The discussion of [ergotropy](@entry_id:1124640) naturally leads to the concept of states from which no work can be extracted. A state $\rho$ is defined as **passive** if its [ergotropy](@entry_id:1124640) is zero, $\mathcal{W}(\rho,H)=0$. This means its energy is already at the minimum possible value for any state on its unitary orbit: $\operatorname{Tr}(\rho H) = \inf_U \operatorname{Tr}(U\rho U^\dagger H)$.

From our previous analysis, this condition is met if and only if the state $\rho$ is identical to its associated passive state $\pi_\rho$. This implies two conditions:
1.  The state $\rho$ must be diagonal in the energy [eigenbasis](@entry_id:151409) of $H$, meaning it commutes with the Hamiltonian: $[\rho, H] = 0$.
2.  The populations of $\rho$ in the energy [eigenbasis](@entry_id:151409), which are its eigenvalues, must be sorted in a non-increasing order with respect to the [energy eigenvalues](@entry_id:144381). That is, if $E_i  E_j$, then the corresponding populations must satisfy $p_i \ge p_j$.

Why does this "energy-ordered" population distribution prevent [work extraction](@entry_id:1134128)? The reason lies deep in the mathematics of unitary transformations . The populations $q_i$ of the final state $U\rho U^\dagger$ in the energy basis are related to the initial populations $p_j$ by the transformation $q_i = \sum_j D_{ij} p_j$, where $D_{ij} = |\langle E_i|U|E_j\rangle|^2$. The matrix $D$ is **doubly stochastic**, meaning its rows and columns all sum to 1. **Birkhoff's theorem** states that any [doubly stochastic matrix](@entry_id:1123952) is a convex combination of permutation matrices. This implies that the final population vector $q$ is a convex combination of permutations of the initial [population vector](@entry_id:905108) $p$.

The final energy is a linear function of these populations, $\sum_i E_i q_i$. The minimum of a linear function over a [convex set](@entry_id:268368) is achieved at an extreme point. Here, the [extreme points](@entry_id:273616) correspond to permutations of the initial populations. By the rearrangement inequality, the sum $\sum_i E_i (P p)_i$ (where $P$ is a permutation) is minimized when the largest probabilities are paired with the smallest energies. For a passive state, the populations are already arranged in this optimal, energy-minimizing configuration. Any [unitary transformation](@entry_id:152599) can only shuffle these populations, leading to a final state with an average energy that is greater than or equal to the initial energy. Thus, no work can be extracted.

A simple illustration is the qubit system . For a Hamiltonian $H = \frac{\omega}{2}\sigma_z$, states can be represented by a Bloch vector $\mathbf{r}$. The energy is $\operatorname{Tr}(\rho H) = \frac{\omega}{2} r_z$. Unitary operations correspond to rotations of the Bloch vector, which preserve its length $|\mathbf{r}|$. The minimum energy is achieved when the vector is rotated to point along the negative $z$-axis, yielding energy $-\frac{\omega}{2}|\mathbf{r}|$. A state is passive if its energy is already at this minimum, i.e., $\frac{\omega}{2} r_z = -\frac{\omega}{2}|\mathbf{r}|$. This implies $r_z = -|\mathbf{r}|$, which is only possible if $r_x=r_y=0$ and $r_z \le 0$. These are states diagonal in the energy basis with population $p_0 \ge p_1$, perfectly matching the general criteria.

### Decomposing Ergotropy: The Roles of Populations and Coherence

When a state is not passive, its ergotropy is positive. This extractable work originates from two distinct quantum features: the non-passive ordering of its populations and the presence of coherences in the energy basis. We can decompose the total [ergotropy](@entry_id:1124640) into two parts reflecting these contributions .

Consider the process of **[dephasing](@entry_id:146545)** a state $\rho$ in the energy [eigenbasis](@entry_id:151409), which destroys all off-diagonal elements (coherences) while preserving the diagonal elements (populations). This is described by the map $\Delta_E(\rho) = \sum_n |E_n\rangle\langle E_n|\rho|E_n\rangle\langle E_n| \equiv \rho_d$. The resulting dephased state $\rho_d$ has the same populations as $\rho$ but no coherences. Crucially, [dephasing](@entry_id:146545) does not change the average energy: $\operatorname{Tr}(\rho_d H) = \operatorname{Tr}(\rho H)$.

The ergotropy of this dephased state, $\mathcal{W}(\rho_d, H)$, represents the work that can be extracted solely by rearranging the initial populations into the optimal passive configuration. We call this the **population ergotropy**, $W_{\text{pop}}$:
$$
W_{\text{pop}} = \mathcal{W}(\rho_d, H) = \operatorname{Tr}(\rho_d H) - \operatorname{Tr}(\pi_{\rho_d} H)
$$
Here, $\pi_{\rho_d}$ is the passive state associated with $\rho_d$, formed by sorting the initial populations $\{p_n\}$ into descending order.

The remainder of the ergotropy must be attributed to the initial coherences. We define the **coherence ergotropy**, $W_{\text{coh}}$, as the difference between the total ergotropy and the population [ergotropy](@entry_id:1124640):
$$
W_{\text{coh}} = \mathcal{W}(\rho, H) - W_{\text{pop}} = (\operatorname{Tr}(\rho H) - \operatorname{Tr}(\pi_\rho H)) - (\operatorname{Tr}(\rho_d H) - \operatorname{Tr}(\pi_{\rho_d} H))
$$
Since $\operatorname{Tr}(\rho H) = \operatorname{Tr}(\rho_d H)$, this simplifies to:
$$
W_{\text{coh}} = \operatorname{Tr}(\pi_{\rho_d} H) - \operatorname{Tr}(\pi_\rho H)
$$
This expression reveals that coherence contributes to ergotropy by lowering the minimum achievable energy. The eigenvalues of the full state $\rho$ are "more spread out" (in the sense of [majorization](@entry_id:147350)) than the populations of its dephased version $\rho_d$, allowing access to a lower-energy passive state $\pi_\rho$.

Let's apply this to a qubit with Hamiltonian $H = \hbar\omega |1\rangle\langle 1|$ and state $\rho = \begin{pmatrix} 0.4   0.2 \\ 0.2   0.6 \end{pmatrix}$ . The dephased state is $\rho_d = \operatorname{diag}(0.4, 0.6)$. Its populations $p_0=0.4, p_1=0.6$ are not passive. The population ergotropy is the work from swapping them: $W_{\text{pop}} = (p_1-p_0)\hbar\omega = (0.6-0.4)\hbar\omega = 0.2\hbar\omega$. To find $W_{\text{coh}}$, we compare the minimal energies. For $\rho_d$, the minimal energy is $0.4\hbar\omega$. For the full state $\rho$, its eigenvalues are $r_0 = \frac{1+\sqrt{0.2}}{2}$ and $r_1 = \frac{1-\sqrt{0.2}}{2}$. The minimal energy is $r_1 \hbar\omega = \frac{1-\sqrt{0.2}}{2}\hbar\omega$. The coherence [ergotropy](@entry_id:1124640) is the difference: $W_{\text{coh}} = (0.4 - \frac{1-\sqrt{0.2}}{2})\hbar\omega = (\frac{\sqrt{5}-1}{10})\hbar\omega$.

### Beyond Single-Copy Passivity: Activation and Complete Passivity

If a state is passive, we cannot extract work from a single copy. But what if we have access to multiple identical copies of the system? This leads to a stronger notion of stability known as **complete passivity**. A state $\rho$ is completely passive if the $n$-copy state $\rho^{\otimes n}$ is passive with respect to the total Hamiltonian $H^{(n)} = \sum_{k=1}^n I^{\otimes(k-1)} \otimes H \otimes I^{\otimes(n-k)}$ for all positive integers $n$.

Remarkably, a state can be passive but not completely passive. This means that while a single copy is useless as a work source, a collection of copies can be "activated" to produce work. This phenomenon is known as the **activation of work** .

Consider a [three-level system](@entry_id:147049) with energies $E_0=0, E_1=2, E_2=3$ (in some energy units) and a diagonal state $\rho$ with populations $p_0=0.5, p_1=0.4, p_2=0.1$ . Since the populations are ordered non-increasingly with energy ($0.5  0.4  0.1$), the state $\rho$ is passive.

Now, let's examine the two-copy state $\rho^{\otimes 2}$. Its [eigenstates](@entry_id:149904) are $|ij\rangle$ with energies $E_{ij}=E_i+E_j$ and populations $P_{ij}=p_i p_j$. Let's compare two specific energy levels of the two-copy system:
-   The state $|02\rangle$ has energy $E_{02} = E_0 + E_2 = 3$ and population $P_{02} = p_0 p_2 = 0.5 \times 0.1 = 0.05$.
-   The state $|11\rangle$ has energy $E_{11} = E_1 + E_1 = 4$ and population $P_{11} = p_1 p_1 = 0.4 \times 0.4 = 0.16$.

We have found that $E_{02}  E_{11}$, but the corresponding populations violate the passivity condition, $P_{02}  P_{11}$. This is a **[population inversion](@entry_id:155020)**. Because of this inversion, the two-copy state $\rho^{\otimes 2}$ is not passive. A [unitary operator](@entry_id:155165) that swaps the states $|02\rangle$ and $|11\rangle$ can lower the system's average energy, thereby extracting work. By performing the full ergotropy calculation for $\rho^{\otimes 2}$, we would find a non-zero value, confirming that work has been activated.

### The Structure of Completely Passive States: Thermal Equilibrium

The example above shows that the condition for complete passivity is much more stringent than for simple passivity. The requirement that for all $n$, the product populations $P_{\vec{i}} = p_{i_1}\cdots p_{i_n}$ must be ordered non-increasingly with the sum of energies $E_{\vec{i}} = E_{i_1}+\cdots+E_{i_n}$, imposes a powerful constraint on the initial populations $\{p_i\}$.

A foundational theorem of quantum thermodynamics states that a state $\rho$ is completely passive if and only if it is a **Gibbs state** (or thermal state) for some non-negative inverse temperature $\beta \ge 0$ :

$$
\rho = \rho_\beta = \frac{\exp(-\beta H)}{Z}, \quad \text{where } Z = \operatorname{Tr}[\exp(-\beta H)]
$$

The populations of such a state take the familiar Boltzmann form, $p_i = \frac{1}{Z}\exp(-\beta E_i)$. One can see intuitively why this form guarantees complete passivity. If $E_{\vec{i}}  E_{\vec{j}}$, then $\sum_k E_{i_k}  \sum_k E_{j_k}$. For $\beta \ge 0$, this implies $-\beta E_{\vec{i}} > -\beta E_{\vec{j}}$, and therefore $\exp(-\beta E_{\vec{i}}) > \exp(-\beta E_{\vec{j}})$. This means the corresponding product populations $P_{\vec{i}}$ and $P_{\vec{j}}$ will always be correctly ordered.

Conversely, for the population ordering to hold for arbitrary combinations of energies, the relationship between populations and energies must be exponential . For any two levels $i,j$, the ratio must be $p_i/p_j = \exp(-\beta(E_i - E_j))$ for a single, consistent $\beta$. This provides a practical test: a diagonal state is a Gibbs state if and only if the quantity $-\frac{\ln(p_i/p_j)}{E_i - E_j}$ yields the same value of $\beta$ for all pairs of distinct energy levels . Any passive state that does not satisfy this strict condition (e.g., the one in our activation example) is not completely passive.

### Subtleties of Degenerate Spectra

The discussion so far has implicitly assumed non-degenerate Hamiltonians. The presence of **degeneracy**, where multiple orthogonal states share the same energy, introduces important subtleties, particularly regarding the role of coherence .

For a single copy, the condition for passivity, $[\rho, H] = 0$, only requires that the [density matrix](@entry_id:139892) be block-diagonal with respect to the degenerate [eigenspaces](@entry_id:147356) of $H$. It does *not* forbid coherences *within* a degenerate subspace. A [unitary transformation](@entry_id:152599) $V$ that acts non-trivially only within a single degenerate [eigenspace](@entry_id:150590) commutes with $H$, $[V,H]=0$. Such a transformation can create or remove intra-[eigenspace](@entry_id:150590) coherences, but it leaves the average energy $\operatorname{Tr}(\rho H)$ unchanged. Since the spectrum of $\rho$ is also unchanged, the [ergotropy](@entry_id:1124640) $\mathcal{W}(\rho, H)$ is invariant. Therefore, coherence confined to a degenerate energy [eigenspace](@entry_id:150590) has no effect on the passivity or ergotropy of a single copy of a state.

The situation is entirely different for complete passivity. A completely passive state must be a Gibbs state, $\rho_\beta = Z^{-1}\exp(-\beta H) = Z^{-1}\sum_E \exp(-\beta E)\Pi_E$, where $\Pi_E$ is the projector onto the [eigenspace](@entry_id:150590) of energy $E$. This form dictates that within any degenerate [eigenspace](@entry_id:150590), the state must be proportional to the [identity operator](@entry_id:204623) for that subspace—it must be **maximally mixed**. Any deviation from this, such as having non-uniform populations for different states within the same degenerate subspace, creates an "internal anisotropy". While this anisotropy is not a source of work for a single copy, it constitutes a resource that can be activated when multiple copies are available, breaking complete passivity. Thus, for a state to be completely passive in the presence of degeneracies, it must not only have Boltzmann-distributed populations across different energies but also be completely isotropic within each energy level.