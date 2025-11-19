## Introduction
In modern control engineering, the ability to implement feedback based on a system's complete internal state is often the key to achieving high performance. State-feedback controllers rely on access to the full [state vector](@entry_id:154607), but in practice, it is rare to have sensors for every state variable due to cost, physical constraints, or technical feasibility. While full-order observers can reconstruct the entire state vector from output measurements, they introduce a critical question: why re-estimate states that are already being measured accurately? This inefficiency is the primary knowledge gap addressed by the **[reduced-order observer](@entry_id:178703)**, an elegant and powerful technique that focuses computational effort exclusively on the unmeasured states.

This article provides a comprehensive guide to understanding and implementing reduced-order observers. We will embark on a structured journey through three key chapters. First, in **Principles and Mechanisms**, we will dissect the theoretical foundation of the observer, from the logic of state partitioning to the [pole placement](@entry_id:155523) design that guarantees stable estimation. Next, in **Applications and Interdisciplinary Connections**, we will explore the remarkable versatility of this method, showcasing its use in fields ranging from aerospace and chemical engineering to biomedical systems, and even for estimating unknown disturbances. Finally, in **Hands-On Practices**, you will have the opportunity to solidify your understanding by working through practical design problems, bridging the gap between theory and real-world application.

## Principles and Mechanisms

In the study of control systems, the ability to estimate the internal state of a plant is foundational for implementing [state-feedback control](@entry_id:271611). While a full-order observer provides a robust method for estimating the entire state vector, it can be both computationally inefficient and suboptimal in performance, particularly when some states are already accessible through direct measurement. This chapter delves into the principles and mechanisms of the **[reduced-order observer](@entry_id:178703)**, an elegant and efficient alternative that leverages available measurements to simplify the estimation task.

### The Rationale for Reduced-Order Estimation

The fundamental motivation for a [reduced-order observer](@entry_id:178703) stems from a simple question: If we can directly and accurately measure a portion of the system's state, why should we expend computational resources to estimate it again? A full-order observer, by design, reconstructs the entire $n$-dimensional [state vector](@entry_id:154607), creating an $n$-dimensional dynamic system. In contrast, a [reduced-order observer](@entry_id:178703) only estimates the components of the state that are *not* directly available from the measurements.

Consider a system with $n$ state variables and $p$ independent outputs, where $p \lt n$. A full-order observer implements $n$ dynamic [state equations](@entry_id:274378). A [reduced-order observer](@entry_id:178703), however, only needs to estimate the $n-p$ unmeasured [state variables](@entry_id:138790) or their combinations, thus requiring a dynamic system of only order $n-p$ [@problem_id:1604231]. The computational savings can be substantial. For instance, in a large-scale structural model with $n=10$ states and $p=9$ direct measurements (a common scenario where many sensor placements are feasible), a full-order observer requires 10 dynamic states. A [reduced-order observer](@entry_id:178703) only needs to estimate the single unmeasured state, representing a fractional reduction of $p/n = 9/10 = 0.9$ in the observer's dynamic order [@problem_id:1604212]. This reduction in complexity is critical for implementation on hardware with limited processing power.

Beyond computational efficiency, a [reduced-order observer](@entry_id:178703) can offer superior estimation performance. A full-order observer processes the measured output $y(t)$ to correct its estimate of the entire state vector, including the states that are being directly measured. If the measurement of a state is very precise (i.e., has low noise), the filtering process within a full-order observer can paradoxically degrade this high-quality information by mixing it with estimates derived from noisier process dynamics. A [reduced-order observer](@entry_id:178703), by its structure, accepts the measured states as true and focuses its efforts exclusively on the unmeasured ones. This can lead to a significantly lower estimation error variance for the unmeasured states, as it avoids corrupting the clean measurement data [@problem_id:1604249].

### The Principle of State Partitioning

The design of a [reduced-order observer](@entry_id:178703) is predicated on a formal separation of the [state vector](@entry_id:154607) into "measured" and "unmeasured" components. For a linear time-invariant (LTI) system given by:

$$
\begin{aligned}
\dot{x}(t) = Ax(t) + Bu(t) \\
y(t) = Cx(t)
\end{aligned}
$$

where $x \in \mathbb{R}^n$, $y \in \mathbb{R}^p$, and the output matrix $C$ has full row rank $p$. The equation $y(t) = Cx(t)$ provides $p$ independent algebraic constraints on the state vector $x(t)$. The core idea is to use these constraints to reduce the dynamic estimation problem.

This is best illustrated by performing a state coordinate transformation. Since $C$ has rank $p$, we can always find a non-singular [transformation matrix](@entry_id:151616) $T \in \mathbb{R}^{n \times n}$ that transforms the state $x$ into a new state $z = Tx$, partitioned such that the measured output $y$ constitutes part of the new [state vector](@entry_id:154607) [@problem_id:2737319]. For conceptual clarity and without loss of generality, we can assume the system coordinates are already in a form where the first $p$ states are directly measured. This is equivalent to an output matrix of the form $C = \begin{pmatrix} I_p & 0 \end{pmatrix}$, and the [state vector](@entry_id:154607) $x$ is partitioned as:

$$
x(t) = \begin{pmatrix} x_a(t) \\ x_b(t) \end{pmatrix}
$$

Here, $x_a \in \mathbb{R}^p$ is the vector of measured states and $x_b \in \mathbb{R}^{n-p}$ is the vector of unmeasured states. The output equation simplifies to $y(t) = x_a(t)$ [@problem_id:1604223].

Conformably with this partition, the state dynamics can be written as:

$$
\begin{pmatrix} \dot{x}_a(t) \\ \dot{x}_b(t) \end{pmatrix} = \begin{pmatrix} A_{aa} & A_{ab} \\ A_{ba} & A_{bb} \end{pmatrix} \begin{pmatrix} x_a(t) \\ x_b(t) \end{pmatrix} + \begin{pmatrix} B_a \\ B_b \end{pmatrix} u(t)
$$

Our objective is to design a dynamic system that provides an estimate $\hat{x}_b(t)$ of the unmeasured state $x_b(t)$, which should converge to the true value, i.e., $x_b(t) - \hat{x}_b(t) \to 0$.

### Mechanism of the Observer

To derive the observer dynamics, we can examine the partitioned system equations. The dynamics of the unmeasured state $x_b$ are:

$$
\dot{x}_b = A_{bb}x_b + A_{ba}x_a + B_b u
$$

This equation suggests that the evolution of $x_b$ is driven by itself ($A_{bb}x_b$) and a set of known inputs ($A_{ba}x_a + B_b u$, since $x_a=y$ and $u$ are known). A naive estimator might simply copy these dynamics, but this would not correct for errors in the initial estimate.

To introduce error correction, we utilize the dynamics of the measured state, $x_a$:

$$
\dot{x}_a = A_{aa}x_a + A_{ab}x_b + B_a u
$$

We can rearrange this equation to express a quantity involving the unmeasured state $x_b$ in terms of known signals:

$$
A_{ab}x_b = \dot{x}_a - A_{aa}x_a - B_a u
$$

This equation can be viewed as an "output" of a system whose state is $x_b$. We can compare the measured value of this "output" (the right-hand side) with its estimated value, $A_{ab}\hat{x}_b$. The difference represents an error that can be used for correction. However, the term $\dot{x}_a = \dot{y}$ requires differentiation of the output signal, a process that is highly sensitive to noise and generally avoided in practical implementations.

The solution, pioneered by David Luenberger, is to define an auxiliary state variable for the observer that implicitly contains the necessary correction term without explicit differentiation. Let the observer's estimate for $x_b$ be constructed as:

$$
\hat{x}_b(t) = \eta(t) + L y(t)
$$

where $\eta(t) \in \mathbb{R}^{n-p}$ is the internal state of the [reduced-order observer](@entry_id:178703) and $L \in \mathbb{R}^{(n-p) \times p}$ is a constant **[observer gain](@entry_id:267562) matrix** to be designed. The term $Ly(t)$ acts as a feedforward from the measurement. The dynamics of $\eta(t)$ are then designed to ensure that the [estimation error](@entry_id:263890) for $x_b$ converges to zero.

Let's define the [estimation error](@entry_id:263890) for the unmeasured state as $\tilde{x}_b(t) = x_b(t) - \hat{x}_b(t)$. Substituting the definition of $\hat{x}_b$ and using $y=x_a$, we have:

$$
\tilde{x}_b = x_b - (\eta + L x_a) \implies \eta = x_b - L x_a - \tilde{x}_b
$$

By carefully deriving the dynamics for $\dot{\eta}(t)$ that mimic the structure of the system while ensuring the error $\tilde{x}_b$ has stable dynamics, one can arrive at a practical observer implementation. The final dynamics of the observer's internal state $\eta(t)$ take the form:

$$
\dot{\eta}(t) = (A_{bb}-LA_{ab})\eta(t) + \left(A_{ba}-LA_{aa} + (A_{bb}-LA_{ab})L\right)y(t) + (B_b-LB_a)u(t)
$$

This equation describes the $(n-p)$-dimensional dynamics of the [reduced-order observer](@entry_id:178703). It is driven by the known plant input $u(t)$ and output $y(t)$ [@problem_id:1604223]. The full state estimate is then reconstructed algebraically: the measured part is known, $\hat{x}_a(t) = y(t)$, and the unmeasured part is calculated as $\hat{x}_b(t) = \eta(t) + L y(t)$. This structure perfectly embodies the observer's operating principle: it propagates the estimate of the unmeasured component dynamically, while reconstructing the full state estimate algebraically [@problem_id:2737319].

### Error Dynamics and Pole Placement

The true power of this observer structure lies in the simplicity of its error dynamics. By taking the time derivative of the error, $\dot{\tilde{x}}_b = \dot{x}_b - \dot{\hat{x}}_b$, and substituting the plant and observer dynamics, a remarkable cancellation of terms occurs. The resulting error dynamics are governed by the homogeneous [linear differential equation](@entry_id:169062) [@problem_id:1604227]:

$$
\dot{\tilde{x}}_b(t) = (A_{bb} - L A_{ab}) \tilde{x}_b(t)
$$

This elegant result is the cornerstone of [reduced-order observer](@entry_id:178703) design. It shows that the [estimation error](@entry_id:263890) $\tilde{x}_b(t)$ converges to zero if and only if the characteristic matrix of the error dynamics, $M = A_{bb} - L A_{ab}$, is Hurwitz (i.e., all its eigenvalues have negative real parts) [@problem_id:1604262].

Crucially, the [observer gain](@entry_id:267562) matrix $L$ provides a degree of freedom to shape these dynamics. The eigenvalues of $(A_{bb} - L A_{ab})$, often called the **observer poles**, determine the rate at which the [estimation error](@entry_id:263890) decays. We can choose these poles to make the convergence as fast as desired. The ability to place these poles arbitrarily at any self-conjugate locations in the complex plane is guaranteed if and only if the pair of matrices $(A_{bb}, A_{ab})$ is **observable** [@problem_id:1604245].

This condition has a deep connection to the properties of the original system. It can be shown that the pair $(A_{bb}, A_{ab})$ is observable if and only if the original system pair $(A, C)$ is observable. This highlights a fundamental prerequisite: one cannot hope to estimate unmeasured states if they are not observable from the system's output in the first place.

### Duality with State-Feedback Control

The design problem of finding a gain $L$ to place the eigenvalues of $(A_{bb} - L A_{ab})$ is mathematically dual to the state-feedback [pole placement](@entry_id:155523) problem. Specifically, it is equivalent to finding a state-[feedback gain](@entry_id:271155) $K$ to place the poles of a regulator system $(F-GK)$ where the system matrices are $F=A_{bb}^T$ and $G=A_{ab}^T$.

This principle of **duality** is immensely practical. It implies that any algorithm used for [state-feedback controller design](@entry_id:270917), such as Ackermann's formula or numerical software functions, can be directly applied to find the [observer gain](@entry_id:267562) $L$. If one designs a feedback gain $K_{reg}$ for the dual system defined by $(A_{bb}^T, A_{ab}^T)$, the required [observer gain](@entry_id:267562) is simply the transpose of the [controller gain](@entry_id:262009), $L = K_{reg}^T$ [@problem_id:1604273]. This provides a systematic and powerful method for observer design.

### A Critical Prerequisite: System Detectability

The entire framework of observer design, whether full or reduced-order, rests upon the fundamental system property of **detectability**. A system $(A,C)$ is detectable if all its [unobservable modes](@entry_id:168628) are asymptotically stable. If a system has an unstable mode that is unobservable, the state associated with this mode will grow without bound, and no observer, which relies solely on the output $y=Cx$, can ever track or stabilize it.

Attempting to apply the state-partitioning mechanism to a non-detectable system will not resolve this issue. A coordinate transformation and partitioning of a non-detectable system $(A,C)$ will invariably lead to a pair $(A_{bb}, A_{ab})$ that is also non-detectable [@problem_id:1604209]. Consequently, the error dynamics matrix $(A_{bb} - L A_{ab})$ will have uncontrollable, unstable eigenvalues for any choice of gain $L$, making it impossible to design an observer that guarantees the [estimation error](@entry_id:263890) converges to zero. Therefore, the very first step in any observer design must be to verify the detectability of the plant $(A,C)$. If arbitrary [pole placement](@entry_id:155523) is desired, the stronger condition of [observability](@entry_id:152062) must be confirmed.