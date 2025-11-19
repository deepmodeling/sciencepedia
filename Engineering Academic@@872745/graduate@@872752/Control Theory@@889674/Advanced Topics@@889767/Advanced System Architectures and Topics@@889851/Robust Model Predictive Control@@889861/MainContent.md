## Introduction
Model Predictive Control (MPC) has become a [dominant strategy](@entry_id:264280) for controlling [constrained systems](@entry_id:164587), but its reliance on a perfect 'nominal' model presents a critical vulnerability in real-world applications. Physical systems are inevitably subject to disturbances, sensor noise, and modeling errors, creating a significant gap between theoretical performance and practical reality. A controller designed for an idealized system may fail catastrophically when faced with uncertainty, violating safety constraints and losing stability. Robust Model Predictive Control (RMPC) directly confronts this challenge, providing a rigorous framework to design high-performance controllers that offer formal guarantees of safety and stability despite unknown but bounded uncertainties.

This article provides a comprehensive graduate-level exploration of RMPC. We will begin by dissecting the mathematical toolkit—including set theory, [invariant sets](@entry_id:275226), and the Pontryagin difference—that underpins robust guarantees in "Principles and Mechanisms," where premier strategies like tube-based and min-max MPC are explored. Following this, "Applications and Interdisciplinary Connections" demonstrates the versatility of these methods in solving complex engineering challenges, from [actuator saturation](@entry_id:274581) and communication delays to [distributed control](@entry_id:167172) and biomedical applications. Finally, "Hands-On Practices" offers guided problems to translate these theoretical concepts into practical computational skills. We begin by establishing the fundamental shift in thinking required to move from nominal MPC to its [robust counterpart](@entry_id:637308).

## Principles and Mechanisms

Having established the foundational principles of Model Predictive Control (MPC) for nominal, disturbance-free systems in the preceding chapter, we now turn our attention to the more realistic and challenging scenario where the system is subject to uncertainty. Real-world systems are invariably affected by external disturbances, [measurement noise](@entry_id:275238), and [unmodeled dynamics](@entry_id:264781). A controller designed solely for a nominal model may perform poorly or, more critically, violate system constraints when implemented on a physical plant. Robust Model Predictive Control (RMPC) is a branch of MPC that provides a framework for designing controllers that can guarantee [constraint satisfaction](@entry_id:275212) and stability despite the presence of bounded uncertainty. This chapter elucidates the core principles and mechanisms that underpin these guarantees.

### From Nominal to Robust MPC: The Fundamental Challenge

Let us first recall the standard formulation of nominal MPC for a discrete-time Linear Time-Invariant (LTI) system, $x_{k+1} = Ax_k + Bu_k$. At each time step $k$, given a state measurement $x_k$, the controller solves a finite-horizon optimal control problem [@problem_id:2741130]. A typical formulation seeks to minimize a quadratic [cost function](@entry_id:138681) over a [prediction horizon](@entry_id:261473) $N$:

$$
J_N(x_k, \{u_{i|k}\}) = \sum_{i=0}^{N-1} (x_{i|k}^{\top}Q x_{i|k} + u_{i|k}^{\top}R u_{i|k}) + x_{N|k}^{\top}P x_{N|k}
$$

subject to the constraints:
1.  $x_{0|k} = x_k$
2.  $x_{i+1|k} = A x_{i|k} + B u_{i|k}$ for $i \in \{0, \dots, N-1\}$
3.  $x_{i|k} \in \mathcal{X}$ and $u_{i|k} \in \mathcal{U}$ for $i \in \{0, \dots, N-1\}$
4.  $x_{N|k} \in \mathcal{X}_f$

Here, $\mathcal{X}$ and $\mathcal{U}$ are state and input constraint sets, while $\mathcal{X}_f$ is a carefully chosen **[terminal set](@entry_id:163892)** and $P$ is a **terminal cost** matrix. These terminal ingredients are crucial for ensuring the **[recursive feasibility](@entry_id:167169)** (the ability to always find a solution) and **[asymptotic stability](@entry_id:149743)** of the closed-loop system. The controller then implements only the first element of the optimal input sequence, $u_k = u_{0|k}^{\star}$, and repeats the entire process at the next time step—a strategy known as the **[receding horizon](@entry_id:181425) principle**.

The fundamental challenge arises when the [system dynamics](@entry_id:136288) are uncertain. We can broadly classify uncertainty into two categories [@problem_id:2736375]:
-   **Additive Disturbances**: The system is affected by an unknown but bounded additive term, e.g., $x_{k+1} = Ax_k + Bu_k + w_k$, where the disturbance $w_k$ belongs to a known set $\mathcal{W}$.
-   **Parametric Uncertainty**: The system matrices themselves are uncertain, e.g., $x_{k+1} = A(\theta_k)x_k + B(\theta_k)u_k$, where the parameter vector $\theta_k$ lies in a known set.

In either case, the nominal prediction model $x_{i+1|k} = A x_{i|k} + B u_{i|k}$ is no longer accurate. The actual state trajectory will deviate from the planned nominal trajectory, potentially leading to constraint violations. A robust controller must account for all possible realizations of the uncertainty to provide guarantees.

### The Objectives of Robust Control

An RMPC controller must satisfy three fundamental properties:

1.  **Robust Constraint Satisfaction**: The state and input constraints, $x_k \in \mathcal{X}$ and $u_k \in \mathcal{U}$, must be satisfied for all time and for *every* possible sequence of disturbances allowed by the uncertainty model.

2.  **Recursive Feasibility**: If the RMPC optimization problem is feasible at the current time step for the measured state $x_k$, it must remain feasible at the next time step for any possible successor state $x_{k+1}$ that can result from any admissible disturbance $w_k$ [@problem_id:2741149]. This property ensures the controller can always compute a valid control action.

3.  **Robust Stability**: In the presence of persistent disturbances, convergence to the origin is generally not possible. Instead, we seek a property known as **Input-to-State Stability (ISS)** [@problem_id:2741150]. The system is ISS if the state remains bounded, with the ultimate bound on the state's norm, $\lVert x_k \rVert$, being proportional to the magnitude of the supremum of the disturbance norm, $\sup_j \lVert w_j \rVert$. Formally, there must exist functions $\beta \in \mathcal{KL}$ (a function that is class-$\mathcal{K}$ in its first argument and decreasing to zero in its second) and $\gamma \in \mathcal{K}$ (a continuous, strictly increasing function with $\gamma(0)=0$) such that:
    $$
    \lVert x_k \rVert \le \beta(\lVert x_0 \rVert, k) + \gamma\left(\sup_{j \ge 0} \lVert w_j \rVert\right)
    $$
    This elegant definition ensures that the influence of the initial condition decays to zero, while the steady-state error is bounded by a function of the disturbance magnitude. Critically, if the disturbances vanish ($w_k \equiv 0$), the system becomes asymptotically stable to the origin. This provides a rigorous and practical notion of robust [asymptotic stability](@entry_id:149743).

### A Mathematical Toolkit for Handling Uncertainty Sets

To formalize these objectives, we must work with sets of possible states and disturbances. Convex analysis provides a powerful toolkit for this purpose.

#### Set Operations: Minkowski Sum and Pontryagin Difference

Two [set operations](@entry_id:143311) are indispensable in robust control: the Minkowski sum and the Pontryagin difference.

The **Minkowski sum** of two sets $\mathcal{C}, \mathcal{D} \subset \mathbb{R}^n$, denoted $\mathcal{C} \oplus \mathcal{D}$, is the set of all possible vector sums of their elements:
$$
\mathcal{C} \oplus \mathcal{D} = \{ c + d \mid c \in \mathcal{C}, d \in \mathcal{D} \}
$$
This operation is fundamental for propagating uncertainty. For instance, consider the error dynamics $e_{k+1} = A e_k + w_k$, where the error $e_k$ is known to lie in a set $\mathcal{E}_k$ and the disturbance $w_k$ lies in $\mathcal{W}$. The set of all possible next errors, $\mathcal{E}_{k+1}$, is the Minkowski sum of the propagated error set and the disturbance set: $\mathcal{E}_{k+1} = A\mathcal{E}_k \oplus \mathcal{W}$ [@problem_id:2741208].

The **Pontryagin difference** (or Minkowski difference) of two sets $\mathcal{X}, \mathcal{S} \subset \mathbb{R}^n$, denoted $\mathcal{X} \ominus \mathcal{S}$, is defined as:
$$
\mathcal{X} \ominus \mathcal{S} = \{ x \in \mathbb{R}^n \mid x + s \in \mathcal{X} \text{ for all } s \in \mathcal{S} \} = \{ x \in \mathbb{R}^n \mid \{x\} \oplus \mathcal{S} \subseteq \mathcal{X} \}
$$
The Pontryagin difference is the cornerstone of **[constraint tightening](@entry_id:174986)**. Suppose the true state is $x_k = \hat{x}_k + e_k$, where $\hat{x}_k$ is a nominal state we can control and $e_k$ is an error residing in a set $\mathcal{E}$. To guarantee that the true state satisfies the constraint $x_k \in \mathcal{X}$, we must enforce a stricter, or tightened, constraint on the nominal state: $\hat{x}_k \in \mathcal{X} \ominus \mathcal{E}$. This ensures that no matter which error $e_k \in \mathcal{E}$ occurs, the sum $\hat{x}_k + e_k$ will remain within $\mathcal{X}$ [@problem_id:2741173].

#### The Support Function

While [set operations](@entry_id:143311) are conceptually clear, their explicit computation can be complex. The **[support function](@entry_id:755667)** of a [compact convex set](@entry_id:272594) $\mathcal{C} \subset \mathbb{R}^n$ provides an alternative, often more tractable, representation. It is defined as:
$$
h_{\mathcal{C}}(s) = \sup_{x \in \mathcal{C}} s^{\top} x
$$
The [support function](@entry_id:755667) gives the maximum projection of the set $\mathcal{C}$ onto the direction of vector $s$. It has several useful properties [@problem_id:2741208]:
-   **Summation**: $h_{\mathcal{C} \oplus \mathcal{D}}(s) = h_{\mathcal{C}}(s) + h_{\mathcal{D}}(s)$
-   **Linear Transformation**: $h_{M\mathcal{C}}(s) = h_{\mathcal{C}}(M^{\top}s)$ for a matrix $M$.

The [support function](@entry_id:755667) is particularly useful for [constraint tightening](@entry_id:174986). To robustly enforce a linear constraint $F x \le g$, where $x = \hat{x} + e$ and $e \in \mathcal{E}$, we require $F(\hat{x}+e) \le g$ for all $e \in \mathcal{E}$. Let $F_i$ be the $i$-th row of $F$. The constraint for this row is $F_i \hat{x} + F_i e \le g_i$. This must hold for all $e \in \mathcal{E}$, which means we must satisfy:
$$
F_i \hat{x} \le g_i - \sup_{e \in \mathcal{E}} (F_i e) = g_i - h_{\mathcal{E}}(F_i^{\top})
$$
This shows that the amount of tightening required for each linear constraint can be calculated directly using the [support function](@entry_id:755667) of the error set [@problem_id:2741208].

#### Invariant Sets

The concept of invariance is central to guaranteeing properties over an infinite horizon.
-   A set $\mathcal{S}$ is **Positively Invariant (PI)** for a nominal system $e_{k+1} = f(e_k)$ if, for any state $e \in \mathcal{S}$, the next state $f(e)$ is also in $\mathcal{S}$. In [set notation](@entry_id:276971): $f(\mathcal{S}) \subseteq \mathcal{S}$ [@problem_id:2741213].
-   A set $\mathcal{S}$ is **Robustly Positive Invariant (RPI)** for a disturbed system $e_{k+1} = f(e_k, w_k)$ with $w_k \in \mathcal{W}$ if, for any state $e \in \mathcal{S}$ and *any* disturbance $w \in \mathcal{W}$, the next state $f(e, w)$ is also in $\mathcal{S}$. In [set notation](@entry_id:276971), this is equivalent to requiring the set of all possible next states to be contained within $\mathcal{S}$: $f(\mathcal{S}, \mathcal{W}) \subseteq \mathcal{S}$. For [linear dynamics](@entry_id:177848) $e_{k+1} = A_{cl}e_k + w_k$, this becomes $(A_{cl}\mathcal{S}) \oplus \mathcal{W} \subseteq \mathcal{S}$ [@problem_id:2741213].

RPI sets are the key to containing the effects of persistent disturbances. If we can design a controller that keeps the system's error within an RPI set, we can then use that set to compute fixed constraint tightenings that are valid for all time.

### A Premier Strategy: Tube-Based Model Predictive Control

Tube-based MPC is a computationally efficient and widely used RMPC strategy for systems with additive disturbances. It elegantly decouples the problem of robustness from the problem of optimal planning.

#### The Core Mechanism: State and Dynamics Decomposition

The central idea is to decompose the actual state $x_k$ into a nominal part $\bar{x}_k$ and an error part $e_k = x_k - \bar{x}_k$. The control input is similarly decomposed: a nominal input $\bar{u}_k$ is augmented with an **ancillary feedback controller** $K e_k$, yielding the total input $u_k = \bar{u}_k + K e_k$ [@problem_id:2741077]. The feedback gain $K$ is typically pre-designed offline such that the closed-loop matrix $A+BK$ is stable (Schur).

By substituting these decompositions into the system dynamics $x_{k+1} = Ax_k + Bu_k + w_k$, we can separate the evolution of the system into two parts [@problem_id:2741246]:
1.  **Nominal Dynamics**: $\bar{x}_{k+1} = A\bar{x}_k + B\bar{u}_k$. This is a predictable, disturbance-free model that the MPC controller will use for planning.
2.  **Error Dynamics**: $e_{k+1} = (A+BK)e_k + w_k$. This equation governs the deviation from the nominal path and is driven by the system disturbance $w_k$.

The ancillary controller $K$ is designed to stabilize the error dynamics. Because $A+BK$ is stable and the disturbance $w_k$ is bounded, the error $e_k$ will remain within a bounded RPI set, which we will call $\mathcal{E}$. This set $\mathcal{E}$ forms a "tube" around the nominal trajectory, within which the actual state is guaranteed to lie.

#### The Tube-RMPC Algorithm

The [online algorithm](@entry_id:264159) involves solving a standard nominal MPC problem, but with constraints tightened to account for the error tube.

1.  **Offline**:
    -   Design a stabilizing feedback gain $K$ such that $A+BK$ is Schur.
    -   Compute a suitable RPI set $\mathcal{E}$ for the error dynamics $e_{k+1} = (A+BK)e_k + w_k$. For example, if $\mathcal{W}$ is an $\ell_\infty$-ball of radius $\delta_w$, one can often find an RPI set $\mathcal{E}$ that is also an $\ell_\infty$-ball of radius $\varepsilon$. The minimal such radius can be found by solving $\varepsilon = \lVert A+BK \rVert_\infty \varepsilon + \delta_w$, which gives $\varepsilon = \delta_w / (1 - \lVert A+BK \rVert_\infty)$ [@problem_id:2741246].
    -   Compute the tightened constraint sets $\bar{\mathcal{X}} = \mathcal{X} \ominus \mathcal{E}$ and $\bar{\mathcal{U}} = \mathcal{U} \ominus K\mathcal{E}$.

2.  **Online (at each time $k$)**:
    -   Measure the current state $x_k$.
    -   Find an initial nominal state $\bar{x}_{0|k}$ such that $x_k - \bar{x}_{0|k} \in \mathcal{E}$.
    -   Solve the finite-horizon optimal control problem for the nominal system using the tightened constraints:
        $$
        \min_{\{\bar{u}_{i|k}\}} \sum_{i=0}^{N-1} \ell(\bar{x}_{i|k}, \bar{u}_{i|k}) + V_f(\bar{x}_{N|k})
        $$
        subject to:
        - $\bar{x}_{i+1|k} = A \bar{x}_{i|k} + B \bar{u}_{i|k}$
        - $\bar{x}_{i|k} \in \bar{\mathcal{X}}$, $\bar{u}_{i|k} \in \bar{\mathcal{U}}$
        - $\bar{x}_{N|k} \in \bar{\mathcal{X}}_f$ (a suitable [terminal set](@entry_id:163892) within $\bar{\mathcal{X}}$)
    -   Let the optimal nominal sequence be $\{\bar{u}_{i|k}^{\star}\}$.
    -   Apply the control input $u_k = \bar{u}_{0|k}^{\star} + K(x_k - \bar{x}_{0|k})$ to the plant.

This separation of concerns makes tube-based RMPC computationally attractive: the [online optimization](@entry_id:636729) is a standard nominal MPC problem (often a QP), which is much simpler than solving a full min-max problem. The robustness is handled by the offline design of $K$ and the [constraint tightening](@entry_id:174986). Recursive feasibility is proven by constructing a candidate solution at the next time step, which involves shifting the previous optimal nominal plan and appending a move dictated by a terminal controller, a standard technique in MPC proofs [@problem_id:2741149].

#### Example: Calculating Tightened Constraints

Consider a system with $A=0.2I_2$ and a disturbance set $\mathcal{W}$ being an $\ell_\infty$-box with radius $0.5$. The error dynamics are $e_{k+1} = 0.2e_k + w_k$. The minimal RPI set $\mathcal{E}$ for these dynamics is the infinite Minkowski sum $\bigoplus_{i=0}^\infty (0.2)^i \mathcal{W}$. Since all sets are $\ell_\infty$-boxes, the radius of $\mathcal{E}$ is the sum of the radii of the component sets: $0.5 \sum_{i=0}^\infty (0.2)^i = 0.5 \times \frac{1}{1-0.2} = 0.625$. If the original state constraint set is $\mathcal{X} = \{x : \lVert x \rVert_\infty \le 5\}$, the tightened constraint on the nominal state is $\hat{x}_k \in \mathcal{X} \ominus \mathcal{E}$, which becomes $\lVert \hat{x}_k \rVert_\infty \le 5 - 0.625 = 4.375$ [@problem_id:2741173].

### An Alternative Philosophy: Min-Max MPC

Instead of decoupling the problem, min-max RMPC directly confronts the adversarial nature of the disturbance. The goal is to find a control sequence that minimizes the cost function under the worst-possible disturbance sequence.

The optimization problem at each step takes the form of a game against nature [@problem_id:2746618]:
$$
\min_{u_{0:N-1}} \left( \max_{w_{0:N-1} \in \mathcal{W}^N} \left[ \sum_{i=0}^{N-1} \ell(x_i, u_i) + V_f(x_N) \right] \right)
$$
subject to the constraints being satisfied for *all* disturbance sequences $w_{0:N-1} \in \mathcal{W}^N$. The decision variable is an open-loop sequence of inputs $u_{0:N-1}$. This formulation is conceptually powerful and can be less conservative than tube-based methods, as it does not rely on a single, fixed ancillary gain. However, solving this min-max problem is computationally formidable. In general, it is a semi-infinite program that is often intractable for real-time implementation. Stability proofs for min-max MPC rely on showing that the optimal value function is an ISS-Lyapunov function for the closed-loop system, which typically requires a robust control invariant [terminal set](@entry_id:163892) and an associated robust control Lyapunov function as the terminal cost [@problem_id:2746618], [@problem_id:2741150].

### A Spectrum of RMPC Methods

Tube-based and min-max RMPC represent two ends of a spectrum trading off conservatism and [computational complexity](@entry_id:147058). Several other methods exist in between [@problem_id:2741076]:
-   **Affine Disturbance Feedback**: Here, the control policy is optimized over a class of affine functions of past disturbances, $u_k = v_k + \sum_{i=0}^{k-1} L_{k,i} w_i$. This is more flexible than the fixed-gain feedback in tube MPC but leads to a convex (though larger) optimization problem, which is still tractable.
-   **Multi-Stage (Scenario) RMPC**: This approach discretizes the disturbance set and builds a scenario tree of possible future state trajectories. The controller optimizes a policy that adapts to the specific branch of the tree that is realized. This "wait and see" approach can significantly reduce conservatism but at the [cost of complexity](@entry_id:182183) that grows exponentially with the [prediction horizon](@entry_id:261473).

### A Probabilistic Alternative: Stochastic MPC

All the methods discussed so far provide hard, worst-case guarantees. An alternative is to adopt a probabilistic framework, which can be significantly less conservative. **Stochastic MPC (SMPC)** aims to satisfy constraints with a high probability, rather than with certainty. This is formalized using **[chance constraints](@entry_id:166268)** [@problem_id:2741106]:
$$
\mathbb{P}(Hx_k \le h) \ge 1 - \alpha
$$
Here, $\alpha \in (0,1)$ is a small, user-defined risk level (e.g., $0.01$). Instead of guaranteeing that the constraint is never violated, we accept a $1\%$ chance of violation. For systems with known stochastic disturbance distributions (e.g., Gaussian noise, $w \sim \mathcal{N}(0, \Sigma)$), such [chance constraints](@entry_id:166268) can often be reformulated as deterministic, convex constraints.

For a scalar constraint $y = \mu + g^{\top}w \le y_{max}$, where $w \sim \mathcal{N}(0, \Sigma)$, the variable $y$ is also Gaussian, $y \sim \mathcal{N}(\mu, g^{\top}\Sigma g)$. The chance constraint $\mathbb{P}(y \le y_{max}) \ge 1-\alpha$ can then be converted to the deterministic [second-order cone](@entry_id:637114) constraint [@problem_id:2741106]:
$$
\mu + \Phi^{-1}(1-\alpha) \sqrt{g^{\top}\Sigma g} \le y_{max}
$$
where $\Phi^{-1}$ is the inverse CDF of the standard normal distribution. Comparing this to the [robust counterpart](@entry_id:637308) for an $\ell_\infty$-bounded disturbance, $\mu + \bar{w}\lVert g \rVert_1 \le y_{max}$, we see a fundamentally different structure in the safety margin. The probabilistic approach often yields a much smaller margin, allowing for better performance at the cost of accepting a small, quantifiable risk of [constraint violation](@entry_id:747776).

The choice between worst-case robust MPC and stochastic MPC depends heavily on the application: for safety-critical systems where [constraint violation](@entry_id:747776) is catastrophic, robust methods are paramount. For performance-driven systems where occasional, small violations are tolerable, stochastic methods offer a compelling alternative.