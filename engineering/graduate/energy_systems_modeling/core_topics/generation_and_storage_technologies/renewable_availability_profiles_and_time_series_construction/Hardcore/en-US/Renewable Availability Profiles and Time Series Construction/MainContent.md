## Introduction
The transition to a decarbonized energy system hinges on the large-scale integration of variable renewable energy (VRE) sources like wind and solar. However, their fluctuating nature poses significant challenges for grid planning and operation. Accurately capturing this variability is paramount, yet there is often a gap between raw meteorological data and the model-ready time series needed for robust analysis. This article provides a comprehensive guide to bridging that gap by detailing the construction and application of renewable availability profiles.

This guide is structured to take you from foundational theory to practical application.
-   The first section, **Principles and Mechanisms**, lays the theoretical groundwork, detailing the steps from acquiring and cleaning raw weather data to applying physical conversion models and advanced statistical techniques to generate availability profiles.
-   The second section, **Applications and Interdisciplinary Connections**, explores how these profiles are utilized in critical energy system tasks, such as economic dispatch, reliability assessment, and long-term planning, and highlights their connection to fields like climate and computational science.
-   The final section, **Hands-On Practices**, provides practical exercises to reinforce the methods discussed and build tangible skills in time series construction and analysis.

We begin by establishing the core principles and mechanisms that govern the creation of these essential data products.

## Principles and Mechanisms

The modeling of renewable energy resources is a cornerstone of modern energy system analysis. An accurate representation of their variable and uncertain nature is essential for tasks ranging from long-term investment planning to real-time operational security. This chapter establishes the fundamental principles and mechanisms for constructing renewable availability profiles, which are the time series that quantify the maximum potential power output of a generator. We will proceed from foundational definitions to the practical steps of data acquisition and cleaning, through the physical models of power conversion, and culminating in advanced statistical techniques for capturing seasonality and inter-resource dependencies.

### Foundational Concepts of Renewable Availability

In energy systems modeling, it is critical to distinguish between the potential for generation and the actual, realized output of a power plant. This distinction is especially important for variable renewable energy (VRE) sources like wind and solar, whose potential is dictated by fluctuating meteorological conditions. We formalize this by defining three distinct but related time series. [@problem_id:4115861]

Let us consider a renewable generator with a fixed nameplate capacity, denoted by $\bar{p}$, measured in megawatts (MW).

The **availability profile**, denoted as $a_t$, is a dimensionless time series where each value $a_t \in [0, 1]$. It represents the fraction of the nameplate capacity that is available for generation at time $t$ based solely on the ambient resource conditions (e.g., wind speed, solar irradiance) and the technical and operational status of the plant itself. The availability profile is an **exogenous** input to most energy system models, as it is determined by factors external to the model's economic dispatch decisions. It defines an instantaneous technical upper bound on what the generator *can* produce.

The **realized generation profile**, $g_t$, is the actual power output of the generator in MW at time $t$. This is an **endogenous** variable in optimization models, meaning it is an outcome of the model's decision-making process. The realized generation must respect the physical limits imposed by the availability profile. This fundamental constraint is expressed as:
$$0 \le g_t \le \bar{p} a_t$$
In addition to this upper bound, $g_t$ is also subject to other system-level constraints, such as network limitations or economic signals from the grid operator that may lead to **curtailment**—a deliberate reduction of output below the available potential.

The **capacity factor time series**, $c_t$, is a dimensionless series derived from the realized generation, defined as $c_t = g_t / \bar{p}$. Since $g_t$ is an endogenous outcome that reflects both resource availability and any economic curtailment, $c_t$ is also endogenous. It represents the fraction of the nameplate capacity that was actually used. From the definitions above, it follows that these three series are linked by the inequality:
$$0 \le c_t \le a_t \le 1$$
This hierarchy is fundamental: the capacity factor can never exceed the availability, and the availability can never exceed $1$ (or $100\%$ of nameplate capacity). Understanding this distinction is the first step in correctly modeling VRE resources.

### From Raw Data to Resource Time Series

The construction of an availability profile begins with acquiring raw meteorological data. The choice of data source is a critical decision that influences the accuracy and reliability of the final model. Three primary classes of data are commonly used, each with distinct characteristics concerning spatial coverage, temporal resolution, and bias. [@problem_id:4115918]

**Ground measurements**, such as those from weather stations, provide direct, point-based observations of variables like wind speed, temperature, and solar irradiance. They typically offer high temporal resolution (e.g., one minute to one hour) and, with proper calibration, low instrument bias. However, their spatial coverage is sparse and non-uniform. When used to represent a larger area, such as a wind farm or a regional grid zone, they suffer from significant **representativeness error** because conditions at a single point may not accurately reflect the average conditions over the broader area.

**Satellite products** offer a significant advantage in spatial coverage, providing data over vast regions, often with near-global reach. For solar energy, geostationary satellites can provide irradiance data at high spatial (e.g., $1-5$ km) and temporal (e.g., $5-15$ minutes) resolutions. However, these products are not direct measurements; they are derived by inverting satellite-observed radiation through complex radiative transfer models. This process introduces **retrieval errors** and biases related to factors like cloud detection, aerosol concentrations, and surface reflectivity.

**Reanalysis datasets** are produced by Numerical Weather Prediction (NWP) models that assimilate a wide range of historical observations (including ground and satellite data) into a physically consistent, gridded reconstruction of the Earth's atmosphere. Products like ERA5 provide global, spatially complete datasets with hourly time steps and resolutions on the order of $25-30$ km. While they are invaluable for their consistency and completeness, they have their own biases. The finite resolution of the model tends to smooth out the data, often underestimating the intensity of extreme events like wind gusts or the sharp variability of solar irradiance on partly cloudy days.

The selection of a data source must be aligned with the modeling objective. Specifically, the data's temporal and spatial resolution must be sufficient to capture the key scales of variability that drive system dynamics. [@problem_id:4115857] These scales include:
-   **Diurnal variability**: The daily cycle driven by the Earth's rotation (e.g., the solar cycle).
-   **Synoptic variability**: Associated with large-scale weather systems like cyclones and anticyclones, with characteristic periods of $2$ to $10$ days.
-   **Seasonal variability**: The annual cycle driven by the Earth's axial tilt.

To avoid aliasing and accurately resolve these phenomena, the data must adhere to the **Nyquist-Shannon sampling theorem**, which requires the sampling frequency to be at least twice the highest frequency component of the signal. This implies that to capture diurnal cycles and the sub-daily ramps characteristic of VRE, a sampling interval ($\Delta t$) of at least one hour is necessary, with higher resolutions (e.g., $15$ minutes) being preferable. To capture seasonal and synoptic patterns, the total record length ($L$) of the time series must span multiple years, which allows for the characterization of inter-annual variability and provides a robust statistical sample of different weather regimes. A record length of at least three years is often considered a minimum for planning studies.

### Data Quality Control and Preprocessing

Raw meteorological time series are invariably contaminated with errors, including missing values, sensor drift, and physically implausible readings. A rigorous quality control (QC) process is therefore an indispensable step before any data is used for modeling. A QC procedure typically involves a series of automated checks designed to flag or remove suspect data points. [@problem_id:4115834]

A robust QC framework for solar and wind data should include the following tests:

1.  **Physical Bounds Check**: Data must lie within physically possible ranges. For solar irradiance, the global horizontal irradiance ($G(t)$) cannot be negative and cannot exceed the theoretical maximum given by the extraterrestrial solar irradiance projected onto a horizontal surface. This upper envelope $U(t)$ depends on the solar constant ($I_0 \approx 1361 \, \text{W m}^{-2}$) and the solar zenith angle $\theta_z(t)$:
    $$U(t) = I_0 \max\left(0, \cos(\theta_z(t))\right)$$
    During the night, when $\theta_z(t) \ge 90^\circ$ and thus $U(t)=0$, any measured irradiance greater than a small tolerance (e.g., $5 \, \text{W m}^{-2}$) indicates a sensor offset error. For wind speed $u(t)$, it must be non-negative ($u(t) \ge 0$) and below an extreme physical maximum (e.g., $u_{\max} = 60 \, \text{m s}^{-1}$).

2.  **Rate-of-Change Check**: Physical systems cannot change state instantaneously. This principle can be used to detect unrealistic "jumps" in the data. By examining the change between consecutive data points, $|x(t_i) - x(t_{i-1})| / \Delta t$, one can flag any changes that exceed plausible physical limits. For example, thresholds might be set at $r_G = 4 \, \text{W m}^{-2} \text{s}^{-1}$ for irradiance and $r_u = 0.5 \, \text{m s}^{-2}$ for wind speed.

3.  **Consistency and Stuck-Value Check**: This test looks for anomalies in the data's behavior. A common sensor failure mode is a "flatline" or "stuck value," where the sensor reports the same value for an extended period. A rule can be implemented to flag any run of $k$ or more identical, non-missing values (e.g., $k=3$ for hourly wind data) as suspect.

4.  **Missing Data Handling**: Any missing values (often represented as NaN, "Not a Number") must be identified. While simple removal may be sufficient for some analyses, more sophisticated models often require gap-filling using statistical imputation methods.

Applying such a QC pipeline ensures that the time series used as the foundation for the availability profile is as clean and physically consistent as possible.

### Modeling the Resource-to-Power Conversion

Once a clean time series of a meteorological resource is obtained, the next step is to convert it into a time series of available electrical power. This involves a physical or engineering model that represents the conversion technology.

#### Solar Photovoltaic Availability

For a photovoltaic (PV) array, the primary input is the **plane-of-array (POA) irradiance**, $G_{\text{POA}}$, which is the total solar radiation incident on the tilted surface of the panels. Meteorological data sources typically provide horizontal irradiance components: Global Horizontal Irradiance (GHI), Direct Normal Irradiance (DNI), and Diffuse Horizontal Irradiance (DHI). A solar geometry model is required to transpose these to the plane of the array. [@problem_id:4115905]

The total POA irradiance is the sum of three components:
$$G_{\text{POA}} = G_{\text{beam}} + G_{\text{diffuse}} + G_{\text{ground}}$$

The **direct beam component**, $G_{\text{beam}}$, is the DNI projected onto the panel surface. This projection depends on the angle of incidence $\theta_i$, which is the angle between the sun's rays and the vector normal to the panel surface. Using vector analysis, this component can be expressed as:
$$G_{\text{beam}} = DNI \cdot \max(0, \cos(\theta_i))$$
where $\cos(\theta_i) = \sin(\theta_z) \sin(\beta) \cos(\gamma_s - \gamma_p) + \cos(\theta_z) \cos(\beta)$. Here, $\theta_z$ and $\gamma_s$ are the solar zenith and azimuth angles, while $\beta$ and $\gamma_p$ are the panel tilt and azimuth angles.

The **diffuse sky component**, $G_{\text{diffuse}}$, is the portion of the DHI that is visible to the tilted panel. Using a common isotropic sky model, this is determined by the sky view factor:
$$G_{\text{diffuse}} = DHI \cdot \left( \frac{1 + \cos(\beta)}{2} \right)$$

The **ground-reflected component**, $G_{\text{ground}}$, represents the portion of the GHI that reflects off the ground and strikes the panel. Assuming Lambertian (perfectly diffuse) reflection from the ground with an albedo (reflectance) of $\rho_g$, this component is:
$$G_{\text{ground}} = GHI \cdot \rho_g \cdot \left( \frac{1 - \cos(\beta)}{2} \right)$$
where the final term is the ground view factor. Summing these three terms gives the total incident irradiance $G_{\text{POA}}$. This value, along with cell temperature, is then fed into a PV performance model to calculate the final DC power output, which is then converted to AC power to determine the availability $a_t$.

#### Wind and Tidal Power Availability

For technologies that harness kinetic energy from a fluid flow, such as wind and tidal stream turbines, the available power is fundamentally related to the cube of the fluid speed. The instantaneous kinetic energy flux through a swept area $A$ is given by:
$$P_{\text{flux}}(t) = \frac{1}{2} \rho A v(t)^3$$
where $\rho$ is the fluid density and $v(t)$ is the fluid speed. The available electrical power is a fraction $\eta$ of this flux, where $\eta$ incorporates both the aerodynamic/hydrodynamic efficiency and mechanical/electrical losses.

For a wind turbine, the relationship between hub-height wind speed and power output is encapsulated in a **power curve**. This curve specifies a zero output below a **cut-in speed** $v_{\text{ci}}$, a rapidly increasing output (often approximated by the cubic relationship) up to the **rated speed** $v_{\text{r}}$, a constant rated power output between $v_{\text{r}}$ and the **cut-out speed** $v_{\text{co}}$, and zero output above $v_{\text{co}}$ to prevent damage. [@problem_id:4115882]

For tidal stream turbines, the velocity $v(t)$ is highly predictable, governed by astronomical forces. It can be modeled as a superposition of harmonic components corresponding to the principal tidal constituents (e.g., the semi-diurnal lunar M2 and solar S2 tides). [@problem_id:4115883] For a velocity of the form $v(t) = v_b + \sum_i a_i \cos(\omega_i t + \phi_i)$, the non-linear cubic relationship means that the long-term average power $\langle P_{\text{avail}} \rangle$ depends not only on the mean speed but also on the amplitudes of the oscillations:
$$\langle P_{\text{avail}} \rangle = \frac{1}{2} \eta \rho A \langle v(t)^3 \rangle$$
Calculating $\langle v(t)^3 \rangle$ shows that $\langle P_{\text{avail}} \rangle = \frac{1}{2} \eta \rho A \left[ v_b^3 + \frac{3}{2}v_b \sum_i a_i^2 \right]$, demonstrating that the variability of the resource contributes significantly to the average energy yield.

### Deconstructing Availability: Physical Capability versus Operational Constraints

The availability profile $a_t$ is a composite signal that encapsulates all factors limiting a generator's output, aside from system-level economic decisions. For clarity in modeling, it is often useful to deconstruct $a_t$ into distinct components representing different categories of constraints. [@problem_id:4115908]

We can define a **capability factor**, $\kappa_t \in [0, 1]$, to represent the limits imposed by physics and engineering alone. This factor combines the resource-to-power conversion function (e.g., from the power curve) with any hard physical operating envelopes. For instance, for a wind turbine, $\kappa_t$ would be zero if the wind speed is outside the cut-in/cut-out range, and equal to the normalized power curve value otherwise. Formally, if $g(R_t, \Theta_t)$ is the per-unit conversion mapping for resource state $R_t$ and ambient state $\Theta_t$, and $\mathcal{S}_{\text{phys}}$ is the set of times where operation is physically permissible, then:
$$\kappa_t = \mathbf{1}_{\mathcal{S}_{\text{phys}}}(t) \cdot g(R_t, \Theta_t)$$
where $\mathbf{1}_{\mathcal{S}_{\text{phys}}}(t)$ is an indicator function that is $1$ if $t \in \mathcal{S}_{\text{phys}}$ and $0$ otherwise.

Separately, we can define an **operational availability factor**, $u_t \in [0, 1]$, to represent non-physical constraints. These include planned events like scheduled maintenance, unplanned events like forced outages, and external constraints such as regulatory curfews (e.g., for wildlife protection) or limits on grid injection capacity. If $\mathcal{S}_{\text{op}}$ is the set of times when the plant is operationally permitted to run, and $d_t$ is the normalized grid export limit at time $t$, then the combined operational availability is:
$$u_t = \mathbf{1}_{\mathcal{S}_{\text{op}}}(t) \cdot d_t$$

Since the generator must be both physically capable *and* operationally available, the final availability profile $a_t$ is determined by the most limiting of these factors. This is mathematically expressed using the minimum operator:
$$a_t = \min\{\kappa_t, u_t\}$$
This decomposition provides a transparent framework for building up an availability profile from its constituent parts, allowing for detailed modeling of different types of outages and constraints.

### Advanced Topics in Time Series Construction

While historical time series are often used directly, more advanced energy system studies may require the generation of synthetic time series that preserve key statistical properties or the analysis of profiles under specific constraints.

#### Modeling Seasonality and Stochasticity

To capture long-term patterns and generate alternative weather-year scenarios, we can model resource availability using time-varying statistical distributions. For wind energy, the wind speed at a given time is often modeled with a Weibull distribution. Seasonality can be introduced by allowing the Weibull shape parameter $k$ and scale parameter $\lambda$ to vary over the year, for example, using sinusoidal functions. [@problem_id:4115882]
$$k(t) = k_0 \left[1 + a_k \cos\left(2\pi \frac{t}{T} + \phi_k\right)\right]$$
$$\lambda(t) = \lambda_0 \left[1 + a_\lambda \cos\left(2\pi \frac{t}{T} + \phi_\lambda\right)\right]$$
With this parameterization, the availability profile $A(t)$ is no longer a direct mapping of a single wind speed value, but rather the **expected** normalized power output, calculated by integrating the turbine power curve $p(v)$ over the Weibull probability density function $f(v; k(t), \lambda(t))$ for that hour:
$$A(t) = \mathbb{E}[p(V(t))] = \int_0^\infty p(v) f(v; k(t), \lambda(t)) \, dv$$
This approach yields a smooth availability profile that inherently captures the average effect of wind speed variability within each hour, conditioned on the seasonal cycle.

#### Quantifying the Impact of Constraints

Probabilistic availability profiles can also be used to analytically assess the impact of operational constraints. For example, if an availability profile $a_t$ is known to follow a certain probability distribution, such as a Beta distribution, we can calculate the expected energy generation under a curtailment limit. [@problem_id:4115922] Suppose a generator with capacity $K$ has its output capped at $P_{\max}$. The realized generation is $g_t = \min\{K a_t, P_{\max}\}$. If the probability density function of $a_t$ is $f(x)$, the long-term expected generation is:
$$\mathbb{E}[g_t] = \int_0^1 \min\{Kx, P_{\max}\} f(x) \, dx$$
By splitting the integral at the point where the curtailment becomes binding ($x = P_{\max}/K$), one can derive a closed-form expression for the expected generation. This allows for rapid quantification of curtailment losses as a function of the resource's statistical properties and the grid constraint, a powerful tool for transmission planning and economic analysis.

#### Modeling Inter-Resource Dependencies

In systems with multiple VRE resources, the statistical dependence between them is a critical factor for reliability assessment. For example, the negative correlation often observed between wind and solar output on diurnal and synoptic scales can be beneficial for smoothing total renewable production. Modeling this dependence structure accurately is a sophisticated challenge.

The mathematically rigorous tool for this task is the **copula**. Sklar's Theorem states that any multivariate joint distribution can be decomposed into its marginal distributions (which describe each variable individually) and a copula function that describes their dependence structure. This separation is powerful because it allows us to model the marginals (e.g., the distribution of solar availability) and the dependence (e.g., the correlation between wind and solar) independently. [@problem_id:4115854]

A common choice is the **Gaussian copula**, which imposes a dependence structure identical to that of a multivariate normal distribution. The procedure to generate correlated time series for wind ($W_t$) and solar ($S_t$) with given marginal CDFs $F_W$ and $F_S$ and a target correlation $\rho$ is as follows:
1.  Generate a pair of correlated standard normal random variables $(Z_W, Z_S)$ from the distribution $\mathcal{N}(\mathbf{0}, \Sigma)$, where $\Sigma = \begin{pmatrix} 1  \rho \\ \rho  1 \end{pmatrix}$.
2.  Transform these normal variables into uniformly distributed variables on $[0,1]$ using the probability integral transform with the standard normal CDF, $\Phi$: $(U_W, U_S) = (\Phi(Z_W), \Phi(Z_S))$. This pair $(U_W, U_S)$ is now distributed according to the Gaussian copula.
3.  Transform the uniform variables into the final target variables using their respective inverse CDFs (quantile functions): $W_t = F_W^{-1}(U_W)$ and $S_t = F_S^{-1}(U_S)$.

This method correctly generates synthetic time series that not only honor the individual statistical properties of each renewable resource but also preserve the crucial correlations between them, enabling more realistic and robust energy system simulations.