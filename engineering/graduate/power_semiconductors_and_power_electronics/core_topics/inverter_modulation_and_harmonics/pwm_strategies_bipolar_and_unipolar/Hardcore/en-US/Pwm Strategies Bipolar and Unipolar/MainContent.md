## Introduction
Pulse Width Modulation (PWM) is a cornerstone technique in modern power electronics, enabling the precise and efficient control of power converters. For single-phase inverters, which are ubiquitous in applications ranging from renewable energy systems to uninterruptible power supplies, the choice of PWM strategy is a critical design decision with far-reaching consequences for system efficiency, cost, and performance. The two most fundamental carrier-based approaches, bipolar and unipolar PWM, present distinct operational characteristics and performance trade-offs.

This article addresses the crucial knowledge gap between the theoretical principles of these PWM strategies and their practical implications in real-world systems. It provides a comprehensive comparative analysis to equip engineers and researchers with the understanding needed to select and optimize the modulation scheme for a given application.

Across the following chapters, you will gain a deep understanding of these methods. The first chapter, **Principles and Mechanisms**, will derive the operational fundamentals of both bipolar and unipolar PWM from first principles, comparing their output characteristics and harmonic spectra. The second chapter, **Applications and Interdisciplinary Connections**, will explore the profound impact of this choice on hardware design, electromagnetic interference (EMI), and digital [control [system stabilit](@entry_id:271437)y](@entry_id:148296). Finally, the **Hands-On Practices** section provides targeted problems to solidify your understanding and apply these concepts to practical scenarios.

## Principles and Mechanisms

This chapter delineates the fundamental principles and operational mechanisms of carrier-based Pulse Width Modulation (PWM), focusing on the two predominant strategies for single-phase voltage source inverters: bipolar and unipolar PWM. We will derive the operational characteristics of each strategy from first principles, compare their performance, and analyze their behavior under both linear and nonlinear modulation conditions.

### The Foundation of Carrier-Based PWM

At its core, carrier-based PWM is a technique for encoding a low-frequency analog signal into a high-frequency digital pulse train. The width of the pulses in this train is modulated such that their average value over a switching period tracks the desired low-frequency signal. This process is most commonly achieved by comparing the desired analog signal, termed the **reference** or **modulating signal** ($v_{ref}(t)$), with a high-frequency periodic waveform, known as the **carrier signal** ($v_c(t)$).

For sinusoidal PWM (SPWM), the reference is a sinusoid, $v_{ref}(t) = V_m \sin(\omega_m t)$, where $V_m$ is the peak amplitude and $\omega_m$ is the desired fundamental angular frequency. The carrier is typically a symmetric triangular wave of a much higher frequency, $\omega_c \gg \omega_m$, with a peak amplitude of $V_c$. The output of the comparator is high when $v_{ref}(t) \ge v_c(t)$ and low otherwise. This method of determining the switching instants based on the real-time intersection of the two waveforms is known as **natural sampling**.

Under the valid assumption that $v_{ref}(t)$ is approximately constant over a single carrier period $T_c = 2\pi/\omega_c$, we can establish a direct relationship between the reference voltage and the **duty ratio**, $D(t)$. The duty ratio is the fraction of the carrier period for which the PWM output is in the high state. For a symmetric triangular carrier oscillating between $-V_c$ and $+V_c$, a straightforward [geometric analysis](@entry_id:157700) of the intersection points reveals that the [duty ratio](@entry_id:199172) is a linear function of the instantaneous reference voltage . For a non-inverting comparator, this relationship is:

$$
D(t) = \frac{1}{2} + \frac{v_{ref}(t)}{2V_c}
$$

This equation is fundamental to understanding how PWM linearizes the otherwise nonlinear behavior of a switching converter. The local average of the switched output is directly proportional to the duty ratio, and thus, to the reference signal.

The ratio of the reference signal's peak amplitude to the carrier's peak amplitude is a critical parameter known as the **modulation index**, $m_a$:

$$
m_a = \frac{V_m}{V_c}
$$

For the linear relationship between $v_{ref}$ and $D(t)$ to hold throughout the fundamental cycle, the reference signal must remain within the bounds of the carrier, i.e., $|v_{ref}(t)| \le V_c$. This condition is satisfied when $m_a \le 1$, which defines the **linear modulation range** . Operation with $m_a > 1$ is termed **[overmodulation](@entry_id:1129249)** and introduces nonlinear distortion, as will be discussed later.

### Bipolar PWM Strategy

In a single-phase full-bridge inverter, the bipolar PWM strategy employs a single comparator whose output dictates the state of all four switches. The two legs of the inverter, A and B, are driven complementarily. When leg A is connected to the positive DC rail, leg B is connected to the negative DC rail, and vice versa. This coordination is achieved by applying the same gate signal to the upper switch of leg A and the lower switch of leg B, and its inverse to the remaining two switches.

This complementary switching action results in the differential output voltage, $v_o(t)$, toggling directly between the full positive and negative DC bus voltages, $+V_{dc}$ and $-V_{dc}$. The output waveform is therefore a two-level voltage signal .

A switching transition occurs each time the reference signal $v_{ref}(t)$ intersects the carrier signal $v_c(t)$. Since a symmetric triangular carrier has one rising and one falling edge per period, and the reference signal lies between its peaks (for $m_a \le 1$), there are precisely two intersections per carrier cycle. Consequently, the output voltage undergoes two large-amplitude transitions in every carrier period. While this results in an output edge rate of $2f_c$, the spectral properties of the resulting pulse train show dominant high-frequency [harmonic content](@entry_id:1125926) appearing in clusters around the carrier frequency $f_c$ and its multiples .

In the linear modulation range ($m_a \le 1$), the fundamental component of the output voltage $v_o(t)$ has a peak amplitude given by:

$$
V_{o,1,\text{peak}} = m_a V_{dc}
$$

For example, for an inverter with $V_{dc} = 400\,\text{V}$ controlled with a [modulation index](@entry_id:267497) of $m_a = 0.75$, the peak fundamental output voltage would be $0.75 \times 400\,\text{V} = 300\,\text{V}$. The RMS value of this fundamental component would be $300/\sqrt{2} \approx 212.1\,\text{V}$ .

### Unipolar PWM Strategy

The unipolar PWM strategy offers a more sophisticated method of control for the full-bridge inverter. Instead of driving the legs complementarily, they are modulated independently. Leg A is controlled by comparing a reference $v_{ref}(t)$ with the carrier $v_c(t)$, while leg B is controlled by comparing an inverted reference, $-v_{ref}(t)$, with the *same* carrier signal .

The instantaneous output voltage is the difference between the two pole voltages, $v_o(t) = v_{AN}(t) - v_{BN}(t)$. With each pole voltage switching between $+V_{dc}/2$ and $-V_{dc}/2$ (relative to a DC bus midpoint), the differential output can assume one of three levels:
1.  $v_{AN} = +V_{dc}/2, v_{BN} = -V_{dc}/2 \implies v_o = +V_{dc}$
2.  $v_{AN} = -V_{dc}/2, v_{BN} = +V_{dc}/2 \implies v_o = -V_{dc}$
3.  $v_{AN} = v_{BN} \implies v_o = 0$

The existence of the zero-voltage state is the defining characteristic of unipolar PWM. The output voltage no longer swings across the full $2V_{dc}$ at every switching event; instead, it transitions between a non-zero state and a zero state.

A remarkable property of unipolar PWM is its spectral characteristic. While the fundamental component of the output voltage remains identical to that of bipolar PWM, $V_{o,1,\text{peak}} = m_a V_{dc}$, the high-frequency [harmonic content](@entry_id:1125926) is significantly different . Because the two legs are modulated by references of opposite phase but with the same carrier, the harmonic components around the carrier frequency $f_c$ in the two pole voltages are largely in-phase (common-mode). When the differential voltage $v_o(t) = v_{AN}(t) - v_{BN}(t)$ is formed, these common-mode harmonics cancel out. This cancellation effectively pushes the first significant cluster of switching harmonics to twice the carrier frequency, $2f_c$  . This effect gives unipolar PWM an effective switching frequency, as seen by the load, of $2f_c$ . This carrier cancellation is contingent on using the exact same carrier signal for both legs; using different or unsynchronized carriers would negate this benefit .

### Comparative Analysis and Practical Implications

The choice between bipolar and unipolar PWM involves trade-offs in performance metrics such as output current ripple, switching losses, and [common-mode voltage](@entry_id:267734) generation.

#### Output Current Ripple

For an inverter driving an [inductive load](@entry_id:1126464), the high-frequency ripple in the output current is a primary concern. The inductor's behavior is described by $v_L(t) = L \frac{di(t)}{dt}$. The peak-to-[peak current](@entry_id:264029) ripple, $\Delta i_L$, over a short interval is approximately proportional to the magnitude of the high-frequency voltage applied ($\Delta v$) and the duration for which it is applied ($\Delta t$).

Unipolar PWM provides substantially lower current ripple compared to bipolar PWM for two main reasons :
1.  **Reduced Voltage Step Magnitude:** In bipolar PWM, the voltage across the load alternates between $+V_{dc}$ and $-V_{dc}$, creating high-frequency voltage steps of magnitude $2V_{dc}$. In unipolar PWM, the output voltage switches between a DC rail and the zero state, resulting in voltage steps of magnitude $V_{dc}$. This halving of the applied ripple voltage magnitude directly reduces the rate of change of current, thereby reducing the current ripple.
2.  **Increased Effective Ripple Frequency:** As established, the dominant output voltage ripple in unipolar PWM occurs at $2f_c$, whereas for bipolar it is at $f_c$. A higher ripple frequency allows less time for the current to deviate from its fundamental component during each switching cycle.

A simplified analysis assuming the high-frequency voltage component is a square wave shows that the current ripple is proportional to $\Delta v / f_{eff}$, where $f_{eff}$ is the effective ripple frequency. Unipolar PWM benefits from both a smaller $\Delta v$ and a larger $f_{eff}$, leading to a significant reduction in output current ripple. This allows for the use of smaller (and thus cheaper and less bulky) output filter inductors to achieve the same level of current quality. Modeling this effect from first principles, if we isolate the impact of halving the [effective voltage](@entry_id:267211) step, the ripple current is also halved . When combined with the doubling of the effective frequency, the improvement is even more pronounced.

#### Switching Losses

Switching losses in power devices (e.g., MOSFETs, IGBTs) occur during the finite time it takes to transition between on and off states. In a standard full-bridge inverter, each power device must block the full DC bus voltage, $V_{dc}$, regardless of the PWM strategy. Furthermore, for both bipolar and unipolar schemes, each of the four switches turns on and off once per carrier cycle. Therefore, the number of switching events per device is identical. Based on this, the total device switching losses are, to a first approximation, the same for both strategies. However, the dynamics of switching (e.g., hard vs. soft switching, diode reverse recovery) differ significantly between the two methods and can lead to different real-world losses, a topic explored further in the Applications section.

#### Common-Mode Voltage (CMV)

The common-mode voltage, defined with respect to the DC bus midpoint as $v_{cm}(t) = (v_{AN}(t) + v_{BN}(t))/2$, is a critical parameter related to electromagnetic interference (EMI) and, in motor drives, damaging bearing currents.

In **bipolar PWM**, the legs are always in opposite states. If $v_{AN}(t) = +V_{dc}/2$, then $v_{BN}(t) = -V_{dc}/2$, and vice versa. As a result, their sum is always zero, and the ideal [common-mode voltage](@entry_id:267734) is identically zero at all times: $v_{cm}(t) \equiv 0$  . This is a significant advantage of the bipolar strategy.

In **unipolar PWM**, the legs are modulated independently. This can lead to states where both legs are connected to the same DC rail ($v_{AN} = v_{BN} = +V_{dc}/2$ or $v_{AN} = v_{BN} = -V_{dc}/2$). In these cases where both legs are connected to the same rail, the common-mode voltage becomes $v_{cm}(t) = \pm V_{dc}/2$. During the active states where the legs are connected to opposite rails, the CMV is zero. Consequently, the CMV in unipolar PWM is a high-frequency, three-level switching waveform (taking values of $+V_{dc}/2$, $0$, and $-V_{dc}/2$), which is a major source of [common-mode noise](@entry_id:269684) .

### Operation in Overmodulation ($m_a > 1$)

When the application requires a fundamental voltage amplitude greater than what is achievable in the [linear range](@entry_id:181847) ($V_{o,1,\text{peak}} > V_{dc}$), the inverter is operated in overmodulation by setting $m_a > 1$. In this regime, the peak of the reference signal $v_{ref}(t)$ exceeds the peak of the carrier $V_c$.

During the portions of the fundamental cycle where $|v_{ref}(t)| > V_c$, the comparator output saturates, and the PWM pulses merge. This "clipping" of the ideal pulse pattern means the output duty cycle is held at its maximum or minimum value for a continuous interval. This is a nonlinear process that introduces low-order harmonics (3rd, 5th, 7th, etc.) into the output voltage, increasing its [total harmonic distortion](@entry_id:272023) (THD). The amplitude of the fundamental component no longer increases linearly with $m_a$ but grows at a progressively slower rate, asymptotically approaching the fundamental amplitude of a square wave, $(4/\pi)V_{dc}$, as $m_a \to \infty$  .

A crucial and often subtle point about [overmodulation](@entry_id:1129249) concerns waveform symmetry. Because the sinusoidal reference and the clipping process are symmetric around the zero crossings, the resulting line voltage waveform $v_o(t)$ for both bipolar and unipolar strategies preserves **half-wave odd symmetry**, i.e., $v_o(t) = -v_o(t - T_1/2)$. A direct consequence of this symmetry is that **no even-order harmonics (including a DC component) are generated in the line voltage**, even under heavy [overmodulation](@entry_id:1129249) . While the individual pole voltages in unipolar PWM do develop even-order harmonics due to asymmetric clipping, these harmonics are common-mode and are cancelled in the differential output voltage, preserving the spectral purity of the line voltage with respect to even harmonics .