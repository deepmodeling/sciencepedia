## Introduction
Spray injection and [evaporation](@entry_id:137264) are fundamental processes in a vast array of engineering and natural systems, from internal combustion engines and gas turbines to atmospheric cloud formation. The challenge for computational scientists lies in accurately simulating this complex multiphase phenomenon, which spans multiple scales from the macroscopic injector to the microscopic behavior of individual droplets. Effective modeling requires a hierarchical approach, integrating the physics of liquid [atomization](@entry_id:155635), droplet transport, and thermodynamic [phase change](@entry_id:147324) within a robust numerical framework. This article bridges this knowledge gap by providing a comprehensive guide to modern [spray modeling](@entry_id:755251) techniques. The "Principles and Mechanisms" chapter lays the groundwork by detailing the physics of [atomization](@entry_id:155635), droplet dynamics, and the Lagrangian-Eulerian numerical method. The "Applications and Interdisciplinary Connections" chapter explores how these foundational models are extended to tackle real-world challenges like dense sprays, [combustion](@entry_id:146700), and [inverse design](@entry_id:158030). Finally, the "Hands-On Practices" section offers practical exercises to solidify understanding and verify numerical implementations. By progressing through these sections, you will gain a deep, practical understanding of how to model and simulate spray injection and [evaporation](@entry_id:137264) in a CFD context.

## Principles and Mechanisms

The modeling of spray injection and [evaporation](@entry_id:137264) in a Computational Fluid Dynamics (CFD) framework is a quintessential [multiphase flow](@entry_id:146480) problem, bridging the gap between macroscopic engineering hardware and microscopic transport phenomena. It requires a hierarchy of models to describe the journey of a liquid from a continuous bulk phase to a dispersed collection of evaporating droplets interacting with a turbulent gas. This chapter details the fundamental principles and mechanisms that underpin these models, progressing from the initial [atomization](@entry_id:155635) of the liquid, through the life cycle of individual droplets, to their collective behavior and numerical representation.

### From Liquid Core to Droplets: The Physics of Atomization

The transformation of a continuous liquid stream into a spray of discrete droplets is known as **[atomization](@entry_id:155635)**. This process is broadly categorized into two sequential stages: primary and secondary breakup. 

**Primary breakup** refers to the initial, near-nozzle disintegration of the continuous liquid core. High-speed injection creates a large velocity difference between the liquid and the surrounding quiescent gas, leading to rapid growth of interfacial instabilities. These instabilities, driven by aerodynamic shear, amplify until they shatter the liquid column into ligaments and large, irregular fragments.

**Secondary breakup** describes the subsequent fragmentation of these large, detached liquid fragments and droplets. If a droplet's relative velocity with respect to the gas is sufficiently high, the aerodynamic forces acting on it can overcome its own surface tension, causing it to deform and break apart into smaller, more stable droplets.

The onset and dynamics of both breakup processes are governed by the competition between disruptive aerodynamic forces and restorative [cohesive forces](@entry_id:274824) within the liquid. This competition is quantified by two key [dimensionless numbers](@entry_id:136814):

1.  The **Weber number** ($We$), defined as $We = \frac{\rho_g U_r^2 d}{\sigma}$, represents the ratio of the disruptive aerodynamic pressure ($\sim \rho_g U_r^2$) to the restorative capillary pressure due to surface tension ($\sim \sigma/d$). Here, $\rho_g$ is the gas density, $U_r$ is the relative velocity between the phases, $d$ is a [characteristic length](@entry_id:265857) scale (e.g., the nozzle diameter for primary breakup or the droplet diameter for secondary breakup), and $\sigma$ is the liquid's surface tension. Aerodynamically driven breakup is initiated when the Weber number exceeds a critical value, typically on the order of $We_{crit} \sim 10$. It is crucial to use the gas density $\rho_g$, as it is the motion of the gas relative to the liquid that generates the deforming aerodynamic stress. 

2.  The **Ohnesorge number** ($Oh$), defined as $Oh = \frac{\mu_l}{\sqrt{\rho_l \sigma d}}$, relates the liquid's internal [viscous forces](@entry_id:263294) to its inertial and surface tension forces. Here, $\mu_l$ is the liquid viscosity and $\rho_l$ is the liquid density. Viscosity acts as a stabilizing influence by damping internal fluid motion and resisting deformation. A higher Ohnesorge number signifies a more viscous liquid, which requires a stronger aerodynamic force to break apart. Consequently, the critical Weber number for breakup, $We_{crit}$, increases with increasing $Oh$. 

The timescales of these processes are also of critical importance. For primary breakup driven by shear instabilities, a characteristic timescale can be estimated as $t_{pb} \sim (\rho_l / \rho_g)^{1/2} D/U_r$, indicating that breakup is faster for higher injection velocities and denser ambient gases. For secondary breakup at high Weber numbers ($We \gg 1$) and low Ohnesorge numbers ($Oh \ll 1$), the process is often governed by Rayleigh-Taylor instabilities. The corresponding breakup timescale, $t_{sb}$, scales as $t_{sb} \sim (\rho_l / \rho_g)^{1/2} d/U_r$, which can also be expressed in terms of the capillary-inertial timescale $t_{\sigma} = \sqrt{\rho_l d^3 / \sigma}$ as $t_{sb} \sim t_{\sigma}/\sqrt{We}$. 

### Modeling the Spray Source: Injection Boundary Conditions

In a CFD simulation, the complex physics of [atomization](@entry_id:155635) are typically not resolved directly. Instead, they are encapsulated in an injection model that specifies the initial properties of the spray at a boundary. For a simple pressure atomizer, such as a plain-orifice injector, these properties can be derived from fundamental conservation laws. 

Consider a liquid of density $\rho_l$ injected from an upstream reservoir at pressure $p_u$ through a nozzle of area $A_o$ into a chamber at [back pressure](@entry_id:188390) $p_b$. The key parameters for the spray boundary condition are the total mass flow rate ($\dot{m}$), the mean injection velocity vector ($\mathbf{u}_0$), the spray cone angle ($\theta$), and the liquid temperature ($T_l$).

The [mass flow rate](@entry_id:264194) can be determined using the Bernoulli equation, modified to account for real-fluid effects such as viscous losses and [vena contracta](@entry_id:273611). These effects are lumped into an empirical **[discharge coefficient](@entry_id:276642)**, $C_d \in (0,1)$. The resulting expression for the [mass flow rate](@entry_id:264194) is:
$$ \dot{m} = C_d A_o \sqrt{2 \rho_l (p_u - p_b)} $$
Once the mass flow rate is known, the mean injection velocity magnitude, $u_0$, is found from mass conservation at the nozzle exit: $u_0 = \frac{\dot{m}}{\rho_l A_o}$. If the injection is normal to the boundary, with an outward [unit normal vector](@entry_id:178851) $\hat{\mathbf{n}}$, the velocity vector is $\mathbf{u}_0 = u_0 \hat{\mathbf{n}}$.

For a non-cavitating, plain-orifice injector, the liquid exits as a coherent jet, so the initial spray cone half-angle is taken to be $\theta = 0$. The liquid temperature at the exit, $T_l$, depends on the thermal energy balance across the nozzle. While [viscous dissipation](@entry_id:143708) can cause a slight temperature rise (Joule-Thomson effect), this is often negligible for the short residence time in the orifice. Under the common modeling assumption of an [adiabatic process](@entry_id:138150) with negligible [viscous heating](@entry_id:161646), the exit temperature is equal to the upstream liquid temperature, $T_l = T_u$. 

### Dynamics and Thermodynamics of a Single Droplet

Once injected, the spray is modeled as a collection of individual droplets. The evolution of each droplet's velocity, temperature, and size is governed by a set of coupled [ordinary differential equations](@entry_id:147024) that model the transport of momentum, heat, and mass between the droplet and the surrounding gas.

#### Momentum Transfer and Drag

A droplet's motion is governed by Newton's second law, $m_p \frac{d\mathbf{u}_p}{dt} = \sum \mathbf{F}_i$. In many spray applications, the dominant force is the [aerodynamic drag](@entry_id:275447), $\mathbf{F}_D$. This force is expressed as:
$$ \mathbf{F}_D = \frac{1}{2} \rho_g C_D A_p |\mathbf{u}_g - \mathbf{u}_p| (\mathbf{u}_g - \mathbf{u}_p) $$
where $\mathbf{u}_p$ and $\mathbf{u}_g$ are the droplet and local gas velocities, $A_p = \pi d_p^2/4$ is the droplet's projected area, and $C_D$ is the dimensionless **[drag coefficient](@entry_id:276893)**.

The [drag coefficient](@entry_id:276893) is not constant; it is a strong function of the **particle Reynolds number**, defined based on the slip velocity:
$$ Re_p = \frac{\rho_g |\mathbf{u}_g - \mathbf{u}_p| d_p}{\mu_g} $$
where $\mu_g$ is the gas dynamic viscosity. Different correlations for $C_D(Re_p)$ are used depending on the flow regime :
-   **Stokes Regime ($Re_p \lesssim 1$):** At very low Reynolds numbers, viscous forces dominate, and the drag coefficient is given by the analytical solution $C_D = \frac{24}{Re_p}$.
-   **Transitional Regime ($1 \lesssim Re_p \lesssim 1000$):** As inertial effects become significant, $C_D$ deviates from the Stokes law. A widely used empirical correlation for rigid spheres in this regime is the **Schiller-Naumann correlation**:
    $$ C_D = \frac{24}{Re_p} \left( 1 + 0.15 Re_p^{0.687} \right) $$
-   **Newton Regime ($Re_p \gtrsim 1000$):** At high Reynolds numbers, the flow in the droplet's wake is fully turbulent, and the drag coefficient becomes nearly constant, $C_D \approx 0.44$.

For instance, a $50\,\mu\mathrm{m}$ ethanol droplet with a slip speed of $15\,\mathrm{m/s}$ in air at standard conditions has a particle Reynolds number of approximately $Re_p = 50$. This falls squarely in the transitional regime, making the Schiller-Naumann correlation an appropriate choice for modeling its drag. 

#### Heat Transfer

The temperature of a droplet evolves due to [convective heat transfer](@entry_id:151349) from the hot ambient gas and the energy consumed by evaporation. A common approach to modeling the droplet's internal energy is the **[lumped-capacitance model](@entry_id:140095)**, which assumes the droplet has a uniform internal temperature, $T_d$. This is justified when internal heat conduction is much faster than external heat convection. The [energy balance](@entry_id:150831) for the droplet is then:
$$ m c_l \frac{dT_d}{dt} = \dot{Q}_{conv} - \dot{Q}_{evap} = h A_p (T_g - T_s) - \dot{m} L_v $$
Here, $m$ is the droplet mass, $c_l$ is the liquid specific heat, $h$ is the [convective heat transfer coefficient](@entry_id:151029), $T_g$ is the ambient gas temperature, $T_s$ is the droplet surface temperature, $\dot{m}$ is the [evaporation rate](@entry_id:148562), and $L_v$ is the latent heat of vaporization. 

The validity of the [lumped-capacitance model](@entry_id:140095) is determined by the **Biot number**:
$$ Bi = \frac{h d_p}{k_l} $$
where $k_l$ is the thermal conductivity of the liquid. The Biot number represents the ratio of internal conductive resistance to external convective resistance. The lumped model is accurate when $Bi \ll 0.1$. If this condition is not met, internal temperature gradients are significant, and a more complex **finite-conductance model**, which solves the [heat conduction](@entry_id:143509) equation within the droplet, must be employed. 

The heat transfer coefficient $h$ is obtained from correlations for the **Nusselt number**, $Nu = \frac{h d_p}{k_g}$, where $k_g$ is the gas thermal conductivity. A standard correlation for spheres is the **Ranz-Marshall correlation**:
$$ Nu = 2 + 0.6 Re_p^{1/2} Pr^{1/3} $$
where $Pr$ is the gas-phase Prandtl number. The constant 2 represents the theoretical limit for pure heat conduction from a sphere in a stagnant medium ($Re_p \to 0$), while the second term accounts for the enhancement of heat transfer by [forced convection](@entry_id:149606). 

#### Mass Transfer and Evaporation

The physics of mass transfer from the droplet surface are analogous to heat transfer. The [evaporation rate](@entry_id:148562) $\dot{m}$ is determined by the [convective mass transfer coefficient](@entry_id:156604), which is expressed in terms of the dimensionless **Sherwood number**, $Sh = \frac{k_m d_p}{D_{v,g}}$, where $k_m$ is the [mass transfer coefficient](@entry_id:151899) and $D_{v,g}$ is the binary diffusivity of the vapor in the gas. The [heat-mass transfer analogy](@entry_id:149984) allows the use of a similar Ranz-Marshall correlation for the Sherwood number:
$$ Sh = 2 + 0.6 Re_p^{1/2} Sc^{1/3} $$
where $Sc$ is the gas-phase Schmidt number. 

Under a set of simplifying assumptions (quasi-steady gas phase, infinite liquid conductivity, constant properties), these principles lead to the classic **$D^2$-law** of droplet evaporation. This law states that the square of the droplet diameter decreases linearly with time:
$$ d^2(t) = d_0^2 - K t $$
The **evaporation constant** $K$ is given by:
$$ K = 4 \left( \frac{\rho_g}{\rho_l} \right) D_{v,g} Sh \ln(1 + B_M) $$
This expression highlights the key factors controlling evaporation. The term $B_M$ is the **Spalding mass transfer number**, which represents the dimensionless driving force for evaporation, defined by the difference in vapor [mass fraction](@entry_id:161575) between the droplet surface ($Y_{v,s}$) and the [far field](@entry_id:274035) ($Y_{v,\infty}$). The logarithmic term, $\ln(1+B_M)$, arises from the correction for **Stefan flow**, the bulk motion of gas away from the surface caused by the evaporation itself. 

For **multicomponent droplets**, such as real-world fuels, the [evaporation](@entry_id:137264) process is more complex. Each component has a different volatility, leading to preferential [evaporation](@entry_id:137264) of the more volatile species and a continuous change in the liquid composition. The closure for the vapor mole fractions at the droplet surface, $y_i$, is provided by [vapor-liquid equilibrium](@entry_id:182756) (VLE) models. 
-   For an ideal liquid mixture, **Raoult's law** applies:
    $$ y_i p = x_i p_i^{\text{sat}}(T_s) $$
    where $x_i$ is the liquid [mole fraction](@entry_id:145460) of component $i$, $p$ is the total pressure, and $p_i^{\text{sat}}(T_s)$ is the pure-component saturation pressure at the surface temperature.
-   For [non-ideal mixtures](@entry_id:178975), liquid-phase interactions are accounted for by an **activity coefficient**, $\gamma_i$, leading to the **modified Raoult's law**:
    $$ y_i p = \gamma_i x_i p_i^{\text{sat}}(T_s) $$
These VLE relations are fundamental for accurately predicting the [evaporation rate](@entry_id:148562) and composition change of multicomponent fuel droplets. 

### The Influence of Turbulence on Droplet Behavior

Droplets in a spray are rarely in a quiescent environment; they are typically dispersed within a [turbulent flow](@entry_id:151300). The interaction between droplets and [turbulent eddies](@entry_id:266898) can significantly alter their trajectory and [spatial distribution](@entry_id:188271). This interaction is primarily governed by the **particle Stokes number** ($St$). 

The Stokes number is the ratio of the particle's momentum [response time](@entry_id:271485), $\tau_p$, to a characteristic timescale of the turbulent flow, $\tau_f$. The particle [response time](@entry_id:271485), derived from the Stokes drag law for a heavy particle ($\rho_l \gg \rho_g$), is:
$$ \tau_p = \frac{\rho_l d_p^2}{18 \mu_g} $$
For analyzing interaction with the smallest, most energetic eddies, the relevant flow timescale is the **Kolmogorov timescale**, $\tau_\eta = (\nu/\varepsilon)^{1/2}$, where $\nu$ is the gas kinematic viscosity and $\varepsilon$ is the [turbulent kinetic energy](@entry_id:262712) [dissipation rate](@entry_id:748577). The Stokes number is thus $St = \tau_p/\tau_\eta$.

The behavior of the droplets can be classified into three regimes based on their Stokes number:
-   **$St \ll 1$**: The particle response time is much shorter than the eddy turnover time. The droplets behave as passive **tracers**, closely following the fluid [pathlines](@entry_id:261720). Their slip velocity is small, and their spatial distribution tends to be uniform.
-   **$St \sim 1$**: The particle [response time](@entry_id:271485) is comparable to the eddy timescale. This leads to the strongest dynamic coupling. Due to their inertia, particles cannot follow the curved streamlines within an eddy and are centrifuged towards the outer regions. This mechanism results in strong **[preferential concentration](@entry_id:199717)**, where particles cluster in regions of high strain and low vorticity.
-   **$St \gg 1$**: The particle inertia is very large, and the [response time](@entry_id:271485) is much longer than the eddy timescale. The droplets are unresponsive to the fluctuations of the small eddies and follow near-**ballistic** trajectories, effectively filtering out the influence of the small-scale turbulence. They are largely influenced only by the larger, mean-flow structures. 

### The Numerical Framework of Lagrangian-Eulerian Simulation

The most common approach for simulating disperse sprays is the **Lagrangian-Eulerian** method. The continuous gas phase is solved on a fixed (Eulerian) grid, while the [dispersed phase](@entry_id:748551) is tracked as a large number of individual particles (Lagrangian). The [sub-grid models](@entry_id:755588) described above are applied to these Lagrangian particles.

#### The Computational Parcel

Tracking every single droplet in a real spray (which can number in the billions) is computationally prohibitive. Instead, the concept of a **computational parcel** is used. A parcel is a single computational entity that represents a group of $N_w$ physically identical droplets that share the same properties (size, velocity, temperature) and trajectory. $N_w$ is known as the **parcel weight**. The equations of motion, heat transfer, and [mass transfer](@entry_id:151080) are solved once for the parcel, and the result is assumed to apply to all $N_w$ droplets it represents. 

This approach is a form of a Monte Carlo method. While using parcels is an unbiased estimator of the mean behavior, it introduces statistical noise or variance. A fundamental trade-off exists: for a fixed total number of physical droplets being simulated, using larger parcel weights ($N_w$) reduces the number of parcels that must be tracked, thereby lowering the computational cost (cost $\propto 1/N_w$). However, this also increases the variance of the estimated source terms exchanged with the gas phase (variance $\propto N_w$). Choosing an appropriate number of parcels is therefore a critical balance between computational feasibility and statistical accuracy. 

#### Phase Coupling: Source Term Deposition

The two phases are not independent; they exchange mass, momentum, and energy. This [two-way coupling](@entry_id:178809) is achieved by calculating the source terms from the Lagrangian parcels (e.g., [mass loss](@entry_id:188886) from [evaporation](@entry_id:137264), momentum change from drag) and **depositing** them onto the Eulerian grid cells. This mapping from discrete particle locations to the grid is a critical step. 

Several **deposition** schemes exist, each with different properties regarding conservation and numerical accuracy:
-   **Nearest-Cell Deposition:** The entire source from a parcel is deposited into the single cell that contains the parcel's position. This is the simplest method and introduces the least [numerical diffusion](@entry_id:136300) (spreading), but it can cause artificial displacement of the source location, which may affect stability and accuracy.
-   **Volume-Weighted (Cloud-in-Cell) Deposition:** The source is distributed between the two (in 1D) or more bracketing cells based on the parcel's proximity to the cell centers. This linear interpolation scheme perfectly preserves the center of mass of the deposited source, avoiding artificial displacement. However, it introduces a small amount of numerical diffusion.
-   **Kernel-Based Deposition:** The source is distributed over several neighboring cells using a smooth, continuous kernel function (e.g., a Gaussian). This method provides smooth source fields, which is desirable for [numerical stability](@entry_id:146550), but it introduces the most numerical diffusion, effectively acting as a [low-pass filter](@entry_id:145200) on the source distribution.

When properly implemented, all these schemes are globally conservative, meaning the total amount of mass, momentum, and energy deposited on the grid exactly equals the total amount sourced from the parcels. The choice of scheme involves a trade-off between localization, smoothness, and [computational complexity](@entry_id:147058). 