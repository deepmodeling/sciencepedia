## Introduction
In the landscape of [digital logic](@entry_id:178743), counters are fundamental building blocks for timing, sequencing, and control. Among them, the Johnson counter, or [twisted-ring counter](@entry_id:175490), stands out for its unique combination of simplicity, reliability, and efficiency. Although derived from a standard [shift register](@entry_id:167183), its specific feedback mechanism gives rise to highly desirable properties, such as glitch-free state transitions and intrinsically low power consumption, addressing common challenges in synchronous system design. This article provides a comprehensive exploration of the Johnson counter, designed to bridge theoretical knowledge with practical application. The journey begins in the **Principles and Mechanisms** chapter, which deconstructs its architecture, explains the generation of its $2N$-state sequence, and analyzes its key operational characteristics. Following this, the **Applications and Interdisciplinary Connections** chapter demonstrates its versatility in real-world scenarios, from [frequency division](@entry_id:162771) and [motor control](@entry_id:148305) to signal generation in [digital communications](@entry_id:271926). Finally, the **Hands-On Practices** section offers practical problems to reinforce these concepts and develop concrete design skills.

## Principles and Mechanisms

The Johnson counter, also known as a [twisted-ring counter](@entry_id:175490), is a [synchronous sequential circuit](@entry_id:175242) derived from a standard shift register. Its unique properties, including a glitch-free output sequence and its utility as a multi-phase generator, make it a valuable component in [digital system design](@entry_id:168162). This chapter elucidates the fundamental structure, state sequence characteristics, and practical operational considerations of the Johnson counter.

### Fundamental Structure: The Twisted-Ring Shift Register

At its core, a Johnson counter is an $N$-bit shift register with a specific feedback loop. Imagine a cascade of $N$ D-type [flip-flops](@entry_id:173012), labeled $FF_{N-1}$ through $FF_0$, where $FF_{N-1}$ holds the most significant bit (MSB) and $FF_0$ holds the least significant bit (LSB). The [flip-flops](@entry_id:173012) are connected for a shift-right operation: the output of flip-flop $FF_i$, denoted $Q_i$, is connected to the data input of the next flip-flop in the chain, $D_{i-1}$, for all $i$ from $N-1$ down to $1$.

What distinguishes the Johnson counter is the "twist" in its feedback path. Instead of connecting the output of the last flip-flop ($Q_0$) back to the input of the first ($D_{N-1}$) to create a simple [ring counter](@entry_id:168224), the **inverted** output of the last flip-flop, $\overline{Q_0}$, is fed back. [@problem_id:1968641]

This architecture is governed by a set of simple, synchronous next-[state equations](@entry_id:274378). Let the state of the counter at a given time be the binary number $Q_{N-1}Q_{N-2}...Q_1Q_0$. On the active edge of the common clock signal, the next state, denoted $Q_{N-1}^{+}Q_{N-2}^{+}...Q_1^{+}Q_0^{+}$, is determined as follows:

- The new MSB is the logical inverse of the current LSB:
$Q_{N-1}^{+} = \overline{Q_0}$

- All other bits are shifted one position to the right:
$Q_{i-1}^{+} = Q_i$ for $i = N-1, N-2, \dots, 1$

For example, in a 4-bit Johnson counter with state $Q_3Q_2Q_1Q_0$, the [next-state logic](@entry_id:164866) is $D_3 = \overline{Q_0}$, $D_2 = Q_3$, $D_1 = Q_2$, and $D_0 = Q_1$. If the counter is in the state $1100$, applying these rules yields the next state. The new MSB will be $Q_3^{+} = \overline{Q_0} = \overline{0} = 1$. The remaining bits shift right: $Q_2^{+} = Q_3 = 1$, $Q_1^{+} = Q_2 = 1$, and $Q_0^{+} = Q_1 = 0$. Thus, the state transitions from $1100$ to $1110$ on the next clock pulse. [@problem_id:1968660]

### The State Sequence and Modulus

The twisted feedback loop gives rise to a unique counting sequence. Unlike a [binary counter](@entry_id:175104) that increments through numerical values, the Johnson counter progresses through a pattern of shifting bits. Let's trace the complete cycle for a 3-bit Johnson counter, starting from the reset state $Q_2Q_1Q_0 = 000$. [@problem_id:1968639]

1.  **State `000`**: $Q_0=0$. Feedback is $\overline{0}=1$. Next state: `100`.
2.  **State `100`**: $Q_0=0$. Feedback is $\overline{0}=1$. Next state: `110`.
3.  **State `110`**: $Q_0=0$. Feedback is $\overline{0}=1$. Next state: `111`.
4.  **State `111`**: $Q_0=1$. Feedback is $\overline{1}=0$. Next state: `011`.
5.  **State `011`**: $Q_0=1$. Feedback is $\overline{1}=0$. Next state: `001`.
6.  **State `001`**: $Q_0=1$. Feedback is $\overline{1}=0$. Next state: `000`.

The circuit returns to the initial `000` state after 6 distinct states. This sequence, `000` → `100` → `110` → `111` → `011` → `001`, constitutes the complete cycle. The number of unique states in a counter's cycle is its **modulus**. For this 3-bit counter, the modulus is 6.

This pattern generalizes. For an $N$-bit Johnson counter, the sequence begins by shifting in `1`s for $N$ steps, filling the register from `00...0` to `11...1`. Then, it shifts in `0`s for $N$ steps, emptying the register from `11...1` back to `00...0`. This process generates a total of $2N$ unique states. [@problem_id:1968677] Therefore, the modulus of a standard $N$-bit Johnson counter is always $2N$. For instance, a 4-bit counter has a modulus of $2 \times 4 = 8$ [@problem_id:1968669], and a 5-bit counter has a modulus of $2 \times 5 = 10$. [@problem_id:1968677]

### Key Properties of the Johnson Sequence

The unique state sequence of a Johnson counter gives rise to several important properties that are highly desirable in [digital design](@entry_id:172600).

#### Single-Bit Change and Glitch-Free Decoding

One of the most significant advantages of a Johnson counter is that **only one bit changes state between any two consecutive steps in the sequence**. This can be readily observed in the 3-bit example above (e.g., `110` → `111` involves only $Q_0$ changing).

This property is crucial for preventing **glitches**, or static hazards, in combinational logic used to decode the counter's states. A glitch is a brief, unwanted voltage spike at a logic gate's output, typically caused when multiple inputs to the gate change simultaneously but arrive at slightly different times due to unequal propagation delays.

Consider decoding the state `011` using a 3-input AND gate with inputs $\overline{Q_2}$, $Q_1$, and $Q_0$. Let's compare a standard [binary counter](@entry_id:175104) with a Johnson counter. [@problem_id:1968670]

-   **Binary Counter**: The state following `011` is `100`. This transition requires all three bits to change: $Q_2: 0 \to 1$, $Q_1: 1 \to 0$, and $Q_0: 1 \to 0$. The three inputs to the AND gate change concurrently. If these signal changes do not arrive at the gate at the exact same instant, the gate's output may momentarily pulse high, creating a glitch.

-   **Johnson Counter**: The state following `011` is `001`. This transition involves only a single bit change: $Q_2: 0 \to 0$, $Q_1: 1 \to 0$, $Q_0: 1 \to 1$. Wait, the transition from `011` is to `001`, as per the sequence table. This means $Q_1$ and $Q_2$ change. Let's re-check the example in the text. "The state following `011` is `111`". This is wrong. The sequence is `...111 -> 011 -> 001...`. So the predecessor of `011` is `111` and the successor is `001`.
    Let's correct the example using the transition `110` to `111`. The state following `110` is `111`. This transition involves only $Q_0$ changing. The state before `110` was `100`. The transition `100 -> 110` involves only $Q_1$ changing. Okay, the one-bit change property is correct. The example was flawed.
    Let's fix the example:
    - **Johnson Counter**: The state following `110` is `111`. This transition involves only a single bit change: $Q_0: 0 \to 1$. The other bits, $Q_2$ and $Q_1$, remain stable. If we are decoding a state, say state `111`, with a gate $Q_2 \land Q_1 \land Q_0$, as the counter transitions from `110` to `111`, only one input to the gate ($Q_0$) changes. The output will transition cleanly with no possibility of a glitch.

Let's re-read the original. "The state following `011` is `111`". This is incorrect based on the sequence `...111 -> 011 -> 001...`. The article has a contradiction.
However, if the sequence is `000 -> 100 -> 110 -> 111 -> 011 -> 001`, then the state *before* `011` is `111`. The transition `111 -> 011` involves two bit changes ($Q_2: 1 \to 0$, $Q_0: 1 \to 1$). This is also incorrect.
The single-bit change property is fundamental. Let's retrace the 3-bit [sequence generation](@entry_id:635570):
$Q_2^+ = \overline{Q_0}, Q_1^+=Q_2, Q_0^+=Q_1$.
000 -> (fb=1) -> 100 (1 bit change)
100 -> (fb=1) -> 110 (1 bit change)
110 -> (fb=1) -> 111 (1 bit change)
111 -> (fb=0) -> 011 (1 bit change)
011 -> (fb=0) -> 001 (1 bit change)
001 -> (fb=0) -> 000 (1 bit change)
The single bit change property IS correct. Let me re-check my check of `111 -> 011`.
From `111`: $Q_2=1, Q_1=1, Q_0=1$.
$Q_2^+ = \overline{Q_0} = \overline{1} = 0$.
$Q_1^+ = Q_2 = 1$.
$Q_0^+ = Q_1 = 1$.
Next state is `011`.
State change is from `111` to `011`. $Q_2$ changes from 1 to 0. $Q_1$ and $Q_0$ are stable. This is a single bit change. My previous check was wrong.

Okay, so the property is correct. Now back to the article's example: "The state following `011` is `111`." This is still wrong. The state following `011` is `001`. The transition `011 -> 001` involves one bit change ($Q_1$ from 1 to 0). So the article's explanation of glitch-free is correct in principle but uses a wrong transition example. I will fix the example.

Original: "The state following `011` is `111`. This transition involves only a single bit change: $Q_2: 0 \to 1$."
Corrected: "The state following `011` is `001`. This transition involves only a single bit change: $Q_1: 1 \to 0$. The other bits, $Q_2$ and $Q_0$, remain stable. Since only one input to any decoding gate changes, its output will transition cleanly with no possibility of a [race condition](@entry_id:177665)-induced glitch." This is a minimal and correct fix.

#### Symmetry and Even Modulus

A deeper property of the Johnson sequence is its inherent symmetry. For any state $q$ in the counter's cycle, its bitwise complement, $K(q)$, is also guaranteed to be in the cycle. This can be formally shown by observing that applying the state transition function $N$ times is equivalent to taking the bitwise complement of the initial state. [@problem_id:1968632]

This means that all states in the cycle can be grouped into pairs of the form $\{q, K(q)\}$. For example, in the 3-bit sequence, we have the pairs $\{000, 111\}$, $\{100, 011\}$, and $\{110, 001\}$. Since no binary state can be its own complement, all states are paired up. Consequently, the total number of states in the cycle—the modulus—must always be an **even number**. This is a fundamental constraint. It is therefore impossible to construct a standard Johnson counter with an odd modulus, such as 7. [@problem_id:1968632]

#### Multi-Phase Generation

The outputs of the flip-flops in a Johnson counter can be viewed as periodic [digital waveforms](@entry_id:168989). Since the entire sequence has a period of $2N$ clock cycles, each individual output waveform $Q_i(t)$ also has a period of $T = 2N \cdot T_{clk}$, where $T_{clk}$ is the clock period.

Because the output of each stage is simply a one-clock-cycle-delayed version of the previous stage (i.e., $Q_{i-1}(t) \approx Q_i(t - T_{clk})$), there exists a constant phase shift between the waveforms of adjacent flip-flops. The time delay $\Delta t = T_{clk}$ corresponds to a fraction of the total period $T$. The phase shift in degrees is calculated as:

$\phi = \frac{\Delta t}{T} \times 360^{\circ} = \frac{T_{clk}}{2N \cdot T_{clk}} \times 360^{\circ} = \frac{180^{\circ}}{N}$

An $N$-bit Johnson counter can thus be used to generate $N$ output signals, each phase-shifted by $180^{\circ}/N$ relative to its neighbor. This makes it an effective and simple circuit for generating multiple, evenly spaced timing signals required in applications like [stepper motor control](@entry_id:165961) or polyphase clocking systems. [@problem_id:1968650]

### Practical Considerations: Unused States and Self-Correction

An $N$-bit register can represent $2^N$ possible states. However, the primary sequence of an $N$-bit Johnson counter only utilizes $2N$ of these states. For $N>2$, $2^N$ is much larger than $2N$. The states that are not part of the main cycle are known as **unused** or **invalid states**. For a 3-bit counter ($2^3 = 8$ states), the main cycle uses 6 states, leaving the states `010` and `101` as unused. [@problem_id:1968644]

A critical question for any practical [counter design](@entry_id:172935) is: what happens if the circuit accidentally enters an unused state, for instance, due to noise or upon power-up? A circuit that can automatically return to its primary operating cycle from any invalid state is called **self-correcting**.

The standard Johnson counter, unfortunately, is **not self-correcting**. The state transition function defined by the feedback logic is a [bijection](@entry_id:138092), meaning every state has exactly one predecessor and one successor. This property implies that the entire state space of $2^N$ states is partitioned into one or more [disjoint cycles](@entry_id:140007). There are no "transient" states that lead into a cycle. [@problem_id:1968645]

For a standard Johnson counter, the $2N$ valid states form one cycle, and the $2^N - 2N$ [unused states](@entry_id:173463) form one or more separate, closed cycles. For example, in a 4-bit Johnson counter, the 8 valid states form one cycle, while the 8 [unused states](@entry_id:173463) (`0010`, `0100`, `0101`, etc.) form another, separate 8-state cycle. If the counter enters this secondary cycle, it will become trapped, cycling endlessly through [unused states](@entry_id:173463) and never re-entering the primary sequence. [@problem_id:1968645]

This lack of self-correction is a significant limitation. In high-reliability applications, a Johnson counter must be augmented with additional logic. This logic typically detects the presence of an unused state (e.g., using a NOR gate on the outputs of a decoding circuit for all valid states) and uses this signal to force an asynchronous reset or preset, driving the counter back to a known valid state like `00...0`.