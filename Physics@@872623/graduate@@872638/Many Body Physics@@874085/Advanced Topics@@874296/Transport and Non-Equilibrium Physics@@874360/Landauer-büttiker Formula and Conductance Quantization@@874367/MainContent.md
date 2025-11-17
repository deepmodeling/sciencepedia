## Introduction
The way electrons travel through small-scale conductors is fundamentally different from their flow in bulk materials, rendering classical concepts like Ohm's law inadequate. At the mesoscopic scale—the bridge between the microscopic quantum world and our macroscopic classical world—a new perspective is needed. The Landauer-Büttiker formalism provides this perspective, representing a paradigm shift by recasting electrical and [thermal transport](@entry_id:198424) as a quantum mechanical scattering problem. It addresses the crucial gap in understanding how conductance arises from the wave-like nature of electrons and their transmission through a device. This article serves as a graduate-level guide to this powerful framework. The reader will first delve into the foundational concepts in "Principles and Mechanisms," exploring how the simple idea of transmission probability leads to profound consequences like [conductance quantization](@entry_id:144928). Following this, "Applications and Interdisciplinary Connections" will demonstrate the formalism's vast utility in explaining phenomena in spintronics, topological materials, and superconductivity. Finally, "Hands-On Practices" will offer practical exercises to solidify this theoretical knowledge, beginning with an exploration of the core tenets of the formalism.

## Principles and Mechanisms

The Landauer-Büttiker formalism represents a paradigm shift in the understanding of electrical and [thermal transport](@entry_id:198424) in [mesoscopic systems](@entry_id:183911). Moving away from the classical, macroscopic concepts of [resistivity](@entry_id:266481) and Ohm's law, this framework recasts transport as a quantum mechanical scattering problem. It posits that conductance is not an intrinsic property of a material but is instead determined by the quantum mechanical transmission probability of electrons through a conductor. This chapter delineates the foundational principles and key mechanisms of this powerful approach, starting from the basic two-terminal conductance and extending to multi-terminal networks, quantum interference, current fluctuations, and thermoelectric phenomena.

### The Landauer Formula: Conductance from Transmission

The central tenet of the Landauer formalism is that the [electrical conductance](@entry_id:261932) of a sample is fundamentally linked to its ability to transmit electrons. Imagine a conductor connected between two large electron reservoirs, termed the source and the drain, held at electrochemical potentials $\mu_L$ and $\mu_R$ respectively. At zero temperature, a small voltage bias $V = (\mu_L - \mu_R)/e$ creates a current $I$. Landauer's insight was to express the resulting conductance, $G = I/V$, in terms of the quantum mechanical scattering properties of the conductor itself.

For a single-channel conductor, where electrons can propagate in only one transverse mode, the conductance is given by the remarkably simple Landauer formula:

$$
G = \frac{e^2}{h} T
$$

Here, $e$ is the elementary charge, $h$ is Planck's constant, and $T$ is the total [transmission probability](@entry_id:137943) for an electron at the Fermi energy to travel from the source to the drain. The quantity $G_q = e^2/h$ is the **[quantum of conductance](@entry_id:753947)**, with a value of approximately $38.74 \, \mu\text{S}$. The inverse, $R_q = h/e^2 \approx 25.812 \, \text{k}\Omega$, is known as the von Klitzing constant. It is important to note that throughout this chapter, we will often incorporate spin degeneracy by using a [conductance quantum](@entry_id:200956) of $G_0 = 2e^2/h$, which applies when both spin-up and spin-down electrons contribute equally and independently to transport.

In a realistic conductor, transport may occur through multiple parallel channels or modes. Each channel, labeled by an index $n$, has its own transmission probability $T_n$. These probabilities are the eigenvalues of the matrix product $t^\dagger t$, where $t$ is the transmission matrix block of the full [scattering matrix](@entry_id:137017) that connects incoming states in the source lead to outgoing states in the drain lead. The total conductance is the sum of the contributions from all channels:

$$
G = \frac{e^2}{h} \sum_n T_n = \frac{e^2}{h} \mathrm{Tr}(t^\dagger t)
$$

This summation over channels is a key feature of the formalism, treating each channel as an independent conductor in parallel. For instance, consider a two-terminal [quantum wire](@entry_id:140839) supporting two spin-polarized [transverse modes](@entry_id:163265). If the scattering within the wire mixes these modes, the total conductance is still found by summing the individual transmission probabilities for each mode [@problem_id:1162380]. If the scattering matrices for mode 1 and mode 2 are given by $S_1$ and $S_2$, the transmission probabilities are $|t_1|^2$ and $|t_2|^2$, where $t_1$ and $t_2$ are the off-diagonal elements of $S_1$ and $S_2$ that describe transmission from left to right. The total conductance is simply $G = (e^2/h)(|t_1|^2 + |t_2|^2)$.

A profound consequence of this formalism is the phenomenon of **[conductance quantization](@entry_id:144928)**. In a clean, ballistic conductor, where electrons travel without scattering, the [transmission probability](@entry_id:137943) for a channel is either 1 (if the channel is open for propagation) or 0 (if it is closed). A channel is "open" if the electron's energy is above the minimum energy of the corresponding transverse subband. In devices like a **Quantum Point Contact (QPC)**, the number of open channels can be controlled by an external gate voltage, which varies the width of the constriction. As the gate voltage is made less negative, the constriction widens, and successive subbands drop below the Fermi energy, opening new channels for transport. Each time a new spin-degenerate channel opens, the conductance ideally jumps by a step of $G_0 = 2e^2/h$.

This quantization can be further manipulated. If a magnetic field is applied parallel to the direction of transport in a QPC, it does not affect the orbital motion but lifts the spin degeneracy via the Zeeman effect. The energy of the spin-up and spin-down subbands shifts by $\mp\frac{1}{2} g \mu_B B$. If the Fermi energy $E_F$ is initially just slightly above a spin-degenerate subband, applying a magnetic field will raise the energy of the spin-down channel. At a critical field $B_c$, the bottom of this spin-down band will be pushed above $E_F$, closing the channel. At this point, only the spin-up channel remains conductive, and the conductance drops from $2e^2/h$ to $e^2/h$, i.e., it is halved [@problem_id:1162374]. This demonstrates the ability to control individual [quantum channels](@entry_id:145403).

### The Microscopic Origin of Transmission

While the Landauer formula provides a powerful conceptual link between scattering and conductance, a full understanding requires a microscopic theory for the transmission probability $T(E)$ itself. The **Non-Equilibrium Green's Function (NEGF)** formalism provides such a framework.

In this approach, the system is partitioned into a central device region (the scatterer) and the semi-infinite leads that connect to it. The effect of the leads on the device is entirely captured by a complex, energy-dependent quantity known as the **[self-energy](@entry_id:145608)**, $\Sigma(E)$. The retarded self-energy, $\Sigma^r(E)$, has a real part that shifts the energy levels of the device and an imaginary part that broadens them, reflecting the fact that electrons can escape from the device into the leads. The rate of escape into lead $\alpha$ is described by the broadening function $\Gamma_\alpha(E) = i(\Sigma^r_\alpha(E) - \Sigma^a_\alpha(E))$, where $\Sigma^a_\alpha = (\Sigma^r_\alpha)^\dagger$ is the advanced self-energy.

Within the NEGF framework, the transmission probability from a lead $L$ to a lead $R$ is given by the Fisher-Lee relation:

$$
T(E) = \mathrm{Tr}[\Gamma_L(E) G^r(E) \Gamma_R(E) G^a(E)]
$$

Here, $G^r(E)$ and $G^a(E)$ are the retarded and advanced Green's functions of the device region, which incorporate the influence of all leads. The retarded Green's function is given by $G^r(E) = [ (E+i\eta)I - H_D - \sum_\alpha \Sigma^r_\alpha(E) ]^{-1}$, where $H_D$ is the Hamiltonian of the isolated device and $\eta$ is an infinitesimal positive quantity.

A concrete example illustrates this formalism [@problem_id:1162404]. Consider a finite one-dimensional [tight-binding](@entry_id:142573) chain of $N$ sites serving as the device, connected seamlessly to identical semi-infinite leads. This means the on-site energies and hopping integrals are uniform throughout the entire system. For an electron with energy $E=0$ (the center of the band in this model), the NEGF calculation reveals that the [transmission probability](@entry_id:137943) $T(0)=1$, regardless of the length $N$ of the chain. This confirms our intuition: a perfectly ordered system without any structural defects should not scatter electrons at this specific energy, leading to perfect transmission. The formalism provides a rigorous mathematical basis for this physical picture.

### Quantum Interference and Mesoscopic Effects

The wave nature of electrons is central to transport in [mesoscopic systems](@entry_id:183911), leading to a host of interference phenomena that have no classical analogue.

#### The Aharonov-Bohm Effect

The **Aharonov-Bohm (AB) effect** is a quintessential demonstration of quantum interference. In a ring-like geometry, an electron wave can be split, traverse two different paths (the arms of the ring), and recombine. The total transmission amplitude is the coherent sum of the amplitudes for each path. If a magnetic flux $\Phi$ threads the loop, it introduces a relative [phase difference](@entry_id:270122) between the two paths, even if the magnetic field is zero along the paths themselves. This phase is $\Delta\phi = e\oint \mathbf{A} \cdot d\mathbf{l} / \hbar = 2\pi\Phi/\Phi_0$, where $\Phi_0 = h/e$ is the [magnetic flux quantum](@entry_id:136429).

As a result, the total [transmission probability](@entry_id:137943) $T$, and thus the conductance $G$, oscillates as a function of the magnetic flux. The total transmission amplitude for a symmetric ring can be written as $t_{tot} \propto (t_1 e^{i\pi\Phi/\Phi_0} + t_2 e^{-i\pi\Phi/\Phi_0})$, where $t_1$ and $t_2$ are the intrinsic transmission amplitudes of the two arms. The resulting conductance exhibits oscillations with a period of $\Phi_0$ [@problem_id:1162389].

#### Fabry-Pérot Interference

Interference can also arise from multiple reflections within a cavity. A one-dimensional wire with two potential barriers forms an electronic **Fabry-Pérot interferometer**. An electron incident on the structure undergoes a series of reflections between the two barriers. The multiply-reflected waves interfere, leading to sharp resonances in the transmission probability $T(E)$ at energies where the interference is constructive. The [transmission probability](@entry_id:137943) is given by an Airy-like distribution. When experiments are performed at temperatures or voltage biases large compared to the energy spacing of these resonances, one measures an energy-averaged conductance. This averaging procedure shows that the effective resistance of the two barriers is not simply the sum of their individual resistances. Instead, the average transmission is given by $\langle T \rangle = T_1 T_2 / (1 - R_1 R_2) = T_1 T_2 / (T_1 + T_2 - T_1 T_2)$, where $T_i$ and $R_i=1-T_i$ are the transmission and reflection probabilities of the individual barriers [@problem_id:1162408]. This result can be interpreted as the series addition of resistances, but in a way that respects the coherent nature of the underlying transport.

#### Weak Localization

Quantum interference can also increase the resistance of a disordered conductor compared to its classical value. This phenomenon, known as **weak localization**, arises from the [constructive interference](@entry_id:276464) between a path and its exact time-reversed counterpart. An electron can follow a closed loop-like path and return to its starting point. In the absence of a magnetic field (which preserves [time-reversal symmetry](@entry_id:138094)), the amplitude for traversing this loop clockwise is exactly equal to the amplitude for traversing it counter-clockwise. These two paths interfere constructively, enhancing the probability that the electron returns to its origin. This enhanced [backscattering](@entry_id:142561) probability reduces the overall transmission and increases the measured resistance.

In an Aharonov-Bohm ring with a weak scatterer, this effect manifests as a negative correction to the classical conductance. Applying a magnetic flux breaks time-reversal symmetry, destroys the constructive interference, and thus suppresses weak localization. By averaging the conductance over one flux quantum, one can isolate the [weak localization](@entry_id:146052) correction, which is found to be negative and proportional to the square of the reflection probability of the scatterer for weak scattering [@problem_id:1162398].

### The Landauer-Büttiker Formalism: Multi-Terminal Devices

The Landauer formalism can be generalized to describe conductors with more than two terminals. This multi-terminal **Landauer-Büttiker formalism** is one of the most significant achievements of [mesoscopic physics](@entry_id:138415). For a device with $N$ terminals, each held at a voltage $V_i$, the net current flowing out of terminal $i$ is given by:

$$
I_i = \frac{2e^2}{h} \sum_{j=1, j \neq i}^{N} \left( T_{ji} V_i - T_{ij} V_j \right)
$$

where $T_{ij}$ is the total transmission probability from terminal $j$ to terminal $i$. In the absence of a magnetic field, time-reversal symmetry implies that the [scattering matrix](@entry_id:137017) is symmetric, which leads to the [reciprocity relation](@entry_id:198404) $T_{ij} = T_{ji}$. The formula then simplifies to:

$$
I_i = \frac{2e^2}{h} \sum_{j=1, j \neq i}^{N} T_{ij} (V_i - V_j)
$$

This set of [linear equations](@entry_id:151487) relates all currents to all voltages, defining a complete resistance matrix for the device.

#### Non-Local Resistance and Symmetry

The Landauer-Büttiker formalism predicts fascinating non-local effects. Consider a four-terminal measurement on a symmetric H-shaped conductor, where current $I$ is passed between terminals 1 and 2 on the left, and the voltage difference $V_3 - V_4$ is measured between terminals 3 and 4 on the right, which draw no current. The non-local resistance is defined as $R_{12,34} = (V_3 - V_4)/I$. Due to the spatial symmetry of the H-structure, the transmission probabilities obey certain relations (e.g., $T_{13} = T_{24}$ and $T_{14} = T_{23}$). Applying the Landauer-Büttiker equations with the conditions $I_3 = I_4 = 0$ reveals that the symmetry forces the voltages to be equal, $V_3 = V_4$. Consequently, the non-local resistance is exactly zero [@problem_id:1162397]. This result is a direct consequence of coherent, [ballistic transport](@entry_id:141251) and the symmetry of the scatterer.

#### The Büttiker Voltage Probe and Dephasing

A crucial conceptual tool introduced by Büttiker is the idea of a **voltage probe** to model [dephasing](@entry_id:146545). In a real conductor, electrons can undergo inelastic scattering events (e.g., with phonons or other electrons) that destroy their [phase coherence](@entry_id:142586). Such a process can be modeled by attaching a fictitious terminal to the conductor. This terminal is a conceptual reservoir that absorbs an electron and re-emits it with a randomized phase, effectively breaking the coherent evolution. This probe is defined to be "floating," meaning it is not connected to any external circuitry and thus draws zero net current. Its electrochemical potential adjusts itself to satisfy this condition.

Attaching a voltage probe between two scattering elements in a wire effectively turns a single coherent conductor into two incoherent conductors in series. For example, if a single scatterer with transmission $T_0$ is followed by a dephasing probe and then a perfect wire segment, the system behaves like two resistors in series. The effective two-terminal conductance is no longer simply $G_0 T_0$, but is reduced. A calculation using the three-terminal Landauer-Büttiker equations shows the effective conductance becomes $G_{eff} = G_0 \frac{T_0}{T_0+1}$ [@problem_id:1162435]. This demonstrates how decoherence degrades conductance.

#### Quantum Analogues of Classical Circuits

The Landauer-Büttiker formalism allows for the design and analysis of quantum analogues of classical circuit elements. A **quantum Wheatstone bridge** can be constructed from four quantum conductors connecting four terminals. A voltage is applied between two opposite terminals (e.g., 1 and 3), and the other two terminals (2 and 4) act as voltage probes. The bridge is "balanced" if the potentials on these probes are equal, $\mu_2 = \mu_4$. By applying the zero-current condition at probes 2 and 4, one can derive a balance condition. For a bridge with arm transmission probabilities $\mathcal{T}_a, \mathcal{T}_b, \mathcal{T}_c, \mathcal{T}_d$, the balance condition is found to be $\mathcal{T}_a / \mathcal{T}_c = \mathcal{T}_b / \mathcal{T}_d$, or $\mathcal{T}_a \mathcal{T}_d = \mathcal{T}_b \mathcal{T}_c$ [@problem_id:1162428]. This is a direct quantum analogue of the condition for a classical Wheatstone bridge, with transmission probabilities playing the role of conductances (or inverse resistances).

### Beyond Average Current: Fluctuations and Full Counting Statistics

While conductance describes the average current flow, the discrete nature of charge carriers leads to temporal fluctuations in the current, known as noise. The Landauer-Büttiker framework provides a comprehensive theory not just for the mean current, but for its entire statistical distribution.

#### Shot Noise

At zero temperature, the primary source of noise in a mesoscopic conductor under a voltage bias is **shot noise**. It originates from the random, probabilistic nature of electron transmission. Each electron arriving at the scatterer acts like a coin toss: it is either transmitted with probability $T$ or reflected with probability $R=1-T$. This random partitioning of the electron stream leads to fluctuations in the current.

The zero-frequency shot [noise power spectral density](@entry_id:274939), $S_I(0)$, for a multi-channel conductor is given by:
$$
S_I(0) = \frac{4e^3|V|}{h} \sum_n T_n(1-T_n)
$$
The factor $T_n(1-T_n)$ is crucial. It shows that noise vanishes for both perfectly transmitting ($T_n=1$) and perfectly reflecting ($T_n=0$) channels, as there is no randomness in these cases. The noise is maximized for $T_n=1/2$. This is a purely quantum mechanical result. For example, for a two-channel conductor with given transmission eigenvalues $T_1$ and $T_2$, the total noise is simply the sum of the contributions from each channel [@problem_id:1162410].

The ratio of the shot noise to the classical Poissonian noise value ($2e|I|$) is called the **Fano factor**, $F = S_I/(2e|I|)$. For a multi-channel conductor, it is given by:
$$
F = \frac{\sum_n T_n(1-T_n)}{\sum_n T_n}
$$
The Fano factor quantifies the suppression of noise below the classical expectation and can provide detailed information about the transport mechanism. For instance, in a conductor with a spin-flipping scatterer, the transmission eigenvalues depend on the relative strengths of spin-conserving and spin-flipping processes. The Fano factor can then be expressed in terms of the total transmission probability $T$ and the conditional spin-flip probability $p_f$, yielding a non-trivial dependence $F=1-T(1+4p_f(1-p_f))$ [@problem_id:1162370]. Measuring the Fano factor can thus serve as a probe of [spin-dependent scattering](@entry_id:138781).

#### Full Counting Statistics

Shot noise is just the second cumulant of the current fluctuations. A complete description is provided by **Full Counting Statistics (FCS)**, which aims to find the probability distribution $P(Q)$ that a total charge $Q$ is transferred through the conductor in a given time $\tau$. This information is encoded in the **Cumulant Generating Function (CGF)**, $\mathcal{F}(\chi) = \ln \langle e^{i\chi Q} \rangle$, where $\chi$ is a "counting field". For a single channel at zero temperature, the CGF is given by the Levitov-Lesovik formula:
$$
\mathcal{F}(\chi) = \frac{\tau eV}{h} \ln\left[1 + T\left(e^{i\chi e} - 1\right)\right]
$$
The current cumulants $S_k$ can be obtained by successive differentiation of the CGF.
*   $S_1 = \langle I \rangle = \frac{e^2 V}{h} T$ (the average current).
*   $S_2 = S_I(0) = \frac{e^3 V}{h} T(1-T)$ (the [shot noise](@entry_id:140025), for spinless electrons).
*   $S_3 = \frac{e^4 V}{h} T(1-T)(1-2T)$ (the third cumulant, or skewness) [@problem_id:1162418].

The third cumulant reveals the asymmetry of the [charge distribution](@entry_id:144400). For a symmetric barrier ($T=1/2$), $S_3=0$, indicating a symmetric, binomial-like distribution of transmitted charges. For other values of $T$, the distribution is skewed. The FCS formalism can be applied to more complex systems, such as a [resonant tunneling](@entry_id:146897) device. In the limit of high bias, the CGF for a Breit-Wigner resonance takes a simple form that depends only on the [resonance width](@entry_id:186927) $\Gamma$, highlighting the universal nature of charge statistics in certain limits [@problem_id:1162416].

### Advanced and Dynamic Phenomena

The versatility of the Landauer-Büttiker framework extends to dynamic and time-dependent transport phenomena.

#### Adiabatic Quantum Pumping

A remarkable prediction of [mesoscopic physics](@entry_id:138415) is that a DC current can be generated in the absence of any applied voltage bias. This is achieved through **adiabatic quantum pumping**, where two or more parameters of the scatterer are varied slowly and cyclically in time. As the scattering potential changes, it can "pump" electrons from one lead to another.

The charge pumped per cycle, $Q$, is a geometric quantity. According to **Brouwer's formula**, it is given by the integral of a "Berry curvature" over the area enclosed by the cycle in parameter space. For a two-terminal, single-channel device with a [scattering matrix](@entry_id:137017) $S(x,y)$ dependent on two parameters $x$ and $y$, the charge pumped into the right lead is:
$$
Q_R = \frac{e}{2\pi} \iint_D \mathrm{Im}\left[ \left(\frac{\partial t^*}{\partial x}\right)\left(\frac{\partial t}{\partial y}\right) + \left(\frac{\partial (r')^*}{\partial x}\right)\left(\frac{\partial r'}{\partial y}\right) \right] dx\,dy
$$
where $t$ and $r'$ are elements of the [scattering matrix](@entry_id:137017). This formula provides a direct method to calculate the pumped charge for any given cyclic modulation of the scatterer's properties [@problem_id:1162394].

#### Wigner-Smith Time Delay

Beyond *what* is transmitted, we can also ask *how long* the transmission process takes. The **Wigner-Smith time delay** measures the excess time a particle spends in a scattering region compared to free propagation. It is profoundly connected to the phase of the [scattering matrix](@entry_id:137017). For a transmitted particle, the time delay $\tau_t$ is related to the [energy derivative](@entry_id:268961) of the transmission phase $\phi_t(E)$:
$$
\tau_t(E) = \hbar \frac{d\phi_t(E)}{dE}
$$
This relationship implies that rapidly varying phases, which occur near scattering resonances, are associated with long time delays. For a Breit-Wigner resonance, which describes scattering through a [quasi-bound state](@entry_id:144141), the time delay is maximized at the [resonance energy](@entry_id:147349) $E_0$. At this point, the delay is $\tau_t(E_0) = 2\hbar/\Gamma$, where $\Gamma$ is the [resonance width](@entry_id:186927) [@problem_id:1162379]. Since the lifetime of the [quasi-bound state](@entry_id:144141) is $\tau_{life} \sim \hbar/\Gamma$, the Wigner-Smith delay is directly proportional to the time the particle is trapped in the resonant state before escaping.

### Thermoelectric and Thermal Transport

The Landauer-Büttiker formalism is not limited to [charge transport](@entry_id:194535); it provides an equally elegant description of [heat transport](@entry_id:199637) carried by electrons. This allows for a unified quantum theory of thermoelectric phenomena.

#### Thermal Conductance

When a temperature difference $\Delta T$ is applied across a conductor (with zero voltage bias), a heat current $J_Q$ flows. The electronic [thermal conductance](@entry_id:189019) is $\kappa_e = J_Q / \Delta T$. The Landauer formula for [thermal conductance](@entry_id:189019) in a single channel is:
$$
\kappa_e = \frac{\pi^2 k_B^2 T}{3h} \mathcal{T}
$$
where $\mathcal{T}$ is the transmission probability at the Fermi energy. The prefactor $\kappa_Q = \pi^2 k_B^2 T / (3h)$ is the universal **[quantum of thermal conductance](@entry_id:190013)**.

Similar to [electrical conductance](@entry_id:261932), dephasing affects [thermal transport](@entry_id:198424). If a wire is modeled with an intermediate floating probe that breaks [phase coherence](@entry_id:142586) but allows for local [thermalization](@entry_id:142388), the system behaves as two thermal conductors in series. For a perfect wire with such a probe at its midpoint, each half has a [thermal conductance](@entry_id:189019) of $\kappa_Q$. The total [thermal conductance](@entry_id:189019) of the system is then $\kappa_e = \kappa_Q/2$, just as two identical resistors in series halve the total conductance [@problem_id:1162357]. The formalism also extends to non-local thermal effects in multi-terminal devices, allowing for the calculation of coefficients like $\mathcal{L}_{12} = \partial I_{Q,1} / \partial T_2$, which describes how the heat current in lead 1 changes in response to a temperature change in lead 2 [@problem_id:1162405].

#### Thermopower and the Mott Formula

The **Seebeck effect**, or [thermopower](@entry_id:142873), is the generation of a voltage difference in response to a temperature gradient. The Seebeck coefficient is defined as $S = -\Delta V / \Delta T$ under the condition of zero electrical current. At low temperatures, it is given by the **Mott formula**:
$$
S = -\frac{\pi^2 k_B^2 T}{3e} \left. \frac{d\ln G(E)}{dE} \right|_{E=E_F} = -\frac{\pi^2 k_B^2 T}{3e} \left. \frac{G'(E_F)}{G(E_F)} \right|
$$
where $G(E) = (2e^2/h) T(E)$ is the energy-dependent conductance. The [thermopower](@entry_id:142873) is therefore sensitive to the *asymmetry* of the transmission function around the Fermi energy. A symmetric transmission function ($T(E_F+\delta E) = T(E_F-\delta E)$) yields zero [thermopower](@entry_id:142873). For a Fabry-Pérot [interferometer](@entry_id:261784), where $T(E)$ exhibits sharp resonances, the [thermopower](@entry_id:142873) oscillates strongly as a function of Fermi energy, changing sign as $E_F$ is swept across a transmission peak [@problem_id:1162417]. The formalism can also handle complex multi-terminal thermoelectric problems, such as calculating the [thermopower](@entry_id:142873) of a device that includes a floating voltage probe [@problem_id:1162393].

#### The Wiedemann-Franz Law

In classical metals, the **Wiedemann-Franz law** states that the ratio of the [electronic thermal conductivity](@entry_id:263457) to the [electrical conductivity](@entry_id:147828) is proportional to the temperature, with a universal constant of proportionality known as the Lorenz number, $L = \kappa_e/(GT) = L_0 = (\pi^2/3)(k_B/e)^2$.

In the Landauer-Büttiker framework, this law holds exactly if the transmission probability $T(E)$ is constant over the energy scale of $k_B T$ around the Fermi energy. However, if $T(E)$ varies significantly, deviations occur. For a conductor dominated by a sharp resonance centered at the Fermi energy, the transmission is strongly energy-dependent. A Sommerfeld expansion can be used to calculate the low-temperature corrections to both $G$ and $\kappa_e$. This reveals that the Lorenz number acquires a temperature-dependent correction: $L = L_0 + \Delta L$. The correction $\Delta L$ is positive and proportional to $(k_B T / \Gamma)^2$, where $\Gamma$ is the [resonance width](@entry_id:186927) [@problem_id:1162381]. This violation of the Wiedemann-Franz law is a direct signature of the energy-dependent nature of quantum transmission.