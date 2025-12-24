## Introduction
In the realm of [numerical weather prediction](@entry_id:191656) and climate modeling, a fundamental challenge lies in representing the vast diversity of the Earth's surface. A single model grid cell, often spanning tens or hundreds of kilometers, can contain a complex mosaic of forests, croplands, cities, and water bodies. How can a model capture the unique interactions of each surface type with the atmosphere without being overwhelmed by complexity? Simply averaging the properties of the landscape leads to significant, [systematic errors](@entry_id:755765) in predicting water and energy fluxes, a critical knowledge gap that modern Earth System Models must address.

This article provides a comprehensive overview of the two key methods used to solve this problem: [surface heterogeneity tiling](@entry_id:1132679) and river routing. We will explore how these techniques allow models to simulate a complex world with fidelity and [computational efficiency](@entry_id:270255). The following chapters will guide you through this essential topic. "Principles and Mechanisms" delves into the theoretical basis for tiling, explaining why averaging fails and detailing the physical and numerical frameworks for calculating tile-specific budgets and routing water through river networks. "Applications and Interdisciplinary Connections" showcases how these methods are applied to real-world problems, from urban [flood forecasting](@entry_id:1125087) to understanding the effects of land-use change. Finally, "Hands-On Practices" offers practical exercises to solidify your understanding of these critical modeling concepts.

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms governing the representation of [surface heterogeneity](@entry_id:180832) and river routing in modern Earth System Models (ESMs). We will explore the fundamental reasons for adopting subgrid-scale parameterizations, the formal structure of the "tiling" or "mosaic" approach, the physical processes resolved within each tile, and the methods used to transport water across the model's landscape through river networks.

### The Rationale for Tiling: The Fallacy of Averaged States

Atmospheric models, which provide the forcing for land surface processes, operate on spatial grids with resolutions typically ranging from tens to hundreds of kilometers. Within a single grid cell, however, the land surface can be immensely heterogeneous, comprising a mosaic of forests, croplands, urban areas, water bodies, and bare soils. Each of these surfaces interacts with the atmosphere in a unique and often highly nonlinear fashion.

A critical question thus arises: can we represent the net effect of this subgrid heterogeneity by first averaging the surface properties (like soil moisture or temperature) and then computing a single grid-cell-averaged flux? The answer, in general, is no. This is due to the nonlinear nature of the functions that describe land-atmosphere exchanges.

Consider the process of evapotranspiration, which is often limited by soil moisture availability. A common parameterization relates the flux $E$ to the volumetric soil water content $\theta$ through a nonlinear stress function. For instance, the flux might be zero below a wilting point ($\theta_w$), increase nonlinearly to a potential rate as moisture increases to field capacity ($\theta_{fc}$), and remain constant thereafter. Let's examine a hypothetical scenario with a convex stress function, such as $E(\theta) \propto ((\theta - \theta_w)/(\theta_{fc} - \theta_w))^\beta$ for $\beta > 1$ . Imagine a grid cell composed of two equal-area tiles: one is very dry, at the wilting point ($\theta_1 = \theta_w = 0.1$), and the other is very wet, at field capacity ($\theta_2 = \theta_{fc} = 0.4$).

The "flux of the average" approach would first compute the average soil moisture, $\bar{\theta} = 0.5 \times (0.1 + 0.4) = 0.25$. The corresponding flux, $E(\bar{\theta})$, would be some intermediate value, as the average soil moisture is halfway between wilting and capacity.

The "average of the fluxes" approach, however, calculates the flux for each tile first. The dry tile produces zero flux, $E(\theta_1) = 0$, while the wet tile evaporates at its potential rate, $E(\theta_2) = E_{pot}$. The correct area-averaged flux for the grid cell is therefore $\bar{E} = 0.5 \times (0 + E_{pot}) = 0.5 E_{pot}$. Due to the convexity of the [response function](@entry_id:138845), the flux computed from the average state is significantly lower than the true average flux. This mathematical reality, an example of **Jensen's inequality**, demonstrates that averaging state variables before calculating nonlinear fluxes leads to systematic biases.

This principle applies to numerous surface processes, including [runoff generation](@entry_id:1131147). Infiltration-excess runoff often occurs only when soil moisture $S$ exceeds a critical threshold $S_c$. A parameterization might take a convex form like $Q(S) \propto (S - S_c)^2$ for $S > S_c$ . If a grid cell contains some patches of soil that are saturated ($S > S_c$) and some that are dry ($S  S_c$), the saturated patches will generate runoff. However, if the area-averaged soil moisture $\bar{S}$ is below the threshold $S_c$, the model would erroneously calculate zero runoff for the entire grid cell. The correct approach—averaging the runoff computed from each individual patch—captures the localized [runoff generation](@entry_id:1131147) that is missed by the aggregated-state method.

### The Tiling Approach: A Formal Framework for Subgrid Heterogeneity

To overcome the pitfalls of averaging state variables, modern Land Surface Models (LSMs) employ a **[surface heterogeneity tiling](@entry_id:1132679)** scheme, often called a **mosaic** approach. This framework provides a structured way to account for subgrid variability while maintaining computational feasibility.

The core components of this framework are defined as follows :

1.  **Atmospheric Grid Cell**: This is the fundamental computational unit of the atmospheric model. It is the scale at which atmospheric forcings (e.g., precipitation $P$, downward radiation $S^\downarrow$, wind speed $\mathbf{U}$) are provided to the land surface, and it is the scale at which the land must return aggregated surface fluxes (e.g., sensible heat $H$, latent heat $\lambda E$) to the atmosphere.

2.  **Land Surface Tile**: A tile is a subgrid, non-overlapping fractional area within a single atmospheric grid cell. Each tile is assumed to be internally homogeneous, characterized by a single set of land surface properties (e.g., vegetation type, soil texture, albedo) and a corresponding set of prognostic [state variables](@entry_id:138790) (e.g., soil moisture, surface temperature). All physical calculations of water and energy balance are performed independently for each tile.

The grid cell is partitioned into $n$ tiles, with each tile $i$ occupying a fractional area $a_i$, where $a_i > 0$ and $\sum_{i=1}^n a_i = 1$. The model operates by taking the grid-cell scale atmospheric forcings and applying them to each tile. Each tile then computes its own surface fluxes and changes in state based on its unique parameters and current state.

To provide feedback to the atmospheric model, these tile-specific fluxes must be aggregated back to the grid-cell scale. This is achieved through **area-weighted averaging**. For any intensive flux quantity $\mathcal{F}$ (a flux per unit area, such as $\mathrm{W\,m^{-2}}$ or $\mathrm{mm\,day^{-1}}$), the effective grid-cell flux $\mathcal{F}_{\text{grid}}$ is calculated as:

$$
\mathcal{F}_{\text{grid}} = \sum_{i=1}^n a_i \mathcal{F}_i
$$

This linear aggregation of fluxes, performed *after* the nonlinear physical calculations on each tile, ensures that extensive quantities like total water mass and energy are conserved across the grid cell. For example, the total volume of water evaporated from a grid cell of area $A$ is $A \times \mathcal{F}_{\text{grid}} = A \sum a_i \mathcal{F}_i = \sum (a_i A) \mathcal{F}_i$, which is precisely the sum of the water volumes evaporated from the physical area of each tile.

This same principle applies to energy balance closure. If initial calculations result in an energy imbalance for each tile, a correction can be applied to preserve the grid-cell energy budget. A common method is to calculate the grid-averaged available energy, $A_{\text{grid}} = \sum a_i (R_{n,i} - G_i)$, and the initial grid-averaged total [turbulent flux](@entry_id:1133512), $(H+\lambda E)_{\text{grid}}^{(0)} = \sum a_i (H_i^{(0)} + \lambda E_i^{(0)})$. A single correction factor $c = A_{\text{grid}} / (H+\lambda E)_{\text{grid}}^{(0)}$ can then be multiplied by the initial turbulent fluxes of each tile, ensuring the final aggregated fluxes close the energy budget while preserving properties like the Bowen ratio on each tile .

Similarly, the effective albedo $\alpha$ of a grid cell is, to a first approximation, the area-weighted average of the tile albedos $\alpha_i$ :

$$
\alpha = \sum_{i=1}^n a_i \alpha_i
$$

This [linear mixing model](@entry_id:895469) is valid under the assumption that there are no lateral radiative interactions between tiles. In reality, particularly where surfaces with highly contrasting albedos are adjacent (e.g., snow and forest), photons reflected from a bright tile can illuminate a neighboring dark tile. This three-dimensional radiative transfer effect introduces a nonlinear coupling that generally reduces the effective albedo below the value predicted by the linear model.

### Tile-Level Physics: Closing the Water and Energy Budgets

For the tiling approach to be physically meaningful, each tile must function as a self-contained, one-dimensional model capable of closing its own water and energy budgets. This requires defining a minimal set of **prognostic [state variables](@entry_id:138790)** (quantities that evolve over time according to a differential equation) and the **flux processes** that govern their evolution .

For a comprehensive LSM tile that includes vegetation and snow, the minimal set of prognostic [state variables](@entry_id:138790) typically includes:

*   **Water Storage Variables**:
    *   $S_i$: Soil water storage (often discretized into multiple layers).
    *   $C_i$: Water intercepted by the plant canopy.
    *   $W_{s,i}$: Snow water equivalent (the mass of water in the snowpack).
    *   $W_{p,i}$: Water ponded on the surface.
*   **Energy/Temperature Variables**:
    *   $T_{g,i}$: Temperature of the soil column.
    *   $T_{c,i}$: Temperature of the canopy.
    *   $T_{s,i}$: Temperature of the snowpack.

The evolution of these [state variables](@entry_id:138790) is governed by the fluxes entering and leaving the tile's control volume. Key external flux processes include:

*   **Water Fluxes**:
    *   Precipitation, partitioned into liquid ($P_{r,i}$) and solid ($P_{s,i}$).
    *   Evapotranspiration, partitioned into canopy evaporation ($E_{c,i}$), plant [transpiration](@entry_id:136237) ($\mathrm{Tr}_i$), and ground/snow evaporation/sublimation ($E_{g,i}$).
    *   Runoff, which provides the input to the [river routing model](@entry_id:1131058), partitioned into [surface runoff](@entry_id:1132694) ($R_{\text{surf},i}$) and subsurface/baseflow ($Q_{\text{sub},i}$).
*   **Energy Fluxes**:
    *   $R_{n,i}$: Net radiation (the sum of net shortwave and net longwave radiation).
    *   $H_i$: Sensible heat flux.
    *   $\lambda E_i$: Latent heat flux, which is the energy equivalent of total evapotranspiration and directly couples the water and energy budgets.
    *   $G_i$: Ground heat flux into the deep soil.

By solving the conservation equations for mass and energy using these states and fluxes, each tile independently simulates its physical response to atmospheric forcing.

### River Routing: Transporting Water Across the Landscape

While tiling effectively handles the vertical exchanges of water and energy, ESMs must also represent the horizontal transport of water via river networks. This process, known as **river routing**, takes the runoff generated by land surface tiles as input and simulates its movement through channels, rivers, and floodplains.

#### Coupling the Land to the River

The first step in river routing is to map the runoff generated on the distributed land surface tiles to the inlet of a discrete river network. A routing model is typically defined on a separate graph or grid representing river reaches, whose geometry is dictated by topography, not the regular grid of the atmospheric model. Therefore, a **hydrologic response unit (HRU)** in a routing model is a distinct concept from an LSM tile; an HRU is a lumped element defined by drainage characteristics and can aggregate runoff from multiple tiles or even multiple grid cells .

The coupling is achieved by pre-calculating drainage fractions, $a_{ir}$, which represent the fraction of runoff from tile $i$ that drains into a specific river reach $r$. The total inflow $I_r$ into reach $r$ is the sum of contributions from all tiles in the grid cell that drain to it, ensuring mass conservation :

$$
I_r = \sum_{i=1}^{N} a_{ir} Q_i
$$

Here, $Q_i$ is the total volumetric runoff rate (surface + subsurface) from tile $i$.

#### Physics-Based and Conceptual Routing Models

Once water enters a river reach, its movement is governed by the principles of [open-channel hydraulics](@entry_id:273093), mathematically described by the **Saint-Venant equations**. These are a pair of partial differential equations representing the conservation of mass (continuity) and momentum:

*   **Continuity**: $\frac{\partial A}{\partial t} + \frac{\partial q}{\partial x} = 0$
*   **Momentum**: $\frac{\partial q}{\partial t} + \frac{\partial}{\partial x}(\frac{q^2}{A}) + gA \frac{\partial h}{\partial x} = gA(S_0 - S_f)$

Here, $A$ is the cross-sectional area, $q$ is discharge, $h$ is water surface elevation, $S_0$ is the channel bed slope, and $S_f$ is the [friction slope](@entry_id:265665). The terms in the momentum equation represent [local acceleration](@entry_id:272847), convective acceleration, pressure gradient, gravity, and friction, respectively.

Solving the full Saint-Venant equations (the **dynamic wave** model) is computationally intensive. Therefore, simpler approximations are widely used in large-scale models :

1.  **Diffusive Wave Model**: This model neglects the acceleration (inertial) terms in the momentum equation. It is suitable for gradually varying flows where the water surface slope is the dominant factor balancing bed slope and friction. The momentum equation simplifies to $\partial h / \partial x = S_0 - S_f$. This model can simulate backwater effects and produces a hydrograph that both translates and attenuates.

2.  **Kinematic Wave Model**: This model further simplifies the diffusive wave by also neglecting the pressure gradient term ($\partial h / \partial x$). This is valid for steep channels where the flow is primarily driven by gravity balancing friction. The momentum equation reduces to a simple algebraic relationship, $S_0 = S_f$, which implies that discharge $q$ is a unique function of flow area $A$, often expressed as a power-law rating curve $q = \alpha A^p$. This model purely translates the flood wave downstream without attenuation. The downstream propagation speed of perturbations is $c_k = dq/dA$.

In addition to physics-based simplifications, many routing models employ **conceptual methods** that capture the essential behavior of a river reach without [solving partial differential equations](@entry_id:136409). A classic example is the **Muskingum method** . It is based on the continuity equation, $dS/dt = I - Q$, where $S$ is the storage in the reach, $I$ is inflow, and $Q$ is outflow. The key assumption is a linear relationship for storage:

$$
S = K[XI + (1-X)Q]
$$

Here, $K$ is a storage time constant (with units of time) representing the travel time through the reach, and $X$ is a dimensionless weighting factor ($0 \le X \le 0.5$) that partitions the influence of inflow and outflow on storage. This conceptualizes storage as a combination of a prism (proportional to outflow) and a wedge (proportional to inflow). By discretizing the continuity equation and substituting the storage relationship, one can derive an explicit [recurrence relation](@entry_id:141039) for the outflow at the next time step, $Q^{n+1}$, as a linear function of $I^{n+1}$, $I^n$, and $Q^n$.

### Numerical Implementation and Conservation

The implementation of routing schemes in a numerical model requires careful consideration of stability and conservation.

#### Numerical Stability: The CFL Condition

Many routing schemes, particularly those based on [kinematic wave](@entry_id:200331) or advection approaches, use [explicit time-stepping](@entry_id:168157) methods for computational efficiency. An explicit forward-in-time, upwind-in-space discretization of the [linear advection equation](@entry_id:146245), $\partial q / \partial t + u \partial q / \partial x = 0$, is stable only if the time step $\Delta t$ satisfies the **Courant-Friedrichs-Lewy (CFL) condition** :

$$
\Delta t \le \frac{\Delta x}{u}
$$

Here, $\Delta x$ is the length of the discretized river reach and $u$ is the flow velocity. The quantity $C = u \Delta t / \Delta x$ is the Courant number, and the condition requires $C \le 1$. Physically, this means that the fluid cannot travel more than one grid cell length in a single time step, ensuring that the numerical scheme's [domain of dependence](@entry_id:136381) contains the physical [domain of dependence](@entry_id:136381). When a model includes a network of heterogeneous reaches (e.g., fast-flowing mountain streams and slow-moving floodplains), a single global time step must be chosen that satisfies the CFL condition for the *most restrictive* case—that is, the minimum value of $\Delta x_i / u_i$ across all reaches $i$.

#### Mass Conservation Diagnostics

A fundamental requirement of any routing model is that it must conserve water mass. Over a network of $J$ tiles or reservoirs, the total rate of change of storage must equal the total external inflow minus the total external outflow. The internal fluxes between reservoirs, $F_{i \to j}$, must cancel out when summed over the entire network . The network-wide [mass balance](@entry_id:181721) is:

$$
\frac{d}{dt} \sum_{j=1}^{J} S_j(t) = \sum_{j=1}^{J} I_j(t) - \sum_{j=1}^{J} Q_j(t)
$$

In a numerical model, small errors from [floating-point arithmetic](@entry_id:146236) or inconsistencies in the discretization can lead to violations of this principle. It is therefore crucial to implement a **mass balance diagnostic**. For each time step $k$, one can compute a residual error, $r_k$:

$$
r_k = \left( \sum_{j=1}^{J} I_j(t_k) - \sum_{j=1}^{J} Q_j(t_k) \right) - \frac{\sum_{j=1}^{J} S_j(t_{k+1}) - \sum_{j=1}^{J} S_j(t_k)}{\Delta t}
$$

An ideal model would have $r_k=0$ at all times. By tracking the maximum instantaneous residual, $|r_k|$, and the cumulative mass error, $\sum r_k \Delta t$, over the course of a simulation, model developers can verify that the implementation is behaving as expected and that water is not being artificially created or destroyed.