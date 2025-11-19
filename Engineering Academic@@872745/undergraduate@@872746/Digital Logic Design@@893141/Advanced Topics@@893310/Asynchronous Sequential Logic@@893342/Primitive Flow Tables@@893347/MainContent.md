## Introduction
In the world of digital logic, while [synchronous circuits](@entry_id:172403) provide predictability through a global clock, [asynchronous circuits](@entry_id:169162) offer unique advantages in speed and power by reacting directly to input events. This event-driven nature, however, introduces significant design challenges, requiring a formal method to manage state transitions and avoid timing hazards. The [primitive flow table](@entry_id:168105) emerges as the quintessential tool for this purpose, providing a systematic way to capture, analyze, and synthesize the behavior of these clockless systems.

This article serves as a comprehensive guide to mastering the [primitive flow table](@entry_id:168105). The first chapter, **Principles and Mechanisms**, will dissect the structure of the [flow table](@entry_id:175022), explaining the core concepts of stable and unstable states, [fundamental mode](@entry_id:165201) operation, and the critical issue of race conditions. Building on this foundation, the second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the table's practical power by walking through the design of essential components like memory latches, sequence detectors, and communication protocol controllers. Finally, the **Hands-On Practices** section will offer targeted problems to reinforce these concepts, allowing you to apply your knowledge to real-world design scenarios. By the end, you will have a robust understanding of how to use primitive flow tables to bridge the gap from abstract specifications to reliable asynchronous circuit implementations.

## Principles and Mechanisms

In contrast to synchronous systems governed by a global clock, [asynchronous sequential circuits](@entry_id:170735) transition between states in response to changes in their inputs. The primary formal tool for analyzing and synthesizing these circuits is the **[flow table](@entry_id:175022)**. A [flow table](@entry_id:175022) is analogous to the [state table](@entry_id:178995) used for [synchronous circuits](@entry_id:172403), but its interpretation is fundamentally different, reflecting the event-driven nature of asynchronous logic. This chapter elucidates the principles of operation for [asynchronous circuits](@entry_id:169162) by dissecting the structure and mechanics of the [flow table](@entry_id:175022).

### The Flow Table: Representing Asynchronous Behavior

A [flow table](@entry_id:175022) is a tabular representation that maps a circuit's present internal state and its external inputs to a subsequent internal state and its outputs. The rows of the table correspond to the internal states of the circuit, while the columns correspond to the possible combinations of input values. Each cell, or entry, at the intersection of a row (present state $y$) and a column (input vector $X$) specifies the **next state** ($Y$) that the circuit will transition to. In many cases, the cell also specifies the output value ($Z$) produced during that condition.

The fundamental behavior of the circuit is defined by the relationship between the present state $y$ and the next state $Y$. This relationship dictates whether the circuit will remain in its current state or initiate a transition.

### Stable and Unstable States: The Core Dynamics

The core of asynchronous circuit operation revolves around the concepts of stability and instability.

A **stable state** is a combination of a present state and an input vector for which the circuit's next state is the same as its present state. That is, for a present state $y$ and an input vector $X$, the state is stable if the next-[state function](@entry_id:141111) dictates $Y = y$. Once a circuit enters a stable state, it will remain in that state indefinitely, maintaining its internal state and output, until one or more inputs change. Stable states represent the quiescent points of the circuit's operation.

Conversely, an **unstable state** is a condition where the next state is different from the present state ($Y \neq y$). If the circuit finds itself in an unstable state, it will spontaneously transition to the specified next state without any further changes to the external inputs. This internal transition is a defining characteristic of asynchronous behavior.

To illustrate, consider a circuit with one input $x$, one output $z$, and four internal states {A, B, C, D}. The behavior specified in a [flow table](@entry_id:175022) can be examined to identify all stable states [@problem_id:1953737]. A stable state exists wherever the next-state entry in a cell matches the state of the row it is in. For example, if for present state $y=A$ and input $x=0$, the table specifies the next state is $Y=A$, then the combination $(y, x) = (A, 0)$ constitutes a stable state. The corresponding output, say $z=0$, completes the description of this stable condition as the triplet $(A, 0, 0)$. By systematically scanning the entire table, we can enumerate all such stable points. If the [flow table](@entry_id:175022) shows transitions to state $A$ for $(A, x=0)$, to $B$ for $(B, x=1)$, to $C$ for $(C, x=0)$, and to $D$ for $(D, x=1)$, these four conditions represent the complete set of stable states for the circuit. The total number of stable states is simply a count of these occurrences across the entire table [@problem_id:1953713].

### Fundamental Mode Operation and State Transitions

To ensure predictable behavior, [asynchronous circuits](@entry_id:169162) are typically designed to operate in **fundamental mode**. This operational model rests on a crucial assumption: **only one input variable is allowed to change at any given time, and no further input changes occur until the circuit has completed any internal state transitions and settled into a new stable state.**

The sequence of events under fundamental mode operation is as follows:
1. The circuit is initially at rest in a stable state.
2. A single input variable changes, causing the circuit's [operating point](@entry_id:173374) to shift horizontally along its current state row to the new input column.
3. The entry in this new cell is examined.
    a. If the entry specifies a stable state (i.e., next state equals present state), the circuit has reached its new destination and remains there, awaiting the next input change.
    b. If the entry specifies an unstable state, the circuit begins an internal transition. It changes its present state to the specified next state, effectively moving vertically to a new row in the same input column.
4. If the circuit has moved to a new row (a new internal state), the process repeats from step 3b. The circuit continues to transition between internal states within the same input column until it lands in a row that is stable for that input.

This "flow" from one state to another gives the [flow table](@entry_id:175022) its name. Let's trace a transition sequence for a circuit starting in a stable state `a` with inputs $x_1x_2 = 00$ [@problem_id:1953708]. When the input changes to $x_1x_2=01$, we consult the entry in row `a`, column `01`. If this entry is `b, 1`, it indicates an unstable state. The circuit transitions to internal state `b`. With the inputs still held at `01`, we now examine the entry in row `b`, column `01`. If this entry is `c, 1`, it is also unstable, causing a further transition to state `c`. Finally, upon examining row `c`, column `01`, we might find the entry `(c, 1)`, indicating a stable state. At this point, the transition sequence ($a \to b \to c$) concludes, and the circuit stabilizes in state `c` with output `1`.

This cascading internal transition is common. A single input change can trigger a series of state changes before stability is re-established [@problem_id:1953728]. For instance, if a circuit in stable state $S_3$ with input `10` experiences an input change to `00`, its path might be $S_3 \to S_1 \to S_0$, finally stabilizing at $S_0$ because the entry for state $S_0$ and input `00` is $S_0$ itself. A series of input changes will initiate a corresponding sequence of stabilization processes [@problem_id:1953736].

### The Primitive Flow Table

A particularly useful form of [flow table](@entry_id:175022) in the initial stages of design is the **[primitive flow table](@entry_id:168105)**. Its defining characteristic is that **each row contains exactly one stable state**. The remaining entries in a row describe the transitions that occur when the circuit, resting in that row's stable state, experiences an input change.

A key feature of primitive flow tables is the presence of **"don't care"** entries, often denoted by a dash (`-`). These arise directly from the single-input-change assumption of [fundamental mode](@entry_id:165201). Consider a circuit in a stable state `A` where the input is $I_1I_0 = 01$ [@problem_id:1953709]. Under the fundamental mode assumption, the only permissible subsequent input combinations are `00` (a change in $I_0$) and `11` (a change in $I_1$). A transition to the input combination `10` would require both $I_1$ and $I_0$ to change simultaneously. Since this event is disallowed by the operating model, the behavior of the circuit for this transition is not specified. The entry in row `A`, column `10` is therefore a "don't care," signifying that this condition is assumed never to occur. These "don't cares" provide valuable flexibility during the [logic minimization](@entry_id:164420) and implementation phases.

### Output Generation: Mealy and Moore Models

Like their synchronous counterparts, [asynchronous sequential circuits](@entry_id:170735) can be classified as either Mealy or Moore machines, based on how their outputs are generated. This distinction is clearly visible in the [flow table](@entry_id:175022).

- A **Moore model** circuit has outputs that are a function of the present state only. In a [flow table](@entry_id:175022), this means that for any given row (present state), all specified output values must be the same, regardless of the input column. The output is associated with the state itself.

- A **Mealy model** circuit has outputs that are a function of both the present state and the current inputs. This is identified in a [flow table](@entry_id:175022) if there is at least one row where the specified output values differ across different input columns.

For example, consider a [flow table](@entry_id:175022) where the entries are pairs of (Next State, Output) [@problem_id:1953714]. If in the row for present state `B`, the entry for input `01` is `(B, 0)` but the entry for input `11` is `(C, 1)`, the output changes with the input while the circuit is in state `B`. This dependency on both state and input makes it a Mealy machine. If every row had a constant output, it would be a Moore machine.

### Race Conditions: The Perils of Asynchronous Design

The absence of a synchronizing clock makes [asynchronous circuits](@entry_id:169162) susceptible to **race conditions**, where the circuit's behavior depends on the unpredictable delays of gates and wires. These races are a primary challenge in asynchronous design and can be broadly categorized into input races and state races.

#### Input Races

An **input race** occurs when two or more input signals change simultaneously, violating the [fundamental mode](@entry_id:165201) assumption. Because physical signals never change at the exact same instant, the circuit will perceive the changes in some arbitrary order. If the final state of the circuit depends on this order, the behavior is unpredictable.

For instance, imagine a circuit in a stable state `a` with inputs $x_1x_2 = 00$ [@problem_id:1953721]. If both inputs are commanded to change to `1`, creating the input $x_1x_2 = 11$, two paths are possible due to propagation delays:
1.  $x_1$ changes first: The input sequence is perceived as $00 \to 10 \to 11$. The circuit first stabilizes in a new state corresponding to the `10` input, then transitions to a final state for the `11` input. This might lead to a final stable state `e`.
2.  $x_2$ changes first: The input sequence is perceived as $00 \to 01 \to 11$. This path would cause the circuit to stabilize at an intermediate state for the `01` input, and then transition to a final state for the `11` input, which might be state `c`.

Since the final stable state could be either `c` or `e` depending on minute timing variations, the circuit's behavior is ambiguous. This is a design flaw that must be addressed, typically by ensuring that only one input can change at a time.

#### State Races: Non-Critical vs. Critical

Even when the single-input-change rule is followed, races can occur among the [internal state variables](@entry_id:750754). A **state race** happens when an input change triggers a transition between two internal states whose binary encodings ([state assignment](@entry_id:172668)) differ by more than one bit. For example, a transition from a state encoded as $y_1y_2=00$ to one encoded as $y_1y_2=11$ requires both state variables to change. Since they will not change at precisely the same time, the circuit may momentarily pass through an intermediate state (`01` or `10`). The consequences of this race determine whether it is non-critical or critical.

A **non-[critical race](@entry_id:173597)** occurs when, regardless of the order in which the state variables change, the circuit is guaranteed to reach the same correct final stable state. The transient behavior might differ, but the final outcome is deterministic. This can be identified in a [flow table](@entry_id:175022) where two unstable states in the same column, reachable from different intermediate states, both direct the circuit to the same final stable state [@problem_id:1953725]. For example, if during a transition, the circuit could go to either state `A` or `E` (unstable for input `11`), and both the `A` and `E` rows for input `11` point to the same stable state `F`, the race is non-critical.

A **[critical race](@entry_id:173597)**, however, is a severe design fault. It occurs when the order of state variable changes can lead the circuit to different final stable states. The circuit's behavior becomes unpredictable. This hazard arises from an improper **[state assignment](@entry_id:172668)**. For instance, consider a transition from state $p$ (coded as `00`) to state $q$ (coded as `11`) for input `01` [@problem_id:1953690]. The Hamming distance between the state codes is 2.
- If $y_1$ changes first, the state becomes `10` (state `s`). From state `s` with input `01`, the [flow table](@entry_id:175022) might direct the circuit to stabilize at state `q`.
- If $y_2$ changes first, the state becomes `01` (state `r`). From state `r` with input `01`, the table might indicate that `r` is itself a stable state.

In this scenario, the final state could be `q` or `r`, depending on internal gate delays. This is a [critical race](@entry_id:173597) that renders the circuit unreliable. The prevention of critical races through careful [state assignment](@entry_id:172668) is a cornerstone of robust [asynchronous circuit design](@entry_id:172174), a topic that is a critical part of the overall design process.