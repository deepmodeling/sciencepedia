## Introduction
The thousands of exoplanetary systems discovered to date display a bewildering diversity in their architectures, from 'hot Jupiters' orbiting perilously close to their stars to compact systems of planets locked in resonant chains. These configurations are often profoundly different from our own solar system and pose a fundamental challenge to [planet formation](@entry_id:160513) theories. A critical piece of this puzzle lies in the dynamic interaction between a newly formed planet and the gaseous [protoplanetary disk](@entry_id:158060) from which it is born. This interplay governs a planet's early life, driving orbital migration that can transport it across vast distances and fundamentally sculpting the final structure of its planetary system. Understanding the physics of this interaction is therefore essential to bridging the gap between the initial stages of [planet formation](@entry_id:160513) and the observed architectures of mature systems.

This article provides a comprehensive guide to the principles and applications of modeling planet-disk interactions. Over the next three chapters, you will build a robust understanding of this complex process.
- **Principles and Mechanisms** will lay the theoretical groundwork, deriving the governing hydrodynamic equations and explaining the fundamental torque mechanisms—Lindblad and [corotation torques](@entry_id:747895)—that drive [planetary migration](@entry_id:158688).
- **Applications and Interdisciplinary Connections** will explore how these principles manifest in observable phenomena, such as the formation of gaps and vortices in disks, and how they shape the architecture of multi-planet systems.
- **Hands-On Practices** will offer the opportunity to apply these concepts through targeted computational exercises, building skills in simulating and analyzing these dynamic systems.

We begin by delving into the core physics, examining the set of equations and physical ingredients that form the foundation of modern [planet-disk interaction](@entry_id:157799) models.

## Principles and Mechanisms

The interaction between a newly formed planet and its natal [protoplanetary disk](@entry_id:158060) is a complex hydrodynamical problem that governs the planet's early orbital evolution and sculpts the structure of the disk itself. Understanding this interplay is fundamental to explaining the architecture of observed planetary systems, many of which bear the tell-tale signs of significant orbital migration. This chapter delineates the core physical principles and mathematical formalisms used to model planet-disk interactions, building from the governing equations of fluid dynamics to the emergent phenomena of [planetary migration](@entry_id:158688).

### The Governing Equations of a Planet-Disk System

The foundation for modeling a [protoplanetary disk](@entry_id:158060) is the set of conservation laws for mass, momentum, and energy. As these disks are typically geometrically thin, with a vertical [scale height](@entry_id:263754) $H$ much smaller than the radial distance from the central star $r$, it is often computationally advantageous to simplify the three-dimensional ($3$D) problem by integrating over the vertical direction. This results in a two-dimensional ($2$D) system described by surface quantities.

Let us consider the disk in the midplane, with [surface density](@entry_id:161889) $\Sigma(\boldsymbol{x},t)$ and a planar [velocity field](@entry_id:271461) $\boldsymbol{v}(\boldsymbol{x},t)$, where $\boldsymbol{x}$ is the position vector in the disk plane. The fundamental laws governing the evolution of these quantities are the vertically integrated continuity and momentum equations. In their [conservative form](@entry_id:747710), which is particularly well-suited for numerical methods that ensure conservation of physical quantities, these equations are expressed as follows [@problem_id:3520473]:

**Continuity Equation (Conservation of Mass):**
$$ \frac{\partial \Sigma}{\partial t} + \nabla \cdot (\Sigma \boldsymbol{v}) = 0 $$
This equation states that the local change in [surface density](@entry_id:161889) over time is balanced by the divergence of the mass flux, $\Sigma \boldsymbol{v}$.

**Momentum Equation (Conservation of Momentum):**
$$ \frac{\partial (\Sigma \boldsymbol{v})}{\partial t} + \nabla \cdot (\Sigma \boldsymbol{v} \boldsymbol{v} + P\mathbf{I} - \mathbf{T}) = -\Sigma \nabla \Phi $$
This is the fluid dynamics equivalent of Newton's second law. The term on the left, $\frac{\partial (\Sigma \boldsymbol{v})}{\partial t}$, represents the rate of change of momentum density. This change is driven by the terms on the right. The divergence term, $\nabla \cdot (\dots)$, accounts for the flux of momentum. This flux consists of three parts:
1.  **Advection of momentum**, $\Sigma \boldsymbol{v} \boldsymbol{v}$, which is the momentum carried along by the bulk flow of the fluid.
2.  **Pressure forces**, represented by the vertically integrated pressure $P$. The term $P\mathbf{I}$, where $\mathbf{I}$ is the identity tensor, describes an isotropic force that acts to compress or expand the fluid.
3.  **Viscous forces**, represented by the [viscous stress](@entry_id:261328) tensor $\mathbf{T}$, which describes [momentum transport](@entry_id:139628) due to internal friction within the fluid. The negative sign is a convention indicating that viscous stresses are subtracted from the total momentum flux.

The term on the far right, $-\Sigma \nabla \Phi$, represents the external [body force](@entry_id:184443) exerted on the fluid by gravity. The total gravitational potential $\Phi$ is the sum of contributions from the central star ($\Phi_\star$), the embedded planet ($\Phi_p$), and, if significant, the disk's own self-gravity ($\Phi_{\rm sg}$) [@problem_id:3520473].

### Essential Physical Ingredients and Closures

The governing equations are not a closed system on their own; they contain the quantities $P$ and $\mathbf{T}$, which must be related to the primary variables $\Sigma$ and $\boldsymbol{v}$. These relations are known as **closure relations** and encapsulate the physical assumptions made about the disk's thermodynamics and internal friction.

#### Thermodynamic Models and the Equation of State

The choice of a thermodynamic model determines the [equation of state](@entry_id:141675), which provides the closure for the pressure $P$. Three models are prevalent in planet-disk simulations [@problem_id:3520469].

1.  **Locally Isothermal Model:** This is the simplest model, assuming that any heat generated (e.g., by compression or viscosity) is radiated away instantaneously. The disk temperature $T$ is therefore not a dynamic variable but is a fixed, prescribed function of position, typically a power law of the radius $r$. The isothermal sound speed, $c_s = \sqrt{k_B T / \mu}$ (where $k_B$ is Boltzmann's constant and $\mu$ is the mean molecular weight), is also a prescribed function. The vertically integrated pressure is then directly related to the [surface density](@entry_id:161889) via the closure:
    $$ P = \Sigma c_s^2(r) $$
    In this model, only the continuity and momentum equations are evolved.

2.  **Adiabatic Model:** This model represents the opposite extreme, where no heat is exchanged with the surroundings. The gas evolves adiabatically, conserving its entropy in the absence of shocks. The pressure is related to the vertically integrated internal energy, $E$, via the ideal gas law for a given [adiabatic index](@entry_id:141800) $\gamma$:
    $$ P = (\gamma - 1)E $$
    In this case, the internal energy $E$ is a dynamic variable that changes due to work done by pressure forces (compressional heating) and [viscous dissipation](@entry_id:143708). An additional conservation equation for energy must be solved alongside the continuity and momentum equations.

3.  **Radiative Model:** A more physically realistic approach lies between the isothermal and adiabatic limits. Here, heating and cooling processes occur at finite rates. The pressure closure is still $P = (\gamma - 1)E$, but the energy equation is augmented with [source and sink](@entry_id:265703) terms representing [viscous heating](@entry_id:161646) and [radiative cooling](@entry_id:754014). More sophisticated models might explicitly evolve the radiation energy density, coupling it to the gas energy.

The choice of thermodynamics is critical, as it profoundly affects the disk's response to the planet, particularly in the co-orbital region where entropy gradients can drive powerful torques.

#### Viscosity and Turbulence Modeling

Protoplanetary disks are believed to be turbulent, primarily due to the **[magnetorotational instability](@entry_id:159446) (MRI)**. Direct numerical simulation of this MHD turbulence is computationally expensive. Therefore, in purely hydrodynamic models, the effect of turbulence is commonly parameterized as an effective viscosity. This is formalized within a **Reynolds-Averaged Navier-Stokes (RANS)** framework, where the velocity is decomposed into a mean flow and a fluctuating component. The correlations of these fluctuations give rise to a **Reynolds stress**, which acts to transport angular momentum, mimicking a [viscous stress](@entry_id:261328) [@problem_id:3520508].

The most widely used prescription for this effective viscosity is the **Shakura-Sunyaev $\alpha$-model**. It posits that the kinematic viscosity $\nu$ can be estimated from a mixing-length argument. The largest [turbulent eddies](@entry_id:266898) are assumed to have a size comparable to the smallest dimension of the system, the disk [scale height](@entry_id:263754) $H$, and velocities that are a fraction of the sound speed $c_s$ (to remain subsonic). This leads to the parameterization:
$$ \nu = \alpha c_s H $$
where $\alpha$ is a dimensionless efficiency parameter, typically assumed to be much less than $1$. The [viscous stress](@entry_id:261328) tensor $\mathbf{T}$ is then modeled as that of a compressible Newtonian fluid, where the stress is proportional to the [rate of strain](@entry_id:267998) of the fluid. The [dynamic viscosity](@entry_id:268228) is $\eta = \Sigma \nu$. For a 2D flow, the tensor components are:
$$ \mathbf{T}_{ij} = 2\eta \mathbf{S}_{ij} + \left(\zeta - \frac{2}{3}\eta\right)(\nabla \cdot \boldsymbol{v})\delta_{ij} $$
where $\mathbf{S}_{ij} = \frac{1}{2}(\partial_i v_j + \partial_j v_i)$ is the [rate-of-strain tensor](@entry_id:260652) and $\zeta$ is the [bulk viscosity](@entry_id:187773), often assumed to be zero (the Stokes hypothesis) [@problem_id:3520473]. The most important component for accretion is the shear stress, which in cylindrical coordinates for an [axisymmetric flow](@entry_id:268625) is $\tau_{r\phi} = \Sigma \nu r \frac{d\Omega}{dr}$ [@problem_id:3520508]. This viscous stress is the primary mechanism for [angular momentum transport](@entry_id:160167) and [mass accretion](@entry_id:163137) through the disk in the absence of a planet.

#### The Planetary Gravitational Potential

The planet's gravitational influence is the driving force of the entire interaction. In 3D, its potential is the standard Newtonian point-mass potential, $\Phi_p = -G M_p / |\boldsymbol{x} - \boldsymbol{x}_p|$. However, in 2D vertically integrated models, using this potential leads to a singularity that is both numerically problematic and physically inaccurate. The finite vertical thickness of the disk means that gas does not interact with a true [point mass](@entry_id:186768); the force is "smeared out" over the vertical [scale height](@entry_id:263754) $H$.

To mimic this 3D effect in 2D simulations, the planetary potential is regularized or "softened" [@problem_id:3520483]. A common choice is a Plummer-like potential:
$$ \Phi_p(\boldsymbol{r}) = -\frac{G M_p}{\sqrt{|\boldsymbol{r}-\boldsymbol{r}_p|^2 + \epsilon^2}} $$
where $\epsilon$ is the **[softening length](@entry_id:755011)**. The value of $\epsilon$ is not arbitrary. It is chosen to ensure that the force exerted by this 2D softened potential accurately approximates the true vertically-averaged 3D [gravitational force](@entry_id:175476). By comparing the acceleration from the softened potential, $a_{\text{soft}}$, with the vertically-averaged acceleration from the 3D potential, $a_{\text{3D,avg}}$, one can find an optimal value for $\epsilon$. This analysis shows that the best match, particularly at separations of order the [scale height](@entry_id:263754) ($s \sim H$) which are most important for launching density waves, is achieved when $\epsilon$ is a constant fraction of the local [scale height](@entry_id:263754) $H$. A widely adopted value is:
$$ \epsilon \approx 0.6 H(r) $$
This ensures that the representation of the planet's gravity correctly adapts to the local disk structure as it varies with radius [@problem_id:3520483].

### The Consequences: Torques and Angular Momentum Exchange

The [gravitational force](@entry_id:175476) from the planet perturbs the disk, creating non-axisymmetric structures such as spiral arms and density asymmetries in the co-orbital region. These structures exert a gravitational torque back on the planet. According to Newton's third law, the total torque on the planet, $\Gamma$, is the negative of the torque exerted by the planet on the disk.

This torque is the engine of [planetary migration](@entry_id:158688). The angular momentum of a planet in a circular Keplerian orbit is $L_p = M_p \sqrt{G M_\star a}$. The torque causes this to change over time, $\Gamma = dL_p/dt$, which leads to a change in the [semi-major axis](@entry_id:164167) $a$. This relationship provides the direct link between the torque and the migration rate, $\dot{a}$:
$$ \dot{a} = \frac{2\Gamma}{M_p a \Omega} $$
where $\Omega$ is the Keplerian orbital frequency at radius $a$ [@problem_id:3520527]. A negative torque ($\Gamma \lt 0$) leads to a loss of angular momentum and inward migration ($\dot{a} \lt 0$). A positive torque leads to outward migration. The net torque $\Gamma$ is the sum of two distinct contributions: Lindblad torques and [corotation torques](@entry_id:747895).

#### Lindblad Torques and Spiral Density Waves

A planet on a circular orbit stirs the disk at its orbital frequency, $\Omega_p$. Due to the [differential rotation](@entry_id:161059) of the disk, there are locations where the forcing frequency matches natural oscillation frequencies of the disk fluid. These locations are called **Lindblad resonances**. The planet excites [spiral density waves](@entry_id:161546) at these resonances, which then propagate away from the planet.

These waves carry angular momentum and energy. In a typical [protoplanetary disk](@entry_id:158060), the inner spiral arm (launched at the inner Lindblad resonance, inside the planet's orbit) carries negative angular momentum, while the outer spiral arm (launched at the outer Lindblad resonance) carries positive angular momentum. The reaction force on the planet is such that the inner disk exerts a positive torque, pulling it forward, and the outer disk exerts a negative torque, pulling it backward. For typical disk profiles, the outer torque is stronger, resulting in a net negative **Lindblad torque** that drives inward migration.

The angular momentum carried by a wave is described by the **wave angular [momentum flux](@entry_id:199796)**. As these waves propagate, they can steepen into weak shocks and dissipate their energy and angular momentum into the background disk, heating it and altering its rotation profile [@problem_id:3520538]. The local deposition of angular momentum from the wave into the disk is given by the negative divergence of the angular momentum flux. If a wave with incoming flux $F_J(r_s)$ decays exponentially with a damping length $\ell$ beyond a radius $r_s$, the fraction of its angular momentum deposited into the disk over a distance $\Delta r$ is given by $1 - \exp(-\Delta r / \ell)$ [@problem_id:3520538]. This process of wave launching, propagation, and dissipation is the fundamental mechanism of the Lindblad torque.

#### Corotation Torques and Horseshoe Dynamics

The **corotation torque** arises from gas in the region co-orbiting with the planet. In the frame rotating with the planet, fluid elements near corotation do not simply pass by but are deflected by the planet's potential, executing characteristic U-turns. These trajectories are called **horseshoe orbits**, and the region they occupy is the **horseshoe region**.

The half-width of this region, $x_s$, and the time it takes for a fluid element to traverse a full horseshoe orbit, the **[libration](@entry_id:174596) period** $t_{\text{lib}}$, are key parameters. In a low-mass regime, an energy balance argument shows that the kinetic energy of the [shear flow](@entry_id:266817) is balanced by the planet's potential energy, leading to a scaling for the half-width [@problem_id:3520489]:
$$ x_s \propto a \sqrt{\frac{q}{h}} $$
where $q=M_p/M_\star$ is the [mass ratio](@entry_id:167674) and $h=H/a$ is the disk [aspect ratio](@entry_id:177707). A more massive planet or a colder (thinner) disk results in a wider horseshoe region. The [libration](@entry_id:174596) period is inversely proportional to the shear across this region, scaling as:
$$ t_{\text{lib}} \propto \frac{1}{\Omega} \sqrt{\frac{h}{q}} $$
A wider horseshoe region leads to a shorter [libration](@entry_id:174596) time [@problem_id:3520489].

The corotation torque itself arises because fluid elements executing horseshoe turns carry their "native" [fluid properties](@entry_id:200256) with them. A fluid parcel from the inner disk that gets torqued onto an outer orbit brings its higher vortensity and (potentially) different entropy to the outer part of the horseshoe region. This advection of conserved quantities creates an azimuthal asymmetry in the [surface density](@entry_id:161889) distribution around the planet, which in turn exerts a gravitational torque [@problem_id:3520505]. Two primary components contribute to this torque:

1.  **Vortensity-Related Torque**: In a barotropic disk, [potential vorticity](@entry_id:276663) (or **vortensity**), defined as $w = \zeta/\Sigma$ (where $\zeta$ is the vorticity), is conserved along streamlines. The advection of vortensity creates a density perturbation that is proportional to the negative of the vortensity gradient. This leads to a torque whose sign and magnitude depend on the radial gradient of $\Sigma/B$, where $B$ is Oort's second constant related to vorticity. Specifically, $\Gamma_w \propto +d\ln(\Sigma/B)/d\ln r$.

2.  **Entropy-Related Torque**: In a non-barotropic disk, specific entropy, proportional to $\ln(P/\Sigma^\gamma)$, is also conserved. Advection of entropy creates [density perturbations](@entry_id:159546) at nearly constant pressure, leading to an additional torque component. This torque is proportional to the negative of the entropy gradient: $\Gamma_S \propto -d\ln(P/\Sigma^\gamma)/d\ln r$.

These [corotation torques](@entry_id:747895) can be positive and very powerful, potentially strong enough to counteract the negative Lindblad torque and even drive outward migration.

However, the corotation torque is subject to **saturation**. Over one [libration](@entry_id:174596) period, the horseshoe flow tends to mix the fluid within the co-orbital region, erasing the very radial gradients in vortensity and entropy that generate the torque. If this happens, the torque "saturates" and decays to a small value. Saturation can be prevented if there is a diffusive process—such as viscosity (for vortensity) or thermal diffusion (for entropy)—that acts to replenish the gradients across the horseshoe region from the background disk. The torque remains unsaturated if the diffusion timescale, $t_D \sim x_s^2/D$ (where $D$ is the relevant diffusivity), is shorter than or comparable to the [libration](@entry_id:174596) timescale, $t_{\text{lib}}$. If $t_D \gg t_{\text{lib}}$, the torque will saturate [@problem_id:3520478]. Because viscosity and [thermal diffusivity](@entry_id:144337) can be different ($\nu \neq \chi$), it is possible for one component of the corotation torque to be saturated while the other is not.

### Synthesis: Regimes of Planetary Migration

The combination of these physical mechanisms gives rise to distinct, well-defined regimes of [planetary migration](@entry_id:158688), primarily characterized by the planet's mass relative to the disk properties [@problem_id:3520527].

-   **Type I Migration**: This regime applies to low-mass planets (typically $q \lesssim h^3$) that only weakly perturb the disk and do not open a gap. The migration is governed by the linear sum of Lindblad and [corotation torques](@entry_id:747895). The characteristic migration rate is very fast and scales as:
    $$ \dot{a}_{\mathrm{I}} \sim - \Omega a \left(\frac{\Sigma a^2}{M_\star}\right) \frac{q}{h^2} $$
    The direction and speed depend sensitively on the balance between the (usually negative) Lindblad torque and the (often positive) unsaturated corotation torque.

-   **Type II Migration**: When a planet becomes massive enough to overcome the disk's pressure and viscous forces (typically for $q \gtrsim h^3$), it carves out a deep annular gap around its orbit. The planet becomes gravitationally locked to the disk gas at the gap edges. Its migration is no longer governed by local torques but is slaved to the viscous evolution of the entire disk. The planet drifts inward at the viscous drift speed of the gas:
    $$ \dot{a}_{\mathrm{II}} \sim - \alpha h^2 a \Omega $$
    This is generally much slower than Type I migration.

-   **Type III Migration (Runaway Migration)**: This is a rapid, potentially runaway regime that can occur for intermediate-mass planets (e.g., Saturn-mass) in massive disks. It is driven by a large-scale mass flux across the planet's co-orbital region. If the co-orbital region is partially depleted, a **co-orbital mass deficit** ($M_{\text{def}}$) is established. The planet's [radial drift](@entry_id:158246) induces a mass flux across its orbit that interacts with this deficit, creating a powerful feedback torque. Runaway is triggered when the mass in the co-orbital region is comparable to or greater than the planet's own mass ($M_{\text{local}} \gtrsim M_p$). This condition allows the co-orbital torque to effectively reduce the planet's inertia, leading to extremely fast migration on a timescale much shorter than the viscous time [@problem_id:3520498].

### Beyond the Plane: Three-Dimensional Effects

While 2D models capture much of the essential physics, the disk is a 3D structure. One important 3D effect occurs when a planet's orbit is inclined relative to the disk midplane. Such a planet exerts a vertical gravitational force on the disk, exciting a **warp**. The warp is a large-scale twist or bend in the disk structure. The propagation of this warp through the disk depends on a competition between pressure and viscosity [@problem_id:3520543].

-   **Wave-like Propagation**: In disks with low viscosity relative to their thickness ($\alpha \lesssim h$), pressure forces dominate. The warp propagates as a bending wave at a speed on the order of the sound speed, $v_{\text{wave}} \sim c_s$.

-   **Diffusive Propagation**: In disks with high viscosity ($\alpha \gtrsim h$), viscous torques damp the bending wave motion before it can propagate. The warp's evolution becomes diffusive. In this regime, the warp spreads rapidly on a timescale that is much shorter than the standard viscous timescale of the disk.

Understanding these 3D effects is crucial for explaining phenomena such as inclined and misaligned [planetary orbits](@entry_id:179004), which are commonly observed.