## Introduction
Superfluids, quantum fluids that exhibit [frictionless flow](@entry_id:195983), are home to some of the most fascinating [collective phenomena](@entry_id:145962) in condensed matter physics. Among the most striking predictions of the [two-fluid model](@entry_id:139846), which describes a superfluid as an intimate mixture of a superfluid and a normal fluid component, is the existence of unique modes of [wave propagation](@entry_id:144063). Beyond the familiar pressure waves found in all fluids, [superfluids](@entry_id:180718) support a distinct type of wave—a [thermal wave](@entry_id:152862) known as second sound. Understanding these wave phenomena is not just a theoretical exercise; it is fundamental to probing the very nature of the superfluid state and provides a bridge to concepts in [high-energy physics](@entry_id:181260), astrophysics, and cosmology.

This article addresses the fundamental principles governing these quantum acoustic phenomena and their practical utility. It aims to elucidate not only what first and second sound are, but also how they function and why they are so important. The reader will gain a comprehensive understanding of the physics of wave propagation in [superfluids](@entry_id:180718), from their basic mechanisms to their advanced applications.

The article is structured to guide you from foundational theory to practical application. The first section, **"Principles and Mechanisms,"** delves into the hydrodynamic origins of first, second, and [fourth sound](@entry_id:158255) using the [two-fluid model](@entry_id:139846), exploring their distinct characteristics, coupling, and attenuation. The second section, **"Applications and Interdisciplinary Connections,"** showcases how these sound modes are used as powerful experimental tools to probe superfluid properties, study [quantum turbulence](@entry_id:160221), and even simulate cosmological phenomena like [sonic black holes](@entry_id:157885). Finally, the **"Hands-On Practices"** appendix will allow you to apply these concepts to solve quantitative problems, solidifying your understanding of these remarkable wave phenomena.

## Principles and Mechanisms

The quantum mechanical nature of superfluids gives rise to a rich spectrum of [collective phenomena](@entry_id:145962), chief among them being unique modes of [wave propagation](@entry_id:144063). Building upon the foundational [two-fluid model](@entry_id:139846), we now delve into the principles and mechanisms governing these wave phenomena. The [two-fluid model](@entry_id:139846) describes a superfluid as a mixture of two interpenetrating components: an inviscid **superfluid component** with density $\rho_s$ and velocity $\vec{v}_s$, which carries zero entropy, and a viscous **normal fluid component** with density $\rho_n$ and velocity $\vec{v}_n$, which carries all of the system's entropy. The total density is $\rho = \rho_s + \rho_n$, and the total mass current density is $\vec{j} = \rho_s \vec{v}_s + \rho_n \vec{v}_n$.

The dynamics of small-amplitude waves are governed by a set of linearized hydrodynamic equations that describe the conservation of mass, momentum, and entropy, along with the [equation of motion](@entry_id:264286) for the superfluid component. For small perturbations (denoted by primed quantities like $P'$, $\rho'$, $S'$) from a uniform equilibrium state, these equations form the basis of our analysis.

### First Sound: The Pressure-Density Wave

The most familiar type of wave propagation in any medium is a sound wave, which involves longitudinal oscillations of pressure and density. Superfluids are no exception and support such a wave, termed **[first sound](@entry_id:144225)**. In the context of the two-fluid model, [first sound](@entry_id:144225) is characterized by the **in-phase motion** of the superfluid and [normal fluid](@entry_id:183299) components, such that $\vec{v}_s \approx \vec{v}_n$. This cooperative motion results in an oscillation of the total density $\rho$.

For low frequencies and long wavelengths, the propagation of [first sound](@entry_id:144225) can be considered a reversible, [isentropic process](@entry_id:137496). This means the entropy per unit mass, $S$, remains constant during the wave's passage. However, constant entropy does not imply constant temperature. A propagating density wave, $\delta\rho$, will be accompanied by a [temperature wave](@entry_id:193534), $\delta T$. We can quantify this relationship using standard [thermodynamic principles](@entry_id:142232).

The change in entropy per unit mass, $S$, can be expressed as a function of temperature $T$ and density $\rho$ via a standard thermodynamic relation:

$dS = \left(\frac{\partial S}{\partial T}\right)_{\rho} dT + \left(\frac{\partial S}{\partial \rho}\right)_{T} d\rho$

Using standard [thermodynamic identities](@entry_id:152434), we can substitute $\left(\frac{\partial S}{\partial T}\right)_{\rho} = \frac{C_V}{T}$ (where $C_V$ is the specific heat at constant volume per unit mass) and the Maxwell relation $\left(\frac{\partial S}{\partial \rho}\right)_{T} = -\frac{1}{\rho^2}\left(\frac{\partial P}{\partial T}\right)_{\rho}$. For an [isentropic process](@entry_id:137496), $dS=0$, which leads to:

$\frac{C_V}{T} dT = \frac{1}{\rho^2}\left(\frac{\partial P}{\partial T}\right)_{\rho} d\rho$

The partial derivative $(\partial P / \partial T)_{\rho}$ can be expressed in terms of more common experimental coefficients: the isobaric thermal expansion coefficient, $\alpha = -\frac{1}{\rho}\left(\frac{\partial \rho}{\partial T}\right)_P$, and the [isothermal compressibility](@entry_id:140894), $\beta_T = \frac{1}{\rho}\left(\frac{\partial \rho}{\partial P}\right)_T$. Using the cyclic relation for [partial derivatives](@entry_id:146280), we find $(\partial P / \partial T)_{\rho} = \alpha / \beta_T$.

Substituting this back, we arrive at the ratio of temperature to density oscillation amplitudes for a [first sound](@entry_id:144225) wave [@problem_id:1246063]:

$\frac{\delta T}{\delta \rho} = \frac{T \alpha}{\rho^2 C_V \beta_T}$

This result confirms that [first sound](@entry_id:144225), while primarily a pressure-density wave, is also a [temperature wave](@entry_id:193534). The magnitude of this temperature oscillation is governed by the thermal expansion coefficient $\alpha$. In the idealized case where $\alpha=0$, [first sound](@entry_id:144225) would be purely a mechanical wave, completely decoupled from thermal effects. For liquid helium, $\alpha$ is very small but non-zero, indicating a weak but definite coupling. The speed of [first sound](@entry_id:144225), denoted $c_1$, is given by the familiar expression for adiabatic sound speed, $c_1^2 = (\partial P / \partial \rho)_S$.

### Second Sound: The Entropy Wave

Perhaps the most dramatic and unique prediction of the [two-fluid model](@entry_id:139846) is the existence of a second, distinct mode of wave propagation known as **[second sound](@entry_id:147020)**. Unlike [first sound](@entry_id:144225), [second sound](@entry_id:147020) does not have an analogue in ordinary classical fluids. It is fundamentally a **[thermal wave](@entry_id:152862)**, or an **entropy wave**.

The defining characteristic of [second sound](@entry_id:147020) is the **out-of-phase motion** of the two fluid components. They oscillate in such a way that the total mass current remains zero:

$\vec{j} = \rho_s \vec{v}_s + \rho_n \vec{v}_n = 0$

This [counterflow](@entry_id:156755) condition implies that there is no net oscillation in the center of mass, and thus the total density $\rho$ and pressure $P$ remain nearly constant. Instead of a pressure wave, we have a wave of "fluid composition": regions of higher [normal fluid](@entry_id:183299) concentration (and thus higher entropy and temperature) alternate with regions of higher superfluid concentration (lower entropy and temperature). The [normal fluid](@entry_id:183299) "carries" the heat, and as it moves, the superfluid flows in the opposite direction to maintain constant density.

The [counterflow](@entry_id:156755) condition directly implies that the velocity amplitudes are related by the inverse ratio of their densities:
$\frac{|\vec{v}_n|}{|\vec{v}_s|} = \frac{\rho_s}{\rho_n}$

This highlights the perfect counter-oscillation of the two components in a pure second sound wave.

The propagation speed of this [thermal wave](@entry_id:152862), denoted $c_2$, is given by:

$c_2^2 = \frac{\rho_s S^2 T}{\rho_n C_P}$

where $S$ is the entropy per unit mass, and $C_P$ is the specific heat at constant pressure per unit mass. This expression (which uses $C_P$ as it assumes constant pressure) shows that the existence of [second sound](@entry_id:147020) is contingent on having both $\rho_s > 0$ and $\rho_n > 0$, and that its speed is directly related to the fluid's thermal properties.

Because second sound is an entropy wave, it can be generated efficiently by a source that modulates temperature or injects heat without injecting mass. A classic example is a thin, oscillating heater submerged in the superfluid. The oscillating heat flux, $W(t) = W_0 \cos(\omega t)$, is carried away from the heater by the [normal fluid](@entry_id:183299), whose velocity is given by the heat flux relation $\vec{q} = \rho S T \vec{v}_n$. This oscillating normal [fluid velocity](@entry_id:267320), coupled with the counter-propagating superfluid, generates a pure [second sound](@entry_id:147020) wave. The amplitude of the resulting entropy wave, $S'_{\text{amp}}$, can be directly related to the heater's power [@problem_id:1246151]:

$S'_{\text{amp}} = \frac{W_0}{\rho T c_2}$

This provides a direct experimental method for generating and studying [second sound](@entry_id:147020).

### Second Sound in the Low-Temperature Phonon Gas Limit

The properties of [second sound](@entry_id:147020) take on a particularly elegant form at very low temperatures. In this regime, the thermal excitations in the superfluid are dominated by a gas of non-interacting phonons (quanta of sound waves). The normal fluid component can be thought of as this very [phonon gas](@entry_id:147597).

The thermodynamic properties of a [phonon gas](@entry_id:147597) have specific temperature dependencies:
-   Normal fluid density: $\rho_n \propto T^4$
-   Entropy per unit mass: $S \propto T^3$
-   Specific heat per unit mass: $C_V \propto T^3$

Substituting these dependencies into the formula for $c_2^2$ reveals a remarkable result. Let us write $S(T) = B T^3$, $C_V(T) = 3 B T^3$, and $\rho_n(T) = A T^4$, where $A$ and $B$ are constants. In this [low-temperature limit](@entry_id:267361) where the thermal expansion coefficient is negligible, $C_P \approx C_V$. Also, $\rho_n \ll \rho$, so we can approximate the [superfluid density](@entry_id:142018) $\rho_s \approx \rho$. The speed of [second sound](@entry_id:147020) is then [@problem_id:1246037]:

$c_2^2 = \frac{\rho_s S^2 T}{\rho_n C_V} \approx \frac{\rho (B T^3)^2 T}{(A T^4)(3 B T^3)} = \frac{\rho B^2 T^7}{3 A B T^7} = \frac{\rho B}{3 A}$

This shows that at very low temperatures, the speed of [second sound](@entry_id:147020) becomes independent of temperature.

This result has a profound physical interpretation. If the normal component is a gas of phonons, [second sound](@entry_id:147020) can be viewed as a density wave propagating *within this [phonon gas](@entry_id:147597)*. The speed of sound in any ideal gas is proportional to the [root-mean-square speed](@entry_id:145946) of its constituent particles. For a relativistic gas like a gas of photons or phonons, the speed of sound is $c/\sqrt{3}$, where $c$ is the particle speed. In our case, the "particles" are phonons, and their speed is the speed of [first sound](@entry_id:144225), $c_1$. Therefore, we should expect the speed of [second sound](@entry_id:147020) to be related to the speed of [first sound](@entry_id:144225).

A detailed derivation confirms this intuition precisely. By using the thermodynamic and hydrodynamic relations for a [phonon gas](@entry_id:147597), one can prove the famous result [@problem_id:1246133]:

$c_2 = \frac{c_1}{\sqrt{3}}$

This elegant formula connects the two sound modes in a fundamental way and provides strong evidence for the interpretation of second sound as sound in the gas of [elementary excitations](@entry_id:140859).

### Coupling and Attenuation of Sound Modes

In our discussion so far, first and [second sound](@entry_id:147020) have been treated as largely independent modes. In reality, they are coupled, and they are subject to dissipative effects that cause them to attenuate.

The primary mechanism for coupling is a non-zero [thermal expansion coefficient](@entry_id:150685). As we saw, this means a pressure wave ([first sound](@entry_id:144225)) is accompanied by a [temperature wave](@entry_id:193534), and conversely, a [temperature wave](@entry_id:193534) can induce small pressure fluctuations. This coupling modifies the speeds of both modes. The [dispersion relation](@entry_id:138513) for the coupled waves with [phase velocity](@entry_id:154045) $u$ can be written as:

$(u^2 - c_1^2)(u^2 - c_2^2) = u^2 c_2^2 \left(\frac{C_P}{C_V} - 1\right)$

Here, $c_1$ and $c_2$ are the uncoupled speeds. The right-hand side, which is proportional to the difference between the specific heats $C_P$ and $C_V$, represents the strength of the [thermomechanical coupling](@entry_id:183230). Typically, this coupling is weak. We can use [perturbation theory](@entry_id:138766) to find the correction to the sound speeds. For [first sound](@entry_id:144225), the first-order correction to its squared speed, $\delta(c_1^2)$, is found to be [@problem_id:1246036]:

$\delta(c_1^2) = \frac{c_1^2 c_2^2}{c_1^2 - c_2^2}\left(\frac{C_P}{C_V} - 1\right)$

This shows that the speeds are "repelled" by the coupling; since $c_1 > c_2$ in helium, the correction is positive, slightly increasing the speed of [first sound](@entry_id:144225).

Beyond coupling, dissipative processes inherent in the two-fluid model lead to the **attenuation** of the sound waves. For second sound, the dominant dissipative mechanism is the **shear viscosity $\eta$ of the normal fluid**. As the [normal fluid](@entry_id:183299) oscillates, viscous forces dissipate energy, damping the wave. By including the viscous term in the linearized hydrodynamic equations, one can derive the attenuation coefficient $\alpha_2$, which describes the [exponential decay](@entry_id:136762) of the wave's amplitude. The result for a wave of [angular frequency](@entry_id:274516) $\omega$ is [@problem_id:1246066]:

$\alpha_2 = \frac{\eta \omega^2}{2 \rho_n c_2^3}$

The $\omega^2$ dependence is characteristic of attenuation due to viscosity.

First sound can also be attenuated, but the mechanism is more subtle. Since the superfluid component is inviscid, viscosity does not directly damp the in-phase motion of [first sound](@entry_id:144225). Instead, attenuation arises from **[thermal conduction](@entry_id:147831)** acting on the small temperature component of the [first sound](@entry_id:144225) wave. The thermal conductivity, $\kappa$, allows heat to flow irreversibly from the warmer crests to the cooler troughs of the wave, dissipating energy. The calculation is complex because it relies on the coupling between the modes. The resulting attenuation coefficient for [first sound](@entry_id:144225), $\alpha_1$, has a more complicated form, but it is also found to be proportional to $\omega^2$ and the thermal conductivity $\kappa$ [@problem_id:1246137].

Finally, it is important to recognize that while a [second sound](@entry_id:147020) wave involves oscillations of temperature with no net flow at the linear level, there can be second-order effects. A traveling [second sound](@entry_id:147020) wave can, in fact, carry a net, time-averaged heat current. This heat current arises from correlations between the oscillating quantities. A detailed calculation retaining second-order terms in the wave amplitudes reveals that a second sound wave with temperature amplitude $\Delta T$ transports a time-averaged heat current density $\langle q_z \rangle$ that is proportional to $(\Delta T)^2$ [@problem_id:1246057]. This reinforces the identity of [second sound](@entry_id:147020) as a fundamentally thermal phenomenon.

### Fourth Sound: Waves in Confined Geometries

The [propagation of sound](@entry_id:194493) in a superfluid can be dramatically altered by boundary conditions. A particularly important case is that of a **superleak**, a porous medium or a set of very narrow channels where the viscous normal fluid component is effectively clamped by the walls and cannot move, i.e., $\vec{v}_n = 0$. The superfluid component, being inviscid, can still flow freely.

In such a confined geometry, neither first nor [second sound](@entry_id:147020) can propagate in their usual form. Instead, a new mode appears, known as **[fourth sound](@entry_id:158255)**. Since the [normal fluid](@entry_id:183299) is stationary, any density oscillation must be carried entirely by the superfluid component. This means [fourth sound](@entry_id:158255) is a pressure and [density wave](@entry_id:199750), similar to [first sound](@entry_id:144225). However, because only the superfluid fraction $\rho_s/\rho$ of the fluid participates in the motion, its speed is modified. Furthermore, as the [superfluid density](@entry_id:142018) changes, the entropy per unit volume $\rho S$ must also change to maintain [local thermodynamic equilibrium](@entry_id:139579), which induces temperature oscillations. Thus, [fourth sound](@entry_id:158255) is a hybrid mode involving oscillations in pressure, density, and temperature.

By solving the two-fluid hydrodynamic equations under the constraint $\vec{v}_n = 0$, one can derive the speed of [fourth sound](@entry_id:158255), $c_4$. A full derivation shows that its speed is a hybrid of the first and second sound modes:

$c_4^2 = \frac{\rho_s}{\rho} c_1^2 \frac{C_V}{C_P} + \frac{\rho_n}{\rho} c_2^2$

This expression shows that the speed of [fourth sound](@entry_id:158255) depends on the properties of both first and second sound. In the limit of negligible [thermal expansion](@entry_id:137427) ($C_P \approx C_V$), it simplifies further. The existence of this mode and its characteristic speed makes it a powerful experimental tool for studying superfluid properties in confinement.