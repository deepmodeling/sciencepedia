## Introduction
Model Predictive Control (MPC) stands as a cornerstone of modern control theory, offering a powerful framework for managing complex, [multivariable systems](@entry_id:169616) subject to operational constraints. Unlike traditional controllers with fixed gains, MPC optimizes a system's behavior over a future horizon in real-time, making it uniquely suited for challenges where performance and safety are paramount. However, moving from the concept of MPC to its practical and theoretical implementation involves understanding a sophisticated interplay of prediction, optimization, and [stability theory](@entry_id:149957). This article bridges that gap by providing a structured journey through the world of MPC.

The journey begins in the **Principles and Mechanisms** chapter, where we will dissect the core [receding horizon](@entry_id:181425) strategy, formulate the underlying optimal control problem, and explore the theoretical guarantees for stability. Next, the **Applications and Interdisciplinary Connections** chapter broadens our view, showcasing how the basic framework is extended to handle uncertainty, nonlinearity, economic objectives, and how it connects to fields like synthetic biology and reinforcement learning. Finally, the **Hands-On Practices** section provides concrete exercises to solidify your understanding of these critical concepts.

## Principles and Mechanisms

Model Predictive Control (MPC) is an advanced control methodology predicated on the repeated [online optimization](@entry_id:636729) of a system's predicted future behavior. Unlike classical controllers that employ a fixed, pre-computed control law, MPC determines the control action at each sampling instant by solving a finite-horizon [optimal control](@entry_id:138479) problem. This chapter elucidates the core principles and mechanisms that govern the behavior of MPC, from its fundamental feedback structure to the theoretical constructs that guarantee its stability and performance.

### The Receding Horizon Principle: Feedback Through Re-Optimization

The operational heart of MPC is the **[receding horizon](@entry_id:181425)** (or sliding horizon) strategy. This process can be deconstructed into a repeating sequence of steps executed at each control interval, indexed by time $k$:

1.  **Measure:** The current state of the system, $x_k$, is measured or estimated.
2.  **Predict and Optimize:** Using a mathematical model of the system, the controller predicts the evolution of the state over a future interval of $N$ steps, called the **[prediction horizon](@entry_id:261473)**. It then solves a finite-horizon [optimal control](@entry_id:138479) problem to find an entire sequence of future control inputs, $\{u_{0|k}^*, u_{1|k}^*, \dots, u_{N-1|k}^*\}$, that minimizes a predefined [cost function](@entry_id:138681) while satisfying all system constraints over this horizon.
3.  **Apply:** Only the *first* element of the [optimal control](@entry_id:138479) sequence, $u_{0|k}^*$, is applied to the physical system. That is, the actual control input is set as $u_k = u_{0|k}^*$.
4.  **Discard and Repeat:** The remainder of the [optimal control](@entry_id:138479) sequence, $\{u_{1|k}^*, \dots, u_{N-1|k}^*\}$, is discarded. At the next time step, $k+1$, the horizon "recedes" (or slides forward), and the entire process from Step 1 is repeated using the new measured state $x_{k+1}$.

A crucial question arises from this procedure: why does this repeated open-[loop optimization](@entry_id:751480) result in a closed-loop (feedback) control system? The answer lies in the dependence of the optimal solution on the initial state. At each time $k$, the entire optimization problem is parameterized by the measured state $x_k$, which serves as the initial condition for the prediction. Consequently, the resulting [optimal control](@entry_id:138479) sequence, and specifically its first element $u_{0|k}^*$, is a function of $x_k$. This process implicitly defines a highly complex, state-dependent control law, $u_k = \kappa(x_k)$, where the function $\kappa(\cdot)$ represents the action of solving the optimal control problem and selecting the first input.

Because the control action $u_k$ is a function of the most recent measurement $x_k$, the controller continuously reacts to the actual state of the system. If an unmeasured disturbance or [model-plant mismatch](@entry_id:263118) causes the system state at time $k+1$ to deviate from what was predicted at time $k$, the controller will automatically compensate. At time $k+1$, it solves a new optimization problem based on the *actual* perturbed state $x_{k+1}$, generating a new, corrective control action. This inherent re-planning at every step is the fundamental mechanism that endows MPC with its feedback nature and its notable ability to handle disturbances and uncertainties [@problem_id:2884358].

### Formalizing the Optimal Control Problem

To implement MPC, we must first formulate the finite-horizon [optimal control](@entry_id:138479) problem (FHOCP) that is solved at each time step. For a discrete-time system with dynamics $x_{i+1} = f(x_i, u_i)$, the problem solved at time $k$ (using the measurement $x(k)$) takes the following general form:

Minimize, over the sequence of control inputs $\{u_0, \dots, u_{N-1}\}$, the cost function:
$$ J = \Phi(x_N) + \sum_{i=0}^{N-1} \ell(x_i, u_i) $$

This optimization is subject to the following constraints:
1.  **Initial Condition:** $x_0 = x(k)$
2.  **System Dynamics:** $x_{i+1} = f(x_i, u_i)$ for $i = 0, \dots, N-1$
3.  **State and Input Constraints:** $x_i \in \mathcal{X}$ and $u_i \in \mathcal{U}$ for $i=0, \dots, N-1$
4.  **Terminal Constraint:** $x_N \in \mathcal{X}_f$

Here, $\ell(x_i, u_i)$ is the **stage cost**, which penalizes undesirable states and excessive control effort at each step $i$ along the horizon. $\Phi(x_N)$ is the **terminal cost**, which penalizes the final predicted state $x_N$. The sets $\mathcal{X}$ and $\mathcal{U}$ represent physical or operational limits on states and inputs, respectively. The **[terminal set](@entry_id:163892)** $\mathcal{X}_f$ is a specially designed subset of $\mathcal{X}$ that is crucial for guaranteeing stability, as will be discussed later.

For discrete-time Linear Time-Invariant (LTI) systems, $x_{k+1} = Ax_k + Bu_k$, a canonical and widely used formulation employs quadratic costs [@problem_id:2724696]. The stage cost is typically $\ell(x, u) = x^\top Q x + u^\top R u$, and the terminal cost is $\Phi(x_N) = x_N^\top P x_N$. The matrices $Q$ and $R$ are positive semidefinite and [positive definite](@entry_id:149459), respectively, allowing the designer to specify the relative importance of regulating the state towards the origin versus minimizing control energy. The matrix $P$ is a positive semidefinite terminal weight. The constraint sets $\mathcal{X}$ and $\mathcal{U}$ are often convex [polytopes](@entry_id:635589), representable by linear inequalities. This LTI formulation with quadratic costs results in a Quadratic Program (QP), a class of [optimization problems](@entry_id:142739) that can be solved very efficiently.

### From Dynamic Problem to Solvable QP

Solving the constrained FHOCP at each time step requires casting it into a standard mathematical programming format. For LTI systems with linear constraints, this format is a QP. The transformation involves two key steps: creating a "lifted" model of the dynamics and then condensing the cost and constraints into a matrix-vector representation.

#### The Lifted Prediction Model

The recursive nature of the LTI dynamics $x_{i+1} = Ax_i + Bu_i$ can be unrolled over the [prediction horizon](@entry_id:261473) $N$ to express all future predicted states as a single linear function of the initial state $x_k$ and the entire sequence of future inputs.

Let us define the stacked vector of future inputs as $U = [u_k^\top, u_{k+1}^\top, \dots, u_{k+N-1}^\top]^\top \in \mathbb{R}^{Nm}$ and the stacked vector of future predicted states as $X = [x_{k+1}^\top, x_{k+2}^\top, \dots, x_{k+N}^\top]^\top \in \mathbb{R}^{Nn}$. By successively substituting the state equation, we can derive the following relationship [@problem_id:2884331]:
$$ X = S_x x_k + S_u U $$
where $x_k$ is the state measured at the current time. The matrices $S_x \in \mathbb{R}^{Nn \times n}$ and $S_u \in \mathbb{R}^{Nn \times Nm}$ are the prediction matrices, given by:
$$ S_x = \begin{bmatrix} A \\ A^2 \\ \vdots \\ A^N \end{bmatrix}, \quad S_u = \begin{bmatrix} B & 0 & \cdots & 0 \\ AB & B & \cdots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ A^{N-1}B & A^{N-2}B & \cdots & B \end{bmatrix} $$
The matrix $S_x$ captures the evolution of the state due to the initial condition (the [zero-input response](@entry_id:274925)), while $S_u$ captures the evolution due to the control inputs (the [zero-state response](@entry_id:273280)). The matrix $S_u$ has a distinctive block lower-triangular Toeplitz structure, reflecting the causality of the system: the input $u_{k+j}$ can only affect states from time $k+j+1$ onwards.

#### Condensing the Cost and Constraints

With the lifted model, we can eliminate the state sequence $X$ from the optimization problem, leaving only the input sequence $U$ as the decision variable.

First, the quadratic [cost function](@entry_id:138681) for a general tracking problem can be written in a compact form. Let the total cost be $J = (X - \bar{r})^\top \bar{Q} (X - \bar{r}) + (U - \bar{v})^\top \bar{R} (U - \bar{v})$, where $\bar{r}$ and $\bar{v}$ are stacked reference trajectories for the states and inputs, and $\bar{Q} = \text{diag}(Q, \dots, Q, P)$ and $\bar{R} = \text{diag}(R, \dots, R)$ are block-diagonal weighting matrices. Substituting $X = S_x x_k + S_u U$ into this expression and rearranging terms yields a standard quadratic form in $U$ [@problem_id:2884306]:
$$ J(U) = \frac{1}{2} U^\top H U + f^\top U + \text{constant} $$
The Hessian matrix $H$ and the linear coefficient vector $f$ are given by:
$$ H = 2(S_u^\top \bar{Q} S_u + \bar{R}) $$
$$ f = 2(S_u^\top \bar{Q} (S_x x_k - \bar{r}) - \bar{R} \bar{v}) $$
Note that the Hessian $H$ is constant, while the linear term $f$ depends on the current state $x_k$ and the reference trajectories, and must be recomputed at each time step.

Second, the constraints on states and inputs must also be expressed in terms of $U$. If the state and input constraints are defined by [polytopes](@entry_id:635589), e.g., $\mathcal{X} = \{x | H_x x \le h_x\}$ and $\mathcal{U} = \{u | H_u u \le h_u\}$, we can stack these inequalities for all time steps along the horizon. Using the lifted model to substitute for the state variables, we arrive at a single, large [linear inequality](@entry_id:174297) that constrains the decision variable $U$ [@problem_id:2724707]:
$$ G U \le w $$
The full constraint matrix and vector incorporate the input constraints directly and the [state constraints](@entry_id:271616) via the prediction matrices:
$$ \begin{bmatrix} I \otimes H_u \\ (I \otimes H_x) S_u \end{bmatrix} U \le \begin{bmatrix} \mathbf{1} \otimes h_u \\ (\mathbf{1} \otimes h_x) - (I \otimes H_x) S_x x_k \end{bmatrix} $$
This expression neatly separates the constant parts of the constraints from the part that depends on the current state $x_k$.

By combining the condensed cost function and condensed constraints, the entire MPC problem for an LTI system is reduced at each time step to solving a standard QP of the form:
$$ \min_U \quad \frac{1}{2} U^\top H U + f(x_k)^\top U \quad \text{subject to} \quad G U \le w(x_k) $$
This QP can be passed to a highly optimized numerical solver, which returns the optimal control sequence $U^*$. The controller then implements the first part of this solution, $u_k = u_{0|k}^*$.

### Stability and Recursive Feasibility

While MPC is powerful, its finite [prediction horizon](@entry_id:261473) presents a significant theoretical challenge: myopic optimization does not inherently guarantee long-term stability. A key goal of MPC design is to select the problem ingredients—specifically the terminal cost $\Phi(x_N)$ and [terminal set](@entry_id:163892) $\mathcal{X}_f$—to provide provable guarantees of **[asymptotic stability](@entry_id:149743)** and **[recursive feasibility](@entry_id:167169)**.

-   **Recursive Feasibility:** This property ensures that if the optimization problem is feasible at time $k$, it will remain feasible for all future times $k+1, k+2, \dots$. Without this, the controller could fail at some point by being unable to find a valid control sequence.
-   **Asymptotic Stability:** This property ensures that, in the absence of persistent disturbances, the system state will converge to the desired equilibrium point (typically the origin).

The standard method for proving these properties relies on Lyapunov theory. The optimal cost of the MPC problem, $J^*(x_k)$, is used as a candidate **Lyapunov function**. The proof requires showing that (a) $J^*(x_k)$ is [positive definite](@entry_id:149459) and (b) it strictly decreases along the trajectory of the system under MPC control, i.e., $J^*(x_{k+1})  J^*(x_k)$ for all $x_k \neq 0$.

The terminal ingredients, $\mathcal{X}_f$ and $\Phi(x_N) = x_N^\top P x_N$, are the tools to enforce this behavior. A sufficient set of conditions for stability involves designing these elements to work in concert [@problem_id:2884303] [@problem_id:2724726]:

1.  **A Stabilizing Terminal Controller:** A local control law, $u = Kx$, is defined, which is known to be stabilizing for the system.
2.  **A Positively Invariant Terminal Set:** The [terminal set](@entry_id:163892) $\mathcal{X}_f$ is chosen to be a **positively invariant** set for the system under the terminal control law $u=Kx$. This means that for any state $x \in \mathcal{X}_f$, the next state $(A+BK)x$ is also in $\mathcal{X}_f$. Furthermore, the constraints must be satisfied within this set, meaning for all $x \in \mathcal{X}_f$, we have $x \in \mathcal{X}$ and $Kx \in \mathcal{U}$.
3.  **A Terminal Cost as a Local Lyapunov Function:** The terminal cost $\Phi(x_N)$ must act as a Lyapunov function within the [terminal set](@entry_id:163892). Specifically, the matrix $P$ is chosen such that for any state $x \in \mathcal{X}_f$, the cost decreases along the trajectory dictated by the terminal controller: $x^\top P x - ((A+BK)x)^\top P ((A+BK)x) \ge \ell(x, Kx)$.

When these conditions are met, a feasible path always exists for the next time step's optimization: simply use the tail of the previous optimal plan followed by the terminal controller $K$. This guarantees [recursive feasibility](@entry_id:167169). The Lyapunov decrease condition on $P$ ensures that the value function $J^*(x_k)$ will decrease at each step, guaranteeing [asymptotic stability](@entry_id:149743). It is useful to distinguish positive invariance from the weaker notion of **controlled invariance**, where for any state in a set, there merely *exists* some admissible control to keep the next state in the set. While controlled invariance is sufficient for [recursive feasibility](@entry_id:167169) arguments, the stronger positive invariance property under a *fixed* law is typically used in the stability proof [@problem_id:2884349].

#### The Connection to LQR

A particularly elegant and systematic method for selecting the terminal ingredients is to leverage the theory of the infinite-horizon Linear Quadratic Regulator (LQR). For an unconstrained LTI system, the LQR provides the globally optimal control law $u = Kx$ that minimizes $\sum_{i=0}^\infty (x_i^\top Q x_i + u_i^\top R u_i)$.

The key insight is to choose the terminal components of the MPC formulation to match the LQR solution [@problem_id:2884350] [@problem_id:2884303]:
-   Set the terminal control law gain $K$ to be the LQR gain.
-   Set the terminal [cost matrix](@entry_id:634848) $P$ to be the unique, [positive definite](@entry_id:149459) solution of the corresponding **Discrete-time Algebraic Riccati Equation (DARE)**.

This choice has a profound consequence. The terminal cost $x_N^\top P x_N$ now represents the exact optimal cost-to-go from state $x_N$ to the origin over an infinite horizon using the LQR controller. This special choice of $P$ satisfies the Lyapunov decrease condition with equality: $x^\top P x - ((A+BK)x)^\top P ((A+BK)x) = \ell(x, Kx)$. This establishes the terminal cost as a perfect local Lyapunov function, providing the strongest possible stability guarantee and often leading to the largest possible region of attraction for the MPC controller.

### Practical Refinement: Soft Constraints

In practice, unforeseen disturbances can sometimes push the system into a state from which it is impossible to satisfy the hard [state constraints](@entry_id:271616) over the [prediction horizon](@entry_id:261473), rendering the QP infeasible. To prevent such controller failure, **soft constraints** are a common and effective mechanism.

The idea is to introduce non-negative **[slack variables](@entry_id:268374)**, often denoted by $\epsilon$, into the constraints, allowing them to be violated if necessary. For instance, a state constraint $H_x x_i \le h_x$ can be softened to $H_x x_i \le h_x + \epsilon_i$, where $\epsilon_i \ge 0$. To ensure that these violations are used sparingly and only when unavoidable, a penalty term is added to the cost function. The choice of [penalty function](@entry_id:638029) has a significant impact on the controller's behavior [@problem_id:2884364].

Two common choices are the $L_1$ and $L_2$ penalties:
-   **$L_1$ Penalty:** A term of the form $\sum_i \rho_i^\top |\epsilon_i|_1$ is added to the cost. A key property of the $L_1$ penalty is **exact penalization**. This means there exists a finite penalty weight $\rho$ above which the [slack variable](@entry_id:270695) $\epsilon_i$ will be driven to zero if the original hard constraint is satisfiable. The controller will only use the slack if it is truly impossible to satisfy the hard constraint. This makes the $L_1$ penalty very effective at enforcing constraints whenever possible.

-   **$L_2$ Penalty:** A term of the form $\sum_i \epsilon_i^\top S \epsilon_i$ (where $S$ is a [positive definite matrix](@entry_id:150869)) is added to the cost. The [quadratic penalty](@entry_id:637777) is smooth and easy to handle in QP solvers. However, it does not possess the exact penalization property. For any finite penalty weight, if the unconstrained optimal trajectory violates a constraint, the soft-constrained solution will still exhibit a small, non-zero violation. The violation only vanishes in the limit as the penalty weight approaches infinity.

In general, as the penalty weight $\rho$ increases, the magnitude of the allowed violation $\epsilon^*$ decreases. The choice between penalty types depends on the application: $L_1$ is preferred when [constraint satisfaction](@entry_id:275212) is critical if feasible, while $L_2$ provides a smoother trade-off between tracking performance and [constraint violation](@entry_id:747776). The use of soft constraints transforms MPC into a more robust and practical control strategy, capable of handling unexpected events without abrupt failure.