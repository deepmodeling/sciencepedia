## Introduction
Neutral Beam Injection (NBI) is a cornerstone technology for modern fusion research, serving as a powerful and versatile method for heating plasmas to thermonuclear temperatures, driving non-inductive currents for [steady-state operation](@entry_id:755412), and controlling plasma rotation. The effectiveness of NBI hinges on a complex sequence of physical phenomena, from the creation of an energetic [neutral beam](@entry_id:752451) to its intricate interaction with the [magnetically confined plasma](@entry_id:202728). Accurately predicting and optimizing these effects requires sophisticated computational models that can capture this multi-stage journey with high fidelity. This article addresses the need for a comprehensive understanding of NBI modeling by systematically deconstructing the underlying physics and its application in a computational context.

The following sections will guide you through the essential aspects of modeling [neutral beam injection](@entry_id:204293). We will begin in **"Principles and Mechanisms"** by exploring the fundamental physics, from the generation and neutralization of the beam to its attenuation in the plasma and the subsequent behavior of the resulting fast ions. Next, **"Applications and Interdisciplinary Connections"** will demonstrate how these models are applied, serving as critical inputs for simulations of plasma transport, equilibrium, and stability, as well as enabling advanced [plasma diagnostics](@entry_id:189276). Finally, **"Hands-On Practices"** will provide opportunities to apply these concepts through targeted computational exercises, solidifying your understanding of the techniques used in modern NBI codes.

## Principles and Mechanisms

The efficacy of Neutral Beam Injection (NBI) as a tool for plasma heating, current drive, and momentum injection hinges on a sequence of physical processes, each governed by fundamental principles of [atomic physics](@entry_id:140823), electromagnetism, and plasma kinetics. This section systematically deconstructs the journey of a beam particle, from its origin in an ion source to its [thermalization](@entry_id:142388) within the tokamak plasma. We will explore the mechanisms that determine the beam's quality, its transport to and through the plasma, and its ultimate interaction with the confined plasma volume.

### Generation of the Neutral Beam

The creation of a high-power beam of energetic neutral atoms is a multi-stage process, beginning with the extraction and acceleration of ions, followed by their conversion to neutrals. The characteristics of the final neutral beam are largely determined during these initial stages.

#### Ion Source and Beam Quality: Emittance

The quality of a particle beam is often quantified by its **emittance**, a measure of the volume it occupies in phase space. For a beam propagating primarily along the $z$-axis, the transverse geometric emittance characterizes the beam's spread in both position ($x$) and angle ($x' = v_x / v_z$). The root-mean-square (rms) geometric emittance, $\epsilon$, in one transverse plane is defined by $\epsilon = \sqrt{\langle x^2 \rangle \langle x'^2 \rangle - \langle x x' \rangle^2}$, where the angle brackets denote an average over the particle distribution. A lower emittance corresponds to a more collimated, higher-quality beam.

The minimum possible emittance is set by the intrinsic properties of the ion source itself. Ions are extracted from a source plasma with a finite transverse temperature, $T_\perp$. This temperature corresponds to a Maxwell-Boltzmann distribution of transverse velocities. From kinetic theory, the mean square transverse velocity is $\langle v_x^2 \rangle = k_B T_\perp / m$, where $k_B$ is the Boltzmann constant and $m$ is the ion mass. After acceleration to a high axial velocity $v_z \approx v$, the rms angular spread is $\sqrt{\langle x'^2 \rangle} \approx \sqrt{\langle v_x^2 \rangle} / v$. Assuming the beam is extracted from an [aperture](@entry_id:172936) with rms spatial size $\sigma_x = \sqrt{\langle x^2 \rangle}$ and that there is negligible correlation between particle position and angle at the source ($\langle x x' \rangle \approx 0$), the geometric emittance is approximately $\epsilon \approx \sigma_x \sqrt{\langle x'^2 \rangle}$.

A more fundamental quantity is the **normalized emittance**, $\epsilon_n = \beta \gamma \epsilon$, where $\beta = v/c$ and $\gamma = (1-\beta^2)^{-1/2}$ are the relativistic factors. Substituting the expressions for $\epsilon$ and $\langle x'^2 \rangle$, we find a direct link between the normalized emittance and the source temperature :
$$
\epsilon_n = (\beta \gamma) \left( \frac{\sigma_x}{v} \sqrt{\frac{k_B T_\perp}{m}} \right) = \frac{\gamma \sigma_x}{c} \sqrt{\frac{k_B T_\perp}{m}}
$$
This relation reveals that the source [ion temperature](@entry_id:191275) $T_\perp$ establishes a fundamental lower limit on the [beam emittance](@entry_id:184476), a manifestation of the conservation of [phase space volume](@entry_id:155197) known as Liouville's theorem. For instance, for a deuterium beam extracted with a typical transverse temperature of $T_\perp = 2 \, \mathrm{eV}$ from a [circular aperture](@entry_id:166507) of radius $a=0.5 \, \mathrm{mm}$ (for which $\sigma_x = a/2$), the resulting normalized emittance at a beam energy of $100 \, \mathrm{keV}$ is on the order of $8 \times 10^{-6} \, \mathrm{mm \cdot rad}$, a small but non-zero value representing the intrinsic divergence of the beam.

#### Multi-Species Beams in Positive-Ion NBI

Conventional NBI systems, known as positive-ion NBI (P-NBI), extract positive ions from a plasma source. For a deuterium beam, the source plasma contains not only atomic ions ($\mathrm{D}^+$) but also molecular ions ($\mathrm{D}_2^+$ and $\mathrm{D}_3^+$). All these singly-charged ion species are extracted and accelerated through the same electrostatic potential, $V$. Consequently, each ion, regardless of its mass, gains the same kinetic energy, $E_{ion} = e V \equiv E_0$.

In the subsequent neutralizer stage, these energetic molecular ions dissociate. A $\mathrm{D}_2^+$ ion, carrying total energy $E_0$, breaks into two deuterium atoms, which share the energy, resulting in two neutrals each with energy $E_0/2$. Similarly, a $\mathrm{D}_3^+$ ion dissociates into three neutrals, each with energy $E_0/3$. The atomic $\mathrm{D}^+$ ions simply become neutrals with the full energy, $E_0$.

This process invariably produces a neutral beam composed of three distinct energy components: the **full-energy**, **half-energy**, and **third-energy** components . The total power delivered by the beam is distributed among these components. If the particle number fractions of the injected neutrals at energies $E_0$, $E_0/2$, and $E_0/3$ are $f_1$, $f_{1/2}$, and $f_{1/3}$ respectively, the fraction of the total power carried by the full-energy component is:
$$
w_1 = \frac{f_1 E_0}{f_1 E_0 + f_{1/2} (E_0/2) + f_{1/3} (E_0/3)} = \frac{f_1}{f_1 + f_{1/2}/2 + f_{1/3}/3}
$$
For a typical beam with particle fractions $f_1=0.7$, $f_{1/2}=0.2$, and $f_{1/3}=0.1$, the full-energy component carries $w_1 \approx 0.84$, or $84\%$, of the power. While the full-energy component is dominant, the presence of lower-energy species has significant consequences for beam penetration and slowing-down dynamics, as will be discussed later.

#### Neutralization: Converting Ions to Neutrals

To cross the confining magnetic fields of a tokamak, the accelerated particles must be electrically neutral. The process of neutralization is the most critical step distinguishing different NBI technologies.

A simple model for neutralization in a gas cell of length $L$ and uniform gas density $n_g$ treats the process as a simple attenuation of the ion beam. An ion has a probability $n_g \sigma_{cx} dx$ of undergoing a charge-exchange collision in an infinitesimal length $dx$, where $\sigma_{cx}$ is the neutralization cross-section. Integrating over the length of the neutralizer, the fraction of ions that are converted to neutrals, defined as the **neutralization efficiency** $f_n$, is given by :
$$
f_n = 1 - \exp(-n_g \sigma_{cx} L)
$$
The term $n_g \sigma_{cx} L$ is the **[optical depth](@entry_id:159017)** of the neutralizer. This efficiency quantifies only the conversion process within the neutralizer and must be distinguished from the overall **transmission efficiency** of the beamline, which also accounts for geometric losses and other particle loss mechanisms.

The critical factor in this process is the cross-section, which depends strongly on the ion species (positive or negative) and its energy. This dependence dictates the choice of NBI technology for different applications .

For **positive-ion NBI (P-NBI)**, neutralization occurs via [electron capture](@entry_id:158629) (charge exchange), e.g., $\mathrm{D}^+ + \mathrm{D}_2 \rightarrow \mathrm{D}^0 + \dots$. The cross-section for this reaction, $\sigma_{cx}$, decreases rapidly with increasing beam energy. As a result, the achievable neutralization efficiency becomes unacceptably low for energies above approximately $150 \, \mathrm{keV}$. This physical limitation makes P-NBI unsuitable for future large-scale fusion reactors, which require beam energies in the mega-[electron-volt](@entry_id:144194) (MeV) range for the neutrals to penetrate the large, dense plasma core.

For **negative-ion NBI (N-NBI)**, the process is electron stripping, e.g., $\mathrm{D}^- + \mathrm{D}_2 \rightarrow \mathrm{D}^0 + e^- + \dots$. The cross-section for single-electron stripping decreases much more slowly with energy, making N-NBI viable at MeV energies. However, in a gas neutralizer, this process competes with double-stripping ($\mathrm{D}^- \rightarrow \mathrm{D}^+$), which limits the maximum theoretical efficiency to around $55-60\%$. An advanced concept, laser photodetachment, uses a high-power laser to selectively detach the weakly bound outer electron of the negative ion. This process has no competing channels and can in principle achieve neutralization efficiencies exceeding $90\%$. Consequently, N-NBI is the only technology capable of providing the MeV-class neutral beams required for heating and [current drive](@entry_id:186346) in reactor-scale devices like ITER.

### Transport and Attenuation of the Neutral Beam

Once created, the [neutral beam](@entry_id:752451) must travel from the neutralizer to the tokamak and penetrate the plasma to deposit its energy and momentum. During this transit, several loss and attenuation mechanisms are active.

#### Beamline Losses: Re-ionization in the Duct

The duct connecting the NBI system to the tokamak is not a perfect vacuum; it contains some residual background gas. As the energetic neutrals traverse this duct, they can be re-ionized by collisions with these gas molecules. This process represents a loss, as the newly formed ions will be deflected by the tokamak's fringe magnetic fields and will not enter the plasma.

The probability of a neutral surviving a path length $L$ through a duct with residual gas density $n_g(l)$ is governed by the same kinetic principles as neutralization. The [survival probability](@entry_id:137919) $P_s$ against re-ionization (with cross-section $\sigma_r$) is given by an exponential attenuation law :
$$
P_s(L) = \exp\left(-\int_{0}^{L} n_g(l) \sigma_r(E) dl\right)
$$
The probability of re-ionization is then $P_r = 1 - P_s(L)$. For a typical duct several meters long with a residual gas density on the order of $10^{18} \, \mathrm{m}^{-3}$, the re-ionization loss fraction can be a few percent. This process must be distinguished from the desired ionization that occurs within the [high-density plasma](@entry_id:187441), which involves a different set of target particles (electrons and ions) and a more complex set of interactions.

#### Beam Penetration and Deposition Profile

Upon entering the plasma, the [neutral beam](@entry_id:752451) is attenuated by several collisional processes that ionize the beam atoms. The primary mechanisms are:
1.  **Charge Exchange (CX):** A beam neutral transfers its electron to a plasma ion, e.g., $\mathrm{D}^0_{beam} + \mathrm{D}^+_{plasma} \rightarrow \mathrm{D}^+_{beam} + \mathrm{D}^0_{plasma}$.
2.  **Ion-Impact Ionization:** A collision with a plasma ion strips the electron from the beam neutral, e.g., $\mathrm{D}^0_{beam} + \mathrm{D}^+_{plasma} \rightarrow \mathrm{D}^+_{beam} + \mathrm{D}^+_{plasma} + e^-$.
3.  **Electron-Impact Ionization:** A collision with a plasma electron strips the electron, e.g., $\mathrm{D}^0_{beam} + e^-_{plasma} \rightarrow \mathrm{D}^+_{beam} + 2e^-$.

Each of these processes contributes to the stopping of the beam. The effectiveness of each channel is characterized by its cross-section. The **mean free path** ($\lambda$) for a given process is the average distance a beam neutral travels before undergoing that interaction and is given by $\lambda = (n_{target} \sigma)^{-1}$, where $n_{target}$ is the density of the target species and $\sigma$ is the relevant cross-section .

The total attenuation is determined by the sum of the rates of all processes. The beam intensity $I$ decreases with [penetration depth](@entry_id:136478) $s$ approximately as $I(s) = I_0 \exp(-s/\lambda_{eff})$, where the effective mean free path $\lambda_{eff}$ is determined by the plasma density, composition, and the relevant [cross-sections](@entry_id:168295). For a $100 \, \mathrm{keV}$ deuterium beam in a plasma with density $n_e = n_D = 3 \times 10^{19} \, \mathrm{m}^{-3}$, the mean free path for [charge exchange](@entry_id:186361) is approximately $0.7 \, \mathrm{m}$, while for ion-impact ionization it is nearly $7 \, \mathrm{m}$, indicating the dominance of charge exchange in this regime.

Crucially, the deposition profile of the beam energy and particles can be controlled by the injection geometry. For a beam injected in the poloidal plane, the key geometric parameter is the **tangency radius** $R_t$, defined as the minimum major radius the beam path reaches. Plasma parameters like density and temperature are typically constant on magnetic flux surfaces. In a simplified model of concentric circular flux surfaces, the beam path length $dl$ within a thin radial shell $dr$ can be shown to vary as $dl/dr \propto r/\sqrt{r^2 - R_t^2}$. This expression reveals a mathematical singularity, known as a **[caustic](@entry_id:164959)**, at $r = R_t$. This means the beam spends a disproportionately long path length in the flux surfaces near the tangency radius. This path-length amplification effect strongly peaks the beam's ionization and energy deposition profiles near $r=R_t$ . By adjusting the beam's aim, and thus changing $R_t$, operators can controllably deposit heat and particles in specific regions of the plasma, from the core to the edge.

### Interaction of Fast Ions with the Plasma

When a beam neutral is ionized, it becomes a fast ion, a highly energetic particle that is now confined by the tokamak's magnetic field. The subsequent behavior of this fast ion—how it transfers its energy and momentum to the bulk plasma and what loss channels it may be subject to—is central to the effect of NBI.

#### The Birth of a Fast Ion and Toroidal Momentum Injection

The act of ionization itself is a critical event for momentum input. In an axisymmetric tokamak, the **[canonical toroidal momentum](@entry_id:1122015)**, $P_\phi$, of a charged particle is a conserved quantity in the absence of collisions or non-axisymmetric fields. It is defined as:
$$
P_\phi = m R^2 \dot{\phi} + q R A_\phi = m R v_\phi + q R A_\phi
$$
where $R$ is the major radius, $v_\phi$ is the toroidal velocity, $q$ is the particle's charge, and $A_\phi$ is the toroidal component of the [magnetic vector potential](@entry_id:141246), which is related to the [poloidal magnetic flux](@entry_id:1129914).

A neutral atom has $q=0$, so its [canonical momentum](@entry_id:155151) is purely mechanical: $P_{\phi, neutral} = m R v_\phi$. At the instant of ionization, the particle's position $R$ and velocity $v_\phi$ are unchanged, but its charge abruptly changes to $q=+e$. Its canonical momentum instantly becomes $P_{\phi, ion} = m R v_\phi + e R A_\phi$. This new value of $P_\phi$ is then conserved as the ion gyrates and drifts in the axisymmetric fields. The change in [canonical momentum](@entry_id:155151) at ionization, $\Delta P_\phi = e R A_\phi$, represents an injection of momentum into the plasma system . The Lorentz force subsequently acts on the particle, converting this "potential" momentum into mechanical momentum, which is then transferred to the bulk plasma via collisions, driving toroidal rotation. For a 1 MA plasma current, a deuterium neutral ionizing at $R = 2.0 \, \mathrm{m}$ receives an instantaneous change in canonical momentum of approximately $6.4 \times 10^{-20} \, \mathrm{kg \cdot m^2/s}$.

#### Slowing Down of Fast Ions

The newly created fast ion possesses energy far greater than the thermal energy of the background plasma particles. It thermalizes primarily through a multitude of small-angle Coulomb collisions with background electrons and ions. The characteristic time for a fast ion to lose most of its energy and merge with the thermal population is the **slowing-down time**, $\tau_s$. This time depends strongly on the fast ion's energy $E$, generally scaling as $\tau_s \propto E^{3/2}$ when slowing on ions is significant . This has important consequences for multi-species beams. The full-, half-, and third-energy components will thermalize on different timescales. For a $100 \, \mathrm{keV}$ deuterium beam, the half-energy ($50 \, \mathrm{keV}$) component slows down about three times faster than the full-energy component, and the third-energy ($33.3 \, \mathrm{keV}$) component slows down more than five times faster. The overall heating dynamic is thus a superposition of these different [thermalization](@entry_id:142388) processes, weighted by the power fraction of each species. This also impacts the current-drive efficiency, as higher-energy, longer-lived fast ions are more effective at driving current.

#### Loss of Fast Ions: Magnetic Ripple Trapping

While most fast ions thermalize and heat the plasma, some can be lost before transferring their energy. A significant loss channel in real tokamaks arises from the discrete nature of the toroidal field (TF) coils. The finite number of coils creates a periodic variation, or **ripple**, in the [toroidal magnetic field](@entry_id:756057) strength.

These ripples create small local magnetic wells between the TF coils. A fast ion can become trapped in one of these wells if its pitch angle (the angle between its velocity vector and the magnetic field line) is large enough. The condition for trapping can be derived from the conservation of the particle's kinetic energy $E$ and its magnetic moment $\mu = mv_\perp^2 / (2B)$. A particle at a ripple field minimum $B_{min}$ will be trapped if its perpendicular velocity is large enough to be reflected before it reaches the adjacent field maximum $B_{max}$. This leads to the trapping condition $\sin^2\alpha \ge B_{min}/B_{max}$, where $\alpha$ is the pitch angle at the minimum .

Particles trapped in these ripple wells are no longer on well-confined orbits. Their vertical drifts are no longer compensated, and they tend to drift vertically out of the plasma, striking the vessel wall. The fraction of fast ions susceptible to this loss mechanism depends on the ripple amplitude $\delta = (B_{max}-B_{min})/(B_{max}+B_{min})$ and the pitch-angle distribution of the fast ions. For an isotropic distribution, the fraction of trapped (and thus lost) particles is approximately $\sqrt{2\delta/(1+\delta)}$. Even a modest ripple of $\delta = 1\%$ can lead to the loss of over $14\%$ of the fast ion population under these conditions, highlighting the critical importance of minimizing TF ripple in [tokamak design](@entry_id:1133215) and optimizing NBI injection geometry to avoid creating fast ions in the trapped region of velocity space.