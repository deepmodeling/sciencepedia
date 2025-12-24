## Introduction
The first law of thermodynamics is a fundamental principle of energy conservation. Extending this cornerstone of physics into the quantum realm, especially for open systems that interact with their environment, requires a rigorous and nuanced framework. How do we precisely define and distinguish between between [heat and work](@entry_id:144159) for a quantum system exchanging energy, particles, and information with its surroundings? A simple application of classical ideas is insufficient and can lead to paradoxes. This article addresses this knowledge gap by developing a consistent thermodynamic description for [open quantum systems](@entry_id:138632).

Across the following chapters, this article provides a comprehensive exploration of this topic. The first chapter, **Principles and Mechanisms**, establishes the foundational definitions of quantum [heat and work](@entry_id:144159), connects them to the system's dynamics via master equations, and discusses subtleties in both weak and strong coupling regimes. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the power of this framework by applying it to [quantum thermal machines](@entry_id:1130419), transport phenomena, and information theory. Finally, the **Hands-On Practices** section offers concrete problems to solidify the reader's understanding of these core concepts.

## Principles and Mechanisms

The first law of thermodynamics, a cornerstone of classical physics, is a statement of energy conservation. It posits that the change in a system's internal energy, $U$, is equal to the heat, $Q$, supplied to the system plus the work, $W$, done on it. In the context of [open quantum systems](@entry_id:138632), which [exchange energy](@entry_id:137069) and information with their surroundings, this law requires a careful and precise formulation. The principles and mechanisms governing this energy exchange are not only fundamental to understanding the thermodynamics of quantum processes but also underpin the development of [quantum thermal machines](@entry_id:1130419) and information engines.

### The First Law for Open Quantum Systems

Let us consider a quantum system, which we will call the *system of interest* or simply the *system*, described by a Hilbert space $\mathcal{H}_S$ and a possibly time-dependent Hamiltonian $H_S(t)$. Its state is given by the density operator $\rho_S(t)$. The **internal energy** of this system at time $t$ is defined as the [expectation value](@entry_id:150961) of its Hamiltonian:

$U(t) = \mathrm{Tr}[\rho_S(t) H_S(t)]$

The rate of change of the internal energy can be found by applying the product rule for differentiation:

$\dot{U}(t) = \frac{d}{dt}\mathrm{Tr}[\rho_S(t) H_S(t)] = \mathrm{Tr}[\dot{\rho}_S(t) H_S(t)] + \mathrm{Tr}[\rho_S(t) \dot{H}_S(t)]$

This expression naturally separates the total energy change into two distinct contributions, providing the foundation for the [first law of thermodynamics](@entry_id:146485) in the quantum regime.

The first term, which involves the change in the system's Hamiltonian $\dot{H}_S(t)$, represents the energy change due to the action of an external agent or control field that explicitly modifies the system's energy structure. This is identified as the **power**, or the rate of work done on the system:

$\dot{W}(t) = \mathrm{Tr}[\rho_S(t) \dot{H}_S(t)]$

The second term, which involves the change in the system's state $\dot{\rho}_S(t)$, represents the energy flow resulting from the system's interaction with its environment for a given Hamiltonian. This is identified as the **[heat rate](@entry_id:1125980)** or **heat current**:

$\dot{Q}(t) = \mathrm{Tr}[\dot{\rho}_S(t) H_S(t)]$

With these definitions, the first law for [open quantum systems](@entry_id:138632) takes the familiar differential form:

$\dot{U}(t) = \dot{Q}(t) + \dot{W}(t)$

To make these abstract definitions concrete, consider a paradigmatic example: a single [two-level system](@entry_id:138452) (qubit) subjected to external driving. Let its Hamiltonian be $H_S(t) = \frac{\omega}{2}\sigma_z + \Omega(t)\sigma_x$, where $\omega$ is a constant [energy splitting](@entry_id:193178) and $\Omega(t)$ is a time-dependent driving amplitude. The state of the qubit can be described by the Bloch vector $\mathbf{r}(t) = (r_x, r_y, r_z)$, such that $\rho_S(t) = \frac{1}{2}(I + \mathbf{r}(t) \cdot \boldsymbol{\sigma})$, where $\boldsymbol{\sigma} = (\sigma_x, \sigma_y, \sigma_z)$ is the vector of Pauli matrices.

The power is found by first computing the time derivative of the Hamiltonian, $\dot{H}_S(t) = \dot{\Omega}(t)\sigma_x$. The power is then:

$\dot{W}(t) = \mathrm{Tr}[\rho_S(t) \dot{H}_S(t)] = \mathrm{Tr}\left[\frac{1}{2}(I + r_x\sigma_x + r_y\sigma_y + r_z\sigma_z) \dot{\Omega}(t)\sigma_x\right]$

Using the linearity and cyclic property of the trace, along with the fundamental identities $\mathrm{Tr}[\sigma_i] = 0$ and $\mathrm{Tr}[\sigma_i \sigma_j] = 2\delta_{ij}$, this simplifies to:

$\dot{W}(t) = \frac{1}{2}\dot{\Omega}(t) (r_x \mathrm{Tr}[\sigma_x^2]) = \dot{\Omega}(t) r_x(t)$

The power is directly proportional to the rate of change of the driving field and the system's coherence in the direction of the drive, $r_x = \langle \sigma_x \rangle$.

The heat rate is given by $\dot{Q}(t) = \mathrm{Tr}[H_S(t) \dot{\rho}_S(t)]$. Since the time derivative of the density matrix is $\dot{\rho}_S(t) = \frac{1}{2}(\dot{r}_x\sigma_x + \dot{r}_y\sigma_y + \dot{r}_z\sigma_z)$, the [heat rate](@entry_id:1125980) becomes:

$\dot{Q}(t) = \mathrm{Tr}\left[ \left(\frac{\omega}{2}\sigma_z + \Omega(t)\sigma_x\right) \frac{1}{2}(\dot{r}_x\sigma_x + \dot{r}_y\sigma_y + \dot{r}_z\sigma_z) \right]$

Again, applying the [trace identities](@entry_id:188149), only the terms with matching Pauli matrices survive:

$\dot{Q}(t) = \frac{1}{2} \left( \frac{\omega}{2} \dot{r}_z \mathrm{Tr}[\sigma_z^2] + \Omega(t) \dot{r}_x \mathrm{Tr}[\sigma_x^2] \right) = \frac{\omega}{2}\dot{r}_z(t) + \Omega(t)\dot{r}_x(t)$

These expressions for $\dot{W}(t)$ and $\dot{Q}(t)$ provide a practical framework for calculating energy flows in a driven [open quantum system](@entry_id:141912) based on the dynamics of its Bloch vector components .

### Connecting Heat to System Dynamics

The definition of the heat rate, $\dot{Q}(t) = \mathrm{Tr}[H_S(t) \dot{\rho}_S(t)]$, connects heat flow to the evolution of the system's state. For systems weakly coupled to a large environment (a [heat bath](@entry_id:137040)), the dynamics are often well-described by a **Gorini-Kossakowski-Lindblad-Sudarshan (GKLS) master equation**:

$\dot{\rho}_S(t) = -i[H_S'(t), \rho_S(t)] + \mathcal{D}_t[\rho_S(t)]$

Here, the first term describes the coherent, unitary evolution of the system, governed by an effective Hamiltonian $H_S'$ which includes the bare system Hamiltonian $H_S$ and a bath-induced correction known as the **Lamb shift**. The second term, $\mathcal{D}_t$, is the **dissipator** or **Lindbladian**, which describes the irreversible, non-unitary dynamics arising from the [system-environment interaction](@entry_id:145659), such as decoherence and thermal relaxation.

Substituting the GKLS equation into the definition of the heat rate yields:

$\dot{Q}(t) = \mathrm{Tr}[H_S(t)(-i[H_S'(t), \rho_S(t)] + \mathcal{D}_t[\rho_S(t)])]$

A crucial simplification occurs if we assume for the moment that the Lamb shift is negligible or absorbed into $H_S$, so $H_S' = H_S$. The contribution from the unitary part is:

$-i\mathrm{Tr}[H_S(t)[H_S(t), \rho_S(t)]] = -i\mathrm{Tr}[H_S^2 \rho_S - H_S \rho_S H_S] = -i(\mathrm{Tr}[H_S^2 \rho_S] - \mathrm{Tr}[\rho_S H_S^2]) = 0$

This identity, which relies on the cyclic property of the trace, reveals a profound connection: the heat exchanged by the system is determined solely by the dissipative part of its dynamics.

$\dot{Q}(t) = \mathrm{Tr}[H_S(t) \mathcal{D}_t[\rho_S(t)]]$

This formula is central to the study of [quantum thermodynamics](@entry_id:140152). It establishes that heat is the [energy flow](@entry_id:142770) associated with the [irreversible processes](@entry_id:143308) described by the Lindbladian. A direct consequence is that if a system is in a steady state with respect to the dissipative dynamics (i.e., $\mathcal{D}_t[\rho_{ss}] = 0$), then the heat current vanishes, provided the unitary part of the dynamics is also stationary. This is the case, for example, for a system in thermal equilibrium with its environment.

Consider a [quantum harmonic oscillator](@entry_id:140678) coupled to a thermal bath. Its dynamics can be described by a GKLS equation with jump operators for annihilation ($a$) and creation ($a^\dagger$) of quanta, with rates $\Gamma_\downarrow$ and $\Gamma_\uparrow$ respectively. These rates are not independent but are related by the **Kubo-Martin-Schwinger (KMS) condition**, which reflects the thermal nature of the bath: $\Gamma_\uparrow / \Gamma_\downarrow = \exp(-\beta \omega)$, where $\beta$ is the inverse temperature of the bath and $\omega$ is the oscillator frequency. The heat current can be shown to be proportional to the rate of change of the mean occupation number $n(t) = \langle a^\dagger a \rangle$. In the steady state, the occupation number reaches the Bose-Einstein distribution value, $n_{ss} = (\exp(\beta\omega)-1)^{-1}$, at which point the detailed balance between absorption and emission processes leads to a vanishing net heat current, $J_Q^{(\mathrm{ss})} = 0$. This illustrates the general principle that there is no net heat flow between systems in thermal equilibrium .

### The Physical Interpretation of Heat

The formula $\dot{Q}(t) = \mathrm{Tr}[H_S(t) \mathcal{D}_t[\rho_S(t)]]$ is mathematically precise, but its physical meaning requires further elucidation. By expressing the trace in the **instantaneous energy [eigenbasis](@entry_id:151409) (IEB)** of the Hamiltonian, $\{|\varepsilon_n(t)\rangle\}$, where $H_S(t)|\varepsilon_n(t)\rangle = \varepsilon_n(t)|\varepsilon_n(t)\rangle$, we find:

$\dot{Q}(t) = \sum_n \langle\varepsilon_n(t)| H_S(t) \mathcal{D}_t[\rho_S(t)] |\varepsilon_n(t)\rangle = \sum_n \varepsilon_n(t) \langle\varepsilon_n(t)| \mathcal{D}_t[\rho_S(t)] |\varepsilon_n(t)\rangle$

The term $\langle\varepsilon_n(t)| \mathcal{D}_t[\rho_S(t)] |\varepsilon_n(t)\rangle$ is precisely the rate of change of the population of the energy level $\varepsilon_n(t)$ that is caused by the dissipator. Therefore, the heat rate is the sum of the system's energy levels weighted by their rates of population change due to the interaction with the environment. This provides a clear physical picture: **heat is the energy exchanged through incoherent transitions between the system's energy levels**.

This interpretation, however, hinges critically on the choice of basis. A common misconception is to associate heat with population changes in any convenient, fixed basis. This is incorrect and can lead to physical paradoxes. Consider a driven qubit with Hamiltonian $H(t) = \frac{\hbar \omega}{2}[\cos\theta(t)\sigma_z + \sin\theta(t)\sigma_x]$ interacting with an environment that causes [dephasing](@entry_id:146545) along the fixed $\sigma_z$ axis, described by the dissipator $\mathcal{D}_z[\rho] = \frac{\gamma}{2}(\sigma_z \rho \sigma_z - \rho)$ .

In the basis of $\sigma_z$ [eigenstates](@entry_id:149904), this dissipator only affects the off-diagonal elements (coherences), leaving the populations unchanged. A naive identification of heat with population changes in this basis would imply zero heat flow. However, the true [heat rate](@entry_id:1125980) is:

$\dot{Q}(t) = \mathrm{Tr}[H(t) \mathcal{D}_z[\rho(t)]]$

When calculated, this yields a non-zero result: $\dot{Q}(t) \propto -\sin\theta(t) \mathrm{Re}\{\rho_{01}(t)\}$. Heat is generated whenever the energy [eigenbasis](@entry_id:151409) (which depends on $\theta(t)$) is misaligned with the [dephasing](@entry_id:146545) basis ($\sigma_z$). This demonstrates that the presence of **quantum coherences** (off-diagonal elements of the [density matrix](@entry_id:139892)) is essential for this heat exchange. The dephasing process, in conjunction with the driving field, induces transitions between the *true* energy levels of the system, even though the populations in the fixed dephasing basis remain constant. This highlights that a proper thermodynamic description must be based on the instantaneous energy [eigenbasis](@entry_id:151409) of the system .

### Thermodynamics Beyond Weak Coupling: The Hamiltonian of Mean Force

The formulation of the first law presented thus far relies on the assumption of [weak coupling](@entry_id:140994) between the system and its environment. This assumption allows us to define the system's internal energy as $U = \mathrm{Tr}[\rho_S H_S]$ and to factorize the total state of the system and bath. When the interaction is strong, this factorization is no longer valid, and system-bath correlations become significant. The very definition of the system's energy must be reconsidered.

In the [strong coupling regime](@entry_id:143581), the equilibrium state of the reduced system, $\rho_S^\beta = \mathrm{Tr}_B[\exp(-\beta H_{total}) / Z_{total}]$, is generally not of the form $\exp(-\beta H_S)/Z_S$. To maintain a thermodynamic structure, we introduce the **Hamiltonian of Mean Force**, $H^*(\beta, \lambda)$, an effective, temperature-dependent system Hamiltonian defined such that it correctly reproduces the true equilibrium state:

$\rho_S^\beta(\lambda) = \frac{\exp(-\beta H^*(\beta, \lambda))}{Z_S^*(\beta, \lambda)}$

where $Z_S^* = \mathrm{Tr}_S[\exp(-\beta H^*)]$. The Hamiltonian of mean force is formally given by:

$H^*(\beta, \lambda) = -\frac{1}{\beta}\ln\left(\frac{\mathrm{Tr}_B[\exp(-\beta(H_S(\lambda) + H_B + H_{SB}))]}{\mathrm{Tr}_B[\exp(-\beta H_B)]}\right)$

This effective Hamiltonian includes all equilibrium effects of the [strong interaction](@entry_id:158112) with the bath, appropriately renormalizing the system's energy levels. For a consistent thermodynamic description, the internal energy of the strongly coupled system must be defined using this effective Hamiltonian: $U(t) = \mathrm{Tr}_S[\rho_S(t) H^*(\beta, \lambda_t)]$.

With this redefinition, the first law for infinitesimal processes retains its structure. The change in internal energy $dU$ is decomposed as:

$dU = \mathrm{Tr}_S[\rho_S(t) dH^*(\beta, \lambda_t)] + \mathrm{Tr}_S[H^*(\beta, \lambda_t) d\rho_S(t)]$

The infinitesimal work is identified with the change in the effective Hamiltonian, $\delta W = \mathrm{Tr}_S[\rho_S dH^*]$, while the infinitesimal heat is the energy change associated with the change in the reduced state, $\delta Q = \mathrm{Tr}_S[H^* d\rho_S]$. This framework provides a thermodynamically consistent extension of the first law to the non-perturbative, strong-coupling regime .

### Ambiguities and Consistency Conditions

The apparent simplicity of the first law, $\dot{U} = \dot{Q} + \dot{W}$, belies several subtleties related to the definition of its constituent terms. The partition of energy flow into heat and work is not always unique and requires careful physical justification.

#### Lamb Shift and the Partition of Dynamics

When deriving a master equation from a microscopic model, the [system-bath interaction](@entry_id:193025) gives rise to both dissipative terms ($\mathcal{D}$) and a unitary correction to the system's Hamiltonian, the Lamb shift $H_{LS}$. The full GKLS equation reads $\dot{\rho} = -i[H_S + H_{LS}, \rho] + \mathcal{D}[\rho]$. This raises a fundamental question: which operator should define the system's energy? Is it the bare Hamiltonian $H_S$, or the physically dressed Hamiltonian $\widetilde{H}_S = H_S + H_{LS}$?

This choice constitutes a "[gauge freedom](@entry_id:160491)" that affects the calculated values of [heat and work](@entry_id:144159) . If one redefines the internal energy from $U = \mathrm{Tr}[\rho H_S]$ to $\widetilde{U} = \mathrm{Tr}[\rho \widetilde{H}_S]$, the [work and heat](@entry_id:141701) rates change as follows:

$\Delta \dot{W}(t) = \mathrm{Tr}[\rho(t) \dot{H}_{LS}(t)]$
$\Delta \dot{Q}(t) = \mathrm{Tr}[\dot{\rho}(t) H_{LS}(t)]$

The division of energy into heat and work is invariant under this redefinition only under strict conditions. Specifically, the power $\dot{W}$ is unchanged if the Lamb shift is time-independent ($\dot{H}_{LS} = 0$). The [heat rate](@entry_id:1125980) $\dot{Q}$ is unchanged if the Lamb shift Hamiltonian does not contribute to the energy flow from the dissipator, which requires that $H_{LS}$ is a "[dark state](@entry_id:161302)" of the dissipator's dual map, i.e., $\mathcal{D}^*(H_{LS})=0$. Furthermore, for the original splitting based on $H_S$ to be physically unambiguous, the Lamb shift should not generate additional unitary energy exchanges, which is ensured if $[H_S, H_{LS}] = 0$. These conditions highlight that while mathematically one can partition the generator in different ways, a physically meaningful and consistent thermodynamic interpretation requires careful justification of the chosen system Hamiltonian.

#### Local versus Global Master Equations

Another source of inconsistency arises in [composite quantum systems](@entry_id:193313). Consider two coupled subsystems, each interacting with its own local environment. One might be tempted to model the dynamics using a "local" master equation, where the dissipators for each subsystem are derived by ignoring the inter-system coupling. While this approach is simpler, it can be thermodynamically inconsistent.

For instance, if the two local environments are at the same temperature, the [second law of thermodynamics](@entry_id:142732) dictates that there should be no net heat flow in the steady state. However, a local master equation can predict a spurious, persistent heat current circulating between the two subsystems, a clear violation of thermodynamic principles .

A thermodynamically consistent model requires a "global" master equation. In this approach, one first diagonalizes the full Hamiltonian of the composite system, including the inter-system coupling. The dissipators are then constructed in the basis of these global [energy eigenstates](@entry_id:152154). This procedure ensures that the steady state of the system coupled to baths at a uniform temperature is the correct global Gibbs state, $\rho_\beta \propto \exp(-\beta H_S)$, for which all heat currents individually vanish. This illustrates a critical lesson: the choice of an appropriate open-system model is not merely a matter of mathematical convenience but is essential for thermodynamic consistency.

#### Frame Dependence and Spurious Heat

The definition of heat as $\dot{Q} = \mathrm{Tr}[H \dot{\rho}]$ is sensitive to the reference frame in which the dynamics are described. An improper choice of frame can lead to the misidentification of purely unitary dynamics as dissipative heat flow.

Suppose an observer analyzes a system in a time-dependent [rotating frame](@entry_id:155637) defined by a [unitary transformation](@entry_id:152599) $U(t)$. In this frame, the state is $\rho'(t) = U^\dagger(t) \rho(t) U(t)$. If the observer mistakenly calculates the heat flow using the [total time derivative](@entry_id:172646) $\dot{\rho}'(t)$ as $\dot{Q}_{\text{wrong}} = \mathrm{Tr}[H_0 \dot{\rho}'(t)]$ (where $H_0$ is the lab-frame Hamiltonian), they will generate a spurious contribution. The derivative $\dot{\rho}'(t)$ contains terms arising from the frame's motion, $\dot{U}^\dagger \rho U$ and $U^\dagger \rho \dot{U}$, which are purely unitary and should not be counted as heat . This error leads to an incorrect [entropy production](@entry_id:141771) rate that can even become transiently negative, appearing to violate the second law. The spurious contribution to [entropy production](@entry_id:141771) can be shown to be proportional to the rate of frame rotation and the quantum coherences present in the system's state. This underscores the necessity of carefully separating the truly dissipative part of the dynamics from coherent evolution when identifying thermodynamic quantities.

### Advanced Perspectives on Quantum Heat

The fundamental framework of the first law can be extended and refined to capture more complex phenomena and provide deeper physical insight.

#### Non-Markovian Dynamics and Heat Backflow

The GKLS master equation describes Markovian dynamics, where the environment is assumed to have no memory. However, for systems strongly coupled to structured environments or interacting over short timescales, memory effects become important, leading to **non-Markovian dynamics**.

One signature of non-Markovianity is the temporary negativity of decay rates in a time-local master equation. Consider an amplitude-damping process described by $\dot{\rho} = \gamma(t)(\sigma_- \rho \sigma_+ - \frac{1}{2}\{\sigma_+\sigma_-, \rho\})$. In a Markovian scenario, $\gamma(t)$ is a positive constant. In a non-Markovian setting, $\gamma(t)$ can become transiently negative.

The heat current for this process is $\dot{Q}(t) = \dot{U}(t) = -\hbar\omega_0 \gamma(t) p_e(t)$, where $p_e(t)$ is the excited state population . When $\gamma(t) > 0$, the system loses energy to the environment ($\dot{Q}  0$), as expected. However, during intervals where $\gamma(t)  0$, the heat current becomes positive ($\dot{Q} > 0$). This corresponds to **heat backflow**: energy flows from the environment back into the system. This phenomenon is a direct consequence of the [environmental memory](@entry_id:136908), where energy previously dissipated is temporarily returned to the system, and is a hallmark of non-Markovian quantum thermodynamics.

#### Ergotropy: Decomposing Heat into Useful and Useless Components

The first law treats all energy that is not work as heat. However, not all of this "heat" is of the same quality. The energy stored in quantum coherences can, in principle, be extracted as work via unitary operations. This extractable energy is called **[ergotropy](@entry_id:1124640)**, $\mathcal{W}$. The remaining energy, which cannot be accessed by unitary means, is the **passive energy**, $U_{\text{pass}}$. The total internal energy can thus be decomposed as $U = \mathcal{W} + U_{\text{pass}}$.

This leads to a more refined decomposition of the first law: $\dot{U} = \dot{\mathcal{W}} + \dot{Q}_{\text{pas}}$, where we have defined a "passive heat" rate. Let's reconsider the case of pure dephasing in the energy basis . In this process, the "traditional" heat flow $\dot{Q}_{\text{trad}} = \mathrm{Tr}[H\mathcal{D}(\rho)]$ is identically zero because the dissipator does not induce transitions between energy levels. However, the process is far from trivial: the [dephasing](@entry_id:146545) destroys coherences, causing the [ergotropy](@entry_id:1124640) to decrease ($\dot{\mathcal{W}}  0$). Since the total energy $U$ is constant in this process (as $\dot{Q}_{\text{trad}} = 0$ and $\dot{W} = 0$), the loss in [ergotropy](@entry_id:1124640) must be compensated by an increase in passive energy: $\dot{Q}_{\text{pas}} = \dot{U}_{\text{pass}} = -\dot{\mathcal{W}} > 0$. From this perspective, dephasing is a process that converts a useful form of energy ([ergotropy](@entry_id:1124640)) into an inaccessible, "useless" form (passive energy), which can be seen as a fundamental form of heat generation.

#### The Stochastic Nature of Heat: A Trajectory Perspective

The master equation describes the average behavior of an ensemble of quantum systems. A deeper understanding of heat can be gained by "unraveling" the master equation into individual **[quantum trajectories](@entry_id:149300)**. In the [quantum jump](@entry_id:149204) formalism, the evolution of a single system consists of continuous, deterministic segments under a non-Hermitian effective Hamiltonian, punctuated by instantaneous, stochastic [quantum jumps](@entry_id:140682).

From this perspective, [heat and work](@entry_id:144159) have distinct characters at the single-realization level . Work is performed continuously during the deterministic segments, corresponding to the change in energy due to the externally driven Hamiltonian: $\delta W_{\text{trj}} = \langle\psi(t)|\dot{H}(t)|\psi(t)\rangle dt$.

Heat, in contrast, is exchanged in discrete, quantized packets exclusively during the stochastic jumps. For a system interacting with a thermal bath, a jump corresponding to an excitation from state $|g\rangle$ to $|e\rangle$ represents the absorption of a quantum of energy from the bath. The associated heat is $\delta Q_{\text{trj}} = +\hbar\omega$, where $\omega$ is the transition frequency. Conversely, a de-excitation jump from $|e\rangle$ to $|g\rangle$ corresponds to the emission of a quantum of energy to the bath, with an associated heat of $\delta Q_{\text{trj}} = -\hbar\omega$. During the continuous no-jump evolution, no heat is exchanged, $\delta Q_{\text{trj}} = 0$.

This trajectory-level definition provides a powerful microscopic picture of heat as a fundamentally stochastic and quantized process. Averaging the heat exchanged in these discrete jump events over many trajectories precisely recovers the ensemble-averaged heat current predicted by the master equation, bridging the microscopic stochastic picture with the macroscopic deterministic one.