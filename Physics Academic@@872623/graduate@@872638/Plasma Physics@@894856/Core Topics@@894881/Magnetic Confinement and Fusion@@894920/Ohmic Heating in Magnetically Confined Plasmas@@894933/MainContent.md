## Introduction
Ohmic heating, or Joule heating, represents the most fundamental method for increasing the temperature of a [magnetically confined plasma](@entry_id:202728). By driving an electrical current through the plasma, which acts as a resistor, thermal energy is dissipated, heating the constituent particles. This process is not only a source of power but is also intrinsically linked to the creation of the [poloidal magnetic field](@entry_id:753563) essential for confinement in devices like [tokamaks](@entry_id:182005). However, this conceptual simplicity belies a rich and complex reality where heating efficiency, [plasma stability](@entry_id:197168), and energy transport are deeply intertwined. The primary challenge addressed is the diminishing effectiveness and potential instability of Ohmic heating as plasmas approach the extreme temperatures required for nuclear fusion.

This article provides a graduate-level exploration of this critical topic, navigating from foundational principles to advanced applications. In **Principles and Mechanisms**, we will deconstruct the physics of [plasma resistivity](@entry_id:196902), starting with the classical Spitzer model and extending to the crucial neoclassical and [relativistic corrections](@entry_id:153041) that arise in modern fusion devices. We will analyze the dynamics of power balance and the consequences of [resistivity](@entry_id:266481) for current profile shaping and [thermal stability](@entry_id:157474). Following this, **Applications and Interdisciplinary Connections** will broaden the perspective, examining how the Ohmic current shapes [magnetic topology](@entry_id:751637), drives MHD instabilities, and interacts with other energy channels and heating methods in the complex ecosystem of a fusion plasma. Finally, **Hands-On Practices** will provide a series of targeted problems to reinforce the theoretical concepts and build practical problem-solving skills in the context of Ohmic heating.

## Principles and Mechanisms

Ohmic heating, also known as Joule heating, is the most fundamental mechanism for heating a [magnetically confined plasma](@entry_id:202728). It leverages the plasma's inherent [electrical resistivity](@entry_id:143840). In a [tokamak](@entry_id:160432), a time-varying current in a [central solenoid](@entry_id:747208) induces a toroidal electromotive force, or loop voltage, which drives a large [toroidal plasma](@entry_id:202484) current. This current serves a dual purpose: it generates the [poloidal magnetic field](@entry_id:753563) necessary for stable confinement and simultaneously heats the plasma through resistive dissipation. While conceptually simple, the physics of Ohmic heating in a high-temperature, magnetized plasma is rich and complex, involving the interplay of collisional physics, [magnetic topology](@entry_id:751637), and [energy transport](@entry_id:183081). This chapter elucidates the core principles and mechanisms governing this process.

### The Physics of Plasma Resistivity

The origin of Ohmic heating is the [electrical resistivity](@entry_id:143840) of the plasma, which impedes the free acceleration of electrons by the applied electric field. In a [fully ionized plasma](@entry_id:200884), this friction arises from Coulomb collisions between electrons and ions.

#### Spitzer Resistivity

The foundational model for [plasma resistivity](@entry_id:196902) was developed by Lyman Spitzer. The **Spitzer [resistivity](@entry_id:266481)**, $\eta$, for current flowing parallel to the magnetic field is given by:

$$ \eta_{\parallel} \approx C_S \frac{Z_{eff} \ln\Lambda}{T_e^{3/2}} $$

where $T_e$ is the [electron temperature](@entry_id:180280), $\ln\Lambda$ is the Coulomb logarithm (a slowly varying term accounting for the long-range nature of Coulomb interactions), and $Z_{eff}$ is the **effective ion charge**. The constant $C_S$ comprises [fundamental physical constants](@entry_id:272808). This formula reveals two critical dependencies.

First is the strong inverse dependence on [electron temperature](@entry_id:180280), $\eta \propto T_e^{-3/2}$. This arises because the Coulomb [collision cross-section](@entry_id:141552) is a strong function of particle energy. As electrons become hotter and move faster, they spend less time in the vicinity of any given ion, and the cumulative effect of [small-angle scattering](@entry_id:754965) is reduced. Consequently, the plasma becomes a better conductor as it heats up. This scaling is a double-edged sword: while Ohmic heating is efficient at low temperatures, its efficacy dramatically decreases as the plasma approaches fusion-relevant temperatures, a challenge we will explore later.

Second is the dependence on the effective ion charge, **$Z_{eff}$**. This quantity is a measure of the average charge state of ions in the plasma, weighted by their density. It is defined as:

$$ Z_{eff} = \frac{\sum_j n_j Z_j^2}{n_e} $$

where the sum is over all ion species $j$ with density $n_j$ and charge number $Z_j$, and $n_e = \sum_j n_j Z_j$ is the total electron density ensuring [quasi-neutrality](@entry_id:197419). For a pure hydrogenic plasma (Deuterium or Tritium), $Z_{eff} = 1$. However, real plasmas are inevitably contaminated with impurities eroded from the vessel walls (e.g., carbon, beryllium, tungsten). These impurities, having a higher charge number $Z_j > 1$, are much more effective at scattering electrons. As a result, the presence of impurities increases $Z_{eff}$ and, consequently, the [plasma resistivity](@entry_id:196902).

For a given plasma current $I_p$, the total Ohmic heating power is $P_{OH} = R_p I_p^2$, where $R_p$ is the total plasma resistance. Since $R_p$ is proportional to the [resistivity](@entry_id:266481) $\eta$, impurities increase the Ohmic heating power for a fixed current. However, they also enhance power losses through radiation, and their impact is a complex optimization problem. The effect of impurities is not uniform; if impurity density profiles differ from electron density or temperature profiles, the local [resistivity](@entry_id:266481) and power deposition can be significantly altered. For instance, in a hypothetical scenario where an impure plasma must maintain the same current and temperature profiles as a pure one, it must have a higher total Ohmic [power dissipation](@entry_id:264815), which is achieved through an elevated $Z_{eff}$ profile [@problem_id:293600].

#### Anisotropy in a Magnetized Plasma

The presence of a strong magnetic field introduces anisotropy into the plasma's [transport properties](@entry_id:203130), including its [resistivity](@entry_id:266481). Electron motion is largely confined to follow magnetic field lines. As a result, the resistivity for current flowing parallel to the magnetic field, $\eta_{\parallel}$, is different from that for current flowing perpendicular to it, $\eta_{\perp}$.

The parallel [resistivity](@entry_id:266481), $\eta_{\parallel}$, is governed by the Spitzer formula described above. In this case, collisions impede the flow of electrons along the field lines. A more detailed kinetic treatment, accounting for momentum conservation in electron-electron collisions, reveals that the classical Spitzer value is reduced by a factor of approximately 0.51 for $Z=1$.

The perpendicular resistivity, $\eta_{\perp}$, describes the resistance to current flowing across magnetic field lines. In a simple model, this is also determined by electron-ion collisions. However, the Lorentz force, which causes electrons to gyrate around field lines, fundamentally alters the dynamics. A [phenomenological model](@entry_id:273816) of the resistive electric field can illuminate this distinction. Consider a model where the resistive field $\mathbf{E}_{res} = \bar{\bar{\eta}} \cdot \mathbf{J}$ is given by [@problem_id:293769]:

$$ \mathbf{E}_{res} = \eta_0 \left[ \mathbf{J} + \delta (\hat{\mathbf{b}} \times \mathbf{J}) - \alpha_c (\mathbf{J} \cdot \hat{\mathbf{b}})\hat{\mathbf{b}} \right] $$

Here, $\hat{\mathbf{b}}$ is the unit vector along the magnetic field $\mathbf{B}$, and $\alpha_c$ is a factor accounting for the reduction in parallel friction due to electron-electron collisions. Projecting this equation parallel and perpendicular to $\mathbf{B}$ reveals that $\eta_{\parallel} = \eta_0(1-\alpha_c)$ while $\eta_{\perp} = \eta_0$. This leads to a ratio $\eta_{\perp} / \eta_{\parallel} = (1-\alpha_c)^{-1}$. Detailed kinetic theory (e.g., by Braginskii) shows this ratio is approximately 1.96 for $Z=1$, confirming that it is significantly harder to drive current across field lines than along them.

### Ohmic Power Balance and Dynamics

The temperature of an Ohmically heated plasma is determined by the balance between the Ohmic power input and various power loss channels, such as radiation and particle transport.

#### Steady-State Equilibrium

In the simplest, zero-dimensional (0D) model, we can write a power balance equation for the plasma's thermal energy content, $W$:

$$ \frac{dW}{dt} = P_{Ohm} - P_{loss} $$

where all quantities are volume-averaged. In steady-state ($dW/dt = 0$), heating must balance losses. The scaling of these terms with temperature determines the [equilibrium state](@entry_id:270364). As a basic example, consider a plasma where Ohmic heating is balanced solely by [collisional energy transfer](@entry_id:196267) to a cold ion population, whose temperature $T_i$ is fixed [@problem_id:293784]. The Ohmic [power density](@entry_id:194407), for a constant applied electric field $E$, scales as $P_{Ohm} = E^2/\eta \propto E^2 T_e^{3/2}$. The collisional power transfer to ions scales as $P_{ei} \propto (T_e - T_i) / T_e^{3/2}$. In the physically relevant limit where electrons are much hotter than ions ($T_e \gg T_i$), this loss term simplifies to $P_{loss} \approx P_{ei} \propto T_e^{-1/2}$.

Equating the heating and loss rates ($P_{Ohm} = P_{loss}$) gives a unique, stable equilibrium temperature:

$$ T_e \propto E^{-1} $$

This simple case illustrates a key feature: equilibrium is achieved when the heating, which increases with temperature, intersects the power loss curve.

#### Inductive and Resistive Loop Voltage

During the critical start-up phase of a [tokamak](@entry_id:160432) discharge, the [plasma current](@entry_id:182365) $I_p$ is ramped up from zero. The total loop voltage $V_{loop}$ applied by the [central solenoid](@entry_id:747208) must do two things: it must overcome the plasma's resistance and it must build up the magnetic field associated with the plasma current. This leads to two components:

$$ V_{loop}(t) = V_{res}(t) + V_{ind}(t) = R_p(t) I_p(t) + L_p \frac{dI_p(t)}{dt} $$

where $R_p$ is the plasma resistance and $L_p$ is the plasma [inductance](@entry_id:276031) (assumed constant for simplicity). Early in the ramp-up, when $dI_p/dt$ is large and the plasma is still cold (high $R_p$), both components are significant. As the discharge evolves, their relative importance changes. In a scenario with a linear current ramp, the inductive voltage $V_{ind}$ is constant. Meanwhile, as the current rises, the Ohmic power increases, raising the temperature. This, in turn, lowers the resistance ($R_p \propto T_e^{-3/2}$). The complex interplay between current, temperature, and power balance determines the evolution of the resistive voltage. A detailed analysis shows how the ratio $V_{res}/V_{ind}$ at the end of the ramp depends on plasma [transport properties](@entry_id:203130) and operational parameters, providing a diagnostic for the plasma state [@problem_id:293636].

### Current Profiles, Stability, and Limitations

The strong temperature dependence of Spitzer [resistivity](@entry_id:266481) has profound consequences for the [spatial distribution](@entry_id:188271) of the plasma current and for the overall [thermal stability](@entry_id:157474) of the discharge.

#### Current Profile Shaping

In a steady-state tokamak discharge, Faraday's law implies that the toroidal electric field, $E_\phi$, is uniform across the plasma cross-section. Ohm's law, $J_\phi(r) = E_\phi / \eta_\parallel(r)$, then dictates that the toroidal [current density](@entry_id:190690) profile $J_\phi(r)$ is inversely proportional to the resistivity profile. Given that $\eta_\parallel \propto T_e(r)^{-3/2}$, we find:

$$ J_\phi(r) \propto T_e(r)^{3/2} $$

Since [plasma temperature](@entry_id:184751) is almost always peaked at the magnetic axis ($r=0$) and decreases toward the edge ($r=a$), the current density will also be peaked on-axis. This natural **current peaking** is a characteristic feature of Ohmic discharges.

This link between temperature and current has a crucial impact on the magnetic equilibrium itself. The current profile determines the [poloidal magnetic field](@entry_id:753563) profile $B_\theta(r)$ via Ampere's Law. This, in turn, sets the radial profile of the **[safety factor](@entry_id:156168)**, $q(r)$, a key parameter for magnetohydrodynamic (MHD) stability:

$$ q(r) = \frac{r B_\phi}{R_0 B_\theta(r)} $$

For example, if the [electron temperature](@entry_id:180280) has a parabolic profile, $T_e(r) = T_0 (1 - r^2/a^2)$, the resulting current profile is $J_\phi(r) \propto (1 - r^2/a^2)^{3/2}$. Integrating this current density to find $B_\theta(r)$ allows for the calculation of the full $q(r)$ profile. Such a calculation reveals that the safety factor on-axis, $q_0$, is significantly lower than the value at the plasma edge, $q_a$. For this specific parabolic temperature profile, the ratio is found to be a constant, $q_a / q_0 = 5/2$ [@problem_id:293801]. This illustrates the intimate connection between the physics of [plasma resistivity](@entry_id:196902) and the MHD stability of the entire confinement configuration.

#### Thermal Instability

The very property that makes Ohmic heating effective at low temperatures, $P_{Ohm} \propto T_e^{3/2}$ (for constant $E$-field, or constant voltage), can also lead to a dangerous **[thermal instability](@entry_id:151762)**. Consider a plasma in equilibrium. If a small positive temperature perturbation $\delta T$ occurs, the Ohmic heating power increases. If this increase in heating is greater than the corresponding increase in power losses, the temperature will rise further, leading to a thermal runaway.

A stability analysis can be performed by examining the derivative of the net power, $P_{net} = P_{Ohm} - P_{loss}$, with respect to temperature. For stability, we require $dP_{net}/dT  0$ at the equilibrium temperature $T_0$. If we model the heating and loss terms as power laws, $P_{Ohm} \propto T^\gamma$ and $P_{loss} \propto T^\beta$, the condition for [thermal instability](@entry_id:151762) is $\gamma > \beta$. For Spitzer [resistivity](@entry_id:266481) at constant voltage, $\gamma = 3/2$. Many empirical scaling laws for plasma energy confinement find that losses scale weakly with temperature, often with an exponent $\beta \le 1/2$. Thus, a purely Ohmically heated plasma is often thermally unstable.

This instability is a fundamental limitation of Ohmic heating. To reach high temperatures stably, tokamaks require **auxiliary heating** ($P_{aux}$), such as from [neutral beam injection](@entry_id:204293) or radiofrequency waves. This external heating is typically independent of the [plasma temperature](@entry_id:184751). By adding a constant power source, the stability criterion is modified. Marginal stability is achieved when a certain fraction of the total heating power comes from the auxiliary source. This minimum required auxiliary heating fraction can be shown to be [@problem_id:293764]:

$$ f_{min} = \frac{P_{aux}}{P_{Ohmic} + P_{aux}} = \frac{\gamma - \beta}{\gamma} $$

This result quantitatively explains why Ohmic heating alone is insufficient to reach [fusion reactor](@entry_id:749666) conditions; it becomes inefficient and thermally unstable at high temperatures, necessitating the large and expensive auxiliary heating systems found on all modern [tokamaks](@entry_id:182005).

### Advanced Corrections to Resistivity

The Spitzer model provides an excellent first approximation, but a more accurate description of [resistivity](@entry_id:266481) in a toroidal fusion device requires considering several advanced physical effects.

#### Toroidal and Kinetic Effects

In the [toroidal geometry](@entry_id:756056) of a [tokamak](@entry_id:160432), the magnetic field strength varies along a field line, being stronger on the inboard side and weaker on the outboard side. This creates magnetic mirrors that can trap a population of electrons on the outboard side of the torus. These **trapped electrons** do not complete full toroidal transits and thus do not contribute to the net toroidal current. This leads to a significant modification of the [plasma resistivity](@entry_id:196902), a phenomenon known as **[neoclassical resistivity](@entry_id:194823)**.

In the low-collisionality "banana" regime, two effects increase the resistivity above the Spitzer value. First, the current must be carried by a smaller population of **passing electrons**. Second, these passing electrons experience additional frictional drag from colliding with the relatively stationary trapped electron population. A simplified fluid model of the passing electrons illustrates this clearly. By balancing the electric field force against the frictional drag from both ions and trapped electrons, one can derive the neoclassical conductivity, $\sigma_\parallel$, and compare it to the Spitzer value, $\sigma_{Sp}$. The [neoclassical resistivity](@entry_id:194823) correction factor, $C_{neo} = \eta_{neo}/\eta_{Sp} = \sigma_{Sp}/\sigma_\parallel$, is found to depend on the geometry (via the inverse [aspect ratio](@entry_id:177707), $\epsilon = r/R$) and the collisionality (via $Z_{eff}$) [@problem_id:293658]. This enhancement of [resistivity](@entry_id:266481) is a crucial factor in the power balance and current profile evolution of modern [tokamaks](@entry_id:182005).

Furthermore, [toroidal geometry](@entry_id:756056) induces additional currents needed for MHD equilibrium. The most prominent are the **Pfirsch-Schlüter currents**, which flow parallel to the magnetic field to ensure that the total current density is [divergence-free](@entry_id:190991) ($\nabla \cdot \mathbf{J} = 0$). These currents also dissipate power through [resistivity](@entry_id:266481). However, analysis shows that the Ohmic power dissipated by Pfirsch-Schlüter currents, $P_{PS}$, is generally much smaller than that from the primary toroidal current, $P_\phi$. For a large-aspect-ratio [tokamak](@entry_id:160432), the ratio scales as $P_{PS}/P_\phi = \epsilon^2 \beta_p^2$, where $\beta_p$ is the poloidal beta [@problem_id:293800]. Since both $\epsilon$ and $\beta_p$ are typically of order unity or less, this contribution is a secondary, though not entirely negligible, part of the total Ohmic heating.

#### Runaway Electrons and Relativistic Effects

The simple picture of [resistivity](@entry_id:266481) as a gentle friction on the electron fluid breaks down under extreme conditions. If the accelerating force from the toroidal electric field, $eE$, exceeds the maximum collisional drag force that the background plasma can exert, an electron will be accelerated continuously. Such electrons are called **[runaway electrons](@entry_id:203887)**. The drag force on an electron is a non-[monotonic function](@entry_id:140815) of its velocity, peaking at a velocity near the thermal speed of the background particles and then decreasing as $1/v^2$ for high velocities. The electric field required to overcome this peak drag is known as the **[critical electric field](@entry_id:273150)**, $E_{crit}$. Its value depends sensitively on the density and temperature of the background plasma. In complex situations, such as plasmas with multiple [electron temperature](@entry_id:180280) populations, the drag force profile can have multiple local maxima, complicating the prediction of runaway generation [@problem_id:293756]. Runaway electrons are a major concern for tokamak operations, as they can be accelerated to relativistic energies (MeV) and cause severe, localized damage to the reactor wall if their confinement is lost.

Finally, at the very high temperatures envisioned for a fusion reactor ($T_e > 10$ keV), the thermal velocities of electrons can become a non-negligible fraction of the speed of light. In this regime, [relativistic effects](@entry_id:150245) must be included in the calculation of [resistivity](@entry_id:266481). The electron [distribution function](@entry_id:145626) is no longer Maxwellian but is described by the Maxwell-Jüttner distribution, and the [collision operator](@entry_id:189499) must be formulated in relativistic terms. Performing the conductivity calculation with these corrections shows that the [resistivity](@entry_id:266481) is higher than the classical Spitzer prediction. To first order in the normalized temperature $\theta_e = k_B T_e / (m_e c^2)$, the [resistivity](@entry_id:266481) can be expressed as [@problem_id:293652]:

$$ \eta = \eta_{NR} (1 + C \theta_e) $$

where $\eta_{NR}$ is the non-relativistic Spitzer [resistivity](@entry_id:266481) and $C$ is a numerical coefficient of order unity, found to be $C = 31/8$ in a simplified Lorentz gas model. This relativistic enhancement, while a small correction, highlights the frontiers of our understanding and the need to continually refine our models as we push toward the conditions required for sustained nuclear fusion.