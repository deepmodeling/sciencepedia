## Introduction
In the design of modern AC-DC power supplies, achieving high power factor and low line-current distortion is no longer an option but a regulatory necessity. Among the multitude of control strategies for Power Factor Correction (PFC) preregulators, Critical Conduction Mode (CrCM), also known as Boundary Conduction Mode (BCM), stands out for its elegant simplicity and high efficiency. This method addresses the challenge of creating a resistive input characteristic without the complexity of many other control schemes. This article provides a deep dive into CrCM PFC control, guiding the reader from core theory to advanced application.

The journey begins in the **Principles and Mechanisms** chapter, where we will deconstruct the operation of a CrCM boost converter, analyzing the inductor current behavior cycle-by-cycle to derive the fundamental control laws that enable high power factor. Next, the **Applications and Interdisciplinary Connections** chapter moves from the ideal to the practical, exploring real-world design trade-offs, advanced topologies like interleaved and bridgeless converters, and the profound impact of semiconductor technology and EMC standards. Finally, **Hands-On Practices** will solidify this knowledge through targeted problems designed to reinforce key analytical skills.

We will start by examining the defining characteristics of CrCM and the mechanisms that govern its operation.

## Principles and Mechanisms

In the pursuit of high power factor and low [harmonic distortion](@entry_id:264840) in AC-DC converters, the control strategy applied to the power stage is of paramount importance. Among the various techniques, Critical Conduction Mode (CrCM) control for boost converters offers a unique combination of simplicity, efficiency, and performance. This chapter elucidates the fundamental principles and operating mechanisms of CrCM, building from the behavior of the inductor current to the system-level characteristics of the complete Power Factor Correction (PFC) preregulator.

### Defining Critical Conduction Mode

The operation of a boost converter is conventionally categorized into three modes, distinguished by the behavior of the inductor current, $i_L(t)$, over a switching cycle. In **Continuous Conduction Mode (CCM)**, the inductor current remains positive throughout the switching period ($i_L(t) > 0$), meaning it has a non-zero valley value. In **Discontinuous Conduction Mode (DCM)**, the inductor current falls to zero before the switching cycle ends, resulting in a "[dead time](@entry_id:273487)" or idle interval during which no current flows through the inductor.

**Critical Conduction Mode (CrCM)**, also widely known as **Boundary Conduction Mode (BCM)**, represents the precise operational boundary between CCM and DCM . The defining characteristic of CrCM is that the inductor current returns to exactly zero at the very instant the next switching cycle is initiated . This eliminates the idle interval found in DCM, yet it ensures that each cycle begins with the inductor current at zero, a condition shared with DCM. A key advantage of this is that the power switch turns on when the current through it is zero, a condition known as **Zero-Current Switching (ZCS)**, which significantly reduces turn-on switching losses.

### Analysis of a Single Switching Cycle

To understand the mechanics of CrCM, we analyze the trajectory of the inductor current $i_L(t)$ within a single high-frequency switching cycle. We assume that the switching frequency is much higher than the AC line frequency, allowing us to treat the rectified input voltage, $v_g(t)$, and the DC output voltage, $V_o$, as constant values ($v_g$ and $V_o$) within this brief period. The operation unfolds in two primary phases .

**Phase 1: Switch On-Time ($t_{on}$)**

The cycle begins at $t=0$ when the controller, having detected that the inductor current is zero, turns on the main power switch (e.g., a MOSFET). The inductor is now connected directly across the rectified input voltage source. The voltage across the inductor, $v_L$, is therefore equal to the input voltage:

$v_L = v_g$

According to the fundamental inductor constitutive relation, $v_L = L \frac{di_L}{dt}$, the rate of change of the inductor current is:

$\frac{di_L}{dt} = \frac{v_g}{L}$

Since $v_g$ and $L$ are considered constant within the cycle, the current slope is a positive constant. Consequently, the inductor current $i_L(t)$ increases linearly from its starting value of zero. This linear ramp continues for the duration of the on-time, $t_{on}$.

**Phase 2: Switch Off-Time ($t_{off}$)**

At the end of the on-time, the controller turns the switch off. The inductor current, which has reached its peak value $I_{pk}$, cannot change instantaneously. It is rerouted through the boost diode to the output capacitor and load. Applying Kirchhoff's Voltage Law to this new path yields the inductor voltage:

$v_L = v_g - V_o$

For a boost converter, the output voltage $V_o$ must be greater than the input voltage $v_g$. Therefore, the inductor voltage $v_L$ is a negative constant. The current slope is now:

$\frac{di_L}{dt} = \frac{v_g - V_o}{L} = -\frac{V_o - v_g}{L}$

This constant negative slope causes the inductor current to decrease linearly from its peak value $I_{pk}$. The CrCM condition dictates that the duration of this off-time, $t_{off}$, is precisely the time required for the current to fall back to zero. The moment $i_L(t)$ reaches zero, a **Zero-Current Detection (ZCD)** circuit signals the controller to begin the next cycle, initiating a new turn-on event.

Because the inductor current consists of a linear ramp-up followed by a linear ramp-down, the current waveform over a complete switching cycle is triangular  .

### Governing Equations and Control Principles

The unique behavior of CrCM gives rise to specific mathematical relationships that dictate how it can be controlled to achieve [power factor correction](@entry_id:1130033).

#### Volt-Second Balance and Timing Relationships

A fundamental principle for any inductor operating in a [periodic steady state](@entry_id:1129524) is that the net change in its current over one full cycle must be zero. In CrCM, this is explicitly enforced by the boundary conditions ($i_L$ starts and ends at zero). This implies that the volt-second product during the on-time must equal the magnitude of the volt-second product during the off-time.

$\text{Volt-seconds during } t_{on}: v_g \cdot t_{on}$

$\text{Volt-seconds during } t_{off}: (v_g - V_o) \cdot t_{off}$

For the net current change to be zero:

$v_g \cdot t_{on} + (v_g - V_o) \cdot t_{off} = 0$

Rearranging this gives the relationship between the on-time and off-time:

$t_{off}(t) = \frac{v_g(t)}{V_o - v_g(t)} t_{on}(t)$

This equation, derived directly from the CrCM condition, is a cornerstone of the mode's behavior .

#### The Challenge of Duty-Cycle Control

In many power converters, the duty cycle, $D = \frac{t_{on}}{t_{on} + t_{off}}$, is the primary control variable. However, in CrCM, this is not the case. By substituting the expression for $t_{off}$ into the definition of $D$, we find:

$D(t) = \frac{t_{on}}{t_{on} + \frac{v_g(t)}{V_o - v_g(t)} t_{on}} = \frac{1}{1 + \frac{v_g(t)}{V_o - v_g(t)}} = \frac{V_o - v_g(t)}{V_o} = 1 - \frac{v_g(t)}{V_o}$

This reveals a critical insight: in CrCM, the duty cycle is not an independent control variable. Instead, it is inherently fixed by the instantaneous voltage ratio $\frac{v_g(t)}{V_o}$. Attempting to externally impose a different duty cycle would violate the CrCM condition, forcing the converter into either CCM or DCM. Therefore, duty cycle modulation is an unsuitable control method for CrCM PFC .

#### Achieving Power Factor Correction with On-Time Modulation

The goal of PFC is to make the converter appear as a resistor to the AC line, meaning the input current should be proportional to the input voltage. The input current, averaged over a high-frequency switching cycle, $\langle i_g(t) \rangle$, is what the AC line effectively sees. For the triangular CrCM current waveform, the average value is simply half its peak:

$\langle i_g(t) \rangle = \frac{I_{pk}(t)}{2}$

The [peak current](@entry_id:264029) reached during the on-time is $I_{pk}(t) = \frac{v_g(t)}{L} t_{on}(t)$. Substituting this into the average current expression yields:

$\langle i_g(t) \rangle = \frac{v_g(t) \cdot t_{on}(t)}{2L}$

This equation illuminates a remarkably elegant control strategy. If the on-time $t_{on}$ is held constant over the AC line half-cycle, the average input current $\langle i_g(t) \rangle$ becomes directly proportional to the input voltage $v_g(t)$:

$\langle i_g(t) \rangle = \left(\frac{t_{on}}{2L}\right) v_g(t)$

This simple **constant on-time control** scheme naturally achieves a high power factor . The overall power level drawn from the line can then be regulated by an outer voltage loop that slowly adjusts the value of this "constant" $t_{on}$.

More generally, PFC controllers employ a **multiplier** within a two-loop structure. An outer voltage loop senses the DC output voltage $V_o$ and compares it to a reference, generating a slow-varying error signal. This [error signal](@entry_id:271594), which represents the required power level, is then multiplied by a signal representing the shape of the rectified line voltage, $|v_{in}(t)|$. The output of this multiplier serves as the instantaneous reference for the inner current-shaping loop. The inner loop then modulates a parameter, such as $t_{on}$, to ensure the peak (or average) inductor current tracks this reference, thus shaping the current envelope to be sinusoidal and in phase with the line voltage .

### System Characteristics and Performance Trade-offs

The choice to operate in CrCM has significant system-level implications, most notably regarding the switching frequency.

#### Inherent Variable Switching Frequency

Unlike CCM converters that typically operate at a fixed frequency, a CrCM PFC converter is inherently a **variable-frequency system**. The total switching period, $T_s(t) = t_{on} + t_{off}$, varies as the line voltage $v_g(t)$ changes. Using the previously derived relationships, we can express the switching period under constant on-time control:

$T_s(t) = t_{on} + t_{off}(t) = t_{on} + \frac{v_g(t)}{V_o - v_g(t)} t_{on} = t_{on} \left( \frac{V_o}{V_o - v_g(t)} \right)$

The instantaneous switching frequency $f_s(t) = 1/T_s(t)$ is therefore:

$f_s(t) = \frac{1}{t_{on}} \left( \frac{V_o - v_g(t)}{V_o} \right)$

This expression shows that the switching frequency is not constant but modulates over the line half-cycle .
*   Near the **line zero-crossings**, where $v_g(t) \to 0$, the frequency approaches its maximum value, $f_{s,max} \approx \frac{1}{t_{on}}$.
*   Near the **line voltage peak**, where $v_g(t)$ is at its maximum ($V_m$), the frequency reaches its minimum value, $f_{s,min} = \frac{1}{t_{on}} \frac{V_o - V_m}{V_o}$.

This wide variation in switching frequency is a defining characteristic of CrCM PFC and presents challenges for EMI [filter design](@entry_id:266363).

#### Load-Dependent Frequency Variation

The switching frequency in CrCM also depends on the output power, $P_{out}$. Higher output power requires a higher average input current. In a constant on-time system, the controller's outer loop will command a larger $t_{on}$ to increase the current and deliver more power. From the equation for $f_s(t)$, we can see that a larger $t_{on}$ leads to a lower switching frequency across the entire line cycle. A more formal derivation shows that the switching frequency is inversely proportional to the output power, $P_{out}$ .

$f_s(t) \propto \frac{1}{P_{out}}$

This means that at light loads, a CrCM PFC converter will operate at a very high frequency, which can improve efficiency due to smaller inductor size and ZCS, but at heavy loads, the frequency will decrease significantly. The range of frequency variation must be carefully considered during the design process.

#### Practical Considerations: Valley Switching

While ideal CrCM offers zero-current turn-on, practical implementations often introduce a small delay, $t_d$, after the inductor current reaches zero but before the switch is turned on again. During this delay, parasitic capacitance at the switch node resonates with the boost inductor, causing the switch-node voltage to oscillate. By timing the turn-on to coincide with a minimum of this voltage oscillation (a "valley"), it is possible to achieve Zero-Voltage Switching (ZVS) or near-ZVS, further reducing switching losses. This technique, known as **[valley switching](@entry_id:1133694)** or quasi-resonant control, slightly distorts the input current but can significantly improve efficiency, especially at high frequencies .