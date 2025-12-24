## Introduction
Discrete-event and state-based modeling provides the formal bedrock for designing, analyzing, and controlling the complex, dynamic systems that define our modern technological landscape. From manufacturing automation to networked control, these formalisms are indispensable, particularly in the advanced fields of Cyber-Physical Systems (CPS) and their high-fidelity virtual counterparts, Digital Twins. The power of these models lies in their ability to abstract complex behavior into a structured representation of states and the events that trigger transitions between them, allowing for rigorous analysis and prediction.

However, a significant gap often exists between understanding the abstract theory of automata, [temporal logic](@entry_id:181558), and concurrency, and applying these concepts to solve tangible engineering problems. This article is designed to bridge that gap by systematically connecting foundational principles to practical applications. The reader will gain a comprehensive understanding of not just *what* these models are, but *how* they are used to ensure [system safety](@entry_id:755781), performance, and reliability.

To achieve this, the article is structured into three progressive chapters. We begin with **Principles and Mechanisms**, which lays the theoretical groundwork by exploring core formalisms like Labeled Transition Systems, [concurrency](@entry_id:747654) models, advanced tools such as Petri nets and [timed automata](@entry_id:1133177), and the logic for specifying system properties. Next, **Applications and Interdisciplinary Connections** demonstrates these theories in action, showing how they are used for performance analysis, [supervisory control](@entry_id:1132653) design, and the verification of hybrid and [real-time systems](@entry_id:754137). Finally, **Hands-On Practices** provides a set of targeted problems designed to solidify understanding through implementation, moving from theory to tangible skill.

## Principles and Mechanisms

This chapter delves into the fundamental principles and operational mechanisms that underpin discrete-event and state-based modeling. We will begin by establishing the core formalisms used to represent system structure, such as Labeled Transition Systems and automata. We will then explore the nuances of system behavior, including language semantics and notions of equivalence like [bisimulation](@entry_id:156097). Subsequently, we will examine methods for modeling concurrency and composing systems, followed by an introduction to advanced formalisms capable of representing resource contention and [real-time constraints](@entry_id:754130). Finally, we will discuss the principles of formal specification using temporal logic and the mechanisms of [deterministic simulation](@entry_id:261189).

### Foundational Models: Representing State and Events

At the heart of state-based modeling is the concept of a system that occupies a specific **state** at any given moment and changes state in response to the occurrence of an **event**. The most general and foundational mathematical structure for this is the **Labeled Transition System (LTS)**.

An LTS is formally a tuple $M=(S, \Sigma, \to, s_0)$, where:
- $S$ is a set of states.
- $\Sigma$ is a set of labels or events, often called the alphabet.
- $\to \subseteq S \times \Sigma \times S$ is a labeled transition relation. A transition $(s, a, s')$ is written as $s \xrightarrow{a} s'$.
- $s_0 \in S$ is the initial state.

This simple structure is remarkably powerful and forms the basis for many other formalisms  . In the context of modeling cyber-physical systems (CPS) and their digital twins, states can represent physical configurations (e.g., a robot's position), resource availability, or software variables. Events can represent sensor readings, actuator commands, or internal computational steps.

While the transition relation $\to$ is general, it is often convenient to work with a functional representation. This leads to the closely related formalism of an automaton or **Discrete-Event System (DES)**, often defined as a tuple $G=(X, E, f, x_0)$ . Here, $X$ is the state set, $E$ is the event set, and $f$ is a transition function that maps a state-event pair to a set of next states. The properties of this function $f$ define the nature of the automaton.

A key distinction in automaton theory is between deterministic and nondeterministic systems. A **Deterministic Finite Automaton (DFA)**, a cornerstone of computer science, imposes strict conditions: the set of states must be finite, and the transition function $\delta: Q \times \Sigma \to Q$ must be **total** and **single-valued**. "Total" means that for every state-event pair $(q, a)$, there is a defined next state. "Single-valued" means there is exactly one such next state . This guarantees that for any given input string of events, there is one unique path of execution.

However, many real-world systems do not conform to this strict determinism. Two important variations are crucial for practical modeling:

1.  **Partiality**: In many DES models, the transition function $f: X \times E \to X$ is **partial**, meaning it is not defined for all state-event pairs. If $f(x, e)$ is undefined, the event $e$ is said to be **disabled** at state $x$. This is a natural and direct way to model the physical or logical impossibility of an event occurring in a given situation. For instance, a command to move a robot arm might be disabled if a safety interlock is engaged. The system's behavior, or its **generated language**, consists only of event sequences corresponding to defined transitions. Making the function partial effectively prunes impossible traces from the system's behavior . This is distinct from modeling an infeasible event with a [self-loop](@entry_id:274670), $f(x, e) = x$, which implies the event *occurs* but the state does not change, thereby including the event in the trace. An undefined transition means the event does not occur at all.

2.  **Nondeterminism**: In some systems, an event can lead to one of several possible outcomes. This is modeled by allowing the transition function to be **set-valued**, i.e., $f: X \times \Sigma \to 2^X$, where $2^X$ is the [power set](@entry_id:137423) of $X$. For a given state $x$ and event $a$, $f(x, a)$ is the set of all possible next states. For example, after a "measure" event, a system might nondeterministically transition to a "high_value" or "low_value" state, abstracting away the precise conditions that determine the outcome. This [nondeterminism](@entry_id:273591) arises from abstraction, concurrency, or underspecification in a model .

### Behavioral Semantics and System Equivalence

Given a model, its most fundamental behavioral description is its language—the set of all possible finite sequences of events, or **traces**, that it can generate. For a system $G$ starting at $x_0$, the **generated language**, denoted $L(G)$, is the set of all traces $s \in \Sigma^*$ for which an execution path exists from $x_0$.

Nondeterminism introduces subtleties in defining behavior. When a trace can lead to multiple states, we must clarify what it means for a property to hold. This gives rise to two forms of semantics :
- **Existential (or "May") Semantics**: A property is said to hold if there exists *at least one* execution path for a trace that satisfies it. For example, the marked language $L_m(G)$ is the set of traces $s$ for which at least one resulting state is a marked (or accepting) state.
- **Universal (or "Must") Semantics**: A property is said to hold only if it is true for *all* possible execution paths for a trace. For instance, a trace $s$ might be considered "universally marked" only if *every* state reachable via $s$ is a marked state.

With a definition of behavior, we can ask when two systems are "the same." The most straightforward notion is **[trace equivalence](@entry_id:756080)**: two systems are trace equivalent if they generate the same language. However, this equivalence is often too coarse, as it ignores the branching structure of nondeterministic systems.

Consider two systems. System A, after event $a$, enters a state where it can perform either event $b$ or event $c$. System B, after event $a$, can nondeterministically choose to enter a state where only $b$ is possible, or a state where only $c$ is possible. Both systems have the same trace language $\{\epsilon, a, ab, ac\}$. However, in System A, the choice between $b$ and $c$ is made *after* event $a$, while in System B, the choice is resolved *with* event $a$. Trace equivalence cannot distinguish these two structurally different systems.

To capture such structural differences, a stronger notion of equivalence is needed: **(strong) [bisimulation](@entry_id:156097)**. Two states, $s_1$ and $s_2$, are said to be bisimilar if they can match each other's moves indefinitely. Formally, a relation $R$ between the states of two systems is a strong [bisimulation](@entry_id:156097) if for any pair $(s_1, s_2) \in R$:
1.  For any transition $s_1 \xrightarrow{a} s'_1$, there must exist a matching transition $s_2 \xrightarrow{a} s'_2$ such that the resulting states are also related, i.e., $(s'_1, s'_2) \in R$.
2.  Symmetrically, for any transition $s_2 \xrightarrow{a} s'_2$, there must exist a matching transition $s_1 \xrightarrow{a} s'_1$ such that $(s'_1, s'_2) \in R$.

Bisimulation equivalence is strictly stronger than [trace equivalence](@entry_id:756080): if two systems are bisimilar, they are necessarily trace equivalent. The converse is not true, as demonstrated by the example above  . This distinction is critical in verification, where preserving the branching properties of a system is often essential.

### Modeling Concurrency and Composition

Cyber-physical systems are inherently concurrent, with multiple components operating in parallel. Modeling this [concurrency](@entry_id:747654) is a central challenge. A common approach is to represent [concurrency](@entry_id:747654) via **interleaving**, where the behavior of the composite system includes all possible shuffles of the independent actions of its components.

A more sophisticated view is offered by **[partial order](@entry_id:145467) semantics**, which treats concurrent events as genuinely unordered rather than just arbitrarily ordered. **Mazurkiewicz traces** provide a formal basis for this view . The key idea is to define an **independence relation** $I \subseteq \Sigma \times \Sigma$ that identifies pairs of events that can occur concurrently without interfering with each other (e.g., reading two independent sensors). This relation induces an equivalence on traces: two traces are equivalent if one can be obtained from the other by swapping adjacent [independent events](@entry_id:275822). For example, if events $a$ and $b$ are independent, the sequential traces $abc$ and $bac$ are considered two different interleavings of the same single partially ordered execution, where $a$ and $b$ are concurrent and both precede $c$. This [equivalence class](@entry_id:140585) of traces is the Mazurkiewicz trace.

While [partial order](@entry_id:145467) semantics provides a powerful theoretical foundation, the most widely used mechanism for building models of concurrent systems is the **synchronous product** (or parallel composition), which is based on an interleaving and synchronization model. Given two LTSs, $M_1 = (S_1, \Sigma_1, \to_1, s_{1,0})$ and $M_2 = (S_2, \Sigma_2, \to_2, s_{2,0})$, and a set of shared synchronization events $\Sigma_s \subseteq \Sigma_1 \cap \Sigma_2$, their composition $M = M_1 \parallel_{\Sigma_s} M_2$ is defined as follows :

-   **State Space**: The composite state space is the Cartesian product $S_1 \times S_2$.
-   **Synchronization**: For a shared event $a \in \Sigma_s$, the composite system can perform an $a$-transition if and only if *both* $M_1$ and $M_2$ can perform an $a$-transition from their current states. This is known as **handshaking**. If one component is not ready to synchronize on a shared event, the other is blocked from performing it .
-   **Interleaving**: For a private (non-shared) event $a \in \Sigma_1 \setminus \Sigma_s$, $M_1$ can perform its transition while $M_2$ remains in its state (it "stutters"). Symmetrically, $M_2$ can perform its private events while $M_1$ stutters.

This composition operator allows engineers to model individual components and then formally combine them to create a model of the entire system, capturing their interactions through shared events.

### Advanced Modeling Formalisms

While LTS and automata are universal, certain system characteristics are more conveniently modeled using specialized formalisms. We will explore two such formalisms: Petri nets for resource management and [timed automata](@entry_id:1133177) for real-time systems.

#### Petri Nets

**Petri nets** are a graphical and [mathematical modeling](@entry_id:262517) tool particularly well-suited for describing systems with concurrency, resource sharing, and synchronization. A Petri net consists of **places** (drawn as circles), **transitions** (drawn as bars or rectangles), and directed arcs connecting them. The state of a Petri net, called its **marking**, is given by the distribution of **tokens** across its places.

The dynamic behavior is governed by the firing of transitions. A transition is enabled if each of its input places contains at least one token. When an enabled transition fires, it consumes one token from each input place and produces one token in each output place.

This dynamic can be captured elegantly using linear algebra . The structure of a net with $m$ places and $n$ transitions is encoded in its **[incidence matrix](@entry_id:263683)** $C \in \mathbb{Z}^{m \times n}$. The entry $C(i, j)$ represents the change in the number of tokens in place $p_i$ when transition $t_j$ fires. A sequence of firings can be represented by a vector $\sigma \in \mathbb{N}_0^n$, where $\sigma_j$ is the number of times transition $t_j$ has fired. The evolution of the marking from an initial marking $M_0$ to a new marking $M'$ is then given by the **state equation**:

$M' = M_0 + C \cdot \sigma$

This equation describes the set of all markings reachable from $M_0$. A powerful technique for analyzing Petri nets involves finding **place invariants**. A place invariant is a vector $y$ such that $y^\top C = 0$. This implies that for any reachable marking $M'$, the quantity $y^\top M'$ is constant: $y^\top M' = y^\top (M_0 + C\sigma) = y^\top M_0 + (y^\top C)\sigma = y^\top M_0$. Such invariants represent conservation laws in the system (e.g., "the total number of parts in the buffer and on the machine is always constant") and can be used to prove properties like [boundedness](@entry_id:746948), which ensures that the number of tokens in any place does not grow infinitely .

#### Timed Automata

Standard automata models are untimed; events are ordered, but the time elapsed between them is not represented. **Timed automata** extend [finite automata](@entry_id:268872) with a [finite set](@entry_id:152247) of real-valued **clocks** to model real-time systems . The semantics of a timed automaton is defined over states of the form $(s, v)$, where $s$ is a location (state) of the automaton and $v$ is a clock valuation mapping each clock to a non-negative real number.

Behavior in a timed automaton unfolds through two kinds of steps:
1.  **Time Elapse**: Time can pass, during which all clock values increase uniformly at the same rate. Time may only elapse as long as a **state invariant** is satisfied. An invariant is a condition on clock values associated with a location (e.g., $x \le 5$) that must hold true for the system to remain in that location.
2.  **Discrete Transitions**: The system can take an instantaneous transition from one location to another. A transition is enabled only if its associated **guard**—a condition on clock values (e.g., $x \ge 2$)—is satisfied by the current clock valuation. When a transition is taken, a specified subset of clocks can be **reset** to zero.

The interplay between guards, invariants, and resets allows for the specification of complex timing behavior. For example, a task can be constrained to take at least 1 time unit and at most 4 time units by resetting a clock $x$ upon entering the task's state, having a guard $x \ge 1$ on the transition that completes the task, and an invariant $x \le 4$ on the task's state . If time elapses such that an invariant is about to be violated (e.g., $x$ is about to exceed 4), the system is forced to take an available outgoing transition. This elegant mechanism is fundamental to the modeling and verification of real-time control systems.

### Formal Specification and Verification

Building a model is only part of the task; we must also be able to precisely specify the desired properties of that model and verify that they hold. Properties of reactive systems are typically classified into two main categories:

-   **Safety Properties**: These stipulate that "something bad never happens." Examples include [mutual exclusion](@entry_id:752349), absence of [deadlock](@entry_id:748237), or the property that a robot arm never enters a [forbidden zone](@entry_id:175956). A violation of a safety property can always be demonstrated by a finite trace.
-   **Liveness Properties**: These stipulate that "something good eventually happens." Examples include the property that every request is eventually granted or that a process will eventually terminate. A violation of a liveness property can only be confirmed by observing an infinite trace.

**Linear Temporal Logic (LTL)** is a [formal language](@entry_id:153638) used to specify such properties over infinite traces of events or states . LTL extends [propositional logic](@entry_id:143535) with temporal modalities that reason about the future:
-   $\mathbf{G} \phi$ (**Globally**): $\phi$ holds at the current time and at all future points. Often used for safety properties (e.g., $\mathbf{G}(\neg \mathrm{crash})$).
-   $\mathbf{F} \phi$ (**Finally/Eventually**): $\phi$ will hold at some future point. The canonical liveness operator (e.g., $\mathbf{G}(\mathrm{request} \rightarrow \mathbf{F} \mathrm{grant})$).
-   $\mathbf{X} \phi$ (**Next**): $\phi$ holds at the very next time step. Useful for specifying immediate responses (e.g., $\mathbf{G}(\mathrm{fault} \rightarrow \mathbf{X} \mathrm{reset})$).
-   $\phi \mathbf{U} \psi$ (**Until**): $\phi$ must hold until $\psi$ holds, and $\psi$ is guaranteed to eventually hold.
-   $\phi \mathbf{W} \psi$ (**Weak Until**): Either $\phi$ holds until $\psi$ holds, or $\phi$ holds forever (if $\psi$ never occurs).

The distinction between Strong Until ($\mathbf{U}$) and Weak Until ($\mathbf{W}$) is crucial. A requirement like "after an `estop`, no `move` may occur until a `reset`" must be formalized with Weak Until, as it allows for the possibility that a `reset` never occurs, in which case `move` remains forbidden forever. Using Strong Until would incorrectly require a `reset` to always eventually happen .

These formal specifications can be used in **[model checking](@entry_id:150498)**, an automated verification technique that algorithmically checks if a system model (like an LTS or timed automaton) satisfies a property specified in a logic like LTL. Safety properties can also be enforced by construction, for example, by modifying the model to remove all transitions that would lead to a forbidden state .

### Simulation Mechanisms

While the formalisms above describe the abstract behavior of a system, a **simulation** provides a concrete execution. A [discrete-event simulation](@entry_id:748493) kernel's task is to execute a model by processing events in chronological order. The core component of such a kernel is a **Future Event Set (FES)**, a [data structure](@entry_id:634264) (typically a [priority queue](@entry_id:263183)) that stores pending events, ordered by their scheduled time of occurrence.

A typical simulation loop proceeds as follows:
1.  Extract the event(s) with the minimum timestamp from the FES.
2.  Advance the simulation clock to this timestamp.
3.  Process the event(s).
4.  Processing an event may update the system state and schedule new events, which are inserted into the FES.

A critical challenge in this process is the deterministic handling of **simultaneous events**—multiple events scheduled for the same timestamp . If these events are processed sequentially in an arbitrary order, and the state is updated after each one, the final state can depend on this arbitrary ordering, making the simulation nondeterministic and non-repeatable.

The correct and deterministic approach is to treat all events at a given timestamp as logically simultaneous. This is achieved through a **macro-step/micro-step** execution model:
1.  **Macro-Step**: The simulation clock advances to the next timestamp $t^*$ present in the FES.
2.  **Micro-Steps**: An inner loop is initiated to process all events at time $t^*$. This loop follows a read-collect-write discipline:
    a. All events currently scheduled for time $t^*$ are identified.
    b. The reactions of *all* these events are computed based on the state *at the beginning* of the macro-step.
    c. The resulting state updates are collected and applied in a single write phase to produce the next state.
    d. These reactions may generate new events. Events scheduled for a future time ($>t^*$) are added to the FES. Events scheduled for the *current* time ($=t^*$) are collected to be processed in the next micro-step.
    e. This inner loop continues until no new instantaneous events are generated, a state known as **quiescence**. This process effectively computes a fixed point for the chain of instantaneous reactions at time $t^*$.

This mechanism ensures that the simulation outcome is independent of the internal processing order of simultaneous events, guaranteeing causality and determinism, which are essential for the analysis and validation of digital twins.