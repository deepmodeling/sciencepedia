## Introduction
Analyzing the ocean's vast circulation and its role in the global climate system requires comparing parcels of water from different locations and depths. However, raw, in-situ measurements of temperature and density are heavily distorted by the immense changes in pressure, masking the subtle thermodynamic properties that actually drive [ocean dynamics](@entry_id:1129055). This article addresses the fundamental challenge of a compressible ocean by introducing conservative variables designed to remove these confounding pressure effects, providing a clearer view of the ocean's structure and movement.

Our journey begins in the **Principles and Mechanisms** chapter, where we will deconstruct the problem of compressional heating and derive the concepts of potential temperature and potential density—the classical tools for this task. We will then advance to the modern, thermodynamically rigorous framework of TEOS-10 and its key variable, Conservative Temperature. Next, in **Applications and Interdisciplinary Connections,** we will explore how these variables are applied in practice, from diagnosing ocean stability and inferring large-scale currents to forming the foundation of crucial parameterizations within computational ocean models. Finally, the **Hands-On Practices** section offers an opportunity to engage directly with these concepts, tackling problems that highlight the subtleties of stability analysis, mixing, and the differences between classical and modern [thermodynamic variables](@entry_id:160587).

## Principles and Mechanisms

The analysis of water masses, their circulation, and the ocean's role in the global heat budget depends critically on our ability to compare parcels of seawater from different locations and depths. In-situ measurements of temperature and density, however, are strongly influenced by the immense pressure variations within the ocean, obscuring the more subtle thermodynamic differences that drive [ocean dynamics](@entry_id:1129055). This chapter elucidates the principles and mechanisms developed to account for the effects of pressure, leading to the formulation of conservative variables that are indispensable in modern computational oceanography.

### The Challenge of a Compressible Ocean

A water parcel moving vertically in the ocean experiences significant changes in ambient pressure. As a parcel descends, it is compressed by the weight of the overlying water, and as it rises, it expands. These mechanical processes involve work being done on or by the parcel, which alters its internal energy and, consequently, its temperature.

This phenomenon, known as **compressional heating** or **expansional cooling**, occurs even if the parcel does not exchange heat with its surroundings—a process termed **adiabatic**. The rate at which temperature changes with pressure in an adiabatic process is known as the **[adiabatic lapse rate](@entry_id:193843)**, denoted by $\Gamma$. It can be derived from the first law of thermodynamics and is given by:

$$
\Gamma \equiv \left(\frac{\partial T}{\partial p}\right)_{\eta} = \frac{T \alpha}{\rho c_p}
$$

Here, $T$ is the [absolute temperature](@entry_id:144687), $\rho$ is the density, $c_p$ is the specific [heat capacity at constant pressure](@entry_id:146194), and $\alpha$ is the isobaric [thermal expansion coefficient](@entry_id:150685), defined as $\alpha = -\frac{1}{\rho}\left(\frac{\partial \rho}{\partial T}\right)_{p,S}$. The subscript $\eta$ indicates that specific entropy is held constant, which is characteristic of a reversible [adiabatic process](@entry_id:138150).

For a representative deep-ocean parcel, we might have $T \approx 275\,\mathrm{K}$, $\rho \approx 1025\,\mathrm{kg\,m^{-3}}$, $c_p \approx 3990\,\mathrm{J\,kg^{-1}\,K^{-1}}$, and $\alpha \approx 2 \times 10^{-4}\,\mathrm{K^{-1}}$. Using these values, the [adiabatic lapse rate](@entry_id:193843) is approximately $\Gamma \approx 1.3 \times 10^{-4}\,\mathrm{K\,dbar^{-1}}$ . This implies that for a vertical displacement of $1000\,\mathrm{dbar}$ (roughly $1000$ meters), a parcel's in-situ temperature will change by about $0.13\,\mathrm{K}$ solely due to compression or expansion.

This effect demonstrates that **in-situ temperature** is not a conserved quantity during vertical motion. A water mass could appear to warm or cool simply by changing its depth, making in-situ temperature an unreliable tracer for following water masses or assessing heat content. Similarly, **in-situ density** is dominated by pressure. The density of seawater increases by approximately $2\%$ between the surface and a depth of $4000\,\mathrm{m}$, a change that dwarfs the density variations of about $0.2\%$ that arise from the salinity and temperature differences driving deep ocean circulation. To analyze ocean dynamics, we must therefore employ variables that remove these dominant, but dynamically secondary, effects of pressure.

### Removing Compressibility Effects: Potential Temperature and Potential Density

The classical approach to removing the effect of pressure is to compare all water parcels as if they were moved to a common reference pressure.

The **potential temperature**, denoted $\boldsymbol{\theta}$, is defined as the temperature a parcel of seawater would attain if it were moved adiabatically (at constant entropy) and isohalinically (at constant salinity) from its in-situ pressure and temperature to a specified reference pressure, $p_r$ . Because it is defined based on an adiabatic process, potential temperature is, by construction, materially conserved for a parcel undergoing such motion. This property makes $\theta$ a vastly superior tracer for water masses compared to in-situ temperature.

Building on this concept, **potential density**, $\boldsymbol{\rho_\theta}$, is defined as the density a parcel would have at the reference pressure $p_r$. It is computed using the equation of state evaluated at the parcel's Absolute Salinity $S_A$, its potential temperature $\theta$ (itself calculated relative to $p_r$), and the reference pressure $p_r$ itself :

$$
\rho_{\theta,r} = \rho(S_A, \theta(p_r), p_r)
$$

For convenience, oceanographers often use the **potential density anomaly**, $\boldsymbol{\sigma_\theta}$, which is simply the potential density minus $1000\,\mathrm{kg\,m^{-3}}$. For a surface reference pressure ($p_r = 0\,\mathrm{dbar}$), this is denoted $\sigma_0$.

The use of potential density effectively removes the direct effect of pressure, allowing for meaningful comparisons of the intrinsic density of water parcels from different depths. The difference between a parcel's in-situ density and its potential density is substantial. A first-order analysis shows that this difference, $\rho_{in-situ} - \rho_{\theta,r}$, is composed of two parts: a large term due to the direct compression of water, and a much smaller term due to the adiabatic temperature change . For a parcel at $4000\,\mathrm{dbar}$, the direct effect of decompression when moving it to the surface ($p_r=0\,\mathrm{dbar}$) accounts for a density decrease of approximately $18.8\,\mathrm{kg\,m^{-3}}$. The accompanying adiabatic cooling of about $0.5\,\mathrm{K}$ slightly increases the parcel's density, opposing the decompression effect by only about $0.1\,\mathrm{kg\,m^{-3}}$. The net result is that the in-situ density is about $18.7\,\mathrm{kg\,m^{-3}}$ greater than its potential density $\sigma_0$, a difference almost entirely attributable to compressibility.

### The Modern Thermodynamic Framework: TEOS-10 and Conservative Temperature

While potential temperature and [potential density](@entry_id:1129991) are foundational concepts that greatly improve upon in-situ variables, they possess a subtle but critical flaw related to the concept of "heat content." In thermodynamics, the quantity that correctly represents the heat content of a system subject to pressure changes and mixing is **enthalpy**, not temperature.

The specific heat capacity of seawater, $c_p$, which links temperature changes to enthalpy changes, is not constant; it is a complex function of temperature, salinity, and pressure. This has a profound consequence: when two water parcels are mixed, the potential temperature of the mixture is *not* the mass-weighted average of the initial potential temperatures. This non-conservative behavior under mixing makes $\theta$ an unsuitable variable for accurately diagnosing oceanic heat budgets, which must distinguish between the redistribution of heat by mixing and the addition or removal of heat by external (diabatic) sources  .

To address this and other inaccuracies of the previous standard (EOS-80), the **Thermodynamic Equation of Seawater 2010 (TEOS-10)** was developed. TEOS-10 is built upon a thermodynamically rigorous foundation: a precisely formulated **specific Gibbs potential**, $g(S_A, T, p)$, where $S_A$ is Absolute Salinity, $T$ is in-situ temperature, and $p$ is pressure. From this single function, all thermodynamic properties of seawater can be derived through differentiation. For instance, the specific volume $v = 1/\rho$, specific entropy $\eta$, and specific heat capacity $c_p$ are given by :

$$
v = \left(\frac{\partial g}{\partial p}\right)_{T,S_A} \quad ; \quad \eta = -\left(\frac{\partial g}{\partial T}\right)_{p,S_A} \quad ; \quad c_p = -T\left(\frac{\partial^2 g}{\partial T^2}\right)_{p,S_A}
$$

Within this framework, a new variable, **Conservative Temperature**, denoted $\boldsymbol{\Theta}$, was defined. Conservative Temperature is constructed to be directly proportional to **potential enthalpy**, $h^0$, which is the specific enthalpy a parcel would have if moved adiabatically and isohalinically to a reference pressure of zero . Because enthalpy is an additive quantity, the potential enthalpy of a mixture is the [exact mass](@entry_id:199728)-weighted average of the components' potential enthalpies. As $\Theta$ is linearly proportional to $h^0$, it shares this property of being conserved during isobaric mixing.

Therefore, $\Theta$ is conserved under adiabatic motion *and* under mixing, making it the ideal variable for studying ocean heat content and energetics.

The use of $(S_A, \Theta, p)$ as state variables requires a specific computational pathway. Since the Gibbs function is defined in terms of in-situ temperature $T$, one cannot simply substitute $\Theta$ for $T$. Instead, to find the density $\rho(S_A, \Theta, p)$, one must first numerically solve the implicit equation relating Conservative Temperature to potential enthalpy, $c_p^0 \Theta = h^0(S_A, T, p)$, to find the in-situ temperature $T$. Once $T$ is known, the density is computed using the equation of state $\rho(S_A, T, p)$ derived from the Gibbs function .

Despite the thermodynamic superiority of $\Theta$, potential temperature $\theta$ remains a widely used variable. Its primary modern roles are in the calculation of potential density (which is defined using $\theta$, not $\Theta$) and in the classification of water masses, providing crucial continuity with decades of historical oceanographic data .

### Advanced Topics: The Consequences of Nonlinearity

The equation of state of seawater is nonlinear, and this reality gives rise to complex phenomena that have significant consequences for computational oceanography.

#### Thermobaricity and the Relativity of Potential Density

The [thermal expansion coefficient](@entry_id:150685), $\alpha$, and the haline contraction coefficient, $\beta$, which govern how density responds to changes in temperature and salinity, are themselves functions of pressure. The pressure dependence of $\alpha$ is particularly important and is known as **thermobaricity**. For cold deep water, $\alpha$ increases significantly with pressure .

This has a critical implication: the [relative density](@entry_id:184864) of two water parcels can depend on the reference pressure chosen for the [potential density](@entry_id:1129991) calculation. Consider two deep-ocean parcels, A and B, at the same pressure ($3500\,\mathrm{dbar}$), where A is slightly colder and fresher than B. At a surface reference pressure ($p_r=0\,\mathrm{dbar}$), the haline effect might dominate, making the fresher parcel A appear lighter than B. However, at a deep reference pressure ($p_r=4000\,\mathrm{dbar}$), the larger value of $\alpha$ amplifies the effect of the temperature difference, causing the colder parcel A to appear denser than B .

This demonstrates that surfaces of constant potential density (isopycnals) are not unique material surfaces; their geometry depends on the choice of reference pressure.

#### Neutral Surfaces and Spurious Mixing

The dynamically correct surfaces for analyzing fluid parcel motion and stability are **neutral surfaces**. A neutral surface is one along which a parcel can be moved without experiencing a buoyant restoring force. A potential density surface, $\sigma_{p_r}$, is only an approximation of a true neutral surface. The quality of this approximation is best when the reference pressure $p_r$ is chosen to be close to the local in-situ pressure of the fluid being studied .

Due to [thermobaricity](@entry_id:1133045), the direction defining a local neutral surface is generally different from the direction defining a potential density surface when $p \neq p_r$. The [normal vector](@entry_id:264185) to a neutral surface at pressure $p$ can be written as $\mathbf{g}_n(p) = \alpha(p)\nabla\theta - \beta(p)\nabla S$, whereas the normal to a potential density surface is $\mathbf{g}_{pd}(p_r) = \alpha(p_r)\nabla\theta - \beta(p_r)\nabla S$. Since $\alpha(p) \neq \alpha(p_r)$, these vectors are not parallel, and the angle between them quantifies the misalignment .

This misalignment has profound consequences for ocean modeling. If a model parameterizes subgrid-scale mixing as occurring along isopycnals (e.g., surfaces of constant $\sigma_0$), these surfaces are tilted relative to the true neutral surfaces in the deep ocean. Mixing along these tilted surfaces introduces an artificial component of mixing across the neutral surfaces. This is known as **spurious diapycnal mixing**, an artifact that can seriously corrupt a model's representation of water mass transformation and heat uptake .

To mitigate this, oceanographers use different reference pressures for different depth ranges (e.g., $\sigma_0$ for the upper ocean, $\sigma_2$ for mid-depths around $2000\,\mathrm{dbar}$, and $\sigma_4$ for the abyss). More advanced approaches use specially constructed **neutral density** variables (e.g., $\gamma^n$) that attempt to follow neutral surfaces more faithfully across a range of pressures. However, because of the complex thermodynamics of seawater, which make neutral surfaces mathematically non-integrable (a parcel following a neutral path can spiral and not return to its starting density surface), no single [scalar density](@entry_id:161438) variable can perfectly represent them globally . Understanding these principles is therefore essential for the correct implementation and interpretation of modern ocean circulation models.