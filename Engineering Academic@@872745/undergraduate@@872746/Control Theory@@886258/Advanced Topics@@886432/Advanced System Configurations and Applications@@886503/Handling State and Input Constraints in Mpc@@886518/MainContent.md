## Introduction
Model Predictive Control (MPC) stands apart from many classical control strategies due to its inherent ability to respect the physical and operational limits of a system. Where traditional methods often require separate, ad-hoc logic to handle [actuator saturation](@entry_id:274581) or state limitations, MPC integrates these constraints directly into its core predictive optimization framework. This allows the controller to proactively plan future actions, foreseeing and avoiding potential violations. However, this powerful capability introduces a critical challenge: the risk of infeasibility, where the controller fails to find any valid plan that satisfies all constraints. This article provides a comprehensive guide to mastering [constrained control](@entry_id:263479) in MPC. It begins by laying out the fundamental principles for formulating constraints and ensuring controller feasibility. It then showcases the versatility of these techniques through a wide range of interdisciplinary applications. Finally, it offers hands-on practice to solidify these concepts, equipping you with the skills to design robust and reliable predictive controllers. The journey starts in the first chapter, **Principles and Mechanisms**, which details how physical limits are translated into mathematical language for the MPC optimizer. This is followed by **Applications and Interdisciplinary Connections**, demonstrating how [constrained control](@entry_id:263479) solves real-world problems from robotics to biomedicine. The final chapter, **Hands-On Practices**, provides opportunities to apply these theories.

## Principles and Mechanisms

A defining feature of Model Predictive Control (MPC) is its innate ability to handle constraints on system inputs and states. Unlike classical control methods that often require ad-hoc [anti-windup schemes](@entry_id:267727) or saturation logic, MPC incorporates constraints directly into the formulation of its underlying optimization problem. This allows the controller to proactively plan future actions to avoid constraint violations, respecting the physical and operational limits of the system. This chapter delves into the principles and mechanisms for formulating these constraints, explores the critical challenge of ensuring controller feasibility, and presents standard techniques for achieving robust and reliable [constrained control](@entry_id:263479).

### Formulating Constraints for the MPC Problem

At its core, the MPC algorithm solves a [constrained optimization](@entry_id:145264) problem at each sampling instant. For [linear systems](@entry_id:147850) with quadratic cost functions, this problem is typically a **Quadratic Program (QP)**. Standard QP solvers are designed to handle constraints written in a specific [linear matrix inequality](@entry_id:174484) form. Consequently, a crucial first step in designing an MPC controller is to translate all physical and operational limits into this canonical format.

#### Basic Input and State Constraints

The most common constraints are simple [upper and lower bounds](@entry_id:273322) on individual input or state variables. These are often called "[box constraints](@entry_id:746959)". Consider a control input $u_k$ that must remain within a given range, $u_{min} \le u_k \le u_{max}$. This single condition is equivalent to two simultaneous linear inequalities: $u_k \le u_{max}$ and $-u_k \le -u_{min}$.

In the MPC optimization, the decision variable is the entire sequence of future control inputs over the [prediction horizon](@entry_id:261473) $N_p$, denoted by the vector $\mathbf{U} = [u_{k|k}, u_{k+1|k}, \dots, u_{k+N_p-1|k}]^T$. To enforce the input bound for every element in this sequence, we must stack these inequalities for each future time step. For a hypothetical DC motor where the input voltage $u$ is limited by a power supply, $V_{min} \le u \le V_{max}$, with a [prediction horizon](@entry_id:261473) of $N_p=2$, the control vector is $\mathbf{U} = [u_{k|k}, u_{k+1|k}]^T$. The constraints are:
1.  $u_{k|k} \le V_{max}$
2.  $-u_{k|k} \le -V_{min}$
3.  $u_{k+1|k} \le V_{max}$
4.  $-u_{k+1|k} \le -V_{min}$

These can be expressed compactly in the standard form $M\mathbf{U} \le \mathbf{p}$ by defining the matrix $M$ and vector $\mathbf{p}$ as follows [@problem_id:1579666]:
$$
M = \begin{pmatrix}
1  0 \\
-1  0 \\
0  1 \\
0  -1
\end{pmatrix}, \quad
\mathbf{p} = \begin{pmatrix}
V_{max} \\
-V_{min} \\
V_{max} \\
-V_{min}
\end{pmatrix}
$$
Each row of the [matrix inequality](@entry_id:181828) $M\mathbf{U} \le \mathbf{p}$ corresponds to one of the individual scalar inequalities.

State constraints are formulated in an identical manner. For a system with [state vector](@entry_id:154607) $x(k)$, a general linear state constraint is written as $M_x x(k) \le d$. For instance, if a satellite's pointing error $\theta(k)$, the first component of its [state vector](@entry_id:154607) $x(k) = [\theta(k), \omega(k)]^T$, must be kept within a tolerance $|\theta(k)| \le \theta_{max}$, we can rewrite this absolute value constraint as two linear inequalities: $\theta(k) \le \theta_{max}$ and $-\theta(k) \le \theta_{max}$. These are then translated into the matrix form $M x(k) \le d$ [@problem_id:1579658]:
$$
\begin{pmatrix} 1  0 \\ -1  0 \end{pmatrix}
\begin{pmatrix} \theta(k) \\ \omega(k) \end{pmatrix}
\le
\begin{pmatrix} \theta_{max} \\ \theta_{max} \end{pmatrix}
$$
These constraints are then imposed on the predicted state trajectory at each step in the horizon, forming a larger set of linear inequalities for the optimization problem.

#### Handling Complex Constraints via State Augmentation

Not all practical constraints are simple bounds on states or inputs. A common and important constraint in many mechanical and electrical systems is a limit on the **rate of change** of the control input, i.e., $|\dot{u}(t)| \le \dot{u}_{max}$. In discrete time, this is approximated as $|u_k - u_{k-1}| \le \Delta u_{max}$. This constraint is problematic because it couples the input at the current step, $u_k$, with the input from the previous step, $u_{k-1}$, which is a fixed value and not part of the optimization's decision variables.

A powerful technique to handle such constraints is **[state augmentation](@entry_id:140869)**. The core idea is to redefine the system's state and input to absorb the problematic [constraint dynamics](@entry_id:747773). To handle an input rate constraint, we can augment the state vector $\mathbf{x}_k$ with the previous input, defining a new [state vector](@entry_id:154607) $\mathbf{z}_k = [\mathbf{x}_k^T, u_{k-1}]^T$. The new control input is defined as the change in the actuator signal, $v_k = u_k - u_{k-1}$.

Let the original system be $\mathbf{x}_{k+1} = A \mathbf{x}_k + B u_k$. We can rewrite this using the new variables. Since $u_k = u_{k-1} + v_k$, the original dynamics become $\mathbf{x}_{k+1} = A \mathbf{x}_k + B (u_{k-1} + v_k) = A \mathbf{x}_k + B u_{k-1} + B v_k$. The dynamics of the augmented part of the state are simply $u_k = u_{k-1} + v_k$. Combining these gives the new augmented system $\mathbf{z}_{k+1} = \tilde{A} \mathbf{z}_k + \tilde{B} v_k$, where [@problem_id:1579628]:
$$
\tilde{A} = \begin{pmatrix} A  B \\ \mathbf{0}^T  1 \end{pmatrix}, \quad
\tilde{B} = \begin{pmatrix} B \\ 1 \end{pmatrix}
$$
The benefit of this transformation is that the input rate constraint $|u_k - u_{k-1}| \le \Delta u_{max}$ becomes a simple magnitude constraint on the new input: $|v_k| \le \Delta u_{max}$. However, this comes at a cost. The original input magnitude constraint, $|u_k| \le u_{max}$, now becomes a coupled constraint on the new state and input: $|u_{k-1} + v_k| \le u_{max}$. In the augmented framework, this is a constraint of the form $|C\mathbf{z}_k + D v_k| \le u_{max}$, which is still a linear constraint suitable for QP solvers. This technique is indispensable for handling rate constraints, slew rate limits, and other dynamic actuator limitations.

### The Challenge of Feasibility in MPC

The greatest strength of MPC—its ability to handle hard constraints—is also the source of its primary failure mode: **infeasibility**. An MPC problem is deemed infeasible if the optimization solver cannot find any sequence of control inputs that satisfies all specified constraints over the [prediction horizon](@entry_id:261473). When this occurs, the controller has no valid control action to apply, which can lead to system failure. Understanding the sources of infeasibility is critical to designing reliable controllers.

#### Sources of Infeasibility

Infeasibility can arise from several conditions. The most straightforward cause is a direct violation of a hard state constraint by the current measured state of the system. If an MPC is configured with a hard state constraint $x_k \le x_{max}$ for all steps $k$ in the horizon, this includes the current step, $k=0$. The state at the current step, $x(0|t) = x_t$, is a fixed parameter in the optimization problem, not a variable to be chosen. If the measured state $x_t$ already violates the constraint (e.g., $x_t > x_{max}$), then no possible control sequence can remedy this fact. The set of feasible solutions is empty from the outset [@problem_id:1579679]. This situation can occur if a large, unexpected disturbance pushes the system into a forbidden region of the state space.

A more subtle source of infeasibility arises from the controller's limited foresight. A finite [prediction horizon](@entry_id:261473) $N$ means the controller is "myopic"; it only plans for events within the next $N$ steps. Consider an autonomous vehicle using MPC to brake before an obstacle. The controller is subject to an input constraint (maximum braking deceleration) and a state constraint (vehicle position must be less than the obstacle position). If the [prediction horizon](@entry_id:261473) is very short, the controller may not initiate braking early enough because the predicted collision is beyond its planning window. By the time the obstacle enters the horizon, the vehicle may have reached a combination of position and velocity from which it is physically impossible to stop before the obstacle, given the maximum braking available. Even though the vehicle is not yet at the obstacle, no valid sequence of control inputs *over the limited horizon* can prevent the *predicted* trajectory from violating the state constraint. The problem becomes infeasible because the controller has "painted itself into a corner" [@problem_id:1579651].

#### The Recursive Feasibility Problem

The scenario described above is a manifestation of a fundamental issue in standard MPC: the lack of guaranteed **[recursive feasibility](@entry_id:167169)**. This means that even if a [feasible solution](@entry_id:634783) is found at the current time step $k$, there is no inherent guarantee that a [feasible solution](@entry_id:634783) will exist at the next time step, $k+1$.

The root cause lies in the [receding horizon](@entry_id:181425) mechanism. At time $k$, the MPC solves for an optimal control sequence $\{u^*(0|k), \dots, u^*(N-1|k)\}$. It applies only the first action, $u^*(0|k)$, causing the system to transition to state $x_{k+1}$. While the full plan from time $k$ was feasible, the tail of that plan, $\{u^*(1|k), \dots, u^*(N-1|k)\}$, is not necessarily optimal for the new problem starting from state $x_{k+1}$. The optimizer at time $k$ is free to choose an initial action $u^*(0|k)$ that, while optimal for its $N$-step view, steers the system into a state $x_{k+1}$ from which the feasible set for the next optimization problem (at time $k+1$) is empty [@problem_id:1579662]. Without specific safeguards, the controller may choose a short-term optimal action that leads to long-term infeasibility.

### Techniques for Ensuring Feasible and Robust Operation

Given the critical nature of feasibility, several techniques have been developed to either prevent infeasibility or gracefully handle constraint violations. These methods are essential for deploying MPC in real-world applications where reliability is paramount.

#### Soft Constraints

The most common and practical method for avoiding infeasibility is to relax hard constraints, turning them into **soft constraints**. Instead of rigidly forbidding [constraint violation](@entry_id:747776), this approach allows violations but adds a penalty to the [objective function](@entry_id:267263), encouraging the controller to minimize them.

This is implemented by introducing non-negative **[slack variables](@entry_id:268374)**, typically denoted by $\epsilon_k \ge 0$. A hard state constraint, such as $x_k \le x_{max}$, is replaced with a softened version: $x_k \le x_{max} + \epsilon_k$. The [slack variable](@entry_id:270695) $\epsilon_k$ represents the amount of violation. To discourage this violation, a penalty term is added to the MPC's [objective function](@entry_id:267263). For a [quadratic program](@entry_id:164217), a [quadratic penalty](@entry_id:637777) is natural. If the original objective function over a horizon $N$ was $J = V_f(x_N) + \sum_{k=0}^{N-1} (x_k^T Q x_k + u_k^T R u_k)$, the new objective becomes [@problem_id:1579625] [@problem_id:1579644]:
$$
J_{soft} = V_f(x_N) + \sum_{k=0}^{N-1} (x_k^T Q x_k + u_k^T R u_k) + \sum_{k=1}^{N} \rho_k \epsilon_k^2
$$
The [slack variables](@entry_id:268374) $\epsilon_k$ become additional decision variables in the optimization, subject to the constraint $\epsilon_k \ge 0$. The penalty weight $\rho_k$ is a large positive value chosen by the designer. A very large $\rho_k$ makes the constraint "harder," as the optimizer will incur a high cost for even small violations. By allowing for non-zero slack, the optimization problem remains feasible even if the state enters a region where the original hard constraint cannot be satisfied. The controller will find the best possible action that minimizes the [constraint violation](@entry_id:747776).

#### Guaranteeing Recursive Feasibility: Terminal Constraints

While soft constraints provide a practical fix, a more rigorous method to guarantee [recursive feasibility](@entry_id:167169) involves adding a **[terminal constraint](@entry_id:176488)** to the MPC problem. This approach ensures that the optimization at time $k$ will always produce a plan that contains within it a seed for a feasible plan at time $k+1$.

The key ingredient is a pre-computed **[terminal set](@entry_id:163892)**, $\mathcal{X}_f$. This set has two crucial properties:
1.  Any state within it satisfies the [state constraints](@entry_id:271616): $\mathcal{X}_f \subseteq \mathcal{X}$.
2.  It is a **control [invariant set](@entry_id:276733)**. This means that for any state $\tilde{x} \in \mathcal{X}_f$, there exists a control input $\tilde{u} \in \mathcal{U}$ (often given by a simple local controller, $\tilde{u} = K\tilde{x}$) such that the resulting state $A\tilde{x} + B\tilde{u}$ is also in $\mathcal{X}_f$. In essence, once the system enters $\mathcal{X}_f$, it can be kept inside $\mathcal{X}_f$ forever without violating constraints.

The MPC problem is then formulated with an additional constraint that the final predicted state must lie within this set: $x(N|t) \in \mathcal{X}_f$. The guarantee of [recursive feasibility](@entry_id:167169) is established by a "shift-and-append" argument [@problem_id:1579678]. Assume the problem is feasible at time $t$, yielding an optimal plan $\{x^*(0|t), \dots, x^*(N|t)\}$ and $\{u^*(0|t), \dots, u^*(N-1|t)\}$. The first control $u^*(0|t)$ is applied, leading to state $x_{t+1} = x^*(1|t)$.

To prove feasibility at time $t+1$, we only need to construct one feasible candidate solution. We can do this by shifting the optimal plan from time $t$: use $\{u^*(1|t), \dots, u^*(N-1|t)\}$ as the first $N-1$ inputs of the new plan. The resulting state trajectory will be $\{x^*(1|t), \dots, x^*(N|t)\}$, which we know satisfies all state and input constraints. The final state of this partial trajectory is $x^*(N|t)$, which, by the [terminal constraint](@entry_id:176488) at time $t$, is in $\mathcal{X}_f$. Because $\mathcal{X}_f$ is control invariant, we are guaranteed to find a final control input that keeps the new terminal state within $\mathcal{X}_f$. This constructed sequence is fully feasible for the problem at time $t+1$. Since at least one [feasible solution](@entry_id:634783) exists, the optimization problem is guaranteed to be feasible.

#### Robustness to Uncertainty: Constraint Tightening

The methods discussed so far assume a perfect model of the system. In reality, all systems are subject to uncertainties and disturbances. Consider a system with bounded additive disturbances: $x_{k+1} = A x_k + B u_k + d w_k$, where the disturbance $w_k$ is unknown but bounded, $|w_k| \le w_{max}$.

Standard MPC plans for the nominal system (assuming $w_k=0$). However, the true state will deviate from the nominal prediction due to the disturbance. To guarantee that the *true* state satisfies a constraint, e.g., $h^T x_k \le g$, we must be more conservative with our plan for the *nominal* state. This is achieved through **[constraint tightening](@entry_id:174986)**.

The idea is to compute the maximum possible deviation between the true state and the nominal state at each step of the horizon, and then tighten the original constraint by that amount. The error between the true and nominal state, $e_k = x_k - x_{nom, k}$, propagates according to $e_{k+1} = A e_k + d w_k$, starting with $e_0=0$. After $N$ steps, the total error is $e_N = \sum_{i=0}^{N-1} A^{N-1-i} d w_i$.

The constraint on the true state is $h^T x_N \le g$. Substituting $x_N = x_{nom,N} + e_N$, we get $h^T x_{nom,N} + h^T e_N \le g$. To guarantee this for any possible disturbance sequence, we must satisfy it for the [worst-case error](@entry_id:169595):
$$
h^T x_{nom,N} + \max_{|w_i| \le w_{max}} (h^T e_N) \le g
$$
This leads to a tightened constraint on the nominal state:
$$
h^T x_{nom,N} \le g - \max_{|w_i| \le w_{max}} \left( h^T \sum_{i=0}^{N-1} A^{N-1-i} d w_i \right)
$$
The maximum deviation term can be calculated offline. For a scalar disturbance, it simplifies to $w_{max} \sum_{i=0}^{N-1} |h^T A^{N-1-i} d|$. The new, tightened constraint for the nominal prediction, $h^T x_{nom,N} \le g_{tight}$, ensures that even under the worst possible sequence of disturbances, the true state will not violate the original constraint boundary $g$ [@problem_id:1579690]. This approach forms the basis of many robust MPC schemes, providing a rigorous way to maintain safety and performance in the presence of bounded uncertainty.