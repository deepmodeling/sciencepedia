## Introduction
Model Predictive Control (MPC) has become a cornerstone of modern control theory, but the increasing complexity and economic imperatives of today's systems demand more advanced strategies. Standard MPC often focuses on regulation to a fixed setpoint, falling short when the true goal is optimizing dynamic economic performance or managing large-scale, interconnected networks. This is the gap filled by Economic MPC (eMPC) and Distributed MPC (dMPC), which shift the paradigm from simple stabilization to sophisticated, [real-time optimization](@entry_id:169327) and coordination.

This article provides a comprehensive exploration of these advanced control frameworks. We will first dissect the core **Principles and Mechanisms**, establishing the theoretical foundations of eMPC and dMPC, from stability analysis to distributed coordination algorithms. Next, we will explore their impact through a wide range of **Applications and Interdisciplinary Connections**, demonstrating their utility in fields from energy systems to [systems biology](@entry_id:148549). Finally, you will have the opportunity to apply these concepts through a series of **Hands-On Practices** designed to solidify your understanding.

## Principles and Mechanisms

Following the introduction to the motivations and applications of advanced [model predictive control](@entry_id:146965), this chapter delves into the core principles and mechanisms that govern its behavior and enable its application to complex, [large-scale systems](@entry_id:166848). We begin by revisiting the foundational structure of Model Predictive Control (MPC) before extending it to economic objectives. We then explore the theoretical underpinnings that guarantee stability and desirable performance, namely the use of terminal ingredients and the concept of [dissipativity](@entry_id:162959). Finally, we transition from centralized to [distributed control](@entry_id:167172) architectures, examining the key mechanisms of coordination that make the control of large-scale networked systems tractable and efficient.

### The Foundation: Receding Horizon Control

The operational backbone of Model Predictive Control is the **[receding horizon](@entry_id:181425)** policy. This strategy leverages a system model to make optimal decisions by repeatedly solving a finite-horizon [optimal control](@entry_id:138479) problem (FHOCP) at each sampling instant. For a discrete-time system, this process is a constant cycle of measurement, optimization, and actuation.

Consider a system with state $x_k \in \mathbb{R}^n$ and input $u_k \in \mathbb{R}^m$, governed by the dynamics $x_{k+1} = f(x_k, u_k)$, and subject to constraints $x_k \in \mathcal{X}$ and $u_k \in \mathcal{U}$. At a given time $k$, the MPC controller performs the following steps:

1.  **State Measurement:** The current state of the system, $x_k$, is measured or estimated.

2.  **Optimal Control Problem:** An open-loop [optimal control](@entry_id:138479) problem is solved over a finite [prediction horizon](@entry_id:261473) of $N$ steps. This involves finding a sequence of future inputs $\mathbf{u}_k = \{ u_{k|k}, u_{k+1|k}, \dots, u_{k+N-1|k} \}$ and the corresponding state trajectory $\mathbf{x}_k = \{ x_{k|k}, x_{k+1|k}, \dots, x_{k+N|k} \}$ that minimizes a [cost function](@entry_id:138681). A standard formulation for a linear system $x_{k+1} = Ax_k + Bu_k$ is as follows [@problem_id:2701661]:
    $$
    \begin{aligned}
    \min_{\mathbf{u}_k, \mathbf{x}_k}  \quad \sum_{i=0}^{N-1} \ell(x_{k+i|k}, u_{k+i|k}) + V_f(x_{k+N|k}) \\
    \text{subject to}  \quad x_{k|k} = x_k, \\
     \quad x_{k+i+1|k} = A x_{k+i|k} + B u_{k+i|k},  \forall i \in \{0, \dots, N-1\}, \\
     \quad x_{k+i|k} \in \mathcal{X},  \forall i \in \{0, \dots, N\}, \\
     \quad u_{k+i|k} \in \mathcal{U},  \forall i \in \{0, \dots, N-1\}.
    \end{aligned}
    $$
    Here, $\ell(\cdot, \cdot)$ is the **stage cost**, which penalizes undesirable states and inputs at each step, and $V_f(\cdot)$ is the **terminal cost**, which approximates the cost-to-go beyond the horizon. The notation $z_{k+i|k}$ denotes the predicted value of a variable $z$ at time $k+i$, based on the state measurement at time $k$.

3.  **Actuation:** Although an entire sequence of optimal inputs is computed, only the *first* element of this sequence, $u_{k|k}^\star$, is applied to the plant. The rest of the sequence is discarded.

4.  **Horizon Shift:** At the next time step, $k+1$, the horizon recedes, and the entire process is repeated from Step 1 with the new state measurement $x_{k+1}$.

This [receding horizon](@entry_id:181425) implementation is what closes the feedback loop in MPC. By re-optimizing at every step based on the latest state measurement, the controller can compensate for disturbances and [model-plant mismatch](@entry_id:263118), a feature that an open-loop strategy (applying the entire sequence $\mathbf{u}_k^\star$) would lack.

### Economic MPC: Optimizing System Performance

Standard MPC is often designed for regulation or tracking, where the stage cost $\ell(x,u)$ is a [positive definite function](@entry_id:172484) that penalizes deviations from a desired setpoint $(x_r, u_r)$, for example, $\ell(x,u) = \|x-x_r\|_Q^2 + \|u-u_r\|_R^2$. The control objective is to stabilize the system at this predetermined reference.

**Economic Model Predictive Control (eMPC)** generalizes this framework by replacing the tracking cost with a stage cost $\ell(x,u)$ that represents a direct measure of system performance, such as operating cost, profit, or energy consumption [@problem_id:2701652]. Crucially, this economic stage cost is not required to be positive definite with respect to any particular setpoint. The primary goal of eMPC is not to track a pre-specified reference, but to operate the system in a way that optimizes its economic performance over time. The optimal mode of operation—be it a steady state or a dynamic pattern—is not an input to the controller but an emergent property of the optimization.

#### Optimal Behavior: From Fixed Points to Periodic Orbits

The shift from a tracking objective to an economic one can lead to fundamentally different and often superior closed-loop behavior. Consider an inventory management system where the goal is to satisfy a constant demand $d$ [@problem_id:2701689].

A **tracking MPC** might be designed to keep the inventory level $x_k$ at a reference target $x_r=0.5$, penalizing deviations with a cost like $(x_k - 0.5)^2 + \rho u_k^2$. The controller will naturally steer the system to the steady state where the inventory is held at $0.5$ and the input (production) exactly matches the demand, $u_k=d$. The attractor is a fixed point determined by the tracking objective.

An **eMPC**, in contrast, might be tasked with minimizing the purchasing cost $\ell_k(u_k) = p_k u_k$, where the unit price $p_k$ is known to be periodic—for example, low on even days ($p_{2m}=0$) and high on odd days ($p_{2m+1}=1$). A steady-state policy of buying $u_k = d$ every day would incur a certain average cost. However, the eMPC will discover a more intelligent, periodic strategy: buy more than the demand when the price is low, and buy less (or nothing) when the price is high, using the stored inventory to satisfy demand on expensive days. This behavior results in the system converging not to a steady state, but to a **2-[periodic orbit](@entry_id:273755)** in its state and input. This periodic operation achieves a strictly lower average cost than any steady-state policy.

This example illustrates a central tenet of eMPC: the economically optimal mode of operation may not be a fixed point. The closed-loop system should converge to an **economically optimal [invariant set](@entry_id:276733)**, which could be a steady state, a periodic orbit, or even a more complex dynamic pattern, depending on the [system dynamics](@entry_id:136288) and the economic objective.

#### The Turnpike Property

The tendency of eMPC systems to operate near an optimal steady state is formalized by the **turnpike property** [@problem_id:2701670]. This principle, central to [optimal control](@entry_id:138479) theory, posits that for a sufficiently long horizon, the optimal trajectory for an economic problem will consist of three phases: a transient from the initial state to a neighborhood of the optimal steady state, a long period spent near this steady state (the "turnpike"), and a final transient to the terminal state.

Intuitively, the optimal steady state $(x^s, u^s)$ is the most economical mode of operation. Any deviation from it incurs an instantaneous performance loss. To minimize the total cost over a long horizon, the most efficient strategy is to rapidly move to this turnpike, exploit its economic benefits for as long as possible, and only exit near the end of the horizon to satisfy terminal conditions. This property implies that for long-horizon problems, the bulk of the trajectory is largely independent of the initial and terminal conditions, being dominated by the system's intrinsic economic optimum.

### Mechanisms for Stability and Feasibility

A key challenge in MPC is ensuring that the optimization problem remains feasible at every time step (**[recursive feasibility](@entry_id:167169)**) and that the resulting closed-loop system is stable. The finite horizon can make the controller "myopic," potentially leading it to a state from which constraints cannot be satisfied in the future. For eMPC, the challenge is compounded because the stage cost does not necessarily decrease as the state approaches a desirable equilibrium, and thus cannot act as a Lyapunov function.

#### Terminal Ingredients for Stability

A standard mechanism to enforce stability is the use of **terminal ingredients**: a terminal cost function $V_f(x)$ and a [terminal constraint](@entry_id:176488) set $\mathcal{X}_f$ [@problem_id:2701657]. These are designed to guarantee that if the state enters the [terminal set](@entry_id:163892) $\mathcal{X}_f$, it can be kept there indefinitely while satisfying all constraints.

The design of these ingredients is often linked to the infinite-horizon Linear Quadratic Regulator (LQR) problem associated with the system's dynamics. For a linear system with quadratic costs, the design process is as follows:

1.  **Terminal Cost Design:** The terminal cost $V_f(x) = x^\top P x$ is chosen as the value function of the unconstrained infinite-horizon LQR problem. The matrix $P$ is the unique [positive definite](@entry_id:149459) solution to the **Discrete Algebraic Riccati Equation (DARE)**, which arises from the Bellman equation for the infinite-[horizon problem](@entry_id:161031).

2.  **Terminal Controller:** The LQR problem also yields an optimal linear state-[feedback gain](@entry_id:271155) $K$ that stabilizes the unconstrained system. This gain defines the **terminal controller** $u = Kx$.

3.  **Terminal Set Design:** The [terminal set](@entry_id:163892) $\mathcal{X}_f = \{x \in \mathbb{R}^n \mid x^\top P x \le \alpha\}$ is an ellipsoid defined using the matrix $P$. It must be designed to satisfy two crucial properties:
    *   **Positive Invariance:** If the state $x_k$ is in $\mathcal{X}_f$, the subsequent state $x_{k+1}$ under the terminal controller $u_k=Kx_k$ must also lie within $\mathcal{X}_f$. The Lyapunov stability of the LQR controller ensures this.
    *   **Constraint Adherence:** For every state $x$ within the [terminal set](@entry_id:163892) $\mathcal{X}_f$, the corresponding input $u=Kx$ from the terminal controller must satisfy the system's input constraints, i.e., $Kx \in \mathcal{U}$. This condition determines the maximum allowable size of the [terminal set](@entry_id:163892), specified by the parameter $\alpha$.

By including these terminal ingredients in the FHOCP, one can prove [recursive feasibility](@entry_id:167169) and [asymptotic stability](@entry_id:149743) of the MPC-controlled system.

#### Dissipativity and Stability of eMPC

For eMPC, where the stage cost $\ell(x,u)$ may not be [positive definite](@entry_id:149459), a more advanced tool is needed to establish stability: the theory of **[dissipativity](@entry_id:162959)** [@problem_id:2701669]. A system is said to be dissipative if the change in some stored internal "energy," represented by a **storage function** $S(x)$, is less than or equal to an external "supply rate" $s(x,u)$.

For analyzing eMPC stability, we are interested in **strict [dissipativity](@entry_id:162959)** with respect to the optimal steady state $(x^\star, u^\star)$. This property is defined by the inequality:
$$
S(f(x,u)) - S(x) \le \ell(x,u) - \ell(x^\star, u^\star) - \rho(\|(x,u)-(x^\star, u^\star)\|)
$$
where $S(x)$ is a storage function and $\rho(\cdot)$ is a [positive definite function](@entry_id:172484). This inequality states that any deviation from the optimal steady state leads to a performance loss $\ell(x,u) - \ell(x^\star, u^\star)$ that is greater than the change in stored energy, with the excess loss bounded below by the distance to the steady state.

The power of this concept lies in its ability to construct a Lyapunov function for the eMPC system. By rearranging the inequality, one can define a **rotated stage cost**:
$$
\ell_r(x,u) := \ell(x,u) - \ell(x^\star, u^\star) + S(x) - S(f(x,u))
$$
The strict [dissipativity](@entry_id:162959) condition ensures that this rotated cost $\ell_r(x,u)$ is [positive definite](@entry_id:149459) with respect to $(x^\star, u^\star)$. The optimal [value function](@entry_id:144750) of the eMPC problem formulated with this rotated cost can then be shown to be a valid Lyapunov function for the closed-loop system, guaranteeing [asymptotic stability](@entry_id:149743) of the economically optimal steady state.

### Distributed MPC: Taming Complexity

For [large-scale systems](@entry_id:166848), such as power grids, chemical process networks, or multi-robot formations, a centralized MPC controller becomes impractical. The computational burden of solving a single, massive optimization problem is often prohibitive, and the communication requirement—that a central unit has real-time information about every part of the system—is a critical bottleneck. This motivates the development of [distributed control](@entry_id:167172) architectures.

#### System Representation and Control Architectures

A large-scale system is naturally viewed as a set of interconnected subsystems [@problem_id:2701665]. The influence of one subsystem's state on another's is termed **dynamic coupling**. These physical interconnections can be represented by a [directed graph](@entry_id:265535) $G = (\mathcal{V}, \mathcal{E})$, where the vertices $\mathcal{V}$ are the subsystems and a directed edge $(j, i) \in \mathcal{E}$ exists if the state of subsystem $j$ directly affects the dynamics of subsystem $i$. This physical graph is distinct from the communication graph that may be available to the controllers.

Based on the flow of information and decision-making authority, several architectures exist [@problem_id:2701637]:

*   **Decentralized Control:** Each local controller makes decisions based only on its own local information, with no communication with others. It must treat the effects of coupling as unknown disturbances, which can lead to conservative and suboptimal performance.
*   **Hierarchical Control:** A multi-layered structure where a high-level coordinator makes coarse decisions for the whole network (e.g., by setting targets or prices) and communicates these to low-level local controllers, which then solve their own detailed [optimization problems](@entry_id:142739).
*   **Distributed Control:** A "flat" architecture where local controllers engage in peer-to-peer communication and negotiation to coordinate their actions and collectively account for system-wide couplings, aiming to approximate the performance of a centralized controller.

#### Mechanism 1: Coordination via Iterative Negotiation

Many distributed MPC (dMPC) schemes can be understood as iterative algorithms for solving the large centralized optimization problem in a distributed manner [@problem_id:2701692]. If the centralized problem is a convex Quadratic Program (QP), as is common, local controllers can negotiate their planned actions through a series of best-response updates.

Two classical schemes for this are:
*   **Jacobi (Parallel) Iteration:** At each negotiation round, all controllers compute their optimal plan for the upcoming horizon, assuming the plans of their neighbors remain fixed at the values from the *previous* round. Since all controllers use the same "old" information from their neighbors, these computations can be performed in parallel.
*   **Gauss-Seidel (Sequential) Iteration:** Controllers update their plans in a fixed sequence. When its turn comes, a controller computes its [best response](@entry_id:272739) using the *most recently updated* plans from the neighbors that preceded it in the sequence. This uses newer information but imposes a sequential communication and computation structure.

The convergence of these negotiations to the true centralized optimum depends on the properties of the system coupling. For a strictly convex problem, the Gauss-Seidel scheme is generally guaranteed to converge. The Jacobi scheme, however, requires stronger conditions, such as the coupling between subsystems being sufficiently weak (a property known as block [diagonal dominance](@entry_id:143614) of the problem's Hessian matrix). A practical technique to enforce convergence in parallel schemes is **proximal regularization**, where each local objective is augmented with a term that penalizes large deviations from its previous plan, effectively damping the iterations.

#### Mechanism 2: Coordination via Pricing (Dual Decomposition)

When subsystems are coupled through shared constraints—for example, a limit on total power consumption or a shared raw material supply—a powerful coordination mechanism is **[dual decomposition](@entry_id:169794)**, which can be given an intuitive economic interpretation [@problem_id:2701681].

The core idea is to relax the coupling constraint by introducing a **Lagrange multiplier**, which can be interpreted as a **shadow price** for the shared resource. This price represents the marginal value of the resource; specifically, the sensitivity of the optimal total cost to a small change in the resource's availability.

This pricing mechanism enables a decomposition of the problem:
1.  **Decentralized Subproblems:** A central coordinator (or a [distributed consensus](@entry_id:748588) protocol) broadcasts the current price for the resource. Each local controller then solves its own MPC problem, where its local economic cost is augmented by the cost of using the shared resource, calculated as (price) $\times$ (amount consumed).
2.  **Price Updates:** After solving their subproblems, the local controllers report their planned resource consumption to the coordinator. The coordinator then updates the price based on the mismatch between total demand and available supply. If total demand exceeds supply, the price is increased to incentivize conservation. If supply exceeds demand, the price is lowered. This update is mathematically equivalent to performing gradient ascent on the [dual problem](@entry_id:177454).

This iterative process continues until the prices converge and the shared resource constraint is met. An intuitive result from this method is **[complementary slackness](@entry_id:141017)**: if at the optimum a resource is not fully utilized (i.e., the constraint is not active), its [shadow price](@entry_id:137037) will be zero. This price-based coordination fits naturally within a hierarchical control structure, where the upper layer's role is to set the market prices for the lower layers [@problem_id:2701637].