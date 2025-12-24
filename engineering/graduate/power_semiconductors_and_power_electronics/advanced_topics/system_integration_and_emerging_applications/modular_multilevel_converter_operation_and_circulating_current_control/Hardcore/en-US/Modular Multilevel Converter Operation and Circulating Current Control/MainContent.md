## Introduction
The Modular Multilevel Converter (MMC) has emerged as the leading topology for high-voltage, high-power applications, underpinning modern energy systems from HVDC transmission to large-scale renewable integration. Its [scalability](@entry_id:636611), low [harmonic distortion](@entry_id:264840), and high efficiency set it apart. However, realizing these benefits hinges on mastering the converter's complex internal dynamics. A significant challenge lies in understanding and managing the internal circulating currents—currents that do not flow to the AC terminals but have a profound impact on the converter's efficiency, component stress, and overall reliability. This article addresses this knowledge gap by providing a rigorous analysis of MMC operation and the critical role of circulating current control.

Over the next three chapters, you will embark on a comprehensive exploration of this advanced topic. The journey begins in **Principles and Mechanisms**, where we will develop the fundamental electrodynamic model of the MMC, uncover the physical origins of circulating currents and [capacitor voltage ripple](@entry_id:1122038), and introduce the core control strategies required for stable operation. Next, in **Applications and Interdisciplinary Connections**, we will see how these principles are applied in real-world systems like HVDC links and STATCOMs, and explore the system-level challenges that arise when integrating MMCs into complex grids. Finally, **Hands-On Practices** will provide the opportunity to solidify your understanding by tackling practical design and analysis problems related to arm inductance sizing and quantifying the benefits of [active control](@entry_id:924699).

## Principles and Mechanisms

This chapter delves into the core principles and operational mechanisms of the Modular Multilevel Converter (MMC). Building upon the introductory concepts, we will develop a rigorous mathematical model of the converter's behavior, explore the origins and consequences of its internal dynamic phenomena, and detail the fundamental control strategies and design considerations necessary for stable and efficient operation.

### Electrodynamic Model of the MMC Phase Leg

The fundamental building block of an MMC is the phase leg, which consists of an upper and a lower arm connecting a direct-current (DC) link to a single alternating-current (AC) phase terminal. Each arm is a complex, controllable voltage source, comprising a series connection of $N$ submodules (SMs) and an arm inductor. To analyze this system, we begin by applying Kirchhoff's Voltage Law (KVL).

Let us consider a single phase leg connected to a DC link of total voltage $V_{dc}$. It is conventional and convenient to define a virtual midpoint for the DC link, such that the positive and negative DC poles are at potentials of $+\frac{V_{dc}}{2}$ and $-\frac{V_{dc}}{2}$, respectively. Let the AC phase-node voltage be $v_p(t)$ with respect to this midpoint. The upper arm connects the positive pole to the AC node, and the lower arm connects the AC node to the negative pole. We denote the upper and lower arm currents as $i_u(t)$ and $i_l(t)$, and the series arm inductance and resistance as $L_{\text{arm}}$ and $R_{\text{arm}}$, respectively.

The stack of submodules in each arm synthesizes a controllable voltage. If we denote the number of inserted submodules in the upper and lower arms as $n_u(t)$ and $n_l(t)$, and assume all inserted submodules have an average capacitor voltage of $\bar{v}_c(t)$, the total synthesized voltages are $n_u(t)\bar{v}_c(t)$ and $n_l(t)\bar{v}_c(t)$. Applying KVL to the upper and lower arms yields two fundamental equations that govern the converter's [electrodynamics](@entry_id:158759) :

For the upper arm, traversing from the positive DC pole to the AC terminal:
$$ \frac{V_{dc}}{2} - v_{p}(t) = n_{u}(t)\bar{v}_{c}(t) + L_{\text{arm}}\frac{d i_{u}(t)}{dt} + R_{\text{arm}}i_u(t) $$

For the lower arm, traversing from the AC terminal to the negative DC pole:
$$ v_{p}(t) + \frac{V_{dc}}{2} = n_{l}(t)\bar{v}_{c}(t) + L_{\text{arm}}\frac{d i_{l}(t)}{dt} + R_{\text{arm}}i_l(t) $$

These equations describe how the arm submodule stacks, in conjunction with the arm inductors, create the voltage difference between the DC poles and the AC terminal. Summing these two equations eliminates the AC phase voltage $v_p(t)$ and reveals a crucial constraint related to the DC link voltage:
$$ V_{dc} = \left( n_{u}(t)\bar{v}_{c}(t) + n_{l}(t)\bar{v}_{c}(t) \right) + L_{\text{arm}}\frac{d}{dt}\left(i_{u}(t) + i_{l}(t)\right) + R_{\text{arm}}\left(i_{u}(t) + i_{l}(t)\right) $$
This equation shows that the sum of the synthesized arm voltages must, at every instant, equal the total DC link voltage, plus any voltage drop across the arm impedances due to the [common-mode current](@entry_id:1122687) flowing through the leg.

For analysis and control design, it is often useful to employ an **averaged model**. This technique replaces the discrete, high-frequency switching actions of the submodules with continuous variables. This is valid under the assumption that the switching frequency is much higher than the fundamental frequencies of interest, allowing us to neglect the switching ripple. The instantaneous number of inserted submodules, an integer, is replaced by a continuous **insertion index** $n(t) \in [0,1]$, representing the [duty ratio](@entry_id:199172) or desired fraction of inserted submodules. The actual number of inserted submodules, $K(t)$, is then the integer nearest to the continuous target value $N \cdot n(t)$, where $N$ is the total number of submodules per arm . The total synthesized arm voltage is then modeled as $v_{\text{arm,SM}}(t) = n(t) \cdot N \cdot \bar{v}_c(t)$.

This averaging approach simplifies the system model significantly. For instance, if we neglect the dynamic voltage drops across the arm impedances in the DC-side KVL equation (a reasonable approximation for low-frequency analysis), we obtain a key algebraic constraint :
$$ V_{dc} \approx n_{u}(t)N\bar{v}_{c}(t) + n_{l}(t)N\bar{v}_{c}(t) = (n_u(t) + n_l(t))N\bar{v}_{c}(t) $$
In normal operation, the average voltage of each submodule capacitor is regulated to be $\bar{v}_c(t) \approx V_{dc}/N$. Substituting this into the constraint implies that the sum of the insertion indices must be approximately unity:
$$ n_u(t) + n_l(t) \approx 1 $$
This is a fundamental rule for MMC modulation: the number of submodules inserted across the entire phase leg must be constant and equal to $N$ to withstand the DC voltage, but the distribution of these inserted submodules between the upper and lower arms is varied to synthesize the desired AC voltage. An alternative modeling framework using a specific set of sign conventions can also be formulated to describe this averaged behavior .

### Internal Currents and Energy Dynamics

A unique characteristic of the MMC topology is the existence of internal currents that circulate within the converter and do not appear at the AC terminals. Understanding these currents is paramount to understanding MMC operation. The upper and lower arm currents, $i_u(t)$ and $i_l(t)$, can be decomposed into two components: a differential-mode current and a [common-mode current](@entry_id:1122687).

The **differential-mode current** is what produces the AC output. It is defined as half the difference between the arm currents, but by Kirchhoff's Current Law (KCL) at the AC node, the phase current $i_a(t)$ is simply the difference:
$$ i_a(t) = i_u(t) - i_l(t) $$

The **[common-mode current](@entry_id:1122687)**, known as the **circulating current**, flows through both arms in the same direction (e.g., downwards from the DC link) and completes its path through the DC source. It is defined as the average of the arm currents:
$$ i_z(t) = \frac{1}{2}(i_u(t) + i_l(t)) $$
Using these definitions, the arm currents can be expressed as:
$$ i_u(t) = i_z(t) + \frac{i_a(t)}{2} \quad \text{and} \quad i_l(t) = i_z(t) - \frac{i_a(t)}{2} $$

The physical origin of the circulating current is a fundamental consequence of single-phase power pulsation . The [instantaneous power](@entry_id:174754) $p_a(t) = v_a(t)i_a(t)$ delivered to a single AC phase is not constant, even under balanced sinusoidal conditions. It contains a DC component (the average active power) and a component that oscillates at twice the fundamental grid frequency ($2\omega$). For instance, if $v_a(t) = \hat{V} \cos(\omega t)$ and $i_a(t) = \hat{I} \cos(\omega t - \phi)$, the [instantaneous power](@entry_id:174754) is:
$$ p_a(t) = \frac{\hat{V}\hat{I}}{2} [\cos(\phi) + \cos(2\omega t - \phi)] = P_{\text{avg}} + \tilde{p}_{a,2\omega}(t) $$

By the law of conservation of energy, this oscillating power $\tilde{p}_{a,2\omega}(t)$ must be managed within the phase leg. It is either absorbed by the submodule capacitors, causing their stored energy to fluctuate, or it is exchanged with the DC link. The power balance for the total energy stored in the phase leg capacitors, $W_{\text{leg}}$, can be expressed as:
$$ \frac{dW_{\text{leg}}}{dt} = V_{dc}i_z(t) - p_a(t) $$
This equation reveals that the power associated with the circulating current, $V_{dc}i_z(t)$, must balance the AC power $p_a(t)$ and the rate of change of stored energy. To maintain bounded [capacitor voltage ripple](@entry_id:1122038) (i.e., bounded [energy fluctuation](@entry_id:146501)), $i_z(t)$ must contain a component at $2\omega$ to counteract the $2\omega$ component in $p_a(t)$. Thus, a second-harmonic circulating current is an intrinsic and unavoidable feature of the MMC's internal physics, not necessarily a fault or non-ideality.

This exchange of oscillating power directly causes a **[capacitor voltage ripple](@entry_id:1122038)** at $2\omega$ . The power fluctuation $\tilde{p}_{a,2\omega}(t)$ is the primary driver of this ripple. If the circulating current has no AC component ($i_{z,ac}(t)=0$), the entire oscillating power must be buffered by the leg's [equivalent capacitance](@entry_id:274130), $C_{\text{eq}}$. The resulting peak amplitude of the leg voltage ripple, $\Delta \hat{V}_{\Sigma C}$, can be shown to be:
$$ \Delta \hat{V}_{\Sigma C} = \frac{VI}{2\omega C_{\text{eq}} V_{dc}} $$
where $V$ and $I$ are the RMS values of the phase voltage and current.

A more formal, [state-space](@entry_id:177074) description of these energy dynamics can be formulated by defining the total leg energy $W_{\Sigma}$ and the differential energy between the arms $W_{\Delta}$ .
$$ W_{\Sigma} = \sum_{k=1}^N \frac{1}{2} C \left(v_{u,k}^2 + v_{l,k}^2\right) \quad \text{and} \quad W_{\Delta} = \sum_{k=1}^N \frac{1}{2} C \left(v_{u,k}^2 - v_{l,k}^2\right) $$
The time derivatives of these energy states are governed by the system's electrical variables:
$$ \dot{W}_{\Sigma} = V_{dc} i_z - v_a i_a $$
$$ \dot{W}_{\Delta} = \frac{V_{dc}}{2} i_a - 2 v_a i_z $$
These equations form a powerful basis for advanced energy-based control strategies, explicitly linking the control variables ($i_z$) to the internal energy states.

### Consequences of Uncontrolled Circulating Currents

While a second-harmonic circulating current is inherent to MMC operation, if it is not properly controlled, it can have several detrimental effects on the converter's performance, efficiency, and reliability .

*   **Increased Capacitor Voltage Ripple:** The fundamental role of the circulating current is to manage the internal energy balance. An uncontrolled or improperly phased circulating current fails to cancel the AC power pulsation effectively, forcing the submodule capacitors to buffer large energy swings. This manifests as excessive voltage ripple, which stresses the capacitors and can degrade the quality of the synthesized arm voltages.

*   **Increased Semiconductor Losses:** The total current flowing through the [semiconductor devices](@entry_id:192345) in each arm is the sum of the circulating current and the AC phase current component ($i_u = i_z + i_a/2$). An uncontrolled circulating current increases the RMS value of the total arm current, leading to higher conduction losses ($I^2R$) in the switches and diodes. It can also increase the peak current that needs to be switched, thereby increasing switching losses. This reduction in efficiency is a primary reason for actively controlling the circulating current.

*   **DC-Link Stress:** The circulating current of each phase leg is drawn from the DC link. If the uncontrolled circulating current has a zero-sequence nature (i.e., it is identical in all three phases), the total ripple current on the DC bus will be the sum of the contributions from all three phases. For a $2\omega$ zero-sequence circulating current, this results in a significant $2\omega$ current ripple on the DC link, which can stress the DC source or any DC-link capacitors.

*   **Asymmetrical Operation due to Parameter Mismatches:** In a real-world converter, small mismatches in component values are inevitable. If the arm inductances ($L_p$) or submodule capacitances ($C_p$) differ from phase to phase, the same internal driving voltage will produce different circulating current amplitudes and phase shifts in each leg. This asymmetry leads to unbalanced capacitor voltage ripples and uneven thermal stress distribution across the converter phases, potentially compromising long-term reliability .

### Principles of Circulating Current Control and Voltage Balancing

Given the adverse effects of uncontrolled circulating currents, their active management is a cornerstone of MMC control. The strategy involves two key aspects: high-level control of the circulating current itself and low-level balancing of individual submodule capacitor voltages.

The primary objective of **Circulating Current Suppression Control (CCSC)** is to shape the $2\omega$ component of the circulating current to actively cancel the $2\omega$ AC power pulsation within each phase leg . Instead of letting the capacitors buffer this energy, the controller forces the leg to draw a pulsating power from the DC link that is equal in magnitude and opposite in phase to the AC-side pulsation. This is achieved by injecting a specific second-harmonic circulating current. The ideal reference for this current component, $i_{z,2\omega}(t)$, can be derived from the power balance equation $V_{dc} i_{z,2\omega}(t) = - \tilde{p}_{a,2\omega}(t)$, which yields:
$$ i_{z,2\omega}(t) = -\frac{\hat{V}\hat{I}}{2 V_{dc}} \cos(2\omega t - \phi) $$
Injecting this current minimizes the power that needs to be absorbed by the capacitors, thus suppressing the dominant $2\omega$ [voltage ripple](@entry_id:1133886) . For instance, a control scheme that injects a circulating current to cancel a fraction $\alpha$ of the power pulsation will reduce the corresponding [voltage ripple](@entry_id:1133886) by a factor of $(1-\alpha)$. A secondary objective is to minimize losses by ensuring the circulating current contains only the necessary DC and $2\omega$ components, with no other extraneous harmonics.

While CCSC manages the aggregate energy of the arm, **capacitor voltage balancing** ensures that this energy is evenly distributed among all submodules within the arm. This is a low-level control action that operates at the switching frequency. A widely used and effective method is **Nearest Voltage Sorting (NVS)** . This algorithm's logic is elegantly simple and is based on directing the energy flow to counteract voltage deviations:

1.  At each control step, the capacitor voltages of all $N$ submodules in the arm are measured and sorted in ascending order.
2.  The required integer number of submodules to insert, $K(t)$, is determined from the arm's insertion index reference.
3.  The direction of the arm current, $i_{\text{arm}}(t)$, is checked.
4.  If $i_{\text{arm}}(t) > 0$ (charging current), the controller inserts the $K(t)$ submodules with the *lowest* voltages. This action charges the most discharged capacitors, pushing their voltages up towards the average.
5.  If $i_{\text{arm}}(t)  0$ (discharging current), the controller inserts the $K(t)$ submodules with the *highest* voltages. This action discharges the most overcharged capacitors, pulling their voltages down towards the average.

By consistently applying this logic, the NVS algorithm actively forces the capacitor voltages to cluster tightly around their mean value, ensuring stable operation and validating the assumptions of the averaged model used for higher-level control.

### The Role of Arm Inductors: A Design Trade-Off

The arm inductor, $L_a$, is a critical passive component whose size is determined by a series of important engineering trade-offs . While it may seem like a simple element, its inductance value profoundly impacts the converter's performance, safety, and cost.

A larger arm inductance offers several key benefits:

*   **Fault Current Limitation:** In the event of a DC-side short-circuit through a phase leg, the arm inductors are the primary elements limiting the rate of rise of the fault current. The initial rate of rise is approximately $di/dt \approx V_{dc}/(2L_a)$. A larger $L_a$ slows this rise, providing crucial time for protection systems (like circuit breakers) to operate before the current reaches destructive levels.
*   **Ripple Attenuation:** The inductors act as a low-pass filter. They provide high impedance to the high-frequency voltage steps generated by submodule switching, thereby attenuating the resulting high-frequency current ripple in the arms.
*   **Passive Circulating Current Suppression:** The inductor presents an impedance of $2\omega L_a$ to the second-harmonic circulating current. A larger inductance passively helps to reduce the magnitude of this current for a given internal disturbance voltage.

However, a larger inductance also comes with significant drawbacks:

*   **Slower Dynamic Response:** The inductor limits the rate at which the arm current can be changed by the controller, resulting in a slower dynamic response for the AC output current control loop.
*   **Increased Reactive Voltage Drop:** Driving a sinusoidal current through the inductor requires a reactive voltage drop of $\omega L_a I_a$, which must be supplied by the submodules. A larger inductor consumes more of the available modulation voltage range, potentially limiting the converter's operating envelope.
*   **Physical Size, Cost, and Losses:** Larger inductors are physically bigger, heavier, and more expensive. They also have higher winding resistance, contributing to converter losses and reducing overall efficiency.

The selection of the arm inductance is therefore a classic optimization problem, balancing the need for [fault tolerance](@entry_id:142190) and low ripple against the requirements for fast dynamics, high efficiency, and low cost.