## Introduction
Heating a plasma to the extreme temperatures required for [thermonuclear fusion](@entry_id:157725)—often exceeding 100 million Kelvin—is one of the central challenges in fusion energy science. This process is not merely about pouring in energy; it requires a sophisticated understanding of how energy is deposited, transported, and retained within the magnetically confined gas. This article delves into the two primary methods for achieving and sustaining these conditions: Ohmic heating and radiofrequency (RF) heating. It addresses the fundamental problem that while Ohmic heating is intrinsic to current-carrying tokamaks, its effectiveness diminishes precisely when it is needed most, necessitating powerful auxiliary RF systems with their own complex physics.

This exploration is structured to build a comprehensive understanding from the ground up. The first chapter, **Principles and Mechanisms**, lays the theoretical foundation, starting with the resistive nature of plasma that gives rise to Ohmic heating and moving to the intricate physics of [wave-particle interactions](@entry_id:1133979) that govern RF heating. The second chapter, **Applications and Interdisciplinary Connections**, expands on these principles, showcasing their critical role not only in controlling fusion plasmas but also in driving innovations across diverse fields such as semiconductor manufacturing and advanced medical procedures. Finally, the **Hands-On Practices** chapter provides an opportunity to apply these concepts through targeted problems, bridging the gap between theory and practical analysis. Together, these sections offer a complete journey into the physics of plasma heating, from first principles to real-world impact.

## Principles and Mechanisms

### Ohmic Heating: The Foundation of Plasma Current and Heating

In magnetically [confined plasmas](@entry_id:1122875), particularly in the tokamak configuration, the simplest and most fundamental method of heating is **Ohmic heating**, also known as Joule heating. This process is intrinsically linked to the generation of the [plasma current](@entry_id:182365) necessary for confinement itself. This section elucidates the principles governing Ohmic heating, starting from the microscopic origins of [plasma resistivity](@entry_id:196902) to its macroscopic consequences for plasma operation.

#### Plasma Resistivity and Ohm's Law

The flow of current in a plasma, as in any conductor, is met with resistance. This resistance arises from the collisional friction between the current-carrying electrons and the much heavier, relatively stationary ions. We can formalize this concept by considering the momentum balance for the electron fluid in a steady-state, [fully ionized plasma](@entry_id:200884). An externally applied parallel electric field, $E_{\parallel}$, exerts a force on the electrons, accelerating them along the magnetic field lines. This directed motion is balanced by the drag force from collisions with ions.

The parallel component of the electron momentum equation, neglecting inertial and pressure gradient effects, is given by:
$$ 0 = -n_e e E_{\parallel} + R_{ei, \parallel} $$
where $n_e$ is the electron density, $-e$ is the electron charge, and $R_{ei, \parallel}$ is the parallel component of the friction force density exerted by the ions on the electrons. This friction force is proportional to the [relative velocity](@entry_id:178060) between electrons and ions and the [collision frequency](@entry_id:138992). If the current is carried primarily by electrons, we can write $R_{ei, \parallel} \approx m_e n_e \nu_{ei} v_{e\parallel}$, where $m_e$ is the electron mass, $\nu_{ei}$ is the electron-ion momentum-transfer collision frequency, and $v_{e\parallel}$ is the electron fluid velocity.

The parallel current density is $J_{\parallel} = -n_e e v_{e\parallel}$. Substituting this into the [momentum balance](@entry_id:1128118), we arrive at a relationship between the electric field and the current density:
$$ E_{\parallel} = \left(\frac{m_e \nu_{ei}}{n_e e^2}\right) J_{\parallel} $$
This expression is the plasma equivalent of Ohm's law, $E_{\parallel} = \eta J_{\parallel}$. From this, we define the **parallel [plasma resistivity](@entry_id:196902)**, $\eta$, as the proportionality factor :
$$ \eta = \frac{m_e \nu_{ei}}{n_e e^2} $$
The inverse of resistivity is the **conductivity**, $\sigma = 1/\eta$. Understanding [plasma heating](@entry_id:158813) and current dynamics begins with understanding the behavior of this resistivity.

#### The Temperature Dependence of Resistivity: The Spitzer Formula

A key feature of a plasma is that its resistivity is not a constant material property but depends strongly on its temperature. This dependence arises from the nature of Coulomb collisions. In a hot plasma, charged particles interact via long-range Coulomb forces. The effective cross-section for these interactions decreases as the [relative velocity](@entry_id:178060) of the colliding particles increases. Faster electrons are deflected less by ions, leading to a lower [collision frequency](@entry_id:138992).

For a Maxwellian distribution of electrons with temperature $T_e$, the characteristic electron speed is the thermal speed, $v_{th,e} \propto \sqrt{T_e}$. The [collision frequency](@entry_id:138992) for momentum transfer in small-angle Coulomb scattering scales inversely with the cube of the particle speed, leading to a strong temperature dependence for the average [collision frequency](@entry_id:138992) :
$$ \nu_{ei} \propto v_{th,e}^{-3} \propto T_e^{-3/2} $$
Substituting this scaling into our expression for resistivity, we find:
$$ \eta \propto \frac{\nu_{ei}}{n_e} \propto \frac{n_e T_e^{-3/2}}{n_e} \propto T_e^{-3/2} $$
Remarkably, the explicit dependence on electron density $n_e$ in the numerator (from $\nu_{ei}$) and denominator cancels out. This leads to the celebrated **Spitzer resistivity** scaling, which states that the resistivity of a [fully ionized plasma](@entry_id:200884) is strongly dependent on temperature but nearly independent of density. A more detailed kinetic derivation provides the full scaling :
$$ \eta \propto \frac{Z_{\mathrm{eff}} \ln\Lambda}{T_e^{3/2}} $$
where $\ln\Lambda$ is the **Coulomb logarithm**, a weakly dependent term accounting for the range of impact parameters in collisions, and $Z_{\mathrm{eff}}$ is the effective ion charge, which accounts for the presence of impurities.

#### The Role of Impurities: Effective Charge $Z_{\mathrm{eff}}$

Real-world plasmas are never perfectly pure; they always contain a mixture of ion species, including the main fuel ions (e.g., deuterium) and impurity ions (e.g., carbon, tungsten) eroded from the vessel walls. Since the Coulomb force scales with charge, collisions with highly charged impurity ions are much more effective at scattering electrons than collisions with singly charged fuel ions. The momentum-transfer [collision frequency](@entry_id:138992) with a given ion species $j$ scales as $\nu_{ej} \propto n_j Z_j^2$, where $n_j$ and $Z_j$ are the density and charge number of that species.

The total resistivity depends on the sum of collision frequencies with all ion species. This dependence is conveniently captured by a single dimensionless parameter, the **effective ion charge**, $Z_{\mathrm{eff}}$ :
$$ Z_{\mathrm{eff}} \equiv \frac{\sum_j n_j Z_j^2}{n_e} = \frac{\sum_j n_j Z_j^2}{\sum_j n_j Z_j} $$
The resistivity is directly proportional to this parameter, $\eta \propto Z_{\mathrm{eff}}$. Even a very small concentration of high-$Z$ impurities can have a disproportionately large impact on resistivity. For instance, consider an initially pure deuterium plasma ($Z_D=1$, so $Z_{\mathrm{eff},0}=1$). If a trace amount of an impurity with charge $Z_{\mathrm{imp}}=30$ is introduced, such that the impurity-to-deuterium density ratio is a mere $f = n_{\mathrm{imp}}/n_D = 2.0 \times 10^{-4}$, the new [effective charge](@entry_id:190611) becomes:
$$ Z_{\mathrm{eff,trace}} = \frac{1 + f Z_{\mathrm{imp}}^2}{1 + f Z_{\mathrm{imp}}} = \frac{1 + (2.0 \times 10^{-4})(30)^2}{1 + (2.0 \times 10^{-4})(30)} \approx 1.173 $$
This corresponds to a fractional increase in resistivity of $\Delta = (Z_{\mathrm{eff,trace}}/Z_{\mathrm{eff},0}) - 1 \approx 0.173$, or a $17.3\%$ increase from a $0.02\%$ impurity concentration . This highlights the critical importance of impurity control in fusion devices.

#### Operational Implications of Spitzer Resistivity

The strong temperature dependence of Spitzer resistivity has profound consequences for tokamak operation .
During the **startup phase** of a discharge, the plasma is relatively cold (e.g., tens of eV). The resistivity $\eta$ is consequently very high. This is a double-edged sword:
1.  **Efficient Ohmic Heating**: The Ohmic power density, $p_\Omega = \eta J_\parallel^2$, is large, allowing the plasma to heat itself effectively and bootstrap its temperature upwards.
2.  **High Loop Voltage Requirement**: To drive a given current against the high resistive drag, a large toroidal electric field, and thus a high [loop voltage](@entry_id:1127453) from the [central solenoid](@entry_id:747208), is required.

Conversely, in a **high-temperature, reactor-grade plasma** (e.g., $T_e > 10$ keV), the plasma becomes an exceptionally good conductor, with resistivity lower than that of copper.
1.  **Inefficient Ohmic Heating**: The resistivity becomes so low that Ohmic heating alone is insufficient to sustain or further increase the plasma temperature against energy losses. This necessitates the use of **auxiliary heating** methods, such as radiofrequency waves or [neutral beam injection](@entry_id:204293).
2.  **Slow Current Profile Evolution**: The [characteristic timescale](@entry_id:276738) for the diffusion of the magnetic field and current profile is the **[resistive diffusion time](@entry_id:1130912)**, $\tau_R \sim \mu_0 a^2 / \eta$, where $a$ is the plasma minor radius. Since $\eta \propto T_e^{-3/2}$, it follows that $\tau_R \propto T_e^{3/2}$. In a hot plasma, $\tau_R$ can be extremely long (hours), meaning the current profile evolves very slowly and is essentially "frozen" into the plasma on operational timescales.

#### Power Balance and Electron-Ion Equilibration

The energy from Ohmic heating is deposited directly into the most mobile charge carriers: the electrons. Thus, Ohmic power is an exclusive energy source for the electron population, $P_\Omega = P_{\Omega,e}$. However, ions must also be heated to fusion-relevant temperatures. This occurs primarily through collisional energy exchange with the hotter electrons.

When electrons and ions are not at the same temperature, they [exchange energy](@entry_id:137069) via Coulomb collisions, with energy flowing from the hotter species to the colder one. In an Ohmically heated plasma, it is typical to find $T_e > T_i$. The volumetric rate at which electrons transfer power to ions is given by :
$$ p_{e \to i} = \frac{3 m_e}{m_i} \nu_{ei} n_e k_B (T_e - T_i) $$
where $m_i$ is the ion mass and $k_B$ is the Boltzmann constant. This equilibration power is a crucial term in the ion power balance equation, often serving as the dominant heat source for the ions. For a representative deuterium plasma with $n_e=10^{20}\,\text{m}^{-3}$, $T_e=5\,\text{keV}$, and $T_i=3\,\text{keV}$, the equilibration power density can be calculated to be approximately $p_{e \to i} \approx 0.366\,\text{MW/m}^3$, a significant power flow that couples the electron and ion energy channels .

### Anisotropy and Geometry: Beyond Simple Resistivity

The Spitzer model provides a powerful description of resistivity along magnetic field lines. However, a magnetized plasma is an inherently [anisotropic medium](@entry_id:187796), and its [toroidal geometry](@entry_id:756056) introduces further complexities that modify this simple picture.

#### Conductivity in a Magnetized Plasma: Anisotropy

When an electric field has a component perpendicular to the magnetic field, the plasma's response is dramatically different from its parallel response. The Lorentz force causes electrons to gyrate around magnetic field lines, severely restricting their ability to move across them in response to a perpendicular electric field. We can derive the full [conductivity tensor](@entry_id:155827) by solving the steady-state electron momentum equation including the magnetic force :
$$ 0 = -e(\mathbf{E} + \mathbf{V}_e \times \mathbf{B}) - m_e \nu_e \mathbf{V}_e $$
Solving for the electron velocity $\mathbf{V}_e$ and relating it to the current density $\mathbf{J} = -n_e e \mathbf{V}_e$ yields a tensor relationship $\mathbf{J} = \boldsymbol{\sigma} \cdot \mathbf{E}$. The components of this tensor reveal the anisotropy.

The **parallel conductivity**, limited only by collisions, is simply the Spitzer conductivity:
$$ \sigma_{\parallel} = \frac{n_e e^2}{m_e \nu_e} $$
The **perpendicular (Pedersen) conductivity**, which describes the current flowing parallel to a perpendicular electric field, is drastically reduced by the magnetic field:
$$ \sigma_{\perp} = \frac{\sigma_{\parallel}}{1 + (\omega_{ce}/\nu_e)^2} $$
where $\omega_{ce} = eB/m_e$ is the electron cyclotron frequency. In a typical tokamak core plasma ($T_e \sim 10$ keV, $B \sim 5$ T), the ratio of cyclotron frequency to collision frequency can be enormous, $\omega_{ce}/\nu_e \sim 10^8$. This leads to an extreme anisotropy in conductivity :
$$ \frac{\sigma_{\parallel}}{\sigma_{\perp}} = 1 + \left(\frac{\omega_{ce}}{\nu_e}\right)^2 \sim 10^{16} $$
This means it is vastly easier for current to flow along magnetic field lines than across them. The dominant response to a perpendicular electric field is not a parallel current but a perpendicular, non-dissipative current known as the **Hall current**, which arises from the $\mathbf{E}\times\mathbf{B}$ drift.

#### Neoclassical Effects: The Role of Toroidal Geometry

In the [toroidal geometry](@entry_id:756056) of a tokamak, the magnetic field strength varies along a field line, being weaker on the outboard side ($B \propto 1/R$). This spatial variation, combined with the conservation of energy and magnetic moment, leads to the phenomenon of **[magnetic trapping](@entry_id:159124)**. Particles with a high ratio of perpendicular to parallel velocity are reflected from the high-field regions, causing them to be trapped in "banana-shaped" orbits on the low-field side.

These **neoclassical effects** fundamentally alter plasma transport, including parallel conductivity . The impact depends critically on the **collisionality** of the plasma, a dimensionless parameter $\nu_*$ that compares the effective collision frequency to the [trapped particle](@entry_id:756144) bounce frequency:
$$ \nu_{*} \equiv \frac{\nu_{ei} q R}{\epsilon^{3/2} v_{the}} $$
where $\epsilon=a/R$ is the inverse aspect ratio and $q$ is the safety factor.

- In the **low-collisionality (banana) regime** ($\nu_* \ll 1$), trapped electrons execute many bounce orbits between collisions. Since they are trapped, they cannot contribute to the net parallel current driven by the toroidal electric field. The current is carried only by the fraction of untrapped, or "passing," particles. This leads to a reduction in the parallel conductivity compared to the Spitzer value, with the leading correction being proportional to the trapped particle fraction, $\sqrt{\epsilon}$: $\sigma_{\parallel}^{\mathrm{nc}} \approx \sigma_{\mathrm{Sp}} (1 - C \sqrt{\epsilon})$.

- In the **high-collisionality (Pfirsch-Schlüter) regime** ($\nu_* \gg 1$), collisions are too frequent for [trapped particle](@entry_id:756144) orbits to form. However, another neoclassical effect emerges. The combination of pressure gradients and field-line curvature drives perpendicular currents. To maintain charge neutrality ($\nabla \cdot \mathbf{J} = 0$), these perpendicular currents must close via parallel currents flowing along the magnetic field lines. These additional **Pfirsch-Schlüter currents** lead to extra dissipation, effectively increasing the parallel resistivity by a factor that scales with the geometry as $\eta_{\parallel}^{\mathrm{nc}} \approx \eta_{\mathrm{Sp}} (1 + c_{PS} q^2)$ . This corresponds to a reduction in conductivity.

In the hypothetical limit of a straight cylinder ($\epsilon \to 0$), all magnetic field variations along a field line vanish. The trapped particle fraction goes to zero, and the geometric effects driving Pfirsch-Schlüter currents disappear. In this limit, all neoclassical corrections become negligible, and the conductivity correctly reverts to the classical Spitzer result .

### Radiofrequency (RF) Heating and Current Drive

As Ohmic heating becomes inefficient at high temperatures, auxiliary heating systems are required. Radiofrequency (RF) heating is a versatile method that involves launching high-power [electromagnetic waves](@entry_id:269085) into the plasma.

#### Fundamental Principles: Wave-Particle Resonances

RF heating works by tuning the frequency of the launched waves to match a natural [resonant frequency](@entry_id:265742) of the plasma particles. When this condition is met, a [strong interaction](@entry_id:158112) occurs, and energy is efficiently transferred from the wave to the particles. The primary schemes include :

- **Electron Cyclotron Resonance Heating (ECRH)**: Waves at or near the electron cyclotron frequency ($\omega \approx \Omega_{ce}$) are resonantly absorbed by electrons, increasing their perpendicular kinetic energy.
- **Ion Cyclotron Resonance Heating (ICRH)**: Waves near the ion cyclotron frequency ($\omega \approx \Omega_{ci}$) or its harmonics are absorbed by ions. This can heat the bulk ions directly or, more commonly, a minority ion species which then transfers its energy to the bulk plasma via collisions.
- **Lower Hybrid (LH) Heating**: Waves at the lower hybrid frequency are used to accelerate electrons parallel to the magnetic field through Landau damping, a resonant interaction between the wave's phase velocity and the particle's velocity.

This allows for targeted heating of either electrons or ions, providing a powerful tool for controlling the plasma's energy distribution.

#### Accessibility, Cutoffs, and Resonances

For RF heating to be effective, the waves launched from an antenna at the plasma edge must be able to propagate to the desired resonance location in the plasma core. This is the problem of **accessibility**. The propagation of a wave is described by its refractive index, $n$. A wave propagates where $n^2 > 0$, is evanescent (exponentially decaying) where $n^2  0$, and reflects at a **cutoff** where $n^2=0$. The wave is absorbed at a **resonance**, where the cold-plasma model often predicts a singularity ($n^2 \to \infty$) that is resolved into strong absorption by kinetic effects in a hot plasma.

Accessibility requires a [continuous path](@entry_id:156599) of propagation ($n^2>0$) from the antenna to the resonance layer. If an evanescent region lies in the path, the wave may be reflected before reaching its target .

As a concrete example, consider an Ordinary-mode (O-mode) wave used for ECRH. In the cold-plasma model, its refractive index is given by $n^2 = P = 1 - \omega_{pe}^2/\omega^2$, where $\omega_{pe}$ is the [electron plasma frequency](@entry_id:197401).
- A **cutoff** occurs where $n^2=0$, which implies $\omega = \omega_{pe}$. This sets a density limit for propagation; if the plasma density is too high, the wave cannot penetrate.
- The **resonance** occurs where the wave frequency matches the local [electron cyclotron frequency](@entry_id:203398), $\omega=\Omega_{ce}(R)$. In a tokamak, this defines a specific vertical layer where $B(R) = \omega m_e/e$.

For a high-field tokamak with parameters like $B_0=5\,\text{T}$ and a central density of $n_{e,core}=8\times10^{19}\,\text{m}^{-3}$, a $140\,\text{GHz}$ ECRH wave has a frequency well above the maximum plasma frequency, so no O-mode cutoff is encountered. The [resonance condition](@entry_id:754285) $\omega=\Omega_{ce}$ occurs where $B=5\,\text{T}$, which is precisely on the magnetic axis. Thus, the wave has clear access to the core for central heating . Other wave types, like the Extraordinary (X-mode) wave, have more complex cutoffs and resonances involving Stix parameters $R$, $L$, and $S$, but the fundamental principle of accessibility remains the same .

#### Non-Inductive Current Drive and Its Impact on the Plasma

In addition to transferring energy, RF waves can also transfer momentum to the plasma particles, thereby driving a **non-inductive current**, $J_{\mathrm{NI}}$. This is a critical capability for achieving long-pulse or steady-state tokamak operation, which cannot be sustained by a transformer with finite magnetic flux.

The presence of a non-inductive current source modifies the parallel Ohm's law. The total parallel current, $J_\parallel$, is now the sum of the Ohmically driven current ($J_\Omega$) and the non-inductive current ($J_{\mathrm{NI}}$). The parallel electric field is only responsible for driving the Ohmic portion :
$$ E_\parallel = \eta J_\Omega = \eta (J_\parallel - J_{\mathrm{NI}}) $$
In steady state, the toroidal electric field $E_\varphi \approx E_\parallel$ must be uniform across the plasma radius. Integrating the current density profile over the plasma cross-section, we can find the required [loop voltage](@entry_id:1127453) $V_{\mathrm{loop}} = 2\pi R_0 E_\varphi$ to sustain a total plasma current $I_p$ :
$$ V_{\mathrm{loop}} = \frac{I_p - I_{\mathrm{NI}}}{\int_0^a \sigma(r) (2\pi r / 2\pi R_0) dA_p} \approx \frac{2\pi R_0 (I_p - I_{\mathrm{NI}})}{\int_0^a \sigma(r) 2\pi r dr} $$
where $I_{\mathrm{NI}} = \int J_{\mathrm{NI}}(r) dA_p$ is the total non-inductive current. This shows that the loop voltage drives only the portion of the current not provided by external sources. **Fully non-inductive operation**, the goal for a steady-state reactor, is achieved when the entire plasma current is driven externally ($I_{\mathrm{NI}} = I_p$), allowing the [loop voltage](@entry_id:1127453) to be zero ($V_{\mathrm{loop}} = 0$) .

#### Local Power Exchange and Negative Ohmic Heating

A fascinating consequence of non-ohmic [current drive](@entry_id:186346) arises when considering the local power exchange between the electromagnetic field and the plasma, given by $Q = \mathbf{E}\cdot\mathbf{J}$. Using the decomposition of the current, we find :
$$ Q(\mathbf{x}) = \mathbf{E}\cdot\mathbf{J}_{\mathrm{res}} + \mathbf{E}\cdot(\mathbf{J}_{\mathrm{bs}} + \mathbf{J}_{\mathrm{rf}}) $$
The first term, $\mathbf{E}\cdot\mathbf{J}_{\mathrm{res}} = \mathbf{E}\cdot(\boldsymbol{\sigma}:\mathbf{E})$, is the irreversible resistive dissipation. As the [conductivity tensor](@entry_id:155827) $\boldsymbol{\sigma}$ is positive-definite, this term is always non-negative, $Q_{\mathrm{irr}} \ge 0$, in accordance with the second law of thermodynamics.

However, the second term, representing the work done by the field $\mathbf{E}$ on the non-ohmic currents, can be negative. The bootstrap current ($\mathbf{J}_{\mathrm{bs}}$) and RF-driven current ($\mathbf{J}_{\mathrm{rf}}$) are sustained by pressure gradients and external waves, respectively, not by $\mathbf{E}$. If these currents are driven in the direction opposite to the inductive electric field $\mathbf{E}$, and are sufficiently strong, the total power exchange $Q$ can become negative. The precise condition for this is :
$$ |J_{\mathrm{bs},\parallel} + J_{\mathrm{rf},\parallel}| > \sigma_{\parallel}|E_{\parallel}| $$
When $Q(\mathbf{x})  0$, the plasma in that region is not being heated by the inductive field; instead, it is acting as a dynamo, converting particle kinetic energy (supplied by the bootstrap or RF mechanisms) into electromagnetic energy. According to the Poynting theorem, $\nabla \cdot \mathbf{S} = -\mathbf{E}\cdot\mathbf{J}$, this energy appears as an outward flux of electromagnetic power from that region, which can be delivered back to the external transformer circuit. This "negative Ohmic heating" is a key feature of [advanced tokamak scenarios](@entry_id:746315) with high fractions of non-inductive current.

### Extreme Electric Fields: Runaway Electron Generation

Under certain conditions, particularly during plasma disruptions where a rapid thermal quench occurs, large toroidal electric fields can be induced. These fields can cause a fraction of the electron population to be accelerated to relativistic energies, creating a beam of **[runaway electrons](@entry_id:203887)**.

#### The Runaway Phenomenon

The phenomenon arises from the velocity dependence of the collisional drag force. The drag on an electron peaks at low energies and decreases as $\sim v^{-2}$ for super-thermal electrons. If an electron is accelerated by an electric field $E_\parallel$ to an energy where the accelerating force $eE_\parallel$ exceeds the collisional drag, it will be accelerated indefinitely, or "run away".

#### Primary and Secondary Generation Mechanisms

There are two principal mechanisms for runaway electron generation :
1.  **Primary (Dreicer) Generation**: This process creates runaways directly from the thermal electron population. Electrons in the high-energy tail of the Maxwellian distribution may already be moving fast enough that the electric field can overcome the collisional drag. This mechanism, first described by Dreicer, seeds the runaway population.
2.  **Secondary (Avalanche) Generation**: This mechanism requires a pre-existing seed of relativistic runaways. When a high-energy runaway electron collides with a thermal electron in a "knock-on" event, it can transfer a large amount of energy, promoting the thermal electron into the runaway regime. This new runaway can then create others, leading to an [exponential growth](@entry_id:141869), or avalanche, of the runaway population.

#### The Avalanche Threshold

An avalanche becomes self-sustaining if a newly created secondary runaway gains more energy from the electric field than it loses to collisions. The drag force has a [local minimum](@entry_id:143537) at relativistic energies. The avalanche threshold is defined by the **critical electric field**, $E_c$, at which the accelerating force balances this minimum drag. Avalanche multiplication occurs when :
$$ E_{\parallel} > E_c $$
The [critical field](@entry_id:143575), derived by Connor and Hastie, is given by:
$$ E_c = \frac{n_e e^3 \ln\Lambda}{4\pi\epsilon_0^2 m_e c^2} $$
During a disruption in a large tokamak, the post-quench plasma might have $n_e = 5 \times 10^{19}\,\text{m}^{-3}$ and an induced electric field of $E_\parallel = 0.12\,\text{V/m}$. For these parameters, the critical field is calculated to be $E_c \approx 0.038\,\text{V/m}$. Since $E_\parallel \approx 3.1 E_c$, the applied field is well above the avalanche threshold, indicating that if a seed population exists, a large [runaway avalanche](@entry_id:754455) is likely to occur, posing a significant risk to the integrity of the fusion device .