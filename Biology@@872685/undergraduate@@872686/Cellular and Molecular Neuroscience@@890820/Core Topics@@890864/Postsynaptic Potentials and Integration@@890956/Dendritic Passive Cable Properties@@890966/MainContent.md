## Introduction
How does a single neuron make sense of the constant barrage of signals it receives from thousands of others? The answer begins in its intricate dendritic tree, where incoming synaptic potentials are filtered, summed, and transformed before they ever reach the cell body. While complex active processes play a role, the fundamental rules governing this integration can be understood through a powerful and elegant framework known as [passive cable theory](@entry_id:193060). This article demystifies how a dendrite's basic electrical properties—its resistance and capacitance—dictate its computational function. We will explore the core concepts of this theory and its profound implications for [neuronal signaling](@entry_id:176759).

This article will guide you through the essentials of [dendritic computation](@entry_id:154049) in three parts. In **Principles and Mechanisms**, we will deconstruct the dendrite into its fundamental electrical components and derive the crucial characteristic constants of time and space that govern [signal propagation](@entry_id:165148). Next, in **Applications and Interdisciplinary Connections**, we will see how these principles explain vital neuronal functions like [synaptic integration](@entry_id:149097), the effects of [neuromodulation](@entry_id:148110), and the rules of [synaptic plasticity](@entry_id:137631). Finally, the **Hands-On Practices** section provides opportunities to apply these concepts to solve concrete neurobiological problems. We begin by examining the biophysical principles and mathematical models that form the foundation of [passive cable theory](@entry_id:193060).

## Principles and Mechanisms

The function of a neuron is critically dependent on how it integrates synaptic signals distributed across its complex dendritic tree. While the generation of action potentials involves active, voltage-dependent processes, the initial propagation and filtering of synaptic potentials along [dendrites](@entry_id:159503) can be largely understood through the lens of passive electrical properties. This framework, known as **[passive cable theory](@entry_id:193060)**, models the dendrite as an electrical cable composed of a series of fundamental resistive and capacitive elements. By understanding these elements and their interplay, we can derive key principles that govern how the location, timing, and shape of synaptic inputs determine their ultimate impact at the soma.

### The Fundamental Electrical Components of a Passive Dendrite

To model the flow of electrical current through a dendrite, we must account for three fundamental passive properties: the resistance of the cell membrane, the capacitance of the cell membrane, and the resistance of the intracellular cytoplasm. These properties arise directly from the biophysical structure of the neuron.

#### Membrane Resistance

A neuron's [lipid bilayer](@entry_id:136413) membrane is a very poor conductor of ions, forming a high-resistance barrier between the intracellular and extracellular fluids. However, this barrier is not perfect. It is studded with various [ion channels](@entry_id:144262), and even at rest, a subset of these channels, often called **[leak channels](@entry_id:200192)**, are open. These open channels provide a pathway for ions to flow across the membrane, creating an [electrical resistance](@entry_id:138948).

This property is quantified by the **[specific membrane resistance](@entry_id:166665)**, denoted as $R_m$ (with units of $\Omega \cdot \text{m}^2$). $R_m$ is an intrinsic property of a unit area of the membrane and is inversely proportional to the density of open [leak channels](@entry_id:200192). If a neurotoxin were to block a fraction of these [leak channels](@entry_id:200192), the total number of paths for current to escape would decrease, and thus the [specific membrane resistance](@entry_id:166665) $R_m$ would increase [@problem_id:2333470].

For a cylindrical dendrite of radius $a$, the total membrane surface area increases with length. We therefore often work with the **membrane resistance per unit length**, $r_m$ (units of $\Omega \cdot \text{m}$). This is calculated by dividing the specific resistance $R_m$ by the circumference of the dendrite ($2\pi a$):

$$r_m = \frac{R_m}{2\pi a}$$

This equation shows that for a given intrinsic membrane resistivity, a thicker dendrite (larger $a$) has more surface area per unit length and thus more parallel pathways for current to leak out, resulting in a lower [membrane resistance](@entry_id:174729) per unit length.

#### Membrane Capacitance

The thin lipid bilayer of the cell membrane also acts as a capacitor. It separates two conductive media—the intracellular cytoplasm and the extracellular fluid—with a very thin insulating layer. This structure allows for the separation and storage of [electrical charge](@entry_id:274596). Any change in the [membrane potential](@entry_id:150996) requires the addition or removal of charge to or from this capacitor.

The intrinsic capacitive property of the membrane is described by the **[specific membrane capacitance](@entry_id:177788)**, $C_m$ (units of $\text{F}/\text{m}^2$). Because the thickness of the [lipid bilayer](@entry_id:136413) is remarkably consistent across different cell types and even different species, the value of $C_m$ is relatively constant in biology, typically around $0.01 \text{ F/m}^2$ (or $1\,\mu\text{F/cm}^2$).

The total capacitance ($C$) of a patch of membrane depends on its surface area ($A$). The fundamental relationship from physics, $Q = C \Delta V$, states that the amount of charge ($Q$) required to change the voltage across a capacitor by an amount $\Delta V$ is proportional to its capacitance. Since the total capacitance of a membrane patch is $C = C_m A$, the charge required for a given [depolarization](@entry_id:156483) is $Q = C_m A \Delta V$ [@problem_id:2333410]. This means that a larger dendritic compartment, or one with a membrane that has intrinsically higher specific capacitance, will require more [synaptic current](@entry_id:198069) (i.e., more charge delivered over time) to achieve the same change in voltage.

Analogous to resistance, for a cylindrical cable, we define the **[membrane capacitance](@entry_id:171929) per unit length**, $c_m$ (units of $\text{F/m}$), as:

$$c_m = C_m (2\pi a)$$

Unlike $r_m$, the capacitance per unit length $c_m$ is directly proportional to the dendritic radius $a$.

#### Axial Resistance

While current can leak out across the membrane, it also flows longitudinally down the core of the dendrite toward the soma. The cytoplasm, being an ionic solution, is not a perfect conductor and resists this flow of current. This is the **[axial resistance](@entry_id:177656)**.

The intrinsic resistivity of the cytoplasm is called the **specific axial [resistivity](@entry_id:266481)**, $\rho_i$ (or sometimes $\rho_a$), with units of $\Omega \cdot \text{m}$. For a dendrite of radius $a$, the cross-sectional area available for current flow is $A = \pi a^2$. The **[axial resistance](@entry_id:177656) per unit length**, $r_a$ (units of $\Omega/\text{m}$), is given by:

$$r_a = \frac{\rho_i}{\pi a^2}$$

This relationship shows that [axial resistance](@entry_id:177656) is inversely proportional to the square of the radius; thicker [dendrites](@entry_id:159503) provide a much wider path for current flow and thus have a dramatically lower [axial resistance](@entry_id:177656). Furthermore, if the intrinsic [resistivity](@entry_id:266481) of the cytoplasm itself were to be reduced, for example by increasing the concentration of mobile ions, $r_a$ would decrease proportionally [@problem_id:2333408].

It is also important to recognize that the cytoplasm is not a simple, empty tube of saline. It is a crowded environment filled with [organelles](@entry_id:154570), cytoskeletal elements, and proteins. These components are largely non-conductive and act as obstacles to the longitudinal flow of ions. This has the effect of reducing the effective cross-sectional area available for conduction. If a fraction $f$ of the cross-sectional area is obstructed, the effective [axial resistance](@entry_id:177656) increases by a factor of $1/(1-f)$ compared to an idealized, empty cylinder [@problem_id:2333442].

### Characteristic Constants of the Dendritic Cable: Time and Length

The three fundamental parameters—$r_m$, $c_m$, and $r_a$—combine to produce two powerful [emergent properties](@entry_id:149306) that characterize the spatiotemporal behavior of the entire cable: the [membrane time constant](@entry_id:168069) and the [space constant](@entry_id:193491).

#### The Membrane Time Constant ($\tau_m$)

When a current is injected into a neuron, the membrane potential does not change instantaneously. The [membrane capacitance](@entry_id:171929) must first be charged or discharged. The speed of this voltage change is characterized by the **[membrane time constant](@entry_id:168069)**, $\tau_m$. It is defined as the product of the [membrane resistance](@entry_id:174729) and capacitance per unit length:

$$\tau_m = r_m c_m$$

A crucial feature of the [time constant](@entry_id:267377) becomes apparent when we substitute the geometry-dependent expressions for $r_m$ and $c_m$:

$$\tau_m = \left(\frac{R_m}{2\pi a}\right) \left(C_m (2\pi a)\right) = R_m C_m$$

This derivation reveals a profound result: the [membrane time constant](@entry_id:168069) is **independent of the dendrite's geometry** (i.e., its radius $a$) [@problem_id:2333473]. It depends only on the intrinsic properties of the membrane itself—its specific resistance and specific capacitance. This means that, assuming the [membrane composition](@entry_id:173244) is uniform, the [time constant](@entry_id:267377) is the same for all parts of a neuron, from the thinnest [dendritic spine](@entry_id:174933) to the large cell body.

The [time constant](@entry_id:267377) $\tau_m$ represents the time it takes for the membrane potential to reach approximately $63\%$ (specifically, $1 - 1/e$) of its final steady-state value in response to a step injection of current. In a typical [current-clamp](@entry_id:165216) experiment, if a hyperpolarizing current pulse changes the membrane potential from $V_{rest}$ to a new steady-state $V_{ss}$, the voltage at any time $t$ follows an exponential curve:

$$V(t) = V_{ss} + (V_{rest} - V_{ss}) \exp\left(-\frac{t}{\tau_m}\right)$$

By measuring the voltage at a known time point during this charging phase, one can solve this equation to experimentally determine the value of $\tau_m$ for the neuron [@problem_id:2333406]. Because $\tau_m = R_m C_m$, any manipulation that alters the [specific membrane resistance](@entry_id:166665), such as blocking [leak channels](@entry_id:200192), will directly change the time constant. Blocking channels increases $R_m$, which in turn increases $\tau_m$, causing the neuron's voltage to respond more sluggishly to input currents [@problem_id:2333470].

#### The Space Constant ($\lambda$)

Just as a voltage change takes time to develop locally, it also decays in amplitude as it propagates along the dendrite. The **[space constant](@entry_id:193491)** (or [length constant](@entry_id:153012)), $\lambda$, is the characteristic distance over which this spatial decay occurs. It is defined by the balance between the current that leaks out across the membrane (governed by $r_m$) and the current that flows down the core of the dendrite (governed by $r_a$):

$$\lambda = \sqrt{\frac{r_m}{r_a}}$$

Intuitively, a signal will travel farther if the [membrane resistance](@entry_id:174729) is high (less leak) and the [axial resistance](@entry_id:177656) is low (easier flow down the core). The [space constant](@entry_id:193491) formally captures this. For a steady-state voltage change injected at one point, $\lambda$ is the distance over which the voltage attenuates to $37\%$ ($1/e$) of its original amplitude.

Unlike the time constant, the [space constant](@entry_id:193491) is **highly dependent on dendritic geometry**. Substituting the expressions for $r_m$ and $r_a$ yields:

$$\lambda = \sqrt{\frac{R_m/(2\pi a)}{\rho_i/(\pi a^2)}} = \sqrt{\frac{R_m \pi a^2}{2\pi a \rho_i}} = \sqrt{\frac{R_m a}{2\rho_i}}$$

This shows that the [space constant](@entry_id:193491) is proportional to the square root of the dendrite's radius ($\lambda \propto \sqrt{a}$) [@problem_id:2333473]. This has a major functional consequence: **thicker [dendrites](@entry_id:159503) propagate signals over longer distances** than thinner [dendrites](@entry_id:159503). Furthermore, any factor that increases [membrane resistance](@entry_id:174729) (e.g., blocking [leak channels](@entry_id:200192)) or decreases [axial resistance](@entry_id:177656) (e.g., higher cytoplasmic ion concentration) will lead to a larger [space constant](@entry_id:193491), allowing for more effective [signal propagation](@entry_id:165148) [@problem_id:2333470] [@problem_id:2333408].

### Functional Consequences: Dendrites as Signal Processors

The passive cable properties of [dendrites](@entry_id:159503) mean that they do not simply relay signals; they actively shape and filter them. The combination of distributed resistance and capacitance transforms the incoming synaptic currents into attenuated and temporally smeared voltage signals at the soma.

#### Linearity of the Passive Cable

A foundational concept in [passive cable theory](@entry_id:193060) is that of **linearity**. The entire model is built upon linear electrical components: resistors and capacitors whose values are constant and do not change with the voltage across them or the current through them. The current through the membrane [leak channels](@entry_id:200192) is assumed to be directly proportional to the voltage difference across the membrane (Ohm's Law), and the [capacitive current](@entry_id:272835) is directly proportional to the rate of change of the voltage. Because the component parameters $r_m$, $c_m$, and $r_a$ are assumed to be constant, the [cable equation](@entry_id:263701) that describes the voltage $V(x,t)$ is a linear [partial differential equation](@entry_id:141332) [@problem_id:2333426].

This linearity has a critical implication: the principle of superposition holds. The response to multiple inputs is simply the sum of the responses to each input individually. Another consequence is that a passive cable cannot generate new frequencies. If a purely sinusoidal current of frequency $\omega$ is injected, the resulting steady-state voltage response everywhere along the cable will also be a pure [sinusoid](@entry_id:274998) of frequency $\omega$, though its amplitude and phase will vary with position. No [harmonic distortion](@entry_id:264840) (i.e., components at $2\omega$, $3\omega$, etc.) is created. This idealized linear behavior is a defining feature of the passive model and stands in stark contrast to the highly non-linear behavior of membranes containing [voltage-gated ion channels](@entry_id:175526).

#### Dendritic Filtering: Attenuation and Delay

The most important computational function of passive dendrites is their role as **low-pass filters**. They preferentially attenuate the high-frequency components of a signal more than the low-frequency components. The biophysical reason for this lies with the [membrane capacitance](@entry_id:171929).

Consider a [synaptic current](@entry_id:198069) with both fast and slow components. The fast components (high frequencies) involve rapid changes in voltage. According to the capacitor equation $I_C = c_m \frac{dV}{dt}$, these rapid voltage changes generate large currents across the [membrane capacitance](@entry_id:171929). This capacitive pathway acts as a low-impedance "shunt" that diverts high-frequency currents out of the dendrite to the extracellular space. Slow signals, by contrast, generate very little [capacitive current](@entry_id:272835), so more of their associated charge is free to travel longitudinally down the dendrite's [axial resistance](@entry_id:177656) [@problem_id:2333449].

This low-pass filtering profoundly shapes synaptic signals as they propagate.

1.  **Amplitude Attenuation:** As a signal travels from a synapse to the soma, its amplitude decays. For transient signals like an EPSP, this attenuation is more severe for inputs located at more distal [dendrites](@entry_id:159503). An EPSP generated at a distance of one [space constant](@entry_id:193491) ($x = 1.0 \lambda$) will be much smaller upon reaching the soma than one generated proximally at $x = 0.2 \lambda$ [@problem_id:2333429].

2.  **Temporal Filtering and Delay:** The filtering process also "smears" the signal in time. As the signal propagates, it must sequentially charge the capacitance of each segment of the membrane, a process that takes time. This causes the voltage waveform to become slower to rise and fall. Consequently, the time-to-peak of an EPSP measured at the soma is longer for more distal inputs [@problem_id:2333429]. The signal not only gets smaller with distance, it also gets slower.

For a more rigorous analysis, we can consider the response to a continuous sinusoidal input. As a wave of a given frequency $\omega$ propagates down the cable, both its amplitude and phase are altered. The signal is attenuated exponentially with distance, but the [effective length](@entry_id:184361) constant is itself frequency-dependent. Higher frequency signals are attenuated more severely over the same distance. Simultaneously, the signal experiences a phase lag that increases with distance, which manifests as a time delay in the propagation of the wave's peak. Both the amplitude attenuation and the time delay can be precisely calculated from the cable's fundamental parameters, providing a quantitative description of how dendrites filter signals in both space and time [@problem_id:2333451].

In summary, the passive electrical structure of [dendrites](@entry_id:159503) makes them sophisticated computational devices. Through the interplay of [membrane resistance](@entry_id:174729), capacitance, and [axial resistance](@entry_id:177656), they filter synaptic inputs based on their location and temporal frequency content, shaping the final integrated signal that arrives at the soma to determine the neuron's output.