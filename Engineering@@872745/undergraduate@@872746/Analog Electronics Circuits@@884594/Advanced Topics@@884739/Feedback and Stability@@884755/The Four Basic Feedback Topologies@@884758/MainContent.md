## Introduction
Negative feedback is one of the most powerful and fundamental concepts in [analog electronics](@entry_id:273848), enabling engineers to transform imperfect amplifiers into stable, predictable, and high-performance circuits. While the general benefits of feedback—such as gain stabilization and distortion reduction—are widely appreciated, the true art of feedback design lies in its implementation. How we connect a feedback network to an amplifier is not arbitrary; it is a critical design choice that systematically sculpts the circuit's behavior. The core challenge is understanding how to configure this connection to achieve specific goals, such as creating a high-impedance input for a sensor or a low-impedance output to drive a speaker.

This article addresses this challenge by providing a systematic classification of the four basic [feedback topologies](@entry_id:261245). By mastering these structures, you will gain the ability to analyze and design amplifiers with precision, tailoring their characteristics for any given application. The following chapters will guide you through this essential topic:

-   **Principles and Mechanisms** will deconstruct the feedback connection into its two core actions—sampling and mixing—and use them to define the four topologies: series-shunt, shunt-shunt, series-series, and shunt-series. You will learn how each one predictably modifies the amplifier's input and output impedances.

-   **Applications and Interdisciplinary Connections** will bridge theory and practice by demonstrating these topologies at work in real-world circuits, from [op-amp](@entry_id:274011) configurations to power converters. We will also explore how these same principles govern the behavior of complex systems in other fields, including control engineering and biology.

-   **Hands-On Practices** will provide a set of guided problems, allowing you to apply your knowledge to analyze practical amplifier circuits and solidify your understanding of feedback analysis.

## Principles and Mechanisms

Having established the fundamental benefits of [negative feedback](@entry_id:138619)—such as gain stabilization, [bandwidth extension](@entry_id:266466), and reduction of nonlinear distortion—we now turn to the practical implementation of feedback systems. The manner in which the feedback network is connected to the core amplifier is a critical design choice that profoundly influences the circuit's overall characteristics. This connection scheme, known as the **[feedback topology](@entry_id:271848)**, determines the nature of the signals being processed and systematically modifies the amplifier's input and output impedances. Understanding these topologies is essential for designing amplifiers that are tailored to specific applications, whether it be buffering a high-impedance sensor or driving a low-impedance load.

### The Two Fundamental Actions: Sampling and Mixing

At its core, any feedback connection can be deconstructed into two distinct actions:

1.  **Sampling** at the output: The feedback network must sense or "sample" the output signal. The nature of the output signal (voltage or current) dictates how this connection is made.

2.  **Mixing** at the input: The feedback network generates a signal that is combined or "mixed" with the external input signal. This creates an [error signal](@entry_id:271594) that is then fed into the basic amplifier. The way these signals are combined determines the type of mixing.

The specific combination of sampling and mixing methods defines one of four basic [feedback topologies](@entry_id:261245). Each topology is suited to a particular type of amplification and sculpts the terminal impedances in predictable ways. We will explore these sampling and mixing techniques before classifying the four resulting structures.

### Output Sampling: Sensing Voltage or Current

The first step in closing a feedback loop is to measure the output signal. There are two ways to accomplish this, corresponding to the two possible types of output signals: voltage and current.

#### Shunt (Voltage) Sampling

To sample the output **voltage** ($v_o$), the feedback network is connected in **parallel** or **shunt** across the output port of the amplifier. In this configuration, the voltage across the output terminals is directly applied to the input of the feedback network.

A key consequence of shunt sampling is a **reduction in [output impedance](@entry_id:265563)**. Intuitively, the feedback mechanism strives to maintain a constant output voltage, as determined by the input signal and the closed-loop gain. If an external load attempts to draw more current and pull the output voltage down, the feedback loop will adjust the amplifier's output to counteract this change. This action makes the output "stiffer" and more closely resembles an [ideal voltage source](@entry_id:276609), which by definition has zero [output impedance](@entry_id:265563). For a basic amplifier with open-loop [output resistance](@entry_id:276800) $R_o$ and a [loop gain](@entry_id:268715) of $T = A\beta$, the closed-loop [output resistance](@entry_id:276800) $R_{out,f}$ is given by:

$$R_{out,f} = \frac{R_o}{1 + T}$$

This reduction is a defining feature of topologies designed for voltage-output applications, as demonstrated in the analysis of voltage amplifiers and transresistance amplifiers [@problem_id:1337959] [@problem_id:1337898].

#### Series (Current) Sampling

To sample the output **current** ($i_o$), the feedback network must be connected in **series** with the load. This ensures that the entire load current flows through the sensing element of the feedback network.

In direct contrast to shunt sampling, series sampling **increases the output impedance**. The feedback loop now works to maintain a constant output current, irrespective of the voltage across the load. If the load impedance changes, the feedback adjusts the output voltage to ensure the current remains stable. This behavior is characteristic of an [ideal current source](@entry_id:272249), which has an infinite [output impedance](@entry_id:265563). The closed-loop [output resistance](@entry_id:276800) $R_{out,f}$ is increased by the same [feedback factor](@entry_id:275731):

$$R_{out,f} = R_o (1 + T)$$

This property is indispensable when designing an amplifier that must deliver a precise current to a variable load, a requirement for creating a high-quality [transconductance](@entry_id:274251) or [current amplifier](@entry_id:274238) [@problem_id:1337917].

### Input Mixing: Voltage Summation or Current Summation

After sampling the output, the feedback network produces a signal that must be combined with the external source signal at the input of the amplifier. This "mixing" can be performed by summing either voltages or currents.

#### Series (Voltage) Mixing

In **series mixing**, the feedback signal is a voltage ($v_f$) that is connected in series with the input signal source ($v_s$). This is typically accomplished within an input loop, such that the voltage appearing at the basic amplifier's input terminals, the error voltage $v_e$, is the difference between the source and feedback voltages:

$$v_e = v_s - v_f$$

Series mixing has the profound effect of **increasing the input impedance** of the amplifier. The feedback voltage effectively "cancels out" a portion of the input signal voltage that would normally appear across the amplifier's [finite input resistance](@entry_id:275363) $R_{in}$. This reduces the input current $i_{in}$ drawn from the source for a given source voltage $v_s$. Since input impedance is defined as $R_{in,f} = v_s / i_{in}$, a smaller input current for the same source voltage implies a larger [input impedance](@entry_id:271561). The increase is substantial, governed by the loop gain $T$:

$$R_{in,f} = R_{in} (1 + T)$$

This "impedance bootstrapping" is crucial for applications like buffers or instrument pre-amplifiers that must measure a voltage from a high-impedance source without loading it [@problem_id:1337917] [@problem_id:1337958]. It is the defining input characteristic of voltage-controlled amplifiers [@problem_id:1337942].

#### Shunt (Current) Mixing

In **shunt mixing**, the feedback signal is a current ($i_f$) that is combined with the input signal current ($i_s$) at a common node. The current that actually enters the basic amplifier, the error current $i_e$, is the difference between the source and feedback currents, in accordance with Kirchhoff's Current Law:

$$i_e = i_s - i_f$$

Shunt mixing acts to **decrease the [input impedance](@entry_id:271561)**. The feedback connection provides an alternative path for the input current, effectively shunting it away from the amplifier's input terminals. This phenomenon, often related to the Miller effect in specific circuit implementations, creates a virtual low-impedance point at the input. The input impedance is reduced by the loop gain factor:

$$R_{in,f} = \frac{R_{in}}{1 + T}$$

This low [input impedance](@entry_id:271561) is highly desirable when the signal source is itself a [current source](@entry_id:275668), such as a photodiode or a photomultiplier tube. A low input impedance ensures that nearly all of the signal current flows into the amplifier for processing rather than developing a voltage across the source's internal impedance [@problem_id:1337922].

### The Four Basic Topologies: A Systematic Classification

By combining the two types of input mixing with the two types of output sampling, we arrive at four fundamental [feedback topologies](@entry_id:261245). The standard naming convention is **(Input Mixing Type)-(Output Sampling Type)**. Each topology is optimized to create a specific type of ideal controlled source by tailoring the input and output impedances.

#### 1. Series-Shunt Feedback (Voltage Amplifier)

*   **Connections:** Series mixing at the input, shunt sampling at the output.
*   **Signals:** The input is a voltage ($v_s$) and the output is a voltage ($v_o$). The feedback network samples $v_o$ and returns a voltage $v_f$ to be subtracted from $v_s$.
*   **Impedances:** Input impedance is increased; output impedance is decreased.
*   **Ideal Model:** This topology creates a **Voltage-Controlled Voltage Source (VCVS)**, or a voltage amplifier. Its high input impedance prevents loading of the source, and its low output impedance allows it to drive various loads without its voltage changing [@problem_id:1337918].
*   **Gain Analysis:** The closed-[loop gain](@entry_id:268715) is a voltage ratio, $A_f = v_o / v_s$. In the standard formula $A_f = A / (1 + A\beta)$, the open-loop gain $A$ is the amplifier's voltage gain ($v_o/v_e$), and the [feedback factor](@entry_id:275731) $\beta$ is the feedback network's voltage ratio ($v_f/v_o$). Both $A$ and $\beta$ are dimensionless quantities [@problem_id:1337938]. The classic non-inverting operational amplifier configuration is a prime example of this topology [@problem_id:1337958] [@problem_id:1337959].

#### 2. Shunt-Shunt Feedback (Transresistance Amplifier)

*   **Connections:** Shunt mixing at the input, shunt sampling at the output.
*   **Signals:** The input is a current ($i_s$) and the output is a voltage ($v_o$). The feedback network samples $v_o$ and returns a current $i_f$ to be subtracted from $i_s$.
*   **Impedances:** Both input and output impedances are decreased.
*   **Ideal Model:** This topology creates a **Current-Controlled Voltage Source (CCVS)**, more commonly known as a [transresistance amplifier](@entry_id:275441). Its low input impedance is ideal for a [current source](@entry_id:275668) input, and its low output impedance provides a stable voltage output [@problem_id:1337922]. A common implementation is an op-amp with a resistor from the output to the inverting input, often used in [optical power](@entry_id:170412) meters.
*   **Gain Analysis:** The closed-[loop gain](@entry_id:268715) is a transresistance, $R_{mf} = v_o / i_s$. Here, the open-loop gain $A$ is a transresistance ($v_o/i_e$) with units of Ohms, and the [feedback factor](@entry_id:275731) $\beta$ is a [transconductance](@entry_id:274251) ($i_f/v_o$) with units of Siemens. Their product, the loop gain $A\beta$, remains dimensionless. A BJT amplifier with a feedback resistor from collector to base exemplifies this topology [@problem_id:1337936].

#### 3. Series-Series Feedback (Transconductance Amplifier)

*   **Connections:** Series mixing at the input, series sampling at the output.
*   **Signals:** The input is a voltage ($v_s$) and the output is a current ($i_o$). The feedback network samples $i_o$ and returns a voltage $v_f$ to be subtracted from $v_s$.
*   **Impedances:** Both input and output impedances are increased.
*   **Ideal Model:** This topology creates a **Voltage-Controlled Current Source (VCCS)**, or a [transconductance amplifier](@entry_id:266314). The high [input impedance](@entry_id:271561) is suitable for a voltage source, and the high output impedance makes it an excellent [current source](@entry_id:275668), capable of delivering a constant current regardless of the load [@problem_id:1337917].
*   **Gain Analysis:** The closed-[loop gain](@entry_id:268715) is a transconductance, $G_{mf} = i_o / v_s$. The open-[loop gain](@entry_id:268715) $A$ is a transconductance ($i_o/v_e$), and the [feedback factor](@entry_id:275731) $\beta$ is a transresistance ($v_f/i_o$). Again, the [loop gain](@entry_id:268715) $A\beta$ is dimensionless.

#### 4. Shunt-Series Feedback (Current Amplifier)

*   **Connections:** Shunt mixing at the input, series sampling at the output.
*   **Signals:** The input is a current ($i_s$) and the output is a current ($i_o$). The feedback network samples $i_o$ and returns a current $i_f$ to be subtracted from $i_s$.
*   **Impedances:** Input impedance is decreased; [output impedance](@entry_id:265563) is increased.
*   **Ideal Model:** This topology creates a **Current-Controlled Current Source (CCCS)**, or a [current amplifier](@entry_id:274238). It is designed to take an input current signal and deliver a proportional output current from a high-impedance output, making it ideal for current boosting applications.
*   **Gain Analysis:** The closed-[loop gain](@entry_id:268715) is a current ratio, $A_{if} = i_o / i_s$. For this topology, the open-loop gain $A$ is a [current gain](@entry_id:273397) ($i_o/i_e$), and the [feedback factor](@entry_id:275731) $\beta$ is a current ratio ($i_f/i_o$). Both are dimensionless.

The relationship between the four topologies and their corresponding [ideal amplifier](@entry_id:260682) models is a cornerstone of feedback analysis [@problem_id:1337950]. By selecting the appropriate topology, an engineer can transform a general-purpose, non-ideal amplifying block into a specialized circuit that approaches an ideal VCVS, CCVS, VCCS, or CCCS, tailored precisely to the demands of the application.