## Introduction
The dynamics of chemical and biological systems are fundamentally stochastic, governed by probabilistic events at the molecular level. While [deterministic rate equations](@entry_id:198813) can describe average behaviors, they fail to capture the crucial role of random fluctuations in dictating the timing of key processes, such as the formation of a product, the depletion of a reactant, or the switching between cellular states. To understand these characteristic timescales, a more rigorous, probabilistic framework is required. The Mean First Passage Time (MFPT) provides precisely this tool, offering a way to calculate the average time a [stochastic system](@entry_id:177599) takes to reach a specific state or set of states for the first time.

This article provides a graduate-level introduction to the theory and application of Mean First Passage Times in the context of [reaction networks](@entry_id:203526). It addresses the fundamental question: how can we quantify the timescales of stochastic transitions in complex biological and chemical systems? By bridging the gap between microscopic reaction events and macroscopic observable timings, MFPT analysis offers profound insights into system stability, efficiency, and function.

Across the following chapters, you will build a comprehensive understanding of this powerful concept. The first chapter, **Principles and Mechanisms**, establishes the mathematical foundation by modeling [reaction networks](@entry_id:203526) as Continuous-Time Markov Chains and deriving the central backward Kolmogorov equation for the MFPT. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the framework's utility by exploring its application to real-world problems in cell biology, [pharmacology](@entry_id:142411), and [biophysics](@entry_id:154938), such as quantifying epigenetic stability and [drug-target residence time](@entry_id:189024). Finally, the **Hands-On Practices** chapter provides a series of targeted problems to help you master the computational techniques and theoretical insights discussed. This journey from first principles to practical application will equip you with the essential tools to analyze the temporal dynamics of [stochastic systems](@entry_id:187663).

## Principles and Mechanisms

### Mathematical Framework for Stochastic Reaction Networks

To analyze the temporal evolution of chemical reactions at the molecular level, where stochastic fluctuations are significant, we model the system as a **Continuous-Time Markov Chain (CTMC)**. This formalism provides a rigorous mathematical foundation for describing the probabilistic transitions between discrete system states.

The state of a well-mixed chemical system with $d$ distinct species is defined by a vector of non-negative integers, $\mathbf{X}(t) = (X_1(t), \dots, X_d(t))$, where $X_i(t)$ is the number of molecules of species $i$ at time $t$. The state space is therefore a subset of the integer lattice $\mathbb{Z}_{\ge 0}^d$.

Changes in the state occur through the firing of chemical reactions. The network consists of $R$ reaction channels. Each reaction $r \in \{1, \dots, R\}$ is defined by its **stoichiometric vector**, $\boldsymbol{\nu}_r \in \mathbb{Z}^d$. This vector represents the net change in the molecule counts of each species when one instance of reaction $r$ occurs. If the system is in state $\mathbf{x}$, the firing of reaction $r$ causes an instantaneous transition to the new state $\mathbf{x} + \boldsymbol{\nu}_r$.

The timing of these reactions is governed by **propensity functions**, denoted $a_r(\mathbf{x})$. The quantity $a_r(\mathbf{x}) \mathrm{d}t$ represents the probability that reaction $r$ will occur in an infinitesimal time interval $[t, t+\mathrm{d}t)$, given the system is in state $\mathbf{x}$ at time $t$. For [mass-action kinetics](@entry_id:187487), the propensity $a_r(\mathbf{x})$ is proportional to the number of distinct combinations of reactant molecules available in state $\mathbf{x}$. An important property is that $a_r(\mathbf{x})=0$ if the state $\mathbf{x}$ lacks the necessary reactant molecules for reaction $r$ to fire.

The dynamics of the CTMC are entirely captured by its **[infinitesimal generator](@entry_id:270424)**, often denoted as an operator $\mathcal{L}$ or a matrix $Q$. The generator describes the expected rate of change of any function of the system's state. For any bounded function $f(\mathbf{x})$ defined on the state space, the action of the generator is given by:
$$ (\mathcal{L}f)(\mathbf{x}) = \lim_{h \to 0^+} \frac{\mathbb{E}_{\mathbf{x}}[f(\mathbf{X}(h))] - f(\mathbf{x})}{h} $$
where $\mathbb{E}_{\mathbf{x}}[\cdot]$ denotes the expectation conditional on the system starting in state $\mathbf{x}$ at time $0$.

Using the definition of the propensity functions, we can find an explicit expression for the generator [@problem_id:2654494]. In a small interval $h$, the system can either undergo one reaction $r$ (transitioning to $\mathbf{x}+\boldsymbol{\nu}_r$ with probability $a_r(\mathbf{x})h + o(h)$), or remain in state $\mathbf{x}$ (with probability $1 - \sum_{s=1}^R a_s(\mathbf{x})h + o(h)$). The probability of two or more reactions is negligible ($o(h)$). The expected value of $f(\mathbf{X}(h))$ is thus:
$$ \mathbb{E}_{\mathbf{x}}[f(\mathbf{X}(h))] = f(\mathbf{x})\left(1 - h\sum_{r=1}^R a_r(\mathbf{x})\right) + \sum_{r=1}^R f(\mathbf{x}+\boldsymbol{\nu}_r)a_r(\mathbf{x})h + o(h) $$
Substituting this into the definition of $\mathcal{L}f(\mathbf{x})$ and taking the limit gives the fundamental expression for the generator's action [@problem_id:2654464]:
$$ (\mathcal{L}f)(\mathbf{x}) = \sum_{r=1}^R a_r(\mathbf{x}) [f(\mathbf{x}+\boldsymbol{\nu}_r) - f(\mathbf{x})] $$
This equation elegantly shows that the expected rate of change of $f$ is a sum over all possible reactions, where each term is the rate of a reaction multiplied by the change in $f$ caused by that reaction.

The generator can also be represented as an infinite-dimensional matrix $Q$, where the entry $Q(\mathbf{x}, \mathbf{y})$ gives the [transition rate](@entry_id:262384) from state $\mathbf{x}$ to state $\mathbf{y}$. By comparing the matrix action $(Qf)(\mathbf{x}) = \sum_{\mathbf{y}} Q(\mathbf{x}, \mathbf{y}) f(\mathbf{y})$ with the operator form, we can identify the matrix entries:
-   **Off-diagonal entries**: $Q(\mathbf{x}, \mathbf{x}+\boldsymbol{\nu}_r) = a_r(\mathbf{x})$ for each reaction $r$. All other off-diagonal entries are zero, as no other single transitions are possible.
-   **Diagonal entries**: $Q(\mathbf{x}, \mathbf{x}) = -\sum_{r=1}^R a_r(\mathbf{x})$. This is the negative of the total exit rate from state $\mathbf{x}$.

This structure ensures that the sum of each row in the [generator matrix](@entry_id:275809) is zero: $\sum_{\mathbf{y}} Q(\mathbf{x}, \mathbf{y}) = 0$.

### The Backward Kolmogorov Equation for Mean First Passage Time

A central question in the study of [reaction networks](@entry_id:203526) is determining the characteristic timescale of a process, such as the time until a reactant is fully depleted or a product is first formed. This timescale is quantified by the **Mean First Passage Time (MFPT)**.

Let $A$ be a specific subset of the state space, which we call the **target set**. This set could represent, for example, all states where the number of molecules of a certain species reaches zero. The **[first passage time](@entry_id:271944)** to $A$, denoted $\tau_A$, is the random variable representing the time it takes for the process to first enter any state in $A$. Formally,
$$ \tau_A = \inf\{t \ge 0 : \mathbf{X}(t) \in A\} $$
The MFPT, denoted $m(\mathbf{x})$, is the expected value of this time, given that the process starts in state $\mathbf{x}$:
$$ m(\mathbf{x}) = \mathbb{E}_{\mathbf{x}}[\tau_A] $$

The vector of MFPTs for all possible starting states can be found by solving a [system of linear equations](@entry_id:140416) known as the **backward Kolmogorov equation**. This equation can be derived from a **first-step analysis** [@problem_id:2654484]. Consider a process starting in a state $\mathbf{x}$ that is not in the target set $A$. The total time to reach $A$ can be decomposed into two parts: (1) the time spent waiting for the first reaction to occur, and (2) the time to reach $A$ from the new state after the reaction.

The waiting time in state $\mathbf{x}$ is an exponential random variable with a rate equal to the total exit rate, $\lambda(\mathbf{x}) = \sum_{r=1}^R a_r(\mathbf{x})$. The mean of this waiting time is $1/\lambda(\mathbf{x})$. After this wait, the system jumps to state $\mathbf{x}+\boldsymbol{\nu}_r$ with probability $p_r = a_r(\mathbf{x})/\lambda(\mathbf{x})$. By the law of total expectation and the [memoryless property](@entry_id:267849) of the Markov chain, we can write:
$$ m(\mathbf{x}) = \frac{1}{\lambda(\mathbf{x})} + \sum_{r=1}^R p_r \, m(\mathbf{x}+\boldsymbol{\nu}_r) = \frac{1}{\sum_{s=1}^R a_s(\mathbf{x})} + \sum_{r=1}^R \frac{a_r(\mathbf{x})}{\sum_{s=1}^R a_s(\mathbf{x})} m(\mathbf{x}+\boldsymbol{\nu}_r) $$
Multiplying by $\sum_{s=1}^R a_s(\mathbf{x})$ and rearranging the terms, we find:
$$ -1 = \sum_{r=1}^R a_r(\mathbf{x}) [m(\mathbf{x}+\boldsymbol{\nu}_r) - m(\mathbf{x})] $$
The right-hand side of this equation is precisely the action of the generator operator $\mathcal{L}$ on the MFPT function $m(\mathbf{x})$. This gives us the fundamental backward equation for the MFPT:
$$ (\mathcal{L}m)(\mathbf{x}) = -1, \quad \text{for all } \mathbf{x} \notin A $$
In matrix notation, this is written as $(Qm)(\mathbf{x}) = -1$. The inhomogeneous term $-1$ arises directly from the unit rate at which time accumulates as the process evolves [@problem_id:2654484].

This system of equations must be supplemented with **boundary conditions**. If the process starts in a state $\mathbf{x}$ that is already in the target set $A$, the [first passage time](@entry_id:271944) is zero by definition. Therefore, the boundary condition is:
$$ m(\mathbf{x}) = 0, \quad \text{for all } \mathbf{x} \in A $$
It is crucial to note that this condition applies to *every* state within the target set. This distinguishes the calculation of MFPT to a set from MFPT to a single state; in the former case, the "absorption" occurs as soon as *any* state in the set is hit [@problem_id:2654444].

### Computational Methods for Finite State Spaces

For systems with a finite number of states (or where the state space has been suitably truncated), the backward Kolmogorov equation becomes a solvable system of linear equations. This provides a direct computational method for finding MFPTs.

Let us partition the state space $\mathcal{S}$ into the set of **transient states** $T$ (those outside the target set) and the **absorbing target set** $A$. We can order the states such that all transient states come first, followed by the [absorbing states](@entry_id:161036). The generator matrix $Q$ can then be written in a [block matrix](@entry_id:148435) form:
$$ Q = \begin{pmatrix} Q_{TT} & Q_{TA} \\ \mathbf{0} & \mathbf{0} \end{pmatrix} $$
Here, $Q_{TT}$ is the sub-generator containing rates for transitions between transient states, $Q_{TA}$ contains rates for transitions from transient states to [absorbing states](@entry_id:161036), and the zero blocks indicate that there are no transitions out of the [absorbing set](@entry_id:276794) $A$.

Similarly, we can partition the vector of MFPTs, $m$, into a vector $m_T$ for the transient states and a vector $m_A$ for the [absorbing states](@entry_id:161036). The backward equation $(Qm)(\mathbf{x}) = -1$ for $\mathbf{x} \in T$ and the boundary condition $m(\mathbf{x})=0$ for $\mathbf{x} \in A$ can be written in block form:
$$ Q_{TT} m_T + Q_{TA} m_A = -\mathbf{1} $$
where $\mathbf{1}$ is a column vector of ones. Since the boundary condition dictates that $m_A = \mathbf{0}$, the equation simplifies to:
$$ Q_{TT} m_T = -\mathbf{1} $$
This can be rewritten as $-Q_{TT} m_T = \mathbf{1}$. The matrix $-Q_{TT}$ is invertible (since all its eigenvalues have positive real parts), so we can solve for the MFPTs of the transient states by [matrix inversion](@entry_id:636005):
$$ m_T = -Q_{TT}^{-1} \mathbf{1} $$

**Example: Solving a Finite-State System**
Consider a four-state system $\{S_1, S_2, S_3, S_4\}$ where $T=\{S_1, S_2, S_3\}$ are transient and $A=\{S_4\}$ is absorbing. Let the generator be given by [@problem_id:2654479]:
$$ Q = \begin{pmatrix} -2 & 1 & 0 & 1 \\ 0 & -3 & 2 & 1 \\ 0 & 0 & -3 & 3 \\ 0 & 0 & 0 & 0 \end{pmatrix} $$
The relevant sub-generator for the transient states is:
$$ Q_{TT} = \begin{pmatrix} -2 & 1 & 0 \\ 0 & -3 & 2 \\ 0 & 0 & -3 \end{pmatrix} $$
The MFPTs for the transient states, $m_T = \begin{pmatrix} m_1 & m_2 & m_3 \end{pmatrix}^T$, are found by solving $-Q_{TT} m_T = \mathbf{1}$:
$$ \begin{pmatrix} 2 & -1 & 0 \\ 0 & 3 & -2 \\ 0 & 0 & 3 \end{pmatrix} \begin{pmatrix} m_1 \\ m_2 \\ m_3 \end{pmatrix} = \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix} $$
This system can be solved by back-substitution. From the third row, $3m_3 = 1 \implies m_3 = 1/3$. From the second row, $3m_2 - 2m_3 = 1 \implies 3m_2 - 2(1/3) = 1 \implies m_2 = 5/9$. Finally, from the first row, $2m_1 - m_2 = 1 \implies 2m_1 - 5/9 = 1 \implies m_1 = 7/9$.
The resulting MFPTs are $m_T = \begin{pmatrix} 7/9 & 5/9 & 1/3 \end{pmatrix}^T$.

### Mechanistic Insights from MFPT Decomposition

Beyond providing a single number for a timescale, the MFPT equations offer deep insights into reaction mechanisms. The first-step analysis equation can be used to decompose the total MFPT into contributions from different reaction channels, helping to identify bottlenecks or dominant pathways.

Recall the equation for $m(\mathbf{x})$:
$$ m(\mathbf{x}) = \underbrace{\frac{1}{\sum_s a_s(\mathbf{x})}}_{\text{Waiting Time}} + \underbrace{\sum_r \frac{a_r(\mathbf{x})}{\sum_s a_s(\mathbf{x})} m(\mathbf{x}+\boldsymbol{\nu}_r)}_{\text{Expected Future Time}} $$
This equation shows that the total mean time from state $\mathbf{x}$ is the sum of the mean waiting time in state $\mathbf{x}$ and the expected mean time from whatever state is visited next. The contribution of a specific outgoing channel $r$ to the "Expected Future Time" term is the product of the probability of taking that channel, $p_r = a_r(\mathbf{x})/\sum_s a_s(\mathbf{x})$, and the MFPT from the resulting state, $m(\mathbf{x}+\boldsymbol{\nu}_r)$.

By analyzing these contributions, we can determine which pathway is more influential on the overall timescale. A channel may be dominant because it is highly probable (large $p_r$) or because it leads to a state with a long subsequent MFPT (large $m(\mathbf{x}+\boldsymbol{\nu}_r)$).

Consider a biochemical network with states $A, B, C$ and an absorbing product state $D$ [@problem_id:2654490]. Let the rates be $k_{AB}=1.0$, $k_{AC}=0.1$, $k_{BA}=2.0$, $k_{BD}=0.2$, $k_{CB}=0.05$, and $k_{CD}=5.0$. The MFPT from state $A$, $T_A$, is given by:
$$ T_A = \frac{1}{k_{AB}+k_{AC}} + \frac{k_{AB}}{k_{AB}+k_{AC}} T_B + \frac{k_{AC}}{k_{AB}+k_{AC}} T_C $$
Solving the full system of equations for $T_A, T_B, T_C$ with boundary condition $T_D=0$ yields $T_A \approx 7.76 \text{ s}$, $T_B \approx 7.51 \text{ s}$, and $T_C \approx 0.27 \text{ s}$.

Let's decompose $T_A$:
-   Mean Waiting Time in $A$: $\tau_A = \frac{1}{1.0+0.1} \approx 0.91 \text{ s}$.
-   Contribution from channel $A \to B$: $C_{AB} = \frac{k_{AB}}{k_{AB}+k_{AC}} T_B = \frac{1.0}{1.1} \times 7.51 \approx 6.83 \text{ s}$.
-   Contribution from channel $A \to C$: $C_{AC} = \frac{k_{AC}}{k_{AB}+k_{AC}} T_C = \frac{0.1}{1.1} \times 0.27 \approx 0.025 \text{ s}$.

The total MFPT is $T_A \approx 0.91 + 6.83 + 0.025 = 7.765 \text{ s}$. This analysis clearly shows that despite the $A \to C$ pathway leading to a state ($C$) from which absorption is very fast ($T_C$ is small), its contribution to the total MFPT from $A$ is negligible. The overwhelming contribution comes from the $A \to B$ channel, not because state $B$ is particularly slow, but because the transition $A \to B$ is ten times more probable than $A \to C$. This pathway dominates the overall timescale.

### Advanced Topics in First Passage Time Theory

#### Conditions for Finiteness of MFPT

The methods described above assume that the MFPT is a well-defined, finite quantity. While this is true for many systems of practical interest, especially those on finite state spaces, it is not guaranteed in general. The existence of a finite MFPT depends on the structural properties of the Markov chain [@problem_id:2654468].

A fundamental necessary condition for $m(\mathbf{x}) = \mathbb{E}_{\mathbf{x}}[\tau_A]$ to be finite is that the process must be guaranteed to reach the target set $A$ eventually. That is, the probability of hitting $A$ must be one: $\mathbb{P}_{\mathbf{x}}(\tau_A  \infty) = 1$. If there is a non-zero probability of the process wandering forever without hitting $A$, the expectation of the [first passage time](@entry_id:271944) will be infinite.

However, even if hitting is certain, the MFPT can still be infinite. This occurs in systems that are **[null recurrent](@entry_id:201833)**. An example is a [simple symmetric random walk](@entry_id:276749) on the infinite integer lattice $\mathbb{Z}$. While it is guaranteed to return to any state, the mean time to do so is infinite.

The conditions for a finite MFPT can be summarized as follows:
-   For any CTMC on a **finite state space**, the MFPT from a state $\mathbf{x}$ to a set $A$ is finite if and only if $\mathbb{P}_{\mathbf{x}}(\tau_A  \infty)=1$. This is equivalent to stating that every recurrent (closed communicating) class reachable from $\mathbf{x}$ must have a state in common with $A$.
-   More generally, for CTMCs on infinite state spaces, if the starting state $\mathbf{x}$ and the target set $A$ belong to the same **[positive recurrent](@entry_id:195139)** [communicating class](@entry_id:190016), the MFPT will be finite. Positive recurrence means that the mean time to return to any state within the class is finite.

#### Reversible Networks and Electrical Analogies

A special but important class of [reaction networks](@entry_id:203526) are those that satisfy the property of **detailed balance**. For an irreducible CTMC with a stationary distribution $\pi$ (satisfying $\pi Q = \mathbf{0}$), the system is said to satisfy detailed balance if, for every pair of states $i, j$:
$$ \pi_i q_{ij} = \pi_j q_{ji} $$
This condition implies that in the stationary state, the probabilistic flux from state $i$ to $j$ is exactly balanced by the flux from $j$ to $i$. A CTMC that satisfies detailed balance is also called **time-reversible** [@problem_id:2654455].

Reversibility has profound consequences for the mathematical structure of the system. While the generator matrix $Q$ is generally not symmetric, detailed balance implies that it is symmetric with respect to a [weighted inner product](@entry_id:163877). This allows the non-symmetric MFPT problem, $-Q_{TT} h_T = \mathbf{1}$, to be transformed into an equivalent symmetric system. By defining symmetric edge **conductances** $c_{ij} = \pi_i q_{ij} = c_{ji}$, the backward equation for the MFPT $h_i$ can be rewritten as:
$$ \sum_{j \neq i} c_{ij} (h_i - h_j) = \pi_i, \quad \text{for } i \notin A $$
This equation is identical in form to Kirchhoff's current law for an electrical network where nodes correspond to states, $h_i$ is the [electrical potential](@entry_id:272157) at node $i$, $c_{ij}$ is the conductance of the wire between $i$ and $j$, and $\pi_i$ is an external current injected into node $i$. This powerful analogy allows tools from [potential theory](@entry_id:141424) and circuit theory to be applied to MFPT problems, leading to elegant results such as expressing the mean "[commute time](@entry_id:270488)" between two states in terms of [effective resistance](@entry_id:272328).

#### Quasi-Stationary Distributions and Escape from Metastability

Many [reaction networks](@entry_id:203526) feature **[metastable states](@entry_id:167515)**—long-lived intermediates or sets of states that the system explores for a long time before eventually transitioning to a final [absorbing state](@entry_id:274533). In such cases, the overall MFPT can be dominated by the time spent trapped in the metastable region.

The behavior of the system conditioned on not having yet been absorbed is described by the **[quasi-stationary distribution](@entry_id:753961) (QSD)**, denoted $\alpha$. It is a probability distribution on the transient states $T$ with the property that if the system starts with this distribution, its [conditional distribution](@entry_id:138367) at any later time $t$, given it has not yet been absorbed, remains $\alpha$ [@problem_id:2654443]:
$$ \mathbb{P}_{\alpha}(\mathbf{X}(t) = \mathbf{x} | \tau_A  t) = \alpha_{\mathbf{x}}, \quad \text{for } \mathbf{x} \in T $$
The QSD has a direct connection to the generator. It is the unique positive left eigenvector of the sub-generator $Q_{TT}$ corresponding to its principal eigenvalue (the eigenvalue with the largest real part), which we denote $-\lambda$:
$$ \alpha Q_{TT} = -\lambda \alpha $$
The value $\lambda  0$ has a critical physical meaning: it is the **[escape rate](@entry_id:199818)** from the quasi-stationary state. If the process starts in the QSD, the survival probability (the probability of not being absorbed by time $t$) decays exponentially with this rate: $\mathbb{P}_{\alpha}(\tau_A  t) = \exp(-\lambda t)$.

Consequently, the [mean first passage time](@entry_id:182968) to absorption, when starting from the QSD, is simply the reciprocal of the [escape rate](@entry_id:199818):
$$ \mathbb{E}_{\alpha}[\tau_A] = \frac{1}{\lambda} $$
This result provides a powerful link between the spectral properties of the generator and the macroscopic kinetic rate of escaping a metastable region.

#### Competing Pathways and Conditional MFPTs

In many realistic scenarios, a reactant can proceed through multiple, competing channels to form different, irreversible products. For example, a system might have two distinct [absorbing sets](@entry_id:276239), $P_1$ and $P_2$. Here, two key questions arise: (1) What is the probability that the reaction yields product $P_1$ instead of $P_2$? (2) What is the mean time for this to happen, given that it does happen?

The first question is answered by the **[committor probability](@entry_id:183422)** (or [splitting probability](@entry_id:196942)), $q_{\mathbf{x}}^{P_1}$, which is the probability that a trajectory starting from state $\mathbf{x}$ will reach the set $P_1$ before reaching $P_2$. This quantity is found by solving the homogeneous backward equation $\mathcal{L}q(\mathbf{x})=0$, but with heterogeneous boundary conditions: $q(\mathbf{x})=1$ for all $\mathbf{x} \in P_1$ and $q(\mathbf{x})=0$ for all $\mathbf{x} \in P_2$ [@problem_id:2654475].

The second question requires calculating the **conditional MFPT**, $m_{\mathbf{x}}^{P_1} = \mathbb{E}_{\mathbf{x}}[\tau_{P_1} | \tau_{P_1}  \tau_{P_2}]$. This is the mean time to reach $P_1$ averaged only over those trajectories that are successful in doing so. This quantity does *not* satisfy the standard MFPT equation.

A standard method to compute the conditional MFPT involves a two-step process:
1.  First, solve for the [committor probability](@entry_id:183422) $q_{\mathbf{x}}^{P_1}$ as described above.
2.  Second, solve a modified backward equation for an auxiliary quantity $T_{\mathbf{x}} = q_{\mathbf{x}}^{P_1} m_{\mathbf{x}}^{P_1}$. This quantity satisfies:
    $$ (\mathcal{L}T)(\mathbf{x}) = -q_{\mathbf{x}}^{P_1}, \quad \text{with } T(\mathbf{x})=0 \text{ on } P_1 \cup P_2 $$
3.  Finally, the conditional MFPT is recovered by division: $m_{\mathbf{x}}^{P_1} = T_{\mathbf{x}} / q_{\mathbf{x}}^{P_1}$.

For example, for the [unimolecular reaction](@entry_id:143456) network from [@problem_id:2654475] with reactant $R$, intermediate $I$, and products $P_1, P_2$, one first finds the [committor probability](@entry_id:183422) from $R$ to $P_1$ to be $q_R = 0.25$. Then, by solving the modified backward equation for $T_R$ and $T_I$, one finds $T_R = 7/16 \text{ s}$. The conditional MFPT is then $m_R = T_R/q_R = (7/16)/(1/4) = 1.75 \text{ s}$. This procedure correctly isolates the timescale of a specific reaction channel in the presence of competition.