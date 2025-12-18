## Introduction
In modern power electronics, the relentless pursuit of higher efficiency and power density has made soft-switching techniques indispensable. Traditional hard-switched converters are fundamentally limited by switching losses, which escalate with frequency. Phase-Shifted Full-Bridge (PSFB) and Quasi-Resonant (QR) converters represent two prominent families of [soft-switching](@entry_id:1131849) topologies designed to overcome this barrier by ensuring that switches turn on or off at zero voltage or zero current. This article provides a comprehensive exploration of these advanced converters, addressing the critical question of how to design and optimize them for high-performance applications.

To build a robust understanding, we will first delve into the foundational **Principles and Mechanisms**, dissecting how phase-shift modulation controls power and how Zero-Voltage Switching (ZVS) is achieved. Next, in **Applications and Interdisciplinary Connections**, we will bridge theory with practice, examining the real-world design challenges and trade-offs involving magnetics, semiconductors, and control systems. Finally, the **Hands-On Practices** section offers practical problems to reinforce the theoretical and applied knowledge gained. This structured journey will equip you with the expertise to design and analyze state-of-the-art soft-[switching power converters](@entry_id:1132733).

## Principles and Mechanisms

This chapter delves into the fundamental principles and operational mechanisms of Phase-Shifted Full-Bridge (PSFB) and Quasi-Resonant (QR) converters. We will begin by examining how the PSFB topology modulates power through phase control, then dissect the mechanism of Zero-Voltage Switching (ZVS) that enables its high efficiency. This will lead to a [quantitative analysis](@entry_id:149547) of the conditions required to achieve and maintain ZVS. Subsequently, we will explore practical design challenges, including the loss of soft-switching at light loads and the associated trade-offs. Finally, we will introduce the distinct principles of quasi-resonant conversion and conclude with a comparative analysis of the two [soft-switching](@entry_id:1131849) families.

### Phase-Shift Modulation for Power Control

The Phase-Shifted Full-Bridge converter departs from traditional Pulse-Width Modulation (PWM) by fixing the duty cycle of the switches in each bridge leg at $50\%$. Instead of varying the on-time of the switches, power flow is controlled by adjusting the relative timing, or **phase shift**, between the two legs of the H-bridge.

Consider a full-bridge inverter fed by a DC input voltage $V_g$. The bridge consists of a "leading leg" (Leg A) and a "lagging leg" (Leg B). Each leg's midpoint voltage, $v_A(t)$ and $v_B(t)$, is a square wave that toggles between the positive and negative DC rails. In **phase-shift modulation (PSM)**, the switching actions of Leg B are delayed by a time $\Delta t$ relative to Leg A. This time delay corresponds to a phase angle $\delta = \omega_s \Delta t$, where $\omega_s$ is the switching [angular frequency](@entry_id:274516).

The voltage applied to the primary of the transformer, $v_p(t)$, is the differential voltage $v_p(t) = v_A(t) - v_B(t)$. Because the legs are phase-shifted, there are three possible voltage levels across the primary: $+V_g$, $0$, and $-V_g$.
- When Leg A is high and Leg B is low, $v_p(t) = +V_g$.
- When Leg A is low and Leg B is high, $v_p(t) = -V_g$.
- When both legs are in the same state (both high or both low), $v_p(t) = 0$.

The duration of the power-delivering intervals (when $v_p(t) \ne 0$) is directly proportional to the phase shift $\delta$. As $\delta$ increases from $0$ to $\pi$, the duration of the non-zero voltage pulses widens, transferring more energy per cycle. This method decouples the control of power flow from the turn-on and turn-off instants of individual switches, which remain fixed within their respective leg's timing sequence.

The average output voltage $V_o$ after rectification and filtering is proportional to the average of the rectified secondary voltage. By applying volt-second balance to the output filter inductor, we can derive the voltage transfer function of an ideal PSFB converter. The duration of the positive primary voltage pulse within a half-period $T_s/2$ is equal to the time delay $\Delta t$. This creates an **effective duty cycle** $D_{eff}$ for the power transfer interval.

The duration of the positive voltage pulse is $W_p(\delta) = \Delta t = \delta / \omega_s = \delta T_s / (2\pi)$. The average rectified voltage applied to the output filter is the average of two such pulses per period $T_s$. The output voltage $V_o$ is therefore:

$V_o = \frac{2 \times (W_p / T_s) \times (V_g/n)}{1} = \frac{2}{T_s} \left(\frac{\delta T_s}{2\pi}\right) \frac{V_g}{n} = \frac{V_g \delta}{n \pi}$

Here, $n$ is the primary-to-secondary turns ratio ($N_p/N_s$), and the phase angle $\delta$ is in radians, where $\delta \in [0, \pi]$. This linear relationship between phase shift and output voltage is the fundamental control law of the PSFB converter.

### The Mechanism of Zero-Voltage Switching in PSFB

The key advantage of the PSFB topology is its ability to achieve **Zero-Voltage Switching (ZVS)**, which dramatically reduces the switching losses associated with hard-switched converters. Hard switching forces a device to turn on or off while it has both significant voltage across it and current through it, leading to a momentary spike in [power dissipation](@entry_id:264815) ($p(t)=v(t)i(t)$). ZVS avoids this by ensuring the voltage across a switch is driven to zero *before* it is commanded to turn on.

This [soft-switching](@entry_id:1131849) mechanism is not inherent but is enabled by the interaction of the transformer's **leakage inductance** ($L_{lk}$) and the **output capacitances** ($C_{oss}$) of the MOSFETs. The sequence of events, particularly for the more favorably switched "leading leg," can be broken down into distinct intervals:

1.  **Power Transfer:** One diagonal pair of switches is on (e.g., S1 top-left, S4 bottom-right), and power is delivered to the load. The primary current $i_p(t)$ flows through the switches and the transformer primary.

2.  **Commutation Interval (Dead Time):** The leading-leg switch (S1) turns off. The primary current, which cannot change instantaneously due to the leakage inductance, is now diverted. Instead of flowing through S1, it flows into the switch node of Leg A, charging the output capacitance of the now-off S1 and discharging the output capacitance of the still-off S2. This process is a **resonant transition**, where energy stored in the leakage inductance is used to shuttle charge between the parasitic capacitances.

3.  **Clamping and ZVS Turn-On:** If there is sufficient energy in the inductor, the switch node voltage of Leg A will be driven all the way to the negative DC rail. At this point, the body diode of the complementary switch (S2) will forward-bias and begin to conduct the primary current. This clamps the voltage across S2 to near-zero. The controller can then turn on S2 with virtually no voltage across it, achieving ZVS.

4.  **Freewheeling Interval:** With both bottom switches (S2 and S4) now on, the primary winding is effectively short-circuited. The primary voltage is zero, and the primary current freewheels. The energy transfer to the output ceases.

The cycle proceeds with the commutation of the lagging leg and the subsequent reverse power transfer interval. The ZVS transition in the PSFB is thus a "forced" commutation, driven by the inductor current, resulting in a nearly linear, monotonic slewing of the switch-node voltage. This contrasts with the natural, sinusoidal oscillation seen in fully resonant converters. The PSFB is therefore classified as a **resonant-transition** or [quasi-resonant converter](@entry_id:1130446), as it leverages resonance only during the brief switching transitions.

### Quantitative Conditions for Zero-Voltage Switching

For ZVS to occur reliably, two fundamental conditions must be met: there must be enough energy to complete the voltage swing, and the swing must happen fast enough to finish within the allotted dead-time.

#### Energy Sufficiency Condition

The primary source of energy for the resonant transition is the kinetic energy stored in the commutation inductance, $E_L = \frac{1}{2} L_r i_p^2$. The commutation inductance $L_r$ is primarily the [transformer leakage inductance](@entry_id:1133310) $L_{lk}$, as the magnetizing inductance is effectively shorted by the rectified output during this interval. This energy must be sufficient to change the potential energy stored in the [equivalent capacitance](@entry_id:274130) of the commutating leg, $C_{eq} \approx C_{oss,top} + C_{oss,bottom}$, as its voltage swings by $V_{dc}$. The required capacitive energy is $E_C = \frac{1}{2} C_{eq} V_{dc}^2$.

The energy condition for ZVS is therefore $E_L \ge E_C$:
$$
\frac{1}{2} L_r i_p^2 \ge \frac{1}{2} C_{eq} V_{dc}^2
$$
This gives a minimum required magnitude for the primary current $i_p$ at the start of the commutation:
$$
|i_p| \ge V_{dc} \sqrt{\frac{C_{eq}}{L_r}}
$$

#### Time Sufficiency Condition

Even if there is enough energy, the transition must complete within the programmed dead-time, $t_d$. Using the fundamental capacitor relation $i_C = C \frac{dv}{dt}$, and approximating the commutating current $i_p$ as a constant [current source](@entry_id:275668) discharging $C_{eq}$, we find the time required to slew the node voltage by $V_{dc}$ is $t_{slew} = \frac{C_{eq} V_{dc}}{|i_p|}$.

For a successful transition, we must have $t_{slew} \le t_d$. This leads to a second condition on the primary current:
$$
|i_p| \ge \frac{C_{eq} V_{dc}}{t_d}
$$

#### Combined ZVS Requirement

A robust design must satisfy both the energy and time conditions. The commutating current must be large enough to meet whichever of the two bounds is more stringent. Therefore, the minimum required current for guaranteed ZVS is the maximum of these two values:
$$
|I_{\mathrm{comm,min}}| = \max \left( V_{dc} \sqrt{\frac{C_{eq}}{L_r}}, \frac{C_{eq} V_{dc}}{t_d} \right)
$$
This composite expression is a critical tool for PSFB design, linking the converter's operating voltage, component parasitics, and control timing to its ability to achieve [soft-switching](@entry_id:1131849).

### Practical Design Challenges in PSFB Converters

While elegant in principle, achieving robust ZVS in a PSFB converter across all operating conditions presents significant challenges.

#### Loss of ZVS at Light Load

The ZVS conditions are critically dependent on the primary current, which is the sum of the reflected load current and the transformer's magnetizing current. At heavy loads, the primary current is large, and ZVS is typically easy to achieve. However, at light loads, the reflected load current diminishes, and the only current available for commutation may be the magnetizing current alone. If this magnetizing current is less than $|I_{\mathrm{comm,min}}|$, the converter will lose ZVS.

When the ZVS condition $I_{\mathrm{comm}} t_d \ge V_{dc} C_{\mathrm{oss,eq}}$ is not met, the switch node voltage does not reach zero by the end of the dead-time. The switch is then forced to turn on with a non-zero **residual voltage** $V_{\mathrm{rem}}$ across it:
$$
V_{\mathrm{rem}} = V_{\mathrm{dc}} - \frac{I_{\mathrm{comm}} t_d}{C_{\mathrm{oss,eq}}}
$$
The energy stored in the output capacitance at this instant, $E_{\mathrm{on}} = \frac{1}{2} C_{\mathrm{oss,eq}} V_{\mathrm{rem}}^2$, is dissipated as heat in the MOSFET channel upon turn-on, creating a [hard-switching](@entry_id:1125911) loss. This phenomenon, known as **partial ZVS**, degrades efficiency, particularly at light loads.

#### The Circulating Current Trade-off

To maintain ZVS at light loads, designers may be forced to increase the current available for commutation. One common technique is to design the transformer with a lower [magnetizing inductance](@entry_id:1127592), which increases the magnetizing current. This extra current circulates in the primary circuit even at no load, ensuring sufficient energy for ZVS. However, this **circulating current** flows through the primary-side switches and windings for a significant portion of the cycle, incurring additional conduction losses ($P=I^2R$).

This creates a fundamental design trade-off: increasing magnetizing current reduces switching losses but increases conduction losses. There exists an optimal magnetizing current that minimizes the total loss for a given load profile. By modeling the expected switching loss (which decreases with magnetizing current) and the conduction loss (which increases with the square of magnetizing current), one can solve for the optimal bias current that maximizes overall efficiency across the operational range.

#### Non-ideal Component Effects

The simple energy calculation $E_C = \frac{1}{2} C_{eq} V_{dc}^2$ assumes a constant, voltage-independent output capacitance. In reality, the MOSFET $C_{oss}$ is highly non-linear, decreasing significantly as the drain-source voltage increases. A more accurate calculation of the energy required to discharge the capacitance involves integrating over the voltage swing:
$$
E = \int_{0}^{V_{\mathrm{dc}}} v C_{oss}(v) dv
$$
This integral often yields a lower energy requirement than the linear approximation, which can be an important consideration in precise design calculations for ZVS margin.

### Principles of Quasi-Resonant Conversion

Quasi-resonant (QR) converters represent a different family of soft-switching topologies. Unlike the PSFB, where resonance is an auxiliary mechanism confined to the dead-time, in QR converters, a resonant L-C "tank" is an integral part of the power conversion process.

The core principle of QR operation is to **time the switching events to coincide with the natural zero-crossings of voltage or current** in the resonant tank. This is fundamentally different from the [forced commutation](@entry_id:1125208) of a PSFB.

A common implementation is **valley-switching ZVS**. In this mode, after the main power transfer phase, the energy in the resonant tank elements (an inductor $L_r$ and capacitor $C_r$) causes the switch-node voltage to oscillate or "ring" in a sinusoidal fashion. The control circuit monitors this voltage and waits for it to swing to a minimum, or "valley." By turning on the switch at the bottom of this valley, near-zero voltage is achieved.

Control in QR converters is typically achieved by modulating the switching frequency. To track the resonant valleys as load and line conditions change, the controller must adjust the switch's off-time, leading to variable-frequency operation. This inherent mechanism allows QR converters to maintain ZVS down to very light loads without needing the extra circulating currents that are often a drawback in PSFB designs.

### Comparative Analysis of PSFB and QR Topologies

The choice between a PSFB and a QR topology depends heavily on the specific application requirements. Their key differences are summarized below:

| Feature | Phase-Shifted Full-Bridge (PSFB) | Quasi-Resonant (QR) |
| :--- | :--- | :--- |
| **Soft-Switching** | **ZVS**. Achieved by [forced commutation](@entry_id:1125208) using inductor energy to discharge switch capacitance during [dead-time](@entry_id:1123438). | **ZVS (Valley Switching) or ZCS**. Achieved by synchronizing switching to natural [extrema](@entry_id:271659) of a resonant tank waveform. |
| **Control Method** | **Fixed Frequency**. Power is controlled by modulating the phase shift between bridge legs. | **Variable Frequency**. Power is controlled by modulating the switching frequency to track resonant zero-crossings. |
| **Light-Load ZVS** | Challenging. Prone to losing ZVS, often requiring additional circulating current, which increases conduction loss. | Excellent. Inherently maintains ZVS over a wide load range by adjusting frequency. |
| **EMI Spectrum** | Discrete harmonics at multiples of the fixed switching frequency. Easier to filter with tuned components. | Spread-spectrum noise over a wide frequency band. Peak EMI is lower, but filtering is more complex. |
| **Typical Use Case** | High-power applications where fixed-frequency operation is required for synchronization or simplified magnetics design. | Applications prioritizing high efficiency over a wide load range, especially at light loads, where variable frequency is acceptable. |

In summary, the PSFB converter is a robust, fixed-frequency solution ideal for high-power systems, but it requires careful design to manage soft-switching at light loads. The QR converter, on the other hand, offers superior light-load performance and inherent [soft-switching](@entry_id:1131849) but at the cost of variable-frequency operation, which complicates EMI management and [filter design](@entry_id:266363). The selection between them is a classic engineering decision based on optimizing for the most critical performance metrics of the target application.