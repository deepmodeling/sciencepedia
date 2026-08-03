## Introduction
How do gas giant planets like Jupiter and Saturn acquire their vast and intricate systems of moons? The answer lies in a miniature version of the planet-forming process itself, unfolding within a swirling vortex of gas and dust known as a [circumplanetary disk](@entry_id:1122411) (CPD). Understanding these disks is fundamental to planetary science, as they represent the final stage of planet accretion and the direct birthplace of regular satellite systems. This article addresses the key question of how solid material within a CPD overcomes physical barriers to grow from microscopic dust into the diverse moons we observe today.

This exploration is structured into three distinct parts. In **"Principles and Mechanisms,"** we will dissect the fundamental physics governing the formation, structure, and evolution of CPDs, from the gravitational boundaries that define them to the turbulent processes that drive their evolution and the mechanisms like [pebble accretion](@entry_id:158008) that enable satellite growth. Next, **"Applications and Interdisciplinary Connections"** will bridge theory and observation, demonstrating how these principles explain the architecture and composition of systems like Jupiter’s Galilean moons, inform the search for [exomoons](@entry_id:1124730), and connect to broader topics like [tidal heating](@entry_id:161808) and [orbital resonance](@entry_id:163430). Finally, **"Hands-On Practices"** will provide practical, computational exercises to model key disk processes, allowing you to apply these concepts and investigate the conditions that foster the birth of new worlds.

## Principles and Mechanisms

The formation of a satellite system around a giant planet is a microcosm of the planet formation process itself. It unfolds within a dynamic, gaseous structure known as a **[circumplanetary disk](@entry_id:1122411) (CPD)**. This chapter elucidates the fundamental principles governing the formation, structure, and evolution of these disks, and the mechanisms by which solid material within them grows to form satellites.

### The Circumplanetary Environment: Defining the Stage

A [circumplanetary disk](@entry_id:1122411) is a rotationally supported disk of gas and solids that is gravitationally bound to a forming planet. It is the crucible for regular satellite formation, distinct from the larger **protoplanetary disk (PPD)** in which the planet itself is embedded . To understand the processes within a CPD, we must first define its physical boundaries, which are governed by a delicate balance of gravitational forces and magnetohydrodynamic interactions.

#### The Hill Sphere: The Outer Boundary

The gravitational sphere of influence of a planet orbiting a star is not infinite. The planet's gravity must compete with the tidal pull of the central star. The region where the planet's gravity dominates is approximated by the **Hill sphere**. For a planet of mass $M_p$ orbiting a star of mass $M_{\star}$ at a semi-major axis $a$, the Hill radius, $R_H$, is derived by balancing the planet's gravity with the differential gravitational and centrifugal forces from the star in the corotating frame. This yields the expression:

$R_H = a \left( \frac{M_p}{3 M_{\star}} \right)^{1/3}$

Material within this radius can be considered gravitationally bound to the planet. Consequently, the Hill radius sets the natural outer scale for a [circumplanetary disk](@entry_id:1122411). However, hydrodynamic interactions and torques from the surrounding protoplanetary disk typically truncate the CPD at a fraction of this radius, often estimated to be between $0.3$ and $0.5$ times $R_H$ .

#### The Roche Limit: The Inner Boundary for Satellite Formation

While the Hill sphere defines the outer domain, another critical boundary exists closer to the planet: the **Roche limit**, $a_R$. Inside this radius, the planet's [tidal forces](@entry_id:159188) are so strong that they can overcome the [self-gravity](@entry_id:271015) of a satellite, disrupting it. For a fluid satellite of density $\rho_s$ orbiting a planet of radius $R_p$ and mean density $\rho_p$, the Roche limit is given by:

$a_R \approx 2.44 R_p \left( \frac{\rho_p}{\rho_s} \right)^{1/3}$

This radius sets a firm inner boundary for the formation of satellites through the gentle accumulation of material. Any object held together primarily by gravity that strays inside this limit will be torn apart. Notably, the Roche limit depends only on the properties of the planet and the satellite, not on the planet's distance from the star .

For a Jupiter-like planet ($M_p = 1\,M_J$, $R_p = 1\,R_J$, $\rho_p = 1.33\,\mathrm{g\,cm^{-3}}$) orbiting a Sun-like star at $5\,\mathrm{AU}$, the Hill radius is vast, $R_H \approx 0.35\,\mathrm{AU}$. In contrast, the Roche limit for an icy satellite ($\rho_s = 1.0\,\mathrm{g\,cm^{-3}}$) is only $a_R \approx 0.0012\,\mathrm{AU}$. The ratio $R_H / a_R$ is on the order of $300$, signifying a very large radial domain—from a few planetary radii out to several hundred—where satellite formation can occur .

#### The Magnetospheric Radius: The Inner Disk Edge

At the innermost edge of the CPD, the planet's magnetic field can become the dominant force. The interaction between the conducting gas of the disk and the planet's magnetosphere can truncate the disk at the **magnetospheric radius**, $R_t$. This occurs where the magnetic pressure of the planetary field, $P_{\text{mag}}$, balances the [ram pressure](@entry_id:194932) of the accreting gas, $P_{\text{ram}}$. For a dipolar magnetic field with moment $\mu$, the magnetic pressure scales as $P_{\text{mag}} \propto B^2 \propto \mu^2 / r^6$. The [ram pressure](@entry_id:194932) of gas in free-fall onto the planet, accreting at a rate $\dot{M}$, scales as $P_{\text{ram}} = \rho v^2 \propto \dot{M} \sqrt{G M_p} / r^{5/2}$.

Equating these pressures at $r = R_t$ and solving for the radius yields the scaling relationship :

$R_t \propto \left( \frac{\mu^4}{G M_p \dot{M}^2} \right)^{1/7}$

This relationship shows that a stronger magnetic field ($\mu$) or a lower planetary mass ($M_p$) leads to a larger magnetosphere. Crucially, a higher [mass accretion rate](@entry_id:161925) ($\dot{M}$) results in a more powerful inflow that compresses the magnetosphere, causing $R_t$ to decrease. Gas flow is disrupted at this radius, and material is channeled along magnetic field lines onto the planet in **accretion funnels**.

### Formation and Structure of the Circumplanetary Disk

A CPD does not simply appear fully formed. It is built and sustained by a continuous inflow of gas and dust from the surrounding protoplanetary disk. The physics of this inflow process dictates the fundamental properties of the CPD, such as its size, mass, and thermal structure.

#### Angular Momentum and the Circularization Radius

Gas flowing from the PPD toward the planet carries with it the specific angular momentum, $j$, it possessed in its orbit around the star. Due to the conservation of angular momentum, this material cannot fall directly onto the planet. Instead, it spirals inward until the [centrifugal force](@entry_id:173726) balances the planet's gravity, at which point it settles into a circular orbit. The radius at which this occurs is the **circularization radius**, $R_c$.

For a particle in a [circular orbit](@entry_id:173723), the specific angular momentum is $j = r v_{\phi}$, where $v_{\phi} = \sqrt{G M_p / r}$ is the Keplerian velocity. Solving for the radius gives:

$R_c = \frac{j^2}{G M_p}$

This fundamental relation shows that the initial size of the CPD is determined by the square of the specific angular momentum of the inflowing gas. A higher $j$ results in a larger, more extended disk. If the inflowing material has very low angular momentum, rotational support is weak, and the gas may form a compact, pressure-supported envelope around the planet rather than a thin, rotationally supported disk . Accretion shocks, which dissipate [orbital energy](@entry_id:158481) but largely conserve angular momentum, are the mechanism by which the gas transitions from an infall trajectory to a [circular orbit](@entry_id:173723) at $R_c$ .

#### Three-Dimensional Accretion Flows

The supply of mass and angular momentum to the CPD is a complex, three-dimensional process. Numerical simulations have revealed two primary accretion channels :

1.  **Midplane Flows**: Gas originating from the PPD midplane, near the planet's orbit, possesses high specific angular momentum relative to the planet due to the background Keplerian shear. This material enters the Hill sphere in a quasi-coplanar fashion and spirals inward, feeding the outer regions of the CPD and exciting prominent [spiral density waves](@entry_id:161546).

2.  **High-Latitude Streams**: Gas from above and below the dense midplane of the PPD ($|z| \gtrsim H$, where $H$ is the PPD scale height) is less rotationally supported and has very low specific angular momentum relative to the planet. This material can fall more directly toward the planet in nearly ballistic, high-latitude streams.

These high-latitude streams plunge toward the planet and shock violently upon impact with the surface of the denser, rotationally supported disk below. For a Jupiter-mass planet at 5 AU, the free-fall speed of this material from the Hill radius can reach several kilometers per second, generating a strong, **supercritical accretion shock** with a Mach number $M \gg 1$. This shock is a major source of heat, depositing energy at the disk surface and puffing up the inner regions of the CPD, making it geometrically thick .

#### Conditions for Disk Formation

For a stable, rotationally supported disk to form and persist, two key conditions must be met :

1.  **Gravitational Capture**: The planet must be massive enough to gravitationally capture gas from the PPD. This is typically met when the planet's Hill radius is larger than the local PPD pressure [scale height](@entry_id:263754), $R_H \gtrsim H = c_s / \Omega_{\star}$. This ensures the planet's gravitational influence extends over a region large enough to efficiently channel the two-dimensional midplane flows.

2.  **Thermal Settling**: Once captured, the gas must be able to cool efficiently to dissipate the heat from compression and shocks. This allows the gas to lose pressure support and collapse vertically into a thin, centrifugally supported disk. The condition for this is that the local cooling time, $t_{\text{cool}}$, must be comparable to or shorter than the local dynamical (orbital) time around the planet, $t_{\text{dyn}} = \Omega_p^{-1} = \sqrt{r^3 / (G M_p)}$. If $t_{\text{cool}} \gg t_{\text{dyn}}$, the gas remains hot and pressure-supported, forming a quasi-spherical envelope instead of a disk. For a Jupiter-like planet at 5 AU, typical parameters show $R_H/H > 1$ and $t_{\text{cool}}/t_{\text{dyn}} \sim 1-2$, conditions conducive to the formation of a turbulent, rotationally supported CPD.

### The Thermal and Dynamical State of the Disk

The evolution of the CPD and its ability to foster satellite formation are dictated by its internal physics, namely its energy balance and the mechanisms that transport angular momentum.

#### The CPD Energy Budget

The temperature of a CPD at any given location is set by a balance between heating sources and cooling mechanisms. Understanding this energy budget is crucial, as the temperature determines the location of icelines, influences disk dynamics, and sets the scale for many physical processes. The main components are :

*   **Viscous Heating ($Q^+_{\text{visc}}$)**: As gas flows inward through the disk, angular momentum is transported outward via turbulent viscosity. This process dissipates gravitational potential energy as heat. For a steady [accretion disk](@entry_id:159604), this heating rate per unit area scales steeply with radius as $Q^+_{\text{visc}} \propto r^{-3}$. Since it arises from internal shear, this heating is volumetric, peaking at the dense midplane.

*   **Irradiation ($F_{\text{irr}}$)**: The disk is illuminated by both the central planet and the distant star. Planetary [irradiation](@entry_id:913464) provides a flux that decreases with distance as $F_{\text{irr},p} \propto r^{-2}$. Stellar [irradiation](@entry_id:913464), from a source at distance $a \gg r$, provides a nearly uniform flux across the disk, $F_{\text{irr},*} \approx \text{constant}$. Both sources are absorbed in the surface layers of the optically thick disk, primarily heating its atmosphere.

*   **Shock Heating ($Q^+_{\text{shock}}$)**: As discussed previously, the infall of high-latitude streams creates strong shocks at the disk surface. This provides a powerful heating source, with a flux $Q^+_{\text{shock}} \propto \dot{\Sigma}_{\text{in}} r^{-1}$, where $\dot{\Sigma}_{\text{in}}$ is the local mass infall rate.

*   **Radiative Cooling ($Q^-$)**: The disk cools by radiating thermal energy into space from its surfaces (photospheres). For an optically thick disk, the emergent flux is given by the Stefan-Boltzmann law, $Q^{-} = 2\sigma T_{\text{eff}}^4$, where $T_{\text{eff}}$ is the effective surface temperature. This cooling process is highly sensitive to temperature and is regulated by the efficiency of vertical energy transport from the hot midplane to the cool surface, which depends on the disk's opacity.

#### Angular Momentum Transport and Turbulence

For gas in the CPD to accrete onto the central planet, it must lose angular momentum. This requires a mechanism to transport angular momentum outward. The most widely accepted mechanism is **turbulence**, which generates an [effective viscosity](@entry_id:204056). In the phenomenological **$\alpha$-disk model** proposed by Shakura and Sunyaev, the kinematic viscosity $\nu$ is parameterized as:

$\nu = \alpha c_s H$

where $c_s$ is the sound speed, $H = c_s / \Omega$ is the vertical [scale height](@entry_id:263754), and $\alpha$ is a dimensionless parameter representing the efficiency of turbulent transport. For a thin, isothermal Keplerian disk, this simplifies to $\nu = \alpha c_s^2 / \Omega$ . The value of $\alpha$ is determined by the underlying physical drivers of the turbulence.

Potential drivers include :
*   **Magnetorotational Instability (MRI)**: This is a powerful instability that can operate in weakly magnetized, differentially rotating disks. It is considered a primary source of turbulence in many astrophysical disks. However, its operation requires sufficient coupling between the gas and the magnetic field. In the dense, cool midplanes of CPDs, the ionization fraction can be very low, leading to high electrical resistivity. This can quench the MRI, creating a quiescent or "dead" zone. The activity of MRI is often quantified by the **Elsasser number**, $\Lambda = v_A^2 / (\eta \Omega)$, where $v_A$ is the Alfvén speed and $\eta$ is the magnetic diffusivity. MRI is suppressed when $\Lambda \ll 1$. Calculations for typical CPD conditions often yield $\Lambda \ll 1$ in the midplane, suggesting that a constant-$\alpha$ model is an oversimplification and that turbulence may be layered, with active surface layers and a dead midplane.
*   **Hydrodynamic Instabilities**: In regions where MRI is inactive, purely [hydrodynamic instabilities](@entry_id:750450) may drive turbulence, albeit typically at a lower level ($\alpha \ll 10^{-2}$). Examples include the **Vertical Shear Instability (VSI)** and **convective overstability**, which can operate in disks with radial temperature gradients and sufficiently short cooling times.

### From Dust to Satellites

The final step in our narrative is the formation of solid satellites from the dust and ice embedded in the gaseous CPD. This process involves the growth of microscopic grains into kilometer-sized bodies and their subsequent migration within the disk.

#### The Fragmentation Barrier

Microscopic dust grains in the CPD collide and stick together via van der Waals forces, a process known as **coagulation**. However, this growth is limited by destructive collisions induced by turbulence. Turbulent gas motions impart random velocities to the particles, with the resulting [relative velocity](@entry_id:178060) $\delta v$ between two similar particles depending on their aerodynamic properties. For particles with a dimensionless [stopping time](@entry_id:270297) (Stokes number) ${\rm St} \ll 1$, the [relative velocity](@entry_id:178060) scales as $\delta v \sim \sqrt{\alpha} c_s \sqrt{\rm St}$.

Collisions are only productive up to a certain impact speed, known as the **fragmentation threshold velocity**, $v_{\text{frag}}$, which depends on the material properties of the grains (e.g., icy vs. rocky). When turbulent velocities exceed this threshold, collisions lead to fragmentation rather than growth. This "fragmentation barrier" sets a maximum particle size that can be reached by simple coagulation . By setting $\delta v = v_{\text{frag}}$, we can derive the maximum Stokes number, ${\rm St}_{\max}$, and the corresponding maximum particle size, $a_{\max}$:

${\rm St}_{\max} \sim \frac{v_{\text{frag}}^2}{\alpha c_s^2}$

In the Epstein drag regime, this translates to a maximum physical size $a_{\max} \propto \frac{\Sigma_g v_{\text{frag}}^2}{\rho_s \alpha c_s^2}$, where $\Sigma_g$ is the gas surface density. This barrier poses a significant challenge for growing planetesimals directly from dust.

#### Pebble Accretion: A Path to Growth

A powerful mechanism to overcome the fragmentation barrier is **[pebble accretion](@entry_id:158008)**. "Pebbles" are solid particles, typically centimeter-sized, that have reached the fragmentation limit but are still strongly coupled to the gas. Their motion is characterized by the **Stokes number**, ${\rm St} = t_{\text{stop}}\Omega$, which compares the aerodynamic [stopping time](@entry_id:270297) $t_{\text{stop}}$ to the orbital timescale $\Omega^{-1}$.

*   If ${\rm St} \ll 1$, particles are tightly coupled to the gas and follow its flow, making it difficult for a satellite embryo to accrete them as they are diverted around it.
*   If ${\rm St} \gg 1$, particles are decoupled from the gas and behave ballistically, passing by an embryo too quickly for gravity to capture them.
*   If ${\rm St} \sim 1$, particles are optimally coupled. They are not entirely bound to the gas flow, allowing them to drift toward an embryo, but they experience enough [gas drag](@entry_id:1125488) to dissipate energy and be gravitationally captured.

This makes [pebble accretion](@entry_id:158008) an extremely efficient process for particles with Stokes numbers of order unity, allowing satellite embryos to grow rapidly to substantial masses .

#### Satellite Migration

Once satellite embryos reach a sufficient mass, their gravitational influence on the surrounding gas disk generates a net torque, causing them to migrate radially. For low-mass satellites that do not open a gap in the disk (the **Type I migration** regime), the total torque $\Gamma$ is a delicate sum of two competing effects :

1.  **Lindblad Torque ($\Gamma_L$)**: The satellite excites [spiral density waves](@entry_id:161546) at Lindblad resonances. The inner wave pulls the satellite back, exerting a negative torque, while the outer wave pulls it forward, exerting a positive torque. In typical disks with density decreasing with radius, the inner torque dominates, resulting in a net negative Lindblad torque ($\Gamma_L  0$) that drives rapid inward migration.

2.  **Corotation Torque ($\Gamma_C$)**: This torque arises from gas in horseshoe orbits near the satellite. In a non-isothermal disk, it has two key components. The first is related to the radial gradient of vortensity. The second, and often more powerful, component is the **entropy-related torque**. It arises from buoyancy forces acting on gas parcels as they move across the radial entropy gradient of the disk. This torque is positive ($\Gamma_C > 0$) when the disk's entropy decreases with radius.

A strong, positive [corotation torque](@entry_id:1123086) can partially offset or even overcome the negative Lindblad torque, potentially slowing, halting, or even reversing the inward migration. This effect is crucial, as it provides a potential mechanism for stopping satellites at specific locations, possibly explaining the observed architecture of systems like the Galilean moons around Jupiter . The survival and final placement of satellites are thus intricately linked to the thermal and dynamical structure of their parent [circumplanetary disk](@entry_id:1122411).