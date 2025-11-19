## Introduction
The behavior of interacting quantum particles, such as electrons in a metal or atoms in liquid helium, presents one of the most fundamental challenges in many-body physics. While the individual particles engage in a complex web of interactions, they often give rise to surprisingly simple and organized [collective motions](@entry_id:747472). Among the most fascinating of these are collective modes, particularly the phenomenon of [zero sound](@entry_id:142772)—a quantum mechanical sound wave that can propagate even in the absence of collisions. This article addresses the challenge of moving from the complex microscopic interactions to a coherent description of these macroscopic collective dynamics.

To unravel this topic, we will embark on a structured journey. The first chapter, "Principles and Mechanisms," establishes the foundational concepts of Landau's Fermi liquid theory, deriving the kinetic equation that governs quasiparticle dynamics and revealing the conditions under which [zero sound](@entry_id:142772) emerges. The second chapter, "Applications and Interdisciplinary Connections," explores the far-reaching implications of these ideas, examining how [zero sound](@entry_id:142772) manifests as plasmons in charged systems and serves as a crucial probe in [superfluids](@entry_id:180718), ultracold atoms, and even [neutron stars](@entry_id:139683). Finally, "Hands-On Practices" offers a set of targeted problems to deepen your analytical understanding of the core principles. We begin by delving into the theoretical heart of the matter: the principles and mechanisms of Fermi liquid theory.

## Principles and Mechanisms

This chapter delves into the theoretical underpinnings of collective excitations in interacting Fermi systems, focusing on the principles and mechanisms that give rise to phenomena such as [zero sound](@entry_id:142772). We will build our understanding from the foundational concepts of Landau's Fermi liquid theory, progress to the kinetic description of quasiparticle dynamics, and culminate in a detailed analysis of the properties and experimental signatures of these collective modes.

### Foundations of Landau's Fermi Liquid Theory

The description of interacting fermions, such as electrons in a metal or the atoms in liquid ³He, is a formidable many-body problem. At low temperatures, however, Lev Landau proposed a phenomenological framework that simplifies this problem immensely. The central idea is that the low-energy [excited states](@entry_id:273472) of an interacting system are in a one-to-one correspondence with the excited states of a non-interacting Fermi gas. The [elementary excitations](@entry_id:140859) of the interacting system are not the bare particles themselves, but rather **quasiparticles**. A quasiparticle can be visualized as a bare particle "dressed" by a cloud of surrounding particle-hole pairs, representing its complex interactions with the medium.

The state of the system is described by the [distribution function](@entry_id:145626) of these quasiparticles, $n_{\mathbf{k}\sigma}$, where $\mathbf{k}$ is momentum and $\sigma$ is spin. The total energy $E$ is a functional of this distribution. The energy of a single quasiparticle, $\epsilon_{\mathbf{k}\sigma}$, is defined as the change in the total energy of the system when one quasiparticle with quantum numbers $(\mathbf{k}, \sigma)$ is added:
$$
\epsilon_{\mathbf{k}\sigma} = \frac{\delta E}{\delta n_{\mathbf{k}\sigma}}
$$
Crucially, this quasiparticle energy is not a constant but is itself a functional of the distribution of all other quasiparticles. This dependence captures the essence of the interactions.

The effect of these interactions is quantified by the **Landau interaction function**, $f_{\mathbf{k}\sigma, \mathbf{k}'\sigma'}$. It represents the change in the energy of a quasiparticle $(\mathbf{k}, \sigma)$ due to the presence of another quasiparticle $(\mathbf{k}', \sigma')$. Mathematically, it is the second functional derivative of the total energy:
$$
f_{\mathbf{k}\sigma, \mathbf{k}'\sigma'} = \frac{\delta \epsilon_{\mathbf{k}\sigma}}{\delta n_{\mathbf{k}'\sigma'}} = \frac{\delta^2 E}{\delta n_{\mathbf{k}\sigma} \delta n_{\mathbf{k}'\sigma'}}
$$
For a homogeneous, isotropic, and paramagnetic system (invariant under translations, rotations, and spin rotations), the interaction function for quasiparticles on the Fermi surface ($|\mathbf{k}| = |\mathbf{k}'| = k_F$) simplifies considerably. It can depend only on the angle $\theta$ between the momenta $\mathbf{k}$ and $\mathbf{k}'$ and the relative spin orientation. Its most general form is:
$$
f_{\mathbf{k}\sigma, \mathbf{k}'\sigma'} = f^{s}(\cos\theta) + f^{a}(\cos\theta) \boldsymbol{\sigma} \cdot \boldsymbol{\sigma}'
$$
Here, $f^s(\cos\theta)$ is the **spin-symmetric** part, which governs interactions that are independent of spin, such as those mediating [density fluctuations](@entry_id:143540). The term $f^a(\cos\theta)$ is the **spin-antisymmetric** part, which mediates [spin-dependent interactions](@entry_id:158547) and is relevant for spin-density fluctuations.

Because $f^s$ and $f^a$ are functions on a sphere that only depend on the polar angle, they can be naturally expanded in the basis of **Legendre polynomials**, $P_{\ell}(\cos\theta)$:
$$
f^{s,a}(\cos\theta) = \sum_{\ell=0}^{\infty} f_{\ell}^{s,a} P_{\ell}(\cos\theta)
$$
The expansion coefficients $f_{\ell}^{s,a}$ are the fundamental [interaction parameters](@entry_id:750714) of the theory. To make them dimensionless and independent of system volume, they are multiplied by the [density of states](@entry_id:147894) at the Fermi level (per spin, per unit volume), $N(0)$. This defines the dimensionless **Landau parameters** [@problem_id:3024843]:
$$
F_{\ell}^{s,a} = N(0) f_{\ell}^{s,a}
$$
These parameters, which must be determined from experiment or a more microscopic theory, encode all the low-energy interaction effects and determine the thermodynamic and transport properties of the Fermi liquid. For instance, $F_0^s$ is related to the [compressibility](@entry_id:144559), $F_0^a$ to the [spin susceptibility](@entry_id:141223), and $F_1^s$ to the effective mass.

### The Dynamics of Quasiparticles

To understand collective modes, which are dynamic phenomena, we must study the time evolution of the quasiparticle [distribution function](@entry_id:145626), $n_{\mathbf{k}}(\mathbf{r}, t)$. This is governed by the **Landau kinetic equation**, a semiclassical Boltzmann-like equation that accounts for both the [self-consistent field](@entry_id:136549) of interactions and collisions [@problem_id:3024846].
$$
\frac{\partial n_{\mathbf{k}}}{\partial t} + \nabla_{\mathbf{k}}\epsilon_{\mathbf{k}} \cdot \nabla_{\mathbf{r}}n_{\mathbf{k}} - \nabla_{\mathbf{r}}\epsilon_{\mathbf{k}} \cdot \nabla_{\mathbf{k}}n_{\mathbf{k}} = \mathcal{I}_{\mathrm{coll}}[n]
$$
Here, $\mathcal{I}_{\mathrm{coll}}[n]$ is the [collision integral](@entry_id:152100) that drives the system towards equilibrium. The terms involving gradients describe the motion of quasiparticles in phase space under the influence of the spatially and temporally varying energy landscape $\epsilon_{\mathbf{k}}(\mathbf{r}, t)$.

For small deviations $\delta n_{\mathbf{k}}(\mathbf{r}, t)$ from a uniform equilibrium $n_{\mathbf{k}}^0$, the equation can be linearized. The quasiparticle energy becomes $\epsilon_{\mathbf{k}} = \epsilon_{\mathbf{k}}^0 + \delta\epsilon_{\mathbf{k}}$, where the energy shift $\delta\epsilon_{\mathbf{k}}$ includes any external potential $U_{\mathrm{ext}}$ and the self-consistent mean-field contribution from the [density fluctuations](@entry_id:143540) themselves:
$$
\delta\epsilon_{\mathbf{k}}(\mathbf{r}, t) = U_{\mathrm{ext}}(\mathbf{r}, t) + \sum_{\mathbf{k}'} f_{\mathbf{k}\mathbf{k}'} \delta n_{\mathbf{k}'}(\mathbf{r}, t)
$$
Substituting this into the kinetic equation and keeping only first-order terms yields the linearized Landau kinetic equation:
$$
\frac{\partial \delta n_{\mathbf{k}}}{\partial t} + \mathbf{v}_{\mathbf{k}} \cdot \nabla_{\mathbf{r}} \delta n_{\mathbf{k}} - \nabla_{\mathbf{r}} \delta\epsilon_{\mathbf{k}} \cdot \nabla_{\mathbf{k}} n_{\mathbf{k}}^0 = \mathcal{I}_{\mathrm{coll}}[\delta n]
$$
where $\mathbf{v}_{\mathbf{k}} = \nabla_{\mathbf{k}} \epsilon_{\mathbf{k}}^0$ is the equilibrium quasiparticle velocity. This equation forms the basis for studying all low-frequency, long-wavelength phenomena in a Fermi liquid.

### Hydrodynamic vs. Collisionless Regimes

The nature of the collective dynamics is determined by the competition between the oscillation frequency of a mode, $\omega$, and the quasiparticle collision rate, $1/\tau$. This competition is captured by the dimensionless parameter $\omega\tau$.

In the **hydrodynamic regime**, defined by $\omega\tau \ll 1$, collisions are extremely frequent. A quasiparticle undergoes many scattering events during a single period of the collective oscillation. This rapidly drives the system to a state of *local* thermodynamic equilibrium, described by local temperature, density, and velocity fields. The dynamics are governed by the conservation laws of fluid mechanics. The resulting collective mode is a pressure wave, known as **[first sound](@entry_id:144225)**. Its velocity, $c_1$, is determined by the isentropic compressibility of the liquid. For a Fermi liquid, this gives $c_1^2 = \frac{v_F^2}{3}(1+F_0^s)$, where $v_F$ is the Fermi velocity. Damping in this regime is due to [transport phenomena](@entry_id:147655) like viscosity and scales with the [wavevector](@entry_id:178620) as $q^2$ [@problem_id:3024823].

In the opposite limit, the **collisionless regime**, defined by $\omega\tau \gg 1$, a quasiparticle oscillates for many periods before it scatters. Collisions are negligible, and the [collision integral](@entry_id:152100) $\mathcal{I}_{\mathrm{coll}}$ can be dropped from the kinetic equation. The system is driven far from [local equilibrium](@entry_id:156295). The dynamics are now dominated by the [mean-field interaction](@entry_id:200557) term, where quasiparticles move in a self-consistent potential generated by the [density fluctuations](@entry_id:143540). If the interaction is sufficiently repulsive ($F_0^s > 0$), it can provide a restoring force that sustains a collective [density wave](@entry_id:199750) even without collisions. This uniquely quantum mechanical mode is called **[zero sound](@entry_id:142772)** [@problem_id:3024823]. The criterion $\omega\tau \gg 1$ can be expressed spatially: since $\omega \approx c_0 q$ (where $c_0$ is the [zero sound](@entry_id:142772) velocity) and the mean free path is $l = v_F \tau$, the condition is equivalent to $q l \gg c_0/v_F$, meaning the mean free path is much larger than the wavelength of the oscillation [@problem_id:3024823].

### The Mechanism of Zero Sound

To investigate the properties of [zero sound](@entry_id:142772), we analyze the collisionless Landau kinetic equation. For a plane-wave perturbation of the form $\delta n_{\mathbf{k}} \propto \phi(\hat{\mathbf{p}}) \exp[i(\mathbf{q}\cdot\mathbf{r} - \omega t)]$, where $\phi(\hat{\mathbf{p}})$ describes the angular distortion of the Fermi surface, the kinetic equation transforms into an integral equation for $\phi(\hat{\mathbf{p}})$ [@problem_id:3024822]. For longitudinal oscillations, this equation is:
$$
(\omega - \mathbf{q} \cdot \mathbf{v}_{\mathbf{p}}) \phi(\hat{\mathbf{p}}) = (\mathbf{q} \cdot \mathbf{v}_{\mathbf{p}}) \sum_{\ell} F_\ell^s \int \frac{d\Omega'}{4\pi} P_{\ell}(\hat{\mathbf{p}}\cdot\hat{\mathbf{p}}') \phi(\hat{\mathbf{p}}')
$$

A crucial concept for understanding whether a mode can propagate without damping is the **[particle-hole continuum](@entry_id:191825)**. This is the region in the $(\omega, q)$ plane where it is kinematically possible to create a single particle-hole excitation by exciting a quasiparticle from an occupied state inside the Fermi sea to an empty state outside. At zero temperature, this corresponds to pairs of energy $\hbar\omega$ and momentum $\hbar\mathbf{q}$ that satisfy $\hbar\omega \le \hbar q v_F$. In terms of the dimensionless velocity $s = \omega / (q v_F)$, the [particle-hole continuum](@entry_id:191825) occupies the region $s \le 1$.

If a collective mode has a phase velocity that falls within this region ($s \le 1$), its energy and momentum can be resonantly absorbed by quasiparticles moving with the same velocity component along $\mathbf{q}$ (i.e., $\mathbf{v}_{\mathbf{p}} \cdot \hat{\mathbf{q}} = \omega/q$). This [resonant energy transfer](@entry_id:191410) constitutes a powerful decay mechanism known as **Landau damping**. A collective mode that is Landau-damped is not a long-lived, well-defined excitation.

For a well-defined, undamped collective mode to exist, its phase velocity must lie outside the [particle-hole continuum](@entry_id:191825), meaning its dispersion must satisfy $s > 1$. In this case, no single quasiparticle can keep up with the wave to absorb energy from it, and Landau damping is kinematically forbidden [@problem_id:3024883]. The denominator $\omega - \mathbf{q} \cdot \mathbf{v}_{\mathbf{p}}$ in the kinetic response never vanishes, the [response function](@entry_id:138845) is purely real, and there is no dissipation.

Let's seek such a solution by considering only the dominant interaction parameter for density waves, $F_0^s$. The integral equation for $\phi$ can be solved, and a non-[trivial solution](@entry_id:155162) requires that the parameters satisfy a specific dispersion relation [@problem_id:3024822]:
$$
\frac{1}{F_0^s} = \frac{1}{2} \int_{-1}^{1} d\mu \frac{\mu}{s-\mu}
$$
where $\mu = \cos\theta = \hat{\mathbf{p}} \cdot \hat{\mathbf{q}}$. The integral on the right-hand side can be evaluated analytically for $s>1$, yielding the function $\Phi(s)$:
$$
\Phi(s) = -1 + \frac{s}{2} \ln\left(\frac{s+1}{s-1}\right)
$$
The dispersion relation for [zero sound](@entry_id:142772) is thus $1/F_0^s = \Phi(s)$. By analyzing the function $\Phi(s)$, we find that it is positive and monotonically decreasing for $s \in (1, \infty)$, approaching $+\infty$ as $s \to 1^+$ and $0$ as $s \to \infty$. Therefore, for this equation to have a solution for $s>1$, we must have $1/F_0^s > 0$, which implies $F_0^s > 0$. This confirms our intuition: a repulsive interaction is required to provide the restoring force for a collisionless density wave. Furthermore, as the repulsive [interaction strength](@entry_id:192243) $F_0^s$ increases, $1/F_0^s$ decreases. Since $\Phi(s)$ is a decreasing function of $s$, this means $s$ must increase. A stronger repulsion leads to a faster [zero sound](@entry_id:142772) mode, moving it further away from the [particle-hole continuum](@entry_id:191825) [@problem_id:3024871].

### Experimental Probes and Related Phenomena

Collective modes are not mere theoretical constructs; they appear as distinct features in experimental measurements. A key experimental probe is inelastic scattering (of neutrons or X-rays), which measures the **[dynamic structure factor](@entry_id:143433)**, $S(\mathbf{q}, \omega)$. This function describes the probability that the system absorbs energy $\hbar\omega$ and momentum $\hbar\mathbf{q}$ from the probe.

The [dynamic structure factor](@entry_id:143433) is not an independent quantity; it is deeply connected to the dissipative part of the system's linear response. This connection is formalized by the **Fluctuation-Dissipation Theorem (FDT)**, which states [@problem_id:3024851]:
$$
S(\mathbf{q}, \omega) = -\frac{2\hbar}{1 - e^{-\beta\hbar\omega}} \mathrm{Im}\,\chi_{nn}(\mathbf{q}, \omega)
$$
where $\chi_{nn}(\mathbf{q}, \omega)$ is the retarded density-density response function and $\beta = 1/(k_B T)$. A weakly damped collective mode, like [zero sound](@entry_id:142772), appears as a sharp pole in the response function. For a pole at frequency $\omega_0(\mathbf{q})$ with a small damping rate $\gamma(\mathbf{q})$, the imaginary part of $\chi_{nn}$ is a Lorentzian function peaked at $\omega_0$. The FDT then implies that the [zero sound](@entry_id:142772) mode will manifest in $S(\mathbf{q}, \omega)$ as a sharp Lorentzian peak at the [zero sound](@entry_id:142772) frequency $\omega_0(\mathbf{q})$. In the ideal limit of zero damping ($\gamma \to 0$), this peak becomes an infinitely sharp [delta function](@entry_id:273429), $\delta(\omega - \omega_0(\mathbf{q}))$, signifying a stable, infinitely long-lived excitation [@problem_id:3024851].

The nature of collective modes is highly dependent on the range of the underlying interaction. Zero sound arises from the short-range part of the interaction between quasiparticles. In a charged Fermi liquid, such as a [two-dimensional electron gas](@entry_id:146876) (2DEG), the long-range Coulomb interaction ($V(q) \propto 1/q$) dominates. This leads to a different kind of collective density wave: the **plasmon**. Using a similar kinetic approach within the Random Phase Approximation (RPA), one finds that the 2D [plasmon](@entry_id:138021) is gapless, with a characteristic dispersion $\omega_p \propto \sqrt{q}$ at long wavelengths. This unusual square-root dispersion arises from the interplay between the $1/q$ interaction and a density response that scales as $q^2$. Because $\sqrt{q}$ grows faster than the boundary of the [particle-hole continuum](@entry_id:191825) ($v_F q$) at small $q$, the 2D [plasmon](@entry_id:138021) is undamped at long wavelengths. However, as $q$ increases, the [plasmon dispersion](@entry_id:197117) curve eventually intersects the continuum boundary at a characteristic wavevector $q_*$, beyond which the [plasmon](@entry_id:138021) becomes susceptible to Landau damping and ceases to be a well-defined mode [@problem_id:3024825].

### Advanced Considerations

#### Crossover and Broken Symmetries

Our discussion has treated the hydrodynamic and collisionless regimes as distinct. In reality, there is a continuous crossover between them as the parameter $\omega\tau$ is varied. A unified theory capable of describing this crossover must correctly interpolate between the two limits. This can be achieved by employing a more sophisticated [kinetic theory](@entry_id:136901) that uses a particle-number-conserving form of the [relaxation-time approximation](@entry_id:138429) (RTA) for the [collision integral](@entry_id:152100). By constructing the density [response function](@entry_id:138845) to satisfy key constraints like the static [compressibility](@entry_id:144559) in the $\omega\tau \to 0$ limit and the collisionless response in the $\omega\tau \to \infty$ limit, a continuous evolution of the sound mode pole from the first-sound velocity to the zero-sound velocity is obtained [@problem_id:3024881].

A final, crucial distinction arises between systems that possess **Galilean invariance** (like liquid ³He, to a good approximation) and those that do not (like electrons in a crystal lattice). In a Galilean invariant system, a powerful Ward identity enforces a direct relationship between the [quasiparticle effective mass](@entry_id:140437) $m^*$ and the Landau parameter $F_1^s$: $m^*/m = 1 + F_1^s/3$. This links the two sound velocities, as both depend on this set of parameters.

On a lattice, Galilean invariance is broken by the [periodic potential](@entry_id:140652) of the ions. The relation between $m^*$ and $F_1^s$ no longer holds; they become independent parameters. The [inertial mass](@entry_id:267233) in the hydrodynamic sound velocity formula is the band mass $m_b$, leading to $c_1^2 \propto (1+F_0^s)(m^*/m_b)$. In contrast, the collisionless [zero sound](@entry_id:142772) velocity $c_0$ is determined primarily by $F_0^s$ and the quasiparticle velocity $v_F^* = \hbar k_F/m^*$, with no direct dependence on $m_b$ or $F_1^s$ at leading order. The breaking of Galilean invariance thus decouples the two sound velocities, and there is no fundamental reason for them to be similar in magnitude in an electronic system [@problem_id:3024886]. This subtle point underscores the importance of underlying symmetries in determining the macroscopic properties of [quantum fluids](@entry_id:140332).