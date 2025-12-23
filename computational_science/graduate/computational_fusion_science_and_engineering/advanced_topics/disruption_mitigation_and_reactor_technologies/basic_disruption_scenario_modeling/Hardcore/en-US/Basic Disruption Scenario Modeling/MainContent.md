## Introduction
Tokamak disruptions represent one of the most significant challenges to achieving commercially viable fusion energy. These catastrophic events involve a rapid loss of plasma confinement, capable of inflicting severe damage on reactor components and jeopardizing operational safety. To design robust future power plants, it is imperative to develop predictive models that can anticipate and mitigate these events. This article provides a foundational framework for understanding and modeling basic disruption scenarios. In the following chapters, you will explore the core physics governing these events, from their initial triggers to their final consequences. "Principles and Mechanisms" will deconstruct the disruption into its fundamental phases, detailing the magnetohydrodynamic instabilities and transport processes at play. "Applications and Interdisciplinary Connections" will bridge theory and practice, showing how these models inform experimental validation, engineering design of control and mitigation systems, and [structural analysis](@entry_id:153861). Finally, "Hands-On Practices" will allow you to apply these concepts to solve concrete problems in disruption analysis, solidifying your understanding of this critical field in fusion science.

## Principles and Mechanisms

### The Anatomy of a Disruption: A Phased Evolution

A [tokamak disruption](@entry_id:756033) represents a catastrophic failure of magnetic confinement, leading to the rapid loss of the plasma's thermal energy and the termination of the [plasma current](@entry_id:182365). This complex event is not monolithic but evolves through a sequence of distinct phases, each governed by different physical mechanisms and timescales. Understanding this sequence is fundamental to modeling disruptions and mitigating their severe consequences on the surrounding machine components.

The canonical disruption scenario can be deconstructed into the following key phases :

1.  **Precursor/Trigger:** The disruption is initiated by the growth of one or more magnetohydrodynamic (MHD) instabilities. These instabilities, which will be discussed in detail later, corrupt the nested magnetic surfaces that are essential for confinement.

2.  **Thermal Quench (TQ):** This is the first and fastest phase of the disruption, characterized by a precipitous collapse of the plasma's thermal energy, $W_p$. As the confining magnetic structure is destroyed by the precursor instability, heat from the hot plasma core is rapidly transported to the cold vessel walls. In a large tokamak, this phase can release hundreds of megajoules of energy in a timescale typically under a millisecond ($ 1\,\mathrm{ms}$). The [plasma temperature](@entry_id:184751) plummets from many kiloelectronvolts (keV) to just a few electronvolts (eV).

3.  **Current Quench (CQ):** Following the [thermal quench](@entry_id:755893), the now cold and impure plasma becomes extremely resistive. According to Ohm's law, this dramatic increase in resistivity leads to a rapid decay of the toroidal plasma current, $I_p$. This phase, known as the current quench, occurs on a timescale of several to tens of milliseconds ($5$–$50\,\mathrm{ms}$), significantly slower than the [thermal quench](@entry_id:755893). The rapid change in magnetic flux associated with the current decay induces immense electromagnetic forces on the surrounding vacuum vessel and other structures.

4.  **Final Termination:** The [plasma current](@entry_id:182365) fully decays, and the discharge is terminated.

During this sequence, two other [critical phenomena](@entry_id:144727) can occur:

*   **Runaway Electron (RE) Generation:** During the rapid [current quench](@entry_id:748116), the large change in magnetic flux induces a strong toroidal electric field. This field can accelerate a portion of the electron population to relativistic energies, creating a beam of so-called **[runaway electrons](@entry_id:203887)**. These RE beams can persist after the thermal plasma has dissipated and can cause highly localized damage to [plasma-facing components](@entry_id:1129762). RE generation and avalanche typically occur on millisecond timescales during the current quench.

*   **Vertical Displacement Event (VDE):** Modern tokamaks utilize vertically elongated plasma shapes to improve performance. This shaping, however, makes the plasma inherently unstable to vertical motion. While this instability is managed by [feedback control systems](@entry_id:274717) during normal operation, the rapid changes in pressure and current profiles during a disruption can lead to a loss of control. The plasma then drifts vertically and collides with the top or bottom of the vessel. The timescale for this motion is governed by the resistive decay of stabilizing eddy currents in the conducting structures, known as the **[resistive wall time](@entry_id:754278)**, $\tau_w$, which is typically on the order of tens to hundreds of milliseconds. A VDE can either be a trigger for a disruption or a consequence of one.

The typical causal sequence is therefore: an MHD instability triggers a **[thermal quench](@entry_id:755893)**, which in turn causes the **current quench**. Runaway electron generation may occur during the current quench, and a [vertical displacement event](@entry_id:1133790) may develop concurrently with or following the loss of [plasma control](@entry_id:753487).

### Precursors and Instability Triggers

Disruptions are the result of the plasma state crossing a stability boundary. While many complex chains of events can lead to a disruption, the triggers can often be categorized into instabilities that violate limits on the plasma pressure, current profile, or density.

#### Resistive Instabilities: The Neoclassical Tearing Mode

In high-performance tokamak plasmas, a common and insidious trigger for disruptions is the **Neoclassical Tearing Mode (NTM)**. Classical [tearing modes](@entry_id:194294) are [resistive instabilities](@entry_id:186275) that grow at **rational surfaces**, where the magnetic field line safety factor $q(r)$ equals a rational number $m/n$. They are driven by gradients in the equilibrium current density and are stable if the classical stability index, $\Delta'$, is negative.

However, in the hot, low-collisionality plasmas of modern tokamaks, neoclassical effects become important. Specifically, the pressure gradient drives a parallel current known as the **bootstrap current**, $j_{\mathrm{bs}}$, which is not sustained by an external electric field. For a standard plasma with a negative pressure gradient ($dp/dr  0$) and positive poloidal magnetic field, the bootstrap current flows in the same direction as the main plasma current (a co-current). A simplified scaling for this current is :

$j_{\mathrm{bs}} \propto - \frac{1}{B_\theta} \frac{dp}{dr}$

An NTM is a nonlinearly unstable mode. It requires a "seed" magnetic island, perhaps created by another small-scale instability like a sawtooth oscillation. Within this [magnetic island](@entry_id:1127585), the helical magnetic field lines connect regions of different pressure. The extremely rapid heat and [particle transport](@entry_id:1129401) along these field lines tends to flatten the pressure profile across the island. This pressure flattening, $(dp/dr)_{\mathrm{island}} \approx 0$, eliminates the local drive for the bootstrap current.

This creates a localized "hole" or deficit in the co-flowing bootstrap current. This helical current deficit has the correct phase to reinforce the magnetic perturbation that created the island. This provides a positive, destabilizing feedback loop. This neoclassical drive term can cause the seed island to grow even if the plasma is classically stable (i.e., $\Delta'  0$). As the NTM island grows, it can degrade confinement, alter the global current profile, and ultimately trigger a major disruption .

#### Ideal MHD Instabilities: The Pressure Limit

The amount of pressure a given magnetic field configuration can confine is fundamentally limited. Exceeding this limit triggers fast-growing **ideal MHD instabilities** that can lead to a disruption on the plasma's fastest timescale, the Alfvén time (microseconds). The key parameter for quantifying this limit is the **plasma beta**, $\beta$, which is the ratio of plasma pressure to magnetic pressure:

$\beta = \frac{\overline{p}}{B_T^2 / (2\mu_0)}$

Extensive experimental and theoretical studies, pioneered by Francis Troyon, found that the maximum achievable $\beta$ scales with the [plasma current](@entry_id:182365) normalized by the machine size and toroidal field, $I_p / (a B_T)$. This led to the definition of the **[normalized beta](@entry_id:1128891)**, $\beta_N$:

$\beta_N \equiv \frac{\beta [\%] a[\mathrm{m}] B_T[\mathrm{T}]}{I_p[\mathrm{MA}]}$

For typical plasma shapes, there exists a critical value of $\beta_N$ beyond which the plasma becomes unstable to ideal MHD modes like the external kink or ballooning modes. This is the **Troyon limit**. In the absence of a nearby conducting wall to stabilize the mode (a "no-wall" condition), this limit is empirically and theoretically found to be around $\beta_N \approx 3$ .

For example, consider a large tokamak with $B_T = 5.0\,\mathrm{T}$, $a = 1.0\,\mathrm{m}$, and $I_p = 8.0\,\mathrm{MA}$. If the plasma achieves an average pressure of $\overline{p} = 0.55\,\mathrm{MPa}$, the corresponding plasma beta is $\beta \approx 0.055$, or $5.5\%$. The [normalized beta](@entry_id:1128891) would be:

$\beta_N = \frac{5.5 \times 1.0 \times 5.0}{8.0} \approx 3.44$

This value exceeds the typical no-wall limit of $\beta_N \approx 3$, indicating that the plasma is likely unstable to a pressure-driven ideal MHD mode. Such an instability would grow very rapidly and almost certainly precipitate a major disruption .

#### Operational Boundaries: The Density Limit

Another critical boundary for tokamak operation is the density limit. As the plasma density is increased, a point is reached where radiation losses from the cooler plasma edge become so large that they trigger a thermal collapse, leading to a disruption. Based on data from many different machines, Martin Greenwald found a remarkably simple and robust empirical scaling for the line-averaged density limit, now known as the **Greenwald density limit**, $n_G$ :

$n_G [10^{20}\,\mathrm{m}^{-3}] = \frac{I_p[\mathrm{MA}]}{\pi a^2[\mathrm{m}^2]}$

The quantity on the right is the average plasma current density. Operation is often characterized by the **Greenwald fraction**, $f_G = \bar{n}_e / n_G$.

It is crucial to recognize that the Greenwald limit is an *empirical* observation, not a hard stability boundary derived from first-principles theory like the Troyon limit. As such, exceeding $f_G=1$ does not deterministically cause a disruption, and many advanced scenarios have demonstrated sustained operation at $f_G  1$. However, it serves as an extremely useful guideline in operational planning and as a key feature in statistical [disruption prediction](@entry_id:748575) models. As a plasma's density approaches and exceeds the Greenwald limit, the risk of a radiative-collapse disruption increases dramatically .

### The Thermal Quench: Rapid Energy Loss

The thermal quench is the first catastrophic phase of the disruption proper. It is defined by the rapid collapse of [plasma temperature](@entry_id:184751) and stored thermal energy on a sub-millisecond timescale. This process is driven by the sudden failure of [thermal insulation](@entry_id:147689) caused by the precursor MHD instability.

#### Macroscopic Energy Balance

From a macroscopic viewpoint, the evolution of the total plasma thermal energy, $W_p$, can be described by a zero-dimensional (0D) [energy balance equation](@entry_id:191484) :

$\frac{dW_p}{dt} = P_{\mathrm{heat}} - P_{\mathrm{rad}} - P_{\mathrm{cond}}$

Here, $P_{\mathrm{heat}}$ represents all heating sources (ohmic, auxiliary, and [alpha heating](@entry_id:193741) in a burning plasma). The two loss terms are key to the [thermal quench](@entry_id:755893):
- $P_{\mathrm{rad}}$ is the power lost through radiation, primarily bremsstrahlung and [line radiation](@entry_id:751334) from impurities.
- $P_{\mathrm{cond}}$ is the power lost through conductive and [convective transport](@entry_id:149512) of particles and energy to the vessel wall.

During the [thermal quench](@entry_id:755893), both $P_{\mathrm{rad}}$ and $P_{\mathrm{cond}}$ increase by orders of magnitude, overwhelming the heating terms and causing a rapid decrease in $W_p$. The conductive loss can be modeled phenomenologically as $P_{\mathrm{cond}} = W_p/\tau_{\mathrm{cond}}$, where $\tau_{\mathrm{cond}}$ is an effective [energy confinement time](@entry_id:161117) that becomes extremely short during the quench . The physical origin of this dramatic drop in $\tau_{\mathrm{cond}}$ lies in the change of the magnetic field topology.

#### The Underlying Mechanism: Magnetic Stochasticity and Parallel Transport

In a well-confined plasma, heat transport is a story of extreme anisotropy. Transport *along* magnetic field lines is extremely fast, while transport *across* them is comparatively slow. The effectiveness of a tokamak relies on its nested magnetic surfaces, which act as barriers to prevent hot core particles from ever reaching the wall by following a field line.

The precursor MHD instability destroys these nested surfaces, creating a region of chaotic or **stochastic** magnetic field lines. In this region, a single field line wanders erratically, eventually connecting the hot core to the cold material boundary. This opens up a "short circuit" for heat loss via the highly efficient [parallel transport](@entry_id:160671) channel .

The physics of parallel electron heat conduction in a collisional plasma was described by Spitzer and Härm. The parallel heat conductivity, $\kappa_\parallel$, has a very strong dependence on the electron temperature:

$\kappa_\parallel \propto \frac{T_e^{5/2}}{Z_{\mathrm{eff}}}$

where $Z_{\mathrm{eff}}$ is the effective ionic charge. This strong temperature dependence means that parallel [heat transport](@entry_id:199637) is exceptionally rapid in a hot plasma. Once the field lines become stochastic, the thermal quench timescale, $\tau_T$, is governed by the time it takes for heat to conduct along the newly formed connection length $L_\parallel$ to the wall. This timescale can be estimated as:

$\tau_T \sim \frac{n_e L_\parallel^2}{\kappa_\parallel} \propto \frac{n_e L_\parallel^2 Z_{\mathrm{eff}}}{T_e^{5/2}}$

This scaling demonstrates why the [thermal quench](@entry_id:755893) is so rapid: the very high initial temperature $T_e$ leads to an enormous $\kappa_\parallel$ and a very short quench time $\tau_T$. This constitutes a positive feedback loop: as the plasma cools, the parallel transport becomes less effective, but by then the bulk of the energy has already been lost. The validity of this collisional model relies on the [electron mean free path](@entry_id:185806) being much shorter than the connection length, a condition that is often met, especially as impurity influx during the disruption increases [plasma collisionality](@entry_id:753486) .

### The Current Quench: Resistive Decay and Inductive Response

The thermal quench leaves behind a cold, dense, and impure plasma. According to Spitzer's formula for resistivity, $\eta \propto Z_{\mathrm{eff}} T_e^{-3/2}$, the plasma's electrical resistivity increases by several orders of magnitude. This sets the stage for the [current quench](@entry_id:748116).

The plasma can be modeled, to a first approximation, as a simple RL circuit, where the [toroidal plasma](@entry_id:202484) loop has an inductance $L_p$ and a resistance $R_p$. The governing equation for the plasma current $I_p$, assuming negligible externally applied voltage, is Faraday's law applied to the loop :

$L_p \frac{dI_p}{dt} + R_p I_p = 0$

This is the equation for the free decay of current in an RL circuit. The solution is a simple exponential decay:

$I_p(t) = I_{p0} \exp(-t/\tau_{CQ})$

where $I_{p0}$ is the current at the beginning of the quench and $\tau_{CQ}$ is the characteristic **[current quench](@entry_id:748116) timescale**, defined as:

$\tau_{CQ} = \frac{L_p}{R_p}$

Using typical parameters for a large tokamak after a [thermal quench](@entry_id:755893) ($L_p \approx 4.5\,\mu\mathrm{H}$, post-TQ resistance $R_p \approx 6.0\times 10^{-4}\,\Omega$), the [current quench](@entry_id:748116) timescale would be on the order of $\tau_{CQ} \approx 7.5\,\mathrm{ms}$. For a plasma with an initial current of $10\,\mathrm{MA}$, this implies an initial decay rate $|dI_p/dt| \approx 1.3\,\mathrm{GA/s}$, illustrating the immense speed of the current decay .

In reality, the plasma resistance and inductance can evolve during the quench, leading to a non-exponential decay. A more general characterization is the instantaneous decay time, $\tau_{\mathrm{eff}}(t) = -I_p / (dI_p/dt)$. Furthermore, coupling to eddy currents in the vessel increases the effective inductance, which tends to slow the initial current decay .

### Critical Consequences and Associated Modeling Challenges

The violent dynamics of the thermal and current quenches lead to severe consequences for the tokamak device, presenting significant modeling challenges.

#### Runaway Electron Generation

The rapid decay of plasma current during the CQ induces a large toroidal electric field, $E_\parallel \propto -dI_p/dt$. This electric field can accelerate electrons to relativistic energies if it overcomes the frictional drag from collisions. An electron "runs away" if the electric field exceeds a **[critical field](@entry_id:143575)**, $E_c$, which is proportional to the plasma density and inversely related to temperature in some regimes.

Two primary mechanisms are responsible for creating an initial "seed" population of [runaway electrons](@entry_id:203887) :

1.  **Dreicer Mechanism:** In any plasma, there is a small population of electrons in the high-energy tail of the Maxwellian distribution that can be accelerated by an electric field. The rate of this process is extremely sensitive to the ratio $E_\parallel/E_D$, where $E_D$ is the Dreicer field, which represents the drag on thermal electrons. As the plasma cools during the [thermal quench](@entry_id:755893), $E_D$ decreases and the induced $E_\parallel$ increases, causing the ratio $E_\parallel/E_D$ to grow significantly and making Dreicer generation more likely.

2.  **Hot-Tail Mechanism:** If the thermal quench is extremely fast—faster than the collisional slowing-down time of energetic electrons—a fraction of the electrons from the hot, pre-quench plasma tail will not have time to thermalize with the cold bulk. These "leftover" energetic electrons find themselves far above the [thermal velocity](@entry_id:755900) of the cold plasma and are easily accelerated by the [induced electric field](@entry_id:267314). This mechanism is most effective for rapid quenches and high pre-quench temperatures and is suppressed by high density, which increases collisionality .

Once a seed population is formed, these relativistic electrons can knock out further runaways from the thermal population via close-range collisions, leading to an exponential or "avalanche" growth of the RE population.

#### Electromagnetic Loads and Vessel Current Modeling

The time-varying magnetic fields during a disruption, particularly the rapid decay of $I_p$ and any motion of the plasma column (VDE), induce powerful [eddy currents](@entry_id:275449) in the surrounding conducting structures, most notably the vacuum vessel. The interaction of these [eddy currents](@entry_id:275449) with the strong background magnetic field generates immense $\mathbf{J} \times \mathbf{B}$ forces that can stress the vessel structure to its mechanical limits.

Modeling these currents is a critical task in [fusion engineering](@entry_id:1125401). The behavior of the induced currents is governed by the [magnetic diffusion equation](@entry_id:181381). A key parameter that determines the appropriate modeling approach is the **[skin depth](@entry_id:270307)**, $\delta$, which describes how far an alternating magnetic field can penetrate into a conductor :

$\delta = \sqrt{\frac{2}{\omega \mu \sigma}}$

where $\omega \sim 1/\tau_q$ is the characteristic frequency of the [current quench](@entry_id:748116), and $\mu$ and $\sigma$ are the permeability and conductivity of the vessel material.

The choice of model depends on the comparison between the skin depth $\delta$ and the vessel wall thickness $t$:
-   **Slow Quench ($\delta \gtrsim t$):** For slower events, the magnetic field fully penetrates the wall. The induced current is distributed uniformly through the wall's thickness. In this "thin shell" regime, simplified **lumped-parameter models** (e.g., treating the vessel as one or a few R-L circuits) can accurately capture the global evolution of the total vessel current and the net forces. These models are computationally very fast (tractable).
-   **Fast Quench ($\delta \lesssim t$):** For faster events, the magnetic field is shielded from the interior of the wall material. The [induced current](@entry_id:270047) is confined to a thin "skin" on the plasma-facing surface. This violates the assumption of uniform current, and lumped-parameter models become inaccurate. For accurate prediction of current distribution and local stress concentrations, especially around non-axisymmetric features like ports, full **3D electromagnetic simulations** using methods like the Finite Element Method (FEM) are required. These models are far more computationally expensive but provide much higher fidelity .

### A Systems View: The 0D Disruption Model

To capture the coupled dynamics of a disruption in a computationally efficient manner, physicists often employ zero-dimensional (0D) models. These models treat the plasma as a single point in space and evolve a set of volume-averaged quantities over time. Despite their simplicity, they are powerful tools for understanding the interplay between different physical processes.

To create a self-consistent 0D model of a thermal and [current quench](@entry_id:748116), a minimal set of **[state variables](@entry_id:138790)** must be chosen. This state vector must contain enough information to calculate all the key physical processes—heating, radiation, resistivity, and transport—that govern the disruption. A necessary and sufficient set of [state variables](@entry_id:138790) includes :

-   $W_p$: The total plasma thermal energy. Its evolution is governed by the energy balance equation.
-   $I_p$: The total [plasma current](@entry_id:182365). Its evolution is governed by the circuit equation.
-   $n_e$: The electron density. Its evolution is governed by particle sources (e.g., wall material influx) and losses.
-   $Z_{\mathrm{eff}}$: The effective ionic charge, representing the impurity content of the plasma. Its evolution is also determined by material influx from the walls.

From this state vector, other critical quantities can be derived algebraically. For example, the electron temperature $T_e$ can be found from $W_p$, $n_e$, and $Z_{\mathrm{eff}}$. The plasma resistance $R_p$ and radiated power $P_{\mathrm{rad}}$ depend sensitively on $T_e$, $n_e$, and $Z_{\mathrm{eff}}$, creating the [critical coupling](@entry_id:268248) between the thermal and electrical evolution of the plasma. The edge safety factor, $q(a)$, a key parameter for stability, is a function of $I_p$ and the machine geometry. Evolving this minimal set of variables according to the physical principles outlined in this chapter allows for the construction of a basic but insightful model of the entire disruption scenario .