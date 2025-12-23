## Introduction
The [current quench](@entry_id:748116), a rapid and often destructive termination of plasma current, represents one of the most critical challenges for the successful operation of a [tokamak fusion](@entry_id:756037) reactor. Understanding, predicting, and mitigating this phenomenon is paramount for ensuring machine integrity and safety. This article delves into the core physics of the [current quench](@entry_id:748116) through the lens of magnetohydrodynamic (MHD) simulation, addressing the knowledge gap between the fundamental plasma behavior and its real-world engineering consequences. By exploring this topic, you will gain a comprehensive understanding of how a [tokamak disruption](@entry_id:756033) unfolds and how computational models are used to master it.

This article is structured to build your expertise progressively. The first chapter, "Principles and Mechanisms," establishes the theoretical foundation, deriving the resistive MHD model and explaining how a thermal quench triggers catastrophic [magnetic diffusion](@entry_id:187718), [halo currents](@entry_id:750136), and instabilities. Building on this, "Applications and Interdisciplinary Connections" explores the far-reaching impact of the current quench, from the immense structural forces exerted on the tokamak to its role in driving runaway electron generation and the strategies used for [disruption mitigation](@entry_id:748573). Finally, "Hands-On Practices" will allow you to apply these concepts through targeted problems, reinforcing your grasp of the key physical and computational principles.

## Principles and Mechanisms

The [current quench](@entry_id:748116) is a rapid, and often destructive, termination of the [plasma current](@entry_id:182365) that follows the initial loss of thermal energy in a [tokamak disruption](@entry_id:756033). Simulating this phenomenon requires a robust understanding of the underlying magnetohydrodynamic (MHD) principles and the complex interplay of transport, [atomic physics](@entry_id:140823), and [plasma-wall interactions](@entry_id:187149). This chapter elucidates these core principles and mechanisms, building from the governing equations to the practical considerations of numerical modeling.

### The Governing Model: Resistive Magnetohydrodynamics

The appropriate physical model for describing the macroscopic evolution of the plasma during a current quench is **resistive [magnetohydrodynamics](@entry_id:264274) (MHD)**. The choice of this model, a simplification of the more complete [two-fluid plasma](@entry_id:1133541) description, is justified by the characteristic parameters of the quench phase. The full behavior of the plasma is described by the **generalized Ohm's law**:

$$
\mathbf{E} + \mathbf{v} \times \mathbf{B} = \eta \mathbf{J} + \frac{1}{n_e e} (\mathbf{J} \times \mathbf{B}) - \frac{1}{n_e e} \nabla p_e + \frac{m_e}{n_e e^2} \frac{\partial \mathbf{J}}{\partial t}
$$

Here, $\mathbf{E}$ is the electric field, $\mathbf{v}$ is the bulk fluid velocity, $\mathbf{B}$ is the magnetic field, $\eta$ is the [plasma resistivity](@entry_id:196902), $\mathbf{J}$ is the current density, $n_e$ is the electron density, $e$ is the elementary charge, $p_e$ is the electron pressure, and $m_e$ is the electron mass. The terms on the right-hand side represent, respectively, the resistive electric field, the Hall effect, the electron pressure gradient ([thermoelectric effect](@entry_id:161618)), and electron inertia.

During a current quench, the plasma is cold and highly collisional, and the evolution of the global current is relatively slow compared to microscopic timescales. We can therefore assess the importance of the two-fluid terms . The component of Ohm's law parallel to the magnetic field, which governs the dissipation of the large toroidal current, is key. The Hall term, $\frac{1}{n_e e}(\mathbf{J} \times \mathbf{B})$, is perpendicular to $\mathbf{B}$ and thus makes no direct contribution to the parallel electric field, $E_{\parallel}$.

The electron inertia term becomes significant only for very rapid changes in current. We can compare its timescale to the current quench timescale, $\tau_{\text{CQ}} \approx 10 \, \mathrm{ms}$. The condition for neglecting electron inertia is that the quench timescale is much longer than the electron [collision time](@entry_id:261390), $\tau_e \approx m_e/(n_e e^2 \eta)$, and the electron plasma period, $\omega_{pe}^{-1}$. For a typical quench plasma with $n_e \approx 10^{20} \, \mathrm{m}^{-3}$, the electron plasma frequency is $\omega_{pe} \approx 5.6 \times 10^{11} \, \mathrm{rad/s}$, so $\omega_{pe}^{-1} \sim 10^{-12} \, \mathrm{s}$. The electron skin depth is $d_e = \sqrt{m_e/(\mu_0 n_e e^2)} \sim 5.3 \times 10^{-4} \, \mathrm{m}$, which is many orders of magnitude smaller than the device scale $L \sim 0.5 \, \mathrm{m}$. These scale separations, $\tau_{\text{CQ}} \gg \omega_{pe}^{-1}$ and $L \gg d_e$, are robustly satisfied, confirming that electron inertia is negligible for the global current decay .

While the electron pressure gradient term, $\nabla p_e$, does not vanish in a cold plasma, its effect is typically subdominant to the resistive term, which grows to enormous values. Consequently, for studying the global decay of current, the single-fluid resistive MHD model, which retains only the resistive term $\eta \mathbf{J}$, provides a valid and powerful framework.

### The Fundamental Cause: Resistive Magnetic Diffusion

The current quench is fundamentally a process of rapid **[magnetic diffusion](@entry_id:187718)**, triggered by a catastrophic increase in [plasma resistivity](@entry_id:196902). This process can be understood as a direct causal sequence.

#### Thermal Quench and Impurity Radiation

The process begins with a **thermal quench**, a rapid collapse of the plasma's thermal energy and electron temperature, $T_e$, typically occurring on a timescale of $0.1-1 \, \mathrm{ms}$ in a large tokamak . In disruptions mitigated by material injection, this cooling is driven by intense radiation from impurity atoms. The volumetric radiative power can be expressed as $P_{\text{rad}} = n_{e} n_{Z} L_{Z}(T_{e})$, where $n_Z$ is the impurity density and $L_{Z}(T_{e})$ is the **impurity cooling function**.

The shape of $L_Z(T_e)$ is a convolution of two competing effects . First, for an impurity to radiate efficiently via [line emission](@entry_id:161645), it must be in a charge state that possesses bound electrons. The fractional abundance of any given charge state, $f_q(T_e)$, peaks at a specific temperature. Second, the rate of electron-impact excitation, which leads to [line radiation](@entry_id:751334), generally decreases with temperature for electrons far above the excitation energy threshold (scaling roughly as $T_e^{-1/2}$). The combination of these effects results in $L_Z(T_e)$ having a strong peak at a particular temperature where the impurity is most effective at radiating energy. For instance, a model for argon cooling might peak at an electron temperature around $22 \, \mathrm{eV}$ . The goal of a [disruption mitigation](@entry_id:748573) system is to introduce impurities that cause $T_e$ to rapidly drop into this highly radiative range.

#### The Role of Spitzer Resistivity

The critical link between the thermal quench and the current quench is the temperature dependence of [plasma resistivity](@entry_id:196902). For a collisional, fully-ionized plasma, the **Spitzer resistivity** is given by:

$$
\eta \propto Z_{\text{eff}} \ln\Lambda \, T_e^{-3/2}
$$

where $Z_{\text{eff}} = \sum_s n_s Z_s^2 / n_e$ is the effective ion charge (a measure of impurity content), and $\ln\Lambda$ is the weakly-dependent Coulomb logarithm. The dependence on $T_e^{-3/2}$ is extremely strong. During a thermal quench, $T_e$ can plummet from several keV to just a few eV. For example, a drop from $T_{e0} = 5 \, \mathrm{keV}$ to $T_{e1} = 50 \, \mathrm{eV}$ (a factor of 100) increases the resistivity by a factor of $100^{3/2} = 1000$ from temperature alone. If this is accompanied by an increase in impurity content, for instance from $Z_{\text{eff},0} = 1.5$ to $Z_{\text{eff},1} = 6$, the total resistivity increase can be enormous, on the order of $\eta_1/\eta_0 \approx 3500$ .

#### Magnetic Diffusion and Current Decay

The evolution of the magnetic field in resistive MHD is governed by the [magnetic diffusion equation](@entry_id:181381), which can be derived from Faraday's law and Ohm's law:

$$
\frac{\partial \mathbf{B}}{\partial t} = \nabla \times (\mathbf{v} \times \mathbf{B}) - \nabla \times (\eta \mathbf{J})
$$

Neglecting flow and using Ampère's Law, $\mathbf{J} = (\nabla \times \mathbf{B})/\mu_0$, this becomes:

$$
\frac{\partial \mathbf{B}}{\partial t} \approx \frac{\eta}{\mu_0} \nabla^2 \mathbf{B}
$$

This equation shows that magnetic field structures decay on a characteristic **[resistive diffusion time](@entry_id:1130912)**, $\tau_R \sim \mu_0 L^2 / \eta$, where $L$ is the characteristic length scale of the [magnetic field gradient](@entry_id:924531) . A hot, stable tokamak plasma is an excellent conductor with a very low $\eta$ and a correspondingly long $\tau_R$ (hundreds of seconds), which is why it can confine a magnetic configuration for long periods.

During the [thermal quench](@entry_id:755893), the resistivity $\eta$ increases by several orders of magnitude. Consequently, the [resistive time](@entry_id:754275) $\tau_R$ collapses by the same factor. This drastically shortened timescale *is* the **[current quench](@entry_id:748116) timescale**, $\tau_{\text{CQ}}$. The [stored magnetic energy](@entry_id:274401) is no longer well-confined and rapidly dissipates as Ohmic heat, leading to the decay of the plasma current over tens of milliseconds.

### Macroscopic Dynamics and Energetics

The [current quench](@entry_id:748116) can be viewed from a macroscopic perspective, either through energy conservation or a simplified circuit model.

#### Energy Conservation and Ohmic Dissipation

The Poynting theorem provides a rigorous statement of energy conservation for the electromagnetic field. In a volume $V$ bounded by a perfectly conducting wall (where the energy flux is zero), and neglecting [electric field energy](@entry_id:270775) and plasma kinetic energy, the theorem simplifies to :

$$
\frac{d W_B}{dt} = - \int_V \mathbf{J} \cdot \mathbf{E} \, dV
$$

where $W_B = \int_V \frac{B^2}{2\mu_0} dV$ is the total magnetic energy stored in the system. Using the resistive Ohm's law, $\mathbf{E} = \eta\mathbf{J}$, the term on the right becomes the total Ohmic dissipation power, $P_{\text{Ohmic}} = \int_V \eta J^2 dV$. This gives the fundamental energy balance of the [current quench](@entry_id:748116):

$$
P_{\text{Ohmic}}(t) = \int_V \eta J^2 dV = - \frac{d W_B}{dt}
$$

The rate of energy dissipated as heat throughout the plasma volume is precisely equal to the rate of decrease of the [stored magnetic energy](@entry_id:274401). The total magnetic energy associated with the [plasma current](@entry_id:182365) $I_p$ can be written as $W_B = \frac{1}{2}L_p I_p^2$, where $L_p$ is the plasma's total inductance, which includes contributions from the magnetic field both internal and external to the plasma column . If the current decays exponentially, $I(t) = I_0 \exp(-t/\tau_I)$, the instantaneous dissipated power is $P_{\text{Ohmic}}(t) = (L_p I_0^2 / \tau_I) \exp(-2t/\tau_I)$. For a major disruption in a large tokamak with $I_0 = 12 \, \mathrm{MA}$ and $\tau_I = 6 \, \mathrm{ms}$, this can correspond to an [instantaneous power](@entry_id:174754) of over $11 \, \mathrm{GW}$ dissipated into the cold plasma .

#### The Lumped Parameter Model

A simplified, yet insightful, view is the **lumped parameter circuit model**, which treats the plasma as a single-turn coil with inductance $L$ and a time-varying resistance $R(t)$:

$$
L \frac{dI}{dt} + R(t) I(t) = 0
$$

The solution to this equation is $I(t) = I_0 \exp\left[-\frac{1}{L}\int_0^t R(\tau) d\tau\right]$. This model elegantly captures how the evolution of plasma parameters translates to the current decay. For example, in a mitigated disruption, the effectiveness of the impurity injection can be parameterized by an **assimilation fraction**, $f$. A larger $f$ leads to a more rapid temperature drop and a higher effective charge $Z_{\text{eff}}$. Both effects increase the [plasma resistivity](@entry_id:196902) $\eta(t)$ and thus the total resistance $R(t)$, leading to a faster current decay .

### Evolution of Internal Structure and Stability

The [current quench](@entry_id:748116) is not merely a uniform decay of current; it involves a significant evolution of the internal current density profile, which in turn affects MHD stability.

#### Current Profile Broadening and Safety Factor Evolution

The resistive diffusion equation, $\partial_t \psi = (\eta/\mu_0) \Delta^* \psi$, governs the evolution of the [poloidal magnetic flux](@entry_id:1129914), $\psi$. For a typical centrally-peaked current profile, diffusion causes the profile of $\psi$ to flatten. This corresponds to a **broadening of the current [density profile](@entry_id:194142)**, as current effectively diffuses from the core to the edge of the plasma .

This profile evolution directly impacts the **safety factor**, $q(r,t)$, which measures the winding pitch of the magnetic field lines. In a simplified cylindrical geometry, $q(r) \approx r B_\phi / (R_0 B_p(r))$, where $B_p$ is the poloidal field generated by the plasma current. As the current profile broadens and the total current decays, the poloidal field $B_p$ decreases everywhere. Consequently, the safety factor $q(r,t)$ increases across the entire profile. This process tends to flatten the $q$-profile, reducing the **magnetic shear**, $s = (r/q) (dq/dr)$. This evolution can cause the plasma to pass through various MHD instability thresholds during the quench itself.

#### Tearing Modes and Magnetic Reconnection

The high-resistivity environment of a current quench is extremely favorable for the growth of **[tearing modes](@entry_id:194294)**. These are [resistive instabilities](@entry_id:186275) that occur at "rational surfaces" where the magnetic field lines close on themselves after a rational number of toroidal and poloidal transits (i.e., where $q$ is a rational number). Tearing modes cut and reconnect magnetic field lines, forming structures called magnetic islands .

The linear growth rate $\gamma$ of these modes, as derived by Furth, Killeen, and Rosenbluth (FKR), scales with resistivity as:

$$
\gamma \propto \eta^{3/5}
$$

Since $\eta \propto T_e^{-3/2}$, the growth rate scales with temperature as $\gamma \propto T_e^{-9/10}$. A temperature drop from $5 \, \mathrm{keV}$ to $5 \, \mathrm{eV}$ (a factor of 1000) can increase the tearing mode growth rate by a factor of $1000^{9/10} \approx 500$ . The rapid growth of multiple [tearing modes](@entry_id:194294) can lead to an overlap of magnetic islands, resulting in widespread **stochasticity** of the magnetic field. This chaotic field structure destroys confinement and can dramatically accelerate the transport of heat and current, further hastening the quench.

### Plasma-Wall Interaction: Halo Currents

When a disruption involves a loss of position control, such as in a **Vertical Displacement Event (VDE)**, the plasma comes into contact with the conducting vacuum vessel wall. This introduces a critical new phenomenon: **[halo currents](@entry_id:750136)**.

As the hot plasma edge touches the wall, magnetic field lines that were previously closed are "scraped off" and become **open field lines**, intersecting the material boundary at two points. The strong toroidal electric field induced during the quench drives a current parallel to these open field lines. This current flows out of the plasma, through the conducting vessel structure, and re-enters the plasma elsewhere. This [current loop](@entry_id:271292), partly in the plasma and partly in the wall, is the halo current .

Halo currents are distinct from both the bulk [plasma current](@entry_id:182365) (which flows on closed surfaces) and eddy currents (which are induced entirely within the vessel). They are a direct consequence of the plasma becoming a part of the electrical circuit of the machine. The interaction of these large [halo currents](@entry_id:750136) with the strong background magnetic field produces immense $\mathbf{J} \times \mathbf{B}$ forces that can cause severe mechanical stress and damage to in-vessel components.

### Principles of Numerical Simulation

Simulating the [current quench](@entry_id:748116) requires numerical methods capable of handling the extreme conditions and multiple timescales involved.

#### Numerical Stiffness and Implicit Methods

The [magnetic diffusion equation](@entry_id:181381), $\partial_t \mathbf{B} = (\eta/\mu_0) \nabla^2 \mathbf{B}$, becomes **numerically stiff** during a current quench . Stiffness arises because the characteristic diffusion time, $\tau_R \sim \mu_0 L^2/\eta$, becomes extremely short as resistivity $\eta$ skyrockets. When using an **explicit time-stepping method** (e.g., forward Euler), the [numerical stability condition](@entry_id:142239) requires the time step $\Delta t$ to be smaller than this fastest physical timescale, typically $\Delta t \lesssim (\Delta x)^2 / (\eta/\mu_0)$, where $\Delta x$ is the grid spacing. As $\eta$ increases by orders of magnitude, the required $\Delta t$ becomes prohibitively small, rendering the simulation computationally intractable.

To overcome this, [current quench](@entry_id:748116) simulations must employ **implicit time-stepping methods** (e.g., backward Euler). Implicit schemes are generally [unconditionally stable](@entry_id:146281) for diffusion problems. This means the time step $\Delta t$ is limited only by considerations of accuracy, not stability, and can be orders of magnitude larger than what an explicit scheme would allow. For example, the amplification factor for the least-damped mode in a backward Euler scheme for cylindrical diffusion is $g = (1 + \Delta t \, \eta \, j_{0,1}^2 / (\mu_0 a^2))^{-1}$, where $j_{0,1}$ is the first zero of the Bessel function $J_0$. Since $|g|  1$ for any $\Delta t > 0$, the method is unconditionally stable, making it essential for efficiently modeling the resistive evolution .

#### Boundary Conditions

Accurate simulation also depends critically on the implementation of appropriate boundary conditions. This is particularly true for capturing [halo currents](@entry_id:750136). A simulation that imposes an "insulating wall" boundary condition, $\mathbf{J} \cdot \hat{\mathbf{n}} = 0$ (where $\hat{\mathbf{n}}$ is the normal to the wall), artificially prevents any current from flowing between the plasma and the wall. Such a model would completely suppress [halo currents](@entry_id:750136) by fiat. Realistic simulations must therefore implement conductive-wall or sheath boundary conditions that permit a non-zero normal current, $\mathbf{J} \cdot \hat{\mathbf{n}} \neq 0$, enabling the closure of the halo current circuit through the vessel .