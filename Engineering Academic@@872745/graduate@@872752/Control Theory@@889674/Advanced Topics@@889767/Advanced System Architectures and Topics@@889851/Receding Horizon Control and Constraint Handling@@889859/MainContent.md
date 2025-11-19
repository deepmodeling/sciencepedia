## Introduction
Receding Horizon Control (RHC), more commonly known as Model Predictive Control (MPC), stands as one of the most powerful and widely adopted advanced control strategies in modern engineering and beyond. Its defining feature is the ability to explicitly handle system constraints—a critical requirement for nearly every real-world application, from chemical reactors to autonomous vehicles, which classical methods like the LQR often fail to address. This article bridges the gap between foundational theory and practical application, providing a comprehensive guide to designing, analyzing, and implementing RHC systems.

This article will guide you through the essential concepts in a structured, three-part journey. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, explaining how RHC formulates a [constrained optimization](@entry_id:145264) problem, creates a feedback loop, and guarantees stability through terminal ingredients. Building on this foundation, the second chapter, "Applications and Interdisciplinary Connections," explores practical enhancements for handling disturbances, advanced formulations like nonlinear and robust MPC, and its surprising utility in fields ranging from [bioprocess engineering](@entry_id:193847) to [computational economics](@entry_id:140923). Finally, the "Hands-On Practices" chapter provides a set of guided problems to translate these theoretical concepts into concrete computational skills. We begin our exploration by delving into the core principles that make Receding Horizon Control such a versatile and effective methodology.

## Principles and Mechanisms

This chapter delves into the foundational principles and operational mechanisms of Receding Horizon Control (RHC), also known as Model Predictive Control (MPC). We will dissect the core optimization problem that lies at its heart, explore the feedback mechanism that endows it with robustness, and formalize its structure as a tractable mathematical program. Crucially, we will investigate the central challenges of stability and [constraint satisfaction](@entry_id:275212), and systematically develop the theoretical apparatus required to guarantee them.

### The Finite-Horizon Optimal Control Problem

The fundamental building block of any RHC scheme is a **Finite-Horizon Optimal Control Problem (FHOCP)**. This is an optimization problem solved over a limited, moving window of future time steps. For a discrete-time linear time-invariant (LTI) system with dynamics $x_{k+1} = Ax_k + Bu_k$, the FHOCP is formulated at a given time $k$ with a measured initial state $x_k$.

The objective is to find a sequence of control inputs $\{u_{0|k}, u_{1|k}, \dots, u_{N-1|k}\}$ over a **[prediction horizon](@entry_id:261473)** of length $N$ that minimizes a [cost function](@entry_id:138681). A standard choice is a quadratic cost, which penalizes deviations of the state from the origin and the magnitude of the control effort:

$J = \sum_{i=0}^{N-1} (x_{i|k}^{\top} Q x_{i|k} + u_{i|k}^{\top} R u_{i|k}) + x_{N|k}^{\top} P x_{N|k}$

Here, $x_{i|k}$ denotes the predicted state at future time $k+i$, starting from $x_{0|k} = x_k$. The matrices $Q \succeq 0$ and $R \succ 0$ are the **stage cost** weights, penalizing the state and input at each step within the horizon. The final term, governed by the matrix $P \succeq 0$, is the **terminal cost**, which penalizes the final predicted state of the trajectory, $x_{N|k}$. This optimization is performed subject to constraints on the system's evolution:

1.  **System Dynamics:** $x_{i+1|k} = A x_{i|k} + B u_{i|k}$ for $i=0, \dots, N-1$.
2.  **State and Input Constraints:** The state and input at each step must remain within admissible sets, e.g., $x_{i|k} \in \mathcal{X}$ and $u_{i|k} \in \mathcal{U}$ for all $i$ in the horizon.

It is instructive to contrast this FHOCP with the classical infinite-horizon **Linear Quadratic Regulator (LQR)** problem [@problem_id:2736369]. While both often use quadratic costs, their structure and objectives differ fundamentally:

*   **Decision Variables**: The FHOCP directly solves for an **open-loop sequence** of control inputs, $\{u_{0|k}, \dots, u_{N-1|k}\}$. In contrast, the infinite-horizon LQR problem solves for a **[stationary state](@entry_id:264752)-feedback policy**, $u_k = Kx_k$, which is a rule applicable at any time.

*   **Constraints**: The FHOCP is designed to explicitly handle **hard constraints** on states and inputs (e.g., $x_k \in \mathcal{X}$, $u_k \in \mathcal{U}$). The standard LQR problem is fundamentally unconstrained; it cannot guarantee that the state or input will remain within prescribed bounds.

*   **Terminal Cost**: In the FHOCP, the terminal weight matrix $P$ is a crucial **design parameter**. As we will see, its careful selection is key to ensuring stability and performance. In the infinite-horizon LQR problem, the optimal cost is itself a quadratic function of the initial state, $J^*(x_0) = x_0^\top P_\infty x_0$, where $P_\infty$ is not a design choice but the unique stabilizing solution to the **Discrete Algebraic Riccati Equation (DARE)**.

In essence, the FHOCP provides a framework for finding an optimal plan over a finite window, explicitly respecting system limits. The RHC strategy, as we will now see, cleverly uses this finite-horizon planner to construct an [implicit feedback](@entry_id:636311) controller.

### The Receding Horizon Control Policy

Solving the FHOCP at time $k=0$ yields an optimal sequence of inputs $\{u_{0|0}^*, \dots, u_{N-1|0}^*\}$. A naive approach, known as **open-loop [optimal control](@entry_id:138479)**, would be to apply this entire sequence to the plant over time. However, this strategy is highly sensitive to disturbances and modeling errors. If the real plant dynamics are $x_{k+1} = A_p x_k + B_p u_k + d_k$ instead of the model $x_{k+1} = Ax_k + Bu_k$, the actual state trajectory will quickly diverge from the planned one, potentially leading to poor performance and constraint violations.

The **Receding Horizon Control (RHC)** policy provides an elegant solution through the principles of feedback and repeated re-planning [@problem_id:2736404]. The RHC algorithm proceeds as follows at each time step $k$:

1.  **Measure**: Obtain the current state of the plant, $x_k$.
2.  **Plan**: Solve the FHOCP with $x_k$ as the initial state to compute the optimal control sequence $\{u_{0|k}^*, u_{1|k}^*, \dots, u_{N-1|k}^*\}$.
3.  **Act**: Apply only the **first element** of the optimal sequence, $u_k = u_{0|k}^*$, to the plant.
4.  **Repeat**: Discard the rest of the computed sequence. At the next time step, $k+1$, the horizon "recedes" (or shifts forward), and the entire process is repeated from the new measured state $x_{k+1}$.

This "measure, plan, act" cycle creates a powerful feedback mechanism. The solution to the FHOCP at time $k$, specifically the first input $u_{0|k}^*$, is a function of the initial state $x_k$. Therefore, the RHC strategy implicitly defines a **[state-feedback control](@entry_id:271611) law**, $u_k = \kappa_{MPC}(x_k)$. Unlike a simple linear feedback $u=Kx$, this policy is the result of a complex [online optimization](@entry_id:636729).

This inherent feedback is what gives RHC its characteristic robustness [@problem_id:2736385]. When a disturbance or model mismatch causes the actual state $x_k$ to deviate from where the controller *thought* it would be, the re-optimization at time $k$ generates a new plan that is optimal and feasible *from the new, corrected state*. This continuous correction steers the plant back towards a desirable trajectory, mitigating the effects of past prediction errors. In contrast, an open-loop controller is blind to such deviations and will continue to execute its original, now-suboptimal plan, potentially leading to catastrophic failure.

### Formulation as a Quadratic Program

For LTI systems with quadratic costs and polyhedral constraints (i.e., constraints defined by linear inequalities), the FHOCP can be converted into a **Quadratic Program (QP)**. A QP is a convex optimization problem that can be solved very efficiently with modern [numerical solvers](@entry_id:634411). This conversion is a cornerstone of practical MPC implementation. The key is to express the entire prediction, cost, and constraints in terms of the initial state $x_k$ and the sequence of control inputs to be determined.

#### The Stacked Prediction Model

Let us define the sequence of control inputs over the horizon as a single stacked vector, $U = [u_{0|k}^\top, u_{1|k}^\top, \dots, u_{N-1|k}^\top]^\top \in \mathbb{R}^{mN}$. We wish to express the resulting sequence of predicted states, $X = [x_{1|k}^\top, x_{2|k}^\top, \dots, x_{N|k}^\top]^\top \in \mathbb{R}^{nN}$, as an [affine function](@entry_id:635019) of $x_k$ and $U$.

By recursively unrolling the dynamics $x_{i+1|k} = A x_{i|k} + B u_{i|k}$, we find:
$x_{1|k} = A x_k + B u_{0|k}$
$x_{2|k} = A x_{1|k} + B u_{1|k} = A(A x_k + B u_{0|k}) + B u_{1|k} = A^2 x_k + AB u_{0|k} + B u_{1|k}$
and so on. By collecting all terms dependent on $x_k$ and all terms dependent on the various $u_{i|k}$, we can write the entire predicted state trajectory in a compact matrix form [@problem_id:2736414]:

$X = \mathcal{A} x_k + \mathcal{B} U$

where the prediction matrices $\mathcal{A}$ and $\mathcal{B}$ are given by:
$\mathcal{A} = \begin{bmatrix} A \\ A^2 \\ \vdots \\ A^N \end{bmatrix}, \quad \mathcal{B} = \begin{bmatrix} B & 0 & \cdots & 0 \\ AB & B & \cdots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ A^{N-1}B & A^{N-2}B & \cdots & B \end{bmatrix}$

The matrix $\mathcal{A}$ maps the initial state to the "free response" of the system (evolution with zero input). The matrix $\mathcal{B}$ is a block lower-triangular Toeplitz matrix that maps the control sequence to the "[forced response](@entry_id:262169)." The lower-triangular structure reflects causality: the input $u_{i|k}$ can only affect states $x_{j|k}$ for $j > i$.

#### The Quadratic Cost Function

With the prediction model in hand, we can rewrite the total cost $J$ as a function of the decision variable $U$. The cost consists of a sum of stage costs and a terminal cost:
$J = x_k^\top Q x_k + \sum_{i=1}^{N-1} x_{i|k}^\top Q x_{i|k} + x_{N|k}^\top P x_{N|k} + \sum_{i=0}^{N-1} u_{i|k}^\top R u_{i|k}$

This can be expressed in stacked vector form as:
$J = x_k^\top Q x_k + X^\top \bar{Q}_P X + U^\top \bar{R} U$
where $\bar{Q}_P = \mathrm{diag}(Q, \dots, Q, P)$ and $\bar{R} = \mathrm{diag}(R, \dots, R) = I_N \otimes R$.

Substituting the prediction equation $X = \mathcal{A} x_k + \mathcal{B} U$ into this expression and grouping terms by powers of $U$ yields the standard QP cost form [@problem_id:2736413]:

$J(U) = \frac{1}{2} U^\top H U + x_k^\top F^\top U + \text{constant}$

where the Hessian matrix $H$ and the linear term matrix $F$ are given by:
$H = 2(\mathcal{B}^\top \bar{Q}_P \mathcal{B} + \bar{R})$
$F = 2 \mathcal{B}^\top \bar{Q}_P \mathcal{A}$

The term constant in $x_k$ does not affect the minimizer $U$ and can be ignored during optimization. The matrix $H$ is positive definite if $R \succ 0$, ensuring the QP is strictly convex and has a unique minimum.

#### The Stacked Constraint Inequalities

Finally, the constraints must also be expressed in terms of $U$. If the state and input constraints are polyhedral, they can be written as a set of linear inequalities. Consider a mixed stage constraint of the form $F_c x_i + G_c u_i \le f_c$ for $i=0, \dots, N-1$ and a [terminal constraint](@entry_id:176488) $F_f x_N \le f_f$.

By substituting the expressions for each $x_i$ in terms of $x_k$ and the inputs $u_j$ (for $j < i$), we can consolidate all $N$ stage constraints and the [terminal constraint](@entry_id:176488) into a single large [matrix inequality](@entry_id:181828) [@problem_id:2736393]:

$S_u U \le s - S_x x_k$

The matrices $S_u$, $S_x$, and the vector $s$ have a block structure that mirrors the structure of the prediction matrices.

With the cost function and constraints formulated in this manner, the FHOCP at each time step becomes a standard QP to be solved for the [optimal control](@entry_id:138479) sequence $U$:
$\min_{U} \quad \frac{1}{2} U^\top H U + x_k^\top F^\top U$
subject to $\quad S_u U \le s - S_x x_k$

This formulation is the gateway to implementing RHC on real-world systems, leveraging decades of research in efficient [numerical optimization](@entry_id:138060).

### Stability and Recursive Feasibility

While RHC is a powerful and intuitive control strategy, its naive application can lead to unexpected and undesirable behavior. Two of the most [critical properties](@entry_id:260687) that a well-designed RHC must possess are **stability** and **[recursive feasibility](@entry_id:167169)**. Stability ensures that the controlled system state converges to the desired equilibrium (e.g., the origin). Recursive feasibility guarantees that if the optimization problem is feasible at the current time step, it will remain feasible at all future time steps. Without this guarantee, the controller might one day fail to find a solution, leaving the system without a control input.

#### The Challenge of Naive RHC

The challenge arises from the "myopic" nature of a finite [prediction horizon](@entry_id:261473). An RHC controller optimizing over a short horizon might make a decision that is locally optimal but globally disastrous. Consider an unstable plant, $x_{k+1}=1.5x_k+u_k$, with constraints $|x_k| \le 1$ and $|u_k| \le 0.1$. If the controller's objective is simply to minimize control effort ($\ell(x,u)=u^2$) over a short horizon, it may choose to apply zero control to a small initial state, as this appears cheapest. However, the unstable dynamics cause the state to grow. This growth can lead the system into a "corner" of the state space from which it is impossible to satisfy the constraints in the subsequent time step, regardless of the control action. The optimization problem becomes infeasible, and the controller fails [@problem_id:2736362]. This highlights a crucial insight: for unstable systems, feasibility and stability are not guaranteed by default.

#### Terminal Ingredients for Stability

The standard and most elegant solution to this problem is to augment the FHOCP with a carefully designed **terminal cost** and **[terminal constraint](@entry_id:176488) set**. These "terminal ingredients" guide the end of the predicted trajectory into a region of the state space where stability can be guaranteed.

*   **The Terminal Set $\mathcal{X}_f$**: This is a subset of the state space, $\mathcal{X}_f \subseteq \mathcal{X}$, containing the origin. It is designed to be a region where a simple, stabilizing local controller, such as a linear feedback law $u = Kx$, can be used indefinitely without violating constraints. To achieve this, a valid [terminal set](@entry_id:163892) $\mathcal{X}_f$ must satisfy two key properties [@problem_id:2736421]:
    1.  **Admissibility**: For any state $x \in \mathcal{X}_f$, both the state and the control action from the local controller must be admissible, i.e., $x \in \mathcal{X}$ and $Kx \in \mathcal{U}$.
    2.  **Positive Invariance**: For any state $x \in \mathcal{X}_f$, the subsequent state under the local controller must also lie within the set, i.e., $(A+BK)x \in \mathcal{X}_f$. This property ensures that once the system enters $\mathcal{X}_f$, it can be kept there forever using the local controller.

*   **The Terminal Cost $V_f(x)$**: The terminal cost should act as an accurate approximation of the true infinite-horizon cost-to-go from the terminal state $x_N$. An excellent choice is the quadratic value function of the unconstrained LQR problem, $V_f(x) = x^\top P x$, where $P$ is the solution to the corresponding DARE [@problem_id:2736392]. This choice is not arbitrary; for the unconstrained system under the control of the LQR gain $K$, $x_N^\top P x_N$ is precisely the sum of all future stage costs from time $N$ to infinity. This makes the FHOCP cost function $J$ an approximation of the true infinite-horizon cost.

#### The Lyapunov Stability Proof

With these ingredients—a [terminal constraint](@entry_id:176488) $x_N \in \mathcal{X}_f$ and a terminal cost $V_f(x)$ satisfying a Lyapunov decrease condition within $\mathcal{X}_f$—we can formally prove stability. The proof demonstrates that the optimal [cost function](@entry_id:138681) of the RHC problem, $J_N^*(x)$, serves as a **Lyapunov function** for the closed-loop system. The argument proceeds as follows [@problem_id:2736353]:

1.  Let $J_N^*(x_k)$ be the optimal cost at time $k$. The controller applies $u_k^*$ and the system evolves to $x_{k+1}$.
2.  At time $k+1$, we construct a specific but feasible candidate control sequence. This sequence is formed by taking the "tail" of the optimal sequence from time $k$ (i.e., $\{u_{1|k}^*, \dots, u_{N-1|k}^*\}$) and appending the local terminal controller for the last step ($u=Kx_{N|k}^*$).
3.  The invariance and admissibility properties of the [terminal set](@entry_id:163892) $\mathcal{X}_f$ guarantee that this constructed sequence is feasible for the optimization problem at time $k+1$.
4.  Since the true optimal cost $J_N^*(x_{k+1})$ must be less than or equal to the cost of any feasible candidate, we can establish an inequality relating $J_N^*(x_{k+1})$ to $J_N^*(x_k)$.
5.  By choosing the terminal cost $V_f(x) = x^\top P x$ where $P$ is the solution to the discrete-time Lyapunov equation $V_f((A+BK)x) - V_f(x) = -\ell(x, Kx)$, the inequality simplifies remarkably to:
    $J_N^*(x_{k+1}) - J_N^*(x_k) \le -\ell(x_k, u_k^*)$

Since the stage cost $\ell(x,u)$ is positive definite, this inequality shows that the value function $J_N^*(x)$ strictly decreases along the system's trajectory, proving [asymptotic stability](@entry_id:149743) of the origin.

#### The Role of the Horizon Length, Revisited

A profound consequence of this framework is that with proper terminal ingredients, [asymptotic stability](@entry_id:149743) and [recursive feasibility](@entry_id:167169) are guaranteed for any [prediction horizon](@entry_id:261473) $N \ge 1$ (provided an [initial feasible solution](@entry_id:178716) exists) [@problem_id:2736377]. The stability proof outlined above holds for any $N \ge 1$.

This fundamentally changes the role of the [prediction horizon](@entry_id:261473) $N$. Instead of being a parameter that must be "sufficiently large" to hope for stability, $N$ becomes a tuning parameter for performance. A larger $N$ generally expands the **region of attraction** (the set of initial states for which the problem is feasible) and improves performance (by allowing the controller to find better long-term trade-offs), but the fundamental guarantee of stability rests on the shoulders of the [terminal set](@entry_id:163892) and terminal cost.