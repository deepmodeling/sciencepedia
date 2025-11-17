## Introduction
Energy and momentum conservation is a cornerstone of physics, providing a powerful lens through which to understand nearly every physical system. However, when applied to the universe as a whole, this familiar principle reveals profound and counter-intuitive consequences. In the context of general relativity, the dynamic, expanding nature of spacetime means that the total energy of the cosmos is not, in general, conserved. This article addresses the apparent contradiction between this foundational principle and the observed reality of our evolving universe, providing a rigorous yet intuitive guide to the dynamics of energy and momentum on a cosmological scale.

Across the following chapters, you will embark on a journey from abstract principles to concrete applications. The first chapter, **Principles and Mechanisms**, will lay the groundwork by introducing the concept of [local conservation](@entry_id:751393) in curved spacetime and deriving the crucial fluid equation that governs the evolution of cosmic energy density. You will learn why different components like matter, radiation, and vacuum energy behave so differently as the universe expands. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how these principles are essential tools for understanding [the thermal history of the universe](@entry_id:204719), the formation of galaxies, and even speculative theories about dark energy and [quantum gravity](@entry_id:145111). Finally, the **Hands-On Practices** chapter offers an opportunity to actively engage with these concepts, challenging you to solve problems that illuminate the real-world consequences of these cosmological laws.

## Principles and Mechanisms

Having established the foundational kinematic framework of an expanding universe in the previous chapter, we now turn to the dynamical principles that govern the evolution of its material and energetic contents. At the heart of this discussion lies the concept of energy and momentum conservation. While this principle is a cornerstone of physics, its application in the context of general relativity and an evolving spacetime reveals profound and counter-intuitive consequences, most notably that the total energy in an expanding universe is, in general, not conserved. This chapter will derive the fundamental equations governing energy evolution, interpret their physical meaning, and explore the microscopic mechanisms responsible for the changing energy content of the cosmos.

### The Law of Local Conservation in General Relativity

In the flat spacetime of special relativity, the [conservation of energy and momentum](@entry_id:193044) for any system described by a stress-energy tensor, $T^{\mu\nu}$, is expressed by the vanishing of its ordinary four-divergence: $\partial_{\mu}T^{\mu\nu} = 0$. Integrated over a spatial volume, this local law gives rise to globally conserved quantities of energy and momentum, provided the system is isolated.

General relativity, however, is built upon the **[principle of general covariance](@entry_id:157638)**, which demands that physical laws be written in a form independent of the observer's coordinate system. This is achieved by replacing ordinary derivatives ($\partial_{\mu}$) with **covariant derivatives** ($\nabla_{\mu}$), which correctly account for the curvature of spacetime. Consequently, the law of [energy-momentum conservation](@entry_id:191061) is generalized to:

$$ \nabla_{\mu}T^{\mu\nu} = 0 $$

It is crucial to recognize that this is not merely a notational change. The covariant derivative includes terms involving the Christoffel symbols, which encode the properties of the gravitational field. The equation $\nabla_{\mu}T^{\mu\nu} = 0$ does not imply that the energy-momentum of matter and radiation is conserved in isolation. Instead, it must be interpreted as a statement of local *exchange*: it describes the flow of energy and momentum *between* the material contents of the universe and the gravitational field itself. [@problem_id:1832860] The energy of matter can decrease, for instance, by doing work on the [expanding spacetime](@entry_id:161389).

The question of whether a globally conserved total energy (including gravity's contribution) can be defined is a deep and subtle one. In general relativity, such a conserved quantity exists only if the spacetime possesses a specific symmetry—namely, a continuous [time-translation invariance](@entry_id:270209). This symmetry is mathematically represented by the existence of a global, future-directed, **timelike Killing vector field**. [@problem_id:1814665] A static, unchanging spacetime possesses such a vector, and thus a conserved energy. However, the Friedmann-Lemaître-Robertson-Walker (FLRW) metric, which describes our expanding universe, is explicitly time-dependent. It lacks a global timelike Killing vector, and as a consequence, there is no universally applicable definition of total conserved energy.

### The Fluid Equation in an Expanding Universe

While global energy is not conserved, the [local conservation law](@entry_id:261997) $\nabla_{\mu}T^{\mu\nu}=0$ remains a powerful tool. For the homogeneous and isotropic universe described by the FLRW metric, we can model the cosmic contents as a **[perfect fluid](@entry_id:161909)**. Its [stress-energy tensor](@entry_id:146544) is given by $T^{\mu\nu} = (\rho + p)u^{\mu}u^{\nu} + p g^{\mu\nu}$, where $\rho$ is the energy density, $p$ is the pressure, and $u^{\mu}$ is the [four-velocity](@entry_id:274008) of the fluid, which is at rest in [comoving coordinates](@entry_id:271238), $u^{\mu}=(1,0,0,0)$.

By explicitly calculating the $\nu=0$ component of $\nabla_{\mu}T^{\mu\nu}=0$ in the spatially flat FLRW metric, the covariant derivatives and Christoffel symbols combine to yield a remarkably simple and fundamental equation governing the evolution of the energy density. This is the **fluid equation**, or the continuity equation of cosmology [@problem_id:1837236]:

$$ \dot{\rho} + 3H(\rho+p) = 0 $$

Here, the dot denotes a derivative with respect to cosmological time $t$, and $H = \dot{a}/a$ is the Hubble parameter. This equation is one of the pillars of modern cosmology, describing how the energy density of any fluid component changes as the universe expands.

A powerful physical intuition for this equation comes from thermodynamics. Consider a comoving region of space with a fixed coordinate volume. Its physical volume expands with the universe as $V(t) \propto a(t)^3$. The total energy of the fluid within this volume is $E = \rho V$. If we differentiate this expression for energy and substitute the fluid equation, we arrive at an expression identical in form to the [first law of thermodynamics](@entry_id:146485) [@problem_id:824419]:

$$ dE = -p dV $$

This elegant result provides a clear physical picture: the change in energy within a comoving patch of the universe is equal to the work done by the pressure of the fluid as the volume expands. If a component has positive pressure ($p > 0$), it does positive work on the expansion, and its internal energy decreases. If a component has zero pressure, it does no work, and its energy is conserved. This thermodynamic analogy is the key to understanding why the energy of some components is conserved while that of others is not.

### Evolution of Cosmological Components

The behavior of different substances in the expanding universe is dictated by their **equation of state**, which relates their pressure to their energy density. For many [cosmological fluids](@entry_id:159433), this relationship can be approximated by a simple linear equation of state, $p = w\rho$, where $w$ is the dimensionless **[equation of state parameter](@entry_id:159133)**.

By substituting $p=w\rho$ into the fluid equation and solving the resulting differential equation, we find the universal scaling relation for the energy density of any such component [@problem_id:824337]:

$$ \rho(a) = \rho_0 \left(\frac{a}{a_0}\right)^{-3(1+w)} $$

where $\rho_0$ is the energy density at a reference [scale factor](@entry_id:157673) $a_0$. Let us examine the three most important components of the [standard cosmological model](@entry_id:159833).

**1. Non-Relativistic Matter (Dust)**
For non-relativistic matter (like galaxies or cold dark matter), the particles have random thermal velocities that are negligible compared to the speed of light. Their pressure is effectively zero, so $w=0$. The scaling relation becomes:

$$ \rho_m \propto a^{-3} $$

The energy density of matter simply dilutes as the inverse of the volume, which is what one would intuitively expect for a fixed number of particles in an expanding box. The energy in a comoving volume, $E_m = \rho_m V \propto a^{-3}a^3$, is **constant**. This aligns perfectly with our thermodynamic picture: with $p=0$, no work is done, and energy is conserved.

**2. Radiation**
For relativistic particles like photons and neutrinos, [kinetic theory](@entry_id:136901) shows that their pressure is one-third of their energy density, so $w=1/3$. The scaling relation is then:

$$ \rho_r \propto a^{-4} $$

The energy density of radiation decreases faster than that of matter. The total energy of radiation in a comoving volume is therefore not conserved [@problem_id:1837205]:

$$ E_r = \rho_r V \propto a^{-4}a^3 = a^{-1} $$

The total energy of a [photon gas](@entry_id:143985) in an expanding volume *decreases*. This is a direct consequence of the positive pressure of the radiation field. As the universe expands, the photon gas does work, and its energy diminishes. This energy is not transferred to another component; it is lost to the [expansion of spacetime](@entry_id:161127) itself. We can quantify this work. For instance, the total work done by the [photon gas](@entry_id:143985) per unit volume from the epoch of [matter-radiation equality](@entry_id:161150) ($a_{eq}$) until today ($a=1$) is given by $w_\gamma = \rho_{\gamma,0}(a_{eq}^{-1}-1)$ [@problem_id:824419].

**3. Cosmological Constant (Vacuum Energy)**
The cosmological constant, or [vacuum energy](@entry_id:155067), has the peculiar property that its energy density, $\rho_{\Lambda}$, is constant in both space and time. This implies that $\dot{\rho}_{\Lambda} = 0$. For the fluid equation to hold, we must have $\rho_{\Lambda} + p_{\Lambda} = 0$, which yields an [equation of state parameter](@entry_id:159133) $w = -1$. The scaling relation correctly gives $\rho_{\Lambda} \propto a^0 = \text{constant}$. The consequence for the total energy in a comoving volume is startling:

$$ E_{\Lambda} = \rho_{\Lambda} V \propto a^3 $$

The total energy of the vacuum *increases* as the universe expands. In the thermodynamic picture, the [negative pressure](@entry_id:161198) $p_{\Lambda} = -\rho_{\Lambda}$ means that the expansion does work *on* the vacuum, increasing its energy content.

### Microscopic Origins of Energy Dilution

The macroscopic fluid description can be complemented by a microscopic particle perspective. The decay of energy for both relativistic and non-relativistic particles can be traced to a single underlying phenomenon: the redshifting of momentum. For any [free-streaming](@entry_id:159506) particle (one not subject to non-gravitational forces), its physical momentum $p$ decays inversely with the scale factor:

$$ p \propto \frac{1}{a(t)} $$

For a **photon**, its energy is given by $E=pc$. Therefore, its energy also redshifts as $E \propto 1/a$. This is the microscopic explanation for the macroscopic result $E_r \propto a^{-1}$. This effect is directly observable as the **[cosmological redshift](@entry_id:152343)** of light from distant galaxies; the wavelength of a photon stretches with the universe, $\lambda \propto a$, and since $E=hc/\lambda$, its energy decreases. [@problem_id:1864049]

For a massive **non-relativistic particle**, its energy is dominated by its rest mass energy $mc^2$, with a small amount of kinetic energy $K = p^2/(2m)$. While the total energy is approximately constant, its peculiar motion relative to the [cosmic rest frame](@entry_id:194833) is damped. The kinetic energy decays as:

$$ K = \frac{p^2}{2m} \propto \left(\frac{1}{a}\right)^2 = a^{-2} $$

This means that any initial random velocities of non-relativistic particles are "cooled" by the [cosmic expansion](@entry_id:161002). For a particle that is initially relativistic, its evolution is more complex. As the universe expands, its momentum decays, and it will eventually become non-relativistic. The full evolution of its kinetic energy, starting from an initial value $K_i$ at [scale factor](@entry_id:157673) $a_i$, is given by the relativistic expression [@problem_id:824358]:

$$ K_f = \sqrt{\bigl(K_i^2 + 2K_i mc^2\bigr)\Bigl(\frac{a_i}{a_f}\Bigr)^2 + m^2c^4} - mc^2 $$
This general formula correctly reproduces the $K \propto a^{-2}$ behavior in the [non-relativistic limit](@entry_id:183353) ($K \ll mc^2$) and the $K \approx E \propto a^{-1}$ behavior in the ultra-relativistic limit ($K \gg mc^2$).

### Thermal Evolution and Entropy Conservation

The cooling of cosmic components can also be analyzed from the perspective of statistical mechanics. For a dilute, non-relativistic monatomic gas undergoing an [adiabatic expansion](@entry_id:144584), its entropy is conserved. Using the Sackur-Tetrode formula for entropy, one can show that this conservation implies a temperature evolution of $T \propto a^{-2}$ [@problem_id:824374]. This provides a thermodynamic justification for the kinetic energy scaling $K \propto a^{-2}$ derived from momentum redshift, since for a non-relativistic gas, $K \propto T$.

While energy in a comoving volume is not generally conserved, **entropy** is. For a system in thermal equilibrium, the total entropy $S = s a^3$ within a comoving volume remains constant, where $s$ is the physical entropy density. For a bath of relativistic particles, the entropy density is dominated by these species and is given by $s = \frac{2\pi^2}{45}g_*(T)T^3$, where $g_*(T)$ is the effective number of relativistic degrees of freedom at temperature $T$.

If $g_*$ were a constant, [entropy conservation](@entry_id:749018) ($s a^3 = \text{const}$) would imply $T^3 a^3 = \text{const}$, or $T \propto 1/a$. This simple scaling law holds for much of the universe's history. However, at certain epochs, the temperature drops to become comparable to the rest mass energy of a particle species ($k_B T \approx mc^2$). These particles then annihilate and cease to be relativistic, causing $g_*$ to decrease. During this transition, the entropy from the annihilating species is transferred to the remaining relativistic particles (primarily photons). This injection of entropy slows down the cooling rate of the photon bath. The temperature no longer scales as $1/a$ but follows a more complex evolution determined by the precise functional form of $g_*(T)$. [@problem_id:824367] This process of "reheating" is a crucial feature of [the thermal history of the universe](@entry_id:204719), ensuring a continuous and calculable relationship between temperature and the [scale factor](@entry_id:157673), even as the particle content of the cosmos evolves.

In summary, the dynamics of energy and momentum in an [expanding universe](@entry_id:161442) are governed by the principle of local covariant conservation, which translates into a thermodynamic exchange between the cosmic fluid and the [expanding spacetime](@entry_id:161389) itself. This leads to the [non-conservation of energy](@entry_id:276143) for components with non-zero pressure, a phenomenon rooted in the redshifting of particle momenta. While energy is a fluid concept, comoving entropy provides a more robust conserved quantity, shaping the detailed [thermal history](@entry_id:161499) of our universe.