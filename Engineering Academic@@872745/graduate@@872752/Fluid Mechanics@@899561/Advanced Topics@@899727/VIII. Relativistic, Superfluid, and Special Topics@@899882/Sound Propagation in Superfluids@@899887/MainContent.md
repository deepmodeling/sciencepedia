## Introduction
Classical fluids support a single type of sound wave—a longitudinal oscillation of pressure and density. Superfluids, however, defy this classical intuition, exhibiting a rich spectrum of wave phenomena that directly reflects their underlying quantum mechanical nature. The [propagation of sound](@entry_id:194493) in these systems is not just a curiosity; it is one of the most powerful tools for probing the exotic properties of the quantum fluid state. This article addresses the fundamental question of how sound propagates in superfluids and what these unique collective modes reveal about quantum matter.

You will begin by exploring the foundational principles and mechanisms, starting with the two-fluid model that successfully explains the existence of first and [second sound](@entry_id:147020) in [liquid helium](@entry_id:139440). This section will also delve into the microscopic origins of sound in Bose-Einstein condensates and [fermionic superfluids](@entry_id:158561), as well as the unique modes that arise in confined geometries. Next, you will discover the diverse applications of these principles, from probing [quantized vortices](@entry_id:147055) to their surprising connections with astrophysics and the simulation of black holes in [analogue gravity](@entry_id:144870) systems. Finally, you will have the opportunity to solidify your understanding through hands-on practices that challenge you to derive key results in superfluid acoustics. The journey begins with the core principles governing these fascinating quantum waves.

## Principles and Mechanisms

A defining characteristic of the superfluid state is its unique response to perturbations, most strikingly revealed in the [propagation of sound](@entry_id:194493). Unlike classical fluids which support a single longitudinal sound mode, superfluids exhibit a rich spectrum of wave phenomena. These collective modes arise from the quantum mechanical nature of the fluid and provide a powerful experimental probe into its fundamental properties. This section elucidates the principles and mechanisms governing these distinct sound modes, from the phenomenological two-fluid model to microscopic descriptions and the effects of geometric confinement.

### Sound in the Two-Fluid Model: First and Second Sound

The behavior of [superfluid helium-4](@entry_id:137809) (He II) below the [lambda point](@entry_id:141863) ($T_{\lambda} \approx 2.17 \text{ K}$) is remarkably well-described by the **two-fluid model**. This model posits that He II behaves as if it were a mixture of two interpenetrating fluid components: a **superfluid component** and a **normal component**. The superfluid component, with density $\rho_s$, has zero viscosity and, crucially, zero entropy. The normal component, with density $\rho_n$, possesses viscosity and carries the entire thermal entropy of the system. The total density of the liquid is the sum of the two, $\rho = \rho_n + \rho_s$. The proportions of the two components are temperature-dependent; as $T \to 0$, $\rho_n \to 0$ and $\rho \to \rho_s$.

The existence of two dynamical components allows for two distinct longitudinal sound modes, distinguished by the [relative motion](@entry_id:169798) of the normal and superfluid constituents [@problem_id:1994370].

**First sound** is analogous to ordinary sound in a classical fluid. It is a wave of pressure and density. In a [first sound](@entry_id:144225) wave, the superfluid and normal components oscillate **in-phase** with each other, such that $\mathbf{v}_n \approx \mathbf{v}_s$. This co-moving oscillation results in a non-zero total mass current, $\mathbf{j} = \rho_n \mathbf{v}_n + \rho_s \mathbf{v}_s \neq 0$, which according to the [continuity equation](@entry_id:145242), $\frac{\partial \rho}{\partial t} + \nabla \cdot \mathbf{j} = 0$, directly supports oscillations in the total density $\rho$. These density variations, in turn, produce pressure variations.

**Second sound**, by contrast, is a phenomenon unique to superfluids. It is a wave of temperature and entropy that propagates with negligible oscillation in the overall pressure or density. This remarkable behavior is achieved when the two fluid components oscillate **out-of-phase**. Specifically, the motions are opposed in such a way that the net mass current is zero: $\mathbf{j} = \rho_n \mathbf{v}_n + \rho_s \mathbf{v}_s = 0$. This condition implies a strict [counterflow](@entry_id:156755), $\mathbf{v}_s = -(\rho_n / \rho_s) \mathbf{v}_n$. Although there is no net mass transport, there is a net transport of entropy, since only the normal component carries it. The entropy current is $\rho s \mathbf{v}_n$, where $s$ is the specific entropy. An oscillation in the entropy current leads to local variations in entropy density, which, by the laws of thermodynamics, are accompanied by temperature variations. Thus, [second sound](@entry_id:147020) is a propagating [thermal wave](@entry_id:152862).

The speed of [second sound](@entry_id:147020), $c_2$, can be derived from the linearized hydrodynamic equations of the two-fluid model [@problem_id:604008]. The essential physics is captured by two equations. The first is the superfluid acceleration equation, which states that a gradient in chemical potential drives the flow. Since temperature gradients induce chemical potential gradients through the thermodynamic relation $d\mu = -s dT + (1/\rho) dP$, a [temperature wave](@entry_id:193534) creates a relative acceleration between the components. In linearized form, this becomes:
$$
\rho_n \left( \frac{\partial \mathbf{v}_n}{\partial t} - \frac{\partial \mathbf{v}_s}{\partial t} \right) = - \rho s \nabla T'
$$
where primed quantities denote small fluctuations around equilibrium. The second equation is the conservation of entropy, which, for negligible [density fluctuations](@entry_id:143540), is:
$$
\frac{\partial s'}{\partial t} + s \nabla \cdot \mathbf{v}_n = 0
$$
Combining these with the [counterflow](@entry_id:156755) condition $\mathbf{v}_s = -(\rho_n / \rho_s) \mathbf{v}_n$ and [thermodynamic relations](@entry_id:139032) yields a wave equation. For a hypothetical superfluid where the entropy per unit mass follows a power law $s = \alpha T^\beta$, the [specific heat](@entry_id:136923) at constant volume is $c_v = T(\partial s/\partial T)_V = \beta s$. The resulting speed of second sound is then given by the celebrated Landau formula (generalized for an arbitrary $\beta$):
$$
c_2^2 = \frac{\rho_s s^2 T}{\rho_n c_v} = \frac{\rho_s s T}{\beta \rho_n}
$$
This expression shows that the speed of [second sound](@entry_id:147020) depends explicitly on the superfluid fraction $\rho_s/\rho_n$ and the thermal properties ($s, T, c_v$) of the fluid. The existence and properties of second sound provide direct and compelling evidence for the validity of the two-fluid model.

### Coupling and Attenuation of Sound Modes

The strict separation of [first sound](@entry_id:144225) into a pure pressure wave and second sound into a pure [thermal wave](@entry_id:152862) is an idealization that holds only when the coefficient of thermal expansion of the fluid is zero. In any real fluid, pressure and temperature fluctuations are thermodynamically linked, leading to a coupling between the two sound modes.

This coupling can be seen by examining the full [dispersion relation](@entry_id:138513) that arises from the complete set of linearized hydrodynamic equations [@problem_id:603991]. The speeds of the two propagating modes, $c_1$ and $c_2$, are the roots of a biquadratic equation for the wave velocity squared, $u^2 = (\omega/k)^2$:
$$
u^4 - u^2 \left[ \left(\frac{\partial P}{\partial \rho}\right)_s + \frac{\rho_s s^2 T}{\rho_n c_v} \right] + \left(\frac{\partial P}{\partial \rho}\right)_T \frac{\rho_s s^2 T}{\rho_n c_v} = 0
$$
Here, $(\partial P/\partial \rho)_s = u_s^2$ and $(\partial P/\partial \rho)_T = u_T^2$ are the squares of the isentropic and isothermal sound velocities, respectively. Using Vieta's formulas for the sum and product of the roots ($c_1^2$ and $c_2^2$), one can relate the sound speeds to fundamental thermodynamic quantities. For instance, the [ratio of specific heats](@entry_id:140850), $\gamma = c_p/c_v$, which is thermodynamically equal to $u_s^2 / u_T^2$, can be expressed entirely in terms of measurable sound speeds:
$$
\gamma = \frac{u_s^2 (c_1^2 + c_2^2 - u_s^2)}{c_1^2 c_2^2}
$$
This demonstrates that $c_1$ and $c_2$ are not independent but are mixed modes whose properties are intertwined with the fluid's thermodynamic equation of state.

In liquid helium, the coupling is weak, and it is often sufficient to treat its effects perturbatively [@problem_id:604031]. The primary coupling mechanism is the finite coefficient of thermal expansion, $\beta_P = -(1/\rho)(\partial \rho/\partial T)_P$. A non-zero $\beta_P$ means that a pressure wave ([first sound](@entry_id:144225)) will be accompanied by a small temperature fluctuation, and a [temperature wave](@entry_id:193534) ([second sound](@entry_id:147020)) will have a small associated pressure fluctuation. Calculating the [first-order correction](@entry_id:155896) to the speed of [second sound](@entry_id:147020) due to this coupling, one finds that the unperturbed speed $c_{2,0}$ is modified:
$$
\delta c_2 = c_2 - c_{2,0} = -\frac{T s \beta_P}{2 C_P} c_{2,0}
$$
This result quantifies how the mixing of modes alters their propagation speeds.

Beyond coupling, real-world sound waves also experience **attenuation**, or damping. Dissipative processes, such as viscosity and [thermal conduction](@entry_id:147831), convert coherent wave energy into heat. The attenuation coefficient $\alpha$ describes the [exponential decay](@entry_id:136762) of the wave's amplitude. For [first sound](@entry_id:144225), attenuation can arise from the thermal conductivity $\kappa$ of the [normal fluid](@entry_id:183299) component [@problem_id:604015]. Although [first sound](@entry_id:144225) is primarily a pressure wave, the weak coupling induced by thermal expansion creates small temperature oscillations. These temperature gradients drive heat flow via the [normal fluid](@entry_id:183299), leading to entropy production and [energy dissipation](@entry_id:147406). The attenuation coefficient for [first sound](@entry_id:144225) due to this mechanism is given by:
$$
\alpha_1 = \frac{\kappa \beta_P^2 T \omega^2}{2 \rho u_1 c_p^2}
$$
This expression highlights a key feature of dissipation: its strong dependence on frequency ($\propto \omega^2$). The presence of the term $\beta_P^2$ confirms that this dissipative channel is only open because of the thermal expansion that couples the pressure and thermal degrees of freedom.

### Sound in Diverse Superfluid Systems

The concept of sound as a collective density oscillation extends beyond liquid helium to other superfluid systems, such as atomic Bose-Einstein condensates (BECs) and [fermionic superfluids](@entry_id:158561).

#### Microscopic Origin in Bose-Einstein Condensates

In a weakly interacting Bose gas at zero temperature, all atoms condense into a single macroscopic quantum state described by a wavefunction $\Psi(\mathbf{r}, t)$. The dynamics are governed by the **Gross-Pitaevskii equation (GPE)**, a mean-field theory that provides a microscopic foundation for superfluidity. Sound waves emerge in this description as the long-wavelength limit of the elementary excitations of the condensate, known as **Bogoliubov quasiparticles**.

For a uniform condensate with density $n_0$, the speed of sound $c_s$ can be derived directly from the GPE. Thermodynamically, sound speed in a [compressible fluid](@entry_id:267520) is related to the derivative of the chemical potential $\mu$ with respect to density $n$: $c_s^2 = (n/m)(\partial \mu / \partial n)$. For a BEC described by a GPE with two-body ($g_1$) and three-body ($g_2$) interactions, the chemical potential is $\mu = g_1 n_0 + g_2 n_0^2$. This yields a sound speed of [@problem_id:604020]:
$$
c_s = \sqrt{\frac{n_0 (g_1 + 2 g_2 n_0)}{m}}
$$
This derivation shows that sound is a direct consequence of the repulsive interactions ($g_1, g_2 > 0$) that provide the restoring force against density compressions.

The phenomenology becomes even richer in **two-component BECs**, mixtures of two different atomic species or hyperfine states. Such systems support two sound-like modes, analogous to first and [second sound](@entry_id:147020) in He II [@problem_id:604044]. One mode is an **in-phase** oscillation, where the densities of the two components fluctuate together, corresponding to a wave of total density. The other is an **out-of-phase** mode, where one component's density increases as the other's decreases, corresponding to a wave of relative concentration. The speed of this lower-energy, out-of-phase mode, $c_-$, depends on both the intra-[species interactions](@entry_id:175071) ($g_{11}, g_{22}$) and the inter-[species interaction](@entry_id:195816) ($g_{12}$):
$$
c_- = \sqrt{\frac{1}{2m} \left( g_{11}n_1 + g_{22}n_2 - \sqrt{(g_{11}n_1 - g_{22}n_2)^2 + 4g_{12}^2n_1n_2} \right)}
$$
This demonstrates the universality of in-phase and out-of-phase collective modes in multi-component quantum fluids.

#### Sound in Fermionic Superfluids

In neutral fermionic systems, like liquid ${}^3\text{He}$ or ultracold atomic Fermi gases, the story of sound propagation is more subtle and deeply connected to [fundamental symmetries](@entry_id:161256) [@problem_id:3024867]. Above the superfluid transition temperature $T_c$, in the collisionless regime, a repulsive Fermi liquid supports a collective density mode known as **[zero sound](@entry_id:142772)**. This is not a hydrodynamic mode but a coherent oscillation of the distorted Fermi surface.

Below $T_c$, the fermions form Cooper pairs, and the system enters a superfluid state. This transition involves the spontaneous breaking of a continuous global symmetry—the $\mathrm{U}(1)$ symmetry associated with particle number conservation. **Goldstone's theorem** dictates that such a symmetry breaking must give rise to a gapless collective excitation, or Goldstone mode. In a neutral superfluid, this mode is the **Anderson-Bogoliubov mode**, which is a sound-like wave of density and phase.

A key insight, due to P.W. Anderson, is that the [zero sound](@entry_id:142772) mode of the normal state continuously evolves into the Anderson-Bogoliubov mode of the superfluid state as the temperature is lowered through $T_c$. The collective pole in the density [response function](@entry_id:138845) persists across the transition, with its velocity and character changing smoothly. Experimentally, this is observed as a shift in the sound velocity from the zero-sound value $c_0$ to the first-sound (hydrodynamic) value $c_1$. Concurrently, the [sound attenuation](@entry_id:189896) drops dramatically for frequencies below twice the superfluid gap ($\omega  2\Delta$), as the gapping of the quasiparticle spectrum eliminates the primary channel for dissipation.

### Sound in Confined Geometries

Imposing boundary conditions by confining a superfluid to restricted geometries can dramatically alter its dynamics and give rise to new types of sound waves where the motion of the normal component is constrained.

**Third sound** is a surface wave that propagates on a thin superfluid film adsorbed onto a substrate [@problem_id:492021]. In this geometry, the viscous [normal fluid](@entry_id:183299) component is effectively clamped to the stationary substrate. The superfluid component, however, is free to move. Third sound consists of oscillations of the superfluid component parallel to the surface, which leads to variations in the film's thickness. The restoring force for this wave is not pressure, but rather the thickness-dependent chemical potential, $\mu(d)$, arising from the van der Waals interaction with the substrate. The speed of [third sound](@entry_id:187597) is given by the general relation:
$$ c_3^2 = \frac{\rho_s}{\rho} d \left(-\frac{\partial \mu}{\partial d}\right) $$
The speed of [third sound](@entry_id:187597) is thus a direct probe of the [superfluid density](@entry_id:142018) in the film and the film-substrate interaction potential.

**Fourth sound** is a bulk wave that exists when a superfluid fills a porous medium or a dense array of fine capillaries, which again serves to clamp the normal component ($\mathbf{v}_n = 0$) [@problem_id:604036]. With the [normal fluid](@entry_id:183299) immobilized, any pressure or [density wave](@entry_id:199750) must be carried solely by the superfluid component. The resulting wave is [fourth sound](@entry_id:158255). The physics can be extended to [anisotropic media](@entry_id:260774), where the effective inertia of the superfluid depends on direction. This is modeled by a **[superfluid density](@entry_id:142018) tensor** $\boldsymbol{\rho}_s$. The resulting [fourth sound](@entry_id:158255) speed is also anisotropic, described by a velocity-squared tensor $\mathbf{C}_4^2$. For a propagation direction given by the [unit vector](@entry_id:150575) $\hat{\mathbf{q}}$, the speed is $c_4^2(\hat{\mathbf{q}}) = \hat{\mathbf{q}} \cdot \mathbf{C}_4^2 \cdot \hat{\mathbf{q}}$. Assuming thermal effects are negligible (an approximation valid at low temperatures), derivation from the hydrodynamic equations yields:
$$
\mathbf{C}_4^2 = \frac{c_1^2}{\rho} \boldsymbol{\rho}_s
$$
where $c_1$ is the [first sound](@entry_id:144225) speed and $\rho$ is the total density. Fourth sound measurements in [anisotropic media](@entry_id:260774) thus provide a unique tool to map out the directional dependence of the superfluid response.

In summary, the study of sound in [superfluids](@entry_id:180718) reveals a rich tapestry of wave phenomena that reflect the underlying quantum nature of the fluid state. From the counter-oscillations of two fluids to the Goldstone modes of broken symmetries and [surface waves](@entry_id:755682) on thin films, these collective excitations remain one of the most powerful and versatile probes of the world of quantum matter.