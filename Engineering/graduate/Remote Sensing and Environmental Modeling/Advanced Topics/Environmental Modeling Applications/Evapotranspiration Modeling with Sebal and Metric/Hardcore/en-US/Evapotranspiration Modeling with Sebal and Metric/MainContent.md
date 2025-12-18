## Introduction
The precise quantification of evapotranspiration (ET)—the combined water loss from soil evaporation and plant [transpiration](@entry_id:136237)—is a cornerstone of modern hydrology, agriculture, and environmental science. While traditional methods provide point measurements, managing water resources effectively requires understanding ET as a spatially and temporally dynamic process across vast landscapes. This knowledge gap is addressed by remote sensing-based [surface energy balance](@entry_id:188222) models, with the Surface Energy Balance Algorithm for Land (SEBAL) and its refinement, Mapping EvapoTranspiration at high Resolution with Internalized Calibration (METRIC), standing as preeminent examples. These models ingeniously convert satellite-observed radiances into detailed maps of actual water consumption, providing invaluable data for everything from farm-level irrigation scheduling to basin-scale water accounting.

This article provides a comprehensive exploration of these powerful models. To build a solid foundation, we will first deconstruct their core physical principles in **Principles and Mechanisms**, exploring how the law of conservation of energy is leveraged to estimate latent heat flux. Next, in **Applications and Interdisciplinary Connections**, we will examine how these ET maps are transformed into actionable intelligence for agricultural water management, regional hydrology, and [environmental monitoring](@entry_id:196500). Finally, **Hands-On Practices** will allow you to engage directly with the fundamental calculations that underpin these sophisticated workflows. By progressing through these sections, you will gain a thorough understanding of both the theory and practice of modeling evapotranspiration with SEBAL and METRIC.

## Principles and Mechanisms

The estimation of evapotranspiration (ET) using satellite remote sensing is fundamentally an exercise in applying the principle of conservation of energy to the land surface. Models such as the Surface Energy Balance Algorithm for Land (SEBAL) and Mapping EvapoTranspiration at high Resolution with Internalized Calibration (METRIC) are built upon this foundation. This chapter will deconstruct the physical principles and operational mechanisms that enable these models to convert satellite-observed radiances into spatially distributed maps of [latent heat flux](@entry_id:1127093).

### The Surface Energy Balance Equation

The cornerstone of surface energy balance modeling is the [first law of thermodynamics](@entry_id:146485) applied to a control volume at the land-atmosphere interface. For a given surface area, the net available radiative energy is partitioned into heating the ground, heating the overlying air, and providing the energy for the phase change of water from liquid to vapor. This relationship is expressed through the surface energy balance equation:

$R_n = G + H + LE$

Here, each term represents an energy flux density, typically measured in watts per square meter ($W \cdot m^{-2}$).

-   **Net Radiation ($R_n$)** is the balance of all incoming and outgoing shortwave (solar) and longwave (thermal) radiation. It represents the total radiative energy available to the surface. By convention, $R_n$ is positive when the net flux is directed toward the surface, which is typical during daylight hours.

-   **Soil Heat Flux ($G$)** is the energy transferred into or out of the soil substrate via molecular conduction. During the day, as the surface is heated by net radiation, energy is typically conducted downward into the cooler soil, making $G$ a sink of energy from the surface.

-   **Sensible Heat Flux ($H$)** is the energy transferred between the surface and the atmosphere via [turbulent convection](@entry_id:151835), driven by a temperature difference. When the surface is warmer than the overlying air, as is common at midday, heat is transferred upward, warming the lower atmosphere.

-   **Latent Heat Flux ($LE$)** represents the energy consumed in the process of **evapotranspiration (ET)**, which is the sum of evaporation from soil and water surfaces and transpiration from plant leaves. This [phase change](@entry_id:147324) from liquid water to water vapor requires a substantial amount of energy, known as the [latent heat of vaporization](@entry_id:142174) ($L_v$). Consequently, $LE$ is the energy equivalent of the water vapor mass flux ($ET$), expressed as $LE = L_v \times ET$. This energy consumption leads to cooling at the surface, and the resulting water vapor is transported upward into the atmosphere.

In SEBAL and METRIC, the primary objective is to determine the latent heat flux, $LE$. This is achieved by calculating the other three terms of the energy balance and solving for $LE$ as the residual:

$LE = R_n - G - H$

Consider a well-watered agricultural field under clear-sky midday conditions. The [net radiation](@entry_id:1128562) provides a substantial energy input, for instance, $R_n = 650 \, \mathrm{W m^{-2}}$. A fraction of this energy is conducted into the ground, say $G = 60 \, \mathrm{W m^{-2}}$. Another portion heats the air via convection, for example, $H = 240 \, \mathrm{W m^{-2}}$. The remaining energy, $LE = 650 - 60 - 240 = 350 \, \mathrm{W m^{-2}}$, must be consumed by the process of evapotranspiration. This large upward flux of latent heat is characteristic of a healthy, transpiring vegetated surface . The remainder of this chapter details how each term on the right-hand side of the equation is estimated from remote sensing data and meteorological inputs.

### Estimating the Energy Balance Components

The successful application of the energy balance residual method hinges on the accurate estimation of $R_n$, $G$, and, most critically, $H$.

#### Net Radiation ($R_n$): The Driving Energy Source

Net radiation is the sum of net shortwave and net longwave radiation fluxes:

$R_n = (S_{\downarrow} - S_{\uparrow}) + (L_{\downarrow} - L_{\uparrow})$

where $S_{\downarrow}$ and $S_{\uparrow}$ are the incoming and outgoing shortwave fluxes, and $L_{\downarrow}$ and $L_{\uparrow}$ are the incoming and outgoing longwave fluxes. This can be rewritten in terms of surface properties as:

$R_n = (1 - \alpha) S_{\downarrow} + \varepsilon L_{\downarrow} - \varepsilon \sigma T_s^{4}$

Here, $\alpha$ is the broadband [surface albedo](@entry_id:1132663), $\varepsilon$ is the broadband surface emissivity, $T_s$ is the land surface temperature, and $\sigma$ is the Stefan-Boltzmann constant. The incoming fluxes, $S_{\downarrow}$ and $L_{\downarrow}$, are typically derived from a nearby weather station or [atmospheric models](@entry_id:1121200). The core task for remote sensing is to estimate the surface properties $\alpha$, $\varepsilon$, and $T_s$ for every pixel.

**Broadband Surface Albedo ($\alpha$)** is defined as the fraction of incident solar radiation reflected by the surface. Multispectral satellites measure reflectance in several discrete, narrow bands. To compute the broadband albedo, these narrowband reflectances are combined using a weighted average. The weights, which are specific to each sensor, account for the distribution of solar energy across the shortwave spectrum. The general formula is:

$\alpha \approx \sum_{i} w_i \rho_{s,i}$

where $\rho_{s,i}$ is the surface reflectance in band $i$ and $w_i$ is the corresponding weight. It is crucial to use **atmospherically corrected surface reflectances** for this calculation. The signal measured by a satellite, known as top-of-atmosphere (TOA) reflectance, is a mixture of the signal reflected from the surface and radiation scattered by the atmosphere (path radiance). Using TOA reflectance would incorrectly attribute atmospheric effects to the surface, biasing the albedo and all subsequent energy balance calculations .

**Surface Emissivity ($\varepsilon$) and Land Surface Temperature ($T_s$)** are required for the longwave radiation balance. Land surface temperature is derived from the satellite's thermal infrared band(s), but this requires a correction for surface emissivity. Emissivity, like albedo, varies with surface type. In SEBAL and METRIC, emissivity is often parameterized using a vegetation index, such as the **Normalized Difference Vegetation Index (NDVI)**. NDVI is a robust indicator of the presence and health of green vegetation, defined as:

$NDVI = \frac{\rho_{NIR} - \rho_{red}}{\rho_{NIR} + \rho_{red}}$

where $\rho_{NIR}$ and $\rho_{red}$ are the surface reflectances in the near-infrared and red portions of the spectrum, respectively. Healthy vegetation strongly absorbs red light for photosynthesis and strongly reflects near-infrared light, resulting in high NDVI values (e.g., $0.7$ to $0.8$). Bare soil, in contrast, has a relatively flat reflectance spectrum and thus a low NDVI (e.g., $0.05$ to $0.15$). Since vegetation generally has a higher emissivity (e.g., $\varepsilon_v = 0.985$) than bare soil (e.g., $\varepsilon_s = 0.950$), the pixel-scale emissivity can be estimated as a function of NDVI, often through an intermediate calculation of fractional vegetation cover .

#### Soil Heat Flux ($G$): Energy into the Substrate

Soil heat flux ($G$) cannot be measured directly from space and must be parameterized. SEBAL and METRIC estimate $G$ as a fraction of net radiation ($R_n$). This fraction, $G/R_n$, is not constant; it depends heavily on the amount of vegetation cover. A dense vegetation canopy intercepts most of the incoming radiation, leaving little energy to reach the soil surface and be conducted downward. Conversely, for a bare soil surface, a large fraction of the net radiation is transferred into the ground.

This relationship is captured by empirical functions that relate the $G/R_n$ ratio to surface properties derived from the satellite, primarily NDVI, but also surface temperature and albedo. For a dense canopy with a high NDVI, $G/R_n$ is small (e.g., $0.05$), whereas for bare soil with a low NDVI, it can be quite large (e.g., $0.3$ or higher) .

#### Sensible Heat Flux ($H$): The Critical Internal Calibration

The estimation of sensible heat flux ($H$) is the most challenging and innovative component of the SEBAL and METRIC models. The bulk aerodynamic formulation for $H$ is:

$H = \rho c_p \frac{dT}{r_{ah}}$

where $\rho$ is air density, $c_p$ is the [specific heat](@entry_id:136923) of air, $r_{ah}$ is the aerodynamic resistance to [heat transport](@entry_id:199637), and $dT$ is the near-surface temperature difference that drives the flux. A primary difficulty is that this temperature difference, which physically represents the difference between the aerodynamic surface temperature ($T_{aero}$) and the air temperature at a reference height ($T_a$), cannot be directly measured from space. Remote sensing provides the radiometric surface temperature ($T_s$), which is not necessarily equal to $T_{aero}$.

SEBAL and METRIC overcome this obstacle with an ingenious **internal calibration** procedure. They assume that, for a given satellite scene at a specific time, there is a linear relationship between the unobservable driving temperature difference $dT$ and the observable radiometric surface temperature $T_s$:

$dT = a T_s + b$

The scene-specific coefficients, $a$ and $b$, are determined by identifying two "anchor" pixels within the image that represent extreme hydrological conditions , .

**The Anchor Pixels** are the linchpins of the calibration. Their proper selection is critical.

-   The **"hot" anchor pixel** is chosen over a dry, bare, or non-transpiring agricultural surface. The key assumption is that evapotranspiration is zero ($LE_{hot} = 0$). This surface should be radiometrically hot (high $T_s$), have low NDVI, and be located in a large, uniform area away from water bodies or irrigated fields to avoid cooling by advection.
-   The **"cold" anchor pixel** is chosen over a well-watered, full-cover crop (like alfalfa) or a deep open water body, where evapotranspiration is occurring at near-potential rates. This surface should be radiometrically cool (low $T_s$), have high NDVI (if vegetation), and also have a sufficient fetch (a large uniform upwind area) to ensure the overlying air is in equilibrium with the surface .

**Deriving the Calibration**
The physical assumptions at the anchor pixels provide the two equations needed to solve for the two unknowns, $a$ and $b$.

1.  **At the cold pixel**, the surface is assumed to be transpiring so efficiently that sensible heat flux is minimal. In SEBAL, the assumption is $H_{cold} \approx 0$, which implies $dT_{cold} \approx 0$.
2.  **At the hot pixel**, the assumption is $LE_{hot} = 0$. The energy balance simplifies to $H_{hot} = R_{n,hot} - G_{hot}$. From the bulk aerodynamic equation, we can then solve for the temperature difference at the hot pixel: $dT_{hot} = \frac{H_{hot} \cdot r_{ah,hot}}{\rho c_p}$.

With these two points—($T_{s,cold}$, $dT_{cold} \approx 0$) and ($T_{s,hot}$, $dT_{hot}$)—the linear equation is solved. The slope $a$ and intercept $b$ are found as:

$a = \frac{dT_h}{T_{s,h} - T_{s,c}}$

$b = -a \cdot T_{s,c}$

This scene-specific calibration is remarkably powerful. Because it is performed for every satellite image, it automatically accounts for the atmospheric conditions at the time of the overpass, including the effects of regional advection (the transport of heat by wind). A "universal" model with fixed coefficients would fail to capture these site-specific dynamics, leading to biased results .

To illustrate, consider the data from a hypothetical scenario . At a hot pixel, we have $R_n^{hot} = 650 \, W m^{-2}$ and $G^{hot} = 80 \, W m^{-2}$. Assuming $LE^{hot}=0$, the sensible heat flux must be $H^{hot} = 650 - 80 = 570 \, W m^{-2}$. Given an aerodynamic resistance $r_{ah}^{hot} = 60 \, s m^{-1}$ and $\rho c_p \approx 1205 \, J m^{-3} K^{-1}$, the temperature difference is $dT^{hot} = (570 \times 60) / 1205 \approx 28.4 \, K$. At a cold pixel, depending on the specific model (SEBAL vs. METRIC), a boundary condition is set that results in a much lower sensible heat flux, for example, $H^{cold} = 20 \, W m^{-2}$, yielding a correspondingly lower $dT^{cold} \approx 1.0 \, K$. These two ($T_s, dT$) pairs then define the linear relationship for the entire scene.

Once the coefficients $a$ and $b$ are known, $dT$ can be calculated for every pixel using its measured $T_s$. The sensible heat flux $H$ is then computed for every pixel, which requires an iterative calculation because the **aerodynamic resistance ($r_{ah}$)** itself depends on [atmospheric stability](@entry_id:267207), which in turn depends on $H$. This calculation is performed using Monin-Obukhov Similarity Theory, incorporating wind speed from a weather station and pixel-by-pixel estimates of [surface roughness](@entry_id:171005), which are also often parameterized using NDVI .

### Distinguishing SEBAL and METRIC

While SEBAL and METRIC share the same fundamental framework, they differ in two key aspects: the cold pixel calibration and the method for scaling from instantaneous to daily ET.

#### Calibration Philosophy

The primary difference lies in the assumption made at the cold anchor pixel .

-   **SEBAL** typically uses the simpler assumption that at the cold pixel, sensible heat flux is nearly zero ($H_{cold} \approx 0$). This assumes that the well-watered surface is evaporating at a rate that consumes nearly all available energy ($R_n - G$).

-   **METRIC** employs a more refined approach by calibrating the cold pixel to a standardized **[reference evapotranspiration](@entry_id:1130773) ($ET_r$)**. This $ET_r$ is calculated for a hypothetical reference crop (e.g., alfalfa) using the full Penman-Monteith equation and data from a high-quality weather station. At the cold pixel, which is selected to be a well-irrigated crop similar to the reference, the actual evapotranspiration is set to a fraction of the reference ET (e.g., $ET_{cold} = 1.05 \times ET_r$). This directly ties the satellite-based energy balance to a ground-based meteorological standard, improving transferability and consistency, particularly in advective environments.

#### Scaling from Instantaneous to Daily ET

Evapotranspiration is a cumulative process, and for most applications, a daily total ($ET_{24}$) is more useful than an instantaneous flux. Both models extrapolate the instantaneous estimate from the satellite overpass time to a 24-hour total, but they use different assumptions about what property remains constant throughout the day .

-   **SEBAL** assumes that the **evaporative fraction ($\Lambda = LE / (R_n - G)$)** is constant during daylight hours. The rationale is that on a clear day, the partitioning of available energy between latent and sensible heat is relatively stable.

-   **METRIC** assumes that the **fraction of reference ET ($ET_{rF} = ET / ET_r$)** is constant throughout the day. The rationale here is that the factors making the actual surface differ from the reference crop (e.g., water stress, crop type) exert a proportionally constant effect over the day. This assumption has been shown to be more robust, especially under advective conditions where the evaporative fraction can exceed 1 and vary significantly.

The two scaling methods yield identical results if, and only if, the ratio of the reference ET to the available energy is constant throughout the day. This condition is often approximately met on clear, non-advective days, but the methods can diverge otherwise .

### Summary of the SEBAL/METRIC Workflow and Key Assumptions

The entire process, from raw satellite imagery to a final map of evapotranspiration, can be summarized in a series of steps :

1.  **Radiometric Preprocessing:** Convert raw satellite digital numbers to [at-sensor radiance](@entry_id:1121171), then to atmospherically corrected surface reflectance and land surface temperature ($T_s$).
2.  **Surface Property Estimation:** Calculate key surface properties for each pixel, including broadband albedo ($\alpha$), NDVI, and surface emissivity ($\varepsilon$).
3.  **Energy Balance Component Estimation:**
    *   Calculate [net radiation](@entry_id:1128562) ($R_n$) using the derived surface properties and meteorological data for incoming radiation.
    *   Calculate [soil heat flux](@entry_id:1131878) ($G$) using an empirical function of NDVI, $T_s$, and $\alpha$.
4.  **Internal Calibration:**
    *   Identify suitable hot and cold anchor pixels in the scene.
    *   Apply the physical boundary conditions ($LE_{hot}=0$; $H_{cold} \approx 0$ for SEBAL or $LE_{cold} \propto LE_r$ for METRIC) to solve for $H$ and $dT$ at the anchors.
    *   Determine the coefficients of the linear $dT-T_s$ relationship.
5.  **Flux Calculation:**
    *   For every pixel, use its $T_s$ and the calibrated linear relationship to find its $dT$.
    *   Iteratively solve for sensible heat flux ($H$) and aerodynamic resistance ($r_{ah}$) using Monin-Obukhov Similarity Theory.
    *   Calculate the instantaneous [latent heat flux](@entry_id:1127093) ($LE$) as the residual: $LE = R_n - G - H$.
6.  **Daily Scaling:** Extrapolate the instantaneous $LE$ to a daily total ($ET_{24}$) by assuming either a constant evaporative fraction (SEBAL) or a constant fraction of reference ET (METRIC).

This sophisticated process relies on several key assumptions, including clear-sky conditions at the time of overpass, a steady-state energy balance, horizontally uniform atmospheric conditions, and negligible heat storage within the vegetation canopy itself.

### Limitations and Sources of Error

While powerful, these models are subject to errors when their underlying assumptions are violated. Understanding these limitations is critical for the proper application and interpretation of the results .

-   **Lateral Advection:** In an "oasis effect" scenario, where warm, dry air blows over a cooler, irrigated field, the standard cold pixel assumption ($H \approx 0$) is violated because [sensible heat flux](@entry_id:1131473) is actually downward ($H  0$). This leads the model to overestimate $H$ and consequently underestimate $LE$ for the irrigated field.
-   **Canopy Heat Storage ($S$):** The models typically assume the heat storage in the canopy biomass and air is negligible ($S \approx 0$). However, during periods of rapid warming, such as mid-morning, $S$ is positive. Neglecting this term in the energy balance ($LE = R_n - G - H - S$) causes the residual $LE$ to be overestimated.
-   **Surface Heterogeneity:** The models assume horizontal homogeneity in the atmosphere, yet surface properties like roughness can vary dramatically. Using a single roughness value or a calibration biased by a smooth hot pixel can lead to an overestimation of the aerodynamic resistance ($r_{ah}$) over rougher vegetated areas. This, in turn, causes an underestimation of $H$ and an overestimation of the residual $LE$.
-   **Daily Scaling Instability:** The assumption of a constant evaporative fraction or reference ET fraction can be violated on days with changing cloud cover or on days where plants exhibit afternoon [stomatal closure](@entry_id:149141) to conserve water. If the satellite passes in the morning when the evaporative fraction is high, but it decreases in the afternoon, the model will overestimate the total daily evapotranspiration.

In conclusion, SEBAL and METRIC are physically-based models that cleverly leverage the [surface energy balance](@entry_id:188222) and an internal calibration scheme to map evapotranspiration. Their accuracy depends not only on the quality of the input data but also on the degree to which the physical conditions in a given scene adhere to the models' core assumptions. A critical awareness of these principles and limitations is essential for any practitioner in the field.