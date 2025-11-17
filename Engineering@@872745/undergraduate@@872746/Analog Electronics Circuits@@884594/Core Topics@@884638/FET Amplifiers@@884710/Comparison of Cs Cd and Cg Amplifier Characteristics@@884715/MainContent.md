## Introduction
The Common-Source (CS), Common-Drain (CD), and Common-Gate (CG) amplifier configurations form the bedrock of modern [analog circuit design](@entry_id:270580). While each utilizes a single transistor, their performance characteristics diverge significantly, presenting designers with a critical choice for any given application. This article addresses the fundamental question of how to select the optimal topology by systematically comparing their distinct properties. It aims to bridge the gap between theoretical models and practical application, providing a clear framework for understanding when and why to use each configuration.

Throughout the following sections, you will embark on a comprehensive journey through these essential circuits. The first section, **Principles and Mechanisms**, will dissect the small-signal behavior of each topology, deriving their voltage gain, [input impedance](@entry_id:271561), and output impedance. Next, **Applications and Interdisciplinary Connections** will explore how these characteristics translate into real-world roles, from simple buffering to integration in complex systems like RF circuits and [feedback loops](@entry_id:265284). Finally, **Hands-On Practices** will offer practical problems to reinforce these concepts and develop your design intuition. By the end, you will have a robust understanding of how to leverage the unique strengths of the CS, CD, and CG amplifiers in your own designs.

## Principles and Mechanisms

The three fundamental single-transistor amplifier topologies—Common-Source (CS), Common-Drain (CD), and Common-Gate (CG)—represent the foundational building blocks of analog integrated [circuit design](@entry_id:261622). While all three utilize a single transistor, their performance characteristics diverge dramatically based on a simple but critical choice: which of the transistor's three terminals serves as the common AC ground reference for the input and output signals. Understanding the principles that govern each configuration and the mechanisms that give rise to their unique properties is essential for any circuit designer.

This chapter will systematically analyze each topology by evaluating a consistent set of key performance metrics: voltage gain ($A_v$), [input impedance](@entry_id:271561) ($R_{in}$), and output impedance ($R_{out}$). We will explore how these characteristics arise from the amplifier's structure and the transistor's intrinsic small-signal parameters, namely its **transconductance** ($g_m$) and **intrinsic output resistance** ($r_o$).

### The Common-Source (CS) Amplifier: The Voltage Gain Workhorse

The Common-Source (CS) configuration is arguably the most intuitive and widely used amplifier topology. The input signal is applied to the gate, the output is taken from the drain, and the source terminal is connected to a common potential, typically AC ground. This arrangement is designed to achieve significant voltage amplification.

**Voltage Gain ($A_v$)**

A defining characteristic of the CS amplifier is its ability to provide a large voltage gain. The mechanism is straightforward: a small change in the gate-to-source voltage ($v_{gs}$) causes a proportional change in the drain current ($i_d = g_m v_{gs}$). This current flows through the load impedance connected at the drain, which is typically a drain resistor ($R_D$) in parallel with the transistor's own output resistance ($r_o$). The output voltage is the product of this current and the total drain impedance. Because an increasing gate voltage increases drain current, which in turn increases the voltage drop across the drain resistor, the drain voltage *decreases*. This results in an inverted output signal.

The small-signal voltage gain is therefore given by:
$$
A_{v,CS} = -g_m (R_D \parallel r_o) = -g_m \frac{R_D r_o}{R_D + r_o}
$$
This expression reveals two key facts. First, the gain is negative, signifying a $180^\circ$ phase inversion between the input and output. If one were to observe the input and output on an oscilloscope, the output waveform would appear as a vertically flipped and amplified version of the input [@problem_id:1294157]. Second, the magnitude of the gain is directly proportional to both the [transconductance](@entry_id:274251) $g_m$ and the effective [load resistance](@entry_id:267991) at the drain [@problem_id:1294108]. For significant voltage gain, a high value for $g_m (R_D \parallel r_o)$ is required.

**Input and Output Impedance ($R_{in}$, $R_{out}$)**

In the CS configuration, the input signal is applied to the MOSFET's gate. Since the gate is dielectrically insulated from the channel, it draws virtually no DC current. At low frequencies, the input impedance is therefore theoretically infinite [@problem_id:1294127]. In practice, it is extremely high, limited only by gate leakage currents and the biasing network resistors.

The [output impedance](@entry_id:265563), viewed from the drain terminal, is determined by setting the input voltage to zero ($v_{in} = 0$). This grounds the gate, turning off the dependent current source ($g_m v_{gs} = 0$). The only paths to AC ground from the drain are through the external drain resistor $R_D$ and the transistor's [internal resistance](@entry_id:268117) $r_o$. The [output impedance](@entry_id:265563) is thus:
$$
R_{out,CS} = R_D \parallel r_o
$$
Since both $R_D$ and $r_o$ are typically large resistances (in the kilo-ohm to mega-ohm range), the CS amplifier is characterized by a **high output impedance** [@problem_id:136].

**Summary and High-Frequency Behavior**

The CS amplifier is a high-gain, inverting voltage amplifier with high [input impedance](@entry_id:271561) and high [output impedance](@entry_id:265563). However, its high-frequency performance is often limited by the **Miller effect**. The parasitic gate-to-drain capacitance, $C_{gd}$, connects the input node to the output node. Due to the large, inverting gain ($A_{v,CS}$), this capacitance appears at the input as a much larger effective capacitance, $C_{in,Miller} = C_{gd}(1 - A_{v,CS}) = C_{gd}(1 + |A_{v,CS}|)$. This large [input capacitance](@entry_id:272919) forms a [low-pass filter](@entry_id:145200) with the [source resistance](@entry_id:263068), severely restricting the amplifier's bandwidth [@problem_id:1294164].

### The Common-Drain (CD) Amplifier: The Voltage Buffer

When the primary goal is not voltage gain but [impedance transformation](@entry_id:262584), the Common-Drain (CD) configuration excels. In this topology, the input is applied to the gate, but the output is taken from the source. The drain terminal is the common reference, typically connected to the positive supply voltage ($V_{DD}$), making it an AC ground. This circuit is ubiquitously known as the **[source follower](@entry_id:276896)**.

**Voltage Gain ($A_v$)**

The name "[source follower](@entry_id:276896)" aptly describes its function. The voltage at the source terminal ($v_s$) closely follows the voltage at the gate ($v_g$). The mechanism involves inherent negative feedback: if the gate voltage rises, the source voltage also tries to rise. This maintains a relatively constant gate-source voltage $v_{gs}$, which in turn keeps the drain current stable. The small-signal voltage gain is given by:
$$
A_{v,CD} = \frac{g_m (R_S \parallel r_o)}{1 + g_m (R_S \parallel r_o)}
$$
where $R_S$ is the resistance at the source. This gain is always positive (non-inverting) and has a magnitude strictly less than 1. For typical designs where $g_m (R_S \parallel r_o) \gg 1$, the gain approaches unity ($A_v \approx +1$). This non-inverting, near-unity gain is a hallmark of the [source follower](@entry_id:276896) [@problem_id:1294154].

**Input and Output Impedance ($R_{in}$, $R_{out}$)**

Like the CS amplifier, the CD stage takes its input at the gate, granting it a very **high [input impedance](@entry_id:271561)** [@problem_id:1294127]. This is a crucial feature, as it allows the amplifier to connect to a high-impedance signal source without loading it down and attenuating the signal.

The most valuable characteristic of the [source follower](@entry_id:276896) is its **low [output impedance](@entry_id:265563)**. When looking into the source terminal, the transistor actively works to supply current and maintain the output voltage. Any attempt to change the source voltage is strongly opposed by a large change in the transistor's current, which is the definition of a low impedance node. The output impedance is approximately:
$$
R_{out,CD} \approx \frac{1}{g_m} \parallel r_o \parallel R_S
$$
In most cases, $1/g_m$ is much smaller than the other resistances, so the [output impedance](@entry_id:265563) is effectively $R_{out,CD} \approx 1/g_m$. This value is typically low, ranging from a few ohms to a few hundred ohms [@problem_id:1294147].

**Summary and Application**

The CD amplifier combines high [input impedance](@entry_id:271561) with low output impedance, with a non-inverting voltage gain of approximately one. It does not amplify voltage; instead, it provides **[current gain](@entry_id:273397)** and acts as an exceptional **voltage buffer**. Its primary application is to serve as an intermediary stage that connects a high-impedance source (like a condenser microphone or a weak sensor) to a low-impedance load (like a cable or the next amplifier stage), ensuring maximum signal voltage transfer [@problem_id:1294154] [@problem_id:1294147].

### The Common-Gate (CG) Amplifier: The Current Buffer

The Common-Gate (CG) configuration is the third and [final topology](@entry_id:150988), completing the trio. Here, the input signal is applied to the source terminal, the output is taken from the drain, and the gate is held at AC ground. This arrangement results in properties that are, in many ways, the inverse of the CD stage.

**Voltage Gain ($A_v$)**

Similar to the CS amplifier, the CG configuration can provide significant voltage gain. An input signal at the source modulates the gate-to-source voltage ($v_{gs} = v_g - v_s = 0 - v_{in} = -v_{in}$), which in turn controls the drain current. This current flows through the drain's load impedance ($R_D \parallel r_o$) to produce the output voltage. The small-signal voltage gain is:
$$
A_{v,CG} = g_m (R_D \parallel r_o)
$$
Notice that this gain is non-inverting (positive) and can be large, with a magnitude identical to that of the CS amplifier [@problem_id:1294108]. The lack of phase inversion is a key [differentiator](@entry_id:272992) from the CS stage.

**Input and Output Impedance ($R_{in}$, $R_{out}$)**

The most distinguishing feature of the CG amplifier is its **low input impedance**. Unlike the CS and CD stages, the input signal is applied to the source, a current-carrying terminal. The input voltage $v_{in}$ at the source directly drives a current $i_{in} \approx g_m v_{in}$ into the transistor. Consequently, the [input impedance](@entry_id:271561) is:
$$
R_{in,CG} \approx \frac{1}{g_m}
$$
This inherently low input impedance makes the CG stage uniquely suited for specific applications [@problem_id:1294110] [@problem_id:1294127].

The [output impedance](@entry_id:265563) of the CG amplifier, looking into the drain, is identical to that of the CS amplifier: **high**. With the input source grounded for the calculation, the analysis is the same, yielding:
$$
R_{out,CG} = R_D \parallel r_o
$$

**Summary and Application**

The CG amplifier offers non-inverting voltage gain, low [input impedance](@entry_id:271561), and high [output impedance](@entry_id:265563). These characteristics make it an excellent **[current buffer](@entry_id:264846)**. It is ideal for situations where the signal source has a very low [output impedance](@entry_id:265563), such as a dynamic microphone or a 50-ohm transmission line, as it provides a natural impedance match at the input [@problem_id:1294144]. Furthermore, because the grounded gate acts as an electrostatic shield between the input (source) and output (drain), the capacitive feedback responsible for the Miller effect in the CS stage is eliminated. This gives the CG amplifier superior high-frequency performance [@problem_id:1294164].

### A Comparative Synthesis

The choice among the CS, CD, and CG topologies is a fundamental design decision driven entirely by the specific requirements of the application. A side-by-side comparison crystallizes their distinct roles [@problem_id:1294146] [@problem_id:136]:

*   **Common-Source (CS):** The quintessential voltage amplifier. It is chosen when the primary objective is to achieve a large, inverted voltage gain from a source that is not heavily loaded by the amplifier's high [input impedance](@entry_id:271561). Its primary drawback is a relatively high output impedance and poor high-[frequency response](@entry_id:183149) due to the Miller effect.

*   **Common-Drain (CD) / Source Follower:** The ideal voltage buffer. It is chosen to interface a high-impedance source with a low-impedance load. It trades voltage gain (providing only unity gain) for the critical function of [impedance transformation](@entry_id:262584), preserving [signal integrity](@entry_id:170139) across disparate stages.

*   **Common-Gate (CG):** The specialized [current buffer](@entry_id:264846) and [high-frequency amplifier](@entry_id:270993). It is selected to interface with low-impedance signal sources where a low input impedance is required for proper matching. It provides non-inverting voltage gain and, thanks to its immunity to the Miller effect, is a preferred choice in many radio-frequency (RF) circuits.

Ultimately, these three configurations are not competitors but rather complementary tools in the analog designer's toolkit. Mastery of their individual principles and mechanisms enables the construction of sophisticated, multi-stage amplifier systems tailored to any performance specification.