## Introduction
Simulating fusion plasmas with high fidelity requires capturing the complex interplay of microscopic kinetic dynamics and macroscopic transport. While the Vlasov-Maxwell system provides a fundamental description of a [collisionless plasma](@entry_id:191924), real fusion devices are open, driven systems, far from [thermodynamic equilibrium](@entry_id:141660). They are continuously fueled, heated by external power, and subject to particle and energy losses. This introduces a critical knowledge gap: how do we mathematically account for these external interactions within a first-principles kinetic framework? The answer lies in the rigorous modeling of sources and sinks. This article provides a comprehensive guide to this essential topic. In the first chapter, "Principles and Mechanisms," we will explore the theoretical foundation, detailing the conservation laws that constrain source models and the mathematical forms used to represent physical processes. The second chapter, "Applications and Interdisciplinary Connections," demonstrates how these models are applied to study fusion phenomena and reveals their conceptual links to other fields like control engineering and electrochemistry. Finally, "Hands-On Practices" offers targeted exercises to build practical skills in implementing these models correctly. To begin, we must first understand the fundamental principles and mechanisms that govern these crucial modeling components.

## Principles and Mechanisms

In the study of magnetized plasmas through full-distribution-function (full-$f$) simulations, the accurate representation of [sources and sinks](@entry_id:263105) is paramount. While the Vlasov-Maxwell system describes the collisionless evolution of charged particles under self-consistent electromagnetic fields, and [collision operators](@entry_id:1122657) account for their thermalization, real-world plasmas are open systems. They are continuously fueled, heated, and subject to various loss mechanisms. Sources and sinks are the mathematical constructs within the kinetic framework that model these external interactions, enabling simulations to achieve and sustain quasi-steady states far from thermodynamic equilibrium, where interesting transport phenomena occur. This chapter elucidates the fundamental principles governing these terms and the mechanisms by which they are modeled.

### The Necessity of Sources and Sinks in Full-f Simulations

A full-$f$ simulation evolves the complete [phase-space distribution](@entry_id:151304) function, $f_s(\mathbf{Z}, t)$, for each plasma species $s$. Its governing equation is a kinetic equation, often of the Vlasov-Fokker-Planck type:
$$
\frac{\partial f_s}{\partial t} + \dot{\mathbf{Z}}\cdot \nabla_{\mathbf{Z}} f_s = C_s[f] + S_s
$$
Here, $\dot{\mathbf{Z}}\cdot \nabla_{\mathbf{Z}} f_s$ represents the collisionless dynamics (the Vlasov operator), $C_s[f]$ is the [collision operator](@entry_id:189499), and $S_s$ is a generic term encompassing all external [sources and sinks](@entry_id:263105).

In a closed, [isolated system](@entry_id:142067) with only Vlasov and collisional dynamics, the plasma would inevitably evolve towards global thermodynamic equilibrium—a state of uniform density and temperature, devoid of the gradients that drive turbulence and transport. The primary role of [sources and sinks](@entry_id:263105) is to counteract this relaxation. Sources inject particles, momentum, and energy, building and sustaining the pressure and flow profiles that are characteristic of fusion devices. Sinks, in turn, represent the various loss channels, such as radiation and particle losses to the wall.

The interplay between sources, sinks, and transport is the cornerstone of global plasma dynamics. In a quasi-steady state, turbulent and neoclassical transport processes continuously attempt to flatten the plasma profiles, while sources work to rebuild them. A **[full-f simulation](@entry_id:1125367)** is essential for capturing this global balance self-consistently. Unlike **delta-f ($\delta f$) models**, which evolve only the fluctuating part of the distribution function ($\delta f_s$) around a fixed background ($f_{0s}$), full-$f$ models evolve the total $f_s$. This allows the background profiles, contained within $f_{0s} = \langle f_s \rangle$, to respond dynamically to the turbulent fluxes they generate. Sources primarily sustain the background profiles, while turbulent transport, arising from the fluctuating components, acts to deplete them. A full-$f$ approach is therefore required to correctly model the global evolution of profiles under the combined influence of external drives and self-generated turbulence .

### Fundamental Conservation Properties and Constraints

The construction of [source and sink](@entry_id:265703) models is not arbitrary; it is rigidly constrained by the fundamental conservation laws of physics. Understanding these constraints requires examining the effect of different operators on the macroscopic moments of the distribution function, such as density, momentum, and energy.

#### Distinguishing Collisional Relaxation from External Forcing

It is crucial to first distinguish the role of the **collision operator**, $C_s[f]$, from that of external sources and sinks, $S_s$. The collision operator models binary Coulomb collisions, which are an *internal* process within the plasma. As such, it must adhere to strict conservation laws :

1.  **Particle Number Conservation (per Species):** Coulomb collisions are scattering events that do not change a particle's species identity. Therefore, the [collision operator](@entry_id:189499) conserves the number of particles for each species independently. Mathematically, its zeroth velocity-space moment vanishes locally in configuration space:
    $$
    \int C_s[f] \, d^3v = 0 \quad \text{for each species } s.
    $$
    This means collisions only redistribute particles in velocity space (e.g., driving the distribution towards a Maxwellian), but they cannot act as a source or sink of particles to balance transport losses.

2.  **Total Momentum and Energy Conservation:** While momentum and energy can be exchanged between different species during inter-species collisions (e.g., electron-ion friction and [thermal equilibration](@entry_id:1132996)), the total momentum and energy of the entire plasma system are conserved. This implies that the momentum and energy moments of the collision operator for a single species are generally non-zero, but their sum over all species vanishes:
    $$
    \sum_s \int m_s \mathbf{v} \, C_s[f] \, d^3v = \mathbf{0}
    $$
    $$
    \sum_s \int \frac{1}{2} m_s v^2 \, C_s[f] \, d^3v = 0
    $$

**External [sources and sinks](@entry_id:263105)**, $S_s$, model interactions with the world outside the plasma (e.g., [neutral beam](@entry_id:752451) injectors, RF antennas, material walls). They are not bound by the same conservation rules. They are specifically designed to represent the injection or removal of particles, momentum, and energy from the system. For instance, a particle source term $S_s$ will generally have a non-zero zeroth moment, $\int S_s \, d^3v \neq 0$.

#### The Hierarchy of Macroscopic Balance Equations

By taking velocity-space moments of the full kinetic equation, we can derive the macroscopic fluid-like balance equations. This process reveals precisely how [sources and sinks](@entry_id:263105) drive the evolution of macroscopic quantities. Let's consider the kinetic equation:
$$
\frac{\partial f_s}{\partial t} + \boldsymbol{v}\cdot \nabla f_s + \frac{q_s}{m_s}\left(\boldsymbol{E} + \boldsymbol{v}\times \boldsymbol{B}\right)\cdot \nabla_{\boldsymbol{v}} f_s = C_s[f] + S_s
$$

-   **Particle Balance (Continuity Equation):** Integrating the equation over [velocity space](@entry_id:181216) gives the evolution of the particle density $n_s = \int f_s \, d^3v$:
    $$
    \frac{\partial n_s}{\partial t} + \nabla \cdot (n_s \mathbf{u}_s) = \int S_s \, d^3v
    $$
    where $\mathbf{u}_s$ is the fluid velocity. The collision term integrates to zero. The source term's zeroth moment, $\Gamma_{p,s} \equiv \int S_s \, d^3v$, acts as the local particle source density.

-   **Momentum Balance:** Multiplying by $m_s\mathbf{v}$ and integrating yields the evolution of the [momentum density](@entry_id:271360) $m_s n_s \mathbf{u}_s$:
    $$
    \frac{\partial (m_s n_s \mathbf{u}_s)}{\partial t} + \nabla \cdot \mathbf{\Pi}_s = n_s q_s (\mathbf{E} + \mathbf{u}_s \times \mathbf{B}) + \mathbf{F}_{coll,s} + \mathbf{M}_s
    $$
    Here, $\mathbf{\Pi}_s$ is the full [pressure tensor](@entry_id:147910), $\mathbf{F}_{coll,s} = \int m_s \mathbf{v} C_s[f] \, d^3v$ is the collisional friction force, and $\mathbf{M}_s = \int m_s \mathbf{v} S_s \, d^3v$ is the [momentum density](@entry_id:271360) injection rate from the external source .

-   **Energy Balance:** Multiplying by $\frac{1}{2}m_s v^2$ and integrating gives the evolution of the kinetic energy density $W_s = \int \frac{1}{2}m_s v^2 f_s \, d^3v$:
    $$
    \frac{\partial W_s}{\partial t} + \nabla \cdot \mathbf{Q}_s = \mathbf{J}_s \cdot \mathbf{E} + P_{coll,s} + P_s
    $$
    In this equation, $\mathbf{Q}_s$ is the kinetic energy flux, $\mathbf{J}_s \cdot \mathbf{E}$ is the work done by the electric field, $P_{coll,s} = \int \frac{1}{2}m_s v^2 C_s[f] \, d^3v$ is the power transferred via collisions, and $P_s = \int \frac{1}{2}m_s v^2 S_s \, d^3v$ is the power density delivered by the external source .

These balance equations form the bridge between the microscopic kinetic description and the macroscopic evolution of the plasma. They explicitly show that the velocity moments of the source operator $S_s$ directly correspond to the physical rates of particle, momentum, and energy injection.

#### Electromagnetic Consistency: The Charge Conservation Constraint

When the kinetic simulation is coupled to Maxwell's equations, an additional, powerful constraint emerges. Taking the divergence of Ampère's law ($\nabla\times\mathbf{B} = \mu_0\mathbf{J} + \mu_0\varepsilon_0\frac{\partial \mathbf{E}}{\partial t}$) and combining it with Gauss's law ($\nabla\cdot\mathbf{E} = \rho/\varepsilon_0$) yields the [charge continuity](@entry_id:747292) equation:
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot \mathbf{J} = 0
$$
where $\rho = \sum_s q_s n_s$ and $\mathbf{J} = \sum_s q_s n_s \mathbf{u}_s$ are the total charge and current densities.

However, if we derive the [charge continuity](@entry_id:747292) equation from the kinetic equations by multiplying by $q_s$, summing over species, and integrating over velocity, we find:
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot \mathbf{J} = \sum_s q_s \int S_s \, d^3v
$$
For the kinetic description to be consistent with Maxwell's equations, these two expressions must be equal. This imposes the fundamental constraint that the source term must be locally **charge-neutral** :
$$
\sum_s q_s \int S_s(\mathbf{x}, \mathbf{v}, t) \, d^3v = 0
$$
This means that any process modeled by $S_s$ must inject or remove positive and negative charges at the same rate at every point in space. This constraint does not, however, restrict the injection of net momentum or energy. For example, a [neutral beam](@entry_id:752451) that gets ionized into an ion-electron pair is a charge-neutral source, but it can inject significant net momentum and energy into the plasma.

### A Taxonomy of Source and Sink Models

With the governing principles established, we can explore the construction of specific source and sink models. These models are typically phenomenological but are designed to reproduce the correct conservation properties and macroscopic effects of the physical processes they represent.

#### Particle Sources: Modeling Ionization

A common particle source in fusion plasmas is the ionization of neutral atoms that enter the plasma from the edge or are injected by a [neutral beam](@entry_id:752451). A physically motivated model for this process can be constructed as follows :
$$
S_s(\mathbf{x},\mathbf{v}) = n_n(\mathbf{x}) \nu_{\mathrm{ion}}(\mathbf{x}) M(\mathbf{v}; T_n(\mathbf{x}), \mathbf{U}_n(\mathbf{x}))
$$
This model states that the rate of creation of ions of species $s$ at a location $\mathbf{x}$ with velocity $\mathbf{v}$ is proportional to:
-   The local neutral density, $n_n(\mathbf{x})$.
-   The ionization frequency, $\nu_{\mathrm{ion}}(\mathbf{x})$, which for electron-impact ionization depends on the electron density and temperature: $\nu_{\mathrm{ion}} = n_e \langle \sigma v \rangle_{e,n}(T_e)$.
-   A normalized velocity distribution for the newly born ions, $M(\mathbf{v})$, which is typically assumed to be a Maxwellian distribution reflecting the temperature $T_n$ and mean velocity $\mathbf{U}_n$ of the parent neutral population.

By taking moments of this source term, we can find the exact rates of particle, momentum, and energy injection. Since $\int M(\mathbf{v}) d^3v = 1$, the particle source rate is simply $\Gamma_{p,s} = n_n \nu_{\mathrm{ion}}$. The momentum source rate is $\mathbf{M}_s = m_s (n_n \nu_{\mathrm{ion}}) \mathbf{U}_n$, reflecting the momentum carried by the parent neutrals. The energy source rate is the sum of the thermal and flow energy of the new ions: $P_s = (n_n \nu_{\mathrm{ion}}) (\frac{3}{2} T_n + \frac{1}{2}m_s |\mathbf{U}_n|^2)$. This illustrates how a single, well-defined kinetic operator provides a self-consistent source for all the macroscopic balance equations.

#### Energy Sources and Sinks: Heating and Cooling Operators

Energy can be injected or removed without adding particles. This requires operators whose zeroth moment is zero but whose energy moment is non-zero.

-   **Radio-Frequency (RF) Heating:** The absorption of RF waves by plasma particles is often modeled using a **[quasilinear diffusion operator](@entry_id:1130457)** in [velocity space](@entry_id:181216) .
    $$
    S_{\text{RF}}[f_s] = \nabla_{\mathbf{v}} \cdot \left( \mathbf{D}_{\text{RF}}(\mathbf{v}) \cdot \nabla_{\mathbf{v}} f_s \right)
    $$
    Here, $\mathbf{D}_{\text{RF}}$ is the [quasilinear diffusion](@entry_id:753965) tensor, which is large in the regions of velocity space where particles are resonant with the wave. By virtue of being a pure divergence in [velocity space](@entry_id:181216), this operator exactly conserves particles: $\int S_{\text{RF}} \, d^3v = 0$. However, it systematically pushes particles towards higher energies, resulting in a positive energy moment, $\int \frac{1}{2}m_s v^2 S_{\text{RF}} \, d^3v > 0$, and thus acts as a heating source. Furthermore, if $\mathbf{D}_{\text{RF}}$ is asymmetric in $\mathbf{v}$ (e.g., larger for particles moving in one direction along the magnetic field), it will also have a non-zero momentum moment, which is the mechanism for RF-driven [plasma current](@entry_id:182365).

-   **Radiative Cooling:** Bremsstrahlung and [line radiation](@entry_id:751334) cause electrons to lose energy by emitting photons. This is an energy sink. Crucially, the electron is not destroyed in this process, so the operator must conserve electron number. A model operator that achieves this is a **number-conserving Krook operator** :
    $$
    S_{\text{br}}[f_e] = -\nu_{\text{br}} \left( \frac{E}{T_e} - \frac{3}{2} \right) f_e
    $$
    where $E = \frac{1}{2}m_e v^2$ is the electron kinetic energy. The term $(\frac{E}{T_e} - \frac{3}{2})$ is constructed such that the operator is particle-conserving ($\int S_{\text{br}}[f_e] \, d^3v = 0$), while its energy moment is non-zero. The rate $\nu_{\text{br}}$ is then chosen to ensure that the energy moment of the operator matches the physically-prescribed radiative power loss rate, $P_{\text{br}}$. This operator preferentially "cools" the high-energy electrons that are most responsible for radiation, while "heating" the low-energy electrons to maintain zero net particle change.

#### Momentum Sources: Driving Plasma Rotation

Plasma rotation is critical for stabilizing certain instabilities. It is driven by external sources of momentum. As discussed, [neutral beam injection](@entry_id:204293) (NBI) is a primary example, injecting both particles and momentum . The momentum injected by the source term, $\mathbf{M}_s$, enters the momentum balance equation. In a steady state, this external torque must be balanced by the divergence of the momentum flux ([viscous transport](@entry_id:157790)) and collisional friction forces . For example, in a simplified 1D model of toroidal momentum balance, a constant external toroidal force density $f_0$ balanced by [viscous transport](@entry_id:157790) ($\eta_0 \frac{d^2 u_\varphi}{dx^2}$) and [frictional damping](@entry_id:189251) ($-m_i n_i \nu_0 u_\varphi$) leads to a steady-state rotation profile of the form:
$$
u_{\varphi}(x) = \frac{f_{0}}{m_{i} n_{i} \nu_{0}} \left( 1 - \frac{\cosh(x/L_m)}{\cosh(a/L_m)} \right)
$$
where $L_m = \sqrt{\eta_0 / (m_i n_i \nu_0)}$ is a momentum transport length scale. This shows a direct link between the microscopic source model (whose moment is $f_0$) and the resulting macroscopic flow profile.

### Sources and Sinks in the Global Context

The local source and sink models culminate in a global balance that determines the overall state of the plasma.

#### Achieving Global Power Balance

By integrating the local [energy balance equation](@entry_id:191484) over the entire plasma volume, we obtain a statement of global power balance :
$$
\frac{dW}{dt} = P_{\text{input}} - P_{\text{transport}} - P_{\text{radiation}}
$$
Here, $W$ is the total stored energy in the plasma. $P_{\text{input}}$ is the total power delivered by all heating sources (e.g., the [volume integral](@entry_id:265381) of the energy moment of heating operators). $P_{\text{transport}}$ is the total power lost across the plasma boundary due to turbulent and [neoclassical transport](@entry_id:188243), and $P_{\text{radiation}}$ is the total power lost via radiation. In a steady state, $\frac{dW}{dt} = 0$, and the input power must exactly balance the total losses. This global balance is a fundamental check on the self-consistency of a full-$f$ simulation and allows for direct comparison with experimental measurements.

#### Flux-Driven versus Profile-Driven Simulations: A Methodological Contrast

Finally, the way sources are implemented defines the simulation strategy, with profound implications for the study of turbulence. There are two main paradigms :

1.  **Flux-Driven Simulation:** In this approach, a source (e.g., of heat) is prescribed with a fixed magnitude, often localized in the plasma core. The simulation is then forced to transport this fixed input flux across the domain. The plasma profiles and their gradients are not directly controlled; they are free to evolve dynamically. This allows the system to self-organize, fully capturing the "predator-prey" dynamics between gradients and turbulence. This approach is considered more physically realistic and is necessary for studying phenomena like transport barrier formation and turbulent avalanches.

2.  **Profile-Driven Simulation:** In this approach, the source term is designed to relax the plasma profile towards a predefined target profile, $X_\star(r)$. For example, using a source term of the form $S_X = \omega_X (X_\star - X)$. This method effectively "clamps" the gradients, which are the primary drive for turbulence. While computationally stable and useful for studying local turbulent [transport properties](@entry_id:203130) at a fixed gradient, this method artificially breaks the feedback loop between transport and profile evolution. It suppresses large-scale self-organization and can bias the observed turbulent dynamics.

In conclusion, [sources and sinks](@entry_id:263105) are not mere numerical conveniences but are integral components of a physically complete kinetic model. Their construction must obey fundamental conservation laws and electromagnetic consistency. Through their moments, they directly drive the macroscopic evolution of the plasma, and the strategy for their implementation dictates the very nature of the scientific questions a full-$f$ simulation can address.