## Introduction
The simultaneous flow of multiple phases—such as gas and liquid or liquid and solid—is a ubiquitous phenomenon in nature and industry, underpinning processes from oil and gas transport to steam generation in power plants. These multiphase flows do not mix arbitrarily; instead, they organize into distinct, recognizable patterns known as [flow regimes](@entry_id:152820). The specific regime, whether it be a tranquil [stratified flow](@entry_id:202356) or a violent [slug flow](@entry_id:151327), profoundly impacts critical engineering parameters like pressure drop, heat transfer, and structural integrity. The challenge, therefore, lies in moving beyond simple observation to develop a systematic framework for classifying and predicting these regimes based on fundamental principles. This is essential for the safe and efficient design and operation of any multiphase system.

This article provides a comprehensive guide to understanding and classifying [multiphase flow](@entry_id:146480) regimes. In the following chapters, you will embark on a structured journey through this complex topic. "Principles and Mechanisms" will lay the theoretical groundwork, exploring the fundamental forces and dimensionless numbers that govern the formation of different [flow patterns](@entry_id:153478). "Applications and Interdisciplinary Connections" will demonstrate the critical importance of this knowledge across various engineering disciplines and its connections to other scientific fields, from rheology to data science. Finally, "Hands-On Practices" will offer the opportunity to apply these concepts through targeted computational exercises, bridging theory with practical implementation.

## Principles and Mechanisms

The emergence of distinct [multiphase flow](@entry_id:146480) regimes is a direct consequence of the complex interplay between the constituent phases, the confining geometry, and the external forces acting upon the system. The specific pattern, or [morphology](@entry_id:273085), adopted by the flow is not arbitrary; rather, it represents a state of dynamic equilibrium that is governed by fundamental principles of mass, momentum, and [energy conservation](@entry_id:146975). Understanding the classification of these regimes requires moving beyond mere phenomenological description to a mechanistic analysis of the dominant forces at play. This chapter elucidates these underlying principles, providing a framework for predicting and interpreting the rich variety of structures observed in multiphase flows.

### Governing Forces and Key Dimensionless Parameters

The morphology of a [multiphase flow](@entry_id:146480) is determined by the competition between several fundamental forces. The relative importance of these forces can be quantified using dimensionless numbers, which are the cornerstones of flow regime analysis and mapping.

**Inertial Forces:** These forces are associated with the momentum of the fluid. A characteristic inertial stress in a flow with velocity $U$ and density $\rho$ scales as $\rho U^2$. Inertia acts to sustain the motion of the fluid and can be a primary driver of instabilities that deform interfaces.

**Gravitational Forces:** Gravity exerts a body force, $\rho \mathbf{g}$, on each phase. In multiphase systems, it is the difference in this [body force](@entry_id:184443), $(\rho_l - \rho_g)\mathbf{g}$, that gives rise to **[buoyancy](@entry_id:138985)**. Buoyancy acts to stratify fluids of different densities and to induce a [relative velocity](@entry_id:178060) (or slip) between them. The ratio of inertial to gravitational forces is captured by the **Froude number**, $Fr$:
$Fr = \dfrac{U}{\sqrt{gL}}$
where $L$ is a characteristic length scale (e.g., pipe diameter). A high $Fr$ indicates that the flow's inertia is dominant over gravitational effects.

**Surface Tension Forces:** At the interface between two immiscible fluids, cohesive molecular forces create surface tension, $\sigma$. Surface tension acts to minimize the interfacial surface area, creating a restoring force that resists deformation. The pressure jump across a curved interface, known as the capillary pressure, scales as $\sigma/L$. The competition between destabilizing inertial forces and stabilizing surface tension is quantified by the **Weber number**, $We$:
$We = \dfrac{\rho U^2 L}{\sigma}$
The Weber number is paramount in determining when bubbles or droplets will break apart. For instance, in an [annular flow](@entry_id:149763) where liquid droplets are entrained in a high-speed gas core, the breakup of these droplets is governed by the gas-phase Weber number, $We_g = \rho_g U_g^2 D / \sigma$, where $D$ is the droplet diameter. Breakup occurs when $We_g$ exceeds a critical value (typically of order 10), indicating that the aerodynamic pressure from the gas is sufficient to overcome the droplet's surface tension .

**Viscous Forces:** These forces arise from [fluid friction](@entry_id:268568) and resist motion. A characteristic [viscous stress](@entry_id:261328) scales as $\mu U/L$, where $\mu$ is the [dynamic viscosity](@entry_id:268228). The ratio of inertial to viscous forces is the familiar **Reynolds number**, $Re$:
$Re = \dfrac{\rho U L}{\mu}$
While $Re$ is critical for determining whether a single-phase flow is laminar or turbulent, in [multiphase flow](@entry_id:146480), its role is often secondary to the interfacial parameters, though it remains important in characterizing film flows and the drag on dispersed elements.

A final important parameter, particularly for static bubbles or droplets, is the **Eötvös number** (or Bond number), $Eo$, which compares gravitational forces to surface tension forces:
$Eo = \dfrac{\Delta\rho g L^2}{\sigma}$
The Eötvös number determines whether a dispersed element (bubble or droplet) will remain nearly spherical (dominated by surface tension) or become significantly deformed by buoyancy (dominated by gravity).

### The Decisive Role of Orientation: Vertical vs. Horizontal Flow

The direction of the gravity vector relative to the main flow axis fundamentally alters the nature of the force balance, leading to distinct sets of [flow regimes](@entry_id:152820) in vertical and horizontal pipes .

In **horizontal flow**, the gravitational [body force](@entry_id:184443) acts perpendicular (transversely) to the pipe axis. This transverse force drives stratification, pulling the denser phase toward the bottom of the pipe and allowing the lighter phase to rise to the top. This gives rise to gravity-dominated regimes such as **[stratified flow](@entry_id:202356)** (smooth or wavy) and **[plug flow](@entry_id:263994)** (elongated bubbles at the top of the pipe). The stability of these stratified layers against disruption by fluid inertia is governed by a Froude-type number.

In **vertical flow**, gravity acts parallel to the main flow axis. There is no transverse component to cause large-scale phase segregation across the pipe's cross-section. Instead, the axial [buoyancy force](@entry_id:154088) becomes the primary driver of the **slip velocity**—the difference in velocity between the gas and liquid phases. Consequently, the [flow regimes](@entry_id:152820) that develop tend to be more axisymmetric. A typical progression in vertical upward gas-liquid flow, with increasing gas velocity, is from [bubbly flow](@entry_id:151342), through slug and churn flow, to [annular flow](@entry_id:149763). The transitions between these regimes are governed by mechanisms like bubble coalescence and interfacial shear instabilities, which are influenced by parameters like the void fraction and Weber number .

### Canonical Regimes in Vertical Gas-Liquid Flow

Let us examine the characteristic progression of [flow regimes](@entry_id:152820) in a vertical pipe as the gas flow rate is increased for a fixed liquid flow rate.

#### Dispersed Flows: Bubbly and Mist Regimes

At low gas flow rates, the gas phase is dispersed as discrete bubbles within a continuous liquid phase, a regime known as **[bubbly flow](@entry_id:151342)**. At very high gas flow rates, the situation inverts, and liquid is dispersed as droplets in a continuous gas phase, known as **mist flow**. While both are "dispersed flows," their physics are dramatically different due to the reversal of the density ratio between the continuous ($c$) and dispersed ($d$) phases .

In **[bubbly flow](@entry_id:151342)**, the continuous phase (liquid) is much denser than the [dispersed phase](@entry_id:748551) (gas), i.e., $\rho_c \gg \rho_d$.
*   **Force Balance:** The dominant forces on a bubble are the upward [buoyancy force](@entry_id:154088), which scales with the liquid density ($\sim \rho_c g d^3$), and the downward drag force from the liquid. The bubble's own weight is negligible. The force required to accelerate the surrounding liquid out of the way (the **[added mass](@entry_id:267870)** force) is significant and scales with $\rho_c$, often dwarfing the bubble's own inertia which scales with $\rho_d$.
*   **Breakup:** Bubble breakup in turbulent flow is caused by inertial stresses in the surrounding liquid, so the relevant criterion is a Weber number based on the liquid density, $We_c = \rho_c U'^2 d / \sigma$, where $U'$ is a characteristic turbulent velocity fluctuation.

In **mist flow**, the continuous phase (gas) is much lighter than the [dispersed phase](@entry_id:748551) (liquid), i.e., $\rho_c \ll \rho_d$.
*   **Force Balance:** The dominant forces on a liquid droplet are its own weight, which is a downward [gravitational force](@entry_id:175476) scaling with the droplet density ($\sim \rho_d g d^3$), and the upward drag force from the gas. In this case, the [buoyancy](@entry_id:138985) from the displaced gas is negligible. The droplet's own inertia ($\sim \rho_d d^3$) is dominant, and the [added mass effect](@entry_id:269884) from the surrounding gas is negligible.
*   **Breakup:** Droplet breakup is caused by the high relative velocity between the droplet and the fast-moving gas. The deforming force is the aerodynamic pressure from the gas, so the relevant criterion is a Weber number based on the gas density, $We_c = \rho_c U_{rel}^2 d / \sigma$.
*   **Coalescence:** In turbulent mist flow, droplet coalescence may be suppressed. The [collision time](@entry_id:261390) can be very short compared to the time required to drain the thin gas film between droplets, causing them to rebound instead of merging .

This comparison underscores a critical principle: the physics of a dispersed flow are dictated not just by its morphology, but by the density ratio of the phases.

#### Intermittent Flows: Plug and Slug Regimes

As the gas flow rate in [bubbly flow](@entry_id:151342) increases, bubbles begin to coalesce into larger, bullet-shaped bubbles known as **Taylor bubbles**. These bubbles span a significant portion of the pipe diameter and mark the onset of the **intermittent flow** regime. A key distinction exists within this regime between [plug flow](@entry_id:263994) and [slug flow](@entry_id:151327) .

**Plug flow** (also called Taylor bubble flow) occurs at the initial stages of [intermittency](@entry_id:275330). It is characterized by:
*   **Bubble Length:** The Taylor bubbles are well-defined and relatively short, with a length-to-diameter ratio ($L_b/D$) of order unity to perhaps ten.
*   **Liquid Slugs:** The liquid slugs separating the Taylor bubbles are largely quiescent and contain very few small dispersed bubbles. A thin, lubricating film of liquid separates the Taylor bubble from the pipe wall.
*   **Pressure Fluctuations:** The passage of these regular bubble-slug units creates quasi-periodic pressure fluctuations of moderate amplitude and relatively high frequency.

**Slug flow** develops at higher gas and/or liquid flow rates. It is a more chaotic and violent regime characterized by:
*   **Bubble Length:** Coalescence leads to very long and often distorted Taylor bubbles, with $L_b/D \gg 1$.
*   **Liquid Slugs:** The liquid slugs are no longer quiescent but are highly turbulent and frothy, containing a significant volume of smaller dispersed bubbles. This aeration lowers the effective density of the slug.
*   **Pressure Fluctuations:** The passage of the very long gas bubbles and the heavy, churning liquid slugs produces large-amplitude, intermittent pressure surges at a much lower characteristic frequency than in [plug flow](@entry_id:263994) .

#### Transitional and Separated Flows: Churn and Annular Regimes

At even higher gas flow rates, the integrity of the liquid slugs breaks down completely. This leads to **churn flow**, a highly chaotic and oscillatory transitional regime. It is characterized by the collapse of liquid slugs, with liquid seen to fall downwards against the main flow direction, and large, unstable gas structures. The underlying mechanism can be viewed as the extreme nonlinear growth and [coalescence](@entry_id:147963) of interfacial waves on the liquid films separating the gas pockets .

Finally, at the highest gas flow rates, the flow reorganizes into **[annular flow](@entry_id:149763)**. Here, the gas forms a continuous, high-velocity core in the center of the pipe, while the liquid flows as a slower film along the pipe wall. A significant feature of this regime is the shearing of waves from the liquid film by the fast gas core, which generates a mist of entrained liquid droplets that are carried in the core. As discussed previously, the stability and size of these droplets are governed by the gas-phase Weber number .

### Macroscopic Descriptors of Flow Regimes

The physical changes across these regimes are reflected in key macroscopic parameters that can be measured or calculated. Analyzing their trends provides deep insight into the underlying mechanisms .

**Void Fraction ($\alpha$)**: Defined as the volume fraction occupied by the gas, the void fraction is the most fundamental descriptor. As the gas mass flux is progressively increased at a constant liquid flux, more volume must be made available for the gas. Consequently, the void fraction $\alpha$ **increases monotonically** through the bubbly-slug-churn-annular progression.

**Interfacial Area Concentration ($a_i$)**: This parameter, defined as the total interfacial area per unit volume, exhibits a complex, **non-monotonic behavior**.
*   It is often highest in a **finely dispersed [bubbly flow](@entry_id:151342)**, where a large number of very small bubbles creates an immense surface area (since $a_i \sim \alpha/d_b$ for bubbles of diameter $d_b$).
*   As the flow transitions to the **slug and churn regimes**, [coalescence](@entry_id:147963) dominates. The merging of small bubbles into large Taylor bubbles drastically reduces the total surface area for a given gas volume. Thus, $a_i$ drops significantly.
*   In the **annular regime**, the interfacial area consists of the large surface of the gas core-liquid film interface plus the surface area of all entrained droplets. This typically results in an intermediate value of $a_i$, higher than in churn flow but lower than the peak achieved in finely dispersed [bubbly flow](@entry_id:151342) .

**Slip Ratio ($S = U_g/U_l$)**: The ratio of the actual average gas velocity ($U_g$) to the actual average liquid velocity ($U_l$) also **increases monotonically** with gas flow rate, but for different reasons in different regimes .
*   In **[bubbly flow](@entry_id:151342)**, slip arises because individual bubbles rise due to [buoyancy](@entry_id:138985) faster than the surrounding liquid. The slip velocity ($U_g - U_l$) is determined by a balance of [buoyancy](@entry_id:138985) and drag. As the void fraction $\alpha$ increases, hydrodynamic hindrance from the bubble swarm increases the effective drag, which tends to reduce the slip velocity and thus the [slip ratio](@entry_id:201243) for a fixed liquid velocity.
*   In **slug and churn flow**, the large Taylor bubbles have a much higher rise velocity than small bubbles due to their large volume-to-surface area ratio, leading to a significant increase in $S$.
*   In **[annular flow](@entry_id:149763)**, the [slip ratio](@entry_id:201243) reaches very high values. The fast-moving gas core is driven by the axial pressure gradient, while the [liquid film](@entry_id:260769) is slowed dramatically by shear at the pipe wall. As the film thins with increasing $\alpha$, its [average velocity](@entry_id:267649) $U_l$ decreases, causing the [slip ratio](@entry_id:201243) $S = U_g/U_l$ to increase sharply .

### From Principles to Practice: Flow Regime Maps

To be practically useful, this knowledge must be organized into a predictive tool. This is the purpose of a **flow regime map**, which graphically delineates the boundaries between different regimes in a parameter space.

A robust and universal map must be constructed using appropriate coordinates. The most logical axes for a map are the externally controllable variables, which for [pipe flow](@entry_id:189531) are typically the **superficial velocities** of the phases, $J_g$ and $J_l$. The [superficial velocity](@entry_id:152020), $J_k$, is the [volumetric flow rate](@entry_id:265771) of phase $k$ divided by the total pipe cross-sectional area. It is related to the actual velocity $U_k$ and phase fraction $\alpha_k$ by $J_k = \alpha_k U_k$. Using $J_g$ and $J_l$ as axes avoids the circularity of using [dependent variables](@entry_id:267817) like $U_k$ or $\alpha_k$, which are themselves outcomes of the flow regime .

To make the map applicable across different pipe scales and fluid properties, the boundaries should be expressed in terms of the [dimensionless parameters](@entry_id:180651) that govern the transitions. For instance, the transition from stratified to [slug flow](@entry_id:151327) in horizontal pipes involves the competition of inertia and gravity, and is thus described by a critical Froude number. The onset of droplet [entrainment](@entry_id:275487) in [annular flow](@entry_id:149763) is governed by a critical Weber number. Therefore, a truly universal classification framework involves plotting regime boundaries in a space defined by the superficial velocities, where the boundaries themselves are functions of the relevant [dimensionless groups](@entry_id:156314) like the Froude and Weber numbers based on mixture properties .

### Broader Applications: The Case of Gas-Solid Fluidization

The fundamental approach of classifying regimes based on competing forces is universally applicable. Consider a **gas-solid [fluidized bed](@entry_id:191273)**, where a gas flows upward through a bed of solid particles. The resulting behavior is famously categorized by the **Geldart classification**, which maps particle properties (primarily size $d_p$ and density difference $\rho_p - \rho_g$) to [fluidization](@entry_id:192588) regimes .

*   **Group C (Cohesive):** For very fine particles ($d_p  \sim 30 \, \mu\mathrm{m}$), attractive interparticle forces (e.g., van der Waals) dominate hydrodynamic forces. The gas tends to form channels through the powder rather than fluidizing it uniformly.
*   **Group A (Aeratable):** For fine particles ($30 \, \mu\mathrm{m}  d_p  150 \, \mu\mathrm{m}$), the bed first expands smoothly and uniformly (particulate [fluidization](@entry_id:192588)) after the [minimum fluidization velocity](@entry_id:189057) is exceeded. Bubbles only form at a higher gas velocity.
*   **Group B (Bubbling):** For intermediate particles ($150 \, \mu\mathrm{m}  d_p  1000 \, \mu\mathrm{m}$), hydrodynamic and gravitational forces are dominant. Bubbles form as soon as the bed is fluidized and coalesce vigorously as they rise.
*   **Group D (Spoutable):** For large, dense particles ($d_p > 1000 \, \mu\mathrm{m}$), a very high gas velocity is required. The gas momentum tends to form a stable central jet, leading to a spouting regime rather than bubbling.

The Geldart chart is a perfect example of a regime map derived from balancing particle-level forces: gravity, drag, and [cohesion](@entry_id:188479). It reinforces the central theme that the diverse and complex macroscopic structures of [multiphase flow](@entry_id:146480) are deterministic outcomes of the competition between a handful of fundamental physical forces.