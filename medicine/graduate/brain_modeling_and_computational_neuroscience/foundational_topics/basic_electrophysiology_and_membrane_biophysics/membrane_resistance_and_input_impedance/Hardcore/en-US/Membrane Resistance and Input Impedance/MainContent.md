## Introduction
The ability of a neuron to process and transmit information is fundamentally rooted in its electrical properties. Key among these are [membrane resistance](@entry_id:174729) and input impedance, which dictate how a neuron responds to the barrage of synaptic currents it receives. Understanding these parameters is crucial for bridging the gap between a neuron's physical structure—its intricate morphology and the ion channels embedded in its membrane—and its ultimate computational function. This article provides a foundational framework for grasping these concepts, guiding you from basic electrical models to their complex roles in shaping [neural dynamics](@entry_id:1128578).

Across three chapters, you will build a robust understanding of these critical properties. The journey begins in **"Principles and Mechanisms"** with the foundational model of the membrane as a simple electrical circuit, expanding to cover the frequency-dependent nature of impedance and its manifestation in spatially extended dendrites. Next, **"Applications and Interdisciplinary Connections"** will demonstrate how these principles explain a wide range of neurophysiological phenomena, from [shunting inhibition](@entry_id:148905) and [dendritic integration](@entry_id:151979) to [network synchrony](@entry_id:1128547) and the technical requirements of bioinstrumentation. Finally, **"Hands-On Practices"** will allow you to solidify your knowledge by applying these concepts to solve practical problems in [cellular neuroscience](@entry_id:176725).

## Principles and Mechanisms

This chapter delves into the fundamental principles governing the passive and quasi-active electrical properties of neuronal membranes. We begin by establishing a foundational model of a small, isopotential patch of membrane as a simple electrical circuit. We will then extend this model to account for the frequency-dependent nature of membrane responses, introducing the concept of [input impedance](@entry_id:271561). Subsequently, we will explore how these properties manifest in spatially extended structures like dendrites and axons using [passive cable theory](@entry_id:193060). Finally, we will examine how voltage-dependent ion channels, even below the threshold for action potential generation, shape the membrane's impedance, giving rise to complex phenomena such as resonance.

### The Membrane as a Resistor-Capacitor (RC) Circuit

At its core, the [neuronal membrane](@entry_id:182072) separates two conductive solutions—the cytoplasm and the extracellular fluid—with a thin insulating lipid bilayer. This structure behaves electrically like a capacitor. Embedded within this bilayer are ion channels, which provide pathways for ions to cross the membrane. Collectively, these channels behave as resistors. The simplest and most powerful model for a small, isopotential patch of membrane is therefore a parallel Resistor-Capacitor (RC) circuit.

#### Membrane Resistance and Conductance

The flow of ions across the membrane at rest is primarily mediated by a diverse population of "leak" channels. For small deviations from the resting potential, the net current through these channels can be approximated by Ohm's Law. The ease with which this current flows is quantified by the **[membrane conductance](@entry_id:166663)**, denoted as $G_{\text{mem}}$. Since individual ion channels on a patch of membrane are arranged in parallel, their conductances sum. If a patch contains $N$ [leak channels](@entry_id:200192) each with a [single-channel conductance](@entry_id:197913) $g_i$, the total membrane conductance is the arithmetic sum:

$G_{\text{mem}} = \sum_{i=1}^{N} g_i$

This summation property is a direct consequence of the parallel arrangement of channels across the membrane . The unit of conductance is the siemens (S).

Conversely, the opposition to this current flow is described by the **membrane resistance**, $R_{\text{mem}}$. For a linear (ohmic) system, resistance is simply the reciprocal of conductance:

$R_{\text{mem}} = \frac{1}{G_{\text{mem}}}$

The unit of resistance is the ohm ($\Omega$). In the steady state, where voltage is constant, the relationship between a small injected current $\Delta I$ and the resulting change in membrane potential $\Delta V$ is given by Ohm's law: $\Delta V = \Delta I \cdot R_{\text{mem}}$.

It is crucial to distinguish between these **[lumped parameters](@entry_id:274932)** ($R_{\text{mem}}$, $G_{\text{mem}}$), which describe an entire patch of membrane and depend on its size, and the intrinsic properties of the membrane itself. These are captured by **specific parameters**, which are normalized by area.
*   The **[specific membrane resistance](@entry_id:166665)**, $R_m$, is the resistance of a unit area of the membrane and has units of $\Omega \cdot \text{m}^2$.
*   The **specific [membrane conductance](@entry_id:166663)**, $g_m$, is the conductance per unit area, with units of $\text{S}/\text{m}^2$.

These are related by $R_m = 1/g_m$. For a uniform membrane patch of area $A$, the lumped and specific parameters are related as follows:

$G_{\text{mem}} = g_m \cdot A$

$R_{\text{mem}} = \frac{R_m}{A}$

This inverse relationship between total resistance and area is intuitive: a larger membrane area contains more parallel ion channels, providing more pathways for current to flow and thus reducing the overall resistance of the patch .

#### Membrane Capacitance and the Time Constant

The [lipid bilayer](@entry_id:136413)'s ability to store charge is described by the **membrane capacitance**. Like resistance, it can be described by a specific, area-independent parameter and a lumped, area-dependent one.
*   The **[specific membrane capacitance](@entry_id:177788)**, $C_m$, represents the capacitance of a unit area of the membrane and is typically around $0.01 \, \text{F}/\text{m}^2$ (or $1 \, \mu\text{F}/\text{cm}^2$) for most [biological membranes](@entry_id:167298). Its units are $\text{F}/\text{m}^2$.
*   The **total [membrane capacitance](@entry_id:171929)**, $C_{\text{mem}}$, for a patch of area $A$ is given by $C_{\text{mem}} = C_m \cdot A$. The unit is the farad (F).

When a current $I(t)$ is injected into our isopotential RC circuit model, it splits into two components: a resistive current ($I_R$) flowing through the channels and a [capacitive current](@entry_id:272835) ($I_C$) that charges the membrane capacitance. By Kirchhoff's current law, $I(t) = I_R + I_C$. Substituting the constitutive relations for the resistor ($I_R = V/R_{\text{mem}}$) and capacitor ($I_C = C_{\text{mem}} \frac{dV}{dt}$), we obtain the governing differential equation for the membrane potential $V(t)$:

$C_{\text{mem}} \frac{dV}{dt} + \frac{V}{R_{\text{mem}}} = I(t)$

The solution to the homogeneous version of this equation (when $I(t)=0$) shows that the voltage relaxes exponentially to its resting state. The [characteristic time scale](@entry_id:274321) of this relaxation is the **membrane time constant**, $\tau_m$.

$\tau_m = R_{\text{mem}}C_{\text{mem}}$

The time constant is a pivotal parameter in neuroscience, as it determines how quickly a neuron's membrane potential responds to changes in input. A remarkable property of $\tau_m$ becomes evident when we express it in terms of the specific parameters :

$\tau_m = \left(\frac{R_m}{A}\right) (C_m A) = R_m C_m$

The surface area $A$ cancels out. This reveals that the [membrane time constant](@entry_id:168069) is an intrinsic property of the membrane itself, independent of the neuron's size or shape, assuming uniform membrane properties. It is determined solely by the specific resistance and specific capacitance of the membrane material. For instance, doubling the specific membrane conductance $g_m$ (which is equivalent to halving $R_m$) would halve the membrane time constant, causing the neuron to respond more quickly to inputs .

### Frequency-Dependent Response: Input Impedance

Neurons rarely receive simple, constant currents. Instead, they are bombarded with synaptic inputs that fluctuate over time. To understand how a neuron responds to such dynamic inputs, we must move beyond simple resistance and consider its frequency-dependent response, which is encapsulated by the **[input impedance](@entry_id:271561)**.

#### Defining Input Impedance

The **input impedance**, $Z_{\text{in}}(\omega)$, is the frequency-[domain generalization](@entry_id:635092) of resistance. For a sinusoidal input current with [angular frequency](@entry_id:274516) $\omega$ (where $\omega = 2\pi f$), the impedance is the complex ratio of the resulting voltage [phasor](@entry_id:273795) $V(\omega)$ to the current phasor $I(\omega)$:

$Z_{\text{in}}(\omega) = \frac{V(\omega)}{I(\omega)}$

Impedance is a complex number, comprising a magnitude $|Z_{\text{in}}(\omega)|$ and a phase $\phi(\omega)$. The magnitude represents the ratio of voltage amplitude to current amplitude at that frequency, while the phase represents the lag of the voltage response behind the current input.

For our single-compartment RC model, we can find the impedance by analyzing the governing equation in the frequency domain, where the derivative operator $\frac{d}{dt}$ becomes multiplication by $j\omega$ (with $j = \sqrt{-1}$). The current balance equation $I = V/R_{\text{mem}} + C_{\text{mem}} \frac{dV}{dt}$ becomes:

$I(\omega) = \frac{V(\omega)}{R_{\text{mem}}} + j\omega C_{\text{mem}} V(\omega) = V(\omega) \left(\frac{1}{R_{\text{mem}}} + j\omega C_{\text{mem}}\right)$

The term in the parenthesis is the **[admittance](@entry_id:266052)**, $Y(\omega)$, which is the reciprocal of impedance. Solving for the impedance $Z_{\text{in}}(\omega) = V(\omega)/I(\omega)$ gives:

$Z_{\text{in}}(\omega) = \frac{1}{\frac{1}{R_{\text{mem}}} + j\omega C_{\text{mem}}} = \frac{R_{\text{mem}}}{1 + j\omega R_{\text{mem}} C_{\text{mem}}}$

Substituting $\tau_m = R_{\text{mem}}C_{\text{mem}}$, we arrive at the canonical expression for the impedance of a passive membrane patch  :

$Z_{\text{in}}(\omega) = \frac{R_{\text{mem}}}{1 + j\omega\tau_m}$

This expression shows that the membrane acts as a **low-pass filter**. At zero frequency (DC, $\omega \to 0$), the impedance is real and equals the membrane resistance, $|Z_{\text{in}}(0)| = R_{\text{mem}}$. As frequency increases, the capacitive term in the denominator grows, causing the magnitude of the impedance to decrease. At very high frequencies ($\omega \to \infty$), the capacitor effectively short-circuits the resistor, and the impedance approaches zero. This means the membrane is much more responsive to slow inputs than to fast ones.

#### The Corner Frequency

The transition from the low-frequency pass-band to the high-frequency stop-band is characterized by the **corner frequency**, $f_c$. It is defined as the frequency at which the impedance magnitude drops to $1/\sqrt{2}$ (approximately 0.707) of its DC value. This corresponds to a power drop of one-half, or $-3$ decibels (dB) in amplitude. Setting $|\frac{Z_{\text{in}}(2\pi f_c)}{Z_{\text{in}}(0)}| = \frac{1}{\sqrt{2}}$, we find:

$\frac{1}{\sqrt{1+(2\pi f_c \tau_m)^2}} = \frac{1}{\sqrt{2}} \implies 2\pi f_c \tau_m = 1$

This gives the definition of the corner frequency :

$f_c = \frac{1}{2\pi \tau_m}$

At this specific frequency, the voltage response not only has a reduced amplitude but also lags the current input by a phase of exactly $-45^{\circ}$ (or $-\pi/4$ [radians](@entry_id:171693)). A powerful physical interpretation of the corner frequency arises from considering the admittances of the parallel components . The [admittance](@entry_id:266052) of the resistor is its conductance, $G_{\text{mem}} = 1/R_{\text{mem}}$. The [admittance](@entry_id:266052) of the capacitor is $j\omega C_{\text{mem}}$, and its magnitude is called the capacitive susceptance, $B_C = \omega C_{\text{mem}}$. The corner frequency is precisely the frequency at which the resistive conductance equals the capacitive susceptance:

$\omega_c C_{\text{mem}} = \frac{1}{R_{\text{mem}}} \implies \omega_c = \frac{1}{R_{\text{mem}}C_{\text{mem}}} = \frac{1}{\tau_m}$

This signifies the point where the current begins to flow more easily through the capacitive pathway than the resistive one.

### Spatial Integration: The Passive Cable Theory

Neurons are not simple isopotential spheres; they possess intricate dendritic and axonal structures. To understand how signals propagate and integrate within these structures, we must extend our model from a single patch to a continuous cable. This is the domain of **[passive cable theory](@entry_id:193060)**.

#### From Patches to Cables: Per-Unit-Length Parameters

We model a thin dendritic or axonal process as an idealized cylinder of radius $a$. To apply calculus, we transition from [lumped parameters](@entry_id:274932) (for a whole patch) to distributed **per-unit-length parameters**, which describe the properties of an infinitesimally thin slice of the cable of length $\Delta x$ .

*   **Axial resistance per unit length ($r_i$)**: This describes the resistance of the cytoplasm to current flowing longitudinally along the cable. For a cylinder of cross-sectional area $\pi a^2$ and cytoplasmic resistivity $R_i$ (in $\Omega \cdot \text{m}$), the resistance per unit length is $r_i = \frac{R_i}{\pi a^2}$. Its units are $\Omega/\text{m}$. Note that $r_i$ is strongly dependent on radius, scaling with $a^{-2}$.
*   **Membrane resistance per unit length ($r_m$)**: This is derived from the [specific membrane resistance](@entry_id:166665) $R_m$. The resistance of a segment of length $\Delta x$ is $R_m / (2\pi a \Delta x)$. The resistance-length product is therefore $r_m = R_m / (2\pi a)$. Its units are $\Omega \cdot \text{m}$.
*   **Membrane capacitance per unit length ($c_m$)**: This is derived from the specific capacitance $C_m$. The capacitance of a segment of length $\Delta x$ is $C_m (2\pi a \Delta x)$. The capacitance per unit length is therefore $c_m = C_m \cdot 2\pi a$. Its units are $\text{F}/\text{m}$.

#### The Space Constant and Electrotonic Length

Using these parameters, we can derive the **[passive cable equation](@entry_id:1129411)**, which governs the membrane potential $V(x,t)$ as a function of both position $x$ and time $t$. For steady-state (DC) inputs, the time derivative term vanishes, and the equation simplifies to:

$\frac{d^2 V}{d x^2} - \frac{r_i}{r_m}V = 0$

This equation introduces a fundamental parameter, the **[space constant](@entry_id:193491)** (or **[electrotonic length](@entry_id:170183)**), $\lambda$:

$\lambda = \sqrt{\frac{r_m}{r_i}}$

The solution to the steady-state cable equation for a voltage applied at one point shows that the voltage decays exponentially with distance: $V(x) = V(0) \exp(-x/\lambda)$. The [space constant](@entry_id:193491) $\lambda$ is thus the distance over which the steady-state voltage attenuates to $1/e$ (about 37%) of its value at the origin . It is the characteristic length scale for passive [signal propagation](@entry_id:165148). A larger space constant, resulting from high membrane resistance ($r_m$) and low [axial resistance](@entry_id:177656) ($r_i$), allows potentials to spread further along the cable before decaying.

#### Input Resistance and Impedance in Extended Structures

Just as we defined input impedance for a single patch, we can define it for a point on a cable. For a semi-infinite cable (a useful idealization for an electrically long dendrite), the steady-state **[input resistance](@entry_id:178645)** at the origin ($x=0$) is found to be :

$R_{\text{in}} = \sqrt{r_m r_i}$

The full frequency-dependent **[input impedance](@entry_id:271561)** for this semi-infinite cable is :

$Z_{\text{in}}(\omega) = \frac{\sqrt{r_m r_i}}{\sqrt{1 + j\omega\tau_m}}$

Comparing this to the single-compartment impedance reveals key differences. While both are low-pass filters, the cable's impedance has a different frequency dependence. At high frequencies, where $\omega\tau_m \gg 1$, the impedance magnitude of the semi-infinite cable scales as $|Z_{\text{in}}(\omega)| \sim 1/\sqrt{\omega}$, a gentler [roll-off](@entry_id:273187) than the $1/\omega$ scaling of the single compartment. The phase at high frequencies approaches $-\pi/4$ (or $-45^\circ$), not $-\pi/2$ as in the single compartment .

This analysis also shows that frequency affects the spatial spread of signals. The propagation of signals along the cable is governed by a complex, frequency-dependent [propagation constant](@entry_id:272712) $\gamma(\omega)$, where $\gamma^2 = (1+j\omega\tau_m)/\lambda^2$. The real part of $\gamma(\omega)$ determines the attenuation. As frequency $\omega$ increases, the magnitude of $\gamma(\omega)$ increases, meaning that high-frequency signals are attenuated more strongly with distance than low-frequency signals . The cable thus acts as a spatiotemporal low-pass filter.

#### The Role of Morphology: Somatic vs. Dendritic Impedance

A crucial consequence of [cable theory](@entry_id:177609) is that [input impedance](@entry_id:271561) is highly **location-dependent**. Current injected into a thin distal dendrite faces a very different electrical load than current injected into the large soma .

*   **Distal dendrites** typically have a very high [input impedance](@entry_id:271561). This is because thin dendrites have a large [axial resistance](@entry_id:177656) per unit length ($r_i \propto 1/a^2$), which dominates the local impedance.
*   The **soma**, by contrast, has a much lower [input impedance](@entry_id:271561). This is due to two factors. First, its large surface area gives it a low [membrane resistance](@entry_id:174729) ($R_{\text{mem}} \propto 1/A$). Second, and more importantly, the entire dendritic tree acts as an electrical load attached in parallel to the soma. Each dendritic branch provides an additional pathway for current to leak away. This phenomenon, often called the **somatic shunt**, means that increasing the number of dendritic branches decreases the somatic input impedance .

This impedance gradient has profound functional consequences. A given synaptic current will produce a much larger local voltage deflection in a high-impedance distal dendrite than it would in the low-impedance soma. This compartmentalization allows for localized nonlinear processing in dendrites, a key element of modern theories of neural computation.

### Beyond Passive Membranes: Active and Nonlinear Properties

While the passive model is a powerful foundation, real neurons are endowed with a rich repertoire of [voltage-gated ion channels](@entry_id:175526) that are active even at [subthreshold potentials](@entry_id:195783). These channels introduce nonlinearities and more complex dynamics into the membrane's response.

#### Input Resistance vs. Zero-Frequency Impedance

In the context of any linear system, the DC [input resistance](@entry_id:178645) $R_{\text{in}}$ is precisely equal to the zero-frequency limit of the [input impedance](@entry_id:271561) magnitude, $R_{\text{in}} = \lim_{\omega \to 0} |Z_{\text{in}}(\omega)|$. This equality holds for passive models and even for linearized models of active membranes .

However, this equivalence must be handled with care in experimental and nonlinear contexts. An experimental measurement of $R_{\text{in}}$ often uses a finite-amplitude current step. If this step moves the membrane potential into a range where voltage-gated currents are significantly recruited, the measured resistance $(\Delta V_{ss}/\Delta I)$ is the slope of a [secant line](@entry_id:178768) on the neuron's true, nonlinear steady-state I-V curve. The theoretical $R_{\text{in}}$ derived from [impedance analysis](@entry_id:1126404), however, corresponds to the slope of the tangent line at the resting potential. These values will differ for any nonlinear I-V curve . Furthermore, near a dynamical [bifurcation point](@entry_id:165821) (such as the threshold for spiking), the steady-state differential conductance of the membrane approaches zero. This causes the small-signal [input resistance](@entry_id:178645) and zero-frequency impedance to diverge to infinity, and the concept of a stable [input resistance](@entry_id:178645) becomes ill-defined .

#### The Quasi-Active Approximation

To analyze the influence of subthreshold voltage-gated channels, we can use the **quasi-active approximation**. This technique involves linearizing the dynamics of a voltage-gated channel around a steady holding potential, $V_0$. Consider a current with a [simple activation](@entry_id:1131661) variable $m$, where the channel's kinetics are described by $\tau_m(V) \frac{dm}{dt} = m_\infty(V) - m$. By linearizing this system for small voltage perturbations, we can derive the channel's contribution to the total membrane [admittance](@entry_id:266052) .

The result of this linearization is a complex, frequency-dependent [admittance](@entry_id:266052) for the active channel. This admittance consists of an instantaneous conductance term and a dynamic term that reflects the channel's [gating kinetics](@entry_id:1125527). For a typical activation current, this dynamic admittance has the form:

$Y_{\text{active}}(\omega) = \text{constant} \times \frac{1}{1 + j\omega\tau_0}$

where $\tau_0$ is the gating time constant at the holding potential $V_0$. This term is added in parallel to the passive leak and capacitive admittances to yield the total membrane admittance.

#### Amplifying and Restorative Currents: Resonance

Quasi-active currents can be classified based on the nature of the feedback they provide to voltage perturbations. The key factor is the sign of the term $(V_0 - E_x) m'_\infty(V_0)$, where $E_x$ is the channel's reversal potential and $m'_\infty(V_0)$ is the slope of its steady-state activation curve at the holding potential $V_0$ .

*   **Amplifying (Regenerative) Currents**: If this term is negative, the current provides positive feedback, amplifying voltage deviations. Persistent sodium currents are a classic example.
*   **Restorative Currents**: If this term is positive, the current provides negative feedback, opposing voltage deviations and pulling the potential back toward rest. Potassium currents like the M-current, or the [hyperpolarization](@entry_id:171603)-activated cation current ($I_h$), are examples of restorative currents.

Restorative currents have a particularly interesting effect on impedance. Their [admittance](@entry_id:266052) contributes a negative imaginary component to the total membrane [admittance](@entry_id:266052). This is the opposite of the capacitor, whose [admittance](@entry_id:266052) has a positive imaginary component. This behavior is mathematically equivalent to that of an **inductor**.

A restorative current can thus endow the membrane with an **effective inductance**. At a specific frequency, this [inductive effect](@entry_id:140883) can cancel the capacitive effect. This cancellation minimizes the total membrane [admittance](@entry_id:266052), leading to a peak in the impedance magnitude $|Z_{\text{in}}(\omega)|$. This phenomenon is known as **subthreshold resonance**. Neurons with prominent restorative currents, therefore, do not act as simple low-pass filters; instead, they are band-pass filters, responding most strongly to inputs within a preferred frequency range. This resonant property is thought to play a critical role in network oscillations and temporal processing in the brain.