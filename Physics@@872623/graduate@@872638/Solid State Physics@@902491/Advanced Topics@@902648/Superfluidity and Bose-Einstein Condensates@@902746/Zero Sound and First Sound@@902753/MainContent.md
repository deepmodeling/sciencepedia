## Introduction
In the quantum realm of interacting particles, such as the electrons in a metal or the atoms in liquid $^3$He, collective behavior often manifests as propagating waves. Among the most fundamental of these are two distinct sound-like modes: [first sound](@entry_id:144225) and [zero sound](@entry_id:142772). While both represent collective density oscillations, their underlying physical mechanisms and the conditions for their existence are profoundly different. This distinction addresses a key question in [many-body physics](@entry_id:144526): how does the nature of a collective excitation change as a system transitions from a state governed by frequent collisions to one where particles travel freely?

This article provides a comprehensive exploration of these two fundamental modes of propagation in Fermi liquids. By dissecting their origins, we reveal how macroscopic phenomena like the speed of sound are directly dictated by the microscopic interactions between quasiparticles. The following chapters are structured to guide you from foundational theory to real-world applications and practical problem-solving.

*   **Principles and Mechanisms** will lay the theoretical groundwork, defining the hydrodynamic and collisionless regimes and deriving the properties of first and [zero sound](@entry_id:142772) using the elegant framework of Landau's Fermi liquid theory.
*   **Applications and Interdisciplinary Connections** will demonstrate the power of these concepts as experimental probes, exploring their roles in archetypal [quantum fluids](@entry_id:140332), complex electronic materials, and even at the frontiers of astrophysics and [quantum gravity](@entry_id:145111).
*   **Hands-On Practices** will offer a chance to engage with the material directly, reinforcing the core principles through targeted problem-solving exercises.

We begin by examining the crucial parameter that separates these two sonic worlds and delving into the distinct principles that govern each mode.

## Principles and Mechanisms

In a system of interacting fermions, such as liquid $^3$He or the electrons in a metal, collective excitations can propagate as waves. The nature of these waves is profoundly dependent on the interplay between the wave's characteristic frequency, $\omega$, and the average time between quasiparticle collisions, $\tau$. This interplay defines two distinct physical regimes, each hosting a unique type of sound-like propagation: [first sound](@entry_id:144225) and [zero sound](@entry_id:142772).

### The Two Regimes: Collisions vs. Mean-Field Dynamics

The dimensionless product $\omega\tau$ serves as the crucial parameter distinguishing the two regimes.

In the **collision-dominated** or **hydrodynamic regime**, defined by the condition $\omega\tau \ll 1$, quasiparticles undergo many collisions during a single period of the wave. These frequent collisions ensure that the system remains in a state of [local thermodynamic equilibrium](@entry_id:139579) at all times. Any disturbance propagates as a conventional sound wave, characterized by oscillations in local density, pressure, and temperature. This mode is known as **[first sound](@entry_id:144225)**. It is analogous to the sound that travels through ordinary air or water, where [molecular collisions](@entry_id:137334) are the mechanism of wave propagation.

Conversely, in the **collisionless regime**, where $\omega\tau \gg 1$, a quasiparticle travels over many wavelengths before experiencing a collision. In this limit, the system cannot maintain [local equilibrium](@entry_id:156295), and the hydrodynamic description breaks down. A new type of collective mode, unique to Fermi liquids, can emerge. This mode, termed **[zero sound](@entry_id:142772)**, is not sustained by collisions but by the long-range mean-field interactions between quasiparticles. It corresponds to a coherent, propagating distortion of the Fermi surface itself.

A key challenge is to understand the transition between these two limiting behaviors. The crossover can be conceptually located at a frequency $\omega_c$ where the characteristics of the sound wave change. A practical way to estimate this crossover is by comparing the attenuation rates of the two modes. The attenuation of [first sound](@entry_id:144225), being a viscous effect, typically increases with frequency, while the attenuation of [zero sound](@entry_id:142772) is governed by the collision rate $1/\tau$, which is independent of frequency. By equating the extrapolated attenuation rate of [first sound](@entry_id:144225), $\Gamma_1$, with the attenuation rate of [zero sound](@entry_id:142772), $\Gamma_0 \approx 1/\tau$, we can define a [crossover frequency](@entry_id:263292). For a 3D Fermi liquid, the viscosity-driven attenuation rate for [first sound](@entry_id:144225) is approximately $\Gamma_1 \approx \frac{2\tau\omega^2}{5(1+F_0^s)}$. Setting $\Gamma_1 = \Gamma_0$ at $\omega = \omega_c$ yields a [crossover frequency](@entry_id:263292) of $\omega_c = \frac{1}{\tau}\sqrt{\frac{5(1+F_0^s)}{2}}$ [@problem_id:267675]. This signifies the frequency scale around which $\omega\tau \sim 1$ and the system's response transitions from collective and collisional to coherent and collisionless.

### First Sound: The Hydrodynamic Mode

First sound is the manifestation of density and pressure waves in the limit of rapid local equilibration. Its velocity, $c_1$, is determined by the thermodynamic properties of the Fermi liquid, specifically its [compressibility](@entry_id:144559). The fundamental relation for the speed of sound in any fluid is $c^2 = K/\rho$, where $K$ is the [bulk modulus](@entry_id:160069) ($K = n \frac{\partial P}{\partial n}$) and $\rho$ is the mass density. At zero temperature, this is equivalent to the expression:

$$
c_1^2 = \frac{n}{m} \frac{\partial \mu}{\partial n}
$$

where $n$ is the particle density, $m$ is the bare particle mass, and $\mu$ is the chemical potential.

Within Landau's Fermi liquid theory, the derivative $\frac{\partial\mu}{\partial n}$, which represents the inverse [compressibility](@entry_id:144559), is directly modified by quasiparticle interactions. It is related to the density of states at the Fermi energy, $N(E_F)$, by $\frac{\partial\mu}{\partial n} = 1/N(E_F)$. The theory further states that $N(E_F) = N^*(0)/(1+F_0^s)$, where $N^*(0)$ is the quasiparticle [density of states](@entry_id:147894) and $F_0^s$ is the isotropic, spin-symmetric Landau parameter that quantifies the strength of quasiparticle interactions. By combining these relations with the expressions for particle density ($n = k_F^3 / (3\pi^2)$), Fermi velocity ($v_F = \hbar k_F/m^*$), and the effective mass ($m^*/m = 1+F_1^s/3$), we can derive a comprehensive expression for the [first sound](@entry_id:144225) velocity [@problem_id:267674]:

$$
c_1 = v_F \sqrt{ \frac{1}{3} (1 + F_0^s) \left(1 + \frac{F_1^s}{3}\right) }
$$

This powerful result reveals how microscopic interactions, encoded in the Landau parameters $F_0^s$ and $F_1^s$, dictate a macroscopic property like the speed of sound. The term $(1+F_0^s)$ reflects the interaction-induced change in [compressibility](@entry_id:144559), while $(1+F_1^s/3)$ accounts for the change in quasiparticle inertia through the effective mass.

The expression for $c_1$ also provides deep insight into the stability of the Fermi liquid. A fundamental condition for thermodynamic stability is that the [compressibility](@entry_id:144559) must be positive, which implies $1+F_0^s > 0$. As the system approaches a [phase separation](@entry_id:143918) instability (an isotropic Pomeranchuk instability), the Landau parameter $F_0^s$ approaches $-1$ from above. If we define the proximity to this quantum critical point by the small parameter $\delta = 1 + F_0^s$, the velocity of [first sound](@entry_id:144225) scales as $c_1 \propto \sqrt{\delta}$ [@problem_id:267682]. The vanishing of the sound velocity, $c_1 \to 0$, is a direct physical signature of an infinitely compressible system on the verge of collapsing into distinct high-density and low-density phases. In the vicinity of this instability, the sound mode becomes "soft." Conversely, for strong repulsive interactions ($F_0^s \gg 1$), $c_1$ becomes large, reflecting a stiff, incompressible liquid.

The propagation of [first sound](@entry_id:144225) is not without loss; its amplitude attenuates due to [transport processes](@entry_id:177992) like viscosity. In a clean Fermi liquid at low temperatures, the quasiparticle [scattering time](@entry_id:272979) follows the characteristic law $\tau \propto T^{-2}$. Since viscosity $\eta$ is proportional to $\tau$, the attenuation coefficient for [first sound](@entry_id:144225), $\alpha_I$, which is proportional to viscosity, scales as $\alpha_I(T) \propto T^{-2}$. If other scattering mechanisms are present, the temperature dependence can change. For instance, in a hypothetical scenario where sound waves also scatter off a dilute gas of collective modes whose density is proportional to $T^2$, this second channel would contribute an attenuation term $\alpha_{II}(T) \propto T^2$. The total attenuation $\alpha(T) = \alpha_I + \alpha_{II}$ would then exhibit a minimum at a temperature $T_{min} = (\mathcal{A}/\mathcal{B})^{1/4}$, where $\mathcal{A}$ and $\mathcal{B}$ are constants for the two processes [@problem_id:267750]. This illustrates how [sound attenuation](@entry_id:189896) measurements can serve as a sensitive probe of the dominant scattering mechanisms in a material.

### Zero Sound: The Collisionless Mode

When $\omega\tau \gg 1$, the concept of a local pressure wave becomes ill-defined. Instead, a collective excitation can be sustained by the [mean-field interaction](@entry_id:200557) itself. This is [zero sound](@entry_id:142772). Imagine a slight forward displacement of a group of quasiparticles on one side of the Fermi sea. Through the [mean-field interaction](@entry_id:200557) potential, these quasiparticles create an attractive potential "wake" behind them. This potential then pulls other quasiparticles along, creating a self-sustaining ripple—a distortion of the Fermi surface that propagates through the system.

This mechanism can be formally described by the linearized Landau-Boltzmann kinetic equation in the collisionless limit. For a longitudinal (density) wave, this leads to a [dispersion relation](@entry_id:138513) that connects the sound velocity to the [interaction parameters](@entry_id:750714). For a simple model with only an isotropic interaction $F_0^s$, the velocity $c_0$ of [zero sound](@entry_id:142772) is found by solving for the dimensionless speed $s = c_0/v_F$:

$$
\frac{1}{F_0^s} = g(s) = \frac{s}{2} \ln\left(\frac{s+1}{s-1}\right) - 1
$$

A critical requirement for an undamped, propagating mode is that its velocity must exceed the Fermi velocity, $c_0 > v_F$, or $s>1$. If $s \le 1$, the wave would be moving slower than the fastest quasiparticles and could efficiently lose energy by exciting individual particle-hole pairs. This dissipation mechanism is known as **Landau damping**. By analyzing the function $g(s)$, one finds that it is positive and monotonically decreasing for $s \in (1, \infty)$, spanning the range from $+\infty$ (as $s \to 1^+$) to $0$ (as $s \to \infty$). Therefore, a solution $s>1$ exists if and only if $1/F_0^s > 0$, which implies **$F_0^s > 0$** [@problem_id:277766]. This is a profound result: longitudinal [zero sound](@entry_id:142772) can only propagate if the quasiparticle interactions are, on average, repulsive.

The specific solution depends on the dimensionality and the value of $F_0^s$. For a two-dimensional Fermi liquid, an analogous derivation from the kinetic equation yields a [closed-form expression](@entry_id:267458) for the [zero sound](@entry_id:142772) speed [@problem_id:267649]:

$$
c_0 = v_F \frac{F_0^s + 1}{\sqrt{2F_0^s + 1}}
$$

This expression again confirms that for $F_0^s > 0$, we have $c_0 > v_F$, satisfying the condition to avoid Landau damping.

The full [dispersion relation](@entry_id:138513), which bridges the hydrodynamic and collisionless regimes, can be derived by including a [relaxation-time approximation](@entry_id:138429) for the [collision integral](@entry_id:152100) in the Boltzmann equation. This general equation reveals a rich variety of solutions beyond the simple propagating modes. For instance, under specific conditions, the system can support purely diffusive (non-propagating) modes. One such mode occurs when the dimensionless velocity equals the dimensionless collision parameter, $s=a$, where $a=i/(\omega\tau)$. This exotic solution requires the Landau parameter to take on a specific frequency-dependent value, $F_0^s = -1 + \frac{\pi}{2\omega\tau}$ [@problem_id:267672]. Furthermore, for strongly attractive interactions ($F_0^s  -1$), where the system is unstable towards collapse, the theory predicts an [overdamped](@entry_id:267343) mode with a purely [imaginary frequency](@entry_id:153433) $\omega = -i\gamma$, whose damping rate $\gamma$ can be calculated [@problem_id:267772].

### Varieties of Zero Sound

The concept of [zero sound](@entry_id:142772) is not restricted to longitudinal density fluctuations. Any persistent distortion of the quasiparticle distribution on the Fermi surface can, in principle, propagate as a wave, provided the interactions are suitable. This leads to a rich zoology of [zero sound](@entry_id:142772) modes.

#### Spin Zero Sound
If we consider a fluctuation in spin polarization rather than density, a **spin [zero sound](@entry_id:142772)** can propagate. This is a wave of traveling spin density. Its dynamics are governed by the spin-antisymmetric Landau parameter, $F_0^a$. The dispersion relation takes the same form as for density [zero sound](@entry_id:142772), but with $F_0^s$ replaced by $F_0^a$. Consequently, a propagating spin [zero sound](@entry_id:142772) mode requires repulsive spin-channel interactions, $F_0^a > 0$. In the limit of strong interactions ($F_0^s, F_0^a \gg 1$), the velocities of the two modes are related in a simple way. The velocity of density [zero sound](@entry_id:142772) becomes $c_0 \approx v_F \sqrt{F_0^s/3}$, while the velocity of spin [zero sound](@entry_id:142772) is $c_{s0} \approx v_F \sqrt{F_0^a/3}$. Their ratio is therefore given by $c_{s0}/c_0 \approx \sqrt{F_0^a/F_0^s}$ [@problem_id:267651].

#### Transverse Zero Sound
Perhaps more surprisingly, Fermi liquids can also support **transverse [zero sound](@entry_id:142772)**, which is a propagating shear wave. A classical fluid cannot support shear waves, as it has no restoring force against shear stress. In a Fermi liquid, however, the [mean field](@entry_id:751816) can provide such a restoring force. This mode's existence and velocity are governed by the $\ell=1$ Landau parameter, $F_1^s$. The dispersion relation is more complex, but an analysis reveals that a transverse mode emerges when $F_1^s$ is sufficiently large and positive. The critical value for the emergence of transverse [zero sound](@entry_id:142772) with a velocity infinitesimally above $v_F$ is $F_1^s > 6$ [@problem_id:267748].

#### Higher-Order Zero Sound
The principle can be extended to distortions of the Fermi surface with higher angular momentum character. For instance, one can consider a d-wave ($\ell=2$) distortion, described by the second Legendre polynomial. The propagation of such a mode would be governed by the Landau parameter $F_2^s$. Again, a propagating mode only exists if the interaction is sufficiently repulsive, $F_2^s > 0$. In the limit of very [strong interaction](@entry_id:158112) ($F_2^s \gg 1$), the velocity of this d-wave [zero sound](@entry_id:142772) is approximately $v_F \sqrt{5F_2^s/3}$ [@problem_id:267678].

In summary, [first sound](@entry_id:144225) represents the [hydrodynamic limit](@entry_id:141281) of density propagation, governed by thermodynamics and dissipated by collisions. Zero sound, in its various forms (longitudinal, spin, transverse, etc.), represents a fundamentally quantum-mechanical collective mode of the Fermi surface itself, sustained by mean-field interactions in the collisionless limit. The study of these sound modes provides an invaluable experimental and theoretical window into the nature and strength of quasiparticle interactions that define a Fermi liquid.