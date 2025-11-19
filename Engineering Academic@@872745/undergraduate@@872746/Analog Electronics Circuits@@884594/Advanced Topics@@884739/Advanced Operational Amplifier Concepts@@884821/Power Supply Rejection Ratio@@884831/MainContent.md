## Introduction
In the world of [analog electronics](@entry_id:273848), the performance of any circuit is fundamentally tied to the quality of its power supply. While designers often start with the assumption of a perfect, noiseless voltage source, reality presents a far more challenging environment of ripple, transients, and noise. A critical question then arises: how resilient is a circuit to these inevitable supply imperfections? The answer lies in a key [figure of merit](@entry_id:158816) known as the **Power Supply Rejection Ratio (PSRR)**, which quantifies a circuit's ability to reject unwanted variations on its supply lines and preserve [signal integrity](@entry_id:170139). Understanding and optimizing PSRR is not merely an academic exercise; it is essential for designing robust, high-performance electronic systems.

This article provides a comprehensive exploration of this vital parameter. The first chapter, **"Principles and Mechanisms,"** will lay the theoretical groundwork by defining PSRR, examining the physical mechanisms of noise coupling, and analyzing its behavior in fundamental amplifier stages. Following this, the **"Applications and Interdisciplinary Connections"** chapter will bridge theory and practice, demonstrating how finite PSRR impacts performance in real-world systems, from precision instrumentation and audio amplifiers to mixed-signal and RF circuits. Finally, the **"Hands-On Practices"** section will offer targeted exercises to reinforce these concepts and develop practical analysis skills.

## Principles and Mechanisms

In the design of [analog circuits](@entry_id:274672), the power supply is often assumed to be an ideal, constant voltage source. In reality, all power supplies exhibit some form of imperfection, such as noise, ripple from AC-DC conversion, or transient fluctuations due to changing load conditions. The **Power Supply Rejection Ratio (PSRR)** is a critical [figure of merit](@entry_id:158816) that quantifies a circuit's ability to reject these unwanted variations on its supply lines and prevent them from corrupting the output signal. A high PSRR is synonymous with high immunity to power supply noise and is a hallmark of robust analog design.

### Defining Power Supply Rejection

Conceptually, an [ideal amplifier](@entry_id:260682) or circuit would be completely insensitive to variations in its power supply. Any ripple or noise on the supply rail would have no effect on the output voltage. For such a hypothetical ideal circuit, the change in output voltage due to a change in supply voltage would be zero. This corresponds to a theoretically infinite Power Supply Rejection Ratio, representing perfect rejection [@problem_id:1325970].

In practice, imperfections in circuit components and design mean that some fraction of the supply noise will always "leak" through to the output. To quantify this leakage, we first define the **power supply gain**, denoted as $A_{ps}$, which is the small-signal transfer function from the supply voltage to the output voltage:

$$
A_{ps} = \frac{v_{out}}{v_{supply}}
$$

where $v_{out}$ is the small-signal change in the output voltage and $v_{supply}$ is the small-signal change (the noise or ripple) on the power supply rail. A smaller magnitude of $A_{ps}$ indicates better performance.

The Power Supply Rejection Ratio (PSRR) is the metric derived from this gain. However, its formal definition can vary depending on the context. Two common definitions are prevalent in academic literature and industry datasheets:

1.  **PSRR as Reciprocal of Supply Gain:** This definition expresses PSRR as the inverse of the magnitude of the power supply gain. It directly quantifies how much a supply variation is attenuated at the output. This definition is common for circuits like voltage references, where the primary function is to provide a stable output.
    $$
    \text{PSRR} = \frac{1}{|A_{ps}|} = \left| \frac{v_{supply}}{v_{out}} \right|
    $$

2.  **PSRR as Ratio of Gains:** For amplifying circuits, PSRR is often defined as the magnitude of the ratio of the desired signal gain ($A_v$) to the undesired supply gain ($A_{ps}$). This definition intuitively compares how much better the circuit is at amplifying the signal than it is at passing the noise.
    $$
    \text{PSRR} = \left| \frac{A_v}{A_{ps}} \right|
    $$

Regardless of the definition used, a larger PSRR value always signifies superior rejection of power supply noise. PSRR is almost universally expressed in **decibels (dB)**:

$$
\text{PSRR}_{\text{dB}} = 20 \log_{10}(\text{PSRR})
$$

It is essential to distinguish PSRR from the **Common-Mode Rejection Ratio (CMRR)**. While both are measures of rejection, they address different interference sources. CMRR quantifies the rejection of noise that appears identically on both differential inputs, whereas PSRR quantifies the rejection of noise originating from the power supply rails [@problem_id:1293369]. A circuit can have excellent CMRR but poor PSRR, or vice-versa, as the underlying coupling mechanisms are distinct.

### Fundamental Coupling Mechanisms

The most fundamental way supply noise couples to an output is through resistive paths. Consider a simple resistive voltage divider used to create a bias voltage, $V_{OUT}$, from a supply $V_{SUPPLY}$ using resistors $R_1$ and $R_2$ [@problem_id:1325937]. The output voltage is given by:

$$
V_{OUT} = V_{SUPPLY} \frac{R_2}{R_1 + R_2}
$$

The supply gain is the derivative of $V_{OUT}$ with respect to $V_{SUPPLY}$:

$$
A_{ps} = \frac{\mathrm{d}V_{OUT}}{\mathrm{d}V_{SUPPLY}} = \frac{R_2}{R_1 + R_2}
$$

Using the first definition, the PSRR for this simple network is:

$$
\text{PSRR} = \frac{1}{|A_{ps}|} = \frac{R_1 + R_2}{R_2} = 1 + \frac{R_1}{R_2}
$$

This simple result reveals that a passive divider offers very limited power supply rejection. To achieve a high PSRR (e.g., 100, which is 40 dB), $R_1$ would need to be 99 times larger than $R_2$, which is often impractical and leads to other issues like high [output impedance](@entry_id:265563). This illustrates the need for active circuitry to achieve effective supply [noise rejection](@entry_id:276557).

### PSRR in Single-Stage Amplifiers

Active devices introduce more complex coupling paths. Let's analyze a canonical [common-source amplifier](@entry_id:265648), a stage commonly used in bio-potential acquisition systems where supply noise can corrupt weak signals [@problem_id:1325994]. The amplifier uses an N-channel MOSFET with [transconductance](@entry_id:274251) $g_m$ and output resistance $r_o$, and a load resistor $R_D$ connected to the noisy supply.

To find the PSRR, we must derive both the signal gain $A_v$ and the supply gain $A_{ps}$ using [small-signal analysis](@entry_id:263462).

1.  **Signal Gain ($A_v$):** With the [supply ripple](@entry_id:271017) $v_{dd}$ set to zero (AC ground), the load resistor $R_D$ is in parallel with the transistor's [output resistance](@entry_id:276800) $r_o$. The signal gain is:
    $$
    A_v = \frac{v_{out}}{v_{in}} = -g_m (R_D \parallel r_o) = -g_m \frac{R_D r_o}{R_D + r_o}
    $$

2.  **Supply Gain ($A_{ps}$ or $A_{DD}$):** With the input $v_{in}$ set to zero, the transistor's dependent current source $g_m v_{gs}$ is inactive ($v_{gs}=0$). The circuit simplifies to a voltage divider where the [supply ripple](@entry_id:271017) $v_{dd}$ is divided between the load resistor $R_D$ and the transistor's output resistance $r_o$. The output voltage is the voltage across $r_o$.
    $$
    A_{ps} = A_{DD} = \frac{v_{out}}{v_{dd}} = \frac{r_o}{R_D + r_o}
    $$

This derivation reveals a key physical mechanism: the finite output resistance of the transistor, $r_o$, provides some isolation from the supply rail, but the noise still couples to the output through the divider formed by $R_D$ and $r_o$. A higher $r_o$ leads to a lower $A_{ps}$ and thus better inherent rejection.

Now, if we apply the gain-ratio definition of PSRR [@problem_id:1325994] [@problem_id:1325958]:

$$
\text{PSRR} = \left| \frac{A_v}{A_{ps}} \right| = \left| \frac{-g_m \frac{R_D r_o}{R_D + r_o}}{\frac{r_o}{R_D + r_o}} \right| = g_m R_D
$$

This elegant result shows that for a [common-source amplifier](@entry_id:265648) with a resistive load, this particular definition of PSRR is surprisingly independent of the transistor's [output resistance](@entry_id:276800) $r_o$. While $r_o$ fundamentally determines the supply gain $A_{ps}$, its effect cancels out when forming the ratio with the signal gain $A_v$. For a transistor with $g_m = 2.5 \text{ mA/V}$ and a load $R_D = 8.0 \text{ k}\Omega$, the PSRR would be $20 \log_{10}(2.5 \times 10^{-3} \times 8.0 \times 10^3) = 20 \log_{10}(20) \approx 26.0 \text{ dB}$ [@problem_id:1325958].

### PSRR in Differential and Multi-Stage Circuits

In more complex circuits like operational amplifiers, we must consider rejection from both positive and negative supply rails, denoted **PSRR+** and **PSRR-**, respectively. The coupling mechanisms can be very different for each rail.

Consider a BJT [differential pair](@entry_id:266000), the input stage of many op-amps [@problem_id:1325963].
*   **PSRR+ (Positive Supply):** Noise on the positive supply, $V_{CC}$, directly affects the voltage across the collector load resistors. If the circuit were perfectly symmetrical (e.g., perfectly matched load resistors), this noise would appear as an identical [common-mode signal](@entry_id:264851) at both collectors, resulting in zero differential output voltage. However, any mismatch in the load resistors converts this common-mode variation into a differential signal, degrading PSRR+. Therefore, **asymmetry is the primary enemy of PSRR+** in a differential stage.
*   **PSRR- (Negative Supply):** Noise on the negative supply, $V_{EE}$, affects the biasing of the [tail current source](@entry_id:262705) that sets the stage's operating current. The finite output resistance of this non-[ideal current source](@entry_id:272249) allows the supply noise to modulate the tail current. This modulated current then flows through the [differential pair](@entry_id:266000), and any asymmetry (even the same load mismatch as before) will cause it to produce a net differential output voltage. Thus, **the finite [output impedance](@entry_id:265563) of the [tail current source](@entry_id:262705) is a primary limiting factor for PSRR-**.

When these stages are combined in a standard two-stage [op-amp architecture](@entry_id:263426), one path often dominates the overall PSRR. For PSRR-, the dominant limitation at low frequencies is typically the second stage [@problem_id:1325935]. This is because the second stage is often a common-source or [common-emitter amplifier](@entry_id:272876) whose source terminal is connected directly to the negative supply rail ($V_{SS}$ or $V_{EE}$). Any variation on this rail directly modulates the gate-source (or base-emitter) voltage of the driving transistor, which is then amplified by the full gain of the second stage, leading to poor rejection.

### Improvement of PSRR with Negative Feedback

While individual stages may have modest PSRR, the application of **[negative feedback](@entry_id:138619)** around an amplifier dramatically improves its performance, including its PSRR. The effect of supply noise can be modeled as a disturbance voltage injected at the output of the open-loop amplifier. Negative feedback works to sense this output disturbance and apply a corrective signal at the input to counteract it.

The relationship between the closed-loop PSRR ($\text{PSRR}_{CL}$) and open-loop PSRR ($\text{PSRR}_{OL}$) is directly related to the amount of feedback in the circuit, quantified by the [loop gain](@entry_id:268715), $\beta A_{OL}$, where $\beta$ is the [feedback factor](@entry_id:275731) and $A_{OL}$ is the open-[loop gain](@entry_id:268715). The supply gain is reduced by the [loop gain](@entry_id:268715) factor:

$$
A_{ps,CL} = \frac{A_{ps,OL}}{1 + \beta A_{OL}}
$$

Consequently, the PSRR (defined as $1/|A_{ps}|$) is improved by this same factor [@problem_id:1326767]:

$$
\text{PSRR}_{CL} = \text{PSRR}_{OL} \times (1 + \beta A_{OL})
$$

Consider an [op-amp](@entry_id:274011) with an open-loop gain $A_{OL} = 1.25 \times 10^{5}$ and an open-loop PSRR of 80 dB. If this op-amp is configured as a [non-inverting amplifier](@entry_id:272128) with a closed-loop gain of $G = 25$, the [feedback factor](@entry_id:275731) is $\beta = 1/G = 0.04$. The loop gain factor is $1 + (0.04)(1.25 \times 10^5) = 5001$. The PSRR improves by this factor. In decibels, the new PSRR is:

$$
\text{PSRR}_{CL,dB} \approx \text{PSRR}_{OL,dB} + 20 \log_{10}(1 + \beta A_{OL}) \approx 80 \text{ dB} + 20 \log_{10}(5001) \approx 80 + 74 = 154 \text{ dB}
$$
This substantial improvement highlights the power of [negative feedback](@entry_id:138619) in creating precision circuits from non-ideal components.

### Frequency Dependence of PSRR

The impressive PSRR achieved with feedback is not constant across all frequencies. In virtually all op-amps, **PSRR degrades significantly at higher frequencies**.

The primary reason for this degradation is the frequency-dependent nature of the op-amp's open-loop gain, $A_{OL}$ [@problem_id:1325989]. Internally compensated op-amps are designed to have a dominant low-frequency pole, after which their open-loop gain rolls off, typically at -20 dB/decade. Since the PSRR improvement factor, $(1 + \beta A_{OL})$, depends directly on this gain, the benefits of feedback diminish as frequency increases.

As the [loop gain](@entry_id:268715) falls, the feedback loop becomes less effective at correcting for the supply-induced errors. At very high frequencies, the [loop gain](@entry_id:268715) approaches zero, and the closed-loop PSRR converges toward the amplifier's much poorer open-loop PSRR.

This behavior is often modeled with a single-pole response. For an audio pre-amplifier design, for example, the PSRR as a function of frequency $f$ might be given by a formula like [@problem_id:1326000]:

$$
\text{PSRR}_{\text{dB}}(f) = \text{PSRR}_{\text{dB,dc}} - 10 \log_{10}\left(1 + \left(\frac{f}{f_c}\right)^2\right)
$$

Here, $\text{PSRR}_{\text{dB,dc}}$ is the excellent PSRR at DC, and $f_c$ is a corner frequency where the rejection begins to roll off. This model allows engineers to calculate the available rejection at specific frequencies of interest, such as the switching frequency of a power supply, and determine if it meets the system requirements. For an op-amp with 95 dB of DC PSRR and a corner frequency of 150 Hz, the PSRR would drop to 30 dB at a frequency of approximately 267 kHz, a calculation crucial for ensuring [signal integrity](@entry_id:170139) in high-fidelity applications [@problem_id:1326000]. Understanding this frequency dependence is vital for successful real-world circuit design.