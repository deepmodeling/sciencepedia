## Introduction
In the study of [modern control systems](@entry_id:269478), the [state-space representation](@entry_id:147149) provides a powerful framework for analyzing the behavior of dynamic systems. However, analysis alone is often not enough; the ultimate goal of control engineering is synthesis—the active design of controllers to shape a system's behavior to meet desired performance objectives. This article addresses the fundamental question: How can we systematically alter a system's dynamics to make it stable, fast, and accurate? The answer lies in the elegant and potent technique of [state-feedback control](@entry_id:271611).

This article will guide you through the theory and application of [state-feedback controller](@entry_id:203349) design, moving from core principles to practical implementation strategies. Across three chapters, you will gain a deep, practical understanding of this cornerstone of control theory.

The journey begins in **Principles and Mechanisms**, where we will dissect the structure of a state-feedback law and explore how it modifies a system's internal dynamics. You will learn the central design technique of [pole placement](@entry_id:155523) and discover the critical prerequisite of controllability, which determines the limits of what can be achieved.

Next, in **Applications and Interdisciplinary Connections**, we will see these principles in action. This chapter demonstrates how state-feedback is used to stabilize inherently unstable systems like magnetic levitators, prescribe specific transient responses, and achieve perfect tracking using [integral control](@entry_id:262330). We will also bridge the crucial gap between theory and practice by introducing state observers, which allow state-feedback to be implemented even when not all states are measurable.

Finally, **Hands-On Practices** will solidify your understanding by walking you through concrete design problems. You will apply the techniques learned to calculate feedback gains, analyze performance trade-offs, and build an intuitive feel for the relationship between pole locations and system response. By the end, you will be equipped with the knowledge to design controllers that actively command a system's behavior.

## Principles and Mechanisms

Having established the foundational concepts of [state-space representation](@entry_id:147149), this chapter delves into the principles and mechanisms of one of the most powerful techniques in modern control theory: **[state-feedback control](@entry_id:271611)**. Our objective is to move beyond mere analysis of a system's inherent behavior and into the realm of synthesis—actively designing controllers to modify that behavior to meet specific performance objectives. We will explore how to systematically alter a system's dynamics, what fundamental limitations govern our ability to do so, and how to ensure the controlled system accurately responds to external commands.

### The Structure of State-Feedback Control

The core idea of state-feedback is to use the full internal state of a system to compute a corrective control action. Consider a linear time-invariant (LTI) system, often referred to as the "plant," described by the state equation:
$$
\dot{\mathbf{x}}(t) = A\mathbf{x}(t) + B\mathbf{u}(t)
$$
Here, $\mathbf{x}(t) \in \mathbb{R}^n$ is the **[state vector](@entry_id:154607)**, a collection of variables that completely describes the internal energetic state of the system at time $t$. The vector $\mathbf{u}(t) \in \mathbb{R}^m$ is the **control input**, which we can manipulate to influence the system's evolution.

In the simplest form of state-feedback, known as a regulator, the goal is to stabilize the system around its equilibrium point (typically the origin, $\mathbf{x} = \mathbf{0}$). This is achieved by generating a control input that is a [linear combination](@entry_id:155091) of the state variables:
$$
\mathbf{u}(t) = -K\mathbf{x}(t)
$$
Here, $K$ is a constant $m \times n$ matrix known as the **state-[feedback gain](@entry_id:271155) matrix**. The negative sign is a convention, reflecting the typical use of [negative feedback](@entry_id:138619) to reduce error.

When this control law is applied to the plant, the system's dynamics are fundamentally altered. By substituting the control law into the state equation, we obtain the dynamics of the **closed-loop system**:
$$
\dot{\mathbf{x}}(t) = A\mathbf{x}(t) + B(-K\mathbf{x}(t)) = (A - BK)\mathbf{x}(t)
$$
The behavior of the controlled system is now governed by a new system matrix, $A_{cl} = A - BK$. The [feedback gain](@entry_id:271155) matrix $K$ provides a powerful mechanism to reshape the system's natural dynamics, represented by $A$, into the desired closed-loop dynamics, represented by $A_{cl}$.

For instance, consider a one-dimensional [magnetic levitation](@entry_id:275771) system modeled with state matrix $A = \begin{pmatrix} 0  1 \\ 4  -2 \end{pmatrix}$ and input matrix $B = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$ [@problem_id:1614716]. If we apply a [state-feedback control](@entry_id:271611) law with gain matrix $K = \begin{pmatrix} 5  3 \end{pmatrix}$, the crucial matrix product $BK$ becomes:
$$
BK = \begin{pmatrix} 0 \\ 1 \end{pmatrix} \begin{pmatrix} 5  3 \end{pmatrix} = \begin{pmatrix} 0  0 \\ 5  3 \end{pmatrix}
$$
The resulting closed-loop [system matrix](@entry_id:172230) is then:
$$
A_{cl} = A - BK = \begin{pmatrix} 0  1 \\ 4  -2 \end{pmatrix} - \begin{pmatrix} 0  0 \\ 5  3 \end{pmatrix} = \begin{pmatrix} 0  1 \\ -1  -5 \end{pmatrix}
$$
The original system, with eigenvalues of $A$ at approximately $-3.24$ and $1.24$, is unstable. The new system, governed by $A_{cl}$, has its eigenvalues at approximately $-4.79$ and $-0.21$, rendering it stable. This simple calculation demonstrates the profound impact of [state feedback](@entry_id:151441).

Most control systems are designed not just to be stable but to follow external commands. This introduces a third key signal: the **reference input**, denoted $r(t)$, which specifies the desired setpoint or target for the system's state or output. In this more general architecture, the control input is computed as:
$$
\mathbf{u}(t) = N\mathbf{r}(t) - K\mathbf{x}(t)
$$
where $N$ is a feedforward [scaling matrix](@entry_id:188350). The trio of signals—the [state vector](@entry_id:154607) $\mathbf{x}(t)$, control input $\mathbf{u}(t)$, and reference input $\mathbf{r}(t)$—form the basic vocabulary of state-feedback design [@problem_id:1614717].

### The Principle of Pole Placement

The stability and transient response characteristics (such as speed of response and overshoot) of an LTI system are completely determined by the locations of the eigenvalues of its state matrix. In the Laplace domain, these eigenvalues are the roots of the characteristic polynomial, and are thus known as the system's **poles**.

Since [state feedback](@entry_id:151441) modifies the system matrix to $A_{cl} = A - BK$, it directly modifies the poles of the system. The central design methodology of state-feedback is therefore **[pole placement](@entry_id:155523)**: the procedure of choosing the gain matrix $K$ to place the closed-loop poles at desired locations in the complex plane that correspond to a desired system performance.

The closed-loop poles are the roots of the [characteristic equation](@entry_id:149057) $\det(sI - A_{cl}) = 0$, where $s$ is the Laplace variable. Our goal is to select $K$ such that the [characteristic polynomial](@entry_id:150909) $\det(sI - (A - BK))$ matches a target polynomial $\phi_{des}(s)$ whose roots are the desired poles.

Let's illustrate this with a concrete example. Suppose we have a system with matrices $A = \begin{pmatrix} 0  1 \\ 3  -2 \end{pmatrix}$ and $B = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$, and we choose a feedback gain $K = \begin{pmatrix} 5  4 \end{pmatrix}$ [@problem_id:1614750]. The closed-loop matrix is:
$$
A_{cl} = A - BK = \begin{pmatrix} 0  1 \\ 3  -2 \end{pmatrix} - \begin{pmatrix} 0 \\ 1 \end{pmatrix} \begin{pmatrix} 5  4 \end{pmatrix} = \begin{pmatrix} 0  1 \\ -2  -6 \end{pmatrix}
$$
The characteristic polynomial of this closed-loop system is:
$$
\det(sI - A_{cl}) = \det \begin{pmatrix} s  -1 \\ 2  s+6 \end{pmatrix} = s(s+6) - (-1)(2) = s^2 + 6s + 2
$$
The roots of this polynomial, which are the closed-loop poles, dictate the final system behavior.

The power of this method lies in working backwards. We can start with performance specifications, translate them into desired pole locations, construct the corresponding target characteristic polynomial, and then solve for the required gain matrix $K$. For a standard second-order system, performance is often specified by the **natural frequency** $\omega_n$ and the **[damping ratio](@entry_id:262264)** $\zeta$. These parameters define the desired [characteristic polynomial](@entry_id:150909):
$$
\phi_{des}(s) = s^2 + 2\zeta\omega_n s + \omega_n^2
$$
By equating the coefficients of this polynomial with those of $\det(sI - (A-BK))$, which will be functions of the unknown gains in $K$, we can solve for the gains. For instance, to control a drone's vertical dynamics [@problem_id:1614777] with $\omega_n = 2.0$ rad/s and $\zeta = 0.707$, the desired polynomial is $s^2 + 2(0.707)(2)s + 2^2 \approx s^2 + 2.828s + 4$. If the system's [characteristic polynomial](@entry_id:150909) with symbolic gains $k_1$ and $k_2$ is $s^2 + 5k_2 s + 5k_1$, we can find the gains by matching coefficients: $5k_1 = 4 \Rightarrow k_1 = 0.8$ and $5k_2 = 2.828 \Rightarrow k_2 \approx 0.566$.

### The Fundamental Requirement: Controllability

The [pole placement](@entry_id:155523) procedure raises a critical question: Can we always find a gain matrix $K$ to place the closed-loop poles at any arbitrary locations we desire? The answer is no. This capability is dependent on a fundamental property of the system known as **controllability**.

A system is defined as **completely state controllable** if, for any initial state $\mathbf{x}(t_0)$, it is possible to find a control input $\mathbf{u}(t)$ that will transfer the state to any desired final state $\mathbf{x}(t_f)$ within a finite time interval. Intuitively, controllability means that the input $\mathbf{u}(t)$ has the ability to influence every state variable in the system.

The connection between this property and [pole placement](@entry_id:155523) is one of the most important results in control theory, often called the **Pole Placement Theorem**. It states that for a system $(\mathbf{A}, \mathbf{B})$, a gain matrix $K$ can be found to place the closed-loop eigenvalues at any arbitrary set of locations (provided that complex-conjugate eigenvalues are assigned in pairs for real systems) if and only if the system is completely state controllable [@problem_id:1613595].

If a system is controllable, we can always design a stabilizing [state-feedback controller](@entry_id:203349), regardless of whether the original open-loop system (governed by $A$) is stable or unstable. Controllability is the key that unlocks the full power of [state feedback](@entry_id:151441).

Fortunately, there is a straightforward algebraic test for this crucial property. For an $n$-dimensional system with state matrix $A$ and input matrix $B$, we construct the **[controllability matrix](@entry_id:271824)**:
$$
\mathcal{C} = \begin{pmatrix} B  AB  A^2B  \cdots  A^{n-1}B \end{pmatrix}
$$
This is an $n \times nm$ matrix formed by concatenating the matrix $B$ and its successive products with $A$. The system is completely state controllable if and only if this matrix has full rank, i.e., $\text{rank}(\mathcal{C}) = n$.

For example, consider a third-order magnetic levitation model [@problem_id:1614769] with matrices $A = \begin{pmatrix} 0  1  0 \\ k_1  0  -k_2 \\ 0  0  -k_3 \end{pmatrix}$ and $B = \begin{pmatrix} 0 \\ 0 \\ k_4 \end{pmatrix}$. To test for [controllability](@entry_id:148402), we compute the columns of $\mathcal{C}$:
$$
B = \begin{pmatrix} 0 \\ 0 \\ k_4 \end{pmatrix}, \quad AB = \begin{pmatrix} 0 \\ -k_2 k_4 \\ -k_3 k_4 \end{pmatrix}, \quad A^2B = A(AB) = \begin{pmatrix} -k_2 k_4 \\ k_2 k_3 k_4 \\ k_3^2 k_4 \end{pmatrix}
$$
The full [controllability matrix](@entry_id:271824) is $\mathcal{C} = \begin{pmatrix} 0  0  -k_2 k_4 \\ 0  -k_2 k_4  k_2 k_3 k_4 \\ k_4  -k_3 k_4  k_3^2 k_4 \end{pmatrix}$. Provided the physical constants are non-zero, this matrix will typically have full rank (rank 3), indicating the system is controllable. Many common physical systems, such as the series RLC circuit, are inherently controllable for any set of positive physical parameters ($R, L, C$), meaning we can always design a [state-feedback controller](@entry_id:203349) to modify their dynamics [@problem_id:1614742].

### Interpretations of Uncontrollability

When a system is not controllable, it means there are certain "modes" or parts of the system's dynamics that the control input cannot affect. These are called **uncontrollable modes**, and their corresponding eigenvalues cannot be moved by [state feedback](@entry_id:151441).

A powerful physical intuition for uncontrollability arises in vibrational systems [@problem_id:1614775]. Imagine a system of two masses connected by springs. This system has two natural modes of vibration, each with a specific frequency and pattern of motion (an eigenvector). If we apply a control force, its ability to excite a particular mode depends on how it is applied. If the actuator is positioned such that it applies force at a **node** of a specific vibrational mode (a point that does not move in that mode), the actuator will be unable to put energy into or take energy out of that mode. Consequently, that mode becomes uncontrollable. The controller is effectively "blind" to it, and its dynamics (e.g., an unstable oscillation) cannot be altered.

From a system-theoretic perspective, uncontrollability is intimately linked to **pole-zero cancellations** in the transfer function representation of a system [@problem_id:14786]. If a transfer function $G(s) = \frac{N(s)}{D(s)}$ has a common factor $(s-p)$ in both its numerator and denominator, i.e., $G(s) = \frac{(s-p)\tilde{N}(s)}{(s-p)\tilde{D}(s)}$, this corresponds to a hidden dynamic mode. When we create a [state-space realization](@entry_id:166670) of this transfer function, the state associated with the pole at $s=p$ will either be uncontrollable or unobservable. An uncontrollable realization means that the input is decoupled from the mode at $s=p$, rendering it impossible to change its location via feedback. This highlights that a minimal [state-space model](@entry_id:273798) (one with the lowest possible dimension) is always both controllable and observable.

### Reference Tracking and Steady-State Error

Thus far, we have focused on placing the poles of $(A-BK)$ for stability and transient response, which corresponds to regulating the state to zero. The next critical task is to make the system's output, $y(t) = Cx(t)$, follow a non-zero reference command, $r(t)$.

A naive approach might be to use the control law $u(t) = r(t) - Kx(t)$. Let's analyze the steady-state behavior for a constant step input $r(t) = r_{ref}$. At steady state, $\dot{x}_{ss} = \mathbf{0}$, and the closed-loop equation becomes:
$$
\mathbf{0} = (A - BK)x_{ss} + Br_{ref} \quad \implies \quad x_{ss} = -(A-BK)^{-1}Br_{ref}
$$
The steady-state output is then $y_{ss} = Cx_{ss} = -C(A-BK)^{-1}Br_{ref}$.

Notice that the term $-C(A-BK)^{-1}B$ is the DC gain of the closed-loop system from the reference $r$ to the output $y$. There is no guarantee that this value will be equal to 1. In general, it is not, which means $y_{ss} \neq r_{ref}$. This discrepancy is the **steady-state error**, $e_{ss} = r_{ref} - y_{ss}$. For many systems, this simple control structure results in a significant, non-[zero steady-state error](@entry_id:269428), failing a primary control objective [@problem_id:1614763].

To correct this, we introduce a **feedforward gain**, historically denoted as $N$, into the control law:
$$
u(t) = -Kx(t) + Nr(t)
$$
Here, the roles are distinct: the feedback term $-Kx(t)$ stabilizes the system and shapes the transient response (by placing the poles), while the feedforward term $Nr(t)$ scales the reference command to ensure the output matches it at steady state [@problem_id:1614757].

To achieve [zero steady-state error](@entry_id:269428) ($y_{ss} = r_{ref}$), the DC gain from $r$ to $y$ must be unity. The steady-state output for this new control law is $y_{ss} = -C(A-BK)^{-1}BNr_{ref}$. For this to equal $r_{ref}$ for any $r_{ref}$, we must have:
$$
-C(A-BK)^{-1}BN = 1
$$
Solving for the scalar feedforward gain $N$ gives the required value:
$$
N = \frac{-1}{C(A-BK)^{-1}B}
$$
By first choosing $K$ to satisfy dynamic performance requirements (pole locations) and then calculating the corresponding value of $N$ using this formula, we can design a controller that is both stable, has a good transient response, and tracks constant reference commands with [zero steady-state error](@entry_id:269428). This two-degree-of-freedom structure separates the problem of regulation from the problem of tracking, forming the basis of practical [state-feedback controller](@entry_id:203349) design.