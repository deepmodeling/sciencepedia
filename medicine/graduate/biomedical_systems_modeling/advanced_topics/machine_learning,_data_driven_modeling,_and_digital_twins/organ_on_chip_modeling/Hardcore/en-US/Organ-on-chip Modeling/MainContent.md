## Introduction
Organ-on-chip (OoC) technology represents a paradigm shift in biological research, offering unprecedented potential to mimic human physiology in a controlled microscale environment. By integrating [microfluidics](@entry_id:269152) with living cells, these systems move beyond the limitations of traditional static cultures. However, to fully harness their power for applications in [drug development](@entry_id:169064), [disease modeling](@entry_id:262956), and [personalized medicine](@entry_id:152668), we must move beyond qualitative observation to a rigorous, quantitative understanding. This requires a robust modeling framework to design, operate, and interpret data from these complex [microphysiological systems](@entry_id:913338).

This article provides a comprehensive guide to the [mathematical modeling](@entry_id:262517) of [organ-on-chip](@entry_id:899828) devices. It is structured to build knowledge from foundational principles to practical application. The first chapter, **"Principles and Mechanisms,"** will delve into the core physics of [transport phenomena](@entry_id:147655), deriving the governing equations and key dimensionless numbers that define the OoC microenvironment. The second chapter, **"Applications and Interdisciplinary Connections,"** will demonstrate how these principles are applied to solve real-world problems in pharmacology, [mechanobiology](@entry_id:146250), and [systems biology](@entry_id:148549), showcasing the technology's role in bridging the *in vitro*-*in vivo* gap. Finally, the **"Hands-On Practices"** section will offer practical exercises to solidify understanding of key modeling concepts, such as parameter identifiability and sensitivity analysis. By navigating these chapters, the reader will gain the quantitative skills necessary to model, analyze, and innovate in the burgeoning field of [organ-on-chip](@entry_id:899828) technology.

## Principles and Mechanisms

The successful design, fabrication, and operation of [organ-on-chip](@entry_id:899828) (OoC) systems hinge upon a rigorous understanding of the underlying physical and biochemical principles that govern their function. Unlike traditional static cell cultures, OoCs are dynamic [microphysiological systems](@entry_id:913338) where the interplay of fluid flow, mass transport, chemical reactions, and mechanical forces dictates the cellular microenvironment. This chapter elucidates the core principles and mechanisms that form the quantitative basis for modeling these complex systems. We will derive the governing equations from first principles, introduce key [dimensionless parameters](@entry_id:180651) that characterize system behavior, and explore the fundamental trade-offs inherent in replicating *in vivo* physiology *in vitro*.

### Defining an Organ-on-Chip Through Transport Regimes

A defining characteristic of an [organ-on-chip](@entry_id:899828), which distinguishes it from other three-dimensional culture systems like [organoids](@entry_id:153002), is its precisely engineered control over the transport microenvironment. This control is achieved through [microfabrication](@entry_id:192662) and microfluidics. To quantify this, we can analyze the dominant modes of momentum and [mass transport](@entry_id:151908) using dimensionless numbers.

Consider a typical OoC [microchannel](@entry_id:274861) with a height $h$ on the order of $100\,\mu\mathrm{m}$, perfused with a culture medium whose properties are similar to water (density $\rho \approx 10^3\,\mathrm{kg/m^3}$, [dynamic viscosity](@entry_id:268228) $\mu \approx 10^{-3}\,\mathrm{Pa\cdot s}$). For a physiologically relevant flow rate, such as $5\,\mu\mathrm{L}/\mathrm{min}$ in a channel of $500\,\mu\mathrm{m}$ width, the average fluid velocity $v$ is on the order of $1-2\,\mathrm{mm/s}$. The flow regime is characterized by the **Reynolds number ($Re$)**, which represents the ratio of inertial forces to viscous forces. Using the channel height $H$ as the characteristic length scale, $Re$ is defined as $Re = \frac{\rho v H}{\mu}$. For the conditions described, the Reynolds number is approximately $0.17$ . As $Re \ll 1$, the flow is deep within the **laminar regime**, where viscous forces dominate and the fluid moves in smooth, parallel layers without turbulence. This is a universal feature of OoC [microfluidics](@entry_id:269152).

Similarly, [mass transport](@entry_id:151908) is characterized by the **Péclet number ($Pe$)**, which represents the ratio of advective (convective) transport to diffusive transport, defined as $Pe = \frac{v H}{D}$, where $D$ is the molecular diffusivity of a solute. For a small molecule like a drug or nutrient with $D \approx 2 \times 10^{-9}\,\mathrm{m^2/s}$, the Péclet number under the same flow conditions is approximately $83$ . Since $Pe \gg 1$, mass transport is dominated by **advection**, meaning solutes are primarily carried by the bulk fluid motion rather than slowly diffusing.

This analysis provides a quantitative definition: an [organ-on-chip](@entry_id:899828) is a microfluidic system operating in a laminar ($Re \ll 1$), advection-dominated ($Pe \gg 1$) transport regime. This contrasts sharply with a static organoid, where in the absence of forced perfusion ($v=0$), both $Re$ and $Pe$ are zero, and all transport of nutrients and waste products occurs purely by diffusion. This [diffusion limitation](@entry_id:266087) often leads to the formation of necrotic cores in larger [organoids](@entry_id:153002), a problem that OoC perfusion is designed to solve.

### Governing Principles of Transport Phenomena

To build predictive models of OoCs, we must formalize the physics of momentum and [mass transport](@entry_id:151908) through their governing partial differential equations.

#### Momentum Transport and Fluid Dynamics

The motion of the culture medium, treated as an incompressible Newtonian fluid, is governed by the **Navier-Stokes equation**, which is a statement of the conservation of momentum:
$$
\rho \left( \frac{\partial \mathbf{v}}{\partial t} + (\mathbf{v} \cdot \nabla)\mathbf{v} \right) = - \nabla p + \mu \nabla^2 \mathbf{v}
$$
Here, $\mathbf{v}$ is the velocity vector, $p$ is pressure, $\rho$ is density, and $\mu$ is [dynamic viscosity](@entry_id:268228). The term on the left represents fluid inertia (transient and convective acceleration), while the terms on the right represent the pressure [gradient force](@entry_id:166847) and the viscous force, respectively.

By nondimensionalizing this equation using characteristic scales for velocity ($U$), length ($H$), and pressure ($P_c = \mu U / H$), we can rigorously derive the Reynolds number . The dimensionless form of the steady-state momentum equation becomes:
$$
Re ((\mathbf{v}^* \cdot \nabla^*) \mathbf{v}^*) = - \nabla^* p^* + \nabla^{*2} \mathbf{v}^*
$$
where the asterisk denotes dimensionless variables. In this form, the importance of inertia is explicitly scaled by $Re$. In the microfluidic context where $Re \ll 1$, the inertial term on the left becomes negligible. The equation simplifies to the **Stokes equation**, or **creeping flow** equation:
$$
0 \approx - \nabla p + \mu \nabla^2 \mathbf{v}
$$
This balance between pressure and viscous forces dictates the flow field in almost all OoC devices. The absence of the nonlinear inertial term makes the equation linear and time-reversible, a peculiar feature of the low-$Re$ world. This dominance of viscosity is what ensures flows are smooth and laminar, as any small perturbation is quickly damped by [viscous dissipation](@entry_id:143708) rather than being amplified by inertia into turbulence. For a typical microvessel-on-chip, a Reynolds number of $0.1$ is common, justifying the use of the Stokes flow approximation .

A direct consequence of this physics is the ability to generate well-defined mechanical cues. A critical cue for many cell types, especially [endothelial cells](@entry_id:262884) lining blood vessels, is the **wall shear stress ($\tau_w$)**, the [frictional force](@entry_id:202421) exerted by the moving fluid on the channel walls. For a common OoC geometry—a high-aspect-ratio rectangular channel ($w \gg h$)—the flow can be approximated as flow between two infinite [parallel plates](@entry_id:269827). Solving the Stokes equation for this geometry yields a [parabolic velocity profile](@entry_id:270592). From this profile, the wall shear stress can be derived as :
$$
\tau_w = \frac{6 \mu Q}{w h^2}
$$
where $Q$ is the [volumetric flow rate](@entry_id:265771), $w$ is the channel width, and $h$ is the channel height. This simple algebraic relationship allows for the precise control of a key mechanobiological signal. For instance, in an endothelialized channel with dimensions $w=1\,\mathrm{mm}$ and $h=100\,\mu\mathrm{m}$, a flow rate of $100\,\mu\mathrm{L}/\mathrm{min}$ generates a physiologically relevant shear stress of $1.0\,\mathrm{Pa}$ .

#### Mass Transport: Advection, Diffusion, and Reaction

The concentration of a solute $c(\mathbf{x}, t)$—be it a nutrient, a drug, or a secreted signaling molecule—is governed by the principle of species conservation. A [mass balance](@entry_id:181721) over an infinitesimal control volume, accounting for transport by advection (with the fluid velocity $\mathbf{v}$) and diffusion (described by **Fick's law**, $\mathbf{J}_{\text{diff}} = -D \nabla c$), and loss or production by chemical reaction ($R(c)$), leads to the general **advection-diffusion-reaction equation** :
$$
\frac{\partial c}{\partial t} + \mathbf{v} \cdot \nabla c = D \nabla^2 c - R(c)
$$
Here, $\frac{\partial c}{\partial t}$ is the local rate of accumulation, $\mathbf{v} \cdot \nabla c$ is the advective transport term, $D \nabla^2 c$ is the diffusive transport term, and $R(c)$ is the net volumetric rate of consumption (if $R>0$) or production (if $R0$).

Nondimensionalizing this equation using [characteristic scales](@entry_id:144643) for length ($L$), velocity ($U$), and concentration ($c_0$) formally yields the Péclet number, $Pe = \frac{UL}{D}$, as the coefficient that balances advection and diffusion. When $Pe \gg 1$, as is typical in perfused OoC channels, the advection term $\mathbf{v} \cdot \nabla c$ dominates the diffusion term $D \nabla^2 c$. This means solutes are transported primarily along the direction of flow, and diffusion is mainly relevant for transporting solutes from the bulk stream to the cell surface. A typical Péclet number in an OoC can be on the order of $160$, confirming that the system is strongly advection-dominated .

### Modeling Key Biological and Biophysical Mechanisms

The general transport equations provide a framework. To model a specific organ's function, we must define the terms—especially the reaction term $R(c)$ and the boundary conditions—that represent its unique biology.

#### Reaction Kinetics and Metabolism

The reaction term $R(c)$ encapsulates all biochemical transformations, such as [cellular metabolism](@entry_id:144671) or [drug clearance](@entry_id:151181). A common and fundamental model for enzyme-catalyzed reactions is the **Michaelis-Menten kinetics**. This model arises from a simple reaction scheme where a substrate ($S$) binds reversibly to an enzyme ($E$) to form a complex ($ES$), which then irreversibly breaks down to release the product ($P$) and regenerate the free enzyme.

Starting from the law of mass action for each step and applying the **Quasi-Steady-State Approximation (QSSA)**—which assumes the concentration of the intermediate complex $[ES]$ remains relatively constant—we can derive the reaction rate $v$ as a function of substrate concentration $c$ :
$$
v(c) = \frac{V_{\max} c}{K_m + c}
$$
Here, $V_{\max}$ is the maximum reaction rate at saturating substrate concentrations, and $K_m$ is the Michaelis constant, representing the substrate concentration at which the reaction rate is half-maximal.

To understand the interplay between reaction and transport, we introduce the **Damköhler number ($Da$)**. It compares the characteristic timescale of transport (e.g., advective residence time, $\tau_{adv} = L/U$) to the characteristic timescale of reaction ($\tau_{rxn}$). For a [first-order reaction](@entry_id:136907) (the low-concentration limit of Michaelis-Menten kinetics), $\tau_{rxn} = K_m/V_{\max}$. The Damköhler number is then :
$$
Da = \frac{\tau_{\text{adv}}}{\tau_{\text{rxn}}} = \frac{V_{\max} L}{K_m U}
$$
If $Da \gg 1$, the reaction is fast compared to the fluid residence time, and the system is **transport-limited**; a significant fraction of the substrate may be consumed as it flows through the device. If $Da \ll 1$, the reaction is slow, and the system is **reaction-limited**; the substrate concentration will not change significantly. A calculated $Da$ of approximately $4.3$ for a representative system indicates a regime where reaction and transport rates are comparable, meaning both phenomena are crucial to the system's overall behavior .

#### Barrier Function and Membrane Transport

Many OoCs model barrier tissues like the gut, lung, or blood-brain barrier. Transport across these barriers is a critical function.

For a simple, non-porous membrane (or cell layer), transport of a solute is governed by its ability to partition into the membrane and then diffuse across it. Assuming [steady-state diffusion](@entry_id:154663) across a membrane of thickness $\delta$, we can use Fick's law to derive an **[effective permeability](@entry_id:1124191) ($P$)** . The flux density $j$ (moles per area per time) is related to the concentration difference across the aqueous phases, $\Delta c$, by $j = P \Delta c$. The permeability is a composite parameter of the material properties:
$$
P = \frac{K D_m}{\delta}
$$
where $K$ is the dimensionless **[partition coefficient](@entry_id:177413)** ([solute concentration](@entry_id:158633) in membrane / concentration in water at equilibrium) and $D_m$ is the solute's diffusion coefficient within the membrane. For a barrier-on-a-chip, this permeability can be experimentally determined by measuring the [steady-state flux](@entry_id:183999) across a known area for a given concentration difference. For example, a solute with a measured permeability of $1.20 \times 10^{-6}\,\mathrm{m\,s^{-1}}$ might correspond to a material with a [partition coefficient](@entry_id:177413) of $0.75$, a membrane diffusivity of $8.0 \times 10^{-11}\,\mathrm{m^2\,s^{-1}}$, and a thickness of $50\,\mu\mathrm{m}$ .

For more complex [biological barriers](@entry_id:921962) that allow the passage of both water and solutes, transport becomes a coupled process. The **Kedem-Katchalsky equations**, derived from non-equilibrium thermodynamics, describe this coupling. The volumetric solvent flux ($J_v$) is driven by both hydrostatic ($\Delta p$) and osmotic ($\Delta \pi$) pressure differences, modulated by the barrier's **hydraulic permeability ($L_p$)** and **[reflection coefficient](@entry_id:141473) ($\sigma$)**:
$$
J_v = L_p (\Delta p - \sigma \Delta \pi)
$$
The [reflection coefficient](@entry_id:141473) ($\sigma$, ranging from 0 to 1) quantifies the selectivity of the barrier; $\sigma=1$ means the solute is completely reflected and exerts its full osmotic potential, while $\sigma=0$ means it passes as freely as water.

Crucially, the solute flux ($J_s$) is not just diffusive but also has a convective component due to being dragged along by the solvent flux. This is known as **[solvent drag](@entry_id:174626)**. The total solute flux is :
$$
J_s = P_s \Delta c + (1-\sigma)\bar{c}J_v
$$
The first term is the Fickian diffusive flux, while the second term is the [solvent drag](@entry_id:174626) contribution, where $\bar{c}$ is the mean [solute concentration](@entry_id:158633) across the barrier. The term $(1-\sigma)$ acts as a solvent [drag coefficient](@entry_id:276893). This framework is essential for accurately modeling transport across leaky endothelia, where hydrostatic and osmotic pressures drive significant convective transport of both water and small solutes. For a barrier with a reflection coefficient of $0.15$ under typical pressure gradients, the [solvent drag](@entry_id:174626) can contribute a substantial solute flux, on the order of $8.18 \times 10^{-9}\,\mathrm{mol}\,\mathrm{m}^{-2}\,\mathrm{s}^{-1}$ .

#### Interfacial and Boundary Phenomena

Beyond [bulk transport](@entry_id:142158) and reaction, phenomena at the interfaces between fluid, cells, and device materials are critical.

The transport of a solute from the flowing perfusate to the surface of a tissue construct is often modeled using a **mass transfer coefficient ($h$)**, which encapsulates the complex fluid dynamics of the boundary layer into a single parameter. The ratio of the resistance to [mass transfer](@entry_id:151080) inside the tissue (internal resistance) to the resistance at the fluid-tissue interface (external resistance) is captured by the **Biot number ($Bi$)** :
$$
Bi = \frac{\text{Internal Resistance}}{\text{External Resistance}} = \frac{L/D_t}{1/h} = \frac{hL}{D_t}
$$
where $L$ is the tissue thickness and $D_t$ is the diffusivity in the tissue. If $Bi \ll 1$, transport is limited by the interface; if $Bi \gg 1$, transport is limited by diffusion within the tissue.

A practical, non-[ideal boundary](@entry_id:200849) phenomenon is the **nonspecific adsorption** of hydrophobic compounds to device materials, particularly poly(dimethylsiloxane) (PDMS). This can lead to significant loss of a drug from the medium, confounding experimental results. By modeling the OoC chamber as a well-mixed reactor at steady state, we can derive the fractional loss of solute, $f = 1 - C_{out}/C_{in}$, due to first-order [surface adsorption](@entry_id:268937) :
$$
f = \frac{k_a S}{Q + k_a S}
$$
where $k_a$ is the [surface adsorption](@entry_id:268937) coefficient, $S$ is the wetted surface area, and $Q$ is the flow rate. This equation highlights a critical scaling issue: as devices are miniaturized, their surface-area-to-volume ratio increases, potentially exacerbating fractional loss. For a typical PDMS device, this loss can be substantial, with a calculated $f$ of over $0.5$, meaning more than half the drug is lost to the device walls before it can interact with the cells .

### Principles of Scaling and Biomimicry

The ultimate goal of OoC modeling is to achieve physiological relevance. This is a problem of scaling. The key insight from dimensional analysis is that [biomimicry](@entry_id:154466) is achieved not by matching individual physical parameters (e.g., matching the exact size of a blood vessel), but by matching the dimensionless groups that govern the system's behavior. To replicate *in vivo* function, one must strive to match the *in vivo* values of $Pe$, $Da$, and $Bi$, as these ratios dictate the balance of advection, diffusion, reaction, and interfacial transport that cells actually experience . The Reynolds number is less critical to match exactly, as long as it remains in the correct laminar regime ($Re \ll 1$).

However, achieving this matching is non-trivial and reveals fundamental engineering trade-offs. Consider the challenge of simultaneously matching two critical physiological parameters in a geometrically scaled-down [microchannel](@entry_id:274861): the mean **residence time** of a fluid parcel ($t_r = V/Q$) and the **wall shear stress** ($\tau_w$).

To match residence time in a channel whose cross-section is scaled by a factor $s$ ($w_c = sw_*$, $h_c=sh_*$) but whose length $L_c$ may not be scaled by the same factor, the flow rate $Q_c$ must be set to $Q_c = Q_* (s^2 L_c / L_*)$. To match wall shear stress, the flow rate must be set to $Q_c = Q_* s^3$. These two conditions can only be satisfied simultaneously if $L_c = s L_*$ .

If the device length is constrained by other factors (e.g., the size of a chip), a trade-off is inevitable. If one chooses to match the residence time, the resulting wall shear stress will be mismatched by a factor $r = \tau_{w,c}/\tau_{w,*} = L_c / (s L_*)$. For a system scaled down by $s=0.1$, if the on-chip length is five times longer than the ideally scaled length, the shear stress will be five times higher than the *in vivo* target when residence time is matched . This illustrates a crucial lesson in OoC design: simple [geometric scaling](@entry_id:272350) often leads to complex, coupled changes in the physical microenvironment, and quantitative modeling is essential to understand and navigate the resulting trade-offs.