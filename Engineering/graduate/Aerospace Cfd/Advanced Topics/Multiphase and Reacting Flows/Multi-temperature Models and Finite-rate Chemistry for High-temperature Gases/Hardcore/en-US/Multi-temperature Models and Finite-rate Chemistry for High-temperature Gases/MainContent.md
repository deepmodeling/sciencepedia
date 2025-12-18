## Introduction
The study of [high-temperature gas dynamics](@entry_id:750321), particularly in the context of [hypersonic flight](@entry_id:272087) and atmospheric entry, pushes the boundaries of classical fluid mechanics. In these extreme regimes, gas is heated so rapidly that it deviates from thermal and [chemical equilibrium](@entry_id:142113), rendering traditional modeling approaches insufficient. This state, known as [thermochemical nonequilibrium](@entry_id:1133048), presents a significant challenge for accurately predicting flow behavior, aerodynamic forces, and, most critically, the intense heating experienced by a vehicle. This article addresses this knowledge gap by providing a comprehensive overview of the advanced physical models required to simulate these complex flows.

Across the following chapters, you will gain a graduate-level understanding of this critical topic. The journey begins with the foundational "Principles and Mechanisms," where we will dissect the concept of [thermochemical nonequilibrium](@entry_id:1133048) and introduce the multi-temperature frameworks (2-T and 3-T models) and finite-rate chemistry that form the basis of [modern analysis](@entry_id:146248). Next, "Applications and Interdisciplinary Connections" will demonstrate how these theories are applied to solve real-world problems in hypersonic [aerothermodynamics](@entry_id:155070), from predicting shock-layer structure to modeling surface heating, and explore their connections to plasma physics and planetary science. Finally, "Hands-On Practices" will offer concrete problems to solidify your grasp of the computational and theoretical techniques discussed. We begin by exploring the fundamental principles that govern these high-energy phenomena.

## Principles and Mechanisms

The study of high-temperature gas flows, particularly those encountered in hypersonic flight and atmospheric entry, necessitates a departure from the simplifying assumptions of classical gas dynamics. In these extreme environments, the gas is no longer in a state of [local thermodynamic equilibrium](@entry_id:139579). Instead, the various internal energy modes of the constituent molecules and atoms do not have sufficient time to equilibrate with one another, and chemical reactions proceed at finite rates. This chapter delves into the fundamental principles and mechanisms that govern these **[thermochemical nonequilibrium](@entry_id:1133048)** phenomena, providing the theoretical foundation for the advanced computational models used to simulate such flows.

### The Concept of Thermochemical Nonequilibrium

At the microscopic level, the energy of a gas is distributed among several modes. These include the **[translational energy](@entry_id:170705)** associated with the random motion of particles, the **[rotational energy](@entry_id:160662)** of molecules, the **vibrational energy** stored in the oscillations of atomic bonds, and the **electronic energy** corresponding to the quantum states of electrons orbiting atomic nuclei. In a state of **thermodynamic equilibrium**, energy is distributed among these modes according to a single, well-defined temperature, $T$, as described by the Maxwell-Boltzmann distribution from statistical mechanics.

However, consider the gas flow through a strong shock wave, a canonical problem in hypersonic [aerothermodynamics](@entry_id:155070) . As gas particles cross the infinitesimally thin shock front, their bulk kinetic energy is converted almost instantaneously into random thermal motion. This energy preferentially populates the [translational energy](@entry_id:170705) mode, causing a near-discontinuous jump in the **translational temperature**. The other internal energy modes—rotational, vibrational, and electronic—do not adjust instantaneously. Their equilibration requires energy to be transferred from the translational mode through intermolecular collisions, a process that occurs at a finite rate.

Each of these energy transfer processes is characterized by a **relaxation time**, $\tau$, which represents the average time required for that mode to equilibrate with the translational mode. The timescales for these processes vary dramatically:
*   **Rotational relaxation** ($\tau_{\text{rot}}$) is very efficient, typically requiring only 5 to 10 collisions. Its relaxation time is therefore very short.
*   **Vibrational relaxation** ($\tau_{\text{vib}}$) is much less efficient, as the [energy quanta](@entry_id:145536) are larger. It can require hundreds or thousands of collisions, resulting in a significantly longer relaxation time.
*   **Electronic relaxation** ($\tau_{\text{elec}}$) and chemical reactions like **dissociation** and **ionization** ($\tau_{\text{chem}}$) involve even larger energy transfers and typically have the longest [relaxation times](@entry_id:191572).

The state of the gas in the post-shock region is determined by the competition between these microscopic relaxation times and the macroscopic **flow time**, $t_{\text{flow}}$, which is the characteristic time a fluid particle spends in a region of interest (e.g., the shock layer).

When $t_{\text{flow}}$ is not sufficiently large compared to a given relaxation time $\tau_m$, the corresponding mode $m$ will not have enough time to reach equilibrium with the translational mode. This leads to a state of **[thermal nonequilibrium](@entry_id:191586)**, where different energy modes are characterized by different temperatures. For instance, immediately behind a shock, we typically find $T_{\text{tr}} > T_{\text{vib}}$ because [vibrational relaxation](@entry_id:185056) is slow. Similarly, if $t_{\text{flow}}$ is comparable to or shorter than $\tau_{\text{chem}}$, the chemical composition of the gas will lag behind the equilibrium composition corresponding to the local temperature and pressure. This is a state of **[chemical nonequilibrium](@entry_id:265362)**. The simultaneous existence of both thermal and [chemical nonequilibrium](@entry_id:265362) is termed **[thermochemical nonequilibrium](@entry_id:1133048)** .

In such a state, the assumption of a single temperature is fundamentally invalid. An accurate physical description requires models that can account for the separate evolution of energy in different modes. This is the motivation for [multi-temperature models](@entry_id:1128289).

### Multi-Temperature Modeling Frameworks

To capture the physics of [thermal nonequilibrium](@entry_id:191586), we partition the internal energy modes into groups, each assumed to be in internal equilibrium and characterized by its own temperature. The choice of grouping depends on the relevant physics and desired model fidelity.

#### The Two-Temperature (2-T) Model

The most common approach for neutral and weakly ionized gases is the **[two-temperature model](@entry_id:180856)**. Because rotational relaxation is so rapid ($\tau_{\text{rot}} \ll t_{\text{flow}}$ in most continuum flows), the rotational energy mode is almost always in equilibrium with the translational mode. It is therefore standard practice to group these two modes together, described by a single **translational-rotational temperature**, $T$. The remaining internal energy modes—vibrational and electronic—are often lumped together and described by a single **vibrational-electronic temperature**, $T_v$. This lumping is justified when the [relaxation times](@entry_id:191572) for vibration and [electronic excitation](@entry_id:183394) are of a similar order of magnitude and are much longer than the rotational relaxation time . This ($T$, $T_v$) framework is the foundation for many practical engineering models of hypersonic flows.

#### The Three-Temperature (3-T) Model

In more extreme conditions where significant ionization occurs, the free electrons introduce another level of complexity. Due to their extremely small mass compared to heavy particles (atoms and ions), electrons [exchange energy](@entry_id:137069) very inefficiently in elastic collisions with them. This allows the electron gas to maintain its own translational temperature, the **electron temperature**, $T_e$, which can be very different from the heavy-particle translational temperature.

Furthermore, electron-impact collisions are highly efficient at causing [electronic excitation](@entry_id:183394) and de-excitation of heavy particles. This strong coupling suggests that the population of electronic [excited states](@entry_id:273472) will be in equilibrium with the electron [translational energy](@entry_id:170705). This leads to the formulation of a **three-temperature model** , which is standard for modeling partially ionized plasmas. The energy modes are typically grouped as follows:
*   **Translational-Rotational Temperature ($T$)**: Characterizes the [translational energy](@entry_id:170705) of all heavy species (atoms, molecules, ions) and the rotational energy of molecules.
*   **Vibrational Temperature ($T_v$)**: Characterizes the vibrational energy of the molecular species. In some variants, this is lumped with the electronic temperature as in the 2-T model, but a three-temperature segregation is often more accurate.
*   **Electron-Electronic Temperature ($T_e$)**: Characterizes the [translational energy](@entry_id:170705) of the free electrons and the [electronic excitation](@entry_id:183394) energy of all atoms, molecules, and ions.

This framework provides a more detailed and physically accurate description of the energy distribution in high-enthalpy, ionized flows.

### Governing Equations for Multi-Temperature Flows

The implementation of a [multi-temperature model](@entry_id:1128288) within a Computational Fluid Dynamics (CFD) framework requires modifications to the standard Navier-Stokes equations. Specifically, for each new temperature introduced, an additional conservation equation must be solved.

Let us start with a baseline single-temperature model for a reacting gas mixture, which solves [conservation equations](@entry_id:1122898) for species mass, mixture momentum, and mixture total energy. To upgrade to a 2-T ($T, T_v$) model, we must introduce a new conservation equation for the energy mode that is out of equilibrium—in this case, the vibrational-electronic energy, $e_v$ . This new equation must account for the convection and diffusion of vibrational energy, as well as the sources and sinks that cause it to change. The crucial source terms are:
1.  **Inter-modal Energy Exchange**: This term, often denoted $Q_{VT}$, represents the net rate of energy transfer from the translational-[rotational modes](@entry_id:151472) to the vibrational-electronic modes due to molecular collisions. It drives the system towards thermal equilibrium ($T_v \to T$).
2.  **Chemical-Vibrational Coupling**: Chemical reactions create or destroy molecules. When a molecule is formed or dissociated, a discrete amount of vibrational energy is gained or lost by the vibrational energy pool. This is a powerful coupling mechanism between the chemistry and the thermal state of the gas.

A critical requirement is the strict conservation of total energy. The inter-modal exchange term $Q_{VT}$ represents an internal redistribution of energy. Therefore, if it appears as a source $(+Q_{VT})$ in the vibrational energy equation, it must appear as an equal and opposite sink $(-Q_{VT})$ in the translational-rotational energy equation.

Generalizing to a full 3-T ($T, T_v, T_e$) framework for a reacting mixture of $N$ species, the system of governing equations becomes significantly more complex . Assuming a single bulk velocity $\mathbf{u}$ for the mixture, the system can be written as:

**Species Continuity:** For each species $s=1, ..., N$:
$$
\frac{\partial (\rho Y_s)}{\partial t} + \nabla \cdot \left(\rho Y_s \mathbf{u} + \mathbf{J}_s\right) = \dot{\omega}_s
$$
where $\rho$ is the mixture density, $Y_s$ is the mass fraction of species $s$, $\mathbf{J}_s$ is the diffusive mass flux, and $\dot{\omega}_s$ is the mass production rate due to chemical reactions.

**Mixture Momentum:**
$$
\frac{\partial (\rho \mathbf{u})}{\partial t} + \nabla \cdot \left(\rho \mathbf{u} \otimes \mathbf{u} + p \mathbf{I} - \boldsymbol{\tau}\right) = \mathbf{0}
$$
where $p$ is the total pressure (sum of [partial pressures](@entry_id:168927), including electron pressure), $\mathbf{I}$ is the identity tensor, and $\boldsymbol{\tau}$ is the viscous stress tensor.

**Vibrational-Electronic Energy ($e_v$):**
$$
\frac{\partial (\rho e_v)}{\partial t} + \nabla \cdot \left(\rho e_v \mathbf{u} + \mathbf{q}_v\right) = \sum_{s=1}^{N} \dot{\omega}_s e_{v,s} + Q_{T \leftrightarrow v} + Q_{e \leftrightarrow v}
$$
Here, $e_{v,s}$ is the vibrational-electronic energy of species $s$, $\mathbf{q}_v$ is the vibrational energy flux (including conduction and diffusion), $Q_{T \leftrightarrow v}$ is the energy exchange with heavy-particle translation, and $Q_{e \leftrightarrow v}$ is the exchange with electrons.

**Electron-Electronic Energy ($e_e$):**
$$
\frac{\partial (\rho e_e)}{\partial t} + \nabla \cdot \left(\rho e_e \mathbf{u} + \mathbf{q}_e\right) = -p_e \nabla \cdot \mathbf{u} + \sum_{s=1}^{N} \dot{\omega}_s e_{e,s} + Q_{T \leftrightarrow e} - Q_{e \leftrightarrow v}
$$
This equation includes the [pressure work](@entry_id:265787) done by the electron [partial pressure](@entry_id:143994) $p_e$, chemical coupling via $e_{e,s}$, and exchange terms with heavy-particle translation ($Q_{T \leftrightarrow e}$) and vibration ($-Q_{e \leftrightarrow v}$).

**Total Energy ($E$):**
The [total energy equation](@entry_id:1133263) is also solved, but it is formulated such that the internal exchange terms ($Q$) cancel out, ensuring conservation.
$$
\frac{\partial (\rho E)}{\partial t} + \nabla \cdot \left[(\rho E + p)\mathbf{u} - \boldsymbol{\tau}\cdot \mathbf{u} + \mathbf{q}\right] = 0
$$
where $E$ is the total energy per unit mass (sum of internal and kinetic), and $\mathbf{q}$ is the total heat flux vector (sum of all modal contributions). This set of coupled partial differential equations forms the basis of multi-temperature CFD solvers.

### Modeling Physical Mechanisms: Source Terms and Properties

The accuracy of a multi-temperature simulation depends critically on the physical models used for the source terms and thermodynamic properties that appear in the governing equations.

#### Vibrational Energy and Relaxation

To solve the [vibrational energy](@entry_id:157909) equation, we first need expressions for the vibrational energy $e_v$ and the [vibrational heat capacity](@entry_id:151645) $c_{v,v}$ as functions of $T_v$. These are derived from statistical mechanics. For a [diatomic molecule](@entry_id:194513) modeled as a **[simple harmonic oscillator](@entry_id:145764)** with a [characteristic vibrational temperature](@entry_id:153344) $\Theta_v = h\nu/k_B$ (where $\nu$ is the vibrational frequency), the molar vibrational energy (excluding the [zero-point energy](@entry_id:142176)) and [specific heat](@entry_id:136923) are given by :
$$
e_{v}(T_{v}) = \frac{R \Theta_{v}}{\exp\left(\frac{\Theta_{v}}{T_{v}}\right) - 1}
$$
$$
c_{v,v}(T_{v}) = \frac{\partial e_v}{\partial T_v} = R \left( \frac{\Theta_{v}}{T_{v}} \right)^{2} \frac{\exp\left(\frac{\Theta_{v}}{T_{v}}\right)}{\left(\exp\left(\frac{\Theta_{v}}{T_{v}}\right) - 1\right)^{2}}
$$
where $R$ is the universal gas constant. These expressions allow us to relate the conserved quantity, $e_v$, to the vibrational temperature, $T_v$.

The energy exchange term, $Q_{T \leftrightarrow v}$, is commonly described by the **Landau-Teller relaxation law** . This law postulates that the rate of change of vibrational energy is proportional to the deviation from its equilibrium value:
$$
\frac{d e_v}{d t} = \frac{e_v(T) - e_v(T_v)}{\tau_v(T, p)}
$$
where $e_v(T)$ is the equilibrium vibrational energy at the local translational temperature $T$, and $\tau_v$ is the [vibrational relaxation](@entry_id:185056) time, which depends on temperature and pressure. This macroscopic law can be derived from a microscopic **master equation** describing the evolution of vibrational level populations, under the assumption of small deviations from equilibrium. The derivation reveals that $\tau_v$ is fundamentally related to the collisional transition rates between vibrational quantum states.

#### Finite-Rate Chemistry in Multi-Temperature Systems

In a multi-temperature environment, [chemical reaction rates](@entry_id:147315) are no longer functions of a single temperature. The rate of an elementary reaction is described by the **law of [mass action](@entry_id:194892)**, which relates the net [rate of reaction](@entry_id:185114) to the difference between forward and backward reaction rates . For a general reaction $r$, the molar production rate of a species $s$ is:
$$
\dot{\omega}_s = \sum_{r} (\nu_{sr}^{b} - \nu_{sr}^{f}) \left( k_{f,r} \prod_{j} c_{j}^{\nu_{jr}^{f}} - k_{b,r} \prod_{j} c_{j}^{\nu_{jr}^{b}} \right)
$$
where $\nu_{jr}^{f}$ and $\nu_{jr}^{b}$ are the stoichiometric coefficients of species $j$ as a reactant and product, respectively, $c_j$ is the [molar concentration](@entry_id:1128100) of species $j$, and $k_{f,r}$ and $k_{b,r}$ are the forward and backward rate constants.

A key challenge is modeling the forward rate constant $k_{f,r}$ under nonequilibrium conditions. This is particularly important for dissociation reactions, which are strongly coupled to the vibrational state of the molecule. This phenomenon is known as **vibration-[dissociation](@entry_id:144265) coupling**. Since molecules in high [vibrational states](@entry_id:162097) are already "stretched" and closer to breaking, they dissociate much more readily.

To account for this, the standard Arrhenius expression for the rate constant is modified. A widely used engineering approach is **Park's [two-temperature model](@entry_id:180856)**, which introduces a controlling temperature $T^*$ in the exponential term :
$$
k_f(T, T_v) = A T^n \exp\left(-\frac{E_a}{k_B T^*}\right)
$$
The controlling temperature is typically taken as the geometric mean of the translational and vibrational temperatures:
$$
T^* = \sqrt{T T_v}
$$
This form empirically captures the fact that both high collisional energy (related to $T$) and high internal [vibrational energy](@entry_id:157909) (related to $T_v$) are required for efficient [dissociation](@entry_id:144265). It correctly reduces the reaction rate in post-shock regions where vibration lags ($T_v \ll T$) and recovers the equilibrium rate when $T_v \to T$. While other forms exist, some with a stronger physical basis in certain regimes , the geometric mean model remains a robust and popular choice in CFD.

The backward (recombination) rate constant $k_{b,r}$ is not modeled independently. It is determined from the forward rate constant and an [equilibrium constant](@entry_id:141040) $K_{c,r}$ via the principle of **detailed balance**. In a non-equilibrium system, this equilibrium constant itself becomes a function of the multiple temperatures, e.g., $K_{c,r}(T, T_v)$, calculated using partition functions evaluated at their respective mode temperatures .

### Domain of Validity of Multi-Temperature Models

While powerful, [multi-temperature models](@entry_id:1128289) are still based on several key assumptions, and it is crucial to understand their domain of validity. They are fundamentally continuum models and assume that the velocity distribution of particles within each group is Maxwellian and that internal energy level populations within each mode follow a Boltzmann distribution. These assumptions break down in certain flow regimes .

1.  **Rarefaction Effects**: At very high altitudes, the gas density becomes so low that the **mean free path** $\lambda$ (the average distance a particle travels between collisions) becomes comparable to the characteristic length scale of the flow, $L$. This regime is characterized by a high **Knudsen number**, $K_n = \lambda/L$. When $K_n$ is no longer small (e.g., $K_n \gtrsim 0.1$), the continuum assumption itself fails. Collisions are too infrequent to maintain even a local Maxwell-Boltzmann distribution, and the Navier-Stokes equations, even with multiple temperatures, are no longer valid. In such cases, more fundamental methods like the Direct Simulation Monte Carlo (DSMC) method are required.

2.  **Strong Radiative Effects**: In very hot, low-density plasmas, radiative processes can become as important as, or even more important than, collisional processes in populating and de-populating electronic energy levels. The ratio of the spontaneous radiative emission rate to the collisional de-excitation rate is a key parameter. When this ratio is large, radiation can drain energy from the upper electronic states faster than collisions can replenish them. This leads to a strong deviation from a Boltzmann distribution for the electronic level populations. The concept of a single electronic temperature becomes ill-defined. In these situations, a **collisional-radiative (CR) model** is necessary, which solves a master equation for the population of each individual electronic state, explicitly accounting for both collisional and radiative transitions.

For example, a hypersonic vehicle at very high altitude ($K_n \sim 0.2$, low density) or in a near-space wake ($K_n \sim 0.5$, very low density) would exhibit both strong [rarefaction](@entry_id:201884) and dominant radiative effects, rendering a [two-temperature model](@entry_id:180856) inadequate. Conversely, for a shock layer at intermediate altitudes or in a high-pressure rocket exhaust, the flow is dense ($K_n \ll 0.1$) and collision-dominated, making the multi-temperature continuum approach highly suitable . When [multi-temperature models](@entry_id:1128289) fail due to non-Boltzmann distributions within a mode, the next level of fidelity is a **state-to-state model**, which tracks the population of individual quantum states (e.g., each vibrational level) with its own governing equation.