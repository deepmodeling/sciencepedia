## Introduction
Superfluids represent a fascinating state of matter where the strange rules of quantum mechanics become manifest on a macroscopic scale. Defined by their ability to flow without any viscosity, these [quantum fluids](@entry_id:140332) exhibit behaviors that defy classical intuition, such as creeping up the walls of their container or forming intricate arrays of quantized whirlpools when rotated. Understanding these phenomena requires moving beyond traditional fluid dynamics into a rich theoretical landscape that connects thermodynamics, [many-body quantum mechanics](@entry_id:138305), and topology. This article addresses the fundamental question of how to describe the motion of these remarkable systems.

This article provides a comprehensive overview of [superfluid dynamics](@entry_id:196160), designed to bridge foundational theory with cutting-edge applications. First, in **Principles and Mechanisms**, we will build the theoretical toolkit needed to understand superfluidity, starting with the elegant [two-fluid model](@entry_id:139846) and the Landau criterion for [frictionless flow](@entry_id:195983), and connecting them to their microscopic origins in quantum [field theory](@entry_id:155241). We will investigate signature phenomena like [quantized vortices](@entry_id:147055) and the mechanisms that lead to the breakdown of superflow. Next, in **Applications and Interdisciplinary Connections**, we will explore how these core principles are applied across a vast scientific landscape, from the rich phenomenology of liquid helium and engineered Bose-Einstein condensates to the exotic interiors of neutron stars and theories of the early universe. Finally, **Hands-On Practices** will provide an opportunity to actively engage with these concepts by solving key problems related to vortex interactions and the collective motion of [quantum fluids](@entry_id:140332).

## Principles and Mechanisms

This chapter delves into the fundamental principles and microscopic mechanisms that govern the remarkable dynamics of superfluids. Building upon the introductory concepts, we will construct a robust theoretical framework, starting with the phenomenological two-fluid model and the intrinsic conditions for [frictionless flow](@entry_id:195983). We will then connect this macroscopic picture to its microscopic origins in the quantum mechanics of [many-body systems](@entry_id:144006). Finally, we will explore the signature phenomena of superfluidity, such as macroscopic [quantum coherence](@entry_id:143031) and [quantized vortices](@entry_id:147055), and investigate the mechanisms by which superflow can break down.

### The Two-Fluid Model and the Landau Criterion for Superfluidity

The behavior of superfluids, particularly [liquid helium](@entry_id:139440) below its [lambda transition](@entry_id:139776), is elegantly captured by the **two-fluid model**. This model posits that the fluid behaves as if it were a mixture of two distinct, interpenetrating components:

1.  A **superfluid component** with density $\rho_s$ and velocity $\mathbf{v}_s$. This component is characterized by zero viscosity and zero entropy. It flows without any dissipation.

2.  A **[normal fluid](@entry_id:183299) component** with density $\rho_n$ and velocity $\mathbf{v}_n$. This component behaves like a classical viscous fluid and carries the entire entropy of the system. Microscopically, it is understood as a gas of the system's [elementary excitations](@entry_id:140859) (quasiparticles).

The total density of the fluid is $\rho = \rho_s + \rho_n$, and the total momentum density is $\mathbf{J} = \rho_s \mathbf{v}_s + \rho_n \mathbf{v}_n$. The proportions of the two components are temperature-dependent; at absolute zero, $\rho_n \to 0$ and $\rho \to \rho_s$, while as the temperature approaches the critical temperature $T_c$, $\rho_s \to 0$.

The central question of [superfluidity](@entry_id:146323) is: why can the superfluid component flow without dissipation? The answer was provided by Lev Landau through a beautifully simple and general argument. Consider a superfluid flowing with velocity $\mathbf{v}$ through a stationary channel. For the flow to dissipate kinetic energy, the fluid must be able to transition to a lower energy state. The most basic way to do this is by creating an elementary excitation within the fluid.

Let us analyze the energetics of this process from the perspective of the stationary channel (the [lab frame](@entry_id:181186)). In the rest frame of the fluid, an elementary excitation is characterized by its energy $\epsilon(p)$ and momentum $\mathbf{p}$. Due to Galilean invariance, the energy of this excitation in the lab frame is not simply $\epsilon(p)$. If we create an excitation with momentum $\mathbf{p}$ in the fluid that is moving at velocity $\mathbf{v}$, the change in the total energy of the system in the [lab frame](@entry_id:181186) is:
$$
\Delta E = \epsilon(p) + \mathbf{p} \cdot \mathbf{v}
$$
The flow remains superfluid and non-dissipative as long as it is not energetically favorable to create any excitation, meaning $\Delta E > 0$ for all possible excitations. Dissipation can only occur if, for some excitation, $\Delta E \leq 0$. The condition for dissipation is therefore:
$$
\epsilon(p) + \mathbf{p} \cdot \mathbf{v} \leq 0
$$
To find the lowest flow velocity $v = |\mathbf{v}|$ at which this can happen, we consider the most favorable case for dissipation, which occurs when the momentum of the excitation $\mathbf{p}$ is directed opposite to the flow velocity $\mathbf{v}$. In this case, $\mathbf{p} \cdot \mathbf{v} = -pv$, and the condition for dissipation becomes $\epsilon(p) - pv \leq 0$, or $v \geq \epsilon(p)/p$.

The flow will be perfectly superfluid as long as the velocity $v$ is less than the minimum value of the ratio $\epsilon(p)/p$ for any possible excitation momentum $p > 0$. This defines the **Landau critical velocity**, $v_c$:
$$
v_c = \min_{p>0} \left( \frac{\epsilon(p)}{p} \right)
$$
If the flow velocity exceeds $v_c$, the creation of excitations becomes energetically possible, leading to the breakdown of superfluidity. The value of $v_c$ is therefore determined entirely by the **[dispersion relation](@entry_id:138513)** $\epsilon(p)$ of the system's [elementary excitations](@entry_id:140859). For a simple dispersion like $\epsilon(p) = p^2/(2m)$, the ratio $\epsilon(p)/p = p/(2m)$ approaches zero as $p \to 0$, implying $v_c = 0$. This explains why a [free particle](@entry_id:167619) gas cannot be a superfluid. A non-zero critical velocity requires that the ratio $\epsilon(p)/p$ has a finite minimum for $p>0$.

As a concrete example, consider a hypothetical superfluid whose excitations are described by a [roton](@entry_id:140066)-like dispersion relation, as is found in liquid Helium-4 [@problem_id:492049]. Let this dispersion be modeled by:
$$
\epsilon(p) = \Delta + \frac{(p - p_0)^2}{2\mu}
$$
Here, $\Delta > 0$ is an energy gap, $p_0 > 0$ is a characteristic momentum, and $\mu > 0$ is an effective mass. To find the critical velocity, we must find the minimum of the function $f(p) = \epsilon(p)/p$. We compute the derivative and set it to zero:
$$
\frac{df}{dp} = \frac{d}{dp} \left( \frac{\Delta}{p} + \frac{p}{2\mu} - \frac{p_0}{\mu} + \frac{p_0^2}{2\mu p} \right) = -\frac{\Delta}{p^2} + \frac{1}{2\mu} - \frac{p_0^2}{2\mu p^2} = 0
$$
Solving for the momentum $p_{min}$ that minimizes this ratio gives $p_{min}^2 = p_0^2 + 2\mu\Delta$. Substituting this back into the expression for velocity, $v_c = f(p_{min})$, and simplifying yields the Landau critical velocity for this system:
$$
v_c = \frac{\sqrt{p_0^2 + 2\mu\Delta} - p_0}{\mu}
$$
This result demonstrates explicitly how the specific features of the [excitation spectrum](@entry_id:139562)—in this case, the "[roton minimum](@entry_id:138478)" characterized by $\Delta$, $p_0$, and $\mu$—determine the intrinsic limit for stable, [frictionless flow](@entry_id:195983).

### The Microscopic Picture: Quasiparticles and Condensate Depletion

The two-fluid model provides a powerful macroscopic description, but its components, $\rho_s$ and $\rho_n$, have a deeper microscopic origin. In [superfluids](@entry_id:180718) formed from Bose-Einstein condensation, the superfluid component is associated with the macroscopic population of the ground state (the condensate), while the normal fluid is the gas of thermally excited quasiparticles.

In a weakly-interacting Bose gas, the nature of these quasiparticles is revealed by the **Bogoliubov theory**. For an ideal Bose gas, all particles would occupy the zero-momentum ground state at zero temperature. However, inter-particle interactions modify this picture significantly. Even at absolute zero, these interactions cause some particles to be scattered out of the condensate into states with non-zero momentum. This effect is known as **[quantum depletion](@entry_id:139939)**.

The Bogoliubov approximation diagonalizes the Hamiltonian of the interacting gas, revealing that its elementary excitations are not the original bosons but new entities called **Bogoliubov quasiparticles**. The ground state of the interacting system is, in fact, the vacuum state for these quasiparticles. The number of "real" particles outside the condensate can be calculated by finding the expectation value of the [number operator](@entry_id:153568) for non-zero momentum states, $a_{\mathbf{k}}^{\dagger}a_{\mathbf{k}}$, in this new ground state.

This calculation shows that the density of depleted atoms, $n_{ex}$, relative to the condensate density, $n_0$, depends on the strength of the interactions [@problem_id:491997]. For a dilute Bose gas characterized by the [s-wave scattering length](@entry_id:142891) $a$, the condensate depletion fraction at zero temperature is found to be:
$$
\frac{n_{ex}}{n_0} = \frac{8}{3\sqrt{\pi}}\sqrt{n_0a^3}
$$
The dimensionless parameter $n_0a^3$ represents the "gas parameter," which must be small for the theory to be valid. This result is profound: it demonstrates that the ground state of an interacting superfluid is not a simple condensate but a complex correlated state containing a "sea" of virtual and real excitations.

At finite temperatures, thermal energy creates additional quasiparticles, which constitute the [normal fluid](@entry_id:183299). The density of this normal fluid component, $\rho_n$, can be calculated directly from the statistical mechanics of the quasiparticle gas. By considering the momentum carried by the gas in a frame moving with velocity $\mathbf{v}_n$, one can derive a general formula for the [normal fluid](@entry_id:183299) density tensor:
$$
(\rho_n)_{ij} = - \int \frac{d^3p}{(2\pi\hbar)^3} \, p_i p_j \, \frac{\partial n(\epsilon_{\mathbf{p}})}{\partial \epsilon_{\mathbf{p}}}
$$
where $n(\epsilon_{\mathbf{p}})$ is the Bose-Einstein distribution for quasiparticles with energy $\epsilon_{\mathbf{p}}$. This formula provides a direct bridge between the microscopic quasiparticle properties and a macroscopic parameter of the [two-fluid model](@entry_id:139846).

For example, for a superfluid with anisotropic low-energy [phonon excitations](@entry_id:159714), where the dispersion relation is $\epsilon(\mathbf{p}) = \sqrt{c_x^2 p_x^2 + c_y^2 p_y^2 + c_z^2 p_z^2}$, we can calculate the components of the density tensor [@problem_id:492047]. By performing the integration over the phonon distribution at low temperatures, the component $(\rho_n)_{zz}$ is found to be:
$$
(\rho_n)_{zz} = \frac{2\pi^2}{45}\,\frac{(k_B T)^4}{\hbar^3\,c_x\,c_y\,c_z^3}
$$
The strong $T^4$ dependence is a characteristic signature of a phonon-dominated [normal fluid](@entry_id:183299), analogous to the Stefan-Boltzmann law for photons. This calculation powerfully illustrates how the macroscopic properties of the superfluid system are determined by the underlying nature of its elementary excitations.

### Macroscopic Quantum Phenomena

The description of a superfluid by a single [macroscopic wavefunction](@entry_id:143853), $\Psi(\mathbf{x}, t) = \sqrt{n(\mathbf{x}, t)} e^{i\theta(\mathbf{x}, t)}$, implies that the phase $\theta$ is a coherent, physical degree of freedom across the entire system. This [phase coherence](@entry_id:142586) gives rise to extraordinary dynamical phenomena that have no counterpart in classical fluids.

#### Second Sound

One of the most striking predictions of the two-fluid model is the existence of **[second sound](@entry_id:147020)**. While ordinary sound (or "[first sound](@entry_id:144225)") is a propagating wave of pressure and density, [second sound](@entry_id:147020) is a wave of temperature and entropy. In a second sound wave, the superfluid and [normal fluid](@entry_id:183299) components oscillate out of phase in a specific manner: they engage in a [counterflow](@entry_id:156755) such that the total mass current is zero, i.e., $\rho_s \mathbf{v}_s' + \rho_n \mathbf{v}_n' = 0$ (where primes denote small perturbations from equilibrium). This condition ensures that the total density $\rho$ remains nearly constant, and consequently, there are minimal pressure fluctuations.

The physical mechanism is intuitive: if a local hot spot appears in the superfluid, the concentration of the [normal fluid](@entry_id:183299) (quasiparticles) increases. To restore equilibrium, the normal fluid flows away from the hot spot, carrying entropy with it. To conserve mass locally, the superfluid component must flow towards the hot spot. This coupled counter-oscillatory motion of the two fluids propagates as a wave.

The speed of this [temperature wave](@entry_id:193534), $c_2$, can be derived directly from the linearized hydrodynamic equations of the [two-fluid model](@entry_id:139846) [@problem_id:492057]. By combining the superfluid [equation of motion](@entry_id:264286), the [entropy conservation](@entry_id:749018) equation, and the relevant [thermodynamic relations](@entry_id:139032) under the conditions of zero pressure perturbation ($P' \approx 0$) and zero total mass current, we can derive a wave equation for the temperature perturbation $T'$. The resulting equation is of the form:
$$
\frac{\partial^2 T'}{\partial t^2} - c_2^2 \nabla^2 T' = 0
$$
From this, we identify the speed of second sound as:
$$
c_2 = \sqrt{\frac{T s^2 \rho_s}{\rho_n C_V}}
$$
where $s$ is the equilibrium entropy per unit mass and $C_V$ is the specific [heat capacity at constant volume](@entry_id:147536). The experimental observation of [second sound](@entry_id:147020) in liquid Helium-II was a major triumph for the [two-fluid model](@entry_id:139846), confirming the reality of its distinct fluid components and their unique coupling.

#### The Josephson Effect

The [phase coherence](@entry_id:142586) of a superfluid becomes particularly evident when two superfluid reservoirs are connected by a "weak link," a barrier through which particles can quantum mechanically tunnel. This setup is known as a **superfluid Josephson junction**. The dynamics of such a system reveal a deep relationship between the particle current and the [phase difference](@entry_id:270122) across the junction.

Let the two superfluids be described by macroscopic wavefunctions $\Psi_1 = \sqrt{N_1} e^{i\theta_1}$ and $\Psi_2 = \sqrt{N_2} e^{i\theta_2}$. Their coupling via tunneling is governed by a Schrödinger-like equation. If a constant chemical potential difference $\Delta\mu = \mu_1 - \mu_2$ is maintained across the junction, the quantum mechanical evolution equations predict that the phase difference, $\Delta\theta = \theta_2 - \theta_1$, evolves linearly with time [@problem_id:492015]:
$$
\frac{d(\Delta\theta)}{dt} = -\frac{\Delta\mu}{\hbar}
$$
This is the **AC Josephson relation**. It states that a DC "voltage" (chemical [potential difference](@entry_id:275724)) produces an AC "current" in the phase. The mass current $I_m$ flowing across the junction is, in turn, proportional to the sine of this [phase difference](@entry_id:270122). Integrating the phase evolution equation, $\Delta\theta(t) = \phi_0 - (\Delta\mu/\hbar)t$, where $\phi_0$ is the initial [phase difference](@entry_id:270122), gives an oscillating mass current:
$$
I_m(t) = I_c \sin\left(\phi_0 - \frac{\Delta\mu}{\hbar}t\right)
$$
Here, $I_c$ is a [critical current](@entry_id:136685) that depends on the strength of the tunneling coupling and the number of particles. This phenomenon, an oscillating current in response to a constant potential difference, is a direct and spectacular consequence of the [macroscopic phase coherence](@entry_id:199906) of the superfluid state.

### Quantized Vortices: The Superfluid's Response to Rotation

The single-valuedness of the [macroscopic wavefunction](@entry_id:143853) $\Psi$ imposes a powerful constraint on the superfluid velocity field $\mathbf{v}_s = (\hbar/m)\nabla\theta$. The velocity must be irrotational, meaning its curl must be zero everywhere: $\nabla \times \mathbf{v}_s = 0$. This immediately raises a paradox: how can a superfluid, contained in a rotating bucket, ever come into rotation with the container?

The resolution lies in the formation of [topological defects](@entry_id:138787) known as **[quantized vortices](@entry_id:147055)**. A vortex is a line-like region where the [superfluid density](@entry_id:142018) $n_s$ goes to zero. Outside this singular core, the fluid remains irrotational. However, the phase of the wavefunction $\theta$ changes by an integer multiple of $2\pi$ upon traversing a closed loop around the vortex line. This condition, $\oint \mathbf{v}_s \cdot d\mathbf{l} = \frac{\hbar}{m} \oint \nabla\theta \cdot d\mathbf{l} = \frac{h}{m} k$, means that the circulation is quantized in units of $\kappa = h/m$, where $k$ is an integer called the winding number.

By filling its volume with a lattice of these [quantized vortices](@entry_id:147055), a superfluid can mimic [solid-body rotation](@entry_id:191086) on a macroscopic scale, while remaining locally irrotational [almost everywhere](@entry_id:146631).

#### Vortex Structure

The structure of a [vortex core](@entry_id:159858) is determined by the balance between the kinetic energy of the circulating flow, which favors a larger core, and the interaction or "condensation" energy, which favors keeping the density uniform. In a weakly-interacting Bose-Einstein condensate at T=0, this balance is described by the **Gross-Pitaevskii equation (GPE)**.

For an idealized straight vortex line, the GPE can be solved to find the radial profile of the density. Far from the core, the density $n(r)$ approaches its bulk value $n_0$. The density deficiency, $n_0 - n(r)$, decays with distance from the core. A detailed analysis [@problem_id:491998] shows that for large $r$, this decay follows a power law:
$$
n_0 - n(r) \approx \frac{C}{r^2}, \quad \text{where} \quad C = \frac{\hbar^2 k^2}{2 m g}
$$
Here, $k$ is the [winding number](@entry_id:138707) and $g$ is the [interaction strength](@entry_id:192243) parameter. This result can be understood by recognizing that far from the core, the density is almost constant at $n_0$, so the chemical potential is $\mu \approx g n_0$. The GPE then shows that the density depletion must balance the kinetic energy of the circulating flow, which is proportional to $v_s^2 \propto (\hbar k / mr)^2$. This balance defines a [characteristic length](@entry_id:265857) scale over which the density recovers its bulk value, known as the **[healing length](@entry_id:139128)**, $\xi = \hbar/\sqrt{2mgn_0}$. The [healing length](@entry_id:139128) effectively sets the size of the [vortex core](@entry_id:159858).

#### Vortex Nucleation

Whether vortices form in a rotating superfluid is a matter of thermodynamics. In a frame rotating with angular velocity $\mathbf{\Omega}$, the stable state is the one that minimizes the free energy $F' = E - \mathbf{\Omega} \cdot \mathbf{L}$, where $E$ is the kinetic energy and $\mathbf{L}$ is the angular momentum.

Consider a superfluid in a cylindrical bucket rotating at a low [angular velocity](@entry_id:192539) $\Omega$. The fluid can remain at rest in the [lab frame](@entry_id:181186) ($E=0, L=0, F'=0$), as this is a locally stable state due to the energy barrier to create a vortex. However, as $\Omega$ increases, a critical point is reached where it becomes energetically favorable to create a single [quantized vortex](@entry_id:161003) along the [axis of rotation](@entry_id:187094) [@problem_id:491995]. The kinetic energy of a single vortex line of length $H$ in a cylinder of radius $R$ is $E_v = (\rho \kappa^2 H / 4\pi) \ln(R/a_0)$, where $a_0$ is the core radius. Its angular momentum is $L_v = \rho \kappa \pi R^2 H / (2\pi) = \rho\kappa R^2 H/2$. The free energy of this state is $F'_v = E_v - \Omega L_v$. The [vortex state](@entry_id:204018) becomes favorable when $F'_v  0$. The critical [angular velocity](@entry_id:192539) $\Omega_c$ at which the free energies of the two states are equal ($F'_v = 0$) is therefore:
$$
\Omega_c = \frac{E_v}{L_v} = \frac{\kappa}{2\pi R^2} \ln\left(\frac{R}{a_0}\right)
$$
Above this critical angular velocity, the ground state of the system contains at least one vortex. As $\Omega$ increases further, it becomes favorable to nucleate an increasing number of vortices, which arrange themselves into a [regular lattice](@entry_id:637446).

### Mechanisms for Dissipation and Breakdown of Superflow

While the Landau criterion defines an intrinsic critical velocity, in practice, superflow often breaks down at much lower speeds through processes involving [topological defects](@entry_id:138787) like vortices. These events provide a mechanism for the system to dissipate energy.

#### Vortex-Mediated Dissipation

In restricted geometries, such as narrow channels or [thin films](@entry_id:145310), the primary mechanism for the decay of a [persistent current](@entry_id:137094) is the [nucleation](@entry_id:140577) and motion of vortices. Such an event is often termed a **phase slip**, as the passage of a vortex across the sample changes the overall [phase difference](@entry_id:270122) along the channel by $2\pi$, leading to a discrete drop in the current.

In a quasi-one-dimensional channel like a thin torus, these [phase slips](@entry_id:161743) can be thermally activated. A current-carrying state with velocity $v_s$ is metastable, protected by a [free energy barrier](@entry_id:203446) $\Delta F(v_s)$. According to the Langer-Ambegaokar theory, the rate of [phase slips](@entry_id:161743) is proportional to $\exp(-\Delta F(v_s)/k_B T)$. The energy barrier itself is reduced by the flow; for instance, it might be modeled as $\Delta F(v_s) = U_0 - h A n_s v_s$, where $U_0$ is the barrier at zero velocity and the second term is the work done by the flow during the slip event. A practical critical current can be defined as the current at which the lifetime of the state drops to an observable timescale, $\tau_{obs}$. This leads to a temperature-dependent [critical current density](@entry_id:185715) [@problem_id:491978]:
$$
J_c = \frac{C \hbar^2 n_s}{h \xi} - \frac{m k_B T}{h A} \ln(\Omega \tau_{obs})
$$
This expression shows how the ideal critical current at $T=0$ is reduced by thermal fluctuations that help the system overcome the energy barrier.

In [two-dimensional systems](@entry_id:274086), the analogous process is the [nucleation](@entry_id:140577) of a vortex-antivortex (V-AV) pair [@problem_id:492044]. The energy of a V-AV pair separated by a distance $d$ in a flow of velocity $v_s$ is a competition between their logarithmic binding energy, $E_{int} \propto \ln(d/\xi)$, and the energy gained from the flow, $E_{flow} \propto -v_s d$. The total energy $E(d, v_s)$ has a maximum at a certain separation $d^*$, which forms an energy barrier to dissipation. As the flow velocity $v_s$ increases, this barrier decreases. The critical velocity $v_c$ is reached when the barrier vanishes entirely, allowing for spontaneous V-AV creation and subsequent dissipation. This occurs when the flow is strong enough that the energy maximum is at the [vortex core](@entry_id:159858) separation scale, yielding a critical velocity:
$$
v_c = \frac{\kappa}{2\pi e\xi} = \frac{\hbar}{m e \xi}
$$
This is an example of a Feynman-type [critical velocity](@entry_id:161155), where the limit is set by the [nucleation](@entry_id:140577) of [topological defects](@entry_id:138787) rather than the Landau criterion for quasiparticle creation.

#### Mutual Friction

When there is relative motion between the superfluid and normal fluid components, an interaction force known as **mutual friction** arises. This force is crucial for understanding the dynamics of vortices in a thermal environment. One particularly interesting component of this force is the **Iordanskii force**, a non-dissipative force that acts perpendicular to the relative velocity between the [normal fluid](@entry_id:183299) and the vortex line.

This force has a microscopic origin in the asymmetric scattering of thermal quasiparticles ([phonons and rotons](@entry_id:146031)) from the [vortex core](@entry_id:159858). Consider a stationary vortex ($\boldsymbol{\kappa} = \kappa \hat{\mathbf{z}}$) in a gas of phonons drifting with velocity $\mathbf{v}_n$. The scattering process imparts momentum to the [phonon gas](@entry_id:147597). By Newton's third law, the vortex experiences an equal and opposite force. A detailed calculation [@problem_id:491968], integrating the momentum transfer over the non-[equilibrium distribution](@entry_id:263943) of phonons, shows that the [net force](@entry_id:163825) on the vortex contains a term of the form:
$$
\mathbf{f}_I = D (\boldsymbol{\kappa} \times \mathbf{v}_n)
$$
The coefficient $D$ is found to be directly proportional to the normal fluid density, $D = -\alpha \rho_n$, where $\alpha$ is a constant related to the scattering cross-section. The Iordanskii force is analogous to the Magnus force on a spinning object in a classical fluid, but its origin is purely quantum mechanical. It plays a key role in the motion of vortices, causing them to drift sideways in response to a flow of the normal fluid, a process that is central to the thermal damping of superfluid turbulence.