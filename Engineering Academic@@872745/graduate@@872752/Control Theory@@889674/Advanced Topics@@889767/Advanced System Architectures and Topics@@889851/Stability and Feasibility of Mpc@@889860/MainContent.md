## Introduction
Model Predictive Control (MPC) has emerged as a premier control strategy, renowned for its ability to handle complex, [multivariable systems](@entry_id:169616) subject to operational constraints. By optimizing a system's predicted behavior over a finite horizon, MPC can achieve high performance in a vast range of applications. However, this predictive power introduces a fundamental challenge: without a rigorous design, the controller may lead the system to a state where no feasible solution exists, or it may fail to stabilize the system at its desired objective. The gap between a naive implementation and a provably reliable controller lies in addressing the twin pillars of [recursive feasibility](@entry_id:167169) and [asymptotic stability](@entry_id:149743).

This article provides a graduate-level exposition of the theoretical framework designed to guarantee the safe and stable operation of MPC. We will dissect the elegant mechanisms that form the bedrock of modern MPC design, ensuring controllers are not just optimal for a short-term prediction, but are guaranteed to perform correctly indefinitely.

Across the following sections, you will gain a deep understanding of these concepts. First, **"Principles and Mechanisms"** will lay the theoretical foundation, introducing terminal sets, terminal costs, and Control Lyapunov Functions as the primary tools for ensuring [recursive feasibility](@entry_id:167169) and stability. Next, **"Applications and Interdisciplinary Connections"** will demonstrate the remarkable versatility of these principles, showing how they are extended to solve real-world problems involving disturbances, economic objectives, and large-scale networked systems. Finally, **"Hands-On Practices"** will provide the opportunity to apply this theory, solidifying your understanding by working through concrete design and analysis problems.

## Principles and Mechanisms

Following the introduction to the fundamental concept of Model Predictive Control (MPC), this section delves into the theoretical underpinnings that guarantee its successful operation. The central challenges in MPC are ensuring that the controller can continue to operate at all future times (**[recursive feasibility](@entry_id:167169)**) and that it guides the system to its desired objective, typically the origin (**[asymptotic stability](@entry_id:149743)**). We will dissect the principles and mechanisms—namely terminal sets, terminal costs, and control Lyapunov functions—that have been developed to rigorously address these challenges.

### The Finite-Horizon Optimal Control Problem in MPC

At each time step $k$, the MPC controller solves a finite-horizon [optimal control](@entry_id:138479) problem based on the current state measurement $x_k$. For a system with dynamics $x_{k+1} = f(x_k, u_k)$, a stage cost $\ell(x,u)$, a terminal cost $V_f(x)$, and constraints on states ($x \in \mathcal{X}$), inputs ($u \in \mathcal{U}$), and the terminal state ($x_N \in \mathcal{X}_f$), this problem can be formally stated.

Let the [prediction horizon](@entry_id:261473) be $N$. Given the initial state $x_k$, the controller seeks an optimal input sequence $\mathbf{u} = \{u_0, \dots, u_{N-1}\}$ that minimizes a total cost function. The states along the [prediction horizon](@entry_id:261473), $\{x_0, \dots, x_N\}$, are generated recursively from the initial state $x_0 = x_k$ and the input sequence. The optimization problem is [@problem_id:2746588]:
$$
V_N(x_k) := \min_{u_0, \dots, u_{N-1}} \quad \sum_{i=0}^{N-1} \ell(x_i, u_i) + V_f(x_N)
$$
subject to:
$$
\begin{align*}
x_{i+1} = f(x_i, u_i), \quad x_0 = x_k \\
x_i \in \mathcal{X} \quad \text{for } i \in \{0, \dots, N\} \\
u_i \in \mathcal{U} \quad \text{for } i \in \{0, \dots, N-1\} \\
x_N \in \mathcal{X}_f
\end{align*}
$$

The function $V_N(x)$ is the **value function**, representing the minimum achievable cost starting from state $x$. If no input sequence can satisfy all the constraints, the problem is infeasible, and by convention, $V_N(x) = +\infty$. Assuming a strictly convex cost and convex constraints, the optimal input sequence $\mathbf{u}^\star(x_k) = \{u_0^\star, \dots, u_{N-1}^\star\}$ is unique if it exists.

The MPC controller implements a **[receding horizon](@entry_id:181425)** strategy. It solves for the entire optimal sequence $\mathbf{u}^\star(x_k)$, but applies only the *first* element, $u_k = u_0^\star$, to the system. At the next time step, $k+1$, the system state is measured again, and the entire optimization is solved anew for the new state $x_{k+1}$. The resulting [closed-loop control](@entry_id:271649) law is therefore an implicit state-feedback law, $\kappa_N(x_k) := u_0^\star(x_k)$ [@problem_id:2746588].

### The Twin Pillars: Recursive Feasibility and Stability

This [receding horizon](@entry_id:181425) strategy presents two fundamental challenges that must be addressed for the controller to be viable.

1.  **Feasibility**: At any given time $k$, the MPC problem is **feasible** if there exists at least one control sequence that satisfies all constraints. The set of all initial states for which the problem is feasible is called the **[domain of attraction](@entry_id:174948)** or feasible set for the horizon $N$.

2.  **Recursive Feasibility**: This is a stronger, crucial property. **Recursive feasibility** means that if the MPC problem is feasible at time $k$, then after applying the control $u_k = \kappa_N(x_k)$, the problem is guaranteed to be feasible again at time $k+1$ for the resulting state $x_{k+1}$ [@problem_id:2746593]. Without this guarantee, the controller might operate successfully for a few steps, only to drive the system to a state where the optimization problem becomes infeasible. At that point, the controller fails, as it cannot find a valid control input.

Beyond mere feasibility, the ultimate goal is typically stabilization. **Asymptotic stability** of the origin means that for any initial state within the [domain of attraction](@entry_id:174948), the closed-loop system trajectory not only remains feasible for all time but also converges to the origin, i.e., $\lim_{k \to \infty} x_k = 0$.

The remainder of this section is devoted to the elegant theoretical framework developed to ensure both [recursive feasibility](@entry_id:167169) and [asymptotic stability](@entry_id:149743).

### Guaranteeing Recursive Feasibility via Invariant Terminal Sets

The key to guaranteeing [recursive feasibility](@entry_id:167169) lies in the intelligent design of the terminal components of the MPC problem: the [terminal set](@entry_id:163892) $\mathcal{X}_f$ and an associated terminal control law $\kappa_f(x)$. The core idea is to ensure that the predicted state at the end of the horizon, $x_N$, lands in a "safe" region $\mathcal{X}_f$ from which feasibility can be perpetuated indefinitely. This safety is formalized through the concept of set invariance.

A set $\mathcal{S}$ is said to be **positively invariant** for a closed-loop system $x^+ = f(x, \kappa(x))$ if, for any state $x \in \mathcal{S}$, the next state $x^+$ is also in $\mathcal{S}$ [@problem_id:2746570]. A more general concept is **control invariance**: a set $\mathcal{S}$ is control invariant if for every $x \in \mathcal{S}$, there *exists* an admissible control $u \in \mathcal{U}$ such that $f(x, u) \in \mathcal{S}$. Positive invariance under a specific feedback law $\kappa$ is a special case of control invariance.

The standard method to prove [recursive feasibility](@entry_id:167169) is the **"shift-and-append" argument** [@problem_id:2746593]. Suppose at time $k$, we find an optimal feasible sequence $\mathbf{u}^\star_k = \{u^\star_{0|k}, \dots, u^\star_{N-1|k}\}$ and state sequence $\mathbf{x}^\star_k = \{x^\star_{0|k}, \dots, x^\star_{N|k}\}$, where $x^\star_{0|k}=x_k$. We apply $u_k = u^\star_{0|k}$, and the system moves to $x_{k+1} = x^\star_{1|k}$.

Now, at time $k+1$, we need to show that the MPC problem is still feasible. We do this by constructing a candidate (suboptimal but feasible) control sequence:
1.  **Shift**: Take the tail of the previous optimal sequence: $\{u^\star_{1|k}, \dots, u^\star_{N-1|k}\}$. This sequence is feasible for the state trajectory segment $\{x^\star_{1|k}, \dots, x^\star_{N|k}\}$.
2.  **Append**: At the end of this sequence, the state is $x^\star_{N|k}$, which is in the [terminal set](@entry_id:163892) $\mathcal{X}_f$. We now append one final control input using a predefined **terminal controller** $\kappa_f(x)$ designed to keep the state within $\mathcal{X}_f$. The new final input is $u^c_{N-1|k+1} = \kappa_f(x^\star_{N|k})$.

The candidate control sequence at time $k+1$ is $\mathbf{u}^c_{k+1} = \{u^\star_{1|k}, \dots, u^\star_{N-1|k}, \kappa_f(x^\star_{N|k})\}$. For this sequence to be feasible, two conditions on the [terminal set](@entry_id:163892) $\mathcal{X}_f$ and controller $\kappa_f$ are required for all $x \in \mathcal{X}_f$:
- The terminal control law must be admissible: $\kappa_f(x) \in \mathcal{U}$.
- The [terminal set](@entry_id:163892) must be positively invariant under this law: $f(x, \kappa_f(x)) \in \mathcal{X}_f$.

If these conditions hold, our candidate sequence is guaranteed to be feasible at time $k+1$. The existence of at least one [feasible solution](@entry_id:634783) proves that the problem is feasible. Thus, a positively invariant [terminal set](@entry_id:163892) provides the crucial guarantee of [recursive feasibility](@entry_id:167169).

For systems with disturbances $w \in \mathcal{W}$, this concept is extended to **robust positive invariance**: for all $x \in \mathcal{X}_f$ and for all possible disturbances $w \in \mathcal{W}$, the next state $f(x, \kappa_f(x)) + w$ must remain in $\mathcal{X}_f$ [@problem_id:2746570].

### Characterizing the Domain of Attraction: Backward Reachable Sets

The choice of horizon $N$ and the [terminal set](@entry_id:163892) $\mathcal{X}_f$ directly determines the MPC controller's [domain of attraction](@entry_id:174948)—the set of initial states from which a feasible trajectory can be found. This set can be formally characterized using the concept of **backward reachable sets**.

Let $\mathcal{X}_0$ be the [terminal set](@entry_id:163892). We can define the set of states that can be driven to $\mathcal{X}_0$ in one step as the predecessor set:
$$
\text{Pre}(\mathcal{S}) = \{x \in \mathbb{R}^n \mid \exists u \in \mathcal{U} \text{ such that } f(x,u) \in \mathcal{S}\}
$$
The $N$-step feasible set, denoted $\mathcal{X}_N$, is the set of all states in $\mathcal{X}$ that can be steered to the [terminal set](@entry_id:163892) $\mathcal{X}_0$ in $N$ steps while respecting all constraints. This set can be computed recursively [@problem_id:2746607]:
$$
\mathcal{X}_N = \mathcal{X} \cap \text{Pre}(\mathcal{X}_{N-1})
$$
If the [terminal set](@entry_id:163892) $\mathcal{X}_0$ is control invariant (i.e., $\mathcal{X}_0 \subseteq \text{Pre}(\mathcal{X}_0)$), then it follows by induction that the sequence of feasible sets is **nested**:
$$
\mathcal{X}_0 \subseteq \mathcal{X}_1 \subseteq \mathcal{X}_2 \subseteq \dots \subseteq \mathcal{X}_N
$$
This formally shows that increasing the [prediction horizon](@entry_id:261473) $N$ enlarges the [domain of attraction](@entry_id:174948) of the controller. The limit of this sequence, $\mathcal{X}_\infty = \bigcup_{N=0}^{\infty} \mathcal{X}_N$, is the **maximal controllable set**: the set of all states that can be steered to $\mathcal{X}_0$ in any finite number of steps.

This [recursive definition](@entry_id:265514) provides insight into the relationship between the horizon and feasibility [@problem_id:2746590]. If the problem is feasible from $x_k$ with horizon $N$, the next state $x_{k+1}$ is guaranteed to be in $\mathcal{X}_{N-1}$. This means [recursive feasibility](@entry_id:167169) is naturally preserved if the horizon is allowed to shrink. To maintain feasibility with a *constant* horizon $N$, we rely on the nesting property, $\mathcal{X}_{N-1} \subseteq \mathcal{X}_N$, which is guaranteed by the invariance of the [terminal set](@entry_id:163892) $\mathcal{X}_0$.

**Example: A Scalar System** [@problem_id:2746607]
Consider the scalar system $x_{k+1} = ax_k + u_k$ with constraints $|x| \le \bar{x}$ and $|u| \le \bar{u}$. Let the [terminal set](@entry_id:163892) be the origin, $\mathcal{X}_0 = \{0\}$. The feasible sets $\mathcal{X}_N$ will be symmetric intervals $[-r_N, r_N]$, with $r_0=0$. The [recurrence relation](@entry_id:141039) for the radius $r_N$ is:
$$
r_N = \min\left(\bar{x}, \frac{r_{N-1} + \bar{u}}{|a|}\right)
$$
The sequence $\{r_N\}$ is non-decreasing and bounded by $\bar{x}$, so it converges to a limit $r_\infty$. This limit must be a fixed point of the recurrence. For the specific parameters $a=1.5$, $\bar{x}=10$, and $\bar{u}=2$, the recurrence is $r_N = \min(10, (r_{N-1}+2)/1.5)$. The fixed point is found by solving $r_\infty = (r_\infty+2)/1.5$, which yields $r_\infty = 4$. This is consistent with the constraint $r_\infty \le 10$. The maximal controllable set to the origin is the interval $[-4, 4]$. Any initial state outside this interval cannot be stabilized by any MPC controller, regardless of horizon length.

### Proving Asymptotic Stability via Control Lyapunov Functions

Ensuring the controller can run forever ([recursive feasibility](@entry_id:167169)) is not enough; we need it to guide the system to the origin. This is achieved by designing the cost function such that the optimal [value function](@entry_id:144750) $V_N(x)$ acts as a **Lyapunov function** for the closed-loop system. A function $V(x)$ is a discrete-time Lyapunov function if it is positive definite ($V(0)=0, V(x)>0$ for $x \ne 0$) and strictly decreases along system trajectories ($V(x_{k+1})  V(x_k)$ for $x_k \ne 0$).

The key idea is to impose a condition on the terminal cost $V_f$ that forces the [value function](@entry_id:144750) $V_N(x)$ to decrease. This condition requires $V_f$ to be a **Control Lyapunov Function (CLF)** on the [terminal set](@entry_id:163892) $\mathcal{X}_f$ [@problem_id:2746605].

A function $V_f$ is a CLF on $\mathcal{X}_f$ with respect to the terminal controller $\kappa_f$ if it is positive definite and satisfies the following **decrease condition** for all $x \in \mathcal{X}_f$:
$$
V_f(f(x, \kappa_f(x))) - V_f(x) \le -\ell(x, \kappa_f(x))
$$
This condition states that within the [terminal set](@entry_id:163892), applying the terminal control law decreases the terminal cost by at least the value of the stage cost.

Let's see how this powerful condition leads to the stability of the entire MPC scheme. Recall the candidate solution $\mathbf{u}^c_{k+1}$ from the shift-and-append argument. The optimal cost at time $k+1$, $V_N(x_{k+1})$, must be less than or equal to the cost of this candidate solution. Following a careful derivation [@problem_id:2746594], we can establish a bound on the one-step change in the value function:

$V_N(x_{k+1}) \le J_N(\mathbf{u}^c_{k+1}) = \left( \sum_{i=1}^{N-1} \ell(x^\star_{i|k}, u^\star_{i|k}) \right) + \ell(x^\star_{N|k}, \kappa_f(x^\star_{N|k})) + V_f(f(x^\star_{N|k}, \kappa_f(x^\star_{N|k})))$

The optimal cost at time $k$ was $V_N(x_k) = \ell(x_k, u_k) + \sum_{i=1}^{N-1} \ell(x^\star_{i|k}, u^\star_{i|k}) + V_f(x^\star_{N|k})$. Subtracting $V_N(x_k)$ from the inequality for $V_N(x_{k+1})$ gives:
$$
V_N(x_{k+1}) - V_N(x_k) \le -\ell(x_k, u_k) + \left[ V_f(f(x^\star_{N|k}, \kappa_f(x^\star_{N|k}))) - V_f(x^\star_{N|k}) + \ell(x^\star_{N|k}, \kappa_f(x^\star_{N|k})) \right]
$$
The term in the square brackets is exactly the term from the CLF definition, which is guaranteed to be less than or equal to zero. This leads to the fundamental result:
$$
V_N(x_{k+1}) - V_N(x_k) \le -\ell(x_k, u_k)
$$
If the stage cost $\ell(x,u)$ is [positive definite](@entry_id:149459), this inequality proves that $V_N(x)$ is a strict Lyapunov function for the closed-loop system, ensuring [asymptotic stability](@entry_id:149743) of the origin.

### Synthesis: A Sufficient Condition for Asymptotic Stability

We can now assemble a complete set of [sufficient conditions](@entry_id:269617) for an MPC scheme (including nonlinear MPC, or NMPC) to be recursively feasible and render the origin asymptotically stable [@problem_id:2746599].

1.  **System and Problem Properties**: The system dynamics $f(x,u)$ should be continuous (and typically locally Lipschitz), with $f(0,0)=0$. The constraint sets $\mathcal{X}$ and $\mathcal{U}$ should be [compact sets](@entry_id:147575) containing the origin. The stage cost $\ell(x,u)$ must be continuous and positive definite.

2.  **Existence of a Terminal Triplet $(\mathcal{X}_f, \kappa_f, V_f)$**: There must exist a [terminal set](@entry_id:163892) $\mathcal{X}_f$, a terminal control law $\kappa_f(x)$, and a terminal cost function $V_f(x)$ that collectively satisfy two critical conditions for all $x \in \mathcal{X}_f$:
    *   **Control Invariance**: The terminal controller must be admissible ($\kappa_f(x) \in \mathcal{U}$) and render the [terminal set](@entry_id:163892) positively invariant ($f(x, \kappa_f(x)) \in \mathcal{X}_f$). This ensures [recursive feasibility](@entry_id:167169).
    *   **CLF Decrease Condition**: The terminal cost $V_f$ must be a Control Lyapunov Function, satisfying $V_f(f(x, \kappa_f(x))) - V_f(x) \le -\ell(x, \kappa_f(x))$. This ensures stability.

If these conditions are met, then for any initial state $x_0$ within the $N$-step feasible set $\mathcal{X}_N$, the MPC controller is guaranteed to be recursively feasible and will drive the system state asymptotically to the origin.

### On the Practical Design of Terminal Ingredients

The theoretical framework provides clear requirements for the terminal ingredients. The final step is to design them in practice. For Linear Time-Invariant (LTI) systems $x_{k+1} = Ax_k+Bu_k$ with quadratic costs $\ell(x,u) = x^\top Q x + u^\top R u$, this design can be made systematic.

#### Designing the Terminal Set $\mathcal{X}_f$

The [terminal set](@entry_id:163892) $\mathcal{X}_f$ is typically chosen as an [ellipsoid](@entry_id:165811), $\mathcal{X}_f = \{x \mid x^\top P x \le \alpha\}$, where $P \succ 0$ is a [positive definite matrix](@entry_id:150869). This set must be contained within the state and input constraint regions. For example, if we have polytopic constraints like $|x_1| \le \bar{x}_1$ and $|u_1| \le \bar{u}_1$, we need to find the largest $\alpha$ such that the [ellipsoid](@entry_id:165811) satisfies these constraints.

The maximum value of any linear function $c^\top x$ over the ellipsoid $x^\top P x \le \alpha$ is given by $\sqrt{\alpha c^\top P^{-1} c}$. This allows us to convert set inclusion constraints into algebraic inequalities. For example, to satisfy $|x_1| \le \bar{x}_1$, which is equivalent to $|\begin{pmatrix} 1  0  \dots \end{pmatrix} x| \le \bar{x}_1$, we must enforce $\sqrt{\alpha c_1^\top P^{-1} c_1} \le \bar{x}_1$, where $c_1 = [1, 0, \dots]^\top$. Similarly, for an input constraint $|k_1^\top x| \le \bar{u}_1$ (where $k_1^\top$ is a row of the terminal controller matrix $K$), we must enforce $\sqrt{\alpha k_1^\top P^{-1} k_1} \le \bar{u}_1$. By solving these inequalities for $\alpha$ for all state and input constraints, we find the largest possible ellipsoid for a given $P$ [@problem_id:2746612].

#### Designing the Terminal Cost $V_f$ and Controller $\kappa_f$

For LTI systems, a powerful and systematic choice for the terminal cost $V_f(x) = x^\top P x$ and controller $\kappa_f(x) = Kx$ comes from the solution to the infinite-horizon Linear Quadratic Regulator (LQR) problem. The LQR controller for the cost $\sum (x_k^\top Q x_k + u_k^\top R u_k)$ is given by the gain $K = -(R+B^\top P B)^{-1}B^\top PA$, where $P$ is the unique positive definite solution to the **Discrete-time Algebraic Riccati Equation (DARE)**:
$$
P = A^\top P A - (A^\top P B)(R+B^\top P B)^{-1}(B^\top P A) + Q
$$
This equation can be rearranged to:
$$
(A+BK)^\top P (A+BK) - P = -Q - K^\top R K
$$
Multiplying by $x^\top$ and $x$, this becomes $V_f((A+BK)x) - V_f(x) = -\ell(x, Kx)$. This shows that the DARE solution $P$ and LQR gain $K$ automatically satisfy the CLF decrease condition *with equality*, and this condition holds *globally* for all $x \in \mathbb{R}^n$ [@problem_id:2746567].

This is a profound result. By choosing the terminal cost and controller from the LQR problem associated with the MPC's stage cost, the CLF condition is automatically satisfied everywhere. The only remaining task is to find the largest positively invariant ellipsoid that also satisfies the state and input constraints. This choice of $P$ and $K$ allows for the largest possible [terminal set](@entry_id:163892) $\mathcal{X}_f$, and consequently, the largest possible [domain of attraction](@entry_id:174948) for the MPC controller. Using a "hand-tuned" matrix $\tilde{P}$ that is not the DARE solution will typically only satisfy the CLF condition on a smaller, local region, thus restricting the size of the [terminal set](@entry_id:163892) and shrinking the MPC's guaranteed region of stability [@problem_id:2746567].