## Introduction
In the field of Computational Fluid Dynamics (CFD), the simulation of multiphase flows presents a significant leap in complexity compared to single-phase systems. The critical challenge lies in accurately accounting for the continuous exchange of mass, momentum, and heat across the dynamic interfaces separating the phases. This article addresses the fundamental knowledge gap of how to model these unresolved interfacial phenomena within the widely used Euler-Euler framework, where phases are treated as interpenetrating continua.

The reader will gain a comprehensive understanding of the theoretical underpinnings and practical application of [interphase transfer closures](@entry_id:750763). The first chapter, **Principles and Mechanisms**, delves into the derivation of these models, explaining how microscopic interfacial fluxes are translated into macroscopic volumetric source terms and detailing the key forces and transport coefficients involved. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these [closures](@entry_id:747387) are employed to solve real-world problems in engineering reactors, turbulent flows, and advanced fields like [granular physics](@entry_id:750007) and magnetohydrodynamics. Finally, **Hands-On Practices** provides a bridge from theory to implementation, offering practical exercises on [numerical schemes](@entry_id:752822) and data-driven [model calibration](@entry_id:146456). This structured journey provides the essential tools for modeling complex multiphase systems with fidelity and physical rigor.

## Principles and Mechanisms

The transition from single-phase to multiphase [computational fluid dynamics](@entry_id:142614) (CFD) introduces a fundamental challenge: the need to account for the exchange of mass, momentum, and energy across the interfaces separating the phases. In the Euler-Euler framework, where the phases are treated as interpenetrating continua, these exchanges are not resolved at the scale of the computational grid. Instead, their effects are modeled as volumetric source terms in the phase-averaged conservation equations. This chapter elucidates the principles and mechanisms that form the basis for these crucial closure models.

### From Interfacial Phenomena to Volumetric Source Terms

In the Euler-Euler [two-fluid model](@entry_id:139846), the conservation equations for each phase $k$ are derived by applying a volume-averaging operator to the local, instantaneous conservation laws. This mathematical procedure gives rise to additional terms that represent the net exchange of quantities across the unresolved interface. These **interphase exchange terms** appear as volumetric sources in the averaged equations.

Let us consider a [control volume](@entry_id:143882) containing two immiscible phases. The phase-averaged continuity, momentum, and enthalpy equations for phase $k$ take the general form:

$ \frac{\partial (\alpha_k \rho_k)}{\partial t} + \nabla \cdot (\alpha_k \rho_k \mathbf{u}_k) = \Gamma_k $

$ \frac{\partial (\alpha_k \rho_k \mathbf{u}_k)}{\partial t} + \nabla \cdot (\alpha_k \rho_k \mathbf{u}_k \mathbf{u}_k) = -\alpha_k \nabla p_k + \nabla \cdot (\alpha_k \boldsymbol{\sigma}_k) + \alpha_k \rho_k \mathbf{g} + \mathbf{M}_k $

$ \frac{\partial (\alpha_k \rho_k h_k)}{\partial t} + \nabla \cdot (\alpha_k \rho_k \mathbf{u}_k h_k) = \dots + S_k^h $

Here, $\alpha_k$, $\rho_k$, $\mathbf{u}_k$, and $h_k$ are the volume fraction, density, velocity, and [specific enthalpy](@entry_id:140496) of phase $k$, respectively. The terms on the right-hand side, $\Gamma_k$, $\mathbf{M}_k$, and $S_k^h$, are the volumetric source terms for mass, momentum, and enthalpy. These terms are formally defined by averaging the fluxes at the interface. For a property flux $\psi''$ into phase $k$ across the interface, the corresponding volumetric source is the product of the average flux and the **interfacial [area density](@entry_id:636104)**, $a_i$, which is the total interfacial area per unit mixture volume ($m^2/m^3$).

The source terms are precisely defined as follows [@problem_id:3336694]:
-   The **volumetric mass source**, $\Gamma_k$, is the net rate of mass entering phase $k$ per unit volume. It is given by $\Gamma_k = a_i \langle \dot{m}_{q \rightarrow k}'' \rangle_i$, where $\dot{m}_{q \rightarrow k}''$ is the local mass flux per unit area from the other phase $q$ into phase $k$. Conservation of mass requires $\Gamma_1 + \Gamma_2 = 0$.

-   The **volumetric momentum source**, $\mathbf{M}_k$, represents the total force exerted by the other phase on phase $k$ per unit volume, including momentum transferred by [phase change](@entry_id:147324). It is given by $\mathbf{M}_k = a_i \langle \mathbf{f}_{q \rightarrow k}'' \rangle_i + \Gamma_k \mathbf{u}_i$, where $\mathbf{f}_{q \rightarrow k}''$ is the local interfacial traction (force per unit area) and $\mathbf{u}_i$ is the velocity of the matter crossing the interface. Newton's third law requires $\mathbf{M}_1 + \mathbf{M}_2 = \mathbf{0}$.

-   The **volumetric enthalpy source**, $S_k^h$, represents the net rate of enthalpy transfer into phase $k$ per unit volume. It is given by $S_k^h = a_i \langle q_{q \rightarrow k}'' \rangle_i + \Gamma_k h_i$, where $q_{q \rightarrow k}''$ is the local heat flux and $h_i$ is the [specific enthalpy](@entry_id:140496) at the interface. Conservation of energy for a closed mixture requires $S_1^h + S_2^h = 0$.

This formulation is fundamentally different from that used in **[sharp-interface methods](@entry_id:754746)** (e.g., Volume-of-Fluid or Level-Set), where the interface is explicitly tracked. In such methods, the bulk phase equations contain no volumetric interphase sources. Instead, the exchange is imposed through jump conditions (e.g., stress balance with surface tension, heat [flux balance](@entry_id:274729) with [latent heat](@entry_id:146032)) applied directly as boundary conditions on the resolved interface [@problem_id:3336694].

The central task of closure modeling, therefore, is to develop physically sound expressions for the local fluxes ($\dot{m}''$, $\mathbf{f}''$, $q''$) and the interfacial [area density](@entry_id:636104) ($a_i$). For simple [transport processes](@entry_id:177992) like heat and species transfer driven by a potential difference, the relationship is direct. If the local interfacial heat flux follows Newton's law of cooling, $q'' = h(T_s - T_\infty)$, and the species flux follows a two-film model, $j'' = k_L(C_s - C_\infty)$, the corresponding volumetric source terms for the continuous phase become [@problem_id:3336749]:

$ Q = a_i q'' = a_i h (T_s - T_\infty) $

$ J = a_i j'' = a_i k_L (C_s - C_\infty) $

Here, $h$ and $k_L$ are the [heat and mass transfer](@entry_id:154922) coefficients, respectively. These equations highlight the dual nature of closure modeling: one part concerns the geometry of the interface ($a_i$), and the other concerns the intensity of the transport process at the interface ($h, k_L$, etc.).

### Interphase Momentum Transfer

The [interphase](@entry_id:157879) momentum [source term](@entry_id:269111), $\mathbf{M}_k$, is often decomposed into several distinct physical forces. For a [dispersed phase](@entry_id:748551) (e.g., particles, drops, bubbles) in a continuous fluid, the total force is the sum of quasi-steady and unsteady contributions.

#### Quasi-Steady Forces

These forces depend only on the instantaneous state of the flow field.

##### Drag Force

The **drag force** is the component of the [hydrodynamic force](@entry_id:750449) that acts parallel to the direction of [relative motion](@entry_id:169798) between the phases. It is the dominant mechanism of momentum exchange in most multiphase flows. The drag force on a single dispersed element (particle, bubble, or drop) is expressed using a dimensionless **[drag coefficient](@entry_id:276893)**, $C_D$:

$ \mathbf{F}_D = \frac{1}{2} \rho_f C_D A |\mathbf{u}_r| \mathbf{u}_r $

where $\rho_f$ is the continuous fluid density, $A$ is the projected area of the element, and $\mathbf{u}_r = \mathbf{u}_f - \mathbf{u}_p$ is the relative or slip velocity. The [drag coefficient](@entry_id:276893) $C_D$ is primarily a function of the particle **Reynolds number**, $Re_p$, which represents the ratio of inertial to [viscous forces](@entry_id:263294) acting on the fluid flowing around the element:

$ Re_p = \frac{\rho_f |\mathbf{u}_r| d_p}{\mu_f} $

Here, $d_p$ is the particle diameter and $\mu_f$ is the fluid [dynamic viscosity](@entry_id:268228).

For dilute suspensions of isolated, rigid spherical particles, a widely used closure is the **Schiller-Naumann correlation** [@problem_id:3336753], valid for $Re_p \lesssim 1000$:

$ C_D = \frac{24}{Re_p}(1 + 0.15 Re_p^{0.687}) $

In dense systems, however, the drag on a particle is significantly altered by its neighbors. Two main approaches exist for modeling this effect. **Homogeneous drag models** (e.g., Wen-Yu, Ergun) assume a uniform particle distribution and account for increased "hindrance" by multiplying the drag by a factor that increases with solids [volume fraction](@entry_id:756566), $\epsilon_s$. For example, a correction factor of $\epsilon_f^{-m}$ (where $\epsilon_f = 1-\epsilon_s$ is the fluid volume fraction and $m > 1$) increases the effective drag.

In reality, many dense flows like gas-solid fluidized beds are not homogeneous. They form meso-scale structures such as clusters and particle-lean voids. **Cluster-corrected drag models** account for this heterogeneity. The gas preferentially flows through the low-resistance voids (channeling), and particles within dense clusters are shielded from the flow by their neighbors (wake shielding). The net effect is often a significant *reduction* in the volume-averaged drag force compared to the prediction of a homogeneous model at the same average volume fraction. For instance, in a dense gas-solid flow with $\epsilon_s = 0.3$, a particle Reynolds number of $Re_p \approx 33$ would yield an isolated-particle [drag coefficient](@entry_id:276893) of $C_D \approx 1.9$ from the Schiller-Naumann formula. A homogeneous model would predict a substantially higher effective drag, whereas a cluster-corrected model would predict a reduced drag that could be closer to the isolated-particle value due to the strong effects of heterogeneity [@problem_id:3336753].

##### Lateral Lift Forces

Dispersed elements can also experience forces perpendicular to their direction of [relative motion](@entry_id:169798), known as **lift forces**. These are particularly important for predicting phase distribution in sheared flows, such as [pipe flow](@entry_id:189531).

-   **Saffman Lift**: This shear-induced lift acts on a non-rotating particle moving through a flow with a velocity gradient (shear). The velocity difference across the particle creates a pressure imbalance, resulting in a force. For a small sphere in a linear [shear flow](@entry_id:266817) at low $Re_p$, the [lift coefficient](@entry_id:272114) scales as $C_{L,S} \propto \sqrt{\nu \gamma} / U_{\mathrm{rel}}$, where $\gamma$ is the shear rate. This force is significant whenever slip and shear coexist [@problem_id:3336764].

-   **Magnus Lift**: This rotation-induced lift acts on a spinning particle. The rotation generates circulation in the surrounding fluid, and by the Kutta-Joukowski principle, this circulation produces a lift force. The [lift coefficient](@entry_id:272114) is typically modeled as being linearly proportional to the spin ratio, $C_{L,M} \propto \omega a / U_{\mathrm{rel}}$, where $\omega$ is the particle's [angular speed](@entry_id:173628) and $a$ is its radius.

-   **Tomiyama Lift (for bubbles)**: The lift on deformable bubbles is more complex. Small, nearly spherical bubbles behave like solid particles and experience a positive [lift coefficient](@entry_id:272114) ($C_L > 0$), pushing them away from regions of high velocity. However, as bubbles grow larger, buoyancy and inertial forces deform them into ellipsoidal or cap shapes. This deformation dramatically alters the pressure distribution, and can cause the lift force to reverse direction ($C_L  0$), pushing the bubbles toward the high-velocity core of the flow. The **Tomiyama lift model** is an empirical correlation that captures this sign change. The [lift coefficient](@entry_id:272114) is expressed as a function of dimensionless numbers that characterize deformation, primarily the **Eötvös number**, $Eo$, which compares buoyancy to surface tension. The transition from positive to negative lift typically occurs at a critical $Eo$ between 4 and 10 [@problem_id:3336764].

#### Unsteady Forces

When a particle accelerates relative to the fluid, the quasi-steady force models are insufficient. The total [hydrodynamic force](@entry_id:750449) also includes contributions that depend on the history of the relative acceleration. These are critical for accurately modeling transient phenomena.

-   **Added Mass Force**: This is an inviscid, potential-flow effect that represents the inertia of the surrounding fluid that must be accelerated along with the particle. The force is proportional to the relative acceleration between the fluid and the particle. For a sphere, the force on the particle is given by:
    $ \mathbf{F}_{\mathrm{AM}} = C_A \rho_f V_p \left( \frac{D \mathbf{u}_f}{D t} - \frac{d \mathbf{u}_p}{d t} \right) $
    Here, $V_p$ is the particle volume and $C_A$ is the **added mass coefficient**, which is a purely geometric factor. For a sphere in an unbounded fluid, $C_A = 1/2$. This force vanishes when the relative velocity is constant [@problem_id:3336740].

-   **Basset History Force**: This is a viscous unsteady effect arising from the slow diffusion of [vorticity](@entry_id:142747) generated at the particle's surface into the surrounding fluid. Because [vorticity](@entry_id:142747) from past motion lingers and affects the present flow, this force creates a "memory" of the particle's acceleration history. It is expressed as a temporal convolution integral:
    $ \mathbf{F}_{\mathrm{B}} \propto \int_{-\infty}^{t} \frac{d\mathbf{u}_r/d\tau}{\sqrt{t-\tau}} d\tau $
    The kernel, with its $(t-\tau)^{-1/2}$ dependence, gives the force a long memory. Following a sudden change in slip velocity, the Basset force contribution decays algebraically as $t^{-1/2}$, much more slowly than an exponential decay. Like the [added mass](@entry_id:267870) force, it vanishes for a constant slip velocity [@problem_id:3336740].

### Interphase Heat Transfer

The closure for interphase heat transfer typically takes the form of Newton's law of cooling, where the interfacial heat flux per unit area, $q''$, is proportional to the temperature difference between the particle surface ($T_s$) and the bulk fluid ($T_\infty$).

$ q'' = h (T_s - T_\infty) $

The key closure parameter is the **heat transfer coefficient**, $h$. It is crucial to recognize that $h$ is not a material property of the fluid or solid. Instead, it is an effective parameter that encapsulates the complex microscale physics of conduction and convection in the [thermal boundary layer](@entry_id:147903) around the particle. Its value depends on the flow conditions, [fluid properties](@entry_id:200256), and geometry [@problem_id:3336770].

To generalize correlations for $h$, it is made dimensionless in the form of the **Nusselt number**, $Nu$:

$ Nu = \frac{h d_p}{k_f} $

The Nusselt number represents the ratio of the total [convective heat transfer](@entry_id:151349) to the purely conductive heat transfer that would occur across a fluid layer of thickness $d_p$. Here, $k_f$ is the thermal conductivity of the *fluid*, as it is the medium through which heat must pass. For a stationary sphere in a stagnant fluid, theory shows $Nu=2$. For flows with non-zero relative velocity, $Nu > 2$, indicating the enhancement of heat transfer by convection. In CFD, [closures](@entry_id:747387) for $Nu$ are typically empirical correlations expressed as a function of the Reynolds number ($Re$) and the **Prandtl number**, $Pr = \nu_f / \alpha_f$, which is the ratio of [momentum diffusivity](@entry_id:275614) to [thermal diffusivity](@entry_id:144337).

### Interphase Mass Transfer

Mass transfer closures are developed in close analogy to heat transfer, but often involve additional complexities from [phase equilibrium](@entry_id:136822), chemical reactions, and multicomponent interactions.

#### Convective Mass Transfer

The basic closure for the interfacial mass flux of a solute, $j''$, is:

$ j'' = k_L (C_s - C_\infty) $

Here, $k_L$ is the **[mass transfer coefficient](@entry_id:151899)** and $(C_s - C_\infty)$ is the concentration difference driving force. The dimensionless form is the **Sherwood number**, $Sh$:

$ Sh = \frac{k_L d_p}{D} $

where $D$ is the [mass diffusivity](@entry_id:149206) of the solute in the fluid. The Sherwood number represents the ratio of convective to diffusive [mass transport](@entry_id:151908). Closures for $Sh$ are typically functions of the Reynolds number and the **Schmidt number**, $Sc = \nu_f/D$, which is the ratio of [momentum diffusivity](@entry_id:275614) to [mass diffusivity](@entry_id:149206) [@problem_id:3336708].

#### Advanced Mass Transfer Mechanisms

-   **Interfacial Equilibrium and Two-Resistance Theory**: In many systems, the interfacial concentration $C_s$ is unknown. It must be determined by assuming [local thermodynamic equilibrium](@entry_id:139579) at the interface. This equilibrium is described by relations like **Henry's Law** for a gas dissolving in a liquid ($C_{s,liq} = H p_{s,gas}$) or a **distribution coefficient** for a solute between two liquids ($C_{s,1} = K_{12} C_{s,2}$). The total resistance to [mass transfer](@entry_id:151080) is the sum of resistances in each phase's boundary layer (film). The relative importance of each resistance depends on the [mass transfer](@entry_id:151080) coefficients in each phase and the slope of the equilibrium curve. For a highly soluble gas, for instance, the gas-side resistance can be dominant, contradicting the common assumption that it is always negligible [@problem_id:3336708].

-   **Mass Transfer with Chemical Reaction**: If the transferred species undergoes a chemical reaction within the [concentration boundary layer](@entry_id:151238), the rate of [mass transfer](@entry_id:151080) can be significantly increased. The reaction consumes the solute, steepening the concentration gradient at the interface and enhancing the flux. This is quantified by an **enhancement factor**, $E$, such that the effective [mass transfer coefficient](@entry_id:151899) is $k_{L,eff} = E \cdot k_L$. The magnitude of this enhancement depends on the relative rates of diffusion and reaction, a relationship captured by the dimensionless **Hatta number**, $Ha$ [@problem_id:3336708].

-   **Multicomponent Diffusion and Maxwell-Stefan Equations**: Simple Fick's law, which relates the flux of a species only to its own [concentration gradient](@entry_id:136633), is often inadequate for multicomponent mixtures, especially in non-ideal systems or when fluxes are large. The rigorous framework for describing multicomponent diffusion is the **Maxwell-Stefan equations**. These equations arise from balancing the thermodynamic driving force on each species (the gradient of its chemical potential, $\nabla\mu_i$) with the frictional drag forces exerted by all other species. This results in a coupled system of equations of the form [@problem_id:3336725]:
    $ -\frac{x_i}{RT} \nabla \mu_i = \sum_{j \ne i} \frac{x_j \mathbf{N}_i - x_i \mathbf{N}_j}{c D_{ij}} $
    This formulation naturally accounts for thermodynamic non-ideality (through the chemical potential) and **cross-diffusion** (the flux of one species induced by the gradient of another). It is the physically correct framework for the complex reactive absorption scenario involving species A, B, and C described in [@problem_id:3336725]. Fick's law is recovered only in simplified cases, such as for a binary [ideal mixture](@entry_id:180997) under [equimolar counter-diffusion](@entry_id:153009).

#### Mass Transfer via Phase Change

A distinct and fundamentally important mode of [mass transfer](@entry_id:151080) is evaporation and condensation. A widely used closure for this process, based on the [kinetic theory of gases](@entry_id:140543), is the **Hertz-Knudsen-Schrage relation**. It expresses the net mass flux, $\dot{m}''$, as a function of the difference between the actual [vapor pressure](@entry_id:136384) at the interface, $p_v$, and the saturation pressure corresponding to the interface temperature, $p_{sat}(T_i)$. For [condensation](@entry_id:148670) (vapor to liquid), the flux is:

$ \dot{m}'' = \alpha_m \frac{p_v - p_{\mathrm{sat}}(T_i)}{\sqrt{2\pi R_v T_i}} $

Here, $\alpha_m$ is the mass [accommodation coefficient](@entry_id:151152) (a value between 0 and 1 representing the fraction of impinging molecules that stick) and $R_v$ is the [specific gas constant](@entry_id:144789) for the vapor. This [mass transfer](@entry_id:151080) is directly coupled to a significant [energy transfer](@entry_id:174809) due to the **[latent heat of vaporization](@entry_id:142174)**, $L_v$. The corresponding volumetric heat source released into the liquid during condensation is [@problem_id:3336710]:

$ S_h^{(\ell)} = + a_i \dot{m}'' L_v(T_i) $

During evaporation ($\dot{m}''  0$), this term becomes negative, representing an energy sink.

### Synthesis: A Regime Map with Dimensionless Groups

The selection of appropriate [interphase transfer closures](@entry_id:750763) for a given application is not arbitrary. It must be guided by a physical understanding of the dominant forces and phenomena, which can be quantified using [dimensionless groups](@entry_id:156314). For a dispersed flow like an air bubble rising in water, a set of key numbers helps to map the regime and select models [@problem_id:3336709].

-   **Reynolds Number ($Re = \rho_l U d / \mu_l$)**: Compares inertia to [viscous forces](@entry_id:263294). A large $Re$ (e.g.,  100) indicates an inertial flow with a significant wake, where [form drag](@entry_id:152368) dominates.

-   **Eötvös Number ($Eo = g(\rho_l - \rho_g) d^2 / \sigma$)**: Compares [buoyancy](@entry_id:138985) forces to surface tension forces. It is the primary indicator of bubble deformation due to gravity. $Eo \ll 1$ implies nearly spherical bubbles, while $Eo > 1$ implies significant flattening.

-   **Weber Number ($We = \rho_l U^2 d / \sigma$)**: Compares inertial forces to surface tension forces. It measures the tendency of the flow's inertia to deform the bubble.

-   **Morton Number ($Mo = g \mu_l^4 / (\rho_l \sigma^3)$)**: This unique group depends only on fluid properties and gravity. It characterizes the fluid system itself. In combination with $Eo$ or $Re$, it provides a complete map of bubble shape and dynamics (e.g., the Grace diagram).

-   **Capillary Number ($Ca = \mu_l U / \sigma$)**: Compares viscous forces to surface tension forces. A very low $Ca$ suggests that the interface is highly mobile ("clean"), allowing for internal circulation, which can affect drag and mass transfer.

For an illustrative scenario of a 3 mm air bubble rising in water at 0.25 m/s, the dimensionless numbers are approximately $Re \approx 750$, $Eo \approx 1.2$, $We \approx 2.6$, and $Mo \approx 2.6 \times 10^{-11}$. This analysis tells a clear story: the bubble is in an inertial flow regime ($Re \gg 1$) where both [buoyancy](@entry_id:138985) and inertia are strong enough to deform it into a slightly ellipsoidal shape ($Eo, We \sim \mathcal{O}(1)$). The extremely low Morton number is characteristic of a low-viscosity fluid like water. This diagnosis dictates that one cannot use simple drag laws for rigid spheres. Instead, a drag closure dependent on $Re$ and $Eo$ is required. Similarly, heat and [mass transfer correlations](@entry_id:148027) must be chosen that account for the enhanced transfer due to shape deformation and a mobile interface [@problem_id:3336709]. This systematic approach, grounded in the principles of dimensional analysis, is fundamental to the robust application of multiphase CFD.