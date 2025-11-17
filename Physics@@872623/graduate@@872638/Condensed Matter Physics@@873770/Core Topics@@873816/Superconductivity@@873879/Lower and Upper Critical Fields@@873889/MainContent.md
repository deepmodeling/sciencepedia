## Introduction
The discovery of superconductivity—the complete disappearance of electrical resistance below a critical temperature—opened a new frontier in condensed matter physics. A key aspect of this phenomenon is its interaction with magnetic fields, which reveals a rich and complex behavior. While all superconductors expel magnetic fields up to a certain limit (the Meissner effect), they do not all break down in the same way. This raises a fundamental question: what governs the distinct magnetic responses that lead to the classification of superconductors into Type-I and Type-II? The answer lies in the concept of critical magnetic fields, which not only define this classification but also dictate the technological utility of these extraordinary materials. This article provides a graduate-level exploration of the lower and upper [critical fields](@entry_id:272263), which are the hallmarks of Type-II superconductivity. In the first chapter, **Principles and Mechanisms**, we will dissect the energetic basis for the two superconductor types using Ginzburg-Landau theory, deriving expressions for the [lower critical field](@entry_id:144776) ($H_{c1}$) and the [upper critical field](@entry_id:139431) ($H_{c2}$) and exploring the physics of the intervening Abrikosov [vortex state](@entry_id:204018). The second chapter, **Applications and Interdisciplinary Connections**, will bridge theory and experiment, demonstrating how measurements of these [critical fields](@entry_id:272263) are used to characterize materials and how the [vortex state](@entry_id:204018) enables high-field technologies. Finally, the **Hands-On Practices** section will provide opportunities to apply these concepts through guided problems, solidifying your understanding by deriving critical field expressions and analyzing their behavior in idealized systems.

## Principles and Mechanisms

In the preceding chapter, we introduced the phenomenon of superconductivity and its macroscopic hallmarks: [zero electrical resistance](@entry_id:151583) and the Meissner-Ochsenfeld effect. We now delve into the rich and complex behavior of superconductors in the presence of an external magnetic field. This behavior is not monolithic; rather, it gives rise to a fundamental classification of all superconductors into two distinct categories—Type-I and Type-II. This chapter elucidates the principles governing this classification and the mechanisms that define the characteristic magnetic field scales, known as the lower and upper [critical fields](@entry_id:272263), which are central to the physics of Type-II superconductors.

### The Energetic Basis for Two Types of Superconductors

The distinction between Type-I and Type-II superconductivity originates from a subtle energetic balance at the interface between a normal, field-penetrated region and a superconducting, field-expelled region. The Ginzburg-Landau (GL) theory of superconductivity formalizes this by identifying two [characteristic length scales](@entry_id:266383) that govern the material's response.

The first is the **[magnetic penetration depth](@entry_id:140378)**, $\lambda$, which describes the distance over which an external magnetic field is screened by supercurrents and decays to zero inside the superconductor. The second is the **coherence length**, $\xi$, which represents the minimum distance over which the superconducting order parameter, $\psi$, can vary significantly. Physically, it can be thought of as the intrinsic size of a Cooper pair.

Consider an interface between a normal (N) and a superconducting (S) phase held in equilibrium at the thermodynamic [critical field](@entry_id:143575), $H_c$. The stability of this interface is determined by its **[surface energy](@entry_id:161228)**, $\sigma_{ns}$. This energy is the result of two competing contributions [@problem_id:3002060]:

1.  A positive energy contribution arises from the suppression of the superconducting order parameter. Across a region of width $\sim\xi$ at the interface, $|\psi|$ must vary from zero in the normal phase to its full value in the superconducting phase. Within this layer, the system has not gained the full superconducting condensation energy, resulting in an energy cost.

2.  A [negative energy](@entry_id:161542) contribution arises from the magnetic field. Across a region of width $\sim\lambda$ at the interface, the magnetic field is only partially expelled. This partial presence of the field reduces the Gibbs free energy compared to a state of perfect expulsion, resulting in an energy gain.

The net surface energy, $\sigma_{ns}$, therefore depends on the balance between the energy cost over the length scale $\xi$ and the energy gain over the length scale $\lambda$. The dimensionless **Ginzburg-Landau parameter**, $\kappa = \lambda / \xi$, captures this competition. A rigorous calculation within GL theory reveals that the sign of the [surface energy](@entry_id:161228) changes at a critical value, $\kappa = 1/\sqrt{2}$.

-   If $\kappa  1/\sqrt{2}$, then $\lambda  \xi$. The energy cost of suppressing the order parameter dominates, and the surface energy $\sigma_{ns}$ is positive. The system seeks to minimize the area of N-S interfaces. Such materials are classified as **Type-I superconductors**. They maintain a perfect Meissner state (complete flux expulsion) until the applied field reaches the thermodynamic [critical field](@entry_id:143575) $H_c$, at which point the entire sample undergoes a [first-order phase transition](@entry_id:144521) into the normal state. A state with intermixed normal and superconducting regions is energetically unstable. [@problem_id:3002072]

-   If $\kappa > 1/\sqrt{2}$, then $\lambda > \xi$. The energy gain from field penetration dominates, and the surface energy $\sigma_{ns}$ is negative. It becomes energetically favorable for the system to create N-S interfaces. Such materials are classified as **Type-II superconductors**. Instead of a single transition, their response to a magnetic field is divided into three distinct phases, separated by two [critical fields](@entry_id:272263). [@problem_id:3002072]

### The Critical Fields of Type-II Superconductors

For a Type-II superconductor ($\kappa > 1/\sqrt{2}$), the negative [surface energy](@entry_id:161228) allows for a novel thermodynamic phase: a **[mixed state](@entry_id:147011)** (or Shubnikov phase), where magnetic flux penetrates the material in the form of discrete, [quantized flux](@entry_id:157931) tubes known as **Abrikosov vortices**. This phase is bracketed by the lower and upper [critical fields](@entry_id:272263), $H_{c1}$ and $H_{c2}$.

1.  **Meissner State ($H  H_{c1}$):** At low applied fields, the material behaves like a Type-I superconductor, completely expelling the magnetic field via surface screening currents. The magnetic induction in the bulk is zero (far from the surface), and the material exhibits strong diamagnetism. [@problem_id:3002014]

2.  **Mixed State ($H_{c1}  H  H_{c2}$):** Above a **[lower critical field](@entry_id:144776)**, $H_{c1}$, magnetic flux begins to penetrate the superconductor in the form of vortices. Each vortex consists of a normal-state core of radius $\sim\xi$, where the order parameter $\psi$ is suppressed, surrounded by circulating supercurrents that decay over the scale of $\lambda$. Crucially, each vortex carries a single quantum of magnetic flux, $\Phi_0 = h/(2e)$. As the applied field increases, the density of these vortices increases, and the average magnetic induction $\mathbf{B}$ in the bulk grows. However, diamagnetism is still present ($M0$), so the average induction remains less than the applied field (in SI units, $\mathbf{B}  \mu_0 \mathbf{H}$).

3.  **Normal State ($H > H_{c2}$):** Above an **[upper critical field](@entry_id:139431)**, $H_{c2}$, the vortex cores begin to overlap, and superconductivity is destroyed throughout the bulk of the material. The order parameter $\psi$ vanishes everywhere, and the material transitions into its normal, non-superconducting state. This is a [second-order phase transition](@entry_id:136930). [@problem_id:3002014]

### The Lower Critical Field, $H_{c1}$: The Onset of Flux Penetration

The [lower critical field](@entry_id:144776) $H_{c1}$ is rigorously defined as the applied field at which the Gibbs free energy cost of introducing a single vortex into the bulk becomes zero [@problem_id:3002014]. To understand this, we consider the system at constant temperature and constant applied field $H_a$, for which the Gibbs free energy $G$ is the relevant thermodynamic potential to be minimized. The change in Gibbs free energy per unit length, $\Delta G/L$, upon creating a single, straight vortex is given by the balance of two terms [@problem_id:3002062]:

$$
\frac{\Delta G}{L} = \varepsilon_1 - \Phi_0 H_a
$$

Here, $\varepsilon_1$ is the intrinsic self-energy per unit length required to create the vortex (the energy of its normal core and circulating supercurrents), which is always positive. The second term, $-\Phi_0 H_a$, represents the favorable interaction energy (work done by the field source) as the vortex's flux quantum $\Phi_0$ aligns with the applied field $H_a$.

Vortex entry is energetically unfavorable as long as $\Delta G > 0$. The threshold for spontaneous entry occurs when $\Delta G$ becomes negative. The crossover point defines $H_{c1}$:
$$
\varepsilon_1 - \Phi_0 H_{c1} = 0 \implies H_{c1} = \frac{\varepsilon_1}{\Phi_0}
$$

The magnitude of the vortex self-energy $\varepsilon_1$, and thus of $H_{c1}$, is dominated by the kinetic and [magnetic energy](@entry_id:265074) of the supercurrents circulating around the core. The superfluid velocity decays as $1/r$ from the vortex center, leading to an energy density that scales as $1/r^2$. Integrating this energy density from the core radius (the lower cutoff, $\sim\xi$) to the penetration depth (the upper cutoff, $\sim\lambda$) yields a term proportional to $\int_{\xi}^{\lambda} dr/r = \ln(\lambda/\xi) = \ln\kappa$ [@problem_id:3001989]. This logarithmic dependence is a hallmark of vortex physics. For large $\kappa$, this leads to the celebrated expression:

$$
H_{c1} \approx \frac{\Phi_0}{4\pi\mu_0\lambda^2} \ln \kappa
$$

For moderate values of $\kappa$, this expression must be corrected to properly account for the energy of the [vortex core](@entry_id:159858) and the detailed current profile near $r \sim \xi$. This correction takes the form of an additive constant, $c$, of order unity: $H_{c1} \approx \frac{\Phi_0}{4\pi\mu_0\lambda^2} (\ln \kappa + c)$. For isotropic superconductors near $T_c$, this constant is approximately $c \approx 0.5$. At lower temperatures, microscopic effects such as nonlocal [electrodynamics](@entry_id:158759) and the Kramer-Pesch shrinkage of the [vortex core](@entry_id:159858) further modify this constant, making it temperature-dependent, but the robust logarithmic structure remains [@problem_id:3001989].

### The Upper Critical Field, $H_{c2}$: The End of Superconductivity

The [upper critical field](@entry_id:139431), $H_{c2}$, marks the [second-order phase transition](@entry_id:136930) to the normal state, where the superconducting order parameter continuously vanishes throughout the bulk. The physical mechanism behind this transition, known as **orbital pair-breaking**, is elegantly captured by the linearized Ginzburg-Landau equation. As $H \to H_{c2}$, the order parameter $|\psi|$ becomes infinitesimally small, allowing us to simplify the full GL equation to:

$$
\frac{1}{2m^*} \left( -i\hbar\nabla - 2e\mathbf{A} \right)^2 \psi = -\alpha \psi
$$

This equation is formally identical to the time-independent Schrödinger equation for a particle of charge $2e$ in a magnetic field. The eigenvalues of the kinetic operator on the left are the famous **Landau levels**. A non-trivial superconducting solution ($\psi \neq 0$) can exist only if the condensation energy term, $-\alpha$ (which is positive for $T  T_c$), is equal to one of these [energy eigenvalues](@entry_id:144381). The highest magnetic field for which a solution exists corresponds to the lowest possible eigenvalue of the kinetic operator. This lowest eigenvalue, $E_{\min}$, for a particle in 3D includes both the lowest Landau level ($n=0$) for motion perpendicular to the field and the minimum kinetic energy for motion parallel to the field ($p_z=0$):
$$
E_{\min} = \frac{1}{2}\hbar\omega_c = \frac{\hbar e B}{m^*}
$$
where $\omega_c = 2eB/m^*$ is the cyclotron frequency. The condition for the onset of superconductivity at $H_{c2}$ (where $B = \mu_0 H_{c2}$) is thus $E_{\min} = -\alpha$. Using the GL relation $\xi^2 = \hbar^2 / (2m^*|\alpha|)$, this yields the fundamental result:
$$
H_{c2} = \frac{\Phi_0}{2\pi\mu_0\xi^2}
$$
This expression shows that the [upper critical field](@entry_id:139431) is fundamentally limited by the [coherence length](@entry_id:140689): a smaller Cooper pair size allows the material to withstand a higher magnetic field. For a clean superconductor at zero temperature, $H_{c2}(0) = \Phi_0/(2\pi\mu_0\xi(0)^2)$. In real materials, this orbital limit can be further reduced by the **Pauli paramagnetic effect**, where the magnetic field aligns the spins of the electrons in a Cooper pair, breaking it. This effect introduces another field scale, the Pauli limiting field $H_p$, and the actual [upper critical field](@entry_id:139431) is determined by the interplay between orbital and Pauli pair-breaking mechanisms.