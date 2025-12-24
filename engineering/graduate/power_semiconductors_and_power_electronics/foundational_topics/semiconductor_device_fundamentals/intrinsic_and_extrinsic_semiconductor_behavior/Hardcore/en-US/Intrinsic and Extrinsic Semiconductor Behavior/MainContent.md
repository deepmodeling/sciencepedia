## Introduction
The performance and reliability of modern power electronic systems are built upon the microscopic behavior of charge carriers within semiconductor materials. Understanding the distinction between intrinsic (pure) and extrinsic (doped) semiconductor properties is not just a foundational concept in solid-state physics; it is the key to designing, optimizing, and troubleshooting the power devices that drive our world, from electric vehicles to renewable energy grids. This article bridges the gap between abstract quantum mechanics and tangible engineering outcomes, addressing how fundamental [carrier dynamics](@entry_id:180791) translate into real-world device characteristics.

In the chapters that follow, we will embark on a comprehensive exploration of this critical topic. We will begin in **Principles and Mechanisms** by dissecting the core physics, from the quantum origins of energy bands and effective mass to the statistical laws governing carrier populations and transport. Next, in **Applications and Interdisciplinary Connections**, we will see how these principles are applied to engineer device performance, examining concepts like conductivity modulation, the [superjunction](@entry_id:1132645) principle, and the pivotal role of wide-bandgap materials. Finally, the **Hands-On Practices** section will provide opportunities to apply this knowledge to solve practical engineering problems, reinforcing the connection between theory and application. This journey will equip you with a graduate-level understanding of how to control semiconductor behavior to build more efficient and robust power devices.

## Principles and Mechanisms

The behavior of power [semiconductor devices](@entry_id:192345) is fundamentally governed by the population and motion of charge carriers—electrons and holes—within the crystalline structure of the semiconductor material. Understanding the principles that dictate carrier concentrations, energy states, and transport mechanisms is therefore essential for device analysis and design. This chapter delineates these core principles, beginning with the quantum mechanical description of carriers in a periodic lattice and proceeding to the statistical mechanics of their populations, their response to fields and gradients, and the dynamic processes of generation and recombination that control their numbers.

### Energy Bands and Effective Mass

The defining characteristic of a crystalline solid is the [periodic potential](@entry_id:140652) created by the atomic lattice. The solutions to the Schrödinger equation for an electron in such a potential are not discrete energy levels, as in an isolated atom, but rather continuous bands of allowed energy states, separated by forbidden [energy gaps](@entry_id:149280). For a semiconductor, the highest energy band that is completely filled with electrons at absolute zero temperature is called the **valence band**, and the lowest empty band is the **conduction band**. The energy difference between the top of the valence band ($E_v$) and the bottom of the conduction band ($E_c$) is the **[bandgap energy](@entry_id:275931)**, $E_g = E_c - E_v$. This bandgap is the primary determinant of a semiconductor's electrical and optical properties.

The energy of an electron state, $E$, is not only a function of the band it is in but also of its [crystal momentum](@entry_id:136369), represented by the wavevector $k$. The relationship $E(k)$, known as the **[energy dispersion relation](@entry_id:145014)** or **band structure**, encodes the dynamics of charge carriers.

#### Direct and Indirect Bandgaps

The locations in $k$-space where the valence band maximum and conduction band minimum occur determine whether a semiconductor has a direct or [indirect bandgap](@entry_id:268921).
- In a **[direct-gap semiconductor](@entry_id:191146)** (e.g., Gallium Arsenide, GaAs), the valence band maximum and conduction band minimum occur at the same value of $k$. An electron can transition from the top of the valence band to the bottom of the conduction band (e.g., by absorbing a photon) without a significant change in its crystal momentum.
- In an **indirect-gap semiconductor** (e.g., Silicon, Si, and Silicon Carbide, SiC), the valence band maximum and conduction band minimum occur at different values of $k$. A transition between these band edges requires both a change in energy and a change in momentum. Since a photon carries negligible momentum, another particle must be involved to conserve crystal momentum. This role is filled by a **phonon**, a quantum of lattice vibration. The necessity of this third particle (a phonon) makes band-edge transitions a second-order process, which is statistically less probable than the first-order process in direct-gap materials . This has profound consequences: indirect-gap materials like silicon are inefficient light emitters but tend to have longer carrier lifetimes, a property that is critical in many power devices.

#### The Effective Mass Approximation

To describe the motion of an electron within a band under the influence of an external force (e.g., from an electric field), it is inconvenient to work with the full $E(k)$ diagram. Instead, we can use the **[effective mass approximation](@entry_id:137643)**. Near a band extremum (e.g., the bottom of the conduction band), we can approximate the band structure using a Taylor [series expansion](@entry_id:142878) of $E(k)$ around the extremum point $k_0$. Since the gradient $\nabla_k E$ is zero at an extremum, the first-order term vanishes. Truncating at the second-order term gives a [quadratic approximation](@entry_id:270629) :
$$
E(k) \approx E(k_0) + \frac{1}{2} \sum_{i,j} \left(\frac{\partial^2 E}{\partial k_i \partial k_j}\right)_{k=k_0} (k_i - k_{0,i})(k_j - k_{0,j})
$$
By comparing the semiclassical acceleration of an electron, $a_i = \frac{1}{\hbar^2} \sum_j \frac{\partial^2 E}{\partial k_i \partial k_j} F_j$, with Newton's second law, $a_i = \sum_j (m^*)^{-1}_{ij} F_j$, we can define the **inverse [effective mass tensor](@entry_id:147018)**:
$$
\left( (m^*)^{-1} \right)_{ij} = \frac{1}{\hbar^2} \frac{\partial^2 E}{\partial k_i \partial k_j}
$$
The effective mass $m^*$ encapsulates how a carrier responds to an external force; a flatter band (small curvature) corresponds to a larger effective mass, while a more curved band corresponds to a smaller effective mass.

For many cases, especially near the center of the Brillouin zone ($\Gamma$-point), the band can be approximated as isotropic. The tensor reduces to a scalar $m^*$, and the energy dispersion simplifies to the familiar **[parabolic band approximation](@entry_id:1129305)**:
$$
E(k) - E_c = \frac{\hbar^2 |k|^2}{2 m_n^*}
$$
where $m_n^*$ is the electron effective mass at the conduction band edge. This simple parabolic relationship allows us to treat electrons in the crystal lattice as quasi-[free particles](@entry_id:198511), but with a mass modified by the lattice potential.

However, this is an approximation valid only for carriers with low energy, close to the band edge. In power devices operating at high electric fields, carriers can be accelerated to higher energies where the $E(k)$ relationship deviates from a simple parabola. This is known as **[non-parabolicity](@entry_id:147393)**. For instance, a more accurate dispersion for a material like 4H-SiC might be modeled as $\Delta E(k) \approx A|k|^2 + B|k|^4$. The band-edge effective mass is determined solely by the quadratic coefficient, $m^* = \hbar^2 / (2A)$, but the quartic term becomes significant at higher energies, making the effective mass itself energy-dependent. Furthermore, if carriers gain enough energy, they can scatter into other, higher-energy valleys in the band structure (**intervalley scattering**), which may have a different effective mass. The simple scalar effective mass model is therefore most applicable under conditions of low fields, low temperatures, and non-degenerate doping .

### Carrier Statistics: The Fermi Level and Doping

While the band structure describes the available states for carriers, **Fermi-Dirac statistics** describes the probability of these states being occupied. The **Fermi-Dirac distribution function**, $f(E)$, gives the probability that a state with energy $E$ is occupied by an electron:
$$
f(E) = \frac{1}{1 + \exp\left(\frac{E - \mu}{k_B T}\right)}
$$
where $k_B$ is the Boltzmann constant, $T$ is the absolute temperature, and $\mu$ is the **Fermi level**.

#### The Fermi Level as Electrochemical Potential

The Fermi level is a concept of central importance. From a thermodynamic perspective, the Fermi level $\mu$ is the **[electrochemical potential](@entry_id:141179)** of the electron system. It represents the total energy required to add one electron to the system and is the sum of two components: the chemical potential $\mu^{\mathrm{chem}}$ and the [electrical potential](@entry_id:272157) energy $-q\phi$, where $\phi$ is the local electrostatic potential .
$$
\mu = \mu^{\mathrm{chem}} - q\phi
$$
The fundamental condition for a system in **thermal equilibrium** is that the electrochemical potential (the Fermi level) must be spatially constant throughout the system, i.e., $\nabla \mu = 0$. This implies that any spatial variation in the chemical potential (driven by, for example, a concentration gradient) must be perfectly balanced by a variation in the electrostatic potential (an electric field). This principle of a constant Fermi level at equilibrium is the key to understanding phenomena like the formation of a [built-in potential](@entry_id:137446) and band bending at a p-n junction. The balance it enforces between drift and diffusion currents guarantees zero net current without needing to consider the specific scattering mechanisms that determine mobility or diffusivity .

#### Intrinsic and Extrinsic Semiconductors

In a perfectly pure semiconductor, the only mobile charge carriers are electrons that have been thermally excited from the valence band to the conduction band, leaving behind an equal number of holes in the valence band. Such a material is an **[intrinsic semiconductor](@entry_id:143784)**. The [electron concentration](@entry_id:190764) $n$ equals the hole concentration $p$, and this value is known as the **[intrinsic carrier concentration](@entry_id:144530)**, $n_i$. At equilibrium, the product of electron and hole concentrations is constant for a given temperature, a result known as the **law of mass action**:
$$
np = n_i^2
$$
The intrinsic concentration $n_i$ is strongly dependent on temperature and the bandgap, with the dominant dependence being $n_i \propto \exp(-E_g / (2k_B T))$. This exponential rise means that even in doped devices, intrinsic carriers can become dominant at the high operating temperatures typical of power electronics, leading to significant leakage currents .

To control the [carrier concentration](@entry_id:144718) and conductivity, semiconductors are intentionally doped with impurities.
- **Donors** are impurity atoms (e.g., Phosphorus in Silicon) that can easily donate an electron to the conduction band. A semiconductor with a majority of donors is called **n-type**, where electrons are the majority carriers and holes are the minority carriers.
- **Acceptors** are impurity atoms (e.g., Boron in Silicon) that can easily accept an electron from the valence band, creating a mobile hole. A semiconductor with a majority of acceptors is called **p-type**, where holes are the majority carriers.

In such **[extrinsic semiconductors](@entry_id:138316)**, the carrier concentrations are determined by the dopant concentrations and the principle of **[charge neutrality](@entry_id:138647)**, which states that the total positive charge density must equal the total negative charge density. Assuming complete ionization of dopants, this is expressed as:
$$
p + N_D^+ = n + N_A^- \implies p + N_D = n + N_A
$$
where $N_D$ and $N_A$ are the donor and acceptor concentrations, respectively. In a **[compensated semiconductor](@entry_id:143085)**, both [donor and acceptor impurities](@entry_id:266183) are present. The net effective doping determines the material type. If $N_D > N_A$, the material is n-type with an effective donor concentration of $N_D - N_A$.

To find the equilibrium electron ($n$) and hole ($p$) concentrations in a [compensated semiconductor](@entry_id:143085), one must solve the [charge neutrality equation](@entry_id:260929) and the law of mass action simultaneously. This leads to a quadratic equation for the majority [carrier concentration](@entry_id:144718). For example, in an n-type compensated material ($N_D > N_A$), the electron concentration is given by :
$$
n = \frac{(N_D - N_A) + \sqrt{(N_D - N_A)^2 + 4n_i^2}}{2}
$$
In most practical cases for [extrinsic semiconductors](@entry_id:138316) at room temperature, the net doping $|N_D - N_A|$ is much larger than $n_i$. The majority [carrier concentration](@entry_id:144718) is then approximately equal to the [net doping concentration](@entry_id:1128552), $n \approx N_D - N_A$, and the minority carrier concentration can be found from the law of [mass action](@entry_id:194892), $p \approx n_i^2 / (N_D - N_A)$. For instance, in a silicon drift region with $N_D = 1.00 \times 10^{15} \, \text{cm}^{-3}$ and $N_A = 2.00 \times 10^{14} \, \text{cm}^{-3}$ at 300 K, the net effective doping is $8.00 \times 10^{14} \, \text{cm}^{-3}$. This results in a majority [electron concentration](@entry_id:190764) of $n \approx 8.000 \times 10^{14} \, \text{cm}^{-3}$ and a minority hole concentration of $p \approx 1.250 \times 10^{5} \, \text{cm}^{-3}$ .

### Carrier Transport: Mobility and Diffusion

Charge carriers in a semiconductor are in constant random thermal motion. A net transport of charge, or current, arises in response to two main driving forces: an electric field (drift) and a concentration gradient (diffusion).

#### Mobility and Scattering Mechanisms

An electric field $\mathbf{E}$ exerts a force on carriers, causing them to accelerate. This acceleration is constantly interrupted by scattering events with the lattice and impurities. The net effect is a steady-state average velocity called the **drift velocity**, $\mathbf{v}_d$, which is proportional to the electric field for low fields:
$$
\mathbf{v}_d = \mu \mathbf{E}
$$
The proportionality constant, $\mu$, is the **mobility**. It is a measure of how easily carriers can move through the crystal and is limited by scattering. The two most important scattering mechanisms are:
1.  **Lattice Scattering**: Also known as phonon scattering, this is due to interactions with the thermal vibrations of the crystal lattice. As temperature increases, lattice vibrations become more energetic, increasing the scattering rate and thus decreasing mobility.
2.  **Ionized Impurity Scattering**: This is caused by the electrostatic (Coulomb) interaction between carriers and the fixed charged donor and acceptor ions. This mechanism is most effective at low temperatures and for slow-moving carriers. As temperature increases, carriers move faster and are less effectively deflected by the impurity ions, so mobility due to this mechanism increases with temperature.

In a moderately [doped semiconductor](@entry_id:1123927) over a typical operating temperature range (e.g., 200-400 K), lattice scattering is the dominant mechanism. A theoretical analysis of **acoustic [deformation potential](@entry_id:748275) scattering**—the primary form of lattice scattering in nonpolar semiconductors like silicon—predicts that the average [scattering time](@entry_id:272979) $\langle\tau\rangle$ is proportional to $T^{-3/2}$. Since mobility is proportional to $\langle\tau\rangle$, this yields the classic temperature dependence for lattice-limited mobility :
$$
\mu_L \propto T^{-3/2}
$$
Experimental data for electron mobility in silicon, such as values of approximately $1350 \, \text{cm}^2/(\text{V}\cdot\text{s})$ at 300 K and $880 \, \text{cm}^2/(\text{V}\cdot\text{s})$ at 400 K, are well-fitted by a power law $\mu(T) \propto T^{-m}$ with an exponent $m \approx 1.5$, confirming the dominance of this scattering mechanism in this regime .

#### Diffusion and the Continuity Equation

Carriers will also move from a region of high concentration to a region of low concentration. This process, **diffusion**, gives rise to a [diffusion current](@entry_id:262070) density, which is proportional to the concentration gradient:
$$
\mathbf{J}_{p, \text{diff}} = -q D_p \nabla p \quad \text{(for holes)}
$$
$$
\mathbf{J}_{n, \text{diff}} = +q D_n \nabla n \quad \text{(for electrons)}
$$
The parameter $D$ is the **diffusion coefficient**. It is not an independent parameter but is related to mobility through the **Einstein relation**:
$$
D = \frac{k_B T}{q} \mu
$$
This relationship is a manifestation of the fluctuation-dissipation theorem, linking the random thermal motion (diffusion) to the response to a systematic force (mobility).

The interplay between drift, diffusion, and [carrier generation](@entry_id:263590)/recombination is described by the **carrier continuity equation**. For holes, it is:
$$
\frac{\partial p}{\partial t} = G_p - U_p - \frac{1}{q} \nabla \cdot \mathbf{J}_p
$$
where $G_p$ is the generation rate and $U_p$ is the recombination rate. In steady-state, under [low-level injection](@entry_id:1127474) in a region with no electric field and uniform recombination lifetime $\tau_p$, this equation simplifies to a differential equation for the excess minority [carrier concentration](@entry_id:144718), $\Delta p(x) = p(x) - p_0$ :
$$
D_p \frac{d^2 \Delta p(x)}{d x^2} - \frac{\Delta p(x)}{\tau_p} = 0
$$
The solution to this equation shows that an excess concentration injected at a point decays exponentially with distance. For example, for a semi-infinite region with an excess concentration $\Delta p_0$ maintained at $x=0$, the profile is:
$$
\Delta p(x) = \Delta p_0 \exp\left(-\frac{x}{L_p}\right)
$$
The [characteristic decay length](@entry_id:183295), $L_p$, is the **[minority carrier diffusion](@entry_id:188843) length**, defined as:
$$
L_p = \sqrt{D_p \tau_p}
$$
The [diffusion length](@entry_id:172761) represents the average distance a [minority carrier](@entry_id:1127944) can diffuse before it recombines. It is a critical parameter that determines the behavior of many power devices, such as the current gain of bipolar transistors and the forward voltage drop of p-i-n diodes. For a typical silicon drift region with a [hole mobility](@entry_id:1126148) of $400 \, \text{cm}^2/(\text{V}\cdot\text{s})$ and a lifetime of $8.0 \, \mu\text{s}$ at 300 K, the [diffusion length](@entry_id:172761) is approximately $91 \, \mu\text{m}$ .

### Generation and Recombination Processes

The concentration of carriers is determined by the dynamic balance between generation (creation of electron-hole pairs) and recombination (annihilation of electron-hole pairs). The net [recombination rate](@entry_id:203271), $U$, dictates the carrier lifetime and is governed by three primary mechanisms.

1.  **Shockley-Read-Hall (SRH) Recombination**: This is an indirect, two-step process that occurs via a defect or impurity state within the bandgap, known as a **recombination center** or **trap**. An electron is first captured by the trap, and then a hole is captured, completing the recombination. In indirect-gap semiconductors like silicon, SRH is typically the dominant lifetime-limiting mechanism at low to moderate carrier concentrations. The net recombination rate is given by the SRH formula:
    $$
    U_{\text{SRH}} = \frac{np - n_i^2}{\tau_p (n + n_1) + \tau_n (p + p_1)}
    $$
    where $\tau_n$ and $\tau_p$ are fundamental capture lifetimes related to the trap density $N_t$ and capture [cross-sections](@entry_id:168295) $\sigma_n, \sigma_p$. Under high injection conditions ($n=p \gg n_i$), the rate becomes approximately linear with carrier concentration, $U_{\text{SRH}} \approx n/(\tau_n+\tau_p)$.

2.  **Radiative Recombination**: This is the direct recombination of an electron and a hole, resulting in the emission of a photon. It is the inverse process of optical absorption. The rate is proportional to the product of the electron and hole concentrations: $U_{\text{rad}} = B(np - n_i^2)$, where $B$ is the [radiative recombination](@entry_id:181459) coefficient. This process is dominant in direct-gap materials but is relatively inefficient in silicon.

3.  **Auger Recombination**: This is a three-particle process. An electron and hole recombine, but instead of emitting a photon, the excess energy is transferred to another free carrier (either an electron or a hole), exciting it to a higher energy state. Since it requires three carriers to interact, its rate is strongly dependent on [carrier concentration](@entry_id:144718): $U_{\text{Auger}} = (C_n n + C_p p)(np - n_i^2)$, where $C_n$ and $C_p$ are the Auger coefficients.

The relative importance of these three mechanisms depends critically on the injection level. A comparison for silicon reveals a distinct hierarchy :
- At moderate injection levels, such as $n=p=10^{15} \, \text{cm}^{-3}$, SRH recombination is by far the dominant process.
- At very high injection levels, typical of the on-state of power devices, such as $n=p=10^{18} \, \text{cm}^{-3}$, the cubic dependence of Auger recombination causes it to become the dominant mechanism. Radiative recombination remains a minor contributor in silicon across all typical injection levels.

This transition from SRH to Auger dominance is a critical aspect of power device physics, as it makes the effective [carrier lifetime](@entry_id:269775) strongly dependent on the current density.

The **carrier lifetime**, $\tau$, is the average time an excess carrier exists before recombining. For [low-level injection](@entry_id:1127474) of minority holes into an n-type material, the hole lifetime $\tau_p$ is defined via the [recombination rate](@entry_id:203271) $U \approx \Delta p / \tau_p$. From the SRH formula, under [low-level injection](@entry_id:1127474) ($n_0 \gg p_0, \Delta p$) in n-type material, the minority hole lifetime simplifies to $\tau_p \approx \tau_{p0}$, a parameter directly related to the trap density and hole [capture cross-section](@entry_id:263537) .

In power devices, lifetime is a critical design parameter that is often intentionally controlled. This is known as **lifetime engineering**. A shorter lifetime allows for faster device switching but increases the on-state voltage drop, creating a fundamental trade-off. Lifetime can be reduced by introducing recombination centers. Common methods include diffusing metallic impurities like gold (Au) or platinum (Pt), or creating lattice defects through irradiation with high-energy particles like electrons or protons. Controlled electron [irradiation](@entry_id:913464) is often preferred as it creates defects that are efficient recombination centers (reducing lifetime) but have a relatively small impact on the generation rate in the off-state, thus minimizing increases in leakage current and preserving blocking capability .

### Advanced Topics in Carrier Behavior

The principles outlined above form the standard model of semiconductor physics. However, under the extreme conditions encountered in modern power devices—high fields, high current densities, and heavy doping—several non-ideal effects become important.

#### The Law of Mass Action and Quasi-Fermi Levels

The simple law of mass action, $np=n_i^2$, is strictly valid only in thermal equilibrium. When a device is under bias or illumination, it is in a **non-equilibrium steady state**. In many cases, we can still assume that the electron and hole populations are each internally in thermal equilibrium, but not with each other. This state is described by introducing separate electrochemical potentials for electrons and holes, known as **quasi-Fermi levels**, $E_{Fn}$ and $E_{Fp}$. The carrier concentrations are then given by:
$$
n = n_i \exp\left(\frac{E_{Fn} - E_i}{k_B T}\right), \quad p = n_i \exp\left(\frac{E_i - E_{Fp}}{k_B T}\right)
$$
The splitting of the quasi-Fermi levels, $E_{Fn} - E_{Fp}$, is a measure of the departure from equilibrium. Under these conditions, the $np$ product is no longer constant but is given by the generalized [mass action law](@entry_id:161309) :
$$
np = n_i^2 \exp\left(\frac{E_{Fn} - E_{Fp}}{k_B T}\right)
$$
This framework of quasi-Fermi levels is essential for analyzing p-n junctions under forward bias, bipolar transistors, and [optoelectronic devices](@entry_id:1129187). However, its validity is also limited. In regions of very high electric fields, carriers can gain energy from the field faster than they can lose it to the lattice via phonon emission. These **hot carriers** have an effective temperature greater than the lattice temperature, and their energy distribution is no longer a simple Fermi-Dirac function. In such cases, or under conditions of **impact ionization** (avalanche breakdown), the system is [far from equilibrium](@entry_id:195475), and the concept of quasi-Fermi levels and the generalized [mass action law](@entry_id:161309) break down .

#### Heavy Doping Effects: Bandgap Narrowing

In lightly [doped semiconductors](@entry_id:145553), dopant atoms are sufficiently far apart that they can be treated as isolated impurity states. However, in the heavily doped regions common in power device emitters and contact layers ($N > 10^{18} \, \text{cm}^{-3}$), this assumption fails. Two [main effects](@entry_id:169824) occur: the wavefunctions of neighboring dopant atoms overlap to form an **[impurity band](@entry_id:146742)**, and [many-body interactions](@entry_id:751663) (exchange and correlation) between the dense gas of free carriers modify the crystal potential.

The combined result of these phenomena is a reduction of the effective bandgap, an effect known as **bandgap narrowing (BGN)**, $\Delta E_g$. The effective bandgap becomes $E_{g, \text{eff}} = E_{g0} - \Delta E_g(N)$, where $E_{g0}$ is the intrinsic bandgap and the narrowing is a function of the dopant density $N$ .

Bandgap narrowing has significant consequences. A key effect is an increase in the [effective intrinsic carrier concentration](@entry_id:1124181), $n_{ie}$:
$$
n_{ie}^2(N) = n_{i0}^2 \exp\left(\frac{\Delta E_g(N)}{k_B T}\right)
$$
This increase in $n_{ie}$ directly impacts device characteristics. For example, in a $p^+$-$n^+$ junction, the built-in potential $V_{bi}$ is determined by the need to align the Fermi levels across the junction. BGN on both sides of the junction leads to a reduction in the [built-in potential](@entry_id:137446) compared to the ideal case. The magnitude of this reduction, $\delta V_{bi}$, is directly related to the average [bandgap narrowing](@entry_id:137814) on the two sides :
$$
\delta V_{bi} = \frac{\Delta E_g(N_D) + \Delta E_g(N_A)}{2q}
$$
For a silicon junction with [heavy doping](@entry_id:1125993) on both sides (e.g., $N_A \sim 5 \times 10^{19} \, \text{cm}^{-3}$ and $N_D \sim 1.5 \times 10^{20} \, \text{cm}^{-3}$), this reduction can be on the order of $0.1 \, \text{V}$, a significant fraction of the total [built-in potential](@entry_id:137446). Accurately modeling BGN is therefore crucial for the design and simulation of modern power devices.