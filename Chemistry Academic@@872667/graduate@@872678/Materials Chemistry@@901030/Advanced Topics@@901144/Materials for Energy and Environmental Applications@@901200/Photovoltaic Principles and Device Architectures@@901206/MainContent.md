## Introduction
The conversion of sunlight into electricity via photovoltaic devices stands as a cornerstone of modern sustainable energy strategies. Achieving high efficiency and long-term stability in [solar cells](@entry_id:138078), however, is a complex scientific and engineering challenge that demands a deep, integrated understanding of [materials chemistry](@entry_id:150195), [solid-state physics](@entry_id:142261), and device engineering. This article addresses the knowledge gap between fundamental concepts and their practical application by providing a comprehensive exploration of the principles that govern solar cell operation. It aims to equip the reader with the theoretical framework necessary to analyze, design, and innovate within the field of photovoltaics.

The journey begins with **Principles and Mechanisms**, where we will dissect the foundational physics of [solar energy conversion](@entry_id:199144). This chapter covers the initial absorption of light, the nature of [electronic excitations](@entry_id:190531) in different types of semiconductors, the dynamics of [charge carrier transport](@entry_id:267465) and recombination, and the critical role of interfaces and defects. Following this, **Applications and Interdisciplinary Connections** bridges theory and practice by examining how these core principles are implemented in diverse, real-world device architectures. We will explore materials from crystalline silicon to [halide perovskites](@entry_id:260767) and investigate advanced concepts like light management and multi-junction cells. Finally, **Hands-On Practices** provides a series of targeted problems designed to solidify your understanding of key quantitative relationships in photovoltaic device analysis.

## Principles and Mechanisms

The conversion of light into electricity in a photovoltaic device is a multi-step process governed by fundamental principles of [solid-state physics](@entry_id:142261), materials chemistry, and thermodynamics. Each step, from the initial absorption of a photon to the final collection of charge at the electrical contacts, involves specific mechanisms that determine the overall efficiency of the device. This chapter elucidates these core principles and mechanisms, building a foundational understanding of how [solar cells](@entry_id:138078) operate. We will explore the nature of [light absorption](@entry_id:147606) in different types of semiconductors, the dynamics of photogenerated charge carriers, the essential mechanism of charge separation that defines the [photovoltaic effect](@entry_id:161247), the critical role of interfaces and defects, and the key metrics used to quantify device performance.

### Light Absorption and Electronic Excitation

The initial and indispensable step in the photovoltaic process is the absorption of a photon by the semiconductor material. This event promotes an electron from a lower-energy state in the valence band to a higher-energy state in the conduction band, creating an electron-hole pair.

#### Bandgaps: Direct and Indirect Transitions

For absorption to occur, the energy of the incident photon ($E_{ph} = \hbar\omega$) must be at least equal to the **[bandgap energy](@entry_id:275931)** ($E_g$) of the semiconductor. The [bandgap](@entry_id:161980) is defined as the minimum energy difference between the top of the valence band (valence band maximum, VBM) and the bottom of the conduction band (conduction band minimum, CBM).

The nature of the [bandgap](@entry_id:161980) is critical to the absorption properties of a material. In solid-state physics, the energy of electrons is described as a function of their crystal momentum, $\mathbf{k}$, in what is known as the electronic band structure. Based on the alignment of the VBM and CBM in $\mathbf{k}$-space, semiconductors are classified as having either a direct or an [indirect bandgap](@entry_id:268921) [@problem_id:2510075].

-   A **[direct-gap semiconductor](@entry_id:191146)** is one in which the VBM and CBM occur at the same crystal momentum vector $\mathbf{k}$. When a photon is absorbed, an electron can be promoted vertically in the $E$-$\mathbf{k}$ diagram, conserving both energy and momentum (as the photon's momentum is negligible compared to that of electrons in the crystal). This is a highly probable, first-order process. According to Fermi's Golden Rule, the [absorption coefficient](@entry_id:156541) $\alpha(\hbar\omega)$ for an allowed direct transition in a three-dimensional material rises sharply above the band edge, typically following the relationship:
    $$ \alpha(\hbar\omega) \propto \sqrt{\hbar\omega - E_g} $$
    This strong absorption allows for the fabrication of very thin yet effective absorber layers, which is advantageous for many thin-film photovoltaic technologies.

-   An **indirect-gap semiconductor**, such as silicon, has its VBM and CBM at different values of $\mathbf{k}$. For an electron to be excited across the fundamental gap, it must undergo a change in both energy and momentum. Since the photon carries negligible momentum, the required momentum change must be supplied by the crystal lattice in the form of a phonon (a quantum of lattice vibration). The simultaneous involvement of a photon and a phonon makes this a second-order process, which is intrinsically much less probable than a direct transition. Consequently, the [absorption coefficient](@entry_id:156541) for an indirect-gap material is significantly weaker near the band edge and exhibits a more gradual onset. The absorption process can involve either the absorption or emission of a phonon, leading to thresholds slightly below or above $E_g$. The functional form for absorption involving a phonon of energy $\hbar\Omega$ is approximately:
    $$ \alpha(\hbar\omega) \propto (\hbar\omega - E_g \mp \hbar\Omega)^2 $$
    This weaker absorption necessitates the use of thicker absorber layers (e.g., hundreds of micrometers for silicon wafers) to capture a sufficient fraction of the solar spectrum.

#### Absorption in Disordered Materials: The Urbach Tail

In perfectly ordered crystals at zero temperature, no absorption should occur for photons with energy less than the [bandgap](@entry_id:161980). However, in real materials, particularly disordered ones like amorphous semiconductors or organic molecular films, a notable exponential tail of absorption extends into the sub-bandgap region. This feature is known as the **Urbach tail** [@problem_id:2510071].

The physical origin of the Urbach tail lies in disorder. Both **[static disorder](@entry_id:144184)** (e.g., variations in bond lengths and angles, defects, [grain boundaries](@entry_id:144275)) and **[dynamic disorder](@entry_id:187807)** (thermal vibrations of the lattice, or phonons) create local fluctuations in the [electrostatic potential](@entry_id:140313). These fluctuations effectively smear the sharp band edges of a perfect crystal, creating a [continuous distribution](@entry_id:261698) of "tail states" that extend into the forbidden gap. An optical transition can then occur at an energy $E  E_g$ if it takes place in a region where the local bandgap has been momentarily or permanently reduced to be less than or equal to $E$.

The probability of such a favorable fluctuation decreases exponentially with the required energy deviation from the mean [bandgap](@entry_id:161980). This leads to an absorption coefficient that follows the empirical Urbach rule:
$$ \alpha(E) = \alpha_0 \exp\left( \frac{E - E_0}{E_U} \right) $$
Here, $\alpha_0$ and $E_0$ are material-specific constants, and $E_U$ is the characteristic **Urbach energy**. The Urbach energy quantifies the degree of [energetic disorder](@entry_id:184846) in the material and is determined experimentally as the inverse slope of a plot of $\ln\alpha$ versus photon energy $E$. A larger $E_U$ signifies greater disorder and a more gradual absorption onset. Since [dynamic disorder](@entry_id:187807) is temperature-dependent, $E_U$ typically increases with temperature.

#### Fundamental Energy Levels

To discuss the energetics of interfaces, it is crucial to define the absolute energy levels of a material with respect to a common reference, the [vacuum level](@entry_id:756402) ($E_{\mathrm{vac}}$). The key parameters are [@problem_id:2510064]:

-   **Ionization Energy ($I$)**: The minimum energy required to remove an electron from the solid (from the highest occupied molecular orbital, HOMO, or VBM) to the vacuum. It is given by $I = E_{\mathrm{vac}} - E_{\mathrm{HOMO}}$.
-   **Electron Affinity ($A$)**: The energy released when an electron is added from the vacuum to the solid (into the lowest unoccupied molecular orbital, LUMO, or CBM). It is given by $A = E_{\mathrm{vac}} - E_{\mathrm{LUMO}}$.
-   **Work Function ($\Phi$)**: The minimum energy required to remove an electron from the Fermi level ($E_F$) of the material to the vacuum. It is given by $\Phi = E_{\mathrm{vac}} - E_F$. The [work function](@entry_id:143004) depends on the material's [doping](@entry_id:137890), as $E_F$ shifts within the [bandgap](@entry_id:161980).

In disordered [organic semiconductors](@entry_id:186271), the HOMO and LUMO levels are not sharp edges but rather broad distributions of states, often modeled as Gaussians. Charge transport in these materials occurs by hopping between [localized states](@entry_id:137880). Due to the interplay between the density of available states and the thermal energy for activation, charge carriers tend to move through a narrow band of energies known as the **transport energy**, which can be significantly shifted from the center of the Gaussian density of states. For example, in an n-type organic material with a Gaussian LUMO distribution of width $\sigma$, the electron transport energy lies approximately $\sigma^2/(k_B T)$ below the center of the LUMO band [@problem_id:2510064]. This distinction between thermodynamic band edges (related to $I$ and $A$) and kinetic transport levels is critical for accurately modeling charge injection and transport in organic devices.

### Carrier Dynamics: Transport, Recombination, and Collection

Following photogeneration, the electron and hole must be separated and transported to their respective contacts to produce an external current. During their journey, they are subject to various scattering and recombination processes. The interplay between these dynamics governs the efficiency of charge collection.

#### Drift and Diffusion Currents

The motion of charge carriers in a semiconductor is governed by two principal mechanisms [@problem_id:2510114]:

1.  **Drift**: The movement of charged particles in response to an electric field ($E$). The drift velocity is proportional to the field, with the proportionality constant being the mobility ($\mu$). The resulting drift current density for electrons ($J_{n, \text{drift}}$) and holes ($J_{p, \text{drift}}$) is given by:
    $$ J_{n, \text{drift}} = q \mu_n n E $$
    $$ J_{p, \text{drift}} = q \mu_p p E $$
    Here, $q$ is the [elementary charge](@entry_id:272261), and $n$ and $p$ are the electron and hole concentrations, respectively. Note that although electrons have a negative charge and drift in the opposite direction to the field, the convention for electrical current results in the electron drift current being in the same direction as the hole drift current for a given field.

2.  **Diffusion**: The net movement of particles from a region of higher concentration to a region of lower concentration. This process is driven by the concentration gradient ($\nabla n$ or $\nabla p$) and is described by Fick's first law. The resulting diffusion current density is:
    $$ J_{n, \text{diff}} = q D_n \frac{dn}{dx} $$
    $$ J_{p, \text{diff}} = -q D_p \frac{dp}{dx} $$
    Here, $D_n$ and $D_p$ are the diffusion coefficients for electrons and holes. The signs reflect that electrons (negative charge) diffusing down their [concentration gradient](@entry_id:136633) and holes (positive charge) diffusing down their gradient produce currents in opposite directions.

The total current density for each carrier is the sum of its drift and diffusion components:
$$ J_n(x) = q \mu_n n(x) E(x) + q D_n \frac{dn}{dx} $$
$$ J_p(x) = q \mu_p p(x) E(x) - q D_p \frac{dp}{dx} $$

#### The Continuity Equation

The principle of charge conservation is expressed by the **continuity equation**. It states that the rate of change of [carrier concentration](@entry_id:144718) in a small volume is determined by the net flow of carriers into that volume (the divergence of the current) plus the net rate of [carrier generation](@entry_id:263590) within that volume. In steady state, the carrier concentrations do not change with time, so the net rate of change is zero. This implies that the rate at which carriers enter a region must be balanced by the rate at which they leave or are generated/recombined within it.

Let $G(x)$ be the volumetric generation rate of electron-hole pairs (due to light) and $R(n,p)$ be the net [recombination rate](@entry_id:203271). The steady-state continuity equations for [electrons and holes](@entry_id:274534) are [@problem_id:2510114]:
$$ \frac{1}{q}\frac{dJ_n}{dx} = G(x) - R(n,p) $$
$$ -\frac{1}{q}\frac{dJ_p}{dx} = G(x) - R(n,p) $$
These equations, coupled with the drift-diffusion and Poisson's equation (which relates the electric field to the [charge distribution](@entry_id:144400)), form the fundamental set of semiconductor device equations used to model and simulate photovoltaic cells.

#### Recombination Mechanisms

Recombination, the annihilation of an electron-hole pair, is the primary loss mechanism that competes with charge collection. It releases the energy gained during absorption, typically as light (radiative) or heat (nonradiative). The three main bulk recombination mechanisms are distinguished by their dependence on carrier concentrations [@problem_id:2510119].

-   **Radiative (Band-to-Band) Recombination**: An electron in the conduction band directly recombines with a hole in the [valence band](@entry_id:158227), emitting a photon with energy close to the [bandgap](@entry_id:161980). The net rate, $R_{\mathrm{rad}}$, is proportional to the product of the electron and hole concentrations minus the [thermal generation](@entry_id:265287) rate: $R_{\mathrm{rad}} = B(np - n_i^2)$, where $B$ is the radiative coefficient and $n_i$ is the [intrinsic carrier concentration](@entry_id:144530).
    -   Under **low injection** in an n-type material ($n \approx n_0 \gg p_0, \Delta n, \Delta p$), the rate is limited by the minority carrier (hole) concentration: $R_{\mathrm{rad}} \propto n_0 \Delta p$.
    -   Under **high injection** ($n \approx p \approx \Delta n \gg n_0, p_0$), the rate is a bimolecular process: $R_{\mathrm{rad}} \propto (\Delta n)^2$.

-   **Shockley–Read–Hall (SRH) Recombination**: This is a nonradiative process that occurs via an intermediate energy state, or "trap," within the bandgap, typically associated with a point defect or impurity. The process involves two steps: capture of one carrier, followed by capture of the opposite carrier. The rate is complex, but in many practical cases it simplifies.
    -   Under **low injection** in an n-type material, the rate-limiting step is the capture of the scarce minority holes by the traps. The net rate scales linearly with the excess minority carrier concentration: $R_{\mathrm{SRH}} \propto \Delta p$.
    -   Under **high injection**, the rate becomes limited by the capture process itself and scales linearly with the total excess carrier concentration: $R_{\mathrm{SRH}} \propto \Delta n$.

-   **Auger Recombination**: This is a three-particle nonradiative process. The energy from an [electron-hole recombination](@entry_id:187424) is transferred to a third carrier (either an electron or a hole), which is excited to a higher energy state and subsequently relaxes by emitting phonons (heat). The net rate depends on the product of three carrier concentrations: $R_{\mathrm{Aug}} = (C_n n + C_p p)(np - n_i^2)$, where $C_n$ and $C_p$ are the Auger coefficients.
    -   Under **low injection** in an n-type material, the dominant process involves two majority carriers (electrons) and one minority carrier (hole), so the rate scales as $R_{\mathrm{Aug}} \propto n_0^2 \Delta p$.
    -   Under **high injection**, the rate involves three excess carriers and scales cubically with the excess carrier concentration: $R_{\mathrm{Aug}} \propto (\Delta n)^3$.

The relative importance of these mechanisms depends on the material quality (defect density for SRH), injection level, and intrinsic material properties. In high-quality direct-gap semiconductors at high injection, [radiative recombination](@entry_id:181459) can dominate, while in indirect-gap semiconductors like silicon, SRH and Auger recombination are typically the [limiting factors](@entry_id:196713).

### The Photovoltaic Effect: Harnessing Photogenerated Charge

Generating electron-hole pairs is not sufficient to produce electricity. A mechanism must exist to separate these charges and drive them through an external circuit. This is the essence of the [photovoltaic effect](@entry_id:161247), which is fundamentally distinct from the related photoconductive effect.

A **photoconductor** is a symmetric piece of semiconductor with identical ohmic contacts. Illumination increases its conductivity by creating more free carriers. However, with no internal asymmetry, there is no preferential direction for charge flow. Without an external applied voltage, there is no net current and no terminal voltage; it cannot generate power [@problem_id:2510048].

A **photovoltaic device**, in contrast, possesses an intrinsic asymmetry that creates a **built-in electric field**. This asymmetry can be a p-n junction, a Schottky barrier ([metal-semiconductor junction](@entry_id:273369)), or a [heterojunction](@entry_id:196407) (interface between two different semiconductors). This built-in field acts to separate photogenerated electron-hole pairs: it sweeps electrons to one side and holes to the other.

This separation of charge leads to an accumulation of electrons at the n-type terminal and holes at the p-type terminal, establishing a [potential difference](@entry_id:275724) across the device. This voltage is the **photovoltage**. Under open-circuit conditions (no current flowing), this voltage reaches its maximum value, the **[open-circuit voltage](@entry_id:270130) ($V_{oc}$)**. If the terminals are connected to an external load, the separated charges can drive a current, the **[photocurrent](@entry_id:272634)**, delivering [electrical power](@entry_id:273774) to the load.

From a thermodynamic perspective, illumination drives the system out of equilibrium. The steady-state population of excess carriers is described by separate **quasi-Fermi levels** for electrons ($F_n$) and holes ($F_p$). In the dark, at equilibrium, $F_n = F_p$. Under illumination, $F_n$ is higher in energy than $F_p$, and the magnitude of this splitting, $F_n - F_p$, represents the free energy available from the absorbed photons. The built-in field of a photovoltaic device allows this internal chemical potential difference to be expressed as an external [electrical potential](@entry_id:272157). At open circuit, the measurable voltage across the device is a direct reflection of this quasi-Fermi level splitting:
$$ q V_{oc} = (F_n - F_p)_{\text{junction}} $$
In a symmetric photoconductor, while local quasi-Fermi level splitting also occurs, the symmetry of the device and contacts prevents this splitting from manifesting as a net terminal voltage [@problem_id:2510048].

### The Critical Role of Interfaces and Defects

The performance of a photovoltaic device is critically dependent on the quality of its interfaces and the nature of defects within the bulk material.

#### Metal-Semiconductor Contacts and Fermi Level Pinning

Electrical contacts are required to extract the photogenerated current. An ideal "ohmic" contact should present negligible resistance to current flow. However, the interface between a metal and a semiconductor often forms a rectifying Schottky barrier. According to the ideal **Schottky-Mott rule**, the electron barrier height ($\Phi_{Bn}$) should be the difference between the metal [work function](@entry_id:143004) ($\Phi_M$) and the semiconductor [electron affinity](@entry_id:147520) ($\chi$): $\Phi_{Bn} = \Phi_M - \chi$.

In practice, this rule often fails because of [electronic states](@entry_id:171776) present at the semiconductor surface. A high density of these interface states ($D_{it}$) can lead to **Fermi-level pinning** [@problem_id:2510057]. These states can trap charge, creating an interfacial dipole layer that accommodates the [work function](@entry_id:143004) difference. If $D_{it}$ is sufficiently large, the Fermi level at the interface becomes "pinned" near a [specific energy](@entry_id:271007) level characteristic of the semiconductor surface, known as the **charge neutrality level ($E_{CNL}$)**. In this strong pinning limit, the Schottky barrier height becomes largely independent of the metal [work function](@entry_id:143004) and is instead determined by the properties of the semiconductor's surface:
$$ \Phi_{Bn} \approx \Phi_{CNL} - \chi $$
For example, for typical high-$D_{it}$ silicon surfaces ($\chi \approx 4.05$ eV, $\Phi_{CNL} \approx 4.70$ eV), the barrier height is pinned at approximately $0.65$ eV, regardless of whether a low [work function](@entry_id:143004) metal like aluminum or a high [work function](@entry_id:143004) metal like platinum is used [@problem_id:2510057].

This phenomenon has profound practical consequences. To create low-resistance contacts, one can either:
1.  **Passivate the surface**: Use chemical treatments to reduce the density of interface states ($D_{it}$), thereby "unpinning" the Fermi level and restoring the dependence of the barrier height on the metal work function.
2.  **Use heavy doping**: By heavily doping the semiconductor region beneath the contact (e.g., $N_D > 10^{18}$ cm$^{-3}$), the depletion width of the Schottky barrier becomes extremely narrow. This allows carriers to tunnel through the barrier via thermionic-[field emission](@entry_id:137036), dramatically reducing the [contact resistance](@entry_id:142898) even in the presence of a significant barrier height [@problem_id:2510057].

#### Donor-Acceptor Heterojunctions

In many thin-film technologies, such as organic photovoltaics (OPVs), the primary charge separation occurs at a [heterojunction](@entry_id:196407) between an electron-donating material and an electron-accepting material. In these systems, [light absorption](@entry_id:147606) typically creates a tightly bound [electron-hole pair](@entry_id:142506) called an **[exciton](@entry_id:145621)**. This [exciton](@entry_id:145621) must diffuse to the donor-acceptor (D/A) interface, where it can dissociate into free charges.

The efficiency of this process involves a critical trade-off [@problem_id:2510091]. The dissociation is driven by an energetic offset, $\Delta E$, between the exciton energy and the energy of the separated [charge-transfer](@entry_id:155270) (CT) state at the interface. A larger $\Delta E$ increases the rate of charge transfer, improving the charge separation yield. However, the energy of the CT state, $E_{CT}$, sets the upper limit for the device's [open-circuit voltage](@entry_id:270130) ($qV_{oc} \lesssim E_{CT}$). Since $\Delta E$ is defined as the energy *lost* in going from the [exciton](@entry_id:145621) to the CT state, a large driving force inherently lowers $E_{CT}$ and thus reduces the maximum achievable $V_{oc}$.

Optimizing an OPV material system therefore requires finding the minimum driving force $\Delta E$ that is still sufficient to ensure that charge transfer is much faster than competing [exciton](@entry_id:145621) decay processes. This analysis requires kinetic models, such as Marcus theory, which relate the charge transfer rate to the driving force, the reorganization energy ($\lambda$), and temperature. The goal is to operate in a regime where the charge separation yield is near unity while sacrificing the minimum possible energy, thereby maximizing the voltage output [@problem_id:2510091].

#### Point Defects and Formation Energy

Point defects, such as vacancies, [interstitials](@entry_id:139646), and antisites, can act as powerful SRH recombination centers, severely limiting device efficiency. Understanding and controlling their concentration is a central challenge in materials science for photovoltaics.

The equilibrium concentration of a given defect is determined by its **formation energy ($E_f$)**. This is the thermodynamic energy cost to create the defect. Using first-principles computational methods, the formation energy of a defect $D$ with charge state $q$ can be calculated as [@problem_id:2510087]:
$$ E_f(D^q; E_F, \{\mu_i\}) = \left[ E_{\text{tot}}(D^q) - E_{\text{tot}}(\text{bulk}) \right] - \sum_i n_i \mu_i + q E_F + E_{\text{corr}} $$
This equation reveals several key dependencies:
-   $E_{\text{tot}}(D^q)$ and $E_{\text{tot}}(\text{bulk})$ are the total energies of supercells with and without the defect.
-   The term $\sum_i n_i \mu_i$ accounts for the atoms exchanged with the environment, where $\mu_i$ are the atomic chemical potentials that describe the growth conditions (e.g., element-rich or element-poor).
-   The term $qE_F$ describes the energy cost of exchanging charge with the electron reservoir, where $E_F$ is the Fermi level. This shows that the formation energy of a charged defect is not constant but depends linearly on the Fermi level position. The slope of $E_f$ versus $E_F$ is the charge state $q$. This explains why donor defects ($q>0$) are easier to form in p-type material (low $E_F$) and acceptor defects ($q0$) are easier to form in n-type material (high $E_F$).
-   $E_{\text{corr}}$ represents necessary corrections for finite-size electrostatic artifacts in supercell calculations.

By calculating formation energies, researchers can predict which defects are most likely to form under given synthesis conditions and how their concentrations might be controlled through [doping](@entry_id:137890) or tuning the chemical environment.

### Device Performance Metrics

To evaluate and compare photovoltaic devices, a standardized set of performance metrics is used. These metrics quantify how efficiently a device converts photons of a [specific energy](@entry_id:271007) into collected electrons.

-   **Spectral Responsivity ($R_s$)**: Defined as the ratio of the short-circuit [photocurrent](@entry_id:272634) generated ($I_{sc}$) to the incident [optical power](@entry_id:170412) ($P_{inc}$) at a specific wavelength $\lambda$. It is typically measured in amperes per watt (A/W).
    $$ R_s(\lambda) = \frac{I_{sc}(\lambda)}{P_{inc}(\lambda)} $$

-   **External Quantum Efficiency (EQE)**: A dimensionless quantity representing the ratio of the number of charge carriers collected by the [solar cell](@entry_id:159733) to the number of *incident* photons of a given energy.
    $$ \mathrm{EQE}(\lambda) = \frac{\text{Collected electrons per second}}{\text{Incident photons per second}} = \frac{I_{sc}(\lambda)/q}{P_{inc}(\lambda)/(hc/\lambda)} = R_s(\lambda) \frac{hc}{q\lambda} $$
    EQE accounts for all loss mechanisms: photons that are reflected or transmitted without being absorbed, and electron-hole pairs that are created but then recombine before being collected [@problem_id:2510110].

-   **Internal Quantum Efficiency (IQE)**: Represents the ratio of the number of charge carriers collected to the number of photons *absorbed* by the device.
    $$ \mathrm{IQE}(\lambda) = \frac{\text{Collected electrons per second}}{\text{Absorbed photons per second}} $$
    IQE specifically measures the efficiency of charge collection once a photon has been successfully absorbed. It is therefore a probe of recombination losses within the device. The relationship between IQE and EQE is given by:
    $$ \mathrm{EQE}(\lambda) = \mathrm{IQE}(\lambda) \times (1 - R(\lambda) - T(\lambda)) $$
    where $R(\lambda)$ and $T(\lambda)$ are the fractions of light reflected and transmitted, respectively. By measuring EQE and the optical properties (R and T), one can calculate IQE and thereby distinguish between optical losses (imperfect absorption) and electronic losses (recombination). For instance, if a device has an EQE of $0.40$ at a wavelength where reflectance is $0.20$ and [transmittance](@entry_id:168546) is negligible, its IQE is $0.40 / (1 - 0.20) = 0.50$. This indicates that while 40% of incident photons produce collected electrons, 50% of *absorbed* photons do, with the difference being due to reflection losses [@problem_id:2510110].