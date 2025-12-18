## Introduction
The three-phase Voltage Source Inverter (VSI) is a fundamental building block in modern power electronics, enabling the conversion of DC power into high-quality AC power for a vast range of applications, including variable-speed motor drives, renewable energy grid integration, and uninterruptible power supplies. At the heart of VSI operation lies the control strategy that dictates how semiconductor switches are turned on and off to synthesize the desired AC voltage. While numerous advanced modulation techniques exist, a profound understanding of the foundational control modes is essential for any power electronics engineer. This article addresses the critical knowledge gap between basic circuit topology and the nuanced operational differences and trade-offs inherent in the two most fundamental strategies: 180° and 120° conduction.

To build this comprehensive understanding, this article is structured into three progressive chapters. The first chapter, **Principles and Mechanisms**, will lay the theoretical groundwork, exploring the direct relationship between switching states and output voltages, introducing the powerful space vector representation, and conducting a detailed comparative analysis of the 180° and 120° conduction modes. Following this, the **Applications and Interdisciplinary Connections** chapter will bridge theory with practice, examining how these conduction modes perform with different load types, the impact of non-ideal device behavior, and the critical trade-offs concerning efficiency, harmonic distortion, and electromagnetic compatibility. Finally, the **Hands-On Practices** chapter offers a series of guided problems to reinforce these concepts and develop practical analytical skills. We begin by delving into the core principles that govern all VSI operations.

## Principles and Mechanisms

This chapter delves into the fundamental principles and operational mechanisms of the three-phase Voltage Source Inverter (VSI). We will systematically build an understanding of how switching actions translate into synthesized AC voltages. We will begin by defining the relationships between discrete inverter states and the continuous voltages they produce. Then, we will introduce the elegant framework of space vector representation. Finally, we will conduct a detailed examination and comparison of two foundational operating strategies: the 180° and 120° conduction modes, culminating in an analysis of their practical implications.

### The Inverter State and Fundamental Voltage Relationships

A three-phase VSI consists of three half-bridge legs, one for each phase ($a, b, c$). Each leg contains a pair of complementary switches connecting the output terminal to the positive and negative rails of a DC voltage source, $V_{dc}$.

#### Switching States and Pole Voltages

The state of the inverter at any instant can be precisely described by a set of binary [switching functions](@entry_id:755705), $[s_a, s_b, s_c]$, where $s_x \in \{0, 1\}$ for each phase $x \in \{a, b, c\}$. By convention, $s_x = 1$ signifies that the upper switch of leg $x$ is conducting, connecting the output terminal to the positive DC rail. Conversely, $s_x = 0$ signifies that the lower switch is conducting, connecting the terminal to the negative DC rail. To prevent a direct short-circuit of the DC source (a "shoot-through" fault), the upper and lower switches of the same leg are never commanded to be on simultaneously.

The voltage at each inverter output terminal relative to a reference point is known as the **pole voltage**. A convenient and common reference is the negative DC bus, which we can label as node $M$ and assign a potential of $0$. The positive DC bus, node $P$, is then at potential $V_{dc}$. With ideal switches (zero voltage drop when on), the pole voltage for phase $x$ with respect to the negative DC rail, $v_{xM}$, is directly determined by its switching state:

$$v_{xM}(t) = s_x(t) V_{dc}$$

This simple yet powerful equation is the most fundamental link between the [digital control](@entry_id:275588) state of the inverter and the analog voltage it produces.

#### Line-to-Line Voltages

The primary function of the VSI is to create AC line-to-line voltages at its output terminals. The instantaneous line-to-line voltage between any two phases, say $x$ and $y$, is simply the difference in their pole voltages. Using Kirchhoff's Voltage Law (KVL), we find:

$$v_{xy}(t) = v_{xM}(t) - v_{yM}(t)$$

Substituting the expression for pole voltages, we arrive at a universally applicable formula for the line-to-line voltage :

$$v_{xy}(t) = (s_x(t) - s_y(t))V_{dc}$$

Remarkably, this relationship depends only on the switching states of the two involved legs and the DC bus voltage. It is independent of the load characteristics, the presence of a neutral connection, or the specific modulation strategy being employed. Since $s_x$ and $s_y$ can each be $0$ or $1$, the instantaneous line-to-line voltage can only take on three possible values: $V_{dc}$, $0$, or $-V_{dc}$.

#### Pole Voltage vs. Load Phase Voltage

It is crucial to distinguish between the inverter's pole voltage and the voltage that appears across a phase of the load. For a star (Y) connected load, the load impedances are connected from the inverter terminals ($a, b, c$) to a common load neutral point, which we will label $O$. The voltage across the phase-$x$ load impedance is $v_{xO}$.

The potential of the load neutral point $O$ relative to the inverter's DC reference midpoint $N$ (assuming a center-tapped DC bus for this definition) is called the **neutral displacement voltage**, $v_{ON}$. By applying KVL to the loop containing points $x$, $O$, and $N$, we find the relationship :

$$v_{xO} = v_{xN} - v_{ON}$$

Here, $v_{xN}$ is the pole voltage relative to the DC midpoint $N$. This equation reveals that the voltage experienced by the load is not necessarily equal to the pole voltage produced by the inverter. It is modulated by the behavior of the load neutral, $v_{ON}$, which itself depends on the switching states and the load configuration. If the load neutral $O$ were physically connected to the DC midpoint $N$, then $v_{ON}$ would be forced to zero, and the load phase voltage would equal the pole voltage. However, for a standard 3-wire system with an isolated neutral, $v_{ON}$ is dynamic and non-zero, as we will explore later.

### Space Vector Representation of Inverter States

While analyzing individual phase and line voltages is essential, a more holistic and geometrically intuitive view is provided by the **space vector** representation. This mathematical transformation maps the three phase quantities into a single rotating vector in a two-dimensional complex plane ($\alpha-\beta$ frame).

#### Mapping States to Space Vectors

The [space vector](@entry_id:1132014) of the inverter's output voltage, $\vec{v}$, is defined by the Clarke Transform of the load's phase-to-neutral voltages, $v_{aO}, v_{bO}, v_{cO}$. However, a more direct mapping from the switching states can be derived. For a balanced, 3-wire load, the condition $v_{aO} + v_{bO} + v_{cO} = 0$ holds. This allows us to derive a compact formula for the [space vector](@entry_id:1132014) directly from the pole voltages, and thus from the switching states $[s_a, s_b, s_c]$ . If we define the complex operator $\alpha = \exp(j\frac{2\pi}{3})$, the [space vector](@entry_id:1132014) is given by:

$$\vec{v} = \frac{2V_{dc}}{3} (s_a + s_b\alpha + s_c\alpha^2)$$

This equation elegantly synthesizes the discrete, three-dimensional state $[s_a, s_b, s_c]$ into a single complex number representing the instantaneous voltage vector applied to the load.

#### The Eight Fundamental Vectors

Since there are three legs, each with two possible states, there are $2^3 = 8$ unique switching states. Each state corresponds to a specific voltage [space vector](@entry_id:1132014)  :

*   **Zero Vectors:** Two states result in a zero-magnitude vector.
    *   State $[0,0,0]$: $\vec{v}_0 = \frac{2V_{dc}}{3}(0 + 0 + 0) = 0$. All phases are connected to the negative DC rail.
    *   State $[1,1,1]$: $\vec{v}_7 = \frac{2V_{dc}}{3}(1 + \alpha + \alpha^2) = 0$. All phases are connected to the positive DC rail.
    These states effectively apply zero voltage to the load.

*   **Active Vectors:** The remaining six states produce non-zero vectors of equal magnitude, forming the vertices of a regular hexagon in the complex plane.
    *   State $[1,0,0]$: $\vec{v}_1 = \frac{2}{3}V_{dc}$ (Angle: $0°$)
    *   State $[1,1,0]$: $\vec{v}_2 = \frac{2}{3}V_{dc} \exp(j\frac{\pi}{3})$ (Angle: $60°$)
    *   State $[0,1,0]$: $\vec{v}_3 = \frac{2}{3}V_{dc} \exp(j\frac{2\pi}{3})$ (Angle: $120°$)
    *   State $[0,1,1]$: $\vec{v}_4 = \frac{2}{3}V_{dc} \exp(j\pi)$ (Angle: $180°$)
    *   State $[0,0,1]$: $\vec{v}_5 = \frac{2}{3}V_{dc} \exp(j\frac{4\pi}{3})$ (Angle: $240°$)
    *   State $[1,0,1]$: $\vec{v}_6 = \frac{2}{3}V_{dc} \exp(j\frac{5\pi}{3})$ (Angle: $300°$)

All eight of these states are physically admissible. The goal of any modulation scheme is to sequence through a subset of these eight fundamental vectors in such a way that their time-averaged effect approximates a smoothly rotating sinusoidal voltage vector.

### The 180° Conduction Mode

The 180° conduction mode, also known as six-step operation, is one of the simplest and most fundamental control strategies for a VSI.

#### Gating Principle

The defining principle of this mode is straightforward: each of the six switching devices is gated on for a contiguous $180°$ of the fundamental electrical cycle. Within each leg, the upper and lower switches are gated complementarily. The gating signals for the three legs are phase-shifted by $120°$ relative to each other.

#### State Sequence and Vector Trajectory

This gating logic dictates a deterministic sequence of switching states. At any given moment, exactly three switches are on—one in each leg. As the electrical angle progresses, a commutation (one switch turning off, another turning on) occurs every $60°$. This results in the inverter cycling through the six active vector states sequentially, dwelling on each one for exactly $60°$ or $\pi/3$ [radians](@entry_id:171693) . For example, a typical sequence is $\vec{v}_1 \to \vec{v}_2 \to \vec{v}_3 \to \vec{v}_4 \to \vec{v}_5 \to \vec{v}_6$ and back to $\vec{v}_1$.

A critical characteristic of ideal 180° conduction is that the zero vectors, $\vec{v}_0$ and $\vec{v}_7$, are never applied. The inverter is always in one of the six active states  .

#### Output Voltage Waveforms

The fixed sequence of active vectors produces a distinctive output voltage waveform. The line-to-line voltage, such as $v_{ab}$, is a quasi-square wave or **six-step waveform**. It holds a value of $+V_{dc}$ for $120°$, drops to $0$ for $60°$, then goes to $-V_{dc}$ for $120°$, and back to $0$ for $60°$ within each cycle .

While non-sinusoidal, this waveform is periodic and can be analyzed using Fourier series. The waveform is rich in harmonics, specifically of orders $6k \pm 1$ (i.e., 5th, 7th, 11th, 13th, ...). The primary objective is to produce a strong fundamental component. Through Fourier analysis, the peak amplitude of the fundamental component of the line-to-line voltage can be shown to be :

$$V_{ab, peak(1)} = \frac{2\sqrt{3}}{\pi}V_{dc} \approx 1.103 V_{dc}$$

#### Load Neutral Behavior

With an isolated star-connected load, the neutral displacement voltage $v_{ON}$ is determined by applying KCL at the neutral point, which implies that the sum of the phase currents must be zero. For a balanced resistive load, this means the sum of the phase voltages must also be zero. This leads to the result that the neutral displacement is the average of the three pole voltages :

$$v_{ON} = \frac{v_{AN} + v_{BN} + v_{CN}}{3}$$

Since the pole voltages jump between $+V_{dc}/2$ and $-V_{dc}/2$ (relative to a DC midpoint $N$), the neutral point voltage $v_{ON}$ also jumps between distinct levels. For instance, in state $[1,1,0]$, where $v_{AN}=+V_{dc}/2$, $v_{BN}=+V_{dc}/2$, and $v_{CN}=-V_{dc}/2$, the neutral voltage is $v_{ON} = (+V_{dc}/2 + V_{dc}/2 - V_{dc}/2)/3 = +V_{dc}/6$. This fluctuating neutral voltage contributes to the [harmonic content](@entry_id:1125926) of the phase voltages experienced by the load.

### The 120° Conduction Mode

The 120° conduction mode represents an alternative fundamental operating strategy with distinct characteristics.

#### Gating Principle

In this mode, each switching device is gated on for only $120°$ per cycle. The key operational feature is that at any given time, only two switches are actively gated on: one upper switch in one leg, and one lower switch in another leg. The third leg is intentionally left in a **floating** state, with both its upper and lower switches commanded off . This state persists for $60°$ before the next commutation.

#### State Sequence and Floating Leg Behavior

The behavior of the floating leg is a crucial aspect of this mode. Although no switches in that leg are gated on, the load current for that phase must still find a path. Since the load is typically inductive and currents are continuous, the current will freewheel through one of the anti-parallel diodes of the floating leg.

If the current in the floating phase $x$ is flowing out of the inverter ($i_x > 0$), it will flow back into the negative DC rail through the lower diode. This clamps the terminal voltage $v_{xM}$ to near $0$, corresponding to a state $s_x = 0$. If the current is flowing into the inverter ($i_x  0$), it will flow from the positive DC rail through the upper diode, clamping $v_{xM}$ to near $V_{dc}$, corresponding to a state $s_x = 1$.

Therefore, even though one leg is not actively switched, its terminal is still connected to one of the DC rails. The remarkable result is that the inverter cycles through the exact same sequence of six active states—$[100], [110], [010], [011], [001], [101]$—as in the 180° mode. The mechanism for achieving these states is different, but the resulting voltage vectors applied to the load are identical .

#### Load Neutral Behavior

The behavior of the load neutral in 120° mode differs from the 180° case. When one phase is floating, its current is zero only if the gating commands it to be open. In the typical implementation where it floats and current is conducted by a diode, KCL applies to the two actively driven phases and the floating phase. If we consider the simpler idealized case where the floating leg's current is forced to be zero (as with a resistive load), KCL at the neutral dictates that the currents in the two active phases are equal and opposite ($i_A = -i_B$ if C is floating). For a balanced load, this implies $v_{AO} = -v_{BO}$. Substituting $v_{xO} = v_{xN} - v_{ON}$ leads to :

$$v_{ON} = \frac{v_{AN} + v_{BN}}{2}$$

The neutral displacement is now the average of only the two connected pole voltages. For instance, in the state where leg A is high ($v_{AN}=+V_{dc}/2$) and leg B is low ($v_{BN}=-V_{dc}/2$) with leg C floating, the neutral voltage becomes $v_{ON} = (+V_{dc}/2 - V_{dc}/2)/2 = 0$. This illustrates a different dynamic behavior of the common point compared to 180° conduction.

### Comparative Analysis and Practical Implications

While both 180° and 120° conduction modes sequence through the same six active voltage vectors, their underlying mechanisms give rise to significant practical differences.

#### Zero Vector Accessibility and PWM

The 180° mode is a form of continuous modulation; all three legs are always actively switching. There are no natural intervals in the switching pattern to insert a zero vector. In contrast, the 120° mode is a form of discontinuous modulation. The fact that one leg is "off" for a third of the cycle provides a natural opportunity. While the basic 120° mode does not produce zero vectors, its structure is the foundation for advanced PWM techniques like Discontinuous PWM (DPWM). In these schemes, the "floating" intervals are strategically used to apply a zero vector, which can reduce switching losses .

#### Common-Mode Voltage

The voltage of the load neutral with respect to ground can cause significant electromagnetic interference (EMI) and damaging bearing currents in motors. This common-mode voltage is directly related to the inverter's zero-sequence component, which we can define as $v_0(t) = (v_{aM} + v_{bM} + v_{cM})/3 = \frac{V_{dc}}{3}(s_a+s_b+s_c)$.

The instantaneous value of $v_0(t)$ depends on how many upper switches are on:
*   $s_a+s_b+s_c = 0$ (state [000]): $v_0 = 0$
*   $s_a+s_b+s_c = 1$ (states [100], [010], [001]): $v_0 = V_{dc}/3$
*   $s_a+s_b+s_c = 2$ (states [110], [011], [101]): $v_0 = 2V_{dc}/3$
*   $s_a+s_b+s_c = 3$ (state [111]): $v_0 = V_{dc}$

In 180° conduction, only active vectors are used, so $v_0(t)$ only takes values of $V_{dc}/3$ and $2V_{dc}/3$. In PWM schemes that utilize zero vectors (often based on the 120° structure), all four voltage levels appear. Let $\alpha$ be the fraction of time per cycle that zero vectors are applied. The RMS value of the common-mode voltage can be shown to be a function of this fraction :

$$V_{0,rms} = V_{dc} \sqrt{\frac{4\alpha + 5}{18}}$$

For a purely 180° scheme, $\alpha=0$, giving $V_{0,rms} = V_{dc} \sqrt{5/18} \approx 0.527 V_{dc}$. For a PWM scheme that maximizes zero-vector time, $\alpha$ increases, and the RMS common-mode voltage changes, illustrating a key trade-off between control strategy and EMI performance.

#### Switching Losses

Perhaps the most significant practical difference lies in switching losses. In 180° mode, all six devices are actively switching throughout the cycle. In 120° mode, each device is inactive (clamped to a rail or floating) for one-third of the [fundamental period](@entry_id:267619). This means that two of the six devices are not experiencing switching losses at any given time. Consequently, the 120° conduction mode and its PWM derivatives inherently offer lower total switching losses, leading to higher inverter efficiency, especially at high switching frequencies. This trade-off between harmonic performance, implementation complexity, and efficiency is a central theme in the design of power electronic converters.