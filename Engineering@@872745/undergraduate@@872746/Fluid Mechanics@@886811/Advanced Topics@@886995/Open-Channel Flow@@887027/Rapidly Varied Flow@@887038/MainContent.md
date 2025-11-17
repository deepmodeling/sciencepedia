## Introduction
In the study of [open-channel hydraulics](@entry_id:273093), flows are often characterized by how their properties change over distance. While uniform and gradually varied flows describe many natural and engineered conditions, a distinct and critical regime exists where flow depth and velocity change dramatically over a very short distance. This phenomenon, known as **Rapidly Varied Flow (RVF)**, is fundamental to the behavior of water around hydraulic structures and in dynamic natural events. Understanding RVF is not merely an academic exercise; it is essential for the safe and efficient design of dams, weirs, spillways, and culverts, where abrupt changes in flow conditions are intentionally created or must be safely managed.

This article addresses the challenge of analyzing these complex, high-energy transitions, which cannot be described by the simplified assumptions used for [gradually varied flow](@entry_id:264271). We will bridge the gap between basic fluid principles and the practical tools needed to master RVF. Over the next three chapters, you will gain a comprehensive understanding of this dynamic topic. We will begin in **Principles and Mechanisms** by establishing the theoretical foundation, exploring the Froude number, the concept of specific energy, and the [momentum principle](@entry_id:261235) that governs the iconic [hydraulic jump](@entry_id:266212). Following this, **Applications and Interdisciplinary Connections** will demonstrate how these theories are put into practice to design flow measurement devices and energy dissipators, and how they connect to phenomena in other scientific fields. Finally, **Hands-On Practices** will solidify your knowledge through practical exercises designed to test and reinforce these key concepts.

## Principles and Mechanisms

Following our introduction to the classification of open-channel flows, we now delve into the core principles and mechanisms governing **Rapidly Varied Flow (RVF)**. This regime is characterized by pronounced changes in flow depth and velocity over a comparatively short distance, often accompanied by significant energy transformations. Understanding these phenomena is critical for the design of hydraulic structures such as spillways, gates, and energy dissipators. Our exploration will be grounded in the fundamental concepts of flow classification, specific energy, and the [momentum principle](@entry_id:261235).

### Characterizing Open-Channel Flow: Celerity and the Froude Number

A key distinction in [open-channel flow](@entry_id:267863) is whether the flow is faster or slower than the speed at which a surface disturbance can propagate. This propagation speed, known as the **celerity** ($c$), is a fundamental property of the fluid system.

Imagine a small disturbance, such as a pebble dropped into calm, shallow water. It creates ripples that travel outwards. The speed of these ripples, or waves, depends on the properties of the flow. For a long wave of small amplitude in a shallow body of water of depth $y$, we can determine this celerity. By analyzing the flow from a reference frame moving with the wave, the problem becomes one of [steady flow](@entry_id:264570). Applying the principles of mass and [energy conservation](@entry_id:146975) between an undisturbed upstream section and the wave crest reveals that the celerity is solely a function of the water depth and gravity [@problem_id:1783912]. For a channel that is wide enough for wall effects to be negligible, this relationship is remarkably simple:

$c = \sqrt{gy}$

Here, $g$ is the [acceleration due to gravity](@entry_id:173411). This expression tells us that in shallow water, waves travel faster in deeper water. For channels that are not wide, the depth $y$ is replaced by the **hydraulic depth**, $D_h$, defined as the ratio of the wetted cross-sectional area $A$ to the top surface width $T$. The general expression for celerity is thus:

$c = \sqrt{gD_h}$

The ratio of the mean flow velocity $V$ to the wave celerity $c$ provides a crucial dimensionless parameter for classifying flow: the **Froude number**, $Fr$.

$Fr = \frac{V}{c} = \frac{V}{\sqrt{gD_h}}$

The Froude number represents the ratio of [inertial forces](@entry_id:169104) to gravitational forces. Its value dictates the character of the flow and how it responds to changes in channel geometry or obstructions:

*   **Subcritical Flow ($Fr  1$)**: The flow velocity is less than the wave celerity ($V  c$). The flow is deep and tranquil. Disturbances can propagate upstream, against the flow, allowing for gradual adjustments to downstream conditions. This is analogous to moving slower than the information about upcoming changes.

*   **Supercritical Flow ($Fr > 1$)**: The flow velocity is greater than the wave celerity ($V > c$). The flow is shallow and rapid. Disturbances cannot travel upstream, as the flow sweeps them away. Downstream conditions cannot influence the flow upstream.

*   **Critical Flow ($Fr = 1$)**: The flow velocity is exactly equal to the wave celerity ($V = c$). This state represents a delicate balance and is a key transitional point between subcritical and supercritical regimes.

To illustrate, consider a practical engineering scenario involving a trapezoidal drainage channel [@problem_id:1783906]. For a channel with a bottom width $b$, side slopes $m$ (horizontal distance per unit vertical rise), and flow depth $y$, the area $A$ and top width $T$ are given by $A = y(b+my)$ and $T = b+2my$, respectively. By calculating the hydraulic depth $D_h = A/T$ and the [mean velocity](@entry_id:150038) $V=Q/A$ from the given discharge $Q$, one can compute the Froude number. A result such as $Fr = 1.63$ would immediately classify the flow as supercritical, indicating a rapid, high-velocity state where upstream propagation of waves is impossible.

### The Principle of Specific Energy

While the Froude number classifies the flow state, the concept of **specific energy**, $E$, provides a powerful tool for analyzing changes in that state. Specific energy is defined as the total energy head of the flow with respect to the channel bed. It is the sum of the potential energy head (due to depth) and the kinetic energy head (due to velocity):

$E = y + \frac{V^2}{2g}$

For a given channel geometry and a constant discharge $Q$, the velocity $V$ can be expressed as a function of depth $y$ ($V = Q/A(y)$). This makes the [specific energy](@entry_id:271007) solely a function of depth. For a simple rectangular channel of width $b$, it is often convenient to work with the discharge per unit width, $q = Q/b$. The [specific energy](@entry_id:271007) equation then becomes:

$E = y + \frac{q^2}{2gy^2}$

Plotting $E$ as a function of $y$ for a constant $q$ yields the characteristic **E-y diagram**. This curve reveals several fundamental properties of [open-channel flow](@entry_id:267863). The curve shows that for any given specific energy greater than a certain minimum, there are two possible depths at which the flow can occur [@problem_id:1783923]. These two depths are known as **[alternate depths](@entry_id:193161)**. One is a large depth corresponding to slow, [subcritical flow](@entry_id:276823) (high potential energy, low kinetic energy), and the other is a small depth corresponding to fast, supercritical flow (low potential energy, high kinetic energy).

The E-y curve also exhibits a point of minimum [specific energy](@entry_id:271007), $E_{min}$. The depth at which this minimum occurs is the **[critical depth](@entry_id:275576)**, $y_c$. At this point, the flow is in the [critical state](@entry_id:160700) ($Fr=1$). We can find this depth mathematically by differentiating the specific energy equation with respect to $y$ and setting the derivative to zero, which physically represents finding the depth that can pass a given discharge with the least possible energy [@problem_id:1783954]. For a rectangular channel, this procedure yields:

$\frac{dE}{dy} = \frac{d}{dy} \left( y + \frac{q^2}{2gy^2} \right) = 1 - \frac{q^2}{gy^3} = 0$

Solving for the depth $y$ gives the [critical depth](@entry_id:275576) $y_c$:

$y_c = \left( \frac{q^2}{g} \right)^{1/3}$

At this [critical depth](@entry_id:275576), the specific energy is minimal, and one can verify that the Froude number is exactly one. The minimum [specific energy](@entry_id:271007) is $E_{min} = y_c + q^2/(2gy_c^2) = y_c + y_c/2 = \frac{3}{2}y_c$.

This principle can be extended to channels of arbitrary cross-section. For a channel whose area is described by a power-law relationship $A=ky^m$ [@problem_id:1783907], the general condition for [critical flow](@entry_id:275258), $Fr=1$, translates to the relationship $Q^2/g = A^3/T$. By substituting the expressions for $A$ and $T = dA/dy$, we can derive a general formula for the [critical depth](@entry_id:275576) for that specific geometry, demonstrating the universal applicability of these core principles.

### The Hydraulic Jump: A Phenomenon of Rapid Change

The most dramatic example of rapidly varied flow is the **[hydraulic jump](@entry_id:266212)**. This is a highly turbulent phenomenon where a flow transitions abruptly from a shallow, high-velocity supercritical state ($y_1, V_1, Fr_1 > 1$) to a deep, low-velocity subcritical state ($y_2, V_2, Fr_2  1$). This transition occurs over a very short distance and is characterized by a standing wave, significant surface aeration, and intense mixing.

Due to the extreme turbulence and viscous effects within the jump, [mechanical energy](@entry_id:162989) is not conserved; it is dissipated into thermal energy. Therefore, the [specific energy](@entry_id:271007) of the flow decreases across the jump ($E_2  E_1$). This makes the [energy equation](@entry_id:156281) unsuitable for relating the upstream and downstream conditions.

Instead, we must turn to the conservation of momentum. Over the short length of a [hydraulic jump](@entry_id:266212) on a horizontal channel, the external frictional forces from the bed are negligible compared to the large pressure and momentum flux terms. Applying the [linear momentum equation](@entry_id:262110) to a [control volume](@entry_id:143882) encompassing the jump leads to the concept of **[specific force](@entry_id:266188)**, $M$. The [specific force](@entry_id:266188) is the sum of the [momentum flux](@entry_id:199796) per unit weight and the pressure force resultant per unit weight at a cross-section.

$M = \frac{Q^2}{gA} + A\bar{z}$

Here, $A$ is the cross-sectional area and $\bar{z}$ is the depth of the [centroid](@entry_id:265015) of the area $A$ from the free surface. For a rectangular channel of width $b$, this simplifies to $M = \frac{Q^2}{gby} + \frac{by^2}{2}$ [@problem_id:1783909].

The [momentum principle](@entry_id:261235) dictates that the [specific force](@entry_id:266188) is conserved across the jump: $M_1 = M_2$. This equality allows us to relate the depths before and after the jump, which are called **sequent depths** or **conjugate depths**. For a rectangular channel, this momentum balance yields the celebrated **sequent depth ratio** equation:

$\frac{y_2}{y_1} = \frac{1}{2} \left( \sqrt{1 + 8Fr_1^2} - 1 \right)$

This powerful relationship shows that the downstream depth is determined entirely by the upstream depth and Froude number.

The primary engineering application of the hydraulic jump is as an energy dissipator, for example, in a **[stilling basin](@entry_id:266255)** at the base of a dam spillway [@problem_id:1783886]. The jump effectively "kills" the high kinetic energy of the supercritical flow, preventing [erosion](@entry_id:187476) of the downstream channel bed. The amount of energy dissipated, or **head loss** ($\Delta E$), across the jump is the difference in specific energy:

$\Delta E = E_1 - E_2 = \left( y_1 + \frac{V_1^2}{2g} \right) - \left( y_2 + \frac{V_2^2}{2g} \right)$

This [head loss](@entry_id:153362) is always positive for a jump ($Fr_1 > 1$). A compact and elegant formula for the [head loss](@entry_id:153362) in a rectangular channel can be derived by combining the energy and momentum equations [@problem_id:1783913]:

$\Delta E = \frac{(y_2 - y_1)^3}{4 y_1 y_2}$

The rate of energy dissipation, a measure of power, is then given by $P = \rho g Q \Delta E$. To quantify the efficiency of a jump as an energy dissipator, we can derive an expression for the **fractional [energy dissipation](@entry_id:147406)**, $\frac{\Delta E}{E_1}$. This ratio can be expressed solely as a function of the upstream Froude number, $Fr_1$ [@problem_id:1783934]. Such an expression reveals that the [energy dissipation](@entry_id:147406) efficiency increases dramatically with increasing $Fr_1$, making jumps with high initial Froude numbers extremely effective at dissipating energy.

### Application to Flow Over Obstructions: Choking

Specific energy is also the key to understanding how flows react to changes in the channel bottom elevation, such as a smooth, rounded upward step. For a smooth transition without significant friction, the total energy of the flow is conserved. If the channel bed rises by a height $\Delta z$, the specific energy available to the flow over the step is reduced:

$E_{step} = E_{upstream} - \Delta z$

Consider a supercritical flow approaching such a step. As the flow passes over the step, its depth changes to accommodate the reduced specific energy. If the step height $\Delta z$ is gradually increased, the [specific energy](@entry_id:271007) available over the step, $E_{step}$, decreases. The flow can only adjust its depth as long as $E_{step}$ is greater than or equal to the minimum [specific energy](@entry_id:271007), $E_{min}$, required to pass the given discharge.

This leads to the critical condition known as **choking** [@problem_id:1783930]. Choking occurs when the step height is just large enough to reduce the available [specific energy](@entry_id:271007) to the minimum possible value. At this point, the flow over the crest of the step becomes critical ($Fr_{step} = 1$), and the depth over the step is the [critical depth](@entry_id:275576), $y_c$. The maximum step height, $\Delta z_{max}$, that can be installed without choking the flow is therefore:

$\Delta z_{max} = E_{upstream} - E_{min}$

If the step height exceeds this maximum value, the given upstream flow conditions are no longer possible. The flow is "choked" and a backwater effect will occur, forcing the upstream depth to increase until it has enough energy to pass over the obstruction. This principle is fundamental to the design of control structures like weirs and flumes, where forcing the flow through a critical condition is used to establish a unique relationship between depth and discharge for flow measurement.