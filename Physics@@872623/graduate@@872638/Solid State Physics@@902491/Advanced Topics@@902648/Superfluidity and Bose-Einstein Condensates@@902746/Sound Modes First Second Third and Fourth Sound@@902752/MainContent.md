## Introduction
In the counterintuitive realm of quantum mechanics, certain fluids cooled to near absolute zero enter a state of superfluidity, exhibiting extraordinary properties like [frictionless flow](@entry_id:195983). One of their most remarkable features is the ability to support multiple types of "sound," collective wave phenomena that go far beyond the conventional pressure waves we experience daily. The existence of a "[temperature wave](@entry_id:193534)," known as second sound, challenges classical intuition and highlights the need for a specific theoretical framework to understand the rich dynamics of these [quantum fluids](@entry_id:140332).

This article provides a comprehensive exploration of the four primary sound modes in superfluids. The following chapters will systematically build your understanding of this fascinating topic.

- **Principles and Mechanisms** will introduce the foundational two-fluid model, using it to derive the physical origins and characteristics of first, second, third, and [fourth sound](@entry_id:158255). We will examine how their properties are determined by the underlying thermodynamics of the superfluid state.

- **Applications and Interdisciplinary Connections** will demonstrate how these sound modes are utilized as precise experimental probes to measure fundamental superfluid properties. We will also explore surprising connections to other scientific fields, showcasing [superfluids](@entry_id:180718) as tabletop laboratories for [acoustic metamaterials](@entry_id:174319) and even analogues for black hole physics.

- **Hands-On Practices** will offer a selection of problems, allowing you to apply the theoretical concepts to practical scenarios involving resonant cavities and [wave propagation](@entry_id:144063) in various superfluid setups.

We begin by delving into the principles and mechanisms that govern these unique quantum waves.

## Principles and Mechanisms

The existence of a superfluid state, characterized by the condensation of a macroscopic number of particles into a single quantum ground state, gives rise to a rich spectrum of collective excitations and wave phenomena. These phenomena are elegantly described by the **[two-fluid model](@entry_id:139846)**, which posits that a superfluid acts as an intimate mixture of two interpenetrating components: a **superfluid component** with density $\rho_s$ and velocity $\mathbf{v}_s$, which possesses zero viscosity and zero entropy, and a **[normal fluid](@entry_id:183299) component** with density $\rho_n$ and velocity $\mathbf{v}_n$, which behaves like a conventional viscous fluid and carries all of the system's entropy. The total mass density is simply the sum of the two, $\rho = \rho_s + \rho_n$. The relative proportions of these two components are temperature-dependent, with $\rho_s \to \rho$ as the temperature $T \to 0$ and $\rho_s \to 0$ as $T$ approaches the critical temperature $T_\lambda$.

The dynamics of these two fluids, and consequently the wave modes they support, are governed by a set of coupled hydrodynamic equations. In the limit of small-amplitude oscillations (the linear regime), these equations provide the foundation for understanding the various "sounds" in [superfluids](@entry_id:180718).

### First Sound: A Conventional Pressure Wave

The most familiar of these modes is **[first sound](@entry_id:144225)**. It is analogous to ordinary sound in a conventional fluid. In this mode, the superfluid and normal fluid components oscillate **in phase**, meaning $\mathbf{v}_s = \mathbf{v}_n$. This collective motion results in a local variation of the total density, $\rho$. Consequently, [first sound](@entry_id:144225) is a longitudinal wave of pressure and density. Its propagation speed, $c_1$, is determined by the [adiabatic compressibility](@entry_id:139833) of the liquid, given by the standard thermodynamic relation:

$c_1^2 = \left(\frac{\partial P}{\partial \rho}\right)_s$

where the derivative is taken at constant entropy per unit mass, $s$. First sound can be excited by conventional means, such as an oscillating diaphragm, which creates a local density compression.

### Second Sound: A Wave of Temperature and Entropy

A phenomenon unique to [superfluids](@entry_id:180718) is **second sound**. Unlike [first sound](@entry_id:144225), it is not a pressure wave but a **[temperature wave](@entry_id:193534)**. This remarkable mode arises when the two fluid components oscillate **out of phase**. Specifically, the motions are such that the total mass current remains zero, preserving a constant overall density. This condition is expressed as:

$\mathbf{j} = \rho_s \mathbf{v}_s + \rho_n \mathbf{v}_n = 0$

Since the [normal fluid](@entry_id:183299) carries all the entropy, its motion constitutes an entropy current. The [counterflow](@entry_id:156755) of the zero-entropy superfluid component ensures that the total density does not change, yet there is a propagating disturbance in the local entropy and, consequently, temperature.

To derive the speed of second sound, $c_2$, we examine the linearized two-fluid equations under this zero mass-current condition [@problem_id:213308]. The fundamental equations are the conservation of entropy and the equation of motion for the superfluid component. The linearized [entropy conservation](@entry_id:749018) equation is:

$\frac{\partial s}{\partial t} + s_0 \nabla \cdot \mathbf{v}_n = 0$

where $s$ is the specific entropy and $s_0$ is its equilibrium value. The superfluid accelerates in response to a gradient in the chemical potential, $\mu$:

$\frac{\partial \mathbf{v}_s}{\partial t} = -\nabla \mu$

Using the [thermodynamic identity](@entry_id:142524) $d\mu = -s dT + \frac{1}{\rho} dP$ and the fact that pressure fluctuations are negligible for second sound ($dP \approx 0$), the superfluid acceleration becomes driven by a temperature gradient: $\frac{\partial \mathbf{v}_s}{\partial t} \approx s_0 \nabla T$.

By combining these equations with the zero mass-current condition, which implies $\mathbf{v}_n = -(\rho_s / \rho_n) \mathbf{v}_s$, and relating entropy fluctuations to temperature fluctuations via the specific heat at constant volume, $c_v = T (\partial s / \partial T)_V$, one can derive a wave equation for the entropy (or temperature). The result is the classic wave equation:

$\frac{\partial^2 s}{\partial t^2} = c_2^2 \nabla^2 s$

where the squared velocity of second sound is given by:

$c_2^2 = \frac{\rho_s}{\rho_n} \frac{s^2 T}{c_v}$

This equation reveals that the propagation of a [thermal wave](@entry_id:152862) is a direct consequence of the two-fluid nature of the superfluid state.

#### Microscopic Origins and Temperature Dependence of Second Sound

The velocity of [second sound](@entry_id:147020) is strongly dependent on temperature because the quantities $\rho_s$, $\rho_n$, $s$, and $c_v$ all vary with $T$. These thermodynamic quantities are determined by the gas of [elementary excitations](@entry_id:140859) ([phonons and rotons](@entry_id:146031)) that constitutes the [normal fluid](@entry_id:183299).

At very low temperatures (below approximately $0.6$ K in $^4\text{He}$), the normal fluid is dominated by a gas of **phonons**—the quanta of [first sound](@entry_id:144225)—which have a [linear dispersion relation](@entry_id:266313) $\epsilon(p) = c_1 p$. By analyzing the thermodynamic properties of this [phonon gas](@entry_id:147597), we can predict the low-temperature behavior of $c_2$ [@problem_id:213405]. The energy density of the [phonon gas](@entry_id:147597) is proportional to $T^4$, leading to specific relationships for entropy, specific heat, and the normal fluid density. Substituting these into the formula for $c_2^2$ yields a remarkable and simple result:

$c_2 = \frac{c_1}{\sqrt{3}}$

This prediction, confirmed by experiment, is a triumph of Landau's theory of superfluidity. It directly links the velocity of the exotic [temperature wave](@entry_id:193534) to that of ordinary sound.

As the temperature rises (towards $1$ K), **[rotons](@entry_id:158760)** become the dominant [elementary excitations](@entry_id:140859). These excitations have a more complex [dispersion relation](@entry_id:138513), characterized by an energy gap $\Delta$: $\epsilon(p) = \Delta + (p-p_0)^2/(2\mu)$. Since the number of [rotons](@entry_id:158760) grows exponentially with temperature, $\exp(-\Delta/k_B T)$, they rapidly come to dominate the thermodynamic properties of the [normal fluid](@entry_id:183299). Calculating the entropy and specific heat from the [roton](@entry_id:140066) gas model allows for the determination of the [second sound](@entry_id:147020) velocity in this regime [@problem_id:213404]. The result is a complex function of temperature, but it simplifies to $c_2^2 = 3(k_B T/p_0)^2$, showing that $c_2$ initially rises linearly with temperature in the [roton](@entry_id:140066)-dominated regime before eventually decreasing as $\rho_s$ diminishes near $T_\lambda$.

#### The Thermomechanical and Fountain Effects

The same [thermodynamic coupling](@entry_id:170539) that gives rise to second sound also produces the striking **[thermomechanical effect](@entry_id:144463)**. The fundamental relation $d\mu = (1/\rho)dP - s dT$ implies that a gradient in temperature can be balanced by a gradient in pressure to maintain a constant chemical potential. If two reservoirs of superfluid are connected by a "superleak"—a channel so narrow that the viscous normal component is immobilized—only the superfluid component can flow. Imposing a temperature difference $\Delta T$ across the superleak will drive a superfluid flow to the hotter side, building up a pressure difference $\Delta P$ until equilibrium is reached. This equilibrium condition, $\nabla \mu = 0$, leads to the London equation:

$\Delta P = \rho s \Delta T$

This phenomenon is dramatically demonstrated in the **[fountain effect](@entry_id:199881)**, where heating a reservoir connected to a superleak can generate a pressure sufficient to create a fountain of helium. The magnitude of this pressure can be calculated from first principles. For instance, in the low-temperature phonon-dominated regime, the entropy per unit mass is $s \propto T^3$, allowing for a direct calculation of the pressure difference from the [phonon gas](@entry_id:147597) properties [@problem_id:213386].

### Sound in Confined Geometries and Mixtures

The spectrum of sound modes is further enriched when the superfluid is placed in confined geometries or when impurities are introduced.

#### Third Sound: Waves on a Superfluid Film

When a superfluid forms a thin film on a solid surface, a new wave mode called **[third sound](@entry_id:187597)** can propagate. In this mode, the viscous [normal fluid](@entry_id:183299) is effectively clamped to the substrate due to its viscosity, while the superfluid component is free to move. Third sound is a surface wave involving oscillations in the **thickness of the film** coupled with oscillations in its temperature. The restoring force for the thickness oscillation can arise from gravity or, more commonly for very [thin films](@entry_id:145310), from the van der Waals interaction with the substrate.

To understand the mechanism, consider a simplified model where the restoring force is due solely to a van der Waals potential of the form $U(d) = -\gamma/d^n$, where $d$ is the film thickness [@problem_id:213387]. This potential contributes to the chemical potential of the film. A local change in film thickness $\delta d$ creates a [chemical potential gradient](@entry_id:142294), $\nabla(\delta\mu)$, which then drives a superfluid flow according to the acceleration equation. This flow, in turn, alters the film thickness elsewhere, as described by the [mass conservation](@entry_id:204015) equation. Combining these dynamics yields a wave equation for the film thickness. The resulting wave propagates with a speed $c_3$ given by:

$c_3^2 = \frac{\rho_s n \gamma}{\rho d_0^n}$

where $d_0$ is the equilibrium film thickness. This shows how the propagation speed is directly tied to the strength of the substrate interaction and the superfluid fraction.

#### Fourth Sound: Pressure Waves in a Superleak

If a superfluid fills a porous medium or a packed powder with channels fine enough to immobilize the normal component (a superleak), the condition $\mathbf{v}_n = 0$ holds throughout the bulk. In this situation, the superfluid component can still support a pressure-[density wave](@entry_id:199750), which is known as **[fourth sound](@entry_id:158255)**. Unlike second sound, where density is constant, [fourth sound](@entry_id:158255) involves oscillations in both pressure and density, much like [first sound](@entry_id:144225). However, since only the superfluid component participates in the motion, its velocity differs from $c_1$.

A straightforward derivation based on the linearized equations for [mass conservation](@entry_id:204015) and superfluid acceleration under the condition $\mathbf{v}_n = 0$ yields a wave equation for the [density perturbations](@entry_id:159546) [@problem_id:213403]. The velocity of [fourth sound](@entry_id:158255), $c_4$, is found to be:

$c_4^2 = \frac{\rho_s}{\rho} c_1^2$

This simple result shows that the velocity is reduced from that of [first sound](@entry_id:144225) by a factor related to the superfluid fraction, which is intuitive as only that fraction of the fluid is oscillating. A more complete thermodynamic analysis reveals a coupling to thermal effects, leading to a more general expression that connects [fourth sound](@entry_id:158255) to both first and second sound [@problem_id:213385]:

$c_4^2 = \frac{\rho_s c_1^2 + \rho_n c_2^2}{\rho}$

This formula beautifully illustrates the hybrid nature of [fourth sound](@entry_id:158255): it is primarily a pressure wave (like [first sound](@entry_id:144225)) but carries a thermal component (like second sound) because the oscillating [superfluid density](@entry_id:142018) forces a local temperature change that cannot be equilibrated by the clamped normal fluid.

#### Second Sound in $^3\text{He}$-$^4\text{He}$ Mixtures

Adding $^3\text{He}$ impurities to superfluid $^4\text{He}$ provides another knob for tuning the properties of the normal fluid. The $^3\text{He}$ atoms do not participate in the [superfluid condensate](@entry_id:755648) and behave as quasiparticles that contribute to the [normal fluid](@entry_id:183299) density, entropy, and specific heat. At sufficiently low temperatures, these impurities can dominate the thermodynamic properties over the native [phonons and rotons](@entry_id:146031).

Treating the $^3\text{He}$ impurities as a degenerate Fermi gas allows for the calculation of their contribution to the [normal fluid](@entry_id:183299) [@problem_id:213285]. By substituting the entropy and [specific heat](@entry_id:136923) of a degenerate Fermi gas into the formula for [second sound](@entry_id:147020), one finds that the velocity becomes dependent on the $^3\text{He}$ concentration $n_3$ and is directly proportional to temperature, with a proportionality constant set by fundamental constants and the impurity concentration.

### Advanced Perspectives and Dissipative Effects

While the hydrodynamic two-fluid model is remarkably successful, modern condensed matter physics offers more abstract and powerful frameworks for understanding these phenomena.

#### An Effective Field Theory Approach

From a [field theory](@entry_id:155241) perspective, the sound modes of a superfluid are the **Goldstone bosons** associated with spontaneously broken symmetries. Second sound, in particular, can be described using an effective Lagrangian for the low-energy degrees of freedom. In a simplified model that neglects [first sound](@entry_id:144225), these degrees of freedom are the superfluid phase $\pi(x,t)$ and an entropic mode $\psi(x,t)$. The dynamics are captured by a Lagrangian of the form [@problem_id:213242]:

$L = \frac{1}{2} A (\dot{\pi})^2 + B \dot{\pi} \dot{\psi} + \frac{1}{2} C (\dot{\psi})^2 - \frac{1}{2} \rho_s (\nabla \pi)^2$

Here, the coefficients $A$, $B$, and $C$ are thermodynamic susceptibilities, such as compressibility and [specific heat](@entry_id:136923). By deriving and solving the Euler-Lagrange equations of motion for this system, one can find the [dispersion relation](@entry_id:138513) of the collective modes. This analysis yields the squared velocity of the propagating mode, which corresponds to second sound:

$c_2^2 = \frac{\rho_s C}{AC - B^2}$

This result, when the coefficients are mapped back to standard thermodynamic quantities, reproduces the hydrodynamic formula, demonstrating the power and consistency of the [effective field theory](@entry_id:145328) framework.

#### Attenuation of Sound Waves

The idealized picture of undamped [wave propagation](@entry_id:144063) must be corrected by including dissipative processes inherent in the normal fluid, such as viscosity and thermal conductivity. These effects lead to the **attenuation** of the sound waves. For [second sound](@entry_id:147020), the primary dissipative mechanism is the thermal conductivity $\kappa$ of the normal fluid. Including the corresponding heat flux term in the [entropy conservation](@entry_id:749018) equation modifies the wave equation [@problem_id:213306].

Solving for the [dispersion relation](@entry_id:138513) with this dissipative term reveals that the [wavevector](@entry_id:178620) $k$ becomes complex, $k = k_R + i\alpha$. The imaginary part, $\alpha$, is the attenuation coefficient, which describes the [exponential decay](@entry_id:136762) of the wave's amplitude as it propagates. For small dissipation, the attenuation coefficient for [second sound](@entry_id:147020) is found to be:

$\alpha = \frac{\kappa \omega^2}{2 \rho C_P u_2^3}$

This characteristic $\omega^2$ dependence on frequency is a hallmark of attenuation from such dissipative processes and highlights how real-world imperfections modify the ideal wave phenomena predicted by the [two-fluid model](@entry_id:139846).