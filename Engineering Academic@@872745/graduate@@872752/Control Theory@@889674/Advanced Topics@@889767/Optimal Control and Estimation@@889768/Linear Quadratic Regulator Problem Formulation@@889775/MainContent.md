## Introduction
The Linear Quadratic Regulator (LQR) represents a cornerstone of modern optimal control theory, offering a powerful and systematic framework for designing feedback controllers. It addresses the fundamental challenge of driving a linear system's state to zero while minimizing a performance cost that balances regulation accuracy against control energy expenditure. The elegance of the LQR solution lies in its ability to yield an optimal, stable, and robust controller through a well-defined mathematical procedure.

This article provides a comprehensive exploration of the LQR problem, structured to build from foundational principles to advanced applications. The first chapter, **"Principles and Mechanisms,"** delves into the core mathematical setup, explaining the quadratic [cost functional](@entry_id:268062), the significance of the weighting matrices Q and R, and the critical system-theoretic conditions of [stabilizability and detectability](@entry_id:176335). It culminates in the derivation of the celebrated Riccati equation, the mechanism for computing the [optimal control](@entry_id:138479) law. Building on this foundation, the second chapter, **"Applications and Interdisciplinary Connections,"** reveals the versatility of LQR by extending it to solve practical problems like output tracking and [stochastic control](@entry_id:170804) (LQG), and explores its profound connections to modern paradigms such as Model Predictive Control (MPC) and adaptive systems. Finally, the **"Hands-On Practices"** section provides a set of targeted problems to solidify theoretical understanding through concrete calculation and simulation.

## Principles and Mechanisms

The Linear Quadratic Regulator (LQR) is a cornerstone of modern control theory, providing a systematic method for designing optimal feedback controllers for [linear systems](@entry_id:147850). The "optimality" is defined with respect to a quadratic performance index, or [cost functional](@entry_id:268062), which balances the objectives of regulating the system's state against the expenditure of control effort. This chapter elucidates the fundamental principles underlying the formulation of the LQR problem and the mechanisms through which its solution is derived.

### The Core Problem Formulation

At its heart, the LQR framework addresses the challenge of controlling a linear time-invariant (LTI) system to achieve a desired objective with minimal cost. We begin by examining the canonical infinite-horizon LQR problem, which forms the basis for many practical applications.

Consider a continuous-time LTI system whose evolution is described by the state-space equation:
$$
\dot{x}(t) = A x(t) + B u(t)
$$
where $x(t) \in \mathbb{R}^{n}$ is the state vector, $u(t) \in \mathbb{R}^{m}$ is the control input vector, and $A$ and $B$ are constant matrices of appropriate dimensions. The objective is to design a control law that minimizes the infinite-horizon quadratic [cost functional](@entry_id:268062):
$$
J = \int_{0}^{\infty} \left( x(t)^{\top} Q x(t) + u(t)^{\top} R u(t) \right) dt
$$
This [cost functional](@entry_id:268062) integrates two critical terms over an infinite time horizon: the state penalty $x(t)^{\top} Q x(t)$ and the control penalty $u(t)^{\top} R u(t)$. The matrices $Q$ and $R$ are known as **weighting matrices**, and their selection is a crucial aspect of the engineering design process.

#### The Role of the Weighting Matrices Q and R

The structure of the [cost functional](@entry_id:268062) $J$ is not arbitrary. The specific properties of the weighting matrices $Q$ and $R$ are chosen to ensure the optimization problem is mathematically well-posed and physically meaningful. For any quadratic form $v^{\top}Mv$, its value depends only on the symmetric part of the matrix $M$, since $v^{\top}Mv = v^{\top}\left(\frac{M+M^{\top}}{2}\right)v$. Therefore, without loss of generality, we assume $Q$ and $R$ are symmetric matrices. The standard assumptions for the LQR problem are:

1.  **State Weighting Matrix:** $Q$ is symmetric and **positive semidefinite** ($Q = Q^{\top} \succeq 0$).
2.  **Control Weighting Matrix:** $R$ is symmetric and **positive definite** ($R = R^{\top} \succ 0$).

These assumptions are critical for three fundamental properties of the [cost functional](@entry_id:268062) [@problem_id:2719928] [@problem_id:2719906]:

*   **Non-negativity:** The [cost functional](@entry_id:268062) must be bounded below to have a meaningful minimum. The condition $Q \succeq 0$ ensures that $x^{\top}Qx \ge 0$, and $R \succ 0$ implies $u^{\top}Ru \ge 0$. Consequently, the integrand is always non-negative, and the total cost $J$ is guaranteed to be in the range $[0, \infty]$.

*   **Convexity:** The LQR problem is an optimization problem over the space of admissible control functions. For this problem to be tractable and have a unique global minimum, the [cost functional](@entry_id:268062) $J$ should be a [convex function](@entry_id:143191) of the control input $u$. Because the state $x(t)$ depends linearly on the history of $u(\tau)$ for $\tau  t$, the entire cost $J$ becomes a convex functional of the control history if the integrand is a [convex function](@entry_id:143191) of the pair $(x, u)$. This is guaranteed if $Q \succeq 0$ and $R \succeq 0$.

*   **Strict Convexity and Uniqueness:** To ensure the [optimal control](@entry_id:138479) is unique, we require a stronger condition: the [cost functional](@entry_id:268062) must be strictly convex with respect to the control input. The term $u^{\top}Ru$ is strictly convex in $u$ if and only if $R$ is positive definite ($R \succ 0$). Since the term involving $Q$ is convex, the sum is strictly convex in $u$, which guarantees that if a minimizer exists, it is unique [@problem_id:2719932]. The condition $R \succ 0$ also implies that any non-zero control input incurs a positive cost, which is a physically realistic assumption.

Furthermore, the requirement $R \succ 0$ ensures a property known as **coercivity** in the control input [@problem_id:2719979]. This means the cost grows unboundedly as the "size" of the control input grows. Specifically, we can establish a lower bound on the cost. Let $\lambda_{\min}(R) > 0$ be the [smallest eigenvalue](@entry_id:177333) of $R$. Then, for any vector $u$, $u^{\top}Ru \ge \lambda_{\min}(R) \|u\|^2$. Integrating this inequality and using the fact that the state penalty is non-negative, we get:
$$
J \ge \int_{0}^{\infty} u(t)^{\top} R u(t) \, dt \ge \lambda_{\min}(R) \int_{0}^{\infty} \|u(t)\|^2 \, dt = \lambda_{\min}(R) \|u\|_{L^2}^2
$$
This inequality shows that an infinite control effort (an infinite $L^2$ norm) necessarily leads to an infinite cost, which prevents pathological solutions where the controller applies enormous, unbounded inputs.

#### The Physical Interpretation: The Q-R Trade-off

The choice of $Q$ and $R$ encodes the trade-off between competing performance objectives: the speed of state regulation versus the magnitude of control effort. Adjusting the relative "size" of these matrices allows the designer to shape the behavior of the closed-loop system [@problem_id:2719953].

*   **Increasing State Penalty (large $Q$):** If we increase the elements of $Q$ relative to $R$, we are placing a higher penalty on state deviations from the origin. To minimize the cost, the optimal controller will become more "aggressive." It will apply larger control inputs to drive the state to zero more quickly. This results in a faster response but consumes more control energy.

*   **Increasing Control Penalty (large $R$):** Conversely, if we increase the elements of $R$ relative to $Q$, we make control action more "expensive." The optimal controller will become more "conservative," using smaller control inputs to avoid a high penalty. This results in a slower, more sluggish response but is more efficient in terms of control effort.

A crucial insight is that the optimal control law depends only on the *ratio* of the penalties, not their absolute values. If we scale both $Q$ and $R$ by the same positive constant $\sigma > 0$, the new cost is simply $\sigma J$. Minimizing $\sigma J$ is equivalent to minimizing $J$, so the optimal control law remains unchanged. Only the numerical value of the optimal cost is scaled by $\sigma$ [@problem_id:2719953].

#### Discrete-Time and Finite-Horizon Formulations

The LQR problem can be formulated in various settings. The **discrete-time LQR problem** considers a system evolving in [discrete time](@entry_id:637509) steps, $x_{k+1} = Ax_k + Bu_k$. The [cost functional](@entry_id:268062) becomes a summation:
$$
J = \sum_{k=0}^{\infty} \left( x_k^{\top} Q x_k + u_k^{\top} R u_k \right)
$$
The same principles regarding the weighting matrices apply: $Q \succeq 0$ and $R \succ 0$ are the standard assumptions to ensure the problem is well-posed with a unique minimizing control sequence [@problem_id:2719932].

For problems defined over a **finite horizon** $[0, T]$, it is natural to add a **terminal cost** to penalize the final state $x(T)$. The [cost functional](@entry_id:268062) for a continuous-time finite-[horizon problem](@entry_id:161031) is:
$$
J = x(T)^{\top} S x(T) + \int_{0}^{T} \left( x(t)^{\top} Q x(t) + u(t)^{\top} R u(t) \right) dt
$$
Here, $S$ is a symmetric positive semidefinite terminal weighting matrix ($S \succeq 0$). Adding this terminal cost is essential for two reasons [@problem_id:2719946] [@problem_id:2719914]. First, it provides a well-defined objective for the final state, which is necessary to initialize the backward-in-time solution process. Second, it preserves the quadratic structure of the problem, ensuring the solution remains computationally tractable. In many cases, the horizon $T$ is an approximation of a much longer process; the terminal cost can then be chosen to represent the optimal cost-to-go from time $T$ onward, effectively linking the finite-horizon solution to its infinite-horizon counterpart.

### System-Theoretic Prerequisites for Stability

The goal of the LQR is not just to find a control law that minimizes $J$, but one that also results in a stable closed-loop system. The existence of such a stabilizing optimal controller is not guaranteed for all systems; it depends on fundamental structural properties of the system matrices $A$ and $B$, and their relationship with the [cost matrix](@entry_id:634848) $Q$.

#### Stabilizability: Can the Control Input Influence Unstable States?

A linear system is **controllable** if it is possible to steer the state from any initial point to any final point in finite time using the control input. A weaker but more crucial property for LQR is **[stabilizability](@entry_id:178956)**. The pair $(A,B)$ is stabilizable if any unstable mode of the system can be influenced by the control input [@problem_id:2719944]. More formally, a system is stabilizable if all eigenvalues of $A$ with non-negative real parts are controllable.

Stabilizability of $(A,B)$ is a **necessary condition** for the existence of a stabilizing LQR solution. The reasoning is fundamental: the control input $u$ affects the state dynamics through the term $Bu$. The resulting feedback law, $u = -Kx$, modifies the system dynamics to $\dot{x} = (A - BK)x$. A fundamental result of [linear systems theory](@entry_id:172825) is that [state feedback](@entry_id:151441) cannot change the location of uncontrollable eigenvalues. If the system has an unstable eigenvalue that is uncontrollable, this eigenvalue will remain an eigenvalue of the closed-loop matrix $A-BK$ for any choice of gain $K$. The system will remain unstable regardless of the control law. The LQR framework, being a method to find an optimal *stabilizing* controller, cannot overcome this intrinsic structural limitation. This requirement is independent of the choice of $Q$ and $R$ [@problem_id:2719944] [@problem_id:2719946].

#### Detectability: Can the Cost Function "See" Unstable States?

The dual concept to [stabilizability](@entry_id:178956) is **detectability**. A system mode is unobservable if its behavior does not appear in the system's output. In the LQR context, the "output" is implicitly defined by the state penalty term, $y(t) = Q^{1/2}x(t)$, where $Q^{1/2}$ is a square root of $Q$ such that $Q = (Q^{1/2})^{\top}Q^{1/2}$. The pair $(A, Q^{1/2})$ is **detectable** if any unstable mode of the system is observable through this output [@problem_id:2719974].

Detectability of $(A, Q^{1/2})$ is also a **necessary condition** for obtaining a stabilizing LQR solution. The intuition relates to the controller's "incentive." Suppose the system has an unstable mode corresponding to an eigenvalue $\lambda$ with $\text{Re}(\lambda) \ge 0$. If this mode is unobservable by the [cost function](@entry_id:138681), it means there exists a corresponding eigenvector $v$ such that $Q^{1/2}v = 0$, and thus $v^{\top}Qv=0$. A trajectory along this eigenvector, $x(t) = e^{\lambda t}v$, would be unstable but would contribute nothing to the state-penalty portion of the [cost functional](@entry_id:268062). An optimal controller, seeking to minimize cost, would have no incentive to expend energy to suppress this unstable state. The optimal action would be to apply zero control, leading to a minimal cost of zero but an unstable, divergent state trajectory. The detectability condition precisely rules out this pathological scenario, ensuring that any unstable behavior is penalized by the [cost function](@entry_id:138681) and will therefore be acted upon by the controller [@problem_id:2719974].

In summary, the cornerstone [existence theorem](@entry_id:158097) of LQR states that for the infinite-[horizon problem](@entry_id:161031) with weighting matrices $Q \succeq 0$ and $R \succ 0$, a unique, positive semidefinite, stabilizing solution exists if and only if the pair $(A, B)$ is stabilizable and the pair $(A, Q^{1/2})$ is detectable [@problem_id:2719974].

### The Mechanism of Optimal Control: The Riccati Equation

Having established the problem formulation and its prerequisites, we now turn to the mechanism for finding the optimal control law. The solution emerges from the theory of dynamic programming and leads to the celebrated Riccati equation.

#### The Infinite-Horizon Solution and the Algebraic Riccati Equation (ARE)

For the infinite-horizon LTI problem, the [optimal control](@entry_id:138479) law is a constant **linear state-feedback law**:
$$
u(t) = -K x(t)
$$
The optimal gain matrix $K$ is found through the solution of the **Algebraic Riccati Equation (ARE)**. The derivation can be shown elegantly using the Hamilton-Jacobi-Bellman (HJB) equation, a fundamental result in optimal control [@problem_id:2719933].

We begin by positing that the optimal cost-to-go from a state $x$, known as the value function, is a quadratic function of the state: $V(x) = x^{\top} P x$, where $P$ is a symmetric, [positive semidefinite matrix](@entry_id:155134) to be determined. The HJB equation for the infinite-[horizon problem](@entry_id:161031) states that the optimal cost must satisfy:
$$
0 = \min_{u} \left\{ x^{\top} Q x + u^{\top} R u + \nabla V(x)^{\top} (A x + B u) \right\}
$$
With $V(x) = x^{\top} P x$, the gradient is $\nabla V(x) = 2Px$. The expression to be minimized, the Hamiltonian, becomes $x^{\top} Q x + u^{\top} R u + 2x^{\top}P(Ax+Bu)$. To find the minimizing control $u^{\star}$, we differentiate with respect to $u$ and set the result to zero:
$$
\frac{\partial}{\partial u} (\dots) = 2Ru + 2B^{\top}Px = 0
$$
Since $R \succ 0$, we can solve for $u^{\star}$:
$$
u^{\star}(t) = -R^{-1} B^{\top} P x(t)
$$
This gives the structure of the optimal feedback gain as $K = R^{-1} B^{\top} P$. Substituting this optimal control back into the HJB equation and requiring it to hold for all $x$ yields the **continuous-time Algebraic Riccati Equation (ARE)** for the unknown matrix $P$:
$$
A^{\top} P + PA - P B R^{-1} B^{\top} P + Q = 0
$$
The [stabilizability and detectability](@entry_id:176335) conditions guarantee that there is a unique, symmetric, positive semidefinite solution $P$ to this equation that results in a stable closed-loop [system matrix](@entry_id:172230) $A-BK$. This stabilizing solution is the one used to compute the optimal LQR gain. An alternative and equally valid derivation involves a "completing the square" argument on the [cost functional](@entry_id:268062)'s integrand [@problem_id:2719933].

#### The Finite-Horizon Solution and the Differential Riccati Equation (DRE)

In the finite-horizon case, the optimal strategy depends on the time remaining until the terminal time $T$. Consequently, the optimal [feedback gain](@entry_id:271155) becomes time-varying, $u(t) = -K(t)x(t)$ [@problem_id:2719914]. The matrix $P$ in the value function $V(x,t) = x^{\top}P(t)x$ also becomes time-dependent. Applying the same HJB procedure results not in an algebraic equation, but in a matrix differential equation known as the **Differential Riccati Equation (DRE)**:
$$
-\dot{P}(t) = A^{\top} P(t) + P(t) A - P(t) B R^{-1} B^{\top} P(t) + Q
$$
This equation is solved backward in time from the terminal boundary condition imposed by the terminal cost: $P(T) = S$. The solution $P(t)$ for $t  T$ is then used to find the time-varying optimal gain $K(t) = R^{-1} B^{\top} P(t)$. The time-dependence of the gain reflects the controller's changing strategy as the end of the horizon approaches.

### An Extension: The Cross-Term Formulation

The standard LQR formulation can be generalized to include a cross-term in the [cost functional](@entry_id:268062):
$$
J = \int_{0}^{\infty} \left( x^{\top}Qx + 2x^{\top}Su + u^{\top}Ru \right) dt
$$
This form can be useful in certain applications where there is a direct coupling between state and control in the performance objective. The analysis of this problem follows similar principles [@problem_id:2719910]. For the integrand to be jointly convex in the combined vector $(x,u)$, it is necessary and sufficient that the [block matrix](@entry_id:148435) representing the quadratic form be positive semidefinite:
$$
\begin{pmatrix} Q  S \\ S^{\top}  R \end{pmatrix} \succeq 0
$$
This condition implies $Q \succeq 0$ and $R \succeq 0$. The presence of the cross-term modifies the ARE and the optimal gain formula, but the fundamental principles of dynamic programming and the structural requirements of convexity, [stabilizability](@entry_id:178956), and detectability remain the guiding pillars of the solution.