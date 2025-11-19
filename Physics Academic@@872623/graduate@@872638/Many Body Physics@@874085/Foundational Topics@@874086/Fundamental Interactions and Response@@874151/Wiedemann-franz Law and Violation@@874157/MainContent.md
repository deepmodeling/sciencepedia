## Introduction
The Wiedemann-Franz (WF) law stands as a cornerstone of metal physics, establishing a surprisingly simple and universal relationship between a material's thermal and electrical conductivities. This principle, which holds true for a vast array of conventional metals, is a direct consequence of the Fermi liquid picture where the same electronic quasiparticles carry both charge and heat. However, the true power of the WF law in modern research lies not in its confirmation, but in its violation. Deviations from the universal Lorenz number provide a powerful, quantitative window into the fundamental nature of [elementary excitations](@entry_id:140859), the role of [inelastic scattering](@entry_id:138624), and the emergence of exotic [states of matter](@entry_id:139436) that defy the standard quasiparticle paradigm. This article provides a comprehensive exploration of this pivotal law. We will first delve into the **Principles and Mechanisms** that underpin the WF law and lead to its violation. Next, we will survey its **Applications and Interdisciplinary Connections**, showcasing how measuring the Lorenz ratio serves as a crucial diagnostic tool in fields from [mesoscopic physics](@entry_id:138415) to the study of non-Fermi liquids. Finally, you will have the opportunity to solidify your understanding through **Hands-On Practices**, applying the theoretical concepts to concrete physical systems.

## Principles and Mechanisms

The Wiedemann-Franz (WF) law is a foundational principle in the physics of metals, establishing a profound connection between a material's ability to conduct electricity and its ability to conduct heat. It posits that for a vast range of metallic conductors, the ratio of the [electronic thermal conductivity](@entry_id:263457), $\kappa$, to the electrical conductivity, $\sigma$, is directly proportional to the [absolute temperature](@entry_id:144687), $T$. This relationship is captured by the Lorenz number, $L$, defined as:

$L = \frac{\kappa}{\sigma T}$

Remarkably, for simple metals at low temperatures, this value converges to a universal constant, the Sommerfeld value $L_0 = \frac{\pi^2}{3} \left(\frac{k_B}{e}\right)^2 \approx 2.44 \times 10^{-8} \, \text{W}\Omega\text{K}^{-2}$, where $k_B$ is the Boltzmann constant and $e$ is the elementary charge. The remarkable success of this law stems from the fact that in many metals, the same itinerant electrons are responsible for both charge and [heat transport](@entry_id:199637). However, deviations from this law, or "violations," are equally profound, offering a powerful diagnostic tool to probe the nature of [elementary excitations](@entry_id:140859), scattering mechanisms, and the very fabric of [electronic states](@entry_id:171776) in [quantum materials](@entry_id:136741). This chapter elucidates the core principles underpinning the Wiedemann-Franz law and explores the diverse mechanisms that lead to its violation.

### The Wiedemann-Franz Law in the Fermi Liquid Paradigm

The theoretical basis for the Wiedemann-Franz law is most transparently established within the framework of Fermi liquid theory, which describes the collective behavior of interacting electrons in a metal as a gas of weakly interacting "quasiparticles." The transport properties of this gas can be modeled using the semi-classical Boltzmann transport equation.

Within the [relaxation time approximation](@entry_id:139275), the electrical conductivity $\sigma$ and the [electronic thermal conductivity](@entry_id:263457) $\kappa$ can be expressed in terms of transport integrals. For an isotropic system, these are given by:

$\sigma = e^2 \mathcal{K}_0$

$\kappa = \frac{1}{T} \left( \mathcal{K}_2 - \frac{\mathcal{K}_1^2}{\mathcal{K}_0} \right)$

where the kinetic coefficients $\mathcal{K}_n$ are defined as:

$\mathcal{K}_n = \int_0^\infty d\epsilon \, \mathcal{T}(\epsilon) (\epsilon - \mu)^n \left( - \frac{\partial f_0}{\partial \epsilon} \right)$

Here, $\mu$ is the chemical potential, $f_0(\epsilon) = [ \exp((\epsilon-\mu)/(k_B T)) + 1]^{-1}$ is the Fermi-Dirac distribution function, and $\mathcal{T}(\epsilon)$ is a general transport function that encapsulates details of the electronic band structure and scattering processes. For a system with a [group velocity](@entry_id:147686) $v(\epsilon)$ and an energy-dependent [relaxation time](@entry_id:142983) $\tau(\epsilon)$, this function is proportional to the [density of states](@entry_id:147894) $g(\epsilon)$ as $\mathcal{T}(\epsilon) \propto g(\epsilon) v(\epsilon)^2 \tau(\epsilon)$.

The key to deriving the Wiedemann-Franz law lies in evaluating these integrals in the [low-temperature limit](@entry_id:267361) ($k_B T \ll \mu$). In this regime, the term $-\frac{\partial f_0}{\partial \epsilon}$ acts like a narrow window function centered at the chemical potential $\mu$. We can employ the Sommerfeld expansion, which shows that for a smooth transport function $\mathcal{T}(\epsilon)$, the integrals are dominated by the properties of the system right at the Fermi energy.

The crucial assumptions are:
1.  **Degenerate Fermi Statistics:** The charge carriers obey Fermi-Dirac statistics, and the temperature is low enough that only electrons within a narrow energy shell of width $\sim k_B T$ around the Fermi surface contribute to transport.
2.  **Elastic Scattering:** The scattering events that limit the electrons' free motion are elastic, meaning the electron's energy is conserved in a collision. This implies that the relaxation time $\tau$ does not depend on energy in the immediate vicinity of the Fermi surface, i.e., $\tau(\epsilon) \approx \tau(\mu)$.

Under these conditions, $\mathcal{T}(\epsilon)$ can be treated as a constant, $\mathcal{T}(\mu)$, and taken out of the integrals. The evaluation of the remaining integrals yields:
$\mathcal{K}_0 \approx \mathcal{T}(\mu)$
$\mathcal{K}_1 \approx 0$
$\mathcal{K}_2 \approx \mathcal{T}(\mu) \frac{\pi^2}{3}(k_B T)^2$

Substituting these back into the expressions for conductivity gives:
$\sigma \approx e^2 \mathcal{T}(\mu)$
$\kappa \approx \frac{1}{T} \mathcal{K}_2 = \frac{\pi^2 k_B^2}{3} \mathcal{T}(\mu) T$

The ratio then becomes:
$L = \frac{\kappa}{\sigma T} = \frac{\frac{\pi^2 k_B^2}{3} \mathcal{T}(\mu) T}{(e^2 \mathcal{T}(\mu))T} = \frac{\pi^2}{3} \left( \frac{k_B}{e} \right)^2 = L_0$

This celebrated result demonstrates that the Lorenz number is a universal constant, independent of the specific details of the metal, such as its dimensionality, the effective mass of the electrons, or the precise value of the [scattering time](@entry_id:272979) [@problem_id:1221120]. The same universal value is obtained from the more rigorous, fully quantum-mechanical Kubo formalism, reinforcing its fundamental nature within the Fermi liquid picture [@problem_id:1221150].

The importance of Fermi-Dirac statistics becomes evident when contrasted with a classical gas of charged particles obeying Maxwell-Boltzmann statistics. For such a classical system, a similar calculation yields a Lorenz number of $L = \frac{5}{2} \left( \frac{k_B}{e} \right)^2$ [@problem_id:1221192]. The difference arises because in a classical gas, particles over a much broader range of energies contribute to transport, fundamentally altering the relationship between the average energy carried per particle (relevant for $\kappa$) and their response to an electric field (relevant for $\sigma$).

### Conditions for Validity and Sources of Deviation

The validity of the Wiedemann-Franz law hinges critically on the assumption of [elastic scattering](@entry_id:152152), where the transport relaxation time $\tau$ is effectively constant for the narrow band of energies relevant for low-temperature transport. Any energy dependence in the transport function $\mathcal{T}(\epsilon)$ can lead to deviations.

A subtle but important point is that the law remains robust even if the scattering is anisotropic on the Fermi surface. As long as the [scattering time](@entry_id:272979) $\tau(\mathbf{k})$ depends only on the direction of the wavevector $\mathbf{k}$ on the Fermi surface but not on energy, the energy-independent part of the transport function factors out of the Sommerfeld integrals in the same way, and the universal Lorenz number $L_0$ is recovered [@problem_id:1221104].

Deviations from $L_0$ can emerge even in the presence of purely [elastic scattering](@entry_id:152152) if the scattering rate itself has a strong energy dependence near the Fermi energy. For instance, consider a hypothetical case where the [relaxation time](@entry_id:142983) vanishes for electrons exactly at the Fermi surface, described by a power-law dependence $\tau(\epsilon) \propto (\epsilon - \epsilon_F)^n$. For $n=2$, a calculation shows that the Lorenz number deviates significantly from the standard value, yielding $L = \frac{7\pi^2}{5} \left( \frac{k_B}{e} \right)^2$ [@problem_id:1221265]. In this scenario, the thermal current, which gives more weight to electrons further from $\epsilon_F$, experiences a disproportionately longer average [scattering time](@entry_id:272979) than the electrical current, enhancing $\kappa$ relative to $\sigma$ and increasing the Lorenz number.

More commonly, deviations arise from a combination of an energy-dependent [scattering time](@entry_id:272979) and a non-parabolic band structure. In general, any energy dependence in the transport function $\mathcal{T}(\epsilon)$ will introduce temperature-dependent corrections to the Lorenz number. For small deviations at low temperature, the Lorenz ratio can be expressed as a [series expansion](@entry_id:142878) in temperature [@problem_id:1221239]:
$\frac{L}{L_0} = 1 + c_1 (k_B T)^2 \left[ \frac{\mathcal{T}''(\mu)}{\mathcal{T}(\mu)} - c_2 \left(\frac{\mathcal{T}'(\mu)}{\mathcal{T}(\mu)}\right)^2 \right] + \mathcal{O}(T^4)$
where $c_1$ and $c_2$ are numerical constants. This shows that the WF law holds exactly only if the transport function is effectively constant near the chemical potential.

A prime example of such a correction comes from **particle-hole asymmetry**, where the [electronic density of states](@entry_id:182354) is not symmetric about the Fermi energy. Modeling the DOS with a linear energy dependence, $g(\epsilon) \approx g_0 + g_1(\epsilon - \mu)$, leads to a non-zero thermoelectric coefficient $\mathcal{L}_1$ and a correction to the Lorenz number [@problem_id:1221179]:
$L \approx L_0 \left( 1 - \frac{\pi^2 (k_B T)^2 g_1^2}{3 g_0^2} \right)$
This result shows that even a small departure from perfect [particle-hole symmetry](@entry_id:142469) results in a suppression of the Lorenz number, with the deviation scaling as $T^2$.

### Strong Violations from Inelastic Scattering

The most dramatic and commonly observed violations of the Wiedemann-Franz law occur when **inelastic scattering** processes become significant. Inelastic collisions, such as those between electrons or between electrons and phonons, do not conserve the energy of the charge carrier. This affects heat and charge transport differently, breaking the simple proportionality that underpins the WF law.

A powerful [phenomenological model](@entry_id:273816) illustrates this principle clearly. In a "dirty metal" where scattering is dominated by static impurities (elastic, time $\tau_{el}$) but with a weak overlay of inelastic scattering (time $\tau_{in}$), we have $\tau_{el} \ll \tau_{in}$. Electrical [resistivity](@entry_id:266481) arises from processes that relax the total momentum of the [electron gas](@entry_id:140692), which requires scattering off external objects like impurities or the lattice. Inelastic [electron-electron scattering](@entry_id:152847), by contrast, conserves total momentum and thus does not directly contribute to [electrical resistance](@entry_id:138948). Therefore, the relaxation time for electrical conductivity is simply $\tau_\sigma = \tau_{el}$. A heat current, however, represents a flow of energy and can be degraded by any process that thermalizes the electron distribution, including [inelastic scattering](@entry_id:138624). Assuming the rates add (Matthiessen's rule), the relaxation time for thermal conductivity is given by $1/\tau_\kappa = 1/\tau_{el} + 1/\tau_{in}$. This leads to a modified Lorenz number [@problem_id:1221165]:

$L = L_0 \frac{\tau_\kappa}{\tau_\sigma} = L_0 \frac{\tau_{in}}{\tau_{el} + \tau_{in}}$

Since $\tau_{in} > 0$, this immediately shows that [inelastic scattering](@entry_id:138624) suppresses the Lorenz number, $L  L_0$. The [first-order correction](@entry_id:155896) is $\Delta L = L - L_0 \approx -L_0 (\tau_{el}/\tau_{in})$.

This principle finds application in several key physical scenarios:

**1. Electron-Phonon Scattering:** At temperatures well below the Debye temperature ($\theta_D$), the energy of emitted or absorbed phonons is comparable to $k_B T$, making [electron-phonon scattering](@entry_id:138098) strongly inelastic. This leads to a significant suppression of the Lorenz number. For instance, in a model with scattering from a single [optical phonon](@entry_id:140852) mode of energy $\hbar\omega_0$, the Lorenz ratio is suppressed according to $L/L_0 = (1 + \frac{3}{2\pi^2} (\hbar\omega_0/k_B T)^2)^{-1}$ [@problem_id:1221220]. However, in the high-temperature limit ($T \gg \theta_D$), the typical phonon energy is much smaller than $k_B T$. Scattering becomes quasi-elastic, as the energy exchanged is negligible compared to the thermal energy of the electrons. In this limit, the conditions for the WF law are restored, and $L$ approaches $L_0$ [@problem_id:1221190].

**2. Electron-Electron Scattering and the Hydrodynamic Regime:** In ultraclean materials, electron-electron (e-e) scattering can become the fastest scattering process ($\tau_{ee} \ll \tau_{mr}$, where $\tau_{mr}$ is the momentum-relaxing time). As e-e scattering conserves momentum, it does not contribute to [electrical resistivity](@entry_id:143840), which is governed by the much slower $\tau_{mr}$. However, e-e scattering is extremely effective at relaxing a heat current. This leads to the so-called **hydrodynamic regime** of electron transport. Applying Matthiessen's rule to the thermal *[resistivity](@entry_id:266481)* ($W = 1/\kappa$), we have $W = W_{mr} + W_{ee}$. This leads to a strongly temperature-dependent Lorenz number [@problem_id:1221240]:

$L(T) = L_0 \frac{\tau_{ee}}{\tau_{mr} + \tau_{ee}}$

Since Fermi liquid theory predicts $\tau_{ee} \propto 1/T^2$, this results in a dramatic suppression $L(T) \propto 1/T^2$ at low temperatures, a hallmark of [electron hydrodynamics](@entry_id:143742).

**3. Non-Fermi Liquids:** The concept of WF violation can be generalized to non-Fermi liquids (NFLs), where the very notion of a quasiparticle is ill-defined. Using a kinetic theory framework, we can relate the Lorenz number to the anomalous temperature scaling of other physical quantities. If the [electronic specific heat](@entry_id:144099) scales as $C_e \propto T^\alpha$ and the resistivity as $\rho \propto T^\beta$, and a single scattering mechanism with time $\tau \propto 1/\rho$ controls transport, then the thermal conductivity scales as $\kappa \propto C_e \tau$. This leads to a scaling relation for the Lorenz number [@problem_id:1221140]:

$L(T) \propto T^{\alpha - 1}$

This provides a powerful way to classify NFL behavior. For a Fermi liquid, $\alpha=1$, and we recover a constant Lorenz number. For many NFLs, $\alpha  1$, leading to a diverging Lorenz number as $T \to 0$.

### Manifestations in Complex and Quantum Systems

The Wiedemann-Franz law serves as a crucial benchmark in modern condensed matter physics, where its violation often signals the emergence of exotic [electronic states](@entry_id:171776).

**Quantum Interference Effects:** In disordered conductors, quantum interference between different [electron scattering](@entry_id:159023) paths gives rise to corrections to the classical Drude [transport coefficients](@entry_id:136790).
- **Weak Localization:** This effect leads to a negative correction to the [electrical conductivity](@entry_id:147828), $\delta\sigma  0$. Crucially, for purely elastic scattering, the corresponding correction to the thermal conductivity vanishes, $\delta\kappa = 0$. This is because the quantum interference is sensitive to the electron's phase, which is preserved in [thermal transport](@entry_id:198424) due to particle-hole cancellations. The result is a net *enhancement* of the Lorenz number [@problem_id:1221222]: $L = L_0 (\sigma_0 / (\sigma_0 + \delta\sigma))  L_0$.
- **Altshuler-Aronov Effect:** Electron-electron interactions in a disordered system lead to a correction in the [density of states](@entry_id:147894) near the Fermi energy. If this correction, $\delta N(\epsilon_F)$, is the only one considered, it affects both $\sigma$ and $\kappa$ proportionally, as both are proportional to the DOS. Consequently, the correction cancels out in the ratio, and the Lorenz number remains unchanged, $L=L_0$ [@problem_id:1221207]. This provides a fascinating contrast to [weak localization](@entry_id:146052), highlighting that not all quantum corrections violate the WF law.

**Multi-Band Effects and Exotic Excitations:**
- **Lifshitz Transitions:** In metals with multiple [electronic bands](@entry_id:175335), the overall transport is an average over all contributing bands. If a system undergoes a Lifshitz transition where a new Fermi pocket appears, and this new channel contributes differently to charge and heat transport, the total Lorenz number will be affected. For instance, if a new band opens that conducts charge but not heat, it effectively short-circuits the electrical path, leading to a suppression of the overall Lorenz number below $L_0$ [@problem_id:1221125].
- **Spin-Charge Separation:** In one-dimensional interacting systems known as Luttinger liquids, the fundamental electronic quasiparticle disintegrates into separate collective modes for charge (holons) and spin (spinons). Since holons carry charge and heat, while neutral [spinons](@entry_id:140415) carry only heat, the carriers for charge and heat are fundamentally different. The total [thermal conductance](@entry_id:189019) is the sum of contributions from both modes, whereas the electrical conductance arises only from the charge mode. This leads to a profound violation of the WF law, with the Lorenz number depending on the interaction strength, characterized by the Luttinger parameter $K_c$. For a spin-1/2 system, the Lorenz ratio becomes $L/L_0 = 2/K_c$ [@problem_id:1221158]. For repulsive interactions ($K_c  1$), this results in an enhanced Lorenz number.
- **Charge-Heat Separation near Mott Transitions:** Extreme violations are predicted near certain quantum critical points. The problem text of [@problem_id:1221163] describes a hypothetical exotic metal where electrical resistivity vanishes ($\rho \to 0$, so $\sigma \to \infty$) while thermal conductivity remains finite. This complete decoupling of charge and heat transport would lead to a Lorenz number that vanishes, $L \to 0$. Conversely, and more characteristic of systems approaching a Mott insulating state, one can have a scenario where charge carriers become localized ($\rho \to \infty$) while charge-neutral excitations (like spinons) can still transport heat, keeping $\kappa$ finite. In this case, the Lorenz number would diverge, $L \to \infty$. Both scenarios represent a total breakdown of the Fermi liquid picture.

### Practical Implications and Connections

Beyond its role as a diagnostic tool for fundamental physics, the Wiedemann-Franz law has significant practical implications.

**Experimental Considerations:** When measuring the Lorenz number, experimentalists typically access the *total* thermal conductivity, $\kappa_{total}$, which includes contributions from both electrons ($\kappa_{el}$) and lattice vibrations or phonons ($\kappa_{ph}$). The measured Lorenz number is therefore $L_{meas} = (\kappa_{el} + \kappa_{ph}) / (\sigma T)$. Even if the electronic system perfectly obeys the WF law ($\kappa_{el} = L_0 \sigma T$), the phonon contribution leads to an apparent enhancement [@problem_id:1221152]:

$L_{meas} = L_0 \left(1 + \frac{\kappa_{ph}}{\kappa_{el}}\right)$

This effect is particularly important in materials that are poor electrical conductors, where the ratio $\kappa_{ph}/\kappa_{el}$ can be large, leading to a measured Lorenz number significantly greater than $L_0$.

**Thermoelectric Materials:** The efficiency of thermoelectric devices, which convert heat into electrical energy, is quantified by the dimensionless figure of merit, $ZT = S^2 \sigma T / \kappa$, where $S$ is the Seebeck coefficient. To achieve a high $ZT$, a material must paradoxically be a good electrical conductor ($\sigma$) but a poor thermal conductor ($\kappa$). The Wiedemann-Franz law presents a fundamental obstacle, as it implies that enhancing $\sigma$ will also enhance $\kappa_{el}$. Therefore, a key strategy in designing high-performance [thermoelectrics](@entry_id:142625) is to find materials that strongly violate the WF law, specifically with $L  L_0$. Theoretical bounds suggest a direct relationship between the maximum possible $ZT$ and the suppression of the Lorenz number. For a material where $L=f L_0$ with $f1$, the maximum $ZT$ is bounded by $ZT_{max} = (1-f)/f$ [@problem_id:1221097]. This establishes the violation of the Wiedemann-Franz law as a central design principle in the search for better [thermoelectric materials](@entry_id:145521).