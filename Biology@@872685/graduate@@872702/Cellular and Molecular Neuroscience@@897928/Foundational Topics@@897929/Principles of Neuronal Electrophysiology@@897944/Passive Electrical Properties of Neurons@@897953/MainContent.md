## Introduction
The ability of the nervous system to process information relies on the intricate electrical signaling of its [fundamental units](@entry_id:148878), the neurons. While the all-or-none action potential is the most famous of these signals, it is built upon a more fundamental substrate: the passive electrical properties of the neuron. These properties dictate how a neuron responds to subthreshold inputs, how signals from thousands of synapses are integrated, and how far and fast electrical currents spread through complex dendritic and axonal structures. Understanding this passive behavior is the first and most critical step in deciphering the computational language of the brain.

This article addresses the foundational question of how neuronal voltage changes in space and time in the absence of active, voltage-gated conductances. It provides a systematic framework for modeling the neuron as a passive electrical device. Across three chapters, you will gain a deep, quantitative understanding of this topic. The first chapter, **"Principles and Mechanisms,"** deconstructs the neuron into its core electrical components—resistors and capacitors—to derive the fundamental parameters of the [time constant](@entry_id:267377) and [space constant](@entry_id:193491). The second chapter, **"Applications and Interdisciplinary Connections,"** explores how these principles explain critical biological phenomena such as [synaptic integration](@entry_id:149097), [shunting inhibition](@entry_id:148905), and [saltatory conduction](@entry_id:136479), connecting them to fields like experimental neuroscience and bioenergetics. Finally, the **"Hands-On Practices"** section provides practical problems to solidify your understanding by applying these models to realistic scenarios. By the end, you will appreciate how the passive properties of a neuron are not a static background but a dynamic and essential element of [neural computation](@entry_id:154058).

## Principles and Mechanisms

The passive electrical properties of neurons form the fundamental substrate upon which all electrical signaling, from [synaptic integration](@entry_id:149097) to [action potential propagation](@entry_id:154135), is built. These properties govern how a neuron responds to currents in the absence of voltage-gated channel activity, dictating the spread and filtering of signals in both time and space. Understanding these principles is essential for comprehending the computational capabilities of single neurons. This chapter systematically deconstructs the passive neuron, beginning with its most basic representation as an electrical circuit and building towards a comprehensive model of its [spatiotemporal dynamics](@entry_id:201628).

### The Basic Model: The Passive Membrane as an RC Circuit

At its core, the [neuronal membrane](@entry_id:182072) can be modeled as a simple electrical circuit consisting of a resistor and a capacitor arranged in parallel. This is known as the **RC circuit model**. The [lipid bilayer](@entry_id:136413), being a thin insulator separating two conductive solutions (the cytoplasm and the extracellular fluid), acts as a **capacitor**. It stores [electrical charge](@entry_id:274596). Simultaneously, [ion channels](@entry_id:144262) that are open at rest provide pathways for ions to flow across the membrane, acting as **resistors**. These are typically non-gated "leak" channels.

#### Specific versus Total Membrane Properties

To describe these electrical properties in a way that is independent of a neuron's particular size or shape, we use **specific** or intensive parameters, which are normalized to a unit area of the membrane.

The **[specific membrane capacitance](@entry_id:177788)**, denoted $c_m$, is the capacitance per unit area of the membrane. For virtually all [biological membranes](@entry_id:167298), its value is remarkably constant, approximately $c_m \approx 1 \, \mu\mathrm{F/cm}^2$. This uniformity arises because the thickness of the [lipid bilayer](@entry_id:136413) is highly conserved across cell types.

The **[specific membrane resistance](@entry_id:166665)**, denoted $R_m$, represents the resistance of a unit area of membrane to [ionic current](@entry_id:175879) flow. Its units are typically $\Omega \cdot \mathrm{cm}^2$. Unlike $c_m$, the value of $R_m$ varies widely among different types of neurons (from $10^3$ to $10^5 \, \Omega \cdot \mathrm{cm}^2$), as it is determined by the density and type of resting ion channels embedded in the membrane. A high $R_m$ signifies a "tighter" or less leaky membrane, while a low $R_m$ signifies a leakier one.

To obtain the **total** or extrinsic parameters for a neuron or a piece of membrane with a given surface area $A$, we must consider how these elements combine. The entire membrane can be envisioned as a vast number of small, identical patches connected in parallel.
- For [capacitors in parallel](@entry_id:266592), the total capacitance is the sum of individual capacitances. Therefore, the **total capacitance** $C$ is directly proportional to the area: $C = c_m A$. [@problem_id:2737144]
- For resistors in parallel, it is their conductances (the reciprocal of resistance, $G = 1/R$) that add. The specific [membrane conductance](@entry_id:166663) is $g_m = 1/R_m$. The total conductance $G$ is thus $G = g_m A$. Consequently, the **total resistance** $R$ is inversely proportional to the area: $R = 1/G = 1/(g_m A) = R_m/A$. [@problem_id:2737144]

This inverse relationship is a crucial concept: a larger neuron, having more membrane area, possesses more [leak channels](@entry_id:200192) in total, providing more pathways for current to escape. It therefore has a lower total [input resistance](@entry_id:178645) than a smaller neuron with the same intrinsic membrane properties.

#### The Leak Reversal Potential and the Linear Current Model

The resistive pathway is not merely a simple resistor connected to ground. The flow of ions through [leak channels](@entry_id:200192) is driven by both the [electrical potential](@entry_id:272157) difference across the membrane, $V_m$, and the chemical concentration gradients of the permeable ions. This is modeled by including an ideal battery, representing an [electromotive force](@entry_id:203175), in series with the leak resistance. The voltage of this battery is the **leak [reversal potential](@entry_id:177450)**, $E_L$.

The leak reversal potential is the membrane potential at which the net flow of all [ionic currents](@entry_id:170309) through the passive [leak channels](@entry_id:200192) is zero. At $V_m = E_L$, the outward electrical forces on positive ions are perfectly balanced by the net inward chemical (diffusional) forces, and vice-versa. $E_L$ is an intensive property determined by the relative permeabilities and concentration gradients of the principal ions involved (usually K$^+$, Na$^+$, and Cl$^-$), as described by the Goldman-Hodgkin-Katz (GHK) equation. In the absence of any other currents, the neuron's membrane potential will settle at $E_L$, which is thus equivalent to the **resting membrane potential**. [@problem_id:2737114]

The current flowing through this leak pathway, $I_L$, is described by Ohm's Law, with the driving potential being the difference between the membrane potential $V_m$ and the reversal potential $E_L$:
$$I_L = G (V_m - E_L) = \frac{V_m - E_L}{R}$$
where $G = 1/R$ is the total leak conductance.

It is important to recognize that this linear relationship is an approximation. The true current-voltage relationship for [ion channels](@entry_id:144262), as described by the GHK current equation, is nonlinear. However, for small voltage perturbations around the reversal potential, we can perform a first-order Taylor series expansion of the total leak current $I_L(V_m)$ around $V_m = E_L$. Since $I_L(E_L) = 0$ by definition, the expansion simplifies to $I_L(V_m) \approx (V_m - E_L) \cdot \frac{dI_L}{dV_m}\Big|_{V_m=E_L}$. This justifies the linear model, where the slope conductance $g_L$ is identified as the derivative of the I-V curve at the [reversal potential](@entry_id:177450). [@problem_id:2737161]

### Temporal Dynamics of the Passive Membrane

The parallel combination of the capacitor and the resistive leak pathway dictates how the neuron's voltage changes over time in response to an injected current, $I_{inj}$. By Kirchhoff's Current Law, the injected current must split between the capacitive path ($I_C$) and the resistive path ($I_L$):
$$I_{inj} = I_C + I_L$$
Substituting the expressions for each current, $I_C = C \frac{dV_m}{dt}$ and $I_L = \frac{V_m - E_L}{R}$, we arrive at the governing first-order linear ordinary differential equation for a single, isopotential compartment:
$$C \frac{dV_m}{dt} + \frac{V_m - E_L}{R} = I_{inj}(t)$$

#### The Membrane Time Constant

This equation can be rewritten in a standard form by defining the **[membrane time constant](@entry_id:168069)**, $\tau_m = R C$:
$$\tau_m \frac{dV_m}{dt} + (V_m - E_L) = R \cdot I_{inj}(t)$$
The time constant $\tau_m$ is a fundamental parameter that characterizes the response speed of the passive membrane. If a constant current step is applied, $\tau_m$ is the time it takes for the [membrane potential](@entry_id:150996) to change by approximately $63\%$ (i.e., $1 - 1/e$) of its final, steady-state value. A longer time constant implies a slower response.

Crucially, the [membrane time constant](@entry_id:168069) is independent of the neuron's size and geometry, provided the specific properties $R_m$ and $c_m$ are uniform. This can be seen by substituting the area-dependent expressions for $R$ and $C$:
$$\tau_m = R \cdot C = \left(\frac{R_m}{A}\right) \cdot (c_m A) = R_m c_m$$
For example, a neuron with $R_m = 2.5 \times 10^4 \, \Omega \cdot \mathrm{cm}^2$ and $c_m = 1.0 \, \mu\mathrm{F/cm}^2$ will have a time constant of $\tau_m = (2.5 \times 10^4) \cdot (1.0 \times 10^{-6}) = 25 \, \mathrm{ms}$, regardless of its surface area. [@problem_id:2737114] [@problem_id:2737144]

#### The Membrane as a Low-Pass Filter

The [time constant](@entry_id:267377) reveals the membrane's behavior in the time domain. In the frequency domain, it manifests as a filtering property. When a neuron is driven by time-varying or oscillatory inputs, such as those arising from synaptic activity, the passive membrane acts as a **low-pass filter**.

To see this, we analyze the circuit's **[complex impedance](@entry_id:273113)**, $Z(\omega)$, which is the frequency-dependent ratio of voltage to current, $Z(\omega) = V(\omega)/I(\omega)$. For the parallel RC circuit, the total [admittance](@entry_id:266052) $Y(\omega)$ (reciprocal of impedance) is the sum of the admittances of the conductor ($G$) and the capacitor ($i\omega C$):
$$Y(\omega) = G + i\omega C$$
The impedance is therefore:
$$Z(\omega) = \frac{1}{Y(\omega)} = \frac{1}{G + i\omega C}$$
The magnitude of the impedance, or the gain, is $|Z(\omega)| = 1 / \sqrt{G^2 + (\omega C)^2}$. At zero frequency (DC, $\omega=0$), the gain is maximal, $|Z(0)| = 1/G = R$. As the frequency $\omega$ increases, the term $(\omega C)^2$ grows, causing the denominator to increase and the overall gain $|Z(\omega)|$ to decrease, approaching zero as $\omega \to \infty$. This is the definition of a low-pass filter: it "passes" low-frequency signals while attenuating high-frequency signals. [@problem_id:2737088]

The **corner frequency**, $\omega_c$, is the frequency at which the signal power is attenuated by half (the voltage gain drops to $1/\sqrt{2}$ of its DC value). For the passive membrane, this occurs when the resistive and capacitive admittances are equal in magnitude, which yields:
$$\omega_c = \frac{G}{C} = \frac{1}{RC} = \frac{1}{\tau_m}$$
The phase of the impedance, $\phi(\omega) = -\arctan(\omega C/G) = -\arctan(\omega \tau_m)$, is negative, indicating that for [sinusoidal inputs](@entry_id:269486), the voltage response lags behind the current input. This lag approaches $-90^\circ$ ($-\pi/2$ [radians](@entry_id:171693)) at very high frequencies. Functionally, this low-pass filtering means that the passive membrane tends to smooth out rapid voltage fluctuations, integrating synaptic inputs over the timescale of its [time constant](@entry_id:267377).

### Spatial Dynamics: The Passive Cable

Neurons are not simple spheres; they have complex, extended geometries like dendrites and axons. This spatial dimension introduces a new critical element: the propagation of signals along these structures. To analyze this, we model [dendrites](@entry_id:159503) and unmyelinated axons as **passive cables**.

#### Axial versus Membrane Resistance

In a spatially extended cable, current does not only flow across the membrane (radially), but also along the length of the cable (axially) through the cytoplasm. This introduces a second key resistive property.

1.  **Membrane Resistance:** As before, this describes the resistance to current flowing *across* the membrane. For a cable, we often use the **membrane resistance per unit length**, $r_m$, with units of $\Omega \cdot \mathrm{m}$. It is related to the [specific membrane resistance](@entry_id:166665) $R_m$ and the cable's circumference ($2\pi a$, for a cylinder of radius $a$) by $r_m = R_m / (2\pi a)$.

2.  **Axial Resistance:** This describes the resistance of the cytoplasm to current flowing *along* the longitudinal axis of the cable. It is determined by the **intracellular [resistivity](@entry_id:266481)** (or axial resistivity), $\rho_i$, an [intrinsic property](@entry_id:273674) of the cytoplasm with units of $\Omega \cdot \mathrm{m}$. The **[axial resistance](@entry_id:177656) per unit length**, $r_a$, with units of $\Omega/\mathrm{m}$, is given by $r_a = \rho_i / A_{cross}$, where $A_{cross} = \pi a^2$ is the cross-sectional area of the cable.

It is vital to distinguish these two resistances: $r_m$ governs how much current leaks out of the cable, while $r_a$ governs how easily current flows down the cable. [@problem_id:2737159]

#### The Space Constant

The interplay between these two resistances determines how far a voltage signal can passively spread. In steady state (after capacitive currents have ceased), a local depolarization will decay with distance from its point of origin. This decay is governed by the **steady-state [cable equation](@entry_id:263701)**:
$$\lambda^2 \frac{d^2V(x)}{dx^2} - V(x) = 0$$
where $V(x)$ is the deviation from resting potential at position $x$. The parameter $\lambda$ is the **[space constant](@entry_id:193491)** (or [length constant](@entry_id:153012)), defined as:
$$\lambda = \sqrt{\frac{r_m}{r_a}}$$
The [space constant](@entry_id:193491) has units of length and represents the characteristic distance over which a steady-state voltage signal decays to $1/e$ (approximately $37\%$) of its initial value. A large [space constant](@entry_id:193491) allows signals to propagate over long distances with minimal loss, while a small [space constant](@entry_id:193491) causes signals to decay rapidly.

By substituting the expressions for $r_m$ and $r_a$ in terms of intrinsic properties and geometry, we find:
$$\lambda = \sqrt{\frac{R_m / (2\pi a)}{\rho_i / (\pi a^2)}} = \sqrt{\frac{R_m a}{2\rho_i}}$$
This crucial relationship shows that $\lambda$ increases with the square root of the [specific membrane resistance](@entry_id:166665) ($R_m$) and the radius ($a$), and decreases with the square root of the axial [resistivity](@entry_id:266481) ($\rho_i$). A thicker dendrite or a less leaky membrane promotes the long-distance spread of signals. In contrast, the [membrane time constant](@entry_id:168069) $\tau_m = R_m c_m$ is a purely local property, independent of both axial resistivity and geometry. [@problem_id:2737159]

#### Electrotonic Length

To provide a universal, dimensionless measure of distance in a neuronal cable, we define the **[electrotonic length](@entry_id:170183)**, $L$, as the ratio of the physical length of a cable segment, $\ell$, to its [space constant](@entry_id:193491), $\lambda$:
$$L = \frac{\ell}{\lambda}$$
An [electrotonic length](@entry_id:170183) of $L=1$ means that the physical length of the dendrite is exactly one [space constant](@entry_id:193491). A dendrite with $L \ll 1$ is considered "electrotonically compact," meaning a signal can spread from one end to the other with little attenuation. A dendrite with $L \gg 1$ is "electrotonically extensive," and signals will be severely attenuated as they propagate. For a signal propagating from a distal site towards the soma, the degree of steady-state voltage attenuation is approximately proportional to $\exp(-L)$. Thus, [electrotonic length](@entry_id:170183) is the primary determinant of **dendrite-to-soma coupling** for steady-state inputs: a smaller $L$ implies stronger coupling. [@problem_id:2737142]

### Applications and Consequences of Passive Properties

The principles of [passive cable theory](@entry_id:193060) have profound implications for neuronal function, from [synaptic integration](@entry_id:149097) to the speed of [neural communication](@entry_id:170397).

#### Synaptic Integration and Dendritic Load

When a dendrite is attached to a soma, it acts as an additional pathway for current to flow away from the soma. This is known as **dendritic load**. Consider a simplified "ball-and-stick" neuron, with a soma connected to a long (modeled as semi-infinite) dendrite. An injected current at the soma can either leak out through the somatic membrane (conductance $G_s$) or flow into the dendrite. The dendrite itself presents an effective input conductance to the soma. For a semi-infinite cable, this input conductance can be shown to be $G_{in,dendrite} = 1/\sqrt{r_a r_m}$.

Because the somatic leak and the dendritic input are in parallel, their conductances add. The total input conductance of the neuron is $G_{in,total} = G_s + G_{in,dendrite}$. The total [input resistance](@entry_id:178645) is therefore:
$$R_{in,total} = \frac{1}{G_s + G_{in,dendrite}} = \frac{1}{G_s + 1/\sqrt{r_a r_m}}$$
This is always less than the resistance of the isolated soma, $1/G_s$. The presence of the dendritic tree thus lowers the neuron's overall input resistance and, by Ohm's Law ($V = IR$), reduces the voltage response at the soma for a given [synaptic current](@entry_id:198069). [@problem_id:2737172]

#### Frequency-Dependent Filtering in Dendrites

The dendritic cable does not just attenuate signals; it filters them in a frequency-dependent manner. The combination of the distributed [membrane capacitance](@entry_id:171929) and the [axial resistance](@entry_id:177656) forms a distributed [low-pass filter](@entry_id:145200). High-frequency components of a signal are shunted out through the [membrane capacitance](@entry_id:171929) more effectively than low-frequency components.

This effect becomes more pronounced with distance. Consider a proximal synaptic input versus a distal one. For a high-frequency input current, the low impedance of the local dendritic capacitance provides an easy escape path. For a distal input, this effect is compounded along the entire path to the soma. As a result, the fraction of current from a dendritic input that successfully reaches the soma decreases with both frequency and distance. This means the soma's response is inherently biased toward low-frequency and/or proximal inputs. At high frequencies, the dendritic tree effectively compartmentalizes signals, making distal inputs far less effective at influencing somatic voltage than proximal ones. [@problem_id:2737108]

#### Myelination and Saltatory Conduction

Perhaps the most dramatic biological application of passive properties is **[myelination](@entry_id:137192)**. In [myelinated axons](@entry_id:149971), [glial cells](@entry_id:139163) (Schwann cells or [oligodendrocytes](@entry_id:155497)) wrap the axon in many layers of membrane, forming an insulating myelin sheath. This sheath is interrupted at regular intervals by the unmyelinated Nodes of Ranvier.

The myelin sheath profoundly alters the passive cable properties of the internodal axon segments:
1.  **Capacitance decreases:** The multiple layers of membrane act as [capacitors in series](@entry_id:262454). The total capacitance of $N$ layers is $C_{total} = C_{single}/N$. Thus, [myelination](@entry_id:137192) dramatically *decreases* the [specific membrane capacitance](@entry_id:177788) $c_m$.
2.  **Resistance increases:** The layers act as resistors in series, and the density of [leak channels](@entry_id:200192) in the internodal axolemma is very low. Both factors cause a massive *increase* in the [specific membrane resistance](@entry_id:166665) $R_m$.

Let's examine the consequences for $\lambda$ and $\tau_m$. Using realistic parameters where [myelination](@entry_id:137192) increases $R_m$ by a factor of 100 (e.g., from $1\,\mathrm{k}\Omega\cdot\mathrm{cm}^2$ to $100\,\mathrm{k}\Omega\cdot\mathrm{cm}^2$) and decreases $c_m$ by a factor of 200 (e.g., from $1.0\,\mu\mathrm{F/cm}^2$ to $0.005\,\mu\mathrm{F/cm}^2$):
-   The **[space constant](@entry_id:193491)**, $\lambda \propto \sqrt{R_m}$, increases by a factor of $\sqrt{100} = 10$.
-   The **[time constant](@entry_id:267377)**, $\tau_m = R_m c_m$, changes by a factor of $100 / 200 = 0.5$, i.e., it is halved.

The huge increase in the [space constant](@entry_id:193491) is the key to **[saltatory conduction](@entry_id:136479)**. It allows the passive, electrotonic current generated by an action potential at one node to spread with very little decay down the long internodal segment. In conjunction with the reduced [time constant](@entry_id:267377) (which allows for faster charging of the membrane), this current quickly brings the next node to threshold. This passive "jump" is much faster than the process of sequentially regenerating action potentials along an [unmyelinated axon](@entry_id:172364). [@problem_id:2737145]

### The Formal Framework: Linearity and Time-Invariance

The powerful analytical tools used in this chapter, such as impedance analysis and the superposition of solutions, rely on the assumption that the underlying system is **Linear and Time-Invariant (LTI)**. It is crucial to understand the conditions under which this assumption holds for a neuron.

A system is **linear** if its response to a sum of inputs is the sum of its responses to each individual input. For the passive [cable equation](@entry_id:263701), this requires that all coefficients of the voltage $V$ and its derivatives be independent of $V$. This condition is met if membrane conductances are constant ("ohmic") but is violated by the presence of [voltage-gated ion channels](@entry_id:175526), whose conductance $g(V)$ is a function of membrane potential. [@problem_id:2737141]

A system is **time-invariant** if its response to a time-shifted input is simply the original response, but also time-shifted. This requires that all coefficients and parameters in the governing equation (like $c_m, R_m, \rho_i, E_L$) do not change over time. This assumption holds for a purely passive cable with a stable internal and external environment. However, it can be violated. For instance, a synaptic input modeled as a time-varying conductance, $g_s(t)$, makes the system time-varying, even if it remains linear. Similarly, slow drifts in ion concentrations that alter reversal potentials, $E_L(t)$, would also render the system time-variant. [@problem_id:2737141]

Therefore, the passive models discussed here provide a powerful and accurate framework for understanding subthreshold neuronal behavior, but one must remain mindful of their limitations in the face of the nonlinear, time-varying conductances that define active [neuronal signaling](@entry_id:176759).