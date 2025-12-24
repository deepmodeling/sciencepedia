## Introduction
The accurate representation of [moist convection](@entry_id:1128092) is a formidable and long-standing challenge in numerical weather prediction and climate modeling. Because convective clouds, thunderstorms, and their associated circulations are typically far smaller than the grid cells of a global model, their crucial effects on the large-scale atmospheric state cannot be resolved directly. This knowledge gap necessitates the use of parameterization schemes—simplified physical models that represent the collective impact of this subgrid-scale activity. While simple approaches exist, they often fail to capture the complex, nonlocal transport of heat, moisture, and momentum that characterizes convection.

This article provides a comprehensive overview of the dominant framework used to address this challenge: the [mass-flux parameterization](@entry_id:1127657) of convective plumes. Across the following chapters, you will gain a graduate-level understanding of this essential modeling component. We will begin in the **Principles and Mechanisms** chapter by dissecting the core physics of [entrainment](@entry_id:275487), detrainment, and downdrafts, establishing the foundational equations that govern mass exchange between a convective plume and its environment. Next, the **Applications and Interdisciplinary Connections** chapter will bridge theory and practice, exploring how these principles are implemented in modern [weather and climate models](@entry_id:1134013), their critical role in simulating phenomena from squall lines to the Madden-Julian Oscillation, and their surprising relevance to fields like planetary science. Finally, the **Hands-On Practices** section offers a chance to engage directly with the material, tackling problems that illuminate the practical consequences of different modeling choices. Together, these sections will equip you with the knowledge to understand, evaluate, and critically analyze one of the most important components of modern Earth system models.

## Principles and Mechanisms

The representation of subgrid-scale [moist convection](@entry_id:1128092) is a central challenge in [numerical weather prediction](@entry_id:191656) (NWP) and climate modeling. Because convective clouds and their associated circulations are often much smaller than a typical model grid cell, their collective effects on the large-scale state must be parameterized. At the heart of many such parameterizations is the concept of a convective plume—an idealized, [one-dimensional representation](@entry_id:136509) of a coherent updraft or downdraft that interacts with its surrounding environment. This chapter elucidates the fundamental principles and mechanisms governing these interactions: [entrainment](@entry_id:275487), detrainment, and the dynamics of convective downdrafts.

### The Mass-Flux Framework: Entrainment and Detrainment

We begin by conceptualizing a convective updraft or downdraft as a distinct entity, or **plume**, occupying a fractional area of a model grid column. This plume can be treated as a control volume that exchanges mass, momentum, and thermodynamic properties with the much larger environmental region of the column. The vertical mass flux within the plume, denoted by $M(z)$ in units of $\mathrm{kg}\cdot\mathrm{m}^{-2}\cdot\mathrm{s}^{-1}$, represents the net upward or downward transport of mass by the coherent convective motion. By convention, $M(z) > 0$ for an updraft and $M(z)  0$ for a downdraft.

The change in this mass flux with height, $z$, is governed by two fundamental processes:

1.  **Entrainment ($E$)**: The lateral incorporation of environmental air into the plume.
2.  **Detrainment ($D$)**: The lateral expulsion of plume air into the environment.

These are defined as rates of mass exchange per unit vertical distance, with units of $\mathrm{kg}\cdot\mathrm{m}^{-2}\cdot\mathrm{s}^{-1}\cdot\mathrm{m}^{-1}$. Considering a thin horizontal slab of the plume between $z$ and $z+dz$, mass conservation for a steady-state plume requires that the change in vertical mass flux, $M(z+dz) - M(z)$, must be balanced by the net lateral exchange within that slab. This leads to the fundamental plume mass continuity equation :

$$
\frac{dM}{dz} = E(z) - D(z)
$$

This equation states that the vertical mass flux of the plume increases in regions where [entrainment](@entry_id:275487) dominates detrainment ($E > D$) and decreases where detrainment is dominant ($D > E$).

For convenience in parameterization schemes, it is common to define **fractional [entrainment and detrainment](@entry_id:1124548) rates**, denoted by $\varepsilon(z)$ and $\delta(z)$ respectively, which have units of inverse length ($\mathrm{m}^{-1}$). These are defined as the mass exchange rates normalized by the plume's own mass flux:

$$
\varepsilon(z) \equiv \frac{E(z)}{|M(z)|}, \quad \delta(z) \equiv \frac{D(z)}{|M(z)|}
$$

Substituting these definitions into the mass budget equation yields a commonly used form:

$$
\frac{dM}{dz} = (\varepsilon(z) - \delta(z)) |M(z)|
$$

This framework forms the backbone of all **[mass-flux parameterization](@entry_id:1127657) schemes**. It represents the organized, coherent transport by convective plumes, a process that is physically distinct from the smaller-scale, more random turbulent mixing that occurs throughout the atmospheric column.

### The Physical Basis of Entrainment Parameterization

The necessity of parameterizing [entrainment and detrainment](@entry_id:1124548) arises because the processes themselves are fundamentally subgrid-scale. The mixing occurs across the turbulent interface of a convective cloud, which has a characteristic radius, $R$, and internal turbulence with length scales, $L$, that are typically much smaller than the horizontal grid spacing, $\Delta x$, of a large-scale model. Therefore, the filtered governing equations solved by the model do not explicitly resolve this lateral exchange, and its effect on the grid-mean state must be represented through a parameterization .

A cornerstone of [entrainment](@entry_id:275487) theory is the hypothesis, first advanced by Morton, Taylor, and Turner, that the lateral velocity of environmental air entrained into a turbulent plume, $v_{in}$, is proportional to the plume's own mean vertical velocity, $w$. This can be written as $v_{in} = \alpha w$, where $\alpha$ is a dimensionless entrainment coefficient. From this, we can derive a powerful scaling law for the fractional [entrainment](@entry_id:275487) rate, $\varepsilon$. The rate of mass increase per unit height, $dM/dz$, is the product of the plume perimeter ($2\pi R$), density ($\rho$), and the inflow velocity ($v_{in}$):

$$
\frac{dM}{dz} \approx \rho (2\pi R) v_{in} = \rho (2\pi R) (\alpha w)
$$

Recalling the definition of mass flux for a simple top-hat plume, $M = \rho (\pi R^2) w$, the fractional entrainment rate is:

$$
\varepsilon = \frac{1}{M} \frac{dM}{dz} = \frac{1}{\rho \pi R^2 w} (2 \pi \alpha \rho w R) = \frac{2\alpha}{R}
$$

This elegantly simple result, $\varepsilon \propto 1/R$, reveals that the fractional [entrainment](@entry_id:275487) rate is inversely proportional to the plume radius . This has profound implications for modeling different types of convection:
-   **Shallow Convection**: Characterized by narrow plumes ($R$ is small), [shallow convection](@entry_id:1131529) experiences a large fractional entrainment rate. This leads to rapid dilution of the plume's buoyancy and moisture, helping to explain why these clouds remain shallow and have a significant impact on boundary layer structure. Near cloud base, where $R$ is smallest, $\varepsilon$ is at its maximum and decreases with height as the plume widens.
-   **Deep Convection**: The protected cores of deep convective storms are characterized by a large radius ($R$ is large). Consequently, their fractional [entrainment](@entry_id:275487) rate is much smaller. These "undiluted" cores are better able to preserve the high energy and moisture content from the boundary layer, allowing them to ascend through the full depth of the troposphere.

The focus of this one-dimensional [plume model](@entry_id:1129836) on lateral exchange is physically justified. For a typical deep cumulus updraft, the timescale for a parcel to be advected vertically through the cloud depth ($t_{\mathrm{adv}} = H/w$) is much shorter than the timescale for turbulent motions to mix properties horizontally across the plume's radius ($t_{\mathrm{mix}} = R^2/K_t$, where $K_t$ is an eddy diffusivity). The ratio of these timescales, a form of the **Péclet number**, is typically large ($Pe \gg 1$), indicating that vertical advection dominates internal mixing. For example, for an updraft with height $H = 10 \, \mathrm{km}$, velocity $w = 10 \, \mathrm{m\,s^{-1}}$, radius $R = 500 \, \mathrm{m}$, and internal diffusivity $K_t = 50 \, \mathrm{m^2\,s^{-1}}$, the advection timescale is $1000 \, \mathrm{s}$ while the internal mixing timescale is $5000 \, \mathrm{s}$. This five-fold difference confirms that the primary control on the evolution of the plume's mean properties is the continuous lateral entrainment of environmental air, not the redistribution of properties within the core .

### Thermodynamic Consequences and Closure

Entrainment fundamentally alters a plume's thermodynamic properties by mixing in environmental air, which is typically cooler, drier, and less energetic than a buoyant updraft parcel. This dilution process directly reduces the plume's buoyancy and, consequently, the total energy available for convection. This can be quantified by examining the **Convective Available Potential Energy (CAPE)**, defined as the vertical integral of parcel buoyancy, $B(z)$. The buoyancy is approximately $B(z) \approx g (\theta_{v,p}(z) - \theta_{v,e}(z))/\theta_{v,e}(z)$, where $\theta_{v,p}$ and $\theta_{v,e}$ are the virtual potential temperatures of the parcel and environment, respectively.

Entrainment causes the parcel's [virtual potential temperature](@entry_id:1133825) excess, $\Delta\theta_v(z) = \theta_{v,p}(z) - \theta_{v,e}(z)$, to decay with height. For a simple case with a constant fractional [entrainment](@entry_id:275487) rate, $\varepsilon_0$, this decay is exponential: $\Delta\theta_v(z) \propto \exp(-\varepsilon_0 z)$. The CAPE for an entraining parcel, $\text{CAPE}_{\text{entr}}$, is therefore significantly less than the CAPE of an undilute parcel, $\text{CAPE}_0$. The reduction, $\Delta\text{CAPE} = \text{CAPE}_0 - \text{CAPE}_{\text{entr}}$, can be calculated analytically. For a layer of depth $L$ with initial buoyancy excess proportional to $\Delta\theta_{v0}$, the CAPE lost to [entrainment](@entry_id:275487) is :

$$
\Delta\text{CAPE} = g \frac{\Delta \theta_{v0}}{\theta_{v,e}} \left[ L - \frac{1 - \exp(-\varepsilon_0 L)}{\varepsilon_0} \right]
$$

While [entrainment](@entry_id:275487) governs how a plume is modified on its way up, detrainment governs where it deposits its mass and energy. A widely used closure for this is the **zero-buoyancy detrainment hypothesis**. This principle posits that plume air preferentially detrains at the level where it becomes neutrally buoyant with the environment, i.e., at the height $z^*$ where $B(z^*) = 0$. At this level, the density of the plume matches the environment ($\rho_p = \rho_e$). A parcel exiting the plume laterally experiences no initial vertical buoyancy force, removing the primary barrier to mixing. This **Level of Neutral Buoyancy (LNB)** is therefore the natural termination height for a convective updraft .

The thermodynamics of these processes are distinct. The ascent of an air parcel within the core of the plume, retaining its condensed water, is modeled as a reversible, moist-adiabatic process, for which moist entropy ($s$) or liquid-[water potential](@entry_id:145904) temperature ($\theta_l$) are conserved. Entrainment itself is an irreversible mixing process. Detrainment, which occurs after some condensed water has been converted to precipitation and has fallen out, is fundamentally an irreversible, pseudoadiabatic process. For such a process, the approximately conserved quantity is the equivalent potential temperature ($\theta_e$). The detrained air, having been warmed by latent heat release during its ascent, has higher entropy than the surrounding environment, while its total water content has been depleted by precipitation .

### The Role and Representation of Downdrafts

Convection is a full circulation, and updrafts are only half the story. The descending branches of the circulation, or **downdrafts**, are equally crucial for transporting low-entropy air to the boundary layer and regulating the life cycle of convection. In [mass-flux schemes](@entry_id:1127658), the column is often partitioned into three regions: updraft, downdraft, and environment, with corresponding mass fluxes $M_u(z)$, $M_d(z)$, and $M_e(z)$. Mass conservation for the entire column requires that the sum of these fluxes is zero at every level, a consequence of the [anelastic approximation](@entry_id:1121006) applied to a horizontally homogeneous domain. This gives the fundamental constraint that links the convective plumes to their environment :

$$
M_u(z) + M_d(z) + M_e(z) = 0
$$

This equation shows that the vertical motion in the updrafts and downdrafts must be compensated by a return flow, or subsidence, in the environment, so that $M_e(z) = -(M_u(z) + M_d(z))$.

Downdrafts are primarily driven by negative buoyancy, which is generated by two main mechanisms: the loading effect of precipitation and cooling due to the evaporation of that precipitation into subsaturated environmental air. The total energy available for a downdraft is quantified by the **Downdraft Convective Available Potential Energy (DCAPE)**, defined as the integral of negative buoyancy along the parcel's descent path from a starting level $z_t$ to a base level $z_b$:

$$
\text{DCAPE} \equiv \int_{z_b}^{z_t} -B_d(z) dz
$$

For an idealized, non-mixing downdraft parcel starting from rest, DCAPE is exactly equal to the kinetic energy per unit mass, $w^2/2$, gained by the parcel upon reaching the base level . It is the [work-energy theorem](@entry_id:168821) for the downdraft. Just as entrainment weakens updrafts, it also weakens downdrafts. By mixing in warmer and drier environmental air, [entrainment](@entry_id:275487) reduces the downdraft's negative buoyancy at every level. This means that the DCAPE calculated for an undilute parcel represents a theoretical upper bound on the kinetic energy that a realistic, entraining downdraft can achieve.

### Synthesis with Diffusive Turbulence Schemes

It is important to recognize that the [mass-flux framework](@entry_id:1127656) described here represents one component of subgrid turbulence. It excels at capturing the organized, [non-local transport](@entry_id:1128806) by coherent structures, which can even transport properties *against* the mean gradient (e.g., transporting moisture upward into a dry mid-troposphere). This is fundamentally different from traditional turbulence [closures](@entry_id:747387) based on **eddy-diffusivity**, where the turbulent flux is parameterized as a down-gradient process proportional to an eddy-diffusivity coefficient, $K$. These two approaches are not mutually exclusive but are complementary. Mass-flux parameters like $\varepsilon$ and $\delta$ have units of inverse length and describe organized exchange at a plume interface, whereas $K$ has units of area per time and describes disorganized, local diffusion.

Modern parameterizations, known as **Eddy-Diffusivity Mass-Flux (EDMF)** schemes, unify these two perspectives. In an EDMF framework, the total subgrid-scale vertical flux is partitioned into a coherent mass-flux component and a diffusive component. The mass-flux part, governed by [entrainment and detrainment](@entry_id:1124548), handles the strong, organized plumes, while the eddy-diffusivity part represents the smaller-scale, more [isotropic turbulence](@entry_id:199323) in the environment. This hybrid approach provides a more complete and physically consistent representation of the full spectrum of turbulent motions within a model grid cell .