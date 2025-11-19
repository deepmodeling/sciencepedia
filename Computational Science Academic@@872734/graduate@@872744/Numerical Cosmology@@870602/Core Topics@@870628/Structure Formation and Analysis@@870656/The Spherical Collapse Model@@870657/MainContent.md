## Introduction
The emergence of vast cosmic structures like galaxies and galaxy clusters from the near-uniformity of the early universe is a cornerstone of modern cosmology. While large-scale numerical simulations are essential for capturing the full complexity of this process, a simpler, more intuitive analytical framework is needed to understand the fundamental physics of [gravitational instability](@entry_id:160721). The [spherical collapse model](@entry_id:159843) provides exactly this: a powerful, albeit idealized, tool for tracing the non-linear growth of a single density perturbation into a collapsed, gravitationally bound object.

This article provides a comprehensive exploration of this foundational model. The first chapter, "Principles and Mechanisms," will derive the dynamical equations governing the collapse and explain its two cornerstone predictions: the [critical density](@entry_id:162027) for collapse and the final virial density. The second chapter, "Applications and Interdisciplinary Connections," will demonstrate how this simple model is applied to predict the abundance and clustering of halos, and how it can be extended to test new theories of dark matter and gravity. Finally, the "Hands-On Practices" section offers opportunities to apply these concepts by building numerical solvers. We begin by dissecting the core principles and dynamical equations that define the [spherical collapse model](@entry_id:159843).

## Principles and Mechanisms

The [spherical collapse model](@entry_id:159843) provides a simplified yet remarkably insightful framework for understanding the formation of gravitationally bound structures in an expanding universe. By idealizing an initial density perturbation as a spherically symmetric "top-hat" overdensity, the model allows for an exact, non-linear calculation of its evolution, from early expansion to eventual collapse and [virialization](@entry_id:161222). This chapter elucidates the core principles and dynamical mechanisms of this model.

### The Idealized System: Lagrangian and Eulerian Views

The foundational element of the model is a **spherical top-hat perturbation**: a spherical region of space with an initially uniform matter density, $\rho_p(t)$, embedded in a homogeneous and isotropic background universe with mean matter density $\bar{\rho}_m(t)$. At any given time $t$, the region is characterized by a physical radius, which we denote as $R(t)$.

To track the motion of matter, it is essential to distinguish between three coordinate systems [@problem_id:3498611]:

1.  The **physical radius**, $R(t)$, is the standard Euclidean radius of a given mass shell at cosmic time $t$. Its dynamics are governed by local physics.

2.  The **comoving Eulerian radius**, $x(t)$, is the physical radius scaled by the [cosmic scale factor](@entry_id:161850) $a(t)$, defined as $x(t) \equiv R(t)/a(t)$. It measures the radius of the shell in the coordinate system that expands with the background universe. A shell that perfectly follows the Hubble expansion has a constant comoving radius.

3.  The **Lagrangian radius**, $r$, is a time-independent label assigned to each mass shell. It is defined as the comoving radius the shell *would* have if its enclosed mass $M$ were distributed at the mean comoving matter density of the universe, $\bar{\rho}_{m,0}$ (defined at $a=1$). This definition stems from the principle of [mass conservation](@entry_id:204015) for a Lagrangian fluid element.

The total mass $M$ enclosed within a Lagrangian radius $r$ is, by definition, constant:
$$
M = \frac{4\pi}{3} \bar{\rho}_{m,0} r^3
$$
This relation provides the fundamental mapping between the mass of a perturbation and its initial Lagrangian scale [@problem_id:3498647]. At any time $t$, this same mass is contained within the physical radius $R(t)$ at the interior density $\rho_p(t) = \bar{\rho}_m(t)[1+\delta(t)]$, where $\delta(t)$ is the non-linear Eulerian [density contrast](@entry_id:157948). Recalling that $\bar{\rho}_m(t) = \bar{\rho}_{m,0}a(t)^{-3}$ and $R(t) = a(t)x(t)$, [mass conservation](@entry_id:204015) gives:
$$
M = \frac{4\pi}{3} R(t)^3 \rho_p(t) = \frac{4\pi}{3} [a(t)x(t)]^3 \left(\bar{\rho}_{m,0}a(t)^{-3} [1+\delta(t)]\right) = \frac{4\pi}{3} \bar{\rho}_{m,0} x(t)^3 [1+\delta(t)]
$$
Equating the two expressions for $M$ yields a crucial relationship between the Lagrangian radius, the comoving Eulerian radius, and the [density contrast](@entry_id:157948):
$$
r^3 = x(t)^3 [1+\delta(t)]
$$
This equation shows that for an overdense region ($\delta > 0$), its comoving radius $x(t)$ must be smaller than its Lagrangian radius $r$. As the perturbation collapses and $\delta$ grows, $x(t)$ must shrink accordingly.

### Cosmological Background and Dynamics

The spherical perturbation evolves within a background universe described by the Friedmann–Lemaître–Robertson–Walker (FLRW) metric. The expansion of this background is governed by the Friedmann equation. In its most general form, including contributions from matter ($\Omega_{m,0}$), radiation ($\Omega_{r,0}$), a [cosmological constant](@entry_id:159297) ($\Omega_{\Lambda,0}$), and [spatial curvature](@entry_id:755140) ($\Omega_{k,0}$), the Hubble parameter $H(a) \equiv \dot{a}/a$ evolves as [@problem_id:3498594]:
$$
H^2(a) = H_0^2 \left[ \Omega_{m,0}a^{-3} + \Omega_{r,0}a^{-4} + \Omega_{\Lambda,0} + \Omega_{k,0}a^{-2} \right]
$$
For the study of galaxy and cluster formation, which primarily occurs at redshifts $z \lesssim 100$, we can make a significant simplification. Given that the radiation-to-matter density ratio today is small, $\Omega_{r,0}/\Omega_{m,0} \sim 3 \times 10^{-4}$, radiation dominates only at very high redshifts ($z \gtrsim 3400$) and is negligible during the epoch of halo formation. Furthermore, observations indicate the universe is very nearly spatially flat, $|\Omega_{k,0}| \ll 1$. The curvature term's contribution relative to matter scales as $a$, so it is subdominant at all times $a \le 1$. Therefore, for practical purposes, the background evolution can be accurately described by a flat, matter- and cosmological-constant-dominated model:
$$
H^2(a) \approx H_0^2 \left[ \Omega_{m,0}a^{-3} + \Omega_{\Lambda,0} \right]
$$

Within this background, the dynamics of a mass shell at physical radius $R(t)$ are governed by Newton's second law, including the gravitational pull of the enclosed mass $M$ and the repulsive force from the [cosmological constant](@entry_id:159297) $\Lambda$. By Birkhoff's theorem, the external mass distribution has no effect. The equation of motion is [@problem_id:3498611]:
$$
\ddot{R}(t) = -\frac{G M}{R(t)^2} + \frac{\Lambda c^2}{3}R(t)
$$
where $\Lambda$ is the [cosmological constant](@entry_id:159297), related to the [density parameter](@entry_id:265044) via $\Omega_{\Lambda,0} = \Lambda c^2 / (3 H_0^2)$.

A key feature of the top-hat model is that an initially uniform sphere remains uniform prior to shell-crossing. This arises because the [net force](@entry_id:163825) on a particle at radius $R$ is proportional to $R$. The self-gravity term becomes $-\frac{G}{R^2}(\frac{4\pi}{3} R^3 \rho_p) = -(\frac{4\pi G \rho_p}{3})R$, and the [cosmological constant](@entry_id:159297) term is $(\frac{\Lambda c^2}{3})R$. Since the total acceleration $\ddot{R}$ is linear in $R$, all shells evolve homologously, maintaining the uniformity of the density profile [@problem_id:3498598]. The cosmological constant term, being linear in $R$, does not spoil this property [@problem_id:3498598].

To better understand the dynamics relative to the background expansion, we transform the [equation of motion](@entry_id:264286) to the comoving radius $x(t) = R(t)/a(t)$. Differentiating $R(t) = a(t)x(t)$ twice and substituting into the equation for $\ddot{R}$, then using the background acceleration equation, one can derive the [equation of motion](@entry_id:264286) for the peculiar motion of the shell [@problem_id:3498611]:
$$
\ddot{x}(t) + 2H(t)\dot{x}(t) = -\frac{4\pi G}{3} \bar{\rho}_m(t) \delta(t) x(t)
$$
This equation beautifully separates the different physical effects. The term $2H(t)\dot{x}(t)$ is a **Hubble drag** or friction term, which damps peculiar velocities in an [expanding universe](@entry_id:161442). The right-hand side represents the **peculiar gravitational acceleration**—the extra gravitational pull generated by the local overdensity $\delta(t)$ relative to the background. This equation is the central dynamical equation for the evolution of the perturbation.

### Initial Conditions from Linear Theory

To solve the evolution, we must specify [initial conditions](@entry_id:152863). These are set at a very early time, $t_i$, when the perturbation is still small ($|\delta_i| \ll 1$) and can be described by linear theory. In the standard cosmological paradigm, structure arises from the gravitational amplification of initial [primordial fluctuations](@entry_id:158466) generated during inflation. These are typically assumed to be adiabatic, growing-mode perturbations.

A crucial task is to connect the relativistic description of [primordial fluctuations](@entry_id:158466) to the Newtonian quantities $\delta$ and $\vec{v}$ of the [spherical collapse model](@entry_id:159843). This must be done in a gauge-invariant manner to avoid spurious artifacts. The standard procedure begins with the conserved, gauge-invariant **[comoving curvature perturbation](@entry_id:161457)**, $\zeta$, which is the primary output of inflation. For a [matter-dominated era](@entry_id:272362), this is related to the Newtonian gravitational potential $\Phi$ by $\Phi = -\frac{3}{5}\zeta$. The potential, in turn, is related to the gauge-[invariant density](@entry_id:203392) contrast $\Delta$ via the relativistic Poisson equation. Finally, the initial overdensity for the top-hat, $\delta_i$, is obtained by averaging $\Delta$ over the spherical volume [@problem_id:3498658].

This procedure also sets the [initial velocity](@entry_id:171759). A pure growing-mode perturbation has a specific relationship between its density and velocity fields. For a small initial Lagrangian overdensity $\delta_i$ at [scale factor](@entry_id:157673) $a_i$, this corresponds to setting the initial conditions for the normalized physical radius, $y(a) \equiv R(a)/(a R_i)$, where $R_i$ is the initial Lagrangian radius. To leading order, these are [@problem_id:3498651]:
$$
y(a_i) \approx 1 - \frac{\delta_i}{3}
$$
$$
\left.\frac{\mathrm{d} y}{\mathrm{d}\ln a}\right|_{a_i} \approx -\frac{\delta_i}{3}
$$
The first condition shows that an initial overdensity implies the shell is already smaller than its unperturbed counterpart. The second condition ensures the shell has an initial inward peculiar velocity relative to the Hubble flow, consistent with a pure growing mode in a [matter-dominated universe](@entry_id:158254) where the growth rate $f(a) \equiv d\ln D/ d\ln a \approx 1$.

### Evolution, Turnaround, and Collapse

With the [equation of motion](@entry_id:264286) and initial conditions established, we can solve for the evolution of the shell. For simplicity, let's first consider a flat, matter-only background (the Einstein-de Sitter, or EdS, model), where $\Omega_m=1$ and $\Lambda=0$. In this case, the overdense region behaves exactly like a closed FRW universe, with its fate determined by its total energy. A perturbation is gravitationally bound and destined to collapse if its total energy (kinetic + potential) is negative [@problem_id:885732].

The evolution of the physical radius $R$ of the bound perturbation is described by a parametric [cycloid](@entry_id:172297) solution [@problem_id:813396] [@problem_id:3498668]:
$$
R(\theta) = A(1 - \cos\theta)
$$
$$
t(\theta) = B(\theta - \sin\theta)
$$
Here, $\theta$ is a "development angle," and the constants $A$ and $B$ are determined by the mass and initial energy of the perturbation, with the relation $M = A^3/(G B^2)$.

This solution traces the life of the perturbation:
-   **Initial Expansion ($\theta \to 0$)**: The perturbation expands along with the universe, but its expansion is slowed by its excess gravity.
-   **Turnaround ($\theta = \pi$)**: The expansion halts at a maximum radius, $R_{ta} = 2A$, at time $t_{ta} = \pi B$. At this moment, the kinetic energy of the shell is zero.
-   **Collapse ($\theta = 2\pi$)**: The shell collapses back to a point of formally infinite density at time $t_{coll} = 2t_{ta} = 2\pi B$.

For underdense regions ($\delta  0$), the perturbation behaves like an open universe and expands forever. Its evolution is described by an analogous hyperbolic solution [@problem_id:3498668].

### Key Predictions: Collapse Threshold and Virialization

The [spherical collapse model](@entry_id:159843) yields two foundational predictions that are cornerstones of modern cosmology.

#### The Critical Overdensity for Collapse ($\delta_c$)

While the top-hat follows its non-linear evolution, the corresponding initial perturbation in the background, if it had been small, would have continued to grow linearly. The **critical linear overdensity for collapse**, $\delta_c$, is defined as the value of this linearly-extrapolated overdensity at the time the non-linear model predicts complete collapse ($t_{coll}$).

In an EdS universe, linear perturbations grow as $\delta_{lin} \propto a(t) \propto t^{2/3}$. By relating the [linear growth](@entry_id:157553) to the exact collapse time $t_{coll}$ from the [cycloid](@entry_id:172297) solution, one finds a remarkable result: $\delta_c$ is a constant, independent of the mass of the perturbation or its collapse time. Its value is:
$$
\delta_c^{\mathrm{EdS}} = \frac{3}{20}(12\pi)^{2/3} \approx 1.686
$$
This value serves as the threshold for collapse in theories of structure formation like the Press-Schechter formalism.

In a $\Lambda$CDM universe, the cosmological constant affects both the non-linear collapse and the linear growth. The repulsive force from $\Lambda$ slows the non-linear collapse, meaning a larger initial perturbation is needed to collapse by a given [redshift](@entry_id:159945). Simultaneously, $\Lambda$ accelerates the background expansion, which suppresses the rate of [linear growth](@entry_id:157553). These two effects—the need for a larger seed and the smaller linear amplification—nearly cancel each other out. The result is that $\delta_c(z)$ in a $\Lambda$CDM universe has only a very weak dependence on redshift [@problem_id:3498634]. A highly accurate fitting formula is given by:
$$
\delta_c(z) \approx 1.686 \left[\Omega_m(z)\right]^{0.0055}
$$
For a typical cosmology ($\Omega_{m,0}=0.3$), $\delta_c$ varies from $\approx 1.685$ at $z=2$ to $\approx 1.674$ at $z=0$, a change of less than 1% [@problem_id:3498634]. This near-constancy is crucial for the success of simplified models of halo statistics.

#### The Virial Overdensity ($\Delta_{vir}$)

In reality, the collapsing perturbation does not form a singularity. Instead, processes like [violent relaxation](@entry_id:158546) cause the system to settle into a gravitationally bound, quasi-equilibrium state known as a **virialized halo**. The virial theorem relates the kinetic ($K$) and potential ($U$) energies of this final state. For a self-gravitating system, $2K + U = 0$.

By conserving energy from the moment of turnaround (where $K=0$ and the total energy is $E = U_{ta}$) to the final virialized state (where $E = K+U = U_{vir}/2$), we find that the radius of the virialized halo is half the turnaround radius: $R_{vir} = R_{ta}/2$ [@problem_id:813396].

With this result, we can calculate the final density of the halo, $\rho_{vir}$, relative to the background critical density at the time of [virialization](@entry_id:161222), $\rho_c(t_{vir})$. In an EdS universe, where $t_{vir} = t_{coll} = 2t_{ta}$, this overdensity contrast is:
$$
\Delta_{vir} = \frac{\rho_{vir}}{\rho_c(t_{vir})} = 18\pi^2 \approx 178
$$
This classic result provides a physical basis for defining the boundary of a dark matter halo. In a $\Lambda$CDM cosmology, the background evolution and the virial equilibrium condition are modified by the cosmological constant. The [virial overdensity](@entry_id:756504) becomes redshift-dependent. An accurate fitting formula, calibrated by numerical solutions, is given by Bryan  Norman (1998) [@problem_id:3490323]:
$$
\Delta_{\mathrm{vir}}(z) = 18\pi^2 + 82x - 39x^2, \quad \text{where} \quad x = \Omega_m(z) - 1
$$
At high [redshift](@entry_id:159945), $\Omega_m(z) \to 1$, and this formula correctly recovers the EdS value of $18\pi^2$. At $z=0$ in a [flat universe](@entry_id:183782) with $\Omega_{m,0}=0.3$, $\Delta_{vir}(0) \approx 101$.

### Domain of Validity and Limitations

The [spherical collapse model](@entry_id:159843), for all its power, relies on strong idealizations. Its validity breaks down when these assumptions are violated [@problem_id:3498598].
-   **Shell Crossing**: The fluid description fails when faster-moving outer shells overtake slower inner shells. In the idealized model, this occurs at the center at the moment of collapse, but imperfections can lead to earlier, off-center [shell crossing](@entry_id:754769).
-   **Anisotropy**: Real perturbations are not perfectly spherical. External tidal fields from neighboring structures exert anisotropic forces, deforming the collapsing region and invalidating the assumption of [spherical symmetry](@entry_id:272852).
-   **Pressure and Velocity Dispersion**: The model assumes a pressureless fluid (cold dark matter). If the collapsing matter has significant pressure (as in baryonic gas) or velocity dispersion, the resulting pressure-gradient forces will counteract gravity, altering the dynamics and potentially preventing collapse on small scales (Jeans stabilization).

Despite these limitations, the [spherical collapse model](@entry_id:159843) provides an indispensable conceptual and quantitative foundation for modern theories of [structure formation](@entry_id:158241). Its predictions for $\delta_c$ and $\Delta_{vir}$ are used ubiquitously in analytical models and in the interpretation of cosmological N-body simulations, where halos are often identified using a **Spherical Overdensity (SO)** criterion based on the virial [density contrast](@entry_id:157948). The choice of a real-space top-hat filter for smoothing the initial density field in the Press-Schechter formalism is directly motivated by its conceptual consistency with the spherical volume assumed by the collapse model [@problem_id:3498647].