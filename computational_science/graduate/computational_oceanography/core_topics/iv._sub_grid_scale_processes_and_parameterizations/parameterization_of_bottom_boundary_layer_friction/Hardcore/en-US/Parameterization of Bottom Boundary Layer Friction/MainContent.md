## Introduction
The interaction between the ocean and the seafloor is a fundamental process that shapes marine environments, yet it occurs at scales too small for most ocean models to resolve directly. The resulting friction in the bottom boundary layer (BBL) acts as a primary sink for oceanic energy, influencing coastal currents, the dissipation of tides, and even the stability of [global circulation patterns](@entry_id:1125664). The critical challenge for computational oceanographers is to represent this complex, turbulent process through an effective parameterization. This article bridges the gap between physical theory and numerical practice, providing a graduate-level guide to understanding and implementing bottom friction in ocean models.

The following chapters will guide you through this essential topic. In "Principles and Mechanisms," we will deconstruct the physics of the [turbulent boundary layer](@entry_id:267922) to derive the foundational [quadratic drag law](@entry_id:1130356). "Applications and Interdisciplinary Connections" will then explore the far-reaching impact of friction on coastal hazards, large-scale dynamics, and [biogeochemical cycles](@entry_id:147568), demonstrating its crucial role across ocean science. Finally, "Hands-On Practices" will provide opportunities to apply these concepts through practical data analysis and modeling exercises, solidifying your understanding of how theory translates into research.

## Principles and Mechanisms

The interaction between oceanic currents and the seabed is a critical process governing coastal and shelf sea dynamics, global ocean circulation, and the transport of sediments, nutrients, and pollutants. The momentum exchange at this interface manifests as a frictional force, or stress, that the fluid exerts on the bed. In computational oceanography, where the fine details of near-bed turbulence cannot be explicitly resolved, this bottom friction must be represented through a parameterization. This chapter elucidates the fundamental principles and mechanisms that underpin modern bottom friction parameterizations, progressing from foundational concepts to the advanced physical processes that modify them.

### Fundamental Concepts of Bottom Stress

The force per unit area exerted by the flowing fluid on the seabed is termed the **bottom shear stress**, denoted by the vector $\boldsymbol{\tau}_b$. From a fluid dynamics perspective, this stress is equivalent to the downward vertical flux of horizontal momentum to the bed. For the vast majority of oceanic flows, the Reynolds number is extremely large, ensuring that the bottom boundary layer (BBL) is turbulent. In a turbulent flow, momentum is transferred not only by molecular viscosity but also, and more importantly, by the chaotic, swirling motions of turbulent eddies.

The total stress at any point is the sum of viscous stress and turbulent stress (known as Reynolds stress). However, within a **hydraulically rough** turbulent boundary layer—a regime where the bed's roughness elements are large enough to disrupt the viscous sublayer—the area-averaged viscous shear at the bed becomes negligible. Instead, the total stress is dominated by two mechanisms: tangential shear on the grain surfaces (**skin friction**) and, more significantly, pressure differences that develop across bluff roughness elements like sediment grains or larger bedforms (**[form drag](@entry_id:152368)**). The momentum is primarily extracted from the flow by the pressure forces acting on these features .

To work with the physics of this turbulent layer, it is convenient to define a velocity scale that is directly related to the stress itself. This is the **[friction velocity](@entry_id:267882)**, $u_*$. It is defined from the magnitude of the bottom shear stress, $\tau_b = |\boldsymbol{\tau}_b|$, and the fluid density, $\rho$, as:

$u_* = \sqrt{\frac{\tau_b}{\rho}}$

or equivalently,

$\tau_b = \rho u_*^2$

This definition is dimensionally consistent, as the units of $\rho u_*^2$ are $(M L^{-3}) \cdot (L T^{-1})^2 = M L^{-1} T^{-2}$, which are the units of stress (force per area, or Pascals). The [friction velocity](@entry_id:267882) $u_*$ is not a directly measurable mean flow velocity at a specific point, but rather a characteristic velocity that scales the intensity of near-bed turbulence and shear .

### The Velocity Profile in a Neutral Boundary Layer

Under idealized conditions of a steady, horizontally uniform, and neutrally stratified (i.e., constant density with depth) flow, the structure of the turbulent BBL takes on a universal form. In the region close to the bed but sufficiently above the individual roughness elements, a "[constant stress layer](@entry_id:747747)" or **inner layer** exists. Here, the total shear stress is approximately constant with height and equal to the [bottom stress](@entry_id:1121796), $\tau_b$.

Classical [mixing-length theory](@entry_id:752030), which models the turbulent [momentum flux](@entry_id:199796), leads to a remarkable result for the mean velocity profile $U(z)$ as a function of height $z$ in this layer. This is the **[logarithmic law of the wall](@entry_id:262057)** for a rough boundary:

$U(z) = \frac{u_*}{\kappa} \ln\left(\frac{z}{z_0}\right)$

This equation is a cornerstone of boundary layer [meteorology](@entry_id:264031) and oceanography . It contains two crucial parameters:

1.  The **von Kármán constant**, $\kappa$, is a dimensionless empirical constant that describes the efficiency of [turbulent momentum transport](@entry_id:1133519). It is considered nearly universal for a wide range of turbulent shear flows, with a value of approximately $\kappa \approx 0.4$.

2.  The **[hydrodynamic roughness length](@entry_id:1126256)**, $z_0$, is the integration constant that emerges from the derivation. It has units of length and represents the extrapolated height at which the idealized [logarithmic velocity profile](@entry_id:187082) would go to zero. It is not the physical height of the roughness elements themselves but a parameter that encapsulates their collective hydrodynamic effect on the overlying flow.

The logarithmic law is not universally valid throughout the water column. Its derivation relies on assumptions that restrict its applicability to the inner part of the BBL. Specifically, it is valid for heights $z$ such that $z \gg z_0$ (well above the roughness sublayer where flow is complex) and $z \ll \delta$, where $\delta$ is the total thickness of the boundary layer. In the ocean, this thickness $\delta$ is often limited by the scale over which Earth's rotation becomes important, a scale proportional to $u_*/f$, where $f$ is the Coriolis parameter. Therefore, the log-law is expected to hold for $z_0 \ll z \ll u_*/f$ in a neutrally stratified, rotating fluid .

### The Quadratic Drag Law Parameterization

While the log-law provides a physical description of the velocity profile, ocean models often operate with grid cells far too large to resolve this structure. These models require a "drag law" that relates the [bottom stress](@entry_id:1121796) $\boldsymbol{\tau}_b$ directly to a representative near-bed velocity, such as the velocity at the lowest model grid point, $U_r$, at height $z_r$.

The [logarithmic law of the wall](@entry_id:262057) provides a direct physical basis for such a drag law. By evaluating the log-law at the reference height $z_r$, we can write:

$U_r = \frac{u_*}{\kappa} \ln\left(\frac{z_r}{z_0}\right)$

Recalling that $\tau_b = \rho u_*^2$, we can solve for $u_*$ in terms of $U_r$ and substitute it into the stress definition:

$\tau_b = \rho \left( \frac{\kappa U_r}{\ln(z_r/z_0)} \right)^2 = \rho \left[ \left( \frac{\kappa}{\ln(z_r/z_0)} \right)^2 \right] U_r^2$

This relationship reveals that for a fully [turbulent boundary layer](@entry_id:267922), the [bottom stress](@entry_id:1121796) is proportional to the square of the near-bed velocity. This is the origin of the ubiquitous **[quadratic drag law](@entry_id:1130356)** . In vector form, to ensure the drag force opposes the flow, it is written as:

$\boldsymbol{\tau}_b = \rho C_d |\boldsymbol{U}_r| \boldsymbol{U}_r$

Here, $\boldsymbol{U}_r$ is the velocity vector at the reference height $z_r$, and $C_d$ is the dimensionless **drag coefficient**. From our derivation, we see that $C_d$ is not an arbitrary constant but is determined by the properties of the logarithmic profile :

$C_d = \left( \frac{\kappa}{\ln(z_r/z_0)} \right)^2$

This formulation serves as a closure, providing the necessary bottom boundary condition for the Reynolds-Averaged Navier-Stokes (RANS) equations used in large-scale models. It is crucial to recognize that the quadratic dependence of stress on speed is a specific consequence of high-Reynolds-number, turbulent flow dynamics. Other regimes, such as slow, viscous (laminar) flows, exhibit a **[linear drag](@entry_id:265409) law** where stress is proportional to velocity. While such laws can arise in simplified oceanographic models (e.g., those assuming a constant eddy viscosity), the quadratic law is the physically appropriate choice for representing fully turbulent bottom friction .

### The Physical Nature of Roughness

The [drag coefficient](@entry_id:276893) $C_d$ is critically dependent on the roughness length $z_0$. Understanding what determines $z_0$ is therefore essential for accurate friction parameterization. As previously mentioned, the total stress arises from two sources: **[skin friction](@entry_id:152983)**, the viscous drag on the surface of individual sediment grains, and **form drag**, the [pressure drag](@entry_id:269633) arising from flow separation around larger bedforms like ripples and dunes .

For a bed composed of granular material but lacking larger bedforms, the roughness is primarily due to the grains themselves. This is often characterized by an **equivalent sand roughness**, $k_s$, which is typically related to the median grain diameter ($d_{50}$), for example, via an empirical relation like $k_s \approx 2.5 d_{50}$. In this grain-only, hydraulically rough regime, classical laboratory experiments (by Nikuradse) and theory show a relationship between $z_0$ and $k_s$:

$z_0 \approx \frac{k_s}{30}$

This gives a baseline estimate for the roughness length based on sediment properties .

However, in many natural environments, the seabed is not flat but is covered with bedforms. The form drag generated by these features can be substantially larger than the skin friction. Since the [logarithmic velocity profile](@entry_id:187082) and the effective roughness $z_0$ are shaped by the *total* stress ($\tau_{tot} = \tau_{skin} + \tau_{form}$), the presence of bedforms leads to a much larger effective $z_0$ than would be predicted from grain size alone.

Consider a hypothetical observation where a measured velocity profile over a sandy seabed ($d_{50} = 0.5 \, \mathrm{mm}$) yields an effective roughness length of $z_0 = 1.8 \, \mathrm{mm}$. The predicted grain roughness would be $k_s \approx 2.5 \times 0.5 \, \mathrm{mm} = 1.25 \, \mathrm{mm}$, corresponding to an expected $z_0 \approx 1.25/30 \approx 0.04 \, \mathrm{mm}$. The observed roughness is over 40 times larger than the grain-only estimate. This large discrepancy strongly indicates that the dominant source of drag is not [skin friction](@entry_id:152983) but [form drag](@entry_id:152368) from unseen bedforms, which are extracting significant momentum from the flow .

### Factors Modifying Bottom Friction

The idealized picture of a neutral boundary layer is often complicated by other physical processes. A robust parameterization scheme must account for these effects.

#### Stratification and Monin-Obukhov Similarity Theory

When the water column is stratified (density varies with depth), buoyancy forces can significantly alter turbulence. **Monin-Obukhov Similarity Theory (MOST)** provides the framework for quantifying this effect. The theory introduces a crucial length scale, the **Obukhov length** ($L$), which represents the height at which the production of [turbulent kinetic energy](@entry_id:262712) by buoyancy becomes comparable to production by shear. It is defined as:

$L = -\frac{u_*^3}{\kappa B_0}$

where $B_0$ is the turbulent [buoyancy flux](@entry_id:261821) at the bed. By convention, a destabilizing buoyancy flux (e.g., from geothermal heating) is positive ($B_0 > 0$), resulting in $L  0$ (unstable conditions). A stabilizing buoyancy flux (e.g., cold, dense water near the bed) is negative ($B_0  0$), resulting in $L > 0$ (stable conditions) .

MOST postulates that the dimensionless [velocity shear](@entry_id:267235) is a universal function, $\phi_m$, of the stability parameter $\zeta = z/L$. The shear profile is thus modified from the neutral law:

$\frac{\partial U}{\partial z} = \frac{u_*}{\kappa z} \phi_m(\zeta)$

Under stable conditions ($\zeta > 0$), buoyancy suppresses turbulent mixing, making it less efficient. To maintain a given stress, the mean shear must increase, thus $\phi_m(\zeta) > 1$. Conversely, under unstable conditions ($\zeta  0$), convective motions enhance mixing, so less shear is required, and $\phi_m(\zeta)  1$. For neutral conditions ($\zeta=0$), we recover the standard log-law, so $\phi_m(0) = 1$ .

This modification directly impacts the drag coefficient. Integrating the modified shear profile (e.g., using a common [linear form](@entry_id:751308) for stable conditions, $\phi_m(\zeta) = 1 + \beta \zeta$) yields a new relationship between $U_r$ and $u_*$. This results in a **dynamic drag coefficient** that depends on stratification . For stable stratification, the drag coefficient decreases because the suppressed turbulence reduces the efficiency of [momentum transfer](@entry_id:147714) to the bed. A dynamic $C_d$ that adapts to changing roughness ($z_0$) and stratification ($L$) allows a model to represent these physical changes, preventing systematic biases in [energy dissipation](@entry_id:147406) and momentum balance.

#### Rotation and Flow Veering

The [quadratic drag law](@entry_id:1130356) relates the [bottom stress](@entry_id:1121796) to the *near-bed* velocity. In the ocean, the Coriolis force causes the velocity vector to rotate with height, a phenomenon known as the **Ekman spiral**. The flow near the bed is turned at an angle relative to the flow higher up in the water column. Since the [bottom stress](@entry_id:1121796) vector $\boldsymbol{\tau}_b$ is oriented anti-parallel to the near-bed velocity, it will generally *not* be anti-parallel to the depth-averaged (barotropic) current. This misalignment, or veering, is a fundamental feature of rotating boundary layers and is influenced by both the Coriolis parameter $f$ and stratification, which modifies the boundary layer's vertical structure .

#### Wave-Current Interaction

On continental shelves, the [orbital motion](@entry_id:162856) from surface gravity waves often dominates the near-bed velocity field. The high-frequency oscillations of the **wave orbital velocity**, $U_w$, generate intense shear and turbulence within a thin **wave boundary layer** near the bed. This wave-generated turbulence is then felt by the much weaker mean current.

The **Grant-Madsen model** and similar theories provide a framework for this interaction. The core idea is that the strong oscillatory shear from waves creates an enhanced level of turbulence, which can be modeled as a large, time-invariant eddy viscosity. This enhanced viscosity dramatically increases the frictional drag experienced by the mean current . This effect is parameterized by using an **enhanced effective roughness**, $z_{0,eff}$, which is a function of the wave parameters ($U_w$, wave period) and the physical roughness $z_0$. Since $z_{0,eff}$ is typically much larger than $z_0$, the resulting drag coefficient for the mean current is significantly increased. This mechanism is another primary reason why observed drag coefficients on shelves are often much larger than those predicted from sediment size alone .

#### Anisotropic Roughness

If the bed roughness elements, such as sand ripples or geological features, have a preferred orientation, the drag they exert will depend on the direction of the flow. In this case, a simple scalar drag coefficient is insufficient. The drag law must be generalized to a tensorial form:

$\boldsymbol{\tau}_b = \rho |\boldsymbol{U}_r| \mathbf{D} \boldsymbol{U}_r$

Here, $\mathbf{D}$ is a dimensionless **drag tensor**. If the bed is anisotropic, $\mathbf{D}$ is not simply the identity matrix multiplied by $C_d$. The action of this tensor on the velocity vector $\boldsymbol{U}_r$ can result in a stress vector $\boldsymbol{\tau}_b$ that is rotated relative to the near-bed flow direction. This is a mechanism for misalignment that is purely due to the geometry of the bed, independent of rotation or stratification  . For the drag to be physically realistic (i.e., always dissipative), the drag tensor $\mathbf{D}$ must be symmetric and positive-definite, ensuring that the rate of energy dissipation is always non-negative.

### The Energetic Role of Bottom Friction

Bottom friction is a primary sink of mechanical energy in the ocean. The rate at which work is done by the bed on the fluid is given by the dot product of the frictional force and the velocity at the point of application. The rate of energy dissipation per unit area, $\epsilon_b$, is therefore:

$\epsilon_b = \boldsymbol{\tau}_b \cdot \boldsymbol{U}_b$

where $\boldsymbol{U}_b$ is the velocity at the bottom. This term appears as a sink ($-\epsilon_b$) in the depth-integrated kinetic [energy equation](@entry_id:156281). Since friction always opposes motion, $\boldsymbol{\tau}_b$ and $\boldsymbol{U}_b$ are generally co-aligned (for isotropic roughness), ensuring that $\epsilon_b$ is a positive-definite quantity .

In a turbulent flow, both the stress and velocity have mean and fluctuating components. Applying Reynolds averaging to the dissipation expression reveals how the total mean dissipation is partitioned:

$\overline{\epsilon_b} = \overline{\boldsymbol{\tau}}_b \cdot \overline{\boldsymbol{U}}_b + \overline{\boldsymbol{\tau}_b' \cdot \boldsymbol{u}_b'}$

The first term, $\overline{\boldsymbol{\tau}}_b \cdot \overline{\boldsymbol{U}}_b$, represents the dissipation of mean flow energy by the [mean stress](@entry_id:751819). The second term, $\overline{\boldsymbol{\tau}_b' \cdot \boldsymbol{u}_b'}$, represents the dissipation associated with the fluctuating components of the flow (e.g., eddies and turbulence). This term is the covariance of the stress and velocity fluctuations and is a crucial pathway for the cascade of energy from larger scales to the small scales where it is ultimately converted to heat .