## Introduction
Accretion disks around [supermassive black holes](@entry_id:157796) (SMBHs) are the engines that power some of the most luminous phenomena in the cosmos, including [active galactic nuclei](@entry_id:158029) (AGN) and [quasars](@entry_id:159221). Their incredible brilliance is not an intrinsic property but the result of an extraordinarily efficient conversion of energy. As gas and dust spiral inward toward the central black hole, immense [gravitational potential energy](@entry_id:269038) is released. The fundamental question this article addresses is: how is this mechanical energy transformed into the thermal energy that we observe as radiation? Answering this requires a deep dive into the complex physics of magnetized plasmas under extreme gravitational conditions.

This article will systematically unpack the processes that heat these cosmic structures. You will gain a comprehensive understanding of the physical principles at play, from foundational concepts to the frontiers of modern astrophysical research. The "Principles and Mechanisms" section will lay the groundwork, introducing [viscous heating](@entry_id:161646) through the classic $\alpha$-disk model and then revealing its physical origin in the magnetohydrodynamic turbulence driven by the Magneto-Rotational Instability (MRI). Following this, "Applications and Interdisciplinary Connections" will broaden the perspective, exploring how external factors like irradiation, winds, and companion objects contribute to heating, and how accretion disks serve as laboratories for fundamental physics. Finally, the "Hands-On Practices" section will provide an opportunity to apply these theoretical concepts to solve concrete astrophysical problems related to disk heating.

## Principles and Mechanisms

Accretion disks surrounding [supermassive black holes](@entry_id:157796) are some of the most luminous objects in the universe. Their brilliance is not intrinsic but is powered by the conversion of gravitational potential energy into thermal energy, which is then radiated away. As gas spirals inward toward the central black hole, a series of complex physical processes operate to dissipate its [orbital energy](@entry_id:158481). This section delves into the fundamental principles and mechanisms responsible for heating the plasma within these disks, moving from foundational phenomenological models to the intricate physics of magnetohydrodynamic turbulence and [relativistic effects](@entry_id:150245).

### Viscous Heating in Keplerian Shear Flows

The most fundamental heating mechanism in an [accretion disk](@entry_id:159604) arises from **[viscous dissipation](@entry_id:143708)**. The gas in a disk does not orbit as a solid body. Instead, it typically follows a **Keplerian velocity profile**, where the angular velocity $\Omega(r)$ depends on the radial distance $r$ from the central object of mass $M$:

$$
\Omega(r) = \sqrt{\frac{GM}{r^3}}
$$

where $G$ is the [gravitational constant](@entry_id:262704). This **[differential rotation](@entry_id:161059)** means that gas at an inner radius orbits faster than gas at an adjacent outer radius. This velocity difference, or **shear**, creates friction-like viscous stresses within the fluid. These stresses act to transport angular momentum outward, allowing mass to flow inward, and in doing so, they dissipate [mechanical energy](@entry_id:162989) as heat.

The rate of [energy dissipation](@entry_id:147406) per unit area of the disk, the [viscous heating](@entry_id:161646) rate $Q^+(r)$, is given by the product of the vertically-integrated shear stress, $W_{r\phi}(r)$, and the magnitude of the local shear, $r (d\Omega/dr)$:

$$
Q^+(r) = W_{r\phi}(r) \left( r \frac{d\Omega}{dr} \right)
$$

For a Keplerian disk, the shear term is straightforward to calculate:

$$
r \frac{d\Omega}{dr} = r \frac{d}{dr} \left( (GM)^{1/2} r^{-3/2} \right) = r \left( -\frac{3}{2} (GM)^{1/2} r^{-5/2} \right) = -\frac{3}{2} \sqrt{\frac{GM}{r^3}} = -\frac{3}{2} \Omega(r)
$$

The primary challenge lies in specifying the viscous stress $W_{r\phi}$. In their seminal 1973 paper, Shakura and Sunyaev introduced a phenomenological prescription that remains a cornerstone of [accretion disk](@entry_id:159604) theory. The **Shakura-Sunyaev $\alpha$-prescription** parameterizes the stress as being proportional to the vertically-integrated gas pressure, $\Pi(r)$:

$$
W_{r\phi}(r) = -\alpha \Pi(r)
$$

Here, $\alpha$ is a dimensionless constant, typically assumed to be between $0$ and $1$, which encapsulates the unknown efficiency of [angular momentum transport](@entry_id:160167). The negative sign signifies that viscous torques transport angular momentum outwards. Combining these elements provides a [closed-form expression](@entry_id:267458) for the heating rate per unit area:

$$
Q^+(r) = (-\alpha \Pi(r)) \left( -\frac{3}{2} \Omega(r) \right) = \frac{3}{2} \alpha \Pi(r) \Omega(r) = \frac{3}{2} \alpha \Pi(r) \sqrt{\frac{GM}{r^3}}
$$

This foundational result links the local heating rate directly to the local pressure and orbital frequency, parameterized by the efficiency factor $\alpha$.

### The Vertical Structure and Distribution of Heating

The $\alpha$-disk model can be extended from a two-dimensional, vertically-integrated picture to a three-dimensional one by considering the disk's vertical structure. In the vertical direction, the disk is supported against the vertical component of the central object's gravity, $g_z \approx \Omega^2 z$ (for a thin disk where height $z \ll r$), by an internal pressure gradient. This balance is known as **vertical hydrostatic equilibrium**:

$$
\frac{dP}{dz} = -\rho g_z = -\rho \Omega^2 z
$$

where $P$ is the local pressure and $\rho$ is the local density. For a vertically isothermal disk with a constant sound speed $c_s$ (where $P = \rho c_s^2$), this equation can be integrated to show that the [density profile](@entry_id:194142) is Gaussian:

$$
\rho(z) = \rho_0 \exp\left(-\frac{z^2}{2H^2}\right)
$$

Here, $\rho_0$ is the midplane density and $H$ is the characteristic **pressure [scale height](@entry_id:263754)** of the disk, given by $H = c_s / \Omega_K$. The [scale height](@entry_id:263754) represents the typical thickness of the disk at a given radius.

The [viscous heating](@entry_id:161646) can also be described by a local, volumetric rate, $Q^+(z)$. In terms of a [kinematic viscosity](@entry_id:261275), $\nu$, this is $Q^+(z) = \nu \rho (r \frac{d\Omega}{dr})^2$. The $\alpha$-prescription can be formulated locally as $\nu = \alpha c_s H$. By combining these relations, we can determine how the heating is distributed vertically within the disk. Substituting the expressions for the Keplerian shear, the local viscosity, and the vertical [density profile](@entry_id:194142), the volumetric heating rate becomes:

$$
Q^+(z) = (\alpha c_s H) \rho_0 \exp\left(-\frac{z^2}{2H^2}\right) \left(-\frac{3}{2}\Omega_K\right)^2 = \frac{9}{4} \alpha c_s H \Omega_K^2 \rho_0 \exp\left(-\frac{z^2}{2H^2}\right)
$$

Using the relations $P_0 = \rho_0 c_s^2$ and $H = c_s / \Omega_K$, this simplifies to an expression in terms of the midplane pressure $P_0$:

$$
Q^+(z) = \frac{9}{4} \alpha P_0 \Omega_K \exp\left(-\frac{z^2 \Omega_K^2}{2c_s^2}\right)
$$

This result demonstrates that [viscous heating](@entry_id:161646) is not uniform throughout the disk's thickness; it is concentrated near the midplane where the density and pressure are highest.

### The Role of Magnetic Fields

While the $\alpha$-model is powerfully descriptive, it is physically incomplete as it does not specify the origin of viscosity. The molecular viscosity of [astrophysical plasmas](@entry_id:267820) is far too low to account for observed accretion rates. The modern consensus is that "viscosity" is not a microscopic property but an effective stress arising from turbulence, which itself is driven by magnetic fields.

#### Ohmic Dissipation from Sheared Fields

A simple magnetohydrodynamic (MHD) model can illustrate how magnetic fields convert shear energy into heat. Consider a weak, pre-existing radial magnetic field, $B_R$, embedded in the differentially rotating disk. The Keplerian shear stretches these radial field lines in the azimuthal direction, generating a toroidal component, $B_\phi$. This process is described by the [induction equation](@entry_id:750617). In a steady state, the generation of $B_\phi$ by shear is balanced by its dissipation through the plasma's finite resistivity (or magnetic diffusivity, $\eta$).

Under the simplifying assumption that vertical gradients dominate, the steady-state [induction equation](@entry_id:750617) gives a relationship for the second derivative of the [toroidal field](@entry_id:194478). Integrating this equation with appropriate boundary conditions (e.g., $B_\phi$ vanishing at the disk surfaces $z=\pm H$) yields the vertical profile of the generated [toroidal field](@entry_id:194478). This spatially varying magnetic field induces an electric current density, $\mathbf{J} = (\nabla \times \mathbf{B})/\mu_0$. The presence of this current in a resistive medium leads to **[ohmic heating](@entry_id:190028)**, with a volumetric rate given by $Q^+ = \eta J^2$. For the sheared field model, this yields:

$$
Q^+(z) = \frac{9}{4} \frac{\Omega^2 B_R^2 z^2}{\mu_0 \eta}
$$

This result demonstrates a concrete physical mechanism for [viscous heating](@entry_id:161646): [differential rotation](@entry_id:161059) generates magnetic fields and currents, and the dissipation of these currents heats the plasma.

#### The Magneto-Rotational Instability (MRI): A Physical Origin for Turbulence

The simple shearing of a pre-existing field is not the full story. The most important process is the **Magneto-Rotational Instability (MRI)**. First identified by Velikhov and Chandrasekhar, and applied to [accretion disks](@entry_id:159973) by Balbus and Hawley, the MRI is a powerful linear instability that afflicts any weakly magnetized, differentially rotating fluid in which angular velocity decreases outward. The MRI efficiently converts the free energy in the orbital shear into [magnetic field energy](@entry_id:268850), driving vigorous MHD turbulence. This turbulence is now believed to be the primary source of the effective viscosity in most accretion disks.

The heating rate can be expressed in terms of the properties of this MRI-driven turbulence. A common approach is to assume the turbulent stress, $W_{r\phi}$, is a fraction of the local magnetic pressure, $P_{mag} = B^2/(2\mu_0)$. This gives a magnetically-based $\alpha$-parameter: $W_{r\phi} = \alpha_m P_{mag}$. The relative strength of gas and magnetic pressures is characterized by the **[plasma beta](@entry_id:192193) parameter**, $\beta = P_{gas}/P_{mag}$.

Following a model where the disk is in vertical [hydrostatic equilibrium](@entry_id:146746) under the total pressure ($P_{tot} = P_{gas} + P_{mag}$), we can relate the MRI-driven heating to the fundamental disk parameters. The effective sound speed is modified by the magnetic pressure, and the [scale height](@entry_id:263754) $H$ depends on $\beta$. The resulting turbulent heating rate per unit volume, $Q^+$, is found to be:

$$
Q^+ = \frac{3}{2} \frac{\alpha_m}{1+\beta} \rho \Omega^3 H^2
$$

This expression connects the phenomenological framework of [viscous heating](@entry_id:161646) to the underlying physics of MHD turbulence, replacing the generic $\alpha$ with parameters ($\alpha_m$, $\beta$) that have a more direct physical basis in magnetic field dynamics.

#### Magnetic Reconnection and Parasitic Instabilities

Going a level deeper, we can ask how the energy in the turbulent magnetic fields is ultimately converted to thermal energy. The non-linear evolution of the MRI often leads to the formation of large-scale [coherent structures](@entry_id:182915), such as **channel flows**, which feature regions of reversing magnetic field. These reversals create intense **current sheets**.

Such current sheets are unstable to secondary **parasitic instabilities**, notably resistive **[tearing modes](@entry_id:194294)**. These modes break and re-join magnetic field lines in a process called **[magnetic reconnection](@entry_id:188309)**, which rapidly converts [stored magnetic energy](@entry_id:274401) into particle kinetic energy (heat) and bulk flows. Using a simplified model for steady-state reconnection (similar to the Sweet-Parker model), we can estimate the heating rate from this process. The model relates the reconnection inflow and outflow speeds to the Alfven speed, $v_A = B/\sqrt{\mu_0 \rho}$, and uses Ampere's law and Ohm's law to solve for the current density $J$ and the resulting ohmic dissipation $Q = \eta J^2$. The result shows that the volumetric heating rate depends on the properties of the large-scale MRI flow:

$$
Q = \frac{k_z B_{ch}^3}{\gamma_L \mu_0^{3/2} \rho^{1/2}}
$$

where $B_{ch}$ and $k_z$ are the magnetic field amplitude and vertical wavenumber of the channel flow, and $\gamma_L$ is a geometric factor. This provides a microscopic picture of dissipation: energy stored in large-scale turbulent eddies cascades down and is ultimately thermalized in small-scale reconnection events.

### Other Heating Mechanisms

While viscous/[turbulent dissipation](@entry_id:261970) is often the dominant heating source, other mechanisms can be significant, particularly in certain regions of the disk or under specific conditions.

#### External Irradiation and Photoionization Heating

Accretion disks are not [isolated systems](@entry_id:159201). They are often bathed in intense radiation from a central X-ray source, commonly believed to be a hot, tenuous **corona** above the inner disk. This high-energy radiation can be a powerful source of heating for the disk's outer layers, or its **atmosphere**.

The primary mechanism is **[photoionization](@entry_id:157870) heating**. When a photon with energy $h\nu$ greater than the ionization potential $\chi$ of an atom strikes it, the atom is ionized. The excess energy, $h\nu - \chi$, is imparted to the ejected photoelectron, which then rapidly shares this energy with the surrounding plasma through collisions, thereby heating it. The total heating rate per unit volume, $\Gamma$, is found by integrating this energy deposition over the entire incident [photon flux](@entry_id:164816) distribution. For a pure hydrogen disk irradiated by a power-law [photon flux](@entry_id:164816), the calculation involves integrating the incident flux $F_\nu$ and the [photoionization cross-section](@entry_id:196879) $\sigma_{ph}(\nu)$ above the ionization [threshold frequency](@entry_id:137317) $\nu_{th} = \chi_H / h$:

$$
\Gamma = n_H \int_{\nu_{th}}^\infty (h\nu - \chi_H) \sigma_{ph}(\nu) F_\nu d\nu
$$

This calculation leads to a heating rate that depends on the incident flux properties and the [atomic physics](@entry_id:140823) of the gas. For a power-law flux $F_\nu \propto \nu^{-\alpha}$ and a cross-section $\sigma_{ph} \propto \nu^{-3}$, the result is:

$$
\Gamma = \frac{n_H \sigma_{th} K h^{\alpha-1} \chi_H^{2-\alpha}}{(\alpha+1)(\alpha+2)}
$$

where $K$ is the flux normalization and $\sigma_{th}$ is the cross-section at the threshold. Irradiation is crucial for determining the thermal and [ionization](@entry_id:136315) structure of the disk's upper layers and can dominate heating in the outer, cooler regions of the disk.

#### Heating from Shocks

Large-scale non-axisymmetric structures, such as **[spiral density waves](@entry_id:161546)**, can be excited in [accretion disks](@entry_id:159973) by [tidal forces](@entry_id:159188) or instabilities. As these waves propagate, they can steepen into **shock fronts**. Shocks are fundamentally irreversible phenomena where macroscopic kinetic energy is converted into thermal energy over a very narrow region, leading to a discontinuous jump in [fluid properties](@entry_id:200256) like density and pressure, and a sharp increase in entropy.

The [energy dissipation](@entry_id:147406) at a shock can be quantified using the **Rankine-Hugoniot [jump conditions](@entry_id:750965)**, which enforce the [conservation of mass](@entry_id:268004), momentum, and energy across the shock front. For a weak, isothermal shock, the dissipation rate per unit area, $\mathcal{F}_E$, can be calculated as a function of the pre-shock density $\rho_1$, the sound speed $c_s$, and the [relative density](@entry_id:184864) jump $s = (\rho_2 - \rho_1)/\rho_1 \ll 1$. To the leading order in shock strength, the [dissipation rate](@entry_id:748577) is approximately:

$$
\mathcal{F}_E \approx \frac{1}{6}\rho_1 c_s^3 s^3
$$

This shows that even weak shocks can be a significant source of local heating, converting the organized energy of the wave into disorganized thermal energy.

#### Compressional (PdV) Heating

In any fluid system, work can be done on a fluid element by pressure forces. This is known as **compressional heating** (or cooling), often referred to as $P dV$ work. The heating rate per unit area from this process is given by $\Gamma_{comp} = -\mathcal{P}(\nabla \cdot \mathbf{v})$, where $\mathcal{P}$ is the vertically-integrated pressure and $\nabla \cdot \mathbf{v}$ is the divergence of the flow velocity.

If the gas is being compressed ($\nabla \cdot \mathbf{v}  0$), $\Gamma_{comp}$ is positive, and the gas heats up. If it is expanding ($\nabla \cdot \mathbf{v} > 0$), $\Gamma_{comp}$ is negative, corresponding to adiabatic cooling. In a perfectly steady-state, circular Keplerian disk, this term is zero. However, it becomes important in non-steady disks or in regions with significant radial inflows or outflows. For instance, in a non-steady disk model with a time-dependent [surface density](@entry_id:161889) profile $\Sigma(r, t)$, the continuity equation can be used to solve for the [radial velocity](@entry_id:159824) $v_r$ and thus the divergence $\nabla \cdot \mathbf{v}$. This allows for the direct calculation of the compressional heating or cooling rate, which will depend on the rate of change of the disk's [surface density](@entry_id:161889).

### Global Energetics and Relativistic Effects

The local heating mechanisms collectively determine the total luminosity of the disk. The overall **radiative efficiency**, $\eta$, is the fraction of the accreted rest-mass energy ($\dot{M}c^2$) that is converted into radiation: $\eta = L_{disk} / (\dot{M}c^2)$. This efficiency is ultimately set by the total amount of [gravitational binding energy](@entry_id:159053) released as matter spirals from a large distance down to the inner edge of the disk.

For a standard thin disk, this inner edge is located at the **Innermost Stable Circular Orbit (ISCO)**. Inside the ISCO, [stable circular orbits](@entry_id:164103) are not possible according to General Relativity, and matter plunges rapidly into the black hole with little further energy release. The efficiency is therefore determined by the specific energy $E_{ISCO}$ of a particle at the ISCO, such that $\eta = 1 - E_{ISCO}/c^2$.

The radius of the ISCO, and consequently the value of $E_{ISCO}$, depends critically on the spin of the black hole. For a non-rotating (Schwarzschild) black hole, $r_{ISCO} = 6M$ (in geometrized units where $G=c=1$), which yields a modest efficiency of $\eta \approx 0.057$. For a rotating (Kerr) black hole, [frame-dragging](@entry_id:160192) effects pull the ISCO inwards for prograde orbits. For a **maximally rotating Kerr black hole** ($a=M$), the prograde ISCO is located at the gravitational radius, $r_{ISCO} = M$. By evaluating the general relativistic expression for a particle's specific energy at this limiting radius, we find the [specific energy](@entry_id:271007) is $E_{ISCO} = c^2/\sqrt{3}$. This yields a remarkable maximum radiative efficiency of:

$$
\eta = 1 - \frac{1}{\sqrt{3}} \approx 0.42
$$

This is over seven times more efficient than a disk around a non-[rotating black hole](@entry_id:261667) and nearly 42% of the rest-mass energy can be extracted. This demonstrates the profound impact of General Relativity and [black hole spin](@entry_id:274108) on the global energetics and observable properties of [accretion disks](@entry_id:159973).

### Thermal Stability of Accretion Disks

The balance between heating and cooling determines the thermal state of the disk. A crucial question is whether this thermal equilibrium ($Q^+ = Q^-$) is stable. A disk is **thermally unstable** if a small perturbation in temperature leads to a runaway effect. For example, if a slight increase in temperature causes heating to exceed cooling ($Q^+ > Q^-$), the temperature will continue to rise.

The condition for [thermal stability](@entry_id:157474), assuming perturbations occur at constant [surface density](@entry_id:161889) $\Sigma$, is that the cooling rate must respond more sensitively to changes in the disk structure than the heating rate does. Expressed logarithmically in terms of the disk [scale height](@entry_id:263754) $H$ (which is a proxy for temperature), the stability criterion is:

$$
\frac{\partial \ln Q^+}{\partial \ln H}\bigg|_\Sigma  \frac{\partial \ln Q^-}{\partial \ln H}\bigg|_\Sigma
$$

This criterion can be used to test the physical viability of different disk models. Consider the inner regions of a bright [accretion disk](@entry_id:159604), which are expected to be dominated by radiation pressure ($P \approx P_{rad} \propto T^4$) and have an opacity $\kappa$ dominated by electron scattering ($\kappa = \text{const.}$, so $n=0, m=0$ in the [opacity](@entry_id:160442) law $\kappa \propto \rho^n T^m$). If we assume a generalized [viscous heating](@entry_id:161646) where the stress tensor scales as a power of the pressure, $\tau_{r\phi} \propto P^b$, we can analyze the stability.

For the standard Shakura-Sunyaev model where stress is proportional to the total pressure ($\tau_{r\phi} \propto P$), and in a radiation-pressure dominated region ($P \approx P_{rad}$), we have $b=1$. The analysis shows that for electron-scattering [opacity](@entry_id:160442), the stability criterion becomes $b  0$, which is violated for $b=1$. Therefore, the standard $\alpha$-disk model is predicted to be thermally unstable in its inner, radiation-pressure-dominated regions. This famous instability suggests that such regions of the disk cannot remain smooth and steady, but may instead become clumpy, puff up into a geometrically thick "slim disk," or undergo limit-cycle variations in brightness. This demonstrates how a detailed understanding of heating and cooling mechanisms is essential not only for predicting the structure of disks but also their stability and time-dependent behavior.