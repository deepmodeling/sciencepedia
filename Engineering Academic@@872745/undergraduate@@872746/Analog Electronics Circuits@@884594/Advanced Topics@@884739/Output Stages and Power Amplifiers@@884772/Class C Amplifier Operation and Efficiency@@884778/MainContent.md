## Introduction
In the world of radio-frequency (RF) engineering, maximizing power efficiency is a paramount goal. The Class C amplifier stands out as a cornerstone of high-power RF systems, renowned for its ability to convert DC supply power into RF [signal power](@entry_id:273924) with minimal waste. However, this remarkable efficiency comes at the cost of high non-linearity, a critical trade-off that defines its applications and design challenges. This article provides a comprehensive exploration of the Class C amplifier, bridging the gap between its fundamental theory and practical implementation.

To achieve this, our journey is structured into three chapters. We begin with **Principles and Mechanisms**, where we will dissect the pulsed conduction mode and the [resonant tank circuit](@entry_id:271853) that are central to its operation and high efficiency. Next, **Applications and Interdisciplinary Connections** will showcase how these properties are exploited in RF transmitters, frequency multipliers, and advanced architectures like Doherty and Envelope Tracking amplifiers. Finally, the **Hands-On Practices** section offers practical problems to reinforce these key concepts. This structured approach will equip you with a robust understanding of why and how the Class C amplifier remains a vital component in modern communication technology.

## Principles and Mechanisms

This chapter delves into the fundamental principles and operational mechanisms of Class C amplifiers. Building upon the introductory concepts, we will dissect the unique characteristics that distinguish this amplifier class, focusing on the interplay between its pulsed conduction mode, the resonant output network, and its resulting high efficiency. Our exploration will be both qualitative and quantitative, providing the analytical tools necessary for the design and evaluation of these critical radio-frequency (RF) circuits.

### The Principle of Pulsed Conduction

The defining characteristic of a **Class C amplifier** is its biasing condition. Unlike Class A or Class B amplifiers, the active device—be it a Bipolar Junction Transistor (BJT) or a Field-Effect Transistor (FET)—is biased deep into its **[cutoff region](@entry_id:262597)**. This means that for a sinusoidal input signal, the transistor remains completely non-conductive for a significant majority of the input cycle. Conduction only occurs when the peak of the input signal swings far enough to overcome the [reverse bias](@entry_id:160088) and forward-bias the device's control junction (the base-emitter junction for a BJT or the gate-source junction for a FET).

This mode of operation results in a collector or drain current that flows in short, periodic pulses. The duration of each pulse relative to the total period of the input signal is defined by the **[conduction angle](@entry_id:271144)**, denoted as $2\theta_c$. For Class C operation, the [conduction angle](@entry_id:271144) is, by definition, less than 180 degrees ($\pi$ [radians](@entry_id:171693)). The smaller the [conduction angle](@entry_id:271144), the narrower the current pulses.

This pulsed conduction immediately reveals a critical trade-off. Because the output current waveform is a series of pulses and not a scaled replica of the sinusoidal input, the Class C amplifier is a highly **non-linear** device. It introduces severe distortion. For instance, consider a hypothetical amplifier that only produces an output when the input sine wave is positive and exceeds 60% of its peak value. A simple calculation reveals that such an amplifier would produce zero output for over 70% of the input cycle [@problem_id:1289655]. This extreme distortion makes Class C amplifiers entirely unsuitable for applications requiring high fidelity, such as audio amplification or the amplification of amplitude-modulated (AM) signals where the information is encoded in the signal's envelope. Instead, their utility is found in applications where the input signal has a constant envelope, such as in [frequency modulation](@entry_id:162932) (FM) or continuous wave (CW) transmitters.

### The Resonant Tank Circuit and the Flywheel Effect

If the amplifier's output current consists of sharp pulses, how is a useful, continuous sinusoidal output voltage generated? The answer lies in the load connected to the collector or drain, which is not a simple resistor but a parallel **resonant LC [tank circuit](@entry_id:261916)**. This circuit is fundamental to the operation of a Class C amplifier and performs two critical functions: frequency selection and waveform restoration.

First, the [tank circuit](@entry_id:261916) acts as a high-quality [band-pass filter](@entry_id:271673). The impedance of a parallel LC circuit is maximized at its **[resonant frequency](@entry_id:265742)**, $f_0 = \frac{1}{2\pi\sqrt{LC}}$, and falls off sharply at other frequencies. The current pulses from the transistor are rich in harmonics—integer multiples of the fundamental input frequency. When these pulses drive the [tank circuit](@entry_id:261916), the circuit presents a high impedance only to the frequency component at or near $f_0$. All other harmonic components see a very low impedance and are effectively shunted to ground. Thus, the [tank circuit](@entry_id:261916) is primarily responsible for selecting the desired carrier frequency for transmission and rejecting all unwanted harmonics [@problem_id:1289679].

The second function, waveform restoration, is elegantly described by the **[flywheel](@entry_id:195849) effect**. The most direct way to visualize this phenomenon is to imagine plotting the transistor's collector current and the voltage across the output load on the same time axis [@problem_id:1289676]. One would observe sharp, narrow pulses of current periodically "kicking" the [tank circuit](@entry_id:261916), and in response, the [tank circuit](@entry_id:261916) would produce a smooth, continuous sinusoidal voltage.

This effect can be understood from an energy perspective. During the brief conduction interval, the current pulse delivers a packet of energy to the [tank circuit](@entry_id:261916), storing it in the electric and magnetic fields of the capacitor and inductor. When the transistor turns off, this stored energy is not lost but oscillates back and forth between the inductor and capacitor. This sustained oscillation, analogous to a mechanical [flywheel](@entry_id:195849) that maintains its rotation between pushes, "fills in the gaps" between the current pulses, thereby reconstructing a full sinusoidal voltage waveform at the output. The quality of this reconstructed sine wave depends on the **[quality factor](@entry_id:201005) (Q)** of the [tank circuit](@entry_id:261916). A higher Q means less energy is dissipated per cycle, resulting in a purer sinusoid. The average energy, $\langle W \rangle$, stored in the tank is related to the output power, $P_{out}$, and the quality factor, $Q$, by the fundamental definition of Q for a resonator:

$$ Q = \omega_0 \frac{\langle W \rangle}{P_{out}} $$

where $\omega_0 = 2\pi f_0$ is the resonant angular frequency. This relationship allows an engineer to calculate the [energy storage](@entry_id:264866) required for a given output power and Q-factor [@problem_id:1289707].

Furthermore, the Q-factor directly determines the **bandwidth** of the amplifier. For a high-Q [resonant circuit](@entry_id:261776), the 3-dB bandwidth, $\Delta f$, is given by:

$$ \Delta f = \frac{f_c}{Q} $$

where $f_c$ is the center frequency. This relationship is crucial for ensuring that the amplifier's [passband](@entry_id:276907) is narrow enough to filter harmonics effectively, yet wide enough to accommodate the desired signal's bandwidth, for instance, within a designated amateur radio band [@problem_id:1289684].

### Analysis of Collector Efficiency

The primary motivation for using a Class C amplifier is its potential for extremely high efficiency. The **collector efficiency** (or drain efficiency for a FET), $\eta_c$, is defined as the ratio of the AC power delivered to the load to the DC power drawn from the supply:

$$ \eta_c = \frac{P_{out}}{P_{DC}} $$

The DC power drawn from the supply, which has a constant voltage $V_{CC}$, is given by $P_{DC} = V_{CC} I_{DC}$, where $I_{DC}$ is the average (DC component) of the pulsed collector current. The AC output power, delivered at the fundamental frequency, is $P_{out} = \frac{1}{2} V_{peak} I_1$, where $V_{peak}$ is the peak amplitude of the sinusoidal output voltage and $I_1$ is the peak amplitude of the fundamental frequency component of the collector current. Under ideal conditions for maximum power, the output voltage swings from $V_{CC}$ down to a saturation voltage of nearly 0 V, making the peak AC voltage amplitude $V_{peak} \approx V_{CC}$. With this assumption, the efficiency simplifies to:

$$ \eta_c = \frac{\frac{1}{2} V_{CC} I_1}{V_{CC} I_{DC}} = \frac{1}{2} \frac{I_1}{I_{DC}} $$

If we express the power in terms of RMS values, where $I_{p1}$ is the RMS value of the fundamental current ($I_1 = \sqrt{2}I_{p1}$), the efficiency can also be written as $\eta_c = \frac{I_{p1}}{\sqrt{2} I_{DC}}$ [@problem_id:1289666]. Both expressions show that efficiency is fundamentally determined by the ratio of the fundamental component of the current to its DC component.

To find this ratio, we must use Fourier analysis. Let's model the collector current pulses, centered at phase angle $\phi = 0$, as a clipped cosine wave that is non-zero only for $-\theta_c \le \phi \le \theta_c$ [@problem_id:1289673]:

$$ i_C(\phi) = \begin{cases} I_{C,max} (\cos(\phi) - \cos(\theta_c))  \text{for } -\theta_c \le \phi \le \theta_c \\ 0  \text{otherwise} \end{cases} $$

The DC component, $I_{DC}$, is the average value of this waveform over a full cycle:
$$ I_{DC} = \frac{1}{2\pi} \int_{-\theta_c}^{\theta_c} i_C(\phi) \,d\phi = \frac{I_{C,max}}{\pi}(\sin\theta_c - \theta_c\cos\theta_c) $$

The amplitude of the fundamental component, $I_1$, is found from the Fourier series coefficient for the first harmonic:
$$ I_1 = \frac{1}{\pi} \int_{-\theta_c}^{\theta_c} i_C(\phi) \cos(\phi) \,d\phi = \frac{I_{C,max}}{\pi}(\theta_c - \sin\theta_c\cos\theta_c) $$

Substituting these into the efficiency formula yields a remarkable result that depends only on the half-[conduction angle](@entry_id:271144) $\theta_c$ (in radians):

$$ \eta_c = \frac{1}{2} \frac{I_1}{I_{DC}} = \frac{1}{2} \cdot \frac{\theta_c - \sin\theta_c\cos\theta_c}{\sin\theta_c - \theta_c\cos\theta_c} $$

This equation is central to understanding Class C performance. It shows that as the [conduction angle](@entry_id:271144) $2\theta_c$ is made smaller, the efficiency $\eta_c$ increases, approaching a theoretical maximum of 100% as $\theta_c \to 0$. This is because a narrower pulse contains proportionally more harmonic energy and less DC energy relative to its fundamental component. For instance, for a total [conduction angle](@entry_id:271144) of $2\theta_c = \frac{\pi}{2}$ [radians](@entry_id:171693) (i.e., $\theta_c = \frac{\pi}{4}$), the theoretical efficiency is approximately 0.940, or 94% [@problem_id:1289677]. The same analytical approach can be applied to other device models, such as a MOSFET with a square-law characteristic, yielding similarly high efficiencies that depend on the device parameters and bias conditions [@problem_id:1289718].

### Practical Biasing and Input Characteristics

Establishing the deep cutoff bias for a Class C amplifier can be done with a fixed negative voltage supply connected to the base [or gate](@entry_id:168617). However, a more common and elegant technique is **self-biasing**. In this configuration, the input AC signal is coupled to the base via a capacitor, and there is no DC path from the base to ground.

During the first few positive cycles of the input signal, the base-emitter junction becomes forward-biased and draws current, charging the [coupling capacitor](@entry_id:272721). This charging action creates a DC voltage across the capacitor with a polarity that reverse-biases the junction. An equilibrium is quickly reached where the capacitor holds a steady DC voltage, $V_{bias}$, that is just large enough to allow only the positive peaks of the input signal to turn the transistor on. The base voltage is effectively "clamped" at the turn-on voltage, $V_{BE(on)}$. The DC bias voltage established is $V_{bias} = V_{in,peak} - V_{BE(on)}$. This self-generated bias voltage forces the transistor into Class C operation without requiring a separate negative power supply. An important design consideration arises from this: during the negative swing of the input signal, the base-emitter junction experiences a maximum [reverse bias](@entry_id:160088) of $2V_{in,peak} - V_{BE(on)}$. The transistor must be chosen to withstand this voltage without breaking down [@problem_id:1289654].

Finally, it is crucial to recognize that the input of a Class C amplifier presents a highly **non-linear load** to its preceding driver stage. The input draws current only during the brief conduction intervals at the peak of the input swing. For the rest of the cycle, it presents a very high impedance. A driver amplifier designed to drive a constant resistive load may fail to perform correctly. For design and [impedance matching](@entry_id:151450) purposes, it is useful to calculate the **effective [input resistance](@entry_id:178645)**, $R_{in}$, at the fundamental frequency. This is defined as the ratio of the amplitude of the fundamental input voltage to the amplitude of the fundamental component of the input current. This calculation, which again relies on Fourier analysis of the pulsed input current, provides the equivalent linear resistance that the driver "sees" at the operating frequency, enabling proper matching for maximum power transfer [@problem_id:1289661].