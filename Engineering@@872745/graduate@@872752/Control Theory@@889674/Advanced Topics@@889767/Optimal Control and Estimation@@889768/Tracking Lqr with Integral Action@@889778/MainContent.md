## Introduction
In [modern control systems](@entry_id:269478), achieving precise tracking of reference signals in the face of disturbances and model uncertainties is a paramount objective. While the standard Linear Quadratic Regulator (LQR) provides an elegant framework for optimal state regulation, it does not inherently guarantee [zero steady-state error](@entry_id:269428) for tracking problems. This gap is robustly filled by augmenting the LQR with integral action, resulting in the Linear Quadratic Integral (LQI) controller—a powerful and widely used methodology. The LQI framework systematically combines the performance optimality of LQR with the error-eliminating properties of an integrator, providing a principled approach to designing high-performance servomechanisms.

This article provides a comprehensive exploration of the LQI controller, from its theoretical underpinnings to its practical implementation. We will begin in the **"Principles and Mechanisms"** chapter by formalizing the servomechanism problem and introducing the Internal Model Principle to justify the need for an integrator. We will then detail the construction of the [augmented state-space system](@entry_id:265590) and the LQR-based design process. Following this, the **"Applications and Interdisciplinary Connections"** chapter will bridge theory and practice, discussing crucial real-world challenges such as [state estimation](@entry_id:169668), [actuator saturation](@entry_id:274581), and extensions to multi-input systems. Finally, the **"Hands-On Practices"** section will offer concrete problems to solidify your understanding and build practical design skills.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms underpinning the design of tracking controllers with integral action. We will begin by rigorously defining the distinct objectives of regulation, tracking, and [disturbance rejection](@entry_id:262021). Subsequently, we will introduce the Internal Model Principle as the theoretical cornerstone justifying the use of integral action. We will then formalize the construction of an [augmented state-space system](@entry_id:265590) that incorporates this integral action, and establish the precise conditions under which such a system can be stabilized. Finally, we will detail the procedure for designing an optimal controller using the Linear Quadratic Regulator (LQR) framework, a method commonly referred to as Linear Quadratic Integral (LQI) control.

### The Servomechanism Problem: Regulation, Tracking, and Disturbance Rejection

In control theory, we address several canonical problems. Understanding their distinctions is crucial for selecting and designing appropriate control strategies. Consider a linear time-invariant (LTI) plant described by:
$$
\dot{x}(t) = Ax(t) + Bu(t)
$$
$$
y(t) = Cx(t)
$$
where $x(t) \in \mathbb{R}^n$ is the state, $u(t) \in \mathbb{R}^m$ is the control input, and $y(t) \in \mathbb{R}^p$ is the measured output.

**State Regulation** is the problem of stabilizing the system around an [equilibrium point](@entry_id:272705), typically the origin ($x=0$), from any initial condition $x(0)$. In this context, there is no external reference signal, so we can consider the reference to be identically zero, $r(t) \equiv 0$. The objective is to ensure that $\lim_{t\to\infty} x(t) = 0$. A standard LQR controller, which minimizes a [cost functional](@entry_id:268062) of the form $J = \int_{0}^{\infty} (x^\top Qx + u^\top Ru) dt$, provides a state-feedback law $u(t) = -Kx(t)$ that achieves this by making the closed-loop matrix $(A-BK)$ stable. Notice that the tracking error $e(t) = r(t) - y(t)$ is not explicitly used in this formulation [@problem_id:2755126].

**Output Tracking**, also known as the servomechanism problem, is more ambitious. The goal is to make the plant's output $y(t)$ follow a specified reference trajectory $r(t)$, such that the [tracking error](@entry_id:273267) $e(t) = r(t) - y(t)$ converges to zero. A key challenge is achieving **[zero steady-state error](@entry_id:269428)**, which is formally defined as $\lim_{t\to\infty} e(t) = 0$. This chapter focuses on the important case of tracking constant, or stepwise, references, where $r(t)$ is a constant vector $r_0$ for $t \ge 0$ [@problem_id:2755073]. For the system to be capable of maintaining an output $y_{ss} = r_0$ in steady state, there must exist a corresponding steady-state pair $(x_{ss}, u_{ss})$ that satisfies the plant's [equilibrium equations](@entry_id:172166):
$$
\begin{cases}
Ax_{ss} + Bu_{ss} = 0 \\
Cx_{ss} = r_0
\end{cases}
$$
The set of all such constant references $r_0$ for which a solution $(x_{ss}, u_{ss})$ exists defines the set of trackable constant references for the plant.

**Disturbance Rejection** aims to mitigate the effect of external disturbances on the plant's output. For instance, consider a constant matched disturbance $d$ entering through the input channel: $\dot{x}(t) = A x(t) + B(u(t) + d)$. The goal is typically to regulate the output to zero, i.e., $y(t) \to 0$, despite the unknown, constant disturbance $d$. In this setting, the reference is $r(t) \equiv 0$, and the error becomes $e(t) = -y(t)$ [@problem_id:2755126].

As we will see, the problems of tracking constant references and rejecting constant disturbances are deeply related and can be solved using the same powerful mechanism: integral action.

### The Internal Model Principle: Why Integral Action Works

Why can't a simple [state-feedback controller](@entry_id:203349) $u(t) = -Kx(t)$, perhaps with a feedforward term, reliably achieve [zero steady-state error](@entry_id:269428)? While one could carefully select a feedforward gain $N_r$ to design a controller $u(t) = -Kx(t) + N_r r(t)$ that achieves zero error for a specific, perfectly known plant model, this approach is not robust. Any small modeling error or unmeasured disturbance will typically lead to a non-[zero steady-state error](@entry_id:269428).

The robust solution is provided by the **Internal Model Principle**. This fundamental theorem of control theory states that for a controller to achieve perfect asymptotic tracking and/or rejection of a class of signals, the controller must contain a generative model of those signals within its feedback loop [@problem_id:2755129].

The signals we wish to track and reject are constants. A constant signal $w(t) = w_0$ can be thought of as the output of the simplest possible dynamic system, an "exosystem," described by $\dot{w}(t) = 0$. In the Laplace domain, this corresponds to a pole at $s=0$. Therefore, to robustly track constant references and reject constant disturbances, the control loop must incorporate a pole at $s=0$.

An integrator is a system with a single pole at $s=0$. By introducing a new state variable, the integral state $z(t)$, whose dynamics are governed by the [tracking error](@entry_id:273267):
$$
\dot{z}(t) = e(t) = r(t) - y(t)
$$
we embed the required internal model directly into the controller. Now, consider the conditions for a stable closed-loop system to reach a steady state. At steady state, all state derivatives must be zero. In particular, the derivative of the integral state must be zero: $\dot{z}_{ss} = 0$. By the definition of the integrator, this immediately implies that the [steady-state error](@entry_id:271143) must be zero:
$$
e_{ss} = r_0 - y_{ss} = 0
$$
This elegant result shows that the very structure of the integral controller forces the tracking error to zero, provided a stable steady state can be reached. The integrator's output, $z(t)$, effectively accumulates any persistent error, continuously adjusting the control input until the error is eliminated.

### Augmenting the State: System Representation for LQI Control

To design a controller that utilizes the original plant state $x$ and the new integral state $z$, we combine them into a single **augmented [state vector](@entry_id:154607)**, $x_a(t) \in \mathbb{R}^{n+p}$:
$$
x_a(t) = \begin{pmatrix} x(t) \\ z(t) \end{pmatrix}
$$
We can then derive the [state-space model](@entry_id:273798) for the augmented system. The time derivative of the augmented state is $\dot{x}_a(t) = \begin{pmatrix} \dot{x}(t) \\ \dot{z}(t) \end{pmatrix}$. For the purpose of feedback design, we consider the regulation problem around a reference, so we can set $r=0$ in the dynamics. Substituting the plant and integrator dynamics, we have:
$$
\dot{x}(t) = Ax(t) + Bu(t)
$$
$$
\dot{z}(t) = -y(t) = -Cx(t)
$$
We can write this in the standard state-[space form](@entry_id:203017) $\dot{x}_a = A_a x_a + B_a u$:
$$
\dot{x}_a(t) = \begin{pmatrix} Ax(t) + Bu(t) \\ -Cx(t) \end{pmatrix} = \begin{pmatrix} A & 0 \\ -C & 0 \end{pmatrix} \begin{pmatrix} x(t) \\ z(t) \end{pmatrix} + \begin{pmatrix} B \\ 0 \end{pmatrix} u(t)
$$
This gives us the augmented system matrices [@problem_id:2719957] [@problem_id:2755121]:
$$
A_a = \begin{pmatrix} A & 0 \\ -C & 0 \end{pmatrix}, \quad B_a = \begin{pmatrix} B \\ 0 \end{pmatrix}
$$
A [state-feedback controller](@entry_id:203349) for this augmented system takes the form $u(t) = -K_a x_a(t)$. By partitioning the gain matrix $K_a = \begin{pmatrix} K_x & K_i \end{pmatrix}$, where $K_x \in \mathbb{R}^{m \times n}$ and $K_i \in \mathbb{R}^{m \times p}$, we get the familiar control law:
$$
u(t) = -K_x x(t) - K_i z(t)
$$
The term $-K_x x(t)$ provides feedback from the plant's state, primarily shaping the transient response. The term $-K_i z(t)$ provides the integral action, driving the [steady-state error](@entry_id:271143) to zero.

Substituting this control law into the augmented dynamics yields the closed-loop system:
$$
\dot{x}_a(t) = (A_a - B_a K_a) x_a(t) = \begin{pmatrix} A - BK_x & -BK_i \\ -C & 0 \end{pmatrix} x_a(t)
$$
The matrix $A_{cl} = A_a - B_a K_a$ is the closed-loop dynamics matrix that governs the stability and performance of the overall system [@problem_id:2755118]. The entire design problem now reduces to finding a gain matrix $K_a = \begin{pmatrix} K_x & K_i \end{pmatrix}$ that makes $A_{cl}$ stable.

### Conditions for Success: Stabilizability and Transmission Zeros

The existence of a stabilizing gain matrix $K_a$ is not guaranteed. It is equivalent to the condition that the augmented pair $(A_a, B_a)$ is **stabilizable**. A fundamental result in control theory provides the [necessary and sufficient conditions](@entry_id:635428) for this [@problem_id:2755050]:

The pair $(A_a, B_a) = \left( \begin{pmatrix} A & 0 \\ -C & 0 \end{pmatrix}, \begin{pmatrix} B \\ 0 \end{pmatrix} \right)$ is stabilizable if and only if:
1.  The original plant pair $(A, B)$ is stabilizable.
2.  The plant $(A, B, C)$ has no **[transmission zeros](@entry_id:175186)** at $s=0$.

The first condition is intuitive: if the original plant has [unstable modes](@entry_id:263056) that cannot be controlled by the input $u$, adding an integrator will not remedy this. The second condition is more subtle and critical. A transmission zero at $s=0$ means there is a non-zero input at zero frequency (a DC input) that produces zero output. This creates a "blind spot" for the controller. When the integrator, which operates at $s=0$, is combined with a plant that has a zero at the same frequency, a [pole-zero cancellation](@entry_id:261496) occurs in the control loop, rendering a mode of the system uncontrollable.

For a MIMO system, the condition of having no transmission zero at $s=0$ is equivalent to the **Rosenbrock [system matrix](@entry_id:172230)** $R(s) = \begin{pmatrix} sI-A & -B \\ C & D \end{pmatrix}$ having full row rank at $s=0$. In the common case where the feedthrough matrix $D=0$, this condition becomes:
$$
\text{rank} \begin{pmatrix} -A & -B \\ C & 0 \end{pmatrix} = n+p
$$
or equivalently, $\text{rank} \begin{pmatrix} A & B \\ C & 0 \end{pmatrix} = n+p$. If this rank is less than $n+p$, denoted as $\text{rank } R(0)  n+p$, then asymptotic tracking of arbitrary constant references is precluded [@problem_id:2755074].

Let's illustrate this failure mode with a concrete example [@problem_id:2755092]. Consider the plant:
$$
A=\begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix}, \quad B=\begin{pmatrix} 0 \\ 1 \end{pmatrix}, \quad C=\begin{pmatrix} 0  1 \end{pmatrix}
$$
This system represents a double integrator where the output is the velocity. The pair $(A,B)$ is controllable and thus stabilizable. However, this plant has a transmission zero at $s=0$. If we construct the augmented system, we find:
$$
A_a = \begin{pmatrix} 0  1  0 \\ 0  0  0 \\ 0  -1  0 \end{pmatrix}, \quad B_a = \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix}
$$
The eigenvalues of $A_a$ are all at $\lambda=0$. Applying the Popov-Belevitch-Hautus (PBH) [rank test](@entry_id:163928) for [stabilizability](@entry_id:178956) at $\lambda=0$, we check the rank of $\begin{pmatrix} A_a  B_a \end{pmatrix}$. The rank is found to be 2, which is less than the augmented state dimension of 3. This indicates an uncontrollable mode at $s=0$, making the augmented system unstabilizable. No LQI controller can be designed for this plant.

### Optimal Design: The Linear Quadratic Integral (LQI) Controller

Assuming the [stabilizability](@entry_id:178956) conditions are met, we can proceed to find an optimal gain matrix $K_a$ using the LQR framework. This involves defining a quadratic [cost functional](@entry_id:268062) for the augmented system:
$$
J = \int_{0}^{\infty} \left( x_a(t)^{\top} Q_a x_a(t) + u(t)^{\top} R u(t) \right) dt
$$
This can be expanded in terms of the original state and integral state penalties:
$$
J = \int_{0}^{\infty} \left( x(t)^{\top} Q x(t) + z(t)^{\top} Q_i z(t) + u(t)^{\top} R u(t) \right) dt
$$
where $Q_a = \text{diag}(Q, Q_i)$. The selection of the weighting matrices $Q$, $Q_i$, and $R$ is a critical part of the design process, allowing the designer to trade off between performance (speed of response, error magnitude) and control effort.

For the LQR problem to be well-posed and yield a unique, stabilizing solution via the standard framework, certain conditions must be placed on these matrices [@problem_id:2755121]:
*   **$R$ must be symmetric and positive definite ($R \succ 0$).** This penalizes control effort and ensures that the [optimal control](@entry_id:138479) $u(t)$ is finite and uniquely determined. The invertibility of $R$ is required for the [standard solution](@entry_id:183092) formula.
*   **$Q$ and $Q_i$ must be symmetric and positive semidefinite ($Q \succeq 0, Q_i \succeq 0$).** This ensures the cost is always non-negative.
*   **Crucially, $Q_i$ must be positive definite ($Q_i \succ 0$).** The [augmented matrix](@entry_id:150523) $A_a$ has $p$ eigenvalues at the origin, corresponding to the integrators. These are [unstable modes](@entry_id:263056) that must be stabilized. For the LQR framework to "see" and control these modes, they must be detectable through the cost function. Making $Q_i$ positive definite ensures that any non-zero value of the integral state $z$ incurs a cost, thereby making the integrator modes detectable. If $Q_i$ were only semidefinite, some integrator states might be unobservable in the cost, leading to an unstable closed-loop system.

Under these conditions, along with the [stabilizability](@entry_id:178956) of $(A_a, B_a)$, there exists a unique, symmetric, [positive definite](@entry_id:149459) solution $P_a$ to the **continuous-time Algebraic Riccati Equation (ARE)** for the augmented system:
$$
A_a^\top P_a + P_a A_a - P_a B_a R^{-1} B_a^\top P_a + Q_a = 0
$$
The solution $P_a$ can be found numerically or, in some cases, analytically. The theoretical foundation for this solution lies in the properties of the associated **Hamiltonian matrix** $H = \begin{pmatrix} A_a  -B_a R^{-1} B_a^\top \\ -Q_a  -A_a^\top \end{pmatrix}$. The solution $P_a$ is uniquely determined by the [stable invariant subspace](@entry_id:755318) of this Hamiltonian matrix [@problem_id:2755095].

Once the solution $P_a$ is found, the optimal augmented feedback gain is given by:
$$
K_a = R^{-1} B_a^\top P_a
$$
This gain matrix $K_a = \begin{pmatrix} K_x  K_i \end{pmatrix}$ provides the feedback gains for the final control law, $u(t) = -K_x x(t) - K_i z(t)$, which guarantees both stability and optimal performance with respect to the chosen cost function. For practical implementation, a feedforward term on the reference, $u(t) = -K_x x(t) - K_i z(t) + F r(t)$, is often added to improve the transient response, though it is the integral action that guarantees [zero steady-state error](@entry_id:269428).