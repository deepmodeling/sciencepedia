## Introduction
The ability to precisely remove material from a substrate is fundamental to modern semiconductor manufacturing, directly impacting device performance, yield, and cost. However, the material removal rate (MRR) is rarely uniform, exhibiting a complex dependence on the underlying circuit pattern. This spatial variation, if not understood and controlled, leads to critical defects and process variability. This article provides a comprehensive framework for modeling MRR and its pattern dependence, addressing the gap between idealized process assumptions and the physical reality of fabrication.

The following chapters will guide you through this complex topic. The first chapter, **"Principles and Mechanisms,"** delves into the fundamental physics governing MRR in [plasma etching](@entry_id:192173) and Chemical Mechanical Planarization (CMP), exploring concepts like Aspect Ratio Dependent Etching (ARDE), microloading, and the convolution model. The second chapter, **"Applications and Interdisciplinary Connections,"** demonstrates how these models are applied in practice for predictive simulation, Design for Manufacturability (e.g., [dummy fill](@entry_id:1124032)), and advanced [process control](@entry_id:271184), highlighting connections to fields like [optimal control](@entry_id:138479) and [applied mathematics](@entry_id:170283). Finally, the third chapter, **"Hands-On Practices,"** offers practical exercises to solidify your understanding by deriving rate laws, modeling statistical effects, and designing an optimized [dummy fill](@entry_id:1124032) pattern. We begin by establishing the foundational principles and mechanisms that drive pattern-dependent material removal.

## Principles and Mechanisms

The removal of material from a substrate is the central physical action in numerous semiconductor manufacturing processes, including plasma etching and Chemical Mechanical Planarization (CMP). The rate at which material is removed, and its spatial variation across a patterned wafer, are critical [determinants](@entry_id:276593) of process outcome, influencing device performance, yield, and manufacturing cost. This chapter elucidates the fundamental principles governing the material removal rate (MRR) and the key mechanisms that give rise to its complex dependence on the circuit pattern.

### Fundamental Definition of Material Removal Rate

At its core, the **material removal rate (MRR)**, denoted as $R$, is a measure of the change in material thickness over time. For a process that removes a thickness $H$ from a surface, the instantaneous removal rate at time $t$ is formally defined as the time derivative of the removed thickness:

$$
R(t) = \frac{\mathrm{d}H(t)}{\mathrm{d}t}
$$

This definition is universal, applying to any subtractive process. In practice, however, instantaneous rates are difficult to measure directly. Instead, we typically characterize an average rate over a specific time interval. It is crucial to distinguish between different types of averaging. A simple average taken over the entire process duration, $R_{avg} = H_{total}/T_{total}$, may obscure important dynamics, such as initial start-up transients where process conditions are not yet stable.

A more scientifically sound approach, particularly for [process modeling](@entry_id:183557) and control, is to measure the rate during a period of **quasi-steady-state** operation. This involves taking at least two measurements of removed thickness, $H(t_1)$ and $H(t_2)$, after any initial transients have subsided. The steady-state rate $R_{steady}$ is then calculated as:

$$
R_{steady} = \frac{H(t_2) - H(t_1)}{t_2 - t_1}
$$

This [finite difference](@entry_id:142363) provides a robust approximation of the derivative $\mathrm{d}H/\mathrm{d}t$ during the stable phase of the process.

It is also important to distinguish a time-based rate (e.g., in units of nm/min) from an event-based metric. In a pulsed plasma process, for instance, one could define an etch depth per pulse. While this metric is related to the time-based rate through the pulse frequency, the fundamental definition of rate in physics is based on the continuous variable of time .

A foundational concept in MRR modeling is **pattern dependence**: the observation that the removal rate is not uniform across a wafer but varies with the local geometric layout. A simple demonstration of this is found in [plasma etching](@entry_id:192173), where two adjacent windows with different open-area fractions (the fraction of the local area exposed to the etch chemistry) will exhibit significantly different removal rates, even under globally uniform plasma conditions . Understanding the physical origins of this pattern dependence is the primary goal of advanced MRR modeling. We will explore these mechanisms in the context of both plasma etching and CMP.

### Mechanisms of Pattern Dependence in Plasma Etching

In low-pressure plasma etching, pattern-dependent variations in etch rate, often termed **etch loading effects**, arise from limitations in the transport and consumption of reactive species. These effects can be broadly categorized by the physical scale at which they operate: the feature scale and the die or reactor scale.

#### Feature-Scale Effects: Aspect Ratio Dependent Etching (ARDE)

One of the most critical feature-scale phenomena is **Aspect Ratio Dependent Etching (ARDE)**, also known as RIE lag. This refers to the general observation that features with a higher **aspect ratio (AR)**—defined as the ratio of a feature's depth $d$ to its width $w$, $\mathrm{AR} = d/w$—tend to etch more slowly than features with a lower aspect ratio.

The physical origin of ARDE lies in transport limitations within the feature itself, particularly in the **free-molecular (or Knudsen) regime**, where the mean free path of gas molecules is much larger than the feature dimensions ($\lambda \gg w$) . In this regime, reactive neutral species travel in straight lines until they collide with a surface. For a particle to reach the bottom of a high-AR trench, it must traverse a long, narrow opening. This journey is impeded in two ways:

1.  **Geometric Shadowing:** The solid angle through which particles can directly enter from the plasma bulk and reach the bottom of the trench decreases significantly as AR increases.
2.  **Sidewall Collisions:** Particles are more likely to collide with the sidewalls one or more times before reaching the bottom. If the sidewalls have a non-zero reaction or "sticking" probability $s_w$, each collision presents an opportunity for the reactive species to be consumed, thus depleting the flux of reactants that ultimately reaches the feature bottom .

This process can be modeled by considering the [steady-state flux](@entry_id:183999) of a reactive species into a trench. Let's assume 1D transport along the trench axis, where the flux is described by Knudsen diffusion, $J = -D_K \frac{dC}{dz}$, and the reaction at the bottom is first-order, $J_{rxn} = k_s C_b$. Here, $D_K$ is the Knudsen diffusivity (proportional to $w\bar{v}$, where $\bar{v}$ is the mean thermal speed), $k_s$ is the surface [reaction rate constant](@entry_id:156163), and $C_b$ is the reactant concentration at the trench bottom. By equating the transport flux to the reaction flux at steady state, one can derive an expression for the etch rate $R$, which is proportional to $J_{rxn}$. The result shows that the overall process is governed by two resistances in series: a transport resistance and a reaction resistance. The resulting rate takes the general form :

$$
R \propto \frac{1}{1 + \beta \cdot \mathrm{AR}}
$$

where $\beta$ is a dimensionless number that compares the intrinsic reaction rate to the transport rate. This model reveals two important limiting regimes:

*   **Reaction-Limited Regime:** When transport is fast compared to the surface reaction (e.g., low AR or slow chemistry), the rate is limited by the [reaction kinetics](@entry_id:150220) ($R \propto k_s C_0$) and is largely independent of the aspect ratio.
*   **Transport-Limited Regime:** When the surface reaction is very fast compared to transport (e.g., high AR or fast chemistry), the rate becomes limited by the supply of reactants. In this limit, the model predicts that the etch rate scales inversely with the aspect ratio, $R \propto 1/\mathrm{AR}$ .

#### Die-Scale Effects: Microloading

Whereas ARDE is a feature-scale effect, **microloading** is a die-scale or reactor-scale phenomenon. It is defined as the dependence of the local etch rate on the **local open-area fraction** $\phi$, which is the fraction of the surface in a given region that is being etched. Generally, regions with a higher open-area fraction etch more slowly than regions with a lower open-area fraction.

The physical origin of microloading is the **global depletion of reactive neutrals** within the reactor. The total consumption of reactants is proportional to the total exposed area on the wafer. A wafer with a higher average open-area fraction presents a larger reactive load to the plasma, consuming more reactants and thus lowering the average steady-state concentration $n$ of those species throughout the reactor. By writing a simple [mass balance](@entry_id:181721) for the reactive species in the reactor at steady state, we can see this effect explicitly :

$$
G = \frac{nV}{\tau_g} + \frac{1}{4} n \bar{v} A_w \phi_{avg} s_{eff}
$$

Here, $G$ is the generation rate of the species, $V$ is the reactor volume, $\tau_g$ is the gas residence time, $A_w$ is the wafer area, and $\phi_{avg}$ is the wafer-averaged open area. Solving for the steady-state concentration $n$ shows that $n$ decreases as $\phi_{avg}$ increases. Local variations in $\phi$ on the die create local variations in this depletion, resulting in a spatially varying etch rate.

Microloading and ARDE are distinct phenomena originating at different physical scales. Consequently, they can be partially decoupled and mitigated by different process controls. For example, increasing the total gas flow rate reduces the residence time $\tau_g$, making the pumping loss term dominant and stabilizing the reactant concentration $n$ against variations in the reactive load $\phi_{avg}$. This primarily mitigates microloading. In contrast, ARDE is best mitigated by targeting the feature-scale physics, for instance, by altering the surface chemistry to reduce the sidewall sticking probability $s_w$ or by using ion-assistance to preferentially enhance the bottom reaction rate .

### Mechanisms of Material Removal in Chemical Mechanical Planarization (CMP)

Chemical Mechanical Planarization (CMP) is a process that relies on the synergistic action of chemistry and mechanics to achieve planar surfaces. Its MRR is governed by a different, though equally complex, set of physical principles.

#### The Preston Equation and the Nature of the Preston Coefficient

The empirical cornerstone of CMP modeling is **Preston's Law**, which posits that the material removal rate is directly proportional to the applied pressure $P$ and the relative sliding velocity $V$ between the pad and the wafer:

$$
R = KPV
$$

The proportionality factor $K$ is known as the **Preston coefficient**. This simple linear relationship can be derived from first principles by combining a tribological wear model (such as Archard's law, which states that the volume of wear is proportional to the [real area of contact](@entry_id:152017) and the sliding distance) with a contact mechanics model that assumes the [real area of contact](@entry_id:152017) between the pad asperities and the wafer is proportional to the applied load .

However, this linear law is an idealization that holds only in specific regimes of boundary or mixed [lubrication](@entry_id:272901), at moderate pressures and velocities. At high pressures, the pad asperities begin to flatten, and the real contact area no longer increases linearly with load. At high velocities, a hydrodynamic fluid film can form, lifting the wafer off the pad, or the process may become limited by the rate of chemical reactions or transport of species in the slurry. These effects lead to a sub-linear, saturating behavior of the removal rate .

Crucially, the Preston coefficient $K$ is not a universal constant. It is a composite parameter that encapsulates the complex interplay of a multitude of physical and chemical processes occurring at the interface . Its value depends on:

*   **Slurry Chemistry:** The type and concentration of chemical agents (e.g., oxidizers, complexing agents) determine the rate constant $k_{chem}$ of the surface reaction.
*   **Pad Properties:** The mechanical properties (modulus, thickness) and micro-topography ([asperity](@entry_id:197484) density and shape) of the pad dictate the contact mechanics and the [real area of contact](@entry_id:152017).
*   **Lubrication Regime:** The thickness of the slurry film, which depends on $P$, $V$, and slurry viscosity, determines the degree of solid-solid contact.

Because $K$ is not fundamental, it can evolve over time. During polishing, the pad surface undergoes **glazing**, a process where asperities are worn down and plastically deformed, and pores become clogged with polishing debris. This leads to a reduction in [asperity](@entry_id:197484) density and an increase in asperity tip radius. The result is lower contact stresses and impeded slurry transport, causing a decrease in $K$ and a drift-down in the MRR. To counteract this, pads are periodically "dressed" or **conditioned** using a diamond-impregnated disk. This mechanical abrasion re-roughens the surface, restoring the asperity population and reopening pores, which abruptly resets $K$ to a higher value. Over many cycles, this results in a characteristic sawtooth temporal pattern for the MRR .

#### Reaction-Diffusion Limits in CMP

The "chemo-mechanical" nature of CMP can be analyzed using [reaction-diffusion models](@entry_id:182176), similar to those in etching. The removal of a material like copper often involves its oxidation by a species in the slurry, followed by mechanical abrasion of the soft oxide layer. The overall rate can be limited by either the chemical reaction rate or the transport of the oxidizing species to the wafer surface.

We can model this by considering a [one-dimensional diffusion](@entry_id:181320) of an oxidizer across an effective boundary layer of thickness $L$, coupled with a first-order [surface reaction](@entry_id:183202) with rate constant $k_s$. At steady state, the [diffusive flux](@entry_id:748422) must equal the reactive flux. This balance allows us to solve for the removal rate. The competition between these two processes is captured by a dimensionless group known as the surface **Damköhler number**, $Da$:

$$
Da = \frac{\text{characteristic reaction rate}}{\text{characteristic diffusion rate}} = \frac{k_s L}{D}
$$

where $D$ is the diffusivity of the oxidizer in the slurry . The value of $Da$ dictates the limiting regime:

*   **$Da \ll 1$ (Reaction-Limited):** The reaction is slow compared to transport. The removal rate is controlled by the [surface chemistry](@entry_id:152233) ($R \approx M k_s C_{\infty}$, where $M$ is a conversion factor and $C_{\infty}$ is the bulk oxidizer concentration) and is insensitive to transport limitations.
*   **$Da \gg 1$ (Transport-Limited):** The reaction is very fast. The rate is limited by how quickly the oxidizer can diffuse to the surface ($R \approx M D C_{\infty} / L$). In this regime, [pattern density](@entry_id:1129445) can play a significant role. For instance, dense patterns can increase the tortuosity of the diffusion path, effectively increasing $L$ and thus locally reducing the removal rate .

#### The Convolution Model for Pattern Density Effects

The most significant source of pattern dependence in CMP arises from the mechanical compliance of the polishing pad. Raised features on the wafer press into the compliant pad, and the pad redistributes this pressure over a characteristic lateral distance. This means the pressure at any given point on the wafer is not determined just by whether that point is "up" or "down," but by the average feature density in a surrounding neighborhood.

For a linear, shift-invariant system, this spatial averaging can be elegantly described by a **[convolution integral](@entry_id:155865)**. The local removal rate $R(\mathbf{x})$ is modeled as a baseline blanket rate $R_0(\mathbf{x})$ plus a term that accounts for the pattern:

$$
R(\mathbf{x}) = R_0(\mathbf{x}) + \int_{\mathbb{R}^2} K(\mathbf{x}-\mathbf{y}) \rho(\mathbf{y}) \mathrm{d}\mathbf{y} = R_0(\mathbf{x}) + (K * \rho)(\mathbf{x})
$$

In this powerful model :
*   $\rho(\mathbf{y})$ is the local **pattern density** at location $\mathbf{y}$, often defined as the local fraction of "up" area.
*   $K(\mathbf{r})$ is the **[influence function](@entry_id:168646)** or **kernel**, which describes how a point of high density at one location influences the pressure (and thus the removal rate) at another location. The range of this kernel is often called the **planarization length**.
*   $R_0(\mathbf{x})$ is the baseline removal rate that would be observed on a blanket (unpatterned) wafer. It can be spatially non-uniform due to tool-level effects like carrier head [pressure distribution](@entry_id:275409) or velocity variations across the wafer radius.

The kernel $K(\mathbf{r})$ is not simply a blurring function. Because the total downforce on the wafer is fixed, if some areas experience higher-than-average pressure, other areas must experience lower-than-average pressure to maintain [force balance](@entry_id:267186). Consequently, the kernel typically has a central lobe surrounded by a region of opposite sign. For instance, a high-density region (which stands proud) experiences high pressure, leading to a positive contribution to removal. To compensate, the surrounding lower-density regions are shielded from pressure by the pad, leading to a negative contribution to removal in those areas. The kernel thus reflects this pressure redistribution .

The width of this kernel, $\sigma$, is a critical parameter. It can be physically modeled by treating the pad as a thin elastic plate resting on a compliant foundation (a "plate-on-elastic-foundation" model). The characteristic length $\sigma$ emerges from the balance between the pad's ability to transmit shear laterally (proportional to its shear modulus $G_p$ and thickness $t_p$) and the vertical stiffness $K_{found}$ of its [asperity](@entry_id:197484)-based foundation. This leads to a scaling relationship of the form :

$$
\sigma \sim \sqrt{\frac{G_p t_p}{K_{found}}}
$$

The foundation stiffness $K_{found}$ itself can be derived from micro-[contact mechanics](@entry_id:177379) models (e.g., Hertzian contact, Greenwood-Williamson models), revealing its dependence on [asperity](@entry_id:197484) geometry, pad modulus, and applied pressure. This provides a deep physical linkage from the microscopic properties of the pad to the macroscopic planarization length observed in manufacturing .

#### Consequences: Topography Evolution, Dishing, and Erosion

Ultimately, the motivation for modeling MRR is to predict and control the evolution of the wafer's surface topography. In damascene interconnect fabrication, where metal (like copper) is inlaid into a dielectric (like SiO$_2$), non-uniform removal rates lead to critical defects after the initial metal "overburden" is cleared. During the subsequent **overpolish** step, both metal and dielectric are exposed to the pad. Because the softer metal typically polishes faster than the harder dielectric ($R_{Cu} > R_{SiO_2}$), topography is created.

Two key defects are :
*   **Dishing:** Within a single wide metal line, the center polishes faster than the edges, which are supported by the adjacent, slower-polishing dielectric. This creates a concave "dish" in the metal feature. The maximum dishing depth is proportional to the difference in removal rates and the duration of the overpolish: $D_{max} \approx (R_{Cu} - R_{SiO_2}) t_{over}$.
*   **Erosion:** In a dense array of fine metal lines, the entire region, being mechanically weaker on average than a solid dielectric region, compresses the pad more and experiences a higher local pressure. This leads to an excessive removal of the dielectric within the array, a defect known as erosion.

These phenomena highlight the direct link between the fundamental mechanisms of material removal and the final, device-critical wafer topography. Accurate, physically-based models of material removal rate and its pattern dependence are therefore indispensable tools for modern semiconductor process development and control.