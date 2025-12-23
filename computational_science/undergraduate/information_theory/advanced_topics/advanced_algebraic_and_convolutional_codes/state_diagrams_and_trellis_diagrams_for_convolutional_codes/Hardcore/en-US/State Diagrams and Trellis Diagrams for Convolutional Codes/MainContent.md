## Introduction
Convolutional codes are a cornerstone of modern digital communications, offering powerful error-correction capabilities that ensure reliable [data transmission](@entry_id:276754) across noisy channels. Unlike simpler block codes, their defining feature is **memory**: the encoded output at any moment depends not only on the current input but also on a finite history of past inputs. This property allows for the creation of exceptionally robust codes but also introduces a layer of complexity that requires specialized tools for analysis and decoding. The primary challenge lies in visualizing and navigating the intricate web of dependencies created by the encoder's internal states.

This article provides a comprehensive exploration of the graphical tools designed to master this complexity: state diagrams and trellis diagrams. By translating the algebraic properties of an encoder into an intuitive visual format, these diagrams unlock a deeper understanding of the code's behavior. The journey begins in the **Principles and Mechanisms** chapter, where we will construct these diagrams from the ground up, linking them to encoder memory and [generator polynomials](@entry_id:265173). Next, the **Applications and Interdisciplinary Connections** chapter will reveal their true power, showing how they form the basis for the celebrated Viterbi decoding algorithm, guide the design of superior codes, and connect to advanced topics like Trellis-Coded Modulation. Finally, the **Hands-On Practices** section provides targeted exercises to reinforce these concepts and build practical skills.

## Principles and Mechanisms

A convolutional encoder, at its core, is a [finite-state machine](@entry_id:174162). Its behavior is governed by its current internal state and the incoming data stream. Unlike block codes, which operate on fixed, independent blocks of data, a convolutional encoder has **memory**, meaning that the output generated at any given time depends not only on the current input bit but also on a finite number of previous input bits. This chapter will explore the fundamental principles that define a convolutional encoder's behavior and the primary mechanisms—state diagrams and trellis diagrams—used to represent and analyze it.

### The Encoder as a Finite-State Machine

The "memory" of a convolutional encoder is captured by its **state**. For a typical feedforward (non-recursive) binary encoder, the state is simply the set of the most recent $m$ input bits stored in its internal [shift register](@entry_id:167183), where $m$ is the **memory order** of the encoder. Since each of the $m$ memory elements can hold either a 0 or a 1, the total number of distinct internal configurations, or states, is $N_{\text{states}} = 2^m$.

This relationship is fundamental. For example, if an analysis of an encoder reveals that it has a total of 8 unique internal states, we can directly infer its memory. By solving the equation $8 = 2^m$, we find that the memory order is $m=3$, as $2^3=8$ . The memory order $m$ is one of the most critical parameters of a convolutional code, as it determines the code's complexity and its error-correcting capability.

The concept of memory and state can be generalized for more complex encoders, such as those that accept multiple input streams simultaneously. For a rate $R = k/n$ encoder that processes $k$ input streams to produce $n$ output streams, the total memory is not a single number but is determined by the specific connections for each input stream. The encoder is defined by a $k \times n$ **[generator matrix](@entry_id:275809)** $G(D)$, where each entry is a polynomial in the delay operator $D$. The memory required for the $i$-th input stream, denoted $m_i$, is the highest degree of any polynomial in the $i$-th row of $G(D)$. The **total memory** of the encoder, often denoted by $\nu$, is the sum of the individual memory requirements: $\nu = \sum_{i=1}^{k} m_i$. The total number of states is then $2^\nu$.

Consider a hypothetical rate $R=2/3$ encoder specified by the [generator matrix](@entry_id:275809) :
$$
G(D) = \begin{pmatrix} 1+D^2  & 1+D  & 1 \\ 1+D  & D  & 1+D+D^2 \end{pmatrix}
$$
For the first input stream (row 1), the polynomial degrees are $2, 1, 0$. The maximum degree is $m_1 = 2$. For the second input stream (row 2), the polynomial degrees are $1, 1, 2$, giving a maximum of $m_2 = 2$. The total memory is $\nu = m_1 + m_2 = 2 + 2 = 4$. Consequently, a [state diagram](@entry_id:176069) for this encoder would require $2^4 = 16$ distinct states.

### The State Diagram: A Compact Representation

The most fundamental graphical representation of a convolutional encoder's behavior is the **[state diagram](@entry_id:176069)**. This is a directed graph where each node represents one of the $2^m$ possible states of the encoder. Directed edges, or branches, represent the transitions between states. Since a transition is caused by a new input bit, there are two outgoing branches from each state in a binary encoder: one for an input of '0' and one for an input of '1'.

Each branch is labeled with the "input / output" pair that corresponds to that transition. This compact diagram contains all the information necessary to understand the encoder's operation in a time-invariant manner. To construct a [state diagram](@entry_id:176069), one must systematically determine the next state and the output for every possible combination of current state and input.

Let's illustrate this with an example. Consider a rate $1/2$ encoder with memory $m=2$. The state at time $k$ is given by the two previous inputs, $s_k = (u_{k-1}, u_{k-2})$. The four possible states are $S_0=(0,0)$, $S_1=(0,1)$, $S_2=(1,0)$, and $S_3=(1,1)$. The encoder's logic is given by the output equations (where $\oplus$ denotes addition modulo-2, or XOR):
$$
v_k^{(0)} = u_k \oplus u_{k-1} \oplus u_{k-2}
$$
$$
v_k^{(1)} = u_k \oplus u_{k-2}
$$
The state update rule is that of a shift register: the new input $u_k$ enters the memory, and the oldest bit is discarded. Thus, the next state is $s_{k+1} = (u_k, u_{k-1})$.

To determine the transitions from a specific state, say $S_2=(1,0)$, we analyze the two possible inputs :
- **Current State:** $s_k = (u_{k-1}, u_{k-2}) = (1,0)$.
- **Case 1: Input $u_k=0$.**
  - **Output:**
    $v_k^{(0)} = 0 \oplus 1 \oplus 0 = 1$
    $v_k^{(1)} = 0 \oplus 0 = 0$
    The output pair is $(1,0)$.
  - **Next State:**
    $s_{k+1} = (u_k, u_{k-1}) = (0,1)$, which corresponds to state $S_1$.
  - This gives a branch from $S_2$ to $S_1$ with the label "0 / 10".
- **Case 2: Input $u_k=1$.**
  - **Output:**
    $v_k^{(0)} = 1 \oplus 1 \oplus 0 = 0$
    $v_k^{(1)} = 1 \oplus 0 = 1$
    The output pair is $(0,1)$.
  - **Next State:**
    $s_{k+1} = (u_k, u_{k-1}) = (1,1)$, which corresponds to state $S_3$.
  - This gives a branch from $S_2$ to $S_3$ with the label "1 / 01".

By repeating this process for all four states, the complete [state diagram](@entry_id:176069) is constructed. This diagram serves as a complete and timeless blueprint of the encoder's functionality.

### Structural Properties and Variations

While a [state diagram](@entry_id:176069) can be drawn for any [finite-state machine](@entry_id:174162), the diagrams for standard convolutional encoders have a specific, constrained structure due to their shift-register-based memory. The next state, $s_{k+1}$, is determined solely by the current input $u_k$ and the first $m-1$ bits of the current state $s_k$. Specifically, for a state $s_k=(s_{k,1}, s_{k,2}, \dots, s_{k,m})$, the next state is $s_{k+1}=(u_k, s_{k,1}, \dots, s_{k,m-1})$.

This implies a rigid connectivity pattern. From any two states that share the same first $m-1$ bits, say $(a_1, \dots, a_{m-1}, 0)$ and $(a_1, \dots, a_{m-1}, 1)$, an input of $u_k$ must lead to the same next state, $(u_k, a_1, \dots, a_{m-1})$. A set of transitions that violates this principle cannot represent a standard convolutional encoder. For instance, a proposed set of transitions where state A transitions to A (on input 0) and C (on input 1), while state C transitions to A (on input 0) and D (on input 1), can be shown to be invalid. If we assume a shift-register structure, the first set of transitions implies that A and C differ only in their first memory bit. However, the transitions from C then lead to a logical contradiction, proving that the proposed state machine cannot be realized with a standard shift-register architecture .

An important classification of [convolutional codes](@entry_id:267423) is whether they are **systematic**. A code is systematic if one of its output streams is an identical, uncoded copy of the input stream. For a rate $R=1/2$ encoder with outputs $(c_1, c_2)$, the code is systematic if either $c_1 = u$ for all time or $c_2 = u$ for all time. This property can be verified by inspecting the [state diagram](@entry_id:176069). For every branch in the diagram, one of the output bits in the "u / c1c2" label must match the input bit $u$. If this holds for all transitions for the same output position (e.g., always $c_1$), the code is systematic. This is a desirable property in some applications as it simplifies certain aspects of decoding and [synchronization](@entry_id:263918) .

### Encoding a Message Sequence

With a complete description of the encoder—either through its [generator polynomials](@entry_id:265173), a [state transition table](@entry_id:163350), or a [state diagram](@entry_id:176069)—we can find the output codeword for any given input message. The process involves starting at a known initial state (typically the all-zero state, where all memory elements are 0) and tracing the path dictated by the input sequence.

Let's trace the encoding of the input message $u = (1, 0, 1, 1)$ using an encoder with memory $m=2$ and generator sequences $g_1 = (1, 1, 1)$ and $g_2 = (1, 0, 1)$. The state is $s_t = (u_{t-1}, u_{t-2})$, and the outputs are $y_{1,t} = u_t \oplus u_{t-1} \oplus u_{t-2}$ and $y_{2,t} = u_t \oplus u_{t-2}$, with all arithmetic modulo-2 .

- **Initial State:** At $t=1$, the encoder is in state $s_1 = (u_0, u_{-1}) = (0, 0)$.
  - **Input $u_1=1$:** Output is $(1\oplus 0\oplus 0, 1\oplus 0) = (1,1)$. Next state is $s_2 = (u_1, u_0) = (1,0)$.
- **Time $t=2$:** Current state is $s_2=(1,0)$.
  - **Input $u_2=0$:** Output is $(0\oplus 1\oplus 0, 0\oplus 0) = (1,0)$. Next state is $s_3 = (u_2, u_1) = (0,1)$.
- **Time $t=3$:** Current state is $s_3=(0,1)$.
  - **Input $u_3=1$:** Output is $(1\oplus 0\oplus 1, 1\oplus 1) = (0,0)$. Next state is $s_4 = (u_3, u_2) = (1,0)$.
- **Time $t=4$:** Current state is $s_4=(1,0)$.
  - **Input $u_4=1$:** Output is $(1\oplus 1\oplus 0, 1\oplus 0) = (0,1)$. Final state is $s_5 = (u_4, u_3) = (1,1)$.

Concatenating the output pairs yields the final codeword: `11100001`. This step-by-step procedure is the fundamental mechanism of encoding, whether followed manually as shown here, or implemented in hardware or software  .

### The Trellis Diagram: Unrolling in Time

While the [state diagram](@entry_id:176069) is an excellent compact representation, it is less suited for visualizing the path of a specific sequence over time. For this, we use a **[trellis diagram](@entry_id:261673)**. The trellis unrolls the [state diagram](@entry_id:176069) along a time axis. It consists of columns of nodes, where each column represents the set of all possible states at a [discrete time](@entry_id:637509) step $t$. Branches connect the states at time $t$ to the states at time $t+1$, corresponding exactly to the transitions in the [state diagram](@entry_id:176069).

The crucial insight is that for a time-invariant encoder, the structure of connections between any two adjacent time steps, $t$ and $t+1$, is identical. In fact, a single time-section of the [trellis diagram](@entry_id:261673) is structurally identical to the [state diagram](@entry_id:176069) itself . The trellis's power comes from making the temporal evolution of the state explicit. An input message sequence of length $L$ corresponds to a unique path of length $L$ through the trellis, starting from the initial state. The sequence of labels on the branches of this path gives the corresponding output codeword. This path-based representation is the foundation for the most powerful decoding algorithms for [convolutional codes](@entry_id:267423), most notably the Viterbi algorithm.

### Trellis Termination for Block Coding

Convolutional codes are designed to operate on a continuous stream of data. However, in many practical packet-based or block-based communication systems, we transmit finite-length messages. This raises the question of how to handle the start and end of a block. If the encoder is left in an arbitrary state at the end of a message, the decoder has no known end-point to work towards, which complicates decoding.

The standard solution is **[trellis termination](@entry_id:262014)**. This is the process of forcing the encoder from its final state after processing the message back to the known all-zero state. For non-recursive, feedforward encoders, this is achieved simply by appending a sequence of $m$ zero-bits, known as **tail bits**, to the end of the message block. Each zero that is input shifts one more zero into the encoder's shift register. After $m$ such inputs, the register is guaranteed to be filled with zeros, meaning the encoder has returned to the all-zero state . This action ensures that the encoded block corresponds to a path in the trellis that starts at the all-zero state and ends at the all-zero state, providing well-defined boundaries that are essential for optimal decoding.