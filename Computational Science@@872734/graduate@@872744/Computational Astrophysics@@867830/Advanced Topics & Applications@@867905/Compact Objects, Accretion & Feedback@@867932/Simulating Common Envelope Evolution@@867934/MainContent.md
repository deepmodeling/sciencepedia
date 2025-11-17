## Introduction
Common envelope evolution (CEE) is a brief but transformative phase in the life of a binary star system, critical for forging the [compact binaries](@entry_id:141416) that become sources of gravitational waves, X-ray binaries, and [cataclysmic variables](@entry_id:157825). Despite its importance, the rapid, chaotic nature of the inspiral, where one star plunges into the envelope of its companion, shrouds the process in uncertainty. Direct observation is nearly impossible, forcing astrophysicists to rely on complex numerical simulations to unravel the underlying physics. The central challenge lies in understanding how orbital energy is converted into the kinetic energy needed to expel the vast stellar envelope, a process that determines whether the binary survives or merges.

This article provides a comprehensive guide to simulating this enigmatic process. The first chapter, **Principles and Mechanisms**, will lay the theoretical foundation, exploring the stability criteria that trigger the event, the hydrodynamic equations governing the inspiral, and the energetic framework used to predict its outcome. Following this, **Applications and Interdisciplinary Connections** will demonstrate how these principles are put into practice, from building 3D initial models to generating synthetic [observables](@entry_id:267133) that link simulations to astronomical data. Finally, **Hands-On Practices** will offer the chance to apply these concepts to concrete astrophysical problems. We begin by examining the core physics that dictates the onset, progression, and conclusion of this dramatic stellar interaction.

## Principles and Mechanisms

The evolution of a [binary system](@entry_id:159110) through a [common envelope](@entry_id:161176) (CE) phase is one of the most complex and consequential processes in [stellar astrophysics](@entry_id:160229). It is responsible for forming a diverse array of compact [binary systems](@entry_id:161443), including [cataclysmic variables](@entry_id:157825), X-ray binaries, and the progenitors of [gravitational wave sources](@entry_id:273194) like binary [neutron stars](@entry_id:139683) and black holes. Understanding the CE phase requires a synthesis of [stellar structure](@entry_id:136361) theory, orbital mechanics, and hydrodynamics. This chapter elucidates the fundamental principles and physical mechanisms that govern the onset, progression, and outcome of [common envelope evolution](@entry_id:158383), with a focus on the theoretical and computational underpinnings required for its simulation.

### The Onset of Common Envelope Evolution: A Stability Analysis

Common envelope evolution is initiated when a star in a [binary system](@entry_id:159110) expands to fill its **Roche lobe**—the gravitational [equipotential surface](@entry_id:263718) that defines the region of space gravitationally bound to that star. If the subsequent mass transfer to the companion star is unstable, it can lead to a runaway process where the companion is unable to accrete the transferred material, resulting in the formation of a shared, encompassing envelope.

The stability of [mass transfer](@entry_id:151080) is determined by comparing the response of the donor star's radius to mass loss with the response of its Roche lobe. Let us define the logarithmic mass-radius exponents for the donor star, $\zeta_{\ast}$, and its Roche lobe, $\zeta_{\mathrm{L}}$:
$$ \zeta_{\ast} \equiv \frac{d\ln R_{\ast}}{d\ln M_{\mathrm{d}}}, \quad \zeta_{\mathrm{L}} \equiv \frac{d\ln R_{\mathrm{L}}}{d\ln M_{\mathrm{d}}} $$
where $R_{\ast}$ is the donor's radius and $M_{\mathrm{d}}$ is its mass. Mass transfer is stable if, upon losing a small amount of mass ($dM_{\mathrm{d}}  0$), the star shrinks to remain within its new, smaller Roche lobe. This translates to the condition $\zeta_{\ast} \ge \zeta_{\mathrm{L}}$. Conversely, [mass transfer](@entry_id:151080) becomes dynamically unstable, leading to a [common envelope](@entry_id:161176), when the star expands, or shrinks less rapidly than its Roche lobe, upon mass loss. For a star losing mass, this instability criterion is $\zeta_{\ast}  \zeta_{\mathrm{L}}$.

The donor's response, $\zeta_{\ast}$, depends on its internal structure and the timescale of mass loss. For the giant stars that typically initiate CE evolution, their deep convective envelopes cause them to respond adiabatically to rapid mass loss. For a fully convective star, which can be modeled as an $n=3/2$ [polytrope](@entry_id:161798), the adiabatic mass-radius exponent is $\zeta_{\mathrm{ad}} = -1/3$. This means the star *expands* as it loses mass.

The Roche lobe's response, $\zeta_{\mathrm{L}}$, depends on the [mass ratio](@entry_id:167674) $q \equiv M_{\mathrm{d}}/M_{\mathrm{a}}$ (donor mass over accretor mass) and the assumptions about mass and [angular momentum conservation](@entry_id:156798) during the transfer. For conservative [mass transfer](@entry_id:151080) in a circular binary, where total mass and orbital angular momentum are conserved, the Roche lobe mass-radius exponent can be derived [@problem_id:3533088]. The result is a function of the mass ratio, $\zeta_{\mathrm{L}}(q)$.

The critical condition for the onset of instability is met when $\zeta_{\mathrm{ad}} = \zeta_{\mathrm{L}}(q_{\mathrm{crit}})$. For a donor with a deep convective envelope ($\zeta_{\mathrm{ad}} = -1/3$), solving this equality for $q$ using a standard approximation for the Roche lobe radius (e.g., the Eggleton formula) yields a critical [mass ratio](@entry_id:167674) of approximately $q_{\mathrm{crit}} \approx 0.634$ [@problem_id:3533088]. If the donor is more massive than the accretor by a factor greater than this, [mass transfer](@entry_id:151080) is dynamically unstable, and a [common envelope phase](@entry_id:158700) is the expected outcome.

### The Physical Regimes of the Spiral-In

Once the companion is engulfed, a rapid and dramatic inspiral phase begins. The nature of this evolution is determined by the interplay of several key timescales. To understand the physics, we must compare the characteristic times over which different processes occur.

The three fundamental timescales of a star are [@problem_id:3533095]:
1.  The **[nuclear timescale](@entry_id:159793)**, $t_{\mathrm{nuc}}$, over which the star consumes its nuclear fuel. For a giant star, this is typically millions to hundreds of millions of years.
2.  The **thermal (Kelvin-Helmholtz) timescale**, $t_{\mathrm{KH}}$, over which the star radiates away its thermal energy content. For a [red giant](@entry_id:158739) envelope, this is on the order of decades to millennia. It is estimated as $t_{\mathrm{KH}} \approx E_{\mathrm{bind}}/L_{\star}$, where $E_{\mathrm{bind}}$ is the envelope binding energy and $L_{\star}$ is the star's luminosity.
3.  The **dynamical timescale**, $t_{\mathrm{dyn}}$, which is the response time to a mechanical perturbation, on the order of the [free-fall time](@entry_id:261377). For a [red giant](@entry_id:158739), this is typically days to weeks, calculated as $t_{\mathrm{dyn}} \approx \sqrt{R_{\star}^3 / (G M_{\star})}$.

The clear hierarchy $t_{\mathrm{dyn}} \ll t_{\mathrm{KH}} \ll t_{\mathrm{nuc}}$ is a cornerstone of [stellar evolution](@entry_id:150430) theory. The CE spiral-in introduces a fourth crucial timescale: the **inspiral timescale**, $t_{\mathrm{insp}}$, over which the companion's orbit decays due to drag forces within the envelope.

The evolution is considered to be in the **dynamical regime** if the inspiral is much faster than the thermal timescale ($t_{\mathrm{insp}} \ll t_{\mathrm{KH}}$). In this case, the enormous amount of [orbital energy](@entry_id:158481) released by the inspiraling companion is deposited into the envelope far too quickly for it to be radiated away. The process is therefore essentially adiabatic on a global scale and must be modeled with hydrodynamics.

Alternatively, if the inspiral were slow enough that $t_{\mathrm{insp}} \gtrsim t_{\mathrm{KH}}$, the envelope could maintain thermal equilibrium by radiating away the deposited energy. This would constitute a **thermal-timescale** or **self-regulated regime**.

To determine which regime applies, we must estimate $t_{\mathrm{insp}}$. This timescale is primarily set by the efficiency of drag forces, which in turn depends on whether the companion's motion is subsonic or supersonic relative to the envelope gas. The orbital velocity of the companion inside the envelope is given by Kepler's law, using the enclosed mass $M_{\mathrm{enc}}(r)$: $v_{\mathrm{orb}} = \sqrt{G M_{\mathrm{enc}}(r) / r}$. The Mach number is $\mathcal{M} = v_{\mathrm{orb}} / c_s$, where $c_s$ is the local sound speed.

In the vast, low-density envelopes of red giants, the sound speed is relatively low (e.g., $10-20\, \mathrm{km}\,\mathrm{s}^{-1}$), while the orbital velocity required to support the companion against the gravity of the donor's core is high (e.g., $50-100\,\mathrm{km}\,\mathrm{s}^{-1}$). Consequently, the companion's motion is almost always highly supersonic ($\mathcal{M} \gg 1$) during the initial plunge [@problem_id:3533077]. Supersonic motion generates strong **gravitational drag** (also known as [dynamical friction](@entry_id:159616)), where the companion's gravity creates a dense wake behind it, exerting a powerful braking force. This leads to a very short inspiral timescale, often comparable to the donor's dynamical time ($t_{\mathrm{insp}} \sim t_{\mathrm{dyn}}$). Given the timescale hierarchy, this definitively places the initial CE phase in the dynamical regime ($t_{\mathrm{insp}} \ll t_{\mathrm{KH}}$). This has a profound implication for simulations: any explicit hydrodynamic code must use timesteps that satisfy the Courant-Friedrichs-Lewy (CFL) condition, meaning timesteps must be much smaller than the dynamical timescale (typically on the order of hours or less) [@problem_id:3533095].

### Governing Equations and Hydrodynamic Phases

To simulate [common envelope evolution](@entry_id:158383), one must solve the equations of [hydrodynamics](@entry_id:158871) coupled with self-gravity. The fundamental governing equations are the Euler equations, which express the conservation of mass, momentum, and energy. For a fluid with density $\rho$, velocity $\mathbf{v}$, pressure $P$, and specific internal energy $e$, in a [gravitational potential](@entry_id:160378) $\Phi$, these are:

-   **Continuity Equation (Mass Conservation):**
    $$ \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) = 0 $$

-   **Momentum Equation (Euler Equation):**
    $$ \frac{\partial (\rho \mathbf{v})}{\partial t} + \nabla \cdot \left(\rho \mathbf{v} \mathbf{v} + P \mathbf{I}\right) = -\rho \nabla \Phi $$

-   **Energy Equation:**
    $$ \frac{\partial E}{\partial t} + \nabla \cdot \left[ (E+P)\mathbf{v} \right] = -\rho \mathbf{v} \cdot \nabla\Phi $$
    where $E = \rho e + \frac{1}{2}\rho |\mathbf{v}|^2$ is the total energy density (internal plus kinetic).

Because the problem involves an orbiting binary, it is computationally advantageous to solve these equations in a **[co-rotating reference frame](@entry_id:158071)** that rotates with the binary's angular velocity $\boldsymbol{\Omega}$. This transformation introduces inertial forces (Coriolis and centrifugal) as source terms in the momentum and energy equations. For a frame with constant $\boldsymbol{\Omega}$, the equations become [@problem_id:3533027]:

-   **Momentum:**
    $$ \partial_{t}(\rho \mathbf{v}) + \nabla\cdot\left(\rho \mathbf{v}\mathbf{v} + P \mathbf{I}\right) = -\rho \nabla \Phi - 2\rho\, (\boldsymbol{\Omega}\times \mathbf{v}) - \rho\, \boldsymbol{\Omega}\times(\boldsymbol{\Omega}\times \mathbf{r}) $$

-   **Energy:**
    $$ \partial_{t}E + \nabla\cdot\left[(E+P)\mathbf{v}\right] = - \rho\, \mathbf{v}\cdot \nabla \Phi - \rho\, \mathbf{v}\cdot\big[\boldsymbol{\Omega}\times(\boldsymbol{\Omega}\times \mathbf{r})\big] $$
The two new source terms in the [momentum equation](@entry_id:197225) are the **Coriolis force** ($-2\rho\,(\boldsymbol{\Omega}\times \mathbf{v})$) and the **[centrifugal force](@entry_id:173726)** ($- \rho\, \boldsymbol{\Omega}\times(\boldsymbol{\Omega}\times \mathbf{r})$). Notably, the Coriolis force is always perpendicular to the velocity $\mathbf{v}$ in the rotating frame and therefore does no work, so it does not appear in the energy equation. The [centrifugal force](@entry_id:173726) is conservative and can be included in an effective potential, $\Phi_{\mathrm{eff}} = \Phi - \frac{1}{2}|\boldsymbol{\Omega}\times\mathbf{r}|^2$.

The hydrodynamic evolution itself can be broadly divided into two phases [@problem_id:3533017]:
1.  **The Plunge-In Phase:** This is the initial, rapid inspiral. As established, the companion's motion is highly supersonic ($\mathcal{M} \gg 1$). A scaling analysis of the [momentum equation](@entry_id:197225) reveals that the inertial term, $\rho(\mathbf{v}\cdot\nabla)\mathbf{v} \sim \rho v^2/H$, dominates over the pressure gradient, $\nabla P \sim \rho c_s^2/H$, by a factor of $\mathcal{M}^2$. The primary force balance is between inertia and gravity. The flow is far from hydrostatic equilibrium. In this phase, the ratio of the [radiative diffusion](@entry_id:158401) timescale to the advection timescale, given by the radiative Péclet number $Pe_{\mathrm{rad}}$, is typically very large ($Pe_{\mathrm{rad}} \gg 1$). This confirms that [radiative transport](@entry_id:151695) is negligible, and the flow is approximately adiabatic, with energy being deposited via shock heating and compressional work.

2.  **The Self-Regulated Phase:** After the initial plunge, the inspiral may slow down. This can happen if the companion transfers enough energy to the inner envelope to cause it to expand and co-rotate, reducing the drag. In this phase, the companion's motion becomes subsonic or transonic ($\mathcal{M} \lesssim 1$). The inertial terms in the [momentum equation](@entry_id:197225) become subdominant to the pressure gradient, and the envelope achieves a state of quasi-[hydrostatic balance](@entry_id:263368) where $\nabla P \approx -\rho \nabla \Phi$. The inspiral proceeds on a longer timescale, regulated by the rate at which angular momentum can be transported through the envelope. During this phase, [radiative transport](@entry_id:151695) can become more significant ($Pe_{\mathrm{rad}} \lesssim 1$), and the simple adiabatic assumption may break down.

### The Energetics of Envelope Ejection

The ultimate outcome of the CE phase—whether the envelope is successfully ejected to leave a compact binary, or the companion merges with the donor's core—is determined by an [energy balance](@entry_id:150831). The standard framework for analyzing this is the **$\alpha$-formalism** [@problem_id:3533063].

The principle is simple: the energy required to unbind the envelope must be supplied by the orbital energy released during the spiral-in. The [energy balance](@entry_id:150831) is written as:
$$ \Delta E_{\mathrm{bind}} = \alpha_{\mathrm{CE}} \Delta E_{\mathrm{orb}} $$
Here, $\Delta E_{\mathrm{bind}}$ is the energy required to eject the envelope (equal to the negative of its binding energy). $\Delta E_{\mathrm{orb}} = E_{\mathrm{orb,final}} - E_{\mathrm{orb,initial}}$ is the change in the binary's orbital energy, which is negative for a spiral-in. The equation is often written as $E_{\mathrm{bind,abs}} = \alpha_{\mathrm{CE}} (E_{\mathrm{orb,initial}} - E_{\mathrm{orb,final}})$, where $E_{\mathrm{bind,abs}}$ is the positive magnitude of the binding energy.

Two key parameters, $\alpha_{\mathrm{CE}}$ and $\lambda$, parameterize our ignorance of the complex physics:

-   **The CE Efficiency, $\alpha_{\mathrm{CE}}$:** This dimensionless parameter quantifies the fraction of the released orbital energy that is effectively used to unbind the envelope. $\alpha_{\mathrm{CE}}=1$ implies perfect conversion, while $\alpha_{\mathrm{CE}}  1$ implies that some energy is lost (e.g., to radiation or kinetic energy of the outflow) or is not efficiently coupled to the envelope. It is a parameterization of the complex 3D hydrodynamic [energy transfer](@entry_id:174809). While often assumed to be less than 1, if other energy sources contribute to the ejection (e.g., accretion luminosity, or energy from hydrogen/helium recombination as the envelope expands), the *effective* value of $\alpha_{\mathrm{CE}}$ required to balance the equation could exceed 1.

-   **The Envelope Structure Parameter, $\lambda$:** The envelope binding energy, $E_{\mathrm{bind}}$, is a complex integral of the gravitational and internal energy over the [stellar structure](@entry_id:136361). To simplify this, it is often parameterized as:
    $$ E_{\mathrm{bind}} = - \frac{G M_{\mathrm{d}} M_{\mathrm{env}}}{\lambda R_{\mathrm{d}}} $$
    where $M_{\mathrm{d}}$, $M_{\mathrm{env}}$, and $R_{\mathrm{d}}$ are the donor's total mass, envelope mass, and radius, respectively. The dimensionless parameter $\lambda$ encapsulates the details of the donor's internal structure (its density profile) and the physics included in the binding energy calculation (e.g., whether thermal and recombination energy are included).

The value of $E_{\mathrm{bind}}$ is critically sensitive to the definition of the **core-envelope boundary**. A composition-based boundary (e.g., where the hydrogen [mass fraction](@entry_id:161575) drops below a certain value) typically lies deeper inside the star than a dynamically-motivated boundary, such as the base of the convective envelope. Since the deepest layers of the envelope are the most tightly bound, choosing a deeper boundary results in a significantly larger (more negative) binding energy [@problem_id:3533030]. For a given energy budget, a more tightly bound envelope is harder to eject, leading to a smaller post-CE orbital separation or a higher likelihood of merger.

### Essential Microphysics and Numerical Techniques

Realistic simulations of [common envelope evolution](@entry_id:158383) depend on both accurate microphysical inputs and robust numerical methods.

#### The Equation of State (EOS)

The thermodynamic properties of the envelope gas are described by the Equation of State (EOS). A simple ideal gas law is insufficient because the envelope spans a vast range of temperatures and densities. A suitable EOS for CE simulations must include [@problem_id:3533082]:
1.  **Gas Pressure:** The pressure from ions and electrons, typically behaving as an ideal gas.
2.  **Radiation Pressure:** At high temperatures in the deep envelope, radiation pressure ($P_{\mathrm{rad}} = \frac{1}{3}aT^4$) becomes significant and can even dominate.
3.  **Partial Ionization:** As gas is heated during the inspiral, hydrogen and helium undergo [ionization](@entry_id:136315). This is a crucial physical process. Energy is diverted into breaking atomic bonds rather than increasing the [kinetic temperature](@entry_id:751035). This acts as a thermodynamic "buffer," dramatically increasing the gas's specific heat capacity.

The consequence of ionization is most clearly seen in the behavior of the **first adiabatic exponent**, $\Gamma_1 = (\partial \ln P / \partial \ln \rho)_s$.
- In the cool, neutral outer envelope, the gas is monatomic, and $\Gamma_1 \approx 5/3$.
- In the hydrogen and helium ionization zones ($T \sim 10^4 - 10^5\,\mathrm{K}$), the large heat capacity makes the gas "soft" and highly compressible, causing $\Gamma_1$ to plummet to values as low as $1.1-1.3$.
- In the hot, fully ionized deep interior, ionization is complete, but [radiation pressure](@entry_id:143156) becomes important. An ideal gas and radiation mixture has an adiabatic index between $5/3$ (gas-dominated) and $4/3$ (radiation-dominated). Thus, as one moves deeper, $\Gamma_1$ approaches $4/3$.

The "dips" in $\Gamma_1$ in the ionization zones are dynamically important, as they can promote instabilities and affect the efficiency of energy deposition from shocks.

#### Numerical Implementation: Sink Particles and Resolution

Two key numerical challenges in CE simulations are representing the compact companion and adequately resolving the flow around it.

-   **Sink Particles:** The companion star is often much smaller than the grid [cell size](@entry_id:139079). It is therefore modeled as a **sink particle**—a point mass that interacts gravitationally with the gas and accretes mass and momentum from surrounding grid cells [@problem_id:3533044]. A robust sink algorithm must enforce exact conservation of mass and momentum: the mass and momentum removed from the gas on the grid must be precisely equal to the mass and momentum added to the sink particle. The region from which the sink accretes, the accretion radius $R_{\mathrm{acc}}$, is typically tied to the physical **Bondi-Hoyle-Lyttleton (BHL) radius**, $R_{\mathrm{BHL}} = 2GM_s / (v_{\mathrm{rel}}^2 + c_s^2)$, which represents the [gravitational capture](@entry_id:174700) radius.

-   **Resolution Requirements:** To capture the physics of gravitational drag accurately, simulations must resolve the key physical length scales. These are the BHL radius, which sets the scale of the gravitational wake, and the local **pressure [scale height](@entry_id:263754)**, $H_P = c_s^2/g$, which sets the scale of vertical stratification [@problem_id:3533091]. A common criterion is to require a minimum of $N$ grid cells (e.g., $N=32$) across the smaller of these two lengths: $\Delta x \le \min(R_{\mathrm{BHL}}, H_P) / N$. Since the domain is vast and these scales are small, achieving this resolution everywhere is computationally prohibitive. This necessitates the use of **Adaptive Mesh Refinement (AMR)**, where the grid resolution is increased locally in regions of interest. The resolution criterion can be used to determine the maximum AMR level ($L_{\max}$) required near the companion, according to the relation $\Delta x(L) = L_{\mathrm{dom}} / (N_0 f^L)$, where $L_{\mathrm{dom}}$ is the domain size, $N_0$ is the base grid resolution, and $f$ is the refinement factor per level. Ensuring adequate resolution is paramount for obtaining numerically converged and physically meaningful results.