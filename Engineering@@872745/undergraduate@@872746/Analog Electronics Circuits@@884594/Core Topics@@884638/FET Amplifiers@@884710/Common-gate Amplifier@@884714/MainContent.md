## Introduction
Among the foundational building blocks of analog electronics, the three single-transistor amplifier topologies—common-source, common-drain, and common-gate—provide the basis for nearly all complex [circuit design](@entry_id:261622). While the common-source configuration is often the default choice for voltage amplification, the **Common-Gate (CG) Amplifier** possesses a distinct and powerful set of characteristics that are indispensable for certain high-performance applications. This article addresses the critical knowledge gap of when and why to employ the CG topology by providing a comprehensive exploration of its principles, applications, and practical design considerations.

In the chapters that follow, you will embark on a structured journey to master the CG amplifier. We will begin in **"Principles and Mechanisms"** by deconstructing its operation through [small-signal analysis](@entry_id:263462), deriving its unique low [input impedance](@entry_id:271561), non-inverting gain, and high [output impedance](@entry_id:265563). Next, **"Applications and Interdisciplinary Connections"** will demonstrate how these properties are leveraged in crucial roles, such as [impedance matching](@entry_id:151450) in RF systems, current buffering, and forming the high-gain cascode configuration. Finally, **"Hands-On Practices"** will solidify your understanding by guiding you through practical exercises that bridge theory and real-world design. Let us begin by examining the fundamental principles that define the behavior of the common-gate amplifier.

## Principles and Mechanisms

Following our introduction to the three fundamental single-transistor amplifier topologies, we now undertake a detailed examination of the **common-gate (CG) amplifier**. This configuration, while less prevalent as a general-purpose voltage amplifier than the common-source stage, possesses a unique set of characteristics that make it indispensable in specific applications, particularly in high-frequency and impedance-matching circuits. Our exploration will proceed from an idealized model to a more comprehensive analysis that incorporates practical device non-idealities, ultimately situating the amplifier's behavior within a system-level context.

### Defining the Common-Gate Configuration

An amplifier's topology is defined by which of the transistor's three terminals serves as the "common" reference point for the input and output signals. For a Metal-Oxide-Semiconductor Field-Effect Transistor (MOSFET), the terminals are the gate, source, and drain. In the **common-gate** configuration, the gate terminal is held at a constant DC potential. For small-signal AC analysis, this stable DC voltage source acts as an AC ground. The input signal is applied to the **source** terminal, and the amplified output signal is taken from the **drain** terminal [@problem_id:1292828]. This arrangement is distinct from the common-source (input at gate, output at drain) and common-drain (input at gate, output at source) configurations.

### Small-Signal Analysis: The Ideal Amplifier

To build an intuitive understanding of the CG amplifier's core behavior, we first analyze an idealized model. In this model, we assume the MOSFET's [channel-length modulation](@entry_id:264103) effect is negligible, which implies that its intrinsic small-signal output resistance, $r_o$, is infinitely large. We also neglect the [body effect](@entry_id:261475). The amplifier consists of a MOSFET, M1, with its gate at AC ground, an input signal $v_{in}$ applied to its source, and a load resistor $R_D$ connected from its drain to the power supply (an AC ground).

Our analysis begins with the small-signal equivalent circuit. The key relationship is that between the controlling gate-source voltage, $v_{gs}$, and the terminal voltages. With the gate at AC ground ($v_g = 0$) and the input signal applied to the source ($v_s = v_{in}$), the gate-source voltage is:
$v_{gs} = v_g - v_s = 0 - v_{in} = -v_{in}$

The small-signal drain current, $i_d$, is given by $i_d = g_m v_{gs}$, where $g_m$ is the transconductance of the transistor. Substituting our expression for $v_{gs}$, we find:
$i_d = g_m(-v_{in}) = -g_m v_{in}$

This equation is central to understanding the CG amplifier. It shows that the drain current is directly proportional to the input voltage applied at the source.

#### Input Resistance

The input resistance, $R_{in}$, is the impedance "seen" by the signal source driving the amplifier's input terminal. For the CG stage, this means looking into the source. $R_{in}$ is defined as the ratio of the input voltage, $v_{in}$, to the input current, $i_{in}$. In a MOSFET, the gate current is zero. By Kirchhoff's Current Law (KCL), the current entering the source, $i_{in}$, must be equal to the current leaving the drain (ignoring the path through $r_o$ in this ideal case). More precisely, the current flowing *into* the source from the input must equal the current flowing *out* of the source into the channel, which is the source current $i_s$. Since $i_s = i_d$, we have $i_{in} = i_s = i_d$. However, we must be careful with current directions.

The drain current $i_d = -g_m v_{in}$ flows from the drain terminal, through the channel, and into the source terminal. The input current, $i_{in}$, is defined as flowing from the external circuit *into* the source terminal. Therefore, $i_{in}$ is exactly the current flowing into the source, which is $-i_d$.
$i_{in} = -i_d = -(-g_m v_{in}) = g_m v_{in}$

The input resistance is then found to be:
$R_{in} = \frac{v_{in}}{i_{in}} = \frac{v_{in}}{g_m v_{in}} = \frac{1}{g_m}$

This is a defining characteristic of the common-gate amplifier: it exhibits a **low input resistance** [@problem_id:1292829]. The value of $g_m$ is typically in the range of millisiemens (mS), making $R_{in}$ on the order of hundreds of ohms to a few kilo-ohms. This property is in stark contrast to the nearly infinite input resistance of the common-source and common-drain stages.

#### Voltage Gain

The output voltage, $v_{out}$, is developed at the drain terminal. In our ideal circuit, the drain current $i_d$ flows out of the drain and into the load resistor $R_D$. By Ohm's law, and noting the standard current direction for a load resistor (current flows from the node to ground), we have:
$v_{out} = -i_d R_D$

Substituting our expression for $i_d$:
$v_{out} = -(-g_m v_{in}) R_D = g_m R_D v_{in}$

The voltage gain, $A_v = v_{out}/v_{in}$, is therefore:
$A_v = g_m R_D$

This result reveals two important properties [@problem_id:1292829]. First, the voltage gain is **positive**, meaning the CG amplifier is **non-inverting**. An increase in the input voltage at the source leads to an increase in the output voltage at the drain. Second, the magnitude of the gain is identical to that of an ideal [common-source amplifier](@entry_id:265648).

#### Current Gain

The CG amplifier is often described as a **[current buffer](@entry_id:264846)** or **current follower**. To see why, we can examine its short-circuit current gain, $A_{is} = i_{out}/i_{in}$. If the output at the drain is short-circuited to ground, the output current $i_{out}$ is simply the drain current, $i_d$. As established earlier, the input current $i_{in}$ is $-i_d$.
$A_{is} = \frac{i_{out}}{i_{in}} = \frac{i_d}{-i_d} = -1$
The negative sign arises from the convention of defining both currents as flowing *into* their respective ports. In terms of signal flow, a current injected into the source appears at the drain with nearly the same magnitude. This near-unity current transfer characteristic, combined with the low [input impedance](@entry_id:271561), makes the CG configuration highly effective at conveying a current signal from a low-impedance source to a load. A more detailed analysis shows the [current gain](@entry_id:273397) is slightly less than unity in a practical circuit [@problem_id:1292796].

### Incorporating Practical Device Characteristics

Our ideal model provides a solid foundation, but a practical design requires accounting for the non-ideal characteristics of the MOSFET, namely its finite [output resistance](@entry_id:276800) $r_o$ and the body effect.

#### The Effect of Finite Output Resistance ($r_o$)

The parameter $r_o$ models [channel-length modulation](@entry_id:264103) and appears in the [small-signal model](@entry_id:270703) as a resistor between the drain and source terminals. Its presence affects all three key amplifier parameters.

**Input Resistance ($R_{in}$):** To find the [input resistance](@entry_id:178645) in the presence of $r_o$, we again apply a test voltage $v_{in}$ to the source and calculate the input current $i_{in}$. The analysis is more involved, requiring KCL at both the source and drain nodes. Following this procedure [@problem_id:1292767], the input resistance is found to be:
$R_{in} = \frac{R_D + r_o}{1 + g_m r_o}$

Since the [intrinsic gain](@entry_id:262690) of the transistor, $g_m r_o$, is typically much greater than 1, we can approximate this expression:
$R_{in} \approx \frac{R_D + r_o}{g_m r_o} = \frac{1}{g_m} + \frac{R_D}{g_m r_o}$

This result shows that the input resistance is slightly larger than the ideal value of $1/g_m$. However, because $g_m r_o$ is large, the second term is usually small, and $R_{in}$ remains low.

**Voltage Gain ($A_v$):** With $r_o$ present, the output node at the drain sees a total resistance to ground equal to the parallel combination of the load resistor $R_D$ and the resistance looking back into the drain. The total resistance seen at the output is $R_D || r_o$. The dependent current $(g_m+g_{mb})v_{in}$ (including body effect for generality) flows through this combined resistance. Using the KCL derivation from [@problem_id:1292776] and setting the body-effect [transconductance](@entry_id:274251) $g_{mb} = 0$, the gain expression becomes:
$A_v = \frac{v_{out}}{v_{in}} = \frac{g_m + 1/r_o}{1/R_D + 1/r_o} = (g_m r_o + 1) \frac{R_D}{R_D + r_o}$

This can be interpreted as the effective transconductance $(g_m + 1/r_o)$ multiplied by the effective [load resistance](@entry_id:267991) $(R_D || r_o)$. As $r_o \to \infty$, this expression simplifies back to the ideal gain, $A_v = g_m R_D$. The finite [output resistance](@entry_id:276800) always reduces the voltage gain from its ideal value.

**Output Resistance ($R_{out}$):** The [output resistance](@entry_id:276800), $R_{out}$, is the impedance seen looking into the drain terminal with the input source turned off (i.e., the source terminal is connected to ground through the [source resistance](@entry_id:263068) $R_S$). The derivation [@problem_id:1292792] yields a striking result:
$R_{out} = r_o + R_S + g_m r_o R_S = r_o(1 + g_m R_S) + R_S$

This shows that the [output resistance](@entry_id:276800) is not simply $r_o$, but is significantly boosted by the presence of the [source resistance](@entry_id:263068) $R_S$. This phenomenon, known as **gain degeneration feedback**, makes the output impedance of the CG amplifier very high, a characteristic that is exploited in cascode amplifier designs to create high-gain stages. If the source is driven by an [ideal voltage source](@entry_id:276609) ($R_S = 0$), then $R_{out}$ reduces to just $r_o$.

#### The Body Effect

When the transistor's body (or substrate) terminal is not connected to its source terminal (e.g., the body is tied to ground), a change in the source voltage $v_s$ will modulate the [threshold voltage](@entry_id:273725), which in turn affects the drain current. This is the **body effect**. It is modeled by an additional dependent [current source](@entry_id:275668), $g_{mb}v_{bs}$, where $g_{mb}$ is the body-effect transconductance and $v_{bs}$ is the body-source voltage.

In the CG configuration, $v_s = v_{in}$ and the body is typically at AC ground ($v_b=0$). Therefore, $v_{bs} = v_b - v_s = -v_{in}$. The total drain-to-source dependent current becomes:
$i_{dep} = g_m v_{gs} + g_{mb} v_{bs} = g_m(-v_{in}) + g_{mb}(-v_{in}) = -(g_m + g_{mb})v_{in}$

The [body effect](@entry_id:261475) essentially acts in concert with the primary transconductance. Including this in the gain calculation [@problem_id:1292776] modifies the voltage gain to:
$A_v = \frac{g_m + g_{mb} + 1/r_o}{1/R_D + 1/r_o}$

The [body effect](@entry_id:261475) increases the effective [transconductance](@entry_id:274251) to $(g_m + g_{mb})$, thus slightly increasing the voltage gain of the amplifier. In many designs, its contribution is relatively small compared to $g_m$, but it must be included for precise analysis.

### System-Level Performance and Applications

The unique impedance characteristics of the CG amplifier define its primary applications.

#### Impedance Matching for Low-Impedance Sources

The low input resistance of the CG stage makes it an excellent choice for an input amplifier driven by a low-impedance source, such as a $50\,\Omega$ antenna or [transmission line](@entry_id:266330). To maximize power transfer and minimize signal reflections, the amplifier's [input impedance](@entry_id:271561) should match the source's output impedance. A [common-source amplifier](@entry_id:265648), with its high [input impedance](@entry_id:271561), would create a severe mismatch.

Consider an RF receiver front-end where a CG amplifier is driven by an antenna with a [source resistance](@entry_id:263068) $R_{sig} = 50\,\Omega$ [@problem_id:1292816]. The input of the CG amplifier has a low resistance, providing a reasonable match. However, we must analyze the **overall voltage gain**, $G_v = v_{out}/v_{sig}$, which accounts for the voltage division between the [source resistance](@entry_id:263068) $R_{sig}$ and the amplifier's [input resistance](@entry_id:178645) $R_{in}$. A detailed derivation [@problem_id:1292822] gives the overall gain as:
$G_v = \frac{v_{out}}{v_{sig}} = \frac{(1+g_m r_o)R_D}{R_D+r_o+R_{sig}(1+g_m r_o)}$

Conversely, driving a CG amplifier with a high-impedance source leads to poor performance. A large $R_{sig}$ forms a voltage divider with the small $R_{in}$ of the CG stage, causing most of the signal voltage to be dropped across $R_{sig}$, resulting in significant [signal attenuation](@entry_id:262973) before amplification even begins. This is precisely the scenario explored in a hypothetical bio-potential sensor application with high source impedance [@problem_id:1292808]. In such a case, inserting an ideal unity-gain voltage buffer (with infinite [input impedance](@entry_id:271561) and zero [output impedance](@entry_id:265563)) before the CG stage dramatically improves the overall gain by preventing this input voltage division. The ratio of gain with the buffer to gain without it quantifies this improvement, highlighting the importance of proper impedance matching.

#### Comparison with BJT Common-Base Amplifier

The BJT equivalent of the CG amplifier is the **common-base (CB) amplifier**. It also features low input impedance and is used in similar applications. It is instructive to compare the input resistance of the two. For a BJT biased at a collector current $I_Q$, its ideal [input resistance](@entry_id:178645) (looking into the emitter) is $r_e = V_T/I_Q$, where $V_T$ is the [thermal voltage](@entry_id:267086). For a MOSFET biased at a drain current $I_Q$, its [input resistance](@entry_id:178645) is $1/g_m$. The transconductance $g_m$ can be expressed as $2I_Q/V_{OV}$, where $V_{OV}$ is the [overdrive voltage](@entry_id:272139).

The ratio of the two input resistances at the same [quiescent current](@entry_id:275067) $I_Q$ is therefore [@problem_id:1292830]:
$\frac{R_{in,CG}}{R_{in,CB}} = \frac{1/g_{m,MOS}}{1/g_{m,BJT}} = \frac{V_{OV}/(2I_Q)}{V_T/I_Q} = \frac{V_{OV}}{2V_T}$

Since a typical [overdrive voltage](@entry_id:272139) ($V_{OV} \approx 100-200\,\text{mV}$) is significantly larger than twice the [thermal voltage](@entry_id:267086) ($2V_T \approx 52\,\text{mV}$), the input resistance of a CG amplifier is generally several times higher than that of a CB amplifier biased at the same current. This means the BJT common-base stage provides an even lower input impedance.

### Summary of Characteristics

The common-gate amplifier can be summarized by the following key properties:

*   **Voltage Gain:** Moderate and non-inverting ($A_v \approx g_m R_D$).
*   **Input Resistance:** Low ($R_{in} \approx 1/g_m$), making it suitable for current sensing or for interfacing with low-impedance signal sources.
*   **Output Resistance:** High ($R_{out} \approx r_o(1+g_mR_S)$), especially when driven by a source with finite resistance.
*   **Primary Applications:** Current buffer (current follower), input stage for low-impedance sources (e.g., RF antennas), and as the second stage in a cascode amplifier to provide high [output impedance](@entry_id:265563).

By understanding these principles and mechanisms, the circuit designer can effectively leverage the unique strengths of the common-gate configuration to solve specific challenges in analog and RF circuit design.