## Introduction
Model Predictive Control (MPC) has emerged as a premier advanced control strategy, indispensable for managing the complex dynamics and operational constraints inherent in modern cyber-physical systems. Unlike traditional controllers that rely on fixed feedback laws, MPC leverages an explicit system model and [online optimization](@entry_id:636729) to make intelligent, forward-looking decisions. However, understanding its inner workings—from mathematical formulation to stability guarantees and practical application—presents a significant learning curve. This article bridges that gap by providing a structured journey into the world of MPC.

The following chapters will guide you from core theory to real-world impact. First, "Principles and Mechanisms" will dissect the fundamental concepts of MPC, including the [receding horizon](@entry_id:181425) principle, its formulation as a solvable Quadratic Program, and the critical techniques used to ensure [system stability](@entry_id:148296) and robustness. Next, "Applications and Interdisciplinary Connections" will showcase the versatility of MPC, exploring how the core framework is extended to handle challenges like steady-state errors, economic objectives, and malicious attacks across fields such as energy systems and biomedical engineering. Finally, "Hands-On Practices" will offer targeted problems to solidify your understanding of key computational and design aspects of MPC.

## Principles and Mechanisms

Model Predictive Control (MPC) is a powerful and versatile control strategy that has found widespread application in complex cyber-physical systems. Its efficacy stems from a unique combination of [online optimization](@entry_id:636729), explicit use of a system model, and systematic handling of constraints. This chapter delves into the fundamental principles and mechanisms that underpin MPC, moving from its core operational concept to the mathematical machinery that enables its implementation and guarantees its performance. We will explore how MPC is formulated as a solvable optimization problem, the critical role of terminal conditions in ensuring stability, and extensions that provide robustness against real-world uncertainties.

### The Receding Horizon Principle: Implicit Feedback through Re-planning

At the heart of Model Predictive Control lies the **[receding horizon](@entry_id:181425)** (or **sliding horizon**) principle. Unlike classical controllers that employ a fixed, pre-computed control law, MPC operates through a repetitive, three-step process at each sampling instant $k$:

1.  **Measure**: The controller acquires the current state of the system, $x_k$.
2.  **Optimize**: The controller solves a finite-horizon, open-loop [optimal control](@entry_id:138479) problem. This involves using a mathematical model of the system to predict its future evolution over a **[prediction horizon](@entry_id:261473)** of $N$ steps. The optimizer computes an entire sequence of future control inputs, $\{u_{0|k}^*, u_{1|k}^*, \dots, u_{N-1|k}^*\}$, that minimizes a predefined cost function while satisfying all system constraints.
3.  **Apply**: Despite having computed a full sequence of optimal inputs, the controller implements only the *first* element of this sequence, $u_k = u_{0|k}^*$, to the plant. The rest of the sequence, $\{u_{1|k}^*, \dots, u_{N-1|k}^*\}$, is discarded.

At the next time step, $k+1$, the horizon "recedes" or "slides" forward, and the entire process is repeated with the new measured state, $x_{k+1}$.

This seemingly simple procedure of re-planning at every step is precisely what endows MPC with the characteristics of a **closed-loop feedback** controller . Although the optimization solved at any given time $k$ is an *open-loop* problem (i.e., it determines a sequence of inputs based only on the state at time $k$ without considering future measurements), the overall strategy is closed-loop. The solution to the optimization problem, specifically the first control input $u_{0|k}^*$, is a function of the initial state $x_k$ used to initialize the optimization. We can therefore think of the entire measure-optimize-apply cycle as implicitly defining a highly complex, nonlinear state-feedback law, $u_k = \kappa(x_k)$. Because this control law is re-evaluated at every step based on the most recent state measurement, it allows the controller to react and compensate for deviations from the predicted path caused by external disturbances or mismatch between the predictive model and the real plant. This constant re-planning is the fundamental mechanism that generates feedback in MPC.

### The Anatomy of the Optimization Problem

The effectiveness of MPC hinges on our ability to formulate and efficiently solve the [optimal control](@entry_id:138479) problem at each time step. For a broad and important class of systems—Linear Time-Invariant (LTI) systems with quadratic costs—this problem can be transformed into a standard convex Quadratic Program (QP), for which highly efficient numerical solvers exist. Let us dissect this transformation.

#### State Prediction for LTI Systems

The foundation of MPC is the predictive model. Consider a discrete-time LTI system described by the state-space equation:

$x_{k+1} = A x_k + B u_k$

where $x_k \in \mathbb{R}^n$ is the state, $u_k \in \mathbb{R}^m$ is the control input, and $A$ and $B$ are constant matrices of appropriate dimensions. To optimize over a future horizon, we must be able to express future states as a function of the current state $x_k$ and the sequence of future inputs $\{u_k, u_{k+1}, \dots\}$.

By recursively applying the [state-space](@entry_id:177074) equation, we can unroll the dynamics :

The state one step ahead is simply:
$x_{k+1} = A x_k + B u_k$

Two steps ahead, we have:
$x_{k+2} = A x_{k+1} + B u_{k+1} = A (A x_k + B u_k) + B u_{k+1} = A^2 x_k + A B u_k + B u_{k+1}$

Continuing this process, the state $i$ steps into the future, $x_{k+i}$, can be expressed in a [closed form](@entry_id:271343):

$x_{k+i} = A^i x_k + \sum_{j=0}^{i-1} A^{i-1-j} B u_{k+j}$

This equation is the cornerstone of prediction in linear MPC. It shows that any future state is an [affine function](@entry_id:635019) of the current state $x_k$ and the sequence of control inputs $\{u_k, \dots, u_{k+i-1}\}$. The first term, $A^i x_k$, represents the **free response** of the system (how the state evolves from $x_k$ with zero input), while the summation represents the **[forced response](@entry_id:262169)** due to the control inputs.

#### The Lifted Representation and QP Formulation

While the [recursive formula](@entry_id:160630) is insightful, for optimization purposes it is more convenient to express the entire predicted state trajectory in a single [matrix equation](@entry_id:204751). We can stack the predicted states and future inputs into large column vectors:

$X = \begin{bmatrix} x_{k+1} \\ x_{k+2} \\ \vdots \\ x_{k+N} \end{bmatrix} \in \mathbb{R}^{Nn}, \quad U = \begin{bmatrix} u_{k} \\ u_{k+1} \\ \vdots \\ u_{k+N-1} \end{bmatrix} \in \mathbb{R}^{Nm}$

Using the prediction formula derived above for each state from $x_{k+1}$ to $x_{k+N}$, we can construct a **lifted representation** of the system dynamics :

$X = S_x x_k + S_u U$

Here, the matrices $S_x$ and $S_u$ encapsulate the system's dynamics over the entire horizon:

$S_x = \begin{bmatrix} A \\ A^2 \\ \vdots \\ A^N \end{bmatrix}, \quad S_u = \begin{bmatrix} B  0  \cdots  0 \\ AB  B  \cdots  0 \\ \vdots  \vdots  \ddots  \vdots \\ A^{N-1}B  A^{N-2}B  \cdots  B \end{bmatrix}$

The matrix $S_x$ maps the current state $x_k$ to the free response of the system over the horizon, while the block [lower-triangular matrix](@entry_id:634254) $S_u$ maps the entire input sequence $U$ to the [forced response](@entry_id:262169).

Now, consider a standard quadratic cost function for MPC, aiming to minimize tracking errors and control effort:

$J = \sum_{i=1}^{N} (x_{k+i} - r_{k+i})^T Q_{i} (x_{k+i} - r_{k+i}) + \sum_{i=0}^{N-1} (u_{k+i} - v_{k+i})^T R (u_{k+i} - v_{k+i})$

where $r_{k+i}$ and $v_{k+i}$ are state and input reference targets, and $Q_i$ and $R$ are positive (semi)definite weighting matrices. The terminal state cost for $i=N$ is often denoted with a separate matrix, $P$, so $Q_N = P$. Using stacked notation, this cost function can be written compactly as:

$J = (X - \bar{r})^T \bar{Q} (X - \bar{r}) + (U - \bar{v})^T \bar{R} (U - \bar{v})$

where $\bar{Q} = \text{diag}(Q_1, \dots, Q_{N-1}, P)$ and $\bar{R} = \text{diag}(R, \dots, R)$.

The final step is to substitute the lifted model $X = S_x x_k + S_u U$ into the cost function. This eliminates the state vector $X$ and expresses the cost solely as a function of the decision variable $U$ . After algebraic expansion, the cost function takes the standard [quadratic form](@entry_id:153497):

$J(U) = \frac{1}{2}U^T H U + f^T U + c$

The Hessian matrix $H$ and the linear coefficient vector $f$ are given by:

$H = 2(S_u^T \bar{Q} S_u + \bar{R})$

$f = 2(S_u^T \bar{Q} (S_x x_k - \bar{r}) - \bar{R} \bar{v})$

The term $c$ is a constant that depends on $x_k$ and the references, but not on $U$, and can therefore be ignored by the optimizer.

Any [linear constraints](@entry_id:636966) on the states and inputs, such as $E_x x_{k+i} + E_u u_{k+i} \le e$, can also be rewritten in terms of $U$ using the lifted model, resulting in a set of linear inequalities of the form $A_{ineq} U \le b_{ineq}$. The MPC problem is thus reduced to a standard **Quadratic Program (QP)**:

$\min_{U} \frac{1}{2}U^T H U + f^T U$
subject to $A_{ineq} U \le b_{ineq}$

For this QP to be efficiently and reliably solvable, it must be **convex**. Since the feasible set defined by [linear constraints](@entry_id:636966) is always convex, [convexity](@entry_id:138568) hinges on the objective function being convex, which requires the Hessian matrix $H$ to be positive semidefinite ($H \succeq 0$). From the expression for $H$, this is guaranteed if the weighting matrices $\bar{Q}$ and $\bar{R}$ are positive semidefinite. In practice, $R$ is almost always chosen to be strictly [positive definite](@entry_id:149459) ($R \succ 0$) to penalize control effort and ensure a unique solution.

More generally, if a cross-term $2x_k^T S u_k$ is present in the stage cost, the condition for convexity becomes that the [block matrix](@entry_id:148435) $\begin{pmatrix} Q  S \\ S^T  R \end{pmatrix}$ must be positive semidefinite. A practical test for this, given $R \succ 0$, is the Schur complement condition: $Q - S R^{-1} S^T \succeq 0$ .

### Ensuring Stability and Recursive Feasibility

Formulating MPC as a solvable QP is only part of the story. A critical challenge, especially in [constrained systems](@entry_id:164587), is to provide formal guarantees of performance. Two properties are paramount:

1.  **Recursive Feasibility**: If a [feasible solution](@entry_id:634783) to the optimization problem exists at time $k$, a [feasible solution](@entry_id:634783) must also exist for all future times $k' > k$. Without this, the controller could fail at some point, leaving the system without a valid control input.
2.  **Asymptotic Stability**: The state of the closed-loop system must converge to the desired equilibrium point (typically the origin) as time progresses.

Naively implementing MPC with a finite horizon provides neither of these guarantees. The key to achieving them lies in augmenting the optimization problem with a carefully designed **terminal cost** and **[terminal constraint](@entry_id:176488) set**.

The standard approach introduces a [terminal set](@entry_id:163892) $X_f$ and a terminal cost $V_f(x)$. The optimization problem is modified to include the constraint that the predicted state at the end of the horizon, $x_{k+N}$, must lie within this set: $x_{k+N} \in X_f$. The term $V_f(x_{k+N})$ is added to the cost function.

The role of this terminal apparatus is twofold . To understand it, we introduce the concept of a **terminal controller**, $u = \kappa(x)$, which is a pre-designed stabilizing feedback law defined for states within the [terminal set](@entry_id:163892) $X_f$. The [terminal set](@entry_id:163892) and cost are then chosen to satisfy three crucial properties:

1.  **Positive Invariance**: The set $X_f$ must be **positively invariant** under the terminal control law $\kappa(x)$. This means that for any state $x \in X_f$, applying the control $u = \kappa(x)$ results in a next state $x^+ = A x + B \kappa(x)$ that is also in $X_f$. Furthermore, the constraints must be satisfied within this set: $x \in X_f \implies x \in \mathcal{X}$ and $\kappa(x) \in \mathcal{U}$.
2.  **Lyapunov Decrease**: The terminal cost $V_f(x)$ must act as a **Lyapunov function** within the [terminal set](@entry_id:163892). Specifically, for any $x \in X_f$, it must decrease along trajectories generated by the terminal controller: $V_f(A x + B \kappa(x)) - V_f(x) \le -\ell(x, \kappa(x))$, where $\ell(x,u)$ is the stage cost.

These properties provide the necessary guarantees. **Recursive feasibility** is proven by construction. At time $k+1$, we can always construct a feasible (though likely suboptimal) input sequence by taking the tail of the optimal sequence from time $k$ and appending the terminal control action $\kappa(x_{k+N|k}^*)$. The positive invariance of $X_f$ ensures that this new sequence satisfies all constraints, including the [terminal constraint](@entry_id:176488).

**Asymptotic stability** is proven by showing that the optimal cost of the MPC problem, $J_N^*(x)$, is itself a Lyapunov function for the overall closed-loop system. The Lyapunov decrease condition on $V_f$ is the critical ingredient that ensures the value of $J_N^*(x)$ decreases at every time step, driving the state towards the origin.

The concept of **positive invariance** used here is distinct from the related notion of **controlled invariance** . A set is controlled invariant if for every state within it, there *exists* some admissible control to keep the next state in the set. In contrast, positive invariance for a [terminal set](@entry_id:163892) requires that for every state within it, a *specific* control law $\kappa(x)$ keeps the next state in the set. This stronger condition is what enables the rigorous stability proof.

### The LQR Connection: A Canonical Design

A powerful and elegant method for designing the terminal cost and controller is to draw upon the theory of the infinite-horizon Linear Quadratic Regulator (LQR). For an unconstrained LTI system, the LQR problem seeks to minimize a quadratic cost over an infinite horizon. Its solution is a linear state-feedback law $u_k = K x_k$, where the gain $K$ and the optimal cost-to-go $V^*(x) = x^T P x$ are found by solving the **Discrete Algebraic Riccati Equation (DARE)**.

This provides a canonical choice for the terminal ingredients in MPC :

*   **Terminal Controller**: Use the LQR gain, $\kappa(x) = Kx$.
*   **Terminal Cost**: Use the LQR value function, $V_f(x) = x^T P x$, where $P$ is the solution to the DARE corresponding to the stage cost weights $(Q,R)$.

This choice is special because the LQR [value function](@entry_id:144750) $x^T P x$ exactly satisfies the Lyapunov decrease condition with equality: $V_f((A+BK)x) - V_f(x) = -\ell(x, Kx)$. This property leads to a remarkable result for the unconstrained case: if the terminal cost is the DARE solution $P$, the finite-horizon MPC law becomes identical to the infinite-horizon LQR law, $u_k = Kx_k$, and the optimal cost is simply $x_k^T P x_k$, regardless of the horizon length $N$ .

In the constrained case, this LQR-based design provides a complete recipe for stabilizing MPC. The full set of [sufficient conditions](@entry_id:269617) for [asymptotic stability](@entry_id:149743) is:
1.  The system $(A,B)$ is stabilizable and $(A, Q^{1/2})$ is detectable.
2.  The terminal cost is $V_f(x) = x^T P x$, where $P$ is the stabilizing solution to the DARE.
3.  The [terminal set](@entry_id:163892) $X_f$ is a positively invariant set under the closed-loop dynamics $x^+ = (A+BK)x$.
4.  Within this set $X_f$, the state and input constraints are satisfied (i.e., $X_f \subseteq \mathcal{X}$ and $Kx \in \mathcal{U}$ for all $x \in X_f$).

### Introduction to Robust MPC: Handling Uncertainty

The principles discussed so far assume a perfect model and no disturbances. In reality, cyber-physical systems are subject to both. **Robust MPC** extends the framework to provide formal guarantees in the presence of bounded uncertainty. A prominent approach is **tube-based MPC**.

The central idea is to decompose the actual state trajectory $x_k$ into a predictable **nominal trajectory** $\bar{x}_k$ and a bounded **error trajectory** $e_k = x_k - \bar{x}_k$ . The control input is similarly decomposed into a nominal part $\bar{u}_k$ and a local feedback part designed to counteract the error:

$u_k = \bar{u}_k + K(x_k - \bar{x}_k) = \bar{u}_k + K e_k$

Given a system with additive disturbances $x_{k+1} = A x_k + B u_k + w_k$, where $w_k$ belongs to a known set $\mathcal{W}$, we can derive separate dynamics for the nominal and error components:

*   **Nominal Dynamics**: $\bar{x}_{k+1} = A \bar{x}_k + B \bar{u}_k$
*   **Error Dynamics**: $e_{k+1} = (A+BK) e_k + w_k$

The MPC controller optimizes the nominal trajectory $\{\bar{u}_k, \bar{x}_k\}$ using the predictable, disturbance-free nominal model. The ancillary feedback gain $K$ is pre-designed to ensure the error dynamics are stable and the error $e_k$ remains confined to a small set, or "tube," around the origin. This tube is formally characterized by a **Robust Positively Invariant (RPI)** set $\mathcal{Z}$, which has the property that if $e_k \in \mathcal{Z}$, then $e_{k+1}$ is guaranteed to be in $\mathcal{Z}$ for any possible disturbance $w_k \in \mathcal{W}$.

To guarantee that the *actual* state $x_k$ and input $u_k$ satisfy their constraints, the constraints on the *nominal* system are tightened. Since $x_k = \bar{x}_k + e_k$ and $e_k \in \mathcal{Z}$, the nominal state must be restricted to a smaller set such that even the [worst-case error](@entry_id:169595) will not cause a [constraint violation](@entry_id:747776). This is achieved using the **Pontryagin [set difference](@entry_id:140904)**:

*   Tightened State Constraint: $\bar{x}_k \in \mathcal{X} \ominus \mathcal{Z} = \{x \mid x+z \in \mathcal{X} \text{ for all } z \in \mathcal{Z} \}$
*   Tightened Input Constraint: $\bar{u}_k \in \mathcal{U} \ominus K\mathcal{Z} = \{u \mid u+v \in \mathcal{U} \text{ for all } v \in K\mathcal{Z} \}$

By planning for the nominal system within these tightened constraints, tube-based MPC ensures that the real, disturbed system will remain feasible and satisfy its constraints for all time, providing a powerful mechanism for robust control of uncertain systems.