## Introduction
Rectifiers are essential components in power electronics for converting AC to DC power, but ideal models that assume instantaneous switching are insufficient for practical analysis. In reality, every AC source has an inherent impedance, primarily inductive, known as [source inductance](@entry_id:1131992). This seemingly small inductance fundamentally alters rectifier operation by preventing instantaneous current transfer, leading to a phenomenon called commutation overlap. This gap between ideal theory and practical behavior has significant consequences for system performance, including voltage regulation, power quality, and device stress.

This article provides a comprehensive exploration of commutation overlap. The first chapter, "Principles and Mechanisms," will dissect the physical origins of [source inductance](@entry_id:1131992) and derive the governing equations for the overlap process in various rectifier topologies. The second chapter, "Applications and Interdisciplinary Connections," will examine the real-world implications, from design trade-offs and regenerative braking to power factor issues and grid interaction. Finally, "Hands-On Practices" will offer practical exercises to solidify these concepts. By understanding these interactions, we can move beyond simplified models to grasp the true dynamics of line-commutated converters, starting with the fundamental principles that govern this behavior.

## Principles and Mechanisms

In the preceding introduction, we established that rectifiers are fundamental components in power electronic systems for converting AC to DC power. Our initial analyses often rely on ideal models, assuming an ideal AC voltage source and instantaneous switching. However, in any practical power system, the AC source is non-ideal and possesses a finite impedance, which is predominantly inductive. This **source inductance**, though often small, has a profound and non-negligible impact on the rectifier's operation. This chapter delves into the principles and mechanisms governing the interaction between source inductance and the [rectification](@entry_id:197363) process, a phenomenon known as **commutation overlap**.

### The Physical Origin and Quantification of Source Inductance

Before analyzing its effects, we must first understand what constitutes the source inductance, typically denoted as $L_s$. This parameter is not a discrete component but rather the lumped representation of all inductances in the AC supply path, as seen from the AC terminals of the rectifier. The primary contributors to $L_s$ are the **leakage inductance** of supply [transformers](@entry_id:270561) and the inductance of the feeders (cables and busbars) connecting the source and transformer to the rectifier.

To accurately model the system, we must determine the equivalent per-phase inductance at the rectifier's point of connection. This often involves referring inductances from the primary side of a supply transformer to the secondary side. For a transformer with a primary-to-secondary turns ratio of $n = N_p / N_s$, any inductance $L_p$ on the primary side has an equivalent inductance of $L_p / n^2$ when viewed from the secondary side.

Consider a practical scenario where a three-phase bridge rectifier is fed from a high-voltage bus through a step-down transformer . The total [source inductance](@entry_id:1131992) per phase, $L_s$, as seen by the rectifier on the secondary side, is the sum of the native secondary-side inductances and the primary-side inductances referred to the secondary.

$$L_s = L_{\text{leak},s} + L_{\text{feed},s} + \frac{L_{\text{leak},p} + L_{\text{feed},p}}{n^2}$$

Here, $L_{\text{leak},s}$ and $L_{\text{leak},p}$ are the secondary and primary leakage inductances per phase, respectively, and $L_{\text{feed},s}$ and $L_{\text{feed},p}$ are the secondary and primary feeder inductances. It is crucial to distinguish this AC-side source inductance from any filtering inductance placed on the DC side of the rectifier, as the latter does not participate in the AC-side commutation process.

### The Inevitability of Commutation Overlap

In an ideal rectifier connected to a source with zero inductance ($L_s = 0$), the transfer of current from one conducting device to the next—a process called **commutation**—would be instantaneous. Conduction would switch from the outgoing diode to the incoming diode at the very instant the source voltages make the incoming diode more forward-biased . This implies an infinite rate of change of current ($di/dt \to \infty$) in the switching devices, resulting in discontinuous, step-like phase current waveforms.

However, the presence of a finite source inductance $L_s$ makes this scenario physically impossible. The fundamental [constitutive relation](@entry_id:268485) for an inductor, described by Faraday's Law of Induction, is:

$$v_L(t) = L_s \frac{di}{dt}$$

This equation dictates that an instantaneous change in current ($dt \to 0$) would require an infinite voltage across the inductor. Since the AC source provides a finite voltage, the current through the [source inductance](@entry_id:1131992) cannot change instantaneously. This fundamental constraint is the physical reason why commutation must occur over a finite period.

This finite period, during which the current gradually transfers from the outgoing device to the incoming device, is known as the **commutation overlap** interval. During this interval, both the outgoing and incoming devices in the commutating group conduct simultaneously. This simultaneous conduction fundamentally alters the rectifier's behavior, affecting its output voltage, input current harmonics, and overall performance. The duration of this interval is quantified by the **[overlap angle](@entry_id:1129247)**, $\mu$.

### The Mechanism of Commutation

To understand and quantify the overlap angle $\mu$, we must analyze the electrical circuit during the commutation interval. The process is governed by the interplay between the source voltages and the source inductances.

#### The Commutating Voltage and Inductance

Let us consider a commutation event in a three-phase [bridge rectifier](@entry_id:1121881), where current is transferring from an outgoing phase to an incoming phase. During the overlap interval, the two corresponding [semiconductor devices](@entry_id:192345) are conducting simultaneously. For ideal devices, this creates a short-circuit path between the two commutating AC lines.

Applying Kirchhoff's Voltage Law (KVL) around this AC-side loop reveals the driving force behind commutation . The loop contains the two phase voltage sources and their respective source inductances. The KVL equation is:

$$v_{\text{in}}(t) - L_s \frac{di_{\text{in}}}{dt} = v_{\text{out}}(t) - L_s \frac{di_{\text{out}}}{dt}$$

where $v_{\text{in}}$ and $i_{\text{in}}$ are the voltage and current of the incoming phase, and $v_{\text{out}}$ and $i_{\text{out}}$ are for the outgoing phase. Rearranging this equation gives:

$$v_{\text{in}}(t) - v_{\text{out}}(t) = L_s \frac{di_{\text{in}}}{dt} - L_s \frac{di_{\text{out}}}{dt}$$

The term on the left, $v_{\text{in}}(t) - v_{\text{out}}(t)$, is the instantaneous line-to-line voltage between the two commutating phases. This is the **commutating voltage**, $v_{com}(t)$, that drives the current transfer.

Now, consider the currents. Assuming a highly inductive DC load, the total DC current $I_d$ remains constant. During overlap, this current is shared between the two conducting phases:

$$i_{\text{in}}(t) + i_{\text{out}}(t) = I_d$$

Since $I_d$ is constant, differentiating with respect to time yields $\frac{di_{\text{in}}}{dt} + \frac{di_{\text{out}}}{dt} = 0$, or $\frac{di_{\text{out}}}{dt} = -\frac{di_{\text{in}}}{dt}$. Substituting this into the KVL equation:

$$v_{com}(t) = L_s \frac{di_{\text{in}}}{dt} - L_s \left(-\frac{di_{\text{in}}}{dt}\right) = 2L_s \frac{di_{\text{in}}}{dt}$$

This is the fundamental governing equation for commutation overlap. It reveals two critical insights  :
1.  The instantaneous rate of current transfer, $\frac{di_{\text{in}}}{dt}$, is directly proportional to the instantaneous commutating voltage, $v_{com}(t)$.
2.  The effective inductance that this voltage acts across is the **commutating inductance**, $L_{com} = 2L_s$, which is the total inductance in the commutation loop.

#### The Volt-Second Balance and the Overlap Angle $\mu$

To complete the commutation, the incoming current $i_{in}$ must rise from $0$ to $I_d$. We can find the time required for this by integrating the governing equation. Rearranging and integrating over the overlap interval (from time $t_0$ to $t_0 + \Delta t$):

$$\int_{0}^{I_d} di_{\text{in}} = \int_{t_0}^{t_0+\Delta t} \frac{v_{com}(t)}{2L_s} dt$$

$$I_d = \frac{1}{2L_s} \int_{t_0}^{t_0+\Delta t} v_{com}(t) dt$$

This integral relationship expresses a profound principle: to effect a change in current of $I_d$ against a commutating inductance of $2L_s$, a specific **volt-second area** ($\int v_{com}(t) dt$) must be supplied by the commutating voltage. An instantaneous commutation ($\Delta t \to 0$) is impossible because it would require an infinite voltage impulse, reaffirming our initial reasoning from $v=L \frac{di}{dt}$ .

To find the overlap angle $\mu$, we express this relationship in terms of electrical angle $\theta = \omega t$. The integration is performed over the angular interval of overlap, which spans from the start of commutation to its completion over an angle $\mu$.

### Analysis of Specific Rectifier Topologies

While the underlying principle is universal, its application yields specific formulas for different rectifier configurations.

#### Single-Phase Full-Wave Rectifier

In a single-phase [bridge rectifier](@entry_id:1121881), commutation occurs around the zero-crossings of the AC source voltage $v_s(t) = V_m \sin(\omega t)$. At each zero-crossing, the roles of the two diode pairs reverse. During overlap, all four diodes conduct, short-circuiting the AC source through its own inductance $L_s$. The source current $i_s(t)$ must reverse completely, changing from $-I_d$ to $+I_d$. The total change in current is $\Delta i_s = 2I_d$.

The KVL equation during this interval is $v_s(t) = L_s \frac{di_s}{dt}$. Integrating over the overlap angle $\mu$, which starts at $\omega t = 0$:

$$\int_{-I_d}^{+I_d} di_s = \int_{0}^{\mu/\omega} \frac{V_m \sin(\omega t)}{L_s} dt$$

$$2I_d = \frac{V_m}{\omega L_s} \int_{0}^{\mu} \sin(\theta) d\theta = \frac{V_m}{\omega L_s} (1 - \cos\mu)$$

This provides the governing equation for a [single-phase rectifier](@entry_id:1131702) :
$$L_s (2I_d) = \frac{V_m}{\omega}(1 - \cos\mu)$$

#### Three-Phase Six-Pulse Bridge Rectifier

This is the most common polyphase rectifier. Commutation occurs every $60^\circ$ ($\pi/3$ [radians](@entry_id:171693)), as conduction passes sequentially through the six devices. During the overlap interval, exactly **three** diodes conduct simultaneously: the outgoing and incoming diodes of one group (e.g., the positive group), and the single conducting diode of the opposite group .

The commutation is driven by the line-to-line voltage. For an uncontrolled [diode rectifier](@entry_id:276300), the process begins at the **[natural commutation](@entry_id:1128434) instant**, which is the point where the line-to-line voltages corresponding to two consecutive conduction states are equal . For a commutation from phase 'c' to 'a' in the positive group, this is when $v_a = v_c$.

Let's set our angular reference $\theta=0$ at this [natural commutation](@entry_id:1128434) instant. The commutating voltage can be written as $v_{com}(\theta) = V_{LL,\text{peak}} \sin(\theta)$, where $V_{LL,\text{peak}}$ is the peak of the line-to-line voltage. Applying the [volt-second balance principle](@entry_id:1133873) with commutating inductance $2L_s$:

$$\int_{0}^{I_d} di_{\text{in}} = \frac{1}{2\omega L_s} \int_{0}^{\mu} V_{LL,\text{peak}} \sin(\theta) d\theta$$

$$I_d = \frac{V_{LL,\text{peak}}}{2\omega L_s} [-\cos\theta]_0^\mu = \frac{V_{LL,\text{peak}}}{2\omega L_s} (1 - \cos\mu)$$

This yields the classic expression for the overlap angle in a three-phase uncontrolled rectifier  :

$$\cos\mu = 1 - \frac{2\omega L_s I_d}{V_{LL,\text{peak}}}$$

This equation quantitatively shows that the [overlap angle](@entry_id:1129247) $\mu$ increases with increasing source inductance $L_s$ and load current $I_d$, and decreases with increasing line voltage magnitude $V_{LL,\text{peak}}$.

### Extensions to Advanced Converter Systems

The fundamental principles of commutation overlap extend directly to more complex and practical converter systems.

#### Controlled Rectifiers

In a controlled rectifier using thyristors (SCRs), commutation is intentionally delayed. The key timing parameters are precisely defined :
*   **Firing Angle ($\alpha$)**: This is the electrical angle of delay from the [natural commutation](@entry_id:1128434) instant to the application of the gate pulse to the incoming thyristor.
*   **Overlap Angle ($\mu$)**: This is the duration of the commutation event itself, which now begins at the angle $\alpha$. Its value still depends on $L_s$, $I_d$, and the voltage, but the integration now starts from $\alpha$. The governing equation becomes $\cos\alpha - \cos(\alpha+\mu) = \frac{2\omega L_s I_d}{V_{LL,\text{peak}}}$.
*   **Extinction Angle ($\gamma$)**: This is the angle from the end of commutation (when an outgoing thyristor's current reaches zero) until that same thyristor is again forward-biased by the AC source. It represents the time margin available for the device to turn off and regain its blocking capability. For successful operation, particularly in inverter mode, it's essential that $\gamma$ is large enough. These angles are related by $\alpha + \mu + \gamma = \pi$.

#### Twelve-Pulse Rectifiers

To reduce AC-side harmonics and DC-side ripple, high-power systems often employ multi-pulse rectifiers. A common configuration is a **12-pulse rectifier**, formed by two 6-pulse bridges fed from a transformer with two secondary windings, one Y-connected and one $\Delta$-connected. This provides two sets of three-phase voltages with a $30^\circ$ phase shift. The DC outputs are typically combined using an Interphase Transformer (IPT), which allows the two bridges to operate largely independently, each carrying half the total DC current ($I_d/2$).

A crucial point is that the commutation overlap mechanism is an **internal process** for each 6-pulse bridge . The overlap angle $\mu$ for one bridge is determined solely by its own parameters: its commutating inductance $L_s$, the current it carries ($I_d/2$), and the magnitude of its own AC line voltage. The $30^\circ$ phase displacement between the two bridges does not alter the overlap angle $\mu$ for either bridge. Its effect is to stagger the commutation instants of the two bridges, interleaving their output voltage pulses. This doubles the ripple frequency (from 6 to 12 times the line frequency) and leads to significant cancellation of lower-order harmonics, greatly improving the overall [power quality](@entry_id:1130058) of the system.