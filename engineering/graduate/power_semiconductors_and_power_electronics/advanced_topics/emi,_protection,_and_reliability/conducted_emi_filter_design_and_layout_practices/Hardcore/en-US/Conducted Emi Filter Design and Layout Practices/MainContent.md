## Introduction
In modern power electronics, the quest for higher efficiency and power density has driven the adoption of high-frequency switching. While beneficial, this rapid switching is the primary source of conducted electromagnetic interference (EMI)—unwanted high-frequency noise that propagates along power lines. This noise can disrupt the operation of the device itself and other nearby electronics, making its mitigation a critical requirement for regulatory compliance and [system reliability](@entry_id:274890). Addressing conducted EMI is not merely an act of adding components; it is a systematic design discipline that integrates circuit theory, magnetics, and a deep understanding of high-frequency parasitic effects.

This article provides a comprehensive guide to the design and implementation of conducted EMI filters. The first chapter, **Principles and Mechanisms**, delves into the fundamental theory, deconstructing noise into its differential and common modes and analyzing the behavior of filter components, including their non-ideal parasitic effects. The second chapter, **Applications and Interdisciplinary Connections**, shifts to practical implementation, exploring diagnostic techniques, source mitigation strategies like optimized PCB layout, and system-level considerations such as stability and advanced modulation schemes. Finally, the **Hands-On Practices** section offers targeted exercises to solidify your understanding of noise separation, attenuation requirements, and the crucial impact of system impedances on filter performance.

## Principles and Mechanisms

The design of effective conducted EMI filters is a discipline that marries fundamental circuit theory with a deep appreciation for the non-ideal behavior of components and the pervasive influence of physical layout. This chapter elucidates the core principles and mechanisms governing the generation, propagation, and mitigation of conducted electromagnetic interference in power electronic systems. We will deconstruct the problem into its [canonical forms](@entry_id:153058), analyze the components of a solution, and explore the practical limitations that define the boundaries of filter performance.

### Noise Modes: Differential and Common-Mode

Conducted emissions measured at the mains interface of a power converter manifest as radio-frequency (RF) currents flowing in the power conductors. These emissions are not monolithic; they can be systematically decomposed into two fundamental modes: **differential-mode (DM)** and **common-mode (CM)** noise. This decomposition is essential because the mitigation strategies for each mode are distinct. The distinction arises from the different paths these currents take.

Consider a standard two-conductor system (Line and Neutral) connected to a power converter, with a chassis referenced to Protective Earth (PE). The measurement apparatus, a Line Impedance Stabilization Network (LISN), provides a standardized impedance, typically $50\,\Omega$, from each conductor to earth.

**Differential-mode noise** is characterized by RF currents that circulate between the line and neutral conductors. At any instant, the DM current on the line, $i_{DM}(t)$, is equal in magnitude and opposite in direction to the current on the neutral, $-i_{DM}(t)$. This [current loop](@entry_id:271292) is confined to the power conductors themselves. To suppress DM noise, we must increase the impedance of this loop or provide a low-impedance path to shunt the current before it reaches the LISN. This is the role of **series inductors** (or differential-mode chokes) placed in the line and neutral conductors and **Class X capacitors** (or X-capacitors) placed directly across the line and neutral conductors .

**Common-mode noise**, in contrast, consists of RF currents that flow in the same direction—in phase—on both the line and neutral conductors, $i_{CM}(t)$. By Kirchhoff's Current Law, these currents cannot return via the power conductors. Instead, their return path is through displacement currents flowing via parasitic capacitances from the converter's internal circuits and chassis to the surrounding environment and, ultimately, back to the source via the earth connection provided by the LISN. To mitigate CM noise, we must impede this common-mode path or provide a more favorable, localized return path. This is achieved using a **[common-mode choke](@entry_id:1122686)**, which presents a high impedance to in-phase currents, and **Class Y capacitors** (or Y-capacitors), which are connected from each power conductor to the chassis/earth, shunting the CM currents away from the LISN .

### Physical Origins of Conducted Noise

The DM and CM noise currents are not arbitrary; they are direct consequences of the fast-switching operation inherent to modern power converters. The high rates of change of voltage ($\mathrm{d}v/\mathrm{d}t$) and current ($\mathrm{d}i/\mathrm{d}t$) interact with parasitic inductances and capacitances within the converter's physical structure to generate these noise sources.

The dominant source of **[differential-mode noise](@entry_id:1123677)** is typically the rapid change of current, $\mathrm{d}i/\mathrm{d}t$, in high-frequency current loops, such as the input loop of a DC-DC converter. Every physical loop possesses a small but finite stray inductance, $L_s$. The time-varying current induces a noise voltage, $v_{DM} = L_s \frac{\mathrm{d}i}{\mathrm{d}t}$, in series with the loop. This can be modeled as a Thevenin voltage source driving DM current into the power lines. For instance, an input loop with a residual inductance of $L_s = 30\,\mathrm{nH}$ and a current slew rate of $\mathrm{d}i/\mathrm{d}t = 100\,\mathrm{A}/\mu\mathrm{s}$ generates a DM noise voltage source of $3.0\,\mathrm{V}$, which can drive significant current into the $100\,\Omega$ differential impedance of a LISN .

The dominant source of **[common-mode noise](@entry_id:269684)** is the high rate of change of voltage, $\mathrm{d}v/\mathrm{d}t$, on switching nodes that have parasitic capacitance to a common reference plane like the chassis or a heatsink. A prime example is the switch node of a half-bridge, which experiences rapid voltage swings. This voltage acts across the parasitic capacitance, $C_p$, (e.g., between a device's drain tab and its earthed heatsink) to inject a displacement current, $i_{CM} = C_p \frac{\mathrm{d}v}{\mathrm{d}t}$, into the chassis. This can be modeled as a Norton current source that injects current into the earth reference, which then returns through the LISN. A modest parasitic capacitance of $C_{p} = 50\,\mathrm{pF}$ exposed to a slew rate of $\mathrm{d}v/\mathrm{d}t = 5\,\mathrm{V/ns}$ generates a CM current source of $250\,\mathrm{mA}$, often making CM noise the dominant mode at higher frequencies .

### Filter Performance and Insertion Loss

The effectiveness of an EMI filter is quantified by its **insertion loss (IL)**, defined as the ratio of the noise voltage at the load *without* the filter to the noise voltage *with* the filter, expressed in decibels:

$IL(f) = 20\log_{10}\! \left( \left| \frac{V_{\text{noise, unfiltered}}(f)}{V_{\text{noise, filtered}}(f)} \right| \right)$

It is a critical error to assume that insertion loss is an intrinsic property of the filter itself. By modeling the filter as a generic two-port network with ABCD parameters, and with a source impedance $Z_s$ and load impedance $Z_L$, the insertion loss can be derived as:

$IL(f) = 20\log_{10}\!\left(\left|\frac{Z_L}{Z_s + Z_L}\right| \cdot \left|A + \frac{B}{Z_L} + Z_s C + \frac{Z_s D}{Z_L}\right|\right)$

This expression explicitly shows that the filter's performance depends fundamentally on the impedances of the source and load it is connected between . In the specific and standardized context of conducted EMI testing, the source impedance is defined by the LISN (typically $50\,\Omega$ per line), but the load impedance (the converter's [input impedance](@entry_id:271561)) can be complex and frequency-dependent.

For analysis purposes, it is common to evaluate filters in a matched $Z_0$ system (e.g., $50\,\Omega$), where $Z_s = Z_L = Z_0$. In this special case, the insertion loss simplifies and can be related directly to the filter's forward transmission scattering parameter, $S_{21}$:

$IL(f) = -20\log_{10}|S_{21}(f)|$

where $S_{21}$ is the complex ratio of the voltage wave delivered at the output port to the voltage wave incident on the input port. A higher insertion loss corresponds to a smaller $|S_{21}|$, signifying greater attenuation. This relationship provides a powerful link between filter performance and standard RF network analysis techniques .

### Common-Mode Filter Design and Constraints

A common-mode filter stage consists of a CM choke providing series impedance and Y-capacitors providing a shunt path to earth.

The **[common-mode choke](@entry_id:1122686)** is a masterful example of applied magnetics. It consists of two or more windings on a single high-permeability magnetic core. The windings are oriented such that for differential-mode currents (equal and opposite), the magnetic fluxes they produce in the core cancel each other out. This prevents the core from saturating under the large 50/60 Hz [line current](@entry_id:267326) and results in a very low impedance path, characterized by the small **leakage inductance**, $L_{leak} = L - M$, where $L$ is the [self-inductance](@entry_id:265778) of one winding and $M$ is the [mutual inductance](@entry_id:264504). For common-mode currents (equal and in-phase), the fluxes add, magnetizing the core and producing a very high impedance. The effective inductance seen by CM currents on each line is the **magnetizing inductance**, $L_{CM} = L + M$. For a tightly coupled choke where the [coupling coefficient](@entry_id:273384) $k \approx 1$ and $M \approx L$, the CM inductance approaches $2L$ while the DM inductance approaches zero. This selective impedance is the key to its function: it strongly attenuates CM noise while being transparent to the desired DM power flow .

The **Y-capacitors** complete the CM filter by providing a low-impedance path to shunt the CM currents from the lines to the chassis/earth. However, their size is not limited by filtering requirements, but by stringent safety standards. These capacitors bridge the safety isolation barrier between the user-accessible chassis and the hazardous mains voltage. At the mains frequency (50/60 Hz), they conduct a continuous displacement current to the protective earth conductor. This current, known as **leakage current** or protective conductor current, can pose a shock hazard if the earth connection is lost.

International safety standards, such as IEC 60335 for household appliances and IEC 62368 for IT equipment, place strict limits on this current (e.g., $0.75\,\mathrm{mA}$ and $3.5\,\mathrm{mA}$, respectively). For a [worst-case analysis](@entry_id:168192) where the full mains voltage $V_{rms}$ is applied across two parallel Y-capacitors of value $C_Y$, the total RMS leakage current is $I_{PE,rms} = V_{rms} \cdot 2\pi f \cdot (2C_Y)$. This relationship imposes a hard ceiling on the maximum allowable Y-capacitance. For example, to meet a $0.75\,\mathrm{mA}$ limit at $240\,\mathrm{V_{rms}}$, $60\,\mathrm{Hz}$, the total Y-capacitance is limited to approximately $8.3\,\mathrm{nF}$ (or $4.15\,\mathrm{nF}$ per capacitor) . This capacitance constraint directly limits the filter's low-frequency CM attenuation, as the shunt impedance $Z_Y = 1/(j\omega C_Y)$ cannot be made arbitrarily low.

### Differential-Mode Filter Design

A typical differential-mode filter stage is a second-order low-pass LC filter, comprising series inductors and a shunt X-capacitor across the lines. The design objective is to achieve a desired attenuation over the regulatory frequency band, which for most standards begins at $150\,\mathrm{kHz}$ .

The core principle is **[impedance mismatch](@entry_id:261346)**. The filter is designed such that its corner frequency, $f_c = 1/(2\pi\sqrt{L_{total}C_X})$, is placed well below the start of the band of interest (i.e., $f_c \lt 150\,\mathrm{kHz}$). Above this corner frequency, the filter enters its [stopband](@entry_id:262648). Here, the series impedance of the inductors, $|Z_L| = \omega L_{total}$, rises with frequency, while the shunt impedance of the capacitor, $|Z_C| = 1/(\omega C_X)$, falls with frequency. This combination of a high series impedance and a low shunt impedance provides effective attenuation. The resulting transfer function exhibits a characteristic $-40\,\mathrm{dB/decade}$ attenuation slope, providing broad and increasing suppression across the frequency band . Designing the filter without this impedance overlap (e.g., relying only on a capacitor) would result in a much shallower first-order ($-20\,\mathrm{dB/decade}$) slope.

### The Impact of Non-Idealities and Layout

An EMI filter schematic is an idealization. At the high frequencies relevant to EMI, the performance of a real filter is dominated by parasitic elements inherent to the components and the physical layout of the printed circuit board (PCB).

#### Component Self-Resonance

Every real component has a **[self-resonant frequency](@entry_id:265549) (SRF)** where its behavior deviates from the ideal.

A **capacitor** possesses parasitic equivalent series inductance (ESL) and [equivalent series resistance](@entry_id:275904) (ESR). Its impedance is $Z_C(\omega) = R_{ESR} + j\omega L_{ESL} + 1/(j\omega C)$. At the SRF, $f_{SRF,C} = 1/(2\pi\sqrt{L_{ESL}C})$, the inductive and capacitive reactances cancel, and the impedance reaches a minimum value equal to the ESR. Above its SRF, the capacitor behaves as an inductor, with its impedance rising with frequency. This fundamentally limits the performance of a shunt element, as its impedance no longer falls at high frequencies  .

An **inductor** possesses parasitic inter-winding capacitance ($C_p$) and winding resistance. Its impedance model is a [parallel resonance](@entry_id:262383). At its SRF, $f_{SRF,L} \approx 1/(2\pi\sqrt{LC_p})$, its impedance peaks. Above this frequency, it behaves as a capacitor, with its impedance falling with frequency. This undermines its role as a series blocking element.

A crucial [filter design](@entry_id:266363) rule is to select components whose SRFs lie **above** the highest frequency of interest (e.g., $> 30\,\mathrm{MHz}$). This ensures the components behave as intended across the entire regulatory band .

#### Layout Parasitics

The PCB layout is not a benign interconnect; it is an active circuit element at high frequencies.
- **Parasitic Inductance:** Every trace, via, and component lead has inductance. The inductance of a via connecting a shunt capacitor to its return plane, $L_v$, can form an unintended [series resonance](@entry_id:268839) with the capacitor $C$. This creates an impedance peak at $f_{res} = 1/(2\pi\sqrt{L_v C})$, turning the intended low-impedance shunt into a high-impedance path and creating a major hole in the filter's attenuation profile . Minimizing trace lengths and using multiple vias in parallel are critical techniques to reduce this parasitic inductance and push such resonances to higher frequencies.
- **Parasitic Capacitance:** Stray capacitance between the input and output nodes of a filter creates a high-frequency "sneak path" that allows noise to bypass the filter entirely. This parasitic coupling places a ceiling on the maximum achievable attenuation, or "[stopband](@entry_id:262648) floor," regardless of how ideal the filter components are . Physical separation and shielding between filter stages are essential to maximize isolation.
- **Mutual Coupling:** Magnetic fields from filter inductors can couple to each other if they are placed too closely. This [mutual inductance](@entry_id:264504), $M$, alters the behavior of multi-stage filters, collapsing their intended high-order response and potentially creating unexpected resonant peaks . Orienting adjacent inductors at 90 degrees to each other is a common practice to minimize this coupling.
- **Shared Impedance Coupling:** If the return current from a [filter capacitor](@entry_id:271169) shares a segment of PCB trace with another current loop, the voltage developed across the impedance of that shared trace ($V_{noise} = I_{return} \cdot Z_{trace}$) will be injected as noise. This is a common failure mode. The solution is to use dedicated return paths, often called **Kelvin connections**, to ensure that sensitive filter return points connect directly to a single, quiet reference point .

### System-Level Interaction: Filter Stability

An EMI filter cannot be designed in isolation. It forms a subsystem that interacts with the power converter it is attached to. A switching converter operating with a closed-[loop voltage](@entry_id:1127453) regulator often presents a **negative incremental [input impedance](@entry_id:271561)** over a certain frequency range. This means that when the input voltage increases, the input current decreases, as the converter adjusts its duty cycle to maintain a constant output power.

When an LC filter, which has a resonant peak in its output impedance $Z_s$, is connected to a converter with [input impedance](@entry_id:271561) $Z_{in,conv}$, the combination can become unstable and oscillate. This interaction can be modeled as a minor feedback loop with a [loop gain](@entry_id:268715) of $T(j\omega) = Z_s(j\omega) / Z_{in,conv}(j\omega)$. The system will oscillate if the Nyquist criterion is violated—that is, if $T(j\omega)$ encircles the -1 point in the complex plane.

The **Middlebrook stability criterion** provides a conservative but robust design rule to prevent this oscillation: the magnitude of the source impedance must be kept much smaller than the magnitude of the converter's input impedance at all frequencies.

$|Z_s(j\omega)| \ll |Z_{in,conv}(j\omega)|$

This is equivalent to requiring the loop gain magnitude $|T(j\omega)| \ll 1$. By keeping the [loop gain](@entry_id:268715) small, we ensure a large stability margin, preventing the denominator of the system's closed-[loop transfer function](@entry_id:274447), $1+T(j\omega)$, from approaching zero. This rule is most critical near the filter's resonant frequency, where $|Z_s(j\omega)|$ is at its maximum. Proper damping of the filter's resonance is therefore essential not only for its own performance but for the stability of the entire system .