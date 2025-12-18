## Introduction
Dynamic logic offers significant advantages in high-speed and area-efficient integrated circuit design, but its performance comes with a critical vulnerability. During the evaluation phase, the logic state is held on a high-impedance node, making it susceptible to noise sources that can corrupt the stored data and cause catastrophic functional failures. This article addresses the fundamental problem of maintaining [signal integrity](@entry_id:170139) on these dynamic nodes, focusing specifically on the pervasive challenges of [charge sharing](@entry_id:178714) and leakage current.

This guide provides a comprehensive exploration of the analysis and mitigation strategies essential for robust dynamic circuit design. You will gain a deep understanding of the physical phenomena that threaten data integrity and the practical engineering solutions used to counteract them. The first chapter, **Principles and Mechanisms**, will deconstruct the physics of charge sharing and leakage, introduce the keeper circuit as the primary solution, and detail the analytical methods for its proper sizing. Following this, **Applications and Interdisciplinary Connections** will demonstrate how these principles are applied in real-world scenarios, from high-performance [arithmetic circuits](@entry_id:274364) to the sophisticated algorithms used in Electronic Design Automation (EDA) tools. Finally, **Hands-On Practices** will offer a series of guided problems to solidify your understanding and build practical design skills.

## Principles and Mechanisms

In the design of dynamic [logic circuits](@entry_id:171620), the integrity of the logic state stored on the dynamic node is paramount. During the precharge phase, this node is set to a high voltage, typically $V_{DD}$, representing a default logic state. The subsequent evaluation phase determines whether this state should be maintained or discharged to ground. However, the high-impedance nature of the dynamic node during the evaluation phase makes it susceptible to various noise sources that can corrupt the stored charge, potentially leading to catastrophic logic failures. This chapter delves into the physical principles and mechanisms of these noise sources, primarily charge sharing and leakage, and explores the design of mitigation strategies, with a focus on the ubiquitous keeper circuit.

### The Challenge of Maintaining State: Noise in Dynamic Logic

Once the precharge phase ends and the pull-up transistor turns off, the dynamic node, with its total capacitance $C_D$, becomes a floating island of charge. Ideally, if the logic evaluation is false, this charge should remain indefinitely, holding the node voltage at $V_{DD}$. In reality, two primary physical mechanisms conspire to deplete this charge and cause the node voltage to "droop." Understanding the distinct nature of these two mechanisms—leakage current and [charge sharing](@entry_id:178714)—is the first step toward robust design.

#### Leakage Current

Even when transistors in the [pull-down network](@entry_id:174150) (PDN) are logically off, they are not perfect insulators. A small but persistent **leakage current**, denoted $I_{leak}$, flows through the "off" transistors. This current is a combination of several device-level phenomena, including subthreshold conduction, gate-induced drain leakage (GIDL), and junction leakage. While small, this current continuously removes charge from the dynamic node capacitance $C_D$.

Using the fundamental capacitor relationship $I = C \frac{dV}{dt}$, we can approximate the voltage droop $\Delta V_{leak}$ over an evaluation window $\Delta t$ due to a nearly constant leakage current as:
$$
\Delta V_{leak} \approx \frac{I_{leak} \Delta t}{C_D}
$$
Leakage is a slow, time-dependent degradation. For instance, with a dynamic node capacitance $C_{out} = 30\,\mathrm{fF}$ and a total leakage current of $I_{leak} = 60\,\mathrm{nA}$, the voltage droop over a $50\,\mathrm{ns}$ evaluation window would be approximately $0.10\,\mathrm{V}$ . While this may seem small, it is cumulative and can become significant in low-power designs with long hold times or high operating temperatures, which exacerbate leakage.

#### Charge Sharing

A more abrupt and often more severe noise mechanism is **charge sharing**. This phenomenon occurs when a portion of the pull-down network turns on, not to form a complete path to ground, but to connect the precharged dynamic node to one or more internal, floating nodes within the PDN. These internal nodes, typically corresponding to the source/drain diffusions between series transistors, possess parasitic capacitance ([junction capacitance](@entry_id:159302), gate-to-drain coupling, etc.). If these internal nodes were at a lower potential (e.g., $0\,\mathrm{V}$) from a previous evaluation cycle, a [charge redistribution](@entry_id:1122303) occurs upon connection.

Charge sharing is governed by the principle of **[conservation of charge](@entry_id:264158)**. Consider a dynamic node with capacitance $C_D$ precharged to $V_{DD}$, which is suddenly connected to a single internal node with capacitance $C_X$ initially at $0\,\mathrm{V}$. The total charge in this isolated two-capacitor system before connection is $Q_{initial} = C_D V_{DD} + C_X \cdot 0 = C_D V_{DD}$. After the connection, the charge redistributes until both capacitors reach a common equilibrium voltage, $V_{final}$. The final total charge is $Q_{final} = (C_D + C_X) V_{final}$. By conservation of charge, $Q_{initial} = Q_{final}$, which yields:
$$
V_{final} = V_{DD} \frac{C_D}{C_D + C_X}
$$
The voltage drop, $\Delta V_{CS} = V_{DD} - V_{final}$, is instantaneous and depends only on the ratio of the capacitances, not on time.

To illustrate the severity, consider a scenario where $C_D = 30\,\mathrm{fF}$ and a parasitic internal capacitance is $C_X = 10\,\mathrm{fF}$. If the dynamic node is at $1.0\,\mathrm{V}$ and the internal node is at $0\,\mathrm{V}$, the moment they are connected, the dynamic node's voltage will instantly drop to $V_{final} = 1.0\,\mathrm{V} \frac{30\,\mathrm{fF}}{30\,\mathrm{fF} + 10\,\mathrm{fF}} = 0.75\,\mathrm{V}$. This is a $0.25\,\mathrm{V}$ drop, which is significantly larger and faster than the $0.10\,\mathrm{V}$ droop caused by leakage in the previous example . Unlike leakage, charge sharing is an event-driven phenomenon, tied directly to the switching of transistors in the PDN.

### Analyzing the Worst-Case Scenario

To design a robust circuit, one must protect against the worst-case noise. For [charge sharing](@entry_id:178714), the worst case corresponds to the largest possible voltage droop. From the equation for $V_{final}$, the droop is maximized when the ratio of the internal capacitance to the dynamic node capacitance, $C_X / C_D$, is maximized . This occurs when an input pattern connects the largest possible amount of internal capacitance, which was previously discharged to ground, to the dynamic node.

A critical insight for modern circuit design is that this worst-case scenario is **pattern-dependent** or **history-dependent**. The initial voltage on the internal nodes is not always zero; it depends on the operations performed in the preceding clock cycles. Consider a long stack of series transistors. If the previous cycle created a full path to ground, all internal nodes in the stack would have been discharged to $0\,\mathrm{V}$. If the current cycle then partially activates this stack, a large value of $C_X$ at $0\,\mathrm{V}$ is connected to the dynamic node, leading to a severe droop. Conversely, if the previous cycle kept the stack off, many internal nodes might have been charged towards $V_{DD}$, mitigating the charge sharing effect in the current cycle.

Electronic Design Automation (EDA) tools must perform sophisticated analysis to identify the sequence of input vectors that establishes the true worst-case initial conditions for [charge sharing](@entry_id:178714). For a given evaluation pattern, the tool may enumerate all possible states of internal nodes based on previous discharge patterns ($d_{prev}$) to find the combination that results in the minimum instantaneous voltage, $V_{eq}$. This analysis reveals that the minimum voltage on the dynamic node occurs at the very beginning of the charge sharing event ($t=0^+$), as any subsequent restorative action only serves to increase the voltage .

### The Keeper Circuit: A Controlled Leakage Countermeasure

The primary defense against these noise mechanisms is the **keeper circuit**. In its most common form, it is a weak PMOS transistor with its source tied to $V_{DD}$ and its drain connected to the dynamic node. The keeper's function is to source a small current into the dynamic node, replenishing charge lost to leakage or other noise sources.

The keeper must be "weak" (i.e., have a low current-driving capability) for a crucial reason. During a valid evaluation where the PDN pulls the dynamic node to ground, the PDN must be strong enough to overpower the keeper. This creates a direct contention between the pull-up keeper and the pull-down network, a scenario that designers aim to manage carefully. A strong keeper would improve noise immunity but at a significant cost: it would slow down the evaluation, increasing the gate's propagation delay, and would increase the [short-circuit power](@entry_id:1131588) consumed during evaluation. This tension between robustness and performance is the central **keeper design trade-off** .

A more advanced implementation is the **feedback keeper**, where the keeper's gate is not tied to ground but is instead driven by the output of the static inverter that follows the dynamic node. This configuration provides a significant advantage. During the hold state, $V_D$ is high, the inverter output is low, and the PMOS keeper is on, protecting the node. During a valid evaluation, as $V_D$ is pulled low and crosses the inverter's switching threshold, the inverter's output begins to rise. This rising voltage on the keeper's gate automatically weakens and eventually turns off the keeper. This self-regulating action mitigates the contention, allowing for faster and lower-power evaluation compared to a simple, always-on keeper .

It is important to note that a keeper's primary role is to combat slow noise like leakage. Due to its weak nature, it cannot supply the massive, instantaneous current required to prevent the initial voltage drop from charge sharing. It can only help the node recover *after* the charge sharing event has occurred .

### Principles of Keeper Sizing

The efficacy of a keeper circuit is determined by its size (specifically, its channel width-to-length ratio, $W/L$). Sizing a keeper is a precise engineering task that involves balancing the aforementioned trade-offs to meet specific design constraints for robustness and performance.

#### Sizing for Leakage Immunity

The most fundamental requirement for a keeper is to prevent a false evaluation due to leakage current. A false evaluation occurs if the dynamic node voltage droops below the hold voltage, $V_{hold}$, which is typically defined as the switching threshold of the output inverter, $V_M$, plus a safety guardband, $\Delta V_g$. Let's define the total allowable voltage droop as $\Delta V_{\text{allow}} = V_{DD} - V_{hold}$,

Over an evaluation window $T_{eval}$, the total charge that the dynamic node capacitance $C_D$ can lose before the voltage drops by $\Delta V_{\text{allow}}$ is $C_D \Delta V_{\text{allow}}$. This represents the node's intrinsic charge storage budget. The total charge lost to leakage over this period is $I_{leak,max} T_{eval}$. A keeper is only needed if the charge lost to leakage exceeds the node's intrinsic budget. The keeper current, $I_k$, must therefore make up for this deficit. The charge supplied by the keeper is $I_k T_{eval}$.

Balancing the charge budget gives:
$$
\text{Charge Supplied by Keeper} + \text{Intrinsic Charge Budget} \ge \text{Charge Lost to Leakage}
$$
$$
I_k T_{eval} + C_D \Delta V_{\text{allow}} \ge I_{leak,max} T_{eval}
$$
Solving for the minimum keeper current, $I_{k,min}$, and ensuring it's non-negative, we arrive at the critical sizing formula:
$$
I_{k,min} = \max\left\{0, I_{leak,max} - \frac{C_D \Delta V_{\text{allow}}}{T_{eval}}\right\}
$$
This elegant result shows that the keeper needs to supply only the difference between the worst-case leakage current and the average current that the node capacitance can tolerate over the evaluation window. If the node capacitance is large enough to absorb the leakage on its own ($\frac{C_D \Delta V_{\text{allow}}}{T_{eval}} \ge I_{leak,max}$), no keeper is theoretically required to combat leakage .

#### Sizing for Post-Sharing Recovery

After a [charge sharing](@entry_id:178714) event causes an initial voltage drop, the keeper is responsible for restoring the node voltage. The sizing requirement here is often time-based: the voltage must recover to a certain level, $V_{target}$, within a specified recovery time, $T$. This analysis requires modeling the keeper's current-voltage characteristic.

A simple yet effective approach, especially for small voltage droops where the dynamic node voltage $V_D$ remains close to $V_{DD}$, is to model the keeper PMOS as a **linear resistor**. When $V_D$ is high, the PMOS keeper operates in its [triode region](@entry_id:276444). By linearizing its current equation for small source-drain voltages ($V_{SD} = V_{DD} - V_D$), the keeper can be modeled as a conductor with an effective conductance $G_k$. This turns the recovery process into a simple first-order RC circuit, where the capacitance $C_D$ is charged toward $V_{DD}$ through the [effective resistance](@entry_id:272328) $R_k = 1/G_k$. The voltage recovers exponentially with a time constant $\tau = R_k C_D$. By setting the target voltage and time, one can solve for the required conductance $G_k$, which in turn determines the necessary transistor width $W$ .

For larger voltage drops, a more accurate **non-linear model** using the transistor's square-law equations is necessary. If the keeper is in saturation, its current $I_k$ is proportional to $(V_{SG} - |V_{TP}|)^2$, which can be written as a function of the dynamic node voltage $V_D(t)$. This leads to a first-order [non-linear differential equation](@entry_id:163575):
$$
(C_D + C_X) \frac{dV_D}{dt} = \frac{1}{2}\mu_p C_{ox}\frac{W_k}{L_k}(V_{DD} - V_D - |V_{TP}|)^2
$$
By solving this [separable differential equation](@entry_id:169899), one can derive a closed-form analytic expression for the minimum keeper width, $W_k^{\star}$, required to recover the voltage from its post-sharing value to a target $V_{min}$ within a time $T_{eval}$ .

#### Holistic Sizing for Overall Robustness

In a real-world design, a keeper must be sized to withstand the cumulative effect of all relevant noise sources. This includes [clock feedthrough](@entry_id:170725) from the precharge transistor, multiple sequential [charge sharing](@entry_id:178714) events, and background leakage. A robust design methodology involves tracking the total charge on the dynamic node through a worst-case sequence of events. By applying [charge conservation](@entry_id:151839) at each [charge sharing](@entry_id:178714) instant and integrating the net current (keeper minus leakage) between events, one can derive an expression for the final node voltage, $V(t_{hold})$. Setting this voltage to the required specification, $V_{spec}$, allows for the calculation of the minimum keeper current, $I_{k,min}$, needed to guarantee robustness under this comprehensive noise model .

### Alternative Mitigation: Node Precharging and Design Discipline

While keeper circuits are the most common solution, other techniques exist. One direct method to eliminate charge sharing is to **precharge the internal nodes** of the PDN to $V_{DD}$ along with the main dynamic node. If all nodes start at the same potential, there is no voltage differential to drive [charge redistribution](@entry_id:1122303). This completely solves the [charge sharing](@entry_id:178714) problem . However, this solution comes at a cost. It increases the total charge that must be supplied during precharge and, more importantly, discharged during a valid evaluation. This leads to higher [dynamic power consumption](@entry_id:167414) and can increase the evaluation delay, making it a less-favored option in high-performance paths.

Finally, good design discipline is a crucial, non-circuit-based mitigation strategy. This includes careful **layout practices** to minimize the parasitic capacitances of internal diffusion nodes. It also involves ensuring a clean **clocking scheme** to prevent glitches on the inputs of dynamic gates during the precharge phase. Such glitches can partially turn on the PDN, leading to either DC contention or unintended charge sharing, jeopardizing the precharged state before evaluation even begins . Robust [dynamic logic](@entry_id:165510) design is therefore a holistic effort, combining clever circuit solutions like keepers with disciplined [physical design](@entry_id:1129644) and system-level signal integrity.