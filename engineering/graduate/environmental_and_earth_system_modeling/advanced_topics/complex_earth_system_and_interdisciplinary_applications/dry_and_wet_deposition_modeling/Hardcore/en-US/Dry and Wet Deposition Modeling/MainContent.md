## Introduction
The removal of trace gases and aerosols from the atmosphere is a fundamental process that governs air quality, dictates the lifetime of pollutants, and links atmospheric composition to the health of terrestrial and aquatic ecosystems. This removal occurs through two primary pathways: dry deposition, the continuous transfer to surfaces in the absence of precipitation, and wet deposition, the scavenging by rain, snow, and fog. Understanding and quantifying these processes is essential for accurately simulating the Earth system, from local air pollution episodes to [global biogeochemical cycles](@entry_id:149408).

However, the mechanisms governing deposition are complex, spanning micro-scale physics, chemistry, and biology. The central challenge for environmental modelers is to represent these intricate processes in a computationally efficient yet physically robust manner. This article addresses this challenge by providing a comprehensive overview of the theoretical frameworks used to model dry and wet deposition.

Across the following chapters, you will gain a deep understanding of deposition modeling. The first chapter, **"Principles and Mechanisms,"** lays the theoretical groundwork, introducing the core concepts of [deposition velocity](@entry_id:1123566), the resistance-in-series analogy, and the physics of particle and gas scavenging. The second chapter, **"Applications and Interdisciplinary Connections,"** explores how these principles are implemented in state-of-the-art [atmospheric models](@entry_id:1121200) and demonstrates their critical role in linking atmospheric science with [biogeochemistry](@entry_id:152189), [cryospheric science](@entry_id:1123256), and paleoclimate studies. Finally, the **"Hands-On Practices"** section will allow you to apply these concepts through practical exercises, solidifying your ability to work with and interpret deposition models. We begin by examining the fundamental principles that form the foundation of this crucial field.

## Principles and Mechanisms

### The Fundamentals of Dry Deposition

The removal of pollutants from the atmosphere in the absence of precipitation, known as **dry deposition**, is a continuous process governing the transfer of gases and particles from the air to the Earth's surface. To quantify this process, we must establish a framework that links the rate of removal to the concentration of the substance in the atmosphere.

#### The Deposition Velocity Concept

Consider a trace gas or aerosol species with a mean concentration $C(z_r)$ at a reference height $z_r$ within the [atmospheric surface layer](@entry_id:1121210). The downward vertical flux of this substance to the surface, denoted as $F_d$, is observed to be proportional to this concentration. We can therefore define a proportionality factor, the **[deposition velocity](@entry_id:1123566)** $V_d$, which parameterizes this relationship. Adopting the convention that a downward flux is positive, the defining equation is:

$$F_d = V_d C(z_r)$$

From this definition, the physical dimensions of $V_d$ can be deduced. With flux $F_d$ having units of mass per area per time (e.g., $\mathrm{kg} \cdot \mathrm{m}^{-2} \cdot \mathrm{s}^{-1}$) and concentration $C(z_r)$ having units of mass per volume (e.g., $\mathrm{kg} \cdot \mathrm{m}^{-3}$), the units of $V_d$ are length per time ($\mathrm{m} \cdot \mathrm{s}^{-1}$). While dimensionally a velocity, $V_d$ is not a true physical velocity of a particle or molecule. Instead, it is a **bulk mass-transfer coefficient** that encapsulates all the complex processes responsible for transporting a substance from the reference height down to the surface, where it is ultimately captured or absorbed .

It is crucial to distinguish this bulk parameterization from the local, gradient-based description of turbulent transport. Within the [atmospheric surface layer](@entry_id:1121210), the turbulent flux $J_t$ at any height $z$ can be described by first-order closure (or K-theory) as:

$$J_t(z) = -K(z) \frac{\mathrm{d}C}{\mathrm{d}z}$$

where $K(z)$ is the **eddy diffusivity**, representing the efficiency of turbulent mixing at that height. Under steady-state and horizontally homogeneous conditions, the mass conservation equation simplifies to show that the vertical flux is constant with height (the "constant-flux layer"). Therefore, the surface deposition flux $F_d$ is numerically equal to the [turbulent flux](@entry_id:1133512) $J_t(z)$ at any height $z$ within this layer. However, their conceptual foundations differ: $F_d = V_d C(z_r)$ is a parameterization of a boundary flux using a concentration far from the boundary, while $J_t(z) = -K(z) \frac{\mathrm{d}C}{\mathrm{d}z}$ is a local relationship between flux and the concentration gradient at a specific point in the fluid . The power of the [deposition velocity](@entry_id:1123566) concept lies in its ability to represent the integrated effect of the entire transport pathway in a single, measurable parameter.

### The Resistance-in-Series Model for Gas Deposition

A powerful analogy for conceptualizing the processes encapsulated by $V_d$ is that of an electrical circuit. In this framework, the flux $F_d$ is analogous to current, the concentration difference between the reference height and the surface is the [potential difference](@entry_id:275724) (voltage), and the opposition to transport is represented by a series of resistances. The [deposition velocity](@entry_id:1123566) is then the inverse of the total resistance, $R_{total}$:

$$V_d = \frac{1}{R_{total}}$$

For the deposition of gases, this total resistance is commonly partitioned into three primary components acting in series: the aerodynamic resistance ($R_a$), the quasi-laminar boundary layer resistance ($R_b$), and the surface or [canopy resistance](@entry_id:1122022) ($R_c$).

$$R_{total} = R_a + R_b + R_c$$

This model provides a mechanistic basis for understanding how different physical and biogeochemical factors control the overall rate of deposition  .

#### Aerodynamic Resistance ($R_a$)

The **aerodynamic resistance**, $R_a$, represents the resistance to turbulent transport from the reference height $z_r$ down to the effective "surface" of the roughness elements (e.g., the top of a forest canopy). This transport is governed by the physics of the [atmospheric surface layer](@entry_id:1121210), which is well-described by **Monin-Obukhov Similarity Theory (MOST)**. MOST introduces three fundamental scaling parameters that govern the turbulence structure :

1.  **Friction Velocity ($u_*$)**: Defined from the surface shear stress $\tau_0$ and air density $\rho$ as $u_* = \sqrt{\tau_0 / \rho}$, $u_*$ is the characteristic velocity scale of near-surface turbulence. It quantifies the intensity of mechanically generated eddies.
2.  **Roughness Length ($z_0$)**: An extrinsic property of the surface itself, $z_0$ is the height at which the extrapolated [logarithmic wind profile](@entry_id:1127429) under neutral conditions goes to zero. It parameterizes the surface's ability to extract momentum from the flow and is an aggregate measure of the size, shape, and density of roughness elements.
3.  **Obukhov Length ($L$)**: A length scale that quantifies the relative importance of buoyant (thermal) production of turbulence to mechanical (shear) production. $L$ is negative in unstable (convective) conditions, positive in stable (stratified) conditions, and infinite in neutral conditions. The dimensionless ratio $z/L$ is the key parameter that characterizes atmospheric stability.

The aerodynamic resistance $R_a$ is primarily a function of these three parameters. It is inversely proportional to the friction velocity $u_*$—stronger winds and more intense turbulence lead to more efficient mixing and a lower $R_a$. The value of $R_a$ is modulated by [atmospheric stability](@entry_id:267207) through functions of $z/L$. Crucially, because turbulent transport involves the movement of macroscopic air parcels, $R_a$ is largely insensitive to the molecular properties of the diffusing gas .

#### Quasi-laminar Boundary Layer Resistance ($R_b$)

As a gas molecule approaches a surface element like a leaf or soil particle, it must traverse a very thin layer of air where turbulent motions are suppressed by viscosity. In this **quasi-laminar boundary layer**, transport is dominated by slow molecular diffusion. The resistance of this layer is the **quasi-[laminar boundary layer](@entry_id:153016) resistance**, $R_b$.

The thickness of this layer is inversely related to the intensity of the overlying turbulence; thus, $R_b$ decreases as $u_*$ increases. Unlike $R_a$, $R_b$ is strongly dependent on the molecular properties of the gas. This dependence is typically expressed through the **Schmidt number ($Sc$)**, which is the ratio of the kinematic viscosity of air to the molecular diffusivity of the gas, $D_g$. Semi-empirical relationships, drawing analogies from heat transfer, often show that $R_b$ scales with a power of the Schmidt number, for instance, $R_b \propto Sc^{2/3}$ .

#### Canopy Resistance ($R_c$)

The final step in the deposition process is the actual uptake or destruction of the gas molecule at the surface. The **canopy resistance**, $R_c$, represents the limitation imposed by these surface processes. Since a gas can be taken up by multiple surfaces simultaneously (e.g., through [plant stomata](@entry_id:153552), onto the leaf cuticle, or by the soil), $R_c$ is best modeled as a combination of several resistances acting in **parallel**. The total surface conductance ($1/R_c$) is the sum of the individual pathway conductances :

$$\frac{1}{R_c} = \frac{1}{R_s} + \frac{1}{R_{cut}} + \frac{1}{R_{soil}} + \dots$$

where $R_s$, $R_{cut}$, and $R_{soil}$ are the stomatal, cuticular, and soil resistances, respectively.

The relative importance of these pathways depends critically on the gas's physicochemical properties and the prevailing environmental conditions. Consider the contrasting deposition of ozone ($\mathrm{O}_3$) and ammonia ($\mathrm{NH}_3$) to a wet, acidic forest canopy at midday :
-   **Ozone ($\mathrm{O}_3$)**: As a highly reactive but only moderately soluble gas, its primary uptake pathway is through open stomata ($R_s$ is low), where it rapidly reacts with internal cell structures. Uptake by the wet leaf cuticle ($R_{cut}$) provides a secondary path. Therefore, stomatal uptake dominates.
-   **Ammonia ($\mathrm{NH}_3$)**: As a highly soluble base, its behavior is different. On a wet, acidic leaf surface ($pH  7$), $\mathrm{NH}_3$ rapidly dissolves and is neutralized to the non-volatile ammonium ion ($\mathrm{NH}_4^+$). This chemical trapping makes the cuticular pathway extremely efficient, resulting in a very low $R_{cut}$. Stomatal exchange, in contrast, may be negligible or even reversed (outgassing) if the internal plant concentration exceeds the ambient air concentration. Thus, for $\mathrm{NH}_3$ under these conditions, non-stomatal uptake by the wet cuticle is the dominant deposition pathway.

### The Diurnal Cycle of Dry Deposition

The interplay between atmospheric stability and surface physiology, as described by the resistance model, leads to a pronounced diurnal cycle in the [deposition velocity](@entry_id:1123566), particularly for gases whose uptake is regulated by [stomata](@entry_id:145015).

During the **daytime** over land, solar radiation warms the surface, creating unstable atmospheric conditions ($L  0$). This buoyant production of turbulence enhances mixing, leading to low aerodynamic ($R_a$) and quasi-laminar ($R_b$) resistances. Concurrently, sunlight drives photosynthesis, causing [plant stomata](@entry_id:153552) to open, which results in a low surface resistance ($R_s$). With all three resistances being low, the total resistance is minimized, and the [deposition velocity](@entry_id:1123566) $V_d$ reaches its maximum. For a gas like ozone over a temperate forest, typical daytime $V_d$ values are in the range of $0.003$–$0.010 \ \mathrm{m \ s^{-1}}$ ($0.3$–$1.0 \ \mathrm{cm \ s^{-1}}$) .

During the **nighttime**, the surface cools via longwave radiation, leading to stable atmospheric conditions ($L  0$). This [thermal stratification](@entry_id:184667) suppresses turbulence, increasing both $R_a$ and $R_b$. In the absence of light, [stomata](@entry_id:145015) close, causing $R_s$ to become very large. The combination of high transport resistance and high surface resistance leads to a much lower [deposition velocity](@entry_id:1123566). Typical nighttime $V_d$ values for ozone drop to $0.0001$–$0.002 \ \mathrm{m \ s^{-1}}$ ($0.01$–$0.2 \ \mathrm{cm \ s^{-1}}$) .

### Bidirectional Exchange and the Compensation Point

For some compounds, such as ammonia ($\mathrm{NH}_3$), the surface is not always a perfect sink. Biological processes within plants and soils can produce the compound, leading to an internal concentration. If this internal concentration is high enough, the net flux can be directed from the surface to the atmosphere (emission). This phenomenon is termed **bidirectional exchange**.

In this case, the simple resistance model must be modified to include an internal potential concentration, $C^*$. The flux is then driven by the difference between the ambient concentration $C_a$ and this internal potential, divided by the total resistance:

$$F = \frac{C_a - C^*}{R_a + R_b + R_c}$$

A key concept in this framework is the **compensation point ($C_{comp}$)**, defined as the ambient concentration $C_a$ at which the net flux $F$ is zero. In the simple model above, setting $F=0$ directly implies that $C_{comp} = C^*$. At ambient concentrations above the compensation point, deposition occurs; below it, emission occurs .

The reality can be more complex if multiple surface pathways exist with different internal concentrations. For instance, if ammonia exchange occurs via a stomatal pathway (resistance $R_s$, potential $C^*$) in parallel with an irreversible cuticular sink (resistance $R_{cut}$, potential $0$), the overall system compensation point is no longer equal to $C^*$. At net zero flux, the depositional flux to the cuticle must exactly balance the emissive flux from the [stomata](@entry_id:145015). This equilibrium results in a compensation point given by:

$$C_{comp} = \frac{C^*}{1 + R_s/R_{cut}}$$

This demonstrates that the presence of an efficient, irreversible deposition pathway can lower the ambient concentration at which the canopy as a whole switches from a net source to a net sink .

### Mechanisms of Particle Dry Deposition

The dry deposition of aerosol particles is also governed by transport through the aerodynamic and quasi-laminar layers. However, the final capture at the surface is a physical process, not a biochemical one. The concept of [surface resistance](@entry_id:149810) is replaced by a set of collection mechanisms whose efficiencies are strongly dependent on particle size, $d_p$. The key mechanisms are :

-   **Brownian Diffusion**: The random thermal motion of air molecules causes very small particles (ultrafine particles, $d_p \lesssim 0.1 \ \mathrm{\mu m}$) to diffuse across the quasi-laminar layer to the surface. The efficiency of this process increases dramatically as particle size decreases ([deposition velocity](@entry_id:1123566) scales roughly as $d_p^{-1}$ to $d_p^{-2}$).
-   **Gravitational Settling**: All particles are subject to gravity, which induces a downward [terminal velocity](@entry_id:147799). This process is negligible for small particles but becomes significant for coarse particles ($d_p \gtrsim 2.5 \ \mathrm{\mu m}$), with a contribution to [deposition velocity](@entry_id:1123566) scaling as $d_p^2$.
-   **Inertial Impaction**: Larger particles have sufficient inertia that they cannot follow the curving [streamlines](@entry_id:266815) of air flowing around a collector (like a leaf or needle). They continue in a straighter path and impact the surface. This mechanism is most effective for coarse particles in high winds, and its contribution also scales strongly with particle size (e.g., as $d_p^2$).
-   **Interception**: This occurs when a particle, even while following an air [streamline](@entry_id:272773), comes into contact with a surface element simply due to its finite size. Its contribution to [deposition velocity](@entry_id:1123566) scales approximately with $d_p$.

The combined effect of these mechanisms results in a characteristic "U-shaped" curve when $V_d$ is plotted against particle diameter on a logarithmic scale. Deposition is efficient for ultrafine particles (dominated by diffusion) and for coarse particles (dominated by settling and impaction). It is least efficient for particles in the intermediate **accumulation mode** (roughly $0.1 \ \mathrm{\mu m}  d_p  2.5 \ \mathrm{\mu m}$), where none of the mechanisms are particularly effective. Increasing surface roughness ($z_0$) and turbulence ($u_*$) enhances deposition for all particle sizes by thinning the quasi-laminar layer and increasing collision rates with surface elements .

### Principles of Wet Deposition

Wet deposition is the removal of atmospheric substances by precipitation, including rain, snow, and fog. The underlying processes can be divided into two main categories: in-cloud scavenging and below-cloud scavenging.

#### In-Cloud vs. Below-Cloud Scavenging

**In-cloud scavenging**, also known as **rainout**, involves the incorporation of gases and particles into cloud droplets that later form precipitation. This can occur through gases dissolving into the droplets or through aerosol particles acting as [cloud condensation nuclei](@entry_id:1122511) (CCN).

**Below-cloud scavenging**, or **washout**, is the removal of gases and aerosols from the air below a cloud by falling hydrometeors (raindrops, snowflakes).

For many pollutants, the distinction between these two pathways is critical for determining the overall efficiency of wet removal .

#### Wet Scavenging of Soluble Gases

The dominant wet deposition pathway for a gas is determined by its partitioning between the gas and aqueous phases, which is governed by **Henry's Law**. For a gas with concentration $C_g$ in the air, its equilibrium concentration $C_l$ in a cloud droplet is given by $C_l = H C_g$, where $H$ is the Henry's Law constant.

Within a cloud, we can calculate the fraction of the total pollutant mass that resides in the liquid phase, $f_l$. This fraction depends on $H$ and the cloud liquid water volume fraction, $\phi_l$:

$$f_l = \frac{H \phi_l}{1 + H \phi_l}$$

For a highly soluble gas (large $H$), the term $H \phi_l$ can be much greater than 1. In this limit, $f_l$ approaches 1. This means that virtually the entire mass of the pollutant is dissolved within the cloud droplets. Consequently, when these droplets are removed from the atmosphere as precipitation, the removal of the pollutant is extremely efficient. Rainout is therefore the dominant wet deposition mechanism for highly soluble gases like [nitric acid](@entry_id:153836) ($\mathrm{HNO}_3$) or [sulfur dioxide](@entry_id:149582) ($\mathrm{SO}_2$). Washout is comparatively insignificant because very little mass remains in the gas phase below the cloud for raindrops to scavenge .

#### Wet Scavenging of Aerosols

The below-cloud scavenging (washout) of aerosol particles by falling raindrops is typically modeled as a first-order loss process. The rate of change of the aerosol concentration $C$ is given by:

$$\frac{\mathrm{d}C}{\mathrm{d}t} = -\Lambda C$$

where $\Lambda$ is the **scavenging coefficient**, with units of inverse time (e.g., $\mathrm{s}^{-1}$). This coefficient can be derived from microphysical principles. The rate of removal is found by integrating the collection of aerosol particles by raindrops over the entire raindrop size distribution. This leads to a complex integral expression for $\Lambda$.

For practical applications, $\Lambda$ is often parameterized as being proportional to the precipitation rate (rainfall intensity) $P$:

$$\Lambda = \beta P$$

The proportionality factor $\beta$ can be derived by taking the ratio of the full integral expressions for $\Lambda$ and $P$. The result shows that $\beta$ is a spectrally-averaged collection efficiency, depending on the raindrop size distribution $n(D)$, fall velocity $v(D)$, and the collection efficiency $E(D, d_p)$ for a drop of diameter $D$ collecting a particle of diameter $d_p$ :

$$\beta = \frac{3}{2} \frac{\int_0^\infty n(D) v(D) E(D,d_p) D^2 \mathrm{d}D}{\int_0^\infty n(D) v(D) D^3 \mathrm{d}D}$$

This relationship forms the basis for modeling aerosol washout in many large-scale atmospheric transport models, linking a microphysical process to a macroscopic meteorological variable.