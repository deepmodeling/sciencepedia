## Introduction
Asynchronous [sequential circuits](@entry_id:174704), operating without the synchronizing beat of a global clock, offer unique advantages in speed and power consumption but present significant design challenges due to complex timing dependencies. The **[fundamental-mode model](@entry_id:171765)** provides a structured and systematic framework for taming this complexity, enabling the creation of reliable and robust clockless systems. This article serves as a comprehensive guide to this essential model, addressing the knowledge gap between the theoretical elegance of asynchronous logic and the practical difficulties of its implementation.

To achieve this, the article is divided into three key sections. The first, **Principles and Mechanisms**, delves into the core tenets of the model, explaining the concepts of stable and unstable states, the central role of the [flow table](@entry_id:175022), and the physical realities of gate delays. It provides a detailed taxonomy of timing pitfalls, including [combinational hazards](@entry_id:166945), critical races, and essential hazards, which are the primary obstacles in asynchronous design. Following this theoretical foundation, the second section, **Applications and Interdisciplinary Connections**, demonstrates how these principles are applied to solve real-world problems. You will learn how the model is used to synthesize critical components like memory latches, communication protocol controllers, and resource arbiters, and how it informs the design of robust interfaces with physical devices. Finally, the **Hands-On Practices** section offers a set of curated problems, allowing you to apply your knowledge to identify stable states, analyze race conditions, and eliminate [logic hazards](@entry_id:174770), cementing your understanding of the [fundamental-mode model](@entry_id:171765).

## Principles and Mechanisms

Following our introduction to the distinction between synchronous and [asynchronous sequential circuits](@entry_id:170735), this chapter delves into the operational principles of the **[fundamental-mode model](@entry_id:171765)**, a foundational framework for analyzing and designing [asynchronous circuits](@entry_id:169162). In this model, we impose specific constraints on the circuit's inputs to manage the complexities arising from the absence of a global clock. Understanding these principles is paramount, as they reveal the inherent challenges of asynchronous design, such as timing hazards and race conditions, and provide a systematic methodology for creating robust and reliable systems.

### The Core Tenets of the Fundamental-Mode Model

The [fundamental-mode model](@entry_id:171765) is built upon a set of core assumptions about how the circuit and its environment interact. These assumptions simplify the design process by restricting the timing of input events.

The two primary tenets are:
1.  **Single Input Change**: Only one external input variable is permitted to change at any given time.
2.  **Stabilization**: After an input change, sufficient time must be allowed for the circuit's internal state and outputs to become completely stable before the next input change occurs.

An asynchronous circuit's internal state is defined by the values of its **[state variables](@entry_id:138790)**, typically denoted as $y_1, y_2, \dots, y_n$. These are the outputs of memory elements (often simple feedback loops) that are fed back as inputs to the circuit's [combinational logic](@entry_id:170600) block. The [combinational logic](@entry_id:170600) then computes the **next-state** values, denoted $Y_1, Y_2, \dots, Y_n$, as well as the circuit's external outputs.

A circuit is said to be in a **stable state** when, for a given combination of external inputs, the next-state values are identical to the present-state values. That is, $Y_i = y_i$ for all [state variables](@entry_id:138790). When an input changes, the circuit enters a period of transition. The new input values may cause the next-state outputs $Y$ to differ from the present-state inputs $y$. This discrepancy creates an **unstable state**. The circuit will then automatically evolve, with the new $Y$ values feeding back to become the new $y$ values, until it eventually settles into a new stable state (or, in a faulty design, enters a sustained oscillation).

#### The Flow Table: A Map of Circuit Behavior

The complete behavior of a fundamental-mode circuit is captured in a **[flow table](@entry_id:175022)**. This tabular representation maps each combination of present state and external inputs to a corresponding next state and output.

Stable states are conventionally circled or bolded in the table to distinguish them from unstable states. To illustrate, consider a circuit with five states (S0-S4), two inputs ($x_1, x_2$), and one output ($Z$). If the circuit is stable in state S0 with input $x_1x_2=00$, and the input changes to $01$, the [flow table](@entry_id:175022) would direct the circuit to a new (potentially unstable) state, S1. The circuit then internally transitions to S1. If S1 is stable for the input $01$, the circuit will wait there for the next input change. By tracing a sequence of input changes, we can determine the corresponding sequence of states and outputs [@problem_id:1967909]. For example, if a circuit starts stable in S0 at $x_1x_2=00$ and receives the input sequence $01 \to 11 \to 10$, it might traverse states S1, then S2, then S3, producing a specific output at each new stable point.

The [flow table](@entry_id:175022) can be derived directly from the circuit's gate-level implementation. For instance, a simple circuit made of two cross-coupled NOR gates, forming a basic Set-Reset (SR) latch, can be analyzed to determine its stable states [@problem_id:1967936]. If the gate outputs are $y_1$ and $y_2$ and the inputs are $x_1$ and $x_2$, the next-[state equations](@entry_id:274378) are $Y_1 = \overline{x_1 + y_2}$ and $Y_2 = \overline{x_2 + y_1}$. A stable state must satisfy $y_1 = \overline{x_1 + y_2}$ and $y_2 = \overline{x_2 + y_1}$. By substituting the four possible input combinations for $(x_1, x_2)$, we can solve for the corresponding stable states $(y_1, y_2)$. Interestingly, for the input $(x_1, x_2) = (0, 0)$, we find two stable states: $(1, 0)$ and $(0, 1)$. This bistability is the essence of memory storage and demonstrates that a single input combination can support multiple stable states.

#### Output Generation: Mealy vs. Moore Models

As with [synchronous circuits](@entry_id:172403), the outputs of an asynchronous circuit can be classified as either **Mealy-type** or **Moore-type**.
*   A **Moore-type** output depends only on the present internal state. Its value is constant for a given state, regardless of the current external input.
*   A **Mealy-type** output depends on both the present state and the current external inputs. Its value can change if the input changes, even if the internal state remains the same.

In a [flow table](@entry_id:175022), a Moore output will have the same value across an entire row (for a given present state). A Mealy output may have different values in the same row. For example, consider an output $Z_2$ that is $0$ for state S0 and $1$ for states S1 and S2, irrespective of the inputs. This is a Moore-type output. In contrast, an output $Z_1$ that is $1$ only when the circuit is in state S0 *and* the input is $11$ is a Mealy-type output, as its value depends on both state and input [@problem_id:1967928].

### Timing Constraints and Physical Reality

The idealized assumptions of the [fundamental-mode model](@entry_id:171765) must be grounded in the physical realities of gate delays. The rules of "one change at a time" and "wait for stabilization" directly address these physical limitations.

#### The Single-Input-Change Rule and Its Violation

The requirement that only one input changes at a time is not arbitrary; it is a critical guard against ambiguity. In a physical system, it is impossible to guarantee that two signals change at precisely the same instant. If a circuit is designed assuming a simultaneous change from, say, $x_1x_2=01$ to $x_1x_2=10$, the reality is that one input will arrive slightly before the other due to differing path delays.

If $x_2$ changes from $1$ to $0$ just before $x_1$ changes from $0$ to $1$, the circuit will briefly experience the transient input combination $x_1x_2=00$. The circuit will react to this transient input, potentially moving to an intermediate state that was never intended in the original design. When the second input change finally arrives, the circuit starts its transition from this new, unintended state, which can lead it to a completely different final stable state than the one expected from the direct $01 \to 10$ transition [@problem_id:1967929]. This demonstrates that designing for multi-input changes is fraught with peril and why the single-input-change constraint is so fundamental.

#### The Stabilization Interval

The second rule, allowing the circuit to stabilize, is directly related to the **[propagation delay](@entry_id:170242)** of the logic gates. When an input changes, a signal must ripple through the combinational logic to compute the new next-state values, $Y_i$. This process takes a finite amount of time. Furthermore, if the state is unstable ($Y \neq y$), the new $Y$ values must feed back and propagate through the logic again. This process may repeat several times.

The minimum time interval, $T_{min}$, that must be maintained between consecutive input changes is therefore determined by the worst-case time it takes for the circuit to settle into a stable state. This is calculated by finding the longest possible path from any input ($x_i$ or $y_i$) to any next-state output ($Y_j$) through the [combinational logic](@entry_id:170600). For example, in a circuit with next-state equation $Y' = (X_1 \wedge Y) \vee (\neg X_1 \wedge X_2)$, a change in $X_1$ must propagate through a NOT gate, then an AND gate, then an OR gate. If each gate has a delay of $\tau$, the total delay along this path is $3\tau$. The external system driving the inputs must therefore wait at least $3\tau$ after changing an input before it can apply the next change, ensuring the fundamental-mode assumption holds [@problem_id:1967895].

### Hazards and Race Conditions: The Perils of Asynchronous Design

Even when the fundamental-mode assumptions are respected, [asynchronous circuits](@entry_id:169162) are susceptible to several types of timing-related errors known as hazards and races. A thorough understanding of these phenomena is essential for reliable design.

#### Combinational Hazards

The [combinational logic](@entry_id:170600) block of an asynchronous circuit must be free of hazards. A **[static hazard](@entry_id:163586)** is a condition where a single input change is supposed to leave the output unchanged, but the output momentarily glitches to the opposite value.
*   A **[static-1 hazard](@entry_id:261002)** occurs when the output is meant to stay at 1 but briefly drops to 0.
*   A **[static-0 hazard](@entry_id:172764)** occurs when the output is meant to stay at 0 but briefly pulses to 1.

These glitches are caused by propagation delays within the [combinational logic](@entry_id:170600). Consider the function $Y = x_1'y + x_1x_2$. If $y=1$ and $x_2=1$, the function simplifies to $Y = x_1' + x_1$. As $x_1$ transitions from $0$ to $1$, the term $x_1'y$ turns off and the term $x_1x_2$ turns on. If the NOT gate that generates $x_1'$ is slow, there can be a moment where both the old $x_1$ (seen by the second term) and the new $x_1'$ (propagated from the inverter) are effectively 0, causing $Y$ to glitch to 0.

Such hazards are identified and eliminated using Karnaugh maps. A [static-1 hazard](@entry_id:261002) exists if two adjacent 1s on the map are not covered by the same product term. The solution is to add a redundant product term, known as a **consensus term**, that covers the two adjacent 1s. For the function $Y = x_1'y + x_1x_2$, the hazardous transition is between minterms $x_1'x_2y$ and $x_1x_2y$. Adding the redundant term $x_2y$ covers this transition and ensures the output remains stable at 1, yielding the hazard-free expression $Y = x_1'y + x_1x_2 + x_2y$ [@problem_id:1967923].

#### Sequential Hazards: Races, Cycles, and Oscillations

More complex hazards arise from the feedback nature of [sequential circuits](@entry_id:174704).

A **race condition** occurs when a state transition requires two or more state variables to change value simultaneously. For example, a transition from state $(y_1, y_2) = (0,0)$ to $(1,1)$. Due to unavoidable differences in gate and wire delays, one variable will always change slightly before the other. The circuit will temporarily pass through an intermediate state, either $(0,1)$ or $(1,0)$. The nature of the race depends on what happens from these intermediate states.

*   **Non-Critical Race**: If all possible intermediate paths lead to the same final, correct stable state, the race is non-critical. The circuit's behavior is still reliable.
*   **Critical Race**: If different intermediate paths lead to different final stable states, the race is critical. The circuit's final state becomes unpredictable and dependent on minute timing variations, which is a major design flaw.

A clear example of a [critical race](@entry_id:173597) can be seen in a circuit requiring a transition from state $(0,0)$ to $(1,1)$ for a given input, say $x=1$. Suppose that for this same input $x=1$, the intermediate states $(0,1)$ and $(1,0)$ are both *stable*. If $y_1$ changes first, the circuit enters state $(1,0)$ and stays there. If $y_2$ changes first, it enters $(0,1)$ and stays there. The intended destination $(1,1)$ is never reached, and the final state is incorrect and unpredictable [@problem_id:1967910]. Analysis of a merged [flow table](@entry_id:175022) with a specific binary [state assignment](@entry_id:172668) can also reveal transitions where two bits must change (e.g., from state 01 to 10). Investigating the intermediate states (00 and 11) and their subsequent transitions under the given input will determine if the race is critical [@problem_id:1967914].

In some cases, an unstable transition does not lead to a stable state at all but instead to another unstable state, which in turn leads back to the first, or to a third unstable state. This can result in a **cycle** or **sustained oscillation**, where the circuit never settles. For a fixed input, the state variables may continuously toggle, for example, between $(0,1)$ and $(1,1)$, burning power and producing no stable outcome [@problem_id:1967899].

A combinational hazard can also induce a [critical race](@entry_id:173597). A [static-0 hazard](@entry_id:172764), for instance, could cause a next-state line $Y_i$ that should be 0 to briefly pulse to 1. If this glitch is fast enough to be latched by the feedback loop, the state variable $y_i$ will change incorrectly. This takes the circuit to an unintended state, from which its subsequent evolution will be different, likely ending in the wrong stable state [@problem_id:1967908]. This highlights the critical need for hazard-free combinational logic.

#### The State Assignment Problem

Critical races are fundamentally a problem of [state encoding](@entry_id:169998). They can be avoided by ensuring that any two states that transition between each other are assigned binary codes with a Hamming distance of 1 (i.e., they are **adjacent**). This is known as the **state [assignment problem](@entry_id:174209)**.

For some flow tables, however, finding a race-free assignment with the minimum number of [state variables](@entry_id:138790) ($k = \lceil\log_2 N\rceil$ for $N$ states) is impossible. This can be proven by constructing a state adjacency graph, where states are nodes and required transitions are edges. For a race-free assignment with $k$ variables to exist, this graph must be embeddable onto the graph of a $k$-dimensional [hypercube](@entry_id:273913). If any state in the required adjacency graph has a degree (number of required adjacencies) greater than $k$, embedding is impossible. For instance, a 4-state machine requires 2 [state variables](@entry_id:138790), where each code can be adjacent to at most 2 others. If the [flow table](@entry_id:175022) requires one state to be adjacent to 3 other states, a race-free assignment is impossible with 2 variables. Any minimal assignment will inevitably contain a [critical race](@entry_id:173597) [@problem_id:1967902]. The solution in such cases is to add extra state variables to provide the necessary adjacencies.

#### Essential Hazards

The most subtle of hazards is the **essential hazard**. It is not caused by races between [state variables](@entry_id:138790) or glitches in the logic but is inherent to the structure of the [flow table](@entry_id:175022) itself. An essential hazard represents a race between the external input signal and the internal state-variable feedback signal.

An essential hazard exists if a single change in an input variable can lead to a different final state than a sequence of three changes of that same input variable (e.g., $x: 0 \to 1$ versus $x: 0 \to 1 \to 0 \to 1$). The hazard occurs because a slow-propagating input change might arrive at the [next-state logic](@entry_id:164866) *after* a state variable has already changed and fed back. The logic then sees the *old* input value combined with the *new* state value, a combination that can steer the circuit to a wrong state. Consider starting stable at $(y_1y_2, x) = (00, 0)$. A single input change $x:0 \to 1$ might cause the circuit to transition to a final stable state of 01. However, if the input signal path has significant delay, the state could change first, and the sequence of events could unfold differently, leading to an incorrect final state like 10. This type of hazard can only be fixed by ensuring the feedback path delays are longer than the input path delays, often by inserting delay elements [@problem_id:1967921].

In summary, the [fundamental-mode model](@entry_id:171765) provides a structured approach to asynchronous design but also reveals a landscape of potential timing pitfalls. Successful design requires not only adhering to the model's core tenets but also meticulously analyzing the [flow table](@entry_id:175022) and the physical implementation to identify and mitigate [combinational hazards](@entry_id:166945), critical races, and essential hazards.