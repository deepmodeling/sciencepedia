## Introduction
In the world of high-performance analog and mixed-signal integrated circuits, the assumption of a clean, stable power supply is a luxury rarely afforded. Unwanted noise, ripple, and transient fluctuations on power supply rails can couple into sensitive signal paths, degrading critical performance metrics from signal-to-noise ratio to timing accuracy. The ability of a circuit to reject these pervasive disturbances is a crucial figure of merit known as Power Supply Rejection (PSR). A thorough understanding of PSR is not merely academic; it is essential for designing robust and reliable electronic systems.

This article provides a comprehensive exploration of Power Supply Rejection, addressing the knowledge gap between basic definitions and advanced, real-world design challenges. We will dissect the problem of supply noise from first principles up to system-level implications. The reader will learn how to analyze, quantify, and ultimately design for high PSR. The journey is structured across three key chapters. First, "Principles and Mechanisms" establishes the formal mathematical framework for PSRR and investigates the fundamental physical mechanisms of noise coupling. Next, "Applications and Interdisciplinary Connections" demonstrates how these principles are applied in the design and analysis of real-world circuits and systems, from op-amps to data converters. Finally, "Hands-On Practices" solidifies this theoretical knowledge through targeted exercises that address common design challenges.

By progressing through these chapters, you will gain the expertise to analyze, diagnose, and design analog circuits with robust immunity to power supply noise, a critical skill for any modern IC designer. We begin by delving into the core principles that govern this essential characteristic.

## Principles and Mechanisms

This chapter delves into the fundamental principles and physical mechanisms that govern the sensitivity of [analog circuits](@entry_id:274672) to variations in their power supply. We will establish a rigorous mathematical framework for quantifying [power supply rejection](@entry_id:1130064) and then explore the specific circuit-level and system-level phenomena that determine its performance.

### Formalism of Power Supply Rejection

The performance of an analog circuit is predicated on the stability of its operating point, which is established by its direct-current (DC) power supplies. However, these supply voltages are rarely ideal. They are subject to noise, ripple, and transient fluctuations originating from the regulator, [digital logic](@entry_id:178743) sharing the same supply rail, or external interference. The ability of an analog block to maintain its intended output behavior in the presence of such supply disturbances is a critical figure of merit.

#### The Supply-to-Output Transfer Function

The most fundamental way to characterize a circuit's sensitivity to supply noise is through a **small-signal transfer function**. We consider a small, time-varying perturbation, or ripple, $v_s(t)$, superimposed on a nominal DC supply voltage $V_{S0}$. This ripple will propagate through the circuit and manifest as an unwanted perturbation, $v_{\text{out}}(t)$, at the output node. For small enough perturbations, the circuit's response can be accurately described by a linear, time-invariant (LTI) system.

The relationship between the [supply ripple](@entry_id:271017) and the output perturbation is formally captured by the **supply-to-output transfer function**, denoted as $H_{V_{s}\to V_{\text{out}}}(j\omega)$. This is a complex function of angular frequency $\omega$ defined as the ratio of the output voltage [phasor](@entry_id:273795) to the supply voltage phasor, under the condition that all other independent signal inputs are set to their small-signal zero values (e.g., voltage inputs are shorted to ground). 

$$
H_{V_{s}\to V_{\text{out}}}(j\omega) \triangleq \frac{V_{\text{out}}(j\omega)}{V_{s}(j\omega)}
$$

Here, $V_{s}(j\omega)$ and $V_{\text{out}}(j\omega)$ are the [phasors](@entry_id:270266) of the small-signal ripple $v_{s}(t)$ and the resulting small-signal output variation $v_{\text{out}}(t)$, respectively. The input port is the supply pin, driven by an ideal voltage source representing the ripple, and the output port is the circuit's output node, both referenced to the circuit's ground. The transfer function's magnitude, $|H_{V_{s}\to V_{\text{out}}}(j\omega)|$, quantifies the gain from the supply to the output at a given frequency, while its phase, $\angle H_{V_{s}\to V_{\text{out}}}(j\omega)$, describes the phase shift. A smaller magnitude implies better noise immunity.

#### PSRR and Related Metrics

While the transfer function is the most complete description, several related metrics are used in practice for convenience.

The most common of these is the **Power Supply Rejection Ratio (PSRR)**. It is defined as the reciprocal of the magnitude of the supply-to-output transfer function. A high PSRR signifies that a large [supply ripple](@entry_id:271017) results in only a small output disturbance.

$$
\text{PSRR}(\omega) \triangleq \frac{1}{|H_{V_{s}\to V_{\text{out}}}(j\omega)|} = \left| \frac{V_{s}(j\omega)}{V_{\text{out}}(j\omega)} \right|
$$

PSRR is a dimensionless quantity and is almost universally expressed in decibels (dB):

$$
\text{PSRR}_{\text{dB}} = 20 \log_{10}(\text{PSRR}(\omega)) = -20 \log_{10}(|H_{V_{s}\to V_{\text{out}}}(j\omega)|)
$$

Two other related terms are important to distinguish :

*   **Line Regulation**: This is a DC metric that quantifies the change in the DC output voltage for a change in the DC supply voltage. It is formally the DC limit of the supply-to-output transfer function magnitude, often expressed in units of $\text{mV/V}$ or as a percentage.
    $$
    \text{Line Regulation} \triangleq \left. \frac{d V_{\text{out,DC}}}{d V_{s,\text{DC}}} \right| = |H_{V_{s}\to V_{\text{out}}}(0)|
    $$

*   **Power-Supply Modulation Ratio (PSMR)**: This metric quantifies the sensitivity of a specific circuit *parameter* $p$ (such as gain, offset voltage, or oscillation frequency) to supply variations. It is defined as the [normalized sensitivity](@entry_id:1128895) of the parameter to the supply voltage, with units of $1/\text{V}$ (often reported as $\%/\text{V}$).
    $$
    \text{PSMR}_{p} \triangleq \frac{1}{p} \frac{\partial p}{\partial V_{s}}
    $$

### Physical Coupling Mechanisms

To design circuits with high PSRR, it is essential to understand the physical mechanisms through which supply noise couples to the output. These mechanisms can be broadly categorized into low-frequency and high-frequency paths.

#### Low-Frequency Coupling Paths

At low frequencies, where capacitive effects are negligible, supply noise propagates through resistive paths and the active behavior of transistors. Consider a canonical [common-source amplifier](@entry_id:265648), a fundamental building block.

A simple model involves a transistor with finite output resistance $r_o$ and a resistive load $R_D$ connected to the supply rail $V_{DD}$. If the transistor's gate is held at an AC ground, its transconductance does not contribute to the output ripple. The [supply ripple](@entry_id:271017) $v_{DD}$ is applied to the output node through the load resistor $R_D$. The output node is connected to ground through the transistor's output resistance $r_o$. The resulting small-signal circuit is a simple voltage divider.  The transfer function is:

$$
H_{V_{DD}\to V_{\text{out}}}(0) = \frac{v_{\text{out}}}{v_{DD}} = \frac{r_o}{R_D + r_o}
$$

This demonstrates the most direct coupling path: through the load impedance. To improve PSRR, one must either decrease $r_o$ or increase $R_D$. Using an [active load](@entry_id:262691), such as a [current source](@entry_id:275668), dramatically increases the effective $R_D$ and thus improves PSRR from this path.

However, a more complete analysis reveals other, more subtle paths. Supply ripple does not only affect the load; it can also affect the biasing of the amplifying transistor itself.  Let's consider a common-source stage where the gate and bulk bias networks are derived from the same noisy supply, $V_{DD}$. A fraction of the [supply ripple](@entry_id:271017) may couple to the gate ($\tilde{v}_g = \alpha_g \tilde{V}_{DD}$) and the bulk ($\tilde{v}_b = \alpha_b \tilde{V}_{DD}$). These voltage variations modulate the drain current through the transconductance ($g_m$) and body-effect transconductance ($g_{mb}$), respectively. Applying Kirchhoff's Current Law (KCL) at the output node, considering the currents through the load $R_D$, the transistor's output resistance $r_o$, and the transistor's controlled current source, yields a more comprehensive transfer function:

$$
H_{V_{DD}\to V_{\text{out}}}(0) = \frac{r_{o} - (g_{m} \alpha_{g} + g_{mb} \alpha_{b}) R_{D} r_{o}}{R_{D} + r_{o}} = \frac{r_o}{R_D + r_o} - (g_m \alpha_g + g_{mb} \alpha_b) (R_D \parallel r_o)
$$

This expression elegantly combines all low-frequency mechanisms. The first term represents the passive voltage divider path through the load, as derived before. The second term represents the active paths, where supply noise is converted into a current signal by $g_m$ and $g_{mb}$, which then develops a voltage across the parallel combination of the load and output resistances ($R_D \parallel r_o$). Notably, the active path often contributes with a negative sign, potentially leading to cancellation and a "notch" (very high PSRR) at DC if terms are balanced, or it can degrade PSRR if it adds constructively.

#### High-Frequency Coupling Paths

As frequency increases, parasitic capacitances become the dominant pathways for noise coupling. At a high-impedance node, such as the output of a common-source stage with an [active load](@entry_id:262691), even small capacitances can provide significant feedthrough.

Consider a high-impedance output node loaded by a total capacitance to ground $C_L$. Suppose the [active load](@entry_id:262691) is a PMOS transistor whose source and bulk are tied to the noisy supply $V_{DD}$. The [gate-to-drain capacitance](@entry_id:1125509) ($C_{gd}$) and drain-to-bulk capacitance ($C_{db}$) of this load transistor connect the output node directly to the $V_{DD}$ rail. 

At high frequencies, the circuit acts as a **capacitive voltage divider**. The [supply ripple](@entry_id:271017) $V_{dd}(j\omega)$ is applied across a series combination of capacitors: the total capacitance from the supply rail to the output node ($C_{supply} = C_{gd} + C_{db}$) and the capacitance from the output node to ground ($C_L$). The output ripple $V_x(j\omega)$ is the voltage across $C_L$. The transfer function is ratiometric and, in this simplified model, independent of frequency:

$$
H_{V_{DD}\to x}(j\omega) = \frac{V_{x}(j\omega)}{V_{dd}(j\omega)} = \frac{C_{gd} + C_{db}}{C_{gd} + C_{db} + C_{L}}
$$

This result is critical: it shows that at high frequencies, the PSRR is determined by a ratio of parasitic capacitances. To improve high-frequency PSRR, one must minimize the direct coupling capacitance from the supply to the output ($C_{gd}$, $C_{db}$) and/or maximize the capacitance from the output to ground ($C_L$). This is a fundamental trade-off, as increasing $C_L$ reduces the circuit's bandwidth.

### Power Supply Rejection in Differential Circuits

Differential signaling is a cornerstone of high-performance analog design, largely due to its inherent ability to reject common-mode noise, including [supply ripple](@entry_id:271017).

The principle is based on symmetry. Consider a perfectly symmetric differential pair, where both halves are identical. When a [supply ripple](@entry_id:271017) is applied, it acts as a common-mode excitation. Due to the perfect symmetry of the circuit, this symmetric excitation produces an identical, symmetric response at the two differential outputs, $v_{o1}(t)$ and $v_{o2}(t)$.  That is, the disturbance is purely common-mode ($v_{o1}(t) = v_{o2}(t)$). The differential output signal, which is the quantity of interest, is the difference $v_{od}(t) = v_{o1}(t) - v_{o2}(t)$. Since the two output ripples are identical, they cancel perfectly, and the differential output remains clean.

$$
v_{od}(t) = v_{o1}(t) - v_{o2}(t) = 0 \quad (\text{for a perfectly symmetric circuit})
$$

This leads to an ideally infinite **differential PSRR**. In practice, any asymmetry or mismatch between the two halves of the circuit will disrupt this perfect cancellation, leading to a finite but still very high PSRR.

For a [fully differential amplifier](@entry_id:268611) (FDA), we formalize this by defining two distinct PSRR metrics :
*   **Common-Mode PSRR ($PSRR_{cm}$)**: Measures the rejection of supply noise appearing at the common-mode output $v_{out,cm} = (v_{out+} + v_{out-})/2$.
    $$
    PSRR_{cm} = \left| \frac{\tilde{V}_{s,cm}(\omega)}{\tilde{V}_{out,cm}(\omega)} \right|
    $$
*   **Differential PSRR ($PSRR_{dm}$)**: Measures the rejection of supply noise appearing at the differential output $v_{out,dm} = v_{out+} - v_{out-}$. This is typically the more important metric as it quantifies noise corrupting the signal path.
    $$
    PSRR_{dm} = \left| \frac{\tilde{V}_{s,cm}(\omega)}{\tilde{V}_{out,dm}(\omega)} \right|
    $$
Here, $\tilde{V}_{s,cm}$ is the common-mode [supply ripple](@entry_id:271017) that excites the circuit. The high performance of differential circuits stems from their ability to achieve a very large $PSRR_{dm}$.

### The Impact of Asymmetry and Non-Idealities

The ideal performance described above is limited by various non-idealities in real-world circuits. Asymmetries, whether structural or random, are the primary culprits in degrading PSRR.

#### Structural Asymmetry in PSRR

Many circuits, even if internally differential, have single-ended output stages or are inherently asymmetric with respect to their positive ($V_{DD}$) and negative ($V_{SS}$) supply rails. This leads to a significant difference in the rejection of noise from each rail, i.e., $PSRR_+ \neq PSRR_-$.

A classic example is a CMOS [operational amplifier](@entry_id:263966) output stage consisting of an NMOS common-source pulldown transistor and a PMOS cascode [current source](@entry_id:275668) pull-up.  The small-signal impedance looking from the output node down to the $V_{SS}$ rail, $r_n$, is simply the output resistance of the NMOS device, $r_{o1}$. The impedance looking up to the $V_{DD}$ rail, $r_p$, is the much larger [output impedance](@entry_id:265563) of the cascode structure, which is approximately $g_{m3}r_{o3}r_{o2}$.

The output node acts as a voltage divider between these two impedances.
*   For noise on $V_{DD}$ (with $V_{SS}$ quiet), the transfer function is $H_+ = r_n / (r_p + r_n)$. The PSRR is $PSRR_+ = (r_p + r_n) / r_n = 1 + r_p/r_n$.
*   For noise on $V_{SS}$ (with $V_{DD}$ quiet), the transfer function is $H_- = r_p / (r_p + r_n)$. The PSRR is $PSRR_- = (r_p + r_n) / r_p = 1 + r_n/r_p$.

The **PSRR asymmetry metric**, $\mathcal{A} \equiv PSRR_+ / PSRR_-$, is therefore:
$$
\mathcal{A} = \frac{1 + r_p/r_n}{1 + r_n/r_p} = \frac{r_p}{r_n}
$$
Since the cascode impedance $r_p$ is designed to be much larger than the common-source impedance $r_n$, the circuit will be significantly more effective at rejecting noise from the positive supply ($V_{DD}$) than from the negative supply ($V_{SS}$). For typical parameters, this asymmetry $\mathcal{A}$ can be in the hundreds.

#### Statistical Effects of Random Mismatch

Even in circuits designed for perfect symmetry, such as a differential pair, unavoidable random variations in the manufacturing process lead to small mismatches between corresponding devices. These mismatches in parameters like threshold voltage ($V_T$), transconductance factor ($\beta$), and output resistance ($r_o$) break the perfect symmetry and degrade the differential PSRR.

This effect is statistical in nature. While a single chip might have a specific PSRR, the PSRR will vary from chip to chip. We can analyze the variance of the supply-to-output transfer function, $\text{Var}\{H_{V_{s}\to V_{out}}\}$, to quantify this degradation.

Consider a simple CMOS inverter acting as an amplifier, with supply-to-output transfer function $H = r_{o\text{N}} / (r_{o\text{N}} + r_{o\text{P}})$. Using [first-order perturbation theory](@entry_id:153242), the variance of $H$ can be related to the variances of the underlying output resistances, which in turn depend on mismatches in fundamental device parameters governed by Pelgrom's law.  The final expression for the variance of $H$ reveals its dependency on both device sizing and operating point:

$$
\operatorname{Var}\!\{H\} \approx \frac{r_{o\text{N}}^{2} r_{o\text{P}}^{2}}{(r_{o\text{N}} + r_{o\text{P}})^{4}} \left[ \frac{\operatorname{Var}\{r_{o\text{N}}\}}{r_{o\text{N}}^2} + \frac{\operatorname{Var}\{r_{o\text{P}}\}}{r_{o\text{P}}^2} \right]
$$

where each term for the relative variance of the output resistance, for a device $X \in \{\text{N, P}\}$, is given by:

$$
\frac{\operatorname{Var}\{r_{oX}\}}{r_{oX}^2} = \frac{1}{W_X L_X} \left( A_{\beta X}^2 + A_{\lambda X}^2 + \frac{4 A_{V_T X}^2}{V_{OVX}^2} \right)
$$

This advanced analysis shows that the variance of the transfer function, and thus the degradation of PSRR due to mismatch, is inversely proportional to the device area ($W \times L$) and highly dependent on the overdrive voltage ($V_{OV}$). Larger devices and higher overdrive voltages lead to better matching and more predictable, higher PSRR.

### System-Level Interaction with the Power Distribution Network

The PSRR of an isolated circuit block is only half the story. The actual noise seen at the supply pins of the block is shaped by the entire **Power Distribution Network (PDN)**, from the voltage regulator to the chip.

A simplified but highly effective model for the PDN consists of the regulator's output resistance ($R_s$), the series inductance of the package and board traces ($L_s$), and the on-chip decoupling capacitance ($C$). This forms a series RLC circuit. 

This RLC network has a characteristic resonant frequency. The condition for [series resonance](@entry_id:268839) is when the inductive and capacitive reactances cancel, leaving only the resistance $R_s$ to limit the current. This occurs at an [angular frequency](@entry_id:274516) $\omega_0$:

$$
\omega_0 L_s - \frac{1}{\omega_0 C} = 0 \implies \omega_0 = \frac{1}{\sqrt{L_s C}}
$$

The [resonant frequency](@entry_id:265742) in Hertz is therefore:

$$
f_0 = \frac{1}{2\pi \sqrt{L_s C}}
$$

At this frequency, the impedance of the PDN is at a minimum. This allows the maximum amount of current from a remote noise source to flow, which in turn develops the largest possible [voltage ripple](@entry_id:1133886) across the on-chip capacitor $C$. This phenomenon is known as **resonant peaking**. The transfer function from the remote regulator noise ($V_s$) to the on-chip supply voltage ($V_{DD}$) exhibits a sharp peak at $f_0$.

This has a profound impact on the overall system's immunity to supply noise. Even if an analog block has a high intrinsic PSRR, if there is a large noise peak on its supply pin at $f_0$, the output noise can still be substantial. This effect manifests as a sharp **dip** in the system's end-to-end PSRR (measured from the regulator to the circuit output) at the PDN resonant frequency. Careful design of the PDN, including the selection of decoupling capacitors and the control of parasitic inductance, is therefore as critical as the circuit-level design for achieving robust [power supply rejection](@entry_id:1130064) in a complete system.