## Introduction
Model Predictive Control (MPC) has emerged as a cornerstone of modern control theory, prized for its ability to systematically handle complex system dynamics and operational constraints. Its power lies in a predictive, optimization-based approach that allows for optimal decision-making in real-time. However, moving from the conceptual idea of MPC to a robust, stable, and practical implementation presents a significant challenge, requiring a deep understanding of its theoretical underpinnings and numerical formulation. This article bridges that gap by providing a comprehensive exploration of MPC principles and practices.

The journey begins in the **Principles and Mechanisms** chapter, where we will dissect the core of MPC: the [receding horizon](@entry_id:181425) [optimal control](@entry_id:138479) problem. You will learn how to translate this problem into a solvable Quadratic Program (QP), understand the crucial role of [discretization](@entry_id:145012), and master the techniques for guaranteeing closed-loop stability using terminal sets and costs. Next, the **Applications and Interdisciplinary Connections** chapter showcases the versatility of the MPC framework. We will explore its use in trajectory tracking, offset-free control, and its extension to nonlinear (NMPC), economic (eMPC), and distributed systems, highlighting its impact in fields from robotics to synthetic biology. Finally, the **Hands-On Practices** section provides concrete exercises to solidify your understanding, guiding you through the analytical solution of a simple MPC problem and the implementation of advanced features like terminal sets and soft constraints. By the end of this article, you will have a thorough grasp of both the theory and application of Model Predictive Control.

## Principles and Mechanisms

This chapter delves into the fundamental principles and operational mechanisms of Model Predictive Control (MPC). We will move from the conceptual formulation of the control problem to its practical implementation as a numerical optimization, and then explore the theoretical underpinnings that guarantee stability and robustness.

### The Receding Horizon Optimal Control Problem

At the heart of MPC lies the repeated solution of a **Finite-Horizon Optimal Control Problem (FHOCP)**. At each [discrete time](@entry_id:637509) instant $t$, the controller performs three main actions:

1.  It measures or estimates the current state of the system, $x(t)$.
2.  It solves an open-loop [optimal control](@entry_id:138479) problem over a finite [prediction horizon](@entry_id:261473) of $N$ steps into the future, using a model of the system to predict its behavior.
3.  It applies only the first element of the computed [optimal control](@entry_id:138479) sequence to the plant and discards the remainder of the plan.

This process is then repeated at the next time instant, $t+1$, with a new state measurement. This iterative strategy is known as **[receding horizon control](@entry_id:270676)** (or rolling horizon control), and it is this constant re-planning that imbues MPC with its feedback nature, allowing it to react to disturbances and model mismatch.

The FHOCP solved at each time $t$ is typically formulated as follows. Given the current state $x(t)$, we seek to find an optimal control sequence $\{u_k\}_{k=0}^{N-1}$ and the corresponding state sequence $\{x_k\}_{k=0}^{N}$ that minimize a [cost function](@entry_id:138681), subject to [system dynamics](@entry_id:136288) and constraints [@problem_id:2724696].

The [objective function](@entry_id:267263), $J$, is a sum of costs incurred at each step of the horizon, comprising a **stage cost**, $\ell(x_k, u_k)$, and a final **terminal cost**, $V_f(x_N)$. A common choice, particularly for [linear systems](@entry_id:147850), is a quadratic cost function:
$$
J = \sum_{k=0}^{N-1} \left( x_{k}^{\top} Q x_{k} + u_{k}^{\top} R u_{k} \right) + x_{N}^{\top} P x_{N}
$$
Here, the matrices $Q \succeq 0$ and $R \succ 0$ are user-defined weights that penalize state deviations and control effort, respectively. The matrix $P \succeq 0$ penalizes the final predicted state, and as we will see, it plays a critical role in ensuring the stability of the closed-loop system.

This minimization is subject to a set of constraints that define the feasible behavior of the system over the [prediction horizon](@entry_id:261473):
*   **Initial Condition**: The predicted trajectory must start from the current measured state: $x_0 = x(t)$.
*   **System Dynamics**: The predicted trajectory must evolve according to the system's discrete-time model: $x_{k+1} = A x_k + B u_k$ for $k \in \{0, \dots, N-1\}$.
*   **State and Input Constraints**: The predicted states and inputs must lie within admissible sets, often defined by convex [polytopes](@entry_id:635589): $x_k \in \mathcal{X}$ and $u_k \in \mathcal{U}$.
*   **Terminal Constraint**: The state at the end of the horizon is often constrained to lie within a specific **[terminal set](@entry_id:163892)**, $\mathcal{X}_f \subseteq \mathcal{X}$. This constraint is, like the terminal cost, a crucial ingredient for guaranteeing stability.

Once the optimization problem is solved, an [optimal control](@entry_id:138479) sequence $u_0^\star, u_1^\star, \dots, u_{N-1}^\star$ is obtained. The [receding horizon](@entry_id:181425) principle dictates that only the first input, $u(t) = u_0^\star$, is applied to the system. At the next sampling time, a new state $x(t+1)$ is measured, and the entire process—optimization over a shifted horizon—is repeated [@problem_id:2724696].

### From Continuous Reality to a Discrete-Time Model

The predictive power of MPC hinges on the availability of a dynamical model. While physical systems evolve in continuous time, MPC is typically implemented on digital hardware, necessitating a discrete-time model. Therefore, a crucial first step is the accurate discretization of the underlying continuous-time plant dynamics.

Consider a linear time-invariant (LTI) continuous-time plant described by $\dot{x}(t) = A_c x(t) + B_c u(t)$. In a [digital control](@entry_id:275588) setting, the state is sampled at intervals of period $T_s$, and the control input is held constant between sampling instants. This is known as a **[zero-order hold](@entry_id:264751) (ZOH)**. Under these standard assumptions, we can derive an exact discrete-time model of the form $x_{k+1} = A x_k + B u_k$, where $x_k \triangleq x(k T_s)$ and $u_k$ is the constant input applied over the interval $[k T_s, (k+1) T_s)$.

The solution to the continuous-time state equation over one sampling interval is given by the [variation of constants](@entry_id:196393) formula:
$$
x((k+1)T_s) = \exp(A_c T_s) x(k T_s) + \int_{k T_s}^{(k+1)T_s} \exp(A_c ((k+1)T_s - \tau)) B_c u(\tau) \, \mathrm{d}\tau
$$
With the ZOH assumption, $u(\tau) = u_k$ for $\tau \in [k T_s, (k+1)T_s)$. Substituting this and performing a change of integration variable, we obtain the exact discrete-time matrices [@problem_id:2724702]:
$$
A = \exp(A_c T_s)
$$
$$
B = \left( \int_{0}^{T_s} \exp(A_c \sigma) \, \mathrm{d}\sigma \right) B_c
$$
It is important to note that simpler approximations, like the forward Euler method which yields $A \approx I + A_c T_s$ and $B \approx B_c T_s$, are generally not exact and can lead to significant prediction errors, especially for larger sampling times $T_s$.

For practical computation, the integral for $B$ can be evaluated in several ways. If the matrix $A_c$ is invertible, the integral has a convenient closed form:
$$
B = A_c^{-1} \left( \exp(A_c T_s) - I \right) B_c
$$
This formula, however, cannot be used if $A_c$ is singular. The integral definition remains valid in all cases and can be computed, for instance, via a series expansion. A particularly elegant and general computational method, often attributed to Van Loan, involves exponentiating an augmented [block matrix](@entry_id:148435) [@problem_id:2724702]:
$$
\exp\left( \begin{pmatrix} A_c & B_c \\ 0 & 0 \end{pmatrix} T_s \right) = \begin{pmatrix} A & B \\ 0 & I \end{pmatrix}
$$
This technique provides both $A$ and $B$ in a single matrix operation and is numerically robust for both singular and non-singular $A_c$.

### Formulation as a Quadratic Program

While the FHOCP provides a conceptual framework, its implementation requires recasting it into a standard form that numerical solvers can handle. For LTI systems with quadratic costs and polytopic constraints, the MPC problem can be formulated as a **Quadratic Program (QP)**. A QP involves minimizing a convex quadratic [objective function](@entry_id:267263) subject to linear [inequality constraints](@entry_id:176084).

The key step is to eliminate the [state variables](@entry_id:138790) from the optimization problem, leaving only the sequence of control inputs as decision variables. This is achieved through a process called **condensation**. We begin by expressing the future states as an explicit function of the initial state $x_0$ and the sequence of control inputs $U = \begin{pmatrix} u_0^\top & u_1^\top & \cdots & u_{N-1}^\top \end{pmatrix}^\top \in \mathbb{R}^{mN}$.

By recursively applying the state equation $x_{k+1} = Ax_k + Bu_k$, we find:
$x_1 = A x_0 + B u_0$
$x_2 = A x_1 + B u_1 = A^2 x_0 + AB u_0 + B u_1$
...
$x_k = A^k x_0 + \sum_{j=0}^{k-1} A^{k-1-j} B u_j$

This allows us to write the entire predicted state trajectory (excluding $x_0$) as a single linear equation. If we stack the predicted states into a vector $\mathbf{X} = \begin{pmatrix} x_1^\top & \cdots & x_N^\top \end{pmatrix}^\top \in \mathbb{R}^{nN}$, this relationship becomes:
$$
\mathbf{X} = \mathcal{A} x_0 + \mathcal{B} U
$$
where $\mathcal{A} \in \mathbb{R}^{nN \times n}$ and $\mathcal{B} \in \mathbb{R}^{nN \times mN}$ are known as the prediction matrices, constructed from $A$ and $B$.

With this substitution, the quadratic [objective function](@entry_id:267263) $J$ can be rewritten purely in terms of the decision variable $U$ [@problem_id:2724637]. After some algebraic manipulation, $J$ takes the [canonical form](@entry_id:140237):
$$
J(U) = \frac{1}{2} U^\top H U + h^\top U + c
$$
where the Hessian matrix $H$ and the linear term $h$ are given by:
$$
H = 2(\mathcal{B}^\top \mathcal{Q} \mathcal{B} + \mathcal{R})
$$
$$
h = 2\mathcal{B}^\top \mathcal{Q} \mathcal{A} x_0
$$
The matrices $\mathcal{Q} = \mathrm{diag}(Q, \dots, Q, P)$ and $\mathcal{R} = \mathrm{diag}(R, \dots, R)$ are block-[diagonal matrices](@entry_id:149228) of the cost weights. The term $c$ depends only on $x_0$ and does not affect the [optimal solution](@entry_id:171456). Since $R \succ 0$ and $Q, P \succeq 0$, the Hessian $H$ is positive definite, ensuring the [objective function](@entry_id:267263) is strictly convex and has a unique minimum.

Similarly, the state and input constraints must be expressed as linear inequalities on $U$. If the constraints are polytopic, e.g., $H_x x_k \le h_x$ and $H_u u_k \le h_u$, they can be stacked over the horizon. By substituting $\mathbf{X} = \mathcal{A} x_0 + \mathcal{B} U$, all constraints can be consolidated into a single large [matrix inequality](@entry_id:181828) [@problem_id:2724707]:
$$
G U \le w + E x_0
$$
where the matrices $G, w, E$ are constructed from the original constraint matrices $H_x, h_x, H_u, h_u$ and the prediction matrices $\mathcal{A}, \mathcal{B}$.

The MPC problem is thus transformed into a standard QP that can be efficiently solved at each time step using readily available optimization software.

### Guaranteeing Stability via Terminal Ingredients

A fundamental challenge in MPC is to guarantee the stability of the closed-loop system despite optimizing over a finite horizon. A short-sighted controller might take actions that are optimal in the short term but lead to instability in the long run. The [standard solution](@entry_id:183092) is to augment the FHOCP with a carefully designed **terminal cost** $V_f(x_N)$ and **[terminal set](@entry_id:163892)** $\mathcal{X}_f$. These terminal ingredients serve as an approximate representation of the infinite-horizon cost and constraints, guiding the controller towards stable behavior.

To prove [asymptotic stability](@entry_id:149743), we aim to show that the optimal [cost function](@entry_id:138681) of the MPC problem, $J_N^*(x)$, acts as a **Lyapunov function** for the closed-loop system. This requires demonstrating two key properties:

1.  **Recursive Feasibility**: If the optimization problem is feasible for the current state $x_k$, it must remain feasible for all future states $x_{k+1}, x_{k+2}, \dots$.
2.  **Lyapunov Decrease**: The optimal cost must strictly decrease along the system's trajectory, i.e., $J_N^*(x_{k+1})  J_N^*(x_k)$ for all $x_k \neq 0$.

A standard set of [sufficient conditions](@entry_id:269617) to achieve this involves designing the terminal ingredients based on a known, stabilizing local control law, $u=Kx$ [@problem_id:2724726] [@problem_id:2884303]. The conditions are:

*   The [terminal set](@entry_id:163892) $\mathcal{X}_f$ is a **positively [invariant set](@entry_id:276733)** for the closed-loop system $x^+ = (A+BK)x$. This means that if a state $x$ is in $\mathcal{X}_f$, applying the control $u=Kx$ will result in a successor state $x^+$ that is also in $\mathcal{X}_f$.
*   For all states within the [terminal set](@entry_id:163892), the state and input constraints are satisfied: $x \in \mathcal{X}$ and $Kx \in \mathcal{U}$ for all $x \in \mathcal{X}_f$.
*   The terminal cost $V_f(x)$ is a local Lyapunov function for the terminal controller, satisfying $V_f((A+BK)x) - V_f(x) \le -\ell(x, Kx)$ for all $x \in \mathcal{X}_f$.

These conditions ensure that once the predicted state enters the [terminal set](@entry_id:163892), a feasible and stabilizing control sequence can always be constructed for the next time step (by shifting the previous plan and appending the terminal control law), thus guaranteeing [recursive feasibility](@entry_id:167169). The decrease condition on $V_f(x)$ ensures that the overall cost function $J_N^*(x)$ decreases at each step.

A powerful and systematic way to design these ingredients is to leverage the theory of the **Linear Quadratic Regulator (LQR)**. The LQR provides an optimal infinite-horizon controller for the unconstrained system by minimizing $\sum_{k=0}^{\infty} (x_k^\top Q x_k + u_k^\top R u_k)$. The solution is a linear feedback law $u_k = Kx_k$, where the gain $K$ and the optimal cost-to-go matrix $P$ are found by solving the **Discrete-time Algebraic Riccati Equation (DARE)**.

By choosing the terminal [cost matrix](@entry_id:634848) $P$ and terminal controller gain $K$ as the solution to the DARE associated with the stage cost weights $(Q,R)$, the local Lyapunov decrease condition is met with equality: $x^\top Px$ becomes the optimal cost-to-go for the terminal controller, and its one-step evolution is precisely the Bellman equation, $x^\top((A+BK)^\top P(A+BK))x - x^\top Px = -x^\top(Q+K^\top RK)x = -\ell(x,Kx)$ [@problem_id:2884303].

This leads to a concrete design procedure [@problem_id:2724634]:
1.  **Select Weights and Solve DARE**: Choose stage cost weights $Q$ and $R$. Solve the corresponding DARE to obtain the unique [positive definite](@entry_id:149459) solution $P$ and the LQR gain $K$.
2.  **Define Terminal Set Structure**: A natural choice for the [terminal set](@entry_id:163892) is an [ellipsoid](@entry_id:165811) defined by a [sublevel set](@entry_id:172753) of the terminal cost: $\mathcal{X}_f(\alpha) = \{ x \in \mathbb{R}^n \mid x^\top P x \le \alpha \}$. By the properties of the DARE solution, this set is guaranteed to be positively invariant under the control $u=Kx$.
3.  **Determine Maximal Admissible Set**: Find the largest value of $\alpha$, denoted $\alpha^\star$, such that the [ellipsoid](@entry_id:165811) $\mathcal{X}_f(\alpha^\star)$ is fully contained within the state and input constraints. This involves checking that for all $x$ satisfying $x^\top Px \le \alpha^\star$, we have $x \in \mathcal{X}$ and $Kx \in \mathcal{U}$. This defines the largest possible "safe" region where the terminal controller can operate. For example, if we have constraints $|x_1| \le 1$ and $|u| \le 1$, we must find the largest $\alpha$ such that $\max_{x \in \mathcal{X}_f(\alpha)}|x_1| \le 1$ and $\max_{x \in \mathcal{X}_f(\alpha)}|Kx| \le 1$. In a worked example for a double integrator with specific constraints, this procedure identifies the limiting constraint and yields a specific value for $\alpha^\star$, thereby fully defining the MPC controller [@problem_id:2724634].

### Advanced Mechanisms for Practical Implementation

Beyond the core principles of formulation and stability, practical MPC design often involves mechanisms to handle infeasibility and [model uncertainty](@entry_id:265539).

#### Soft Constraints for Feasibility

A major practical issue with MPC is that the optimization problem can become infeasible. If the system is perturbed into a state from which no input sequence can satisfy the hard [state constraints](@entry_id:271616) over the horizon, the controller fails. To prevent this, [state constraints](@entry_id:271616) are often "softened" by introducing non-negative **[slack variables](@entry_id:268374)**, $s_k \ge 0$.

Instead of enforcing a hard constraint like $Cx_k \le d$, we enforce a softened version $Cx_k \le d + s_k$. The [slack variables](@entry_id:268374) are then penalized in the [objective function](@entry_id:267263) to ensure they are only used when necessary. Common choices for the penalty are quadratic ($L_2^2$) or linear ($L_1$) [@problem_id:2724828]:
*   **Quadratic Penalty**: Add $\rho \sum_{k=0}^{N-1} s_k^\top s_k$ to the cost.
*   **Linear Penalty**: Add $\rho \sum_{k=0}^{N-1} \mathbf{1}^\top s_k$ to the cost.

These two penalties lead to qualitatively different behaviors. The [quadratic penalty](@entry_id:637777) is smooth and tends to distribute any necessary [constraint violation](@entry_id:747776) across many components and time steps, as it heavily penalizes large, concentrated violations. The linear penalty, on the other hand, is non-smooth and often results in [sparse solutions](@entry_id:187463), where the violation is confined to the fewest components possible. From an optimization perspective, for a linear penalty, the Karush-Kuhn-Tucker (KKT) conditions show that the Lagrange multipliers on the softened [state constraints](@entry_id:271616) are bounded by the penalty weight $\rho$. For a [quadratic penalty](@entry_id:637777), the multipliers are proportional to the [slack variables](@entry_id:268374) themselves [@problem_id:2724828].

Crucially, as long as the input constraint set $\mathcal{U}$ is non-empty, a soft-constrained MPC problem is always feasible. For any valid input sequence, a sufficiently large slack can always be found to satisfy the softened [state constraints](@entry_id:271616). This property of guaranteed [recursive feasibility](@entry_id:167169) makes soft constraints an essential tool for robust, real-world MPC implementation [@problem_id:2724828].

#### Robustness to Disturbances: Tube-Based MPC

The nominal MPC formulation assumes a perfect model. Real systems are subject to disturbances and model mismatch, described by dynamics like $x_{k+1} = Ax_k + Bu_k + w_k$, where $w_k$ is a bounded but unknown disturbance. To guarantee [constraint satisfaction](@entry_id:275212) in the presence of such uncertainty, robust MPC methods are required.

A key concept here is the distinction between different types of [invariant sets](@entry_id:275226) [@problem_id:2724771]. For nominal MPC, a **control [invariant set](@entry_id:276733)** is sufficient for the [terminal set](@entry_id:163892). This is a set where for any state, *there exists* an admissible control to keep the successor state within the set. For robust MPC, a stronger property is needed: **robust positive invariance (RPI)**. An RPI set is one where for any state and for *all possible* disturbances, the successor state remains in the set.

**Tube-based MPC** is a popular strategy for achieving robustness. The idea is to design a controller that keeps the true system state $x_k$ within a "tube" centered around a nominal trajectory $\bar{x}_k$. The control law is decomposed into two parts: a nominal input $v_k$ computed by a nominal MPC, and an ancillary feedback law $K e_k$ to correct for deviations, $e_k = x_k - \bar{x}_k$. The total control is $u_k = v_k + K e_k$.

The feedback law $K$ is designed to ensure that the error dynamics, $e_{k+1} = (A+BK)e_k + w_k$, are stable and that the error $e_k$ is always confined to a known RPI set $\mathcal{Z}$, which defines the cross-section of the tube.

To guarantee that the true state $x_k$ and input $u_k$ satisfy their constraints $\mathcal{X}$ and $\mathcal{U}$, we must solve the nominal MPC problem with **tightened constraints**. Since $x_k = \bar{x}_k + e_k$ and $u_k = v_k + K e_k$, with $e_k \in \mathcal{Z}$, the nominal variables must be restricted to ensure that $\bar{x}_k + e_k \in \mathcal{X}$ and $v_k + Ke_k \in \mathcal{U}$ for all possible errors $e_k \in \mathcal{Z}$.

This leads to tightened constraint sets defined by the **Pontryagin difference** ($\ominus$):
$$
\mathcal{X}_{\text{tight}} = \mathcal{X} \ominus \mathcal{Z} \triangleq \{ x \mid x + z \in \mathcal{X} \text{ for all } z \in \mathcal{Z} \}
$$
$$
\mathcal{U}_{\text{tight}} = \mathcal{U} \ominus K\mathcal{Z} \triangleq \{ u \mid u + y \in \mathcal{U} \text{ for all } y \in K\mathcal{Z} \}
$$
For simple hyperrectangular sets, this tightening amounts to shrinking the boundaries of the original constraint sets. For example, if $\mathcal{X} = \{x \mid |x_i| \le \bar{x}_i\}$ and $\mathcal{Z} = \{z \mid |z_i| \le \bar{z}_i\}$, the tightened state constraint is $|x_i| \le \bar{x}_i - \bar{z}_i$. By planning with these more conservative constraints for the nominal system, we can provide hard guarantees on [constraint satisfaction](@entry_id:275212) for the true, uncertain system [@problem_id:2724784].