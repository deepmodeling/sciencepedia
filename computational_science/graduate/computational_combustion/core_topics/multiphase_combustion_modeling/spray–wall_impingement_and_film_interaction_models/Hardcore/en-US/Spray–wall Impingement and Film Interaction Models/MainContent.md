## Introduction
The interaction of liquid sprays with solid surfaces is a ubiquitous phenomenon in engineering, critically influencing the performance of systems ranging from internal combustion engines and gas turbines to industrial coating and cooling processes. The ability to predict and control whether droplets splash, rebound, or form a [liquid film](@entry_id:260769) is essential for optimizing efficiency, managing heat transfer, and minimizing pollutant formation. However, the complex, multiscale physics involved presents a significant modeling challenge. This article provides a comprehensive overview of the theoretical framework and computational models developed to address this challenge. The journey begins in the **Principles and Mechanisms** chapter, which lays the groundwork by examining the physics of single droplet impact and the dynamics of thin liquid films. We then explore how these foundational models are put into practice in the **Applications and Interdisciplinary Connections** chapter, highlighting their use in engineering systems and their links to thermodynamics, turbulence, and other fields. Finally, the **Hands-On Practices** section offers an opportunity to apply these concepts to practical computational problems. By navigating these chapters, the reader will gain a deep, model-based understanding of [spray-wall impingement](@entry_id:1132214) and film interaction.

## Principles and Mechanisms

The interaction of liquid sprays with solid surfaces is a multiscale phenomenon governed by a complex interplay of fluid dynamics, heat transfer, and surface science. Understanding the fundamental principles and mechanisms that dictate the outcome of these interactions is paramount for the design and optimization of numerous engineering systems, from internal combustion engines to thermal spray coatings and industrial cooling processes. This chapter delineates these core principles, beginning with the physics of a single droplet impact and progressing to the collective dynamics of the resulting [liquid film](@entry_id:260769).

### The Physics of Single Droplet Impingement

The collision of a single liquid droplet with a wall, though seemingly simple, encapsulates a rich array of physical processes. The outcome of this event—whether the droplet splashes, rebounds, or gently deposits—is determined by a competition between various forces acting over very short timescales.

#### Characterizing the Impact: Dimensionless Numbers

To analyze the dynamics of droplet impingement, we can non-dimensionalize the governing Navier-Stokes equations for fluid motion. This process reveals a set of dimensionless numbers, each representing the ratio of two physical forces. These numbers provide a framework for classifying and predicting impact behavior. The primary forces at play are inertial, viscous, surface tension, and gravitational forces.

Let us consider a droplet of diameter $D$, density $\rho$, [dynamic viscosity](@entry_id:268228) $\mu$, and surface tension $\sigma$, impacting a wall with a normal velocity component $U$. The key dimensionless groups are:

*   **Weber Number ($We$)**: This number compares inertial forces, which promote [droplet deformation](@entry_id:1123997) and breakup, to surface tension forces, which resist deformation and seek to maintain a [minimal surface](@entry_id:267317) area. It is defined as:
    $We = \dfrac{\rho U^2 D}{\sigma}$
    A high Weber number ($We \gg 1$) indicates that the droplet's kinetic energy is sufficient to overcome surface tension, leading to significant flattening, spreading, and potentially splashing. Conversely, at low Weber numbers, the droplet tends to remain more spherical and resist breakup.

*   **Reynolds Number ($Re$)**: This number represents the ratio of [inertial forces](@entry_id:169104) to [viscous forces](@entry_id:263294):
    $Re = \dfrac{\rho U D}{\mu}$
    It characterizes the nature of the flow within the deforming droplet. High Reynolds numbers ($Re \gg 1$) correspond to inertia-dominated flows where viscous effects are confined to thin boundary layers. Low Reynolds numbers ($Re \ll 1$) signify slow, creeping flows where [viscous dissipation](@entry_id:143708) dominates and damps out motion.

*   **Ohnesorge Number ($Oh$)**: This number provides a velocity-independent measure of the relative importance of [viscous forces](@entry_id:263294) to surface tension and inertial forces. It is a characteristic of the fluid and the droplet size:
    $Oh = \dfrac{\mu}{\sqrt{\rho \sigma D}} = \dfrac{\sqrt{We}}{Re}$
    The Ohnesorge number is particularly useful because it isolates the fluid's intrinsic properties from the impact dynamics ($U$). A low $Oh$ indicates that the fluid is relatively inviscid and surface tension effects are strong compared to viscous damping, a condition conducive to complex interfacial phenomena like oscillation and splashing. A high $Oh$ signifies a highly viscous fluid where deformations are strongly damped.

*   **Capillary Number ($Ca$)**: This number is the ratio of viscous forces to surface tension forces:
    $Ca = \dfrac{\mu U}{\sigma} = \dfrac{We}{Re}$
    The Capillary number is critical in describing processes where a competition between viscous drag and surface tension drive is central, such as the motion of a contact line or the retraction of a liquid sheet. Low capillary numbers ($Ca \ll 1$) imply that surface tension dominates, favoring retraction and beading, while high capillary numbers ($Ca \gg 1$) suggest that viscous forces can overcome surface tension, allowing for the stable extension of fluid interfaces.

*   **Froude Number ($Fr$)**: This number compares inertial forces to gravitational forces:
    $Fr = \dfrac{U}{\sqrt{g D}}$
    For the microsecond-to-millisecond timescale of a single droplet impact, gravity is typically negligible. However, for the subsequent, slower evolution of the resulting liquid film over larger scales, gravity can become a dominant driving force for film drainage, particularly when $Fr \lt 1$. 

#### Macroscopic Impingement Regimes

The interplay of the forces described by these dimensionless numbers leads to distinct macroscopic outcomes upon impact. The primary regimes are **stick** (or deposition), **rebound**, and **splash**.

*   **Stick (Deposition)**: The droplet spreads on the surface and remains attached, eventually coming to rest as a sessile drop or merging into a [liquid film](@entry_id:260769). This outcome occurs when the initial kinetic energy is entirely dissipated by [viscous forces](@entry_id:263294) and the work of adhesion to the surface. Sticking is favored at low impact energies (low $We$) or for highly viscous fluids (high $Oh$).

*   **Rebound**: The droplet spreads to a maximum diameter, but the surface energy stored in the deformed shape is sufficient to overcome dissipation and adhesion, causing the droplet to retract and lift off from the surface. Rebound is most prominent for non-[wetting](@entry_id:147044) (hydrophobic) surfaces, which have low adhesion, and for low-viscosity fluids (low $Oh$) that minimize energy dissipation.

*   **Splash**: The impact energy is high enough to cause the ejection of secondary, or satellite, droplets. This is an inertial phenomenon, typically occurring above a critical Weber number, $We_{\mathrm{crit}}$. The lamella, a thin sheet of liquid that spreads radially from the impact center, becomes unstable and breaks up at its rim, often forming a crown-like structure.

The transitions between these regimes are not sharp but occur over ranges of parameters. The thresholds for these transitions are functions of multiple variables :

*   **Effect of Viscosity ($Oh$)**: Higher viscosity (larger $Oh$) increases energy dissipation, which suppresses both rebound and splashing. Thus, the Weber number thresholds for both rebound and splash, $We_s$ and $We_{\mathrm{crit}}$, increase with increasing $Oh$.

*   **Effect of Wettability ($\theta_e$)**: The equilibrium [contact angle](@entry_id:145614), $\theta_e$, quantifies the wettability of the surface. A hydrophilic surface (small $\theta_e$) has high adhesion, which promotes sticking and suppresses rebound. A hydrophobic surface (large $\theta_e$) has low adhesion, making rebound easier. Low adhesion also facilitates the lift-off of the spreading lamella edge, thus promoting splashing and lowering $We_{\mathrm{crit}}$.

*   **Effect of Roughness**: Surface roughness has a dual effect. It can increase the wetted area and pin the contact line, which enhances energy dissipation and promotes sticking, thereby suppressing rebound. However, roughness elements also act as perturbation sites that can disrupt the spreading lamella and nucleate instabilities, significantly promoting splashing and lowering $We_{\mathrm{crit}}$.

*   **Effect of Impact Angle ($\theta$)**: For an [oblique impact](@entry_id:165134), the normal component of velocity ($U \cos\theta$) governs the spreading and recoil dynamics, while the tangential component ($U \sin\theta$) promotes shearing and asymmetry. Obliquity tends to suppress rebound (as the normal impact energy is lower) but strongly promotes splashing, as the asymmetric flow is more easily destabilized.

#### Momentum and Energy Exchange During Impact

To model the effect of a spray on the surrounding gas flow and the wall itself, it is essential to quantify the exchange of momentum and energy during each droplet impact.

**Momentum Transfer**: The change in a droplet's momentum during the brief impact duration is due to an impulse from the wall. By the [impulse-momentum theorem](@entry_id:162655), the impulse imparted to the wall, $\vec{J}_{\mathrm{wall}}$, is equal to the change in the droplet's momentum. A common approach to modeling this exchange involves defining coefficients for the normal and tangential directions .

The normal impulse, $J_{n,\mathrm{wall}}$, can be related to the droplet's mass $m$, its initial normal velocity $v_{n,i}$, and a **normal [coefficient of restitution](@entry_id:170710) ($e_n$)**, which is the ratio of rebound to impact normal velocity magnitudes.
$J_{n,\mathrm{wall}} = m(v_{n,i} - v_{n,f}) = m(1+e_n)v_{n,i}$
Here, $v_{n,f} = -e_n v_{n,i}$ is the final normal velocity.

The tangential impulse, $J_{t,\mathrm{wall}}$, arises from friction. In a **sustained-sliding** scenario, where the droplet slips relative to the surface throughout the contact time, the tangential impulse is limited by the normal impulse via a **[coefficient of kinetic friction](@entry_id:162794) ($\mu_k$)**:
$J_{t,\mathrm{wall}} = \mu_k J_{n,\mathrm{wall}} = \mu_k m(1+e_n)v_{n,i}$

For example, consider a hydrocarbon droplet ($m = 5.235 \times 10^{-11}\ \mathrm{kg}$) impacting a wall at $U = 35\ \mathrm{m/s}$ and an angle $\alpha = 20^{\circ}$ to the normal. With a restitution coefficient $e_n = 0.30$ and friction coefficient $\mu_k = 0.10$, and assuming the droplet is sliding over a film moving at $u_f = 2.0\ \mathrm{m/s}$, the initial normal velocity is $v_{n,i} = 35 \cos(20^{\circ}) \approx 32.9\ \mathrm{m/s}$. The impulses delivered to the wall are calculated as $J_{n,\mathrm{wall}} = m(1+e_n)v_{n,i} \approx 2.238 \times 10^{-9}\ \mathrm{N\cdot s}$ and $J_{t,\mathrm{wall}} = \mu_k J_{n,\mathrm{wall}} \approx 2.238 \times 10^{-10}\ \mathrm{N\cdot s}$. The final result is presented as a row matrix: $\begin{pmatrix} 2.238 \times 10^{-9} & 2.238 \times 10^{-10} \end{pmatrix}$. 

**Energy Partitioning**: The initial kinetic energy of the droplet, $E_{\mathrm{kin},0}$, is transformed into other forms upon impact. A complete energy budget accounts for the partitioning of this energy:
$E_{\mathrm{kin},0} = E_s + E_v + E_{\mathrm{def}} + E_{\mathrm{ej}}$
where:
*   $E_s = \sigma \Delta A$ is the increase in **surface energy** due to the creation of new liquid-gas interface area ($\Delta A$).
*   $E_v$ is the energy dissipated into heat by **[viscous forces](@entry_id:263294)** within the deforming liquid.
*   $E_{\mathrm{def}}$ is the **deformation energy**, or the work done on the wall or a pre-existing film.
*   $E_{\mathrm{ej}}$ is the residual **kinetic energy** carried away by any ejected satellite droplets.

Each of these components can be estimated using scaling laws. For a splashing event, the kinetic energy of the ejected droplets ($E_{\mathrm{ej}}$) can be found by subtracting the other energy sinks from the initial kinetic energy. For instance, in a simulated ethanol droplet impact ($D=200\ \mu\mathrm{m}$, $U=15\ \mathrm{m/s}$) on a thin film, the initial kinetic energy of approximately $3.72 \times 10^{-7}\ \mathrm{J}$ might be partitioned into deformation, [viscous dissipation](@entry_id:143708), and surface energy creation, with the remainder—in one specific scenario, as much as $79\%$—being converted into the kinetic energy of the splashed ejecta. This highlights that splashing can be a highly efficient mechanism for redistributing kinetic energy. 

#### The Mechanics of Splashing

Splashing is initiated by the growth of instabilities in the thin, radially expanding liquid sheet, or **lamella**. In the inviscid limit (low $Oh$), the onset of lamella ejection can be analyzed through a balance of forces at the lamella's rim . The outward [momentum flux](@entry_id:199796) of the fluid flowing into the rim, $\rho h U_r^2$, is balanced by the containing [capillary force](@entry_id:181817), which scales with the surface tension $\sigma$.

By combining this [force balance](@entry_id:267186) with scaling laws for mass conservation ($h \sim D^3/R^2$) and inertial spreading kinematics ($R \sim (DUt)^{1/2}$), one can determine the characteristic velocity of the ejected material, $U_e$. A [scaling analysis](@entry_id:153681) reveals that this velocity, normalized by the impact speed $U$, depends on the Weber number:
$\dfrac{U_e}{U} \sim We^{-1/4}$
This scaling relationship demonstrates that as the impact inertia ($We$) increases, the relative ejection velocity decreases. This counter-intuitive result arises because higher impact inertia leads to a faster-spreading and thus thinner lamella. The thinner lamella carries less [momentum flux](@entry_id:199796) for a given radial velocity, making it easier for surface tension to contain the rim, delaying the onset of splashing to a point where the radial velocity has decayed further. This analysis provides a fundamental physical insight into the mechanism governing prompt splashing. 

### The Dynamics of the Wall Film

Repeated droplet impingements lead to the formation of a continuous [liquid film](@entry_id:260769) on the wall. The dynamics of this film—its spreading, thinning, and transport of species—are central to spray-wall interaction models.

#### Governing Equations for Thin Films

When the film thickness $h$ is much smaller than the characteristic length scale $L$ over which it varies (i.e., $h/L \ll 1$), the full Navier-Stokes equations can be simplified using the **[lubrication approximation](@entry_id:203153)**. This [reduced-order model](@entry_id:634428) provides a computationally efficient way to describe film evolution. A key quantity in this framework is the depth-integrated volumetric flux per unit span, $\mathbf{q}$.

Starting from the Stokes momentum balance for an inertia-less flow, and integrating the velocity profile across the film thickness, we can derive an expression for $\mathbf{q}$ that accounts for the primary driving forces :
$\mathbf{q} = -\dfrac{h^3}{3\mu}\nabla p + \dfrac{h^2 \tau_w}{2\mu}\hat{\mathbf{s}} + \dfrac{\rho g h^3}{3\mu}\hat{\mathbf{g}}$

Each term in this equation represents a distinct physical mechanism:
1.  **Capillary-driven flow**: The first term, $-\frac{h^3}{3\mu}\nabla p$, represents a Poiseuille-type flow driven by in-plane pressure gradients. In the absence of external pressure fields, this pressure arises from surface tension acting on a curved interface. For small slopes, the capillary pressure is given by the Young-Laplace equation as $p = -\sigma \nabla^2 h$. This term drives fluid from regions of [positive curvature](@entry_id:269220) (bumps) to [negative curvature](@entry_id:159335) (dents), acting to level the film.
2.  **Shear-driven flow**: The second term, $\frac{h^2 \tau_w}{2\mu}\hat{\mathbf{s}}$, represents a Couette-type flow driven by the tangential shear stress $\tau_w$ exerted by the overlying gas phase in the direction $\hat{\mathbf{s}}$. This is a crucial mechanism for film transport in environments with high-speed crossflows, such as in combustor liners or intake ports.
3.  **Gravity-driven flow**: The third term, $\frac{\rho g h^3}{3\mu}\hat{\mathbf{g}}$, is a Poiseuille-type flow driven by the component of gravitational acceleration $g$ acting along the wall in the direction $\hat{\mathbf{g}}$. This term is responsible for the drainage of films on non-horizontal surfaces.

#### Mass and Species Transport in Multicomponent Films

In many applications, such as fuel injection, the film is a mixture of different chemical species. Modeling the evolution of this film requires tracking the mass concentration of each species $i$, denoted by $c_i$. Using the Reynolds [transport theorem](@entry_id:176504) for a control area on the wall, we can derive a depth-averaged conservation equation for the areal mass density of species $i$, which is $h c_i$. The resulting equation is a convection-diffusion-reaction equation :
$\dfrac{\partial (h c_i)}{\partial t} + \nabla \cdot (c_i \mathbf{q} - h D_i \nabla c_i) = S_{m,i} - j_{e,i}$

This equation states that the rate of change of species mass in a given area (the first term) is balanced by four processes:
*   **Convection**: The term $\nabla \cdot (c_i \mathbf{q})$ represents the advection of species $i$ with the bulk motion of the film, where $\mathbf{q}$ is the total volumetric flux derived previously.
*   **Diffusion**: The term $-\nabla \cdot (h D_i \nabla c_i)$ represents the Fickian diffusion of species $i$ relative to the bulk flow, driven by concentration gradients $\nabla c_i$. Here, $D_i$ is the effective molecular diffusivity of species $i$ within the film.
*   **Source from Impingement ($S_{m,i}$)**: This term accounts for the rate at which mass of species $i$ is added to the film per unit area by impinging spray droplets.
*   **Sink due to Evaporation ($-j_{e,i}$)**: This term represents the rate at which mass of species $i$ is lost from the film per unit area due to evaporation into the gas phase.

Summing this equation over all species $i$ and using the fact that $\sum c_i = \rho$ (if $c_i$ were mass per unit volume) or $\sum c_i = 1$ (if $c_i$ is mass fraction), one can recover the overall mass conservation equation for the film.

#### Thermal Effects and Non-Isothermal Films

Temperature variations along the wall can introduce powerful new mechanisms that drive film flow and alter impact dynamics.

**Thermocapillary (Marangoni) Effects**: The surface tension of most liquids decreases with increasing temperature. If a temperature gradient exists along the surface of a film, it will induce a [surface tension gradient](@entry_id:156138). This gradient exerts a tangential stress on the free surface, pulling fluid from warmer (low surface tension) regions to colder (high surface tension) regions. This phenomenon is known as the **Marangoni effect**.

The Marangoni stress, $\tau_M = \partial\sigma/\partial x$, acts as an additional boundary condition on the free surface. By incorporating this stress into the [lubrication](@entry_id:272901) analysis, we can derive the flux contribution from thermocapillarity. For a flow driven solely by a constant streamwise temperature gradient $G = \partial T/\partial x$, the resulting depth-integrated flux $q$ is given by :
$q = \dfrac{h^2}{2\mu} \dfrac{\partial\sigma}{\partial x} = \dfrac{h^2}{2\mu} \left(\dfrac{d\sigma}{dT}\right) G$

For a typical hydrocarbon fuel film with thickness $h=50\ \mu\mathrm{m}$, viscosity $\mu = 4.0 \times 10^{-4}\ \mathrm{Pa\cdot s}$, and a surface tension sensitivity $d\sigma/dT = -1.5 \times 10^{-4}\ \mathrm{N/(m\cdot K)}$, a strong temperature gradient of $G = 1.0 \times 10^4\ \mathrm{K/m}$ can induce a flux of $q \approx -4.688 \times 10^{-6}\ \mathrm{m^2/s}$. The negative sign indicates that the flow is directed opposite to the temperature gradient (i.e., toward the colder, high-surface-tension region), demonstrating the significance of this mechanism in redistributing liquid on non-isothermal surfaces. 

**Boiling Regimes at Hot Walls**: When a droplet or film interacts with a wall whose temperature $T_w$ is above the liquid's saturation temperature $T_{sat}$, boiling can occur. The nature of this boiling profoundly changes the interaction dynamics. The behavior is classified into three main regimes based on the wall superheat, $\Delta T_w = T_w - T_{sat}$, which can be non-dimensionalized by the **Stefan number**, $Ste = c_{p,\ell} \Delta T_w / h_{fg}$, representing the ratio of sensible heat available in the wall to the [latent heat of vaporization](@entry_id:142174).

The three regimes are :
1.  **Nucleate Boiling**: At low superheats ($Ste \lesssim O(1)$), discrete vapor bubbles form at [nucleation sites](@entry_id:150731) on the wall, but direct liquid-solid contact is maintained. This efficient heat transfer and strong liquid-solid adhesion promotes wetting and deposition, effectively suppressing droplet rebound.
2.  **Transition Boiling**: At intermediate superheats, the interaction is chaotic. Unstable, large vapor patches form and collapse violently. This explosive vapor generation can tear the liquid film apart, leading to intense splashing and **secondary atomization**. The intermittent nature of wall contact allows for partial rebound.
3.  **Film Boiling (Leidenfrost Effect)**: At high superheats ($\Delta T_w$ above the Leidenfrost temperature, $Ste \gg 1$), vapor generation is so rapid that a stable, continuous vapor cushion forms, completely insulating the liquid from the wall. This vapor layer eliminates adhesion and friction, causing impinging droplets to **rebound** with very high efficiency and minimal deposition. The levitation also tends to suppress crown-type splashing by preventing the formation of a thin, surface-bound lamella.

### A Note on Computational Modeling Strategies

The physical principles described in this chapter can be captured computationally through various modeling strategies. The choice of strategy involves a trade-off between fidelity and computational cost. Two broad classes of models are prevalent :

1.  **Fully Resolved Free-Surface Models**: Methods like the **Volume of Fluid (VOF)** or **Level-Set** methods solve the full, un-approximated Navier-Stokes equations throughout the domain. They capture the interface by tracking the volume fraction of the liquid in each computational cell or the signed distance to the interface. These methods are general and powerful, capable of simulating complex phenomena like splashing, [topological changes](@entry_id:136654) (breakup and [coalescence](@entry_id:147963)), and large interface deformations. Their main drawback is high computational expense, as they require a fine 3D mesh to resolve the interface accurately. They are necessary when the fundamental assumptions of simpler models are violated.

2.  **Reduced-Order Thin-Film Models**: As discussed previously, **[lubrication theory](@entry_id:185260)** provides a simplified model valid for slender films where the thickness $h$ is much smaller than the lateral length scale $D$ (i.e., $h/D \ll 1$) and interfacial slopes are small. These models reduce the problem from solving 3D equations to solving a single 2D equation for the film thickness $h(x,y,t)$. This results in a massive reduction in computational cost. They are highly efficient and accurate within their regime of validity, which is typically for non-splashing, gently curved films. This condition is often promoted by dominant surface tension, corresponding to low Capillary numbers ($Ca \ll 1$).

The choice of model is dictated by the physics of the problem. For the detailed study of primary atomization from a splashing droplet, where $h/D$ is not small and the interface undergoes violent deformation, a VOF or [level-set method](@entry_id:165633) is required. For modeling the subsequent evolution of a thin, widespread fuel film on a combustor liner, a [lubrication](@entry_id:272901) model is often the more practical and appropriate choice.