## Introduction
The Cold Dark Matter (CDM) model has been remarkably successful in explaining the large-scale structure of the universe, but tensions with observations on smaller scales have motivated the exploration of alternatives. Among the most compelling of these is Warm Dark Matter (WDM), which posits that dark matter particles possessed a significant primordial velocity. This intrinsic "warmth" provides a natural mechanism for suppressing the formation of small-scale structures, potentially resolving discrepancies like the predicted overabundance of dwarf galaxies. However, accurately modeling the cosmological consequences of WDM requires moving beyond simple theoretical prescriptions and tackling the complex, [non-linear dynamics](@entry_id:190195) through numerical simulation. This introduces a host of unique theoretical and computational challenges, from correctly initializing particle velocities to distinguishing physical phenomena from numerical artifacts.

This article provides a graduate-level guide to the theory and practice of simulating Warm Dark Matter. It is designed to bridge the gap between abstract [kinetic theory](@entry_id:136901) and the practical implementation in cosmological N-body codes. The first chapter, **Principles and Mechanisms**, will delve into the fundamental physics of WDM, deriving the Vlasov-Poisson system and explaining how primordial velocities lead to the characteristic [free-streaming](@entry_id:159506) effect. The second chapter, **Applications and Interdisciplinary Connections**, will explore how these principles are applied to constrain WDM models with observational data and connect to broader topics in particle physics and statistical mechanics. Finally, **Hands-On Practices** will present a series of targeted problems designed to solidify understanding of the key numerical techniques and challenges inherent in creating high-fidelity WDM simulations.

## Principles and Mechanisms

### The Kinetic Theory of Warm Dark Matter

The fundamental distinction between Cold Dark Matter (CDM) and Warm Dark Matter (WDM) is rooted in the primordial velocity dispersion of the constituent particles. In the [standard cosmological model](@entry_id:159833), CDM particles are assumed to have negligible thermal velocities from the moment of their creation. This physical property is mathematically idealized by a [phase-space distribution](@entry_id:151304) function, $f_{\mathrm{CDM}}(\mathbf{p})$, that approximates a Dirac delta function in momentum space, $f_{\mathrm{CDM}}(\mathbf{p}) \propto \delta^{(3)}(\mathbf{p})$. In stark contrast, WDM consists of particles that decoupled from the primordial thermal bath while still relativistic, thereby inheriting a significant thermal motion that persists throughout cosmic history.

For a canonical WDM candidate, such as a sterile neutrino, that is a fermionic thermal relic, its primordial [phase-space distribution](@entry_id:151304) is described by the **Fermi-Dirac distribution**:

$f_{\mathrm{WDM}}(p, t) = \frac{g_s}{(2\pi\hbar)^3} \frac{1}{\exp(p(t)/T_w(t))+1}$

where $p(t)$ is the physical momentum, $T_w(t)$ is the [effective temperature](@entry_id:161960) of the WDM species, and $g_s$ is the number of internal (spin) degrees of freedom. In cosmological contexts, it is common to work in units where $k_B = \hbar = 1$. The "warmth" of WDM is entirely encapsulated by the finite width of this momentum distribution.

As the universe expands, a freely streaming particle's physical momentum redshifts due to the stretching of spacetime. For a particle subject to no peculiar forces, the [geodesic equation](@entry_id:136555) in a Friedmann–Lemaître–Robertson–Walker (FLRW) metric yields the simple relation $p(t) \propto a(t)^{-1}$, where $a(t)$ is the [scale factor](@entry_id:157673). Similarly, the temperature of any decoupled relativistic species redshifts as $T_w(t) \propto a(t)^{-1}$. A crucial consequence of this identical scaling is that the ratio $p(t)/T_w(t)$ remains constant over time. This implies that the shape of the WDM [phase-space distribution](@entry_id:151304), when expressed in terms of the **comoving momentum** $\mathbf{q} \equiv a(t)\mathbf{p}(t)$, is "frozen in" after decoupling. Since both $p$ and $T_w$ scale as $a^{-1}$, the distribution can be written as a time-independent function of $q$, $f(q) = (\dots)/(e^{q/T_{w,0}}+1)$, where $T_{w,0}$ is a constant. This conservation is a manifestation of Liouville's theorem for a collisionless fluid in a homogeneous background .

For a non-relativistic particle of mass $m_\chi$, the peculiar velocity $v_{\mathrm{pec}}$ is related to the physical momentum by $v_{\mathrm{pec}} = p/m_\chi$. Since $p \propto a^{-1}$, the peculiar velocities of WDM particles also [redshift](@entry_id:159945) with the expansion:

$v_{\mathrm{pec}}(a) \propto a^{-1}$

Consequently, the non-[relativistic kinetic energy](@entry_id:176527), $E_k = \frac{1}{2}m_\chi v_{\mathrm{pec}}^2$, redshifts more rapidly, with $E_k \propto a^{-2}$ .

The evolution of a collection of collisionless particles under self-gravity is governed by the **Vlasov-Poisson system**. In an [expanding universe](@entry_id:161442), it is most convenient to formulate these equations in [comoving coordinates](@entry_id:271238) $\mathbf{x}$ (where physical position $\mathbf{r} = a\mathbf{x}$) and peculiar velocity $\mathbf{v}$ (defined such that physical velocity $\mathbf{u} = H\mathbf{r} + \mathbf{v}$). The Vlasov equation, expressing the conservation of the [phase-space density](@entry_id:150180) $f(\mathbf{x}, \mathbf{v}, t)$ along particle trajectories, becomes :

$\frac{\partial f}{\partial t} + \frac{\mathbf{v}}{a} \cdot \nabla_{\mathbf{x}} f - \left( \frac{\nabla_{\mathbf{x}}\phi}{a} + H\mathbf{v} \right) \cdot \nabla_{\mathbf{v}} f = 0$

Here, the second term, $(\mathbf{v}/a) \cdot \nabla_{\mathbf{x}} f$, represents **streaming**: particles with [peculiar velocity](@entry_id:157964) $\mathbf{v}$ move across comoving coordinate grids. The term $(\nabla_{\mathbf{x}}\phi/a) \cdot \nabla_{\mathbf{v}} f$ accounts for the acceleration due to peculiar gravitational forces, derived from the peculiar potential $\phi$. The final term, $(H\mathbf{v}) \cdot \nabla_{\mathbf{v}} f$, is the **Hubble drag**, a fictitious force arising from the use of an accelerating coordinate system, which ensures that peculiar velocities are correctly redshifted. The potential $\phi$ is sourced by [density fluctuations](@entry_id:143540) via the comoving Poisson equation:

$\nabla_{\mathbf{x}}^2\phi = 4\pi G a^2 (\rho - \bar{\rho})$

Crucially, the effects of WDM's thermal motion are entirely contained within the initial condition for $f$—specifically, its finite velocity dispersion. There are no explicit pressure or collision terms in the Vlasov equation, as the particles are, by definition, collisionless .

### Free-Streaming and the Suppression of Small-Scale Structure

The most significant cosmological consequence of WDM's primordial velocity dispersion is **[free-streaming](@entry_id:159506)**. At early times, high-velocity WDM particles can travel large distances, effectively escaping from small-scale overdense regions and smoothing out density fluctuations. This process introduces a characteristic scale into the matter distribution, below which [structure formation](@entry_id:158241) is suppressed.

This scale can be quantified by the **comoving [free-streaming](@entry_id:159506) horizon**, $\lambda_{\mathrm{fs}}(a)$, which represents the maximum [comoving distance](@entry_id:158059) a typical WDM particle could have traveled from the early universe ($a' \to 0$) until a time corresponding to scale factor $a$. It is defined by the integral:

$\lambda_{\mathrm{fs}}(a) = \int_{0}^{t(a)} \frac{v_{\mathrm{pec}}(t')}{a(t')} dt' = \int_{0}^{a} \frac{v_{\mathrm{pec}}(a')}{a'^2 H(a')} da'$

To evaluate this, we consider the different epochs of cosmic history. For a typical keV-scale WDM particle, there is a transition from relativistic ($v_{\mathrm{pec}} \approx c$) to non-relativistic behavior at a [scale factor](@entry_id:157673) $a_{\mathrm{nr}}$, which occurs well before [matter-radiation equality](@entry_id:161150) at $a_{\mathrm{eq}}$. The integral can be split into three parts: (i) relativistic motion during radiation domination ($a' \lt a_{\mathrm{nr}}$), (ii) non-relativistic motion during radiation domination ($a_{\mathrm{nr}} \lt a' \lt a_{\mathrm{eq}}$), and (iii) non-relativistic motion during matter domination ($a' \gt a_{\mathrm{eq}}$).

The key insight from this calculation is that the integral is dominated by the earliest epochs when velocities were highest and the universe was expanding most rapidly. The contribution from the [matter-dominated era](@entry_id:272362) converges quickly because the particle's velocity redshifts away ($v_{\mathrm{pec}} \propto a'^{-1}$) while the expansion slows. As a result, $\lambda_{\mathrm{fs}}(a)$ asymptotes to a nearly constant value at late times ($a \gg a_{\mathrm{eq}}$). This "fossil" scale, set by physics around $a_{\mathrm{nr}}$ and $a_{\mathrm{eq}}$, becomes the characteristic [cutoff scale](@entry_id:748127) for [structure formation](@entry_id:158241) .

This suppression is fundamentally a kinetic and non-local effect, reflecting the entire [thermal history](@entry_id:161499) of the particles. It is crucial to distinguish it from the Jeans instability in a collisional fluid. While one can define an effective Jeans scale, $k_J(a) = \sqrt{4\pi G \bar{\rho} a^2 / c_s^2}$, using the WDM velocity dispersion as an effective sound speed $c_s$, this scale describes an instantaneous balance between pressure and gravity. Simulations and theoretical analysis show that the suppression of the linear [growth of structure](@entry_id:158527) is accurately predicted by the integrated [free-streaming](@entry_id:159506) scale ($k_{\mathrm{fs}} \sim 1/\lambda_{\mathrm{fs}}$), not the instantaneous Jeans scale, which can differ by orders of magnitude at late times .

The result of [free-streaming](@entry_id:159506) is a scale-dependent suppression of the [linear matter power spectrum](@entry_id:751315), $P(k)$, compared to the CDM case. This is described by the **WDM transfer function**, $T(k)$, defined such that $P_{\mathrm{WDM}}(k) = T^2(k) P_{\mathrm{CDM}}(k)$. For $k \ll k_{\mathrm{fs}}$, $T(k) \approx 1$, while for $k \gg k_{\mathrm{fs}}$, $T(k)$ falls off rapidly. A widely used fitting formula that captures this behavior is :

$T(k) = \left[1 + (\alpha k)^{2\nu}\right]^{-5/\nu}$

where $\alpha$ is a parameter related to the [free-streaming](@entry_id:159506) scale (and thus the WDM particle mass), and $\nu \approx 1.12$ is a [shape parameter](@entry_id:141062) found to be nearly universal for thermal relics.

### Simulating Warm Dark Matter

Modeling the evolution of WDM in a cosmological N-body simulation requires careful treatment of both the initial conditions and the subsequent [numerical integration](@entry_id:142553).

#### Initial Conditions

A WDM simulation cannot be initialized simply by using a "cold" particle distribution with a suppressed initial power spectrum. While applying the WDM transfer function $T(k)$ to a [primordial power spectrum](@entry_id:159340) correctly sets up the initial density field, it is equally important to impart the correct thermal velocities to the simulation particles. These velocities are not merely a historical relic; they act as a velocity dispersion that continues to resist [gravitational collapse](@entry_id:161275) on small scales throughout the simulation. Omitting these "velocity kicks" leads to artificial fragmentation of filaments and the spurious formation of small halos, fundamentally misrepresenting the non-linear evolution .

The procedure for assigning these thermal velocities is to give each particle a random velocity kick drawn from the primordial distribution. A particle's peculiar velocity, $\mathbf{v}$, is related to its physical momentum $\mathbf{p}$ by $\mathbf{v} = \mathbf{p}/m_\chi$. Since the physical momentum of a [free-streaming](@entry_id:159506) particle redshifts as $p \propto a^{-1}$, the [peculiar velocity](@entry_id:157964) does as well: $\mathbf{v}(a) \propto a^{-1}$. To determine the magnitude of the velocity kicks at an initial redshift $z_i$ ([scale factor](@entry_id:157673) $a_i = (1+z_i)^{-1}$), one must compute the root-mean-square (rms) velocity, $v_{\mathrm{rms}}(a_i) = \sqrt{\langle v^2 \rangle}$, by averaging over the Fermi-Dirac distribution at that epoch. The calculation, which involves Fermi-Dirac integrals, shows that the rms velocity scales inversely with the scale factor and particle mass :

$v_{\mathrm{rms}}(a_i) \propto \frac{1}{m_{\chi} a_i}$

This scaling shows that the required [peculiar velocity](@entry_id:157964) kicks are largest at high initial redshifts. In practice, for each particle, three velocity components are drawn from the full momentum distribution (often approximated by a Maxwell-Boltzmann distribution for simplicity, though this is not strictly correct ) and then added to the peculiar velocity derived from linear theory for the large-scale density field.

#### Particle Evolution and Numerical Considerations

The N-body simulation evolves particles according to the discretized equations of motion, which are the characteristics of the Vlasov equation. The first-order system for the comoving position $\mathbf{x}$ and peculiar velocity $\mathbf{v}$ is :

$\frac{d\mathbf{x}}{dt} = \frac{\mathbf{v}}{a}$

$\frac{d\mathbf{v}}{dt} = -\nabla_{\mathbf{x}}\phi - \frac{\dot{a}}{a}\mathbf{v}$

Standard integration schemes like the leapfrog method are used to evolve this system. However, the large initial thermal velocities of WDM particles introduce a significant numerical challenge. Standard timestep criteria in N-body codes are often based on particle accelerations. For WDM, especially at early times, particles can travel a significant [comoving distance](@entry_id:158059) in a single step due to their large peculiar velocities, even in regions of low acceleration. This can lead to integration errors and incorrect orbit calculations.

To prevent this, a **streaming-based timestep criterion** must be imposed. This criterion ensures that a particle does not travel more than a small fraction $\eta$ of the force resolution scale $L_{\mathrm{force}}$ in a single timestep $\Delta t$. From the [equation of motion](@entry_id:264286) for $\mathbf{x}$, the comoving displacement is $\Delta\mathbf{x} \approx (\mathbf{v}/a)\Delta t$. To be conservative, we use the maximum velocity in the simulation, $v_{\max}$, leading to the bound :

$\Delta t \le \eta \frac{a L_{\mathrm{force}}}{v_{\max}}$

Since peculiar velocities redshift as $v_{\max}(a) \propto a^{-1}$, this timestep constraint scales as $\Delta t \propto a^2$. This means the timestep must be quadratically smaller at higher redshifts, making the early stages of WDM simulations computationally demanding.

### Interpreting Simulation Results: The Challenge of Numerical Artifacts

A defining feature of WDM cosmology is the absence of small primordial halos. However, N-body simulations of WDM robustly produce a population of small-mass halos, many of which are purely numerical artifacts. Understanding the origin of these spurious structures is critical for correctly interpreting simulation results.

The source of these artifacts lies in the interplay between the physical properties of WDM and the discrete nature of N-body simulations. Any simulation using a finite number of particles $N$ to represent a continuous density field inherently introduces **[shot noise](@entry_id:140025)**. For a Poisson sampling of particles with mean number density $\bar{n} = N/V$, this manifests as a white-noise [power spectrum](@entry_id:159996) with amplitude :

$P_{\mathrm{sn}} = \frac{1}{\bar{n}} = \frac{L^3}{N}$

In WDM, where the physical power spectrum is truncated above the [free-streaming](@entry_id:159506) scale $k_{\mathrm{fs}}$, this numerical shot noise can dominate the total power spectrum at small scales.

Gravitational collapse in the early universe is highly anisotropic, forming sheet-like structures (Zel'dovich pancakes) which then collapse into dense filaments. Along these filaments, the physical WDM power spectrum has been erased by [free-streaming](@entry_id:159506). However, the filament is still composed of discrete particles, and their random positions constitute shot noise. This numerical noise provides artificial seeds for [gravitational instability](@entry_id:160721) along the one-dimensional filament. The filament then fragments into a series of regularly spaced clumps, a phenomenon often described as "[beads-on-a-string](@entry_id:261179)". These are **[spurious halos](@entry_id:755257)** .

We can estimate the characteristic properties of these [spurious halos](@entry_id:755257). Their formation is seeded by particle noise, so their typical comoving spacing along a filament is set by the mean inter-particle separation, $d = \bar{n}^{-1/3}$. The mass of each spurious clump can be estimated as the mass contained in a segment of the filament. The volume of such a segment is its length ($\sim d$) multiplied by the filament's cross-sectional area, which is set by the physical [free-streaming](@entry_id:159506) scale ($\sim k_{\mathrm{fs}}^{-2}$). Therefore, the characteristic mass of a spurious halo, $M_{\mathrm{spur}}$, scales as :

$M_{\mathrm{spur}} \propto \bar{\rho} \cdot (\text{Area}) \cdot (\text{Length}) \propto \bar{\rho} \, k_{\mathrm{fs}}^{-2} \, d$

This scaling reveals the numerical origin of these halos: their mass depends directly on the inter-particle separation $d$. Increasing the simulation's [mass resolution](@entry_id:197946) (more particles $N$, smaller $d$) reduces the mass of individual [spurious halos](@entry_id:755257), a clear signature that they are not physical. Identifying and distinguishing these artifacts from potentially real, low-mass WDM halos is one of the foremost challenges in the field of [numerical cosmology](@entry_id:752779).