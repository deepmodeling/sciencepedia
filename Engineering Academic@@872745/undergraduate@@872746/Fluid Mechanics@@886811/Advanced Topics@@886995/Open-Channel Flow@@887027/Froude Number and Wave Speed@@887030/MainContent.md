## Introduction
In the realm of [fluid mechanics](@entry_id:152498), the behavior of water in rivers, oceans, and engineered channels is governed by a constant struggle between the fluid's inertia and the pull of gravity. Understanding this dynamic is crucial for everything from designing safe bridges to predicting the path of a tsunami. The key to unlocking this understanding lies in a single, powerful dimensionless parameter: the Froude number. This article provides a foundational exploration of the Froude number, addressing the knowledge gap between basic fluid principles and their application in complex free-surface flows. It illuminates how this number quantifies the critical relationship between flow velocity and wave propagation speed, dictating the very nature of the flow.

Across the following chapters, you will gain a multi-faceted understanding of this fundamental concept. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, deriving the speed of [shallow water waves](@entry_id:267231) and defining the Froude number, its physical significance, and its connection to flow energy. Building on this foundation, the "Applications and Interdisciplinary Connections" chapter showcases the remarkable versatility of the Froude number, demonstrating its use in civil engineering, [naval architecture](@entry_id:268009), [geosciences](@entry_id:749876), and even as an analogue for phenomena in astrophysics. Finally, the "Hands-On Practices" section will allow you to apply these principles to solve practical problems, solidifying your grasp of how to analyze and engineer systems governed by these powerful fluid dynamics principles.

## Principles and Mechanisms

In the study of fluid mechanics, particularly in flows with a free surface such as rivers, canals, and the ocean, the interaction between the fluid's inertia and the force of gravity gives rise to a rich variety of phenomena. The balance between these forces is encapsulated by a fundamental dimensionless parameter, the Froude number, which governs the behavior of surface waves and the classification of [flow regimes](@entry_id:152820). This chapter explores the principles underlying the Froude number and its connection to [wave speed](@entry_id:186208), elucidating the mechanisms through which it dictates the dynamics of open-channel flows and other related systems.

### The Celerity of Surface Waves in Shallow Water

Imagine a disturbance on the surface of still water, such as the ripple created by a gentle tap. This disturbance does not remain localized; it propagates outwards as a wave. The speed of this wave, known as its **celerity** ($c$), is a crucial property of the medium. For waves whose wavelength is significantly longer than the water depth, a condition known as the **shallow-water approximation**, the primary restoring force is gravity. In this regime, the wave celerity is independent of the wavelength and is determined solely by the [acceleration due to gravity](@entry_id:173411), $g$, and the local water depth, $h$.

The celerity of a small-amplitude shallow-water wave is given by the remarkably simple and powerful formula:

$$c = \sqrt{gh}$$

This equation reveals that waves travel faster in deeper water. For instance, in a decorative fountain with a uniform water depth of $0.150$ meters, a small ripple will propagate at a speed of $c = \sqrt{9.81 \, \text{m/s}^2 \times 0.150 \, \text{m}} \approx 1.21 \, \text{m/s}$ [@problem_id:1758900]. It is important to recognize that this is the speed of the wave *relative to the fluid*. If the fluid itself is moving, the wave's speed relative to a stationary observer will be different.

Because the celerity depends on the local depth, waves will change speed as they travel through regions of varying depth. Consider a wave propagating over a seabed with a linearly increasing depth profile. The total time taken for the wave to travel a certain distance is not simply the distance divided by a constant speed, but rather the integral of the inverse of the local celerity over the path. For a wave traveling from a point A to a point B over a distance $L$, the travel time $T_{\text{wave}}$ is:

$$T_{\text{wave}} = \int_{A}^{B} \frac{dx}{c(x)} = \int_{0}^{L} \frac{dx}{\sqrt{g h(x)}}$$

This principle has practical consequences. For example, to ensure an autonomous underwater vehicle (AUV) can outpace a surface wave generated at its starting point, its speed must be calculated by considering the wave's changing celerity over the variable-depth path. For a path from depth $h_A$ to $h_B$, the AUV's required average speed to arrive simultaneously with the wave can be shown to be the arithmetic mean of the wave celerities at the start and end points: $v_{\text{AUV}} = \frac{1}{2}(\sqrt{gh_A} + \sqrt{gh_B})$ [@problem_id:1758887].

### The Froude Number and Flow Regimes

In most practical scenarios, such as rivers and canals, the fluid itself is in motion with a characteristic velocity $V$. The dynamics of the flow are critically dependent on the comparison between this flow velocity $V$ and the wave celerity $c$. This comparison is formalized by the **Froude number** ($Fr$), a dimensionless quantity defined as the ratio of the flow velocity to the wave celerity:

$$Fr = \frac{V}{c} = \frac{V}{\sqrt{gh}}$$

The Froude number quantifies the relative importance of the flow's inertia (related to $V$) to the gravitational forces (which determine $c$). The magnitude of the Froude number allows us to classify open-channel flows into three distinct regimes:

*   **Subcritical Flow ($Fr  1$)**: In this regime, the flow velocity is less than the wave celerity ($V  c$). The flow is often described as tranquil or streaming. Because waves can travel faster than the flow, disturbances are able to propagate both upstream and downstream. A leaf dropped into a channel with [subcritical flow](@entry_id:276823) will create ripples that expand in all directions, including against the current [@problem_id:1758881].

*   **Supercritical Flow ($Fr > 1$)**: Here, the flow velocity is greater than the wave celerity ($V > c$). The flow is described as rapid, shooting, or torrential. Inertial forces dominate. Any disturbance created on the surface is swept downstream because the flow is moving too fast for the wave to make headway against it. Ripples will only be observed downstream of the point of disturbance [@problem_id:1758881].

*   **Critical Flow ($Fr = 1$)**: This is the transitional state where the flow velocity is exactly equal to the wave celerity ($V = c = \sqrt{gh}$) [@problem_id:1758879]. This condition holds special significance in hydraulics, often corresponding to points of minimum energy or maximum discharge, and represents the boundary between the subcritical and supercritical regimes.

### Energetic Interpretation of the Froude Number

The Froude number is more than just a ratio of speeds; it carries a deep physical meaning related to the energy of the flow. We can demonstrate that the square of the Froude number, $Fr^2$, represents the ratio of the flow's specific kinetic energy to its average specific potential energy [@problem_id:1758911].

Let us define the **[specific energy](@entry_id:271007)** as the energy per unit mass. For a fluid moving at speed $V$, the **specific kinetic energy** is simply:

$$e_k = \frac{1}{2}V^2$$

The **specific potential energy** requires more careful consideration. For a vertical column of fluid of depth $h$, the potential energy is not uniform, as fluid particles near the surface have more potential energy than those at the bottom. To find the average specific potential energy, we integrate the potential energy of the entire column and divide by its total mass. The [total potential energy](@entry_id:185512) $U$ of a column with base area $A$ is found by integrating the potential energy $gz$ of infinitesimal layers of mass $dm = \rho A \, dz$:

$$U = \int_{0}^{h} (gz) (\rho A \, dz) = \rho g A \int_{0}^{h} z \, dz = \frac{1}{2} \rho g A h^2$$

The total mass $M$ of this column is $M = \rho A h$. Therefore, the average specific potential energy $e_{p, \text{avg}}$ is:

$$e_{p, \text{avg}} = \frac{U}{M} = \frac{\frac{1}{2} \rho g A h^2}{\rho A h} = \frac{1}{2}gh$$

Now, taking the ratio of the specific kinetic energy to the average specific potential energy, we find:

$$\frac{e_k}{e_{p, \text{avg}}} = \frac{\frac{1}{2}V^2}{\frac{1}{2}gh} = \frac{V^2}{gh}$$

This is precisely the definition of the Froude number squared.

$$Fr^2 = \frac{V^2}{gh} = \frac{\text{Specific Kinetic Energy}}{\text{Average Specific Potential Energy}}$$

This powerful interpretation frames the Froude number as a direct measure of the balance between inertial (kinetic) and gravitational (potential) energies in the flow.

### Applications in Open-Channel Hydraulics

The concepts of Froude number and [critical flow](@entry_id:275258) are central to the engineering design and analysis of open channels, such as canals, rivers, and spillways.

#### Specific Energy and Critical Depth

In [open-channel hydraulics](@entry_id:273093), it is convenient to work with energy per unit weight, known as **head**. The **specific energy** $E$ is the total head relative to the channel bottom:

$$E = y + \frac{V^2}{2g}$$

Here, $y$ is the flow depth (potential energy head) and $\frac{V^2}{2g}$ is the velocity head (kinetic energy head). For a given discharge per unit width, $q = Vy$, there is a unique depth, the **[critical depth](@entry_id:275576)** $y_c$, at which the specific energy is at a minimum. This minimum energy condition corresponds exactly to [critical flow](@entry_id:275258), $Fr=1$.

Conversely, for a fixed specific energy $E$, there is a maximum possible discharge per unit width, $q_{max}$, that the channel can convey. This maximum discharge condition also occurs precisely when the flow is critical [@problem_id:1758888]. At this state, the velocity head is exactly half the potential energy head:

$$\frac{V^2}{2g} = \frac{y}{2}$$

Substituting $V = \sqrt{gy}$ (the condition for $Fr=1$), we confirm this relationship: $\frac{(\sqrt{gy})^2}{2g} = \frac{gy}{2g} = \frac{y}{2}$. This principle is fundamental to the design of control structures that regulate flow.

#### Flow Over Obstructions and Wave Drag

A classic application of these principles is the analysis of flow over a smooth, submerged hump on a channel floor. As a [subcritical flow](@entry_id:276823) ($Fr  1$) approaches the hump, it must rise over it. To conserve energy, the fluid accelerates, and its depth decreases. If the hump is sufficiently high, the flow can be forced to reach the [critical state](@entry_id:160700) ($Fr=1$) at the crest of the hump. This condition is known as **choking**, as any further increase in the hump's height cannot be accommodated by the upstream flow without altering its depth; the hump effectively acts as a dam, backing up the water upstream. The maximum height of a hump that a given [subcritical flow](@entry_id:276823) can pass over without choking corresponds to the difference between the initial [specific energy](@entry_id:271007) and the minimum (critical) [specific energy](@entry_id:271007) required at the crest [@problem_id:1758906].

The condition $Fr=1$ is also associated with a dramatic increase in **[wave drag](@entry_id:263999)**. When a vessel, such as a boat or a surface probe, moves at a speed close to the shallow-water wave speed, it is essentially moving in resonance with the waves it generates. It continuously transfers energy into a large wave that it can neither outrun nor leave behind. This results in a significant buildup of wave amplitude and a corresponding sharp peak in drag force around $Fr=1$. This phenomenon, sometimes called the "sound barrier" of [naval architecture](@entry_id:268009), poses a significant design challenge, as it requires a great deal of power to accelerate through the critical speed regime. The stability of a craft's operating speed can be compromised by this drag peak, potentially leading to multiple stable operating speeds or unstable regions where the craft cannot maintain a steady velocity [@problem_id:1758916].

### The Froude Number in Dynamic Similarity and Model Testing

Beyond its role in characterizing [flow regimes](@entry_id:152820), the Froude number is an indispensable tool in experimental fluid dynamics, particularly for **[dynamic similarity](@entry_id:162962)** and model testing. To ensure that a small-scale model accurately predicts the behavior of a full-scale prototype (like a ship), the model flow must be dynamically similar to the full-scale flow. This requires that the ratios of all relevant forces acting on the fluid are the same in both cases.

For phenomena dominated by inertia and gravity, such as the [wave-making resistance](@entry_id:263946) of a ship, [dynamic similarity](@entry_id:162962) is achieved by ensuring that the Froude number of the model is identical to that of the ship [@problem_id:1758950]:

$$Fr_{\text{model}} = Fr_{\text{ship}} \implies \frac{V_m}{\sqrt{gL_m}} = \frac{V_s}{\sqrt{gL_s}}$$

where the subscripts $m$ and $s$ denote the model and ship, respectively, and $L$ is a characteristic length (e.g., the hull length). If the length scale factor is $\lambda = L_s/L_m$, this requirement immediately dictates the relationship between the test speed and the ship speed:

$$V_s = V_m \sqrt{\frac{L_s}{L_m}} = V_m \sqrt{\lambda}$$

This is known as **Froude's law of correspondence**. Furthermore, by analyzing the forces, one can derive scaling laws for other quantities. Wave-making resistance ($R_w$) scales with the product of fluid density, the square of velocity, and a surface area. By maintaining Froude number similarity, the [scaling law](@entry_id:266186) for wave resistance can be shown to be:

$$R_{w,s} = R_{w,m} \left( \frac{\rho_s}{\rho_m} \right) \lambda^3$$

This allows engineers to measure the resistance on a small, manageable model in a towing tank and accurately predict the resistance, and thus the required power, for the full-size vessel.

### Generalization to Stratified Flows: The Internal Froude Number

The concept of a Froude number is not limited to waves on a free surface. It can be generalized to any flow where a density-[stratified fluid](@entry_id:201059) is displaced against the force of gravity. A common example is found in [estuaries](@entry_id:192643), where a layer of lighter freshwater flows over a denser layer of saltwater. Disturbances on the interface between these two layers can propagate as **[internal waves](@entry_id:261048)**.

These [internal waves](@entry_id:261048) are driven by a much weaker restoring force than [surface waves](@entry_id:755682). The effective gravitational acceleration is reduced by the buoyancy effect and is given by the **reduced gravity**, $g'$:

$$g' = g \frac{\Delta\rho}{\rho}$$

where $\Delta\rho$ is the density difference between the layers and $\rho$ is a reference density. The speed of long [internal waves](@entry_id:261048), $c_i$, is analogous to that of [surface waves](@entry_id:755682), but with $g$ replaced by $g'$ and $h$ replaced by an effective depth that depends on the thicknesses of both layers. In the simple case of a thin top layer of thickness $h_1$ flowing over a very deep, quiescent bottom layer, the internal [wave speed](@entry_id:186208) is $c_i = \sqrt{g'h_1}$ [@problem_id:1902650].

To characterize the dynamics of this [stratified flow](@entry_id:202356), we define an **internal Froude number**, $F_i$:

$$F_i = \frac{U}{c_i} = \frac{U}{\sqrt{g'h_1}}$$

Just like the surface Froude number, the internal Froude number distinguishes between subcritical ($F_i  1$) and supercritical ($F_i > 1$) internal flows. This parameter is critical for understanding phenomena such as the formation of internal hydraulic jumps and the mixing processes in oceans, lakes, and the atmosphere, demonstrating the unifying power of this fundamental principle across diverse fluid systems.