## Introduction
While an ideal [differential amplifier](@entry_id:272747) perfectly rejects signals common to both its inputs, real-world circuits exhibit an unwanted response known as common-mode gain. This non-ideality is a fundamental challenge in [analog circuit design](@entry_id:270580), as it allows noise and interference to corrupt sensitive measurements and high-speed data. This article addresses the crucial need to understand and control this phenomenon. Across the following sections, you will learn the core principles governing common-mode gain and its measurement via the Common-Mode Rejection Ratio (CMRR). We will explore its significant impact across diverse applications, from biomedical sensors to [integrated circuits](@entry_id:265543), and conclude with hands-on practice problems to solidify your analytical skills. This comprehensive journey begins with an in-depth look at the principles and mechanisms that define and create common-mode gain in differential amplifiers.

## Principles and Mechanisms

Following our introduction to the [differential amplifier](@entry_id:272747), we now delve into the principles and mechanisms that govern its non-ideal behavior. An ideal [differential amplifier](@entry_id:272747) would respond only to the difference between its two input signals. In practice, however, all differential amplifiers exhibit some response to the component of the input signal that is common to both inputs. This chapter will define, analyze, and characterize this response, known as the **common-mode gain**. Understanding and minimizing this gain is a central objective in high-performance [analog circuit design](@entry_id:270580).

### Characterizing Common-Mode Amplification

The behavior of a [differential amplifier](@entry_id:272747) can be described by a linear model that relates the output voltage, $v_o$, to both the differential and common-mode components of the input. Any pair of input signals, $v_1$ and $v_2$, can be decomposed into a **differential-mode input voltage**, $v_d$, and a **common-mode input voltage**, $v_{cm}$:

$$
v_d = v_1 - v_2
$$

$$
v_{cm} = \frac{v_1 + v_2}{2}
$$

The output voltage of the amplifier is then a linear superposition of the amplified versions of these two components:

$$
v_o = A_d v_d + A_{cm} v_{cm}
$$

Here, $A_d$ is the desired **[differential-mode gain](@entry_id:264461)**, and $A_{cm}$ is the undesired **common-mode gain** [@problem_id:1293088]. For an amplifier with fully differential outputs, $v_{o1}$ and $v_{o2}$, the common-mode gain is typically defined with respect to the common-mode output voltage, $v_{ocm} = (v_{o1} + v_{o2})/2$, such that $A_{cm} = v_{ocm} / v_{cm}$. In the case of a single-ended output, $v_o$ is simply the voltage at one of the output terminals.

The primary goal of a [differential amplifier](@entry_id:272747) is to amplify $v_d$ while completely ignoring $v_{cm}$. Therefore, in an ideal [differential amplifier](@entry_id:272747), the **common-mode gain is zero**. The quality of a real amplifier is measured by how close it comes to this ideal. This quality is quantified by the **Common-Mode Rejection Ratio (CMRR)**, which is the ratio of the [differential-mode gain](@entry_id:264461) to the common-mode gain:

$$
\text{CMRR} = \left| \frac{A_d}{A_{cm}} \right|
$$

A larger CMRR indicates superior performance. For convenience, CMRR is almost always expressed in decibels (dB):

$$
\text{CMRR}_{\text{dB}} = 20 \log_{10} \left| \frac{A_d}{A_{cm}} \right| = 20 \log_{10}(\text{CMRR})
$$

To appreciate the practical importance of a high CMRR, consider a scenario where an [instrumentation amplifier](@entry_id:265976) is used to measure a small differential signal from a sensor, such as a [thermocouple](@entry_id:160397) or a strain gauge. The long wires connecting the sensor to the amplifier can act as antennas, picking up ubiquitous electromagnetic interference, like 50/60 Hz hum from power lines. This noise appears as an identical voltage on both input lines—a pure [common-mode signal](@entry_id:264851). The amplifier must amplify the tiny differential sensor signal while rejecting the large, unwanted [common-mode noise](@entry_id:269684).

**Example Application:**
Suppose an amplifier with a [differential gain](@entry_id:264006) $A_d = 500$ and a CMRR of $80 \text{ dB}$ receives a desired differential signal of amplitude $V_d = 2.0 \text{ mV}$ superimposed with a [common-mode noise](@entry_id:269684) of amplitude $V_{cm} = 100.0 \text{ mV}$. We can determine the ratio of the desired signal to the undesired noise at the output. First, we find the magnitude of the common-mode gain from the CMRR [@problem_id:1293139]:
$$
80 = 20 \log_{10} \left| \frac{500}{A_{cm}} \right| \implies \left| \frac{500}{A_{cm}} \right| = 10^{4} \implies |A_{cm}| = \frac{500}{10000} = 0.05
$$
The amplitude of the desired signal component at the output is $|A_d| |V_d| = 500 \times (2.0 \times 10^{-3} \text{ V}) = 1.0 \text{ V}$.
The amplitude of the noise component at the output is $|A_{cm}| |V_{cm}| = 0.05 \times (100.0 \times 10^{-3} \text{ V}) = 0.005 \text{ V}$.
The ratio of the desired signal to noise at the output is thus $1.0 / 0.005 = 200$. Even though the input noise was 50 times larger than the input signal, the amplifier's high CMRR ensures the output signal is 200 times larger than the output noise, demonstrating the power of [common-mode rejection](@entry_id:265391).

### Analysis of Common-Mode Gain in Symmetric Differential Pairs

To understand how to design amplifiers with low common-mode gain, we must first derive an analytical expression for it. Let's analyze a symmetric [differential pair](@entry_id:266000), first using N-channel MOSFETs (NMOS) and then Bipolar Junction Transistors (BJTs).

Consider a MOS differential pair with identical transistors M1 and M2, identical load resistors $R_D$, and a tail resistor $R_{SS}$ connecting their common source node to ground. We apply a small-signal [common-mode voltage](@entry_id:267734) $v_{icm}$ to the gates of both M1 and M2. We assume the transistors are in saturation and neglect their intrinsic output resistance $r_o$ for now.

When $v_{icm}$ is applied, the symmetry of the circuit dictates that the small-signal behavior of both halves is identical. Let $v_s$ be the small-signal voltage at the common source node. The gate-source voltage for each transistor is $v_{gs} = v_{icm} - v_s$. The drain current in each transistor is $i_d = g_m v_{gs} = g_m(v_{icm} - v_s)$.

The total current from both transistors flows through the tail resistor $R_{SS}$. Applying Kirchhoff's Current Law (KCL) at the source node:
$$
i_{d1} + i_{d2} = \frac{v_s}{R_{SS}} \implies 2 g_m (v_{icm} - v_s) = \frac{v_s}{R_{SS}}
$$
This equation reveals a key insight: the tail resistor $R_{SS}$ provides [negative feedback](@entry_id:138619). An increase in $v_{icm}$ tends to increase the drain currents, which in turn raises the voltage $v_s$. This rise in $v_s$ reduces the gate-source voltage $v_{gs}$, counteracting the initial increase in current. This feedback mechanism is what suppresses the common-mode response.

Solving for $v_s$ gives:
$$
v_s = \frac{2 g_m R_{SS}}{1 + 2 g_m R_{SS}} v_{icm}
$$
The single-ended output voltage, taken at the drain of M2, is $v_o = -i_{d2} R_D$. The drain current is:
$$
i_{d2} = g_m(v_{icm} - v_s) = g_m \left( v_{icm} - \frac{2 g_m R_{SS}}{1 + 2 g_m R_{SS}} v_{icm} \right) = \frac{g_m}{1 + 2 g_m R_{SS}} v_{icm}
$$
Therefore, the single-ended common-mode gain is:
$$
A_{cm} = \frac{v_o}{v_{icm}} = - \frac{g_m R_D}{1 + 2 g_m R_{SS}}
$$
This fundamental result appears in many analyses [@problem_id:1293090] [@problem_id:1293070]. An identical derivation for a BJT differential pair yields a structurally identical result, where $R_D$ is replaced by the collector resistor $R_C$ and $R_{SS}$ is replaced by the [output resistance](@entry_id:276800) of the [tail current source](@entry_id:262705), $R_o$ [@problem_id:1293120].

#### The Role of Tail Impedance

The expression for $A_{cm}$ leads to the most important conclusion in the design for high CMRR: to minimize $|A_{cm}|$, the denominator must be maximized. This means the product $g_m R_{SS}$ must be as large as possible. Since $g_m$ and $R_D$ also determine the [differential gain](@entry_id:264006), the most effective and independent parameter to adjust for minimizing $A_{cm}$ is the **tail resistance $R_{SS}$** [@problem_id:1293128].

If we could use an [ideal current source](@entry_id:272249) to bias the tail, it would have an infinite output resistance ($R_{SS} \to \infty$). In this theoretical limit:
$$
\lim_{R_{SS} \to \infty} A_{cm} = \lim_{R_{SS} \to \infty} - \frac{g_m R_D}{1 + 2 g_m R_{SS}} = 0
$$
This confirms our intuition: an ideal differential pair biased with an [ideal current source](@entry_id:272249) has zero common-mode gain and therefore infinite CMRR [@problem_id:1293094]. In practice, designers use sophisticated current source circuits (like cascode current sources) to achieve a very high, but finite, output resistance. For large $g_m R_{SS}$, the gain approximates to $A_{cm} \approx -R_D / (2R_{SS})$, showing that the gain is inversely proportional to the tail resistance.

#### The Common-Mode Half-Circuit

The symmetry of the common-mode response allows for a powerful simplification technique known as the **[common-mode half-circuit](@entry_id:275516)**. Since the two halves of the differential pair behave identically under common-mode excitation, we can analyze just one half of the circuit to find the gain.

Imagine splitting the tail resistor $R_{SS}$ into two parallel resistors, each with a value of $2R_{SS}$. The parallel combination is $(2R_{SS}) || (2R_{SS}) = R_{SS}$, so the circuit is unchanged. Now, because no current flows between the identical source nodes of M1 and M2 (due to symmetry), we can conceptually sever the connection between them. The circuit is now reduced to two identical common-source amplifiers. The "half-circuit" for M2 consists of the transistor M2, its load resistor $R_D$, and a [source degeneration](@entry_id:260703) resistor of value $2R_{SS}$.

This effective doubling of the tail resistance is a critical concept [@problem_id:1293130]. In a tail-biased [differential pair](@entry_id:266000) with a [tail current source](@entry_id:262705) having an [output resistance](@entry_id:276800) $R_{SS}$, the effective resistance seen looking down from the source of one of the transistors in the [common-mode half-circuit](@entry_id:275516) is $2R_{SS}$. This is because the small-signal source current from one transistor, $i_s$, is only half of the total current, $2i_s$, that flows through the actual tail resistance $R_{SS}$. By Ohm's law, the resistance seen by one transistor is $v_s / i_s = v_s / ((v_s/R_{SS})/2) = 2R_{SS}$. The gain of this [common-source amplifier](@entry_id:265648) with [source degeneration](@entry_id:260703) is precisely the common-mode gain we derived earlier: $A_{cm} = -g_m R_D / (1 + g_m (2R_{SS}))$, which matches our full-[circuit analysis](@entry_id:261116).

### Non-Ideal Effects on Common-Mode Performance

Beyond the fundamental limitation imposed by a finite tail impedance, several other non-ideal effects can degrade [common-mode rejection](@entry_id:265391) in practical circuits.

#### Common-Mode to Differential-Mode Conversion

Our analysis so far has assumed perfect symmetry. In reality, component mismatches are unavoidable. Mismatches in the load resistors or transistors can cause a pure common-mode input signal to generate a differential output signal. This effect is known as **common-mode to differential-mode (CM-to-DM) conversion**.

Consider a BJT differential pair with perfectly matched transistors but mismatched collector resistors, $R_{C1} = R_C$ and $R_{C2} = R_C(1+\delta)$, where $\delta$ is the fractional mismatch [@problem_id:1293133]. When a [common-mode voltage](@entry_id:267734) $v_{cm}$ is applied, the same small-signal collector current, $i_c$, flows in each branch. However, the output voltages at the collectors are different:
$$
v_{c1} = -i_c R_{C1} = -i_c R_C
$$
$$
v_{c2} = -i_c R_{C2} = -i_c R_C(1+\delta)
$$
This results in a non-zero differential output voltage $v_{od}$:
$$
v_{od} = v_{c1} - v_{c2} = -i_c R_C - (-i_c R_C(1+\delta)) = i_c R_C \delta
$$
The gain from the common-mode input to this spurious differential output is the CM-to-DM gain, $A_{cd} = v_{od}/v_{cm}$. Since $i_c$ is proportional to $v_{cm}$, $A_{cd}$ is non-zero if $\delta$ is non-zero. This generated differential signal is indistinguishable from a true differential input and will be subsequently amplified by the [differential gain](@entry_id:264006) of later stages, directly degrading the amplifier's effective CMRR. This highlights the critical importance of component matching for achieving high CMRR.

#### Frequency Dependence of Common-Mode Gain

CMRR is not a constant value; it typically degrades significantly at high frequencies. The primary culprit is [parasitic capacitance](@entry_id:270891) at the common-mode node (the shared source/emitter node). The [tail current source](@entry_id:262705), which we have modeled with a large resistance $R_T$, also has a [parasitic capacitance](@entry_id:270891) to ground, $C_T$.

At high frequencies, this capacitance provides a low-impedance path to ground. The total tail impedance is no longer just $R_T$, but rather $Z_T(j\omega) = R_T || (1/j\omega C_T)$. As the frequency $\omega$ increases, the magnitude of this impedance, $|Z_T|$, decreases.
From our gain expression $A_{cm} \approx -R_D/(2Z_T)$, we can see that a decrease in $|Z_T|$ leads to an **increase** in the magnitude of the common-mode gain, $|A_{cm}|$.

A more detailed analysis reveals that the transfer function for the common-mode gain has a zero introduced by the parallel $R_T C_T$ network in the feedback path [@problem_id:1293135]. This zero often occurs at a lower frequency than the pole, causing $|A_{cm}|$ to rise with frequency before eventually rolling off. This rising gain directly causes the CMRR to fall, often being the limiting factor for the high-frequency performance of differential amplifiers.

#### Dependence on DC Input Level

Another subtle but important non-ideality is the dependence of common-mode gain on the DC common-mode input level, $V_{CM}$. The output resistance of a transistor-based current source (e.g., $R_{SS}$ for a MOS source) is a function of the DC voltage across it, which is primarily due to the Early effect (in BJTs) or [channel-length modulation](@entry_id:264103) (in MOSFETs).

Consider a MOS differential pair biased by a single NMOS transistor (M3) as the [current source](@entry_id:275668). The DC voltage at the common source node, $V_P$, will track the DC input [common-mode voltage](@entry_id:267734), $V_{CM}$ (i.e., $V_P \approx V_{CM} - V_{GS,on}$). The drain-source voltage of the tail transistor M3 is thus $V_{DS3} = V_P - V_{supply}$, which is a direct function of $V_{CM}$.

Because the output resistance of M3, $R_{SS}$, is proportional to its $V_{DS3}$, $R_{SS}$ itself becomes a function of $V_{CM}$. Since the common-mode gain, $A_{cm}$, is inversely related to $R_{SS}$, it follows that $A_{cm}$ will vary as the DC common-mode input level changes [@problem_id:1293114]. This means the CMRR of an amplifier is not a single number but can change across its specified input [common-mode voltage](@entry_id:267734) range, a factor that must be considered in precision applications.