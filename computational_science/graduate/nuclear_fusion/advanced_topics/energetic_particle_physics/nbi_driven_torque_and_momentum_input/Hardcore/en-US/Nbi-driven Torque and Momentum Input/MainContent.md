## Introduction
Plasma rotation is a critical parameter in modern [tokamak](@entry_id:160432) experiments, profoundly influencing magnetohydrodynamic (MHD) stability, [turbulent transport](@entry_id:150198), and overall plasma performance. Achieving control over the rotation profile is therefore a key goal for optimizing fusion energy production. One of the most powerful and widely used methods for driving this rotation is Neutral Beam Injection (NBI). While seemingly straightforward, the process by which NBI delivers momentum and establishes a macroscopic rotation profile involves a complex chain of physics, from the injection of single particles to their collective interaction with the plasma and the subsequent redistribution of momentum. This article aims to bridge this knowledge gap by providing a comprehensive overview of NBI-driven torque and [momentum transport](@entry_id:139628).

The first chapter, **Principles and Mechanisms**, lays the theoretical foundation, explaining how momentum is transferred from beam particles to the plasma, distinguishing between mechanical and [canonical momentum](@entry_id:155151), and detailing the transport models that govern its radial transport. The second chapter, **Applications and Interdisciplinary Connections**, explores how this injected torque is used as a practical tool to stabilize instabilities, improve confinement, and probe transport physics, highlighting its deep connections to nearly every subfield of plasma science. Finally, the **Hands-On Practices** section provides guided problems to solidify understanding of key concepts like radial force balance, momentum pinch dynamics, and charge-exchange losses.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms governing the injection, transfer, transport, and loss of toroidal momentum in tokamak plasmas, with a primary focus on Neutral Beam Injection (NBI) as the driving source. We will begin with the foundational mechanics of how a single beam particle imparts momentum to the plasma, distinguish between the mechanical and [canonical forms](@entry_id:153058) of momentum, and then explore the complex processes of momentum [thermalization](@entry_id:142388) and macroscopic transport.

### The Injection and Conservation of Toroidal Momentum

#### The Mechanism of Neutral Beam Injection

The primary function of Neutral Beam Injection (NBI) is to deliver high-energy particles deep into the core of a [magnetically confined plasma](@entry_id:202728). A direct injection of ions is unfeasible, as the strong confining magnetic fields would exert a powerful Lorentz force, $\mathbf{F} = q(\mathbf{E} + \mathbf{v} \times \mathbf{B})$, deflecting the ions at the plasma edge and preventing them from penetrating to the core. To circumvent this, NBI systems employ a multi-step process. First, ions (typically hydrogen isotopes like deuterium) are generated and accelerated to high energies, ranging from tens of keV to over an MeV. This energetic ion beam is then passed through a gas cell, known as a neutralizer, where the fast ions undergo [charge-exchange reactions](@entry_id:161098), capturing an electron to become fast neutral atoms.

Being electrically neutral, these fast atoms are impervious to the magnetic fields and can travel in straight lines across the plasma boundary and into the core. Once inside the hot, dense plasma, the fast neutrals are ionized through collisions with plasma electrons and ions. At the instant of ionization, a fast neutral atom of mass $m_b$ and velocity $\mathbf{v}_b$ becomes a fast ion, which is now trapped by the magnetic field. This newly created fast ion possesses significant kinetic energy and momentum, which it subsequently transfers to the bulk plasma through collisions, resulting in heating and toroidal rotation.

The fundamental momentum input from this process is the mechanical angular momentum imparted by each beam particle at the moment of [ionization](@entry_id:136315). The toroidal angular momentum, $L_\phi$, is the component of the angular momentum vector, $\mathbf{L} = \mathbf{r} \times \mathbf{p}$, along the [tokamak](@entry_id:160432)'s [axis of symmetry](@entry_id:177299). For a particle of mass $m_b$ ionized at a major radius $R$, with a toroidal velocity component $v_\phi$, its linear momentum in the toroidal direction is $p_\phi = m_b v_\phi$. The [lever arm](@entry_id:162693) for this momentum component with respect to the symmetry axis is the major radius $R$. Therefore, the mechanical toroidal angular momentum delivered at the instant of ionization is :
$$
L_\phi = R p_\phi = m_b R v_\phi
$$
This quantity represents the initial mechanical torque source from a single NBI particle. The collective effect of billions of such events per second provides a continuous torque that drives the plasma's toroidal rotation.

#### Mechanical versus Canonical Toroidal Momentum

In the electromagnetic environment of a tokamak, it is crucial to distinguish between **mechanical momentum** and **canonical momentum**. The mechanical toroidal angular momentum, as defined above, is the quantity associated with the physical motion of the particles, $L_\phi = m_i R v_\phi$. This is the quantity that directly corresponds to the plasma's rotation.

However, for a charged particle moving in a magnetic field, the conserved quantity in the presence of toroidal symmetry is the canonical toroidal momentum, $P_\phi$. It is derived from the Lagrangian formulation of mechanics and includes a contribution from the magnetic field itself. For a particle of mass $m_i$ and charge $q_i = Z_i e$, the canonical toroidal momentum is given by:
$$
P_\phi = m_i R v_\phi + q_i R A_\phi
$$
where $A_\phi$ is the toroidal component of the magnetic vector potential. In an axisymmetric tokamak, the quantity $R A_\phi$ is directly related to the poloidal magnetic flux function, $\psi$, which labels nested [magnetic flux surfaces](@entry_id:751623). Choosing a standard gauge, we can write $\psi \approx R A_\phi$. Thus, the canonical toroidal momentum is expressed as :
$$
P_\phi = m_i R v_\phi + q_i \psi
$$
The first term is the mechanical momentum, and the second, $q_i \psi$, is the [electromagnetic momentum](@entry_id:268129) associated with the particle's interaction with the confining field.

According to Noether's theorem, if the system is perfectly axisymmetric (i.e., the electromagnetic fields have no dependence on the toroidal angle $\phi$), then $\phi$ is an ignorable coordinate in the Lagrangian, and the conjugate canonical momentum, $P_\phi$, is a constant of motion for a collisionless particle. This conservation law holds even if the fields, and thus $\psi$, vary in time, as long as the axisymmetry is preserved. This law dictates a direct trade-off: if a [particle drifts](@entry_id:753203) radially to a different flux surface (changing its $\psi$), its mechanical momentum $m_i R v_\phi$ must change to keep $P_\phi$ constant. This principle governs the behavior of single particles but also forms the foundation for understanding macroscopic momentum conservation and its violation.

### Slowing-Down Dynamics and Momentum Partitioning

Once a fast ion is born inside the plasma, it begins to slow down via Coulomb collisions, transferring its momentum and energy to the background electrons and ions. The efficiency of the NBI system in driving [plasma rotation](@entry_id:753506) depends critically on how this momentum is partitioned.

#### The Critical Energy and Momentum Partition

The collisional drag force on a fast ion can be separated into contributions from background electrons, $\mathbf{F}_e$, and background ions, $\mathbf{F}_i$. The rate at which momentum is transferred to each species is equal to the magnitude of these respective drag forces. The relative strength of these forces depends strongly on the fast ion's energy, $E$.

For interactions with background ions, which are typically much slower than the fast ion ($v \gg v_{th,i}$), the drag force behaves like Rutherford scattering, with a magnitude scaling as $|\mathbf{F}_i| \propto E^{-1}$. For interactions with electrons, which are typically much faster than the fast ion ($v \ll v_{th,e}$), the drag force behaves like viscous drag, with a magnitude scaling as $|\mathbf{F}_e| \propto v \propto E^{1/2}$.

The **[critical energy](@entry_id:158905)**, $E_c$, is defined as the fast-ion energy at which the drag forces from electrons and ions are equal: $|\mathbf{F}_e(E_c)| = |\mathbf{F}_i(E_c)|$. Using the energy scalings of the drag forces, one can derive the fraction of momentum instantaneously transferred to the electrons, $f_e(E)$, as a function of the fast-ion energy $E$ relative to $E_c$ :
$$
f_e(E) = \frac{|\mathbf{F}_e(E)|}{|\mathbf{F}_e(E)| + |\mathbf{F}_i(E)|} = \frac{1}{1 + (E_c/E)^{3/2}}
$$
This relationship shows that:
*   For high-energy fast ions ($E \gg E_c$), $f_e(E) \to 1$, and momentum is predominantly transferred to electrons.
*   For low-energy fast ions ($E \ll E_c$), $f_e(E) \to 0$, and momentum is predominantly transferred to ions.
*   At the [critical energy](@entry_id:158905) ($E = E_c$), momentum is shared equally, $f_e(E_c) = 0.5$.

#### The Role of Plasma Parameters in Torque Efficiency

The [critical energy](@entry_id:158905) $E_c$ is not a constant; it depends on the plasma parameters. A key dependence is on the [electron temperature](@entry_id:180280), $T_e$. A more detailed derivation shows that, for a test particle of mass $m_t$ in a plasma with background ions of mass $m_i$ :
$$
E_c \propto T_e \frac{m_t}{m_i^{2/3} m_e^{1/3}}
$$
The direct proportionality, $E_c \propto T_e$, has a significant consequence for torque efficiency. Since toroidal rotation is driven by momentum transferred to the massive ions, maximizing this transfer is desirable. By increasing the [electron temperature](@entry_id:180280) $T_e$, one increases $E_c$. For a fixed beam injection energy $E_b$, a higher $E_c$ means that the beam ion spends a larger fraction of its slowing-down time in the energy regime $E  E_c$, where [momentum transfer](@entry_id:147714) to background ions is dominant. Therefore, operating at higher electron temperatures generally improves the efficiency of NBI-driven torque.

#### From Electrons to Ions: The Importance of Collisional Coupling

The analysis above might suggest that if $E_b \gg E_c$, the injected momentum is "wasted" on the electrons. However, this conclusion is incomplete. The crucial next step is to consider the interaction between the background electrons and ions themselves. Any momentum imparted to the electron fluid is subject to two competing processes: it can be lost from the plasma via transport (on a characteristic momentum confinement timescale, $\tau_\phi$), or it can be transferred to the ion fluid via electron-ion collisions.

The rate of this collisional momentum exchange is characterized by the electron-ion collision frequency, $\nu_{ei}$. In typical hot, dense [tokamak](@entry_id:160432) plasmas, this frequency is very high. For example, in a plasma with $n_e = 8 \times 10^{19} \text{ m}^{-3}$ and $T_e = 3 \text{ keV}$, the characteristic time for [momentum transfer](@entry_id:147714) from electrons to ions is $\tau_{ei} \sim 1/\nu_{ei} \approx 40 \text{ } \mu\text{s}$. This is typically orders of magnitude shorter than the global [momentum confinement time](@entry_id:752134), which is often in the range of tens of milliseconds ($\tau_\phi \sim 50 \text{ ms}$).

This condition, $\tau_{ei} \ll \tau_\phi$ (or equivalently, $\nu_{ei} \gg 1/\tau_\phi$), signifies extremely strong collisional coupling between the electron and ion fluids. As a result, any toroidal momentum the electrons receive from the fast ions is almost immediately transferred to the ions. The two species are forced to rotate together at nearly the same toroidal velocity. Because the ions are vastly more massive than the electrons ($m_i \gg m_e$), even with equal velocities, the ions carry almost all of the plasma's total mechanical momentum ($P_{i\phi} / P_{e\phi} = n_i m_i v_{i\phi} / (n_e m_e v_{e\phi}) \approx m_i/m_e \gg 1$). Therefore, regardless of whether the initial slowing-down is dominated by electrons or ions, the strong collisional coupling ensures that the injected toroidal momentum ultimately resides in the bulk ions .

### Macroscopic Transport of Toroidal Momentum

The momentum deposited by NBI is not confined to the deposition region. It is redistributed radially by various transport mechanisms, setting up a [plasma rotation](@entry_id:753506) profile. Understanding this transport is key to predicting and controlling [plasma rotation](@entry_id:753506).

#### The Momentum Transport Equation

The evolution of the flux-surface-averaged toroidal angular [momentum density](@entry_id:271360), $\langle L_\phi \rangle = \langle n_i m_i R v_\phi \rangle$, is governed by a 1D radial transport equation in [conservative form](@entry_id:747710):
$$
\frac{\partial \langle L_\phi \rangle}{\partial t} + \frac{1}{V'} \frac{\partial}{\partial r} (V' \Pi_\phi) = \langle T_\phi \rangle
$$
Here, $r$ is a radial flux-surface label, $V'(r)$ is the differential volume of a flux-surface shell, $\Pi_\phi$ is the radial flux of toroidal angular momentum, and $\langle T_\phi \rangle$ is the flux-surface-averaged density of external torques (like NBI) and sinks.

From the ion fluid momentum equation, this flux is composed of two primary mechanical contributions: a convective part due to bulk radial plasma flow, and a stress part due to viscosity . The total radial flux of toroidal angular momentum is given by:
$$
\Pi_\phi = \langle R (n_i m_i v_r v_\phi - \pi_{r\phi}) \rangle
$$
where $v_r$ is the radial fluid velocity and $\pi_{r\phi}$ is the $r-\phi$ component of the [viscous stress](@entry_id:261328) tensor, which describes the transport of toroidal momentum in the radial direction due to microscopic fluctuations and collisions.

#### Phenomenological Transport Model: Diffusivity, Pinch, and Residual Stress

In practice, the momentum flux $\Pi_\phi$ is often described by a [phenomenological model](@entry_id:273816) that parameterizes the complex underlying physics. A standard linear model decomposes the flux into diffusive, convective (or "pinch"), and [residual stress](@entry_id:138788) components. The full [transport equation](@entry_id:174281) for the toroidal [angular frequency](@entry_id:274516) $\omega_\phi = v_\phi/R$ takes the form :
$$
\frac{\partial}{\partial t} (n m R^2 \omega_\phi) = \frac{1}{V'} \frac{\partial}{\partial r} \left( V' n m R^2 \chi_\phi \frac{\partial \omega_\phi}{\partial r} \right) - \frac{1}{V'} \frac{\partial}{\partial r} \left( V' n m R^2 V_\phi \omega_\phi \right) + S_L - \mathcal{D}_\phi
$$
Let's examine the key transport coefficients in the corresponding flux expression $\Pi_\phi = -n m R^2 \chi_\phi \frac{\partial\omega_\phi}{\partial r} + n m R^2 V_\phi \omega_\phi$:

1.  **Momentum Diffusivity ($\chi_\phi$)**: The coefficient $\chi_\phi$, with units of $\text{m}^2/\text{s}$, represents [diffusive transport](@entry_id:150792). This term drives a flux of momentum down the gradient of angular frequency, $\partial\omega_\phi/\partial r$. It is a Fickian process that tends to flatten the rotation profile. The use of $\omega_\phi$ as the gradient quantity (rather than $v_\phi$) is physically motivated by the requirement that the [diffusive flux](@entry_id:748422) must vanish for a [rigid-body rotation](@entry_id:268623) ($\omega_\phi = \text{constant}$), which is a state of thermodynamic-like equilibrium for momentum .

2.  **Momentum Pinch ($V_\phi$)**: The coefficient $V_\phi$, a [radial velocity](@entry_id:159824) with units of $\text{m/s}$, represents a [convective transport](@entry_id:149512) of momentum that is proportional to the local [momentum density](@entry_id:271360) itself, not its gradient. This "pinch" term describes a non-diffusive advection of momentum. Experimentally, rotation profiles are often observed to be more peaked than can be explained by diffusion and the known torque source profile alone. This is particularly evident in cases with off-axis NBI torque, where the rotation profile nonetheless peaks at the magnetic axis ($r=0$). This phenomenon is explained by an inward momentum pinch. In the standard sign convention (outward flux is positive), an inward pinch corresponds to $V_\phi  0$. This negative $V_\phi$ generates an inward [convective flux](@entry_id:158187), $\Pi_{\text{conv}} = (n m R^2 \omega_\phi) V_\phi  0$, which transports momentum "uphill" against the density gradient, thereby sharpening the rotation profile .

3.  **Residual Stress ($\Pi_{\text{res}}$)**: More sophisticated models include a third component in the [momentum flux](@entry_id:199796), known as **[residual stress](@entry_id:138788)**. This is a non-[diffusive flux](@entry_id:748422) that can exist even when both the rotation and its gradient are zero. It arises from symmetry breaking in the underlying turbulence (e.g., due to $E \times B$ shear or magnetic geometry). The flux model becomes $\Pi_\phi = -n m R^2 \chi_\phi \frac{\partial\omega_\phi}{\partial r} + \Pi_{\text{pinch}} + \Pi_{\text{res}}$. The existence of [residual stress](@entry_id:138788) is profound: in a steady-state, source-free plasma ($\langle S_L \rangle = 0$), the total flux must be zero. A non-zero $\Pi_{\text{res}}$ must be balanced by the diffusive and pinch fluxes, which requires a finite rotation gradient. In this way, [residual stress](@entry_id:138788) can drive **intrinsic rotation**—[plasma rotation](@entry_id:753506) without any external torque input. The presence of residual stress also complicates the experimental inference of transport coefficients. For instance, a naive calculation of diffusivity, $\chi_\phi^{\text{app}} = -\Pi_\phi / (n m R^2 \partial\omega_\phi/\partial r)$, will be contaminated by the [residual stress](@entry_id:138788) term, leading to an apparent diffusivity that may differ significantly from the true value and could even be negative .

### Momentum Sinks

A steady-state rotation profile is achieved when the input torque from sources like NBI is balanced by momentum losses, or "sinks."

#### Mechanical Momentum Sinks: Charge-Exchange

A dominant sink for **mechanical toroidal momentum** in the plasma edge region is **charge-exchange (CX)** with cold neutral atoms. These neutrals originate from [gas puffing](@entry_id:749726) and recycling of ions that strike the vessel walls. When a rotating plasma ion collides with a slow-moving neutral, an electron can be transferred from the neutral to the ion. The result is a fast neutral atom (with the original velocity of the ion) and a new, cold ion (with the original velocity of the neutral).

The fast neutral is no longer confined by the magnetic field. If this event occurs near the edge, the neutral has a high probability of escaping the plasma and striking the material wall, permanently removing its momentum $m_i R v_\phi$ from the system. Meanwhile, the new, non-rotating ion dilutes the plasma's average rotation. This process acts as a powerful friction or drag on the [plasma rotation](@entry_id:753506). Crucially, this is a purely kinetic process of [particle exchange](@entry_id:154910) and loss, and it operates perfectly well within a perfectly axisymmetric system .

#### Canonical Momentum Sinks: Breaking the Symmetry

Sinks for **canonical toroidal momentum** are fundamentally different. As established by Noether's theorem, the total canonical momentum of a plasma, $P_\phi^{\text{total}}$, can only be changed by an external toroidal torque that breaks the toroidal axisymmetry. Mechanical sinks like CX, while removing momentum from the plasma volume, do so by physically removing particles that carry momentum; they do not violate the underlying symmetry of the fields.

An electromagnetic sink of canonical momentum, by contrast, is a torque exerted by the fields themselves on the charged plasma. A common example is the torque from externally applied, non-axisymmetric magnetic fields, such as those used for Edge Localized Mode (ELM) mitigation or those arising from coil misalignments (error fields). These fields create a drag on the [plasma rotation](@entry_id:753506), formally appearing as a non-zero flux-surface-averaged toroidal Lorentz force, $\langle R(\mathbf{J} \times \mathbf{B})_\phi \rangle \neq 0$. This term directly represents a change in the plasma's total [canonical momentum](@entry_id:155151) and is a direct consequence of the [broken symmetry](@entry_id:158994) .