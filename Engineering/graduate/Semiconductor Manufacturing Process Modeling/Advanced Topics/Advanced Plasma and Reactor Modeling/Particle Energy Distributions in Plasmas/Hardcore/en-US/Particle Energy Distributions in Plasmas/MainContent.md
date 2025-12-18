## Introduction
To truly master modern [plasma processing](@entry_id:185745), one must look beyond macroscopic properties like temperature and density and delve into the kinetic behavior of the individual particles. Particle energy distributions, which describe how energy is partitioned among the electrons and ions, are the fundamental link between the external parameters of a plasma reactor and the atomic-scale outcomes on a semiconductor wafer. Understanding these distributions is crucial for controlling complex processes such as anisotropic etching and [thin-film deposition](@entry_id:1133096) with precision. This article addresses the need for a kinetic-level understanding by providing a comprehensive overview of particle energy distributions in plasmas.

This article will guide you through the core concepts, applications, and practical analysis of energy distributions. The first chapter, **Principles and Mechanisms**, lays the theoretical foundation, explaining what energy distribution functions are, why they often deviate from simple [equilibrium models](@entry_id:636099), and the physical mechanisms that govern their shape. Following this, the **Applications and Interdisciplinary Connections** chapter demonstrates how this theoretical knowledge is put into practice, covering experimental diagnostics, computational modeling, and advanced process control, while also highlighting connections to fields like nuclear fusion and astrophysics. Finally, the **Hands-On Practices** chapter provides targeted problems to solidify your understanding of key phenomena like collisional effects and thermal broadening in shaping ion energy distributions.

## Principles and Mechanisms

The behavior of a processing plasma is fundamentally governed by the collective motion of its constituent particles. While fluid models provide a macroscopic overview, a deeper understanding requires a kinetic description that resolves the distribution of particle velocities or energies. This chapter delves into the principles that determine these distributions and the physical mechanisms that shape them, focusing on the electron and ion populations that are central to semiconductor manufacturing processes.

### Fundamental Concepts: Describing Particle Ensembles

In [plasma kinetic theory](@entry_id:1129794), we describe a population of particles not by tracking each one individually, but by using a **distribution function**. This function quantifies the density of particles in a six-dimensional phase space of position and velocity. For a spatially uniform plasma, we can focus on the distribution in [velocity space](@entry_id:181216).

The most fundamental of these is the **[velocity distribution function](@entry_id:201683)**, $f_{\mathrm{v}}(\mathbf{v})$, which describes how particles are distributed among different velocities $\mathbf{v}$. Its primary definition is that its integral over all of [velocity space](@entry_id:181216) yields the total number density of the particle species. For electrons, with [number density](@entry_id:268986) $n_e$, this is:
$$
n_e = \int f_{\mathrm{v}}(\mathbf{v}) \, d^3v
$$
This normalization implies that $f_{\mathrm{v}}(\mathbf{v})$ has units of [number density](@entry_id:268986) per unit volume of velocity space (e.g., $\mathrm{s}^3 \mathrm{m}^{-6}$). The full, vector-dependent EVDF is essential for modeling phenomena where directionality is critical, such as transport in magnetic fields or interactions with anisotropic sheath fields .

In many low-temperature plasmas, collisions are frequent enough to randomize the direction of electron velocities faster than other [characteristic timescales](@entry_id:1122280). In such **isotropic** plasmas, the velocity distribution depends only on the magnitude of the velocity, or speed $v = |\mathbf{v}|$. This simplification allows us to transition from [velocity space](@entry_id:181216) to energy space, which is often more convenient for analyzing energy-dependent collision processes. The kinetic energy of an electron (mass $m_e$) is given by the non-relativistic formula $\varepsilon = \frac{1}{2} m_e v^2$.

The **Electron Energy Distribution Function (EEDF)**, denoted $f_{\mathrm{E}}(\varepsilon)$, is defined such that its integral over all possible energies also gives the electron [number density](@entry_id:268986):
$$
n_e = \int_0^\infty f_{\mathrm{E}}(\varepsilon) \, d\varepsilon
$$
The EEDF and the isotropic EVDF are related through a [change of variables](@entry_id:141386). The number of electrons in a spherical shell of speeds $[v, v+dv]$ must equal the number of electrons in the corresponding energy range $[\varepsilon, \varepsilon+d\varepsilon]$. This conservation principle leads to the relation:
$$
f_{\mathrm{E}}(\varepsilon) d\varepsilon = 4\pi v^2 f_{\mathrm{v}}(v) dv
$$
where the $4\pi v^2$ term is the volume of the spherical shell in [velocity space](@entry_id:181216). Solving for $f_{\mathrm{E}}(\varepsilon)$ and including the Jacobian of the transformation, $\frac{dv}{d\varepsilon} = (m_e v)^{-1}$, we get:
$$
f_{\mathrm{E}}(\varepsilon) = 4\pi v^2 f_{\mathrm{v}}(v) \frac{dv}{d\varepsilon} = \frac{4\pi \sqrt{2}}{m_e^{3/2}} \sqrt{\varepsilon} \, f_{\mathrm{v}}(v(\varepsilon))
$$
The factor of $\sqrt{\varepsilon}$ that universally appears in energy distributions originates from the three-dimensional nature of [velocity space](@entry_id:181216); it represents the density of states in energy .

For comparing the *shapes* of distributions or for use in certain calculations, it is often useful to work with a normalized probability distribution. The **Electron Energy Probability Function (EEPF)**, $P(\varepsilon)$, is the EEDF normalized by the electron density, such that it integrates to unity:
$$
P(\varepsilon) = \frac{f_{\mathrm{E}}(\varepsilon)}{n_e}, \quad \text{with} \quad \int_0^\infty P(\varepsilon) \, d\varepsilon = 1
$$
It is crucial to distinguish between the EEDF, which is a number density distribution (units of $\mathrm{m}^{-3}\mathrm{J}^{-1}$), and the EEPF, which is a probability density function (units of $\mathrm{J}^{-1}$) .

The primary utility of these energy distributions lies in calculating macroscopic rates from microscopic data. For instance, the [rate coefficient](@entry_id:183300) $k$ for an electron-impact reaction with an energy-dependent cross-section $\sigma(\varepsilon)$ is the average of the product $\sigma v$ over the distribution:
$$
k = \langle \sigma v \rangle = \int_0^\infty \sigma(\varepsilon) v(\varepsilon) P(\varepsilon) \, d\varepsilon = \int_0^\infty \sigma(\varepsilon) \sqrt{\frac{2\varepsilon}{m_e}} P(\varepsilon) \, d\varepsilon
$$
This integral forms the bridge between the kinetic description of the plasma (the EEPF) and the plasma chemistry (the reaction rates) that determines the species concentrations and ultimately the process outcome  .

### Equilibrium and Non-Equilibrium Distributions

#### The Maxwellian Distribution

The benchmark for any particle energy distribution is the **Maxwell-Boltzmann distribution** (or simply **Maxwellian**), which describes a system in thermal equilibrium at a single temperature $T$. For a neutral gas at temperature $T_g$, the normalized energy distribution function can be derived from the well-known Maxwell-Boltzmann speed distribution. The result is:
$$
f_{\varepsilon}(\varepsilon) = \frac{2}{\sqrt{\pi}(k_B T_g)^{3/2}} \varepsilon^{1/2} \exp\left(-\frac{\varepsilon}{k_B T_g}\right)
$$
where $k_B$ is the Boltzmann constant. This distribution is characterized by a peak at $\varepsilon = k_B T_g / 2$ and an exponential decay at high energies. Its shape is a direct consequence of statistical mechanics in a system dominated by frequent, energy-conserving collisions. When this distribution is used to calculate a [reaction rate coefficient](@entry_id:1130643) for a process with a constant cross-section $\sigma_0$, the result simplifies to $k = \sigma_0 \langle v \rangle$, where $\langle v \rangle = \sqrt{8k_B T_g / (\pi m)}$ is the mean speed of the particles .

#### Departure from Equilibrium

While the Maxwellian distribution is a useful idealization, the electrons in low-pressure processing plasmas are rarely in thermal equilibrium. This is because the energy balance is governed by competing processes that do not lead to a single thermal state:
1.  **Heating**: Electrons are accelerated by external radio-frequency (RF) electric fields, gaining significant energy.
2.  **Collisions**: Electrons lose energy through collisions with neutral gas atoms. Crucially, **[inelastic collisions](@entry_id:137360)** (e.g., excitation, ionization) involve the loss of large, discrete quanta of energy, a process fundamentally different from the gradual energy exchange in a thermal system.
3.  **Transport**: In low-pressure environments, energetic electrons can travel large distances, carrying energy from one region (like an oscillating sheath) to another.

The result is an EEDF that can deviate significantly from a Maxwellian shape. For ions, the situation is even more dramatic. While they are created with near-thermal energies, they are accelerated across plasma sheaths by potential drops of tens to hundreds of volts, resulting in a highly directed, non-thermal [ion energy distribution](@entry_id:189418) at the wafer surface .

#### Common Non-Maxwellian Models

To describe these non-[equilibrium states](@entry_id:168134), several model distributions are used. The **Druyvesteyn distribution**, for example, arises in the specific case of an electron swarm in a DC electric field where the dominant collision process has a constant cross-section.

A more general and widely used model is the **kappa (or Lorentzian) distribution**. In its energy form, it is often written as:
$$
f_{\varepsilon}(\varepsilon) = A_{\kappa}\,\varepsilon^{1/2}\left(1+\frac{\varepsilon}{\kappa\,\theta}\right)^{-(\kappa+1)}
$$
Here, $\theta$ is an energy parameter related to the effective temperature, and the index $\kappa$ controls the shape of the distribution's high-energy tail. For finite $\kappa$, the distribution exhibits a power-law tail ($f_\varepsilon \propto \varepsilon^{-(\kappa+1/2)}$) rather than an exponential one, meaning it has a higher population of energetic ("suprathermal") electrons than a Maxwellian with the same average energy. This is a common feature in plasmas with [long-range interactions](@entry_id:140725) or intermittent acceleration mechanisms. In the limit that $\kappa \to \infty$, the power-law term converges to an exponential, and the [kappa distribution](@entry_id:197233) smoothly recovers the Maxwellian distribution:
$$
\lim_{\kappa\to\infty} \left(1+\frac{\varepsilon}{\kappa\,\theta}\right)^{-(\kappa+1)} = \exp\left(-\frac{\varepsilon}{\theta}\right)
$$
This makes the [kappa distribution](@entry_id:197233) a flexible tool for modeling systems that are "quasi-thermal" but possess an excess of high-energy particles .

### Mechanisms Shaping the Electron Energy Distribution (EEDF)

The precise shape of the EEDF is determined by the kinetic balance of all processes that supply and remove electrons from a given energy level. This balance is formally described by the **Boltzmann equation**.

For a spatially uniform plasma, the Boltzmann equation for the EVDF $f(\mathbf{v},t)$ is:
$$
\frac{\partial f}{\partial t} + \frac{q}{m}\mathbf{E}(t)\cdot \nabla_{\mathbf{v}} f = \mathcal{C}[f]
$$
where the term with the electric field $\mathbf{E}(t)$ represents acceleration in velocity space, and $\mathcal{C}[f]$ is the [collision operator](@entry_id:189499), encapsulating all collisional processes.

A powerful method for solving this equation in weakly anisotropic plasmas is the **two-term [spherical harmonic expansion](@entry_id:188485)**, where the EVDF is approximated as $f(\mathbf{v},t) \approx f_0(\varepsilon, t) + f_1(\varepsilon, t) \cos\theta$. Here, $f_0$ is the dominant isotropic part, $f_1$ is a small anisotropic perturbation ($|f_1| \ll f_0$), and $\theta$ is the angle between the velocity and the electric field. This approximation reduces the single complex integro-differential equation into a coupled pair of simpler equations for $f_0$ and $f_1$ .

After averaging over an RF cycle, the steady-state equation for the isotropic EEDF $f_0(\varepsilon)$ takes on a form that highlights the physical mechanisms at play. The equation can be written as a balance of fluxes in energy space:
$$
\frac{\partial}{\partial \varepsilon} \left( J_{field} + J_{coll} \right) + S_{inel} = 0
$$
Here, $J_{field}$ is the [energy flux](@entry_id:266056) from RF heating, $J_{coll}$ is the flux from elastic collisions, and $S_{inel}$ represents [sources and sinks](@entry_id:263105) from [inelastic collisions](@entry_id:137360).

For a sinusoidal RF field $E(t)$, the heating process is stochastic. An electron is accelerated by the field, and a subsequent [elastic collision](@entry_id:170575) with a heavy neutral atom randomizes its direction, converting the directed motion into random thermal energy. This process, averaged over many cycles and collisions, acts as a **diffusion in energy space**. The RF heating term in the equation for $f_0$ takes a Fokker-Planck form, characterized by a heating (or energy diffusion) coefficient $D_\varepsilon(\varepsilon)$ that is proportional to the square of the electric field strength ($E_{rms}^2$) and to a factor that depends on the interplay between the momentum-transfer collision frequency $\nu_m(\varepsilon)$ and the RF [angular frequency](@entry_id:274516) $\omega$:
$$
D_\varepsilon(\varepsilon) \propto E_{rms}^2 \frac{\nu_m(\varepsilon)}{\nu_m^2(\varepsilon) + \omega^2} v^2(\varepsilon)
$$
This term shows that heating is most efficient when $\omega \approx \nu_m$, but in many low-pressure plasmas, $\omega \gg \nu_m$, and the heating is proportional to $\nu_m$.

The [collision operator](@entry_id:189499) $\mathcal{C}[f]$ is separated into its constituent parts. **Elastic collisions** with heavy neutrals result in very little energy loss per event and primarily contribute to the randomization of velocity, which is already captured in the diffusive heating term. **Inelastic collisions** are non-local in energy space; they act as a sink of electrons at energy $\varepsilon$ and a source at a lower energy $\varepsilon - \varepsilon_{th}$, where $\varepsilon_{th}$ is the reaction threshold. **Electron-electron (Coulomb) collisions**, with frequency $\nu_{ee}$, are a special case. They efficiently redistribute energy among the electron population, strongly driving the EEDF towards a Maxwellian shape. The frequency of these collisions scales as $\nu_{ee} \propto n_e / \varepsilon^{3/2}$, meaning they are most influential at high electron densities and low electron energies  .

The final shape of the EEDF is a result of the competition between these mechanisms. For example, a hybrid distribution with a **Druyvesteyn-like core and a Maxwellian tail** can form under specific conditions. In a regime of intermediate electron density, electron-neutral collisions may dominate at low energies ($\nu_m \gg \nu_{ee}$), where the RF heating and collisional dynamics produce a distribution depleted of low-energy electrons compared to a Maxwellian. At higher energies, the electron-neutral collision frequency may decrease while the electron density is still high enough for Coulomb collisions to become dominant ($\nu_{ee} \gtrsim \nu_m$). In this energy window, electron-electron collisions will thermalize the distribution, producing a Maxwellian tail. This tail is ultimately cut off at even higher energies by the onset of high-threshold [inelastic collisions](@entry_id:137360) .

#### Nonlocal Effects

The Boltzmann formalism just described assumes the EEDF at a given point is determined by the [local electric field](@entry_id:194304) ($E/N$). This **local-field approximation** breaks down when the distance an electron travels before its energy is randomized, the [energy relaxation](@entry_id:136820) length $\lambda_\varepsilon$, is comparable to or larger than the plasma dimensions $L$. This is common in low-pressure CCPs, where the [electron mean free path](@entry_id:185806) can exceed the electrode gap. In this **nonlocal regime**, an electron's energy is not a function of the local field, but of the integrated work done by the field over its entire trajectory, which may span the entire plasma volume. The transport term $\mathbf{v}\cdot\nabla_{\mathbf{r}} f$ in the Boltzmann equation becomes crucial. To correctly compute the EEDF, one must adopt a nonlocal approach, for example, by tracking electron trajectories from their source (typically the expanding sheaths) and accounting for their energy gain and collisional losses as they transit across the plasma .

### Mechanisms Shaping the Ion Energy Distribution (IEDF) at Surfaces

While the EEDF governs the plasma's ability to create ions and reactive species, the **Ion Energy Distribution Function (IEDF)** at the wafer surface is what dictates the energy of [ion bombardment](@entry_id:196044), a critical parameter for anisotropic etching and [surface modification](@entry_id:273724). The IEDF is almost entirely shaped by the **plasma sheath**.

Ions are typically formed in the bulk plasma with low, near-thermal energies. To enter the sheath, they must be accelerated in the presheath to satisfy the **Bohm criterion**, which requires they attain a minimum directed speed, classically $u_n \ge \sqrt{k_B T_e / m_i}$, for a stable sheath to form. Once in the sheath, their fate depends on the competition between acceleration by the strong sheath electric field and collisions with background neutrals.

#### The Collisionless Sheath

In low-pressure plasmas, it is common for the ion-neutral mean free path, $\lambda_i$, to be larger than the sheath thickness, $s$. For example, in a 5 mTorr argon plasma, $\lambda_i$ can be several millimeters, exceeding a typical sheath thickness of ~1 mm . Under this **collisionless** condition ($s / \lambda_i \ll 1$), an ion traverses the sheath without interruption. It is accelerated by the full potential drop of the sheath, $V_s$. If an ion enters the sheath with a small initial energy, it will arrive at the wafer with a kinetic energy $E \approx e V_s$. The resulting IEDF is a single, sharp peak centered at this energy.

The time-varying nature of the sheath in RF plasmas adds a crucial dynamic. The ion transit time across the sheath, $\tau_{ion}$, must be compared to the RF period, $\tau_{RF}$.
*   If $\tau_{ion} \gg \tau_{RF}$ (low frequency, heavy ions), the ion effectively experiences the time-averaged sheath potential, leading to a single, narrow IEDF peak.
*   If $\tau_{ion} \ll \tau_{RF}$ (high frequency, light ions), the ion crosses the sheath so quickly it experiences an almost instantaneous snapshot of the sheath potential. The IEDF would reflect the distribution of sheath potentials over the RF cycle.
*   If $\tau_{ion} \sim \tau_{RF}$, which is common for typical ions like $\text{Ar}^+$ in 13.56 MHz plasmas, the ion's final energy depends on the phase of the RF field as it transits. Ions that cross during the more negative part of the cycle gain more energy than those that cross during the less negative part. This phase-dependent acceleration splits the IEDF peak into a characteristic **bimodal (two-peaked) structure** .

#### The Collisional Sheath

At higher pressures, the ion mean free path becomes shorter than the sheath thickness. The sheath becomes **collisional**, a regime defined by an ion Knudsen number $K_n = \lambda_i / s \lesssim 1$ . The dominant ion-neutral collision process in noble gas plasmas is typically **[charge exchange](@entry_id:186361) (CX)**. In a CX collision, a fast ion collides with a slow neutral atom, transferring its charge:
$$
\text{Ion}_{\text{fast}}^+ + \text{Neutral}_{\text{slow}} \rightarrow \text{Neutral}_{\text{fast}} + \text{Ion}_{\text{slow}}^+
$$
This event has two consequences for the IEDF. First, the original fast ion is lost from the ion population bombarding the electrode. Second, a new, slow ion is created at the collision location *inside* the sheath. This new ion then begins to accelerate towards the wafer, but only through the *remaining* potential drop.

Ions created near the plasma-sheath edge will be accelerated by nearly the full potential $V_s$, contributing to the high-energy peak in the IEDF. However, ions created by CX collisions deep within the sheath, close to the wafer, will gain very little energy. The superposition of ions created at all positions throughout the sheath results in a broad, [continuous distribution](@entry_id:261698) of energies below the main peak. This forms a significant **low-energy tail** in the IEDF. Under the simplifying assumption of a [uniform electric field](@entry_id:264305) and uniformly distributed collision events, this tail takes the shape of a flat, box-like distribution extending from zero energy up to $e V_s$ .

### Advanced Topics and Generalizations

#### Energy Distributions of Other Species: Negative Ions

In electronegative plasmas used for dielectric etching, **negative ions** are an important species. Their behavior is starkly different from positive ions. Because they carry a negative charge, they are repelled by the negative potential of the wafer and are largely confined to the plasma bulk. Their mass is comparable to that of positive ions, so they exchange energy efficiently with the background neutral gas, typically remaining thermalized at the gas temperature $T_g$. They can only reach the wafer during the brief phase of the RF cycle when the oscillating sheath potential collapses or even becomes positive. Due to their large mass and the short duration of this escape window, they gain very little energy from the sheath fields. Consequently, the energy distribution of negative ions striking the wafer is typically narrow and near-thermal, peaked at an energy close to $k_B T_g$ .

#### Anisotropy and Magnetic Fields

The presence of a [static magnetic field](@entry_id:924015) introduces a preferred direction in the plasma, rendering the particle distributions anisotropic. A common model for this is the **bi-Maxwellian distribution**, which assigns different temperatures to motion parallel ($T_{e,\parallel}$) and perpendicular ($T_{e,\perp}$) to the magnetic field lines $\mathbf{B}$ .

This anisotropy fundamentally changes the concept of pressure. Instead of a scalar pressure, the plasma exerts a **pressure tensor**, $\mathbf{P}_e$. For a gyrotropic distribution (one that is symmetric around the magnetic field lines), this tensor can be written as:
$$
\mathbf{P}_{e} = p_{\parallel}\mathbf{b}\mathbf{b} + p_{\perp}(\mathbf{I} - \mathbf{b}\mathbf{b})
$$
where $\mathbf{b}$ is the [unit vector](@entry_id:150575) along $\mathbf{B}$, $\mathbf{I}$ is the identity tensor, and $p_{\parallel} = n_e k_B T_{e,\parallel}$ and $p_{\perp} = n_e k_B T_{e,\perp}$ are the parallel and perpendicular pressures.

This tensorial pressure has direct physical consequences. For instance, the Bohm criterion for sheath formation must be re-evaluated. If the magnetic field is oriented at an angle $\theta$ to the wall normal, the electron pressure force resisting plasma compression depends on a geometric projection of both pressure components. The minimum ion speed required for a stable sheath to form is then given by a generalized Bohm criterion:
$$
u_{n} \ge \sqrt{\frac{k_{B} (T_{e,\parallel} \cos^2\theta + T_{e,\perp} \sin^2\theta)}{m_{i}}}
$$
This result demonstrates how fundamental principles like sheath stability are adapted in more complex, magnetized environments, with the ion dynamics at the sheath edge being directly coupled to the anisotropic nature of the electron energy distribution in the bulk .