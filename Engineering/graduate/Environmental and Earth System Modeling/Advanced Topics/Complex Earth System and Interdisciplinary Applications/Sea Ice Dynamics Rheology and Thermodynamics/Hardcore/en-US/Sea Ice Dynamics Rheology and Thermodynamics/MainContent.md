## Introduction
Sea ice is a critical and dynamic component of the Earth's climate system, influencing global energy balance, ocean circulation, and polar ecosystems. However, its behavior is uniquely complex, existing at the interface of fluid dynamics, solid mechanics, and thermodynamics. To accurately simulate and predict the future of Earth's polar regions, it is essential to build a robust physical understanding of how sea ice moves, deforms, and evolves. This article addresses the challenge of modeling this complex material by systematically deriving its governing principles from first principles.

This article will guide you through the foundational physics of sea ice modeling. The first chapter, "Principles and Mechanisms," establishes the core physical laws, from the momentum equation that governs large-scale motion to the [viscous-plastic rheology](@entry_id:1133845) defining its mechanical failure and the thermodynamic rules controlling its growth and melt. The second chapter, "Applications and Interdisciplinary Connections," demonstrates how these principles are applied to understand real-world phenomena, such as the [ice-albedo feedback](@entry_id:199391), and how they are synthesized within comprehensive Earth System Models. Finally, "Hands-On Practices" provides a set of problems designed to solidify your understanding of these key concepts, bridging theory with practical application.

## Principles and Mechanisms

The behavior of sea ice is governed by a complex interplay of dynamical and thermodynamical processes that span a vast range of spatial and temporal scales. To model this behavior, we must first establish the fundamental physical laws that describe its motion, its internal deformation, and its exchange of energy with the ocean and atmosphere. This chapter lays out these foundational principles, beginning with the conservation of momentum to describe large-scale motion, proceeding to the constitutive laws that define the unique mechanical response of sea ice, and finally examining the thermodynamic processes that drive its growth and melt.

### The Sea Ice Momentum Balance

The motion of sea ice across the ocean surface is governed by Newton's second law, which states that the acceleration of a body is proportional to the net force acting upon it. For sea ice, treated as a two-dimensional continuum, this principle is expressed through the **[sea ice momentum equation](@entry_id:1131344)**. This equation balances the inertia of the ice against a set of forces, including external stresses from the wind and ocean, internal stresses transmitted through the ice pack, and body forces arising from the Earth's rotation and gravity.

For a parcel of sea ice with a mass per unit horizontal area of $m$, moving with a two-dimensional velocity $\mathbf{u}$, the momentum balance is given by:

$$m \frac{D\mathbf{u}}{Dt} = \boldsymbol{\tau}_a + \boldsymbol{\tau}_o + \nabla \cdot \boldsymbol{\sigma} - m f \hat{\mathbf{k}} \times \mathbf{u} - m g \nabla \eta$$

Let us deconstruct each term in this fundamental equation. 

*   **Inertia ($m \frac{D\mathbf{u}}{Dt}$):** This term represents the rate of change of momentum per unit area. The mass per unit area, $m$, is defined as $m = \rho_i h c$, where $\rho_i$ is the density of pure ice, $h$ is the mean ice thickness, and $c$ is the ice concentration (the fraction of the area covered by ice). The [material derivative](@entry_id:266939), $\frac{D\mathbf{u}}{Dt} = \frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla)\mathbf{u}$, accounts for both the [local acceleration](@entry_id:272847) at a fixed point ($\frac{\partial \mathbf{u}}{\partial t}$) and the advective acceleration due to the ice moving through a spatially varying velocity field ($(\mathbf{u} \cdot \nabla)\mathbf{u}$). In many large-scale models, the advective term is neglected as a "slow-flow" approximation, since ice velocities are typically small.

*   **Interfacial Stresses ($\boldsymbol{\tau}_a$ and $\boldsymbol{\tau}_o$):** These are the external forces per unit area applied to the top and bottom surfaces of the ice. The **air-ice stress**, $\boldsymbol{\tau}_a$, is the force exerted by the wind, while the **ocean-ice stress**, $\boldsymbol{\tau}_o$, is the drag force exerted by the underlying ocean current. These are not body forces, but rather boundary stresses integrated into the 2D framework.

*   **Internal Stress Divergence ($\nabla \cdot \boldsymbol{\sigma}$):** This term represents the net internal force per unit area arising from mechanical interactions within the ice pack, such as collisions between floes, shearing, and resistance to compression. Here, $\boldsymbol{\sigma}$ is the two-dimensional, thickness-integrated internal stress tensor, with units of force per unit length (e.g., N/m). Its divergence, $\nabla \cdot \boldsymbol{\sigma}$, has units of force per unit area (N/m$^2$). This formulation is a critical distinction from standard fluid dynamics. In the Navier-Stokes equations for a simple fluid, stress is separated into an isotropic thermodynamic pressure and a viscous stress. For sea ice, all internal resistance to deformation, including any pressure-like compressive strength, is encapsulated within the single tensor $\boldsymbol{\sigma}$, which is defined by the ice's **[rheology](@entry_id:138671)**. Sea ice can sustain significant compressive and shear stresses up to a failure point, a plastic behavior not found in Newtonian fluids.  

*   **Coriolis Force ($- m f \hat{\mathbf{k}} \times \mathbf{u}$):** This is an apparent (or inertial) force that arises from describing motion in the Earth's [rotating reference frame](@entry_id:175535). It acts per unit area on the moving ice mass $m$, is directed perpendicular to the velocity vector $\mathbf{u}$ (to the right in the Northern Hemisphere, where the Coriolis parameter $f > 0$), and is proportional to the ice speed. The vector $\hat{\mathbf{k}}$ is the [unit vector](@entry_id:150575) in the vertical direction. This term is structurally identical to the Coriolis force in the [shallow-water equations](@entry_id:754726), with the ice mass per unit area $m$ playing the role of the water column mass per unit area. 

*   **Sea Surface Tilt Force ($- m g \nabla \eta$):** This term represents the [gravitational force](@entry_id:175476) per unit area acting on the ice mass as it rests on a sloping sea surface. Here, $g$ is the acceleration due to gravity and $\eta$ is the sea surface height, so $\nabla \eta$ is the sea surface slope. This force is analogous to the pressure gradient force in the [shallow-water equations](@entry_id:754726) and acts to move the ice "downhill" along the slope of the sea surface. 

### External Forcing: Interfacial Stresses

The momentum balance is driven by the external stresses, $\boldsymbol{\tau}_a$ and $\boldsymbol{\tau}_o$. Accurately parameterizing these fluxes is a central challenge in sea ice modeling.

#### Air-Ice Stress

The stress imparted by the wind is typically parameterized using a **[bulk aerodynamic formula](@entry_id:1121923)** or **drag law**. A simple form is the [quadratic drag law](@entry_id:1130356):

$$\boldsymbol{\tau}_a = \rho_a C_a |\mathbf{U}_a| \mathbf{U}_a$$

where $\rho_a$ is the air density, $\mathbf{U}_a$ is the wind velocity vector at a reference height (e.g., 10 m) relative to the ice, and $C_a$ is a dimensionless [drag coefficient](@entry_id:276893). While simple, using a constant $C_a$ is a significant idealization.

A more physically robust approach is based on **Monin-Obukhov Similarity Theory (MOST)**, which accounts for the influence of atmospheric stability on turbulent exchange.  In this framework, the [drag coefficient](@entry_id:276893) is not constant but depends on the [surface roughness](@entry_id:171005) and the stability of the atmospheric boundary layer. The effective [drag coefficient](@entry_id:276893), $C_d$, can be expressed as:

$$C_d(z_r, L, z_0) = \left[ \frac{\kappa}{\ln(z_r/z_0) - \psi_m(z_r/L)} \right]^2$$

Here, $\kappa$ is the von Kármán constant, $z_r$ is the reference height, $z_0$ is the aerodynamic roughness length of the surface, $L$ is the Obukhov length that quantifies stability, and $\psi_m$ is an empirical stability correction function.

The effect of stability is crucial:
*   **Stable Conditions ($L > 0$):** This occurs when the air is colder than the ice surface, suppressing vertical turbulent mixing. This suppression reduces the efficiency of [momentum transfer](@entry_id:147714), leading to a *smaller* effective drag coefficient and a weaker air-ice stress for a given wind speed.
*   **Unstable Conditions ($L  0$):** This occurs when the air is warmer than the ice, enhancing turbulent mixing through convection. This enhancement increases the efficiency of momentum transfer, leading to a *larger* effective [drag coefficient](@entry_id:276893) and a stronger air-ice stress.

For instance, for a typical 10-m wind of $8 \, \mathrm{m\,s^{-1}}$ over sea ice with a roughness of $z_0 = 5 \times 10^{-4} \, \mathrm{m}$, a constant [drag coefficient](@entry_id:276893) of $C_a = 1.5 \times 10^{-3}$ would yield a stress of about $0.125 \, \mathrm{N\,m^{-2}}$. Under unstable conditions ($L = -50 \, \mathrm{m}$), the stability-corrected stress would be significantly higher, around $0.15 \, \mathrm{N\,m^{-2}}$, whereas under stable conditions ($L = +50 \, \mathrm{m}$), it would be lower, around $0.11 \, \mathrm{N\,m^{-2}}$. Ignoring stability can thus lead to substantial errors in the primary driving force on the ice. 

#### Ocean-Ice Stress

Similarly, the drag from the ocean is parameterized based on the relative velocity between the ice and the ocean current, $\mathbf{U} - \mathbf{u}$. Two common forms are the [linear and quadratic drag](@entry_id:261257) laws. 

*   **Linear Drag:** $\boldsymbol{\tau}_o = C_L (\mathbf{U} - \mathbf{u})$
*   **Quadratic Drag:** $\boldsymbol{\tau}_o = \rho_w C_d |\mathbf{U} - \mathbf{u}| (\mathbf{U} - \mathbf{u})$

Here, $C_L$ is a dimensional drag coefficient, while $\rho_w$ is water density and $C_d$ is a dimensionless [drag coefficient](@entry_id:276893). While seemingly a minor detail, the choice of closure has profound implications for the predicted ice motion.

Consider an idealized case of **steady free drift**, where an ice floe moves under the sole influence of an ocean current $\mathbf{U}$ and the Coriolis force (i.e., $\boldsymbol{\tau}_a = \mathbf{0}$ and $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$). The [momentum balance](@entry_id:1128118) simplifies to $\boldsymbol{\tau}_o = -m f \hat{\mathbf{k}} \times \mathbf{u}$.
*   With **[linear drag](@entry_id:265409)**, solving this balance shows that the ice velocity $\mathbf{u}$ is deflected from the ocean current direction $\mathbf{U}$ by an angle that is *constant* and independent of the current speed. The deflection angle depends only on the ratio of the Coriolis parameter to the [drag coefficient](@entry_id:276893), $\arctan(mf/C_L)$.
*   With **quadratic drag**, the solution reveals a very different behavior. The deflection angle is not constant but *decreases* as the ocean current speed increases. In very strong currents, the ice is dragged along with almost no deflection, whereas in weak currents, the deflection angle approaches $90^\circ$. This velocity-dependent behavior arises from the nonlinear nature of the [quadratic drag law](@entry_id:1130356) and more accurately reflects the physics of turbulent boundary layers. 

### Internal Mechanics: Sea Ice Rheology

The term $\nabla \cdot \boldsymbol{\sigma}$ in the momentum equation represents the forces that arise from the ice pack resisting deformation. The relationship between the [internal stress](@entry_id:190887) $\boldsymbol{\sigma}$ and the rate of deformation is called the **rheology**, and it defines the mechanical character of sea ice.

#### Kinematics of Deformation

To define [rheology](@entry_id:138671), we must first quantify how the ice pack is deforming. This is described by the **[strain rate tensor](@entry_id:198281)**, $\dot{\boldsymbol{\epsilon}}$. For a 2D velocity field $\mathbf{u}(x,y)$, the strain rate is the symmetric part of the [velocity gradient tensor](@entry_id:270928):

$$\dot{\boldsymbol{\epsilon}} = \frac{1}{2} (\nabla \mathbf{u} + (\nabla \mathbf{u})^\top)$$

The components of this tensor describe specific types of deformation. For $\mathbf{u}=(u,v)$:
*   $\dot{\epsilon}_{xx} = \partial_x u$ and $\dot{\epsilon}_{yy} = \partial_y v$ are the **[normal strain](@entry_id:204633) rates**, representing stretching or compression along the coordinate axes.
*   $\dot{\epsilon}_{xy} = \frac{1}{2}(\partial_y u + \partial_x v)$ is the **[shear strain rate](@entry_id:189459)**, representing the change in angle between initially [perpendicular lines](@entry_id:174147).

The anti-symmetric part of the [velocity gradient](@entry_id:261686) describes [rigid-body rotation](@entry_id:268623) (vorticity) and does not contribute to the deformation of the material itself. Therefore, rheological laws are based on $\dot{\boldsymbol{\epsilon}}$. 

Any strain rate can be decomposed into two fundamental modes: a change in area ([volumetric strain](@entry_id:267252)) and a change in shape ([shear strain](@entry_id:175241)). These are captured by two key **invariants** of the [strain rate tensor](@entry_id:198281):
1.  **Divergence:** $I_1 = \text{tr}(\dot{\boldsymbol{\epsilon}}) = \dot{\epsilon}_{xx} + \dot{\epsilon}_{yy} = \nabla \cdot \mathbf{u}$. This measures the rate of fractional area change.
2.  **Effective Shear Strain Rate:** $\Delta = \sqrt{(\dot{\epsilon}_{xx} - \dot{\epsilon}_{yy})^2 + 4\dot{\epsilon}_{xy}^2}$. This quantity is derived from the **deviatoric** part of the [strain rate tensor](@entry_id:198281) (the part with the volumetric change removed) and measures the magnitude of the shape-changing deformation. 

#### The Viscous-Plastic Constitutive Law

Sea ice is neither a simple solid nor a simple liquid. It flows like a highly viscous fluid over long timescales but can also fracture and fail like a brittle solid under rapid forcing. This dual nature is captured by a **viscous-plastic (VP) [rheology](@entry_id:138671)**.

In a typical VP model, the stress tensor $\boldsymbol{\sigma}$ is related to the [strain rate tensor](@entry_id:198281) $\dot{\boldsymbol{\epsilon}}$ through effective bulk and shear viscosities, $\zeta$ and $\eta$:

$$\boldsymbol{\sigma} = 2\eta \dot{\boldsymbol{\epsilon}} + (\zeta - \eta)(\nabla \cdot \mathbf{u}) \mathbf{I} - \frac{P}{2} \mathbf{I}$$

A crucial feature of this model is that the viscosities are not constant. They depend on the strain rate itself and on the ice strength, $P$. The formulation is designed such that:
*   Resistance to area change (divergence) is very high, enforced by a large [bulk viscosity](@entry_id:187773) $\zeta$. This reflects the fact that it is difficult to compress a field of ice floes, making the ice pack [nearly incompressible](@entry_id:752387) on large scales.
*   Resistance to shape change (shear) is governed by a [shear viscosity](@entry_id:141046) $\eta$ that decreases as the deformation rate increases. This allows the ice to yield and "flow" plastically when the internal stress reaches a predefined failure envelope (often represented as an ellipse in [stress space](@entry_id:199156)).

The onset of this [plastic flow](@entry_id:201346) is primarily controlled by the **deviatoric** (shape-changing) components of the strain rate, as the volumetric changes are so strongly resisted. When shearing or non-uniform compression deforms the ice pack, the internal stress builds until it reaches the yield strength, at which point the ice fails. 

#### Mechanisms of Plastic Failure: Ridging

The most dramatic manifestation of plastic failure in sea ice is **pressure ridging**. When two regions of the ice pack converge ($\nabla \cdot \mathbf{u}  0$), the compressive stress builds until the ice buckles and fractures. The broken pieces of ice pile up, forming a ridge with a portion extending above the water line (the **sail**) and a much larger portion extending below (the **keel**).

The formation of these ridges can be understood through an energy balance. The mechanical work done by the stress field to deform the ice is converted into the gravitational potential energy required to lift the ice blocks and stack them into the sail and keel.  A simplified work-energy budget equates the mechanical work per unit length, $W_{\text{mech}}$, to the change in potential energy, $\Delta E_p$:

$$W_{\text{mech}} = \Delta E_p$$

The mechanical work done by a compressive [yield stress](@entry_id:274513) $\sigma_y$ to shorten a slab of ice of thickness $h$ by a length $\ell$ is $W_{\text{mech}} = \sigma_y h \ell$. This work goes into creating the ridge. The change in potential energy is the difference between the final potential energy of the ice rubble in the ridge and the initial potential energy of the level ice from which it formed. This change depends on the geometry of the sail and keel, the densities of ice ($\rho_i$) and water ($\rho_w$), the porosity of the ridge rubble ($\phi$), and gravity ($g$). For a ridge with sail height $s$ and keel depth $k$ formed from a uniform ice sheet, a detailed calculation yields the following balance:

$$\sigma_y (1 - \phi) (s + k) = \rho_i g \left[ \frac{s^2 - k^2}{3} - (1 - \phi) (s + k) h \left( \frac{1}{2} - \frac{\rho_i}{\rho_w} \right) \right]$$

This equation provides a powerful link between the macroscopic strength of the ice pack ($\sigma_y$) and the geometric outcome of its failure ($s, k$), forming a key component of models that parameterize the evolution of the [ice thickness distribution](@entry_id:1126327). 

### Sea Ice Thermodynamics

While dynamics and rheology govern the motion and fracture of sea ice, thermodynamics controls its very existence—its formation, growth, and decay.

#### The Foundation: Phase Equilibrium in Seawater

Unlike freshwater, which freezes at a fixed temperature of $0^\circ \text{C}$ (at standard pressure), seawater freezes at a lower temperature that depends on its salinity. This phenomenon, known as **[freezing point depression](@entry_id:141945)**, is a **[colligative property](@entry_id:191452)**, meaning it depends on the concentration of solute particles (dissolved salts) rather than their specific identity.

The presence of salts lowers the chemical potential of the liquid water. For ice to form, the temperature must drop to a point where the chemical potential of water in the solid phase (pure ice) equals the lowered chemical potential in the liquid phase (brine). Based on thermodynamic principles, for salinities typical of the ocean, this leads to a nearly linear relationship between the Absolute Salinity $S$ (in $\mathrm{g\,kg^{-1}}$) and the freezing temperature $T_f$ (in $^\circ \text{C}$):

$$T_f(S) \approx -\mu S$$

The proportionality constant, $\mu$, is derived from fundamental thermodynamic properties including the [cryoscopic constant](@entry_id:141749) of water and the effective [molar mass](@entry_id:146110) of sea salts. Its empirically determined value is approximately $\mu \approx 0.055 \, \mathrm{K} / (\mathrm{g\,kg^{-1}})$. This simple relationship is a cornerstone of [sea ice thermodynamics](@entry_id:1131346), setting the temperature at which ice can form and coexist with seawater. 

#### Growth and Melt: The Surface Energy Balance

The temperature of the ice surface, and whether it is melting or accumulating snow, is determined by the **surface energy balance**. This is an accounting of all energy fluxes at the ice-atmosphere interface. Assuming a positive-downward sign convention, the net [energy flux](@entry_id:266056) available at the surface, $F_{\text{net}}$, is given by:

$$F_{\text{net}} = (1-\alpha)S_{\text{SW}} + L_{\text{net}} + F_{\text{sens}} + F_{\text{lat}} - F_c$$

If $F_{\text{net}} > 0$, there is a surplus of energy available to warm the surface or melt ice. If $F_{\text{net}}  0$, there is a deficit that will cool the surface. The components are: 
*   **Absorbed Shortwave Radiation ($(1-\alpha)S_{\text{SW}}$):** The incoming solar radiation ($S_{\text{SW}}$) that is not reflected. The surface **albedo** ($\alpha$), or reflectivity, is a critical parameter, as it controls this primary energy input.
*   **Net Longwave Radiation ($L_{\text{net}}$):** The difference between the downwelling infrared radiation from the atmosphere and clouds ($L_{\downarrow}$) and the upwelling infrared radiation emitted by the ice surface itself ($L_{\uparrow} = \varepsilon \sigma T_s^4$, where $T_s$ is the surface temperature).
*   **Sensible Heat Flux ($F_{\text{sens}}$):** The turbulent transfer of heat due to the temperature difference between the air and the ice surface.
*   **Latent Heat Flux ($F_{\text{lat}}$):** The energy flux associated with [phase changes](@entry_id:147766) of water at the surface, such as evaporation/sublimation (cooling) or condensation/deposition (warming).
*   **Conductive Heat Flux ($F_c$):** The heat conducted from the surface *into* the ice interior. This represents an energy loss from the surface.

This balance equation is the central diagnostic tool for understanding and modeling the thermal state of the ice surface.

#### Thermodynamic Growth at the Base: The Stefan Problem

While surface processes can lead to growth (e.g., snow turning to ice) or melt, most of the thermodynamic growth of sea ice occurs at its base, in contact with the ocean. This process is governed by the rate at which heat can be conducted through the existing ice layer. This classic moving-boundary problem is known as the **Stefan problem**. 

Consider a 1D column of ice of thickness $h(t)$. Its base is at the freezing temperature $T_f$, while its surface is maintained at a colder temperature $T_s$ by atmospheric conditions. Heat flows from the warmer base to the colder surface according to the heat equation: $\rho_i c_i \frac{\partial T}{\partial t} = k_i \frac{\partial^2 T}{\partial z^2}$. As this heat is conducted away from the ice-ocean interface, it allows more water to freeze, releasing latent heat $L$. The rate of ice growth, $dh/dt$, is determined by the balance between this latent heat release and the rate of heat conduction:

$$\rho_i L \frac{dh}{dt} = -k_i \left.\frac{\partial T}{\partial z}\right|_{\text{interface}}$$

By non-dimensionalizing this system, we can identify the key dimensionless group that governs the behavior: the **Stefan number (Ste)**.

$$\text{Ste} = \frac{c_i (T_f - T_s)}{L}$$

The Stefan number represents the ratio of the characteristic sensible heat that can be stored in the ice to the latent heat required for [phase change](@entry_id:147324). When $\text{Ste} \ll 1$, as is typical for sea ice, it implies that the latent heat term dominates. Most of the energy transfer is associated with the phase change itself, and the temperature profile within the ice can be well-approximated as linear. This simplifies the Stefan condition, leading to the famous result that ice thickness grows approximately as the square root of time. 

### Synthesis in Earth System Models

The principles of dynamics, rheology, and thermodynamics must be synthesized into a coherent framework for use in large-scale climate and Earth system models. This involves developing parameterizations that capture the essential physics while remaining computationally tractable.

#### Representing Sub-Grid Heterogeneity: The Ice Thickness Distribution

An Earth system model grid cell can be hundreds of kilometers across and contain a complex mosaic of open water, thin new ice, and thick, ridged old ice. To represent this sub-grid scale heterogeneity, models use a statistical approach based on the **[ice thickness distribution](@entry_id:1126327)**, $g(h)$. 

The function $g(h)$ is an [area density](@entry_id:636104) function, defined such that $g(h) \, \mathrm{d}h$ is the fractional area of a grid cell covered by ice with thickness between $h$ and $h+\mathrm{d}h$. From this fundamental function, we can compute key macroscopic properties:
*   **Ice Concentration ($A$):** The total fractional area covered by ice of any thickness. It is the integral of the distribution over all thicknesses: $A = \int_0^\infty g(h) \, \mathrm{d}h$.
*   **Mean Ice Thickness ($H$):** The average thickness of the ice that is present. It is the first moment of the *normalized* distribution, $g(h)/A$: $H = \frac{1}{A} \int_0^\infty h g(h) \, \mathrm{d}h$.
*   **Ice Volume per Unit Area ($\bar{h}$):** The total volume of ice in the grid cell, averaged over the cell area. It is the product of the concentration and the mean thickness: $\bar{h} = A \cdot H = \int_0^\infty h g(h) \, \mathrm{d}h$.

The evolution of $g(h)$ is governed by an [advection-diffusion](@entry_id:151021)-like equation that accounts for transport of ice into and out of the grid cell, as well as changes in thickness due to thermodynamic growth/melt (which shifts ice from one thickness category to another) and mechanical redistribution via ridging (which moves ice from thinner categories to thicker ones). 

#### Internal Structure and Transport: Permeability

The thermal state of sea ice has profound implications for its internal microstructure. As seawater freezes, it forms a matrix of pure ice crystals, trapping concentrated brine in a network of pockets and channels. The volume fraction of this brine, $\phi$, is primarily a function of the ice temperature and salinity.

This brine network makes sea ice a porous medium. The ability of the brine to move through this network is quantified by the **permeability**, $k$. Empirical evidence and theory show that sea ice is effectively impermeable until the brine [volume fraction](@entry_id:756566) exceeds a critical threshold, $\phi_c \approx 0.05$ (the "rule of fives"). 

This behavior is explained by **percolation theory**. For $\phi  \phi_c$, the brine channels exist as isolated pockets. At $\phi = \phi_c$, these pockets connect to form a continuous, sample-spanning network for the first time. This [geometric phase](@entry_id:138449) transition allows for macroscopic fluid flow. The reason $\phi_c$ is so low (compared to thresholds of ~0.3 for simple spherical pores) is the high aspect ratio of the brine channels, which are constrained by ice grain boundaries. Elongated features can form a connected network at much lower volume fractions. Just above the threshold, the permeability is predicted to grow as a power law:

$$k(\phi) \propto (\phi - \phi_c)^t$$

where the exponent $t \approx 2$ in three dimensions. This [percolation threshold](@entry_id:146310) is of paramount importance, as it controls the flushing of salt out of the ice (desalination) and the transport of nutrients to [microbial communities](@entry_id:269604) living within the brine channels, linking the physics of sea ice to its [biogeochemistry](@entry_id:152189). 